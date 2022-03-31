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
