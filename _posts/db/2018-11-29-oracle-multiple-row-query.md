---
layout: post
title: Oracle 다중쿼리(Multiple row query)
categories: [db]
tags: [db,oracle,basic,query]
comments: true
---
### 다중쿼리

- 서브 쿼리의 결과가 여러개인 경우 사용
- 서브 쿼리의 결과를 하나의 값과 비교할 수 도 있고, 두개 이상도 비교 가능
- WHERE 컬럼 = (SELECT ~ ) => 단일로우
- WHERE 컬럼 IN(SELECT ~ ) =>다중로우

- IN : 검색된 값 중에 하나만 일치하면 참이다
- ANY : 검색된 값 중에 조건에 맞는 것이 하나 이상 있으면 참
- ALL : 검색된 값과 조건에 모두 일치해야 참

- 컬럼 > ALL(서브쿼리) => 컬럼 > MAX : 가장 큰 값 보다 크다.
- 컬럼 < ALL(서브쿼리) => 컬럼 > MIN: 가장 작은 값 보다 작다.

- 컬럼 > ANY(서브쿼리) => 컬럼 > MIN : 가장 작은 값 보다 크다.
- 컬럼 < ANY(서브쿼리) => 컬럼 > MAX: 가장  큰 값 보다 작다.

~~~
SELECT 컬럼
FROM 테이블
WHERE 비교대상 (서브쿼리)
~~~

- 두 개 이상의 값을 쿼리로 받아서 비교

~~~
SELECT * FROM STUDENT WHERE MAJOR = '화학';
SELECT SNO, SNAME, SYEAR, MAJOR, AVR
FROM STUDENT S
WHERE (AVR,SYEAR) IN (SELECT AVR,SYEAR FROM STUDENT WHERE MAJOR = '화학' )
AND MAJOR != '화학';
~~~

### FROM절 서브쿼리(Top-N SQL
- FROM 절에 테이블 이름 대신 서브쿼리 사용
- 테이블을 질의하기 편하게 수정하면 데이터 찾기가 쉽다
- 예를 들어 입사를 제일 오래한 사원을 출력 시, 테이블에 입사순서대로 정렬되어있으면 편하다
- FROM에 서브쿼리로 입사순으로 정렬된 테이블을 가져올 수 있다

~~~
서브쿼리 SELECT * FROM 테이블이름 ORDER BY DESC
SELECT A.*
FROM (서브쿼리).A
WHERE 조건
~~~
- 4.5 환산평점이 가장 높은 3명의 학생을 검색하는 예제

~~~
SELECT SNO,SNAME,(AVR/4.0 *4.5)  FROM STUDENT ORDER BY 3 DESC;
SELECT ROWNUM, S.*
FROM (SELECT SNO,SNAME,(AVR/4.0 *4.5)  FROM STUDENT ORDER BY AVR DESC)S
WHERE ROWNUM <= 3;
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
                            


 