# Boxing/Unboxing

1. Boxing vs Unboxing 개념
    - boxing : 기본자료형 -> wrapper class

```java
char pType = 'A';
Character wClass1  = new Character(pType); // 박싱
Character wClass2 = pType; // 오토박싱 : 스택영역의 값을 힙 영역에 객체를 생성해서 넣음
```

- unboxing : wrapper class -> 기본자료형

```java
Character wClass = new Character('A');
char c1 = wClass.CharValue(); // 언박싱
char c2 = 'A'; //오토 언박싱 : 힙 영역에서 값을 꺼내 스택영역으로 복사함 
```

1. 사용 이유
    - 기본자료형을 Object로 변환할 수 있다.
    - 제네릭에서는 기본자료형을 사용하지 않고 wrapper class를 사용할수 밖에 없으므로 박싱을 사용한다.
    - 멀티스레딩에서 동기화를 지원하려면 객체가 필요하다. → 멀티스레드에서는 공유객체를 사용해야할 경우가 있는데 기본자료형처럼 스레드 내에 할당되어서 독립적인 메모리상에서 굴러가는것 보다는 자원을 공유할 같은 메모리를 바라보는 객체를 사용해야한다.
2. Wrapper class 가 있는데 왜 기본자료형을 사용하는가?
    - 기본자료형은 stack 영역에 저장이 되고 wrapper class(객체)는 heap영역에 저장이 된다.
    Heap은 주소값을 참조로 하여 값을 읽고 가져오기때문에 스택에서 바로 읽는것보다 속도가 느리고 메모리를 더 많이 차지한다. 그렇기 때문에 기본자료형으로 표현할수 있는것은 기본자료형으로 표현하는게 좋다.

*기본자료형 - primitive type(boolean, char, byte, short, int, long, float, double)

*wrapper class (Boolean, Character, Double, Float, Integer, Long, Short, Byte)

+)

JAVA에서 메모리 공간은 크게 Static영역, Stack 영역, Heap 영역으로 구분된다.

1. Static area(스태틱 메모리 영역)
    - 필드, 생성자, 메소드
    - 필드 부분에서 선언된 변수(전역변수)와 정적 멤버변수(static 자료형)가 Static 영역에 데이터를 저장함
    - 프로그램의 시작부터 종료될때까지 메모리에 남아있다.
2. Stack area(스택 메모리 영역)
    - 기본자료형에 해당하는 지역변수(매개변수 및 블럭 내 변수)의 데이터 값이 저장되는 공간
    - 메소드가 호출될때 메모리에 할당되고 종료되면 메모리가 해제된다.
    - LIFO(Last In First Out)
    - 변수에 새로운 데이터가 할당되면 이전데이터는 지워진다.
3. Heap area(힙 메모리 영역)
    - 참조형(Reference Type)의 데이터를 갖는 객체(인스턴스), 배열 등은 heap 영역에 데이터가 저장된다
    - 변수(객체, 참조변수)는 stack 영역에서 실제 데이터가 저장된 heap 영역의 참조값을 new 연산자를 통해 리턴받는다 → 실제 데이터를 갖고 있는 heap영역의 참조값을 stack 영역의 객체가 갖고있다.
    - heap 영역에 저장된 데이터가 더이상 불필요하면 메모리 관리를 위해 JVM(GC)에 의해 알아서 해제된다.