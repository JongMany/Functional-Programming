# take

```ts
const take = curry((limit, iterable) => {
  const result = [];
  for (const item of iterable) {
    result.push(item);
    if (result.length === limit) return result;
  }
  return result;
});
console.time('');
take(5, range(100000)); // [0, 1, 2, 3, 4]
go(range(10000), take(5), reduce(add), console.log);
console.timeEnd('');

console.time('');
take(5, L.range(100000)); // [0, 1, 2, 3, 4]
go(L.range(10000), take(5), reduce(add), console.log);
console.timeEnd('');

console.time('');
take(5, L.range(Infinity)); // [0, 1, 2, 3, 4]
go(L.range(Infinity), take(5), reduce(add), console.log);
console.timeEnd('');
```

L.range로 가져오는 값은 메모리 효율성이 좋다 (값을 미리 만들어 놓지 않기 때문임)  
또한 무한 배열을 표현해도 메모리 문제가 발생하지 않는다.

take는 연산을 미루고, 특정 개수를 뽑아서 연산을 할 때 유용하다.
