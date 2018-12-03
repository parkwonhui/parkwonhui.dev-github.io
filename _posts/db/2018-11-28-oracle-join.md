---
layout: post
title: Oracle JOIN 정리
categories: [db]
tags: [db,oracle,basic]
comments: true
---
### 조인(JOIN)
- 2개 이상의 테이블에서 데이터를 검색하기 위해서 사용
- FROM 절에 두 개 이상의 테이블을 명시한다(View, Subquery도 가능)
- 공통된 컬럼이 없다면, 두 테이블의 공통컬럼을 가진 다른 테이블과 JOIN한 후 목표 테이블과 JOIN
- 두 테이블의 모든 조합 확인

~~~
SELECT * FROM 테이블1, 테이블2;
~~~
- 만약 테이블1, 테이블 2에 각 각 3개의 정보가 있다면 모든 데이터를 조합하므로 총 9개의 데이터가 나옴
- 조건을 걸어서 데이터에 알맞은 값을 매칭 시켜줘야 함

### INNER JOIN 사용법
- 조건에 부합하는 두 테이블의 데이터를 합치는 방식
- 컬럼 사용 시 테이블 구분이 필요

~~~
SELECT a컬럼명, b.컬럼명 etc... FROM TABLE_NAME  a, TABLE_NAME b
WHERE a.조건컬럼 == b.조건컬럼 (그외 조건이 있다면 추가)
~~~

- INNER JOIN ANSI JOIN
- WHERE절에 조건이 길어지만 AND가 많이 늘어남
- 결과는 같은데 표기법이 다름

~~~
SELECT a.칼럼명, b.칼럼명 ...
FROM 테이블1 A JOIN테이블2 B
ON 조건
~~~

- 3개 이상의 테이블 JOIN

~~~
SELECT a.칼럼명, b.칼럼명 ...
FROM 테이블1 A, 테이블2 B
ON 조건
JOIN 테이블3
ON 조건
~~~

### SEFE JOIN
- 자기 자신의 테이블과 합치는 것
- 찾고자 하는 값이 자신의 테이블에 있을 때 사용

~~~
SELECT a.칼럼명, b.칼럼명 ...
FROM 테이블1 A JOIN 테이블1 B
ON A.컬럼 = B.다른컬럼 
~~~

### OUTER JOIN
- INNER JOIN 사용시 테이블 데이터가 매칭되지 않은 정보는 볼 수 없음
- 데이터가 매칭 되지 않더라도 한쪽의 테이블을 전부 보고 싶을 때 OUTER JOIN을 사용함
- 매칭되는 데이터가 없을 때 NULL이 표시
- +표시는 전체를 보고 싶은쪽 반대편에 붙이도록 함

~~~
SELECT A.칼럼, B.칼럼 ..
FROM TALBLE1 A, TABLE2 B
WHERE A.칼럼 = B.칼럼(+)
~~~

- OUTER JOIN ANSI JOIN
- 전체 데이터를 보고 싶은 쪽을 JOIN에 지정
- 왼쪽 테이블의 데이터를 전체 출력하고 싶다면 LEFT JOIN, 오른쪽일 경우 RIGHT JOIN

~~~
SELECT TABLE1 A, TABLE2 B
FROM TABLE1 A LEFT JOIN TABLE2 B
ON A.컬럼 = B.컬럼
~~~

### SUB QUERY
- 예를들어 '평균 연봉보다 많은 사람만 출력하시오'란 예제가 있다면 먼저 평균연봉을 구해야한다
- 이 때 평균연봉을 구한 후 결과를 복사해서 비교하면 2번 실행해야하므로 비효율적이다
- SUB QUERY를 사용해서 결과값을 구한 후 메인쿼리에서 사용할 수 있다
- 서브쿼리를 먼저 작성 후 메인쿼리를 작성한다

~~~
SELECT TABLE1 칼럼
FROM TABLE1
WHERE 연봉 > (SELECT AVG(연봉) FROM TABLE1)
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
                            

