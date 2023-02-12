# DBMS (데이터베이스)

- 데이터베이스에 대한 개념을 정리하였습니다.

- 학습 내용은 T 아카데미의 [데이터 베이스 강좌](https://tacademy.skplanet.com/live/player/onlineLectureDetail.action?seq=72)를 참고하였습니다.

---

## DBMS 기초

<br>

**DataBase Management System**

> - 데이터베이스(DB)를 관리하는(Management) 시스템(System)
>   - DB : 테이블들이 모여 이루는 데이터 단위
> - 데이터를 저장하고 유지보수(수정, 삭제, 추가)하고 이를 검색하는 시스템
>   - CRUD(Create, Retrieve, Update, Delete)
> - 대량의 데이터를 처리하는 시스템
> - 다양한 자료구조와 검색구조(소팅, 인덱싱, ...) 사용해 **빠른** 검색 가능
> - 대부분의 시스템은 R(검색)>>>>> CUD(업데이트)의 빈도수가 많음
>   - 하지만 만약 CUD도 빈도가 많을 경우 NOSQL을 사용할 수 있음
> - 검색에 최적화

<br>



**정렬**

> - 빠른 검색을 위해서는 - 데이터는 반드시 **정렬(Sorting)되어 있어야 함**
> - 정렬 되어 있지 않다면(Pile) 평균적으로 전체 데이터의 절반 필요
> - 정렬되어 있을 경우 데이터를 빠른 시간 안에 찾을 수 있음
>   - O(NlogN), O(N^2)
> - 퀵정렬/힙정렬 계열이 주로 사용됨

<br>


**인덱스(Index)**

- 인덱스 종류
  - 이진검색(Binary Search)
    - 최대 log2(N)번 내에 검색 가능
  - B-Tree 계열
    - 최대 log3(N) 번 내에 검색 가능
    - 상용 DBMS에서 가장 일반적으로 많이 사용됨

`데이터 추가/ 수정 / 삭제 할 때마다 정렬/인덱스 업데이트가 일어남`

<br>


**이진탐색(Binary Search)**

- 데이터를 정렬 후 "test" 단어를 검색하는 경우
  - 한가운데 값을 확인 - sample - 뒤쪽 절반 (t 가 s 보다 뒤에 있으므로)
  - 뒤쪽 중 한가운데 확인 - zeal - 앞쪽 절반 (t 가 z 보다 앞에 있으므로)
  - 위를 계속 반복 "test" 단어가 나올 때 까지 반복
  - > 데이터가 1000개 있을 경우 10번만 찾으면 데이터를 찾을 수 있는 것이 이론적으로 보장됨(2^n > 1000 이므로, n=10)
  - 데이터가 추가/삭제/변경될 때 마다 한 가운데/왼쪽 가운데/오른쪽 가운데 값들을 미리 계산해 놓음
    - 이를 **인덱스(INDEX)** 라고 통칭함

<br>


**B-트리**

- 이진 검색과 유사하지만 한 번에 비교를 2번 (a, b: a<b)
  - 작은 값 보다 작은경우 (x<a)
  - 큰 값과 작은 값 사이인 경우 (a<x<b)
  - 큰 값보다 큰 경우 (x>b)
- B-트리 계열 > 이진 검색 계열
  - O(log3N) > O(log2N) - 즉 n^3 이 n^2 보다 빨리 증가함
- 데이터가 추가/삭제/변경 될 때마다 a, b 값을 업데이트

<br>


**DBMS의 종류**

- 계층형 데이터베이스
- 네트워크형 데이터베이스
- 관계형 데이터베이스
- 객체지향 데이터베이스
- 객체관계형 데이터베이스(ORDBMS)
- NoSQL(Not Only SQL)

<br>


**RDBMS란 ?**

- 관계형(Relational) 데이터베이스 시스템
- 테이블(Table based)기반의 DBMS
  - 테이블-컬럼 형태의 데이터 저장 방식
  - 테이블과 테이블 간의 연관관계(주로 외래키형태)를 이용해 필요한 정보를 구하는 방식
- 모델링은 E-R(Entity Relationaship) 모델을 사용
- 테이블을 엔티티(기본)와 릴레이션십(유도) 테이블로 구분하는 방식
- 데이터를 테이블(Table)단위로 관리
  - 하나의 테이블은 여러 개의 컬럼으로 구성됨
- **테이블끼리의 중복정보는 최소화 시킴**
  - 동일한 데이터가 여러군데 중복되어 존재하면 데이터의 수정시 문제 발생확률 높아짐
  - 정규화(Normalize) - 정규형 (1, 2, 3)
- 사용방식
  - 여러 테이블을 합쳐 큰 테이블을 생성(조인 JOIN)해서 필요한 정보를 찾아내는 방식

<br>


**기본용어**

스키마(Schema)
- DB, 테이블 정의 내역

SQL쿼리
- 관계형 DBMS를 사용하는 전용 질의 언어
- 대소문자 가리지 않음 / Interpreter 언어

기본키(Primary Key : PK)
- 테이블에서 하나의 레코드를 지정할 수 있는 하나 이상의 컬럼집합
- 예) 주민등록번호, SSN(Social Security Number)

외래키(Foreign Key : FK)
- 어떤 테이블의 기본키가 다른 테이블의 컬럼에 들어 있는 경우

테이블
- 정보들의 묶음 단위
- 예) 학교, 학생, 교수 ...

컬럼
- 테이블을 구성하는 정보들
- 예) 학생테이블-이름, 주소, 전화번호, 나이, 성별 ...

레코드
- 테이블에 들어있는 여러가지 인스턴스 하나하나를 지정
- 예) name:홍길동, 주소:서울 노원구, 전화번호:111, 나이:28, ...
- 대학교의 학과 테이블일 경우 과 하나하나가 레코드가 될 수 있음
- 예) 경영학과, 미술학과, 수학과, 컴퓨터공학과 ...
- 기본키(PK)로 구별가능

도메인 값(Domain Value)
- 각 컬럼에서 나올 수 있는 후보 값

**정리**

DBMS(Database Management System)
- 데이터를 CRUD(생성, 수정, 삭제, 검색)하는 시스템
- 검색에 최적화(인덱스)
- 업데이트가 많을 경우 대안이 필요 - NoSQL

RDBMS(Relational DBMS)
- 테이블 형태로 관리되는 DBMS의 한 형태
- SQL이라는 질의 언어를 사용

**기본 DBMS 사용법**

MySQL 기본 사용법

로그인 후 sql 프롬프트 상에서
- show databases; DB들의 리스트를 표시하라
- use world; WORLD DB를 사용한다
- show tables; WORLD DB의 테이블 리스트를 표시하라
- desc city; city 테이블의 구조를 표시달라
- select * from city; city 테이블의 내용을 표시하라

<br>

------------------



<br>

## SQL의 DML-1

SQL의 이해

**SQL (Structured Query Language)**

- 데이터베이스에 있는 필요한 정보를 사용할 수 있도록 도와주는 언어
- 사용방법이나 문법이 다른 언어(Java, C, C# 등) 보다 단순하다
- 하나를 배워두면 모든 DBMS에서 사용가능하다
- 인터프리터
- 대소문자 구별하지 않음 (데이터 내용은 구별함)

**DML (Data Manipulation Language)**

- 테이블의 데이터를 조작하는 기능
- 테이블의 레코드를 CRUD(Create, Retrieve, Update, Delete)

INSERT : 데이터베이스 객체에 데이터를 입력한다.
DELETE : 데이터베이스 객체에 데이터를 삭제한다.
UPDATE : 데이터베이스 객체 안의 데이터를 수정한다.
SELECT : 데이터베이스 객체 안의 데이터를 조회한다.

**DDL (Data Definition Language)**

- DB, 테이블의 스키마를 정의, 수정하는 기능
- 테이블 생성, 컬럼 추가, 타입 변경, 각종 제약조건 지정, 수정 등

CREATE : 데이터베이스 객체를 생성한다.
DROP : 데이터베이스 객체를 삭제한다.
ALTER : 기존에 존재하는 데이터베이스 객체를 다시 정의한다.

**DCL (Data Control Language)**

- DB나 테이블의 접근권한이나 CRUD 권한을 정의하는 기능
- 특정 사용자에게 테이블의 조회권한 허가/금지 등

GRANT : 데이터베이스 객체에 권한을 부여한다.
REVOKE : 이미 부여된 데이터베이스 객체 권한을 취소한다.

<br>


**CRUD (Create, Retrieve, Update, Delete)**

> Create : 데이터베이스 객체 생성
INSERT INTO
새로운 레코드를 추가

> Update : 데이터베이스 객체 안의 데이터 수정
> UPDATE
> 특정 조건의 레코드들의 컬럼값을 수정

> Delete : 데이터베이스 객체의 데이터 삭제
> DELETE
> 특정 조건의 레코드들을 삭제

> Retrieve(Search) : 데이터베이스 객체 안의 데이터 검색
> SELECT
> 조건을 만족하는 레코드들을 찾아 특정 컬럼 값(모두의 경우 *)을 표시

<br>


**SELECT 문**

SELECT 컬럼명 FROM 테이블명 WHERE 조건절;

select * from city;

질의문
- 국가 코드가 'KOR'로 되어 있는 도시의 '이름'을 구하시오
- 인구가 500만 이상인 도시들의 '이름'

SQL
```sql
select Name from city where CountryCOde='KOR';
select Name from city where Population > 5000000;
```

**INSERT 문**

INSERT INTO 테이블명(컬럼명) VALUES (값);

```sql
insert into city(ID, Name, CountryCode, District, Population) values
(10000, 'sample', 'KOR', 'Test', 1000000);
```

만약 모든 컬럼값들이 위치에 맞게 지정될 경우 컬럼명 생략이 가능 
```sql
insert into city values(200000, 'SampleTest', 'KOR', 'Test', 2000000);
```


**UPDATE 문**

UPDATE 테이블명 SET 컬럼명=값, .. WHERE 조건절;
```sql
update city set name='SampleRevised' where id=10000;
```

>주의할 점 : 만약 UPDATE 시 where에 매칭되는 조건이 여러개일 경우 해당되는 모든 레코드(객체)가 영향을 받게 된다.
그래서 반드시 하나의 레코드 혹은 원하는 레코드를 확인하여 사용해야 한다.


**DELETE 문**

DELETE FROM 테이블명 WHERE 조건절;
```sql
delete from city where ID = 10000;
```

**정리**

DML (DAta Manipulatino Language)
SQL 종류의 하나로, 데이터의 삽입(INSERT), 삭제(DELETE), 갱신(UPDATE) 등을 처리함

CRUD (Create, Retrieve, Update, Delete)
기본적인 데이터 처리 기능은 CRUD 를 묶어서 하는 말

SELECT 컬럼명 FROM 테이블명 WHERE 조건절;
INSERT INTO 테이블명 (컬럼명) VALUES (값);
UPDATE 테이블명 SET 컬럼명='값' WHERE 조건절;
DELETE FROM 테이블명 WHERE 조건절;

<br>

-------------

<br>

## SQL의 DML-2

**DISTINCT**
- select 문의 결과값에서 특정 컬럼만 출력할 경우 중복된 값들이 나오는 경우에 이를 제거해서 표시하는 기능
- select distinct 컬럼명1, 컬럼명2, ... from 테이블 명

국가코드가 'KOR'인 도시들의 국가코드를 중복 제거해서 표시하시오.

- 70개의 'KOR'인 도시들이 있다면 70개의 동일한 정보인 KOR row(행)가 출력됨, 따라서 아래와 같이 중복을 없애고 출력을 해야함 

```sql
select distinct CountryCode from city where CountryCode='KOR';
```

<br>


**논리연산자 AND, OR, NOT**
- SELECT문의 조건절에 논리 조건 적용해서 적용할 수 있는 연산자
- select * from 테이블명 where (not) 조건1 and/or (not) 조건2 ...

국가코드가 'KOR'이면서 인구가 100만 이상인 도시를 찾으시오.
국가코드가 'KOR', 'CHN', 'JPN'인 도시를 찾으시오.
국가코드가 'KOR'이 아니면서 인구가 100만 이상인 도시를 찾으시오.

```sql
select * from city where CoutnryCode='KOR' and population > 1000000;
select * from city where CountryCode='KOR' or CountryCode = 'CHN' or CountryCode = 'JPN';
select * from city where CountryCode!= 'KOR' and population > 1000000;
```


<br>


**논리연산자 IN, BETWEEN**
- 영어로 표현하는 것이 가능

city 테이블에서

국가코드가 'KOR', 'CHN', 'JPN'인 도시를 찾으시오.
국가코드가 'KOR'이고 인구가 100만 이상 500만 이하인 도시를 찾으시오.

아래 두 코드는 동일한 결과

```sql
select * from city where CountryCode in ('KOR', 'CHN', 'JPN');
select * from city where CountryCode='KOR' or CountryCode = 'CHN' or CountryCode = 'JPN';
```

아래 두 코드는 동일한 결과

```sql
select * from city where CountryCode = 'KOR' and (Population between 1000000 and 5000000);
select * from city where CountryCode = 'KOR' and (Population >= 1000000 and Population <= 5000000);
```

국가코드가 'KOR' 혹은 'ESP' 혹은 'USA' 혹은 'SVK' 이고 인구수가 1000000 에서 3000000 사이인 레코드를 city 테이블에서 찾으시오.

```sql
select * from city where CountryCode in ('KOR', 'ESP', 'USA', 'SVK') and Population between 1000000 and 3000000;
```

<br>


**결과정렬 ORDER BY**
- SELECT 문의 결과값을 특정한 컬럼을 기준으로 오름차순/내림차순으로 정렬해서 표시
- select * from 테이블명 where 조건절 order by 컬럼명 asc(오름차순)/desc(내림차순), ...
- 기본값은 오름차순 정렬임(asc는 생략 가능)/여러 개의 컬럼을 나열하면 순서대로 정렬

국가코드가 'KOR'인 도시를 찾아 인구수의 역순으로 표시하시오.

```sql
select * from city where CountryCode = 'KOR' order by Population desc;
```

city 테이블에서 국가코드와 인구수를 출력하라. 정렬은 국가코드별로 오름차순으로, 동일한 코드(국가) 안에서는 인구 수의 역순으로 표시하시오.

```sql
select CountryCode, Population from city order by CountryCode (asc 생략가능), Population desc;
```

<br>


**정리**

중복성 제거 (distinct)
- 결과값이 특정컬럼이 중복되어 표현될 때 동일한 값은 한 번만 표시

논리 연산자 (and, or, not, in, between)
- 조건절의 조건식을 논리식으로 표현하는 방법 제공

결과값 정렬 (order by)
- 결과값을 특정 컬럼을 기준으로 오름차순(asc)/ 내림차순(desc) 정렬해서 표현
- 여러 개의 경우 컬럼 나열된 순서로 적용 (1차정렬, 2차 정렬, ...)


## SQL의 DML-3

결과값 일부 조회 LIMIT
- SQL 쿼리 결과 중 상위 몇 개만 보여주는 쿼리
- select 컬럼명1, 컬럼명2, .. from 테이블명 where 조건절 limit 숫자
- 대ㅛ적인 비 표준기능 (DBMS 종류마다 다름)

국가코드가 'KOR'인 도시들중 인구수 많은 순서로 상위 10개만 표시하시오

```sql
select * from city where CountryCode = 'KOR' order by Population desc limit 10;
```

<br>


**집합함수**
- 테이블의 전체 레코드를 대상으로 특정 컬럼을 적용해서 한 개의 값을 리턴하는 함수
- count(), avg(), sum(), min(), max() ...

count() - 레코드의 개수를 리턴하는 함수

sum(), avg() - 컬럼값의 합/평균을 리턴

min(), max() - 컬럼값의 최소/최대값을 리턴

city 테이블에서 국가코드가 'KOR'인 도시의 수를 표시하시오.

city 테이블에서 국가코드가 'KOR'인 도시들의 인구수 총합/평균을 구하시오.

city 테이블에서 국가코드가 'KOR'인 도시들의 인구수 중 최대값/최소값을 구하시오.

```sql
select count(*) from city where CountryCode = 'KOR';
select sum(Population) from city where CountryCode = 'KOR';
select avg(Population) from city where CountryCode = 'KOR';
select min(Population) from city where CountryCode = 'KOR';
select max(Population) from city where CountryCode = 'KOR';
```


<br>

**유용한 함수**
LENGTH() - 레코드의 문자열 컬럼의 글자수를 리턴한다.

MID() - 문자열의 중간부분을 리턴한다.

UPPER()/LOWER() - 문자열을 대문자/소문자로 리턴한다.

ROUND() - 레코드의 숫자컬럼값을 반올림해서 리턴한다.


country 테이블의 나라명을 앞 세글자만 대문자로 표시하시오.
```sql
select upper(mid(Name, 1, 3)) from country;
```

<br>


**정리**

- 결과값 일부 조회 (LIMIT)
- 집합함수 (Count, min, max, sum, avt)
- 유용한 함수 (round, mid(substring), length, upper)


## SQL의 DML-4

<br>


**JOIN의 개념**

- 서로 다른 테이블을 공통 컬럼을 기준으로 합치는(결합하는) 테이블 단위 연산
- 조인의 결과 테이블은 이전 테이블의 컬럼 수의 합과 같다.
- **select * from 테이블 1 join 테이블 2 on 테이블1. 컬럼명 = 테이블2.컬럼명 ...**
- 조인시 서로 다른 테이블에 같은 컬럼명이 존재하면 구분을 위해 테이블명.컬럼명으로 사용해서 표시
- A join B 를 하게되면 A 테이블을 기준으로 join 하는 것


city 테이블과 country테이블을 조인하시오
(city.CountryCode = country.Code)

```sql
select * from city join country on city.CountryCode = country.Code;
```


국가코드와 해당 나라의 GNP를 표시하시오

```sql
select city.CountryCode, country.GNP from city join country on city.CountryCode = country.Code;
```

<br>



**JOIN의 종류**
- 조인시 NULL 값을 허용하는 내부조인(불가)과 외부조인(허용)으로 구분
- 내부 : INNER JOIN 외부 : LEFT JOIN / RIGHT JOIN / FULL JOIN

INNER : 조인시 NULL 값을 허용하지 않음 (NULL 값을 가진 레코드는 조인결과에 빠짐)

`A JOIN B`

- LEFT JOIN : 조인시 JOIN의 왼쪽 테이블(A)의 NULL값을 포함해서 표시
- RIGHT JOIN : 조인시 JOIN의 오른쪽 테이블(B)의 NULL값을 포함해서 표시
- FULL JOIN : MYSQL 지원 안함

city 테이블에 국가코드가 없는 도시가 있는지 확인해보시오.

country 테이블에는 존재하지만 도시가 하나도 없는 나라가 있는지 확인하시오.

이때 INNER JOIN / LEFT JOIN / RIGHT JOIN 의 차이점으로 확인하시오.

```sql
select count(*) from city where CountryCode is NULL;
select count(*) from city left join country on city.CountryCode = country.Code; (country 값이 존재하지 않는 city 포함)
select count(*) from city right join country on city.CountryCode = country.Code; (country 중 도시 수가 하나도 없는 country는 포함)
```

아래 그림에서 볼 수 있듯

- city 테이블에는 존재하지만 country가 없는 나라 즉 **도시에는 속하지만 country는 NULL 값인 레코드는 0개 인것을 알 수 있지만**
- country 테이블에는 존재하지만 도시가 하나도 없는 나라 즉 **소속국가가 없는 도시는 7개(4079 - 4086)가 있다**

![](https://user-images.githubusercontent.com/109144975/218303521-ff06ad54-c597-4f06-b13b-5d663f7cb051.png)

<br>


**별명(ALIAS)**
- SQL쿼리 결과 생성시 컬럼명에 대한 별명을 사용해 표시하는 기능
- SELECT 테이블명1.컬럼명 AS 별명1, 테이블명2.컬럼명2 AS 별명2 FROM ...
- 조인할 때 많이 사용됨

city 테이블과 country 테이블을 조인해서 국가코드가 'KOR'인 나라의 축양표시명과 정식명을 표시하시오

```sql
select distinct city.countryCode as Abbr, country.Name as FullName from city join country on city.CountryCode = country.Code where city.countryCode = 'KOR';
```

<br>


**정리**

- JOIN : 서로 다른 두 테이블을 원하는 공통 컬럼으로 합쳐서 큰 테이블을 생성하는 연산  
  - INNER JOIN(모든 null은 누락) / LEFT JOIN / RIGHT JOIN / FULL JOIN
  - 각 테이블에 조인 기준컬럼의 NULL 값을 포함여부에 따라 결정 (예 : LEFT JOIN 경우 LEFT 테이블에 NULL값이 있더라도 누락이 되지 않음)
- ALIAS : 쿼리 결과 컬럼명을 다른 이름으로 대체해서 표시 (테이블에 스키마를 노출하고 싶지 않은 경우, 컬럼을 한글로 사용하고 싶은 경우)
- VIEW : 쿼리 결과를 임시테이블에 저장하고 사용 


## SQL의 DML-5

<br>


**SELECT INTO**

select into : select를 하고나서 그 값이 나오는 결과 값을 어떤 테이블에 insert하는 것 = insert into
- 쿼리 결과를 새 테이블로 만든다
- 기존에 존재하지 않는 테이블이 새로 생성된다.
- MySQL에서는 `CREATE TABLE 테이블명 SELECT * FROM 테이블명` 이다.

city 테이블의 내용에서 국가코드가 'KOR'인 도시를 찾아 city_new 테이블에 넣으시오

<br>


**INSERT INTO SELECT**
- 쿼리 결과를 기존의 테이블에 추가한다 (기존 테이블이 존재해야함)
- INSERT INTO 테이블명1 SELECT * FROM 테이블명2 WHERE 조건절...
- SELECT 하는 테이블과 INSERT하는 테이블은 동일한 구조를 가져야 함
- 두 개의 별도 쿼리를 하나로 합침

city 테이블의 내용에서 국가코드가 'KOR'인 도시를 찾아 city_kor 테이블에 넣으시오.

```sql
city 테이블의 스키마를 DDL로 조회 후 새 테이블을 생성
show create table city; 후 city_kor 이름으로 새로 생성
    
insert into city_kor select * from city where CountryCode = 'KOR';
```

![](https://user-images.githubusercontent.com/109144975/218305598-29a1b378-0674-440a-9ea4-43dea293c825.png)

<br>


**CASE .. WHEN .. END**

- SQL 의 조건문(if/switch문) 에 해당
- 조건값에 따른 처리 구분

city 테이블에서 도시명(Name) 이 3자가 넘어가는 경우 앞쪽 세 자만 대문자로 출력, 도시의 인구를 같이 표시하시오.

```sql
이름부분을 처리하는 것임 원래는 select Name, Populatoin from city;
    
select case when length(Name) > 3 then upper(mid(Name, 1, 3))
        when length(Name) <= 3 then upper(Name)
        end, Population from city;
```

<br>


**정리**

- SELECT INTO(CREATE TABLE SELECT * FROM ...)
  - 쿼리문의 결과값을 새로운 테이블을 만들고 레코드를 추가한다
- INSERT INTO SELECT
  - 쿼리문의 결과값을 "기존" 테이블에 레코드로 추가한다.
- CASE WHEN END
  - 조건식에 따른 다른 처리를 할 수 있다.

<br>


## SQL의 DML-6

<br>


**LIKE 검색이란 ?**
- 정확한 키워드를 모를 경우 일부만으로 검색하는 방법
- 와일드카드(%, _)를 사용하여 패턴매칭
  - select 컬럼명 from 테이블명 where 컬럼명 like 패턴
- 와일드카드
  - % : 0-n글자, _ : 1글자
- LIKE 검색은 매치앟기 위해 DBMS에 부담이 많음으로 LIKE에 OR와 같은 논리조건자를 중복해서 사용하지 않는게 좋음
  - (좋지 않은 예)
  - select * from 테이블명 where like 컬럼명1 like ... or 컬럼명2 like ...;

city 테이블에서 국가코드가 k로 시작하는 / 끝나는 / 중간에 들어있는 국가코드를 표시하시오
city 테이블에서 국가코드가 k로 시작하는 3글자 국가코드를 표시하시오.

```sql
select countryCode from city where CountryCode like 'K%';
select countryCode from city where CountryCode like '%K';
select countryCode from city where CountryCode like '%K%';
select countryCode from city where CountryCode like 'K__';
```

주의해야할 패턴

`select * from city where CountryCode like 'KOR%' or district like 'KOR%';`

<br>


**NULL 값**
- NULL이란 해당 컬럼의 값이 없다는 의미(해당 컬럼이 NULL값을 허용하는 경우)
- NULL 값을 가지고 있는 컬럼을 검색하려면 is NULL
- NULL 이 아닌 값을 가지고 있는 컬럼을 검색하려면 is not NULL

country 테이블에서 기대수명 (LifeExpectancy)이 없는 국가개수를 표시하시오.

country 테이블에서 기대수명 (LifeExpectancy)이 있는 국가개수를 표시하시오.

```sql
select count(*) from country where LifeExpectancy is NULL;
select count(*) from country where LifeExpectancy is not NULL;
```

<br>



**NULL 함수**
- 숫자컬럼을 연산해야 할 때 NULL을 처리해주는 함수
- NULL값이 나오면 다른 값(주로 0)으로 대체해서 계산에 문제 없도록 처리 함
- IFNULL / COALESCE(MySQL), ISNULL(SQL Server)
- 숫자연산 / 집합함수 (sum)의 경우 처리가 내장되어 있음
- 직접 함수나 쿼리에 넣는 경우는 NULL 함수를 사용해야 함

country 테이블의 기대수명의 평균값을 표시하시오 (NULL값 미반경 / 반영)
country 테이블의 기대수명값이 들어있는 개수를 표시하시오. (NULL값 미반경 / 반영)

```sql
select avg(LifeExpectancy) from country;
select avg(IFNULL(LifeExpectancy, 0)) from country; NULL값을 0으로 대체 
select count(LifeExpectancy) from country;
select count(IFNULL(LifeExpectancy, 0)) from country;
```

<br>


**GROUP BY / HAVING**
- 집합함수와 같이 사용해 그룹별 연산을 적용한다.
  - select 컬럼명, 집합함수명(컬럼명) from 테이블명 group by 컬럼명;

GROUP BY

city 테이블의 국가코드별 도시 숫자를 구하시오

> 여기서 포인트는 도시 숫자 count(CountryCode)이다. 도시숫자는 동일한 국가코드를 가지고 있으므로 국가코드를 count하게되면 도시 숫자를 알 수 있게 된다.

```sql
select CountryCode, count(CountryCode) from city group by CountryCode;
```

HAVING
- HAVING은 집합연산에 where 조건절 대체로 사용

city 테이블의 국가코드별 도시숫자를 구하시오. (단 70개 이상의 도시를 가지는 국가만 표시하시오.)

```sql
select CountryCode, count(CountryCode) from city group by CountryCode having count(CountryCode) >= 70;
```

<br>


**정리**
- LIKE 검색
  - 패턴을 기반으로 검색하는 기능
  - 와일드카드 %(여러 자 매칭), _(1자 매칭)
- NULL 값
  - 컬럼 값이 존재하지 않을 때 사용
  - 검색시 is NULL / is not NULL
- NULL 함수
  - 숫자 컬럼 연산시 NULL 값 처리 IFNULL()
- GROUP BY
  - 집합함수를 사용해 그룹연산
- HAVING
  - GROUP BY 와 같이 사용해 조건을 적용


<br>

## SQL의 DML-7

<br>

**서브쿼리**
- 쿼리문 내에 또다른 쿼리문이 있는 형태
- 서브쿼리는 메인쿼리에 포함되는 관계
  - ()를 사용해 감싸는 형태
  - ORDER BY를 사용하지 못한다.

사용가능한 위치
- SELECT / FROM / WHERE / HAVING / ORDER BY / VALUES(INSERT) / SET(UPDATE), ...

종류
- 단일행(single row) 서브쿼리
  - 결과가 레코드 하나인 서브쿼리
  - 일반 연산자 (=, >, <, ..)사용
- 다중행(multi row) 서브쿼리
  - 결과가 레코드 여러 개인 서브쿼리
  - 다중행 연산자 (IN, ALL, ANY, EXISTS) 사용
- 다중컬럼(multi column) 서브쿼리
  - 결과가 컬럼 여러 개인 서브쿼리
  - ALL
    - 여러 개의 레코드의 AND효과(가장 큰 값보다 큰)
    - Population > ALL(select Population)
  - ANY
    - 여러 개의 레코드의 OR 효과(가장 작은 값보다 큰)
    - Population > ANY(select Population)
  - IN / EXISTS
    - 결과값 중 있는 것 중에서의 의미
    - IN 은 전체 레코드를 스캔
    - EXISTS는 존재 여부만 확인하고 스캔하지 않음(상대적으로 빠름), 존재하면 TRUE / 존재하지 않으면 FALSE 만 반환


서브쿼리(단일행, 다중행, 다중컬럼)

### 단일행

국가명이 'South Korea'의 국가코드를 찾아 이에 해당되는 도시의 수를 표시하시오

```sql
select count(*) from city where CountryCode = (select Code from country where Name = 'South Korea');
```

city 테이블에서 국가코드가 'KOR'인 도시의 평균 인구 수보다 많은 도시들의 이름과 인구를 표시하시오.

```sql
select Name, Population from city where Population > (select avg(Population) from city where CountryCode = 'KOR') order by Population desc;
```

### 다중행

국가명이 'South Korea', 'China', 'Japan'의 국가코드를 찾아 이에 해당되는 도시의 수를 각각 표시하시오.

```sql
select CountryCode, count(*) from city where CountryCode IN (select Code from country where Name in ('South Korea', 'China', 'Japan')) group by CountryCode;
```

인구가 5,000,000 명이 넘어가는 도시의 이름, 국가코드, 인구 수를 표시하시오

```sql
select Name, CountryCode, Population from city where (Name, CountryCode) IN (select Name, CountryCode from city where Population > 5000000);
```

### 다중컬럼

한국의 모든(ALL) 도시의 인구 수보다 많은 도시를 찾아 표시하시오.

```sql
select Name, CountryCode, Population from city where Population > ALL(select Population from city where CountryCode = 'KOR');
```

한국의 어떤(ANY) 도시의 인구 수보다 많은 도시를 찾아 표시하시오.

```sql
select min(Population) from city where Population > ANY(select Population from city where CountryCode = 'KOR');
```

국가코드가 'KOR', 'CHN', 'JPN' 인 도시명과 국가코드, 인구 수를 출력하시오 (EXISTS)

```sql
select Name, CountryCode, Population from city where exists (select * from country where CountryCode in ('KOR', 'CHN', 'JPN'));
```

해당되는 국가코드에 대해서는 1(True)가 넘어오고 다른 국가코드에 대해서는 0이 넘어옴


**집합연산**
- 각종 집합 연산
- 합집합(UNION), 교집합(INTERSECT), 차집합(MINUS), ...
- MySQL은 INTERSECT / MINUS는 지원하지 않음

city 테이블에서 국가코드가 'KOR', 국가코드가 'CHN'인 도시를 구하시오 (UNION사용)

```sql
select * from city where CountryCode = 'KOR' UNION select * from city where CountryCode = 'CHN';
```

UNION/UNION ALL을 사용해 차이를 확인하시오 (국가코드명을 사용)

- UNION (기본적으로 distinct 적용 됨)

```sql
select CountryCode from city where CountryCode = 'KOR' UNION select CountryCode from city where CountryCode = 'CHN';
```

2개의 row가 출력

- UNION ALL

```sql
select CountryCode from city where CountryCode = 'KOR' UNION ALL select CountryCode from city where CountryCode = 'CHN';
```

433개의 row가 출력

country 테이블에서 기대수명이 80세 이상인 나라와 인구가 100만 이상인 나라를 구하고 공통되는 나라를 표시하시오.

```sql
select Code from Country  where LifeExpectancy >= 80 and Code in (select Code from Country where Population >= 1000000);
```

city 테이블에서 인구가 500만이 넘는 도시의 국가명 (단, 국가코드가 'CHN' 인 도시를 제외) 를 표시

```sql
select distinct CountryCode from city where Population > 5000000 and CountryCode not in (select distinct CountryCode from city where CountryCode = 'CHN');
```

**정리**

서브쿼리 : 쿼리문 내에 다른 쿼리가 내장된 형태
- 단일행, 다중행(IN, ANY, ALL, EXISTS), 다중컬럼

집합연산 : 두개 이상의 쿼리결과에 대한 합집합/교집합/차입합 연산