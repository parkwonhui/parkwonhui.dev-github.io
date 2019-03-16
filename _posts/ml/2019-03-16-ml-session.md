---
layout: post
title: 텐서플로우(TensorFlow) 아키텍쳐 및 Session
categories: [ml]
tags: [ml,tensorflow]
comments: true
---

https://youtu.be/QNSuzvL6SeA 내용을 정리하였습니다

### 텐서플로우(TensorFlow) 아키텍쳐
- 텐서플로우란 대규모 분산 학습 및 추론을 위한 라이브러리
- 많은 기계학습 모델을 제공
- 크로스 플랫폼 라이브러리(C API가 아래에 존재하고 그 위에 다양한 프로그래밍 언어를 이용해 소스코드 작성 가능)
- 클라이언트는 컴퓨터 연산 과정을 데이터 플로우 그래프 형태로 표현
- Session을 이용해 한번의 그래프 실행 시작을 알릴 수 있음
- 분산된 마스터는 부분 그래프를 정리
- 작업자 서비스에 전달하기 전 그래프 조각으로 분리하고 분배함. 초기화
- 작업자 서비스는 하드웨어에게 커널 기능을 이용하는 그래프 작업의 실행을 관리
- 커널 기능은 개별적인 그래프 작업 처리

### 텐서플로우(TensorFlow) Session
- 아래 코드 실행 시 결과는 Tensor("Add:0", shape=(), dtype=float32)
- 텐서플로우의 기본 실행 단위는 텐서이기 때문이다.
- 일종의 다차원 배열의 객체, 식이라고 볼 수 있음
- constant 및 add는 그래프를 작성한 것이지 연산한 것이 아님
- session은 텐서 데이터를 넣어서 데이터 흐름이 이루어지도록 만드는 것

~~~
import tensorflow as tf
a = tf.constant(2.2)
b = tf.constant(4.2)
c = tf.add(a,b)
print(c)

# 실제 연산
sess = tf.Session()
sess.run(c)
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
                            

					


