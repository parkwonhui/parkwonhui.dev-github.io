---
layout: post
title: Interceptor(인터셉터)
categories: [spring]
tags: [spring]
comments: true
---

### Interceptor
- Interceptor란 컨트롤러를 실행할 때 별도의 처리를 할 수 있는 기능

### JavaConfig 설정 방법

- WebMvcConfigurer를 인터페이스 상속한 Servlet class에서 오버라이딩 해야한다
- addInterceptors를 오버라이딩하여 InterceptorRegistration class를 사용해 interceptor class를 등록한다
- addPathPatterns 함수로 interceptor가 가로챌 controller 범위를 설정할 수 있다

~~~
@Bean
public LoginInterceptor loginLogInterceptor() {
       return new LoginInterceptor();
}
@Override
public void addInterceptors(InterceptorRegistry registry)  {
       InterceptorRegistration interceptor =  registry.addInterceptor(loginLogInterceptor());
       interceptor.addPathPatterns("/**");
}
~~~

- HandlerInterceptor를 인터페이스 상속받아 Interceptor 처리 클래스를 만든다
- preHandle 함수는 Controller가 실행되기 전 호출된다
- postHandle 함수는 View를 전부 그리기 전 호출된다
-afterCompletion 함수는 View를 그린 후 호출된다

~~~
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.HandlerInterceptor;
public class LoginInterceptor implements HandlerInterceptor {
      @Override
      public boolean preHandle(HttpServletRequest request,   HttpServletResponse response, Object handler)
                 throws Exception {
          return true;
      }
      
      @Override
      public void postHandle(HttpServletRequest request,   HttpServletResponse response, Object handler,
                 ModelAndView modelAndView) throws Exception {
     }
      
      @Override
      public void afterCompletion(HttpServletRequest request,   HttpServletResponse response, Object handler, Exception ex)
                 throws Exception {
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