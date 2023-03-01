# 인터넷 네트워크

## 인터넷 통신


컴퓨터 두대가 바로 옆에 붙어있다면 ?

- 케이블로 연결하여 데이터를 주고 받으면 됨

만약 다른나라에 있다면?

- 인터넷 망을 통해서 보내야함

- 인터넷이 어떤 규칙을 가지고 있는걸까 ?

<br>

## IP(internet protocol)


### IP - internetprotocol 인터넷 규칙

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

### IP프로토콜의 한계

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

### UDP 특징 (사용자 데이터그램 프로토콜)


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


### URI - 리소스를 식별하는 방법

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


### URL 전체 문법

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



### 웹 브라우저 요청 흐름

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


### 클라이언트 서버 구조

HTTP 특징

- request response 구조
- HTTP 클라이언트가 서버에게 요청을 보냄, 서버의 응답이 오기 전까지 무작정 대기함, 응답이 오면 그 메세지를 열어서 동작함
- 클라이언트와 서버를 분리하는 것이 중요(요즘에는 기본적으로 분리되어있지만 아주 예전에는 그렇지 못함)
- 서버는 비즈니스 로직, 데이터들에 집중
- 클라이언트들을 UI, 사용성에 집중
- 이렇게 되면 각각 독립적으로 진화 가능
  - 만약 100배 트래픽이 증가하였을 경우 UI, 사용성에 집중하는 것이 아닌 서버 아키텍처, 비즈니스로직에 집중할 수가 있음

<br>

### 무상태 프로토콜

> 클라이언트의 상태를 유지 하는지, 하지 않는지 여부

- 서버가 클라이언트의 상태를 보존하지 않음
- 장점 : 서버 확장성 높음(스케일아웃)
- 단점 : 클라이언트가 추가 데이터 전송

<br>

### Stateful, Stateless 차이

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

### 비 연결성(connectionless)

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

## HTTP 메세지

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

### 시작라인

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

### HTTP 메서드

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

### GET
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


### POST
- 요청데이터 처리
**- 메세지 바디를 통해 서버로 요청 데이터 전달**
- 서버는 요청 데이터를 **처리**
  - 메세지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
- 주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용


요청 데이터
```http request
POST /members/100 HTTP/1.1
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
3. 다른 메서드로 처리하기 애매한 경우
   - JSON으로 조회 데이터를 넘겨야 하는데, GET 메서드를 사용하기 어려운 경우
   - 애매하면 POST


### HTTP 메서드 PUT, PATCH, DELETE



## HTTP 메서드 속성

![](https://user-images.githubusercontent.com/109144975/210503306-711f53c0-d283-442a-a88a-8d0d87a29e11.png)

**안전**

호출해도 리소스 변경하지 않는다.
get만 안전, put, post, patch, delete는 안전하지 않음

**멱등**

한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다.

자동복구 메커니즘 사용시 - 서버가 timeout 등으로 정상 응답을 못주었을 때, 클라이언트가 같은 요청을
다시 해도 되는가 ? 판단근거
멱등 메서드

GET
PUT
DELETE

멱등이 아닌 메서드

POST

두 번 호출하면 같은 결제가 중복해서 발생할 수 있기 때문

**캐시가능**

응답 결과 리소스를 캐시해서 사용해도 되는가 ?

GET, HEAD 정도만 캐시로 사용

## 클라이언트에서 서버로 데이터 전송

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
앱 클라이언트(아이폰, 안드로이드)
웹 클라이언트 - React, Vuejs 같은 웹 클라이언트와 데이터 전송
Put, Post, Patch - 메시지 바디를 통해 데이터 전송
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




