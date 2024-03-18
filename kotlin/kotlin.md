# Kotlin
---
## Kotlin
```
JetBrains에서 2011년에 공개한 언어로 자바와 호환이 되며 자바보다 더 간결하고 많은 기능을 추가한 언어
```
> JetBrains : 자바를 만든 회사인 IntelliJ IDEA의 개발사

---
### 개발된 이유
`가독성`과 `접근성` 때문이다

초장기 개발 언어와는 달리 요즘엔 `객체 지향`이면서 `변수 유형 유추` 및 `손쉬운 캡슐화`, `직관적인 기능`을 많이 갖는 함수를 많이 탑재한 더욱 사람의 언어와 비슷해지는 언어들이 나오는 추세이다

자바도 객체 지향 언어이지만 초장기에 개발된 만큼 절차 지향에 가까운 문법을 가지고 있다
때문에 개발 언어 트렌드에 맞게 `더욱 간결`하며, `생산성을 높일 수 있는 언어`가 필요했고 코틀린이 개발되었다

---
### 자바와 코틀린 문법 차이
자바
```java
public class RandomSort {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>();
        Random random = new Random();
        for (int i = 0; i < 100; i++) {
            numbers.add(randomNumber);
        }

        Collections.sort(numbers);
        for (Integer number: numbers) {
            System.out.println(number);
        }
    }
}
```
코틀린
```kotlin
fun main() {
    val numbers = nutableListOf<Int>()

    val random = Random()
    repeat(100){
        val randomNumber = random.nextInt(100) + 1
        numbers.add(randomNumber)
    }

    numbers.sort()

    numbers.forEach {println(it)}
}
```
---