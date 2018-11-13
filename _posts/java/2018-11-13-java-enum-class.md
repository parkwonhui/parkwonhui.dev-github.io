---
layout: post
title: Enum Class
categories: [java]
tags: [java,enum,enumclass]
comments: true
---
### enum class 사용하기
- enum은 관련있는 상수의 모음
- 필드와 메소드 추가가 가능하다
- final 로써 사용한다
- class 처럼 함수선언, 오버라이드가 가능하다
- 숫자 뿐 아니라 실제 Type 비교 가능

### 그 외 enum 정리
- enum 첫번째 요소는 0이고 순서대로 번호가 부여된다
- enum이름.요소이름.ordinal() 함수를 사용해서 번호를 확인할 수 있다

### Source
~~~
public class Main {
     enum SHAPE{
           CICLE{
                @Override
                public void draw() {
                      System.out.println("Cicle draw");
                }
                @Override
                public void getName() {    
                     System.out.println(this.getClass().getSimpleName());
                }
                
           },
           RECTANGLE{
                @Override
                public void draw() {
                      System.out.println("Rectangle draw");
                }
                @Override
                public void getName() {    
                     System.out.println(this.getClass().getSimpleName());
                }
                
           },
           TRIANGLE{
                @Override
                public void draw() {
                      System.out.println("triangle draw");                 
                }
                @Override
                public void getName() {
                     System.out.println(this.getClass().getSimpleName());
                }
                
           };
           
           public abstract void draw();
           public abstract void getName();
     }
     
     public static void main(String[] args) {
           
           SHAPE shape = SHAPE.CICLE;
           shape.draw();
           shape = SHAPE.RECTANGLE;
           shape.draw();
           shape = SHAPE.TRIANGLE;
           shape.draw();
     }
}
~~~

결과<br>
~~~
Cicle draw
Rectangle draw
Triangle draw
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
                            