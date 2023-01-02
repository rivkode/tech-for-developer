## variable, mutable, shadowing

variable, mutable

기본 변수는 불변성입니다. 안전성과 손쉬운 동시성이라는 장점을 취할 수 있도록 코드를 작성하게끔 강제하는 요소 중 하나입니다.

```
fn main() {
    let x = 5;
    println!("The vaule of x is: {}", x);
    x = 6;
    println!("The vaule of x is: {}", x);
```

위와 같이 하게 되면 컴파일에러가 발생합니다. 기본 변수는 불변성인데 변수 x에 두 번째로 값을 재할당
하였기 때문입니다.

변수명의 접두어로 mut 를 추가하여 `let mut x = 5;` 가변성 변수를 선언할 수 있습니다. 이를 통해 향후 코드를 보는 사람에게
해당 변수의 값을 변경할 것이라는 의도를 주지시킵니다.

### 상수의 특징 및 변수와의 차이점

상수는 mut 사용이 허용되지 않음, 상수는 바뀌지 않는 값이므로 
상수는 어떤 영역에서도 선언될 수 있다.
상수는 함수 호출의 결과값이나 그 외에 실행시간에 결정되는 값으로 설정될 수는 없다.

```
const MAX_POINTS: u32 = 100_000; // _는 rust가 읽지 않는다 즉 100000와 같다
```

shadowing

이전에 선언한 변수와 같은 이름의 새 변수를 선언할 수 있고, 새 변수는 이전 변수를 shadows 하게 됩니다.
let 키워드를 사용해서 다음처럼 반복하여 같은 변수명으로 변수를 shadow 할 수 있습니다.

```
fn main() {
    let x = 5;
    let x = x+1;
    let x = x*2;
    println!("The value of x is: {}", x);
    // The value of x is: 12
```

이는 mut와 차이가 있습니다. let 키워드를 사용하여 효과적으로 새 변수를 선언하고, 값의 유형을 변경할 수 있으면서도
동일 이름을 사용할 수 있다는 점 입니다.

```
fn main() {
    let spaces = "      ";
    let spaces = spaces.len();
    println!("{}", spaces);
    // 6
}
```

만약 mut를 사용하였다면 변수 타입 유형을 str -> num 으로 변경할 수 없으므로 컴파일 에러가 발생합니다. 


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

```
fn main() {
    let my_city = "Seoul";
    let year = 2022;
    let population = 60_000_000;
    println!(
        "The city if {city} in {year} had a population of {population},
        "The city if {0} in {1} had a population of {2}. I love {0} !,
        city = my_city,
        year = year,
        population = population
        );
}
```

## 함수 동작 원리

함수 선언 방법

```
fn main() {
    println!("Hello, world!");

    another_function();
}

fn another_function() {
    println!("Another function.");
}
//Hello, world!
//Another function.
```

함수 매개변수

```
fn main() {
    another_function(5);
}

fn another_function(x: i32) {
    println!("The value of x is: {}", x);
}
```

another_function의 선언은 x로 명명된 하나의 매개변수를 갖습니다.
반드시 각 매개변수의 타입을 정의해야한다. 이는 rust를 설계하며 내려야 하는 중요한 결정이다.
