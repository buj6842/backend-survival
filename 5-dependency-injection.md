# 5주차 Dependency Injection

Dependency injection

\


Factory

\


객체를 직접 만들지 않고, 객체를 생성하는 책임만 가진 객체를 만들어서 쓴다.

\


Post 객체에서 예시를 들면

\


서비스 단에 post service에

내가 생성자로 만들고 싶지않고 factory에게 넘겨주고 싶다. 할때 사용을 할 수 있음

(Repository나..)

\


`public class Factory {`

\


&#x20;   `public static PostRepository PostRepository() {`

&#x20;       `return new PostRepository();`

&#x20;   `}`

`}`

\


`public class GetPostDtoListService {`

\


&#x20;   `private final PostRepository postRepository;`

\


&#x20;   `public GetPostDtoListService() {`

&#x20;       `postRepository = Factory.`_`PostRepository`_`();`

&#x20;   `}`

`}`

Pluggable (?)하다 라고 표현 하자

\> 생각해보니 나도 이렇게 querydsl에서 entitymanager 를 factory처럼 만들어서 썼었던 기억이있었다.

\


D I (Dependency injection)> 제어 반전, 제어의 역전, 역제거 등등 이런 말로 들었었음

종종 프레임워크의 특징 이라고 표현이 된다.

\


IOC 컨테이너와 DI 패턴에 대한 글에서의 특징

\


Spring 등이 EJB를 비판하면서 POJO,IoC 컨테이너를 이야기했었고, 이 논쟁을 끝내러 Marin Fowler가 새로운 용어를 제안함.

그것이 Dependency Injection!

\


예전에 스프링 개발자들이 Property 주입(setter Injection) 을 많이 썻지만(Java Bean의 흔적) , 최근에는 생성자 주입을 선호.

특히 final 필드로 만들어서 쓰는걸 강력하게 권장하고 있다.

(내가쓰는 프로젝트 모듈에서도 boot 모듈은 final로, 그냥 spring framework는 예전 개발자들이 만들어서 setter로 되어있던 것을 확인했다.)

우리 강의에선 final을 사용해서 주로쓰고있음!

\


BeanFactory

\


스프링이 관리하는 객체를 Bean이라고 함 (이거 처음배울때 직접 주입해주고 세팅해주고 했던기억남…) 대게는 Spring Bean 이라고 콕 짚어서 이야기한다.

\


JUnit을 이용해 작고 간단한 프로그램을 만들 수 있다. Spring Boot Test 에서 포함되어 있고(스프링 이니셜라이저로 만들면 기본 포함!)

각 테스트 메소드는 서로 독립적이란 점을 주의하자.

\


Application Context를 사용할때가 많지만

요즘은 Annotaion으로 처리한다.  전자가 진정한 POJO라고 말하지만, 후자가 너무 편하다.

\


Bean 은 config 에서 @Bean 애너테이션을 써서 정의를 하거나

@Component를 붙여주면 bean 주입이 된다

@Service 어노테이션 안에도 @Component가 있기때문에 달면 된다.

@ComponentScan을 사용해야 Scan이 된다.

\


스프링을 이용해서 쓰는건 쉽지만

이게 어떻게 돌아가는지 알기위해서 여러가지 실험을해보는게 도움이 될것!
