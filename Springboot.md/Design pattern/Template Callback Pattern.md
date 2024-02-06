# Spring boot
---
## Design Pattern
---
### Template Callback Pattern
```
스프링 프레임워크에서 DI(Dependency injection) 의존성 주입에서 사용하는 특별한 전략 패턴
```
> GOF 디자인 패턴은 아니고 `전략 패턴의 확장판` 정도로 보면된다

복잡하지만 바뀌지 않는 일정한 패턴을 갖는 흐름이 존재하고 그중 일부분만 자주 바꿔서 사용해야 하는 경우에 적합한 패턴이다

---
### 장단점
**장점**   
- 별도의 전략 클래스 없이 전략을 사용하는 메서드에 매개변수값으로 전략 로직을 넘겨 실행하기 때문에 `전략 객체를 일일히 만들 필요가 없다`

- 외부에서 어떤 전략을 `사용하는지 감추고 중요한 부분`에 집중 할 수 있다


**단점**    
- 스프링 클라이언트에서 DI를 사용하지 않게 되면 `Bean`으로 등록되지 않아 싱글톤 객체가 되지 않게 된다

- 인터페이스를 사용하지만 실제 사용할 클래스를 직접 선언하기 때문에 `결합도가 증가`하게 된다
    > 그렇다고 해서 결합도를 `낮추는 행위`을 할 필요는 없다

---
### 콜백(Callback)
```
하나의 오브젝트르 다른 오브젝트의 메서드에 매개변수로 넘거주는 실행가능한 코드
```
코드가 호출은 되는데 코드를 `넘겨준 곳의 뒤`에서 실행된다
필요에 따라 즉시 실행할 수도 있고 나중에 실행할 수도 있다

**자바**   
자바의 메서드는 일급 객체가 아니기 때문에 콜백 행위를 하지 못하였다
하지만 자바 8에서 등장한 `람다 함수`를 통해 콜백을 구현할 수 있게 되었다
```java
interface IAdd {
    int add(int x, int y);
}
 
public class Main {
    public static void main(String[] args) {
    	int n = result( (x, y) -> x + y ); // 메소드의 매개변수에 람다식을 전달
        System.out.println(n); // 3
    }
    
    public static int result(IAdd lambda) {
    	return lambda.add(1,2);
    }
}
```

**자바 스크립트**   
간단하게 함수를 변수에 할당하고 함수의 인자로 넘겨주면 콜백이다
```javascript
// 콜백 함수
const callback = function(num) {
	return ++num;
}

// 콜백을 함수의 매개변수로 넘김
function increaseNum(num, callback) {
	let result = callback(num);
    console.log(result);
}

increaseNum(1, callback); // 2
```
---