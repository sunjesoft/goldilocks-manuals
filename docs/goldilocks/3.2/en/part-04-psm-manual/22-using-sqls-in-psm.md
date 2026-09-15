<a id="43a04d4d888c370c"></a>

# 22. Using SQLs in PSM

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/43a04d4d888c370c)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 21. Using PSM Subprograms](21-using-psm-subprograms.md) · [Table of contents](../README.md) · [23. PSM Language Element References →](23-psm-language-element-references.md)

<a id="14d23fd216b36895"></a>
## Static SQLs

Static SQLs are SQLs can be used in PSM, and it is classified are follows.

- [SELECT](#6c447c2a91f2e29a)
- [INSERT](#85882ee9f9dae47a)
- [UPDATE](#1dbb24bb31449b4e)
- [DELETE](#76803b0b71d64afd)
- [RETURNING INTO](#8d334c3990a31187)
- [LOCK TABLE](../part-03-sql-manual/16-sql-references.md#64e196a787076509)
- [COMMIT, ROLLBACK, SAVEPOINT](#654c67abb1f26123)

A static SQL is an extended SQL to perform SQL supported by GOLDILOCKS through PSM variable. This chapter describes features and precautions of a static SQL available only in PSM.

<a id="6c447c2a91f2e29a"></a>
### SELECT

A SELECT statement within PSM receives the result returned from the database, and stores value in a PSM variable specified in INTO clause. The result set of GOLDILOCKS PSM through SELECT INTO can be stored only in a single row.

It can be specified as follows.

```
SELECT target_list INTO variable_list FROM table_expression
```

For more information, refer to [Data Query Language](../part-03-sql-manual/12-sql-languages.md#b04061edd8d6e7d9).

The following is an example of storing a value in a variable declared as an SQL data type by using SELECT statement within PSM.

```
DECLARE
  V1 INTEGER;
BEGIN
  DBMS_OUTPUT.PUT_LINE( 'V1 =[' || V1 || ']');
```

- It stores the result in the variable V1 through SELECT INTO.

```
SELECT 1 INTO V1 FROM DUAL;

  DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1);
END;
/
V1 =[]
V1 = 1
```

The following is an example of storing value in a variable declared as a record type.

```
DECLARE
  TYPE rec is RECORD (F1 INTEGER, F2 INTEGER );
  var1 rec;
BEGIN
  DBMS_OUTPUT.PUT_LINE( 'Var1.f1 =[' || Var1.f1 || ']');
  DBMS_OUTPUT.PUT_LINE( 'Var1.f2 =[' || Var1.f2 || ']');
```

- Store the result in var which is a record type variable.

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

If a result set which has two or more results of SELECT statement is returned form the database, then the following error occurs. A user can catch the error by using TOO_MANY_ROWS exception among predefined exceptions.

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

If a result does not exist in SELECT INTO, then an error occurs. A user can catch the error by using NO_DATA_FOUND exception among predefined exceptions.

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

> If a result of SELECT INTO statement is stored through a record type in GOLDILOCKS, it can not be used by mixing together with a different type variable. If they are used being mixed together, the following error may occur.

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

However, it can be used as follows when a user uses a partial field of a record type by mixing with the SQL data type variable.

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

- A value is not stored in V1.c2.

```
DBMS_OUTPUT.PUT_LINE('V1.c1 = ' || V1.C1 || ' , V1.c2 = ' || V1.C2);
  DBMS_OUTPUT.PUT_LINE('V2    = ' || V2);
END;
/
V1.c1 = Seoul , V1.c2 = 
V2    = 24

Anonymous PL block executed.
```

<a id="85882ee9f9dae47a"></a>
### INSERT

An INSERT statement in PSM provides the following expansion features.

- It can store the data in the database by using a user defined record type variable.
- It can store the data in RETURNING INTO clause by using a record type variable.

In PSM, it can inserts the data in the following form through a record type variable.

```
INSERT INTO table_name VALUES record_type_variable
```

For more information, refer to [Inserting Data](../part-03-sql-manual/12-sql-languages.md#4e6c39af67bfc040).

The following is an example of storing the record in the database by using PSM variable declared as an SQL data type.

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

The following is an example of inserting which uses a record type variable declared with %ROWTYPE.

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

For more information, refer to [%ROWTYPE](18-psm-datatypes.md#6f1a2600407e03f0).

The following is an example of storing the record in the database by using a user defined record type variable.

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

For more information, refer to [User Defined Record Type](18-psm-datatypes.md#a7fe2678730e2a7f).

> If a record type variable is specified in a form other than PSM insert expansion, then the following error occurs.

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

In the example above, two columns are listed and a variable of a specified VALUES clause is one. Though it is a record type variable, but the numbes of values to be bound is different, so an error occurs as above. To use a variable by mixing with a type different from a record type, then it should be specified in a scalar type as follows.

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

<a id="1dbb24bb31449b4e"></a>
### UPDATE

The followings are features expanded from PSM.

- It can alter the database value to a value in a record type variable by using SET ROW clause.
- It can store the value of before/ after the alteration as a PSM variable through RETURNING INTO clause.

A record type variable can be used in the following form through an UPDATE expansion feature within PSM.

```
UPDATE table_list SET ROW = Record_type_variable [WHERE condition]
```

For more information, refer to [Updating Data](../part-03-sql-manual/12-sql-languages.md#afcb9624dda28536).

The following is an example of altering the record through a PSM record type variable and UPDATE ... SET ROW clause.

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

<a id="76803b0b71d64afd"></a>
### DELETE

An expansion feature of PSM DELETE is as follows.

- It can store the deleted value as a record type variable through RETURNING INTO.

The following is an example of performing DELETE through PSM variable of SQL data type.

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

<a id="8d334c3990a31187"></a>
### RETURNING INTO

It can store the result of processing DML (INSERT, UPDATE, DELETE) as a PSM variable by using RETURNING INTO clause.

- It has following restrictions when storing the result in RETURNING INTO of PSM.
    - The result returned to the database can be stored only in a single row. (Two or more results can not be stored.)
    - It can not be used together with a different type variable when storing as a record type variable.

<a id="a82fe7958e78df8f"></a>
#### INSERT RETURNING INTO

INSERT RETURNING INTO clause stores the result value stored in the database as a PSM variable specified in RETURNING INTO clause.

The following is an example of storing the result of performing *insert* in a PSM variable.

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

The following is an example storing the result of a *returning into* by using a record type variable.

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

<a id="b9322698566f4985"></a>
#### UPDATE RETURNING INTO

UPDATE RETURNING INTO can store the result before/ after the alteration in the database through a PSM variable specified in RETURNING INTO clause.

It stores the result of RETURNING INTO through an SQL type variable as follows.

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

- It stores the result of when before it is altered by UPDATE in V3 and variable V3.

```
UPDATE T1 SET C2 = V2 WHERE C1 = V1
RETURNING OLD * INTO V3, V4;

DBMS_OUTPUT.PUT_LINE('OLD');
DBMS_OUTPUT.PUT_LINE('V3 = ' || V3);
DBMS_OUTPUT.PUT_LINE('V4 = ' || V4);
ROLLBACK;
```

- It stores the result of when after it is altered by UPDATE in V3 and variable V3.

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

The following is an example of storing the result of RETURNING INTO by using a record type variable.

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

- Store the result in a record type variable (V3).

```
UPDATE T1 SET C2 = V2 WHERE C1 = V1
RETURNING OLD * INTO V3;

DBMS_OUTPUT.PUT_LINE('OLD');
DBMS_OUTPUT.PUT_LINE('V3.C1 = ' || V3.C1);
DBMS_OUTPUT.PUT_LINE('V3.C2 = ' || V3.C2);
ROLLBACK;
```

- Store the result in a record type variable (V3).

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

<a id="6a7682d1eb0340c6"></a>
#### DELETE RETURNING INTO

DELETE RETURNING INTO can store the data of a row deleted from the database in a PSM variable.

The following is an example of using SQL type variables.

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

- Store the data of when before DELETE in the variable V1 and V2.

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

The following is an example of storing the data of when before DELETE through a record type variable.

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

- Store the data of when before DELETE in the variable V3.

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

<a id="654c67abb1f26123"></a>
### COMMIT, ROLLBACK, SAVEPOINT

COMMIT, ROLLBACK, SAVEPOINT statements permanently store the transaction result which occurred within PSM in the database, or rolls back it to the state of when before the alteration.

<a id="abe5e5c770bf8b62"></a>
#### COMMIT

COMMIT permanently stores the transaction result in the database. It is used as follows.

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

<a id="f380981ea59c46c6"></a>
#### ROLLBACK

ROLLBACK rolls back the transaction to its previous state. It is used as follows.

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

- 		 	Verify if the DELETE ROLLBACK data is normally retrieved in PSM.

```
gSQL> SELECT * FROM T1;

C1 C2
-- --
 1  1

1 row selected.
```

<a id="e4b2f9b826b4c4cd"></a>
#### SAVEPOINT

SAVEPOINT rolls back a transaction to the user defined location by using ROLLBACK TO SAVEPOINT statement.

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

- Assign the current location as a SAVEPOINT.

```
SAVEPOINT SV1;

DELETE FROM T1 WHERE C1 = 1;
```

- ROLLBACK it to the savepoint SV1.

```
ROLLBACK TO SAVEPOINT SV1;
```

- Verify if it is normally ROLLBACK to the SAVEPOINT.

```
SELECT C2 INTO V1 FROM T1 WHERE C1 = 1;
DBMS_OUTPUT.PUT_LINE('After Rollback: V1 = ' || V1 );
END;
/
Before delete: V1 = 10
After Rollback: V1 = 10

Anonymous PL block executed.
```

<a id="00efcd85c1685f45"></a>
## Dynamic SQL

Unlike a static SQL, the syntax of a dynamic SQL is determined at the time of execution.

In PSM, a dynamic SQL created by a user at run-time can be performed through EXECUTE IMMEDIATE or OPEN FOR statement.

- A dynamic SQL is used in the following cases.
    - When an SQL statement can not be determined when compiling. (e.g. When an SQL statement should be altered according to conditions.)
    - When an SQL which is not supported in a static SQL is performed. (e.g. DDL)
- The syntax of a dynamic SQL is unknown until the time of execution, so a run-time error may occur due to a syntax error, existence of a target object and validation of a user privilege.

- A dynamic SQL can be used in the following PSM statements.
    - [EXECUTE IMMEDIATE Statement](23-psm-language-element-references.md#514a111028d257d2)
    - [OPEN FOR Statement](23-psm-language-element-references.md#68fe3a5ddf93af86)

<a id="0f0e1fda103c0e4c"></a>
### EXECUTE IMMEDIATE

Various dynamic SQLs can be performed in EXECUTE IMMEDIATE. However, a statement in a form of an SQL extension provided by PSM can not be used.

The statement is provided in the following form.

```
EXECUTE IMMEDIATE 'dynamic sql' [ USING [IN | OUT | INOUT] variable_list] [INTO variable_list] [RETURNING INTO variable_list]
```

A value stored in a PSM variable can be applied to a database through USING, INTO, RETURNING INTO statements which are provided to an EXECUTE IMMEDIATE statement, or a value can be stored from a database to a PSM variable. The differences of using each statement are as follows.

- USING 
    - It uses an IN-mode when applying a value of PSM variable to an SQL.
    - It uses an OUT-mode when storing the result of SQL processing in a PSM variable.
        - Therefore, if uses an OUT-mode, it should be described with PSM variables. (An expression is not available.)
    - An IN-mode is applied when a binding type of the variable specified in USING clause is not specified.
    - It is operated as same as using SELECT INTO clause when a target of SELECT is returned as USING OUT.
    - Only a single row can be returned from the database. If two or more results occurs then an error occurs.
    - A PSM variable in a USING IN clause can use only a form of scalar type.
    - A PSM variable in a USING OUT clause can use a record type, but it can not use it by mixing with another type.
- INTO
    - It is used when storing the result of SELECT which is internally processed in a database using an implicit cursor.
    - It can be used only when executing SELECT clause using a dynamic SQL method. (SELECT INTO clause can not be used.)
    - A PSM variable can be a record-type, but it can not be used by mixing with another type. 
- RETURING INTO
    - It is used when storing the before/ after of the data processed by INSERT/ UPDATE/ DELETE.
    - It can store only a single row.
    - A PSM variable can be a record-type, but it can not be used by mixing with another type.

The following is an example of outputting the SELECT_INTO statement result by using a dynamic SQL.

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

The following is an example of performing an altering operation and storing the result of when before the alteration in a variable specified in RETURNING INTO.

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

For more information. refer to [EXECUTE IMMEDIATE Statement](23-psm-language-element-references.md#514a111028d257d2).

<a id="281b4c385d6add60"></a>
### OPEN FOR, FETCH and CLOSE

When processing a query by using EXECUTE IMMEDIATE, the database can not return one or more results. If an SQL to be processed is a dynamic SQL, and two or more result sets should be fetched, like as a cursor, then use OPEN FOR.

The a dynamic SQL in the following form can be used in OPEN FOR statement.

```
OPEN Cursor_variable FOR dynamic_sql [USING variable_list]
```

The following is an example of performing OPEN FOR statement through a dynamic SQL.

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

- USING clause in OPEN FOR statement has the following constraints. 
    - Binding mode
        - Only IN mode is available.
    - Available items
        - PSM variable
        - Value expression whose result is returned as a scalar type

For more information, refer to [OPEN FOR Statement](23-psm-language-element-references.md#68fe3a5ddf93af86), [FETCH Statement](23-psm-language-element-references.md#d0a634aca82150c3), [CLOSE Statement](23-psm-language-element-references.md#9a94c6cb1ad85bd0).

---

[← 21. Using PSM Subprograms](21-using-psm-subprograms.md) · [Table of contents](../README.md) · [23. PSM Language Element References →](23-psm-language-element-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
