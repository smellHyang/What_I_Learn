# SRP(Single Responsibility Principle) : 단일 책임 원칙

## 1. 단일책임원칙(SRP)

- 하나의 클래스는 하나의 기능만을 수행해야한다.
- 단일 책임 원칙을 지키지 않으면 특정기능 수정 시 여러 클래스를 수정해야한다.

## 2. 장점

- 테스트 용이 : 테스트케이스가 줄어든다
- 낮은 결합도 : 클래스의 기능이 적어져 종속성이 줄어든다.
- 쉬운 검색 : 작고 잘 조직된 클래스는 모놀리식 클래스보다 검색에 용이
- 쉬운 구현 : 하나의 기능만 가지고 있어 구현 및 이해가 쉽다.

## 3. 예시

- SRP를 지키지 않은 예시

```java
//사용자 도메인은 사용자 정보를 저장, 변경의 책임이 있지만, 
//이메일의 유효성을 검사하거나 이메일을 전송하는 책임을 가질 필요는 없다.
//사용자의 클래스가 하나의 기능만을 가지고 있지 않음
public class User {
    private static Pattern EMAIL =
    Pattern.compile("^[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]{2,3}$");
    private Long id;
    private String name;
    private String email;

    public User(Long id, String name, String email) {
        validateEmail(email);
        this.id = id;
        this.name = name;
        this.email = email;
    }

    private void validateEmail(String email) {
        if(!EMAIL.matcher(email).matches()) {
            throw new IllegalArgumentException("이메일 형식이 아닙니다.");
        }
    }

    public void sendMail() {
        System.out.println("send Mail by" + email);
    }
}
```

- 객체가 하나의 책임을 갖도록 클래스를 분리
```java
//유저 담당
public class User {
    private Long id;
    private String name;
    private Email email;

    public User(Long id, String name, Email email) {
        this.id = id;
        this.name = name;
        this.email = email;
    }
}    

//이메일 담당
public class Email {
    private final String email;

    public Email(String email) {
        validateEmail(email);
        this.email = email;
    }

    private void validateEmail(String email) {
        if (!EmailString.isValidEmailString(email)) {
            throw new IllegalArgumentException("이메일 형식이 아닙니다.");
        }
    }

    public void sendMail() {
        System.out.println("send Mail by" + email);
    }
}
```
