# Static

## 1. 개념

- static 변수와 static 메소드 → 정적 멤버(클래스 멤버)
- 객체에 소속된 멤버가 아니라 클래스에 고정된 멤버
- 메모리에 한번 할당되어 프로그램 종료 시까지 그대로 존재
- 모든 객체가 메모리를 공유한다.

[https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8786a918-7349-49a5-83a0-8e2b1fa4ec6b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220722%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220722T090110Z&X-Amz-Expires=86400&X-Amz-Signature=b66ed9fe16393aa1fe7f3f823dee1afdc6dd54bd22de6eb5850c86480cc464a7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject]

## 3. 사용

- 쉽게 재사용하는 멤버나 잘 변하지 않는변수, 메소드 사용 시 유리
    - 만들어 놓고 클래스 호출 및 객체 생성 필요 없이 바로바로 해당 영역에서 사용할 수 있다.
    - 메모리 자원을 미리 할당해 놓고 사용하는 것이기 때문에 남용 시 메모리 부족할 수도.
- 인스턴스 들이 공통적으로 같은 값이 유지되어야 하는 경우 사용
