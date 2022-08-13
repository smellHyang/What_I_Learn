# ISP(Interface Segregation Principle) : 인터페이스 분리 원칙

## 1. 인터페이스 분리원칙(ISP)

- 자신이 사용하지 않는 메소드에 의존하지 말아야한다.

## 2. 목적

- 시스템 내부 의존성을 약화시켜 리팩토링, 수정, 재배포 용이
- 사용하고자 하는 메소드만 구현하여 객체의 응집도 향상
- 불필요한 의존성 제거
- 기능에 의존하지 않도록 확장성을 고려

## 3. ISP를 위반한 예시

```java
public interface Bank {
    void doPersonalFinance();
    void doEnterpriseFinance();

    default String msg(String bankName, Duty duty) {
        return String.format("%s는 %s를 합니다.", bankName, duty.description());
    }
}

//doPersonalFinance업무는 하지만 doEnterpriseFinance업무는 X
public class HappyBank implements Bank {
    @Override
    public void doPersonalFinance() {
        System.out.println(this.msg(this.getClass().getSimpleName(), Duty.PERSONAL_FINANCE));
    }

    @Override
    public void doEnterpriseFinance() {
        //
    }
}

//doEnterpriseFinance업무는 하지만 doPersonalFinance업무는 X
public class UnhappyBank implements Bank {
    @Override
    public void doPersonalFinance() {
       //
    }

    @Override
    public void doEnterpriseFinance() {
        System.out.println(this.msg(this.getClass().getSimpleName(), Duty.ENTERPRISE_FINANCE));
    }

}
```

⇒ 인터페이스를 분리하여 사용

```java
public interface BankMessage {
    default String msg(String bankName, Duty duty) {
        return String.format("%s는 %s를 합니다.", bankName, duty.description());
    }
}

public interface BankPersonalFinance extends BankMessage {
    void doPersonalFinance();
}

public interface BankEnterpriseFinance extends BankMessage {
    void doEnterpriseFinance();
}

```

## 4. SRP와 ISP

- ISP를 만족하면 SRP도 만족하는가?
    - SRP는 “클래스”, ISP는 “클라이언트 기준으로 인터페이스 분리”
    - 이 말은 즉 하나의 여러 기능을 가진 인터페이스보다는 여러개의 구체적인 인터페이스를 사용하라는 의미이다.
    
    ```java
    class A implements featA, featB, featC{}
    ```
    
    - 다음과 같이 여러개의 인터페이스 위임 시 SRP원칙을 위반 할 수도 있는거 아닌가?
    - 하지만 인터페이스에서 위임한 모든 메소드를 구현하지 않고 필요한 메소드만 A클래스에서 구현한다면 SRP원칙을 맞는거라고 볼수있을거 같음 (해당 기능을 상속한 자식클래스 입장에서는..)
- SRP를 만족하면 ISP도 만족하는가?
    - 예를들어 CRUD메소드를 가진 게시판 클래스가 있다.
    - 일반사용자는 게시판 삭제기능이 없지만 관리자는 삭제가 가능하다.
    - 이 경우 게시판에 관련된 책임을 수행하므로 SRP는 만족
    - BUT 이 CRUD모든 메소드가 들어있는 인터페이스를 클라이언트 상관없이 사용한다면 ISP에 위배된다.

⇒ 상속은 풍성하게 인터페이스는 빈약하게..

<aside>
💡 두 클래스관계가 IS-A면 상속, 확장이면 위임(Implements)

</aside>
