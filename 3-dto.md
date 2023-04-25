# 3주차 DTO

DTO

FE는 사용자의 입력을 받아서 B/E에 요청, B/E는 요청을 처리 후 응답. 이 응답을 F/E는 사용자에게 적절한 형태로 보여주게 되고, 사용자는 다시 다른 입력을 하게 됨(반복)

우리는 JSON이란 포맷을 활용하려고 하고, Java에서는 DTO란 형태로 다룰것임.

엔터프라이즈 아키텍쳐의 설계에서 사용되는 조각이라 생각하자

Data Transfer Object 데이터 전송 객체

제약조건 안에서 목적이 있음.

between processes

remote interface, remote facade

processes 간에 통신과 remote 간에서 리소스가 큼

IPC Inter-Process Communication (프로세스 간 통신)

* 거칠게 이야기하면 서로 다른 프로그램이 통신
*
* File > 가장 기본적인 접근. 원격 환경에서 활용하기가 어렵다.
* Socket > 파일과 유사하게 읽고 쓸 수 있지만, 원격 환경에서도 활용할 수 있다. (1주차에서 진행했었음)
  * HTTP 같은 고수준 프로토콜을 활용하면 어느정도 정해진 틀이 잇기 때문에 상대적으로 쉬워짐.
  * REST를 활용하면 RPC(SOAP의 일반적인 활용)이 아닌 Resource에 대한 CRUD 로 정리해야함.(2주차에서 진행햇던 내용)

DTO

* 단순하게 보면 setter, getter로 이뤄짐
* JavaBeans에서 유래한 Java Bean 또는 그냥 Bean이라 부르는 형태에 가까움(Spring Bean, POJO와 다른걸 주의하자)
* 제대로 된 객체가 아니라 그냥 무기력한 데이터 덩어리. C/C++ 등에선 구조체로 구분할 수있지만 Java에선 불가능 최신 Java에선 record를 활용할 수 있지만, 오래된 Bean관련 라이브러리에선 지원하지 않음

> > 자바 15버전부터 들어왔었고 17버전에 확정된걸로 알고있음 (아직 사용해본적은 없음..)

Tier간 통신

* F/E와 B/E 사이 - 우리가 오늘 집중하려는 부분 - DTO 자체를 그대로 전송할 수는 없고, 직렬화(마샬링)을 통해야 한다. - 어떤 직렬화 기술을 사용할 건지도 결정해야 함 > 우리는 JSON 으로 사용할것(XML도 있지만 이건 사용하진않음)
*   B/E 와 DB 사이 - 아주 옛날에는 Value Object 에선 DTO 란 의미로 썻지만 Transfer Object라고 정정했음 아직도 오래된 SI기업에선 VO(Value Object)를 DTO란 의미로 사용(현재 내 프로젝트에선 실제로 VO로 사용하고있음..)

    <pre><code><strong>  - JPA를 지양하고 DDD를 따르는 사람 중 일부는 ORM(JPA, 하이버네트)는 Active Record > DTO 처럼 접근
    </strong>  - 아샬은 Kotlin과 Expoesed를 쓸 때도 이렇게 접근함 (나도 지금 하고있는 kotlin프로젝트를 사용할때 해보자)
      
      DDD란 Domain Driven Design 
      > 비즈니스 Domain별로 설계하는 방식이라 생각하자.
    </code></pre>
