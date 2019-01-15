---
layout: post
title: ajax로 데이터 전달/응답 받는법
categories: [java]
tags: [java,jsp,mybatis]
comments: true
---
### 데이터 전달 주의사항
- JavaBeans는 sevlet이란 Controller가 없을 때, jsp에서 jsp로 데이터를 전달할 때 사용한다. 
- servlet을 Controller로 사용한다면 Attribute에 데이터를 저장하고 cos라이브러리를 사용해 ${AttributeName} 처럼 간단하게 사용할 수 있다

### ajax요청 처리 순서
#### ajax 요청

~~~
$.ajax({
	url:'projectBoardRead.do',
	data: {"project_id":project_id},
	dataType:'json',
	success:function(data){
	console.log("성공");
    }
~~~
#### list를 Attribute에 넣어줌

~~~
forward.setRedirect(false);
forward.setPath("/jsp/module/schedule/calenderListJsonParse.jsp");
~~~

#### data를 json으로 변환
- java에서 해도 되지만 간편하게 하기위해 jsp 사용
- < html > 같은 태그는 전부 삭제해야 한다
- out.println도 사용하면 안된다(에러의 원인이 될 수도 있음)
- 반드시 하나의 list만 된다(Attribute를 두개 넣지 않는다)
- 왜냐하면 json은 서로 다른 데이터를 받으면 parsing 하지 못하기 때문이다
- json 변환을 해서 ajax 요청 성공 시 데이터를 간편하게 parsing할 수 있다

~~~
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@page import="kosta.model.module.vo.ScheduleCalender"%>
<%@page import="kosta.model.module.vo.ScheduleCategory"%>
<%@page import="java.util.List"%>
<%@page import="net.sf.json.JSONArray"%>
<%@page import="java.util.ArrayList"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<%!
	List<ScheduleCategory> category_list;
	List<ScheduleCalender> calender_list;
%>
<% 
	category_list = (List<ScheduleCategory>)request.getAttribute("categoryList");
	//System.out.println("list: " + category_list.size());
	//calender_list = (List<ScheduleCalender>)request.getAttribute("calenderList");
	//out.println(category_list);
	System.out.println(JSONArray.fromObject(category_list).toString());
	out.println(JSONArray.fromObject(category_list).toString());
%>
~~~

#### json 데이터 출력
- 이미 json으로 변경했으므로 따로 json으로 변환할 필요 없음
- ajax 요청 성공 시 json으로 데이터 변경은 안되는지 궁금

~~~
if(false == JSONObject.isNull(data[i].category_id))
   	console.log(data[i].category_id);
~~~

### json 사용 시 필요한 라이브러리
- commons-beanutils.jar
- commons-collections-3.2.jar
- commons-lang-2.4.jar
- commons-logging-1.1.jar
- ezmorph-1.0.6.jar
- json-lib-2.3-jdk13.jar



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
                            
