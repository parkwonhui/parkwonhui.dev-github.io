---
layout: post
title: javascript 암호화(md5, base64)
categories: [front]
tags: [front, md5, base64]
comments: true
---
# 암호화(MD5, Base64)

### Hash(MD5)
- Hash함수는 text를 고정길이의 hash값으로 바꿔주는 역활을 한다.
- 같은 입력에 대해 같은 값이 나온다.
- 암호화 알고리즘이 공개되어 있어서 보안이 취약하다. 그렇기 때문에 Hash 후 다시 암호화를 해야한다.

### Encryption(base64)
- 정보의 형태나 형식을 보안을 위해 다른 형태로 변경하는 것.
- Base64란 Binary Date를 Text로 바꾸는 Encoding이다.
- 둘의 차이는 Hash는 암호화 기능만 있고, Encryption은 암호화, 복호화 기능을 가지고 있다.

### Javascript Example
- CryptoJS 라이브러리
- CryptoJS.MD5 함수로 쉽게 MD5, Base64를 사용할 수 있다

~~~
<html>
<head>
<script src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
<script src="http://code.jquery.com/jquery-migrate-1.2.1.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/3.1.2/rollups/aes.js"></script>
<script>
$(document).ready(function(){
    // encode
    var hash = CryptoJS.MD5("hello");
    var key = CryptoJS.enc.Utf8.parse(hash);               // hex로 변환
    var base64 = CryptoJS.enc.Base64.stringify(key);  // hex를 원래 포멧으로 변환

    console.log("hash:"+hash);
    console.log("base64:"+base64);
    
    // decrypt
    var decrypt = CryptoJS.enc.Base64.parse(base64);
    var hashData = decrypt.toString(CryptoJS.enc.Utf8);
    console.log("decrypt hash:", hashData);
});
</script>
</head>
</html>
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
