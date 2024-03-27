# kotlin
---
## 반복문
---
### for 문
**기본 for 문**   
```kotlin
for (변수명 : 타입 in 범위) {
    반복문 내용
}
```
```kotlin
ex)
// 1부터 10까지 반복하는 for 문
for(i : Int in 1..10)
    print(i)

// 변수 선언하여 반복
val len : Int = 10
for (i in 1..len)
    print(i)
```
- `until` : 마지막 숫자 전까지 반복
- `downTo` : 숫자가 증가가 아니라 감소하는 for문을 만들때 사용
- `step` : 증가, 감소 값을 설정할 때 사용한다
    > 음수는 지원하지 않는다
```kotlin
// until을 사용한 예제
for(i in 1 until len)
    print(i) // len이 10이므로 1부터 9까지만 반복된다

// step을 사용한 예제
for(i : Int in 1..10 step(2))
    print(i) // 1, 3, 5, 7, 9

// downTo를 사용한 예제
for(i in 10 downTo 1)
    print(i) // 10, 9, 8, 7, 6, 5, 4, 3, 2, 1
```

**배열과 리스트를 탐색하는 for문**   
```kotlin
for (i in 리스트 / 배열 / 컬렉션) {
    반복문 내용
}
```
- `reversed` : 배열을 거꾸로 탐색
- `count` : 배열 또는 리스트의 길이로 탐색 가능
- 인덱스와 원소 값을 함께 사용할 수 있다
```kotlin
val arr : Array<Int> = arrayOf(1, 2, 3, 4, 5)

// reversed을 사용한 예제
for (i in arr.reversed())
    print(i) // 5, 4, 3, 2, 1

// count를 사용한 예제
for (i in 0 until list.count())
    print(list[i])
```
---
### while 문
**while 문**   
```kotlin
var a: Int = 1
while(a <= 10) {
    print("${a++}")
}
```

**do-while 문**   
```kotlin
var b: Int = 10
do {
    print("${b--}")
} while (b > 0)
```

> 다른 언어들과 거의 유사함
---
### repeat
```kotlin
repeat(반복횟수) {
    반복할 내용
}
```
내부적으로 `for문`을 사용하는 `inline 함수`이다
인자로 `반복횟수`와 `action(반복할 함수)`를 전달하여 실행한다

```kotlin
ex)
repeat(3) { index ->
    println("Hello World !! $index")
}

// 이렇게도 사용 가능
println("Hello".repeat(3))
```
---
### while vs repeat
while문과 비교했을 때 repeat 함수는 `반복 횟수가 명확하게 제공`되기 대문에 `가독성`면에서 장점이 있다
또한 무한 루프에 빠지는 실수를 방지할 수 있다

- while 문을 주로 사용하는 상황
    - `복잡한 종료 조건`을 가질 경우
    - 조건이 loop 내부에서 `동적으로 변경`되는 경우
    - `무한루프`가 필요한 경우

반복 횟수가 명확하게 정해져있을 경우에는 `repeat`을 사용하는게 좋다

---
### foreach
collection이나 배열 등의 요소를 반복하는데 사용되는 함수
```kotlin
배열(coolection).forEach {println(it)}
```

for문보다 직관적이고 `가독성면`에서 좋다
만약 index 값이 필요하다면 `forEachIndexed`를 사용하면 된다

---