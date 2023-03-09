# 인터넷 네트워크 HTTP

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

# HTTP 헤더

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
- Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달

