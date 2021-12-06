---
description: https://ko.javascript.info/nullish-coalescing-operator
---

# null 병합 연산자 '??'

### <mark style="color:blue;">null 병합 연산자(nullish coalescing operator) '??'</mark>

* 짧은 문법으로 여러 피연산자 중 그 값이 ‘확정되어있는’ 변수를 찾을 수 있음
* <mark style="color:red;">**a ?? b**</mark>
  * `a`가 `null`도 아니고 `undefined`도 아니면 `a`
  * 그 외의 경우는 `b`
  * (a !== null && a !== undefined) ? a : b; 과 같은 의미 &#x20;

```
let firstName = null;
let lastName = null;
let nickName = "바이올렛";

// null이나 undefined가 아닌 첫 번째 피연산자
alert(firstName ?? lastName ?? nickName ?? "익명의 사용자"); // 바이올렛
```



### ['??'와 '||'의 차이](https://ko.javascript.info/nullish-coalescing-operator#ref-111)

* `||`는 첫 번째 _truthy_ 값을 반환
* `??`는 첫 번째 _정의된(defined)_ 값을 반환

```
let height = 0;

alert(height || 100); // 100
alert(height ?? 100); // 0
```

*   `height || 100`

    * `height`에 `0`을 할당했지만 `0`을 falsy 한 값으로 취급했기 때문에&#x20;
    * `null`이나 `undefined`를 할당한 것과 동일하게 처리
    * 따라서 `height || 100`의 평가 결과는 `100`

    ``
* &#x20;`height ?? 100`
  * `height`가 정확하게 `null`이나 `undefined`일 경우에만 `100`이 됨&#x20;
  * 예시에선 `height`에 `0`이라는 값을 할당했기 때문에 alert에는 `0`이 출력\


### [연산자 우선순위](https://ko.javascript.info/nullish-coalescing-operator#ref-112)

* [`??`의 연산자 우선순위](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator\_Precedence#Table)는 `5`로 낮기 때문에 복잡한 표현식 안에서 `??`를 사용해 값을 하나 선택할 땐 괄호를 추가

```
let height = null;
let width = null;

// 괄호 추가!
let area = (height ?? 100) * (width ?? 50);

alert(area); // 5000
```

* <mark style="color:orange;">**안정성 관련 이슈 때문에**</mark><mark style="color:orange;">** **</mark><mark style="color:orange;">**`??`**</mark><mark style="color:orange;">**는**</mark><mark style="color:orange;">** **</mark><mark style="color:orange;">**`&&`**</mark><mark style="color:orange;">**나**</mark><mark style="color:orange;">** **</mark><mark style="color:orange;">**`||`**</mark><mark style="color:orange;">**와 함께 사용하지 못함**</mark>

```
let x = 1 && 2 ?? 3; // SyntaxError: Unexpected token '??'

let x = (1 && 2) ?? 3; // 제약을 피하려면 괄호를 사용

alert(x); // 2 
```
