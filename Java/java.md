# JAVA

> JRE(Java Runtime Environment): 자바 실행 환경
> * JVM, 표준 클래스 라이브러리  
> JDK(Java Development Kit): 자바 개발 키트
> * JRE, 컴파일러, 디버거 등의 개발도구

> 메모리 영역
> * 메소드 영역: 모든 클래스 정보와 클래스의 정적 필드, 상수, 메소드 데이터를 저장
> * 힙 영역: 객체의 인스턴스와 배열을 저장(가비지 컬렉션의 주요 대상이 되는 영역)
> * 스택 영역: 실제로 프로그램이 실행되는 과정에 필요한 데이터를 스택 구조로 관리하는 영역
>            메소드 단위로 프레임이라는 내부 스택 구조를 생성하고 각각 필요한 정보를 메소드 영역 및 힙 영역에서 가져와서 실행 됨

> 형변환
> int를 float로 형 변환 시 float의 가수 영역이 23비트이므로 23비트를 초과하는 수를 형변환 하면 값의 정밀도를 보장할 수 없다.
> 따라서 int를 실수로 변경 시 명확하게 범위를 특정할 수 없다면 double을 사용해서 값의 손실을 방지 할 수 있다.

* [maven 기본 세팅](https://byul91oh.tistory.com/304)

* [멀티스레드 예제](https://withhamit.tistory.com/522)

* [동시성이슈 해결](https://thalals.tistory.com/370)

* [DI, IOC 간단 설명](https://velog.io/@gillog/Spring-DIDependency-Injection)
