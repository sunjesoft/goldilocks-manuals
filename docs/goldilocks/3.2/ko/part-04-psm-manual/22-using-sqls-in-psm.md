<a id="8b691252fb3da255"></a>

# 22. Using SQLs in PSM

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/8b691252fb3da255)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 21. Using PSM Subprograms](21-using-psm-subprograms.md) · [전체 목차](../README.md) · [23. PSM Language Element References →](23-psm-language-element-references.md)

<a id="ddbc3cfb099c2b99"></a>
## Static SQLs

Static SQL은 PSM에서 사용할 수 있는 SQL로써 다음과 같이 분류한다.

- [SELECT](#acf83506e65b676e)
- [INSERT](#553e18805b90b336)
- [UPDATE](#bb5bcf08f7a150d4)
- [DELETE](#46b7f75f8770bd1b)
- [RETURNING INTO](#598dfc464326df87)
- [LOCK TABLE](../part-03-sql-manual/16-sql-references.md#a6a53775fc0e6d73)
- [COMMIT, ROLLBACK, SAVEPOINT](#33b3ce2ad9875923)

Static SQL은 GOLDILOCKS에서 지원하는 SQL을 PSM 변수를 통해 실행할 수 있도록 확장된 SQL이다.   
본 장에서는 PSM에서만 사용할 수 있는 static SQL의 기능과 주의사항에 대해 설명한다.

<a id="acf83506e65b676e"></a>
### SELECT

PSM 내의 SELECT 문은 데이터베이스로부터 결과를 반환받아 INTO 절에 기술된 PSM 변수에 값을 저장한다. SELECT INTO를 통한 GOLDILOCKS PSM의 결과 집합은 single row만 저장할 수 있다.

다음과 같은 형태로 표현할 수 있다.

```
SELECT target_list INTO variable_list FROM table_expression
```

자세한 내용은 [Data Query Language](../part-03-sql-manual/12-sql-languages.md#5de8d922befce410)를 참조한다.

다음은 PSM 내에서 SELECT 문을 이용하여 SQL data type으로 선언된 변수에 값을 저장하는 예이다.

```
DECLARE
  V1 INTEGER;
BEGIN
  DBMS_OUTPUT.PUT_LINE( 'V1 =[' || V1 || ']');
```

- SELECT INTO를 통해 V1 변수에 결과를 저장한다.

```
SELECT 1 INTO V1 FROM DUAL;

  DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1);
END;
/
V1 =[]
V1 = 1
```

다음은 record type으로 선언된 변수에 값을 저장하는 예이다.

```
DECLARE
  TYPE rec is RECORD (F1 INTEGER, F2 INTEGER );
  var1 rec;
BEGIN
  DBMS_OUTPUT.PUT_LINE( 'Var1.f1 =[' || Var1.f1 || ']');
  DBMS_OUTPUT.PUT_LINE( 'Var1.f2 =[' || Var1.f2 || ']');
```

- Record type 변수인 var에 결과를 저장한다.

```
SELECT 1, 2 INTO var1 FROM DUAL;

  DBMS_OUTPUT.PUT_LINE( 'Var1.f1 = ' || Var1.f1);
  DBMS_OUTPUT.PUT_LINE( 'Var1.f2 = ' || Var1.f2);
END;
/
Var1.f1 =[]
Var1.f2 =[]
Var1.f1 = 1
Var1.f2 = 2
```

SELECT 문의 결과가 두 개 이상인 결과 집합이 데이터베이스로부터 반환될 경우 다음과 같은 오류가 발생한다. 사용자는 predefined exception 중에 TOO_MANY_ROWS exception으로 오류를 catch 할 수 있다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.


gSQL> INSERT INTO T1 VALUES ('Seoul', '24');

1 row created.

gSQL> INSERT INTO T1 VALUES ('Pusan', '44');

1 row created.




gSQL> DECLARE
  v1 VARCHAR(20);
  v2 VARCHAR(20);
BEGIN

  BEGIN
     SELECT * INTO V1, V2 FROM T1;
  EXCEPTION WHEN TOO_MANY_ROWS 
            THEN DBMS_OUTPUT.PUT_LINE( 'SQLCODE=' || SQLCODE);
                 DBMS_OUTPUT.PUT_LINE( 'SQLERRM=' || SQLERRM);
  END;
END;
/
SQLCODE=-16289
SQLERRM=[SUNJESOFT][PSM][GOLDILOCKS]into clause can have only one row

Anonymous PL block executed.
```

SELECT INTO에 결과가 존재하지 않으면 오류가 발생한다. 사용자는 predefined exception 중에 NO_DATA_FOUND exception으로 오류를 catch 할 수 있다.

```
DECLARE
    V1 T1%ROWTYPE;
BEGIN
    SELECT * INTO V1 FROM T1 WHERE C1 = 'NONE';
END;
/

ERR-HY000(17041): execution fail : 
    SELECT * INTO V1 FROM T1 WHERE C1 = 'NONE';
    *
ERROR at line 4:
ERR-HY000(17045): no data found
```

> GOLDILOCKS에서 SELECT INTO 문의 결과를 record type을 통해 저장할 경우 다른 타입 변수와 섞어서 사용할 수 없다. 섞어서 사용할 경우, 다음과 같은 오류가 발생한다.

```
DECLARE
  TYPE rec is RECORD (F1 INTEGER, F2 INTEGER );
  var1 rec;
  v1 integer;
BEGIN
  DBMS_OUTPUT.PUT_LINE( 'Var1.f1 =[' || Var1.f1 || ']');
  DBMS_OUTPUT.PUT_LINE( 'Var1.f2 =[' || Var1.f2 || ']');

  SELECT 1, 2, 3 INTO Var1, v1 FROM DUAL;

  DBMS_OUTPUT.PUT_LINE( 'Var1.f1 = ' || Var1.f1);
  DBMS_OUTPUT.PUT_LINE( 'Var1.f2 = ' || Var1.f2);
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (9:29): ERR-HY000(17046): variables of record type can not be mixed with other variables
```

다만, record type의 일부 필드와 SQL data type 변수는 다음과 같이 섞어서 사용할 수 있다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);
Table created.

gSQL> INSERT INTO T1 VALUES ('Seoul', '24');
1 row created.

gSQL> INSERT INTO T1 VALUES ('Pusan', '44');
1 row created.

gSQL> DECLARE
  v1 t1%ROWTYPE;
  v2 VARCHAR(20);
BEGIN
  SELECT * INTO V1.C1, V2 FROM T1
  WHERE C1 = 'Seoul';
```

- V1.c2에는 값이 저장되지 않는다.

```
DBMS_OUTPUT.PUT_LINE('V1.c1 = ' || V1.C1 || ' , V1.c2 = ' || V1.C2);
  DBMS_OUTPUT.PUT_LINE('V2    = ' || V2);
END;
/
V1.c1 = Seoul , V1.c2 = 
V2    = 24

Anonymous PL block executed.
```

<a id="553e18805b90b336"></a>
### INSERT

PSM에서 INSERT 문은 다음과 같은 확장 기능을 제공한다.

- 사용자가 정의한 record type 변수를 이용하여 데이터베이스에 데이터를 저장할 수 있다.
- Record type 변수를 이용하여 RETURNING INTO 절에 데이터를 저장할 수 있다.

PSM에서는 record type 변수를 통해 다음과 같은 형식으로 데이터를 삽입할 수 있다.

```
INSERT INTO table_name VALUES record_type_variable
```

자세한 내용은 [데이터 추가](../part-03-sql-manual/12-sql-languages.md#667eb3068f5ef598)를 참조한다.

다음은 SQL data type으로 선언된 PSM 변수를 이용하여 데이터베이스에 레코드를 저장하는 예이다.

```
gSQL>
CREATE TABLE T1 
(
  C1 INTEGER,
  C2 INTEGER
);

Table created.

gSQL>
DECLARE
  V1 INTEGER;
  V2 INTEGER;
BEGIN
  V1 := 10;
  V2 := 20;
  
  INSERT INTO T1 (C1, C2) VALUES (V1, V2);
  COMMIT;
END;
/

Anonymous PL block executed.


gSQL> SELECT * FROM T1;

C1 C2
-- --
10 20

1 row selected.
```

다음은 %ROWTYPE으로 선언된 record type 변수를 이용하여 insert하는 예이다.

```
gSQL>
CREATE TABLE T1 
(
  C1 INTEGER,
  C2 INTEGER
);

Table created.


gSQL>
DECLARE
  V1 T1%ROWTYPE;
BEGIN
  V1.C1 := 10;
  V1.C2 := 20;
  
  INSERT INTO T1 VALUES V1;
  COMMIT;
END;
/

Anonymous PL block executed.


gSQL> SELECT * FROM T1;

C1 C2
-- --
10 20

1 row selected.
```

자세한 내용은 [%ROWTYPE](18-psm-datatypes.md#7036485e1abecc35)을 참조한다.

다음은 user-defined record type 변수를 이용하여 데이터베이스에 레코드를 저장하는 예이다.

```
gSQL>
CREATE TABLE T1 
(
  C1 INTEGER,
  C2 INTEGER
);

Table created.

gSQL>
DECLARE
  TYPE rec IS RECORD (F1 INTEGER, F2 INTEGER);
  v1 rec;
BEGIN
  V1.F1 := 10;
  V1.F2 := 20;
  
  INSERT INTO T1 VALUES V1;
  COMMIT;
END;
/

Anonymous PL block executed.


gSQL> SELECT * FROM T1;

C1 C2
-- --
10 20

1 row selected.
```

자세한 내용은 [User-defined Record Type](18-psm-datatypes.md#b5920fbcd6dc58b1)을 참조한다.

> PSM insert 확장이 아닌 다른 형태로 record type 변수를 기술할 경우 다음과 같은 오류가 발생한다.

```
gSQL>
DECLARE
  TYPE rec IS RECORD (F1 INTEGER, F2 INTEGER);
  v1 rec;
  v2 INTEGER;
BEGIN
  V1.F1 := 10;
  V1.F2 := 20;

  V2 := 30;
  
  INSERT INTO T1 (c1, c2) VALUES (V1);
  COMMIT;
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (11:3): ERR-42000(16053): not enough values
```

위의 예에는 두 개의 column이 나열되어 있으며 기술된 VALUES 절의 변수는 한 개이다. Record type의 변수이긴하지만 binding 되어야 하는 값의 개수가 다르기 때문에 위의 예와 같은 오류가 발생한다. Record type과 다른 유형의 변수를 섞어서 사용하려면 다음과 같이 scalar-type으로 기술해야 한다.

```
gSQL> 
DECLARE
  TYPE rec IS RECORD (F1 INTEGER, F2 INTEGER);
  v1 rec;
  v2 INTEGER;
BEGIN
  V1.F1 := 10;
  V1.F2 := 20;

  V2 := 30;
  
  INSERT INTO T1 (c1, c2) VALUES (V1.F1, V2);
  COMMIT;
END;
/

Anonymous PL block executed.


gSQL> SELECT * FROM T1;

C1 C2
-- --
10 30

1 row selected.
```

<a id="bb5bcf08f7a150d4"></a>
### UPDATE

PSM에서 확장된 기능은 다음과 같다.

- SET ROW 절을 이용하여 데이터베이스의 값을 record type 변수에 있는 값으로 갱신할 수 있다.
- RETURNING INTO 절을 통해 갱신 전/ 후의 값을 PSM 변수로 저장할 수 있다.

PSM 내 UPDATE 확장 기능을 통해 record type 변수를 다음과 같은 형태로 사용할 수 있다.

```
UPDATE table_list SET ROW = Record_type_variable [WHERE condition]
```

자세한 내용은 [데이터 갱신](../part-03-sql-manual/12-sql-languages.md#87a151f5a8e28b83)을 참조한다.

다음은 PSM record type 변수와 UPDATE ... SET ROW 절을 통해 레코드를 갱신하는 예이다.

```
gSQL> CREATE TABLE T1 
(
  C1 INTEGER,
  C2 INTEGER
);

Table created.


gSQL> INSERT INTO T1 VALUES (1, 1);

1 row created.

gSQL> DECLARE
  V1 T1%ROWTYPE;
BEGIN
  V1.C1 := 10;
  V1.C2 := 20;
  
  UPDATE T1 SET ROW = V1 WHERE c1 = 1;
  COMMIT;
END;
/

Anonymous PL block executed.


gSQL> SELECT * FROM T1;

C1 C2
-- --
10 20

1 row selected.
```

<a id="46b7f75f8770bd1b"></a>
### DELETE

PSM DELETE의 확장 기능은 다음과 같다.

- RETURNING INTO를 통해 삭제된 값을 record type 변수로 저장할 수 있다.

다음은 SQL data type PSM 변수를 통해 DELETE를 수행하는 예이다.

```
gSQL> CREATE TABLE T1 
(
  C1 INTEGER,
  C2 INTEGER
);

Table created.


gSQL> INSERT INTO T1 VALUES (1, 1);

1 row created.


gSQL> DECLARE
  V1 INTEGER;
BEGIN
  V1 := 1;
  
  DELETE FROM T1 WHERE C1 = V1;
  COMMIT;
END;
/

Anonymous PL block executed.


gSQL> SELECT * FROM T1;

no rows selected.
```

<a id="598dfc464326df87"></a>
### RETURNING INTO

DML (INSERT, UPDATE, DELETE) 처리 결과를 RETURNING INTO 절을 이용해 PSM 변수로 저장할 수 있다.

- PSM의 RETURNING INTO에 결과를 저장할 경우 다음과 같은 제약을 받는다.
    - 데이터베이스로 반환되는 결과는 single row로만 저장할 수 있다. (두 건 이상의 결과를 저장할 수 없다.)
    - Record type 변수로 저장할 경우 다른 유형의 변수와 함께 사용할 수 없다.

<a id="b3395e978238f012"></a>
#### INSERT RETURNING INTO

INSERT RETURNING INTO 절은 데이터베이스에 저장된 결과값을 RETURNING INTO에 기술된 PSM 변수로 저장한다.

다음은 insert를 수행한 결과를 PSM 변수에 저장하는 예이다.

```
gSQL>
DECLARE
  v1 INTEGER;
  v2 INTEGER;
  v3 INTEGER;
  v4 INTEGER;
BEGIN
  V1 := 10;
  V2 := 20;
  
  INSERT INTO T1 (c1, c2) VALUES (V1, V2)
  RETURNING * INTO V3, V4;

  DBMS_OUTPUT.PUT_LINE( 'V3 = ' || V3 );
  DBMS_OUTPUT.PUT_LINE( 'V4 = ' || V4 );
END;
/
V3 = 10
V4 = 20
```

다음은 record type 변수를 이용하여 returning into의 결과를 저장하는 예이다.

```
gSQL>
DECLARE
  v1 INTEGER;
  v2 INTEGER;
  v3 T1%ROWTYPE;
BEGIN
  V1 := 10;
  V2 := 20;
  
  INSERT INTO T1 (c1, c2) VALUES (V1, V2)
  RETURNING * INTO V3;

  DBMS_OUTPUT.PUT_LINE( 'V3.C1 = ' || V3.C1 );
  DBMS_OUTPUT.PUT_LINE( 'V3.C2 = ' || V3.C2 );
END;
/
V3.C1 = 10
V3.C2 = 20

Anonymous PL block executed.
```

<a id="b5a9a238cef7e3e4"></a>
#### UPDATE RETURNING INTO

UPDATE RETURNING INTO는 RETURNING INTO 절에 기술된 PSM 변수를 통해 갱신되기 전/ 후의 결과를 데이터베이스에 저장할 수 있다.

다음과 같이 SQL type 변수를 통해 RETURNING INTO의 결과를 저장한다.

```
gSQL> CREATE TABLE T1 
(
  C1 INTEGER,
  C2 INTEGER
);

Table created.


gSQL> INSERT INTO T1 VALUES (1, 1);

1 row created.


gSQL> DECLARE
  V1 INTEGER;
  V2 INTEGER;
  V3 INTEGER;
  V4 INTEGER;
BEGIN
  V1 := 1;
  V2 := 2;
```

- UPDATE에 의해 갱신되기 전의 결과를 V3와 V3 변수에 저장한다.

```
UPDATE T1 SET C2 = V2 WHERE C1 = V1
RETURNING OLD * INTO V3, V4;

DBMS_OUTPUT.PUT_LINE('OLD');
DBMS_OUTPUT.PUT_LINE('V3 = ' || V3);
DBMS_OUTPUT.PUT_LINE('V4 = ' || V4);
ROLLBACK;
```

- UPDATE에 의해 갱신된 후의 결과를 V3와 V3 변수에 저장한다.

```
UPDATE T1 SET C2 = V2 WHERE C1 = V1
RETURNING NEW * INTO V3, V4;

DBMS_OUTPUT.PUT_LINE('NEW');
DBMS_OUTPUT.PUT_LINE('V3 = ' || V3);
DBMS_OUTPUT.PUT_LINE('V4 = ' || V4);

END;
/
OLD
V3 = 1
V4 = 1
NEW
V3 = 1
V4 = 2

Anonymous PL block executed.
```

다음은 record type 변수를 이용하여 RETURNING INTO의 결과를 저장하는 예이다.

```
gSQL> CREATE TABLE T1 
(
  C1 INTEGER,
  C2 INTEGER
);

Table created.


gSQL> INSERT INTO T1 VALUES (1, 1);

1 row created.


gSQL> DECLARE
  V1 INTEGER;
  V2 INTEGER;
  V3 T1%ROWTYPE;
BEGIN
  V1 := 1;
  V2 := 2;
```

- Record type 변수인 V3에 결과를 저장한다.

```
UPDATE T1 SET C2 = V2 WHERE C1 = V1
RETURNING OLD * INTO V3;

DBMS_OUTPUT.PUT_LINE('OLD');
DBMS_OUTPUT.PUT_LINE('V3.C1 = ' || V3.C1);
DBMS_OUTPUT.PUT_LINE('V3.C2 = ' || V3.C2);
ROLLBACK;
```

- Record type 변수인 V3에 결과를 저장한다.

```
UPDATE T1 SET C2 = V2 WHERE C1 = V1
RETURNING NEW * INTO V3;

DBMS_OUTPUT.PUT_LINE('NEW');
DBMS_OUTPUT.PUT_LINE('V3.C1 = ' || V3.C1);
DBMS_OUTPUT.PUT_LINE('V3.C2 = ' || V3.C2);

END;
/
OLD
V3.C1 = 1
V3.C2 = 1
NEW
V3.C1 = 1
V3.C2 = 2

Anonymous PL block executed.
```

<a id="77ec31f0dfc70f9e"></a>
#### DELETE RETURNING INTO

DELETE RETURNING INTO는 데이터베이스에서 삭제한 row의 데이터를 PSM 변수에 저장할 수 있다.

다음은 SQL type 변수들을 사용하는 예이다.

```
gSQL> CREATE TABLE T1 
(
  C1 INTEGER,
  C2 INTEGER
);

Table created.


gSQL> INSERT INTO T1 VALUES (1, 1);

1 row created.


gSQL> DECLARE
  V1 INTEGER;
  V2 INTEGER;
  V3 INTEGER;
BEGIN
  V3 := 1;
```

- V1, V2 변수에 DELETE 이전의 데이터를 저장한다.

```
DELETE FROM T1 WHERE C1 = V3
RETURNING * INTO V1, V2;

DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 );
DBMS_OUTPUT.PUT_LINE('V2 = ' || V2 );
END;
/
V1 = 1
V2 = 1

Anonymous PL block executed.
```

다음은 record type 변수를 통해 DELETE 이전의 data를 저장하는 예이다.

```
gSQL> CREATE TABLE T1 
(
  C1 INTEGER,
  C2 INTEGER
);

Table created.


gSQL> INSERT INTO T1 VALUES (1, 1);

1 row created.


gSQL> DECLARE
  V1 T1%ROWTYPE;
  V3 INTEGER;
BEGIN
  V3 := 1;
```

- V3 변수에 DELETE 전의 데이터를 저장한다.

```
DELETE FROM T1 WHERE C1 = V3
RETURNING * INTO V1;

DBMS_OUTPUT.PUT_LINE('V1.C1 = ' || V1.C1 );
DBMS_OUTPUT.PUT_LINE('V1.C2 = ' || V1.C2 );
END;
/
V1.C1 = 1
V1.C2 = 1

Anonymous PL block executed.
```

<a id="33b3ce2ad9875923"></a>
### COMMIT, ROLLBACK, SAVEPOINT

COMMIT, ROLLBACK, SAVEPOINT 구문은 PSM 내에서 발생한 트랜잭션 결과를 데이터베이스에 영구 저장하거나 갱신 이전의 상태로 돌려 놓는다.

<a id="6ed7412edc9f691d"></a>
#### COMMIT

COMMIT은 트랜잭션 결과를 데이터베이스에 영구적으로 저장한다. 다음과 같이 사용된다.

```
CREATE TABLE T1 
(
  C1 INTEGER,
  C2 INTEGER
);

Table created.


INSERT INTO T1 VALUES (1, 1);

1 row created.


DECLARE
  V3 INTEGER;
BEGIN
  V3 := 1;
  
  DELETE FROM T1 WHERE C1 = V3;
  COMMIT;
END;
/

Anonymous PL block executed.


SELECT * FROM T1;

no rows selected.
```

<a id="446f597c5f4398eb"></a>
#### ROLLBACK

ROLLBACK은 트랜잭션을 이전 상태로 복구한다. 다음과 같이 사용된다.

```
gSQL> CREATE TABLE T1 
(
  C1 INTEGER,
  C2 INTEGER
);

Table created.


gSQL> INSERT INTO T1 VALUES (1, 1);

1 row created.

gSQL> COMMIT;

Commit complete.

gSQL> DECLARE
  V3 INTEGER;
BEGIN
  V3 := 1;
  
  DELETE FROM T1 WHERE C1 = V3;
  ROLLBACK;
END;
/

Anonymous PL block executed.
```

- DELETE ROLLBACK 한 데이터가 PSM에서 정상적으로 조회되는지 확인한다.

```
gSQL> SELECT * FROM T1;

C1 C2
-- --
 1  1

1 row selected.
```

<a id="6589f8a44229ebcc"></a>
#### SAVEPOINT

SAVEPOINT는 ROLLBACK TO SAVEPOINT 문을 이용하여 사용자가 지정한 위치로 트랜잭션을 rollback 한다.

```
gSQL> CREATE TABLE T1 
(
  C1 INTEGER,
  C2 INTEGER
);

Table created.


gSQL> INSERT INTO T1 VALUES (1, 1);

1 row created.


gSQL> DECLARE
  V1 INTEGER;
  BEGIN
  UPDATE T1 SET C2 = 10 WHERE C1 = 1;

  SELECT C2 INTO V1 FROM T1 WHERE C1 = 1;
  DBMS_OUTPUT.PUT_LINE('Before delete: V1 = ' || V1 );
```

- 현재 위치를 SAVEPOINT로 지정한다.

```
SAVEPOINT SV1;

DELETE FROM T1 WHERE C1 = 1;
```

- SV1 지점까지 ROLLBACK 한다.

```
ROLLBACK TO SAVEPOINT SV1;
```

- SAVEPOINT까지 정상적으로 ROLLBACK 되었는지 확인한다.

```
SELECT C2 INTO V1 FROM T1 WHERE C1 = 1;
DBMS_OUTPUT.PUT_LINE('After Rollback: V1 = ' || V1 );
END;
/
Before delete: V1 = 10
After Rollback: V1 = 10

Anonymous PL block executed.
```

<a id="0aa8ef32a2403c92"></a>
## Dynamic SQL

Dynamic SQL은 static SQL과 달리 syntax가 실행 시점에 결정된다.

PSM에서는 EXECUTE IMMEDIATE나 OPEN FOR 구문을 통해 run-time에 사용자가 작성한 dynamic SQL을 수행할 수 있다.

- 다음과 같은 경우에 dynamic SQL을 사용한다.
    - Compile 할 때 SQL 문을 결정할 수 없는 경우 (예: 조건에 따라 SQL 문이 달라져야 하는 경우)
    - Static SQL에서 지원되지 않는 SQL을 수행하는 경우 (예: DDL)
- Dynamic SQL은 실행 시점까지 syntax를 알 수 없기 때문에 syntax 오류, 대상 object의 존재 여부, 사용자 권한 등의 validation에 따라 run-time 오류가 발생할 수 있다.

- Dynamic SQL은 다음과 같은 PSM statement에서 사용할 수 있다.
    - [EXECUTE IMMEDIATE Statement](23-psm-language-element-references.md#56868d6728d2874b) 
    - [OPEN FOR Statement](23-psm-language-element-references.md#e42e171c8ed8be7c)

<a id="79b45e791be7a6b8"></a>
### EXECUTE IMMEDIATE

EXECUTE IMMEDIATE에서는 다양한 dynamic SQL을 수행할 수 있다. 다만, PSM에서 제공되는 SQL extension 형태의 구문은 사용할 수 없다.

다음과 같은 형태의 구문이 제공된다.

```
EXECUTE IMMEDIATE 'dynamic sql' [ USING [IN | OUT | INOUT] variable_list] [INTO variable_list] [RETURNING INTO variable_list]
```

EXECUTE IMMEDIATE 구문에 제공되는 USING, INTO, RETURNING INTO 구문을 통해 PSM 변수에 저장된 값을 데이터베이스에 적용하거나 데이터베이스로부터 PSM 변수에 값을 저장할 수 있다.   
각 구문의 사용 방법에는 다음과 같은 차이가 있다.

- USING 
    - PSM 변수의 값을 SQL에 적용할 경우 IN-mode를 사용한다.
    - SQL의 처리 결과를 PSM 변수에 저장하고자 할 경우 OUT-mode를 사용한다.
        - 따라서 OUT-mode로 사용된 경우 반드시 PSM 변수로 기술되어야 한다. (Expression 사용 불가)
    - USING 절에 기술된 변수의 binding type이 명시되지 않을 경우 IN-mode가 적용 된다.
    - SELECT의 target을 USING OUT으로 반환받을 경우 SELECT INTO 절을 사용한 것과 동일하게 동작한다.
    - 데이터베이스로부터는 single row만 반환받을 수 있으며 두 개 이상의 결과가 발생하면 오류가 발생한다.
    - USING IN 절의 PSM 변수는 scalar type 형태로만 사용할 수 있다.
    - USING OUT 절의 PSM 변수는 record type도 가능하지만 다른 유형과 섞어서 사용할 수는 없다.
- INTO
    - 데이터베이스 내부적으로 implicit cursor를 사용하여 처리되는 SELECT의 결과를 저장할 경우에 사용한다.
    - SELECT 절을 dynamic SQL 방식으로 실행했을 경우에만 사용할 수 있다. (SELECT INTO 절 사용 불가)
    - PSM 변수는 record-type도 가능하지만 다른 유형과 섞어서 사용할 수 없다.
- RETURING INTO
    - INSERT/ UPDATE/ DELETE에 의해 처리된 데이터의 전/ 후를 저장할 경우에 사용한다.
    - Single row만 저장할 수 있다.
    - PSM 변수는 record type도 가능하지만 다른 유형과 섞어서 사용할 수 없다.

다음은 dynamic SQL을 사용하여 SELECT_INTO 구문의 결과를 출력하는 예이다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.


gSQL> INSERT INTO T1 VALUES ('Seoul', '24');

1 row created.

gSQL> INSERT INTO T1 VALUES ('Pusan', '44');

1 row created.


gSQL> DECLARE
  V1 VARCHAR(20);
  V2 VARCHAR(20);
BEGIN
  EXECUTE IMMEDIATE 'SELECT * INTO ?, ? FROM T1 WHERE C1 = ''Seoul''' 
  USING OUT V1, OUT V2;

  DBMS_OUTPUT.PUT_LINE('V1 = ' || V1);
  DBMS_OUTPUT.PUT_LINE('V2 = ' || V2);
END;
/
V1 = Seoul
V2 = 24

Anonymous PL block executed.
```

다음은 갱신 연산을 수행하고 갱신되기 이전의 결과를 RETURNING INTO에 기술된 변수로 저장하는 예이다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.


gSQL> INSERT INTO T1 VALUES ('Seoul', '24');

1 row created.

gSQL> INSERT INTO T1 VALUES ('Pusan', '44');

1 row created.


gSQL> DECLARE
  V1 VARCHAR(20);
  V2 VARCHAR(20);
  V3 VARCHAR(20);
  V4 VARCHAR(20);
BEGIN
  V1 := 'Daegu';
  V2 := '50';

  EXECUTE IMMEDIATE 
      'UPDATE T1 SET C1 = ? ,  C2 = ? WHERE C1 = ''Seoul'' RETURNING OLD * INTO ?, ?' 
  USING V1, V2 RETURNING INTO V3, V4;

  DBMS_OUTPUT.PUT_LINE('V3 = ' || V3);
  DBMS_OUTPUT.PUT_LINE('V4 = ' || V4);
END;
/
V3 = Seoul
V4 = 24

Anonymous PL block executed.
```

자세한 내용은 [EXECUTE IMMEDIATE Statement](23-psm-language-element-references.md#56868d6728d2874b)를 참조한다.

<a id="3c24247c2fd0d332"></a>
### OPEN FOR, FETCH and CLOSE

EXECUTE IMMEDIATE를 사용하여 조회를 처리할 경우 한 건 이상을 데이터베이스로부터 반환받을 수 없다. 처리할 SQL이 dynamic SQL이고 cursor와 같이 두 건 이상의 결과 집합을 fetch 해야 할 경우라면 OPEN FOR를 사용할 수 있다.

다음과 같은 형태로 OPEN FOR에 dynamic SQL을 사용할 수 있다.

```
OPEN Cursor_variable FOR dynamic_sql [USING variable_list]
```

다음은 dynmaic SQL을 통해 OPEN FOR를 수행하는 예이다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.


gSQL> INSERT INTO T1 VALUES ('Seoul', '24');

1 row created.

gSQL> INSERT INTO T1 VALUES ('Pusan', '44');

1 row created.


gSQL> DECLARE
  v1 VARCHAR(20);
  v2 VARCHAR(20);
  v3 VARCHAR(20);

  cv1 SYS_REFCURSOR;
  sqlstr VARCHAR(1024);
BEGIN
   
    sqlstr := 'SELECT * FROM T1 WHERE C1 >= ?';

    v3 := 'AAAA';
    OPEN cv1 FOR sqlstr USING v3;

    FETCH cv1 INTO v1, v2;

    DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);

    CLOSE cv1;
END;
/
V1 = Seoul , V2 = 24

Anonymous PL block executed.
```

- OPEN FOR Statement의 USING 절에는 다음과 같은 제한이 있다.
    - Binding mode
        - IN mode만 가능하다.
    - 사용 가능한 항목
        - PSM 변수
        - Scalar type으로 결과가 반환되는 value expression이다.

자세한 내용은 [OPEN FOR Statement](23-psm-language-element-references.md#e42e171c8ed8be7c), [FETCH Statement](23-psm-language-element-references.md#594c76c9a93d727b), [CLOSE Statement](23-psm-language-element-references.md#e7fbe6f6f64c9346)를 참조한다.

---

[← 21. Using PSM Subprograms](21-using-psm-subprograms.md) · [전체 목차](../README.md) · [23. PSM Language Element References →](23-psm-language-element-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
