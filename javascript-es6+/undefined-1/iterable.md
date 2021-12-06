---
description: https://ko.javascript.info/iterable
---

# iterable 객체

* _<mark style="color:orange;">**반복 가능한(iterable, 이터러블)**</mark>_<mark style="color:orange;">** **</mark><mark style="color:orange;">**객체**</mark> : 배열을 일반화한 객체
* 이터러블 이라는 개념을 사용하면 어떤 객체에든 `for..of` 반복문을 적용할 수 있음
* 배열은 대표적인 이터러블
  * 배열 외에도 다수의 내장 객체가 반복 가능
  * 문자열 역시 이터러블의 대표적인 예



### [Symbol.iterator](https://ko.javascript.info/iterable#ref-1153)

```
let range = {
  from: 1,
  to: 5
};

// 아래와 같이 for..of가 동작할 수 있도록 하는 게 목표
// for(let num of range) ... num=1,2,3,4,5
```

*   `range`를 이터러블로 만들려면(`for..of`가 동작하도록 하려면) 객체에

    * `Symbol.iterator`(특수 내장 심볼)라는 메서드를 추가해 아래와 같은 일이 벌어지도록 해야함


*   `for..of`가 시작되자마자 `for..of`는 `Symbol.iterator`를 호출

    * `Symbol.iterator`가 없으면 에러 발생
    * `Symbol.iterator`는 반드시 _이터레이터(iterator, 메서드 `next`가 있는 객체)_ 를 반환해야 함


*   이후 `for..of`는 _반환된 객체(이터레이터)만_을 대상으로 동작


*   `for..of`에 다음 값이 필요하면, `for..of`는 이터레이터의 `next()`메서드를 호출


* `next()`의 반환 값은 `{done: Boolean, value: any}`와 같은 형태이어야 함
  * `done=true`는 반복이 종료되었음을 의미
  * `done=false`일땐 `value`에 다음 값이 저장



* `range`를 반복 가능한 객체로 만들어주는 코드

```
let range = {
  from: 1,
  to: 5
};

// 1. for..of 최초 호출 시, Symbol.iterator가 호출
range[Symbol.iterator] = function() {

  // Symbol.iterator는 이터레이터 객체를 반환
  // 2. 이후 for..of는 반환된 이터레이터 객체만을 대상으로 동작하는데, 이때 다음 값도 정해
  return {
    current: this.from,
    last: this.to,

    // 3. for..of 반복문에 의해 반복마다 next()가 호출
    next() {
      // 4. next()는 값을 객체 {done:.., value :...}형태로 반환해야 합니다.
      if (this.current <= this.last) {
        return { done: false, value: this.current++ };
      } else {
        return { done: true };
      }
    }
  };
};

// 이제 의도한 대로 동작
for (let num of range) {
  alert(num); // 1, then 2, 3, 4, 5
}
```



* 이터러블 객체의 핵심은 '관심사의 분리(Separation of concern, SoC)'에 있음
  * `range`엔 메서드 `next()`가 없음
  * 대신 `range[Symbol.iterator]()`를 호출해서 만든 ‘이터레이터’ 객체와 이 객체의 메서드 `next()`에서 반복에 사용될 값을 만들어냄
* 이렇게 하면 이터레이터 객체와 반복 대상인 객체를 분리할 수 있
* 이터레이터 객체와 반복 대상 객체를 합쳐서 `range` 자체를 이터레이터로 만들면 코드가 더 간단해

```
let range = {
  from: 1,
  to: 5,

  [Symbol.iterator]() {
    this.current = this.from;
    return this;
  },

  next() {
    if (this.current <= this.to) {
      return { done: false, value: this.current++ };
    } else {
      return { done: true };
    }
  }
};

for (let num of range) {
  alert(num); // 1, then 2, 3, 4, 5
}
```



### [문자열은 이터러블](https://ko.javascript.info/iterable#ref-1154)

* 배열과 문자열은 가장 광범위하게 쓰이는 내장 이터러블
* `for..of`는 문자열의 각 글자를 순회

```
for (let char of "test") {
  // 글자 하나당 한 번 실행(4회 호출).
  alert( char ); // t, e, s, t가 차례대로 출력됨
}
```

