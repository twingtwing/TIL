# 🧷 LATERAL & APPLY JOIN 연산

FROM 절의 메인테이블의 값에 따라 JOIN 절의 서브쿼리 결과가 달라진다. 즉 이러한 종속성 때문에 서브 쿼리에서 외부 매개변수를 인식 할 수 없다. 

그러나 LATERAL, CROSS APPLY 및 OUTER APPLY를 사용하면, 서브쿼리의 결과 집합을 메인 쿼리와 관련시킬 수 있다. 이 기능을 통해 서브쿼리의 결과를 메인 쿼리의 각 행에 대해 계산하거나 필터링할 수 있다. 이는 서브쿼리가 메인쿼리의 각 행에 대해 실행되는 경우에 유용하다.

## 🖇️ LATERAL
LATERAL은 서브쿼리에서 메인쿼리의 컬럼을 참조하는데 사용한다. 서브쿼리 내에서 메인쿼리의 컨텍스트를 유지하고, 메인 쿼리의 열을 참조할 수 있다. 

```SQL
SELECT A.*, B.*
FROM 메인 테이블 A
[INNER | LEFT] JOIN LATERAL (
    SELECT S.*
    FROM 서브 테이블 S
    WHERE A.COLUMN = S.COLUMN ) B -- 서브 쿼리
ON A.COLUMN = B.COLUMN
```
왼쪽 상관 관계가 있기 때문에 RIGHT LATERAL 또는 FULL OUTER LATERAL 조인을 사용할 수 없다.

#### 예제
ORDERS 주문 테이블에서 가장 높은 금액을 차지하는 상품을 알고 싶은 경우 LATERAL을 사용하여 구할 수 있다.

```SQL
SELECT A.ORDER_ID, B.PRODUCT_NAME, B.PRICE
FROM ORDERS A
LEFT JOIN LATERAL(
    SELECT O.ORDER_ID, P.PRODUCT_NAME, O.QUANTITY * O.UNIT_PRICE AS PRICE
    FROM ORDER_ITEMS O
    INNER JOIN PRODUCTS P
    ON O.ITEM_ID = P.PRODUCT_ID
    WHERE A.ORDER_ID = O.ORDER_ID
    ORDER BY O.QUANTITY * O.UNIT_PRICE DESC
    FETCH FIRST 1 ROW ONLY ) B
ON A.ORDER_ID = B.ORDER_ID
ORDER BY ORDER_ID;
```

![LATERAL TEST 이미지](https://drive.google.com/thumbnail?id=1kjbRZrHf1XOZiCPLR9-i3Jc7JTrytJHu&sz=w1000)

## 🖇️ APPLY
APPLY 함수는 메인쿼리의 각 행에 대해 서브쿼리를 실행하고, 메인쿼리의 각 행과 서브쿼리의 결과 간에 관계를 설정할 수 있다.

```SQL
SELECT A.*, B.*
FROM 메인 테이블 A
{CROSS | OUTER} JOIN (
    SELECT S.*
    FROM 서브 테이블 S
    WHERE A.COLUMN = S.COLUMN ) B -- 서브 쿼리
```

### CROSS APPLY
CROSS APPLY 연산자는 메인쿼리의 각 행에 대해 서브쿼리를 실행하며, 서로 매칭되는 행만을 반환한다. 따라서, INNER JOIN과 유사한 동작을 한다.

#### 예제
EMPLOYEES 직원 테이블에서 가장 최근 판매한 날짜를 알고 싶은 경우 CROSS APPLY를 사용하여 구할 수 있다.

```SQL
SELECT A.EMPLOYEE_ID, C.ORDER_DATE
FROM EMPLOYEES A
CROSS APPLY (
    SELECT B.SALESMAN_ID, B.ORDER_DATE
    FROM ORDERS B
    WHERE A.EMPLOYEE_ID = B.SALESMAN_ID
    ORDER BY B.ORDER_DATE DESC
    FETCH FIRST 1 ROW ONLY
     ) C
ORDER BY A.EMPLOYEE_ID;
```

![CROSS APPLY 이미지](https://drive.google.com/thumbnail?id=1uhOl0Ahrn_Rc3M3taG3uSM7LWAz3JCB5&sz=w1000)

### OUTER APPLY
OUTER APPLY 연산자는 메인쿼리의 각 행에 대해 서브쿼리를 실행하며, 서로 매칭되지 않는 행이 있더라도 모든 메인 쿼리의 행을 반환한다. 따라서, LEFT JOIN과 유사한 동작을 한다.

#### 예제
EMPLOYEES 직원 테이블에서 가작 최근 판매한 날짜를 알고 싶지만, 판매하지 않은 직원 또한 알고 싶은 경우 OUTER APPLY를 사용하여 구할 수 있다.

```SQL
SELECT A.EMPLOYEE_ID, C.ORDER_DATE
FROM EMPLOYEES A
OUTER APPLY (
    SELECT B.SALESMAN_ID, B.ORDER_DATE
    FROM ORDERS B
    WHERE A.EMPLOYEE_ID = B.SALESMAN_ID
    ORDER BY B.ORDER_DATE DESC
    FETCH FIRST 1 ROW ONLY
     ) C
ORDER BY A.EMPLOYEE_ID;
```

![OUTER APPLY 이미지](https://drive.google.com/thumbnail?id=1hPoXPQgu1MC0HMLvKHyFS006skYWSZnS&sz=w1000)

## Reference

- [참고 사이트](https://emrahmeteen.wordpress.com/2015/12/24/oracle-sql-lateral-cross-apply-outer-apply/)