---
layout: post
title: DataTable
categories: [spring]
tags: [java,dataTable]
comments: true
---

# DataTable
- Jquery PlugIn으로 테이블과 데이터를 연동만 해주시면 페이징, 검색, 정렬 등 기능을 쉽게 사용할 수 있다.
- [DataTable 공식 홈페이지](https://datatables.net/)

### DataTable 기본 예제
- server를 사용하지 않고 오로지 client에서 처리하는 예제. 그러므로 페이징, order, search가 server 없이 동작한다
- [기본예제](https://datatables.net/examples/basic_init/zero_configuration.html)
- 아무런 옵션 없이 dataTable을 만들기만 하면 기본테이블이 생성된다

### DataTable 주요옵션
- pageLength: 한 페이지에 보이는 게시물 개수
- searching : 검색 기능 사용 여부
- ordering : 게시물 정렬 기능 사용 여부
- select : 한 페이지에 보일 게시물 개수 지정 기능
- serverSide: server와 통신여부
- processing : 서버와 통신 시 응답을 받기 전이라는 ui를 띄울 것인지 여부

### 데이터 전달
- 서버에서 데이터를 전달할 때 반드시 'data'로 전달해야함.
- 데이터에 링크를 걸고 싶거나 class를 주고 싶을 뗀 render:function 함수로 데이터를 수정 후 return

~~~
columns : [
				{"data":"boardSeq", render:function(data, type, full, meta){
					return '<div class="board-list-boardSeq">'+data+'</div>';
				
				}},
				{"data":"title", render:function(data, type, full, meta){
            		return '<div class="board-list-title">'+data+'</div>';
            	}},
				{"data":"writer"},
				{"data":"dateString"},
				{"data":"count"}
            ],
~~~

### ajax 사용 시 주의사항
- dataTable에 대해서 잘 모르고 성공 여부를 알기 위해서 success 함수를 정의했다가 죽는줄 알았다.. dataTable이 적용이 되지 않았는데 이유는 success 함수를 내가 선언했기 때문이었다.
dataTable이 성공일 때 테이블을 그려주는 동작을 알아서 한다. 그런데 success 함수를 내가 재정의 해서 그 동작을 지워버린 것이다. 습관대로 success 를 호출하지 말도록 하자.

### 페이지 무한 없애기
- 처음 페이징을 적용하면 페이지가 최대 페이지에 상관없이 무한히 생성됨
- 전체 게시물 개수가 없어서 생기는 현상. 클라이언트에 값을 전달할 때 iTotalRecords, iTotalDisplayRecords 값 전달값이

~~~
result.put("iTotalRecords", totalCount);
result.put("iTotalDisplayRecords", totalCount);
~~~
### 페이지 숫자로만 추가
- ...라는 줄임표를 빼고 싶다면 "simple_numbers_no_ellipses" 옵션 사용 
- cdn 추가
~~~
<script type="text/javascript" charset="utf8"
     src="https://cdn.datatables.net/plug-ins/1.10.19/pagination/simple_numbers_no_ellipses.js"></script>
~~~

- 옵션추가
~~~
pagingType:"simple_numbers_no_ellipses"
~~~

### 검색 구현
- 검색창에 단어를 입력할 때 마다 검색함.
- 버튼을 눌러서 데이터를 검색하고싶다면 custom하게 새로 만들어야 함
- 내가 만든 검색창의 데이터를 서버로 전달하고 싶다면 데이터 전달할 때 id나 class명으로 찾은 요소의 값을 줘야함(찾은 요소와 연결되나봄??)

~~~
  d.searchValue = selectValue;    					// x
  d.searchType =  $('.list-select-form').val();		// o
~~~
- 버튼을 누를 때 마다 우의 요소의 값을 새로 넣어줌
- 그리고 reload 함수 호출

~~~
$('#searchBoardButton').click(function(){
	$('.list-select-form').val( $('.list-select-form').val());
	$('.board-list-serach-form').val($('.board-list-serach-form').val());
	$('#board1-table').DataTable().ajax.reload();
});
~~~

### Source Code

~~~
table = $('#board1-table').DataTable({
	pagingType:"simple_numbers_no_ellipses",        // 페이징에서 생략부호 빼기
	serverSide: true,                                             // ajax로 서버 데이터 처리
	pageLength: pageLen,                                          // 게시물 뒤로가기 시 기존 가지고 있던 페이지 크기를 넣어주므로 변수에 값 저장 
	searching: true,
	ordering: false,
	select: true,
	ajax : {
		 "type":"POST",
		 "url":'/board/list',
		 "data":function(d, event){                                   // 서버에 전달할 데이터
			   d.searchValue = $('.board-list-serach-form').val();    // 검색 버튼을 누르면 .board-list-search-form 의 값을 가져옴.
			   d.searchType =  $('.list-select-form').val();
			   var info =  $('#board-list-select-vo').val();
			   if(info != undefined){
					d.start =  ($('#board-list-select-vo .page').val()-1) * 10;
					d.length =  $('#board-list-select-vo .length').val();
					d.searchType =  $('#board-list-select-vo .searchType').val();
					d.searchValue =  $('#board-list-select-vo .searchValue').val();
			   }
			   return d;                    
		 }
		 
	},    
	columns : [                                                       // 서버에서 받은 값을 넣어주기 전 커스텀마이징 할 수 있다.
		 {"data":"boardSeq", render:function(data,  type, full, meta){
			   return '<div  class="board-list-boardSeq">'+data+'</div>';
		 
		 }},
		 {"data":"title", render:function(data,  type, full, meta){
		 return '<div  class="board-list-title">'+data+'</div>';
	}},
		 {"data":"writer"},
		 {"data":"dateString"},
		 {"data":"count"}
],
"initComplete":function(oSettings){                            		// 데이터 테이블 초기화
	var info = $('#board-list-select-vo').val();
	if(info != undefined){
		 var pageNum = $('#board-list-select-vo  .page').val();
			   pageNum *= 1;
			   this.fnPageChange( pageNum-1 );
			   $('#board-list-select-vo').remove();
	}
}
,"fnDrawCallback": function(){                                      // 서버에서 데이터 전달 후 처리
	var api = this.api();
	var json = api.ajax.json().selectVO;
	gLength = json.length;
	gPage = table.page.info().page + 1;
	gStart = json.start;
	gSearchType = json.searchType;
	gSearchValue = json.searchValue;
	
	$('#board1-table').on("click",  ".board-list-title", function(){
		  var parent = $(this).parent();
		 if(undefined == parent){
			   return;
		 }
		 
		 var parent = $(parent).parent();
		 if(undefined == parent){
			   return;
		 }
			   
		 var boardSeq =   $(parent).children('td').children('.board-list-boardSeq').html();
		 if(undefined == $('#boardSearchForm')){
			   return;
		 }
			   
		 var data = {
			   "boardSeq" : boardSeq
		 };
									
		 var url = getHrefBoardList('#actionForm',   '/board/'+boardSeq);
		 ajaxRequest("/board/"+boardSeq,  JSON.stringify(data),  "POST", url);
	});             
}
});

$('#searchBoardButton').click(function(){            				// 검색 버튼 누르기

$('.list-select-form').val( $('.list-select-form').val());			// 값을 전달 할 때 값을 직접참조($('.list-select-form').val();)로 전달하지 않으면 전달값이 갱신이 안됨
$('.board-list-serach-form').val($('.board-list-serach-form').val());
$('#board1-table').DataTable().ajax.reload();						// reload 를 받드시해야한다
	
});
~~~

<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIA*BLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
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


