# HTTP
---
## 인터넷 네트워크
---
### IP
IP(인터넷 프로토콜)
- 지정한 IP 주소(IP Address)에 데이터 전달
- 패킷(Packet)이라는 통신 단위로 데이터 전달

IP 프로토콜의 한계
- 비연결성
    - 패킷을 받을 대산이 없거나 서비스 불능 상태여도 패킷 전송
- 비신뢰성
    - 중간에 패킷이 사라지면?
    - 패킷이 순서대로 안오면?
- 프로그램 구분
    - 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면?

대상이 서비스 불능, 패킷 전송   
![](https://velog.velcdn.com/images/seong_li/post/f4e6170b-f02b-4ffc-9c6e-de9975e301ed/image.png)

패킷소실   
![](https://velog.velcdn.com/images%2Fsyleemk%2Fpost%2Fbd039541-4a54-4ec9-aeec-46a55c19b34e%2Fimage.png)

패킷 전달 순서 문제 발생   
![](https://velog.velcdn.com/images%2Fsyleemk%2Fpost%2F565320fa-bc8c-49a1-a54f-c2981fa34705%2Fimage.png)

---
### TCP/UDP

인터넷 프로토콜 스택의 4계층
- 애플리케이션계층 - HTTP,FTP
- 전송 계층 - TCP,UDP
- 인터넷 계층 - IP
- 네트워크 인터페이스 계층

프로토콜 계층   
![](https://velog.velcdn.com/images%2Fwnsqud70%2Fpost%2F303e940c-a0f9-403c-b048-afa4e546f315%2F2.JPG)

IP 패킷 정보   
![](https://www.jaeme.dev/static/f2b6cc249665fdcbe38d7da221408591/37523/packet.png)

TCP/IP 패킷 정보   
![](https://mblogthumb-phinf.pstatic.net/MjAyMTEwMDZfMTIw/MDAxNjMzNTIzODA5MjAx.lr7ehZ2xdceOZfdLtfPvFlEVfgDcufPLU_0DJ0_oVE0g.qFY5feSoPoejRriF36AGwkf2m3dYZAWPSau_tJGbIs4g.PNG.sosow0212/image.png?type=w800)

TCP 
```
전송 제어 프로토콜 (Transmission Control Protocol)
```
특징   
- 연결지향 - TCP 3 way handshake (가상연결)
- 데이터 전달 보증
- 순서보장
- 신뢰할 수 있는 프로토콜
- 현재는 대부분 TCP 사용

TCP 3 way handshake   
![](https://velog.velcdn.com/images%2Fyujuck%2Fpost%2F26305cd8-1a13-4f53-a5e0-7d10035a3977%2F2-4.png)

데이터 전달 보증   
![](https://velog.velcdn.com/images%2Focto__%2Fpost%2F0e1cfeba-854a-4aaa-9a0e-3d2904c8f4f5%2FScreen%20Shot%202022-03-09%20at%2011.58.51%20AM.png)

순서 보장   
![](https://velog.velcdn.com/images%2Focto__%2Fpost%2F81405f33-7611-42fc-8379-42e4a6dc34b5%2FScreen%20Shot%202022-03-09%20at%2011.59.16%20AM.png)

UDP
```
사용자 데이터그램 프로토콜(User Datagram Protocol)
```
특징
- 하얀 도화지에 비유(기능이 거의 없음)
- 연결지향 - TCP 3 way handshake X
- 데이터 전달 보증 X
- 순서 보장 X
- 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
- 정리
    - IP와 거의 같음 + PORT + 체크섬 정도만 추가
    - 애플리케이션에서 추가 작업 필요
---
### PORT
```
같은 IP 내에서 프로세스 구분
```

- 0 ~ 65535 할당 가능
- 0 ~ 1023 : 잘 알려진 포트, 사용하지 않는 것이 좋음
    - FTP - 20, 21
    - TELNET - 23
    - HTTP - 80
    - HTTPS - 443
---
### DNS
```
도메인 네임 시스템(Domain Name System)
```
- 전화번호부
- 도메인 명을 IP 주소로 변환

- DNS 사용   
![](https://mblogthumb-phinf.pstatic.net/MjAyMjA2MjFfMTkg/MDAxNjU1Nzg1NzQwNTYx.LurwcfstEUxRHsLcU53sFaOwWLkE1fxnmUvj28S3uZYg.5ohcOc5wX3yqfkNqMejouyz_E1rzyD9e-vX8PyIvqm8g.PNG.whitesunny65/image.png?type=w800)

> IP는 기억하기 어렵고 변경될수 있기 때문에 사용