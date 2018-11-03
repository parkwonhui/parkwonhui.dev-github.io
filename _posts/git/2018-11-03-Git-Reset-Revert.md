---
layout: post
title: Git Reset, Revert
categories: [git]
tags: [git,gitcli]
comments: true
---
### reset
- git reset version --option
- 특정 상황으로 되돌아가고 싶을 때 사용. version 이후 커밋은 사라진다(로그에도 reset했다는 내용이 남지 않음)
- --option은 hard, mix, soft가 있다
- <b>reset은 내 컴퓨터에 있는 작업일 경우에만 해야한다. 원격 저장소에 올려져있는 내용을 하면 안됨</b>

### revert
- git revert version id
- revert하면 reset과 달리 새로운 version이 생긴다
- 현재version <-> 되돌아간 verison 사이에 변경 된 파일이 working copy 에 들어가는 것 같다
- revert 로그가 바로 보이지 않고 해당 파일 수정 후 커밋해야 한다
- 충돌했는지 꼭 해당 파일을 확인할 

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
                            