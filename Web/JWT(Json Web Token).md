## 1. JWT(Json Web Token)

- 웹 상에서 client와 server사이에서 통신할때 정보를 json으로 주고 받기 위해 생성한 **암호화된 토큰**

## 2. 구성요소

![image](https://user-images.githubusercontent.com/73684562/176439476-7522f12b-b843-418f-b365-742cf1ce3232.png)

- 헤더 (Header)
    - 어떤 알고리즘, 토큰을 사용할것인지에 대한 정보가 담겨있다.
- 정보(Payload)
    - 전달하려는 정보(사용자id같은..)가 들어있다.
    - 수정이 가능하며 정보 추가 가능
    - 수정이 가능하기 때문에 인증이 필요한 최소한의 정보만을 담아야함
- 서명(Signature)
    - 헤더와 정보를 합친 후 발급해준 서버가 지정한 secret key로 암호화 시켜 토큰을 변조하기 어렵게 만든다.
    - 예시 ) payload에 조작된 정보가 들어가 있을 시 signature는 수정 전의 payload 내용을 기반으로 이미 암호화 되어있다. 따라서 조작되어 있는 payload와 다른결과 값이 나오면서 토큰의 조작유무 파악 가능

## 3. 동작 원리

![image](https://user-images.githubusercontent.com/73684562/176439445-fc947f38-ed2c-4301-ba9e-a6855281d810.png)

- 사용자 id, pw를 입력하여 로그인 요청
- 서버는 회원db에 들어가 있는 사용자 인지 확인
- 확인이 되면 서버는 로그인 요청 확인 후 secret key를 통해 토큰 발급(각각 base64로 인코딩)하고 이를 client에 전달
    - +) RSA의 경우 header(RSA) + payload(username..)으로 구성되고 서버가 개인키로 시크니쳐를 만들고 client에 보낸다.
- client는 서비스 요청과 권한을 확인하기 위해 헤더에 데이터(JWT) 요청
    - 로컬스토리지JWT를 담고 이와 함께 개인정보를 달라고 server에 다시 전달
- 데이터를 확인하고 JWT에서 사용자 정보 확인
    - +) RSA의 경우 서버는 공개키로 서명 검증
    - signiture에 header + payload + cors(HS256)을 담아 보내는데
    - server가 가진 cors로 client가 보낸 JWT를 디코딩하여 값이 맞으면 인증
- Client요청에 대한 응답과 요청한 데이터를 전달
    - payload정보 기반으로 해당 정보를 db에서 select하여 응답

## 4. JWT 단점

- 토큰이 만료되기전에 노출되면 보안적으로 취약
- Claim이 많아질수록 JWT토큰이 길어짐 → 네트워크 대역폭 낭비
- Payload에 대한 정보는 암호화하지않고 base64 encoding만 하기때문에 중간에서 데이터 확인 가능
- token의 영구성으로 만료까지 기다려야함 → 만료시간 꼭 게시

## 5. JWT 장점

- 토큰 자체에 모든 정보가 담겨있어 별도 인증 저장소 필요 X
- 트래픽 부담 X

## 6. Session기반 인증과의 차이

![image](https://user-images.githubusercontent.com/73684562/176439391-3a12ec6c-e947-471d-a8b2-b8fd3de80071.png)


- 사용자가 로그인하면
- 서버는 세션 저장소에서 사용자를 조회하고 세션 id를 발급(브라우저 쿠키에 저장)
- 사용자가 다른 요청을 보낼 때 마다 서버는 세션 저장소에서 세션조회 후 로그인 여부 결정하고 작업 처리

### 단점

- 서버 확장하기 번거로움
- 모든 서버끼리 같은 세션을 공유해야하고 관리가 어렵다.

| 세션 기반 인증 | 토큰 기반 인증 |
| --- | --- |
| 서버 확장성 X | 서버 확장성 용이 |
| 서버끼리 사용자정보 공유 O | 공유 X |
| 무결성 보장 X | 무결성 보장 |
| 요청 마다 인증 확인 | 인증과정 감소 |

## 6. JWT와 Session-Cookie모두 사용

- JWT를 Local Storage에 저장하면 영구적으로 저장되고 javascript를 통해 접근이 가능하여 보안에 취약 → 메모리에 저장
- Local Storage 미사용 시 브라우저 restart마다 로그인을해야함 → cookie사용으로 jwt발급
