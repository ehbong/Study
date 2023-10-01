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
> - 클래스이름@16진수 해시코드 형식으로 반환한다.
> toString 메서드는 클래스 내부에 의미있는 값들을 간결하고 읽기 쉬운 형태로 반환 해야한다.
> 구체적인 포맷을 가진 경우나, 포맷이 없는 경우 모두 의도가 명확해야 한다.

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
> 