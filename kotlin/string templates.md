# kotlin
---
## 문자열 템플릿(String Templates)
```
문자열 내에 변수나 표현식을 사용하여 값을 문자열에 포함시킬 수 있도록 한다
```
주로 문자열을 `동적`으로 구성할 때 사용하며, 코드를 `간결하게 작성`하는데 도움이 된다

---
### $
변수 이름 앞에 `$`를 붙이면, 문자열 템플릿이 변수의 값을 문자열에 담아준다
```kotlin
// ex)
fun main() {
    val number = 42

    println("number = $number")
}

// 출력
number = 42
```

$ 다음에 오는 대상이 `숫자`인 경우 이를 인식하지 않으며 그대로 출력한다
또한 $ 다음에 문자가 오는 경우 $ 앞에 `역슬래시(\)`를 붙여 그대로 출력할 수 있다

```kotlin
// ex)
fun main() {
    val number = 123

    println("$number")
    println("$123")
    println("\\$number")
}

// 출력
123
$123
$number
```

`${}`의 중괄호 안에 식을 넣으면 해당 식의 결과를 `String`으로 변환하여 문자열에 값을 삽입한다
```kotlin
// ex)
fun main() {
    val a = 10
    val b = 20

    println("a + b: ${a + b}")
    println("${if (a > b) a else b}")
}

// 출력
a + b: 30
20
```

문자열에 특수 문자를 넣어야 하는 경우 `역슬래시(\)`를 통해 표현하거나 `문자열 리터럴(""")`을 사용해야 한다
```kotlin
fun main() {
    val s = "value"

    println("s = \\"$s\\".")
    println("""s = "$s".""")
}

// 출력
s = "value".
s = "value".
```