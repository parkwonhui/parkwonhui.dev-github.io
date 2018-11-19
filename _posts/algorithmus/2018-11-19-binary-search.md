---
layout: post
title: binary search(이진탐색)
categories: [algorithmus]
tags: [algorithmus]
comments: true
---
### 이진탐색
- 오름차순으로 정렬되어있는 배열에 임의의 중간값을 정한다.
- 찾는 값이 임의의 중간값보다 작으면 큰 쪽(오른쪽) 영역을 탐색에서 제외한다 
- 찾는 값이 임의의 중간값보다 크면 작은 쪽(왼쪽) 영역을 탐색에서 제외한다
- 탐색 영역 왼쪽, 오른쪽 key가 서로 만날 때 까지 반복한다


### source

~~~
public class Main {
       // 배열, 찾는 값, 크기
       static int search(final int[] arr, final int searchValue, final int size) {
              int lp = 0; // left pivot
              int rp = size - 1; // right pivot
              while (rp >= lp) {// lp, rp가 만날 때 까지 반복한다
                                         
                     int key = (lp + rp) / 2;   // 중간 값을 구한다 이를 key라고  한다
                     if (searchValue == arr[key])
                           return key;
                     if (arr[key] < searchValue) // key값 보다 찾는 값이 크다면 왼쪽  범위를 삭제한다
                           lp = key + 1;
                     else                        // key값 보다 찾는  값이 작다면 오른쪽 범위를 삭제한다
                           rp = key - 1;
              
              }
              return -1;
       }
       public static void main(String[] args) {
              int[] arr = { 1, 2, 5, 6, 7, 8, 10, 11, 20, 31 }; // 오름차순 정렬되어있는 배열만 이진 탐색을 할 수 있다 
              int searchNum = 0;                                   // 찾을 값을 넣는다
              System.out.println(searchNum + "은 " + search(arr, searchNum,  arr.length) + "인덱스에 있습니다");
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
                            
