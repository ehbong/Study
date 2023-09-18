# GO

* [공식문서](https://go.dev/)
* [유튜브 강의](https://www.youtube.com/watch?v=KBdz5c-0t1w&list=PLy-g2fnSzUTBHwuXkWQ834QHDZwLx6v6j)
* [go Web Framework top5](https://blog.logrocket.com/5-top-go-web-frameworks/)
* [패키지 관리](https://doitnow-man.tistory.com/entry/Go-Lang-3-Package-%EA%B4%80%EB%A6%AC%EC%84%A4%EC%B9%98%EC%82%AD%EC%A0%9C%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8)

* [기초문법](https://gyurious.tistory.com/42)

#### 자료형
> 숫자 타입
> * uint, uint8, uint16, uint32, uint64
> 	* 부호가 없는 int 
> 	* 뒤에 숫자는 크기(bit)
> 	* uint는 실행환경에 맞춰 크기 변화(32bit 면 uint32, 64bit면 uint64)
> 	* 기본 값 0
> * int, int8, int16, int32, int64
> 	* integer
> 	* 뒤에 숫자는 크기(bit)
> 	* int는 실행환경에 맞춰 크기 변화
> 	* 2진수 표현 시 맨 앞 비트는 부호 비트
> 		* int8 의 경우 -128 ~ 127
> 		* 음수는 2의 보수로 표현됨(1의 보수를 구하고 +1)
> 	* 기본 값 0
> *  float32, float64
> 	* 실수자료형
> 	* 뒤에 숫자는 크기(bit)
> 	* 기본 값 0.0
> 	* 지수부(10의 몇승인지 표현), 가수부(분수)로 표현됨 
> 	* 소수부 크기로 인해 32는 7자리, 64는 15자리 까지만 표현 가능
> * byte
> 	* uint8 의 별칭 타입
> * rune
> 	* 한글자를 나타내는 자료형
> 	* 한글자가 3byte이상이 필요함
> 	* int32 의 별칭 타입
> 기타
> * bool
> 	* true or false
> 	* 8bit(1byte) 크기
> 	* 기본 값 false
> * string
> 	* 유니코드를 지원하는 바이트의 배열
> 	* 불변형으로 생성된 문자열은 수정될 수 없고, 수정하려면 새로 생성됨
> 	* 문자열 리터럴이 같을 경우 복사 생성하지 않고 공유
> 	* 기본 값 ""
> 형변환 시 주의 사항
> * 크기가 큰 자료형에서 작은 자료형으로 형변환 할 때,
>    작은 자료형의 크기보다 데이터가 클 경우 데이터가 소실 돼서 다른 값으로 변경 발생

#### 변수, 상수
> 변수
> * 사용하지 않은 변수 선언 시 오류 발생
> * 2개 이상의 반환 값을 받는 함수를 사용할 때, 사용하지 않는 변수는 _ 로 지정하면 오류 방지
> 상수
> * 컴파일 시점에 알고 있는 값만 상수로 선언 가능
> * 특정파일의 값을 불러와서 선언하거나, 실행 시점에 선언 불가능
```go
    // const 로 선언
    // const 상수명 자료형 = 대입 값
	const FloatPI float64 = 3.14

	// 타입을 지정하지 않을 경우 사용할 때 결정 됨
	const PI = 3.14
    var a int = PI * 100 // 결과 값이 소숫점이 생기면 오류 발생
    var b int = FloatPI * 100 // 컴파일 에러 발생
	// 괄호로 일괄 선언 가능
	// iota 는 괄호 안 몇번째 선언된 상수인지 반환 초기값 0
	// 선언 생략하면 앞에 값 기준으로 선언 
    const (
	    Red int = iota
	    Blue int = iota
	    Green
	    Yellow
    )
```


#### 조건문
> if
> * 조건 실행 전 초기화 가능
```go
// if 초기화 ; 조건 {}
// 초기화 변수의 스코프가 제한
// if에서 초기화 한 변수는 else 에서도 사용
if a := 1; a >= 1{
	fmt.Print(a)
}
```
> switch case
> * 값을 기준으로 조건을 나눌 때
> * break를 생략해도 기본값으로 동작
> * 뒤로도 진행하고 싶으면 fallthrough 추가
```go
a := 5
switch a {
	case 1:
		fmt.Println("1 입니다.")
	case 2:
		fmt.Println("2 입니다.")
	case 3:
		fmt.Println("3 입니다.")
		fallthrough // 다음 case도 진행
	default:
	    fmt.Println("없는 수 입니다.")
} 
```
> * True를 사용해서 case 에 조건을 줄 수 있음(if 문 사용 권장)
```go
a := 5
switch true {
	case a > 5:
		fmt.Println("5초과 입니다.")
	case a > 3:
		fmt.Println("3초과 입니다.")
	case a > 1:
		fmt.Println("1초과 입니다.")
	default:
	    fmt.Println("1이하 입니다.")
} 
```
>*\ if 문 처럼 초기화 블록 사용 가능

#### 반복문
> for
> * while 문이 없이 for 문만 존재
```go
// 조건 반복문
tf := true
for tf {
}
// 무한 방복문 
for {
}
// 기본 반복문
for i:=0; i < 10; i ++ {
}
// 인덱스 외부 변수 반복문
x := 0
for ; x < 10; x++ {
}
for x < 10{
	x++
}
// range 사용
// i는 index, v는 값
var intA [5] int64 = [5]int64{3, 2, 1, 4, 5}
for i, v := range intA {
	fmt.Println(i, v)
} 

```
> * label 이 존재
```go
// label 을 사용해서 break 시 특정 반복문까지 중지 시킬 수 있다.
//  
i : = 0
LabelName:
for i < 10{
	for j:=0; j < 10; j++{
		if 특정조건{
			break LabelName
		}
	} 
}
```

#### 배열
> 선언
```go
// 기본
// var 변수명[크기]자료형 = [크기]자료형{데이터}
// 데이터 생략 시 각 자료형 기본값으로 초기화
var a[3]int = [3]int{1, 2, 3}

// 3크기만큼 0으로 초기화
var b[3]int

// 자동 크기 지정
// {} 안에 값 개수만큼 배열크기 지정
var c = [...]int{1, 2, 3}

// 동적으로 배열 크기를 지정할 수 없음
// 컴파일 시 배열의 크기를 할당해야함으로
// 변수로 배열 크기를 지정할 수 없음
// 상수는 배열 크기로 지정 가능
var i int = 3
var d[i]int // 컴파일 에러
```

#### 구조체
> 유사성이 있는 데이터의 묶음
> * 다른 언어의 dto와 비슷함
> 선언
```go
// type 타입명 struct
type Person struct {
	age int8
	name string
}
// 다른 구조체를 포함하는 구조체
type Student struct {
	Person // 구조체를 풀어서 포함
	person Person // 구조체 안에 구조체를 그룹지어 포함
	grade int8
	class string
}
```
> 구조체 메모리 정렬
> * 구조체의 필드에는 순서가 존재
> * CPU가 읽기 쉽게 하도록 특정 데이터 크기 단위로 데이터가 정렬 됨
> * 필드 중 가장 큰 메모리 기준으로 데이터 크기가 정의되고, 그보다 작은 데이터는 패딩이 발생
> * 예) 2, 4, 8 byte의 데이터가 있을 경우 2+4+8= 14가 아니라 16byte의 저장공간을 차지함  
>          2+4+(패딩2)+8 과 같은 형식으로 16byte를 차지함
> * 데이터 정렬은 순서에 따라 같은 데이터여도 다른 저장공간을 차지
> * 예2) 2, 8, 4의 경우 16이 아니라 24byte를 차지 (2+6(패딩)) +8+ (4+4(패딩))
> 사용 이유
> * 데이터를 구조화
> * 코드 가독성, 재사용성 증가
> * 데이터의 일관성과 안정성 유지
> * 클래스가 없이 객체 지향을 구현을 위해 사용


#### 문자열
> 선언
```go
    // 한줄 표시, 개행문자 등 특수문자 삽입 가능
	str1 := "동해 물과\n 백두산이"
	// 개행 등을 반영한 결과 값 저장
	str2 := `동해 물과
	         백두산이`
```
> 특징
> * 불변형
```go
var str string = "Hello World"
str = "How are you?" // 전체 바꾸기 가능(실제로는 기존 데이터와 별개로 복사해서 저장)
str[2] = 'a' // 일부 변경은 불가능 오류 발생

// 자바와 동일하게 string을 + 연산으로 결합할 경우 계속 새로운 메모리에 저장
// 이에 해당 작업 실행 시 string 을 그대로 사용하면 메모리 낭비 및 gc 작업 증가
// strings.Builder 사용, 내부적으로 slice 로 동작(동적 배열)
var builder strings.Builder

builder.WriteRune('A') // 한글자 추가 Rune 자료형
builder.WriteString("BCDEFG") // 문자열 추가

builder.String() // string 으로 변환
```
> * 참조형(포인터가 가르키는 8바이트 헤더)
> 	* 문자열 데이터의 실제 주소 data
> 	* 바이트 길이 len
```go
// data 와 len 확인 방법
var s1 string = "hello"
// 현재 권장 되지 않는 방법
// stringHeader1 := *(*relect.StringHeader)(unsafe.Pointer(&s1))
// 대체 방법
stringHeader1 := *(*[2]uintptr)(unsafe.Pointer(&s1))
```
> * len(str)  을 통해 길이 확인 시 바이트 크기 반환
```go
// 문자열의 문자 길이 확인 하는 방법 1
// rune 자료형의 배열로 만들어서 배열의 길이를 확인하는 방법
len([]rune(str))

// utf8.RuneCountInString
```
### orm
* [gorm 공식 페이지](https://gorm.io/docs/)
