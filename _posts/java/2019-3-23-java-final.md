---
layout: post
title: final 키워드
categories: [java]
tags: [java, final]
comments: true
---

### Final 정리

- 변수에 final 키워드 사용
- 변수의 값을 변경할 수 없음

~~~
public class Test{

	public static void main(String[] args) {
		final int value = 10;			// value 값 변경 불가
	}
}
~~~
- 함수에 final 키워드 사용
- 함수를 상속해서 오버라이딩 할 수 없음

~~~
class A{
	final public void print() {
		
	}
}

class B extends A{
	public void print() {	// error
		
	}
}
~~~
- class에 final 키워드 사용
- class를 상속할 수 없음

~~~
final class A{
	public void print() {
		
	}
}

class B extends A{
	public void print() {
		
	}
}
~~~


~~~

<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
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
                            

			