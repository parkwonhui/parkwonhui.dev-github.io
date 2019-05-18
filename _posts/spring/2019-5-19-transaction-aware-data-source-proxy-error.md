---
layout: post
title: TransactionAwareDataSourceProxy Error
categories: [spring]
tags: [spring,error]
comments: true
---

# NoClassDefFoundError TransactionAwareDataSourceProxy Error
- db 접속 테스트 코드 실행 시 발생
- TransactionAwareDataSourceProxy class 를 찾을 수 없어서 나는 에러
- TransactionAwareDataSourceProxy는 spring-jdbc안에 있다.
- 현재 프로젝트의 spring-jdbc 버전에서 TransactionAwareDataSourceProxy가 없는 듯
그래서 현재 버전인 5.1.5.RELEASE 에서 5.1.4.RELEASE 로 바꿔주었더니 잘 되었다.
- 진짜 5.1.5.RELEASE에 TransactionAwareDataSourceProxy가 선언안되어 있거나
다른 라이브러리랑 충돌나서 TransactionAwareDataSourceProxy를 인식하지 못하는 듯.

~~~
Caused by: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'sqlSessionFactory' defined in base.toy.config.RootConfig: Bean instantiation via factory method failed; nested exception is org.springframework.beans.BeanInstantiationException: Failed to instantiate [org.apache.ibatis.session.SqlSessionFactory]: Factory method 'sqlSessionFactory' threw exception; nested exception is java.lang.NoClassDefFoundError: org/springframework/jdbc/datasource/TransactionAwareDataSourceProxy
~~~

- pom.xml

~~~
<!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-jdbc</artifactId>
	<version>5.1.4.RELEASE</version>
</dependency>
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


