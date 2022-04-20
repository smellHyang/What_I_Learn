# Java I/O

- 바이트 기반의 데이터 처리 → Stream
- char기반의 파일 → Reader/Writer
- 빠른 I/O를 처리하기 위한 NIO(Buffer/Channel기반)

1. InputStream/OutputStream(데이터 입출력)
    - 데이터를 읽을때 자식클래스를 통해 읽으면된다.
    - abstract 클래스로 선언되어있다.
    - 해당 리소스를 다른 클래스에서 작업할수 있도록 작업이 종료되면 무조건 닫아줘야한다.(close())

1. Reader/Writer
    - abstract 클래스로 선언되어있다.
    - 해당 리소스를 다른 클래스에서 작업할수 있도록 작업이 종료되면 무조건 닫아줘야한다. (close())
