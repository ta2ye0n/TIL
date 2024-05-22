# SQL
---
## DCL(Data Control Language)
```
데이터 제어어
```
데이터 관리 목적으로 보안, 무결성, 회복, 병행 제어 등을 정의하는데 사용한다

---
### GRANT
```
권한을 정의할 때 사용하는 명령어
```
```sql
-- 시스템권한 부여
GRANT [시스템 권한 / ROLE] TO [사용자 이름 / ROLE 이름 / PUBLIC] [WITH ADMIN OPTION]

-- 객체 권한 부여
GRANT [객체 권한] ON [스키마.객체이름] TO [사용자 이름 / ROLE 이름 / PUBLIC] [WITH GRANT OPTION]
```
- PUBLIC : 시스템 권한 및 ROLE을 모든 사용자에게 부여
- WITH ADMIN OPTION : 부여받은 권한을 다른 사용자 및 ROLE에게 부여할 수 있는 권한도 함께 부여받음

---
### REVOKE
```
권한을 삭제할 때 사용하는 명령어
```
```sql
-- 시스템권한 삭제
REVOKE [시스템 권한 / ROLE] FROM [사용자 이름 / ROLE 이름 / PUBLIC]

-- 객체 권한 부여
REVOKE [권한 / ALL] ON [스키마.객체이름] FROM [USER / ROLE / PUBLIC] [CASCADE CONSTRATINTS]
```
- CASCADE CONSTRAINTS : 참조 객체에 사용된 참조 무결성 제약을 함께 삭제할 수 있음
- `객체 권한의 회수는 부여한 사용자만`이 할 수 있다 

---