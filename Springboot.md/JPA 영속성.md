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