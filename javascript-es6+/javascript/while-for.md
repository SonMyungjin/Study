---
description: https://ko.javascript.info/while-for
---

# while과 for 반복문

### [‘while’ 반복문](https://ko.javascript.info/while-for#ref-900)

```
while (condition) {
// 코드 
// '반복문 본문(body)'이라 불림 
}

// ex)
let i = 3;
while (i) { // i가 0이 되면 조건이 falsy가 되므로 반복문이 멈
  alert( i );
  i--;
}
```

* `condition`(조건)이 truthy 이면 반복문 본문의 `코드`가 실행

{% hint style="info" %}
본문이 한 줄이면 대괄호를 쓰지 않아도 됨

* 반복문 본문이 한 줄짜리 문이라면 대괄호 `{…}`를 생략할 수 있음
* let i = 3;

&#x20;     while (i) alert(i--);
{% endhint %}



### [‘do…while’ 반복문](https://ko.javascript.info/while-for#ref-901)

* `do..while` 문법을 사용하면 `condition`을 반복문 본문 _아래_로 옮길 수 있
* 본문이 먼저 실행되고, 조건을 확인한 후 조건이 truthy인 동안엔 본문이 계속 실행

```
do {
  // 반복문 본문
} while (condition);

// ex)
let i = 0;
do {
  alert( i );
  i++;
} while (i < 3);
```

* `do..while` 문법은 조건이 truthy 인지 아닌지에 상관없이, 본문을 **최소한 한번**이라도 실행하고 싶을 때만 사용



### [‘for’ 반복문](https://ko.javascript.info/while-for#ref-902)

```
for (begin; condition; step) {
// ... 반복문 본문 ... 
}

// ex)
for (let i = 0; i < 3; i++) { // 0, 1, 2 출력
  alert(i);
}
```

* for 구성 요소

|        begin        |                             condition                            |              body             |          step          |
| :-----------------: | :--------------------------------------------------------------: | :---------------------------: | :--------------------: |
|        i = 0        |                               i < 3                              |            alert(i)           |           i++          |
| 반복문에 진입할 때 단 한 번 실행 | <ul><li>반복마다 해당 조건이 확인</li></ul><ul><li>false이면 반복문을 멈</li></ul> | condition이 truthy일 동안 계속해서 실행 | 각 반복의 body가 실행된 이후에 실행 |

&#x20;

### [반복문 빠져나오기](https://ko.javascript.info/while-for#ref-904)

* `break`를 사용하면 언제든 원하는 때에 반복문을 빠져나올 수 있음

```
let sum = 0;

while (true) {

  let value = +prompt("숫자를 입력하세요.", '');

  if (!value) break;

  sum += value;

}
alert( '합계: ' + sum );
```



### [다음 반복으로 넘어가기](https://ko.javascript.info/while-for#continue)

* `continue`는 현재 반복을 종료시키고 다음 반복으로 넘어가고 싶을 때 사용

```
for (let i = 0; i < 10; i++) {

  // 조건이 참이라면 남아있는 본문은 실행되지 않습니다.
  if (i % 2 == 0) continue;

  alert(i); // 1, 3, 5, 7, 9가 차례대로 출력됨
}
```

{% hint style="info" %}
‘?’ 오른쪽엔 `break`나 `continue`가 올 수 없음

* 표현식이 아닌 문법 구조(syntax construct)는 삼항 연산자 `?`에 사용할 수 없음
* `break`나 `continue` 같은 지시자는 삼항 연산자에 사용 X
{% endhint %}



### [break/continue와 레이블](https://ko.javascript.info/while-for#ref-905)

* 여러 개의 중첩 반복문을 한 번에 빠져나와야 하는 경우 <mark style="color:orange;">**레이블(label)**</mark> <mark style="color:orange;"></mark><mark style="color:orange;"></mark> 사용

```
outer: for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`(${i},${j})의 값`, '');

    // 사용자가 아무것도 입력하지 않거나 Cancel 버튼을 누르면 두 반복문 모두를 빠져나옴
    if (!input) break outer; // outer라는 레이블이 붙은 반복문을 찾고, 해당 반복문 빠져 나   

    // 입력받은 값을 가지고 무언가를 함
  }
}
alert('완료!');
```

