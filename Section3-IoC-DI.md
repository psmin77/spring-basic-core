### 새로운 할인 정책 적용과 문제점

```java
public class OrderServiceImpl implements OrderService {
  //    private final DiscountPolicy discountPolicy = new FixDiscountPolicy();
      private final DiscountPolicy discountPolicy = new RateDiscountPolicy();
  }
```
- 새로운 할인 정책으로 변경할 때, 클라이언트 코드인 OrderServiceImpl의 코드도 변경해야 하는 문제 발생 --> OCP 위반
- OrderServiceImpl이 DiscountPolicy뿐만 아니라 FixDiscountPolicy에도 의존 --> DIP 위반

### 관심사 분리
#### AppConfig
~~~ java
public class AppConfig {
    public MemberService memberService() {
        return new MemberServiceImpl(memberRepository());
    }
    public OrderService orderService() {
        return new OrderServiceImpl(memberRepository(),discountPolicy());
    }
    // 회원 저장소 의존관계 주입
    public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
        // return new DbMemberRepository();
    }
    // 할인 정책 의존관계 주입
    public DiscountPolicy discountPolicy() {
        return new FixDiscountPolicy();
        // return new RateDiscountPolicy();
    }
}
~~~
![](https://velog.velcdn.com/images/psmin77/post/b055089d-a48e-4055-aded-a122a5d3d999/image.png)
- 구체적인 구현 객체를 생성하고 연결하는 별도의 설정 클래스를 만들어 관심사를 분리
- 전체 영역이 사용 영역과 구성 영역으로 분리되어, 구성 영역에서만 코드를 변경하고 영향을 받음
- AppConfig는 일종의 공연기획자 역할

### 좋은 객체 지향 설계의 원칙
- SRP 단일 책임 원칙
- DIP 의존관계 역전 원칙
- OCP 확장에는 열려 있으나 변경에는 닫혀 있어야 함
--> 3가지 원칙 적용됨

### 제어의 역전(Inversion of Control, IoC)
- 기존 코드에서는 구현 객체가 스스로 서버 구현 객체를 생성, 연결, 실행하여 직접 흐름을 제어했지만, AppConfig를 통해 프로그램의 제어 흐름을 외부에서 관리하게 됨 --> 제어의 역전
- 구현 객체는 어떤 프로그램이 생성되어 주입되어도 자신의 로직을 실행하는 역할만 담당

### 의존관계 주입(Dependency Injection)
- 프로그램을 실행하지 않고 import 코드만으로 파악할 수 있는 정적인 클래스 의존 관계
- 실행 시점(런타임)에 결정되는 동적인 객체(인스턴스) 의존관계로 분리
- 외부에서 구현 객체를 생성하여 클라이언트에 전달하고, 클라이언트와 서버의 의존관계가 연결됨 --> 의존관계 주입(DI)
- 의존관계 주입을 통해 정적인 클래스 의존관계는 변경에 영향을 받지 않음

### IoC 컨테이너, DI 컨테이너
- AppConfig와 같이 구현 객체를 생성하고 관리하여 의존관계를 주입하는 기능 
- IoC 컨테이너, DI 컨테이너 또는 어셈블러, 오브젝트 팩토리 등으로 불리기도 함
- AppConfig 대신 스프링 컨테이너(ApplicationContext)를 적용할 수 있음
<br>

> 
[[출처] 스프링 핵심 원리 - 기본편, 김영한](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)
