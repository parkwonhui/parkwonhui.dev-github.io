---
layout: post
title: node.js 기본 내장 모듈
categories: [server]
tags: [server,nodejs]
comments: true
---
# 기본 내장 모듈
- 아래 url에서 node.js에서 사용하는 기본 내장 모듈 api를 확인할 수 있다
- https://nodejs.org/api/

### os모듈
- node.js 서버가 실행되고 있는 운영체제에 대한 정보

~~~
const os = require('os');
console.log(os.hostname()); // 운영체제의 호스트 이름 리턴
console.log(os.type());   // 운영체제의 이름 리턴
console.log(os.platform()); // 운영체제의 플랫폼 리턴
console.log(os.arch()); // 운영체제의 아키텍처 리턴
console.log(os.release()); // 운영체제의 버전 리턴
console.log(os.uptime()); // 운영체제가 실행된 시간 리턴
console.log(os.loadavg()); // 로드 에버리지 정보를 담은 배열 리턴
console.log(os.totalmem()); // 시스템의 총 메모리 리턴
console.log(os.freemem()); // 시스템의 사용 가능한 메모리 리턴
console.log(os.cpus()); // CPU의 정보를 담은 객체 리턴
console.log(os.networkInterfaces()); // 네트워크 인터페이스의 정보를 담은 배열 리턴
~~~

### url 모듈
- url 분석 및 구문 분석을 위해서 사용

~~~
var url = require('url');
// parse는 url문자열을 url 객체로 변환해서 리턴
var obj = url.parse('https://parkwonhui.github.io/');
console.log(obj);
~~~

### Query String 모듈
- url객체와 쿼리에 관련된 모듈
- 아래 예제는 url 중에 query만 뽑아내는 예제이다
- 그래서 쿼리가 있는 Obj1은 쿼리정보가 출력되지만 쿼리정보가 없는 Obj2는 아무것도 출력되지 않는다

~~~
//모듈을 추출
var url = require('url');
var querystring = require('querystring');

// parse:쿼리문자열을 쿼리 객체로 리턴
var parsedObj1 = url.parse('http://www.hanbit.co.kr/store/books/look.php?p_code= B4250257160');
var parsedObj2 = url.parse('https://parkwonhui.github.io/java/2018/12/28/java-javabean.html');
console.log(querystring.parse(parsedObj1.query));
console.log(querystring.parse(parsedObj2.query));
~~~

###  Util 모듈
- node.js에 보조적인 기능을 모아둠

~~~
var util = require('util');
// 매개변수로 입력한 문자열을 조합해 리턴
var data = util.format('%d + %d = %d', 52, 273, 52+273);
console.log(data);
~~~

### crypto 모듈
- 해시(전자지문)생성과 암호화를 수행하는 모듈
- 아래 예제는 문자열을 암호화해서 해시값을 출력하는 예제

~~~
var crypto = require('crypto');

// 해시생성
var shasum = crypto.createHash('sha256');
shasum.update('werwetg');        // 문자열에 따라 해시 값이 달라진다
var output = shasum.digest('hex');

console.log('crypto_hash:', output);
~~~
- 다음 예제는 암호화 및 복호화를 하는 예제

~~~
var crypto = require('crypto');

var key = 'abce1123123';
var input = 'password';

var cipher = crypto.createCipher('aes192', key);
cipher.update(input, 'utf8', 'base64');
var cipheredOutput = cipher.final('base64');

var decipher = crypto.createDecipher('aes192', key);
decipher.update(cipheredOutput, 'base64', 'utf8');
var decipheredOutput = decipher.final('utf8');

console.log(input);             //  암호화 전
console.log(cipheredOutput);    // 암호화 후
console.log(decipheredOutput);  // 복호화
~~~

### File System 모듈
| 객체 이름 | 설명 |
|:--------:|:--------:|
| readFile(file,encoding, callback) | 파일을 비동기적으로 읽음 |
| readFileSync(file, encoding) | 파일을 동기적으로 읽음 |
| writeFile(file, data, encoding, callback) |파일을 비동기적으로 씀 |
| writeFileSync(file, data, encoding) | 파일을 동기적으로 씀 |

- 파일을 동기적으로 읽는다.
- 그래서 파일 내용다음에 1이 출력된다
~~~
var fs = require('fs');
var text = fs.readFileSync('ttt.txt', 'utf8');
console.log(text);
console.log('1');
~~~

- 비동기적 파일 읽기. readFile 함수를 만나면 이벤트 리스너에 등록하고 파일을 읽으면 이벤트 리스너를 실행
- 비동기적이므로 파일을 읽으면서 프로그램을 실행한다.
- 그래서 1다음에 파일 내용이 출력된다

~~~
var fs = require('fs');

fs.readFile('ttt.txt', 'utf8', function(error, data){
  console.log(data);
});
console.log('1');
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
                            