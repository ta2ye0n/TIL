# 관계형 데이터 베이스
---
## 내장 함수
```
MySQL은 사용자의 편의를 위해 다양한 기능의 내장 함수를 미리 정의하여 제공하고 있다

MySQL에서 미리 정의하여 제공해 주는 대표적인 내장 함수의 종류
1. 문자열 함수
2. 수학 함수
3. 날짜와 시간 함수
```
---
### 문자열 함수
- 문자열 길이   
Length()함수는 전달받은 문자열의 길이를 반환한다
```SQL
예제
SELECT LENGTH('12345678');

실행 결과
8
```

- 문자열 결합   
CONCAT()함수는 전달받은 문자열을 모두 결합하여 하나의 문자열로 반환한다   
만약 전달받은 문자열 중 하나라도 NULL이 존재하면, NULL을 반환한다
```SQL
예제
SELECT CONCAT('Ora','cle Cor', 'poration'),
CONCAT('Oracle', NULL, 'Corporation');

실행 결과
Oracle Corporation
NULL
```

- 특정 문자열의 위치 검색   
LOCATE() 함수는 인수로 전달받은 문자열이 특정 문자열에서 처음으로 나타나는 위치를 찾아서, 해당 위치를 반환한다   
만약 전달받은 문자열이 특정 문자열 내에 존재하지 않으면 0을 반환한다   
이때 세 번째 인수로 특정 문자열에서 전달받은 문자열을 찾기 시작할 인덱스를 전달할 수도 있다
> 다른 대부분의 프로그래밍 언어에서는 문자열의 첫 번째 문자의 인덱스를 0부터 시작하여 그 위치를 계산한다
하지만 MySQL에서는 문자열의 첫 번째 문자의 인덱스를 언제나 1부터 시작하여 계산하므로, 주의를 기울여야 한다
```SQL
예제
SELECT LOCATE('abc', 'ababcDEFabc'),
LOCATE('abc', 'ababcDEFabc', 4);

실행 결과
3
9
```

- 문자열 추출   
LEFT() 함수는 전달받은 문자열의 왼쪽부터 명시한 개수만큼의 문자를 반환한다   
RIGHT() 함수는 전달받은 문자열의 오른쪽부터 명시한 개수만큼의 문자를 반환한다
```SQL
예제
SELECT LEFT('MySQL PHP HTML Java', 5),
RIGHT('MySQL PHP HTML Java', 4);

실행결과
MySQL
Java
```

- 문자열 대소문자 변경   
LOWER() 함수는 전달받은 문자열의 문자를 모두 소문자로 변경한다   
UPPER() 함수는 전달받은 문자열의 문자를 모두 대문자로 변경한다
```SQL
예제
SELECT LOWER('MySQL PHP HTML Java'),
UPPER('MySQL PHP HTML Java');

실행결과
mysql php html java
MYSQL PHP HTML JAVA
```

- 문자열 대체   
REPLACE() 함수는 전달받은 문자열에서 특정 문자열을 찾은 후에, 찾은 문자열을 대체 문자열로 교체한다   
```SQL
예제
SELECT REPLACE('MySQL', 'My', 'MS');

실행결과
MS SQL
```

- 문자열 다듬기   
TRIM() 함수는 전달받은 문자열의 앞이나 뒤, 또는 양쪽 모두에 있는 특정 문자를 제거한다   
만약 지정자를 명시하지 않으면, 자동으로 BOTH로 설정된다   
또한, 제거할 문자를 명시하지 않으면, 자동으로 공백을 제거하게 된다

```
TRIM() 함수에서 사용할 수 있는 지정자

1. BOTH : 전달받은 문자열의 양 끝에 존재하는 특정 문자를 제거함. (기본 설정)
2. LEADING : 전달받은 문자열 앞에 존재하는 특정 문자를 제거함.
3. TRALING : 전달받은 문자열 뒤에 존재하는 특정 문자를 제거함
```
```SQL
예제
SELECT TRIM('   !!!MySQL PHP HTML Java!!!    '), 
TRIM(LEADING '!' FROM '!!!MySQL PHP HTML Java!!!')

실행결과
!!!MySQL PHP HTML Java!!!
MySQL PHP HTML Java!!!
```

- 숫자로 이루어진 문자열의 형식화   
FORMAT() 함수는 숫자 타입의 데이터를 세 자리마다 쉼표(,)를 사용하는 '#,###,###.##' 형식으로 변환해 준다   
하지만 반환되는 데이터의 형식이 숫자 타입이 아닌 문자열 타입이므로, 주의를 기울여야 한다   
이때 두 번째 인수로 반올림할 소수 부분의 자릿수까지 전달할 수 있다
```SQL
예제
SELECT FORMAT(123456789.123456, 3);

실행결과
123,456,789.12346
```
---