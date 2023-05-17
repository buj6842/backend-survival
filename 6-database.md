# 6주차  Database

구조화된 정보 or 데이터의 조직화 된 모음

\


사용자 DB 라고 하면 사용자 정보가 쌓여있는걸 의미하지만, 개발하면서 DB라고 하면 사실은 DBMS를 의미할 때가 많다!

\


DBMS (database management System)

\


간단하게는 db 관리 시스템

\


응용 프로그램은 데이터베이스에서 데이터를 쉽게 찾을 수 있어야 하고, 효율적으로 조작(추가,수정,삭제) 할 수 있어야 한다.

또한 접근 권한, 보안 문제를 다룰 수 있어야한다. 즉, ‘데이터베이스를 관리하는 시스템’이 필요하다.

\


요새 인기있는건 RDBMS(Relational database management system)다.&#x20;

Mysql,maria db, postgresql, ms sql server, oracle 등이 여기에 속한다. 즉 일반적으로 DB라고 부르고 DBMS,&#x20;

그 중에서도 RDBMS를 의미할 때가 많다.

\


DBMS는 데이터베이스 언어를 제공한다.

\


1.DDL (data definition langauage) > Schema.  >> 평소에 가장 자주 보이는 단어이다

2.DML (data manipulation language) > query & command >> 평소에 많이쓰이고

3.DCL (data control language ) > grant, revoke, commit, rollback

\


Schema 를 강조하기 위해 ddl 이란 표현을 자주 사용한다.

SQL은 사실 SEQUEL이 이름을 바꾼 것 !!!!!

\


Data Model

\


크게 3가지로 나뉘게된다.

\


1. Conceptual Data Model
2. Logical Data Model
3. Physical Data Model

\


일반적으로 데이터 모델을 구분한다고 하면 이들을 다시 세분화한 모델 (특히 논리적 데이터 모델)의 유형을 다룬다.

\


Relation Model 관계형 모델

\


가장 인기 있는 논리적 데이터 모델. 다른 논리적 데이터 모델로 Hierarchial , Network, Object-based Model이 있다.

\


많은 사람들이 ERM (Entity-Relationship Model) 과 RM (Relational Model)을 구분하지 못 한다. ERM은 RelationShip은 Entity 사이의 관계를 의미

RM 의 Relational은 Tuple의 집합 (거칠게 말하면 Table) 을 의미한다.

굳이따지면 락과 락스처럼 상관없는 용어라고 생각하자

맥락이 다르다.

\


Account -> 사용자 계정으로 쓰이지만 계좌 라고 쓰이는것 처럼.

\


관계형 모델에 쓰이는 3개의 개념을 정확히 이해해야 한다.

\


1.Relation

2.Tuple

3.Attribute
