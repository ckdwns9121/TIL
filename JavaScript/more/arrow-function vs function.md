# Arrow Function이란?

- ES6부터 추가된 표현
- function 표현에 비해 구문이 짧다.
- 자신의 this, arguments, super 또는 new.target을 바인딩 하지 않는다.
- **항상 익명 함수**이다.
- 메소드 함수가 아닌 곳에 적합하다. 그래서 생성자로 사용할 수 없다.

### Arrow Function vs Function

1. 간결한함수표현

```js
var elements = ['foo', 'bar', 'hello'];

// [3,3,5]
elements.map(function (element) {
  return element.length;
});
// 위의 표현을 아래 화살표 함수로 쓸 수 있다.
elements.map(element => {
  return element.length;
});
// 파라미터가 하나만 있을 때는 괄호를 생략할 수 있다.
elements.map(element => {
  return element.length;
});
// 화살표 함수내부에 리턴할 코드가 하나라면 중괄호({})화  return을 생략할 수 있다.
element.map(element => element.length);
```

2. 바인딩 되지않는 this

- 일반 Function 표현에서는 모든 함수가 자신만의 this를 가진다.
- 함수 종류에 따라 this가 가르키는 객체가 다름

  - 함수 실행시 전역(window)객체를 가리킨다.
  - 메소드 실행시에는 메소드를 소유하고 있는 객체를 가리킨다.
  - 생성자 실행시에는 새롭게 만들어진 객체를 가리킨다.

- Arrow Function에서는 전역 컨텍스트에서 실행될 때 this를 새로 정의하지 않는다.
  - 스코프에서 바로 바깥 스코프의 this값을 사용
  - this를 클로저 값으로 처리하는것과 같음

```js
var Person = function (name, age) {
  this.name = name;
  this.age = age;
  this.say = function () {
    console.log(this); // Person {name: "Nana", age: 28}

    setTimeout(function () {
      console.log(this); // Window
      console.log(this.name + ' is ' + this.age + ' years old');
    }, 100);
  };
};
var me = new Person('Nana', 28);
me.say();
```

왜 함수안에서 this를 쓰면 window객체를 가르키는거지? 싶을땐 화살표 함수를 쓰면된다.  
화살표 함수는 전역 컨텍스트에서 실행되더라도 this를 새로정의하지 않고 바로 바깥 함수나 클래스의 this를 가리키기 때문이다.

```js
var Person = function (name, age) {
  this.name = name;
  this.age = age;
  this.say = function () {
    console.log(this); // Person {name: "Nana", age: 28}

    setTimeout(() => {
      console.log(this); // Window
      console.log(this.name + ' is ' + this.age + ' years old');
    }, 100);
  };
};
var me = new Person('Nana', 28);
me.say();
```

### This
