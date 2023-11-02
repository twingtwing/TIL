# 🧷 PIVOT과 UNPIVOT  

## 🖇️ PIVOT
PIVOT 연산은 데이터를 행에서 열로 변환하는 기능을 가진 함수이다. 지정한 열의 값을 열로 PIVOT하고, 집계함수를 사용하여 그 열의 데이터를 집계한다.

```SQL
PIVOT [XML]
    (
    집계함수(expr) [AS 별칭] 
    FOR column
    IN (
        expr [AS 별칭] | 
        Subquery | 
        ANY
        ) 
    )
```
- 집계함수(expr) : 집계함수와 집계할 열을 지정하고, 여러 개의 집계함수를 지정할 수 있다.
- FOR 절 : FOR 절은 PIVOT 할 열을 지정한다. 
  - 다수의 열을 기술할 수 있다.
  - FOR 절에 지정되지 않은 열을 기준으로 집계되기 때문에 Inline View를 통해 사용할 열을 지정해야 한다.
- IN 절은 PIVOT 할 열 값 (= FOR 절에서 지정된 열 값)을 지정한다. 
  - IN에 지정된 열 값은 별칭을 통해 원하는 이름으로 지정할 수 있다.
  - XML 옵션을 사용하면 Subquery 혹은 ANY 연산자를 사용할 수 있다.
  
#### 예제 #1

```SQL
SELECT *
FROM(
    SELECT STANDARD_COST, CATEGORY_ID, SUBSTR(DESCRIPTION,0,1) AS DESCS
    FROM PRODUCTS
    )
PIVOT(
    SUM(STANDARD_COST) 
    FOR CATEGORY_ID 
    IN (1, 2, 5, 4)
    );
```
FOR 절의 값(IN 절의 값)들은 열로 변환된다. PIVOT 절은 집계함수에 사용된 STANDARD_COST 컬럼과 FOR 절에 명시되지 않은 DESCS 컬럼을 기준으로 집계된다. 그러므로, Inline View를 사용하여 사용할 열을  지정해야 한다.

![PIVOT TEST 이미지 1](https://drive.google.com/uc?export=view&id=1ycBvnIXkgQlbPnwt8hMCWMzQoDusz3if)

#### 예제 #2 별칭
```SQL
SELECT *
FROM(
    SELECT STANDARD_COST, CATEGORY_ID, SUBSTR(DESCRIPTION,0,1) AS DESCS
    FROM PRODUCTS
    )
PIVOT(
    SUM(STANDARD_COST) AS COST 
    FOR CATEGORY_ID 
    IN (1 AS ID01, 2 AS ID02, 4 AS ID04, 5 AS ID05)
    );
```

FOR절과 IN절은 모두 별칭을 지정 할 수 있다. IN별칭_FOR별칭 형식으로 열 명이 지정된다. 

![PIVOT TEST 이미지 2](https://drive.google.com/uc?export=view&id=1VYIFD8ZeFMhD8xPdSQ6I6QB1je5o7qHd)

**[ 별칭 예시 ]**

|                   | 1      | 1 AS ID01 |
|-------------------|:--------:|:-----------:|
| SUM(COST)         | 1      | ID01      | 
| SUM(COST) AS COST | 1_COST | ID01_COST |

#### 예제 #3 다중 열

**PIVOT 절**은 다수의 집계함수를 지원한다.

```SQL
SELECT *
FROM(
    SELECT STANDARD_COST, LIST_PRICE, CATEGORY_ID, SUBSTR(DESCRIPTION,0,1) AS DESCS
    FROM PRODUCTS
    )
PIVOT(
    SUM(STANDARD_COST) AS COST, MAX(LIST_PRICE) AS PRICE 
    FOR CATEGORY_ID 
    IN (1, 2, 4, 5)
    );
```
집계함수에서 여러 개의 집계함수를 사용할 경우, 서로 구분할 수 있는 별칭을 지정해야 한다. 지정하지 않으면 `ORA-00918: 열의 정의가 애매합니다` 오류가 발생할 수 있다.

![PIVOT TEST 이미지 3](https://drive.google.com/uc?export=view&id=1EaaFjMt7OpFrx0Ym_RCxkRvDDOLu-U7e)

<br>


집계함수 뿐만 아니라 **FOR 절**에도 다수의 열을 기술할 수 있다. 
```SQL
SELECT *
FROM(
    SELECT STANDARD_COST, LIST_PRICE, CATEGORY_ID, 
           SUBSTR(DESCRIPTION,0,1) AS DESCS, MOD(PRODUCT_ID,2) AS PRD_ID
    FROM PRODUCTS
    )
PIVOT(
    SUM(STANDARD_COST) AS COST, MAX(LIST_PRICE) AS PRICE 
    FOR (PRD_ID, CATEGORY_ID) 
    IN ((0,1) AS ID01,(0,2) AS ID02,(0,4) AS ID04,(0,5) AS ID05,(1,1) AS ID11,(1,2) AS ID12,(1,4) AS ID14,(1,5) AS ID15)
    );
```
FO R절에 다수의 열을 사용할 경우, FOR 절의 괄호 안에 열 순서와 IN 절의 괄호 안의 열 값 순서가 일치해야 한다.

![PIVOT TEST 이미지 4](https://drive.google.com/uc?export=view&id=1kkyWVLCOKvW9Ib2uNvsX-0aWiV9gwQ5U)

#### 예제 #4 Subquery & ANY
ORACLE은 IN 절에 동적 값 집합을 직접 사용하기 어려우며, 대신 XML PIVOT을 사용하여 동적 값 집합을 다룰 수 있다. 그러나 XML 없이 Subquery 및 ANY 연산자로 동적 값 집합을 다루는 것은 어렵다.

**[ Subquery ]**

```SQL
SELECT *
FROM(
    SELECT STANDARD_COST, CATEGORY_ID
    FROM PRODUCTS
    )
PIVOT XML
    (
    SUM(STANDARD_COST) AS COST 
    FOR (CATEGORY_ID)
    IN (
        SELECT DISTINCT CATEGORY_ID
          FROM PRODUCTS
       )
    );
```

![PIVOT TEST 이미지 5](https://drive.google.com/uc?export=view&id=1zeBQ_RTjE2MmcCfTt3BX73z0NBXc1jFN)

**[ ANY ]**

```SQL
SELECT *
FROM(
    SELECT STANDARD_COST, CATEGORY_ID, SUBSTR(DESCRIPTION,0,1) AS DESCS
    FROM PRODUCTS
    )
PIVOT XML
    (
    SUM(STANDARD_COST) AS COST 
    FOR (CATEGORY_ID)
    IN (ANY)
    );
```

![PIVOT TEST 이미지 6](https://drive.google.com/uc?export=view&id=1BuQbCxqLK8RI1D_uHiFP0j7j6kS9CTS0)

#### 예제 #5 동적 SQL
ORACLE에서는 IN 절에 동적 값 집합을 직접 사용할 수는 없지만, Dynamic SQL을 통해 이를 구현할 수 있다.

```SQL
VAR RESULT REFCURSOR;

DECLARE
    dynamic_sql VARCHAR(4000);
BEGIN
    FOR X IN (SELECT DISTINCT CATEGORY_ID FROM PRODUCTS)
    LOOP
        dynamic_sql := dynamic_sql || '''' || X.CATEGORY_ID || '''' || ', ';
    END LOOP;
    
    dynamic_sql := SUBSTR(dynamic_sql, 1, LENGTH(dynamic_sql) - 2);

    dynamic_sql :=
        '
            SELECT *
            FROM(
                SELECT STANDARD_COST, CATEGORY_ID
                FROM PRODUCTS
                )
            PIVOT 
                (
                SUM(STANDARD_COST) AS COST 
                FOR (CATEGORY_ID)
                IN (' || dynamic_sql || ')
                )
        ';
        
    DBMS_OUTPUT.PUT_LINE('Dynamic SQL: ' || dynamic_sql);
    OPEN :RESULT FOR dynamic_sql;
    
END;
/

PRINT RESULT
```
![PIVOT TEST 이미지 7](https://drive.google.com/uc?export=view&id=1FfD_stygMDJreJUt1bXUJ7f2DMHRj5WA)

## 🖇️ UNPIVOT
UNPIVOT 연산은 PIVOT 연산과는 반대로 데이터를 열에서 행으로 변환하는 함수이다. 지정한 열의 값을 행으로 UNPIVOT한다.

```SQL
UNPIVOT [{INCLUDE | EXCLUDE} NULLS]
    (
        column  
        FOR column
        IN  column [AS literal]
    )
```
- UNPIVOT 절 : UNPIVOT 절은 UNPIVOT 된 값을 포함할 열의 이름을 지정한다.
  - INCLUDE NULLS : NULL 값 포함
  - EXCLUDE NULLS : NULL 값 미 포함
  - 옵션을 지정하지 않으면 기본적으로 NULL 값을 포함하지 않는다.
- FOR 절 : FOR 절은 UNPIVOT 절에 명시한 열 이름이 포함할 열의 이름을 지정한다.
- IN 절 : IN 절은 UNPIVOT 절에 명시한 열 값과 리터럴 값을 지정한다.

#### 예제 # 1
```SQL 
SELECT *
  FROM (
        SELECT FIRST_NAME, LAST_NAME
          FROM CONTACTS
        )
UNPIVOT(
        NAMES FOR FIRST_LAST IN (FIRST_NAME, LAST_NAME)
        )
```
IN 절의 열 값이 UNPIVOT절에 명시한 열 값으로 이동한다. 또한, IN 절의 열 이름은 FOR 절에 명시한 열 값으로 이동한다.

![UNPIVOT TEST 이미지 1](https://drive.google.com/uc?export=view&id=1OjzRUyw1grdsR18TyOBSJgT23y2nCZbP)

#### 예제 # 2 별칭

```SQL
SELECT *
  FROM (
        SELECT FIRST_NAME, LAST_NAME
          FROM CONTACTS
        )
UNPIVOT(
        NAMES FOR FIRST_LAST IN (FIRST_NAME AS 'FIRST', LAST_NAME AS 'LAST')
        )
```

IN 절에 별칭을 지정하면, FOR 절에 명시한 열의 값이 아닌 별칭으로 열 값을 변경 할 수 있다.

![UNPIVOT TEST 이미지 2](https://drive.google.com/uc?export=view&id=1Wl15qiwKt9OwqT_rPhR4XRXTfdfk9W53)

#### 예제 # 3 옵션

```SQL
SELECT *
  FROM (
        SELECT FIRST_NAME, '' AS LAST_NAME
          FROM CONTACTS
        )
UNPIVOT INCLUDE NULLS
        (
        NAMES FOR FIRST_LAST IN (FIRST_NAME AS 'FIRST', LAST_NAME AS 'LAST')
        );
```

UNPIVOT 연산은 NULL 값을 포함하지 않지만 `INCLUDE NULLS`을 통해 NULL 값을 결과에 포함 할 수 있다.

![UNPIVOT TEST 이미지 3](https://drive.google.com/uc?export=view&id=10SGoQjBz4uxXYP-c_wAfLqqvy4oQ1VUj)

## Reference

- [SQL 전문가 가이드](https://www.yes24.com/Product/Goods/90613346)