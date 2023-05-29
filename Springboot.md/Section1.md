# Spring boot
---
### 라이브러리 살펴보기
Gradle은 의존관계가 있는 라이브러리를 함께 다운로드 한다

*스프링부트 라이브러리*
```
● spring-boot-starter-web
    ● spring-boot-starter-tomcat : 톰캣(웹서버)
    ● spring-webmvc : 스프링 웹 MVC
● spring-boot-starter-thymeleaf : 타임리프 템플릿 엔진(View)
● spring-boot-starter(공통) : 스프링 부트 + 스프링 코어 + 로깅
    ● spring-boot
        ● spring-core
    ● spring-boot-starter-logging
        ● logback,slf4j
```
*테스트 라이브러리*
```
● spring-boot-starter-test
    ● junit : 테스트 프레임워크
    ● mockito : 목 라이브러리
    ● assertj : 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
    ● spring-test : 스프링 통합 테스트 지원
```
---
### View 환경설정
#### Welcome Page 만들기
``` html
<!DOCTYPE HTML>
<html>
<head>
    <title>Hello</title>
    <meta http-equiv="Content-Type" content="test/html; charset=UTF-8" />
</head>
<body>
Hello
<a href="/hello">hello</a>
</body>
</html>
```
```
● 스프링 부트가 제공하는 Welcome Page 기능
    ● static/indew.htmal을 올려두면 Welcome page기능을 제공한다.

● thymeleaf 템플릿 엔진   
    ● thymeleaf 공식사이트 : https://www.thymeleaf.org/
    ● 스프링 공식 튜토리얼 : https://spring.io/guides/gs/serving-web-content/
    ● 스프링부트 메뉴얼 : https://docs.spring.io/spring-boot/docs/current/reference/html/howto.html#howto.build
```
``` java
@Controller
public class HelloController{

    @GetMapping("hello")
    public String hello(Model model){
        model.addAttribute("data","hello!!")
        return "hello";
    }
}
```
``` html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Hello</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UFT-8"/>
</head>
<body>
    <p th:text="'안녕하세요. ' + ${data}">안녕하세요. 손님</p>
</body>
</html>
```
**thymelaf 템플릿엔젠 동작 확인**   
실행 : http://localhost:8080/hello   

동작 환경 그림
![](https://velog.velcdn.com/images/junsj119/post/8f5938a4-b7e4-46a2-963b-7084f4486366/image.png)   

● 컨트롤러에서 리턴 값으로 문자를 반환하면 뷰 리졸버`('viewResolver')`가 화면을 찾아서 처리한다.   
● 스프링 부트 탬플릿엔진 기본 viewName 매핑   
● `resources:temlates/`+{ViewName}+`'.html'`

> 참고 : `spring-boot-devtools`라이브러리를 추가하면,`html`파일을 컴파일만 해주면 서버 재시작 없이 View파일 변경이  가능하다.   
> 인텔리J컴파일 방법 : 메뉴 build → Recompile
---
**빌드하고 실행하기**   
콘솔로 이동   
1. `./gradlew build`   
2. `cd build/libs`   
3. `java -jar hello-spring-0.0.1-SNAPSHOT.jar`   
4. 실행확인