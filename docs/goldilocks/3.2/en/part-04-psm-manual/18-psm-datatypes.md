<a id="fc4c07f6fbc6efb4"></a>

# 18. PSM DataTypes

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/fc4c07f6fbc6efb4)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 17. Overview of PSM](17-overview-of-psm.md) · [Table of contents](../README.md) · [19. PSM Control Statements →](19-psm-control-statements.md)

<a id="eb879fe12d06c29b"></a>
## Built-in Data Types

GOLDILOCKS PSM supports all basic data types provided by GOLDILOCKS SQL in the same way.  
The followings are the basic data types.  
For more information, refer to [Data Type](../part-03-sql-manual/11-sql-elements.md#9ebaf6ccb06f475d).

<a id="75aa09fa54fae961"></a>
### Numeric Types

- NUMBER
- NUMERIC
- FLOAT
- NATIVE_INTEGER
- NATIVE_DOUBLE

<a id="81590d45651c4766"></a>
### CHARACTER STRING Types

- CHARACTER (CHAR)
- CHARACTER VARYING (VARCHAR, VARCHAR2)
- CHARACTER LONG VARYING (LONG VARCHAR)

> Exceptionally, for the compatibility with other database, GOLDILOCKS PSM provides VARCHAR types (VARCHAR2, CHAR VARYING, CHARACTER VARYING) whose precision is not specified, and which is not supported by GOLDILOCKS SQL.   
>   
> This type can not be used when declaring an ordinary variable, but it can be used only when declaring an argument of a subprogram, a return type or an argument of a cursor. If this type is specified, then the argument and the return type is determined as a type with the biggest value among VARCHAR types. (precision = 4000)

<a id="4a65e6e94ef06f18"></a>
### BINARY STRING Type

- BINARY
- BINARY VARYING (VARBINARY)
- BINARY LONG VARYING (LONG VARBINARY)

<a id="d1fd9e272723d4f5"></a>
### DATE/TIME Type

- DATE
- TIME [WITH/WITHOUT TIME ZONE]
- TIMESTAMP [WITH/WITHOUT TIME ZONE]

<a id="647e735c3afc2f8d"></a>
### INTERVAL Type

- INTERVAL YEAR
- INTERVAL MONTH
- INTERVAL YEAR TO MONTH
- INTERVAL DAY
- INTERVAL HOUR
- INTERVAL MINUTE
- INTERVAL SECOND
- INTERVAL DAY TO HOUR
- INTERVAL DAY TO MINUTE
- INTERVAL DAY TO SECOND
- INTERVAL HOUR TO MINUTE
- INTERVAL HOUR TO SECOND
- INTERVAL MINUTE TO SECOND

<a id="f0c5b43b36f8a8fe"></a>
### BOOLEAN Type

BOOLEAN

<a id="69ba87637236541d"></a>
### ROWID Type

ROWID

<a id="f73427d124e6c7e4"></a>
### Declaring Built-in Data Type Variables

A variable can be declared in each declaration section within an anonymous block, a procedure or a function.

```
DECLARE
  V_MSG VARCHAR(20) := 'HELLO, WORLD!';
BEGIN
  DBMS_OUTPUT.PUT_LINE( 'My First Message Is : ' || V_MSG );
END;
/
```

For more information, refer to [Built-in Data Type References](../part-03-sql-manual/11-sql-elements.md#fb134a7b0cc3f5f7).

<a id="d6c7dfda365e716b"></a>
## Attribute Data Types

It is a data type which is used when specifying types of other PSM variables, cursors, tables or a specific column in a table.

If an attribute variable or a target object (table) of a function is altered, then PSM (procedure, function) is automatically compiled again according to the altered type and it is applied.

<a id="c0fceea86400ec50"></a>
### %TYPE

It is used when specifying a type of other variables or a column type of a specific table. The following objects can be referenced.

- Scalar type (Including built-in data type) variables
- User defined record type variables
- A specific field of a record type variable
- Collection type variables
- A specific field of a collection type variable
- A specific column of a table

%TYPE is used as follows.

```
CREATE TABLE EMP ( ID INTEGER, NAME VARCHAR(32) );
INSERT INTO EMP VALUES ( 1001, 'Tom Jackson' );
COMMIT;

DECLARE
  V_NAME EMP.NAME%TYPE;
BEGIN
  SELECT NAME INTO V_NAME FROM EMP;
  DBMS_OUTPUT.PUT_LINE( 'EMP.NAME = ' || V_NAME );
END;
/
```

<a id="6f1a2600407e03f0"></a>
### %ROWTYPE

It is used to specify the structure of a specific table, or the record type as same as the returned type of a specific cursor. It can refer to the following objects.

- Table
- Cursor
- Cursor variable

Neither the record type variable nor collection type variable can be a target of %ROWTYPE.

The following is an example of using %ROWTYPE.

```
DECLARE
  V_EMP EMP%ROWTYPE;
BEGIN
  SELECT * INTO V_EMP FROM EMP WHERE ID = 1001;
  DBMS_OUTPUT.PUT_LINE( 'Name of ID 1001 Is : ' || V_EMP.NAME );
END;
/
```

<a id="53f06c84e41019d3"></a>
### Constraint Attributes Inheritance

The constraint attributes of variables declared as an attribute type inherits the constraint attributes of the reference target as follows.

<a id="ad70939ee622c7b0"></a>
<table class="table column_count_4"><caption>Whether to inherit constraints of the attribute types</caption><thead><tr><th class="to_center"><div>Attribute type</div></th><th class="to_center"><div>Reference target</div></th><th class="to_center"><div>NOT NULL</div></th><th class="to_center"><div>Default value</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="7"><div>%TYPE</div></td><td class="to_middle"><div>Scalar variable</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>Record type variable</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>A specific field of a record type variable</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>Collection type variable - scalar element</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>Collection type variable - record element</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>A specific field of a collection type variable</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>A specific column of a table</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle" rowspan="3"><div>%ROWTYPE</div></td><td class="to_middle"><div>Table</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>Cursor</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>Cursor Variable</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td></tr></tbody></table>

<a id="a7fe2678730e2a7f"></a>
## User-defined Record Type

The record type variable is a complex structure type which consists of several fields of each different type. A record type variable can be created by copying types of other tables or cursors by using %ROWTYPE, or by declaring a data structure which is appropriate to a specific purpose by a user.

A user defined record type can be defined by using TYPE keyword in PSM declarative part as follows. Each field can optionally specify a NOT NULL constraint and a default value.

```
DECLARE
  TYPE MY_EMP_TYPE IS RECORD
  ( 
    ID INTEGER := 99999,
    NAME VARCHAR(32) NOT NULL DEFAULT 'anonymous'
  );
  V_EMP MY_EMP_TYPE;
BEGIN
  SELECT ID, NAME INTO V_EMP.ID, V_EMP.NAME FROM EMP;
  DBMS_OUTPUT.PUT_LINE('ID = ' || V_EMP.ID);
  DBMS_OUTPUT.PUT_LINE('NAME = ' || V_EMP.NAME);
END;
/
```

The following is an example of using it in a nested procedure or in a nested function.

```
DECLARE
  TYPE MY_EMP_TYPE IS RECORD
  ( 
    ID INTEGER := 99999,
    NAME VARCHAR(32) NOT NULL DEFAULT 'anonymous'
  );
  V_EMP MY_EMP_TYPE;
  PROCEDURE SET_EMP( A_EMP IN OUT MY_EMP_TYPE )
  IS
  BEGIN
    DBMS_OUTPUT.PUT_LINE('ID = ' || A_EMP.ID);
    DBMS_OUTPUT.PUT_LINE('NAME = ' || A_EMP.NAME);
    SELECT ID, NAME INTO A_EMP.ID, A_EMP.NAME FROM EMP;
  END;
BEGIN
  SET_EMP( V_EMP );
  DBMS_OUTPUT.PUT_LINE('ID = ' || V_EMP.ID);
  DBMS_OUTPUT.PUT_LINE('NAME = ' || V_EMP.NAME);
END;
/
```

A user defined record type can be used as an argument or a returned type of a general regional variable, a nested procedure, or a nested function. However, it can not be used as an argument or a returned type of a schema-level procedure or a schema-level function.

<a id="311393b9ebe54ea6"></a>
## User-defined Collection Type

User defined collection type is a kind of an array structure which stores one or more data. GOLDILOCKS PSM supports an associative array type which can be stored as key/value pair among collection types.

The following is a basic SYNTAX to declare an associative type.

```
TYPE <type_name> IS TABLE OF <element_data_type> INDEX BY <index_key_data_type>
```

- &lt;type_name&gt; is a user defined name for the type. 
- &lt;element_data_type&gt; specifies a data type of a value which configures an array.
- &lt;index_key_data_type&gt; specifies a data type of an index key which explores for an element.

For example, if the information corresponding to (number) is in form of (name, age), then a table can be created and stored in a database as follows.

```
CREATE TABLE INFO
(
   NO INTEGER,
   NAME VARCHAR(20),
   AGE INTEGER
)
CREATE UNIQUE INDEX IDX_NO ON INFO (NO)
```

- If the information above is stored as an associative array, then its configuration is as follows. 
    - Index_key corresponds to a number (NO).
    - Element_data consists of a name (NAME) and an age (AGE).

An associative array variable to store it is defined within a real PSM as follows.

```
TYPE rec IS RECORD (NAME VARCHAR(20), AGE INTEGER);
TYPE info IS TABLE OF rec INDEX BY INTEGER;
```

For more information, refer to [COLLECTION Variable Declaration](23-psm-language-element-references.md#183f1ba7cf5ec0be).

<a id="27f35b0c9ada8c90"></a>
### Associative Array

An associative array type variable has a data type key specified in an index clause, and it is a PSM variable which can store a value of element data type specified in TABLE OF clause in one or more values in a key/value form.

- The features of an associative array type of GOLDILOCKS PSM is as follows.
    - It has an exploring key in a data type form specified in INDEX BY clause, and it is automatically sorted and stored.
    - It consists of elements specified in TABLE OF clause.
    - It provides exploring functions called as collection methods.
    - It is stored in a replace form when storing an element in an existing index key.
    - The maximum storage size is restricted to the available size of MEMORY_TEMP_TBS_SIZE.

The following is an example of declaring an element type as an SQL data type, and inserting data.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.



gSQL> DECLARE
  TYPE rec IS TABLE OF VARCHAR(20) INDEX BY VARCHAR(10);
  V1 rec;
BEGIN
  V1('aa') := 'Dog';
  V1('bb') := 'Cat';

  INSERT INTO T1 VALUES ( V1('aa'), V1('bb') );
END;
/

Anonymous PL block executed.


gSQL> SELECT * FROM T1;

C1  C2 
--- ---
Dog Cat

1 row selected.
```

The following is an example of having a record type as an element.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.



gSQL> DECLARE
  TYPE rec IS TABLE OF T1%ROWTYPE INDEX BY VARCHAR(10);
  V1 rec;
BEGIN
  V1('person1').C1 := 'seoul';
  V1('person1').C2 := '12';

  V1('person2').C1 := 'busan';
  V1('person2').C2 := '24';

  INSERT INTO T1 VALUES V1('person1'), V1('person2');
END;
/

Anonymous PL block executed.


gSQL> SELECT * FROM T1;

C1    C2
----- --
seoul 12
busan 24

2 rows selected.
```

- The following is a data type which can be specified in an index key of an associative array of GOLDILOCKS PSM. 
    - INTEGER
    - LONG
    - CHAR
    - VARCHAR

- The following is a data type which can be used as an element type of an associative array of GOLDILOCKS PSM.
    - SQL Data Type
    - %TYPE
    - %ROWTYPE
    - User defined Record Type

For more information, refer to [Built-in Data Types](#eb879fe12d06c29b), [%TYPE](#c0fceea86400ec50), [%ROWTYPE](#6f1a2600407e03f0), [User Defined Record Type](#a7fe2678730e2a7f).

<a id="93c91078abe11433"></a>
### Assign Values to Collection Variables

The following rules are applied when assigning values to collection valuables.

- The rules as same as &lt;Assign Statement&gt; is applied to an element assignment. 
- To assign values to the entire collection variable, the types of collection variables should be same.
- When assigning an element of a collection variable, it is operated according to the element data type as follows.
    - Assigning a user defined type element is allowed among same type.
    - Else, it is allowed to assign when data types of a field configuring an element are compatible at a run-time.

The following is an example of an error due to the assignment of a different type.

```
DECLARE
  TYPE udr1 IS RECORD (F1 INTEGER, F2 VARCHAR(20));
  TYPE udr2 IS RECORD (F1 INTEGER, F2 VARCHAR(20));

  TYPE rec1 IS TABLE OF udr1 INDEX BY VARCHAR(10);
  TYPE rec2 IS TABLE OF udr2 INDEX BY VARCHAR(10);

  V1 rec1;
  V2 rec2;
BEGIN
  V2('person1').F1 := 24;
  V2('person1').F2 := 'seoul korea';

  V1 := V2;

END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (14:9): ERR-HY000(17007): invalid expression
```

In the example above, configuration of each field of an element which consists of user defined type is same. However, the variable types are different, so the assignment fails.

The following is an example of succeeding in an assignment by using the same type.

```
DECLARE
  TYPE udr1 IS RECORD (F1 INTEGER, F2 VARCHAR(20));

  TYPE rec1 IS TABLE OF udr1 INDEX BY VARCHAR(10);

  V1 rec1;
  V2 rec1;
BEGIN
  V2('person1').F1 := 24;
  V2('person1').F2 := 'seoul korea';

  V1 := V2;

END;
/

Anonymous PL block executed.
```

Assignment of an associative type in an element unit is allowed only when the data types of elements are compatible.

Refer to the following example.

```
gSQL> CREATE TABLE T1 
(
  c1 VARCHAR(20), 
  c2 VARCHAR(20)
);

Table created.


gSQL> DECLARE
TYPE record_org1 IS RECORD (f1 VARCHAR(20), f2 VARCHAR(20));

TYPE rec1 IS TABLE OF t1%rowtype INDEX BY VARCHAR(10);
TYPE rec2 IS TABLE OF record_org1 INDEX BY VARCHAR(10);

v1 record_org1;
v2 rec1;
v3 rec2;
v4 t1%rowtype;
BEGIN
   
  -- From record_org1 type to %rowtype
  V2('first') := v1;

  -- From record_org1 type to record_org1 type
  V3('first') := v1;
  
  -- From t1%rowtype to record_org1 type
  V3('second') := V2('first');

END;
/

Anonymous PL block executed.
```

An associative type variable is stored in a volatile memory space, and the user accessible TEMP TABLESPACE should be extended when the space is insufficient. The following is an example of an error due to the memory insufficiency.

```
DECLARE
TYPE rec IS TABLE OF t1%rowtype INDEX BY varchar(20);
v1 rec;
BEGIN
  BEGIN
    FOR i IN 1 .. 100000
    LOOP
      v1(i).c1 := i;
      v1(i).c2 := i;
      v1(i).c3 := i;
    END LOOP;

    EXCEPTION WHEN OTHERS THEN
                 dbms_output.put_line('error: count=' || v1.count());
                 dbms_output.put_line('sqlcode=' || SQLCODE);
                 dbms_output.put_line('sqlmsg =' || SQLERRM);
  END;
  dbms_output.put_line('v1.count=' || v1.count());
END;
/
error: count=95004
sqlcode=-14015
sqlmsg =[SUNJESOFT][PSM][GOLDILOCKS]there is no extendible datafile in tablespace 'MEM_TEMP_TBS'
v1.count=95004

Anonymous PL block executed.
```

<a id="1b52c977c635e970"></a>
### Collection Method

A collection method is a function or a procedure which is provided to easily operate a collection type variable. Associative array provides the following methods.

**Collection method**

<a id="8a10f555c0532979"></a>
| Method | Type | Input argument | Return type | Description |
| --- | --- | --- | --- | --- |
| FIRST | Function | X | Index key data type | It returns the first index key. |
| LAST | Function | X | Index key data type | It returns the last index key. |
| COUNT | Function | X | INTEGER | It returns the number of elements. |
| EXISTS | Function | O | BOOLEAN | It returns whether an index key exists or not. |
| PRIOR | Function | O | Index key data type | It returns an index key prior to the input index key. |
| NEXT | Function | O | Index key data type | It returns an index key next to the input index key. |
| DELETE | Procedure | O | N/A | It deletes an element corresponding to the input index key. |

A collection method is used as follows.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.



gSQL> DECLARE
  TYPE rec IS TABLE OF T1%ROWTYPE INDEX BY VARCHAR(10);
  V1 rec;
BEGIN
  V1('person1').C1 := 'seoul';
  V1('person1').C2 := '12';

  V1('person2').C1 := 'busan';
  V1('person2').C2 := '24';

  V1('person3').C1 := 'Daegu';
  V1('person3').C2 := '36';

  -- First method
  DBMS_OUTPUT.PUT_LINE('First Index Key = ' || V1.first() );

  -- Last method
  DBMS_OUTPUT.PUT_LINE('Last Index Key = ' || V1.last() );

  -- Count method
  DBMS_OUTPUT.PUT_LINE('Count of element = ' || V1.count() );

  -- Prior Method
  DBMS_OUTPUT.PUT_LINE('Prior (person1) = ' || V1.prior('person1') ); -- return NULL
  DBMS_OUTPUT.PUT_LINE('Prior (person3) = ' || V1.prior('person3') );

  -- Next Method
  DBMS_OUTPUT.PUT_LINE('Next (person1) = ' || V1.next('person1') );
  DBMS_OUTPUT.PUT_LINE('Next (person3) = ' || V1.next('person3') ); -- return NULL

  -- Exists Method
  DBMS_OUTPUT.PUT_LINE('Exists (person2) = ' || V1.exists('person2') );

  -- Delete Method
  V1.delete('person2');

  -- Exists Method
  DBMS_OUTPUT.PUT_LINE('After delete, Exists (person2) = ' || V1.exists('person2') );
END;
/
First Index Key = person1
Last Index Key = person3
Count of element = 3
Prior (person1) = 
Prior (person3) = person2
Next (person1) = person2
Next (person3) = 
Exists (person2) = TRUE
After delete, Exists (person2) = FALSE

Anonymous PL block executed.
```

If a delete procedure deleting an element can not find an index key corresponding to the input argument, then an error occurs as follows.

```
gSQL> DECLARE
  TYPE rec IS TABLE OF T1%ROWTYPE INDEX BY VARCHAR(10);
  V1 rec;
BEGIN
  V1('person1').C1 := 'seoul';
  V1('person1').C2 := '12';

  -- Call delete procedure
  V1.delete('person2');

END;
/

ERR-HY000(17045): no data found : 
  V1.delete('person2');
  *
ERROR at line 9:
Anonymous PL block executed.
```

<a id="bd15acd74358e3b3"></a>
## SYS_REFCURSOR

SYS_REFCURSOR is a predefined type for a cursor variable, and it is used to declare a cursor variable.

It is used to declare a cursor variable in the following form.

```
cursor_variable_name SYS_REFCURSOR;
```

Cursor variable can be used together with OPEN FOR, FETCH, CLOSE statement as follows.

```
DECLARE
  v1 VARCHAR(20);
  v2 VARCHAR(20);

  cv1 SYS_REFCURSOR;
  cv2 SYS_REFCURSOR;

BEGIN

  OPEN cv1 FOR SELECT * FROM T1;

  cv2 := cv1;

  FETCH cv2 INTO V1, V2;

  DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);
  
END;
/
V1 = Seoul , V2 = 24

Anonymous PL block executed.
```

- The variable declared by using SYS_REFCURSOR is used as follows.
    - It is possible to assign each cursor variable among cursor variables. An existing open cursor of the cursor variable which is on the right of the assign can not be used any more.
    - An explicit cursor can not be assigned to a cursor variable.
    - A variable of a different data type can not be assigned to a cursor variable.
    - A nested function/procedure and schema-level function/procedure can be used as a parameter.

For more information, refer to [CURSOR VARIABLES](20-psm-cursor-statements.md#0a3626c1b20c59c8), [Cursor Variable Declaration](23-psm-language-element-references.md#6646917a8f23fc7a), [OPEN FOR Statement](23-psm-language-element-references.md#68fe3a5ddf93af86).

---

[← 17. Overview of PSM](17-overview-of-psm.md) · [Table of contents](../README.md) · [19. PSM Control Statements →](19-psm-control-statements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
