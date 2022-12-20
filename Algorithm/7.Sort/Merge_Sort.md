# Merge Sort

병합정렬은 여러개의 정렬된 자료의 집합을 결합하여 한 개의 정렬된 집합으로 만드는 방법이다. 병합 정렬은 전체 원소들에 대해서 수행하지 않고, 부분집합으로 분할(divide)하고, 각 부분집합에 대해서 정렬 작업을 완성(conquer)한 후에 정렬된 부분집합들을 다시 결합(combine)하는 분할 정복(Divide and Conquer)기법을 사용한다.  
- 2개의 정렬된 자료의 집합을 결합하여 하나의 집합으로 만드는 병합방법을 2-way병합이라한다.  
- n개의 정렬된 자료의 집합을 결합하여 하나의 집합으로 만드는 병합방법을 n-way병합이라고 한다.   

> 2-way 병합 정렬은 다음과 같은 작업을 반복수행한다.  
1. 분할단계 : 입력자료를 같은 크기의 부분집합 2개로 분할한다. 
2. 병합단계 :  2개의 부분집합을 정렬하면서 하나의 집합으로 병합한다. 
    - 정복(conquer) : 부분집합의 원소들을 정렬한다 부분집합의 크기가 층분히 작지 않으면 재귀호출을 이용하여 다시 분할 정복 기법을 적용한다.   
    - 결합(combine) : 정렬된 부분집합들을 하나의 집합으로 통합한다.

병합 정렬은 저장공간을 추가로 필요하기 때문에 정렬한 원소 n개에 대해서 2 x n개의 메모리 공간을 사용한다. n개의 원소를 분할하여 정렬하기 때문에, <u>**병합 정렬의 시간 복잡도는 O(nlog<sub><small>2</small></sub>n)**</u>이 된다. 시간복잡도 O(nlogn)이 걸린다. n개 만큼 logN번 돌리기 때문이다.

<details>
<summary>Merge Sort 알고리즘</summary>

```java
public static void mergeSort(int[] ary) { mergeSort(ary,  new int[ary.length], 0, ary.length - 1);}

private static void mergeSort(int[] ary, int[] tmp, int start, int end) {
    if(start >= end) return;
    int mid = (start + end) / 2;
    // divide
    mergeSort(ary, tmp, start, mid);
    mergeSort(ary, tmp, mid + 1, end);
    // merge
    merge(ary,tmp,start,mid,end);
}

private static void merge(int[] ary, int[] tmp, int start, int mid, int end) {
    // 임시저장소에 copy
    for (int i = 0; i < ary.length; i++) tmp[i] = ary[i];

    // 2개의 pointer가 동시에 움직임
    int one = start; // pointer
    int two = mid + 1; // pointer
    int index = start; // 원본 index

    //merge와 동시에 sort
    while (one <= mid && two <= end) { // 배열 2개중 한개가 끝에 도달하면 끝난다.
        if (tmp[one] <= tmp[two]) ary[index++] = tmp[one++];
        else ary[index++] = tmp[two++];
    }

    //앞의 배열이 남았을 경우
    for (int i = 0; i <= mid - one; i++) ary[index + i]  = tmp[one + i];

    // 뒤의 배열이 남았을 경우는 이미 ary 배열에 뒷쪽에 남아있음

}
```
</details>    
<br>