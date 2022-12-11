# Graph 
    ✍️ Graph는 원소들간의 관계를 표현하는 망구조를 갖는 자료구조이다.
## 1. Graph란?
그래프는 연결할 객체를 나타내는 정점(vertax)과 객체를 연결하는 간선(edge)의 집합으로 구성된다. 그래프 G를  G=(V,E)로 정의하는데 V는 그래프에 있는 정점들의 집합을 의미하고, E는 정점을 연결하는 간선들의 집합을 의미한다.  

<img width="350" src="../../Image/Graph.png" title="Graph Data Structure">   

<small>출처 : <cite>https://en.wikipedia.org/wiki/Vertex_(graph_theory)</cite> </small>

그래프는 선형자료구조나 트리가 표현할 수 없는 모든 연결 구조들을 표현할 수 있기 때문에 여러 분야에서 폭 넓게 사용할 수 있다.  

### 1.1 Graph 특징
- 방향 그래프에서 정점에 부속된 간선의 방향에 따라 정점을 향하면 진입차수(in-degree), 정점을에서 나가면 진출차수(out-degree)로 한다. 방향 그래프에서 정점의 차수는 (진입차수 + 진출차수) 합친 값이다. 
- 정점 a에서 b까지 간선으로 연결된 정점을 순서대로 나열한 리스트를 정점 a → b 까지의 경로(path)라고 한다. 이때 구성하는 간선의 수는 경로 길이가 된다.  

## 2. Graph 종류
그래프는 방향성과 연결 정도에 따라 여러 종료가 있다.
### 2.1 Directed Graph ⟷ Undirected Graph  
간선에 방향이 있는 Graph를 **다이그래프(digraph)** 혹은 **방향그래프(Directed Graph)**라고 한다.  
방향 그래프에서 간선은 a → b를 <a,b>라고 하며, a를 꼬리(tail), b를 머리(head)라고 한다. 방향 그래프에는 방향이 있기 때문에, <a,b>와 <b,a>는 서로 다른 간선으로 취급한다. 방향 그래프 G의 정점의 집합 V를 V(G) = { a,b }로, 간선의 집합을 E(G) = { <a,b>,<b,a> }로 표현할 수 있다.  

두 정점을 연결하는 간선에 방향이 없는 Graph를 **무방향그래프**라고 한다.  
정점 a와 정점 b을 연결하는 간선을 (a,b)로 표현한고, 방향이 없는 그래프이기에 (a,b)와 (b,a)는 같은 간선으로 취급한다. 무방향 그래프 G의 정점의 집합 V를 V(G) = { a,b }로, 간선의 집합을 E(G) =  { (a,b) }로 표현할 수 있다.

### 2.2 Cyclic ⟷ Acyclic  
모든 경로는 단순 경로라고 하고, 시작정점과 마지막 정점이 같은 경로를 사이클(Cycle)이라 한다.  

사이클이 없는 그래프를 DAG(Directed Acyclic Garph) 혹은 비순환그래프라고 한다. 

### 2.3 Complete Graph ⟷ Subgraph
한 정점에서 다른 모든 정점을 연결되어 최대의 간선 수를 가지는 Graph를 완전 그래프라고 한다. 정점이 n개인 무방향 그래프의 최대 간선수는 (n(n-1))/2개 이며, 방향 그래프의 경우 n(n-1)개가 된다.  

Complete Graph에서 일부의 정점/간선을 제외하여 만든 Graph를 부분그래프라고 한다. 부분그래프의 정점 집합과 간선집합은 완전그래프의 정점 집합과 간선집합에 포함되는 관계를 가진다.

### 2.4 Weight graph
정점을 연결하는 간선에 가중치를 할당하는 Graph를 가중 그래프 혹은 Network라고 한다.

### 2.5 Connected Graph ⟷ Disconnected Graph
Path(경로) 유무에 따라 연결 그래프(Connected Graph)와 단절 그래프(Disconnected Graphh) 라고 한다.

## 3. Graph 구현
### 3.1 순차 자료구조 방식을 이용하여 Graph를 구현 : Adjacent Matrix
    👉 그래프를 표(2차원 배열)에 구현하는 방법
N개의 정점을 가진 그래프를 구성하는 간선의 유무를 저장하는 방법으로 N x N 정방행렬을 사용한다. 정점이 인접하면 1, 아니면 0으로 저장하여 간선의 유무를 표현한다. 이렇게 그래프를 표현한 행렬을 인접 행렬(Adjacent Matrix)이라고 한다.

- 자기자신으로의 자체 간선은 있을 수 없으므로 대각선을 항상 0 값을 가진다.
- 무방향 그래프에서는 대각선을 중심으로 양쪽은 값이 항상 같기 때문에 대칭을 이룬다.   
- 방향그래프에서는 서로 다른 간선으로 취급하기 때문에, 대칭을 이루지 않는다. 행 i의 합은 정점 i의 진출차수가 되고, 열 i의 합은 정점 i의 진입차수가 된다.   

단점 : N개의 정점을 가지는 그래프를 표현할려면, 간선의 개수에 상관없이 항상 N x N 개의 메모리를 사용하기 때문에 메모리 낭비 문제가 발생한다.

<details>
<summary>Adjacent Matrix 알고리즘</summary>

```java
class AdjMatrix{
    private int matrix[][] = new int[10][10];
    private int totalV = 0;

    public void insertVertex(){
        if (totalV < 10){
            totalV++;
        }
    }

    public void insertEdge(int val01, int val02){
        if (val01 < totalV && val02 < totalV){
            matrix[val01][val02] = 1;
        }
    }

    public void printMatrix(){
        for (int i = 0; i < totalV; i++){
            for (int j = 0; j<totalV; j++){
                System.out.printf("%2d", matrix[i][j]);
            }
            System.out.println();
        }
    }
}
```
</details>    
<br>

### 3.2 연결 자료구조 방식을 이용하여 Graph를 구현 : Adjacent List
    👉 각 정점에 대한 인접 정점들을 Linked List로 구현하는 방법
그래프를 구성하는.각 정점에 대한 참조변수를 배열로 구성하고, 각 정점에 대한 Head 노드는 인접 정점의 노드 번호에 대한 오름차순으로 정렬??하고 연결한 Linked List를 가리킨다. 이렇게 그래프를 표현한 리스트을 인접 리스트(Adjacent List)이라고 한다.  
N개의 정점과 X개의 간선을 가진 인접 리스트는 N개의 Head 노드 배열과 2X개의 노드가 필요하다. 방향그래프의 경우,  각 Head 노드에 연결되는 노드의 수는 각 정점 진출차수가 된다.

<details>
<summary>Adjacent List 알고리즘</summary>

```java
class Graph{

    Node [] nodes; // node들을 저장할 배열

    class Node {
        int data;
        boolean marked; // 방문 여부
        LinkedList<Node> adjacent; // 인접한 node
        Node(int data) {
            this.data = data;
            this.marked = false;
            adjacent = new LinkedList<>();
        }
    }

    Graph(int size){
        this.nodes = new Node[size];
        for (int i = 0; i < size; i++) nodes[i] = new Node(i);
    }

    void addEdge(int i1, int i2){
        Node n1 = this.nodes[i1];
        Node n2 = this.nodes[i2];
        if (!n1.adjacent.contains(n2)) n1.adjacent.add(n2);
        if (!n2.adjacent.contains(n1)) n2.adjacent.add(n1);
    }

}
```
</details>    
<br>

## 4. Graph 순회
>하나의 정점에서 시작하여 그래프에 있는 모든 정점을 한번씩 방문하는 것을 그래프 순회 또는 그래프 탐색이라 한다. 

### Search는 bfs가 유리??

### 4.1 [Depth - First - Search(DFS : 깊이 우선 방법)](Depth%20_First%20_Search.md) :  
깊이 우선 탐색은 시작 정점에서 한 방향으로 갈 수 있는 가장 먼 경로 까지 깊이 탐색하다가 더 이상 갈 곳이 없으면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아와서 반복하는 순회방법이다. Stack 혹은 재귀호출를 이용하여 구현한다.  
Tree의 경우에는 child Node 이어가면서 leaf까지 가고 다시 올라가서 다시 아래로 내려가는 방법이다. tree 검색 방법이었던 inorder, preorder, postorder들도 DFS에 속한다.

### 4.2 [Breadth - First - Search(BFS : 넓이 우선 방법)](Breadth%20_First%20_Search.md) 
너비 운선 탐색은 시작 정점으로부터 인접한 정점들을 모두 차례로 방문한 후 방문했던 정점을 다시 시작점으로 하여 인접한 정점들을 차례로 방문하는 방법이다. 가까운 정점들을 가장 먼저 방문하고, 멀리있는 정점들은 나중에 방문하는 순회 방법이다. Queue을 이용하여 구현한다.
Tree의 경우에는 level단위로 형제노드들을 차례로 검색하는 방법이다.

## 5. 신장트리와 최소 비용 신장 트리
트리는 사이클이 없는 연결 그래프이다.
사실 tree는 graph의 한종류이다.? tree는 graph에서 루트가 있고, 사이클이 없으며, 아래로만 흐르는 한방향이며, 들어오는 곳이 한개이다.? 그래프는 tree와는 달리 제약이 없다.  
그래프는 방향이 있을수도 없을수도 있다. tree는  Directed graph이다. 방향 그래프는 셀프엣지라고 자기자신을 가리키루도 있다.  

그래프에는 tree와는 달리 부모 자식 관계가 없다.

### 5.1 Spanning...?
Graph의 관점에서는 **Tree는 사이클이 없는 단순 연결 그래프**이다. N개의 정점으로 이루어진 무방향 그래프에서 N개의 모든 정점과 N-1개의 간선으로 만들어진 트리를 신장트리(Spanning Tree)라고 한다.  
연결그래프에서 순회를 하면 n-1개의 간선을 이동하면서 모든 정점을 방문하게 되므로 신장트리를 생성하게 된다. 깊이 우선탐색을 이용하여 생성된 신장트리를 깊이 우선 신장(Depth First Spanning Tree)라 하고, 너비 우선 탐색을 이용하여 생성된 신장트리를 너비 우선 신장 트리(Bredth First Spanning Tree)라고 한다.  

### 5.2 최소 비용 신장트리
가중치 그래프에서 간선에 주어진 가중치는 비용이나 거리,시간을 의미하는 값이 될 수 있다. 따라서 무방향 가중치 그래프에서 신장트리의 비용은 신장트리를 구성하는 간선들의 가중치의 합이되는데, 가중치의 합이 최소인 신장트리를 최소 비용 신장 트리(Minimum Cost Spnning Tree)라고 한다. 최소 비용신장트리를 만들기 위해 kruskal이 만든 알고리즘과 prime이 만든 알고리즘을 주로 사용한다. 
    - Kruskal 알고리즘  
    해당 알고리즘은 가중치가 높은 간서을 제거하면서 최소 비용 신장트리르 만드는 Kruskal 알고리즘1과 가중치가 낮은 간선을 삽입하면서 최소 비용 신장트리를 만드는 Kruskal알고리즘2가 있다.  
        (1) Kruskal알고리즘1  
        ㄱ. 그래프 g의 모든 간선을 가중치에 따라 내림차순으로 정리한다.
        ㄴ. 그래프 g에서 가중치가 가장 높은 간선을 제거한다. (이때, 정점을 그래프에서 분리시키는 간선은 제거할 수 없다. 이런경우에는 그 다음 높은 간선을 제거한다.)  
        ㄷ. 그래프 g에 n-1개의 간선만 남을때까지 (2)를 반복한다.  
        ㄹ. 그래프에 n-1개의 간선이 남게 되면 최소 비용 신장트리가 완성된다.  
        (2) Kruskal알고리즘2
        ㄱ. 그래프 g의 모든 간선을 가중치에 따라 오름차순으로 정리한다.
        ㄴ. 그래프 g에서 가중치가 가장 작은 간선을 삽입한다.. (이때, 삽입하면 사이클을 형성시키는 간선은 삽입할수없고, 그 다음 작은 간선을 삽입한다.)  
        ㄷ. 그래프 g에 n-1개의 간선만 남을때까지 (2)를 반복한다.  
        ㄹ. 그래프에 n-1개의 간선이 남게 되면 최소 비용 신장트리가 완성된다.  
    - Prime 알고리즘  
    해당 알고리즘은 간선을 정렬하지 않고, 하나의 정점에서 시작하여 트리를 확장해 나가는 방법이다.  
        ㄱ. 그래프 g에서 시작 정점을 선택한다.  
        ㄴ. 선택한 정점에 부속된 간선중에서 가중치가 가장작은간선을 연결하여 트리를 확장한다.  
        ㄷ. 이전에 선택한 정점과 새로 확장한 정점에 부속된 모든 간선중에 가장 작은 간선을 삽입한다.(이때까지 선택한 정점과 확장한 정점(누적된 정점)중에서 부속된 간선들에서 고른다.) 이때 사이클을 형성하는 간선은 삽입할 수 없다. 이런 경우에는 다음 작은 간선을 삽입한다.  
        ㄹ. 그래프 g에 n-1개의 간선만 남을때까지 (2)를 반복한다.  
        ㅁ. 그래프에 n-1개의 간선이 남게 되면 최소 비용 신장트리가 완성된다.  

<br>

---

## Reference

- 자바로 배우는 자료구조 방식