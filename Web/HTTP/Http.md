# 인터넷 네트워크

## 인터넷 통신

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c020d67d-e5cf-4ff8-ae4e-79faf1305bcd/Untitled.png)

컴퓨터 두대가 바로 옆에 붙어있다면 ?

케이블로 연결하여 데이터를 주고 받으면 됨

만약 다른나라에 있다면?

인터넷 망을 통해서 보내야함

인터넷이 어떤 규칙을 가지고 있는걸까 ?

## IP(internet protocol)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2d82674b-b3ca-48e4-a11f-e338889c401c/Untitled.png)

IP - internetprotocol 인터넷 규칙

IP의 역할

지정한 IP주소에 데이터 전달

전송할때 패킷이라는 통신 단위로 데이터 전달

IP 패킷이란?

출발지IP, 목적지IP, 기타 데이터를 담은 것

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/33905fbe-4bbb-4e59-9c26-c4405745c9e0/Untitled.png)

이 패킷을 클라이언트에서 서버로 전달을 할때

인터넷 망에서 IP프로토콜 내에서 서버들이 이미 규약을 따르고 있으므로 출발지와 목적지를 이해하고 있음 노드들을 통해 서버측에서 데이터 전달 받을 수있음

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/92eff2c2-fda4-4b25-90a0-48523e6f6b94/Untitled.png)

IP주소를 확인하며 찾아가는 과정

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/30b977f1-0e05-4d99-a9c4-02f1619427ae/Untitled.png)

IP주소를 확인하며 찾아가는 과정

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b5d76d62-cb5a-4b3d-8299-0c7aae972521/Untitled.png)

받는 수신측이 서비스 불능 상태여도 그냥 보냄

신뢰할 수 없음

프로그램 구분

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/04f3722f-9a78-4634-9e8e-0ea31f32728b/Untitled.png)

서버가 사용할 수 없는 상태라면 ?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/87d67815-8831-4efb-a8ff-c2ef46f2052d/Untitled.png)

중간 노드가 꺼져버린다면 ?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fc7d8ff9-6689-427d-97a8-6cd0f0896f68/Untitled.png)

순서는 언제든지 바뀔 수 있음

아래와 같이 2번이 먼저 도착할 수도 있음

이와 같은 문제를 해결하기 위해 TCP, UDP 가 등장함

## TCP/UDP

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b7468db3-f08b-4ec9-898d-e8f3c8ed6074/Untitled.png)

IP라는 것을 위에 살짝 TCP라는 것을 얹어서 보완해주는 느낌으로 이해

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/01668017-3cec-41dd-848a-2885e3a575f4/Untitled.png)

만약 미국에 있는 친구에게 채팅을 보낸다면 ?

소켓 라이브러리를 사용하여 OS에 hello라는 메세지를 전달

전달시 tcp라는 초록색 정보를 씌워서 보냄, 그리고 IP에 노란색 IP 정보를 씌워서 보냄

이렇게 하면 IP패킷이 생기며 수신측에서 전달받을 수 있는 상태가 됨 - 이정도로만 이해해보자 !

패킷이란 ?

정보기술에서 패킷방식의 컴퓨터 네트워크가 전달하는 데이터의 형식화된 블록.

즉 컴퓨터에서 데이터를 주고 받을 때 정해 놓은 규칙

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4a71b0a8-fff6-4e3b-85f8-7993a7bc56de/Untitled.png)

TCP 프로토콜은 위 정보들을 가지고 문제를 해결함

(서버측 불능상태, 순서보장, 노드 손실 등)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9572a018-e475-4756-b071-0a9182f84db6/Untitled.png)

연결지향 - 연결이 되었나 안되었나 확인 후 메세지를 전송하는 것

데이터 전달 보증 - 데이터를 전달한 것에 대한 보장을 해줌, 즉 누락이 되었을 때 알 수 있음

순서 보장 - 데이터 전송의 순서가 보장됨

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d343b8c8-1f57-4ce2-9222-d473f6c51619/Untitled.png)

1. 클라이언트에서 서버로 먼저 SYN이라는 메세지를 보냄
2. 서버에서 SYN과 ACK를 클라이언트에게 보냄
3. 클라이언트가 서버에게 ACK를 보냄

즉 클라이언트, 서버가 각각 SYN을 보내고 ACK를 보냄으로써 서로의 연결 여부를 확인하는 방법임

(요즘에는 최적화가 되어 3번 ACK를 보낼때 데이터도 같이 보냄)

이 연결은 가상연결임 (개념적)

위와같은 것들이 가능한 이유는 TCP 패킷에 정보들이 다 있기 때문임

(출발지 - IP, PORT번호 목적지 - IP, PORT 번호, 데이터 등등)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18ced4b5-04f5-4586-9e74-6c44de6f6225/Untitled.png)

기능이 많지 않음 IP에서 Port번호 , 체크섬(해당 데이터가 맞는지 검증하는 것) 정도만 추가된 것임 (3 way hand shaking 없음)

그럼 UDP는 왜쓰나?

속도가 빠름 (TCP같은 경우 잘 구축이 되어있지만 그만큼 필요로 하는 과정이 많으므로 속도가 느림..)

최적화시키고 싶을 경우 UDP로 원하는 것대로 만들어 내면 됨

최근 HTTP 3 가 대두되고 있는데 여기서는 UDP를 사용한다고 함.. 이유는 3 way handshaking 에 걸리는 시간을 줄이기 위해

## PORT

Port가 뭐지 ?

"논리적인 접속장소"이며, 특히 인터넷 프로토콜인 TCP/IP를 사용할 때에는 클라이언트 프로그램이 네트워크 상의 특정 서버 프로그램을 지정하는 방법으로 사용된다

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2d168106-3a53-4a83-bbbb-55fc56ef6b06/Untitled.png)

예를들어 게임과 화상통화를 동시에 하는 상황에서 데이터들이 들어오는데 어떤 애플리케이션에 필요한 데이터들인지를 모를때 구분할 수 있도록 도와주는 역할

클라이언트가 여러개의 서버와 통신을 해야함, 패킷들이 나의 IP에 올때 어떻게 구분할 것인가 ?

와 같은 현상을 해결해줌

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3220a716-fe7d-41a1-bb50-171fdad97e56/Untitled.png)

이때 TCP에서 패킷에서 출발지 PORT와 목적지 PORT가 있음, 이것을 사용하여 구분함

즉 IP 개념과 PORT 두가지가 있는 것임

IP는 목적지 서버를 찾는 것, PORT는 서버 안에서의 애플리케이션을 구분하는 것

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eb0285fe-2ab3-462f-b6ac-b72c6bbfcee3/Untitled.png)

즉 아래와 같이 구분할 수 있음

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/27ba78e4-908a-49e8-9754-80315908a7db/Untitled.png)

주소를 찾을때 IP가 아파트 이름이라면 PORT는 동 호수로 예를 들 수 있음

## DNS

도메인 네임 시스템(Domain Name System)

DNS를 사용하지 않을때의 두가지 어려움

- IP는 기억하기가 어려움 .. 숫자들의 나열
- IP는 변경될 수 있음

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2c75ab77-3ea7-4d49-8a4d-6f5382720b3c/Untitled.png)

위와 같은 어려움이 있으니 전화번호부 같은 서비스를 제공해주자 - 도메인 이름과 IP주소를 매칭시켜주자

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2fd0d4dc-ba4a-46d5-bb59-8238daaf4bee/Untitled.png)

네이버 - 125.209.222.141

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fcd7c63f-d83a-4e69-a0f8-9f24b3b49876/Untitled.png)

# URI(Uniform Resource Identifier)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/466f1d7a-97a1-4b31-97c4-6e8dcc81cb62/Untitled.png)

URI - 리소스를 식별하는 방법

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1f486e5c-dd96-4662-8def-ea0ca47d7cc1/Untitled.png)

URI, URL, URN 이 각각 의미하는 것은 뭘까?

URI는 로케이터(locator), 이름(name), 또는 둘 다 추가로 분류될 수 있다.

이게 의미하는게 무엇인지 아래에서 살펴보겠습니다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4049ee8e-5886-4d8c-b0f7-59e94dd8b6b9/Untitled.png)

URI라는 큰 개념안에 URL, URN이 있습니다.

리소스를 식별한다는것이 무슨 말일까요 ?

이는 사람들을 주민번호처럼 식별한다라고 편하게 생각해볼 수 있음

URL - Resourse Locator - 리소스의 위치 - 이종훈이 노원에 살고있다

URN - Resource Name - 리소스의 이름 - 이종훈 그 자체

아래와 같이 생김

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8e7dbd00-4272-4421-a8c6-ed58e4b3e0f8/Untitled.png)

기본적으로 검색창에 적는 것은 URL

이름만 부여하여 사용하는 것이 URN - 그런데 잘 사용하기가 어려움 그래서 URL만 사용함

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c701613f-1d9b-4d5f-9361-4b2f29ce10fc/Untitled.png)

Uniform은 식별방식

Resource는 URI로 식별할 수 있는 모든 것. 즉 웹 브라우저의 HTML이나 파일 뿐만이 아니라 현재 실시간 교통량, 날씨 정보 등

Identifier 은 식별하기 위한 정보 (ex 주민번호) 입니다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a7cf71be-cd83-4fec-bfc5-195c8c36ee9f/Untitled.png)

URL을 주소창에 검색하는 의미는 리소스가 해당 위치에 있을 것이라는 의미입니다.

URN은 사용하지 않음 ..

URL을 살펴보겠습니다. 만약 google에 hello라고 검색하면 어떻게 될까요 ?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ec4e3805-3cb8-43d0-bd67-fa3c2ad01677/Untitled.png)

전체 문법은 프로토콜, 호스트명, 포트번호, 패스, 쿼리 파라미터로 이루어져있습니다.

프로토콜이란 어떤 방식으로 자원에 접근할 것인가라는 약속, 규칙을 의미합니다.

http, https, ftp 등이 있습니다.

(userinfo는 거의 사용하지 않음)

호스트명 - 도메인명이나 IP주소를 직접 입력할 수 있습니다.

패스 - 리소스가 있는 경로입니다. 이는 보통 계층적 구조로 아래와 같이 되어있음

/home/file1.jpg, /members, /members/100 등등

쿼리 파라미터 - key value 형태로 데이터가 들어감

q 뒤에 값을 넣으면 검색하는 것이며 ?(물음표)로 시작함, & 로 값 추가가 가능합니다.

이를 쿼리 파라미터로 부르는 이유는 파라미터를 넘겨준다는 의미이기 때문입니다.

웹 브라우저 요청 흐름

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18879a02-a7d4-4ce2-942c-180466ad8cb9/Untitled.png)

검색창에 위와 같이 입력을 한다면 어떤일이 발생할까요 ?

웹 브라우저가 DNS서버를 조회를 하여 해당 IP와 Port정보를 찾아냄- HTTP 요청 메세지를 생성함

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6258317b-0a15-4392-a9d6-f8e4b4263914/Untitled.png)

메소드, 패스, http 버전, host 정보가 들어있음

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e58ab7be-db94-4461-aecd-57686b2b5ce4/Untitled.png)

이 과정을 설명하기 위해 인터넷 기본 요소들을 알아본 것임

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/80b881f7-a657-43bf-8cba-1cafe9cdae01/Untitled.png)

위와 같이 만든 패킷을 웹 브라우저가 구글 서버로 인터넷 망을 통해 보내게 되면 아래와 같이 됨

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fbf23fb3-5689-4e6a-bb3e-ae8d2e9b01b2/Untitled.png)

인터넷망으로 온 패킷은 수많은 인터넷 노드들을 통해서 100.100.100.1 에서 200.200.200.2로 전달이 됩니다.

이후 요청패킷이 도착하게 되면 TCP, IP 패킷들을 다 벗겨내고 http 메세지를 가지고 해석을 합니다

/search로 왔네 ? 무언가를 검색하는 거구나 - q가 hello고 hl이 한글이네 그러면 검색엔진을 통해 검색결과를 한국어로 데이터를 찾음 - 그렇게 된 후 구글 서버에서 http 응답 메세지를 만들어 냄

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9816e3b6-5749-44e2-9dba-5985f8b07f58/Untitled.png)

content type - text이며 데이터가 html 형식이고 언어형식은 UTF-8로 되어있음

content length 는 크기가 3423이다

이 메세지를 동일하게 패킷에 씌운 후 웹브라우저에게 전송함

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/15d96633-c165-4dde-aac9-34668b8398e8/Untitled.png)

웹 브라우저에게 도착하게 되면 브라우저는 해당 패킷들을 벗겨내고 메세지를 랜더링하여 화면에 표시함

# HTTP

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6e989cfe-6c44-4648-a024-f10b4a793c1d/Untitled.png)

## 모든것이 HTTP

초기에는 텍스트 정보들을 전달하는 목적으로 사용되었으나 현재는 모든 것을 HTTP 메세지로 전송함

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3076eb2f-61ed-43e5-a755-49b61a919233/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bc067aa3-bd8f-4721-b120-da1eaddfb015/Untitled.png)

2, 3이 중요하지 않나? → 아님 1.1의 스펙에 거의 대부분의 기능이 들어있음 2, 3은 성능개선일 뿐임

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/db3de92d-5d94-4d7a-8e8c-b74ac6371010/Untitled.png)

TCP가 안정적이고 좋은것이 아닌가 ?

기본적인 데이터가 많고 속도가 느림..

UDP에서 최적화 하여 나온것이 HTTP 3임

어떤 것들이 HTTP 버전으로 통신되고 있는지 보자

chrome을 연다 - f12 - hello 라고 검색 - 오른쪽버튼 protocol 누름

중요한 것은 http1.1을 잘 이해하는 것 - 대부분의 기능이 있기 때문

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9ce4da2a-7560-45d8-a970-cd99f5bab33f/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e4cdde80-3f72-4db2-b9e2-0a35d0126809/Untitled.png)

request response 구조

클라이언트가 서버에게 요청을 보냄, 서버의 응답이 오기 전까지 무작정 대기함, 응답이 오면 그 메세지를 열어서 동작함

클라이언트와 서버를 분리하는 것이 중요(요즘에는 기본적으로 분리되어있지만 아주 예전에는 그렇지 못함)

서버는 비즈니스 로직, 데이터들에 집중

클라이언트들을 UI, 사용성에 집중

이렇게 되면 각각 독립적으로 진화 가능

만약 100배 트래픽이 증가하였을 경우 UI, 사용성에 집중하는 것이 아닌 서버 아키텍처, 비즈니스로직에 집중할 수가 있음

## 무상태 프로토콜

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c2ff7444-0c83-4840-9764-27008fcb6336/Untitled.png)

서버가 클라이언트의 상태를 보존하지 않는다 ? - 무슨말일까요

고객과 점원의 예시로 들어보겠습니다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4a1a23e7-3ab5-4221-b8b3-b25af26384fe/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/11d1fd38-8930-4b94-944c-a8bf083dd14d/Untitled.png)

만약 점원이 중간에 바뀐다면 ??

무상태 프로토콜 - 서버가 클라이언트의 상태를 보존하지 않음

stateful은 서버가 클라이언트 상태를 보존

stateless는 서버가 클라이언트 상태를 보존하지 않음

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f75af31e-7580-4169-ba84-4768268aee16/Untitled.png)

상태유지 - stateful

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f3cf8688-df12-4c01-9512-dc9c5a477703/Untitled.png)

무상태 - stateless

고객의 마지막 대화만으로도 통신할 수 있음

stateful - 신용카드로 구매하겠습니다.

stateless - 노트북 2개를 신용카드로 구매하겠습니다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/138ad015-9acb-43ed-b654-5d770627221a/Untitled.png)

stateless 에서는 점원(서버)이 바뀌어도 대화가 가능하다

만약 서비스로 바꿔 생각해본다면 점원이 중간에 바뀌면 서비스장애가 발생하는 것임

다른점원에게 가면 context정보가 사라지는 것임

stateless에서는 점원에게 그때그때 필요한 모든 정보들을 넘김으로써 점원이 바뀌어도 서비스에 아무 이상이 없음

이 부분이 클라이언트 서버의 아키텍처에서 엄청난 확장성을 가질 수 있음

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2370b291-3089-4c17-b347-ed2fda7dbf32/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1f6b2396-95ba-46ec-bc9b-16ae6e2097b1/Untitled.png)

서버가 장애가 나면? 처음부터 다시 대화를 해야함

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1774fcb4-c3f2-4f88-8ebc-6e97430eddf8/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/98583295-a093-4c33-953d-c5b669959af6/Untitled.png)

예를들어 이벤트 페이지에서는 장비만 늘리면 되는 것임

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b4d902de-a6b4-4f82-bf81-ced7046962b0/Untitled.png)

stateless 단점 - 한번 보낼때 데이터를 너무 많이 보내야 함

## 비 연결성(connectionless)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ba1e67e6-4e63-4722-bc81-62176a51a1b5/Untitled.png)

연결성을 유지 하게되면 클라이언트가 아무 작업을 필요로 하지 않아도 연결을 유지해야하므로 서버 자원 소모가 크다

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3d74548a-21be-409a-935d-cb45768ae53e/Untitled.png)

필요한 것만 주고받고 연결을 끊어버림

서버 - 최소한의 자원을 유지할 수 있음

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/90e31766-f979-45e0-b7d0-50364fae47ae/Untitled.png)

비 연결성은 클라이언트가 요청 당시에만 서버측에서 응답을 하면 연결을 유지하지 않아 서버 자원을 효율적으로 사용할 수 있음

예를들어 구글이나 네이버의 경우 수천 명이 동시에 검색을 하고 있는게, 아니라 결과값이 나오면 한참 읽다가 다시 검색을 하기 때문에, 수천명이 사용해도 실제 초당 동시 처리하는 요청의 숫자는 매우 적다. 이럴 때, 비연결성으로 자원 절약을 할 수 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/717ce7c5-ea0b-4889-9298-a89e15a1388b/Untitled.png)

하지만 비연결성도 단점이 존재한다

만약 새로 검색을 하게되면 매번 연결(3way hand shaking)을 맺어야 함

이를 해결하기 위해 지속연결을 사용함

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b361f63d-2fb3-4ccd-bfcd-3ae1adddc8c7/Untitled.png)

지속연결

일반적으로 연결을 몇 십 초 정도 유지한거나 하는 내부 매커니즘이 있다. 이러면, 연결이 유지되는 동안, 새로운 요청을 할 때마다 더 빠르게 응답을 받을 수있어서 더 좋은 UX를 제공한다.

## HTTP 메세지

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1c238ca3-467f-4a12-8b18-779841ddc887/Untitled.png)

지금은 HTTP 시대!!

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cb2f8e12-a1e5-48ec-b85a-2234bd09f642/Untitled.png)

요청 메세지와 응답 메세지는 구조가 다름

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0201b7e1-782a-430e-b6a3-78a349eda7ca/Untitled.png)

HTTP메세지는

오른쪽과 같은 구조를 가짐

시작라인, 헤더, 공백라인, 메세지 바디

예를들어 구글에 hello를 검색한다면 위와 같은 형태

요청메세지의 시작라인 → GET/패스/http 버전

메세지 바디가 없다면 공백으로 보냄

응답메세지도 위와 같은 형태

100 조건응답

300 redirect 개발자 의도대로 되돌아 가는 것



![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e0272134-22a7-434a-90db-57c9ceb52711/Untitled.png)

요청메세지의 시작라인

시작라인은 크게 request line / status line으로 구분됨

요청 메세지는 request line 임 아래 3가지가 들어감

method(get,post,delete, put등), request-target(path패스), http 버전

**요청 메세지**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ef88f5c7-9a9e-4d7c-aac2-1519bbca3ab5/Untitled.png)

http 메서드

get - 서버에게 리소스 요청

post - 리스소 처리 요청

delete - 삭제

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/05ff5b40-80c5-462f-9dd5-79ca1a8b2fac/Untitled.png)

search - 무언가를 찾는 것이구나

파라미터로 q - hello이네 ? 이는 검색 대상이 hello 인 것(구글에서 정함) hl- 한글이네 ? 한글로된 글들을 검색하여 반환

절대경로로 시작한다 정도로만 알고있자

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7a9c263d-a5e4-492a-a9dd-c79b98215344/Untitled.png)

http 버전

**응답 메세지**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c70d97c2-faca-4c7a-a5ef-44c1de6452b0/Untitled.png)

응답 메세지

http 버전, http 상태코드, 이유문구

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d2354471-7698-41d0-834d-98455c6925df/Untitled.png)

http 헤더의 용도

http 전송에 필요한 모든 부가정보가 들어가 있음

예) 메세지 바디의 내용(어떤것으로 구성되어있는지html/xml), 메세지 바디의 크기, 압축, 인증, 요청 클라이언트(chrome 등)의 정보 등

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c0898545-edd8-4604-8f59-d36a74644242/Untitled.png)

byte로 표현 가능한 모든 데이터

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7cfc479e-2c45-48bb-9043-86480b0fb06e/Untitled.png)

HTTP 메세지 구조 - 시작줄, 헤더, 바디