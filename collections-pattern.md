# Collections Pattern

Collections

\


Collections을 쓰는경우

/posts > 모든 게시물을 하나의 URI로 표현(게시물 목록으로 활용 가능)  . 일반적으로 단어의 복수형으로 사용함.

/posts/1-the-first >> 첫번쨰

/posts/2-test >> 두번째

/postst/{id} 또는 /posts/:id 등으로 사용할 수 있다. (나는 :id 는 써본적 없음)&#x20;

\


Post ID 는 리로스 ID 가 아님에 주의

Resource Id = URI = URL&#x20;

Post ID = Resource ID 를 구성하는 요소 중 하나. Posts 그룹 내 식별자(ID >> 보통 db 의 seq 같은걸 많이썼었음.)

\


그룹명은 복수형으로 쓰기 때문에 collection(items) 이 아니라 element(item)을 지정할 때도 복수형이 쓰인다는 점에 주의해야한다.

/posts/1 > 복수형으로 그룹명을 지정하고, 그 아래에서 개별 아이템을 지정

/post/1 > 흔히 하는 실수. 반드시 복수형을 써야 하는건 아니지만, 배운티를 내자 (rest api에 대해 공부좀 했구나 할수있음 ㅋㅋㅋ)

일관된 형태로 쓸수 있기 때문에 보통 복수형을 씀

\


게시물에 댓글을 달리는 상황이라면, 디렉터리처럼 구성할 수 있다

/posts/{post\_id}/comments > Collection

&#x20; \> /comments?post\_id={post\_id} 형태로 써줘도 된다.

\


URI 만 보면 조금 다르게 느껴질 수 있지만, 구현하는 코드나 결과가 사실상 동의함.

“/posts/{post\_id}”/comments/{id} > 여기서의 id 는 댓글의 id 를 의미함  “”기준으로 한묶음씩 이라 생각하자

/comments/{id} 형태로 간단히 구성해도 되지만 . 이렇게 했을경우 어느 게시물의 댓글인지 알수가 없다. (삭제 등 간단한 작업 요청 상황이면 오히려 좋을 수 있음)

\


특정 게시물을 고치는 페이지를 표현하고 싶다면?

“/posts/{id}”/edit >> Edit Page 라는 리소스

/edit?post\_id={post\_id} 형태로 써줄 수 있지만 /comments/{id}/edit 같은게 도입될 경우 /edit?comment\_id={comment\_id}같은것과 구분해서 처리하는게 복잡할 수 있다.

\


REST API 는 페이지만 표현할일이 거의 없기 때문에 이런 표현은 F/E 에게 맡기고, 그냥 /items, /items/{id}같은 URL만 쓰도록 제약해도 무방하다.

\


다만 사용하는데 문제는 없지만 보통 이럴일이 없다.

\


그룹이 아닌 경우라면 단수형을 써도 된다.

/session 세션은 하나만 유지되고, 다른 세션을 참고할 일이 없으므로 단수형으로 써도 됨

/edit?blahblah > 위에서 언급한 케이스

만약 편집 페이지의 유형을 Edit ID 따위로 표현하고 싶다면

/edits/post, /edits/comment 같이 컬렉션 패턴과 복수형을 사용할 수 있다.

\-하지만 이렇게 표현할거면 그냥 page라는 리소스를 사용하는걸 추천

/pages/edit-post

/pages/edit-comment 같이 훨씬 자연스럽게 표현할 수 있게 된다.

강의 교재 페이지도 document로 사용되고 있음 (복수형은 아니지만)

\


* 이걸 좀 더 숙련해서 표현할 수 있도록 훈련하는게 중요할 것 같다!
