# JAVA
---
## enum
```
열거형
상수로 구성된 클래스
```
클래스처럼 변수와 메서드를 가질 수 있지만, 상속이나 인스턴스는 생성할 수 없으며, enum 값은 상수로 public, static, final 속성을 가지고 있어 변경될 수 없다

---
### 장점
- 데이터 값의 `의미`를 명확히 알 수 있다
- 컴파일 시 `데이터 타입 및 유효성 체크`를 할 수 있다
- 허용 가능한 값들을 제한하여 `유형 안전(type safe)`을 제공한다
- 자체 클래스 상수와 달리 `switch문`에서도 사용할 수 있다

---
### 선언 방법
```java
ex)
enum Week {
    SUN, MON, TUE, WED, THU, FRI, SAT
}
```
- `enum` 키워드로 정의

- 열거형의 이름은 보통 클래스명과 같이 `첫 글자를 대문자`로 시작
- `{}`안에 열거값은 `,`로 구분
- 상수와 같이 `대문자` 사용

열거형은 클래스 안에서도 선언할 수 있도, 클래스 밖에서도 선언할 수 있다

---
### 참조 방법
enum 타입 객체도 하나의 데이터 타입이므로 변수를 선언하고 사용하면 된다
```java
열거타입 변수 = 열거타입.열거상수;

ex) Week monday = Week.MONDAY;
Week sunday = Week.SUNDAY;
```
enum 타입은 `특수한 클래스`이다   
즉, primitive 타입이 아닌 `referece 타입`으로 분류되며, 그래서 enum 상수값은 `힙(heap)영역`에 저장되게 된다

---
### 메서드
- `valueOf(String str)` : 문자열 str과 일치하는 열거 값 반환

- `values()` : 열거값 전부를 배열로 반환
- `ordinal()` : 열거값의 순서를 반환
- `name` : 열거 객체의 문자열을 반환
- `compareTo()` : 열거 객체를 비교해서 순번 차이를 리턴

---
### java.lang.Enum
모든 클래스가 Object 클래스를 자동 상속하는 것처럼, Enum 클래스도 무조건 `java.lang.Enum`이라는 클래스를 상속 받는다
그리고 클래스에 정의되어 있는 메서드를 가져와 사용하는 것이다
```java
public abstract class Enum<E extends Enum<E>> implements Comparable<E>, Serializable {
    private final String name;
    private final int ordinal;

    protected Enum (String name, int ordinal) {
        this.name = name;
        this.ordinal = ordinal;
    }
}
```
- `String name` : Enum (열거)상수 이름
- `int ordinal` : Enum의 순서, 상수가 선언된 순서대로 0부터 증가
- `protected Enum` 생성자 : 컴파일러에서 자동으로 호출되도록 해놓은 생성자
하지만 개발자가 이 생성자를 호출할 수 없다

---
### 오버라이딩 하지 못하는 메서드
Enum 클래스는 개발자들이 Object 클래스 중 4개의 메서드를 오버라이딩하지 못하도록 메서드를 `final`화 하여 막아놓았다
왜냐면 enum은 `고유한 상수`이기 때문에 오버라이딩해서 자기 마음대로 바꿔버리면 `고유성이 깨지기 때문`이다

|메서드|내용|
|:----:|------|
|clone()|객체를 복제하기 위한 메서드<br> 하지만 enum 클래스에서 사용하면 안된다 <br> 호출될 경우 `CloneNotSupportedException`이라는 예외를 발생시킨다|
|finalize()|GC가 발생할 때 처리하기 위한 메서드|
|hashCode()|int 타입의 해시 코드 값을 리턴하는 메서드|
|equals()|두 개의 객체가 동일한지를 확인하는 메서드|