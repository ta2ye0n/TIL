# 관계형 데이터 베이스
---
## 타입
---
### 숫자 타입
 타입(data type)
 ```
 MySQL에서 테이블의 정의할때는 필드별로 저장할 수 있는 타입까지 명시해야 한다

 MySQL에서 제공하는 기본 타입
 1. 숫자 타입
 2. 문자열 타입
 3. 날짜와 시간 타입
 ```
 - 숫자타입(numeric types)
 ```
 MySQL은 SQL 표준에서 지원하는 모든 숫자 타입을 제공한다

 MySQL에서 제공하는 숫자 타입
 1. 정수 타입(integer types)
 2. 고정 소수점 타입(fixed-point types)
 3. 부동 소수점 타입(floating-point types)
 4. 비트값 타입(bit-value type)
 ```
 - 정수 타입
 ```
MySQL은 SQL표준 정수 타입인 INTEGER(또는 INT)와 SAMLLINT를 제공한다
또한, 표준 정수 타입의 범위를 더욱 확장한 TINYINT, MEDIUMINT, BIGINT까지 제공하고 있다

각 정수 타입에 따라 요구되는 저장 공간과 표현할 수 있는 최댓값과 최솟값까지 달라진다
또한, 정수 타입은 으수까지 표현할 수 있는 SIGNED 타입과 양수만을 표현할 수 있는 UNSIGNED 타입으로 구분된다
```
MySQL 정수 타입에 따른 표현할 수 있는 최댓값, 최솟값과 요구되는 저장 공간의 크기
![](https://velog.velcdn.com/images%2Fdnjscksdn98%2Fpost%2F516cf6b8-e695-40c3-aa1f-9ca470322a9f%2Fimage.png)

- 고정 소수점 타입(fixed-point types)
```
MySQL에서 고정 소수점 타입인 DECIMAL은 실수의 값을 정확하게 표현하기 위해 사용된다
DECIMAL에서 사용하는 고정 소수점 방식은 실수를 표현할 때 소수부의 자릿수를 고정하여 표현한다

즉, 소수부의 자릿수를 미리 정해 놓고, 고정된 자릿수로만 소수 부분을 표현하는 방식이다
```