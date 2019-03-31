---
layout: post
title: 소수구하기(PrimeNumber)
categories: [algorithmus]
tags: [algorithmus]
comments: true
---

### 문제
https://www.acmicpc.net/problem/1978

### 풀이
- 소수와 합성수로 나뉜다.
- 소수란 1과 자기 자신의 수만 약수로 가진 자연수.(즉 1은 소수가 아니다)
- 합성수는 약수의 개수가 3개 이상인 수.
- 예를들어 2, 3, 5, 7 은 소수이다.
- 에라토스테네스의 체 알고리즘은 추후 정리

### 소스코드 풀이
- value를 1부터 value 까지의 자연수로 계속 나눈다. 그 중 나누어지면 복합수. 나누어지지 않으면 소수

~~~
import java.util.Scanner;
public class Main{
       public static boolean isPrimeNumber(final int value) {
              if(1 == value)
                     return false;
              
              int val = value;
              for(int i = 2; i < value; ++i) {
                     int mod = val%i;
                     if(0 == mod) {
                           System.out.println("value:"+value+" i:"+i);
                           return false;
                     }
              }
              return true;
       }
       
       public static void main(String[] args) {
              
        Scanner sc = new Scanner(System.in);
        int length = sc.nextInt();
        int[] arr = new int[length];
        int count = 0;
        for(int i = 0; i < length; ++i) {
              arr[i] = sc.nextInt();
              if(true == isPrimeNumber(arr[i])) {
                     ++count;
              }
        }
        
        System.out.println(count);
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
                            
