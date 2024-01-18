# Spring boot
---
## Design Pattern
---
### Adaptor Pattern
![](https://velog.velcdn.com/images%2Fnewtownboy%2Fpost%2F261f7abf-d13c-444c-9296-17632ede3add%2Fimage.png)
```
호환성이 없는 인터페이스 때문에 함께 동작할 수 없는 클래스들을 함께 작동해주도록 변환해주는 패턴
어댑터를 이용하면 인터페이스 호환성 문제 때문에 같이 쓸 수 없는 클래스들을 연결해서 사용할 수 있다
```
기존 시스템에서 새로운 업체에서 제공하는 기능을 사용하려고 할때 서로 간의 인터페이스를 어댑터를 일치시켜줌으로써 `호환성 및 신규 기능 확장`을 할 수 있다고 보면 된다

> 어댑터가 Legecy 인터페이스를 감싸서 새루운 인터페이스로 변환하기 때문에 `Wrapper 패턴`이라고도 불린다

---
### 어댑터 패턴 구조
```
기존 시스템의 클래스를 상속(Inheritance) 해서 호환 작업을 해주냐
합성(Composition)해서 호환 작업을 해주냐에 따라 나뉜다
```

**객체 어댑터(Object Adaptor)**   
- 합성된 멤버에게 `위임`을 이용한 어댑터 패턴
    > 위임: 자기가 해야 할 일을 클래스 멤버 객체의 메서드에게 다시 시킴으로써 목적을 달성하는 것

- 합성을 활용했기 때문에  `런타임 중에 Adaptee(Service)가 결정`되어 유연하다
    - 그러나  Adaptee(Service) 객체를 `필드 변수`로 저장해야 되기 때문에 `공간 차지 비용`이 든다

![](https://refactoring.guru/images/patterns/diagrams/adapter/structure-object-adapter.png?id=33dffbe3aece294162440c7ddd3d5d4f)
```
Adaptee(Service) : 어댑터 대상 객체 기존 시스템 / 외부 시스템/ 써드파티 라이브러리
Target(Client Interface) : Adapter 가 구현하는 인터페이스
Adapter : Client와 adaptee(Service) 중간에서 호환성이 없는 둘을 연결시켜주는 역할
Client 기존 시스템을 어댑터를 통해 이용하려는 쪽
```
```java
// Adaptee : 클라이언트에서 사용하고 싶은 기존의 서비스 (하지만 호환이 안되서 바로 사용 불가능)
class Service {

    void specificMethod(int specialData) {
        System.out.println("기존 서비스 기능 호출 + " + specialData);
    }
}

// Client Interface : 클라이언트가 접근해서 사용할 고수준의 어댑터 모듈
interface Target {
    void method(int data);
}

// Adapter : Adaptee 서비스를 클라이언트에서 사용하게 할 수 있도록 호환 처리 해주는 어댑터
class Adapter implements Target {
    Service adaptee; // composition으로 Service 객체를 클래스 필드로

    // 어댑터가 인스턴스화되면 호환시킬 기존 서비스를 설정
    Adapter(Service adaptee) {
        this.adaptee = adaptee;
    }

    // 어댑터의 메소드가 호출되면, Adaptee의 메소드를 호출하도록
    public void method(int data) {
        adaptee.specificMethod(data); // 위임
    }
}

---------------------------------------------------------------------------------

class Client {
    public static void main(String[] args) {
        // 1. 어댑터 생성 (기존 서비스를 인자로 받아 호환 작업 처리)
        Target adapter = new Adapter(new Service());

        // 2. Client Interfac의 스펙에 따라 메소드를 실행하면 기존 서비스의 메소드가 실행된다.
        adapter.method(1);
    }
}
```

**클래스 어댑터(Class Adaptor)**   
- `클래스 상속`을 이용한 어댑터 패턴
    - Adaptee(Service)를 상속했기 때무에 따로 `객체 구현없이 바로 코드 재사용`이 가능하다
    - 상속은 대표적으로 기존에 구현된 코드를 재사용하는 방식이지만, 자바에서는 `다중 상속 불가 문제` 때문에 전반적으로 `권장하지 않는 방법`이다

![](https://refactoring.guru/images/patterns/diagrams/adapter/structure-class-adapter.png?id=e1c60240508146ed3b98ac562cc8e510)
```
Adaptee(Service) : 어댑터 대상 객체 기존 시스템 / 외부 시스템/ 써드파티 라이브러리
Target(Client Interface) : Adapter 가 구현하는 인터페이스
Adapter : Client와 adaptee(Service) 중간에서 호환성이 없는 둘을 연결시켜주는 역할
Client 기존 시스템을 어댑터를 통해 이용하려는 쪽
```
```java
// Adaptee : 클라이언트에서 사용하고 싶은 기존의 서비스 (하지만 호환이 안되서 바로 사용 불가능)
class Service {

    void specificMethod(int specialData) {
        System.out.println("기존 서비스 기능 호출 + " + specialData);
    }
}

// Client Interface : 클라이언트가 접근해서 사용할 고수준의 어댑터 모듈
interface Target {
    void method(int data);
}

// Adapter : Adaptee 서비스를 클라이언트에서 사용하게 할 수 있도록 호환 처리 해주는 어댑터
class Adapter extends Service implements Target {

    // 어댑터의 메소드가 호출되면, 부모 클래스 Adaptee의 메소드를 호출
    public void method(int data) {
        specificMethod(data);
    }
}
----------------------------------------------------------------------------
class Client {
    public static void main(String[] args) {
        // 1. 어댑터 생성
        Target adapter = new Adapter();

        // 2. 인터페이스의 스펙에 따라 메소드를 실행하면 기존 서비스의 메소드가 실행된다.
        adapter.method(1);
    }
}
```
---
### 패턴 사용 시기
- 레거시 코드를 사용하고 싶지만 새로운 인터페이스가 `레거시 코드와 호환되지 않을 때`

- 이미 만든 것을 재사용하고자 하나 `재사용 가능한 라이브러리를 수정 할 수 없을 때`
- 이미 만들어진 클래스를 `새로운 인터페이스(API)`에 맞게 개조할 때
- 소프트웨어의 `구 버전과 신 버전을 공존`시키고 싶을 때

---
### 장단점
**장점**   
- 프로그램의 기본 비즈니스 로직에서 인터페이스 또는 데이터 변환 코드를 분리할 수 있기 때문에 `단일 책임 원칙(SRP)`을 만족한다

- 기존 클래스 코드를 건들지 않고 클라이언트 인터페이스를 통해 어댑터와 작동하기 때문에 `개방 폐쇄 원칙(OCP)`을 만족한다  
- 만일 추가로 필요한 메서드가 있다면 어댑터에 빠르게 만들 수 있다   
버그가 발생해도 개존의 클래스에서 버그가 없으므로 `Adapter역할의 클래스를 중점적`으로 조사하면 되고, `프로그램 검사`도 쉬어진다

**단점**   
- 새로운 인터페이스와 어댑터 클래스 세트를 도입해야 하기 때문에 `코드의 복잡성`이 증가한다
- 때로는 `직접 서비스(Adaptee) 클래스를 변경하는 것이 간단할 수 있는 경우`가 있기 때문에 `신중히 선택` 해야한다