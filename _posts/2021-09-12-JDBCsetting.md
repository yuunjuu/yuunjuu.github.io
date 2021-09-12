---
title: "이클립스 JDBC 개발 환경 설정"
excerpt: "이클립스와 데이터베이스(Oracle, MySQL)를 연동한다."

categories:
  - JSP
tags:
  - [Java, JSP, JDBC, Eclipse, Oracle, MySQL]

toc: true
toc_sticky: true

date: 2021-09-12
last_modified_at: 2021-09-12
---

# JDBC(Java Database Connectivity)

---
```
✔ JDBC(Java Database Connnectivity)는 자바에서 데이터베이스에 접속할 수 있도록 하는 자바 API이다. JDBC는 데이터베이스에서 자료를 쿼리하거나 업데이트하는 방법을 제공한다.
```
**java.sql package**

- java.sql.DriverManager
  
- java.sql.Connection
  
- java.sql.Statement
  
- java.sql.ResultSet
  
- java.sql.PreparedStatement
  
- java.sql.CallableStatement

**JDBC 실행순서**

1. Driver loading: `Class.forName(driver);` - Oracle Driver 로딩
2. Connection: `conn = DriverManager.getConnection(url, id, pw);` - Java와 Oracle 연결
3. Statement: `stmt = con.createStatement();` - query 전송 객체
4. query: `String sql = "SELECT * FROM 테이블명"` - query 작성
5. run: res = `stmt.executeQuery(sql);` - query 전송

## ○ Oracle 연결
```
✔ Oracle이 설치되어 있어야 한다.
```
1. Oracle과 JDBC를 연결하기 위해 다음의 경로로 이동하여 ojdbc6.jar을 복사한다.
    - C:\oraclexe\app\oracle\product\11.2.0\server\jdbc\lib
2. 이 파일을 톰캣과 연동하기 위해 C:\Tomcat 8.5\lib로 이동하여 붙여넣는다.
3. 이클립스에 실행되고 있는 서버가 있다면  해당 서버를 재실행 한다. (마우스 우클릭 > Restart)

### ○ Oracle 연결 예제

이클립스와 Oracle이 잘 연결되는지 확인하기 위해 아래 코드를 실행해본다.

```java
<%@ page import="java.sql.SQLException"%>
<%@ page import="java.sql.DriverManager"%>
<%@ page import="java.sql.Connection"%>
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<%
	Connection conn = null;
	try {
		String url = "jdbc:oracle:thin:@localhost:1521:xe";
		String user = "scott";
		String pwd = "tiger";
		
		Class.forName("oracle.jdbc.driver.OracleDriver");
		conn = DriverManager.getConnection(url, user, pwd);
		out.print("데이터베이스 연결에 성공했습니다.");
	} catch (SQLException ex) {
		out.print("데이터베이스 연결에 실패했습니다.");
		out.print("SQLException: " + ex.getMessage());
	} finally {
		if (conn != null) {
			conn.close();
		}
	}
%>
```

만약 Oracle과 연결이 되지 않은 상태에서 JSP 파일을 실행하면 아래 그림과 같이 HTTP 500 에러가 발생한다.

Oracle과 제대로 연결되었다면 아래 그림과 같이 데이터베이스 연결에 성공했다는 메시지를 확인할 수 있다.

---

## ○ MySQL 연결
```
✔ MySQL이 설치되어 있어야 한다.
```
**MySql Connector 다운로드**

1. Java와 MySQL을 연결하기 위해 MySQL Connector/J 설치가 필요하다. [이 링크](https://dev.mysql.com/downloads/connector/j/)에 접속하여 Platform Independent에서 압축(Zip) 파일을 다운로드한다.

2. 압축 파일을 풀면 해당 폴더에 최신 버전의 MySql Connector(mysql-connector-java-8.0.26.jar)가 있다. 이 파일을 복사하여 아래 경로에 붙여넣기 한다.
    - C:\Program Files\Java\jdk1.8.0_291\lib
    - C:\Tomcat 8.5\lib

**이클립스 설정**

1. 이클립스 하단 > Database Source Explorer > 마우스 우클릭 New... > 'New Connection Profile'창
    - 이클립스의 하단에 위치한 Database Source Explorer에서 오른쪽 마우스의 New...를 클릭하면 'New Connection Profile' 창이 나타난다.

2. Connection Profile Types: > MySQL 선택 > Name: > MySQL_Connection > Next >
    - Connection Profile 타입을 MySQL로 선택한 후, MySQL이름을 설정한다. 필자는 MySQL_Connection으로 설정하였다. 그리고 Next > 버튼을 클릭한다.

3. Drivers: > 동그란 버튼 클릭
    - Driver를 설정할 수 있는 창이 나타나고, Drivers 우측에 있는 버튼을 클릭하면 New Driver Definition 창이 나타난다.

4. **Name/Type 탭**
    - 최신 버전을 선택한다.

5. **JAR List 탭**
    - 기존의 connector.jar 파일을 삭제하고, Add JAR/Zip을 클릭하여 Java 폴더에 복사한 connector.jar의 위치를 찾는다.

6. **Properties 탭**
    - Connection URL: jdbc:mysql://localhost:[3306]/[database]에서 [3306]은 MySQL을 설치하며 설정한 포트번호로, [database]부분을 데이터베이스 이름으로 바꾸어준다.
    - Database Name: URL에 적은 데이터베이스 이름을 적어준다.
    - Password: MySQL을 설치하며 설정한 비밀번호를 입력한다.

7. OK > Test Connection > Finish
    - OK를 클릭하면 아래 화면과 같이 앞에서 설정한 드라이버 속성들을 확인할 수 있다.
    - Test Connection을 클릭하면 좌측화면과 같이 Ping Succeeded!가 나타나야 한다.
    - Finish를 하면 하단에 다음과 같이 나타나는 것을 확인할 수 있다.

8. 하단 우측의 Open scrapbook to edit SQL statements 클릭 > SQL Scarpbook 창
    - Type: MySql_5.1
    - Name: MySQL_Connection
    - Database: jdbc
    - 저장(필자는 showDB.sql로 저장하였다.)

9. 이 창에서 sql문을 입력하여 테스트해볼 수 있다.
    - show database 입력 > 오른쪽 마우스의 Execute Selected Text 클릭

### ○ MySQL 예제

MySQL Command 창을 열어 다음과 같이 테이블을 생성한다.

```sql
USE jspdb

SHOW TABLES;

CREATE TABLE member(
id int NOT NULL auto_increment,
name varchar(100) NOT NULL,
passwd varchar(50) NOT NULL,
PRIMARY KEY(id)
);

DESC member;

INSERT INTO member VALUES(1, '홍길동', '1234');

SELECT * FROM member;
```
이클립스와 MySQL이 잘 연결되는지 확인하기 위해 아래 코드를 실행해본다.

```java
<%@ page import="java.sql.SQLException"%>
<%@ page import="java.sql.DriverManager"%>
<%@ page import="java.sql.Connection"%>
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<%
	Connection conn = null;
	try {
		String url = "jdbc:mysql://localhost:3306/jspdb";
		String user = "root";
		String pwd = "1234";
		
		Class.forName("com.mysql.jdbc.Driver");
		conn = DriverManager.getConnection(url, user, pwd);
		out.print("데이터베이스 연결에 성공했습니다.");
	} catch (SQLException ex) {
		out.print("데이터베이스 연결에 실패했습니다.");
		out.print("SQLException: " + ex.getMessage());
	} finally {
		if (conn != null) {
			conn.close();
		}
	}
%>
```