# 2주차 REST API

REST API 말고도

\


SOAP ,GraphQL 를 사용할 수 있다

\


(나는 SOAP 방식 썻던 기억이 난다..xml의 지옥을 경험했었다… SOAP 로 만들어진 모듈과 api 통신하기 위해서 나도 SOAP 방식으로 불러왔었기 떄문에..)

GrapQL 은?

\


Servlet , Boot ,Spring Web , impeded tomcat(Spring Boot 안에 내장된 톰캣)

\


API (Application Programming Interface)

\


항상 입에 달고다니는 말이지만.. 그래서 이게뭔데 ?? 라고하면 몇초정도 침묵이 됬던것 같다.

\


캡슐화 > 인터페이스 안에 숨긴다 라고 생각을 하자(캡슐안에 숨긴다)

\


정보은닉 > 벽을 쳐서 가린다

\


로이필딩 형님…(이라고 최찍시간에 들었던거같..다)

\


Rest api

\


1️⃣ Starting with the Null Style

2️⃣ Client-Server

3️⃣ Stateless

4️⃣ Cache

5️⃣ Uniform Interface → 핵심!

\


핵심적인걸 uniform Interface를 사용한다

\


훨씬 심플하고 가시적이다.

\


구현은 ? Decoupled 된다. > 분리가 된다 > 독립적으로 발전 가능

\


대신 trade off 가 된다. 이부분은 효율성이 떨어질 수 있다. Standard form을 쓰고있기 때문에

\


대규모 데이터를 전달하는데 효과적인데, 일반적으로 사용할때 효과적이나 , 특수하게 사용할땐 비효율적일수도 있다.

\


4가지 인터페이스의 제약 (로이 필딩 제약)

HATEOSA (헤이토오사?)

\


REST 를 얘기할때 필딩 제약을 지켜야한다. 하지만 대부분 다 따르진 않음 ㅋㅋ;

\


리소스란게 내가 생각하는거랑 쪼끔은 다른거같기도하고..\


\*\* 추가 내용

Naver D2 유튜브를 보면서 내용 이 재미있어서 추가적으로 정리하였음

실제로 사용하는 REST API 와 로이필딩이 얘기한 REST API 가 너\~무 다르다

REST 는 우선 아키텍쳐 스타일 아키텍쳐 스타일은 제약조건의 집합이기에 모두 따라야 하는게 맞다

하지만 하이브리드 아키텍쳐 스타일임

Starting with the Null Style

Client-Server

Stateless

Cache

Uniform Interface

> > 보통 이걸 잘 못 지킨다

self-descripvtive messages

> > 보통 이메시지를 보면 API 전체를 알아야한다 하지만 현재 그렇지 않음

HATEOAS 항상 HYPERLINK 여야한다. 보통 html의 a태그를 이용하면 정상적으로 됨 json으로 표현하려면 Link 라는 태그를 사용해야한다.

이 두가지를 거의 못지키고 있음

왜 Uniform Interface 를 지켜야하냐

독립적 진화를 하기위해서

독립적 진화란 서버와 클라이언트가 각각 독립적으로 진화한다. \*\* 중요 > 서버의 기능이 변경되어도 클라이언트를 업데이트 할 필요가 없다.

웹에서 지키는 REST

웹페이지가 변경되었다고 웹 브라우저를 업데이트할 필요는 없다. 웹 브라우저를 업데이트했다고 웹 페이지를 변경할 필요가 없다. HTTP , HTML 명세가 변경되어도 웹은 잘 동작한다.

사례1. 현재 상용중인 모바일 웹애플리케이션이 예전 모델(갤럭시 s3)로 동작해서 브라우저를 사용하였는데 UI가 깨지거나 이럴수 있지만 기능적인 동작은 할수 있다.

상호운용성(interoperability) 에 대한 집착 Referer 오타지만 안고침 charset 잘못 지은 이름이지만 안 고침 HTTP 상태코드 416 포기함(i'm a teapot) HTTP/0.9 아직도 지원함(크롬,파이어폭스)
