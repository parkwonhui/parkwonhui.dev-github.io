---
layout: post
title: Oracle 제약조건 정리
categories: [db]
tags: [db,oracle,basic]
comments: true
---
### 제약조건
- 데이터를 추가, 삭제, 수정하는 가운데 DB의 무결성을 유지
- 무결성이란 DB 데이터가 정확하고 기본 규칙을 지킨다는 뜻이다

|종류   |설명   |
|:---|:---:|
|  NOT NULL | NULL의 저장을 허용하지 않는다(반드시 값이 존재해야 됨), 중복여부와는 상관없다 |
| UNIQUE | 해당 컬럼에서 중복 데이터를 허용하지 않는다, NULL은 중복 대상에서 제외 |
|  PRIMARY KEY| UNIQUE + NOT NULL 제약조건을 전부 가짐, 중복 데이터 허용X NULL 허용X, 자동으로 인덱스 생성됨 |
|  FOREIGN KEY  | 서로 다른 테이블 간 관계를 정의 함 |
|  CHECK | 열에 저장할 수 있는 값의 범위, 패턴을 정의할 수 있음 |
|  DEFAULT | 특정 열에 저장할 값이 지정되지 않았을 경우에 기본값을 지정 |


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
                            