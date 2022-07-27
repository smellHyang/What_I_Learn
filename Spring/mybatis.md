# mybatis

## 1. Mybatis란?

- 자바 객체와 SQL사이의 자동매핑을 지원하는 프레임워크
- JDBC를 통해 DB에 접근하는 작업을 캡슐화하고 일반 SQL쿼리, 저장 프로시저 및 고급 매핑을 지원하여 모든 JDBC코드 및 매개변수의 중복작업을 제거

## 2. 특징

- 복잡한 쿼리나 동적 쿼리에 강하다
- 프로그램 코드와 SQL쿼리 분리
- 쉬운 접근성과 코드의 간결함
    - JDBC의 모든 기능을 제공하여 JDBC의 중복 작업을 줄이고 깔끔한 소스 코드 유지
    - 수동적인 파라미터 설정과 쿼리 결과에 대한 맵핑구문을 제거
- VO 또는 도메인 객체로 개발이가능
- 다양한 프로그래밍 언어로 구현가능

## 3. 아키텍쳐

![image](https://user-images.githubusercontent.com/73684562/181252556-f775ab17-9d3d-4542-9649-9726949b1820.png)

- JDBC만 사용하는 어플리케이션은 Application Modules에서 JDBC Interfaces 를바로 호출하지만 JDBC API를 감싸서 개발자가 조금 더 편리하게 접근할 수 있도록 해준다.

## 4. 데이터 액세스

![image](https://user-images.githubusercontent.com/73684562/181252496-413ce8a1-6ebd-4a8a-84da-c9b06096c3e2.png)

- Controller → Service → DAO → Mybatis
