# 변수와 상수

### <mark style="color:blue;">변수</mark>

* 데이터를저장할 때 쓰이는 '이름이 붙은 저장소'
* `let` 키워드를 사용해 변수를 생성  &#x20;

```jsx
let message;

message = 'Hello'; // 문자열을 저장
```

![](<../../.gitbook/assets/image (2) (1) (1).png>) `message`라는 이름표가 붙어있는 상자에 `"Hello!"`라는 값을 저장



#### 변수 명명 규칙

* 변수명에는 오직 문자와 숫자, 그리고 기호 `$`와 `_`만 들어갈 수 있음
* 첫 글자는 숫자가 될 수 없음 &#x20;

{% hint style="info" %}
예약어

* [예약어(reserved name) 목록](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical\_grammar#Keywords)에 있는 단어는 변수명으로 사용할 수 없음
* 예약어 예시: `let`, `class`, `return`, `function`
* 위 코드는 문법 에러를 발생
{% endhint %}



### <mark style="color:blue;">상수</mark>

* 변화하지 않는 변수를 선언할 땐, `let` 대신 `const`를 사용
* 상수는 재할당할 수 없으므로 상수를 변경하려고 하면 에러가 발생

```
const myBirthday = '1995.12.20';

myBirthday = '1996.12.20'; // error, can't reassign the constant!
```



#### 대문자 상수&#x20;

* 기억하기 힘든 값을 변수에 할당해 별칭으로 사용하는 것은 널리 사용되는 관습
* 코드가 실행되기 전에 <mark style="background-color:orange;">이미 그 값을 알고 있는 상수</mark>는 <mark style="color:orange;">대문자와 밑줄로 구성된 이름</mark>으로 명명

```
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";
const COLOR_ORANGE = "#FF7F00";

// 색상을 고르고 싶을 때 별칭을 사용할 수 있게 됨  
let color = COLOR_ORANGE;
alert(color); // #FF7F00
```



