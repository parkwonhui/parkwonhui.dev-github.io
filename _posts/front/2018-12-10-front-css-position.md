---
layout: post
title: CSS position
categories: [html]
tags: [db,html,basic,css]
comments: true
---

### position
- html에서 위치 지정, 객체 보임, 안보임 여부
- static : 기본값으로 일반적인 내용물의 흐름. 상단과 좌측에서의 거리를 지정할 수 없음.
- relative : 상대적인 위치로, top, left 거리르 지정
- absolute : 자신의 상위 box 속에서의 top, left, right, bottom 등의 절대적인 위치를 지정
- fixed :스크롤이 일어나도 항상 지정된 위치에 고정되어있음
- 만약 부모-자식 오브젝트 관계라면 부모 기준으로 자식위치를 설정할 수 있다
- 부모위치 기준일 때 부모는 반드시 position이 relative 속성이여야 한다

### top, left, bottom, right
-  4개의 위치 중 하나를 정해서 px, %(퍼센트)단위 만큼 떨어진 곳에 위치하게 된다
- 예를 들어 top:50px left:50px 일 경우 top, left 각각 50px 떨어진 곳에 위치한다

### float
- float 속성은 박스가 화면의 어느 위치에 배치할 것 인지
설정하기 위해 사용
- left 설정 시 왼쪽에 배치되고, 오른쪽에는 글씨가 올 수 있게 된다

### width, height
- 해당 오브젝트의 길이값을 설정
- px, %(백분율)로 나타낼 수 있습니다

- position, selector 등을 사용하는 예제

~~~
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"  "http://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
<title>레이아웃 연습하기</title>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<style type="text/css">
       
       #menu ul li{
       list-style-type:none;
       display:inline;
       margin-left: 30px;
       }
       
       a{
             text-decoration: none;
       }
       
       #menu ul{
             background: #B9FFFF;
             width:80%;
             position:static;
             margin:50px 1px 50px 1px;
             padding: 50px 1px 50px 1px;
             border-bottom: 1px solid;
             border-top: 1px solid;
       }
       
       #balm{
             float:left;
       }
       #content1{
             float:left;
             width: 40%;
             margin-right: 20px;
       }
       
       #content2{
             margin-bottom:70px;
             margin-left: 40%;
             margin-right: 20%;
             text-indent: 50px;
       }
       
       #infolist li{
             list-style-type:none;
             display:inline;
             margin-left: 10px;
             text-decoration: none;
             
       
       }
       #infolist a{
                    border-right: 1px black solid;
             padding-right:20px;
       }
       
       
       dt{
       background:url("images/menu_bg.gif")no-repeat 0 0;
       margin-left: 10px;
       }
       
       dd{
       margin-left : 0px;
       margin-top: 20px;
       margin-bottom: 20px;
       }
       
       #infolist{
       padding : 5px;
       background-color:#46FFFF;
       width:80%;
       }
       
       #infolist li.first{
             border:none;
       }
</style>
</head>
<body>
<div>
       <img src="images/herblogo.jpg">
</div>
<div id="menu">
<ul>
  <li><a href="#">허브란?</a></li>
  <li><a href="#">허브의 종류</a></li>
  <li><a href="#">허브 키우는 법</a></li>
  <li><a href="#">직접 만드는 허브차</a></li>
  <li><a href="#">허브, 이렇게 활용하세요</a></li>
</ul>
</div>
<div id="content1">
<h5>허브란? </h5>
<img src="images/balm.jpg" id="balm">
<p>라틴어의 ‘푸른 풀’을 의미하는 Herba에서 유래된 말로, ‘잎, 줄기와 뿌리 등이  식용, 약용에 쓰이거나, 향기나 향미가 이용되는 식물의 총체’ 라고 할 수 있다. 즉, 잎,  줄기, 뿌리, 꽃 등을 허브의 의미에 포함하며 그 성분이 식품이나 음료속에 보존용 향신료  또는 건강증진제로서 첨가되는 식물과 식품, 음료 외에 제품에 향수, 화장, 세정의 효과를  기대하여 이용되는 식물의 전부라고 할 수 있다.현재 국내에서 일반적으로 알고 있는  허브에 대한 개념은 외국에서 도입된 식물에 한정지어 생각하는 경우가 대부분이나 사실은  이미 수 천년 전부터 우리 조상들도 생활 전반에 걸쳐 많은 곳에서 이용하여 왔다. 즉,  산야초들, 예를들면 쑥, 냉이, 씀바귀, 곰취 등 봄철식단에 반찬으로 이용된 것과 한방  처방에 들어가 있는 모든 식물들도 넓게는 모두 허브의 범주에 넣을 수 있는 것이다.</p>
<ul>
  <li>허브는 약용식물이다</li>
  <li>허브는 향기식물이다</li>
  <li>허브는 채소이다</li>
  <li>허브는 향신료이다</li>
  <li>허브는 미인을 만든다</li>
</ul>
</div>
<div id="content2">
<h5>허브의 종류</h5>
<dt>바질(Basil)</dt>
  <dd>두통, 신경과민, 구내염, 강장효과, 건위, 진정, 살균, 불면증에 좋고 젖을 잘  나오게 하는 효능이 있으며, 졸림을 방지하여 늦게까지 공부하는 수험생에게 좋다. 또한  신장의 활동을 촉진시키며 벌레 물린데에 살균효과가 있다.</dd>
<dt>캐모마일(Chamomile)</dt>
  <dd>목욕제로 쓰면 심신의 긴장을 풀어주며 전신 미용에 효과가 크다. 불면증에도 차로  마시면 좋고 감기에 발한 해열 작용, 신경통, 류마티스에 진통 진정작용, 여성의 냉증에도  좋으며 미용효과로는 식후나 취침 전 뜨거운 물 한 컵에 꽃 3~5송이를 넣고 몇 분 간  우렸다가 건져내고 마시면 좋다.</dd>
<dt>레몬밤(Lemonbalm)</dt>
  <dd>레몬밤의 차는 뇌의 활동 강화, 기억력 증진에 효과가 있어 공부하는 수험생에게  좋다. 또한 우울증을 해소시키며 해열, 발한작용이 있어 감기 초기에 조석으로 마시면  효과적이며 체력소모가 많은 여름철 청량음료로도 좋다.</dd>
</div>
<div id="infolist">
<ul>
  <li id="list_title">허브 향기 가득한 곳</li>
  <li><a href="http://www.herbisland.net/" target="_blank">포천  허브아일랜드</a></li>
  <li><a href="http://www.herbhillz.com/" target="_blank">대구  허브힐즈</a></li>
  <li><a href="http://www.herbnara.com/" target="_blank">평창 허브나라</a></li>
  <li><a href="http://www.iyherbland.co.kr/" target="_blank">일영  허브랜드</a></li>
  <li><a href="http://www.herbvillage.co.kr/" target="_blank">연천  허브빌리지</a></li>
</ul>
</div>
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
                            