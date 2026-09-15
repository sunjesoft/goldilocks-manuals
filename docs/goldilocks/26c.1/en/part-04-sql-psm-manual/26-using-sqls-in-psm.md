<a id="64082b0803f1502a"></a>

# 26. Using SQLs in PSM

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/64082b0803f1502a)  
> Tag: `26c.1_0_tag`

[← 25. Using PSM Subprograms](25-using-psm-subprograms.md) · [Table of contents](../README.md) · [27. PSM Packages →](27-psm-packages.md)

<a id="488de6a8c43df084"></a>
## Static SQLs

<a id="d860f905cf1376e4"></a>
### Overview

A static SQL is an extended SQL to use PSM variable supported by GOLDILOCKS. PSM variable is available in every expression which allows the bind parameter in SQL.

- SELECT INTO Statement
    - For more information, refer to [SELECT INTO Statement](30-psm-language-element-references.md#25c07665814250e4) in PSM Language Element References.
- Data Manipulation Language( DML )
    - INSERT Statement Extension
        - For more information, refer to [INSERT Statement Extension](30-psm-language-element-references.md#8ba7356240cd29cd) in PSM Language Element References.
    - INSERT INTO ... UPDATE Statement Extension
        - For more information, refer to [INSERT INTO ... UPDATE Statement Extension](30-psm-language-element-references.md#a6c8cd4e6ef22c56) in PSM Language Element References.
    - UPDATE Statement Extension
        - For more information, refer to [UPDATE Statement Extension](30-psm-language-element-references.md#0a1eff9c02b8d066) in PSM Language Element References.
    - DELETE Statement Extension
        - For more information, refer to [DELETE Statement Extension](30-psm-language-element-references.md#a2dbb0a0acf3741e) in PSM Language Element References.
- Transaction Control Language
    - COMMIT
        - For more information, refer to [COMMIT](../part-03-sql-manual/19-sql-references-c-g.md#3beee453ea244831) in SQL References.
    - ROLLBACK
        - For more information, refer to [ROLLBACK](../part-03-sql-manual/20-sql-references-h-z.md#a7f186a4dca1588e) in SQL References.
    - SAVEPOINT
        - For more information, refer to [SAVEPOINT savepoint_specifier](../part-03-sql-manual/20-sql-references-h-z.md#79cec2425d42b60f) in SQL References.
    - LOCK TABLE
        - For more information, refer to [LOCK TABLE](../part-03-sql-manual/20-sql-references-h-z.md#41362c316d3f7f25) in SQL References.

<a id="9e52671c4ab50b97"></a>
#### Examples

- When using the built-in data type PSM variable

```
gSQL> 
DECLARE
  v_id      NUMBER;
  v_name    VARCHAR(50);
BEGIN
  -- SELELECT INTO Statement
  SELECT id , name
    INTO v_id , v_name 
    FROM emp
   WHERE id = 201;

   DBMS_OUTPUT.PUT_LINE( '[SELECT INTO] ' || v_id || ' , ' || v_name );

  -- INSERT Statement Extension
  v_id   := 200;
  v_name := 'Jennifer Whalen';
  INSERT INTO emp VALUES( v_id , v_name );
     
  -- DELETE Statement Extension
  DELETE FROM emp 
   WHERE id = v_id
  RETURNING name INTO v_name;

  DBMS_OUTPUT.PUT_LINE( '[DELETE] ' || v_id || ' , ' || v_name );
 
  -- UPDATE Statement Extension
  UPDATE emp 
     SET id = v_id , name = v_name
   WHERE id = 200;

  -- Commit
  COMMIT;
END;
/

[SELECT INTO] 201 , Michael Hartstein
[DELETE] 200 , Jennifer Whalen
Anonymous PL block executed.
```

- When using the ROW type PSM variable

```
gSQL>
DECLARE
  TYPE rec_emp IS RECORD( f_id emp.id%TYPE , f_name emp.name%TYPE );
  v_rec_emp rec_emp;

BEGIN
  -- SELELECT INTO Statement
  SELECT id , name
    INTO v_rec_emp 
    FROM emp
   WHERE id = 201;

   DBMS_OUTPUT.PUT_LINE( '[SELECT INTO] ' || v_rec_emp.f_id ||
                         ' , ' || v_rec_emp.f_name );

  -- INSERT Statement Extension
  v_rec_emp.f_id   := 200;
  v_rec_emp.f_name := 'Jennifer Whalen';
  INSERT INTO emp VALUES( v_rec_emp.f_id , v_rec_emp.f_name );
     
  -- DELETE Statement Extension
  DELETE FROM emp 
   WHERE id = v_rec_emp.f_id
  RETURNING * INTO v_rec_emp;

   DBMS_OUTPUT.PUT_LINE( '[DELETE] ' || v_rec_emp.f_id ||
                         ' , ' || v_rec_emp.f_name );
 
  -- UPDATE Statement Extension
  UPDATE emp 
     SET ROW = v_rec_emp
   WHERE id = 200;

  -- Commit
  COMMIT;
END;
/

[SELECT INTO] 201 , Michael Hartstein
[DELETE] 200 , Jennifer Whalen
Anonymous PL block executed.
```

<a id="75f12b37ab0b08c5"></a>
### Processing Query Result Sets

PSM processes result sets by using an implicit cursor or an explicit cursor.

PSM defines the implicit cursor as follows.

    - SELECT INTO
    - Implicit Cursor FOR LOOP

PSM defines the explicit cursor as follows.

    - Explicit Cursor FOR LOOP
        - It is an explicit cursor defined by a user, and it is available during executing PSM statement.

<a id="18a8872dc7ab7d5d"></a>
#### Processing Query Result Sets with SELECT INTO Statements

It retrieves the value by executing SELECT INTO statement using an implicit cursor, then stores it in PSM variable.  
The result set of select into statement is always a single row.

<a id="41163e915b34a593"></a>
##### Examples

```
gSQL>
DECLARE
  v_id   emp.id%TYPE;
  v_name emp.name%TYPE;
BEGIN
  SELECT id , name
    INTO v_id , v_name
    FROM emp
   WHERE id = 201;
   
   DBMS_OUTPUT.PUT_LINE( 'SQL%FOUND = ' || SQL%FOUND );
END;
/

SQL%FOUND = TRUE
Anonymous PL block executed.
```

<a id="b684de18dff0aace"></a>
#### Processing Query Result Sets with Cursor FOR LOOP Statements

Cursor For LOOP statement executes an implicit cursor and an explicit cursor, then repeatedly returns the row in the result set.

Implicit cursor FOR LOOP statement is cursor FOR LOOP statement which uses SELECT statement. Implicit cursor FOR LOOP statement returns a row in the result set by using an implicit cursor for the select statement.

An explicit cursor declared by a user is available in cursor FOR LOOP statement  
An explicit cursor declared by a user is also available in another statement in PSM block.

Cursor FOR LOOP statement implicitly creates and uses %ROWTYPE variable for the type returned as a loop index by a cursor.  
A loop index is a variable which is available only during executing cursor FOR LOOP statement.  
PSM statement which is operated during the loop can refer to the record and the field by using a loop index.

Cursor FOR LOOP statement is executed by opening the user defined cursor after creating the loop index variable.   
It stores the row result in the loop index variable whenever repeating the loop.  
If the row is not returned anymore, then the cursor is closed. The cursor is closed even when it throws an exception during the execution.

<a id="e67b7de8a2b943d1"></a>
##### Examples

- When using SELECT statement in cursor FOR LOOP statement

```
gSQL> 
BEGIN
  FOR tmp IN ( SELECT id , name , manager_id FROM emp ) LOOP
    DBMS_OUTPUT.PUT_LINE( 'id = ' || tmp.id || 
                          ' , name = ' || tmp.name || 
                          ' , manager_id = ' || tmp.manager_id );
  END LOOP;


END;
/

id = 200 , name = Jennifer Whalen   , manager_id = 101
id = 201 , name = Michael Hartstein , manager_id = 101
id = 202 , name = Pat Fay           , manager_id = 301
id = 203 , name = Susan Mavris      , manager_id = 201
id = 204 , name = Hermann Baer      , manager_id = 201
id = 205 , name = Shelley Higgins   , manager_id = 301
id = 206 , name = William Gietz     , manager_id = 201
Anonymous PL block executed.
```

- When using an explicit cursor in cursor FOR LOOP statement
    - If the explicit cursor does not have a parameter

```
gSQL>
DECLARE
  CURSOR cur1 IS SELECT id , name , manager_id FROM emp;
BEGIN
  FOR tmp IN cur1 LOOP
    DBMS_OUTPUT.PUT_LINE( 'id = ' || tmp.id || 
                          ' , name = ' || tmp.name || 
                          ' , manager_id = ' || tmp.manager_id );
  END LOOP;
END;
/

id = 200 , name = Jennifer Whalen   , manager_id = 101
id = 201 , name = Michael Hartstein , manager_id = 101
id = 202 , name = Pat Fay           , manager_id = 301
id = 203 , name = Susan Mavris      , manager_id = 201
id = 204 , name = Hermann Baer      , manager_id = 201
id = 205 , name = Shelley Higgins   , manager_id = 301
id = 206 , name = William Gietz     , manager_id = 201
Anonymous PL block executed.
```

    - If the explicit cursor has a parameter

```
gSQL> 
DECLARE
  CURSOR cur1( p1 NUMBER ) IS SELECT id , name , manager_id 
                                FROM emp 
                               WHERE manager_id = p1;
BEGIN
  FOR tmp IN cur1( 201 ) LOOP
    DBMS_OUTPUT.PUT_LINE( 'id = ' || tmp.idgSQL>  || 
                          ' , name = ' || tmp.name || 
                          ' , manager_id = ' || tmp.manager_id );
  END LOOP;
END;
/

id = 203 , name = Susan Mavris      , manager_id = 201
id = 204 , name = Hermann Baer      , manager_id = 201
id = 206 , name = William Gietz     , manager_id = 201
Anonymous PL block executed.
```

<a id="7cc15c407da3e43d"></a>
#### Processing Query Result Sets with Explicit Cursors, OPEN, FETCH, and CLOSE

Declare and use an explicit cursor to control the result set as desired.  
The user can manage the result set by using OPEN, FETCH, CLOSE statement after declaring the explicit cursor.

The query using PL statement may look complicated, but it can flexibly manage the result set as follows.

    - It can process result sets in parallel by using multiple explicit cursors.
    - It can process multiple rows in the result set in parallel or skip a specific row in a single loop statement.
    - Also, it can use multiple loop statements to process the result sets by dividing them.

For more information, refer to [Explicit Cursor](24-psm-cursor-statements.md#c88b9a32652f256c).

<a id="e6a7c66cd03680da"></a>
## Dynamic SQL

Unlike a static SQL, the syntax of a dynamic SQL is determined at the time of execution.

In PSM, a dynamic SQL created by a user at run-time can be performed through EXECUTE IMMEDIATE or OPEN FOR statement.

- A dynamic SQL is used in the following cases.
    - When an SQL statement can not be determined when compiling. (e.g. When an SQL statement should be altered according to conditions.)
    - When an SQL which is not supported in a static SQL is performed. (e.g. DDL)
- The syntax of a dynamic SQL is unknown until the time of execution, so a run-time error may occur due to a syntax error, existence of a target object and validation of a user privilege.

- A dynamic SQL can be used in the following PSM statements.
    - [EXECUTE IMMEDIATE Statement](30-psm-language-element-references.md#0d4e109b14705c96)
    - [OPEN FOR Statement](30-psm-language-element-references.md#326b0ac4f8704e21)

<a id="3b8a47d8373d530a"></a>
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
    - It is operated the same as using SELECT INTO clause when a target of SELECT is returned as USING OUT.
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

For more information. refer to [EXECUTE IMMEDIATE Statement](30-psm-language-element-references.md#0d4e109b14705c96).

<a id="01962a36b0c8f57d"></a>
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

For more information, refer to [OPEN FOR Statement](30-psm-language-element-references.md#326b0ac4f8704e21), [FETCH Statement](30-psm-language-element-references.md#eded620a01801e55), [CLOSE Statement](30-psm-language-element-references.md#be3b8f9c4ae5e8b7).

---

[← 25. Using PSM Subprograms](25-using-psm-subprograms.md) · [Table of contents](../README.md) · [27. PSM Packages →](27-psm-packages.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
