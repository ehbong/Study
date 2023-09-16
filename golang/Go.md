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
> 상수
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
// range 함수 사용
var intA [5] int64 = [5]int64{3, 2, 1, 4, 5}
for i

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


### orm
* [gorm 공식 페이지](https://gorm.io/docs/)
