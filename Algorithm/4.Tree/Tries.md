# Tries
    문자열에서 검색을 빠르게 하기위해 고안된 자료구조
## 1. Tries의 구현
루트 값이 비고, 자식들부터 문자열이 아닌 단어 한글자만 가지고있다. 그리고 차례로 내려오면서 지나간 단어를 연결하면, ex copy라는 문자열이 완성된다. 그리고 y라는 node에는 copy라는 문자열의data가 담겨져 있다. 그냥 문자열을 노드에 저장하면 문자열 길이 M의 시간 까지 합해서 시간이 M(log n)이 걸리지만, tries처럼 하면 o(M)의 시간밖에 걸리지 않는다

---

## Reference

- 자바로 배우는 자료구조 방식
- 강의....