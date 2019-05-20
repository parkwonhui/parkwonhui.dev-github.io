---
layout: post
title: 계층형 게시판
categories: [spring]
tags: [spring,board]
comments: true
---

# 계층형 게시판 만들기
- 게시물 답글이 가능한 게시판.
- parentSeq(자기 게시물 seq), order, depth 필드를 추가한다.
- parentSeq는 자신이 최상위 게시물일 경우 자신의 seq, 답글일 경우 부모 게시물 seq를 저장한다
- order 는 순서이다. 하나의 최상위 게시물로 묶여진 순서. 이 순서대로 출력된다(그러므로 답글이 달리면 답글 아래의 게시글들은 순서를 하나씩 미뤄야한다)
- depth 는 깊이이다. 최상단이면 0, 최상단 게시물의 답글은 1, 그 답글의 답글은 2.. 이런식으로 늘어난다.\
- order와 depth에 제한이 없도록 한다.

### Index 규칙
- 부모 게시물의 답글이 없다면 부모 게시물의 order+1, depth+1
- 부모 게시물의 답글이 있다면 맨 마지막 게시물 정보에서 order+1

### 게시물 생성 규약
* 클라이언트에게 자신의 부모 게시물 id을 받아야 한다
1. 신규 게시글인지 답글인지 확인한다. 신규 게시글이면 게시물 생성 후 종료
2. 부모 게시물 id로 부모에게 자식이 있는지 확인한다(확인하는 방법은 부모의 계층 정보에서 order+1, depth+1하고 동일한 부모게시물id로 가진 게시물이 있는지 확인하면 된다)
3. 자식이 없다면 부모 정보를 기준으로 계층 정보를 넣어준다. 그리고 새로운 ordering 후 게시물 생성 및 종료
4, 자식이 있다면 마지막 자식을 찾는다. 그 마지막 자식을 기준으로 계층 정보를 넣어준다


### DB 컬럼 추가
- alter table board add parent_seq bigint(20) DEFUALT NULL;
- alter table board add board_order bigint(20) DEFAULT 0;
- alter table board add board_depth int DEFAULT 0;

### VO 수정
- 추가한 필드에 대응되는 멤버 변수 추가

~~~
     private long    parentSeq;
     private int       boardOrder;
     private long    boardDepth;
~~~

### 조회 쿼리 수정
- 게시물 SEQ 순서가 아니라 부모 SEQ, order 순서대로 정렬해야한다.
- 최신 게시물이 위로 올라가야하므로 부모 SEQ는 desc 정렬. 답글은 순서대로 출력되어야 하므로 ASC 정렬
- select로 추가필드를 조회할 수 있도록 수정한다.

~~~
<select id="getTitleVOList" parameterType="SelectVO"  resultType="TitleVO">
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
                   , board_depth as boardDept  
           FROM board
           
           <include refid="searchBoard"></include>
           ORDER BY parent_seq DESC, board_order ASC
           LIMIT #{start}, #{length}  
     </select>
~~~

### 게시물 생성 코드

~~~
private PostReplyVO getMyRelpyVO(PostReplyVO parentReplyVo)  throws Exception {
           if (parentReplyVo == null) {
                throw new  LogicException(Constants.RESULT_STATE.BOARD_UNKOWN_ERROR.getState(), Constants.RESULT_STATE.BOARD_UNKOWN_ERROR.getMessage());                
           }
           
           PostReplyVO myReplyVO = new PostReplyVO();                 // 현재 게시물 자신의 정보
           myReplyVO.setParentSeq(parentReplyVo.getParentSeq());     // 최상위 부모 seq 넣어줌
           
           boolean isChild =  isParentFirstChild(parentReplyVo.getBoardSeq());
           if (!isChild) {                                                      // 자식이 존재하지 않는다
                PostReplyVO lastPostReplyVO =  dao.getPostReplyVO(parentReplyVo.getBoardSeq());  // 직계부모  정보를 가져와서 자신의 정보를 정한다
                if (lastPostReplyVO == null) {
                     throw new  LogicException(Constants.RESULT_STATE.BOARD_UNKOWN_ERROR.getState(), Constants.RESULT_STATE.BOARD_UNKOWN_ERROR.getMessage());
                }
                myReplyVO.setBoardOrder(lastPostReplyVO.getBoardOrder() +  1);
                myReplyVO.setBoardDepth(lastPostReplyVO.getBoardDepth() +  1);
                
           } else {
                PostReplyVO postReplyVO =  getMyParentLastChildBoardReplyVO(parentReplyVo);     // 자신의  부모의 마지막 자식을 찾음
                if (postReplyVO == null) {
                     throw new  LogicException(Constants.RESULT_STATE.BOARD_UNKOWN_ERROR.getState(), Constants.RESULT_STATE.BOARD_UNKOWN_ERROR.getMessage());
                }
                myReplyVO.setBoardOrder(postReplyVO.getBoardOrder() + 1);                // 마지막 자식의 정보를 가지고 자신의 정보를 정한다
                myReplyVO.setBoardDepth(parentReplyVo.getBoardDepth() +  1);  // 부모의 깊이에서 하나 더해주기
           }
           
           return myReplyVO;
     }
~~~

### 자식 있는지 확인 쿼리

~~~
<select id="getParentNextChildBoardCount"  parameterType="PostReplyVO" resultType="int">
   SELECT
                   count(*)
   FROM       board
   WHERE      parent_seq = #{parentSeq} and board_order  = #{boardOrder} + 1 and board_depth = #{boardDepth} + 1
</select>
~~~

### 부모 게시물의 마지막 자식을 찾음

~~~
<select id="getLastReplyBoard" resultType="PostReplyVO"  parameterType="ParamMap" >
   SELECT            
                     board_seq as boardSeq
                   , parent_seq as parentSeq
                   , board_order as boardOrder
                   , board_depth as boardDepth  
   FROM       board
   WHERE      parent_seq = #{parentSeq} and board_depth  >= #{boardDepth} + 1 and (board_order > #{boardOrder}) AND  board_state IN (0, 2)
   ORDER BY   board_order DESC
   LIMIT      0,1
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


