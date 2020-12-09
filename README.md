## CHAPTER 02. 스프링부트에서 테스트 코드를 작성하자

### **TDD**

- 테스트가 주도하는 개발
- 레드 그린 사이클
  - Red: 항상 실패하는 테스트를 먼저 작성
  - Green: 테스트가 통과하는 프로덕션 코드 작성
  - Refactor: 테스트가 통과하면 프로덕션 코드를 리팩토링
</br>


### **단위 테스트**

- 기능 단위의 테스트 코드를 작성하는 것
- 테스트 코드의 이점
  - 개발단계 초기에 문제를 발견하게 도와줌
  - 개발자가 나중에 코드를 리팩토링하거나 라이브러리 업그레이드 등에서 기존 기능이 올바르게 작동하는지 확인할 수 있음(예, 회귀 테스트)
  - 기능에 대한 불확실성을 감소시킬 수 있음
  - 시스템에 대한 실제 문서를 제공함
    즉, 단위 테스트 자체가 문서로 사용할 수 있음

</br></br>



## CHAPTER 03. 스프링 부트에서 JPA로 데이터베이스 다뤄보자

- MyBatis, iBatis - SQL Mapper(쿼리를 매핑) 

- JPA - ORM(객체를 매핑)
</br>


### **JPA 소개**

- SQL 사용시 문제
  - 단순 반복 작업의 문제
  - 패러다임 불일치 문제(관계형 데이터베이스와 객체지향 프로그래밍 언어의 패러다임이 서로 다른데, 객체를 데이터베이스에 저장하려고 하니 문제 발생)
- JPA는 서로 지향하는 바가 다른 2개 영역을 중간에서 패러다임 일치를 시켜주기 위한 기술
- 개발자는 객체지향적으로 프로그래밍을 하고, JPA가 관계형 데이터베이스에 맞게 SQL을 대신 생성해서 실행
- SQL에 종속적인 개발을 하지 않아도 됨
- 생산성 향상, 유지 보수가 편함
</br>


### **Spring Data JPA**

- JPA는 인터페이스로서 자바 표준 명세서
- 추상화시킨 Spring Data JPA라는 모듈을 이용하여 JPA 기술을 다룸
  관계: JPA <- Hibernate <- Spring Data JPA
- Spring Data JPA가 등장한 이유
  - 구현체 교체의 용이성: Hibernate 외에 다른 구현체로 쉽게 교체하기 위함
  - 저장소 교체의 용이성: 관계형 데이터베이스 외에 다른 저장소로 쉽게 교체하기 위함
</br>


### **Spring 웹 계층**

![web](C:\Users\LEE\Desktop\web.png)

**Web Layer**

- 흔히 사용하는 컨트롤러(@Controller)와 JSP/Freemarker 등의 뷰 템플릿 영역
- 필터(@Filter), 인터셉터, 컨트롤러 어드바이스(@ControllerAdvice) 등 외부 요청과 응답에 대한 전반적인 영역



**Service Layer**

- @Service에 사용되는 서비스 영역
- 일반적으로 Controller와 Dao의 중간 영역에서 사용
- @Transactionl이 사용되어야 하는 영역



**Repository Layer**

- Database와 같이 데이터 저장소에 접근하는 영역



**Dtos**

- Dto(Data Transfer Object)는 계층간에 데이터 교환을 위한 객체를 이야기하며 Dtos는 이들의 영역



**Domain Model**

- 도메인이라 불리는 개발 대상을 모든 사람이 동일한 관점에서 이해할 수 있고 공유할 수 있도록 단순화시킨 것을 도메인 모델이라고 함
- @Entity가 사용된 영역
- 다만, 무조건 데이터베이스의 데이블과 관계가 있어야만 하는 것은 아님
- VO처럼 값 객체들도 이 영역에 해당
- 비즈니스 처리를 담당해야 하는 곳

</br>



### **Bean을 주입받는 방식**

- @Autowired
- setter
- 생성자

생성자로 주입받는 방식을 권장 (@Autowired는 권장하지 않음)

생성자로 Bean 객체를 받도록 하면 @Autowired와 동일한 효과를 볼 수 있음

-> @RequiredArgsConstructor: final이 선언된 모든 필드를 인자값으로 하는 생성자를 롬복의  @RequiredArgsConstructor가 대신 생성해줌

이점: 해당 클래스의 의존성 관계가 변경될 때마다 생성자 코드를 계속해서 수정하는 번거로움 해결


</br></br></br>


출처: 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 - 이동욱님
