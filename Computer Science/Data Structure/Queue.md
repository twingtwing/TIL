# Queue
> 데이터를 순서대로 저장하고, 삭제하는 자료구조이다.

## 📌 큐(Queue) 란?
Queue는 Rear라는 위치에서는 삽입 연산이, Front라는 위치에서 삭제가 되도록 만든 자료구조이다. 따라서, 큐는 시간 순서에 따라 자료가 저장되고, 가장 처음에 저장되는 데이터가 가장 먼저 삭제되는 **선입선출**(FIFO, First-In-First-Out)의 구조를 가진다. 

                            Rear                               Front 
         삽입                 ⇓                                   ⇓
    +-----------+       +-----------+-----------+-----------+-----------+
    |   데이터   |   →  |   데이터   |   데이터  |   데이터   |   데이터  |    → 삭제
    +-----------+       +-----------+-----------+-----------+-----------+

#### 특징
- 선입선출(FIFO) : 가장 먼저 삽입된 데이터가 가장 먼저 제거된다.
- 삽입과 삭제의 위치가 정해져 있다. [ 삽입 : Rear | 삭제 : Front ]

#### 기본 연산
- EnQueue : 큐의 마지막 위치(Rear) 데이터를 삽입
- DeQueue : 큐의 처음 위치(Front) 데이터 제거
- Peek : 큐의 처음 데이터(Front) 반환
- IsEmpty : 비어있는지를 True, False로 반환
- Size : 저장된 데이터의 갯수를 반환

## 📌 큐(Queue) 구현

### 순차 자료구조
큐를 1차월 배열을 통해 구현되는 방식은 순차적으로 쌓이는 순서를 인덱스로 표현한다. 첫번째 원소의 인덱스를 front라는 변수에 저장하고, 마지막 원소의 인덱스를 rear라는 변수에 저장하여 삽입과 삭제가 마지막과 처음 위치에서만 이루어지도록 구현한다.  

❗이때, rear의 위치가 마지막에 위치하게되면, 포화상태가 아니더라도 포화상태로 인삭하는 문제가 생긴다. 추가적인 데이터 이동작업으로 위치를 조정할 수 있지만, 큐의 효율성을 떨어뜨리는 문제가 발생한다.

<details>
<summary>Queue Code</summary>

```java
class Queue{
    int front;
    int rear;
    int [] queue;

    Queue(int len){
        front = -1;
        rear = -1;
        queue = new int[len];
    }

    int size(){
        return rear - front;
    }

    boolean isEmpty(){
        return front == rear;
    }

    boolean isFull(){
        return rear == queue.length - 1;
    }

    public void enQueue(int data){
        if (isFull()) throw new IllegalStateException("Queue is Full");
        queue[++rear] = data;
    }

    public int deQueue(){
        if(isEmpty()) throw new IllegalStateException("Queue is Empty");
        queue[++front];
    }

    public int peek(){
        if(isEmpty()) throw new IllegalStateException("Queue is Empty");
        return queue[front + 1];
    }

}
```
</details>
<br>

          rear = 2                rear = 3            rear = 3 
            ↓         삽입          ↓      삭제          ↓
    [ 3, 7, 2, 0, 0 ] ⇢ [ 3, 7, 2, 9, 0 ] ⇢ [ 3, 7, 2, 9, 0 ] 
    ↑                    ↑                     ↑
    front = -1           front = -1          front = 0    

### Circular Queue  
배열의 처음과 끝이 연결되어 있는 자료구조를 원형큐라고 한다. 
- 공백 상태와 포화 상태를 구분하기 위해 자리 하나를 항상 비워둔다.  
- 삽입연산 시 rear 인덱스 혹은 삭제 연산 시 front 인덱스를 원형으로 표현하기 위해서 ( index + 1 ) % length 연산을 통해 인덱스 값을 가져온다.

<details>
<summary>Circular Queue Code</summary>

```java
class Queue {
    int front;
    int rear;
    int [] queue;

    Queue(int len){
        this.front = 0;
        this.rear = 0;
        this.queue = new int[len];
    }

    boolean isEmpty() {
        return (front == rear);
    }

    boolean isFull(){ 
        return front == getNextIdx(rear);
    }

    int getNextIdx(int idx){
        return (idx + 1) % queue.length;
    }

    void enQueue(int data) {
        if (isFull()) throw new IllegalStateException("Queue is Full");
        rear = getNextIdx(rear);
        queue[rear] = data;
    }

    public int deQueue() { 
        if(isEmpty()) throw new IllegalStateException("Queue is Empty");
        front = getNextIdx(front);
        return queue[front];
    }

    public char peek() {
        if(isEmpty()) throw new IllegalStateException("Queue is Empty");
        return queue[getNextIdx(front)];
    }
}
```
</details>
<br>

#### 삽입

#### 삭제

여기에 그림 묘사 추가

### 연결 자료구조 
큐를 연결 리스트를 통해 구현되는 방식은 데이터가 순차적으로 쌓이는 순서를 Node가 참조되는 순서로 표현한다. 첫번째 Node를 front라는 참조변수에 저장하고, 마지막 Node를 rear라는 참조변수에 저장하여 삽입과 삭제가 해당 위치에서만 이루어지도록 구현한다.

<details>
<summary>Queue Code</summary>

```java
class Queue{

    Node front; 
    Node rear;  

    class Node{
        int data;
        Node link;
        Node(){}
        Node(int data){this.data = data;}
    }

    Queue(){
        front = null;
        rear = null;
    }

    boolean isEmpty(){return front == null;}

    void enQueue(int data){
        Node node = new Node(data);
        if (isEmpty()) front = node;
        if (rear != null) rear.link = node;
        rear = node;
    }

    int deQueue(){
        if(isEmpty()) throw new IllegalStateException("Queue is Empty");
        int data = front.data;
        front = front.link;
        if (isEmpty()) rear = null;
        return data;
    }

    int peek(){
        if(isEmpty()) throw new IllegalStateException("Queue is Empty");
        return front.data;
    }

}
```
</details>
<br>


여기에 그림 묘사 추가

## 📌 Deque (Double-ended Queue) 
> Deque는 Stack과 Queue의 특징을 모두 가지고 있다.

#### 특징
- 양쪽 끝에서 각각 삽입과 삭제가 모두 이루어진다.
- Front/Rear를 Stack의 top으로 생각하여 push, pop연산 모두 각각 가능하다.

#### 기본 연산
- AddFirst / OfferFirst : Deque의 Front 위치에 데이터를 삽입
- AddLast  / OfferLast  : Deque의 Rear 위치에 데이터를 삽입
- RemoveFirst / PollFirst : Deque의 Front 위치에 데이터 삭제
- RemoveLast  / PollLast  : Deque의 Rear 위치에 데이터 삭제
- PeekFirst / GetFirst : Deque의 Front 위치에 데이터를 반환
- PeekLast  / GetLast  : Deque의 Rear 위치에 데이터를 반환
- IsEmpty : 비어있는지를 True, False로 반환
- Size : 저장된 데이터의 갯수를 반환

<details>
<summary>Deque Code</summary>

```java
class Node{
    int data;
    Node right;
    Node left;
    Node(int data){data = data;}
}

class Deque{
    Node front;
    Node rear;

    public Deque(){
        this.front = null;
        this.rear = null;
    }

    public boolean isEmpty(){
        return (front == null);
    }

    public void addFirst(int data){
        Node node = new Node(data);
        if (isEmpty()){
            front = node;
            rear = node;
        }else{
            node.right = front;
            front.left = node;
            front = node;
        }
    }

    public void addLast(int data){
        Node node = new Node(data);
        if (isEmpty()){
            front = node;
            rear = node;
        }else{
            node.left = rear;
            rear.right = node;
            rear = node;
        }
    }

    public int pollFirst(){
        if(isEmpty()) throw new IllegalStateException("Deque is Empty");
        int data = front.data;
        if (front.right == null){
            front = null;
            rear = null;
        }else{
            front = front.right;
            front.left = null;
        }
        return data;
    }

    public int pollLast(){
        if(isEmpty()) throw new IllegalStateException("Deque is Empty");
        int data = rear.data;
        if (rear.left == null){
            front = null;
            rear = null;
        }else{
            rear = rear.left;
            rear.right = null;
        }
        return data;
    }

    public int peekFirst(){
        if(isEmpty()) throw new IllegalStateException("Deque is Empty");
        return front.data;
    }

    public int peekLast(){
        if(isEmpty()) throw new IllegalStateException("Deque is Empty");
        return rear.data;
    }

}
```
</details>
<br>

#### 삽입

#### 삭제

여기에 그림 묘사 추가

## Reference

- [자바로 배우는 자료구조 방식](https://product.kyobobook.co.kr/detail/S000001636199)
- [엔지니어 대한민국](https://www.youtube.com/@eleanorlim)