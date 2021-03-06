# DB 트랜잭션

## 1. 트랜잭션?

- 데이터베이스에서 기능을 수행하기 위한 하나의 작업 단위

## 2. 특징

- 원자성 : 완전 반영 or 완전 실패
- 일관성 :  실행 전 후가 같아야한다.
- 독립성 : 다른 트랜잭션이 작업 중 끼어들수 없다.
- 지속성 : 고장 시 결과 반영

## 3. 목적

- 데이터 부정합 방지 : 동시 접근X
- DB의 완전성 유지 : 서로 간섭X
- 안정성 확보 : 트랜잭션 성공 시에만 DB에 반영

## 4. 연산

- COMMIT
    - 트랜잭션 수행 성공!
    - commit 후 트랜잭션 수행 결과가 DB에 반영되어 DB가 일관된 상태를 지속적으로 유지
    - commit을통해 트랜잭션 수행이 완료되었음을 선언하고 최종 DB에 반영
- ROLLBACK
    - 트랜잭션 수행 실패
    - 트랜잭션의 모든 결과가 취소되고 수행 전 상태로 돌아감
    - 실행 도중 일부 연산이 처리 되지 못한 상황에서는 rollback연산을 싱행하여 트랜잭션의 수행 실패를 선언
    - DB를 트랜잭션 수행 전의 일관된 상태로 돌린다.

## 5. 상태

![image](https://user-images.githubusercontent.com/73684562/168645321-2aa30e95-9aa4-4930-bed9-43cb76d16a8b.png)

- 활동(Active) : 트랜잭션이 실행 중
- 실패(Failed) : 트랜잭션 실행 중 오류 발생으로 중단
- 철회(Aborted) : 트랜잭션이 비정상으로 종료되어 rollback연산을 수행
- 부분 완료(Partially Committed) : 트랜잭션의 마지막 연산까지 실행됐지만, commit 연산이 실행되기 직전의 상태
- 완료(Committed) : 트랜잭션이 성공 수행되어 commit연산을 실행한 후의 상태

## 6. 회복

- 트랜잭션이 실행되는 동안 발생한 오류로부터 가장 가까운 정상상태로 복귀
- **Undo** : 트랜잭션 로그를 이용해 오류와 관련된 `모든 변경을 취소`하여 복구수행
- **Redo** : 트랜잭션 로그를 이용해 오류가 발생한 트랜잭션을 `재실행`하여 복구수행

| Undo | Redo |
| --- | --- |
| 되돌리기 | 재실행 |
| rollback | 복구 |
| Undo Segment | Redo 로그파일 |
| 멀티유저의 읽기 일관성 보호 | 데이터 손실방지 |

### 로그기반 회복

- 지연 갱신 회복
    - 트랜잭션이 부분완료에 이르기까지 발생한 모든 변경내용을 로그파일에만 저장하고 커밋 저장을 지연하는 방식
    - 중간에 장애 발생 시 DB에 아직 기록이 없기 때문에 Undo과정 불필요
- 즉시 갱신 회복
    - 트랜잭션 수행중 발생한 변경내용을 로그파일에 저장하고, 모든 변경 내용을 즉시 DB에 반영
    - 트랜잭션 완료 이전에 수행된 갱신은 미완료 갱신이라 하여 회복하는 경우 Undo, Redo 모두 수행

### 검사점 기반 회복(CheckPoint)

- 장애 발생 시 검사점 이전은 Undo, 이후는 Redo 회복작업 실행

### 그림자 페이징 회복

- 현재 테이블은 주기억장치, 그림자 페이지 테이블은 디스크에 저장하여 트랜잭션 성공 시 그림자 페이지 테이블을 삭제하고, 실패 시 그림자 페이지 테이블을 통해 복구
- 트랜잭션 시작 시 현재 테이블과 동일한 그림자 테이블 생성
