<a id="e3727cfc601c6344"></a>

# 24. PSM Cursor Statements

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/e3727cfc601c6344)  
> Tag: `22c.1_10_tag`

[← 23. PSM Control Statements](23-psm-control-statements.md) · [Table of contents](../README.md) · [25. Using PSM Subprograms →](25-using-psm-subprograms.md)

<a id="2775063fcb2c810b"></a>
## Implicit Cursor

An implicit cursor is defined and managed by PSM statement in the database. PSM statement uses an implicit cursor whenever executing SELECT statement or DML statement. A user can not control an implicit cursor, but it can obtain the information about the query through an implicit cursor attribute.

<a id="9a4254a268428c75"></a>
### Implicit Cursor Attributes

An implicit cursor attributes refer to the execution result of the most recently executed SELECT statement or DML statement. If neither SELECT statement nor is DML statement recently executed, then the attributes values are NULL.

**Implicit cursor attributes**

<a id="fd9b5f35a8083034"></a>
| Attribute name | Return type | Description |
| --- | --- | --- |
| SQL%ISOPEN | BOOLEAN | It always returns FALSE, because the most recently executed SELECT statement or DML statement is always terminated. |
| SQL%FOUND | BOOLEAN | It it TRUE when the most recently executed SELECT statement or DML statement returns a result. Otherwise, it is FALSE. |
| SQL%NOTFOUND | BOOLEAN | It has the opposite value of SQL%FOUND. |
| SQL%ROWCOUNT | INTEGER | It is the number of ROWs returned from the most recently executed SELECT statement or DML statement. |

<a id="60ca189b2937c89b"></a>
### Examples

- When the most recently executed query does not exist

```
gSQL> 
BEGIN
  DBMS_OUTPUT.PUT_LINE('SQL%ISOPEN   = ' || SQL%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('SQL%FOUND    = ' || SQL%FOUND);
  DBMS_OUTPUT.PUT_LINE('SQL%NOTFOUND = ' || SQL%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('SQL%ROWCOUNT = ' || SQL%ROWCOUNT);
END;
/

SQL%ISOPEN   = FALSE
SQL%FOUND    = 
SQL%NOTFOUND = 
SQL%ROWCOUNT = 
Anonymous PL block executed.
```

- When the most recently executed query exists

```
gSQL> 
CREATE TABLE t_month( month_char VARCHAR(15) , month_num INTEGER );
Table created.

gSQL> 
INSERT INTO t_month VALUES( 'JANUARY' , 1 ), ( 'MARCH' , 3 ),
                          ( 'MAY' , 5 ), ( 'JULY' , 7 ),
                          ( 'SEPTEMBER' , 9 ), ( 'NOVEMBER' , 11 );
6 rows created.

gSQL> 
DECLARE
  row_count INTEGER;
BEGIN
  SELECT COUNT(*) INTO row_count FROM t_month;

  DBMS_OUTPUT.PUT_LINE('SQL%ISOPEN   = ' || SQL%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('SQL%FOUND    = ' || SQL%FOUND);
  DBMS_OUTPUT.PUT_LINE('SQL%NOTFOUND = ' || SQL%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('SQL%ROWCOUNT = ' || SQL%ROWCOUNT);
END;
/

SQL%ISOPEN   = FALSE
SQL%FOUND    = TRUE
SQL%NOTFOUND = FALSE
SQL%ROWCOUNT = 1
Anonymous PL block executed.
```

<a id="a6230e6fefe1d385"></a>
## Explicit Cursor

An explicit cursor is declared, defined and managed by a user. The user specifies the cursor name and should connect to SELECT statement or DML statement.

- Use an explicit cursor as follows.
    - The user open the explicit cursor through open statement, and fetches the query result by executing the fetch statement. Last, it closes the cursor with close statement. 
    - The explicit cursor is available for *cursor for loop* statement.

The explicit cursor is not available for an expression. In other words, it can not assign the value to the cursor, nor is it used as a parameter of the procedure or the routine.

- Example of Explicit Cursor

```
gSQL>
CREATE TABLE t_month( month_char VARCHAR(15), month_num INTEGER );
Table created.

gSQL>
INSERT INTO t_month VALUES( 'FEBRUARY' , 2 ), ( 'APRIL' , 4 ), 
                          ( 'JUNE' , 6 ), ( 'AUGUST' , 8 ),
                          ( 'OCTOBER' , 10 ), ( 'DECEMBER' , 12 );
6 rows created.

gSQL>
DECLARE
  CURSOR cur_month IS SELECT * FROM t_month;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN cur_month;                                         ❶ OPEN explicit cursor. 
LOOP                                                   ❷ Fetch multiple ROWs by using loop.
    FETCH cur_month INTO v_month_char, v_month_num;      ❸ FETCH explicit cursor.
     
    EXIT WHEN cur_month%NOTFOUND;                        ❹ Check if all ROWs in the result set are fetched.
    
    DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );
  END LOOP;
    
  CLOSE cur_month;                                       ❺ CLOSE explicit cursor.
END;
/

v_month_char : FEBRUARY , v_month_num : 2
v_month_char : APRIL , v_month_num : 4
v_month_char : JUNE , v_month_num : 6
v_month_char : AUGUST , v_month_num : 8
v_month_char : OCTOBER , v_month_num : 10
v_month_char : DECEMBER , v_month_num : 12
Anonymous PL block executed.
```

<a id="70ec4a4076ebfd00"></a>
### Declaring and Defining Explicit Cursors

An explicit cursor should be declared and defined in PSM declare section to use it. The cursor name, the parameter information and the return type of when declaring the explicit cursor should be as same as when defining the explicit cursor. For more information about the syntax of the explicit cursor and others, refer to [Explicit Cursor Declaration and Definition](28-psm-language-element-references.md#62d5cee16d9ec063).

<a id="36240354f23b2b29"></a>
#### Example of Declaring and Defining Explicit Cursor

```
gSQL>
DECLARE
  CURSOR cur_month1( p1 INTEGER ) RETURN t_month%rowtype;
  CURSOR cur_month1( p1 INTEGER ) RETURN t_month%rowtype IS SELECT * FROM t_month WHERE month_num = p1;

  CURSOR cur_month2 IS SELECT * FROM t_month;
BEGIN
  NULL;
END;
/

Anonymous PL block executed.
```

<a id="1a04855ffaf5f445"></a>
### Opening and Closing Explicit Cursors

- Perform the cursor query by executing [OPEN Statement](28-psm-language-element-references.md#0b103b7706cdb5b9) after declaring and defining the explicit cursor.
- If the query of the explicit cursor is SELECT ... FOR UPDATE statement, then it locks the ROW in the result set
- If the query of the explicit cursor refers to an explicit cursor parameter or a PSM variable, then it affects the query result.
- Close the explicit cursor by using [CLOSE Statement](28-psm-language-element-references.md#01a3ed87cb2dd917) after using the cursor. It can not fetch the record from the result set after the explicit cursor is closed. 
- Once after the explicit cursor is OPENed it can not be reopened, CLOSE it first to OPEN it again.

<a id="7a39ba27e64017ce"></a>
#### Example of Explicit Cursor OPEN and CLOSE

```
gSQL>
DECLARE
  CURSOR cur_month( p1 INTEGER ) IS SELECT * FROM t_month WHERE month_num = p1;
BEGIN
  OPEN cur_month( 2 );      -- Explicit Cursor OPEN

  CLOSE cur_month;          -- Explicit Cursor CLOSE
END;
/

Anonymous PL block executed.
```

<a id="024479e162cd51ee"></a>
### Fetching Data With Explicit Cursors

- It fetches the row from the result set by executing [FETCH Statement](28-psm-language-element-references.md#913b57099867758a) after OPENing the explicit cursor.
- Fetch statement retrieves the current ROW of the result set and stores the ROW value in PSM variable or in record type variable, then moves the cursor to the next ROW.
- PSM [FETCH Statement](28-psm-language-element-references.md#913b57099867758a) does not throw an exception even when there is not a fetched ROW.
- When performing FETCH in [Basic LOOP Statement](28-psm-language-element-references.md#6e3a459559169fc8), then use %NOTFOUND property to detect the terminating condition.

<a id="4cbeaee0916105c6"></a>
#### Example of FETCHing Explicit Cursor

```
gSQL>
DECLARE
  CURSOR cur_month IS SELECT * FROM t_month;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN cur_month;
  
  LOOP
    FETCH cur_month INTO v_month_char, v_month_num;
    
    EXIT WHEN cur_month%NOTFOUND;
    
    DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );
  END LOOP;
    
  CLOSE cur_month;
END;
/

v_month_char : FEBRUARY , v_month_num : 2
v_month_char : APRIL , v_month_num : 4
v_month_char : JUNE , v_month_num : 6
v_month_char : AUGUST , v_month_num : 8
v_month_char : OCTOBER , v_month_num : 10
v_month_char : DECEMBER , v_month_num : 12
Anonymous PL block executed.
```

<a id="4cad9bef3d111216"></a>
### When Explicit Cursor Queries Need Column Aliases

If the query of an explicit cursor includes an expression, then the column always needs an alias name. The fetched result is stored in %ROWTYPE variable created by referring to the explicit cursor, and it can be used as a reference.

<a id="3d16e41db1f9a44c"></a>
#### Example of Using Alias in Query of Explicit Cursor

```
gSQL>
DECLARE
  CURSOR cur_month IS SELECT month_char, ( ' == ' || month_num ) as equal_month_num FROM t_month;
  var cur_month%rowtype;
BEGIN
  OPEN cur_month;
  
  LOOP
    FETCH cur_month INTO var; 
    
    EXIT WHEN cur_month%NOTFOUND;
    
    DBMS_OUTPUT.PUT_LINE( var.month_char || var.equal_month_num );
  END LOOP;

  CLOSE cur_month;
END;
/

FEBRUARY == 2
APRIL == 4
JUNE == 6
AUGUST == 8
OCTOBER == 10
DECEMBER == 12
Anonymous PL block executed.
```

<a id="598aada2ce46489a"></a>
### Explicit Cursors that Accept Parameters

It can declare and define the explicit cursor having the parameter.

- Parameter of the explicit cursor
    - It allows IN bind type only.
    - It can have DEFAULT value. It is not necessary to specify an argument.
    - It can be referenced in the query of the cursor.
    - If it is out of the explicit cursor's range, then it can not refer to the parameter of the explicit cursor.

<a id="767b915b64c92e83"></a>
#### Example of Using Explicit Cursor Parameter

```
gSQL>
DECLARE
  CURSOR cur_month( p1 IN INTEGER ) IS SELECT month_char, month_num FROM t_month WHERE month_num = p1;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN cur_month(4);
  
  FETCH cur_month INTO v_month_char, v_month_num;      
  DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );
gSQL> 
  CLOSE cur_month;
END;
/ 

v_month_char : APRIL , v_month_num : 4
Anonymous PL block executed.
```

- Example of Explicit Cursor Parameter's DEFAULT value

```
gSQL>
DECLARE
  CURSOR cur_month( p1 INTEGER DEFAULT 2 ) IS SELECT month_char, month_num FROM t_month WHERE month_num = p1;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN cur_month;                   ❶ It is allowed to omit the actual parameter.
   
  FETCH cur_month INTO v_month_char, v_month_num;      
  DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );

  CLOSE cur_month;
  
  OPEN cur_month(4);       ❷ It can be OPENed by specifying the actual parameter.
  
  FETCH cur_month INTO v_month_char, v_month_num;      
  DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );

  CLOSE cur_month;
END;
/

v_month_char : FEBRUARY , v_month_num : 2
v_month_char : APRIL , v_month_num : 4
Anonymous PL block executed.
```

<a id="eb75151012c2e398"></a>
### Explicit Cursor Attributes

The explicit cursor attribute describes the status of an explicit cursor. It can be used as an explicit cursor attribute by adding the attribute after the cursor name.

**Explicit cursor attributes**

<a id="c2885d1b83da39e2"></a>
| Attribute name | Return type | Description |
| --- | --- | --- |
| explicit_cursor_name%ISOPEN | BOOLEAN | If the explicit cursor is normally OPEN, then it is TRUE. Otherwise, it is FALSE. |
| explicit_cursor_name%FOUND | BOOLEAN | If the explicit cursor is not FETCHed yet, then it is NULL. If the data exists, then it is TRUE. If the data does not exist, then it is FALSE. If it is CLOSEd, then it is NULL. |
| explicit_cursor_name%NOTFOUND | BOOLEAN | It has an opposite value of explicit_cursor_name%FOUND. |
| explicit_cursor_name%ROWCOUNT | INTEGER | If the explicit cursor is not OPEN yet, then it is NULL. If it is normally OPEN, then it is 0. It is increased by 1 whenever executing FETCH, and it is NULL after CLOSE. |

<a id="2ad4e7925aa9e6af"></a>
#### Example of Using Explicit Cursor Parameter

- Before OPEN the explicit cursor

```
gSQL> 
DECLARE
  CURSOR cur_month IS SELECT month_char, month_num FROM t_month;
BEGIN
  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);
END;
/

cur_month%ISOPEN   = FALSE
cur_month%FOUND    = 
cur_month%NOTFOUND = 
cur_month%ROWCOUNT = 
Anonymous PL block executed.
```

- After OPEN the explicit cursor

```
gSQL> 
DECLARE
  CURSOR cur_month IS SELECT month_char, month_num FROM t_month;
BEGIN
  OPEN cur_month;
  
  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);

  CLOSE cur_month;
END;
/

cur_month%ISOPEN   = TRUE
cur_month%FOUND    = 
cur_month%NOTFOUND = 
cur_month%ROWCOUNT = 0
Anonymous PL block executed.
```

- After FETCH the explicit cursor

```
gSQL>
DECLARE
  CURSOR cur_month IS SELECT month_char, month_num FROM t_month LIMIT 3;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN cur_month;


  DBMS_OUTPUT.PUT_LINE( '[ First Fetch ]' );
  
  FETCH cur_month INTO v_month_char, v_month_num;      

  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);


  DBMS_OUTPUT.PUT_LINE( '[ Second Fetch ]' );

  FETCH cur_month INTO v_month_char, v_month_num;      

  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);


  DBMS_OUTPUT.PUT_LINE( '[ Last Fetch ]' );
  
  FETCH cur_month INTO v_month_char, v_month_num;
  
  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);


  DBMS_OUTPUT.PUT_LINE( '[ Over Last Fetch ]' );

  FETCH cur_month INTO v_month_char, v_month_num;            

  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);


  CLOSE cur_month;
END;
/

[ First Fetch ]
cur_month%ISOPEN   = TRUE
cur_month%FOUND    = TRUE
cur_month%NOTFOUND = FALSE
cur_month%ROWCOUNT = 1
[ Second Fetch ]
cur_month%ISOPEN   = TRUE
cur_month%FOUND    = TRUE
cur_month%NOTFOUND = FALSE
cur_month%ROWCOUNT = 2
[ Last Fetch ]
cur_month%ISOPEN   = TRUE
cur_month%FOUND    = TRUE
cur_month%NOTFOUND = FALSE
cur_month%ROWCOUNT = 3
[ Over Last Fetch ]
cur_month%ISOPEN   = TRUE
cur_month%FOUND    = FALSE
cur_month%NOTFOUND = TRUE
cur_month%ROWCOUNT = 3
Anonymous PL block executed.
```

- After CLOSE the explicit cursor

```
gSQL>
DECLARE
  CURSOR cur_month IS SELECT month_char, month_num FROM t_month;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN cur_month;
  
  FETCH cur_month INTO v_month_char, v_month_num;      

  CLOSE cur_month;

  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);
END;
/

cur_month%ISOPEN   = FALSE
cur_month%FOUND    = 
cur_month%NOTFOUND = 
cur_month%ROWCOUNT = 
Anonymous PL block executed.
```

<a id="5cc5cecfbf8fbd3b"></a>
## Cursor Variable

<a id="856c2d93b5ce403c"></a>
### Create Cursor Variables

Declare the variable by declaring predefined SYS_REFCURSOR type variable or by defining REF CURSOR TYPE so that the cursor variable is created. For more information, refer to [Cursor Variable Declaration](28-psm-language-element-references.md#32070bc40fcbdd69).

- REF CURSOR types are as follows.
    - Strong REF CURSOR type
        - If return_type is specified when defining REF CURSOR type, then it is the strong REF CURSOR type.
        - The strong REF CURSOR type variable can connect only the query whose query set type is as same as the defined return_type to the query of CURSOR VARIABLE.
        - Assigning the strong REF CURSOR type variable is available when the defined return_types are same.
    - Weak REF CURSOR type
        - If return_type is not specified when defining REF CURSOR type, then it is the weak REF CURSOR type.
        - SYS_REFCURSOR type is the weak REF CURSOR type as well.
        - It is more flexible than the strong REF CURSOR variable.
        - The weak ref cursor type variable can be assigned as the SYS_REFCURSOR type variable, and the SYS_REFCURSOR type variable can be assigned as the weak REF CURSOR type variable.

<a id="95440d8360b246f1"></a>
#### Example of Create Cursor Variable

- Definition of REF CURSOR type

```
gSQL>
DECLARE
  TYPE strong_refcur IS REF CURSOR RETURN t_month%ROWTYPE;   ❶ strong ref cursor type
  TYPE weak_refcur IS REF CURSOR;                            ❷ weak ref cursor type
BEGIN
  NULL;
END;
/

Anonymous PL block executed.
```

- Declaration of CURSOR VARIABLE

```
gSQL>
DECLARE
  TYPE strong_refcur IS REF CURSOR RETURN t_month%ROWTYPE;   ❶ strong ref cursor type
  TYPE weak_refcur IS REF CURSOR;                            ❷ weak ref cursor type

  v_sys_refcursor     SYS_REFCURSOR;                         ❸ weak ref cursor type variable
  v_strong_refcursor  strong_refcur;                         ❹ strong ref cursor type variable
  v_weak_refcursor    weak_refcur;                           ❺ weak ref cursor type variable
BEGIN
  NULL;
END;
/

Anonymous PL block executed.
```

<a id="80e0c0073ba79f0b"></a>
### Opening and Closing Cursor Variables

- It connects the cursor variable and SELECT statement or DML statement to perform by performing [OPEN FOR Statement](28-psm-language-element-references.md#0e5039afeb0434a1) after declaring the cursor variable.
- The cursor query may have the bind variable designating the specified value in using clause of OPEN FOR statement.
- If FOR UPDATE statement exists in cursor query, then it LOCKs the ROW in the result set. 
- When REOPENing the cursor variable, then it does not require CLOSE. The connection to the previous query is cut after REOPENing.
- Perform [CLOSE Statement](28-psm-language-element-references.md#01a3ed87cb2dd917) after finish using the cursor variable. 
- It does not allow accessing the query result of CLOSEd cursor variable or referring to the cursor variable attributes.

<a id="3ccc183a8044ce38"></a>
#### Example of Cursor Variable's OPEN and CLOSE

```
DECLARE
  v_refcur_month SYS_REFCURSOR;
BEGIN
  OPEN v_refcur_month FOR SELECT * FROM t_month;
  CLOSE v_refcur_month;
END;
/

Anonymous PL block executed.
```

- Cursor variable's OPEN with using clause.

```
gSQL>
DECLARE
  v_refcur_month SYS_REFCURSOR;
  var            INTEGER;
BEGIN
  var := 1;
  
  OPEN v_refcur_month FOR 'SELECT * FROM t_month WHERE month_num = :v' USING IN var;
END;
/

Anonymous PL block executed.
```

<a id="00dc0d9b779b1329"></a>
### Fetching Data with Cursor Variables

It can bring the row from the result set by executing [FETCH Statement](28-psm-language-element-references.md#913b57099867758a) after OPENing the cursor variable. The result returned by the cursor variable should be compatible with into clause.

<a id="d9221bd519aaf860"></a>
#### Example of FETCHing Cursor Variable

```
gSQL>
DECLARE  
  TYPE ref_month IS REF CURSOR RETURN t_month%ROWTYPE;
  v_refcur_month ref_month;
  
  v_month        t_month%ROWTYPE;  
BEGIN
  OPEN v_refcur_month FOR SELECT * FROM t_month;
  
  LOOP
    FETCH v_refcur_month INTO v_month;
    
    EXIT WHEN v_refcur_month%NOTFOUND;
    
    DBMS_OUTPUT.PUT_LINE( 'v_month.month_char : ' || v_month.month_char || ' , v_month.month_num : ' || v_month.month_num );
  END LOOP;
  
  CLOSE v_refcur_month;
END;
/

v_month.month_char : JANUARY , v_month.month_num : 1
v_month.month_char : MARCH , v_month.month_num : 3
v_month.month_char : MAY , v_month.month_num : 5
v_month.month_char : JULY , v_month.month_num : 7
v_month.month_char : SEPTEMBER , v_month.month_num : 9
v_month.month_char : NOVEMBER , v_month.month_num : 11
Anonymous PL block executed.
```

<a id="8170404e7ee4d8e5"></a>
### Assigning Value to Cursor Variables

The cursor variable can assign another cursor variable value or the host variable value. If the source cursor variable is OPEN and assigns the target cursor variable value, then both cursor variables indicate the same SQL. If the source cursor variable is not OPEN and assigns the target cursor variable value, then both cursor variables are not OPEN.

<a id="114b572a8ed05592"></a>
#### Example of Assigning Cursor Variable

```
gSQL>
DECLARE  
  source_refcur_month SYS_REFCURSOR;
  target_refcur_month SYS_REFCURSOR;
  v_month_char   VARCHAR(15);
  v_month_num    INTEGER;
BEGIN

  DBMS_OUTPUT.PUT_LINE( 'OPEN source_refcur_month' );
  
  OPEN source_refcur_month FOR SELECT * FROM t_month;

  DBMS_OUTPUT.PUT_LINE( 'source_refcur_month%ISOPEN : ' || source_refcur_month%ISOPEN );
  DBMS_OUTPUT.PUT_LINE( 'target_refcur_month%ISOPEN : ' || target_refcur_month%ISOPEN );


  DBMS_OUTPUT.PUT_LINE( 'Assign source_refcur_month to target_refcur_month' );
  
  target_refcur_month := source_refcur_month;

  DBMS_OUTPUT.PUT_LINE( 'source_refcur_month%ISOPEN : ' || source_refcur_month%ISOPEN );
  DBMS_OUTPUT.PUT_LINE( 'target_refcur_month%ISOPEN : ' || target_refcur_month%ISOPEN );


  DBMS_OUTPUT.PUT_LINE( 'CLOSE source_refcur_month' );  

  CLOSE source_refcur_month;

  DBMS_OUTPUT.PUT_LINE( 'source_refcur_month%ISOPEN : ' || source_refcur_month%ISOPEN );
  DBMS_OUTPUT.PUT_LINE( 'target_refcur_month%ISOPEN : ' || target_refcur_month%ISOPEN );
END;
/

OPEN source_refcur_month
source_refcur_month%ISOPEN : TRUE
target_refcur_month%ISOPEN : FALSE
Assign source_refcur_month to target_refcur_month
source_refcur_month%ISOPEN : TRUE
target_refcur_month%ISOPEN : TRUE
CLOSE source_refcur_month
source_refcur_month%ISOPEN : FALSE
target_refcur_month%ISOPEN : FALSE
Anonymous PL block executed.
```

<a id="c68372e7ae448d09"></a>
### Cursor Variable Attributes

Cursor variable attributes are as same as explicit cursor attributes, and it describes the status of the cursor variable. It can be used as a cursor variable attribute by adding the attribute after the cursor variable name. Attributes except for cursor_variable_name%ISOPEN attribute cause 'cursor is not defined' error before OPEN the cursor variable or after CLOSE the cursor variable.

**Cursor variable attributes**

<a id="77365ed0c5fce122"></a>
| Attribute name | Return type | Description |
| --- | --- | --- |
| cursor_variable_name%ISOPEN | BOOLEAN | If the cursor variable is OPEN, then it is TRUE. Otherwise, it is FALSE. |
| cursor_variable_name%FOUND | BOOLEAN | If the data exists after FETCH, then it is TRUE. If the data does not exist, then it is FALSE. |
| cursor_variable_name%NOTFOUND | BOOLEAN | It has an opposite value of cursor_variable_name%FOUND after FETCH. |
| cursor_variable_name%ROWCOUNT | INTEGER | If the cursor variable is OPEN, then it is 0, and it is increased by 1 whenever executing FETCH. |

<a id="d03c8362600f540c"></a>
#### Example of Using Cursor Variable Attributes

- Before OPEN the cursor variable

```
gSQL> 
DECLARE
  v_refcur_month SYS_REFCURSOR;
BEGIN
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);
END;
/

v_refcur_month%ISOPEN   = FALSE
ERR-2F000(17036): cursor is not defined : 
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
                       *
ERROR at line 5:
```

- After OPEN the cursor variable

```
gSQL> 
DECLARE
  v_refcur_month SYS_REFCURSOR;
BEGIN
  OPEN v_refcur_month FOR SELECT * FROM t_month;
  
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);

  CLOSE v_refcur_month;
END;
/

v_refcur_month%ISOPEN   = TRUE
v_refcur_month%FOUND    = 
v_refcur_month%NOTFOUND = 
v_refcur_month%ROWCOUNT = 0
Anonymous PL block executed.
```

- After FETCH the cursor variable

```
gSQL>
DECLARE
  v_refcur_month SYS_REFCURSOR;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN v_refcur_month FOR SELECT * FROM t_month LIMIT 3;


  DBMS_OUTPUT.PUT_LINE( '[ First Fetch ]' );
  
  FETCH v_refcur_month INTO v_month_char, v_month_num;      
 
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);


  DBMS_OUTPUT.PUT_LINE( '[ Second Fetch ]' );
  
  FETCH v_refcur_month INTO v_month_char, v_month_num;      
 
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);


  DBMS_OUTPUT.PUT_LINE( '[ Last Fetch ]' );
  
  FETCH v_refcur_month INTO v_month_char, v_month_num;      
 
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);


  DBMS_OUTPUT.PUT_LINE( '[ Over Last Fetch ]' );
  
  FETCH v_refcur_month INTO v_month_char, v_month_num;      
 
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);


  CLOSE v_refcur_month;
END;
/

[ First Fetch ]
v_refcur_month%ISOPEN   = TRUE
v_refcur_month%FOUND    = TRUE
v_refcur_month%NOTFOUND = FALSE
v_refcur_month%ROWCOUNT = 1
[ Second Fetch ]
v_refcur_month%ISOPEN   = TRUE
v_refcur_month%FOUND    = TRUE
v_refcur_month%NOTFOUND = FALSE
v_refcur_month%ROWCOUNT = 2
[ Last Fetch ]
v_refcur_month%ISOPEN   = TRUE
v_refcur_month%FOUND    = TRUE
v_refcur_month%NOTFOUND = FALSE
v_refcur_month%ROWCOUNT = 3
[ Over Last Fetch ]
v_refcur_month%ISOPEN   = TRUE
v_refcur_month%FOUND    = FALSE
v_refcur_month%NOTFOUND = TRUE
v_refcur_month%ROWCOUNT = 3
Anonymous PL block executed.
```

- After CLOSE the cursor variable

```
gSQL>
DECLARE
  v_refcur_month SYS_REFCURSOR;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN v_refcur_month FOR SELECT * FROM t_month LIMIT 3;

  FETCH v_refcur_month INTO v_month_char, v_month_num;      
 
  CLOSE v_refcur_month;
   
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);
END;
/

gSQL>
v_refcur_month%ISOPEN   = FALSE
ERR-2F000(17036): cursor is not defined : 
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
                       *
ERROR at line 13:
```

<a id="1c9178dd2b53b242"></a>
### Cursor Variable as Routine Parameter

Using the cursor variable as routine parameter is useful to transfer the query result. The parameter should be IN or IN OUT type to FETCH or CLOSE the cursor variable in the procedure or the function. The parameter should be OUT or IN OUT type to OPEN the cursor variable. Declaring the ref cursor type in the package is useful to transfer the query result of the cursor variable in each different routine.

<a id="c1877f6a1a14afe9"></a>
#### Example of Using Cursor Variable as Parameter

- Example of routine parameter

```
gSQL>
CREATE OR REPLACE PROCEDURE p_open( p_refcur_month OUT SYS_REFCURSOR ) AS 
BEGIN
  OPEN p_refcur_month FOR SELECT * FROM t_month;
END;
/

Procedure created.

gSQL>
CREATE OR REPLACE PROCEDURE p_fetch( p_refcur_month IN SYS_REFCURSOR ) AS 
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  FETCH p_refcur_month INTO v_month_char, v_month_num;
  DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );
END;
/

Procedure created.

gSQL>
DECLARE
  v_refcur_month SYS_REFCURSOR;
BEGIN
  p_open( v_refcur_month );
  DBMS_OUTPUT.PUT_LINE( 'v_refcur_month%ISOPEN : ' || v_refcur_month%ISOPEN );
  
  p_fetch( v_refcur_month );
  DBMS_OUTPUT.PUT_LINE( 'v_refcur_month%FOUND : ' || v_refcur_month%FOUND );
  
  CLOSE v_refcur_month;
  DBMS_OUTPUT.PUT_LINE( 'v_refcur_month%ISOPEN : ' || v_refcur_month%ISOPEN );
END;
/

v_refcur_month%ISOPEN : TRUE
v_month_char : JANUARY , v_month_num : 1
v_refcur_month%FOUND : TRUE
v_refcur_month%ISOPEN : FALSE
Anonymous PL block executed.
```

- Example of using package's ref cursor type

```
gSQL>
CREATE OR REPLACE PACKAGE pkg_refcur AS
  TYPE ref_month IS REF CURSOR RETURN t_month%ROWTYPE;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
  
  PROCEDURE p_open( p_refcur_month OUT ref_month, p_month IN INTEGER );
  PROCEDURE p_fetch( p_refcur_month IN ref_month );
  PROCEDURE p_close( p_refcur_month IN ref_month );
END;
/

Package created.

gSQL>
CREATE OR REPLACE PACKAGE BODY pkg_refcur AS
  PROCEDURE p_open( p_refcur_month OUT ref_month, p_month IN INTEGER ) AS
  BEGIN
    IF p_month = 1 THEN
      OPEN p_refcur_month FOR SELECT * FROM t_month WHERE month_num = 1;
    ELSIF p_month = 3 THEN
      OPEN p_refcur_month FOR SELECT * FROM t_month WHERE month_num = 3;
    ELSIF p_month = 5 THEN
      OPEN p_refcur_month FOR SELECT * FROM t_month WHERE month_num = 5;    
    ELSIF p_month = 7 THEN    
      OPEN p_refcur_month FOR SELECT * FROM t_month WHERE month_num = 7;
    ELSIF p_month = 9 THEN        
      OPEN p_refcur_month FOR SELECT * FROM t_month WHERE month_num = 9;    
    ELSIF p_month = 11 THEN
      OPEN p_refcur_month FOR SELECT * FROM t_month WHERE month_num = 11;    
    ELSE
      DBMS_OUTPUT.PUT_LINE( 'NO ODD MONTH' );
    END IF;
    
    DBMS_OUTPUT.PUT_LINE( 'p_refcur_month%ISOPEN : ' || p_refcur_month%ISOPEN );
  END;
  
  PROCEDURE p_fetch( p_refcur_month IN ref_month ) AS
  BEGIN
    FETCH p_refcur_month INTO v_month_char, v_month_num;
    DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );
  END;
  
  PROCEDURE p_close( p_refcur_month IN ref_month ) AS
  BEGIN
    CLOSE p_refcur_month;
    DBMS_OUTPUT.PUT_LINE( 'p_refcur_month%ISOPEN : ' || p_refcur_month%ISOPEN );    
  END;
END;
/

Package created.

gSQL>
DECLARE
  v_pkg_refcur_month pkg_refcur.ref_month;
BEGIN
  pkg_refcur.p_open( v_pkg_refcur_month, 5 );
  pkg_refcur.p_fetch( v_pkg_refcur_month );
  pkg_refcur.p_close( v_pkg_refcur_month );  
END;
/

p_refcur_month%ISOPEN : TRUE
v_month_char : MAY , v_month_num : 5
p_refcur_month%ISOPEN : FALSE
Anonymous PL block executed.
```

<a id="378e1c7463ffd304"></a>
### Cursor Variable as Host Variable

The cursor variable can be declared as the host variable. The host cursor variable is useful to transfer the query result between the server and the client, and it can share the same query result sets between the server and the client.

Declare REF CURSOR type host variable and transfer it to the server to use the cursor variable as the host variable. Calling the cursor variable between the server and the client is not limited. Declare the cursor variable in the client and fetch it after OPENing in the server, then it can be closed after it is FETCHed in the client.

<a id="d7c13dddd57553b0"></a>
#### Example of Host Cursor Variable

```
gSQL>
\var host_refcur_month REFCURSOR

gSQL>
BEGIN
  OPEN :host_refcur_month FOR SELECT * FROM t_month;
END;
/

Anonymous PL block executed.

gSQL>
DECLARE
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  FETCH :host_refcur_month INTO v_month_char, v_month_num;
  DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );  
END;
/

v_month_char : JANUARY , v_month_num : 1
Anonymous PL block executed.

gSQL>
BEGIN
  CLOSE :host_refcur_month;
END;
/

Anonymous PL block executed.
```

---

[← 23. PSM Control Statements](23-psm-control-statements.md) · [Table of contents](../README.md) · [25. Using PSM Subprograms →](25-using-psm-subprograms.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
