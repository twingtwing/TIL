# Tree
    ✍️ Tree는 비선형 자료구조 중에서 자료들간에 계층 관계를 가지는 계층형 자료구조(Hierarchical Data Structure)다.

## 1. Tree의 구조
- 트리를 구성하는 원소를 Node라고 하고, Node를 연결하는 선을 간선(edge)라고 한다. Tree의 시작노드를 Root Node라 하고, level 0 이다. 
- 노드가 가지는 서브트리 혹은 자식노드의 수를 그 노드의 차수(degree)라 한다.
- 같은 부모 노드를 공유하는 Node를 형제노드(Sibling Node)라고 한다. 
- 자식노드가 없는 Node를 Leaf Node라고 한다.
- 자식노드들은 각자 독립하여 새로은 Tree를 구성 할 수 있기 때문에, 각 노드는 자식 노드 수만큼 서브트리를 가진다.
- 여러 Tree의 집합을 Forest라고 한다. N개의 서브트리를 가진 Root Node를 제거하면 n개의 분리된 Tree가 생기고, 그 Tree들은 포리스트가 된다.

## 2. Tree 종류
- [Binary Tree](Binary_Tree.md) : Child Node가 최대 2개인 Tree를 이진트리라고 한다.  
    ⬌ Ternary Tree
- [Binary Search Tree](Binary_Search_Tree.md) : Child Node가 최대 2개이면서,  Left Child Node < Right Child Node라는 규칙을 가지고 있는 Tree를 이진 검색트리라고한다.
- Balanced Tree : 한쪽으로 치우치지 않은 Tree (ex, re-black tree/AVL tree)  
    ⬌ UnBalanced Tree
- [Heap](Heap.md) : 최댓값이랑 최솟값을 빠르게 검색하게 하기 위해 만든 완전 이진트리이다.
- [Tries](Tries.md) : 문자열에서 검색을 빠르게 하기 위해 만든 Tree

<br>

---

## Reference

- 자바로 배우는 자료구조 방식