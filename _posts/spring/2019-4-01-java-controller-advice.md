---
layout: post
title: ControllerAdvice
categories: [spring]
tags: [java,controllerAdvice]
comments: true
---

### ControllerAdvice
- @ControllerAdvice는 스프링 프레임워크 3.2부터 사용 가능
- 예외 상황은 @ExceptionHandler와 @ControllerAdvice를 사용해서 처리할 수 있다(다른 방법으로 @ResponseEntity를 사용할 수 있다)
- AOP를 이용하는 방식(공통사항은 따로 분리하는 방식)
- 기존 방식으로 예외를 처리하면 예외 처리가 있을 때 마다 중복작성된다. 하지만 AOP 개념을 도입하면 한곳에서만 처리하면 된다.(if문으로 체크하지 않고 예외를 발생시키는 이유)
- 체계적으로 로직검사를 하여 유지보수가 쉬워진다
- @Valid를 사용하여 Setter 호출 시 형식체크를 해서 값을 넣지 않을 수도 있다)

### 설정
- CommonExceptionAdvice java 파일 생성
- 예외를 처리하는 클래스
- 먼저 pom.xml에서 버전 등을 알맞게 세팅한다

~~~
<java-version>1.8</java-version>
<org.springframework-version>5.0.7.RELEASE</org.springframework-version>
<org.aspectj-version>1.6.10</org.aspectj-version>
<org.slf4j-version>1.6.6</org.slf4j-version>
~~~
### ControllerAdvice 처리 클래스 추가

- @ControllerAdvice는 해당 객체가 스프링의 컨트롤러에서 발생하는 예외를 처리하는 존재임을 명시
- @ExceptionHandler는 해당 메서드가 괄호에 들어가는 예외를 처리한다는 의미

~~~
package test.exam.advice;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import lombok.extern.log4j.Log4j;
@ControllerAdvice
@Log4j
public class CommonExceptionAdvice {
       @ExceptionHandler(Exception.class)
       public String except(Exception ex, Model model){
              log.error("Exception"+ex.getMessage());
              model.addAttribute("exception", ex);
              log.error(model);
              return "error";
       }
}
~~~

### 패키지 추가
- ControllerAdvice 어노테이션 클래스를 알 수 있도록 scan

~~~
<context:component-scan base-package="test.exam.advice" /> 
~~~

### 에러화면 추가
- jsp를 추가하고 아래 코드를 작성해서 view 단을 만든다
- 그리고 일부러 예외가 발생하는 코드를 만든다(ex. 4/0 같은..)
- 그리고 그 에러가 나는 코드가 있는 url로 접속해서 예외를 강제로 발생시킨다.
- 그러면 ExceptionHandler 어노테이션이 발생했으므로 해당 함수가 호출되어 error 페이지로 이동한다.

~~~
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  "http://www.w3.org/TR/html4/loose.dtd">
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=EUC-KR">
<title>Insert title here</title>
</head>
<body>
       <h4><c:out value="${exception.getMessage()}"></c:out></h4>
</body>
</html>
~~~

### 404 에러 페이지 추가
- 스프링 MVC의 요청은 DispatcherServlet을 이용해서 처리되므로 404 에러도 같이 처리되도록 web.xml 수정

~~~
<servlet>
              <servlet-name>appServlet</servlet-name>
              <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
              <init-param>
                     <param-name>contextConfigLocation</param-name>
                     <param-value>/WEB-INF/spring/appServlet/servlet-context.xml</param-value>
              </init-param>
              <init-param>
                     <param-name>throwExceptionIfNoHandlerFound</param-name>
                     <param-value>true</param-value>
              </init-param>
              <load-on-startup>1</load-on-startup>
</servlet>
~~~
- 404 에러 시 호출 될 함수 추가

~~~
@ExceptionHandler(NoHandlerFoundException.class)
@ResponseStatus(HttpStatus.NOT_FOUND)
public String error404(NoHandlerFoundException ex){
    return "error404";
}
~~~

- jsp 추가 후 404 페이지 처리
- 없는 페이지 url 을 입력하면 해당 jsp 출력

~~~
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=EUC-KR">
<title>Insert title here</title>
</head>
<body>
<h1>해당 페이지를 찾을 수 없습니다</h1>
</body>
</html>
~~~

<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIA*BLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
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