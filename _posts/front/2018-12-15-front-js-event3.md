### 이벤트 추가
- on
- 이벤트를 연결
- 아래 이벤트는 해당 태그를 클릭 시 내용에 플러스 문자가 붙는다

~~~
    $('h1').on('click', function(){
      $(this).html(function(index, html){
        return html + '+';
      });
    });
~~~


- hover
- mouseenter는 태그 위에 마우스가 놓여져있을 때 발생
- mouseleave는 태그 위에 마우스가 놓였다가 다른곳으로 가면 발생
- mouseenter 이벤트와 mouseleave 이벤트를 동시에 연결합니다

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
.reverse{
  background: black;
  color:white;
}
</style>
<script src="http://code.jquery.com/jquery-3.1.1.js"></script>
<script type="text/javascript">

  $(function(){
    $('h1').hover(function(){
      $(this).addClass('reverse');

    }, function(){
      $(this).removeClass('reverse');
    });
  });

</script>
</head>
<body>
  <h1>1</h1>
  <h1>2</h1>
  <h1>3</h1>
</body>
</html>
~~~

### 이벤트 연결 제거
- off
- 이벤트 제거
- one()
- 이벤트를 한번만 실행

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
.reverse{
  background: black;
  color:white;
}
</style>
<script src="http://code.jquery.com/jquery-3.1.1.js"></script>
<script type="text/javascript">

  $(function(){


    $('h1').click(function(){
      $(this).html('CLICK');
      alert('이벤트가 발생');

      //이벤트 제거
      $(this).off();
    });
    $('h1').off();
  });

</script>
</head>
<body>
  <h1>1</h1>
  <h1>2</h1>
  <h1>3</h1>
</body>
</html>
~~~

### 매개변수 context
- 매개변수로 selector 외에 context도 사용할 수 있음
- 해당 선택한 태그의 자식을 선택하고 싶을 때 사용
-  (자식태그명, 선택엘레먼트)로 사용

~~~
      var header = $('h1', this).text();
      var paragraph = $('p', this).text();
~~~

### 이벤트 강제 발생
- trigger()
- 이벤트를 강제로 발생시킵니다
- 아래 예제는 h1 태그의 첫번째 엘레먼트의 click이벤트가 발생하면 1초마다 골뱅이가 붙는 예제

~~~

  $(function(){
    $('h1').click(function(){
      $(this).html(function(index, html){
        return '@'+html;
      });

      // 1초마다 함수실행
      setInterval(function(){
        $('h1').first().trigger('click');
      }, 1000);
    });
  });
~~~

- preventDefault
- 기본 이벤트를 제거한다
- stopPropagation
- 이벤트 전달 막기
- <h1>안에 <a> 태그가 있어서  a 태그 실행 시 이벤트 버블링이 일어난다
- 이벤트 버블링을 끄려면 함수가 끝나기 전에 stopPropagation()을 호출하면 된다
- stopPropagation() 함수 호출 대신 return false를 해도 이벤트 전달이 일어나지 않는다

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
  *{
    margin: 5px;
    padding: 5px;
    border: 3px solid black;
  }
</style>
<script src="http://code.jquery.com/jquery-3.1.1.js"></script>
<script type="text/javascript">

  $(function(){
    $('a').click(function(){
      $(this).css('background-color','blue');
      event.preventDefault();
      event.stopPropagation();
    });

    $('h1').click(function(){
      $(this).css('background-color', 'red');
    });
  });

</script>
</head>
<body>
  <h1>
    <a href = "html://hanbit.co.kr">Hanbit</a>
  </h1>
</body>
</html>
~~~

### 이벤트 연결 범위 한정
- on() 메서드는 이벤트 범위를 한정할 수 있다(delegate)
- 아래 예제를 실행하면 Header를 누를 때마다 h1 태그가 늘어난다
- 하지만 새로생긴 h1 태그는 클릭해도 이벤트가 작동하지 않는다

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>

</style>
<script src="http://code.jquery.com/jquery-3.1.1.js"></script>
<script type="text/javascript">

  $(function(){
    $('h1').on('click', function(){
      var length = $('h1').length;
      var targetHTML = $(this).html();
      $('#wrap').append('<h1>'+length+'-'+targetHTML+'</h1>');
    });
  });

</script>
</head>
<body>
  <div id='wrap'>
    <h1>Header</h1>
  </div>
</body>
</html>
~~~

- 상위태그에 이벤트를 연결하고, h1 태그를 연결했을 때를 찾아야 한다
- 함수안에서 this는 h1을 의미(wrap x)
- 수정후
~~~
  $(function(){
    $('#wrap').on('click','h1', function(){
      var length = $('h1').length;
      var targetHTML = $(this).html();
      $('#wrap').append('<h1>'+length+'-'+targetHTML+'</h1>');
    });
  });
~~~

### 마우스 이벤트
- mouseover
- 마우스가 해당 태그 안에 있고 움직일 때 마다 발생
- mouseenter
- 마우스가 해당 태그 밖에서 안으로 들어올 때만 발생

method | 설명
-------|-------
click | 마우스를 클릭할 때 발생
dbclick | 더블클릭 할 때 발생
mousedown |  마우스 버튼을 누를 때 발생
mouseup | 마우스 버튼을 땔 때 발생
mouseenter | 마우스가 요소의 경계 외부에서 내부로 이동할 때 발생
mouseleave | 마우스가 요소의 경계 내부에서 외부로 이동할 때 발생
mousemove | 마우스를 움직일 때 발생
mouseout | 마우스가 요소를 벗어날 때 발생
mouseover | 마우스를 요소 안에 들어올 때 발생

### 윈도우 이벤트
- 무한 스크롤 예제
- scrollTop : 스크롤의 위치
- (window).height() : 현재 웹브라우저의 보이는 길이 위치
- (document).height : 현재 웹프라우저의 문서길이(스크롤해야 보이는 위치까지 계산)
- 스크롤위치와 현재 웹브라우저가 보이는 위치길이를 더해서 문서길이와 같다면 Infinity Scoll 단어를 계속 body에 추가한다(화면을 끝까지 내리면서 무한스크롤이 된다)

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
</style>
<script src="http://code.jquery.com/jquery-3.1.1.js"></script>
<script type="text/javascript">

  $(window).scroll(function(){
    var scrollHeight = $(window).scrollTop() + $(window).height();
    var documentHeight = $(document).height();
    if(scrollHeight == documentHeight){
      for(var i = 0; i < 10; ++i){
        $('<h1>Infinity Scroll</h>').appendTo('body');
      }
    }

  });

  $(function(){
      for(var i = 0; i <20 ;++i)
      $('<h1>Infinity Scroll</h1>').appendTo('body');
  });

</script>
</head>
<body>
</body>
</html>

~~~