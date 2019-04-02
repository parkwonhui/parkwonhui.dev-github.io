---
layout: post
title: Nexacro 설명
categories: [front]
tags: [front, nexacro]
comments: true
---

### Nexacro
- 넥스크로 플랫폼은 비즈니스 UI/UX 플랫폼
- UI/UX를 쉽게 편집할 수 있는 강력한 도구이다
- 화면을 배치하는 부분은 XML기반으로 컴포넌트 등의 정보를 저장
- 빌드과정을 거쳐 자바스크립트 기반의 코드로 변환됨
- xprj 확장자는 Project 정보 파일
- *.xfdl 확장자는 화면, 컴포넌트, 스크립트 등의 파일
- 공식 메뉴얼 : http://docs.tobesoft.com/getting_started_nexacro_17_ko

### 단축키
- CTRL+SHIFT+N : 새로운 프로젝트 만들기
- Ctrl+N : 새로운 폼 만들기(width:800 height:600)
- Crtl+F6 : 실행

### 프로젝트 설명
- 오브젝트의 세부창에 번개모양 아이콘을 글릭하면 기본함수명, 사용자 함수명을 정의할 수 있다
- 기본 함수명은 event 옆에 더블클릭, 사용자 함수명은 그냥 작성
- 실행버튼은 돋보기+번개모양 아이콘. 설정으로 웹으로 올릴수도 있으나 라이센스가 필요함
- Service는 이미지 소스,스크립트,서버경로 등을 편집하는 곳

### 기본예제
- 버튼 아이콘을 눌러서 버튼을 생성한다. 그리고 그 버튼을 더블 클릭한다.
- 임의의 이름을 가진 클릭 이벤트가 생성된다. 클릭 시 동작할 코드를 작성한다.
- 아래처럼 알람을 추가한다. 실행 후 버튼을 클릭하면 알람창이 뜬다.

~~~
arelt("hello world");
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