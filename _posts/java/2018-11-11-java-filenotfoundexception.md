---
layout: post
title: FileNotFoundException Solve
categories: [java]
tags: [java,error]
comments: true
---

### 상황
txt파일을 읽기위해 소스코드와 같은 위치에 txt파일을 넣은 후<br>
FileReader 객체로 파일읽기를 하니 java.io.FileNotFoundException 런타임 에러가 났다<br>

### 해결
txt파일을 소스코드와 같은 위치가 아니라 해당 프로젝트 최상단에 넣어야 한다<br>
예를들어 프로젝트 이름이 JavaEx라면 JavaEx 폴더에 넣어야 한다<br>
.classpath,.project, src폴더, bin폴더가 있는 곳이 최상단 폴더이다<br>


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
                            