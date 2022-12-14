# 좋은객체지향프로그래밍_SOLID

---

좋은 객체 지향 프로그래밍이란?

## 역할과 구현을 분리

자바언어

- 자바언어의 다형성을 활용
  - 역할 - 인터페이스
  - 구현 - 인터페이스를 구현한 클래스, 구현 객체
- 객체를 설계할 때 **역할** 과 **구현**을 명확히 분리
- 객체 설계시 역할(인터페이스)을 먼저 부여하고, 그 역할을 수행하는 구현 객체 만들기

> 구현보다 인터페이스가 먼저이다


## 객체의 협력이라는 관계부터 생각

- 혼자있는 객체는 없다.
- 클라이언트 : 요청, 서버 : 응답
- 수 많은 객체 클라이언트와 객체 서버는 서로 협력관계를 가진다.

> 다형성을 생각할때 막연하게 상속, 오버라이딩 등등 생각할 수 있지만 클라이언트, 서버를 주의깊게 생각해보자.


## 자바 언어의 다형성

- 오버라이딩을 사용한다.
- 다형성으로 인터페이스를 구현한 객체를 실행 시점에 유연하게 변경할 수 있다.
- 클래스 상속 관계도 다형성, 오버라이딩 적용 가능

![다형성](https://user-images.githubusercontent.com/109144975/203838249-44863ca8-a934-4446-9008-0eb9204ffbc2.JPG)

## 다형성의 본질

- 인터페이스를 구현한 객체 인스턴스를 실행시점에 유연하게 변경할 수 있다.
- 다형성의 본질을 이해하려면 **협력**이라는 객체사이의 관계에서 시작해야함
- 클라이언트를 변경하지 않고, 서버의 구현 기능을 유연하게 변경할 수 있다.


## 역할과 구현을 분리

정리
- 실세계의 역할과 구현이라는 편리한 컨셉을 다형성을 통해 객체 세상으로 가져올 수 있음
- 유연하고, 변경이 용이
- 확장 가능한 설계, 클라이언트에 영향을 주지 않는 변경 가능
- 인터페이스를 안정적으로 잘 설계하는 것이 중요


한계
- 역할(인터페이스) 자체가 변하면, 클라이언트, 서버 모두에 큰 변경이 발생한다.
- 자동차를 비행기로 변경해야한다면 ? -> 수많은 기능들이 추가되어야 함
- 대본 자체가 변경된다면 ? -> 로미오, 줄리엣이 모두 다시 변경된 내용을 알아야 함
- 따라서 인터페이스를 안정적으로 잘 설계하는 것이 중요함


스프링과 객체 지향

- 다형성이 가장 중요하다!
- 스프링은 다형성을 극대화해서 이용할 수 있게 도와준다.
- 스프링에서 이야기하는 제어의 역전(IOC), 의존관계 주입(DI)은 다형성을 활용해서 역할과 구현을 편리하게 다룰 수 있도록 지원한다.
- 스프링을 사용하면 마치 레고 블럭 조립하듯이, 공연 무대의 배우를 선택하듯이, 구현을 편리하게 변경할 수 있다.



## SOLID
### 클린코드로 유명한 로버트 마틴이 좋은 객체 지향 설계의 5가지 원칙을 정리

## SRP 단일 책임 원칙

단일 책임 원칙
(single responsibility principle)


- 한 클래스는 하나의 책임만 가져야 한다 → 애매함
- 중요한 기준은 변경이다. 변경이 있을 때 파급 효과가 적으면 단일 책임 원칙을 잘 따른 것.




클래스를 변경하는 이유는 단 한가지의 책임에서 시작해야 한다.

SRP를 지키기 위해 하나의 클래스는 반드시 하나의 일만 할 수 있어야 하는 것은 아닙니다.

쉽게 말해 코드의 변경을 해야할때 최소한의 책임을 가지게 하는 것이라 할 수 있습니다.
여기서의 책임은 하나의 특정 엑터를 위한 기능 집합이며, 엑터란 기능(=클래스, 모듈)을 사용하는 주체입니다.

SRP를 적용 전

<br>






OCP 개방 폐쇄 원칙
- 이는 클라이언트와 서버가 있다고 가정하였을때
- 클라이언트 코드의 변경 없이 서버의 구현객체를 바꿔줄 수 있어야 한다는 개념이다
- 인터페이스를 활용하여 구조를 만들었다 하여도 이와 같은 원칙이 깨질 수 있다.

LSP 리스코프 치환 원칙
- 기능적으로 무조건 보장이 되어야 함
- 즉 앞으로 가는 엑셀의 기능이 있다고 가정할때 다른 기능으로 변경하여 느리게 가더라도 앞으로는 가야함

ISP 인터페이스 분리 원칙
- 적당한 크기의 인터페이스로 나누어야 함

## DIP 의존관계 역전 원칙

의존성 역전
(Dependency Inversion Princple)


- 클라이언트가 구현체 즉 구현 클래스를 바라보고 의존하는 것이 아닌 구현의 역할인 인터페이스를 바라보고 의존해야 함
- 구현에 의존하면 안됨 역할에 의존하도록 설계해야함

> 의존의존하는데 → 의존이 뭘까 ?
> 
>코드에서 의존은 해당되는 클래스, 파라미터등을 알고 있다는 것이다.

![Untitled](https://user-images.githubusercontent.com/109144975/203948768-2d383bac-79c8-486c-aaf1-2276e43be19b.png)

위 예시에서는 MemberService 에서 memberRepository 라는 인터페이스뿐만아니라 MemoryMemberRepository 라는 구현체까지도 알고 있다는 것이다.

즉 MemberRepository 가 구현체를 직접 선택하고 있음 → 구현체에 의존하고 있음

<br>

다형성을 안전하고 편리하게 적용할 수 있는 메커니즘이 등장하기 전에 소프트웨어는 아래 그림과 같이 main 함수가 고수준 함수를 
호출하고, 고수준 함수는 다시 중간수준 함수, 저수준 함수 순으로 호출한다. 이러한 코드 의존성의 방향은 반드시 제어흐름을 따르게 된다.

![](https://user-images.githubusercontent.com/109144975/205373526-16172d97-b643-4dc8-a19d-293c5e31beb1.png)

위와같이 코드 흐름이 진행되면 개발자가 소스 코드를 설계할때 선택지가 줄어들게 된다. 제어 흐름은 시스템의 행위에 따라 결정되며 소스 코드 의존성은 제어 흐름에 따라 결정된다.

하지만 인터페이스를 사용하게되면 특별한 일이 일어난다.

> 인터페이스를 사용하게 되면 의존성 역전이 발생한다

위 말이 무슨 의미일까? 아래 사진을 보자

![](https://user-images.githubusercontent.com/109144975/205373600-30174e37-75ed-4d04-b57e-28cd032f53ca.png)


위 사진을 보게 되면 HL1 모듈은 ML1 모듈의 F() 함수를 호출한다. 소스 코드에서는 HL1모듈은 인터페이스 I 를 통해 F() 함수를 호출한다. 이 인터페이스는 런타임에 존재하지 않으며 HL1은 단순히 ML1 모듈의 함수 F()를 호출 할 뿐이다.

여기서 중요한 점은 ML1과 I 인터페이스 사이의 소스 코드 의존성(상속관계)이 제어흐름과는 반대인 점이다.

> 쉽게 말해 인터페이스를 활용하여 상황에 따라 구현체를 넣는 방식으로 코드를 작성한다면 의존관계가 역전이 된다.
> 

이를 의존성 역전 dependency inversion 이라 부르며, 소프트웨어 아키텍트 관점에서 이러한 현상은 심오한 의미를 갖는다.

위 접근법을 사용한다면, 시스템의 소스 코드 의존성에 전부에 대해 방향을 결정할 수 있는 권한을 갖게 된다. 즉, 소스 코드 의존성을 원하는 방향대로 결정할 수 있다.



## 정리

>객체지향의 핵심은 다형성
>
>하지만 다형성만으로는 쉽게 부품을 갈아 끼우듯이 개발할 수 없다. → 구현객체를 변경할 때 클라이언트 코드도 함께 변경된다
>
>다형성만으로는 OCP, DIP를 지킬 수 없다.