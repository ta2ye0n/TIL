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

---
### 언제 사용할 것인가?
- 스키마에 얽매이지 않고 다양한 형태(structured, semi-structured, unstructured)의 데이터를 다뤄야 할 때
```
SQL에서는 현실 세계의 데이터가 어떻든 간에 데이터베이스 제품군에 ㅁ자는 형식으로 변환하여 미리 고정된 자료구조(스키마)에 맞춰 삽입하고 조회해야 한다. NoSQL은 이런 고정된 자료구조에서 벗어나서 자료구조를 원하는 대로 정의할 수 있기 때문에 데이터를 데이터베이스 대신 애플리케이션에 좀 더 가깝게 다룰 수 있다

예를 들어 RDBMS에서는 컬럼값이 배열을 가질 수 없다. 하지만 무서형 데이터베이스에서는 JSON으로 데이터를 표현하여 배열을 포함한 복잡한 자료구조를 표현할 수 있고 이를 애플리케이션에서 JSON 파서 등으로 읽어서 좀 더 간편하게 다룰 수 이싿 비슷하게 새로 삽입된 데이터가 이전에 삽입된 데이터와 같은 컬럼(또는 키)을 가질 필요가 없기 때문에 좀 더 유연하게 데이터를 다룰 수 있다

이런 유연성은 요구사항이 자주 변하는 애자일 애플리케이션 개발 방식에도 적합하다는 의견이 있다
```
- 스케일-아웃을 통해 SQL보다 더 많은 데이터를 빠르게 처리해야 할때(빅 데이터 vs 웹 애플리케이션 수준)
```
더 많은 데이터를 빠르게 처리한다는 것은 스케일-아웃과 연관된 특징이라 할 수 있다 RDBMS에서는 OK,FK를 이용한 JOIN 연관관계로 데이터를 구성하기 때문에 참조관계 등 일관성 보장 측면에서 확장이 자유롭지 않다 그러자 NoSQL의 레코드는 그런 연관관계가 없는 독립적인 레코드기 때문에 확장(스케일-아웃)에 수월하여 유동적으로 서버를 확장하거나 축소하는 클라우드 환경에 적합하다는 것이다

별다른 연관관계가 없다는 것은 단순히 키(PK)만으로 모든 데이터를 조회할 수 있다는 것을 의미하기 때문에 당연히 RDBMS보다 데이터를 빠르게 조회할 수 있다

하지만 이건 연관관계가 필요한 경우에는 까다로워질 수 있다 예를 들어 어떤 레코드가 어떤 속성을 가졌는지는 빠르게 파악할 수 있지만 반대로 어떤 속성을 가진 레코드들을 필터링(검색)하는 경우에는 적합하지 않다는 것이다(불가능한 것은 아니다 NoSQL에서도 쿼리를 사용 가능)
```