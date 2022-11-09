### 의존관계 주입 방법
#### 생성자 주입
~~~java
@Component
public class OrderServiceImpl implements OrderService {
    private final MemberRepository memberRepository;
    private final DiscountPolicy discountPolicy;
    
    @Autowired
    public OrderServiceImpl(MemberRepository memberRepository, 
                            DiscountPolicy discountPolicy) {
        this.memberRepository = memberRepository;
        this.discountPolicy = discountPolicy;
    }
}
~~~
- 일반적으로 주입하는 방법 -> 사용 권장 
  - 대부분 의존관계 주입은 변경할 일이 없음
  - final 키워드 사용 가능
- 생성자 호출 시점에 한 번만 실행
- 생성자가 1개인 경우, @Autowired 생략해도 자동 주입됨(스프링 빈인 경우)
- 불변, 필수인 의존관계에 사용
- cf. 롬복 @RequiredArgsConstructor 사용하면 final 필드를 모두 생성자로 만들어줌

#### 수정자 주입(setter 주입)
~~~java
@Component
public class OrderServiceImpl implements OrderService {
    private MemberRepository memberRepository;

    @Autowired
    public void setMemberRepository(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }
}
~~~
- 필드 값을 변경하는 수정자(setter) 메서드를 통해 주입
- 선택, 변경 가능성이 있는 의존관계에 사용
- 주입할 대상이 없으면 오류 발생, 필요한 경우 required=false 지정
- 기본적으로 생성자 주입을 사용하고, 필요한 경우 수정자 방식 권장

#### 필드 주입
~~~java
@Component
public class OrderServiceImpl implements OrderService {
    @Autowired
    private MemberRepository memberRepository;
    @Autowired
    private DiscountPolicy discountPolicy;
}
~~~
- 필드에 바로 주입하는 방법
- 사용 지양(테스트 코드나 설정 등에서만 사용할 것)
- DI 프레임워크가 없으면 외부에서 변경이 불가능하여 테스트가 어려움 

#### 일반 메서드 주입
- 메서드를 통해 주입하는 방법
- 생성자와 유사함, 잘 사용하지 않음

### 옵션 처리 
- @Autowired(required=false): 대상이 없으면 호출 안됨
- org.springframework.lang.@Nullable: 대상이 없으면 null 입력
- Optional<>: 대상이 없으면 Optional.empty 입력

### 여러 개의 빈 조회
- @Autowired는 타입(Type)으로 조회함 => 2개 이상일 때 오류 발생
- @Autowired 필드명, 파라미터명 매칭
~~~ java
/* (EX) DiscountPolicy 타입 2개일 때,
     - FixDiscountPolicy 
     - RateDiscountPolicy
 1. 타입(DiscountPolicy)
 2. 필드명(rateDiscountPolicy)
 3. 파라미터명 순으로 조회 
*/

@Autowired
private DiscountPolicy rateDiscountPolicy
@Qualifier("이름")

@Component
@Qualifier("mainDiscountPolicy")
public class RateDiscountPolicy implements DiscountPolicy {}
/
@Component
@Qualifier("fixDiscountPolicy")
public class FixDiscountPolicy implements DiscountPolicy {}
/
@Autowired
public OrderServiceImpl(MemberRepository memberRepository,
                  @Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) {
    this.memberRepository = memberRepository;
    this.discountPolicy = discountPolicy;
}
~~~
- @Primary : 우선순위 설정
- 동시에 사용할 때는 @Qualifier 우선권 -> @Primary 순으로 동작함 
- 어노테이션 직접 설정 가능


### 모든 빈 조회
- Map, List 사용하여 모든 타입 주입한 뒤, 조회 및 사용 가능
~~~java
static class DiscountService {
        private final Map<String, DiscountPolicy> policyMap;
        private final List<DiscountPolicy> policies;
...
}
~~~
- 스프링 컨테이너를 생성하면서 스프링 빈을 자동으로 등록함

~~~java
AnnotationConfigApplicationContext(AutoAppConfig.class, DiscountService.class);
~~~
- AutoAppConfig와 DiscountService를 파라미터로 넘기면서 스프링 빈 자동 등록

### 올바른 실무 운영 기준
- 기본으로 자동 기능을 사용 권장
- 업무 로직 빈(핵심 비즈니스 로직 서비스 등) / 기술 지원 빈(AOP, 공통 로그 처리 설정 등)
- 기술 지원 로직은 수동 빈으로 등록하여 잘 보이게 하는 것이 좋음
<br>

> 
[[출처] 스프링 핵심 원리 - 기본편, 김영한](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)
