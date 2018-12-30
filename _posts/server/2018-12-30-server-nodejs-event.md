---
layout: post
title: node.js event
categories: [server]
tags: [server,nodejs]
comments: true
---
# 이벤트
### javascript 이벤트 연결
- 아래 예제에서 load를 '이벤트 이름' or '이벤트 타입'이라고 부름
- 매개변수로 입력한 함수를 '이벤트 리스너' or '이벤트 핸들러'라고 부름

~~~
<script>
    // window 객체에 load 이벤트를 연결
    window.addEventListener('load', function(){
    });
</script>
~~~

### 이벤트 연결
- node.js에서 addEventListener함수를 사용하거나 on함수를 사용하면 이벤트 연결이 된다
| 메서드 이름 | 설명 |
|:--------:|:--------:|
| on(eventName, eventHandler) | 이벤트를 연결 |
- process에 exit 이벤트를 연결했으므로 프로그램이 종료되면 '안녕히가세요'라는 단어를 출력한다

~~~
// process 객체에 exit 이벤트를 연겷
process.on('exit', function(code){
  console.log("안녕히가세요");
});
~~~

- 만약 이벤트 연결을 10번 초과하면 에러가 난다(process.on(exit, function(){}) 을 11번 복사)

~~~
(node:4396) MaxListenersExceededWarning: Possible EventEmitter memory leak detected. 11 exit listeners added. Use emitter.setMaxListeners() to increase limit
~~~

- 이벤트 리스너 개수가 10번 넘어가는 건 빈번하므로 개수를 수정해야한다
- process.setMaxListeners함수를 사용해서 이벤트연결 최대개수를 수정하면 에러가 사라진다
| 메서드 이름 | 설명 |
|:--------:|:--------:|
| setMaxListeners(limit) | 이벤트 리스너 연결 개수를 조절 |

### 이벤트 제거
| 메서드 이름 | 설명 |
|:--------:|:--------:|
| removeListener(eventName, handler) | 특정이벤트의 이벤트 리스너를 제거 |
| removeAllListeners([eventName]) | 모든 이벤트 리스너를 제거 |

~~~
var onUncaughtException = function(error){
  console.log('예외가 발생했다 삭제하자');
  // 이벤트 제거
  process.removeListener('onUncaughtException', onUncaughtException);
};

// process 객체에 onUncaughtException 이벤트를 연결
process.on('uncaughtException', onUncaughtException);

// 2초 간격으로 예외를 발생시킴
var test = function(){
  setTimeout(test, 2000);
  error.error.error();
};

setTimeout(test, 2000);
~~~

### 이벤트 강제 발생
| 메서드 이름 | 설명 |
|:--------:|:--------:|
| emit(event, [arg1], [arg2]) | 이벤트를 강제로 실행 |
- 프로그램 종료 시에도 이벤트 리스너만 실행된다

~~~
process.on('exit', function(code){
  console.log('안녕히 계세요..!');
});

// 이벤트를 강제로 발생
process.emit('exit');
process.emit('exit');
process.emit('exit');
process.emit('exit');

// 프로그램 실행중
console.log('프로그램 실행 중');
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
                            
