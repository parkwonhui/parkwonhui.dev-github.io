---
layout: post
title: mybatis trim
categories: [java]
tags: [java,mybatis]
comments: true
---
# mybatis trim

### 여러개의 질의어 사용
- if 조건을 사용해서 쿼리문을 동적으로 만들면 어느 데이터가 마지막에 붙는지 모르므로 콤마(,)가 붙어서 에러가 발생한다
- 이 때 trim을 사용해서 마지막 붙은 조건의 콤마를 삭제할 수 있다
- 질의문을 < trim > 으로 감싸준다
- suffixOverrides="," 을 사용하면 마지막 조건의 콤마를 삭제해준다

~~~
<update id = "editCalender" parameterType="ScheduleCalender">
	 update calender
     <trim prefix="SET" suffixOverrides=",">
       <if test="title != null">
        title = #{title},
       </if>
       <if test="startDt != null">
        start_dt = #{startDt},
        </if>
       <if test="endDt != null">
        end_dt= #{endDt},
        </if>
       <if test="backgroundColor != null">
        background_color= #{backgroundColor},
        </if>
       <if test="completionPer != null">
        completion_per= #{completionPer},
        </if>
      </trim>
       where calender_id = #{calenderId}
</update>
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
                            
