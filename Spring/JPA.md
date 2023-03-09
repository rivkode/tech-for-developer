# JPA

---

# 목차

- JDBC
- JPA
  - ORM
  - JPA
  - Entity
    - 엔티티의 분류
    - 속성(Attribute)
  - 컨트롤러


![JDBC](https://user-images.githubusercontent.com/109144975/198022030-c9d39efc-4eea-45aa-ac9b-f5e7828ba2ad.png)

JPA를 들어가기 전

# JDBC

JDBC는 자바의 데이터 엑세스 기술의 기본이 되는 로우 레벨의 API이다. 표준 인터페이스를 제공하여 SQL 호환성만 유지된다면 JDBC로 개발한 코드는 DB가 변경되어도 그대로 재사용이 가능하다.

모든 자바의 데이터 엑세스 기술의 근간이 되는 만큼 점차 로우레벨 기술로 취급되기도 한다.(스프링 데이터 JPA와 비교해본다면 ..) 따라서 실질적으로 코드를 적으면서 사용하지는 않지만 어떤 역할을 가지고 동작하는지 알고 있는것도 중요하다.

SQL에 대한 간단한 내용(CRUD)

SQL - structured Query Language, 데이터베이스 제어 언어

DML - data manipulation language

(CRUD)

INSERT(create)

SELECT(read)

UPDATE(Update)

DELETE(Delete)

<br>

JDBC란?

자바 프로그램이 데이터베이스와 연결되어 데이터를 주고 받을 수 있게 해주는 프로그래밍 인터페이스입니다.

<br>

JDBC의 역할

- Java Database Connectivity
- 자바언어와 DB를 연결해주는 통로와 같은 것.
- 자바를 이용한 DB접속과 SQL문장의 실행, 그리고 실행 결과로 얻어진 데이터의 핸들링을 제공하는 방법과 절차에 관한 규약.
- 자바 프로그램내에서 SQL문을 실행하기 위한 자바 API.

<br>

JDBC를 사용한 이유 (저희는 JPA(스프링 데이터 JPA)를 사용하며 개념만 알고 넘어가겠습니다.)

- db 학습시 SQL이용해서 db에다 직접 값을 넣거나 조회하는 등의 일을 수행했음.
- 하지만 우리가 웹을 동작,수행시킬 때마다 매번 그럴 수는 없음.
- 그래서 프로그램이 이 일을 대신할 수 있게 만들어줘야 하는데 이때 사용하는 것이 JDBC이다.

# JPA

![JPA](https://user-images.githubusercontent.com/109144975/198022038-de3cb76a-2dc2-4962-a608-435462cf47d3.png)

## **ORM**

ORM 이란 **Object-Relational Mapping** 의 약자로, 이름 그대로 객체(Object)와 관계형 데이터(Relational data) 를 매핑하기 위한 기술이다. 이러한 매핑이 필요한 이유는 객체 지향 언어과 관계형 데이터베이스사이의 패러다임 불일치가 있기때문이다.  이 둘 간의 패러다임 불일치 때문에 개발자는 더 많은 코드를 작성해야 하며, 이는 반복적이고 실수하기 쉬운 작업이 된다. 그렇기 때문에 개발자는 **객체지향적인 설계에 집중**할 수 없게 된다. ORM이 바로 이러한 문제를 해결해 준다.

## **JPA**

Java persistance api의 약자로 영속성(persistence)관리와 O/R 매핑(ORM - Object객체와 Relational data 관계형 데이터를 매핑하기위한 기술)을 위한 표준 명세(약속?)입니다.

자바에서 데이터를 영구히 기록할 수 있는 DBMS 환경을 제공하는 API 입니다.

즉 인터페이스의 모음입니다.(구현체가 필요하겠죠? - 하이버네이트)

JPA는 애플리케이션과 JDBC 사이에서 동작합니다. 개발자가 JPA를 사용하면, JPA 내부에서 JDBC API를 사용하여 SQL을 호출하여 DB와 통신합니다. 즉, 개발자가 직접 JDBC API를 쓸 필요가 없습니다.

JPA가 생겨난 이유는 여러가지가 있습니다.

기존에는 SQL을 만들어 DB와 주고받으면서 데이터 액세스 로직을 처리하는 방식은 등장한지 수십년이 지난 레거시 기술입니다. 텍스트 문장인 SQL을 직접 작성하고 파라미터를 바인딩(바인딩은 일반적으로 하나를 다른 것으로 매핑시키는 것을 의미)해야하는 수고와 번거로움이 있다.

ORM이란 이렇게 오브젝트와 RDB 사이에 존재하는 개념과 접근 방법, 성격의 차이 때문에 요구되는 불편한 작업을 제거해주며 자바 개발자가 오브젝트를 가지고 정보를 다루면 ORM 이 RDB에 적절한 형태로 변환해주어 더 이상 SQL문장을 직접 작성할 필요가 없습니다. - 기술개발에 집중 가능



![Untitled](https://user-images.githubusercontent.com/109144975/198024056-02f240d8-d877-45eb-95bc-4e4b8193908e.png)

<br>

JPA 예시코드를 아래로 참고하겠습니다.

SQL

```sql
insert into question (subject, content) values ('안녕하세요', '가입 인사드립니다 ^^');
insert into question (subject, content) values ('질문 있습니다', 'ORM이 궁금합니다');
```

JPA

```java
Question q1 = new Question();
q1.setSubject("안녕하세요");
q1.setContent("가입 인사드립니다 ^^");
this.questionRepository.save(q1);

Question q2 = new Question();
q2.setSubject("질문 있습니다");
q2.setContent("ORM이 궁금합니다");
this.questionRepository.save(q2);
```

위 두 코드는 동일한 역할을 수행합니다.

이렇게만 보면 SQL문이 짧아보일 수는 있지만 위가 동일한 역할을 한다고만 이해하고 넘어갑시다 !

여기서 question은 클래스이며 이를 이용해 q1 이라는 객체를 생성하여 원하는 value 값을 넣을 수 있습니다. 이처럼 데이터관리에 사용되는 ORM클래스를 엔티티라고 합니다. 이렇게 사용하면 내부에서 SQL 쿼리를 자동으로 생성해주므로 SQL문을 직접 작성하지 않고 자바코드로만 데이터베이스에 값을 넣고 가져올 수 있다는 장점이 있습니다.

그리고 이는 유지보수가 편리하다는 장점이 있습니다. SQL쿼리 또한 개발자가 직접 작성하지 않고 자동으로 동일하게 생성해주므로 이로인해 발생되는 오류를 줄일 수 있습니다.

<br>

JPA는 인터페이스 입니다. 즉 구현체가 없으므로 실제 클래스가 필요합니다. SBB에서는 하이버네이트라는 구현체를 사용하였습니다.

**Spring data jpa**

Spring framework에서 **JPA를 편리하게 사용할 수 있도록 지원하는 프로젝트(모듈)** 이다. Spring Data JPA의 목적은 JPA를 사용할 때 필수적으로 생성해야하나, 예상가능하고 반복적인 코드들을 대신 작성해줘서 코드를 줄여주는 것이다. 이는 JPA를 한 단계 추상화시킨 **Repository**라는 인터페이스를 제공함으로써 이루어진다.

Spring Data JPA는 JPA Provider이 아니다. 단지데이터 계층에 접근하기위해 필요한 뻔한 코드들의 사용을 줄여주도록 하는 인터페이스이다. 여기서 반드시 기억해야할 점은 **Spring Data JPA는 항상 하이버네이트와 같은 JPA provider가 필요하다** 는 것이다.

<br>

![Application](https://user-images.githubusercontent.com/109144975/198022047-65f46c72-4472-4516-b243-d03d53ce106c.png)

Spring Data Jpa 예제 코드

<br>

entity 생성

```java
@Entity
public class Product extends Timestamped {
    @GeneratedValue(strategy = GenerationType.AUTO)
    @Id
    private Long id;
    private Long userId;
    private String title;
    private String image;
    private String link;
    private int lprice;
    private int myprice;
}
```
<br>

spring data jpa)Repository 생성

```java
public interface ProductRepository extends JpaRepository<Product, Long> {
}
```

<br>

spring data jpa) repository 기본 제공 기능

```java
// 1. 상품 생성
Product product = new Product(...);
productRepository.save(product);

// 2. 상품 전체 조회
List<Product> products = productRepository.findAll();

// 3. 상품 전체 개수 조회
long count = productRepository.count();

// 4. 상품 삭제
productRepository.delete(product);
```
<br>

spring data jpa) 추가기능 - interface만 선언해주면, 구현은 spring data jpa 가 대신한다.

```java
public interface ProductRepository extends JpaRepository<Product, Long> {
  // (1) 회원 ID 로 등록된 상품들 조회
  List<Product> findAllByUserId(Long userId); /**구현없이 선언만 해주어도 됨**/

  // (2) 상품명이 title 인 관심상품 1개 조회
  Product findByTitle(String title);

  // (3) 상품명에 word 가 포함된 모든 상품들 조회
  List<Product> findAllByTitleContaining(String word);

  // (4) 최저가가 fromPrice ~ toPrice 인 모든 상품들을 조회
  List<Product> findAllByLpriceBetween(int fromPrice, int toPrice);
}
```

![Untitled](https://user-images.githubusercontent.com/109144975/198022069-c5177e2f-b806-4f3e-8459-62b2270bd50f.png)

<br>

## Entity

아래 예시코드로 확인해보겠습니다.

```java
package com.mysite.sbb;

import java.time.LocalDateTime;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

import lombok.Getter;
import lombok.Setter;

@Getter
@Setter
@Entity
public class Question {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer id;

    @Column(length = 200)
    private String subject;

    @Column(columnDefinition = "TEXT")
    private String content;

    private LocalDateTime createDate;
}
```

어노태이션에 대한 정보

**@Entity(이를 적용해야 아래 클래스를 JPA가 엔티티로 인식함)**

- 엔티티 클래스
- 클래스를 테이블과 매핑

**@Table(생략가능)**

- 매핑할 테이블 정보
- name 속성에 테이블 이름 명시 (ex. @Table(name="MEMBER"))
- 생략할 경우 엔티티 클래스 이름으로 매핑(위의 경우 Question이므로 Question 테이블 생성)

**@Id**

- 클래스의 식별자 필드를 테이블의 PK(primary key)에 매핑
- 고유 번호 id 속성에 적용한 @Id 애너테이션은 id 속성을 기본 키로 지정한다. 기본 키로 지정하면 이제 id 속성의 값은 데이터베이스에 저장할 때 동일한 값으로 저장할 수 없다.

**@Column**

- 클래스의 필드를 테이블의 컬럼에 매핑
- 엔티티의 속성은 테이블의 컬럼명과 일치하는데 컬럼의 세부 설정을 위해 @Column 애너테이션을 사용한다.

엔티티란? (토비스프링 참고)

데이터 베이스의 개념 중에서도 데이터 모델에 대해 공부를 시작할 때 제일 먼저 나오는 개념이 '엔터티(Entity)' 이다. 엔티티는 쉽게 말해 개념 정도라고 생각할 수 있다. 일반적으로 엔티티를 정의하는 개념들을 정리하여 나타내면 다음과 같이 볼 수 있다.

모델의 구성요소

- 엔터티는 사람, 장소, 물건, 사건, 개념 등과 같은 명사에 해당된다.

- 엔터티는 업무상 관리가 필요한 것에 해당된다.

- 엔터티는 저장 되기 위한 어떤 것(Thing)에 해당된다.

예를 들어 학교라는 곳에선 과목이라는 엔터티가 존재할 수 있다.그리고 엔터티는 인스턴스의 집합으로 나타나게 된다. 즉 과목이라는 엔터티가 있다면, 수학, 영어, 국어와 같은 인스턴스가 과목이라는 엔터티에 포함되는 것이다. 이때 엔터티는 자신이 가지고 있는 인스턴스를 설명할 수 있는, 나타낼 수 있는 속성(Attribute)를 가지게 된다. 앞에서 이야기한 수학, 영어, 국어와 같은 인스턴스가 존재한다면 이들은 과목이라는 엔터티에서 이름이라는 속성을 가지고 있는 것이죠. 속성에 대해서는 엔터티를 알아본 후에 보다 자세히 알아보자.

엔티티 요약

- 서로 연관된 데이터의 집합을 의미합니다. (테이블과는 조금 다른 개념임)
- 저장되고, 관리가 되어야하는 데이터 입니다.
- 개념, 장소, 사건등을 의미합니다.
- 유형, 무형의 대상을 의미합니다.

엔티티의 특징

1. 반드시 엔티티가 사용되는 곳의 업무에서 필요하고 관리하고자 하는 정보여야 한다.
2. 엔티티가 포함하는 인스턴스에 대해 유일한 식별자로 식별 가능해야 한다.
3. 지속적으로 존재하는 두 개 이상의 인스턴스들의 조합이어야 한다
4. 반드시 속성을 지녀야 한다.
5. 업무 프로세스에 의해 이용되어야 한다.
6. 타 엔티티와 최소 한 개 이상의 관계가 있어야 한다. [두개 이상의 엔티티를 사용하는 경우 무조건 관계를 가져야 한다.]

<br>

### 엔티티의 분류

**실체유형에 따른 분류**

- 유형 엔티티 (Tangible Entity) : 물리적인 형태가 존재하는 엔티티로 안정적이고 지속적으로 활용되는 엔티티.

  > 예시 : 학생, 교수, 물품, 사원 등

- 개념 엔티티 (Conceptual Entity) : 물리적인 형태는 존재하지 않고 관리해야 할 개념적인 정보로 구분되는 엔티티.

  > 예시 : 조직 등

- 사건 엔티티 (Event Entity) : 업무를 수행함에 따라 생성되는 엔티티.

  > 예시 : 주문, 주문취소, 조회수 등


**발생 시점에 따른 분류**

- 기본, 키 엔티티 (Fundamental, Key Entity) : 해당 업무에 원래 존재하는 엔티티. 다른 엔티티와의 관계에 의해 발생되지 않고 독립적으로 존재하며 다른 엔티티의 부모 역할을 함.

  > 예시 : 고객, 상품 등

- 중심 엔티티 (Main Entity) : 업무의 중심적인 역할을 하는 엔티티. 기본 엔티티로부터 생성되며 일반적으로 데이터양이 많고 다른 엔티티와의 관계를 통해 행위 엔티티를 생성함.

  > 예시 : 주문, 취소, 체결 등

- 행위 엔티티 (Active Entity) : 주로 두 개 이상의 부모 엔티티로부터 발생되는 엔티티. 엔티티의 내용이 자주 바뀌거나 데이터의 양이 증감함.

  > 예시 : 주문 목록, 취소 사유, 사원 변경 이력 등


**이제 작성한 엔티티 클래스를 다시 확인해봅시다.**

<br>

엔티티 관련 문제

다음 중 아래 시나리오에서 엔터티로 적합한 것은? S병원은 여러 명의 환자가 존재하고 각 환자에 대한 이름, 주소 등을 관리해야 한다.(단, 업무 범위와 데이터의 특성은 상기 시나리오에 기술되어 있는 사항만을 근거하여 판단해야 한다.)

⑴ 병원

⑵ 환자

⑶ 이름

⑷ 주소

- 답

  2번.

  병원은 S병원 1개만 존재하므로

<br>

### 속성(Attribute)

속성(Attribute)이란?

- 어떤 사물의 성질이나 특징
- 인스턴스로 관리하고자 하는 의미로 더이상 분리되지 않는 최소의 데이터 단위
- 엔티티를 설명하는 요소, 인스턴스를 구성하는 요소

속성의 특징

엔터티와 마찬가지로 반드시 해당 업무에서 필요하고 관리하고자 하는 정보이어야 한다.- 정규화 이론에 근간하여 정해진 주 식별자에 함수적 종속성을 가져야 한다.쉽게 말해, 다양하게 존재하는 인스턴스들에 대해 유일하게 구별할 수 있는 주식별자를 통해서 식별될 수 있어야 한다.- 하나의 속성에는 단 한개의 값만을 가진다.

그렇다면 엔티티, 인스턴스, 속성, 속성값들의 서로 관계는?

한 개의 엔터티는 두 개 이상의 인스턴스(q1, q2)의 집합이다.

한 개의 엔터티는 두 개 이상의 속성을 가진다.

한 개의 속성은 한 개의 속성 값을 가진다.

<br>

**엔티티 구성방식에 따른 분류**

유일성, 최소성(최소한의 컬럼으로 구별을 해야하는 것)

후보키 중 하나가 PK

PK(Primary Key) 속성 - 개념

엔터티를 유일하게 구분할 수 있는 속성을 PK 속성이라고 한다. (이름, 학번을 묶어서 PK 집합을 만들 수 있음)

FK(Foreign Key)속성 - (다른 테이블과의 관계성을 묶어주는 것)

다른 엔터티와의 관계에 있어서 포함된 속성을 FK 속성이라고 한다.

일반 속성

엔터티에 포함되어 있고, PK 또는 FK에 포함되지 않는 속성을 일반 속성이라고 한다.

속성 관련 문제

1. 다음 중 속성에 대한 설명으로 가장 부적절한 것은?

⑴ 엔터티에 대한 자세하고 구체적인 정보를 나타낸다.

⑵ 하나의 엔터티는 두 개 이상의 속성을 갖는다.

⑶ 하나의 인스턴스에서 각각의 속성은 하나 이상의 속성값을 가질 수 있다.

⑷ 속성도 집합이다.

- 답

  3번.

  속성은 하나의 인스턴스에서 단 한개의 속성값만 가질 수 있다.

<br>

# 컨트롤러

컨트롤러란 무엇인가 ?

컨트롤러란 서버의 첫 진입점이며 사용자의 요청을 받아 처리를 결정한 후 지정된 뷰에 모델 객체를 넘겨주는 역할을 합니다.

![Untitled](https://user-images.githubusercontent.com/109144975/198022100-8c78baa2-ded5-485a-aff3-f362dfdd96f9.png)

즉 최초 진입 지점이며 사용자의 요청에 따라 어떤 처리를 할지 결정을 Service에 넘겨줍니다. 그 후 Service에서 실질적으로 처리한 내용을 받아 View로 넘겨줍니다.

<br>

컨트롤러를 사용하는 이유가 뭘까요 ?

만약 대규모 서비스를 구현한다면 A서비스, B서비스, C서비스 등등 있다고 하겠습니다. 그러면 이 많은 종류의 서비스를 한 클래스를 만들어서 꽉꽉 몰아 처리할 게 아니라 Controller라는 중간 제어자를 만들어서 A서비스에 대한것은 A-Controller가 맡고 B서비스는 B-Controller 이런식으로 **역할**
에 따라 설계를 하고 코딩을하면 개발비용이나 유지보수비용이 대폭 줄어들기 때문에 Controller를 사용한다고 합니다

<br>

컨트롤러는 MVC 세가지 컴포넌트 중에서 가장 많은 책임을 지고 있습니다. 서블릿이 넘겨주는 HTTP 요청을 파악하려면 클라이언트 호스트, 포트, URI, 쿼리스트링, 폼 파라미터, 쿠키, 세션 등을 매우 다양한 정보를 참고해야합니다. 이러한 정보를 파악한 뒤 서비스계층의 메소드를 불러서 요청에 따른 작업을 수행할 수 있습니다. 이 과정에서 컨트롤러의 역할은 서비스계층의 메소드를 선정하는 것과 적절한 파라미터 타입에 맞게 변환해주는 것입니다.

<br>

이후 컨트롤러는 서비스 계층의 메소드가 돌려준 결과에 따라 어떤 뷰를 보여줘야 하는지 결정해야합니다.  때로는 페이지가 바뀌도록 리다이렉트해줘야 합니다. 이 경우 적절한 URL을 만들어줘야 합니다.

<br>

Controller 관련 대표적인 어노테이션

@Controller

> 내가 컨트롤러다 ! 를 명시하는 것  
필요한 비즈니스 로직을 호출하여 전달할 모델과 이동할 뷰 정보를 서브렛에 반환


@RequestMapping

> 요청에 대해 어떤 메소드로 처리할지에 대한 어노테이션  
> URL을 명시하여 함께 사용함

RequestMapping 속성

value

```java
@RequestMapping("/login")
```

method(get, post, head, put 등등): HTTP 메소드 값

```java
// Spring4.3 이후 ex1), ex2)는 다음과 같이 쓸수 있다.
@GetMapping("/login")
  == @RequestMapping("/login", method=@RequestMethod.GET) // url에 붙여서 전송
@PostMapping("/login")
   == @RequestMapping("/login", method=@RequestMethod.POST) // html body안에 전송
```

params(string[]): HTTP 파라미터

```java
@PostMapping("/member")
public String member(String name, Int age)
```

Post(Question)Controller 예시코드를 보겠다.

```java
/** 게시물리스트 컨트롤러*/
@RequiredArgsConstructor
@Controller
public class PostController {

    private final PostService postService;

    @RequestMapping("/post/list")
    public String list(Model model) {
        List<Post> postList = this.postService.getList();
        model.addAttribute("postList", postList);
        return "post_list";
    }

    @RequestMapping(value= "/post/detail/{id}")
    public String detail(Model model, @PathVariable("id") Integer id) {
        return "post_detail";
    }
}
```

<br>

## SOLID에 대해

- 객체지향 SOLID 원칙

SOLID란?

SRP(단일 책임 원칙) : 어떤 클래스를 변경해야 하는 이유는 오직 하나뿐이어야 한다.

OCP(개방 폐쇄 원칙): 자신의 확장에는 열려있고, 주변의 변화에 대해서는 닫혀있어야 한다.

LSP(리스코프 치환 원칙): 서브 타입은 언제나 자신의 기반 타입으로 교체할 수 있어야 한다.

ISP(인터페이스 분리 원칙): 클라이언트는 자신이 사용하지 않는 메서드에 의존관계를 맺으면 안된다.

DIP(의존 역전 원칙): 자신보다 변하기 쉬운 것에 의존하지 마라.

SOLID는 객체 지향을 올바르게 프로그램에 녹여내기 위한 원칙이다. SOLID는 갑자기 하늘에서 떨어진 것이 아니라 객체 지향 4대 특성(캡상추다)를 제대로 활용한 결과로 당연히 나타나는 것이다.(실제로 원칙들이 연관관계가 있는 것 같습니다 !)


