# JAVA

> JRE(Java Runtime Environment): 자바 실행 환경
> * JVM, 표준 클래스 라이브러리

> JDK(Java Development Kit): 자바 개발 키트
> * JRE, 컴파일러, 디버거 등의 개발도구

## JVM
#### Class Loader
> * Loading: 바이트 코드(.class)를 메모리로 로드
>   * 부트스트랩 클래스 로더: 표준 자바 패키지 로드
>   * 확장 클래스 로더: 확장 라이브러리 클래스 로드
>   * 어플리케이션 클래스 로더: 직접 작성한 클래스 파일 로드 
> * linking: 의존관계 분석 및 링크
>   * 검증: 클래스 파일의 형식 및 메모리 접근 권한 등을 확인
>   * 준비: 정적 필드에 메모리 공간 할당(생성자 호출 전 우선 모든 필드값은 0으로 초기화)
>   * 해결: 클래스 간의 상속, 구현 등을 매핑하는 과정
> * initialization: 생성자 호출
>   * 클래스 생성자 호출
>   * 정적 필드에 0이 아닌 실제 초기값으로 설정
>   * 동기화 이슈가 발생할 코드는 생성자에 포함 금지


#### Runtime Data Area: 실시간 데이터 구역
> * 메소드 영역: 모든 클래스 정보와 클래스의 정적 필드, 상수, 메소드 데이터를 저장
> * 힙 영역: 객체의 인스턴스와 배열을 저장(가비지 컬렉션의 주요 대상이 되는 영역)
> * 스택 영역: 실제로 프로그램이 실행되는 과정에 필요한 데이터를 스택 구조로 관리하는 영역  
>            메소드 단위로 프레임이라는 내부 스택 구조를 생성하고  
>            각각 필요한 정보를 메소드 영역 및 힙 영역에서 가져와서 실행 됨
> * PC(program counter) 레지스터 영역: 현재 실행 중인 명령어의 주소를 가리키는 레지스터
> * 네이티브 메소드 스택: 자바 코드가 아닌 네이티브 코드 호출 정보 저장
#### Excution Engine: 실행 엔진
> interpreter 와 JIT Compiler를 혼용해서 사용
> * interpreter: 바이트 코드를 한줄 씩 해석 실행
> * JIT(Just In Time) Compiler: 인터프리터로 실행된 코드 중 실행 빈도가 높은 코드 블록을 네이티브 코드로 변환, 캐싱

#### Garbage Collector: 가비지 컬렉터
> 힙 영역에 사용하지 않는 데이터를 제거
* [가비지 컬렉션 알고리즘 및 메모리 관리](https://www.programmersought.com/article/4905216600/)


#### JIT 컴파일러
> 자주 사용되는 코드에 대해 바이트 코드로 변환해서 성능을 향상
> * final 선언 된 객체의 경우 직접 초기화 된 것은 상수로, 동적 초기화 된 것은 변수로 처리
<br><br>
----
> ****형변환****  
> int를 float로 형 변환 시 float의 가수 영역이 23비트이므로 23비트를 초과하는 수를 형변환 하면 값의 정밀도를 보장할 수 없다.
> 따라서 int를 실수로 변경 시 명확하게 범위를 특정할 수 없다면 double을 사용해서 값의 손실을 방지 할 수 있다.

* [maven 기본 세팅](https://byul91oh.tistory.com/304)

* [동시성이슈 해결](https://thalals.tistory.com/370)

* [DI, IOC 간단 설명](https://velog.io/@gillog/Spring-DIDependency-Injection)

#### JAVA 가 call by value 인 이유
> * 원시 타입은 매개변수로 전달 시 스택영역에 메소드 단위 케이스에 복사해서 전달
> * 참조 타입은 매개변수로 전달 시 참조 주소 값을 복사해서 들어가서, 주소 값 영역을 공유하지는 않음  
    따라서 참조 타입을 전달했을 때, 해당 객체를 직접 수정하면 기존 객체에도 영향이 가지만  
    대입 연산자로 새로 대입할 경우, 기존 객체를 대체 함
> * call by value는 변수에 할당 된 값을 전달(원시 데이터 또는 참조 데이터의 주소 값)
> * call by reference는 변수의 주소 자체를 전달(참조 데이터의 주소 값이 아닌 변수 자체의 주소)


<br><br>
----
### 상속, 구현
* 업 캐스팅, 다운 캐스팅
```java
 // TestA 를 상속받은 TestB, TestB를 상속받은 TestC가 있을 때
 TestA a = new TestA();
 TestA b = new TestB();
 TestA c = new TestC();
```
> 업 캐스팅  
> * 위 코드 처럼 A에 대입했을 때, 자식 클래스 객체가 부모 클래스로 형변환 되는 것
> * 형변환 되면서 자식 클래스만 가지고 있던 필드 및 메소드의 접근이 제한
```java
 TestB b2 = (TestB)b;
```
> 다운 캐스팅  
> * 업캐스팅 된 객체를 명시적으로 지정해서 다시 자식클래스로 형변환 하는 것
> * 기존 자식 클래스만 가지고 있던 필드와 메소드들을 복구
> * 형 변환 시, 실제 자식클래스의 객체가 아닌 부모 클래스의 객체를 형변환 시 오류 발생(instanceof 로 확인 필요)

> 추상 클래스 상속과, 구현(인터페이스) 차이
> * 추상 클래스는 추상 메소드 외에 일반 메소드를 생성 가능
> * 자바에서 상속은 다중 상속 불가
> * 인터페이스는 추상 메소드와 필드만 가능
> * 인터페이스는 형식만 있기 때문에 구현체에서 실제 동작을 구현해야하고, 이로 인해 다중 인터페이스 구현이 가능.



<br><br>
----
#### 정적 변수, 메소드
> * 정적 메소드는 클래스 로더가 클래스를 로딩해서 메소드 메모리 영역에 적재
> * 정적 메소드 및 블록 사용 시 주의
>   * 정적 메소드 및 블록은 클래스 객체가 생성 되기 전에 생성 되므로, 클래스 내 인스턴스 필드 및 메소드에 접근할 수 없음
>   * 접근 하려면 블륵 내에서 new키워드로 클래스 객체를 생성 후 접근 가능
>   * GC가 동작하지 않으므로, collection 변수를 사용할 때는 주의 필요(메모리 무한 점유 발생)


#### 접근 제한자
> 아래로 갈수록 제한이 강화
> |접근제한|적용대상|접근금지 대상|
> |----|----|----|
> |public|클래스,필드,생성자,메소드|없음|
> |protected|필드,생성자,메소드|자식 클래스가 아닌 다른 패키지에 소속된 클래스|
> |default|클래스,필드,생성자,메소드|다른 패키지에 소속된 클래스|
> |private|필드,생성자,메소드|모든 외부 클래스|


### 어노테이션  
> 어노테이션 용도  
> * 컴파일러 지시: @override, @Deprecated
> * 런타임 처리: @RequestMapping, @Bean
> * 코드 분석 및 문서화: @Author, @Version


### String
> 불변성을 가진 이유
> * 캐싱: 가장 많이 사용되는 자료형으로, String pool를 이용해 같은 값에 대해 같은 주소를 가르키도록 변경
> * 보안: String 객체도 참조형이므로, 실행 중 일어나는 외부 변경에서 안전하기 위해
> * 스레드 안전성: 여러 스레드에서 String 객체를 참조한다고 해도, 변수에 새로운 값을 할당 할 수 있지만 heap 영역에 String 객체는 변하지 않음
> 문자열 결합  
> * String: 짧은 문자열 결합에 사용(+ 로 결합할 때 마다 메모리 복사가 이루어져서, GC의 부하가 발생 => 불변성 때문에)
> * StringBuilder: 스레드의 안전여부와 상관없이 사용할 때 사용(메모리 복사를 하지 않음, 메소드 내부 변수 등)
> * StringBuffer: 스레드에 안전이 필요하거나 필요한지 모를 때 사용(메모리 복사 하지 않음, 클래스의 Static 문자열 또는 싱글톤 클래스의 문자열 등)

### 컬렉션
> Collection. 
> * 데이터를 그룹화하고 관리하기 위한 자료구조들의 집합  
> * 제네릭 지원, 동적 크기 지원
> 종류
> 	* List
> 		* LinkedList : 연결 리스트
> 		* Stack: 스택 자료 구조
> 		* Vector: 동기화 보장 배열 
> 		* ArrayList : 배열
> 	* Set
> 		* HashSet: 순서 보장 하지 않는 set
> 		* SortedSet: 순서 Set
> 	* Map
> 		* Hashtable: 동기화 보장 Map
> 		* HashMap: 기본 Map
> 		* TreeMap: 키의 null을 허용하지 않음, 정렬 트리 구조
> HashSet 에서 중복을 비교할 때, 객체의 hashCode, equals 메소드로 확인을 하기 때문에,  
> 동일한 값을 가지는 객체를 저장하지 않으려면 두 메소드를 override 해서 구현하면 된다.

#### 리스트
> 리스트 구현 클래스별 특징
> |대상|설명|장단점|사용처|
> |----|----|----|----|
> |ArrayList|기본동적배열|인덱스 접근 빠름, 크기 동적 조절, 삽입삭제 느림, 메모리 소비 많음|변경이 적은 경우|
> |Vector|thread safe ArrayList|ArrayList와 비슷한 장단점 가짐, synchronized사용|단일 스레드에서 ArrayList보다 성능이 느림|스레드로부터 안전이 필요할 때|
> |LinkedList|이중연결리스트|요소 삽입 및 삭제 빠름, 엑세스 시간 느림, 반복 엑세스 느림, 메모리 소비 많음|요소의 삽입 및 삭제가 빈번할 경우|

#### HashMap
> HashMap의 구현 원리
> 1. key와 value를 가진 클래스를 만든다.(HashMap 클래스 안에 Map.Entry<K,V> 의 구현체 Node클래스)
> 2. LinkedList<Node<K,V>>[] 형태의 배열을 만든다.
> 3. 해시버킷의 크기(배열의 크기) 기본 값으로 배열을 초기화 한다.
> 4. hash 메서드를 만들고, 해시 값 범위를 해비버킷 크기를 초과하지 않게 작성한다.
> 5. 값을 넣을 때
> 	1. key로 hash 코드를 구해서 위에 작성한 배열의 index로 넣어서, 배열에 값이 있느지 확인 한다.
> 	2. 배열에 값이 없으면 new LinkedList<Node<K,V>>() 를 통해 새로운 연결리스트를 만든다.  
> 	   (이 때 버킷 크기를 확인해서 버킷크기의 특정 비율만큼의 크기를 초과하면, 버킷크기를 늘린다.)  
> 	   버킷 크기를 늘리지 않으면 hashKey의 중복이 늘어서 속도 저하가 발생한다.
> 	4. 해당 연결리스트에 new Node<K, V>(key, value); 형태로 add한다.
> 6. 값을 찾을 때
> 	1. key로 hash 코드를 구해서 배열에 해당 값이 있는지 확인한다.
> 	2. 값이 있으면, 연결리스트를 반복문으로 돌며 키와 비교해서 값을 찾아 반환한다.
> 7. 값을 반환할 때: 찾을 때와 동일한 방법으로 찾아서, 삭제 처리한다.

### 제네릭  
> 제네릭 사용 이유  
> * 타입 안정성: 컴파일러의 타입체크
> * 타입 변환 감소: 컴파일러에게 타입을 지정해서 불필요한 형변환을 줄일 수 있음
> * 재사용성과 유연성 증가: 다양한 타입을 수용할 수 있음
> * 제네릭은 컴파일 시점에 타입 체크 및 자동 형변환을 제공하고 바이트 코드에는 사라짐
> * 이는 제네릭 기능 추가 이전 시점의 자바와의 호환성과도 관련 있음
```java
// 임의로 타입을 지정한 경우 바이트 코드로 변환 되면서 Object 타입으로 지정
// Object 타입이기 때문에 Ojbect 타입에 있지 않은 필드 및 메서드 사용 불가
public <T> T getValue(T input){
	return input;
}
// Object로 선언 됐지만, 아래와 같이 입력 매개변수에 맞춰서
// 제네릭의 타입추론 기능으로 자동으로 형변환
Integer intValue = getValue(12);
String strValue = getValue("Hello");
```

### enum (열거형)
> 서로 관련된 상수를 선언하기 위한 자료형
```java
// 기본 사용
enum Type1 {
 TYPE_A, TYPE_B, TYPE_C
}
// 값 포함하여 선언
enum Type2 {
	TYPE_A(100), TYPE_B(200), TYPE_C(300);
	
	public final int value;
	
	Type2(int value){
		this.value = value;
	}
}
// 값 사용
Type2.TYPE_A.value // 100

// 추상 메서드 사용
enum Type3 {
	TYPE_A(100) {
		@override
		long sum(int someValue){
			return value + someValue;
		}
	},
	TYPE_B(200) {
		@override
		long sum(int someValue){
			return value + someValue;
		}
	},
	TYPE_C(300) {
		@override
		long sum(int someValue){
			return value + someValue;
		}
	};
	public final int value;
	// 생성자
	Type2(int value){
		this.value = value;
	}
	// 추상 메서드
	abstract long sum(int someValue);
}

// 값 사용
Type3.Type_A.sum(200) // 300

```


### 의존성 주입
#### 의존성 주입 어노테이션
> * @Autowired: 스프링 지원, 타입에 맞게 연결
> * @Inject: 자바 지원, 타입에 맞게 연결
> * @Resource: 자바 지원, 이름, 타입에 맞게 연결  
    @Resource(name='aClass'): 명시적인 name 값이 있을 때 이름 기준 연결, 없으면 타입 기준 연결

#### Error
> 시스템의 비정상적인 동작으로 발생한 경우
> * OutofMemoryError : 메모리 부족
> * StackOverflowError : 스택공간 부족
> 위 vm 에러 외에 [링크 참고](https://docs.oracle.com/javase/8/docs/api/java/lang/Error.html)
### Exception
> CheckedException : 컴파일 처리 예외(ClassNotFoundException, IOException, SQLException...)  
> * 예외가 발생할 수 있는 상황을 미리 예측하고, 이에 대한 처리를 강제(try catch 를 강제)
> * Checked Exception을 던지거나 처리하지 않으면 컴파일 오류가 발생
> * Exception 클래스를 상속받은 클래스 중 RuntimeException 클래스를 상속받지 않은 모든 Exception 
> UnCheckedException: 런타임 처리 예외(NullPointException, ArrayIndexOutOfBoundsException...)
> * 예외 처리를 강제하지 않으며, 개발자의 실수나 프로그램 논리 오류로 인해 발생
> * RuntimeException 클래스를 상속받은 모든 Exception


### 리플렉션
> 컴파일 시점이 아닌 실행 시점에 클래스의 멤버에 접근하거나 수정하는 기능  
> 동적으로 클래스 멤버를 사용, 변경이 필요할 때 사용  
> 런타임 시점에 클래스 분석이 필요해서 성능 이슈가 발생할 수 있음
```java
// 리플렉션은 컴파일 시점에 결정되지 않은 동적 대상에 대해,
// 런타임 시점에 지정해서 실행하도록 기능 제공
public class Book{
	public void read(){
		System.out.println("read Book")
	}
}
public class Main{
	public static void main(String[] arg) throws ClassNotFoundException, ...{
		// 일반적인 클래스 인스턴스 생성 방법
		// 어떤 클래스 인스턴스를 생성할지 코드 작성 단계에 알고 있음
		Book objBook = new Book();
		// 리플렉션을 이용한 클래스 및 인스턴스 생성 방법
		// Book이란 클래스 name은 동적으로 변경 할 수 있음
		Class bookClass = Class.forName("Book");  
		// 이 단계에서 컴파일 단계에서는 obj는 Object로 인식해서
		// Book 클래스의 인스턴스 임에도 obj.read() 로 메소드를 실행하도록 코드를 작성할 수 없음
		// 하지만 런타임 시점에 JVM에서 obj가 Book 클래스의 인스턴스임을 확인
		Object obj = bookClass.newInstance();
		// m Book 클래스의 read 메소드 참조를 넣음
		Method m = bookClass.getDeclaredMethod("read", null);  
		// obj가 Book 클래스의 인스턴스임을 알고 있는 JVM 이 read 메소드를 실행
		m.invoke(obj, null);
	}
}

```
* [리플렉션 코드 설명](https://hudi.blog/java-reflection/)
* [리플렉션, 스프링 DI 동작에 대해](https://velog.io/@suyeon-jin/%EB%A6%AC%ED%94%8C%EB%A0%89%EC%85%98-%EC%8A%A4%ED%94%84%EB%A7%81%EC%9D%98-DI%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EB%8F%99%EC%9E%91%ED%95%98%EB%8A%94%EA%B1%B8%EA%B9%8C)

### 멀티스레드
* [멀티스레드 예제](https://withhamit.tistory.com/522)
> Thread 클래스
> * 스레드를 직접적으로 생성하고 제어하는 클래스
> * start 메소드를 호출하여 스레드를 실행
> * 상속 받아서 run 메소드를 오버라이드 해서 새로운 동작을 구현할 수 있음
```java
class MyThread extends Thread {
    @Override
    public void run() {
        // 스레드 동작을 정의
    }
}
```
> Runnable 인터페이스
> * Thread 클래스를 상속받지 않고 스레드를 사용하기 위한 인터페이스
> * 인터페이스 구현체 클래스를 생성하고 run 메소드를 오버라이드 해서 새로운 동작을 구현할 수 있음
> * Thread 클래스의 생성자에 매개변수로 전달해서 스레드 객체를 생성할 수 있음
```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        // 스레드 동작을 정의
    }
}

// 스레드 생성 및 실행
Thread thread = new Thread(new MyRunnable());
thread.start();
// 스레드 작업이 끝날 떄 까지 대기
// 대기 하지 않으면 메인스레드가 먼저 종료 시, 스레드 작업 완료를 보장하지 않음
thread.join();
```


###### Supplier
> 자바스크립트의 함수를 인자로 전달하는 것처럼 메소드 자체를 전달하기 위해 자바8 부터 도입된 기능
> java.util.function.Supplier
```java
import java.util.function.Supplier;

public class Main {
    public static void main(String[] args) {
        // 제네릭에는 메소드가 리턴하는 자료형
        // 클래스명::메소드명 문법은 클래스 안에 메소드를 참조하겠다는 문법
        Supplier<Integer> supplier = Main::calculateValue;

        // 메소드를 아래와 같은 방식으로 .get() 하는 순간 실행
        int result = supplier.get();
        System.out.println("Result: " + result);
    }

    private static int calculateValue() {
        return 42;
    }
}

```