# Stack  
> 데이터를 쌓아 올리는 형태의 선형 자료구조

## 📌 스택(Stack)이란?
Stack은 top으로 정한 한 곳에서만 데이터를 쌓을 수 있고, 접근하도록 제한하여 만든 자료구조이다. 따라서, 스택은 시간순서에 따라 자료가 쌓이고, 삭제 할때는 가장 최근에 삽입된 데이터가 가장 먼저 삭제되는 **후입선출**(LIFO, Last-In-First-Out)의 구조를 가진다. 

    +-----------+
    |   데이터   |
    +-----------+ ↴
                +-----------+
                |   데이터   | ⇐ TOP [삽입,삭제가 발생하는 곳]
                +-----------+
                |   데이터   |
                +-----------+
                |   데이터   |
                +-----------+ 


#### 특징
- 후입선출(LIFO) : 가장 최근 삽입된 데이터가 가장 먼저 제거된다. 
- 삽입, 삭제가 Top으로 정한 곳에서만 이루어진다.

#### 기본 연산
- Push : 스택의 최상단(Top)에 데이터를 삽입
- Pop : 스택의 가장 최근 데이터 제거
- Peek : 스택의 최상단(Top) 데이터 반환
- IsEmpty : 비어있는지를 True, False로 반환
- Size : 저장된 데이터의 갯수를 반환

## 📌 스택(Stack) 구현

### 순차 자료구조
스택이 1차원 배열을 통해 구현되는 방식은 데이터가 순차적으로 쌓이는 순서를 배열의 인덱스로 표현한다. 마지막 데이터의 인덱스를 top이라는 변수에 저장하여 삽입 과 삭제가 마지막 데이터에서만 이루어지도록 구현한다.

<details>
<summary>Stack Code</summary>

```java
class Stack{
    int top;
    int [] stack;

    Stack(int len){
        top = -1;
        stack = new int[len];
    }

    int size(){
        return top + 1;
    }

    boolean isEmpty(){
        return top == -1;
    }

    boolean isFull(){
        return size() == stack.length;
    }

    void push(int data){
        if (isFull()) throw new IllegalStateException("Stack is Full");
        stack[++top] = data;
    }

    int pop(){
        if (isEmpty()) throw new IllegalStateException("Stack is Empty");
        return stack[top--];
    }

    int peek(){
        if (isEmpty()) throw new IllegalStateException("Stack is Empty");
        return stack[top];
    }

}
```
</details>
<br>


                     삽입                 삭제 
    [ 3, 7, 2, 0, 0 ] ⇢ [ 3, 7, 2, 9, 0 ] ⇢ [ 3, 7, 2, 9, 0 ] 
            ↑                       ↑                ↑
           top = 2                 top = 3          top = 2

### 연결 자료구조 
스택은 연결 리스트을 통해 구현 되는 방식은 데이터가 순차적으로 쌓이는 순서를 Node가 참조되는 순서로 표현한다. 첫번째 Node를 top이라는 참조변수에 저장하여 삽입 과 삭제가 첫번째 노드에서만 이루어지도록 구현한다.

<details>
<summary>Stack Code</summary>

```java
class Stack{

    Node top;

    class Node{
        int data;
        Node link;

        Node(){}
        Node(int data){this.data = data;}
    }

    Stack(){
        top = new Node();
    }

    boolean isEmpty(){return top.link == null;}

    void push(int data){
        Node node = new Node(data);
        node.link = top.link;
        top.link = node;
    }

    int pop(){
        if (isEmpty()) throw new EmptyStackException();
        int data = top.link.data;
        top.link = top.link.link;
        return data;
    }

    int peek(){
        if (isEmpty()) throw new EmptyStackException();
        return top.link.data;
    }
    
}
```
</details>

#### 삽입

[1] 삽입 전

    +-----------+-----------+
    |  데이터 A  |   NULL    | 
    +-----------+-----------+
                ↓
    +-----------+-----------+        +-----------+-----------+
    |  데이터 B  |   주소 C  |   --   |  데이터 C  |    NULL   |
    +-----------+-----------+        +-----------+-----------+                      top : Node B

[2] 삽입 후

    +-----------+-----------+        +-----------+-----------+        +-----------+-----------+
    |  데이터 A  |   주소 B  |   --   |  데이터 B  |   주소 C  |   --   |  데이터 C  |    NULL   |
    +-----------+-----------+        +-----------+-----------+        +-----------+-----------+
                                                                                    top : Node A


#### 삭제

[1] 삭제 전

    +-----------+-----------+        +-----------+-----------+        +-----------+-----------+
    |  데이터 A  |   주소 B  |   --   |  데이터 B  |   주소 C  |   --   |  데이터 C  |    NULL   |
    +-----------+-----------+        +-----------+-----------+        +-----------+-----------+
                                                                                    top : Node A

[1] 삭제 후

    +-----------+-----------+
    |  데이터 A  |   주소 B  | 
    +-----------+-----------+
                ↑
    +-----------+-----------+        +-----------+-----------+
    |  데이터 B  |   주소 C  |   --   |  데이터 C  |    NULL   |
    +-----------+-----------+        +-----------+-----------+                      top : Node B

### 🏷️ 응용 분야

### 틀렸는지 맞았는지 정보 확인하고 진행하기


## Reference

- [자바로 배우는 자료구조 방식](https://product.kyobobook.co.kr/detail/S000001636199)
- [엔지니어 대한민국](https://www.youtube.com/@eleanorlim)