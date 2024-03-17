# JPA
---
## QueryDSL
```
하이버네이트 쿼리 언어(HQL: Hibernate Query Language)의 쿼리를 
타입에 안전하게 생성 및 관리해주는 프레임워크
```
QueryDSL은 정적 타입을 이요하여 SQL과 같은 쿼리를 생성할 수 있게 해준다

자바 백엔드 기술은 Spring Boot와 Spring Data JPA를 함께 사용한다
하지만 복잡한 쿼리, 동적 쿼리를 구현하는 데 있어 한계가 있다
이러한 문제점을 해결할 수 있는 것이 QueryDSL이다

QueryDSL를 사용하면 `컴파일 시에 오류를 발생`하여 `잘못된 쿼리가 실행되는 것을 방지` 할 수 있다

---
### QueryDSL 동작원리
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnI4T8%2FbtspeIPCLp0%2FpmndIdQ8Q3VbuNHFFUgUt1%2Fimg.png) 

개발자가 JPQL을 문자열로 직접 작성하면, 타입 안정성을 체크할 수 없고 직관적인 동적쿼리도 작성할 수 없다      
QueryDSL은 JPQL을 대신 생성하여 이런 문제를 해결한다

QueryDSL의 목적은 JPQL 생성이다

QueryDSL은 쿼리 생성에 특화된 프레임워크로, JPA 프레임워크와 분리되어 있다 
그러므로 다른 프레임워크의 모듈을 그대로 사용하면 JPA 프레임워크에 종속되어버린다
막기위해 QueryDSL은 Entity 정보를 담은 `Q타입 클래스`를 사용한다

---
### 장단점
**장점**   
- 문자가 아닌 코드로 쿼리를 작성할 수 있어 `컴파일 시점에 문법오류`를 확인할 수 있다

- 인텔리제이와 같은 `IDE의 자동 완성 기능`의 도움을 받을 수 있다
- 복잡한 쿼리나 동적쿼리 작성이 편리하다
- 쿼리 작성 시 제약 조건 등을 `메서드 추출을 통해 재사용`할 수 있다
- `JPQL 문법`과 유사한 형태로 작성할 수 있어 쉽게 적응할 수 있다

**단점**   
- `초기세팅`이 어렵다

- `JPA 1차 캐시` 사용이 불가능하다
---