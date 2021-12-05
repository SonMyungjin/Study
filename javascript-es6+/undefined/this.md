---
description: https://ko.javascript.info/object-methods
---

# 메소드와 this

* 자바스크립트에서는 객체의 프로퍼티에 함수를 할당해 객체에게 행동할 수 있는 능력을 부여함
* <mark style="color:orange;">**객체 프로퍼티에 저장된 함수**</mark>를 '<mark style="color:red;">**메소드**</mark>’라고 부름



### [메소드 만들기](https://ko.javascript.info/object-methods#ref-760)

```
let user = {
  name: "John",
  age: 30
};

user.sayHi = function() {
  alert("안녕하세요!");
};

user.sayHi(); // 안녕하세요!
```

* 함수 표현식으로 함수를 만들고, 객체 프로퍼티 `user.sayHi`에 함수를 할당

{% hint style="info" %}
객체 지향 프로그래밍(OOP)

* 객체를 사용하여 개체를 표현하는 방식을 [객체 지향 프로그래밍(object-oriented programming, OOP)](https://en.wikipedia.org/wiki/Object-oriented\_programming) 이라 부름.
* 올바른 개체를 선택하는 방법, 개체 사이의 상호작용을 나타내는 방법 등에 관한 의사결정은 객체 지향 설계를 기반으로 이루어짐
{% endhint %}



#### 메소드 단축 구문&#x20;

```
// 아래 두 객체는 동일하게 동작

user = {
  sayHi: function() {
    alert("Hello");
  }
};

user = {
  sayHi() { // "sayHi: function()"과 동일
    alert("Hello");
  }
};
```

* `function`을 생략해도 메서드를 정의할 수 있



### [메소드와 this](https://ko.javascript.info/object-methods#ref-762)

* 메소드는 객체에 저장된 정보에 접근할 수 있어야 제 역할을 할 수 있음
* 모든 메서드가 그런 건 아니지만, 대부분의 메서드가 객체 프로퍼티의 값을 활용
* `user.sayHi()`의 내부 코드에서 객체 `user`에 저장된 이름(name)을 이용해 인사말을 만드는 경우가 이런 경우에 속함
* **메소드 내부에서 `this` 키워드를 사용하면 객체에 접근할 수 있습니다.**
* 이때 '점 앞’의 `this`는 객체를 나타냄 -> 정확히는 메서드를 호출할 때 사용된 객체를 나타냄

```
let user = {
  name: "John",
  age: 30,

  sayHi() {
    // 'this'는 '현재 객체'를 나타냅니다.
    alert(this.name);
  }

};

user.sayHi(); // John
```

* `user.sayHi()`가 실행되는 동안에 `this`는 `user`를 나타냄



### [자유로운 this](https://ko.javascript.info/object-methods#ref-763)

* 자바스크립트의 `this`는 다른 프로그래밍 언어의 `this`와 동작 방식이 다름
* 자바스크립트에선 모든 함수에 `this`를 사용할 수 있음

```
function sayHi() {
  alert( this.name ); // 문법 에러 X 
}
```

* `this` 값은 런타임에 결정 -> 컨텍스트에 따라 달라짐
* 동일한 함수라도 다른 객체에서 호출했다면 'this’가 참조하는 값이 달라짐

```
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert( this.name );
}

// 별개의 객체에서 동일한 함수를 사용함
user.f = sayHi;
admin.f = sayHi;

// 'this'는 '점(.) 앞의' 객체를 참조하기 때문에
// this 값이 달라짐
user.f(); // John  (this == user)
admin.f(); // Admin  (this == admin)

admin['f'](); // Admin (점과 대괄호는 동일하게 동작함)
```



### [this가 없는 화살표 함수](https://ko.javascript.info/object-methods#ref-764)

* 화살표 함수는 일반 함수와는 달리 <mark style="color:orange;">**‘고유한’**</mark><mark style="color:orange;">** **</mark><mark style="color:orange;">**`this`**</mark><mark style="color:orange;">**를 가지지 않음**</mark>
* 화살표 함수에서 `this`를 참조하면, 화살표 함수가 아닌 ‘평범한’ 외부 함수에서 `this` 값을 가져옴
* 아래 예시에서 함수 `arrow()`의 `this`는 외부 함수 `user.sayHi()`의 `this`가 됨

```
let user = {
  firstName: "보라",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // 보라
```

* 별개의 `this`가 만들어지는 건 원하지 않고, 외부 컨텍스트에 있는 `this`를 이용하고 싶은 경우 화살표 함수가 유용
*
