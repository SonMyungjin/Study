# 큐

## 큐의 정의

* 컴퓨터의 기본적인 자료 구조의 한가지
* **Java**는 LinkedList를 이용해서 구현할 수 있으며 **add / offer**를 통해 삽입하거나 **poll**을 통해 데이터를 삭제할 수 있다.
* 먼저 집어 넣은 데이터가 먼저 나오는 선입선출(FIFO - Frist In First Out)구조로 저장하는 형식
* 프린터의 출력 처리나 윈도우 시스템의 메시지 처리기, 프로세스 관리 등 데이터가 입력된 시간 순서대로 처리해야 할 필요가 있는 상황에 이용



### 큐의 용어

* put : 큐에 자료를 넣는 것
* get : 큐에서 자료를 꺼내는 것
* front : 데이터를 get할 수 있는 위치
* rear : 데이터를 put할 수 있는 위치
* Overflow : 큐가 꽉 차서 더 이상 자료를 넣을 수 없는 경우
* Underflow : 큐가 비어 있어 자료를 꺼낼 수 없는 경우



## 큐의 종류

#### 1. 선형 큐

* 막대 모양으로 된 큐
*   크기가 제한되어 있고 빈 공간을 사용하려면 모든 자료를 꺼내거나 자료를 한 칸씩 옮겨야

    한다는 단점이 있음
* Data : A → B → C → D



#### 2. 환형 큐

* 배열로 큐를 선언할 시 큐의 삭제와 생성이 계속 일어났을 때, 마지막 배열에 도달 후 실제로는 데이터 공간이 남아있지만 오버플로우가 발생하는 선형 큐의 문제점을 보완한 것
* front(head)가 큐의 끝에 닿으면 큐의 맨 앞으로 자료를 보내어 원형으로 연결
* Data : A → B → C → D → E



* 배열로 구현된 선형 큐 (java)

```java
public class Main {
    public static void main(String args[]) {
        int size = 3;
        ArrayQueue arrQueue = new ArrayQueue(size);
        
        arrQueue.enqueue("A");
        arrQueue.print();
        
        arrQueue.enqueue("B");
        arrQueue.print();

        arrQueue.peek();
        arrQueue.print();
        
        arrQueue.enqueue("C");
        arrQueue.print();
        
        arrQueue.enqueue("D");
        arrQueue.print();

        arrQueue.dequeue();
        arrQueue.print();

        arrQueue.enqueue("E");
        arrQueue.print();
        
        arrQueue.dequeue();
        arrQueue.print();
        
        arrQueue.clear();
        arrQueue.print();

        arrQueue.clear();

        arrQueue.dequeue();
    } 
}

class ArrayQueue {    
    private int front;
    private int rear;
    private int size;
    private String arr[];
 
    public ArrayQueue(int size) {
        front = -1;    
        rear = -1;    
        this.size = size;    
        arr = new String[this.size];    
    }
    
    public boolean isEmpty() {
        return (front == rear);
    }
    
    public boolean isFull() {
        return (rear == this.size - 1);
    }
    
    public void enqueue(String item) {
        if(isFull()) {
            System.out.println("Queue is full");
        } else {             
            arr[++rear] = item; 
        }
    }

    public String dequeue() {
        if(isEmpty()) {
            System.out.println("Queue is empty");
            return null;
        } else {
            System.out.println(arr[front + 1]);
            front = (front + 1) % this.size;
            return arr[front];
        }
    }
    
    public String peek() {
        if(isEmpty()) {
            System.out.println("Queue is empty");
            return null;
        } else { 
            System.out.println(arr[front + 1]);
            return arr[front + 1];
        }
    }
    
    public void clear() {
        if(isEmpty()) {
            System.out.println("Queue is already empty");
        } else {
            front = -1;    
            rear = -1;    
            arr = new String[this.size];   
            System.out.println("Queue is clear");
        }
    }
    
    public void print() {
        if(isEmpty()) {
            System.out.println("Queue is empty");
        } 
        else {
            for (int i = front + 1; i <= rear; i++) {
                System.out.print(arr[i] + " ");
            }
            System.out.println();
        }
    }
}
```

```java
// 출력
A 
A B
A
A B
A B C
Queue is full
A B C
A
B C
// 배열로 구현한 선형 큐의 단점 : 실제로는 데이터 공간이 남아있지만 오버플로우가 발생
Queue is full
B C
B
C
Queue is clear
Queue is empty
Queue is already empty
Queue is empty
```



* 리스트로 구현된 선형 큐 (java)

```java
public class Main {
    public static void main(String args[]) {
        int size = 3;
        ListQueue listQueue = new ListQueue(size);   
    
        listQueue.enqueue("A");
        listQueue.print();

        listQueue.enqueue("B");
        listQueue.print();

        listQueue.peek();
        listQueue.print();

        listQueue.enqueue("C");
        listQueue.print();

        listQueue.enqueue("D");
        listQueue.print();

        listQueue.dequeue();
        listQueue.print();

        listQueue.enqueue("E");
        listQueue.print();
        
        listQueue.dequeue();
        listQueue.print();

        listQueue.clear();
        listQueue.print();

        listQueue.clear();

        listQueue.dequeue();
        listQueue.print();
    }
}

class Node {
    private String data;    
    public Node link;    
     
    public Node(String data) {
        this.data = data;
        this.link = null;
    }
    
    public Node(String data, Node link) {
        this.data = data;
        this.link = link;
    }
    
    public String getData() {
        return this.data;
    }
}
 
class ListQueue {
    private Node head;    
    private Node front;   
    private Node rear;    
    private int size;   
    
    public ListQueue(int size) {
        head = null; 
        front = null;    
        rear = null;    
        this.size = size;    
    }
    
    public boolean isEmpty(){
        return (front == null && rear == null);
    }
    
    public boolean isFull() {
        if (isEmpty()) {
            return false;
        } 
        else {
            int nodeCnt = 0;   
            Node tmpNode = head;    
            
            while(tmpNode.link != null) {
                nodeCnt++;
                tmpNode = tmpNode.link;    
            }
            return (this.size - 1 == nodeCnt);
        }
    }
    
    public void enqueue(String data) {
        Node newNode = new Node(data);   
 
        if (isFull()) {
            System.out.println("Queue is full");
            return;
        } 
        else if (isEmpty()) {
            this.head = newNode;
            this.front = this.head;
            this.rear = this.head;
        } else {
            rear.link = newNode;
            rear = newNode;
        }
    }
    
    public void dequeue() {
        Node tmpNode;
        if (isEmpty()) {
            System.out.println("Queue is empty");
            return;
        }

        if(front.link == null) {
            head = null;
            front = null;
            rear = null;
        } 
        else {
            tmpNode = front.link;    
            head = tmpNode;    
            front.link = null;    
            front = head;   
        }
    }
    
    public void peek() {
        if(isEmpty()) {
            System.out.println("Queue is empty");
            return;
        } 
        else {
            System.out.println(front.getData());
        }
    }
    
    public void clear() {
        if(isEmpty()) {
            System.out.println("Queue is already empty");
            return;
        } 
        else {
            head = null;
            front = null;
            rear = null;
        }
    }
    
    public void print() {
        if (isEmpty()) {
            System.out.println("Queue is empty");
            return;
        } 
        else {
            Node tmpNode = this.front;               
            while(tmpNode != null) {
                System.out.print(tmpNode.getData() + " ");
                tmpNode = tmpNode.link;    
            }
            System.out.println();
        }
    }
}
```

```java
// 출력
A 
A B
A
A B
A B C
Queue is full
A B C
B C
B C E
C E
Queue is empty
Queue is already empty
Queue is empty
Queue is empty
```



* Queue 라이브러리 (java)

```java
import java.util.LinkedList;
import java.util.Queue;

public class Main {
    public static void main(String args[]) {
        Queue<String> queue = new LinkedList<String>();

        queue.offer("A");
        System.out.println(queue.toString());

        queue.offer("B");
        System.out.println(queue.toString());

        System.out.println(queue.peek());
        System.out.println(queue.toString());

        queue.offer("C");
        System.out.println(queue.toString());

        queue.offer("D");
        System.out.println(queue.toString());

        System.out.println(queue.poll());
        System.out.println(queue.toString());

        queue.offer("E");
        System.out.println(queue.toString());

        System.out.println(queue.poll());
        System.out.println(queue.toString());
        
        queue.clear();
        System.out.println(queue.toString());
    }
}
```

```java
// 출력
[A]
[A, B]
A
[A, B]
[A, B, C]
[A, B, C, D]
A
[B, C, D]
[B, C, D, E]
B
[C, D, E]
[]
```
