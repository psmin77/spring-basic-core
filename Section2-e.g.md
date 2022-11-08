### 비즈니스 요구사항과 설계
- 회원
  - 회원 가입과 회원 조회를 할 수 있다
  - 회원 등급은 일반과 VIP가 있다
  - 회원 데이터는 자체 DB와 외부 시스템 연결 중 미확정이다

- 주문과 할인
  - 회원 등급에 따라 할인 정책을 적용한다
  - VIP는 1000원을 할인해주는 고정 할인을 적용한다
  - 단, 위 할인 정책은 변경 가능성이 높고 아예 적용하지 않을 수도 있다(미확정)

### 회원 도메인
![](https://velog.velcdn.com/images/psmin77/post/06b2337a-bad4-4698-85f3-9dc2076ebc0c/image.png)
- 회원 도메인 설계 
  - Grade(Basic, VIP), Member(id, name, grade)
  - MemberService(join, findMember) 
    - MemberServiceImpl
  - MemberRepository(save, findById) 
    - MemoryMemberRepository

### 주문과 할인 도메인
![](https://velog.velcdn.com/images/psmin77/post/8099a7cf-7ef3-4a0c-98a5-0715790f1ccc/image.png)
- 주문과 할인 도메인 설계
  - Order(memberId, itemName, itemPrice, discountPrice) : 회원아이디, 주문아이템, 할인된 가격
  - DiscountPolicy.discount(member, price) 
    - FixDiscountPolicy: VIP등급인 경우, price에서 -1000원 계산
  - OrderService.createOrder(memberId, itemName, itemPrice)
    - OrderServiceImpl
      - 회원조회(MemberServiceImpl.findById) 
      - 할인적용(FixDiscountPolicy.createOrder)
      - 주문결과 반환(return new Order)
      
<br>

> 
[[출처] 스프링 핵심 원리 - 기본편, 김영한](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)
