# 단일 책임 원칙 (Single Responsiblity Principle)

## 단일 책임 원칙이란?

**하나의 객체는 반드시 하나의 동작만의 책임을 갖는다** 라는 원칙이다.

모듈화가 강해질수록 다른 객체와의 의존/연관성이 줄어든다. 반대로 이야기하면 모듈화가 약해질수록 다른 객체와의 의존/연관성은 크게늘어나며, 최악의 경우 어떠한 은닉화 정책도 존재하지 않아 모듈의 메소드에 무분별하게 접근할 수도 있게된다.

## 코드로 보는 예제

- 함수

아래 코드를 보자 x+y를 return 해주는 `add`함수와 그 결과를 출력해주는 `numPrint`함수가 있다.

```js
function add(x, y) {
  return x + y;
}
function numPrint(num) {
  console.log(num);
}
```

함수의 개수를 줄이려고 아래 코드처럼 통합할 필요는 없다.

```js
function addPrint(x, y) {
  var num = x + y;
  console.log(num);
  return num;
}
```

- 클래스

고양이 클래스를 만들었다.

```js
class Cat {
  constructor(age, name) {
    this.age = age;
    this.name = name;
  }
  eat(food) {
    console.log(`eat ${food}`);
  }
  walk() {
    console.log('walk');
  }
  speak(message) {
    console.log(message);
  }
  print() {
    console.log(`나이는 ${this.age} 이름은 ${this.name}`);
  }
}
```

위 코드는 문제가있다. 고양이에 대해서 생각을 해보자. 고양이는 음식을 먹기, 걷기, 말하기 같은 동작을 하는것은 당연한데 프린트 하기는 고양이가 가지고 있는 특징과 맞지 않다.

따라서 고양이의 상태를 출력해주는 함수는 따로 빼주어야 한다.

```js
class Cat {
  constructor(age, name) {
    this.age = age;
    this.name = name;
  }
  eat(food) {
    console.log(`eat ${food}`);
  }
  walk() {
    console.log('walk');
  }
  speak(message) {
    console.log(message);
  }
}
let tom = new Cat(13, 'tom');
console.log(`나이는 ${tom.age} 이름은 ${tom.name}`);
```
