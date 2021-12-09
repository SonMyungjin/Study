---
description: https://ko.javascript.info/prototype-methods
---

# 프로토타입 메서드와 \_\_proto\_\_가 없는 객체

*   `__proto__`는 대신 사용하는 메소드

    * [Object.create(proto, \[descriptors\])](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global\_Objects/Object/create) – `[[Prototype]]`이 `proto`를 참조하는 빈 객체를 만듦,이때 프로퍼티 설명자를 추가로 넘길 수 있음
    * [Object.getPrototypeOf(obj)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global\_Objects/Object/getPrototypeOf) – `obj`의 `[[Prototype]]`을 반환
    * [Object.setPrototypeOf(obj, proto)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global\_Objects/Object/setPrototypeOf) – `obj`의 `[[Prototype]]`이 `proto`가 되도록 설정

    &#x20;

```
let animal = {
  eats: true
};

// 프로토타입이 animal인 새로운 객체를 생성
let rabbit = Object.create(animal);

alert(rabbit.eats); // true

alert(Object.getPrototypeOf(rabbit) === animal); // true

Object.setPrototypeOf(rabbit, {}); // rabbit의 프로토타입을 {}으로 바
```



* 사용자가 키를 직접 만들 수 있게 허용하면, 내장 `__proto__` getter·setter는 안전하지 않음
* 키가 `"__proto__"`일 때 에러가 발생할 수 있고,예측 불가능한 결과가 생김&#x20;
