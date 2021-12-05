---
description: https://ko.javascript.info/constructor-new
---

# new 연산자와 생성자 함수

* 개발을 하다 보면 유사한 객체를 여러 개 만들어야 할 때가 생기곤 함
  * 복수의 사용자, 메뉴 내 다양한 아이템을 객체로 표현하려고 하는 경우
* `'new'` 연산자와 생성자 함수를 사용하면 유사한 객체 여러 개를 쉽게 만들 수 있음



### [생성자 함수](https://ko.javascript.info/constructor-new#ref-1039)

* 생성자 함수(constructor function)와 일반 함수에 기술적인 차이는 없음 -> 두 관례를 따름

1. 함수 이름의 첫 글자는 대문자로 시작
2. 반드시 `'new'` 연산자를 붙여 실행

```
function User(name) {
  // 1. this = {};  (빈 객체가 암시적으로 만들어짐)
  
  // 2. 새로운 프로퍼티를 this에 추가
  this.name = name;
  this.isAdmin = false;
  
 // 3. return this; (this가 암시적으로 반환됨)

}

let user = new User("보라");

alert(user.name); // 보라
alert(user.isAdmin); // false
```

* `new User(...)`를 써서 함수를 실행하면 아래와 같은 알고리즘이 동작

1. 빈 객체를 만들어 `this`에 할당
2. 함수 본문을 실행합니다. `this`에 새로운 프로퍼티를 추가해 `this`를 수정
3. `this`를 반환

* 생성자의 의의
  * <mark style="color:orange;">재사용할 수 있는 객체 생성 코드를 구현</mark>

<mark style="color:orange;"></mark>
