---
layout: post
title: pyramid draw
categories: [algorithmus]
tags: [algorithmus]
---
### 문제

피라미드 그리기

### result

        *
       ***
      *****
     *******
    *********

### 문제풀이

공백은 한칸씩 늘어난다.  그래서1열에 길이가 1씩 증가. 

그리는 위치는 한칸씩 앞으로 간다.

> row value와 공백은 비례한다

> row value와 *위치는 반비례한다

> if(col >= count - row) * 위치를 이렇게 체크할 수 있다

### source

~~~
package kosta.basic;
package pack.com;
import java.util.Scanner;
import MyExample.src.pack.com;
public class Main {
     public static void main(String[] args) {
           // TODO Auto-generated method stub
           Scanner sc = new Scanner(System.in);
           int count = sc.nextInt();
           int starCount = 1;
           int colCount = count;
           for(int row = 0; row < count; ++row )
           {
                for(int col = 1; col <= colCount; ++col)
                {
                      if(col >= count - row)
                           System.out.print("*");
                      else
                           System.out.print(" ");                           
                }
                ++colCount;
                System.out.print("\n");
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
                            