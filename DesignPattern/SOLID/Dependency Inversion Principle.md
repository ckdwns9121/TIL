# 의존성 역전 원칙(Dependency Inversion Principle)

## 의존성 역전 원칙이란?

**객체는 저수준 모듈보다 고수준 모듈에 의존해야 한다.**

- 고수준 모듈: 인터페이스와 같은 객체 형태나 추상적인 개념
- 저수준 모듈: 이미 구현된 객체

가급적 객체의 상속은 **인터페이스**를 통해 이루어져야 한다는 말이다.

## 코드로 보는 예제

동물원이 있다고 가정하자. 동물원에는 고양이, 강아지, 소 등등 많은 동물들이 있다.

```js
class Zoo {
  constructor(cat, cow, dog) {
    this.cat = cat;
    this.cow = cow;
    this.dog = dog;
  }
}
class Cat {}
class Cow {}
class Dog {}
```

위와 같이 동물원은 각각의 동물들을 생성자로 받고 추가한다. 하지만 동물들이 추가되면 동물원 생성자에 계속해서 추가해야하는 번거로움이 발생한다.

이는 각각의 동물들에 의존하고 있기 때문이다. 더욱더 `고수준의 인터페이스`에 의존하도록 만들자

## 의존성 역전 원칙을 준수하는 코드

동물이라는 인터페이스에 의존하도록 개선하였다.

```ts
interface Animal{
    speak: void()
}

class Zoo{
    constructor(){
        this.animal=[]
    }
    addAnimal(animal:Animal){
        this.animal.push(animal)
    }
}

let zoo = new Zoo();
let cat = new Cat();
let dog = new Dog();
zoo.addAnimal(cat)
zoo.addAnimal(dog)
```
