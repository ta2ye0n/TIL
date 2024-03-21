# Kotlin
---
## 배열
```
동일한 자료형을 가진 데이터들을 나열한 구조
```
데이터 항목에는 `인덱스(index)`를 사용하여 접근한다
인덱스는 배열의 순서로 `0부터` 시작한다

---
### 선언 방법
**arrayOf**   
```kotlin
val 변수명 = arrayOf<자료형 / 생략>(값1, 값2, 값3)
```
자료형은 `생략 가능`하며, 배열의 크기는 항목의 개수에 따라 자동으로 결정된다

```kotlin
Ex)
// 자료형을 생략한 예제
// 정수 배열
val numbers = arrayOf(1, 2, 3, 4, 5)

// 객체 배열
data class Person(val name: String, val age: Int)

// 자료형을 생략하지 않은 예제
// 정수 배열
val numbers: Array<Int> = arrayOf(1, 2, 3, 4, 5)
```
자료형을 작성했을 경우, 해당 자료형만 인자로 들어올 수 있다

```kotlin
// 자료형을 대체할 수 있는 예제
val 변수명 = (자료형)ArrayOf(값1, 값2, 값3)
```
ArrayOf 앞에 자료형을 붙이면 된다

---
