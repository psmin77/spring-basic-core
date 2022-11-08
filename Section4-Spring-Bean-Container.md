### 스프링 컨테이너
- 일반적으로 ApplicationContext(interface)를 말함
  - 자바 설정 클래스(어노테이션 기반) 
  - XML 기반

### 스프링 컨테이너 생성 과정
- 스프링 컨테이너 생성(AppConfig.class)
- 스프링 빈 등록 
  - 빈 이름은 모두 달라야 함
- 스프링 빈 의존관계 설정 준비
- 스프링 빈 의존관계 설정 완료(DI 주입)

### 스프링 빈
- getBeanDefinitionNames() : 등록된 모든 빈의 이름 조회
- getBean("빈 이름", 타입) :  빈 이름으로 빈 객체(인스턴스) 조회(빈 이름 생략 가능)
- getBeansOfType(타입) : 해당 타입의 빈 객체를 모두 조회
- 상속 관계: 부모 타입으로 조회하면 모든 자식 타입도 함께 조회함
- 부모 타입으로 조회 시 여러 자식이 있는 경우,
  - 빈 이름을 지정하여 조회
  - 특정 하위 타입(자식 객체의 타입)으로 조회

### BeanFactory
- 스프링 컨테이너의 최상위 인터페이스
- 스프링 빈을 관리하고 조회하는 역할
- getBean() 제공
- 대부분 직접 사용하지 않고 ApplicationContext를 통해 사용함 


### ApplicationContext
![](https://velog.velcdn.com/images/psmin77/post/2c7284bf-934b-4699-8635-9ab5d78b8a0d/image.png)
- BeanFactory 기능을 모두 상속받아 제공
- 빈 관리 기능(BeanFactory) 외 MessageSource, EnviromentCapable 등 기타 부가 기능을 제공함

### 스프링 빈 설정 메타 정보 (BeanDefinition)
- 스프링은 다양한 형식 설정이 가능함(자바, XML, Groovy 등)
  - 추상화된 메타 정보(BeanDefinition)를 기반으로 스프링 빈을 생성하기 때문에 가능
- BeanClassName, FactoryBeanName, Scope 등의 정보를 가지고 있음
<br>

> 
[[출처] 스프링 핵심 원리 - 기본편, 김영한](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)
