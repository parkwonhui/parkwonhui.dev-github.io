---
layout: post
title: mybatis 게시판 만들기 순서
categories: [java]
tags: [java,jsp,mybatis]
comments: true
---
# 게시판 만들기 정리
### 파일 작성순서
1. xml 파일 작성
2. ado 작성
3. jsp 작성

### 게시물 삭제 추가하기
- 데이터 추가,삭제에 따라 태그명이 달라진다. 삭제 태그명은 delete이다
- xml에 id명(함수명), parameter, return 값을 생각하고 정의한다
- 태그의 id는 ado 함수명과 일치시켜야 한다

~~~
<delete id="deleteContents" parameterType="int">
delete from board where seq = #{seq}
</delete>
~~~
- mapperClass에 삭제 함수선언

~~~
int deleteContents(int seq);
~~~
- dao 삭제 함수 추가

~~~
public int deleteContents(int seq){
SqlSession sqlSession = getSqlSessionFactory().openSession();
int re = -1;
try{
    re =  sqlSession.getMapper(BoardMapper.class).deleteContents(seq);
    if(re > 0){
        sqlSession.commit();
    }else{
        sqlSession.rollback();
    }
}catch(Exception e){
    e.printStackTrace();
}finally{
    sqlSession.close();
}
return re;
}
~~~
- jsp 수정. 삭제 링크를 누르면 게시물이 바로 삭제되도록 한다
- get방식으로 parameter를 전달한다

~~~
<td><a href="delete.jsp?seq=<%= board.getSeq() %>">삭제하기</a></td>
~~~
- 삭제링크 클릭 시 이동하는 delete.jsp 파일을 만든다
- dao 객체의 데이터 삭제 함수를 호출한다.

~~~
<%
int seq = Integer.parseInt(request.getParameter("seq"));
BoardDao2 dao = BoardDao2.getInstance();
int re = dao.deleteContents(seq);
if(re > 0)
       out.println("삭제 성공");
else
       out.println("삭제 실패");
%>
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
                            
