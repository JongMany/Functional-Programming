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
    reduce((acc, cur) => `${acc}&${cur}`),
  );

const getQueryString = pipe(
  Object.entries,
  map(([k, v]) => `${k}=${v}`),
  reduce((acc, cur) => `${acc}&${cur}`),
);

console.log(queryString({ limit: 10, offset: 10, type: 'notice' }));
```

Join 함수로 리팩토링하기

```ts
const join = curry((separator = ',', iterable) => {
  reduce((acc, cur) => `${acc}${separator}${cur}`, iterator);
});

const getQueryString = pipe(
  Object.entries,
  map(([k, v]) => `${k}=${v}`),
  join('&'),
);

function* a() {
  yield 10;
  yield 20;
  yield 30;
  yield 40;
}
join(',', a()); // 10,20,30,40
```

L.map을 활용

```ts
L.entries = function* (obj){
  for (Const k in obj) {
    yield [k,obj[k]];
  }
}

const join = curry((separator = ',', iterable) => {
  reduce((acc, cur) => `${acc}${separator}${cur}`, iterator);
});

const getQueryString = pipe(
  L.entries,
  L.map(([k, v]) => `${k}=${v}`),
  join('&'),
);
```

### take, find

```ts
const users = [
  { age: 32 },
  { age: 31 },
  { age: 37 },
  { age: 28 },
  { age: 25 },
  { age: 32 },
  { age: 31 },
  { age: 37 },
];

const find = curry((fn, iterable) =>
  go(iterable, L.filter(f), take(1), ([a]) => a),
);
console.log(find((user) => user.age <= 30)(users));

go(
  users,
  L.map((u) => u.age),
  find((age) => age < 30),
  log,
);
```
