# JWT
---
## JWT - Json Web Token
```
인증에 필요한 정보들을 암호화시킨 JSON 토큰
```

주로 사용자의 `인증(authentication)`또는 `인가(authorization)정보`를 서버와 클라이언트간에 안전하게 주고 받기 위해서 사용된다

JWT 토큰 웹에서 보통 `Authorization` HTTP 헤더를 `Bearer <토큰>`의 형태로 설정하여 클라이언트에서 서버로 전송되며, 서버에서는 토큰에 포함되어 있는 서명(signature) 정보를 통해서 위변조 여부를 빠르게 검증할 수 있게 된다

> JSON - Key, Value 가 한 쌍을 이루는 객체
---
### JWT 구조
하나의 JWT 토큰은 `헤더(header)`와 `페이로드(payload)`,`서명(signature)` 이렇게 세부분으로 이루어지며 각 구역이 `.` 기호로 구분된다
```
<헤더>.<페이로드>.<서명>
```
첫 번째 부분인 헤더(header)에는 `토큰의 유형과 서명 알고리즘에 명시`되고, 중간 부분인 페이로드(payload)에는 소위 claim 이라고도 불리는 `인증/인가 정보`가 담긴다
마지막 부분인 서명(signature)에는 `헤더와 페이로드가 비밀키로 서명되어 저장`된다

JWT 토큰은 네트워크로 전송되야하기 때문에 공간을 적게 차지하는 것이 유리하다
그래서 JSON 형식으로 데이터를 저장할 때 `키(key)를 3글자로 줄이는 관행`이 있다

>전형적인 JWT 토큰의 디코딩 결과
>```javascript
>헤더
>{
>    "alg" : "HS256",
>    "typ" : "JWT"
>}
>
>페이로드
>{
>  "sub": "1234567890",
>  "lat": 1516239022
>}
>```

JWT에서 자주 사용되는 JSON 키 이름
- `sub` 키 : 인증 주체(subject)
- `iss` 키 : 토큰 발급처
- `typ` 키 : 토큰의 유형 (type)
- `alg` 키 : 서명 알고리즘 (algorithm)
- `iat` 키 : 발급 시각(issued at)
- `exp` 키 : 만료 시작(expiration time)
- `aud` 키 : 클라이언트(audience)

---
### Token 인증 방식
![](https://blog.kakaocdn.net/dn/ogoAg/btqAriyT5sY/YYt2wkEz50kKN47mLwRDXK/img.png)
1. 사용자가 아이디와 비밀번호로 로그인을 한다

2. 서버 측에서 사용자(클라이언트)에게 **유일한 토큰**을 발급한다
3. 클라이언트는 서버 측에서 전달받은 토큰을 쿠키나 스토리지에 저장해 두고, 서버에 요청을 할 때마다 해당 토큰을 HTTP 요청 헤더에 포함시켜 전달한다
4. 서버는 전달받은 토큰을 검증하고 요청에 응답한다   
토큰에는 요청한 사람의 정보가 담겨있기에 서버는 DB를 조회하지 않고 누가 요청하는지 알 수 있다

> 토큰 인증이 신뢰성을 가지는 이유
>```
>유저 JWT :A(Header) + B(PayLoad) + C(Signature)일 때 (만일 임의의 유저가 B를 수정했다고 하면 B'로 표시)
>```
>1. 다른 유저가 B를 임의로 수정 -> 유저 JWT: A + B' + C
>2. 수정한 토큰을 서버에 요청을 보내면 서버는 유효성 검사 시행   
    유저 JWT: A + B' + C   
    서버에서 검증 후 생성한 JWT: A + B' + C' => (signature) 불일치
> 3. 대조 결과가 일치하지 않아 유저의 정보가 임의로 조작되었음을 알 수 있다.
>
> 정리 
>```
> 서버는 토큰안에 들어있는 정보가 무엇인지 아는게 중요하는 것이 아니라 해당 토큰이 유요한 토큰인지 확인하는 것이 중요하기 때문에, 클라이언트로부터 받은 JWT의 헤더, 페이로드를 서버의 key값을 이용해 시그니처를 다시 만들고 이를 비교하여 일치했을 경우 인증을 통과시킨다
>```

---
### JWT를 이용한 인증 과정
![](https://velog.velcdn.com/images/gimminjae/post/c2ed0742-909b-4cbd-a9ef-0acc69831a03/image.png)

1. 사용자가 ID, PW를 입력하여 서버에 로그인 인증을 요청한다
2. 서버에서 클라이언트로부터 인증 요청을 받으면, `Header, PayLoad, Signture`를 정의한다   
Header, PayLoad, Signature를 각각 BAse64로 한 번 더 암호화하여 JWT를 생성하고 이를 쿠키에 담아 클라이언트에게 발급한다

3. 클라이언트는 서버로부터 받은 JWT를 로컬 스토리지에 저장한다. (쿠키나 다른 곳에 저장할 수도 있음)
API를 서버에 요청할때 `Authorization header에 Access Token`을 담아서 보낸다
4. 서버가 할 일은 클라이언트가 Header에 담아서 보낸 JWT가 내 서버에서 발행한 토큰인지 일치 여부를 확인하여 일치한다면 인증을 통과시켜주고 아니라면 통과시키지 않으면 된다.
인증이 통과되었으므로 페이로드에 들어있는 유저의 정보들을 select해서 클라이언트에 돌려준다.
5. 클라이언트가 서버에 요청을 했는데, 만일 액세스 토큰의 시간이 만료되면 클라이언트는 리프래시 토큰을 이용해서
서버로부터 새로운 엑세스 토큰을 발급 받는다.

---
### JWT 장점
- 데이터의 `위변조를 방지`한다

- JWT는 인증에 필요한 모든 정보를 담고 있기 때문에 인증을 위한 별도의 저장소가 없어도 된다
- 세션(Stateful)과 다르게 서버는 무상태(StateLess)가 된다
- `확장성`이 우수하다
- 토큰 기반으로 다른 로그인 시스템에 `접근 및 권한 공유`가 가능하다 (쿠키와의 차이)
- OAuth의 경우 소셜 계정을 통해서 다른 웹서비스에 로그인 할 수 있다
- 모바일에서도 잘 동작한다(세션은 모바일x)

> 서버에서 가장 피해야 할 것은 DB 조회이다
서버가 죽는 경우 중 대부분은 DB가 터져서 서버도 같이 죽는 경우이다
이와 관련해서 JWT는 `DB조회가 필요없다`는 장점을 가지고 있다

---
### JWT 단점
- 쿠키/세션과 다르게 토큰의 길이가 길어, 인증 요청이 많아질수록 네트워크 부하가 심해진다
- Payload 자체는 암호화가 되지 않아 `중요한 정보는 담을 수 없다`
- `토큰을 탈취`당한다면 대처가 매우 어렵다
- JWT는 유효기간을 따로 정하지 않는 이상 소멸되지 않기 때문에 `장기간 방치시 해킹의 위험`이 커진다 (따라서 사용 기간 제한을 설정하는 식으로 극복한다)
> JWT를 localstorage에 보관한다면 `XSS공격`에 취약해진다 (XSS는 외부의 해커가 우리의 프로그램에 특정 javascript 코드를 심어서 localstorage에 접근하는 공격)
>> 보통 httpOnly가 설정되서 브라우저만 접근 가능한 쿠키에 토큰을 실어보내서 XSS 공격을 막는다

---
### JWT vs Cookie & Session
||장점|단점|
|:--:|:----:|:-----:|
|Cookie & Session|1. Cookie만 사용하는 방식보다 보안 향상<br> 2. 서버쪽에서 Session 통제 가능 <Br>3. 네트워크의 부하가 낮음|세션 저장소 사용으로 인한 서버의 부하|
|JWT|1. 인증을 위한 별도의 저장소가 필요 없음<Br>2.  빠른 인증 처리 <Br>3. 확장성 우수|토큰의 길이가 길수록 네트워크의 부하 증가 <br> 특정 토큰을 강제로 만료시키기 어려움|

---
### JWT와 OAuth 차이
> OAuth는 프레임워크라서 비교하는 것이 맞지는 않다
- OAuth
```
인터넷 사용자들이 비밀번호를 제공하지 않고 다른 웹사이트 상의 자신들의 정보에 대해 웹사이트나 애플리케이션의 접근 권한을 부여할 수 있는 공통적인 수단으로서 사용되는, 접근 위임을 위한 개방형 표준
```

JWT가 과일이라면 OAuth는 과일을 담는 상자라고 볼수 있다    
JWT는 `Token의 한형식`이고, OAuth는 하나의 `Framework`이다

여기서 OAuth가 Framework인 이유는<br>
1. `토큰을 요청할 때 사용할 수 있어야하는 요청 및 응답의 순서와 형식`만 있다
2. `각기 다른 시나리오에서 어떤 방식으로 권한 부여 유형을 사용`할지 정한다

-> JWT는 이러한 Framework에서 발생하는 산출물로 볼 수 있다

하지만 **Auth Framework를 통해 나온 Oauth Bearer token과 단순한 JWT 토큰은 차이**가 있다

- OAuth Token 
```
어떤 사용자의 정보와 같은 중요한 정보가 있는 토큰이 아니다 그래서 이 토큰을 사용하는 사용자는 이 토큰이 가지고 있는 정보에 대해서 아는 바가 전혀 없다
```
OAuth Token이 가지고 있는 정보는 `일련의 랜덤한 문자열`인데, 이는 `일존의 Pointer로 OAuth Framework`로 들어가서 해당 정보가 `저장되어 있는 주소`를 확인할 수 있는 인식표이다
> 이때 토큰이 JWT 유형의 토큰이 될 수도 있다

- JWT Token
```
명확한 정보를 가지고 있는 토큰
토큰의 크리는 300 ~ 500 byte 혹은 가지고 있는 속성 정보에 따라 더 커지기도 한다
```

**정리**
- JWT -> 클라이언트와 `서버 간의 인증을 처리하기 위한 토큰`, `토큰 자체에 정보를 포함`한다
- OAuth -> 사용자의 `인증과 권한 부여를 위한 프로토콜``, 클라이언트가 사용자의 동의를 얻어 `제한된 액세스 토큰을 발급받아 자원에 접근`한다

---
### Access Token & Refresh Token
```
기본 JWT 방식의 인증(보안) 강화 방식인 Access Token & Refresh Token 인증방식
```

JWT도 제 3자에게 토큰 탈취의 위험성이 있기 때문에, 그대로 사용하는 것이 아닌 `Access Token, Refresh Token`으로 이중으로 나누어 인증을 하는 방식을 현업에선 취한다

- Access Token : `클라이언트가 갖고 있는 실제로 유저의 정보가 담긴 토큰`으로, 클라이언트에서 요청이 오면 서버에서 해당 토큰에 있는 정보를 활용하여 사용자 정보에 맞게 응답을 진행한다

- Refresh Token : `새로운 Access Token을 발급해주기 위해 사용하는 토큰`으로 짧은 수명을 가지는 Access Token에게 새로운 토큰을 발급해주기 위해 사용한다   
해당 토큰은 보통 `데이터베이스`에 유저 정보와 같이 기록한다
> Access Token과 Refresh Token은 둘다 똑같은 JWT이다 다만 토큰이 어디에 저장되고 관리되느냐에 따른 사용 차이일 뿐이다

**Access / Refresh Token 재발급 원리**   
1. 기본적으로 `로그인 같은 과정`을 하면 Access Token과 Refresh Token을 모두 발급한다   
이때, Refresh Token만 `서버측의 DB에 저장`하며, Refresh Token과 Access Token을 `쿠키 혹은 웹소토리지`에 저장한다

2. 사용자가 `인증이 필요한 API에 접근`하고자 하면, 가장 먼저 토큰을 검사한다   
이때, 토큰을 검사함과 동시에 각 경웨 대해서 `토큰의 유효기간을 확인하여 재발급 여부를 결정`한다
    ```
    - access token과 refresh token 모두가 만료된 경우 
        -> 에러발생 (재 로그인하여 둘다 새로 발급)

    - access token 만료, refresh token 유효 
        -> refresh token을 검증하여 access token 재발급

    - access token 유효, refresh token 만료 
        -> access token을 검증하여 refresh token 재발급

    - access token과 refresh token 모두가 유효한 경우 
        -> 정상처리
    ```
    > refresh token을 검증하여 access token 재발급
    >> 클라이언트(쿠키, 웹스토리지)에 저장되어있는 refresh token과 서버 DB에 저장되어있는 refresh token 일치성을 확인한 뒤 access token 재발급한다
    > access token을 검증하여 refresh token 재발급
    >> access token이 유효하다라는 것은 이미 인증된 것과 마찬가지니 바로 refresh token 재발급한다

3. 로그아웃을 하면 Access Token과 Refresh Token을 모두 만료시킨다

**Refresh Token 인증과정**   
![](https://blog.kakaocdn.net/dn/bL0Upi/btqEF44TxgK/KwUK00u4qq3VRSzDpcRkx1/img.png)

1. 사용자가 ID , PW를 통해 로그인.

2. 서버에서는 회원 DB에서 값을 비교

3. ~ 4. 로그인이 완료되면 Access Token, Refresh Token을 발급한다. 이때 회원DB에도 Refresh Token을 저장해둔다.

5. 사용자는 Refresh Token은 안전한 저장소에 저장 후, Access Token을 헤더에 실어 요청을 보낸다.

6. ~ 7. Access Token을 검증하여 이에 맞는 데이터를 보낸다.

8. 시간이 지나 Access Token이 만료됐다.

9. 사용자는 이전과 동일하게 Access Token을 헤더에 실어 요청을 보낸다.

10~11. 서버는 Access Token이 만료됨을 확인하고 권한없음을 신호로 보낸다.
> Access Token 만료가 될 때마다 계속 과정 9~11을 거칠 필요는 없다.
사용자(프론트엔드)에서 Access Token의 Payload를 통해 유효기간을 알 수 있다.
따라서 프론트엔드 단에서 API 요청 전에 토큰이 만료됐다면 곧바로 재발급 요청을 할 수도 있다.

12. 사용자는 Refresh Token과 Access Token을 함께 서버로 보낸다.

13. 서버는 받은 Access Token이 조작되지 않았는지 확인한후, Refresh Token과 사용자의 DB에 저장되어 있던 Refresh Token을 비교한다. Token이 동일하고 유효기간도 지나지 않았다면 새로운 Access Token을 발급해준다.

14. 서버는 새로운 Access Token을 헤더에 실어 다시 API 요청 응답을 진행한다. 