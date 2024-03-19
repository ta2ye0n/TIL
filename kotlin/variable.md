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