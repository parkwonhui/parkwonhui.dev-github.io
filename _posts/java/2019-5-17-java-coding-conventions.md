---
layout: post
title: Java Coding Conventions 
categories: [java]
tags: [java,conventions]
comments: true
---

# Java Coding Conventions 
- 프로젝트 란에 노란 느낌표 있는지 확인(ctrl+o로 정리)
- Java Conding Convertions는 ctrl+f로 정리 가능
- logger.info 삭제(자바 로그 정리)
- System.out.println 삭제
- 사용안하거나 필요 없는 console.log, alert 삭제
- 괄호 다음을 띄운다
- if( 를 if ( 로 수정
- else if( 를 else if ( 로 수정
- }else if 를 } else if 로 수정
- else{ 를 else ( 로 수정
- }else 를 } else 로 수정
- for(  를 for ( 로 수정
- }( 을 ) { 로 수정
- + 검색해서 안띄워져 있으면 띄위기(xml 에도 적용할 것)
- true, false 는 true는 없애고 false는 ! 로 수정
- private인데 public으로 접근제어자 사용하지 않았는지 체크!
- naming 알맞게 짓기
- 자료형에 기반한 네이밍을 하지 않는다. 예를들어 List<String> userList 였다가 Map 으로 바뀌면 userMap으로 네이밍을 다시 해줘야한다
- 불필요한 코드나 java대신 xml로 간단하게 처리할 수 있는지 확인하기

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

