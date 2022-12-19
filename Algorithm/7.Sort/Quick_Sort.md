# Quick Sort

퀵정렬은 기준값을 중심으로 분할하고 작은값은 왼쪽, 큰 값은 오른쪽 부분 집합으로 재배치하는 방식으로 정렬한다.

퀵정렬은 정렬할 전체 원소에 대해서 정렬을 수행하지 않는다. 먼저 기준값을 중심으로 전체 원소들을 왼쪽 부분집합과 오른쪽 부분집합으로 분할(divide)한다. 왼쪽 부분집합에는 기준값인 피봇(pivot)보다 작은 원소들을 이동시키고, 오른쪽 집합에는 기준값보다 큰 원소들을 이동시킨다. 부분집합의 크기가 1 이하가 될때까지 분할 작업을 순환적으로 반복하면서 피봇의 왼쪽 부분집합과 오른쪽 부분집합을 정렬하는 방법을 반복하면서 전체 원소들을 정렬한다.   
퀵정렬은 버블정렬은 인접한 두개의 원소를 비교하여 자리를 교환하기 때문에 원소가 이동하는 거리가 1이되어 자기 자리를 찾기까지 비교횟수와 자리교환횟수가 많음점을 개선하여 자기자리에 최대한 가까이 이동시켜서 비교횟수와 자리교환횟수를 줄인 정렬 방법이다.

분할하면서 이동횟수가 반으로 줄어들기 때문에  <u>**퀵 정렬의 시간 복잡도는 O(nlog<sub><small>2</small></sub>n)**</u>이 된다.

정렬이 되어 있지 않은 배열에 임의의 값을 잡아서 오른쪽은 큰값으로, 왼쪽은 작은값으로 재배치되면,
작은쪽에서 또 임의값을 정해서 재배치 하는 정렬 즉, 파티션을 계속 나눠서 재배치하면서 정렬하는 알고리즘,.,,???
=> 시간복잡도 : O(nlogn) <= 평균적으로 걸리는 것이고, 더 빨리 걸릴수도 있고, 최악으로는  O(n^2)가 걸릴수도 있다.(기준값을 최소 혹은 최대로 계속 잡을 경우)
=> 이진검색트리와 비슷하기에 logn이 걸린다.
=> partitioning을 하면서 start end 두개의 포인터로 앞에서 뒤로 가면서 pivot값과 비교해서 start와 end의 위치를 바꾼다
=> start가 가면서 큰값을 발견하면 멈추가, end도 가다가 pivot보다 작은 값을 발견하면 start와 end를 변경한다.

<details>
<summary>Quick Sort 알고리즘</summary>

```java
private static void quickSort(int [] ary) {quickSort(ary, 0, ary.length -1);}

private static void quickSort(int[] ary, int start, int end) {
    // 정렬 후 기준값 out
    int point = partition(ary,start, end);
    // 왼쪽이 1개 밖에 없을 경우(start = point -1), 왼쪽 정렬할 필요가 없음
    if (start < point - 1) quickSort(ary, start, point-1);
    // 오른쪽이 1개 밖에 없을 경우(end = point), 오른쪽 정렬할 필요가 없음
    if (point < end) quickSort(ary, point, end);
}

private static int partition(int[] ary, int start, int end) {
    int pivot = (start + end) / 2;
    // start, end 2개의 포인터가 앞, 뒤 양쪽에서 오면서 값을 비교하고
    // 양쪽 다 변경해야하는 인덱스를 도착했을 때, 위치를 변경한다.
    while(start <= end){
        // 기준값보다 큰 값을 찾을 때까지 인덱스 변경
        while(ary[start] < ary[pivot]) start ++ ;
        // 기준값보다 작은 값을 찾을 때까지 인덱스 변경
        while (ary[end] > ary[pivot]) end --;

        if (start <= end){
            swap(ary, start, end);
            start ++;
            end --;
        }

    }
    // 마지막에는 start = end = pivot 위치에 도달함 ?
    return pivot;
}

private static void swap(int[] ary, int prev, int next) {
    int tmp = ary[prev];
    ary[prev] = ary[next];
    ary[next] = tmp;
}
```
</details>    
<br>
