# HTTP
---
## HTTP 메서드 활용
---
### 클라이언트에서 서버로 데이터 전송
데이터 전달 방식은 크게 2가지
- 쿼리 파라미터를 통한 데이터 전송
    - GET
    - 주로 정렬 필터(검색어)
- 메시지 바디를 통한 데이터 전송
    - POST, PUT, PATCH
    - 회원 가입, 상품 주문, 리소스 등록, 리소스 변경

4가지 상황
```
1. 정적 데이터 조회
    - 이미지, 정적 텍스트 문서

2. 동적 데이터 조회    
    주로 검색, 게시판 목록에서 정렬 필터(검색어)

3. HTML Form을 통한 데이터 전송
    - 회원 가입, 상품 주문, 데이터 변경

4. HTTP API를 통한 데이터 전송
    - 회원 가입, 상품 주문, 데이터 변경
    - 서버 to 서버, 앱 클라이언트, 웹 클라이언트(Ajax)
```
1. 정적 데이터 조회   
![](https://user-images.githubusercontent.com/72541544/147842181-19dca5f8-a1ff-45a1-a4c8-8c34d83d3682.png)
- 정리
    - 이미지, 정적 텍스트 문서
    - 조회는 GET 사용
    - 정적 데이터는 일반적으로 쿼리 파라미터 없이 리소스 경로로 단순하게 조회 가능

2. 동적 데이터 조회   
![](https://user-images.githubusercontent.com/72541544/147842182-5f500658-a2de-48aa-b917-3c02a7eedc47.png)
- 정리
    - 주로 검색, 게시판 목록에서 정렬 필터(검색어)
    - 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 조건에 주로 사용
    - 조회는 GET 사용
    - GET은 쿼리 파라미터 사용해서 데이터를 전달

3. HTML Form을 통한 데이터 전송    
![](https://user-images.githubusercontent.com/72541544/147842183-71c25d4d-2d95-4582-b526-6f50e71871ea.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FblryAc%2FbtrrUsQrMVY%2FiZpU4Kot8cGWpRQIzsB7LK%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCLvaJ%2FbtrrRfdgzNr%2FM0p1Ag8v6ql7UWk4vXAt1K%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLf93C%2FbtrrTim4tfa%2FjeeLh7RkxlPPK0pLXvkJI1%2Fimg.png)   
- 정리
    - HTML Form submit시 POST전송
        - 예) 회원 가입, 상품 주문, 데이터 변경

    - Content-Type : application/x-www-form-urlencoded 사용
        - form의 내용을 메시지 바디를 통해서 전송(key=value, 쿼리 파라미터 형식)
        - 전송 데이터를 url encoding 처ㅣ
            - 예) abc 김 -> abc%EA%B9%80
    - HTML Form은 GET 전송도 가능
    - Content-Type : mulipart/form-data
        - 파일 업로드 같은 바이너리 데이터 전송시 사용
        - 다른 종류의 여러 파일과 폼의 내용 함께 전송 가능(그래서 이름이 multipart)
> 참고 : HTML Form 전송은 GET, POST만 지원

4. HTTP API를 통한 데이터 전송   
![](https://velog.velcdn.com/images%2Fgil0127%2Fpost%2F45423ef4-61e8-49d4-946d-38f598d483d9%2F1.PNG)
- 정리
    - 서버 to 서버
        - 백엔드 시스템 통신

    - 앱 클라이언트
        - 아이폰, 안드로이드
    - 웹 클라이언트
        - HTML에서 Form 전송 대신 자바 스크립트를 통한 통신에 사용(AJAX)
        - 예) React, VuesJs 같은 웹 클라이언트와 API 통신
    - POST, PUT, PATCH : 메시지 바디를 통해 데이터 전송
    - GET : 조회, 쿼리 파라미터로 데이터 전달
    - Content-Type : application/json을 주로 사용(사실상 표준)
        - TEXT,XML,JSON 등등