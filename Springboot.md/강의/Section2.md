# Spring boot
---
## 스프링 웹 개발 기초
--- 
### 정적 컨텐츠
● 스프링 부트 정적 컨텐츠 기능   
● https://docs.spring.io/spring-boot/docs/current/reference/html/
``` html
<!DOCTYPE HTML>
<html>
<head>
    <title>static content</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
정적 컨텐츠 입니다.
</body>
</html>
```

**실행**   
● http://localhost:8080/hello-static.html    

정적 컨텐츠 이미지
![](https://velog.velcdn.com/images/gene028/post/33fb1460-1ad8-41ba-8e8e-b96e15816aee/image.png)   

---
### MVC와 템플릿 엔진
● MVC : Model, View, Controller   
*Controller*
``` java
@Controller
Public class HelloController{

    @GetMapping("hello-mvc")
    public String helloMvc(@RequestParam("name") String name, Model model){
        model.addAttribute("name", name);
        return "hello-template";
    }
}
```
*View*   
`'resources/template/hello-template.html'`
``` html
<html xmlns:th="http://www.thymleaf.org">
<body>
<p th:text="'hello ' + ${name}">hello! empty</p>
</body>
</html>
```
**실행**   
● http://localhost:8080/hello-mvc?name=spring   

MVC, 템플릿 엔진 이미지
![](https://velog.velcdn.com/images%2Ffalling_star3%2Fpost%2F4d916c32-880f-40ce-b487-f592c59a23d9%2Fimage.png)

---
### API
**@ResponseBody 문자 반환**
``` java
@controoler
public class HelloController{

    @GetMapping("hello-string")
    @ResponseBody
    public String helloString(@RequestParam("name") String name) {
        return "hello " + name;
    }

}
```
● `'@ResponseBody'`를 사용하면 뷰 리졸버`('viewReslover')`를 사용하지 않음   
● HTTP의 BODY에 문자 내용을 직접 반환(HTML BODY TAG를 말하는 것이 아님)   

**실행**   
● http://localhost:8080/hello-api?name=spring   

@ResponseBody 사용원리   
![](https://blog.kakaocdn.net/dn/uoFSH/btrg1JPyimy/pm2rm72xLdXR4Iv66IsJCK/img.png)

● `@ResponseBody`를 사용      
● HTTP의 BODY에 문자 내용을 직접 반환   
● `viewResolver`대신에 `HttpMessageConverter`가 동작   
● 기본 문자처리 : `StringHttpMessageConverter`   
● 기본 객체처리 : `MappingJacksonHttpMessageConverter`   
● byte 처리 등등 기타 여러 HttpMessageConverter가 기본으로 등록 되어 있음

---