---
layout: post
title: JavaScript 이벤트2
categories: [front]
tags: [basic,js,javascript]
comments: true
---
### 이벤트
- 키보드, 마우스를 이용해서 입력을 받으면 어떤 이벤트가 발생하는 것을 의미
- 아래 예제는 window 객체에 onload속성에 함수를 할당하고 있다(=이벤트 연결)

~~~
<script type="text/javascript">
window.onload = function(){
       console.log('window onload');
};
</script>
~~~

### 인라인 이벤트
- html 소스코드 안에 이벤트를 정의하는 것
- html와 javascript는 따로 있어야함. 인라인 이벤트는 사용x

~~~
function doProcess(){
       var result = document.getElementById("result");
       result.innerHTML = "<span>이벤트 결과</span>";
}
</script>
</head>
<body>
<input type="button" value="버튼1" onclick="doProcess()">
<input type="button" value="버튼2">
<div id="result"></div>
~~~

### 고전 이벤트
- javascript에서 이벤트를 추가하는 방식
- onload 함수는 dom이 완성된 후 호출됨(html을 다 읽고나서)
- 보통 javascript 파일을 만들고 안에서 처리한다
- javascript 링크를 잘 걸었는지 확인하는 법 ctrl+위에 마우스 대면 손가락 모양으로 바뀜. 잘못하면 안바뀜
- this를 사용하면 이벤트를 호출한 객체를 알 수 있다

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script type='text/javascript'>
window.onload = function(){
  //변수 선언
  var event = document.getElementById('clickButton');
  // 이벤트 연결
  event.onclick = function(){
    alert('클릭');
  };
};
</script>
</head>
<body>
<input type ="button" id="clickButton" value = "버튼">
</body>
</html>
~~~

### 이벤트 리스너
- 이벤트 리스너는 하나의 행동에 여러 이벤트가 일어나게 할 수 있음

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>

<script>

window.onload = function(){
function clickEvent(){
  alert("클릭!");
}

function updateValue(event){
  this.value = '눌렀다';
}

var btn = document.getElementById("btn");
btn.addEventListener("click", clickEvent);
btn.addEventListener("click", updateValue);
}

</script>
</head>
<body>
  <input type="button" id="btn" value="button"/>
</body>
</html>
~~~

### 디폴트 이벤트 제거
- 일부 HTML 태그는 이미 이벤트 리스너 존재
- 기본 이벤트 방식이 마음에 안들어 제거하고 싶을 때 사용
- 이벤트 리스너에서 false 리턴 시 제거


### 이벤트 버블링
- 이벤트 버블링은 자식->부모로 이벤트가 흘러감
- 캡쳐링은 반대로 부모->자식 순으로 이벤트가 실행됨(익스플로, jquery 캡쳐링 지원x)
- 아래 예제 실행 시 Paragraph 만 클릭해도 모든 이벤트가 실행됨
- 이벤트 버블링을 막는 방법은 event인자의 cancelBubble을 true로 주고 event의 stopPropagation()함수를 호출하는 것
- 이벤트 버블링 수정 전(부모 이벤트까지 호출)

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
*{border:3px solid black;}
</style>
<script>
</script>
</head>
<body>
  <div onClick="alert('outer-div')">
    <h1 onclick="alert('header')">
      <p onclick="alert('paragraph')">Paragraph</p>
    </h1>
  </div>
</body>
</html>
~~~
- 이벤트 버블링 수정 후(자신의 이벤트만 호출)

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
*{border:3px solid black;}
</style>
<script>

var paragraph_func = function paragraphfunc(e){
  var event = e || window.event;

  // 이벤트 발생을 알립니다
  alert('paragraph');
  // 이벤트 전달을 제거합니다
  event.cancelBubble = true;
  if(event.stopPropagation){
    event.stopPropagation();
  }
}

var header_func = function headerfunc(e){
  var event = e || window.event;

  // 이벤트 발생을 알립니다
  alert('header');
  // 이벤트 전달을 제거합니다
  event.cancelBubble = true;
  if(event.stopPropagation){
    event.stopPropagation();
  }
}

</script>
</head>
<body>
<div onClick="alert('outer-div')">
  <h1 onclick='header_func(event);'>
    <p onclick='paragraph_func(event);'>Paragraph</p>
  </h1>
</div>
</body>
</html>
~~~

### 표준 이벤트 모델
- 구형 웹브라우저에서는 이벤트 리스너가 동작하지 않는다
- 어느 웹브라우저라도 동일한 동작을 하게 만들어줘야 한다

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>

<script>
window.onload = function(){
    var header = document.getElementById('my-header');
    if(header.attachEvent){ // 구형 버전은 attach. 존재한다면 구형이란 뜻. 신형은 eventListener
      // 인터넷 익스플로러의 경우 실행
      var hanndler = function(){
        window.event.srcElement.style.color = 'red';
        window.event.srcElement.detachEvent('onClick', handler);
      };
      header.attachEvent('onClick', handler);
    }else {
      // 그 이외의 브라우저에 실행합니다
      var handler = function(){
        this.style.color = 'red';
        this.removeEventListener('click', handler);
      };
      header.addEventListener('click', handler);
    }
}
</script>
</head>
<body>
  <h1 id = "my-header">Click</h1>
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
                            

