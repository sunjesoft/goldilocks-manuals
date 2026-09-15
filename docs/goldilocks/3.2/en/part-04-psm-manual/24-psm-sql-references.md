<a id="19d17c1a159c5123"></a>

# 24. PSM SQL References

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/19d17c1a159c5123)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 23. PSM Language Element References](23-psm-language-element-references.md) · [Table of contents](../README.md) · [25. ODBC →](../part-05-developer-manual/25-odbc.md)

<a id="baf1588e5c178990"></a>
## ALTER FUNCTION

<a id="44e841eef975fc18"></a>
### Function

It compiles a function again.

<a id="8443e1331c0876a3"></a>
### Syntax

```
<alter function statement> ::=
    ALTER FUNCTION function_name COMPILE
    ;
```

<a id="70ee289dea234d4e"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter function statement&gt;.

- The owner of that function
- (ALTER PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the function belongs
- ALTER ANY PROCEDURE ON DATABASE

<a id="3659020d586603a0"></a>
### Syntax Rules and Parameters

- function Name
    - It is the function name to be compiled.
    - It can define the schema to which the function belongs, such as schema_name.func_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="49a768dfac574963"></a>
### Description

It compiles a specified schema-level function again.

<a id="c81a9ef80b39a1a8"></a>
### Examples

```
gSQL> ALTER FUNCTION FUNC1 COMPILE;

Function altered.
```

<a id="58c76546c2ebe701"></a>
### Compatibility

It is a statement altering characteristics specified when performing CREATE in the SQL standard, and astatement recreating a plan of a function in GOLDILOCKS.

**SQL standard compatibility**

<a id="4a7cdca879605b00"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="e3eed5ebe9492760"></a>
### For More Information

Refer to the followings.

- [CREATE FUNCTION](#21b6c80060dfcc44)
- [DROP FUNCTION](#aec5d4c01f2a2c6d)

<a id="44b3febc407216fc"></a>
## ALTER PROCEDURE

<a id="3978008570f137b2"></a>
### Function

It compiles a procedure again.

<a id="7eb574763c99df4b"></a>
### Syntax

```
<alter procedure statement> ::=
    ALTER PROCEDURE proc_name COMPILE
    ;
```

<a id="12531f31ea9afd7d"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter procedure statement&gt;.

- The owner of that procedure
- (ALTER PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- ALTER ANY PROCEDURE ON DATABASE

<a id="ce6a99fb7d6fd2c8"></a>
### Syntax Rules and Parameters

- Proc Name
    - It is the procedure name to be compiled.
    - It can define the schema to which the procedure belongs, such as schema_name.proc_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="e6e9eab60414206b"></a>
### Description

It compiles a specified schema-level procedure again.

<a id="4a07c3abc6a82a09"></a>
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

<a id="2e913be58b0abc14"></a>
### Compatibility

It is a statement altering characteristics specified when performing CREATE in the SQL standard, and astatement recreating a plan of a procedure in GOLDILOCKS.

**SQL standard compatibility**

<a id="5a3a3f36c47be7b4"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="9165bba3342a349e"></a>
### For More Information

Refer to the followings.

- [CREATE PROCEDURE](#730491b1fd9dfcc3)
- [DROP PROCEDURE](#8c112cc6728145b1)

<a id="a5f9ce4650e1b317"></a>
## CALL Statement

<a id="0fbbc26a06889a2c"></a>
### Function

It performs a schema-level procedure or a function.

<a id="81ef78fb39d3d023"></a>
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

<a id="208620d00f6dc278"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;call statement&gt;.

- The EXECUTE privilege for that procedure
- (EXECUTE PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- EXECUTE ANY PROCEDURE ON DATABASE

<a id="cbc78767544826f9"></a>
### Syntax Rules and Parameters

- proc_name
    - It is a name of a procedure/ function to be executed.
    - It may includes a schema to which the procedure belongs such as Schema_name.Proc_name.
- value_expr
    - It expresses an argument value which were transferred to the procedure. It can use a bind parameter such as '?' or ':V1'.

<a id="7a99626ed0df4861"></a>
### Description

It executes a schema-level SQL procedure or a function by using specified arguments.

A function of &lt;sql call statement&gt; form returns the result value by using a host variable expression or a dynamic bind parameter (?) after INTO clause.

&lt;odbc procedure call escape sequence&gt; form is a standard statement to call PROCEDURE in ODBC/ JDBC, and GOLDILOCKS supports this statement in a server. (It can also be used in a tool such as gsql.) A function returns the result value by using assign expressions ( ? = ) at the front.

<a id="368f4115bad2fbe5"></a>
### Examples

<a id="fe995c2154cae74f"></a>
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

<a id="27c814fffa2936e1"></a>
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

<a id="96bc113ef6010305"></a>
### Compatibility

The SQL standard allows only the call for a PROCEDURE, so it does not define below [INTO] clause.

<a id="21b6c80060dfcc44"></a>
## CREATE FUNCTION

<a id="c8824ff6be0f686d"></a>
### Function

It defines a schema-level function.

<a id="33a4f35282ef630c"></a>
### Syntax

```
<create procedure statement> ::=
    CREATE [ OR REPLACE ]  
        FUNCTION func_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
        RETURN datatype
        [ <func_characteristics> ]
        { IS | AS } <item_declaration> BEGIN <pl_stmt_list> END
    ;

<func_characteristics> ::=
    DETERMINISTIC | AUTHID CURRENT_USER | AUTHID DEFINER
```

<a id="7b6734c0eaff01fa"></a>
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

<a id="c4047f69c665edaa"></a>
### Syntax Rules and Parameters

<a id="29a0e70a0a25ce4a"></a>
#### OR REPLACE

It replaces an existing function when the function already exists.

<a id="454b729750be1fe7"></a>
#### FUNCTION NAME

It is a name of function to be created, and it should be a unique name in a schema.  
It can define the schema to which the function belongs, such as schema_name.func_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of a function name should be shorter than 128 bytes.

<a id="23e8a6e28ff3f7c7"></a>
#### PARAM NAME

It defines a name of an argument to be used in a function.  
The name of each argument should be unique in a function.  
The length of each argument name should be shorter than 128 bytes.  
It does not limit the maximum number of an argument to be used in a single function.

<a id="fc7a00147465e830"></a>
#### Bind Type

It specifies a bind type of each argument.  
If it is not specified, the default type is IN.

<a id="f0033ecc24fe963b"></a>
#### Func_Characteristics

It defines options to perform a function. It should be specified only once per a single item.

- DETERMINISTIC: The function always returns the same result value when the same argument values are input.
- AUTHID CURRENT_USER: SQLs which are being performed during performing a function are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing a function are interpreted and performed according to an authorization of a definer.

<a id="4a34fc72a3dbb9d4"></a>
#### Item Declaration

It declares items such as a local variable to be used within a function.  
It can declare all items which can be declared in a PL block.

<a id="b5d2a9b98b056fc9"></a>
#### PL Stmt List

It is a body section of a function, and it lists PL statements to be performed.  
It can not use a bind parameter such as '?' or ':V1'. within a function.

<a id="54b5e833fb79a180"></a>
### Description

It defines a schema-level SQL function. The created fucntion can be called from all expressions.

The definition of a function can be viewed in ROUTINES table of INFORMATION_SCHEMA. The definition of a function parameter can be viewed in PARAMETERS table of INFORMATION_SCHEMA.

If a function becomes temporarily unstable due to absences of related objects, then it can try to recreate a plan by using &lt;alter function&gt; statement.

The created function can be dropped by using &lt;drop function&gt; statement.  
The maximum number of functions to be created is not limited. Therefore, they can be created as many as the storage space is available.

<a id="0ea1156c26cfc2c1"></a>
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

<a id="5403975ca44ca69f"></a>
### Compatibility

The SQL standard does not define OR REPLACE clause.

**SQL standard compatibility**

<a id="838ba7063f532a9f"></a>
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
| T326 | Table functions | X |
| T651 | SQL-schema statements in SQL routines | X |
| T652 | SQL-dynamic statements in SQL routines | O |
| T653 | SQL-schema statements in external routines | X |
| T654 | SQL-dynamic statements in external routines | X |
| T655 | Cyclically dependent routines | X |
| T272 | Enhanced savepoint management | X |
| T522 | Default values for IN parameters of SQL-invoked procedures | O |
| B121 | Routine language Ada | X |
| B122 | Routine language C | X |
| B123 | Routine language COBOL | X |
| B124 | Routine language Fortran | X |
| B125 | Routine language MUMPS | X |
| B126 | Routine language Pascal | X |
| B127 | Routine language PL/I | X |
| B128 | Routine language SQL | O |
| B129 | Routine language Ada: VARCHAR and NUMERIC support | X |

<a id="1adb280c93e437dd"></a>
### For More Information

Refer to the followings.

- [DROP FUNCTION](#aec5d4c01f2a2c6d)
- [ALTER FUNCTION](#baf1588e5c178990)

<a id="730491b1fd9dfcc3"></a>
## CREATE PROCEDURE

<a id="8f0d00d65d761cc6"></a>
### Function

It defines a schema-level procedure.

<a id="2453c015414699f1"></a>
### Syntax

```
<create procedure statement> ::=
    CREATE [ OR REPLACE ]  
        PROCEDURE proc_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
        [ <proc_characteristics> ]
        { IS | AS } <item_declaration> BEGIN <pl_stmt_list> END
    ;

<proc_characteristics> ::=
    AUTHID CURRENT_USER | AUTHID DEFINER
```

<a id="b63a3af5d24d7bba"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;create procedure statement&gt;.

- One of the following privileges is required to create a procedure.
    - (CREATE PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
    - CREATE ANY PROCEDURE ON DATABASE 
- If a procedure already exists when using OR REPLACE clause, then one of the following privileges dropping the existing procedure is required.
    - The owner of that procedure
    - (DROP PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
    - DROP ANY PROCEDURE ON DATABASE
- The user who performed the statement becomes the owner of the created procedure.

<a id="7e19a78c1a33e522"></a>
### Syntax Rules and Parameters

<a id="1907b50c34c53715"></a>
#### OR REPLACE

It replaces an existing procedure when the procedure already exists.

<a id="75ef017d596168b0"></a>
#### PROC NAME

It is a name of procedure to be created, and it should be a unique name in a schema.  
It can define the schema to which the procedure belongs, such as schema_name.proc_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of a procedure name should be shorter than 128 bytes.

<a id="3946d01171770ff8"></a>
#### PARAM NAME

It defines a name of an argument to be used in a procedure.  
The name of each argument should be unique in a procedure.  
The length of each argument name should be shorter than 128 bytes.  
It does not limit the maximum number of an argument to be used in a single procedure.

<a id="16b3ca3780c3f9d6"></a>
#### Bind Type

It specifies a bind type of each argument.  
If it is not specified, the default type is IN.

<a id="6f8bbacd0f6fc562"></a>
#### proc_characteristics

It defines options to perform a procedure. It should be specified only once per a single item.

- AUTHID CURRENT_USER: SQLs which are being performed during performing a procedure are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing a procedure are interpreted and performed according to an authorization of a definer.

<a id="efb2b84757933899"></a>
#### Item Declaration

It declares items such as a local variable to be used within a procedure.  
It can declare all items which can be declared in a PL block.

<a id="54db78a2a07d6a47"></a>
#### PL Stmt List

It is a body section of a procedure, and it lists PL statements to be performed.  
It can not use a bind parameter such as '?' or ':V1'. within a procedure.

<a id="90b14615acf743cf"></a>
### Description

It defines a schema-level SQL procedure. The created procedure can be called from CALL statement, anonymous block, or other procedure/ function.

The definition of a procedure can be viewed in ROUTINES table of INFORMATION_SCHEMA. The definition of a procedure parameter can be viewed in PARAMETERS table of INFORMATION_SCHEMA.

If a procedure becomes temporarily unstable due to absences of related objects, then it can try to recreate a plan by using &lt;alter procedure&gt; statement.

The created procedure can be dropped by using &lt;drop procedure&gt; statement.  
The maximum number of procedures to be created is not limited. Therefore, they can be created as many as the storage space is available.

<a id="90f0c6710fa7ec14"></a>
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

<a id="e998f8f2d4fa7a80"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="cf69b0c5ec31b290"></a>
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
| T326 | Table functions | X |
| T651 | SQL-schema statements in SQL routines | X |
| T652 | SQL-dynamic statements in SQL routines | O |
| T653 | SQL-schema statements in external routines | X |
| T654 | SQL-dynamic statements in external routines | X |
| T655 | Cyclically dependent routines | X |
| T272 | Enhanced savepoint management | X |
| T522 | Default values for IN parameters of SQL-invoked procedures | O |
| B121 | Routine language Ada | X |
| B122 | Routine language C | X |
| B123 | Routine language COBOL | X |
| B124 | Routine language Fortran | X |
| B125 | Routine language MUMPS | X |
| B126 | Routine language Pascal | X |
| B127 | Routine language PL/I | X |
| B128 | Routine language SQL | O |
| B129 | Routine language Ada: VARCHAR and NUMERIC support | X |

<a id="87dc7b9e11f4ceb5"></a>
### For More Information

Refer to the followings.

- [DROP PROCEDURE](#8c112cc6728145b1)
- [ALTER PROCEDURE](#44b3febc407216fc)

<a id="aec5d4c01f2a2c6d"></a>
## DROP FUNCTION

<a id="aa88a217ca0355ea"></a>
### Function

It drops a function.

<a id="674dc72b54e6bd08"></a>
### Syntax

```
<drop function statement> ::=
    DROP FUNCTION [ IF EXISTS ] func_name
    ;
```

<a id="514a86e1d55c8189"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop function statement&gt;.

- The owner of that function
- (DROP PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the function belongs
- DROP ANY PROCEDURE ON DATABASE

<a id="138ecd6fd2ad6808"></a>
### Syntax Rules and Parameters

<a id="e8990d099a1b8c00"></a>
#### IF EXISTS

Even when the function does not exist, an error does not occur.

<a id="9491a23d183e55ac"></a>
#### FUNC NAME

It is the function name to be dropped.  
It can define the schema to which the function belongs, such as schema_name.func_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="3918c8d0f032a35a"></a>
### Description

It drops a specified schema-level function.

<a id="69407e31bfda3728"></a>
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

<a id="86e1fc60073f376a"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="e339547f4cfd8286"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="37a23ab2f62173b3"></a>
### For More Information

Refer to the followings.

- [CREATE FUNCTION](#21b6c80060dfcc44)
- [ALTER FUNCTION](#baf1588e5c178990)

<a id="8c112cc6728145b1"></a>
## DROP PROCEDURE

<a id="95e7a89c2354f888"></a>
### Function

It drops a procedure.

<a id="14c5b1b3ae1306f4"></a>
### Syntax

```
<drop procedure statement> ::=
    DROP PROCEDURE [ IF EXISTS ] proc_name
    ;
```

<a id="def56249e0d9e750"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop procedure statement&gt;.

- The owner of that procedure
- (DROP PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- DROP ANY PROCEDURE ON DATABASE

<a id="b0076781261bb634"></a>
### Syntax Rules and Parameters

<a id="b7735ab6138ba7ef"></a>
#### IF EXISTS

Even when the procedure does not exist, an error does not occur.

<a id="30594035c1302212"></a>
#### PROC NAME

It is the procedure name to be dropped.  
It can define the schema to which the procedure belongs, such as schema_name.proc_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="58572e009b193449"></a>
### Description

It drops a specified schema-level procedure.

<a id="a8d4831f2d83e55b"></a>
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

<a id="f875eba06b5fbc73"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="3464642e3e23c1a3"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="68566187616d063b"></a>
### For More Information

Refer to the followings.

- [CREATE PROCEDURE](#730491b1fd9dfcc3)
- [ALTER PROCEDURE](#44b3febc407216fc)

---

[← 23. PSM Language Element References](23-psm-language-element-references.md) · [Table of contents](../README.md) · [25. ODBC →](../part-05-developer-manual/25-odbc.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
