---
layout: post
title: circular queue(원형큐)
categories: [algorithmus]
tags: [algorithmus,queue]
comments: true
---
### 원형 큐 (Circular Queue)
- Queue란 먼저 들어간 데이터가 먼저 나가는 선입선출 자료구조이다
- Queue는 데이터가 들어오면 사용할 수 있는 데이터 공간이 줄어들게 된다
- Queue의 데이터를 앞으로 당기는 것도 데이터 양에 비례해 시간이 걸린다
- Circular Queue란 원형 큐의 단점을 보완해 마지막 배열과 첫번째 인덱스가 붙어져 원형으로 사용되는 것을 말한다
- 첫번째 배열이 비어있다면 값을 배열 끝까지 써도 다시 첫번째 배열에 돌아와 값을 넣는다

### Source
CircularQueue.java

~~~
public class CircularQueue {
       private final int max;            // 큐의 용량
       private int front;                // 첫 번째 요소 커서
       private int rear;                 // 마지막 요소 커서, max랑 만나면 0으로  돌아가기
       private int num;                  // 현재 데이터 수
       private int[] que;                // 큐 본체
       
       public CircularQueue(final int max) {
              this.max = max;
              que = new int[max];
              front = rear = num = 0;
       }
       
       public final int enque(final int value) {
              if(true == isFull())
                     return -1;
              que[rear++] = value;                            // 맨 첫번째 값을  저장한 후 rear은 다음을 가르킨다
              rear %= max;                                           // 나머지  계산하면 0~max-1 값이 나온다
              ++num;
              
              return value;
       }
       
       public final int deque() {
              if(true == isEmpty())
                     return -1;
              
              int value = que[front++];
              front %= max;
              --num;
              
              return value;
       }
       
       public final boolean print() {
              if(true == isEmpty())
                     return false;
              
              for(int i = 0; i < num; ++i)                           // num만큼  queue에 저장된 값을 출력한다
                     System.out.println("["+(front+i)%max+"]:"+que[(front+i)%max]);
              
              return true;
       }
       
       private final boolean isFull() {
              return max <= num ? true : false;
       }
       
       private final boolean isEmpty() {
              return 0 >= num ? true : false;
       }
}
~~~

Main.java

~~~
import java.util.Scanner;
public class Main {
       public static void main(String[] args) {
              Scanner sc = new Scanner(System.in);
              CircularQueue circularQueue = new CircularQueue(10);
              int value = 0;
              try {
                     while(value != 4) {
                           System.out.println("1.enque 2.deque 3.print 4.exit");
                           value = sc.nextInt();
                           switch(value) {
                           case 1:
                                  System.out.println("input value:");
                                  int input = sc.nextInt();
                                  if(-1 == circularQueue.enque(input))
                                         System.out.println("queue pull");
                                  break;
                           case 2:
                                  int deque = circularQueue.deque();
                                  if(-1 == deque)
                                         System.out.println("queue empty");
                                  else
                                         System.out.println("deque:"+deque);
                                  break;
                           case 3:
                                  circularQueue.print();
                                  break;
                           }
                     
                     }
              }catch(Exception e) {
                     System.out.println(e.getLocalizedMessage());
              }
              
              System.out.println("종료");
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
                            

					