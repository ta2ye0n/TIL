# DATEBASE
---
## NoSQL
```
비관계형 데이터베이스를 지칭한다
즉, 관계형 데이터 모델을 지양하며 대량의 분산된 데이터를 저장하고 조회하는데 특화되었으며 스키마 없이 사용 가능하거나 느슨한 스키마를 제공하는 저장소를 말한다
```
NoSQL은 기존 RDBMS 형태의 관계형 데이터베이스가 아닌 다른 형태의 데이터 저장 기술을 의미하며, 관계형 데이터베이스의 한계를 극복하기 위한 데이터 저장소의 새로운 형태이다
> 관계형 데이터베이스 관리 시스템(RDBMS)은 관계형 데이터베이스를 만들고 업데이트하고 관리하는데 사용하는 프로그램

---
### NoSQL의 특징
1. RDBMS와 달리 데이터 간의 관계를 정의하지 않는다
    - RDBMS는 데이터 관계를 외래키등으로 정의하고 JOIN 연산을 수행할 수 있지만, NoSQL은 JOIN연산이 불가능하다
2. RDBMS에 비해 대용량의 데이터를 저장할 수 있다
    - 페타베이트 급의 대용량 데이터를 저장할 수 있다
3. 분산형 구조이다
    - 여러 곳의 서버에 데이터를 분산 저장해 특정 서버에 장애가 발생했을 때도 데이터 유실 혹은 서비스 중지가 발생하지 않도록 한다
4. 고정되지 않은 테이블 스키마를 갖는다
    - RDBMS와 달리 테이블의 스키마가 유동적이다 데이터를 저장하는 칼럼이 각기 다른 이름과 다른 데이터 타입을 갖는 것이 허용된다

---
### NoSQL의 장점
1. RDBMS에 비해 저렴한 비용으로 분산처리와 병렬 처리 가능
2. 비정형 데이터 구조 설계로 설계 비용 감소
3. Big Data 처리에 효과적
4. 가변적인 구조로 데이터 저장이 가능
. 데이터 모델의 유연한 변화가 가능

---
### NoSQL의 단점
1. 데이터 업데이트 중 장애가 발생하면 데이터 손실 발생 가능
2. 많은 인덱스를 사용하려면 충분한 메모리가 필요. 인덱스 구조가 메모리에 저장
3. 데이터 일관성이 항상 보장되지 않음

---
### NoSQL의 종류
1. Key-Value Database
```
기본적인 패턴으로 KEY-VALUE 하나의 묶음(Unique)으로 저장되는 구조로 단순한 구조이기에 속도가 빠르면 분산 저장 시 용이하다
Key안에(COLUMN, VALUE) 형태로 된 여러 개의 필드, 즉 COLUMN FAMILIES 갖는다
주로 SERVER CONFIG, SESSION CLUSTERING 등에 사용되고 엑세스 속도는 빠르지만 SCAN에는 용이하지 않다
```
> ex) Redis, Oracle NoSQL Database, VoldeMorte

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcLHLU3%2Fbtrl1KWUzKh%2FqmxrYHWowRdRySXwfff02K%2Fimg.png)

2. Wide-Column Database
```
행마다 키와 해당 값을 저장할 때마다 각각 다른값의 다른 수의 스키마를 가질 수 있다
그림을 참고하면 사용자의 이름(key)에 해당하는 값에스키마들이 각각 다름을 볼 수 있다
이러한 구조는 갖는 WIDE COLUMN DATABASE는 대량의 데이터의 압축, 분산처리, 집계쿼리(SUM, COUNT, AVG 등)및 쿼리 동작 속도 그리고 확장성이 뛰어난 것이 그 대표적 특징이라 할 수 있다
```
> ex) Hbase, GoogleBigTable, Vertica

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbfn57O%2FbtrlZcNnz2Q%2FpDkBekmixEqT4fuZVMSlF0%2Fimg.png)

3. Documnet Database
```
테이블의 스키마가 유동적, 즉 레코드마다 각각 다른 스키마를 가질 수 있다
보통 XML, JSON과 같은 DOCUMENT를 이용해 레코드를 저장한다
트리형 구조로 레코드를 저장하거나 검색하는데 효과적이다
```
> ex) MongoDB, CouchDB, Azure Cosmos DB

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQMYuk%2Fbtrl4RHV2mS%2FZ7qx8jgmf1ipyyzJGKLFJk%2Fimg.png)

4. Graph Database
```
데이터를 노드로(그림에서 파란, 녹색 원) 표현하며 노드 사이의 관계를 엣지(그림에서 화살표)로 표현
일반적으로 RDBMS보다 성능이 좋고 유연하며 유지보수에 용이한것이 특징
Social networks, Network diagrams 등에 사용할 수 있다
```
> ex) Neo4j, BlazeGraph, OrientDB

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdGWxPj%2Fbtrl3Mf5YU7%2FEQpP5elwmBk7Ho4ylPFiG1%2Fimg.png)