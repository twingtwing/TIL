# Heap
    ✍️ 최댓값이랑 최솟값을 빠르게 검색하게 하기위한 완전이진트리를 기본으로 한 자료구조
## 1. Heap
> Max Heap : 가장 작은 key값이 Root에 위치하고, 부모노드 key값 ≤ 자식노드 key값 관계를 가짐  
Min Heap : 가장 큰 key값이 Root에 위치하고, 부모노드 key값 ≥ 자식노드 key값 관계를 가짐  

일반적으로 힙은 최대 힙을 의미하면, 같은 키값의 중복을 허용한다.

## 2. Heap의 연산     
한번 갈수록 가야할길이 절반으로 줄기 때문 최대 O(logn)의 시간이 걸린다.
### 2.1 삽입 연산
힙에서의 삽입연산은 완전이진트리의 형태를 유지하기 위해서 현재의 마지막 노드(leaf)의 다음 자리를 삽입할 노드를 임시 저장한다. 그 후, 최대 힙 혹은 최소 힙이 되도록 삽입할 노드의 키값과 부모노드의 키값을 비교하면서 재구성한다.  
### 2.2 삭제 연산
힙에서의 삭제연산은 언제나 루트노드에 있는 원소를 삭제하여 반환한다. 그러므로 최대 힙에서의 삭제연산은 키값이 가장 큰 원소를 삭제하여 반환한다. 최소힙은 가장 작은 원소를 삭제하여 반환한다.  
그 후에는 완전 이진트리로 재구성하기 위해 가장 마지막 노드가 있던 자리를 제거하고, Root Node에 임시 저장한다. 자식노드와 비교해서 재구성작업을 해야한다.

## 3. 순차 자료구조 방식을 이용한 Heap의 구현
힙에서의 삽입/삭제 연산에서 어느 위치에서든지 부모노드를 쉽게 찾아야 하기 때문에 1차원 배열의 순차 자료구조방식을 이용하여 힙을 표현한다.  
Heap은 완전 이진 트리이기 때문에 배열의 메모리 문제가 발생하지 않는다.

<details>
<summary>순차자료구조 방식을 이용한 Heap 알고리즘</summary>

```java
class Heap{
    private int heapSize;
    private int itempHeap[];

    public Heap(int size){
        heapSize = 0;
        itempHeap = new int[size];
    }

    public void insertHeap(int data){
        int i = ++heapSize;
        while ((i != 1) && (data > itempHeap[i/2])){
            itempHeap[i] = itempHeap[i/2];
            i /= 2;
        }
        itempHeap[i] = data;
    }

    public int getHeapSize(){
        return this.heapSize;
    }

    public int deleteHeap(){
        int parent, child;
        int data, temp;
        data = itempHeap[1]; // 인덱스 계산을 용이하기 위해 인덱스 0번을 비워두고, 인덱스 1번을 root로 한다.
        temp = itempHeap[heapSize--];
        parent = 1;
        child = 2;

        while (child<=heapSize){
            if ((child < heapSize) && (itempHeap[child] < itempHeap[child+1])) child++;
            if (temp >= itempHeap[child]) break;
            itempHeap[parent] = itempHeap[child];
            parent = child;
            child += 2;
        }
        itempHeap[parent] = temp;
        return data;
    }

    public void printHeap(){
        for (int i =1; i<=heapSize; i++){
            System.out.printf("[%d] ",itempHeap[i]);
        }
        System.out.println();
    }
}
```
</details>
<br>

---

## Reference

- 자바로 배우는 자료구조 방식