# Relational Algebra

연산

\


하나 이상의 Relation으로 새로운 Relation을 만들 수 있다.

산술 연산의 경우 1 + 2 같은 산술 표현식으로 1과 2라는 두 개의 정수의 덧셈 연산을 표현할 수 있고, 이를 계산(평가)하면 3이라는 새로운 정수를 얻을 수 있다. Relation도 마찬가지로 여러 연산을 통해 새로운 Relation을 얻을 수 있다.

* 단항 연산: Selection, Projection, Rename, …
* 이항 연산: Cartesian Product, Set Union, Set Difference, …

여기서는 대표적인 연산 몇 가지만 알아보자.

\


Projection

원하는 Attribute을 포함하는 Pair로 Tuple을 구성.

\


SQL에선 SELECT절 바로 뒤에 속성 이름을 나열하는 방식으로 표현할 수 있다.

\


보통 sql 문을 대문자로, type은 소문자로 구분 (보통은… 아닌경우도있으니)

\


SELECT name, age, gender >> 타입을 select

FROM people;

\>> 이걸 Projection 이라고 부를 수 있음.

\


이렇게 나오는 결과를 새로운 Relation을 만들었다 라고 표현을 할 수 있다.

\


특별히 속성을 제한하고 싶지 않다면 그냥 와일드카드(\*)를 쓰면 된다.

SELECT \*

FROM people;

\


Projection ? 이거 querydsl 에서 사용할 때 썼었는데 이 단어의 뜻을 이제서야 알게된 느낌;;;;

\


Selection

주어진 술어(거칠게 말하면 “조건”)를 만족하는 Tuple만 선택.

SQL에선 SELECT문의 WHERE절로 술어를 표현할 수 있다.

\


SELECT name, age, gender

FROM people

WHERE age < 13;

\


Where 절은 그냥 if 문이랑 똑같다고 생각하면 된다.

\


Cartesian Product

\


Relation의 Cartesian Product는 원래 의미와 다르다. 원래는 각 요소의 쌍을 요소로 취하지만(x와 y가 있다면 (x, y)를 새로운 요소로 사용)

관계 대수에서는 그냥 Tuple을 합친다.

SQL에선 그냥 FROM 뒤에 관계(SQL에선 Table) 이름을 나열하면 된다.

(듣다보니 jpa를 쓸 때 카테시안의 곱 문제 라는 부분을 들어본 적이있어서 뭔가 친숙한 단어들 인 것 같다).

\


SELECT \*

FROM r1, r2;

\


대부분은 Cartesian Product를 그대로 사용하지 않고 Selection과 함께 사용하는데, 이를 Join이라고 한다.

\


견우, 직녀 등 사람을 다루는 관계 people이 있고, 각 사람이 소유한 물건을 다루는 관계 items가 있을 때, 사람의 이름(name)을 키로 사용한다면 다음과 같이 표현할 수 있다.

_σpeople.name = items.person\_name(people × items)_ σ = Selection × = Cartesian Product

\


SQL로 표현하면 다음과 같다. 속성 이름이 겹칠 경우엔 관계(SQL에선 Table) 이름과 마침표를 써서 특정해줄 수 있다. 속성 이름을 바꿔주기 위해 AS도 함께 써주자.

\


SELECT people.name, age, gender, items.name AS item\_name, usage

FROM people, items

WHERE people.name = items.person\_name;

\


SQL에선 SELECT와 WHERE로 표현할 수도 있지만, JOIN을 쓰면 편하다.

\


SELECT people.name, age, gender, items.name AS item\_name, usage

FROM people

JOIN items ON people.name = items.person\_name;

\


아무 것도 소유하지 않은 사람을 포함시키고 싶다면 OUTER JOIN을 사용하면 된다.

SELECT people.name, age, gender, items.name AS item\_name, usage

FROM people

LEFT OUTER JOIN items ON people.name = items.person\_name;

\


없는 곳은 NULL로 처리됨(그래서 예전에 프로젝트때 seq쪽이 null인 부분으로 나와서 해당부분을 처리한 적이 있었음)

\


\


누구도 소유하지 않은 아이템을 포함시키고 싶다면 LEFT 대신 RIGHT를 쓰면 된다. 하지만 이렇게 쓰지 않는 걸 추천한다(SELECT - FROM items로 아이템에 방점을 찍는 게 더 낫다).

SELECT people.name, age, gender, items.name AS item\_name, usage

FROM people

RIGHT OUTER JOIN items ON people.name = items.person\_name;

\


실제로는 사람이 아니라 아이템에 방점이 찍히는 경우가 대부분이라 그냥 조인도 다음과 같이 쓸 때가 많다.

SELECT items.name AS name, usage, people.gender

FROM items

JOIN people ON items.person\_name = people.name;

\


좀 더 무게를 두는곳에 따라서 JOIN쪽이 달라진다는점.

아샬 말대로 JOIN을 그냥 썻었는데 어떻게 구성되는지 뜯어본것같음.
