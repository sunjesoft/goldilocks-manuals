<a id="3203d9e98a32d593"></a>

# 27. PSM SQL References

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/3203d9e98a32d593)  
> Tag: `20c.1_30_tag`

[← 26. PSM Language Element References](26-psm-language-element-references.md) · [Table of contents](../README.md) · [28. Database Connection →](../part-05-developer-manual/28-database-connection.md)

<a id="d12efb20032d9505"></a>
## ALTER FUNCTION

<a id="09755b4a3c9ba2b6"></a>
### Function

It recompiles a function.

<a id="ed929231ae778b08"></a>
### Syntax

```
<alter function statement> ::=
    ALTER FUNCTION function_name COMPILE
    ;
```

<a id="c98d6c41cf116b31"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter function statement&gt;.

- The owner of that function
- (ALTER PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the function belongs
- ALTER ANY PROCEDURE ON DATABASE

<a id="639535c0b9bfcd0d"></a>
### Syntax Rules and Parameters

- function Name
    - It is the function name to be compiled.
    - It can define the schema to which the function belongs, such as schema_name.func_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="abb1c5e945a2473e"></a>
### Description

It recompiles a specified schema-level function.

<a id="43e29ad61e1ea0d5"></a>
### Examples

```
gSQL> ALTER FUNCTION FUNC1 COMPILE;

Function altered.
```

<a id="5f4df4ac8147e9ef"></a>
### Compatibility

It is a statement altering characteristics specified when performing CREATE in the SQL standard, and astatement recreating a plan of a function in GOLDILOCKS.

**SQL standard compatibility**

<a id="6d7efddf46b0f655"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="fc167f380cb0ed10"></a>
### For More Information

Refer to the followings.

- [CREATE FUNCTION](#d8170858a1ff601a)
- [DROP FUNCTION](#7a369d8891ee7e56)

<a id="d764dcd97c314905"></a>
## ALTER PACKAGE

<a id="56534149d1bd3570"></a>
### Function

It recompiles a package.

<a id="629ea56e5529b84b"></a>
### Syntax

```
<alter package statement> ::=
    ALTER PACKAGE package_name <package compile clause>
    ;

<package compile clause> ::=
    COMPILE [PACKAGE|SPECIFICATION|BODY]
```

<a id="f7e6e0a92cd40e0d"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter package statement&gt;.

- The owner of that package
- (ALTER PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs 
- ALTER ANY PACKAGE ON DATABASE

<a id="195df73cc0195fb5"></a>
### Syntax Rules and Parameters

- Package name
    - It is a name of package to be compiled.
    - It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

- Package compile clause
    - PACKAGE: It recompiles both the specification and the body. (Default)
    - SPECIFICATION: It recompiles only the specification.
    - BODY: It recompiles only the body.

<a id="5a4bc35777e7812f"></a>
### Description

It recompiles the specified package.  
The execution code of the compiled package is stored in the plan cache.

<a id="72f0db3b3c97e3ef"></a>
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

<a id="9960b1f68d36aca9"></a>
### Compatibility

It is ALTER MODULE statement in the SQL standard.

<a id="2eae3c04c9d7da22"></a>
### For More Information

Refer to the followings.

- [CREATE PACKAGE](#1703e698a9990747)
- [CREATE PACKAGE BODY](#8cd428de365c3d39)
- [DROP PACKAGE](#275183c395e46b67)

<a id="ecd363c4a7a70bd3"></a>
## ALTER PROCEDURE

<a id="dc70604578cfd763"></a>
### Function

It recompiles a procedure.

<a id="8d5a0a408015cd16"></a>
### Syntax

```
<alter procedure statement> ::=
    ALTER PROCEDURE proc_name COMPILE
    ;
```

<a id="f6b0088849226840"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter procedure statement&gt;.

- The owner of that procedure
- (ALTER PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- ALTER ANY PROCEDURE ON DATABASE

<a id="be0320fcdeb3b9d2"></a>
### Syntax Rules and Parameters

- Proc Name
    - It is the procedure name to be compiled.
    - It can define the schema to which the procedure belongs, such as schema_name.proc_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="ecdd69cf924e294a"></a>
### Description

It recompiles a specified schema-level procedure.

<a id="fabd5f8cfa61dc7f"></a>
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

<a id="68556fa54e76e96e"></a>
### Compatibility

It is a statement altering characteristics specified when performing CREATE in the SQL standard, and astatement recreating a plan of a procedure in GOLDILOCKS.

**SQL standard compatibility**

<a id="8e21d5682dba4fd9"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="4347125f951bbdfd"></a>
### For More Information

Refer to the followings.

- [CREATE PROCEDURE](#5d4ca7cc7bd25c89)
- [DROP PROCEDURE](#42a1923f875beab4)

<a id="d2db260011a29f5b"></a>
## CALL Statement

<a id="006c212a2b20fcd0"></a>
### Function

It performs a schema-level procedure or a function.

<a id="0c9026a3e74d576d"></a>
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

<a id="29ac150d953d9d24"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;call statement&gt;.

- The EXECUTE privilege for that procedure
- (EXECUTE PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- EXECUTE ANY PROCEDURE ON DATABASE

<a id="ece6a4f9f12cde76"></a>
### Syntax Rules and Parameters

- proc_name
    - It is a name of a procedure/ function to be executed.
    - It may includes a schema to which the procedure belongs such as Schema_name.Proc_name.
- value_expr
    - It expresses an argument value which were transferred to the procedure. It can use a bind parameter such as '?' or ':V1'.

<a id="2dc2a54260f6f648"></a>
### Description

It executes a schema-level SQL procedure or a function by using specified arguments.

A function of &lt;sql call statement&gt; form returns the result value by using a host variable expression or a dynamic bind parameter (?) after INTO clause.

&lt;odbc procedure call escape sequence&gt; form is a standard statement to call PROCEDURE in  ODBC/ JDBC, and GOLDILOCKS supports this statement in a server. (It can also be used in a tool such as gsql.) A function returns the result value by using assign expressions ( ? = ) at the front.

<a id="559180047d982224"></a>
### Examples

<a id="2788c223ff99bdad"></a>
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

<a id="27f6429c0ac0972c"></a>
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

<a id="2bd532a0fce3ed5d"></a>
### Compatibility

The SQL standard allows only the call for a PROCEDURE, so it does not define below [INTO] clause.

<a id="d8170858a1ff601a"></a>
## CREATE FUNCTION

<a id="938c46efcc2b296f"></a>
### Function

It defines a schema-level function.

<a id="9d59cb0f92a63845"></a>
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

<a id="f31278a162a6e5c5"></a>
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

<a id="45b741cce93af574"></a>
### Syntax Rules and Parameters

<a id="9902907c7b7043a3"></a>
#### OR REPLACE

It replaces an existing function when the function already exists.

<a id="05f9ec9eb4162d9b"></a>
#### FUNCTION NAME

It is a name of function to be created, and it should be a unique name in a schema.  
It can define the schema to which the function belongs, such as schema_name.func_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of a function name should be shorter than 128 bytes.

<a id="45fb15519c286463"></a>
#### PARAM NAME

It defines a name of an argument to be used in a function.  
The name of each argument should be unique in a function.  
The length of each argument name should be shorter than 128 bytes.  
It does not limit the maximum number of an argument to be used in a single function.

<a id="8399a56f810fd6db"></a>
#### Bind Type

It specifies a bind type of each argument.  
If it is not specified, the default type is IN.

<a id="0e984895ecb5023b"></a>
#### Func_Characteristics

It defines options to perform a function. It should be specified only once per a single item.

- DETERMINISTIC: The function always returns the same result value when the same argument values are input.
- AUTHID CURRENT_USER: SQLs which are being performed during performing a function are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing a function are interpreted and performed according to an authorization of a definer.

<a id="d6bb174fabaccd5e"></a>
#### Item Declaration

It declares items such as a local variable to be used within a function.  
It can declare all items which can be declared in a PL block.

<a id="ce7a410a1df456b7"></a>
#### PL Stmt List

It is a body section of a function, and it lists PL statements to be performed.  
It can not use a bind parameter such as '?' or ':V1'. within a function.

<a id="91e707c18b8ff499"></a>
### Description

It defines a schema-level SQL function. The created fucntion can be called from all expressions.

The definition of a function can be viewed in ROUTINES table of INFORMATION_SCHEMA. The definition of a function parameter can be viewed in PARAMETERS table of INFORMATION_SCHEMA.

If a function becomes temporarily unstable due to absences of related objects, then it can try to recreate a plan by using &lt;alter function&gt; statement.

The created function can be dropped by using &lt;drop function&gt; statement.  
The maximum number of functions to be created is not limited. Therefore, they can be created as many as the storage space is available.

<a id="d10945555da68efc"></a>
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

<a id="08f4d89821a1efbd"></a>
### Compatibility

The SQL standard does not define OR REPLACE clause.

**SQL standard compatibility**

<a id="956f5f1dce2e4440"></a>
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

<a id="f6a6cfc5f7a02327"></a>
### For More Information

Refer to the followings.

- [DROP FUNCTION](#7a369d8891ee7e56)
- [ALTER FUNCTION](#d12efb20032d9505)

<a id="1703e698a9990747"></a>
## CREATE PACKAGE

<a id="04f06babe34a9804"></a>
### Function

It defines the spec about public items to be used in a package.

<a id="f9b326cebab03569"></a>
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

<a id="6f6d234401bf3f31"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;create package statement&gt;.

- One of the following privileges is required to create a package.
    - (CREATE PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
    - CREATE ANY PACKAGE ON DATABASE
- If a package already exists when using OR REPLACE clause, then one of the following privileges dropping the existing package is required.
    - The owner of that package
    - (DROP PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
- The user who performed the statement becomes the owner of the created package.

<a id="b1982a875e18ad7a"></a>
### Syntax Rules and Parameters

<a id="6a21e25954e63c78"></a>
#### OR REPLACE

It replaces an existing package specification when the package already exists.

<a id="3f761f156f85bf96"></a>
#### PACKAGE NAME

It is a name of package to be created, and it should be a unique name in a schema.   
It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.   
The length of a package name should be shorter than 128 bytes.

<a id="10e70a2f31ed8811"></a>
#### Package Characteristics

It defines options to perform a package. It should be specified only once per a single item.

- AUTHID CURRENT_USER: SQLs which are being performed during performing items in a package are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing items in a package are interpreted and performed according to an authorization of a definer.

<a id="48ccfbf0369b40a8"></a>
#### Item Declaration

It declares a public variable, a type cursor, a cursor variable, a function spec, and a procedure spec which are accessible from out of the package.   
A function and a procedure in the package should be defined through *create package body* statement.  
The cursor which was declared in a package without SQL should be defined through *create package body* statement.   
Also, a function, a procedure, an argument of a cursor and the returning type in a package should be as same as those defined in a body statement.

<a id="c10ff614ba7902b7"></a>
### Description

It creates the schema-level package specification.   
All public items in the created package can be referred by another procedure/ function/ package/ anonymous block.

The information about package creation can be viewed in MODULES table in DEFINITION_SCHEMA or INFORMATION_SCHEMA.   
The list of each public procedure/ function in the package can be viewed in ROUTINES table in DEFINITION_SCHEMA or INFORMATION_SCHEMA.   
The definition about parameters of each public procedure/ function in the package can be viewed in PARAMETERS table in DEFINITION_SCHEMA or INFORMATION_SCHEMA.  
Private procedure/ function can be viewed in MODULE_BODY table.   
If the information about objects referred by a procedure/ function/ variable in the package are temporarily unstable, try to recompile it by using &lt;alter package&gt; statement.

<a id="4cf1e4f2a9272baa"></a>
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

<a id="460b233f41e7707f"></a>
### Compatibility

It is CREATE MODULE statement in the SQL standard.

<a id="7d2c1772b960ccc0"></a>
### For More Information

Refer to the followings,

- [CREATE PACKAGE BODY](#8cd428de365c3d39)
- [DROP PACKAGE](#275183c395e46b67)
- [ALTER PACKAGE](#d764dcd97c314905)

<a id="8cd428de365c3d39"></a>
## CREATE PACKAGE BODY

<a id="96f09850c8281ea1"></a>
### Function

It creates the definition about procedure/ function/ cursors to be used in the package.

<a id="dff4c3176f1f6bd3"></a>
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

<a id="8f792a5d8c98bc44"></a>
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

<a id="2ea732afc229cf38"></a>
### Syntax Rules and Parameters

<a id="bcb5171a7ebef083"></a>
#### OR REPLACE

It replaces an existing package body definition when the package body already exists.

<a id="5ff2f6c173c8f8f5"></a>
#### PACKAGE NAME

It is a name of package body to be created, and the name as same as the name used in creating a package spec should be used. It should be a unique name in a schema.   
It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.   
The length of a package name should be shorter than 128 bytes.

<a id="8fd60f9a89d97790"></a>
#### Item Declaration

It declares PSM identifiers (variable, type, cursor, function spec, procedure spec, exception) to be used in a package body.  
Routines declared in a package spec should be defined in a package body.  
The cursor which was declared in a package spec without SQL should be defined in a package body.   

Also, a function, a procedure, an argument of a cursor and the returning type in a package should be as same as those defined in a body statement.

<a id="1a71157d4f1d6e8f"></a>
#### Initialization Part

It describes statements which are performed only once to initialize internal variables while creating a package instance.

<a id="b6fcbe9cb47876ab"></a>
### Description

It creates the schema-level package specification.   
All public items in the created package can be referred by another procedure/ function/ package/ anonymous block.

The information about package body creation can be viewed in MODULES_BODY table in DEFINITION_SCHEMA or INFORMATION_SCHEMA.   
The list of each private items in a package body can not be viewed in DEFINITION_SCHEMA or INFORMATION_SCHEMA.   
If the information about objects referred by a procedure/ function/ variable in the package are temporarily unstable, try to recompile it by using &lt;alter package body&gt; statement.

The created package body can be dropped by using &lt;drop package&gt; or &lt;drop package body&gt; statement.

<a id="7925788e42e1b586"></a>
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

<a id="058cdd1b3416005a"></a>
### Compatibility

The SQL standard does not define it.

<a id="c7befd93d1ef4ea0"></a>
### For More Information

Refer to the followings.

- [CREATE PACKAGE](#1703e698a9990747)
- [DROP PACKAGE](#275183c395e46b67)
- [ALTER PACKAGE](#d764dcd97c314905)

<a id="5d4ca7cc7bd25c89"></a>
## CREATE PROCEDURE

<a id="8c485f337dba1419"></a>
### Function

It defines a schema-level procedure.

<a id="169431ab83a4d1ec"></a>
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

<a id="eb1e30b531df2750"></a>
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

<a id="e247b4e8e8d49565"></a>
### Syntax Rules and Parameters

<a id="b5d481f524d88a5c"></a>
#### OR REPLACE

It replaces an existing procedure when the procedure already exists.

<a id="fe7268a799a586a3"></a>
#### PROC NAME

It is a name of procedure to be created, and it should be a unique name in a schema.  
It can define the schema to which the procedure belongs, such as schema_name.proc_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of a procedure name should be shorter than 128 bytes.

<a id="44149440f2a07e03"></a>
#### PARAM NAME

It defines a name of an argument to be used in a procedure.  
The name of each argument should be unique in a procedure.  
The length of each argument name should be shorter than 128 bytes.  
It does not limit the maximum number of an argument to be used in a single procedure.

<a id="67396fdd460745c7"></a>
#### Bind Type

It specifies a bind type of each argument.  
If it is not specified, the default type is IN.

<a id="3f4a3753af8144cc"></a>
#### proc_characteristics

It defines options to perform a procedure. It should be specified only once per a single item.

- AUTHID CURRENT_USER: SQLs which are being performed during performing a procedure are interpreted and performed according to an authorization of an invoker.
- AUTHID DEFINER: SQLs which are being performed during performing a procedure are interpreted and performed according to an authorization of a definer.

<a id="f5d52ae099f745a1"></a>
#### Item Declaration

It declares items such as a local variable to be used within a procedure.  
It can declare all items which can be declared in a PL block.

<a id="1ceef10f93b7a69c"></a>
#### PL Stmt List

It is a body section of a procedure, and it lists PL statements to be performed.  
It can not use a bind parameter such as '?' or ':V1'. within a procedure.

<a id="d395dccd4d0ab44f"></a>
### Description

It defines a schema-level SQL procedure. The created procedure can be called from CALL statement, anonymous block, or other procedure/ function.

The definition of a procedure can be viewed in ROUTINES table of INFORMATION_SCHEMA. The definition of a procedure parameter can be viewed in PARAMETERS table of INFORMATION_SCHEMA.

If a procedure becomes temporarily unstable due to absences of related objects, then it can try to recreate a plan by using &lt;alter procedure&gt; statement.

The created procedure can be dropped by using &lt;drop procedure&gt; statement.  
The maximum number of procedures to be created is not limited. Therefore, they can be created as many as the storage space is available.

<a id="639dcc8fa24d0f97"></a>
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

<a id="4440340150c56d7d"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="f4fe334b5d9e81dc"></a>
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

<a id="697cd14ff0a32828"></a>
### For More Information

Refer to the followings.

- [DROP PROCEDURE](#42a1923f875beab4)
- [ALTER PROCEDURE](#ecd363c4a7a70bd3)

<a id="7a369d8891ee7e56"></a>
## DROP FUNCTION

<a id="80e993d6b4599886"></a>
### Function

It drops a function.

<a id="9e019f8f54596fab"></a>
### Syntax

```
<drop function statement> ::=
    DROP FUNCTION [ IF EXISTS ] func_name
    ;
```

<a id="db4ba004c12a8b23"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop function statement&gt;.

- The owner of that function
- (DROP PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the function belongs
- DROP ANY PROCEDURE ON DATABASE

<a id="da9c37859c591a3a"></a>
### Syntax Rules and Parameters

<a id="6701e1ddd43be321"></a>
#### IF EXISTS

Even when the function does not exist, an error does not occur.

<a id="d267c704acfdd99e"></a>
#### FUNC NAME

It is the function name to be dropped.  
It can define the schema to which the function belongs, such as schema_name.func_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="c334a4326b274eb1"></a>
### Description

It drops a specified schema-level function.

<a id="ba598cc8ed3a4e5c"></a>
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

<a id="f6766d52500fe71e"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="8a0b9c91101097c8"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="015fbcdb47ce9214"></a>
### For More Information

Refer to the followings.

- [CREATE FUNCTION](#d8170858a1ff601a)
- [ALTER FUNCTION](#d12efb20032d9505)

<a id="275183c395e46b67"></a>
## DROP PACKAGE

<a id="87e04b880a0d04f3"></a>
### Function

It drops a package (of only body or both spec/ body).

<a id="e6d33ec6af1d99ac"></a>
### Syntax

```
<drop package statement> ::=
    DROP PACKAGE [BODY] [ IF EXISTS ] package_name
    ;
```

<a id="d3e6f13521c16552"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop package statement&gt;.

- The owner of that package 
- (DROP PACKAGE or CONTROL SCHEMA) ON SCHEMA for the schema to which the package belongs
- DROP ANY PACKAGE ON DATABASE

<a id="780df69bcd69a0ad"></a>
### Syntax Rules and Parameters

<a id="a0c024d95a549227"></a>
#### BODY

It drops only the body object in the package of the given name. If the keyword *BODY* is not specified it drops both the package specification and the body.

<a id="e2faef063dc0e5b6"></a>
#### IF EXISTS

Even when the package does not exist, an error does not occur.

<a id="caabd90189348fde"></a>
#### PACKAGE NAME

It is the package name to be dropped.  
It can define the schema to which the package belongs, such as schema_name.package_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="3ec2f1d5b49d18b5"></a>
### Description

It drops the specified package object.

<a id="9ed9e6e972361423"></a>
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

<a id="afb0bb9c7a13a19e"></a>
### Compatibility

It is DRO MODULE statement in the SQL standard.

<a id="914f5853b74e8893"></a>
### For More Information

Refer to the followings.

- [CREATE PACKAGE](#1703e698a9990747)
- [CREATE PACKAGE BODY](#8cd428de365c3d39)
- [ALTER PACKAGE](#d764dcd97c314905)

<a id="42a1923f875beab4"></a>
## DROP PROCEDURE

<a id="ce626c9747b2bd7f"></a>
### Function

It drops a procedure.

<a id="4de197b4e5c45cee"></a>
### Syntax

```
<drop procedure statement> ::=
    DROP PROCEDURE [ IF EXISTS ] proc_name
    ;
```

<a id="02ec4ecf827cd13c"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop procedure statement&gt;.

- The owner of that procedure
- (DROP PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
- DROP ANY PROCEDURE ON DATABASE

<a id="1d5ce1461a41b658"></a>
### Syntax Rules and Parameters

<a id="9672d7f96e23b7d9"></a>
#### IF EXISTS

Even when the procedure does not exist, an error does not occur.

<a id="a4c6b1064fee9df3"></a>
#### PROC NAME

It is the procedure name to be dropped.  
It can define the schema to which the procedure belongs, such as schema_name.proc_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="6a2e8b01bc8d02c5"></a>
### Description

It drops a specified schema-level procedure.

<a id="7cf32821dc84e538"></a>
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

<a id="9819b22998a4eceb"></a>
### Compatibility

The SQL standard does not define the following clauses.

**SQL standard compatibility**

<a id="a03e1c3d31d21ed7"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="4dd35d041904971c"></a>
### For More Information

Refer to the followings.

- [CREATE PROCEDURE](#5d4ca7cc7bd25c89)
- [ALTER PROCEDURE](#ecd363c4a7a70bd3)

---

[← 26. PSM Language Element References](26-psm-language-element-references.md) · [Table of contents](../README.md) · [28. Database Connection →](../part-05-developer-manual/28-database-connection.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
