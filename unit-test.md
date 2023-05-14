# Unit Test



\


V-Model

\


우리가 프로그래밍을 하는 이유 ! 문제(특히나 비즈니스 문제)를 해결하기 위해서

\


문제가 잘 해결 됐는지 어떻게 확신할 수 있을까? 문제를 잘 정의하고, 문제가 해결된 모습을 미리 그려보면 절반 정도는 확신할 수 있게 된다.

뒤로 돌아갈 수 없는 폭포수 모델은 현실에 부합하지 않지만, 폭포수 모델이 다루는 단계 들은 매우 유용하다.

V 모델은 각 단계에 대한 테스트를 나누고, 처음부터 어떻게 테스트해야 하는지 결정하려고 노력한다.

1. 요구사항 분석 → 사용자 중심 ⇒ 인수 테스트
2. 시스템 설계 → 시스템 사양 결정 ⇒ 시스템 테스트
3. 아키텍처 설계 → 고수준 설계 ⇒ 통합 테스트
4. 모듈 설계 → 저수준 설계 ⇒ 단위 테스트
5. 구현 → 코딩

\


각 단계의 끝부분 테스트를 활용해서 다음단계의 설계에 도움을 준다고 생각하자.

\


Test Matrix

\


품질에 대해서 두가지로 나뉜다 내부품질과 외부품질

\


소프트가 제대로 만들어졌는지 >> 일반적으로 말하는 품질 >> 외적 품질

내부적으로 (코딩적으로) 제대로 만들어졌는지? >> 눈에 보이지않는 품질 >> 내적품질

\


내적품질을 자주 놓치는건 눈에 잘 안보이기 때문에

Ex: 맛만좋고 주방이 깨끗할 필요가 있냐고 항변하는 식당, 어떻게든 수술만 잘하면 되지 손을 씻을 필요가 있냐고 항변하는 의사.

\


개발자 테스트라는 개념도 사용한다.

\


JUnit 5 (Unit Test)

\


SUnit -> XUnit

\


JUnit은 자동화된 테스트를 지원하는 도구. 이름에 Unit이 들어가지만 단위 테스트만 지원하는 건 아님. 통합 테스트, 심지어는 E2E 테스트를 작성하는데도 사용한다.

단위 테스트의 관점에서 질문을 던져보자:

* 믿고 쓸 수 있는 부품인가?
* 믿을 수 있는 부품이 있다면 어떻게 하면 되는가?

\


SICP 1.1.7 Newton’s Method 예제

[Example: Square Roots by Newton's Method](https://mitp-content-server.mit.edu/books/content/sectbyfn/books\_pres\_0/6515/sicp.zip/full-text/book/book-Z-H-10.html#%25\_sec\_1.1.7)

맨 처음에는 몇 가지 부품이 있다고 가정하고 코드를 작성함.

(define (sqrt-iter guess x)

(if (\*\*good-enough?\*\* guess x)

guess

(sqrt-iter (\*\*improve\*\* guess x)

x)))

\


Java로 옮기면 이렇게 된다.

public double sqrtIter(double guess, double x) { if (goodEnough(guess, x)) { return guess; } return sqrtIter(improve(guess, x), x); }

\


올바른 goodEnough 와 improve 만 주어진다면, 코드의 대부분의 경우에는 문제가 없을 것이다.

\


\
