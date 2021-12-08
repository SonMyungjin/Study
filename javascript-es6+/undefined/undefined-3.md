---
description: https://ko.javascript.info/symbol
---

# 심볼형

* 자바스크립트는 객체 프로퍼티 키로 오직 **문자형**과 **심볼형**만을 허용



### [심볼](https://ko.javascript.info/symbol#ref-1137)

* '심볼(symbol)'은 <mark style="color:orange;">**유일한 식별자(unique identifier)**</mark>를 만들고 싶을 때 사용
* `Symbol()`을 사용하면 심볼값을 만들 수 있음 &#x20;

```
// id는 새로운 심볼이 됨
let id = Symbol();
```

* 심볼을 만들 때 심볼 이름이라 불리는 설명을 붙일 수도 있음 -> 심볼 이름은 디버깅 시 아주 유용

```
// 심볼 id에는 "id"라는 설명이 붙음
let id = Symbol("id");
```

* 심볼은 유일성이 보장되는 자료형이라서, 설명이 동일한 심볼을 여러 개 만들어도 각 심볼값은 다름
* 심볼에 붙이는 설명(심볼 이름)은 어떤 것에도 영향을 주지 않는 이름표 역할만 함

```
let id1 = Symbol("id");
let id2 = Symbol("id");

alert(id1 == id2); // false
```



### [‘숨김’ 프로퍼티](https://ko.javascript.info/symbol#ref-1138)

* 심볼을 이용한 숨김 프로퍼티는 외부 코드에서 접근이 불가능하고 값도 덮어쓸 수 없는 프로퍼티

```
let user = { // 서드파티 코드에서 가져온 객체
  name: "John"
};

let id = Symbol("id");

user[id] = 1;

alert( user[id] ); // 심볼을 키로 사용해 데이터에 접근할 수 있음  
```

*   문자열 `"id"`를 키로 사용해도 되는데 `Symbol("id")`을 사용한 이유가 무엇일까?

    * `user`는 서드파티 코드에서 가지고 온 객체이므로 함부로 새로운 프로퍼티를 추가할 수 없음
    * 그런데, 심볼은 서드파티 코드에서 접근할 수 없기 때문에,&#x20;
    * 심볼을 사용하면 서드파티 코드가 모르게 `user`에 식별자를 부여할 수 있음



### [전역 심볼](https://ko.javascript.info/symbol#ref-1141)

* 전역 심볼 레지스트리 안에 심볼을 만들고 해당 심볼에 접근하면,&#x20;
  * 이름이 같은 경우 항상 동일한 심볼을 반환
* 레지스트리 안에 있는 심볼을 읽거나, 새로운 심볼을 생성하려면 `Symbol.for(key)`를 사용
  * 이 메서드를 호출하면 이름이 `key`인 심볼을 반환
  * &#x20;조건에 맞는 심볼이 레지스트리 안에 없으면 새로운 심볼 `Symbol(key)`을 만들고 레지스트리 안에 저장

```
// 전역 레지스트리에서 심볼을 읽음
let id = Symbol.for("id"); // 심볼이 존재하지 않으면 새로운 심볼을 만듦

// 동일한 이름을 이용해 심볼을 다시 읽음(좀 더 멀리 떨어진 코드에서도 가능)
let idAgain = Symbol.for("id");

// 두 심볼은 같음
alert( id === idAgain ); // true
```

* 전역 심볼 레지스트리 안에 있는 심볼은 _<mark style="color:orange;">**전역 심볼**</mark>_이라고 불림

#### Symbol.keyFor

* 전역 심볼을 찾을 때 사용되는 `Symbol.for(key)`에 반대되는 메소드 &#x20;
* `Symbol.keyFor(sym)`를 사용하면 이름을 얻을 수 있음

```
// 이름을 이용해 심볼을 찾음
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// 심볼을 이용해 이름을 얻음
alert( Symbol.keyFor(sym) ); // name
alert( Symbol.keyFor(sym2) ); // id
```

* `Symbol.keyFor`는 전역 심볼 레지스트리를 뒤져서 해당 심볼의 이름을 얻어냄
* 검색 범위가 전역 심볼 레지스트리이기 때문에 전역 심볼이 아닌 심볼에는 사용할 수 없음
* 전역 심볼이 아닌 인자가 넘어오면 `Symbol.keyFor`는 `undefined`를 반환
* 전역 심볼이 아닌 모든 심볼은 `description` 프로퍼티가 있음
* 일반 심볼에서 이름을 얻고 싶으면 `description` 프로퍼티를 사용하면 됨

```
let globalSymbol = Symbol.for("name");
let localSymbol = Symbol("name");

alert( Symbol.keyFor(globalSymbol) ); // name, 전역 심볼
alert( Symbol.keyFor(localSymbol) ); // undefined, 전역 심볼이 아님

alert( localSymbol.description ); // name
```



### [시스템 심볼](https://ko.javascript.info/symbol#ref-1143)

* '시스템 심볼(system symbol)'은 자바스크립트 내부에서 사용되는 심볼
* 시스템 심볼을 활용하면 객체를 미세 조정할 수 있음
  * `Symbol.hasInstance`
  * `Symbol.isConcatSpreadable`
  * `Symbol.iterator`
  * `Symbol.toPrimitive`
