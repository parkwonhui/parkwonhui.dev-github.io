---
layout: post
title: Array
categories: [java]
tags: [java]
comments: true
---
### 생성자 호출 순서
C가 B를 상속하고 B가 A를 상속하고 있다

~~~
public class A {
     public A(){
           System.out.println("A 생성자 호출");
     }
}

public class B extends A{
      public B() {
            System.out.println("B 생성자 호출");
      }
}

public class C extends B{
     public C(){
           System.out.println("C 생성자 호출");
     }
}
~~~

결과

~~~
A 생성자 호출
B 생성자 호출
C 생성자 호출
~~~

### this, this(), super, super()
- this : 현재 클래스를 가르킴. this.멤버변수 사용 시 현재 클래스의 멤버변수를 사용
- super : 부모 클래스를 가르킴. super.멤버변수 사용 시 부모클래스의 멤버변수를 사용
만약 B클래스가 a 멤버변수가 없다면 C클래스가 super.a 하면 A의 멤버변수 a가 호출됨

~~~
public class A {
     protected int a = 1;
     public A(){
           System.out.println("A 생성자 호출");
     }
}
public class B extends A{
     int a = 2;
      public B() {
            System.out.println("B class super.a:"+super.a+"  this.a:"+this.a+" a:"+a);
      }
}

public class C extends B{
     int a = 3;
     public C(){
            System.out.println("C class super.a:"+super.a+"  this.a:"+this.a+" a:"+a);
     }
}
~~~
출력결과

~~~
A 생성자 호출
B class super.a:1 this.a:2 a:2
C class super.a:2 this.a:3 a:3
~~~

- this() : 자신의 생성자를 불러온다
- super() : 자신의 부모클래스의 생성자를 불러온다
	- 둘 다 { 다음에 바로 써야한다. 그렇지 않으면 'Constructor call must be the first statement in a constructor' 에러가 난다
	- { 다음에 바로 써야 하기 때문에 this(), super() 동시에 사용하진 못한다

~~~
public class A {
     protected int a;
     public A(){
           this(2);
           System.out.println("A() 생성자 호출");
           //this(2);      // error must be first!
           //A(1);               // error
           //this.A(1);    // error
     }
     
     public A(int a){
           System.out.println("A(int a) 생성자 호출");
           this.a = a;
     }
}
~~~
출력결과

~~~
A(int a) 생성자 호출
A() 생성자 호출
~~~

- 자식 클래스에서 super 호출
~~~
public class B extends A{
     protected int a;
      public B() {
            System.out.println("B()");
      }
      public B(int a){
           super(1);
           System.out.println("B(int a)");
           this.a = a;
      }
}
~~~

출력결과

~~~
A(int a) 생성자 호출
B(int a)
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
                            