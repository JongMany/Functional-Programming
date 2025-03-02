# 평가와 일급

## 평가

- 코드가 계산(evaluation)되어 값을 만드는 것  
  ex) [1, 2 + 3]는 [1, 5]로 평가 된다.

## 일급

- 값으로 다를 수 있다.
- 변수에 담을 수 있다.
- 함수의 인자/결과로 사용될 수 있다.

```ts
const a = 10; // 변수에 담을 수 있다.
const add10 = (a) => a + 10;
const r = add10(a); // 함수의 인자/결과로 사용될 수 있다
```

## 일급 함수

- 함수를 값으로 다룰 수 있다.
- 조합성과 추상화의 도구

```ts
const add5 = (a) => a + 5; // 함수를 값으로 다룰 수 있다.
console.log(add5); // a => a + 5 (함수의 인자로 함수를 사용할 수 있다.)
console.log(add5(5));

const f1 = () => () => 1; // 함수의 결과값으로 함수를 사용할 수 있다.
console.log(f1()); // () => 1

const f2 = f1(); // 함수의 결과를 변수에 담을 수 있다.
console.log(f2()); // 함수를 원하는 시점에 평가해서 결과를 만들 수 있다.
```

## 고차 함수

- 함수를 값으로 다루는 함수

### 고차함수의 유형 1 - 함수를 인자로 받아 실행하는 함수

```ts
// 함수가 함수를 인자로 받아 내부에서 실행
const apply1 = (f) => f(1);
const add2 = (a) => a + 2;
console.log(apply1(add2)); // 3
console.log(apply1((a) => a - 1)); // 0
```

```ts
const times = (f, number) => {
  let i = -1;
  while (++i < n) f(i);
};

times(console.log, 3); // 0 -> 1 -> 2
times((a) => console.log(a + 10), 3); // 10 -> 11 -> 12
```

### 고차함수의 유형 2 - 함수를 만들어 리턴하는 함수 (클로저를 만들어 리턴하는 함수)

```ts
const addMaker = (a) => (b) => a + b;
const add10 = addMaker(10);
console.log(add10); // b => a + b (b => 10 + b) a를 클로저를 가지고 있음
console.log(add10(10)); // 20
```
