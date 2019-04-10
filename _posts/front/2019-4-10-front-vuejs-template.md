---
layout: post
title: Vue.js template
categories: [front]
tags: [front, vuejs]
comments: true
---
### Vue 템플릿
- {{}}를 사용하고 중간에 el 속성이나 자바스크립트 문법 사용
- 간단한 문법만 사용할 것
- if문은 사용하면 안됨.

~~~
<body>
<div id="test">
    <div>{{ new Date() }}</div>
    <div>{{ 1 + 1 }}</div>
    <div>{{ 1 ? '1이다' : '0이다' }}</div>
</div>
</body>
<script>
new Vue({
  el: '#test'
})
</script>
~~~

### v-html
- 아래 예제를 실행하면 a 태그를 사용해서 링크를 걸었지만 그냥 일반텍스트로 출력된다
- {{}}는 일반 텍스트만 해석. 실제 html을 사용하고 싶을 땐 v-html 사용 해야한다.

~~~
<body>
<div id="test">
{{url}}
</div>
</body>
<script>
new Vue({
  el: '#test',
  data:{ url : "<a href='http://www.naver.com'>네이버</a>"}
})
</script>
~~~
- el 설정이 된 하위 dom에서 v-html 태그 속성을 사용해야 url링크가 적용된다

~~~
<body>
<div id="test">
<div v-html="url"></div>
</div>
</body>
~~~
- 그 외 v-if, v-for, v-bind, v-text, v-on 등 다양한 문법이 있다
- v-if는 if문처럼 true, false 결과를 전달한다
- v-on은 클릭했을 때 데이터를 갱신시킬 수 있음
- v-for은 data를 list 형태로 보여줌

~~~
<body>
<div id="test">
<div v-if="1 == 1"> 표시됨 </div>
<div v-if="1 == 0"> 표시안됨 </div>

<div v-text="text">text</div>
<button v-on:click="text='클릭 했습니다'">클릭하면 글자가 바뀝니다</button>

<ul>
    <li v-for="value in list">
        {{ value }}
    </li>
</ul>
</div>
</body>
<script>
var vue = new Vue({
  el: '#test',
  data:{ text : "클릭 안했어요",
  list :["apple","banana","grape"]}
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
