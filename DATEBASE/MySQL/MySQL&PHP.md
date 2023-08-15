# 관계형 데이터 베이스
---
## MySQL과 PHP
```
MySQL은 C언어, C++,JAVA,PHP 등 다양한 프로그래밍 언어와 결합하여 사용할 수 있다
이 중에서도 MySQL을 이용한 웹 개발에는 PHP가 가장 많이 사용되고 있다

PHP는 MySQL을 조작하기 위한 많은 함수를 별도로 제공하고 있다
이러한 함수를 사용하면 PHP 스크립트 상에서 MySQL과 관련된 거의 모든 작업을 수행할 수 있다
```
---
### PHP 기초
- MySQLi와 PDO
```
예전에는 PHP에서 MySQL데이터베이스에 연결하기 위해 MySQL extension이라는 API를 사용했다
MySQL Extension은 mysql_로 시작하는 다양한 함수를 사용하여 MySQL 데이터베이스를 관리할 수 있었다

하지만 이 API는 PHP 5.5.0부터는 사용을 권장하지 않고(deprecated) 있으며, PHP 7.0.0에서는 삭제되었다
따라서 현재 PHP를 사용하여 MySQL 데이터베이스에 연결하기 위해 사용할 수 있는 API는 다음과 같다

1. MySQL improved extension(MySQLi extension)
2. PHP Data Objects(PDO)

위의 두 가지 API는 각각 장단점을 가지지만, MySQL 환경에서 성능상의 큰 차이를 보이지는 않는다
하지만 MySQLi는 객체 기반 형식(object-oriented)과 절차식 형식(procedural)으로 모두 사용할 수 있다
```

- PHP와 MySQL의 동작 원리   
PHP와 연동되어 사용되는 MySQL의 동작 원리
![](https://www.tcpschool.com/lectures/img_php_works.png)
```
1. 클라이언트가 브라우저를 통해 웹 서버에 원하는 웹 페이지를 요청한다
2. 웹 서버는 클라이언트가 요청한 웹 페이지의 내용 작성 및 데이터베이스와의 연동을 위해 PHP파서(parser)에 이것에 대한 처리를 요청한다
3. 이때 PHP 파서는 데이터베이스와의 연동이 필요하면 데이터베이스에 접속해서 SQL문을 확인하고, 데이터베이스와 데이터의 처리를 수행한다
4. PHP 파서는 웹 페이지의 내용 작성 및 데이터베이스의 작업 처리 결과를 웹 서버로 전달한다
5. 웹 서버는 완성된 웹 페이지를 클라이언트의 브라우저로 전송한다
```
---
