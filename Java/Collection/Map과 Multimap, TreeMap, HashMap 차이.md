# Map과 Multimap, TreeMap, HashMap 차이

## 1. Map

- HashMap, TreeMap, LinkedHashMap, HashTable
- 키(key)와 값(value)으로 이루어져있음 (1:1구조)
    - 키가 없이 값만 저장될 수 없다.
    - 값없이 키만 저장될 수 없다.
    - 중복된 키가 저장되면 기존의 키는 없어지고 덮어씌워짐
    - key는 중복xxxxx
    - value는 중복ooooo
- 주요 메소드
    
    
    | 리턴타입 | 메소드명 | 설명 |
    | --- | --- | --- |
    | V  | put(K key, V value) | 데이터 추가(키, 값) |
    | Set<K>  | keySet() | 키의 목록을 set으로 리턴 |
    | Collection<V> | values() | 값의 목록을 Collection으로 리턴 |
    | Set<Map.Entry<k,v>> | entrySet() | 엔트리타입의 set을 리턴 |
    | V  | remove(K key) | key에 해당하는 엔트리를 삭제한다. |
    | V | get(K key) | key에 해당하는 value를 반환한다. |

```java
//데이터 추가
Map<String, Integer> map = new HashMap<>();
	map.put("이향아", 28);
  map.put("문다영", 29);
  map.put("신정연", 29);
	//{이향아=95, 문다영=94, 신정연=29}

Set<String> names = map.keySet();
	//[이향아, 문다영, 신정연]

Collection<Integer> ages = map.values();
  //28, 29, 29

Collection<Map.Entry<String, Integer>> nameAndAges = map.entrySet();
	//[이향아=28, 문다영=29, 신정연=29]
```

## 2. MultiMap

- 구글 자바 오픈소스 라이브러리인 Guava에서 제공
- Key : value ( 1: N )
- 중복 허용 가능 ( Key - value)

```java
ListMultimap<String, String> multimap = ArrayListMultimap.create();
 
multimap.put("John", "Adams");
multimap.put("John", "Tyler");
multimap.put("John", "Kennedy");
 
System.out.println(multimap);    // {John=[Adams, Tyler, Kennedy]}
```

## 3. TreeMap

- 이진트리 구조
- 오름차순 - key를 정렬 (숫자 > 알파벳 대문자 > 소문자 > 한글)
- 정렬되기 때문에 HashMap보다 느림 but, 범위 검색 시 유용
- Red-Black Tree 구조
    - 부모 노드 > 자식 노드 : 왼쪽
    - 부모 노드 < 자식 노드 : 오른쪽
    - 데이터 변동 시 트리가 한쪽으로 치우쳐 지지않도록 균형을 맞춘다(이진탐색 트리의 단점 보완)

## 4. HashMap

[Map - HashMap이란?](https://www.notion.so/Map-HashMap-566c7c0eb56548648b276be39a2a57be) 

- 순서 xxxxx( 입력한대로 출력되지않음,....!)
- 동작원리 (set과 비슷 - key값이 기준)
    - 동일한 key일 경우 새로운 객체를 저장하기전 해시코드값을 얻고 이미 저장되어 있는 객체들의 해시코드 값과 비교한다.
    - 동일한 해시코드값이 있다면 equals()로 두 객체를 비교하여 동일한 객체로 판단하고 저장하지 않는다
- 왜 필요한가?? 성능때문에
    - 만약 list를 사용했다면 원소를 검색하는데 시간복잡도는 O(n), HashMap은 O(1)
    - 따라서 HashMap이 더 빠름
    
    |  | key-value | Key중복 | value 중복 | 순서 |
    | --- | --- | --- | --- | --- |
    | map | 1:1 | X | O | X |
    | TreeMap | 1:1 | X | O | O - 오름차순 |
    | HashMap | 1:1 | X | O | X |
    | LinkedHashMap | 1:1 | X | O | O - 입력순 |
    | Hashmultimap | 1:N | X | O | X |
    | TreeMultimap | 1:N | X | O | O |
    | ArrayListMultimap | N:N | O | O  | O - 입력순 |
    | LinkedListMultimap | N:N | O | O | O - 입력순 |
    

+) C++의 MultiMap

- map과 같이 key,value로 구성
- key의 중복 허용
- 오름차순
- 이진탐색 트리
