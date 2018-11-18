---
layout: post
title: port forwarding(포트포워딩)
categories: [server]
tags: [server,portforwarding]
comments: true
---

### 포트포워딩
- 외부에서 공유기로 ip가 할당된 서버에 접속할 수 있도록 접속port번호로 서버 ip, port번호를 매칭시키는 것
- 공유기를 통해 ip를 할당받으면 서버의 외부ip, 내부ip가 다르다
- 서버가 여러대라면 접속요청을 받아도 어느 서버에 요청한 것인지 알 수 없다
- 포트번호로 접속할 서버 ip와 port 번호를 지정해주는 것이 포트포워딩이다.

### 포트포워딩 방법
- cmd 창을 켜서 ipconfig 명령어를 친다. 기본 게이트 웨이 ip를 인터넷창에 친다
- 공유기 설정창이 뜨면 로그인한다 (asus)
-  WAN-가상 서버/포트 포워딩 메뉴 클릭
-  유명한 서버 리스트 http를 선택
- sourcetarget은 허용 ip(없으면 모든 ip 허용)
- 포트 범위는 외부컴퓨터가 접속 요청한 포트
- 로컬 ip는 내 컴퓨터의 내부ip를 적는다
- 로컬 포트는 내부 포트 번호(나는 포트범위와 똑같이 적었다)
- 프로토콜은 웹이지만 tcp
- bitnami로 올린 아파치 server로 외부에서 접속이 잘 되는 것을 확인

~~~
서비스 이름 : HTTP Server
sourcetarget : 비워둠
포트 범위 : 80
로컬 ip : 192.168.1.11
내부 포트 번호 : 80
프로토콜 : TCP
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
                            