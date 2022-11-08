### 싱글톤 패턴
- 순수한 DI 컨테이너는 요청할 때마다 새로운 객체를 생성함 
  - 메모리 낭비
- 싱글톤 패턴은 클래스의 인스턴스를 하나만 생성하여 공유하는 디자인 패턴
- 싱글톤 패턴 적용 방법
~~~java
public class SingletonService {

// 1. instance를 static 객체로 미리 생성함
private static final SingletonService instance = new SingletonService();

// 2. getInstatnce() 메서드를 통해서만 조회 가능
public static SingletonService getInstance() {
    return instance;
}

// 3. private 생성자를 선언하여 외부에서 new 객체 생성을 할 수 없음
private SingletonService() {}
~~~

- 싱글톤 패턴의 문제점
  - 싱글톤 패턴을 구현하는 코드가 많아짐
  - 구체 클래스에 의존함 -> DIP 위반 -> OCP 위반할 가능성이 높아짐
  - 유연성이 떨어지는 등의 단점
  
### 싱글톤 컨테이너![](https://velog.velcdn.com/images/psmin77/post/2bd47447-448e-49e5-976b-413dd152fa17/image.png)
- 스프링은 스프링 컨테이너를 통해 객체 인스턴스를 싱글톤으로 관리함
  - 싱글톤 컨테이너 / 싱글톤 레지스트리
- 싱글톤 방식의 주의점
  - 무상태(stateless)로 설계해야 한다
  - 특정 클라이언트에 의존하거나 값을 변경하는 필드가 있으면 안됨(읽기만 가능하도록)
  - 필드 대신 공유되지 않는 지역변수, 파라미터 등을 사용해야 함

### @Configuration과 싱글톤
- 스프링은 CGLIB라는 바이트코드 조작 라이브러리를 사용하여, AppConfig 자체가 아니라 AppConfig를 상속받은 임의의 클래스를 만들어 빈으로 등록함
  - 기본적으로 싱글톤 보장
- 필요한 경우가 아니면, 스프링 설정 정보에는 항상 @Configuration를 사용해야 함
<br>

> 
[[출처] 스프링 핵심 원리 - 기본편, 김영한](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)
