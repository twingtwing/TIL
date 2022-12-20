# BitOperation 

 * Integer : 4bytes = 32 bits =  2^32개(-2^32 ~ (2 ^31 -1))
 => 음의 정수는 맨 앞자리를 1로 표현하기 때문에 -2^32까지 표현 가능하지만, 양의 정수는 맨 앞자리가 0으로 표현되기에 전원 0인 0의값을 제외하면 2 ^31 -1 개를 표현하는 것이다.
 => + - * / 이진법 연산?
 => |(OR)연산자 : 둘중 하나라도 1이면 1이다.
         => 전원 0인값과 연산하면 자기자신이 나오고, 전원 1인값과 하면 전원 1이 나온다. 자기자신과 하면 자기자신이 출력된다.
    &(AND)연산자 : 둘 보두 1이어야지 1이다.
         => 전원 0인값과 연산하면 전원 0이 값이 나오고, 전원 1인값과 연산하면 자기자신이 나온다. 자기 자신과하면 마찬가지로 자기자신이 나온다.
    ~ : 둘이 반대가 됨
    ^(XOR)연산자 : 두개가 서로 다른값을 가지고 있으면 1로 셋팅됨
         => 특징 전원 0인 값을 ^하면 원래 값이 나오고, 전원 1인값과 연산하면, 원래값의 ~반대 값이 출력된다. 또한, 자기자신과 하면 전원 0이 출력된다.
    <</>>(SHIFT)연산자 : 해당방향으로 1을 각각 N만큼 이동한다. >>이동할때 더이상자리가 없으면 그 값은 사라진다.
         => 사인비트를 고려하는냐 안하는냐로 달라짐
             - 고려 할 경우 : 부호와 상관없이 SHIFT를 logical right shift >>>라고 한다. 계속 반복하면 모든 비트가 0이 된다.
             - 하지 않을 경우 : 부호를 고려해서 하는 shift를 arithmetic right shift >> 라고 한다. shift하는 값이 음수이면 움직이면서 생기는 맨 앞자리 값을 1로 셋팅한다.
                              계속 반복하면 모든 bit가 1로 셋팅된다.
                              즉, <<, >>는 부호만은 꼭 고려한다.

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