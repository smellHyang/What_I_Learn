# 의존성주입(Dependency Injection)

1. 의존성 주입이란? 
    - 외부에서 두 객체의 관계를 결정해주는 디자인패턴
    - new키워드 대신 객체를 생성 해준다.
    - 객체를 직접 생성하는게 아니라 외부에서 필요한 객체를 받아서 사용하는것.
    - 생성자 주입, 필드 주입, 수정자 주입 등등 있다.
    
2. WHY 필요한가..?
    
    ```java
    public class Introduce{
    
    	public void intro(){
    		//Teacher human = new Teacher(); // 나는 선생이다.
    		Student human = new Student(); //나는 학생이다.
    	
    		human.intro
    	}
    }
    
    ---
    
    public class Main{
    	public static void main(String[] args){
    		Introduce intro = new Introduce();
    		intro.intro();
    	}
    }
    ```
    
    - 특정 클래스가 제 기능을 다하기 위해, 다른 클래스의 생성을 필요로 하는 경우 클래스 간의 의존성이 존재한다고 표현한다.
    - Introduce 클래스는 human 패키지 내에 있는 Teacher, Student 클래스의 의존하고있고 따라서 클래스간 결합력이 강하다. → 값이 바뀔때마가 수정해야한다.
    - 의존도와 결합도를 낮추고 유연성을 확보하기 위해
        
        → 소프트웨어에서는 기능이 추가될때마다 매번 코드를 변경하고 다시 컴파일하는데 비용이 많이 든다. 이처럼 코드의 변경을 최소화하기 위해서는 필드, 게터세터, 생성자 등으로 의존성을 
        
3. 특징 
    - 소스 변경 x
    - 의존 클래스의 구현이 완성되지 않더라고 테스트를 할 수 있다.
    
4. 의존성 주입의 종류
    - 필드 주입(Field Injection)
        
        ```java
        @Component
        public class SampleComponent {
        
            @Autowired
            private FieldService fieldService;
        }
        ```
        
        - 단일책임 원칙(SRP) 위반
            
            → 개수 제한 없이 무한정 추가하게 되면 class가 할게 많아진다.
            
        - 의존성이 숨는다
            
            → 외부에서 해당 클래스가 어떤 의존성 책임을 가지고 있는지 알 수 없다.
            
        - 불변성 활용 불가
            
            → 필드 주입은 final을 선언 할 수 없다.
            
        - 컴파일 단계에서 순환의존성을 알 수 없다.
        
        <aside>
        💡 순환의존성? (A class → B class, B class → A class), (A class → B class, B class → C class, C class → A class) *→ : 참조
        
        </aside>
        
        ⇒ 읽기 쉽고 사용이 용이하지만 컨테이너 말고는 외부에서 주입할 수 없다. 
        
    - 수정자 주입(Setter Injection)
        
        ```java
        @Component
        public class SampleComponent {
            private SetterService setterService;
         
        		@Autowired
            public void setSetterService(SetterService setterService) {
            	this.setterService = setterService;
            }
        }
        ```
        
        - 런타임 시에 할 수 있어 결합도가 낮다.
        - NullPointerException 발생 가능성
            
            → service구현체를 주입하지 않아고 controller객체 생성이 가능하다.(내부의 service 메소드 호출 가능) 따라서 service 구현체를 주입해주지않아도 set에 접근이 가능하여 NullPointerException이 발생할 수 있다.
            
    
    - 생성자 주입(Constructor Injection)
        
        ```java
        @Component
        public class SampleComponent {
            private SampleDAO sampleDAO;
         
            @Autowired
            public SampleService(SampleDAO sampleDAO) {
                this.sampleDAO = sampleDAO;
            }
        }
        
        @Component
        public class SampleController {
        
        	private final SampleService sampleService = new SampleService(new SampleDAO());
            
        	...
        }
        ```
        
        - NullPointerException발생 가능성을 막는다
            
            → 의존선 주입을 하지 않은 경우에는 controller 객체를 생성 할 수 없다.
            
        - 불변성 활용(final)
            
            →  누군가가 controller내부에서 service 객체를 바꿔치기 할 수 없다.
            
        - 컴파일 단계에서 순환의존성을 알 수 있다.
        - 단일 책임 원칙(SRP)원칙
            
            → 생성자의 인자가 많아지고 코드가 길어지면 사용자로 하여금 다시 생각하게 된다. 
            
5. Spring에서 어떤 기능을 통해 DI가 실행되는가?
    - Bean
        - 스프링 컨테이너가 관리하는 자바객체를 bean이라고한다.
        - 코드 상에서는 ApplicationContext인터페이스 이다.
        - 컨테이너 안에 빈 객체가 있어서 등록 요청을 하면 bean 저장되고 이를 사용한다.
        
        ![Untitled](%E1%84%8B%E1%85%B4%E1%84%8C%E1%85%A9%E1%86%AB%E1%84%89%E1%85%A5%E1%86%BC%E1%84%8C%E1%85%AE%E1%84%8B%E1%85%B5%E1%86%B8(Dependency%20Injection)%207e711e9ba7f046abbefb7ba908dfa4b0/Untitled.png)
        
    
    +)  [스프링 컨테이너(Container)](%E1%84%89%E1%85%B3%E1%84%91%E1%85%B3%E1%84%85%E1%85%B5%E1%86%BC%20%E1%84%8F%E1%85%A5%E1%86%AB%E1%84%90%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%82%E1%85%A5(Container)%20b8d6948ef8ae42b2967326b948ada1bc.md)
