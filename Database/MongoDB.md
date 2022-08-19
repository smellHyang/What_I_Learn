# MongoDB

## 1. MongoDB

- NoSQL(Not Only SQL) DBMS의 한 종류
- Schema가 없고 json형태의 문서지향적 NoSQL 데이터베이스
- 오픈소스 문서지향(Document-Oriented)적 데이터베이스

## 2. RDBMS와 비교

![image](https://user-images.githubusercontent.com/73684562/185583127-b306b5dd-9333-4ed6-96a8-cd1d1665ef41.png)

|  | RDBMS | MongoDB |
| --- | --- | --- |
| 사용처 | 데이터 정합성이 보장되는 시스템 | 낮은 지연시간, 가용성이 중요한 시스템 |
| 데이터 모델 | 정규화 및 참조 무결성이 보장된 스키마 | 스키마 X |
| 트랜잭션 | ACID | BASE |
| 확장 | Scale Up | 수평확장(Scale out) |
| API | SQL 쿼리 | BSON |

## 4. 물리적 데이터구조

![image](https://user-images.githubusercontent.com/73684562/185583167-3f3f368b-0858-4a2b-bc07-1219912d7fe7.png)

- mongoDB의 데이터 저장소는 메모리 맵 파일(Memory Mapped File)기반의 가상 메모리를 사용한다.
- write동작과정
    - 디스크에 바로 작업하는것이 아닌 memory공간에 작업하고 일정주기에 따라 메모리 block들을 주기적으로 디스크에 write한다.
    - 이 디스크 write작업은 os에 의해 이루어짐
- 가상메모리
    - 페이지(page)라는 블록 단위로 나뉘어진다.
    - 이 블록들은 디스크 블록에 mapping
    - 이 블록들의 집합이 하나의 데이터파일이 된다.
- 성능이슈
    - 메모리 성능을 좌우하는건 page fault와 관련이 있다.
    - 물리메모리에 해당 데이터 블록이 없으면 page fault가 발생하게 되고 디스크에서 그 데이터 블록을 로드하면서 다른 데이터 블록을 사용한다.
    - 여기서 페이지를 memory와 disk사이에 스위칭 현상이 일어나기 때문에 diskIO가 발생하고 성능저하를 유발한다.
    
    ⇒ 자주 사용하는 데이터들이 집중되서 메모리에 올라가도록 key를 설계해야한다. 
    
    ⇒ 쓸데없이 전체 데이터를 scan하는 작업을 하게되면 page fault가 발생할 수 있으므로 table scan이 필요할떄는 별도의 index table을 만들어서 사용한다.
    

## 5. 특징

- 문서지향 스토리지
    - database > collections > documents 구조로 document는 key-value형태의 BSON(Binary JSON)으로 되어있다.
- 다양한 인덱싱 제공
- Replication 및 고가용성 : 데이터 복제 및 가용성 향상
- Auto-Sharding : 데이터를 자동으로 분산하여 저장하며, 하나의 collection 처럼 사용할수 있게한다 → 수평적 확장
- 다양한 종류의 쿼리문 지원 (정렬, 정규표현식, 배열..)
- 분산 파일 저장을 자동으로 지원, 실제 파일이 어디에 저장되어 있는지 신경쓸 필요없고 복구도 자동.

## 6. 장단점

### 장점

- 유연성 : 어떤 형태의 데이터라도 저장 가능
- 성능 : Read & Write성능이 뛰어나 캐싱이나 많은 트래픽 감당 시 유용
- 확장성 : Scale Out구조로 auto-sharding지원
- 쌓아놓고 삭제가 없는 경우 적합(ex. 로그데이터, 세션..)
- 문서지향적 query사용으로 뛰어난 성능제공
- json형태로 저장하여 직관적이고 개발이 편하다

### 단점

- 정합성이 떨어지므로 트랜잭션이 필요한 경우에는 부적절(ex.금융, 결제..)
- Join이 필요없도록 데이터 구조화 필요
- memory기반 DB이므로 메모리 관리를 OS에게 위임한다. 메모리에 의존적을수 밖에 없다
- SQL을 완전이 이전하기는 어렵다.
- B-Tree인덱스를 사용하는데 크기가 커질수록 새로운 데이터를 입력하고나 삭제할때는 성능저하 → 변하지 않는 데이터 정보 조회시 유용
