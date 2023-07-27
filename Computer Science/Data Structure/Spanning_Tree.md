# 📑 Spanning Tree

## 🏷️ 신장 트리(Spanning Tree) 란?
> 무방향 그래프에서 모든 노드를 포함하는 부분 그래프이며, 사이클이 없는 단순 연결 그래프(Tree)이다.

#### 특징
- N개의 모든 정점과 N-1개의 간선으로 이루어져 있다.
- 사이클과 방향이 존재하지 않는다.
- 연결 그래프 탐색을 통해 신장트리를 생성 할 수 있다.
    - DFS를 통해 생성된 신장 트리 : 깊이 우선 신장 트리(Depth First Spanning Tree)
    - BFS를 통해 생성된 신장 트리 : 너비 우선 신장 트리(Bredth First Spanning Tree)

## 🏷️ Minimum Spanning Tree 란?
> 최소 신장 트리는 가중치 그래프에서 간선에 주어진 가중치의 합이 최소인 신장트리를 말한다.

### MST 구현

#### [Kruskal Algorithm](/Algorithm/MST.md#🏷️-kruskal-algorithm)
크루스칼 알고리즘은 가중치에 따라 정렬된 간선 중에서 최소 가중치의 간선을 추가하면서 트리를 확장해 나가는 알고리즘이다.

#### [Prime 알고리즘](/Algorithm/MST.md#🏷️-prime-algorithm)
프림 알고리즘은 하나의 정점에서 시작하여 가중치에 따라 최소 가중치의 간선을 추가하면서 트리를 확장해 나가는 알고리즘이다.

### 🏷️ 응용 분야

## Reference

- [자바로 배우는 자료구조 방식](https://product.kyobobook.co.kr/detail/S000001636199)
- [사이트 링크](https://www.tutorialspoint.com/data_structures_algorithms/spanning_tree.htm)