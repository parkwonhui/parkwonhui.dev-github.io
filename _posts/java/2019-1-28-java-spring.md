---
layout: post
title: spring 세팅 및 기본설정
categories: [java]
tags: [java,spring]
comments: true
---
# Spring 프로젝트 만들기 및 기본예제
### Spring 기본 세팅
- - Eclipse 말고 STS 사용
- Dynamic project 생성(xml 생성)
- 프로젝트 오른쪽마우스 클릭 - Configure - Convert to Maven

### pom.xml
- 사용하는 lib 추가
- maven lib 는 https://mvnrepository.com/ 에서 검색
- lib의 버전은 맞춰줘야 한다. 예를 들어 spring 버전이 4.3.3이면 같은 버전으로 맞춰주는것이 좋다
- lib는 감싸는 build 태그 다음에 dependencies 태그를 추가한 후 그 안에서 lib 사용을 선언한다

~~~
  </build>
<dependencies>
              <dependency>
                     <groupId>org.springframework</groupId>
                     <artifactId>spring-webmvc</artifactId>
                     <version>4.3.2.RELEASE</version>
              </dependency>
  </dependencies>
~~~

### springapp-servlet
- 스프링의 장점인 di, aop, transaction 등을 쉽게 사용할 수 있게 만들어주는 spring bean configuration file
- context:component-scan 함으로써 base-package에 있는 controller를 전부 생성한다
- default-servlet-handler를 선언하면 @RequestMapping 어노테이션과 요청을 매칭시켜준다. 만약 mvc 선언이 되어있지 않다면 404 에러가 뜬다
- InternalResourceViewResolver는 url의 위치와 타입, 우선순위를 정할 수 있다

~~~
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/mvc  http://www.springframework.org/schema/mvc/spring-mvc-4.3.xsd
              http://www.springframework.org/schema/beans  http://www.springframework.org/schema/beans/spring-beans.xsd
              http://www.springframework.org/schema/context  http://www.springframework.org/schema/context/spring-context-4.3.xsd">
       <context:annotation-config/>
       <context:component-scan base-package="kosta"/>
       
              
       <mvc:annotation-driven/>
       <mvc:default-servlet-handler/>
       
<!-- <bean id="JsonController" class="kosta.controller.JsonController"></bean> -->
       <bean id="viewResolver"
              class="org.springframework.web.servlet.view.InternalResourceViewResolver">
              <property name="prefix" value="/view/"/>
              <property name="suffix" value=".jsp"/>
              <property name="order" value="1"/>
       </bean>
       
</beans>
~~~

### web.xml
- Dispatcher Servlet은 client의 요청을 받고 Handler Mapping, Controller,  ViewResolver,View 에 요청 및 응답을 받은 후 다시 client로 전달하는 역활을 한다. 아래와 같이 servlet-class 태그로 정의할 수 있다
- url 패턴을 정의할 수 있다. 아래 예제에서는 '/'로 오는 모든 요청을 처리한다
~~~
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  xmlns="http://xmlns.jcp.org/xml/ns/javaee"  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee  http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" id="WebApp_ID" version="3.1">
  <display-name>test</display-name>
  
   <servlet>
       <servlet-name>springapp</servlet-name>
       <servlet-class>
              org.springframework.web.servlet.DispatcherServlet
       </servlet-class>
  </servlet>
  
  <servlet-mapping>
       <servlet-name>springapp</servlet-name>
       <url-pattern>/</url-pattern>
  </servlet-mapping>
  
  <filter>
       <filter-name>encodingFilter</filter-name>
       <filter-class>
              org.springframework.web.filter.CharacterEncodingFilter
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
  
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
  </welcome-file-list>
</web-app>
~~~

### index.html
- index.html 호출 시 client라는 url 을 요청
- @RequestMapping 에 /client 라는 매핑이 있다면 매핑되는 함수를 호출하고 없다면 404 에러가 뜬다

### Controller.java
- @Controller 어노테이션을 붙이면 웹 요청을 처리하는 컨트롤러라는 의미
- @Controller 어노테이션을 붙여야 component-scan 했을 때 bean이 생성된다
- "client"를 return 하는데 이는 view/client.jsp 를 호출한다는 의미이다 ( prefix, suffix 설정)

~~~
@Controller
public class JsonController {
       @RequestMapping("/client")
       public String client(){
              return "client";           
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
                            
