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

#### 순차 자료구조 방식을 이용한 Stack 알고리즘

<details>
<summary>1. 고정길이</summary>

```java
class StackFixArray{
    int len;
    int part;
    int[] top;
    int[] stackAry;

    StackFixArray(int len, int part){
        this.len = len;
        this.part = part;
        this.top = new int[part];
        this.stackAry = new int[len*part];

        Arrays.fill(top,-1);
    }

    boolean isEmpty(int partIndex){return this.top[partIndex] == -1;}

    boolean isFull(int partIndex){return this.top[partIndex] == len-1;}

    int getIndex(int partIndex){
        if (partIndex >= part) throw new IndexOutOfBoundsException();
        return partIndex * len + this.top[partIndex];
    }

    void push(int partIndex, int data) throws FullStackException{
        if (isFull(partIndex)) throw new FullStackException();
        this.stackAry[getIndex(partIndex) + 1] = data;
        this.top[partIndex]++;
    }

    int pop(int partIndex){
        if (isEmpty(partIndex)) throw new EmptyStackException();
        int result = this.stackAry[getIndex(partIndex)];
        this.top[partIndex]--;
        return result;
    }

    int peek(int partIndex){
        if (isEmpty(partIndex)) throw new EmptyStackException();
        return this.stackAry[getIndex(partIndex)];
    }

    void retireve(){
        for (int i = 0; i < this.part; i++){
            if (isEmpty(i)) throw new EmptyStackException();
            System.out.print(i+1+" 번째 stack : ");
            int limit = this.top[i] + i*this.len;
            for (int j = 0; j < this.len; j++){
                int index = i * this.len + j;
                if (limit >= index) {
                    System.out.print(stackAry[index]+" ");
                }
            }
            System.out.println();
        }
    }

}
```
</details>

<details>
<summary>2. 유동길이</summary>

```java
class StackFlowArray{

    Stack[] stacks;
    int[] stackAry;

    class Stack{
        int top;
        int len;
        int start;

        Stack(int len, int start){
            this.top = -1;
            this.len = len;
            this.start = start;
        }

        //입력한 index가 해당 stack영역안에 존재하는지 check
        boolean inStack(int index){
            if(index < 0 || index >= stackAry.length) return false;
            //배열을 하나로 원으로 생각하기 때문에 가상의 값을 만듦
            int fakeIndex = index < start ? index + stackAry.length : index;
            int fakeEnd = start + len;
            return start <= fakeIndex && fakeIndex < fakeEnd;
        }

        boolean isFull(){return this.top == this.len - 1;}

        boolean isEmpty(){return this.top == -1;}

        int getLastStackIndex(){return adjustIndex(start + len - 1);}

        int getLastDataIndex(){return adjustIndex(start + top);}

        int getNewDataIndex(){return adjustIndex(getLastDataIndex() + 1);}
    }

    StackFlowArray(int size, int len){
        stacks = new Stack[size];
        for (int i = 0; i < size; i++){
            stacks[i] = new Stack(len, len*i);
        }
        stackAry = new int[size * len];
    }

    // 가상의 index를 나머지값(%)을 통해 실제 Index값을 구함
    // index가 -일 경우,
    // %를 해도 -이므로 여기서 len값을 더해서 한 번더 %을 해준다.
    int adjustIndex(int index){
        int max = stackAry.length;
        return ((index % max) + max) % max;
    }

    int previousIndex(int index){return adjustIndex(index - 1);}

    int nextIndex(int index){return adjustIndex(index + 1);}

    boolean allStackFull(){return totalDataSize() == stackAry.length;}

    int totalDataSize(){
        int result = 0;
        for (Stack stack : stacks){
            result += stack.top + 1;
        }
        return result;
    }

    // 확장
    void expend(int stackIndex){
        int nextIndex = (stackIndex + 1) % stacks.length;
        if (stacks[nextIndex].isFull()) expend(nextIndex);
        shift(nextIndex);
        stacks[stackIndex].len ++;
    }

    // 뒤로 미르기
    void shift(int stackIndex){
        Stack stack = stacks[stackIndex];
        int index = stack.getLastStackIndex();
        while (stack.inStack(index)){ // 한칸씩 미뤄짐
            stackAry[index] = stackAry[previousIndex(index)];
            index = previousIndex(index);
        }
        stackAry[stack.start] = 0; //미뤄지기 전의 start는 초기화 해주어야함.
        stack.start = nextIndex(stack.start);
        stack.len--;
    }

    void push(int stackIndex, int data) throws FullStackException {
        if (allStackFull()) throw new FullStackException();
        Stack stack = stacks[stackIndex];
        if (stack.isFull()){
            expend(stackIndex);
        }
        stackAry[stack.getNewDataIndex()] = data;
        stack.top++;
    }

    int pop(int stackIndex){
        Stack stack = stacks[stackIndex];
        if (stack.isEmpty()) throw new EmptyStackException();
        int top = stack.getLastDataIndex();
        int result = stackAry[top];
        stackAry[top] = 0;
        stack.top--;
        return result;
    }

    int peek(int stackIndex){
        Stack stack = stacks[stackIndex];
        if (stack.isEmpty()) throw new EmptyStackException();
        return stackAry[stack.getLastDataIndex()];
    }

    void retireve(){
        for (Stack stack : stacks){
            if (stack.isEmpty()) continue;
            int index = stack.start;
            while (index != stack.getLastDataIndex()){
                System.out.print(stackAry[index] + " ");
                index = nextIndex(index);
            }
            System.out.println();

        }
    }

}
```
</details>
<br>

순차 자료구조를 이용한 스택은 배열을 사용하여 구현하기는 쉽고, 데이터 저장/읽기 속도가 빠르다. 하지만 물리적으로 크기가 고정된 배열을 사용하기 때문에 스택의 크기를 변경하기가 어렵고, 메모리의 낭비가 생길 수 있다는 문제가 있다. 

## 3. 연결 자료구조 방식을 이용한 Stack의 구현

연결 자료구조 방식의 단순 연결 리스트를 이용하여 스택을 구현한다. 연결 자료구조 방식은 첫번째 노드에 계속 삽입이 되면서, 참조변수의 값이 계속 바뀌는 구조이다. 이때의 참조변수는 top을 의미하고, **top은 첫번째 Node**를 의미한다.

<details>
<summary>연결 자료구조 방식을 이용한 Stack 알고리즘</summary>

```java
class Stack<T>{

    Node<T> top;

    class Node<T>{
        T data;
        Node<T> link;

        Node(){}
        Node(T data){this.data = data;}
    }

    Stack(){
        top = new Node<T>();
    }

    boolean isEmpty(){return this.top.link == null;}

    void push(T data){
        Node<T> node = new Node<>(data);
        node.link = this.top.link;
        this.top.link = node;
    }

    T pop(){
        if (isEmpty()) throw new EmptyStackException();
        T data = this.top.link.data;
        this.top.link = this.top.link.link;
        return data;
    }

    T peek(){
        if (isEmpty()) throw new EmptyStackException();
        return this.top.link.data;
    }
    
}
```
</details>
<br>

---

## Reference

- 자바로 배우는 자료구조 방식