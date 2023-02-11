# DBMS (데이터베이스)

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

**정리**

중복성 제거 (distinct)
- 결과값이 특정컬럼이 중복되어 표현될 때 동일한 값은 한 번만 표시

논리 연산자 (and, or, not, in, between)
- 조건절의 조건식을 논리식으로 표현하는 방법 제공

결과값 정렬 (order by)
- 결과값을 특정 컬럼을 기준으로 오름차순(asc)/ 내림차순(desc) 정렬해서 표현
- 여러 개의 경우 컬럼 나열된 순서로 적용 (1차정렬, 2차 정렬, ...)

