# flutter

* [flutter 위젯 튜토리얼](https://www.youtube.com/playlist?list=PLIKnSA4GMR4NXpNdCtJOL0BhWcxX_BBHJ)
* [입문자를 위한 강의](https://www.youtube.com/watch?v=Yt-DjG5b4iA&list=PLnIaYcDMsScxP2Nl8pEbmI__wkF0YVu0a)
* [플러터 3.0.0 Version 업데이트 정리](https://kdjun97.github.io/flutter/flutter-version-3/)
* [플러터 보일러 플레이트](https://github.com/zubairehman/flutter-boilerplate-project/tree/master)

###### [버전 관리(FVM)](https://fvm.app/)
> flutter 버전 관리 툴
> fvm설치
```bash
# mac
brew tap leoafarias/fvm # brew 에 서드파티 레파지토리 추가
brew install fvm # fvm 설치
```
> 명령어
```bash
# 플러터 설치
fvm install {version}
# 특정 버전 사용
fvm use {version}
# 버전 목록 조회
fvm list 
```

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
> * 메타데이터를 담은 파일(버전 정보, 의존성, static 파일 경로 등)
> 각 플랫폼 이름의 폴더(ios, android, macos, windows)
> * 배포를 위한 파일들
> /lib
> * main.dart 파일을 포함한 flutter 파일이 작성되는 디렉토리
> * 내부적으로 page, controller, components 등 구분 가능
> /ios, /android, 등
> * 각각 플랫폼에 맞는 설정 등이 포함된 디렉토리
> /assets
> * static 파일들 저장 경로(이미지 파일 등)

###### 라이프사이클
> 앱의 상태 별 라이프 사이클  
> * [AppLifecycleState](https://api.flutter.dev/flutter/dart-ui/AppLifecycleState.html) enum 값으로 구분
> * [WidgetsBindingObserver](https://api.flutter.dev/flutter/widgets/WidgetsBindingObserver-class.html) 클래스를 with 으로 mixin 받아서  
>   didChangeAppLifecycleState 메서드 오버라이드를 통해 상태 변화 감지  
> 상태별 설명
> * detached: 종료 상태
> * resumed: 활성화 상태, 화면에 표시 및 화면조작이 가능한 상태
> * inactive: 비활성화된 상태, 백그라운드 또는 다른앱으로 전환(전화가 왔을 때 등), 화면에 UI 표시 중
> * paused: 일시정지 상태, 백그라운드에 있지만 리소스 소비할 수 있는 상태, 화면에 UI 보이지 않음

###### 앱 종료 방법 비교
> dart:io > exit(0);
> * 운영체제에 프로세스 종료를 요청해서 앱을 강제종료
> * 프로그래밍 생명 주기를 무시하고 종료(AppLifecycleState)
> flutter/services > SystemNavigator.pop(); 
> * 현재 화면을 닫고 이전화면으로 돌아감, 첫번째 화면이라면 앱을 종료
> * 뒤로가기 를 수행할 때 실행 프로그래밍 생명 주기를 수행(AppLifecycleState)

###### [factory](https://dart-ko.dev/language/constructors#factory-%EC%83%9D%EC%84%B1%EC%9E%90)
>새로운 인스턴스를 생성하고 싶지 않을때 사용하는 생성자 키워드
>* 싱글톤 패턴으로 동작
>* 기존 클래스 인스턴스 외에 하위 클래스를 반환할 수 있음
>* this를 사용할 수 없음  
>  factory 생성자는 객체를 직접 생성하는 것이 아니라, 생성된 객체를 반환하거나  
>  다른 생성자나 메서드를 호출해서 동작하므로, 현재 인스턴스를 가르키는 this를 사용할 수 없음

###### 타이틀 로컬라이징
> android
> 1. android/app/src/main/AndroidManifest.xml 파일 검색
> 2. application label 값 수정 로컬 라이징을 위해 변수 지정 @string/app_name
> 3. android/app/src/main/res/values/ 폴더안에 strings.xml 파일 생성
> 4. resources 태그 생성 후 안에 string 태그 네임은 app_name 태그 안에 지정할 앱 이름 지정
> 5. android studio 사용 시 open editor 로 수정 창열고, add Locale 버튼 클릭 해서 지원 국가 추가 후 명칭 입력
> 6. 아닐 경우 values-ko 폴더 생성 후 strings.xml 파일 생성해서 똑같이 작성하고 app_name 안쪽에 한글 명 입력
> 
> ios
> 1. xcode 실행 해서 ios/Runner.xcworkspace 파일로 프로젝트 열기
> 2. project > Runner 선택해서 info에 Localizations 추가(추가 실패 시 시뮬레이터 설치 여부 확인)
> 3. 왼쪽 메뉴에서 Runner 아래 New Group으로 Localization 폴더 생성
> 4. New File 로 InfoPlist.strings 파일 생성(파일 이름 대소문자 주의)
> 5. 파일 선택된 상태에서 우측 Localize... 버튼 클릭 후 팝업에서 korean 선택후 Localize 버튼 클릭
> 6. 우측에 추가된 Korean 체크
> 7. 왼쪽에 InfoPlist 아래 InfoPlist(Korean), InfoPlist(English) 추가 확인
> 8. 각각 선택 후"CFBundleDisplayName" = "지정할 앱이름 각각의 언어로 작성"
> 9. 우측 목록에서 Runner 아래 Info.plist 선택 후
> 10. Bundle display name 항목을 제거

###### Drawing based animation
> * [Rive](https://rive.app/)
> * [Lottie](https://lottiefiles.github.io/lottie-docs/)



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

> Null safety(dart 2.12 이상
> * 클래스 내에 선언된 변수는 null이 될 수 없음
```dart
String a; // 오류
String? b; // null 일 수 있음을 명시적으로 선언
a = b.toUpperCase(); // b 가 null 일 수 있으므로 오류 발생
a = b!.toUpperCase(); // ! 는 값이 null 이 아님을 명시
late String c; // 나중에 초기화 하겠다는 것을 명시
// late 를 사용할 경우 사용 시점에 초기화
late String d = someFunc(); // 이렇게 선언할 경우 변수 사용 시점에 someFunc가 실행됨
```

###### 비동기
> Future, Stream 으로 두가지의 형태가 존재
> * Future : 한번의 응답을 하는 경우
> * Stream : 지속적인 응답이 필요한 경우
```dart
// 비동기로 값을 리턴하는 함수
Future<int> f(int s) async {
  await Future.delayed(Duration(seconds: s));
  print('');
  return s;
}

// void 면 상관없으나,
// 비동기로 처리된 값을 받아야 한다면 아래와 같이 처리
void main() async {
  // 이렇게 처리할 경우 await 가 비동기의 종료를 기다려서 동기처리 됨
  await f(3);
  await f(5);
  await f(2);

  List<Future<int>> futures = [
    f(3),
    f(5),
    f(2),
  ];
  // 동시 처리되어야 할 객체를 Future.wait를 사용해서 동시 처리되도록 설정
  // future seconds : 2, 3, 5 순서대로 출력 됨
  List<int> results = await Future.wait(futures);
  print(results); // [3, 5, 2]
}

```

###### 병렬처리[(Isolate)](https://dart-ko.dev/language/concurrency#isolate-%EC%9E%91%EB%8F%99-%EB%B0%A9%EC%8B%9D)
>Isolate: 다트에서 사용하는 병렬처리의 작업 단위
>* 웹 플랫폼을 제외한 다트 플랫폼에서 지원
>* 다트 코드는 스레드가 아닌 isolate의 내부에서 실행
>* 다트는 main isolate가 있고, 필요 시 isolate를 추가해서 사용
>* isolate는 멀티프로세스 형태(독립적인 메모리와 이벤트 루프)의 다트 런타임에서 실행되는 경량 스레드
```dart
void main() async {
  // 데이터 읽기.
  final jsonData = await Isolate.run(_readAndParseJson);

  // 데이터 사용.
  print('Number of JSON keys: ${jsonData.length}');
}

Future<Map<String, dynamic>> _readAndParseJson() async {
  final fileData = await File(filename).readAsString();
  final jsonData = jsonDecode(fileData) as Map<String, dynamic>;
  return jsonData;
}
```


###### [extension](https://dart.dev/language/extension-methods)
> Dart 2.7 버전부터 도입된 기능으로 기존 클래스에 새로운 기능을 추가할 때 사용
> * 상속 등으로 가능하지만 조금 더 직관적으로 변경 가능
> * 동적 유형에서는 extension 메서드 호출 불가
> * var 로 선언한 추론형에서는 사용 가능
> * 이름 없는 확장도 가능하지만, 이름이 없으면 메서드명 충돌을 해결하기 어려움
```dart
// 선언 방법
// extension <명칭> on <타입>{}
// 
}
extension NumberParsing on String {
  int parseInt() {
    return int.parse(this);
  }
  // ···
}

dynaic d = '2';
d.parseInt() // Runtime exception: NoSuchMethodError
```

###### 특별한 연산자
> cascade
```dart
// 오브젝트를 반환하는 경우 .. 을 통해서 오브젝트의 결과 값에 접근이 가능하다.
// cascade 연산자 사용할 때
var paint = Paint()
  ..color = Colors.black
  ..strokeCap = StrokeCap.round
  ..strokeWidth = 5.0;
// 일반적인 방법  
var paint = Paint();
paint.color = Colors.black;
paint.strokeCap = StrokeCap.round;
paint.strokeWidth = 5.0;
```
> spread
```dart
// 컬렉션을 병합 추가할 때 사용
var list = [1, 2, 3];
var list2 = [0, ...list]; //[0, 1, 2, 3]
var list3 = [0, ...?list]; // list가 빈값일 수 있으면 ? 를 추가
```

#### GetX
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


#### [Isar](https://isar.dev/)
>로컬 DB
>* 


## 무료강의
* [Flutter 로 웹툰 앱 만들기](https://nomadcoders.co/flutter-for-beginners?gclid=CjwKCAiAleOeBhBdEiwAfgmXf_89CWEtkhR17GavHw6X3Il3vs8_d_CqwjIJJTnnl5qBkbWaANdsfBoCWM4QAvD_BwE)
