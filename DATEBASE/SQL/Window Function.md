# SQL
---
## 윈도우 함수 (WINDOW FUNCTION)
```
행과 행 간의 관계를 쉽게 정의하기 위해 만든 함수
```
윈도우 함수는 기존에 사용하더 집계 함수도 있고, 새로이 윈도우 함수 전용으로 만들어진 기능도 있다
다른 함수와 달리 `중천해서 사용은 못하지만`, 서브쿼리에는 사용할 수 있다

---
### 종류
> 벤더별로 지원하는 함수 차이가 있다

1. 그룹 내 `순위(RANK) 관련`함수
2. 그룹 내 `집계(AGGREGATE) 관련` 함수
3. 그룹 내 `행 순서 관련` 함수
4. 그룹 내 `비율 관련` 함수
5. 선형 분석을 포함한 `통계 분석 함수`

---
### 문법
윈도우 함수에는 `OVER`문구가 키워드로 필수 포함된다
```sql
SELECT WINDOW_FUNCTION (ARGUMENTS) OVER
    ([PARITION BY 컬럼] [ORDER BY 컬럼] [WINDOWING 절] )
FROM 테이블 명;
```
- WINDOW_FUNCTION : 윈도우 함수

- ARCUMENTS(인수) : 함수에 따라 0 ~ N개 인수가 지정될 수 있다
- PARTITION BY 절: 전체 집합을 기준에 의해 소그룹으로 나눌 수 있다
- ORDER BY 절 : 어떤 항목에 대해 순위를 지정할 지 order by 절을 기술한다
- WINDOWING 절 : WINDOWING 절은 함수의 대상이 되는 행 기준의 범위를 강력하게 지정할 수 있다
    > sql server 에서는 지원하지 않는다

---
### 그룹 내 순위관련 함수
1. `RANK`
    ```
    순위를 구하는 함수
    ``` 
    - 특정 범위(PARTITION) 내에서 순위를 구할 수도 있고, 전체 데이터에 대한 순위를 구할 수도 있다
    - 동일한 값에 대해서는 `동일한 순위를 부여`하게 된다

2. `DENSE_RANK`
    ```
    누적 순위
    ```
    - `동일한 순위를 하나의 건수로 취급`한다

3. `ROW_NUMBER`
    ```
    연속된 행 번호
    ```
    - 동일한 값이라도 `고유한 순위을 부여`한다

![alt text](image-1.png)

---
### 그룹 내 집계관련 함수
1. `SUM`
    ```
    파티션별 윈도우의 합을 구할 수 있다
    ```

2. `MAX`
    ```
    파티션별 윈도우의 최대값을 구할 수 있다
    ```
    - `INLINE VIEW`를 이용해서 파티션별 최대값을 가진 행만 추출 할 수도 있다

3. `MIN`
    ```
    파티션별 윈도우의 최소값을 구할 수 있다
    ```

4. `AVG`
    ```
    파티션별 통계값을 구할 수 있다
    ```

---
### 그룹 내 행 순서관련 함수
1. `FIRST_VALUE`
    ```
    파티션별 윈도우에서 가장 먼저 나온 값을 구할 수 있다
    ```
    - sql server 에서는 지원하지 않는다
    - `MIN` 함수를 이용해도 같은 결과를 얻을 수 있다
    - FIRST_VALUE는 `공동 등수를 인정하지 않고` 처음 나온 행을 처리하기 때문이다

2. `LAST_VALUE`
    ```
    파티션별 윈도우에서 가장 먼저 나중에 나온 값을 구할 수 있다
    ```
    - sql server 에서는 지원하지 않는다
    - `MAX` 함수를 이용해도 같은 결과를 얻을 수 있다

3. `LAG`
    ```
    파티션별 윈도우에서 이전 몇 번째 행의 값을 가져올 수 있다
    ```
    - sql server에서는 지원하지 않는다

    - `3개의 인수`까지 사용 할 수 있다
    - 두번째 인수는 `몇번째 앞의 행`을 가져올지 결정한다 (디폴트는 1)
    - 세번째 인수는 첫번째 행의 경우 가져올 데이터가 없어 NULL 값이 들어오는데, 이 경우 `다른 값으로 바꾸어 줄 수 있다`

4. `LEAD`
    ```
    파티션별 윈도우에서 이후 몇 번째 행의 값을 가져올 수 있다
    ```
    - sql server 에서는 지원하지 않는다
    - `3개의 인수`까지 사용할 수 있다

---
### 그룹 내 비율관련 함수
1. `CUME_DIST`
    ```
    파티션별 윈도우의 전체건수에서 현재 행보다 작거나 같은 건수에 대한 누적백분율을 구한다
    ```
    - sql server에서는 지원하지 않는다

2. `PERCENT_RANK`
    ```
    파티션별 함수를 이용해서 파티션별 윈도우에서 제일 먼저 나오는 것을 0으로,
    제일 늦게 나오는것을 1로 하여, 행의 순서별 백분율을 구한다
    ```
    - sql server에서는 지원하지 않는다

3. `NTILE`
    ```
    파티션별 전체 건수를 ARGUMENT값으로 N등분한 결과를 구할 수 있다
    ```

4. `PATIO_TO_REPORT`
    ```
    파티션 내 전체 SUM(컬럼) 값에 대한 행별 컬럼 값의 백분율을 소수점으로 구할 수 있다
    ```
    - 결과값은 `>0 & <= 1`의 범위를 가진다
    - sql server에서는 지원하지 않는다

---