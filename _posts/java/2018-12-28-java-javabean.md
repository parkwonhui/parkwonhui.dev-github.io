---
layout: post
title: 자바빈
categories: [java]
tags: [java,javabean,jsp,intermediate]
comments: true
---
### 내장객체 Scope
- 아래 4개의 태그는 request, response 객체를 가짐. 범위를 가짐
- page : pageContext에 저장. 하나의 페이지까지
- request : HttpServletRequest에 저장. 내가 요청하는 페이지까지
- session : HttpSession에 저장. 세션이 만료될 때 까지
- application : ServletContext에 저장. 어플리케이션이 유지될 때 까지

### JSP 객체 생성
- 자바 new 처럼 객체를 생성할 수 있다
- id명으로 객체를 접근할 수 있다

~~~
// jsp
<jsp:useBean  id=“connection” class=“myapp.Connection” />
// java
myapp.Connection connection = new myapp.Connection();
~~~

~~~
//jsp
<jsp:useBean  id=“connection” class=“myapp.Connection” >
      <jsp:setProperty name=“connection” property=“timeout” value=“33”/>
</jsp:useBean>
// java
myapp.Connection connection = new myapp.Connection();
connection.setTimeout(“33”);
~~~

### JSP 객체 사용 예제
- 아래 예제는 'insert_form.jsp'에서 여러 데이터(writer, title, contents)를 'insertAction.jsp'로 전송한다
- 이 때 getParameter를 사용하면 하나의 필드 당 하나의 값만 가져올 수 있어서 파라메터가 많아지면 비효율
- 간편하게 초기화할 수 있는 내장객체를 생성한다
- class의 생성자, set, get 메소드를 전부 만들어야 한다. 왜냐하면 값 생성 및 접근을 하기 위해서이다(만약 해당 함수가 없다면 값을 넣고, 가져오지 못해서 null로 출력된다)
- 해당 컴포넌트의 name과 class 필드의 name을 맞춰줘야 한다. 안맞추면 값 매칭이 안됨
- jsp:setProperty 태그에서 property의 값을 *으로 주면 모든 객체를 가져온다는 뜻이라서 일일이 필드 초기화 x
- jsp:setProperty 태그의 name필드는 생성한 id값과 매칭된다

- insert_form.jsp

~~~
<%@ page language="java" contentType="text/html; charset=utf-8"
    pageEncoding="utf-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>Insert title here</title>
</head>
<body>
<h3>글쓰기</h3>
<hr>
<form action="insertAction.jsp" method="post">
       작성자 : <input type="text" name="writer">

       제목 : <input type="text" name="title">

       내용

       <textarea rows="6" cols="70" name="contents"></textarea>
       

       <input type="submit" value="등록">
</form>
</body>
</html>
~~~
- insertAction.jsp

~~~
<%@ page import="kosta.bean.BoardDao" %>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
<%
// usebean하기전 항상 인코딩 먼저해야한다!
request.setCharacterEncoding("utf-8");
%>
<!-- 객체 생성 -->
<jsp:useBean id="board" class="kosta.bean.Board" />
<!-- name은 id를 넣어주므로 board이다 -->
<!-- * form에서 넘어오는 값을 전부 초기화해준다 request.getParameter할 필요가 없다  -->
<!-- 필드에 set 메소드가 있어서 가능 -->
<jsp:setProperty property="*" name="board"/>
<%
       BoardDao dao = BoardDao.getInsance();
       dao.insertBoard(board);
%>
</body>
</html>
~~~
- Board.java

~~~
public class Board {
       private String writer;
       private String title;
       private String contents;
       
       public Board(){}
       
       public Board(String writer, String title, String contents) {
             super();
             this.writer = writer;
             this.title = title;
             this.contents = contents;
       }
       @Override
       public String toString() {
             return "Board [writer=" + writer + ", title=" + title + ",  contents=" + contents + "]";
       }
       public String getWriter() {
             return writer;
       }
       public void setWriter(String writer) {
             this.writer = writer;
       }
       public String getTitle() {
             return title;
       }
       public void setTitle(String title) {
             this.title = title;
       }
       public String getContents() {
             return contents;
       }
       public void setContents(String contents) {
             this.contents = contents;
       }
}
~~~
- BoardDao.java

~~~
public class BoardDao {
       private static final BoardDao dao = new BoardDao();
       public static BoardDao getInsance(){
             return dao;
       }
       
       public void insertBoard(Board board){
             System.out.println(board);
       }
}
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
                            