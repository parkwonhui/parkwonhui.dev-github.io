---
layout: post
title: Mybatis 객체 안에 객체 매핑
categories: [spring]
tags: [java,resultMap,association]
comments: true
---

# Mybatis 객체 안에 객체 넣기
- Class 안에 Class를 멤버변수로 가지고 있을 때 Mybatis에서 ResultMap과 association를 사용하여 값을 매핑한다.
- 현재 TitleVO 클래스 안에 PostReplyVO 클래스가 데이터형인 멤버변수를 가지고 있다

### TitleVO.java

~~~
@Data
public class TitleVO {
     private long    boardSeq;
     private String  title;
     private String  writer;
     private Date    date;
     private String  dateString;
     private long    count;
     private String  userId;              // userId가 아니라  Name아닌가?
     private long    userSeq;
     private boolean boardDel;
     private PostReplyVO postReplyVO; // 게시물 화면에서 그릴 때  순서 필요
     public PostReplyVO getPostReplyVO() {
           return postReplyVO;
     }
}
~~~

### PostReplyVO.java

~~~
@Data
@NoArgsConstructor
@AllArgsConstructor
public class PostReplyVO {
     private long    boardSeq;
     private long    parentSeq;
     private int          boardOrder;
     private long    boardDepth;
}
~~~

### postReply ID 지정
- TitleVO를 매핑시키는 resultMap을 선언한다.
- TitleVO의 일반 멤버 변수는 그대로 매핑한다.
- property에는 멤버변수 이름, column 은 필드 이름을 적는다(as를 사용하여 별명을 적음)
- TitleVO의 class변수는 association 을 사용해서 매핑한다.
- association 의 propery는 TitleVO 에서 PostReplyVO 멤버변수 이름, javaType은 매핑할 클래스 이름 PostReplyVO을 적어둔다


~~~
<resultMap id="postReply" type="TitleVO">
   <id property="boardSeq" column="boardSeq" />
   <id property="title" column="title" />
   <id property="writer" column="writer" />
   <id property="date" column="date" />
   <id property="count" column="count" />
        <association property="postReplyVO"  javaType="PostReplyVO" >
             <result property="boardSeq"  column="boardSeq" />
             <result property="parentSeq"  column="parentSeq" />
             <result property="boardOrder"  column="boardOrder" />
             <result property="boardDepth"  column="boardDepth" />
        </association>
</resultMap>
~~~

### 쿼리문
- resultMap을 추가하고 위에서 정의한 ResultMap ID 를 적어준다.

~~~
<select id="getTitleVOList" parameterType="SelectVO" resultMap="postReply">
    SELECT board_seq as boardSeq
           , title
           , writer
           , date
           , count
           , user_id as userId
           , user_seq as userSeq
           , board_del as boardDel
           , parent_seq as parentSeq
           , board_order as boardOrder
           , board_depth as boardDepth  
    FROM    board
    
    <include refid="searchBoard"></include>
    ORDER BY parent_seq DESC, board_order ASC
    LIMIT #{start}, #{length}    
</select>
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

