---
description: https://ko.javascript.info/switch
---

# switch문

* 복수의 `if` 조건문은 `switch`문으로 바꿀 수 있음



### [문법](https://ko.javascript.info/switch#ref-875)

```
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]

  case 'value2':  // if (x === 'value2')
    ...
    [break]

  default:
    ...
    [break]
}
```



### [여러 개의 "case"문 묶기](https://ko.javascript.info/switch#ref-877)

```
let a = 3;

switch (a) {
  case 4:
    alert('계산이 맞습니다!');
    break;

  case 3: // (*) 두 case문을 묶음
  case 5:
    alert('계산이 틀립니다!');
    alert("수학 수업을 다시 들어보는걸 권유 드립니다.");
    break;

  default:
    alert('계산 결과가 이상하네요.');
}
```

* `case 3`과 `case 5`는 동일한 메시지를 보여줌 \
