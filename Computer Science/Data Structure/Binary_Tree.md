# Binary Tree
>  Tree의 모든 Node의 차수가 2개 이하가 되도록 만든 자료구조

## 📌 이진 트리(Binary Tree) 란?

#### 특징
- 공백 노드 : 이진트리는 공백 노드 또한 노드로 취급한다. leaf 노드도 공백노드를 자식으로 가진것으로 취급한다.
- 간선 갯수 :  n개의 Node n개⇒ 항상 (n-1)개의 Edge, 공백노드도 노드로 취급하기 때문에 해당 규칙은 항상 준수한다.
- 노드 갯수 : 높이가 h인 이진트리가 공백노드를 제외하고 가질 수 있는 노드의 최소 갯수는 h + 1개, 최대 갯수는 2<sup><small>(h+1)</small></sup> -1 개 이다.

#### 종류

              ◯                      ◯                          ◯                          ◯ 
            /     \                 /     \                     /     \                     /     
          ◯       ◯             ◯       ◯                 ◯       ◯                 ◯      
         /  \                    /  \     /  \               /  \     /  \               /           
       ◯    ◯                ◯    ◯ ◯    ◯           ◯    ◯ ◯    ◯           ◯    
            /  \              /                                                       /            
          ◯    ◯          ◯                                                      ◯ 
       Full Binary Tree      Complete Binary Tree         Perfect Binary Tree         Skewed Binary Tree

- Full Binary Tree (정 이진트리)
    - 모든 Node가 자식 노드를 0개 혹은 2개를 가진다. 
- Complete Binary Tree (완전 이진트리)
    - 왼쪽부터 Node가 채워져 있고, 왼쪽이 채우기 전까지는 오른쪽 노드가 먼저 채워지지 않는다.
- Perfect Binary Tree (포화 이진 트리)
    - 모든 Node가 자식 노드를 2개를 가지고 있고, 단말노드의 Level이 모두 일치한다. 
    - 노드 갯수 
        - n개의 단말노드를 가질 때, Node의 수는 2 X n- 1개를 가진다.
        - 높이 h 를 가질 때, 2<sup><small>(h+1)</small></sup> -1 개를 가진다.
        - 높이 h 인 이진 트리 중에서 최대 갯수의 노드를 가진다.
- Skewed Binary Tree (편향 이진 트리)
    - 모든 노드들은 왼쪽/오른쪽 중 1개만을 서브트리로 가진다. 오른쪽 혹은 왼쪽으로 일직선 형태를 가진다.
    - 노드 갯수
        - 높이 h 를 가질 때, h + 1 개를 가진다.
        - 높이 h 인 이진 트리 중에서 최소 갯수의 노드를 가진다.


## 📌 이진 트리(Binary Tree) 구현

<details>
<summary>Binary Tree Code</summary>

```java
class Node{
    String data;
    Node left;
    Node right;

    Node(){}
    Node(String data){this.data = data;}
}

class BinaryTree{

    private Node root;

    public Node makeTree(Node left, Node right, String data){
        Node result = new Node(data);
        result.left = left;
        result.right = right;
        return result;
    }

    public Node getRoot() {
        return root;
    }

    public void setRoot(Node root) {
        this.root = root;
    }

    public void preOrder(){
        preOrder(this.root);
    }

    private void preOrder(Node node){
        if (node == null) return;
        System.out.print(node.data + " -> ");
        preOrder(node.left);
        preOrder(node.right);
    }

}
```
</details>
<br> 

## 📌 코테 유형


## Reference

- [자바로 배우는 자료구조 방식](https://product.kyobobook.co.kr/detail/S000001636199)
- [엔지니어 대한민국](https://www.youtube.com/@eleanorlim)