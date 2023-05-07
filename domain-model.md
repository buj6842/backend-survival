# Domain Model

Application & domains level

\


사용자 인터페이스

\


응용

\


도메인

\


인프라 스트럭쳐(웹 또는 db)

\


Application Layer

1\. 이 계층은 얇게 유지된다.

2\. 업무 규칙이나 지식이 포함되지 않으며

3\. 오직 작업을 조정하고

4\. 도메인 객체의 협력자에게 작업을 위임한다.

\


Domain Model 은 일반적인 객체. 무엇보다 “행위(behavior)” 가 중요하다. Unit Testing 하기 적합한 존재.

\


행위없이 코딩: (내가 다 파악해서 조작한다 = 협력이 아님 = 복잡성이 감소하지 않음)

\


Long amount = account.getAmount();

account.setAmount(amount+ 10\_000);

\>> set을 이용해 전체값에 10000을 더함

\


행위가 있다면? (내가 알게 뭐야 = 알아서 해 = 위임)

\


account.increateAmount(10\_000);

\>> increateAmount라는 메소드를통해 10000을 더함

\


DAO가 데이터를 관리한다면, Repository 는 도메인 모델을 관리한다. DAO >  DB 중심, Repository는 도메인 모델중심적이다.

\


예전 기술을 활용하는 조직이라면 ERD를 먼저 그리고 나서 DAO와 VO(DTO)를 사용하는 방식으로 개발을 진행할 거고(데이터베이스 주도 개발) >>> 현재 진행중인 프로젝트가 이런형식이다. 모든게 db 중심적으로

형성되어 있음

\


DDD를 극단적으로 따르는 조직이라면 도메인 모델을 먼저 만들고, JPA Entity를 따로 만들어서 도메인 모델과 매핑한다. (이전회사에서는 극단적으로 따르지는 않았지만 어느부분 비슷하게 진행했었다.)

\


전자는 DB가 바뀌면 프로그램이 바뀌고, 후자는 프로그램을 지원하기 위해 DB를 조정한다. 후자는 CQRS, Event Sourcing 등을 도입하거나 솔루션 자체를 변경하기 (어디까지나 상대적으로) 쉽다.

\


\


Post model을 만들어 PostRepository를 만드는 코딩 실습 진행

\


이중 핵심이될만한 부분

Post 모델의 클래스중 update 메소드

\


public void update(String title, MultiLineText content) {

&#x20;   //내가 고칠 수 있는지에 대한 권한 검사

&#x20;   //title 에 대한 유효성 검사

&#x20;   // 기타 등등 치명적인 무언가.. 이곳에서 확인할 수 있다 ! 안그러면 service에서 하기때문에

\


&#x20;   this.title = title;

&#x20;   this.content = content;

&#x20;   //Getter는 절대로 비즈니스 로직을 위해 쓰지 않는다.

}
