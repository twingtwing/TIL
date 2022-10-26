# Stack  
    ✍️ Stack 자료구조는 접시를 쌓듯이 자료를 쌓아 올린 형태의 구조를 말한다.

## 1. Stack이란?
Stack은 top으로 정한 한 곳에서만 쌓을 수 있고, 접근하도록 제한하여 만든 자료구조이다. 
top으로만 접근이 가능하기 때문에 나중에 들어온 자료가 맨 위에 위치하게 되고, 삭제하는 자료도 가장 위에 위치하는 자료이다.(삽입연산을 push, 삭제 연산을 pop이라고 한다.)  
따라서, 스택은 시간순서에 따라 자료가 쌓이고, 삭제 할때믄 가장 마지막에 삽입된 자료가 가장 먼저 삭제되는 **후입선출**(LIFO, Last-In-First-Out)의 구조를 가진다. 

## 2. 순차 자료구조 방식을 이용한 Stack의 구현

순차 자료구조인 1차원 배열을 이용하여 스택을 구현할 수 있다. 스택에 원소가 쌓이는 순서는 배열의 인덱스(index)로 표현한다. 따라서 스택의 첫번째 원소는 stack[0]에 저장하고, i번째 원소는 stack[i-1]에 저장한다. 배열 stack에서의 **top은 마지막 원소의 인덱스**을 의미한다. 스택이 초기 상태(공백)일 때 top은 -1을 저장한다. 

<img width="800" src="../../Image/stack_sequential.jpg" title="Linked list Data Structure">   

<small>출처 : <cite>https://www.geeksforgeeks.org/how-to-implement-stack-in-java-using-array-and-generics/</cite> </small>

<details>
<summary>순차 자료구조 방식을 이용한 Stack 알고리즘</summary>

```java
class ArrayStack implements Stack{
    private int top; // top index를 저장하는 변수
    private int stackSize; 
    private char itemArray[];
    
    ArrayStack(){
        this.top = -1;
        this.stackSize = 0;
        this.itemArray = null;
    }
    ArrayStack(int stackSize){
        this.top = -1;
        this.stackSize = stackSize;
        this.itemArray = new char[stackSize];
    }

    @Override
    public boolean isEmpty() {
        return (this.top == -1);
    }
    
    public boolean isFull(){
        return (this.top == this.stackSize -1);
    }

    @Override
    public void push(char item) {
        if (isFull()) return;
        itemArray[++top] = item;
    }
    
    @Override
    public char pop() {
        if (isEmpty()) return 0;
        return itemArray[top--]; 
    }

    @Override
    public void delete() {
        if (isEmpty()) return;
        top--;
    }

    @Override
    public char peek() {
        if (isEmpty()) return 0;
        return itemArray[top];
    }

    public void printStack(){
        if (isEmpty()) return;
        int temp = this.top;
        while (temp != -1){
            System.out.print(itemArray[temp--]+" ");
        }
        System.out.println();
    }
}
```
</details>
<br>

순차 자료구조를 이용한 스택은 배열을 사용하여 구현하기는 쉽지만, 물리적으로 크기가 고정된 배열을 사용하기 때문에 스택의 크기를 변경하기가 어렵고, 메모리의 낭비가 생길 수 있다는 문제가 있다. 

## 3. 연결 자료구조 방식을 이용한 Stack의 구현

연결 자료구조 방식의 단순 연결 리스트를 이용하여 스택을 구현한다. 연결 자료구조 방식은 첫번째 노드에 계속 삽입이 되면서, 참조변수의 값이 계속 바뀌는 구조이다. 이때의 참조변수는 top을 의미하고, **top은 첫번째 Node**를 의미한다.

<details>
<summary>연결 자료구조 방식을 이용한 Stack 알고리즘</summary>

```java
class StackNode{
    char data;
    StackNode link;
}

class LinkedStack implements Stack{
    private StackNode top;

    LinkedStack(){
        this.top = null;
    }

    @Override
    public boolean isEmpty() {
        return (top == null);
    }

    @Override
    public void push(char item) {
        StackNode node = new StackNode();
        node.data = item;
        node.link = this.top;
        this.top = node;
    }

    @Override
    public char pop() {
        if (isEmpty()) return 0;
        char result = this.top.data;
        this.top = this.top.link;
        return result;
    }

    @Override
    public void delete() {
        if (isEmpty()) return;
        this.top = this.top.link;
    }

    @Override
    public char peek() {
        if (isEmpty()) return 0;
        return this.top.data;
    }

    public void printStack(){
        if (isEmpty()) return;
        StackNode temp = top;
        while (temp != null){
            System.out.print(temp.data+" ");
            temp = temp.link;
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