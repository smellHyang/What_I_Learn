# JAVA8 - 람다(Lambda)

- 익명클래스의 단점(가독성)을 보완하기 위해 만들어짐
- 메소드가 “하나"인 인터페이스만 사용가능 → 인터페이스의 2개의 메소드가 있을때 사용 시 컴파일 오류!
- 익명클래스로 전환가능(익명클래스도 람다로 전환가능)
- 사용방법
    
    ```java
    @FuntionalInterface
    interface Calculate{
    	int operation(int a, int b);
    }
    
    private void calculateLambda(){
    	Calculate calAdd = (a, b) -> a + b;
    	System.out.println(calAdd.operation(1,2); //3
    }
    ```
    
1. 기능적 인터페이스(Funtional Interface)??
    - 하나의 메소드만 선언되어있는 인터페이스
    - 인터페이스 선언 시 어노테이션 사용
    - 처리식이 한줄 이상일 경우 중괄호로 묶어서 사용

1. Stream
    - 연속된 정보를 처리하는데 사용(컬렉션) → 배열은 사용 못함.
    - 사용 방법
        
        ```java
        Integer[] values = {1,3,5};
        List<Integer> list = new ArrayList<Integer>(Arrays.asList(values));
        
        //스트림변환
        List<Integer> list = Arrays.stream(values).collect(Collectors.toList);
        
        //
        list.steam() //스트림생성 : 컬렉션 목록을 스트림객체로 변환
        		.filter(x-> x>10) //중개연산 : 생성된 스트림객체를 사용하여 중개연산부분을 처리(리턴xxx)
        		.count() //종단연산 : 중개연산의 내용을 결과로 리턴해준다
        ```
