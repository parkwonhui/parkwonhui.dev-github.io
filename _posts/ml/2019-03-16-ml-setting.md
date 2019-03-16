---
layout: post
title: 아나콘다(Anaconda), 주피터 개발환경 세팅
categories: [ml]
tags: [ml]
comments: true
---

# 아나콘다, 주피터 개발환경 구축

### 선형 회귀 인공지능 구현
- x가 값이 올라갈 수록 y데이터가 상승한다
- 이것을 수식에 대입하여 x값이 8일 때 y값을 추측할 수 있다

~~~
import tensorflow as tf
xData = [1,2,3,4,5,6,7]
yData = [25000, 55000, 75000, 110000, 128000,155000, 180000]
W = tf.Variable(tf.random_uniform([1], -100, 100))
b = tf.Variable(tf.random_uniform([1], -100, 100))
X = tf.placeholder(tf.float32)
Y = tf.placeholder(tf.float32)
H = W * X + b  # 수식
cost = tf.reduce_mean(tf.square(H-Y)) # 예측값에서 실제값을 뺀 제곱
a = tf.Variable(0.01) # 경사하강 알고리즘에서 얼마만큼 점프를 하는지
optimizer = tf.train.GradientDescentOptimizer(a) # 텐서플로서에서 제공해주는 경사하강 라이브러리
train = optimizer.minimize(cost)
init = tf.global_variables_initializer()
sess = tf.Session()
sess.run(init)
for i in range(5001):
    sess.run(train, feed_dict={X: xData, Y:yData})
    if i % 500 == 0 :
        print(i, sess.run(cost, feed_dict = {X:xData, Y:yData}), sess.run(W), sess.run(b))

print(sess.run(H, feed_dict={X:[8]})) # x가 8일 때 결과값 출력
~~~

### 아나콘다(Anaconda), 주피터 개발환경
- 콘솔보다 효율적인 개발환경 구축 필요

### 다운로드
- https://www.anaconda.com/distribution/
- window 64bit 다운로드 및 설치
- 설치 시 한글 경로x 그 외 기본 설정으로 next만 누르면 된다
- 설치 시간은 20분 정도 걸린다
- 아래 명령어를 cmd창에 치고 만약 list가 적다면 이전에 설치한 python과 충돌나는 것일 수 있기 때문에 anaconda 설치 경로로 Path를 변경해야한다
- Path는 사용자 변수를 설정해야 하고 2개의 경로를 지정해야한다 \Anaconda3\ , Anaconda3\Scripts\

~~~
python -m pip list --format=legacy
~~~

- list 확인 후 tensorflow를 설치

~~~
pip install tensorflow
~~~ 
- jupyter 실행. 가상의 서버를 만들고 python을 실행시킬 수 있는 gui 툴 제공

~~~
jupyter notebook
~~~

- 텐서플로우 예제 실행. No module named 'numpy.core._multiarray_umath' 에러 남.  원인은 python 3.6버전이라서 텐서플로우 버전을 1.12로 맞춰줘야 한다
- 기존 텐서플로우 삭제 및 1.12.0 버전으로 실행하니 실행이 잘 되었다.

~~~
python -m pip uninstall tensorflow
python -m pip install tensorflow==1.12.0
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
                            

					