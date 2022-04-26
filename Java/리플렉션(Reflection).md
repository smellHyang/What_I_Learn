# 리플렉션(Reflection)

1. 리플렉션? 런타임 시 객체를 통해 클래스의 정보를 얻는 기능  (구체적인 클래스 타입을 알지 못해도 그 클래스의 메소트, 타입, 변수들을 접근 할수 있도록하는 Java API)
    
    ```java
    public class Foo{
    	public void getFoo(){
    		//code
    	}
    }
    
    public class Main{
    	public static void main(String[] args){
    		Object foo = new Foo();
    		foo.getFoo();//컴파일에러
    	}
    }
    ```
    
    → 모든클래스의 조상클래스인 Object타입으로 Foo클래스의 인스턴스를 담을수 있지만 Object의 메소드, 변수만 사용가능하기 때문에 에러 발생
    
    - 설계할때 어떤 타입의 클래스를 사용할지 모를수 있으니 일단 코드를 작성하고 런타임 시점에서 확인하여 사용
    
2. 동작방식
    - 자바 클래스 파일은 바이트코드로 컴파일되어 Static 영역에 위치한다. 때문에 클래스 이름만 알고있다면 static 영역에 있는 클래스 정보를 가져올수있다...?
    
3. 왜 사용하는가..?
    - 자바는 컴파일시점에 타입을 결정하는 정적인 언어라 동적인 문제를 해결하기 부족하다 따라서 런타임 시점에 타입을 결정하는 동적인 보완성을 주기위해
    
4. 사용방식
    
    ```java
    class Article {
       private int id;
       private String title;
       private LocalDateTime date;
    }
    
    Class<?> clazz = Article.class;  // Article의 Class를 가져온다.
    Field[] fields = clazz.getDeclaredFields(); // Article의 모든 필드를 가져온다.
    
    for (final Field field : fields) { // field의 type, name 출력
        System.out.printf("%s %s\n", field.getType(), field.getName());
    }
    ```
    
    ```java
    //출력결과
    int id
    class java.lang.String title
    class java.time.LocalDateTime date
    ```
    
5. 주의
    - 이미 인스턴스 만들었음에도 불구하고 남용하는건 성능이슈를 불러올 수 있다.
    - 컴파일시 확인되지않고 런타임 시 동적으로 정보를 가져오기때문에 jvm에 최적화 xxx
    - 접근할 수 없던 접근제어자에 접근하기때문에 내부 노출이 발생되면서 추상화가 깨질 수 있다.
    
6. 활용
    - 프레임워크, 라이브러리 - 사용자가 어떤클래스를 만들지 예측하기 어렵기 때문에 동적으로 해결(확장성)
    - Spring Container,BeanFactory - 런타임에 객체가 호출 될떄 동적으로 객체의 인스턴스를 생성
    - Spring Data JPA - 생성자의 인자정보를 리플렉션이 가져오기 못하기 때문에 Entity에서 기본생성자가 필요한 이유. 기본생성자로 개게 생성만 하면 그 외 정보는 리플렉션으로 확보가능
