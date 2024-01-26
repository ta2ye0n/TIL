# Spring boot
---
## Design Pattern
---
### Builder Pattern 종류
빌더 패턴에는 다른 디자인 패턴과는 다르게 두가지 디자인 종류가 존재한다
`GoF의 디자인 패턴`에서 소개하는 빌더 패턴과 `d이펙티브 자바(Effective Java)` 책에서 소개하는 빌더 패턴 구조가 서로 다르기 때문이다
```
이펙티브 자바 : 생성지 지정해야 할 인자가 많을 때 사용
               객체의 일관성 불변성이 목적
GoF : 객체의 생성 단계 순서를 결정해두고 각 단계를 다양하게 구현하고 싶을 때 사용
```
> 두 책의 관점이 다르고 GoF는 1994년에 발매되었고 이펙티브 자바가 2001년에 나중에 나왔다
---
### 심플 빌더 패턴 (Effective Java)
보통 개발자들이 빌더 패턴을 말할 때 정의되는것이 이펙티브 자바에서 소개한 빌더 패턴이다
GoF와 구분하기 위해 `심플 빌더 패턴(Simple Builder Pattern)` 이라고도 불린다

심플 빌더 패턴은 `생성자가 많은 경우` 또는 `변경 불가능한 불변 객체`가 필요한 경우 코드의 `가독성`과 `일관성`, `불변성`을 유지하는 것에 중점을 둔다

보통 아는 빌더 패턴과 차이가 거의 없지마 Builer 클래스가 구현한 클래스의 `정적 내부 클래스(Static Inner Class)`로 구현되는 점이 다르다

**Static inner class로 구현되는 이유**   
1. 하나의 빌더 클래스는 `하나의 대상 객체 생성`만을 위해 사용된다   

2. 대상 객체는 오로지 `빌더 객체에 의해 초기화` 된다   
생성자를 외부에 노출시키면 안되기 때문에 생성사를 private로 하고, 내부 빌더 클래스에서 생성자를 호출함으로써 오로지 빌더 객체에 의해 초기화 되도록 설계 할 수 있다

3. `static`으로 선언해주는 이유   
정적 내부 클래스는 외부 클래스의 인스턴스 없이도 생성할 수 있기 때문이다

4. `메모리 누수 문제` 때문에 static으로 내부 클래스를 정의해줘야한다

---