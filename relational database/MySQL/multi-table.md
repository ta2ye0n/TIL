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