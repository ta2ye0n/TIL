# Annotation
---
## websocket
웹소켓은 웹 어플리케이션을 위한 `양방향 통신기법`이다   
웹소켓 프로토콜은 웹 브라우저와 웹 서버간의 통신을 허용한다   
HTTP 통신과 차별화된 가장 큰차이점은 `HTTP는 클라이언트가 서버에 요청하는 것`이지만,
WebSocket은 `서버와 클라이언트 간에 양방향 대화(요청)`가 가능하는 것이다

WebSocket으로 연결이 유지되면 메세지를 이동할 수 있으며, 이렇게 `이중 통신을 사용`하여 웹소켓이 `TCP에서 메세지를 스트리밍` 할 수 있다

---
### @Endpoint
```
해당 api를 호출할때의 url이라고 이해하면 된다

해당 api를 호출 하였을때 해당 어떤 로직이 실행되는지 그 위치를 의미하는 url이 endpoint라고 한다
```
> and endpoint is simply one of a communication channel (stackoverflow) ->
커뮤니케이션 채널의 한 쪽 끝

API와 Endpoint의 차이
- API - 두 시스템(어플리케이션이)이 상호작용할 수 있게 하는 프로토콜의 총집합
- ENDPOINT는 API가 서버에서 리소스에 접근할 수 있도록 가능하게 하는 URL

---
### @EnableWebSocket
websocket을 `활성화`한다
구성 클래스에 `웹소켓의 기능을 활용`할 수 있게 해준다

---
### @OnOpen
```
클라이언트가 접속할 때마다 실행된다
```
---
### @OnMessage
```
메세지 수신 시 실행된다
```
---
### @OnClose
```
클라이언트가 접속을 종료할 시 실행된다
```
---
### @SendTo/@SendToUser
- @SendTo   
`1 : n으로 메세지를 뿌릴때 사용`하는 구조이다  
보통 경로가 `/topic`으로 시작한다

- @SendToUser
`1 : 1으로 메세지를 보낼때 사용`하는 구조이다   
보통 경로가 `/queue`로 시작한다

---