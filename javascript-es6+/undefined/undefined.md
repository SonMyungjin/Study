---
description: https://ko.javascript.info/object
---

# 객체

## <mark style="color:blue;">객체</mark>

* 객체형은 원시형과 달리 다양한 데이터를 담을 수 있음
* 키로 구분된 데이터 집합이나 복잡한 개체(entity)를 저장할 수 있음
* 객체는 자바스크립트 거의 모든 면에 녹아있는 개념



#### 객체 만드는 법

* 객체는 중괄호 `{…}`를 이용해 만들 수 있음
* 중괄호 안에는 ‘<mark style="color:orange;">**키(key): 값(value)**</mark>’ 쌍으로 구성된 _<mark style="color:red;">**프로퍼티(property)**</mark>_ 를 여러 개 넣을 수 있는데,&#x20;
  * `키`엔 문자형, `값`엔 모든 자료형이 허용
  * 프로퍼티 키는 ‘프로퍼티 이름’ 이라고도 부름 &#x20;

```
let user = new Object(); // '객체 생성자' 문법
let user = {};  // '객체 리터럴' 문법
```

* 중괄호 `{...}`를 이용해 객체를 선언하는 것을 _<mark style="color:red;">**객체 리터럴(object literal)**</mark>_ 이라고 부름&#x20;
* 객체를 선언할 땐 주로 이 방법을 사용



### [리터럴과 프로퍼티](https://ko.javascript.info/object#ref-410)

```
let user = {     // 객체
  name: "John",  // 키: "name",  값: "John"
  age: 30        // 키: "age", 값: 30
};
```

* `'콜론(:)'`을 기준으로 왼쪽엔 키가, 오른쪽엔 값이 위치
* 프로퍼티 키는 프로퍼티 ‘이름’ 혹은 '식별자’라고도 부름



* 객체 `user`에는 프로퍼티가 두 개 있음

1. 첫 번째 프로퍼티 – `"name"`(이름)과 `"John"`(값)
2. 두 번째 프로퍼티 – `"age"`(이름)과 `30`(값)



* 서랍장(객체 `user`) 안에 파일 두 개(프로퍼티 두 개)가 담겨있는데,&#x20;
* 각 파일에 “name”, "age"라는 이름표가 붙어있다고 생각하면 쉬움



```
let user = {
  name: "John",
  age: 30,
}
```

* 마지막 프로퍼티 끝은 쉼표로 끝날 수 있음!
* 이런 쉼표를 ‘trailing(길게 늘어지는)’ 혹은 ‘hanging(매달리는)’ 쉼표라고 부름
* 이렇게 끝에 쉼표를 붙이면 모든 프로퍼티가 유사한 형태를 보이기 때문에 프로퍼티를 추가, 삭제, 이동하는 게 쉬워짐

{% hint style="info" %}
상수 객체는 수정될 수 있음

* `const`로 선언된 객체는 수정될 수 있음
* const user = { name: "John" }; -> const는 user의 값을 고정하지만, 그 내용은 고정X  &#x20;
{% endhint %}



### [대괄호 표기법](https://ko.javascript.info/object#ref-411)

* 키가 유효한 변수 식별자가 아닌 경우엔 점 표기법 대신에
  * '<mark style="color:orange;">**대괄호 표기법(square bracket notation)**</mark>' 방법을 사용&#x20;
* 대괄호 표기법은 키에 어떤 문자열이 있던지 상관없이 동작

```
let user = {};

// set
user["likes birds"] = true;

// get
alert(user["likes birds"]); // true

// delete
delete user["likes birds"];
```



#### 계산된 프로퍼티

* 객체를 만들 때 객체 리터럴 안의 프로퍼티 키가 대괄호로 둘러싸여 있는 경우를 말함

```
let fruit = prompt("어떤 과일을 구매하시겠습니까?", "apple");
let bag = {};

// 변수 fruit을 사용해 프로퍼티 이름을 만들었음
bag[fruit] = 5;
```

* 사용자가 프롬프트 대화상자에 `apple`을 입력했다면 `bag`에는 `{apple: 5}`가 할당

{% hint style="info" %}
프로퍼티 이름이 확정된 상황이고, 단순한 이름이라면 처음엔 점 표기법을 사용하다가 뭔가 복잡한 상황이 발생했을 때 대괄호 표기법으로 바꾸는 경우가 많음
{% endhint %}



### [단축 프로퍼티](https://ko.javascript.info/object#ref-413)

* 프로퍼티들은 이름과 값이 변수의 이름과 동일할 때&#x20;
  * _프로퍼티 값 단축 구문(property value shorthand)_ 을 사용하면 코드를 짧게 줄일 수 있음

```
function makeUser(name, age) {
  return {
    name, // name: name 과 같음
    age,  // age: age 와 같음
    // ...
  };
}
```



### [프로퍼티 이름의 제약사항](https://ko.javascript.info/object#ref-414)

* 변수 이름(키)엔 ‘for’, ‘let’, ‘return’ 같은 예약어를 사용하면 안됨
* But, 객체 프로퍼티엔 이런 제약이 없음!

```
// 예약어를 키로 사용해도 괜찮음
let obj = {
  for: 1,
  let: 2,
  return: 3
};

alert( obj.for + obj.let + obj.return );  // 6
```



### [‘in’ 연산자로 프로퍼티 존재 여부 확인하기](https://ko.javascript.info/object#ref-415)

* 자바스크립트 객체의 중요한 특징 중 하나는 다른 언어와는 달리,&#x20;
* 존재하지 않는 프로퍼티에 접근하려 해도 에러가 발생하지 않고 `undefined`를 반환

```
let user = { name: "John", age: 30 };

alert( "age" in user ); // user.age가 존재하므로 true 출력
alert( "blabla" in user ); // user.blabla는 존재하지 않기 때문에 false 출력
```



### [‘for…in’ 반복문](https://ko.javascript.info/object#ref-416)

* `for..in` 반복문을 사용하면 객체의 모든 키를 순회할 수 있음

```
for (key in object) {
  // 각 프로퍼티 키(key)를 이용하여 본문(body)을 실행
}
```

* 예시

```
let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

for (let key in user) {
  // 키
  alert( key );  // name, age, isAdmin
  // 키에 해당하는 값
  alert( user[key] ); // John, 30, true
}
```

