## 함수와 블록 스코프

### 스코프
스코프(scope, 유효범위)는 자바스크립트를 포함한 모든 프로그래밍 언어의 기본적인 개념으로 `전역 스코프`와 `지역 스코프` 두 가지가 존재한다.

### 전역 스코프(Global Scope)
전역 변수를 선언하면 자바스크립트 코드 어디에서든 접근 가능하다.(함수 내부라 할지라도)

```js
var globalValue ='hello';

function foo(){
    console.log(globalValue);
}
foo(); // hello
```

### 암묵적 전역

```js
var x = 10;
function foo(){
    y= 20;
    console.log(x+y);
}
foo()//30
```
y는 선언하지 않은 식별자이다. 따라서 `y=20`이 실행되면 참조 에러가 발생할 것 같지만 선언하지 않은 식별자 y는 선언된 변수처럼 동작한다. 이는 선언하지 않은 식별자가 값을 할당하면 전역 객체의 프로퍼티에 할당된다.   

자바스크립트 엔진은 `y=20`을 `window.y = 20`으로 인식한다. 이러한 현상을 **암묵적전역** 이라 한다.


### 지역 스코프(Local Scope)
지역 변수란  코드 내 특정 구역에서만 사용할 수 있는 변수이다. 지역변수에는 함수스코프, 블록스코프 두가지가 있다.

#### 1. 함수 스코프
함수 내에서 변수를 선언했을 때, 함수안에서만 이 변수에 접근할 수 있다.

```js
function sayHello(){
    const hello = 'hello';
    console.log(hello);
}
sayHello(); //hello
console.log(hello)//Error
```

```js
let x = 'global';

function foo(){
  let x = 'local';
  console.log(x);
}

foo() // local
console.log(x) // global
```

#### 2. 블록 스코프

변수를 `{}`중괄호 안에 `const`나 `let`키워드로 선언했을 때, `{}` 중괄호 안에서만 이 변수에 접근할 수 있다.

```js
{
    const hello='hello';
    console.log(hello); 
}
console.log(hello) //Error
```

하지만 `var`키워드는 접근 가능하며 **함수 밖에서 선언된 변수는 코드블록 내에서 선언되었다 할지라도 모두 전역 스코프를 갖게 된다.** 따라서 변수 x는 전역 변수이다.

```js
if(true){
    var x=5;
}
console.log(x) //5
```