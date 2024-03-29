# Spring MVC

---

# servlet

## 서블릿
특징

Servelt이 해주는 것들
- 비즈니스 로직을 제외한 모든것들

- 원래는 아래 줄이 그어져 있는 부분을 다 만들어야 한다.
- 하지만 서블릿이 이를 대신 수행하여 준다.
- 우리는 그것을 잘 사용하면 되는 것이다.


![image](https://user-images.githubusercontent.com/109144975/224255805-12a45f7a-4e31-492b-a36f-b91fdc2c9bd0.png)

localhost:8080/hello 로 접속하게되면 service 코드가 실행이 되게 된다.

서비스 로직에 request, response 파라미터 2개가 있는데 이는

- HTTP 요청 정보를 편리하게 사용할 수 있는 HttpServletRequest
- HTTP 응답 정보를 편리하게 제공할 수 있는 HttpServletResponse
- 개발자는 HTTP 스펙을 매우 편리하게 사용하게 해준다.
- 스펙을 다 직접 만들지 않아도 되고, 객체로 쉽게 다룰 수 있기 때문이다.

예를 들어 request.getUsername 하면 값을 얻을 수 있음

큰 그림으로 예시

- localhost:8080/hello 로 요청하게 되면
- HTTP 요청 메시지를 기반으로 request, response 메시지를 만듦
- HelloServlet을 실행시킴
- HelloServlet이 종료되면 response 객체 정보로 HTTP 응답 메시지를 만듦
- 그리고 웹 브라우저에 응답 메시지를 전달 함


![image](https://user-images.githubusercontent.com/109144975/224258032-248dc5de-70cb-4c6d-9611-92925f7bef50.png)

## 서블릿
HTTP 요청, 응답 흐름
- HTTP 요청시
- WAS는 Request, Response 객체를 새로 만들어서 서블릿 객체 호출
- 개발자는 Request 객체에서 HTTP 요청 정보를 편리하게 꺼내서 사용
- 개발자는 Response 객체에 HTTP 응답 정보를 편리하게 입력
- WAS는 Response 객체에 담겨있는 내용으로 HTTP 응답 정보를 생성

## 서블릿 컨테이너

- 서블릿 객체는 개발자가 직접 생성하는 것이 절대 아니다.
- 서블릿 객체는 서블릿 컨테이너가 자동으로 생성, 호출, 관리해준다.

![image](https://user-images.githubusercontent.com/109144975/224259087-29548de1-3c5d-4fff-a5bc-b2c58b75cf1d.png)

## 서블릿
서블릿 컨테이너

- 톰캣처럼 서블릿을 지원하는 WAS를 서블릿 컨테이너라고 함
- 서블릿 컨테이너는 서블릿 객체를 생성, 초기화, 호출, 종료하는 생명주기 관리
- 서블릿 객체는 싱글톤으로 관리 (싱글톤 : 객체를 하나만 생성, 그것을 공유해서 사용함)
    - 고객의 요청이 올 때 마다 계속 객체를 생성하는 것은 비효율
    - 최초 로딩 시점에 서블릿 객체를 미리 만들어두고 재활용
    - 모든 고객 요청은 동일한 서블릿 객체 인스턴스에 접근
    - **공유 변수 사용 주의**
    - 서블릿 컨테이너 종료시 함께 종료
- JSP도 서블릿으로 변환 되어서 사용
- **동시 요청을 위한 멀티 쓰레드 처리 지원**
    - 동시에 요청을 하더라도 WAS가 잘 해결해줌

helloServlet을 싱글톤으로 사용하는 이유는 ?
- HTTP request, response는 고객마다 다름, 따라서 HTTP 요청이 올땨마다 항상 새로 생성됨

helloServlet은 ?
- 재사용을 함, 동일한 객체를 사용하므로

## 동시 요청 - 멀티 쓰레드 - **정말 중요**

WAS의 servlet은 누가 호출할까 ? -> 쓰레드가 호출함

![image](https://user-images.githubusercontent.com/109144975/224260610-dcfb0fd6-3e20-4738-8ac9-65c6d29d3f20.png)

## 쓰레드
- 애플리케이션 코드를 하나하나 순차적으로 실행하는 것은 쓰레드
- 자바 메인 메서드를 처음 실행하면 main이라는 이름의 쓰레드가 실행
- 쓰레드가 없다면 자바 애플리케이션 실행이 불가능
- 쓰레드는 한번에 하나의 코드 라인만 수행
- 동시 처리가 필요하면 쓰레드를 추가로 생성

## 단일 요청 - 쓰레드 하나 사용

![image](https://user-images.githubusercontent.com/109144975/224261311-14261f00-d35c-4478-86b4-e8341038c3a6.png)

## 단일 요청 - 쓰레드 하나 사용

![image](https://user-images.githubusercontent.com/109144975/224261384-4c95c905-c3ac-4d53-bd3f-a06d21aa3795.png)

## 이후 쓰레드 휴식

## 다중 요청 - 쓰레드 하나 사용

servlet에 문제가 생겨 처리가 지연된다면 ?

![image](https://user-images.githubusercontent.com/109144975/224261715-c5a81037-b6d9-4846-bf66-5208a232f4ee.png)

이때 만약 다른 요청2가 들어온다면 ?

![image](https://user-images.githubusercontent.com/109144975/224261795-2e0dee3a-5d32-4246-8bd9-67127c9a34cc.png)

이렇게 되면 둘다 timeout 등으로 에러 발생

![image](https://user-images.githubusercontent.com/109144975/224261855-c450d5b5-94bd-44cf-8738-47619fd6e80f.png)

해결방법은 ?
- 요청마다 쓰레드를 생성하자

![image](https://user-images.githubusercontent.com/109144975/224262296-9a0069e0-02e4-46ae-960b-a51cacaaf8ad.png)


## 요청 마다 쓰레드 생성
장단점

- 장점
    - 동시 요청을 처리할 수 있다.
    - 리소스(CPU, 메모리)가 허용할 때 까지 처리가능
    - 하나의 쓰레드가 지연 되어도, 나머지 쓰레드는 정상 동작한다.
- 단점
    - 쓰레드는 생성 비용은 매우 비싸다.
        - 고객의 요청이 올 때 마다 쓰레드를 생성하면, 응답 속도가 늦어진다.
    - 쓰레드는 컨텍스트 스위칭 비용이 발생한다.
    - 쓰레드 생성에 제한이 없다.
        - 고객 요청이 너무 많이 오면, CPU, 메모리 임계점을 넘어서 서버가 죽을 수 있다


## 쓰레드 풀
- 풀 안에서 놀고있는 쓰레드 할당해주세요 - 쓰레드 요청
- 사용 후 쓰레드 풀에 다시 반납
- 생성하고 사용하고 버리는것이 아니라 다시 반납하는 시스템

![image](https://user-images.githubusercontent.com/109144975/224263508-0d53d6ef-195d-4ace-80eb-4aa8ff48c98c.png)

장점
- 쓰레드 풀보다 더 많은 요청이 왔을 때 나머지 요청들은 대기, 거절을 할 수 있다.

![image](https://user-images.githubusercontent.com/109144975/224263567-80bc15e7-b62f-431c-8a61-cd14b247a731.png)

## 쓰레드 풀
요청 마다 쓰레드 생성의 단점 보완

- 특징
    - 필요한 쓰레드를 쓰레드 풀에 보관하고 관리한다.
    - 쓰레드 풀에 생성 가능한 쓰레드의 최대치를 관리한다. 톰캣은 최대 200개 기본 설정 (변경 가능)
- 사용
    - 쓰레드가 필요하면, 이미 생성되어 있는 쓰레드를 쓰레드 풀에서 꺼내서 사용한다.
    - 사용을 종료하면 쓰레드 풀에 해당 쓰레드를 반납한다. (종료가 아님, 반납)
    - 최대 쓰레드가 모두 사용중이어서 쓰레드 풀에 쓰레드가 없으면?
        - 기다리는 요청은 거절하거나 특정 숫자만큼만 대기하도록 설정할 수 있다.
- 장점
    - 쓰레드가 미리 생성되어 있으므로, 쓰레드를 생성하고 종료하는 비용(CPU)이 절약되고, 응답 시간이 빠르다.
    - 생성 가능한 쓰레드의 최대치가 있으므로 너무 많은 요청이 들어와도 기존 요청은 안전하게 처리할 수 있다.


## 쓰레드 풀
실무 팁

- WAS의 주요 튜닝 포인트는 최대 쓰레드(max thread) 수이다.
- 이 값을 너무 낮게 설정하면?
    - 동시 요청이 많으면, 서버 리소스는 여유롭지만, 클라이언트는 금방 응답 지연
- 이 값을 너무 높게 설정하면?
    - 동시 요청이 많으면, CPU, 메모리 리소스 임계점 초과로 서버 다운
- 장애 발생시?
    - 클라우드면 일단 서버부터 늘리고, 이후에 튜닝
    - 클라우드가 아니면 열심히 튜닝


![image](https://user-images.githubusercontent.com/109144975/224264918-7d8193e9-cc1c-41e1-9f13-8a49125c585b.png)


## 쓰레드 풀
쓰레드 풀의 적정 숫자

- 적정 숫자는 어떻게 찾나요?
- 애플리케이션 로직의 복잡도, CPU, 메모리, IO 리소스 상황에 따라 모두 다름
- **성능 테스트** (나중에 해보자 !)
    - 최대한 실제 서비스와 유사하게 성능 테스트 시도
    - 툴: 아파치 ab, 제이미터, nGrinder



## WAS의 멀티 쓰레드 지원
핵심

- 멀티 쓰레드에 대한 부분은 WAS가 처리
- **개발자가 멀티 쓰레드 관련 코드를 신경쓰지 않아도 됨**
- 개발자는 마치 **싱글 쓰레드 프로그래밍을 하듯이 편리하게 소스 코드를 개발**
- 멀티 쓰레드 환경이므로 싱글톤 객체(서블릿, 스프링 빈)는 주의해서 사용

백엔드 개발자는 3가지를 고민해야함

- 정적리소스 어떻게 제공할지
- 동적으로 제공되는 HTML 페이지 어떻게 제공할지
- HTTP API 어떻게 제공할지


## 서버사이드 렌더링, 클라이언트 사이드 렌더링
- SSR - 서버 사이드 렌더링
    - HTML 최종 결과를 서버에서 만들어서 웹 브라우저에 전달
    - 주로 정적인 화면에 사용
    - 관련기술: JSP, 타임리프 -> 백엔드 개발자
- CSR - 클라이언트 사이드 렌더링
    - HTML 결과를 자바스크립트를 사용해 웹 브라우저에서 동적으로 생성해서 적용
    - 주로 동적인 화면에 사용, 웹 환경을 마치 앱 처럼 필요한 부분부분 변경할 수 있음
    - 예) 구글 지도, Gmail, 구글 캘린더
    - 관련기술: React, Vue.js -> 웹 프론트엔드 개발자
- 참고
    - React, Vue.js를 CSR + SSR 동시에 지원하는 웹 프레임워크도 있음
    - SSR을 사용하더라도, 자바스크립트를 사용해서 화면 일부를 동적으로 변경 가능

## 어디까지 알아야 하나요?
백엔드 개발자 입장에서 UI 기술

- 백엔드 - 서버 사이드 렌더링 기술
    - JSP, 타임리프
    - 화면이 정적이고, 복잡하지 않을 때 사용
    - 백엔드 개발자는 서버 사이드 렌더링 기술 학습 필수
- 웹 프론트엔드 - 클라이언트 사이드 렌더링 기술
    - React, Vue.js
    - 복잡하고 동적인 UI 사용
    - 웹 프론트엔드 개발자의 전문 분야
- 선택과 집중
    - 백엔드 개발자의 웹 프론트엔드 기술 학습은 옵션
    - 백엔드 개발자는 서버, DB, 인프라 등등 수 많은 백엔드 기술을 공부해야 한다.
    - 웹 프론트엔드도 깊이있게 잘 하려면 숙련에 오랜 시간이 필요하다.

## HttpServletRequest
HttpServletRequest 역할

- HTTP 요청 메시지를 개발자가 직접 파싱해서 사용해도 되지만, 매우 불편할 것이다.
- 서블릿은 개발자가 HTTP 요청 메시지를 편리하게 사용할 수 있도록 개발자 대신에 HTTP 요청 메시지를 파싱한다.
- 그 결과를 HttpServletRequest 객체에 담아서 제공한다.

- START LINE
    - HTTP 메소드
    - URL
    - 쿼리 스트링
    - 스키마, 프로토콜
- 헤더
    - 헤더 조회
- 바디
    - form 파라미터 형식 조회 (request.getParameter 등과 같은 방식으로 편리하게 읽을 수 있도록 함)
    - message body 데이터 직접 조회

임시 저장소 기능
- 해당 HTTP 요청이 시작부터 끝날 때 까지 유지되는 임시 저장소 기능
    - 저장: `request.setAttribute(name, value)`
    - 조회: `request.getAttribute(name)`

세션 관리 기능
- `request.getSession(create: true)`

**중요**
- HttpServletRequest, HttpServletResponse를 사용할 때 가장 중요한 점은 이 객체들이 HTTP 요청 메시지, HTTP 응답 메시지를 편리하게 사용하도록 도와주는 객체라는 점이다.
- 따라서 이 기능에 대해서 깊이있는 이해를 하려면 **HTTP 스펙이 제공하는 요청, 응답 메시지 자체를 이해**해야 한다


## HTTP 요청 데이터 - 개요
HTTP 요청 메시지를 통해 클라이언트에서 서버로 데이터를 전달하는 방법을 알아보자.

주로 다음 3가지 방법을 사용한다.

### GET - 쿼리 파라미터
- /url?username=hello&age=20
- 메시지 바디 없이, URL의 쿼리 파라미터에 데이터를 포함해서 전달
- 예) 검색, 필터, 페이징등에서 많이 사용하는 방식

### POST - HTML Form
- content-type: application/x-www-form-urlencoded
- 메시지 바디에 쿼리 파리미터 형식으로 전달 username=hello&age=20
- 예) 회원 가입, 상품 주문, HTML Form 사용

### HTTP message body에 데이터를 직접 담아서 요청
- HTTP API에서 주로 사용, JSON, XML, TEXT

데이터 형식은 주로 JSON 사용
- POST, PUT, PATCH

