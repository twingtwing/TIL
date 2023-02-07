# String

## 1. String : 문자열 객체
String은 Array와 마찬가지로 한번 생성되면 할당된 메모리 공간이 고정적이다. 길이가 고정적이기 때문에, + 연산자 혹은 concat메서드를 통해 원래 문자열에 새로운 문자열을 합치지 못한다. 문자열을 모두 스캔한 후에 마지막에서 새로운 문자열을 합친 후, 새로운 String 객체에 연결된 문자열을 저장하고 그 객체를 참조한다.  

기존의 문자열 길이 L, 더할려는 문자열 길이 N이라고 하면, 시간복잡도는 O(L + N)의 시간이 걸린다.  

그렇기 때문에, String 객체는 문자열 연산이 많은 경우에는 성능이 좋지 않다.

## 2. StringBuilder
StringBuilder는 클래스 안에 미리 배열 공간을 만들어 놓기때문에, 문자를 순회하지 않고 바로 추가 가능하다. 공간이 부족하게 되면, ArrayList처럼 Doubling 작업을 통해 메모리 공간을 늘릴 수 있다.

이러한 작업을 통해 시간복잡도와 공간복잡도을 매우 현저히 감소할 수 있다.  

<details>
<summary>StringBuilder 알고리즘</summary>

```java
class StringBuilder{
    private int size;
    private int index;
    private char[] value;

    StringBuilder(){
        this.size = 1;
        this.index = 0;
        this.value = new char[this.size];
    }

    public void append(String str) {
        if (str == null) return;
        strCapacity(str.length());
        for (int i = 0; i < str.length(); i++) value[index++] = str.toCharArray()[i];
    }

    // Doubling 작업
    private void strCapacity(int len) {
        if (len == 0) return;
        this.size = this.size + len; 
        char[] newVal = new char[this.size];
        for (int i = 0; i < this.value.length; i++) newVal[i] = this.value[i];
        this.value = newVal;
    }

}
```
</details>        
<br>

## 3. String vs StringBuilder vs StringBuffer
||String|StringBuilder|StringBuffer|
|--|------|-------------|-------------|
|메모리공간|정적|동적|동적|
|시간복잡도|O(L + N)|O(N)|O(N)|
|동기화|Thread-safe|X|Thread-safe|

String은 고정된 메모리공간을 가지고 있기 때문에, 메모리 소모가 적다. 리터럴이 불변한 객체 이기 때문에, 동기화에 대해 신경쓰지 않아도 된다.

추가 연산이 잦을 경우에는 StringBuilder/StringBuffer을 사용하는 것이 좋다.  

StringBuilder와는 달리 StringBuffer는 동기화를 지원해주기 때문에 멀티쓰레드에서 사용하는 것이 좋다. 단일쓰레드에서는 불필요한 동기화가 오히려 성능을 저하시키기 때문에 StringBuilder를 사용하는 것이 좋다.

<br>

---

## Reference
- [[자바] String, StringBuilder, StringBuffer의 차이](https://12bme.tistory.com/42)
- [자료구조 알고리즘 - 엔지니어 대한민국](https://www.youtube.com/user/damazzang)