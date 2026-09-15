<a id="c8a5addde6ef3dc8"></a>

# 17. Overview of PSM

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/c8a5addde6ef3dc8)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 16. SQL References](../part-03-sql-manual/16-sql-references.md) · [Table of contents](../README.md) · [18. PSM DataTypes →](18-psm-datatypes.md)

<a id="3af4f0b010406e80"></a>
## Features of PSM

<a id="6a5170bd16cce3b4"></a>
### Closely Interworking with SQL

GOLIDILOCKS PSM can closely interworks with GOLDILOCKS SQL.

- It supports all data types supported by GOLDILOCKS SQL.
- It supports an attribute type (%TYPE, %ROWTYPE), so a flexible tables and column types are available.
- It supports all operators and built-in functions supported by GOLDILOCKS SQL.
- It supports all DML, DCL (COMMIT/ROLLBACK) supported by GOLDILOCKS SQL.
- It supports SQL SELECT statements by declaring a cursor and using OPEN, FETCH, CLOSE statements.
- It supports SQL DDL statements through the dynamic SQL feature.

<a id="6267d2ee6e82dabb"></a>
### Improving Performance

GOLDILOCKS PSM is operated only within a server, so it reduces the number of communications between the user application and the DBMS server. Therefore, the overall performance is improved.

<a id="5b23507324f48d7b"></a>
### Improving Productivity

The language of GOLDILOCKS PSM is quite similar to that of script, a less effort is required to write a code for the desired feature. The time of writing a client application can be reduced if the procedure and funcure is created by modularizing the user's work logic.

<a id="05805a295340802a"></a>
### Portability

Procedures and functions created by GOLDILOCKS PSM can also be used in ODBC, JDBC, an embedded SQL, and various development tools in the same way. Also, it can be easily transplanted in a different platform regardless of the platform type of server or a client.

<a id="3fcbca2ca0dd3216"></a>
### Easy Maintenance

GOLDILOCKS PSM is implemented into a single module in a server from each similar logics in separate clients. Therefore, it is easy to manage, and enable to modify when it is in need even during the module is in use.

<a id="575bbf90e6d47450"></a>
## Language Elements

<a id="8478bf2c891615f2"></a>
### Data Types

GOLDILOCKS PSM provides all built-in data types provided by GOLDILOCKS SQL, and it even supports user defined records and collection types.  
For more information, refer to [PSM DataTypes](18-psm-datatypes.md#fc4c07f6fbc6efb4).

<a id="ce205b090422d4af"></a>
### Variables

Required variables declared by a user in GOLDILOCKS PSM can be used in all expressions.

For more information, refer to the followings.  
• [Declarative Part](19-psm-control-statements.md#bb7e43eadb147992)  
• [Assignment](19-psm-control-statements.md#5e7672b01eb73314)

<a id="134075c64cbd047e"></a>
### Control Structures

GOLDILOCKS PSM supports most of decision branch statements, unconditional branch statements (GOTO),  loop statement for repeated executions which were provided by a general script language.  
For more information, refer to [PSM Control Statements](19-psm-control-statements.md#c82d9a6259d3acfb).

<a id="31543472760b1ed9"></a>
### Subprograms

GOLDILOCKS PSM subprogram is a PSM block with a name and it can be repeatedly performed. If a subprogramd has an argument, then it can be performed by being given different arguments when each time it is called.   
Subprogram is either in a procedure form or a function form, and the function form has a return value. It also supports a nested subprogram which is declared in a specific block and used within it.  
For more information, refer to [Using PSM Subprograms](21-using-psm-subprograms.md#76c72d3f4b0291c3).

<a id="2b1bdf6cca62cd3d"></a>
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

[← 16. SQL References](../part-03-sql-manual/16-sql-references.md) · [Table of contents](../README.md) · [18. PSM DataTypes →](18-psm-datatypes.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
