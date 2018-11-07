---
layout: post
title: Thread Synchronization(스레드동기화,원자성)
categories: [java]
tags: [java,Thread,Synchronization]
comments: true
---
### 스레드 동기화, 원자성 이란
Atomic Operation
원자성이란 소스코드가 한번에 실행된다는 걸 보장해주는 것이다.<br>
스레드끼리는 지역 변수(stack)를 제외한 code, heap, static 내용을 공유한다.<br>
그렇기 때문에 여러 쓰레드가 공용 변수(code, heap, static 데이터)에 접근해서 값을 바꾼다면<br>

제대로 연산이 되지 않는 문제가 발생한다.<br>
예를들어 다음 class 멤버 함수가 있다.(memberId는 class 멤버 변수이다)<br>

~~~
public void Func()
{
    int temp = memberId + 1;
    memberId = temp;
}
~~~

2개의 쓰레드가 Func() 함수에 접근하고 있다면<br>
다음과 같은 상황이 벌어질 수 있다<br>
 (memberid가 0이라고 가정한다)<br>

~~~
int temp = memberid + 1 실행 ( 1번째 쓰레드 접근 )
컨텍스트 스위칭 발생
int temp = memberid + 1 실행 ( 2번째 쓰레드 접근 )
컨텍스트 스위칭 발생
memberid(0) = 1; ( 1번째 쓰레드 접근 )
컨텍스트 스위치 발생
memberid(1) = 1; ( 2번째 쓰레드 접근, memberid에 1번째 쓰레드가 1을 넣어줬으므로 1이다)
~~~~

만약 순서대로 실행되었다면 2가되었을 텐데 서로 접근하다 보니 temp 에 각 쓰레드마다 1을 넣어줘서 값을 뒤집어씌우게 되었다.<br>
그렇다면 다음과 같이 바꾸면 원자성이 보장될까?<br>

~~~
public void Func()
{
    ++memberId;
}

public void Func()
{
    memberId+=1;
}
~~~

이 소스도 원자성이 보장되지 않는다.<br>
한줄이어서 한번에 처리된다고 생각하기 쉽지만<br>
c++ 에서는 한줄코드가 여러개의 어셈블리어로 변환되기 때문에 연산 도중 컨텍스트 스위칭이 일어날 수 있다.<br>
(자바도 비슷한 이유가 있을거라 생각된다.)<br>
<br>
또 멀티 쓰레드 테스트 시 주의할 사항이 있다.<br>
바로 println을 쓰면 안된다는 것이다.<br>
println이 콘솔창에 찍는 처리를 하면서 다른 동작들을 자주 멈추게 하고 성능에 영향을 준다.<br>
그래서 실행 후 결과를 보면 원자성이 보존된 결과가 나와서 착각하기 쉽다.<br>

~~~
public void Func()
{
    println("before threadID:"+id+"meberid:"+memberId);
    memberId+=2;
    println("after threadID:"+id+"meberid:"+memberId);
}
~~~

원자성을 보장하기 위해선 어떻게 해야할까?<br>
synchronized 키워드 : 자동 동기화 블록. 함수에 사용한다. 이 키워드를 사용하면 쓰레드가 함수 사용중일 때 다른 쓰레드는 대기하고, 처리완료 후 함수를 나갔을 때 다른 쓰레드가 들어가게 된다.<br>
volatile 키워드 :  이것은 원자성은 보장하지 않는다. 이 키워드는 메인 메모리에 저장된 값과 동기화 되도록 한다. 그런데 다른 쓰레드에서 메인 메모리에 값을 쓰기 전에 컨텍스트 스위칭이 일어날 수 있으므로 동기화 할 수 없다.<br>
<br>
volatile 설명 url : http://tutorials.jenkov.com/java-concurrency/volatile.html

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
                            