# Data Access

Data Access

List로 데이터를 받으면 하나씩 받아와야 하니 Map으로 받고싶다.

Presentation > Domain > Data

여러 데이터를 관리하는 방법은 하나가 아님

List,Map

DAO 를 사용하자

Dao 에서 methods를 이용해서 service단에 정리해주었음.

public class PostADO {

```
private final List<PostDto> postDtos;

public PostDAO() {
	this.postDtos = new ArrayList();
	this.postDtos.add(new PostDto("1", "제목", "테스트입니다"));
	this.postDtos.add(new PostDto("2", "2등", "2등이다!"));
}

public List<PostDto> findAll() {
	return new ArrayList<>(postDtos);
}

public PostDto find (String id) [
	return postDtos.stream()
			.filter(post -> post.getId().equals(id))
			.findFirst()
			.orElseThrow(PostNotFound::new);
}

public PostDto createPost(Postdto postDto) {


	Sting id = TsidCreator.getTsid().toString();
	
	PostDto newPostDto = new PostDto();
	newPostDto.setId(id);
	newPostDto.setTitle(postDto.getTitle());
	newPostDto.setContent(postDto.getContent());
	
	postDAO.save(newPostDto);
	
	return newPostDto;
	
	>> 이부분이 collection과 뭐가다르냐 할수 있음
	
}

public PostDto delete (String id) {
	//이상태는 효율적이지 않음 찾는기능을 사용하기 때문
	PostDto postDto = postDAO.find(id);
	postDtos.remove();

	return postDto;
}
```

}

public class PostMapDAO extends PostDAO { private Map\<String, PostDto> postDtos;

```
public PostMapDAO() {
	this.postDtos = new new HashMap<>();
	this.postDtos.put(new PostDto("1", "제목", "테스트입니다"));
	this.postDtos.put(new PostDto("2", "2등", "2등이다!"));
}

@Override
	public List<PostDto> findAll() {
	//id 순서대로 나오지는 않을것임
	return new ArrayList<>(postDtos);
}

@Override
public PostDto find (String id) [
	PostDto postDto = postDtos.get(id);
	if (postDto == null) {
		throw new PostNotFound();
	}
	return postDto;
}

@Override
public void save(Postdto postDto) {
	postDtos.put(postDto.getId(), postDto);
}

@Override
public PostDto delete (String id) {
	postDtos.remove(id);
}

```

}

공통된 목록만 다루기 때문에 PostDAO 를 interFace로 변경하였고 method별로 PostListDAO , PostMapDAO 별로 상속받아 각각의 상황에 맞게 구현하였음.
