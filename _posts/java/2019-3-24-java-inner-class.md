---
layout: post
title: inner class(내부 클래스)
categories: [java]
tags: [java,innerclass]
comments: true
---

### Inner Class(내부 클래스)
- class 안에 class를 선언하는 것
- 내부 클래스를 감추고 싶거나 OuterClass만 InnerClass를 사용할 때 사용(코드의 복잡성 제거)
- 서로 관련있는 클래스만 묶어줌(예를 들어 같은 회사직원이지만 회사가 다를 때 사용할 수 있다)

~~~
class OuterClass{
       private int value = 20;
       class InnerClass{
              void print() {
                     System.out.println("value:"+value);
              }
       }
}
public class Test{
       
       public static void main(String[] args) {
              OuterClass outer = new OuterClass();
              OuterClass.InnerClass inner = outer.new InnerClass();
              inner.print();
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
                            