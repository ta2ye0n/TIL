# Spring boot
---
## Design pattenr
---
### 프록시 패턴 (Proxy pattern)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb3pVn9%2FbtrXv4wX7hZ%2FdKNOALhGqYqpthIcdVRnF0%2Fimg.png)
```
하나의 개체(프록시)가 다른 개체(주체 또는 서비스)에 대한 액세스를 제어할 수 있도록 하는 패턴이다

일반적으로 프록시는 다른 무언가와 이어지는 인터페이스의 역할을 하는 클래스이다
프록시는 어떠한것과도 인터페이스의 역할을 수행할 수 있다
```
어떤 객체를 사용하고자 할때, 객체를 `직접적으로 참조하는 것`이 아닌 해당 객체를 대항하는 객채를 통해 대상 객체에 접근하는 방식을 사용하면 해당 객체가 메모리에 존재하지 않아도 `기본적인 정보를 참조하거나 설정`할 수 있고, 실제 객체의 기능이 필요한 시점까지 객체의 생성을 미룰 수 있다

---
### 장단점
**장점**   
- 사이즈가 큰 객체가 `로딩되기 전`에도 프록시를 통해 참조를 할 수 있다

- 실제 객체의 `public, protected 메서드`를 숨기고 인터페이스를 통해 `노출`시킬 수 있다
- 로컬에 있지 않고 `떨어져있는 객체`를 사용할 수 있다
- 원래 객체에 접근에 대해 `사전처리`를 할 수 있다

**단점**   
- 객체를 생성할 때 한 단계를 거치게 되므로, `빈번한 객체 생성`이 필요한 경우 성능이 저하될 수 있다
- 프록시 내부에서 객체 생성을 위해 `스레드 생성, 동기화`가 구현되어야하는 경우 성능이 저하 될 수 있다

- 로직이 난해해져 `가독성이 떨어질 수`있다

---
### 프록시 패턴의 종류
1. `가상프록시` 
    ```
    꼭 필요로 하는 시점까지 객체의 생성을 연기하고 해당 객체가 생성된 것처럼 동작하도록 만드는 패턴
    ```
    프록시 클래스에서 작은 단위의 작업을 처리하고 `리소스가 많이 요구`되는 작업들이 필요할 경우만 주체 클래스를 사용하도록 구현한다

2. `원격프록시`
    ```
    원격 객체에 대한 접근을 제어 로컬 환경에 존재하며,
    서로 다른 주소 공간에 있는 객체에 대해 마치 같은 주소 공간에 있는 것 처러 동작하게 하는 패턴
    ```
    ex) Google Docs

3. `보호프록시`   
    ```
    주체 클래스에 대한 접근을 제어하기 위한 경우에 객체에 대한 접근 권한을 
    제어하거나 객체마다 접근 권한을 달리하고 싶을 경우 사용하는 패턴
    ```
    프록시 클래스에서 클라이언트가 주체 클래스에 대한 접근을 `허용하지 말지 결정`하도록 할 수 있다