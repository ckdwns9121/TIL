## 함수와 블록 스코프

### 스코프

스코프(scope, 유효범위)는 자바스크립트를 포함한 모든 프로그래밍 언어의 기본적인 개념으로 `전역 스코프`와 `지역 스코프` 두 가지가 존재한다.

### 전역 스코프(Global Scope)

전역 변수를 선언하면 자바스크립트 코드 어디에서든 접근 가능하다.(함수 내부라 할지라도)

```js
var globalValue = 'hello';

function foo() {
  console.log(globalValue);
}
foo(); // hello
```

### 암묵적 전역

```js
var x = 10;
function foo() {
  y = 20;
  console.log(x + y);
}
foo(); //30
```

y는 선언하지 않은 식별자이다. 따라서 `y=20`이 실행되면 참조 에러가 발생할 것 같지만 선언하지 않은 식별자 y는 선언된 변수처럼 동작한다. 이는 선언하지 않은 식별자가 값을 할당하면 **전역 객체의 프로퍼티**에 할당된다.

자바스크립트 엔진은 `y=20`을 `window.y = 20`으로 인식한다. 이러한 현상을 **암묵적 전역** 이라 한다.

전역 변수에서 변수 선언을 할 수 있더라도, 전역 변수에서는 변수를 선언하지 않는 것을 권장한다. 그 이유는 두개 혹은 그 이상의 변수들이 같은 이름을 가지게 되어 네이밍 충돌이 발생할 확률이 높다.

### 지역 스코프(Local Scope)

지역 변수란 코드 내 특정 구역에서만 사용할 수 있는 변수이다. 지역변수에는 함수스코프, 블록스코프 두가지가 있다.

#### 1. 함수 스코프

함수 내에서 변수를 선언했을 때, 함수안에서만 이 변수에 접근할 수 있다.

```js
function sayHello() {
  const hello = 'hello';
  console.log(hello);
}
sayHello(); //hello
console.log(hello); // Error, hello is not defined
```

```js
let x = 'global';

function foo() {
  let x = 'local';
  console.log(x);
}

foo(); // local
console.log(x); // global
```

#### 2. 블록 스코프

변수를 `{}`중괄호 안에 `const`나 `let`키워드로 선언했을 때, `{}` 중괄호 안에서만 이 변수에 접근할 수 있다.

```js
{
  const hello = 'hello';
  console.log(hello);
}
console.log(hello); //Error
```

블록 스코프는 함수 스코프의 부분 집합이다. 함수는 `{}` 괄호로 작성되어야 하기 때문이다. 물론 화살표 함수로 즉시 리턴하면 {} 없이 함수를 만들 수도 있다.

하지만 `var`키워드는 접근 가능하며 **함수 밖에서 선언된 변수는 코드블록 내에서 선언되었다 할지라도 모두 전역 스코프를 갖게 된다.** 따라서 변수 x는 전역 변수이다.

```js
if (true) {
  var x = 5;
}
console.log(x); //5
```

### 함수 호이스팅과 스코프

호이스팅은 끌어올리다 라는 의미를 가지고 있다.

`function` 키워드와 함께 선언된 함수들은 항상 현재 스코프의 가장 위로 호이스팅 된다.

```js
//호이스팅 전
function sayHello() {
  console.log('hello');
}
sayHello();

//호이스팅 후
sayHello();
function sayHello() {
  console.log('hello');
}
```

그러나 함수 표현식으로 작성된 함수들은 현재 스코프 가장 위로 호이스팅 되지 않는다.

```js
sayHello(); //Error, sayHello is no defined;
const sayHello = function () {
  console.log('hello');
};
```

> ## **항상 함수는 사용되기 전 미리 선언하자**

### 함수는 각자의 스코프에 접근할 수 없다.

함수를 각각 선언했을 때, 함수는 다른 함수의 스코프에 접근할 권한을 갖고 있지 않는다. 심지어 함수 내에서 다른 함수를 불러오더라도 스코프는 사용할 수 없다.

아래 예제에서, `second`는 `firstFunctionVariable`에 접근할 권한이 없다.

```js
function first() {
  const firstFunctionVariable = `I'm part of first`;
}

function second() {
  first();
  console.log(firstFunctionVariable); // Error, firstFunctionVariable is not defined
}
```

### 내부 스코프

함수가 다른 함수 안에서 만들어졌고 안쪽 함수(inner function)는 바깥 함수(outer funtion)의 변수에 접근 가능하다. 이러한 것을 **어휘적 스코프(Lexical Scoping)**이라고 한다.

하지만 바깥 함수는 안쪽 함수에 접근할 권한이 주어지지 않는다.

```js
function outerFunction() {
  const outer = `I'm the outer function!`;

  function innerFunction() {
    const inner = `I'm the inner function!`;
    console.log(outer); // I'm the outer function!
  }

  console.log(inner); // Error, inner is not defined
}
```

> 안에서 바깥이 보이지만 밖에선 안이 보이지 않는 유리
