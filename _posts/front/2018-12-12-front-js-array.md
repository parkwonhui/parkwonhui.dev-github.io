---
layout: post
title: JavaScript Array,내장객체
categories: [front]
tags: [basic,js,javascript]
comments: true
---
### Array 객체
- slice : Array 객체의 지정한 위치에서 발췌하여 새로운 배열변수를 만듬
- splice : 특정요소를 삽입하거나 제거
- 배열 선언 3가지 방법

~~~
var arr = [];
arr[0] = 1;
arr[1] = 2;
var arr2 = new Array(2);
arr2[0] = 1;
arr2[1] = 2;
var arr3 = new Array(1,2);
~~~

### 문자열 함수
- arr.toString() : 배열의 요소를 출력(각 요소마다 ,콤마로 나뉘어져 있다)

~~~
document.write(arr1.toString());
~~~
- arr.join(콤마대신 사용할 요소) : 콤마 대신 사용할 요소가 찍힌다. 예를들어 콤마를 없애고 싶다면 " "를 넣어준다

~~~
document.write(arr.join(" "));
~~~

- slice(startIndex, endIndex) : 시작 인덱스부터 끝 인덱스 앞 인덱스 까지 단어를 자른다

~~~
var arr = [];
for(var i = 0; i < 10; ++i){
       arr[i] = i;
}
var arr2 = arr.slice(1,3);
document.write(arr.toString()+"<br>");
document.write(arr2.toString()+"<br>");
~~~

- concat : 문자열 붙이기

~~~
var arr = new Array(1,2,3);
var arr2 = new Array(4,5,6);
document.write(arr2.concat(arr));
~~~

### setTimeout
- setTimeout("함수이름", ms);
- 첫번째 인수인 함수를 일정 시간 후에 한번 호출한다

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script type="text/javascript">
var timeid;
var flag = 0;             // 0이면 안돔 1이면 도는 중
function show(){
       var now = new Date();
       var hour = now.getHours();
       var minute = now.getMinutes();
       var seconds = now.getSeconds();
       var timeValue = hour + "시" + minute + "분" + seconds + "초";
       
       document.fmt.display.value = timeValue;
       
       timeid = setTimeout("show()",1000);
}
function startClock(){
       if(0 != flag)
             return;
       flag = 1;
       show();
       console.log("startClock timeid:"+timeid);
       
}
function stopClock(){
       if(1 != flag)
             return;
       flag = 0;
       console.log("end timeid:"+timeid);
       clearTimeout(timeid);
}
</script>
</head>
<body>
<form name="fmt">
       <input type="text" name="display">

       <input type="button" name="start" value="시작" onclick="startClock()">
       <input type="button" name="stop" value="종료" onclick="stopClock()">
</form>
</body>
</html>
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
                            