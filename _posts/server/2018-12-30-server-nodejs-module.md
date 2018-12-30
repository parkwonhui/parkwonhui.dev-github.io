---
layout: post
title: node.js의 전역 객체
categories: [server]
tags: [server,nodejs]
comments: true
---

# Node.js의 전역 객체
### 전역변수
- node.js 이므로 최상위 객체 window는 없음
- 전역변수, 전역 함수를 가짐.
- 전역 변수
| 객체 이름 | 설명 |
|:--------:|:--------:|
| __filename | 현재 실행 중인 코드의 파일 경로를 나타냅니다 |
| __dimame | 현재 실행 중인 코드의 폴더 경로를 나타냅니다|
- 사용법

~~~
console.log('filename:', __filename);
console.log('dirname:', __dirname);
~~~

### 전역 객체
| 객체 이름 | 설명 |
|:--------:|:--------:|
| console | 콘솔 화면과 관련된 기능을 다루는 객체 |
| exports | 모듈과 관련된 기능을 다루는 객체 |
| process | 프로그램과 관련된 기능을 다루는 객체 |

### console 객체
- 지정한 매개변수 이외의 내용은 그냥 출력된다
- '%j'는 json 데이터가 들어간다

~~~
console.log('숫자: %d + %d = %d', 273, 52, 273 + 52,'가나다라라');
console.log('문자열: %s', 'Hello World..!', '특수기호와 상관 없음');
console.log('JSON: %j', {name:'RintTanTt'});
~~~

- 시간측정 예제
- 'a'는 타이머의 이름이라고 생각하면 된다(아무 글자를 넣어도 됨)

~~~
// 시간측정 시작
console.time('a');

var output = 1;
for(var i = 1; i<=10; ++i){
  output *= 1;
}
console.log('Result:', output);

// 시간 측정을 종료합니다
console.timeEnd('a');
~~~
- 출력 글자 색상을 바꿀 수도 있다

~~~
// 출력합니다.
console.log('\u001b[31m', 'Hello World .. !');
console.log('\u001b[32m', 'Hello World .. !');
console.log('\u001b[33m', 'Hello World .. !');
console.log('\u001b[34m', 'Hello World .. !');
console.log('\u001b[35m', 'Hello World .. !');
console.log('\u001b[36m', 'Hello World .. !');
console.log('\u001b[1m');
console.log('\u001b[31m', 'Hello World .. !');
console.log('\u001b[32m', 'Hello World .. !');
console.log('\u001b[33m', 'Hello World .. !');
console.log('\u001b[34m', 'Hello World .. !');
console.log('\u001b[35m', 'Hello World .. !');
console.log('\u001b[36m', 'Hello World .. !');

// 초기화합니다.
console.log('\u001b[0m');
~~~

### process 객체
- 프로그램과 관련된 정보를 나타내는 객체

| 속성 이름 | 설명 |
|:--------:|:--------:|
| argv | 실행 매개변수를 나타냄 |
| env | 컴퓨터 환경과 관련된 정보를 나타냄 |
| version | Node.js 버전을 나타냄|
| verisons | Node.js와 종속된 프로그램 버전을 나타냄 |
| arch | 프로세서의 아키텍처를 나타냄 |
| platform | 플랫폼을 나타냄 |

- 매개변수를 차례대로 출력하고 '--exit' 문자열을 찾으면 입력 시간 후에 프로그램이 종료되도록 만든 예제

~~~
// process.argv
process.argv.forEach(function(item, index){
  // 출력합니다
  console.log("메모리 사용정보(객체반환):",process.memoryUsage());
  console.log(index+':'+typeof(item)+':',item);
  // 실행 매개변수에 --exit가 있을 때
  console.log("프로그램이 실행된 시간:",process.uptime());
  if('--exit' == item){
    // 다음 실행 매개변수를 얻음
    var exitTime = Number(process.argv[index+1]);

    // 일정 시간 후 프로그램을 종료
    setTimeout(function(){
      process.exit();
    }, exitTime);
  }
});
~~~

### exports 객체와 모듈
- nodejs는 모듈을 사용하여 기능을 확장
- 무듈은 기능을 쉽게 사용하고자 메서드와 속성을 미리 정의해서 모아놓은 것
- 다음 예제는 main.js가 module.js 의 기능을 불러와 사용
- 모듈 추출 시 require 함수 사용
- module.js

~~~
// abs:절대값을 구함
exports.abs = function(number){
  if(0 < number)
    return number;
  else
    return -number;
};

//원의 넓이를 구하는 메서드
exports.circleArea = function(radius){
  return radius * radius * Math.PI;
}
~~~

- main.js

~~~
// 모듈을 추출
var module = require('./module.js');

// 모듈을 사용
console.log('abs(-273)=%d', module.abs(-273));
console.log('circleArea(3) = %d', module.circleArea(3));
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
                            