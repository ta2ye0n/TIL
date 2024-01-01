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
### @WintAnonymousUser
`익명의 유저`로 인증할때 선언한다   
보통 `비로그인 시`인데 `인증이 필요하는 서비스`를 테스트할 때 사용한다

---
### @WithUserDetails
`특정 사용자`로 인증할때 선언한다   
이미 존재하는 사용자를 조회해서 UserDetails를 조회하여 인증한다
```java
@WithUserDetails(value= "Ex", userDEtailsServiceBeanName = "ExService")
```
- value : 사용자 이름
- userDetailsServiceBeanName : UserDetails 조회 서비스의 빈 이름, 이때 하나밖에 없으면 생략가능ㄴ

---
### @PostAuthorize
메서드가 `실행된 이후의 return값`을 활용할 수 있다
`return Object`와 같이 사용하면 된다