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
# 특정 버전 전역 사용
fvm use {version} --force 
# 버전 목록 조회
fvm list 
```
#### 앱 빌드
> 안드로이드
```bash
# 기본 빌드 방법
flutter build apk
# 플랫폼 지정 빌드 방법
flutter build apk --target-platform android-arm64
# 릴리즈 모드 빌드
flutter build apk --release
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

###### FutureBuilder
>비동기 작업 후 빌드하기 위한 위젯
>* 내부적으로 builder 메서드 내에서 snapshot 으로 진행 상태를 가짐 ([ConnectionState 객체](https://api.flutter.dev/flutter/widgets/ConnectionState.html))
>* build 메서드가 상태 변경에 따라 실행되므로, 메서드 내부에 페이지 이동 등을 할 경우 주의 필요(예외 발생)
>	* [addPostFrameCallback](https://api.flutter.dev/flutter/scheduler/SchedulerBinding/addPostFrameCallback.html)
```dart
FutureBuilder<List<DosingModel>>(  
    future: fetchData(),  
    builder: (context, snapshot) {  
      if (snapshot.connectionState == ConnectionState.waiting) {  
        return const Center(child: CircularProgressIndicator());  
      } else {
		  // 1. 이벤트 루프에 대기하여 빌드 이벤트가 끝 나고 실행되도록 설정 방법
          Future.delayed(Duration.zero, () => Get.offNamed('/'));
          // 2. 위젯이 빌드된 이후 실행되는 콜백을 등록 하는 방법
          WidgetsBinding.instance.addPostFrameCallback(() { 
	          Get.offNamed('/'); 
		  });  
          return const SizedBox.shrink();
      }
      ...});  
```

##### 로컬라이징

> 공식 라이브러리 보다 쉽게 로컬라이징 설정
* [이지 로컬라이제이션](https://pub.dev/packages/easy_localization)
> 언어별 파일 sheet로 관리(작성 후, 이지 로컬라이제이션에 맞는 양식으로 변환)
 * [sheet_loader_localization](https://pub.dev/packages/sheet_loader_localization)

타이틀 로컬라이징
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


#### WebView
* [webview_flutter 공식 플러그인](https://pub.dev/packages/webview_flutter)
>공식 플러그인이므로, 추후 지원 및 업데이트 보장 
* [flutter_inappwebview 서드파티 플러그인](https://pub.dev/packages/flutter_inappwebview)
>다양한 옵션 제공  
>* iOS WKUIDelegate(웹페이지 UI 메소드) 지원


##### 광고
> [adMob 설정 방법](https://codelabs.developers.google.com/codelabs/admob-ads-in-flutter?hl=ko#0)

# Dart
> 변수
> * var: 초기 값으로 자료형이 결정
> * dynamic: 자료형이 대입 된 자료형에 따라 지속 변화

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
>* NoSQL DB


#### [freezed](https://github.com/rrousselGit/freezed/blob/master/resources/translations/ko_KR/README.md) & [json_serializable](https://pub.dev/packages/json_serializable)
>* freezed : 모델을 정의할 때 필요한 코드 생성기
>	* [freezed](https://www.youtube.com/watch?v=i5p6wXLAX7I) 사용법 영상
>* json_serializable : toJson, fromJson 코드 생성기 



#### 기타
> WidgetsFlutterBinding.ensureInitialized 함수
> 	 * 플러터 엔진 및 서비스와 플러그인 사용을 초기화 하는 메서드
> 	 * 주로 main 함수에서 실행되며, 주로 네이티브 환경이 필요한 라이브러리 초기화 시 필요
> 	 * 구성요소
> 		 1. `ServicesBinding` 플러그인을 초기화하고 서브시스템 접근 제어 및 관리하며, 플랫폼 메시지를 수신하고 처리하는 역할
> 		 2. `PaintingBinding` 이미지 디코딩 및 이미지 캐시, 폰트 관리.
> 		 3. `RenderBinding` 렌더 트리 관리
> 		 4. `WidgetBinding` 위젯 트리 관리
> 		 5. `SchedulerBinding` 는 애니메이션, 타이머, 비동기 작업 등의 스케줄링을 관리
> 		 6. `SemanticsBinding` 사용자 편의를 위한 접근성 정보 수집 및 이벤트 관리
> 		 7. `GestureBinding` 는 제스처 이벤트 관리

>shared_preferences
>* 디바이스 내에 로컬 저장공간에 간단한 데이터를 저장하기 위해 사용하는 key,value 형식의 라이브러리
>* 동기화 기능을 제공하지 않으므로, 다중 isolate 상황에서는 한쪽에서 변경된 값을 다른 isolate에도 바로 반영되지 않음(2024.01.25 기준)

> 24.01.25
> * flutter_background_service 라이브러리 사용 중에 사용된 어노테이션
```dart
@pragma('vm:entry-point')
```
> * [vm:entry-point 에 대한 공식문서 내용](https://github.com/dart-lang/sdk/blob/master/runtime/docs/compiler/aot/entry_point_pragma.md)
> * [vm:entry-point 스택오버플로의 답변 내용](https://stackoverflow.com/questions/64314719/what-does-pragmavmprefer-inline-mean-in-flutter)
> * 이해한 내용 요약
> 	* Dart 에서 컴파일 시, Tree Shaking 을 통해 사용되지 않는 코드를 제거하는 최적화 과정에서 호출되지 않는 함수를 명시적으로 제거하지 않고 유지하기 위해 사용

>24.01.26
>* flutter_ringtone_player 라이브러리 설치 후 checkdebugduplicateclasses 에러 발생
>	* android/build.gradle 파일 내에 ext.kotlin_version 버전을 올려서 해결


>24.04.20
>* build.gradle, setting.gradle 설정 파일의 형식 변경 발생(3.16 이전에 생성된 프로젝트)
>* 아래 오류 내용
```
You are applying Flutter's app_plugin_loader Gradle plugin imperatively using the apply script method, which is deprecated and will be removed in a future release
```
>* [공식 문서 내 해당내용](https://docs.flutter.dev/release/breaking-changes/flutter-gradle-plugin-apply) 

## 무료강의
* [Flutter 로 웹툰 앱 만들기](https://nomadcoders.co/flutter-for-beginners?gclid=CjwKCAiAleOeBhBdEiwAfgmXf_89CWEtkhR17GavHw6X3Il3vs8_d_CqwjIJJTnnl5qBkbWaANdsfBoCWM4QAvD_BwE)
