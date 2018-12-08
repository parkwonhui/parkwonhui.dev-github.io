---
layout: post
title: git,eclipse 연동
categories: [git]
tags: [java,git,eclipse]
comments: true
---

### 이클립스, git 연동 방법
1. 이클립스 메뉴 Window-Show View-Git Repositories 선택
2. Clone a Git repository 선택
3. URI에 자신이 내려받을 프로젝트 주소를 넣는다
4. Next, Finish를 눌러 Git연동을 완료한다
5. Git Repositories에 있는 방금 프로젝트를 오른쪽 마우스 클릭하여 import projects 메뉴를 클릭한다
6. Import as general project 선택
7. 프로젝트 창으로 가져오기 성공

### 에러
- git연동 프로젝트가 빌드되지 않는 상황 발생
- classpath를 커밋하지 않아,  classpath(빌드path)가 없던게 원인. classpath를 커밋하고 ignore에 추가해서 해결



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
                            