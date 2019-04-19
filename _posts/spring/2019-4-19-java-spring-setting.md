---
layout: post
title: Spring 기본설정(pom.xml, web.xml, encoding)
categories: [spring]
tags: [java,spring]
comments: true
---

## 최소한의 Spring 기본 설정

### 프로젝트 기본 설정
- File - New - Spring Legacy Project - Spring MVC 프로젝트 선택
- Spring Verison 5.0.7로 변경

~~~
<properties>
           <java-version>1.6</java-version>
          <org.springframework-version>5.0.7.RELEASE</org.springframework-version>
           <org.aspectj-version>1.6.10</org.aspectj-version>
           <org.slf4j-version>1.6.6</org.slf4j-version>
</properties>
~~~

### pom.xml 설정
- Java Version 변경
- 스프링 5.x 버전을 사용할 때 JDK 1.8을 사용하는 것이 가장 좋다
- maven-compiler-plugin 내용을 1.6에서 1.8로 수정(version도 바꿨다)

~~~
<groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.5.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                     <compilerArgument>-Xlint:all</compilerArgument>
                    <showWarnings>true</showWarnings>
                    <showDeprecation>true</showDeprecation>
</configuration>
~~~
- lombok 설정
- [lombok 공식 사이트](https://projectlombok.org/)
- lombok 공식 사이트에서 lombok 다운로드하여 설치한 후 pom.xml에 설정 추가

~~~
<!-- lombok -->
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-test</artifactId>
	<version>${org.springframework-version}</version>
</dependency>
<dependency>
	<groupId>org.projectlombok</groupId>
	<artifactId>lombok</artifactId>
	<version>1.18.0</version>
	<scope>provided</scope>
</dependency>
~~~
- junit 설정 추가

~~~
<dependency>
	<groupId>junit</groupId>
	<artifactId>junit</artifactId>
	<version>4.12</version>
	<scope>test</scope>
</dependency>
~~~
		   
### 한글 설정
- web.xml에 한글 인코딩을 하도록 utf-8 filter를 설정한다

~~~
    <!-- 한글 인코딩 설정 -->
     <filter>
           <filter-name>encodingFilter</filter-name>
          <filter-class>org.springframework.web.filter.CharacterEncodingFilter
           </filter-class>
           <init-param>
                <param-name>encoding</param-name>
                <param-value>UTF-8</param-value>
           </init-param>
     </filter>
     <filter-mapping>
           <filter-name>encodingFilter</filter-name>
           <url-pattern>/*</url-pattern>
     </filter-mapping>
~~~
- tomcat server.xml에서 Connector에 Encoding 설정을 추가한다

~~~
<Connector connectionTimeout="20000" port="60000"  protocol="HTTP/1.1" redirectPort="8443" URIEncoding="UTF-8" />
<Connector port="8009" protocol="AJP/1.3"  redirectPort="8443" URIEncoding="UTF-8"/>
~~~
- View단에서도 Encoding 설정을 추가한다

~~~
<%@ page language="java" contentType="text/html; charset=utf-8"  pageEncoding="utf-8"%>
<meta http-equiv="Content-Type" content="text/html;  charset=UTF-8">
~~~

~~~
<%@ page language="java" contentType="text/html; charset=utf-8"  pageEncoding="utf-8"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<html>
<head>
     <meta http-equiv="Content-Type" content="text/html;  charset=UTF-8">
     <title>Home</title>
</head>
<body>
<h1>
     Hello world!  
</h1>
<P>  The time on the server is ${serverTime}. </P>
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