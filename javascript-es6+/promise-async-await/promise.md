---
description: https://ko.javascript.info/promise-basics
---

# promise

```
// 기본 문법
let promise = new Promise(function(resolve, reject) {
  // executor
});
```

* `new Promise`에 전달되는 함수는 _executor(실행자, 실행 함수)_ 라고 부름
* executor는 `new Promise`가 만들어질 때 자동으로 실행되는데,&#x20;
* 결과를 최종적으로 만들어내는 제작 코드를 포함
* executor의 인수 `resolve`와 `reject`는 자바스크립트에서 자체 제공하는 콜백
  * `resolve(value)` — 일이 성공적으로 끝난 경우 그 결과를 나타내는 `value`와 함께 호출
  * `reject(error)` — 에러 발생 시 에러 객체를 나타내는 `error`와 함께 호출

