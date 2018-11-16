---
layout: post
title: Unresolved compilation problem
categories: [java]
tags: [java,error]
comments: true
---

### Unresolved compilation problem 에러

### 에러

~~~
Exception in thread "main" java.lang.Error: Unresolved  compilation problem:
     at fileread.Main.main(Main.java:14)
~~~

### 상황
어떤 소스코드를 내 프로젝트에 포함시키고 나서 빌드하니 에러가 났다<br>

### 해결
소스코드에 현재 package를 추가하지 않아서 난 에러였다<br>
소스코드에 package 키워드로 패키지를 포함하니 해결되었다<br>

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
                            