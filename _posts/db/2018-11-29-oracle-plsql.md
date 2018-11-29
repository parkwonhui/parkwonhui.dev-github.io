---
layout: post
title: Oracle PL/SQL
categories: [db]
tags: [db,oracle,basic,pl/sql]
comments: true
---
### PL/SQL
- SQL에 프로그래밍 언어 기능(변수, 제어문, 함수 등)을 절차적으로 확장한 언어
- Compile이 필요 없이 Script 생성 및 변경 가능
- 선언부(DECLARE), 실행부(BEGIN~END), 예외처리부(Exception)
- output에서 출력하기 위해 set serveroutput on; => 설정 필요

### DECLARE
- 변수선언

~~~
DECLARE
v_no NUMBER(3) := 10;
v_hireDate VARCHAR2(30) := TO_CHAR(SYSDATE, 'YYYY/MM/DD');
~~~

- 상수선언

~~~
c_message CONSTANT VARCHAR2(50) :='hello world'
~~~

###  BEGIN~END
- DBMS_OUTPUT 패키지 PUT_LINE 프로시저를 이용하여 결과 출력

~~~
BEGIN
DBMS_OUTPUT.PUT_LINE('hello world');
DBMS_OUTPUT.PUT_LINE(c_message);
DBMS_OUTPUT.PUT_LINE(v_hireDate);
END;
~~~

- 전체 예제

~~~
DECLARE
v_no NUMBER(3) := 10;
v_hireDate VARCHAR2(30) := TO_CHAR(SYSDATE, 'YYYY/MM/DD');
c_message CONSTANT VARCHAR2(50) :='hello world';

BEGIN
DBMS_OUTPUT.PUT_LINE('hello world');
DBMS_OUTPUT.PUT_LINE(c_message);
DBMS_OUTPUT.PUT_LINE(v_hireDate);
END;
~~~

- 특정 테이블의 로우를 검색하여 변수에 할당 후 출력
- dbms_output.put_line();
- 사용 예제

~~~
DECLARE
    v_name VARCHAR2(20)
    v_salary NUMBER;
    v_hiredate VARCHAR2(30);

BEGINE
    SELECT last_name, salary, TO_CHAR(hire_date, 'yyyy-mm-dd')
    INTO v_name, v_salary, v_hiredate
    FROM employees
    WHERE last_name = 'Chen';

dbms_output.put_line('검색된 사원 정보');
dbms_output.put_line(v_name || ' ' || v_salary || ' ' || v_hiredate);
END;
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
                            

