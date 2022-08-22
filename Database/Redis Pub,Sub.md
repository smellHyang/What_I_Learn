# Redis Pub/Sub

## 1. Redis

- key-value 형태의 비정형 데이터를 저장하고 관리하기 위한 오픈소스 DBMS
- 비관계형 데이터 베이스 시스템으로 캐시, 메시지 브로커로 사용되며 In Memory 데이터 구조이다.
- String, List, Hash, Set, Sorted Set 등 자료구조를 지원한다.
- 캐시서버 사용

## 2. 특징

- 영속성을 지원하는 인메모리 데이터 저장소
    - 영속성 보장을 위해 데이터를 디스크에 저장가능
    - RDB(SnapShootting) : 순간적으로 메모리에 있는 내용 전체를 디스크에 copy
    - AOP(Append On File) : 모든 write/update 연산자체를 log파일에 기록하는 형태
- 다양한 자료구조 지원
- read/write 성능 증대를 위한 Replication/샤딩 지원
- 싱글 스레드 방식으로 인해 연산은 원자적으로 수행가능
- key-value 방식으로 쿼리를 날리지 않아 빠르게 결과값 얻얼수 있다.
- 단점 : 데이터 유실 가능성, 메모리 파편화

## 3. Pub/Sub

![image](https://user-images.githubusercontent.com/73684562/185922764-6d471e1c-847d-42d3-8d61-ce246467a25b.png)

- subscriber가 channel을 구독한다.
- 이때 channerl에는 이벤트를 저장하지 않으므로 이벤트가 도착했을때 해당 channel에 subscriber가 존재하지 않는다면 이벤트는 사라진다.
- 특정한 채널 또는 패턴설정으로 채널구독 가능
- 구독자는 여러channel 구독 가능

## 4. 분산 ****Pub/Sub****

- 마스터에서 publish한 메시지를 슬레이브에서 subscribe할 수 있다.
- 슬레이브에서도 publish가능하고 이 메시지는 다른 슬레이브에서 subscribe가능
- 분산된 pub/sub클러스터 모드에서 글로벌 pub/sub에 비해 메시지 전파를 제한함으로써 샤드를 추가하여 scale out가능
