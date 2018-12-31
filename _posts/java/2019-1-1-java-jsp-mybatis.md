---
layout: post
title: mybatis
categories: [java]
tags: [java,jsp,mybatis]
comments: true
---
# MyBatis
### MyBatis란
- 프레임워크란 잘 짜여진 하나의 틀
- 일관성 있는 코드를 사용할 수 있다
- Low Level의 고민들을 개발자가 고민하지 않아도 된다(핵심 비즈니스 로직에 집중)
- jpa,hibernate
- db에 쉽게 접근하고 데이터를 쉽게 가져오기 위해 사용(jdbc)
- Row의 결과값을 가지고 자바 오브젝트를 매핑을 한다

### Object Relational Mapping(ORM) Framework
- jpa, hibernate
- 각 테이블과 1:1 매칭관계
- 테이블과 테이블이 join되면 실제 자바 오브젝트도 join되어야 함

### MyBatis 정보
- mybatis-config.xml 에 MyBatis의 모든 정보가 들어가 있음
- mybatis-config.xml에 있는 정보를 가져오고 sqlSession 정보를 뽑는다. 그리고 Mapping한 함수를 호출해서 query를 실행시킨다


### Mapper방식
- 고유한 이름으로 메서드를 만드는 방식
- xml파일을 추가하고 각 함수에 따라 query문을 만든다. interface도 추가해서 함수를 정의한다

### JSTL
- DB에서 조건문을 주지 않고 JSTL 문을 사용할 수 있다


### MyBatis 라이브러리 추가
- mybatis-3.2.6.jar tomcat lib 폴더에 추가(프로젝트 폴더서 추가되었는지 확인할 것)


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
                            
