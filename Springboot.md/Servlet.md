# Servlet
---
## Servlet(서블릿)
```
동적 웹 페이지를 만들 때 사용되는 자바 기반의 웹 애플리케이션 프로그래밍 기술

클라이언트의 요청을 처리하고, 그 결과를 반환하는 Servlet 클래스의 구현 규칙을 지킨 자바 웹 프로그래밍 기술
```
웹 요청과 응답의 흐름을 간단한 메서드 호출만으로 체계적으로 다룰 수 있게 해준다

서블릿은 자바로 구현 된 CGI라고 흔히 말한다
> CGI : 서버와 애플리케이션 간에 데이터를 주고 받는 방식 또는 컨벤션(Common Gateway Interface)
---
### 주요 특징
- 클라이언트의 Request에 대해 `동적으로 작동`하는 웹 어플리케이션 컴포넌트

- 기존의 정적 웹 프로그램의 `문제점 보완`하여 동적인 여러 가지 기능을 제공
- JAVA의 스레드를 이용하여 동작
- MVC패턴에서 컨트롤러로 이용됨
- 컨테이너에서 실행
- 보안 기능을 적용하기 쉬움
- html을 사용하여 요청에 응답

#### 단점
- UDP보다 처리 속도가 느림
- HTML 변경 시 Servlet을 재컴파일해야 함
---
### 동작 과정
![](https://velog.velcdn.com/images%2Ffalling_star3%2Fpost%2F4fabf50a-d3d7-4391-8eb5-0cb436379d71%2Fimage.png)
```
1. 클라이언트 요청
2. HttpServletRequest, HttpServletResponse 객체 생성
3. Web.xml이 어느 서블릿에 대한 요청한 것인지 탐색
4. 해당하는 서블릿에서 service() 메서드 호출
5. doGet() 또는 doPost() 호출
6. 동적 페이지 생성 후 ServletResponse 객체에 응답 전송
7. HttpServletRequest, HttpServletResoponse 객체 소멸
```
클라이언트가 웹 서버에 요청하면 웹 서버는 그 요청을 톰캣과 같은 WAS에 위임한다
> WAS : DB 조회나 다양한 로직 처리를 요구하는 동적인 컨텐츠를 제공하기 위해 만들어진 Application Server (Web Application Server)
---
### 생명주기
```
초기화부터 서비스 수행 후 소멸하기까지의 과정

이 과정을 서블릿의 생명주기라하며 각 단계마다 호출되어 기능을 수행하는 콜백 메서드를 서블릿 생명주기 메서드
```

#### 생명주기 메서드
초기화 : `init()`   
- 서블릿 요청 시 맨 처음 한 번만 호출
- 서블릿 생성 시 초기화 작업을 주로 수행

작업 수행 : `doGet()`, `doPost()`
- 서블릿 요청 시 매번 호출
- 실제로 클라이언트가 요청하는 작업을 수행

종료 : `destroy()`
- 서블릿이 기능을 수행하고 메모리에서 소멸될 때 호출
- 서블릿의 마무리 작업을 주로 수행
---
### 서블릿 컨테이너
```
구현되어 있는 servlet 클래스의 규칙에 맞게 서블릿을 담고 관리해주는 컨테이너
```

- `웹서버와의 통신 지원`    
서블릿 컨테이너는 서블릿과 웹서버가 `손쉽게 통신`할 수 있게 해준다   
일반적으로 소켓을 만들고 listen, accept 등을 해야하지만 서블릿 컨테이너는 이러한 기능을 API로 제공하여 `복잡한 과정을 생략`할 수 있게 해준다
그래서 개발자가 서블릿에 구현해야 할 비지니스 로직에 대해서만 초점을 두게끔 도와준다

- `서블릿 생명주기 관리`<br>
서블릿 컨테이너는 서블릿 클래스를 로딩하여 `인스턴스화`하고, `초기화 메서드를 호출`하고, 요청이 들어오면 적절한 `서블릿 메서드를 호출`한다
또한 수명이 다 된 서블릿을 적절하게 `가비지 콜렉터를 호출`하여 필요없는 자원 낭비를 막아준다

- `멀티쓰레드 지원 및 관리`<br>
서블릿 컨테이너는 Request가 올때마다 새로운 자바 쓰레드를 하나 생성하는데,  HTTP 서비스 메서드를 실행하고 나면, 쓰레드는 자동으로 죽게 된다
원래 쓰레드를 관리해야 하지만 서버가 다중 쓰레드를 `생성 및 운영`해주니 쓰레드의 안전성에 대해서 걱정하지 않아도 된다

- `선언적인 보안 관리`<br>
서블릿 컨테이너를 사용하면 개발자는 보안에 관련된 내용을 서블릿 또는 자바 클래스에 구현해 놓지 않아도 된다 일반적으로 보안관리는 XML 배포 서술자에다가 기록하므로, 보안에 대해 수정할 일이 생겨도 자바 소스 코드를 수정하여 다시 컴파일 하지 않아도 보안관리가 가능하다

---
### JSP(Java Server Page)
```
HTML 코드에 JAVA 코드를 넣어 동적 웹페이지를 생성하는 웹어플리케이션 도구
```
JSP가 실행되면 자바 서블릿으로 변환되며 웹 어플리케이션 서버에서 동작되면서 필요한 긴능을 수행하고 그렇게 생성된 데이터를 웹페이지와 함께 클라이언트로 응답한다

---
### Servlet / JSP
||Servlet|JSP|
|:-----:|:----:|:-----:|
|정의 및 구조|순수 JAVA 코드로만 이루어진 웹서버용 클래스 <br> 동적 웹페이즈를 만들 때 java 코드 안에 HTML 태그가 삽입되는 구조|HTML 코드 속에 자바 코드가 들어가는 구조의 스크립트 언어|
|코드 내 처리방법|자바 코드 속에서 HTML 태그로 문자열 ("")로 처리해야함|HTML 속에서 자바코드를 <% 소스코드 %> 또는 <%= 소스코드 =%> 형태로 처리<br>(자바 소스코드로 작성된 부분은 웹 브라우저로 보내는 것이 아니라 웹 서버에서 실행됨)|
|한계(Servlet)와 보완(JSP)|1. 화면 인터페이스 구현에 너무 많은 코드를 필요로 하는 비효율성<br>2. 테스트할 때 빌드를 항상 다시해야 한다는 한계가 있음<br>3. HTML 변경 시 Servlet을 재컴파일해야하는 단점|-> 이에 따라 서블릿 기반의 서버사이트 스크립트 언어 JSP가 등장<br>1. HTML 표준에 따라 작성되므로 서블릿과 달리 웹페이지 작성이 편리<br>2. WAS에서 자동으로 빌드하고 클라이언트 화면에 동적으로 보여줌|
|MVC 패턴에서의 역할|Controller 역할|View 역할|