# HTTP
---
## HTTP 헤더2 - 캐시와 조건부 요청
---
### 캐시 기본 동작
캐시가 없을 때 첫 번째 요청   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F54add6bf-b83a-4c03-bc73-e02e94d4c353%2FUntitled.png&blockId=fa9722e0-ccaa-472b-bf9d-ca7c5ff81979)
- 클라이언트에서 star,jpg 이미지를 요청
- 서버에서는 해당 이미지가 있으면 응답을 주는데, 이미지의 HTTP 헤더 + 바디를 합쳐 대략 1.1M정도 용량의 데이터를 응답한다
- 클라이언트는 해당 이미지를응답 받아 사용한다

캐시가 없을 때 두 번째 요청   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F35eadec5-a161-453f-b8e0-be7ad9785974%2FUntitled.png&blockId=23301500-7ff2-4090-b989-df0323153bed)
- 클라이언트에서는 star.jpg 이미지를 다시 한 번 요청한다
- 서버에서는 동일한 이미지를 다시 1.1M 정도 용량의 데이터를 응답해준다
- 클라이언트에서는 해당 이미지를 응답 받아 사용한다

**캐시가 없을때**
```
- 데이터가 변경되지 않아도 계속 네트워크를 통해서 데이터를 다운로드 받아야 한다
- 인터넷 네트워크는 매우 느리고 비싸다
- 브라우저 로딩 속도가 느리다
- 느린 사용자 경험
```

캐시 적용 첫 번째 요청   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F7532f219-bd97-4508-ac11-6c39504ad4ed%2FUntitled.png&blockId=32f296b6-46e7-4e4d-b9e0-cebce887a410)
- 헤더에 `cache-controll`속성을 넣어주어 캐시가 유효한 시간을 넣어준다
- 그럼 부라우저 캐시에 응답 결과를 저장한다
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fe196d2fe-42e4-4851-970d-ddd67925d6fc%2FUntitled.png&blockId=085dd324-4116-4ff4-b584-c95979766a94)

캐시 적용 두 번째 요청   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F68c9cb24-a786-49c9-9e95-294c22f255b9%2FUntitled.png&blockId=91dfa34d-15ba-44be-9048-a7d68a902c5c)
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F243e5457-533e-4849-b591-299805f21e01%2FUntitled.png&blockId=11d99ea6-0606-442a-bf29-3d3baf0ed1b3)
- 두 번째 요청할때는 우선 캐시를 조회한다
- 캐시가 존재하고 유효시간 이내이기에 유효한 캐시가 있어서 해당 캐시에서 자료를 가져온다

**캐시 적용**
```
- 캐시 덕분에 캐시 기능 시간동안 네트워크를 사용하지 않아도 된다
- 비싼 네트워크 사용량을 줄일 수 있다
- 브라우저 로딩 속도가 매우 빠르다
- 빠른 사용자 경험
```

**캐시 시간 초과**
```
- 캐시 유효 시간이 초과하면, 서버를 통해 데이터를 다시 조회하고, 캐시를 갱신한다
- 이때 다시 네트워크 다운로드가 발생한다
```
---
### 검증 헤더와 조건부 요청1
- 캐시 유효 시간이 초과해서 서버에 요청하면 다음 두 가지 상황이 나타난다
    - 1. 서버에서 기존 데이터를 변경함
    - 2. 서버에서 기존 데이터를 변경하지 않음

**캐시 시간 초과**
- 캐시 만료후에도 서버에서 데이터를 변경하지 않음
- 생각해보면 데이터를 전송하는 대신에 저장해 두었던 캐시를 재사용 할 수 있다
- 단 클라이언트의 데이터와 서버의 데이터가 같다는 사실을 확인할 수 있는 방법 필요
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd8498124-4724-4f08-ac07-0a4cfd5eea31%2FUntitled.png&blockId=77067441-b726-4345-8b04-c36b6006bcd8)

검증 헤더 추가 첫 번째 요청   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F41696473-3bf4-4c4f-a8da-17add5a48fbe%2FUntitled.png&blockId=109af28b-3bbc-4797-b819-ffeae8ffe35b)
- 데이터가 마지막으로 수정된 시간 정보를 헤더에 작성해준다
    - UTC 표기법으로 적어준다
- 응답 결과를 캐시에 저장할 때 데이터 최종 수정일도 저장된다
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fafc8e8b5-1170-4b23-adab-c9edffd5d5df%2FUntitled.png&blockId=061100a4-9e43-4abc-ba9b-4dca33920343)

검증 헤더 추가 두 번째 요청(캐시 시간 초과)   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fbdaf3290-ecf2-4aeb-9f99-3aee84983e63%2FUntitled.png&blockId=ee8da055-8a37-450d-a831-d88f73993570)
- 캐시 시간이 초과해서 다시 요청을 해야하는데, 캐시에 최종 수정일 정보(Last-Modified)가 있다면 요청 헤더에 if-modified-since에 해당 날짜를 담아서 서버에 보낸다
- 서버의 해당 자료의 최종 수정일과 비교해서 데이터가 수정이 안되었을 경우 응답 메세지에 이를 담아서 알려준다
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F340e7891-226f-4943-9506-579966b2a7af%2FUntitled.png&blockId=bf02147d-2808-4932-b536-ecb584df9c03)
    - HTTP Body는 응답 데이터에 없다
    - 상태코드는 304 Not Modified로 변경된것이 없다는 것을 알린다
    - 그래서 전송 데이터는 바디가 빠졌기에 헤더만 포함된 0.1M만 전송된다
    - 클라이언트에서는 해당 응답을 받은 뒤 캐시를 갱신해주고 다시 일정시간(60초) 유효하게 된다

**정리**
- 캐시 유효 시간이 초과해도, 서버의 데이터가 갱신되지 않으면
- 304 Not Modified + 헤더 메타 정보만 응답(바디X)
- 클라이언트는 서버가 보낸 응답 헤더 정보로 캐시의 메타 정보를 갱신
- 클라이언트는 캐시에 저장되어 있는 데이터 재활용
- 결과적으로 네트워크 다운로드가 발생하지만 용량이 적은 헤더 정보만 다운로드
- 매우 실용적인 해결책
---
### 검증 헤더와 조건부 요청2
**검증 헤더와 조건부 요청**
- 검증 헤더
    - 캐시 데이터와 서버 데이터가 같은지 검증하는 데이터
    - Last-Modified, ETag
- 조건부 요청 헤더
    - 검증 헤더로 조건에 따른 분기
    - If-Modified-Since : Last-Modified 사용
    - If-None-Match : ETag 사용
    - 조건이 만족하면 200 OK
    - 조건이 만족하지 않으면 304 Not Modified

**예시**
- If-Modified-Since : 이후에 데이터가 수정되었으면?
    - 데이터 미변경 예시
        - 캐시 : 2020년 11월 10일 10:00:00 vs 서버 : 2020년 11월 10일 10:00:00
        - 304 Not Modified, 헤더 데이터만 전송(BODY 미포함)
        - 전송 용량 0.1M (헤더 0.1M)
    - 데이터 변경 예시
        - 캐시 : 2020년 11월 10일 10:00:00 vs 서버 : 2020년 11월 10일 11:00:00
        - 200 OK, 모든 데이터 전송(BODY 포함)
        - 전송 용량 1.1M(헤더 0.1M, 바디 1.0M)

**Last-Modified, If-Modified-Since 단점**
- 1초 미만(0.x초) 단위로 캐시 조정이 불가능
- 날짜 기반의 로직 사용
- 데이터를 수정해서 날짜가 다르지만, 같은 데이터를 수정해서 데이터 결과가 똑같은 경우
- 서버에서 별도의 캐시 로직을 관리하고 싶은 경우
    - 예) 스페이스나 주석처럼 크게 영향이 없는 변경에서 캐시를 유지하고 싶은 경우

**ETag, If-None-Match**
```
서버에서 완전히 캐시를 컨트롤하고 싶은 경우 ETag를 사용하면 된다
```
- ETag(Entity Tag)
- 캐시용 데이터에 임의의 고유한 버전 이름을 달아둠
    - 예) `ETag : "v1.0"`, `ETag : "a2jiodwjekjl3"`
- 데이터가 변경되면 이 이름을 바꾸어서 변경함(Hash를 다시 생성)
    - 예) `ETag: "aaaaa"` -> `Etag: "bbbbb"`
- 진짜 단순하게 ETag만 보내서 같으면 유지, 다르면 다시 받기!

ETag를 사용한 첫 번째 요청   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F1cdb55fd-c359-4ea6-924e-ce1b98776be4%2FUntitled.png&blockId=022fdc01-78f6-460e-b98d-1585fea33c46)
- 헤더에 ETag를 작성해서 응답해준다
- 클라이언트의 캐시에선 ETag 값을 저장한다
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F51c2a471-2a6a-44bf-a121-e3a6eb7c17d6%2FUntitled.png&blockId=c472bcdf-5eaa-4bfb-bcce-2983cbde2dd7)

ETag를 사용한 두 번째 요청(캐시 시간 초과)    
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F81b89694-14fe-4a0b-a3b8-c33e12606011%2FUntitled.png&blockId=9eece16f-7bbf-4a54-929f-74835b0cac3b)
- 캐시시간이 초과되서 다시 요청을 해야하는 경우이다
- 이때`If-None-Match`를 요청 헤더에 작성해서 보낸다

![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fcb0db35f-5015-4d2a-8ff6-18142cc584e0%2FUntitled.png&blockId=7a1ba204-9c53-41c4-8553-b87b138da5d7)
- 서버에서 데이터가 변경되지 않았을 경우 ETag는 동일하다 그래서 `If-None-Match`는 실패다
- 이 경우 서버에서는 `304 Not Modified`를 응답하며 이때 역시 `HTTP Body`는 없다
- 브라우저 캐시에서는 응답 결과를 재사용하고 헤더 데이터를 갱신한다
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ffd69b9bd-f789-4358-b44a-9df7744a204b%2FUntitled.png&blockId=15a652d9-0ed5-4dcb-b461-05ecfc2c8b0f)

**ETag, If-None-Match 정리**
- 진짜 단순하게 ETag만 서버에 보내서 같으면 유지, 다르면 다시 받기!
- **캐시 제어 로직을 서버에서 완전히 관리**
- 클라이언트는 단순히 이 값을 서버에 제공(클라이언트는 캐시 메커니즘을 모름)
- 예)
    - 서버는 배타 오픈 기간인 3일 동안 파일이 변경되어도 ETag를 동일하게 유지
    - 애플리케이션 배포 주기에 맞추어 ETag 모두 갱신

>검증 헤더와 조건부 요청 헤더
>```
>- 검증 헤더 (Validator)
>    - ETag : "v1.0", ETag : "asid93jkrh2l"
>    - Last-Modified : Thu, 04 Jun 2020 07:19:24 GMT
>-  조건부 요청 헤더
>    - If-Match, If-None-Match : ETag 값 사용
>    - If-Modified-Since, If-Unmodified-Since : Last-Modified 값 사용
>```
---
### 캐시와 조건부 요청 헤더
캐시 제어 헤더
```
- Cache-Control : 캐시 제어
- Pragma : 캐시 제어(하위 호한)
- Expires : 캐시 유효 기간(하위 호환)
```

**Cache-Control**
```
캐시 지시어(directives)
```
- Cache-Control : max-age
    - 캐시 유효 시간, 초 단위
- Cache-Control : no-cache
    - 데이터는 캐시해도 되지만, 항상 원(origin) 서버에 검증하고 사용
- Cache-Control : no-store
    - 데이터에 민감한 정보가 있으므로 저장하면 안됨
    (메모리에서 사용하고 최대한 빨리 삭제)

**Pragma**
```
캐시 제어(하위 호환)
```
- Pragma : no-cache
- HTTP 1.0 하위 호환

**Expires**
```
캐시 만료일 지정(하위 호환)
```
- expires : Mon, 01 Jan 1990 00:00:00 GMT

- 캐시 만료일을 정확한 날짜로 지정
- HTTP 1.0 부터 사용
- 지금은 더 유연한 Cache-Control: max-age 권장
- Cache-Control: max-age와 함께 사용하면 Expires는 무시
---
### 프록시 캐시
원 서버 직접 접근(origin 서버)   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F4aeeb09a-0524-47d3-8952-db4993de5171%2FUntitled.png&blockId=1e32a46b-db1b-4925-a65a-1abd976ca888)

프록시 캐시 도입 - 첫 번째 요청   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F0bff9c23-e093-4622-ac73-285d2525e3f0%2FUntitled.png&blockId=683924e1-14ec-4e30-bd01-034ad2c42dc3)
- 한국에 프록시 캐시서버를 두고 한국의 클라이언트는 프록시 캐시 서버를 통해 자료를 가져오도록 한다
- 여러 사람이 찾은 자료일수록 이미 캐시에 등록되어있기에 빠른 속도로 자료를 가져올 수 있다
    - 같은 국내에 있기에 원서버에 접근하는 것보다 훨씬 빠른 속도 자료를 가져올 수 있다
    - 예) 유튜브에서 고용량의 영상도 빨리 볼 수 있는 이유
- 클라이언트에서 사용되고 저장되는 캐시를 `private캐시`라 하고 프록시 캐시서버의 캐시를 `public 캐시`라 한다

**Cache-Control**
```
캐시 지시어(directives) - 기타
```
- Cache-Contro : public
    - 응답이 public 캐시에 저장되어도 됨
- Cache-Control : private
    - 응답이 해당 사용자만을 위한 것임, private 캐시에 저장해야 함(기본값)
- Cache-Control : s-maxage
    - 프록시 캐시에만 적용되는 max-age
- Age: 60 (HTTP 헤더)
    - 오리진 서버에서 응답 후 프록시 캐시 내에 머문 시간(초)
---
### 캐시 무효화
Cache-Control
```
확실한 캐시 무효화 응답
```
- Cache-Control: no-cache, no-store, numst-revalidate
- Pragema: no-cache
    - HTTP 1.0 하위 호환

**Cache-Control**
```
캐시 지시어(directives) - 확실한 캐시 무효화
```
- Cache-Contro: no-cache
    - 데이터는 캐시해도 되지만, 항상 원 서버에 검증하고 사용(이름에 주의!)
- Cache-Control: no-store
    - 데이터에 민감한 정보가 있으므로 저장하면 안됨(메모리에서 사용하고 최대한 빨리 삭제)
- Cache-Control: must-revalidate
    - 캐시 만료후 최초 조회시 원 서버에 검증해야함
    - 원 서버 접근 실패시 반드시 오류가 발생해야함 - 504(Gateway Timeout)
    - must-revalidate는 캐시 유효 시간이라면 캐시를 사용함
- Pragma: no-cache
    - HTTP 1.0 하위 호환

**no-cache vs must-revalidate**   
no-cache 기본 동작
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F01525460-7f40-4004-be8f-ee4e75a1c082%2FUntitled.png&blockId=da245c9d-7d29-4409-adfd-62cd6df5d267)
- 캐시 서버 요청을 하면 프록시 캐시 서버에 도착하면 no-cache인 경우 원 서버에 요청을 하게된다.그리고 원 서버에서 검증 후 응답을하게 된다
- 하지만, 어떤한 이유라도 프록시 캐시 서버와 원 서버간 네트워크 연결이 단절되어 접근이 불가능 하다면, no-cache에서는 응답으로 오류가 아닌 오래된 데이터라도 보여주자라는 개념으로 200OK으로 응답을 한다   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F48151293-63ed-48fc-bc77-1dfa5a530cd8%2FUntitled.png&blockId=261b634b-f853-495e-83ba-d7bb43c215b8)

must-revalidate   
![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fdaae5f9c-0898-4707-bd60-a84dcfeaffcb%2FUntitled.png&blockId=abd4d418-3157-494f-aed2-3066e4ad3d21)
- 캐시 서버요청을 해 프록시 캐시 서버로 갔을때 캐시 서버와 원 서버간의 연결이 단절되어 접근이 불가능하다면 must-revalidate에서는 원 서버에 접근이 불가능한 경우 항상 오류가 발생해야 한다(504 Gateway Timeout)

> 확실한 캐시 무효화 응답으로 작성한 헤더를 사용하게 되면 no-cache로 무조건 원 서버에서 검증을 하게하고 must-revalidate로 원 서버와 검증이 안되면 오류가 발생하도록 한다 그리고 Pragma를 사용해서 혹시모를 1.0 이하 버전의 하위호환도 적용해준다