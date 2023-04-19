# Spring Web Mvc

목표 : Spring Web Mvc를 통한 http server를 만들어보자



아직은 Spring 문서에서 핵심을 캐치하진 못했다.. 괴롭...



spring 페이지에서 필요 요소를 선택 하고 프로젝트 구조를 잡았다.



spring devtools > 변경점이 있으면 자동으로 빌드를 해준다 . 상당이 편했더것 같음.



예제코드 Controller

```
package com.parrot.http.server.controllers;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class WelcomeController {
    @GetMapping("/")
    public String home() {
        return "Hello, world!";
    }

    @GetMapping("/hi")
    public String hi() {
        return "hi, world!";
    }
}
```



사실 코드를 치는시간보단 이전강의들을 통해 나름 번거롭게 만들었던걸 스프링에서 편하게 세팅을 해두었다는 점을 깨달은것 같다.

정말 괴롭더라도 우선은 Spring의 핵심을 체크할수있도록 잘 읽어봐야 될것 같다.

