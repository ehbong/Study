# flutter

* [flutter 위젯 튜토리얼](https://www.youtube.com/playlist?list=PLIKnSA4GMR4NXpNdCtJOL0BhWcxX_BBHJ)
* [입문자를 위한 강의](https://www.youtube.com/watch?v=Yt-DjG5b4iA&list=PLnIaYcDMsScxP2Nl8pEbmI__wkF0YVu0a)
* [플러터 3.0.0 Version 업데이트 정리](https://kdjun97.github.io/flutter/flutter-version-3/)
* [플러터 보일러 플레이트](https://github.com/zubairehman/flutter-boilerplate-project/tree/master)

###### Widgets
> stateless widgets
> * 변화가 없고, 상태가 없는 위젯
> stateful widgets
> * 모양과 상태가 변경되는 위젯
> widget tree
> * widget들을 부모,자식 관계로 엮은 구조

##### BuildContext
> * 위젯트리상의 현재 위치 식별
> * 위젯트리 내에서 상,하위 관계 식별
> * 위젯설정 및 테마 정보 접근
> * 네비게이터에 접근
###### 기본 파일 구조
> pubspec.yaml
> * 메타데이터를 담은 파일
> 각 플랫폼 이름의 폴더(ios, android, macos, windows)
> * 배포를 위한 파일들
# Dart
> 변수
> * var: 초기 값으로 자료형이 결정
> * dynamic: 자료형이 대입된 자료형에 따라 지속 변화

> final 과 const 
> * 둘다 한번 값을 대입하면 변경할 수 없는 상수
> * final: 런타임 시 값이 정해지는 상수
> * const: 컴파일 시 값이 정해지는 상수

> 접근제어
> * 기본적으로 public
> * 변수 및 메서드 명에 시작을 _ 로 시작할 경우 private로 같은 파일 안에서만 사용 가능
> * get , set 을 이용해서 특정 행위만 가능하게 제어
```dart
class MyClass {
	int _privateVar = 10;_
	int get myValue => _privateVar;
	set myValue(int value) => _privateVar = value;
}
```

> 자료형
> * int: 64비트 보다 크지 않은 정수 값 -2^63~2^63-1 까지(웹에서는 -2^53~2^53-1)
> * double: 64비트 부동 소수점 숫자
> * num: int와 double의 상위 개념, 둘다 허용
> * String: 문자열

> 상속, 구현, 기능추가
> * class and extends : 클래스와 상속 (다중 상속 불가)
```dart
class A {} // 부모
class B extends A {} // 자식 
```
> * abstract class and implements : 추상 클래스 와 구현 (다중 구현 가능)
```dart
abstract class MyInterface1 {
  void method1();
}

abstract class MyInterface2 {
  void method2();
}

class MyClass implements MyInterface1, MyInterface2 {
  @override
  void method1() {
    // 구현
  }
  @override
  void method2() {
    // 구현
  }
}

```
> * mixin and with : 기능 추가(다중 기능 추가 가능)
```dart
mixin Logging { 
	void log(String message) { 
		print('로그: $message'); 
	} 
} 
class Dog with Logging { 
	String name; 
	Dog(this.name); 
	void bark() { 
		log('$name가 멍멍 짖습니다.'); // mixin 으로 with 한 메서드를 사용
	} 
}
```
###### 함수
> 특정 매개변수만 받고 싶을 때
```dart
class Person {
	String? name;
	int? age;
	String? sex;
	// {} 괄호로 감싸면 특정 매개변수만 입력 가능
	Person(String name, {int age = 0, String sex = 'male'}){
	  this.name = name;
		this.age = age;
		this.sex = sex;
	}
	// 아래와 같이 선언도 가능(Dart 2.0 이후)
	Person(this.name, {this.age, this.sex});
}


void main() {
  // : 을 사용해서 키:값 형태로 전달
  Person p1 = new Person('tom',age: 10);
  print(p1.age);
  print(p1.sex);
}


```


#### Getx
* [상태관리 라이브러리 getX 공식](https://pub.dev/packages/get)
* [getX 유튜브 강의](https://www.youtube.com/watch?v=RIR8W5kSfNE&list=PLgRxBCVPaZ_3bPtdyE0Tj-w1CFX01bgUE)
> Navigation
```dart
// 홈 위젯으로 이동
Get.to(Home());
// main.dart, getPages 에 등록해 놓은 설정값에 따라 이동
Get.toNamed('/');
// 뒤로 이동
Get.back();
// 이전화면 없이 이동(로그인 화면 등)
Get.off(Home());
// 이전 경로 모두 삭제 이동(회원가입 등)
Get.offAll(Home());
// 인자 값 전달 
Get.to(Home(), arguments: 'hello GetX');
Get.arguments // 사용 측(문자열)
Get.to(Home(), arguments: {'value': 'hello GetX'});
Get.arguments['value'] // 사용 측(맵)
Get.to(Home(), arguments: User(name: 'kim');
(Get.arguments as User).name // 사용 측(특정 클래스)
// url 로 값 전달 시
Get.toNamed('/user/1234')
Get.parameters['uid'] // ? 를 사용한 쿼리 파라메터도 같은 방식으로 사용

// main.dart 등록 예시
@override  
Widget build(BuildContext context) {  
  return GetMaterialApp(  // GetX 사용을 위해 MaterialApp 에서 변경
    title: 'flutterApp',  
    initialRoute: '/',  
    initialBinding: InitBinding(),  
    getPages: [  
      GetPage(name: '/', page: () => const App()),
      GetPage(name: '/user/:uid', page: () => const UserPage()),  
    ],  
  );  
}
```




## 무료강의
* [Flutter 로 웹툰 앱 만들기](https://nomadcoders.co/flutter-for-beginners?gclid=CjwKCAiAleOeBhBdEiwAfgmXf_89CWEtkhR17GavHw6X3Il3vs8_d_CqwjIJJTnnl5qBkbWaANdsfBoCWM4QAvD_BwE)
