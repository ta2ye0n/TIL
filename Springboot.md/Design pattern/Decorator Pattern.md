# Spring boot
---
## Design pattern
---
### Decorator Pattern
```
대상 객체에 대한 기능 확장이나 변경이 필요할 때 객체의 결합을 통해 
서브 클래싱 대신 쓸 수 있는 유연한 대안 구조 패턴
```
![](https://blog.kakaocdn.net/dn/tgAeA/btroEAqroeM/TgDqkRkvDEROc3ihOkhrnk/img.png)
```
Componet(Interface) : 원본 객체와 장식된 객체 모두를 묶는 역할
Concretecomponent : 원본 객체(데코레이팅 할 객체)
Decorator : 추상화된 장식자 클래스
ConcreteDecorator : 구체적인 장식자 클래스
```
---
### 패턴 흐름
클래스 구조
```java
// 원본 객체와 장식된 객체 모두를 묶는 인터페이스
interface IComponent {
    void operation();
}

// 장식될 원본 객체
class ConcreteComponent implements IComponent {
    public void operation() {
    }
}

// 장식자 추상 클래스
abstract class Decorator implements IComponent {
    IComponent wrappee; // 원본 객체를 composition

    Decorator(IComponent component) {
        this.wrappee = component;
    }

    public void operation() {
        wrappee.operation(); // 위임
    }
}

// 장식자 클래스
class ComponentDecorator1 extends Decorator {

    ComponentDecorator1(IComponent component) {
        super(component);
    }

    public void operation() {
        super.operation(); // 원본 객체를 상위 클래스의 위임을 통해 실행하고
        extraOperation(); // 장식 클래스만의 메소드를 실행한다.
    }

    void extraOperation() {
    }
}

class ComponentDecorator2 extends Decorator {

    ComponentDecorator2(IComponent component) {
        super(component);
    }

    public void operation() {
        super.operation(); // 원본 객체를 상위 클래스의 위임을 통해 실행하고
        extraOperation(); // 장식 클래스만의 메소드를 실행한다.
    }

    void extraOperation() {
    }
}
```
클래스 흐름
```java
public class Client {
    public static void main(String[] args) {
        // 1. 원본 객체 생성
        IComponent obj = new ConcreteComponent();

        // 2. 장식 1 하기
        IComponent deco1 = new ComponentDecorator1(obj);
        deco1.operation(); // 장식된 객체의 장식된 기능 실행

        // 3. 장식 2 하기
        IComponent deco2 = new ComponentDecorator2(obj);
        deco2.operation(); // 장식된 객체의 장식된 기능 실행

        // 4. 장식 1 + 2 하기
        IComponent deco3 = new ComponentDecorator1(new ComponentDecorator2(obj));
    }
}
```
데코레이터 된 객체는 메서드를 호출할 때 장식한 메서드를 호출하여 반환 로직에 추가적으로 더 덧붙여서 `결과값을 반환`할 수 있다

---
### 장단점
**장점**   
- 데코레이터를 사용하면 서브 클래스를 만들때보다 훨씬 더 `유연하게 기능을 확장`할 수 있다

- 객체를 여러 데코레이터로 래핑하여 `여러 동작을 결합`할 수 있다
- 컴파일 타임이 아닌 `런타임에 동적`으로 기능을 변경할 수 있다
- 각 장식자 클래스마다 고유의 책임을 가져 `단일 책임 원칙(SRP)`을 준수한다
- 클라이언트 코드 수정없이 기능 확징이 필요하면 장식자 클래스를 추가하면 되므로 `개방 폐쇠 원칙(OCP)`을 준수한다
- 구현체가 아닌 인터페이스를 바라봄으로써 `의존 역전 원칙(DIP)`을 준수한다

**단점**   
-  만일 장식자 일부를 제거하고 싶다면, Wrapper 스택에서 `특정 wrapper`를 제거하는것이 어렵다

- 데코레이터를 조합하는 `초기 생성 코드`보기 안좋을 수 있다
    > ex) new(A(new B(new C(new D()))))
- 어는 장식자를 먼저 데코레이팅 하느냐에 따라 `데코레이터 스택 순서가 결정`지게 되는데, 만일 `순서에 의존하지 않는 방식`으로 데코레이터를 구현하기는 어렵다