# 화살표 함수

* 화살표 함수 : 함수 표현식보다 단순하고 간결한 문법으로 함수를 만들 수 있는 방법

```
let func = function(arg1, arg2, ...argN) {
  return expression;
};

// (==)

let func = (arg1, arg2, ...argN) => expression
```



### [본문이 여러 줄인 화살표 함수](https://ko.javascript.info/arrow-functions-basics#ref-213)

* 평가해야 할 표현식이나 구문이 여러 개인 함수가 있을 수도 있음
  * 화살표 함수 문법을 사용해 함수를 만들 수 있지만, 중괄호 안에 평가해야 할 코드를 넣어주어야 함

```
let sum = (a, b) => {  // 중괄호는 본문 여러 줄로 구성되어 있음을 알려줌
  let result = a + b;
  return result; // 중괄호를 사용했다면, return 지시자로 결괏값을 반환해주어야 함
};

alert( sum(1, 2) ); // 3
```

