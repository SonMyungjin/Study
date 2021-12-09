---
description: https://ko.javascript.info/prototype-inheritance
---

# 프로토타입 상속

### [\[\[Prototype\]\]](https://ko.javascript.info/prototype-inheritance#ref-1879)

* 자바스크립트의 객체는 명세서에서 명명한 `[[Prototype]]`이라는 숨김 프로퍼티를 가짐
* 이 숨김 프로퍼티 값은 `null`이거나 다른 객체에 대한 참조가되는데,&#x20;
* 다른 객체를 참조하는 경우 참조 대상을 '프로토타입(prototype)'이라 부름

![](<../../.gitbook/assets/image (13).png>)

* `object`에서 프로퍼티를 읽으려고 하는데,
* 해당 프로퍼티가 없으면 자바스크립트는 자동으로 프로토타입에서 프로퍼티를 찾음
* 이를 <mark style="color:orange;">**프로토타입 상속**</mark>이라 부름
* `[[Prototype]]` 프로퍼티는 내부 프로퍼티이면서 숨김 프로퍼티이지만 다양한 방법을 사용해 개발자가 값을 설정할 수 있음

```
let animal = {
  eats: true
};
let rabbit = {
  jumps: true
};

rabbit.__proto__ = animal;
```



{% hint style="info" %}
**`__proto__`는 `[[Prototype]]`용 getter·setter**

* &#x20;`__proto__`는 `[[Prototype]]`의 getter(획득자)이자 setter(설정자)
* `__proto__` 대신 함수 `Object.getPrototypeOf`나 `Object.setPrototypeOf 사`
{% endhint %}



### ['this’가 나타내는 것](https://ko.javascript.info/prototype-inheritance#ref-1881)

* `this`는 프로토타입에 영향을 받지 않음
* 메소드를 객체에서 호출했든 프로토타입에서 호출했든 상관없이 this는 언제나 . 앞에 있는 객체가 됨

