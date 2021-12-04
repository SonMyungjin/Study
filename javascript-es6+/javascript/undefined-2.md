---
description: https://ko.javascript.info/function-basics
---

# 함수

* 스크립트를 작성하다 보면 <mark style="color:orange;">**유사한 동작을 하는 코드**</mark>가 여러 곳에서 필요할 때가 많음
* 함수는 프로그램을 구성하는 주요 '구성 요소(building block)'로
  * 함수를 이용하면 중복 없이 유사한 동작을 하는 코드를 여러 번 호출할 수 있음

### [함수 선언](https://ko.javascript.info/function-basics#ref-1148)

```
function name(parameters) {
  ...함수 본문...
}

// ex)
function showMessage() {
  alert( '안녕하세요!' );
}

showMessage();
```



### [지역 변수](https://ko.javascript.info/function-basics#ref-1149)

* 함수 내에서 선언한 변수인 지역 변수(local variable)는 함수 안에서만 접근할 수 있음

```
function showMessage() {
  let message = "안녕하세요!"; // 지역 변수

  alert( message );
}

showMessage(); // 안녕하세요!

alert( message ); // ReferenceError: message is not defined (message는 함수 내 지역 변수이기 때문에 에러 발생)
```



### <mark style="color:blue;"></mark>[<mark style="color:blue;">외부 변수</mark>](https://ko.javascript.info/function-basics#ref-1150)<mark style="color:blue;">(전역 변수)</mark>

* 함수 내부에서 함수 외부의 변수인 외부 변수(outer variable)에 접근할 수 있음

```
let userName = 'John';

function showMessage() {
  let userName = "Bob"; // 같은 이름을 가진 지역 변수를 선언

  let message = 'Hello, ' + userName; // Bob
  alert(message);
}

// 함수는 내부 변수인 userName만 사용
showMessage();

alert( userName ); // 함수는 외부 변수에 접근 X
                   // 따라서 값이 변경되지 않고, John이 출력
```



### [매개변수](https://ko.javascript.info/function-basics#ref-1151)

* 매개변수(parameter)를 이용하면 임의의 데이터를 함수 안에 전달할 수 있음
* 매개변수는 _인수(argument)_ 라고 불리기도 함

```
function showMessage(from, text) { // 인수: from, text
  alert(from + ': ' + text);
}

showMessage('Ann', 'Hello!'); // Ann: Hello! (*)
showMessage('Ann', "What's up?"); // Ann: What's up? (**)
```



### [기본값](https://ko.javascript.info/function-basics#ref-1152)

* 매개변수에 값을 전달하지 않으면 그 값은 `undefined`가 됨
* 위에서 정의한 함수 `showMessage(from, text)`는 매개변수가 2개지만,&#x20;
  * 아래와 같이 인수를 하나만 넣어서 호출할 수 있음

```
showMessage("Ann"); // Ann: undefined

// 기본값(default value) 설정
function showMessage(from, text = "no text given") {
  alert( from + ": " + text );
}

showMessage("Ann"); // Ann: no text given
```



#### [매개변수 기본값을 설정할 수 있는 또 다른 방법](https://ko.javascript.info/function-basics#ref-1153)

```
function showMessage(text) {
  if (text === undefined) {
    text = '빈 문자열';
  }

  alert(text);
}

showMessage(); // 빈 문자열
```

``

* `if`문을 쓰는 것 대신 논리 연산자 `||`를 사용할 수도 있음

```
// 매개변수가 생략되었거나 빈 문자열("")이 넘어오면 변수에 '빈 문자열'이 할당
function showMessage(text) {
  text = text || '빈 문자열';
  ...
}
```



* null 병합연산자(`??`)를 사용하면 `0`처럼 falsy로 평가되는 값들을 일반 값처럼 처리

```
// 매개변수 'count'가 넘어오지 않으면 'unknown'을 출력해주는 함수
function showCount(count) {
  alert(count ?? "unknown");
}

showCount(0); // 0
showCount(null); // unknown
showCount(); // unknown
```



### [반환 값](https://ko.javascript.info/function-basics#ref-1154)

* 함수를 호출했을 때 함수를 호출한 그곳에 특정 값을 반환하게 할 수 있음
* 이때 이 특정 값을 반환 값(return value)이라 함

```
function sum(a, b) {
  return a + b;
}

let result = sum(1, 2);
alert( result ); // 3
```

{% hint style="info" %}
`return`문이 없거나 `return` 지시자만 있는 함수는 `undefined`를 반환
{% endhint %}

&#x20;&#x20;
