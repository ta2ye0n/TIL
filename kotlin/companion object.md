# Kotlin
---
## Companion object
클래스가 메모리에 올라갈때, 동시에 Companion object가 인스텬스로서 힙에 올라간다하여 `동반 객체`라고 한다

자바의 `static` 개념과 비슷해 보이지만 `자바의 static 개념이 아니다` 라는 말이 많다

---
### 자바 static
자바와 코틀린 모두 JVM을 통해 실행된다

![](https://velog.velcdn.com/images/yongin01/post/a4375368-8379-40fd-a749-367dda598c46/image.png)

- Method Area   
클래스에 대한 정보와 함꼐 클래스 변수(static variable)가 저장 되는 곳이다
런타임 상수 풀, 멤버 변수, 클래스 변수, 생성자 및 메서드를 저장한다
이 곳에 저장되는 정보가 `static한 정보`이다

- Heap Area   
`동적으로 할당되는 정보`가 저장된다
흔히 말하는 붕어빵 틀에 찍힌 붕어빵들이 생성되기도 하고 가비지 컬렉팅되어 없어지기도 한다

---
### Companion object
#### Object 키워드와의 연관성
- `객체 선언`   
object 키워드는 자바에서 static 키워드와 new 키워드를 대신한다
`클래스 정보 적재와 객체 선언이 동시`에 이루어진다

companion object도 object 키워드와 같은 역할을 한다

object 키워드와 companion object의 차이점
```
1. 클래스 내부에 있는 object를 굳힌 형태이다
2. companion object 내부에 있는 변수, 메서드에 대한 접근을 더 자연스럽게 보이도록 눈속임 했다
```