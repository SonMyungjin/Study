---
description: https://ko.javascript.info/arrow-functions
---

# 화살표 함수 다시 살펴보기

### [화살표 함수에는 'this’가 없습니다](https://ko.javascript.info/arrow-functions#ref-2023)

* 화살표 함수 본문에서 `this`에 접근하면, 외부에서 값을 가져옴&#x20;
* 객체의 메소드(`showList()`) 안에서 동일 객체의 프로퍼티(`students`)를 대상으로 순회를 하는 데 사용할 수 있음

```
let group = {
  title: "1모둠",
  students: ["보라", "호진", "지민"],

  showList() {
    this.students.forEach(
      student => alert(this.title + ': ' + student)
    );
  }
};

group.showList();
```

* `forEach`에서 화살표 함수를 사용했기 때문에 화살표 함수 본문에 있는 `this.title`은 화살표 함수 바깥에 있는 메소드인 `showList`가 가리키는 대상과 동일해짐
* 즉, `this.title`은 `group.title`과 같아짐



{% hint style="info" %}
화살표 함수는 `new`와 함께 실행할 수 없음

* `this`가 없기 때문에 화살표 함수는 생성자 함수로 사용할 수 없다는 제약이 있음
* 화살표 함수는 `new`와 함께 호출할 수 없
{% endhint %}

