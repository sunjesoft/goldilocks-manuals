<a id="81bac6153d97c3d6"></a>

# 25. Using PSM Subprograms

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/81bac6153d97c3d6)  
> Tag: `21c.1_35_tag`

[← 24. PSM Cursor Statements](24-psm-cursor-statements.md) · [Table of contents](../README.md) · [26. Using SQLs in PSM →](26-using-sqls-in-psm.md)

<a id="8ed5d6d4e664e37d"></a>
## Anonymous PL Block

An anonymous PL block is an SQL statement for a   one - time execution of a PSM statement instead of storing a PSM statement in the database. An anonymous PL block is a one of a regular SQL provided by GOLDILOCKS, so it is used in the same way as other SQL s in ODBC, JDBC and precompiler which are provided by GOLDILOCKS. A syntax is as same as a syntax of a general basic block   
For more information, refer to [Block (BEGIN .. END)](28-psm-language-element-references.md#ac661ad806550306).

```
<<Label>> ❶ (optional)
DECLARE   ❷ (optional)
❸ declare items (variables, cursors, types, ...) (optional)
BEGIN     ❹ (required)
❺ PSM statements to execute (required)
EXCEPTION ❻ Exception Handling Part (optional)
END;
```

Refer to the following instructions when using an anonymous PL block.

<a id="8d901aa6fd3688e3"></a>
| Interface | Instructions for use |
| --- | --- |
| in common | A bind parameter can be used unlike a schema-level procedure/ function.  It also supports a prepare-execute method. |
| ODBC | It is used completely same as a general SQL. |
| JDBC | A CallableStatement class should be used if it has a bind parameter with IN-OUT or OUT attribute. (Refer to [CallableStatement](../part-05-developer-manual/32-jdbc.md#3e73467a821afdba).) |
| Precompiler (gpec) | N/A |
| Interactive command tool (gsql) | It should notify the end of the statement by entering '/'&lt;Enter&gt; after inputting an anonymous PL block. |

<a id="eeba21f481580979"></a>
## Nested Procedure

A nested procedure is a procedure type subprogram declared within a specific PL block. A nested procedure has a scope which can be referenced only on a declared PL block and its subordinates.  
For more information, refer to [Procedure Declaration and Definition](28-psm-language-element-references.md#809e9ea8094fa81a).

```
DECLARE
  PROCEDURE PROC1( A1 INTEGER )  ❶ Define Nested Procedure
    IS   
    BEGIN
      DBMS_OUTPUT.PUT_LINE( 'A1 = ' || A1 );
    END; 
BEGIN
  PROC1( 100 );  ❷ Call Nested Procedure
END;
/
```

The followings are items available within a nested subprogram.

- An argument variable of a nested subprogram
- A PL block in which a nested subprogram is defined, and variables and various items (type, cursor,...) defined in its superordinate scope.
- A bind parameter when it is an anonymous PL block. (e.g. '?', ':V1')

A nested procedure supports a forward declaration, so it can separately specify a declare statement and a define statement. By using this, a logic of cross call between two nested procedures can be implemented.

```
gSQL> DECLARE

  PROCEDURE PROC1( A1 INTEGER );  ❶ declare proc1

  PROCEDURE PROC2( A1 INTEGER )   ❷ define  proc2
  IS
  BEGIN
    IF A1 > 0 THEN
      DBMS_OUTPUT.PUT_LINE( '(proc2)A1 = ' || A1 );
      PROC1( A1 -1 );  ❸ call proc1
    END IF;
  END; 

  PROCEDURE PROC1( A1 INTEGER )   ❹ define  proc1
  IS
  BEGIN
    IF A1 > 0 THEN
      DBMS_OUTPUT.PUT_LINE( '(proc1)A1 = ' || A1 );
      PROC2( A1 -1 );  ❺ call proc2
    END IF;
  END; 

BEGIN
  PROC1(5); ❻ call proc1
END;
/
 
(proc1)A1 = 5
(proc2)A1 = 4
(proc1)A1 = 3
(proc2)A1 = 2
(proc1)A1 = 1

Anonymous PL block executed.
```

GOLDILOCKS PSM limits the maximum subordinate statement depths to 50 to prevent the infinite cross referencing. If it is exceeded, then the following error occurs. (It is also applied same to a nested function, schema-level procedure/ function.)

```
gSQL> DECLARE
  PROCEDURE PROC1( A1 INTEGER );  ❶ declare proc1
  PROCEDURE PROC2( A1 INTEGER )   ❷ define  proc2
  IS
  BEGIN
    DBMS_OUTPUT.PUT_LINE( 'A1 = ' || A1 );
    PROC1( A1 -1 );
  END;
  PROCEDURE PROC1( A1 INTEGER )   ❸ define  proc1
  IS
  BEGIN
    DBMS_OUTPUT.PUT_LINE( 'A1 = ' || A1 );
    PROC2( A1 -1 );
  END;
BEGIN
  PROC1(100);
END;
/

ERR-42000(16411): maximum number of recursive SQL levels (50) exceeded.
```

<a id="2a77664ba16a9a8a"></a>
## Nested Function

A nested function is as same as a nested procedure, but it is a subprogram in function form.   
For more information, refer to [Function Declaration and Definition](28-psm-language-element-references.md#c51a4fc9ada0cf91).

```
gSQL> DECLARE
  V1 INTEGER := 0;
  FUNCTION FUNC1( A1 INTEGER )
    RETURN INTEGER
    IS   
    BEGIN
      RETURN A1 * 10;
    END; 
BEGIN
  V1 := FUNC1( 10 );
  DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
END;
/

V1 = 100

Anonymous PL block executed.
```

A nested function can be used in all PSM expressions within a visible scope, but is can not be used in an SQL statement.

```
gSQL> DECLARE
  V1 INTEGER := 0;
  FUNCTION FUNC1( A1 INTEGER )
    RETURN INTEGER
    IS
    BEGIN
      RETURN A1 * 10;
    END;
BEGIN
  SELECT FUNC1(10) INTO V1 FROM DUAL;
  DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (10:3): ERR-HY000(17079): a nested function not allowed in executing SQL
```

<a id="612eb041d9316761"></a>
## Schema-level Procedure

A schema-level subprogram is an SQL object which has a name and is stored in a database. A schema-level procedure is a schema-level subprogram in procedure form.

<a id="9a6249863b0f43cb"></a>
### Creating Schema-level Procedure

A schema-level procedure is created as follows. A precision and a scale value should be specified if in need.  
For more information, refer to [CREATE PROCEDURE](29-psm-sql-references.md#c4195b7175b4b1f4).

```
CREATE OR REPLACE PROCEDURE PROC1( A1 INTEGER, A2 INTEGER )
IS  
  V1 INTEGER;
BEGIN
  SELECT COUNT(*)
    INTO V1
    FROM T1
    WHERE T1.I1 >= A1 AND T1.I1 <= A2; 
  DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
END;
/
```

The information about a created schema-level procedure can be found with a INFORMATION_SCHEMA.ROUTINES table.   
For more information, refer to [ROUTINES](../part-02-administration-manual/9-database-information.md#6710cbc9cccd6f34).

```
gSQL> SELECT SPECIFIC_NAME, ROUTINE_DEFINITION
  FROM  INFORMATION_SCHEMA.ROUTINES
  WHERE SPECIFIC_NAME = 'PROC1';

SPECIFIC_NAME ROUTINE_DEFINITION                                   
------------- -----------------------------------------------------
PROC1         PROCEDURE "PUBLIC"."PROC1" ( A1 INTEGER, A2 INTEGER )
              IS                                                   
                V1 INTEGER;                                        
              BEGIN                                                
                SELECT COUNT(*)                                    
                  INTO V1                                          
                  FROM T1                                          
                  WHERE T1.I1 >= A1 AND T1.I1 <= A2;               
                DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );             
              END;                                                 
                                                                   

1 row selected.
```

The information about an argument can be found with a INFORMATION_SCHEMA.PARAMETERS table.  
For more information, refer to [PARAMETERS](../part-02-administration-manual/9-database-information.md#0082e65aaa538188).

```
gSQL> SELECT P.PARAMETER_NAME, P.ORDINAL_POSITION
  FROM  INFORMATION_SCHEMA.ROUTINES     R,
        INFORMATION_SCHEMA.PARAMETERS   P
  WHERE R.SPECIFIC_NAME = 'PROC1'
    AND R.SPECIFIC_SCHEMA = P.SPECIFIC_SCHEMA
    AND R.SPECIFIC_NAME = P.SPECIFIC_NAME
  ORDER BY P.ORDINAL_POSITION;

PARAMETER_NAME ORDINAL_POSITION
-------------- ----------------
A1                            1
A2                            2

2 rows selected.
```

<a id="6297aa365f3abec0"></a>
### Using Schema-level Procedure

A schema-level procedure is used by an inner statement of other PSM or by a CALL statement.   
Other PSM statements call a schema-level procedure in the same form of a nested procedure.

```
gSQL> BEGIN
  PROC1( 2, 4 );  ❶ Call schema-level procedure
END;
/

V1 = 3

Anonymous PL block executed.
```

A CALL statement which is an SQL executing the given PSM is executed as follows.   
For more information, refer to [CALL Statement](29-psm-sql-references.md#bd610f7f021862b8).

```
gSQL> CALL PROC1( 2, 4 );
V1 = 3

Procedure Call complete.
```

It supports the following syntax for a procedure to support a procedure call escape sequence used in ODBC or JDBC.

```
{ CALL procedure_name( param1, param2, ... ) }
```

A syntax of a procedure call escape sequence is used like as a general SQL.

```
gSQL> { CALL PROC1(2, 4) };
V1 = 3

Procedure Call complete.
```

gsql which is an interactive command tool of GOLDILOCKS does not support performing a procedure through `\`EXEC which is the tool's own command.

The following options about a privilege of when executing a schema-level procedure can be specified. If a user except for a definer performs an SQL within PSM according to these options, it may refer to a table with the same name in different schemas according to the definition of that user's schema-path. (A name of the object used when declaring an item (e.g. T1%ROWTYPE) is always interpreted as a definer.)

- AUTHID DEFINER (default): The user is altered to the user created that procedure, then it is performed.
- AUTHID CURRENT_USER: The user is not altered, and it is performed by the current user.

```
CREATE OR REPLACE PROCEDURE "PROC1"( A1 INTEGER, A2 INTEGER )
AUTHID CURRENT_USER
IS
  V1 INTEGER;
BEGIN
  SELECT COUNT(*)
    INTO V1
    FROM T1
    WHERE T1.I1 >= A1 AND T1.I1 <= A2;
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
END;
/
```

<a id="77c064f5979eea11"></a>
### Dropping Schema-level Procedure

A schema-level procedure is dropped by the following DROP PROCEDURE statement.  
For more information, refer to [DROP PROCEDURE](29-psm-sql-references.md#3b6f829e3aa92686).

```
DROP PROCEDURE PROC1;
```

It also supports IF EXISTS statement like as other DROP statements of GOLDILOCKS.

```
DROP PROCEDURE IF EXISTS PROC1;
```

<a id="44d9a3924837b03e"></a>
### Recompiling Schema-level Procedure

If an object referenced inside of a schema-level subprogram is altered, then it may affects the corresponding subprogram and should create the execution plan again.

<a id="94afa97985331313"></a>
#### Referenced Object in a Declarative Part or an Argument

If the used object is altered when defining various items in a declarative part or an argument type, then the procedure plan is automatically recompiled.

- An object used in %TYPE, %ROWTYPE
- An object used in an explicit cursor definition statement

If the corresponding procedure is performed for the first time after an object is altered, then the plan is automatically recreated according to the following order.

1. Bring the plan of the corresponding procedure from a plan cache.
2. Search for objects which were altered during validating an object list of that plan.
3. Discard the current plan, and create a new plan from a procedure definition statement stored in a dictionary.
4. Register a newly created plan on a plan cache. 
5. Execute the plan.

<a id="eea0e20e1ff0c6fe"></a>
#### Referenced Object in an SQL of the Body

An SQL plan used in the body is not stored in a procedure plan, and only the SQL text is stored. When executing a procedure, it creates a plan by compiling the corresponding SQL statement in real time, then executes it. Therefore, an SQL object used within a body does not affect the procedure plan itself.

However, if an object is altered, the number or type of binds which are the existing interfaces of a procedure may be altered, or columns may be dropped. Therefore, an error may occur when executing it if the procedure is not appropriately altered.

<a id="2bf712eaa1bb9303"></a>
## Schema-level Function

A schema-level function is a schema-level subprogram in function form, which is used within an expression.

<a id="d3861e70f564a57d"></a>
### Creating Schema-level Function

A schema-level function is created as follows. A precision and a scale value of an argument type should be specified if in need.  
For more information, refer to [CREATE FUNCTION](29-psm-sql-references.md#7acaf940b774cb75).

```
gSQL> CREATE OR REPLACE FUNCTION FUNC1( A1 INTEGER, A2 INTEGER )
RETURN INTEGER
IS
  V1 INTEGER;
BEGIN
  SELECT COUNT(*)
    INTO V1
    FROM T1
    WHERE T1.I1 >= A1 AND T1.I1 <= A2;
  RETURN V1;
END; 
/

Function created.
```

Like as a procedure, a created schema-level function is found throughINFORMATION_SCHEMA.ROUTINES and INFORMATION_SCHEMA.PARAMETERS table.

<a id="be8c5a253b4f5746"></a>
### Using Schema-level Function

A schema-level function can be used in all expressions in which a general SQL or an SQL object within PSM can be used.

```
gSQL> SELECT FUNC1( 2, 4 ) FROM DUAL;

FUNC1( 2, 4 )
-------------
            3

1 row selected.
```

It is used as follows within PSM.

```
gSQL> DECLARE
  V1 INTEGER;
BEGIN
  V1 := FUNC1( 2, 4 );
  DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
END;
/

V1 = 3

Anonymous PL block executed.
```

It can be performed by using CALL statement as follows.   
For more information, refer to [CALL Statement](29-psm-sql-references.md#bd610f7f021862b8).

```
gSQL> \var V1 INTEGER
gSQL> CALL FUNC1( 2, 4 ) INTO :V1;

Procedure Call complete.

gSQL> \print V1

V1
--
 3
```

Like as a schema-level procedure, a procedure call escape sequence statement is also supported.

```
{ ? = CALL function_name( param1, param2, ... ) }
```

```
gSQL> { :V1 = CALL FUNC1( 2, 4 ) };

Procedure Call complete.

gSQL> \print V1

V1
--
 3
```

<a id="feb412524610f1f5"></a>
### Dropping Schema-level Function

A schema-level function is dropped by the following DROP FUNCTION statement.  
For more information, refer to [DROP FUNCTION](29-psm-sql-references.md#b68d9e7f71d37f62).

```
gSQL> DROP FUNCTION FUNC1;

Function dropped.
```

<a id="dbf8118b3a1e60e0"></a>
## Built-in Procedures

GOLDILOCKS PSM provides the following built-in procedures to debug or process the exception when materializing the procedure and the function.

**Built-in procedures**

<a id="5b5847781e933a24"></a>
| Procedure | Description |
| --- | --- |
| DBMS_OUTPUT.ENABLE( buffer_size IN NATIVE_INTEGER := 20000 ) | It activates a message logging feature to the given buffer size. If the buffer size is not given it is set to 20000 bytes by default. If the feature is already activatedm then it discards all messages and creates a new buffer. |
| DBMS_OUTPUT.DISABLE | It deactivates a message logging feature. All messages previously logged are discarded. |
| DBMS_OUTPUT.SET_LOG( file_path IN VARCHAR(4000) ) | It simultaneously outputs on the file in a given path when logging a message. If the given path is a relative path (its first letter is not /), then it searches for a target file below a directory corresponding to &lt;SYSTEM_LOGGER_DIR&gt; property.  Specify the permission as follows. * CALL DBMS_OUTPUT.SET_LOG( 'a.txt' , 640 ) |
| DBMS_OUTPUT.PUT_LINE( item IN VARCHAR(4000) ) | It stores a message created with a given expression including the new line character on a buffer. |
| DBMS_OUTPUT.PUT( item IN VARCHAR(4000) ) | It stores a message created with a given expression on a buffer. |
| DBMS_OUTPUT.NEW_LINE | It stores the new line character on a buffer. |
| DBMS_OUTPUT.GET_LINE( line OUT VARCHAR(4000), status OUT NATIVE_INTEGER ) | It returns the oldest single message line which is not read among messages stored on a buffer. If there is a message, a status returns 0, if there is not any message it returns 1. |
| DBMS_STANDARD.RAISE_APPLICATION_ERROR( error_code IN NATIVE_INTEGER, error_message IN VARCHAR(4000), stack_flag IN BOOLEAN := FALSE ) | It generates an arbitrary user exception. and error_code should be the value between -20000 and -20999. If it is TRUE, the last stack_flag argument stacks a given error on the existing errors. If it is FALSE, the corresponding error replaces all errors. (It can be omitted, and the default is FALSE when it is omitted.) |

```
gSQL> DECLARE
V1 VARCHAR(1024);
V2 INTEGER;
BEGIN
  DBMS_OUTPUT.ENABLE(2000);
  DBMS_OUTPUT.PUT_LINE('TEST MSG');
  DBMS_OUTPUT.GET_LINE( V1, V2);
  DBMS_OUTPUT.PUT_LINE('V1 = ' || v1);
  DBMS_OUTPUT.PUT_LINE('V2 = ' || v2);
END;
/

V1 = TEST MSG

V2 = 0

Anonymous PL block executed.
```

A message logging feature is managed per each section, and gsql (an interactive command tool of GOLDILOCKS) can turn on or off the message logging feature with a serveroutput option. If any content remains in a message buffer after performing PSM, all are automatically output.

```
gSQL> \set serveroutput on
gSQL> \var msg VARCHAR(4000)
gSQL> \var status NATIVE_INTEGER
gSQL> CALL DBMS_OUTPUT.PUT_LINE( 'aaa' );
aaa

Procedure Call complete.

gSQL> CALL DBMS_OUTPUT.PUT_LINE( 'bbb' );
bbb

Procedure Call complete.

gSQL> CALL DBMS_OUTPUT.GET_LINE( :msg, :status );

Procedure Call complete.

gSQL> \print msg

MSG 
----
null

gSQL> \print status

STATUS
------
     1
```

---

[← 24. PSM Cursor Statements](24-psm-cursor-statements.md) · [Table of contents](../README.md) · [26. Using SQLs in PSM →](26-using-sqls-in-psm.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
