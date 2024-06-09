# SQL
---
## 그룹 함수(GROUP FUNCTION)
```
테이블의 전체 행을 하나 이상의 컬럼을 기준으로 컬럼값에 따라 그룹화하여 그룹별로 결과를 출력하는 함수이고 복수행 함수
```
소계, 중계, 합계, 총 합계 등을 구할 수 있다

---
### 규칙
1. `NULL`값이 있는 컬럼은 조회에 포함시키지 않는다

2. `LOW가 없는 테이블`에 그룹함수 COUNT()를 사용시 `0이 출력`되며 SUM()를 사용시 `NULL 값이 출력`된다

3. COUNT, MAX 와 MIN은 문자, 숫자, 날짜 데이터 `모두에게서 사용할 수 있다`
그러나 AVG SUM, VARIANCE, STDDEV는 NUMBER만 사용 가능하다

4. EXPR이 있는 인수들의 자료 형태는 CHAR, VARCHAR2, NUMBER, DATE 형이 될 수도 있다

---
### COUNT
```
테이블에서 조건을 만족하는 행의 개수를 반환하는 함수
```
```sql
-- NULL 값을 포함한 행의 수 출력
COUNT(*)

-- NULL 값을 제외한 행의 수 출력
COUNT(표현식)
```

---
### MIN, MAX
```
지정한 컬럼 값들 중에서 최대 값, 최소 값을 구하는 함수
```
```sql
-- MAX()
select MAX(컬럼명) from  테이블명;

-- MIN()
select MIN(컬럼명) from 테이블명;
```
`데이터가 없`는 테이블에 사용헸을 때에는 `NULL 값`을 출력한다   
문자, 날짜 타입도 사용 가능하며 날짜의 최대값은 현재랑 가장 가까운 날이다

---
### SUM
```
지정한 컬럼 값의 합계를 변환하는 함수
```
```sql
SELECT SUM(컬럼명) FROM 테이블명;

-- 중복제거
SELECT SUM (DISTINCT 컬럼명) FROM 테이블명;
```
해당 컬럼 값이 `NULL인 것은 제외`하고 계산한다

---
### AVG
```
지정한 컬럼 값의 합계를 변환하는 함수
```
```sql
SELECT AVG(컬럼명) FROM 테이블명;

-- 중복제거
SELECT AVG(DISTINCT 컬럼명) FROM 테이블명;
```
해당 컬럼 값이 `NULL인것은 제외`하고 계산한다

NULL 값을 0으로 하여 전체 평균을 구하고 싶다면 `NVL 함수`를 사용한다
```sql
-- ex)
AVG(NVL(score,0))
```

---