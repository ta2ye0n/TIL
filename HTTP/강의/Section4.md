# HTTP
---
## HTTP 메서드
---
### HTTP API를 만들어보자
HTTP API를 만들어보자
```
요구사항
회원 정보 관리 API를 만들어라
- 회원 목록 조회
- 회원 조회
- 회원 등록
- 회원 수정
- 회원 삭제
``` 

- API URI 설계   
(URI/Uniform Resource Identifier)
```
- 회원 목록 조회 /read-member-list
- 회원 조회 /read-member-by-id
- 회원 등록 /create-member
- 회원 수정 /update-member
- 회원 삭제 /delete-member
```
이것이 좋은 URI 설계일까??   
가장 중요한 것은 **리소스 식별**

- API URI 고민
    - 리소스의 의미는 뭘까?
        - 회원을 등록하고 수정하고 조회하는게 리소스가 아니다
        - 예) 미네랄를 캐라 -> 미네랄이 리소스
        - **회원이라는 개념 자체가 바로 리소스다**
    - 리소스를 어떻게 식별하는게 좋을까?
        - 회원을 등록하고 수정하고 조회하는 것을 모두 배제
        - **회원이라는 리소스만 식별하면 된다 -> 회원 리소스를 URI에 매핑**

- API URI 설계   
리소스 식별, URI 계층 구조 활용
```
- 회원 목록 조회 /members
- 회원 조회 /members/{id}
- 회원 등록 /members/{id}
- 회원 수정 /members/{id}
- 회원 삭제 /members/{id}
```
> 참고 : 계층 구조상 상위를 컬렉션으로 보고 복수단어 사용 권장 (member->members)

- 리소스와 행위를 분리   
가장 중요한 것은 리소스를 식별하는 것
    - URI는 리소스만 식별!
    - 리소스와 해당 리소스를 대상으로 하는 행위를 분리
        - 리소스 : 회원
        - 행위 : 조회, 등록, 삭제, 변경
    - 리소느는 명사, 행위는 동사
    - 행위(메서드)는 어떻게 구분?

---
### HTTP 메서드 - GET, POST
HTTP 메서드 종류
- 주요 메서드
    - GET : 리소스 조회
    - POST : 요청 데이터 처리, 주로 등록에 사용
    - PUT : 리소스를 대체, 해당 리소스가 없으면 생성
    - PATCH : 리소스 부분 변경
    - DELETE : 리소스 삭제

- 기타 메서드
    - HEAD : GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
    - OPTIONS : 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명 (주로 CORS에서 사용)
    - CONNECT : 대상 자원으로 식별되는 서버에 대한 터널을 설정
    - TRACE : 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행


GET
- 리소스 조회
- 서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달
- 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않음

리소스 조회1 - 메시지 전달   
![](https://velog.velcdn.com/images/won05121/post/fc5638c6-4130-439a-83be-d051c4de67dc/image.png)

리소스 조회2 - 서버도착   
![](https://velog.velcdn.com/images/won05121/post/a5e0804f-0cfd-4aeb-93c8-203c236b1a13/image.png)   

리소스 조회3 - 응답 데이터   
![](https://velog.velcdn.com/images/won05121/post/c59fb3d8-8885-4a8d-bc33-ebb42beed836/image.png)   

POST
- 요청 데이터 처리
- 메시지 바디를 통해 서버로 요청데이터 전달
- 서버는 요청 데이터를 처리
    - 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다
- 주로 전다로딘 데이터로 신규 리소스 등록, 프로세스 처리에 사용

리소스 등록1 - 메시지 전달   
![](https://velog.velcdn.com/images/won05121/post/9a13b3d8-d499-41e1-9992-b97ffbc053f2/image.png)   

리소스 등록2 - 신규 리소스 생성
![](https://velog.velcdn.com/images/won05121/post/1e011d82-1390-4c15-8c1b-8a7927619db7/image.png)    

리소스 등록3 - 응답 데이터   
![](https://velog.velcdn.com/images/won05121/post/d3e0b80f-2e86-40be-9a7c-b2dc65da5857/image.png)   

요청데이터를 어떻게 처리한다는 뜻일까?
- 스펙 : POST 메서드는 **대상리소스가 리소스의 고유한 의미 체계에 따라 요청에 포함 된 표현을 처리**하도록 요청한다
- 예를 들어 POST는 다음과 같은 기능에 사용된다
    - HTML 양식에 입력된 필드와 같은 데이터 블록을 데이터 처리 프로세스에 제공
        - 예) HTML FORM에 입력한 정보로 회원 가입, 주문 등에서 사용
    - 게시판, 뉴스 그룸, 메일링 리스트, 블로그 또는 유사한 기사 그룹에 메시지 게시
        - 예) 게시판 글쓰기, 댓글 달기
    - 서버가 아직 식별하지 않는 새 리소스 생성
        - 예) 신규 주문 생성
    - 기존 자원에 데이터 추가
        - 예) 한 문서 끝에 내용 추가하기
- 정리 : 이 리소스 URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지 리소스마다 따로 정해야 함 -> 정해진 것이 없다

POST 정리
1. 새 리소스 생성(등록)
- 서버가 아직 식별하지 않은 새 리소스 생성
2. 요청 데이터 처리
- 단순히 데이터를 생성하거나, 변경하는 것을 넘어서 프로세스를 처리해야 하는 경우
- 예) 주문에서 결제완료 -> 배달시작 -> 배달완료처럼 단순히 값 변경을 넘어 프로세스의 상태가 변경되는 경우
- POST의 결과로 새로운 리소르가 생성되지 않을 수도 있음
- 예) POST/orders/{orderId}/start-delivery (컨트롤 URI)
3. 다른 메서드로 처리하기 애매한 경우
- 예) JSON으로 조회 데이터를 넘겨야 하는데, GET 메서드를 사용하기 어려운 경우
- 애매하면 POST
---
### HTTP 메서드 - PUT,PATCH,DELETE
PUT
- **리소스를 대체**
    - 리소스가 있으면 대체
    - 리소스가 없으면 생성
    - 쉽게 이야기해서 덮어버림
- 중요! **클라이언트가 리소스를 식별**
    - 클라이언트가 리소스 위치를 알고 URI 지정
    - POST와 차이점

리소스가 있는 경우   
![](https://velog.velcdn.com/images%2Fgil0127%2Fpost%2F047edc64-0f71-4fad-b700-92d71de78e12%2F22.PNG)   
![](https://velog.velcdn.com/images%2Fgil0127%2Fpost%2F83fc0cd5-b662-45cb-b5f7-316ac33ed660%2F33.PNG)   

리소스가 없는 경우   
![](https://velog.velcdn.com/images%2Fgil0127%2Fpost%2F5b9db58c-43e2-4732-830b-627efada87f7%2F44.PNG)   
![](https://velog.velcdn.com/images%2Fgil0127%2Fpost%2F2180392b-a8ac-4c2d-8f58-f9ef21de8681%2F55.PNG)   
> 클라이언트가 지정한 위치가 존재하는 리소스가 없으면 신규 리소스가 생성된다   

주의!! - 리소스를 완전히 대체한다   
![](https://velog.velcdn.com/images%2Fgil0127%2Fpost%2F0ef95bf0-531e-4d1a-9a26-5b35457e6634%2F66.PNG)   
![](https://velog.velcdn.com/images%2Fgil0127%2Fpost%2Fccaa190a-11c3-447a-b36f-dee51964ebad%2F77.PNG)   

PATCH
- 리소스 부분 변경
> PATCH가 지원이 안되는 HTTP도 있음

리소스 부분 변경   
![](https://velog.velcdn.com/images%2Fgil0127%2Fpost%2F220a4404-0ded-4272-ad92-b49f4358f4c7%2F2.PNG)    
![](https://velog.velcdn.com/images%2Fgil0127%2Fpost%2F187191f4-065b-4ce3-adac-879f26aab779%2F3.PNG)  

DELETE   
- 리소스 제거

리소스 제거   
![](https://velog.velcdn.com/images%2Fgil0127%2Fpost%2Fc821fe4d-167e-4509-ba08-fe2ce96c2ab0%2F222.PNG)   
![](https://velog.velcdn.com/images%2Fgil0127%2Fpost%2Fd5863383-8add-4993-9c26-cf04534c7082%2F333.PNG)   

---
### HTTP 메서드의 속성
```
안전(Safe Methods)
멱등(Idempotent Methods)
캐시가능(Cacheable Methods)
```
언제 어떤 메소드를 사용?   
![](https://velog.velcdn.com/images%2Fgil0127%2Fpost%2F6a62e540-ceb2-49cd-94e5-ad5907fadec8%2F1.PNG)

안전(Safe)
- 호출해도 리소스를 변경하지 않는다
- Q : 그래도 계속 호출해서, 로그 같은게 쌓여서 장애가 발생하면요?
- A : 안전은 해당 리소스만 고려한다 그런 부분까지 고려하지 않는다

멱등(Idempotent)
- f(f(x)) = f(x)
- 한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다
- 멱등 메서드
    - GET : 한번 조회하든, 두 번 조회하든 같은 결과가 조회된다
    - PUT : 결과를 대체한다 따라서 같은 요청을 여러번해도 최종 결과는 같아
    - DELETE : 결과를 삭제한다 같은 요청을 여러번해도 최종 결과는 같다
    > POST : 멱등이 아니다 두번 호출하면 같은 별제가 중복해서 발생할 수 있다
- 활용
    - 자동 복구 메커니즘
    - 서버가 TIMEOUT 등으로 정상 응답을 못주었을때, 클라이언트가 같은 요청을 다시 해도 되는가? 판단 근거
- Q : 재요청 중간에 다른 곳에서 리소스를 변경해버리면?
    - 사용자1 : GET -> username:A, age:20
    - 사용자2 : PUT -> usernameB, age:30
    - 사용자3 : GET -> username:A, age:30 -> 사용자2의 영향으로 바뀐 데이터 조회
- A : 멱등은 외부 요인으로 중간에 리소스가 변경되는 것까지는 고려하지는 않는다


캐시가능(Cacheable)
- 응답 결과 리소스를 캐시해서 사용해도 되는가?
- GET,HEAD,POST,PATCH 캐시가능
- 실제로는 GET,HEAD 정도만 캐시로 사용
    - POST,PATCH는 본문 내용까지 캐시 키로 고려해야 하는데, 구현이 쉽지 않음