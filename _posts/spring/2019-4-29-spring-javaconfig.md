### Java Configuration
- xml 대신 java로 root, servlet 설정을 함(xml 대신 java로 설정이 느는 추세)
- 아래 예제는 '코드로 배우는 스프링 웹 프로젝트' 책 예제를 정리한 내용

### Java Configuration 방법
- 프로젝트를 생성한다. 임의로 ex.config.test로 지정하였다
- pom.xml 설정
~~~
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://maven.apache.org/POM/4.0.0  http://maven.apache.org/maven-v4_0_0.xsd">
       <modelVersion>4.0.0</modelVersion>
       <groupId>org.zerock</groupId>
       <artifactId>controller</artifactId>
       <name>jex00</name>
       <packaging>war</packaging>
       <version>1.0.0-BUILD-SNAPSHOT</version>
       <properties>
              <java-version>1.6</java-version>
              <org.springframework-version>5.1.5.RELEASE</org.springframework-version>
              <org.aspectj-version>1.6.10</org.aspectj-version>
              <org.slf4j-version>1.6.6</org.slf4j-version>
       </properties>
       <dependencies>
              <!-- Spring -->
              <dependency>
                     <groupId>org.springframework</groupId>
                     <artifactId>spring-context</artifactId>
                     <version>${org.springframework-version}</version>
                     <exclusions>
                           <!-- Exclude Commons Logging in favor of SLF4j -->
                           <exclusion>
                                  <groupId>commons-logging</groupId>
                                  <artifactId>commons-logging</artifactId>
                           </exclusion>
                     </exclusions>
              </dependency>
              
              <dependency>
                     <groupId>org.springframework</groupId>
                     <artifactId>spring-webmvc</artifactId>
                     <version>${org.springframework-version}</version>
              </dependency>
              <dependency>
                     <groupId>org.springframework</groupId>
                     <artifactId>spring-test</artifactId>
                     <version>${org.springframework-version}</version>
              </dependency>
              <!-- AspectJ -->
              <dependency>
                     <groupId>org.aspectj</groupId>
                     <artifactId>aspectjrt</artifactId>
                     <version>${org.aspectj-version}</version>
              </dependency>
              <!-- Logging -->
              <dependency>
                     <groupId>org.slf4j</groupId>
                     <artifactId>slf4j-api</artifactId>
                     <version>${org.slf4j-version}</version>
              </dependency>
              <dependency>
                     <groupId>org.slf4j</groupId>
                     <artifactId>jcl-over-slf4j</artifactId>
                     <version>${org.slf4j-version}</version>
                     <scope>runtime</scope>
              </dependency>
              <dependency>
                     <groupId>org.slf4j</groupId>
                     <artifactId>slf4j-log4j12</artifactId>
                     <version>${org.slf4j-version}</version>
                     <scope>runtime</scope>
              </dependency>
              <dependency>
                     <groupId>log4j</groupId>
                     <artifactId>log4j</artifactId>
                     <version>1.2.17</version>
              </dependency>
              
              <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
              <dependency>
                     <groupId>org.projectlombok</groupId>
                     <artifactId>lombok</artifactId>
                     <version>1.18.6</version>
                     <scope>provided</scope>
              </dependency>
              
              <!-- @Inject -->
              <dependency>
                     <groupId>javax.inject</groupId>
                     <artifactId>javax.inject</artifactId>
                     <version>1</version>
              </dependency>
              <!-- Servlet -->
              <dependency>
                     <groupId>javax.servlet</groupId>
                     <artifactId>servlet-api</artifactId>
                     <version>2.5</version>
                     <scope>provided</scope>
              </dependency>
              <dependency>
                     <groupId>javax.servlet.jsp</groupId>
                     <artifactId>jsp-api</artifactId>
                     <version>2.1</version>
                     <scope>provided</scope>
              </dependency>
              <dependency>
                     <groupId>javax.servlet</groupId>
                     <artifactId>jstl</artifactId>
                     <version>1.2</version>
              </dependency>
              <!-- Test -->
              <dependency>
                     <groupId>junit</groupId>
                     <artifactId>junit</artifactId>
                     <version>4.12</version>
                     <scope>test</scope>
              </dependency>
       </dependencies>
       <build>
              <plugins>
                     <plugin>
                           <artifactId>maven-eclipse-plugin</artifactId>
                           <version>2.9</version>
                           <configuration>
                                  <additionalProjectnatures>
                                         <projectnature>org.springframework.ide.eclipse.core.springnature</projectnature>
                                  </additionalProjectnatures>
                                  <additionalBuildcommands>
                                         <buildcommand>org.springframework.ide.eclipse.core.springbuilder</buildcommand>
                                  </additionalBuildcommands>
                                  <downloadSources>true</downloadSources>
                                  <downloadJavadocs>true</downloadJavadocs>
                           </configuration>
                     </plugin>
                     <plugin>
                           <groupId>org.apache.maven.plugins</groupId>
                           <artifactId>maven-compiler-plugin</artifactId>
                           <version>2.5.1</version>
                           <configuration>
                                  <source>1.8</source>
                                  <target>1.8</target>
                                  <compilerArgument>-Xlint:all</compilerArgument>
                                  <showWarnings>true</showWarnings>
                                  <showDeprecation>true</showDeprecation>
                           </configuration>
                     </plugin>
                     <plugin>
                           <groupId>org.codehaus.mojo</groupId>
                           <artifactId>exec-maven-plugin</artifactId>
                           <version>1.2.1</version>
                           <configuration>
                                  <mainClass>org.test.int1.Main</mainClass>
                           </configuration>
                     </plugin>
                     <plugin>
                           <groupId>org.apache.maven.plugins</groupId>
                           <artifactId>maven-war-plugin</artifactId>
                           <version>3.2.2</version>
                           <configuration>
                                  <failOnMissingWebXml>false</failOnMissingWebXml>
                           </configuration>
                     </plugin>
              </plugins>
       </build>
</project>
~~~
- webapp/resources/spring 아래에 있는 xml 설정파일을 삭제한다
- ex.config.config 패키지를 생성한다. 그리고 RootConfig.java 를 만들고 아래와 같이 코드를 작성
- xml 설정 파일 대신  ex.config.sample 에 있는 클래스를 bean으로 등록

~~~
package ex.config.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(basePackages= {"ex.config.sample"})
public class RootConfig {

    
}
~~~
- Webconfig.xml

~~~
package ex.config.config;
import  org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;
public class WebConfig extends  AbstractAnnotationConfigDispatcherServletInitializer{
       @Override
       protected Class<?>[] getRootConfigClasses() {
              return new Class[]{RootConfig.class};
       }
       @Override
       protected Class<?>[] getServletConfigClasses() {
              // TODO Auto-generated method stub
              return null;
       }
       @Override
       protected String[] getServletMappings() {
              // TODO Auto-generated method stub
              return null;
       }
}
~~~

- ex.config.sample 패키지를 만들고 bean 등록할 class를 생성한다
- Chef.java

~~~
package ex.config.sample;

import org.springframework.stereotype.Component;

import lombok.Data;

@Component
@Data
public class Chef {

}
~~~
- Restaurant.java

~~~
package ex.config.sample;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import lombok.Data;
import lombok.Setter;

@Component
@Data
public class Restaurant {

    @Setter(onMethod_ = @Autowired)
    private Chef chef;
    
}
~~~
- test 폴더에 ex.config.test 패키지 생성. 그리고 junit으로 Test할 JUnitCase 생성

~~~
package ex.config.test;
import static org.junit.Assert.assertNotNull;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
import ex.config.config.RootConfig;
import ex.config.sample.Restaurant;
import lombok.Setter;
import lombok.extern.log4j.Log4j;
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = {RootConfig.class})
@Log4j
public class SampleTests {
       
       @Setter(onMethod_ = @Autowired)
       private Restaurant restaurant;
       
       
       @Test
       public void testExist() {
              
              assertNotNull(restaurant);
              log.info(restaurant);
              
              log.info("-----------------------------------------");
              
              log.info(restaurant.getChef());
              
       }
}
~~~