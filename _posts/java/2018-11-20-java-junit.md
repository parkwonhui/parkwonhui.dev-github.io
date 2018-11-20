---
layout: post
title: junit
categories: [java]
tags: [java,junit]
comments: true
---
### TDD( Test Driven Development )
- 테스트 주도 개발
- JUnit은 단위 테스트를 도와주는 프레임워크

### JUnit 
- JUnit test case 파일을 생성한다
- class under test에 테스트할 함수를 찾아서 넣어준다
- assertEquals 로 내가 원하는 값이 알맞게 나오는지 확인한다
- 값이 정상이면 초록색, 비정상이면 붉은색 바가 뜬다

### JUnit 테스트 함수
- assertEquals : 결과값이 예상결과와 같은지 체크
- assertTrue : 예상값이 true인지 체크(true여야 성공, 아니면 실패)
- assertFalse : 예상값이 false인지 체크
- assertNull : 예상값이 NULL인지 체크
- assertNotNull : 예상값이 NULL이 아닌지 체크
- assertSame : 두 객체가 동일한 객체인지 체크
- assertNotSame : 두 객체가 동일한 객체가 아닌지 체크


Main.java

~~~
package testtdd;
public class Main {
     
     public int Add(int value1, int value2){
           return value1+value2;
     }
}
~~~

TddTest.java

~~~
import static org.junit.Assert.*;
import org.junit.Test;
public class TddTest {
     @Test
     public void test() {
           Main m = new Main();
           assertEquals(4, m.Add(1, 3));
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
                            