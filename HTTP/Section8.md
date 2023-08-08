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

캐시가 없을때
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

캐시 적용
```
- 캐시 덕분에 캐시 기능 시간동안 네트워크를 사용하지 않아도 된다
- 비싼 네트워크 사용량을 줄일 수 있다
- 브라우저 로딩 속도가 매우 빠르다
- 빠른 사용자 경험
```

캐시 시간 초과
```
- 캐시 유효 시간이 초과하면, 서버를 통해 데이터를 다시 조회하고, 캐시를 갱신한다
- 이때 다시 네트워크 다운로드가 발생한다
```
---