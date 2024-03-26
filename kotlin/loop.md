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