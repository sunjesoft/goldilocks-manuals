<a id="866ac7ce70382841"></a>

# 29. PSM SQL References

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/866ac7ce70382841)  
> Tag: `22c.1_10_tag`

[← 28. PSM Language Element References](28-psm-language-element-references.md) · [Table of contents](../README.md) · [30. Database Connection →](../part-05-developer-manual/30-database-connection.md)

<a id="14b653d0765ad6d0"></a>
## ALTER FUNCTION

<a id="4d9fde682567e6cf"></a>
### Function

It recompiles a function.

<a id="97e6fa34b5f721d7"></a>
### Syntax

```
<alter function statement> ::=
    ALTER FUNCTION function_name COMPILE
    ;
```

<a id="2c87e0a0a59f6157"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter function statement&gt;.

- The owner of that function
- (ALTER PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the function belongs
- ALTER ANY PROCEDURE ON DATABASE

<a id="8580369a8f56da85"></a>
### Syntax Rules and Parameters

- function Name
    - It is the function name to be compiled.
    - It can define the schema to which the function belongs, such as schema_name.func_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="25a8c03b39c38556"></a>
### Description

It recompiles a specified schema-level function.

<a id="ab4e6077422603ee"></a>
### Examples

```
gSQL> ALTER FUNCTION FUNC1 COMPILE;

Function altered.
```

<a id="802237cbeb5625ed"></a>
### Compatibility

It is a statement altering characteristics specified when performing CREATE in the SQL standard, and astatement recreating a plan of a function in GOLDILOCKS.

**SQL standard compatibility**

<a id="83ab1636dc86b55f"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="fe8a56a364a2e631"></a>
### For More Information

Refer to the followings.

- [CREATE FUNCTION](#40ab839511f9caec)
- [DROP FUNCTION](#3f3a2b64579299ef)

<a id="d8b3f433e46b0333"></a>
## ALTER PACKAGE

<a id="2b4479bc49068f44"></a>
### Function

It recompiles a package.

<a id="e8fcd70d21513493"></a>
### Syntax

```
<alter package statement> ::=
    ALTER PACKAGE package_name <package compile clause>
    ;

<package compile clause> ::=
    COMPILE [PACKAGE|SPECIFICATION|BODY]
```

<a id="1c7eae56285af031"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter package statement&gt;.

- The owner of that package
- (ALTER PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs 
- ALTER ANY PACKAGE ON DATABASE

<a id="720f3920f1be18d4"></a>
### Syntax Rules and Parameters

- Package name
    - It is a name of package to be compiled.
    - It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

- Package compile clause
    - PACKAGE: It recompiles both the specification and the body. (Default)
    - SPECIFICATION: It recompiles only the specification.
    - BODY: It recompiles only the body.

<a id="10cdc2b16667dc8c"></a>
### Description

It recompiles the specified package.  
The execution code of the compiled package is stored in the plan cache.

<a id="81b6644c86f3889e"></a>
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

<a id="26e22d494a4b2bb5"></a>
### Compatibility

It is ALTER MODULE statement in the SQL standard.

<a id="78417e09c3159bfc"></a>
### For More Information

Refer to the followings.

- [CREATE PACKAGE](#24f22bbbebed2d3b)
- [CREATE PACKAGE BODY](#57d0eac936305ba6)
- [DROP PACKAGE](#8644d4a6d3387eef)

<a id="93ff8d3e64fbbae1"></a>
## ALTER PROCEDURE

<a id="ba11f4a059df0e47"></a>
### Function

It recompiles a procedure.

<a id="1220b7909f2377da"></a>
### Syntax

```
<alter procedure statement> ::=
    ALTER PROCEDURE proc_name COMPILE
    ;
```

<a id="27f52d9fb88942b4"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter procedure statement&gt;.

- The owner of that procedure
- (ALTER PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- ALTER ANY PROCEDURE ON DATABASE

<a id="3271e0874d34b590"></a>
### Syntax Rules and Parameters

- Proc Name
    - It is the procedure name to be compiled.
    - It can define the schema to which the procedure belongs, such as schema_name.proc_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="bd0b47da6799a23c"></a>
### Description

It recompiles a specified schema-level procedure.

<a id="cc22b89713e433a4"></a>
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

<a id="08943e2b6205b99e"></a>
### Compatibility

It is a statement altering characteristics specified when performing CREATE in the SQL standard, and astatement recreating a plan of a procedure in GOLDILOCKS.

**SQL standard compatibility**

<a id="52e510835a864ee6"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="5d922f1bf9a5ab8b"></a>
### For More Information

Refer to the followings.

- [CREATE PROCEDURE](#acd5825880480a80)
- [DROP PROCEDURE](#e555d2b555faabee)

<a id="6fc0291e0821a481"></a>
## CALL Statement

<a id="9eaadd290d36bdb0"></a>
### Function

It performs a schema-level procedure or a function.

<a id="060a5532bdb56aea"></a>
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

<a id="ae8ba6e0d1f6eb2b"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;call statement&gt;.

- The EXECUTE privilege for that procedure
- (EXECUTE PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- EXECUTE ANY PROCEDURE ON DATABASE

<a id="c4273f7df99eea29"></a>
### Syntax Rules and Parameters

- proc_name
    - It is a name of a procedure/ function to be executed.
    - It may includes a schema to which the procedure belongs such as Schema_name.Proc_name.
- value_expr
    - It expresses an argument value which were transferred to the procedure. It can use a bind parameter such as '?' or ':V1'.

<a id="f3a7fb75b96595ee"></a>
### Description

It executes a schema-level SQL procedure or a function by using specified arguments.

A function of &lt;sql call statement&gt; form returns the result value by using a host variable expression or a dynamic bind parameter (?) after INTO clause.

&lt;odbc procedure call escape sequence&gt; form is a standard statement to call PROCEDURE in  ODBC/ JDBC, and GOLDILOCKS supports this statement in a server. (It can also be used in a tool such as gsql.) A function returns the result value by using assign expressions ( ? = ) at the front.

<a id="77d9f007a97767b2"></a>
### Examples

<a id="752bfa9719a0fc32"></a>
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

<a id="7de9dc9df5f3cb69"></a>
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

<a id="e3ab583aa570034b"></a>
### Compatibility

The SQL standard allows only the call for a PROCEDURE, so it does not define below [INTO] clause.

<a id="40ab839511f9caec"></a>
## CREATE FUNCTION

<a id="f6f04010e9505ca0"></a>
### Function

It defines a schema-level function.

<a id="6bc9b15bc711a00b"></a>
### Syntax

```
<create function statement> ::= 
    CREATE [ OR REPLACE ] FUNCTION <function name> [ ( <parameter list> ) ]
       <return clause> 
       [ <function characteristics> ] 
       { IS | AS }  
       <item declaration>  
       BEGIN 
       <pl statement list> 
       END [ <function name> ]
    ; 

<parameter list> ::= 
      <parameter name> [ <parameter mode> ] <datatype> [ <parameter default> ] [ , ... ] 
 
<parameter mode> ::= 
      IN 
    | OUT 
    | IN OUT 
 
<parameter default> ::= 
      { := | DEFAULT } <value expression> 
 
<return clause> ::= 
      RETURN <datatype> 
    | RETURN TABLE ( <table function column list> ) 
 
<table function column list> ::=  
      <column name> <datatype> [ , ... ] 
 
<function characteristics> ::= 
      DETERMINISTIC 
    | AUTHID CURRENT_USER 
    | AUTHID DEFINER
```

<a id="eefb4d5da4fad38c"></a>
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

<a id="1fdb1a9bead3c86c"></a>
### Syntax Rules and Parameters

<a id="b7c3b51a7f17bb79"></a>
#### OR REPLACE

It replaces an existing function with a new function when the function already exists.

<a id="7de8f88291dd14c6"></a>
#### function name

It is a name of function to be created, and it should be a unique name in a schema.  
It can define the schema to which the function belongs, such as schema_name.function_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of a function name should be shorter than 128 bytes.

<a id="24beb7a540daa998"></a>
#### parameter name

It defines a parameter name of the function.   
The name of each parameter should be unique in a function.   
In other words, the function's parameter and PL item can not have the same name.   
The length of a parameter name should be shorter than 128 bytes.   
The maximum number of parameters available in a single function is limitless.

<a id="ac33184dae694247"></a>
#### parameter mode

It sets each parameter mode.   
The parameter modes are IN, OUT, and IN OUT.  
If the parameter mode is not specified, the default mode is *IN*.

<a id="f776756233920037"></a>
#### parameter default

It is the default value of the parameter.  
The parameter with the specified parameter default can be omitted when executing the function.   
If the parameter is not specified but omitted, then the default value is &lt;value expression&gt; specified when defining the parameter.  
The datatype of &lt;value expression&gt; should be the datatype of the parameter.  
All parameters defined after the parameter having &lt;parameter default&gt; should have &lt;parameter default&gt;.

<a id="5732928e42fe5dc2"></a>
#### return clause

It defines the return type of the function.   
It is defined as follows in &lt;return clause&gt;.

- RETURN &lt;datatype&gt;
    - It defines the datatype of the return value returned by the function.
- RETURN TABLE ( &lt;table function column list&gt; )
    - It defines the table type of the returned result set.

<a id="4d7817990ed52102"></a>
#### table function column list

It is the column name of the result set returned by the table function.  
The length of a column name should be shorter than 128 bytes.  
The number of columns are limitless.  
Each column name is unique in &lt;table function column list&gt;.  
The column name can be as same as the parameter name and the declare item name.  
The column defined in &lt;table function column list&gt; can not be referenced in PL block of the function.

<a id="a74a4c37b1665a3a"></a>
#### function characteristics

It defines options to perform a function. It should be specified only once per a single item.

- DETERMINISTIC: The function always returns the same result value when the same argument values are input.
- AUTHID CURRENT_USER: SQLs which are being performed during performing a function are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing a function are interpreted and performed according to an authorization of a definer.

<a id="9557371ea8672540"></a>
#### Item Declaration

It declares items such as a local variable to be used within a function.  
It can declare all items which can be declared in a PL block.

<a id="faefedf3549a029c"></a>
#### PL Stmt List

It is a body section of a function, and it lists PL statements to be performed.  
It can not use a bind parameter such as '?' or ':V1'. within a function.

<a id="bcaa74899439db4c"></a>
### Description

It defines a schema-level SQL function. The created fucntion can be called from all expressions.

The definition of a function can be viewed in ROUTINES table of INFORMATION_SCHEMA. The definition of a function parameter can be viewed in PARAMETERS table of INFORMATION_SCHEMA.

If a function becomes temporarily unstable due to absences of related objects, then it can try to recreate a plan by using [ALTER FUNCTION](#14b653d0765ad6d0) statement.

The created function can be dropped by using [DROP FUNCTION](#3f3a2b64579299ef) statement.  
The maximum number of functions to be created is not limited. Therefore, they can be created as many as the storage space is available.

<a id="efaf30eb2efb4692"></a>
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

<a id="a5bfb28116b87faa"></a>
### Compatibility

The SQL standard does not define OR REPLACE clause.

**SQL standard compatibility**

<a id="b9d22e67a1cf0998"></a>
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
| B122 | Routine language C | X |
| B123 | Routine language COBOL | X |
| B124 | Routine language Fortran | X |
| B125 | Routine language MUMPS | X |
| B126 | Routine language Pascal | X |
| B127 | Routine language PL/I | X |
| B128 | Routine language SQL | O |
| B129 | Routine language Ada: VARCHAR and NUMERIC support | X |

<a id="7ea73e23f9f337d4"></a>
### For More Information

Refer to the followings.

- [DROP FUNCTION](#3f3a2b64579299ef)
- [ALTER FUNCTION](#14b653d0765ad6d0)

<a id="24f22bbbebed2d3b"></a>
## CREATE PACKAGE

<a id="1f90f43f3f0eee25"></a>
### Function

It defines the spec about public items to be used in a package.

<a id="6427a111dd7db3d9"></a>
### Syntax

```
<create package statement> ::=
    CREATE [ OR REPLACE ]  
        PACKAGE package_name 
        [ <package_characteristics> ]
        { IS | AS }
       <item_declaration> 
    END
    ;

<package_characteristics> ::=
    AUTHID CURRENT_USER | AUTHID DEFINER

<item_declaration> ::=    <variable declaration> 
                        | <cursor declaration>
                        | <user-defined type declaration> 
                        | <function declaration> 
                        | <procedure declaration> 
                        | <user exception declaration>
                        | <cursor definition>
```

<a id="300f45a0d8fbd698"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;create package statement&gt;.

- One of the following privileges is required to create a package.
    - (CREATE PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
    - CREATE ANY PACKAGE ON DATABASE
- If a package already exists when using OR REPLACE clause, then one of the following privileges dropping the existing package is required.
    - The owner of that package
    - (DROP PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
- The user who performed the statement becomes the owner of the created package.

<a id="d4df7be59c2666ac"></a>
### Syntax Rules and Parameters

<a id="ed87a1f51c4609bc"></a>
#### OR REPLACE

It replaces an existing package specification when the package already exists.

<a id="e57ae7327d71df4a"></a>
#### PACKAGE NAME

It is a name of package to be created, and it should be a unique name in a schema.   
It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.   
The length of a package name should be shorter than 128 bytes.

<a id="b88710cf86415364"></a>
#### Package Characteristics

It defines options to perform a package. It should be specified only once per a single item.

- AUTHID CURRENT_USER: SQLs which are being performed during performing items in a package are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing items in a package are interpreted and performed according to an authorization of a definer.

<a id="a4610c48817e3632"></a>
#### Item Declaration

It declares a public variable, a type cursor, a cursor variable, a function spec, and a procedure spec which are accessible from out of the package.   
A function and a procedure in the package should be defined through *create package body* statement.  
The cursor which was declared in a package without SQL should be defined through *create package body* statement.   
Also, a function, a procedure, an argument of a cursor and the returning type in a package should be as same as those defined in a body statement.

<a id="8542cb3fa7ab66f5"></a>
### Description

It creates the schema-level package specification.   
All public items in the created package can be referred by another procedure/ function/ package/ anonymous block.

The information about package creation can be viewed in MODULES table in DEFINITION_SCHEMA or INFORMATION_SCHEMA.   
The list of each public procedure/ function in the package can be viewed in ROUTINES table in DEFINITION_SCHEMA or INFORMATION_SCHEMA.   
The definition about parameters of each public procedure/ function in the package can be viewed in PARAMETERS table in DEFINITION_SCHEMA or INFORMATION_SCHEMA.  
Private procedure/ function can be viewed in MODULE_BODY table.   
If the information about objects referred by a procedure/ function/ variable in the package are temporarily unstable, try to recompile it by using &lt;alter package&gt; statement.

<a id="ebff1723dc13f16c"></a>
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

<a id="76a9e2c55ca47dd3"></a>
### Compatibility

It is CREATE MODULE statement in the SQL standard.

<a id="aa6a9aee6a7f45ab"></a>
### For More Information

Refer to the followings,

- [CREATE PACKAGE BODY](#57d0eac936305ba6)
- [DROP PACKAGE](#8644d4a6d3387eef)
- [ALTER PACKAGE](#d8b3f433e46b0333)

<a id="57d0eac936305ba6"></a>
## CREATE PACKAGE BODY

<a id="b7a48f1925c56964"></a>
### Function

It creates the definition about procedure/ function/ cursors to be used in the package.

<a id="c74f56a856d34926"></a>
### Syntax

```
<create package body statement> ::=
    CREATE [ OR REPLACE ] PACKAGE BODY package_name 
    { IS | AS } 
       <item_declaration> 
       <cursor_definition> 
       <routine_definition>
    [ BEGIN <initialization part> ]
    END
    ;

<item_declaration> ::=    VARIABLE_DECLARATION 
                        | CURSOR_DECLARATION
                        | USER_DEFINED_TYPE_DEFINITION 
                        | FUNCTION_DECLARATION 
                        | PROCEDURE_DECLARATION  
                        | USER_EXCEPTION_DECLARATION

<routine_definition> ::= FUNCTION_DEFINITION
                       | PROCEDURE_DEFINITION

<initialization part> ::= <pl_stmt_list>
```

<a id="e1a6b5f427817bfd"></a>
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

<a id="d02e02bf5539f70d"></a>
### Syntax Rules and Parameters

<a id="6ee9984eac80f6ac"></a>
#### OR REPLACE

It replaces an existing package body definition when the package body already exists.

<a id="0db795050b8e8971"></a>
#### PACKAGE NAME

It is a name of package body to be created, and the name as same as the name used in creating a package spec should be used. It should be a unique name in a schema.   
It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.   
The length of a package name should be shorter than 128 bytes.

<a id="73f3f2baf36f5e6c"></a>
#### Item Declaration

It declares PSM identifiers (variable, type, cursor, function spec, procedure spec, exception) to be used in a package body.  
Routines declared in a package spec should be defined in a package body.  
The cursor which was declared in a package spec without SQL should be defined in a package body.   

Also, a function, a procedure, an argument of a cursor and the returning type in a package should be as same as those defined in a body statement.

<a id="ff9dd75a9f7c5379"></a>
#### Initialization Part

It describes statements which are performed only once to initialize internal variables while creating a package instance.

<a id="c2af325ae44e43d6"></a>
### Description

It creates the schema-level package specification.   
All public items in the created package can be referred by another procedure/ function/ package/ anonymous block.

The information about package body creation can be viewed in MODULES_BODY table in DEFINITION_SCHEMA or INFORMATION_SCHEMA.   
The list of each private items in a package body can not be viewed in DEFINITION_SCHEMA or INFORMATION_SCHEMA.   
If the information about objects referred by a procedure/ function/ variable in the package are temporarily unstable, try to recompile it by using &lt;alter package body&gt; statement.

The created package body can be dropped by using &lt;drop package&gt; or &lt;drop package body&gt; statement.

<a id="e19e347c18d5235b"></a>
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

<a id="71e8ceee136dab77"></a>
### Compatibility

The SQL standard does not define it.

<a id="aeb656b904a7864a"></a>
### For More Information

Refer to the followings.

- [CREATE PACKAGE](#24f22bbbebed2d3b)
- [DROP PACKAGE](#8644d4a6d3387eef)
- [ALTER PACKAGE](#d8b3f433e46b0333)

<a id="acd5825880480a80"></a>
## CREATE PROCEDURE

<a id="809e66b3a4dbfa24"></a>
### Function

It defines a schema-level procedure.

<a id="dc3f7104854c1250"></a>
### Syntax

```
<create procedure statement> ::=
      CREATE [ OR REPLACE ] PROCEDURE <procedure name> [ ( <parameter list> ) ]
      { IS | AS } 
      <item declaration>  
      BEGIN
      <pl statement list> 
      END [ <procedure name> ]
      ;
 
<parameter list> ::= 
      <parameter name> [ <parameter mode> ] <datatype> [ <parameter default> ] [ , ... ] 

<parameter mode> ::= 
      IN 
    | OUT 
    | IN OUT 
 
<parameter default> ::= 
      { := | DEFAULT } <value expression> 

<procedure characteristics> ::= 
      AUTHID CURRENT_USER 
    | AUTHID DEFINER
```

<a id="ff271571a91c23a3"></a>
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

<a id="e05844f89237e807"></a>
### Syntax Rules and Parameters

<a id="0f2040f261f51275"></a>
#### OR REPLACE

It replaces an existing procedure with a new function when the procedure already exists.

<a id="cd8599e7a7525c94"></a>
#### procedure name

It is a name of procedure to be created, and it should be a unique name in a schema.  
It can define the schema to which the procedure belongs, such as schema_name.procedure_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of a procedure name should be shorter than 128 bytes.

<a id="7234eff3b2193575"></a>
#### parameter name

It defines a parameter name of the procedure.   
The name of each parameter should be unique in a procedure.   
In other words, the procedure's parameter and PL item can not have the same name.   
The length of a parameter name should be shorter than 128 bytes.   
The maximum number of parameters available in a single procedure is limitless.

<a id="e81d8373b95f9776"></a>
#### parameter mode

It sets each parameter mode.   
The parameter modes are IN, OUT, and IN OUT.  
If the parameter mode is not specified, the default mode is *IN*.

<a id="545ddec2683f41a9"></a>
#### parameter default

It is the default value of the parameter.  
The parameter with the specified parameter default can be omitted when executing the procedure.   
If the parameter is not specified but omitted, then the default value is &lt;value expression&gt; specified when defining the parameter.  
The datatype of &lt;value expression&gt; should be the datatype of the parameter.  
All parameters defined after the parameter having &lt;parameter default&gt; should have &lt;parameter default&gt;.

<a id="7e3100659511637b"></a>
#### procedure characteristics

It defines options to perform a procedure. It should be specified only once per a single item.

- AUTHID CURRENT_USER: SQLs which are being performed during performing a procedure are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing a procedure are interpreted and performed according to an authorization of a definer.

<a id="36d81a455a77593f"></a>
#### Item Declaration

It declares items such as a local variable to be used within a procedure.  
It can declare all items which can be declared in a PL block.

<a id="13d60a5a88ddd11e"></a>
#### PL Stmt List

It is a body section of a procedure, and it lists PL statements to be performed.  
It can not use a bind parameter such as '?' or ':V1'. within a procedure.

<a id="b62f0b00a12ef73d"></a>
### Description

It defines a schema-level SQL procedure. The created procedure can be called from CALL statement, anonymous block, or other procedure/ function.

The definition of a procedure can be viewed in ROUTINES table of INFORMATION_SCHEMA. The definition of a procedure parameter can be viewed in PARAMETERS table of INFORMATION_SCHEMA.

If a procedure becomes temporarily unstable due to absences of related objects, then it can try to recreate a plan by using [ALTER PROCEDURE](#93ff8d3e64fbbae1) statement.

The created procedure can be dropped by using [DROP PROCEDURE](#e555d2b555faabee) statement.  
The maximum number of procedures to be created is not limited. Therefore, they can be created as many as the storage space is available.

<a id="ea8bed30005df035"></a>
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

<a id="8a5db02485db0025"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="394f024387fc68a3"></a>
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
| B122 | Routine language C | X |
| B123 | Routine language COBOL | X |
| B124 | Routine language Fortran | X |
| B125 | Routine language MUMPS | X |
| B126 | Routine language Pascal | X |
| B127 | Routine language PL/I | X |
| B128 | Routine language SQL | O |
| B129 | Routine language Ada: VARCHAR and NUMERIC support | X |

<a id="b1c82c22ee616675"></a>
### For More Information

Refer to the followings.

- [DROP PROCEDURE](#e555d2b555faabee)
- [ALTER PROCEDURE](#93ff8d3e64fbbae1)

<a id="3f3a2b64579299ef"></a>
## DROP FUNCTION

<a id="d49427cf23c94756"></a>
### Function

It drops a function.

<a id="782d3c490927825b"></a>
### Syntax

```
<drop function statement> ::=
    DROP FUNCTION [ IF EXISTS ] func_name
    ;
```

<a id="b2213d48711b788d"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop function statement&gt;.

- The owner of that function
- (DROP PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the function belongs
- DROP ANY PROCEDURE ON DATABASE

<a id="3b3321417cd589bc"></a>
### Syntax Rules and Parameters

<a id="53f70e546c7d0a0c"></a>
#### IF EXISTS

Even when the function does not exist, an error does not occur.

<a id="1d5c6aaf2aab9557"></a>
#### FUNC NAME

It is the function name to be dropped.  
It can define the schema to which the function belongs, such as schema_name.func_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="645101993e8c7ea4"></a>
### Description

It drops a specified schema-level function.

<a id="6c474a87bb88a5d3"></a>
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

<a id="a16f68a40ae7d2dd"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="d1cfd10dfc5473c9"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="e670a44f5ba8720d"></a>
### For More Information

Refer to the followings.

- [CREATE FUNCTION](#40ab839511f9caec)
- [ALTER FUNCTION](#14b653d0765ad6d0)

<a id="8644d4a6d3387eef"></a>
## DROP PACKAGE

<a id="6c4db685c9743d55"></a>
### Function

It drops a package (of only body or both spec/ body).

<a id="bbf1483276454e71"></a>
### Syntax

```
<drop package statement> ::=
    DROP PACKAGE [BODY] [ IF EXISTS ] package_name
    ;
```

<a id="77c3f06df6b5a04d"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop package statement&gt;.

- The owner of that package 
- (DROP PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
- DROP ANY PACKAGE ON DATABASE

<a id="f61d5cf978268085"></a>
### Syntax Rules and Parameters

<a id="88f0cd0767b899f4"></a>
#### BODY

It drops only the body object in the package of the given name. If the keyword *BODY* is not specified it drops both the package specification and the body.

<a id="bb7652fcf52e8ffd"></a>
#### IF EXISTS

Even when the package does not exist, an error does not occur.

<a id="8f88d148f7be3f5a"></a>
#### PACKAGE NAME

It is the package name to be dropped.  
It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="b849e74df8aecc0b"></a>
### Description

It drops the specified package object.

<a id="a02458544aad91f7"></a>
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

<a id="8d730672a326c58c"></a>
### Compatibility

It is DRO MODULE statement in the SQL standard.

<a id="3dd62523eaa44cbe"></a>
### For More Information

Refer to the followings.

- [CREATE PACKAGE](#24f22bbbebed2d3b)
- [CREATE PACKAGE BODY](#57d0eac936305ba6)
- [ALTER PACKAGE](#d8b3f433e46b0333)

<a id="e555d2b555faabee"></a>
## DROP PROCEDURE

<a id="05e601eb0d784e16"></a>
### Function

It drops a procedure.

<a id="3e47c95bd3e7e75c"></a>
### Syntax

```
<drop procedure statement> ::=
    DROP PROCEDURE [ IF EXISTS ] proc_name
    ;
```

<a id="12a19fa7974d3264"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop procedure statement&gt;.

- The owner of that procedure
- (DROP PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- DROP ANY PROCEDURE ON DATABASE

<a id="184c19e36f4513d3"></a>
### Syntax Rules and Parameters

<a id="7a85f30637c402d5"></a>
#### IF EXISTS

Even when the procedure does not exist, an error does not occur.

<a id="2b6a8733e34f6f57"></a>
#### PROC NAME

It is the procedure name to be dropped.  
It can define the schema to which the procedure belongs, such as schema_name.proc_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="b18f023bfe3514d5"></a>
### Description

It drops a specified schema-level procedure.

<a id="32cb4fe53983b127"></a>
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

<a id="692cead3f2446747"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="60fd4bc1f2e0b8de"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="9360efd59358ab10"></a>
### For More Information

Refer to the followings.

- [CREATE PROCEDURE](#acd5825880480a80)
- [ALTER PROCEDURE](#93ff8d3e64fbbae1)

---

[← 28. PSM Language Element References](28-psm-language-element-references.md) · [Table of contents](../README.md) · [30. Database Connection →](../part-05-developer-manual/30-database-connection.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
