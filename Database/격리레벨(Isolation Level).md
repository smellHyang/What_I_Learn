# 격리레벨

## 격리성 문제점

### 1. Dirty Read

- 다른 트랜잭션에 의해 수정됐지만, 아직 커밋되지 않은 데이터를 읽음

### 2. Non-Repeatable Read

- 한 트랜잭션 내에서 같은 key를 가진 row를 두번 읽었는데 그 사이에 값이 변경되거나 삭제되어 결과가 다르게 나타나는 현상
- 1개의 row데이터값 변경

### 3. Phantom Read

- 한 트랜잭션 내에서 같은 쿼리를 두번 수행했는데, 첫번째 쿼리에서 없던 유령레코드가 두번째 쿼리에서 나타나는 현상
- 여러개의 row데이터값 변경

## 격리성 수준

1. **Level 0** Read Uncommitted
2. **Level 1** Read Committed
3. **Level 2** Repeatable Read
4. **Level 3** Serializable

### **Read Uncommitted**

- 트랜잭션에서 처리중인, 아직 커밋되지 않은 데이터를 다른트랜잭션이 읽는 것을 허용
- Dirty Read, Non-Repeatable Read, Phantom Read 발생 가능

### Read Committed

- 트랜잭션이 커밋된 데이터만 다른 트랜잭션이 read허용
- Insert, update와 같은 처리 세션이 lock을건다.(select 대기)
- Non-Repeatable Read, Phantom Read 발생 가능

### Repeatable Read

- 앞서 발생한 트랜잭션에 대해서는 실제 데이터가 아닌 Undo로그에 있는 백업데이터를 read
- select와 같은 쿼리세션이 lock을 건다(insert, update 대기)
- Phantom Read 발생 가능

### Serializable Read

- 트랜잭션 내에서 쿼리를 두번 이상 수행할 때, 첫번째 쿼리에 있던 레코드가 사라지거나 값이 바뀌지 않고 새로운 레코드가 나타나지 않도록 설정
