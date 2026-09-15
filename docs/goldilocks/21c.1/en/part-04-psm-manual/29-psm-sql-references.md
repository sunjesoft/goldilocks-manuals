<a id="26f7b884a5b3e715"></a>

# 29. PSM SQL References

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/26f7b884a5b3e715)  
> Tag: `21c.1_35_tag`

[← 28. PSM Language Element References](28-psm-language-element-references.md) · [Table of contents](../README.md) · [30. Database Connection →](../part-05-developer-manual/30-database-connection.md)

<a id="ef71ec594bad9de2"></a>
## ALTER FUNCTION

<a id="9190db2da3879887"></a>
### Function

It recompiles a function.

<a id="87529a72ad97e4e1"></a>
### Syntax

```
<alter function statement> ::=
    ALTER FUNCTION function_name COMPILE
    ;
```

<a id="b7c7e7931123d03a"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter function statement&gt;.

- The owner of that function
- (ALTER PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the function belongs
- ALTER ANY PROCEDURE ON DATABASE

<a id="55a8d061c13da401"></a>
### Syntax Rules and Parameters

- function Name
    - It is the function name to be compiled.
    - It can define the schema to which the function belongs, such as schema_name.func_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="6c1d65ceebb8b2cc"></a>
### Description

It recompiles a specified schema-level function.

<a id="f077e5c3b1f9628d"></a>
### Examples

```
gSQL> ALTER FUNCTION FUNC1 COMPILE;

Function altered.
```

<a id="02a6c2ce14fe0b91"></a>
### Compatibility

It is a statement altering characteristics specified when performing CREATE in the SQL standard, and astatement recreating a plan of a function in GOLDILOCKS.

**SQL standard compatibility**

<a id="7a49f1110799c9e2"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="89c86e7b7db29987"></a>
### For More Information

Refer to the followings.

- [CREATE FUNCTION](#7acaf940b774cb75)
- [DROP FUNCTION](#b68d9e7f71d37f62)

<a id="2b79a9a854e3c84a"></a>
## ALTER PACKAGE

<a id="2e0e7359eab323a5"></a>
### Function

It recompiles a package.

<a id="e90d1c75b8626234"></a>
### Syntax

```
<alter package statement> ::=
    ALTER PACKAGE package_name <package compile clause>
    ;

<package compile clause> ::=
    COMPILE [PACKAGE|SPECIFICATION|BODY]
```

<a id="19c41635f719134f"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter package statement&gt;.

- The owner of that package
- (ALTER PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs 
- ALTER ANY PACKAGE ON DATABASE

<a id="cf2cb5377650b471"></a>
### Syntax Rules and Parameters

- Package name
    - It is a name of package to be compiled.
    - It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

- Package compile clause
    - PACKAGE: It recompiles both the specification and the body. (Default)
    - SPECIFICATION: It recompiles only the specification.
    - BODY: It recompiles only the body.

<a id="ba14ac08b5fc49ad"></a>
### Description

It recompiles the specified package.  
The execution code of the compiled package is stored in the plan cache.

<a id="e9b3824f61107716"></a>
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

<a id="3ca41d06263c1286"></a>
### Compatibility

It is ALTER MODULE statement in the SQL standard.

<a id="3297e15241d80a17"></a>
### For More Information

Refer to the followings.

- [CREATE PACKAGE](#14a6f29743ca8dc2)
- [CREATE PACKAGE BODY](#e31e58ae43033cda)
- [DROP PACKAGE](#d9944ef018684a7d)

<a id="af11f349dc72408b"></a>
## ALTER PROCEDURE

<a id="56a254e22579ed67"></a>
### Function

It recompiles a procedure.

<a id="f856a6c489b83e8f"></a>
### Syntax

```
<alter procedure statement> ::=
    ALTER PROCEDURE proc_name COMPILE
    ;
```

<a id="c51f9d8d433b6132"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter procedure statement&gt;.

- The owner of that procedure
- (ALTER PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- ALTER ANY PROCEDURE ON DATABASE

<a id="1c33f9656c1baf4f"></a>
### Syntax Rules and Parameters

- Proc Name
    - It is the procedure name to be compiled.
    - It can define the schema to which the procedure belongs, such as schema_name.proc_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="f4035f14dc160b2b"></a>
### Description

It recompiles a specified schema-level procedure.

<a id="f71606723285026c"></a>
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

<a id="fc9fdc28c632d388"></a>
### Compatibility

It is a statement altering characteristics specified when performing CREATE in the SQL standard, and astatement recreating a plan of a procedure in GOLDILOCKS.

**SQL standard compatibility**

<a id="a57d30ede21bd3b0"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="311f5eb535e978fa"></a>
### For More Information

Refer to the followings.

- [CREATE PROCEDURE](#c4195b7175b4b1f4)
- [DROP PROCEDURE](#3b6f829e3aa92686)

<a id="bd610f7f021862b8"></a>
## CALL Statement

<a id="087db42df9890296"></a>
### Function

It performs a schema-level procedure or a function.

<a id="fa7b72fd6c2cc567"></a>
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

<a id="1cfc057e58682781"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;call statement&gt;.

- The EXECUTE privilege for that procedure
- (EXECUTE PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- EXECUTE ANY PROCEDURE ON DATABASE

<a id="7976db466fcf2060"></a>
### Syntax Rules and Parameters

- proc_name
    - It is a name of a procedure/ function to be executed.
    - It may includes a schema to which the procedure belongs such as Schema_name.Proc_name.
- value_expr
    - It expresses an argument value which were transferred to the procedure. It can use a bind parameter such as '?' or ':V1'.

<a id="c53e7b5d8ec9ef03"></a>
### Description

It executes a schema-level SQL procedure or a function by using specified arguments.

A function of &lt;sql call statement&gt; form returns the result value by using a host variable expression or a dynamic bind parameter (?) after INTO clause.

&lt;odbc procedure call escape sequence&gt; form is a standard statement to call PROCEDURE in  ODBC/ JDBC, and GOLDILOCKS supports this statement in a server. (It can also be used in a tool such as gsql.) A function returns the result value by using assign expressions ( ? = ) at the front.

<a id="4295b6ef5698369c"></a>
### Examples

<a id="efc9306019f61163"></a>
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

<a id="a3abe453a7e6a2e2"></a>
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

<a id="8652ee1da338bd9a"></a>
### Compatibility

The SQL standard allows only the call for a PROCEDURE, so it does not define below [INTO] clause.

<a id="7acaf940b774cb75"></a>
## CREATE FUNCTION

<a id="4998495e03f925a3"></a>
### Function

It defines a schema-level function.

<a id="83a2d9249c5a9264"></a>
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

<a id="f4fad9ef1b11ab76"></a>
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

<a id="82db8e491e8794fb"></a>
### Syntax Rules and Parameters

<a id="11e65a45af71c37c"></a>
#### OR REPLACE

It replaces an existing function when the function already exists.

<a id="8fa040dd3c91725b"></a>
#### FUNCTION NAME

It is a name of function to be created, and it should be a unique name in a schema.  
It can define the schema to which the function belongs, such as schema_name.func_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of a function name should be shorter than 128 bytes.

<a id="cfaf880bfa209bbd"></a>
#### PARAM NAME

It defines a name of an argument to be used in a function.  
The name of each argument should be unique in a function.  
The length of each argument name should be shorter than 128 bytes.  
It does not limit the maximum number of an argument to be used in a single function.

<a id="35f06a96c3cfaa6c"></a>
#### Bind Type

It specifies a bind type of each argument.  
If it is not specified, the default type is IN.

<a id="f89eabf52de4ce9c"></a>
#### Func_Characteristics

It defines options to perform a function. It should be specified only once per a single item.

- DETERMINISTIC: The function always returns the same result value when the same argument values are input.
- AUTHID CURRENT_USER: SQLs which are being performed during performing a function are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing a function are interpreted and performed according to an authorization of a definer.

<a id="a6b67c56036b1b2f"></a>
#### Item Declaration

It declares items such as a local variable to be used within a function.  
It can declare all items which can be declared in a PL block.

<a id="b9ec1f334e3ffb19"></a>
#### PL Stmt List

It is a body section of a function, and it lists PL statements to be performed.  
It can not use a bind parameter such as '?' or ':V1'. within a function.

<a id="a3a214666f7eeaed"></a>
### Description

It defines a schema-level SQL function. The created fucntion can be called from all expressions.

The definition of a function can be viewed in ROUTINES table of INFORMATION_SCHEMA. The definition of a function parameter can be viewed in PARAMETERS table of INFORMATION_SCHEMA.

If a function becomes temporarily unstable due to absences of related objects, then it can try to recreate a plan by using &lt;alter function&gt; statement.

The created function can be dropped by using &lt;drop function&gt; statement.  
The maximum number of functions to be created is not limited. Therefore, they can be created as many as the storage space is available.

<a id="ccba7060a585e11e"></a>
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

<a id="f30a0024a7418332"></a>
### Compatibility

The SQL standard does not define OR REPLACE clause.

**SQL standard compatibility**

<a id="3913d1481bd1c461"></a>
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

<a id="c86a5962a29c3511"></a>
### For More Information

Refer to the followings.

- [DROP FUNCTION](#b68d9e7f71d37f62)
- [ALTER FUNCTION](#ef71ec594bad9de2)

<a id="14a6f29743ca8dc2"></a>
## CREATE PACKAGE

<a id="264dc1b5a915d4e4"></a>
### Function

It defines the spec about public items to be used in a package.

<a id="f27422832175214c"></a>
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

<a id="1cb1248d85d8b702"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;create package statement&gt;.

- One of the following privileges is required to create a package.
    - (CREATE PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
    - CREATE ANY PACKAGE ON DATABASE
- If a package already exists when using OR REPLACE clause, then one of the following privileges dropping the existing package is required.
    - The owner of that package
    - (DROP PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
- The user who performed the statement becomes the owner of the created package.

<a id="347e4c5eb864a4d4"></a>
### Syntax Rules and Parameters

<a id="f688d5f3d3650f5c"></a>
#### OR REPLACE

It replaces an existing package specification when the package already exists.

<a id="ea0e690c3680f882"></a>
#### PACKAGE NAME

It is a name of package to be created, and it should be a unique name in a schema.   
It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.   
The length of a package name should be shorter than 128 bytes.

<a id="50d5e5627f0cd323"></a>
#### Package Characteristics

It defines options to perform a package. It should be specified only once per a single item.

- AUTHID CURRENT_USER: SQLs which are being performed during performing items in a package are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing items in a package are interpreted and performed according to an authorization of a definer.

<a id="963d959ed194aaf1"></a>
#### Item Declaration

It declares a public variable, a type cursor, a cursor variable, a function spec, and a procedure spec which are accessible from out of the package.   
A function and a procedure in the package should be defined through *create package body* statement.  
The cursor which was declared in a package without SQL should be defined through *create package body* statement.   
Also, a function, a procedure, an argument of a cursor and the returning type in a package should be as same as those defined in a body statement.

<a id="882a6cb981ff6a6e"></a>
### Description

It creates the schema-level package specification.   
All public items in the created package can be referred by another procedure/ function/ package/ anonymous block.

The information about package creation can be viewed in MODULES table in DEFINITION_SCHEMA or INFORMATION_SCHEMA.   
The list of each public procedure/ function in the package can be viewed in ROUTINES table in DEFINITION_SCHEMA or INFORMATION_SCHEMA.   
The definition about parameters of each public procedure/ function in the package can be viewed in PARAMETERS table in DEFINITION_SCHEMA or INFORMATION_SCHEMA.  
Private procedure/ function can be viewed in MODULE_BODY table.   
If the information about objects referred by a procedure/ function/ variable in the package are temporarily unstable, try to recompile it by using &lt;alter package&gt; statement.

<a id="4d5468e31280c044"></a>
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

<a id="85899446603a2b47"></a>
### Compatibility

It is CREATE MODULE statement in the SQL standard.

<a id="56214ae79bb7b28b"></a>
### For More Information

Refer to the followings,

- [CREATE PACKAGE BODY](#e31e58ae43033cda)
- [DROP PACKAGE](#d9944ef018684a7d)
- [ALTER PACKAGE](#2b79a9a854e3c84a)

<a id="e31e58ae43033cda"></a>
## CREATE PACKAGE BODY

<a id="bfa8b6e7eccbf54e"></a>
### Function

It creates the definition about procedure/ function/ cursors to be used in the package.

<a id="628a24c386404d3d"></a>
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

<a id="5600efcc0f876e9d"></a>
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

<a id="72e48332e6f60ba5"></a>
### Syntax Rules and Parameters

<a id="0bad6e2edb4d91a5"></a>
#### OR REPLACE

It replaces an existing package body definition when the package body already exists.

<a id="bbeec359ac429d22"></a>
#### PACKAGE NAME

It is a name of package body to be created, and the name as same as the name used in creating a package spec should be used. It should be a unique name in a schema.   
It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.   
The length of a package name should be shorter than 128 bytes.

<a id="bb3fc1eef018bd1f"></a>
#### Item Declaration

It declares PSM identifiers (variable, type, cursor, function spec, procedure spec, exception) to be used in a package body.  
Routines declared in a package spec should be defined in a package body.  
The cursor which was declared in a package spec without SQL should be defined in a package body.   

Also, a function, a procedure, an argument of a cursor and the returning type in a package should be as same as those defined in a body statement.

<a id="fb6a1b0c7515e576"></a>
#### Initialization Part

It describes statements which are performed only once to initialize internal variables while creating a package instance.

<a id="e5bdd345ad577cac"></a>
### Description

It creates the schema-level package specification.   
All public items in the created package can be referred by another procedure/ function/ package/ anonymous block.

The information about package body creation can be viewed in MODULES_BODY table in DEFINITION_SCHEMA or INFORMATION_SCHEMA.   
The list of each private items in a package body can not be viewed in DEFINITION_SCHEMA or INFORMATION_SCHEMA.   
If the information about objects referred by a procedure/ function/ variable in the package are temporarily unstable, try to recompile it by using &lt;alter package body&gt; statement.

The created package body can be dropped by using &lt;drop package&gt; or &lt;drop package body&gt; statement.

<a id="ac2000a9bf1dd113"></a>
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

<a id="0ebb4e2f4ef47cdb"></a>
### Compatibility

The SQL standard does not define it.

<a id="037f32b3506ccdea"></a>
### For More Information

Refer to the followings.

- [CREATE PACKAGE](#14a6f29743ca8dc2)
- [DROP PACKAGE](#d9944ef018684a7d)
- [ALTER PACKAGE](#2b79a9a854e3c84a)

<a id="c4195b7175b4b1f4"></a>
## CREATE PROCEDURE

<a id="ba350267bc10cc90"></a>
### Function

It defines a schema-level procedure.

<a id="e9cd579ffa47e7dc"></a>
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

<a id="be9a868dc165db6d"></a>
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

<a id="5fe0c9198825e6fc"></a>
### Syntax Rules and Parameters

<a id="a0768e4b0267013c"></a>
#### OR REPLACE

It replaces an existing procedure when the procedure already exists.

<a id="2724c7ec8d2413ce"></a>
#### PROC NAME

It is a name of procedure to be created, and it should be a unique name in a schema.  
It can define the schema to which the procedure belongs, such as schema_name.proc_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of a procedure name should be shorter than 128 bytes.

<a id="de8118aa86cbabf9"></a>
#### PARAM NAME

It defines a name of an argument to be used in a procedure.  
The name of each argument should be unique in a procedure.  
The length of each argument name should be shorter than 128 bytes.  
It does not limit the maximum number of an argument to be used in a single procedure.

<a id="6ee9965ffc818f19"></a>
#### Bind Type

It specifies a bind type of each argument.  
If it is not specified, the default type is IN.

<a id="f089dcf2fcbede3a"></a>
#### proc_characteristics

It defines options to perform a procedure. It should be specified only once per a single item.

- AUTHID CURRENT_USER: SQLs which are being performed during performing a procedure are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing a procedure are interpreted and performed according to an authorization of a definer.

<a id="3b3f4bace729ab16"></a>
#### Item Declaration

It declares items such as a local variable to be used within a procedure.  
It can declare all items which can be declared in a PL block.

<a id="68c5b0fefc899506"></a>
#### PL Stmt List

It is a body section of a procedure, and it lists PL statements to be performed.  
It can not use a bind parameter such as '?' or ':V1'. within a procedure.

<a id="b31c5f26920425ac"></a>
### Description

It defines a schema-level SQL procedure. The created procedure can be called from CALL statement, anonymous block, or other procedure/ function.

The definition of a procedure can be viewed in ROUTINES table of INFORMATION_SCHEMA. The definition of a procedure parameter can be viewed in PARAMETERS table of INFORMATION_SCHEMA.

If a procedure becomes temporarily unstable due to absences of related objects, then it can try to recreate a plan by using &lt;alter procedure&gt; statement.

The created procedure can be dropped by using &lt;drop procedure&gt; statement.  
The maximum number of procedures to be created is not limited. Therefore, they can be created as many as the storage space is available.

<a id="9add83d8d004cf4e"></a>
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

<a id="79e0e48f55be8af7"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="ea0d9136e1c297c6"></a>
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

<a id="9b17774cf92504bb"></a>
### For More Information

Refer to the followings.

- [DROP PROCEDURE](#3b6f829e3aa92686)
- [ALTER PROCEDURE](#af11f349dc72408b)

<a id="b68d9e7f71d37f62"></a>
## DROP FUNCTION

<a id="372a78456f6fb226"></a>
### Function

It drops a function.

<a id="7ee0b84bde3facef"></a>
### Syntax

```
<drop function statement> ::=
    DROP FUNCTION [ IF EXISTS ] func_name
    ;
```

<a id="3afc5aca37d8c768"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop function statement&gt;.

- The owner of that function
- (DROP PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the function belongs
- DROP ANY PROCEDURE ON DATABASE

<a id="ec32bfc33c96dd25"></a>
### Syntax Rules and Parameters

<a id="7f8d637622b0092b"></a>
#### IF EXISTS

Even when the function does not exist, an error does not occur.

<a id="bdfec181f2971a07"></a>
#### FUNC NAME

It is the function name to be dropped.  
It can define the schema to which the function belongs, such as schema_name.func_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="14aa162645de5c8a"></a>
### Description

It drops a specified schema-level function.

<a id="56f1e105427a5239"></a>
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

<a id="14b90e69006ccbda"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="f9f18a3fbee9572d"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="55898e7637d5d473"></a>
### For More Information

Refer to the followings.

- [CREATE FUNCTION](#7acaf940b774cb75)
- [ALTER FUNCTION](#ef71ec594bad9de2)

<a id="d9944ef018684a7d"></a>
## DROP PACKAGE

<a id="91a1a7b83b14adc1"></a>
### Function

It drops a package (of only body or both spec/ body).

<a id="8b3f508d9814659e"></a>
### Syntax

```
<drop package statement> ::=
    DROP PACKAGE [BODY] [ IF EXISTS ] package_name
    ;
```

<a id="061eb1ba9645c029"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop package statement&gt;.

- The owner of that package 
- (DROP PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
- DROP ANY PACKAGE ON DATABASE

<a id="9ba099a3687bf4ed"></a>
### Syntax Rules and Parameters

<a id="22be296a60c87534"></a>
#### BODY

It drops only the body object in the package of the given name. If the keyword *BODY* is not specified it drops both the package specification and the body.

<a id="e942b8fa57793339"></a>
#### IF EXISTS

Even when the package does not exist, an error does not occur.

<a id="6610d46fa4ab979f"></a>
#### PACKAGE NAME

It is the package name to be dropped.  
It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="c4c58b9d5cb8227c"></a>
### Description

It drops the specified package object.

<a id="a95383affa873321"></a>
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

<a id="286e81ab1110383e"></a>
### Compatibility

It is DRO MODULE statement in the SQL standard.

<a id="7cbed455927e8071"></a>
### For More Information

Refer to the followings.

- [CREATE PACKAGE](#14a6f29743ca8dc2)
- [CREATE PACKAGE BODY](#e31e58ae43033cda)
- [ALTER PACKAGE](#2b79a9a854e3c84a)

<a id="3b6f829e3aa92686"></a>
## DROP PROCEDURE

<a id="df7530cb999b2f1f"></a>
### Function

It drops a procedure.

<a id="6004817bd279a520"></a>
### Syntax

```
<drop procedure statement> ::=
    DROP PROCEDURE [ IF EXISTS ] proc_name
    ;
```

<a id="67a283b50468e931"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop procedure statement&gt;.

- The owner of that procedure
- (DROP PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- DROP ANY PROCEDURE ON DATABASE

<a id="3ca6ce05c03dbbf7"></a>
### Syntax Rules and Parameters

<a id="bd183b678b50709a"></a>
#### IF EXISTS

Even when the procedure does not exist, an error does not occur.

<a id="19d57f8654198fa7"></a>
#### PROC NAME

It is the procedure name to be dropped.  
It can define the schema to which the procedure belongs, such as schema_name.proc_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="6d52672cb45c8546"></a>
### Description

It drops a specified schema-level procedure.

<a id="2db94fbceacbeb08"></a>
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

<a id="20e9dc7af5c20ddf"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="742128af254bd13a"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="2f739d518079669f"></a>
### For More Information

Refer to the followings.

- [CREATE PROCEDURE](#c4195b7175b4b1f4)
- [ALTER PROCEDURE](#af11f349dc72408b)

---

[← 28. PSM Language Element References](28-psm-language-element-references.md) · [Table of contents](../README.md) · [30. Database Connection →](../part-05-developer-manual/30-database-connection.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
