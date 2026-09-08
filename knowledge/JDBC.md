---
tags:
  - jdbc
  - java
  - database
  - prepared-statement
  - resultset
---
**JDBC(Java Database Connectivity)** 는 Java 앱에서 데이터베이스에 접근해 작업을 수행하는 ==일련의 모든 것을 캡슐화한 것==이다.

![[java-jdbc-overview.png]]

## Driver
RDBMS는 벤더마다 다르다. JDBC는 **Driver를 통해 각 벤더사의 RDBMS에 접근**한다. 즉 driver가 **가교 역할**을 한다.

![[java-jdbc-driver.png]]

## 1. Connection — DBMS 접근 (계정 로그인)
url은 DB의 위치다. **jdbc 프로토콜로 시작해 IP, Port, DBMS 닉네임 순**이며 벤더에 따라 다르다.

```java
String url  = "jdbc:oracle:thin:@127.0.0.1:1521:xe";
String user = "scott";
String pwd  = "tiger";

Class.forName("oracle.jdbc.driver.OracleDriver");      // 드라이버 찾기
Connection con = DriverManager.getConnection(url, user, pwd);  // 연결하기
```

## 2. Statement — Query 전송
```java
Statement stmt = con.createStatement();      // SQL을 보낼 객체 생성

stmt.executeQuery("SELECT * FROM emp_test");                       // Query SQL
stmt.executeUpdate("INSERT INTO emp_test VALUES(1,'홍길동',1000)");  // DML SQL
```

### PreparedStatement
**같은 SQL을 반복 수행할 때** 쓴다. 가독성과 사용 편의성이 좋다.

```java
String sql = "INSERT INTO emp_test VALUES(?,?,?)";
PreparedStatement pStmt = con.prepareStatement(sql);

pStmt.setInt(1, 101);
pStmt.setString(2, "홍길동");
pStmt.setInt(3, 50000);
```

## 3. 결과 받기
| 전송한 SQL | 반환 타입 |
| --- | --- |
| **Query SQL** (SELECT) | `ResultSet` |
| **DML SQL** (INSERT/UPDATE/DELETE) | `int` (영향받은 행 수) |

```java
ResultSet rs = stmt.executeQuery("SELECT * FROM emp_test");

rs.next();   // 커서를 움직일 수 있는지 = 값의 유무. return boolean

String name = rs.getString("name");
int salary  = rs.getInt("Salary");
```

## 관련 노트
- [[Java 예외 처리]]
- [[Java IO 패키지와 Stream]]
- [[Java]]
