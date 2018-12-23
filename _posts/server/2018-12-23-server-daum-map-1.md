---
layout: post
title: 다음지도 key 등록(kakao map)
categories: [server]
tags: [server,openapi]
comments: true
---

# 다음 지도 API
### 어플리케이션 생성
- daum지도 사용 참고
- http://apis.map.daum.net/web/guide/#step3
- [kakao developers](https://developers.kakao.com) 에서 회원가입
- map을 선택하고 어플리케이션 생성
- 내 계정에서 map 선택 후 설정-일반-플랫폼-플랫폼 추가 선택
- 도메인 추가(http://localhost:8080)

### 좌표로 지도 출력
~~~
<!DOCTYPE html>
<html>
<head>
       <meta charset="utf-8"/>
       <title>Daum 지도 시작하기</title>
</head>
<body>
       <div id="map" style="width:500px;height:400px;"></div>
       <script type="text/javascript"  src="//dapi.kakao.com/v2/maps/sdk.js?appkey=인증키"></script>
       <script>
              var container = document.getElementById('map');
              var options = {
                     center: new daum.maps.LatLng(33.450701, 126.570667),
                     level: 3
              };
              var map = new daum.maps.Map(container, options);
       </script>
</body>
</html>
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
                            