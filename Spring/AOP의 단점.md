# AOP 단점

- 클래스 내부에서 내부함수호출로는 aop가 동작하지 않는다
    - aop는 proxy로 동작하기 때문이다.
    
    ```java
    @Service
    public class CalculatorService {
        @BeforeStdoutAop
        public int plus(int x, int y) {
            minus(x,y);
            return x + y;
        }
    
        @BeforeStdoutAop
        public int minus(int x, int y) {
            return x - y;
        }  
    }
    //결과 beforecall() 한번만 호출
    ```
    
- 디버깅 난이도 이슈

→ 공통모듈을 미리 만들어놓고 중간중간 끼워넣는건데 스프링에서는 어노테이션을 넣어놓으면 어노테이션이 구현된쪽으로 가게된다 그래서 aop를 내가 어느시점에 어떻게 하라고 구현해 놓아서 의도한대로 진행이 되지 않을 수 있다.
