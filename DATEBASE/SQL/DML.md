# SQL
---
## DML(Data Manipulation Language)
```
데이터 조작 언어
```
테이블에 데이터 검색, 삽입, 수정, 삭제하는데 사용된다

DML문이 실제로 적용되길 원한다면 `commit`을 실행해주어야 한다

---
### Insert
```
새로운 데이터를 집어넣는 기능
```
```sql
insert into 테이블(칼럼명, 칼럼명)
values(data, data)
```
data가 입력되지 않은 컬럼(변수)의 값은 `null`로 입력된다
숫자는 `'`을 사용하지 않아도 되지만, 문자와 날짜는 사용해야한다

> `''`은 null로 처리되지만 `' '`은 null로 처리되지 않는다(문자열로 인식한다)

---
### Update
```
값을 수정하는 기능
```
```sql
update 테이블
set 칼럼 = 수정할 값
where 조건
```
---