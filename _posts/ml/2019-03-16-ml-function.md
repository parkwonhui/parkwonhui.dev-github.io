---
layout: post
title: 텐서플로우(TensorFlow)상수, 변수, 함수
categories: [ml]
tags: [ml,tensorflow]
comments: true
---
- https://youtu.be/JbrBKPm1QEo 의 내용을 요약하였습니다

### 텐서플로우(Tensorflow) 변수와 상수
- jupyter notebook 명령어로 GUI 환경에서 실습
- constant는 하나의 자료형을 반환
- session은 하나의 연산식을 실행시키는 객체

~~~
a = tf.constant(1)
b = tf.constant(2)
c = tf.add(a, b)
sess = tf.Session()
sess.run(c)
~~~

- 만약 그냥 c를 출력하면 Tensor 정보만 나온다. 왜냐하면 c는 Tesor 자료형일 뿐이기 때문이다.

~~~
print(c)

결과
Tensor("Add:0", shape=(), dtype=int32)
~~~
- 변수는 상수와 달리 Variable 함수를 사용한다

~~~
import tensorflow as tf
a = tf.Variable(5)
b = tf.Variable(3)
c = tf.multiply(a, b)
init= tf.global_variables_initializer()
sess = tf.Session()
sess.run(init)
sess.run(c)
~~~

- 변수이므로 다른 값을 넣을 수 있다
- 이 때 sess를 global_variables_initializer로 초기화 해줘야 한다

~~~
a = tf.Variable(15)
c = tf.multiply(a, b)
init = tf.global_variables_initializer()
sess.run(init)
sess.run(c)
~~~

### 텐서플로우(Tensorflow) 플레이스 홀더(Placeholder)
- 학습 데이터를 포함하는 변수
- 다른  텐서를 할당하기 위해 사용
- 실제로 값을 할당할 때는 피딩을 수행
- 텐서 자체가 다차원 배열과 같은 형태를 가지고 있어 플레이스 홀더로 사용할 값 또한 배열이 들어갈 수 있음
- 사용법

~~~
tf.placeholder(dtype, shape, name)
~~~
- dtype : 플레이스 홀더에 저장되는 자료형
- shape : 배열의 차원
- name : 플레이스 홀더의 이름

~~~
import tensorflow as tf
mathScore = [85, 99, 84, 97, 92]
englishScore = [59, 80, 84, 68, 77]
a = tf.placeholder(dtype=tf.float32)
b = tf.placeholder(dtype=tf.float32)
y = (a+b)/2
sess = tf.Session()
sess.run(y, feed_dict={a:mathScore, b:englishScore})

결과
array([72. , 89.5, 84. , 82.5, 84.5], dtype=float32)
~~~

### 텐서플로우(TensorFlow) 주요 함수

| 함수 | 설명 |
|:--------|:--------|
| tf.add | 덧셈을 수행 |
| tf.subtract | 뺄셈을 수행 |
| tf.multiply |  곱셈을 수행 |
| tf.truediv | 나눗셈의 몫을 구함 |
| tf.mod | 나눗셈의 나머지를 구함 |
| tf.abs |  절대값을 구함 |
| tf.negative | 음수를 반환 |
| tf.sign | 부호를 반환(음수:-1 양수:1 0:0)|
| tf.srquare | 제곱을 수행 |
| tf.sqrt | 제곱근을 반환 |
| tf.pow | 거듭제곱을 수행 |
| tf.maximum | 더 큰 값을 반환 |
| tf.minimum | 더 작은 값을 반환 |
| tf.exp | 지수 값을 계산 |
| tf.log | 로그 값을 계산 |

- Sorcecode

~~~
import tensorflow as tf
a = tf.constant(3)
b = tf.constant(5)
sess = tf.Session()
# 덧셈
c = tf.add(a,b)
sess.run(c)

# 뺄셈
c = tf.subtract(a,b)
sess.run(c)

# 곱셈
c = tf.multiply(a, b)
sess.run(c)

# 나눗셈 몫
c = tf.truediv(a, b)
sess.run(c)

# 나머지
c = tf.mod(b, a)
sess.run(c)

# 절대값
c = tf.abs(-a)
sess.run(c)

a = tf.constant(17.5)
b = tf.constant(5.0)

# 음수 반환
c = tf.negative(a)
sess.run(c)

# 부호 반환
c = tf.sign(a)
sess.run(-c)

# 제곱 함수
c = tf.square(a)
sess.run(c)

# 거듭 제곱, 너무 큰 값은 못구한다고 뜸
c = tf.pow(b, 2)
sess.run(c)

# 더 큰 값 확인
c = tf.maximum(a, b)
sess.run(c)

# 더 작은 값
c = tf.minimum(a, b)
sess.run(c)

# 지수 값
c = tf.exp(b)
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
                            

					