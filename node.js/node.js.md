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
