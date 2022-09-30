## PCB(Process Control Block)란?



- 운영체제가 프로세스를 제어하기 위해 정보를 저장해 놓은 구조체
- 프로세스 상태 관리와 Context Swiching을 위해 필요
- 프로세스 생성 시 만들어 지며 주기억장치에 유지된다.

⇒ 프로그램 실행 시 스로세스들이 교체되어 처리한다. 이때 한 프로세스가 수행되고 다시 다른 프로세스를 불러와야하는데 이전작업내용을 기억하고 있다가 동작하게 된다. 이처럼 프로세스 단위로 정보를 저장해주는 block이 pcb이다.

---

- PID : 프로세스 고유의 번호
- 상태 : 준비, 대기, 실행 등의 상태
- 포인터 : 다음 실행될 프로세스의 포인터
- Register Information : 레지스터 관련 정보
- 스케쥴링 : 스케쥴링 및 프로세스 우선순위
- 메모리 관련 정보 : 할당된 자원 정보
- Accounting information : CPU 사용시간, 실제 사용된 시간
- I/O관련 상태 정보 : 입출력 상태 정보

---

### Process Context Swiching 수행과정 및 PCB역할

1. CPU 자체에 Register가 있으니 수행중인 프로세스 정보는 CPU 내부, 레지스터에 저장하고 있다. 
2. 하나의 프로세스(p0)가 실행되다가 긴급한 다른 프로세스가 수행되어야 하는일(p1)이 생기면 해당프로세스는 인터럽트가 걸리고 Ready상태가 된다. 이때 지금 수행되는것들을 먼저 저장한다.
3. 더 자세히는 PCB에 CPU에서 수행되던 레지스터 값들이 저장된다. (어디까지 수행됐는지, stack pointer의 위치가 어딘지..)
4. 이렇게 수행중인 프로세스를 변경할때 **레지스터에 프로세스의 정보가 바뀌는 것을 Context Swiching** 이라고한다.
    1. CPU가 이전의 프로세스 상태를 PCB에 보관하고 또다른 프로세스 정보를 PCB에 읽어 레지스터에 적재하는 과정

---

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/21fe8dbf-16ca-4af9-8712-4979d18f6ec6/Untitled.png)

## TCB(Thread Control Block)란?

- 프로세스에 있는 스레드 라이브러리에 의해 스케쥴링 되는것
- 하나의 thread를 관리하는데 필요한 정보를 담고 있는 구조체
- thread사이의 context swiching하고 process사이의 context swiching을 할때 cpu 스케쥴링을 하는 최소 단위이다.

---

- Thread ID : 쓰레드를 구분하는 식별자
- Stack Pointer : 쓰레드 별로 고유한 Stack pointer
- Program counter : 현재 instructiondml wnth
- 상태 : running, ready, waiting, start, done..
- Thread의 레지스터 값
- 쓰레드가 소속된 프로세스의 PCB주소

---

### Thread Context Swiching

- 동일한 프로세스 속에서 하나의 스레드를 중지하고 다른 스레드의 TCB정보를 바탕으로 그 쓰레드를 실행하는것
- 이때 프로세스는 stack영역의 주소와 레지스터 주소를 포함한 thread의 context정보만 변경하면된다.
- process는 하나이상의 thread로 동작하기 때문에 context swiching의 최소단위는 TCB이다.

---

### Process contexet swiching vs Thread contexet swiching


- 프로세스는 하나이상의 쓰레드 포함
- 쓰레드는 고유 stack영역, 고유 register할당 받는다.
- heap영역의 메모리에서 선언된 데이터는 서로 공유
- 동일 프로세스의 thread contexet swiching 발생경우 프로세스는 stack, register영역의 주소를 포함한 thread context정보만 변경
- process context swiching 발생 경우 thread context정보를 포함한 process context까지 모두 변경
