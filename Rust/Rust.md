* [공식문서](https://www.rust-lang.org/)
* [easyRust](https://github.com/Dhghomon/easy_rust/?tab=readme-ov-file#part-1---rust-in-your-browser)
* [easyRust 문서](https://dhghomon.github.io/easy_rust/Chapter_0.html)

### 자료형

##### Collection types
> ***Array***  
> * 길이가 고정인 배열
> * 길이가 다르면 다른 타입으로 인식해서 비교할 수 없음
```rust
fn main() {
	let array = ["1", "2"]; // [&str; 2]
	let array2 = ["1", "2", "3"]; // [&str; 3]
	// 타입의 형태로 선언 가능
	let array3 = [0; 10]; // 0이 10개 들어있는 array
}
```
> * Slices: 배열 분할
```rust
let array = ["0", "1", "2"];
// rust 가 slices를 사용할 때 원본에 소유권을 유지한 체 참조의 형태로 사용하도록 함
// 따라서 &array[0..2] 로 하면 제대로 실행
// 0 시작 2는 2앞에 까지 즉 0, 1 까지 출력
println!("{:?}", array[0..2]); // error
println!("{:?}", &array[0..2]); // ["0", "1"]
println!("{:?}", &array[0..=2]); // ["0", "1", "2"]
```
> ***Vec***  
> * 길이가 동적인 배열
> * String 도 Vec으로 구현
```rust
let a = String::from("a");
let b = String::from("b");

let mut abc_vec = Vec::new();

abc_vec.push(a);
abc_vec.push(b);
println!("{:?}", abc_vec); // ["a", "b"]
println!("{}", abc_vec.capacity()); // capacity 메서드는 점유한 데이터 공간 개수
// 데이터가 4개 이하면 4, 5~8개는 8, 8~16은 16 으로 기존 데이터 공간을 초과하면 2배씩 확장

// 다른 초기화 방법
let abc_vec = vec![a, b];
```
> ***Tuples***  
> * 길이가 고정된 배열
> * 다양한 자료형을 포함하도록 허용
```rust
// 정의
let tuple: (i32, f64, char) = (42, 3.14, 'a');

// index 접근
tuple.0 // 0번 인덱스 접근, tuple[] 이 아니라 . 을 찍고 그뒤에 index 표기

// 패턴 매칭
let person: (&str, u8) = ("Alice", 30);
let (name, age) = person;

println!("{:?}", name); // "Alice"
println!("{:?}", age); // 30

match person {
	// 튜플의 첫 번째 요소가 "Alice"인 경우
	("Alice", age) => println!("Hello Alice! You are {} years old.", age),
	// 그 외의 경우
	(_, age) => println!("Hello! You are {} years old.", age),
}

```

##### Copy Type
> * 값의 소유권 이전 없이 복사가 이루어지는 타입
> * 기본타입들에 해당(정수, 소수, 부울 등)

##### shadowing
> 같은 이름의 변수가 반복해서 선언되었을 때 기존 변수가 사라지는 것이 아닌, 숨어있는 상황
```rust
fn main() {
    let my_number = 8;
    println!("{}", my_number); // 8
    {
        let my_number = 9.2; // 같은 이름 변수 선언
        println!("{}", my_number) // 9.2
    }
    // 괄호안에 변수가 소멸되면서 기존에 선언했던 값이 출력 
    println!("{}", my_number); // 8
}
```

### Reference
>* ***&*** : immutable reference 수정 불가능
>* ***&mut*** : mutable  reference 수정 가능
```rust
fn main() {
    let country = String::from("Austria");
    let ref_one = &country; // 수정 불가 참조
    let ref_two = &country; // 여러번 참조 가능

    println!("{}", ref_one);
    
	let mut my_number = 8;
    let num_ref = &mut my_number; // 수정 가능 참조
    // 가변 참조는 1개만 가능, 불변 참조와 동시 사용 불가
    *num_ref += 10; // * 는 참조를 값으로 사용한다는 의미
    println!("{}", my_number);
}
```
>* 함수 호출 시
```rust
fn print_country(country_name: String) {
    println!("{}", country_name);
}

fn print_country2(country_name: &String) {
    println!("{}", country_name);
}

fn main() {
    let country = String::from("Austria");
    let country2 = String::from("Korea");
    print_country(country); // 값으로 넘길 경우 소유권이 함수로 넘어감
    print_country(country); // 앞의 호출이 종료되며 변수가 소멸되어 호출 불가
	print_country2(&country2); // 참조로 할 경우 여러번 호출 가능(가변 참조도 가능)
	print_country2(&country2);
}
```

### Match
> 패턴 매칭
> * Elixir 의 패턴 매칭과 유사
> * Switch 문과 비슷 해 보이지만 다름
> 	* match 는 다양한 자료형 지원(변수, 리터럴, 열거형, 튜플 등)
> 	* match 는 반드시 일치 값이 존재(없으면 컴파일 에러)
> 	* match 는 패턴의 중첩 허용
> 	* match 안에 if 문도 허용
```rust
fn main(){
    let children = 0;
    let married = false;
    
    match (children, married) {
    // 패턴 매칭 이후, 안에 if 문으로 추가 조건 가능
        (children, false) if children > 0 => println!("Not married with {} children", children),
        (0, true) => println!("married but with no children"),
        _ => println!("Some other type of marriage and children combination")
    }
    
}
```