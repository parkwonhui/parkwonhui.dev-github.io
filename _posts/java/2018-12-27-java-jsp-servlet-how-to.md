---
layout: post
title: jsp, servlet 정리
categories: [java]
tags: [java,servlet,intermediate,jsp]
comments: true
---
# JSP, Servlet 설정, 사용법
### 톰켓설정
- JavaEE 설정
- Window-Preperence 메뉴 클릭
- Server-Runtime Environments 메뉴에서 톰캣버전 설정, 톰켓 폴더 설정

### 인코딩 설정
- Web-HTML Files - Encoding UTF-8
- Web-JSP Files - Encoding UTF-8

### 프로젝트 생성
- Dynamic Project 만들 때 XML 생성체크하기
- (NEXT, NEXT 클릭하면 XML 생성 체크박스 있음)


### 웹 어플리케이션
- 웹을 기반으로 실행되는 프로그램
- 단순 화면을 출력하는게 아니라, 어떤 동작에 대한 처리를 한다(WAS:Web Application Server)
- Servlet과 JSP는 J2EE를 구성하는 기술 중 하나
- 컨테이너 (WSA, Servlet, JSP) WAS 기반으로 돌아가는 것을 의미
- WAS가 Servlet을 초기화,생성, 실행한다
- 서비스 API (JDBC, JTA, JMS, JNDI, XML...)

### Servlet, JSP
- Servlet은 자바코드 기반에서 HTML이 들어가있다(WEB 페이지 만들기가 어렵다)
- 그래서 만들어진 것이 JSP. HTML안에 자바코드가 들어가있다
- 서블릿, JSP는 같다. 밀접한 관계(WAS가 JSP를 서블릿으로 변경해준다)
- Servlet은 비즈니스 로직을 처리
- JSP는 출력된 결과 처리

### 서블릿 클래스 작성
- HttpServlet 클래스를 상속해서 class를 만들어야 한다
- 서블릿 클래스=>서블릿객체=>서블릿
- 멀티 스레드에서는 데이터 관리를 신경써야 한다
- request : 요청
- response : 응답

### JSP 작성
- 자바코드는 '<%'로 시작한다
- Java코드(처리)와 JSP가 섞이면 복잡하므로 처리부분은 Servlet에서 작성한다

~~~
<%@ page import ="java.text.SimpleDateFormat" %>
<%@ page import ="java.util.Calendar" %>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>JSP예제</h1>
<%
       Calendar date = Calendar.getInstance();
       SimpleDateFormat today =
                    new SimpleDateFormat("YYYY년 MM월 DD일");
%>
오늘은 <%=today.format(date.getTime()) %>
</body>
</html>
~~~
- E:\work\jsp_work\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\work\Catalina\localhost\Servers\org\apache\jsp\JSP
- 위는 실제 실행되는 java파일 위치
- JSP가 java파일로 변환되었고 그 파일이 실제로 실행됨

### JSP, Servlet 예제
- form.jsp에서 주는 값 2개를 FormServlet.java에서 받아서 결과계산 후 다시 result.jsp url을 요청해서 결과값을 넘겨준다
- form.jsp

~~~
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
<!-- action위치는 Project명/Servlet파일명 -->
<form action="/Servers/FormServlet" method="post">
숫자1:<input type="text" name="num1">
숫자2:<input type="text" name="num2">

<input type="submit" value="계산">
</form>
</body>
</html>
~~~

- FormServlet.java
- Post방식으로 호출했으므로 doPost 함수가 호출됨
~~~
import java.io.IOException;
import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
@WebServlet("/FormServlet")
public class FormServlet extends HttpServlet {
       private static final long serialVersionUID = 1L;
       
    public FormServlet() {
        super();
    }
    protected void doPost(HttpServletRequest request, HttpServletResponse  response) throws ServletException, IOException {
       request.setCharacterEncoding("utf-8");
       int num1 = Integer.parseInt(request.getParameter("num1"));
       int num2 = Integer.parseInt(request.getParameter("num2"));
       int result = num1 + num2;
       request.setAttribute("result", result);
    // jsp가 위치한 폴더이름/jsp파일이름
       RequestDispatcher re = request.getRequestDispatcher("/JSP/result.jsp");
       re.forward(request, response);
       }
}
~~~
- result.jsp

~~~
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
       결과:${result}
</body>
</html>
~~~

### redirect, dispatcher
- Dispatcher는 A->B->C로 요청이 들어가면 B->C로 이동할 때 url이 C로 바뀌지 않고 B url 그대로 있다
- Dispatcher는 url을 기존 그대로 사용한다. 같은 요청이므로 데이터를 사용할 수 있다
- redirect는 다른 요청이므로 데이터를 사용할 수 없다. url도 다르다
- 그래서 redirect 사용 시 데이터의 값이 출력되지 않는다. 데이터를 사용하지 못하기 때문

~~~
// dispatcher
RequestDispatcher re = request.getRequestDispatcher("/JSP/result.jsp");
re.forward(request, response);
// redirect
response.sendRedirect("JSP/result.jsp");
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
                            