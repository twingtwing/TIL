# Binary Search Tree
    검색을 위한 자료구조로 저장할 데이터의 크기에 따라 Node를 나열한 Tree를 이진 검색 트리다.
## 1. 이진 검색 트리의 구조
- 모든 원소는 서로 다른 유일한 key(검색키)를 갖는다.
- Left Child Node key값 < Root Node key값 < Right Child Node key값 
- 왼쪽 서브트리와 오른쪽 서브트리 모두 이진 검색 트리이다.

## 2. 이진 검색 트리의 연산
=>> 그림으로 간략하게 표시
### 2.1 검색 연산
탐색은 항상 Root Node에서 시작하므로, 먼저 키값x와 루트노드의 키값을 비교한다. 루튼드에서 원소를 찾을때까지 단말노드로 내려간다.
    - ( 키값 x = 루트노드의 키값 )인 경우 : 원하는 원소를 찾았으므로 탐색연산 성공
    - ( 키값 x < 루트노드의 키값 )인 경우 : 루트 노드의 왼쪽 서브 트리에 대해서 탐색 연산 수행
    - ( 키값 x > 루트노드의 키값 )인 경우 : 루트 노드의 오른쪽 서브 트리에 대해서 탐색 연산 수행
### 2.2 삽입 연산
이진 탐색 트리에 원소를 삽입하려면 먼저 같은 원소가 있는지 확인하기 위해서 탐색을 해야한다. 탐색에 성공하면, 이미 같은 원소가 있으면 삽입연산을 수행하지 않고, 실패하면, 크기롤 비교하여 마지막 단말노드까지 key값이 같은 원소가 없는 것이므로 해당 단말노드의 자식 노드에 원소를 삽입한다. 오른쪽인지 왼쪽인지는 키값을 비교연산을 통해서 선택한다.
### 2.3 삭제 연산
삽입과 마찬가지로 탐색 후 삭제를 해야한다. 삭제 할 노드는 자식 노드의 수에 따라 결정된다.
    - 삭제할 노드가 단말노드인 경우 (차수가 0 인 경우)  
    : 삭제할 노드가 단말 노드인 경우에는 노드를 삭제하고, 부모노드의 링크 필드를 null로 설정한다.
    - 삭제할 노드가 한 개의 자식 노드가 잇는 경우 (차수가 1인경우)  
    : 해당 노드를 삭제하고, 자식노드를 부모노드 위치로 올려준다.
    - 삭제할 노드가 두 개의 자식 노드가 있는 경우 (차수가 2인 경우)   
    : 자손노드의 키값은 이진 탐색 트리 특성에 따라서 왼쪽 서브 트리에 있는 노드을의 키값보다 커야하고, 오른쪽 서브트리에 있는 노드들의 키값보다는 작아야한다. 그러므로 후계자 노드는 삭제할 조상노드의 왼쪽 서브트리에서 가장 큰 자손노드 또는 오른쪽 서브트리에서 가장 작은 자손 노드가 되어야 한다.  
    이진 탐색트리의 정의를 생각해봤을 때, 왼쪽 서브트리에서 가장 큰 키값의 노드를 탐색하는 작업은 왼쪽 서브트릐의 오른쪽 링크를 따라 계속이동하여 오른쪽 링크 필드가 null인 노드, 즉 가장 오른쪽에 있는 노드를 찾는 작업이 된다. 그리고 서브트리에서 가장 작은 키 값의 노드를 탐색하는 작업은 오른 쪽 서브트리에서 왼쪽 링크를 따라 계속 이동하여 왼쪽 링크 필드가 null인 노드, 즉 가장 왼쪽에 있는 노드를 찾는 작업이 된다.

---

## Reference

- 자바로 배우는 자료구조 방식