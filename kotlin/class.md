# kotlin
---
## class
속성과 동작을 가지기 때문에 `프로퍼티`와 `메서드`를 멤버로 가진다

---
### 데이터 클래스
```
데이터 저장을 위한 클래스
```
**선언 방법**   
- `data 키워드` 사용
- 주 생성자는 최소한 `하나의 매개변수`를 가져야한다
- 주 생성자의 모든 매개변수는 `val, var`로 지정된 프로퍼티여야 한다
- 데이터 클래스는 `abstract, open, sealed, inner` 키워드를 사용할 수 없다
```kotlin
// 예시
data class dataClass (
    val id : Long,
    val name : String,
    val email : String
) {}
```

자주 사용하는 데이터를 객체로 묶어준다
`VO 클래스`를 편리하게 이용할 때 주로 사용한다
data 클래스는 `데이터를 다루는데 편리한 기능을 제공하는 것`이 주목적이다

**데이터 클래스에서 사용되는 함수**   
 - `equals()`   
 두 객체의 내용이 같은지 비교하는 연산자 (고유값이 다르지만 의미값이 같은 경우)

 - `hashCode()`   
 객체를 구별하기 위한 고유한 정수값 생성   
 데이터 세트나 해시 테이블을 사용하기 위한 하나의 인덱스
 - `copy()`   
 프로퍼티만 변경해서 객체 복사   
 - `toString()`   
 문자열로 반환   
 - `componentN()`   
 객체의 선언부 구조를 분해

 ---
 ### 내부 클래스
 코틀린은 두가지의 내부 클래스 기법이 있다 하나는 `중첩 클래스`이고, 다른 하나는 `이너 클래스`이다    
 내부 클래스는 `독립적인 클래스로 정의하기 모호`하거나 `다른 클래스에서 잘 사용하지 않아 외부에서 접근할 필요가 없을 때` 사용하면 좋다
> 너무  남용할 경우 클래스 간의 의존성이 커지고 코드가 읽기 어려워진다

**중첩 클래스(nested class)**   
기본적으로 `정적(static)`처럼 다뤄진다
`객체의 생서 없이 접근할 수 있다`는 것이다   
```kotlin
class Outer {
	val ov = 5
		class Nested {// 중첩 클래스의 프로퍼티
			val nv = 10
			fun greeting() = "Nested"
	}
	fun outside() {
		val msg = Nested().greeting() // 외부 클래스에서 중첩 클래스로는 접근 가능
		println(Nested().nv)
	}
}

fun main() {
	val output = Outer.Nested().greeting() // 중첩 클래스의 프로퍼티이므로 객체 생성 없이 접근 가능
	println(output)

	Outer.outside() // 오류 외부 클래스는 객체를 생성해야함
	val outer = Outer()
	println(outer.outside())
```
외부 클래스에서 중첩 클래스의 프로퍼티에는 접근할 수 있지만 반대로 중첩 클래스에서 외부 클래스로의 접근은 불가능하다는 특징이 있다
하지만 만약 외부 클래스에서의 프로퍼티가 `컴패니언 객체`의 프로퍼틴인 경우 접근이 가능하다

**이너 클래스(inner class)**   
중첩 클래스와는 좀 다른 역할을 한다
이너 클래스는 `외부 클래스에 접근`이 가능하다
private로 선언한 경우에도 가능하다
그리고 `외부 클래스를 항상 참조`하고 있다

항상 참조하고 있다?   
->
객체가 삭제되는 시점은 객체가 더 이상한 사용되지 않는 시점이다
그런데 내부 클래스를 사용하면 항상 외부 클래스의 객체를 참조하기 때문에, 객체가 적절한 시점에 삭제되지 못하고 `메모리 누수가 발생`한다

> 누수가 위험한 이유 : 암묵적(프로그래머가 발견하기 전까지 알 수 없는 것)인 것이기 때문
---
### 실드 클래스
```
미리 만들어 놓은 자료형을 묶어서 제공하는 클래스
```
`sealed`라는 키워드를 사용하며 추상클래스와 같이 객체를 만들 수 없다
생성자도 기본적으로 `private`이며 `private가 아닌 다른 생성자는 허용하지 않는다`   
`같은 파일 안에서는 상속이 가능`하나 다른 파일에서는 `불가능`하다
이때 `open` 키워드를 사용하면 된다 

실드 클래스는 `상태를 정의`하고 `관리`하는데 주로 사용된다
```kotlin
// 실드 클래스 선언 방법 첫번째
sealed class Result {
    open class Success (val message: String) : Result()
    class Error(val code: Int, val message: String) : Result()
}
class Status: Result() // 실드 클래스 상속은 같은 파일에서만 가능
class Inside: Result.Success("Status") // 내부 클래스 상속

// 실드 클래스 선언 방법 두번째
sealed class Result
class Error(val code: Int, val message: String) : Result()

class Status: Reuslt()
class Inside: Success("Status")
```
---
### 열거형 클래스(Enum Class)
```
여러 개의 상수를 선언하고 열거된 값을 조건에 따라 선택할 수 있는 특수한 클래스
```
`자료형이 동일한 상수`를 나열할 수 있다
하지만 `한 가지 자료형`만 나열 할 수 있다
```kotlin
ex)

enum class DayOfWeek(val num : Int) { // 주생성자
    Monday(1), Tuesday(2), ... , Sunday(7)
}
```
---