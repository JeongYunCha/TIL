# node 웹 서버 만들기

[TOC]

### 1. http모듈로 간단한 웹서버 만들기



### 2. Express 웹 프레임워크 사용하기

```js
// server.js
var express = require('express');

// 웹 서버 생성
var app = express();

// 미들웨어 사용
app.use(function(request, response, next){ next(); });
app.use(function(request, response, next){ response.send('안녕하세요!'); });

// 라우터 미들웨어로 요청 응답
app.all('/a', function (request, response){ response.send('a 입니다.'); });
app.all('/b', function (request, response){ response.send('b 입니다.'); });
app.all('/c', function (request, response){ response.send('c 입니다.'); });

// 웹 서버 실행
app.listen(54321, function() {
	console.log('Server Running at http://127.0.0.1:54321');
});
```



####  2.1. 라우터와 미들웨어

- 라우팅하다<br>사용자의 요청에 따라 사용자가 필요한 정보를 제공. 클라이언트의 요청패스에 따라 각각을 담당하는 함수로 분리시키는 것
- 미들웨어 함수<br>- 요청/응답 오브젝트(req/res),  요청-응답 주기 중 그 다음의 미들웨어 함수 대한 액세스 권한을 갖는 함수<br>- `next()`를 호출하여 그 다음 미들웨어 함수에 제어를 전달 



#### 2.1.1. static 미들웨어

```js
var options = {
  dotfiles: 'ignore',
  etag: false,
  extensions: ['htm', 'html'],
  index: false,
  maxAge: '1d',
  redirect: false,
  setHeaders: function (res, path, stat) {
    res.set('x-timestamp', Date.now());
  }
}
app.use(express.static('public', options));
app.use(express.static('uploads'));
app.use(express.static('files'));
```



#### 2.1.2. 어플리케이션 레벨 미들웨어 

- `app.use()`  및  `app.METHOD()` 함수 사용



- 오류 처리 미들웨어

```js
app.use(function(err, req, res, next){
  console.error(err.stack);
  res.status(500).send('Sonething broke!')
});
```



#### 2.1.3. 라우터 레벨 미들웨어 

사용자의 요청마다 url확인, 미들웨어 함수를 호출하지않고 사용자의 요청 기능이 무엇인지 패스를 기준으로 구별한다.

```js
// 라우터 객체 참조
var router = express.Router();

// 라우팅 함수 등록 
router.route('/path/...').get(callback);	
router.route('/path/...').post(callback);
router.route('/path/...').put(callback);
router.route('/path/...').delete(callback);
router.route('/path/...').all(callback);

// 라우터 객체를 app 객체에 등록
app.use('/', router);
```

```js
// 등록되지 않은 패스에 대해 페이지 오류 응답
app.all('*', function(req,res) {
  res.status(404).send('<h1>404 error! 페이지가 없습니다.</h1>')
})
```



#### 2.1.4. 써드파티 미들웨어 [(목록보기)](http://expressjs.com/ko/resources/middleware.html) 

- 써드파티 미들웨어는 외장모듈. 설치필요

```bash
$ npm install <모듈명> --save
```

- __body-parser__ : 클라이언트가 POST방식으로 요청할때 body 안의 요청파라미터 파싱

```js
var bodyParser = require('body-parser');
app.use(bodyParser) 
```

- __cookie-parser__ : 요청 객체에 쿠키 속성을 추가 (클라이언트에서 쿠키객체를 그대로 전달받는다.)
- ​

```js
var cookieParser = require('cookie-parser');
app.use(express.cookieParser());

var router = express.Router();

// 요청 패스 처리하는 콜백 함수 등록.
router.route('/path/showCookie').get(function(req, res){
  res.send(req.cookies);
  
  // 쿠키 설정
  res.cookie('user', {
    id:'mike',
    name: '마이크',
    authorized: true
  });
  
  // redirect로 응답
  res.redirect('/path/showCookie');
});

app.use('/', router);
```

- __express-error-handler__ : 오류 핸들러 모듈

```js
var expressErrorHandler = require('express-error-handler');

// 모든 router 처리 끝난 후 404 오류 페이지 처리
var errorHandler = expressErrorHandler({
  static: {
    '404': './public/404.html'
  }
})

app.use( expressErrorHandler.httpError(404) );
app.use( errorHandler );
```



#### 2.3. 요청 객체와 응답 객체

- http모듈에서 사용하는 객체와 같고 그외 익스프레스에서 사용할수있는 추가적인 객체

```js
send([body])
status(code)
sendStatus(statusCode)
redirect([status,] pathe)
render(view[,locals][,callback])
```

- 익스프레스 요청객체 -헤더, 파라미터

```js
query
body
header(name)
```

- 토큰과 함께 요청한 정보 처리하기 

```js
var router = express.Router();

router.route('/path/:id').get( function(req, res){
  
  // 요청 URL 파라미터의 :토큰 확인
  var paramId = req.params.id;
  
  res.writeHead('200', {'Context-Type':'text/html;charset=utf8'});
  res.write('<h1>title</h1>');
  res.end();
});

app.use('/', router);
```



