---
layout: post
title: java, Scanner 정리
categories: [java]
tags: [java]
permalink: javascanner.html
comments: true
---
### Java가 Compile 할 때?
- 소스코드를 save을 하면 Compile됨
- Error를 일부러 내도 그 순간 Error창에는 아무 변화가 없지만 save 시 Error 메시지가 나타난다 
- Compile하면 컴퓨터가 아는 언어로 변환하고 그 결과로 .class 파일이 나옴

### Java Platform 종류
- Standard Edition : Enterprise를 만들기 위한 기본 솔루션. 표준 자바 플랫폼
- Enterprise Edition : 기업용 솔루션, 웹 기반 서버 개발

### eclipse 주석 단축키
- 블록+ctrl+'/' : // 주석
- ctrl+shift+'/' : /**/ 주석

### int temp8 = 010; 의 결과는?
- 결과는 8
- 숫자 맨 앞에 숫자 0을 붙이는 것은 값이 8진수라는 뜻이다.

~~~
package kosta.basic;

public class Hello {
	public static void main(String[] args) {

		int temp16 = 0xb;			// 16진수 알파벳 0x를 붙인다
		int temp8 = 010;			// 8진수 출력 시 숫자 앞에 0을 붙인다
		String temp2 = Integer.toBinaryString(3); // 2진수 출력하려면 toBinaryString 함수 사용
		System.out.println("temp16:"+temp16);
		System.out.println("temp8:"+temp8);
		System.out.println("temp2:"+temp2);
		
	}
}
~~~

### Scanner로 입출력 받기
~~~
package kosta.mission;

import java.util.Scanner;
public class Mission01 {
	public static void main(String[] args) {
		// TODO Auto-generated method stub

		Scanner sc = new Scanner(System.in);		// 키보드 입력받는 객체가 생성된다
		System.out.print("나이: ");
		int age = sc.nextInt();			// 숫자 입력을 받는다
		sc.nextLine();				// 이거 빼면 제대로 입력값을 받지 않는다
		System.out.print("이름: ");
		String name = sc.nextLine();			// 라인 한 줄 내용을 입력 받는다
				
		System.out.println("age: "+age);
		System.out.println("name: "+name);
		
	}

}
~~~
- nextInt()로 숫자값을 받은 다음 문자열을 받을 땐 반드시 nextLine() 문자열 받기 전에 추가한다
- 숫자를 입력할 때 숫자 + enter. 이 때 enter로 인해 개행문자가 생기는데 만약 다음 라인에서 nextInt()함수로 숫자를 받으면 개행문자는 상관없지만
- nextLine()으로 받으면 개행문자를 입력으로 받아버린다. 그래서 더이상 입력을 할 수 없게 된다.
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
                            