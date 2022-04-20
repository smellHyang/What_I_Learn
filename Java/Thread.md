# Thread

1. 쓰레드(Thread)??
    - 프로세스 내에서 실행되는 하나의 단위
    - 쓰레드가 생성될때마다 별도의 스택이 할당된다.
    - 이 쓰레드는 프로세스의 자원들을 공유한다
    
    <aside>
    💡 프로세스란? 사용자가 실행한 프로그램이 운영체제에 의해 메모리공간을 할당받아 실행중인 상태
    데이터, 메모리 등의 자원과 쓰레드로 구성되어있다.
    
    </aside>
    
    [Thread/Process](Thread%203372d/Thread%20Pro%203e1dd.md)
    
2. 쓰레드(Thread)사용 이유?
    - 메모리 절약
        
        → 하나의 작업을 실행할 때 보통 32MB~64MB의 물리 메모리를 점유한다. 
        
            그에 반해 쓰레드 하나 추가하면 1MB 이내의 메모리를 점유한다. (쓰레드 = 경량 프로세스)
        
    - 빠른 계산 처리
    
3. 쓰레드 생성
    
    ```java
    //Runnable 인터페이스로 생성
    class RunnableSample implements Runnable{
    	public void run(){
    		System.out.println("Runnable 인터페이스 생성");
    	}
    }
    
    //Thread 클래스로 생성
    class ThreadSample extends Thread{
    	public void run(){
    		System.out.println("Thread 클래스 생성");
    	}
    }
    
    //실행
    //
    public class RunThreads{
    	public static void main(String[] args){
    		RunThreads threads = new RunThreads();
    		threads.runBasic();
    	}
    
    	public void runBasic(){
    		RunnableSample runnable = new RunnableSample();
    		new Thread(runnable).start();
    
    		ThreadSample thread = new ThreadSample();
    		thread.start();
    		}
    }
    ```
    
    - run()메소드는 시작점, 쓰레드를 시작하는 메소드는 start()
    - run()메소드가 종료되어어야 쓰레드가 끝난다. → run()메소드가 끝나지 않으면 실행한 어플리케이션은 끝나지 않는다.
    - 왜 두가지 방식이 존재?
        
        → 자바에서 상속은 하나의 클래스만 확장가능, but 이미 어떤클래스에서 이미 다른 클래스를 확장해놨으면 쓰레드클래스 상속 못함. 하지만 인터페이스는 여러개를 구현해도 상관없다. 따라서 이럴경우 Runnable 인터페이스로 구현하면됨.
        
    1. 쓰레드 스케쥴링(Thread Scheduling)
        - 우선순위 방식(Priority)
            - 쓰레드가 대기하고 있는 상황에서 더 먼저 수행할 수 있는 순위(but 권장안함..)
                
                ```java
                thread.setPriority(우선순위); // Thread 클래스 상수 제공 
                thread.setPriority(Thread.Max_PRIORITY); // 10 
                thread.setPriority(Thread.NORM_PRIORITY); // 5 
                thread.setPriority(Thread.MIN_PRIORITY); // 1
                ```
                
        - 순환 할당 방식(Round-Robin)
            - 시간을 정해서 하나의 쓰레드를 정해진 시간만큼 실행하고 다시 다른 쓰레드를 실행시키는 방식
            
    2. 데몬 쓰레드 (Daemon Thread)
        - 일반쓰레드의 작업을 돕는 보조적인 역할
        - 일반쓰레드가 모두 종료되면 데몬쓰레드는 강제로 종료된다.
        - e.g. 가비지컬렉션, 워드프로세스의 자동저장
        - 쓰레드가 실행되기전 데몬쓰레드로 지정해주어야한다.
            
            ```java
            DaemonThread dt = new DaemonThread();
            dt.setDaemon(true);
            dt.start();
            ```
            
    
    1. 쓰레드의 동기화(Synchronized)
        - 여러쓰레드에서 하나의 객체를 접근하는것을 막는것
        - 인스턴스 변수만 수정하려고 할때 사용 (매개변수, 지역변수는 xxx)
            - 메소드 자체를 Synchronized로 선언
                
                ```java
                public synchronized void plus(int value){
                	amount += value;
                }
                ```
                
            - 메소드 내의 특정문장만 Synchronized로 감싼다.
                
                ```java
                Object lock = new Object();
                
                public void plus(int value){
                	synchronized(lock){
                		amount+=value;
                	}
                }
                ```
                

7. 쓰레드 그룹(ThreadGroup)

- 여러 쓰레드를 관리하기 위한 클래스
