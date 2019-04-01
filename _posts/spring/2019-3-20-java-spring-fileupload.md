---
layout: post
title: file upload
categories: [spring]
tags: [java,spring]
comments: true
---

### 파일업로드 방식
- form 태그 사용 방식 : 브라우저 제한이 없어야 하는 경우 사용. 일반적으로 페이지 이동과 동시에 첨부파일을 업로드하는 방식
- ajax를 이용하는 방식 : 첨부파일을 별도로 처리하는 방식

### 첨부파일 처리 방식
- cos.jar : 2002년도에 개발 종료. 이제 많이 사용 안함
- commons-fileupload : 일반적으로 많이 활용되고 서블릿 스펙 3.0 이전에도 사용 가능
- 서블릿 3.0 이상 : 3.0 이상부터는 자체적인 파일 업로드 처리가 API 상에서 지원

### 스프링 첨부파일을 위한 설정
- C드라이브 아래에 upload 폴더와 upload 폴더 아래 temp 폴더 생성
- Spring Legacy Project 생성
- pom.xml 버전 변경

~~~
<properties>
    <java-version>1.8</java-version>
    <org.springframework-version>5.0.7.RELEASE</org.springframework-version>
    <org.aspectj-version>1.9.10</org.aspectj-version>
    <org.slf4j-version>1.7.25</org.slf4j-version>
</properties>

<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>3.1.0</version>
    <scope>provided</scope>
</dependency>

<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.0</version>
    <scope>provided</scope>
</dependency>
~~~

- web.xml 변경

~~~
xsi:schemaLocation="http://java.sun.com/xml/ns/javaee  https://java.sun.com/xml/ns/javaee/web-app_3_1.xsd" id="WebApp_ID" version="3.1">
~~~

- <servlet> 태그 내에 <multipart-config> 태그 추가
- max-file-size : 특정 사이즈의 메모리 사용
- max-request-size : 업로드되는 파일의 최대 크기
- max-size-threshold : 한번에 올릴 수 있는 최대 크기

~~~
<multipart-config>
    <location>C:\\upload\\temp</location>
    <max-file-size>20971520</max-file-size>  <!-- 1MB * 20 -->
    <max-request-size>41943040</max-request-size> <!-- 40MB -->
    <file-size-threshold>20981520</file-size-threshold><!-- 20MB -->
</multipart-config>
~~~
- web.xml 설정은 was 자체 설정. 스프링에서 업로드 처리는 MultipartResolver 타입의 객체를 bean으로 등록해야만 가능
- servlet-context.xml 에서 MultipartResolver bean 추가

~~~
<!-- 파일올리기 설정 -->
<beans:bean id="multipartResolver"  class="org.springframework.web.multipart.support.StandardServletMultipartResolver">
</beans:bean>
~~~
- 여기까지 설정하고 실행 시 에러 발생
- web-app에서 version이 중복 설정되어있어서 하나 제거

~~~
정보: At least one JAR was scanned for TLDs yet contained no TLDs. Enable debug  logging for this logger for a complete list of JARs that were scanned but no TLDs  were found in them. Skipping unneeded JARs during scanning can improve startup  time and JSP compilation time.
3월 19, 2019 9:45:43 오후 org.apache.tomcat.util.digester.Digester fatalError
심각: Parse Fatal Error at line 4 column 136: "version" 속성이 "web-app" 요소에  대해 이미 지정되었습니다.
~~~

### form 방식의 업로드
- UploadController 생성

~~~
@Controller
public class UploadController {
       @GetMapping("/uploadForm")
       public void uploadForm() {
              System.out.println("upload form");
       }
}
~~~
- uploadForm.jsp 생성

~~~
<form action="uploadFormAction" method="post" enctype="multipart/form-data">
<input type='file' name='uploadFile' multiple>
<button>Submit</button>
</form>
~~~

- 스프링 MVC에는 MultipartFile 타입을 제공해서 업로드되는 파일 데이터를 쉽게 처리할 수 있음.
- 파일 처리는 MultipartFile 타입 사용
- 여러개의 첨부파일을 첨부할 수 있으므로 배열로 설정
- 파일이름이 한글일 때 처리x 영어만 할 것

~~~
@PostMapping("/uploadFormAction")
       public void uploadFormPost(MultipartFile[] uploadFile, Model model) {
              String uploadFolder = "C:\\upload";
              for(MultipartFile multipartFile : uploadFile) {
                     System.out.println("----------------------------");
                     System.out.println("Upload File  Name:"+multipartFile.getOriginalFilename());
                     System.out.println("Upload File  Size:"+multipartFile.getSize());  
                     
                     File saveFile = new File(uploadFolder,  multipartFile.getOriginalFilename());
                     try {
                           multipartFile.transferTo(saveFile);             //  업로드 되는 파일 저장
                           
                     }catch(Exception e) {
                           
                     }
              }
       }
~~~

### Ajax 방식의 업로드
- Ajax 이용 시 첨부파일 처리는 FormData 객체 사용
- FormData는 가상의 <form>태그와 같다고 생각하면 된다
- uploadAjax.jsp 생성

~~~
<h1>Upload with Ajax</h1>
<div class='uploadDiv'>
	<input type='file' name='uploadFile' multiple>
</div>

<button id='uploadBtn'>Upload</button>

<script src="http://code.jquery.com/jquery-3.3.1.min.js" 
integrity="sha2560FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="crossorigin="anonymous"></script>
<script>
$(document).ready(function(){
	$("#uploadBtn").on("click", function(e){
		var formData = new FormData();
		var inputFile = $("input[name='uploadFile']");
		var files = inputFile[0].files;
		console.log(files);
		
		// add filedate to formdata
		for(var i = 0; i < files.length; ++i){
			formData.append("uploadFile", files[i]);
		}
		
		$.ajax({
			url: '/uploadAjaxAction',
			processData: false,
			contentType: false,
			data: formData,
			type: 'POST',
			success: function(result){
				alert("Uploaded");
			}
		});	// ajax
	});
});
</script>
~~~
- ajaxUpload 처리 Controller에 추가

~~~
@GetMapping("/uploadAjax")
public void uploadAjax() {
   System.out.println("upload ajax");
}
       
@PostMapping("/uploadAjaxAction")
public void uploadAjax(MultipartFile[] uploadFile) {
    String uploadFolder = "C:\\upload";
    for(MultipartFile multipartFile : uploadFile) {
        System.out.println("----------------------------");
        System.out.println("Upload File  Name:"+multipartFile.getOriginalFilename());
        System.out.println("Upload File  Size:"+multipartFile.getSize());  
                     
        File saveFile = new File(uploadFolder,  multipartFile.getOriginalFilename());
        try {
                           multipartFile.transferTo(saveFile);             //  업로드 되는 파일 저장
                           
        }catch(Exception e) {
                           
        }
    }
}
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
                            


