# Spring boot
---
## JPA Persistence
---
### 영속성 컨텍스트(persistence context)
```
엔티티를 영구 저장하는 환경
-> 어플리케이션과 데이터베이스 사이에서 객체를 보관하는 가상의 저장소 같은 역할
```
`EntityManger`를 이용해 Entity을 저장하거나 조회할때 EntityManager는 영속성 컨텍스트에 Entity 를 보관하고 관리한다
`EntityManger객체.persist(Entity객체)`를 실행하면 Entity를 영속성 컨텍스트가 관리하게 된다

영속성 컨텍스트는 `눈에 보이지 않는 논리적인 개념`이다

---
### 영속성 컨텍스트 생명주기
영속성 컨텍스트의 생명주기는 `4가지` 상태가 있다
```
- 비영속 (new) : 영속성 컨텍스트와는 무관한 상태
- 영속 (managed) : 영속성 컨텍스트에 저장된 상태
- 준영속(detached) : 영속성 컨텍스트에 저장되었다가 분리된 상태
- 삭제 (removed) : 영속성 컨텍스트에서 삭제된 상태
```
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcwQFfV%2FbtrIfRfp70x%2FWRmxZC7G8NetTSS5QIHDSK%2Fimg.png)

- `비영속(New)`   
엔티티 객체를 생성했지만 아직 영속성 컨텍스트에는 `저장되지 않은 상태`(순수 객체)
```java
Ex)
Member member = new Member();
```

- `영속(Managed)`   
Entity Manager를 통해서 Entity를 `영속성 컨텍스트에 저장한 상태`   
해당 객체는 영속성 컨텍스트에 의해 관리된다는 의미
```java
Ex)
Member member = new Member(); // 순수 객체

// 영속성 컨텍스트에 저장 -> 영속성 컨텍스트가 관리
EntityManager em;
em.persist(member);
```

- `준영속(Detached)`   
영속성 컨텍스트가 관리하던 상태에서 엔티티를 `더 이상 관리하지 않는 상태`

    `준영속 상태의 특징`    
    `1차 캐시, 쓰기 지연, 변경 감지, 지연 로딩`을 포함한 영속성 컨텍스트가 제공하는 `어떠한 기능도 동작하지 않음`   
    `식별자 값`을 가지고 있음

    ```java
    Ex)
    em.detach(member); // 엔티티를 영속성 컨텍스트에서 분리
    em.claer(); // 영속성 컨텍스트를 비움(초기화)
    em.close(); // 영속성 컨텍스트를 종료
    ```

    `엔티티를 준영속 상태로 전환하는 방법`
    - **detach(entity)**   
    특정 엔티티만 `준영속 상태로 전환`(영속성 컨텍스트로부터 분리)   
    1차 캐시, 쓰기 지연, SQL 저장소 정보 제거   
    영속성 컨텍스트 안에서의 `Insert, Update 쿼리도 제거`되어 `DB에 저장되지 않음`

    - **clear()**   
    영속성 컨텍스트를 `완전히 초기화`   
    영속성 컨텍스트의 모든 엔티티를 `준영속 상태`로 만듦   
    영속성 컨텍스트 `틀은 유지`하지만 `내용은 비워 새로 만든 것`과 같은 상태

    - **close()**   
    영속성 컨텍스트를 `종료`   
    해당 영속성 컨텍스트가 관리하던 `영속성 상태`의 엔티티들은 모두 준영속 상태로 변경

    `엔티티를 영속 상태로 전환하는 방법`   
    - **merger(entity)**   
    준영속 상태의 엔티티를 `다시 영속 상태로 변경`(병합)   
    파라미터로 전달된 엔티티의 식별자 값으로 `영속성 컨텍스트를 조회`하고 엔티티가 없다면, DB에서 조회    
    병합은 `save(저장)` 또는 `update(수정)` 기능 수행

- `삭제(Remove)`   
엔티티 `영속성 컨텍스트와 데이터 베이스`에서 삭제
```java
em.remove(member);
```
---
### EntityManagerFactory / Entity Manager
데이터 베이스를 하나만 사용하는 애플리케이션은 보통 EntityManagerFactory를 하나만 생성한다
EntityManagerFactory는 `여러 EntityManger를 생성`하는 객체이다

**차이점**   
- EntityManagerFactory   
생성하는데 비용이 크기 때문에 전체에서 `한 번`만 생성해 공유하도록 설계되어 있다
여러 스레드가 `동시에 접근`해도 안전하다 따라서 서로 다른 스레드 간에 공유가 가능하다

- EntityManager   
생성하는데 비용이 거의 들지 않는다
여러 스레드가 동시에 접근하면 `동시성 문제`가 발생하기 때문에 스레드 간에 `절대 공유하지 않는다`

> Entity Manager는 데이터베이스 연결이 꼭 필요한 시점까지(보통 트랜잭션을 시작할 때) 커넥션을 얻지 않는다
---