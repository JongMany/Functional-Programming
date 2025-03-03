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
L.filter = function * (fn, iterable){
  fot(const item of iterable) {
    if(fn(item)) {
      yield item;
    }
  }
}

const filter = curry(
  pipe(
    L.filter,
    take(Infinity)
  )
)

```
