# Seletion Sort

    선택정렬은 전체 원소들 중에서 기준 위치에 맞는 원소를 선택하여 자리를 교환하는 방식으로 정렬한다. 

배열을 순회하면서 최솟값 혹은 최댓값을 찾아서 위치를 교환하는 과정을 반복한다.

전체 원소중에서 가장 작은 원소를 찾아서 선택하고  첫번째 원소와 자리를 교환한다. 그 다음 두 번째로 작은 원소를 찾아 선택하여 두번째 원소와 자리를 교환하고, 차례대로 교환하는 과정을 마지막까지 반복하면서 선택 정렬을 완성한다.   

배열을 돌면서 최솟값을 맨 앞 index와 위치와 계속 변경한다. 그 후, 맨 앞 index를 제외하고 순회하고, 마지막 index차례가 올때까지 반복한다.

전체 비교 횟수는 n(n-1)/2이기 때문에 <u>**선택 정렬의 시간 복잡도는 O(n<sup><small>2</small></sup>)**</u>이 된다.

<details>
<summary>Selection Sort 알고리즘</summary>

```java
private static void selectionSort(int [] ary, int index){
    if (index >= ary.length - 1) return;
    int min = index;
     // 가장 작은 최솟값을 찾음
    for (int i = index + 1; i < ary.length; i++)  if (ary[min] > ary[i]) min = i;
    swap(ary, index, min);
    selectionSort(ary, index + 1);
}

private static void swap(int [] ary, int prev, int next) {
    int tmp = ary[prev];
    ary[prev] = ary[next];
    ary[next] = tmp;
}
```
</details>    
<br>