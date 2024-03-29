![image](https://user-images.githubusercontent.com/73684562/187216702-ce6592c2-1fcd-4478-b523-a4fe41c4cd3f.png)

## 사전 개념

### Thread

- 작성한 프로그램이 하나의 프로세스로 실행되고 이는 반드시 메인 thread를 생성하여 처리 (프로그램 → 프로세스 → thread)
- 병렬적으로 동시에 처리할 작업이 있을때 사용
- 사용 이유?
    - cpu가 프로세스들을 처리하기 위해 context switching작업(멀티 태스킹)이 발생하고 여기서 overhead가 발생할수있다.
    - 그래서 process끼리 멀티태스킹 하지않고 thread에서 처리
    - process 컨텍스트 스위칭보다 thread 컨텍스트 스위칭이 오버헤드가 더 적다.

### 멀티쓰레드 객체 공유와 상태제어

![image](https://user-images.githubusercontent.com/73684562/187216671-973d2833-1abc-4604-a6f3-e176e9a95d96.png)

| 동시성(concurrency) | 병렬성(parallelism) |
| --- | --- |
| 2개이상의 여러작업이 동시에 시작 | 2개이상의 여러작업이 동시에 실행 |
- 동시성 제어
    - 멀티 쓰레드 환경에서는 자원이 공유되고 있고 타이밍에 의해 공유자원을 동시에 변경하려고 할떄 생기는 이슈가 발생
    - 원하는 결과값이 안나올수 있다.
- 이를 해결하기 위하여 가시성, 동시성, 원자성 등을 확보해야한다.

## Visibility(가시성)

![image](https://user-images.githubusercontent.com/73684562/187216646-dd14d7c2-cb7e-4ef3-a7c3-45d7127099bb.png)

- 멀티스레드 환경에서 스케쥴링에 의해 cpu core에서 쓰레드를 담당하게 된다.
- 이때 메인 메모리에서 값을 읽어 연산하는것이 아닌 Cpu에 존재하는 Cache에 옮겨놓고 연산을 한다. (main memory에서 값을 읽어오기엔 overhead가 생기므로 cache를 두어 성능향상 목적)
- 문제는 데이터를 cache하려다 보니 main memory에 있는 값과 항상 일치하지 않을 수 있다.
- 예를 들어, 1cpu와 2cpu가 공유되고 있는 객체를 수정할때 어떤 cpu에서 cache됐냐에 따라 서로 다른값을 가질수있다. → 비가시성
- 가시성 확보를 위해 cache memory에서 값을 읽지않고 main memory의 값을 읽어온다.
    - 하지만 메인메모리의 값이 최신값이 아닐수도있고 다른쓰레드에 의해 값이 언제든 바뀔수 있다.
    - 즉, 공유 데이터를 읽을 때 동시성만 보장

## Atomic

- 공유되는 변수를 변경할때 기존값을 새로운 값으로 결정되는 과정에서 여러 쓰레드가 이를 동시에 수행할때 생기는 이슈를 보장하기 위함
- blocking의 단점(성능이슈)을 해결하기 위해 non-blocking하여 원자성 보장
- cpu cache memory와 main memory의 값을 비교하여 일치하지 않는다면 작업을 재시도하는 작업

### Synchronized

- 멀티쓰레드 환경에서 동시성 제어를 위해 공유객체를 동기화 하는 키워드
- 메소드나 메소드 안에 특정블록에만 scope을 지정해놓고 멀티쓰레드가 동시에 접근하지 못하도록 blocking

- 참고
    
    [https://rightnowdo.tistory.com/entry/JAVA-concurrent-programming-Atomic원자성?category=396739](https://rightnowdo.tistory.com/entry/JAVA-concurrent-programming-Atomic%EC%9B%90%EC%9E%90%EC%84%B1?category=396739)
    
    [https://medium.com/thxwelchs/동시성-프로그래밍-2편-멀티쓰레드-객체공유와-상태제어-44e9f697c3d9](https://medium.com/thxwelchs/%EB%8F%99%EC%8B%9C%EC%84%B1-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-2%ED%8E%B8-%EB%A9%80%ED%8B%B0%EC%93%B0%EB%A0%88%EB%93%9C-%EA%B0%9D%EC%B2%B4%EA%B3%B5%EC%9C%A0%EC%99%80-%EC%83%81%ED%83%9C%EC%A0%9C%EC%96%B4-44e9f697c3d9)
