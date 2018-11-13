---
layout: post
title: Regular(정규직)
categories: [java]
tags: [java,regular]
comments: true
---
### 정규표현식
- 특정한 규칙을 가진 문자열의 집합을 표현하는데 사용하는 표현식 언어이다
. : '.'가 위치한 곳에는 반드시 임의의 한글자가 위치하여야 한다는 의미
- '*'가 바로 앞의 문자가 없거나 하나 이상 반복한다는 의미
- '+': '*'과 흡사하지만 '+'는 반드시 하나 이상의 문자가 반복된다는 의미
- '?': 바로 앞의 문자가 없거나 하나임을 의미
- '^': 문장의 처음을 나타내며 '^'가 있는 단어로 문장이 시작됨을 의미
- '$' : 문장의 끝을 나타내며, $가 있는 단어로 문장이 끝남을 의미
- []괄호 안의 문자 중 일치하는 것을 검색할 경우 사용
  - [abc] : a, b, c, abc 등 문자열에 a, b, c등이 있어야 한다
  - [0-9] : 숫자가 포함된 모든 문자열
  - [a-z] : 알파벳 소문자가 포함된 모든 문자열(범위)
  - ^[a-zA-z0-0] : 영문대소문자 또는 숫자로 시작되는 모든 문자열 검색
- [] 안에서의 '^' 특수문자(부정)
  - [] 특수문자 안에 있는 문자를 포함하고 있지 않는 모든 문자열을 찾고자 할 경우
- {} 특수문자 앞의 문자가 반복되는 횟수 의미
- () 안에 문자열을 하나의 문자로 취급
- | or 연산 수행
- [a-zA-Z] 모든 영문자
- 특수문자를 문자 그래도 사용하고 싶다면 특수 문자 앞에는 역슬레시를 써야 한다
- w : [a-zA-Z0-0] 알파벳이나 숫자
- W : [^a-zA-Z0-9] 알파벳이나 숫자를 제외한 문자

### 자바 정규 표현식 처리
- java.util.regex 패키지
- Pattern 클래스

### Source
~~~
import java.util.Scanner;
public class ReqularExam {
     public static void main(String[] args) {
           Scanner sc = new Scanner(System.in);
           System.out.println("문자열 입력:");
           String str = sc.nextLine();
           
           // abc문자 포함
           // . : 앞, 뒤로 데이터가 있다
           // * : 몇 개 반복될 지 모른다
           /*if(str.matches(".*abc.*")){     // 정규표현식 체크
                System.out.println("매칭");
           }else{
                System.out.println("비매칭");
           }*/
           
           /*// 숫자만 3자리 입력
           //[0-9] : 숫자만 입력
           //{} : 앞의 문자가 반복되는 횟수
           if(str.matches("[0-9]{3}")){
                System.out.println("매칭");
           }else{
                System.out.println("비매칭");
           }*/
           
           //
           // 알파벳, 숫자만 5자 이상 입력
           // [//w]{5,}
/*         if(str.matches("^[a-bA-Z0-9]*${6}")){
                System.out.println("매칭");
           }else{
                System.out.println("비매칭");
           }
*/         
           // 한글만 3자리에서 5자리
           if(str.matches("[가-힣]{3,5}"))
                System.out.println("매칭");
           else
                System.out.println("매칭");
     }
}
~~~

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
                            