<a id="31048831dcb5b296"></a>

# 25. Using PSM Subprograms

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/31048831dcb5b296)  
> Tag: `26c.1_0_tag`

[← 24. PSM Cursor Statements](24-psm-cursor-statements.md) · [Table of contents](../README.md) · [26. Using SQLs in PSM →](26-using-sqls-in-psm.md)

<a id="c79ad47867a11e15"></a>
## Anonymous PL Block

An anonymous PL block is an SQL statement for a   one - time execution of a PSM statement instead of storing a PSM statement in the database. An anonymous PL block is a one of a regular SQL provided by GOLDILOCKS, so it is used in the same way as other SQL s in ODBC, JDBC and precompiler which are provided by GOLDILOCKS. A syntax is the same as a syntax of a general basic block   
For more information, refer to [Block (BEGIN .. END)](30-psm-language-element-references.md#acfcdb439eaed2a5).

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

<a id="edab2bfd7edc729c"></a>
| Interface | Instructions for use |
| --- | --- |
| in common | A bind parameter can be used unlike a schema-level procedure/ function.  It also supports a prepare-execute method. |
| ODBC | It is used completely same as a general SQL. |
| JDBC | A CallableStatement class should be used if it has a bind parameter with IN-OUT or OUT attribute. (Refer to [CallableStatement](../part-05-developer-manual/35-jdbc.md#a106ab9d7872dfc0).) |
| Precompiler (gpec) | N/A |
| Interactive command tool (gsql) | It should notify the end of the statement by entering '/'&lt;Enter&gt; after inputting an anonymous PL block. |

<a id="eca431720a5e4890"></a>
## Nested Procedure

A nested procedure is a procedure type subprogram declared within a specific PL block. A nested procedure has a scope which can be referenced only on a declared PL block and its subordinates.  
For more information, refer to [Procedure Declaration and Definition](30-psm-language-element-references.md#6cbc67f75778afa6).

The nested procedure can be declared with &lt;SQL body&gt; or &lt;external body&gt;.  
&lt;SQL body&gt; declares a PL Item, and it can declare &lt;pl statement&gt; which can refer to it.  
&lt;external body&gt; specifies the information to execute the external routine, and it can execute the external routine.

```
DECLARE
  PROCEDURE PROC1( A1 INTEGER )  ❶ Define nested procedure
  IS
    VAR1 INTEGER;                ❷ <SQL Body>
  BEGIN                        
    VAR1 := A1;
    DBMS_OUTPUT.PUT_LINE( 'VAR1 = ' || VAR1 );
  END; 
BEGIN
  PROC1( 100 );                  ❸ Call nested procedure
END;
/
```

```
DECLARE
  var1 NATIVE_INTEGER;
   
  PROCEDURE proc1( p1 NATIVE_INTEGER,             ❶ Define nested procedure
                   p2 NATIVE_INTEGER,
                   p3 OUT NATIVE_INTEGER ) AS
  LANGUAGE C                                      ❷ <external body>
  LIBRARY lib NAME "add"
  PARAMETERS( p1 INT , 
              p2 INT , 
              p3 INT );
BEGIN
  proc1( 5 , 3 , var1 );                          ❸ Call nested procedure
  DBMS_OUTPUT.PUT_LINE ( var1 );
END;
/
```

The following are items available within &lt;SQL body&gt; of a nested subprogram.

- An argument variable of a nested subprogram
- A PL block in which a nested subprogram is defined, and variables and various items (type, cursor,...) defined in its superordinate scope.
- A bind parameter when it is an anonymous PL block. (e.g. '?', ':V1')

A nested procedure which is &lt;external body&gt; can call an external routine.

```
#include <stdio.h>

void add( int a , int b , int * c)
{
    *c = a + b;
}
```

```
gSQL>
create library lib as 'add.so';
/

Library created.

gSQL>
DECLARE
  var1 NATIVE_INTEGER;
   
  PROCEDURE proc1( p1 NATIVE_INTEGER, 
                   p2 NATIVE_INTEGER,
                   p3 OUT NATIVE_INTEGER ) AS
  LANGUAGE C
  LIBRARY lib NAME "add"
  PARAMETERS( p1 INT , 
              p2 INT , 
              p3 INT );
BEGIN
  proc1( 5 , 3 , var1 );
  DBMS_OUTPUT.PUT_LINE ( var1 );
END;
/

8
Anonymous PL block executed.
```

A nested procedure supports a forward declaration, so it can separately specify a declare statement and a define statement.

The following is an example of implementing the logic which two nested procedures call each other by describing the declare statement and the define statement separately.

```
gSQL>
DECLARE
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
  PROC1(5);  ❻ call proc1
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

The following is an example of implementing the logic which calls the &lt;external body&gt; nested procedure from the &lt;SQL body&gt; nested procedure by describing the declare statement and the define statement separately.

```
gSQL>
DECLARE
  PROCEDURE proc1( p1 NATIVE_INTEGER,
                   p2 NATIVE_INTEGER,
                   p3 OUT NATIVE_INTEGER );          ❶ declare proc1
 
  PROCEDURE proc2( p1 NATIVE_INTEGER ) AS            ❷ define  proc2
    var1 NATIVE_INTEGER;
  BEGIN
    PROC1( p1 , p1 - 1 , var1 );                     ❸ call proc1
    DBMS_OUTPUT.PUT_LINE( 'proc2 :: p1 = ' || p1 ||
                          ' , var1 = ' || var1 );
  END; 
       
  PROCEDURE proc1( p1 NATIVE_INTEGER,                ❹ define  proc1
                   p2 NATIVE_INTEGER,
                   p3 OUT NATIVE_INTEGER ) AS
  LANGUAGE C
  LIBRARY lib NAME "add"
  PARAMETERS( p1 INT , 
              p2 INT , 
              p3 INT );
BEGIN
  PROC2(5);                                          ❺ call proc2
END;
/

proc2 :: p1 = 5 , var1 = 9
Anonymous PL block executed.
```

<a id="3088877f9ea253dd"></a>
## Nested Function

A nested function is the same as a nested procedure, but it is a subprogram in function form.   
For more information, refer to [Function Declaration and Definition](30-psm-language-element-references.md#515fb4aa2f801dc3).

- Nested function which is &lt;SQL body&gt;

```
gSQL> 
DECLARE
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

- Nested function which is &lt;external body&gt;

```
#include <stdio.h>

int add( int a , int b )
{
    return a + b;
}
```

```
gSQL>
create library lib as 'add.so';
/

Library created.

gSQL>
DECLARE
  var1 NATIVE_INTEGER;
   
  FUNCTION func1( p1 NATIVE_INTEGER,
                  p2 NATIVE_INTEGER )
    RETURN NATIVE_INTEGER AS
  LANGUAGE C
  LIBRARY lib NAME "add"
  PARAMETERS( p1 INT , 
              p2 INT , 
              RETURN INT );
BEGIN
  var1 := func1( 2 , 8 );
  DBMS_OUTPUT.PUT_LINE ( var1 );
END;
/

10
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

<a id="9d4fc646b05043cc"></a>
## Schema-level Procedure

A schema-level subprogram is an SQL object which has a name and is stored in a database. A schema-level procedure is a schema-level subprogram in procedure form.

<a id="821e13e1307c29dc"></a>
### Creating Schema-level Procedure

A schema-level procedure is created as follows. A precision and a scale value should be specified if in need.  
The format of &lt;routine body&gt; in the schema-level procedure is &lt;SQL body&gt; or &lt;external body&gt;.  
For more information, refer to [CREATE PROCEDURE](31-psm-sql-references.md#d439613cbc283235).

- Schema-level procedure which is &lt;SQL body&gt;

```
gSQL>
CREATE OR REPLACE PROCEDURE sqlbody_proc( a1 INTEGER, a2 INTEGER )
IS  
  v1 INTEGER;
BEGIN
  SELECT COUNT(*)
    INTO v1
    FROM t1
    WHERE t1.i1 >= a1 AND t1.i1 <= a2; 

  DBMS_OUTPUT.PUT_LINE( 'v1 = ' || v1 );
END;
/

Procedure created.
```

- Schema-level procedure which is &lt;external body&gt;

```
gSQL>
CREATE OR REPLACE PROCEDURE externalbody_proc( p1 NATIVE_INTEGER,
                                               p2 NATIVE_INTEGER,
                                               p3 OUT NATIVE_INTEGER ) AS
LANGUAGE C
LIBRARY lib NAME "add"
PARAMETERS( p1 INT , 
            p2 INT , 
            p3 INT );
/

Procedure created.
```

The information about a created schema-level procedure can be found with a INFORMATION_SCHEMA.ROUTINES table.   
For more information, refer to [ROUTINES](../part-02-administration-manual/9-database-information.md#3b7848bde8b71a0c).

```
gSQL>
SELECT specific_name,
       routine_body,
       routine_definition
  FROM information_schema.routines
 WHERE specific_name IN ( 'SQLBODY_PROC' , 'EXTERNALBODY_PROC' );

SPECIFIC_NAME     ROUTINE_BODY
----------------- ------------
ROUTINE_DEFINITION                                                       
-------------------------------------------------------------------------
EXTERNALBODY_PROC EXTERNAL    
PROCEDURE "PUBLIC"."EXTERNALBODY_PROC" ( p1 NATIVE_INTEGER,              
                                               p2 NATIVE_INTEGER,        
                                               p3 OUT NATIVE_INTEGER ) AS
LANGUAGE C                                                               
LIBRARY lib NAME "add"                                                   
PARAMETERS( p1 INT ,                                                     
            p2 INT ,                                                     
            p3 INT );                                                    
                                                                         
SQLBODY_PROC      SQL         
PROCEDURE "PUBLIC"."SQLBODY_PROC" ( a1 INTEGER, a2 INTEGER )             
IS                                                                       
  v1 INTEGER;                                                            
BEGIN                                                                    
  SELECT COUNT(*)                                                        
    INTO v1                                                              
    FROM t1                                                              
    WHERE t1.i1 >= a1 AND t1.i1 <= a2;                                   
                                                                         
  DBMS_OUTPUT.PUT_LINE( 'v1 = ' || v1 );                                 
END;                                                                     
                                                                         

2 rows selected.
```

The information about an external routine can be found in a INFORMATION_SCHEMA.ROUTINES table.

```
gSQL> 
SELECT specific_name,
       external_name,
       external_c_function,
       external_language,
       library_schema,
       library_name
  FROM information_schema.routines
 WHERE specific_name = 'EXTERNALBODY_PROC';

SPECIFIC_NAME     EXTERNAL_NAME EXTERNAL_C_FUNCTION                   
----------------- ------------- --------------------------------------
EXTERNAL_LANGUAGE LIBRARY_SCHEMA LIBRARY_NAME
----------------- -------------- ------------
EXTERNALBODY_PROC add           void add( int P1 , int P2 , int * P3 )
C                 PUBLIC         LIB         

1 row selected.
```

The information about an argument can be found with a INFORMATION_SCHEMA.PARAMETERS table.  
For more information, refer to [PARAMETERS](../part-02-administration-manual/9-database-information.md#b342c61d7fea348a).

```
gSQL> 
SELECT r.specific_name,
       p.parameter_name,
       p.ordinal_position
  FROM information_schema.routines r,
       information_schema.parameters p
 WHERE r.specific_name IN ( 'SQLBODY_PROC' , 'EXTERNALBODY_PROC' )
   AND r.specific_schema = p.specific_schema
   AND r.specific_name = p.specific_name
 ORDER BY p.parameter_name,
          p.ordinal_position;

SPECIFIC_NAME     PARAMETER_NAME ORDINAL_POSITION
----------------- -------------- ----------------
SQLBODY_PROC      A1                            1
SQLBODY_PROC      A2                            2
EXTERNALBODY_PROC P1                            1
EXTERNALBODY_PROC P2                            2
EXTERNALBODY_PROC P3                            3

5 rows selected.
```

<a id="7fa38de1d87c7888"></a>
### Using Schema-level Procedure

A schema-level procedure is used by an inner statement of other PSM or by a CALL statement.   
Other PSM statements call a schema-level procedure in the same form of a nested procedure.

```
gSQL>
BEGIN
  sqlbody_proc( 2 , 4 );     ❶ call schema-level procedure with <SQL body>
END;
/

v1 = 3
Anonymous PL block executed.
```

```
gSQL>
DECLARE
  var1 NATIVE_INTEGER;
BEGIN
  externalbody_proc( 2 , 4 , var1 ); 
                        ❶ call schema-level procedure with <external body>
  DBMS_OUTPUT.PUT_LINE( 'var1 = ' || var1 );
END;
/

var1 = 6
Anonymous PL block executed.
```

A CALL statement which is an SQL executing the given PSM is executed as follows.   
For more information, refer to [CALL Statement](31-psm-sql-references.md#890cdede05098009).

```
gSQL> { CALL sqlbody_proc(2, 4) };
V1 = 3

Procedure Call complete.
```

```
gSQL> \var a NATIVE_INTEGER

gSQL> CALL externalbody_proc( 2, 4 , :a );

Procedure Call complete.

gSQL> \print a

A
-
6
```

It supports the following syntax for a procedure to support a procedure call escape sequence used in ODBC or JDBC.

```
{ CALL procedure_name( param1, param2, ... ) }
```

A syntax of a procedure call escape sequence is used like as a general SQL.

```
gSQL> { CALL sqlbody_proc(2, 4) };
V1 = 3

Procedure Call complete.
```

```
gSQL> \var a NATIVE_INTEGER

gSQL> { CALL externalbody_proc( 2 , 4 , :a ) };

Procedure Call complete.

gSQL> \print a

A
-
6
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

<a id="8a5a397aa0608de2"></a>
### Dropping Schema-level Procedure

A schema-level procedure is dropped by the following DROP PROCEDURE statement.  
For more information, refer to [DROP PROCEDURE](31-psm-sql-references.md#edab1b4697fec9a3).

```
DROP PROCEDURE PROC1;
```

It also supports IF EXISTS statement like as other DROP statements of GOLDILOCKS.

```
DROP PROCEDURE IF EXISTS PROC1;
```

<a id="6fed1496fbe3b383"></a>
### Recompiling Schema-level Procedure

If an object referenced inside of a schema-level subprogram is altered, then it may affects the corresponding subprogram and should create the execution plan again.

<a id="e963d694fbec3307"></a>
#### Referenced Object in an Argument or a Declarative Part of &lt;SQL body&gt;

If the used object is altered when defining various items in a declarative part or an argument type, then the procedure plan is automatically recompiled.

- An object used in %TYPE, %ROWTYPE
- An object used in an explicit cursor definition statement

If the corresponding procedure is performed for the first time after an object is altered, then the plan is automatically recreated according to the following order.

1. Bring the plan of the corresponding procedure from a plan cache.
2. Search for objects which were altered during validating an object list of that plan.
3. Discard the current plan, and create a new plan from a procedure definition statement stored in a dictionary.
4. Register a newly created plan on a plan cache. 
5. Execute the plan.

<a id="52f5bcb8f323a217"></a>
#### Referenced Object in an SQL of &lt;SQL body&gt;'s &lt;pl statement&gt;

An SQL plan used in the body is not stored in a procedure plan, and only the SQL text is stored. When executing a procedure, it creates a plan by compiling the corresponding SQL statement in real time, then executes it. Therefore, an SQL object used within a body does not affect the procedure plan itself.

However, if an object is altered, the number or type of binds which are the existing interfaces of a procedure may be altered, or columns may be dropped. Therefore, an error may occur when executing it if the procedure is not appropriately altered.

<a id="62833595de847a81"></a>
#### Library Object Referenced by &lt;external body&gt;

If the library object referenced by &lt;external body&gt; is changed, then the procedure plan is automatically recompiled. However, the procedure is not recompiled even though the user changes the external routine. The database can not automatically detect changes to the shared library called externally.

<a id="090a35bb2f3c8981"></a>
## Schema-level Function

A schema-level function is a schema-level subprogram in function form, which is used within an expression.

<a id="895845332f6544a8"></a>
### Creating Schema-level Function

A schema-level function is created as follows. A precision and a scale value of an argument type should be specified if in need.  
The format of &lt;routine body&gt; in the schema-level function is &lt;SQL body&gt; or &lt;external body&gt;.  
For more information, refer to [CREATE FUNCTION](31-psm-sql-references.md#8343c001bfba29fc).

- Schema-level function which is &lt;SQL body&gt;

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

- Schema-level function which is &lt;external body&gt;

```
gSQL>
CREATE FUNCTION func1( p1 NATIVE_INTEGER,
                       p2 NATIVE_INTEGER )
  RETURN NATIVE_INTEGER AS
LANGUAGE C
LIBRARY lib NAME "add"
PARAMETERS( p1 INT , 
            p2 INT , 
            RETURN INT );

Function created.
```

Like as a procedure, a created schema-level function is found throughINFORMATION_SCHEMA.ROUTINES and INFORMATION_SCHEMA.PARAMETERS table.

<a id="be84bdb82b65470a"></a>
### Using Schema-level Function

A schema-level function can be used in all expressions in which a general SQL or an SQL object within PSM can be used.

```
gSQL> SELECT sqlbody_func( 2 , 4 ) FROM dual;

SQLBODY_FUNC( 2 , 4 )
---------------------
                    3

1 row selected.
```

```
gSQL> SELECT externalbody_func( 2 , 4 ) FROM dual;

EXTERNALBODY_FUNC( 2 , 4 )
--------------------------
                         6

1 row selected.
```

It is used as follows within PSM.

```
gSQL>
DECLARE
  v1 INTEGER;
BEGIN
  v1 := sqlbody_func( 2, 4 );
  DBMS_OUTPUT.PUT_LINE( 'v1 = ' || v1 );
END;
/

v1 = 3
Anonymous PL block executed.
```

```
gSQL>
DECLARE
  v1 NATIVE_INTEGER;
BEGIN
  v1 := externalbody_func( 2, 4 );
  DBMS_OUTPUT.PUT_LINE( 'v1 = ' || v1 );
END;
/

v1 = 6
Anonymous PL block executed.
```

It can be performed by using CALL statement as follows.

For more information, refer to [CALL Statement](31-psm-sql-references.md#890cdede05098009).

```
gSQL> \var v1 INTEGER

gSQL> CALL sqlbody_func( 2 , 4 ) INTO :v1;

Procedure Call complete.

gSQL> \print v1

V1
--
 3
```

```
gSQL> \var v1 NATIVE_INTEGER

gSQL> CALL externalbody_func( 2 , 4 ) INTO :v1;

Procedure Call complete.

gSQL> \print v1

V1
--
 6
```

Like as a schema-level procedure, a procedure call escape sequence statement is also supported.

```
{ ? = CALL function_name( param1, param2, ... ) }
```

```
gSQL> \var v1 INTEGER

gSQL> { :v1 = CALL sqlbody_func( 2 , 4 ) };

Procedure Call complete.

gSQL> \print v1

V1
--
 3
```

```
gSQL> \var v1 NATIVE_INTEGER

gSQL> { :v1 = CALL externalbody_func( 2 , 4 ) };

Procedure Call complete.

gSQL> \print v1

V1
--
 6
```

<a id="88fdff5d1a1a2642"></a>
### Dropping Schema-level Function

A schema-level function is dropped by the following DROP FUNCTION statement.  
For more information, refer to [DROP FUNCTION](31-psm-sql-references.md#c7cbdaa712da2629).

```
gSQL> DROP FUNCTION FUNC1;

Function dropped.
```

---

[← 24. PSM Cursor Statements](24-psm-cursor-statements.md) · [Table of contents](../README.md) · [26. Using SQLs in PSM →](26-using-sqls-in-psm.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
