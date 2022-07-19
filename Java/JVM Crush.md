# JVM을 크래시 내는 방법

## 1. JAVA Crash??

- JVM 자체가 외부적인 요인으로 종료되는 경우
- JVM도 어찌됐든 어플리케이션이다. 일정 규모 이상의 모든 어플리케이션은 bug를 가지고 있음

## 2. 사례

- Segmentation fault
    - 잘못된 메모리 참조
    - os로부터 배정받지 못항 메모리 영역에 대해 침범하는것을 버그를 통해 알려줌
        - 주로 Null로 설정된 영역을 건드린 경우
        - 할당받은 메모리 공간을 넘은곳을 건드렸을때
        - 더이상 존재하지 않는 메모리 영역을 가리킬떄
        - read-only 표시 메모리 영역에 쓰려고 할때
- kill -3로 발생한 SIGQUIT
- Out Of Memory Error(OOME)
    - JVM의 메모리가 부족하여 메모리 할당 실패로 발생
- StackOverFlow

### Out Of Memory Error

1. Java Heap에서의 OOME
    
    1-1. heap 사이즈 작은경우
    
    - heap 최대 크기가 application 메모리 요구량에 비해 작게 설정 된경우
    - 메모리 leak이 발생하지 않았음에도 발생하면 heap크기 부족
    
    → heap 사이즈 증가
    
    1-2. 메모리 leak 발생한 경우
    
    - 어플리케이션 로직에 의해 발생 → gc에 의한 메모리 해제 불가
    - JDK버그 또는 WAS버그
    - heap사이즈와 무관하게 발생
    
2. Permanent Space에서 OOME
    
    2-1. 클래스나 메소드 객체를 perm space에 할당하지 못하는 경우
    
    - 너무 많은 class를 로드할때 발생
    - 대부분의 was에선 class reloading기능 제공
    
    → perm space 사이즈 조정
    
    <aside>
    💡 Class Reloading? JVM 재부팅 없이 Class 재생성될때 Reloading, 일부 WAS에선 Reloading될때 이전버전의 Class를 해제하지 않는 경우가 있다.
    
    </aside>
    

1. Native Heap에서 OOME
    
    3-1. Thread Stack Space가 부족한 경우
    
    - Thread는 native heap공간에 stack trace 공간 필요
    
    → 쓰레드 수 감소
    
    3-2. VM code 레벨에서 메모리 부족
    
    → java heap크기 감소
    

### StackOverFlow

- stack 영역의 메모리가 넘칠때 발생
- stack은 지역변수를 담아 두는곳이다. 이 변수들은 stack에 할당되었다가 해제되는데 이때 해당 변수의 크기가 stack보다 크거나 함수를 무한으로 호출할 경우 발생
- 해결방법
    - 해당 변수 크기를 stack 보다 작게 변경, 함수 무한 호출 막기
    - stack이 아닌 heap에 할당
    - stack 크기 자체를 조절
