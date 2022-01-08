# 스택

### 스택의 정의

* **스택**(stack)은 목록 끝에서만 데이터가 들어오고 나가는 자료구조이다.&#x20;
* **Java**에서는 **Stack** 클래스를 이용하여 **push**, **pop** 을 사용할 수 있다.
* 스택은 한 쪽 끝에서만 자료를 넣거나 뺄 수 있는 선형 구조(LIFO - Last In First Out)으로 되어 있다.
  * 자료를 넣는 것을 '밀어넣는다' 하여 **푸쉬**(push)라고 하고&#x20;
  * 반대로 넣어둔 자료를 꺼내는 것을 **팝**(pop)이라고 하는데,&#x20;
  * 이때 꺼내는 자료는 가장 최근에 푸쉬한 자료부터 나오게 된다.&#x20;
  * 이처럼 나중에 넣은 값이 먼저 나오는 것을 [LIFO](https://ko.wikipedia.org/wiki/LIFO) 구조라고 한다.
* 스택이 비었다면 1을 반환하고, 그렇지 않다면 0을 반환한다.



### 스택의 연산

* top() : 스택의 가장 윗(마지막) 데이터를 반환한다.
* pop() : 스택의 가장 윗(마지막) 데이터를 삭제한다
*   push() : 스택의 가장 윗 데이터로 top이 가리키는 자리 위에(top = top + 1) 메모리를 생성,

    데이터 x를 넣는다.
* is\_empty() : 스택이 비었다면 True 를 반환하고,그렇지 않다면 False 를 반환한다.



#### <mark style="color:blue;"><mark style="background-color:blue;">배열로 구현한 스택 (java)<mark style="background-color:blue;"></mark>

```java
public class StackArray {
    public static void main(String[] args) {
        int size = 5;
        Stack stack = new Stack(size);

        stack.push(1);
        stack.printStack();
        stack.push(2);
        stack.printStack();
        stack.push(3);
        stack.printStack();
        stack.pop();
        stack.printStack();
    }
}

class Stack {
    private int top;
    private int[] stackArr;
    private int size;

    public Stack(int size) {
        top = -1;
        this.stackArr = new int[size];
        this.size = size;
    }

    public void push(int val) {
        if (isFull()) {
            throw new ArrayIndexOutOfBoundsException();
        }
        stackArr[++top] = val;
    }

    public int pop() {
        if (isEmpty()) {
            throw new ArrayIndexOutOfBoundsException();
        }
        return stackArr[top--];
    }

    public boolean isEmpty() {
        return (top == -1);
    }

    public boolean isFull() {
        return (top == size - 1);
    }

    public void printStack() {
        if (isEmpty()) {
            System.out.println("Stack is empty.");
        }
        else {
            for (int i = 0; i <= top; i++) {
                System.out.print(stackArr[i] + " ");
            }
        }
        System.out.println("");
    }
}
```

```java
// 출력
1 
2 1
3 2 1
2 1
```



#### <mark style="background-color:blue;"><mark style="color:blue;">Stack 라이브러리 (java)<mark style="color:blue;"></mark>

```java
import java.util.Stack;

public class Main {
    public static void main(String args[]) {
        Stack<Integer> stack = new Stack<Integer>();
        
        stack.push(1);
        System.out.println(stack.toString());
        stack.push(2);
        System.out.println(stack.toString());
        stack.push(3);
        System.out.println(stack.toString());
        stack.pop();
        System.out.println(stack.toString());
    }
}
```

```java
// 출력
[1]
[1, 2]
[1, 2, 3]
[1, 2]
```
