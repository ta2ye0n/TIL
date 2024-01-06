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