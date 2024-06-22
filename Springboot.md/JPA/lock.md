# JPA
---
## Lock
```
여러 커넥션에서 동시에 동일한 자원을 요청할 경우 순서대로 하나의 커넥션만 변경할 수 있게 해주는 기능
```
종류는 DB인지 Spring인지에 따라 다르다

---
### 낙관적 락(Optimistic Lock)
```
충돌이 일어나지 않을 것이다

낙관적으로 생각해서 자원에 락을 걸지 않고 충돌이 발생했을때 처리하는 방법
```
DB의 Lock을 사용하지 않고 `Version관리`를 통해 애플리케이션 레벨에서 처리한다
이는 DB에서 동시성을 처리하는 것이 아니라 `애플케이션 단에서 처리하는 방법`이다

- 장점   
충돌이 적은 경우 동시성에 대해서 성능적으로 우수하다

- 단점   
충돌이 많은 경우 롤백처리에 대한 비용이 많이 들어 성능적으로 불리해진다   
롤백 처리 구현이 어려울 수 있다

---
### 비관적 락 (Pessimistic Lock)
```
충돌이 일어날 것이다

비관적으로 생각해서 미리 락을 걸어주는 방법
```
하나의 트랜잭션이 자원에 접근 시 락을 걸고 다른 트랜잭션이 접근하지 못하게 한다

이때 `Shared Lock`과 `Exclusive Lock` 두 가지를 걸 수 있다

`Shared Lock`   
다른 트랜잭션에서 `읽기만 가능`하고 다른 트랜잭션의 Shared Lock과 `자원을 공유`한다
하지만 Exclusive Lock은 `접근할 수 없다`

`Exclusive Lock`   
읽기, 쓰기 다 `공유하지 않는다`

- 장점   
충동이 많은 경우 롤백 횟수를 줄여 성능적인 측면에서 좋다   
데이터 일관성과 무결성을 보장하는 수준이 매우 높다

- 단점   
읽기 작업이 많은 로직의 경우엔 동시성이 떨어지기 때문에 성능이 좋지 않다   
락을 거는 순서가 다른 경우에 데드락이 발생할 수 있다

---