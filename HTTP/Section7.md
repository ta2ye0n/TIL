# HTTP
---
## HTTP 헤더1 - 일반 헤더
---
### HTTP 헤더 개요
HTTP 헤더
```
header-field = field-name ":" OWS field-value OWS 
(OWS : 띄어쓰기 허용)

field- name은 대소문자 구문 없음
```
- 용도
    - HTTP 전송에 필요한 모든 부가정보
    - 예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 관리 정보...
    - 표준 헤더가 너무 많음
    - 필요시 임의의 헤더 추가 가능
        - helloworld: hihi

- 분류 - RFC2616(과거)   
![](https://3513843782-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-LxjHkZu4T9MzJ5fEMNe%2Fsync%2Fbfd3804a7e832ddf73c7986ce2b69658c4896f8e.png?generation=1617536099261358&alt=media)
    - 헤더 분류
        - General 헤더 : 메시지 전체에 적용되는 정보, 예) Connection: close
        - Request 헤더 : 요청 정보, 예) User-Agent: Mozilla/5.0 (Macintosh; ..)
        - Respones 헤더 : 응답 정보, 예) Server: Apache
        - Entity 헤더 : 엔티티 바디 정보, 예) Content-Type: text/html, Content-Length: 3423

HTTP BODY
- message body - RFC2616(과거)   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F703b2736-8fe6-4cd6-8af8-200754ed916f%2FUntitled.png&blockId=e02a97a0-124b-4aae-a81c-c6a27d8c9c7b)
    - 메시지 본문(message body)은 엔티티 본문(entity body)을 전달하는데 사용
    - 엔티티 본문은 요청이나 응답에서 전달할 실제 데이터
    - 엔티티 헤더는 엔티티 본문의 데이터를 해석할 수 있는 정보 제공
        - 데이터 유형(html, json), 데이터 길이, 압축 정보 등등


**그런데**
```
HTTP 표준
1999년 RFC2616 -> 폐기됨
2014년 RFC7230~7235 등장
```

RFC723x 변화
```
- 엔티티(Entity) -> 표현(Representation)
- Representation = representation Metadata + Representation Data
- 표현 = 표현 메타데이터 + 표현 데이터
```

HTTP BODY
- message body - RFC7230(최신)   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc3b31baa-c5b8-40be-b317-286dd27d3c8a%2FUntitled.png&blockId=fb4c7c57-1f47-4027-a849-131dd8ca043c)   
    - 메시지 본문(message body)을 통해 표현 데이터 전달
    - 메시지 본문 = 페이로드(payload)
    - 표현은 요청이나 응답에서 전달할 실제 데이터
    - 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공
        - 데이터 유형(thml, json), 데이터 길이, 압축 정보 등등
    - 참고: 표현 헤더는 표현 메타데이터와, 페이로드 메시지를 구분해야 하지만, 여기서는 생략

---
### 표현
```
- Content-Type : 표현 데이터의 형식
- Content-Encoding : 표현 데이터의 압축 방식
- Content-Language : 표현 데이터의 자연 언어
- Content-Length : 표현 데이터의 길이

- 표현 헤더는 전송, 응답 둘다 사용
```
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc0fbdc83-b061-40a5-86bf-4df7184db205%2FUntitled.png&blockId=8ca73a3f-e079-4d94-9460-2c06876fe5b1)

Content-Type   
```
표현 데이터의 형식 설명
```
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fabcd2b4a-f779-4a3b-a4c2-935e1bb390e7%2FUntitled.png&blockId=ba10c03c-2825-46f3-a462-bf44663d3d3c)
- 미디어 타입, 문자 인코딩
- 예)
    - text/html; charset-utf-8
    - application/json
    - image/png

Content-Encoding
```
표현 데이터 인코딩
```
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fca2848bb-cf2e-4d9a-adb7-4b5656ac3c72%2FUntitled.png&blockId=1a501a0c-1d9b-4561-9679-d7ef4c0f2b9b)
- 표현 데이터를 압축하기 위해 사용
- 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
- 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
- 예)
    - gzip
    - deflate
    - identity

Content-Language
```
표현 데이터의 자연 언어
```
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fad9247a8-4844-40ec-bf7f-2048792f0a22%2FUntitled.png&blockId=030f6bec-8fe3-4822-aab5-0339fea2e68d)
- 표현 데이터의 자연 언어를 표현
- 예) 
    - ko
    - en
    - en-US

Content-Length
```
표현 데이터의 길이
```
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F59ba7df8-58a4-42b1-942c-eba57a3480a8%2FUntitled.png&blockId=4889090d-a9fa-4580-9e63-2e4757a2e506)
- 바이트 단위
- Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안됨

---
### 콘텐츠 협상
협상(콘텐츠 네고시에이션)
```
클라이언트가 선호하는 표현 요청

- Accept : 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset : 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding : 클라이언트가 선호하는 압축 인코딩
- Accept-Language : 클라이언트가 선호하는 자연 언어

- 협상 헤더는 요청시에만 사용
```
콘텐츠 협상 예시   
Accept-Language 적용전   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fac4d78d3-1fe7-44e6-9769-d269518dec75%2FUntitled.png&blockId=46680af7-271d-48ff-9ab0-cf79c2fc6a1d)    

Accept-Language 적용 후   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3000be69-1582-4364-b80c-6f8ececf76c0%2FUntitled.png&blockId=4c50328b-c30b-470f-b7a5-1af5ae38c5a8)

Accept-Language 복잡한 예시   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F79fd12ff-0f44-458a-84d0-e446c43fa060%2FUntitled.png&blockId=861479a1-77c5-4edb-97fe-486b6f6759c5)
-> 우선순위 사용

협상과 우선순위1   
Quality Values(q)
```
Get/event
Accept-Language: ko-KR;q=0.9,en-US;q=0.8,en;q=0.7
```
- Quality Values(q) 값 사용
- 0~1, 클수록 높은 우선순위
- 생략하면 1
- Accept-Language: ko-KR;q=0.9,en-US;q=0.8,en;q=0.7
    - 1. ko-KR;q=1
    - 2. ko;q=0.9
    - 3. en-US;q=0.8
    - 4. en;q=0.7

Accept-Language 복잡한 예시(우선순위 적용 후)      
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff2afd628-0d04-44d3-8c57-f82b73faedc7%2FUntitled.png&blockId=50e8f414-57d9-4e43-8d20-7efe1f4d2060)

협상과 우선순위2   
Quality Values(q)   
```
GET /event
Accept: text/*, text/plain, text/plain;format=flowed, */*
```
- 구체적인 것이 우선한다
- Accept: text/*, text/plain, text/plain;format=flowed, */*
    - 1. text/plain;format=flowed
    - 2. text/plain
    - 3. text/*
    - 4. */*

협상과 우선순위3   
Quality Values(q)
- 구체적인 것을 기준으로 미디어 타입을 맞춘다
- Accept: text/*;q=0.3, text/html;q=0.7, text/html;level=1, text/html;level=2;q=0.4, \*/\*;q=0.5  

|Media Type|Quality|
|:-----:|:-----:|
|text/html;level=1|1|
|text/html|0.7|
|text/plain|0.3|
|image/jpeg|0.5|
|text/html;level=2|0.4|
|text/html;level=3|0.7|

---
### 전송 방식
```
- Transfer-Encoding
- Range, Content-Range
```
전송 방식 설명
```
- 단순 전송
- 압축 전송
- 분할 전송
- 범위 전송
```

- 단순 전송   
Content-Length
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fda24eae9-c345-45aa-8232-61dbfc4bbf54%2FUntitled.png&blockId=59aa6cbd-29aa-4871-879d-4858a0b0438f)
    - 요청을 하면 응답을 할때 메세지 바디에 대한 Content-Length를 지정하는 것
    - 메세지 바디의 길이를 다 알고있을 때 사용
    - 한번에 요청하고 응답한다

- 압축 전송   
Content-Encoding   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9185d145-e264-4dd8-b473-30930356d393%2FUntitled.png&blockId=52b78fb5-0c79-421c-9445-07d36572aa68)
    - 서버에서 메세지 바디를 gzip같은 바익을 이용해 압축해서 전달하는 방식
    - Content-Encoding이라는 항목을 헤더에 넣어서 어떻게 압축했는지 알려줘야 한다

- 분할 전송   
Transfer-Encoding
![](https://blog.kakaocdn.net/dn/uORgc/btrx7xDQ2v9/jySwfmS0j62SKaiO2fAdM1/img.png)
    - Transfer-Encoding: chunked라고 덩어리로 쪼개서 보낸다는 의미
    - 서버에서 클라이언트로 응답 메세지를 특정 단위로 나눠서 보낸다
    - 용량이 매우 큰 응답을 할 때 분할 전송으로 전송되는대로 표현을 하는 방식이다
    - 이때는 Content-Length를 넣으면 안된다(길이를 예측할 수 없기 때문)

- 범위 전송   
Range, Content-Range   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F50951431-cd63-48e7-a243-74b629bf1efb%2FUntitled.png&blockId=3fa99c17-0208-4e0f-a9b0-d2196a0adadf)
    - 이미지와 같이 용량이 큰 데이터를 받을 때 중간에 전송이 끊겼을 경우 범위를 지정해서 요청하면 매번 끊길때마다 새로 받을 필요없이 특정 범위부터 응답해서 속도를 높힐 수 있다

---
### 일반 정보
```
- Form : 유저 에이전트의 이메일 정보
- Referer : 이전 웹 페이지 주소 
- User-Agent : 유저 에이전트 애플리케이션 정보
- Server : 요청을 처리하는 오리진 서버의 소프트웨어 정보
- Date : 메시지가 생성된 날짜 
```

**From** 
```
유저 에이전트의 이메일 정보
```
- 일반적으로 잘 사용되지 않음
- 검색 엔진 같은 곳에서, 주로 사용
- 요청에서 사용

**Referer**
```
이전 웹 페이지 주소
```
- 현재 요청된 페이지의 이전 웹 페이지 주소
- A -> B로 이동하는 경우 B를 요청할 때 Referer: A 를 포함해서 요청
- Referer를 사용해서 유입 경로 분석 가능
- 요청에서 사용
> 참고 : referer는 단어 referrer의 오타

**User-Agent**
```
유저 에이전트 애플리케이션 정보
```
- user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppkeWebkit/537.36(KHTML, like Gecko) Chrome/86.04240.183 Safari/537.36
- 클라이언트의 애플리케이션 정보(웹 브라우저 정보, 등등)
- 통계 정보
- 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
- 요청에서 사용

**Server**
```
요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
```
- Server: Apache/2.2.22 (Debian)
- server: nginx
- 응답에서 사용

**Date**
```
메시지가 발생한 날짜와 시간
```
- Date: Tue, 15 Nov 1994 08: 12:31 GMT
- 응답에서 사용
---
### 특별한 정보
```
- Host : 요청한 호스트 정보(도메인)
- Location : 페이지 리다이렉션
- Allow : 허용 가능한 HTTP 메서드
- Retry-After : 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
```

**Host**
```
요청한 호스트 정보(도메인)
```
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Feb97f5a8-e634-44f5-a1fe-62e6a19479ed%2FUntitled.png&blockId=4fbad671-ec32-4b16-92d6-4f641e9952f2)
- 요청에서 사용
- 필수
- 하나의 서버가 여러 도메인을 처리해야 할 때
- 하나의 IP 주소에 여러 도메인이 적용되어 있을 때

HOST가 없을 경우 생기는 문제   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F086bc3e5-dcb6-413c-bed3-c24836373266%2FUntitled.png&blockId=1085303a-d9a9-4c2b-86bd-718fb68707b3)

![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fddb977be-f31e-410c-b981-a6c61f19f100%2FUntitled.png&blockId=cf869237-56ea-4019-a937-4c0c1a370b67)
- 해당 요청은 서버에서 어떤 도메인으로 들어가야 할지 알수가 없어 문제가 된다   
-> HOST를 추가하여 해결   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fbec742af-8503-47d5-97b4-76e7509a7fe3%2FUntitled.png&blockId=56f4a31e-fd6c-4448-a8bc-e64cd6b9a07a)
- 헤더 정보에 HOST를 추가함으로써 서버에서 어느 도메인으로 들어가야할지 알 수 있다

**Location**
```
페이지 리다이렉션
```
- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동 (리다이렉트)
- 응답코드 3xx 에서 설명
- 201 (Created) : Location 값은 요청에 의해 생성된 리소스 URI
- 3xx (Redirection) : Location 값은 요청을 자동으로 리디렉션하기 위한 대상 리소스를 가리킴

**Allow**
```
허용 가능한 HTTP 메서드
```
- 405 (Method Not Alloewed) 에서 응답에 포함해야함
- Allow : GET, HEAD, PUT

**Retry-After**
```
유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
```
- 503 (Service Unavaliable) : 서비스가 언제까지 불능인지 알려줄 수 있음
- Retry-After : Fri, 31 Dec 1999 23:59:59 GMT (날짜 표기)
- Retry-After: 120 (초단위 표기)
---
### 인증
```
- Authorization : 클라이언트 인증 정보를 서버에 전달
- WWW-Authenticate : 리소스 접근시 필요한 인증 방법 정의
```
**Authorization**
```
클라이언트 인증 정보를 서버에 전달
```
- Authorization : Basic xxxxxxxxxxxxxxxx

**WWW-Authenticate**
```
리소스 접근시 필요한 인증 방법 정의
```
- 리소스 접근시 필요한 인증 방법 정의
- 401 Unauthorized 응답과 함께 사용
- WWW-Authenticate: Newauth realm= "apps", type=1,title="Login to /"apps/"",Basic realm="simple"
---