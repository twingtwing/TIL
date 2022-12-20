# Dynamic Programming

## 문제

### 1. 최소 비용으로 계단오르기
계단에서 i번째 계단을 올라갈려면 양수값을 가진 cost[i]가 지불되어야함(계단 배열마다 지불하는 비용이 다름)
또한, 계단 오르기는 한칸 혹은 두칸만 가능하고, 계단 시작점을 0 혹은 1로 선택할 수 있다.
=> 뒤에서 시작해서 경우의 수를 구한다.

<details>
<summary>뮨재퓰이</summary>

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

    private void strCapacity(int len) {
        if (len == 0) return;
        this.size = this.size + len; // ArrayList와 달리 문자의 길이 만큼 확장한다.
        char[] newVal = new char[this.size];
        for (int i = 0; i < this.value.length; i++) newVal[i] = this.value[i];
        this.value = newVal;
    }

}
```
</details>        
<br>