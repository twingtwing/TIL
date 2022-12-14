# Hash

## Hash 란?

## Hashing

해싱은 키값을 비교하여 찾는 검색 방법이 아니라, 산술적인 연산을 이용하여 키가 있는 위치를 계산하여 바로 찾아가는 계산 검색 방식이다. 키 값을 원소의 위치로 변환하는 함수를 해싱(Hashing)함수라고 한다.

- 해싱 검색 방법  
해싱 검색은 키 값에 대해서 해싱 함수를 계산하여 주소를 구하고, 구한 주소에 해당하는 해시테이블에 찾는 항목이 있으면, 검색이 성공이 되고, 없으면 검색 실패가 된다.   
해시 테이블은 n개의 버킷과 m개의 슬롯으로 구성한다. 해싱함수에 의해서 계산된 주소는 버킷 주소가 된다. 이때 사용하는 해싱함수는 0 ~ n-1 사이의 버킷주소을 만들어야 한다. 해싱함수에 의해서 알아낸 버킷에 키값이 저장된 슬롯이 여러개 있는 경우에는 순차 검색을 하여 해당 슬롯을 검색한다.

색인 순차 테이블의 성능은 인덱스 테이블의 크기에 따라 달라진다. 인덱스 테이블의 크기가 줄어들면 배열의 인덱스를 저장하는 간격이 커지므로 범위도 커진다. 테이블의 크기를 늘리면, 배열의 인덱스를 저장하는 간격이 작아지므로 배열에서 검색해야하는 범위는 작아지지만, 인덱스 테이블을 검색하는 시간이 늘어나게 된다.

## HashTable
해싱함수에 의해 계산된 주소의 위치에 항목을 저장한 표를 해시 테이블(Hash Table)이라고 한다.  
Hash table(hash map)이란 해시함수를 사용해서 변환한 값을 index로 삼아 key와 value를 저장하는 자료구조

해시함수로 변환한 index를 key 값으로 저장한다.

### 충돌을 방지하기 위해 배열 대신 linkedlist에 저장,,,?
배열방 안에 linkedlist를 선언하여 linkedlist에 먼저 저장한다.

<details>
<summary>HashTable 알고리즘</summary>

```java
class HashTable{
    // 충돌을 방지하기 위해, 배열방에 바로 저장하지 않는다.
    // 배열방 안에 LinkedList을 선언하여 LinkedList에 먼저 저장한다.
    LinkedList<Node> [] data;

    class Node{
        String key;
        String value;

        public Node(String key, String value) {
            this.key = key;
            this.value = value;
        }

        public String getValue() {
            return this.value;
        }

        public void setValue(String value) {
            this.value = value;
        }
    }

    HashTable(int sizs) {
        this.data = new LinkedList[sizs];
    }

    // index를 hashcode로 변환
    int getHashCode(String key) {
        int hashCode = 0;
        for (char c : key.toCharArray()) { // 아스키 값을 가지고 옴
            hashCode += c;
        }
        return hashCode;
    }

    // Hashcode를 index로 변환
    int covertToIndex(int hashCode) {
        return hashCode % this.data.length;
    }

    Node searchKey(LinkedList<Node> list, String key) {
        if (list == null) return null;
        for (Node node : list) {
            if (node.key.equals(key)) return node;
        }
        return null;
    }

    void put(String key, String value) {
        int hashCode = getHashCode(key);
        int index = covertToIndex(hashCode);
        LinkedList<Node> list = this.data[index];
        if (list == null) {
            list = new LinkedList<>();
            data[index] = list;
        }
        Node node = searchKey(list, key); // 이미 존재하는지 확인
        if (node == null) list.addLast(new Node(key,value));
        else node.setValue(value);
    }

    String get(String key) {
        int hashcode = getHashCode(key);
        int index = covertToIndex(hashcode);
        LinkedList<Node> list = this.data[index];
        Node node = searchKey(list, key);
        return node == null ? "Not Found" : node.value;
    }
}
```
</details>    
<br>