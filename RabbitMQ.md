# RabbitMQ

## 1. RabbitMQ?

- AMOP프로토콜을 구현한 메세지 브로커
- 생산자에게 메시지를 받아 소비자에게 전달해주는 서비스

<aside>
💡 AMOP(Advanced Message Queuing Protocol) : client(application)와 미들웨어간에 메시지를 주고받기 위한 프로토콜

</aside>

## 2. 구조

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/45677e58-35f5-4c20-abb9-880d54cdebca/Untitled.png)

- producer : 메시지를 보낸다
- consumer : 메시지는 producer로부터 받아 처리
- message : 처리할 내용
- queue : producer가 발송한 메시지 들이 consumer가 소비하기전까지 보관하는 장소
- exchange :  메시지를 queue에 전달
    - 메시지를 어떤 queue에 얼마나 추가할지에대한 규칙으로 라우팅한다.
- binding : exchange에게 메시지를 라우팅할 규칙을 지정하는 행위

## 3. Exchange 방식

- Direct Exchange(Default)
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/966cbbdb-e17b-41e2-a8ef-e51ae3044a6c/Untitled.png)
    
    - 메시지에 포함된 routing key기반으로 직접 선택하여 queue에 메시지를 전달한다.
    - exchage과 queue는 1:N 가능
    - Unicast
- Topic Exchange
    - routing key 문자열 내 *(start), #(hash)를 삽입시켜 유연한 binding을 제공한다.
    - Multicast
    
    ```java
    *(star) - 단어 한개를 대체한다.
    #(hash) - 0개 이상의 단어를 대체한다.
    ```
    
- Fanout Exchange
    - routing key에 상관없이 연결된 모든 queue에 동일한 메시지 전달
    - Broadcast
- Headers Exchange
    - producer에서 정의하는 key-value와 메시지를 받는 consumer의 key-value가 일치하면 binding
    - x-match(all) : 모든 조건을 충족시켜야한다.
    - x-match(any) : 최소 1개의 조건만 충족하면된다.
    - Multicast

| 타입 | 설명 | 특징 |
| --- | --- | --- |
| Direct  | Routing key가 완전 일치 | Unicast |
| Topic | Routing key의 패턴 일치 | Multicast |
| Fanout | key-value값 기준으로 일치 | Multicast |
| Headers | 해당 exchange에 등록된 모든 queue에 메시지 전송 | Broadcast |

## 3. 소비자 서버 다운

- ack를 받지 못한 메시지의경우, 대기를 하고 있다가 소비자 서버의 상태를 파악한 후, disconnected와 같은 신호를 받았을 경우 해당 소비자 제외한다. 이 후 다른 소비자에게 동일한 메시지 전달

## 4. **Message Durability**

- 메시지를 queue에 넣고 소비자에게 전달하기 전 mq서버가 죽는다면 queue는 메모리에 데이터를 쓰는 형식이므로 데이터가 소멸한다.
- message durability는 메시지가 큐에 저장될때 disk의 파일에도 동시에 저장한다.
- 이 방법은 서버가 죽었을때 queue의 데이터가 일부 복구 되지만 메지시가 disk 파일에 쓰는 도중에 서버가 죽는다면 데이터 소실이 발생한다.

## 5. Prefetch Count

- 하나의 queue에 여러 consumer가 존재할 경우, Round-Robin 방식으로 메시지를 분배한다.
- 여기서 consumer가 2개인 상황에서 하나는 메시지 처리가 짧고, 하나는 처리기간이 길때 하나의 consumer만 계속 일을 하는경우가 발생
- 이를 예방하기 위해 prefetch count를 1로 설정해두면, 하나의 메시지가 처리되기 전에 새로운 메시지를 받지않게함으로써 작업을 분산시킨다.

## 6. 특징

- 유연한 라우팅
- 제품성숙도가 높다
- 신속한 요청-응답이 필요한 웹서버에 적합
- 장기실행 작업 처리
- 안정적인 백그라운드 작업실행
- 소비자 중심 설계
