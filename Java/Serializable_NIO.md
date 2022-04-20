# Serializable/NIO

1. Serializable
    - 생성한 객체를 저장/읽기, 저장한 객체를 읽기, 객체를 다른서버에 보내거나 받기
    - JVM에서 해당객체를 저장하거나 다른서버로 전송할 수 있게 해준다
        
        
    
    ```java
    static final long serialVersionUID = 1L;
    ```
    
    - 반드시 static final long serialVersionUID 으로 선언해주어야한다.
        
        → 해당객체를 명시하는 역할
        
    - serialVersionUID를 통해 각 서버거 해당객체를 같은지 다른지 확인할 수 있다
        - 클래스이름, 변수개수, 타입 모두 같아야 한다. (다르면 예외발생)
        - Serializable인터페이스를 사용하면 자동으로 serialVersionUID가 생성된다 .
        - 객체가 변경되면 다시 컴파일하여 serialVersionUID를 생성한다.
        - 명시적으로 serialVersionUID를 생성하고 객체를 변경하는것은 권장하지 않는다 (예외가 발생하지 않기때문에 어디서 틀렸는지 찾기어려움)
    - transient 예약어는 Serializable 대상에서 제외(e.g. 패스워드 전송 시 제외하여 전송)
    
2. NIO(New IO)
    - 속도때문에 생겨났다.
    - 스트림을 사용하지 않고 Buffer와 Channal을 사용한다.
