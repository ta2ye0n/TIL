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
---
### UNIQUE
```
UNIQUE 제약 조건을 설정하면, 해당 필드는 서로 다른 값을 가져야 한다
즉, 이 제약 조건이 설정된 필드는 중복된 값을 저장할 수 있다

UNIQUE 제약 조건은 CREATE 문으로 테이블을 생성할 때나, 나중에 ALTER 문으로 추가할 수도 있다
```

- CREATE문으로 UNIQUE 설정   
CREATE 문으로 테이블을 생성할 때 해당 필드의 타입 뒤에 UNIQUE를 명시하면, 해당 필드에는 더는 중복된 값을 저장할 수 없다
```SQL
문법
1. CREATE TABlE 테이블 이름
(
    필드명 필드타입 UNIQUE,
    ...
)

2. CREATE TABLE 테이블 이름
(
    필드이름 필드타입
    ...,
    [CONSTRAINT 제약조건이름] UNIQUE (필드이름)
)
```
위의 두 문법은 모두 해당 필드에 UNIQUE 제약 조건을 설정한다
이때 두번째 문법을 사용하면, 해당 제약 조건에 이름을 설정할 수 있다

- ALTER 문으로 UNIQUE 설정
ALTER 문으로 테이블에 새로운 필드를 추가하거나 수정할 때도 UNIQUE 제약 조건을 설정할 수 있다

테이블에 새로운 필드를 추가할 때 UNIQUE 제약 조건을 설정하는 문법
```SQL
문법 
1. ALTER TABLE 테이블 이름
   ADD 필드이름 필드타입 UNIQUE

2. ALTER TABLE 테이블 이름
   ADD [CONSTRATINT 제약조건이름] UNIQUE(필드이름)
```

기존 필드에 UNIQUE 제약조건을 설정하는 문법
```SQL
1. ALTER TABLE 테이블이름
   MODIFY COLUMN 필드이름 필드타입 UNIQUE

2. ALTER TABLE 테이블이름
   MODIFY COLUMN [CONSTRAINT 제약조건이름] UNIQUE(필드이름)
```

제약 조건에 이름을 설정하면, 다음과 가이 이름을 사용하여 해당 제약 조건을 삭제할 수 있다
```SQL
문법
ALTER TABLE 테이블이름
DROP INDEX 제약조건이름
```
> UNIQUE 제약조건을 설정하면, 해당 필드는 자동으로 인덱스(INDEX)로 만들어진다