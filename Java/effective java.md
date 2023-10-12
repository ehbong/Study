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

#### i.22 인터페이스는 타입을 정의하는 용도로 사용해라
> 인터페이스는 무엇을 할 수 있는지 기능을 정의해야한다.
> * 인터페이스안에 상수를 선언해서 상수 인터페이스를 사용하지 마라

#### i.23

#### i.24

#### i.25 톱레벨 클래스는 한파일에 하나만 작성해라
> 톱레벨 클래스: 문서에 가장 바깥 쪽에 작성된 클래스
> 톱레벨 클래스를 하나의 파일에 여러개를 작성하면 자바 컴파일 순서에 따라 문제가 발생한다.

#### i.26 로 타입은 사용하지 마라
> 로타입은 제네릭 도입전 코드와 호완성을 위해 제공될 뿐, 가능하면 제네릭을 반드시 사용해라
> * 로 타입을 사용하면 런타임에 예외가 발생한다.
> * 제네릭을 사용하면 타입 안정성을 보장할 수 있다.
```java
// 로 타입
List list = new ArrayList();
```
#### i.27 비검사 경고를 제거하라

#### i.28 배열보다는 리스트를 사용하라

#### i.29 제네릭 클래스로 만들어라 

#### i.30 제네릭 메서드로 만들어라

#### i.31 한정적 와일드 카드를 사용해서 유연성을 높여라

#### i.32	제네릭과 가변인수를 함께 쓸 때는 신중하라
> 제네릭의 타입은 컴파일 시 소거된다.
> 가변인수와 함께 사용될 때 다양한 오류를 발생시킨다.
```java
public class GenericVarargs {  
	// 가변인수로 제네릭 List를 전달 했을 때
    public static void dangerous(List<String>...strLists) {  
        List<Integer> intList = List.of(42);  
        Object[] objs = strLists;
        // 다음과 같이 힙 저장 공간에 덮어써질 경우
        objs[0] = intList;  
        // 꺼내는 순간(런타임)에 힙 저장공간에 데이터가 
        // 타입이 맞지 않아서 ClassCastException 예외 발생
        String s = strLists[0].get(0);  
    }  
  
    public static void main(String[] args) {  
        GenericVarargs.dangerous(List.of("abc"));  
    }  
}
``` 
> 그럼에도 사용이 필요한 경우  
> 신뢰할 수 있게 작성한 후  
> @SafeVarargs 어노테이션으로 경고를 제거하라
> @SafeVarargs : 제네릭 가변 인자 메서드의 안정성을 보장한다고 명시하는 어노테이션
> 신뢰할 수 있게 작성하는 방법
> * 가변매개변수(varargs)에는 아무것도 저장하지 않는다.(대입 금지)
> * 통제가 불가능하다면 반환하지 않는다.
#### i.33	타입 안전 이종 컨테이너를 고려하라
#### i.34	int 상수 대신 열거 타입을 사용하라
> 상수를 나열할 때 단점과 열거 타입의 특징
> * 상수 필드를 나열하는 것은 각각에 값에 연관성을 만들기 어렵다.
> * 필드가 가진 값이 같으면 같은 값으로 인식 된다.
```java
// 아래 두가지 항목은 다른 의미지만 같은 값으로 인식된다.
private static final int APPLE_FUJI = 0;
private static final int ORANGE_NAVEL = 0;
// 이름 앞에 전치사가 APPLE 이라는 것을 제외하면 묶을 방도가 없다.
// APPLE이 뭐가 있는지 몇개 있는지 확인하려면, 리플렉션을 사용하거나 추가작업이 들어간다.
private static final int APPLE_PIPPIN = 1;
```
> * 자바의 열거타입 <span style="color:red;">enum은 클래스 이며, 상수는 각각 자신의 인스턴스를 만들어 public static final 필드로 공개</span>된다.
> * 자바의 열거타입은 싱글턴 이다.
> * 열거타입은 컴파일 안정성을 제공한다. 같은 열거타입으로 묶인 값이 아니면 컴파일 오류를 발생시킨다.
> * 열거타입은 필드나 메서드도 추가 된다. 열거 값에 공통적으로 사용되는 값 또는 메서드를 선언해서 사용할 수 있다.
> * 열거타입 이름을 toString, 목록을 values 메서드를 통해 제공한다.
#### i.35	ordinal 메서드 대신 인스턴스 필드를 사용하라
> ordinal: enum에 있는 해당 상수가 몇 번째 위치인지 반환하는  메서드.
> * 이 메서드는 상수의 순서를 바꾸거나 하면 오류를 발생시킨다.
> * 중간 값을 비울 수 없다.
```java
// ordinal 메서드를 사용하기 위해 값을 따로 지정하지 않음
// 순서가 절대적이고, 중간에 빈 값이 있으면 문제가 발생한다(현재 7이 없다.)
public enum NumberEng {
	ONE, TWO, THREE, FOUR, FIVE, SIX, EIGHT, NINE, TEN
}
// 인스턴스 필드를 이용한 방법
// 각각 값이 있기 때문에 중간에 필요 없으면 값을 빼거나, 순서를 변경할 수 있다.
public enum NumberEng {
	ONE(1), TWO(2), THREE(3), FOUR(4), FIVE(5), SIX(6), SEVEN(7), EIGHT(8), NINE(9), TEN(10)
}
```
#### i.36	비트 필드 대신 EnumSet을 사용하라
#### i.37	ordinal 인덱싱 대신 EnumMap을 사용하라
#### i.38	확장할 수 있는 열거 타입이 필요하면 인터페이스를 사용하라
#### i.39	명명 패턴보다 애너테이션을 사용하라
> 특정이름을 규칙으로 하는 명명 패턴 보다는 애너테이션을 사용해라.  
> 명명 패턴의 단점
> * 오타가 발생하면 동작하지 않는다.
> * 명확한 사용 범위가 없다.(명명패턴이 어디까지 동작하는지 알 수 없다.)
> * 추가 매개변수 전달방법이 없다.
> 애너테이션 사용 예시
```java
import java.lang.annotation.*;
/**
* 테스트메서드임을선언하는애너테이션이다. * 매개변수없는정 적메서드전용이다.
*/
@Retention (RetentionPolicy.RUNTIME) // @Test 를 런타임 시까지 유지하겠다.(이 옵션이 없으면 런타임 시 리플랙션이 해당 애너테이션을 찾지 못한다.)
@Target(ElementType.METHOD) // 에너테이션의 대상을 메서드로 한정한다.
public @interface Test {}

```
#### i.40	@Override 애너테이션을 일관되게 사용하라
> 재정의 할 떄는 Override 어노테이션을 반드시 붙여라.
> * 어노테이션을 붙이지 않으면, 재정의 메서드가 원본 메서드와 이름 또는  
>    매개변수가 다를 때 컴파일러가 체크하지 않는다.
> * 안붙여도 되는 경우는 추상메서드를 정의할 때 뿐이다.
#### i.41	정의하려는 것이 타입이라면 마커 인터페이스를 사용하라
#### i.42	익명 클래스보다는 람다를 사용하라
#### i.43	람다보다는 메서드 참조를 사용하라
#### i.44	표준 함수형 인터페이스를 사용하라
#### i.45	스트림은 주의해서 사용하라
#### i.46	스트림에서는 부작용 없는 함수를 사용하라
#### i.47	반환 타입으로는 스트림보다 컬렉션이 낫다
#### i.48	스트림 병렬화는 주의해서 적용하라
#### i.49	매개변수가 유효한지 검사하라
#### i.50	적시에 방어적 복사본을 만들라
> * 가변 객체들을 생성자나 메서드의 매개변수로 받을 때, 변경을 막으려면 방어적 복사를 해라.  
> * 가변 객체들은 final로 선언해도 변경 가능한 객체들이 많다.
> * 복사를 할 때, 복수 후에 유효성 검사를 해라. 찰나의 순간이지만, 멀티스레딩 환경이라면 다른 환경에서 값을 변경 할 수 있다.
#### i.51	메서드 시그니처를 신중히 설계하라
> * 이름은 명명 규칙에 따라 짓자.
> * 클래스 내 너무 많은 메서드를 만들지 말자.
> * 매개변수 목록은 짧게 유지하자.
> 	* 짧게 만드는 방법으로 메서드를 분리, 빌더 패턴 등이 있다. 
> * 매개변수 타입으로는 클래스보다 인터페이스가 낫다.
#### i.52	다중정의는 신중히 사용하라
#### i.53	가변인수는 신중히 사용하라
#### i.54	null이 아닌, 빈 컬렉션이나 배열을 반환하라
> * 객체의 값이 비어 있을 경우 null을 반환하면 사용 측에서 null에 대응하는 코드를 추가 작성해야한다.
> * null이 아닌 빈 컬렉션이나 배열을 반환하고, 성능 측 이슈가 생긴다면, 불변객체 또는 미리 생성해 놓은 객체를 반환해라
```java
// Collections.emptyList 는 비어 있는 불변 리스트를 반환한다.
public List<Cheese> getCheeses) {
	return cheesesInStock.isEmpty() ? Collections.emptyList() 
		: new ArrayList(cheesesInStock);
}
// 미리 생성해 놓은 객체 활용(static으로 선언 했기 때문에 객체마다 복사 생성되지 않는다.)
private static final Cheese[] EMPTY_CHESE_ARAY = new Cheese[0);
public Cheese[] getCheeses() {
	return cheesesInStock.toAray(EMPTY_CHEESE_ARRAY) ;
}
```
#### i.55	옵셔널 반환은 신중히 하라
#### i.56	공개된 API 요소에는 항상 문서화 주석을 작성하라
#### i.57	지역변수의 범위를 최소화하라
> * 처음 쓰일 때 선언해라
> * 선언과 동시에 초기화 해라
#### i.58	전통적인 for 문보다는 for-each 문을 사용하라
> * 전통적인 for 문은 반복자 및 인덱스 등을 많이 반복해서 코드를 복잡하게 하고, 변수명이 틀리거나 하는 것을 방지하기 어렵다.
> * 전통적인 for 문은 배열, 컬렉션이냐에 따라 코드가 달라진다.
```java
// 전통적인 for
for (int i=0; i < a.length; i++) {
	// a[i] 를 다루는 작업
}
// 전통적인 for 컬렉션
for (Iterator<Element> i = c.iterator(); i.hasNext();) {
	Element e = i.next();
	// e 를 다루는 작업 
}

// for each
// 코드가 훨씬 간결해지고 명확해 진다.
for (Element e : c){
	// e 를 다루는 작업
}

```
> foreach를 사용하지 못하는 상황
> * 켈력션을 순회하면서 특정원소를 제거해야 할 때
> * 리스트나 배열을 순회하면서 원소의 값을 일부 혹은 전체를 교체해야 할 때
> * 병렬로 순회할 때, 반복자와 인덱스를 이용한 조정이 필요할 때

#### i.59	라이브러리를 익히고 사용하라
#### i.60	정확한 답이 필요하다면 float와 double은 피하라
> 부동소수점을 사용하는 계산은 정확하지 않다.
> 금융계산 등 정확한 계산이 필요한 경우 BigDecimal, int, long을 사용해라
> 9자리 내라면 int, 19자리 내라면 long, 그 이상은 BigDecimal을 사용해라
#### i.61	박싱된 기본 타입보다는 기본 타입을 사용하라
> 
#### i.62	다른 타입이 적절하다면 문자열 사용을 피하라
#### i.63	문자열 연결은 느리니 주의하라
#### i.64	객체는 인터페이스를 사용해 참조하라
#### i.65	리플렉션보다는 인터페이스를 사용하라
#### i.66	네이티브 메서드는 신중히 사용하라
#### i.67	최적화는 신중히 하라
#### i.68	일반적으로 통용되는 명명 규칙을 따르라
#### i.69	예외는 진짜 예외 상황에만 사용하라
#### i.70	복구할 수 있는 상황에는 검사 예외를, 프로그래밍 오류에는 런타임 예외를 사용하라
#### i.71	필요 없는 검사 예외 사용은 피하라
#### i.72	표준 예외를 사용하라
#### i.73	추상화 수준에 맞는 예외를 던지라
#### i.74	메서드가 던지는 모든 예외를 문서화하라
#### i.75	예외의 상세 메시지에 실패 관련 정보를 담으라
#### i.76	가능한 한 실패 원자적으로 만들라
#### i.77	예외를 무시하지 말라
#### i.78	공유 중인 가변 데이터는 동기화해 사용하라
#### i.79	과도한 동기화는 피하라
#### i.80	스레드보다는 실행자, 태스크, 스트림을 애용하라
#### i.81	wait와 notify보다는 동시성 유틸리티를 애용하라
#### i.82	스레드 안전성 수준을 문서화하라
#### i.83	지연 초기화는 신중히 사용하라
#### i.84	프로그램의 동작을 스레드 스케줄러에 기대지 말라
#### i.85	자바 직렬화의 대안을 찾으라
#### i.86	Serializable을 구현할지는 신중히 결정하라
#### i.87	커스텀 직렬화 형태를 고려해보라
#### i.88	readObject 메서드는 방어적으로 작성하라
#### i.89	인스턴스 수를 통제해야 한다면 readResolve보다는 열거 타입을 사용하라
#### i.90	직렬화된 인스턴스 대신 직렬화 프록시 사용을 검토하라

