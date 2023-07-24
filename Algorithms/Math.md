# 🧵 Math

## 🪡 누적합

> 수열의 항들을 차례로 더한 값들을 순서대로 구하는 연산

#### 구현

```java
public class Main{
    public static void main(String [] args){

        int [] seq = {1, 2, 3, 4, 5};
        int [] sum = new int[seq.length];

        sum[0] = seq[0];
        for(int i = 1; i < seq.length; i++)
            sum[i] = seq[i] + sum[i - 1];

        System.out.println(sum[seq.length - 1]);
        
    }
}
```

## 🪡 에라토스테네스의 체

> 에라토스테네스의 체는 소수의 배수를 구해서 체로 걸러내는 방법

#### 구현
1. 2부터 시작하여 차례로 소수를 찾는다. (1은 소수가 아니다.)
2. 소수의 배수를 찾아서 모든 수에서 제외 시킨다.
    - 내부 for 구문에서 소수 i의 제곱을 시작값을 해서 중복계산을 피한다.
    - 소수 i의 배수들을 제외할 때, i의 제곱보다 작은 배수들은 이전 단계에서 이미 다른 소수의 배수로서 처리되기 때문이다.
3. √n 까지의 배수를 찾아서 모두 제외시키고, 탐색을 종료한다.
    - √n 이상의 수는 내부 for 구문을 돌 필요가 없으므로, √n까지의 배수만 찾아서 제외한다.

<br>

![위키 백과 사전](https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif)

```java
public class Main{
    public static void main(String [] args){
        int n = 10;
        boolean [] isNotPrime = new boolean[n + 1];

        for(int i = 2; i * i <= n; i++){
            if(isNotPrime[i]) continue;
            for(int j = i * i; j <= n; j += i) 
                isNotPrime[j] = true;;
        }

    }
}
```

<br>

## 🪡 유클리드 호제법
> 두 정수의 최대공약수(GCD, Greatest Common Divisor)를 구하는 알고리즘
- 최소 공배수 = a ⨉ b / 최대 공약수

#### 구현
1. A와 B의 최대 공약수는 A를 B로 나눈 나머지 R의 최대 공약수와 같다.
2. 1번의 원리를 재귀적으로 반복하여 나머지가 0이 될 때까지 나눈다.
3. 나머지가 0이 되면 나누었던 수가 최대공약수이므로 탐색을 종료한다.

```java
public class Main{
    public static void main(String [] args){
        int a = 24;
        int b = 32;

        System.out.println(findGCD(b, a));
    }

    private static int findGCD(int max, int min){
        if(max % min == 0)
            return min;
        return gcd(min, max % min);
    }

}
```

## Reference

#### 위키피디아
- [위키피디아1](https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4)
- [위키피디아2](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95)