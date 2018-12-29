---
layout: post
title: jdbc
categories: [java]
tags: [java,jdbc,jsp,intermediate]
comments: true
---
### 이클립스에 데이터베이스 연동하기
- JDBC 드라이브 설치
- C:\oraclexe\app\oracle\product\11.2.0\server\jdbc\lib
- ojbc6 파일 copy
- Tomcat 8의 lib 폴더에 ojbc 붙여넣기
- 프로젝트에서 라이브러리에서 ojbc가 들어있는 것을 확인할 수 있음

### 오라클 접속 확인
- 접속
- 에러발생(오라클 서비스가 중지되어있어서 oracle 붙은 이름의 서비스는 실행시켜줌)

~~~
The Network Adapter could not establish the connection
~~~


### 이클립스-오라클 접속
- jdbc 로드

~~~
import java.sql.*;
Class.forName("oracle.jdbc.driver.OracleDriver");
~~~
- 데이터베이스 연결 객체인 Connection 생성

~~~
Connection con = null;
con=DriverManager.getConnection(url, uid, pwd);  
~~~

- Statement 객체 생성하기

~~~
Statement stmt = con.createStatement( );
~~~

- SQL문을 실행하여 결과 처리
- ResultSet에 데이터가 저장되어있음

~~~
String str = "select * from member";
ResultSet rs = stmt.executeQuery(str);
~~~

- DAO : CRUD
- DTO : 테이블정보
- query 실행 시 에러 발생
- java.sql.SQLSyntaxErrorException: ORA-00917: missing comma
- 값에 콤마를 안찍어서 발생

### Debuging
한줄한줄 내려가고 싶다: f6
해당 메소드에 들어가고싶다:f5

### DBCP(DB Connection Pool)
- db query 요청할 때 마다 connect을 하면 많은 리소스를 잡아먹는다
- resource tag를 통해 DataSource를 얻음
- DataSource객체 안에 Connection Pool이 있다
1. 'server.xml'에서 Context 태그 사이에 DataResource 태그 추가

~~~
<Context docBase="JSP" path="/JSP" reloadable="true"  source="org.eclipse.jst.jee.server:JSP">
<Resource auth="Container"  driverClassName="oracle.jdbc.driver.OracleDriver" maxActive="100" maxIdle="30"  maxWait="10000" name="jdbc/oracle" password="1234" type="javax.sql.DataSource"  url="jdbc:oracle:thin:@localhost:1521:XE" username="kosta192"/>      
</Context>
</Host>
~~~
2. Connection을 java source code로 가져온다
- name으로 DataSource를 찾고, DataSource 안에 Connection을 가져온다

~~~
       // DBCP방식으로 Connection객체 구하기
       public Connection getConnection(){
             DataSource ds = null;
             try {
                    // server.xml에서 데이터리소스를 가져옴
                    Context ctx = new InitialContext();
                    ds =  (DataSource)ctx.lookup("java:comp/env/jdbc/oracle");// jndi: name을 통해  리소스를 얻어옴.name이 jdbc/oracle
                    return ds.getConnection();
             } catch (Exception e) {
                    // TODO: handle exception
             }
             return null;
       }
~~~
3. 결과 데이터를 가져오는 함수를 만든다
- 함수를 호출해서 Connection을 가져온다

~~~
public List<Board> listBoard(){
             Connection conn = null;
             try {
                    conn = getConnection();
                    System.out.println("conn:"+conn);
             } catch (Exception e) {
                    e.printStackTrace();
             }
             return null;
       }
~~~

4. jsp에서 데이터를 가져오는 함수 호출

~~~
<%@page import="kosta.bean.BoardDao" %>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
       BoardDao dao = BoardDao.getInsance();
       dao.listBoard();
%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
</body>
</html>
~~~

~~~
<h3>글목록 보기</h3>
<a href="insert_form.jsp">글쓰기</a>
<table width="500" border="1" cellpadding='0' cellspacing='0'>
    <tr>
        <td>글번호</td>
        <td>제목</td>
        <td>작성자</td>
        <td>작성일</td>
        <td>조회수</td>
    </tr>
<%
    for(int i = 0; i < list.size(); ++i){
        Board board = list.get(i);
    }
%>
    <tr>
        <td><%= board.getSeq() %></td>
        <td><%= board.getTitle() %></td>
        <td><%= board.getWriter() %></td>
        <td><%= board.getRegdate() %></td>
        <td><%= board.getHitCount() %></td>
    </tr>
<%}%>
</table>
~~~


<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = 'https://parkwonhui.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
                            
