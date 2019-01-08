---
layout: post
title: mybatis error
categories: [java]
tags: [java,jsp,mybatis]
comments: true
---

### Mybatis 에러 정리

##### Error  registering typeAlias for 'Board 에러

~~~
Error building SqlSession.
The error may exist in SQL Mapper Configuration
Cause: org.apache.ibatis.builder.BuilderException: Error parsing SQL  Mapper Configuration. Cause: org.apache.ibatis.builder.BuilderException: Error  registering typeAlias for 'Board'. Cause:
~~~
- MyBatis Config에 typeAliases에 선언된 class를 찾을 수 없다는 에러. 확인해보니 Config 에서 class명을 잘못적어서 수정하였다

##### 부적합한 열 유형 1111 에러

~~~
g.apache.ibatis.exceptions.PersistenceException:
Error updating database.  Cause: org.apache.ibatis.type.TypeException: Error setting null for parameter #1 with JdbcType OTHER . Try setting a different JdbcType for this parameter or a different jdbcTypeForNull configuration property. Cause: java.sql.SQLException: 부적합한 열 유형: 1111
~~~
- servlet에 넘어온 데이터가 NULL이었고 NULL 데이터를 사용하려고 해서 발생

##### invalid character 에러

~~~
Error updating database.  Cause: java.sql.SQLSyntaxErrorException:  ORA-00911: invalid character
The error may involve kosta.mapper.BoardMapper.insertBoard-Inline
The error occurred while setting parameters
SQL: insert into board values(board_seq.nextval, ?, ?, ?, sysdate, 0);
Cause: java.sql.SQLSyntaxErrorException: ORA-00911: invalid character
~~~
- db 쿼리문 끝에 세미콜론(;)을 붙임

##### The Network Adapter could not establish the connection

~~~
The error may exist in kosta/mapper/Board.xml
The error may involve kosta.mapper.BoardMapper.selectList
The error occurred while executing a query
Cause: java.sql.SQLException: Cannot create PoolableConnectionFactory (IO  오류: The Network Adapter could not establish the connection)
~~~
- 오라클 서비스가 꺼져있었다



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
                            
