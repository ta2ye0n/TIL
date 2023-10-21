# DAO, DTO, VO
---
## DAO
```
Data Access Object
Database에 접근하는 역할을 하는 객체
```
- 프로젝트의 서비스 모델에 해당하는 부분과 데이터베이스를 연결하는 역할

- 데이터의 CRUD 작업을 시행하는 클래스 즉, 데이터에 대한 `CRUD 기능을 전담하는 오브젝트`
> repository := dao (비슷함)


### 사용이유
- `효율적인 커넥션 관리`와 `보안성`
- DAO는 비즈니스 로직을 분리하여 도메인 로직으로부터 DB와 관련한 메커니즘을 숨기기 위해 사용

---
## DTO
```
Data Transfer Object
데이터를 전달하기 위한 객체

로직을 가지지 않는 순수한 데이터 객체(getter & setter만 가진 클래스)
```
- 여러 레이어(Layer)간 데이터를 주고 받을 때 사용할 수 있고 `주로 View와 Controller 사이에서 활용`
- DTO는 `getter / setter 메서드`를 포함한다 하지만, 이외의 다른 비즈니스 로직은 포함하지 않는다
- DTO는 어떻게 구현하느냐에 따라 `가변 객체`로 활용할 수도 있고 `불변 객체`로 활용할 수도 있다

### 불변 / 가변 객체
- 가변 객체로써 DTO를 만들 때는 `setter() 메서드를 이용하여 구현`할 수 있다
- 불변 객체로써 DTO를 만들 때는 `생성자를 이용해서 구현시 getter() 메서드만 구현`할 수 있다
- 이러게 구현함으로써 데이터를 전달하는 과정에서 `데이터의 불변성을 보장`한다

---
## VO
```
Value Object
값 자체를 표현하는 객체
```
- DTO와 유사하지만 DTO는 setter를 가지고 있어 값이 변할 수 있다
- `getter() 메서드`를 포함해서, 이외의 비즈니스 로직도 포함할 수 있다
- setter() 메서드는 가지지 않아 `읽기 기능`만 가능하다(read-Only)
- `두 객체의 모든 필드 값들이 동일하면 두 객체는 같다`
---
### DTO vs VO
|종류|용도|동등 결정|가변 / 불변|로직|
|:---:|:----:|:----:|:-----:|:-----:|
|DTO|계층 간 데이터 전달|속성값이 모두 같아도 같은 객체가 아닐 수 있음|setter 존재 시 가변 / seeter 비존재 시 불변|getter/setter 이외의 로직이 불필요함|
|VO|값 자체를 표현|속성값이 모두 같으면 같은 객체|불변|getter / setter 이외의 로직을 가질 수 있음|