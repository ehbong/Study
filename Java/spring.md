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

> ***빈 등록 방법*** 
> * [XML에 명시적으로 등록](https://docs.spring.io/spring-framework/docs/4.2.x/spring-framework-reference/html/xsd-configuration.html)
> * 컴포넌트 스캔을 통해 등록
>    spring-boot 의 경우 @SpringBootApplication 어노테이션에 @ComponentScan 어노테이션이 포함되어 xml 설정 없이 컴포넌트 스캔
```xml
<!-- xml 을 통한 컴포넌트 스캔 -->
<beans ...>
  <context:component-scan base-package="대상패키지" />
</beans>
```
```java
// 소스에서 컴포넌트 스캔 설정
@Configuration
@ComponentScan(basePackage="대상 패키지") // 대상 패키지가 다수일 경우 {"A", "B"}
public class appConfig {}
```
### [Aop](https://docs.spring.io/spring-framework/docs/4.0.x/spring-framework-reference/html/aop.html)
>Aspect-Oriented Programming: 관점 지향 프로그래밍  
>여러 서비스에 공통적으로 적용되는 횡단 관심사에 대해 분리해서 적용하는 방법  
>대표적인 사용사례: 로깅, 트랜잭션 등

>***구성 요소***
>* 어드바이스: 적용 시점 또는 상황
>* 조인포인트: 적용 대상의 메소드 호출 지점 또는필드 값
>* 포인트카드: 적용 대상 필터
>   [pointcut 작성 방법 8.2.2 Declaring an aspect 참조](https://docs.spring.io/spring-framework/docs/4.0.x/spring-framework-reference/html/aop.html)


>***설정 방법***
>* XML
```xml
<!-- Aspect xml 예제 -->  
<beans xmlns="http://www.springframework.org/schema/beans"  
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
xmlns:aop="http://www.springframework.org/schema/aop"  
xsi:schemaLocation="http://www.springframework.org/schema/beans  
http://www.springframework.org/schema/beans/spring-beans.xsd  
http://www.springframework.org/schema/aop  
http://www.springframework.org/schema/aop/spring-aop.xsd">  
  
<!-- Aspect bean -->  
<bean id="loggingAspect" class="com.example.LoggingAspect" />  
  
<!-- Target bean -->  
<bean id="myService" class="com.example.MyService" />  
  
<!-- AOP configuration -->  
<aop:config>  
<aop:aspect id="logAspect" ref="loggingAspect"> 
<!-- point cut 은 적용 대상 -->  
<aop:pointcut id="serviceMethods" expression="execution(* com.example.MyService.*(..))" />  
<aop:before method="logBefore" pointcut-ref="serviceMethods" />  
<aop:after method="logAfter" pointcut-ref="serviceMethods" />  
</aop:aspect>  
</aop:config>  
  
</beans>
```
>* 어노테이션
```yaml
# 디펜던시 등록
dependencies {  
	implementation 'org.springframework.boot:spring-boot-starter-aop'  
}
```
```java 
package com.example.myapp;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.springframework.stereotype.Component;

// @Aspect 어노테이션으로 aop 등록
// Component 로 빈 등록
@Aspect 
@Component
public class LoggingAspect {
	// 
	// Around: 메소드를 실행 전후
	// Before: 메소드 실행 전
	// After: 메소드 실행이 실패, 성공과 관게 없이 후
	// AfterReturning: 메소드 성공 후
	// AfterThrowing: 메소드 예외 발생 후
	// 위 어노테이션의 내부 값 pointcut: 적용 대상 
    @Around("execution(* com.example.myapp..*(..))")
    public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();

        Object proceed = joinPoint.proceed();

        long executionTime = System.currentTimeMillis() - start;

        System.out.println(joinPoint.getSignature() + " executed in " + executionTime + "ms");

        return proceed;
    }
}
```

#### 빌드 자동화, 의존성 관리 도구(Maven, Gradle)
* io.spring.dependency-management : Gradle 플러그인, Gradle에서 BOM(Bill of Materials)을 사용해 버전을 명시하지 않아도 최적화된 버전을 제공

#### JpaRepository
> Spring Data JPA 에서 제공하는 인터페이스
> * 기존 JPA 의 Entity Manger 등의 역할을 포함해 CRUD 기능들을 쉽게 사용하도록 개선 된 인터페이스

### 스케줄링
* [스케줄링 예제](https://spring.io/guides/gs/scheduling-tasks/)

### [Spel](https://docs.spring.io/spring-framework/reference/core/expressions.html)
* [SpEL 사용법](https://amy-it.tistory.com/102)

### 뷰 리졸버 설정
```java
// 소스에서 빈으로 등록해서 설정
@Bean
public ViewResolver viewResolver(){
	InternalResourceViewResolver resolver = new InternalResourceViewResolver();
	resolver.setPrefix("/WEB-INF/views/");
	resolver.setSuffix(".jsp");
	// jstl 사용 시
	resolver.setViewClass(org.springframework.web.servlet.view.JstlView.class);
	return resolver;
}
```
```xml
<bean id="veiwResolver"
	  class="org.springframework.web.servlet.view.InternalResourceViewResolver"
	  p:prefix="/WEB-INF/views/"
	  p:suffix=".jsp"
	  p:viewClass="org.springframework.web.servlet.view.JstlView.class"
	  />
```

#### Webflux
* [공식문서](https://docs.spring.io/spring-framework/reference/web/webflux.html)
> * 비동기 및 이벤트 기반 어플리케이션 개발을 위한 모듈
> * Servlet API을 사용하지 않고, Reactive Streams API 기반으로 동작
> * 대규모 동시 요청 또는 실시간 대응이 필요한 어플리케이션을 위해 사용


#### SpringSecurity
* [공식문서](https://docs.spring.io/spring-security/reference/index.html)
>* 인증, 권한 부여 및 일반적인 공격에 대한 보호 제공
>* 기본 설정은 모든 접근에 대해 로그인 후 접근하도록 처리
>* config 파일을 작성해서 인증 및 권한 통제
>* [요청승인에 관한 메서드](https://docs.spring.io/spring-security/reference/servlet/authorization/authorize-http-requests.html#authorize-requests)
>	* `hasRole`, `hasAuthority` 의 차이는 역할과 권한의 차이
>		* 관리자 역할을 가진사람한테 허용(hasRole)
>		* A라는 사람한테 read 권한 허용(hasAuthority)
>* [계층적 권한](https://docs.spring.io/spring-security/reference/servlet/authorization/architecture.html#authz-hierarchical-roles)
>	* 권한이 계층 형일 경우 계층의 상하 관계를 정의하고 적용
```java
// 계층 구조 정의
@Bean 
static RoleHierarchy roleHierarchy() { 
	RoleHierarchyImpl hierarchy = new RoleHierarchyImpl();
	hierarchy.setHierarchy("ROLE_ADMIN > ROLE_STAFF\n" + 
		"ROLE_STAFF > ROLE_GUEST"); 
	return hierarchy; 
}
// 계층 구조로 단순화 해서 접근 권한을 정의
@Bean 
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception{ 
	http .csrf((auth) -> auth.disable()); 
	http .authorizeHttpRequests((auth) -> auth
	 .requestMatchers("/login").permitAll() 
	 .requestMatchers("/").hasAnyRole("GUEST") // GUEST 이상 권한이면 허용
	 .requestMatchers("/manager").hasAnyRole("STAFF") // STAFF 이상 "
	 .requestMatchers("/admin").hasAnyRole("ADMIN")  // ADMIN 만 허용
	 .anyRequest().authenticated()); 
	http .formLogin((auth) -> auth.loginPage("/login") 
	 .loginProcessingUrl("/loginProc") .permitAll() ); 
	return http.build(); 
}
```


#### Kafka
> 카프카 설정
```yml
# applicaion.yml
# Kafka configuration  
spring:  
    kafka:  
        bootstrap-servers: localhost:9092  
        consumer:  
            group-id: testgroup  
            auto-offset-reset: earliest  
            key-deserializer: org.apache.kafka.common.serialization.StringDeserializer  
			# 값을 스트링으로만 사용 시  
			# value-deserializer: org.apache.kafka.common.serialization.StringDeserializer  
            # 값을 모델 등 특정 형태로 사용 시
            value-deserializer: org.springframework.kafka.support.serializer.JsonDeserializer  
        producer:  
            key-serializer: org.apache.kafka.common.serialization.StringSerializer
            # 값을 모델 등 특정 형태로 사용 시  
            value-serializer: org.springframework.kafka.support.serializer.JsonSerializer
        # 역직렬화 시 패키지를 신용하도록 설정(없으면 오류 발생)      
        properties:  
            spring:  
                json:  
                    trusted:  
                        packages: '*'  
  
message:  
    topic:  
        name: test
```


> 스프링 카프카 컨슈머 예제
```java
@Service  
public class KafkaConsumer {  
	// KafkaListener 어노테이션 사용
	// topics 또는 topicPattern(정규식) 을 사용해서 수신할 토픽 지정
	// groupId 컨슈머 그룹 식별자
	// concurrency 리스너 컨테이너 수(스레드로 병렬처리)
	// 그 밖에 id: 리스너 고유 식별자, properties: 카프카 속성 등
    @KafkaListener(topics = "${message.topic.name}", groupId = "${spring.kafka.consumer.group-id}", concurrency = "3")  
    public void consume(ConsumerRecord<String, MyMessage> message) throws IOException {  
        String key = message.key();  
        MyMessage value = message.value();  
		System.out.printf("Consumed message : %s, %s, %n", key, value.toString());  
    }  
}
```
> 스프링 카프카 프로듀서 예제
```java
@Service  
public class KafkaProducer {  
  
    @Value(value= "${message.topic.name}")  
    private String topicName;
	// org.springframework.kafka.core.KafkaTemplate 를 import 해서
	// 생성자를 통해 의존성 주입
	// 메시지 형태를 제네릭을 통해 정의
    private final KafkaTemplate<String, MyMessage> kafkaTemplate;  
    @Autowired  
    public KafkaProducer(KafkaTemplate<String, MyMessage> kafkaTemplate) {  
        this.kafkaTemplate = kafkaTemplate;  
    }  
	
    public void sendMessage(String key, String value) {  
        System.out.printf("Produced message: %s, %s%n", key, value);  
        MyMessage message = new MyMessage(Instant.now().toEpochMilli(), value);  
        // kafkaTemplate.send 메서드를 이용해서 브로커에 메시지 전달
        kafkaTemplate.send(topicName, key, message);  
    }  
}
```


#### 이슈 및 조치 정리
>* 컨트롤러에서 @PathVariable 어노테이션 사용 시 path에 :id 와 같은 문법 사용하면 id를 값으로 인식하지 못해서 오류 발생
>	* {id}로 수정하여 문제 해결
