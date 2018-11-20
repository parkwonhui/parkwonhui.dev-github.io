---
layout: post
title: algorithmus basic
categories: [algorithmus]
tags: [algorithmus]
comments: true
---
### 알고리즘 1><br>
고전게임을 잘하기로 소문난 두 형제 종현이와 종원이는 요새 갤러그라는 게임에<br>
푹 빠져 있다. 현재 종현이와 종원이의 점수는 각각 A점과 B점이고, 종현이의 점수는<br>
A는 종원이의 점수 B보다 높거나 같다. 조현이는 매주 점수가 2배씩 상승하지만,<br>
노력파인 종원이는 종현이를 이기기 위해 쉬지 않고 연습한 결과 매일 점수가 3배씩<br>
상승하는 능력을 갖추었다.<br>
이때 며칠이 지나야 종원이가 종현이의 점수보다 높아질 수 있을까?<br>

[입력]<br>
첫 번째 줄에 테스트케이스의 수 T(1<= T<=50)가 주어진다.<br>
각 테스트케이스마다 최초 종현이의 점수 A와 종원이의 점수 B가 각각 공백을 두고<br>
주어진다. 단 최초 종현이의 점수 A는 종원잉의 점수 B보다 크거나 같으면 1점<br>
이상 5천점 이하의 점수이다. (A>=B, 1<=B<=5000)<br>

[출력]<br>
각 줄마다 "#T"(T는 테스트케이스 번호)를 출력한 뒤, 종원이의 점수가 종현이의 점수를<br>
추월하게 되는데 필요한 일수를 출력한다.<br>

[sample input]<br>
4<br>
7 1<br>
8 3<br>
4 4<br>
4500 2<br>

[sample output]<br>
#1 5<br>
#2 3<br>
#3 1<br>
#4 20<br>

### Soruce

~~~

package kosta.algorithm;

import java.util.Scanner;

public class Algo1 {
	
	public static long GetDay(long a, long b){
		
		long day = 1;
		while(true){
			a *= 2;
			b *= 3;
		
			if(a < b) 
				break;
			
			++day;
		}
		
		return day;
	}
	
	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);	
		int whileCount = (sc.nextInt())*2;
		int[] arr = new int[whileCount];
		
		for(int i = 0 ; i < whileCount; i+=2){
			arr[i] = sc.nextInt();
			arr[i+1] = sc.nextInt();
		}
		
		int count = 1;
		for(int i = 0; i < whileCount; i+=2, ++count){
			long result = GetDay(arr[i], arr[i+1]);
			System.out.println("#"+count+" "+result);
		}
	}

}

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
                            

					