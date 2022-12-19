# BitOperation 

## 비트 연산

## 응용?
<details>
<summary>응용1</summary>

```java
// 응용 3. 소문자로만 이루어진 경우 ...? 아직도 모르겠음
// 아스키 코드의 특징와 비트연산자의 특징을 알고 있어야한다.
// 숫자(0~9) : 48 ~ 57 대문자 : 65 ~ 90 소문자 : 97 ~ 122
private static boolean isUnique3(String str) {
    int checker = 0;
    for (int i = 0; i < str.length(); i++) {
        int val = str.charAt(i) - 'a'; // a를 빼서 0 ~ 25로 변경함 => 이진법으로 11001까지 표현가능
        // i를 val만큼 이동하고, 둘다 모두 1 이면 1을 반환한다.
        // 즉, 해당값이 check에 있는지 확인가능
        if ((checker & (i << val)) > 0) return false;
        // i를 val만큼 이동하고, 둘중 하나가 1 이면 1을 반환한다.
        // 즉, 쉬프트한 값을 check에 저장한다.
        checker |= (1 << val);
    }
    return true;
}
```
</details>    
<br>


<details>
<summary>응용2</summary>

```java
// Bit Operation : 정수를 이진수 배열방으로 생각하고(짝수는 0,홀수는 1) 마지막에 1이 몇개인지 확인
//                 짝수개를 0으로 만들수잇는것은 &연산다를 통해 가능 여기서 홀수를 그대로 1로 만들려면 |연산자를 사용한다.
//                 만약에 겹치는것이 있을경우 짝수로 만들어야하므로, 기존의값과 새로운 값을 비교해야하므로 기존을 ~한 후에 &을 해야한다.
//                  마지막에 1이 몇개인지를 확인할려면 1을 -연산자를 하고, 다시 그 값으로 &연산을 해서 값이 0이 아니면 홀수개가 1이상이다.
private static boolean isPermutationOfPalindrorne3(String s){
    int bitVector = createBitVector(s);
    return bitVector ==0 || checkExactlyOneBitSet(bitVector); //모두 짝수개이거나 한개만 홀수개
}

private static int createBitVector(String s){
    int bitVector = 0;
    for (char c: s.toCharArray()){
        int x = getCharNumber(c);
        bitVector = toggle(bitVector, x);
    }
    return bitVector;
}

private static int toggle(int bitVector, int index){
    if (index < 0 ) return bitVector;
    int mask =  1 << index;
    if ((bitVector & mask) == 0){
        bitVector |= mask;
    }else {
        bitVector &= ~mask;
    }
    return bitVector;
}
```
</details>    
<br>

---

## Reference

- [자료구조 알고리즘 - 엔지니어 대한민국](https://www.youtube.com/user/damazzang)