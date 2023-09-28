# Spring
---
## Spring Security
스프링 시큐리티는 인증(Authentication), 권한(Authorize) 부여 및 보호 기능을 제공하는 spring의 하위 프레임워크이다

> 인증 : 해당 사용자가 본인이 맞는지를 확인하는 절차
> 인가 : 인증된 사용자가 요청된 자원에 접근가능한가를 결정하는 절차
---
### 인증 방식
```
1. crdential 방식 : username, pawwword를 이용하는 방식
2. 이중 인증(twofactor 인증) : 사용자가 입력한 개인 정보를 인증 후, 
   다른 인증 체계(예: 물리적인 카드)를 이용하여 두가지의 조합으로 인증하는 방식
3. 하드웨어 인증 : 자동차 키와 같은 방식
```
이중 Spring Security는 `credential 기반의 인증`을 취한다
- principal : 아이디(username)
- credential : 비밀번호 (password)

특정 자원에 대한 접근을 제어하기 위해서는 `권한`을 가지게 된다

특정 권한을 얻기 위해서는 유저는 `인증정보(Authentication)가 필요`하고 관리자는 해당 정보를 참고해 `권한을 인가(authorization)`한다

보편적으로 username - password 패턴의 인증방식을 거치기 때문에 `스프링 시큐리티는 principal - credentail 패턴`을 가지게 된다

---
### Spring Security의 특징
1. 서블릿 API 통합

2. Filter를 기반으로 동작
    - Spring MVC와 분리되어 관리하고 동작할 수 있다

2. 인증과 권한 부여를 모두 포괄적이고 확장 가능한 지원
4. 세션 고정, clickjacking, 사이트간 요청 위조 등과 같은 공격으로부터 보호
>- 세션 고정 : 사용자 로그인 시 항상 일정하게 고정된 세션 ID값을 사용하는 취약점
>- Clickjacking : 사용자가 클릭하고 있다고 인지하는 것과 다른 어떤 것을 
클릭하게 속이는 악의적인 기법
>- 사이트간의 요청 위조 : csrf라 부르며, 사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위를 특정 웹 사이트에 요청하게 하는 악의적인 기법

5. Bean으로 설정 가능
> Spring Security 3.2부터는 XML 설정을 하지 않아도 된다

---
### Spring Security 동작 과정
![](https://velog.velcdn.com/images/hope0206/post/f8286929-adcc-4963-82ec-188dd2523afb/image.png)

1. Http Request 수신   
    - 사용자가 로그인 정보와 함께 인증 요청
2. 유저 자격을 기반으로 인증토큰 생성
    - AuthenticationFilter가 요청을 가로채고, 가로챈 정보를 통해 UsernamePAsswordAuthentication Token의 인증용 객체를 생성한다

3. Filter를 통해 Authentication Token을 AuthenticationManager로 위임
    - AuthenticationMAnager의 구현체인 ProviderManager에게 생성한 UsernamePassworkdToken 객체를 전달한다
4. AuthenticationProvider의 목록으로 인증을 시도
    - AutenticationManger는 등록된 AuthenticationProvider들을 조회하며 인증을 요구한다

5. UserDetailsService의 요구
    - 실제 데이터베이스에서 사용자 인증정보를 가져오는 UserDetailService에 사용자 정보를 넘겨준다
6. UserDetails를 이용해 User 객체에 대한 정보 탐색
    - 넘겨받은 사용자 정보를 통해 데이터베이스에서 찾아낸 사용자 정보인 UserDetails 객체를 만든다
7. User 객체의 정보들을 UserDetails가 UserDetailsService(LoginService)로 전달
    - AuthenticationProvider들은 USerDetails를 넘겨받고 사용자 정보를 비교한다
8. 인증 객체 or AuthenticationException
    - 인증이 완료가 되면 권한 등의 사용자 정보를 담은 Authentication 객체를 반환한다
9. 인증 끝
     - 다시 최초의 AuthenticationFilter에 Authentication 객체가 반환된다
10. SecurityContext에 인증 객체를 설정
    - Authentication 객체를 Security Context에 저장한다

최종적으로 SecurityContextHolder는 세션 영역에 있는 SecurityContext에 Authentication 객체를 저장한다. 사용자 정보를 저장한다는 것은 스프링 시큐리티가 전통적인 `세션 - 쿠키 기반의 인증 방식을 사용`한다는 것을 의미한다

---
### Spring Security 기본구조
![](https://blog.kakaocdn.net/dn/buuCmH/btqD9juZn8b/hQ5fDjQRI0Eqff9yrBJIZk/img.png)

**필터별 기능 설명**   

- `SecurityContextPersistenceFilter`   
SecurityContextRepository에서 SecurityContext를 로드하고 저장하는 일을 담당한다

- `LogoutFilter`   
로그아웃 URL로 지정된 가상URL에 대한 요청을 감시하고 매칭되는 요청이 있으면 사용자를 로그아웃시킨다

- `UsernamePasswordAuthenticationFilter`   
사용자명과 비밀번호로 이뤄진 폼기반 인증에 사용하는 가상 URL요청을 감시하고 요청이 있으면 사용자의 인증을 진행한다

- `DefaultLoginPageGeneratingFilter`   
폼기반 또는 OpenID 기반 인증에 사용하는 가상 URL에 대한 요청을 감시하고 로그인 폼 기능을 수행하는데 필요한 HTML을 생성한다

- `BasicAuthenticationFilter`   
HTTP 기본 인증 헤더를 감시하고 이를 처리함

- `RequestCacheAwareFilter`   
로그인 성공 이후 인증 요청에 의해 가로채어진 사용자의 원래 요청을 재구성하는데 사용한다
> SecurityContextHolderAwareRequestFilter <br>HttpServleRequest를 HttpServletRequestWrapper를 상속하는 하위 클래스   
(SecurityContextHolderAwareRequestWrapper)로 감싸서 필터 체인상 하단에 위치한 요청 프로세서에 추가 컨텍스트를 제공한다

- `AnonymousAuthenticationFilter`   
이 필터가 호출되는 시점까지 사용자가 아직 인증을 받지 못했다면 요청 관련 인증 토큰에서 사용자가 익명 사용자로 나타나게 된다

- `SessionManagementFilter`<br>
인증된 주체를 바탕으로 세션 트래킹을 처리해 단일 주체와 관련한 모든 세션들이 트래킹되도록 도와준다

- `ExceptionTranslationFilter`<br>
이 필터는 보호된 요청을 처리하는 동안 발생할 수 있는 거대한 예외의 기본 라우팅과 위임을 처리한다

- `FilterSecuritylnterceptor`<br>
이 필터는 권한부여와 관련한 결정을 AccessDecisionManger에게 위임해 권한부여 결정 및 접근 제어 결정을 쉽게 만들어준다
---
### 동시 세션 제어, 세션 고정 보호, 세션 정책
1. `세션관리` -> 인증 시 사용자의 세션정보를 `등록, 조회, 삭제` 등의 세션 이력을 관리

2. `동시적 세션 제어` -> 동일 계정으로 접속이 허용되는 최대 세션수를 제한
3. `세션 고정 보호` -> 인증 할 때마다 세션 쿠키를 새로 발급하여 공격자의 쿠키 조작을 방지
4. `세션 생성 정책` -> `Always, if_required, Never, Stateless`

#### 동시 세션 제어
```
같은 계정(세션)을 동시에 몇개까지 유지할 수 있게 할 지에 대한 제어를 의미
```

![](https://user-images.githubusercontent.com/58545240/142721883-d5bacb64-41bd-4b48-9253-7c3b341d63d8.png)
**최대 세션 허용 개수를 초과하였을 경우의 처리 로직 2가지 전략**   
1. 이전 사용자 세션 만료 전략   
신규 로그인시 기존 로그인 계정의 세션이 만료되도록 설정하여 기존 사용자가 자원 접근시 세션만료가 된다

2. 현재 사용자 인증 실패 전략   
신규 사용자가 로그인 시도시 인증 예외 발생

#### 세션 고정 보호
```
보호라는 말은 공격으로부터 막는다는 의미로, 악의적인 해커의 세션 고정 공격을 막기위한 대응 전략이다
```
![](https://user-images.githubusercontent.com/58545240/142721888-5c5f40e2-315a-4d14-b48d-6645708f734f.png)

세션 고정 공격을 방지하기 위해 세션 고정 보호가 필요하다
> 세션 고정 공격이란?   
공격자가 서버에 접속을 해서 `JSSEIONID`를 발급받아서 사용자에게 자신이 발급받은 세션 쿠키를 심어놓게되면 사용자가 세션쿠키로 로그인 시도했을 경우 공격자는 같은 쿠키값으로 인증되어 있기 때문에 공격자는 사용자 정보를 공유하게 된다   
> 세션 고정 보호란?   
사용자가 공격자가 세션쿠키로 로그인을 시도하더라도 로그인시마다 새로운 세션ID를 발급하여 제공하게 되면, `JSSEIONID`가 다르기 때문에, 공격자는 같은 쿠키값으로 사용자 정보를 공유받을 수 없다

**세션 고정 보호 설정하기**   
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Autowired
    UserDetailsService userDetailsService;

    @Override
    protected void configure(HttpSecurity http) throws Exception {

        http
                .sessionManagement()
                .sessionFixation().changeSessionId();// 기본값 -> 세션은 유지하되 세션아이디는 계속 새로 발급(servlet 3.1이상 기본 값)
                                                     // none, migrateSession, newSession
		}
}
```
- none()   
세션이 새로 생성되지 않고 그대로 유지되기 때문에 세션 고정 공격에 취약하다

- migrateSession()   
새로운 세션도 생성되고 세션아이디도 발급된다 (sevelt 3.1 이하 기본 값) + 이전 세션의 속성값들도 유지된다

- newSession()   
세션이 새롭게 생성되고, 세션아이디도 발급되지만, 이전 세션의 속성값들을 유지할 수 없다

**세션 정책**   
인증처리를 할 때 꼭 스프링 시큐리티에서 세션을 생성할 필요는 없고, 외부 서비스를 통해 인증 토큰을 발갑하는 방식을 사용 할 수도 있다

**세션 정책 설정하기**
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Autowired
    UserDetailsService userDetailsService;

    @Override
    protected void configure(HttpSecurity http) throws Exception {

        http
                .sessionManagement()// 세션 관리 기능이 작동함.
                .sessionCreationPolicy(SessionCreationPolicy.IF_REQUIRED);
		}
}
```
- SessionCreationPolicy.Always : 스프링 시큐리티가 항상 세션 생성 

- SessionCreationPolicy.IF_REQUIRED : 스프링 시큐리티가 필요 시 생성(default)   
- SessionCreationPolicy.Never : 스프링 시큐리티가 생성하지 않지만 이미 존재하면 사용   
- SessionCreationPolicy.Stateless : 스프링 시큐리티가 생성하지 않고 존재해도 사용하지 않음
-> JWT 토큰방식을 사용할 때는 Stateless 정책을 사용한다

#### 세션 제어 필터 (SessionManagementFilter, ConcurrentSessionFilter)

**SessionManagementFilter**   
1. `세션관리` -> 인증 시 사용자의 세션정보를 `등록, 조회, 삭제` 등의 세션 이력을 관리

2. `동시적 세션 제어` -> 동일 계정으로 접속이 허용되는 최대 세션수를 제한
3. `세션 고정 보호` -> 인증 할 때마다 세션 쿠키를 새로 발급하여 공격자의 쿠키 조작을 방지
4. `세션 생성 정책` -> `Always, if_required, Never, Stateless`

**ConcurrentSessionFilter**    
- 매 요청 마다 현재 사용자의 세션 만료 여부 체크
- 세션이 만료되었을 경우 즉시 만료 처리
- session.isExired() == true
    - 로그아웃 처리
    - 즉시 오류 페이지 응답(This session has been expired)

**SessionManagementFilter, ConcurrentSessionFilter - Flow**   
![](https://user-images.githubusercontent.com/58545240/142767019-ae6c7acf-13cd-46a1-8f27-e7ab968a8597.png)

1. Login 시도   
2. 최대 세션 허용 개수 확인    
    -> 최대 세션 허용 개수가 초과되었을 경우 정책별 로직 수행(이전 사용자 세션 만료/ 현재 사용자 인증 실패) : session.expireNow()
3. 이전사용자가 자원접근(Request) 시도
4. ConcurrentSessionFilter에서 이전 사용자의 세션이 만료되었는지 확인   
    -> SessionManagementFilter 안의 설정 참조
5. 로그아웃 처리 후 오류 페이지 응답   
    -> This session has been expired

**SessionManagementFilter, ConcurrentSessionFilter - sequence diagram**   
![](https://cdn.inflearn.com/public/files/courses/324591/dda4eeff-9e4c-454f-a446-ebb13b3d077b/arch2.jpg)

---
### 예외처리 및 요청 캐시 필터 
```
ExceptionTranslationFilter, RequestCacheAwareFilter
```
`SpringSecurity`가 관리하는 보안 필터중 마지막 필터가 `FilterSecurityInterceptor`이고, 바로 전 필터가 `ExceptionTranslationFilter`이고 해당 필터에서 사용자의 요청을 받을 때, 그 다음 필터로 그 요청을 전달할 때 `try-catch`로 감싸서 `FilterSecurityInterceptor`를 호출하고 있고, 해당 필터에서 생기는 인증 및 인가 예외는 `ExceptionTranslationFilter`로 `throw` 하고 있다

**AuthenticationException**   
- 인증 예외 처리
1. AuthenticationEntryPoint 호출   
-> 로그인 페이지 이동, `401(Unauthorized)` 오류 코드 전달 등
2. 인증 예외가 발생하기 전의 요청 정보를 저장   
-> `RequestCache` - 사용자의 이전 요청 정보를 세션에 저장하고 이를 꺼내 오는 캐시메커니즘   
-> `SavedRequest` - 사용자가 요청했던 request 파라미터 값들, 그 당시의 헤더값들 등이 저장

**AccessDeniedException**   
- 인가 예외 처리
    - AccessEdniedHandler 에서 예외 처리하도록 제공