# Bubble Sort

    버블 정렬은 인접한 두개의 원소를 비교하여 자리를 교환하는 방식으로 정렬한다. 

첫번째 원소부터 마지막 원소까지 반복하면, 가장 큰 원소가 마지막자리로 정렬하게 된다. 마지막을 제외한 나머지 원소 중에서 이러한 과정을 반복하고, 나머지 원소가 없어지면 버블정렬을 완성한다.  
첫번째 원소부터 인접한 원소끼리 계속 자리를 교환하면서, 맨 마지막 자리로 이동하는 모습이 물방울 모양과 같다고해서 버블 정렬이라고 한다.

2개씩 바로 서로 비교하면서 정렬하면서 최댓값을 마지막 위치로 이동한다. 이러한 과정을 반복한다.

전체 비교 횟수는 n(n-1)/2이기 때문에 <u>**버블 정렬의 시간 복잡도는 O(n<sup><small>2</small></sup>)**</u>이 된다.

<details>
<summary>Bubble Sort 알고리즘</summary>

```java
private static void bubbleSort(int [] ary){bubbleSort(ary, ary.length - 1);}

private static void bubbleSort(int[] ary, int end) {
    if (end == 0) return;
    // 최댓값을 가장 끝으로 이동시킴
    for (int i = 0; i < end; i++) if (ary[i] > ary[i + 1]) swap(ary, i, i+1);
    bubbleSort(ary, end - 1);
}

private static void swap(int[] ary, int prev, int next) {
    int tmp = ary[prev];
    ary[prev] = ary[next];
    ary[next] = tmp;
}
```
</details>    
<br>
