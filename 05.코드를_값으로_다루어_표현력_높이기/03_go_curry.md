# curry

함수를 값으로 다루면서 인자로 들어온 함수를 원하는 시점에 평가할 수 있음  
함수를 인자로 받아 함수를 리턴한다. 인자를 원하는 만큼 받은 후에 평가시킬 수 있다.

```ts
const curry =
  (f) =>
  (a, ...rest) => {
    console.log(a, rest);
    if (rest.length > 0) {
      return f(a, ...rest);
    } else {
      return (...rest) => f(a, ...rest);
    }
  };

const multi = curry((a, b) => a * b);
console.log(multi(1)(2)); // 2

const multi3 = multi(3);
```

### Go + Curry를 활용하여 리팩토링하기

As is

```ts
go(
  products,
  products => filter(p => p.price< 20_000, products)
  products => map(p => p.price, products),
  prices => reduce((acc, cur) => acc + cur, prices),
  console.log
);
```

To be

map, filter, reduce에 curry를 적용한다.

```ts
const map = curry((fn, iterable) => {
  const result = [];
  for (const item of iterable) {
    result.push(fn(item));
  }
  return result;
});

const filter = curry((fn, iterable) => {
  const results = [];
  for (const item of iterable) {
    if (fn(item)) {
      results.push(item);
    }
  }
  return results;
});

const reduce = curry((fn, initialValue, iterable) => {
  const iter = !iterable ? initialValue : iterable;
  const iterator = iter[Symbol.iterator]();
  let result = !iterable ? iterator.next().value : initialValue;

  for (const item of iterator) {
    result = fn(result, item);
  }
  return result;
});

go(
  products,
  (products) => filter((p) => p.price < 20_000)(products),
  (products) => map((p) => p.price)(products),
  (prices) => reduce((acc, cur) => acc + cur)(prices),
);

go(
  products,
  filter((p) => p.price < 20_000),
  map((p) => p.price)
  reduce((acc, cur) => acc + cur)
);
```
