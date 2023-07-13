# 관계형 데이터 베이스
---
## 함수
---
### 흐름제어
```
MySQL은 프로그램의 순차적인 흐름을 제어해야 할 때 사용할 수 있는 다양한 연산자와 함수를 제공한다

1. CASE
2. IF()
3. IFNULL()
4. NULLIF()
```

**1. CASE**
```
CASE 연산자는 값을 서로 비교하거나, 표현식의 논리값에 따라 다른 값을 반환한다
```
CASE 연산자의 문법
``` SQL
1. CASE value
   WHEN [compare_value] THEN result
   [WHEN [compare_value] THEN result]...
   [ELSE result]
END
2. CASE
   WHEN[condition] THEN result
   [WHEN[condition] THEN result]...
   [ELSE result]
END
```
첫 번째 CASE 문법에서는 value와 compare_value 값이 같으면 , THEN절의 result 값을 반환한다
만약 서로 값이 같지 않으면 ELSE 절의 result 값을 반환한다
이때 ELSE절이 없으면, NULL을 반환한다

두번째 CASE 문법에서는 condition의 논리값이 참이면, THEN 절의 result 값을 반환한다
만약 논리값이 거짓이라면 , ELSE 절의 result 값을 반환한다
이때 ELSE절이 없으면, NULL을 반환한다

**2. IF()**   
```
IF() 함수는 첫 번째 인수로 전달받은 표현식의 논리값에 따라 다른값을 반환한다
```

IF() 함수의 원형
``` SQL
IF(expr1, expr2, expr3)
```
만약 expr1이 참이면 expr2를 반환하고, 거짓이면 expr3를 반환한다

**3. IFNULL()**   
```
IFNULL() 함수는 첫 번째 인수로 전달받은 값이 NULL인지 아닌지를 검사하여 다른 값을 반환한다
```

IFNULL() 함수의 원형
``` SQL
IFNULL(expr1, expr2)
```

만약 expr1의 값이 NULL이 아니면 expr1 그 자체를 반환하고, NULL이면 expr2를 반환한다

**4. NULLIF()**   
```
NULLIR() 함수는 인수로 전달받은 두 값이 서로 같은지를 검사하여 다른 값을 반환한다
```

NULLIF() 함수의 원형
``` SQL
NULLIF(expr1, expr2)
```

만약 expr1과 expr2의 값이 서로 같으면 NULL을 반환하고, 같지 않으면 expr1을 반환한다

---
### 패턴 매칭(pattern matching)
```
MySQL은 데이터의 특정 패턴을 검색하기 위한 다음과 같은 패턴 매칭 연산자를 제공한다

1. LIKE
2. REGEXP

또한, 임의의 문자나 문자열을 대체하기 위해서 와일드카드(wildcard)문자를 사용할 수도 있다
```

**1. LIKE**   
```
LIKE 연산자는 특정 패턴을 포함하는 데이터만을 검색하기 위해 사용한다
```

``` SQL
/*Reservation 테이블에서 '장'으로 시작하는 
이름(Name)으로 예약한 레코드를 선택하는 예제*/

SELECT * FROM Reservation
WHERE Name LIKe '조%';
```
- 실행 결과   

|ID|Name|ReserveDate|RoomNum|   
|:---:|:---:|:-----:|:-------:|   
|3|조원상|2016-01-16|1208|

> '%'는 0개 이상의 문자라는 의미의 와일드카드(wildcard) 문자이다

만약 특정 패턴을 포함하지 않는 데이터를 검색하고 싶을 때는 `NOT LIKE`연산자를 사용하면 된다

```SQL
/* Reservation 테이블에서 '장'으로 시작하지 않는 
이름(Name)으로 예약한 레코드를 선택하는 예제 */

SELECT * FROM Reservation
WHERE Name NOT LIKE '조%';
```
- 실행 결과

|ID|Name|ReserveDate|RoomNum|
|:----:|:----:|:----:|:----:|
|1|신예찬|2016-01-05|2014|
|2|최상엽|2016-02-12|915|
|4|신광일|2016-03-17|504|

**와일드카드(wildcard)**   
```
문자열 내에서 임의의 문자나 문자열을 대체하기 위해 사용되는 기호
```

MySQL에서 사용할 수 있는 와일드카드 문자
|와일드카드|설명|
|:----:|------|
|%|0개 이상의 문자를 대체함|
|_|1개의 문자를 대체함|

```SQL
/*다음 예제는 RoomNum 필드의 값이 20으로 시작하고, 
바로 뒤에 두 자리 숫자가 더 나오는 레코드를 선택하는 예제*/

SEKECT * FROM Reservation
WHERE RoomNum LIKE '20__';
```

- 실행 결과

|ID|Name|ReserveDate|RoomNum|
|:---:|:----:|:-----:|:-----:|
|1|신예찬|2016-01-05|2014|

> 위의 예제에서 RoomNum 필드의 값이 200이나 20,000인 레코드는 선택되지 않을 것이다

**2. REGEXP**   
```
LIKE 연산자보다 더욱 복잡한 패턴을 검색하고 싶을 때는 REGEXP 연산자를 사용할 수 있다
REGEXP 연산자는 정규 표현식을 토대로 하는 패턴 매칭 연산을 제공한다
```

REGEXP 연산자와 함께 사용할 수 있는 패턴
|패턴|설명|
|:----:|-----|
|.|줄 바꿈 문자(\n)를 제외한 임의의 한 문자를 의미함|
|*|해당 문자 패턴이 0번 이상 반복됨|
|+|해당 문자 패턴이 1번 이상 반복됨|
|^|문자열의 처음을 의미함|
|$|문자열의 끝을 의미함|
|\||선택을 의미함(OR)|
|[...]|괄호([]) 안에 있는 어떠한 문자를 의미함|
|[^...]|괄호([]) 안에 있지 않은 어떠한 문자를 의미함|
|{n}|반복되는 횟수를 지정함|
|{m,n}|반복되는 횟수의 최솟값과 최댓값을 지정함|

``` SQL
/*Name 필드의 값이 '신'으로 시작하거나, '상'으로 끝나는 레코드를 선택하는 예제*/

SELECT * FROM Reservation
WHERE Name REGEXP '^신|상$';
```
- 실행 결과

|ID|Name|ReserveDate|RoomNum|
|:---:|:----:|:-----:|:----:|
|1|신예찬|2016-01-05|2014|
|3|조원상|2016-01-16|1208|
|4|신광일|2016-03-17|504|

만약 해당 패턴과 일치하지 않는 데이터를 찾고 싶을 때는 `NOT REGEXP`연산자를 사용하면 된다
```SQL
/*Name 필드의 값이 '신'으로 시작하지 않고, '상'으로 끝나지도 않는 레코드를 선택하는 예제*/

SELECT * FROM Rexervation
WHERE Name NOT REGEXP '^신|상$';
```
- 실행 결과

|ID|Name|ReserveDate|RoomNum|
|:----:|:----:|:----:|:----:|
|2|최상엽|2016-02-12|918|