## Types

보통 언어들은 Integer, String, Float 등과 같이 간단한 타입들이 있지만 러스트는
보다 다양한 타입들을 가지고 있다.

예를 들어 Integer 의 경우 아래와 같은 타입들을 가진다.

>  + +&#160; plus sign
>  - -&#160; minus sign
> 
> 8bits = 1 byte  
> 아래는 비트 표현
> 
> (**Signed - i**, **Unsigned - u**)
> 
> i8, i16, i32, i64, i128, and isize. <br>
> u8, u16, u32, u64, u128, and usize. 
> 
> i8 범위 [-16 ~ 15]  
> u16 범위 [0 ~ 65,536]  
> _**u128** can hold up to 340282366920938463463374607431768211455_
>
> <br>
> 
> isize, usize : computer architecture 에 따른 것
> 32비트, 64비트에 따라 나뉨
> 
> 32비트일 경우 isize -> i32
> 

러스트의 경우 타입을 꼭 명시하지 않아도 된다.


```
// Chars란 ?
fn main() {
    let space = ' '; // A space inside ' ' is also a char
    let other_language_char = 'Ꮔ'; // Thanks to Unicode, other languages like Cherokee display just fine too
    let cat_face = '😺'; // Emojis are chars too
    char = 4 bytes
    }
```

캐스팅을 'as' 키워드로 할 수 있다.
char 의 경우 캐스팅을 하게되면 아스키코드로 변환이 된다.

```
fn main() {
    let my_number: u16 = 8;
    // let my_number = 8_u8; 위와 완전히 동일하며 _는 몇개가 있어도 상관없다.
    let second_number: u8 10;
    let my_char = 'a' as u8;
    let my_number = 9.; // f64 float 임
    let third_number = my_number + second_number as u16;
    println!("My char is {}", my_char); // My char is 97
```

## println!();

```
fn give_age() -> i32 {
    10
}

fn main() {
    let my_name = "riv";
    let my_age = 10;
    println!("My name is {} and my age is {}", my_name, my_age);
    println!("My name is {} and my age is {}", my_name, give_age()); // 위와 같은 결과
```

