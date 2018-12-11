---
layout: post
title: JavaScript Event
categories: [front]
tags: [basic,js,javascript]
comments: true
---

### Javascript
- Java와 문맥이 비슷한 프로그래밍 언어
- Javascript는 html과 함께 클라이언트로 다운로드하여 실행할 수 있음
- 인터프리터 언어
- HTML과 같이 플랫폼 독립성
- HEAD, BODY 어디서든 선언 가능

### 문법
- null과 undefined
- undefined는 아예 값이 할당되지 않은 상태. null은 값이 없다는 의미
 - parseInt : 문자열을 숫자로 변환함

### 주석
- 자바와 똑같이 //, /**/을 주석으로 사용한다

~~~
/* 주석1 */
// 주석2
~~~

### 이벤트 
- 유저가 어떤 동작을 하면 웹이 상호작용하여 이벤트가 호출된다
- 아래 예제에선 유저가 버튼 클릭을 하면 (onclick) kosta3 함수가 호출되는 것이다
- common.js

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script type='text/javascript' src='common.js'></script>
</script>
</head>
<body>
<form>
<input type ="button" value = "버튼" onclick="kosta3()">
</form>
</body>
</html>
~~~

- 알림창, 문서출력, 콘솔창 출력

~~~
function kosta3(){
       // 알람 함수
       alert('kosta3');
       // 문서에 출력
       document.write('<b>KOSTA3</b>');
       // 콘솔창에 출력
       console.log('kosta3');
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
                            