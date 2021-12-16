---
description: https://ko.javascript.info/recursion
---

# 재귀와 스택

* 재귀
  * 큰 목표 작업 하나를 동일하면서 간단한 작업 여러 개로 나눌 수 있을 때 유용한 프로그래밍 패턴
  * 함수가 _자기 자신_을 호출



### [두 가지 사고방식](https://ko.javascript.info/recursion#ref-1095)

* `x`를 `n` 제곱해 주는 함수 `pow(x, n)`

1. 반복적인 사고를 통한 방법: `for` 루프

```
function pow(x, n) {
  let result = 1;

  // 반복문을 돌면서 x를 n번 곱함
  for (let i = 0; i < n; i++) {
    result *= x;
  }

  return result;
}

alert( pow(2, 3) ); // 8
```



2\. 재귀적인 사고를 통한 방법: 작업을 단순화하고 자기 자신을 호출

```
function pow(x, n) {
  if (n == 1) {
    return x;
  } else {
    return x * pow(x, n - 1);
  }
}

alert( pow(2, 3) ); // 8
```

```
              if n==1  = x
             /
pow(x, n) =
             \
              else     = x * pow(x, n - 1)
```

*   `n == 1`일 때

    * 명확한 결괏값을 즉시 도출하므로 이를 _<mark style="color:orange;">**재귀의 베이스(base)**</mark>_ 라고 함


* `n == 1`이 아닐 때
  * `pow(x, n)`은 `x * pow(x, n - 1)`으로 표현할 수 있고,
  * 이를 _<mark style="color:orange;">**재귀 단계(recursive step)**</mark>_ 라고 부름



* 즉, `pow`는 `n == 1`이 될 때까지 _재귀적으로 자신을 호출_
* 함수 호출의 결과가 명확해질 때까지 함수 호출을 더 간단한 함수 호출로 줄일 수 있음



### [재귀적 구조](https://ko.javascript.info/recursion#ref-1102)

* 재귀적으로 정의된 자료구조인 재귀적 자료 구조는 자기 자신의 일부를 복제하는 형태의 자료 구조



#### 연결 리스트&#x20;

* 빠르게 삽입 혹은 삭제를 해야 할 때는 배열 대신 연결 리스트 사용
* _연결 리스트의 요소_
  * `value`
  * `next`: 다음 _연결 리스트 요소_를 참조하는 프로퍼티. 다음 요소가 없을 땐 `null`이 됨

```
let list = {
  value: 1,
  next: {
    value: 2,
    next: {
      value: 3,
      next: {
        value: 4,
        next: null
      }
    }
  }
};

// (==)

let list = { value: 1 };
list.next = { value: 2 };
list.next.next = { value: 3 };
list.next.next.next = { value: 4 };
list.next.next.next.next = null;
```

![](<../../.gitbook/assets/image (4) (1).png>)



* 연결 리스트를 사용하면 전체 리스트를 여러 부분으로 쉽게 나눌 수 있고, 다시 합치는 것도 가능

```
// 연결 리스트 나누기 
let secondList = list.next.next;
list.next.next = null;
```

![](<../../.gitbook/assets/image (11) (1) (1).png>)



```
// 연결 리스트 합치기 
list.next.next = secondList;
```



* 연결 리스트는 요소를 추가하거나 삭제할 수 있음
  * &#x20;리스트의 처음 객체를 바꾸면 리스트 맨 앞에 새로운 값을 추가할 수 있음 &#x20;

```
let list = { value: 1 };
list.next = { value: 2 };
list.next.next = { value: 3 };
list.next.next.next = { value: 4 };

// list에 새로운 value를 추가
list = { value: "new item", next: list };
```

![](<../../.gitbook/assets/image (3) (1).png>)



* 중간 요소를 제거하려면 이전 요소의 `next`를 변경해주면 됨

```
list.next = list.next.next;
```

![](<../../.gitbook/assets/image (5) (1).png>)



* 연결 리스트의 가장 큰 단점은 번호(인덱스)만 사용해 요소에 쉽게 접근할 수 없음 &#x20;
  * 배열을 사용하면 `arr[n]`처럼 번호 `n`만으로도 원하는 요소에 바로 접근할 수 있지만,
  * 연결 리스트에선 `N`번째 값을 얻기 위해 첫 번째 항목부터 시작해 `N`번 `next`로 이동해야  함 &#x20;
