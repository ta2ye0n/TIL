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
또한, 정수 타입은 음수까지 표현할 수 있는 SIGNED 타입과 양수만을 표현할 수 있는 UNSIGNED 타입으로 구분된다
```
MySQL 정수 타입에 따른 표현할 수 있는 최댓값, 최솟값과 요구되는 저장 공간의 크기
![](https://velog.velcdn.com/images%2Fdnjscksdn98%2Fpost%2F516cf6b8-e695-40c3-aa1f-9ca470322a9f%2Fimage.png)

- 고정 소수점 타입(fixed-point types)
```
MySQL에서 고정 소수점 타입인 DECIMAL은 실수의 값을 정확하게 표현하기 위해 사용된다
DECIMAL에서 사용하는 고정 소수점 방식은 실수를 표현할 때 소수부의 자릿수를 고정하여 표현한다

즉, 소수부의 자릿수를 미리 정해 놓고, 고정된 자릿수로만 소수 부분을 표현하는 방식이다
```
``` SQL
MySQL에서 DECIMAL 타입은 NUMERIC을 구현하여 만들어 졌다
따라서 대부분의 경우 DECIMAL 대신 NUMERIC을 사용해도 똑같이 동작한다

문법
DECIMAL(M,D)

M은 소수 부분을 포함한 실수의 총 자릿수를 나타내며, 최댓값은 65이다
D는 소수 부분의 자릿수를 나타내며, D가 0이면 소수 부분을 가지지 않는다
```

- 부동 소수점 타입(floating-point types)
``` 
부동 소수점 타입인 FLOAT과 DOUBLE은 실수의 값을 대략적으로 표현하기 위해 사용된다
MySQL은 IEEE 754 표준에 따라 FLOAT는 4바이트를 사용하며, DOUBLE은 8바이트를 사용한다
```
``` SQL
SQL 표준에서 FLOAT는 정밀도에 필요한 최소한의 비트 수를 명시할 수 있다

문법
FLOAT(P)

P가 0부터 24까지의 값을 가질 때는 FLOAT 값으로 취급되며, 25부터 
53까지의 값을 가질 때는 DOUBLE 값으로 취급된다

또한, MySQL은 FLOAT과 DOUBLE을 고정 소수점 타입과 같이 사용할 수 있는 비표준 문법도 지원한다

문법
FLOAT(M,D)
DOUBLE(M,D)

M은 소수 부분을 포함한 실수의 총 자릿수를 나타내며, D는 소수 부분의 자릿수를 나타낸다
```

- 비트값 타입(bit-value type)
``` SQL
MySQL에서 비트값 타입인 BIT는 비트의 값을 저장한다
즉, 0과 1로 구성되는 바이너리(binary)값을 저장할 수 있다

문법
BIT(M)

M의 범위는 1부터 64까지 설정할 수 있으며, 명시한 M 비트의 값을 저장할 수 있다
만약 명시한 M 비트보다 짧은 길이의 비트 값을 입력하면, 
입력한 값 앞에 0을 추가하여 자동으로 길이를 맞춘다
```
> MySQL에서는 바이너리 값을 출력하기 위해 BIN()와 같은 변환 함수를 제공하고 있다
---
### 문자열 타입
``` SQL
MySQL은 다양한 형태의 문자열 타입을 제공한다
1. CHAR 와 VARCHAR
2. BINARY 와 VARBINARY
3. BLOB 과 TEXT
4. ENUM
5. SET
```

- CHAR와 VARCHAR
``` SQL
CHAR와 VARCHAR는 둘다 문자열 데이터를 저장할 수 있는 타입이다
하지만 저장 방식과 추출 방식 그리고 최대 길이를 다루는 방식에서 차이점을 가진다

CHAR는 문자열을 길이가 한 번 설정되면 그대로 고정되는 고정 길이의 문자열로 다룬다
하지만 VARCHAR는 문자열을 길이가 고정되지 않는 가변 길이의 문자열로 다룬다

문법
CHAR(M)
VARCHAR(M)

M은 저장할 수 있는 문자열의 최대 길이를 나타낸다
이때 CHAR는 0부터 255까지 설정할 수 있으며, VARCHAR는 0부터 65535까지 설정할 수 있다

CHAR는 설정한 크기보다 작은 길이의 문자열이 입력되면, 
나머지 공간을 공간을 공백으로 채워 길이를 M과 같게 만든다
하지만VARCHAR는 실제 입력된 문자열의 길이만큼만 저장하고 사용한다
```

- BINARY와 VARBINARY
``` SQL
BINARY와 VARBINARY는 각각 CHAR와 VARCHAR과 거의 비슷하다
다만 BINARY와 VARBINARY는 문자 집합이 아닌 바이너리(binary) 데이터를 
저장할 때 사용된다는 점만 다르다

문법
BINARY(M)
VARBINARY(M)
```

- BLOB과 TEXT
```
BLOB은 Binary Large Object를 의미하며, 다양한 크기의 바이너리 데이터를 저장할 수 있는 타입이다
저장할 수 있는 데이터의 최대 크기에 따라 TINYBLOB,BLOB,MEDIUMBLOB,LONGBLOB로 구분된다

TEXT는 VARCHAR와 비슷하지만, VARCHAR와 달리 기본값을 가질 수 없다
또한 TEXT는 BLOB와도 비슷하지만, BLOB와는 달리 문자열의 대소문자를 구분한다
저장할 수 있는 데이터의 최대 크기에 따라 TINYTEXT, TEXT, MEBIUMTEXT, LONGTEXT로 구분된다
```

- SET
``` SQL
SET은 미리 정의한 집합 안의 요소 중 여러 개를 동시에 저장할 수 있는 타입이다
SET 목록 집합은 최대 64개의 SET 데이터를 포함 할 수 있다

문법
SET('데이터값1','데이터값2',...)
```
---
### 날짜와 시간 타입
```
MySQL은 날짜와 시간에 관한 다양한 형태의 타입을 제공한다

1. DATE, DATETIME, TIMESTAMP
2. TIME
3. YEAR
```
- DATE, DATETIME,TIMESTAMP
    - DATE
    ```
    DATE는 날짜를 저장할 수 있는 타입이다
    기본 형식은 'YYYY-MM-DD'이며, 이때 저장할 수 있는 날짜의 범위는 '1000-01-01'부터 '9999-12-31'부터'9999-12-31 23:59:59'까지 이다
    ```
    - DATETIME
    ```
    DATETIME 날짜와 시간을 나타내는 타임스탬프를 저장할 수 있는 타입이다
    기본 형식은 'YYYY-MM-DD HH:MM:SS'이며, 이때 저장할 수 있는 범위는 '1000-01-01 00:00:00' 부터 '9999-12-31 23:59:59'까지 이다
    ```
    - TIMESTAMP
    ```
    TIMESTAMP는 날짜와 시간을 나타내는 타임스탬프를 저장할 수 있는 타입이다
    TIMESTAMP 타입의 필드는 사용자가 별다른 입력을 주지 않으면, 데이터가 마지막으로 입력되거나 변경된 시간이 저장된다
    따라서 데이터의 최종 변경 시각을 저장하고 확인하는데 유용하게 사용된다
    이때 저장할 수 있는 범위는 '1970-01-01 00:00:01' UTC부터 '2038-01-19 03:14:07' UTC까지입니다.
    ```
> 입력받은 데이터가 유효한 날짜와 시간이 아니면, 세 타입 모두 0을 저장한다

- TIME
```
TIME은 시간을 저장할 수 있는 타입이다
기본 형식은 'HH:MM:SS'나 'HHH:MM:SS'이며, 이때 저장할 수 있는 시간의 범위는 '-838:59:59'부터 '838:59:59'까지 이다

범위를 초과한 시간은 '-838:59:59'이나 '838:59:59'로 자동 변환되어 저장된다
또한, 유효하지 않는 시간은 '00:00:00'로 저장된다
```

- YEAR
```
YEAR는 연도를 저장할 수 있는 타입이다
YEAR(2)는 2자리의 연도를 저장할 수 있으며, YEAR(4)는 4자리의 연도를 저장할 수 있다

YEAR는 연도를 나타내는 숫자와 문자열을 모두 저장할 수 있으나, 저장되는 결과가 다음과 같이 조금씩 다르다

1. 4자리 숫자로 저장하면, 저장할 수 있는 범위는 1901년부터 2155년까지가 됩니다.
2. 4자리 문자열로 저장하면, 저장할 수 있는 범위는 1901년부터 2155년까지가 됩니다.
3. 1자리 또는 2자리 숫자로 저장하면, 1부터 69까지는 2001년부터 2069년까지가 되고, 70부터 99까지는 1970년부터 1999년까지가 됩니다.
4. 1자리 또는 2자리 문자열로 저장하면, '0'부터 '69'까지는 2000년부터 2069년까지가 되고, '70'부터 '99'까지는 1970년부터 1999년까지가 됩니다.
5. 숫자 0을 저장하면, 2000년이 아닌 0000년으로 저장되므로, 2000년은 반드시 문자열 '0' 또는 '00'으로 입력해야 합니다.

이때 유효하지 않은 연도는 '0000'으로 저장된다
```
> YEAR(2)는 MySQL 5.7.5 버전부터는 지원하지 않으므로, 연도를 저장할 때는 YEAR(4)를 사용하는 것이 좋다