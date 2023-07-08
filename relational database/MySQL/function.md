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