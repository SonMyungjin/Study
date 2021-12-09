---
description: https://ko.javascript.info/call-apply-decorators
---

# call/apply와 데코레이터, 포워딩

### [코드 변경 없이 캐싱 기능 추가하기](https://ko.javascript.info/call-apply-decorators#ref-2107)

* CPU를 많이 잡아먹지만 결과는 안정적인 함수 `slow(x)`가 있다고 가정
* 결과가 안정적이라는 말은 `x`가 같으면 호출 결과도 같다는 것을 의미
* `slow(x)`가 자주 호출된다면 결과를 어딘가 저장(캐싱)해 재연산에 걸리는 시간을 줄이고 싶을 것임

```
function slow(x) {
  // CPU 집약적인 작업이 여기에 올 수 있음  
  alert(`slow(${x})을/를 호출함`);
  return x;
}

function cachingDecorator(func) {
  let cache = new Map();

  return function(x) {
    if (cache.has(x)) {    // cache에 해당 키가 있으면
      return cache.get(x); // 대응하는 값을 cache에서 읽어옴  
    }

    let result = func(x);  // 그렇지 않은 경우엔 func를 호출하고,

    cache.set(x, result);  // 그 결과를 캐싱(저장) 
    return result;
  };
}

slow = cachingDecorator(slow);

alert( slow(1) ); // slow(1)이 저장 
alert( "다시 호출: " + slow(1) ); // 동일한 결과

alert( slow(2) ); // slow(2)가 저장 
alert( "다시 호출: " + slow(2) ); // 윗줄과 동일한 결과
```

* _<mark style="color:orange;">**데코레이터(decorator) :**</mark>_ `cachingDecorator`같이 인수로 받은 함수의 행동을 변경시켜주는 함수
* 모든 함수를 대상으로 `cachingDecorator`를 호출 할 수 있는데, 이때 반환되는 것은 **캐싱 래퍼**
* 함수에 `cachingDecorator`를 적용하기만 하면,
* 캐싱이 가능한 함수를 원하는 만큼 구현할 수 있기 때문에 데코레이터 함수는 아주 유용하게 사용
* 캐싱 관련 코드를 함수 코드와 분리할 수 있기 때문에 함수의 코드가 간결해진다는 장점도 있음 &#x20;



* 아래 그림에서 볼 수 있듯이 `cachingDecorator(func)`를 호출하면,
  * ‘래퍼(wrapper)’, `function(x)`이 반환
* 래퍼 `function(x)`는 `func(x)`의 호출 결과를 캐싱 로직으로 감쌈 (wrapping)

![](<../../.gitbook/assets/image (1).png>)

* 바깥 코드에서 봤을 때, 함수 `slow`는 래퍼로 감싼 이전이나 이후나 동일한 일을 수행
* `slow` 본문을 수정하는 것 보다 독립된 래퍼 함수 `cachingDecorator`를 사용할 때 생기는 이점
  *   `cachingDecorator`를 재사용 할 수 있음

      \-> 원하는 함수 어디에든 `cachingDecorator`를 적용할 수 있음
  * 캐싱 로직이 분리되어 `slow` 자체의 복잡성이 증가하지 않음 &#x20;
  *   필요하다면 여러 개의 데코레이터를 조합해서 사용할 수도 있음

      \-> 추가 데코레이터는 `cachingDecorator` 뒤를 따름



### ['func.call’를 사용해 컨텍스트 지정하기](https://ko.javascript.info/call-apply-decorators#ref-2108)

* `this`를 명시적으로 고정해 함수를 호출할 수 있게 해주는 특별한 내장 함수 메소드&#x20;

```
// 기본 문법
func.call(context, arg1, arg2, ...)
```

* 메소드를 호출하면 메소드의 첫 번째 인수가 `this`, 이어지는 인수가 `func`의 인수가 된 후, `func`이 호출



```
func(1, 2, 3);
func.call(obj, 1, 2, 3)
```

* 둘 다 인수로 `1`, `2`, `3`을 받음
* 유일한 차이점은 `func.call`에선 `this`가 `obj`로 고정



* 다른 컨텍스트(다른 객체) 하에 `sayHi`를 호출하는 예시

```
function sayHi() {
  alert(this.name);
}

let user = { name: "John" };
let admin = { name: "Admin" };

// call을 사용해 원하는 객체가 'this'가 되도록 
sayHi.call( user ); // this = John
sayHi.call( admin ); // this = Admin
```



* `call`을 사용해 컨텍스트와 `phrase`에 원하는 값을 지정

```
function say(phrase) {
  alert(this.name + ': ' + phrase);
}

let user = { name: "John" };

// this엔 user가 고정되고, "Hello"는 메서드의 첫 번째 인수가 됨  
say.call( user, "Hello" ); // John: Hello
```



### [func.apply](https://ko.javascript.info/call-apply-decorators#ref-2110)

```
// 기본 문법  
func.apply(context, args)
```

*   `apply`는 `func`의 `this`를 `context`로 고정해주고, 유사 배열 객체인 `args`를 인수로 사용할 수 있게 해줌


*   `call`과 `apply`의 문법적 차이

    * `call`은 복수 인수를 따로따로 받음
    * `apply`는 인수를 유사 배열 객체로 받음 &#x20;



```
func.call(context, ...args); // 전개 문법을 사용해 인수가 담긴 배열을 전달하는 것과
func.apply(context, args);   // call을 사용하는 것은 동일
```

* 전개 문법 `...`은 _이터러블_ `args`을 분해 해 `call`에 전달할 수 있도록 해줌
* `apply`는 오직 _유사 배열_ 형태의 `args`만 받음&#x20;



#### <mark style="color:blue;">콜 포워딩(call forwarding)</mark>

* 컨텍스트와 함께 인수 전체를 다른 함수에 전달하는 것
* `apply`를 주로 사용 &#x20;

```
let wrapper = function() {
  return func.apply(this, arguments);
};
```

* 외부에서 `wrapper`를 호출하면, 기존 함수인 `func`를 호출하는 것과 명확하게 구분할 수 있음 &#x20;

