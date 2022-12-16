# Sort
    ✍️ 순서없이 배열되어 있는 자료들을 오름차순(ascending) 혹은 내림차순(descending)으로 재배열
## 1. 정렬 방법의 분류

## java에서의 sort은 무슨 sort??

### 1.1 실행 방법에 따른 분류 
정렬은 실행하는 방법에 따라 비교식 정렬(Comparative Sort)과 분산식 정렬(Distribute Sort)로 구분할 수 있다. 
- 비교식 정렬 : 비교하고자 하는 각 키 값들을 한 번에 두 개씩 비교하여 교환하는 방식으로 정렬을 실행한다.  
- 분산식 정렬 : 키 값을 기준으로 하여 자료를 여러 개의 부분집합으로 분해하고, 각 부분집합을 정렬함으로써 전체를 정렬하는 방식으로 실행한다. 

### 1.2 정렬 장소에 따른 분류   
컴퓨터에서 수행되는 정렬은 컴퓨터 메모리 내부에서 정렬하는 내부정렬(Internal Sort)과 메모리의 외부인 보조 기억 장치에서 정렬하는 외부정렬(External Sort)로 분류할 수 있다.
- 내부정렬 : 내부 정렬은 정렬할 자료를 메인 메모리에 올려서 정렬하는 방식으로 정렬 속도가 빠르지만, 정렬할 수 있는 자료의 양이 메인 메모리의 용량에 따라 제한된다.   
    (내부 정렬을 사용하는 정렬방식)
    1. 교환방식 : 키를 비교하고, 교환하여 정렬하는 방식 (선택 정렬, 버블 정렬, 퀵 정렬)
    2. 삽입방식 : 키를 비교하고, 삽입하여 정렬하는 방식 (삽입정렬, 셀 정렬)
    3. 병합방식 : 키를 비교하고, 병합하여 정렬하는 방식 (2-way 병합, n-way 병합)
    4. 분배방식 : 키를 구성하는 값을 여러 개의 부분집합에 분배하여 정렬하는 방식 (기수 정렬)
    5. 선택방식 : 이진 트리를 사용하여 정렬하는 방식 (힙 정렬, 트리 정렬)
- 외부 정렬 : 외부정렬은 대용량의 보조 기억 장치를 사용하기 때문에 내부 정렬보다 속도는 떨어지지만, 내부 정렬로 처리할 수 없는 대용량의 자료를 정렬 처리할 수 있다.  
    - 병합방식 : 파일을 부분 파일로 분리한 후 각각을 내부 정렬 방법으로 정렬하여 병합하는 정렬방식 (2-way 병합, n-way 병합)

## 2. Sort의 종류
    ❗정렬방법의 효율성을 비교하는 일반적인 기준은 원소에 대한 비교횟수와 이동횟수가 된다. 
### 2.1 Selection Sort
선택정렬은 전체 원소들 중에서 기준 위치에 맞는 원소를 선택하여 자리를 교환하는 방식으로 정렬한다. 전체 원소중에서 가장 작은 원소를 찾아서 선택하고  첫번째 원소와 자리를 교환한다. 그 다음 두 번째로 작은 원소를 찾아 선택하여 두번째 원소와 자리를 교환하고, 차례대로 교환하는 과정을 마지막까지 반복하면서 선택 정렬을 완성한다.

전체 비교 횟수는 n(n-1)/2이기 때문에 <u>**선택 정렬의 시간 복잡도는 O(n<sup><small>2</small></sup>)**</u>이 된다.

<details>
<summary>Selection Sort 알고리즘</summary>

```java
class SelectSort{
    public void sort(int ary []){
        for (int i = 0; i<ary.length-1; i++){
            int min = i;
            for (int j = i+1; j<ary.length; j++){
                if (ary[j] < ary[min]) min = j;
            }
            if(i != min)swap(ary,i, min);
        }
    }

    public void swap(int ary [], int i, int j){
        int temp = ary[i];
        ary[i] = ary[j];
        ary[j] = temp;
    }
}
```
</details>    
<br>

### 2.2 Bubble Sort
버블 정렬은 인접한 두개의 원소를 비교하여 자리를 교환하는 방식으로 정렬한다. 첫번째 원소부터 마지막 원소까지 반복하면, 가장 큰 원소가 마지막자리로 정렬하게 된다. 마지막을 제외한 나머지 원소 중에서 이러한 과정을 반복하고, 나머지 원소가 없어지면 버블정렬을 완성한다.  
첫번째 원소부터 인접한 원소끼리 계속 자리를 교환하면서, 맨 마지막 자리로 이동하는 모습이 물방울 모양과 같다고해서 버블 정렬이라고 한다.

전체 비교 횟수는 n(n-1)/2이기 때문에 <u>**버블 정렬의 시간 복잡도는 O(n<sup><small>2</small></sup>)**</u>이 된다.

<details>
<summary>Bubble Sort 알고리즘</summary>

```java
class BubbleSort{
    public void sort(int ary[]){
        for (int i = ary.length -1; i > 0; i--){
            for (int j = 0; j < i; j++){
                if (ary[j] > ary[j+1])swap(ary,j, j+1);
            }
        }
    }

    public void swap(int ary [], int i, int j){
        int temp = ary[i];
        ary[i] = ary[j];
        ary[j] = temp;
    }
}
```
</details>    
<br>

### 2.3 Quick Sort
퀵정렬은 정렬할 전체 원소에 대해서 정렬을 수행하지 않는다. 먼저 기준값을 중심으로 전체 원소들을 왼쪽 부분집합과 오른쪽 부분집합으로 분할(divide)한다. 왼쪽 부분집합에는 기준값인 피봇(pivot)보다 작은 원소들을 이동시키고, 오른쪽 집합에는 기준값보다 큰 원소들을 이동시킨다. 부분집합의 크기가 1 이하가 될때까지 분할 작업을 순환적으로 반복하면서 피봇의 왼쪽 부분집합과 오른쪽 부분집합을 정렬하는 방법을 반복하면서 전체 원소들을 정렬한다.   
퀵정렬은 버블정렬은 인접한 두개의 원소를 비교하여 자리를 교환하기 때문에 원소가 이동하는 거리가 1이되어 자기 자리를 찾기까지 비교횟수와 자리교환횟수가 많음점을 개선하여 자기자리에 최대한 가까이 이동시켜서 비교횟수와 자리교환횟수를 줄인 정렬 방법이다.

분할하면서 이동횟수가 반으로 줄어들기 때문에  <u>**퀵 정렬의 시간 복잡도는 O(nlog<sub><small>2</small></sub>n)**</u>이 된다.

알고리즘 불완정함 수정필요!! 경우에 따라서 에러 생김🔥
<details>
<summary>Quick Sort 알고리즘</summary>

```java
class QuickSort{
    int i = 0;
    public int partition(int ary[], int begin, int end){
        int pivot, left, right;
        left = begin;
        right = end;
        pivot = (begin+end)/2;
        while (left < right){
             while ((ary[left] <= ary[pivot]) && (left <= right)) left++;
             while ((ary[right] > ary[pivot]) && (left <= right)) right--;
             if (left < right) swap(ary,left,right);
             if (left == pivot) return right;
        }
        swap(ary,pivot,right);
        return right;
    }

    public void sort(int ary[]){
        sort(ary,0,ary.length-1);
    }

    public void sort(int ary[],int begin, int end){
        if (begin < end){
            int part;
            part = partition(ary,begin,end);
            sort(ary,begin,part-1);
            sort(ary,part+1,end);
        }
    }

    public void swap(int ary [], int i, int j){
        int temp = ary[i];
        ary[i] = ary[j];
        ary[j] = temp;
    }
}
```
</details>    
<br>

### 2.4 Insert Sort
삽입 정렬은 정렬되어 있는 부분 집합에 정렬할 새로운 원소의 위치를 찾아 삽입하는 방법이다. 정렬할 자료가 두 개의 부분집합 S(Sorted)와  U(Unsorted)로 나뉘어 있다고 생각한다. 앞부분 원소부터 정렬을 수행하면서, 정렬된 앞부분의 원소들은 부분 집합 S가 되고, 아직 정렬되지 않은 나머지 원소들은 부분 집합 U가 된다. 정렬되지 않은 부분집합 U의 원소를 하나씩 꺼내어 이미 정렬되어 있는 부분집합 S의 마지막 원소부터 차례대로 비교하면서 위치를 찾아 삽입하여 부분집합 S의 원소는 하나씩 늘리고 부분 집합 U의 원소는 하나씩 줄인다. U의 원소를 모두 삽입하여 공집합이 되면 삽입 정렬이 완성된다.  

전체 비교 횟수는 n(n-1)/4이기 때문에 <u>**삽입 정렬의 시간 복잡도는 O(n<sup><small>2</small></sup>)**</u>이 된다.

<details>
<summary>Insert Sort 알고리즘</summary>

```java
class InsertSort{
    public void sort(int ary[]){
        if (ary.length < 2) return;
        for (int i = 1; i < ary.length; i++){
            int now = ary[i]; // for구문을 돌면서 배열의 값이 변하기 때문에 먼저 값을 할당해둠
            for (int j = i -1; j >= 0; j--){
                if (ary[j] > now) swap(ary,j);
                // 배열의 위치는 한칸씩 앞으로 움직이고 있기 때문에 i의 index값은 필요 없어짐
            }
        }
    }

    public void swap(int ary [], int j){
        int temp = ary[j];
        ary[j] = ary[j+1];
        ary[j+1] = temp;
    }
}
```
</details>    
<br>

### 2.5 Shell Sort
셸 정렬은 일정한 간격(interval)으로 떨어져 있는 자료들끼리 부분 집합을 구성하고, 각 부분집합에 있는 원소들에 대해서 삽입 정렬을 수행하는 작업을 반복하면서 전체 원소들을 정렬하는 방법이다. 셸 정렬에서 부분 집합을 만드는 기준이 되는 간격을 매개변수 h에 저장한다. 한 단계가 수행될 때마다 h의 값을 감소시키고, 셸정렬을 순환호출하는데, 결국 h가 1이 될때까지 반복한다.  
전체 원소에 대해서 삽입 정렬을 수행하는것보다 부분 집합으로 나누어 정렬하면, 비교연산과 교환연산의 횟수를 줄일 수 있다. 셸정렬의 성능은 매개변수 h의 값에 따라 달라진다.

일반적으로 <u>**셸 정렬의 시간 복잡도는 O(n<sup><small>1.25</small></sup>)**</u>이 된다.

<details>
<summary>Shell Sort 알고리즘</summary>

```java
class ShellSort{
    public void intervalSort(int ary[], int begin, int end, int interval){
        int item,j;
        for (int i = begin + interval; i <= end; i=i+interval){
            item = ary[i];
            for (j = i-interval; j >= begin && item < ary[j]; j -= interval)
                ary[j+interval] = ary[j];
            ary[j+interval] = item;
        }
    }

    public void sort(int ary[]){
        int interval = ary.length/2;
        while (interval >= 1){
            for (int i =0; i < interval; i++)
                intervalSort(ary,i,ary.length-1,interval);
            interval /= 2;
        }
    }
}
```
</details>    
<br>

### 2.6 Merge Sort
병합정렬은 여러개의 정렬된 자료의 집합을 결합하여 한 개의 정렬된 집합으로 만드는 방법이다. 병합 정렬은 전체 원소들에 대해서 수행하지 않고, 부분집합으로 분할(divide)하고, 각 부분집합에 대해서 정렬 작업을 완성(conquer)한 후에 정렬된 부분집합들을 다시 결합(combine)하는 분할 정복(Divide and Conquer)기법을 사용한다.  
- 2개의 정렬된 자료의 집합을 결합하여 하나의 집합으로 만드는 병합방법을 2-way병합이라한다.  
- n개의 정렬된 자료의 집합을 결합하여 하나의 집합으로 만드는 병합방법을 n-way병합이라고 한다.   

> 2-way 병합 정렬은 다음과 같은 작업을 반복수행한다.  
1. 분할단계 : 입력자료를 같은 크기의 부분집합 2개로 분할한다. 
2. 병합단계 :  2개의 부분집합을 정렬하면서 하나의 집합으로 병합한다. 
    - 정복(conquer) : 부분집합의 원소들을 정렬한다 부분집합의 크기가 층분히 작지 않으면 재귀호출을 이용하여 다시 분할 정복 기법을 적용한다.   
    - 결합(combine) : 정렬된 부분집합들을 하나의 집합으로 통합한다.

병합 정렬은 저장공간을 추가로 필요하기 때문에 정렬한 원소 n개에 대해서 2 x n개의 메모리 공간을 사용한다. n개의 원소를 분할하여 정렬하기 때문에, <u>**병합 정렬의 시간 복잡도는 O(nlog<sub><small>2</small></sub>n)**</u>이 된다.

<details>
<summary>Merge Sort 알고리즘</summary>

```java
class MergeSort{
    private int sorted[] = new int[30];

    public void merge(int ary[], int m, int middle, int n){
        int size= ary.length;
        int i = m;
        int j = middle + 1;
        int k = m;
        while (i<= middle && j <= n){
            if (ary[i] <= ary[j]) sorted[k] = ary[i++];
            else sorted[k] = ary[j++];
            k++;
        }
        if (i>middle){
            for (int t =j; t <= n; t++,k++)
                sorted[k] = ary[t];
        }else{
            for (int t = i; t <= middle; t++, k++)
                sorted[k] = ary[t];
        }

        for (int t = m; t <= n; t++)
            ary[t] = sorted[t];
    }

    public void sort(int a[], int m, int n){
        int middle;
        if(m<n){
            middle = (m+n)/2; // 분할
            sort(a,m,middle); // 정복?
            sort(a,middle+1,n); // 정복
            merge(a,m,middle,n); //결합
        }
    }
```
</details>    
<br>

    ✨Sort의 시간복잡도

| Sort | 시간복잡도 | 
|---|:---:|
| `Selection Sort` | O(n<sup><small>2</small></sup>) | 
| `Bubble Sort` | O(n<sup><small>2</small></sup>) |  
| `Quick Sort` | O(nlog<sub><small>2</small></sub>n)|  
| `Insert Sort` | O(n<sup><small>2</small></sup>) | 
| `Shell Sort` | O(n<sup><small>1.25</small></sup>) | 
| `Merge Sort` | O(nlog<sub><small>2</small></sub>n) |  

<br>

---

## Reference

- 자바로 배우는 자료구조 방식