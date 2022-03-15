# 개방-폐쇄 원칙 (Open-Close Principle)

## 개방-폐쇄 원칙이란?

객체를 다룸에 있어 **객체의 확장은 개방적으로, 객체의 수정은 폐쇄적**으로 대하는 원칙이다.

조금 더 간단하게 말하자면 기능이 변하거나 확장은 가능하지만, 해당 기능의 코드는 수정하면 안된다는 뜻이다.

이처럼 개방-폐쇄 원칙은 각 객체의 모듈화와 정보 은닉의 올바른 구현을 추구하며, 이를 통해 객체 간의 의존성을 최소화하여 코드 변경에 따른 영향력을 낮추기 위한 원칙이다.

## 코드로 보는 예제

`Animal` 클래스를 만들고 `Cat` 일때는 `meow` `Dog`일때는 `bark`라고 출력하는 함수를 만들어보자.

```ts
class Animal {
  constructor(type: string) {
    this.type = type;
  }
}
function hey(animal: Animal) {
  if (animal.type === 'Cat') {
    console.log('meow');
  } else if (animal.type === 'Dog') {
    console.log('bark');
  } else {
    console.error('error');
  }
}
const kitty = new Animal('Cat');
const bingo = new Animal('Dog');
const cow = new Animal('Cow');
hey(kitty); //meow
hey(bingo); //bark
hey(cow); //error
```

Animal 클래스를 만들었지만 Cow와 Sheep에 대해서 정의가 없기 때문에 `Cow`와 `Sheep`이 추가되면 error가 발생한다.

개방-폐쇄 원칙이란 **객체의 확장에는 Open 객체의 수정에는 Close**가 되어야 된다고 했다. 하지만 Cow와 Sheep이 추가되면 코드를 수정해야 한다.

이를 어떻게 해결할 수 있을까? 답은 추상클래스나 인터페이스를 사용하여 해결한다.  
개방-폐쇄 원칙을 준수하는 인터페이스를 만들어보자.

```ts
abstract class Animal {
  //추상 메서드 정의
  public abstract speak(): void;
}

class Cat extends Animal {
  speak() {
    console.log('meow');
  }
}

class Dog extends Animal {
  speak() {
    console.log('bark');
  }
}

class Cow extends Animal {
  speak() {
    console.log('moo');
  }
}

class Sheep extends Animal {
  speak() {
    console.log('ummee');
  }
}

function hey(animal: Animal) {
  animal.speak();
}

const kitty = new Cat();
const bingo = new Dog();
const cow = new Cow();
const sheep = new Sheep();
hey(kitty); //meow
hey(bingo); //bark
hey(cow); //moo
hey(sheep); //ummee
```

위 코드는 개방-폐쇄 원칙을 준수한다. `Animal` 추상 클래스를 만들고 각각의 동물들은 `Animal`클래스를 상속 받는다. 그리고 `hey`함수는 `speak` 함수를 실행한다.

100개 1000개의 객체가 추가되어도 **확장**이 가능하고 hey 함수는 **수정하지 않아도 된다.**

이처럼 **확장**에 대해 **Open** 되어있고 **수정** 에 대해 **Close** 되어있다.
