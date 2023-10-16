# Annotation
---
## Security
---
### @Secured
특정 권한만 `접근이 가능`하다는 것을 나타내는 annotation이다
간단하게 특정 기능을 Admin만 이용하게 하고 싶은 경우에 사용 가능하다

---
### @EnableWebSecurity
`보안 설정이 필요`한 클래스에 선언한다

보통 `extends WebSecurityConfigureAdapter` 같이 사용한다
`인증 / 권한부여 / 로그인, 로그아웃 페이지의 렌더링 등`에 사용된다

---
### @WithMockUser
모의 사용자가 필요한 `테스트 메소드`에 선언한다
인증된 모의 사용자 설정 가능한다
`-roles="권한이름"` 이런 식으로 사용한다

---
### @PostAuthorize
메서드가 `실행된 이후의 return값`을 활용할 수 있다
`return Object`와 같이 사용하면 된다