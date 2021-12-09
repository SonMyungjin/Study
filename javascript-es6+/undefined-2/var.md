---
description: https://ko.javascript.info/var
---

# 오래된 'var'(호이스팅)

### ['var’는 블록 스코프가 없습니다.](https://ko.javascript.info/var#ref-2046)

* `var`로 선언한 변수의 스코프는 **함수 스코프**이거나 **전역 스코프**
* 블록 기준으로 스코프가 생기지 않기 때문에 <mark style="color:orange;">**블록 밖에서 접근 가능**</mark>



```
if (true) {
  var test = true; // 'let' 대신 'var'를 사용 
}

alert(test); // true(if 문이 끝났어도 변수에 여전히 접근할 수 있음)
```

* `var`는 코드 블록을 무시하기 때문에 `test`는 전역 변수가  -> 전역 스코프에서 이 변수에 접근 가능 &#x20;
* `var test`가 아닌 `let test`를 사용했다면, 변수 `test`는 `if`문 안에서만 접근할 수 있음



* 코드 블록이 함수 안에 있다면, `var`는 함수 레벨 변수가 됨&#x20;

```
function sayHi() {
  if (true) {
    var phrase = "Hello";
  }

  alert(phrase); // 제대로 출력
}

sayHi();
alert(phrase); // Error: phrase is not defined
```

&#x20;

### [선언하기 전 사용할 수 있는 ‘var’](https://ko.javascript.info/var#ref-2048)

* `var` 선언은 함수가 시작될 때 처리
* 함수 본문 내에서 `var`로 선언한 변수는 선언 위치와 상관없이 함수 본문이 시작되는 지점에서 정의됨 &#x20;
  * 단, 변수가 중첩 함수 내에서 정의되지 않아야 이 규칙이 적용



* 두 예제는 동일하게 동작  &#x20;

```
// 예제 1
function sayHi() {
  phrase = "Hello";

  alert(phrase);

  var phrase;
}
sayHi();

// 예제 2 
function sayHi() {
  var phrase;

  phrase = "Hello";

  alert(phrase);
}
sayHi();
```



* 이렇게 변수가 끌어올려 지는 현상을 <mark style="color:orange;">**'호이스팅(hoisting)'**</mark>이라고 부름&#x20;
  * `var`로 선언한 모든 변수는 함수의 최상위로 ‘끌어 올려지기(hoisted)’ 때문
  * **선언은 호이스팅 되지만 **<mark style="color:red;">**할당은 호이스팅 되지 않음**</mark> &#x20;

```
function sayHi() {
  alert(phrase);

  var phrase = "Hello";
}

sayHi();
```

* `var phrase = "Hello"`행에선 두 가지 일이 일어남 &#x20;
  1. 변수 선언(`var`)
  2. 변수에 값을 할당(`=`)
* 변수 선언은 함수 실행이 시작될 때 처리되지만(호이스팅),
* 할당은 호이스팅 되지 않기 때문에 할당 관련 코드에서 처리됨

```
function sayHi() {
  var phrase; // 선언은 함수 시작 시 처리 

  alert(phrase); // undefined

  phrase = "Hello"; // 할당은 실행 흐름이 해당 코드에 도달했을 때 처리 
}

sayHi();
```

* &#x20;모든 `var` 선언은 함수 시작 시 처리되기 때문에, `var`로 선언한 변수는 어디서든 참조 가능 &#x20;
  * 하지만 변수에 무언가를 할당하기 전까지 값은 undefined
