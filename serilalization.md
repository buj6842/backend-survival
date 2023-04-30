# Serilalization

Serilalization

완전히 캡슐화 하는데 있어서 어떻게 저장하느냐를 기술적으로 다룬다는걸 의미

객체를 그 자체로 DB에 저장하거나 네트워크로 전송하는건 불가능. (예시 코드로 Human이라는 class를 to string을 응용하지 않고서는 system.out.print(human)을 표현할 수 없었음) 객체를 복구할 수 있도록 데이터화하는게 필요함 바이너리 라면 Byte Stream, 텍스트라면 기계가 파싱할 수 있고 사람도 읽을 수 있는 형태를 XML, JSON 같은 형식이 인기

직렬화와 마샬링은 거의 같지만, Java에선 마샬링을 특수하게 다룸 (마샬링이라는 용어를 처음 들어보았다.)

```
- 직렬화 : 역직렬화를 통해 객체 또는 데이터의 복사본을 만들 수 있음.
- 마샬링 : 직렬화와 같거나, 원격 객체로 복원을 할 수 있음. 원격 객체의 경우 메서드 호출은 RPC(또는 RMI)가 됨. <-> 언마샬링
```

JSON (JavaScript Object Notation) >> 원어를 풀어서 본건 처음인것 같다. (feat.douglas crockford)

JavaScript로 유명한 douglas crockford. 사람이 읽기 쉽고, 기계도 해석 또는 생성하기 쉽다. 보안 문제만 없다면 JavaScript에서 그대로 사용하는 것도 가능하지만, 대부분 JSON.parse(역직렬화)와 JSON.stringify(직렬화) (>> 이두가지는 js에서 많이 사용해봄)로 안전하게 사용한다.

가장 기본적으로 key-value 쌍이다. (array도 제한된 key-value = length 관리에 불과하다) Java는 Map이 비슷하지만(1주차 과제에서 Map으로 Json으로 바꿨었던 기억이있다), 스키마 관리 및 다입 안정성을 위해 DTO를 활용한다.

생성 : DTO(Java 세계관) > 변환기 > JSON 문자열 해석 : JSON문자열 > 변환기 > DTO(Java 세계관)

변환기는 무엇일까? Java에선 Jackson이란 도구가 유명하고, Spring boot Web 의존성을 추가하면 바로 사용할 수 있다(따로 dependency를 추가 안해도된다는점).

변환할 떄 getter 사용@JsonProperty 어노테이션으로 속성 이름(key)지정 가능. 다른 객체(DTO) 를 포함하고 있어도 됨.

Json 스키마로서의 DTO (class) >> F/E <-> B/E 사이에서 사용되는 부분이라 생각하자

DTO는 여러 곳에서 사용될 수 있고, 그 의미는 계속 확대됨. 예를 들어 Tier, 즉 Remote 통신이 아닌 상황인 Layer 사이나 내부 객체를 감춘 공개 인터페이스를 만들 때도 DTO를 활용. "데이터 전송"이기만 딱히 틀리지않다.

오늘 하는건 Json 스키마로서의 DTO에 대해서 얘기를 하는것이니 다른 상황에서도 사용할수 있단걸 생각해야한다.

dto라고 꼭 dto처럼 쓰지 않기때문에 JSON 스키마로서의 DTO 이렇게 얘기가 나왔다고 생각하자.
