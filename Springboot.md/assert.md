# Spring boot
---
## Assert
```
argument를 검증하기 위한 유틸리티 클래스

런타임 유효성을 식별하는데 효과적
```
일반적으로 `configuration properties` 보다는 `method arguments`의 검증에 사용한다
스프링 프레임워크 내부적으로 주로 사용되고 있다

---
### 특징
- `정적 메서드`들을 가지고 있다

- 메서드들은 `llegalArgumentException` 또는 `IllegalStateException`을 예외로 던진다
- 첫 번째 매개변수(parameter)로는 주로 검증 대상 인자(argument)나 확인하고자 하는 논리적 조건(logical condition)이다
- 마지막 매개변수는 보통 검증에 실패했을 때 보여질 `예외 메시지(exception message)`이다
- 예외 메시지의 경우 `String` 타입 파라미터나 `Supplier<String>` 파라미터로 전달될 수 있다

---
### 종류
|함수|설명|
|----|------|
|doesNotContain|해당 문자열 안에 subString이 포함되어있다면 ERROR|
|hasLength|null이 아니고 비어있는 문자열("")이 아니어야함|
|hasText|null이 아니고 공백이 아닌 유효한 문자가 존재하는 문자열이어야함|
|isTrue|해당 조건식이 참이면 OK|
|isNull|해당 객체가 null이면 OK|
|notNull|해당 객체가 not null이면 OK|
|notEmpty|해당 Array가 null이 아니고, 1개 이상의 Element를 가지고 있다면 OK|
|noNullElements|해당 Array에 null인 객체가 없다면 OK|
|state|해당 조건식이 참이면 OK| 