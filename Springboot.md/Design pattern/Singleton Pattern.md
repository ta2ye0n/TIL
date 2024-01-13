# Spring boot
---
## Design pattern
---
### 싱글톤 패턴 (Singleton pattern)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZzBq1%2FbtrXoDm8BrT%2Ft8DxbZwlW79VxL2kxU1h9K%2Fimg.png)
```
싱글톤 패턴을 따르는 클래스는 생성자가 여러 차례 호출 되더라도
실제로 생성되는 객체는 하나이고 최초 생성 이후에 호출된 생성자는 최최의 생성자가 생성한 객체를 리턴한다
```

스프링은 기본적으로 Bean을 추가할 때 하나의 인스턴스를 컨테이너에 등록하고 사용하게 되어있다    
이미지에서 보이듯이 1개의 컨테이너 당 `하나의 싱글톤 인스턴스`를 갖는 구조다   
어플리케이션 내부에 여러개의 컨테이너를 가지는 구조인 경우 전역적 싱글톤이 아니라 `각 컨테이너에서의 싱글톤 인스턴스`라는 걸 알 수 있다

---
### 사용 방법
```java
public class Singleton {

    private static Singleton instance = new Singleton();
    
    private Singleton() {
        // 생성자는 외부에서 호출못하게 private 으로 지정해야 한다.
    }

    public static Singleton getInstance() {
        return instance;
    }

    public void say() {
        System.out.println("hi, there");
    }
}
```
---
### 문제점
- `의존성이 높아진다`   
객체를 미리 생성한 뒤에 필요한 경우 정적 메서드를 이용하기 때문에 클래스 사이의 의존성이 높아지게 된다(= 높은 결합)

- `privte 생성자 때문에 상속이 어렵다`   
기본 생성자를 private로 만들었기에 자식 클래스를 만들 수 없게된다
즉, `다형성`을 적용하지 못한다는 문제로 이어진다

- `테스트하기가 힘들다`   
서로 독립적이어야하는 단위 테스트를 하는데 문제가 된다   
독립적인 테스트가 진행이 되려면 전역에서 상태를 공유하고 잇는 인스턴스의 상태를 매번 초기화해야 한다   
초기화 하지 않으면 `전역에서 상태를 공유 중`이기 때문에 테스트가 정상적으로 수행되지 못할 가능성이 존재한다

이러한 문제점들 때문에 싱글톤 패턴은 `안티패턴`이라고 불리기라도 한다