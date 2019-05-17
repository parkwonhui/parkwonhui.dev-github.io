---
layout: post
title: Java Long과 long의 차이
categories: [java]
tags: [java,WrapperClass]
comments: true
---

### Long과 long의 차이
- Long은 Wrapper Class이다. 크기는 8byte (sizeof 함수가 없어서 인터넷에서 찾아봄)
- long은 순수한 자바 자료형이다. 크기는 8byte
- Long.SIZE 에 대한 설명 The number of bits used to represent a long value in two's complement binary form.
- Wrapper Class는 클래스로써 변환해야할 때, 인자값으로 Class를 받을 때 등.. 의 상황에서 사용한다.
- 예를들어 클라로부터 a라는 인자를 받을 때도 있고, 받지 않을 때도 있다. 이 때 a의 값이 없을 때는 null이 대입되므로 Wrapper Class를 사용해야한다.

~~~
int LongSize = Long.SIZE;
System.out.println("longSize:"+LongSize);
~~~

### 문제 상황
- Long의 값이 null일 때 long에 Long값을 대입하면 형변환이 되지 않아 에러 발생
- Long과 long을 혼용해서 사용하고 있었다.. 주의할 것;;

### 궁금한 것
- 받는 값이 long 일 때 null을 long으로 변환하지 못해서 형변환 에러가 나서 예외처리가 된다. 이 때 형변환 에러 처리를 하므로 그대로 두는지, WrapperClass로 받은 후 null체크를 한 다음 처리하는지?
- WrapperClass를 사용한다. 컨트롤 밖보다 안에서 처리를 하도록 한다.

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

