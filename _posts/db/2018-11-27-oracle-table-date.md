---
layout: post
title: Oracle DDL, DML 정리
categories: [db]
tags: [db,oracle,basic]
comments: true
---
### 테이블 추가
- 테이블을 복사하여 새로운 테이블 만들 때 CREATE 문 사용
- ORI_TABLE을 복사하여 NEW_TABLE을 만든다
- ORI_TABLE의 내용이 그대로 복사된다
~~~
CREATE TABLE NEW_TABLE 
AS SELECT * FROM ORI_TABLE;
~~~

- 일부 복사

~~~
CREATE TABLE NEW_TABLE
AS SELECT 복사할 컬럼 FROM ORI_TABLE;
~~~

- 테이블 구조만 복사

~~~
CREATE TABLE NEW_TABLE
AS SELECT * FROM WHERE 1=0;
~~~

- 컬럼을 새로 설정하는 경우
~~~
CREATE TABLE NEW_TABLE(
  NEW_INDEX NUMBER,
  INEW_COUNT NUMBER
);
~~~

### 테이블 변경
- 이미 생성된 데이터베이스 객체 수정
- 테이블에 새 열을 추가, 삭제, 길이 변경 등의 일을 할 수 있음
- 테이블에 열을 추가하는 ADD

~~~
ALTER TABLE ITEMNAME ADD 컬럼이름 컬럼자료형;
~~~

- 테이블의 열 이름 변경 RENAME

~~~
ALTER TABLE 테이블NAME RENAME COLUMN 컬럼명 TO 바꿀 컬럼명
~~~

- 열의 자료형 변경 MODIFY
- DESC TABLE_NAME 으로 데이터형이 수정되었는지 확인할 수 있다

~~~
ALTER TABLE 테이블NAME MODIFY 컬럼명 수정데이터형
~~~

- 열을 삭제하는 DROP

~~~
ALTER TABLE NAME DROP COLUMN 컬럼명
~~~

- 테이블 이름을 변경하는 RENAME

~~~
RENAME TABLE_NAME TO 바꿀 TABLE_NAME
~~~

- 테이블의 데이터를 삭제하는 TRUNCATE
- TRUNCATE로 삭제한 테이블은 복구할 수 없다

~~~
TRUNCATE TABLE TABLE_NANE
~~~

- 테이블의 데이터를 삭제하는 DROP
- DROP으로 삭제한 테이블은 복구할 수 있다

~~~
DROP TABLE TABLENAME;
~~~

### 테이블 데이터 처리
테이블에 데이터 추가 시 INSERT문 사용
~~~
INSERT INTO ITEM VALUES(VALUE,  VALUE); // 순서대로 값이 들어갈 때
INSERT INTO NEW_ITEM(NEW_COUNT, NEW_INDEX)  VALUES(VALUE, VALUE); // 순서를 지정하고 싶을 때
~~~

- 테이블의 데이터 수정 시 UPDATE문 사용
- ROLLBACK; 명령문으로 이전 데이터로 돌아갈 수 있다
~~~
UPDATE TABLE_NAME SET 컬럼=VALUE WHERE 조건...
~~~

- 테이블에 들어있는 데이터 삭제 시 DELETE 문 사용
~~~
DELETE FROM TABLE_NAME WHERE 조건
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
                            