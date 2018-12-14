---
layout: post
title: JavaScript dom
categories: [front]
tags: [basic,js,javascript,dom]
comments: true
---
### 브라우저 관련 객체
- 웹 브라우저와 관련된 객체 집합
- Window 객체 : 인터넷창과 관련된 객체 정보
- Screen 객체 :  운영체제 화면의 속성을 갖는 객체
- Location 객체 : 웹브라우저의 주소 표시줄과 관려된 객체, 페이지 이동 시 많이 사용됨
- Navigator 객체 : 웹 페이지를 실행하고 있는 브라우저에 대한 정보
- window는 최상위 객체이므로 window 안붙이고 사용할 수 있다(ex. window.alert() 함수)
- open(URL, 이 인터넷창의 이름(통신할 때 필요), 윈도우 옵션) 
- open : 새로운 window 객체를 생성. 새로운 인터넷 브라우저 창이 열린다
- exam.html

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script type="text/javascript">
function winOpen(){
       window.open('address.html', '주소검색', 'width=200,height=200');  //  자식윈도우 생성
       
}
</script>
</head>
<body>
       <form name="fmt">
       주소:<input type='text' name='addr'>
       <input type="button" value="주소검색" onclick="winOpen()">
</form>
</body>
</html>
~~~
- address.html

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script type="text/javascript">
window.onload = function(){      // html을 다 읽고 난 후에
       var links = document.getElementsByTagName('a');     //  getElementsByTagName : 배열을 리턴함
       for(var i=0; i<links.length; ++i){
             links[i].onclick = function(){
                    window.opener.document.fmt.addr.value = this.innerHTML;
                    self.close();
             }
       }
}
</script>
</head>
<body>
<ul>
<li><a href="#">서울시 강남구 대치동</a></li>
<li><a href="#">서울시 금천구 가산동</a></li>
<li><a href="#">경기도 화성시 능동</a></li>
</ul>
</body>
</html>
~~~

### onload이벤트 속성
- window 객체 로드가 완료되는 때 : 모든 태그가 화면에 올라갔을 때(html 다 읽었을 때)
- html 다 읽었을 때 window.onload 함수 호출
- 아래 예제 실행 시 자바스크립트->body부분->onload 순으로 호출 되는 것을 알 수 있다

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script type="text/javascript">
window.onload = function(){
       alert('Process-event');
}
alert('Process-0')
</script>
</head>
<body>
<h1>Process-1</h1>
<script>alert('process-2')</script>
<h2>Process-2</h2>
<script>alert('process-3')</script>
</body>
</html>
~~~

### DOM
- Document Object Model
- 객체지향 모델로써 구조화된 문서를 표현하는 방식
- set, getAttribute : 속성값으로 설정, 찾기
- innerHTML : 노드의 body에 설정된 값(비표준)
- 아래예제는 set,getAttribute로 object에 접근해서 값을 변경해준다
- nodetype 1은 element 2는attribute 태그의 속성 3은 TEXT이다
- gallary02.html

~~~
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=EUC-KR">
<title>Insert title here</title>
<link rel="stylesheet" href="styles/layout.css" target="text/css">
<script type="text/javascript" src="scripts/showPic.js"></script>
</script>
</head>
<body>
       <h1>gallery</h1>
       <ul id="imagegallery">
             <li>
                    <a href="images/fireworks.jpg" title="A fireworks dispaly"  >
                    <img src="images/thumbnail_fireworks.jpg"  alt="Firewokrs"></img></a>
             </li>
             <li>
                    <a href="images/coffee.jpg" title="A cup of black coffee"  >
                    <img src="images/thumbnail_coffee.jpg"  alt="Coffee"></img></a>
             </li>
             <li>
                    <a href="images/rose.jpg" title="A red red rose">
                    <img src="images/thumbnail_rose.jpg" alt="Rose"></img></a>
             </li>
             <li>         
                    <a href="images/bigben.jpg" title="The famous clock">
                    <img src="images/thumbnail_bigben.jpg" alt="Big  Ben"></img></a>
             </li>
       </ul>
       <img id="placeholder" src="images/placeholder.gif" alt="myImage"/>
       <p id="description">Choose an image</p>
</body>
</html>
~~~
- showPic.js

~~~
function showPic(object){
       console.out('were');
       // 이미지 id가져오기
       var clickhref = object.getAttribute('href');
       var placeholder = document.getElementById('placeholder');
       placeholder.setAttribute('src', clickhref);
       
       // object의 title을 바꿔야 한다
       // obj 어트리뷰트 가져오기
       var title = object.getAttribute('title');
       // image의 정보 가져오기
       var image_info =  document.getElementById('description');
       // innerhtml바꾸기
       //image_info.innerHTML = title;
       if(image_info.firstChild.nodeType == 3){//TEXT는 NODETYPE이 3번
             image_info.firstChild.nodeValue = title;
       }
       return false;
}
function prepareGallery(){
       var imagegallery = document.getElementById("imagegallery");
       var atag = imagegallery.getElementsByTagName('a');
       for(var i = 0; i < atag.length; ++i){
             atag[i].onclick = function(){
                    return showPic(this);
             }
       }
}
window.onload = prepareGallery;
~~~


### 레벨로 객체찾기
- nodeType1은 엘레먼트, nodeType2는 속성, nodeType3은 textnode이다
- nodeType이 3이라면 innerHTML처럼 text를 가르키는 것이다
- innerHTML은 표준이 아니므로 nodeType을 체크해서 text을 바꾸도록 한다

~~~
window.onload = function(){
       var id1 = document.getElementById('id1');
       var id2 = document.getElementById('id2');
       if(id1.firstChild.nodeType == 3)
             id1.firstChild.nodeValue = '안녕';
       if(id2.firstChild.nodeType == 3)
             id2.firstChild.nodeValue = '세상';
}
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
                            

