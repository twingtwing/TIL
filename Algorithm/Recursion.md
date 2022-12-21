# Recursion

---

### Fibonacci 수열

```java
class FibonacciNumber{
    public int f(int n, int[] r){
        if (n <= 0) return 0;
        else if (n==1) return r[n] = 1;
        else if (r[n] > 0) return r[n]; // 한번 호출한 데이터는 다시 하지 않음
                                        // 이 로직이 있으면 o(n)의 시간이 걸리지만, 없으면 o(2^n)의 시간이 걸림
        return r[n] = f(n-1, r) + f(n - 2, r);
    }
}
```
 
## Reference

- [자료구조 알고리즘 - 엔지니어 대한민국](https://www.youtube.com/user/damazzang)
- [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C/dashboard)