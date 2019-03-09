---
layout: post
title: restController
categories: [java]
tags: [java,spring]
comments: true
---
# RestController 정리
### @RestController
- Controller 어노테이션은 view를 반환다
- RestController 어노테이션은 return 시 Json, xml 등 객체를 반환한다

###  json lib 추가
~~~
<!--  https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.8.8</version>
</dependency>
~~~

### Member.java
- model
~~~
package kosta.model;
public class Member {
       private String name;
       private String email;
       
       public Member(){}
       public Member(String name, String email) {
              super();
              this.name = name;
              this.email = email;
       }
       
       public String getName() {
              return name;
       }
       
       public void setName(String name) {
              this.name = name;
       }
       
       public String getEmail() {
              return email;
       }
       
       public void setEmail(String email) {
              this.email = email;
       }
       @Override
       public String toString() {
              return "Member [name=" + name + ", email=" + email + "]";
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
                            
