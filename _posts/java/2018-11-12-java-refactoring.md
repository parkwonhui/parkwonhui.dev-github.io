---
layout: post
title: refactoring 이란(상수,제어플래그,assert)
categories: [java]
tags: [java,refactoring]
comments: true
---
### 리팩토링(refactoring) 이란?
- 외부에서 보는 프로그램 동작은 바꾸지 않고 프로그램의 내부 구조를 개선하는 것

### 동작이 변하지 않은 걸 확인하는 테스트
- unit 테스트 반드시 필요
- 리팩토링 전에 테스트->리팩토링->리팩토링 후 다시 테스트
- 입문자라면 junit 테스트 프레임워크 사용해볼 것

### 리팩토링이 필요한 코드들
- 같은 코드 중복, 사양 변경이 있을 때 수정 내용이 곳곳에 흩어져 있다, 언제나 다른 클래스 내용을 수정하는 클래스가 있다
- 합쳐서 다뤄야 할 데이터가 한 클래스에 모여있지 않다, 메서드 호출 연쇄가 너무 많다 등..

### 리팩토리 방법
- 한번에 하나의 수정만 한다(ex 함수 옮기기, 함수 이름바꾸기가 있다면 함수 옮기기->테스트->이름바꾸기->테스트 한번에 하나만 수정하고 따로 테스트 해야한다) 
- 되돌리게 쉽게 하기: 코드가 섞여 있으면 되돌리기 어렵다
- 단계마다 확인: 새로운 클래스 생성 후 빌드 테스트, 빌드 성공 후 새로운 클래스를 사용하면서 버그 테스트
- 오래된걸 바꿈: 동작하는 상태를 유지하면서 새로운 코드를 추가하고 잘 동작하면 오래된 것을 제거한다

### 리팩토링 상황
1. 상수인 숫자가 있다면 기호 상수로 바꾸어라(100 -> MAX_COUNT)
- 상수의 의미를 파악하기 어렵고, 상수가 바뀐다면 관련 상수가 맞는지 확인하면서 일일이 바꿔줘야 한다
- JAVA에서 상수를 만드는 방법은 static final 클래스 필드 사용, enum 사용이 있다
- static final 을 사용할 수 있지만 상수 대신 숫자 0을 적어도 문제 없이 작동한다
- 인자를 int에서 클래스로 치환하거나 enum을 사용해서 잘못된 사용을 막을 수 있다
수정 전

~~~
if(command == 0) {
        System.out.println(name+"works");
}else if(command == 1){
        System.out.println(name+"stops");
}
~~~

수정 후

~~~
if(command == Command.WALK) {
    System.out.println(name+"works");
}else if(command == Command.STOP){
    System.out.println(name+"stops");
}
~~~

- 기호 상수가 적합하지 않은 경우
배열에는 length라는 필드가 있다

~~~
for(int i = 0; i < ARR_COUNT; ++i){
}
~~~

2. 제어 플래그 삭제
- 처리 흐름을 제어하는 플래그를 지나치게 사용하면 가독성이 떨어진다
- 아래 예제에서 flag가 정확히 어떤의미인지 불분명하므로 found로 변수명을 수정한다
- 복잡한 이중 체크 대신 찾은 시점에서 바로 break를 시킵니다
- 찾은 시점에서 바로 return 합니다. 그러면 found 변수가 필요없다는 걸 알 수 있습니다
FindInt.java<br>

~~~
public class FindInt {
       public static boolean find(int[] data, int target) {
              boolean flag = false;
              for(int i = 0;  i < data.length && !flag; ++i) {
                     if(data[i] == target) {
                           flag = true;
                     }
              }
              
              return flag;
       }
       
}

Main.java
public class Main {
       
       public static void main(String[] args) {
              int[] data = {
                     1, 9, 0, 2, 8, 5, 6, 3, 4, 7,
              };
              
              if(FindInt.find(data, 5)) {
                     System.out.println("Found!");
              }else {              
                     System.out.println("Not found!...");
              }
       }
}
~~~

변경 후 FindInt.java<br>

~~~
public class FindInt {
       public static boolean find(int[] data, int target) {
              for(int i = 0;  i < data.length; ++i) {
                     if(data[i] == target)
                           return true;
              }
              return false;
       }
}
~~~

3. assert 도입
- 주석으로 이 상황에 알맞은 값을 적어도 프로그램 실행 시 다른 값이 올 경우 처리 방법이 없다
- assert 도입 시 잘못된 값이 들어올 경우 에러를 발생시킨다
- assert 도입으로 인해 변경되는 내용이 없어야 한다
- 이클립스에서 assert를 사용하려면 메뉴 Run-Run Configurations-Argments의 VM arguments에서 -ea를 추가한다
- 아래 소스코드 주석에서 체크하는 함수를 만든 뒤 원하는 결과인지 assert로 체크한다

SortSample.java

~~~
public class SortSample {
       private final int[] data;
       
       public SortSample(int[] data) {
              this.data = new int[data.length];
              System.arraycopy(data, 0, this.data, 0, data.length);
       }
       
       public void sort() {
              for(int x = 0; x < this.data.length - 1; ++x) {
                     int m = x;
                     for(int y = x+1; y < data.length; ++y) {
                           if(this.data[m] > this.data[y]) {
                                  m = y;
                           }
                     }
                     
                     // 여기서 data[m]은 data[x]~data[data.length - 1]의  최솟값이어야 함
                     int v = data[m];
                     data[m] = data[x];
                     data[x] = v;
                     // 여기서 datat[0]~data[x+1]은 이미 정렬되어 있어야 함
              }
       }
       
       public String toString() {
              StringBuilder buffer = new StringBuilder();
              buffer.append("[ ");
              for(int i = 0; i < data.length; ++i) {
                     buffer.append(data[i]);
                     buffer.append(", ");
              }
              buffer.append("]");
              return buffer.toString();
       }
}
~~~

Main.java<br>

~~~
import java.util.Random;
public class Main {
       private static final Random random = new Random(1234);
       
       private static void execute(int length) {
              // 난수로 데이터 작성
              int[] data = new int[length];
              for(int i = 0; i < data.length; ++i) {
                     data[i] = random.nextInt(data.length);
              }
                     
              // 데이터 표시
              SortSample sorter = new SortSample(data);
              System.out.println("BEFORE:"+sorter);
              
              // 정렬해서 표시
              sorter.sort();
              System.out.println("AFTER:"+sorter);
              
              System.out.println();
       }
       
       public static void main(String[] args) {
              execute(10);
              execute(10);
              execute(10);
              execute(10);
              execute(10);         
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
                            