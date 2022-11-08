### 객체 지향 프로그래밍
- 프로그램을 여러 개의 독립된 단위, 객체들의 모임으로 파악하여 서로 메시지를 주고받거나 데이터를 처리할 수 있다. (협력)
- 유연하고 변경이 용이하다.
- 특징
  - 추상화
  - 캡슐화
  - 상속
  - **다형성***

### 다형성(Polymorphism)![](https://velog.velcdn.com/images/psmin77/post/201f4254-bd02-4f81-91ad-1908217d2f8c/image.png)
- 역할과 구현 분리
  - 역할(인터페이스) <=> 구현(구현 클래스 또는 객체)
  - 클라이언트는 역할(인터페이스)만 알고, 구현 대상을 변경해도 영향을 받지 않는다.
(운전자가 자동차 모델을 바꾸거나 공연에서 배우를 바꾸듯이)
- 다형성의 본질
  - 클라이언트(구현)는 변경하지 않고, 서버의 구현 기능을 유연하게 변경할 수 있다.

### 객체 지향 설계의 5가지 원칙(SOLID) - 클린코드
- SRP(Single Responsibility Principle) : 단일 책임 원칙
  - 한 클래스는 하나의 책임만 가져야 한다
  (변경이 있을 때 파급 효과가 적어야 함)
- OCP(Open/Closed Principle) : 개방 폐쇄 원칙
  - 확장에는 열려 있지만 변경에는 닫혀 있어야 한다
- LSP(Liskov Substitution Principle) : 리스코프 치환 원칙
  - 하위 클래스는 인터페이스 규약을 지켜야 한다
  (자동차 엑셀을 뒤로 가는 기능으로 구현하면 LSP 위반)
- ISP(Interface Segregation Principle) : 인터페이스 분리 원칙
  - 특정 클라이언트를 위한 여러 인터페이스를 분리
  - 개별 인터페이스를 변경해도 다른 인터페이스에 영향을 주지 않는다
(자동차 -> 운전 / 정비 인터페이스로 분리)
- DIP(Dependency Inversion Principle) : 의존관계 역전 원칙
  - 구현이 아닌 추상화(Role, 역할=인터페이스)에 의존해야 한다
<br>

- 다형성만으로는 OCP, DIP 원칙을 지킬 수 없는 등의 한계 
- 스프링이 지원하는 기술로 객체 지향 프로그래밍 구현
  - DI(Dependency Injection, 의존관계, 의존성 주입), DI 컨테이너 제공 등

<br>

> 
[[출처] 스프링 핵심 원리 - 기본편, 김영한](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)
