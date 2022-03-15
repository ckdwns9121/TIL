# 리스코프 치환 원칙(Liskov Substitution Principle)

## 리스코프 치환 원칙이란?

상위 타입의 객체를 하위 타입의 객체로 치환해도 동작에 문제가 없어야 한다. 즉 B가 A의 자식일 때 A타입을 B로 치환해도 문제없이 동작해야 한다.

## 코드로 보는 예제

고양이들도 길고양이가 있고 집에서 키우는 고양이가 있다. 그렇다고 한들 고양이가 가지는 특성은 다 똑같다.

```ts
class Cat {
  speak() {
    console.log('meow');
  }
}
class BlackCat extends Cat {
  speak() {
    console.log('black meow');
  }
}

class HomeCat extends Cat {
  speak() {
    console.log('home meow');
  }
}

let cat = new Cat();
cat.speak(); // meow

cat = new BlackCat();
cat.speak(); // black meow

cat = new HomeCat();
cat.speak(); // home meow
```

위 처럼 어떤 고양이로 대체 하더라도 에러가 발생하지 않는다. 하지만 고양이에 생선을 넣는다면 어떻게 될까?

```ts
class Cat {
  speak() {
    console.log('meow');
  }
}
class Fish extends Cat {
  speak() {
    console.error('fish cannot speak');
  }
}

let cat = new Cat();
cat.speak(); // meow

cat = new Fish();
cat.speak(); // error: fish cannot speak
```

이처럼 고양이를 생선으로 대체할 수 없다. 이 코드는 리스코프 치환 원칙을 위배하는 코드이다.

이를 해결하기 위해서는 **처음부터 전체적인 클래스 구조를 잘 설계 해야한다.**
