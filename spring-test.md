# Spring Test

Spring test (Integration Test) 통합 테스트

\


Spring 공식 문서는 테스트를 크게 둘로 구분한다.

* Unit Testing
* Integration Testing

\


Spring은 코드에 구조적으로 개입하는 게 적어서 단위테스트를 쉽게 작성할 수 있다.

\


Spring의 힘을 빌려서 테스트하는 건 IoC 컨테이너를 적극적으로 활용하고 싶거나, Spring Web MVC로 구현된 부분을 테스트하고 싶을 때, 즉 Spring에서 통합 테스트라고 부르는 경우다.

\


SpringBootTest

1.4버전부터 쓸수 있게되었음!

\


@SpringBootTest(webEnvironment = WebEnvironment.RANDOM\_PORT)

class PostFeatureTest {

@Value("${local.server.port}")

private int port;

@Autowired

private TestRestTemplate restTemplate;

@Test

public void post() {

String url = "http://localhost:" + port + "/posts";

PostDto postDto = new PostDto("ID", "새 글", "제곧내");

restTemplate.postForLocation(url, postDto);

String body = restTemplate.getForObject(url, String.class);

assertThat(body).contains("새 글");

assertThat(body).contains("제곧내");

String id = findLastId(body);

restTemplate.delete(url + "/" + id);

body = this.restTemplate.getForObject(url, String.class);

assertThat(body).doesNotContain("새 글");

}

private String findLastId(String body) {

Pattern pattern = Pattern.compile("\\"id\\":\\"(\[^\\"]+)\\"");

Matcher matcher = pattern.matcher(body);

String id = "";

while (matcher.find()) {

id = matcher.group(1);

}

return id;

}

}

\


MockMvc

MockMvc를 써서 HTTP 요청을 흉내낼 수 있다.&#x20;

\


(인코딩 문제가 났는데 사실 이건 스프링에서 해결했으면 했다는게 아샬의 개인적인 의견 ㅎㅎ)

흉내를 낸다 라고 표현은 했지만 실제로 응답이 왔다갔다 한것 처럼 보였던 점이 특징이였음.

\


@SpringBootTest

\*\*@AutoConfigureMockMvc\*\*

class PostControllerTest {

@Autowired

private MockMvc mockMvc;

@Autowired

private PostRepository postRepository;

@Test

public void list() throws Exception {

this.mockMvc.perform(get("/posts"))

.andExpect(status().isOk())

.andExpect(content().string(

containsString("테스트입니다")

));

}

@Test

public void create() throws Exception {

String json = """

{

"title": "새 글",

"content": "제곧내"

}

""";

int oldSize = postRepository.findAll().size();

this.mockMvc.perform(

post("/posts")

.contentType(MediaType.APPLICATION\_JSON)

.content(json)

)

.andExpect(status().isCreated());

int newSize = postRepository.findAll().size();

assertThat(newSize).isEqualTo(oldSize + 1);

}

}

\


Spy bean, mockBean 어렵고 만들기 어렵지만 어쨌든

전체적으로 해봐야한다는점..

\


사실 테스트부분은 좀 지루하기도 했지만 필수라 생각하고 몇번 더 해보면서 익혀야할것 같음..
