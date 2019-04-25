---
layout: post
title: Spring 회원탈퇴 및 게시판 삭제 플래그 추가
categories: [spring]
tags: [java,spring,board]
comments: true
---

### 회원 탈퇴
- 회원 탈퇴 기능을 만들면 탈퇴한 회원여부를 flag로 기록해야한다
- 데이터 보존을 위한 용도
	- 회원탈퇴 추가
	- 탈퇴한 회원 게시물 플래그 수정
	- 탈퇴한 회원 id로 검색안되도록 수정
	- 회원가입 시 탈퇴한 회원과 같은 id라면 
	- 로그인 시 탈퇴한 회원이 아닌 회원의 비밀번호 체크
	- 회원탈퇴 시 게시물도 접근할 수 없도록 만든다. 그러므로 게시물도 삭제 flag가 필요하다

#### 회원 정보 아이콘 추가
- bootstrap awesome font 'fa-user' icon을 추가한다
~~~
<c:when test="${not empty userVO.id}">
    ${userVO.name} 님 환영합니다
    <span id="user-logout-button">로그아웃</span>
    <span id="user-info-form"><i class="fas fa-user fa-2x"></i></span>    
</c:when>
~~~

#### 회원 정보 페이지
- 회원정보 userInfoForm.jsp를 페이지를 추가한다
- 회원정보 아이콘을 누른 뒤 회원이 존재한다면 페이지 이동을 하고 존재하지 않는다면 알람을 띄운다

|url|설명|Method|
|----|----|-----|
|/user/info| 유저가 존재하는지 체크 |POST |
|/user/info| 유저 정보 페이지로 이동 | GET |

#### DB 수정
- 유저 삭제 flag 추가
~~~
alter table user add USER_DEL boolean DEFAULT '0';
~~~

- VO 수정
- 각각의 vo에 userDel, boaderDel 컬럼을 추가한다 

~~~
private boolean userDel;        // userVO에 추가
~~~
- xml 수정
- 유저 정보나 게시판 정보를 수정하는 부분에 Del정보 추가

- 게시판 삭제 수정
### 게시판 삭제 flag 추가

- board 테이블에 삭제 플래그 추가
~~~
alter table board add BOARD_DEL boolean DEFAULT '0';
~~~
- boardVO 추가

~~~
private boolean boardDel;    // boardVO에 추가
~~~

- 삭제버튼 클릭 시 테이블 삭제 대신 flag 수정
- updateBoardDelFlag 쿼리 추가 ( xml )

~~~
<delete id="updateBoardDelFlag" parameterType="Long">
    UPDATE        board
    SET            board_del = 1
    WHERE        board_seq = #{boardSeq}
</delete>
~~~
- 게시판 list 가져오거나 페이징 처리할 때도 삭제여부 조건 추가

~~~
WHERE BOARD_DEL = 0
~~~ 

- dao 를 추가하고 삭제 dao 대신 updateBoardDelFlag Dao 를 호출한다
~~~
 public int updateBoardDelFlag(Long boardSeq) {
	   return update("board.updateBoardDelFlag", boardSeq);
 }
~~~

수정중...

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