* [공식문서](https://www.rust-lang.org/)
* [easyRust](https://github.com/Dhghomon/easy_rust/?tab=readme-ov-file#part-1---rust-in-your-browser)

### 자료형



### Reference
* & : immutable reference 수정 불가능
* &mut : mutable  reference 수정 가능
```rust
fn main() {
    let country = String::from("Austria");
    let ref_one = &country; // 수정 불가 참조
    let ref_two = &country; // 여러번 참조 가능

    println!("{}", ref_one);
    
	let mut my_number = 8;
    let num_ref = &mut my_number; // 수정 가능 참조
    *num_ref += 10; // * 는 참조를 값으로 사용한다는 의미
    println!("{}", my_number);
}
```