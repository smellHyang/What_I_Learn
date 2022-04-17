# Collection - Queue

- LinkedList(List,Queue), PriorityQueue(Queue), Deque
- FIFO (First In First Out) -선입 선출
- ex) 사용자들의 요청을 들어온 순서대로 처리할 경우 큐를 사용
- 관련 메소드
    
    
    | add(Object o) | 객체를 추가
    성공하면 true, 저장공간 부족 시 Exception 발생 |
    | --- | --- |
    | remove() | 객체를 꺼내 반환
    비어있으면 Exception 발생 |
    | element() | 삭제없이 요소를 읽음
    비어있으면 Exception 발생 |
    | offer(Object o) | 객체를 저장
    성공하면 true, 실패하면 false |
    | poll() | 객체를 떠내 반환
    비어있으면 null |
    | peek() | 삭제 없이 요소를 읽음
    비어있으면 null |
    - add(),remove(),element() - Exception 반환
    - offer(),poll(),peek() - False/Null 반환
    
1. LinkedList
    - [List - LinkedList](Collection%20b2b8c/List%20-%20Lin%2050efb.md)
    
2. PriorityQueue(우선순위 큐)
    - 저장한 순서와 상관없이 우선순위가 높은거 부터 꺼냄(오름차순)
    - 객체를 저장할때는 객체의 우선순위를 제공해줘야함
    - null을 저장 할 수 없다.
    
    ```java
    Queue priorityQueue = new PriorityQueue();
    priorityQueue.offer(3);
    priorityQueue.offer(1);
    priorityQueue.offer(5);
    priorityQueue.offer(2);
    priorityQueue.offer(4);
    ```
    
    ```java
    1
    2
    3
    4
    5
    ```
    
3. Deque
    - 한쪽에서만 추가/삭제할 수 있는 Queue와 달리 양쪽 끝에서 추가/삭제 가능