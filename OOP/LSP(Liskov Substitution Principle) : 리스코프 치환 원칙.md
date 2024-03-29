# LSP(Liskov Substitution Principle) : 리스코프 치환 원칙

## 1. 리스코프 치환 원칙(LSP)

- 특정메소드가 상위타입의 객체를 인자로 사용할때, 그 타입이 하위타입도 문제없이 동작해야한다.

```java
public int calculate(final Item item) {
	return item.calculate();
}
```

- 상위타입이 Item이고 하위타입이 Apple이면, item대신 apple을 넘겨줘도 잘 동작해야한다.

## 2. 목적

- 자식클래스와 부모클래스의 일관성으로 개발자간 소통 위반 방지
- 잘못된 LSP원칙으로인한 하위클래스의 오동작 방지

## 3. LSP를 위반한 예

- 자식클래스가 **오버라이딩**을 잘못한 경우
    - 자식클래스가 부모클래스의 변수타입, 파라미터, 리턴값타입 및 개수를 변경하는 경우
    - 자식클래스가 부모클래스의 의도와 다르게 오버라이딩하는 경우

⇒ 변수타입, 파라미터, 리턴값타입 및 개수 모두 부모클래스의 형식과 일치

⇒ 부모클래스의 행동 규약을 위반하지 않는다.
