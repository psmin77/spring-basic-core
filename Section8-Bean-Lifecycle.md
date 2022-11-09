### 빈 생명주기 콜백
- 데이터베이스 커넥션풀이나 네트워크 소켓과 같이 애플리케이션 초기화와 종료 작업이 필요한 경우
- 스프링 빈의 이벤트 라이프사이클
  - 스프링 컨테이너 생성
  - 스프링 빈 생성
  - 의존관계 주입
  - 초기화 콜백
  - 사용
  - 소멸 전 콜백
  - 종료
- cf. 객체의 생성과 초기화는 분리해야 함
(생성자에서 파라미터로 초기화하는 것은 권장하지 않음)

### 빈 생명주기 콜백 방법
- 인터페이스 InitializingBean, DisposableBean
  - implements InitializingBean, DisposableBean
  - @Override afterPropertiesSet(),destroy()
  - 스프링 전용 인터페이스에 의존함
  - 초기화/소멸 메서드 이름을 변경할 수 없음
  - 외부 라이브러리에 적용할 수 없음
  - 거의 사용하지 않음

- 빈 설정 초기화, 종료 메서드 지정
  - @Bean(initMethod = "init(메서드명)", destroyMethod = "close(메서드명)") 
  - 메서드 이름 설정 가능
  - 스프링 코드에 의존하지 않음
  - 외부 라이브러리에도 적용 가능
  - 종료 메서드에는 추론(destryMethod="(inferred)") 기본값으로 설정되어 있음 
    - close/shutdown과 비슷한 이름의 메서드를 종료 시에 자동으로 호출함
    - 사용하지 않을 경우 destroyMethod="" 공백으로 지정

- @PostConstruct, @PreDestroy 어노테이션
  - 최신 스프링에서 권장
  - 초기화, 종료 시 호출할 메서드에 설정
  - 스프링 종속 기술이 아닌 자바 표준 기술(javax)
  - 외부 라이브러리에서는 사용하지 못함 -> @Bean 설정

=> 기본적으로 어노테이션 설정 권장, 외부 라이브러리 등과 같이 필요한 경우에 @Bean 설정
<br>

> 
[[출처] 스프링 핵심 원리 - 기본편, 김영한](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)
