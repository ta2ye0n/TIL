# DATABASE
---
## Transaction
```
데이터베이스의 상태를 변경시키기 위해 수행하는 작업 단위
```
---
### 트랜잭션의 특징 (ACID)
```
1. 원자성(Atomicity)
2. 일관성(Consistency)
3. 독립성(lsolation)
4. 지속성(Durablility)
```
**원자성**   
```
트랜잭션이 DB에 모두 반영되거나, 전혀 반영되지 않거나를 뜻한다
(= All or Nothing)
```
트랜잭션 내의 모든 명령은 반드시 `완변히 수행`되어야 하며, 모두가 완벽히 수행되지 않고 어느 하나라도 오류가 발생하면 트랜잭션 `전부가 취소`되어야 한다

**일관성**   
```
작업 처리의 결과가 항상 일관되어야 한다
```
데이터 타입이 반환 후와 전이 `항상 동일`해야한다
(기본 키, 외래 키 제약과 같은 명시적인 무결성 제약 조건뿐만 아니라, 비명시적인 일관성 조건도 있다.)

**Isolation**   
```
하나의 트랜잭션은 다른 트랜잭션에 끼어들 수 없고 마찬가지로 독립적임을 의미한다
```
각가의 트랜잭션은 `독립적`이라 서로 간섭이 `불가능`하다

수행 중인 트랜잭션은 완전히 완료될 때까지 다른 트랜잭션에서 수행결과를 참조할 수 없다

isolation 성질을 보장할 수 잇는 가장 쉬운 방법은 `모든 트랜잭션을 순차적으로 수행하는 것`이지만, 병렬적 수행의 장점을 얻기 위해 DBMS는 `병렬적으로 수행하면서도 일렬 수행`과 같은 결과를 보장할 수 있는 방식을 제공한다

**Durablility**   
```
트랜잭션이 성공적으로 완료되면 영구적으로 결과에 반영되어야 함을 뜻한다
```
보통 `commit`이 된다면 지속성은 만족할 수 있다

성공적으로 완료된 트랜잭션의 결과는 시스템이 고장나더라도 `영구적`으로 반영되어야 한다

---
### 트랜잭션 연산
**commit**   
```
성공적으로 끝나서 데이터베이스가 일관성있는 상태에 있음을 의미
```
한개의 논리적 단위(트랜잭션)에 대한 작업이 성공적으로 끝났고 데이터베이스가 다시 일관된 상태에 있을 때,
이 트랜잭션이 행한 `갱신 연산`이 완료된 것을 트랜잭션 `관리자에게 알려`준다

**Rollback**   
```
하나의 트랜잭션 처리가 비정상적으로 종료 되었을 때의 상태
```
Rollback이 이뤄진다면 트랜잭션을 다시 실행하거나 부분적으로 변경된 `결과를 취소`할 수 있다

---
### 트랜잭션의 상태
![](https://velog.velcdn.com/images/chldppwls12/post/beb5a194-9197-4cea-9eb8-618ddca89f5a/image.png)
- `활동(Active)`   
트랜잭션이 현재 실행 중인 상태

- `실패(Failed)`   
트랜잭션 실행에 오류가 발생하여 중단된 상태
- `철회(Aborted)`   
트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태
- `부분 완료(Partially Committed)`   
트랜잭션의 마지막 연산까지 실행하고 Commit 연산이 실행되기 직전의 상태
- `완료(Committed)`   
트랜잭션이 성공적으로 종료되어 Commit 연산을 실행한 후의 상태