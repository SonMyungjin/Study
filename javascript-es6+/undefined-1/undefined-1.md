---
description: https://ko.javascript.info/array-methods
---

# 배열과 메소드

### [요소 추가·제거 메서드](https://ko.javascript.info/array-methods#ref-57)

* `arr.push(...items)` – 맨 끝에 요소 추가
* `arr.pop()` – 맨 끝 요소 제거
* `arr.shift()` – 맨 앞 요소 제거
* `arr.unshift(...items)` – 맨 앞에 요소 추가



#### splice

* `delete` 연산자는 키에 대응하는 값만 지우고  키는 지우지  못함
* `splice`는 <mark style="color:orange;">**요소 추가, 삭제, 교체**</mark>가 모두 가능

```
// 기본 문법
arr.splice(index[, deleteCount, elem1, ..., elemN])
```

* 첫 번째 매개변수는 조작을 가할 첫 번째 요소를 가리키는 `인덱스(index)`
* 두 번째 매개변수는 `deleteCount`로, 제거하고자 하는 요소의 개수
* &#x20;`elem1, ..., elemN`은 배열에 추가할 요소를 나타



* 요소 세 개(3)를 지우고, 그 자리를 다른 요소 두 개로 교체

```
let arr = ["I", "study", "JavaScript", "right", "now"];

// 처음(0) 세 개(3)의 요소를 지우고, 이 자리를 다른 요소로 대체
arr.splice(0, 3, "Let's", "dance");

alert( arr ) // now ["Let's", "dance", "right", "now"]
```

&#x20;

* `splice`는 삭제된 요소로 구성된 배열을 반환

```
let arr = ["I", "study", "JavaScript", "right", "now"];

// 처음 두 개의 요소를 삭제함
let removed = arr.splice(0, 2);

alert( removed ); // "I", "study" <-- 삭제된 요소로 구성된 배열
```



* `splice` 메서드의 `deleteCount`를 `0`으로 설정하면 요소를 제거하지 않으면서 새로운 요소를 추가

```
let arr = ["I", "study", "JavaScript"];

// 인덱스 2부터
// 0개의 요소를 삭제
// 그 후, "complex"와 "language"를 추가
arr.splice(2, 0, "complex", "language");

alert( arr ); // "I", "study", "complex", "language", "JavaScript"
```



#### slice

```
// 기본 문 
arr.slice([start], [end])
```

* &#x20;`"start"` 인덱스부터 (`"end"`를 제외한) `"end"`인덱스까지의 요소를 복사한 새로운 배열을 반환
* `start`와 `end`는 둘 다 음수일 수 있는데 이땐, 배열 끝에서부터의 요소 개수를 의미
*   `arr.slice`는 문자열 메서드인 `str.slice`와 유사하게 동작하는데&#x20;

    * `arr.slice`는 서브 문자열(substring) 대신 서브 배열(subarray)을 반환한다는 점이 다름



```
let arr = ["t", "e", "s", "t"];

alert( arr.slice(1, 3) ); // e,s (인덱스가 1인 요소부터 인덱스가 3인 요소까지를 복사(인덱스가 3인 요소는 제외))

alert( arr.slice(-2) ); // s,t (인덱스가 -2인 요소부터 제일 끝 요소까지를 복사)
```

* `arr.slice()`는 인수를 하나도 넘기지 않고 호출하여 `arr`의 복사본을 만들 수 있음
* 이런 방식은 <mark style="color:orange;">**기존의 배열을 건드리지 않으면서 배열을 조작해 새로운 배열을 만들고자 할 때**</mark> 자주 사용



#### concat

* 기존 배열의 요소를 사용해 <mark style="color:orange;">**새로운 배열을 만들거나 기존 배열에 요소를 추가**</mark>하고자 할 때 사용

```
// 기본 문 
arr.concat(arg1, arg2...)
```

* 메드를 호출하면 `arr`에 속한 모든 요소와 `arg1`, `arg2` 등에 속한 모든 요소를 한데 모은 새로운 배열이 반환됨



```
let arr = [1, 2];

// arr의 요소 모두와 [3,4]의 요소 모두를 한데 모은 새로운 배열이 만들어
alert( arr.concat([3, 4]) ); // 1,2,3,4

// arr의 요소 모두와 [3,4]의 요소 모두, [5,6]의 요소 모두를 모은 새로운 배열이 만들어집니다.
alert( arr.concat([3, 4], [5, 6]) ); // 1,2,3,4,5,6

// arr의 요소 모두와 [3,4]의 요소 모두, 5와 6을 한데 모은 새로운 배열이 만들어짐
alert( arr.concat([3, 4], 5, 6) ); // 1,2,3,4,5,6
```

* `concat` 메소드는 제공받은 배열의 요소를 복사해 활용
* 객체가 인자로 넘어오면 (배열처럼 보이는 유사 배열 객체이더라도) 객체는 분해되지 않고 통으로 복사되어 더해짐



```
let arr = [1, 2];

let arrayLike = {
  0: "something",
  length: 1
};

alert( arr.concat(arrayLike) ); // 1,2,[object Object]
```

```
let arr = [1, 2];

let arrayLike = {
  0: "something",
  1: "else",
  [Symbol.isConcatSpreadable]: true,
  length: 2
};

alert( arr.concat(arrayLike) ); // 1,2,something,else
```

* 인자로 받은 유사 배열 객체에 특수한 프로퍼티 `Symbol.isConcatSpreadable`이 있으면 `concat`은 이 객체를 배열처럼 취급
* 따라서 객체 전체가 아닌 객체 프로퍼티의 값이 더해



### [forEach로 반복작업 하기](https://ko.javascript.info/array-methods#ref-61)

* arr.forEach는 주어진 함수를 배열 요소 각각에 대해 실행할 수 있게 해줌 &#x20;

```
// 기본 문법 
arr.forEach(function(item, index, array) {
  // 요소에 무언가를 할 수 있음
});
```

```
// 예제
["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => {
  alert(`${item} is at index ${index} in ${array}`);
});
```



### [배열 탐색하기](https://ko.javascript.info/array-methods#ref-62)

#### indexOf, lastIndexOf, includes

*   `arr.indexOf(item, from)`

    * 인덱스 `from`부터 시작해 `item(요소)`을 찾음
    * 요소를 발견하면 해당 요소의 인덱스를 반환하고, 발견하지 못했으면 `-1`을 반환


*   `arr.lastIndexOf(item, from)`

    * 위 메소드와 동일한 기능을 하는데, 검색을 끝에서부터 시작한다는 점만 다름


*   `arr.includes(item, from)`

    * 인덱스 `from`부터 시작해 `item`이 있는지를 검색하는데,&#x20;
    * 해당하는 요소를 발견하면 `true`를 반환



```
let arr = [1, 0, false];

alert( arr.indexOf(0) ); // 1
alert( arr.indexOf(false) ); // 2
alert( arr.indexOf(null) ); // -1

alert( arr.includes(1) ); // true
```

* 위 메소드들은 요소를 찾을 때 완전 항등 연산자 `===` 을 사용
  * `false`를 검색하면 정확히 `false`만을 검색하지, 0을 검색하진 않음 &#x20;
* 요소의 위치를 정확히 알고 싶은게 아니고 요소가 배열 내 존재하는지 여부만 확인하고 싶다면 `arr.includes`를 사용



#### find 와 findIndex&#x20;

* <mark style="color:orange;">**특정 조건에 부합하는 객체를 배열 내 찾을 때**</mark> 사용&#x20;

```
let result = arr.find(function(item, index, array) {
  // true가 반환되면 반복이 멈추고 해당 요소를 반환
  // 조건에 해당하는 요소가 없으면 undefined를 반환
});
```

*   요소 전체를 대상으로 함수가 순차적으로 호출

    * `item` – 함수를 호출할 요소
    * `index` – 요소의 인덱스
    * `array` – 배열 자기 자신


* 함수가 참을 반환하면 탐색은 중단되고 해당 `요소`가 반환
  * 원하는 요소를 찾지 못했으면 `undefined`가 반환

```
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

let user = users.find(item => item.id == 1);

alert(user.name); // John
```



* `arr.findIndex`
  * `find`와 동일한 일을 하나, <mark style="color:orange;">**조건에 맞는 요소를 반환하는 대신 해당 요소의 인덱스를 반환**</mark>
  * &#x20;조건에 맞는 요소가 없으면 `-1`이 반환



#### filter

* <mark style="color:orange;">**함수의 반환 값을**</mark><mark style="color:orange;">** **</mark><mark style="color:orange;">**`true`**</mark><mark style="color:orange;">**로 만드는 단 하나의 요소를 찾음**</mark>
* 조건을 충족하는 요소가 여러 개라면 `arr.filter(fn)` 사용
* `filter`는 `find`와 문법이 유사하지만,&#x20;
  * 조건에 맞는 요소 전체를 담은 배열을 반환한다는 점에서 차이가 있음

```
// 기본 문 
let results = arr.filter(function(item, index, array) {
  // 조건을 충족하는 요소는 results에 순차적으로 더해짐
  // 조건을 충족하는 요소가 하나도 없으면 빈 배열이 반환
});
```

```
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

// 앞쪽 사용자 두 명을 반환
let someUsers = users.filter(item => item.id < 3);

alert(someUsers.length); // 2
```



### [배열을 변형하는 메소드](https://ko.javascript.info/array-methods#ref-66)

#### map

* 배열 요소 전체를 대상으로 함수를 호출하고, 함수 호출 결과를 배열로 반환

```
// 기본 문 
let result = arr.map(function(item, index, array) {
  // 요소 대신 새로운 값을 반환
});
```

```
let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length);
alert(lengths); // 5,7,6
```

* 각 요소(문자열)의 길이를 출



#### sort(fn)

* 배열의 요소를 정렬 -> 배열 _자체_가 변경
* 메소드를 호출하면 재정렬 된 배열이 반환되는데,&#x20;
  * 이미 `arr` 자체가 수정되었기 때문에 반환 값은 잘 사용되지 않는 편

```
let arr = [ 1, 2, 15 ];

// arr 내부가 재정렬
arr.sort();

alert( arr );  // 1, 15, 2
```

* **요소는 문자열로 취급되어 재정렬** -> ("2" > "15")



* 기본 정렬 기준 대신 새로운 정렬 기준을 만들려면 `arr.sort()`에 새로운 함수를 넘겨줘야 함
* 인수로 넘겨주는 함수는 반드시 값 두 개를 비교해야 하고 반환 값도 있어야 함

```
function compareNumeric(a, b) {
  if (a > b) return 1; // 첫 번째 값이 두 번째 값보다 큰 경우
  if (a == b) return 0; // 두 값이 같은 경우
  if (a < b) return -1; //  첫 번째 값이 두 번째 값보다 작은 경우
}

let arr = [ 1, 2, 15 ];

arr.sort(compareNumeric);

alert(arr);  // 1, 2, 15
```



#### reverse

* `arr`의 요소를 역순으로 정렬시켜주는 메소드

```
let arr = [1, 2, 3, 4, 5];
arr.reverse();

alert( arr ); // 5,4,3,2,1
```



#### split

* 구분자(delimiter) `delim`을 기준으로 문자열을 쪼개

```
let names = 'Bilbo, Gandalf, Nazgul';

let arr = names.split(', ');

for (let name of arr) {
  alert( `${name}에게 보내는 메시지` ); // Bilbo에게 보내는 메시지
}
```



#### join

* `split`과 반대 역할을 하는 메소드
* 인수 `glue`를 접착제처럼 사용해 배열 요소를 모두 합친 후 하나의 문자열을 만들어줌

```
let arr = ['Bilbo', 'Gandalf', 'Nazgul'];

let str = arr.join(';'); // 배열 요소 모두를 ;를 사용해 하나의 문자열로 합침

alert( str ); // Bilbo;Gandalf;Nazgul
```



#### reduce와 reduceRight

* `forEach`, `for`, `for..of`를 사용하면 배열 내 요소를 대상으로 반복 작업을 할 수 있음
* 각 요소를 돌면서 반복 작업을 수행하고, 작업 결과물을 새로운 배열 형태로 얻으려면 `map`을 사용
* arr.reduce와 arr.reduceRight도 위 메소드들과  유사한 작업을 수행   &#x20;
* `reduce`와 `reduceRight`는 <mark style="color:orange;">**배열을 기반으로 값 하나를 도출할 때 사용**</mark>



```
// 기본 문법
let value = arr.reduce(function(accumulator, item, index, array) {
  // ...
}, [initial]);
```

* 인수로 넘겨주는 함수는 배열의 모든 요소를 대상으로 차례차례 적용되는데,&#x20;
  * 적용 결과는 다음 함수 호출 시 사용됨
  * `accumulator` – 이전 함수 호출의 결과(옵)
  * `initial`- 함수 최초 호출 시 사용되는 초깃값을 나타냄(옵션)
  * `item` – 현재 배열 요소
  * `index` – 요소의 위치
  * `array` – 배열



```
let arr = [1, 2, 3, 4, 5];

let result = arr.reduce((sum, current) => sum + current, 0);

alert(result); // 15
```

* `reduce`에 전달한 함수는 오직 인수 두 개만 받고 있음 -> 대개 이렇게 인수를 두 개만 받음
*   과정

    1. 함수 최초 호출 시, `reduce`의 마지막 인수인 `0(초깃값)`이 `sum`에 할당

    &#x20;    `current`엔 배열의 첫 번째 요소인 `1`이 할당

    &#x20;     따라서 함수의 결과는 `1`이 됨

    1. 두 번째 호출 시, `sum = 1` 이고 여기에 배열의 두 번째 요소(`2`)가 더해지므로 결과는 `3`
    2. 세 번째 호출 시, `sum = 3` 이고 여기에 배열의 다음 요소가 더해지고 이런 과정이 계속 이어

![](<../../.gitbook/assets/image (7) (1) (1) (1) (1).png>)



### [Array.isArray로 배열 여부 알아내기](https://ko.javascript.info/array-methods#ref-72)

* 자바스크립트에서 배열은 독립된 자료형으로 취급되지 않고 객체형에 속함  &#x20;
* 따라서, `typeof`로는 일반 객체와 배열을 구분할 수 없음

```
alert(typeof {}); // object
alert(typeof []); // object
```



* `Array.isArray`는 <mark style="color:orange;">**배열인지 아닌지를 감별해내는 메소드**</mark>
* `value`가 배열이라면 `true`를, 배열이 아니라면 `false`를 반환

```
alert(Array.isArray({})); // false

alert(Array.isArray([])); // true
```

