# 호이스팅

## 호이스팅(hoisting)이란?

호이스트(hoist)는 건축/건설이나 화물 운반에 사용되는 장비로 화물을 **들어올리는** 업무를 수행한다.
즉, 아래에 위치한 것을 위로 끌어올리는 역할을 하는데 이 단어 자체로도 들어올리다는 의미를 가지고 있다.

자바스크립트에서 호이스팅은 코드에 선언된 변수 및 함수를 코드 상단으로 끌어올리는 것이며 이는 **변수 범위가 전역인지 함수내 인지**에 따라 다르게 수행된다.

## 호이스팅의 대상

### 1. var 변수 선언

```javascript
console.log(name);
var name = 'hello';
```

위 코드는 오류를 발생할 것 같지만 오류없이 아래와 같은 로그가 찍힌다.

```javascript
undefined;
```

name이라는 변수는 내부적으로 호이스팅 되어 아래와 같이 동작한다.

```javascript
var name;
console.log(name);
name = 'hello';
```

### 2. 함수 선언문

```js
foo();
foo2();

function foo() {
  // 함수선언문
  console.log('hello');
}
var foo2 = function () {
  // 함수표현식
  console.log('hello2');
};
```

```js
var foo2;
function foo() {
  console.log('hello');
}
foo();
foo2(); //ERROR! foo2 is not function!
foo2 = function () {
  console.log('hello2');
};
```

**호이스팅 시 함수 선언문과 함수 표현식에서 서로 다르게 동작한다.**

## 함수선언문과 함수표현식에서의 호이스팅

**함수의 선언만 위로 끌어올려지며 할당은 위로 끌어올려지지 않는다**

### 1. 함수선언문에서의 호이스팅

```js
function foo() {
  //함수선언문
  var result = inner();
  console.log(typeof inner);
  console.log(result);
  function inner() {
    //함수선언문
    return 'inner';
  }
}
foo(); //함수호출
```

```js
//호이스팅의 결과
function foo() {
  var result;
  function inner() {
    return 'inner';
  }
  result = inner();
  console.log(typeof inner);
  console.log(result);
}
```

위의 코드는 inner가 선언보다 호출이 먼저되었지만 실제로 호이스팅은 아래와 같은 코드로 일어나기 때문에 오류가 발생하지 않는다.

### 2. 함수표현식의 호이스팅

- 함수표현식의 선언이 호출보다 위에있는 경우. -정상출력

```js
function foo() {
  //함수선언문
  var inner = function () {
    //함수표현식
    return 'inner';
  };
  var result = inner();
  console.log(result);
}
foo(); //함수호출
```

```js
function foo() {
  var inner;
  var result;
  inner = function () {
    //함수 할당
    return 'inner';
  };
  result = inner();
  console.log(result);
}
```

- 함수표현식의 선언이 호출보다 아래에있는 경우. -TypeError

```js
function foo() {
  console.log(inner);
  var result = inner();
  console.log(result);
  var inner = function () {
    //함수표현식
    return 'hello';
  };
}
foo(); //TypeError: inner is not a function
```

```js
//호이스팅
function foo() {
  var result;
  var inner;

  result = inner();

  console.log(inner); // TypeError: inner is not a function
  console.log(result); //undefind;

  inner = function () {
    return 'inner';
  };
}
foo();
```

호이스팅에의해 inner는 undefined로 지정되기 때문에 "inner is not a function" 오류가 뜬다.

## 호이스팅 우선순위

변수선언이 함수선언보다 위로 끌어올려진다.

```js
var myName = 'hi';
function myName() {
  console.log('yuddomack');
}
function yourName() {
  console.log('everyone');
}

var yourName = 'bye';

console.log(typeof myName);
console.log(typeof yourName);
```

```js
var myName;
var yourName;
function myName() {
  console.log('yuddomack');
}
function yourName() {
  console.log('everyone');
}
myName = 'hi';
yourName = 'bye';

console.log(typeof myName); //string
console.log(typeof yourName); //string
```

## Temporal Dead Zone(TDZ)

그렇다면 let과 const는 호이스팅이 되지 않나? no
let과 const는 TDZ영역을 받는다.

let과 const가 호이스팅이 되기전 TDZ에 대해 알아야한다.

자바스크립트에서 변수는 선언,초기화,할당 3단계로 나누어진다.

1. var: 선언단계+ 초기화단계 -> 할당단계
2. let: 선언단계 -> 초기화단계 -> 할당단계
3. const: 선언단계 + 초기화단계 + 할당단계

이렇게 변수마다 차이점이 존재한다.
그렇기 때문에 실행 컨텍스트에 변수를 등록했지만, 메모리가 할당이 되질 않아서 접근할 수 없기 때문에 참조 에러가 발생한다.

var는 함수 스코프에서 접근가능하고 let과 const는 블록스코프이다.

# 추가

## 자바스크립트의 어휘적 범위(lexical scope)

의미사용이론에 따르면 단어의 의미는 그 어휘적인, 근처 환경에서의 의미가 된다. 이는 자바스크립트에서 다음처럼 적용된다.

> 변수의 의미는 그 **어휘적인(lexical), 실행문맥(excution context)**에서의 의미가 된다.

그렇기 때문에 동일 범위(실행 문맥)의 모든 `선언`을 참고(호이스팅)하여 의미를 정한다.

> 호이스팅은 실행 컨텍스트 생성 시 렉시컬 스코프 내의 선언이 끌어올려지는게 호이스팅이다.

# 정리

- 호이스팅이란 코드에 선언된 함수, 변수의 `선언문`을 위로 끌어올리는 것
- 변수 범위가 전역인지 함수내 인지에 따라 다르게 동작
- 선언은 끌어올려지지만 할당은 끌어올려지지 않는다.
- 변수선언이 함수선언보다 우선순위가 높다.
