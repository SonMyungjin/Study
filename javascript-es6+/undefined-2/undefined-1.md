---
description: https://ko.javascript.info/rest-parameters-spread
---

# 나머지 매개변수와 전개 문법

### [나머지 매개변수 `...`](https://ko.javascript.info/rest-parameters-spread#ref-1198)

* "나머지 매개변수들을 한데 모아 배열에 집어넣어라."는 것을 의미



* 앞부분의 매개변수는 변수로, 그 이외의 매개변수들은 배열로 모을 수도 있음
* 아래 예시에선 처음 두 인수는 변수에, 나머지 인수들은 `titles`이라는 배열에 할당

```
function showName(firstName, lastName, ...titles) {
  alert( firstName + ' ' + lastName ); // Julius Caesar

  // 나머지 인수들은 배열 titles의 요소가 됨
  // titles = ["Consul", "Imperator"]
  alert( titles[0] ); // Consul
  alert( titles[1] ); // Imperator
  alert( titles.length ); // 2
}

showName("Julius", "Caesar", "Consul", "Imperator");
```

{% hint style="info" %}
나머지 매개변수는 항상 마지막에 있어야 함!

* 나머지 매개변수는 남아있는 인수를 모으는 역할을 하므로 항상 마지막에 있어야 함 &#x20;
{% endhint %}



### [‘arguments’ 변수](https://ko.javascript.info/rest-parameters-spread#ref-1199)

* `arguemnts`라는 특별한 유사 배열 객체(array-like object)를 이용하면 인덱스를 사용해 모든 인수에 접근할 수 있음

```
function showName() {
  alert( arguments.length );
  alert( arguments[0] );
  alert( arguments[1] );

  // arguments는 이터러블 객체이기 때문에
  // for(let arg of arguments) alert(arg); 를 사용해 인수를 나열할 수 있음  
}

// 2, Julius, Caesar가 출력됨
showName("Julius", "Caesar");

// 1, Bora, undefined가 출력됨(두 번째 인수는 없음)
showName("Bora");
```

* `arguments`는 유사 배열 객체이면서 이터러블(반복 가능한) 객체로 배열 X
  * 따라서 배열 메소드를 사용할 수 없다는 단점이 있음&#x20;



### [spread 문법](https://ko.javascript.info/rest-parameters-spread#spread-syntax)

* 배열을 통째로 매개변수에 넘겨주는 것으로 배열을 매개변수 목록으로 가져오는 방법

```
let arr = [3, 5, 1];

alert( Math.max(arr) ); // NaN
alert( Math.max(...arr) ); // 5 
```



* 메드 `Array.from`은 문자열 같은 이터러블 객체를 배열로 바꿔주기 때문에 `Array.from`을 사용해도 동일한 작업을 할 수 있음

```
let str = "Hello";

// Array.from은 이터러블을 배열로 바꿔줌  
alert( Array.from(str) ); // H,e,l,l,o
```

