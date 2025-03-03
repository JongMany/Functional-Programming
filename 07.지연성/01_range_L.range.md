# range와 느긋한 L.range

## range

```ts
const range = (length) => {
  let i = -1;
  const result = [];
  while (++i < length) {
    result.push(i);
  }
  return result;
};

console.log(range(5)); // [0, 1, 2, 3, 4]
console.log(range(2)); // [0, 1]
```

```ts
const add = (a, b) => a + b;
const list = range(4);
console.log(reduce(add, list)); // 6
```

list 값이 배열인 상태임 (배열로 평가된 상태)

## L.range

```ts
const L = {};
L.range = function* (length) {
  let i = -1;
  while (++i < length) {
    yield i;
  }
};

const add = (a, b) => a + b;
const list = L.range(4); // iterator (이 때, 값이 생기지 않음)
console.log(reduce(add, list)); // 6
```

list는 이터레이터이며, next()를 호출할 때 내부 함수가 실행된다.  
-> 사용자가 필요할 때, 값을 꺼내서 쓸 수 있게 된다.

```ts
const L = {};
L.range = function* (length) {
  let i = -1;
  while (++i < length) {
    console.log('L.range', i);
    yield i;
  }
};

const list = L.range(4);
console.log(list.next()); // "L.range" 0 -> {value: 0, done: false}
console.log(list.next()); // "L.range" 1 -> {value: 1, done: false}
```

## range와 L.range 테스트

```ts
const test(name, time, f) {
  console.time(name);
  while(time--) {
    f();
  }
  console.timeEnd(name);
}

test('range', 10, () => reduce(add, range(1_000_000)))
test('L.range', 10, () => reduce(add, L.range(1_000_000)))
```
