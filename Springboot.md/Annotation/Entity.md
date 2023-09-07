# Annotation
---
## Entity
`실체, 객체`라는 의미를 가지며 업무에 필요하고 유용한 정보를 `저장하고 관리하기 위한 집합적인 것`이다
파일시스템이나 데이터베이스에서의 레코드가 개체에 해당한다

---
### @Entity
`JPA`를 사용해 테이블과 매핑할 클래스에 붙여준다
데이터베이스의 `테이블과 일대일로 매칭되는 객체 단위`이며 Entity 객체의 인스턴스 하나가 테이블에서 하나의 `레코드 값`을 의미한다

|속성|기능|
|:-----:|:-----:|
|name|`JPA에서 사용할 엔티티 이름지정`<br> name을 쓰지 않을 경우 (default) 클래스이름을 엔티티이름으로 지정|

> 주의 사항
> - 기본생성자가 꼭필요
> - final, enum, interface, innter class에서는 사용불가
> - 필드(변수)를 final로 선언 불가
---
### @Table
엔티티와 `매핑할` 테이블 지정

|속성|기능|
|:-----:|:------:|
|name|매핑할 테이블 이름 <br> `생략시 엔티티이름 (@Entity(name="~")) 사용`|
|catalog|catalog 기능이 있는 DB에서 catalog 매핑|
|schema|schema 기능이 있는 DB에서 schema 매핑|
|uniqueContraints| DDL 생성시 유니크 제약조건 생성 <br> ※ 스키마 자동 생성 기능을 사용해 DDL을 만들 때만 사용|

> DDL -> 데이터 정의어

---
### @Id
`특정 속성을 기본키로 설정`하는 어노테이션이다   
@Id 어노테이션만 적게될 경우 `기본키값을 직접 부여`해줘야 한다
> 보통은 기본키를 직접 부여하지 않고 Mysql AUTO_INCREMENT처럼 자동 부여되게끔 한다

---
### @GeneratedValue
Id의 값을 entity가 생성될 때마다 `자동 생성`되게 해주는 어노테이션이다
사용하게 되면 `기본값을 DB에서 자동으로 생성하는 전략`을 사용 할 수 있다

전략에는 `IDENEITY, SEQUENCE, TABLE` 3가지가 있다
|속성|기능|
|:------:|:-------:|
|@GeneratedValue(startegy = GenerationType.IDENTITY)|기본 키 생성을 DB에 위임(Mysql)|
|@GeneratedValue(startegy = GenerationType.SEQUENCE)|DB시퀀스를 사용해서 기본 키 할당 (ORACLE)|
|@GeneratedValue(startegy = GenerationType.TABLE)|키 생성 테이블 사용 (모든 DB 사용 가능)|
|@GeneratedValue(startegy = GenerationType.AUTO)|선택된 DB에 따라 자동으로 전략 선택|
다양한 전략이 있는 이유는 `DB마다 지원하는 방식이 다르기` 때문이다
`AUTO 같은 경우 DB에 따라 전략을 JPA가 자동으로 선택`한다 이로 인해 DB를 변경해도 코드를 수정할 필요 없다는 장점이 있다

---
### @Column
`객체 필드`를 테이블의 `컬럼에 매핑`시켜주는 어노테이션이다

|속성|기능|기본값|
|:------:|:------:|:------:|
|name|필드와 매핑할 테이블의 컬럼 이름을 지정<br> `default는 필드이름으로 대체`|객체의 필드 이름|
|insertable<br>(거의 사용하지 않음)|ture : 엔티티 저장시 필드값 저장 <br> false : 필드값이 저장되지 않음|true|
|updatable|true: 엔티티 수정시 값이 수정<br>false: 엔티티 수정시 값이 수정 되지 않음|true|
|table<br>(거의 사용하지 않음)|하나의 엔티티를 두개 이상의 테이블에 매핑할 때 사용(@SecondaryTable 사용)|현재 클래스가 매핑된 테이블|
|nullable(DDL)|null값 허용 여부 설정 <br> false: not null 제약조건|true|
|unique(DDL)|컬럼에 유니크 제약조건 부여|false|
|columnDefinition(DDL)|데이터베이스 컬럼 정보를 직접 부여|자바 필드의 타입과, 데이터베이스 방언 설정 정보를 사용해 적절히 생성|
|length(DDL)|문자 길이 제약조건 <br> `String 타입일 때 사용`|255|
|precision,scale(DDL)|BigDecimal 타입에서 사용 <br> precision: 소수점을 포함한 전체 자릿수 설정 <Br> scale : 수수의 자릿수|precision = 0 <Br> scale = 0|

> @Column의 unique 속성을 true로 사용할 경우 유니크 제약조건의 이름을 다음과 같이 생성한다
>```sql
>ex) UK_dqwjdiowqfnjoiwqfejwqe34912mdqw 
>```
> 위와 같이 랜덤한 이름을 사용하므로 알아보기 힘들다   
따라서 @COlumn의 unique 속성보다는 `@Table의 uniaueConstraints 속성을 사용`하여 제약조건의 이름을 걸어주는 방법을 사용하는 것이 바람직하다

---
### @Access
`JPA가 엔티티 데이터에 접근하는 방식`을 지정한다
|접근 방식|기능|
|:-----:|:------:|
|AccessType.FILED|필드에 직접 접근 <br> 필드 접근 권한이 private여도 접근 가능|
|AccessType.PROPERTY|`getter`를 통해 접근|
@Access를 설정하비 않으면 기본키를 설정하는 `@Id의 위치를 기준으로 접근 방식 설정`

---
### @Enumerated
자바 `enum 타입을 매핑`할 때 사용한다
> enum -> 열거형이라고 불리며, 서로 연관된 상수들의 집합을 의미한다

|속성|기능|
|:-----:|:-----:|
|value|EnumType.ORDINAL : enum 순서를 DB에 저장 <br> EnumType.STRING : enum이름을 DB에 저장|

---
### @Transient
`DB에 저장하지도 않고 조회하지도 않는다` 객체에 임시로 값을 보관하고 싶을 때 사용한다

---
### @Temporal
`날짜 타입을 매핑`할 때 사용한다

|속성|기능|
|:-------:|:-------:|
|value|`TemporalType.DATE` : 날짜 DB data 타입과 매핑(ex 2020-02-12) <br>`TemporalType.TIME` : 시간, DB time 타입과 매핑 (ex 12:12:12)<br>`TemporalType.TIMESTAMP` : 날짜와 시간 DB timestamp 타입과 매핑 (예 : 2020-02-12 12:12:12)|

> Java 8이상에서는 LocalDate, LocalDateTime 타입이 지원되기 때문에 @Temporal을 사용하지 않아도 된다

---
### @Lob
데이터베이스에서 `VARCHAR보다 큰 데이터를 담고 싶을 때 사용`한다

DB BLOB, CLOB 타입과 매핑 @Lob은 정의할 속성이 따로 없다
```
CLOB - 문자기반의 데이터를 저장하는데 사용된다
BLOB - binary 데이터를 저장하는 사용된다

String과 char를 기본으로 하는 타입을 제외하면 @BLOB으로 사용된다
```
---
### 연관관계 매핑
`객체의 참조와 테이블의 외래 키를 매핑하는 것`을 의미한다

1. 방향
    - `단방향 관계` : 두 엔티티가 관계를 맺을 때, 한 쪽의 엔티티만 참조하고 있는 것을 의미
    - `양방향 관계` : 두 엔티티가 관계를 맺을 때, 양 쪽이 서로 참조하고 있는 것을 의미

> 객체지향 모델링에서는 구현하고자 하는 서비스에 따라 단반향 관계인지, 양방향 관계인지 적절한 선택을 해야 한다

2. 다중성   
관계에 있는 두 엔티티는 다음 주 하나의 관계를 갖는다
    - `@ManyToOne` : 다대일 (N : 1)
    - `@OneToMany` : 일대다 (1 : N)
    - `@OneToOne` : 일대일 (1 : 1)
    - `@ManyToMany` : 다대다 (N : N)

> 어떤 엔티티를 중심으로 상대 엔티티를 바라보느냐에 따라 다중성이 다르게 된다

3. 연관관계의 주인 (Owner)   
연관관계를 갖는 두 테이블에서 `외래키를 갖게되는 테이블이 연관관계의 주인`이 된다
연관관계의 `주인만이 외래 키를 관리(등록, 수정, 삭제)`할 수 있고, `주인이 아닌 엔티티는 읽기`만 할 수 있다

---
### @JoinColumn
`외래 키`를 매핑할 때 사용한다

|속성|기능|기본값|
|:------:|:-----:|:------:|
|name|`매핑할 외래 키 컬럼명`|필드명_[참조하는 테이블의 기본 키 컬럼명]|
|referencedColumnName|`외래 키가 참조하는 대상 테이블의 컬럼명`|참조하는 테이블의 기본 키 컬럼명|
|foreignKey(DDL)|외래 키 제약조건을 직접 지정할 때 사용하며, 테이블을 생성할 때만 사용한다||
|unique <br> nullable <br> insertable <br> undatable <br> columnDfinition <br> table |@Column의 속성과 동일하다

> name과 referencedColumnName을 착각하지 않도록 주의!!
name은 마음대로 지정해주어도 되지만, referencedColumnName는 마음대로 지정해주면 예외가 발생한다