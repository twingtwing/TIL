# 🧷 MSSQL Top N 쿼리

## 🖇️ TOP 절
TOP 절은 결과 집합으로 출력되는 ROW의 수를 제한할 수 있다.
```SQL
TOP (Expression) [PERCENT] [WITH TIES]
```
- Expression : 반환할 ROW 수를 지정하는 숫자식 이다.
- PERCENT : 결과 집합에서 처음 Expression%의 행만 반환됨을 나타낸다.
- WITH TIES : ORDER BY 절이 지정된 경우에만 사용할 수 있다. 마지막 ROW과 같은 값이 있는 경우 추가 행이 출력되도록 지정할 수 있다.

#### 예제 # 1
**[ 상수 사용 ]**
```SQL
SELECT TOP(2)
       NAME, SAL
FROM EMP
ORDER BY SAL DESC;
```
![TOP TEST 이미지 1](https://drive.google.com/uc?export=view&id=19v_mKuDn6jUBw2vnAwnL5iZQk-kWb_pP)

**[ 변수 사용 ]**
```SQL
DECLARE @CNT AS INT = 2;

SELECT TOP (@CNT)
       NAME, SAL
FROM EMP
ORDER BY SAL DESC;
```
![TOP TEST 이미지 2](https://drive.google.com/uc?export=view&id=19v_mKuDn6jUBw2vnAwnL5iZQk-kWb_pP)

**[ 백분율 지정 ]**
```SQL
SELECT TOP(50) PERCENT
       NAME, SAL
FROM EMP
ORDER BY SAL DESC;
```
![TOP TEST 이미지 3](https://drive.google.com/uc?export=view&id=19v_mKuDn6jUBw2vnAwnL5iZQk-kWb_pP)

#### 예제 # 2 동률 값 포함
```SQL
SELECT TOP(2) WITH TIES 
       NAME, SAL
FROM EMP
ORDER BY SAL DESC;
```
![TOP TEST 이미지 4](https://drive.google.com/uc?export=view&id=1-Jb-b_Mz67V2MM21QMi0MeYYdh7ccNzX)


### 그 외의 DDL에서의 활용

#### DELETE
```SQL
DELETE TOP(1)
FROM EMP
WHERE SAL < 1000;
```

#### UPDATE
```SQL
UPDATE TOP(50) PERCENT EMP
SET SAL = SAL + 1000
WHERE SAL < 1000;
```

TOP 사용 시 행의 삽입 순서를 기반으로 TOP N 행이 삭제 혹은 수정 처리 된다. ORDER BY 같이 사용하면 에러처리 되므로 MERGE문이나 WHERE절을 이용해야 한다.

#### INSERT
**[OPTION 1]**
```SQL
INSERT INTO DEPT
SELECT TOP(2) 
       empId, name
FROM EMP
ORDER BY empId DESC;
```
INSERT 문은 ORDER BY 처리가 가능하기 때문에 정렬 기반의 TOP N 행을 INSERT 처리가 가능하다.

**[OPTION 2]**
```SQL
INSERT TOP(2) INTO DEPT
SELECT empId, name
FROM EMP
ORDER BY empId DESC;
```
TOP 위치에 따라 INSERT 되는 행이 달라진다. 위의 쿼리는 ORDER BY를 무시하고 행의 삽입 순서를 기반으로 삽입한다.  
ORDER BY 절은 SELECT 절의 결과를 정렬하는 데 사용되지만, 삽입되는 행의 순서에는 영향을 미치지 않기 때문이다. TOP을 사용하여도 정렬 기반 TOP N 행 INSERT 처리가 불가능하다.

## 🖇️ OFFSET FETCH 페이징 처리

```SQL
ORDER BY column [ASC | DESC]
OFFSET offset {ROW | ROWS}
FETCH {FIRST | NEXT} rowcount {ROW | ROWS} ONLY
```
- OFFSET offset : 건너뛸 행의 개수를 지정한다.
- FETCH : 지정된 행의 개수를 지정한다.
- FIRST | NEXT : 행을 검색하는 방법을 지정한다.
  - FIRST : 결과 집합에서 첫 번째 행부터 지정된 개수의 행을 반환한다.
  - NEXT : 현재 위치에서 지정된 개수의 행을 반환한다.
- ONLY : 지정된 행의 개수만큼 행을 반환한다.

#### 예제 # 1 행 건너뛰기

```SQL
SELECT NAME, SAL
FROM EMP
ORDER BY SAL DESC
OFFSET 3 ROWS;
```

#### 예제 # 2 페이징 처리

```SQL
SELECT NAME, SAL
FROM EMP
ORDER BY SAL DESC
OFFSET 0 ROWS
FETCH NEXT 10 ROWS ONLY
```

## Reference

- [참고 사이트 1](https://learn.microsoft.com/ko-kr/sql/t-sql/queries/top-transact-sql?view=sql-server-ver16)
- [참고 사이트 2](https://blog.sqlauthority.com/2010/02/27/sql-server-insert-top-n-into-table-using-top-with-insert/)
- [참고 사이트 3](https://www.tutorialspoint.com/offset-fetch-in-ms-sql-server)