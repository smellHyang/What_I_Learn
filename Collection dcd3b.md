# Collection - Set

- HashSet, TreeSet, LinkedHashSet
- 순서(x), 중복(x)
- 데이터 정렬로 인해 성능차이가 난다.
- 순서가 없어서 index로 검색 xxx
- ex) 1분간의 사용자 로그(Ip)로 사용자의 수 파악하기.

1. HashSet
    - 순서가 필요없는 데이터를 해시테이블에 저장
    - Set중에서 가장 성능이 좋다
    - 동작원리
        - 동일한 값일 경우 새로운 객체를 저장하기전 해시코드값을 얻고 이미 저장되어 있는 객체들의 해시코드 값과 비교한다.
        - 동일한 해시코드값이 있다면 equals()로 두 객체를 비교하여 동일한 객체로 판단하고 저장하지 않는다.
    
2. TreeSet
    - 오름차순으로 데이터를 정렬
    - red-black이라는 트리타입으로 값이 저장
    - HashSet보다는 성능이 느림
    
    [Red-Black 트리](Collection%20dcd3b/Red-Black%20%20e009a.md)
    

1. LinkedHashSet
    - 저장된 순서에 따라 값이 정렬
    - 연결방식으로 해시테이블에 데이터를 저장