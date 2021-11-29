# Promise 객체

## Promise란?

자바스크립트에서 **비동기 함수를 동기 처리**하기 위해 고안한 객체  
`비동기 작업이 완료된 이후에 다음 작업을 연결시켜` 진행할 수 있다.  
작업에 따라 성공 또는 실패를 리턴하며 결과 값을 전달 받을 수 있다.

## Promise의 3가지 상태

- Pending(대기): 처리가 완료되지 않은 상태
- Fulfilled(이행): 성공적으로 완료된 상태
- Rejected(거부): 처리가 실패로 끝난 상태

## 잘못된 비동기 방식

```js
function goToSchool() {
  console.log('학교에 갑니다.');
}

function arriveAtSchool_asis() {
  setTimeout(function () {
    console.log('학교에 도착했습니다.');
  }, 1000);
}

function study() {
  console.log('열심히 공부를 합니다.');
}
goToSchool();
arriveAtSchool_asis();
study();
```

학교에 도착해서 열심히 공부하는 과정을 3가지 함수로 작성해보자.

```
학교에 갑니다.
열심히 공부를 합니다.
학교에 도착했습니다.
```

학교에 도착하기도 전 열심히 공부하는 상태가 발생한다. 이는 자바스크립트 콜스택에서 setTimeout은 이벤트 큐로 빠지기때문에 일어나는 현상이다.

Promise를 적용해보자

## Promise 기본 예제

```js
function arriveAtSchool_tobe() {
  return new Promise(function (resolve) {
    setTimeout(function () {
      console.log('학교에 도착했습니다.');
      resolve();
    }, 1000);
  });
}

goToSchool();
arriveAtSchool_tobe().then(function () {
  study();
});
```

Promise는 객체를 리턴하는데 `then`이라는 메서드를 가지고 있고 그 메서드 파라미터에 콜백 함수를 대입하면서 `resolve()`가 실행되는 구조이다.

## Promise 고급 예제

Promise 객체는 `2가지의 콜백함수`를 가진다. 하나는 resolve 함수이고 하나는 reject함수이다.

```js
function arriveAtSchool_tobe_adv() {
  return new Promise(function (resolve, reject) {
    setTimeout(function () {
      var status = Math.floor(Math.random() * 2);
      if (status === 1) {
        resolve('학교에 도착했습니다.');
      } else {
        reject('중간에 넘어져 다쳤습니다.');
      }
    }, 1000);
  });
}

function cure() {
  console.log('양호실에 가서 약을 발랐습니다.');
}
```

resolve는 성공시 reject는 실패시 실행된다.

`reject`의 경우는 명시적으로 `Error 객치를 만들어 넘겨주는것`이 일반적이다.

```js
reject(new Error('erorr'));
```

## Promise 체이닝

```js
add(1, 1)
  .then(function (res) {
    // res: 2
    return res + 1; // 2 + 1 = 3
  })
  .then(function (res) {
    // res: 3
    return res * 4; // 3 * 4 = 12
  })
  .then(function (res) {
    // res: 12
    console.log(res); // 12 출력
  });
```
