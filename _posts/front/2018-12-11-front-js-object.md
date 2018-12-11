---
layout: post
title: JavaScript 객체,생성자
categories: [front]
tags: [basic,js,javascript]
comments: true
---
### 객체
- object를 의미함
- key와 value로 이루어져있음(배열과 유사)

~~~
// 객체 생성
var student = {
             id: 100,
             name: '홍길동',
             grade: '90'
};
// 객체가 가진 id값 확인
console.log(student.id);
~~~
- 객체는 동적으로 속성 추가와 제거 가능
- 변수, 함수를 선언하고 값을 넣어주면 된다

~~~
// 객체 생성
var student = {
             id: 100,
             name: '홍길동',
             grade: '90'
             
};
student.age = 16;
student.getAge = function(){
       return this.age;
}
console.log(student);
console.log(student.getAge());
~~~

### 객체의 복사
- 객체1=객체2 처럼 객체2가 가진 주소를 객체 1도 가리키게 되었을 때 얕은복사를 했다고 말함(값이 아닌 주소값 복제)
- 깊은 복사는 객체1, 객체2가 가진 주소가 별개여야 함(옳은방향)
 - for문, 펼침연산 등으로 깊은 복사를 할 수 있다

### prototype
- 생성자 함수로 생성된 객체가 공통으로 가지는 공간
- 예를들어 Student란 객체가 3개의 속성과 1개의 함수를 가지고 있다
- Student 객체가 1000개 만들어진다면 1개의 함수를 1000개 만들게 된다
- 메모리낭비가 심하므로 prototype으로 1개의 함수만 만들고 모든 객체가 참고하게 할 수 있다

~~~
Student.prototype.getSum = function(){};
Student.prototype.getAverage = function(){};
Student.prototype.toString = function(){};
~~~

### 생성자
- new functionname(인자)
- new를 사용하여 생성자를 만들 수 있다
- 생성자 함수를 사용하면 프로토타입을 사용할 수 있어서 메모리공간을 아낄 수 있다
- new를 생성하지 않으면 그냥 함수이다. 이 때 함수 내부에서 this 사용 시 Window 객체를 의미하는 것이다

~~~
function Student(name,korean,math,english){
    this.name = name;
    this.korean = korean;
    this.math = math;
    this.english = english;
}
var std = new Student('하나나',90,80,10);
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
                            