---
description: https://ko.javascript.info/array
---

# 배열

#### 배열이란?

* 순서가 있는 컬렉션을 저장할 때 쓰는 자료구조
* 임의의 키를 사용해야 한다면 배열보단 일반 객체 `{}`가 적합한 자료구조



### [배열 선언](https://ko.javascript.info/array#ref-283)

* 빈 배열 만들기

```
let arr = new Array();
let arr = [];
```



* 각 배열 요소엔 0부터 시작하는 숫자(인덱스)가 매겨져 있음
  * 이 숫자들은 배열 내 순서를 나타
* 배열 내 특정 요소를 얻고 싶다면 대괄호 안에 순서를 나타내는 숫자인 인덱스를 넣어주면 됨

```
let fruits = ["사과", "오렌지", "자두"];

alert( fruits[0] ); // 사과
alert( fruits[1] ); // 오렌지
alert( fruits[2] ); // 자두

// 수정
fruits[2] = '배'; // 배열이 ["사과", "오렌지", "배"]로 바뀜

// 추가
fruits[3] = '레몬'; // 배열이 ["사과", "오렌지", "배", "레몬"]으로 바뀜
```



* `length`를 사용하면 배열에 담긴 요소가 몇 개인지 알아낼 수 있음

```
let fruits = ["사과", "오렌지", "자두"];

alert( fruits.length ); // 3
```



* 배열 요소의 자료형엔 제약이 없음

```
// 요소에 여러 가지 자료형이 섞여 있음
let arr = [ '사과', { name: '이보라' }, true, function() { alert('안녕하세요.'); } ];

// 인덱스가 1인 요소(객체)의 name 프로퍼티를 출력
alert( arr[1].name ); // 이보라

// 인덱스가 3인 요소(함수)를 실행
arr[3](); // 안녕하세요.
```



{% hint style="info" %}
**trailing 쉼표**

* 배열의 마지막 요소는 객체와 마찬가지로 쉼표로 끝날 수 있음
* trailing(길게 늘어지는) 쉼표를 사용하면 모든 줄의 생김새가 유사해지기 때문에 요소를 넣거나 빼기가 쉬워짐
{% endhint %}

****

### [pop·push와 shift·unshift](https://ko.javascript.info/array#ref-284)

*   큐(queue)

    * 배열을 사용해 만들 수 있는 대표적인 자료구조로,&#x20;
    * 배열과 마찬가지로 순서가 있는 컬렉션을 저장하는 데 사용
    * 화면에 순차적으로 띄울 메시지를 비축해 놓을 자료 구조를 만들 때 사
    * `push` – 맨 끝에 요소를 추가
    * `shift` – 제일 앞 요소를 꺼내 제거한 후 남아있는 요소들을 앞으로 밀어짐

    ![](<../../.gitbook/assets/image (6) (1) (1) (1).png>)




*   스택(stack)

    * '한쪽 끝’에 요소를 더하거나 뺄 수 있게 해주는 자료구조
    * `push` – 요소를 스택 끝에 집어넣음
    * `pop` – 스택 끝 요소를 추출

    ![](<../../.gitbook/assets/image (4) (1) (1).png>)



* pop
  * <mark style="color:orange;">**배열**</mark>** **<mark style="color:red;">**끝**</mark>** **<mark style="color:orange;">**요소를 제거**</mark>하고, 제거한 요소를 반환

```
let fruits = ["사과", "오렌지", "배"];

alert( fruits.pop() ); // 배열에서 "배"를 제거하고 제거된 요소를 alert 창에 띄움

alert( fruits ); // 사과,오렌지
```



* `push`
  * <mark style="color:orange;">**배열**</mark>** **<mark style="color:red;">**끝**</mark><mark style="color:orange;">**에 요소를 추가**</mark>

```
let fruits = ["사과", "오렌지"];

fruits.push("배");

alert( fruits ); // 사과,오렌지,배
```



* `shift`
  * <mark style="color:orange;">**배열**</mark>** **<mark style="color:red;">**앞**</mark>** **<mark style="color:orange;">**요소를 제거**</mark>하고, 제거한 요소를 반환

```
let fruits = ["사과", "오렌지", "배"];

alert( fruits.shift() ); // 배열에서 "사과"를 제거하고 제거된 요소를 alert 창에 띄

alert( fruits ); // 오렌지,배
```



* `unshift`
  * <mark style="color:orange;">**배열**</mark>** **<mark style="color:red;">**앞**</mark><mark style="color:orange;">**에 요소를 추가**</mark>

```
let fruits = ["오렌지", "배"];

fruits.unshift('사과');

alert( fruits ); // 사과,오렌지,배
```



### [성능](https://ko.javascript.info/array#ref-286)

* `push`와 `pop`은 빠르지만 `shift`와 `unshift`는 느림

![](<../../.gitbook/assets/image (2) (1) (1) (1).png>)



* `shift` 연산은 아래 3가지 동작을 모두 수행해야 이뤄짐

1. 인덱스가 `0`인 요소를 제거
2. 모든 요소를 왼쪽으로 이동시킴->  이때 인덱스 `1`은 `0`, `2`는 `1`로 변함
3. `length` 프로퍼티 값을 갱신

![](<../../.gitbook/assets/image (3) (1) (1).png>)

* **배열에 요소가 많으면 요소가 이동하는 데 걸리는 시간이 길고 메모리 관련 연산도 많아짐**
  * `push`와 `pop`은 끝을 제거/추가 하기 때문에 요소 이동을 수반 X&#x20;
  * 그렇기 때문에 성능적으로 `push`와 `pop` 이 더 우수



### [반복문](https://ko.javascript.info/array#ref-287)

* `for`문

```
let arr = ["사과", "오렌지", "배"];

for (let i = 0; i < arr.length; i++) {
  alert( arr[i] );
}
```



* `for..of` 문

```
let fruits = ["사과", "오렌지", "자두"];

// 배열 요소를 대상으로 반복 작업을 수행
for (let fruit of fruits) {
  alert( fruit );
}
```

* `for..of`를 사용하면 <mark style="color:orange;">**현재 요소의 인덱스는 얻을 수 없고**</mark> 값만 얻을 수 있음



* `for..in` 문

```
let arr = ["사과", "오렌지", "배"];

for (let key in arr) {
  alert( arr[key] ); // 사과, 오렌지, 배
}
```

``

{% hint style="info" %}
`for..in` 문의 문제점

*   `for..in` 반복문은 _모든 프로퍼티_를 대상으로 순회하여,&#x20;

    * 키가 숫자가 아닌 프로퍼티도 순회 대상에 포함
    * ‘필요 없는’ 프로퍼티들이 문제를 일으킬 가능성이 생김


* 배열이 아니라 객체와 함께 사용할 때 최적화되어 있어서,
  * &#x20;배열에 사용하면 객체에 사용하는 것 대비 10\~100배 정도 느림
{% endhint %}

