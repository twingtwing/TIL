# Queue
    ✍️ Queue 자료구조는 삽입하는 순서대로 삭제되는 선입선출 구조이다.
## 1. Queue란?
Queue는 가장 처음에 들어간 데이터가 삭제되는 **선입선출**(FIFO, First-In-First-Out)구조로 운영된다.  
삭제연산이 수행되는 위치를 Front, 삽입연산이 수행되는 위치를 Rear로 정한다. Front 원소는 저장된 원소 중에서 첫번째 원소이고, Rear 원소는 저장된 원소중에서 마지막 원소이다. Queue의 Rear에서 이루어지는 삽입연산을 enQueue, Front에서 이루어지는 삭제연산을 deQueue라고 한다.

<img width="800" src="../../Image/queue_sequential.png" title="Linked list Data Structure">   

<small>출처 : <cite>https://www.geeksforgeeks.org/queue-set-1introduction-and-array-implementation/</cite> </small>

## 2. 순차 자료구조 방식을 이용한 Queue의 구현

### 2.1 Linear Queue  
순차 자료구조인 1차원 배열을 이용하여 선형 큐를 구현할 수 있다. 큐에 원소가 쌓이는 순서는 배열의 인덱스(index)로 표현한다. **Front은 첫번째 원소의 인덱스, Rear은 마지막 원소의 인덱스**를 의미한다.  
초기 상태의 경우에는 Front = Rear = -1, 포화 상태의 경우에는 Rear = length - 1, 공백상태의 경우 Front = Rear이다.

<details>
<summary>순차 자료구조 방식을 이용한 Queue 알고리즘</summary>

```java
class ArrayQueue implements Queue{
    private int front; // 가장 처음 들어가는 데이터 index
    private int rear; // 가장 나중에 들어가는 데이터 index
    private int queueSize;
    private char[] itemArray;

    ArrayQueue(){
        this.front = -1;
        this.rear = -1;
        this.queueSize = 0;
        this.itemArray = null;
    }
    ArrayQueue(int queueSize){
        this.front = -1;
        this.rear = -1;
        this.queueSize = queueSize;
        this.itemArray = new char[this.queueSize];
    }

    @Override
    public boolean isEmpty() {
        return (front == rear);
    }

    public boolean isFull(){
        return (rear == (queueSize -1));
    }

    @Override
    public void enQueue(char item) { // insert연산은 rear
        if (isFull()) return;
        itemArray[++rear] = item;

    }

    @Override
    public char deQueue() { // delete연산은 front
        if (isEmpty()) return 0;
        return itemArray[++front];
    }

    @Override
    public void delete() {
        if (isEmpty()) return;
        ++front;
    }

    @Override
    public char peek() {
        return itemArray[front + 1];
    }

    public void printQueue(){
        if (isEmpty()) return;
        for (int i = front + 1; i <= rear; i++){
            System.out.print(itemArray[i] + " ");
        }
        System.out.println();
    }

}
```
</details>
<br>

❗이때, front = rear가 아님에도 rear = length - 1이면, 포화상태로 인식하는 문제점이 발생한다. 이를 해결하기 위해서는 앞부분으로 이동시켜서 위치를 조정해야하지만, 이런 이동 작업은 큐의 효율성을 떨어 뜨린다.

### 2.2 Circular Queue   
선형 큐와 동일하게 1차원 배열을 사용하지만, 논리적으로는 배열의 처음과 끝이 연결되어 있는 자료구조를 원형큐라고 한다. 초기 상태의 경우 Front = Rear = 0, 공백 상태의 경우 Front = Rear이다. 공백 상태와 포화 상태를 쉽게 구분하기 위해서 자리 하나를 항상 비워둔다.  
rear에 삽입되면서 인덱스 값이 length - 1 인 경우, 다시 0이 되어야한다. 이때, 다음 index는 ((rear + 1) mod length)연산을 통해 구하고,  다음 인덱스가 front위치가 일 경우에는 더 이상 삽입할 수 없는 포화 상태를 의미한다. 삭제 연산도 마찬가지로 front가 다음 index로 바뀌어야 하는데, ((front + 1) mod length) 연산을 통해 구한다.

<details>
<summary>순차 자료구조 방식을 이용한 Queue 알고리즘</summary>

```java
class CircularQueue implements Queue{
    private int front;
    private int rear;
    private int queueSize;
    private char itemArray[];

    CircularQueue(int queueSize){
        this.front = 0;
        this.rear = 0;
        this.queueSize = queueSize;
        this.itemArray = new char[this.queueSize];
    }

    @Override
    public boolean isEmpty() {
        return (front == rear);
    }

    public boolean isFull(){ // 다음 index 값이 front일 경우
        // 공백 상태와 포화 상태를 구분하기 위해 자리를 1개 비워두기 때문에, 모든칸을 전부 사용하지 않는다.
        return ((this.rear + 1) % this.queueSize == front);
    }

    @Override
    public void enQueue(char item) {
        if (isFull()) return;
        rear = (rear + 1) % this.queueSize;
        itemArray[rear] = item;
        System.out.println(rear+" " +item);
    }

    @Override
    public char deQueue() { // front가 다음 인덱스로 수정
        if (isEmpty()) return 0;
        front = (front+1) % this.queueSize;
        return itemArray[front];
    }

    @Override
    public void delete() {
        if (isEmpty()) return;
        front = (front+1) % this.queueSize;
    }

    @Override
    public char peek() {
        if (isEmpty()) return 0;
        return itemArray[(front+1) % this.queueSize];
    }

    public void printQueue(){
        if (isEmpty()) return;
        int tempFront = this.front;
        int tempRear = this.rear;
        while (tempFront != tempRear){
            tempFront = (tempFront + 1) % this.queueSize;
            System.out.print(itemArray[tempFront]+" ");
        }
        System.out.println();
    }
}
```
</details>
<br>

## 3. 연결 자료구조 방식을 이용한 Queue의 구현

### 3.1 Linked Queue  
선형큐와 원형큐에서 가지는 메모리 비효율성 문제를 극복하기 위해, 연결 자료구조 방식을 이용하여 구현한 Queue를 연결 큐라고 한다. 연결 큐에서 Front는 첫번째 Node, Rear은 마지막 Node를 참조한다.  
초기 상태의 경우 Front = Rear = null, 공백 상태의 경우 Front = null이다.

<details>
<summary>연결 자료구조 방식을 이용한 Queue 알고리즘</summary>

```java
class Node{
    char data;
    Node link;
}

class LinkedQueue implements Queue{
    private Node front;
    private Node rear;

    LinkedQueue(){
        this.front = null;
        this.rear = null;
    }

    @Override
    public boolean isEmpty() {
        return (this.front == null);
    }

    @Override
    public void enQueue(char item) {
        Node node = new Node();
        node.data = item;
        if (isEmpty()){
            this.front = node;
            this.rear = node;
        }else{
            rear.link = node;
            this.rear = node;
        }
    }

    @Override
    public char deQueue() {
        if (isEmpty()) return 0;
        char result = this.front.data;
        this.front = front.link;
        if(front == null) rear = null;
        return result;
    }

    @Override
    public void delete() {
        if (isEmpty()) return;
        this.front = front.link;
        if(front == null) rear = null;
    }

    @Override
    public char peek() {
        if (isEmpty()) return 0;
        return this.front.data;
    }

    public void printQueue(){
        if (isEmpty()) return;
        Node temp = this.front;
        while (temp != null){
            System.out.print(temp.data + " ");
            temp = temp.link;
        }
        System.out.println();
    }
}
```
</details>
<br>

## 4. Deque (Double-ended Queue)
Deque는 양쪽 끝에서 삽입과 삭제가 모두 발생하는 Queue로서, Stack과 Queue의 성질을 모두 가지고 있다. Deque에서 Front/Rear를 Stack의 top으로 생각하여 push, pop연산 모두 각각 가능하다.


<details>
<summary>Deque 알고리즘</summary>

```java
class DNode{
    char data;
    DNode rlink;
    DNode llink;
}

class Deque{
    DNode front;
    DNode rear;

    public Deque(){
        front = null;
        rear = null;
    }

    public boolean isEmpty(){
        return (front == null);
    }

    public void insertFront(char item){
        DNode node = new DNode();
        node.data = item;
        if (isEmpty()){
            front = node;
            rear = node;
        }else{
            front.llink = node;
            node.rlink = front;
            front = node;
        }
    }

    public void insertRear(char item){
        DNode node = new DNode();
        node.data = item;
        if (isEmpty()){
            front = node;
            rear = node;
        }else{
            rear.rlink = node;
            node.llink = rear;
            rear = node;
        }
    }

    public char deleteFront(){
        if (isEmpty()) return 0;
        char result = front.data;
        if (front.rlink == null){
            front = null;
            rear = null;
        }else{
            front = front.rlink;
            front.llink = null;
        }
        return result;
    }

    public char deleteRear(){
        if (isEmpty()) return 0;
        char result = rear.data;
        if (rear.llink == null){
            front = null;
            rear = null;
        }else{
            rear = rear.llink;
            rear.rlink = null;
        }
        return result;
    }

    public void removeFront(){
        if (isEmpty()) return;
        if (front.rlink == null){
            front = null;
            rear = null;
        }else{
            front = front.rlink;
            front.llink = null;
        }
    }

    public void removeRear(){
        if (isEmpty()) return;
        if (rear.llink == null){
            front = null;
            rear = null;
        }else{
            rear = rear.llink;
            rear.rlink = null;
        }
    }

    public char peekFront(){
        if (isEmpty()) return 0;
        return front.data;
    }

    public char peekRear(){
        if (isEmpty()) return 0;
        return rear.data;
    }

    public void printDeque(){
        if (isEmpty()) return;
        DNode temp = this.front;
        while (temp != null){
            System.out.print(temp.data +" ");
            temp = temp.rlink;
        }
        System.out.println();
    }

}
```
</details>
<br>

---

## Reference

- 자바로 배우는 자료구조 방식