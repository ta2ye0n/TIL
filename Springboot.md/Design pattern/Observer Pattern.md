# Spring boot
---
## Design Pattern
---
### Observer Pattern(옵저버 패턴)
```
옵저버(관찰자)들이 관찰하고 있는 대상자의 상태가 변화가 있을 때마다
대상자는 직접 목록을 관찰자들에게 통지하고, 관찰자들은 알림을 받아 조치를 취하는 행동 패턴
```
다른 디자인 패턴들과 다르게 `일대다(one-to-many) 의존성`을 가지는데 주로 분산 이벤트 핸들링 시스템을 구현하는데 사용된다

---
### 옵저버 패턴 흐름
![](https://chaelin1211.github.io/img/posts/inPost/observer-01.png)
- 옵저버 패턴에는 한개의 `관찰 대상자(subject)`와 일 대 다 관계로 구성되어 있다

- Observer 패턴에서는 관찰 대상 Subject의 상태가 바뀌면 변경사항을 옵저버한테 통보해준다 (notify)
- 대상자로부터 통보를 받은 Observer는 값을 `바꿀수도`있고, `삭제하는 등 적절히 대응`한다 (update, register)
- 또한 Observer들은 언제든 Subject의 그룹에서 추가 / 삭제 될 수 있다

---
### 패턴 사용 시기
- 입이 `한정된 시간`, `특정한 케이스`에만 다른 객체를 `관찰`해야 하는 경우

- 대상 객체의 상태가 변경될 때마다 `다른 객체의 동작을 트리거` 해야할 때
- 한 객체의 상태가 변경되면 `다른 객체도 변경`해야 할 때   
그런데 어떤 객체들이 변경되어야 하는지 `몰라도 될때`
- `MVC 패턴`에서도 사용됨 (Model, View, Controller)
    - Model과 View의 관계는 Observer 패턴의 Subject 역할과 Observer 역할의 관계에 대응된다
    - 하나의 Model에 복수의 View가 대응한다

---
### 장단점
**장점**    
- Subject의 상태 변경을 `주기적으로 조회`하지 않고 `자동으로 감지`할 수 있다

- 발행자의 코드를 변경하지 않고도 새 구독자 클래스를 도입할 수 있어 `개방 폐쇄 원칙(OCP)` 준수한다
- 런타임 시점에서 발행자와 구독 알림 관계를 맺을 수 있다
- 상태를 변경하는 객체(subject)와 변경을 감지하는 객체(Observer)의 관계를 느슨하게 유지할 수 있다 (`느슨한 결합`)

**단점**   
- 구독자는 알림 순서를 제어할 수 없고, `무작위 순서`로 알림을 받는다
    > 하드 코딩으로 구현할수는 있겠지만, `복잡성과 결합성`만 높아지기 때문에 추천되지 않는 방법

- 자주 구성하면 구조와 동작을 알아보기 힘들어져 `코드 복잡도`가 증가한다
- 다수의 옵저버 객체를 등록 이후 해지하지 않는다면 `메모리 누수`가 발생할 수도 있다

---
### 클래스 구조
``` java
// 관찰 대상자 / 발행자
interface ISubject {
    void registerObserver(IObserver o);
    void removeObserver(IObserver o);
    void notifyObserver();
}

class ConcreteSubject implements ISubject {
    // 관찰자들을 등록하여 담는 리스트
    List<IObserver> observers = new ArrayList<>();

    // 관찰자를 리스트에 등록
    @Override
    public void registerObserver(IObserver o) {
        observers.add(o);
        System.out.println(o + " 구독 완료");
    }

    // 관찰자를 리스트에 제거
    @Override
    public void removeObserver(IObserver o) {
        observers.remove(o);
        System.out.println(o + " 구독 취소");
    }

    // 관찰자에게 이벤트 송신
    @Override
    public void notifyObserver() {
        for(IObserver o : observers) { // 관찰자 리스트를 순회하며
            o.update(); // 위임
        }
    }
}

-------------------------------------------------------------------------------

// 관찰자 / 구독자
interface IObserver {
    void update();
}

class ObserverA implements IObserver {
    public void update() {
        System.out.println("ObserverA 한테 이벤트 알림이 왔습니다.");
    }

    public String toString() { return "ObserverA"; }
}

class ObserverB implements IObserver {
    public void update() {
        System.out.println("ObserverB 한테 이벤트 알림이 왔습니다.");
    }

    public String toString() { return "ObserverB"; }
}
```
---