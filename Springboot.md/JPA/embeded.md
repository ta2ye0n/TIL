# Spring boot
---
## JPA
---
### 임베디드 타입
임베디드 타입은 `복합 값 타입`으로 불리며 새로운 값 타입을 `직접 정의해서 사용하는 JPA`의 방법을 의미한다
주로 기본값 타입을 모아 만들어 사용한다

---
### @Embeddable / @Embedded
임베디드 타입을 적용하려면 새로운 class를 만들고 해당 클래스에 임베디드 타입으로 묶으려던 Attribute들을 넣어준 뒤 `@Embeddable`를 붙여야한다
```
사용방법
- @Embeddable : 값 타입을 정의하는 곳에 표시
- @Embedded : 값 타입을 사용하는 곳에 표시
```
---
### @AttributeOverride
```
속성명 재정의
```
같은 종류의 Attribute에 대해서 중복된 코드를 적을 필요 없이 간단하고 직관성있게 선언 가능하다

---
### 장점
- 재사용 가능
- 높은 응집도
- 객체지향적인 설계 가능