# JPA
---
## JPA(Java Persistence API)
```
자바 진영에서 ORM(Object-Relational Mapping) 기술 표준으로 사용되는 인터페이스의 모임

실제적으로 구현된것이 아니라 구현된 클래스와 매핑을 해주기 위해 사용되는 프레임워크
```
가장 대중적인것으로 `Hibernate`가 있다

> ### ORM (Object-Relational Mapping)
>```
>애플리케이션 Class와 REB(Relational DataBase)의 테이블을 매핑(연결)한다는 >뜻이며, 기술적으로는 애플리케이션의 객체를 RDB 테이블에 자동으로 영속화 해주는 것
>```
---
### 사용이유
1. `생산성`   
JPA를 사용하면 자바 컬렉션에 저장하듯이 JPA에게 저장할 객체를 전달하면 된다
SQL이 아닌 `객체 중심으로 개발`할 수 있다

2. `유지보수`   
필드를 하나만 추가해도 관련된 SQL과 JDBC 코드를 전부 수행해야 했지만 JPA는 이를 대신 처리해주기 때문에 개발자가 유지보수해야하는 코드가 줄어든다

3. `패러다임의 불일치 해결`   
JPA는 연관된 객체를 사용하는 시점에 SQL을 전달할 수 있고, 같은 트랜잭션 내에서 조회할 때 동일성도 보장하기 때문에 다양한 패러다임의 불일치를 해결한다

4. `성능`   
애플리케이션과 데이터베이스 사이에서 성능 최적화 기회를 제공한다

5. `데이터 접근 추상화와 벤더 독립성`   
RDB는 같은 기능이라도 벤더마다 사용법이 다르기 때문에 처음 선택한 데이터베이스에 종속되고 변경이 어렵다
JPA는 애플리케이션과 데이터베이스 사이에서 추상화된 데이터 접근을 제공하기 때문에 종속이 되지 않도록한다

---
### SQL을 직접 다룰 때의 문제점
1. `반복적인 코드의 작성`   
테이블이 100개 존재한다면 100개의 CRUD를 작성해야 한다   
`SQL 작성 -> JDBC API로 SQL 실행 -> 결과를 객체로 매핑`

2. `SQL 의존적 개발`   
만약 테이블에 변동사항이 있다면?
    - 모든 SQL의 변경이 필요
    - INSERT, UPDATE, SELECT 등 관련된 모든 쿼리와 메서드가 변경되어야함
    - 만약 제대로 동작하지 않다면 직접 DAO를 열어 SQL을 확인   
        -> 논리적인 계층 분할이 어렵게 된다

3. `패러다임의 불일치`   
자바는 객체지향 언어지만, 관계형 데이터베이스는 객체지향이 다루는 개념이 존재하지 않고 서로 지향하는 목적이 다르기때문에 이로 인해 피러다임의 불일치가 발생한다

4. `객체 그래프 탐색`   
객체는 자유롭게 객체 그래프를 탐색할 수 있어야 하지만 SQL을 이용해 조회를 했다면 실행된 처음 SQL에 따라 탐색의 범위가 저장되기 때문에 제약이 발생한다   
따라서 개발자는 어디까지 탐색이 가능한지 모르게 되고, DAO를 통해 실행된 SQL을 직접 확인해야만 탐색이 가능하다

---
### 단점
1. `복잡한 쿼리 처리`   
복잡한 쿼리를 사용할 때 JPA에서는 `Native SQL`을 통해 기존의 SQL문을 사용할 수 있지만 그러면 `특정 데이터베이스에 종속`된다는 단점이 생긴다
    > 이를 보완하기 위해서 SQL과 유사한 기술인 `JPQL`을 지원한다

2. `성능 저하 위험`   
객체 간의 ``매핑 설계를 잘못`했을 때 성능 저하가 발생할 수 있으며, 자동으로 생성되는 쿼리가 많기 때문에 `개발자가 의도하지 않은 쿼리`로 인해 성능이 저하되기도 한다

3. `학습시간`   
JPA를 제대로 사용하려면 알아야 할 것이 많아서 학습하는데 시간이 오래 걸린다