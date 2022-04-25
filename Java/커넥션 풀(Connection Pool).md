# 커넥션 풀(Connection Pool)
1. 커넥션풀(Connection Pool)이란??
    - DB연결을 위해서 일정 수의 connection 객체를 만들어 pool에 담가두었다가 사용하는 기법.
    
2. 동작과정
    - 사용자가 DB를 사용하기 위해 connection 객체를 요청한다.
    - connection pool에서 사용되고 있지 않은 connection 객체를 제공한다.
    - 사용자가 connection객체를 사용 완료하면 pool에 반환한다.
        ![image](https://user-images.githubusercontent.com/73684562/165069841-c8d00d0f-03b3-46e8-8c84-9e6cad6b217c.png)
        
        ```java
        Connection conn = null;
        PreparedStatement  pstmt = null;
        ResultSet rs = null;
        
        try {
            sql = "SELECT * FROM T_BOARD"
        
            // 1. 드라이버 연결 DB 커넥션 객체를 얻음
            connection = DriverManager.getConnection(DBURL, DBUSER, DBPASSWORD);
        
            // 2. 쿼리 수행을 위한 PreparedStatement 객체 생성
            pstmt = conn.createStatement();
        
            // 3. executeQuery: 쿼리 실행 후
            // ResultSet: DB 레코드 ResultSet에 객체에 담김
            rs = pstmt.executeQuery(sql);
            } catch (Exception e) {
            } finally {
                conn.close();
                pstmt.close();
                rs.close();
            }
        }
        ```
        
        → 
        
3. 왜사용하는가??
    - DB를 접속하는 과정은 드라비어를 로드하고 커넥션 객체를 받아와야한다. 사용자가 요청할때 마다 이러한 과정이 일어나게 되면 비효율이고 서버 부하를 불러올 수도 있다. 그렇기 때문에 객체를 재활용함으로써 단점을 줄인다.
    
4. 특징 
    - 서버 부하를 줄여준다
        
        → Java에서 DB connection을 맺는 과정은 부하가 많이 걸리는 작업이다(OOME의 주원인). 또한 동시에 많은 사람들이 connection을 요구한다면 서버가 죽어버릴수 있다.  이러한 문제를 해결하기 위해 connection을 재활용하여 서버부하를 줄여준다.
        
    - 자원을 효율적으로 사용할수있다.
        
        → 요청이 올때마다 서버에서 무제한 connection을 생성하게 되면 전체시스템에 문제가 될 수 있다. 따라서 connection pool에 일정 수의 객체를 생성하여 관리한다.
        
    - connection Pool이 클 경우 메모리 소모가 크고, 적게 해놓으면 한정된 객체로 인하여 대기시간이 발생한다.
