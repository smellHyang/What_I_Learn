# Deep Copy와 Shallow Copy에 대해 설명해주세요.

![image](https://user-images.githubusercontent.com/73684562/185116706-1733219f-39f0-4134-9639-c0d5957e1a4c.png)

## 1. Deep Copy

- 데이터 자체를 복사
- 복사된 두 객체는 독립된 메모리를 차지(heap영역)
- 보통 primitive type에서 사용
- 데이터의 기존값은 유지할고 변하게 하지 않을떄 사용 → 가변객체 변경에 대해 안전
- 구현방식
    - 복사생성자 및 복사 팩토리 이용
    - 직접 객체를 생성하여 복사
    - Cloneable인터페이스를 구현하여 clone함수를 오버라이딩하여 복사

## 2. Shallow Copy

- 최소한의 복사
- 인스턴스가 메모리에 생성되지 않음 → deep copy보다 빠름
- 주소값을 복사(stack영역)하여 같은 메모리를 가리킨다. → 값이 바뀜
- 주로 reference type에서 사용

### +) clone 메소드

- 기본적으로 clone메소드는 shallow copy
- Cloneable 인터페이스구현하여 clone 메소드 사용 시 deep copy
- Serializable, deserialize 인터페이스 사용 시 deep copy

- 참고
- https://www.baeldung.com/java-deep-copy
