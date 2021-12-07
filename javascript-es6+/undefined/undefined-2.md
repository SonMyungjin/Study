---
description: https://ko.javascript.info/garbage-collection
---

# 가비지 컬렉션

* 자바스크립트는 눈에 보이지 않는 곳에서 메모리 관리를 수행
* 가비지 컬렉터는 모든 객체를 모니터링하고, 도달할 수 없는 객체는 삭제



### [가비지 컬렉션 기준](https://ko.javascript.info/garbage-collection#ref-32)

* 자바스크립트는 _<mark style="color:orange;">**도달 가능성(reachability)**</mark>_ 이라는 개념을 사용해 메모리 관리를 수행
* ‘도달 가능한(reachable)’ 값은 쉽게 말해 어떻게든 접근하거나 사용할 수 있는 값을 의미
* 도달 가능한 값은 메모리에서 삭제되지 않음

1. 태생부터 도달 가능하기 때문에, 명백한 이유 없이는 삭제되지 않음

* 현재 함수의 지역 변수와 매개변수
* 중첩 함수의 체인에 있는 함수에서 사용되는 변수와 매개변수
* 전역 변수
* 기타 등등 -> 이런 값은 _루트(root)_ 라고 함

2\. 루트가 참조하는 값이나 체이닝으로 루트에서 참조할 수 있는 값은 도달 가능한 값이 됨



### [예시](https://ko.javascript.info/garbage-collection#ref-33)

```
// user엔 객체 참조 값이 저장
let user = {
  name: "John"
};
```

![](<../../.gitbook/assets/image (3) (1) (1).png>)

* 화살표는 객체 참조를 나타냄
* 전역 변수 `"user"`는 `{name: "John"}` (줄여서 John)이라는 객체를 참조
* John의 프로퍼티 `"name"`은 원시값을 저장하고 있기 때문에 객체 안에 표현

```
user = null;
```

![](<../../.gitbook/assets/image (2).png>)

* `user`의 값을 다른 값으로 덮어쓰면 참조(화살표)가 사라짐
* John은 도달할 수 없는 상태가 되어 가비지 컬렉터는 John을 메모리에서 삭제    &#x20;

