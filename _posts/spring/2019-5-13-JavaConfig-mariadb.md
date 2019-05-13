# JavaConfig mariadb 연결
- pom.xml
- pom.xml에서 mariadb 라이브러리 추가

~~~
<dependency>
	<groupId>org.mybatis</groupId>
	<artifactId>mybatis</artifactId>
	<version>3.4.2</version>
</dependency>

<!-- mybatis-spring -->
<dependency>
	<groupId>org.mybatis</groupId>
	<artifactId>mybatis-spring</artifactId>
	<version>1.3.1</version>
</dependency>

<dependency>
	<groupId>org.mariadb.jdbc</groupId>
	<artifactId>mariadb-java-client</artifactId>
	<version>2.3.0</version>
</dependency>
~~~

### JDBC 연결
- JDBC는 어떤 DB 드라이버든 동일한 코드로 제어할 수 있다.
- myBatis에 비해 같은 코드 반복이 많고 복잡하다. 
- 쿼리 실행 시 DB를 연결하고 닫아줘야 한다
- 많은 사용자들이 db에 원활하게 접속할 수 있게 db 커넥션풀을 미리 만들어놔야 한다.
- getConnection("jdbc:mariadb://접속ip:포트번호/데이터베이스이름", id, 비밀번호)
- 아래 코드가 실패하면 비밀번호, db 존재 확인 그 외 1.권한 확인  2. 포트번호 확인 2. 방화벽 확인(ping test)
- 나는 포트가 올라가있음에도 다른 포트번호와 겹쳐서 그런지(mysql?) mariadb에 접속하지 못했다. 그 후 mariadb 포트번호를 변경하고 접속할 수 있었다.


~~~
import static org.junit.Assert.fail;

import java.sql.Connection;
import java.sql.DriverManager;
import org.junit.Test;
import lombok.extern.log4j.Log4j;

@Log4j
public class mysqlDBTest {

	@Test
	public void testConnection() throws ClassNotFoundException {	
		 Class.forName("org.mariadb.jdbc.Driver");
	    try (Connection con = DriverManager.getConnection("jdbc:mariadb://127.0.0.1:3310/test", "test", "1234"))
		{
			System.out.println(con);
		} catch (Exception e) {
			fail(e.getMessage());
		}
	}
}
~~~