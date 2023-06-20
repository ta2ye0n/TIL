# SQL
---
### SQL 작동 방식
```
구조적 쿼리 언어(SQL) 구현에는 데이터베이스 쿼리를 처리하고 결과를 반환하는 서버 시스템이 필요
```
SQL 프로세스는 다음을 포함한 여러 소프트웨어 구성요소를 거침   

● 구문 분석기
```
SQL 문의 일부 단어를 특수 기호로 토큰화하거나 바꾸는 것으로 시작
```
*정확성*
```
구문 분석기는 SQL 문이 쿼리 문의 정확성을 보장하는 SQL 의미 또는 규칙을 준수하는지 확인
```
*권한 부여*
```
구문 분석기는 쿼리를 실행하는 사용자가 해당 데이터를 조작하는데 필요한 권한이 있는지 검증
```
● 관계형 엔진
```
관계형 엔진 또는 쿼리 프로세서는 가장 효과적인 방법으로 해당 데이터를 검색, 쓰기 또는 업데이트하기 위한 계획을 만듬
```
● 스토리지 엔진
```
스토리지 엔진 또는 데이터베이스 엔진은 바이트 코드를 처리하고 의도한 SQL 문을 실행하는 소프트웨어 구성 요소
물리적 디스크 스토리지의 데이터베이스 파일에서 데이터를 읽고 저장
완료되면 스토리지엔진은 요청하는 애플리케이션에 결과를 반환
```
---
### SQL 명령
```
구조적 쿼리 언어(SQL) 명령은 개발자가 관계형 데이터베이스에 저장된 데이터를 조작하는데 사용하는 특정 키워드 또는 SQL문
```
#### SQL 명령 분류
● 데이터 정의 언어
```
데이터베이스 구조를 설계하는 SQL 명령을 나타냄
```
● 데이터 쿼리 언어
```
관계형 데이터베이스에 저장된 데이터를 검색하기 위한 명령으로 구성
소프트웨어 애플리케이션은 SELECT 명령을 사용하여 SQL 테이블의 특정 결과를 필터링하고 반환
```
● 데이터 조작 언어
```
새 정보를 쓰거나 관계형 데이터베이스의 기존레코드를 수정
```
● 데이터 제어 언어
```
데이터 제어 언어(DCL)를 사용하여 다른 사용자의 데이터베이스 액세스를 관리하거나 권한을 부여
```
● 트랜잭션 제어 언어
```
관계형 엔진은 트랜잭션 제어 언어(TCL)를 사용하여 데이터베이스를 자동으로 변경
```