# Collection - Map

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
	//[이향아=95, 문다영=94, 신정연=29]
```

1. HashMap
    - 순서 xxxxx( 입력한대로 출력되지않음,....!)
    - 동작원리 (set과 비슷 - key값이 기준)
        - 동일한 key일 경우 새로운 객체를 저장하기전 해시코드값을 얻고 이미 저장되어 있는 객체들의 해시코드 값과 비교한다.
        - 동일한 해시코드값이 있다면 equals()로 두 객체를 비교하여 동일한 객체로 판단하고 저장하지 않는다
    - 왜 필요한가?? 성능때문에
        
        → HashMap은 해싱함수를 통해 바로 인덱스에 접근할수 있다. 
            만약 list를 사용했다면 원소를 검색하는데 시간복잡도는 O(n), HashMap은 O(1) 
            따라서 HashMap이 더 빠름
        
    
    [Map - HashMap](Collection%2012e5c/Map%20-%20Hash%2099539.md)
    
2. HashTable
    - Thread Safe(동기화 가능)
    

 > 비교 : 

[HashMap/HashTable](Collection%2012e5c/HashMap%20Ha%2066cd9.md)

1. TreeMap
    - 이진트리 구조
    - 오름차순 - key를 정렬 (숫자 > 알파벳 대문자 > 소문자 > 한글)
    - 정렬되기 때문에 HashMap보다 느림

1. LinkedHashMap
    - HashMap과 동일한구조 but, 입력순서대로 관리(중복xxxx)