# JAVA
---
## generic
```
데이터의 타입(data type)을 일반화한다는 것을 의미한다
```
제네릭은 클래스나 메서드에서 사용할 내부 데이터 타입을 컴파일 시에 `미리 지정`하는 방법이다

컴파일 시에 `미리 타입 겁사(type check)`을 수행할 때의 장점
```
1. 클래스나 메서드 내부에서 사용되는 객체의 타입 안전성을 높일 수 있음
2. 반환값에 대한 타입 변환 및 타입 검사에 들어가는 노력을 줄일 수 있다
```
---
### 제네릭의 선언 및 생성
자바에서 제네릭은 `클래스와 메서드`에만 이러한 방법으로 선언할 수 있다
```java
Ex)
class MyArray <T> {
    T element;
    vodi setElement(T element) {this.element = element;}
    T getElement() {return element};
}
```
`T`를 타입 변수(type variable)라고 하며, `임의의 참조형 타입`을 의미한다   
꼭 T 뿐만 아니라 어떠한 문자를 사용해도 상관없으며, 여러개의 타입변수는 `쉼표(,)`로 구분하여 명시할 수 있다   
타입 변수는 클래스에서뿐만 아니라 메서드의 `매개변수나 반환값`으로도 사용할 수 있다

제네릭 클래스(generic class)를 생성할 때에는 타입 변수 자리에 `사용 할 실제 타입`을 명시해야 한다
```java
MyArray<사용할 실제 타입> myArr = new MyArray();
```
> 자바에서 타입 변수 자리에 사용할 실제 타입을 명시할 때 기본 타입을 바로 사용할 수 없다
Integer와 같이 `래퍼(wrapper) 클래스`를 사용해야만 한다

---
### 제네릭의 제거 시기
자바 코드에서 선언되고 사용된 제네릭 타입은 컴파일 시 컴파일러에 의해 `자동으로 검사 되어 타입 변환`된다
그리고서 코드 내의 `모든 제네릭 타입은 제거`되어, 컴파일된 class 파일에는 어떠한 제네릭 타입도 `포함되지 않게` 된다

이런 식으로 동작하는 이유는 `제네릭을 사용하지 않는 코드와의 호환성을 유지`하기 위해서이다

---
### 타입 변수 제한
제네릭은 `T`와 같은 타입 변수(type variable)를 사용하여 `타입을 제한`한다
이때 `extends 키워드`를 사용하면 타입 변수에 특정 타입만을 사용하도록 제한할 수 있다
```java
ex)
class AnimalList<T extends LandAnimal> {...}
```
클래스의 타입 변수에 제한을 걸어 놓으면 `클래스 내부에서 사용된 모든 타입 변수에 제한`이 걸린다
인터페이스를 구현할 경우에도 implements 키워드가 아닌 `extends 키워드`를 사용해야 한다

클래스와 인터페이스를 동시에 상속받고 구현해야 한다면 `엠퍼센트(&)` 기호를 사용하면 된다

---
### 제네릭 메서드(generic method)
```
메서드의 선언부에 타입 변수를 사용한 메서드
```
타입 변수의 선언은 메서드 선언부에서 반환타입 바로 앞에 위치한다
```java
ex)
public static <T> void sort(...) {...}
```

```java
class AnimalList<T> {
    ...
    public static <T> void sort(List<T> list, Comparator<? super T> comp) {
        ...
    }
    ...
}
```
이때 제네릭 클래스에서 정의된 타입 변수 T와 제네릭 메서드에서 사용된 타입 변수 T는 전혀 별개의 것임을 주의해야한다

---
### 와일드카드(wild card)의 사용
```
이름에 제한을 두지 않음을 표현하는데 사용되는 기호

물음표(?) 기호를 사용하여 와일드카드를 사용할 수 있다
```
```java
문법
<?> // 타입 변수에 모든 타입을 사용할 수 있음
<? extends T> // T 타입과 T 타입을 상속받는 자손 클래스 타입만을 사용할 수 있음
<? super T> // T타입과 T 타입이 상속받은 조상 클래스 타입만을 사용할 수 있음
```