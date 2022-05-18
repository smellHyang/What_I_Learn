# HTTP 메소드 종류

## 1. HTTP 메소드란?

- 클라이언트가 웹서버에세 사용자의 요청의 목적이나 종류를 알리는 수단

## 2. 속성

- 안전(safe methods)
    - 메소드를 계속 호출해도 리소스 변경 x (get)
- 멱등(Idempotent Methods)
    - 메소드를 계속 호출해도 결과가 똑같다.(get, put, delete)
- 캐시가능(Cacheable Methods)
    - 캐싱을 해서 데이터를 효율적으로 가져 올수 있다.(get,head, post, patch)

## 3. 종류

| GET | 보통 리소스를 조회할 때 사용하며, 서버에 전달하고 싶은 데이터는 query를 통해서 전달한다. 메시지 바디를 사용해서 데이터를 전달할 수는 있지만, 지원하지 않는 곳이 많아서 권장하지 않는다. |
| --- | --- |
| POST | 데이터 요청을 처리하고, 메시지 바디를 통해 서버로 데이터를 전달한다. 주로 신규 리소스를 등록하거나 프로세스 처리에 사용된다. |
| PUT | 리소스가 있으면 대체하고 리소스가 없으면 생성한다. 쉽게 말해 데이터를 덮어쓴다. |
| DELETE | 리소스를 제거할때 사용한다. |
| PATCH | PUT과 마찬가지로 리소스를 수정할 때 사용하지만, PATCH는 리소스를 일부분만 변경할 수 있다. |
| OPTIONS | 대상 리소스에 대한 통신 가능 옵션을 설명(주로 CORS에서 사용) |
| HEAD | GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환 |
| TRACE | 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행 |
| CONNECT | 대상 자원으로 식별되는 서버에 대한 터널을 설정 |

## 4. 응답코드
| 요청 수신 완료 및 처리 |  |
| --- | --- |
| 100  |  Continue (클라이언트로 부터 일부 요청을 받았으며 나머지 정보를 계속 요청함) |
|  101 |  Switching protocols |
| 요청 성공 |  |
|  200 |  OK(요청이 성공적으로 수행되었음) |
|  201 |  Created (PUT 메소드에 의해 원격지 서버에 파일 생성됨) |
|  202 |  Accepted(웹 서버가 명령 수신함) |
|  203 |  Non-authoritative information (서버가 클라이언트 요구 중 일부만 전송) |
|  204 |  No content, (사용자 요구 처리하였으나 전송할 데이터가 없음) |
| 리다이렉션 |  |
|  301 |  Moved permanently (요구한 데이터를 변경된 타 URL에 요청함) |
|  302 |  Not temporarily |
|  304 |  Not modified (컴퓨터 로컬의 캐시 정보를 이용함, 대개 gif 등은 웹 서버에 요청하지 않음) |
| 클라이언트 오류 |  |
|  400 |  Bad request (사용자의 잘못된 요청을 처리할 수 없음) |
|  401 |  Unauthorized (인증이 필요한 페이지를 요청한 경우) |
|  402 |  Payment required(예약됨) |
|  403 |  Forbidden (접근 금지, 디렉터리 리스팅 요청 및 관리자 페이지 접근 등을 차단) |
|  404 |  Not found, (요청한 페이지 없음) |
|  405 |  Method not allowed (혀용되지 않는 http method 사용함) |
|  407 |  Proxy authentication required (프락시 인증 요구됨) |
|  408 |  Request timeout (요청 시간 초과) |
|  410 |  Gone (영구적으로 사용 금지) |
|  412 |  Precondition failed (전체 조건 실패) |
|  414 |  Request-URI too long (요청 URL 길이가 긴 경우임) |
| 서버측 오류 |  |
|  500 |  Internal server error (내부 서버 오류) |
|  501 |  Not implemented (웹 서버가 처리할 수 없음) |
|  503 |  Service unnailable (서비스 제공 불가) |
|  504 |  Gateway timeout (게이트웨이 시간 초과) |
|  505 |  HTTP version not supported (해당 http 버전 지원되지 않음) |
