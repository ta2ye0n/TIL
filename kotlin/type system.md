# Kotlin
---
## Type System (타입 시스템)
---
### NULL 가능성 (Nullability)
```
NullPointerException(NPE) 오류를 피할 수 있도록 돕는 코틀린 타입 시스템의 특성
```
코틀린에서는 널이 될 수 있는지 여부를 타입 시스템에 추가함으로써 `컴파일러가 여러 가지 오류를 컴파일 시 미리 감지`해서 `실행 시점에 발생할 수 있는 예외의 가능성을 줄일 수 있다`

**NULL이 될 수 있는 타입**   
코틀린의 모든 타입은 `기본적으로 널이 될 수 없는 타입`이다   
코틀린은 널이 될 수 있는 타입을 `명시적으로 지원`한다   
> 타입 옆에 `물음표(?)`를 표시한다

NULL이 될 수 있는 타입의 변수지만, 현재 NULL이 아님을 주장할 수 있다
> `느낌표 2개(!!)`를 변수 뒤에 붙인다   
이 표시를 통해 null 이 될 수 없는 변수에 `null이 될 수 있는 타입을 주입`할 수 있다

널이 될 수 있는 타입인 변수에 대해 메서드를 호출하면 NPE가 발생할 수 있으므로, 코틀린은 그런 메서드 호출을 금지함으로써 NPE 발생을 예방한다
 
--- 
### ?. (안전한 호출 연산자)
```
?. - null 검사와 메서드 호출을 한번의 연산으로 수행
```
```kotlin
변수?.메서드()

ex)
foo?.bar()
```
- foo가 `null이면` bar() `호출이 무시`되고 null이 결과 값이 된다   
- foo가 `null이 아니면` bar() 메서드를 `정상 실행하고 결과값을 얻어온다`

---
### ?: (엘비스 연산자)
```
null 대신 사용할 디폴트 값을 지정할 때 편리한 연산자
```
```kotlin
ex)
fun foo(s: String?) {
    val t : String = s ?: ""
}
```
- s가 null이면 ""(빈 문자열)을 t에 넣고
- s가 null이 아니면 t에 s를 넣는다
```kotlin
fun strLen(s: String?): Int = s?.length ?: 0
---------------------------------------------------------------------------
var b: Int? = 10
var d: Int = b ?: 3
// var d: Int = b -> error
```
---
### as? (안전한 캐스트)
```
as? 연산자는 어떤 값을 지정한 타입으로 캐스트하고, 변환할 수 없으면 null을 반환한다
```

자바 타입 캐스트와 마찬가지로 대상 값을 as로 지정한 타입으로 바꿀 수 없다면 `ClassCastException`일 발생한다
> 자바에서는 보통 `is`를 통해 미리 as로 변환 가능한 타입인지 검사한다

```kotlin
ex)
foo as? Type
```
- foo is Type이면 foo는 `Type으로 변화`
- foo !is Type 이면 `null 반환`

---
### let 함수
```
안전한 호출 연산자와 함께 사용하면 원하는 식을 평가해서
결과가 널인지 검사한 다음에 그 결과를 변수에 넣는 작업을 한다
```
간단한 식을 사용해 한번에 처리 가능하다

```kotlin
fun sendEmailTo(email: String) {
    println("Sending email to $email")
}

fun main(args: Array<String>) {
    var email: String? = "yole@example.com"
//    sendEmailTo(email) -> error
    email?.let { sendEmailTo(it) }
}
```
---