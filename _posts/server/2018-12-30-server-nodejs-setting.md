---
layout: post
title: node.js 개발환경 구축
categories: [server]
tags: [server,nodejs]
comments: true
---
# Nodejs 개발환경 구축
### Node.js란
- 브라우저가 아닌 서버 환경에서 javascript를 사용할 수 있게 해줌
- 이벤트방식과 비동기식. 어떤 이벤트가 발생할 때 처리하며, 처리를 하기 위해 서버가 멈추지 않음(callback함수)=>속도향상

### Node.js 설치
download url : https://nodejs.org/ko/

### Node.js 예제
- server.js 파일을 만들고 아래와 같이 소스코드를 작성한다
- 작성 후 cmd 창을 열고 해당 소스코드가 있는 폴더로 이동한다
- cmd 창에 node server.js 라고 입력한다
- http://127.0.0.1:52273/ 주소로 들어가면 Hello World...! 라는 글을 볼 수 있다

~~~
// 모듈 추출
var http = require('http');

// 웹 서버를 만들고 실행
http.createServer(function(request, response){
    response.writeHead(200, {'Content-Type': 'text/html'});
    response.end('<h1>Hello World...!</h1>');
    
}).listen(52273, function(){
    console.log('Server running at http://127.0.0.1:52273/');    
});
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
                            