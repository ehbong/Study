* [공식문서](https://www.rust-lang.org/)
* [easyRust](https://github.com/Dhghomon/easy_rust/?tab=readme-ov-file#part-1---rust-in-your-browser)
* [easyRust 문서](https://dhghomon.github.io/easy_rust/Chapter_0.html)

### 자료형

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