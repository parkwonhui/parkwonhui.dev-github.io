---
layout: post
title: Android Studio Install
categories: [server]
tags: [server,AndroidStudio]
comments: true
---

# Android Studio Install
### Android Install
- [download](https://developer.android.com/studio/)
- Do not import settings 선택
- Custom 선택
- Performance, Android Virtual Device 선택
- 설치 완료 후 제어판-시스템-고급-환경변수 선택
- 시스템 변수에서 Path 편집. C:\Program Files\Android\Android Studio\jre\bin 추가 후 저장
- 환경변수가 알맞게 잡혔는지 확인하기 위해서 cmd 창을 열고 keytool 입력. keytool 명령어에 대한 정보 출력
- Android 설치 후 뜨는 창에서 Create New Project - Empty Activity 선택
- App Name은 말 그대로 app의 이름
- Package Name은 구글 플레이스토어에 앱의 고유식별자. 중복되면 안됨

### AVD 추가
- 삼성갤럭시 7의 높이, 너비를 가진 AVD를 생성한다
- Tools - AVD - Create Virtual Device - New Hardware Profile 선택
- Screen size 5.1
- Resolution 1440x2560

### Setting 수정
- import를 자동으로 하도록 설정
- File - Settings - Editor - General - Auto Import
- Add unambiguous imports on the fly 체크
- Optimize imports on the floy (for current project) 체크
- Layout view에서 눈모양 아이콘을 클릭한 뒤 Show Layout Decorations 클릭.(앱 아이콘이 보여서 위치가 좀 더 정확해짐)

### 실행
- Shift + F10 을 누르면 안드로이드 폰 화면이 생긴다

### Simple Toast Example
- layout에서 button을 TextView로 끌어서 놓는다
- onClick 이벤트 이름으로 onClick이라고 적어둔다
- 여기까지 하면 아래 xml이 작성된다. 그런데 Button이 빨간색이다. 위치 정보가 없어서 그렇다. 이 때 infer Constraints 버튼을 누르면 위치에 대한 정보가 생긴다
- Before

~~~
<Button
    android:id="@+id/button4"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:onClick="onClick"
    android:text="Button"
    tools:layout_editor_absoluteX="167dp"
    tools:layout_editor_absoluteY="299dp" />
~~~
- After

~~~
<Button
    android:id="@+id/button4"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginBottom="9dp"
    android:onClick="onClick"
    android:text="Button"
    app:layout_constraintBottom_toTopOf="@+id/textView"
    app:layout_constraintStart_toStartOf="@+id/textView" />
~~~
- onClick 함수는 MainActivity에 정의해야한다
- 실행해서 버튼을 누르면 짧은 Toast 메시지가 뜬다

~~~
public void onClick(View v) {
    Toast.makeText(getApplicationContext(),"Hello World",Toast.LENGTH_SHORT).show();
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
                            