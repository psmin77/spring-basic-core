### 빈 스코프
- 빈이 존재할 수 있는 범위
- 스코프 종류
  - 싱글톤: 기본 스코프, 스프링 컨테이너의 시작과 종료까지 유지
  - 프로토타입
    - 스프링 컨테이너는 프로토타입 빈의 생성과 의존관계 주입, 초기화까지만 관여함(관리,소멸 X)
    - 요청 시마다 항상 새로운 인스턴스를 생성하여 반환
    - 많이 사용하지는 않음
  - 웹 관련 스코프
    - request: 웹 요청이 들어오고 나갈 때까지만 유지
    - session: 웹 세션이 생성되고 종료될 때까지 유지
    - application: 웹 서블릿 컨텍스트와 같은 범위로 유지
- 컴포넌트 스캔 자동 등록: @Scope("singleton / prototype") 

### 싱글톤 빈과 프로토타입 동시 사용
- 싱글톤 안에서 프로토타입을 사용하는 경우, 생성 시점에만 의존 관계를 주입 받기 때문에 같은 프로토타입 빈을 계속 싱글톤처럼 사용하는 문제 발생

- 해결 방법
~~~java
@Autowired
private ObjectProvider<PrototypeBean> prototypeBeanProvider;

public void logic() {
    PrototypeBean prototypeBean = prototypeBeanProvider.getObject();
    ...
}
~~~
- ObjectFactory, ObjectProvider
  - logic() 메서드 호출 시마다 provider를 사용해 새로운 프로토타입 빈을 생성함
  - 단위 테스트나 Mock 코드를 만들기 쉬움


~~~java
// implementation 'javax.inject:javax.inject:1' gradle 추가

@Autowired
private Provider<PrototypeBean> provider;

public void logic() {
    PrototypeBean prototypeBean = provider.get();
    ...
}
~~~
- Provider (JSR-330)
  - 자바 표준 기능, 단위 테스트나 Mock 코드를 만들기 쉬움
  - 스프링에 의존하지 않음
- 스프링을 사용하는 경우 ObjectProvider 사용, 다른 프레임워크에서도 사용해야 한다면 JSR-330 Provider 권장

### 웹 스코프
- request: HTTP request 요청 시마다 할당되는 스코프
- ObjectProvider.getObject()를 사용하여 request scope 빈의 생성을 지연할 수 있음
![](https://velog.velcdn.com/images/psmin77/post/20b3e325-052d-45c8-af46-40ac85dfa421/image.png)
- 프록시 @Scope(value = "request", proxyMode = ScopedProxyMode.TARGET_CLASS)
  - CGLIB 라이브러리를 통해 임시 프록시 객체를 미리 주입함
  - 프록시 객체에는 실제 빈을 요청하는 위임 로직을 가지고 있음
  - 실제 요청 시 위 로직을 호출
  - 실제 원본 객체를 상속 받아 만들어졌기 때문에 원본으로 바로 대체 가능 -> 다형성
<br>

> 
[[출처] 스프링 핵심 원리 - 기본편, 김영한](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)
