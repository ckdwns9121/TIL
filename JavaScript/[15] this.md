# this에 대해알아보자

## 1. this란

> **this**는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수이다. this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메소드를 참조할 수 있다.

## 2. this의 이해

그렇다면 이 this값은 어떤 상황에서 어떻게 변할까? this 바인딩을 통해 this가 어떤 값과 연결되는지 확인해볼 수 있다.  
this 바인딩은 4가지 상황에서 각자 다르게 적용된다.

- 일반 함수 내부
- 메서드 내부
- 생성자 함수 내부
- Call, Apply, Bind를 통한 '호출 방식'

1. 일반함수 호출

```js
console.log(this === window); //true
var a = 30;
console.log(this.a); //30
function x() {
  return this;
}
x() === window; //true;
```

2. 객체 메소드 호출시 this는 호출한 객체에 바인딩

```js
let person = {
  firstName: "Changjun",
  lastName: "Park",

  getFullName() {
    console.log(this.firstName + this.LastName);
  },
};

person.getFullName(); // ChangejunPark
```

3. 생성자 함수로 호출시 생성자 함수가 생성할 객체에 바인딩

```js
function Person(color) {
  this.color = red;
}
let apple = new Person("red");
console.log(apple.color); // red
```

4. Call,Apply,Bind 메소드 사용시 메소드에 첫번째 인자로 전달하는 객체에 바인딩.

### 정리

this는 **함수 호출 방식**에 따라 동적으로 결정된다. 함수를 일반함수로 호출할 경우 this는 전역객체를, 메소드로 호출할 경우 이를 호출한 객체를, 생성자 함수를 호출할 때는 생성자 함수가 생성할 인스턴스를 가르킨다.

# 추가

자바스크립트에서 또 다른 악명으로 유명한 특징은 바로 `this`이다. 클래스 기반 객체지향 언어에서의 this와 완전히 다른 동작방식을 가지고 있으므로 대부분의 자바스크립트 초심자가 머리 싸매고 넘어가는게 바로 `this`이다.

이 this가 왜 다른 언어의 this랑 동작방식이 다른지 아무리 찾아봐도 깊게 설명해주는 글은 보지 못하고 암기식으로 this는 `자기자신을 가리키는 객체이다.`, `자기 참조 변수이다.` 라는 암기식 이론만 접했다. 따라서 깊게 이해하려 하지 않았고 arrow function에 의지하게 되었다. 그래서 이 this를 좀더 깊게 톺아보기로 했다.

아래는 this에 대한 대표적인 오해이다.

- this는 기본적으로 window다(x)
- 이벤트 리스너에서 등록한 콜백의 this는 내부에서 bind등을 통해 바뀌기 때문에 무엇인지 알 수 없다.(x)
- this는 외워야한다.(x)

이러한 오해를 바로잡기 위해서는 `프로토타입`에 대한 이해가 필요하다. 자바스크립트에서의 `this`는 어디서 발화했냐가 중요하다. 쉽게 이야기하면 받아들이는 `대상`에 따라 같은 단어도 의미가 달라진다는 것이다.

이것이 바로 프로토타입과 클래스의 대표적인 차이인데 전혀 다르게 `단어`를 보는 방식이고 중요한 세계관의 차이이다. 프로토타입에서는 **받아들이는 주체와 문맥이 가장 중요하다.** 프로그래밍 관점으로 보았을 땐 **실행하는 객체**가 가장 중요하다.

프로토타입 기반 언어에서는 this가 정의된 함수가 어떻게 발화(invoke)했는지에 따라 가리키는 값이 달라진다. **정확히는 받아들이는 대상의 컨텍스트를 가리킨다.**

```js
var someValue = "hello";
function outerFunc() {
  console.log(this.someValue); // 첫번째 : ?, 두번째 : ?
  this.innerFunc();
}
const obj = {
  someValue: "world",
  outerFunc,
  innerFunc: function () {
    console.log("innerFunc's this : ", this); // 첫번째 : ?, 두번째 : ?
  },
};
obj.outerFunc(); // 첫번째
outerFunc(); // 두번째
```

- 3L : 13L 에서 호출한 첫번째는 world가, 14L 에서 호출한 두번째는 hello 가 찍힌다. outerFunc 가 누구를 통해 발화(invoke)되었는지를 알면 this 가 무엇이 될지 알 수 있다.
- 4L : obj를 통해 실행되면 innerFunc이 존재하기 때문에 호출되지만 글로벌에서 실행되면 innerFunc이 없기때문에 에러가 뜬다.
- 10L : this(obj)를 통해 실행 되었기때문에 첫번째는 obj가 된다. 글로벌로 호출했을땐 innerFunc이 없기때문에 에러가 뜬다.
