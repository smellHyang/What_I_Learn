# Kafka

## 1. Kafka

- 대용량, 대규모 메시지 데이터를 빠르게 처리하도록 개발된 분산 메시징 플랫폼
- publisher와 subscriber로 이루어진 비동기 메시징 전송방식
- 수신자가 정해져 있지 않은상태로 발행하면 구독한 수신자만이 메시지를 받을 수 있다.

## 2. 구조 및 작동방식

![image](https://user-images.githubusercontent.com/73684562/185792463-0d2587c7-645f-45f9-80f1-5dc94101356b.png)

![image](https://user-images.githubusercontent.com/73684562/185792467-502811bb-277e-4ac1-949b-ed91b71e52e9.png)

- producer : 데이터를 파티션 내부의 queue로 전송
- consumer : 파티션 내부의 queue에서 데이터를 가져감
- partition : topic내에서 메시지가 분산되어 자장되는 단위
- topic : 데이터를 최종적으로 저장하는 공간, 데이터 구분을 위한 저장소이다.
- broker : Kafka Server
- zookeeper : 분산 어플리케이션 관리를 위한 코디네이션 시스템

-=

### 작동 방식

- 프로듀셔는 새 메시지를 카프카 서버에 전달
- 전달된 메시지는 브로커의 topic에 메시지 구분자에 저장
- consumer는 구독한 토픽에 접근하여 메시지를 가져온다.(pull)

## 3. Topic 내부구조

![image](https://user-images.githubusercontent.com/73684562/185792479-dc5be639-1297-49d4-b3ff-7a1198128a49.png)

- topic 내부동작
    - 프로듀서가 메시지를 토픽에 전송하면 내부에 파티션으로 나누어 관리한다.
    - 여기서 메시지 저장위치를 offset이라고 한다
    - producer는 메시지를 파티션의 맨 뒤에 추가하고 consumer는 offset기준으로 메시지를 순서대로 읽는다
    - 메시지는 삭제되지 않고 일정시간뒤에 삭제된다.
- Partition 메시지 순서
    - 파티션이 여러개인 경우 메시지는 각각 파티션으로 순차적 배분(Round Robin)
    - 같은 key를 같는 메시지는 같은 partition에 저장
    

## 4. Consumer 그룹

![image](https://user-images.githubusercontent.com/73684562/185792484-13a8d742-a4e1-4e8b-a7c3-6251b4984e1b.png)

- Consumer가 prodocer의 메시지 전송속도를 따라가지 못할 경우 consumer를 확장하여 하나의 partion당 하나의 consumer가 연결되도록한다.
- partirion : consumer = 1 :1
- 같은 consumer group의 consumer들은 동일한 partition을 읽을 수 없다.
- consumer group에 consumer가 추가되는 경우 리밸런싱을 통해 파티션을 고르개 소비할 수 있게끔 한다.

## 5. 파티션 Replication

- 고가용성 및 데이터 유실을 막기 위해 replication수행
- 원본 partition은 리더, 복제 partition은 팔로워가 되는데
- 리더 파티션의 브로커가 다운될 경우 팔로워 파티션이 새로운 리더가 되어 producer의 요청을 처리한다.

## 6. 특징

- consumer가 메시지를 소비하더라고 디스크에 메시지를 일정기간 보관하기때문에 메시지 손실이 없다
- producer : consumer = N : M
    - 멀티프로듀셔, 멀티 컨슈머로 하나 이상의 메시지를 주고 받을 수 있다.
- 분산형 스트리밍 플랫폼(고가용성)
    - 단일 시스템 대비 성능이 우수하고, 시스템 확장이 용이하다.
    - 일부 노드가 죽더라도 다른 노드가 해당 일을 지속한다.
- 페이지 캐시
    - disk read/write이 아닌 **페이지 캐시**로 read/write하여 처리속도가 빠름
- 메시지를 단위로 묶어 배치처리 함으로써 속도가 빠름

## 7. 장단점

### 장점

- 분산 처리 시스템으로 고성능, 고가용성, 확장성
- 배치 처리가 가능해 네트워크 왕복 오버헤드를 줄일 수 있다.
- disk 파일 시스템에 데이터를 저정함으로 영속성 보장(복구가능(

### 단점

- prodocer 중심적이고, 메시지 전달보장이 선택적
- 리더와 팔로워 모두에게 응답승인을 받아야 하므로 처리속도가 느려진다.
- 라우팅 기능이 없어 producer가 직접 적절한 topic으로 보내줘야한다.
