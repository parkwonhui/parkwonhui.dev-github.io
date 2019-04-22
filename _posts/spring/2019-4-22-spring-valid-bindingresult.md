---
layout: post
title: Spring 데이터 검증 @Valid, BindingResult
categories: [spring]
tags: [java,spring]
comments: true
---

# Spring 데이터 검증 @Valid, BindingResult

### 데이터 검증
- @Valid는 객체에 들어가는 값을 검증해주는 어노테이션이다
- 유효한 값인지 검증은 소스코드 여러군데서 이루어지기 때문에 불필요한 중복코드가 늘어나고 복잡하다.
- @Valid를 사용하면 @Min,@Max,@NotNull 등의 어노테이션으로 간단하게 값을 체크할 수 있다
- @@Valid 어노테이션을 사용하는 방법, BindingResult를 사용하는 방법 두가지로 나뉜다.

### @Valid 어노테이션 사용
- validation-api 가 아닌 hibernate-validator 를 추가해야한다.
- validation-api 라이브러리를 사용하게 되면 @Range, @NotNull, @Size 등.. 의 어노테이션으로 검증이 불가하다
- validation-api 를 사용하면 Validator를 상속하는 유효검증 클래스를 만든 후 검증을 구현해야한다(아래에 설명)

~~~
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-validator</artifactId>
    <version>4.2.0.Final</version>
</dependency>
~~~

### model 선언

- @NotEmpty 은 null과 ""는 비허용하고 " " 띄어쓰기는 허용한다
- @Size와 @Range 어노테이션은 값이 지정한 범위내로 들어올 때만 값을 넣어준다
- @message는 에러가 발생할 시 defaultText로 지정할 수 있다

~~~
import javax.validation.constraints.Size;
import org.hibernate.validator.constraints.NotEmpty;
import org.hibernate.validator.constraints.Range;
public class UserInfo {
     @NotEmpty(message="name을 입력해주세요")
     private String  name;
     @NotEmpty(message="비밀번호를 입력해주세요")
     @Size(min = 6, max=10, message = "길이가 알맞지 않습니다")
     private String  password;
     @Range(min = 1, max = 5)
     private int     grade;
     
     public UserInfo() {}
     @Override
     public String toString() {
           return "User [name=" + name + ", password=" +  password + ", grade=" + grade + "]";
     }
     public String getName() {
           return name;
     }
     public void setName(String name) {
           this.name = name;
     }
     public String getPassword() {
           return password;
     }
     public void setPassword(String password) {
           this.password = password;
     }
     public int getGrade() {
           return grade;
     }
     public void setGrade(int grade) {
           this.grade = grade;
     }    
}
~~~

### Contorller 선언
- view에 전달받은 값에 @Valid나 @Validated 어노테이션을 붙인다.
- 에러 체크는 hasErrors 함수를 사용한다
- 에러 리스트는 getAllErrors() 함수로 가져온다
- getDefaultMessage()함수로 defaultError 메시지를 가져올 수 있다

~~~
import org.springframework.stereotype.Controller;
import org.springframework.validation.BindingResult;
import org.springframework.validation.annotation.Validated;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import my.test.model.UserInfo;
@Controller
public class UserController {
     @RequestMapping(value="/joinForm",  method=RequestMethod.GET)
     public String joinForm(){
           return "join";
     }    
     
     @RequestMapping(value="/join", method=RequestMethod.POST)
     public String join(@Validated UserInfo userInfo,  BindingResult bindingResult){
           System.out.println("name:"+userInfo.getName());
           System.out.println("pass:"+userInfo.getPassword());
          System.out.println("error:"+bindingResult.hasErrors());
           
          if(bindingResult.hasErrors()){
                List<ObjectError> list =  bindingResult.getAllErrors();
                for(ObjectError e : list) {
                     System.out.println(e.getDefaultMessage());
                }
                return "join";
           }
           return "home";
     }
}
~~~

### View 선언
- UserInfo 에 들어갈 값을 전달하는 화면을 구성한다.

~~~
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  "http://www.w3.org/TR/html4/loose.dtd">
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html;  charset=EUC-KR">
<title>Insert title here</title>
</head>
<body>
     <form action="/join" method="post">
           <label>이름:</label>
           <input name="name" type="text" id="name">

           <label>비밀번호:</label>
           <input name="password" type="password"  id="password">

           <input type="submit" value="전송">
     </form>
</body>
</html>
~~~

### BindingResult를 사용
- Validator를 상속받는 클래스에서 객체값을 검증하는 방식이다
- hibernate-validator 가 아닌 validation-api 라이브러리를 사용한다

~~~
<dependency>
    <groupId>javax.validation</groupId>
    <artifactId>validation-api</artifactId>
    <version>2.0.1.Final</version>
</dependency>
~~~

### model 선언
- 검증 클래스를 따로 만들어서 거기서 유효값을 체크한다. 그래서 @Min, @Max 등의 어노테이션을 사용하지 않는다

~~~
public class UserInfo {
     private String name;
     private String password;
     
     public UserInfo() {
     }
     public String getName() {
           return name;
     }
     public void setName(String name) {
           this.name = name;
     }
     public String getPassword() {
           return password;
     }
     public void setPassword(String password) {
           this.password = password;
     }
}
~~~

### validator 선언
- 객체를 검증할 validator 클래스를 생성
- Validator를 인터페이스 상속 후 supports, validate 함수를 재정의 한다.
- validate 함수에서 값이 유효한지 체크한다.

~~~
package test.controller;
import org.springframework.validation.Errors;
import org.springframework.validation.Validator;
import test.VO.UserInfo;
public class UserInfoValidator implements Validator{
     public UserInfoValidator() {
     }
     @Override
     public boolean supports(Class<?> clazz) {
            return UserInfo.class.isAssignableFrom(clazz);
     }
     @Override
     public void validate(Object target, Errors errors) {
           UserInfo userInfo = (UserInfo) target;
           
           String mName = userInfo.getName();
           if(null == mName || mName.trim().isEmpty()) {
                System.out.println("회원이름을 이름하세요");
                errors.rejectValue("name", "공백");
           }
           
           String password = userInfo.getPassword();
           if(null == password || password.trim().isEmpty()) {
                System.out.println("회원 비밀번호를 입력하세요");
                errors.rejectValue("password", "공백");
           }
     }
}
~~~

### Contorller 선언
- UserInfo값을 받을 때 BindingResult 객체의 값도 받습니다.
- join url에 호출될 때 마다 initBinder 함수가 호출되면서 UserInfoValidator 객체를 생성한 후 해당 객체의 validate 함수를 호출해서 값이 유효한지 체크한다
- bindingResult.hasErrors() 함수로 값이 알맞은지 체크할 수 있다.
- View는 위 예제와 동일하다
 
~~~
import java.text.DateFormat;
import java.util.Date;
import java.util.Locale;
import javax.validation.Valid;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.validation.BindingResult;
import org.springframework.validation.annotation.Validated;
import org.springframework.web.bind.WebDataBinder;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.InitBinder;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import lombok.extern.log4j.Log4j;
import test.VO.UserInfo;

@Controller
public class HomeController {
     
     private static final Logger logger =  LoggerFactory.getLogger(HomeController.class);
     @RequestMapping(value = "/", method = RequestMethod.GET)
     public String home(Locale locale, Model model) {
           logger.info("Welcome home! The client locale is {}.",  locale);
           
           Date date = new Date();
           DateFormat dateFormat =  DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG,  locale);
           
           String formattedDate = dateFormat.format(date);
           
           model.addAttribute("serverTime", formattedDate );
           
           return "home";
     }
     
     @GetMapping(path = "/joinForm")
     public String joinForm(){
           
           return "join";
     }    
     
     @PostMapping(path = "/join")
     public String join(@Validated UserInfo userInfo,  BindingResult bindingResult){
           System.out.println("name:"+userInfo.getName());
           System.out.println("pass:"+userInfo.getPassword());
           
          System.out.println("error:"+bindingResult.hasErrors());
           
           if(bindingResult.hasErrors()){
                return "join";
           }
           
           return "home";
     }    
     
     
     @InitBinder
     protected void initBinder(WebDataBinder binder) {
           binder.setValidator(new UserInfoValidator());
     }
}
~~~

### Valid방식과 BindingResult 방식
- @Valid 방식을 사용하면 유효범위값을 쉽게 체크할 수 있다. BindingResult도 유효범위를 체크하지만 직접 유효범위 체크 코드를 추가해야하므로
@Valid 방식이 좀 더 사용하기 편했다. BindingResult는 일반적으로 유효값을 체크하는 방식보다는 더 간편하고 깔끔하다.

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