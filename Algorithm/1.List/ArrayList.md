# ArrayList

Java에서 Array로 객체를 생성하게 되면, 배열의 크기가 고정되는 문제점이 발생한다. 이를 보완하기 위해 Doubling 작업을 수행하는 ArrayList를 사용한다.  

    고정된 크기에서 검색을 수행하기 때문에 검색 시간은 O(1)의 시간이 걸린다.

**Doubilng 작업**  
고정된 크기를 가진 배열이 모두 차게되면, 배열을 2배로 늘리는 작업이다. 

    Doubilng 작업을 수행하는 시간은 O(n)의 시간이 소요된다.  

전의 더블링은 $n\over2$ , 전전의 더블링은 $n\over4$ . . . $n\over n+1$ 걸린다. 이 모든 시간의 더해도 n 이상의 시간이 걸리지 않기 때문에 Doubling 작업의 O(n) 시간이 걸린다.

<details>
<summary>ArrayList 알고리즘</summary>

```java
class ArrayList {
    private int size;
    private int index;
    private Object[] ary;

    public ArrayList() {
        this.size = 1;
        this.index = 0;
        this.ary = new Object[this.size];
    }

    public void add(Object obj) {
        if (isFull()) doubling();
        ary[this.index++] = obj;
    }

    private boolean isFull() {
        return this.index == this.size - 1;
    }

    private void doubling() {
        System.out.println(this.size + "=>" + this.size * 2);
        this.size = this.size * 2;
        Object[] douAry = new Object[this.size];
        for (int i = 0; i < this.ary.length; i++) douAry[i] = this.ary[i];
        this.ary = douAry;
    }

    public void remove(int index) { // 순차적인 자료구조이기 때문에 배열을 앞당겨야한다.
        if (index > this.size -1 || index < 0) throw new IndexOutOfBoundsException();
        for (int i = index; i < this.size - 1; i++) {
            this.ary[index] = this.ary[index + 1];
        }
        this.index--;
    }

    public Object get(int index) {
        if (index > this.size -1 || index < 0) throw new IndexOutOfBoundsException();
        return this.ary[index];
    }
}
```
</details>    
<br>

## Array vs ArrayList

---