# Queue
    ✍️ Queue 자료구조는 삽입하는 순서대로 삭제되는 선입선출 구조이다.
## 1. Queue란?
Queue는 가장 처음에 들어간 데이터가 삭제되는 **선입선출**(FIFO, First-In-First-Out)구조로 운영된다.  
삭제연산이 수행되는 위치를 Front, 삽입연산이 수행되는 위치를 Rear로 정한다. Front 원소는 저장된 원소 중에서 첫번째 원소이고, Rear 원소는 저장된 원소중에서 마지막 원소이다. Queue의 Rear에서 이루어지는 삽입연산을 enQueue, Front에서 이루어지는 삭제연산을 deQueue라고 한다.

<img width="800" src="../../Image/queue_sequential.png" title="Linked list Data Structure">   

<small>출처 : <cite>https://www.geeksforgeeks.org/queue-set-1introduction-and-array-implementation/</cite> </small>

## 2. 순차 자료구조 방식을 이용한 Queue의 구현

### 2.1 선형큐  
순차 자료구조인 1차원 배열을 이용하여 Queue을 구현할 수 있다. 큐에 원소가 쌓이는 순서는 배열의 인덱스(index)로 표현한다. **Front은 첫번째 원소의 인덱스, Rear은 마지막 원소의 인덱스**를 의미한다.  
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

### 2.2 원형 큐  
선형큐는 포화상태가 아닐 경우에만 삽입연산을 수행하도록 정의되어 있다. 그러나, front의 위치가 진짜 이 아닐경우, 빈자리가 있음에도 raer가 n-1이므로 포화상태로 인식한다. 삽입/삭제 연산을 진행하지 않는다. 그렇기에 빈부분을 없애기 위해 앞부분으로 이동시켜 위치를 조정해야한다. 이러한 이동 작업은 큐의 효율성을 떨어 뜨린다. 이러한 문제를 해결하기 위해 , 1차원 배열을 사용하지만 처음과 끝이 연결되어 있는 원형 Queue가 있다.  
원형큐에서는 초기 공백 상태일 때 front와 rear의 값이 0이 되고, 공백 상태와 포화 상태를 구분하기 위해서 자리 하는 항상 비워둔다. 원형큐에서는 공백 상태 조건은 front = rear가 된다.  rear는 앞으로 이동하면서 원소를 삽입하고, front는 rear가 이동한 방향을 따라가면서 원소를 삭제한다. 원형 큐에서는 배열의 인덱스가 n-1다음에 다시 0이 되어야하므로 사용할 다음 인덱스를 정하기 위해서 나머지 연산자 mod를 사용한다.? 즉, 포화상태인 rear의 다음 위치 ((rear+1) mod n)는 현재의 front위치가 되어 더 이상 원소를 삽입할 수 없는 포화 상태가 된다..?????

<details>
<summary>순차 자료구조 방식을 이용한 Queue 알고리즘</summary>

```java
```
</details>
<br>

## 3. 연결 자료구조 방식을 이용한 Queue의 구현

### 3.1 연결큐  
순차자료구조방식을 이용하게되면, 사용 크기가 데한되어 있어서 큐의 길이를 마음대로 변경할 수 없고, 원소가 없을 때에도 항상 처음 크기를 유지하고 있어야 하므로 메모리도 낭비된다. 이러한 문제를 극복하기 위해 연결 자료구조 방식을 이요하여 크기에 제한이 없는 연결큐를 구현한다.  
연결 큐에서 원소는 데이터 필드와 링크 필드를 가진 노드로 구성하며, 첫 번째 노드를 가리키는 참조변수 front와 마지막 노드를 가리키는 참조변수 rear를 사용한다.(참조변수가 2개를 가진다.) 연결큐의 초기 상태는 front와 rear를 NULL로 초기화하여 표현한다. 즉, 둘다 NULL이면 공백 상태임을 알 수 있다. 삽입연산 시 새노드를 생성하여 데이터 필드에 저장하고, 삽입할 새 노드는 마지막 노드가 되어야하므로 링크 필드에 NULL로 저장한다. 이때 공백 상태였을 경우 FRONT, REAR모두 마지막 노드를 가리키고 참조값을 저장한다. 공백상태가 아니었던 경우에는 마지막이었던 노드가 삽입한 노드 의 참조값을 저장하고(마지막 노드 뒤에 새노드를 삽입) REAR 또한 해당 노드를 가리키도록 설정한다.  삭제연산의 경우에는 첫번째 노드를 삭제하고, FRONT가 새로운 첫번째 노드를 가리킨다. 이때 만약에 노드가 남지 않는다면 FRONT와 REAR에 참조된 값을 지우고 NULL로 초기화시켜준다.

<details>
<summary>연결 자료구조 방식을 이용한 Queue 알고리즘</summary>

```java
```
</details>
<br>

## 4. Deque
Deque는 양쪽 끝에서 삽입과 삭제가 모두 발생하는 Queue로서, Stack과 Queue의 성지를 모두 가지고 있다. Deque에서 Front/Rear를 Stack의 top으로 생각하여 push, pop연산 모두 각각 가능하다.

---

## Reference

- 자바로 배우는 자료구조 방식