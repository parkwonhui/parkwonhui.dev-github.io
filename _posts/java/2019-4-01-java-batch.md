---
layout: post
title: Batch
categories: [java]
tags: [java,batch]
comments: true
---

### Batch

- 대용량의 데이터를 추가나 수정하는 경우 MyBatis에서 쿼리를 하나하나씩 실행하면 느리다.
- 이 때 Batch를 사용할 수 있다. Batch는 MyBatis를 사용하지 않고 여러개의 쿼리를 한번에 실행할 수 있기 때문에 빠르게 데이터 수정이 가능하다.
- addBatch함수는 쿼리문을 실행하지 않고 저장하는 역활을 한다.
- executeBatch함수는 저장된 쿼리문을 한번에 실행한다.
- 1만건 데이터를 5000개 씩 2번 insert 했을 때는 0.149287886초 걸림
- Batch를 사용하지 않고 하나씩 insert 했을 때는 0.757761344초 걸림

~~~
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;
public class Test {
       public static void main(String[] args) {
              
              // 1만건 데이터 넣기
              List<String> list = new ArrayList<String>();
              for(int i = 0; i < 10000; ++i) {
                     list.add(""+i);
              }
              
              Connection conn = null;
              PreparedStatement ps = null;
              
              String sql = "INSERT INTO TEST(NAME, AGE) VALUES (?, ?)";
              
              try {
                     
                     Class.forName("oracle.jdbc.OracleDriver");
                     conn =  DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:xe", "id",  "pass");
                     conn.setAutoCommit(false);
                     ps = conn.prepareStatement(sql.toString());
                     
                     int i = 0;
                 long startTime=System.nanoTime();
                     for(String str:list) {
                           ps.setString(1, str);
                           ps.setString(2, "100");
                           ps.addBatch();                           // 쿼리문 저장
                           ps.clearParameters();             // 파라메터 초기화
                           ++i;
                           
                           if(0 == (i%5000)) {               // 500개 단위로  끊어서 전달
                                  i = 0;
                                  ps.executeBatch();         // 누적된 batch 실행
                                  ps.clearBatch();           // 누적된 batch  초기화
                                  conn.commit();
                           }
                     }
                     long endTime=System.nanoTime();
                     double elapsedTime=(endTime-startTime)/1000000000.0;   //  나노초를 초로 변환
                     System.out.println(elapsedTime+"초");

              }catch(Exception e) {
                     e.printStackTrace();
                     try {
                           conn.rollback();
                     } catch (SQLException e1) {
                           // TODO Auto-generated catch block
                           e1.printStackTrace();
                     }
              }finally {
                     try {
                           ps.close();
                           conn.close();
                     } catch (SQLException e) {
                           // TODO Auto-generated catch block
                           e.printStackTrace();
                     }
              }
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
