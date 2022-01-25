# async & await

## async & await란

`Promise`객체를 좀 더 쉽게 다룰 수 있게 고안된 문법. `ECMAScript 2017`에서 표준으로 정의된 문법이다.

기본적으로 Promise 객체를 사용하지 않고 좀더 간편하게 작성가능하다.  
만약 user의 정보를 가져오는 `fetchUser`함수가 Promise 객체를 리턴한다고 해보자

## async

```js
function fetchUser() {
  return new Promise((resolve, reject) => {
    resolve('changjun');
  });
}
```

하지만 더 간편하게 `async` 키워드를 붙이면 자동적으로 `Promise`를 리턴한다.  
코드 블럭이 자동으로 Promise로 감싸진다고 생각하면 된다.

```js
async function fetchUser() {
  return 'changjun';
}
```

위 예제를 돌려보면 `Promise`객체가 반환된다.  
명시적으로 resolve함수를 통해 반환가능

```js
async function fetchUser() {
  return Promise.resolve('changjun');
}
fetchUser().then(console.log);
```

## await

사과와 바나나를 각각 1초뒤에 받아오는 함수를 짜보자.

```js
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
  await delay(1000);
  return '🍎';
}

async function getBanana() {
  await delay(1000);
  return '🍌';
}

function pickFruits() {
  return getApple().then(apple => {
    return getBanana().then(banana => `${apple} + ${banana}`);
  });
}
pickFruits().then(console.log);
```

`pickFruits` 함수를 보면 promise 체이닝이 되어있는데 이 부분 역시 콜백지옥에 빠질 수 있다.  
이를 async await으로 해결할 수 있다.

```js
async function pickFruits() {
  const apple = await getApple();
  const banana = await getBanana();
  return `${apple} + ${banana}`;
}
pickFruits().then(res => console.log(res));
```
