---
layout: post
title: JavaScript ajax
categories: [front]
tags: [basic,js,javascript,ajax]
comments: true
---
### ajax
- Asynchronous Javascript And XML
- 페이지의 리로딩을 하지 않고 서버로부터 응답을 처리
- 비동기식 프로그램
- 동기식은 요청->응답->다음 요청->다음요청 응답 처럼 순서대로 처리되고 응답올 때까지 아무것도 못함
- 비동기식은 요청을 보내고 바로 다른일을 할 수 있음
- ex. 서울시에 있는 카테고리 누르면 바로 옆에 서울시 전체가 나옴
- ex. 검색창에 글자 하나를 치면 연관검색어가 나옴, 댓글..

### ajax 이벤트 순서
- 이벤트 발생(콜백함수 지정)
- 응답 객체 생성
- 서버에서 데이터 처리
- 받은 데이터를 화면에 출력해준다

###  Ajax-JSP 예제
- 입력창에 이름을 입력하고 버튼을 누르면 '안녕하세요. <이름> 회원님!!!' 값으로 서버로 부터 받는다
- 버튼을 누르면 hello() 함수를 호출한다. hello 함수에서 name입력창의 값을 서버로 전달한다
- 결과값을 받으면 helloResult() 함수(callback)에서 처리한다
- hello.jsp

~~~
<%@ page language="java" contentType="text/plain; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<%
       request.setCharacterEncoding("utf-8");
       String name = request.getParameter("name");
%>  
       안녕하세요. <%= name %>  회원님!!!
~~~
- helloApp.html

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script type="text/javascript" src="httpRequest.js"></script>
<script type="text/javascript">
function hello(){
       var params = "name=" +
             encodeURIComponent(document.fmt.name.value);  // 한글이면 인코딩이  깨지기 때문에 encoding 함수 호출
       sendRequest("hello.jsp", params, helloResult, "GET");
}
function helloResult(){
       // 데이터가 다 도착했다
       if(4 == httpRequest.readyState){
             //정상적인 값인지 체크
             if(200 == httpRequest.status){
                    alert('서버응답:'+httpRequest.responseText);   // XML일 때는  responseXML  
             }
       }
}
</script>
</head>
<body>
<form name="fmt">
       <input type="text" name="name"/>
       <input type="button" value="전송" onclick="hello()"/>
</form>
</body>
</html>
~~~

### Ajax자동완성 예제
- suggestclient.html
- encodeURIComponent : 한글은 깨질 위험이 있다 그러므로 인코딩해줘야 한다. 기본은 utf-8 인코딩
- 한글 => D%95%98%EC 이런식으로 바뀐다
- 패킷은 한번에 올 수도 있지만 나눠서 올 수도 있다. httpRequest.readyState가 4라면 패킷을 모두 받은 것이다
- httpRequest.status가 200이라면 패킷에 에러가 없이 성공적으로 받았다는 뜻이다

~~~
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=EUC-KR">
<title>Insert title here</title>
<script type="text/javascript" src="httpRequest.js"></script>
<script type="text/javascript">
       
       function startSuggest(){
             var keyword = document.search.keyword.value;
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
                          
                          var suggestList =  document.getElementById("suggestList");
                          suggestList.innerHTML = html;
                          show('suggest');
                    }
             }
       }
       
       function show(elementId){
             var element = document.getElementById(elementId);
             if(element){
                    element.style.display="";
             }
       }
       
       function select(selectKeyward){
             document.search.keyword.value = selectKeyward;
             hide('suggest');
       }
       
       
       function hide(elementId){
             var element = document.getElementById(elementId);
             if(element){
                    element.style.display="none";
             }
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
- suggest.jsp

~~~
<%@page import="net.sf.json.JSONArray"%>
<%@page import="java.util.ArrayList"%>
<%@page import="java.util.Collections"%>
<%@page import="java.util.List"%>
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<%!
       String[] keywords ={
             "Ajax", "Ajax마스터", "Ajax교재",
             "자바", "자바박사", "자바강사", "자바서버페이지"
       };
       public List search(String keyword){
             if(keyword == null || keyword.equals("")){
                    return Collections.EMPTY_LIST;
             }
             List result = new ArrayList();
             for(int i=0;i<keywords.length;i++){
                    if(keywords[i].startsWith(keyword)){//첫글자가 문자안에  있는지 체크하고 array안에 넣는다
                          result.add(keywords[i].trim());
                    }
             }
             return result;
       }
%>    
<%
       request.setCharacterEncoding("utf-8");
       String keyword = request.getParameter("keyword");
       
       List keywordList = search(keyword);
       
//     for(int i=0;i<keywordList.size();i++){
//           out.print((String)keywordList.get(i));
//           if(i<keywordList.size()-1){
//                  out.print(",");
//           }
//     }
       
       /* List list = new ArrayList();
       list.add(new Member("홍길동", "서울"));
       list.add(new Member("박길동", "부산"));
       list.add(new Member("조길동", "대구"));
*/
       String json = JSONArray.fromObject(keywordList).toString();
       out.print(json);
%>
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
                            