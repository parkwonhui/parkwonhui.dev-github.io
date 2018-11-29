---
layout: post
title: Oracle 인덱스, 뷰, 시퀀스, 트랜잭션, 세션 정리
categories: [db]
tags: [db,oracle,basic,view,index]
comments: true
---
### 인덱스(INDEX)
- 데이터를 처음부터 끝까지 찾는 건 Table Full Scan, 인덱스를 통해 검색하는 것은 Index Scan이라고 한다
- 데이터 양이 많을 때 Full Scan을 하면 검색 속도가 느려지고, 일정하지 않다
- 기본키(Primary key)또는 고유키(unique key)일 경우 자동으로 생성됨
- Index Scan은 일정한 검색속도를 제공한다
- Index 생성 시 오히려 성능이 떨어질 수도 있다(튜닝 참고)
- 인덱스 생성

~~~
CREATE INDEX index_name
ON table_name(column_name)
~~~
- 인덱스 삭제

~~~
DROP INDEX 인덱스 이름;
~~~

### 뷰(VIEW)
- 하나 이상의 테이블을 조회하는 SELECT 문을 저장한 객체
- 물리적으로 따로 저장하지 않음
- 쿼리의 복잡도를 낮추고, 보안적인 용도로 사용

|뷰 조회   | 기존 테이블 조회|
|:---|:---:|
| SELECT * FROM VM_TOP_3 | SELECT C.CNO, C.CNAME, S.AVG_RESULT FROM COURSE C, (SELECT CNO, AVG(RESULT)  AS AVG_RESULT FROM SCORE GROUP BY CNO ORDER BY AVG(RESULT) DESC)S WHERE C.CNO = S.CN |

- view 생성

~~~
CREATE VIEW VIEW_NAME
AS ( 복잡한 SELECT 쿼리) 
~~~
- view 삭제

~~~
DROP VIEW VW_EMP20;
~~~

### 시퀀스(Sequence)
- 대리 식별자. 특정 규칙에 맞는 연속 숫자를 생성하는 객체. 값이 커지면서, 고유한 값을 생성한다
- 시퀀스는 이전 값을 돌아오게 할 수 없다
- 시퀀스 생성 및 사용

~~~
CREATE SEQUENCE Sequence 이름    -- 시퀀스 생성

CREATE SEQUENCE department_id_seq
START WITH 1                -- 어떤 숫자부터 값을 매길 것인지
INCREMENT BY 10;         -- 다음 숫자는 얼마만큼 커질 것인지

INSERT IINTO departments                --  시퀀스 사용
VALUES(department_id_seq.NEXT , 'IT Education', 103, 1400);

DROP SEQUENCE SEQUENCE_NAME   -- 시퀀스 삭제
~~~

### 트랜잭션(Transaction)
- 실행단위 안에 여러 SQL문이 존재할 수 있다.
- 실행단위 기준으로 실행 되거나, 실행되지 않아야 한다
- 트랜잭션을 취소 하고 싶을 때 ROLLBACK 사용
- 트랜잭션을 영원히 반영하고 싶다면 COMMIT. ROLLBACK되지 않는다
- 트랜잭션 예제

~~~
CREATE TABLE NEW_TABLE(        -- 테이블 생성
NEW_INDEX NUMBER,
INEW_COUNT NUMBER
);

INSERT INTO NEW_TABLE VALUES(1, 10); 
INSERT INTO NEW_TABLE VALUES(2, 10);
COMMIT;                                                      -- 데이터 저장(ROLLBACK으로 못돌림)
INSERT INTO NEW_TABLE VALUES(3, 10); 
INSERT INTO NEW_TABLE VALUES(4, 10);
ROLLBACK;

-- 데이터 3, 4만 존재
~~~

### 세션(Session)
- 세션은 어떤 활동을 위한 시간이나 기간을 뜻함(게임에서 로그인-로그아웃 기간 같은 것)
- 세션이 여러개라는 건 DB 접속을 여러명이 했다는 뜻
- 만약 A세션에서 데이터를 삭제했다면 B세션에는 반영되지 않는다. 반영하려면 COMMIT을 해야한다

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
                            


