# Annotation
---
## 대표적인 어노테이션
---
### @RequestHeader
`Request의 header값을 가져올 수 있으며`, 해당 Annotation을 쓴 메소드의 파라미터에 사용한다
```java
@Controller                   // 이 Class는 Controller 역할을 합니다
@RequestMapping("/user")      // 이 Class는 /user로 들어오는 요청을 모두 처리합니다.
public class UserController {
    @RequestMapping(method = RequestMethod.GET)
    public String getUser(@RequestHeader(value="Accept-Language") String acceptLanguage) {
        //  GET method, /user 요청을 처리
    }
}
```
---

### @RequestParam
`URL에 전달되는 파라미터를 메소드의 인자에 매칭`시켜, 파라미터를 받아서 처리할 수 있는 Annotation으로 아래와 같이 사용한다 JSON 형식의 Body를 MessageConverter를 통해 Java 객체로 변환시킨다
```java
@Controller                   // 이 Class는 Controller 역할을 합니다
@RequestMapping("/user")      // 이 Class는 /user로 들어오는 요청을 모두 처리합니다.
public class UserController {
    @RequestMapping(method = RequestMethod.GET)
    public String getUser(@RequestParam String nickname, @RequestParam(name="old") String age {
        // GET method, /user 요청을 처리
        // https://naver.com?nickname=dog&old=10
        String sub = nickname + "_" + age;
        ...
    }
}
```
---
### @RequestBody
`Body에 전달되는 데이터를 메소드의 인자와 매칭시켜, 데이터를 받아서 처리`할 수 있는 Annotation으로 아래와 같이 사용한다 클라이언트가 보내는 `HTTP 요청 본문(JSON 및 XML 등)을 Java 오브젝트`로 변환한다

클라이언트가 body에 json or xml 과 같은 형태로 형태값(주로 객체)를 전송하면, 해당 내용을 Java Object로 변환한다
```java
@Controller                   // 이 Class는 Controller 역할을 합니다
@RequestMapping("/user")      // 이 Class는 /user로 들어오는 요청을 모두 처리합니다.
public class UserController {
    @RequestMapping(method = RequestMethod.POST)
    public String addUser(@RequestBody User user) {
        //  POST method, /user 요청을 처리
        String sub_name = user.name;
        String sub_old = user.old;
    }
}
```
---
### @RequestMapping
`@RequestMapping(value="")와 같은 형태로 작성`하며, `요청 들어온 URI의 요청과 Annotation value 값이 일치하면 해당 클래스나 메소드가 실행`된다 Controller 객체 안의 메서드와 클래스에 적용 가능하다

- Class 단위에 사용하면 하위 메소드에 모두 적용된다
- 메소드에 적용되면 해당 메소드에서 지정한 방식으로 URI를 처리한다
```JAVA
@Controller                   // 이 Class는 Controller 역할을 합니다
@RequestMapping("/user")      // 이 Class는 /user로 들어오는 요청을 모두 처리합니다.
public class UserController {
    @RequestMapping(method = RequestMethod.GET)
    public String getUser(Model model) {
        //  GET method, /user 요청을 처리
    }
    @RequestMapping(method = RequestMethod.POST)
    public String addUser(Model model) {
        //  POST method, /user 요청을 처리
    }
    @RequestMapping(value = "/info", method = RequestMethod.GET)
    public String addUser(Model model) {
        //  GET method, /user/info 요청을 처리
    }
}
```

spring 4.3부터 Spring MVC Controller Method를 위한 어노테이션이 추가되었는데 각각의 어노테이션들은 HttpMethods에 매칭되며, method단에서 사용 가능하다
- @PostMapping
```java
@Controller                   // 이 Class는 Controller 역할을 합니다
@RequestMapping("/user")      // 이 Class는 /user로 들어오는 요청을 모두 처리합니다.
public class UserController {
    @RequestMapping(method = RequestMethod.POST)
    public String addUser(Model model) {
        //  POST method, /user 요청을 처리
    }

    ////////////////////////////////////
    // 위와 아래 메소드는 동일하게 동작합니다. //
    ////////////////////////////////////

    @PostMapping('/')
    public String addUser(Model model) {
        //  POST method, /user 요청을 처리
    }
}
```
- @GetMapping
```java
@Controller
@RequestMapping("/user")
public class UserController{
    @GetMapping("/")
    Public String getUser(Model model){
        // GET method, /user 요청을 처리
    }

    // 위와 아래 메소드는 동일하게 동작한다

    @RequestMapping(method = RequestMethod.GET)
    public String getUser(Model model){
        // GET mothod, /user 요청을 처리
    }
}
```
- @PutMapping
- @DeleteMapping
- @PatchMapping

---
### @SpringBootTest
Spring Boot Test에 필요한 의존성을 제공해준다
```java
// DemoApplicationTests.java
package com.example.demo;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class DemoApplicationTests {

	@Test
	void contextLoads() {

	}

}
```
### @TEST
Junit에서 테스트 할 대상을 표시한다

---