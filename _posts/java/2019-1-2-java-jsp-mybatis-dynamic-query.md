# 동적쿼리
### 동적쿼리란?
- db 데이터를 crud할 때 조건이 변할 수 있다
- 제목으로 게시물 검색, 작성자이름으로 게시물 검색이 있을 때 조건이 제목, 작성자 이름 둘 중하나로 바뀐다
- 이 때 조건이 계속 바뀌므로 동적 쿼리를 사용해서 조회해야한다
- 아래 예제에서 foreach는 조건이 여러개일 때(ex 체크박스) 사용한다
- collection은 foreach로 돌때마다 선택되는 객체를 의미한다. area 객체 개수만큼 foreach문이 돈다
- item은 구분하기 위한 임의의 이름이다
- separator은 반복되는 사이에 출력할 구문이다

### Source
~~~
<select id="listBoard" resultType="Board" parameterType="Search">
    select * from board
    <if test="area">
    <where>
        <!--( title LIKE %aa% OR writer LIKE %aa% )-->
        <foreach collection="area" item="item222"  separator="OR" open='(' close=')'>
        <!-- $로해줘야한다 상수처럼 리터럴 상수처럼 사용되어야  한다. 변수가 되면 안되기 때문에 #->$ -->
         ${item222} LIKE #{searchKey}
         </foreach>
         </where>            
   </if>
</select>
~~~


