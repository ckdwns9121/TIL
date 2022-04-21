# 전략(Strategy) 패턴

## 전략 패턴이란?

- 실행 중에 알고리즘을 선택할 수 있게 하는 행위 소프트웨어 디자인 패턴이다.
- 각 알고리즘을 캡슐화하며 이 알고리즘들을 해당 계열 안에서 상호 교체가 가능하게 만든다.
- 특정 컨텍스트에서 알고리즘을 별도로 분리하는 설계 방법

## 전략 패턴을 사용하는 이유

- 시스템이 커질 경우 메서드의 중복문제 해결
- OCP 위배 해결

## 전략 패턴 구현

선로를 따라 이동하는 버스가 개발된 상황에서 시스템이 유연하게 변경되고 확장될 수 있도록 전략 패턴을 사용해보자.

### 1. 전략 생성

현재 운송수단은 선로를 따라 움직이든지, 도로를 따라 움직이든지 두 가지 방법(전략)이 있다.

즉 움직이는 두 가지 전략에 대해 Strategy 클래스를 생성해보자. ( RailLoadStrategy, LoadStrategy )

그리고 두 클래스는 `move()` 메소드를 구현하여 어떤 경로로 움직이는지에 대해 구현한다.

또한 두 전략을 캡슐화 하기 위해서 `MovableStrategy` 인터페이스를 생성한다.
이렇게 캡슐화를 하는 이유는 운송수단에 대한 전략 뿐만 아니라, 다른 전략들(예를들어, 주유방식, 주차방식에 대한 전략 등)이 추가적으로 확장되는 경우를 고려한 설계이다.

이를 코드로 표현하면 다음과 같다

```java
public interface MovableStrategy {
    public void move();
}

public class RailLoadStrategy implements MovableStrategy{
    public void move(){
        System.out.println("선로를 통해 이동");
    }
}

public class LoadStrategy implements MovableStrategy{
    public void move() {
        System.out.println("도로를 통해 이동");
    }
}
```

### 2. 운송수단에 대한 클래스를 정의

기차와 버스 같은 운송 수단은 `move()` 메서드를 통해 움직일 수 있다. 그런데 이동 방식을 직접 메서드로 구현하지 않고, 어떻게 움직일 것인지에 대한 전략을 설정하여, 그 전략의 움직임 방식을 사용하여 움직이도록 한다.

전략을 설정하는 메서드인 `setMovableStrategy()` 구현

```java
public class Moving {
    private MovableStrategy movableStrategy;

    public void move(){
        movableStrategy.move();
    }

    public void setMovableStrategy(MovableStrategy movableStrategy){
        this.movableStrategy = movableStrategy;
    }
}

public class Bus extends Moving{

}
public class Train extends Moving{

}
```

### 3. Client를 구현

`Train`과 `Bus` 객체를 생성한 후에, 각 운송수단이 어떤 방식으로 움직이는지 설정하기 위해 `setMovableStrategy()` 메서드를 호출한다.

그리고 전략 패턴을 사용하면 프로그램 상으로 로직이 변경 되었을 때, 얼마나 유연하게 수정을 할 수 있는지 살펴보기 위해

선로를 따라 움직이는 버스가 개발되었다는 상황을 만들어 버스의 이동 방식 전략을 수정해보자.

```java
public class Client {
    public static void main(String args[]){
        Moving train = new Train();
        Moving bus = new Bus();

        /*
            기존의 기차와 버스의 이동 방식
            1) 기차 - 선로
            2) 버스 - 도로
         */
        train.setMovableStrategy(new RailLoadStrategy());
        bus.setMovableStrategy(new LoadStrategy());

        train.move();
        bus.move();

        /*
            선로를 따라 움직이는 버스가 개발
         */
        bus.setMovableStrategy(new RailLoadStrategy());
        bus.move();
    }
}

```
