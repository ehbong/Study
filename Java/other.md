
## Lombok
> 어노테이션으로 반복코드를 줄여주는 라이브러리
* [공식 안내](https://projectlombok.org/features/)
```java
// final 필드 또는 초기화 되지 않은 모든 필드를 가져와서 주입하는 생성자를 생성
// Spring의 경우 생성자 의존성 주입을 받을 수 있음
@RequiredArgsConstructor
class MemberService{
	final MemberRepository memberRepository;
	
	// @RequiredArgsConstructor 어노테이션을 통해
	// 아래처럼 생성자를 작성한 것과 동일한 효과
	void MemberService(MemberRepository mr){
		this.memberRepository = mr;
	}

}

```

## JPA
> java ORM기술을 사용하는 인터페이스
> * Hibernate, OpenJPA 등이 JPA의 구현체
> * JDBC드라이버를 통해 DB와 상호작용
* [JPA공식문서](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/)

###### 영속성 컨텍스트(PersistenceContext)
> 구성요소
> * 엔티티 객체: 데이터베이스 레코드와 매핑된 객체  
> * 엔티티 매니저: 엔티티의 생성주기 및 관리 주체  
> * 1차 캐시: 엔티티 객체를 저장하고 있는 캐시  
>   (같은 데이터 조회를 디비쿼리 없이 처리하거나, 스냅샷을 통해 변경점을 판별하는 역할)  
> * 쓰기지연 저장소: 실제 쿼리로 변환하여 보관했다가 flush 또는 commit 시 디비에 쿼리를 호출하는 역할

###### entity
> @entity 어노테이션 조건
> * final class, abstract class, interface 에 사용 금지  
> * 필드에 final 사용 금지  
> * 식별자 필드 필요  
> * 클래스 이름과 테이블이름 일치 또는 @Table(name="테이블명") 으로 값 일치 필요  
> * 디폴드 생성자 메서드 필요
> 	* JPA 구현체에서 엔티티 객체를 프록시 객체로 대체하거나 리플렉션 사용해서 객체를 초기화할 때 필요  
> 	   프록시 객체: 지연 로딩을 위해 실제 데이터를 대신하고, 필요할 때 실제 데이터를 불러오는 객체
> 	* 엔티티의 생명주기 관리를 위해 객체를 생성할 때 필요

> 생명주기
> * 비영속(New): 영속성 컨텍스트로 관리되기 전(persist() 메서드 실행전)  
> * 영속(Managed): 영속성 컨텍스트에 등록 된 객체(1차 캐시에 등록된 상태)  
> * 준영속(Detached): 영속성 컨텍스트에 관리되다가 분리된 상태(detach, clear 메서드 실행, 수정이 필요하지 않거나, 메모리관리 등의 이유로 분리한 상태)  
> * 삭제(Removed): 영속 데이터의 삭제를 위한 상태(EntityManager.remove())

> Transient : 엔티티의 필드 중 영속화 하지 않는 필드에 사용(DB 에 저장하지 않는 필드)
```java
@Transient
String LastName; // 어노테이션으로 적용
transient public String firstName; // 키워드로 적용
``` 

> 데이터 타입
* [Hibernate Basic Types DB 데이터 타입과 매칭되는 객체 데이터 타입](https://docs.jboss.org/hibernate/orm/5.5/userguide/html_single/Hibernate_User_Guide.html#basic)

##### QueryDSL
>쿼리를 자바 코드를 사용해, 쿼리를 체이닝방식으로 작성하는 라이브러리  
>장점  
>*  복잡한 쿼리 가능 
>단점
>* JPA 1차 캐시를 활용할 수 없음
```java
// 예제
// SqlAlchemy 등 다른 언어 Orm에서도 지원하는 방식
QUser qUser = QUser.user;
List<User> users = new JPAQueryFactory(entityManager)
    .select(qUser)
    .from(qUser)
    .where(qUser.age.gt(25).and(qUser.name.eq("John")))
    .fetch();
```

