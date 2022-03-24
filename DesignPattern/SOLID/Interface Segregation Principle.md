# 인터페이스 분리 원칙(Interface Segregation Principle)

## 인터페이스 분리 원칙이란?

객체는 자신이 호출하지 않는 메소드에 의존하지 않아햐 한다.

구현할 객체에 무의미한 메소드의 구현을 방지하기 위해서 반드시 필요한 메소드만을 상속/구현 하도록 권고한다. 만약 상속할 객체의 규모가 너무 크다면, 해당 객체의 메소드를 작은 인터페이스 단위로 나누는게 좋다.

예를들어, 스마트폰이라는 객체가 있다고 가정하자. 이 스마트폰은 최신에 나온 덕분에 무선 충전, AR 뷰어, 생체인식 등의 다채로운 기능이 있다고 하자.

이를 기반으로 갤럭시 S20을 구현하면 스마트폰 객체 동작 모두가 충족되기 떄문에 ISP가 만족된다. 하지만 이 인터페이스를 S2에 적용하면 안쓰는 기능들이 구현해야 하는 낭비가 발생한다. 때문에 ISP가 만족되지 못한다.

## 코드로 보는 예제

```java
abstract public class SmartPhone
{
    public void call(String number)
    {
        System.out.println(number + " 통화 연결");
    }

    public void message(String number, String text)
    {
        System.out.println(number + ": " + text);
    }

    public void wirelessCharge()
    {
        System.out.println("무선 충전");
    }

    public void ar()
    {
        System.out.println("AR 기능");
    }

    abstract public void biometrics();
}
```

위와 같이 스마트폰 객체에 최신 기능을 다 넣은 클래스를 구현하였다. 하지만 S20 클래스를 만들면 위의 모든 기능을 사용할 수 있지만 S2를 만들 때는 하나하나 예외처리를 해줘야한다.

```java
public class S2 extends SmartPhone
{

    @Override
    public void wirelessCharge()
    {
        System.out.println("지원 불가능한 기기");
    }

    @Override
    public void ar()
    {
        System.out.println("지원 불가능한 기기");
    }

    @Override
    public void biometrics()
    {
        System.out.println("지원 불가능한 기기");
    }
}
```

## 인터페이스 분리 원칙을 준수한 코드

모든 스마트폰에서 적용되는 동작들만 가지고 구현해야한다. 모든 스마트폰은 전화하기, 메세지보내기 기능이 가능하므로 이 두가지 기능만 구현한다.

```java
public class SmartPhone
{
    public void call(String number)
    {
        System.out.println(number + " 통화 연결");
    }

    public void message(String number, String text)
    {
        System.out.println(number + ": " + text);
    }
}
```

그리고 추가 기능들은 인터페이스로 구현하여 상속 받는다.

```java

// 무선충전 인터페이스
public interface WirelessChargable
{
    void wirelessCharge();
}
// AR 인터페이스
public interface ARable
{
    void ar();
}
// 생체인식 인터페이스
public interface Biometricsable
{
    void biometrics();
}
```

**각 기능은 인터페이스 단위로 나누어졌음을 주목하자**

그리고 S2와 S20은 이를 상속받아 사용한다.

```java
public class S20 extends SmartPhone implements WirelessChargable, ARable, Biometricsable
{

    @Override
    public void wirelessCharge()
    {
        System.out.println("무선충전 기능");
    }


    @Override
    public void ar()
    {
        System.out.println("AR 기능");
    }


    @Override
    public void biometrics()
    {
        System.out.println("생체인식 기능");
    }
}
```

```java
public class S2 extends SmartPhone
{

    @Override
    public void message(String number, String text)
    {
        System.out.println("In S2");

        super.message(number, text);
    }
}
```

이제 S2에서는 특수기능이 구현되지 않았으므로 불필요한 함수를 가지고 있지 않아도 된다.
