---
layout: post
title: sort comparable, comparator
categories: [java]
tags: [java,comparator,comparable]
comments: true
---
### Comparable
- 처음 생성 시 정렬 조건을 정함
- CompareTo 함수를 오버라이딩 해서 정렬기준을 재정의한다
- 1: 비교대상의 값이 작다
- 1 : 비교대상의 값이 크다
- 0 : 같다

SortExam.java

~~~
public class SortExam {
     public static void main(String[] args) {
           Random r = new Random();
           TreeSet<Integer> set = new TreeSet<>(new Desending());
           
           for(int i = 0; set.size() < 6;++i){
                int num = r.nextInt(49)+1;
                set.add(num);
           }
           
           System.out.println(set);
     }
}
~~~

Desending.java

~~~
importjava.util.Comparator;
public class Desending implements Comparator<Integer> {
     @Override
     public int compare(Integer o1, Integer o2){
           // 내림차순 대한 정렬기준 정의
           if(o1 < o2)
                return 1;
           else if(o1 > o2)
                return -1;
                      
           return 0;
     }
}
~~~



### Comparator
- 현재 정렬조건과 다른 정렬조건을 설정할 때 사용
- compare 함수를 오버라이딩해서 정렬 기준을 재정의 한다

~~~
mport java.util.ArrayList;
import java.util.Collections;
importjava.util.Comparator;
import java.util.List;
public class SortExam2 {
     
     public static void main(String[] args) {
           List<Person> list = new ArrayList<>();
           
           list.add(new Person("홍자바", 50));
           list.add(new Person("정자바", 80));
           list.add(new Person("한자바", 40));
           list.add(new Person("서자바", 100));
           list.add(new Person("김자바", 20));
           
           Collections.sort(list, new Comparator<Person>() {
                @Override
                public int compare(Person o1, Person o2) {
                      // 이름을 기준으로 오름차순
                      if(o1.getName().compareTo(o2.getName()) >  0)
                           return 1;
                      else  if(o1.getName().compareTo(o2.getName()) < 0)
                           return -1;
                      return 0;
                }
                
                
           });        
           System.out.println(list);
           
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
                            