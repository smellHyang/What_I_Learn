# API Gateway가 무엇일까요?

## 1. API Gateway?

![image](https://user-images.githubusercontent.com/73684562/176889167-da6a58c1-3f8d-4712-a9c6-db7abcf37017.png)

- 서비스로 전달되는 모든 API요청의 GATEWAY 역할을 하여 각 **서비스의 엔드포인트를 단일화**해주는 서비스

## 2. 필요성

![image](https://user-images.githubusercontent.com/73684562/176889147-c7713420-9d7c-4594-9cb7-b91c57662b55.png)

- 클라이언트에서 직접 서비스를 호출할시 발생할수 있는 문제점
    - 수많은 API호출을 기록하고 관리하기 어려움
    - Client마다 수많은 서비스에 대해 로출하기 어렵다.
    - 모든 서비스가 웹통신에 적합합 프로토콜로 통신하지않음
    - 서비스 추가 시 호스트 정보가 변경되고 client의 정보도 수정해줘야함
    

## 3. 장단점

### 장점

- client의 요청을 **일괄적**으로 처리
- 전체 시스템의 부하를 분산시키는 **로드밸런서** 역할
- 동일한 요청에 대해 불필요한 반복작업을 줄여주는 **캐싱**
- 시스템 상 오고가는 요청, 응답에 대한 **모니터링**
- 시스템 내부에 **아키텍쳐**를 숨길수있다.

### 단점

- 모든 요청이 Gateway를 거치기 때문에 응답시간이 늘어날수 있다.
- gateway 장애 시 모든 서비스가 작동하지 않는 SPOF(Single Point Of Failure) 문제가 발생 할 수 있다.

## 4. 기능

- **인증 및 인가**
    - 같은 소스코드를 서비스마다 심어주는것이 아닌 api호출에 대한 인증 및 인가를 지원함으로써 중복 및 관리 용이
- **라우팅과 로드밸런싱**
    - API호출을 적절한 서비스에 라우팅
    - 부하가 많은 서비스에 대해서만 로드밸런싱 가능
- **서비스 디스커버리(Service Discovery)**
    - 서비스가 분리되어 있는 상황에서 호출하려면 각각의 ip,port주소를 알아야 한다. 하지만 API의 갯수가 많아지면 찾기 어려움
    - 내가 원하는 서비스의 ip,port 주소를 찾아주는 역할
- **서비스 오케스트레이션**
    - 여러개의 마이크로서비스를 묶어 새로운 서비스를 만드는 개념
    
- 참고
