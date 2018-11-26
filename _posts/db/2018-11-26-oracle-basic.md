---
layout: post
title: Oracle 기초 쿼리 정리
categories: [db]
tags: [db,oracle,select,basic]
comments: true
---
### Database
- 서로 연관성을 가지며, 중복 없이 지속성으로 유지 관리해야 할 융용한 데이터들의 집합
- 데이터 저장을 위한 가장 원시적인 방법으로 데이터 파일 사용
- 데이터 파일 사용 시 중복 된 데이터 저장
- 대용량의 데이터를 관리하기 힘듬, 보안의 취약
- 파일의 단점으로 인해 Database 사용

### DBMS란
- 데이터베이스 관리 시스템
- 대용량의 데이터를 쉽게 저장하고 효율적으로 검색, 수정,삭제 할 수 있는 환경을 제공해 주는 소프트웨어
Oracle SQL Develop 설치


### Oracle 실행
- cmd 창 열어서 sqlplus/nolog 명령어 사용
- conn sys as sysdba명령어 치고 비밀번호를 치면 sql에 접속이 가능하다

### user 생성 및 로그인
- user 생성

~~~
create user kosta192 identified by 1234;
~~~
- user 권한 전달

~~~
grant connect, resource, dba to kosta192;
~~~
- user 로그인

~~~
conn id/pass
~~~

- 파일가져오기
- cmd창에서 SQL 접속한 후 해당 sql파일 위치를 적고 엔터치면 프로시저가 실행된다

### hr계정 unlock

~~~
conn / as sysdba
alter user hr identified by hr account unlock;
conn hr/hr
select * from tab;
~~~

### scott계정 불러오기

~~~
conn system/1234
@C:\oraclexe\app\oracle\product\11.2.0\server\rdbms\admin\scott.sql
alter user scott identified by tiger;
conn scott/tiger
select * from tab;
~~~

### 테이블 조회
- select * from table name;
- 테이블 구조 불러오기
- DESC 테이블 이름
- 별칭은 AS
- 아래 예제는 LAST_NAME 컬럼 이름을 '성'으로 변경해서 출력한다

~~~
SELECT EMPLOYEE_ID AS 사원번호, LAST_NAME AS "성" FROM employees
~~~

### 중복된 데이터 제거
- DUSTINCT

~~~
SELECT DISTINCT job_id From employees;
~~~

### 정렬 묶음 검색
- ORDER BY 절 사용
- 기준 필드를 내림차순 하고 싶다면 필드명 뒤에 DESC를 쓴다

~~~
SELECT eno, ename, sal from emp ORDER BY sal DESC
~~~

### 조건에 맞는 일부데이터 불러오기
- AND : 조건 두개 다 만족하는지 체크

~~~
select * from employees WHERE SALARY > 5000 AND SALARY < 10000
~~~
- BETWEEN AND  :  BETWEEN 과 AND 사이 값에 들어가는지 체크

~~~
select * from employees WHERE salary BETWEEN 5000 AND 10000
~~~
- OR 연산자 : 조건이 2개 일 때 하나라도 일치하는지 체크

~~~
select employee_id, last_name, job_id from employees where job_id='FI_MGR' OR job_id = 'FI_ACCOUNT';
~~~
- IN 연산자 : 조건이 두개일 때 체크. 둘 중 하나인지 체크
- 조건 연산자의 반복적인 작업들을 덜어줌

~~~
select employee_id, last_name, job_id from employees where job_id in('FI_MGR', 'FI_ACCOUNT')
~~~
- NOT 연산자 : 제외한다는 의미
- NOT을 사용하거나 <>,!= 기호 사용

~~~
SELECT department_id, department_name from departments where not department_id = 10;
SELECT department_id, department_name from departments where not department_id <> 10;
~~~
- IS NOT NULLL : NULL이 아닌지 체크
- NULL이 아닌 값만 출력
~~~
SELECT * FROM employees where commission_pct is not null
~~~
#### LIKE 연산자
- '김%' '김'으로 시작하는 모든 문자열 예)김길동, 김박사, 김밥
- '%과' '과'로 끝나는 모든 문자열 예)화학과, 인산과
- '%김%' '김'이라는 문자를 포함하는 모든 문자열 예) 김씨, 돌김, 삼각김밥볶음밥
- '화_' '화'로 시작하는 2글자 문자열 예) 화약, 화분
- '_등_' '등'이 가운데 들어간 3글자 문자열 예)고등어, 영등포

### 그룹함수
- sum(), avg(), max(), count()
- select sum(salary) from employees;

#### GROUP BY
- GROUP BY절을 사용한 컬럼 단위로 묶어서 출력한다
- group by절에서 언급한 컬럼만 사용할 수 있다

~~~
SELECT department_id, avg(salary) from employees group by department_id
~~~