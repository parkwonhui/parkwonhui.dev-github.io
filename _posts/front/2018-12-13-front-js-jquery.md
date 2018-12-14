---
layout: post
title: JavaScript jquery
categories: [front]
tags: [basic,js,javascript,jquery]
comments: true
---
### JQuery
- DOM스크립팅과 Ajax 복잡성을 쉽게 다루기 위해 만듬
- 소스의 단순화, 다양한 플러그인, 타 프레임웍보다 빠름
- 웹표준을 지킴(따로 구버전,신버전 처리 따로 안해도 됨)
- https://developers.google.com/speed/libraries/#jquery
- 제일 간단하게 사용하는 법 : script에 jquery 사용 선언
- <script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>

### 선택자
- 기본세렉터
- $() : 팩토리함수. jquery 객체를 생성할 때 사용
- 자식태그는 부모 태그 바로 아래에 있는 태그. 자손태그는 부모 태그 바로 아래모든 태그


Selector|설명
-------|-------
*|모든 엘리먼트
E|태그명이 E인 모든 엘리먼트
E F|E의 자손이면서 태그명이 F인 모든 엘리먼트
E>F|E의 바로 아래 자식이면서 바로 다음에 나오는 엘리먼트
E+F|E의 형제 엘리먼트로 바로 다음에 나오는 엘리먼트F
E~F|E의 형제 엘리먼트로 다음에 나오는 모든 엘리먼트 F
E.C 태그명이 E인 모든 엘리먼트 중 클래스명이 C인 엘리먼트

Selector|설명
-------|-------
E[A=V]|값이 V인 어트리뷰트 A를 가지는 모든 엘리먼트 E
E[A^=V]|값이 V로 시작하는 어트리뷰트 A를 가지는 모든 엘리먼트
E[A$=V]|값이 V로 끝나는 어트리뷰트 A를 가지는 모든 엘리먼트
E[A*=V]|값에 V를 포함하는 어트리뷰트 A를 가지는 모든 엘리먼트

- 고급 셀렉터

Selector|설명
-------|-------
:first|첫번째 엘리먼트
:last|마지막 엘리먼트
:first-child|첫번째 자식 엘리먼트
:last-child|마지막 자식 엘리먼트
:nth-child(n)|n번째 자식 엘리먼트
:nth-child(even|odd) | 짝수 또는 홀수 자식 엘리먼트
:even | 짝수 엘리먼트
:odd | 홀수 엘리먼트

### jquery 예제
- 클래스 selected-plays의 자손인데 엘리먼트가 li인 것만 'horizontal' 스타일 적용

~~~
$('#selected-plays>li').addClass('horizontal');
~~~
- horizontal class가 아닌 li엘레멘트에 'sub-level' 스타일 적용

~~~
$('li:not(.horizontal)').addClass('sub-level');
~~~
- 주소값(속성 href)이 pdf로 끝나는 a 엘레먼트에 'pdflink' 스타일 적용

~~~
$('a[href $=pdf]').addClass('pdflink');
~~~
- 주소값(속성 href)이 mailto로시작하는 a엘레먼트에 'mailto' 스타일 적용

~~~
$('a[href ^=mailto]').addClass('mailto');
~~~
- 주소값에 mailto를 포함하는 모든 a 엘레먼트에 'mailto' 스타일 적용

~~~
$('a[href *= henry]:not(.mailto)').addClass('henrylink');
~~~
- tr 엘레먼트에서 홀수번째에 있는 요소는 'alt' 스타일 적용
- odd는 홀수에 적용하지만 인덱스가 0부터 시작하므로 1번째 인덱스부터 홀수로 적용

~~~
$('tr:odd').addClass('alt');                    // 홀수지만 짝수번 부터 시작됨(인덱스 0부터이므로)
~~~
- 첫번째 요소를 홀수로 치고 싶다면 nth-child(odd)를 사용한다

~~~
$('tr:nth-child(odd)').addClass('alt');     //nth는 홀수
~~~
- 필터에 명시한 엘레먼트 적용 ('tr:odd'와 같다)

~~~
$('tr').filter(':odd').addClass('alt');
~~~
-  테이블에서 Henry값을 가진 엘레먼트를 찾고 'alt' 스타일 적용

~~~
$('td:contains(Henry)').addClass('highlight');
~~~
- ajax 예제 jquery로 수정

~~~
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=EUC-KR">
<title>Insert title here</title>
<script type="text/javascript" src="httpRequest.js"></script>
<script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
<script type="text/javascript">
       
       function startSuggest(){
             var keyword = $('[name="keyword"]').val();          // name이  keyword인 태그의 값을 가져오기
             var params = "keyword=" + encodeURIComponent(keyword);
             sendRequest("suggest.jsp", params, displayResult, "POST");
       }
       
       function displayResult(){
             if(httpRequest.readyState == 4){
                    if(httpRequest.status == 200){
                          var html="";
                          var result = httpRequest.responseText;
                          var keywardList = result.split(',');
                          for(var i=0;i<keywardList.length;i++){
                                 var str = keywardList[i].trim();
                                 html += "<a href=javascript:select('"  + str  + "')>" + str + "</a>
";
                          }
                          
                          $('#suggestList').html(html);
                          show('suggest');
                    }
             }
       }
       
       function show(elementId){
             $('#'+elementId).css('display', '');
       }
       
       function select(selectKeyward){
             $('[name="keyword"]').val(selectKeyward);
             hide('suggest');
       }
       
       
       function hide(elementId){
             $('#'+elementId).css('display', '');
       }
       
</script>
</head>
<body>
       <form name="search" onkeyup="startSuggest()">
             <input type="text" name="keyword">
             <input type="button" value="전송">
       </form>
       
       <div id="suggest" style="position: absolute; left: 10px">
             <div id="suggestList"></div>
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
                            