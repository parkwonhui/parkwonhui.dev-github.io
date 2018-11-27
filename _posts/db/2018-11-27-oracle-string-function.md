---
layout: post
title: Oracle 문자열 함수 정리
categories: [db]
tags: [db,oracle,basic]
comments: true
---
### 오라클 함수
- Oracle 함수란 특정한 결과 값을 얻기 위해 데이터를 입력할 수 있는 특수 명령어

### DUAL 테이블이란?
- Oracle의 최고 권한 관리자 계정인 SYS 소유의 테이블
- 임시 연산, 함수의 결과값을 확인할 때 주로 사용

### 문자 함수
|함수   |설명   |사용법| 결과 |
|:---|:---:|:---:|:---:|
| UPEER(문자열)    | 문자열을 모두 대문자로 변경| SELECT UPPER('AbcdEF') FROM DUAL; | ABCDEF |
| LOWER(문자열)    | 문자열을 모두 소문자로 변경| SELECT LOWER('AbcdEF') FROM DUAL;| abcdef |
| INITCAP(문자열)    | 첫글자를 대문자로. 나머지는 소문자로 변경|SELECT INITCAP('AbcdEF') FROM DUAL;|Abcdef|
- 특정 단어를 찾으려고 하는데, 찾을 대상들이 형식이 다를 때('ABcd', 'aBcd') 일원화하여 쉽게 찾을 수 있다
 
|함수   |설명   |사용법|결과 |
|:---|:---:|:---:|:---:|
|  LENGTH(문자열)   | 문자열의 길이를 구한다 | SELECT LENGTH('가나다라') FROM DUAL; |4|
|  LENGTHB(문자열)   | 문자열의 길이를 바이트 수로 반환한다 | SELECT LENGTHB('가나다라') FROM DUAL; |12|
- LENGTH는 문자열 갯수를 반환하지만, LENGTHB는 바이트 수를 반환한다

|함수   |설명   |사용법|결과 |
|:---|:---:|:---:|:---:|
|  SUBSTR(문자열, 시작위치, 추출길이)| 문자열을 시작위치부터 추출길이만큼 구한다. 시작위치는 1부터 시작| SELECT SUBSTR('가나다라',2) FROM DUAL; |나다라|
- 추출길이를 지정하지 않으면 문자 끝까지 추출됩니다
- 시작위치에 음수값을 넣으면 끝에서 부터 추출합니다.
- 가(-4) 나(-3) 다(-2) 라(-1), 시작위치에 -1을 넣으면 '라'가 출력됩니다

|함수   |설명   |사용법|결과 |
|:---|:---:|:---:|:---:|
|  INSTR(대상 문자열 데이터(필수),<br>위치를 찾으려는 부분 문자(필수),<br>위치 찾기를 시작할 대상 문자열 데이터 위치,<br>시작 위치에서 찾으려는 문자가 몇번째인지 지정)<br>| 문자열안에서 특정 문자를 찾는다| SELECT INSTR('가나다라', '나다') FROM DUAL; |2|

|함수   |설명   |사용법|결과 |
|:---|:---:|:---:|:---:|
|  REPLACE(문자열 데이터 또는 열 이름(필수),<br>찾는 문자(필수),대체할 문자)| 문자를 다른 문자로 바꾼다 | SELECT REPLACE('010-1111-2222', '-') FROM DUAL; |01011112222|
- 만약 대체할 문자를 지정하지 않는다면 찾는 문자는 삭제 된다

|함수   |설명   |사용법|결과 |
|:---|:---:|:---:|:---:|
|  LPAD(문자열 또는 열이름(필수),<br>데이터 자릿수(필수),<br>빈공간에 채울 문자)| 빈 공간이 있다면 왼쪽에 특정 문자로 채움 | SELECT RPAD('201204-', 14, '*') FROM DUAL; |201204-*******|
- RPAD는 사용법은 같고, 오른쪽을 특정 문자로 채움

|함수   |설명   |사용법|결과 |
|:---|:---:|:---:|:---:|
|  CONCAT(문자열,문자열)| 두 문자열을 합침 | SELECT CONCAT('AB','CD') FROM DUAL; |ABCD|

|함수   |설명   |사용법|결과 |
|:---|:---:|:---:|:---:|
|  TRIM(삭제옵션, 삭제할 문자) FROM 원본문자열 데이터(필수)| 특정 문자 삭제|  SELECT TRIM('A' FROM 'ABCDEFG') FROM DUAL;|BCDEFG|


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
                            