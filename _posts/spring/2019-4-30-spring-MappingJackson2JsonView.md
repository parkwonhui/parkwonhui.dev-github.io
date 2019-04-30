---
layout: post
title: MappingJackson2JsonView
categories: [spring]
tags: [java,spring,json]
comments: true
---

## MappingJackson2JsonView

### View Resolver
- 클라이언트의 요청을 받은 결과값으로 View이름을 전달한다. 이 View이름으로 ViewObject를 찾아서 전달할 View 내용을 생성한다
- View 이름을 전달하면서 데이터도 같이 전달하게 된다. 이 때 ajax를 사용 중이라면 값을 전달할 때 마다 일일이 json으로 바꿔야 한다
- MappingJaxkson2JsonView를 사용하면 간단하게 전달할 수 있다.

### 사용법
- pom.xml에서 jackson 라이브러리 사용

~~~
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.0</version>
</dependency>

<dependency>
    <groupId>org.codehaus.jackson</groupId>
    <artifactId>jackson-mapper-asl</artifactId>
    <version>1.9.13</version>
</dependency>
~~~
- ServletContext에 MappingJackson2JsonView 객체를 jsonView라는 이름으로 bean 등록
- MappingJackson2JsonView를 사용하면 ModelAndView가 json형식으로 변한다 => 일일이 json 변환하지 않아도 됨

~~~
@Bean(name="jsonView")
public View mappingJacksonJsonView(){
    return new MappingJackson2JsonView();
}
~~~
- 사용 방법

~~~
@RequestMapping(value = "/post/{seq}", method = RequestMethod.DELETE)
public String delete(@PathVariable("seq") Long seq, Model model, HttpSession session) throws Exception {

    BoardVO boardVO = service.getBoardVO(seq);
    UserVO userVO = (UserVO) session.getAttribute("userVO");
    checkUserNull(userVO);

    ResultMap resultMap = service.deleteVO(seq, userVO, boardVO);
    model.addAllAttributes(resultMap);

    return"jsonView"
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

