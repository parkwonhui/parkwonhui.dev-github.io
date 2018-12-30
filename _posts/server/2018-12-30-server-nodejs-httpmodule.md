---
layout: post
title: node.js http module
categories: [server]
tags: [server,nodejs]
comments: true
---
# HTTP 모듈
### HTTP
- TCP/IP를 기반으로 하는 프로토콜
- 웹서버는 클라이언트에서 요청하면 서버에서 응답을 주는 형식으로 되어있다

### server 객체
- http 모듈에서 가장 중요한 객체는 server객체
- http 모듈의 createServer() 메서드를 사용하면 server 객체 생성
- 아래 예제는 서버가 응답하지 않으므로 페이지에 내용을 표시하지 않고 계속 응답만 기다린다

~~~
var http = require('http');
// 웹 서버를 생성합니다.
var server = http.createServer();
// 웹 서버를 실행합니다.
server.listen(52273);
~~~

| 메서드 이름 | 설명 |
|:--------:|:--------:|
| request | 클라이언트가 요청할 때 발생하는 이벤트 |
| connection | 클라이언트가 접속할 때 발생하는 이벤트 |
| close | 클라이언트가 종료될 때 발생하는 이벤트 |
| checkContinue | 클라이언트가 지속적인 연결을 하고 있을 때 발생하는 이벤트 |
| upgrade | 클라이언트가 HTTP 업그레이드를 요청할 때 발생하는 이벤트 |
| clientError | 클라이언트에서 오류가 발생할 때 발생하는 이벤트 |

~~~
var http = require('http');
// server 객체를 생성
var server = http.createServer();

// server 객체에 이벤트 연결
server.on('request', function(code){
  console.log('Request On');
});

server.on('connection', function(code){
  console.log('Connection On');
});

server.on('close', function(code){
  console.log('Close On');
});

// listen()메서드 실행
server.listen(52273);
~~~

### response 객체
| 메서드 이름 | 설명 |
|:--------:|:--------:|
| writeHead(statusCode, object) | 응답 헤더를 작성 |
| end([data], [encoding]) | 응답 본문을 작성|
- 클라이언트가 서버 응답을 받으면 페이지가 정상적으로 띄워짐

~~~
// 웹서버를 생성하고 실행합니다
require('http').createServer(function(request, response){
  response.writeHead(200, {'Content-Type':'text/html'});
  response.end('<h1>Hello World..!</h1>');

}).listen(60001);
~~~

### File System 모듈을 사용한 HTML 페이지 제공
- javascript 파일 위에서 모든 html 페이지를 문자열로 작성하는 것은 불가능
- file System 모듈을 사용하여 서버에 존재하는 HTML 페이지를 클라이언트에 제공
- html과 js 파일을 생성

~~~
// 모듈을 추출합니다.
var fs = require('fs');
var http = require('http');

// 서버를 생성하고 실행합니다.
http.createServer(function (request, response) {
  // HTML 파일을 읽습니다.
  fs.readFile('6-8.html', function (error, data) {
    response.writeHead(200, { 'Content-Type': 'text/html' });
    response.end(data);
  });
}).listen(52273, function () {
  console.log('Server Running at http://127.0.0.1:52273');
});
~~~

-html
~~~
<!DOCTYPE html>
<html>
<head>
  <title>Index</title>
</head>
<body>
  <h1>Hello Node.js</h1>
  <h2>Author. RintIanTta</h2>
  <hr />
  <p>Lorem ipsum dolor sit amet.</p>
</body>
</html>
~~~

### 이미지와 음악파일 제공
- 60001번 포트로는 이미지 파일 제공. 60002번 포트는 음악 파일 제공
~~~
var fs = require('fs');
var http = require('http');

// 60001번 포트에 서버를 생성하고 실행
http.createServer(function(request, response){
   // 이미지 파일 읽기
   fs.readFile('Chrysanthemum.jpg', function(error, data){
     response.writeHead(200, {'Content-Type':'image/jpeg'});
     response.end(data);
   });
}).listen(60001, function(){
   console.log('Server Running at http://127.0.0.1:60001');
});

// 60002번 포트에 서버를 생성하고 실행
http.createServer(function(request, response){
   // 음악 파일을 읽습니다
   fs.readFile('Kalimba.mp3', function(error, data){
     response.writeHead(200, {'Content-Type':'audio/mp3'});
     response.end(data);
   }).lesten(60002, function(){
     console.log('Server Running at http://127.0.0.1:60002');
   });
});
~~~

### 쿠키 생성
- 쿠키는 key, value로 이루어진 데이터
- 이름, 값 파기 날짜, 경로 정보 등을 가지고 있다
- 일정 기간동안 데이터를 저장할 수 있으므로 로그인을 유지할 때 사용
- response 객체의 Set-Cookie 속석으로 쿠기를 할당할 수 있음
- 아래 예제는 쿠키를 출력하는 예제. 첫 접속 시에는 쿠키가 없으므로 undefined를 출력하지만 두번째 부터는 쿠키의 내용을 출력한다
~~~
var http = require('http');
http.createServer(function(request, response){
  // 변수를 선언
  var date = new Date();
  date.setDate(date.getDate() + 7);

  // 쿠키 입력
  response.writeHead(200, {
    'Content-Type':'text/html',
    'Set-Cookie':['breakfast = toast;Expires = '+ date.toUTCString(), 'dinner=chicken']
  });
  // 쿠키를 출력합니다
  response.end('<h1>'+request.headers.cookie + '</h1>');
}).listen(60001, function(){
  console.log('server Start');
});
~~~

### 페이지 강제 이동
- 네이버 로그인 시 흰화면으로 이동후 재빨리 메인화면으로 이동
- 이렇게 페이지 강제 이동이 발생한다
- 사용법은 응답 헤더의 Location 속성에 이동할 url을 넣어주면 된다
| 응답번호 | 설명 |
|:--------:|:--------:|
| 1XX | 처리중 |
| 2XX | 성공 |
| 3XX | 리다이렉트 |
| 4XX | 클라이언트 오류 |
| 5XX | 서버 오류 |

~~~
var http = require('http');

http.createServer(function(request, response){
  response.writeHead(302, {'Location':'https://parkwonhui.github.io/'})
  response.end();
}).listen(60001, function(){
  console.log('server Start');
});
~~~

### request 객체
- 사용자가 요청한 페이지를 적절하게 제공해주고, 요청 방식에 따라서 페이지를 구분할 수 있음
- url 모듈을 사용해 pathname 추출 후 조건문으로 페이지를 따로 처리
| 속성 이름 | 설명 |
|:--------:|:--------:|
| method | 클라이언트의 요청 방식을 나타냄 |
| url | 클라이언트가 요청한 URL을 나타냄 |
| headers | 요청 메시지 헤더를 나타냄 |
| trailers | 요청 메시지 트레일러를 나타냄 |
| httpVersion | http 프로토콜 버전을 나타냄 |

~~~
var http = require('http');
var fs = require('fs');
var url = require('url');

http.createServer(function(request, response){
  // 변수를 선언
  var pathname = url.parse(request.url).pathname;
  // 페이지를 구분
  if('/' == pathname){
    fs.readFile('6-17.html', function(error, data){
      response.writeHead(200, {'Content-Type':'text/html'});
      response.end(data);
    });
  }else if('/OtherPage' == pathname){
    fs.readFile('6-18.html', function(error, data){
      response.writeHead(200, {'Content-Type':'text/html'});
      response.end(data);

    });
  }

}).listen(60001, function(){
  console.log('server Start');
});
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
                            

