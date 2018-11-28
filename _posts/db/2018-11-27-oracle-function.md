---
layout: post
title: Oracle 숫자,날짜,자료형 변환 함수 정리
categories: [db]
tags: [db,oracle,basic]
comments: true
---
### 숫자 함수

|함수   |설명   |사용법| 결과 |<br>
|:---|:---:|:---:|:---:|<br>
| ROUND(숫자,반올림위치) | 숫자를 반올림 위치에서 반올림 | SELECT ROUND(10.12324, 2) FROM DUAL;| 10.12 |<br>
| TRUNC(숫자, 버림위치) | 숫자 반올림을 버림위치에서 무조건 버림| SELECT TRUNC(10.1777, 3) FROM DUAL;| 10.177 |<br>


|함수   |설명   |사용법| 결과 |
|:---|:---:|:---:|:---:|
| CEIL(숫자) | 지정한 숫자에서 큰 정수를 반환 | SELECT CEIL(3.14) FROM DUAL; | 4 |
| FLOOR(숫자) | 지정한 숫자에서 작은 정수를 반환| SELECT FLOOR(3.14) FROM DUAL;| 3 |

|함수   |설명   |사용법| 결과 |
|:---|:---:|:---:|:---:|
| MOD(나눗셈 될 숫자, 나눌 숫자) | 나머지 숫자를 구하는 함수| SELECT MOD(10, 3) FROM DUAL;| 1 |

### 날짜 함수
|함수   |설명   |사용법| 결과 |
|:---|:---:|:---:|:---:|
| SYSDATE | 현재 날짜를 반환하는 함수 | SELECT SYSDATE FROM DUAL;| 18/11/27 |
| ADD_MONTHS(SYSDATE, 더할개월)| 몇 개월 이후의 날짜를 반환하는 함수 | SELECT ADD_MONTHS(SYSDATE,3) FROM DUAL;| 19/02/27 |
| MONTHS_BETWEEN(날짜 데이터1,날짜데이터2) | 두 달간 날짜 차이를 구하는 함수| SELECT ROUND(MONTHS_BETWEEN('2018-11-27', '2019-02-28'),2) FROM DUAL;| -3.03 |

### 자료형 반환
- 형변환을 사용하면 숫자 데이터<->문자 데이터<->날짜 데이터 끼리 변환이 가능하다
|함수   |설명   |사용법| 결과 |
|:---|:---:|:---:|:---:|
| TO_CHAR(날짜나 문자,문자형태) | 날짜OR문자를 자신이 원하는 형태로 반환하는 함수 | SELECT TO_CHAR(SYSDATE, 'YYYY/MM/DD HH24:MI:SS') FROM DUAL;| 2018/11/27 18:55:58 |
| TO_NUMBER(문자,변환 숫자형태) | 문자데이터를 숫자 형태로 반환하는 함수| SELECT TO_NUMBER('5,000', '999,999') FROM DUAL; | 5000 |
| TO_DATE(문자,인식될 날짜형태) | 문자 데이터를 날짜 데이터로 변환하는 함수 | SELECT TO_DATE('20181127', 'yyyy-mm-dd') FROM DUAL;|18/11/27|

### NULL 처리 함수
|함수   |설명   |
|:---|:---:|
| NVL(NULL검사 데이터 OR 열, NULL 대체 문자) | NULL일 경우 대체문자로 변경한다 |

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
                            