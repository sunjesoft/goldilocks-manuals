<a id="85c3f4c1b69063d9"></a>

# 31. PSM SQL References

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/85c3f4c1b69063d9)  
> Tag: `26c.1_0_tag`

[← 30. PSM Language Element References](30-psm-language-element-references.md) · [Table of contents](../README.md) · [32. Built-in Package →](32-built-in-package.md)

<a id="5568841efba34448"></a>
## ALTER FUNCTION

<a id="d52cd80808d91509"></a>
### Function

It recompiles a function.

<a id="bb2c09e356d24496"></a>
### Syntax

```
<alter function statement> ::=
    ALTER FUNCTION function_name COMPILE
    ;
```

<a id="479287854072125a"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter function statement&gt;.

- The owner of that function
- (ALTER PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the function belongs
- ALTER ANY PROCEDURE ON DATABASE

<a id="1a679bd5d7366666"></a>
### Syntax Rules and Parameters

<a id="973e4265045fec79"></a>
#### function_name

It is a name of function to be compiled.  
It can define the schema to which the function belongs, such as schema_name.func_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="61b5b1654b52860b"></a>
### Description

It recompiles a specified schema-level function.

<a id="a1ac961a2e86ae57"></a>
### Examples

```
gSQL> ALTER FUNCTION FUNC1 COMPILE;

Function altered.
```

<a id="43b6ef0b6fa12d58"></a>
### Compatibility

It is a statement altering characteristics specified when performing CREATE in the SQL standard, and astatement recreating a plan of a function in GOLDILOCKS.

**SQL standard compatibility**

<a id="abc0f66cb4186c44"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="b94cf031d7bdf4eb"></a>
### For More Information

Refer to the following.

- [CREATE FUNCTION](#8343c001bfba29fc)
- [DROP FUNCTION](#c7cbdaa712da2629)

<a id="ed764dabc1cf7118"></a>
## ALTER PACKAGE

<a id="32f893a89245ff7f"></a>
### Function

It recompiles a package.

<a id="eb100209076ef05a"></a>
### Syntax

```
<alter package statement> ::=
    ALTER PACKAGE package_name <package compile clause>
    ;

<package compile clause> ::=
    COMPILE [PACKAGE|SPECIFICATION|BODY]
```

<a id="79d1e88f456edde5"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter package statement&gt;.

- The owner of that package
- (ALTER PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs 
- ALTER ANY PACKAGE ON DATABASE

<a id="783744942988f04b"></a>
### Syntax Rules and Parameters

<a id="ca33d0122f9363d0"></a>
#### package_name

It is a name of package to be compiled.  
It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="37e0945d9f72a6fe"></a>
#### &lt;package compile clause&gt;

It specifies the target to compile for a package.  
If the target is omitted, it is the same as specifying PACKAGE, and both the package specification and package body are recompiled.

- PACKAGE
    - It recompiles both the package specification and package body.
- SPECIFICATION
    - It recompiles only the package specification.
- BODY
    - It recompiles only the package body.

<a id="e8a9470a83664c86"></a>
### Description

It recompiles the specified package.  
The execution code of the compiled package is stored in the plan cache.

<a id="99dcb14119543bcd"></a>
### Examples

```
ALTER PACKAGE PKG1 COMPILE;
Package altered.
```

```
ALTER PACKAGE PKG1 COMPILE PACKAGE;
Package altered.
```

```
ALTER PACKAGE PKG1 COMPILE BODY;
Package altered.
```

<a id="0fc0ed1aeaf15dea"></a>
### Compatibility

It is ALTER MODULE statement in the SQL standard.

<a id="21751579362d4c0e"></a>
### For More Information

Refer to the following.

- [CREATE PACKAGE](#d67c80375fa9e3c8)
- [CREATE PACKAGE BODY](#397f0c3a716022e0)
- [DROP PACKAGE](#12916c88f352e944)

<a id="066771bec4083e3c"></a>
## ALTER PROCEDURE

<a id="d647e77d0004ba88"></a>
### Function

It recompiles a procedure.

<a id="1726a330f70439e1"></a>
### Syntax

```
<alter procedure statement> ::=
    ALTER PROCEDURE proc_name COMPILE
    ;
```

<a id="8c0fbb3f37ca8529"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter procedure statement&gt;.

- The owner of that procedure
- (ALTER PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- ALTER ANY PROCEDURE ON DATABASE

<a id="3535a8bb45579092"></a>
### Syntax Rules and Parameters

<a id="5dc57937e4b4fd38"></a>
#### proc_name

It is a name of procedure to be compiled.  
It can define the schema to which the procedure belongs, such as schema_name.proc_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="136ea6a79047f250"></a>
### Description

It recompiles a specified schema-level procedure.

<a id="fb10a5677644e667"></a>
### Examples

```
gSQL> CREATE OR REPLACE PROCEDURE PROC1( A1 INTEGER )
IS
BEGIN
  INSERT INTO T1 VALUES( A1 );
END;
/

ERR-01000(16409): Warning: Routine definition has compilation errors
ERR-HY000(17032): PSM compilation error : 
(1) at (5:15): ERR-17053: schema or table object does not exist
Procedure created.

gSQL> CALL PROC1(1);

ERR-HY000(17032): PSM compilation error : 
(1) at (5:15): ERR-17053: schema or table object does not exist

gSQL> CREATE TABLE T1( I1 INTEGER );

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> ALTER PROCEDURE PROC1 COMPILE;

Procedure altered.

gSQL> COMMIT;

Commit complete.

gSQL> CALL PROC1(2);

Procedure Call complete.

gSQL> SELECT * FROM T1;

I1
--
 2

1 row selected.
```

<a id="60688a3a6b6d7dba"></a>
### Compatibility

It is a statement altering characteristics specified when performing CREATE in the SQL standard, and astatement recreating a plan of a procedure in GOLDILOCKS.

**SQL standard compatibility**

<a id="971df9b208ec75af"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="82f01795fd3f4b5b"></a>
### For More Information

Refer to the following.

- [CREATE PROCEDURE](#d439613cbc283235)
- [DROP PROCEDURE](#edab1b4697fec9a3)

<a id="d86df859bc319efc"></a>
## ALTER TRIGGER name COMPILE

<a id="26314b18f74734f0"></a>
### Function

It recompiles the trigger.

<a id="d201a2cb73eedcb8"></a>
### Syntax

```
<alter trigger compile statement> ::=
    ALTER TRIGGER <trigger name> COMPILE
    ;
```

<a id="c202e687004d2dfe"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter trigger compile statement&gt;.

- The owner of that trigger
- (ALTER TRIGGER or CONTROL SCHEMA) ON SCHEMA for the schema to which the trigger belongs
- ALTER ANY TRIGGER ON DATABASE

<a id="b870892938774ab4"></a>
### Syntax Rules and Parameters

<a id="ceb76a27d770b7d8"></a>
#### &lt;trigger name&gt;

It is a name of trigger to be compiled.  
It can define the schema to which the trigger belongs, such as schema_name.trigger_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="106eb1664bb6b435"></a>
### Description

It recompiles the specified trigger.

<a id="13dfaf18632a77d4"></a>
### Examples

```
-- This is a trigger that records the changes in orders to order_status_history when the orders table is updated.
gSQL> 
CREATE OR REPLACE TRIGGER trg_orders_status_audit
AFTER UPDATE OF status ON orders
REFERENCING OLD ROW AS o_row
            NEW ROW AS n_row            
FOR EACH ROW
BEGIN
  INSERT INTO order_status_history VALUES( o_row.order_id,
                                           o_row.status,
                                           n_row.status,
                                           SYSDATE );
END;
/

ERR-01000(16659): Warning: trigger "PUBLIC"."TRG_ORDERS_STATUS_AUDIT" has compilation errors : 
(1) at (8:3): ERR-42000(16040): table or view does not exist
Trigger created.

-- The UPDATE statement failed because the trigger was invalid.
gSQL>
UPDATE orders
   SET status = 'Shipped', updated_at = SYSDATE
 WHERE order_id = 1;

ERR-0W000(17134): TRIGGER(TRG_ORDERS_STATUS_AUDIT) compilation error : 
(1) at (4:3): ERR-42000(16040): table or view does not exist

-- Created the order_status_history table referenced by the trigger.
gSQL>
CREATE TABLE order_status_history( order_id   NUMBER,
                                   old_status VARCHAR2(20),
                                   new_status VARCHAR2(20),
                                   changed_at DATE );

Table created.

-- Recompiled the trigger to check its status.
gSQL> ALTER TRIGGER trg_orders_status_audit COMPILE;

Trigger altered.

-- Successfully performed the UPDATE on the orders table.
gSQL>
UPDATE orders
   SET status = 'Shipped', updated_at = SYSDATE
 WHERE order_id = 1;

1 row updated.

gSQL> SELECT * FROM order_status_history;

ORDER_ID OLD_STATUS     NEW_STATUS CHANGED_AT
-------- -------------- ---------- ----------
       1 Order Received Shipped    2025-08-12

1 row selected.
```

<a id="9ef538be60e8d85f"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="7a74ed6662f655ef"></a>
### For More Information

Refer to the following.

- [CREATE TRIGGER](#44e30f425949fd8e)
- [DROP TRIGGER](#c5e9e28a6d05bf8b)

<a id="87a5b7084ef9f6ba"></a>
## ALTER TRIGGER name ENABLE/DISABLE

<a id="3c056ebb363665fa"></a>
### Function

It can enable or disable the trigger.

<a id="60bf71edf254489f"></a>
### Syntax

```
<alter trigger enforcement statement> ::=
    ALTER TRIGGER <trigger name> <trigger enforcement>
    ;

<trigger enforcement> ::=
      { ENABLE | ENFORCED }
    | { DISABLE | NOT ENFORCED }
```

<a id="400795337b0aa875"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter trigger enforcement statement&gt; .

- The owner of that trigger
- (ALTER TRIGGER or CONTROL SCHEMA) ON SCHEMA for the schema to which the trigger belongs
- ALTER ANY TRIGGER ON DATABASE

<a id="87262b6ba9d62580"></a>
### Syntax Rules and Parameters

<a id="09b7e825f2aca908"></a>
#### &lt;trigger name&gt;

It is the name of the trigger whose enablement status is to be changed.  
It can define the schema to which the trigger belongs, such as schema_name.trigger_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="46671625abbdf164"></a>
#### &lt;trigger enforcement&gt;

ENABLE and ENFORCED have the same meaning.  
DISABLE and NOT ENFORCED have the same meaning.

- ENABLE
    - It enables the trigger when a DML occurs on the event table. 
- DISABLE
    - It disables the trigger when a DML occurs on the event table.

<a id="a4454bb16fbc9fd2"></a>
### Description

It can enable or disable the trigger.

<a id="98663217bcedcace"></a>
### Examples

- Example of disabling a trigger

```
-- Create an invalid trigger.
gSQL>
CREATE OR REPLACE TRIGGER trg_orders_status_audit
AFTER UPDATE OF status ON orders
REFERENCING OLD ROW AS o_row
            NEW ROW AS n_row            
FOR EACH ROW
BEGIN
  INSERT INTO order_status_history VALUES( o_row.order_id,
                                           o_row.status,
                                           n_row.status,
                                           SYSDATE );
END;
/

ERR-01000(16659): Warning: trigger "PUBLIC"."TRG_ORDERS_STATUS_AUDIT" has compilation errors : 
(1) at (7:3): ERR-42000(16040): table or view does not exist
Trigger created.

-- The UPDATE statement failed because the trigger was invalid.
gSQL> 
UPDATE orders
   SET status = 'Shipped', updated_at = SYSDATE
 WHERE order_id = 1;

ERR-0W000(17134): TRIGGER(TRG_ORDERS_STATUS_AUDIT) compilation error : 
(1) at (4:3): ERR-42000(16040): table or view does not exist

-- Disable the trigger.
gSQL> ALTER TRIGGER trg_orders_status_audit DISABLE;

Trigger altered.

-- Successfully performed the UPDATE.
gSQL> UPDATE orders
   SET status = 'Shipped', updated_at = SYSDATE
 WHERE order_id = 1;

1 row updated.
```

- Example of enabling a trigger

```
-- Create an invalid trigger in a disabled state.
gSQL>
CREATE OR REPLACE TRIGGER trg_orders_status_audit
AFTER UPDATE OF status ON orders
REFERENCING OLD ROW AS o_row
            NEW ROW AS n_row
FOR EACH ROW
DISABLE
BEGIN
  INSERT INTO order_status_history VALUES (o_row.order_id, o_row.status, n_row.status, SYSDATE);
END;
/

ERR-01000(16659): Warning: trigger "PUBLIC"."TRG_ORDERS_STATUS_AUDIT" has compilation errors : 
(1) at (8:3): ERR-42000(16040): table or view does not exist
Trigger created.

-- The trigger does not execute upon creation because it is disabled.
gSQL>
UPDATE orders
   SET status = 'Processing Order', updated_at = SYSDATE
 WHERE order_id = 1;

1 row updated.

gSQL> SELECT * FROM order_status_history;

no rows selected.

-- Create the order_status_history table referenced by the trigger.
gSQL>
CREATE TABLE order_status_history( order_id   NUMBER,
                                   old_status VARCHAR2(20),
                                   new_status VARCHAR2(20),
                                   changed_at DATE );

Table created.

-- Recompiled the trigger to check its status.
gSQL> ALTER TRIGGER trg_orders_status_audit COMPILE;

Trigger altered.

-- Enable the trigger.
gSQL> ALTER TRIGGER trg_orders_status_audit ENABLE;

Trigger altered.

-- The trigger executes on UPDATE.
gSQL>
UPDATE orders
   SET status = 'Shipped', updated_at = SYSDATE
 WHERE order_id = 1;

1 row updated.

gSQL> SELECT * FROM order_status_history;

ORDER_ID OLD_STATUS       NEW_STATUS CHANGED_AT
-------- ---------------- ---------- ----------
       1 Processing Order Shipped    2025-08-12

1 row selected.
```

<a id="9b9f7de3790f7ec6"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="bf5eb836d4cd3048"></a>
### For More Information

Refer to the following.

- [CREATE TRIGGER](#44e30f425949fd8e)
- [DROP TRIGGER](#c5e9e28a6d05bf8b)

<a id="7a2a65b5c770fb59"></a>
## ALTER TRIGGER name RENAME TO

<a id="b6bbbfedd9d03118"></a>
### Function

It renames the trigger.

<a id="625ec15d7b01a637"></a>
### Syntax

```
<alter trigger rename statement> ::=
    ALTER TRIGGER <trigger name> RENAME <new trigger name>
    ;
```

<a id="ef8350fd9bc6c71d"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter trigger rename statement&gt;.

- The owner of that trigger
- (ALTER TRIGGER or CONTROL SCHEMA) ON SCHEMA for the schema to which the trigger belongs
- ALTER ANY TRIGGER ON DATABASE

<a id="d059618eb2af71f6"></a>
### Syntax Rules and Parameters

<a id="bb6571439470eabb"></a>
#### &lt;trigger name&gt;

It is the name of the trigger to be renamed.  
It can define the schema to which the trigger belongs, such as schema_name.trigger_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="33f1780018adfbd6"></a>
#### &lt;new trigger name&gt;

It is the name of the trigger to be renamed, and must be unique within the schema.  
The new trigger name must be less than 128 bytes in length.

<a id="e3a90c9627ccb01c"></a>
### Description

It renames the specified trigger.

<a id="c194bd6de50d5266"></a>
### Examples

```
gSQL> ALTER TRIGGER t1 RENAME TO new_t1;

Trigger altered.
```

<a id="2c40caeb659599b8"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="6f57570defaa9f98"></a>
### For More Information

Refer to the following.

- [CREATE TRIGGER](#44e30f425949fd8e)
- [DROP TRIGGER](#c5e9e28a6d05bf8b)

<a id="890cdede05098009"></a>
## CALL Statement

<a id="092b0bce18126480"></a>
### Function

It performs a schema-level procedure or a function.

<a id="60bef7d984570fa6"></a>
### Syntax

```
<call statement> ::= 
    <sql call statement> | <odbc procedure call escape sequence>
    ;

<sql call statement> ::=
    CALL proc_name [ ( value_expr [ , value_expr ] .. ) ]  [ INTO { '?' | { host_param [ indicator_param ] } } ]

<odbc procedure call escape sequence> ::=
    '{' [ ? = ] CALL proc_name [ ( value_expr [ , value_expr ] .. ) ] '}'
```

<a id="c611fce93171f1ba"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;call statement&gt;.

- The EXECUTE privilege for that procedure
- (EXECUTE PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- EXECUTE ANY PROCEDURE ON DATABASE

<a id="f89160d5a2a84bf8"></a>
### Syntax Rules and Parameters

<a id="ff72b7f7f55435b8"></a>
#### proc_name

- It is a name of a procedure/ function to be executed.
- It may includes a schema to which the procedure belongs such as schema_name.proc_name.

<a id="de454f25d3b4e331"></a>
#### value_expr

It expresses an argument value that were transferred to the procedure.   
It can use a bind parameter such as '?' or ':V1'.

<a id="af1938e200a47300"></a>
### Description

It executes a schema-level SQL procedure or a function by using specified arguments.

A function of &lt;sql call statement&gt; form returns the result value by using a host variable expression or a dynamic bind parameter (?) after INTO clause.

&lt;odbc procedure call escape sequence&gt; form is a standard statement to call PROCEDURE in  ODBC/ JDBC, and GOLDILOCKS supports this statement in a server. (It can also be used in a tool such as gsql.) A function returns the result value by using assign expressions ( ? = ) at the front.

<a id="588476b9113d11c3"></a>
### Examples

<a id="50f0225a927c46bf"></a>
#### Call Procedure

```
gSQL> CREATE OR REPLACE PROCEDURE PROC1
(
  A1 INTEGER
)
IS
BEGIN
  DBMS_OUTPUT.PUT_LINE('A1=' || A1);
END;
/

Procedure created.

gSQL> \var v1 INTEGER;
gSQL> \exec :v1 := 123;
gSQL> CALL PROC1(:v1);
A1=123

Procedure Call complete.
```

<a id="5e0487114d010ec6"></a>
#### Call Function

```
CREATE OR REPLACE FUNCTION FUNC1
(
  A1 INTEGER
)
RETURN INTEGER
IS
BEGIN
    return A1;
END;
/

Function created.


gSQL> \var v1 INTEGER;
gSQL> \var v2 INTEGER;
gSQL> \exec :v1 := 123;
gSQL> CALL FUNC1(:v1) INTO :v2;
Procedure Call complete.

gSQL> \print v2;
 V2
---
123
```

<a id="6c73d7cbfabf32f0"></a>
### Compatibility

The SQL standard allows only the call for a PROCEDURE, so it does not define below [INTO] clause.

<a id="8343c001bfba29fc"></a>
## CREATE FUNCTION

<a id="ec654d480bc7088c"></a>
### Function

It defines a schema-level function.

<a id="70b633338a3ae1c4"></a>
### Syntax

```
<create function statement> ::= 
        CREATE [ OR REPLACE ] FUNCTION <function name> 
        [ ( <parameter list> ) ]
        <return clause>
        [ <function option list> ]
        { IS | AS }
        <routine body>
        ; 

<parameter list> ::=
      <parameter> [ , ... ]

<parameter> ::=
      <parameter name>
      [ <parameter mode> ]
      <datatype>
      [ <parameter default> ]

<parameter mode> ::= 
      IN 
    | OUT 
    | IN OUT

<parameter default> ::= 
      { := | DEFAULT } <value expression>

<function option list> ::=
      <function option> [ ... ]

<function option> ::=
      <invoker rights clause>
    | <function characteristics>

<invoker rights clause> ::=
      AUTHID CURRENT_USER 
    | AUTHID DEFINER

<function characteristics> ::=
      <deterministic characteristic>
    | <null-call clause>
    | <SQL-data access indication>

<routine body> ::=
      <SQL body>
    | <external body>

<SQL body> ::=
      [ <declare item> ]
      <body>

<external body> ::=
      <call specification>
```

<a id="dd71705c2ca788bb"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;create function statement&gt;.

- One of the following privileges is required to create a function.
    - (CREATE PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the function belongs
    - CREATE ANY PROCEDURE ON DATABASE 
- If a function already exists when using OR REPLACE clause, then one of the following privileges dropping the existing function is required.
    - The owner of that function
    - (DROP PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the function belongs
    - DROP ANY PROCEDURE ON DATABASE
- The user who performed the statement becomes the owner of the created function.

<a id="213234019a5a6b8b"></a>
### Syntax Rules and Parameters

<a id="a4a8d55cb39ceaf1"></a>
#### OR REPLACE

It replaces an existing function with a new function when the function already exists.

<a id="ac08778a017e9493"></a>
#### function name

It is a name of function to be created, and it should be a unique name in a schema.  
It can define the schema to which the function belongs, such as schema_name.function_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of a function name should be shorter than 128 bytes.

<a id="99cd0fc31d09c7d6"></a>
#### parameter name

It defines a parameter name of the function.   
The name of each parameter should be unique in a function.   
In other words, the function's parameter and PL item can not have the same name.   
The length of a parameter name should be shorter than 128 bytes.   
The maximum number of parameters available in a single function is limitless.

<a id="5a1f718c01a6813d"></a>
#### parameter mode

It sets each parameter mode.   
The parameter modes are IN, OUT, and IN OUT.  
If the parameter mode is not specified, the default mode is *IN*.

<a id="42f5a40a82758a69"></a>
#### parameter default

It is the default value of the parameter.  
The parameter with the specified parameter default can be omitted when executing the function.   
If the parameter is not specified but omitted, then the default value is &lt;value expression&gt; specified when defining the parameter.  
The datatype of &lt;value expression&gt; should be the datatype of the parameter.  
All parameters defined after the parameter having &lt;parameter default&gt; should have &lt;parameter default&gt;.

<a id="255e578fa12ba583"></a>
#### return clause

It defines the return type of the function.   
It is defined as follows in &lt;return clause&gt;.

- RETURN &lt;datatype&gt;
    - It defines the datatype of the return value returned by the function.
- RETURN TABLE ( &lt;table function column list&gt; )
    - It defines the table type of the returned result set.

<a id="2b036de7c66de1a4"></a>
#### table function column list

It is the column name of the result set returned by the table function.  
The length of a column name should be shorter than 128 bytes.  
The number of columns are limitless.  
Each column name is unique in &lt;table function column list&gt;.  
The column name can be the same as the parameter name and the declare item name.  
The column defined in &lt;table function column list&gt; can not be referenced in PL block of the function.

<a id="e054adcb628fe369"></a>
#### invoker rights clause

It specifies whether to execute the name interpretation and authority of the object referred when executing the function from the perspective of DEFINER or the perspective of CURRENT_USER.

- AUTHID CURRENT_USER: SQLs which are being performed during performing a function are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing a function are interpreted and performed according to an authorization of a definer.

If &lt;invoker rights clause&gt; is omitted, then the default value is AUTHID DEFINER.

<a id="91a145d830adf882"></a>
#### function characteristics

&lt;function characteristics&gt; specifies the characteristics of the function.  
The redundant characteristics are not allowed.  
For more information, refer to [Routine Characteristics](30-psm-language-element-references.md#a870cb9c0d6274b0).

<a id="567a9bdd74c09c43"></a>
#### routine body

- SQL body
    - For more information, refer to [Block (BEGIN .. END)](30-psm-language-element-references.md#acfcdb439eaed2a5).
- external body
    - For more information, refer to [Call Specification](30-psm-language-element-references.md#f24bb921ad663f66).
- The bind parameter such as '?' or ':V1' is not allowed in &lt;routine body&gt; of the function.

<a id="150312308eecbf3e"></a>
### Description

It defines a schema-level SQL function. The created function can be called from all expressions.

The definition of a function can be viewed in ROUTINES table of INFORMATION_SCHEMA. The definition of a function parameter can be viewed in PARAMETERS table of INFORMATION_SCHEMA.

If a function becomes temporarily unstable due to absences of related objects, then it can try to recreate a plan by using [ALTER FUNCTION](#5568841efba34448) statement.

The created function can be dropped by using [DROP FUNCTION](#c7cbdaa712da2629) statement.  
The maximum number of functions to be created is not limited. Therefore, they can be created as many as the storage space is available.

<a id="47d2ed956b2dc4b6"></a>
### Examples

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

<a id="b066df935255a695"></a>
### Compatibility

The SQL standard does not define OR REPLACE clause.

**SQL standard compatibility**

<a id="4a17c5386dc90ace"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T471 | Result sets return value | X |
| T341 | Overloading of SQL-invoked functions and SQL-invoked procedures | X |
| S023 | Basic structured types | X |
| S241 | Transform functions | X |
| S024 | Enhanced structured types | X |
| T571 | Array-returning external SQL-invoked functions | X |
| T572 | Multiset-returning external SQL-invoked functions | X |
| S201 | SQL routines on arrays | X |
| S202 | SQL-invoked routines on multisets | X |
| T323 | Explicit security for external routines | X |
| S231 | Structured type locators | X |
| S232 | Array locators | X |
| S233 | Multiset locators | X |
| T041 | Basic LOB data type support | X |
| S027 | Create method by specific method name | X |
| T041 | Basic LOB data type support | X |
| T324 | Explicit security for SQL routines | O |
| T326 | Table functions | O |
| T651 | SQL-schema statements in SQL routines | X |
| T652 | SQL-dynamic statements in SQL routines | O |
| T653 | SQL-schema statements in external routines | X |
| T654 | SQL-dynamic statements in external routines | X |
| T655 | Cyclically dependent routines | X |
| T272 | Enhanced savepoint management | X |
| T522 | Default values for IN parameters of SQL-invoked procedures | O |
| B121 | Routine language Ada | X |
| B122 | Routine language C | O |
| B123 | Routine language COBOL | X |
| B124 | Routine language Fortran | X |
| B125 | Routine language MUMPS | X |
| B126 | Routine language Pascal | X |
| B127 | Routine language PL/I | X |
| B128 | Routine language SQL | O |
| B129 | Routine language Ada: VARCHAR and NUMERIC support | X |

<a id="cd8cbf825b13f5b7"></a>
### For More Information

Refer to the following.

- [DROP FUNCTION](#c7cbdaa712da2629)
- [ALTER FUNCTION](#5568841efba34448)

<a id="d3c4a1abc483c544"></a>
## CREATE LIBRARY

<a id="650e21b70d63de14"></a>
### Function

It creates a library which is a schema object related to the shared library of C language program.

<a id="44b54d564291c964"></a>
### Syntax

```
<create library statement> ::=
      CREATE [ OR REPLACE ] LIBRARY <library name> 
      { IS | AS }
      '<file path name>';
```

<a id="d4adb2254d7c9a38"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;create library statement&gt;.

- One of the following privileges is required to create a library.
    - (CREATE LIBRARY or CONTROL SCHEMA) ON SCHEMA for the schema to which the library belongs
    - CREATE ANY PACKAGE ON DATABASE
- If OR REPLACE clause is specified, then one of the following privileges is required to drop the existing library.
    - The owner of that library
    - (DROP LIBRARY or CONTROL SCHEMA) ON SCHEMA for the schema to which the library belongs
- The user who performed the statement becomes the owner of the created library.

<a id="cbfa21c3d998f480"></a>
### Syntax Rules and Parameters

<a id="862413df4e4317ac"></a>
#### OR REPLACE

It replaces an existing library with a new library when the library already exists.

<a id="a56f499094dfd9ab"></a>
#### library name

It is a name of library to be created, and it should be a unique name in a schema.  
It can define the schema to which the library belongs, such as schema_name.library_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of a library name should be shorter than 128 bytes.

<a id="97557f61a7e3defc"></a>
#### file path name

It can specify the name or full path of the shared library of C language program.

When creating a Library object, if only the filename is specified, the file must be located in the folder set by the EXTLIB_DIR property. Conversely, if the full path is specified, the shared library at that path will be executed.

When it is used in the cluster system, the same shared library files should be managed on each node.

<a id="c1ee591d0620fbb5"></a>
### Description

It creates a library which is a schema object related to the shared library of C language program.  
The library is called from [Call Specification](30-psm-language-element-references.md#f24bb921ad663f66).  
The created library can be dropped by using [DROP LIBRARY](#ac5c19f8f617c881) statement.

<a id="7ee014a8ef66469b"></a>
### Examples

- Specifying only the file name

```
gSQL>
CREATE LIBRARY lib1 AS 'add.so';
/

Library created.
```

- Specifying the full path and the file name

```
gSQL>
CREATE LIBRARY lib2 AS '/home/user1/files/add.so';
/

Library created.
```

<a id="b1fdc8c9ded78021"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="3b8e3a20888dcfa9"></a>
### For More Information

Refer to [DROP LIBRARY](#ac5c19f8f617c881).

<a id="d67c80375fa9e3c8"></a>
## CREATE PACKAGE

<a id="37e481c8d3f5054e"></a>
### Function

It defines the spec about public items to be used in a package.

<a id="3f49712f4d5e0c89"></a>
### Syntax

```
<create package statement> ::=
      CREATE [ OR REPLACE ] PACKAGE <package name>
      [ <invoker rights clause> ]
      { IS | AS }
      <declare item> 
      END [ <package name> ]
      ;

<invoker rights clause> ::=
      AUTHID CURRENT_USER 
    | AUTHID DEFINER

<declare item> ::=
      <variable declaration>
    | <type definition>
    | <explicit cursor declaration>
    | <explicit cursor definition>
    | <exception declaration>
    | <exception init pragma>
    | <procedure declaration>
    | <function declaration>
```

<a id="0d543e286f9a5d09"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;create package statement&gt;.

- One of the following privileges is required to create a package.
    - (CREATE PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
    - CREATE ANY PACKAGE ON DATABASE
- If a package already exists when using OR REPLACE clause, then one of the following privileges dropping the existing package is required.
    - The owner of that package
    - (DROP PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
- The user who performed the statement becomes the owner of the created package.

<a id="95a9c2ffbdbd68fd"></a>
### Syntax Rules and Parameters

<a id="d7adf8a4fc3a9f47"></a>
#### OR REPLACE

It replaces an existing package specification when the package already exists.

<a id="e0d2f64957041369"></a>
#### PACKAGE NAME

It is a name of package to be created, and it should be a unique name in a schema.   
It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.   
The length of a package name should be shorter than 128 bytes.

<a id="ceafb6d148b6ebba"></a>
#### invoker rights clause

It specifies whether to execute the name interpretation and authority of the object referred when executing the package from the perspective of DEFINER or the perspective of CURRENT_USER.

- AUTHID CURRENT_USER: SQLs which are being performed during performing a package are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing a package are interpreted and performed according to an authorization of a definer.

If &lt;invoker rights clause&gt; is omitted, then the default value is AUTHID DEFINER.

<a id="5c5355c510dde6f1"></a>
#### declare item

It declares an item which is accessible from out of the package. It is called as a public package item.   
A function and a procedure declared in the package spec should be defined in the create package body statement.  
An explicit cursor declared in the package spec without SQL should be defined in the create package body statement.   
For more information about the declarable item, refer to [declare item](30-psm-language-element-references.md#bfd9906c09fe918a) of  [Block (BEGIN .. END)](30-psm-language-element-references.md#acfcdb439eaed2a5).

<a id="b7c49d75eb8f1439"></a>
### Description

It creates the schema-level package specification.   
The information about package creation can be viewed in INFORMATION_SCHEMA.MODULES table.  
The list of each public procedure and function in the package can be viewed in INFORMATION_SCHEMA.ROUTINES table.  
The definitions of parameters of each public procedure and function in the package can be viewed in INFORMATION_SCHEMA.PARAMETERS table.

All public package items of the created package can be referred by another PSM object or the anonymous block.

If the package becomes invalid because the status of the object referred by the package is changed, then it can be recompiled with the following statements.

- ALTER PACKAGE &lt;package name&gt; COMPILE
- ALTER PACKAGE &lt;package name&gt; COMPILE SPECIFICATION

<a id="81f53054b0f0195c"></a>
### Examples

```
CREATE OR REPLACE PACKAGE PKG1
IS
  V1 INTEGER;
  PROCEDURE PROC1;
  FUNCTION FUNC1 RETURN INTEGER;
END;
/

Package created.
```

<a id="01cf383c85787c1e"></a>
### Compatibility

It is CREATE MODULE statement in the SQL standard.

<a id="35f6d0252d2b3798"></a>
### For More Information

Refer to the following.

- [CREATE PACKAGE BODY](#397f0c3a716022e0)
- [DROP PACKAGE](#12916c88f352e944)
- [ALTER PACKAGE](#ed764dabc1cf7118)

<a id="397f0c3a716022e0"></a>
## CREATE PACKAGE BODY

<a id="502c7ae643af8f82"></a>
### Function

It creates the definition about procedure/ function/ cursors to be used in the package.

<a id="959984dda550eafa"></a>
### Syntax

```
<create package body statement> ::=
      CREATE [ OR REPLACE ] PACKAGE BODY <package name>
      { IS | AS }
      <declare item>
      [ <initialization part> ]
      END [ <package name> ]
      ;

<declare item> ::=
    <variable declaration>
    | <type definition>
    | <explicit cursor declaration>
    | <explicit cursor definition>
    | <exception declaration>
    | <exception init pragma>
    | <procedure declaration>
    | <procedure definition>
    | <function declaration>
    | <function definition>

<initialization part> ::=
      BEGIN
      <pl statement list>
      [ <exception block> ]
```

<a id="32e6698cbbea4d7e"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;create package body statement&gt;.

- One of the following privileges is required to create a package body.
    - (CREATE PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
    - CREATE ANY PACKAGE ON DATABASE
- The package spec should be defined in advance.
- If a package body already exists when using OR REPLACE clause, then one of the following privileges dropping the existing package is required.
    - The owner of that package
    - (DROP PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
    - DROP ANY PACKAGE ON DATABASE
- The user who performed the statement becomes the owner of the created package.

<a id="0d9f10acc7d7958c"></a>
### Syntax Rules and Parameters

<a id="c5992e2a5370a499"></a>
#### OR REPLACE

It replaces an existing package body definition when the package body already exists.

<a id="175c4b614fc40f31"></a>
#### PACKAGE NAME

It is a name of package body to be created, and the name the same as the name used in creating a package spec should be used. It should be a unique name in a schema.   
It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.   
The length of a package name should be shorter than 128 bytes.

<a id="884a8231283f9a1e"></a>
#### declare item

It declares an item which can be used in the package body. It is called as a private package item.   
The name of private package item and the public package item should not be the same.  
The routines declared in the package spec should be defined in the package body.  
A cursor declared in the package spec without SQL should be defined in the package body.   
For more information about the declarable item, refer to [declare item](30-psm-language-element-references.md#bfd9906c09fe918a) of  [Block (BEGIN .. END)](30-psm-language-element-references.md#acfcdb439eaed2a5).

<a id="08b3d591faddf93c"></a>
#### Initialization Part

It describes statements which are performed only once to initialize internal variables while creating a package instance.  
For more information about the declarable item, refer to [declare item](30-psm-language-element-references.md#bfd9906c09fe918a) of  [Block (BEGIN .. END)](30-psm-language-element-references.md#acfcdb439eaed2a5).

<a id="24f2e7e86f8d17d0"></a>
### Description

It creates the schema-level package specification.   
The information of creating the package body can be viewed in INFORMATION_SCHEMA.MODULE_BODY table.

The private package item declared in the created package body can not be referred by another PSM object or the anonymous block.

If the package body becomes invalid because the status of the object referred by the package body is changed, then it can be recompiled with the following statements.

- ALTER PACKAGE &lt;package name&gt; COMPILE
- ALTER PACKAGE &lt;package name&gt; COMPILE BODY

The created package body can be dropped with the following statements.

- DROP PACKAGE &lt;package name&gt;
- DROP PACKAGE BODY &lt;package name&gt;

<a id="8044b0a8f1f27f58"></a>
### Examples

```
CREATE OR REPLACE PACKAGE PKG1
IS
  V1 INTEGER;
  PROCEDURE PROC1;
  FUNCTION FUNC1 RETURN INTEGER;
END;
/

Package created.

CREATE OR REPLACE PACKAGE BODY PKG1
IS
  FUNCTION FUNC1 RETURN INTEGER
  IS
  BEGIN
      RETURN V1;
  END;

  PROCEDURE PROC1
  IS
  BEGIN
      IF V1 IS NULL
      THEN
          V1 := 10;
      ELSE
          V1 := V1 + 10;
      END IF;
  END;

END;
/

Package created.
```

<a id="e73330385df94bfb"></a>
### Compatibility

The SQL standard does not define it.

<a id="e9188ec15841b396"></a>
### For More Information

Refer to the following.

- [CREATE PACKAGE](#d67c80375fa9e3c8)
- [DROP PACKAGE](#12916c88f352e944)
- [ALTER PACKAGE](#ed764dabc1cf7118)

<a id="d439613cbc283235"></a>
## CREATE PROCEDURE

<a id="399bd03c3bee39ef"></a>
### Function

It defines a schema-level procedure.

<a id="17f851f3ba3101b2"></a>
### Syntax

```
<create procedure statement> ::= 
        CREATE [ OR REPLACE ] PROCEDURE <procedure name> 
        [ ( <parameter list> ) ]
        [ <procedure option list> ]
        { IS | AS }
        <routine body>
        ; 

<parameter list> ::=
      <parameter> [ , ... ]

<parameter> ::=
      <parameter name>
      [ <parameter mode> ]
      <datatype>
      [ <parameter default> ]

<parameter mode> ::= 
      IN 
    | OUT 
    | IN OUT

<parameter default> ::= 
      { := | DEFAULT } <value expression>

<procedure option list> ::=
      <procedure option> [ ... ]

<procedure option> ::=
      <invoker rights clause>
    | <procedure characteristics>

<invoker rights clause> ::=
      AUTHID CURRENT_USER 
    | AUTHID DEFINER

<procedure characteristics> ::=
      <deterministic characteristic>
    | <SQL-data access indication>

<routine body> ::=
      <SQL body>
    | <external body>

<SQL body> ::=
      [ <declare item> ]
      <body>

<external body> ::=
      <call specification>
```

<a id="019018d24a7d4298"></a>
### Invocation and Access Rules

The user must meet the following conditions to execute the &lt;create procedure statement&gt;.

- One of the following privileges is required to create a procedure.
    - (CREATE PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
    - CREATE ANY PROCEDURE ON DATABASE 
- If a procedure already exists when using OR REPLACE clause, then one of the following privileges dropping the existing procedure is required.
    - The owner of that procedure
    - (DROP PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
    - DROP ANY PROCEDURE ON DATABASE
- The user who performed the statement becomes the owner of the created procedure.

<a id="8976681b1d662861"></a>
### Syntax Rules and Parameters

<a id="a1a0a4d559cc3fa7"></a>
#### OR REPLACE

It replaces an existing procedure with a new function when the procedure already exists.

<a id="7da779074fc9e53d"></a>
#### procedure name

It is a name of procedure to be created, and it should be a unique name in a schema.  
It can define the schema to which the procedure belongs, such as schema_name.procedure_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of a procedure name should be shorter than 128 bytes.

<a id="17a2bd2df61acefc"></a>
#### parameter name

It defines a parameter name of the procedure.   
The name of each parameter should be unique in a procedure.   
In other words, the procedure's parameter and PL item can not have the same name.   
The length of a parameter name should be shorter than 128 bytes.   
The maximum number of parameters available in a single procedure is limitless.

<a id="3d402b5489d6dc58"></a>
#### parameter mode

It sets each parameter mode.   
The parameter modes are IN, OUT, and IN OUT.  
If the parameter mode is not specified, the default mode is *IN*.

<a id="450c0dea5fae5f91"></a>
#### parameter default

It is the default value of the parameter.  
The parameter with the specified parameter default can be omitted when executing the procedure.   
If the parameter is not specified but omitted, then the default value is &lt;value expression&gt; specified when defining the parameter.  
The datatype of &lt;value expression&gt; should be the datatype of the parameter.  
All parameters defined after the parameter having &lt;parameter default&gt; should have &lt;parameter default&gt;.

<a id="1ec4753a6b0bc776"></a>
#### invoker rights clause

It specifies whether to execute the name interpretation and authority of the object referred when executing the procedure from the perspective of DEFINER or the perspective of CURRENT_USER.

- AUTHID CURRENT_USER: SQLs which are being performed during performing a procedure are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing a procedure are interpreted and performed according to an authorization of a definer.

If &lt;invoker rights clause&gt; is omitted, then the default value is AUTHID DEFINER.

<a id="4764ad16d1b5120b"></a>
#### procedure characteristics

&lt;procedure characteristics&gt; specifies the characteristics of the procedure.  
The redundant characteristics are not allowed.  
For more information, refer to [Routine Characteristics](30-psm-language-element-references.md#a870cb9c0d6274b0).

<a id="487cb1a00b218af6"></a>
#### routine body

- SQL body
    - For more information, refer to [Block (BEGIN .. END)](30-psm-language-element-references.md#acfcdb439eaed2a5).
- external body
    - For more information, refer to [Call Specification](30-psm-language-element-references.md#f24bb921ad663f66).
- The bind parameter such as '?' or ':V1' is not allowed in &lt;routine body&gt; of the procedure.

<a id="79091c0bca132062"></a>
### Description

It defines a schema-level SQL procedure. The created procedure can be called from CALL statement, anonymous block, or other procedure/ function.

The definition of a procedure can be viewed in ROUTINES table of INFORMATION_SCHEMA. The definition of a procedure parameter can be viewed in PARAMETERS table of INFORMATION_SCHEMA.

If a procedure becomes temporarily unstable due to absences of related objects, then it can try to recreate a plan by using [ALTER PROCEDURE](#066771bec4083e3c) statement.

The created procedure can be dropped by using [DROP PROCEDURE](#edab1b4697fec9a3) statement.  
The maximum number of procedures to be created is not limited. Therefore, they can be created as many as the storage space is available.

<a id="9b92023ff18337b6"></a>
### Examples

```
gSQL> CREATE OR REPLACE PROCEDURE PROC1( A1 INTEGER, A2 INTEGER )

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

Procedure created.
```

<a id="f60f370fe7090241"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="0c552fdda02a96ad"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T471 | Result sets return value | X |
| T341 | Overloading of SQL-invoked functions and SQL-invoked procedures | X |
| S023 | Basic structured types | X |
| S241 | Transform functions | X |
| S024 | Enhanced structured types | X |
| T571 | Array-returning external SQL-invoked functions | X |
| T572 | Multiset-returning external SQL-invoked functions | X |
| S201 | SQL routines on arrays | X |
| S202 | SQL-invoked routines on multisets | X |
| T323 | Explicit security for external routines | X |
| S231 | Structured type locators | X |
| S232 | Array locators | X |
| S233 | Multiset locators | X |
| T041 | Basic LOB data type support | X |
| S027 | Create method by specific method name | X |
| T041 | Basic LOB data type support | X |
| T324 | Explicit security for SQL routines | O |
| T326 | Table functions | O |
| T651 | SQL-schema statements in SQL routines | X |
| T652 | SQL-dynamic statements in SQL routines | O |
| T653 | SQL-schema statements in external routines | X |
| T654 | SQL-dynamic statements in external routines | X |
| T655 | Cyclically dependent routines | X |
| T272 | Enhanced savepoint management | X |
| T522 | Default values for IN parameters of SQL-invoked procedures | O |
| B121 | Routine language Ada | X |
| B122 | Routine language C | O |
| B123 | Routine language COBOL | X |
| B124 | Routine language Fortran | X |
| B125 | Routine language MUMPS | X |
| B126 | Routine language Pascal | X |
| B127 | Routine language PL/I | X |
| B128 | Routine language SQL | O |
| B129 | Routine language Ada: VARCHAR and NUMERIC support | X |

<a id="9bac952236c43555"></a>
### For More Information

Refer to the following.

- [DROP PROCEDURE](#edab1b4697fec9a3)
- [ALTER PROCEDURE](#066771bec4083e3c)

<a id="44e30f425949fd8e"></a>
## CREATE TRIGGER

<a id="c7e360db565ba72e"></a>
### Function

It creates a trigger.

<a id="3d608cb0da5d9cc0"></a>
### Syntax

```
<create trigger statement> ::=
      CREATE [ OR REPLACE ] TRIGGER <trigger name>
      <trigger action time>
      <trigger event list> ON <table name>
      [ REFERENCING <transition table or variable list> ]
      <triggered action>
      ;

<trigger action time> ::=
        BEFORE 
      | AFTER

<trigger event list> ::=
      <trigger event> [ OR <trigger event> [ ... ] ]

<trigger event> ::=
        INSERT
      | DELETE
      | UPDATE [ OF <trigger column list> ]

<trigger column list> ::=
      <column name list> 

<column name list> ::=
     <column name> [ { <comma> <column name> }... ]

<transition table or variable list> ::=
        OLD [ ROW ] [ AS ] <old transition variable name>
      | NEW [ ROW ] [ AS ] <new transition variable name>
      | OLD TABLE [ AS ] <old transition table name>
      | NEW TABLE [ AS ] <new transition table name>

<triggered action> ::=
        [ FOR EACH { ROW | STATEMENT } ]
        [ <trigger enforcement> ]
        [ <triggered when clause> ]
        <trigger body>

<trigger enforcement> ::=
        ENABLE
      | DISABLE
      | ENFORCED
      | NOT ENFORCED

<triggered when clause> ::=
      WHEN <left paren> <search condition> <right paren>

<trigger body> ::= 
        <PSM block>
      | CALL <procedure name>
```

<a id="769469223a9c3245"></a>
### Invocation and Access Rules

The user must meet the following conditions to execute the &lt;create trigger statement&gt;.

- One of the following privileges is required to create a trigger.
    - (CREATE TRIGGER or CONTROL SCHEMA) ON SCHEMA for the schema to which the trigger belongs
    - CREATE ANY TRIGGER ON DATABASE
- If a trigger already exists when using OR REPLACE clause, then one of the following privileges dropping the existing trigger is required.
    - The owner of that trigger
    - (DROP TRIGGER or CONTROL SCHEMA) ON SCHEMA for the schema to which the trigger belongs
    - DROP ANY TRIGGER ON DATABASE
- A trigger requires the TRIGGER privilege on the table.
    - The user who performed the statement becomes the owner of the created trigger.

<a id="4172f9e529554c5c"></a>
### Syntax Rules and Parameters

<a id="937cf09ad1a69e22"></a>
#### OR REPLACE

If a trigger with the same name already exists, the existing trigger is replaced with the new one.

<a id="a3d728fb350dc601"></a>
#### &lt;trigger name&gt;

It is a name of trigger to be created, and must be unique within the schema.  
It can define the schema to which the trigger belongs, such as schema_name.trigger_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The trigger name must be less than 128 bytes in length.

<a id="e0a6a782d3ca5531"></a>
#### &lt;trigger action time&gt;

It defines the timing of trigger execution as follows:

- BEFORE
    - The trigger is executed before the DML operation is performed.
- AFTER
    - The trigger is executed after the DML operation has been performed.

<a id="65081314cb3e6686"></a>
#### &lt;trigger event&gt;

The execution of a trigger is determined by the DML performed on the event table.  
One or more &lt;trigger event&gt;s can be specified.  
The same &lt;trigger event&gt; cannot be specified more than once.

The types of &lt;trigger event&gt; are as follows:

- INSERT
    - The trigger is executed when an INSERT statement is performed on the specified event table.
- UPDATE [ OF &lt;trigger column list&gt; ]
    - The trigger is executed when an UPDATE statement is performed on the specified event table.
    - If OF &lt;trigger column list&gt; is specified, the trigger is executed only when the specified columns are updated.
- DELETE
    - The trigger is executed when a DELETE statement is performed on the specified event table.

<a id="fe43768559aa332b"></a>
#### &lt;trigger column list&gt;

It is a clause that specifies the trigger to execute only when the designated columns are updated.  
Column names cannot be duplicated.  
All specified columns must actually exist in the event table.

<a id="b54e4d44fdf9d455"></a>
#### &lt;table name&gt;

It is the name of the base table object that is the target of the DML event detected by the trigger.  
The base table name may include a schema name in the form of schema_name.table_name.  
If the schema name is omitted, the default schema name of the user executing the statement is used.

<a id="be7501474a6ddc37"></a>
#### REFERENCING &lt;transition table or variable list&gt;

The REFERENCING transition tables and transition variables are used in a trigger to reference data before and after the execution of DML operations.

After the REFERENCING keyword, transition tables or transition variables can be declared as shown below, and duplicate declarations are not allowed.

- OLD transition table
    - It is a temporary table that can reference the original data before an UPDATE or DELETE is performed.
- NEW transition table
    - It is a temporary table that can reference the new data after an INSERT or UPDATE is performed.
- OLD transition variable
    - It is a variable that can reference the individual row data before an UPDATE or DELETE is performed.
- NEW transition variable
    - It is a variable that can reference the individual row data after an INSERT or UPDATE is performed.

The names of OLD transition table, NEW transition table, OLD transition variable, and NEW transition variable cannot be duplicated.  
Transition tables or transition variables declared by the user can only be used within the &lt;triggered action&gt;.

- Transition table
    - Provides the set of rows affected by the DML in the form of a table.
    - Cannot be declared in a BEFORE trigger.
    - Cannot be declared in a multiple-event trigger.
- Transition variable
    - Cannot be declared in a statement trigger.
    - In a trigger where the &lt;trigger event&gt; is INSERT, OLD transition variable cannot be declared.
    - In a trigger where the &lt;trigger event&gt; is DELETE, NEW transition variable cannot be declared.
    - In a multiple-event trigger including INSERT, if triggered by an INSERT operation, the OLD transition variable is NULL.
    - In a multiple-event trigger including DELETE, if triggered by a DELETE operation, the NEW transition variable is NULL.

<a id="f5be71d5645eb61c"></a>
#### FOR EACH ROW/ FOR EACH STATEMENT

It specifies the execution unit of the trigger.  
If not specified, the default is FOR EACH STATEMENT.

- FOR EACH ROW
    - Executed once for each row affected by the DML operation.
- FOR EACH STATEMENT
    - Executed only once when the DML operation is performed.

<a id="80e139c65a51a16f"></a>
#### &lt;trigger enforcement&gt;

It specifies whether the trigger is created in an enabled or disabled state.  
If not specified, the trigger is created in the enabled state by default.

ENABLE and ENFORCED have the same meaning.  
DISABLE and NOT ENFORCED have the same meaning.

- ENABLE
    - It enables the trigger when a DML occurs on the event table.
    - The trigger is executed when a DML event occurs.
- DISABLE
    - It disables the trigger when a DML occurs on the event table.
    - The trigger is not executed when a DML event occurs.

<a id="418dc82b035e5c69"></a>
#### &lt;triggered when clause&gt;

It specifies a conditional clause that controls whether the trigger is executed.

If the result of the &lt;triggered when clause&gt; is TRUE, the trigger is executed; if the result is FALSE, it is not executed.  
If no &lt;triggered when clause&gt; is specified, the trigger is always executed.

Functions can be used in the expression of the &lt;triggered when clause&gt;, but such functions must not have the MODIFIES SQL DATA attribute.

<a id="dcc8d301ba1bff24"></a>
#### &lt;trigger body&gt;

It defines the statements to be executed by the trigger.  
It consists of a PSM block or a CALL statement.

<a id="6944cd75f0fb844b"></a>
### Description

When a trigger is defined, it is executed when a DML event occurs on the specified base table.  
The definition of a trigger can be viewed in the TRIGGERS table of the INFORMATION_SCHEMA.

If a related object is modified and the trigger becomes invalid, it can be recompiled using the ALTER TRIGGER .. COMPILE statement.

The name of a created trigger can also be changed using the ALTER TRIGGER .. RENAME statement.

The activation state of a trigger can be changed by executing the following statements:

- ALTER TRIGGER .. ENABLE
- ALTER TRIGGER .. ENFORCED
    - It changes the trigger to the enabled state.
- ALTER TRIGGER .. DISABLE
- ALTER TRIGGER .. NOT ENFORCED
    - It changes the trigger to the disabled state.

A created trigger can be dropped using the DROP TRIGGER statement.  
If the event table object is dropped, the corresponding trigger is also dropped.

<a id="2541d66431a5b505"></a>
### Examples

- Example of trigger creation and execution
    - Table creation

```
-- System log table
gSQL>
CREATE TABLE system_log( log_time   DATE,
                         action     VARCHAR2(100),
                         table_name VARCHAR2(50) );

Table created.

-- Order status history table
gSQL>
CREATE TABLE order_status_history( order_id   NUMBER,
                                   old_status VARCHAR2(20),
                                   new_status VARCHAR2(20),
                                   changed_at DATE );

Table created.

-- Administrator notification table
gSQL>
CREATE TABLE admin_notifications( message    VARCHAR2(200),
                                  created_at DATE );

Table created.

-- ORDERS table
gSQL>
CREATE TABLE orders( order_id    NUMBER PRIMARY KEY,
                     customer_id NUMBER,
                     amount      NUMBER,
                     status      VARCHAR2(20),
                     created_at  DATE,
                     updated_at  DATE );

Table created.
```

    - Trigger creation

```
-- DML attempt logging
gSQL>
CREATE OR REPLACE TRIGGER trg_orders_check_before_stmt
BEFORE INSERT OR UPDATE OR DELETE ON orders
DECLARE 
  dml_event VARCHAR(10);
BEGIN
  IF INSERTING THEN
    dml_event := 'INSERT';
  END IF;

  IF UPDATING THEN
    dml_event := 'UPDATE';
  END IF;

  IF DELETING THEN
    dml_event := 'DELETE';
  END IF;

  INSERT INTO system_log VALUES( SYSDATE, dml_event, 'ORDERS' );
END;
/

Trigger created.

-- Automatically set created_at on INSERT
gSQL>
CREATE OR REPLACE TRIGGER trg_orders_set_created_at
BEFORE INSERT ON orders
REFERENCING NEW ROW AS n_row
FOR EACH ROW
BEGIN
  n_row.created_at := NVL(n_row.created_at, SYSDATE);
END;
/

Trigger created.

-- Save history on status changes
gSQL>
CREATE OR REPLACE TRIGGER trg_orders_status_audit
AFTER UPDATE OF status ON orders
REFERENCING OLD ROW AS o_row
            NEW ROW AS n_row            
FOR EACH ROW
WHEN( o_row.status IS DISTINCT FROM n_row.status )
BEGIN
  INSERT INTO order_status_history VALUES (o_row.order_id, o_row.status, n_row.status, SYSDATE);
END;
/

Trigger created.

-- Send notification after status changes
gSQL> 
CREATE OR REPLACE TRIGGER trg_orders_bulk_update_log
AFTER UPDATE ON orders
BEGIN
  INSERT INTO admin_notifications VALUES ('Order status in the ORDERS table has been updated.', SYSDATE);
END;
/

Trigger created.
```

    - DML execution

```
-- BEFORE STATEMENT and BEFORE ROW triggers executed on INSERT
gSQL> 
INSERT INTO orders (order_id, customer_id, amount, status)
VALUES (1, 1001, 50000, 'Order Received ');

1 row created.

gSQL> SELECT * FROM system_log;

LOG_TIME   ACTION TABLE_NAME
---------- ------ ----------
2025-08-08 INSERT ORDERS    

1 row selected.
  
gSQL> SELECT * FROM orders;

ORDER_ID CUSTOMER_ID AMOUNT STATUS          CREATED_AT UPDATED_AT
-------- ----------- ------ --------------- ---------- ----------
       1        1001  50000 Order Received  2025-08-13 null       

1 row selected.

-- BEFORE STATEMENT, AFTER ROW and AFTER STATEMENT triggers executed on UPDATE
gSQL> 
UPDATE orders
   SET status = 'Shipped', updated_at = SYSDATE
 WHERE order_id = 1;

1 row updated.

gSQL> SELECT * FROM system_log;

LOG_TIME   ACTION TABLE_NAME
---------- ------ ----------
2025-08-08 INSERT ORDERS    
2025-08-08 UPDATE ORDERS    

2 rows selected.

gSQL> SELECT * FROM order_status_history;

ORDER_ID OLD_STATUS      NEW_STATUS CHANGED_AT
-------- --------------- ---------- ----------
       1 Order Received  Shipped    2025-08-13

1 row selected.

gSQL> SELECT * FROM admin_notifications;

MESSAGE                                            CREATED_AT
-------------------------------------------------- ----------
Order status in the ORDERS table has been updated. 2025-08-13

1 row selected.

gSQL> SELECT * FROM orders;

ORDER_ID CUSTOMER_ID AMOUNT STATUS  CREATED_AT UPDATED_AT
-------- ----------- ------ ------- ---------- ----------
       1        1001  50000 Shipped 2025-08-13 2025-08-13

1 row selected.
```

- Example of using CALL statement in &lt;trigger body&gt;
    - Table creation

```
gSQL>
CREATE TABLE employees( emp_id NUMBER PRIMARY KEY,
                        name   VARCHAR2(50),
                        salary NUMBER );

Table created.

gSQL> INSERT INTO employees VALUES (1001, 'Alice', 5000);

1 row created.

gSQL> INSERT INTO employees VALUES (1002, 'Bob', 6000);

1 row created.

gSQL> COMMIT;

Commit complete.

gSQL>
CREATE TABLE audit_log( EMP_ID     NUMBER,
                        OLD_SALARY NUMBER,
                        NEW_SALARY NUMBER,
                        CHANGED_AT TIMESTAMP );

Table created.
```

    - Procedure and trigger creation

```
gSQL>
CREATE OR REPLACE PROCEDURE log_salary_change(
		 p_emp_id     IN NUMBER,
         p_old_salary IN NUMBER,
         p_new_salary IN NUMBER )
AS
BEGIN
  INSERT INTO audit_log VALUES( p_emp_id,
                                p_old_salary,
                                p_new_salary,
                                SYSTIMESTAMP );
END;
/

Procedure created.

gSQL>
CREATE OR REPLACE TRIGGER trg_log_salary_change
AFTER UPDATE OF salary ON employees
REFERENCING OLD ROW AS o_row
            NEW ROW AS n_row
FOR EACH ROW
CALL log_salary_change( o_row.emp_id, o_row.salary, n_row.salary );
/

Trigger created.
```

    - DML execution

```
gSQL>
UPDATE employees
   SET salary = 5500
 WHERE emp_id = 1001;

1 row updated.

gSQL> SELECT * FROM audit_log;

EMP_ID OLD_SALARY NEW_SALARY CHANGED_AT                
------ ---------- ---------- --------------------------
  1001       5000       5500 2025-08-08 17:21:35.522820

1 row selected.
```

- Example of using &lt;triggered when clause&gt;
    - Table creation

```
gSQL>
CREATE TABLE employees( emp_id INTEGER PRIMARY KEY,
                        name   VARCHAR(100),
                        salary INTEGER );

Table created.

gSQL> INSERT INTO employees VALUES( 101, 'Alice', 8000 );

1 row created.

gSQL> COMMIT;

Commit complete.

gSQL>
CREATE TABLE salary_log( emp_id     INTEGER,
                         old_salary INTEGER, 
                         new_salary INTEGER,
                         log_time   TIMESTAMP );

Table created.

gSQL> COMMIT;

Commit complete.
```

    - Trigger creation

```
gSQL>
CREATE OR REPLACE TRIGGER trg_log_high_salary
AFTER UPDATE ON employees
REFERENCING OLD ROW AS o_row 
            NEW ROW AS n_row
FOR EACH ROW
WHEN( n_row.salary >= 10000 AND n_row.salary > o_row.salary )
BEGIN
  INSERT INTO salary_log VALUES( o_row.emp_id,
                                 o_row.salary,
                                 n_row.salary,
                                 CURRENT_TIMESTAMP );
END;
/

Trigger created.
```

    - Trigger execution during DML operations

```
-- If the WHEN clause condition is not satisfied → The trigger body is not executed
gSQL> UPDATE employees SET salary = 9000;

1 row updated.

gSQL> SELECT * FROM salary_log;

no rows selected.
```

```
-- If the WHEN clause condition is satisfied → The trigger body is executed
gSQL> UPDATE employees SET salary = 12000;

1 row updated.

gSQL> SELECT * FROM salary_log;

EMP_ID OLD_SALARY NEW_SALARY LOG_TIME                  
------ ---------- ---------- --------------------------
   101       8000      12000 2025-08-08 17:39:38.391413

1 row selected.
```

<a id="7101af265db79e5c"></a>
### Compatibility

**SQL standard compatibility**

<a id="8e087db9fb360590"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T200 | Trigger DDL | O |
| T211 | Basic trigger capability | O |
| T212 | Enhanced trigger capability | O |
| T213 | INSTEAD OF triggers | X |
| T214 | BEFORE triggers | O |
| T215 | AFTER triggers | O |
| T216 | Ability to require true search condition before trigger is invoked | O |
| T217 | TRIGGER privilege | O |
| T218 | Multiple triggers for the same event executed in the order created | O |

<a id="85a0e3a5a82510b1"></a>
### For More Information

Refer to the following.

- [ALTER TRIGGER name COMPILE](#d86df859bc319efc)
- [ALTER TRIGGER name ENABLE/DISABLE](#87a5b7084ef9f6ba)
- [ALTER TRIGGER name RENAME TO](#7a2a65b5c770fb59)
- [ALTER TABLE name SET TRIGGER ORDER](../part-03-sql-manual/18-sql-references-a-b.md#24a95716d0044b84)
- [DROP TRIGGER](#c5e9e28a6d05bf8b)
- [DROP TABLE](../part-03-sql-manual/19-sql-references-c-g.md#5324bfcd0073e53b)

<a id="c7cbdaa712da2629"></a>
## DROP FUNCTION

<a id="410bcfb6a853e49a"></a>
### Function

It drops a function.

<a id="f6611dfe73f4ca53"></a>
### Syntax

```
<drop function statement> ::=
    DROP FUNCTION [ IF EXISTS ] func_name
    ;
```

<a id="df75038f0e73d172"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop function statement&gt;.

- The owner of that function
- (DROP PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the function belongs
- DROP ANY PROCEDURE ON DATABASE

<a id="9f14113d307f0f86"></a>
### Syntax Rules and Parameters

<a id="51df9376c524c1d1"></a>
#### IF EXISTS

Even when the function does not exist, an error does not occur.

<a id="3f4e140e068908dd"></a>
#### FUNC NAME

It is the function name to be dropped.  
It can define the schema to which the function belongs, such as schema_name.func_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="3c8a18110be56b02"></a>
### Description

It drops a specified schema-level function.

<a id="b8b15453694041a3"></a>
### Examples

```
gSQL> CREATE OR REPLACE FUNCTION FUNC1
RETURN INTEGER
 IS
    V1 INTEGER;
  BEGIN
    V1 := 10;
    RETURN V1;
  END;
  /

Function created.


COMMIT;

Commit complete.
gSQL> DROP FUNCTION FUNC1;

Function dropped.
```

<a id="eacabbedf03e2670"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="fbea67c4c6e5305d"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="d9e1a688d73f5f25"></a>
### For More Information

Refer to the following.

- [CREATE FUNCTION](#8343c001bfba29fc)
- [ALTER FUNCTION](#5568841efba34448)

<a id="ac5c19f8f617c881"></a>
## DROP LIBRARY

<a id="a815496c83d0045f"></a>
### Function

It drops a library.

<a id="24ad085a6aa925ee"></a>
### Syntax

```
<drop library statement> ::=
    DROP LIBRARY [ IF EXISTS ] <library name>
    ;
```

<a id="e3a737d78062f21f"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop library statement&gt;.

- The owner of that library
- DROP LIBRARY ON SCHEMA or CONTROL SCHEMA ON SCHEMA for the schema to which the library belongs
- DROP ANY LIBRARY ON DATABASE

<a id="80780c94da6d0854"></a>
### Syntax Rules and Parameters

<a id="36f3ad5046babeff"></a>
#### IF EXISTS

Even when the library does not exist, an error does not occur.

<a id="40328ce29e72aa8e"></a>
#### library name

It is the library name to be dropped.  
It can define the schema to which the library belongs, such as &lt;schema name&gt;.&lt;library name&gt;. If &lt;schema name&gt; is omitted, the default schema name of the user performing the statement is used.

<a id="53bd2044fb4c81e0"></a>
### Description

It drops a specified library.

<a id="77f2555e94150017"></a>
### Examples

```
gSQL>
CREATE LIBRARY lib1 AS 'add.so';
/

Library created.

gSQL> DROP LIBRARY lib1;

Library dropped.

gSQL> DROP LIBRARY IF EXISTS lib2;

Library dropped.
```

<a id="b17ec4d6849d35db"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="5a85e5653840f943"></a>
### For More Information

Refer to [CREATE LIBRARY](#d3c4a1abc483c544).

<a id="12916c88f352e944"></a>
## DROP PACKAGE

<a id="17e544c0cccf28bc"></a>
### Function

It drops a package (of only body or both spec/ body).

<a id="5070d06b8ead4311"></a>
### Syntax

```
<drop package statement> ::=
    DROP PACKAGE [BODY] [ IF EXISTS ] package_name
    ;
```

<a id="f4b35cd976c1e055"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop package statement&gt;.

- The owner of that package 
- (DROP PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
- DROP ANY PACKAGE ON DATABASE

<a id="73814d1dba9effb8"></a>
### Syntax Rules and Parameters

<a id="2664d6c4edb932f1"></a>
#### BODY

It drops only the body object in the package of the given name. If the keyword *BODY* is not specified it drops both the package specification and the body.

<a id="29a65694ef3c25fc"></a>
#### IF EXISTS

Even when the package does not exist, an error does not occur.

<a id="c3e78c24a6dd141e"></a>
#### PACKAGE NAME

It is the package name to be dropped.  
It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="535b33cc80203f1c"></a>
### Description

It drops the specified package object.

<a id="1dd378cacd9a60c8"></a>
### Examples

```
CREATE PACKAGE PKG1
  IS
    V1 INTEGER;
    FUNCTION FUNC1 (A1 INTEGER) RETURN INTEGER;
  END;
  /

Package created.

DROP PACKAGE IF EXISTS PKG1;

Package dropped.
```

<a id="5167b9f6843f55bc"></a>
### Compatibility

It is DRO MODULE statement in the SQL standard.

<a id="715bcd54019b509e"></a>
### For More Information

Refer to the following.

- [CREATE PACKAGE](#d67c80375fa9e3c8)
- [CREATE PACKAGE BODY](#397f0c3a716022e0)
- [ALTER PACKAGE](#ed764dabc1cf7118)

<a id="edab1b4697fec9a3"></a>
## DROP PROCEDURE

<a id="cda349878279daab"></a>
### Function

It drops a procedure.

<a id="7854e3a87defe40f"></a>
### Syntax

```
<drop procedure statement> ::=
    DROP PROCEDURE [ IF EXISTS ] proc_name
    ;
```

<a id="813607f38305bd3a"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop procedure statement&gt;.

- The owner of that procedure
- (DROP PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- DROP ANY PROCEDURE ON DATABASE

<a id="3bd4a3ca2d008541"></a>
### Syntax Rules and Parameters

<a id="21dddf19bf0d962c"></a>
#### IF EXISTS

Even when the procedure does not exist, an error does not occur.

<a id="256a846f6e365599"></a>
#### PROC NAME

It is the procedure name to be dropped.  
It can define the schema to which the procedure belongs, such as schema_name.proc_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="6746b8991f93c398"></a>
### Description

It drops a specified schema-level procedure.

<a id="13d9fa5564329d4e"></a>
### Examples

```
gSQL> CREATE OR REPLACE PROCEDURE PROC1( A1 INTEGER, A2 INTEGER )
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

Procedure created.


COMMIT;

Commit complete.


gSQL> DROP PROCEDURE PROC1;

Procedure dropped.
```

<a id="7b8121a562f96070"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="eaca1765c0929301"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="c757eabe1a72124f"></a>
### For More Information

Refer to the following.

- [CREATE PROCEDURE](#d439613cbc283235)
- [ALTER PROCEDURE](#066771bec4083e3c)

<a id="c5e9e28a6d05bf8b"></a>
## DROP TRIGGER

<a id="3502850bd93b68fd"></a>
### Function

It drops a trigger.

<a id="2e4d100c1aa1449e"></a>
### Syntax

```
<drop trigger statement> ::=
    DROP TRIGGER [ IF EXISTS ] <trigger name>
    ;
```

<a id="646b561e8b60c376"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop trigger statement&gt;.

- The owner of that trigger
- (DROP TRIGGER or CONTROL SCHEMA) ON SCHEMA for the schema to which the trigger belongs
- DROP ANY TRIGGER ON DATABASE

<a id="f19691cff90764f6"></a>
### Syntax Rules and Parameters

<a id="4d6234edf9fb3209"></a>
#### IF EXISTS

Even when the trigger does not exist, an error does not occur.

<a id="a9f8185a0f22ba2f"></a>
#### &lt;trigger name&gt;

It is a name of trigger to be dropped.   
It can define the schema to which the trigger belongs, such as schema_name.trigger_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="69016525f67311c3"></a>
### Description

It drops the specified trigger.  
If the event table is dropped using [DROP TABLE](../part-03-sql-manual/19-sql-references-c-g.md#5324bfcd0073e53b), the corresponding trigger is also dropped.

<a id="9a096a5032d7abf0"></a>
### Examples

```
gSQL>
CREATE OR REPLACE TRIGGER trg_orders_status_audit
AFTER UPDATE OF status ON orders
REFERENCING OLD ROW AS o_row
            NEW ROW AS n_row            
FOR EACH ROW
WHEN( o_row.status IS DISTINCT FROM n_row.status )
BEGIN
  INSERT INTO order_status_history VALUES (o_row.order_id, o_row.status, n_row.status, SYSDATE);
END;
/

Trigger created.

gSQL> DROP TRIGGER trg_orders_status_audit;

Trigger dropped.
```

<a id="57421af4f0e9eddc"></a>
### Compatibility

**SQL standard compatibility**

<a id="7b2a785a43947f0a"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T200 | Trigger DDL | O |

<a id="6db537cf48ae54ee"></a>
### For More Information

Refer to the following.

- [CREATE TRIGGER](#44e30f425949fd8e)
- [ALTER TRIGGER name COMPILE](#d86df859bc319efc)
- [ALTER TRIGGER name ENABLE/DISABLE](#87a5b7084ef9f6ba)
- [ALTER TRIGGER name RENAME TO](#7a2a65b5c770fb59)
- [DROP TABLE](../part-03-sql-manual/19-sql-references-c-g.md#5324bfcd0073e53b)

---

[← 30. PSM Language Element References](30-psm-language-element-references.md) · [Table of contents](../README.md) · [32. Built-in Package →](32-built-in-package.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
