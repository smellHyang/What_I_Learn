# PassByValue/ PassByReference

1. Pass By Value( Call by Vaule ) 
    - 값에 의한 호출
    - 메모리에 저장된 값을 stack영역에 복사하여 새로운 지역변수에 저장한다. → 값이 보존된다.
    - 기본형(Primitive type)
2. Pass By Reference( Call by Reference ) 
    - 참조에 의한 호출
    - 값을 사용할때 새로운 레퍼런스를 생성하여 호출한다.
    - 힙 영역에 같은 주소를 공유하는 변수 이기때문에 값이 보존되지 않는다.
    
3. 자바는 왜 pass by reference를 사용했을까?
    - 자바에서는 c언어와 달리 메모리를 사용자가 직접관리하지 않는다. 자바의 heap영역 안에 있는 가비지 컬렉터가 올드한데이터를 지워가면서 스스로 메모리 관리를 하기때문에.. 메모리 관리 측면에서 pass by reference..라고한다.