## 서블릿 Context란?

- 하나의 서블릿이 서블릿 컨테이너와 통신하기 위해 사용되어지는 메소드를 가지고 있는 클래스

<aside>
💡 서블릿 ? 웹페이지를 동적으로 생성하는 서버측 프로그램

</aside>

## 2. 서블릿 컨텍스트 기능

- 서블릿에서 파일 접근
- 자원 바인딩
- 로그파일
- 컨텍스트에서 제공하는 설정 정보 제공

## 3. 서블렛 컨텍스트 특징

- 서블릿과 컨테이너간의 연동
- 컨텍스트(웹 어플리케니션) 마다 하나의 servletContext가 생성
- 서블릿끼리 자원을 공유하는데 사용
- 컨테이너 실행 시 생성되고 컨테이너 종료 시 소멸된다.

## 4. 서블릿 컨테이너(톰캣..)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bcf48195-cfc1-4b68-a220-10080d30bfa3/Untitled.png)

- 서블릿들을 관리하는 공간
- 웹서버와의 통신 지원
- 서블릿 생명주기 관리
- 멀티쓰레드 지원 및 관리
    - 요청이 올때마다 쓰레드 생성 및 소멸
- 선언적인 보안관리

## 5. 동작 원리

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5a30ac62-36ba-4ca5-806c-4ac2d75ccb28/Untitled.png)

- 클라가 서버에 요청
- 웹에서 정적인 콘텐츠를 처리하고 동적인 콘텐츠는 컨테이너로 전달
- 컨테이너는 요청에 대해 HttpServletRequest와 HttpServletRequest를 생성
- 어떤 서블릿에 대한 요청인지 알아내고 쓰레드에 서블릿을 할당 후 실행(Request와 Response를 인자로 넘김)
- 서블릿 service()를 호출하고 http메소드에 따라 doGet(), doPost() 등을 호출
- 서블릿은 Reponse객체에 실어 응답
- 컨테이너는 사용했던 request, reponse객체를 소멸(gc가 처리)

## 6. 단점

- 프로그램 내에서 html을 처리하기 때문에 간단한 태그를 변경할떄 조차 재컴파일 해야한다.

+) JSP - html내 자바소스

Servlet - 자바 소스 내 html 

---

---

## 1. 스프링 컨텍스트(Application Context)?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8d0206f7-bb43-4e3b-9524-047604b91a61/Untitled.png)

- 컨테이너에서 하는 빈의 생성과 관계설정 외에 추가적인 기능을 하는 인터페이스
- 여러 서블릿에서 공통으로 사용할 빈을 등록하는 contextdlek.

## 2. 역할

- POJO클래스
    - 환경과 기술에 종속되지 않고 필요에 따라 재활용 할 수 있는 방식으로 설계된 Object(OOP에 충실)
- 설정 메타정보
    - IoC컨테이너가 제어할 수 있도록 적절한 메타 정보를 제공
    - IoC컨테이너가 관리하는 빈 객체를 어떻게 만들고 어떻게 동작할 것인지에 대한 정보
    - DI로 연결되는 오브젝트가 모여서 하나의 어플리케이션을 구성하고 동작하게 만듬

## 3. 동작 원리

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c3740786-fa61-4793-ab91-77f3654ffe45/Untitled.png)

- 컨텍스트는 @Configuration이 붙은 클래스들을 설정 정보에 기록해 주고 @Bean이 붙은 메소드의 이름으로 bean목록을 생성한다.
- 클라이언트가 해당 bean을 요청한다
- 컨텍스트는 자신의 bean 목록에서 요청한 이름이 있는지 찾는다
- 설정클래스로부터 bean생성을 요청하고 있다면 @Bean을 호출하여 객체를 생성하고 돌려준다.

## 4. 구조

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/da625eb2-64b0-463b-a3c3-7f79961114ab/Untitled.png)

- 빈을 생성하는 BeanFactory 최상위 인터페이스를 상속받음
- BeanFactory는 1개의 빈을 찾기 위한 메소드를 가지고 있음
- ApplicationContext는 BeanFactory직속으로 상속받지않고 중간에 ListableBeanFactory, HierarchicalBeanFactory를 상속받기 때문에 bean리스트 처리, 계층관계 설정하는 기능을 가지고 있다.
- ApplicationContext의 인터페이스로 AutowireCapableBeanFactory를 가지고 있어서 DI를 처리할 수 있다. (@Autowired 처리)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a3585e5b-dadd-47e4-b4bf-b6071c6ad80f/Untitled.png)

- ContextLoaderListener를 이용하여 root-context를, DispatcherServlet를 이용하여 servlet-context를 생성
- Root-Context
    - 이에 등록 된 bean들은 모든 context에서 사용가능(공유ooo)
    - service, dao를 포함한 웹 환경에 독립적인 빈을 담아둠
    - 서로 다른 servlet-context에서 공유해야하 하는 빈을 등록하고 사용할 수 있다.
    - servlet-context 내 빈들은 사용XXX
- Servlet-Context
    - 이 에 등록된 빈들은 해당 context에서만 사용 가능(공유XXX)
    - DispatcherService가 직접 사용하는 웹 관련 bean을 등록하는 데 사용(Controller)
    - 독자적인 context를 가지며 , root-context 내 bean사용 OOO
    

## 5 . 특징

- 장점
    - 클라이언트는 @Configuration이 붙은 구체적인 팩토리 클래스를 알 필요가 없다
        - 팩토리가 많아져도 일관된 방식으로 원하는 bean을 가져올 수 있기 때문에 어떤 팩토리에 접근해야하는지 몰라도 된다.
    - 종합 IoC서비스를 제공해준다.
        - 객체가 만들어지는 방법, 시점, 전략이 다르고 후 처리 및 조합같은 다양한 기능을 제공한다.
    - 다양한 bean 검색 방법 제공
        - 빈목록을 관리하여 bean을 찾을 수 있다. 이러한 bean을 직접 착는 방식을 의존성 검색이라고 한다.
