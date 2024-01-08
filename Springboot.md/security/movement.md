# spring boot
---
## Security
---
### 동작 과정
![](https://velog.velcdn.com/images/leeeeeyeon/post/123ad38d-541a-45d3-95a7-076113ef79ee/image.png)

---
### 로그인
![](https://velog.velcdn.com/images/leeeeeyeon/post/20721d5c-d97e-4fda-9425-2a09b61f68c4/image.png)

1. 요청
    - 사용자가 로그인 정보를 요청한다
    > 아이디와 비밀번호를 입력하여 서버로 전송

2. `토큰` 생성
    - AuthenticationFilter 가 요청을 받는다
    - 토큰(인증용 객체)를 생성한다 -> UsernamePasswordAuthenticationToken

3. AuthenticationFilter로부터 `인증용 객체` 전달 받는다
    - AuthenticationFilter는 토큰을 AuthenticationManager에게 보내면서 인증을 위임한다
    > ex) 정보가 담긴 토큰을 넘기고 그 토큰으로 회원가입한 유저인지 확인(인증)

4. 토큰을 처리할 수 있는 `AuthenticationProvider` 선택
    - AuthenticationMAnager 은 `List` 형태로 AuthenticationProvider를 가지고 있다
    - AuthenticationProvider에게 인증용 객체를 다시 위임한다
    - AuthenticationManager은 인증을 담당하는 클래스이지만, 실제 인증하는 것은 `AuthenticationProvider`인터페이스

![](https://velog.velcdn.com/images/leeeeeyeon/post/c0c635c6-2921-4dcc-a77d-09245998c1f1/image.png)

5. 인증 절차
    - `AuthenticationProvider 인터페이스`는 DB에 있는 사용자 정보와 인증용 객체에 담긴 정보를 비교한다<br><Br>

    둘을 비교하기 위해서는 DB에 있는 `사용자 정보와 인증용 객체` 둘 다 가지고 있어야한다

6. 인증 성공
    - 인증에 성공하면, AuthenticationProvider에서 인증된 인증용 객체를 `Authentication 객체`에 담아 `AuthenticationManager`에게 전달한다
    - AuthenticationManager은 다시 `AuthenticationFilter`에게 전달한다

7. AuthenticationSuccessHandler 실행
    - AuthenticationFilter는 `SecurityContextHolder`라는 곳에 담은 후, AuthenticationSuccessHandler을 실행한다
        - 실패시 `AuthenticationFailureHandler` 실행
        - 이후 인증된 사용자가 다시 요청을 보내게 되면, SecurityContext 객체 안에 Authentication이 있는지 확인 후 있다면 바로 인과처리로 넘어감으로 인해 효율 적 처리가 가능


