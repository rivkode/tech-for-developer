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
> i8, i16, i32, i64, i128, and isize. **Signed - i**<br>
> u8, u16, u32, u64, u128, and usize. **Unsigned - u**
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