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

#### i.3
#### i.4 인스턴스화를 막는 방법
> 정적 메서드와 필드만 사용할 경우
> private 생성자를 선언해 인스턴스화를 막음
> 클래스 안에서도 막고 싶다면 생성자 안에서 예외 던짐
```java
public class Student {
	private Student(){
		throw new AssertionError();
	}
}
```

#### i.5 싱글톤이 추천되지 않는 클래스와 의존성 주입
> 클래스 내부적으로 하나 이상의 자원에 의존하고, 영향을 받는다면, 싱글톤이 아닌 생성자를 통한 의존성 주입을 하는 방법이 유연성, 재사용성이 증가됨

#### i.6 객체의 재사용
> 불변 객체의 경우 재사용에 안정성이 보장되므로, 재사용 하는 방향으로 작성
```java
// 클래스 생성으로 스트링 객체를 생성하면 매번 추가 메모리 공간을 사용
String a = new String("string");
// 아래 처럼 생성할 경우 같은 문자열의 경우 같은 메모리 공간을 공유
Stirng b = "string";
```
> 위 예시 외에도, 정규식을 사용한 string.matches() 