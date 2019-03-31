---
layout: post
title: Stream
categories: [java]
tags: [java,stream]
comments: true
---

### Stream
- 자바 8에서 람다와 함께 추가됨
- Collection을 for, foreach로 다루면 코드가 복잡해지므로 사용
- 함수형 프로그래밍(동작하는 코드를 간단하체 처리. 상태관리x)
- 병렬처리 가능(그러나 ThreadPool을 사용하여 성능저하를 일으킬 수 있음)

### 예제
- reduece 함수를 이용하여 list에 있는 모든 값을 더하고 첫번째 인자인 1을 더해준다,
- 기존 방식보다 소스코드가 줄어들었고 한눈에 코드를 파악할 수 있다.

~~~
public class Test{
       
       public static void main(String[] args) {
              {
              // 기존방식
              int sum = 1;
              List<Integer> list = Arrays.asList(1,2,3);
              for (Integer value : list) {
                     sum += value;                     
              }
                     
              System.out.println("기존방식:"+sum);
       
              }
       
              // 스트림 방식
              List<Integer> list = Arrays.asList(1,2,3);
              int result = list.stream().reduce(1, (a, b) -> a+b );
              System.out.println("스트림방식:"+result);
    }
}
~~~
### Stream 객체 생성
- array이나 Collection을 이용하여 Stream 생성

~~~
public class Test{
       
       public static void main(String[] args) {
              // Array
              int[] arr = new int[]{1,2,3};
              Arrays.stream(arr);
              
              // Collection List, Set..
              List<Integer> list = new ArrayList<Integer>();
              list.add(1);
              list.add(2);
              list.add(3);
              Stream stream = list.stream();
    }
}
~~~
### Stream builder 함수
- Stream의 값을 차례대로 넣는 함수

~~~
public class Test{
       public static void main(String[] args) {
              // Array
              Stream<Integer> arr =  Stream.<Integer>builder().add(1).add(2).add(3).build();
              arr.forEach((x)->System.out.println("value="+x));
       }
}
~~~
### Stream Filter 함수
- b가 포함된 문자열만 Stream<String>에 추가하는 필터링 기능

~~~
public class Test{
       
       public static void main(String[] args) {
              // Array
              List<String> list = Arrays.asList("ab", "bc", "cd", "de");
              Stream<String> str = list.stream().filter(x->x.contains("b"));
              str.forEach((x)->System.out.println("value="+x));
       }
}
~~~

### Stream generate 함수
- Stream에 값을 무한으로 생성하는 함수. 무한으로 생성하기 때문에 limit 함수로 크기를 제한 해야한다

~~~
public class Test{
       
       public static void main(String[] args) {
              // Array
              Stream<String> stream = Stream.generate(() -> "test").limit(10);
              stream.forEach((x)->System.out.println("value="+x));
       }
}
~~~

### Stream distinct 함수
- 요소의 중복값을 제거하는 함수

~~~
public class Test {
	public static void main(String[] args) {
		List<String> fruit = Arrays.asList("사과", "오렌지", "배", "배", "오렌지");
		fruit.stream().distinct().forEach(System.out::println);
	}
}
~~~

### Stream sorted 함수
- 정렬을 하는 함수. 인자 없이 그냥 호출하면 오름차순이고 Comparator.reverseOrder()함수를 호출하면 내림차순이다.

~~~
public class Test {
	public static void main(String[] args) {
		List<Integer> fruit = Arrays.asList(40, 100, -20, 4, 10);
		fruit.stream().sorted().forEach(System.out::println);
		fruit.stream().sorted(Comparator.reverseOrder() ).forEach(System.out::println);
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
                            
