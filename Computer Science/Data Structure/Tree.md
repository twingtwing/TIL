# Tree
> 비선형 자료구조로 자료들간의 계층 관계를 가지는 계층형 자료구조

## 📌 트리(Tree)란?

          A : Root, Level 0
        /   \
      B       C
     / \     / \
    D   E   F   G
                 \
                  H : Leaf


#### 구조
- Root Node : 최상단 Node
- Parent / Child Node (부모 / 자식 노드) : Node의 바로 위 / 아래에 연결된 노드
- Sibling Node (형제 노드) : 같은 부모 노드(Parent Node)를 가지고 있는 노드
- Leaf Node (단말 노드) : 자식노드를 가지고 있지 않은, 가장 끝 단의 Node  
- Edge (간선) : 노드를 연결하는 선
- Degree (차수) : 노드가 가지는 서브트리 혹은 자식 노드의 갯수
- Level : 루트 노드부터 특정 노드까지의 경로에 존재하는 간선의 수, 루트 노드는 level 0 이다.
- Height : 루트 노드부터 가장 멀리 떨어진 노드까지의 경로에 존재하는 간선의 수
- SubTree : 특정 노드와 해당 노드의 자손들로 이루어진 트리구조, 각각의 노드들은 자식 노드 수만큼 서브트리를 가진다.

#### 특징
- 계층 구조 : 트리는 부모 - 자식 관계를 가진 계층 자료구조이다. 
- Graph : Tree는 사이클이 없는 단순 연결 그래프 자료구조이다.
- 경로 : 비순환 구조이기 때문에, 임의의 두 노드 간에 경로는 오직 하나의 경로만 가진다.

#### 구현
graph 링크 달기

## 📌 트리 순회 (Tree Traversal)
트리 순회란 모든 노드를 한 번씩 모두 방문하는 방법을 말한다.

#### 전위 순회 (Pre-Order)

    현재 Node ⇒ 왼쪽 SubTree ⇒ 오른쪽 SubTree

#### 중위 순회 (In-Order)

    왼쪽 SubTree ⇒ 현재 Node ⇒ 오른쪽 SubTree


#### 후위 순회 (Post-Order)

    현재 Node ⇒ 오른쪽 SubTree ⇒ 왼쪽 SubTree


## 📌 트리(Tree) 종류

### [Binary Tree](Binary_Tree.md) 
자식 노드가 최대 2개인 Tree를 이진 트리라고 한다.

### [Binary Search Tree](Binary_Search_Tree.md) 
자식 노드가 최대 2개이면서, 왼쪽 자식 < 오른쪽 자식 관계를 가지는 Tree를 이진 검색 트리라고 한다.

### [Binary Heap](Heap.md)
최대값 혹은 최솟값 탐색을 빠르게 하기 위해 만든 완전 이진 트리 기반의 자료구조를 이진 힙 이라고 한다.

### Balanced Tree ⬌ UnBalanced Tree

               ◯ : root                 ◯ : root
             /     \                   /     \
           ◯       ◯               ◯       ◯
          /  \     /  \             /       
        ◯    ◯ ◯    ◯         ◯     
        /             /          /              
      ◯            ◯         ◯            
         Balanced Tree             UnBalanced Tree

#### 균형 트리
트리의 모든 노드들이 균형적으로 배치되어 있는 Tree  
균형 트리는 모든 노드의 왼쪽 서브트리와 오른쪽 서브트리 높이 차이가 크지 않다.

Ex, Red - Black Tree, AVL Tree

#### 비균형 트리
트리의 모든 노드들이 한 쪽으로 치우쳐져 있는 Tree  
비균형 트리는 모든 노드의 왼쪽 서브트리와 오른쪽 서브트리 높이 차이가 크다.

### Trie
Trie는 문자열 탐색에 특화된 자료구조로, 각 Node에 Key - Value 형식으로 데이터를 저장하여 문자열을 효율적으로 탐색할 수 있는는 자료구조이다.

               [ Root ] 
               /     \                
              A       O             
             /      /   \           
            N      N     R 
          /   \     \                
         D     T     E : (key : E - value : ONE)
                 Trie     

Root는 공백으로 표시하고, 자식 노드들 부터는 Key - Value 형식 데이터를 저장한다. 루트 노드에서 시작하여 하위 노드를 따라 내려가면서 마지막 노드에 도달하면 검색하고자 했던 데이터가 해당 노드에 저장되어 있다.  
문자열 탐색 시에 Trie에 문자를 저장하고 탐색하게 되면, 문자열 길이(M) 시간만 필요하기 때문에 O(M)의 시간 복잡도를 가진다.


## Reference

- [자바로 배우는 자료구조 방식](https://product.kyobobook.co.kr/detail/S000001636199)
- [엔지니어 대한민국](https://www.youtube.com/@eleanorlim)