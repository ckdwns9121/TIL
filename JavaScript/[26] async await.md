# async/await

## async/await란

`Promise`객체를 좀 더 쉽게 다룰 수 있게 고안된 문법. ECMAScript 2017에서 표준으로 정의된 문법이다.

```js
async function greet() {
  return 'hello';
}
greet().then(res => console.log(res));
```

위 예제를 돌려보면 `Promise`객체가 반환된다.  
명시적으로 resolve함수를 통해 반환가능

```js
async function greet() {
  return Promise.resolve('hello');
}
greet().then(console.log);
```

## await 예제

```js
function greet() {
  return new Promise(function (resolve) {
    setTimeout(function () {
      resolve('hello');
    }, 1000);
  });
}

(async function () {
  var result = await greet(); //resolved 될 때까지 대기
  console.log(result);
})();
```

`await`는 `async` 함수내에서만 사용할 수 있으며
비동기 작업의 순차처리가 일반 프로그래밍과 동일하게 가능하다.
