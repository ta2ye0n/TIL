# Spring
---
## Security
---
### Filter
```
서블릿 필터는 서블릿 기반 애플리케이션의 엔드포인트에 요청이 도달하기 전에 
중간에 요청을 가로챈 후 어떤 처리를 할 수 있도록 해주는 JAVA의 컴포넌트
```

![](https://velog.velcdn.com/images/zini9188/post/4ce1094a-e248-48d3-8d2a-77c48b9871f0/image.png)   
필터의 처리가 완료되면 `DispatcherServlet`에서 클라이언트 요청을 핸들러에 매핑하기 뒹한 다음 작업을 진행한다

---
### Filter Chain
```
여러 개의 필터가 체인을 형성하고 있는 필터의 묶음
```
**특성**   
서블릿 필터 체인은 요청 URI path를 기반으로 HttpServletRequest를 처리하는데 클라이언트가 서버 측 애플리케이션에 요청을 전송하면 서블릿 컨테이너는 `요청 URI의 경로`를 기반으로 어떤 필터와 어떤 서블릿을 `매핑할지 결정`한다

- 필터는 필터 체인안에서 `순서를 지정`할 수 있고, `지정한 순서에 따라 동작`하게 할 수 있다
- 필터 체인에서 `필터의 순서는 매우 중요`하다
- 여러 개의 필터를 등록하고 `순서를 지정`하기
    - `@Order` 어노테이션이나 ,`Ordered 인터페이스`를 구현
    - `FilterRegistrationBean`을 사용하여 명시적으로 필터의 순서를 지정

---
### Security Filter Chain
```
Spring Security 에서 제공하는 인증, 인가를 위한 필터들의 모음
```
Spring Security에서 `가장 핵심이 되는 기능`을 제공하며, 거의 대부분의 서비스는 `Security Filter Chain` 에서 실행된다고 보면 된다
`기본적으로 제공`하는 필터들이 있으며, 사용자는 개발의 취지와 목적에 맞게 `커스텀 필터` 또한 `필터 체인으로 포함`시켜 사용 할 수 있다

![](https://velog.velcdn.com/images/zini9188/post/4cd9f848-8d05-490c-a112-6a220ea942d3/image.png)

---
**Application Context 초기화**   
```
Application Context 초기화 과정에서 사용자가 정의한 Security Filter Chain이 생성된다
```
Spring Security 에서는 인증, 인가에 대한 처리를 여러개의 필터를 통해 연쇄적으로 실행하여 수행한다
이때 상황에 따라 필요한 필터가 있고 굳이 필요 없는 필터가 있다
이걸 설정 클래스를 통해 `Spring Security`에 대한 전반적인 관리 및 제어를 할 수 있다

기존에는 Spring Security을 위한 `설정 클래스임을 정의`하기 위해 `WebSecurityConfigurerAdapter`를 상속했지만 현재는 `SecurityFilterChain` 빈을 직접 만들어야 한다

*정리*   
SecurityFilterChain Bean 을 반환하는 filterchain 메서드의 매개변수인 `HttpSecurity`을 통해 사용할 필터와 사용자가 `직접 정의한 필터를 정의`할 수 있다
해당 설정을 바탕으로, 애플리케이션 구동시 `Security Filter Chain`이 구성되어 실행된다

---
**Delegating Filter Proxy**   
```
Filter 인터페이스를 구현하는 구현 클래스
```
필터를 사용하는 `시작점`이다
서블릿 컨테이너 영역의 필터와 ApplicationContext에 Bean으로 등록된 필터들을 `연결해주는 브릿지` 역할을 한다

DelegatingFilterProxy는 `Servlet 스펙에 있는 기술`이기 때문에 Servlet Container 에서만 생성되고 실행된다
Spring의 Spring Container 와는 다르기 때문에 Spring Bean으로 주입하거나 Spring에서 사용되는 기술을 `Servlet에서 사용할 수 없다`

---
**FilterChainProxy**   
```
보안을 위한 작업을 처리하는 필터의 모음
```
![](https://velog.velcdn.com/images/zini9188/post/e0993728-9f33-4a2a-9f98-e367caf7e890/image.png)   

스프링 시큐리티의 필터를 `사용하기 위한 진입점`으로 보안 필터들이 `필요한 작업`을 수행한다

URL 별로 필터 체인을 등록할 수 있는데, 이때 필터 체인의 우선순위는 `FilterChainProxy`에 의해 결정되며 가장 먼저 매칭된 필터 체인을 사용한다
> `/api/**`과 `/**` 필터 체인이 있고 `/api/message` URL이 들어오는 경우, 가장 먼저 매칭된 `/api/**` 필터 체인을 사용   
`/message/**` URL의 경우, 가장 먼저 매칭되는 `/**` 필터체인을 사용

---
### Filter, Filter Chain 구현
```java
Ex)

public class FirstFilter implements Filter {
     public void init(FilterConfig filterConfig) throws ServletException {
        Filter.super.init(filterConfig);      
     }
     
     public void doFilter(ServletRequest request, ServletResponse response,
                          FilterChain chain)
                          throws IOException, ServletException { 
        chain.doFilter(request, response);
     }
     
     public void destroy() {
        Filter.super.destroy();
     }
  }
```
- `init()` 메서드   
생성한 필터에 대한 초기화 작업을 진행
- `doFilter()` 메서드   
`chain.doFilter()` 이전에서 전처리 작업에 대해 구현   
`chain.doFilter()` 이후에서 후처리 작업에 대해 구현

- `destroy()` 메서드   
필터가 컨테이너에서 종료될 때 호출   
필터가 사용한 자원을 반납하는 처리 등의 로직을 작성