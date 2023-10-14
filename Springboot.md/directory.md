# Directory
---
## Directory 구조
---
### 레이어 계층형
Springboot 프로젝트를 처음 생성하면 아무런 디렉토리 구조가 잡혀있지 않다
그래서 사용자가 다양하게 내부 레이아웃을 구성할 수 있다

보편적으로는 애플리케이션 아키텍쳐(MVC)를 기반으로 설계한다
![](https://velog.velcdn.com/images/jmjmjmz732002/post/de4448ee-583c-4c42-9bfe-a107281f8bbe/image.png)
- Controller : 사용자 요청과 이에 대한 응답 반환의 전반적인 처리가 일어난 영역
- Service : Controller와 Repository 사이에서 실질적인 애플리케이션 비즈니스 로직이 일어나는 영역
- Repository : DB에 접근 및 통신하는 영역

```
EX)
ㄴsrc/main/java/com/example/demo
	ㄴ DemoApplication.java
    ㄴ controller
    ㄴ service
    ㄴ repository
    ㄴ domain
    ㄴ config
```

계층형 구조는 각 애플리케이션 계층을 대표하는 directory를 기준으로 코드가 구성된다

#### 장점
전체 구조를 빠르게 파악할 수 있음

#### 단점
하나의 디렉터리에 많은 class 파일이 모이게 된다    
모듈 단위로 분리 시에 어려움이 있다

---
### 도메인형
스프링 웹 계픙에 주목하기 보다는 도메인에 주목하는 방식
```
EX)
ㄴsrc/main/java/com/example/demo
	ㄴ DemoApplication.java
    ㄴ domain
    	ㄴ user
          ㄴ controller
          ㄴ service
          ㄴ repository
          ㄴ domain
        ㄴ post
          ㄴ controller
          ㄴ service
          ㄴ repository
          ㄴ domain
    ㄴ global
    	ㄴ auth
        ㄴ common
        ㄴ config
```

#### domain
- domain을 담당하는 directory

#### global
- 프로젝트 전방위적으로 사용되는 객체들로 구성
    - config : 스프링 각종 설정
    - common : 공통으로 사용되는 Value 객체들
    - auth : 인증/인가에 사용되는 설정