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
---
### MySQL 주요 구문
``` SQL
1. CREATE DATABASE
2. ALTER DATABASE
3. CREATE TABLE
4. ALTER TABLE
5. DROP TABLE
6. INSERT INTO
7. UPDATE
8. DELETE
9. SELECT
10. CREATE INDEX
11. DROP INDEX
```

#### 1. CREATE   
``` SQL
MySQL에서는 다음과 같은 CREATE 문을 사용하여 데이터베이스와 테이블을 만들 수 있다

1. CREATE DATABASE
2. CREATE TABLE
```
- 데이터 베이스 생성   
CREATE DATABASE 문은 새로운 데이터 베이스를 생성해 준다
``` SQL
CREATE DATABASE 데이터베이스 이름
```
> 생성된 데이터베이스 목록은 SHOW DATABASES 구문을 통해 확인할 수 있다
- 데이터베이스의 선택
데이터베이스를 생성한 후에, 해당 데이터베이스를 사용하기 위해서는 우선 데이터베이스를 선택해야 한다

USE 문을 사용하여 데이터 베이스를 선택할 수 있다
``` SQL
USE 데이터베이스 이름
```
> 유닉스 환경의 MySQL에서는 데이터베이스 이름의 대소문자를 구분한다
그러나 윈도우 환경의 MySQL에서는 데이터베이스의 이름에 대소문자를 구분하지 않는다
하지만 될 수 있으면 언제나 데이터베이스의 이름은 대소문자를 구분하여 사용하는 것이 가독성 측면에서도 좋다   
- 테이블 생성
데이터베이스는 하나 이상의 테이블로 구성되며, 이러한 테이블에 데이터를 저장하여 관리 할 수 있다

CREATE TABLE 문은 새로운 테이블을 생성해준다
``` SQL
CREATE TABLE 테이블이름
(
     필드이름1 필드타입1,
     필드이름2,필드타입2,
     ...
)
```
테이블을 생성하기 위해서는 테이블 이름,필드(field) 목록과 각 필드의 타입을 명시해야 한다
필드의 타입이란 해당 필드에 저장될 데이터가 가질 수 있는 타입을 의미한다
> MySQL에서는 위의 문법처럼 하나의 쿼리를 여러 줄에 걸쳐 입력할 수 있다
- 제약 조건(constraint)
``` SQL
제약 조건(constraint)이란 데이터의 무결성을 지키기 위해 데이터를 입력받을 때 샐행되는 검사 규칙을 의미한다

CREATE TABLE문에서 사용할 수 있는 제약 조건
1. NOT NULL : 해당 필드는 NULL값을 저장할 수 없게 된다
2. UNIQUE : 해당 필드는 서로 다른 값을 가져야만 한다
3. PRIMARY KEY : 해당 필드가 NOT NULL과 UNIQUE 제약 조건의 특징을 모두 가지게 된다
4. FOREIGN KEY : 하나의 테이블을 다른 테이블에 의존하게 만든다
5. DEFAULT : 해당 필드의 기본값을 설정한다

또한, AUTO_INCREMENT 키워드를 사용하면 해당 필드의 값을 1부터 시작하여 새로운 레코드가 추가될 때마다 1씩 증가된 값을 저장한다
이때 AUTO_INCREMENT 키워드 다음에 대입 연산자(=)를 사용하여 시작값을 변경할 수 있다
```
#### 2. ALTER
``` SQL
MySQL에서는 다음과 같은 ALTER문을 사용하여 데이터베이스와 테이블의 내용을 수정 할 수 있다

1. ALTER DATABASE
2. ALTER TABLE
```
- 데이터베이스 수정
ALTER DATABASE문은 데이터베이스의 전체적인 특성을 수정할 수 있게 해준다
이러한 데이터베이스의 특성은 데이터베이스 디렉터리의 db.opt파일에 저장되어 있다

     다음과 같은 구문을 통해 데이터베이스의 문자 집합이나 콜레이션을 변경할 수 있다
``` SQL
1. ALTER DATABASE 데이터베이스이름 CHARACTER SET = 문자집합 이름
2. ALTER DATABASE 데이터베이스이름 COLLATE = 콜레이션 이름
```
> 콜레이션(collation)이란 데이터베이스에서 검색이나 정렬과 같은 작업을 할 때 사용하는 비교를 위한 규칙의 집합을 의미한다   

자주 사용대되는 대표적인 CHARACTER SET
``` SQL
1. utf8 : UTR-8 유니코드를 지원하는 문자셋(1~3바이트)
2. euckr : 한글을 지원하는 문자셋(1~2바이트)
```
또한, 자주 사용되는 대표적인 COLLATE는 다음과 같다
``` SQL
1. utf8_bin
2. utf8_general_ci(기본 설정)
3. euckr_bin
4. euckr_korean_ci
```
> COLLATE에서 ci는 case-insensitive를 의미하며, 대소문자를 구분하지 않게 설정된다

- 테이블 수정
``` SQL
ALTER TABLE 문은 테이블에 필드를 추가, 삭제하거나 필드의 타입을 변경할 수 있게 해준다

1. ADD
2. DROP
3. MODIFY COLUMN
```
- 새로운 필드 추가   
ALTER TABLE문과 함께 ADD문을 사용하면, 테이블에 필드를 추가할 수 있다
``` SQL
ALTER TABLE 테이블이름 ADD 필드이름 필드타입
```
- 기존 필드의 삭제   
ALTER TABLE문과 함께 DROP 문을 사용하면, 테이블의 필드를 삭제할 수 있다
``` SQL
ALTER TABLE 테이블이름 DROP 필드 이름
```
- 필드 타입 변경   
ALTER TABLE 테이블 이름 MODIFY COLUMN 필드이름 필드타입
``` SQL
ALTER TABLE 테이블이름 MODIFY COLUMN 필드이름 필드타입
```