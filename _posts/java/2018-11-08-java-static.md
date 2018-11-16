---
layout: post
title: static
categories: [java]
tags: [java,static]
comments: true
---
### 클래스의 정적 구성 요소
- static 키워드 사용
- 객체를 생성하지 않고도 사용 가능
- 객체 재생성해도 한번만 만들어짐
- 클래스가 로딩될 때 메모리에 올라간다
- static 함수 호출 시 class이름.static함수이름() 으로 호출한다

### 상수 필드
- final 키워드 사용

### 정적 초기화 블록
- static 키워드가 붙은 블록
- 클래스가 사용되기 전에 자바 가상 기계에 의해 단 한 번 호출됨
- 정적 필드의 초기값 설정에 주로 사용됨
- 멤버변수는 정적 초기화 블록에서 초기화 못함. 메모리에 못 올라갔기 때문.

~~~
class HunderNumbers{
    static int arr[];
    static{
    err = new int[10];
    for(int cnt = 0; cnt < 100; ++cnt)
        arr[cnt] = cnt;
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
                            