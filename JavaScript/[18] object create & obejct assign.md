# Object.create와 Object.assign

## Object.create

`Object.create()`메서드는 지정된 프로토타입 및 객체 및 속성을 갖는 새로운 객체를 만든다.

> Object.create(ptoro[,propertiesObject])

```js
const fruit = {};
const apple = Object.create(fruit);
```

매개변수 `proto`는 새로 만든 객체의 프로토타입이어야할 객체이며 `propertiesObject`는 프로토타입에 없는 새로운 프로퍼티를 객체에 추가할 수 있다.

```js
const fruit = {};
const apple = Object.create(fruit, { color: { value: 'red' } });
console.log(apple.color); //red
```

`Object.create()`를 사용해 객체를 생성하는 예제

```js
var dog = {
  eat: function () {
    console.log(this.earFood);
  },
};
var maddie = Object.create(dog);

console.log(dog.isPrototypeOf(maddie)); // true

maddie.eatFood = 'NyamNaym';
maddie.eat(); // NyamNaym
```

1. eat 메소드를 가지고있는 dog 객체를 생성한다.
2. Object.create(dog)를 사용해 middle을 초기화하고 dog의 프로토타입으로 설정된 완전히 새로운 객체를 만든다.
3. 자바스크립트는 프로토타입 체인을 통해 dog에서 eat 메소드를 찾아내고 this를 middle로 설정한다.
4. object.create()는 프로토타입이 dog로 설정된 middle을 새롭게 만들었고 middle은 언제나 dog의 메소드에 접근할 수 있다.

## Object.assign

`Object.assign()`메소드는 ES6 문법에 도입되었으며, 출처 객체들의 모든 열거 가능한 자체 속성을 **복사**해 대상 객체에 붙여넣고 그 대상 객체를 반환한다.

> Object.assign(target, ...source)

```js
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };
const returnedTarget = Object.assign(target, source);

console.log(target);
// expected output: Object { a: 1, b: 4, c: 5 }
console.log(returnedTarget);
// expected output: Object { a: 1, b: 4, c: 5 }
```

목표 객체의 속성 중 출처 객체와 동일한 키를 갖는 경우, 그 값은 객체의 속성 값으로 덮어쓰게 된다.

또한 얕은 복사이므로 원본 객체의 프로퍼티를 수정하면 복사된 객체의 프로퍼티 또한 수정된다.

```js
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const newState = Object.assign(target, soruce);
newState.a = 5;
console.log(target.a); //5
```

# 추가작성

## Object.keys()

- Object.keys() 메소드는 주어진 객체의 속성 이름들을 일반적인 반복문과 동일한 순서로 순회되는 열거할 수 있는 배열로 반환

- 객체의 키 값만 뽑는다.

```js
const object1 = {
  a: 'somestring',
  b: 42,
  c: false,
};

console.log(Object.keys(object1));
// expected output: Array ["a", "b", "c"]
```
