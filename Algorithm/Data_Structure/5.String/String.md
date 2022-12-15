# String

## StringBuilder

String에 문자를 붙이는 과정은 문자를 모두 스캔한 후에 마지막에 붙인다. 즉, 문자배열을 순회할때 l을 문자의 길이라고 한다면, l + 2l + 3l .. nl 이므로 O(ln^2)의  시간이 걸린다.  

매우 비효울적이기 때문에, Java에서는 StringBuilder라는 클래스를 제공해준다. StringBuilder은 클래스안에 미리 배열공간을 만들어 놓고, append라는 추가 함수를 호촐하면 문자를 순회하지않고, 바로 추가하게 된다.  

공간은 배열이기 때문에 공간이 부족하면, ArrayList와 같이 공간을 늘리는 작업이 필요하다. 이러한 작업을 통해 시간복잡도와 공간복잡도을 매우 현저히 감소할 수 있다.  

StirnBuilder은 동기화를 지원하지 않지만 StringBuffer는 동기화를 지원함...? 그렇기 때문에 속도가 느릴수 있지만, 멀티 Thread환경에서는 동기화를 보장해야하기에 사용함

<details>
<summary>StringBuilder 알고리즘</summary>

```java

```
</details>        
<br>