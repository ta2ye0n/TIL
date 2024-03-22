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
- **arrayOf**   
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
문자열과 객체를 저장하는 함수는 존재하지 않아 문자열을 배열로 저장할 때는 `arrayOf`를 사용해야한다

- **(자료형)Array**   
```kotlin
var 변수명 = (자료형)Array(크기, {초기값(생략가능)})
```
array는 10 크기를 가지고, 기본값이 0이 들어간다

중괄호 {} 안의 값은 `초기값을 인자`로 받기 때문에 주의해야한다
> var array = Array(10, {1,2,3}) -> 올바르지 않은 코드

```kotlin
val numbers = IntArray(5) { index -> index + 1}
```
만약 크기가 5인 정수 배열을 생성하고 각 요소를 1부터 순차적으로 초기화할 경우 이렇게 작성한다

index는 현재 요소의 순서를 나타내며 index + 1를 통해 1부터 시작하는 값을 할당한다

```kotlin
// 자료형을 생략한 예제
// 문자열 배열
val fruits = Array(3) { index -> "Fruit ${index + 1}" }

// 자료형을 생략하지 않은 예제
// 문자열 배열
val fruits : Array<String> = Array(3) { index -> "Fruit ${index + 1}" }
```
문자열 배열 StringArray는 존재하지 않기 때문에 `Array`을 이용하여 문자열 배열을 다룬다

- **Array<자료형(생략가능)>**
```kotlin
var array = Array<자료형>(크기, {값(생략가능)})
```
```kotlin
// 자료형을 생략하지 않은 예제
// 실수 배열
val temperatures: Array<Double> = Array<Double>(4) { index -> 20.0 + (index * 2.5) }

// 자료형을 생략한 예제
// 실수 배열
val temperatures = Array(4) { index -> 20.0 + (index * 2.5) }
```

> 변수를 선언하는 방법 중 2번째와 3번째 방법은 비슷하지만 다르다   
2번째 방법은 Array앞에 자료형을 붙이고, 3번째 방법은 <> 안에 자료형이 들어가며, 자료형을 생략하고 Array만 작성한다
> ```kotlin
> // 두번째 방법
> var numbers = IntArray(3) { index -> index + 1 }
>
> // 세번째 방법
> var numbers = Array(3) { index -> index + 1 }
> ```

---
