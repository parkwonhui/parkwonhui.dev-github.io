---
layout: post
title: facebook login api
categories: [server]
tags: [server,facebookapi]
comments: true
---
# 페이스북 로그인
### 인증과정과 Access token
- 사용자의 id, pass를 가지고 있는 것이 부담스럽다(보안적인 측면에서)
- 그래서 나온것이 Federated Identity(oAuth)
- 페이스북 로그인 문서 참고( https://developers.facebook.com/docs/facebook-login/web/ )

### 페이스북 앱 등록
- https://developers.facebook.com/
- 로그인 후 내앱에서 '새 앱 추가' 클릭 ( fex라고 작성 )
- Display Name 작성 후 Create App
- 새창으로 이동하게 되면 메인 페이지에서 제품추가-'Facebook 로그인'의 설정 클릭(새창 이동을 안한다면 product 클릭)
- Web 선택
- site URL 작성( 연습이므로 http://localhost:8080 ) 그리고 save
- 사이트 맨 위에 발급받은 앱 ID를 확인할 수 있다

### 페이스북 로그인 구현 계획
- developers.facebook 메인 화면에서 상단의 문서를 클릭
- facebook 로그인을 클릭한다
- 웹사이트 또는 모바일 웹사이트 클릭
- 필요한 기능 : sdk 로딩, sdk 초기화, login, logout, isLogined,api

### 테스트앱 만들기
- 도메인이 없으므로 테스트 앱을 만든다(본계정보다 가져오는 정보가 제한적임)
- 메인화면에서 내 앱 클릭
- 해당앱의 아래쪽 화살표를 누르고 '테스트앱을 만드세요' 클릭
- 웹사이트 URL 작성(http://localhost:8080)

### 빠른시작
- 해당 앱의 설정의 기본설정 페이지 안에 '빠른시작' 을 누르면 자신의 앱의 정보를 초기화해주는 코드를 얻을 수 있다

### facebook API 사용
- 유저의 정보를 가져오는 api를 확인한다
- https://developers.facebook.com/docs/graph-api/reference/v3.2/profile

### SourceCode

~~~
<!doctype html>
<html>
<head>
  <title>WEB Welcome</title>
  <meta charset="utf-8">
<script src="http://code.jquery.com/jquery-3.1.1.js"></script>
<script>
function statusChangeCallback(response) {
    console.log('statusChangeCallback');
    console.log(response);
    // 로그인이 되어있다면 connected 상태가 된다
    if (response.status === 'connected') {
      // Logged into your app and Facebook.
        console.log('logined');
      testAPI();
    
    } else {
        console.log('not logined');
      // The person is not logged into your app or we are unable to tell.
      document.getElementById('status').innerHTML = 'Please log ' +
        'into this app.';
    }
  }
  // This function is called when someone finishes with the Login
  // Button.  See the onlogin handler attached to it in the sample
  // code below.
  // 로그인이 되었는지 아닌지 상태를 체크한다
  function checkLoginState() {
    FB.getLoginStatus(function(response) {
      statusChangeCallback(response);
    });
  }
  
  // 앱 초기화 init
  window.fbAsyncInit = function() {
    FB.init({
      appId      : '338796300298727',
      xfbml      : true,
      version    : 'v3.2'
    });
   // FB.AppEvents.logPageView();
    
    FB.getLoginStatus(function(response) {
        statusChangeCallback(response);
      });
  };
  // sdk를 다운받아서 페이지로 가져옴
  (function(d, s, id){
     var js, fjs = d.getElementsByTagName(s)[0];
     if (d.getElementById(id)) {return;}
     js = d.createElement(s); js.id = id;
     js.src = "https://connect.facebook.net/en_US/sdk.js";
     fjs.parentNode.insertBefore(js, fjs);
   }(document, 'script', 'facebook-jssdk'));
  
  function testAPI() {
           console.log('Welcome!  Fetching your information.... ');
           // 이름을 가져오기 위해 api 사용. /me는 로그인한 유저를 가르킨다
           FB.api('/me', function(response) {
           //console.log(response);
             console.log('Successful login for: ' + response.name);
             document.getElementById('status').innerHTML =
               'Thanks for logging in, ' + response.name + '!';
           });
         }
</script>
</head>
<body>
  <div
  class="fb-like"
  data-share="true"
  data-width="450"
  data-show-faces="true">
  <div id="fb-root"></div>
<script>(function(d, s, id) {
  var js, fjs = d.getElementsByTagName(s)[0];
  if (d.getElementById(id)) return;
  js = d.createElement(s); js.id = id;
  js.src =  'https://connect.facebook.net/ko_KR/sdk.js#xfbml=1&version=v3.2&appId=2085645551760952&autoLogAppEvents=1';
  fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));</script>
<div class="fb-login-button" data-max-rows="1" data-size="large"  data-button-type="continue_with" data-show-faces="false"  data-auto-logout-link="true" data-use-continue-as="false"></div>
</div>
</body>
</html>
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
                            