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
---
### PRIMARY KEY
```
PRIMARY KEY 제약 조건을 설정하면, 해당 필드는 NOT NULL과 UNIQUE 제약 조건의 특징을 모두 가진다
따라서 이 제약 조건이 설정된 필드는 NULL 값을 가질 수 없으며, 또한 중복된 값을 가져서도 안된다
이러한 PRIMARY KEY 제약 조건을 기본 키라고 한다

UNIQUE는 한 테이블의 여러 필드에 설정할 수 있지만, PRIMARY KEY는 테이블당 오직 하나의 필드에만 설정할 수 있다
이러한 PRIMARY KEY 제약 조건은 테이블의 데이터를 쉽고 빠르게 찾도록 도와주는 역할을 한다
```

- CREATE 문으로 PRIMARY KEY 설정   
CREATE 문으로 테이블을 생성할 때 해당 필드의 타입 뒤에 PRIMARY KEY를 명시하면, 해당 필드가 기본 키로 설정된다
```SQL
문법
1. CREATE TABLE 테이블 이름
(
   필드이름 필드타입 PRIMARY KEY,
   ...
)

2. CREATE TABLE 테이블 이름
(
   필드이름 필드타입,
   ...
   [CONSTRAINT 제약조건이름] PRIMARY KEY (필드이름)
)
```
> 두 문법은 모두 해당 필드에 PRIMARY KEY 제약 조건을 설정한다
이때 두 번째 문법을 사용하면, 해당 제약 조건에 이름을 설정할 수 있다

- ALTER 문으로 PRIMARY KEY 설정   
ALTER문으로 테이블에 새로운 필드를 추가하거나 수정할 때도 PRIMARY KEY 제약 조건을 설정할 수 있다
```SQL
문법
1. ALTER TABLE 테이블 이름
   ADD 필드이름 필드타입 PRIMARY KEY

2. ALTER TABLE 테이블이름
   ADD [CONSTRAINT 제약조건이름] PRIMARY KEY(필드이름)
```
기존에 존재하는 필드를 기본 키로 설정하는 문법
```SQL
1. ALTER TABLE 테이블 이름
   MODIFY COLUMN 필드이름 필드타입 PRIMARY KEY

2. ALTER TABLE 테이블 이름
   MODIRY COLUMN [CONSTRAINT 제약조건이름] PRIMARY KEY (필드이름)
```
> PRIMARY KEY 제약 조건을 추가할 기존 필드는 NULL 값을 갖지 않도록 먼저 선언되어 있어야 한다

설정된 PRIMARY KEY 제약 조건을 삭제하는 방법
```SQL
문법
ALTER TABLE 테이블이름
DROP PRIMARY KEY
```
---
### FOREIGN KEY
```
FOREIGN KEY 제약 조건을 설정한 필드는 외래 키라고 부르며, 한 테이블을 다른 테이블과 연결해주는 역할을 한다
외래 키가 설정된 테이블에 레코드를 입력하면, 기준이 되는 테이블의 내용을 참조해서 레코드가 입력된다
즉, FOREIGN KEY 제약 조건은 하나의 테이블을 다른 테이블에 의존하게 만든다

FOREIGN KEY 제약 조건을 설정할 때 참조되는 테이블의 필드는 반드시 UNIQUE나 PRIMARY KEY 제약 조건이 설정되어 있어야 한다
```
- CREATE 문으로 FOREIGN KEY 설정   
CREAT문으로 테이블을 생성할 때 필드의 타입 뒤에 FOREIGN KEY를 명시하면, 해당 필드가 외래 키로 설정된다
```SQL
문법
CREATE TABELE 테이블 이름
(
   필드이름 필드타입,
   ...,
   [CONSTRAINT 제약조건이름]
   FOREIGN KEY(필드이름)
   REFERENCES 테이블이름(필드이름)
)
```
> 위의 문법을 사용하면 해당 필드에 FOREIGN KEY 제약 조건을 설정한다  
> 이때 참조되는 테이블의 이름은 REFERENCES 키워드 다음에 명시된다

- ALTER 문으로 FOREIGN KEY 설정   
테이블에 새로운 필드를 추가할 때 해당 필드를 외래 키로 설정하는 문법
```SQL
ALTER TABLE 테이블이름
ADD [CONSTRAINT 제약조건이름]
FOREIGN KEY (필드이름)
REFERENCES 테이블이름 (필드이름)
```

FOREIGN KEY 제약 조건 삭제하는 방법
```SQL
ALTER TABLE 테이블이름
DROP FOREIGN KEY 제약조건이름
```

- ON DELETE, ON UPDATE
```
FOREIGN KEY 제약 조건에 의해 참조되는 테이블에서 데이터의 수정이나 삭제가 발생하면, 참조하고 있는 테이블의 데이터도 같이 영향을 받는다
이때 참조하고 있는 테이블의 동작은 다음 키워드를 사용하여 FOREIGN KEY 제약조건에서 미리 설정할 수 있다

1. ON DELETE
2. ON UPDATE

참조되는 테이블의 값이 삭제 될 경우의 동작은 ON DELETE 구문으로 설정할 수 있다
또한, 참조되는 테이블의 값이 수정될 경우의 동작은 ON UPDATE 구문으로 설정할 수 있다
```
설정 할 수 있는 동작
   1. CASCADE
   ```
   참조되는 테이블에서 데이터를 삭제하거나 수정하면, 참조하는 테이블에서도 삭제와 수정이 같이 이루어진다
   ```
   2. SET NULL
   ```
   참조되는 테이블에서 데이터를 삭제하거나 수정하면, 참조하는 테이블의 데이터는 NULL로 변경된다
   ```
   3. NO ACTION 
   ```
   참조되는 테이블에서 데이터를 삭제하거나 수정해도, 참조하는 테이블의 데이터는 변경되지 않는다
   ```
   4. SET DEFAULT
   ```
   참조되는 테이블에서 데이터를 삭제하거나 수정하면, 참조하는 테이블의 데이터는 필드의 기본값으로 설정된다
   ```
   5. RESTRICT
   ```
   참조하는 테이블에 데이터가 남아 있으면, 참조되는 테이블의 데이터를 삭제하거나 수정할 수 없다
   ```