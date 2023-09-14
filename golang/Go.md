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
> 		* int8 의 경우 -128 ~ 127 인데 
> 		  1000 0000 의 경우 -0이 아니라 -128 을 가리킴
> 	* 기본 값 0
> *  float32, float64
> 	* 실수자료형
> 	* 뒤에 숫자는 크기(bit)
> 	* 기본 값 0.0
> 	* 지수부(10의 몇승인지 표현), 소수부(정수로 표현된 수치)로 표현됨 
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



### orm
* [gorm 공식 페이지](https://gorm.io/docs/)
