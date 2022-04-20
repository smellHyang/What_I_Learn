# 데드락(DeadLock)

1. 데드락이란??
    - 교착상태 → 시스템적(멀티프로세스나 쓰레드)으로 한정된 자원을 여러곳에서 사용하려고할 때 자원을 얻지못해 락이 걸려버린 상태
    - thread1이 A자원의 lock을 가지고 있는 상태에서 B자원의 lock을 획득하려한다. 
    그리고 thread2는 B의 lock을 가진상태에서 A의  lock을 가지려고 할때 
    둘다 lock상태에 걸려 다음을 수행할 수 없게된다.
    
    ![Untitled](%E1%84%83%E1%85%A6%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%86%A8(De%209e8c9/Untitled.png)
    
2. 발생 조건(모두 충족되어야)
    - 상호배제(Mutual Exclusion) - 한번에 한개의 쓰레드에서만 자원을 사용할 수 있어야한다.
    - 점유와 대기(Hold and Wait) - 한 쓰레드가 자원을 점유하고 있으면 다른쓰레드는 대기해야한다.
    - 비선점(Non-preemption) - 쓰레드가 자원을 자발적으로 해제하기 전까지 그 자원을 얻을 수 없다.
    - 순환대기(Circular Wait) - 자원과 자원을 사용하기 위해 대기하는 프로세스들이 원형으로 구성되어 있어 자신에게 할당된 자원을 점유하면서 앞이나 뒤에 있는 프로세스의 자원을 요구해야 한다.
    
3. 데드락 발생 코드
    
    ```java
    public class DeadlockClass {
        public static Object object1 = new Object(); //자원1
        public static Object object2 = new Object(); //자원2
    
        public static void main(String[] args) {
            FirstThread thread1 = new FirstThread();
            SecondThread thread2 = new SecondThread();
    
            thread1.start(); //쓰레드1실행
            thread2.start(); //쓰레드2실행
    }
    
        private static class FirstThread extends Thread{
            @Override
            public void run() {
                synchronized (object1){
                    System.out.println("쓰레드1 자원1에 대하여 lock걸음");
    
                    try {
                        Thread.sleep(10);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println("쓰레드1이 자원2를 쓰려고 대기");
    
                    synchronized (object2){
                        System.out.println("쓰레드1은 자원2에 대하여 lock걸림");
                    }
                }
            }
        }
    
        private static class SecondThread extends Thread{
            @Override
            public void run() {
                synchronized (object2){
                    System.out.println("쓰레드2가 자원2에대하여 lock걸음");
    
                    try {
                        Thread.sleep(10);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println("쓰레드2는 자원1쓰려고 대기");
    
                    synchronized (object1){
                        System.out.println("쓰레느2는 자원1에 대해여 lock걸림");
                    }
                }
            }
        }
    }
    ```
    
4. 데드락 해결방안
    - 예방(Prevention) - 발생원인의 4가지중 하나라도 발생하지 않도록 시스템차원에서 미리 예방
        
                                    - 자원의 낭비가 심하다..
        
    - 회피(Avoidance) - 자원을 요구하는 시점에서 쓰레드가 자원을 할당해도 되는지 검사하여 데드락을 막는방법
        
                                  - 자원과 쓰레드의 수가 고정이여야하고 자원요청이 있을때마가 확인하는건 성능 부하..
        
    - 탐지(Detection)와 회복(Recovery) - 데드락이 발생되면 그때 복구로직을 통해 해결
    - 무시(Ignore) - 데드락이 발생되면 어쨋든 해결하는데 성능상 손해를 볼수 밖에 없음. 안정성과 성능을 고려하여 데드락 무시하는 경우
