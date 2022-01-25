# 고차 함수

## 1. 들어가기전

고차 함수의 개념을 완전히 이해하기 위해서 함수형 프로그래밍이 무엇인지와 `퍼스트 클래스 함수`의 개념을 이해해야 한다.

## 2. 함수형 프로그래밍이란?

함수형 프로그래밍은 함수를 다른 함수의 파라미터로 넘길 수도 있고 반환값으로 사용할 수 있는 프로그래밍 형태를 말한다.

자바스크립트, Haskell, Clojure, Scala, Erlang은 전부 함수형 프로그래밍을 구현한 언어

## 3. 퍼스트 클래스 함수

자바스크립트를 사용하면서 함수를 일급 객체로 대한다는것을 알고있다.
일급 객체란? 아래 3가지 조건을 충족하면 일급 객체이다.

- 변수나 데이터에 할당할 수 있다.
- 객체의 인자로 넘길 수 있다.
- 객체의 리턴값으로 사용할 수 있다.

자바스크립트에서 함수는 전부 **객체**이다.

```js
function foo() {
  console.log('hello foo');
}
foo(); // hello foo

foo.test = 'test';
console.log(foo.test); //test
```

오브젝트에 프로퍼티를 추가하듯 함수에 프로퍼티를 추가할 수 있다.

하지만 이런 문법은 굉장히 위험하기 때문에 함수 객체에 프로퍼티를 추가하지 않는것을 권장한다.

- ### 함수를 변수에 할당하기

```js
const foo = function (x) {
  return x + x;
};
foo(1); //2;
```

- ### 함수를 다른함수의 인자로 넘기기

```js
function formalGreeting() {
  console.log('How are you?');
}

function casualGreeting() {
  console.log("What's up?");
}

function greet(type, greetFormal, greetCasual) {
  if (type === 'formal') {
    greetFormal();
  } else if (type === 'casual') {
    greetCasual();
  }
}

// prints "What's up?"
greet('casual', formalGreeting, casualGreeting);
```

## 4. 고차함수란

고차함수는 함수를 인자로 받거나 또는 함수를 반환함으로써 작동하는 함수를 말한다.

```js
function plusTwo(num) {
  return num + 2;
}
function doubleNum(func, num) {
  let doubleArr = [];
  return func(num);
}
```

`Array.prototype.map` , `Array.prototype.filter`등 Array객체 내에 포함된(built-in) 고차함수이다.

### Array.prototype.map

`map()`메소드는 입력으로 들어온 배열 내 모든 엘리먼트를 인자로 제공받는 콜백함수를 호출함으로써 새로운 배열을 만들어낸다.

### 코드예시

```js
//고차함수가 아닌 코드
const arr1 = [1, 2, 3];
const arr2 = [];

for (let i = 0; i < arr1.length; i++) {
  arr2.push(arr[i] * 2);
}
console.log(arr2); // [2,4,6]
```

```js
const arr1 = [1, 2, 3];
const arr2 = arr1.map(item => item * 2);
console.log(arr2); //[2,4,6]
```
