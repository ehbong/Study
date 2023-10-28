# flutter

* [flutter 위젯 튜토리얼](https://www.youtube.com/playlist?list=PLIKnSA4GMR4NXpNdCtJOL0BhWcxX_BBHJ)
* [입문자를 위한 강의](https://www.youtube.com/watch?v=Yt-DjG5b4iA&list=PLnIaYcDMsScxP2Nl8pEbmI__wkF0YVu0a)
* [상태관리 라이브러리 getX 공식](https://pub.dev/packages/get)
* [getX 유튜브 강의](https://www.youtube.com/watch?v=RIR8W5kSfNE&list=PLgRxBCVPaZ_3bPtdyE0Tj-w1CFX01bgUE)
* [플러터 3.0.0 Version 업데이트 정리](https://kdjun97.github.io/flutter/flutter-version-3/)
* [플러터 보일러 플레이트](https://github.com/zubairehman/flutter-boilerplate-project/tree/master)

###### Widgets
> stateless widgets
> * 변화가 없고, 상태가 없는 위젯
> stateful widgets
> * 모양과 상태가 변경되는 위젯
> widget tree
> * widget들을 부모,자식 관계로 엮은 구조

###### 기본 파일 구조
> pubspec.yaml
> * 메타데이터를 담은 파일
> 각 플랫폼 이름의 폴더(ios, android, macos, windows)
> * 배포를 위한 파일들
#### Dart
> 변수
> * var: 초기 값으로 자료형이 결정
> * dynamic: 자료형이 대입된 자료형에 따라 지속 변화

> 자료형
> * int: 64비트 보다 크지 않은 정수 값 -2^63~2^63-1 까지(웹에서는 -2^53~2^53-1)
> * double: 64비트 부동 소수점 숫자
> * num: int와 double의 상위 개념, 둘다 허용
> * String: 문자열

###### 생성자
> 특정 매개변수만 받고 싶을 때
```dart
Class Person {
	String name;
	int age;
	String sex;
	// {} 괄호로 감싸면 특정 매개변수만 입력 가능
	Person({String name, int age, String sex}){
		this.name = name;
		this.age = age;
		this.sex = sex;
	}
}
// : 을 사용해서 키:값 형태로 전달
p1 = new Person(age: 10)

```
## 무료강의
* [Flutter 로 웹툰 앱 만들기](https://nomadcoders.co/flutter-for-beginners?gclid=CjwKCAiAleOeBhBdEiwAfgmXf_89CWEtkhR17GavHw6X3Il3vs8_d_CqwjIJJTnnl5qBkbWaANdsfBoCWM4QAvD_BwE)
