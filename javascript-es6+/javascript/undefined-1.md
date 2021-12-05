# 자료형

* 자바스크립트에는 <mark style="color:orange;">여덟 가지 기본 자료형</mark>이 있음
* Number, String, Bigint, Object, Undefined, Null, Boolean, Symbol



### <mark style="color:blue;">숫자형</mark>

* &#x20;정수, 부동 소수점 숫자 등의 숫자를 나타낼 때 사용
* &#x20;정수의 한계는 ±$$2^{53}$$

```
n = 123;
n = 12.345;
```



### <mark style="color:blue;">bigint</mark>

* &#x20;길이 제약 없이 정수를 나타낼 수 있음
* &#x20;정수 리터럴 끝에 `n`을 붙이면 만들 수 있

```
// 끝에 'n'이 붙으면 BigInt형 자료
const bigInt = 1234567890123456789012345678901234567890n;
```



### <mark style="color:blue;">문자형</mark>

* &#x20;빈 문자열이나 글자들로 이뤄진 문자열을 나타낼 때 사용
* &#x20;단일 문자를 나타내는 별도의 자료형은 없

```
let str = "Hello";                         // 큰 따옴표 
let str2 = 'Single quotes are ok too';     // 작은 따옴표 
let phrase = `can embed another ${str}`;   // 역 따옴표(backtick) 
```

* 역 따옴표로 변수나 표현식을 감싼 후 `${…}`안에 넣어주면,&#x20;
  * 원하는 변수나 표현식을 문자열 중간에 넣을 수 있음

&#x20;

### <mark style="color:blue;">불린형</mark>

* &#x20;`true`, `false`를 나타낼 때 사용

```
let isGreater = 4 > 1;

alert( isGreater ); // true (비교 결과: "yes")
```



### <mark style="color:blue;">null</mark>

* `null` 값만을 위한 독립 자료형
* `null`은 알 수 없는 값을 나타냄

```
let age = null;
```



### <mark style="color:blue;">undefined</mark>

* `undefined` 값만을 위한 독립 자료형
* `undefined`는 할당되지 않은 값을 나타냄

```
// 변수는 선언했지만, 값을 할당하지 않았다면 해당 변수에 undefined가 자동으로 할당
let age;
alert(age); // 'undefined'가 출력
```



### <mark style="color:blue;">객체형과 심볼</mark>&#x20;

* 객체(object)형 : 복잡한 데이터 구조를 표현할 때 사용
* 심볼(symbol)형 : 객체의 고유 식별자를 만들 때 사용    &#x20;



### <mark style="color:blue;">typeof 연산자</mark>

* 인수의 자료형을 반환
* 자료형에 따라 처리 방식을 다르게 하고 싶거나, 변수의 자료형을 빠르게 알아내고자 할 때 유용
* `typeof` 연산자는 두 가지 형태의 문법을 지원
  1. 연산자: `typeof x`
  2. 함수: `typeof(x)`

```
typeof undefined // "undefined"

typeof 0 // "number"

typeof 10n // "bigint"

typeof true // "boolean"

typeof "foo" // "string"

typeof Symbol("id") // "symbol"

typeof Math // "object"

typeof null // "object"

typeof alert // "function"
```
