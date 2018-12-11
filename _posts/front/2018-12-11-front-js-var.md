---
layout: post
title: JavaScript var
categories: [front]
tags: [basic,js,javascript]
comments: true
---

### 자료형
- 자바스크립트의 자료형은 var이고 정수형, 문자형 등.. 다양한 값을 넣을 수 있다

~~~
var intNum = 10;
var floatNum = 3.14;
console.log(typeof intNum);
console.log(typeof floatNum);
//문자형(string)
var singS = 'single';
var doubleS = "double";
console.log(typeof singS);
console.log(typeof doubleS);
// 논리형(boolean)
var boolVal = true;
console.log(typeof boolVar);
~~~

### undefined과 null
- undefined : 변수를 선언하고 값을 할당하지 않음(자료형이 결정되지 않은 상태) 
- null : 값이 없다는 뜻. 하지만 값이 할당되지 않은 undefined와는 다르다(null이라는 값이 할당된 것)
- null이라는 뜻은 문자형의 '', 숫자의 0과 또 다른 뜻
- === 기호는 값과 데이터형까지 동일한지 체크하는 연산자

~~~
var temp2;
if(null===temp2){
       console.log("temp2;는 null이다");
}else{
       console.log("temp2;는 null이 아니다"+temp2);
}
temp2='';
if(null === temp2){
       console.log("temp2=''는 null이다");     
}else{
       console.log("temp2=''는 null이 아니다"+temp2);
}
temp2=null;
if(null === temp2){
       console.log("temp2=null는 null이다");   
}else{
       console.log("temp2=null는 null이 아니다"+temp2);     
}
~~~
- 결과

~~~
temp2;는 null이 아니다undefined
temp2=''는 null이 아니다
temp2=null는 null이다
~~~
- 변수에 함수도 넣을 수 있다
- 변수에 함수를 넣으면 function 타입이 된다

~~~
// function
var func = function(){}
console.log(typeof func);
~~~


### 문자열 변환
- 문자열을 넣었던 변수에 숫자를 넣는 것도 가능하다

~~~
// 데이터형 num->string으로 변한다
intNum = "안녕";
console.log(typeof intNum);
~~~
- 문자+숫자 = 문자

~~~
// 형변환 문자+숫자=문자
var num = "15";
num2 = num+10;
console.log(num2);
~~~
- eval함수 사용 시 숫자로 변환할 수 없는 값을 변환하려고 하면 에러가 난다
- parseInt함수는 자신이 숫자로 변환할 수 있는 값만 변환한다

~~~
// 숫자=>문자 변환
var num = "15";
num = eval(num);
num2 = num+10;
console.log(num2);
//eval 변경하지 못하면 에러난다
/*var num = "15안녕";
num = eval(num);
num2 = num+10;
console.log(num2);*/
//parseInt는 자기가 변경할 수 있는 부분만 변경한다
var num = "15안녕";
num = parseInt(num);
num2 = num+10;
console.log(num2);
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
                            