# OCP(Open-Closed Principle) : 개방-폐쇄 원칙

## 1. 개방폐쇠 원칙(OCP)

- 확장에는 열려있고 수정에는 닫혀있어야 한다.
- 어플리케이션 변경 시 모듈의 기능을 확장할수는 있지만 이에대한 소스코드는 변경하지 않는다.

## 2. 목적

- 하나의 변화가 다른곳에 연쇄적으로 일으키는 영향을 방지하기 위함
- 수정사항이 발생하였을때 이미 설계된 모듈에서의 수정을 적게하기 위함
- 코드의 재사용성 용이

## 3. 예시

![image](https://user-images.githubusercontent.com/73684562/183253926-804f98da-b034-4959-af1f-4ef02b0f5c18.png)


- JDBC매니저는 상속을 통해 PostgreSQL, Oracle, Sybase에서 확장할 수 있지만  JDBC매니저소스를 수정하지는 않는다.
- **추상화 (interface)**를 통해 기능을 고정시킨다.
- **상속 (다형성)**: 상위 클래스의 기능을 그대로 사용하면서 하위클래스에서 오바라이딩하여 일부 구현을 제공(확장)

## 4. OCP를 지키지 않은예시

- 다운캐스팅
    
    ```java
    public void drawCharacter(Character character) {
      if(character instanceof Missile) {  // 타입 확인
        Missile missile = (Missile) character; // 타입 다운 캐스팅
        missile.drawSpecific();
    
      } else {
        character.draw();
      }
    }
    ```
    
    - instanceof를 통해 파라미터 타입이 Missile일 경우 별도로 처리한다.
    - 이 경우에 Character클래스가 확장될떄 같이 수정해주어야하므로 변경에 닫혀 있지 않다.
    
    ⇒ 추상화를 통해 Character타입에 추가해 주어야한다.
    
- if-else블록이 존재
    
    ```java
    public class Enemy extends Character {
      private int pathPattern;
      public Enemy(int pathPattern) {
        this.pathPattern = pathPattern;
    
      }
    
      public void draw() {
        if(pathPattern == 1) {
          x += 4;
    
        } else if(pathPattern == 2) {
          y += 10;
    		...
    }
    ```
    
    - 경로 추가 시 Enemy 클래스가 닫혀 있지 않다
    
    ⇒ 경로패턴을 추상화하고 Enemy클래스에서 추상화 타입을 사용한다.
