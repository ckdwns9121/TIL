# Singleton

# 싱글톤 패턴이란?

프로젝트가 실행중에 **오직 하나의 오브젝트만 생성**이 되도록 하는 디자인 패턴

```java
public class Singleton {

    private static Singleton instance = new Singleton();

    private Singleton() {
        // 생성자는 외부에서 호출못하게 private 으로 지정해야 한다.
    }

    public static Singleton getInstance() {
        return instance;
    }

    public void say() {
        System.out.println("hi, there");
    }
}
```

# 싱글톤 패턴을 사용하는 이유

- 메모리 낭비 방지
- 다른 클래스간 데이터 공유가 쉬움

# 싱글톤 패턴의 문제점

싱글톤 패턴을 구현하는 코드 자체가 많이 필요하다. 정적 팩토리 메서드에서 객체 생성을 확인하고 생성자를 호출하는 경우에 멀티스레딩 환경에서 발생할 수 있는 동시성 문제 해결을 위해 `syncronized` 키워드를 사용해야한다.

테스트하기 어렵다. 싱글톤 인스턴스는 자원을 공유하고 있기 때문에 테스트를 하려면 매번 인스턴스를 초기화 시켜주어야 한다.

의존관계상 클라이언트가 구체 클래스에 의존하게 된다.
