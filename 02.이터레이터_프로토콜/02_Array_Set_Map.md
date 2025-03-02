# Array, Set, Map을 통해 알아보는 이터러블 / 이터레이터 프로토콜

## Array

```ts
const arr = [1, 2, 3];
for (const a of arr) {
  console.log(a);
}
```

## Set

```ts
const set = new Set([1, 2, 3]);
for (const a of arr) {
  console.log(a);
}
```

## Map

```ts
const set = new Set([
  ['a', 1],
  ['b', 2],
  ['c', 3],
]);
for (const a of map) {
  console.log(a);
}
```

---

set과 map은 키 값으로 접근 불가능

- ex) `set[0]`과 `map[0]`은 `undefined` 값임  
  => for - of 문은 내부적으로 index로 동작하는 것이 아니라는 것임

Symbol.iterator은 객체의 키로 사용될 수 있다.

- 배열의 키값으로도 사용된다.
  ```ts
  const arr = [1, 2, 3];
  console.log(arr[Symbol.iterator]); // 함수
  ```
- 만약 배열의 Symbol.iterator 속성을 null로 두게 되면? for-of문이 동작하지 않게 된다. (Set과 Map 역시 마찬가지)
  ```ts
  const arr = [1, 2, 3];
  arr[Symbol.iterator] = null;
  for (const a of arr) {
    console.log(a); // Uncaught TypeError: arr is not iterable;
  }
  ```
  즉, for-of 문과 Symbol.iterator 속성의 함수가 연관되어 있다는 의미가 된다.

## 이터러블 / 이터레이터 프로토콜

- 이터러블: 이터레이터를 리턴하는 `[Symbol.iterator]()`를 가진 값
  - arr, set, map은 이터러블이라고 부를 수 있다.
  - `arr[Symbol.iterator]()`를 호출하면 `Iterator`를 리턴한다.
- 이터레이터: `{ value, done }` 객체를 리턴하는 `next()`를 가진 값
  - `next` 메서드를 가진 값
  - `next` 메서드는 `{ value, done }`을 리턴
- 이터러블/이터레이터 프로토콜: 이터러블을 for...of, 전개 연산자 등과 함께 동작하도록 한 규약

```ts
const arr = [1, 2, 3];
const iterator = arr[Symbol.iterator](); // Array Iterator
const v1 = iterator.next(); // {value: 1, done: false}
const v2 = iterator.next(); // {value: 2, done: false}
const v3 = iterator.next(); // {value: 3, done: false}
const v4 = iterator.next(); // {value: undefined, done: true}
const v5 = iterator.next(); // {value: undefined, done: true}
```

```ts
const arr = [1, 2, 3];
const iterator = arr[Symbol.iterator](); // Array Iterator
const iter = iterator.next(); // {value: 1, done: false}

for (const a of iter) {
  console.log(a); // 2 -> 3
}
```

- map의 `keys`, `values`, `entries` 메서드는 이터러블을 반환한다.
  - 즉 map이라는 이터러블의 `keys`, `values`, `entries` 메서드도 이터러블을 반환한다.

```ts
const map = new Map([
  ['a', 1],
  ['b', 2],
  ['c', 3],
]);

for (const a of map.keys()) {
  console.log(a); // 'a' -> 'b' -> 'c'
}

for (const a of map.values()) {
  console.log(a); // 1 -> 2 -> 3
}

for (const a of map.entries()) {
  console.log(a); // ['a', 1] -> ['b', 2] -> ['c', 3]
}
```
