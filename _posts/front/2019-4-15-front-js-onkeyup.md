# javascript onkeyup
### onkeyup
- 보통 사용자가 로그인을 하기 위해서 id나 password를 적은 후 엔터키를 누르면 로그인이 된다
- 키를 눌렀는지 여부는 onkeyup 이벤트를 호출하면 알 수 있다.
- onkeyup 이벤트는 key를 누른 후 땠을 때 호출된다.
- Enterkey는 window.event.keyCode 값이 13이다

### onkeydown Example
- 아래 소스를 실행하면 input text 상자안에서 enter 키를 입력할 때마다 console 창에 글자가 출력된다

~~~
<script>
function requestLogin(){
    if(13 == window.event.keyCode){
        console.log('enterKey누름');
    }
}
</script>
</head>
<body>
<input onkeyup="requestLogin();" type="text" value="" />
~~~ 