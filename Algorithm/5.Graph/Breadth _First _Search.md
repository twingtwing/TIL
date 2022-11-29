# Breadth - First - Search(BFS : 넓이 우선 방법)
    ✍️ BFS는 시작 정점으로부터 인접한 정점들을 차례대로 탐색하는 방법이다.
너비 우선 탐색은 시작 정점으로부터 인접한 정점들을 모두 차례로 방문한 후 방문 했던 정점을 다시 시작점으로 하여 인접한 정점들을 차례로 방문하는 방법으로, 가까운 정점들을 먼저 방문하여 멀리있는 정점들은 나중에 방문하는 순회 방법이다.

## 1. Queue을 이용하여 구현
가까운 정점을 먼저 방문하고, 멀리있는 정점을 나중에 방문해야하기 때문에 **선입선출 구조를 갖는 Queue**를 사용한다.  
　　[ BFS - Queue 순서 ]
1) 시작정점x를 결정하여 방문  
2) 정점 x에 인접한 정점들 중에서  
    - 방문하지 않은 인접정점이 있으면 차례로 방문하면서 큐에 enQueue한다.
    - 방문하지 않은 인접정점이 없으면 큐를 deQueue하여 구한 정점을 x로 설정하고, 다시 (2)를 반복한다.  

3) 큐가 공백이 될때까지 (2)를 반복한다.  

<details>
<summary>Breadth First Search - Queue 알고리즘</summary>

```java
```
</details>        
<br>

## 2. BFS 변형

### 2.1 BinarySearchTree BFS 변형

<details>
<summary>BinarySearchTree BFS 변형 알고리즘</summary>

```java
```

---

## Reference

- 자바로 배우는 자료구조 방식