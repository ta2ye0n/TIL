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