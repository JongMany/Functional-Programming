# filter

```ts
const products = [
  { name: '반팔티', price: 15_000 },
  { name: '긴팔티', price: 20_000 },
  { name: '핸드폰케이스', price: 15_000 },
  { name: '후드티', price: 30_000 },
  { name: '바지', price: 25_000 },
];
```

명령형 코드로 filtering 작업하기

```ts
const under20000 = [];
for (const item of products) {
  if (p.price < 20_000) {
    under2000.push(p);
  }
}

const over20000 = [];
for (const item of products) {
  if (p.price >= 20_000) {
    over20000.push(p);
  }
}
```

filter 함수로 리팩토링 하기

```ts
const filter = (fn, iterable) => {
  const results = [];
  for (const item of iterable) {
    if (fn(item)) {
      results.push(item);
    }
  }
  return results;
};

const under20000 = filter((prod) => prod.price < 20000, products);
const over20000 = filter((prod) => prod.price >= 20000, products);

const evens = filter((item) => item % 2 === 0, [1, 2, 3, 4]);
```
