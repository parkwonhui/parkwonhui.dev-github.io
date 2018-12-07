---
layout: post
title: Eclipse Web 환경세팅
categories: [db]
tags: [db,html,basic]
comments: true
---
### 톰캣 설정 시 주의사항
- 톰캣 설치 시 마지막 finish 시 체크박스 해제
- 항상 서버가 돌아가는게 아니라 이클립스 사용 시 돌아가도록 체크박스 해제

### 이클립스 설정 변경
- 자바EE로 변경
- window-preference-Server-Runtime E~ - ADD-톰캣버전 선택-톰캣 폴더 추가
- window-preference-WEB 선택. HTML, CSS EUC-KR을 UTF-8로 변경
- 앞으로는 JavaProject가 아닌 Dinamic Web Project 만들기
- WebContent폴더에서 HTML 파일 추가



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
                            


