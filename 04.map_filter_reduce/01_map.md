# map

```ts
const products = [
  { name: '반팔티', price: 15_000 },
  { name: '긴팔티', price: 20_000 },
  { name: '핸드폰케이스', price: 15_000 },
  { name: '후드티', price: 30_000 },
  { name: '바지', price: 25_000 },
];
```

```ts
// name을 배열에 담기
const names = [];
for (const p of products) {
  names.push(p.name);
}

// price를 배열에 담기
const prices = [];
for (const p of products) {
  prices.push(p.price);
}
```

map 함수로 리팩토링하기

- 함수형 프로그래밍에서는 함수가 인자와 리턴값으로 소통하는 것을 권장한다.
- 즉, map 함수에서 리턴한 값을 개발자가 사용할 수 있게 된다.
- map 함수는 고차함수이다.
  - 함수를 값(인자)으로 다루면서 원하는 시점에 내부에서 인자를 적용할 수 있기 때문

```ts
const map = (fn, iterable) => {
  const result = [];
  for (const item of iterable) {
    result.push(fn(item));
  }
  return result;
};
```

```ts
const names = map((prod) => prod.name, products);

const prices = map((prod) => prod.price, products);
```

## 이터러블 프로토콜을 따른 map의 다형성

NodeList는 이터러블 프로토콜을 따르고 있기 때문에 map 함수를 적용할 수 있게 된다.

```ts
const elements = document.querySelectorAll('*');
// Error
elements.map((el) => el.nodeName); // error: map is not a function

// map 함수를 적용
map((el) => el.nodeName, elements);
```

제너레이터도 이터러블 프로토콜을 따르고 있으므로 map 함수를 사용할 수 있다.

```ts
function* gen() {
  yield 1;
  yield 2;
  yield 3;
  return 100;
}
map((a) => a * a, gen()); // 1 -> 4 -> 9
```

이터러블 프로토콜을 따랐을 때의 조합성

```ts
const m = new Map();
m.set('a', 10);
m.set('b', 20);
map(([key, value]) => [key, value * 2], m); // [["a", 20], ["b", 40]]
new Map(map(([key, value]) => [key, value * 2], m));
```
