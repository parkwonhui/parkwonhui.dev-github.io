---
layout: post
title: ArrayList, HashMap
categories: [java]
tags: [java,arraylist,hashmap]
comments: true
---
### 자료구조란?
데이터를 효율적으로 사용할 수 있도록 구조를 만들어서 저장해둔 것

### 자료구조 종류
- 리스트 (ArrayList, LinkedList)
- 스택 (LinkedList )
- 큐 (LinkedList)
- 해시 테이블 (HashMap)
- 집합(HashSet, key와 value가 한 쌍)

### ArrayList
- 순서가 있는 자료구조
- 배열의 길이가 제한이 없다
- ArrayList<DataType> list = new ArrayList<DataType>();
- ArrayList는 내부에 있는 배열에 데이터를 저장. 전체를 순회할 때 사용하면 좋다
- ArrayList는 데이터 삭제하면 자동으로 정렬해준다. 하지만 수정, 삭제가 많으면 성능이 떨어진다
- LinkedList는 인접한 데이터가 서로 메모리를 가르키는 식으로 저장. 수정, 삭제힐 떼 가르키는 주소만 바꾸면 되므로 성능이 좋다
- 보통 web은 view에 list를 뿌려주는 일을 많이 한다=>ArrayList(수정,삭제는 db에서 많이 하므로)

~~~
import java.util.ArrayList;
public class ListEx {
     public static void main(String[] args) {
         ArrayList<String> list = new ArrayList<String>();
        list.add("one");                // 값 추가
        list.add("two");
        list.add(2,"three");            // 값 인덱스로 추가
        list.remove(2);                     // 값 삭제
        list.add(1,"four");
        
        int index = list.indexOf("one");               // 값으로  index 찾기
        System.out.println("index:"+index);
        
        int num = list.size();
        for(int cnt = 0; cnt < num; ++cnt){
             System.out.println(list.get(cnt));        // 값  index로 가져와서 출력하기
        }
     }
}
~~~

### iterator
- 자바의 컬렉션클래스 데이터를 읽어오는 방법 중 하나
- 만약 iterator가 없다면 각 컬렉션 클래스의 값 얻어오는 함수를 알고 있어야 한다. 하지만 iterator를 사용하면 어떤 컬렉션 객체이든간에 iterator로 쉽게 값을 가져올 수 있다

~~~
public static void Show(ArrayList<Integer> list){
           Iterator<Integer> itr = list.iterator();
           while(itr.hasNext()){
                System.out.print(itr.next()+",");
           }
}
~~~

### 스택
- 맨 마지막에 넣은 데이터를 먼저 꺼낸다

~~~
import java.util.LinkedList;
public class LinkedListEx {
     
     public static void main(String[] args) {
           LinkedList<Integer> stack = new LinkedList<Integer>();
           stack.addLast(1);
           stack.addLast(30);
           stack.addLast(33);
           
           while(!stack.isEmpty()){
                Integer num = stack.removeLast();
                System.out.print(num+","); // 출력결과는 33,30,1  최근 넣은 것 부터 출력
           }
     }
}
~~~

### 해쉬테이블
- 데이터가 key, value로 쌍이 이루어진다
- key를 연산을 거쳐 해시값으로 만든다. 예를들어 String 값 "111'을 넣는다면 연산을 통해 해시값이 된다. String을 검색하는 것보다 빠르게 찾을 수 있기 때문에 검색 선능이 향상된다
- key 값은 중복 불가능하다
- 멀티쓰레드에서 문제가 될 수 있으므로 HashTable을 쓴다

~~~

import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;
import java.util.Set;
public class HashEx {
     public static void main(String[] args) {
           HashMap<Integer, String> map = new HashMap<Integer,  String>();
           map.put(1, "one");               // 값 넣기
           map.put(2, "two");
           map.put(3, "three");
           String str = map.get(1);   // 값 가져오기
           System.out.println(str);
           
           if(true == map.containsKey(1))   // 값 체크
                System.out.println("값 1은 있다");
           else
                System.out.println("값 1은 없다");
           
           // map은 iterator을 사용할 수 없으므로 map.keyset,  map.entryset을 사용한다
           System.out.println("=== entryset ===");
           Set set = map.entrySet();
           Iterator iter = set.iterator();
           while(iter.hasNext()){
                Map.Entry<Integer, String> mapTemp =  (Map.Entry<Integer, String>)iter.next();
                System.out.println("key:"+mapTemp.getKey()+"value:"+mapTemp.getValue());
           }
           
           // keyset
           System.out.println("=== keyset ===");
           Set<Integer> set2 = map.keySet();
           Iterator<Integer> iter2 = set2.iterator();
           while(iter2.hasNext()){
                int key2 = iter2.next();
                String str2 = map.get(key2);
                System.out.println("key:"+key2+" value:"+str2);
           }

         // map.values(); 를 사용해서 Collection으로 Iterator 하는 방법도 있다
         // Collections.max(values); // 가장 큰 값
         // Collections.min(values) // 가장 작은 값
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
                            