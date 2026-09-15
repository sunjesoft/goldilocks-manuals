<a id="43f4f9a3f0cfdd0d"></a>

# 20. PSM Cursor Statements

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/43f4f9a3f0cfdd0d)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 19. PSM Control Statements](19-psm-control-statements.md) · [Table of contents](../README.md) · [21. Using PSM Subprograms →](21-using-psm-subprograms.md)

<a id="b5786d3d2831dc7d"></a>
## Declaration

When retrieving through a PSM statement two or more results can not be returned from the database. Therefore, to retrieve two or more results, a cursor should be used by declaring and defining it.

- Cursors are specified as follows.
    - Explicit cursor
        - A user explicitly declares it through cursor declaration/ definition.
    - Implicit cursor
        - It is a cursor processed through PSM statement within the database, and they can not be defined nor is it declared by a user.

A cursor should be declared and defined in a PSM declare section before using an explicit cursor. (In the following description, a cursor means an explicit cursor.)

- A cursor declaration defines the followings.
    - Cursor name
    - Parameter list owned by a cursor
    - Return type of a cursor

- A cursor definition defines the followings.
    - Cursor name
    - Parameter list owned by a cursor
    - Return type of a cursor
    - SELECT and SELECT .. FOR UPDATE statement which are to be performed by a cursor

- Each item used in a cursor declaration and a cursor definition has the following features. 
    - Cursor name
        - A cursor should be unique within the declared SCOPE.
        - The name should be shorter than 128 bytes.
    - Parameter list
        - It is defined when binding a PSM variable or a value in an SQL which is to be performed by a cursor. 
    - Return type
        - It is used to strictly define the result set of validating an SQL statement owned by a cursor.
        - If a definition of the result of SQL statement owned by a cursor is different from a definition of the return type, then an error occurs.

> A cursor definition should be the same type as the type of the previously declared cursor (name, parameter list, return type).

For a cursor declaration/ definition, refer to the followings.

```
DECLARE
```

- Declaration

```
CURSOR C1 RETURN T1%ROWTYPE;
```

- Declaration & definition

```
CURSOR C2 IS SELECT * FROM T1;
```

- Definition for C1

```
CURSOR C1 RETURN T1%ROWTYPE IS SELECT * FROM T1;
BEGIN
  NULL;
END;
/
```

If the declaration and definition of cursor RETURN TYPE with the same cursor_name are different, then the following error may occur.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.

gSQL> DECLARE
    TYPE rec IS RECORD (C1 VARCHAR(20), C2 VARCHAR(20));
```

The following two cursor return types are same, but it is recognized as using different types. Therefore, an error caused by using the same cursor name occurs.

```
CURSOR C1 RETURN rec;
    CURSOR C1 RETURN T1%ROWTYPE IS SELECT * FROM T1;
BEGIN
    NULL;
END;
/
ERR-HY000(17032): PSM compilation error : 
(1) at (4:12): ERR-HY000(17033): duplicated cursor name
```

If the declaration and the definition of items in a parameter list are different, then an error occurs.

```
DECLARE
```

- The declaration and the definition of a parameter are different. (Parameter name)

```
CURSOR C1 (A1 INTEGER, A2 INTEGER DEFAULT 10) RETURN T1%ROWTYPE;
    CURSOR C1 (A1 INTEGER, A3 INTEGER DEFAULT 10) RETURN T1%ROWTYPE IS 
           SELECT * FROM T1;
BEGIN
    NULL;
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (3:12): ERR-HY000(17033): duplicated cursor name
```

If an SQL statement defined in a cursor should be performed by referring to a PSM variable at the run-time, then it can be defined with a parameter of a cursor.

```
DECLARE
  cursor c1 (a1 varchar ) return t1%rowtype; 
  cursor c2 (a1 varchar(20) ) return t1%rowtype;
BEGIN
  NULL;
END;
/
```

If a DEFAULT clause is defined, the definition of a parameter can be omitted at the time of performing a cursor.   
The following is an example of performing a cursor by inputting all parameters, and an example of performing a cursor by omitting the definition of a parameter in a DEFAULT clause.

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

    CURSOR C1 (A1 INTEGER, A2 INTEGER DEFAULT 10)
        IS SELECT * FROM T1 WHERE C2 >= A1 AND C2 <= A2;
BEGIN
```

- Perform a cursor by inputting all parameters.

```
OPEN C1 (10, 50);
    FETCH C1 INTO V1, V2;

    DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);
    CLOSE C1;
```

- Perform a cursor by omitting a default parameter (A2).

```
OPEN C1 (10);
    FETCH C1 INTO V1, V2;
    IF C1%NOTFOUND = TRUE 
    THEN
        DBMS_OUTPUT.PUT_LINE('NO DATA');
    END IF;
    CLOSE C1;
END;
/
V1 = Seoul , V2 = 24
NO DATA

Anonymous PL block executed.
```

<a id="6ca1557ceee00ab2"></a>
## OPEN

A select statement of a cursor can be performed through OPEN statement after declaration/ definition of the explicit cursor. If it is a SELECT .. FOR UPDATE statement, it locks rows in a result set.

If a cursor OPEN again a CURSOR which is normally OPEN, then an error occurs.

```
DECLARE
  V1 VARCHAR(20);
  V2 VARCHAR(20);

  CURSOR C1 IS SELECT * FROM T1;
BEGIN
  
  OPEN C1;
  OPEN C1;

END;
/

ERR-HY000(17037): cursor is already open : 
  OPEN C1;
       *
ERROR at line 9:
```

If an explicit cursor has a parameter, then it is used as follows.

```
DECLARE
  v1 VARCHAR(20);
  v2 VARCHAR(20);

  cursor c1 (a1 varchar(20) ) return t1%rowtype;
  cursor c1 (a1 varchar(20) ) return t1%rowtype 
    is select * from t1 where c1 = a1;
BEGIN

  OPEN c1( 'Seoul' );

  FETCH c1 INTO V1, V2;

  DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);
  
END;
/
V1 = Seoul , V2 = 24

Anonymous PL block executed.
```

For more information, refer to [OPEN Statement](23-psm-language-element-references.md#808e637f278daebb).

<a id="41eab17443c0911e"></a>
## FETCH

If an explicit cursor is normally OPEN, a result can be stored as a PSM variable through a FETCH statement.

- A result is stored in the following PSM variables.
    - SQL data type variable
    - A record type variable which can store a single row
    - An associative array type variable in which a key is specified available to store a single row

The following is an example of fetching by using an SQL data type variable or through %ROWTYPE.

```
DECLARE

V1 VARCHAR(20);
V2 VARCHAR(20);
V3 T1%ROWTYPE;

CURSOR C1 IS SELECT * FROM T1;
BEGIN

OPEN C1;
```

- List of SQL type variables

```
FETCH C1 INTO V1, V2;
DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);
```

- Single record variables

```
FETCH C1 INTO V3;

DBMS_OUTPUT.PUT_LINE('V3.C1 = ' || V3.C1 || ' , V3.C2 = ' || V3.C2);

END;
/
V1 = Seoul , V2 = 24
V3.C1 = Pusan , V3.C2 = 44
```

A record type variable used in FETCH should be separately used, and if it is used together with another variable, then an error occurs as follows.

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
    V3 T1%ROWTYPE;

    CURSOR C1 (A1 INTEGER, A2 INTEGER DEFAULT 10)
        IS SELECT * FROM T1 WHERE C2 >= A1 AND C2 <= A2;
BEGIN
    OPEN C1 (10, 50);
```

V3 is a record type and a scalar type return result can not be stored in a record type, so an error occurs.

```
FETCH C1 INTO V1, V3;

    CLOSE C1;
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (10:23): ERR-HY000(17007): invalid expression
```

For more information, refer to [FETCH Statement](23-psm-language-element-references.md#d0a634aca82150c3).

<a id="1312f7397981aea2"></a>
## CLOSE

It closes a cursor which is normally OPEN. Results and cursor-attributes can not be obtained from a closed cursor. When accessing to a CLOSE cursor and performing fetch, then an INVALID_CURSOR exception.

```
DECLARE

  V1 VARCHAR(20);
  V2 VARCHAR(20);

  CURSOR C1 IS SELECT * FROM T1;
BEGIN
  
  OPEN C1;
  CLOSE C1;

  BEGIN
    FETCH C1 INTO V1, V2;
  EXCEPTION WHEN INVALID_CURSOR 
            THEN DBMS_OUTPUT.PUT_LINE('invalid cursor exception');
  END;

END;
/
invalid cursor exception

Anonymous PL block executed.
```

For more information, refer to [CLOSE Statement](23-psm-language-element-references.md#9a94c6cb1ad85bd0).

<a id="ccc2f9520b0438a4"></a>
## EXPLICIT CURSOR ATTRIBUTES

Explicit cursor attributes have the information about the current status of an explicit cursor. These attributes can be used both in an expression and a conditional expression.

An explicit cursor attribute is used as the following syntax, and refer to the following table for more information about attributes.

```
Cursor_Name % Attribute_name
Attribute_name :=  ISOPEN
                 | FOUND
                 | NOTFOUND
                 | ROWCOUNT
```

**Cursor attributes**

<a id="e43646336c044fa6"></a>
| Attribute | Return type | Description |
| --- | --- | --- |
| %ISOPEN | BOOLEAN | It is TRUE only when a cursor is normally open.  Otherwise, it is FALSE. |
| %FOUND | BOOLEAN | It is NULL before FETCH, and it is TRUE when FETCH is normally performed. It is FALSE when data does not exist, and it is NULL after CLOSE. |
| %NOTFOUND | BOOLEAN | It is the opposite value of %FOUND. |
| %ROWCOUNT | INTEGER | It is NULL before OPEN, and it is 0 when it is normally OPEN. It increases by 1 whenever FETCH succeeds. |

The following is an example of displaying how the value is changed by phase for each cursor attribute.

```
DECLARE

  V1 VARCHAR(20);
  V2 VARCHAR(20);

  CURSOR C1 IS SELECT * FROM T1;
BEGIN
  
  DBMS_OUTPUT.PUT_LINE('<BEFORE OPEN>');
  DBMS_OUTPUT.PUT_LINE('%ISOPEN   = [' || C1%ISOPEN   || ']');
  DBMS_OUTPUT.PUT_LINE('%FOUND    = [' || C1%FOUND    || ']');
  DBMS_OUTPUT.PUT_LINE('%NOTFOUND = [' || C1%NOTFOUND || ']');
  DBMS_OUTPUT.PUT_LINE('%ROWCOUNT = [' || C1%ROWCOUNT || ']');

  OPEN C1;

  DBMS_OUTPUT.PUT_LINE('<AFTER OPEN>');
  DBMS_OUTPUT.PUT_LINE('%ISOPEN   = [' || C1%ISOPEN   || ']');
  DBMS_OUTPUT.PUT_LINE('%FOUND    = [' || C1%FOUND    || ']');
  DBMS_OUTPUT.PUT_LINE('%NOTFOUND = [' || C1%NOTFOUND || ']');
  DBMS_OUTPUT.PUT_LINE('%ROWCOUNT = [' || C1%ROWCOUNT || ']');

  FETCH C1 INTO V1, V2;

  DBMS_OUTPUT.PUT_LINE('<AFTER FETCH>');
  DBMS_OUTPUT.PUT_LINE('%ISOPEN   = [' || C1%ISOPEN   || ']');
  DBMS_OUTPUT.PUT_LINE('%FOUND    = [' || C1%FOUND    || ']');
  DBMS_OUTPUT.PUT_LINE('%NOTFOUND = [' || C1%NOTFOUND || ']');
  DBMS_OUTPUT.PUT_LINE('%ROWCOUNT = [' || C1%ROWCOUNT || ']');



  CLOSE C1;
  DBMS_OUTPUT.PUT_LINE('<AFTER CLOSE>>');
  DBMS_OUTPUT.PUT_LINE('%ISOPEN   = [' || C1%ISOPEN   || ']');
  DBMS_OUTPUT.PUT_LINE('%FOUND    = [' || C1%FOUND    || ']');
  DBMS_OUTPUT.PUT_LINE('%NOTFOUND = [' || C1%NOTFOUND || ']');
  DBMS_OUTPUT.PUT_LINE('%ROWCOUNT = [' || C1%ROWCOUNT || ']');
END;
/
<BEFORE OPEN>
%ISOPEN   = [FALSE]
%FOUND    = []
%NOTFOUND = []
%ROWCOUNT = []
<AFTER OPEN>
%ISOPEN   = [TRUE]
%FOUND    = []
%NOTFOUND = []
%ROWCOUNT = [0]
<AFTER FETCH>
%ISOPEN   = [TRUE]
%FOUND    = [TRUE]
%NOTFOUND = [FALSE]
%ROWCOUNT = [1]
<AFTER CLOSE>>
%ISOPEN   = [FALSE]
%FOUND    = []
%NOTFOUND = []
%ROWCOUNT = []

Anonymous PL block executed.
```

<a id="4b75fe8cab5394df"></a>
## IMPLICIT_CURSOR_ATTRIBUTES

An implicit cursor is a cursor internally processed in a database through a PSM statement, and it has attributes whose name is as same as that of attributes owned by an explicit cursor.   
For more information, refer to the following table.

**Implicit cursor attributes**

<a id="deb63d34c8c97d78"></a>
| Attribute name | Return type | Description |
| --- | --- | --- |
| ISOPEN | BOOLEAN | It is always FALSE because it is internally closed. |
| FOUND | BOOLEAN | If the data is returned by the previous statement, then it is TRUE. Otherwise, it is FALSE. |
| NOTFOUND | BOOLEAN | It is the opposite value of FOUND. |
| ROWCOUNT | INTEGER | It is the number of rows affected by the previous statement. |

The following is an example of implicit cursor attributes.

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
V1 INTEGER;
BEGIN
    SELECT COUNT(*) INTO V1 FROM T1;
    DBMS_OUTPUT.PUT_LINE('COUNT RET    = ' || V1);
    DBMS_OUTPUT.PUT_LINE('SQL%ISOPEN   = ' || SQL%ISOPEN);
    DBMS_OUTPUT.PUT_LINE('SQL%FOUND    = ' || SQL%FOUND);
    DBMS_OUTPUT.PUT_LINE('SQL%NOTFOUND = ' || SQL%NOTFOUND);
    DBMS_OUTPUT.PUT_LINE('SQL%ROWCOUNT = ' || SQL%ROWCOUNT);
END;
/
COUNT RET    = 2
SQL%ISOPEN   = FALSE
SQL%FOUND    = TRUE
SQL%NOTFOUND = FALSE
SQL%ROWCOUNT = 1

Anonymous PL block executed.
```

<a id="0a3626c1b20c59c8"></a>
## CURSOR VARIABLES

A cursor variable is a concept similar to an explicit cursor. However, an explicit cursor is subordinate to a single statement, a cursor variable plays a role as a point indicating one or more cursor. In other words, it can use a cursor by altering N SQL syntaxes by using a single cursor variable.

- The followings are what are different from an explicit cursor.
    - It alters one or more SELECT queries and processes them with a cursor.
    - It is possible to assign each cursor variable among cursor variables.
    - It can be used in an expression.
    - It can be used as a parameter of a subprogram and schema-level procedure/ function.
    - It can not have a parameter.

It is automatically closed if a cursor open through a cursor variable gets out of the SCOPE where the cursor is declared. However, if it is used as a parameter of a subprogram and schema_level procedure/ function, then it is valid even when that procedure/ function ends until it gets out of the SCOPE where it was called.

> To use a cursor variable as a parameter, a binding-mode of that parameter should be declared as OUT or IN OUT.

A cursor variable can use cursor attributes as same as those of an explicit cursor.

```
DECLARE
  v1 VARCHAR(20);
  v2 VARCHAR(20);

  cv1 SYS_REFCURSOR;
BEGIN
  DBMS_OUTPUT.PUT_LINE('Before Open');
  DBMS_OUTPUT.PUT_LINE('ISOPEN   = ' || cv1%ISOPEN );
  DBMS_OUTPUT.PUT_LINE('FOUND    = ' || cv1%FOUND );
  DBMS_OUTPUT.PUT_LINE('NOTFOUND = ' || cv1%NOTFOUND );
  DBMS_OUTPUT.PUT_LINE('ROWCOUNT = ' || cv1%ROWCOUNT );

  OPEN cv1 FOR SELECT * FROM T1;

  DBMS_OUTPUT.PUT_LINE('After Open');
  DBMS_OUTPUT.PUT_LINE('ISOPEN   = ' || cv1%ISOPEN );
  DBMS_OUTPUT.PUT_LINE('FOUND    = ' || cv1%FOUND );
  DBMS_OUTPUT.PUT_LINE('NOTFOUND = ' || cv1%NOTFOUND );
  DBMS_OUTPUT.PUT_LINE('ROWCOUNT = ' || cv1%ROWCOUNT );

  FETCH cv1 INTO V1, V2;

  DBMS_OUTPUT.PUT_LINE('After fetch');
  DBMS_OUTPUT.PUT_LINE('ISOPEN   = ' || cv1%ISOPEN );
  DBMS_OUTPUT.PUT_LINE('FOUND    = ' || cv1%FOUND );
  DBMS_OUTPUT.PUT_LINE('NOTFOUND = ' || cv1%NOTFOUND );
  DBMS_OUTPUT.PUT_LINE('ROWCOUNT = ' || cv1%ROWCOUNT );
  
END;
/
Before Open
ISOPEN   = FALSE
FOUND    = 
NOTFOUND = 
ROWCOUNT = 
After Open
ISOPEN   = TRUE
FOUND    = 
NOTFOUND = 
ROWCOUNT = 0
After fetch
ISOPEN   = TRUE
FOUND    = TRUE
NOTFOUND = FALSE
ROWCOUNT = 1

Anonymous PL block executed.
```

Cursor variable can be used as a parameter of a subprogram and a schema-level procedure/ function as follows.

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

  cv1 SYS_REFCURSOR;

  PROCEDURE PROC1 ( A_CV1 IN OUT SYS_REFCURSOR )
  IS
  BEGIN
```

- Open a cursor by using an input parameter cursor variable.

```
OPEN A_CV1 FOR SELECT * FROM T1;
  END;

BEGIN

  PROC1( cv1 );
```

- Fetch it by using a cursor variable which was used as a parameter.

```
FETCH cv1 INTO V1, V2;

  DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);
  
END;
/
V1 = Seoul , V2 = 24

Anonymous PL block executed.
```

For more information, refer to [Cursor Variable Declaration](23-psm-language-element-references.md#6646917a8f23fc7a).

<a id="1f999f93680198f2"></a>
### OPEN and Close Cursor Variables

It can OPEN a cursor through a cursor variable if using an OPEN FOR statement within PSM. Also, it can CLOSE a cursor of a cursor variable through a CLOSE statement as same as an explicit cursor.

If an already open cursor exists in a cursor variable at the time of performing a cursor through an OPEN FOR statement, then that cursor is automatically closed and a new cursor is OPEN.

The following is an example of using a cursor variable.

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

  cv1 SYS_REFCURSOR;
BEGIN
  OPEN cv1 FOR SELECT * FROM T1;
```

- Fetch with cursor-variable

```
FETCH cv1 INTO V1, V2;
  
  DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);

  CLOSE cv1;
END;
/
V1 = Seoul , V2 = 24

Anonymous PL block executed.
```

For more information, refer to [OPEN FOR Statement](23-psm-language-element-references.md#68fe3a5ddf93af86), [CLOSE Statement](23-psm-language-element-references.md#9a94c6cb1ad85bd0).

<a id="2a85591966db4e40"></a>
### Fetching Data With Cursor Variables

Like as an explicit cursor, it can store the result processed in a database through a fetch statement as a PSM variable.   
For more information, refer to [FETCH Statement](23-psm-language-element-references.md#d0a634aca82150c3).

<a id="de71331f42f1e314"></a>
### Assign Values to Cursor Variables

It is possible to assign a cursor variable each other if RETURN-TYPEs are same. If it is not a cursor variable type, then an error occurs.

It is performed with the following assign statement.

```
target_cursor_variable := source_cursor_variable
```

Assigning a cursor variable makes a cursor pointer indicated by target_cursor_variable indicate a cursor having Source_cursor_variable. Therefore, after it is normally assigned, a cursor already open in a target cursor variable is not valid nor is it accessible. Also, a cursor is internally cleared when getting out of the SCOPE in which a cursor variable is declared.

```
DECLARE
  v1 VARCHAR(20);
  v2 VARCHAR(20);

  cv1 SYS_REFCURSOR;
  cv2 SYS_REFCURSOR;

BEGIN
```

- Open cv1

```
OPEN cv1 FOR SELECT * FROM T1;
```

- Assign cv1 to cv2

```
cv2 := cv1;
```

- Fetch from cv2

```
FETCH cv2 INTO V1, V2;

  DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);
  
END;
/
V1 = Seoul , V2 = 24
```

The following is an example of using the same cursor by assigning after each cursor variable performs OPEN.

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
  cv1 SYS_REFCURSOR;
  cv2 SYS_REFCURSOR;
  v1 t1%ROWTYPE;
BEGIN
```

- Each cursor variable OPEN a cursor.

```
OPEN cv1 FOR select * from t1 where c1 = 'Seoul';
OPEN cv2 FOR select * from t1 where c1 = 'Pusan';
```

- Assign cursor-variable
- A cursor of cv2 is not valid any more.

```
cv2 := cv1;
```

- Fetch the result of cv1.

```
FETCH cv2 INTO v1;
  
  DBMS_OUTPUT.PUT_LINE('C1 = ' || V1.C1 || ' , C2 = ' || V1.C2);
END;
/
C1 = Seoul , C2 = 24

Anonymous PL block executed.
```

---

[← 19. PSM Control Statements](19-psm-control-statements.md) · [Table of contents](../README.md) · [21. Using PSM Subprograms →](21-using-psm-subprograms.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
