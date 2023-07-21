# HTTP
---
## HTTP 기본
---
### 모든 것이 HTTP
```
HTTP
(HyperText Transter Protocol)
```

- HTTP 메시지에 모든 것을 전송
    - HTML, TEXT
    - IMAGE, 음성, 영상, 파일
    - JSON, XML (API)
    - 거의 모든 형태의 데이터 전송가능
    - 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용

- HTTP 역사
    - HTTP/0.9 1991년 : GET 메서드만 지원, HTTP 헤더 X
    - HTTP/1.0 1996년 : 메서드, 헤더 추가
    - HTTP/1.1 1991년 : 가장 많이 사용, 우리에게 가장 중요한 버전
        - RFC2068(1997) -> RFC2616(1999) -> RFC7230~7235(2014)
    - HTTP/2 2015년 : 성능 개선
    - HTTP3 진행중 : TCP 대신에 UDP 사용, 성능 개선

- 기반 프로토콜
    - TCP : HTTP/1.1, HTTP/2
    - UDP : HTTP/3
    - 현재 HTTP/1.1 주로 사용
        - HTTP/2, HTTP/3 도 점점 증가

- HTTP 특징
    - 클라이언트 서버 구조
    - 무상태 프로토콜(스테이스리스), 비연결성
    - HTTP 메시지
    - 단순함, 확장 가능