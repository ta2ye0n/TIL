# Spring boot
---
## Validation
---
### @Valid
```
빈 검증기(Bean Validator)를 이용해 객체의 제약 조건을 검증하도록 지시하는 어노테이션
```
JSR 표준의 빈 검증 기술의 특징은 객체의 필드에 달린 어노테이션으로 `편리하게 검증하는 것`이다

**사용 방법**   
유효성을 체크할 객체 앞에 `@Vaild`를 붙여준다   
모든 요청은 프론트 컨트롤러인 `디스패처 서블릿`을 통해 컨트롤러로 전달된다   
전달 과정에서 컨트롤러 메서드의 객체를 만들어주는 `ArgumentResolver`가 동작한다   
@Valid 역시 ArgumentResolver에 의해 처리된다   
따라서 @Valid는 기본적으로 `컨트롤러에서만 동작`하며 `다른 계층에서는 검증`이 안된다

**@Valid 예외**   
검증에 오류가 생기면 `Method ArgumentNotValidException` 예외가 발생한다

---
@Validated
```
AOP 기반으로 메서드의 요청을 가로채서 유효성 검사를 진행한다
```
컨트롤러가 아닌 `다른 계층`에서 유효성 검사를 하고 싶을 때 사용하면 된다
@Validated는 JSR 표준 기술이 아니며, Spring 프레임워크에서 제공하는 어노테이션이다

@Validated를 서비스 클래스 위에 선언하고 유효성 검사를 하고 싶은 클래스에 @Valid를 붙여주면 된다
```java
ex)
@Service
@Validated
public class UserService {
    public void createUser(@Valid SignUpReq signUpReq) {
    }
}
```
다른 기능으로는 유효성 검증 그룹을 지정해줄 수 있다
하지만 그룹 지정 기능은 코드가 복잡해져 거의 사용이 안되므로 그냥 참고만 하는게 좋다

**@Validated 예외**   
유효성 검사에 실패하면 @Valid만 사용하던 것과는 달리 `ContraintViolationException` 예외가 발생한다   
@Validated를 클래스 레벨에서 선언하면 클래스에 유효성 검사를 위해 AOP 어드바이스 또는 인터셉터가 등록된다
그리고 해당 클래스의 메서드들이 호출될때 AOP의 포인트 컷으로써 요청을 가로채 유효성 검증을 해주는 식으로 동작한다   
따라서 @Validated는 계층과 무관하게 `스프링 빈`이라면 유효성 검증을 할 수 있다