# CheckedException과 UnCheckedException의 차이

![image](https://user-images.githubusercontent.com/73684562/184525094-bf4dae88-7c0e-4101-a566-266c404f68d6.png)

|  | Checked Exception | UnChecked Exception |
| --- | --- | --- |
| 확인시점 | 컴파일 시점 | 런타임시점 |
| 처리여부 | 예외처리 | 하지 않아도 된다. |
| 트랜잭션 처리 | 복구가 가능하여 rollback X | rollback O |
| 종류  | IOException, ClassNotFoundException… | NullPointerException, 
ClassCastException.. |
- 예외 복구 전략이 명확하면 Checked Exception을 try-catch로 잡아서 예외복구
- 그렇지 않다면 Unchecked Exception을 발생시키고 예외에 대한 메시지를 명확히 전달

## 2. 예외처리 방식

- 예외 복구
    - 예외상황을 파악하고 문제를 해결하여 정상상태로 돌려놓는방법
- 예외처리 회피
    - 예외처리를 하지않고 호출한쪽으로 던져 회피
- 예외 전환
    - 메서드 밖으로 예외를 던지지만, 그냥 던지지 않고 적절한 예외로 전환해서 넘기는 방법
    - ```java
// 조금 더 명확한 예외로 던진다.
public void add(User user) throws DuplicateUserIdException, SQLException {
    try {
        // ...생략
    } catch(SQLException e) {
        if(e.getErrorCode() == MysqlErrorNumbers.ER_DUP_ENTRY) {
            throw DuplicateUserIdException();
        }
        else throw e;
    }
}
```
