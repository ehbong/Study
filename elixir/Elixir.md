
#### Elixir 의 특징
> 패턴매칭
> * 엘릭서에서 a = 1 는 단순 대입이 아닌 패턴매칭이다.
```elixir
a = 1
1
1 = a
1
2 = a
```
> 1. a = 1 은 변수에 1을 매칭(대입) 하면서 같은 값을 만든다
> 2. 1 = a 는 1과 a가 같은 지 확인한다.
> 3. 2 = a 는 2와 a가 같은지 확인한다. 다르므로 오류가 발생한다.
> 4. 변수가 좌변에 있을 때는 대입과 매칭이 동시에 이루어진다.

> 불변성
> * 일반적인 프로그래밍 언어와 다르게 엘릭서에서는 모든 값이 불변이다.
> * 배열을 수정하거나 해도 새로운 배열로 복사된다.
> * 이를 통해 동시성 처리에 유리하다.
> * 데이터의 복사에 따른 비용은 작은 프로세스 단위로 해서 힙 영역의 크기를 줄이거나
>   기존 데이터를 참조하는 형식의 복사를 통해 비용을 줄인다.


#### 자료형
###### 내장 자료형
>값 타입
>* 정수: 저장할 수 있는 크기의 제한이 없으며, 10진수 외에 16진수(0x), 8진수(0o), 2진수(0b) 를 값 앞에 붙여 표현할 수 있다. 또한 큰 크기의 숫자를 100_000 과 같이 언더스코어로 자릿 수를 구분해 표현할 수 있다.
>* 실수: 부동소수점 방식 IEEE 754 배정밀도 형식을 따른다.
>* 아톰: 다른 언어의 상수 문자열과 비슷한 역할을 수행하는 자료형
```elixir
:abc123
:<>123/aw
:"asd123"
```
> * 범위: start...end 방식으로 작성하는 2개의 정수 값과 사이의 연속된 값을 표현하는 자료형
>   1.12 버전부터는 start...end\/\/step 방식으로 숫자를 건너뛰는 범위를 만들 수 있다.
> * 정규식: ~r{정규표현식}, ~r{정규표현식}옵션

>시스템 타입
>* 프로세스 ID: 프로세스 고유 식별자
>* 포트: 외부 프로세스와 통신을 위해 사용되는 추상화 인터페이스
>* 레퍼런스: 고유 값을 생성하기 위한 자료형

>컬렉션 타입
>* 튜플: 상수형 리스트, 생성된 후 값을 변경하거나 추가, 삭제가 불가능 {} 중괄호를 이용해 표현
>* 리스트: 링크드리스트의 형태를 가진 자료형, 머리는 값 꼬리는 다른 리스트를 가지는 방식의 리스트
>	* | 파이프 연산자와 패턴 매칭을 이용해서 머리와 꼬리를 분리해서 받을 수 있다.
```elixir
# 파이프 연산자를 활용한 패턴매칭
[head | tail ] = [1, 2, 3]
head # 1
tail # [2, 3]

# 리스트 결합
[1, 2, 3] ++ [4, 5] # [1, 2, 3, 4, 5]

# 평탄화
List.flatten([[1],2, [[3, 4], 5]]) # [1, 2, 3, 4, 5]

# 특정 index 수정
# List.replace_at(리스트, 인덱스, 바꿀 값)
# 링크드리스트 구조이므로 비용이 큼
List.replace_at([1,2,3], 2, "num") # [1, 2, "num"]
```
>   임의의 위치의 값에 접근하는 속도가 느리다. [] 대괄호를 이용해 표현
>* 키워드 리스트: 키-값 쌍으로 이루어진 리스트
>   2-튜플형식의 리스트로 변환된다.
```elixir
[name: "Tom", city: "DE"] # 단축문법
[{:name, "Tom"}, {:city, "DE"}] # 실제 변형된 값

# 키로 접근하기
# List.keyfind(리스트, 값, 값의 index, 없을 경우 대체 출력 값)
# 값이 없을 경우 nil 또는 대체 값
List.keyfind([{:name, "Tom"}], "Tom", 1)
```
>* 맵: 키 값으로 이루어진 자료형
>	* 키로 문자열, 튜플, 아톰 등을 지원한다.
>	* 키워드 리스트와 차이는, 맵은 키가 중복될 수 없다.
>	* %{key=> value} 의 형태를 가진다.
>	* 아톰을 키로 사용할 경우 앞에 :이 생략된다, 
>	   키가 아톰인 경우 %{name: "Tom", age: 15} 형식으로 표현할 수 있다.
```elixir
# 선언 및 키에 접근
person = %{"name"=>"Tom"}
person["name"] # 값이 없을 경우 nil 반환
person2 = %{name: "Tom", age: 10, sex: "M"} # "" 없이 작성하면 아톰 키로 인식
person2[:name] # 키가 아톰일 경우 앞에 : 를 표기
person2.name # . 을 통해 접근 가능, 단 점을 통해 호출할 경우 없으면 오류 발생
# Map 모듈 사용
Map.keys person2 # [:name, :age, :sex]
Map.values person2 # ["Tom", 10, "M"]
Map.drop person2, [:sex] # %{name: "Tom", age: 10}
Map.put person2, :weight, 80 # %{name: "Tom", age: 10, weight: 80}
Map.hash_key? person2, :name # true
Map.pop person2, :age # { 10, %{name: "Tom", weight: 80}} {추출 값, 제외한 맵}
Map.equal? person, person2 # false
```
>* 바이너리: 이진 데이터를 표현하는 데 사용되는 자료형 <<데이터>> 형식으로 표기
>   <<데이터::size(비트수)>> 와 같이 데이터의 크기도 지정 가능
>* 날짜와 시간: 1.3 이후 생긴 날짜와 시간을 다루는 타입

> 참과 거짓 그리고 연산자
> * 참과 거짓: true, false, nil 이 있고 false, nil 이 아닌 모든 값은 참이다.
> * 연산자
> 	* 비교 연산자
> 		* a === b 값과 자료형 모두 일치해야 참
> 		* a !== b 값과 자료형 하나라도 다르면 참
> 		* a == b 값이 같으면 참
> 		* >, < 의 비교 연산이면 일반적으로 비교 가능한 연산이면 연산자대로 처리되고 아니면
> 		  다음과 같은 규칙을 따른다.
> 			* 숫자 < 아톰 < 레퍼런스 < 함수 < 포트 < 프로세스ID < 튜플 < 맵 < 리스트 < 바이너리
> 	 * 연결 연산자
> 		 * 바이너리 연결: <<1, 2>> <> <<3, 4>> 
> 		 * 리스트 연결: list1 ++ list2 
> 		 * 리스트1을 복사해서 리스트2에 포함된 값들 제거: list1 -- list2
> 	 * in 연산자: a in enum a 가 enum 에 있는지 확인, map일 경우는 a가 {키, 값} 형식의 튜플형식 필요
> 	 * 정규식 확인 연산자:  문자열 =~ 정규식 형태로 사용하며 문자열이 정규식 패턴에 일치하는지 확인해서 참, 거짓을 반환

#### 함수
###### 익명 함수
> * 이름을 가지지 않은 함수
> * 변수에 담아서 사용할 수 있다.
> * fn 내용 end 의 구조를 가진다.
```elixir
# 파라메터를 괄호로 감싸거나 생략할 수 있다.
sum = fn a, b -> a + b end
# 익명함수를 사용할 때는 sum() 이 아닌 sum.() 처럼 점을 찍고 괄호를 써야한다.
sum.(1, 2) # 3
```
> * 함수 작성 블럭 fn..end 안에 여러개의 매개변수 타입과 반환 값을 가질 수 있다.
> * 매개변수의 값, 형태에 따라 맞는 패턴이 호출 된다.
> * 단 하나의 함수 선언안에서 매개변수의 수는 같아야한다.
```elixir
find_zero = fn
  0, 0 -> "둘다 0"
  0, _ -> "첫번째가 0"
  _, 0 -> "두번째가 0"
  _, _ -> "0이 없음"
end

find_zero(0, 3) # 첫번째가 0
find_zero("a", 0) # 두번째가 0
find_zero("a", "b") # 0이 없음
find_zero(0, 0) # 둘다 0
```
###### 함수 특징
> 클로저
> * 함수는 자신이 선언될 때 환경을 기억한다.
```elixir
greeter = fn name ->
  fn -> "Hello #{name}" end
end

tom = greeter.name('Tom') # 바깥의 함수가 이 순간 종료되지만 안에 내부함수가 값을 기억한다.
tom.() # Hello Tom
```
>함수 매개변수 고정
>* 핀 연산자(^)를 사용한 것처럼 변수를 고정시킬 수 있다.
```elixir
greeter = fn name, greeting ->
	fn
		# ^name 으로 지정할 경우 바깥 함수의 name 값을 기억한다.
		# ("Tom") -> "#{greeting} #{name}" 처럼 하드코딩한 것과 같이 동작한다.
		(^name) -> "#{greeting} #{name}" 
		(_) -> "I don't know you"
	end
end

name_check = greeter.("Tom", "Hello")
name_check.("Tom") # Hello Tom
name_check.("Jack") # I don't know you
```
>& 표기법
>* 짧은 단축함수를 작성하는 방법
```elixir
# & + 리턴값의 형태 또는 함수 + &1, &2 매개변수의 순서
# &(&1 + 1) 일반적인 함수 형태
# &abs(&1) 특정 함수를 호출하는 형태
# &[&1...&2] 리턴 값이 리스트인 형태
# &{div(&1, 2), div(&2, 2)} 리턴 값이 튜플인 형태
sum = &(&1 + &2)
sum(1, 2) # 3
```

> |> 파이프 연산자
> * 앞의 함수의 리턴 값을 다음 함수의 첫번째 파라메터로 제공하는 문법
> * 파이프연산자를 사용할 때는 파라메터에 괄호가 필수
```elixir
// 파이프 연산자 없는 코드
// 각각의 결과 값을 변수에 담아서 전달
other = other_function()
new = new_function(other)
baz_r = baz(new)
bar_r = bar(baz_r)
foo_r = foo(bar_r)
// 또는
// 함수의 실행 순서가 안쪽에서부터 바깥쪽으로 진행되므로 가독성이 나쁨
foo(bar(baz(new_function(other_function()))))


// 파이프 연산자 코드
// 함수의 실행 순서대로 나열
other_function() |> new_function() |> baz() |> bar() |> foo()
```

> import 문법
> * 문법
```elixir
// 기본 문법
import 모듈이름

// 특정 함수만 불러올 때
// only: 이후에 불러올 함수를 키,값 형식의 리스트로 작성
// 키는 함수 이름, 값은 함수의 인자 값 개수
import List, only: [last: 1]

// 특정 함수를 제외하고 불러올 때
// except: 특정 함수를 제외할 때
import List, except: [last: 1]
```
>* alias : import 를 짧게 줄여 쓰는 방식
```elixir
// 기본 문법
alias My.Other.Module.Parser, as: Parser
alias My.Other.Module.Runner, as: Runner
// 단축 문법
alias My.Other.Module.Parser
alias My.Other.Module.Runner
// 또는 
alias My.Other.Module.{Parser, Runner}
```
>모듈 속성
>* 모듈에 포함하고 있는 일종의 상수(컴파일 시점에 정해진 값)와 비슷한 설정 값
>* 같은 이름의 속성 값을 여러번 설정할 수 있다.
>* 같은 이름의 속성 값을 여러번 살정할 경우 정의될 당시의 값을 기억한다.
```elixir
@name value

// attr 이라는 속성이 2번 선언되고, 사용됐다.
defmodule Example do
	@attr "one"
	def first, do: @attr
	@attr "two"
	def second, do: @attr
end
// 실행 시 second 함수는 선언 당시의 attr 값인 two를
// first 함수는 선언 당시의 attr 값인 one 을 기억해서 출력한다.
IO.puts("Example.second: #{Example.second}, Example.first: #{Example.first}")
```
