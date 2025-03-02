# reduce

reduce는 이터러블 값을 하나의 값으로 축약하는 함수

```ts
const nums = [1, 2, 3, 4, 5];
let total = 0;
for (const n of nums) {
  total += n;
}
```

reduce 함수로 리팩토링하기

```ts
const reduce = (fn, initialValue, iterable) => {
  let result = initialValue;
  for (const item of iterable) {
    result = fn(result, item);
  }
  return result;
};

const sum = reduce((acc, cur) => acc + cur, 0, nums); // 15
```

reduce 함수 고도화시키기

```ts
const reduce = (fn, initialValue, iterable) => {
  const iter = !iterable ? initialValue : iterable;
  const iterator = iter[Symbol.iterator]();
  let result = !iterable ? iterator.next().value : initialValue;

  for (const item of iterator) {
    console.log(item);
    result = fn(result, item);
  }
  return result;
};

const sum = reduce((acc, cur) => acc + cur, nums); // 15
```
