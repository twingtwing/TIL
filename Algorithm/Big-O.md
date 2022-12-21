# Big-O 표기법

    시간 복잡도 추측

+) Big-O 표기법  
- 알고리즘의 성능을 수학적으로 표현한 표기법  
- 시간복잡도와 공간복잡도를 알 수 있음
- 알고리즘 실제 러닝 타임을 표시하는게 아니라, 데이터와 사용자의 증가율에 따른 알고리즘의 성능 예측하는 것이 목표  
(1) O(1) constant time(일정한 시간)  
: 입력 데이터 크기와 상관없이 언제나 일정한 시간이 걸리는 알고리즘을 말함
(2) O(n)  
: 입력 데이터 크기에 비례해서 처리시간이 걸리는 알고리즘을 말함  ex, for구문
(3) O(n^2) quadratic time  
: 입력 데이터 크기에 제곱비례해서 처리시간이 걸리는 알고리즘을 말함  ex, 이중 for구문  
(4) O(nm) 
: 입력 데이터 크기에 비례해서 처리시간이 걸리는 알고리즘을 말함  ex, 길이가 다른? 이중 for구문  
m변수 값에 따라  O(n^2)와 확연하게 차이가 있기때문에 구분해주어야함
(5) O(n^3) polynomial / cubic time  
: 입력 데이터 크기에 세제곱비례해서 처리시간이 걸리는 알고리즘을 말함 ex, 삼중 for구문  
(6) O(2^n) exponential time 
: Fibonacci(피보나치) 수열(재귀함수를 통해 구현)만큼 증가? 세제곱보다 더 급격하게 증가함  
그 밖에 m개씩 n번 늘어나는 알고리즘은 O(m^n)으로 표현  
(7) O(log n)  
: 한번 처리가 될때마다 검색해야할 데이터가 반으로 줄어드는 알고리즘 ex, binary search(이진 검색)  
O(n)보다 적게 걸린다. 또한 데이터가 증가해도 성능이 차이가 나지 않음  
(8) O(sqrt(n))  
: Square root ? 제곱근  
정사각형 이차원 배열에서 하나의 행만 검색하는 것과 마찬가지  
- Drop constants : 빅오 표기법에서 상수를 과감하게 버림 즉, O(2n) => for구문을 따로 두개 돌리는 알고리즘 이면,  
상수 2는 과감하게 버리고 O(n)이 된다. 왜냐하면 러닝타입을 표시하는게 아니라 증가율에 다른 성능 예측을 하는것이 목표이기 때문에 상수는 과감하게 무시함

```java
// 시간복잡도 : O(a/b) <= b부터 a까지 b만큰씩 증가하면서 돎. 즉 a를 b로 나눈 몫만큼 순회함
public int bigOQuestion1(int a, int b){
    int count = 0;
    int sum = b;
    while(sum <= a){
        sum += b;
        count++;
    }
    return count;
}

// 시간복잡도 : O(sqrt(n))
public int bigOQuestion2(int n){
    for (int i = 1; i * i <= n; i++){
        if (i*i == n) return i;
    }
    return -1;
}

// 만약 이진검색트리가 밸런스가 맞지 않을경우의 시간복잡도 => O(n) 한쪽으로만 치우치면 이진검색트리의 특징을 사용하지 못하므로 전부 순회해야함

// 이진검색트리가 아닌 이진트리에서 특정한 값을 찾아야하는 경우의 시간 복잡도 => O(n) 모든 노드를 전부 순회해야함

// 시간복잡도 : O(n^2)
public int[] bigOQuestion3(int[] ary, int val){
    int[] bigger = new int[ary.length + 1]; //사이즈 1 증가
    for (int i =0; i <ary.length; i++){
        bigger[i] = ary[i];
    }
    bigger[bigger.length-1] = val;
    return bigger;
}

public int[] bigOQuestion3Copy(int[] ary){
    int[] copy = new int[0];
    for (int value : ary){
        copy = bigOQuestion3(copy,value);
    }
    return copy;
}

// 시간복잡도 : O(logn) <= 돌때마다 데이터가 1/10 감소하기 때문
public int bigOQuestion4(int n){
    int sum = 0;
    while (n > 0){
        sum += n%10;
        n /= 10;
    }
    return sum;
}
```
