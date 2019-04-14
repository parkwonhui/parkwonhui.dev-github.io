---
layout: post
title: Vue.js computed, methods, watch
categories: [front]
tags: [front, vue.js]
comments: true
---

## Vue.js computed, methods, watch

### computed 속성
- 템플릿 {{}} 안에 간단한 코드를 넣는 것이 좋다
- {{ 20 % 2 == 0 ? '짝수' : 홀수 }} 이 소스는 복잡하다. 간단하게 표현할 수 있는 Computed 속성을 사용해야 한다
- computed 속성에 함수를 정의한 후 {{}} 안에 호출하면 된다

~~~
<div id="test">
  {{checkEvenNumber}}
</body>
<script>
new Vue({
  el: '#test',
  computed: {
    checkEvenNumber: function(){
        return 20 % 2 == 0 ? '짝수' : '홀수';
    }
  }
})
</script>
~~~
- computed는 캐싱을 사용하여 저장된 곳에 변경사항이 있을 때만 함수를 실행.
- method는 렌더링을 다시 할 때 마다 함수를 실행

### vue.js 메소드
- method 속성에 사용자 정의 함수를 선언하는 것

~~~
<div id="test">
    <h1> {{firstNum}} 더하기 {{secondNum}}는 {{addNum(firstNum, secondNum)}} 입니다</h>
    <h1> {{firstNum}} 빼기 {{secondNum}}는 {{MinusNum(firstNum, secondNum)}} 입니다</h>
</div>
</div>
</body>
<script>
var memberData = {
    firstNum : 10,
    secondNum : 20
};
var memberMethod = {
    addNum : function(num1, num2){
        return num1 + num2;
    },
    MinusNum : function(num1, num2){
        return num1 - num2;
    }
}
var option = {
    el : '#test',
    data : memberData,
    methods : memberMethod
};

var vue = new Vue({
    el : '#test',
    data : memberData,
    methods : memberMethod
});
~~~

### watch
- 변경을 감시하고 변경됨에 따라 실행할 동작을 정의
- computed는 호출한 함수를 실행하는 것이고 watch는 어떤 동작을 감시하여 변경될 때 동작을 실행함(트리거)
- 멤버변수를 더하는 것은 행위를 실행하는 함수이므로 computed를 사용한다
- 더한 결과값이 바뀔 때마다 추가적인 동작을 하고 싶다면 watch를 사용한다

~~~
<div id="test">
제 이름은 {{myName}} 입니다 <br>
<input v-model="myName">
</div>
</body>
<script>
var vm = new Vue({
  el: '#test',
  data: {
    myName: 'wwwwww',
    text: '변경 전입니다'
  },
  watch: {
    myName: function (val) {
        text = '이름이'+this.myName+'으로 변경되었습니다';
    }
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