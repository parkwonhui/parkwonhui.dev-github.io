---
layout: post
title: HTML5,CSS 선택자
categories: [html]
tags: [db,html,basic,css]
comments: true
---
### HTML, HTML5의 차이점
- 의미를 가질 수 있도록 시멘틱한 태그가 많이 추가됨
- Section : 제목과 단락으로 구분할 수 있을 때 사용
- Article : Article의 내용을 뽑아서 다른 페이지에서 사용해도 이상하지 않을 때 사용(내용이 독립적일 때)


| 이름 |  설명 |
|:--------:|:--------:|
| < section > | 문서 및 애플리케이션 특정 역역 표시, h1~h6와 함께 사용 |
| < section > | 제목과 단락으로 구분할 수 있다 |
|< header >| 문서 내 소개 및 네비게이션 메뉴 모음 표시
| < footer > |문서 내 꼬릿말, 저자, 저작권 정보 표시
| < nav >  |문서내 네비게이션 요소들 표시
|< acticle >| 독립적인 컨텐츠 단위 표시
|< hgroup >| 섹션 머리말들의 그룹으로 문서의 section의 머리부분 표시

### CSS
- 인라인 스타일 적용
- 중첩된 소스코드가 만들어짐. 되도록 사용하지 않음. 대부분 내부 링크 방식
- 태그가 있는 곳에 스타일을 정의한다

~~~
<h2 style="font-family:돋움,serif; font-size:30px color:blue;  background-color:yellow; ">인라인 스타일 적용</h2>
~~~
- 내부 스타일 적용
- 현재 html에서만 사용 가능
- head에 스타일을 적용한다

~~~
<style type="text/css">
h3{
       font-family: 돋움, serif;
       font-size:20px;
       background:#CC9966;
}
</style>
~~~
- 내부 링크 스타일
- 모든 html 파일에서 사용 가능
- 스타일 파일을 따로 빼서 정의한다

~~~
1. <link rel="stylesheet" type="text/css" href="./style.css">
2. <style type="text/css">
@IMPORT url("style.css");
</style>
~~~

### 선택자(selector)
- 내가 특정 기준으로 스타일을 지정할 수 

| 이름 |  설명 | 예제 |
|:--------:|:--------:|:--------:|
| 전체 선택자| html 문서 내 모든 엘리먼트 선택 | * {}|
|타임 선택자 | 매칭되는 엘리먼트 선택 | h1, h2, h2{} |
| 클래스 선택자 | class 속성이 매칭되는 엘리먼트 선택| .className{} |
|ID 선택자 | id 속성 값과 매칭되는 엘리먼트 선택 | #idName{} |
|하위 선택자 | 하위 엘리먼트 선택 | E1 E2{} |

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
<style type="text/css">
       
       a{
       text-decoration: none;
       }
       *{
             font-size:14px;
       }
       .gold{
       color:#FFEB5A;
       }
       .orange{
       color:orange;
       }
       .silver{
       color:silver;
       }
       
       #blue_border{
       border:1px;
       border-style:dotted;
       border-color:blue;
       padding : 20px 10px ;
       margin: 20px 20px;
       display:inline-block;
       }
       
       
       #red_border{
       border:1px;
       border-style:solid;
       border-color:red;
       padding : 30px;
       }
       
       #layer1{
       padding : 20px;
       }
       
       #layer1 ul{
       list-style-type:none;
       display:inline;
       padding : 20px;
       }
       
       #layer1 ul li{
       float:left;
       border:2px;
       background: green;
       padding : 10px 10px;
       }
       
       /*태그선택자와 클래스 선택자 조합*/
       p.gold{
       background-color:black;
       }
       
       /*가상 클래스 선택자*/
       a:LINK{
       color:##FF0000;
       text-decoration:underline;
       }
       
       a:HOVER{
       color:#CC0303;
       text-decoration:underline;
       }
       
       /*속성 성택자*/
       div[title = def]{
             font-size:30px;
             font_style:italic;
             color:green;
       }
       
       a[href $=pdf]{
             font-size:30px;
             font-style:italic;
             color:orange;
       }
             
</style>
</head>
<body>
       <h3>선택자 이해</h3>
       <hr>
       
       <div title="abc">abcdef</div>
       <div title="def">defffff</div>
       
       <a href="abc.pdf">pdf파일</a>
       <a href="abc.gif">gif파일</a>
       <a href="aac.pdf">pdf파일</a>
       
       <ul>
             <li>전역선택자</li>
             <li>태그선택자</li>
             <li>클래스선택자</li>
             <li>아이디선택자</li>
             <li>후손선택자</li>
             <li>태그선택자와클래스선택자조합</li>
             <li>태그선택자와아이디선택자조합</li>
             <li>가상클래스선택자</li>
             <li>속성선택자</li>
       </ul>
       
       <div class="gold">GOLD2</div>
       
       <p class="gold">GOLD</p>
       <p class="orange">ORANGE</p>
       <p class="silver">SILVER</p>
       
       <div id="blue_border">BLUE_BORDER</div>
       <div id="red_border">RED_BORDER</div>
       
       span태그는 <span>글자선택</span>블럭 역할의 태그이다.
       <div>오늘은 <span>에어콘</span>도 안되고
              <p><span>힘들다</span></p>
        </div>
       
       <div id="layer1">
             <ul>
                    <li>항목1</li>
                    <li>항목2</li>
             </ul>
       </div>
       
       <div id="layer2">
             <ul>
                    <li>항목1</li>
                    <li>항목2</li>
             </ul>
       </div>
       <a href="http://www.naver.com">네이버</a>
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
                            