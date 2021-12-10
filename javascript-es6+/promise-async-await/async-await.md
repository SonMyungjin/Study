---
description: https://ko.javascript.info/async-await
---

# async와 await

### [async 함수](https://ko.javascript.info/async-await#ref-1411)

* `async`는 function 앞에 위치

```
async function f() {
  return 1;
}
```

* function 앞에 `async`를 붙이면 해당 함수는 항상 프라미스를 반환
* 프라미스가 아닌 값을 반환하더라도 이행 상태의 프라미스(resolved promise)로 값을 감싸 이행된 프라미스가 반환되도록 함



### [await](https://ko.javascript.info/async-await#ref-1412)

```
// await는 async 함수 안에서만 동작 
let value = await promise;
```

* 자바스크립트는 `await` 키워드를 만나면 프라미스가 처리(settled)될 때까지 기다림
  * 결과는 그 이후 반환



```
async function f() {

  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("완료!"), 1000)
  });

  let result = await promise; // 프라미스가 이행될 때까지 기다림 (*)

  alert(result); // "완료!"
}

f();
```

* 함수를 호출하고, 함수 본문이 실행되는 도중에 `(*)`로 표시한 줄에서 실행이 잠시 '중단’되었다가 프라미스가 처리되면 실행이 재개
* 이때 프라미스 객체의 `result` 값이 변수 result에 할당
* `await`는 `promise.then`보다 좀 더 세련되게 프라미스의 `result` 값을 얻을 수 있도록 해주는 문법
