# 순차자료 구조 방식 : 선형 리스트(Linear List) 혹은 순차 리스트(Ordered List)

    ✍️ 리스트에서 나열한 원소들간에 논리적인 순서와 메모리에 저장하는 물리적인 순서가 같은 구조

## 1. 장점
> 고정된 크기에서 검색을 수행하기 때문에 검색 시간은 O(1)의 시간이 걸린다.
- 원소의 논리적인 순서와 물리적인 순서가 같기 때문에, 특정 원소의 위치를 쉽게 알 수 있다.
- 원소들의 순서를 따로 표시할 필요가 없이 간단히 구성할 수 있다.
- index를 사용하여 특정 원소를 쉽게 접근 할 수 있기 때문에 접근 속도가 매우 빠르다.

## 2. 단점
- 순차자료구조는 논리/물리적인 순서가 같은 순서대로 연속적으로 저장되기 때문에 중간에 빈
- 순차 자료구조 방식은 배열을 이용하여 구현하기 때문에, 배열이 갖고 있는 메모리 사용의 비효율성 문제를 그대로 갖고 있다. 
- 원소 삽입/삭제가 발생한 원소 이후의 원소들은 한자리씩 앞/뒤로 이동해야한다. 이러한 추가적인 원소이동작업은 추가적인 오버헤드를 많이 발생하여 성능상의 문제를 일으킬 수 있다.

![array delete](..\Image\array_delete.png)

<small>출처 : <cite>https://codeforwin.org/c-programming/c-program-to-delete-element-from-array</cite> </small>  


## 3. ArrayList
Array은 크기를 변경할 수 없고, 메모리를 사용할 수 없는 문제를 가지고 있다. 이를 완하기 위해 Doubling 작업을 수행하는 ArrayList를 사용한다. 

### 3.1 Doubling 작업 : 배열의 길이를 늘리는 작업

    Doubilng 작업을 수행하는 시간은 O(n)의 시간이 소요된다.  

 직전의 더블링 수행 시간은 $n\over2$ , 전전의 더블링은 $n\over4$ . . . $n\over n+1$ 걸린다. 모두 n 이상의 시간이 걸리지 않기 때문에 Doubling 작업의 O(n) 시간이 걸린다.

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

    // Doubling 작업
    private void doubling() {
        System.out.println(this.size + "=>" + this.size * 2);
        this.size = this.size * 2;
        Object[] douAry = new Object[this.size];
        for (int i = 0; i < this.ary.length; i++) douAry[i] = this.ary[i];
        this.ary = douAry;
    }

    public void remove(int index) { 
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

### 3.2 Array vs ArrayList

||Array|ArrayList|
|--|------|-------------|
|메모리공간|정적|동적|
|데이터구조|고정 길이 데이터 구조|가변 길이 데이터 구조|
|성능||Doubling작업으로 Array보다 저하|
|시간복잡도(끝에 추가)|O(1)|O(1) or O(n)|
|시간복잡도(검색)|O(1)|O(1)|
|차원|다차원|1차원|

<br>

    ✨ Array, ArrayList 모두 물리적/논리적 순서가 같기 때문에, 삽입/삭제 연산 시에 이동작업이 필요하는 비효울성을 가지고 있다.

<br>

---

## Reference

- [자바로 배우는 자료구조 방식 - 이지영지음](http://www.yes24.com/Product/Goods/9345752)
- [자료구조 알고리즘 - 엔지니어 대한민국](https://www.youtube.com/user/damazzang)