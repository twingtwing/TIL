# 🧷 ROWNUM and OFFSET-FETCH

## 🖇️ ROWNUM
Oracle의 ROWNUM은 Pseudo Column으로서 SQL 처리 결과 집합의 각 행에 대해 임시로 부여되는 일련번호다. 

> Pseudo Column
> 테이블의 컬럼처럼 동작하지만, 실제로 테이블에 저장되지는 않는 컬럼을 말한다. SEARCH는 가능하지만, INSERT, UPDATE, DELETE 는 불가능하다.

1 건의 행만 가져오고 싶을 때는 ROWNUM = 1은 가능하지만, ROWNUM = N은 불가능하다. 또한, 2건 이상의 N 행을 가져오고 싶을 때는 ROWNUM < N으로 지정할 수 있다.  

최상위 혹은 최하위 N개의 ROW을 가져오고 싶을 때, ORDER BY 절을 같이 사용한다. 단, ORDER BY 절 처리 후에 WHERE 절을 처리해야 한다.

```SQL
SELECT *
FROM (
    SELECT *
    FROM EMP
    ORDER BY SAL DESC
    )
WHERE ROWNUM < 4;
```
위의 쿼리 처럼 INLINE VIEW를 사용해 정렬 후 ROWNUM을 처리함으로써 순위와 ROW 순서를 일치시켜 Top N 쿼리의 결과를 만들 수 있다.

## 🖇️ OFFSET FETCH 페이징 처리

```SQL
ORDER BY column
[OFFSET offset {ROW | ROWS}]
[FETCH {FIRST | NEXT} [{rowcount | percent PERCENT}] {ROW | ROWS} {ONLY | WITH TIES}]
```
- OFFSET offset : 건너뛸 행의 개수를 지정한다.
- FETCH : 반환할 행의 개수나 백분율을 지정한다.
- FIRST | NEXT : 행을 검색하는 방법을 지정한다.
  - FIRST : 결과 집합에서 첫 번째 행부터 지정된 개수의 행을 반환한다.
  - NEXT : 현재 위치에서 지정된 개수의 행을 반환한다.
- ONLY : 지정된 행의 개수나 백분율만큼 행을 반환한다.
- WITH TIES : 마지막 행에 대한 동 순위를 포함해서 반환한다.

#### 예제 # 1 행 건너뛰기

```SQL
SELECT ENAME, SAL
FROM EMP
ORDER BY SAL DESC
OFFSET 3 ROWS;
```

#### 예제 # 2 행 제한

```SQL
SELECT ENAME, SAL
FROM EMP
ORDER BY SAL DESC
FETCH FIRST 3 ROWS ONLY;
```

#### 예제 # 3 페이징 처리

```SQL
SELECT ENAME, SAL
FROM EMP
ORDER BY SAL DESC
OFFSET 0 ROWS
FETCH NEXT 10 ROWS ONLY;
```

## Reference
- [SQL 전문가 가이드](https://www.yes24.com/Product/Goods/90613346)
- [참고 사이트 1](https://www.tutorialspoint.com/offset-fetch-in-ms-sql-server)