---
layout: post
title: Vue.js 소개
categories: [front]
tags: [front, vuejs]
comments: true
---

### Vue.js란?
- 사용자 인터페이스를 만들기 위한 프레임워크
- ECMAScript5 기능을 사용하여 ECMAScript 5 호환 브라우저 지원(IE8 이하 버전 미지원)
- 단일 프레임 워크와 달리 다른 라이브러리와의 통합이 쉬움
- [vue.js 한글번역문서](https://kr.vuejs.org/v2/guide/index.html)

### 기본 예제
- message가 'Hello Vue.js'라는 단어로 대체되었다
- new로 Vue를 생성. message, text, study 속성을 가진다
- el은 vue 인스턴스와 태그(id)를 연결한다
- data는 vue 내부에서 변수처럼 사용할 수 있는 값
- 지정한 id 안의 dom을 제어할 수 있다. id 안에 존재하지 않는다면 값을 제어할 수 없다
- 생성될 때 있었던 변수만 반응형(예를 들어 vue 생성 시 b 속성이 없다가 후에 만들면 반응형 작동을 하지 않는다)
- dom과 vue 인스턴스를 연결하여 템플릿, 이벤트, 디렉티브, 컴포넌트를 사용한다

~~~
<!-- 도움되는 콘솔 경고를 포함한 개발 버전 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<!-- 상용버전, 속도와 용량이 최적화됨. -->
<!--<script src="https://cdn.jsdelivr.net/npm/vue"></script>-->
</head>
<body>
<div id="app">
  <p>{{ text }}</p>
  <p>{{ study }}</p>
</div>
  <p>{{ study }}</p>
</body>
<script>
new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js!',
    text: 'Hi Vue.js!',
    study: 'Study Vue.js'
  }
})
</script>
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