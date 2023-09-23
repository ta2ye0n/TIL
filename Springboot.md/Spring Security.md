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