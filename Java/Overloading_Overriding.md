# Overloading/Overriding

1. 오버로딩(Overloading)
    - 한 클래스 내에서 같은 이름의 메소드를 매개변수 개수 또는 타입을 다르게 해서 사용하는 것
    - 접근제어자 자유롭게 지정가능(public, default, protected, private)
    
    ```jsx
    class OverloadingTest {
    
    	public static void main(String[] args) {
    		OverloadingMethods om = new OverloadingMethods();
    
    		om.print();
    		om.print("오버로딩2");
    		om.print(3);
    		System.out.println(om.print(4));
    		System.out.println(om.print(5, 5));
    	}
    }
    
    class Overloading {
    
    	//1. 매개변수 타입이 다른경우
    	public void print() {
    		System.out.println("오버로딩1");
    	}
    	public void print(String a) {
    		System.out.println(a);
    	
    	public void print(Integer a) {
    		System.out.println(a);
    	}
    
    	// 매개변수 개수가 다른경우
    	String print(Integer a) {
    		return a.toString();
    	}
    	String print(Integer a, Integer b) {
    		return a.toString() + b.toString();
    	}
    
    }
    ```
    
    <결과>
    
    ```java
    오버로딩1
    오버로딩2
    3
    4
    55
    ```
    

- 사용 이유
    - 같은기능의 메소드를 중복하지 않아도 하나의 이름으로 사용 가능

1. 오버라이딩(Overriding)
    - 부모클래스의 메소드를 자식클래스에서 재정의 하는것
    - 자식클래스에서 재정의 할때 메소드의 이름, 매개변수, 리턴값 모두 같아야한다.
    
    ```java
    public class OverridingTest {
    
    	public static void main(String[] args) {
    		Animal animal = new Animal();
    		Cat cat = new Cat();
    		Dog dog = new Dog();
    		
    		animal.makeNoise(); //bark
    		cat.makeNoise(); //Meow
    		dog.makeNoise(); //Woof Woof
    	}
    }
    
    class Animal {
    	void makeNoise() {
    		System.out.println("bark");
    	}
    }
    
    class Cat extends Animal {
    	protected void makeNoise() {
    		System.out.println("Meow");
    	}
    }
    
    class Dog extends Animal {
    	public void makeNoise() {
    		System.out.println("Woof Woof");
    	}
    }
    ```
    
    - 자식클래스에서 접근제어자 ≥ 부모클래스 접근제어자 (범위)
    - 자식클래스에서 부모클래스보다 더 큰범위의 예외를 설정할 수 없다.
    - static메소드로 정의한것은 그대로 static으로 사용해야한다.
    
    1. Overloading  VS Overriding 비교
        
        
        |  | 오버로딩(Overloading) | 오버라이딩(Overriding) |
        | --- | --- | --- |
        | 접근제어자 | 자식클래스 ≥ 부모클래스 | 모든 접근제어자 사용가능 |
        | 리턴형 | 같은 리턴형 | 달라도된다. |
        | 메소드명 | 동일 | 동일 |
        | 매개변수 | 동일 | 달라야한다. |
        | 적요범위 | 상속관계 | 같은 클래스 |
