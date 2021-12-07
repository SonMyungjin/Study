---
description: https://ko.javascript.info/object-copy
---

# 참조에 의한 객체 복사

* 객체와 원시 타입의 근본적인 차이 중 하나는 객체는 ‘참조에 의해(by reference)’ 저장되고 복사
* **변수엔 객체가 그대로 저장되는 것이 아니라, 객체가 저장되어있는 '메모리 주소’인 객체에 대한 '참조 값’이 저장**
* **객체가 할당된 변수를 복사할 땐 객체의 **<mark style="color:red;">**참조 값이 복사**</mark>**되고 객체는 복사되지 않음**

```
let user = { name: "John" };

let admin = user; // 참조값을 복사함
```

![](<../../.gitbook/assets/image (4) (1) (1).png>)



#### 참조에 의한 비교&#x20;

* 객체 비교 시 동등 연산자 `==`와 일치 연산자 `===`는 동일하게 동작
* **비교 시 피연산자인 두 객체가 동일한 객체인 경우에 참을 반환**

```
let a = {};
let b = a; // 참조에 의한 복사

alert( a == b ); // true, 두 변수는 같은 객체를 참조합니다.
alert( a === b ); // true
```

```
let a = {};
let b = {}; // 독립된 두 객체

alert( a == b ); // false
```

* 독립된 객체이기 때문에 일치·동등 비교하면 거짓이 반환



### [객체 복사, 병합과 Object.assign](https://ko.javascript.info/object-copy#ref-809)

* 기존에 있던 객체와 똑같으면서 독립적인 객체를 만들고 싶을 때

```
// 방법 1
let user = {
  name: "John",
  age: 30
};

let clone = {}; // 새로운 빈 객체

// 빈 객체에 user 프로퍼티 전부를 복사해 넣습니다.
for (let key in user) {
  clone[key] = user[key];
}

// 이제 clone은 완전히 독립적인 복제본이 됨
clone.name = "Pete"; // clone의 데이터 변경

alert( user.name ); // 기존 객체에는 여전히 John이 있
```

```
// 방법 2 (Object.assign 사)
let user = { name: "John" };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

// permissions1과 permissions2의 프로퍼티를 user로 복사
Object.assign(user, permissions1, permissions2);

// now user = { name: "John", canView: true, canEdit: true }
```

* **`Object.assign(dest, [src1, src2, src3...])`**
  * 첫 번째 인수 `dest`는 목표로 하는 객체
  * 이어지는 인수 `src1, ..., srcN`는 복사하고자 하는 객체
  * 객체 `src1, ..., srcN`의 프로퍼티를 `dest`에 복사
  * 마지막으로 `dest`를 반환
  * 중첩 객체 처리  X  -> 깊은 복사(deep cloning)가 가능한 <mark style="color:red;">**`.clonDeep(obj`**</mark><mark style="color:red;">`)`</mark> 사용
