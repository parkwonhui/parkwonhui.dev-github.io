---
layout: post
title: Loop(While, For)
categories: [java]
tags: [java]
comments: true
---
### 반복문

while
- (세로)초기식 -> 조건식 -> 명령문 -> 증감식 : 수직방향으로 처리

do while
- 명령을 먼저 실행 후 나중에 조건 체크. 적어도 한번은 실행. 어떤명령을 실행했는데 될 때까지 계속 실행하도록 하고 싶을 때 사용

while
- (세로) 초기식 -> 조건식 -> 명령문 -> 증감식 : 수평방향으로 처리

### break outerloop

- - 중첩  for문에서 사용. 내부 for문에서  중첩 for문 밖으로 나가게 해주는 키워드
- 중첩 for문 위에 outerloop 라벨을 붙여준다
- 중첩 for문을 탈출하고 싶은 위치에 break outerloop를 사용한다
- while문 중첩 시에도 탈출한다
- outerloop 라벨 추가 다음에 바로 반복문이 있어야 한다.(안그러면 에러남)

~~~
outerloop:
             for(int i = 0; i < 3; ++i)
             {
                    for(int j = 0; j < 3; ++j)
                    {
                           if(j == 1)
                                 break outerloop;
                           
                           System.out.println("print!!");
                    }
                    System.out.println(i+"바퀴");
              }
~~~

### 결과

print!!

#### continue outerloop

- 중첩 for문에서 사용.
- 내부for문에서 continue 사용 시 내부 증감연산으로 간다
- 내부for문에서 continue outerloop 사용 시 외부 증감 연산으로 간다

~~~
outerloop:
             for(int i = 0; i < 3; ++i)
             {
                    for(int j = 0; j < 3; ++j)
                    {
                           if(j == 1)
                                 continue outerloop;
                           
                           System.out.println("print!!");
                    }
                    System.out.println(i+"바퀴");
             }
~~~

결과
print!!
print!!
print!!

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
                            