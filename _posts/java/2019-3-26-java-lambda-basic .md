---
layout: post
title: Lambda(람다식)
categories: [java]
tags: [java,lambda]
comments: true
---

### 람다식(Lambda)

- 자바8에서 추가
- cmd 창에서 java -version 명령어를 사용하면 java 버전을 확인할 수 있다(1.8.0_66 라면 두번째 숫자가 8이므로 java 8)
- 함수를 만들지 않고 코드로 실행하는 방식
- 코드를 간단하게 만들 수 있고, 함수를 만들지 않기 때문에 빠르게 개발할 수 있다.
- 익명함수는 재사용이 불가능하고, 디버깅이 어렵다

~~~
(매개변수, ...)->{실행문...}
~~~
- 인터페이스가 하나의 함수만 가지고 있을 때, 함수형 인터페이스라고 한다.(ex Runnable interface)
- 아래 예제에서 Thread 생성 시 Runnable 객체를 매번 생성하고 함수를 정의해야한다.
- 람다표현식을 사용하면 직접 객체를 만들 필요가 없다. JVM이 Thread 생성자를 보고 Runnable을 구현하는 객체로 자동으로 만들어준다.

~~~
public class Test{
       public static void main(String[] args) {
       new Thread(new Runnable() {
                     @Override
                     public void run() {
                           for(int i = 0; i < 10; ++i) {
                                  System.out.println("hello");
                           }
                     }
                     
              }).start();

              new Thread(()-> {
                     for(int i = 0; i < 10; ++i) {
                           System.out.println("hello");
                     }
              }).start();
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
                            