# Spring boot
---
## Design Pattern
---
### Command Pattern
```
실행될 기능 캡슐화함으로써 주어진 여러 기능을 실행할 수 있는 
재사용성이 높은 클래스를 설계하는 패턴
```
이벤트가 발생했을 때 실행될 기능이 다양하면서도 변경이 필요한 경우에 이벤트를 발생시키는 클래스를 변경하지 않고 재사용하고자 할 때 유용하다

실행될 기능을 `캡슐화`함으로써 기능의 실행을 요구하는 호출자(Invoker)클래스와 실제 기능을 실행하는 수진자 (Reciver) 클래스 사이의 `의존성을 제거`한다

---
### 패턴 구조
![](https://images.velog.io/images/ayoung0073/post/3f6fbd8a-61d1-4bee-b4d7-aac07238234c/image.png)
```
- Command : execute() 메서드를 선언하여 Receiver에서 수행할 연산을 구체화하는 방법을 정의

- ConcreteCommand : Command 인터페이스를 구현하고 이를 통해 Receiver 클래스의 함수를 호출
    - 일반적으로 execute() 함수에서 수행

- Invoker : 사용자의 요청을 Command 객체로 변환하며, 객체를 저장하고 실행하는 역할

- Receiver : 요청을 수행하는데 필요한 실제 작업을 구현한 클래스
```
---