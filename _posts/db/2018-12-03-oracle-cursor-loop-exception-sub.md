---
layout: post
title: Oracle 반복문,커서,예외,저장 서브프로그램 
categories: [db]
tags: [db,oracle,basic]
comments: true
---
### 반복문
- 자바의 WHILE, FOR문처럼 사용할 수 있다
- LOOP, WHILE, FOR 예제
~~~
DECLARE
i NUMBER := 0;
BEGIN
-- LOOP
LOOP
i:=i+1;
EXIT WHEN  i > 10;
dbms_output.put_line(i);
END LOOP;

-- WHILE
WHILE i< 10 LOOP
  i:= i+1;
  dbms_output.put_line(i);
  END LOOP;
  
  -- FOR
  FOR i IN 1..10 LOOP
      dbms_output.put_line(i);
  END LOOP;
END;
~~~

### 커서
- SQL문 실행 결과 정보를 저장한 메모리 공간
- 사용방법에 따라 명시적, 묵시적 커서로 나눔
- SELECT INTO
- 조회되는 데이터가 1개일 때 사용
- SELECT로 컬럼을 선택하고 INTO에서 변수에 대입
- 그 외 기존 사용방식 동일(WHERE, GROUP 등.. 사용가능)

~~~
SELECT 열1, 열2, .., 열 n
INTO 변수1, 변수2.., 변수 n
FROM ...
~~~
- 실제 사용 예제

~~~
DECLARE
V_DEPT_ROW DEPT%ROWTYPE;
BEGIN
SELECT DEPTNO, DNAME, LOC INTO V_DEPT_ROW FROM DEPT
WHERE DEPTNO = 40;
DBMS_OUTPUT.PUT_LINE('DEPTNO:' || V_DEPT_ROW.DEPTNO);
END;
~~~
- 명시적 커서 선언

~~~
DECLARE
CURSOR 커서 이름 IS SQL문;    -- 커서 선언
BEGIN
OPEN 커서 이름;                        -- 커서 열기
FETCH 커서 이름 INTO 변수      -- 커서로부터 읽어온 데이터 사용
CLOSE 커서 이름;                       -- 커서 닫기
END;
~~~

- FOR LOOP를 사용하면 OPEN, FETCH를 사용하지 않아도 된다
~~~
FOR 루프 인덱스 이름 IN 커서 이름 LOOP
결과 행별로 반복 수행할 작업;
END LOOP;
~~~

- 사용 예제
~~~
DECLARE
-- 명시적 커서 선언
CURSOR c1 IS
SELECT DEPTNO, DNAME, LOC
FROM DEPT;

BEGIN
-- 커서 FOR LOOP 시작(자동 Open, Fetch, Close)
FOR c1_rec IN LOOP
DBMS_OUTPUT.PUT_LINE('DEPTNO:' || c1_rec.DEPTNO);
END LOOP;
END;
~~~

### 예외처리
- SQL 프로그램 실행 에러를 '예외'라고 함
- 예외 이름 선언, 처리부분으로 나눠짐
- RAISE 예외를 발생시키는 키워드

~~~
DECLARE
  cnt NUMBER:=0;
  e_user_exception EXCEPTION; -- 예외 정의
BEGIN
  SELECT COUNT(*) INTO cnt
    FROM employees
    WHERE department_id = 40;
  
IF cnt < 5 THEN
    RAISE e_user_exception;
END IF;

EXCEPTION
    WHEN e_user_exception THEN
                dbms_output.put_line('인원이 너무 적어요');
END;
~~~

### 저장 서브프로그램
- 여러번 사용할 목적으로 이름을 지정하여 오라클에 저장해두는 것
- 저장할 때 한번만 컴파일
- 메모리, 성능, 재사용성 등 장점이 있다
- 실행은 EXEC 저장 서브프로그램 이름(인자);
- RETURN 값이면 인자에 OUT, 전달 인자면 IN으로 명시
~~~
CREATE [OR REPLACE] PROCEDURE 프로시저 이름
IS | AS
선언부
BEGIN
실행부
EXCEPTION
예외 처리부
END [프로시저 이름];
~~~
- 사용 예제

~~~
create or replace PROCEDURE JOB_UPDATE(p_job_id in JOBS2.JOB_ID%TYPE, p_job_title in JOBS2.JOB_TITLE%TYPE, p_min_salary in JOBS2.MIN_SALARY%TYPE, p_max_salary in JOBS2.MAX_SALARY%TYPE)
IS
v_count NUMBER := 0;
-- CURSOR job_cursors IS SELECT JOB_ID, JOB_TITLE, MIN_SALARY, MAX_SALARY FROM JOBS2;
BEGIN

--CURSOR job_cursors IS
SELECT COUNT(*)
INTO v_count
FROM jobs2
WHERE job_id = p_job_id;
--job_record job_cursors%ROWTYPE;

dbms_output.put_line('count:'||' '||v_count);
IF 0 = v_count THEN
dbms_output.put_line('INSERT2'||' '||p_job_id);
INSERT INTO JOBS2 VALUES(p_job_id, p_job_title, p_min_salary, p_max_salary);
dbms_output.put_line('INSERT'||' '||p_job_id);
ELSE
dbms_output.put_line('UPDATE2'||' '||p_job_id);
UPDATE JOBS2 SET JOB_TITLE = p_job_title, MIN_SALARY = p_min_salary, MAX_SALARY = p_max_salary WHERE JOB_ID = p_job_id;
dbms_output.put_line('UPDATE'||' '||p_job_id);
END IF;
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
                            