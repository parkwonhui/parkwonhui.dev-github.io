---
layout: post
title: JavaScript 함수,클로저
categories: [front]
tags: [basic,js,javascript]
comments: true
---

### 사용자 정의 함수
- 프로그램 내에서 사용자가 직접 정의한 기능함수
- 함수를 변수에 넣을 수 있다

~~~
function add(a, b){        // 선언적 함수
       var sum = a+b;
       return sum;
}
console.log("add:"+add(1,2));
~~~

### 익명함수
- 익명함수는 함수의 이름이 없는 함수. 변수에 넣어서 사용
- 익명함수를 만들기 전에 변수를 호출하면 에러(아직 함수 생성전이므로.. 익명함수는 순서중요! 선언적 함수는 순서x)

~~~
var add2 = function(a, b){    // 익명 함수
       var sum = a+b;
       return sum;
}
console.log("add2:"+add2(10,20));
~~~

### 함수 호출 범위
- 전역, 지역에 같은 이름의 변수가 있을 경우, 지역변수를 우선으로 호출한다
- 전역변수를 호출하고 싶다면 변수 앞에 this.를 붙인다

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script type="text/javascript">
var myVar = "전역변수";
function myFunc(){
       var myVar = "지역변수";
       document.write("지역변수:"+myVar);
       document.write("전역변수:"+this.myVar);
}
myFunc();
</script>
</head>
<body>
</body>
</html>
~~~

### 콜백함수
- 매개변수로 전달하는 함수는 콜백함수

~~~
//함수를 선언합니다
function callTenTimes(callback){
       // 매개변수로 전달된 함수를 호출합니다
       for(var i = 0; i < 10; ++i)
             callback();
}
// 변수를 선언합니다
var callback = function(){
       alert('함수 호출');
};
// 함수를 호출합니다
callTenTimes(callback);
~~~

### 클로저(closure)
- 함수가 종료된 후에도 함수내에 있던 지역변수를 사용하고 싶을 때 활용
- 아래 예제에서 지역변수 add가 num을 계속 사용하고 있으므로 num 변수는 메모리에서 사라지지 않는다

~~~
function funcAdd(){
       var num = 100;
       function add(addNum){
             console.log(addNum+num);
       }
       return add;
}
funcAdd()(4);
~~~

### 내장함수
- setTimeout : 일정 시간 후 함수를 한번 실행
- setInterval : 일정 시간마다 함수를 반복해서 실행
- encodeURIComponent : 문자 대부분을 모두 인코딩


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
                            