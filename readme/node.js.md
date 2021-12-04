---
description: https://www.inflearn.com/course/nodejs-강좌-생활코딩
---

# Node.js 를 이용해 웹애플리케이션 만들기

### 간단한 웹 앱 만들기

#### 실행

* 웹 브라우저를 통해서 요청한 내용을 받아 "`Hello World`"를 전송

```jsx
// 웹 서버를 만드는 역할
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World');
});

server.listen(port, hostname, () => {
  console.log(`Server running at <http://$>{hostname}:${port}/`);
});
```

#### 인터넷의 동작 방법

* 웹 브라우저를 통해서 들어온 접속을 80번 포트를 통해 listening
* HTTP를 통해 알 수 있기 때문에 :80 생략 가능

#### 정리

```jsx
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World');
});

server.listen(port, hostname, () => {
  console.log(`Server running at <http://$>{hostname}:${port}/`);
});
```

* `createServer()`를 통해 서버를 만듦
* `listen()`를 통해 port, hostname에 해당하는 서버 응답

### **섹션: 모듈**

#### 기초

* `모듈` : 부품이라고 생각
* `require('http')` : 'http' 라고 하는 모듈(부품)을 요구
* `const` : constant 약자 → 상수 → 한번 할당되면 항상 그 값을 가짐
* `createServer()` : http.Server를 리턴 → http.Server안에 server.listen()을 가짐

#### NPM 소개

* `NPM`
  * Node Package Manager의 약자
  * Node계의 앱스토어
  * 모듈을 설치, 삭제, 업그레이드, 의존성 관리

[https://www.npmjs.com/](https://www.npmjs.com)

#### NPM 독립적인 앱 설치

* `npm install uglify-js -g`
  * uglify-js 라는 NPM 설치
* `uglify`
  * 컴퓨터는 공백도 모두 데이터로 인식
  * `uglify`를 사용하면 필수적인 코드 빼고는 공백이 제거됨
* `uglifyjs 파일명 -m`
  * 이름을 바꿔도 되는 변수를 한 글자로 가장 짧은 이름으로 변경
* `uglifyjs 파일명 -o 파일명.min.js -m`
  * `-o`를 통해 새로운 파일을 만들고
  * 관습적으로 uglify된 파일은 `파일명.min.js` 명칭을 사용

#### NPM으로 모듈 설치

* npm 상에서 현재 디렉토리를 패키지로 지정하는 명령어 사용
  * `npm init`
  * `package.json`이라는 파일이 생성됨
* `npm i underscore`
  * underscore 모듈 설치
* `npm i underscore --save`
  * `package.json` 내에 dependencies라는 의존성이 생성 → 버전 확인 가능
  * 일시적인 프로젝트일 경우에는 --save 사용 x

#### 모듈 사용법

* `underscore`
  * underscore의 변수명은 '\_' 을 관례적으로 사용
  * `_.first()` : 배열 첫번째 인자값 가져옴
  * `_.last()` : 배열 마지막 인자값 가져옴

```jsx
const _ = require('underscore');
var arr = [3,6,9,1,12];
console.log(arr[0]);
console.log(_.first(arr));
console.log(arr[arr.length-1]);
console.log(_.last(arr));
```

### **섹션: 콜백(Callback)**

#### 콜백(Callback)

* cmd에서 `node`만 치면 javascript 코드를 직접 입력



### **동기와 비동기**

#### 개요

* 동기(Synchronous)
  * 설계가 단순하고 직관적
  * 결과가 주어질 때까지 아무것도 하지 못하고 대기
* 비동기(Asynchronous)
  * 동기보다는 복잡
  * 결과가 주어지는데 시간이 걸리더라도 그 시간동안 다른 작업을 할 수 있어
  * 자원을 효율적 사용할 수 있음

#### 활용

```jsx
var fs = require('fs');

//Sync
console.log(1);
var data = fs.readFileSync('data.txt', {encoding:'utf8'});
console.log(data);

//Async
console.log(2);
var data = fs.readFile('data.txt', {encoding:'utf8'}, function(err, data){
    console.log(3);
    console.log(data);
		});

console.log(4);
```

### **Express**

#### Express 설치

[https://expressjs.com/](https://expressjs.com)

#### Express를 이용한 간단한 웹 앱 만들기

```jsx
var express = require('express');
var app = express();

app.get('/', function(req, res) {
    res.send('Hello home page');
});

app.get('/login', function(req, res) {
    res.send('login please');
});

app.listen(3000, function() {
    console.log('Connected 3000 port!');
});
```

* `Router`
  * 사용자의 요청과 요청에 대한 처리를 하는 Controller를 중계하는 역할

#### Express, 정적 파일을 서비스 하는 법

```jsx
var express = require('express');
var app = express();

//정적 파일 서비스 하기 위한 명령어
app.use(express.static('public'));

app.get('/static.txt', function(req, res) {
    res.send('Hello home page');
});

app.listen(3000, function() {
    console.log('Connected 3000 port!');
});
```

* public이라는 디렉토리에 정적인 파일을 넣으면 정적 파일 서비스 가능

#### Express, 웹페이지를 표현하는 법

* 정적 파일
  * 서버를 다시 안켜도 됨
* 동적 파일
  * 서버를 다시 켜야됨

### **Express 템플릿 엔진**

#### Express, 템플릿 엔진

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/98c49bd2-522b-45d5-9c60-ae89bdeae048/Untitled.png)

* html 태그를 요약적으로 사용할 수 있음

#### Express, 템플릿 엔진 사용법

* 설치
  * `npm i jade --save`
* 설정
  * `views` 폴더 생성 후 `temp.jade` 파일 생성
* `app.js`

```jsx
var express = require('express');
var app = express();

//템플릿 엔진
app.set('view engine', 'jade');
app.set('views', './views');

//라우터
app.get('/template', function(req, res) {
    res.render('temp');
});
```

#### Express, 템플릿 엔진, Jade 문법

* `app.js`

```jsx
var express = require('express');
var app = express();

//코드를 uglify하지 않고 pretty하게
app.locals.pretty = true;

//템플릿 엔진
app.set('view engine', 'jade');
app.set('views', './views');

//라우터
app.get('/template', function(req, res) {
    res.render('temp', {time:Date(), _title:'Jade'});
});
```

* `temp.jade`

```jsx
html
    head 
    title= _title
    body 
        h1 Hello Jade
        ul
         -for(var i=0; i<5; i++)
            li coding 
        div= time
```

* \= 뒤는 변수명 → `app.js` 의 res.render( ) 안에 명시 해줘야 함





### **Express, URL을 이용한 정보의 전달**

#### 쿼리 스트링 소개

#### query 객체의 사용법

```jsx
//라우터
app.get('/topic', function (req, res) {
   res.send(req.query.id); //id 대신 name이라 쓰면 URL에 ?name= 으로
});
```

* function 부터는 express의 함수로 인해 사용 가능

#### query 객체의 이용

```jsx
//라우터
app.get('/topic', function (req, res) {
    var topics = [
        'JavaScript is...',
        'Nodejs is...',
        'Express is...'
    ];
    var output = `
    <a href="/topic?id=0">JavaScript</a><br>
    <a href="/topic?id=1">Nodejs</a><br>
    <a href="/topic?id=2">Express</a><br><br>
    ${topics[req.query.id]}
    `
    res.send(output);
});
```

#### 시멘틱 URL

* URL
  * 쿼리 스트링 : localhost:3000/topic?id=2
  * 시멘틱 URL : localhost:3000/topic/2

```jsx
//라우터
app.get('/topic/:id', function (req, res) {
    var topics = [
        'JavaScript is...',
        'Nodejs is...',
        'Express is...'
    ];
    var output = `
    <a href="/topic?id=0">JavaScript</a><br>
    <a href="/topic?id=1">Nodejs</a><br>
    <a href="/topic?id=2">Express</a><br><br>
    ${topics[req.params.id]}
    `
    res.send(output); 
});

app.get('/topic/:id/:mode', function(req, res) {
    res.send(req.params.id+','+req.params.mode)
})
```

### ****

### **Express, POST 방식을 이용한 정보의 전달**

#### POST 방식을 이용한 정보의 전달 1

* 사용자의 정보를 서버로 전송할 때는 GET 보다는 POST!

#### POST 방식을 이용한 정보의 전달 2 : form

* `form.jade`

```jsx
doctype html 
html 
    head 
        meta(charset='utf-8')
    body
     form(action="/form_receiver" method="post") 
        p 
            input(type="text" name="title")
        p
            textarea(name="description")
        p
            input(type="submit")
```

* `app.js`

```jsx
//라우터
app.get('/form', function(req,res) {
    res.render('form');
})

app.get('/form_receiver', function(req,res) {
    var title = req.query.title;
    var description = req.query.description;
    res.send(title+','+description);

```

#### POST 방식을 이용한 정보의 전달 3 : POST

```jsx
//모듈
var bodyParser = require('body-parser');

//정적 파일
app.use(bodyParser.urlencoded({extended: false}));

//라우터
app.post('/form_receiver', function(req,res) {
    var title = req.body.title;
    var description = req.body.description;
    res.send(title+','+description);
})
```

*   `req.body`

    * `body-parser`라는 모듈을 포함 시켜야 함 → 미들웨어
      * 사용자의 요청을 post 방식으로 사용할 수 있도록 해주는 모듈



#### POST 방식을 이용한 정보의 전달 4 : GET과 POST 용도

* GET
  * URL에 데이터가 포함되는 쿼리 스트링 방식
  * express가 기본적으로 제공
* POST
  * URL에 데이터가 포함되지 않고 용량이 큰 데이터 전송
  * express가 기본적으로 제공 X
    * 미들웨어인 body-parser 사용



### **node.js를 이용한 웹 앱 제작 실습**

* DB사용 x → 파일 사용

#### 라우팅

* `app_file.js`

```jsx
//모듈 가져오기
var express = require('express');
var app = express();

//코드를 uglify하지 않고 pretty하게
app.locals.pretty = true;

//템플릿 엔진
app.set('views', './views_file');
app.set('view engine', 'jade'); //jade 엔진 사용

//라우팅
app.get('/topic/new', function(req,res) {
    res.render('new');
})

app.post('/topic', function(req,res) {
    res.send('Hi, post');
})

//특정 포트 지정
app.listen(3000, function() {
    console.log('Connected, 3000 port!');
})
```

* `new.jade`

```jsx
doctype html 
html 
 head 
  meta(charset='utf-8')
 body 
  form(action='/topic' method='post')
   p
    input(type='text' name='title' placeholder='title')
   p 
    textarea(name='description') 
   p 
    input(type='submit')
```

#### 본문 저장

* `app_file.js`

```jsx
//모듈 가져오기
var express = require('express');
var bodyParser = require('body-parser');
var fs = require('fs');

var app = express();

app.use(bodyParser.urlencoded({ extended: false }))

//코드를 uglify하지 않고 pretty하게
app.locals.pretty = true;

//템플릿 엔진
app.set('views', './views_file');
app.set('view engine', 'jade'); //jade 엔진 사용

//라우팅
app.get('/topic/new', function(req,res) {
    res.render('new');
})

app.post('/topic', function(req,res) {
    var title = req.body.title;
    var description = req.body.description;

    // 좋은 방법은 아님
    fs.writeFile('data/'+title, description, function(err) {
        if(err){
            console.log(err);
            res.status(500).send('Internal Server Error');
        }
        res.send('Success!');
    });

})

//특정 포트 지정
app.listen(3000, function() {
    console.log('Connected, 3000 port!');
})
```

* 사용자에게 받은 정보(title, description)
  * data 폴더 안에 제목은 title, 본문 내용은 description인 파일을 생성

#### 글 목록 만들기

* `app_file.js`

```jsx
//모듈 가져오기
var express = require('express');
var bodyParser = require('body-parser');
var fs = require('fs');

var app = express();

app.use(bodyParser.urlencoded({ extended: false }));

//코드를 uglify하지 않고 pretty하게
app.locals.pretty = true;

//템플릿 엔진
app.set('views', './views_file');
app.set('view engine', 'jade'); //jade 엔진 사용

//라우팅
app.get('/topic/new', function(req,res) {
    res.render('new');
});

app.get('/topic', function(req,res) {
   fs.readdir('data', function(err, files) {
       if(err){
           console.log(err);
           res.status(500).send('Internal Server Error');
        }
        res.render('view', {topics: files});
   });
});

app.post('/topic', function(req,res) {
    var title = req.body.title;
    var description = req.body.description;

    // 좋은 방법은 아님
    fs.writeFile('data/'+title, description, function(err) {
        if(err){
            console.log(err);
            res.status(500).send('Internal Server Error');
        }
        res.send('Success!');
    });

})

//특정 포트 지정
app.listen(3000, function() {
    console.log('Connected, 3000 port!');
})
```

* `view.jade`

```jsx
doctype html 
html 
 head 
  meta(charset='utf-8')
 body 
  h1 Server Side JavaScript 
  ul 
   each topic in topics 
    li 
     a(href='/topic/'+topic)= topic
```

#### 본문 읽기

* app.get('/topic/:id') → : 은 바뀔 수 있는 정보를 의미함
* `app_file.js`

```jsx
//모듈 가져오기
var express = require('express');
var bodyParser = require('body-parser');
var fs = require('fs');

var app = express();

app.use(bodyParser.urlencoded({ extended: false }));

//코드를 uglify하지 않고 pretty하게
app.locals.pretty = true;

//템플릿 엔진
app.set('views', './views_file');
app.set('view engine', 'jade'); //jade 엔진 사용

//라우팅
app.get('/topic/new', function(req,res) {
    res.render('new');
});

app.get('/topic', function(req,res) {
   fs.readdir('data', function(err, files) {
       if(err){
           console.log(err);
           res.status(500).send('Internal Server Error');
        }
        res.render('view', {topics:files});
   });
});

app.get('/topic/:id', function(req, res) {
   var id = req.params.id;

   fs.readdir('data', function(err, files) {
    if(err){
        console.log(err);
        res.status(500).send('Internal Server Error');
     }
     fs.readFile('data/'+id, 'utf-8', function(err, data) {
        if(err){
            console.log(err);
            res.status(500).send('Internal Server Error');
        }
        res.render('view', {topics:files, title:id, description:data});
       });
    });   
});

app.post('/topic', function(req,res) {
    var title = req.body.title;
    var description = req.body.description;

    // 좋은 방법은 아님
    fs.writeFile('data/'+title, description, function(err) {
        if(err){
            console.log(err);
            res.status(500).send('Internal Server Error');
        }
        res.send('Success!');
    });

})

//특정 포트 지정
app.listen(3000, function() {
    console.log('Connected, 3000 port!');
})
```

* `view.jade`

```jsx
doctype html 
html 
 head 
  meta(charset='utf-8')
 body 
  h1 Server Side JavaScript 
  ul 
   each topic in topics 
    li 
     a(href='/topic/'+topic)= topic
  article 
   h2= title 
   = description
```

#### 코드의 개선

* 코드의 개선을 위해서는 중복 제거 필요!

```jsx
//라우팅
app.get(['/topic', '/topic/:id'], function(req,res) {
   fs.readdir('data', function(err, files) {
       if(err){
           console.log(err);
           res.status(500).send('Internal Server Error');
        }
        var id = req.params.id;
        if(id){
        // id값이 있을 때
        fs.readFile('data/'+id, 'utf-8', function(err, data) {
            if(err){
                console.log(err);
                res.status(500).send('Internal Server Error');
            }
            res.render('view', {topics:files, title:id, description:data});
           });
        }else{
        // id값이 있을 때
        res.render('view', {topics:files, title:'Welcome', description:'Hello, JavaScript for server'});
        }
   });
});
```

### **TIP**

#### Supervisor

* 변경이 생기면 노드를 자동으로 껐다 키는 모듈
* **npm i  supervisor -g**

