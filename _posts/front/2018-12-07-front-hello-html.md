---
layout: post
title: HTML 기초 정리
categories: [front]
tags: [db,html,basic]
comments: true
---
### HTML과 HTML5차이
- 웹의 애플리케이션화를 위해서(단순한 정보 전달=>다양한 서비스 제공)
- 문서의 의미를 부여하기 위해(이전에는 꾸미는것도 같이 씀=>CSS와 분리)

### HTML문서 구조
- DOCTYPE 는 HTML 버전을 정의. 버전에 따라 문법이 다르기 때문
- HEAD에 문서 정보를 작성
- BODY는 우리눈에 보이는 화면을 꾸밈

### HTML 기초 문법
- 태그의 대소문자 구별X
- 시작태그와 종료태그로 이루어지거나, 하나의 태그로 이루어진다

### 목록 태그
- ol : 번호가 있는 목록
- ul : 번호가 없는 목록
- dl, dd : key, value로 이루어진 목록. 용어를 정의할 때 사용
- dl, dd 예제

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>타이틀입니당</title>
</head>
<body>
<dl>
<dt>웹표준</dt>
<dd>W3C권고안으로 만든 문서</dd>
</dl>
</body>
</html>
~~~

### div, span
- div는 자기가 있는 줄의 자리를 다 차지한다
- span은 옆에 자리가 비워져 있다

### id, class
- id는 유일한 하나의 식별자이다
- class는 grouping 하는데 쓰인다

### 경로
- 절대경로 : 프로젝트 위치 경로에서 시작( 프로젝트이름/경로... )
- 상대경로 : html 파일 위치에서 시작( ./경로... )

### h1
- 글자크기X 문서를 구조적으로 보여주기 위해서 사용

### 웹마
- 현재 사이트의 이미지를 모두 저장하는 기능을 가진 프로그램

### 다양한 기능들
- IMG SRC
- 이미지 추가. alt는 시각장애인들을 위해 반드시 넣어야 한다(공공프젝 중요!!)

~~~
<li><img src="./img/road2.jpg" alt="5" ></li>
~~~

- INPUT
- 전송버튼, 체크박스, 라디오 박스 등 다양한 기능을 만들 수 있다
- HTML5가 되면서 MAIL FORM에 MAIL체크도 가능(@만 체크하므로 세세한 확인 필요)

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h3>form Exam</h3>
<form action="server_url.jsp" method="get">
       <fieldset>
       <ol>
       <li>
       <label for="userName">이름</label>
       <input type="text" name="userName" id="userName"
       autofocus="autofocus" placeholder="ex)홍길동">
       </li>
       <li>
             <label>이메일</label>
             <input type="email" placeholder="ex)23123@gmail.com"  required="required" />
       </li>
       <li>
       <label>날짜</label>
       <input type="date"/>
       </li>
             <li>
       <label>색상</label>
       <input type="color"/>
       </li>
             <li>
       <label>수량</label>
       <input type="range" min="1" min="10" min="5"/>
       </li>
       <li>
       <label>옵션</label>
       <select>
       <option value="BMW">BMW</option>
       <option value="BENCH">벤츠</option>
       <option value="KTX">KTX</option>
       </select>
       <li>
       <label><input type="checkbox" name="월" value="1"/>월</label>
       <label><input type="checkbox" name="화" value="2"/>화</label>
       <label><input type="checkbox" name="수" value="3"/>수</label>
       <input type="radio" name="fruit" value="사과" /> 사과
       <input type="radio" name="fruit" value="바나나" checked="checked" />  바나나
       </li>
       <li>
       <input type="radio" name="fruit" value="1"/>목
       <input type="radio" name="fruit" value="2"/>금
       <input type="radio" name="fruit" value="3"  checked="checked" />토
       </li>
       </ol>
       </fieldset>
       <fieldset>
             <input type="submit" value="전송">
       </fieldset>  
</form>
</body>
</html>
~~~


- IFRAME
- 다른 페이지의 내용을 불러온다

~~~
<p>
<iframe src="img_exam.html" width="500" title="이미지 예제"></iframe>
</p>
~~~

- VIDEO
- 동영상을 불러오는 태그

~~~
<figure>
<figcaption>
동영상
<video width="640" height="360" controls="controls">
<source src="Merry_Love.MP4" type="video/mp4"/>
</video>
</figcaption>
</figure>
~~~

- TOP
- 페이지의 맨 처음으로 이동

~~~
<a href="#top">top</a>
~~~

- TABLE

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
       <table width="450" border="1" cellpadding="0" cellspacing="0">
       <caption>2018프로야구 순위</caption>
       <thead>
             <tr height='50' align="center">
             <td>순위</td>
             <td>팀명</td>
             <td>승</td>
             <td>무</td>
             <td>패</td>         
       </tr>
       </thead>
       <tbody>
       <tr height='50' align="center">
             <td rowspan="2">1</td>
             <td>SK</td>
             <td>90</td>
             <td>0</td>
             <td>10</td>         
       </tr>
             <tr height='50' align="center">
             <td>두산</td>
             <td>80</td>
             <td>0</td>
             <td>20</td>         
       </tr>
             <tr height='50' align="center">
             <td>3</td>
             <td>넥센</td>
             
             <td>70</td>
             <td>0</td>
             <td>30</td>         
       </tr>
       </tbody>
       <tfoot>
             </tr>
             <tr height='50' align="center">
             <td colspan='2'>합계</td>
             <td></td>
             <td></td>           
       </tr>
       
       </tfoot>
       </table>
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
                            


