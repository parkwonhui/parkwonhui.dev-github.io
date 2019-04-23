---
layout: post
title: bootstrap4 사용법
categories: [front]
tags: [java,front,bootstrap]
comments: true
---

# Bootstrap 정리

### CDN
- head에 bootstrap을 추가하는 소스코드를 추가한다

~~~
<script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script><script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script><script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>

~~~

### 모바일
- 모바일 환경에서 ui가 변경되어야 한다. 적절히 변경될 수 있도록 viewport 메타 태그를 추가한다
- viewport 태그는 모바일 폰에서의 크기 조절을 위해 만듬
- PC의 viewport는 웹 브라우저 창과 같음(크기 조절 가능)
- 모바일의 viewport는 웹 브라우저 창보다 작고 확대 축소로 뷰포트 배율 변경 가능
- 데스크탑에서 같은 px를 보더라도 pc에선 알맞게 나오지만 모바일에선 작게 나온다. 그렇기 때문에 viewport로 적절한 화면 배율을 설정해야 한다


~~~
<meta name="viewport" content="width=device-width, initial-scale=1">    
~~~

### Container
- body에 있는 모든 태그요소는 'container' 안에 존재해야 한다.
- 만약 화면 너비 전체를 사용하고 싶다면 '.container-fluid' class를 사용한다

~~~
<div class="container"></div>
~~~

### Grid
- 크기에 따라 4가지 class 로 나뉜다
- 크기를 좀 더 늘리고 싶다면 맨 뒤의 숫자를 변경한다

| col-lg-1 | col-md-1 | col-sm-1 | col-xs-1 |
|----------|---------|---------|---------|
| 아주 큰 화면| 중간 화면 | 작은 기기(태블릿) | 모바일 폰

~~~
<div class="row">
    <div class="col-lg-1">큰 기기 테스크탑</div>
    <div class="col-md-1">중간 기기 데스크탑</div>
    <div class="col-xs-1">작은 기기 태블릿</div>
    <div class="col-sm-1">매우 작은 기기 모바일폰</div>
</div>
~~~

- pc와 모바일의 요소의 비율을 다르게 하고 싶다면 각 각의 크기를 설정한다
- 아래 소스코드를 보면 첫번째 요소는 보통 pc화면에서는 (md) 크기가 4이고 두번째 요소도 마찬가지로 크기가 4이다. 그러므로 pc에서 두 요소는 5:5 비율이다
- 하지만 모바일에서 첫번째 요소는 크기가 12인데 두번째 요소2이다. 그래서 모바일로 보면 첫번째 요소와 두번째 요소의 크기가 다르다
~~~
<div class="row">
    <div class="col-xs-12 col-md-4">col-xs-12 col-md-8</div>
    <div class="col-xs-2 col-md-4">col-xs-6 col-md-4</div>
</div>
~~~

- 컬럼 오프셋 설정으로 몇 칸 띄어서 요소를 배치할 수 있다
- 예를 들어 <div class="col-md-4 col-md-offset-3">col-md-4</div> 라면 3칸 정도 띄운 후 해당 div 요소를 배치한다

~~~
<div class="row">
    <div class="col-md-4">col-md-4</div>
    <div class="col-md-4 col-md-offset-3">col-md-4</div>        
</div>
~~~

### DataTable
- [DataTable](https://datatables.net/examples/styling/bootstrap4)
- DataTable 사용을 위해 아래 js를 추가한다

~~~
    <script src="https://cdn.datatables.net/1.10.19/js/jquery.dataTables.min.js"></script>
    <script src="https://cdn.datatables.net/1.10.19/js/dataTables.bootstrap.min.js"></script>
~~~

- table 태그로 DataTable을 작성한다
- colgroup으로 순서대로 필드의 크기 비율을 설정한다
- thead 는 맨 위의 필드명을 뜻하고 tbody는 필드의 값을 뜻한다

~~~
<table id="board1-table" class="table table-striped table-bordred">
<colgroup>
    <col width="10%" />
    <col width="40%" />
    <col width="10%" />
</colgroup>
<thead>
    <tr>
        <td>게시물 번호</td>
        <td>게시물 제목</td>
        <td>날짜</td>
    </tr>
</thead>
<tbody>
    <tr>
        <td>1</td>
        <td>1번 게시물</td>
        <td>2019-4-12</td>
    </tr>
    <tr>
        <td>2</td>
        <td>2번 게시물</td>
        <td>2018-4-12</td>
    </tr>
    <tr>
        <td>3</td>
        <td>3번 게시물</td>
        <td>2018-4-13</td>
    </tr>
</tbody>
</table>
~~~

### Pagination
- [pagination](https://getbootstrap.com/docs/4.0/components/pagination/)
- nav 태그는 html5에 등장한 태그. 현재 페이지에서 다른 페이지로 이동(탐색)을 수행할 때 사용한다. 메뉴 뿐 아니라 페이지네이션도 네비게이션에 해당한다
- li태그에 page-item 속성을 준다
- a태그에 class로 "page-link" 속성을 준다
- 현재 선택한 페이지 숫자와 동일하다면 태그에 active를 준다

~~~
<nav>
  <ul class="pagination">
    <li class="page-item"><a class="page-link" href="#">Previous</a></li>
    <li class="page-item active"><a class="page-link" href="#">1</a></li>
    <li class="page-item"><a class="page-link" href="#">2</a></li>
    <li class="page-item"><a class="page-link" href="#">3</a></li>
    <li class="page-item"><a class="page-link" href="#">Next</a></li>
  </ul>
~~~

### selectForm
- form-control class 를 사용한다
- select box의 크기는 col-md-2, col-sm-1 등으로 정할 수 있다\

~~~
<select class="form-control col-sm-1 col-md-2 list-select-form" name="searchType">
    <option value="A">전체</option>
    <option value="T">제목</option>
    <option value="C">내용</option>
    <option value="W">작성자</option>
</select>
~~~

### form 중앙정렬
- text-align:-webkit-center
- webkit 이란 크롬, 사파리 브라우저에 적용, -moz는 파이어폴스, -ms는 익스플로러를 뜻함

### 어썸 폰트
- 어썸폰트란 부트스트랩의 text 아이콘을 뜻한다. text이므로 이미지보다 가공하기 쉽고 깨지지 않는다
- [어썸폰트 공식 홈페이지](https://fontawesome.com/?from=io)
- 아래 style 추가
~~~
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.8.1/css/all.css" integrity="sha384-50oBUHEmvpQ+1lW4y57PTFmhCaXp0ML5d60M1M7uH2+nqUivzIebhndOJK28anvf" crossorigin="anonymous">
~~~
- 사용방법
- fa-spin은 아이콘을 돌린다
- fa-fw는 공백 포함 넓이는 고정하여 깔끔해보이도록 함
- fa-3x는 크기 변경
~~~
<i class="far fa-grin-squint fa-spin fa-fw"></i>
~~~

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