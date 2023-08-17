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
### MySQL 연결
- 서버와의 연결
PHP를 사용하여 MySQL 데이터베이스에 접속하기 우해서는 우선 서버와의 연결이 필요하다   
MySQLi에서는 서버와의 연결을 위해 mysqli_connect()함수를 제공하고 있다
```SQL
MySQLi를 사용하여 서버와 연결하는 예제

<?php

    $servername = "localhost";
    $user = "choi";
    $password = "0219";

①  $connect = mysqli_connect($servername, $user, $password);
    if (!$connect) {
②      die("서버와의 연결 실패! : ".mysqli_connect_error());
    }
    echo "서버와의 연결 성공!";
?>
```
위 예제의 ①번 라인에서는 mysql_conncect() 함수에 서버 이름, 사용자명과 비밀번호를 전달하여 서버와의 연결을 시도한다   
만약 서버와의 연결에 실패했다면, mysqli_connect_error() 함수를 사용하여 마지막 에러 메시지를 출력한다

> die() 함수는 인수로 전달받은 메시지를 출력하고, 현재 실행 중인 PHP 스크립트를 종료시키는 함수이다

- 서버와의 연결 종료
이렇게 생성된 서버와의 연결은 PHP 스크립트가 끝나면 자동으로 같이 종료된다
하지만 PHP 스크립트가 끝나기 전에 서버와의 연결을 종료하고 싶다면, mysqli_close() 함수를 호촐하면 된다
```SQL
예제
<?php
    mysqli_close($connect);
?>
```
---
### MySQL CREATE
- 데이터베이스 생성
MySQL의 CREATE dATABASE문은 새로운 데이터 베이스를 생성할 때 사용한다
```SQL
예제
<?php
    $servername = "localhost";
    $user = "choi";
    $password = "0219";

    $connect = mysqli_connect($servername, $user, $password);

    if (!$connect) {
        die("서버와의 연결 실패! : ".mysqli_connect_error());
    }
 
①  $sql = "CREATE DATABASE Hotel";

②  if (mysqli_query($connect, $sql)) {
        echo "데이터베이스 생성 성공!";
    } else {
        echo "데이터베이스 생성 실패! : ".mysqli_error($connection);
    }
   mysqli_close($connection);
?>
```
위 예제의 ①번 라인에서는 Hotel이라는 ㅇ름의 데이터베이스를 생성하는 SQL 구문(statement)을 작성한다
이렇게 작성한 SQL 구문을 ②번 라인에서 mysqli_query() 함수에 인수로 전달하여 실행한다

mysqli_query() 함수는 인수로 전달받은 SQL 구문을 실행하여, 그 결과를 반환하는 함수이다   
이 함수는 해당 구문의 실행에 실패하면 FALSE를 반환한다   
그리고 SELECT,SHOW,DESCRIBE,EXPLAIN 문을 성공적으로 실행했을 경우에는 해당 결과가 저장된 결과 집합인 mysqli_result 객체를 반환하며, 그 외의 구문이 성공적으로 실행되면 TRUE를 반환한다

- 데이틀 생성
데이터베이스는 하나 이상의 테이블로 구성되며, 이러한 테이블에 데이터를 저장하여 관리할 수 있다 
MySQL의 CREATE TABLE문은 새로운 데이터베이스를 생성할 때 사용한다
```SQL
4개의 필드를 갖는 Reservation 테이블을 생성하는 PHP 예제

<?php
    $servername = "localhost";
    $user = "choi";
    $password = "0219";
    $dbname = "testDB";

    $connect = mysqli_connect($servername, $user, $password, $dbname);
    if (!$connect) {
        die("서버와의 연결 실패! : ".mysqli_connect_error());
    }

①  $sql = "CREATE TABLE Reservation
    (
        ID INT PRIMARY KEY,
        Name VARCHAR(30) NOT NULL,
        ReservDate DATE NOT NULL,
        RoomNum INT
    )";

    if (mysqli_query($connect, $sql)) {

        echo "테이블 생성 성공!";
    } else {
        echo "테이블 생성 실패! : ".mysqli_error($connection);
    }
    mysqli_close($connection);
?>
```
위의 예제는 ①번 라인에서는 4개의 필드를 갖는 Reservation이라는 이름의 테이블을 생성하는 SQL 구문을 작성한다   
테이블을 생성할 때는 필드의 이름뿐만 아니라 타입, 제약조건 등을 함께 명시할 수 있다

> mysqli_error() 함수는 마지막으로 발생한 에러에 대한 정보를 문자열로 반환하는 함수이다

---
### MySQL INSERT
- 레코드 추가
INSERT INTO문을 사용하면 테이블에 새로운 레코드를 추가할 수 있다
```SQL
Reservation 테이블에 새로운 레코드를 추가하는 PHP 예제

<?php
    $servername = "localhost";
    $user = "choi";
    $password = "0219";
    $dbname = "testDB";

    $connect = mysqli_connect($servername, $user, $password, $dbname);
    if (!$connect) {
        die("서버와의 연결 실패! : ".mysqli_connect_error());
    }
    echo "서버와의 연결 성공!";

    // VALUES 절을 통해 전달한 데이터로 Reservation 테이블에 새로운 레코드를 추가하는 SQL 구문
①  $sql = "INSERT INTO Reservation(ID, Name, ReserveDate, RoomNum)
        VALUES(5, '이순신', '2016-02-16', 1108)";

    if (mysqli_query($connect, $sql)) {

        echo "레코드 추가 성공!";
    } else {
        echo "레코드 추가 실패! : ".mysqli_error($connection);
    }
    mysqli_close($connection);
?>
```
위 예제의 ①번 라인에서는 Reservation 테이블에 새로운 레코드를 추가하는 SQL 구문을 작성한다
이때 VALUES 절을 사용하여 새로운 레코드를 구성할 데이터를 함께 전달하고 있다

> 문자열 데이터에는 따옴표를 사용해야 하며, 숫자 데이터에는 따옴표를 사용하지 않아도 된다

- 여러 레코드 추가
mysqli_multi_query() 함수를 사용하면, 여러 레코드를 한 번에 추가할 수 있다   
이때 각각의 INSERT 문은 반드시 세미콜론(;)으로 구분하여 하나의 문자열로 전달해야한다
```SQL
Reservation 테이블에 여러 개의 새로운 레코드를 한 번에 추가하는 PHP 예제
<?php
    $servername = "localhost";
    $user = "choi";
    $password = "0219";
    $dbname = "testDB";

    $connect = mysqli_connect($servername, $user, $password, $dbname);
    if (!$connect) {
        die("서버와의 연결 실패! : ".mysqli_connect_error());
    }
    echo "서버와의 연결 성공!";

①  $sql = "INSERT INTO Reservation(ID, Name, ReserveDate, RoomNum)

        VALUES(1, '홍길동', '2016-01-05', 2014);";
②  $sql .= "INSERT INTO Reservation(ID, Name, ReserveDate, RoomNum)
        VALUES(2, '임꺽정', '2016-02-12', 918);";
③  $sql .= "INSERT INTO Reservation(ID, Name, ReserveDate, RoomNum)
        VALUES(3, '장길산', '2016-01-16', 1208)";

    if (mysqli_query($connect, $sql)) {
        echo "레코드 추가 성공!";
    } else {
        echo "레코드 추가 실패! : ".mysqli_error($connection);
    }
    mysqli_close($connection);
?>
```
위 예제의 ①번 라인에서는 Reservation 테이블에 새로운 레코드를 추가하는 SQL 구문을 작성하고 있다   
그리고 ②번과 ③번 라인에서 새로운 레코드를 추가하는 SQL 구문을 더 작성하여 그것을 문자열 형태로 추가하고 있다   
이때 SQL 구문 사이에는 세미콜론(;)이 반드시 추가되어야 한다

---
### MySQL UPDATE
- 레코드 수정
UPDATE 문을 사용하면 테이블에 저장된 레코드의 내용을 수정할 수 있다
```SQL
Reservation 테이블의 레코드의 내용을 수정하는 PHP 예제

<?php
    $servername = "localhost";
    $user = "choi";
    $password = "0219";
    $dbname = "testDB";

    $connect = mysqli_connect($servername, $user, $password, $dbname);
    if (!$connect) {
        die("서버와의 연결 실패! : ".mysqli_connect_error());
    }

    // SET 절을 통해 전달한 데이터로 Reservation 테이블의 레코드를 수정하는 SQL 구문
①  $sql = "UPDATE Reservation
        SET RoomNum = 2002
        WHERE Name = '홍길동'";

    if (mysqli_query($connect, $sql)) {
        echo "레코드 수정 성공!";
    } else {
        echo "레코드 수정 실패! : ".mysqli_error($connection);
    }
    mysqli_close($connection);
?>
```
위 예제의 ①번 라인에서는 Reservation 테이블에 저장된 Name 값이 '홍길동'인 레코드의 RoomNum 값을 2002로 수정하는 SQL 구문을 작성한다

---
### MySQL DELETE
- 레코드 삭제
DELETE문을 사용하면 테이블에 저장된 레코드를 삭제할 수 있다
```SQL
Reservation 테이블에서 Name 필드의 값이 '홍길동'인 레코드만을 삭제하는 PHP 예제

<?php
    $servername = "localhost";
    $user = "choi";
    $password = "0219";
    $dbname = "testDB";

    $connect = mysqli_connect($servername, $user, $password, $dbname);
    if (!$connect) {
        die("서버와의 연결 실패! : ".mysqli_connect_error());
    }

①  $sql = "DELETE FROM Reservation
        WHERE Name = '홍길동'";

    if (mysqli_query($connect, $sql)) {
        echo "레코드 삭제 성공!";
    } else {
        echo "레코드 삭제 실패! : ".mysqli_error($connection);
    }
    mysqli_close($connection);
?>
```
위 예제의 ①번 라인에서는 Reservation 테이블에서 Name필드의 값이 '홍길동'인 레코드만을 찾아 삭제하는 SQL 구문을 작성한다

> 만약 DELETE문에서 WHERE절을 생략하면, 해당 테이블에 저장된 모든 데이터가 삭제될 것이다   
따라서 DELETE문을 사용하여 레코드를 삭제할 때는 언제나 주의를 기울여야 한다

---
### MySQL SELECT
- 레코드 선택
SELECT 문을 사용하면 테이블에 저장된 레코드를 선택할 수 있다
```SQL
Reservation 테이블에 저장된 모든 레코드의 Name필드와 ReserveDate 필드의 값을 선택하여 출력하는 PHP 예제

<?php
    $servername = "localhost";
    $user = "choi";
    $password = "0219";
    $dbname = "testDB";

    $connect = mysqli_connect($servername, $user, $password, $dbname);
    if (!$connect) {
        die("서버와의 연결 실패! : ".mysqli_connect_error());
    }

①  $sql = "SELECT Name, ReserveDate FROM Reservation";
②  $result = mysqli_query($connection, $sql);

③  if (mysqli_stmt_num_rows($result) > 0) {
④      while ($row = mysqli_fetch_assoc($result)) {
⑤          echo $row['Name']."님의 예약일자 : ".$row['ReserveDate']."<br>";
        }
    } else {
        echo "검색된 결과가 없습니다.";
    }
    mysqli_close($connection);
?>
```
①번 라인에서는 Reservation 테이블에 존재하는 모든 레코드의 Name 필드와 ReserveDate 필드의 값을 선택하는 SQL 구문을 작성한다   
이렇게 작성된 SQL 구문은 ②번 라인에서 mysqli_query() 함수를 통해 실행되고, 그 결과 집합은 변수 $result에 저장된다

③번 라인에서는 mysqli_stmt_num_rows() 함수를 사용하여 결과 집합의 총 행(row)의 수를 검사하며, 그 결과가 하나 이상일 때만 while 문을 실행시키고 있다   
④번 라인에서 mysqli_fetch_assoc() 함수는 인수로 전달받은 결과 집합에서 하나의 행(row)을 불러와 연관 배열(associative array)로 반환한다
따라서 ⑤번 라인에서 선택한 필드의 이름을 인덱스로 사용하여 결과를 출력할 수 있게 된다

> 연관 배열(associative array)이란 배열의 인덱스를 정수가 아닌 다양한 타입으로 설정한 배열을 의미한다