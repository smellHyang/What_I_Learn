# HTTPS는 평문 전송을 해도 안전 할 까?

## 1. HTTP 단점

- 암호화 하지 않은 평문이기 때문에 도청가능
- 통신상대를 확인하지 않기 때문에 위장가능
- 통신 중간에 파일 변조 가능

## 2. HTTPS

![image](https://user-images.githubusercontent.com/73684562/179738458-4f740769-d68a-4065-b25a-12ae98e19da6.png)

- 보안계층의 SSL 프로토콜 위에서 실행되는 프로토콜
- 키를 교환하는 곳에서는 비대칭키 사용
- 통신에서 메시지를 교환하는 곳에서는 대칭키를 사용

## 3. HTTPS는 평문 전송을 해도 안전 할 까?

- HTTPS 비대칭키를 사용하기 때문에 패킷이 암호화 되어있다. 따라서 중간에서 가로채서 암호를 풀기 어렵다.

