---
description: https://ko.javascript.info/closure
---

# 변수의 유효범위와 클로저

### [코드 블록](https://ko.javascript.info/closure#ref-513)

* 코드 블록 `{...}` 안에서 선언한 변수는 블록 안에서만 사용할 수 있음  &#x20;

```
{
  // 지역 변수를 선언하고 몇 가지 조작을 했지만 그 결과를 밖에서 볼 수 없음

  let message = "안녕하세요."; // 블록 내에서만 변숫값을 얻을 수 있음  

  alert(message); // 안녕하세요.
}

alert(message); // ReferenceError: message is not defined
```



* `if`, `for`, `while` 에서도 마찬가지로 `{...}` 안에서 선언한 변수는 오직 블록 안에서만 접근 가능

```
if (true) {
  let phrase = "안녕하세요!";

  alert(phrase); // 안녕하세요!
}

alert(phrase); // ReferenceError: phrase is not defined
```



### [중첩 함수](https://ko.javascript.info/closure#ref-514)

* <mark style="color:orange;">**함수 내부에서 선언한 함수**</mark>는 ‘중첩(nested)’ 함수라고 부름

```
function sayHiBye(firstName, lastName) {

  // 헬퍼(helper) 중첩 함수
  function getFullName() {
    return firstName + " " + lastName;
  }

  alert( "Hello, " + getFullName() );
  alert( "Bye, " + getFullName() );

}
```



### [렉시컬 환경](https://ko.javascript.info/closure#ref-515)

#### [단계 1. 변수](https://ko.javascript.info/closure#ref-516)

*   자바스크립트에서 실행 중인 함수, 코드 블록 `{...}`, 스크립트 전체는 _**렉시컬 환경(Lexical Environment)**_ 이라 불리는 <mark style="color:orange;">**내부 숨김 연관 객체(internal hidden associated object)**</mark>를 가짐


*   렉시컬 환경 객체는 두 부분으로 구성

    1. _**환경 레코드(Environment Record)**_ – 모든 지역 변수를 프로퍼티로 저장하고 있는 객체                          `this` 값과 같은 기타 정보도 여기에 저장
    2. _**외부 렉시컬 환경(Outer Lexical Environment)**_** 에 대한 참조** – 외부 코드와 연관됨


* **’변수’는 특수 내부 객체인 `환경 레코드`의 프로퍼티일 뿐**
  * **'변수를 가져오거나 변경’하는 것은 '환경 레코드의 프로퍼티를 가져오거나 변경’함을 의미**



![](<../../.gitbook/assets/image (9) (1) (1) (1).png>)

* 위 코드에는 렉시컬 환경이 하나만 존재
* 이렇게 스크립트 전체와 관련된 렉시컬 환경은 전역 렉시컬 환경(global Lexical Environment)이라 함
* 위 그림에서 네모 상자는 변수가 저장되는 환경 레코드를 나타내고,
* 붉은 화살표는 외부 렉시컬 환경에 대한 참조를 나타냄
* 전역 렉시컬 환경은 외부 참조를 갖지 않기 때문에 화살표가 `null`을 가리키는 걸 확인할 수 있음 &#x20;



![](<../../.gitbook/assets/image (1) (1) (1) (1).png>)

* 코드가 실행되고 실행 흐름이 이어져 나가면서 **렉시컬 환경은 변화**
*   우측의 네모 상자는 코드가 한 줄, 한 줄 실행될 때마다 전역 렉시컬 환경이 어떻게 변화하는지 보여줌

    1. 스크립트가 시작되면 스크립트 내에서 선언한 변수 전체가 렉시컬 환경에 올라감(pre-populated)
       * 이때 변수의 상태는 특수 내부 상태(special internal state)인 'uninitialized’가 됨
       * 자바스크립트 엔진은 uninitialized 상태의 변수를 인지하긴 하지만,&#x20;
       * `let`을 만나기 전까진 이 변수를 참조할 수 없음
    2. `let phrase` -> 아직 값을 할당하기 전이기 때문에 프로퍼티 값은 `undefined` -> `phrase`는 이 시점 이후부터 사용할 수 있음
    3. `phrase`에 값이 할당
    4. `phrase`의 값이 변경



{% hint style="info" %}
**렉시컬 환경은 명세서에만 존재**

* '렉시컬 환경’은 명세서에서 자바스크립트가 어떻게 동작하는지 설명하는 데 쓰이는 ‘이론상의’ 객체
* 따라서 코드를 사용해 직접 렉시컬 환경을 얻거나 조작하는 것은 불가능
{% endhint %}



#### [단계 2. 함수 선언문](https://ko.javascript.info/closure#ref-517)

* 함수는 변수와 마찬가지로 값
* **다만 함수 선언문(function declaration)으로 선언한 함수는 일반 변수와는 달리 바로 **<mark style="color:orange;">**초기화**</mark>**된다는 점에서 차이가 있음**
* 함수 선언문으로 선언한 함수는 렉시컬 환경이 만들어지는 즉시 사용할 수 있음 -> 함수 표현식은 X &#x20;

![](<../../.gitbook/assets/image (7) (1) (1) (1).png>)

#### [단계 3. 내부와 외부 렉시컬 환경](https://ko.javascript.info/closure#ref-518)

* 함수를 호출해 실행하면 새로운 렉시컬 환경이 자동으로 만들어짐
* 렉시컬 환경에는 함수 호출 시 넘겨받은 **매개변수**와 **함수의 지역 변수**가 저장

![](<../../.gitbook/assets/image (10) (1) (1) (1) (1).png>)

* 함수가 호출 중인 동안엔 호출 중인 함수를 위한 **내부 렉시컬 환경**과 내부 렉시컬 환경이 가리키는 **외부 렉시컬 환경**을 갖게됨
  * 예시의 내부 렉시컬 환경은 현재 실행 중인 함수인 `say`에 상응함&#x20;
    * `say("John")`을 호출했기 때문에, `name`의 값은 `"John"`이 됨
  *   예시의 외부 렉시컬 환경은 전역 렉시컬 환경

      * 전역 렉시컬 환경은 `phrase`와 함수 `say`를 프로퍼티로 가짐


* **코드에서 변수에 접근할 땐, 먼저 내부 렉시컬 환경을 검색 범위로 잡음**
* **내부 렉시컬 환경에서 원하는 변수를 찾지 못하면 검색 범위를 내부 렉시컬 환경이 참조하는 외부 렉시컬 환경으로 확장**
*   **이 과정은 검색 범위가 전역 렉시컬 환경으로 확장될 때까지 반복**

    ****

![](<../../.gitbook/assets/image (12) (1) (1) (1) (1).png>)



* 함수 `say` 내부의 `alert`에서 변수 `name`에 접근할 땐, 먼저 내부 렉시컬 환경을 살펴보고,&#x20;
* 내부 렉시컬 환경에서 변수 `name`을 찾음
* `alert`에서 변수 `phrase`에 접근 -> `phrase`에 상응하는 프로퍼티가 내부 렉시컬 환경엔 없음&#x20;
* 따라서, 검색 범위는 외부 렉시컬 환경으로 확장 -> 외부 렉시컬 환경에서 `phrase`를 찾음



#### [단계 4. 함수를 반환하는 함수](https://ko.javascript.info/closure#ref-519)

![](<../../.gitbook/assets/image (8) (1) (1) (1).png>)

* `makeCounter()`를 호출하면 두 개의 렉시컬 환경이 만들어짐
*   현재는 중첩함수가 생성되기만 하고 실행은 되지 않은 상태


*   모든 함수는 함수가 생성된 곳의 렉시컬 환경을 기억함

    * 함수는 `[[Environment]]`라 불리는 숨김 프로퍼티를 갖는데,&#x20;
    * 여기에 함수가 만들어진 곳의 렉시컬 환경에 대한 참조가 저장됨



![](<../../.gitbook/assets/image (6) (1) (1).png>)

* `counter.[[Environment]]`엔 `{count: 0}`이 있는 렉시컬 환경에 대한 참조가 저장
* 호출 장소와 상관없이 함수가 자신이 태어난 곳을 기억할 수 있는 건 바로 `[[Environment]]` 프로퍼티 덕분
* `[[Environment]]`는 함수가 생성될 때 딱 한 번 값이 세팅되고 영원히 변하지 않음  &#x20;
* `counter()`를 호출하면 각 호출마다 새로운 렉시컬 환경이 생성
* 그리고 이 렉시컬 환경은 `counter.[[Environment]]`에 저장된 렉시컬 환경을 외부 렉시컬 환경으로서 참조



![](<../../.gitbook/assets/image (14) (1) (1) (1).png>)

* 실행 흐름이 중첩 함수의 본문으로 넘어오면 `count` 변수가 필요한데, 먼저 자체 렉시컬 환경에서 변수를 찾음
* 익명 중첩 함수엔 지역변수가 없기 때문에 이 렉시컬 환경은 비어있는 상황(`<empty>`)
* `counter()`의 렉시컬 환경이 참조하는 외부 렉시컬 환경에서 `count`를 찾음
* &#x20;`count++`가 실행되면서 count 값이 1 증가해야하는데, **변숫값 갱신은 변수가 저장된 렉시컬 환경에서 이루어짐** &#x20;



![](<../../.gitbook/assets/image (7) (1) (1).png>)

* 실행이 종료된 후의 상태로  `counter()`를 여러 번 호출하면 `count` 변수가 `2`, `3`으로 증가



### <mark style="color:blue;">클로저</mark>

* 외부 변수를 기억하고 이 외부 변수에 접근할 수 있는 함수를 의미 &#x20;
* 몇몇 언어에선 클로저를 구현하는 게 불가능하거나 특수한 방식으로 함수를 작성해야 클로저를 만들 수 있음&#x20;
*   하지만, 자바스크립트에선 모든 함수가 자연스럽게 클로저가 됨


* 자바스크립트의 함수는 숨김 프로퍼티인 `[[Environment]]`를 이용해 자신이 어디서 만들어졌는지를 기억
* 함수 본문에선 `[[Environment]]`를 사용해 외부 변수에 접근

