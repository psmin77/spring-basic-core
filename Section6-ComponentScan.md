### 컴포넌트 스캔과 의존관계 자동 주입
#### @ComponentScan
~~~java
@Configuration
@ComponentScan(
    excludeFilters = @Filter(type = FilterType.ANNOTATION, 
                             classes = Configuration.class))
public class AutoAppConfig {
}
~~~
- @Component가 붙은 클래스를 모두 스캔하여 스프링 빈으로 등록
  - @Configuration이 붙은 설정 정보(ex. AppConfig)도 자동으로 등록되기 때문에  excludeFilter로 제외해야 함
- 빈 이름 표기는 첫 글자를 대문자로 사용하되, 맨 앞글자만 소문자로 표기
(카멜 표기, MemberService -> memberService)
- 빈 이름 직접 설정 가능 (@Bean (name="myName"))

#### @Autowired 의존관계 자동 주입![](https://velog.velcdn.com/images/psmin77/post/6b102af2-2b72-49d4-88fb-4a1c9ba9850e/image.png)
- 생성자에 @Autowired 설정하면 스프링 컨테이너가 자동으로 빈을 찾아서 주입함
- getBean(MemberService.class)와 같은 기능

### 탐색 위치
~~~java
@ComponentScan(
    basePackages = "hello.core",
}
~~~
- basePackages: 지정한 패키지를 탐색 시작 위치로 지정함
- basePackageClasses: 지정한 클래스를 탐색 시작 위치로 지정함
- 설정정보 클래스를 최상단 경로에 두고 basePackages를 생략하는 것을 권장(=스프링 기본 설정)

### 컴포넌트 스캔 기본 대상
- @Component
- @Controller: 스프링 MVC 컨트롤러에서 사용
- @Service: 스프링 비즈니스 로직에서 사용
- @Repository: 스프링 데이터 접근 계층에서 사용
- @Configuration: 스프링 설정 정보에서 사용, 스프링 빈이 싱글톤을 유지하도록 함

### 필터
- includeFilters: 컴포넌트 스캔 대상으로 추가함 
  - 많이 사용하지 않음
- excludeFilters: 컴포넌트 스캔 대상에서 제외함
- FilterType 옵션
  - ANNOTATION: 기본값, 어노테이션을 인식하여 동작
  - ASSIGNABLE_TYPE: 지정한 타입과 자식 타입을 인식해서 동작
  - ASPECTJ: AspectJ 패턴 사용
  - REGEX: 정규 표현식
  - CUSTOM: TypeFilter 인터페이스를 구현하여 사용

### 중복 등록과 충돌
- 동일한 스프링 빈 이름으로 중복 등록되는 경우
  - 자동 빈 등록 - 자동 빈 등록
    - onflictingBeanDefinitionException 발생
  - 수동 빈 등록 - 자동 빈 등록
    - 수동 빈 등록이 먼저 등록된 후, 다른 빈 Overriding
- 최근 스프링 부트에서는 충돌 발생이 기본값
  - spring.main.allow-bean-definition-overriding=true 설정 필요
 <br>

> 
[[출처] 스프링 핵심 원리 - 기본편, 김영한](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)
