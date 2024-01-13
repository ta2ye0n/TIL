# Spring boot
---
## Design pattern
---
### 팩토리 메서드 패턴 (Factory Method pattern)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbGSapI%2FbtrXrUuRTbI%2FGE3mdXKb38rJFkJMqHIKm0%2Fimg.png)
```
객체지향 디자인 패턴
부모(상위) 클래스에 알려지지 않은 구체 클래스를 생성하는 패턴이며,
자식(하위) 클래스가 어떤 객체를 생성할지 결정도록 하는 패턴이다
부모 클래스 코드에 구체 클래스 이름을 감추기 위한 방법으로도 사용된다
```
---
### 사용 방법
제품(Product) 클래스
```java
EX)
// 제품 객체 추상화 (인터페이스)
interface IProduct {
    void setting();
}

// 제품 구현체
class ConcreteProductA implements IProduct {
    public void setting() {
    }
}

class ConcreteProductB implements IProduct {
    public void setting() {
    }
}
```
공장(Factory) 클래스
```java
EX)
// 공장 객체 추상화 (추상 클래스)
abstract class AbstractFactory {

    // 객체 생성 전처리 후처리 메소드 (final로 오버라이딩 방지, 템플릿화)
    final IProduct createOperation() {
        IProduct product = createProduct(); // 서브 클래스에서 구체화한 팩토리 메서드 실행
        product.setting(); // .. 이밖의 객체 생성에 가미할 로직 실행
        return product; // 제품 객체를 생성하고 추가 설정하고 완성된 제품을 반환
    }

    // 팩토리 메소드 : 구체적인 객체 생성 종류는 각 서브 클래스에 위임
    // protected 이기 때문에 외부에 노출이 안됨
    abstract protected IProduct createProduct();
}

// 공장 객체 A (ProductA를 생성하여 반환)
class ConcreteFactoryA extends AbstractFactory {
    @Override
    public IProduct createProduct() {
        return new ConcreteProductA();
    }
}

// 공장 객체 B (ProductB를 생성하여 반환)
class ConcreteFactoryB extends AbstractFactory {
    @Override
    public IProduct createProduct() {
        return new ConcreteProductB();
    }
}
```
---
### 장점
- 생성자(Creator)와 구현객체(concrete product)의 `강한 결합을 피할 수` 있다

- 팩토리 메서드를 통해 객체의 생성 후 `공통으로 할 일을 수행`하도록 지정해 줄 수 있다
- 캡슐화, 추상화를 통해 생성되는 `객체의 구체적인 타입`을 감출 수 있다

- `단일 책임 원칙` 준수   
객체 생성 코드를 한곳으로 이동하여 코드를 유지보수하기 쉽게 할 수 있기 때문
- `개방 / 폐쇠 원칙` 준수   
기존 코드를 수정하지 않고 새로운 유형의 인스턴스를 프로그램에 도입할 수 있기 때문 (확장성 있는 전체 프로젝트 구성이 가능)

---
### 단점
- 각 제품 구현체마다 팩토리 객체들을 모두 구현해주어야 하기 때문에, 구현체가 늘어날때 마다 `팩토리 클래스`가 증가하여 서브 클래스 수가 폭발한다

- `코드의 복잡성`이 증가한다