# HTTP
---
## HTTP 상태코드
---
### HTTP 상태코드 소개
상태 코드
```
클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능

- 1xx (Informational) : 요청이 수신되어 처리중
- 2xx (Successful) : 요청 정상 처리
- 3xx (Redirection) : 요청을 완료하려면 추가 행동이 필요
- 4xx (Client Error) : 클라이언트 오류, 잘못된 문법 등으로 서버가 요청을 수행할 수 없음
- 5xx (Server Error) : 서버 오류, 서버가 정상 요청을 처리하지 못함
```

만약 모르는 상태 코드가 나타나면?
- 클라이언트가 인식할 수 없는 상태 코드를 서버가 반환하면?
- 클라이언트는 상위 상태코드로 해석해서 처리
- 미래에 새로운 상태 코드가 추가되어도 클라이언트를 변경하지 않아도 됨
- 예) 
    - 299 ??? -> 2xx (Successful)
    - 451 ??? -> 4xx (Client Error)
    - 599 ??? -> 5xx (Server Error)
---
1xx (Informational)
```
요청이 수신되어 처리중
```
- 거의 사용하지 않으므로 생략
---
### 2xx - 성공
2xx (Successful)
```
클라이언트의 요청을 성공적으로 처리

- 200 OK
- 201 Created
- 202 Accepted
- 204 No Content
```

- 200 OK   
요청 성공   
![](https://mblogthumb-phinf.pstatic.net/MjAyMjAzMjVfMjEg/MDAxNjQ4MjA3Mzc5OTgy.nJXKAz82dXhRTOq0eY4MRApB_C59bihV1VUgDvca_igg.uFGf9M2jIxC5no0kZxZtLelCW1liSrpRJj7E-eRJu0sg.PNG.fbfbf1/image.png?type=w800)

- 201 Created   
요청 성공해서 새로운 리소스가 생성됨   
![](https://mblogthumb-phinf.pstatic.net/MjAyMjAzMjVfMTU4/MDAxNjQ4MjA3NDM2NjAw.tIzkwK5pd_Ja9QRXOF-cAUgUoBZmoSwbde0F2cBsmy8g.RwP9e3AizokDabAzzR7qARYhysUz4o_70oxZbh9_WRsg.PNG.fbfbf1/image.png?type=w800)

- 202 Accepted   
요청이 접수되었으나 처리가 완료되지 않았음
    - 배치 처리 같은 곳에서 사용
    - 예) 요청 접수 후 1시간 뒤에 배치 프로세스가 요청을 처리함

- 204 No Content   
서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음
    - 예) 웹 문서 편집기에서 save 버튼
    - save 버튼의 결과로 아무 내용이 없어도 된다
    - save 버튼을 눌러도 같은 화면을 유지해야 한다
    - 결과 내용이 없어도 204 메시지(2xx)만으로 성공을 인식할 수 있다

---
### 3xx - 리다이렉션
3xx (Redirection)
```
요청을 완료하기 위해 유저 에이전트의 추가 조치 필요

- 300 Multiple Choices
- 301 Moved Permanently
- 302 Found
- 303 See Other
- 304 Not Modified
- 307 Temporary Redirect
- 308 Permanent Redirect
```

리다이렉션 이해
```
웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동(리다이렉트)
```
![](https://blog.kakaocdn.net/dn/BJhae/btq9ReBv4Ny/cR9pVvmukuLD6sPKBgNpSK/img.png)
종류
```
- 영구 리다이렉션 - 특정 리소스의 URI가 영구적으로 이동
    - 예) /members -> /users
    - 예) /event -> /new-event
- 일시 리다이렉션 - 일시적인 변경
    - 주문 완료 후 주문 내역 화면으로 이동
    - RPG : Post/Redirect/Get
- 특수 리다이렉션
    - 결과 대신 캐시를 사용
```

- 영구 리다이렉션   
301, 308
    - 리소스의 URI가 영구적으로 이동
    - 원래 URL를 사용 X, 검색 엔진 등에서도 변경인지
    - 301 Moved Permanently
        - 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음 (MAY)   
        ![](https://velog.velcdn.com/images%2Fleemember%2Fpost%2F5096e079-6b49-421d-8b8f-6cb7b0d5b2b9%2Fimage.png)

    - 308 Permanent Redirect
        - 301과 기능은 같음
        - 리다이렉트시 요청 메서드와 본문 유지 (처음 POST를 보내면 리다이렉트도 POST 유지)
        ![](https://velog.velcdn.com/images%2Fleemember%2Fpost%2F516666e4-222d-4f4d-b49b-3a88b893a1c7%2Fimage.png)