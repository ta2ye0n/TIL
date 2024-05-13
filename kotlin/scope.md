# kotlin
---
## 스코프 함수
```
특정 객체의 컨텍스트 안에서 특정 동작(속성 초기화, 활용 등)을 실행하기 위한 목적만을 가진 함수
```
이 스코프 함수를 람다 함수로 사용할시 스코프를 형성하게 되는데 이 스코프 내에서는 객체의 이름을 참조할 필요 없이 객체에 접근하고 핸들링하기 편하게끔 해준다

종류로는 apply, run, with, also, let이 있다

---
### apply
```kotlin
inline fun <T> T.apply(block : T.() -> Unit): T {
		block()
        return this
 }
```
- 객체를 새로 생성하고 특정 변수에 할당하기 전에 `초기화 작업`을 하는 스코프를 만든다

- 함수 내에 모든 명령들이 수행되고 나면 명령들이 적용되어 `새로 생성된 객체를 반환`한다
- 반환 결과가 `객체 자신`이다
- 확장 함수이기 때문에 객체 컨텍스트를 `receiver(this)`로 이용이 가능하다

---
### run
```kotlin
inline fun <T,R> T.run(block : T.() -> R) : R {
		return block()
    }
```
- 반환하는 값이 객체가 아닌 `스코프 내에 실행된 값`이다
- 그러므로 특정 객체의 출력하거나 계산값으로 활용하는 등의 `핸들링을 할 때 사용`한다

- 확장함수이기 때문에 `receiver(this)`로 이요이 가능하다
- safe call(.?)을 붙여 `non-null`일 때만 실행이 가능하다

---
### with
```kotlin
inline fun <T, R> with(receiver : T, block: T.() -> R) : R{
		return receiver.block()
   }
```
- 확장 함수가 아니므로 컨텍스트 객체를 `argument`로 전달하며 람다의 내부에서는 확장함수로 적용되어 `reciever(this)`로 사용이 가능하다

---
### also
```kotlin
inline fun <T> T.also(block: (T) -> Unit) : T {
		block(this)
        return this
 }
```
- `생성된 인스턴스`를 반환한다

- `it`를 사용해 프로퍼티에 접근이 가능하다
- 객체의 프로퍼티를 전혀 사용하지 않거나 변경하지 않고 사용하는 경우에 유용하다
    > ex) 객체의 데이터 유효성 확인, 디버그, 로깅 등의 부가적인 목적

---