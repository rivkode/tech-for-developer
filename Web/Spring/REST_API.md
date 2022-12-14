# REST API

> api 란 ?

응용 프로그램에서 사용할 수 있도록 다른 응용 프로그램을 제어할 수 있게 만든 인터페이스

api를 사용하면 내부 구현 로직을 알지 못해도 정의되어 있는 기능을 쉽게 사용할 수 있음

여기서 인터페이스란 어떤 장치간의 정보를 교환하기 위한 수단이나 방법

대표적으로 마우스, 키보드, 터치패드등이 있을 수 있음

> REST 란 ?

자원의 이름으로 구분하여 해당 자원의 상태를 교환하는 것을 의미

자원은 데이터임

REST는 서버와 클라이언트의 통신 방식 중 하나임

HTTP URI 를 통해 자원을 명시하고 HTTP Method를 통해 자원을 교환함

HTTP Method : Create, Read, Update, Delete

> REST 특징


서버, 클라이언트 구조

 - 자원이 있는 쪽이 서버, 요청하는 쪽이 클라이언트
 - 클라이언트와 서버가 독립적이어야 한다. (각 서버를 두고 교집합이 없어야 한다.)

Stateless
 - 요청에서 클라이언트의 정보를 서버는 저장하지 않는다.

Cacheable
 - HTTP 프로토콜을 사용하므로 캐싱 기능을 적용

> REST 장점


HTTP 표준 프로토콜을 사용하는 플랫폼에서 호환 가능

서버와 클라이언트의 역할을 명확히 분리

여러 서비스 설계에서 생길 수 있는 문제 최소화

> RESTAPI 란 ?


REST 아키텍처의 조건을 준수하는 어플리케이션 프로그래밍 인터페이스를 의미

일반적으로 REST 아키텍처를 구현하는 웹 서비스를 RESTful 하다고 표현함

> REST API 설계 규칙


웹 기반의 REST API 를 설계할 경우에는 URI를 통해 자원을 표현해야 함

https://hipspot/place/23

Resource: place

Resource id: 23

자원에 대한 조작은 HTTP Method(CRUD)를 통해 표현해야 함

URI에 행위가 들어가면 안됨

Header를 통해 표현

메시지를 통한 리소스 조작

HTML, XML, JSON, TEXT가 있음
