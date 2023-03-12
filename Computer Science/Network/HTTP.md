# 인터넷 네트워크 HTTP

아래 내용은 김영한님의

- [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)

을 참고하여 작성하였습니다.

# 인터넷 통신이란 ?


컴퓨터 두대가 바로 옆에 붙어있다면 ?

- 케이블로 연결하여 데이터를 주고 받으면 됨

만약 다른나라에 있다면?

- 인터넷 망을 통해서 보내야함

- 인터넷이 어떤 규칙을 가지고 있는걸까 ?

<br>

## IP(internet protocol)


## IP - internetprotocol 인터넷 규칙

IP의 역할

- 지정한 IP주소에 데이터 전달

- 전송할때 패킷이라는 통신 단위로 데이터 전달

IP 패킷이란?

- 출발지IP, 목적지IP, 기타 데이터를 담은 것


> 이 패킷을 클라이언트에서 서버로 전달을 할때
> 
> 인터넷 망에서 IP프로토콜 내에서 서버들이 이미 규약을 따르고 있으므로 출발지와 목적지를 이해하고 있음 노드들을 통해 서버측에서 데이터 전달 받을 수있음

![image](https://user-images.githubusercontent.com/109144975/222105374-848b253a-8d61-4ca4-93db-fb3e6aa587eb.png)

<br>

## IP프로토콜의 한계

비연결성
- 받는 수신측이 서비스 불능 상태여도 그냥 보냄

비 신뢰성
- 중간에 패킷이 사라지면 알 수 없음
- 패킷이 순서대로 오는 보장이 없음

위와 같은 문제를 해결하기 위해 TCP, UDP 가 등장함

<br>

## TCP/UDP


IP라는 것을 위에 살짝 TCP라는 것을 얹어서 보완해주는 느낌으로 이해보자

![image](https://user-images.githubusercontent.com/109144975/222106107-a95595a1-74df-42df-bacd-2bf2e47b4d47.png)

### 만약 미국에 있는 친구에게 채팅을 보낸다면 ?

- 소켓 라이브러리를 사용하여 OS에 hello라는 메세지를 전달
- 전달시 tcp라는 초록색 정보를 씌워서 보냄, 그리고 IP에 노란색 IP 정보를 씌워서 보냄
- 이렇게 하면 IP패킷이 생기며 수신측에서 전달받을 수 있는 상태가 됨 - 이정도로만 이해해보자 !

<br>

**패킷이란 ?**

정보기술에서 패킷방식의 컴퓨터 네트워크가 전달하는 데이터의 형식화된 블록

즉 컴퓨터에서 데이터를 주고 받을 때 정해 놓은 규칙


TCP 프로토콜은 위 정보들을 가지고 문제를 해결함

(서버측 불능상태, 순서보장, 노드 손실 등)


<br>

TCP 특징 (전송 제어 프로토콜)

- 연결지향 - 연결이 되었나 안되었나 확인 후 메세지를 전송하는 것 TCP 3 way handshake(가상연결)
- 데이터 전달 보증 - 데이터를 전달한 것에 대한 보장을 해줌, 즉 누락이 되었을 때 알 수 있음
- 순서 보장 - 데이터 전송의 순서가 보장됨, 순서가 틀릴 시 누락된 순서부터 다시 보내라고 요청


1. 클라이언트에서 서버로 먼저 SYN이라는 메세지를 보냄
2. 서버에서 SYN과 ACK를 클라이언트에게 보냄
3. 클라이언트가 서버에게 ACK를 보냄

![image](https://user-images.githubusercontent.com/109144975/222106927-22e60bf0-7f1e-4778-ad05-e8002e420d0a.png)


- 즉 클라이언트, 서버가 각각 SYN을 보내고 ACK를 보냄으로써 서로의 연결 여부를 확인하는 방법임
(요즘에는 최적화가 되어 3번 ACK를 보낼때 데이터도 같이 보냄)
- 이 연결은 가상연결임 (개념적)
- 위와같은 것들이 가능한 이유는 TCP 패킷에 정보들이 다 있기 때문임 (출발지 - IP, PORT번호 목적지 - IP, PORT 번호, 데이터 등등)

## UDP 특징 (사용자 데이터그램 프로토콜)


기능이 많지 않음 IP에서 Port번호 , 체크섬(해당 데이터가 맞는지 검증하는 것) 정도만 추가된 것임 (3 way hand shaking 없음, 속도를 줄이기 위해)

그럼 UDP는 왜쓰나?

속도가 빠름 (TCP같은 경우 잘 구축이 되어있지만 그만큼 필요로 하는 과정이 많으므로 속도가 느림..)

최적화시키고 싶을 경우 UDP로 원하는 것대로 만들어 내면 됨

최근 HTTP 3 가 대두되고 있는데 여기서는 UDP를 사용한다고 함.. 이유는 3 way handshaking 에 걸리는 시간을 줄이기 위해

## PORT

Port가 뭐지 ?

- "논리적인 접속장소"이며, 특히 인터넷 프로토콜인 TCP/IP를 사용할 때에는 클라이언트 프로그램이 네트워크 상의 특정 서버 프로그램을 지정하는 방법으로 사용된다
- 예를들어 게임과 화상통화를 동시에 하는 상황에서 데이터들이 들어오는데 어떤 애플리케이션에 필요한 데이터들인지를 모를때 구분할 수 있도록 도와주는 역할
- 클라이언트가 여러개의 서버와 통신을 해야함, 패킷들이 나의 IP에 올때 어떻게 구분할 것인가 ? 와 같은 현상을 해결해줌


이때 TCP에서 패킷에서 출발지 PORT와 목적지 PORT가 있음, 이것을 사용하여 구분함

즉 `IP 개념`과 `PORT` 두가지가 있는 것

IP는 목적지 서버를 찾는 것, PORT는 서버 안에서의 애플리케이션을 구분하는 것


즉 아래와 같이 구분할 수 있음

![image](https://user-images.githubusercontent.com/109144975/222107874-69efe935-5558-4b7f-8da8-cc619122c386.png)


주소를 찾을때 IP가 아파트 이름이라면 PORT는 동 호수로 예를 들 수 있음

PORT
- 0 ~ 65535 할당 기능
- 0 ~ 1023 : 잘 알려진 포트, 사용하지 않는 것이 좋음
  - FTP - 20, 21
  - TELENET - 23
  - HTTP - 80
  - HTTPS - 443

## DNS

도메인 네임 시스템(Domain Name System)

DNS를 사용하지 않을때의 두가지 어려움

- IP는 기억하기가 어려움 .. 숫자들의 나열
- IP는 변경될 수 있음


위와 같은 어려움이 있으니 전화번호부 같은 서비스를 제공해주자 - 도메인 이름과 IP주소를 매칭시켜주자


네이버(www.naver.com) - 125.209.222.141


## URI(Uniform Resource Identifier)


## URI - 리소스를 식별하는 방법

- Uniform : 리소스 식별하는 통일된 방식
- Resource : 자원, URI로 식별할 수 있는 모든 것
- Identifier : 다른 항목과 구분하는데 필요한 정보

URI, URL, URN 이 각각 의미하는 것은 뭘까?
- URI는 로케이터(locator), 이름(name), 또는 둘 다 추가로 분류될 수 있다

URI라는 큰 개념안에 URL, URN이 있습니다.

리소스를 식별한다는것이 무슨 말일까요 ?
- 이는 사람들을 주민번호처럼 식별한다라고 편하게 생각해볼 수 있음
- URL - Resourse Locator - 리소스의 위치 - 이종훈이 노원에 살고있다
- URN - Resource Name - 리소스의 이름 - 이종훈 그 자체


## URL 전체 문법

- scheme://[userinfo@]host[:port][/path][?query][#fragment]
- https://www.google.com:443/search?q=hello&hl=ko

- 프로토콜(https)
- 호스트명(www.google.com)
- 포트번호(443)
- 패스(/search)
- 쿼리 파라미터(q=hello&hl=ko)

URL을 살펴보겠습니다. 만약 google에 hello라고 검색하면 어떻게 될까요 ?


전체 문법은 프로토콜, 호스트명, 포트번호, 패스, 쿼리 파라미터로 이루어져있습니다.

**프로토콜**
- 어떤 방식으로 자원에 접근할 것인가라는 약속, 규칙을 의미
- http, https, ftp 등이 있습니다.

**호스트명**
- 도메인명이나 IP주소를 직접 입력할 수 있습니다.

**패스**
- 리소스가 있는 경로
- /home/file1.jpg, /members, /members/100 등등

**쿼리 파라미터**
- key value 형태로 데이터가 들어감
- q 뒤에 값을 넣으면 검색하는 것이며 ?(물음표)로 시작함, & 로 값 추가가 가능합니다.
- 이를 쿼리 파라미터로 부르는 이유는 파라미터를 넘겨준다는 의미이기 때문



## 웹 브라우저 요청 흐름

`https://www.google.com/search?q=hello&hl=ko`

검색창에 위와 같이 입력을 한다면 어떤일이 발생할까 ?

- 구글 DNS 조회 (IP: 200.200.200.2)
- HTTPS PORT는 생략하므로, 443
- HTTP요청 메세지 생성

메소드, 패스, http 버전, host 정보가 들어있음

![image](https://user-images.githubusercontent.com/109144975/222110579-991ccb98-683d-457a-9e1d-6b6526333694.png)

HTTP 메세지 전송

![image](https://user-images.githubusercontent.com/109144975/222110929-7350e3b6-0de5-4e05-b3c7-49ac3d970db8.png)

1. 웹 브라우저가 위와같이 HTTP 메세지 생성
2. SOCKET 라이브러리를 통해 전달
   1. 위에서 찾은 IP, PORT 를 통해 3 way handshake를 하여 구글서버와 연결함
   2. 원하는 데이터 전달
3. TCP/IP 패킷 생성, HTTP 메시지 포함

![image](https://user-images.githubusercontent.com/109144975/222112838-4408001b-d29e-4133-8772-623d6611aec4.png)



![image](https://user-images.githubusercontent.com/109144975/222113053-ffecd2a1-c310-4257-97a5-54c2d4c40385.png)

![image](https://user-images.githubusercontent.com/109144975/222113111-f40a3a5a-13b7-4c18-b5e6-adb13fbd6bfb.png)

위와 같이 만든 패킷을 웹 브라우저가 구글 서버로 인터넷 망을 통해 보내게 되면 아래와 같이 됨

- 인터넷망으로 온 패킷은 수많은 인터넷 노드들을 통해서 100.100.100.1 에서 200.200.200.2로 전달
- 이후 요청패킷이 도착하게 되면 TCP, IP 패킷들을 다 벗겨내고 http 메세지를 가지고 해석을 합니다
- /search로 왔네 ? 무언가를 검색하는 거구나
- q가 hello고 hl이 한글이네 그러면 검색엔진을 통해 검색결과를 한국어로 데이터를 찾음
- 그렇게 된 후 구글 서버에서 http 응답 메세지를 만들어 냄

HTTP 응답 메세지

![image](https://user-images.githubusercontent.com/109144975/222113401-ccc7d688-9218-46e5-9241-17627981ced9.png)

- content type - text이며 데이터가 html 형식이고 언어형식은 UTF-8로 되어있음
- content length(실제 html길이) 가 3423이다

이 메세지를 동일하게 패킷에 씌운 후 웹브라우저(클라이언트)에게 전송함

웹 브라우저에게 도착하게 되면 브라우저는 해당 패킷들을 벗겨내고 메세지를 랜더링하여 화면에 표시함

![image](https://user-images.githubusercontent.com/109144975/222113863-fbf94383-67ae-4dec-b64f-178f1afd0ae7.png)

---

# HTTP

## 모든것이 HTTP

초기에는 텍스트 정보들을 전달하는 목적으로 사용되었으나 현재는 모든 것을 HTTP 메세지로 전송함
- 2, 3이 중요하지 않나? → 아님 1.1의 스펙에 거의 대부분의 기능이 들어있음 2, 3은 성능개선일 뿐임


TCP가 안정적이고 좋은것이 아닌가 ?
- 기본적인 데이터가 많고 속도가 느림..
- UDP에서 최적화 하여 나온것이 HTTP 3임
- 중요한 것은 http1.1을 잘 이해하는 것 - 대부분의 기능이 있기 때문


## 클라이언트 서버 구조

HTTP 특징

- request response 구조
- HTTP 클라이언트가 서버에게 요청을 보냄, 서버의 응답이 오기 전까지 무작정 대기함, 응답이 오면 그 메세지를 열어서 동작함
- 클라이언트와 서버를 분리하는 것이 중요(요즘에는 기본적으로 분리되어있지만 아주 예전에는 그렇지 못함)
- 서버는 비즈니스 로직, 데이터들에 집중
- 클라이언트들을 UI, 사용성에 집중
- 이렇게 되면 각각 독립적으로 진화 가능
  - 만약 100배 트래픽이 증가하였을 경우 UI, 사용성에 집중하는 것이 아닌 서버 아키텍처, 비즈니스로직에 집중할 수가 있음

<br>

## 무상태 프로토콜

> 클라이언트의 상태를 유지 하는지, 하지 않는지 여부

- 서버가 클라이언트의 상태를 보존하지 않음
- 장점 : 서버 확장성 높음(스케일아웃)
- 단점 : 클라이언트가 추가 데이터 전송

<br>

## Stateful, Stateless 차이

- stateful은 서버가 클라이언트 `상태를 보존`
- stateless는 서버가 클라이언트 `상태를 보존하지 않음`

stateful을 고객과 점원의 예시로 들어보겠습니다.

![image](https://user-images.githubusercontent.com/109144975/222115793-328edeff-d411-4f3c-bdea-a0acaa3f30d7.png)

<br>

stateless를 고객과 점원의 예시로 들어보겠습니다.

![image](https://user-images.githubusercontent.com/109144975/222116021-73b36858-d498-4897-9e15-3eef661ffd86.png)

<br>

고객의 마지막 대화만으로도 통신할 수 있음
- stateful - 신용카드로 구매하겠습니다.
- stateless - 노트북 2개를 신용카드로 구매하겠습니다.

<br>

- stateless 에서는 점원(서버)이 바뀌어도 대화가 가능하다
- 만약 서비스로 바꿔 생각해본다면 점원이 중간에 바뀌면 서비스장애가 발생하는 것임
- 다른점원에게 가면 context정보가 사라지는 것임
- stateless에서는 점원에게 그때그때 필요한 모든 정보들을 넘김으로써 점원이 바뀌어도 서비스에 아무 이상이 없음
- 이 부분이 클라이언트 서버의 아키텍처에서 엄청난 확장성을 가질 수 있음
- 서버가 장애가 나면? 처음부터 다시 대화를 해야함
- 예를들어 이벤트 페이지에서는 장비만 늘리면 되는 것임
- stateless 단점 - 한번 보낼때 데이터를 너무 많이 보내야 함

## 비 연결성(connectionless)

> 클라이언트와 연결을 유지 하는지 하지 않는지 여부

**연결을 유지하는 모델**
- 연결성을 유지 하게되면 클라이언트가 아무 작업을 필요로 하지 않아도 연결을 유지해야하므로 서버 자원 소모가 큼

![image](https://user-images.githubusercontent.com/109144975/222117435-606e2cb1-40d1-4a37-9ce3-5536c15a8112.png)


<br>

**연결을 유지하지 않는 모델**
- 필요한 것만 주고받고 연결을 끊어버림

![image](https://user-images.githubusercontent.com/109144975/222117672-0e92e29a-c165-4d64-8a70-f8a0c4ffaa90.png)
서버 - 최소한의 자원을 유지할 수 있음

- 비 연결성은 클라이언트가 요청 당시에만 서버측에서 응답을 하면 연결을 유지하지 않아 서버 자원을 효율적으로 사용할 수 있음
- 예를들어 구글이나 네이버의 경우 수천 명이 동시에 검색을 하고 있는게, 아니라 결과값이 나오면 한참 읽다가 다시 검색을 하기 때문에,
- 수천명이 사용해도 실제 초당 동시 처리하는 요청의 숫자는 매우 적다. 이럴 때, 비연결성으로 자원 절약을 할 수 있다.

**비연결성 단점**
- 만약 새로 검색을 하게되면 매번 연결(3way hand shaking)을 맺어야 함
- 이를 해결하기 위해 지속연결을 사용함

**HTTP 지속연결 (Persistent Connections)**
- 일반적으로 연결을 몇 십 초 정도 유지한거나 하는 내부 매커니즘이 있다. 이러면, 연결이 유지되는 동안, 새로운 요청을 할 때마다 더 빠르게 응답을 받을 수있어서 더 좋은 UX를 제공한다.


**서버 개발자들이 어려워하는 업무(스테이리스를 기억하자)**
- 정말 같은 시간에 딱 맞추어 발생하는 대용량 트래픽
- 예) 저녁 6:00 선착순 100명 치킨 할인 이벤트

<br>

---

# HTTP 메세지

HTTP 메세지에 모든 것을 전송
- HTML, TEXT
- Image, 음성, 영상, 파일
- JSON, XML
- 거의 모든 형태의 데이터 전송 가능
- 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용

<br>

HTTP메세지

![image](https://user-images.githubusercontent.com/109144975/222119113-938f395f-18b8-40ce-8350-cb93e622f9d5.png)

- 시작라인, 헤더, 공백라인, 메세지 바디
- 예를들어 구글에 hello를 검색한다면 위와 같은 형태
- 요청메세지의 시작라인 → GET/패스/http 버전
- 메세지 바디가 없다면 공백으로 보냄

<br>

## 시작라인

**요청 메세지**
```http request
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
```

- method(GET, POST, PUT, DELETE ..), request-target(path패스), http 버전



HTTP 메서드
- 서버가 수행해야할 동작 지정
  - GET : 리소스 조회
  - POST : 요청 내역 처리

- 파라미터로 q - hello이네 ? 이는 검색 대상이 hello 인 것(구글에서 정함) hl- 한글이네 ? 한글로된 글들을 검색하여 반환
- 절대경로로 시작한다 정도로만 알고있자

<br>

**응답 메세지**

```http request
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3424

<html>
 <body> .. <body>
<html>
```

- http 버전
- http 상태코드
  - 200 : 성공
  - 400 : 클라이언트 요청 오류
  - 500 : 서버 내부 오류
- 이유문구 : 사람이 이해할 수 있는 짧은 상태 코드 설명

<br>

## HTTP 메서드

회원 정보 관리 API를 만들어보자
- 회원 목록 조회
- 회원 조회
- 회원 등록
- 회원 수정
- 회원 삭제

<br>

**API URI 설계 고민**
- 리소스의 의미는 뭘까 ?
  - 회원을 등록하고 수정하고 조회하는게 리소스가 아니다
  - 예) 미네랄을 캐라 -> 미네랄이 리소스
  - **회원이라는 개념 자체가 바로 리소스**
- 리소스를 어떻게 식별하는게 좋을까 ?
  - 회원을 등록하고 수정하고 조회하는 것을 모두 배제
  - 회원이라는 리소스만 식별하면 된다 -> 회원 리소스를 URI에 매핑

<br>

**API URI 설계 (리소스 식별, URI 계층 구조 활용)**
- 회원 목록 조회 /members
- 회원 조회 `/members/{id}` -> 어떻게 구분하지?
- 회원 등록 `/members/{id}` -> 어떻게 구분하지?
- 회원 수정 `/members/{id}` -> 어떻게 구분하지?
- 회원 삭제 `/members/{id}` -> 어떻게 구분하지?

<br>

**리소스와 행위(메서드)를 분리**
- URI는 리소스만 식별
- **리소스**와 해당 리소스를 대상으로 하는 **행위**를 분리
  - 리소스 : 회원
  - 행위 : 조회, 등록, 삭제, 변경
- 리소스는 명사, 행위는 동사
- 행위(메서드)는 어떻게 구분?

<br>

**HTTP 메서드 종류**
- GET : 리소스 조회
- POST : 요청 데이터 처리, 주로 등록에 사용
- PUT : 리소스를 대체, 해당 리소스가 없으면 생성
- PATCH : 리소스 부분 변경
- DELETE : 리소스 삭제

## GET
- 리소스 조회
- 서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달

```http request
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
```

GET 메서드 동작 순서
1. 클라이언트가 서버로 /members/100 해당 유저를 주세로 라고 요청
2. 서버에 HTTP 메서지가 도착함
3. 서버가 클라이언트의 요청사항인 `/members/100` 를 파악하고 데이터베이스를 조회
4. 서버가 JSON 메세지를 만들고 응답 HTTP 메세지를 만들어서 클라이언트로 보냄


요청
```http request
GET /members/100 HTTP/1.1
Host: localhost:8080
```

응답데이터
```http request
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 34

{
  "username" : "hun"
  "age" : 20
}
```


## POST
- 요청데이터 처리
**- 메세지 바디를 통해 서버로 요청 데이터 전달**
- 서버는 요청 데이터를 **처리**
  - 메세지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
- 주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용


요청 데이터
```http request
POST /members HTTP/1.1
Content-Type: application/json

{
  "username" : "hun"
  "age" : 20
}
```

응답 데이터
```http request
HTTP/1.1 201 Created
Content-Type: application/json
Content-Length: 34
Location: /members/100

{
  "username" : "hun"
  "age" : 20
}
```

<br>

**요청 데이터를 어떻게 처리한다는 뜻일까 ?**

- 스펙 : POST메서드는 **대상 리소스가 리소스의 고유한 의미 체계에 따라 요청에 포함된 표현을 처리하도록 요청**합니다. (구글 번역)
- 예시
  - HTML 양식에 입력된 필드와 같은 데이터 블록을 데이터 처리 프로세스에 제공
    - HTML FORM에 입력한 정보로 회원 가입, 주문 등에서 사용
  - 게시판, 뉴스, 그룹, 메일링 리스트, 블로그 또는 유사한 기사 그룹에 메시지 게시
    - 게시판 글쓰기, 댓글 달기
  - 서버가 아직 식별하지 않는 새 리소스 생성
    - 신규 주문 생성
  - 기존 자원에 데이터 추가
    - 한 문서 끝에 내용 추가하기
- **정리 : 이 리소스 URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지 리소스마다 따로 정해야 함 -> 정해진 것이 없음**

### POST 정리
1. 새 리소스 생성(등록)
   - 서버가 아직 식별하지 않은 새 리소스 생성
2. 요청 데이터 처리
   - 단순히 데이터를 생성, 변경하는 것을 넘어서 프로세스를 처리해야하는 경우
   - 예) 주문에서 결제완료 -> 배달시작 -> 배달완료 처럼 단순히 값 변경을 넘어 프로세스의 상태가 변경되는 경우
   - POST의 결과로 새로운 리소스가 생성되지 않을 수도 있음
   - 예) POST/orders/{orderId}/start-delivery **(컨트롤 URI)**
     - orders/{orderId}, method = POST 의 경우 주문을 생성하는것과 같이 이상적으로 URI를 설계할 수 있지만
     - 그것이 어려울 경우 위의 예시와 같이 동사를 활용하여 **컨트롤 URI**를 사용해야할 수도 있음
3. 다른 메서드로 처리하기 애매한 경우
   - JSON으로 조회 데이터를 넘겨야 하는데, GET 메서드를 사용하기 어려운 경우
   - 애매하면 POST


### HTTP 메서드 PUT, PATCH, DELETE

### PUT
- 리소스를 대체
  - 리소스가 있으면 대체
  - 리소스가 없으면 생성
  - 쉽게 이야기 해서 덮어버림, 완전히 대체하므로 속성값 필드가 삭제하고 덮어버릴 수도 있음
- 중요! 클라이언트가 리소스를 식별
  - **POST와 차이점 : 클라이언트가 리소스 위치를 알고 정확히 URI 지정**

```http request
PUT /members/100 HTTP/1.1
Content-Type: application/json

{
  "username" : "hun"
  "age" : 20
}
```

### PATCH
- 리소스 부분 변경

```http request
PATCH /members/100 HTTP/1.1
Content-Type: application/json

{
  "age" : 50
}
```
- age만 50으로 변경

### PATCH
- 리소스 제거

```http request
DELETE /members/100 HTTP/1.1
Host: localhost:8080
```

- members/100 레코드 삭제

---

## HTTP 메서드 속성

- 안전
- 멱등
- 캐시가능

HTTP 메서드 속성 관련

![](https://user-images.githubusercontent.com/109144975/210503306-711f53c0-d283-442a-a88a-8d0d87a29e11.png)

### 안전

- 호출해도 리소스 변경하지 않는다.
- get만 안전(값이 변하지 않으므로), put, post, patch, delete는 안전하지 않음

### 멱등

- 한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다.
- 자동복구 메커니즘 사용시 - 서버가 timeout 등으로 정상 응답을 못주었을 때, 클라이언트가 같은 요청을 다시 해도 되는가 ? 판단근거

**멱등 메서드**
- GET
- PUT
  - 결과를 대체한다. 덮어버리기 때문에 여러번해도 최종 결과는 같다.
- DELETE
  - 결과를 삭제한다. 같은 요청을 여러번 해도 삭제된 결과는 같다.

**멱등이 아닌 메서드**

POST
- 두 번 호출하면 같은 결제가 중복해서 발생할 수 있기 때문

### 캐시가능

- 응답 결과 리소스를 캐시해서 사용해도 되는가 ?
- GET, HEAD 정도만 캐시로 사용

---

## HTTP 메서드 활용

### 클라이언트에서 서버로 데이터 전송

4가지 상황

- 정적 데이터 조회
- 동적 데이터 조회
- HTML Form을 통한 데이터 전송
- HTTP API를 통한 데이터 전송

**정적 데이터 조회**
 - 이미지, 정적 텍스트 문서
 - 쿼리 파라미터 미사용
 - 정적데이터는 쿼리 파라미터 없이 리소스 경로로 단순하게 조회 가능
 - /static/star.jpg를 get으로 요청
 - 200 OK, 와 이미지 url 값을 반환

![image](https://user-images.githubusercontent.com/109144975/221749245-b6d48d96-dcbc-4c0c-b0a0-8c3580cfd4ab.png)



**동적 데이터 조회**
 - 조회를 할때 데이터를 전달해야하는 경우
 - 검색, 게시판 목록에서 정렬 필터
 - `https://www.google.com/search?q=hello&hl=ko`
 - 쿼리 파라미터를 기반으로 정렬 필터해서 결과를 동적으로 생성하여 반환

**HTML FORM 데이터 POST전송**

Html Form submit 시 POST 전송 - 저장
 - name = username, age라는 input type에 텍스트를 넣어 전송 button을 누를때 일어나는 현상
 - 웹 브라우저가 form의 데이터를 읽어서 HTTP 메세지를 생성해줌
 - 생성은 아래와 같이 해줌

웹브라우저가 생성한 요청 HTTP 메세지
```http request
POST /save HTTP/1.1
Host: localhost:8080
Content - Type : applicatoin/x-www-form-urlencoded

username=kim&age=20
```


 - form의 내용을 메시지 바디를 통해서 전송
 - 위와 같이 쿼리 파라미터와 비슷한 방식으로 key value로 전송

**HTML Form 데이터 GET전송**

GET 전송 - 저장

Html Form 은 get전송도 가능

- get은 메세지 바디를 사용하지 않음
- 쿼리 파라미터로 넣어서 서버에 전달

**HTML Form 데이터 GET전송**

파일 전송

- Content-Type : multipart/form-data

- 파일 업로드 같은 바이너리 데이터 전송시 사용
- 다른 종류의 여러 파일과 폼의 내용 함께 전송 가능

**HTTP API 데이터 전송**

애플리케이션에서 클라이언트에서 서버로 데이터를 전송할 경우

http api로 데이터를 전송하는 것

```http request
POST /members HTTP/1.1
Content-Type: application/json

{
"username" : "hun",
"age" : 20
}
```

서버 to 서버
- 앱 클라이언트(아이폰, 안드로이드)
웹 클라이언트 - React, Vuejs 같은 웹 클라이언트와 데이터 전송
- Put, Post, Patch - 메시지 바디를 통해 데이터 전송
Get 조회
Content-Type : application/json 을 주로 사용(사실상 표준)

## HTTP API 설계 예시

- HTTP API - 컬렉션
  - POST 기반 등록
- HTTP API 스토어
  - PUT 기반 등록
- HTML FORM 사용
  - 웹 페이지 회원관리
  - GET, POST만 지원

> URI 는 항상 리소르를 식별해야지, 리소스가 아닌 다른것을 식별하면 안된다.

API 설계 - POST 기반 등록

- 회원목록 /members - GET
- 회원등록 /members - POST
- 회원조회 /members/{id} - GET
- 회원수정 /members/{id} - PATCH, PUT, POST
- 회원삭제 /members/{id} - DELETE

### 회원관리 시스템

POST - 신규자원 등록 특징

- 클라이언트는 등록될 리소스의 URI를 모른다.
  - 회원등록 /members -> POST
  - POST/members
- 서버가 새로 등록된 리소스 URI를 생성해준다.
  - HTTP/1.1 201 Created
  - Location: /members/100
- 컬렉션
  - 서버가 관리하는 리소스 디렉토리
  - 서버가 리소스의 URI를 생성하고 관리
  - 여기서 컬렉션은 /members

### 파일 관리 시스템

API 설계 - PUT 기반 등록

파일 목록 /files -> GET
파일 조회 /files/{filename}
파일 등록 /files/{filename} -> PUT `기존에 파일이 있으면 덮어씌우고 없으면 새로 생성, 파일 등록을 생각하면 PUT이 가장 잘 맞는 예시`
파일 등록 /files/{filename} -> DELETE
파일 대량 등록 /files -> POST

PUT - 신규 자원 등록 특징

- 클라이언트가 리소스 URI를 알고 있어야 한다.
  - 파일등록 /files/{filename} -> PUT
  - PUT /files/star.jpg 
- 클라이언트가 직접 리소스의 URI를 지정한다.
- 스토어
  - 클라이언트가 관리하는 리소스 저장소
  - 클라이언트가 리소스의 URI를 알고 관리
  - 여기서 스토어는 /files


POST로 신규 데이터를 등록한다는 것은 클라이언트가 서버에 요청하는 것
"나 이거 회원 등록해줘" 그러면 서버가 리소스의 URI를 만드는 것

PUT으로 신규 데이터를 등록하면 리소스 URI를 다 알고 등록해야 함
클라이언트가 등록될 리소스의 URI를 모두 관리함

하지만 대부분 POST 기반의 등록을 실무에서 함

### HTML FORM 사용

- HTML FORM은 GET, POST만 지원

- 회원 목록 /members -> GET
- 회원 등록 폼 /members/new -> GET
- 회원 등록 /members/new, /members -> POST `컨트롤 URI, members/new 와 같이 등록 폼과 일치시키는 것을 추천`
- 회원 조회 /members/{id} -> GET
- 회원 수정 폼 /members/{id}/edit -> GET
- 회원 수정 /members/{id}/edit, /members/{id} -> POST `컨트롤 URI`
- 회원 삭제 /members/{id}/delete -> POST `컨트롤 URI, HTML FORM에서는 DELETE를 쓸 수 없으므로 POST로 해결한다. 이를 컨트롤 URI라고 한다.`

컨트롤 URI
- GET, POST만 지원하므로 제약이 있음
- 이런 제약을 해결하기 위해 동사로 된 리소스 경로 사용
- POST /new, /edit, /delete가 컨트롤 URI `동사를 사용함`
- HTTP 메서드로 해결하기 애매한 경우 사용 (HTTP API포함)

## 정리

- 문서(document)
  - 단일 개념 (파일하나, 객체 인스턴스, 데이터베이스 row)
  - 예) /members/100, /files/star.jpg
- 컬렉션(collection)
  - 서버가 관리하는 리소스 디렉터리
  - 서버가 리소스의 URI를 생성하고 관리
  - 예) /members
- 스토어 (store)
  - 클라이언트가 관리하는 자원 저장소
  - 클라이언트가 리소스의 URI를 알고 관리
  - 예) /files
- 컨트롤러(controller), 컨트롤 URI
  - 문서, 컬렉션, 스토어로 해결이 어려운 경우 추가 프로세스 실행
  - 동사를 직접 사용
  - 예) /members/{id}/delete

> API 설계 기준
> 컬렉션과 문서를 사용하여 최대한 GET, POST, PUT, DELETE 로 해결을 하고
> 그런데도 안된다면
> 컨트롤 URI를 넣어 사용한다.

---

# HTTP 상태 코드

- 1XX (Informational) : 요청이 수신되어 처리중
- 2XX (Successful) : 요청 정상 처리
- 3XX (Redirection) : 요청을 완료하려면 추가 행동이 필요
- 4XX (Client Error) : 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행 불가
- 5XX (Server Error) : 서버 오류, 서버가 정상 요청을 처리하지 못함

## 2XX 성공

- 200 OK
- 201 Created (리소스 생성), post
- 202 Accepted
- 204 No content

## 200 OK

요청 성공

Get 요청 -> Start line에 응답 Header에 200 OK 와 Body에 해당 내용을 실어서 보냄

![image](https://user-images.githubusercontent.com/109144975/223975891-993a0812-6d0e-4e48-977b-0589fcee3c86.png)


## 201 Created

요청 성공해서 새로운 리소스가 생성됨

Post 요청 -> 서버에서 자원을 생성함

![image](https://user-images.githubusercontent.com/109144975/223976503-707a0faa-056a-4778-9796-dd89ddfea9a1.png)

## 202 Accepted

요청 접수되었으나 처리 완료되지 않음

- 배치 처리 같은 곳 사용

## 204 No content

서버가 요청 성공수행 하였지만, 응답 페이로드 본문에 보낼 데이터가 없음

- 예) 웹 문서 편집기에서 save 버튼
- save 버튼의 결과로 아무 내용이 없어도 된다
- save 버튼 눌러도 같은 화면 유지해야 함


## 3XX - 리다이렉션

- 300 Multiple Choices (거의 안씀)
- 301 Moved Permanently
- 302 Found
- 303 See Other
- 304 Not Modified
- 307 Temporary Redirect
- 308 Permanent Redirect 


## 리다이렉션 이해

- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동
  (리다이렉트)


- 현재 /event URL을 쓰지 않는 상황 -> new-event로 변경함
- 기존 고객들은 /event로 들어올 수 도 있으므로 리다이렉팅을 시킴
- 상태코드 : 301로 하며 Location 을 /new-event로 한다
- 그렇게 되면 클라이언트는 /event -> /new-event로 변경하여 접속한다
- 이렇게 되면 정상 요청을 서버로 하였으므로 서버는 200 OK의 상태코드를 반환하며
- 올바른 이벤트 페이지 html 코드를 반환한다.

![image](https://user-images.githubusercontent.com/109144975/223980008-fc449f79-b758-4b17-8ce0-a92e7ee09f31.png)

### 종류

- 영구 리다이렉션 - 

영구 리다이렉션 - 특정 리소스의 URI가 영구적으로 이동
• 예) /members -> /users
• 예) /event -> /new-event
• 일시 리다이렉션 - 일시적인 변경
• 주문 완료 후 주문 내역 화면으로 이동
• PRG: Post/Redirect/Get
• 특수 리다이렉션
• 결과 대신 캐시를 사용

![image](https://user-images.githubusercontent.com/109144975/223986662-47cae0b0-9503-481f-963e-842bd86fe144.png)


![image](https://user-images.githubusercontent.com/109144975/223986761-107a3a67-c437-4d1e-b698-f2078a49df09.png)

- 일시적인 리다이렉션

302, 307, 303

- 302 Found
  - 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY)
- 307 Temporary Redirect
  - 302와 기능은 같음
  - 리다이렉트시 요청 메서드와 본문 유지(요청 메서드를 변경하면 안된다. MUST NOT)
- 303 See Other
  - 302와 기능은 같음
  - 리다이렉트시 요청 메서드가 GET으로 변경

## PRG : Post/Redirect/Get

- Post로 주문 후에 웹 브라우저를 새로고침 하면 ?
- 새로고침은 다시 요청
- 중복 주문이 될 수 있음

PRG X

![image](https://user-images.githubusercontent.com/109144975/223987501-4e71f141-8b2a-44be-a8cb-5b2bf394b0fe.png)

주문 후 결과 화면에서 새로고침을 하게되면 마지막 요청이 Post/order 이었으므로 이 요청을 다시 서버에게 보내게 됨

이와 같은 오류를 방지하기 위해 일시적인 리다이렉션을 하게 됨

- POST로 주문 후에 새로 고침으로 인한 주문 방지
- POST로 주문후에 주문 결과 화면을 GET 메서드로 리다이렉트 (Get으로 하게 되면 멱등이므로 서버에는 아무 영향 X)
- 새로고침해도 결과 화면을 GET으로 조회
- 중복 주문 대신에 결과 화면만 GET으로 다시 요청

PRG 사용

![image](https://user-images.githubusercontent.com/109144975/223989327-da9709b9-a9aa-4a18-8158-0cb1d768c44a.png)

- 주문 완료 후 302 FOUND와 Location 정보를 넘겨줌
- 3XX 이므로 클라이언트는 자동 리다이렉트를 함
- GET 메서드로 변후 주문을 요청하므로 주문 결과 화면을 서버로 요청
- 주문 완료 200 OK 를 클라이언트로 보냄
- 이때 새로고침을 하여도 GET 메소드이므로 서버에는 아무 영향 X 결과화면만 다시 요청(5번으로 이동)

**PRG 이후 리다이렉트**
- URL이 이미 POST -> GET으로 리다이렉트 됨
- 새로 고침 해도 GET으로 결과 화면만 조회


### 정리

- 302 FOUND -> GET으로 변할 수 있음 (변할 수 있음)
- 307 Temporary Redirect -> 메서드가 변하면 안됨 (변하면 안됨)
- 303 See Other -> 메서드가 GET으로 변경 (변해야 함)

처음 302 스펙의 의도는 HTTP 메서드를 유지하는 것
- 그런데 웹 브라우저들이 대부분 GET으로 바꾸어버림(일부는 다르게 동작)
- 그래서 모호한 302를 대신하는 명확한 307, 303이 등장함(301 대응으로 308도 등장)
현실
- 307, 303을 권장하지만 현실적으로 이미 많은 애플리케이션 라이브러리들이 302를 기본값으로 사용
- 자동 리다이렉션시에 GET으로 변해도 되면 그냥 302를 사용해도 큰 문제 없음


304 Not Modified

캐시를 목적으로 사용
- 클라이언트에게 리소스가 수정되지 않았음을 알려준다. 따라서 클라이언트는 로컬PC에 저장된 캐시를 재사용한다. (캐시로 리다이렉트 한다.)
- 304 응답은 응답에 메시지 바디를 포함하면 안된다. (로컬 캐시를 사용해야 하므로)
- 조건부 GET, HEAD 요청시 사용

---

## 4XX 오류

클라이언트 오류

- 오류의 원인이 클라이언트에 있음
- 중요 ! 클라이언트가 이미 잘못된 요청을 함, 그러므로 똑같이 시도 하여도 실패함

## 400 Bad Request
클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음

- 요청구문, 메시지 등등
- 클라이언트는 요청 내용을 다시 검토하고, 보내야함
- 예) 요청 파라미터가 잘못되거나, API 스펙이 맞지 않을 때

## 401 Unauthorized

클라이언트가 해동 리소스에 대한 인증이 필요함

- 인증되지 않음
- 인증(Authentication): 본인이 누구인지 확인, (로그인)
  - 인가(Authorization): 권한부여 (ADMIN 권한처럼 특정 리소스에 접근할 수 있는 권한, 인증이 있어야 인가가 있음)
  - 오류 메시지가 Unauthorized 이지만 인증 되지 않음

## 403 Forbidden

서버가 요청을 이해했지만 승인을 거부함

- 주로 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우
- 예) 어드민 등급이 아닌 사용자가 로그인은 했지만, 어드민 등급의 리소스에 접근하는 경우

## 404 Not Found

- 요청 리소스가 서버에 없음
- 또는 클라이언트가 권한이 부족한 리소스에 접근할 때 해당 리소스를 숨기고 싶을 때

---

## 5XX 오류

서버 오류

- 서버 문제로 오류 발생
- 서버에 문제가 있기 때문에 재시도 하면 성공할 수도 있음(복구가 되거나 등등)

## 500 Internal Server Error

서버 문제로 오류 발생, 애매하면 500 오류
- 서버 내부 문제로 오류 발생
- 애매하면 500 오류

## 503 Service Unavailable
서비스 이용 불가
- 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음
- Retry-After 헤더 필드로 얼마뒤에 복구되는지 보낼 수도 있음


조심해야 할 부분, 5XX 에러는 언제 내면 안될까 ?

**예시)**
- 비즈니스 로직상 API스펙이 맞고 서버까지 들어옴
- 고객의 잔고가 부족할때는 ?
- 나이제한이 있는 제품을 미성년자가 구매할 경우 ?
- 5XX을 내면 안됨
- 왜냐하면 이것은 서버문제가 아니기 때문
- 비즈니스 로직상 예외케이스이므로

---

# HTTP 헤더 1 일반헤더

## HTTP BODY

![image](https://user-images.githubusercontent.com/109144975/224009381-40bd4e92-e045-4187-8343-ba0745a4cc7d.png)

표현이 표현인 이유

- 회원 데이터를 html로 표현한다고 가정
- 회원이라는 리소스를 html로 표현
- 회원 데이터를 json으로 조회한다면
- 회원 리소스를 http를 통해 주고 받을 때
- html, json으로 표현이 될 수 있음
- 실제 전달하는 것을 표현이라고 함

## 표현

- Content-Type: 표현 데이터의 형식
- Content-Encoding: 표현 데이터의 압축 방식
- Content-Language: 표현 데이터의 자연 언어
- Content-Length: 표현 데이터의 길이
- 표현 헤더는 전송, 응답 둘다 사용

## Content-Type
표현 데이터의 형식 설명 즉, content-body에 들어가는 내용이 무엇인지에 대한 형식 설명

- 미디어 타입, 문자 인코딩
- text/html; charset=utf-8
- application/json
- image/png

## Content-Encoding
표현 데이터 인코딩

- 표현 데이터(바디)를 압축하기 위해 사용
- 무엇으로 압축하였는지에 대한 정보
- 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
  - gzip
  - deflate
  - identity (압축 안함)

## Content-Language
표현 데이터의 자연 언어
- 표현 데이터의 자연 언어를 표현
  - ko
  - en
  - en-US

## Content-Length
포현 데이터의 길이

- 바이트 단위
- Transfer-Encoding(전송코딩)을 사용하면 Content-Length를 사용하면 안됨 (뒤에서 추가 설명)

---

## 협상(콘텐츠 네고시에이션)
클라이언트가 선호하는 표현 요청

클라이언트가 원하는 표현을 서버가 주는 것

- Accept: 클라이언트가 선호하는 미디어 타입 전달 (html 등)
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩 (utf-8 등)
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩 (gzip 등)
- Accept-Language: 클라이언트가 선호하는 자연 언어 (ko 등)
- 협상 헤더는 요청시에만 사용

## Accept-Languate 적용 전

클라이언트 측에서 한국어에 대한 정보가 아무것도 없는 상황

![image](https://user-images.githubusercontent.com/109144975/224056324-b9a81f4d-eabc-4e4e-8a04-1b1ef93c0874.png)


Accept-Language:ko 이므로 ko에 대한 정보를 가지고 클라이언트가 서버로 전달

![image](https://user-images.githubusercontent.com/109144975/224056399-4341f8b5-032a-4d8a-ac5b-2a324504d036.png)

서버는 한국어도 지원하므로 클라이언트가 원하는 한국어로 반환하여 전송

복잡한 예시

이럴 경우는 어떻게 해야하지 ?
-> 우선순위를 정해야 한다

![image](https://user-images.githubusercontent.com/109144975/224056881-7b73eca1-287d-4048-9978-16022fa1e331.png)

## 협상과 우선순위1
- Qualitu Values (q) 값 사용
- 0~1, 클수록 높은 우선순위
- 생략하면 1
- Accept-Language: ko-KR, ko;q=0.9,en-US;q=0/8,en;q=0.7
  - 1 ko-KR;q=1 (q생략)
  - 2 ko;q=0.9
  - 3 en-US;q=0.8
  - 4 en:q=0.7

## 협상과 우선순위2

- 구체적인 것이 우선한다.
- Accept: text/*, text/plain, text/plain;format=flowed, **/* *
  1. text/plain;format=flowed
  2. text/plain
  3. text/*
  4. **/* *

## 협상과 우선순위3

- 구체적인 것을 기준으로 미디어 타입을 맞춘다.

## 전송 방식 설명
- 단순 전송
- 압축 전송
- 분할 전송
- 범위 전송

## 단순 전송
Content-Length를 미리 알고 보내는 것

클라이언트의 요청에 대한 응답을 보내줄 때 Content에 대한 길이를 알 수 있을 때 사용하는 것

## 압축 전송
예를 들어 gzip으로 압축하여 보내는 것

Content-Encoding : gzip 정보를 함께 보내줘야 클라이언트가 무엇으로 압축되었는지를 알고 Content를 
열어볼 수 있음

## 분할 전송
Tranfer-Encoding

덩어리로 쪼개서 보내는 것

## 범위 전송

Content의 범위 bytes를 적어서 보내는 것

## 일반 정보

- From: 유저 에이전트의 이메일 정보
- Referer: 이전 웹 페이지 주소
- User-Agent: 유저 에이전트 애플리케이션 정보
- Server: 요청을 처리하는 오리진 서버의 소프트웨어 정보
- Date: 메시지가 생성된 날짜

## From
유저 에이전트의 이메일 정보

- 일반적으로 잘 사용되지 않음
- 검색 엔진 같은 곳에서, 주로 사용
- 요청에서 사용

## Referer
이전 웹 페이지 주소

- 현재 요청된 페이지의 이전 웹 페이지 주소
- A->B로 이동하는 경우 B를 요청할 때  Referer: A를 포함해서 요청
- Referer를 사용해서 유입 경로 분석 가능
- 요청에서 사용
- 참고 : referer는 단어 referrer의 오타

![image](https://user-images.githubusercontent.com/109144975/224220704-cfcb8aa4-5e1e-4e2e-a630-fe0e7a715df0.png)


## User-Agent
유저 에이전트 애플리케이션 정보

- user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/ 537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36
- 클리이언트의 애플리케이션 정보(웹 브라우저 정보, 등등)
- 통계 정보
- 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
- 요청에서 사용
- 언제쓸까 ? 특정 브라우저에서 버그가 생길때, log를 parsing하면 알 수 있음

## Server
요청을 처리하는 ORIGIN 서버(최종 목적지인 표현데이터를 만들어 응답을 해주는 서버)의 소프트웨어 정보

- Server: Apache/2.2.22 (Debian)
- server: nginx
- 응답에서 사용

## Date
메시지가 발생한 날짜와 시간

- Date: Tue, 15 Nov 1994 08:12:31 GMT
- 응답에서 사용

## 특별한 정보
- Host: 요청한 호스트 정보(도메인)
- Location: 페이지 리다이렉션
- Allow: 허용 가능한 HTTP 메서드
- Retry-After: 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간

---

## Host

![image](https://user-images.githubusercontent.com/109144975/224066190-ca2ca689-406d-43a6-a499-4947d7e9e8b8.png)


요청한 호스트 정보(도메인)

> 가상호스트란 ?
> 
> 하나의 서버 (IP:200.200.200.2) 가 있는데 이 서버안에 여러개의 애플리케이션이 실제 다른 도메인으로 구동되어있을 수 있다.

![image](https://user-images.githubusercontent.com/109144975/224066456-f912c3bf-1cfe-4c79-91fd-431caf76caa8.png)

만약 아래의 상황이라면 3개의 사이트를 어떻게 구분할까 ? IP로만 통신(TCP/IP로만 연결하여)하기때문에 구분이 불가하다.

![image](https://user-images.githubusercontent.com/109144975/224067038-1aed150e-e4e9-4fe0-9209-da2cbf447423.png)

- Host 정보는 필수이다
- 그래서 Host Header 필드를 넣어줌
- 도메인에 aaa.com이라고 입력함
- 이렇게 되면 TCP/IP로 통신 후 서버에서 받아서 호스트가 aaa.com인것을 알고 내부에서 구분하여 연결이 가능하다.


![image](https://user-images.githubusercontent.com/109144975/224068349-34b7ab86-80c7-4e8f-8cbe-49634e756278.png)


## Location
페이지 리다이렉션

- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동 (리다이렉트)
- 응답코드 3xx에서 설명
- 201 (Created): Location 값은 요청에 의해 생성된 리소스 URI
- 3xx (Redirection): Location 값은 요청을 자동으로 리디렉션하기 위한 대상 리소스를 가리킴

## Allow
허용 가능한 HTTP 메서드

- 405 (Method Not Allowed) 에서 응답에 포함해야함
- Allow: GET, HEAD, PUT (이 메소드만 지원하는구나를 클라이언트가 알 수 있음, 잘 사용하지 않음)

## Retry-After
유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간

- 503 (Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음
- Retry-After: Fri, 31 Dec 1999 23:59:59 GMT (날짜 표기)
- Retry-After: 120 (초단위 표기)


## 인증
- Authorization: 클라이언트 인증 정보를 서버에 전달
- WWW-Authenticate: 리소스 접근시 필요한 인증 방법 정의

## Authorization
클라이언트 인증 정보를 서버에 전달

- Authorization: Basic xxxxxxxxxxxxxxxx

> - 인증은 여러가지 매커니즘이 존재함
> - Oauth 등등
> - 인증마다 Value에 들어가는 값 형태는 다름
> - 따로 공부하며 값을 어떤 헤더를 넣어야 하는구나를 알 수 있음
> - 하지만 HTTP관련된 Authorization Header는 매커니즘과 관계없이 우선 Header를 제공함
> - 그리고 여기에 인증과 관련된 값을 넣어주면 됨


## WWW-Authenticate
리소스 접근시 필요한 인증 방법 정의

- 리소스 접근시 필요한 인증 방법 정의
- 401 Unauthorized 응답과 함께 사용
- 401 에러가 날 경우 이 정보들을 함께 제공해줘야 함 WWW-Authenticate: Newauth realm="apps", type=1,
title="Login to \"apps\"", Basic realm="simple"


## 쿠키

- Set-Cookie: 서버에서 클라이언트로 쿠키 전달(응답)
- Cookie: 클라이언트는 서버에서 받은 쿠키를 쿠키저장소에 하고, HTTP 요청시 무조건 쿠키 저장소의 내용을 서버로 전달

### 쿠키 미사용

welcome 페이지 접속

![image](https://user-images.githubusercontent.com/109144975/224209357-65467255-7b09-491c-ba10-2662426b3d21.png)

로그인 페이지 접속

![image](https://user-images.githubusercontent.com/109144975/224209415-e81a400c-a149-4486-9e14-a9fdbd310aba.png)

로그인 이후 다시 welcom 페이지 접속

- `안녕하세요 홍길동님` 을 기대하였지만 아님
- 왜냐하면 서버입장에서는 위 HTTP 메세지에서 사용자를 구분할 방법이 없기 때문

![image](https://user-images.githubusercontent.com/109144975/224209517-130b6c7b-5717-43b9-b1dd-eddb45e10ec1.png)

## Stateless
- HTTP는 무상태(Stateless) 프로토콜이다.
- 클라이언트와 서버가 요청과 응답을 주고 받으면 연결이 끊어진다.
- 클라이언트가 다시 요청하면 서버는 이전 요청을 기억하지 못한다.
- 클라이언트와 서버는 서로 상태를 유지하지 않는다.

대안 - 모든 사용자 정보 포함

![image](https://user-images.githubusercontent.com/109144975/224209756-67de6d28-8cde-46f1-bc04-be673255b191.png)

이것이 현실적으로 가능할까 ? - 불가함 (이 대안은 심각한 문제를 발생함)

![image](https://user-images.githubusercontent.com/109144975/224209837-722a6eb3-ef5b-4c2e-b6a5-8a4d14c5dcda.png)

## 모든 요청에 정보를 넘기는 문제
- 모든 요청에 사용자 정보가 포함되도록 개발 해야함
- 브라우저를 완전히 종료하고 다시 열면?

## 쿠키 사용

로그인
- 클라이언트가 `user=홍길동` 이라는 정보를 POST로 서버에게 주면
- 서버는 해당 정보를 쿠키 헤더를 만들어서 `set-Cookie=홍길동` 을 입력하여 클라이언트로 응답합니다. (개발자가 로직을 만드는 것)
- 웹 브라우저 내에는 쿠키 저장소가 있음
- 그 저장소에 key는 user이고 value는 홍길동이라는 정보 `user=홍길동`을 저장합니다.


![image](https://user-images.githubusercontent.com/109144975/224210539-44222a28-05bb-40dc-a758-cac07c0dc8ca.png)

로그인 이후 welcome 페이지 접속
- 쿠키 저장소에는 정보가 저장되어있는 상황
- 이때 welcome 페이지에 다시 접속하게 되면
- 자동으로 웹 브라우저는 서버에 요청을 보낼 때 마다 무조건 쿠키 저장소를 찾아봄
- 쿠키 값을 꺼내어 HTTP 헤더를 만들어서 서버에 요청을 보냄
- 그렇게 되면 서버는 `user=홍길동` 정보를 알 수 있게 됨

![image](https://user-images.githubusercontent.com/109144975/224211178-634da7c0-4cd6-448a-8d16-acddc92ecd7e.png)

로그인 이후 모든 요청에 쿠키 정보 자동 포함

![image](https://user-images.githubusercontent.com/109144975/224211812-a6f55d34-9c86-4ed2-8167-54cd6927f95a.png)

## 쿠키

모든곳에 위와같이 쿠키 정보를 보내면 보안 및 여러가지 문제가 발생할 수 있음

따라서 아래와 같이 제약하는 방법이 존재함

- 예) set-cookie: sessionId=abcde1234; expires=Sat, 26-Dec-2020 00:00:00 GMT; path=/; domain=.google.com; Secure
- 주 사용처
  - 사용자 **로그인 세션 관리**
  - 광고 정보 트래킹
- 쿠키 정보는 항상 서버에 전송됨
  - 단점 : 네트워크 트래픽 추가 유발
  - 최소한의 정보만 사용(세션 id, 인증 토큰)
  - 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지 (localStorage, sessionStorage) 참고
- 주의!
- 보안에 민감한 데이터는 저장하면 안됨(주민번호, 신용카드 번호 등등)

## sessionId

- 사용자가 쿠키로 전달한 값들을 직접 주고 받는것이 아닌
- 해당 값들에 대해 sessionId를 부여 하여
- sessionId를 통해 서버는 데이터베이스에 값을 비교하여 확인함


## 쿠키 - 생명주기
Expires, max-age

- Set-Cookie: expires=Sat, 26-Dec-2020 04:39:21 GMT
  - 만료일이 되면 쿠키 삭제
- Set-Cookie: max-age=3600 (3600초)
  - 0이나 음수를 지정하면 쿠키 삭제
- 세션 쿠키: 만료 날짜를 생략하면 브라우저 종료시 까지만 유지 (크롬 종료하면 다시 로그인해야 하는 경우)
- 영속 쿠키: 만료 날짜를 입력하면 해당 날짜까지 유지

## 쿠키 - 도메인
Domain

- 예) domain=example.org
- 명시: 명시한 문서 기준 도메인 + 서브 도메인 포함
  - `domain=example.org`를 도메인 지정해서 쿠키 생성
    - example.org는 물론이고
    - dev.example.org도 쿠키 접근
- 생략: 현재 문서 기준 도메인만 적용
  - `example.org` 에서 쿠키를 생성하고 도메인 지정을 생략
    - example.org 에서만 쿠키 접근
    - dev.example.org는 쿠키 미접근


## 쿠키 - 경로
Path

- 예) path=/home
- 이 **경로를 포함한 하위 경로 페이지**만 쿠키 접근
- 일반적으로 path=/ 루트로 지정, 왜냐하면 보통 한 도메인 안에서 쿠키 정보를 보내기를 원하기 때문
- 예)
  - path=/home 지정
  - /home -> 가능
  - /home/level1 -> 가능
  - /home/level1/level2 -> 가능
  - /hello -> 불가능

## 쿠키 - 보안
Secure, HttpOnly, SameSite

- Secure
  - 쿠키는 http, https를 구분하지 않고 전송
  - Secure를 적용하면 https인 경우에만 전송
- HttpOnly
  - XSS 공격 방지
  - 자바스크립트에서 접근 불가(document.cookie)
  - HTTP 전송에만 사용
- SameSite
  - XSRF 공격 방지
  - 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송


# HTTP 헤더 2 캐시와 조건부 요청

## 캐시 기본 동작

## 캐시가 없을 때

첫 번째 요청
- 클라이언트가 star.jpg를 요청
- HTTP BODY에 star.jpg를 넣어 응답 

![image](https://user-images.githubusercontent.com/109144975/224214176-56260bc5-7bdb-4a0d-b727-4a68b6c2fcc8.png)


두 번째 요청
- 서버에서는 이전과 동일하게 요청을 받았으므로
- 헤더와 바디를 다시 만들어 응답

![image](https://user-images.githubusercontent.com/109144975/224214613-6d12d949-743e-4c7b-b1c7-4338c562c0a0.png)

## 캐시가 없을 때
- 데이터가 변경되지 않아도 계속 네트워크를 통해서 데이터를 다운로드 받아야 한다.
- 인터넷 네트워크는 매우 느리고 비싸다.
- 브라우저 로딩 속도가 느리다.
- 느린 사용자 경험


## 캐시 적용
- 서버에서 캐시 관련 세팅이 되어있다고 가정
- 웹 브라우저가 star.jpg를 요청하게되면
- cache-control을 HTTP header에 넣어줄 수 있음, 캐시가 유효한 시간(초)


![image](https://user-images.githubusercontent.com/109144975/224214865-699a473e-2e93-4bf9-afde-371db7c7d1eb.png)

## 캐시 적용

첫 번째 요청 응답
- 웹 브라우저에 캐시를 저장하는 캐시저장소에 응답 결과 star.jpg를 저장 (60초 유효)

![image](https://user-images.githubusercontent.com/109144975/224215190-c108feb9-8deb-473c-9629-a90f4b449662.png)


## 캐시 적용

두 번째 요청
- 캐시를 먼저 찾아봄
- 캐시 유효 시간 검증 후
- 유효하면 캐시 저장소에서 바로 가져옴


1. 캐시를 먼저 찾아봄

![image](https://user-images.githubusercontent.com/109144975/224215427-10f85dd5-a528-46d9-859b-996284e1b32d.png)

2. 캐시 유효 시간 검증 후

![image](https://user-images.githubusercontent.com/109144975/224215657-14c34df6-4508-4ad4-a2b8-e3c1b2535928.png)


3. 유효하면 캐시 저장소에서 바로 가져옴 (네트워크를 탈 필요 없음)

![image](https://user-images.githubusercontent.com/109144975/224215697-27c22ac9-ca2f-4e17-a619-2c73d9ba983f.png)

## 캐시 적용
- 캐시 덕분에 캐시 가능 시간동안 네트워크를 사용하지 않아도 된다.
- 비싼 네트워크 사용량을 줄일 수 있다.
- 브라우저 로딩 속도가 매우 빠르다.
- 빠른 사용자 경험

## 캐시 적용
세 번째 요청 - 캐시 시간 초과
- 요청시 캐시 저장소에 있는 캐시 찾아봄
- 해당 캐시가 시간초과됨
- 다시 서버로 star.jpg를 요청함
- 서버는 star.jpg를 HTTP 메세지에 담아 다시 클라이언트로 보냄
- 클라이언트, 웹 브라우저는 기존의 캐시를 지우고 새로 받은 캐시 데이터를 캐시 저장소에 저장(초기화)

캐시 저장소에 조회하였지만 실패

![image](https://user-images.githubusercontent.com/109144975/224216029-b4cb425b-79e0-477b-a29e-27161a9cbab8.png)

서버로 다시 star.jpg 요청

![image](https://user-images.githubusercontent.com/109144975/224216502-d22df173-5ada-496c-a9f5-b2d35671ae01.png)

서버로부터 응답받은 데이터를 캐시 저장소에 초기화

![image](https://user-images.githubusercontent.com/109144975/224216536-38906422-73d1-4969-9aca-3b36897934c0.png)

## 캐시 시간 초과
- 캐시 유효 시간이 초과하면, 서버를 통해 데이터를 다시 조회하고, 캐시를 갱신한다.
- 이때 **다시 네트워크 다운로드가 발생**한다.

> 질문
> 
> 다시 다운받는 이유는 서버측에서 60초의 만료기간을 두었기 때문
> 
> 만료기간을 둔 이유는 해당 시간이 지나면 서버에서는 해당 데이터가 변할 수 있기 때문
> 하지만 별이라는 이미지는 변하지 않음
> 
> 만약 캐시 시간 초과가 났을때 클라이언트가 가진 데이터와 서버가 가진 데이터가 동일할때 다시 다운받지 않는 방법은 없을까 ?

## 검증헤더와 조건부 요청 1

## 캐시 시간 초과
캐시 유효 시간이 초과해서 서버에 다시 요청하면 다음 두 가지 상황이 나타난다.

- 서버에서 기존 데이터를 변경함
- 서버에서 기존 데이터를 변경하지 않음
  - 이렇게 되면 굳이 처음부터 다운로드 받아야 할까? 라는 의문이 생기게 됨

![image](https://user-images.githubusercontent.com/109144975/224217897-56b81750-63be-4f48-858a-b9928c90f305.png)

## 검증 헤더 추가

첫 번째 요청
- Last-Modified 를 헤더에 추가함
- 해당 데이터가 마지막에 수정된 시간을 의미


![image](https://user-images.githubusercontent.com/109144975/224218020-2e7556ab-80ba-493c-b115-6beb72c21ed5.png)

## 검증 헤더 추가

첫 번째 요청

응답결과를 캐시 저장소에 저장
- **데이터 최종 수정일(Last-Modified)** 도 함께 저장

![image](https://user-images.githubusercontent.com/109144975/224218163-e63994bd-18c8-43bf-b4b1-b41850559264.png)

## 검증 헤더 추가

두 번째 요청 - 캐시 시간 초과
- 유효 시간이 초과되었으므로 다시 서버로 요청해야 함
- 캐시에 Last-Modified정보가 있으면 서버로 요청 보낼 시 if-Modified-since 정보를 함께 보냄
- 서버에서는 if-modified-since 요청이 오게되면 해당 modified 수정일을 서로 검증해봄
- 만약 수정일이 동일할 경우(변동 X) HTTP응답을 만들시 304 Not Modified를 내보냄
- 이 의미는 `클라이언트 너가 이미지를 요청했지만 서버에서는 변경된것이 없어` 라는 의미
- 중요한것은 HTTP Body가 없음
- 이것이 중요한 이유는 Body가 없으면 비용이 그만큼 줄어들기 때문, 네트워크 부하가 줄어듬
- 클라이언트는 304 Not Modified를 받고 변경되지 않은것을 인식하였기 때문에 다시 cache-control(유효시간)값 갱신함
- 해당 데이터를 다시 캐시 저장소로부터 다운 받음

![image](https://user-images.githubusercontent.com/109144975/224218454-7207c2d0-71e2-447e-a2b9-6295c8b5cfdc.png)

![image](https://user-images.githubusercontent.com/109144975/224218666-522e5a3e-d950-4e51-aaaf-e4b80d2bf129.png)

![image](https://user-images.githubusercontent.com/109144975/224219580-d0ec6390-96c1-4130-b093-63d85a627ac8.png)

![image](https://user-images.githubusercontent.com/109144975/224219628-4fee706f-5483-4ebb-86d3-982b1b01093a.png)

![image](https://user-images.githubusercontent.com/109144975/224219658-2e1d7a8f-0321-4ba0-bc97-ad3d209adb0d.png)

![image](https://user-images.githubusercontent.com/109144975/224219713-cec9fcd9-cfd8-4bf1-ae23-8b61007f2980.png)

![image](https://user-images.githubusercontent.com/109144975/224219748-13f03fdc-ba5c-46a1-b9b7-2878dbe1e7d8.png)

## 검증 헤더와 조건부 요청
정리

- 캐시 유효 시간이 초과해도, 서버의 데이터가 갱신되지 않으면
- 304 Not Modified + 헤더 메타 정보만 응답(바디X)
- 클라이언트는 서버가 보낸 응답 헤더 정보로 캐시의 메타 정보를 갱신
- 클라이언트는 캐시에 저장되어 있는 데이터 재활용
- 결과적으로 네트워크 다운로드가 발생하지만 용량이 적은 헤더 정보만 다운로드 (1.1 -> 0.1)
- 매우 실용적인 해결책

## 실습

### 나의 PC 화면
로컬 PC에서 확인해보았지만 Request Header 에는 if-modified-since 항목이 존재하지 않았다.

(`if-modified` 키워드로 검색시 no result)

상태 코드도 304가 아닌 200으로 확인된다.

![image](https://user-images.githubusercontent.com/109144975/224222396-32721de5-6899-4cdd-a7d7-1a332321e3e8.png)


차이점이라면 내 생각에 강사님의 강의 기준 2019년도에서는 구글이 h2를 채택하였지만 현재 2023년도에는 h3를 적용한 것을 볼 수 있었다.

아마 버전이 HTTP 2 -> HTTP3 으로 업데이트 되면서 무언가가 바뀐게 아닐까 .. 싶다

### 강사님 화면

상태 코드 304

![image](https://user-images.githubusercontent.com/109144975/224221868-18dae25a-eb54-417c-80f6-a6dbfb68babd.png)

if-modified-since

![image](https://user-images.githubusercontent.com/109144975/224221919-d6d9b2fe-2c97-4a6a-99c6-5ba8d6a81a97.png)

## 검증 헤더와 조건부 요청 2

- 검증 헤더
  - 캐시 데이터와 서버 데이터가 같은지 검증하는 데이터
  - Last-Modified , ETag
- 조건부 요청 헤더
  - 검증 헤더로 조건에 따른 분기
  - If-Modified-Since: Last-Modified 사용
  - If-None-Match: ETag 사용
  - 조건이 만족하면 200 OK
  - 조건이 만족하지 않으면 304 Not Modified

### 예시
- If-Modified-Since: 이후에 데이터가 수정되었으면?
  - 데이터 미변경 예시
  - 변경이 일어나지 않았으니 캐시 조회해서 사용해라라는 의미
    - 캐시: 2020년 11월 10일 10:00:00 vs 서버: 2020년 11월 10일 10:00:00
    - 304 Not Modified, 헤더 데이터만 전송(BODY 미포함)
    - 전송 용량 0.1M (헤더 0.1M, 바디 1.0M)
- 데이터 변경 예시
  - 캐시: 2020년 11월 10일 10:00:00 vs 서버: 2020년 11월 10일 **11**:00:00
  - 200 OK, 모든 데이터 전송(BODY 포함)
  - 전송 용량 1.1M (헤더 0.1M, 바디 1.0M)

### Last-Modified, If-Modified-Since 단점
- 1초 미만(0.x초) 단위로 캐시 조정이 불가능
- 날짜 기반의 로직 사용
- 데이터를 수정해서 날짜가 다르지만, 같은 데이터를 수정해서 데이터 결과가 똑같은 경우
  - A -> B, B -> A : 실제로는 결국 A로 같은 데이터지만 날짜가 바뀌는 경우
- 서버에서 별도의 캐시 로직을 관리하고 싶은 경우
  - 예) 스페이스나 주석처럼 크게 영향이 없는 변경에서 캐시를 유지하고 싶은 경우

### ETag, If-None-Match
- ETag(Entity Tag)
  - 캐시용 데이터에 임의의 고유한 버전 이름을 달아둠
    - 예) ETag: "v1.0", ETag: "a2jiodwjekjl3"
- 데이터가 변경되면 이 이름을 바꾸어서 변경함(Hash를 다시 생성)
  - 예) ETag: "aaaaa" -> ETag: "bbbbb"
- 진짜 단순하게 ETag만 보내서 같으면 유지, 다르면 다시 받기!

## 검증 헤더 추가
첫 번째 요청

- 클라이언트에서 start.jpg를 요청
- 서버에서 star.jpg를 ETag를 내려줌

![image](https://user-images.githubusercontent.com/109144975/224541065-81b6ef6a-64f4-4b2f-a66b-b66e95b3c836.png)

- 클라이언트가 응답결과 ETag를 캐시에 저장

![image](https://user-images.githubusercontent.com/109144975/224541088-7c6f9c05-4cbb-4f1c-97f9-cb9e9a870d46.png)

두 번째 요청 - 캐시 시간 초과
- 클라이언트가 캐시를 조회

![image](https://user-images.githubusercontent.com/109144975/224541096-dd51737c-e21c-4a11-9ad8-436b9dbf7abe.png)

- 이때 시간(60초)가 초과 됨

![image](https://user-images.githubusercontent.com/109144975/224541102-10750755-a31f-4a73-b31b-09d201878684.png)

- If-None-Match를 통해 서버로 "aaaaaa"가 변경되었는지 확인요청
- 아직 데이터가 수정되지 않았음

![image](https://user-images.githubusercontent.com/109144975/224541138-75d93a54-f2c9-4440-a1d0-03a1e2c6343e.png)


- 실패 304 Not Modified 를 보냄
- HTTP Body를 보내지 않음

![image](https://user-images.githubusercontent.com/109144975/224541151-15c221c4-a836-4bd6-9091-f0407ebca363.png)

- 캐시를 다시 재사용
- 데이터 갱신

![image](https://user-images.githubusercontent.com/109144975/224541395-1b028f90-f267-48c2-9886-827fe528b0aa.png)

- 캐시에서 조회

![image](https://user-images.githubusercontent.com/109144975/224541429-d53a795f-c4f3-46cb-acd6-d966eb6218ab.png)

ETag, If None Match 정리

- 진짜 단순하게 ETag만 서버에 보내서 같으면 유지, 다르면 다시 받기!
- **캐시 제어 로직을 서버에서 완전히 관리**
- 클라이언트는 단순히 이 값을 서버에 제공(클라이언트는 캐시 메커니즘을 모름)
- 예)
  - 서버는 배타 오픈 기간인 3일 동안 파일이 변경되어도 ETag를 동일하게 유지
  - 애플리케이션 배포 주기에 맞추어 ETag 모두 갱신

## 캐시와 조건부 요청 헤더

## 캐시 제어 헤더

캐시는 캐시 제어와 관련된 헤더(아래 요소)들이 있음

- **Cache-Control: 캐시 제어**
- Pragma: 캐시 제어(하위 호환)
- Expires: 캐시 유효 기간(하위 호환)

## Cache-Control
캐시 지시어(directives)

- Cache-Control: max-age
  - 캐시 유효 시간, 초 단위
- Cache-Control: no-cache
  - 데이터는 캐시해도 되지만, 항상 원(origin) 서버에 검증(if none match)하고 사용
- Cache-Control: no-store
- 데이터에 민감한 정보가 있으므로 저장하면 안됨
(메모리에서 사용하고 최대한 빨리 삭제)


## Expires
캐시 만료일 지정(하위 호환)

- expires: Mon, 01 Jan 1990 00:00:00 GMT
- 캐시 만료일을 정확한 날짜로 지정 (불편함)
- HTTP 1.0 부터 사용
- 지금은 더 유연한 Cache-Control: max-age 권장
- Cache-Control: max-age와 함께 사용하면 Expires는 무시

## 검증헤더 조건부 요청 헤더
정리

- 검증 헤더 (Validator)
  - ETag: "v1.0", ETag: "asid93jkrh2l"
  - Last-Modified: Thu, 04 Jun 2020 07:19:24 GMT
- 조건부 요청 헤더
  - If-Match, If-None-Match: ETag 값 사용
  - If-Modified-Since, If-Unmodified-Since: Last-Modified 값 사용


## 프록시 캐시

## 원 서버 직접 접근

- origin 서버
- 미국에 있는 서버(origin)로 매번 직접 요청을 하게 되면 시간이 너무 오래 걸림
- 모든 사람들이 사진 하나 다운받는데 0.5초나 기다려야 함

![image](https://user-images.githubusercontent.com/109144975/224541933-a33f46dd-8131-4fd4-8b0a-51abcd8baf8c.png)

## 프록시 캐시 도입

- 프록시 캐시 서버를 클라이언트 기준 가까운 곳에 위치시킴
- DNS 요청을 조금 조작하여 미국 origin 서버로 바로 요청하는 것이 아니라 프록시 서버를 거치도록 함

> 이러한 원리로 인해 유튜브를 볼때 빠르게 볼 수 있음
> 
> - 예를 들어 사람들이 많이 보지 않는 기술 유튜버를 보면 유튜브 영상 로딩 속도가 비교적 느림
> - 반대로 사람들이 많이 보는 컨텐츠들을 보게되면 비교적 빠르게 로딩 됨
> - 이러한 서비스를 CDN 서비스라고 함
> - 최초 유저가 다운로드시 비교적 느리고 그 이후부터는 빠르게 로딩


> [CDN](https://www.akamai.com/ko/our-thinking/cdn/what-is-a-cdn) 이란 ?
> 
> - CDN(콘텐츠 전송 네트워크)은 지리적으로 분산된 여러 개의 서버
> - 웹 콘텐츠를 사용자와 가까운 곳에서 전송함으로써 전송 속도를 높임
> - 전 세계 데이터센터는 파일 복사본을 임시로 저장하는 프로세스인 캐싱을 사용
> - 사용자는 가까운 서버를 통해 웹 활성화 디바이스 또는 브라우저에서 인터넷 콘텐츠에 빠르게 접속할 수 있음


![image](https://user-images.githubusercontent.com/109144975/224541940-2cfd1f90-c36f-4ab2-8ba7-d9cae72ecdfe.png)

## 프록시 캐시 도임

- private 캐시는 웹 각각이 사용하는 캐시
- public 캐시는 공용으로 사용하는 캐시 (유튜브 영상)


![image](https://user-images.githubusercontent.com/109144975/224542608-f97d22ab-e2d1-4b51-9aa7-049e853abfb3.png)

## Cache-Control
캐시 지시어 - 기타

- Cache-Control: public
  - 응답이 public 캐시에 저장되어도 됨
- Cache-Control: private
  - 응답이 해당 사용자만을 위한 것(로그인 정보 등)임, private 캐시에 저장해야 함(기본값)
- Cache-Control: s-maxage
  - 프록시 캐시에만 적용되는 max-age
- Age: 60 (HTTP 헤더)
  - 오리진 서버에서 응답 후 프록시 캐시 내에 머문 시간(초)


## 캐시 무효화

## Cache-Control
확실한 캐시 무효화 응답

- Cache-Control: no-cache, no-store, must-revalidate
- Pragma: no-cache
  - HTTP 1.0 하위 호환

캐시를 적용 안하면 캐싱이 안되는거 아닌가 ?
- 아님, GET요청을 하게되면 웹 브라우저가 임의로 캐시를 할 수 있음
- 만약 정말 해당 페이지가 캐시가 되면 안된다면 위의 Cache-Control 요소(HTTP1.0은 Pragma 까지)들을 다 넣어주어야 함
  - ex) 사용자 통장 잔고 - 계속 갱신이 되므로 캐시를 할 필요가 없음

## Cache-Control
캐시 지시어(directives) - 확실한 캐시 무효화

- Cache-Control: no-cache
  - 데이터는 캐시해도 되지만, 항상 원 서버에 검증하고 사용(이름에 주의!)
- Cache-Control: no-store
  - 데이터에 민감한 정보가 있으므로 저장하면 안됨 (메모리에서 사용하고 최대한 빨리 삭제)
- Cache-Control: must-revalidate
  - 캐시 만료후 최초 조회시 **원 서버에 검증**해야함
  - 원 서버 접근 실패시 반드시 오류가 발생해야함 - 504(Gateway Timeout)
  - must-revalidate는 캐시 유효 시간이라면 캐시를 사용함
- Pragma: no-cache
  - HTTP 1.0 하위 호환

## no-cache vs must-revalidate
no-cache 기본 동작

- 웹 브라우저에서 프록시 캐시 서버로 Cache-Control 이 no-cahce로 요청되었을때는 프록시 캐시서버에서 바로 응답을 하는 것이 아님
- 웹 브라우저에서 요청시 이전 HTTP 응답코드에 no-cache 가 있었기 때문에, 그 다음 요청시 no-cache로 보낼 수 있음
- 해당 no-cache 요청을 프록시 서버가 받고 원 서버로의 요청이 필요하므로 다시 원서버로 요청
- 원 서버에서 검증 시도
- 응답을 줌 (사용 가능하므로 304 Not Modified)


![image](https://user-images.githubusercontent.com/109144975/224562310-8ff0e95a-9e9a-4898-9eae-82f6d0e8096d.png)

## no-cache vs must-revalidate

- 프록시 서버에서 원 서버로 순간 네트워크 단절로 인해 접근이 불가할 경우는 ?
- 프록시 캐시 응답에서 no-cache 와 must-revalidate 차이가 남

nocache
- 원 서버에 접근할 수 없는 경우 서버 설정에 따라서 캐시 데이터를 반환할 수 있음
- 오류보다는 오래된 데이터라도 보여주자 (200 OK)

![image](https://user-images.githubusercontent.com/109144975/224562322-b0b81c89-d31c-4600-9f58-c17a26a5b29e.png)


## no-cache vs must-revalidate

must-revalidate
- 원서버에 접근할 수 없는 경우, **항상 오류**가 발생해야 함
- 504 Gateway Timeout
- 만약 송금을 하였는데 이체내역이 업데이트가 안되고 이전 내역(오래된 데이터)이 그대로 보인다면?
  - 나중에 원서버 접근이 되어 업데이트가 되면 결과적으로는 상관이 없겠지만 혼란을 야기할 수 있음

> 따라서 확실한 캐시 처리를 하기 위해서는
> 
> - 서버쪽에서 HTTP 응답 코드 만들경우  Cache-Control 요소(no-cache, must-revalidate)들을 넣어주어야 함

![image](https://user-images.githubusercontent.com/109144975/224562343-3cfdc46c-bf72-488f-a3f8-1b4f37a90a71.png)
