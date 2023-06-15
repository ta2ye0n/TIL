# 관계형 데이터 베이스
---
## MySQL 기본 문법

### MySQL 구문
MySQL에서 데이터베이스에 대한 작업 명령은 SQL 구문을 이용하여 처리 된다
``` SQL
SELECT * FROM Reservation;
```

서버와의 연결을 끊는 구문인 QUIT와 같은 경우를 제외한 일반적인 구문 뒤에는 세미콜론(;)을 붙인다
이러한 세미콜론은 SQL 구문을 구분하는 기준이 된다

또한, MySQL은 키워드와 구문에서 대소문자를 구분하지 않는다
``` SQL
1. SELECT * FROM Reservation;
2. select * from Reservation;
3. SeLECt * FrOm Reservation;
```

### MySQL 주석
```
주석이란 코드에 대한 이해를 돕는 설명을 적거나 디버깅을 위해 작성하는 일종의 메모

1. # 한줄 주석
2. -- 한줄 주석
3. /* 두줄
     이상의
     주석 */

- 두번째 방법에서 두개 이상의 하이픈(-) 뒤에는 반드시 한 칸의 공백이 존재해야만 주석으로 정상 인식 된다
```