---
layout: post
title: JavaConfig mariadb 연결
categories: [spring]
tags: [java,javaConfig]
comments: true
---


# JavaConfig mariadb 연결
- pom.xml
- pom.xml에서 mariadb 라이브러리 추가

~~~
<dependency>
	<groupId>org.mybatis</groupId>
	<artifactId>mybatis</artifactId>
	<version>3.4.2</version>
</dependency>

<!-- mybatis-spring -->
<dependency>
	<groupId>org.mybatis</groupId>
	<artifactId>mybatis-spring</artifactId>
	<version>1.3.1</version>
</dependency>

<dependency>
	<groupId>org.mariadb.jdbc</groupId>
	<artifactId>mariadb-java-client</artifactId>
	<version>2.3.0</version>
</dependency>
~~~

### JDBC 연결
- JDBC는 어떤 DB 드라이버든 동일한 코드로 제어할 수 있다.
- myBatis에 비해 같은 코드 반복이 많고 복잡하다(select 직접 처리) 직접 연결을 열고 닫아줘야 한다
- 많은 사용자들이 db에 원활하게 접속할 수 있게 db 커넥션풀을 미리 만들어놔야 한다.
- getConnection("jdbc:mariadb://접속ip:포트번호/데이터베이스이름", id, 비밀번호)
- 아래 코드가 실패하면 비밀번호, db 존재 확인 그 외 1.권한 확인  2. 포트번호 확인 2. 방화벽 확인(ping test)
- 나는 포트가 올라가있음에도 다른 포트번호와 겹쳐서 그런지(mysql?) mariadb에 접속하지 못했다. 그 후 mariadb 포트번호를 변경하고 접속할 수 있었다.


~~~
import static org.junit.Assert.fail;

import java.sql.Connection;
import java.sql.DriverManager;
import org.junit.Test;
import lombok.extern.log4j.Log4j;

@Log4j
public class mysqlDBTest {

	@Test
	public void testConnection() throws ClassNotFoundException {	
		 Class.forName("org.mariadb.jdbc.Driver");
	    try (Connection con = DriverManager.getConnection("jdbc:mariadb://127.0.0.1:3310/test", "test", "1234"))
		{
			System.out.println(con);
		} catch (Exception e) {
			fail(e.getMessage());
		}
	}
}
~~~

### MyBatis
- SqlSessionFactory는 DataSource를 참고하여 db와 mybatis를 연결시킴
- JDBC에서는 DB에 접근할 때마다 Session을 가져와서 사용했지만 Spring에서는 bean에 올려두고 mapper를 이용해서 접근
- @Mapper, @Service 어노테이션을 이용하면 스프링 빈으로 주입받아 사용 가능[설명](http://wiki.sys4u.co.kr/pages/viewpage.action?pageId=7767258)
- 자동으로 연결과 종료를 수행한다
- 아래는 접속을 확인하기 위해서 유닛테스트를 하기 위해 Connection 직접 호출
- RootConfig.java

~~~
import javax.sql.DataSource;

import org.apache.ibatis.session.SqlSessionFactory;
import org.mybatis.spring.SqlSessionFactoryBean;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.jdbc.datasource.DriverManagerDataSource;

@Configuration
@ComponentScan(basePackages= {"base.toy.vo"})
public class RootConfig {
	
	@Bean
	public DataSource dataSource(){
		DriverManagerDataSource dataSource = new DriverManagerDataSource();
		dataSource.setDriverClassName("org.mariadb.jdbc.Driver");
		dataSource.setUrl("jdbc:mariadb://localhost:3310/test");
		dataSource.setUsername("test");
		dataSource.setPassword("1234");
		
		return dataSource;
	}
	
	  @Bean
	  public SqlSessionFactory sqlSessionFactory() throws Exception {
	    SqlSessionFactoryBean sqlSessionFactory = new SqlSessionFactoryBean();
	    sqlSessionFactory.setDataSource(dataSource());
	    return (SqlSessionFactory) sqlSessionFactory.getObject();
	  }

}
~~~

- test.java

~~~
package base.toy.project;

import static org.junit.Assert.*;

import java.sql.Connection;

import javax.sql.DataSource;

import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;

import base.toy.config.RootConfig;
import lombok.Setter;
import lombok.extern.log4j.Log4j;

@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = {RootConfig.class})
@Log4j
public class test {

	  @Setter(onMethod_ = { @Autowired })
	  private SqlSessionFactory sqlSessionFactory;

	  @Test
	  public void testMyBatis() {

	    try (SqlSession session = sqlSessionFactory.openSession();
	       Connection con = session.getConnection();) {
	      log.info(con);
	      

	    } catch (Exception e) {
	    	log.info("실패"+e.getMessage());
	      fail(e.getMessage());
	    }

	  }
}
~~~

### 커넥션 풀
- 여러명의 사용자를 동시에 처리해야하므로 커넥션 풀을 사용해 미리 접속을 만들어두는 것이 좋다.
- HikariCP 사용
- pom.xml

~~~
<dependency>
	<groupId>com.zaxxer</groupId>
	<artifactId>HikariCP</artifactId>
	<version>2.7.4</version>
</dependency>
~~~

- DataSource가 HikariConfig를 사용하는 것으로 변경
- SqlSession Connect 시 성공

~~~
@Bean
public DataSource dataSource(){
	  HikariConfig hikariConfig = new HikariConfig();
	  hikariConfig.setDriverClassName("org.mariadb.jdbc.Driver");
	  hikariConfig.setJdbcUrl("jdbc:mariadb://localhost:3310/test");
	  hikariConfig.setUsername("test");
	  hikariConfig.setPassword("1234");
	
	  HikariDataSource dataSource = new HikariDataSource(hikariConfig);
	return dataSource;
}
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

