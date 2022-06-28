# DB Master-Slave 개념

## 1. Replication

[ User → Master → Slave ]

- DB 데이터를 물리적으로 복사하여 다른곳(Slave)에 넣어두는 기술(단방향)
- DB 트래픽 분산을 위해 고가용성으로 사용됨.
- Master에서 BinaryLog를 생성하여 Slave에 전달하고 Slave는 Relay Log에 기록하여 데이터로 반영

## 2. Master & Slave 사용

- Master : Insert, Update, Delete
    - 데이터 동시성이 요구 되는 트랜잭션 담당
- Slave : Read
    - 동시성 보장이 필요없는 읽기전용 데이터 담당
    

## 3. 목적

- 데이터 백업
- 부하분산

## 4. 단점

- 데이터 정합성 : master와 slave의 복제 속도 차이로 데이터가 다를수 있다.
- FailOver : Master → Slave 형식의 단방향이라 slave장애시 master를 통해  failover가 가능하지만 반대는 지원하지 않음(하지만 이것도 자동은 아님, 수작업필요)
- binarylog의 관리 : master에 binary log가 무분별하게 쌓을 수 있으므로 데이터 보관주기 설정 필요
