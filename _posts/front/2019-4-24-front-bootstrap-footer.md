---
layout: post
title: footer 하단에 고정시키기
categories: [front]
tags: [html,front,bootstrap]
comments: true
---

### footer 하단에 고정시키기
- footer를 하단에 고정시키지 않으면 contents의 내용이 끝나고 나서 바로 footer가 온다.
- contents의 길이가 어느정도 있도록 보여야 한다.
- footer에 absolute로 위치를 고정시키고 footer위 height 만큼 contents(본문)쪽에 bottom padding 을 준다
- css
~~~
html,
body {
     margin:0;
     padding:0;
     height:100%;
}
.contents-wrap {
     min-height:100%;
     position:relative;
     padding-bottom:100px;/* footer height */
}
.footer {
     width:100%;
     height:100px;
     position:absolute;
     bottom:0;
     background:#5eaeff;
    text-align: center;
    color: white;
}
~~~
- html

~~~
<%@ page language="java" contentType="text/html; charset=utf-8"
     pageEncoding="utf-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%>
<!DOCTYPE html>
<html lang="ko">
<head>
<link rel="stylesheet" type="text/css"  href="/resources/css/common.css">
<script src="http://code.jquery.com/jquery-3.1.1.js"></script>
<sitemesh:write property='head' />
<!-- CSS -->
<link rel="stylesheet"  href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"  integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
<link rel="stylesheet"  href="https://use.fontawesome.com/releases/v5.8.1/css/all.css"  integrity="sha384-50oBUHEmvpQ+1lW4y57PTFmhCaXp0ML5d60M1M7uH2+nqUivzIebhndOJK28anvf" crossorigin="anonymous">
</head>
<body>
     <div class="container contents-wrap">
           <div class="row">
                <div class="top-menu-list pull-right">
                     <c:choose>
                           <c:when test="${not empty  userVO.id}">
                                ${userVO.name} 님 환영합니다
                                <span  id="user-logout-button">로그아웃</span>
                                
                                
                           </c:when>
                           <c:otherwise>              
                                <a  href="/user/loginForm">로그인</a>
                                <a  href="/user/createUserForm">회원가입</a>
                           </c:otherwise>
                     </c:choose>
                </div>
           </div>
           
           <div class="row constants-top-menu">
                <div class="col-md-3 col-xs-3"><a  href="/main">메인화면</a></div>
                <div class="col-md-3 col-xs-3"><a  href="/board/list?page=1&count=10">게시판1</a></div>
                <div class="col-md-3 col-xs-3">게시판2</div>
                <div class="col-md-3 col-xs-3">게시판3</div>
           </div>
           
           <sitemesh:write property='body' />
           <footer class="footer">
                <div>Basic Board</div>
                <div>@ 2019 wonhui Park</div>
                <i class="fab fa-java fa-2x"></i><i class="fab  fa-html5 fa-2x"></i><i class="fab fa-github-alt fa-2x"></i>
           </footer>
     </div>
     <script type="text/javascript"  src="/resources/js/common.js"></script>
</body>
</html>
~~~

### LoginForm 만들 때 팁
- div로 배경화면에 색상을 넣어 LoginForm을 만들면 ui와 form의 여백이 없이 딱 맞게 만들어진다
- 공간이 있어야 하는데 bootstrap을 사용하면 flex가 많아서 padding, margin이 잘 안먹는다.
- 이럴 때 요소에 padding, margin 을 준다. 예를들어 button의 margin을 주면 margin만큼 여백이 들어선다


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