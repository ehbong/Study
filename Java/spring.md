# Spring

* [스프링 부트 쉽게 환경 설정하기](https://start.spring.io/)

> 스프링의 주요 개념
> |대상|설명|
> |----|----|
> |DI(Dependency injection)|클래스 간 의존성을 주입해서 결합도를 낮춤|객체 참조|
> |IOC(Inversion of Control|의존성 관리를 위해 객체를 빈으로 생성하고 관리하는 컨테이너|
> |AOP(Aspect-Oriented Programming)|미들 웨어 처럼 공통로직을 분리해서 필요한 시점에 적용|
> |PSA(Portable Service Abstraction)|서비스를 추상화 해서 비슷한 기능을 가진 라이브러리를 일관 된 방식으로 사용|

### 의존성 관리
> maven
* [maven 의존성 라이브러리 검색](https://central.sonatype.com/?smo=true)

### Container
> 객체(Bean)들을 포함하고 관리하는 스프링의 관리자 개념
##### ㄴ BeanFactory
> 스프링의 기본 컨테이너  
> * Bean 객체를 관리하는 컨테이너
> * Bean의 생성, 관리, 의존성 주입의 역할
##### ㄴ ApplicationContext
> BeanFactory를 상속받아 확장 구현된 컨테이너
> * BeanFactory 대신 사용
> * Bean관리 뿐 아니라 다국어 처리, 리소스 로딩, 이벤트 발행/구현 등 추가 기능 제공


### Bean
> 스프링 IoC(Inversion of Control) 컨테이너에 의해서 관리되는 자바 객체   
> 컨테이너를 통해 객체의 의존성, 라이프사이클을 관리   
> 스코프 관리(singleton, protoType)

> ***주요 어노테이션***   
> 명시적으로 차이가 있을 뿐 동일한 역할을 하는 어노테이션
> * @Component : 일반 컴포넌트
> * @Service: 비지니스 로직을 담당하는 서비스 클래스
> * @Repository: 데이터 엑세스 레이어 클래스 DAO클래스에 사용
> * @Controller: 웹 요청을 처리하는 컨트롤러 클래스  

> 위와 다른 역할을 하는 어노테이션
> * @Configuration: 설정 클래스
> * @Bean: @Configuration 어노테이션이 사용된 클래스 내에서 메소드에 사용되는 어노테이션. ***메소드의 리턴 클래스***를 Bean으로 등록하는 어노테이션
> * @Autowired: 의존성 주입을 위해 사용되는 어노테이션, 생성자, 메소드, 필드에 의존성을 자동 주입
> * @Qualifier: 동일한 클래스를 상속받은 여러개 클래스 중에 의존성을 명시적으로 지정해야 할 때 사용, 주입할 클래스 옆에 @Qualifier(MyServiceA) Myservice 와 같은 형식
> * @Primary: 동일한 클래스를 상속받은 여러개 클래스 중에 기본이 되는 클래스를 지정할 때 사용


#### 빌드 자동화, 의존성 관리 도구(Maven, Gradle)
* io.spring.dependency-management : Gradle 플러그인, Gradle에서 BOM(Bill of Materials)을 사용해 버전을 명시하지 않아도 최적화된 버전을 제공


#### JPA
* [JPA공식문서](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/)



### 스케줄링
* [스케줄링 예제](https://spring.io/guides/gs/scheduling-tasks/)
