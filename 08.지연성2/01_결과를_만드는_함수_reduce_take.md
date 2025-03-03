# 결과를 만드는 함수 reduce, take

`reduce`, `take`는 이터러블한 값들의 값을 꺼내어 결과를 만드는 함수다.

`map`, `filter`는 배열, 이터러블, 모나틱한 값의 원소들에게 함수를 합성하는 역할을 한다. -> 지연성을 가질 수 있다.

### reduce 예시) 객체로부터 queryString을 빼내는 함수

```ts
const getQueryString = (obj) =>
  go(
    obj,
    Object.entries,
    map(([k, v]) => `${k}=${v}`),
    reduce((acc, cur) => `${a}&${b}`),
  );

const getQueryString = pipe(
  Object.entries,
  map(([k, v]) => `${k}=${v}`),
  reduce((acc, cur) => `${a}&${b}`),
);

console.log(queryString({ limit: 10, offset: 10, type: 'notice' }));
```
