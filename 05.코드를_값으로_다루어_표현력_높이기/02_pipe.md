# pipe

함수를 리턴하는 함수 (합성 함수를 만드는데 사용된다.)

```ts
const pipe =
  (...fns) =>
  (initialValue) => {
    return go(initialValue, ...fns);
  };

const f = pipe(
  (a) => a + 1,
  (a) => a + 10,
  (a) => a + 100,
);
```

인자를 2개 이상 받으려면, pipe 함수를 수정해야한다.

```ts
const pipe =
  (f1, ...fns) =>
  (...initialValue) => {
    return go(f1(...initialValue), ...fns);
  };
const f = pipe(
  (a, b) => a + b,
  (a) => a + 1,
  (a) => a + 100,
);

console.log(f(0, 1)); // 102
```
