---
description: https://ko.javascript.info/function-expressions
---

# 함수 표현식

### <mark style="color:blue;">함수 표현식</mark>&#x20;

```
let sayHi = function() {
  alert( "Hello" );
};
```

* 위 예시 풀이: <mark style="color:orange;">**함수를 만들고 그 함수를 변수**</mark><mark style="color:orange;">** **</mark><mark style="color:orange;">**`sayHi`**</mark><mark style="color:orange;">**에 할당하기**</mark>

<mark style="color:orange;">****</mark>

### [콜백 함수](https://ko.javascript.info/function-expressions#ref-346)

* 함수를 함수의 인수로 전달하고, 필요하다면 인수로 전달한 함수를 "나중에 호출(called back)"하는 것

```
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

function showOk() {
  alert( "동의하셨습니다." );
}

function showCancel() {
  alert( "취소 버튼을 누르셨습니다." );
}

// 사용법: 함수 showOk와 showCancel가 ask 함수의 인수로 전달됨
ask("동의하십니까?", showOk, showCancel);
```

* 함수 `ask`의 인수, `showOk`와 `showCancel`은 _**콜백 함수**_** ** 또는 _**콜백**_이라고 불림
* 사용자가 "yes"라고 대답한 경우 `showOk`가 콜백이 되고,
* 사용자가 "no"라고 대답한 경우 `showCancel`가 콜백됨



### [함수 표현식 vs 함수 선언문](https://ko.javascript.info/function-expressions#ref-347)

#### <mark style="color:purple;">함수 선언문</mark>&#x20;

1. 함수는 주요 코드 흐름 중간에 독자적인 구문 형태로 존재
2. 함수 선언문이 정의되기 전에도 호출할 수 있



#### <mark style="color:purple;">함수 표현식</mark>

1. 함수는 표현식이나 구문 구성(syntax construct) 내부에 생성
2. 실제 실행 흐름이 해당 함수에 도달했을 때 함수를 생성

```
// 1. 함수 선언문
function sum(a, b) {
  return a + b;
}

// 1. 함수 표현식
let sum = function(a, b) {
  return a + b;
};
```

```
// 2. 함수 선언문
sayHi("John"); // Hello, John

function sayHi(name) {
  alert( `Hello, ${name}` );
}

// 2. 함수 표현식
sayHi("John"); // error!

let sayHi = function(name) {
  alert( `Hello, ${name}` );
};
```

<mark style="color:purple;"></mark>
