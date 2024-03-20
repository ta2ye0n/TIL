# Kotlin
---
## Variable
---
### 변수 선언 방법
```kotlin
var 변수명 : 변수타입 = 초기화
val 변수명 : 변수타입 = 초기화
```
- `var`   
variable = 읽기 / 쓰기가 가능한 일반 변수

- `val`    
valuable = 읽기만 가능한 final 변수

**Non-Null / Nullable**   
null 값을 가질 수 있으면 `Nullable`, null 값을 가질 수 없으면 `Non-null` 타입이다
```kotlin
var name : String = null //에러

var name : String? = null
```
Nullable 변수를 선언하려면 변수타입 뒤에 `?`를 꼭 붙여야 한다

---
### 안전 호출 연산자
Nullable 타입은 사용 시 안전 호출 연산자인 `?.`을 통해 안전 호출을 한다
호출하는 객체의 null 여부를 판별해 null이 아니면 속성을 참조하거나 메서드를 호출한다
만약 null이라면 null을 리턴한다

> Non-Null 타입도 안전 호출 연산자를 사용할 수 있지만 의미가 없다
---
### 변수 출력 방법
```kotlin
println("text $변수")

자바
System.out.println("text" + 변수);
```
> $를 출력하고 싶으면 $$
---