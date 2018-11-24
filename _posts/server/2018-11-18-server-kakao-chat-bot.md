### Node.js란?
- V8 Engine 사용(구글에서 개발)
- 이벤트가 발생했을 때 동작하는 방식(자원 소모x)
- non-blocking
- 싱글 스레드

### 설치
- https://nodejs.org/ko/
- 명령 프롬프트 창을 열고 node -v 명령어를 친다. 버전이 잘 나온다면 성공

### nodejs 초기화
- 새로운 폴더를 만들고 명령 프롬프트로 새로운 폴더로 이동
- npm init 명령어
- 이름, 설명, 버전 등의 정보를 작성한다 ( 전부 작성했다면 폴더에 package.json 파일이 생성되어 있다 )
- 폴더 안에 app.js 파일을 생성하고 console.log('hello world'); 라고 작성한다
- 명령프롬프트 창에서 node app.js 를 치면 hello world가 나오는지 확인한다


### 카카오 플러스친구 관리자 가입
- https://business.kakao.com/ 접속
- 상단메뉴에서 카카오 플러스친구 를 선택해서 관리자 가입을 합니다
- 새 플러스 친구를 선택해서 플러스 친구를 만듭니다
- 관리자센터-관리-상세설정에서 공개설정을 합니다
- 관리자센터-스마트채팅- 채팅유형을 선택합니다. API형 선택
- Method : GET
- URL : http(s)://your_server_url/keyboard
- Content-Type : application/json; charset=utf-8
- API Document 확인 API SPEC 메뉴를 클릭해서 API 사용 예시를 확인한다

~~~
{
  "type" : "buttons",
  "buttons" : ["선택 1", "선택 2", "선택 3"]
}

curl -XPOST 'https://:your_server_url/message' -d '{
  "user_key": "encryptedUserKey",
  "type": "text",
  "content": "차량번호등록"
}
~~~

### nodejs api 작업
- 명령프롬프트 창에 npm install express --save 명령어를 친다. express 프레임워크를 설치한다
- 서버 소스를 작성한다. 그리고 서버를 띄운다(명령어 node app.js)
- localhost:포트번호/keyboard 으로 접속한다
- 결과가 뜨는것을 확인할 수 있다 

### 공인 ip 설정
- 포트포워딩 글을 참고한다( https://parkwonhui.github.io/server/2018/11/18/server-port-forwarding.html )

### 패킷 전달을 위한 모듈설치
- npm install body-arser --save

### 패킷 전달 코드 추가
- 아래 소스코드를 작성하고 http://외부 ip:포트번호/keyboard 로 접속되는지 확인한다
- 접속 완료 시 API형-앱 url에 http://외부 ip:포트번호를 적는다 (keyboard는 안적어도 된다)
- 응답이 잘 되면 성공한 것이고, 응답이 안되면 포트포워딩이나, url을 다시 확인한다

### 생각할 점
- 내 컴퓨터에선 80번 포트밖에 되지 않았다.
- port open 체크 사이트에서도 open 된 상황이었음( https://www.yougetsignal.com/tools/open-ports/ )

### 소스코드

~~~
var express = require('express');
var http = require('http');
var bodyParser = require('body-parser');

var app = express();

app.use(bodyParser.urlencoded({extended: false}));
app.use(bodyParser.json());


app.get('/keyboard', function(req, res){
  console.log('get');
var data = {
    'type' : 'buttons',
    'buttons' : ['월','화','수','목','금']
  };

  res.json(data);
});

http.createServer(app).listen(80, function(){
  console.log('server start');
});

app.post('/message', function(req, res){
    var msg = req.body.content;
    console.log('전달받은 메시지:'+msg);
    
    var send = {};        // 응답할 데이터
    switch(msg){
        case '월':
        send = {
        'message':{
            'text': '햅쌀밥\n대파육계장\n파파야함박스테이크\n닭볶음탕\n철판두부구이\n메츄리알어묵볶음\n쟁반막국수'
        }
        }
        break;
        case '화':
                send = {
        'message':{
            'text':'햅쌀밥,참치김치찌개\n돼지고기주물럭\n생선까스/소스\n옛날짜장면\n비엔나피망볶음\n쪽파무생채'
        }    
        }    
        break;
        case '수':
                    send = {
        'message':{
            'text':'햄쌀밥\n스끼야끼\n수제닭강정\n파기름오징어두루치기\n한식잡채\n에그샌드위치\n숙주미나리나물\n포기김치'
        }    
        }    
    
        break;
        case '목':
                            send = {
        'message':{
            'text':'햄쌀밥\n팽이된장찌개\n등심돈까스\n매콤등뼈찜\n고구마카레\n군만두\n시금치무침'
        }    
        }    

        break;
        case '금':
                            send = {
        'message':{
            'text':'김치볶음밥\n모듬어묵탕\n수제케이준치킨\n제육간장불고기\n미트볼케첩조림\n조미구이김\n열무나물'
        }    
        }    

        break;
        
        default:
                            send = {
        'message':{
            'text':'알 수 없는 명령'
        }    
        }    

        break;
    }
    res.json(send);
});
~~~