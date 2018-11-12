---
layout: post
title: String Function
categories: [java]
tags: [java,String,문자열]
comments: true
---
String 생성
- 문자열이 등록되었다면 참조, 등록 안 되었다면 새로 생성

~~~
String str = "ABC"
~~~
- 무조건 새로 생성

~~~
String str = new String("ABC");
~~~

String 불변성
- 문자열은 불변하기 때문에 문자열 변경 시 새로운 문자열을 다시 생성함=>비효율적
- 문자열 붙이기
~~~
String str3 = str.concat("DEF");
~~~

- 또 다른 문자열 붙이기

~~~
String sql = "select*from board";
int0 num = 10;
if(num == 10){
    sql +="where num = 10";
}
~~~

- StringBuffer, StringBuilder 가변성

~~~
StringBuffer sb = new StringBuffer("가나다");
sb.append("라마바");
System.out.println(sb);
~~~

- 해당 문자열 위치 파악 IndexOf=>0시작, 없으면 -1

~~~
 System.out.println(sql.indexOf("*"));
~~~

- 문자열 길이 length()

~~~
System.out.println(sql.length());
~~~

- 문자열 부분 추출

~~~
System.out.println(sql.substring(0, 12));
~~~

- .을 기준으로 kosta, jpg를 나누는 예제

~~~
String fileName = "kosta.jpg";
String head = ""; // kosta
String pattern = ""; // jpg
int spotIndex = fileName.indexOf(".");
head = fileName.substring(0, spotIndex);
pattern = fileName.substring(spotIndex+1);
System.out.println("head:"+head);
System.out.println("pattern:"+pattern);
~~~

- 공백 제거 trim
- 같은 글자인지 체크 equals
~~~
String id = "kosta";
String m_id = "kosta ";    // 띄어쓰기가 있는 경우  trim함수로 공백제거를 할 수 있다
           
if(id.trim().equals(m_id.trim())){
    System.out.println("같다");
}else{
    System.out.println("다르다");               
}
~~~

- 문자열=>배열변환
- 콤마로 나누고 싶다

~~~
String fruits = "사과,배,포도,수박";
String arr[] = fruits.split(",");
           
for(String name : arr)
System.out.println(name);
~~~

- 정수형에서 문자열로 변환

~~~
int n = 100;                          
String s = new String("100");    // 너무 길다
int n2 = 100;
String s2 = n+"";                     // 간단
~~~

- 문자 끝의 글자를 알아낼 때 endsWith

~~~
String[] arrString = {"abcd.jpg", "abb.gif", "iiii.jpg",  "kkkk.gif", "pppp.ini"};
for(String fileName1:arrString){
if(true == fileName1.endsWith("jpg")){
    System.out.println("jpg 파일 입니다");
}else if(true == fileName1.endsWith("gif")){
     System.out.println("gif 파일 입니다");
}else{
    System.out.println("그 외 파일 입니다");
    }
}
~~~

그 외  getBytes ( 네트워크로 전달할 때 바이트로 변환),
toCharArray()(Char형으로 변환) 등의 String 함수가 있다


<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIA*BLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
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
                            