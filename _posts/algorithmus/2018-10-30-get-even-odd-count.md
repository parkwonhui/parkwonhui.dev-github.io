---
layout: post
title: 정수값의 짝수,홀수 갯수 구하기
categories: [algorithmus]
tags: [algorithmus]
comments: true
---

### 문제
정수값에 대해서 전체 자리수 중 짝수, 홀수갯수를 구하자.
(5자리로 한정)삼항연산자

문제풀이
~~~
package kosta.mission;

public class Mission03 {

	public static void main(String[] args) {
		int num = 26129;
		final int max_size = String.valueOf(num).length();
		int[] arr = new int[max_size];
		int i = 1;
		for(int m = 0; m < max_size - 1; ++m)
		{
			i = i * 10;
		}
		
		for(int j = 0; j < max_size; i/=10, ++j)
		{
			
			arr[j] = num / i;		// 나누기 몫을 구함
			num -= (i * arr[j]);	// 나누기 몫 * 현재 자리수 = 현재 자리수의 값만 빼준다
		}
		
		int even = 0;
		int odd = 0;			// 홀수
		for(int k = 0; k < max_size; ++k)
		{
			
			int temp = (0 == (arr[k] % 2)) ? ++even : ++odd;
		}
		
		
		System.out.println("짝수의 개수:"+even);
		System.out.println("홀수의 개수:"+odd);	
	}

}
~~~

문제풀이2
~~~
int num = 12345;
int even = 0;
int odd = 0;
even += (num/10000%2 == 0) ? 1 : 0;
even += (num/1000%10%2 == 0) ? 1: 0;
even += (num/100%10%2 == 0) ? 1: 0;
even += (num/10%10%2 == 0) ? 1: 0;
even += (num%2 == 0) ? 1: 0;
		
odd = 5 - even;

System.out.println("짝수의 개수:"+even);
System.out.println("홀수의 개수:"+odd);	
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
                            