---
description: https://ko.javascript.info/map-set
---

# Map과 Set

* 객체 – 키가 있는 컬렉션을 저장함
* 배열 – 순서가 있는 컬렉션을 저장함
* 하지만 현실 세계를 반영하기엔 이 두 자료구조 만으론 부족해서 `맵(Map)`과 `셋(Set)`이 등장



### [맵](https://ko.javascript.info/map-set#ref-890)<mark style="color:blue;">(Map)</mark>

* 키가 있는 데이터를 저장한다는 점에서 `객체`와 유사
*   다만, `맵`은 <mark style="color:orange;">**키에 다양한 자료형을 허용**</mark>한다는 점에서 차이가 있음


* 맵의 주요 메소드와  프로퍼티
  * `new Map()` – 맵 생성
  * `map.set(key, value)` – `key`를 이용해 `value`를 저장
  * `map.get(key)` – `key`에 해당하는 값을 반환 / `key`가 존재하지 않으면 `undefined`를 반환
  * `map.has(key)` – `key`가 존재하면 `true`, 존재하지 않으면 `false`를 반환
  * `map.delete(key)` – `key`에 해당하는 값을 삭제
  * `map.clear()` – 맵 안의 모든 요소를 제거
  * `map.size` – 요소의 개수를 반환

```
let map = new Map();

map.set('1', 'str1');   // 문자형 키
map.set(1, 'num1');     // 숫자형 키
map.set(true, 'bool1'); // 불린형 키

// 객체는 키를 문자형으로 변환
// 맵은 키의 타입을 변환시키지 않고 그대로 유지
// 따라서 아래의 코드는 출력되는 값이 다
alert( map.get(1)   ); // 'num1'
alert( map.get('1') ); // 'str1'

alert( map.size ); // 3
```



### [맵의 요소에 반복 작업하기](https://ko.javascript.info/map-set#ref-891)

* 세 가지 메서드를 사용해 `맵`의 각 요소에 반복 작업을 할 수 있습니다.
  * `map.keys()` – 각 요소의 키를 모은 반복 가능한(iterable, 이터러블) 객체를 반환
  * `map.values()` – 각 요소의 값을 모은 이터러블 객체를 반환
  * `map.entries()` – 요소의 `[키, 값]`을 한 쌍으로 하는 이터러블 객체를 반환
    * 이 이터러블 객체는 `for..of`반복문의 기초로 쓰임

```
let recipeMap = new Map([
  ['cucumber', 500],
  ['tomatoes', 350],
  ['onion',    50]
]);

// 키(vegetable)를 대상으로 순회
for (let vegetable of recipeMap.keys()) {
  alert(vegetable); // cucumber, tomatoes, onion
}

// 값(amount)을 대상으로 순회
for (let amount of recipeMap.values()) {
  alert(amount); // 500, 350, 50
}

// [키, 값] 쌍을 대상으로 순회
for (let entry of recipeMap) { // recipeMap.entries()와 동일
  alert(entry); // cucumber,500 ...
}
```



### [Object.entries: 객체를 맵으로 바꾸기](https://ko.javascript.info/map-set#ref-892)

* 각 요소가 키-값 쌍인 배열이나 이터러블 객체를 초기화 용도로 맵에 전달해 새로운 맵을 만들 수 있음

```
// 각 요소가 [키, 값] 쌍인 배열
let map = new Map([
  ['1',  'str1'],
  [1,    'num1'],
  [true, 'bool1']
]);

alert( map.get('1') ); // str1
```



* 평범한 객체를 가지고 `맵`을 만들고 싶다면 내장 메서드 `Object.entries(obj)`를 활용
* 이 메소드는 객체의 키-값 쌍을 요소(`[key, value]`)로 가지는 배열을 반환

```
let obj = {
  name: "John",
  age: 30
};

let map = new Map(Object.entries(obj));

alert( map.get('name') ); // John
```

* `Object.entries`를 사용해 객체 `obj`를 배열 `[["name","John"], ["age", 30]]`로 바꾸고
* &#x20;이 배열을 이용해 새로운 `맵`을 만듦



### [Object.fromEntries: 맵을 객체로 바꾸기](https://ko.javascript.info/map-set#ref-893)

* 각 요소가 `[키, 값]` 쌍인 배열을 객체로 바꿔줌

```
let map = new Map();
map.set('banana', 1);
map.set('orange', 2);
map.set('meat', 4);

let obj = Object.fromEntries(map.entries()); // 맵을 일반 객체로 변환, map으로 써도 됨

// 맵이 객체가 됨
// obj = { banana: 1, orange: 2, meat: 4 }

alert(obj.orange); // 2
```



### [셋(Set)](https://ko.javascript.info/map-set#ref-894)

* <mark style="color:orange;">**중복을 허용하지 않는 값을 모아놓은**</mark> 특별한 컬렉션
*   셋에 <mark style="color:orange;">**키가 없는 값이 저장**</mark>

    <mark style="color:orange;">****</mark>
* 셋(Set)의 주요 메서드
  * `new Set(iterable)` – 셋을 만듦 -> `이터러블` 객체를 전달받으면(대개 배열을 전달받음) 그 안의 값을 복사해 셋에 넣어줌
  * `set.add(value)` – 값을 추가하고 셋 자신을 반환
  * `set.delete(value)` – 값을 제거 -> 호출 시점에 셋 내에 값이 있어서 제거에 성공하면 `true`, 아니면 `false`를 반환
  * `set.has(value)` – 셋 내에 값이 존재하면 `true`, 아니면 `false`를 반환
  * `set.clear()` – 셋을 비움
  * `set.size` – 셋에 몇 개의 값이 있는지 세어줌

```
let set = new Set();

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

// 어떤 고객(john, mary)은 여러 번 방문할 수 있음
set.add(john);
set.add(pete);
set.add(mary);
set.add(john);
set.add(mary);

// 셋에는 유일무이한 값만 저장
alert( set.size ); // 3

for (let user of set) {
  alert(user.name); // // John, Pete, Mary 순으로 출력
}
```



### [셋의 값에 반복 작업하기](https://ko.javascript.info/map-set#ref-895)

* `for..of`나 `forEach`를 사용하면 셋의 값을 대상으로 반복 작업을 수행할 수 있음

```
let set = new Set(["oranges", "apples", "bananas"]);

for (let value of set) alert(value);

// forEach를 사용해도 동일하게 동작
set.forEach((value, valueAgain, set) => {
  alert(value);
});
```

*   &#x20;`맵`을 `셋`으로 혹은 `셋`을 `맵`으로 교체하기가 쉽게 3개의 인수 사용(`맵`과의 호환성)


* `셋`에도 `맵`과 마찬가지로 반복 작업을 위한 메소드가 있음
  * `set.keys()` – 셋 내의 모든 값을 포함하는 이터러블 객체를 반환
  * `set.values()` – `set.keys`와 동일한 작업 -> `맵`과의 호환성을 위해 만들어진 메소드
  * `set.entries()` – 셋 내의 각 값을 이용해 만든 `[value, value]` 배열을 포함하는 이터러블 객체를 반환 -> `맵`과의 호환성을 위해 만들어진 메소드 &#x20;
