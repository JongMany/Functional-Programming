# L.map, L.filter로 map, filter 만들기

L.map으로 map 함수 만들기

```ts
L.map = curry(function* (fn, iterable) {
  const iterator = iterable[Symbol.iterator]();
  let cur;
  while (!(cur = iterator.next()).done) {
    // for - of 문
    const val = cur.value;
    yield fn(val);
  }
});

const map = curry((fn, iterable) => go(iterable, L.map(fn), take(Infinity)));
const map2 = curry((fn, iterable) => go(L.map(fn, iterable), take(Infinity)));

const map2 = curry(pipe(L.map, take(Infinity)));
```

L.filter로 filter 함수 만들기

```ts
L.filter = function* (fn, iterable) {
  for (const item of iterable) {
    if (fn(item)) {
      yield item;
    }
  }
};

const filter = curry(pipe(L.filter, take(Infinity)));

// L.filter 사용 - 지연 평가
const evenNumbers = L.filter((n) => n % 2 === 0, [1, 2, 3, 4, 5]); // 이터레이터(제너레이터) 반환, 실제 연산은 아직 수행되지 않음
console.log(evenNumbers); // L.filter {<suspended>}
for (const n of evenNumbers) {
  console.log(n); // 요청할 때마다 계산
}

// filter 사용 - 즉시 평가
const evenNumbersArray = filter((n) => n % 2 === 0)([1, 2, 3, 4, 5]); // 바로 [2, 4] 배열 반환, 모든 연산이 즉시 완료됨

console.log(evenNumbersArray);
```

지연 평가로 항목을 생성하지만, take(Infinity)로 인해 모든 결과를 즉시 평가하여 배열로 만듭니다.
즉시 평가(eager evaluation) 방식으로 최종 결과를 반환합니다
