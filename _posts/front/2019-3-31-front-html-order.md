---
layout: post
title: html 페이지 로딩 순서
categories: [front]
tags: [front, html]
comments: true
---

### HTML 페이지 로딩 순서

- html, Javascript, jsp 등.. 은 인터프리터 언어이다. 그러므로 위에서부터 아래로 순서대로 실행된다
- import -> head 태그 - > <body>태그 -> body onload -> window.onload 
- jsp 파일 일 때는 jsp 사용 부분부터 먼저 실행되고 html 부분이 실행된다
- 아래 예제를 실행하면 콘솔창에 head, body, 아래 스크립트, onLoad 순으로 출력되는 것을 확인할 수 있다

~~~

<script>
console.log('head');
</script>
</head>
<body>
<script>
console.log('body');
</script>

</body>
<script>
$(function(){
console.log('onLoad');
});
console.log('아래 스크립트');
</script>

~~~

### CSS, JavaScript 위치

- CSS는 <head>태그 안에 있어야 한다. 왜냐하면 스타일 규칙이 있어야 랜더링을 할 수 있기 때문에 빠르게 알기 위해서이다.
- JavaScript는 <body> 태그 맨 아래에 넣는다.  <head>태그 안에 있다면 랜더링을 멈추고 JavaScript를 읽기 때문에 화면 랜더링이 오래걸릴 수 있다.

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