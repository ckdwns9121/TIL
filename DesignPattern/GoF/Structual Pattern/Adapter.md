# Adapter

한 클래스의 인터페이스를 클라이언트에서 사용하고자 하는 다른 인터페이스로 변환하는 디자인 패턴

어댑터 패턴을 이용하면 인터페이스 호환성 문제 때문에 같이 쓸 수 없는 클래스들을 연결해서 쓸 수 있다.

# UML

![UML](./asset//adapter-uml.jpeg);

- Client : 써드파티 라이브러리나 외부 시스템을 사용하려는 쪽

- Adaptee: 써드파티 라이브러리나 외부 시스템

- TargetInterface: Adapter가 구현 하려는 인터페이스. 클라이언트는 Target Interface를 통해 Adaptee인 써드파티 라이브러리를 사용하게 된다.

- Adapter: client와 Adaptee 중간에서 호환성이 없는 둘을 연결시켜주는 역할을 담당한다.

# 어댑터 패턴의 호출 과정

![과정](./asset/adapter-pattern-2.png)

클라이언트는 Adapter에게 TargetInterface의 함수를 요청한다.

# 어댑터 패턴의 장 단점

## 장점

- 기존 인터페이스를 변경할 필요없이 어댑터만 구현하여 호환성을 갖출 수 있다.
- 새로운 코드의 기능을 기존 인터페이스와 일관되게 사용할 수 있다.

## 단점

- 상황에 따라 어댑터의 구현이 복잡해져 클라이언트가 인터페이스를 수정하는 방법이 더 나은 케이스가 될 수 있다.

# 어댑터 패턴을 언제 사용하는가?

- 기존 코드의 변경 없이 다른 인터페이스를 사용할 때
- 써드 파티 라이브러리를 기존 코드와 분리해 사용하기 위해 어댑터를 중간 역할로 사용한다.

# 예제 코드

```js
class Animal {
  constructor(species) {
    this.species = species;
  }

  walk() {
    return `${this.species} is walking...`;
  }
}

class Dog extends Animal {}

class Cat extends Animal {}

class FishAdapter extends Animal {
  constructor(fish) {
    super(fish);
    this.fish = fish;
  }

  walk() {
    return this.fish.swim();
  }
}

class Fish extends FishAdapter {
  swim() {
    return `${this.fish} is swimming...`;
  }
}

const dog = new Dog('dog');
const cat = new Cat('cat');

console.log(dog.walk()); // dog is walking...
console.log(cat.walk()); // cat is walking...

const fish = new Fish('fish');
const adaptedFish = new FishAdapter(fish);
console.log(adaptedFish.walk()); // fish is swimming...
```
