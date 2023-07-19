# HTTP
---
## URI와 웹 브라우저 요청 흐름
---
### URI
```
Uniform Resource Identifier
```
- URI? URL? URN?
![](https://velog.velcdn.com/images/0woogie/post/ead1328b-030f-4f9d-8f26-ab890347d389/image.png)
URI는 로케이터(locator),이름(name)또는 둘다 추가로 분류 될 수 있다
> URI(Resource Identifier)가 가장 큰 개념
> URL(Resource Locaotr 리소스 위치) URN (Resource Name 리소스 이름)

- URI 단어 뜻
```
Uniform : 리소스를 식별하는 통일된 방식
Resource : 자원, URI로 식별할 수 있는 모든 것(제한 없음)
Identifier : 다른 항목과 구분하는데 필요한 정보
```
> URL : Uniform Resource Locator
> URN : Uniform Resource Name

- URL, URN 단어 뜻
```
URL - Locator : 리소스가 있는 위치를 지정
URN - Name : 리소스에 이름을 부여
위치는 변할 수 있지만, 이름은 변하지 않는다
URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음
```
---
- **URL 전체 문법**
```
scheme://[userinfo@]host[:port][/path][?query][#fragment]

https://www.google.com:443/search?q=hello&hl=ko
```
    - 프로토콜(https)
    - 호스트명(www.google.com)
    - 패스(/search)
    - 쿼리 파라미터(q=hello&hl=ko)

**1. URL scheme**
``` 
'scheme'://[userinfo@]host[:port][/path][?query][#fragment]

'https'://www.google.com:443/search?q=hello&hl=ko
```
- 주로 프로토콜 사용
- 프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
    - 예) http, https, ftp 등등
- http는 80 포트, https는 443 포트를 주로 사용, 포트는 생략 가능
- https는 http에 보안 추가(HTTP Secure)

**2. URL userinfo**
```
scheme://'[userinfo@]'host[:port][/path][?query][#fragment]

https://www.google.com:443/search?q=hello&hl=ko
```
- URL에 사용자정보를 포함해서 인증
- 거의 사용하지 않음

**3. URL host**
```
scheme://[userinfo@]'host'[:port][/path][?query][#fragment]

https://'www.google.com':443/search?q=hello&hl=ko
```
- 호스트명
- 도메인명 또는 IP 주소를 직접 사용가능

**4. URL PORT**
```
scheme://[userinfo@]host'[:port]'[/path][?query][#fragment]

https://www.google.com:'443'/search?q=hello&hl=ko
```
- 포트(PORT)
- 접속 포트
- 일반적으로 생략, 생략시 http는 80, https는 443

**5. URL path**
```
scheme://[userinfo@]host[:port]'[/path]'[?query][#fragment]

https://www.google.com:443/'search'?q=hello&hl=ko
```
- 리소스 경로(path), 계층적 구조
- 예)
    - /home/file1.jpg
    - /members
    - /members/100, /items/iphone12

**6. URL query**
```
scheme://[userinfo@]host[:port][/path]'[?query]'[#fragment]

https://www.google.com:443/search'?q=hello&hl=ko'
```
- key=value 형태
- ?로 시작, &로 추가 가능 ?keyA=valueA&keyB=valueB
- query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자형태

**7. URL fragment**
```
scheme://[userinfo@]host[:port][/path][?query]'[#fragment]'

http://docs,spring.io/spring-boot/docs/current/reference/html/getting-started.html'#getting-started-introducing-spring-boot'
```
- fragment
- html 내부 북마크 등에 사용
- 서버에 전송하는 정보 아님
---
### 웹 브라우저 요청 흐름

1. DNS를 조회하여 IP 주소 받아오기   
![](https://blog.kakaocdn.net/dn/VIToS/btrEjMa2icB/dvCOsBufYGYa9oTjWb79Fk/img.png)

2. HTTP 요청 메시지   
![](https://www.jaeme.dev/static/a404e86e20efb30f6d769d1460ede5d7/2108e/http_message.png)

3. 해당 메세지를 Soket 라이브러리를 통해 전송계층에 전달
4. 전송계층과 네트워크 계층에서 HTTP 메시지가 포함된 TCP/IP 패킷을 생성하고 네트워크 계층으로 보냄
5. 네트워크 계층은 인터넷을 통해 해당 서버로 요청 메시지 전달   
![](https://www.jaeme.dev/static/974def504cfdb8f515f6fdc1fde04fa7/2e195/tcp_http.png)
![](https://www.jaeme.dev/static/690f4f3414ee1b09251239cf7fb27b0e/d125e/request.png)
     > 전송데이터 = HTTP 메시지

6. 서버에서 요청 패킷을 받고 응답 패킷을 전달   
![](https://www.jaeme.dev/static/886b7c8eb5b2515aeda54342492fe868/e85cb/response_message.png)

7. 웹 브라우저는 응답 패킷을 받아 해석하고 HTML 렌더링을 시킴   
![](https://www.jaeme.dev/static/a8e17ffba40daba90b6c88b8f2b184d5/68de2/response.png)