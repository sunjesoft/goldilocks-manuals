<a id="2d83252f81a40d12"></a>

# 19. Overview of PSM

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/2d83252f81a40d12)  
> Tag: `20c.1_30_tag`

[← 18. SQL References](../part-03-sql-manual/18-sql-references.md) · [Table of contents](../README.md) · [20. PSM DataTypes →](20-psm-datatypes.md)

<a id="8f63705e047b846f"></a>
## Features of PSM

<a id="048b85269d295b86"></a>
### Closely Interworking with SQL

GOLIDILOCKS PSM can closely interworks with GOLDILOCKS SQL.

- It supports all data types supported by GOLDILOCKS SQL.
- It supports an attribute type (%TYPE, %ROWTYPE), so a flexible tables and column types are available.
- It supports all operators and built-in functions supported by GOLDILOCKS SQL.
- It supports all DML, DCL (COMMIT/ROLLBACK) supported by GOLDILOCKS SQL.
- It supports SQL SELECT statements by declaring a cursor and using OPEN, FETCH, CLOSE statements.
- It supports SQL DDL statements through the dynamic SQL feature.

<a id="a96cd3d5ef739615"></a>
### Improving Performance

GOLDILOCKS PSM is operated only within a server, so it reduces the number of communications between the user application and the DBMS server. Therefore, the overall performance is improved.

<a id="57faa25a9ac7dc90"></a>
### Improving Productivity

The language of GOLDILOCKS PSM is quite similar to that of script, a less effort is required to write a code for the desired feature. The time of writing a client application can be reduced if the procedure and funcure is created by modularizing the user's work logic.

<a id="c1938bd3076378d0"></a>
### Portability

Procedures and functions created by GOLDILOCKS PSM can also be used in ODBC, JDBC, an embedded SQL, and various development tools in the same way. Also, it can be easily transplanted in a different platform regardless of the platform type of server or a client.

<a id="522a4b4c062c6414"></a>
### Easy Maintenance

GOLDILOCKS PSM is implemented into a single module in a server from each similar logics in separate clients. Therefore, it is easy to manage, and enable to modify when it is in need even during the module is in use.

<a id="8cd1fa81cb2d1170"></a>
## Language Elements

<a id="3acf07a471ca21f1"></a>
### Data Types

GOLDILOCKS PSM provides all built-in data types provided by GOLDILOCKS SQL, and it even supports user defined records and collection types.  
For more information, refer to [PSM DataTypes](20-psm-datatypes.md#8c878b276a789b32).

<a id="6b6a7afd7435192c"></a>
### Variables

Required variables declared by a user in GOLDILOCKS PSM can be used in all expressions.

For more information, refer to the followings.  
• [Declarative Part](21-psm-control-statements.md#7c016b20e103c650)  
• [Assignment](21-psm-control-statements.md#40afa4f298bee66f)

<a id="530d458744daa6c5"></a>
### Control Structures

GOLDILOCKS PSM supports most of decision branch statements, unconditional branch statements (GOTO),  loop statement for repeated executions which were provided by a general script language.  
For more information, refer to [PSM Control Statements](21-psm-control-statements.md#bce0bc9bfd2028a5).

<a id="371548090a86b9c7"></a>
### Subprograms

GOLDILOCKS PSM subprogram is a PSM block with a name and it can be repeatedly performed. If a subprogramd has an argument, then it can be performed by being given different arguments when each time it is called.   
Subprogram is either in a procedure form or a function form, and the function form has a return value. It also supports a nested subprogram which is declared in a specific block and used within it.  
For more information, refer to [Using PSM Subprograms](23-using-psm-subprograms.md#9a3ecbd47d79a3b6).

<a id="f1b878574c508370"></a>
## Processing Transaction in PSM

A database transaction is a work unit which consists of one or more of SQL statements and it can not be disassembled. The followings are SQL statements which use transactions in GOLDILOCKS database.

- DML except for SELECT statements
- All DDL

A transaction starts in the following cases.

- When performing SQL which uses a transaction for the first time immediately after the connection.
- When performing SQL which uses a transaction for the first time since COMMIT or ROLLBACK

A transaction ends when a user performs COMMIT or ROLLBACK, or terminates the connection.

A subprogram module created by GOLDILOCKS PSM is a statement which does not uses its own transaction, so a new transaction does not occur when the subprogram is called.

However, to guarantee atomicity of the SQL statement, the the available SQL types in a subprogram may vary depending on the case of calling the subprogram.

- When a user directly calls a subprogram module by using CALL statement, or performs an anonymous block
    - A superordinate statement does not exists, so all kinds of SQL can be used within a subprogram and COMMIT/ROLLBACK is also allowed.
- When a subprogram module is used within a DML statement (INSERT/UPDATE/DELETE) except for SELECT
    - A superordinate statement has a transaction, so all kinds of SQL can be used within a subprogram. However, to guarantee the atomicity of the superordinate statement, neither COMMIT nor ROLLBACK is allowed.
- When a subprogram module is called within a SELECT statement
    - A superordinate statement does not use a transaction, so any kind of SQL using a transaction can not be used even within a called subprogram, nor is COMMIT/ROLLBACK allowed. Only SELECT statement is allowed.

---

[← 18. SQL References](../part-03-sql-manual/18-sql-references.md) · [Table of contents](../README.md) · [20. PSM DataTypes →](20-psm-datatypes.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
