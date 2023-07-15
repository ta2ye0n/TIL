# 관계형 데이터베이스
---
## 제약조건(constraint)
```
제약 조건(constraint)이란 데이터의 무결성을 지키기 위해, 데이터를 입력받을 때 실행되는 검사 규칙을 ㅡ이미한다
이러한 제약 조건은 CREATE 문으로 테이블을 생성할 때나 ALTER문으로 필드를 추가할 때도 설정할 수 있다

MySQL에서 사용할 수 있는 제약 조건
1. NOT NULL
2. UNIQUE
3. PRIMARY KEY
4. FOREIGN KEY
5. DEFAULT
```
---
### NOT NULL
```
NOT NULL 제약 조건을 설정하면, 해당 필드는 NULL 값을 저장할 수 없다
즉, 이 제약 조건이 설정된 핃드는 무조건 데이터를 가지고 있어야한다

NOT NULL 제약 조건은 CREATE 문으로 테이블을 생성할 때나, 나중에 ALTER 문으로 추가할 수도 있다
```
- CTREATE 문으로 NOT NULL 설정
```SQL
CREATE 문으로 테이블을 생성할 때 해당 필드의 타입 뒤에 NOT NULL을 명시하면,
해당 필드는 NULL 값을 가질 수 없다

문법
CREATE TABLE 테이블이름
(
    필드이름 필드타입 NOT NULL,
    ...
)
```
- ALTER 문으로 NOT NULL 설정
```SQL
ALTER 문으로 테이블에 새로운 필드를 추가하거나 수정할 때도 NOT NULL 제약 조건을 설정할 수 있다

테이블에 새로운 필드를 추가할 때  NOT NULL 제약 조건을 설정하는 문법
ALTER TABLE 테이블 이름
ADD 필드이름 필드타입 NOT NULL

기존 필드에 NOT NULL 제약 조건을 설정하는 문법
ALTER TABLE 테이블이름
MODIFY COLUMN 필드이름 필드타입 NOT NULL
```