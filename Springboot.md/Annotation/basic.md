# Annotation
Spring에서는 Annotation을 많이 사용한다   
`Annotation의 역할`
```
클래스와 메서드에 추가하여 다양한 기능을 부여하는 역할
특별한 의미를 부여하거나 기능을 부여하는 등 다양한 역할을 수행할 수도 있다
```
이러한 Annotation을 통하여 **코드량이 감소하고 유지보수하기 쉬우며, 생산성이 증가**된다

---
## 대표적인 어노테이션
---

### @Component
`개발자가 생성한 Class를 Spring의 Bean으로 등록`할 때 사용하는 Annotation이다 Spring은 해당 Annotation을 보고 Spring의 Bean으로 등록한다   
1개의 class 단위로 bean으로 등록 할때 설정한다
```java
@Compoent
public class Student {
    public Student() {
        System.out.println("hi");
    }
}

@Component(value="myman")
public class Student {
    public Student() {
        System.out.println("hi");
    }
}
```
Component에 대한 추가 정보가 없다면 `Class의 이름을 camelCase로 변경한 것이 Bean id로 사용`된다   
하지만 `@Bean과 다르게 @Component는 name이 아닌 value를 이용해 Bean의 이름을 지정`한다

---
### @ComponentScan
`@Component와 @Service, @Repository, @Controller, @Configuration이 붙은 클래스 Bean들`을 찾아서 `Context에 bean 등록`을 해주는 Annotation이다 

---
### @Bean
@Bean은 `개발자가 직접 제어가 불가능한 외부 라이브러리등을 Bean으로 만들려할 때 사용`되는 Annotation이다
> 1개의 외부 라이브러리로 부터 생성한 객체를 등록시 사용 (new로 객체를 생성 후 직접 bean으로 등록 할 때 사용)
```java
@Configuration
public class ApplicationConfig {
    @Bean
    public ArrayList<String> array(){
        return new ArrayLsit<String>();
    }
}
```
ArrayList 같은 라이브러리등을 Bean으로 등록하기 위해서는 별도로 `해당 라이브러리 객체를 반환하는 Method를 만들고 @Bean Annotation을 사용`하면 된다   
위의 경우 @Bean에 아무런 값을 지정하지 않았으므로 `Method 이름을 camelCase로 변경한 것이 Bean id로 등록`된다
> method 이름이 arrayList()인 경우 arrayList가 Bean id

```java
@Configuration
public class ApplicationCongif {
    @Bean(name="myarray")
    public ArrayList<String> array() {
        return new ArrayList<String> ();
    }
}
```
위와 같이 `@Bean에 name이라는 값을 이용하면 자신이 원하는 id로 Bean을 등록`할 수 있다   
Configuration 클래스에서 외부라이브러리 관련 객체를 미리 객체화 시켜놓을 때 많이 사용한다

---
### Autowired
속성(field), setter method, constructor(생성자)에서 사용하며 `Type에 따라 알아서 Bean을 주입` 해준다
무조건적인 객체에 대한 `의존성을 주입`시킨다
이 Annotation을 사용할 시, 스프링이 자동적으로 값을 할당한다

즉, Dependency Injection를 위한 곳에 사용된다

필드, 생성자, 입력 파라미터가 여러 개인 메소드 (@QUalifier는 메소드의 파라미터)에 적용 가능하다
`Type을 먼저 확인한 후 못 찾으면 Name에 따라 주입`한다
> Name으로 강제하는 방법 : @Qualifier을 같이 명시  

```
@Bean을 주입받는 방식 (3가지)
- @Autowired
- setter
- 생성자 (@AllArgsConstructor 사용) -> 권장방식
```
---
### @Controller
Spring에게 해당 Class가 Controller의 역할을 한다고 명시하기 위해 사용하는 Annotation이다
```java
@Controller                   // 이 Class는 Controller 역할을 합니다
@RequestMapping("/user")      // 이 Class는 /user로 들어오는 요청을 모두 처리합니다.
public class UserController {
    @RequestMapping(method = RequestMethod.GET)
    public String getUser(Model model) {
        //  GET method, /user 요청을 처리
    }
}
```

### @RestController
Spring에서 `Controller 중 View로 응답하지 않는, Controller의 의미`한다   
method의 반환 결과를 JSON형태로 반환한다
> JavaScript Object Notation (JSON)은 Javascript 객체 문법으로 구조화된 데이터를 표현하기 위한 문자 기반의 표준 포맷이다

이 Annotation이 적혀있는 Controller의 method는 HttpRespones로 바로 응답이 가능하다   
@ResponseBody 역할을 자동적으로 해주는 Annotation이다   
@Controller + @ResponseBody를 사용하면 `@ResponseBody를 모든 메소드에서 적용`한다

### @Controller와 @RestController의 차이
- @Controller   
`API와 view를 동시에 사용하는 경우에 사용`한다   
대신 `API 서비스로 사용하는 경우는 @ResponseBody를 사용하여 객체를 반환`한다   
view(화면) return이 주목적이다
- @RestController
`view가 필요없는 API만 지원하는 서비스에서 사용`한다   
Spring 4.0.1부터 제공   
`@RequestMapping 메서드가 기본적으로 @ResponseBody 의미를 가정`한다   
data(json,xml 등) return이 주목적이다

즉, **@RestController = @Controller + @ResponseBody** 이다

---
