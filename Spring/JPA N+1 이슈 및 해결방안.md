# JPA N+1 이슈 및 해결방안

## 1. JPA N+1?

- 1번의 JPA쿼리를 날렸을 때 의도치 않게 N번의 쿼리가 추가적으로 실행되는 경우
- 1: N 구조에서 주로 발생(EX. USER-BOARD)

### 발생 경우

- 즉시로딩(EAGER)
    - JPA에서 Fetch전략을 가지고 해당 데이터의 연관관계인 하위 엔티티를 추가로 조회
    - 2번의 과정으로 N+1 문제 발생
- 지연로딩(LAZY)
    - JPA에서 Fetch전략을 가지지만, 지연로딩이기 때문에 추가 조회 x
    - 하위 엔티티를 가지고 작업하게 되면 추가 조회가 발생하여 N+1 문제 발생

### 발생 예시(User : 1, Board: N)

```java
@Entity
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(length = 10, nullable = false)
    private String name;

    @OneToMany(mappedBy = "user", fetch = FetchType.EAGER)//즉시로딩
		@OneToMany(mappedBy = "user", fetch = FetchType.LAZY) //지연로딩
		private Set<Article> articles = emptySet();
```

```java
@Entity
public class Article {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(length = 50, nullable = false)
    private String title;

    @Lob
    private String content;

    @ManyToOne(fetch = FetchType.EAGER)//즉시로딩
		@ManyToOne(fetch = FetchType.LAZY) //지연로딩
		private User user;
```

- 즉시로딩
    
    ```java
    @Test
    @DisplayName("Eager type은 User를 단일 조회할 때 join문이 날아간다.")
    void userSingleFindTest() {
    
    	User user = userRepository.findById(1L)
    		.orElseThrow(RuntimeException::new);
    }
    ```
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dc544d39-654a-4d7d-8dac-69f89818c61f/Untitled.png)
    
    - findById 메소드는 EntityManager에서 PK값을 찍어서 사용하기 때문에 JPA가 내부적으로 Join문을 사용
    - 내부적으로 inner join문이 발생하면서 User가 조회되면서 Board까지 즉시로딩된다.
    - 즉시로딩을 Article에 걸어두었기 때문에 User는 조회해도 JPA는 EAGER이 걸려있는 Article까지 모두 조회(N+1)
    
- 지연로딩
    
    ```java
    @Test
    @DisplayName("Lazy type은 User 검색 후 필드 검색을 할 때 N+1문제가 발생한다.")
    void userFindTest() {
        List<User> users = userRepository.findAll();
    }
    ```
    
    - 지연로딩은 해당 연결 entity(Article)에 대해서 프록시로 걸어두고, 사용 시 쿼리문을 날린다.
    - 처음 find 할때는 N+1이 발생하지 않지만 추가로 User 검색후 User의 Article을 사용한다면 이미 캐싱된 User의 Article 프록시에 대한 쿼리 발생(N+1)
    

## 2. 해결책

### Fetch Join

- 두 테이블의 join쿼리를 직접 작성

```java
@Query("select distinct u from User u join fetch u.articles")
List<User> findAllJPQLFetch();
```

- 단점
    - 쿼리 한번에 모든 데이터를 가져오기 때문에 JPA가 제공하는 Paging API 사용 불가능(인메모리에서 모든값을 다 가져오기때문에)
    - 1: N 관계가 2개 이상인 경우는 사용 불가
    - 패치 조인 대상에게 별칠 부여 불가능
    - 쿼리문 작성의 복잡성

### Entity Graph 사용

- JPQL을 사용해 쿼리를 작성하고 필요한 연관관계를 EntityGraph에 설정

```java
@EntityGraph(attributePaths = {"articles"})
@Query("select distinct u from User u join u.articles")
List<User> findAllEntityGraph();
```

## 3. 주의사항

- Fetch Join 과 EntityGraph는 카티시안 곱이 발생하여 중복이 생김

<aside>
💡 Cartesian Product? join조건을 적지 않았을때 두 테이블 모두 곱함

</aside>

### DISTINCT

- JPQL에 distinct를 추가하여 중복제거

```java
@Query("select distinct u from User u join fetch u.articles")
List<User> findAllJPQLFetch();

@EntityGraph(attributePaths = {"articles"})
@Query("select distinct u from User u join u.articles")
List<User> findAllEntityGraph();
```

### Set

- Set은 중복을 허용하지 않는다.
- 단, 순서도 보장x(순서보장 필요시 LinkedHashSet)

```java
@OneToMany(mappedBy = "user", fetch = FetchType.EAGER)
private Set<Article> article= new LinkedHashSet<>();
```

- 참고
