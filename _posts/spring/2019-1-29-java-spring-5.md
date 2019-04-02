---
layout: post
title: java spring5 프로젝트 설정
categories: [spring]
tags: [java,spring]
comments: true
---
### Spring 프로젝트 생성
- 1.8 jdk 설치
- Java EE 사용 시 Convert Maven, Controller, View 생성 등을 해야한다. 하지만 STS Spring 프로젝트를 생성하면 기본 세팅이 되어있다
- 프로젝트 창 - Spring Regacy Project - Spring MVC Project 선택

### 프로젝트 창 설명
- src/main/java : service, controller, 도메인 등 대부분의 자바 코드가 들어가 잇다
- src/main/resources : xml 같은 설정파일들이 있다. log4j가 들어가 있다
- src/test/java, resources : 테스트 클래스를 만드는 곳
- src/resource : 리소스 파일이 들어가있음
- src/main/webapp/WEB-INF/spring/appServelt : 디스패쳐에 의해서 생성되는 컨테이너 서블렛. mvc 설정
- src/main/webapp/WEB-INF/spring/root-context : 리스너를 이용해서 스프링 컨테이너를 생성할 수 있다. db, mybatis, service 등의mvc 외 설정
- src/main/webapp/WEB-INF/web.xml: 디스패쳐와 리스너는 부모관계.리스너에서 만들어진 것도 디스패쳐에서 사용할 수 있다. 

### LIB 버전 설정
- jdk 버전 1.6 -> 1.8 로 변경 

~~~
<java-version>1.8</java-version>
<org.springframework-version>5.0.7.RELEASE</org.springframework-version>
<org.aspectj-version>1.6.10</org.aspectj-version>
<org.slf4j-version>1.6.6</org.slf4j-version>
~~~
- junit 버전 1.6 -> 1.8 로 변경

~~~
<dependency>
<groupId>junit</groupId>
<artifactId>junit</artifactId>
<version>4.12</version>
<scope>test</scope>
</dependency>        
~~~
- maven compile 1.6 -> 1.8 버전 변경

~~~
<configuration>
<source>1.8</source>
<target>1.8</target>
<compilerArgument>-Xlint:all</compilerArgument>
<showWarnings>true</showWarnings>
<showDeprecation>true</showDeprecation>
</configuration>
~~~
- log4j 라이브러리 추가

~~~
<dependency>
	<groupId>org.bgee.log4jdbc-log4j2</groupId>
	<artifactId>log4jdbc-log4j2-jdbc4</artifactId>
	<version>1.16</version>
</dependency>
~~~

- pom.xml lib 추가 완료 후 프로젝트 오른쪽 클릭 - maven - update project 해당 프로젝트 업데이트


### Lombok 라이브러리 설치
- setter, getter, toString() 생성자를 자동으로 만들어주는 라이브러리
- https://projectlombok.org/download
- cmd 창 열고 lib 파일 다운로드 받은 곳으로 이동
- java -jar lombok.jar
- specify locatic 클릭
- sts spring 위치로 이동. sts 실행파일 선택 그 후 install update 클릭
- 이클립스 재실행

~~~
<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.4</version>
    <scope>provided</scope>
</dependency>
~~~

- 사용법
- org.zerock.sample 패키지 생성
- @Data 어노테이션은 lombok 라이브러리에 포함된 어노테이션
- @Setter(onMethod_ = {@Autowired}) 어노테이션을 사용해서 자동으로 set,get 메서드를 만들어준다
- @ContextConfiguration("file:src/main/webapp/WEB-INF/spring/root-context.xml")
- 설정파일을 지정해주는 어노테이션. ContextConfiguration 괄호 안에 설정파일 경로를 적어준다.
~~~
@Component
@Data
public class Restaurant {
       @Setter(onMethod_ = {@Autowired})
       private Chef chef;
}
~~~

### 커넥션 풀 설정
- jdbc는 원래 톰캣 lib에 있었기 때문에 lib를 가져온다
- 히카리 lib 가져와야함

~~~
<!-- https://mvnrepository.com/artifact/com.zaxxer/HikariCP -->
<dependency>
<groupId>com.zaxxer</groupId>
<artifactId>HikariCP</artifactId>
<version>2.7.4</version>
</dependency>
<dependency>
<groupId>org.springframework</groupId>
<artifactId>spring-jdbc</artifactId>
<version>${org.springframework-version}</version>
</dependency>
<dependency>
<groupId>org.mybatis</groupId>
<artifactId>mybatis</artifactId>
<version>3.2.6</version>
</dependency>
<dependency>
<groupId>org.mybatis</groupId>
<artifactId>mybatis-spring</artifactId>
<version>1.2.0</version>
</dependency>
<!--  https://mvnrepository.com/artifact/org.springframework/spring-tx -->
<dependency>
<groupId>org.springframework</groupId>
<artifactId>spring-tx</artifactId>
<version>${org.springframework-version}</version>
</dependency>
~~~
- db 접속

~~~
<!-- hikari lib 이용해서 db 접속 -->
<bean id="hikariConfig" class="com.zaxxer.hikari.HikariConfig">
<property name="driverClassName"  value="oracle.jdbc.driver.OracleDriver"/>
<property name="jdbcUrl"  value="jdbc:oracle:thin:@localhost:1521:XE"/>
<property name="username" value="kosta192"/>
<property name="password" value="1234"/>
</bean>
       
<bean id="dataSource" class="com.zaxxer.hikari.HikariDataSource"  destroy-method="close">
<constructor-arg ref="hikariConfig" />
</bean>
       
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
<property name="dataSource" ref="dataSource" />
</bean>

<!-- 이 패키지를 읽어 들이겠다 -->
<mybatis-spring:scan base-package="org.zerock.mapper"/>
       
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
                            

