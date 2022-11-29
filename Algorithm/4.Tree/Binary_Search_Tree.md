# Binary Search Tree
    ✍️ 검색을 위한 자료구조로 저장할 데이터의 크기에 따라 Node를 나열한 Tree를 이진 검색 트리다.
## 1. 이진 검색 트리의 특징
- 모든 원소는 서로 다른 유일한 key(검색키)를 갖는다.
- Left Child Node key값 < Root Node key값 < Right Child Node key값 
- 왼쪽 서브트리와 오른쪽 서브트리 모두 이진 검색 트리이다.

## 2. 순차 자료구조 방식을 이용히여 구현

> 시간 복잡도는 O(logN)

<details>
<summary>순차 자료구조 방식을 이용한 이진검색트리 알고리즘</summary>

```java
class BSTLinearList{

    private Node root;

    class Node{
        int data;
        Node left;
        Node right;
        Node(){}
        Node(int data, Node left, Node right){
            this.data = data;
            this.left = left;
            this.right = right;
        }
    }

    boolean isEmpty(){return this.root == null;}

    // 1. 배열로 insert 구현
    void insertArray(int [] ary){this.root = insertArray(ary, 0, ary.length-1);}

    Node insertArray(int [] ary, int start, int end){
        if (start > end) return null;

        int middle = (start + end)/2;

        return new Node(ary[middle],
                insertArray(ary,start,middle-1),
                insertArray(ary,middle+1, end));

    }

}
```
</details>
<br>

## 3. 연결 자료구조 방식을 이용히여 구현

> 시간 복잡도는 O(logN)

### 3.1 검색 연산
검색은 항상 Root Node에서 시작하므로, 먼저 검색값과 비교하면서, 루트노드에서 원소를 찾을때까지 단말노드로 내려간다.
- ( 키값 x = 루트노드의 키값 )인 경우 : 원하는 원소를 찾았으므로 탐색연산 성공
- ( 키값 x < 루트노드의 키값 )인 경우 : 루트 노드의 왼쪽 서브 트리에 대해서 탐색 연산 수행
- ( 키값 x > 루트노드의 키값 )인 경우 : 루트 노드의 오른쪽 서브 트리에 대해서 탐색 연산 수행

### 3.2 삽입 연산
이진 탐색 트리에 원소를 삽입하려면 먼저 같은 원소가 있는지 확인하기 위해서 검색연산을 수행해야 한다. 검색연산을 성공하면, 삽입을 수행하지 않는다. 실패하면, 현재 단말노드 위치에서 단말노드 key값과 비교연산을 통해서 오른쪽/왼쪽 자식노드에 삽입한다.  

삽입 연산의 시간 복잡도는 O(logN)이 된다.

### 3.3 삭제 연산
삭제 연산도 마찬가지로 검색 연산를 수행해야한다. 삭제할 노드는 자식노드의 수에 따라 달라진다. (Java의 경우 Node를 삭제하지 않아도 가비지컬렉션?이 알아서 처리한다.)  

삭제 연산의 시간 복잡도는 O(logN)이 된다.

1. 삭제할 노드가 단말노드인 경우 (차수가 0 인 경우)  
해당 노드를 삭제하고, 부모노드의 링크 필드를 null로 설정한다. 

2. 삭제할 노드가 한 개의 자식 노드가 잇는 경우 (차수가 1인경우)  
해당 노드를 삭제하고, 자식노드를 부모노드 위치로 올려준다.

3. 삭제할 노드가 두 개의 자식 노드가 있는 경우 (차수가 2인 경우)   
이진 검색 트리를 유지해야하기 때문에, 왼쪽 서브트리의 노드들보다 가장 큰 키값을 가져오거나, 오른쪽 서브트리보다 가장 작은 키값을 가져와서 삭제 노드 대신 교체 해주어야 한다.  
    - 왼쪽 서브트리에서 최댓값 : 왼쪽 서브트릐의 오른쪽 링크를 따라 계속이동하여 오른쪽 링크 필드가 null인 노드, 즉 가장 오른쪽에 있는 노드를 찾는 작업이 된다. 
    - 오른쪽 서브트리의 최솟값 : 오른 쪽 서브트리에서 왼쪽 링크를 따라 계속 이동하여 왼쪽 링크 필드가 null인 노드, 즉 가장 왼쪽에 있는 노드를 찾는 작업이 된다.

<br>
<details>
<summary>연결 자료구조 방식을 이용한 이진검색트리 알고리즘</summary>

```java
class BSTLinkedList{

    private Node root;

    class Node{
        int data;
        Node left, right;
        Node(){}
        Node(int data){this.data = data;}
    }

    boolean isEmpty(){return this.root == null;}

    // 1. 검색 연산
    public Node search(int data){
        if (isEmpty()) throw new NoSuchElementException();
        return search(this.root, data);
    }

    public Node search(Node node, int data){
        if (node == null || node.data == data) return node;
        if (node.data > data) return search(node.left,data);
        return search(node.right,data);
    }

    // 2. 삽입 연산
    public void insert(int data){this.root = insert(this.root, data);}

    private Node insert(Node node, int data) {
        if (node == null) return new Node(data);
        if (node.data > data) node.left = insert(node.left,data);
        if (node.data < data) node.right = insert(node.right,data);
        return node;
    }

    // 3. 삭제 연산
    public void delete (int data){
        if (isEmpty()) throw new NoSuchElementException();
        this.root = delete(this.root,data);
    }

    private Node delete(Node node, int data) {
        if (node == null) return node;
        if (node.data > data) node.left = delete(node.left,data);
        else if (node.data < data) node.right = delete(node.right,data);
        else{
            //경우 1. 자식이 없는 경우
            if (node.left == null && node.right == null) return null;

            // 경우 2. 자식이 한개 있는 경우
            else if (node.left == null || node.right == null) return node.left == null ? node.right : node.left;

            // 경우 3. 자식이 2개 있는 경우
            node.data = findMin(node.right); // link field 없이 data field만 가지고 와야함
            node.right = delete(node.right,node.data); // 값을 교체한 Node 삭제

        }
        return node;
    }

    private int findMin(Node node){
        if (node.left == null) return node.data;
        return findMin(node.left);
    }

}
```
</details>
<br>

---

## Reference

- 자바로 배우는 자료구조 방식