# Spring boot
---
## Auditing
```
사전적 의미로 감시하다, 심사하다 등의 의미를 가짐
```
변경되는 시점을 감지하여 생성시각, 수정시각, 생성한 사람, 수정한 사람을 기록할 수 있다

---
### @EnableJpaAuditing
```
Auditing을 활성화 시켜줌
```
Application 클래스에 붙이거나, @Configuration 이 사용된 클래스에 붙이면 된다

---
### @MappedSuperclass
```
JPA Entity 클래스들이 해당 추상 클래스를 상혹할 경우 createDate, modifiedDate를 컬럼으로 인식
```
---
### @EntityListeners(AuditingEntityListener.class)
```
해당 클래스에 Auditing 기능을 포함
```
---
### @CreatedDate
```
Entity가 생성되어 저장될 때 시간이 자동 저장
```
---
### @LastModifiedDate
```
조회한 Entity의 값을 변경할 때 시간이 자동 저장
```
---