<a id="fa6943adc6ba8583"></a>

# 21. Overview of PSM

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/fa6943adc6ba8583)  
> Tag: `26c.1_0_tag`

[← 20. SQL References (H~Z)](../part-03-sql-manual/20-sql-references-h-z.md) · [Table of contents](../README.md) · [22. PSM DataTypes →](22-psm-datatypes.md)

<a id="bc0d409d4c0f958b"></a>
## Features of PSM

<a id="b00112fdaef6985c"></a>
### Closely Interworking with SQL

GOLIDILOCKS PSM can closely interworks with GOLDILOCKS SQL.

- It supports all data types supported by GOLDILOCKS SQL.
- It supports an attribute type (%TYPE, %ROWTYPE), so a flexible tables and column types are available.
- It supports all operators and built-in functions supported by GOLDILOCKS SQL.
- It supports all DML, DCL (COMMIT/ROLLBACK) supported by GOLDILOCKS SQL.
- It supports SQL SELECT statements by declaring a cursor and using OPEN, FETCH, CLOSE statements.
- It supports SQL DDL statements through the dynamic SQL feature.

<a id="40de25fc47a8a563"></a>
### Improving Performance

GOLDILOCKS PSM is operated only within a server, so it reduces the number of communications between the user application and the DBMS server. Therefore, the overall performance is improved.

<a id="69cbb25d3056a91e"></a>
### Improving Productivity

The language of GOLDILOCKS PSM is quite similar to that of script, a less effort is required to write a code for the desired feature. The time of writing a client application can be reduced if the procedure and funcure is created by modularizing the user's work logic.

<a id="d09b9e0a43074fcd"></a>
### Portability

Procedures and functions created by GOLDILOCKS PSM can also be used in ODBC, JDBC, an embedded SQL, and various development tools in the same way. Also, it can be easily transplanted in a different platform regardless of the platform type of server or a client.

<a id="5fdcf112e4384758"></a>
### Easy Maintenance

GOLDILOCKS PSM is implemented into a single module in a server from each similar logics in separate clients. Therefore, it is easy to manage, and enable to modify when it is in need even during the module is in use.

<a id="5e7023f21599089c"></a>
## Language Elements

<a id="bce4688f2ed02ad9"></a>
### Data Types

GOLDILOCKS PSM provides all built-in data types provided by GOLDILOCKS SQL, and it even supports user defined records and collection types.  
For more information, refer to [PSM DataTypes](22-psm-datatypes.md#2fe90d5805cc1b9e).

<a id="7cbda06c4eecef3d"></a>
### Variables

Required variables declared by a user in GOLDILOCKS PSM can be used in all expressions.

For more information, refer to the following.  
• [Declarative Part](23-psm-control-statements.md#398839cad09efa49)  
• [Assignment](23-psm-control-statements.md#56a4b551cb2918ec)

<a id="94f7b70bcedcf51c"></a>
### Control Structures

GOLDILOCKS PSM supports most of decision branch statements, unconditional branch statements (GOTO),  loop statement for repeated executions which were provided by a general script language.  
For more information, refer to [PSM Control Statements](23-psm-control-statements.md#ef5980dd9dd05ba7).

<a id="a16f09c73fa7c3d8"></a>
### Subprograms

GOLDILOCKS PSM subprogram is a PSM block with a name and it can be repeatedly performed. If a subprogramd has an argument, then it can be performed by being given different arguments when each time it is called.   
Subprogram is either in a procedure form or a function form, and the function form has a return value. It also supports a nested subprogram which is declared in a specific block and used within it.  
For more information, refer to [Using PSM Subprograms](25-using-psm-subprograms.md#31048831dcb5b296).

<a id="a2d6eb2da1383b07"></a>
## Processing Transaction in PSM

A database transaction is a work unit which consists of one or more of SQL statements and it can not be disassembled. The following are SQL statements which use transactions in GOLDILOCKS database.

- DML except for SELECT statements
- All DDL

A transaction starts in the following cases.

- When performing SQL which uses a transaction for the first time immediately after the connection.
- When performing SQL which uses a transaction for the first time since COMMIT or ROLLBACK

A transaction ends when a user performs COMMIT or ROLLBACK, or terminates the connection.

A subprogram module created by GOLDILOCKS PSM is a statement which does not uses its own transaction, so a new transaction does not occur when the subprogram is called.

However, to guarantee atomicity of the SQL statement, the available SQL types in a subprogram may vary depending on the case of calling the subprogram.

- When a user directly calls a subprogram module by using CALL statement, or performs an anonymous block
    - A superordinate statement does not exists, so all kinds of SQL can be used within a subprogram and COMMIT/ROLLBACK is also allowed.
- When a subprogram module is used within a DML statement (INSERT/UPDATE/DELETE) except for SELECT
    - A superordinate statement has a transaction, so all kinds of SQL can be used within a subprogram. However, to guarantee the atomicity of the superordinate statement, neither COMMIT nor ROLLBACK is allowed.
- When a subprogram module is called within a SELECT statement
    - A superordinate statement does not use a transaction, so any kind of SQL using a transaction can not be used even within a called subprogram, nor is COMMIT/ROLLBACK allowed. Only SELECT statement is allowed.

---

[← 20. SQL References (H~Z)](../part-03-sql-manual/20-sql-references-h-z.md) · [Table of contents](../README.md) · [22. PSM DataTypes →](22-psm-datatypes.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
