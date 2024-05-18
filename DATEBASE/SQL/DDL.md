# SQL
---
## DDL (Data Defintion Language)
```
데이터 정의 언어
```
테이블이나 관계의 구조를 생성하는데 사용한다

---
### CREATE
```
테이블을 만드는 명령문
```
```sql
create table 테이블명 (
    컬럼명 데이터유형 (길이),
    컬럼명 데이터유형 (길이)
);
```

데이터의 기본 유형은 크게 `문자형 / 숫자형 / 날짜형`으로 구분 할 수 있다
|데이터 유형|설명|
|:----:|:-----|
|VCARCHAR2(size)|가변 길이 문자 데이터|
|CHAR[(size)]|길이가 size바이트인 고정 길이 문자 데이터|
|NUMBER[(p,s)]|자릿수가 p이고 소수점 이하 자릿수가 s인 숫자|
|DATE|기원전 4712년 1월 1일부터 서기 9999년 12월 31일 사이의 가장 가까운 초 단위에 대한 날짜 및 시간 값|
|Long|가변 길이 문자 데이터|
|CLOB|문자데이터|

---
### Alter
```
테이블의 특정 컬럼을 삭제하거나 추가하거나 변경할 때 사용하는 명령어
```
```sql
alter table 테이블
명령어문 입력;

-- 명령어 : add, modify, drop 등
```

alter를 통해 변경하면 `rollback, flashback`을 통해 복구가 어렵다

**alter table 구문을 통해 테이블 읽기 전용 테이블로 변환**   
```sql
alter table 테이블명 READ ONLY;
```
다시 쓰기 가능한 테이블로 변환하려면?
```sql
alter table 테이블명 READ WRITE;
```
---