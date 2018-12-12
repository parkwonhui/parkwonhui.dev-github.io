---
layout: post
title: JavaScript 객체,생성자
categories: [front]
tags: [basic,js,javascript]
comments: true
---
### 캡슐화
- function 밖에서 일반 인자에 직접 접근이 가능하다
- 인자에 직접 접근하지 못하게 만들려면 this를 뺀다 
- 멤버변수에는 this를 빼고, 함수에서 this를 붙여준다
- 캡슐화 후 멤버변수 값을 가져오지 못하는 것을 확인할 수 있다

~~~
// 생성자 함수
function Student(n){
       this.stname = n;
       this.getstName = function(){return this.stname;}
       this.setstName = function(n){    this.stname = n;};  
}
var st = new Student("강하나");
alert(st.getstName());
alert(st.stname);
~~~

- 캡슐화 후
~~~
// 생성자 함수
function Student(n){
       var stname;
       
       this.getstName = function(){return this.name;}
       this.setstName = function(n){    this.name = n;};    
}
var st = new Student("강하나");
alert(Student.getstName());
alert(Student.stname);
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
                            