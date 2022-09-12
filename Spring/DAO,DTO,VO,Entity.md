# DAO,DTO,VO,Entity

## DAO(Data Access Object)

- 직접 DB의 data에 접근하기 위한 객체 (비즈니스 로직 분리)
- Service와 DB를 연결하는 역할
- SQL을 사용하여 db에 접근하고 CRUD API 제공

## DTO(Data Transfer Object)

- 특정 테이블 정보를 레코드 단위로 정의해 놓은 클래스(비동기처리)
- 로직을 갖지않는 순수한 데이터 객체
- Service와 Controller 사이에서 사용하는 데이터 교환 객체
- getter/setter
- Layer간 통신 용도로 오고가는 객체

```java
public class PersonDTO {
	private String name;
	private int age;
public String getName() {
	return name;
	}
public void setName(String name) {
	this.name = name;
	}
public int getAge() {
	return age;
}
public void setAge(int age) {
	this.age = age;
	}
}

```

## VO(Value Object)

- DTO와 동일한 개념이지만 ReadOnly(불변클래스)
- getter만 존재
- 틀정한 비즈니스 값을 담는 객체
- 서로 다른 이름을 갖는 VO 인스턴스더라도 모든 속성 값이 같다면 두 인스턴스는 같은 객체라고 할 수 있다.(equals(), hashcode())

## Entity

- 실제 DB의 테이블과 매칭될 클래스
- 해당 클래스 안에서 필요한 로직 메소드를 구현한다.(도메인 로직)

## Entity와 DTO를 분리하는 이유

- view와 DB layer의 역할을 분리하기 위해
- entity가 변경되면 여러 클래스에 영향을 끼친다. 하지만 dto는 자주 변경되므로 분리해야한다.

## 전체구조
![image](https://user-images.githubusercontent.com/73684562/189629600-f025f145-3332-4126-9e7a-8dee29e3f910.png)
