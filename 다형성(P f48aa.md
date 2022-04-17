# 다형성(Polymorphism)

1. 상속

- 상속? 부모 클래스의 (멤버)변수 및 클래스를 자식클래스가 사용할수 있다.

                자식클래스에서는 추가로 변수 및 클래스를 사용할 수 있다. 

- 상속 클래스 선언방식

```java
class Parent { }
 
class Child extends Parent { }
```

- 단일상속이어야 한다.

       why? 여러개의 부모클래스에서 같은 이름의 메소드가 존재할 경우 자식 클래스는 분별할 수 없음

- 오버라이딩(Overriding)?
    
    부모클래스의 메소드를 상속 받아 자식클래스에서 같은 메소드를 재정의하는 것
    
1. 다형성이란?
- 하나의 객체가 여러타입을 가질수 있는것
- 다형성 기법
    - 업캐스팅/다운캐스팅

```java
public class Animal { //부모클래스
	public Animal() {}
	public void breath() {}
}

public class Bird extends Animal { //자식클래스
	public Bird() {}
	public void fly() { System.out.println("fly") }
}

public class Polymorphism {
    public static void main(String[] args) {
        
				Animal animal1 = new Bird();
				animal1.fly(); //fly
				// 업캐스팅 : 하위 클래스에만 속한 메소드의 접근권한만 제어하는것 

				Bird bird1 = new Animal();
				bird1.fly(); //컴파일 에러!!!	
				//부모클래스가 추상클래스이거나 인터페이스일경우 미완성일수 있기에 불확실함

				Animal animal2 = new Bird(); //인스턴스가 업캐스팅됨(자식->부모클래스)
				Bird bird2 = (Bird)aniaml2; //(자식->부모클래스) -> 자식클래스
				bird2.fly(); //fly
				//다운캐스팅 : 업캐스팅된 클래스만을 다운캐스팅의 대상으로함
	
				
    }
}
```

- 매개변수를 이용한 다형성 구현

```jsx
class Product { int price; } //부모클래스
 
class Tv extends Product { } //부모클래스(Product)를 상속받은 자식클래스(Tv)
class Computer extends Product { } //부모클래스(Product)를 상속받은 자식클래스(Computer)
 
class Buyer { 
	int money = 1000; 
	void buy(Tv t) { money = money - t.price; }
  void buy(Computer c) { money = money - c.price; }
	// 오버로딩 기법으로 buy메소드를 중복으로 사용하여 구현

  void buy(Produc p) { money = money - p.price; }
  // 부모 클래스인 Product의 변수가 하위 클래스인 Tv, Computer클래스의 인스턴스를 참조하여 다형성 표현
}
```

1. 다형성의 효과?
- 하나의 타입으로 다양한 실행결과를 얻을수 있다.
- 객체를 부품화하여 유지보수가 용이하다. (재활용의 개념) → 상위클래스 에서는 공통적인 부분만 담당하고 하위클래스에서 추가요소를 덧붙여 쉽게 확장간