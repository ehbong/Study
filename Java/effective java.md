#### i.1 생성자 대신 정적 팩토리 메서드 사용
> 장점
> 1. 이름을 지정 가능
> 	* 생성자는 클래스 이름과 동일하게 작성해야 해서 의미를 정확하게 전달하기 어려움
> 	* 오버로딩으로 다양한 매개변수를 받는 생성자를 작성했을 때 어떻게 다른지를 명확하게 전달하기 어려움
> 2. 인스턴스 생성 통제
> 	* 싱글톤, 인스턴스화 불가, 불변 값 클래스 등이 가능
> 3. 반환 타입을 하위 타입 객체로도 반환 가능
> 	* 상속받은 다양한 클래스 인스턴스를 반환 가능
> 4. 매개변수에 따라 매번 다른 클래스 반환 가능
>      * 하나의 메서드가 다양한 클래스 인스턴스를 반환 가능
>      * 이 기능을 통해 매개변수에 맞는 적절한 클래스 인스턴스를 반환 가능
> 5. 정적 팩토리 메서드 작성 시점에 반환 클래스가 없어도 이후에 추가 가능
> 	 * 인터페이스를 통해 규격화(service interface)하고, 인터페이스 구현 클래스(provider service)로 다양한 서비스를 추가에 대응
```java
// 인터페이스 정의
public interface Plugin {
    void performAction();
}

// 인터페이스 구현 클래스 정의(다양한 구현 클래스 추가 가능)
public class SamplePlugin implements Plugin {
    @Override
    public void performAction() {
        System.out.println("SamplePlugin is performing an action.");
    }
}


import java.util.ServiceLoader;

public class PluginFactory {
    public static Plugin createPlugin() {
		// 팩토리 메서드에서 구현 클래스가 뭔지 몰라도 ServiceLoader를 통해
		// 인터페이스의 구현 클래스를 모두 불러와서 조건에 맞게 선택 가능
        ServiceLoader<Plugin> serviceLoader = ServiceLoader.load(Plugin.class);
        for (Plugin plugin : serviceLoader) {
            return plugin; // Return the first implementation found
        }
        
        throw new IllegalStateException("No implementations of Plugin found.");
    }
    
    public static void main(String[] args) {
	    // 사용측에서는 동일한 방식으로, 상황에 맞는 구현 클래스를 사용가능
        Plugin plugin = PluginFactory.createPlugin();
        plugin.performAction();
    }
}

```
> 단점
> * 개발자가 팩토리 메서드 명칭이 무엇인지 직관적으로 알기 어려움
> 	* 메서드 명을 약속을 통해 규격화 필요
#### i.2 생성자에 매개변수가 많으면 빌더 고려
> * 매개변수 중 필수요소 구분 및 매개변수의 요소가 많아서 생성자 오버로딩으로 구현이 힘들때
>    빌더 클래스(내부클래스)를 만들어서 이를 대응
```java
public class Student {
	private final int age;
	private final String name;
	private final String hobby;
	private final String specialty;
	private final int grade;
	//...
	public static class Builder{
		// 필수 값
		private final int age;
		private final String name;
		private final int grade;
		// 선택 값 (기본 값으로 초기화)
		private final String hobby = "";
		private final String specialty = "";
		// 생성자에서 필수 값 수집
		public Builder(int age, String name, int grade){
			this.age = age;
			this.name = name;
			this.grade = grade;
		}
		// 각 매개변수를 setter 로 구현
		// 자기자신을 리턴해서 a().b().c() 처럼 메서드 연쇄 구현
		public Builder hobby(String value){
			this.hobby = value;
			return this;
		}
		public Builder specialty(String value){
			this.specalty = value;
			return this;
		}
		// 빌드 메서드로 Builder 클래스를 매개변수로 생성자 호출
		public Student build(){
			return new Student(this);
		}
	}
	// 생성자를 private로 구현해서 외부에서 호출 막음
	private Student(Builder b){
		age = b.age;
		name = b.name;
		grade = b.grade;
		hobby = b.hobby;
		specialty = b.specialty;
	}
}

// 사용 방법
Student student = Student.Builder(15, "tom", 3).hobby("music").build();
``` 

#### i.3 싱글톤을 만드는 방법
```java
// public static final 필드로 클래스 초기화 시 호출 후, 재 생성을 막음
public class Singleton1 {  
    public static final Singleton1 instance = new Singleton1();  
    private Singleton1(){}  
}
// 정적팩토리 방식
// private static 으로 필드 선언 후, 메서드를 통해 참조
// 메서드 부분을 수정해서 추후 변경 사항에도 유연하게 대처
public class Singleton2 {   
    private static Singleton2 INSTANCE = new Singleton2();  
    private Singleton2(){}
    public static Singleton2 getInstance(){  
        return INSTANCE;  
    }  
}
```
#### i.4 인스턴스화를 막는 방법
> 정적 메서드와 필드만 사용할 경우
> private 생성자를 선언해 인스턴스화를 막음
> 클래스 안에서도 막고 싶다면 생성자 안에서 예외 던짐
```java
public class Student {
	private Student(){
		// 특정 조건을 사용
		throw new AssertionError();
	}
}
```

#### i.5 싱글톤이 추천되지 않는 클래스와 의존성 주입
> 클래스 내부적으로 하나 이상의 자원에 의존하고, 영향을 받는다면, 싱글톤이 아닌 생성자를 통한 의존성 주입을 하는 방법이 유연성, 재사용성이 증가됨

#### i.6 불필요한 객체 생성 제한
> * 불변 객체의 경우 재사용에 안정성이 보장되므로, 재사용 하는 방향으로 작성
```java
// 클래스 생성으로 스트링 객체를 생성하면 매번 추가 메모리 공간을 사용
String a = new String("string");
// 아래 처럼 생성할 경우 같은 문자열의 경우 같은 메모리 공간을 공유
Stirng b = "string";
```
> 위 예시 외에도, 정규식을 사용한 string.matches() 를, Pattern 클래스를 사용한 정적 필드로 선언하면, 재사용이 가능
> * 오토박싱(기본 타입 자료형과, 래퍼 클래스 타입 자료형을 같이 사용할 때, 자동으로 상호 변환하는 기능)을 사용하지 않도록 개선 필요

#### i.7 사용이 끝난 객체 참조를 해제해라
> 배열이나, Map등을 사용할 때, 사용하지 않는 객체를 null처리 해주지 않으면 계속 메모리를 점유한다.
#### i.8 finallize 와 cleaner 사용을 피해라
> Object 클래스의 메서드였던 finallize 는 자바 9부터 지원하지 않음
> 9 부터는  Cleaner 클래스가 사용 됨
> 단점
> * 수행 시점 및 수행 여부를 보장할 수 없다.
> * 동작  중 발생한 예외가 무시 된다.(finallize 의 경우)
> * 해당 동작이 gc 과정 중 일어나기 때문에 추가적인 작업으로 인해 성능 저하가 발생 가능
> 그럼에도 사용 한다면
> * 사용자가 자원을 사용하고 닫지 않을 것을 대비 용도 

#### i.9 자원 사용을 해제 할 때 try-with-resource 사용
 > try catch finally 의 경우 finally에서 오류가 나면 문제 발생
```java
// try 문구 뒤에 소괄호를 통해 자원 사용 객체를 선언
// 아래 괄호안에 들어갈 클래스의 AutoCloseable 인터페이스를 구현 close 메서드 @Override필요
try (InputStream ins = new FileInputStream(src);
	OutputString ots = new FileOutputStream(dsrc)) {
	....
	}
```

#### i.10 equals 재정의 시 규약 준수 필요
> 클래스의 인스턴스는 재정의 하지않으면 자기 자신과만 같음.
> 이 때 equals 를 재정의해서 값이 같을 때 같게 인식하도록 동작 가능
> 잘못 수정하면 equals 메서드를 사용하는 다른 동작에도 영향을 끼침
> 규약(모든 규약은 null이 아님을 전제함, null 과의 비교는 false)
> 	* x.equals(x) true
> 	* x.equals(y) == y.equals(x) true
> 	* x == y, x == z, 두개가 true 면 z == y true
> 	* 반복해서 실행해도 늘 true 또는 false

#### i.11 equals 를 재정의 했다면 hashCode 도 규약에 맞게 수정필요
> hashCode 메서드는 HashMap, HashSet 같은 컬렉션의 원소로 사용될 때 사용되는 메서드
> 해당 컬렉션에서는 hashCode와 equals를 통해 값을 구분
> 따라서 hashCode가 제대로 동작하지 않으면 중복이 의도한 대로 검증되지 않음
> 
> 규약
> * equals 에서 사용하는 값이 변경되지 않으면 반복호출에도 일관된 값 유지(단 어플리케이션이 재 실행되면 값이 달라져도 상관 없음)
> * equals에서 true라면 같은 값을 반환
> * equals에서 다르다고 무조건 다른값을 반환할 필요는 없지만, 해시테이블의 성능이 저하(hashCode가 같은지 판단하고 eqauls로 다시 확인하기 때문에, and연산 특성상 hashCode가 같으면 2번 확인이 필요)
> 
> 예제코드
> 다음과 같이 작성하면, 다른 인스턴스라도 값이 같으면 같다고 판단
```java
public class HashCodeEx {  
	private String name;  
	private int age;  
	  
	private float floatValue;  
	  
	public HashCodeEx(String name, int age, float floatValue) {  
		this.name = name;  
		this.age = age;  
		this.floatValue = floatValue;  
	}  
	// equals 를 만들 때, 사용할 값들을 직접비교  
	@Override  
	public boolean equals(Object obj) {  
		if(this == obj) {  
			return true;  
		}  
		if(!(obj instanceof HashCodeEx)){  
			return false;  
		}  
		HashCodeEx hce = (HashCodeEx) obj;  
			if (hce.name.equals(this.name)  
				&& hce.age == this.age  
				&& hce.floatValue == this.floatValue) {  
				return true;  
			}  
		return false;  
	}  
	// 기본형들은 컬렉션 클래스의 hashCode를 사용  
	@Override  
	public int hashCode() {  
		int result = name.hashCode();  
		result = 31 * result + Integer.hashCode(age);  
		result = 31 * result + Float.hashCode(floatValue);  
		return result;  
	}  
}

```

#### i.12 toString 을 재정의 해라
> Object의 기본 toString 메서드는 클래스의 정보를 제대로 알려주는 경우가 거의 없다.
> * 클래스이름@16진수 해시코드 형식으로 반환한다.  
> * toString 메서드는 클래스 내부에 의미있는 값들을 간결하고 읽기 쉬운 형태로 반환 해야한다.
> * 구체적인 포맷을 가진 경우나, 포맷이 없는 경우 모두 의도가 명확해야 한다.

#### i.13 clone 재정의는 주의 하라
> Object의 clone 메서드를 재정의 하려면 CloneNotSupportedException 예외를 던져야 한다.  
> CloneNotSupportedException 예외를 던지지 않으려면 Cloneable 인터페이스를 구현해야 한다.  
> 규칙
```java
// clone으로 생성된 인스턴스는 새로 생성된 인스턴스여야 한다
x.clone() != x

// clone으로 생성된 인스턴스와 대상 인스턴스는 같은 클래스여야 한다.
x.clone().getClass() == x.getClass()

// 서로 같은 인스턴스(논리) 여야 한다.
// 다만 아래의 값이 true가 되려면 equals를 재정의 해야한다.
x.clone().equals(x)
```
> 주의 사항
> * 래퍼런스 타입의 자료형 필드는 깊은 복사가 이루어지지 않으므로 주의 해야한다.
> * final로 선언된 래퍼런스 타입의 자료형 필드는 깊은 복사 처리할 때 값의 할당이 안된다.
> * 자식 클래스의 clone에서 재정의한 클래스를 사용하면 문제가 발생할 수 있다.
>
> clone을 재정의 하기 보다, 복사 생성자, 복사 팩토리 메서드를 사용하는 것이 좋다.

#### i.14 클래스 간 순서가 존재하고 정렬이 필요하다면 Comparable을 구현해라
> Comparable 을 구현해서 CompareTo를 재정의 하면, 정렬 및 Set(TreeSet) 등에 활용된다.  
> CompareTo 재정의 규칙
> * 기준 객체 < 비교 객체 => 음수
> * 기준 객체 == 비교 객체 => 0
> * 기준 객체 > 비교 객체 => 양수
> 주의 사항
> * 반환 자료형이 int이므로 범위를 넘어서는 값은 반환되지 않도록 주의
> * 반환 값이 0 일 때 equals도 0으로 맞춰주는 것이 좋다. 맞지 않다면 명시해야 한다.

#### i.15 클래스와 멤버의 접근 권한은 최소화해라
> 접근 제한은 최대한 보수적으로, 최소한의 권한을 주고 필요에 따라 확장한다.
> * 널널한 접근 제한은 사용자 측에 자유를 부여하고 이는 의도치 않은 동작 발생 가능성을 높임
> * public 클래스의 필드는 되도록 public가 아니여야 한다. 
```java
	// 접근 제한자를 넓게 사용 했을 때 발생할 수 있는 이슈
	public class Account{
		// 특정 형식이 필요한 문자열 "0000-0000-00000";
		public String accountNo;
		public String setAccountNo(String accountNo){
			// 형식에 맞는 지 확인하고 형식에 맞게 대입
		}
	}
	// 접근 제한자를 공개로 해놓은 경우, 원하지 않는 형태의 값 변경 발생
	Account ac = new Account();
	ac.accountNo = "00000000000000";
```
> * public 클래스는 public static final 필드 외에는 어떤 public 필드도 가져서는 안된다.
> * final로 선언되었다 하더라도 가변 객체인 경우 참조 주소가 바뀌지 못할 뿐, 내부 값은 바뀔 수 있다.
> * [접근제한자](https://github.com/ehbong/Study/blob/main/Java/java.md#%EC%A0%91%EA%B7%BC-%EC%A0%9C%ED%95%9C%EC%9E%90)
> * 톱레벨 class 는 public 과 default(package-private) 둘만 가능
> * 상속 받은 하위 클래스는 접근 제어를 더 좁게는 할 수 없다.
> * 자바 9 에서 모듈 시스템으로 접근을 제한할 수 있다.
> * 내부 클래스를 생성할 때는 static으로 작성해야 숨은참조(내부 클래스의 사용으로 외부 클래스가 GC 대상이 되지 못하는 것) 이슈를 방지할 수 있다.

#### i.16

#### i.17 가능하면 불변 객체를 사용해라
> String, 기본타입의 래퍼 클래스들, 등 이 불변클래스에 속한다.  
> 생성 규칙
> * 변경 메서드를 제공하지 않는다.(생성자 제외)
> * 클래스를 확장을 막는다.(상속을 제한하기 위해 final로 선언)
> * 모든 필드는 private final로 선언한다.(외부 접근과 변경을 막는다.)
> * 자신 외에 가변 객체 필드에는 외부 접근을 막아야 한다.(값 변경 방지, 필요하면 객체를 딥카피 해서 전달)
> 장점
> * 변경이 없기 때문에 스레드에 안전하다.(새로운 값이 필요하면 새로 생성해야한다.)
> * 복사 생성자가 필요없다.(값을 변경하지 못하기 때문에 복사해서 사용할 필요가 없다.)
> * 객체를 만들 때 불변 객체를 구성요소로 사용하면 좋다.(map, set의 키 또는 원소로 사용될 때, 변경될 수 없으므로 변경 관련 문제가 발생할 가능성이 없다.)
> 단점
> * 작은 변경에도 무조건 새로운 객체를 생성해야한다.


#### i.18 상속보다 컴포지션을 사용하라.
> 이미 구현된 클래스를 상속하는 것을 피해라.
> * 혼자 개발하거나, 충분히 공유(문서화 등)가 된 상황이 아니라면, 상속을 피해라.  
> * 다른 패키지에 있는 클래스를 상속하는 것을 피해라.  
> 문제점
> * 메서드와 다르게 상속은 캡슐화를 깨뜨린다.  
> 	* 상위 클래스의 변경이 하위 클래스 동작에 문제를 발생시킬 수 있다.  
> 	* 상위 클래스에서 메서드 추가 시, 하위 클래스의 메서드와 이름이 같고, 반환 타입이 다르면 컴파일 에러가 발생한다.
> 	* 하위 클래스 영향을 고려해서 상위 클래스 수정이 어렵다.
> 	* 상위 클래스의 메서드를 호출할 때 내부동작을 이해하지 못하면 예상치 못한 동작이 발생한다.
```java
public class InstrumentedHashSet<E> extends HashSet<E> {  
	private int addCount = 0;  
	// 기타 내용
	@Override  
	public boolean add(E e) {  
		addCount++;  
		return super.add(e);  
	}  
	  
	@Override  
	public boolean addAll(Collection<? extends E> c) {  
		addCount += c.size();  
		return super.addAll(c);
		// super.addAll(c) 의 내부 동작
		// addAll 메서드가 내부적으로 add 메서드를 호출한다.
		// 즉 addAll 호출 시 의도한 addCount가 아닌 2배의 수가 저장된다.
		// boolean modified = false;   
		// for (E e : c)  
		// 	 if (add(e))  
		//		modified = true;  
		// return modified;  
	}
}
```
> 컴포지션이란?
> * 기존 클래스의 객체를 포함한 새로운 클래스를 만들어서 재활용 하는 것
> 컴포지션 단점
> * 콜백을 활용한 곳에서는 사용이 어려울 수 있음  
> 	* 컴포지션은 객체 간의 관계가 상속처럼 명확하지 않아서,  
>        부모타입을 지정해놓고 자유롭게 자식 타입들을 받을 수 없음.

#### i.19 상속에 문서화는 필수다.

#### i.20 추상 클래스 보다 인터페이스를 사용해라

#### i.21 인터페이스 설계는 신중해라
> 인터페이스의 메서드 선언은 한번 정하면 추후 추가가 어렵다.(자바 8이전에는 불가)
> 메서드를 추후 추가하면 구현한 모든 클래스에 컴파일 에러가 발생한다.
> 자바 8이후 디폴트 메서드를 추가해서 메서드 추가를 지원한다.
```java
public interface Student {
	// 선언 순서
    // 접근제한자 default <제네릭> 반환타입 메소드명
    public default void study(){  
          // 내용 생략
    }  
}
```
> 디폴트 메서드 주의점
> * 디폴트 메서드는 구현 측과 합의되지 않은 추가다.  
>    즉 어떤 구현체에서 문제를 발생 시킬지 예측하기 어렵다.
```java
// 오류 시나리오
// Child 클래스에서 부모클래스를 상속받고 인터페이스를 구현하고 있다.
// 인터페이스의 디폴트 메서드는 추후 추가 됐다.
// Parent의 a 메서드는 접근제한자로 자식이 사용하지 못한다.(컴파일 체크)
// 추후 디폴트 메서드가 같은 이름으로 생성 됐다.
// 이후 Child에서 a메서드를 사용했고, 이는 런타임에서 에러가 발생한다.
// 즉 예측하지 못한 오류를 발생시켰다.
public interface Human {
	// 디폴트 메서드가 추후 추가 됐다.
    public default void a(){  
          // 내용 생략
    }  
}
class Parent{
	private void a(){
		// 구현
	}
}
class Child extends Parent implements Human {	
}

Child c = new Child();
c.a(); // 실행 시 오류 발생
// 자바의 메서드 검색 순서는 자신>부모클래스>인터페이스 이므로
// 부모클래스의 접근제한자가 private이므로 오류 발생
```

