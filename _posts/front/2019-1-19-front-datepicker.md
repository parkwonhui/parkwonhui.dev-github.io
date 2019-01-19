---
layout: post
title: jquery datepicker
categories: [front]
tags: [jquery]
comments: true
---

# jquery Datepicker  사용법

### jquery import

~~~
<link href="http://www.jqueryscript.net/css/jquerysctipttop.css"
	rel="stylesheet" type="text/css">
<script
	src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script
	src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
~~~
### 사용법

~~~    
var jb = jQuery.noConflict();
$( function() {
	  jb( "#addDatepickerStart").datepicker({
		  dateFormat: "yy-mm-dd"
});

<div>시작날짜 <input type="text" id="addDatepickerStart" data-date-format='yy-mm-dd' ></div>

~~~


### import multiple jquery 문제
- 여러 jquery버전을 사용하면 충돌이 발생해서 함수를 못찾는 에러발생
- jquery 사용 범위를 정해놓고 사용 해야한다
- jquery import 후 해당 jquery를 이용하는 코드를 작성한다. 그리고 script를 닫은 후 다른 jquery 를 import한다. 그리고 방금 import 한 jquery만 사용한다
- '$'을 쓰지말고 noConflict 함수로 해당 jquery를 사용해야한다

~~~
<script src="https://code.jquery.com/jquery-1.12.4.js"></script>
<script src="https://code.jquery.com/ui/1.12.1/jquery-ui.js"></script>
<script>
var jb = jQuery.noConflict();
$( function() {
	  jb( "#editDatepickerEnd").datepicker({
		  dateFormat: "yy-mm-dd"
	  });
});
</script>
<script
	src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script>
$('#clickbutton').function({
});
<script>
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
                            
