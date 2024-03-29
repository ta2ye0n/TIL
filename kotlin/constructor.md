# kotlin
---
## 생성자
코틀린에서는 `하나의 주(primary) 생성자`와 `여러 개의 부(secondary) 생성자`를 사용할 수 있다
주 생성자는 클래스의 헤더로써 이름과 동일한 이름을 사용한다 

---
### 기본 생성자
```kotlin
class 클래스명 () {}
```
---
### 주 생성자 (Primary Constructor)
클래스 이름 뒤에 오는 괄호(`()`)로 둘러 쌓인 코드를 주 생성자라고 한다

**주생성자의 목적**
- 생성자 파라미터를 지정하는 것
- 생성자 파라미터 의해 초기화되는 프로퍼티를 정의하는 것

```kotlin
ex)
class User (name: String) {
    val name : String
}

clss User(val nickname: String)
```

클래스에서 인스턴스를 만들때에는 자바와 달리 `new키워드 없이` 생성자를 직접 호출하면 된다
```kotlin
val ex = User("예시")
```
---
### 부 생성자(Secondary Constructor)
클래스의 `본문 안에서 정의되는` 생성자이다
```kotlin
class User () {
    val name: String,
    val password: String

    constructor(name: String, password: String) : this() {
        this.name = name
        this.password = password
    }
}
```
---