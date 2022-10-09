# spring-basic-core
[인프런 / 김영한] 스프링 핵심 원리-기본편

### 스프링 핵심 원리
- 객체 지향 프로그래밍  
   - 다형성(Polymorphism)    
      1. 역할과 구현 분리  
      2. 다형성의 본질  
   - 객체 지향 설계의 5가지 원칙(SOLID) / 클린코드, 로버트 마틴  
      1. SRP(Single Responsibility Principle) : 단일 책임 원칙  
      2. OCP(Open/Closed Principle) : 개방 폐쇄 원칙  
      3. LSP(Liskov Substitution Principle) : 리스코프 치환 원칙  
      4. ISP(Interface Segregation Principle) : 인터페이스 분리 원칙  
      5. DIP(Dependency Inversion Principle) : 의존관계 역전 원칙  
      => 다형성만으로는 OCP, DIP 원칙을 지킬 수 없는 등의 한계
    - DI(Dependency Injection, 의존관계, 의존성 주입): DI 컨테이너 제공
    

	=> 스프링이 지원하는 기술로 객체 지향 프로그래밍 구현
    
### 스프링 핵심 기능
- 스프링 컨테이너, 빈
- 싱글톤
- 컴포넌트 스캔
- 의존관계 자동 주입
- 빈 생명주기 콜백
- 빈 스코프
