# 관계형 데이터 베이스
---
## 다중 테이블 연산
---
### JOIN
```
JOIN은 데이터베이스 내의 여러 테이블에서 가져온 레코드를 조합하여 하나의 테이블이나 결과 집합으로 표현해 준다
이러한 JOIN은 보통 SELECT문과 함께 자주 사용된다

표준 SQL에서는 레코드를 조합하는 방식에 따라 JOIN을 다음과 같이 구분한다

1. INNER JOIN
2. LEFT JOIN
3. RIGHT JOIN
```
- INNER JOIN
```
INNER JOIN은 ON 절과 함께 사용되며, ON 절의 조건을 만족하는 데이터만을 가져온다
```
```SQL
1. 첫번째테이블이름
   INNER JOIN 두번째테이블이름
   ON 조건

2. 첫번째테이블이름
   JOIN 두번째테이블이름
   ON 조건
```
> ON 절에서는 WHERE절에서 사용할 수 있는 모든 조건을 사용할 수 있다   
표준 SQL과는 달리 MySQL에서는 JOIN,INNER JOIN, CROSS JOIN이 모두 같은 의미로 사용된다

INNER JOIN의 결과를 벤 다이어그램으로 나타낸 그림   
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrRzvk%2Fbtq7AdGF7TQ%2FPxMMOhHSDSy7jaezodYm20%2Fimg.png)
> INNER JOIN의 경웨는 앞서 살펴본 표준 SQL방식과는 별도로 MySQL에서만 사용할 수 있는 방식이 따로 존재한다   
> 테이블의 이름이 길거나 복잡한 경우에는 별칭(alias)을 사용하여 SQL 구문을 간략화 할 수 있다

- LEFT JOIN
```
LEFT JOIN은 첫 번째 테이블을 기준으로, 두 번째 테이블을 조합하는 JOIN이다

이때 ON 절의 조건을 만족하지 않는 경우에는 첫 번째 테이블의 필드 값은 그대로 가져온다
하지만 해당 레코드의 두 번째 테이블의 필드 값은 모두 NULL로 표시된다
```
```SQL
문법
첫번째테이블이름
LEFT JOIN 두번째테이블이름
ON 조건
```
> ON 절에서는 WHERE 절에서 사용할 수 있는 모든 조건을 사용할 수 있다

LEFT JOIN의 결과를 벤 다이어그램으로 나타낸 그림
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FC7PGm%2Fbtq7CBUnCvz%2FvIy6ikbl7rRayInO78KGDK%2Fimg.png)

- RIGHT JOIN
```
RIGHT JOIN은 LEFT 조인과는 반대로 두 번째 테이블을 기준으로, 첫 번째 테이블을 조합하는 JOIN이다

이때 ON 절의 조건을 만족하지 않는 경우에는 두 번째 테이블의 필드 값은 그대로 가져온다
하지만 해당 레코드의 첫 번째 테이블의 필드 값은 모두 NULL로 표시된다
```
```SQL
문법
첫번째테이블이름
RIGTH JOIN 두번째테이블이름
ON 조건
```
> ON 절에서는 WHERE 절에서 사용할 수 있는 모든 조건을 사용할 수 있다

RIGHT JOIN의 결과를 벤 다이어그램으로 나타낸 그림
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FyP9Wd%2Fbtq7AbPuiah%2FQQg6kdkVqfYpfWVS1Vi7lK%2Fimg.png)

---
### UNION
```
UNION은 여려 개의 SELECT 문의 결과를 하나의 테이블이나 결과 집합으로 표현할 때 사용한다
이때 각각의 SELECT 문으로 선택된 필드의 개수와 타입은 모두 같아야 하며, 필드의 순서 또한 같아야 한다
```
SELECT 문에 UNION을 적용하는 문법
```SQL
SELECT 필드이름
FROM 테이블이름
UNION
SELECT 필드이름
FROM 테이블이름
```

- UNION ALL
```
UNION은 DISTINCT 키워드를 따로 명시하지 않아도 기본적으로 중복되는 레코드를 제거한다
따라서 이렇게 중복되는 레코드까지 모두 출력하고 싶다면, ALL 키워드를 사용해야한다
```
```SQL
문법
SELECT 필드이름
FROM 테이블이름
UNION ALL
SELECT 필드이름
FROM 테이블이름
```
---
### 서브쿼리 (subquery)
```
서브쿼리(subquery)란 다른 쿼리 내부에 포함되어 있는 SELETE 문을 의미하낟
서브쿼리를 포함하고 있는 쿼리를 외부쿼리(outer query)라고 부르며, 서브쿼리는 내부쿼리(inner query)라고도 부른다
서브쿼리는 반다시 괄호(())로 감싸져 있어야만 한다

MySQL에서 서브쿼리를 포함할 수 있는 외부쿼리는 SELECT, INSERT, UPDATE, DELETE, SET, DO문이 있다
이러한 서브쿼리는 또 다시 다른 서브쿼리 안에 포함될 수 있다
```

주소가 서울인 고객이 예약한 예약 정보만을 선택하는 예제
```SQL
① SELECT ID, ReserveDate, RoomNum
  FROM Reservation
② WHERE Name IN (SELECT Name 
               FROM Customer 
               WHERE Address = '서울')
```
위의 예제에서 ①번 라인의 SELECT 문은 외부쿼리이며, ②번 라인의 SELECT 문은 서브쿼리이다   
우선 ②번 라인의 서브쿼리가 먼저 실행되어 Customer 테이블의 Address 필드의 값이 '서울'인 레코드의 Name 필드를 모두 선택한다   
그리고서 ①번 라인의 외부쿼리가 실행되어 Reservation 테이블에서 서브쿼리에 의해 선택된 결과 집합에 포함된 Name 필드와 일치하는 레코드만을 다시 선택한다