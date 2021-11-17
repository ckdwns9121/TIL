## 팩토리 함수와 클래스

### 클래스

자바스크립트에서 클래스는 프로토타입을 기반으로 만들어진 특수 함수이다. 따라서 함수를 정의하듯 클래스 선언과 표현식으로 정의할 수 있다.

`ES5`에서는 생성사 함수와 프로토타입, 클로저를 사용해 객체지향 프로그래밍을 구현하였다.

```js
var Person = (function () {
  //constructor
  function Person(name) {
    this.name = name;
  }

  //public method
  Person.prototype.sayHi = function () {
    console.log(this.name + 'hi');
  };

  //return constructor
  return Person;
})();

var changjun = new Person('changjun');
changjun.sayHi(); // changjun hi

console.log(changjun instanceof Person); //true
```

이러한 프로토타입 기반의 객체지향 프로그래밍은 클래스 기반 언어에 익숙하지 않은 사람들에게 혼란을 가져왔고 어려웠다. 따라서 `ES6`에서 새로운 클래스 문법이 추가되었다.

### 클래스 정의

```js
class Person {
  constructor(name) {
    this.name = name;
  }
  sayHi() {
    console.log(`${this.name} hi`);
  }
}

const changjun = new Person('changjun');
changjun.sayHi(); // changjun hi;
```

이전 ES5에서 function을 통한 함수 선언은 호이스팅이 일어나지만 `class`를 통한 클래스 선언은 호이스팅이 일어나지 않기 때문에
클래스 선언문 이전에 참조할 수 없다. (정확이 `var`처럼 호이스팅 되지 않는다.)

```js
console.log(Foo); // ReferenceError : Cannot access 'Foo' before initialization
class Foo {}
```

호이스팅이 발생하지 않는다고는 말할 수 없다. let과 const와 같은 방식으로 호이스팅 된다.

### Constructor

`constructor`는 인스턴스를 생성하고 클래스 필드를 초기화 하기위한 특수한 메소드이다.

클래스 필드란 클래스 내부의 캡슐화된 변수를 말한다. 데이터 변수 또는 멤버변수라고 부르며 인스턴스의 프로퍼티 또는 정적 프로퍼티가 될 수 있다.

contructor는 클래스 내에 한개만 존재할 수 있으며 만약 클래스가 2개 이상의 constructor를 포함하면 문법 에러가 발생한다.

### 클래스 필드

클래스 몸체에는 메소드만 선언할 수 있으며 변수 선언시 에러가 발생한다.
변수 선언은 생성자 안에서 해야한다.

```js
class Foo {
  name = ''; //SyntaxError

  constructor() {}
}
```

> 2019년 5월 현재 클래스 몸체에 직접 인스턴스를 선언하고 private한 필드를 선언할 수 있게 브라우저와 최신 node.js가 구현했다.

### getter setter

```js
class Foo {
  constructor(arr = []) {
    this.arr = arr;
  }

  get firstElem() {
    return this.arr;
  }
}
```
