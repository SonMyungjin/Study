---
description: https://ko.javascript.info/settimeout-setinterval
---

# setTimeout과 setInterval을 이용한 호출 스케줄링

* 호출 스케줄링(scheduling a call)
  * 일정 시간이 지난 후에 원하는 함수를 예약 실행(호출)할 수 있게 하는 것&#x20;
  * 종류
    * `setTimeout`을 이용해 일정 시간이 지난 후에 함수를 실행하는 방법
    * `setInterval`을 이용해 일정 시간 간격을 두고 함수를 실행하는 방법



### [setTimeout](https://ko.javascript.info/settimeout-setinterval#ref-1108)

```
// 기본 문법 
let timerId = setTimeout(func|code, [delay], [arg1], [arg2], ...)
```

*   `func|code`

    * 실행하고자 하는 코드로, 함수 또는 문자열 형태로 대개는 이 자리에 함수가 들어감
    * 하위 호환성을 위해 문자열도 받을 수 있게 해놓았지만 추천하진 않음


*   `delay`

    * 실행 전 대기 시간으로, 단위는 밀리초(millisecond, 1000밀리초 = 1초)이며 기본값은 0


* `arg1`, `arg2`…
  * 함수에 전달할 인수들로, IE9 이하에선 지원하지 않음 &#x20;

```
function sayHi(who, phrase) {
  alert( who + ' 님, ' + phrase );
}

setTimeout(sayHi, 1000, "홍길동", "안녕하세요."); // 홍길동 님, 안녕하세요.
```



#### [clearTimeout으로 스케줄링 취소하기](https://ko.javascript.info/settimeout-setinterval#ref-1109)

* `setTimeout`을 호출하면 '타이머 식별자(timer identifier)'가 반환
* 스케줄링을 취소하고 싶을 땐 이 식별자(아래 예시에서 `timerId`)를 사용하면 됨 &#x20;

```
let timerId = setTimeout(...);
clearTimeout(timerId);
```



### [setInterval](https://ko.javascript.info/settimeout-setinterval#ref-1110)

* `setInterval` 메소드는 `setTimeout`과 동일한 문법을 사용

```
// 기본 문
let timerId = setInterval(func|code, [delay], [arg1], [arg2], ...)
```

* `setTimeout`이 함수를 단 한 번만 실행하는 것과 달리,
* `setInterval`은 함수를 주기적으로 실행하게 만듦
* 함수 호출을 중단하려면 `clearInterval(timerId)`을 사용하면 됨 &#x20;

```
// 2초 간격으로 메시지를 보여줌
let timerId = setInterval(() => alert('째깍'), 2000);

// 5초 후에 정지
setTimeout(() => { clearInterval(timerId); alert('정지'); }, 5000);
```

