<a id="e55138d4a45c4fa0"></a>

# 30. PSM Language Element References

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/e55138d4a45c4fa0)  
> Tag: `26c.1_0_tag`

[← 29. Trigger](29-trigger.md) · [Table of contents](../README.md) · [31. PSM SQL References →](31-psm-sql-references.md)

<a id="4261efb6b3bbcaf2"></a>
## Assignment Statement

<a id="e36444db362cf667"></a>
### Function

Within a PSM block, it stores a value in a variable or in an out-bind parameter.

<a id="a4f8862b358b9f80"></a>
### Syntax

```
<assignment statement> ::=
    <assignment target> := <value expression>
    ;

<assignment target> ::=
      collection_variable ( index )
    | cursor_variable
    | :host_cursor_variable
    | out_parameter
    | :host_variable [ :indicator_variable ]
    | record_variable . field_name
    | scalar_variable
```

<a id="adb643d584019335"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="e26313d4c936b253"></a>
### Syntax Rules and Parameters

- collection_variable
    - It is the variable name of COLLECTION type declared in DECLARE section.
- index
    - It is the key value that selects an element among elements of collection_variable.
- cursor_variable
    - It is the cursor name declared in DECLARE section.
- host_variable
    - It is the name of out/ in-out type client-side variable which is transferred from where calling PSM.
- indicator_variable
    - It is the indicator variable name to check the NULL value of host_variable and to find out the actual length of the value.
- record_variable
    - It is the variable name of RECORD type which has already been declared in DECLARE section.
- field_name
    - It is the name of a field among fields included in a RECORD type variable.
- scalar_variable
    - It is the variable name of a general scalar type which has already been declared in DECLARE section.

<a id="5454809d85f1eeaf"></a>
### Description

Targets of assignment statements are classified into an external bind parameter and an internal PSM variable.

- External parameter 
    - Host variable 
    - Host cursor variable 
- Internal variable 
    - Out type function argument 
    - Internally declared variable
        - Scalar/ record/ multi-set type 
        - A specific field of a record type variable
        - A specific element of multi-set type variable

All variables except for a procedure/ function parameter can have a name assigning a scope.

<a id="6164b0150efead76"></a>
### Examples

The following is an example of using an assignment statement.

- Assignment for PSM internal variable

```
gSQL> DECLARE
  V1 INTEGER := 0;
BEGIN
  FOR I IN 1..10 LOOP
    V1 := V1 + I;
  END LOOP;
  DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
END;
/

V1 = 55

Anonymous PL block executed.
```

- Assignment for a host variable

```
gSQL> \var P1 INTEGER

gSQL> 
BEGIN
  :P1 := 100;
END;
/

gSQL> \print P1 
 P1
---
100

Anonymous PL block executed.
```

<a id="0c29fb5cb502bb37"></a>
### Compatibility

The differences between an assignment statement of GOLDILOCKS and that of SQL standard are as follows.

- An assignment statement of the SQL standard defines a singleton variable assignment and a multiple variable assignment, but GOLDILOCKS supports only a singleton variable assignment. 
- An assignment statement of the SQL standard starts with SET keyword, but GOLDILOCKS does not use SET keyword. 
- An assignment statement of the SQL standard uses an equal operator (=) between a target and a value, but GOLDILOCKS uses :=.

**SQL standard compatibility**

<a id="6c121be721fc1d30"></a>
<table><tbody><tr><th align="center">Feature ID</th><th align="center">Description</th><th align="center">Compatibility</th></tr><tr><td align="left">P002</td><td align="left">Computational completeness</td><td align="center">X</td></tr><tr><td align="left">P006</td><td align="left">Multiple assignment</td><td align="center">X</td></tr></tbody></table>

<a id="351355ef69ab7e52"></a>
### For More Information

Refer to the following.

- [Scalar Variable Declaration](#08c1c75dd4095e4d)
- [Record Variable Declaration](#27a37ec216747a75)
- [COLLECTION Variable Declaration](#81da60b6816d1d33)
- [Cursor Variable Declaration](#2b78435faeadac86)

<a id="20e8e5a8347535a1"></a>
## Basic LOOP Statement

<a id="be068070ac007d7e"></a>
### Function

It repeatedly performs statements within LOOP until the LOOP is terminated by performing GOTO or EXIT.

<a id="1a32f51d3ac69298"></a>
### Syntax

```
<basic loop statement> ::=
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="a6667764dabecc8f"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="6ff16e8bcb0b5956"></a>
### Syntax Rules and Parameters

- loop_name
    - It is the label name of &lt;basic loop statement&gt;. 
    - Its role is only a comment, so it does not matter even when it is different from the real label name of &lt;basic loop statement&gt;.

<a id="2be5c7d8ae33edbb"></a>
### Description

A basic loop statement is repeatedly performs statements within LOOP.  
A basic loop statement is a loop-family statement, so it can be a target statement which GOTO, EXIT, and CONTINUE indicates as a label.

<a id="d0fb9e4056e66916"></a>
### Examples

```
DECLARE
  V1 INTEGER := 1;
BEGIN
  LOOP
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
    V1 := V1 + 1;
    EXIT WHEN V1 > 2;
  END LOOP;
END;
/
V1 = 1 
V1 = 2 

Anonymous PL block executed.
```

<a id="775f16e9a759a50f"></a>
### Compatibility

&lt;basic loop statement&gt; statement is the same as &lt;loop statement&gt; of the SQL standard.

**SQL standard compatibility**

<a id="c6a5105b90d8ab0e"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="af375d6573a3773c"></a>
### For More Information

Refer to the following.

- [CONTINUE Statement](#02a73511f88bd73d)
- [EXIT Statement](#d41640b5f286a508)
- [GOTO Statement](#82bb91693962eb5e)

<a id="acfcdb439eaed2a5"></a>
## Block (BEGIN .. END)

<a id="c5f241dd80aee9e6"></a>
### Function

It defines a variable, a type, a cursor and an exception, and groups a pl statement to execute.

<a id="81ed2bbb404eba88"></a>
### Syntax

```
<PSM block> ::=
    [ <label list> ]
    [ DECLARE ]
    [ <declare item list> ] 
    <body>
    ;

<label list> ::=
    << <label name> >> 
    [ ... ]

 <declare item list>
     <declare item> 
     [ ... ]

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

<body> ::=
      BEGIN
      <pl statement list>
      [ <exception block> ]
      END [ <name> ]

<pl statement list> ::=
      [ <label list> ] <pl_statement>
      [ ... ]

<pl statement> ::=
      <assignment statement>
    | <basic loop statement>
    | <block statement>
    | <case statement>
    | <close statement>
    | <collection method invocation>
    | <continue statement>
    | <cursor for loop statement>
    | <delete statement extension>
    | <execute immediate statement>
    | <exit statement>
    | <fetch statement>
    | <for loop statement>
    | <goto statement>
    | <if statement>
    | <insert statement extension>
    | <insert into ... update statement extension>
    | <merge statement extension>
    | <null statement>
    | <open statement>
    | <open for statement>
    | <procedure call statement>
    | <raise statement>
    | <return statement>
    | <return table statement>
    | <select into statement>
    | <sql statement>
    | <update statement extension>
    | <while loop statement>

<sql statement> ::=
      <savepoint statement>
    | <release savepoint statement>
    | <rollback statement>
    | <commit statement>
    | <lock table statement>

<exception block> ::=
      EXCEPTION <exception handler list>

<exception handler list> ::=
      <exception handler> [ ... ]

<exception handler> ::=
      WHEN 
      { <exception list> | OTHERS }
      THEN
      <pl statement list>

<exception list> ::=
      <exception> [ OR ... ]
```

<a id="79db687baa7ae884"></a>
### Invocation and Access Rules

It can be used only within PROCEDURE, FUNCTION, PACKAGE BODY or an anonymous block.

<a id="54b6c504bf78ed3f"></a>
### Syntax Rules and Parameters

<a id="79f70d108572644c"></a>
#### &lt;&lt; label name &gt;&gt;

The label name is a unique identifier for the block, and it is undeclared specifier.  
The length of a cursor name should be shorter than 128 bytes.

<a id="bfd9906c09fe918a"></a>
#### declare item

- Variable declaration
    - It declares the variable, and the following datatype of the variable can be declared. 
        - scalar type
        - record type
        - associate array type
        - reference cursor type
- Type definition
    - It defines a user-defined type.
        - record type
        - associate array type
        - reference cursor type
- Explicit cursor declaration
    - It declares an explicit cursor.
- Explicit cursor definition
    - It defines an explicit cursor.
- Exception declaration
    - It declares an exception variable.
- Exception init pragma
    - It matches the exception declared by a user with the error code in GOLDILOCKS.
- Procedure declaration
    - It declares a procedure.
- Procedure definition
    - It defines a procedure.
- Function declaration
    - It declares a function.
- Function definition
    - It defines a function.

<a id="e8aa6812ed46aafd"></a>
#### body

It is the beginning of executing &lt;PSM block&gt;.  
&lt;body&gt; consists of the executable &lt;pl statement list&gt; and &lt;exception block&gt; for exception handling.

<a id="2df195fa049547d0"></a>
#### pl statement

- assignment statement
    - Refer to [Assignment Statement](#4261efb6b3bbcaf2).
- basic loop statement
    - Refer to [Basic LOOP Statement](#20e8e5a8347535a1).
- block statement
    - Refer to [Block (BEGIN .. END)](#acfcdb439eaed2a5).
- case statement
    - Refer to [CASE Statement](#f8113628a8bee98f).
- close statement
    - Refer to [CLOSE Statement](#be3b8f9c4ae5e8b7).
- collection method invocation
    - Refer to [Collection Method Invocation](#a05c8c71944116f4).
- continue statement
    - Refer to [CONTINUE Statement](#02a73511f88bd73d).
- cursor for loop statement
    - Refer to [Cursor FOR LOOP Statement](#cca7ad1d7d92e4de).
- delete statement extension
    - Refer to [DELETE Statement Extension](#a2dbb0a0acf3741e).
- execute immediate statement
    - Refer to [EXECUTE IMMEDIATE Statement](#0d4e109b14705c96).
- exit statement
    - Refer to [EXIT Statement](#d41640b5f286a508).
- fetch statement
    - Refer to [FETCH Statement](#eded620a01801e55).
- for loop statement
    - Refer to [FOR LOOP Statement](#8eb927ba8d4f181c).
- goto statement
    - Refer to [GOTO Statement](#82bb91693962eb5e).
- if statement
    - Refer to [IF Statement](#8d14b69600360332).
- insert statement extension
    - Refer to [INSERT Statement Extension](#8ba7356240cd29cd).
- insert into ... update statement extension
    - Refer to [INSERT INTO ... UPDATE Statement Extension](#a6c8cd4e6ef22c56).
- merge statement extension
    - Refer to [MERGE Statement Extension](#ce2b52a3e196e8cd).
- null statement
    - Refer to [NULL Statement](#96d51677cf5459a5).
- open statement
    - Refer to [OPEN Statement](#bf1f4e379445065f).
- open for statement
    - Refer to [OPEN FOR Statement](#326b0ac4f8704e21).
- procedure call statement
    - Refer to [Procedure Call](#32725e0b99b728ac).
- raise statement
    - Refer to [RAISE Statement](#4689eec7814aee0e).
- return statement
    - Refer to [RETURN Statement](#1ec88e9f3a1b14ed).
- return table statement
    - Refer to [RETURN TABLE Statement](#06f1e071dedbe4f2).
- select into statement
    - Refer to [SELECT INTO Statement](#25c07665814250e4).
- sql statement
    - savepoint statement
        - Refer to [SAVEPOINT savepoint_specifier](../part-03-sql-manual/20-sql-references-h-z.md#79cec2425d42b60f).
    - release savepoint statement
        - Refer to [RELEASE SAVEPOINT savepoint_specifier](../part-03-sql-manual/20-sql-references-h-z.md#965ceb9eced025a5).
    - rollback statement
        - Refer to [ROLLBACK](../part-03-sql-manual/20-sql-references-h-z.md#a7f186a4dca1588e).
    - commit statement
        - Refer to [COMMIT](../part-03-sql-manual/19-sql-references-c-g.md#3beee453ea244831).
    - lock table statement
        - Refer to [LOCK TABLE](../part-03-sql-manual/20-sql-references-h-z.md#41362c316d3f7f25).
- update statement extension
    - Refer to [UPDATE Statement Extension](#0a1eff9c02b8d066).
- while loop statement
    - Refer to [WHILE LOOP Statement](#9abf0ef3a214066f).

<a id="947f3335e1a72b3b"></a>
#### exception block

It handles the exceptional situation which occurs while executing &lt;psm block&gt;.  
&lt;exception&gt; is a name of a predefined exception defined in GOLDILOCKS or a user-defined exception.   
If the specified exception occurs, then the corresponding &lt;pl statement list&gt; is executed.

<a id="a5b89c3f503e7b5a"></a>
### Description

&lt;psm block&gt; is a basic component of PSM.  
A block can have a declaration part and a exception handling part.  
A block can be duplicated, and the duplicated block has a new subordinate variable scope. A superordinate block can not refer to a variable in a subordinate block.

<a id="4c0ea2278ad0ee89"></a>
### Examples

```
gSQL> 
<<MAIN>>
DECLARE
  V1 INTEGER := 1;
BEGIN
  DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
  <<SUB1>>
  DECLARE
    V1 VARCHAR(10) := 'ABC';
  BEGIN
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
    DBMS_OUTPUT.PUT_LINE( 'SUB1.V1 = ' || SUB1.V1 );
    DBMS_OUTPUT.PUT_LINE( 'MAIN.V1 = ' || MAIN.V1 );
 END;
END;
/
V1 = 1
V1 = ABC
SUB1.V1 = ABC
MAIN.V1 = 1

Anonymous PL block executed.
```

<a id="c7e9ace407667757"></a>
### Compatibility

&lt;compound statement&gt; of the SQL standard defines ATOMIC /NOT ATOMIC statement which specifies a new savepoint, but GOLDILOCKS does not support it.

**SQL standard compatibility**

<a id="82f477a50c342e25"></a>
| Feature ID | Description | Remarks |
| --- | --- | --- |
| P002 | Computational completeness | It does not support ATOMIC statement. |

<a id="84ecd55729004bfd"></a>
### For More Information

Refer to [Overview of PSM](21-overview-of-psm.md#fa6943adc6ba8583).

<a id="f24bb921ad663f66"></a>
## Call Specification

<a id="69a9d857450be591"></a>
### Function

It maps the information corresponding to the function name, the parameter data type and the RETURN data type of the program which were written with C, to call it in PSM.

<a id="87d12f5c694d8f76"></a>
### Syntax

```
<call specification> ::= 
      <c declaration>  
      ; 
 
<c declaration> ::= 
      LANGUAGE C 
      <library clause> 
      [ WITH CONTEXT ] 
      <external parameters> 
 
<library clause> ::= 
      LIBRARY <library name> NAME <double_quote_string>
    | NAME <double_quote_string> LIBRARY <library name>    
 
<external parameters> ::= 
      PARAMETER ( [ <external parameter list> ] ) 
 
<external parameter list> ::= 
      <external parameter>  
     
<external parameter> ::= 
      CONTEXT
    | <parameter name> [ <property> ] [ BY REFERENCE ] <external datatype> 
    | RETURN [ <property> ] [ BY REFERENCE ] <external datatype> 
 
<property> ::= 
       INDICATOR 
     | LENGTH 
     | MAXLEN 
 
<external datatype> ::= 
       UNSIGNED CHAR 
     | CHAR 
     | UNSIGNED SHORT 
     | SHORT 
     | UNSIGNED INT 
     | INT 
     | UNSIGNED LONG 
     | LONG 
     | FLOAT 
     | DOUBLE 
     | STRING 
     | RAW 
     | SQL_LONG_VARIABLE_LENGTH 
     | SQL_NUMERIC 
     | SQL_DATE 
     | SQL_TIME 
     | SQL_TIME_TZ 
     | SQL_TIMESTAMP 
     | SQL_TIMESTAMP_TZ 
     | SQL_INTERNAL
```

<a id="b2ffb637dbd5eb61"></a>
### Invocation and Access Rules

One of the following privileges is required to use a library in &lt;library clause&gt;.

- EXECUTE privilege for the library
- ( EXECUTE LIBRARY or CONTROL SCHEMA ) ON SCHEMA for the schema to which the library belongs 
- EXECUTE ANY LIBRARY ON DATABASE

<a id="f8cc17b88a720221"></a>
### Syntax Rules and Parameters

<a id="062a5606b079a007"></a>
#### LANGUAGE C

It is an external program written in C language.

<a id="bdef5b60c34ec39b"></a>
#### LIBRARY &lt;library name&gt;

It is the name of the library object created with [CREATE LIBRARY](31-psm-sql-references.md#d3c4a1abc483c544) statement.  
It can specify the schema as &lt;schema_name&gt;.&lt;library name&gt;.

<a id="0508818b4ab81127"></a>
#### NAME &lt;double_quote_string&gt;

It displays the function name of the program written in C.  
The function name enclosed with "" should be smaller than 128 bytes.

<a id="43dc91d467b7af23"></a>
#### external parameter

It maps the data types of parameter of a procedure or a function, and of the parameter of the external C function.

- CONTEXT
    - It can access the exception and the memory allocation in an external C function.
- parameter name
    - It is the parameter name of a procedure or a function.
    - All parameters specified in the procedure or the function should be specified. 
    - RETURN of the function should be specified last.
- property
    - INDICATOR
        - It is the property which supports indicating whether the value of a parameter or return is NULL.
        - If the indicator variable is SQL_NULL_DATA, then the corresponding parameter or the return value is NULL.
        - If the indicator variable is not SQL_NULL_DATA, then the corresponding parameter or the return value is not NULL.
    - LENGTH
        - It indicates the current length of a string, RAW type parameter or RETURN.
        - For IN Parameter, LENGTH is transferred to the value.
        - OUT, IN OUT parameter and RETURN are transferred to the pointer.
    - MAXLEN
        - It indicates maximum length of the string, RAW type parameter or RETURN.
        - IN, OUT, IN OUT parameter and RETURN are transferred to the value.
- BY REFERENCE
    - If the parameter of C function is the pointer type, then it specifies BY REFERENCE statement in IN parameter of the routine and transfers it.
- external datatype
    - It maps the datatype of SQL parameter and the data type of the external parameter.
    - For more information, refer to [Parameter Data Type Mapping](28-external-routine.md#6b0591097506393d) of [External Routine](28-external-routine.md#2fb71bf0a9a14e30).

<a id="94537455f3ef9dec"></a>
### Description

&lt;call specification&gt; statement maps the information corresponding to the external C function name, parameter datatype and RETURN datatype.

&lt;call specification&gt; can be used in the following statements.

- [CREATE FUNCTION](31-psm-sql-references.md#8343c001bfba29fc)
- [CREATE PROCEDURE](31-psm-sql-references.md#d439613cbc283235)
- [CREATE PACKAGE](31-psm-sql-references.md#d67c80375fa9e3c8)
- [CREATE PACKAGE BODY](31-psm-sql-references.md#397f0c3a716022e0)

It can not be used in &lt;body&gt; of PL/SQL block.

<a id="0575444dc5c81042"></a>
### Examples

```
gSQL>
CREATE OR REPLACE FUNCTION func1( p1 NATIVE_INTEGER,
                                  p2 NATIVE_INTEGER )
    RETURN NATIVE_INTEGER AS
LANGUAGE C
LIBRARY lib1 NAME "add"
PARAMETERS ( p1 INT ,
             p2 INT ,
             RETURN INT );
/

Function created.
```

<a id="daec87ea4193da0b"></a>
### Compatibility

The SQL standard does not define it.  
It is similar to &lt;external body reference&gt; of the SQL standard.

<a id="ec577120997f2eef"></a>
### For More Information

Refer to [External Routine](28-external-routine.md#2fb71bf0a9a14e30).

<a id="f8113628a8bee98f"></a>
## CASE Statement

<a id="7da79efda16d9bb5"></a>
### Function

It performs a statement list satisfying conditions which returns TRUE among given conditions.

<a id="5621146cb7a1f514"></a>
### Syntax

```
<case statement> ::=
    <simple case statement>
    | <searched case statement>
    ;

<simple case statement> ::=
    CASE <case operand> <simple case statement when clause>...
    [ <case statement else clase> ]
    END CASE

<searched case statement> ::=
    CASE <searched case statement when clause>...
    [ <case statement else clase> ]
    END CASE

<simple case statement when clause> ::=
    WHEN <when operand>
        THEN <executable statement list>

<searched case statement when clause> ::=
    WHEN <search condition>
        THEN <executable statement list>
```

<a id="5cd24c5087701d59"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="67c48a41431267f5"></a>
### Syntax Rules and Parameters

- Case operand
    - They are all expressions which can be evaluated with a scalar value. 
    - However, it can not include a subquery statement.
- When operand
    - It is an expression to compare whether it is the same as &lt;case operand&gt;.
    - However, it can not include a subquery statement.
- Search condition
    - It is a conditional expression to be performed when the evaluation result of &lt;searched case statement&gt; is TRUE.
    - However, it can not include a subquery statement.
- Executable statement list
    - It is a list of all statements which can be performed within PSM.

<a id="c0e3134c41e3a547"></a>
### Description

It performs statements in WHEN clause returning TRUE by evaluating conditions like as IF statement.  
It evaluates conditional expressions in order, and stops evaluating after finding the TRUE conditional clause.  
If the case satisfying the condition does not exist and ELSE clause is not specified, then an error occurs.

<a id="f4d600a16ab40b2b"></a>
### Examples

<a id="60b3be492420ef4f"></a>
#### Using a Simple CASE

```
gSQL> DECLARE
V1 integer := 0;
BEGIN
  SELECT 2 INTO V1 FROM DUAL;

  CASE V1 WHEN 0 THEN DBMS_OUTPUT.PUT_LINE ('Result = 0');
          WHEN 1 THEN DBMS_OUTPUT.PUT_LINE ('Result = 1');
          WHEN 2 THEN DBMS_OUTPUT.PUT_LINE ('Result = 2');
          ELSE DBMS_OUTPUT.PUT_LINE ('Result = OTHER');
  END CASE;
END;
/
Result = 2

Anonymous PL block executed.
```

<a id="61cecf6ed3250ac6"></a>
#### Using a Searched CASE

```
gSQL> DECLARE
V1 integer := 0;
BEGIN
  SELECT 2 INTO V1 FROM DUAL;

  CASE WHEN V1 = 0 THEN DBMS_OUTPUT.PUT_LINE ('Result = 0');
       WHEN V1 = 1 THEN DBMS_OUTPUT.PUT_LINE ('Result = 1');
       WHEN V1 = 2 THEN DBMS_OUTPUT.PUT_LINE ('Result = 2');
       ELSE DBMS_OUTPUT.PUT_LINE ('Result = OTHER');
  END CASE;
END;
/
Result = 2

Anonymous PL block executed.
```

<a id="a42f6cdd2629cf8a"></a>
### Compatibility

CASE statement of the SQL standard defines the comparison of row type (list type) values, but GOLDILOCKS does not support it.  
CASE statement of the SQL standard can define multiple conditions in a list in &lt;when operand&gt; by delimiting them with ',', but GODILOCKS does not support it.

**SQL stantard compatibility**

<a id="a2cae6795b5cb5eb"></a>
| Feature ID | Description | Remarks |
| --- | --- | --- |
| P002 | Computational completeness | It does not support P004, P008. |
| P004 | Extended CASE statement | - |
| P008 | Comma-separated predicates in simple CASE statement | - |

<a id="be3b8f9c4ae5e8b7"></a>
## CLOSE Statement

<a id="c7b467479b23e400"></a>
### Function

It closes an open cursor.

<a id="5324e065859c2b7d"></a>
### Syntax

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="496aa5fd0c2c4432"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="db32c837aecfbbcb"></a>
### Syntax Rules and Parameters

- cursor_name
    - It is the name of a cursor to be closed.

<a id="c3a372957b82f2ce"></a>
### Description

It closes an open cursor.  
A closed cursor can be opened again by using an open statement.

<a id="2f7b0c0eddc1e9a2"></a>
### Examples

```
gSQL> CREATE TABLE T1 ( I1 INTEGER );

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> DECLARE
  CURSOR C1 IS SELECT I1 FROM T1;
  V1 T1%ROWTYPE;
BEGIN
  OPEN C1;
  FETCH C1 INTO V1;

  CLOSE C1;
END;
/

Anonymous PL block executed.
```

<a id="fd8812f6706ff8cc"></a>
### Compatibility

The SQL standard does not define it.

<a id="1efe6e10593fd8d2"></a>
### For More Information

Refer to the following.

- [FETCH Statement](#eded620a01801e55)
- [OPEN Statement](#bf1f4e379445065f)

<a id="a05c8c71944116f4"></a>
## Collection Method Invocation

<a id="f6e436bb2ea7bf18"></a>
### Function

It provides a method which can explores a collection type variable.

<a id="d1e3ae402ea32c15"></a>
### Syntax

```
<collection method> ::=
         variable_name . <method>
    ;

<method> ::=
        first ()
      | last  ()
      | prior ( expression )
      | next  ( expression )
      | count ()
      | exists ( expression )
      | delete ( expression )
```

<a id="08d213e2eb6b6a67"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="67728840dd668ac2"></a>
### Syntax Rules and Parameters

- It can be used only in a variable declared as a collection type.
- FIRST, LAST, COUNT can not have a parameter.
- A parameter should be specified when an object should be specified such as PRIOR, NEXT, EXISTS, DELETE.
- DELETE is operated the same as PSM statement, and it can not return a different variable as a result. (It can not be used in an expression.)

<a id="fcec3dd19acbd719"></a>
### Description

Refer to the following table.

**Function**

<a id="54eb541717d61910"></a>
| Name | Function | Return value | Whether to  require an argument |
| --- | --- | --- | --- |
| FIRST | It returns the smallest key. | A key type specified in INDEX OF | X |
| LAST | It returns the biggest key. | A key type specified in INDEX OF | X |
| PRIOR | It returns a key smaller than the input key. | A key type specified in INDEX OF | O |
| NEXT | It returns a key bigger than the input key. | A key type specified in INDEX OF | O |
| COUNT | It returns the stored count. | INTEGER | X |
| DELETE | It deletes a value corresponding to a key. | N/A | O |
| EXISTS | It returns whether a key exists or not. | BOOLEAN | O |

<a id="1935e216f0c774fa"></a>
### Examples

```
DECLARE
TYPE rec IS TABLE OF VARCHAR(20) INDEX BY VARCHAR(20);
v1 rec;
v2 VARCHAR(20);
BEGIN
  DBMS_OUTPUT.PUT_LINE( '------------------------------------');
  DBMS_OUTPUT.PUT_LINE( 'first = ' || v1.first);
  DBMS_OUTPUT.PUT_LINE( 'last = '  || v1.last);
  DBMS_OUTPUT.PUT_LINE( 'prior = ' || v1.prior('aaa'));
  DBMS_OUTPUT.PUT_LINE( 'next = '  || v1.next('aaa'));
  DBMS_OUTPUT.PUT_LINE( 'count = ' || v1.count());

  FOR I IN 1 .. 9
  LOOP
      v1('a' || to_char(i)) := 'a' || to_char(i);
  END LOOP;

  DBMS_OUTPUT.PUT_LINE( '------------------------------------');
  DBMS_OUTPUT.PUT_LINE( 'first = ' || v1.first);
  DBMS_OUTPUT.PUT_LINE( 'last = '  || v1.last);
  DBMS_OUTPUT.PUT_LINE( 'count = ' || v1.count());

  DBMS_OUTPUT.PUT_LINE( '------------------------------------');
  DBMS_OUTPUT.PUT_LINE( 'Print all from first to last');
  v2 := v1.first;
  WHILE v2 IS NOT NULL
  LOOP
      DBMS_OUTPUT.PUT_LINE('Key= ' || v2 || ',Value=' || v1(v2));
      v2 := v1.next(v2);
  END LOOP;

  DBMS_OUTPUT.PUT_LINE( '------------------------------------');
  DBMS_OUTPUT.PUT_LINE( 'Print all from last to first');
  v2 := v1.last;
  WHILE v2 IS NOT NULL
  LOOP
      DBMS_OUTPUT.PUT_LINE('Key= ' || v2 || ',Value=' || v1(v2));
      v2 := v1.prior(v2);
  END LOOP;

  v1.delete(v1.first());
  DBMS_OUTPUT.PUT_LINE('count = ' || v1.count() );
  DBMS_OUTPUT.PUT_LINE('first = ' || v1.first() );

END;
/
------------------------------------
first = 
last = 
prior = 
next = 
count = 0
------------------------------------
first = a1
last = a9
count = 9
------------------------------------
Print all from first to last
Key= a1,Value=a1
Key= a2,Value=a2
Key= a3,Value=a3
Key= a4,Value=a4
Key= a5,Value=a5
Key= a6,Value=a6
Key= a7,Value=a7
Key= a8,Value=a8
Key= a9,Value=a9
------------------------------------
Print all from last to first
Key= a9,Value=a9
Key= a8,Value=a8
Key= a7,Value=a7
Key= a6,Value=a6
Key= a5,Value=a5
Key= a4,Value=a4
Key= a3,Value=a3
Key= a2,Value=a2
Key= a1,Value=a1
count = 8
first = a2

Anonymous PL block executed.
```

<a id="b241a5bd04a54375"></a>
### For More Information

Refer to [COLLECTION Variable Declaration](#81da60b6816d1d33).

<a id="81da60b6816d1d33"></a>
## COLLECTION Variable Declaration

<a id="5e524ff8a5a05152"></a>
### Function

It declares a collection variable.

<a id="2f1a8025a7b415cc"></a>
### Syntax

```
<declare record variable> ::=
    variable_name <collectionType> 
    ;
 
<Collection Type Definition> ::=
    TYPE <Type-Name> 
    IS TABLE OF <Element-Type> 
    [ NOT NULL ] 
    INDEX BY <Index-Type>
    ;

<Element-Type> ::=
      Built-in SQL Data Type
    | User-Defined Type
    | %TYPE
    | %ROWTYPE

<Index-Type> ::=
      INTEGER
    | LONG
    | CHAR(n)
    | VARCHAR(n)
```

<a id="e40572bdc23627c7"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="c6f913b94253988a"></a>
### Syntax Rules and Parameters

- Type-name
    - It specifies the name of a collection type to be used by a user.
- Element-type
    - It specifies the type of an element to be stored in a collection variable. 
- Index-type
    - It specifies the data type of a key stored in a collection variable.

<a id="1e28943d8a3e9da7"></a>
### Description

It declares a collection type.

<a id="f55e0a89e9e31bac"></a>
### Examples

```
gSQL> DECLARE
TYPE rec IS TABLE OF VARCHAR(20) INDEX BY VARCHAR(20);
v1 rec;
v2 VARCHAR(20);
BEGIN
  DBMS_OUTPUT.PUT_LINE( 'first = ' || v1.first);
  DBMS_OUTPUT.PUT_LINE( 'last = '  || v1.last);
  DBMS_OUTPUT.PUT_LINE( 'prior = ' || v1.prior('aaa'));
  DBMS_OUTPUT.PUT_LINE( 'next = '  || v1.next('aaa'));
  DBMS_OUTPUT.PUT_LINE( 'count = ' || v1.count());

  FOR I IN 1 .. 10
  LOOP
      v1('a' || i) := 'a' || i;
  END LOOP;

  DBMS_OUTPUT.PUT_LINE( 'first = ' || v1.first);
  DBMS_OUTPUT.PUT_LINE( 'last = '  || v1.last);
  DBMS_OUTPUT.PUT_LINE( 'count = ' || v1.count());

  DBMS_OUTPUT.PUT_LINE( 'Print all from first to last');
  v2 := v1.first;
  WHILE v2 IS NOT NULL
  LOOP
      DBMS_OUTPUT.PUT_LINE('Key= ' || v2 || ',Value=' || v1(v2));
      v2 := v1.next(v2);
  END LOOP;

  DBMS_OUTPUT.PUT_LINE( 'Print all from last to first');
  v2 := v1.last;
  WHILE v2 IS NOT NULL
  LOOP
      DBMS_OUTPUT.PUT_LINE('Key= ' || v2 || ',Value=' || v1(v2));
      v2 := v1.prior(v2);
  END LOOP;

END;
/
first =
last =
prior =
next =
count = 0
first = a1
last = a9
count = 10
Print all from first to last
Key= a1,Value=a1
Key= a10,Value=a10
Key= a2,Value=a2
Key= a3,Value=a3
Key= a4,Value=a4
Key= a5,Value=a5
Key= a6,Value=a6
Key= a7,Value=a7
Key= a8,Value=a8
Key= a9,Value=a9
Print all from last to first
Key= a9,Value=a9
Key= a8,Value=a8
Key= a7,Value=a7
Key= a6,Value=a6
Key= a5,Value=a5
Key= a4,Value=a4
Key= a3,Value=a3
Key= a2,Value=a2
Key= a10,Value=a10
Key= a1,Value=a1

Anonymous PL block executed.
```

<a id="970a020656e2f64b"></a>
### Compatibility

The SQL standard does not define it.

<a id="f69ee4834d2d9366"></a>
### For More Information

Refer to [Collection Method Invocation](#a05c8c71944116f4).

<a id="02a73511f88bd73d"></a>
## CONTINUE Statement

<a id="37eb85b7327159ad"></a>
### Function

It stops currently performing statement list, and performs the next iteration of a superordinate loop statement.

<a id="c797500d4368d766"></a>
### Syntax

```
<continue statement> ::=
    CONTINUE [ label_name ] [ WHEN condition ] 
    ;
```

<a id="9a954e9d2a2b24f3"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

A statement with a target label should be one of the following loop family statements.  

• basic loop statement  
• for loop statement  
• while statement  
• forall statement

<a id="b9396e39c3368e9e"></a>
### Syntax Rules and Parameters

- Label name
    - It can have an identifier chain form.
- Condition
    - If it is specified, it returns to a loop statement only when the condition is TRUE.

<a id="ff5270753d2be0e9"></a>
### Description

It stops currently performing statement list, and returns to the superordinate loop statement.

If a label is specified, it returns to the superordinate loop statement of the label name.  
If a label is not specified, it returns to the nearest superordinate loop statement.  
If multiple superordinate loop statements with the same names exist, then the nearest statement is selected.  
It can return to a loop statement (exist in a nested scope) which is visible in the current location.

If a condition is specified, then it returns only when the condition is TRUE.  
If a condition is not specified, then it definitely returns.

<a id="a420f67bcb59576c"></a>
### Examples

```
DECLARE
  V1 INTEGER := 1;
BEGIN
  <<AAA>>
  WHILE V1 <= 10 LOOP
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
    V1 := V1 + 1;
    IF V1 <= 2 THEN
      DBMS_OUTPUT.PUT_LINE( 'CONTINUE' );
      CONTINUE;
    ELSE
      EXIT;
    END IF; 
    DBMS_OUTPUT.PUT_LINE( 'END-OF-WHILE' );
  END LOOP AAA;
END;
/
V1 = 1 
CONTINUE
V1 = 2 

Anonymous PL block executed.
```

<a id="51fd486406eb8baa"></a>
### Compatibility

&lt;continue statement&gt; statement is similar to &lt;iterate statement&gt; of the SQL standard.  
However, &lt;iterate statement&gt; statement does not provide WHEN condition feature.

<a id="13940dd9e3664c25"></a>
### For More Information

Refer to the following.

- [EXIT Statement](#d41640b5f286a508)
- [GOTO Statement](#82bb91693962eb5e)

<a id="cca7ad1d7d92e4de"></a>
## Cursor FOR LOOP Statement

<a id="ad0a792dad66e636"></a>
### Function

It performs loops as many times as the number of rows in the result created by a query or a cursor declared by a user in PSM.

<a id="77a01fef1fd18ffd"></a>
### Syntax

```
<Cursor For Loop statement> ::=
       FOR <Variable_Name> IN <Cursor>
       LOOP
            { <SQL procedure statement> ; }... 
       END LOOP [ Label_Name ]
       ;

<Cursor> ::=
       < ( Implicit_Cursor_Query ) >
     | < Explicit_Cursor_Name > [ ( [ <actual param> ] ) ]
   

<Implicit_Cursor_Query> ::=
       SELECT statement
     | SELECT_FOR_UPDATE statement
     | INSERT_RETURNING_QUERY statement
     | UPDATE_RETURNING_QUERY statement
     | DELETE_RETURNING_QUERY statement


<actual param> ::=
      ( expression [ , expression ] .. )
```

<a id="11a375c89870aa77"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body of PSM.

<a id="674c1667d20cefb6"></a>
### Syntax Rules and Parameters

The variable declared within For~Loop is valid only within that loop scope. (The variable can not be referenced from outside of that Cursor For Loop Block Scope)

<a id="60eea1c5f257c6ff"></a>
#### When Using Cursor Name

A cursor should already have been declared before performing LOOP by using a cursor name.   
For more information about an actual param, refer to [OPEN Statement](#bf1f4e379445065f).

<a id="515377d750b1221d"></a>
#### When Using Cursor Query

It can perform only the query which can be internally processed by using an implicit cursor in GOLDILOCKS such as a select and a returning query.

<a id="adfc7e15d5286116"></a>
### Description

It performs PSM statements within a loop by turning around loops as many time as the number of results created by a cursor.   
If a cursor becomes invalid (e.g. closed) during LOOP, it does not perform the loop and it processes itas an error.   
If an explicit cursor name is specified and the corresponding cursor is already opened, then it is processed as an error.

The variable to which a result of the cursor specified in FOR LOOP clause is returned is automatically created. (It is created as a row type of the result set to be returned by an execution result of a cursor.)   
However, if an alias for a select target expression which is not a column of a specific table among results of a user cursor query is not specified, then an error may occur.

<a id="687fecb27ac11d3a"></a>
### Examples

<a id="51c6f8085e8e4cfb"></a>
#### Using Explicit Cursor

```
DECLARE
CURSOR c1 IS SELECT * FROM T1;
BEGIN
  FOR rec IN C1
  LOOP
    DBMS_OUTPUT.PUT_LINE( 'RowCount=' || c1%rowcount || ',C1=' || rec.c1 || ', C2=' || rec.c2);
  END LOOP;
END;
/
RowCount=1,C1=1, C2=1
RowCount=2,C1=2, C2=2
RowCount=3,C1=3, C2=3
RowCount=4,C1=4, C2=4
RowCount=5,C1=5, C2=5
RowCount=6,C1=6, C2=6
RowCount=7,C1=7, C2=7
RowCount=8,C1=8, C2=8
RowCount=9,C1=9, C2=9
RowCount=10,C1=10, C2=10

Anonymous PL block executed.
```

<a id="8e412772e4d8da10"></a>
#### Using Cursor Query

```
BEGIN
  FOR rec IN (select * from t1)
  LOOP
      DBMS_OUTPUT.PUT_LINE( 'RowCount=' || sql%rowcount || ',C1=' || rec.c1 || ', C2=' || rec.c2);
  END LOOP;
END;
/
C1=1, C2=1
C1=2, C2=2
C1=3, C2=3
C1=4, C2=4
C1=5, C2=5
C1=6, C2=6
C1=7, C2=7
C1=8, C2=8
C1=9, C2=9
C1=10, C2=10

Anonymous PL block executed.
```

<a id="df4eb8beb8344fcd"></a>
### For More Information

Refer to the following.

- [Explicit Cursor Declaration and Definition](#465c051bfb78ee84)
- [GOTO Statement](#82bb91693962eb5e)
- [EXIT Statement](#d41640b5f286a508)

<a id="2b78435faeadac86"></a>
## Cursor Variable Declaration

<a id="0a023ebad2c9eefb"></a>
### Function

It declares a cursor variable in DECLARE section of PSM.

<a id="b01fd56bde98aa08"></a>
### Syntax

```
<cursor variable declaration> ::=
    variable_name <type>
    ;

<cursor type definition> ::=
      TYPE <type_name> IS REF CURSOR [ RETURN <return type> ]

<return type> ::= 
      <table_name | view_name | cursor_name | cursor_variable > % ROWTYPE
    | <record_variable_name> % TYPE
    | <record_type_name>
```

<a id="72d4c1fa6d40631e"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of PSM.

<a id="876d2112276ef911"></a>
### Syntax Rules and Parameters

Specifying the initial value of a cursor variable or assigning a cursor variable is allowed only between cursor variables.

<a id="2868ba35dbd89760"></a>
### Description

A cursor variable is operated like as a pointer indicating a cursor which is not dependent on a specific cursor.

<a id="4a8c949f33557057"></a>
### Examples

```
DECLARE
TYPE rec IS RECORD (V1 VARCHAR(20), V2 VARCHAR(20));
TYPE cv IS REF CURSOR RETURN rec;
BEGIN
    NULL;
END;
/

Anonymous PL block executed.
```

<a id="7983c9f729128e13"></a>
### For More Information

Refer to the following.

- [OPEN Statement](#bf1f4e379445065f)
- [FETCH Statement](#eded620a01801e55)
- [CLOSE Statement](#be3b8f9c4ae5e8b7)

<a id="a2dbb0a0acf3741e"></a>
## DELETE Statement Extension

<a id="f58c6b76994aa7c5"></a>
### Function

It can store the result in RETURNING INTO clause by using a record type variable of PSM.

<a id="ae5ae81e4b9895b6"></a>
### Syntax

```
<PSM delete statement extension: searched> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
        [ <returning into clause> ]
    ;

<delete statement: positioned> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        WHERE CURRENT OF cursor_name
    ;

<result offset clause> ::=
    OFFSET skip_count [ ROW | ROWS ]

<fetch limit clause> ::=
      <fetch first clause>
    | <limit clause>

<fetch first clause> ::=
    FETCH [ FIRST | NEXT ] [ row_count ] [ ROW ONLY | ROWS ONLY ]

<limit clause>
    LIMIT { fetch_row_count | offset_row_count, fetch_row_count | ALL }

<returning into clause> ::=
    { RETURN | RETURNING } { * | { <value expression> [ [AS] alias_name] } [, ...] } INTO variable_name [, ...]
```

<a id="7a4b9ba89ad7d219"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of PSM.

<a id="68aedd539eb28f42"></a>
### Syntax Rules and Parameters

If a variable to be returned through RETURNING INTO is a record type, then it can not be used by mixing together with a different variable type.

<a id="975f100e2a9245dd"></a>
### Description

It can store the result in RETURNING INTO clause by using a record type variable of PSM.

<a id="a8e1fdfec969e966"></a>
### Examples

```
gSQL> CREATE TABLE T1( C1 VARCHAR(20), C2 VARCHAR(20));
Table created.

gSQL> COMMIT;
Commit complete.

gSQL> INSERT INTO T1 VALUES ('AAA', 'BBB'), ('BBB', 'CCC'), ('CCC', 'DDD');
3 rows created.

gSQL> COMMIT;
Commit complete.


gSQL> DECLARE
  rec t1%ROWTYPE;
BEGIN
  DELETE FROM T1 WHERE C1 = 'AAA' RETURNING * INTO rec;
  DBMS_OUTPUT.PUT_LINE('SQL%ROWCOUNT=' || SQL%ROWCOUNT);
  DBMS_OUTPUT.PUT_LINE('rec.c1=' || rec.c1 || ', rec.c2=' || rec.c2);
END;
/
SQL%ROWCOUNT=1
rec.c1=AAA, rec.c2=BBB

Anonymous PL block executed.
```

<a id="ab3bc5c31e3ab5a6"></a>
### For More Information

Refer to [Deleting Data](../part-03-sql-manual/12-sql-languages.md#2bceb0e1068b2a56).

<a id="7f4f22737af3fbe7"></a>
## EXCEPTION_INIT Pragma

<a id="9f052384976a8ba7"></a>
### Function

It sets the error code which is to be processed by a user-defined exception.

<a id="7556f62b81e5ce84"></a>
### Syntax

```
< PRAGMA EXCEPTION_INIT > ::=
     PRAGMA EXCEPTION_INIT ( <Exception-Name>, <Internal-ErrorCode> ) 
     ;
```

<a id="2fe4c4e8fe657d16"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of PSM.

<a id="3d76d82d58d68a0c"></a>
### Syntax Rules and Parameters

A predefined exception can not be used in an exception name which is used as an argument. (A predefined exception name can not be declared.)   
An exception name which is used as an argument in the same PL block DECLARE clause should be declared in advance. (Declaration of an exception name in different BLOCK can not be referenced.)   
&lt;Internal-ErrorCode&gt; should be an internal error code existing within DB SYSTEM. (SUCCESS code can not be set.

<a id="36f9064f38973559"></a>
### Description

A user explicitly declares an exception name corresponding to an error code of DB SYSTEM.

<a id="af78f882eb90d134"></a>
### Examples

```
gSQL> DECLARE
user_exception_1 EXCEPTION;
PRAGMA EXCEPTION_INIT( user_exception_1, -17001);
BEGIN
  RAISE USER_EXCEPTION_1;
  EXCEPTION WHEN user_exception_1 THEN DBMS_OUTPUT.PUT_LINE('User Exception_1');
END;
/
User Exception_1

Anonymous PL block executed.
```

<a id="b13b84a63b4f5e7b"></a>
### Compatibility

Error codes are different each other according to a vendor, so it is not compatible each other.

<a id="4651752382bea209"></a>
### For More Information

Refer to the following.

- [Exception Declaration](#99e4ba38991da3b6)
- [Exception Handler](#d647934fd391349d)

<a id="99e4ba38991da3b6"></a>
## Exception Declaration

<a id="4ccd0a8eebeb88c5"></a>
### Function

It declares an exception name within a PL block.

<a id="6f97102c462db3fd"></a>
### Syntax

```
< Exception-Declaration Statement > ::=
     <Exception-Name>  EXCEPTION 
     ;
```

<a id="55ad9fefa9fdb15d"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of PSM.

<a id="45efd6eff4af97fd"></a>
### Syntax Rules and Parameters

It can not declare a predefined exception name.   
Duplicated declarations are not allowed in DECLARE clause of the same SCOPE.

<a id="253c8060e0c22e09"></a>
### Description

A user explicitly declares an exception.

<a id="c197d78239928acd"></a>
### Examples

```
DECLARE
user_exception_1 EXCEPTION;
user_exception_2 EXCEPTION;
user_exception_3 EXCEPTION;
BEGIN
  RAISE USER_EXCEPTION_2;
  EXCEPTION WHEN user_exception_1 THEN DBMS_OUTPUT.PUT_LINE('User Exception_1');
            WHEN user_exception_2 THEN DBMS_OUTPUT.PUT_LINE('User Exception_2');
            WHEN user_exception_3 THEN DBMS_OUTPUT.PUT_LINE('User Exception_3');
END;
/
User Exception_2

Anonymous PL block executed.
```

<a id="ccac425a7523e26c"></a>
### Compatibility

An exception declaration of the standard SQL is as follows, but GOLDILOCKS supports the syntax as above.

```
<condition declaration> ::=
DECLARE <condition name> CONDITION [ FOR <sqlstate value> ]
```

<a id="4dae9429890d2c07"></a>
### For More Information

Refer to the following.

- [Exception Declaration](#99e4ba38991da3b6)
- [EXCEPTION_INIT Pragma](#7f4f22737af3fbe7)

<a id="d647934fd391349d"></a>
## Exception Handler

<a id="84a7452ed02db74c"></a>
### Function

It performs an operation defined for an exception which is explicitly occurred by a user or an operation defined for an implicit error due to a DB SYSTEM error occurred during performing PL/ SQL.

<a id="4c85595eea4c29ad"></a>
### Syntax

```
< Exception Handler Statement > ::=
       EXCEPTION < Exception_When_List >
       ;

< Exception_When_List > ::=
       WHEN < Exception_Name_List > THEN <excutable statement list>  [ WHEN OTHERS THEN <excutable statement list> ]

< Exception_Name_List > ::= 
        <Exception_Name> [ { OR <Exception_Name> }... ]
```

<a id="0a1c4f7030ed8c05"></a>
### Invocation and Access Rules

It can be used within a PL block.

<a id="fc014b907386e0aa"></a>
### Syntax Rules and Parameters

OTHERS (predefined exception) can not be specified together with another exception name by using OR.  
Duplicated specifying of OTHERS (predefined exception) is not allowed in an exception handler, and OTHERS should be specified at the last.

<a id="b82e7aeaa3f548f0"></a>
### Description

<a id="198689cda14e351e"></a>
#### Exception Types

<a id="202f017eff74a75d"></a>
| Type | Definer | Has error | Has name | Raise implicitly | Raise explicitly |
| --- | --- | --- | --- | --- | --- |
| Predefined | System | Yes | Yes | Yes | Optionally |
| User-defined | User | If user assign | If user assign | No | Yes |

A predefined exception has an exception name and an error code which are specified in advance in GOLDILOCKS.  
Other exceptions are classified into an internally defined exception and a user-defined exception. An internally defined exception is that a user sets the internal error code name of GOLDILOCKS differently from a  predefined exception name, and a user-defined exception is that only the exception name is declared without specifying a separate error code.

<a id="3f59f1053850ff10"></a>
#### Predefined Exception

**Predefined exception type**

<a id="7dc998c29fcfc123"></a>
| Name | Description |
| --- | --- |
| CASE_NOT_FOUND | It can not satisfy all conditions of CASE WHEN, or ELSE clause is not defined. |
| DUP_VAL_ON_INDEX | INDEX duplicated error occurred. |
| INVALID_CURSOR | A cursor status is incorrect. |
| INVALID_NUMBER | It can not be converted to a number. |
| NO_DATA_FOUND | SELECT statement returns zero data. |
| ROWTYPE_MISMATCH | Field types of two RowType variables are different each other. |
| TOO_MANY_ROWS | It returns two or more rows. |
| VALUE_ERROR | It is an error such as type mismatch and invalid casting. |
| ZERO_DIVIDE | It tries dividing by 0. |
| OTHERS | It includes errors which are not defined in a predefined. |

<a id="88ba16bf147b83bd"></a>
### Examples

```
gSQL> DECLARE
V1 INTEGER := 0;
BEGIN
   DBMS_OUTPUT.PUT_LINE('Step1');
   V1 := 1 / 0;
   DBMS_OUTPUT.PUT_LINE('Step2');
   EXCEPTION WHEN OTHERS THEN DBMS_OUTPUT.PUT_LINE( 'Exception V1=' || V1);
END;
/
Step1
Exception V1=0

Anonymous PL block executed.
```

<a id="4be8619f8b3c6823"></a>
### Compatibility

It does not support the SQL standard grammar.

<a id="40864a2cef889315"></a>
### For More Information

Refer to the following.

- [EXCEPTION_INIT Pragma](#7f4f22737af3fbe7)
- [Exception Declaration](#99e4ba38991da3b6)

<a id="0d4e109b14705c96"></a>
## EXECUTE IMMEDIATE Statement

<a id="6c47f14a58d44ff2"></a>
### Function

It executes a dynamic SQL within PSM.

<a id="a541ed08d0e8699b"></a>
### Syntax

```
<EXECUTE IMMEDIATE statement> ::=
    EXECUTE IMMEDIATE <dynamic-sql> [ <binding-parameters> ]
    ;


<dynamic-sql> ::=
      single_quote_string
    | psm_variable


<binding-parameters> ::=
      <into-clause>
    | <using-clause>
    | <returning-into-clause>
    | <into-clause> <using-clause>
    | <using-clause> <returning-into-clause>



<into-clause> ::=
    INTO psm_variable [ {, psm_variable} ... ]


<using-clause> ::=
    USING [ <Bind-Type> ] <expression> [ {, [ <Bind-Type> ] <expression>} ... ]


<Bind-Type> ::=
     IN
   | OUT
   | IN OUT


<returing-into-clause> ::=
    RETURNING INTO psm_variable [ {, psm_variable} ... ]
```

<a id="a91d3ca18d1fff2c"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="869bc9fb83cc3516"></a>
### Syntax Rules and Parameters

<a id="0fbff1cfb5bf8572"></a>
#### Dynamic SQL

- single_quote_string: It is an SQL statement enclosed with a single quote ('). (double_quote_string is recognized as a variable in PSM.)
- Psm-variable: It is an SQL statement stored in a variable which is used in PSM.

The following is an example of expressing a data by using quote(s) in an SQL statement to be performed.

```
EXECUTE IMMEDIATE 'INSERT INTO t1 VALUES ( ''Tom'' ) '; -- Tom 
EXECUTE IMMEDIATE 'INSERT INTO t1 VALUES ( ''Tom''''House'') '; -- Tom'House
EXECUTE IMMEDIATE 'INSERT INTO t1 VALUES ( ''''''Tom'') ';   -- 'Tom
EXECUTE IMMEDIATE 'INSERT INTO t1 VALUES ( CHR(39) || ''TOM'' ) '; -- 'Tom
```

A marker (? or :V1) is used in a location where a user input a variable in a dynamic SQL.  
An SQL statement specified in a dynamic SQL should be valid.

<a id="10c9d5f6bfb59e27"></a>
#### INTO Clause

The result of performing a dynamic SQL exists, and it is not bound through a marker, but the result of processing an SQL statement is returned. (It is internally a form of an implicit cursor fetch.)   
The syntax is as follows.

```
EXECUTE IMMEDIATE 'SELECT ... FROM .. WHERE ...';
EXECUTE IMMEDIATE 'INSERT ... RETURNING ...';
EXECUTE IMMEDIATE 'UPDATE ... RETURNING ...';
EXECUTE IMMEDIATE 'DELETE ... RETURNING ...';
```

<a id="cb9a9710deb95c3b"></a>
#### USING Clause

It lists a variable or an expression in USING clause (IN can be omitted.) as many as the number of input variables used in a dynamic SQL.  
If the result of performing a dynamic SQL exists, then it lists variables as many as the number of result columns in USING OUT clause. (when returning the results to INTO clause)  
The result can be returned in the following syntax by using USING OUT.

```
EXECUTE IMMEDIATE 'SELECT x, y, z INTO :v1, :v2, :v3 ...';
EXECUTE IMMEDIATE 'INSERT INTO ...  RETURNING C1, C2 INTO :V1, :V2';
EXECUTE IMMEDIATE 'UPDATE T1 SET .. RETURNING C1, C2 INTO :V1, :V2';
EXECUTE IMMEDIATE 'DELETE FROM ...  RETURNING C1, C2 INTO :V1, :V2';
```

<a id="c04de15e3b63b7d8"></a>
#### RETURNING Clause

If INSERT/UPDATE/DELETE RETURNING INTO statement is used as a dynamic SQL, the result is returned by binding a variable  specified in USING clause in OUT-mode in GOLDILOCKS.  
The same result can be returned by using RETURNING-INTO clause for the compatibility with other DBMS.

<a id="f4916f139d9a1a36"></a>
#### Other Rules

- DDL/ DCL can not use any BIND clause. (INTO, USING, RETURNING clause)
- It is used as OUT in INTO clause and RETURNING INTO clause, so a separate bind type can not be specified nor it be simultaneously used together. 
- IN BIND type can use only a scalar type variable. 
- OUT BIND type can use a record type variable, but a scalar type or a record type can not be listed being mixed together.
- A result can not be returned being divided through INTO clause and USING OUT or RETURNING INTO.

<a id="11ed722ec9bac5ff"></a>
### Description

- If a dynamic SQL returns the result as a variable specified in INTO clause 
    - A query returning two or more results causes TOO_MANY_ROWS exception. 
    - If the result is zero, it causes NO_DATA_FOUND exception. 
- If a dynamic SQL returns the result as a variable specified in USING or RETURNING clause
    - If two or more variables which are not ARRAY are returned, it causes TOO_MANY_ROWS exception. 
    - If the result is zero, an error does not occur. 
- The following are results of which DDL/ DCL performs implicit cursor SQL%Attribute variables.
    - SQL%ROWCOUNT = 0 
    - SQL%ISOPEN = FALSE
    - SQL%FOUND = FALSE 
    - SQL%NOTFOUND = TRUE 
- Other dynamic SQLs store SQL%Attribute values corresponding to the processing results of that SQL statement.

<a id="44a3e4bdffef9817"></a>
### Examples

```
gSQL> DECLARE
V1 INTEGER;
V2 VARCHAR(20);
BEGIN
    V1 := 1;
    V2 := 'abcdef';
    DBMS_OUTPUT.PUT_LINE('#INSERT');
    EXECUTE IMMEDIATE 'insert into t1 values (:a1, :a2)' USING v1, v2;
    EXECUTE IMMEDIATE 'select c1, c2 from t1 where c1 = 1' INTO v1, v2;
    DBMS_OUTPUT.PUT_LINE('C1='|| v1 || ', C2=' || v2);

    V1 := 1;
    V2 := 'xyz';
    DBMS_OUTPUT.PUT_LINE('#UPDATE');
    EXECUTE IMMEDIATE 'update t1 set c2 = :a1 where c1 = :a2' USING V2, V1;

    V1 := 1;
    V2 := '';
    DBMS_OUTPUT.PUT_LINE('#SELECT');
    EXECUTE IMMEDIATE 'select c1, c2 from t1 where c1 = :a1' INTO v1, v2 USING v1;
    DBMS_OUTPUT.PUT_LINE('C1='|| v1 || ', C2=' || v2);

    V1 := 1;
    V2 := '';
    DBMS_OUTPUT.PUT_LINE('#DELETE');
    EXECUTE IMMEDIATE 'delete from t1 where c1 = :a1' USING v1;
END;
/
#INSERT
C1=1, C2=abcdef
#UPDATE
#SELECT
C1=1, C2=xyz
#DELETE

Anonymous PL block executed.
```

<a id="d41640b5f286a508"></a>
## EXIT Statement

<a id="8d0f57a0aaf08a0e"></a>
### Function

It exits a loop statement which has the given label among superordinate loop statements, then performs the next statement.

<a id="3bb79bac15eceb23"></a>
### Syntax

```
<exit statement> ::=
    EXIT [ label_name ] [ WHEN condition ]
    ;
```

<a id="28838e8bf2a34b00"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="b950660648b4089b"></a>
### Syntax Rules and Parameters

- Label name
    - It is a label name of a loop statement to be exited.
    - It can be in an identifier chain form.
- Condition
    - If a condition is specified, then it can exit a loop statement only when that condition is TRUE.

<a id="e27e931f9fadccdb"></a>
### Description

- It stops currently performing statement list and exits a superordinate loop statement.
- A statement with a target label should be one of the following loop family statements.
    - basic loop statement
    - for loop statement
    - while statement
- If a label is specified, then it exits a superordinate loop statement which has that label name.
- If a label is not specified, then it exits the nearest superordinate loop statement.
- If multiple superordinate loop statements with the same label names exist, then the nearest statement is selected.
- It can exit only a loop statement (exist in a nested scope) which is visible in the current location.

- If a condition is specified, then it exits only when the condition is TRUE.
- If a condition is not specified, then it definitely exits.

<a id="88773b45998ee478"></a>
### Examples

```
gSQL> DECLARE
  V1 INTEGER := 1;
BEGIN
  <<AAA>>
  WHILE V1 <= 10 LOOP
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
    EXIT;
    V1 := V1 + 1;
  END LOOP AAA;
END;
/
V1 = 1 

Anonymous PL block executed.
```

<a id="b29eb6c4882753a9"></a>
### Compatibility

It does not exist in the SQL standard.

<a id="b9de634435328f03"></a>
## Explicit Cursor Attribute

<a id="c270c9ef8f28b1f1"></a>
### Function

It returns the status value of a cursor defined in PSM.

<a id="b3f35df3d482bbf5"></a>
### Syntax

```
<Explicit cursor attribute> ::=
    cursor_name '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="59e592d43573c18f"></a>
### Invocation and Access Rules

It can be used only in the body section of PSM.

<a id="9179049e07e6129b"></a>
### Syntax Rules and Parameters

- Cursor_name
    - It is the name of a cursor whose status value is to be obtained.

<a id="5419fea550e93990"></a>
### Description

- It returns the status value of a given cursor.
    - ISOPEN: It is whether the current cursor is OPEN.
    - FOUND: It is whether the data is returned by the recent fetch.
    - NOTFOUND: It is an opposite of FOUND.
    - ROWCOUNT: It is the number of fetched records after the cursor is recently OPEN.
- The following values are returned according to the cursor status.

**Results according to the performing moment**

<a id="d56e93dc36ac2e7c"></a>
| Attribute name | Before OPEN | After OPEN | After FETCH | After CLOSE |
| --- | --- | --- | --- | --- |
| ISOPEN | FALSE | TRUE | TRUE | FALSE |
| FOUND | NULL | NULL | TRUE/FALSE | NULL |
| NOTFOUND | NULL | NULL | TRUE/FALSE | NULL |
| ROWCOUNT | NULL | NULL | N (the number) | NULL |

<a id="184454f51674fb25"></a>
### Examples

```
gSQL> CREATE TABLE T1 ( I1 INTEGER );

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> DECLARE
  CURSOR C1 IS SELECT * FROM T1; 
  V1 INTEGER := 0;
  V2 INTEGER := 0;
  TOTAL INTEGER := 0;
BEGIN
  FOR I IN 1..100 LOOP
    INSERT INTO T1 VALUES( I );
  END LOOP;

  COMMIT;

  IF NOT C1%ISOPEN THEN
    OPEN C1; 
  END IF; 

  LOOP
    FETCH C1 INTO V1; 
    EXIT WHEN C1%NOTFOUND;

    TOTAL := TOTAL + V1; 
    V2 := V1; 
  END LOOP;

  DBMS_OUTPUT.PUT_LINE( 'COUNT = ' || C1%ROWCOUNT || ' TOTAL = ' || TOTAL );

  CLOSE C1; 

END;
/

COUNT = 100 TOTAL = 5050

Anonymous PL block executed.
```

<a id="875b9da997d91a8a"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="465c051bfb78ee84"></a>
## Explicit Cursor Declaration and Definition

<a id="9a3e9c69cb89295d"></a>
### Function

It declares a cursor in DECLARE section of PSM.

<a id="904b5043c8ac3ec9"></a>
### Syntax

```
<cursor declaration> ::=
    CURSOR cursor_name [ <cursor param spec> ] RETURN rowtype
    ;

<cursor param spec> ::=
      ( <cursor param decl> [ , <cursor param decl> ] .. )

<cursor param decl> ::=
      param_name [ IN ] datatype [ { ':=' | DEFAULT } expression ]

<cursor definition> ::=
    CURSOR cursor_name [ <cursor param spec> ] [ RETURN rowtype ]
    IS <cursor query>
    ;

<cursor query> ::==
    select statement
    | select for update_statement
    | insert returning query statement
    | update returning query statement
    | delete returning query statement
```

<a id="e344d1bb330ce8e1"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="ab89980415024db3"></a>
### Syntax Rules and Parameters

<a id="bbc7bb894249d5cc"></a>
#### Cursor Name

It is a cursor name to be declared.   
The length of a cursor name should be shorter than 128 bytes.  
It should be a unique name in that scope.

<a id="5f0d0498feb49cdc"></a>
#### RowType

It defines a record type of a cursor.  
The number of select targets specified when defining a cursor should be same, and the data type should be compatible.  
If a rowtype is not specified, then a rowtype which is appropriate to a SELECT target of select_statement specified when defining a cursor is automatically specified.

<a id="041a9fd0af5ceea3"></a>
#### Param Name

It is a name which distinguishes parameters within a specific cursor.  
It should be a unique name in that cursor.  
If the name is the same as a name of another variable which can be referenced within a scope, then a parameter of that cursor is preferentially referenced.

<a id="45d6be0627587daa"></a>
#### DataType

It specifies the data type of the corresponding parameter.  
It can use all built-in types provided by GOLDILOCKS and types defined within PSM.  
However, a statement which restricts a scope (precision/ scale) can not be specified in a built-in type, but it is internally specified as the maximum scope of the corresponding data type.

<a id="c04e4330f5759435"></a>
#### Cursor Query

- The cursor can execute the following queries.
    - Select statement
    - Select For Update statement
    - Insert Returning statement
    - Update Returning statement
    - Delete Returning statement
- SELECT INTO statement is not available.

<a id="bac98532eebd5a02"></a>
### Description

- &lt;explicit cursor declaration&gt; statement declares or defines a cursor.
    - Cursor declaration: It declares only a name and format of a cursor.
    - Cursor definition: It detailedly defines a name, format of a cursor and SELECT statement to be performed. 
- An explicit cursor is used by defining it after declaration. or it can be used by defining it without a declaration.
- When using an explicit cursor by defining it after declaration, then the cursor name, the parameter specification and the record type definition should exactly match.
- A declaration and a definition of an explicit cursor should exist in the same block.
- An explicit cursor is created when the cursor enters the defined block, and it is automatically CLOSEd and deleted when it exits the block.
- 'MAXIMUM_NAMED_CURSOR_COUNT' property restricts the maximum number of explicit cursors which can be created in a specific time.
- The following variables can be used in &lt;cursor query&gt; statement performed by an explicit cursor.
    - Parameter of the cursor
    - All PSM variables which can be referenced in a scope at the time of declaration. (It is not a scope of the time of open.)
    - External bind parameter (in case of an anonymous PL block)
- An explicit cursor performing &lt;cursor query&gt; specified by a user has the following properties.
    - IN_SENSITIVE (Changes by another transaction do not affect it.)
    - NON_SCROLLABLE (It can not fetch the previous record again.)
    - READ_ONLY (Only a read operation is available.)
    - WITH-HOLD (A cursor is not automatically closed even though COMMIT/ ROLLBACK is performed.)

<a id="0ea02ab2fc15b637"></a>
### Examples

```
gSQL> CREATE TABLE t1( c1 INTEGER, c2 VARCHAR( 6 ) );

Table created.

gSQL> COMMIT;

Commit complete.
```

- Insert Returning Statement

```
gSQL> 
DECLARE
   var1 t1%ROWTYPE;
   CURSOR cur1( p1 INTEGER, p2 varchar(6) ) RETURN t1%ROWTYPE 
      IS INSERT INTO t1 VALUES ( p1, p2 ) RETURNING *;
BEGIN
   OPEN cur1( 1, 'aaa' );
 
   FETCH cur1 INTO var1;
   DBMS_OUTPUT.PUT_LINE( 'var1.c1 = ' || var1.c1 || ' , var1.c2 = ' || var1.c2 );

   CLOSE cur1;
END;
/

var1.c1 = 1 , var1.c2 = aaa
Anonymous PL block executed.
```

- Select Statement

```
gSQL>
DECLARE
   var1 t1%ROWTYPE;
   CURSOR cur1( p1 INTEGER, p2 varchar(6) ) RETURN t1%ROWTYPE IS 
      SELECT * FROM t1 WHERE c1 = p1 AND c2 = p2;
BEGIN
   OPEN cur1( 1, 'aaa' );

   FETCH cur1 INTO var1;
   DBMS_OUTPUT.PUT_LINE( 'var1.c1 = ' || var1.c1 || ' , var1.c2 = ' || var1.c2 );

   CLOSE cur1;
END;
/

var1.c1 = 1 , var1.c2 = aaa
Anonymous PL block executed.
```

- Update Returning Statement

```
gSQL> 
DECLARE
   var1 t1%ROWTYPE;
   CURSOR cur1( p1 INTEGER, p2 varchar(6) ) RETURN t1%ROWTYPE IS
      UPDATE t1 SET c1 = p1, c2 = p2 RETURNING *;
BEGIN
   OPEN cur1( 3, 'ccc' );
 
   FETCH cur1 INTO var1;
   DBMS_OUTPUT.PUT_LINE( 'var1.c1 = ' || var1.c1 || ' , var1.c2 = ' || var1.c2 );

   CLOSE cur1;
END;
/

var1.c1 = 3 , var1.c2 = ccc
Anonymous PL block executed.
```

- Delete Returning Statement

```
gSQL> 
DECLARE
   var1 t1%ROWTYPE;
   CURSOR cur1( p1 INTEGER, p2 varchar(6) ) RETURN t1%ROWTYPE IS
      DELETE FROM t1 WHERE c1 = p1 AND c2 = p2 RETURNING *;
BEGIN
   OPEN cur1( 3, 'ccc' );
 
   FETCH cur1 INTO var1;
   DBMS_OUTPUT.PUT_LINE( 'var1.c1 = ' || var1.c1 || ' , var1.c2 = ' || var1.c2 );

   CLOSE cur1;
END;
/

var1.c1 = 3 , var1.c2 = ccc
Anonymous PL block executed.
```

<a id="5a144b8dec28d278"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="40a7055b27276c16"></a>
### For More Information

Refer to the following.

- [OPEN FOR Statement](#326b0ac4f8704e21)
- [FETCH Statement](#eded620a01801e55)
- [CLOSE Statement](#be3b8f9c4ae5e8b7)

<a id="eded620a01801e55"></a>
## FETCH Statement

<a id="2306a7f0e1c7fb64"></a>
### Function

It fetches a single record of OPEN cursor.

<a id="a1934d7daf5a7406"></a>
### Syntax

```
<fetch statement> ::=
    FETCH cursor_name <into clause>
    ;

<into clause> ::=
    INTO { variable [ , variable ] .. | record }
```

<a id="5c9ee7171867faa6"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="18f09f80ab3f4c98"></a>
### Syntax Rules and Parameters

- Cursor name
    - It is a cursor name to be fetched.
- Variable
    - It is a scalar type variable or a bind parameter which stores a column value among the fetch results.
- Record
    - It is a record type variable to store the entire single record of which is the fetch result.

<a id="f2ecc1f0b494c039"></a>
### Description

It fetches a record from an open cursor, then copies the value to a variable specified in INTO clause.   
If a cursor is declared only but not defined, then an error occurs.  
The cursor should be open.

A variable type given to INTO clause should be compatible with a data type of the fetched record result.  
The number of variables given to INTO clause should be the same as the number of the cursor's SELECT targets.  
However, if a variable given in INTO clause is a record type, then only a single variable should be specified.  
Also, the number of the record variable fields should be the same as the number of SELECT targets.

If a fetch is called when a record to be fetched does not exist, then the value of target variables in INTO clause is not altered.

<a id="f5a187d8ad760f49"></a>
### Examples

```
gSQL> CREATE TABLE T1 ( I1 INTEGER );

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> DECLARE
  CURSOR C1 IS SELECT * FROM T1; 
  V1 INTEGER := 0;
  V2 INTEGER := 0;
  CNT INTEGER := 0;
  TOTAL INTEGER := 0;
BEGIN
  FOR I IN 1..100 LOOP
    INSERT INTO T1 VALUES( I );
  END LOOP;

  COMMIT;

  OPEN C1; 

  LOOP
    FETCH C1 INTO V1; 

    CNT := CNT + 1;
    TOTAL := TOTAL + V1; 
    V2 := V1; 
    EXIT WHEN V1 = 100; 
  END LOOP;

  CLOSE C1; 

  DBMS_OUTPUT.PUT_LINE( 'CNT = ' || CNT || ' TOTAL = ' || TOTAL );
END;
/

CNT = 100 TOTAL = 5050

Anonymous PL block executed.
```

<a id="585bac527f85af78"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="88e8b521a2254acd"></a>
### For More Information

Refer to the following.

- [OPEN Statement](#bf1f4e379445065f)
- [CLOSE Statement](#be3b8f9c4ae5e8b7)

<a id="8eb927ba8d4f181c"></a>
## FOR LOOP Statement

<a id="bf4a4d725577730b"></a>
### Function

As long as an index variable has the given value scope, it performs internal statements by increasing or reversing the index variable by 1.

<a id="904812f18279bb2c"></a>
### Syntax

```
<for loop statement> ::=
    FOR index_variable_name IN [ REVERSE ] lower_bound .. upper_bound
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="984bd4db45e075dc"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="8d8349b398d36fda"></a>
### Syntax Rules and Parameters

- Index variable name
    - It is a variable name to be used as an index in FOR statement. Internally, NATIVE_BIGINT type variable is used.
- Lower bound
    - It should be an integer type. If a number with a floating point is used, then the number below decimal point is rounded up while converting the type. 
- Upper bound
    - It should be an integer type. If a number with a floating point is used, then the number below decimal point is rounded up while converting the type.

<a id="6e3845eea27aeeaa"></a>
### Description

*for loop* statement performs an internal statement list by increasing or decreasing the index variable value.

- If REVERSE is specified
    - an index variable is decreased by 1 from upper_bound value, and it terminates execution of *for loop* statement when the index variable value becomes smaller than lower_bound.
    - If upper_bound value is smaller than lower_bound then an internal statement list is not performed.
- If REVERSE is not specified
    - an index variable is increased by 1 from lower_bound, and it terminates execution of *for loop* statement when the index variable value becomes bigger than upper_bound.
    - If lower_bound value is bigger than upper_bound, then an internal statement list is not performed.

<a id="2864e79252101023"></a>
### Examples

```
gSQL> BEGIN
  FOR I IN 0 .. 5 LOOP
    DBMS_OUTPUT.PUT_LINE( 'I = ' || I );
  END LOOP;
END;
/

I = 0
I = 1
I = 2
I = 3
I = 4
I = 5
Anonymous PL block executed.


gSQL> BEGIN
  FOR I IN REVERSE 0 .. 5 LOOP
    DBMS_OUTPUT.PUT_LINE( 'I = ' || I );
  END LOOP;
END;
/

I = 5
I = 4
I = 3
I = 2
I = 1
I = 0
Anonymous PL block executed.
```

<a id="6031cb8c2d74bb40"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="db081db5e0947cfa"></a>
### For More Information

Refer to the following.

- [CONTINUE Statement](#02a73511f88bd73d)
- [EXIT Statement](#d41640b5f286a508)
- [GOTO Statement](#82bb91693962eb5e)

<a id="515fb4aa2f801dc3"></a>
## Function Declaration and Definition

<a id="54c28f61d8d755bf"></a>
### Function

It declares and defines a function.

<a id="cbc95d2195a9c61f"></a>
### Syntax

```
<function declaration> ::= 
        FUNCTION <function name> 
        [ ( <parameter list> ) ]
        <return clause>
        [ <function characteristics list> ]
        ; 
 
<function definition> ::= 
        FUNCTION <function name> 
        [ ( <parameter list> ) ]
        <return clause>
        [ <function characteristics list> ]
        { IS | AS }
        <routine body>
        ; 
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

<function characteristics list> ::=
      <function characteristics> [ ... ]

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

<a id="1cb194810da06a7c"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="358162d8acf452d8"></a>
### Syntax Rules and Parameters

<a id="3c21f24a9e9c5dc9"></a>
#### function name

It is a name of function to be created in a PL block, and it should be a unique name in a PL block.  
In other words, PL item and function declared in PL block can not have the same name.  
The length of a function name should be shorter than 128 bytes.

<a id="d25abd5cf7c3585c"></a>
#### parameter name

It defines a parameter name of the function.  
The name of each parameter should be unique in a function.  
In other words, the function's parameter and PL item can not have the same name.  
The length of a parameter name should be shorter than 128 bytes.  
The maximum number of parameters available in a single function is limitless.

<a id="8062b9c111a2c194"></a>
#### parameter mode

It sets each parameter mode.   
The parameter modes are IN, OUT, and IN OUT.  
If the parameter mode is not specified, the default mode is *IN*.

<a id="afbad69990320e84"></a>
#### parameter default

It is the default value of the parameter.  
The parameter with the specified parameter default can be omitted when executing the function.   
If the parameter is not specified but omitted, then the default value is &lt;value expression&gt; specified when defining the parameter.  
The datatype of &lt;value expression&gt; should be the datatype of the parameter.  
All parameters defined after the parameter having &lt;parameter default&gt; should have &lt;parameter default&gt;.

<a id="ada905fe987c1b62"></a>
#### return clause

It defines the return type of the function.   
It is defined as follows in &lt;return clause&gt;.

- RETURN &lt;datatype&gt;
    - It defines the datatype of the return value returned by the function.
- RETURN TABLE ( &lt;table function column list&gt; )
    - It defines the table type of the returned result set.

<a id="0fdcab4d5c2dd853"></a>
#### table function column list

It is the column name of the result set returned by the table function.  
The length of a column name should be shorter than 128 bytes.  
The number of columns are limitless.  
Each column name is unique in &lt;table function column list&gt;.  
The column name can be the same as the parameter name and the declare item name.  
The column defined in &lt;table function column list&gt; can not be referenced in PL block of the function.

<a id="6f6aeede63d7d1bb"></a>
#### function characteristics

&lt;function characteristics&gt; specifies the characteristics of the function.  
The redundant characteristics are not allowed.  
For more information, refer to [Routine Characteristics](#a870cb9c0d6274b0).

<a id="4da5c1aa4380ece9"></a>
#### routine body

- SQL body
    - For more information, refer to [Block (BEGIN .. END)](#acfcdb439eaed2a5).
- external body
    - For more information, refer to [Call Specification](#f24bb921ad663f66).

<a id="35ce1dfa3c2e47d0"></a>
### Description

It declares and defines the function as follows.

- PL block (e.g. anonymous block, procedure and function's block, block statement's block )
    - It is one of PL block's item and it declares and defines the function.
    - The function declared and defined in a PL block is a nested function.
    - Nested function is available only within the PL block range.
- Package specification
    - It declares the public function of the package.
    - The public function of the package is available in the database.
- Package body
    - It defines the public function declared in the package specification.
    - It declares and defines the private function of the package.
    - The private function of the package is available only within the package range.

The usage of the function is the same as that of schema-level function.

<a id="ee2a6cf3759501c7"></a>
### Examples

```
gSQL> CREATE TABLE t_score( c_grade INTEGER, c_score INTEGER ); 
 
Table created. 
 
gSQL> INSERT INTO t_score VALUES ( 1 , 98 ) , ( 1 , 97 ) , ( 1 , 99 ), 
                                 ( 2 , 95 ) , ( 2 , 98 ) , ( 2 , 92 ), 
                                 ( 3 , 98 ) , ( 3 , 96 ) , ( 3 , 94 ); 
 
9 rows created. 
 
gSQL> COMMIT; 
 
Commit complete.
```

- Nested function

```
gSQL> 
DECLARE  
  v_max_score INTEGER; 
   
  FUNCTION nestedfunc RETURN INTEGER; 
   
  FUNCTION nestedfunc RETURN INTEGER AS 
    v_max INTEGER; 
  BEGIN 
    SELECT MAX( c_score )
      INTO v_max 
      FROM t_score;
     
    RETURN v_max; 
  END; 
BEGIN 
  v_max_score := nestedfunc; 
 
  DBMS_OUTPUT.PUT_LINE( 'Max Score : ' || v_max_score ); 
END; 
/ 

Max Score : 99
Anonymous PL block executed.
```

- Package function

```
gSQL>  
CREATE OR REPLACE PACKAGE pkg1 AS 
  -- Declare Package Public Function 
  FUNCTION func1( p_grade INTEGER, p_option VARCHAR ) RETURN INTEGER;
END; 
/ 
 
Package created. 

gSQL>
CREATE OR REPLACE PACKAGE BODY pkg1 AS 
  -- Declare Package Private Function 
  FUNCTION func2( p_grade INTEGER, p_option VARCHAR ) RETURN INTEGER;
 
  -- Define Package Public Function 
  FUNCTION func1( p_grade INTEGER, p_option VARCHAR ) RETURN INTEGER AS
    var INTEGER; 
  BEGIN 
    var := func2( p_grade, p_option ); 
 
    RETURN var; 
  END; 
 
  -- Define Package Private Function 
  FUNCTION func2( p_grade INTEGER, p_option VARCHAR ) RETURN INTEGER AS
    var INTEGER; 
  BEGIN 
    IF p_option = 'MIN' THEN 
      SELECT MIN(c_score) INTO var FROM t_score WHERE c_grade = p_grade; 
    ELSIF p_option = 'MAX' THEN 
      SELECT MAX(c_score) INTO var FROM t_score WHERE c_grade = p_grade; 
    ELSIF p_option = 'AVG' THEN 
      SELECT AVG(c_score) INTO var FROM t_score WHERE c_grade = p_grade; 
    ELSE 
      var := -1; 
    END IF; 
 
    RETURN var; 
  END; 
END; 
/ 
 
Package created. 
 
gSQL> SELECT pkg1.func1(  1 , 'MAX' ) FROM DUAL; 
 
PKG1.FUNC1(  1 , 'MAX' ) 
------------------------ 
                      99 
 
1 row selected.
```

<a id="80c770ebb22c1433"></a>
### Compatibility

It is the same as a schema-level function.

<a id="ed1433914018a5aa"></a>
### For More Information

Refer to [CREATE FUNCTION](31-psm-sql-references.md#8343c001bfba29fc).

<a id="82bb91693962eb5e"></a>
## GOTO Statement

<a id="4b253c297e485cc1"></a>
### Function

It tries to jump into the nearest statement which has a given label among statements accessible from the current location.

<a id="cc92fa31e10d6050"></a>
### Syntax

```
<goto statement> ::=
    GOTO label_name
    ;
```

<a id="a1be5a13d993eaa3"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="9fb05590999ec85d"></a>
### Syntax Rules and Parameters

- Label_name
    - It is a label name of a statement in which is to be jumped.
    - It can be in an identifier chain form.

<a id="44da91ea56f0cb06"></a>
### Description

It starts performing by jumping into a statement which has the corresponding label name.  
If multiple candidate statements exist, then it jumps into the nearest statement.  
It can jump only to a statement (exist in a nested scope) which is visible in the current location.  
Both forward jump and backward jump are possible.

<a id="78035d9eaf9bbd75"></a>
### Examples

```
gSQL> DECLARE
  V1 INTEGER := 0;
BEGIN
  <<LABEL1>>
  IF V1 > 0 THEN
    GOTO LABEL2;
  END IF; 
  V1 := V1 + 1;
  DBMS_OUTPUT.PUT_LINE('a');
  GOTO LABEL1;
  DBMS_OUTPUT.PUT_LINE('b');
  <<LABEL2>>
  DBMS_OUTPUT.PUT_LINE('c');
END;
/
a
c

Anonymous PL block executed.
```

<a id="17e9a1737395ea00"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="8ebe8d27046f2ce2"></a>
### For More Information

Refer to the following.

- [EXIT Statement](#d41640b5f286a508)
- [CONTINUE Statement](#02a73511f88bd73d)

<a id="8d14b69600360332"></a>
## IF Statement

<a id="6f5afd033dbfe856"></a>
### Function

It performs a statement list corresponding to the condition returning TRUE among the given conditions.

<a id="561ae8ef2b7bbc52"></a>
### Syntax

```
<if statement> ::=
    IF <search condition> <if statement then clause>
    [ <if statement elsif clase> ]
    [ <if statement else clase> ]
    END IF
    ;

<if statement then clause> ::=
    THEN <executable statement list>

<if statement elsif clause> ::=
    ELSIF <search condition> THEN <executable statement list>

<if statement elsif clause> ::=
    ELSE <executable statement list>
```

<a id="90e690ca27f69ea7"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="68f7921dadaf66d5"></a>
### Syntax Rules and Parameters

- Search condition
    - It is an expression which can be finally evaluated as a boolean type.
- Executable statement list
    - It is a list of all statements supported by GOLDILOCKS PSM.

<a id="a544ae8053bfc1f3"></a>
### Description

Like as CASE statement, it performs statement lists of IF, ELSIF clauses returning TRUE by evaluating conditions.  
If it can not satisfy any condition and &lt;if statement else clause&gt; exists, then it performs the corresponding statement.   
ELSIF clauses evaluates conditional expressions in order, and stops evaluating after finding the TRUE conditional clause.

<a id="5367df75d43a65d7"></a>
### Examples

```
gSQL> DECLARE
  V1 INTEGER := 10;
BEGIN
  IF V1 > 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'POSITIVE' );
  ELSIF V1 = 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'ZERO' );
  ELSE
    DBMS_OUTPUT.PUT_LINE( 'NEGATIVE' );
  END IF;
END;
/
POSITIVE

Anonymous PL block executed.
```

<a id="f0403deecc80294b"></a>
### Compatibility

&lt;if statement&gt; statement is the same as a syntax and an operation of the SQL standard.

**SQL standard compatibility**

<a id="537937cab370a0ea"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="5efebbcaf29ca1ad"></a>
## Implicit Cursor Attribute

<a id="c6bf697f2de020c9"></a>
### Function

It returns the status value of an implicit cursor defined in PSM.

<a id="35299aad3dc09cc7"></a>
### Syntax

```
<Implicit cursor attribute> ::=
    SQL '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="af73fcc8dbe25713"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="f1a1dd348c717bfb"></a>
### Description

- It stores the result of SQL statement which was executed just before. 
    - ISOPEN: It is whether the cursor is OPEN, and it is always set to FALSE.
    - FOUND: It is whether the data is returned by the SQL result of just before. 
    - NOTFOUND: It is an opposite of FOUND.
    - ROWCOUNT: It is the number of records affected by the SQL result of just before.

<a id="e4169705cb1a1454"></a>
### Examples

```
DECLARE
V1 INTEGER;
BEGIN
    SELECT COUNT(*) INTO V1 FROM T1;
    DBMS_OUTPUT.PUT_LINE('COUNT RET    = ' || V1);
    DBMS_OUTPUT.PUT_LINE('SQL%ISOPEN   = ' || SQL%ISOPEN);
    DBMS_OUTPUT.PUT_LINE('SQL%FOUND    = ' || SQL%FOUND);
    DBMS_OUTPUT.PUT_LINE('SQL%NOTFOUND = ' || SQL%NOTFOUND);
    DBMS_OUTPUT.PUT_LINE('SQL%ROWCOUNT = ' || SQL%ROWCOUNT);
END;
/
COUNT RET    = 0
SQL%ISOPEN   = FALSE
SQL%FOUND    = TRUE
SQL%NOTFOUND = FALSE
SQL%ROWCOUNT = 1

Anonymous PL block executed.
```

<a id="adfc3013c674a73b"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="8ba7356240cd29cd"></a>
## INSERT Statement Extension

<a id="a8efdb551fcf12a4"></a>
### Function

It is an extended feature of an insert statement to input data by specifying record type variable supported in PSM in VALUES clause.

<a id="d29a1d61bb31947d"></a>
### Syntax

```
<PSM Insert Statement Extension Statement> ::=
    INSERT INTO table_name [ ( column_name [, ...] ) ]
           <Insert_source>
           [ <Returning_into_clause> ]
    ;

<Insert_source> ::=
      <value-list>
    | <from_subquery>
    | <from_default>


<from subquery> ::=
    <query_expression>


<from default> ::=
    DEFAULT VALUES


<Value-List> ::=
      VALUES <Value_item> [ , ...]


<value-Item> ::=
     PSM-Record-Type-Variable
     |  ( { <value expression> | DEFAULT } [, ...] ) 


<Returning_into_clause> ::=
      [ RETURN | RETURNING ] { * | { <value_expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]
```

<a id="be203ed08f6f86c0"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.  
A PSM insert extension statement can not be used in an original SQL statement of EXECUTE IMMEDIATE.

<a id="678278c44e3d9a21"></a>
### Syntax Rules and Parameters

It is operated the same as the basic syntax of an insert statement. However, a feature specifying PSM record type variables are added other than a feature consecutively listing existing value expressions in parentheses in value item.

A PSM record type variable should be specified when using a variable without parentheses in Value_Item.   
When using it in an insert extension statement form, a variable which is not a record type can not be used being mixed.

<a id="0bed086226ac652d"></a>
### Description

It stores a record by using a record type variable of PSM other than a general insert statement, or obtains a result through returning into.   
For more information about insert, refer to the following example.

<a id="70ee64e305b3b5de"></a>
### Examples

```
gSQL> DECLARE
  rec t1%ROWTYPE;
BEGIN
    rec.i1 := 'AAA';
    rec.i2 := 'BBB';
    rec.i3 := 'CCC';

    INSERT INTO t1 (i1, i2, i3) VALUES rec ;
END;
/

Anonymous PL block executed.


gSQL> SELECT * FROM t1;

I1  I2  I3 
--- --- ---
AAA BBB CCC
```

<a id="17f7ed02530f8522"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="a6c8cd4e6ef22c56"></a>
## INSERT INTO ... UPDATE Statement Extension

<a id="8a75e8658bf66b34"></a>
### Function

It is the extended function of *insert into .. update* statement. It creates a new row in a table by specifying the record type variable supported by PSM in a values clause, or updates the row by specifying the variable in a set clause.

<a id="d438a31916f6b0fc"></a>
### Syntax

```
<PSM Upsert Statement Extention Statement > ::=    
    INSERT INTO table_name [ ( column_name [, ...] ) ]
        <insert source>
        <duplicate key clause>
        [ <Returning_into_clause> ]
    ;

<insert source> ::=
      <values-list>
    | <from subquery>
    | <from_default>

<Value-List> ::=
      VALUES <Value_item> [ , ...]

<value-Item> ::=
         PSM-Record-Type-Variable
     |  ( { <value expression> | DEFAULT } [, ...] ) 

<from subquery> ::=
    <query expression>

<from default> ::=
    DEFAULT VALUES

<duplicate key clause>
    ON DUPLICATE KEY { DO NOTHING | <do update clause> }

<do update clause> ::=
    [DO] UPDATE <target-list>

<target-List> ::=
        SET <set clause> [, ...]
      | SET ROW = <psm_variable>

<set clause> ::=
      column_name = { <value expression> | DEFAULT }
    | ( column_name [, ...] ) = ( { <value expression> | DEFAULT } [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )

<returning_into_clause> ::=
      [ RETURN | RETURNING ] { * | { <value_expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]
```

<a id="d59d4ec1f145a3c5"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. procedure, function, package)  
It can be used only in the body section of a PL block.

<a id="e22417b97a1589d0"></a>
### Syntax Rules and Parameters

- &lt;values clause&gt;
    - The function specifying PSM record type variable other than consecutively listing existing value expressions in parentheses in the value item has been added. 
    - PSM record type variable should be specified when using the variable without parentheses in the value item.
    - When describing by extending the value item, then the variable other than the record type variable is not allowed.
- &lt;target list&gt; 
    - &lt;PSM_Variable&gt; used in SET ROW statement should be the variable declared as the record type.
- &lt;returning into clause&gt;
    - &lt;Variable&gt; used in RETURNING INTO statement does not need to be a record type. However, if it is specified as a record type, then it can not be used together with other data type variables nor can list two or more record type variables.

<a id="e23a659870fe558d"></a>
### Description

Returning into statement in an upsert statement stores the inserted result when insert is executed, and it stores the updated result when update is executed.

<a id="38fa67d88cb63e95"></a>
### Examples

- Execute insert.

```
gSQL> CREATE TABLE t1( c1 INTEGER UNIQUE, c2 INTEGER, c3 INTEGER );

Table created.

gSQL> DECLARE
  v_rec t1%ROWTYPE;
BEGIN
  v_rec.c1 := 1;
  v_rec.c2 := 1;
  v_rec.c3 := 1;
  
  INSERT INTO t1 VALUES v_rec ON DUPLICATE KEY UPDATE SET c1 = c1 + 1;  
END;
/

Anonymous PL block executed.

gSQL> SELECT * FROM t1; 

C1 C2 C3
-- -- --
 1  1  1

1 row selected.
```

- Execute update.

```
gSQL> CREATE TABLE t1( c1 INTEGER UNIQUE, c2 INTEGER, c3 INTEGER );

Table created.

gSQL> INSERT INTO t1 VALUES ( 1 , 1 , 1 );

1 row created.

gSQL> DECLARE
  v_rec t1%ROWTYPE;
BEGIN
  v_rec.c1 := 2;
  v_rec.c2 := 2;
  v_rec.c3 := 2;

  INSERT INTO t1 VALUES (1, 1, 1) ON DUPLICATE KEY UPDATE SET ROW = v_rec;
END;
/

gSQL> SELECT * FROM t1;

C1 C2 C3
-- -- --
 2  2  2

1 row selected.
```

- Returning statement of when executing insert

```
gSQL> CREATE TABLE t1( c1 INTEGER UNIQUE, c2 INTEGER, c3 INTEGER );

Table created.

gSQL> DECLARE
  v_rec1 t1%ROWTYPE;
  v_rec2 t1%ROWTYPE;
BEGIN
  v_rec1.c1 := 1;
  v_rec1.c2 := 1;
  v_rec1.c3 := 1;

  INSERT INTO t1 VALUES v_rec1 ON DUPLICATE KEY UPDATE SET c1 = c1 + 1 RETURNING * INTO v_rec2;
  DBMS_OUTPUT.PUT_LINE( 'v_rec2.c1 : ' || v_rec2.c1 );
  DBMS_OUTPUT.PUT_LINE( 'v_rec2.c2 : ' || v_rec2.c2 );
  DBMS_OUTPUT.PUT_LINE( 'v_rec2.c3 : ' || v_rec2.c3 );
END;
/

v_rec2.c1 : 1
v_rec2.c2 : 1
v_rec2.c3 : 1
Anonymous PL block executed.

gSQL> SELECT * FROM t1; 

C1 C2 C3
-- -- --
 1  1  1

1 row selected.
```

- Returning statement of when executing update

```
gSQL> CREATE TABLE t1( c1 INTEGER UNIQUE, c2 INTEGER, c3 INTEGER );

Table created.

gSQL> INSERT INTO t1 VALUES ( 1 , 1 , 1 );

1 row created.

gSQL> DECLARE
  v_rec1 t1%ROWTYPE;
  v_rec2 t1%ROWTYPE;
BEGIN
  v_rec1.c1 := 2;
  v_rec1.c2 := 2;
  v_rec1.c3 := 2;

  INSERT INTO t1 VALUES (1, 1, 1) ON DUPLICATE KEY UPDATE SET ROW = v_rec1 RETURNING * INTO v_rec2;
  DBMS_OUTPUT.PUT_LINE( 'v_rec2.c1 : ' || v_rec2.c1 );
  DBMS_OUTPUT.PUT_LINE( 'v_rec2.c2 : ' || v_rec2.c2 );
  DBMS_OUTPUT.PUT_LINE( 'v_rec2.c3 : ' || v_rec2.c3 );
END;
/

v_rec2.c1 : 2
v_rec2.c2 : 2
v_rec2.c3 : 2
Anonymous PL block executed.

gSQL> SELECT * FROM t1;

C1 C2 C3
-- -- --
 2  2  2

1 row selected.
```

<a id="88aa72b4eb165422"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="ce2b52a3e196e8cd"></a>
## Merge Statement Extension

<a id="e1a78d4b255e390d"></a>
### Function

It is the extended merge statement, and it inserts, updates or deletes the table record according to the condition by using the variables supported by PSM.

<a id="e1e6b72dda937f55"></a>
### Syntax

```
<merge statement> ::=
    MERGE [ <hint clause> ] INTO <target table name> [ [ AS ] <target alias> ]
    USING <source relation>
    ON <merge join condition>
    <merge operation specification>
    ;

<target table> ::=
    <table name>

<target alias> ::=
    <correlation name>
    
<source relation> ::=
    {
        <table name> [ [ AS ] <source alias> ]
      | <table subquery> [ [ AS ] <source alias> ]    
    }

<source alias> ::=
    <correlation name>

<merge join condition> ::=
    <search condition>

<merge operation specification> ::=
    <merge when clause> [...]

<merge when clause> ::=
      <merge when matched clause>
    | <merge when not matched clause>

<merge when matched clause> ::=
    WHEN MATCHED [ AND <search condition> ] 
    THEN { <merge update> | <merge delete> | <merge do nothing> }

<merge when not matched clause> ::=
    WHEN NOT MATCHED [ AND <search condition> ] 
    THEN { <merge insert> | <merge do nothing> }

<merge update> ::=
    UPDATE <target list>

<target list> ::=
      SET <set clause> [, ...]
    | SET ROW = <PSM record type variable>

<set clause> ::=
      <column name> = { <value expression> | DEFAULT }
    | ( <column name> [, ...] ) = ( { <value expression> | DEFAULT } [, ...] )

<merge delete> ::=
    DELETE

<merge insert> ::=
    INSERT [ (  column name [, ...] ) ] <insert source>

<insert source> ::=
      VALUES <value item> 
    | DEFAULT VALUES

<value item> ::=
      <PSM record type variable>
    | ( { <value expression> | DEFAULT } [, ...] )

<merge do nothing> ::=
    DO NOTHING
```

<a id="940ebb4e3a638dbb"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="7aa9504c62bd9bf8"></a>
### Syntax Rules and Parameters

Generally, it is the same as the syntax rules of the merge statement, but the following are added.

- &lt;merge update&gt;
    - It can be updated in UPDATE SET ROW statement row by row by using PSM record type variable.
- &lt;merge insert&gt;
    - If the variable is used without parentheses in INSERT VALUES, insert the data by describing PSM record type variable.

<a id="329819959645a97a"></a>
### Description

It is the extended merge statement to use the record type variable supported by PSM.  
For more information, refer to [Merge Statement](../part-03-sql-manual/20-sql-references-h-z.md#2ce51d1a09e94307).

<a id="8bd182479c49716d"></a>
### Examples

- The example of the merge statement using the record type variable supported by PSM

```
gSQL> CREATE TABLE t1 ( c1 INTEGER , c2 INTEGER , c3 INTEGER );

Table created.

gSQL> INSERT INTO t1 VALUES( 1 , 1 , 1 ) , ( 3 , 3 , 3 ) , ( 5 , 5 , 5 );

3 rows created.

gSQL> COMMIT;

Commit complete.

gSQL> CREATE TABLE t2( c1 INTEGER , c2 INTEGER , c3 INTEGER );

Table created.

gSQL> INSERT INTO t2 VALUES( 1 , 1 , 1 ) , ( 2 , 2 , 2 ) , ( 3 , 3 , 3 ) , ( 4 , 4 , 4 ) , ( 5 , 5 , 5 );

5 rows created.

gSQL> COMMIT;

Commit complete.

gSQL> 
DECLARE
  TYPE rec IS RECORD( f1 INTEGER , f2 INTEGER , f3 INTEGER );
  v_rec rec;
BEGIN
  v_rec.f1 := 10;
  v_rec.f2 := 20;
  v_rec.f3 := 30;  
  
  MERGE INTO t1   
  USING t2
  ON t1.c1 = t2.c1
  WHEN MATCHED AND t1.c1 = 1 THEN UPDATE SET ROW = v_rec
  WHEN MATCHED AND t1.c1 = 3 THEN DELETE
  WHEN MATCHED AND t1.c1 = 5 THEN DO NOTHING
  WHEN NOT MATCHED AND t2.c1 = 2 THEN INSERT VALUES v_rec
  WHEN NOT MATCHED AND t2.c1 = 4 THEN DO NOTHING;
END;
/

Anonymous PL block executed.

gSQL> SELECT * FROM t1;

C1 C2 C3
-- -- --
10 20 30
 5  5  5
10 20 30

3 rows selected.
```

<a id="fa5e1a4495997749"></a>
### Compatibility

The SQL standard does not define it.

<a id="96d51677cf5459a5"></a>
## NULL Statement

<a id="9d62ca4022eecc67"></a>
### Function

It is a statement without any feature.

<a id="b4215f5ffbae758f"></a>
### Syntax

```
<null statement> ::=
    NULL
    ;
```

<a id="0e6645b3c97bb3f9"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="e8d88c09fbe84f15"></a>
### Description

It is a statement without any feature, and used to set a label of a specific location.

<a id="630747a8e1c22cc4"></a>
### Examples

```
gSQL> BEGIN
  FOR i in 1..10 LOOP
    DBMS_OUTPUT.PUT_LINE( i );
    IF i > 5 THEN
      GOTO label1;
    END IF;
  END LOOP;
  <<label1>>
  NULL;
END;
/
1
2
3
4
5
6

Anonymous PL block executed.
```

<a id="ad3409508a5628fa"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="bf1f4e379445065f"></a>
## OPEN Statement

<a id="bad8bc9c56683d98"></a>
### Function

It executes SELECT statement of a cursor defined in PSM.

<a id="1ecd41196349c368"></a>
### Syntax

```
<open statement> ::=
    OPEN cursor_name [ <actual param spec> ]
    ;

<actual param spec> ::=
      ( expression [ , expression ] .. )
```

<a id="376c89de7f37b41f"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="351c528c50e08c86"></a>
### Syntax Rules and Parameters

- Cursor_name
    - It is the name of a cursor to be opened.

<a id="6b722304b8526ac1"></a>
### Description

It executes SELECT or SELECT ... FOR UPDATE statement of a defined cursor.  
If a cursor is declared only but is not defined, then an error occurs.  
Values of actual parameters should be compatible with the data type of those parameters.

The number of actual parameters should be same as the number of parameters of a cursor.  
If it is smaller than the number of parameters of a cursor, then the default value should be specified in all other parameters.

<a id="f20da74fdf38e8c0"></a>
### Examples

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I2 VARCHAR(10) );

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> INSERT INTO T1 VALUES( 1, 'AAA' );

1 row created.

gSQL> INSERT INTO T1 VALUES( 2, 'BBB' );

1 row created.

gSQL> INSERT INTO T1 VALUES( 3, 'CCC' );

1 row created.

gSQL> COMMIT;

Commit complete.

gSQL> DECLARE
  CURSOR C1( A1 INTEGER := 1, A2 VARCHAR DEFAULT 'AAA') IS SELECT * FROM T1 WHERE I1 = A1 AND I2 = A2;
  V1 INTEGER;
  V2 VARCHAR(10);
BEGIN
  OPEN C1( 1 );
  FETCH C1 INTO V1, V2;
  DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 || ' V2 = ' || V2 );

  CLOSE C1;
END;
/

V1 = 1 V2 = AAA

Anonymous PL block executed.
```

<a id="ff49af2d8502c7cc"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="6a6e2eba811d029c"></a>
### For More Information

Refer to the following.

- [CLOSE Statement](#be3b8f9c4ae5e8b7)
- [FETCH Statement](#eded620a01801e55)

<a id="326b0ac4f8704e21"></a>
## OPEN FOR Statement

<a id="53fd9aa49a1f1d0e"></a>
### Function

It opens a single cursor by executing SELECT statement through a cursor variable defined in PSM.

<a id="0aee723cca87a09b"></a>
### Syntax

```
<open statement> ::=
    OPEN cursor_variable_name FOR <cursor_query>
    ;

<cursor_query> ::==
      <static_cursor_query>
    | <dynamic_cursor_query> [ <using_clause> ]

<static_cursor_query> ::==
      select_statement
    | select_for_update_statement
    | insert_returning_query_statement
    | update_returning_query_statement
    | delete_returning_query_statement

<dynamic_cursor_query>
      single_quote_string
    | psm_variable

<using_clause> ::=
    USING [ <bind_type> ] <expression> [ {, [ <bind_type> ] <expression>} ... ]

<bind_type> ::=
     IN
   | OUT
   | IN OUT
```

<a id="79597c08644135f8"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="3932175e3c39a851"></a>
### Syntax Rules and Parameters

- &lt;cursor_variable_name&gt;
    - It is the name of cursor variable.
- &lt;cursor_query&gt;
    - A cursor query can use both a static cursor query and a dynamic cursor query.
    - The following are cursor queries.
        - select statement
        - select for update statement
        - insert returning statement
        - update returning statement
        - delete returning statement
    - A dynamic cursor query is used by enclosing sql with a single quoted (') or by storing sql in a psm variable.
    - A using clause is available when writing a dynamic cursor query.
- &lt;using_clause&gt;
    - If a bind variable exists when writing a dynamic cursor query, list variables or expressions in using clause as many as the number of bind variables.
    - The variable in using clause can describe the bind type of IN/ OUT/ IN OUT. The bind type of when writing the dynamic cursor query should be same as the bind type of the bind variable.
    - The bind type of the variable in using clause can be omitted. If omitted, the default bind type is IN.

<a id="230f7e616176dd54"></a>
### Description

It executes the cursor query of the defined cursor variable.   
If the cursor variable is previously open, then that cursor is executed after it is automatically closed and reopened.

<a id="d0704a42de83bbe6"></a>
### Examples

```
gSQL> CREATE TABLE t1( c1 INTEGER, c2 VARCHAR( 6 ) );

Table created.

gSQL> COMMIT;

Commit complete.
```

- Insert Returning Statement

```
gSQL> 
DECLARE
   var1 t1%ROWTYPE;
   curvar1 SYS_REFCURSOR;
BEGIN
   OPEN curvar1 FOR INSERT INTO t1 VALUES ( 1 , 'aaa' ) RETURNING *;

   FETCH curvar1 INTO var1;
   DBMS_OUTPUT.PUT_LINE( 'var1.c1 = ' || var1.c1 || ' , var1.c2 = ' || var1.c2 );

   CLOSE curvar1;
END;
/

var1.c1 = 1 , var1.c2 = aaa
Anonymous PL block executed.
```

- Select Statement

```
gSQL> 
DECLARE
   var1 t1%ROWTYPE;
   curvar1 SYS_REFCURSOR;
BEGIN
   OPEN curvar1 FOR SELECT * FROM t1;
 
   FETCH curvar1 INTO var1;
   DBMS_OUTPUT.PUT_LINE( 'var1.c1 = ' || var1.c1 || ' , var1.c2 = ' || var1.c2 );

   CLOSE curvar1;
END;
/

var1.c1 = 1 , var1.c2 = aaa
Anonymous PL block executed.
```

- Update Returning Statement

```
gSQL> 
DECLARE
   var1 t1%ROWTYPE;
   curvar1 SYS_REFCURSOR;
BEGIN
   OPEN curvar1 FOR UPDATE t1 SET c1 = 3, c2 = 'ccc' RETURNING *;
 
   FETCH curvar1 INTO var1;
   DBMS_OUTPUT.PUT_LINE( 'var1.c1 = ' || var1.c1 || ' , var1.c2 = ' || var1.c2 );

   CLOSE curvar1;
END;
/

var1.c1 = 3 , var1.c2 = ccc
Anonymous PL block executed.
```

- Delete Returning Statement

```
gSQL> 
DECLARE
   var1 t1%ROWTYPE;
   curvar1 SYS_REFCURSOR;
BEGIN
   OPEN curvar1 FOR DELETE FROM t1 RETURNING *; 

   FETCH curvar1 INTO var1;
   DBMS_OUTPUT.PUT_LINE( 'var1.c1 = ' || var1.c1 || ' , var1.c2 = ' || var1.c2 );

   CLOSE curvar1;
END;
/

var1.c1 = 3 , var1.c2 = ccc
Anonymous PL block executed.
```

- Dynamic Cursor Query and Using Clause

```
gSQL> INSERT INTO t1 VALUES( 100 , 'BBB' );
gSQL> COMMIT;

gSQL> 
DECLARE
  v_int_in     INTEGER;
  v_varchar_in VARCHAR(6);
  v_out        t1%ROWTYPE;
  v_sql        VARCHAR(1024);
  cv           SYS_REFCURSOR;
BEGIN
  v_sql := 'SELECT * FROM t1 WHERE c1 = ? AND c2 = ?';

  v_int_in := 100;
  v_varchar_in := 'BBB';
  
  OPEN cv FOR v_sql USING IN v_int_in, v_varchar_in;
  
  FETCH cv INTO v_out;
  DBMS_OUTPUT.PUT_LINE( 'c1 : ' || v_out.c1 || ' , v_out.c2 : ' || v_out.c2 );
  
  CLOSE cv;
END;
/

c1 : 100 , v_out.c2 : BBB
Anonymous PL block executed.
```

<a id="91f72e84071deb09"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="c93264a3b766e237"></a>
### For More Information

Refer to the following.

- [Cursor Variable Declaration](#2b78435faeadac86)
- [FETCH Statement](#eded620a01801e55)
- [CLOSE Statement](#be3b8f9c4ae5e8b7)

<a id="32725e0b99b728ac"></a>
## Procedure Call

<a id="d250983d1f50f3cb"></a>
### Function

It calls a user-defined procedure, a built-in procedure or a nested procedure.

<a id="62901fb32c037f7f"></a>
### Syntax

```
<Procedure call> ::=
    proc_name [ ( expr { , expr } ... ) ]
    ;
```

<a id="9d7fa5cdb0305b01"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

- The following privileges for the corresponding procedure are required to call the user-defined procedure. 
    - EXECUTE PROCEDURE
    - (EXECUTE PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
    - EXECUTE ANY PROCEDURE ON DATABASE

<a id="a2585f6b7cce98e3"></a>
### Syntax Rules and Parameters

- Proc_name
    - It is a name of a procedure to be executed, and it is used in the following format.

<a id="5ea24e93a0752d9e"></a>
<table class="table column_count_3"><caption></caption><thead><tr><th class="to_center"><div>Format</div></th><th class="to_center"><div>Syntax</div></th><th class="to_center"><div>Description</div></th></tr></thead><tbody><tr><td class="to_left to_middle"><div>Single identifier</div></td><td class="to_middle"><div>procedure_name</div></td><td><div>It calls the procedure of the given name.

It is searched in the following order.
1. nested procedure
2. schema-level procedure</div></td></tr><tr><td class="to_left to_middle" rowspan="3"><div>identifier chain</div></td><td><div>label_name.procedure_name</div></td><td><div>It calls a nested procedure.</div></td></tr><tr><td><div>schema_name.procedure_name</div></td><td><div>It calls a schema-level procedure.</div></td></tr><tr><td><div>package_name.procedure_name</div></td><td><div>It calls a built-in procedure.</div></td></tr></tbody></table>

If the given the number and type of arguments which were given in the procedure found first are wrong when searching with the given name (proc_name), then it does not search for another procedure but causes an error.

<a id="0786bff0351775f2"></a>
### Description

It calls a user-defined procedure, a built-in procedure or a nested procedure which was defined an advance.  
The argument value in which the default value is defined can be omitted when calling.

When using a procedure variable or bind parameter (?, :V1) in an argument which were defines as OUT or IN-OUT, then the returned value is obtained.

<a id="e09d1be9827bce46"></a>
### Examples

```
gSQL> DECLARE
  PROCEDURE PROC1( A1 INTEGER )
    IS  
    BEGIN
      PUT_LINE( 'A1 = ' || A1 );
    END;
BEGIN
  PROC1( 100 );
END;
/
A1 = 100

Anonymous PL block executed.
```

<a id="d457211850cee229"></a>
### Compatibility

The SQL standard requires to use &lt;call statement&gt;.

<a id="6cbc67f75778afa6"></a>
## Procedure Declaration and Definition

<a id="6ebd6a8f38becd14"></a>
### Function

It declares and defines a procedure.

<a id="165fb7a248790835"></a>
### Syntax

```
<procedure declaration> ::=
      PROCEDURE <procedure name>
      [ ( <parameter list> ) ]
      [ <procedure characteristics list> ]
      ;
 
<procedure definition> ::= 
      PROCEDURE <procedure name>
      [ ( <parameter list> ) ]
      [ <procedure characteristics list> ]
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

<procedure characteristics list> ::=
      <procedure characteristics> [ ... ]

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

<a id="0f79c45ed36c85db"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the declaration section of a PL block.

<a id="d8fc8c9d1ba2daac"></a>
### Syntax Rules and Parameters

<a id="95044d28c35b61d3"></a>
#### procedure name

It is a name of procedure to be created in a PL block, and it should be a unique name in a PL block.   
In other words, PL item and procedure declared in PL block can not have the same name.   
The length of a procedure name should be shorter than 128 bytes.

<a id="d1105b209996b433"></a>
#### parameter name

It defines a parameter name of the procedure.  
The name of each parameter should be unique in a procedure.  
In other words, the procedure's parameter and PL item can not have the same name.  
The length of a parameter name should be shorter than 128 bytes.  
The maximum number of parameters available in a single procedure is limitless.

<a id="effe90e6c8121dfc"></a>
#### parameter mode

It sets each parameter mode.   
The parameter modes are IN, OUT, and IN OUT.  
If the parameter mode is not specified, the default mode is *IN*.

<a id="60d00868360031a0"></a>
#### parameter default

It is the default value of the parameter.  
The parameter with the specified parameter default can be omitted when executing the procedure.   
If the parameter is not specified but omitted, then the default value is &lt;value expression&gt; specified when defining the parameter.  
The datatype of &lt;value expression&gt; should be the datatype of the parameter.  
All parameters defined after the parameter having &lt;parameter default&gt; should have &lt;parameter default&gt;.

<a id="889ed89b6e2ed059"></a>
#### procedure characteristics

&lt;procedure characteristics&gt; specifies the characteristics of the procedure.  
The redundant characteristics are not allowed.  
For more information, refer to [Routine Characteristics](#a870cb9c0d6274b0).

<a id="d472fc619d6531d8"></a>
#### routine body

- &lt;SQL body&gt;
    - For more information, refer to [Block (BEGIN .. END)](#acfcdb439eaed2a5).
- &lt;external body&gt;
    - For more information, refer to [Call Specification](#f24bb921ad663f66).

<a id="eb52d80615f94236"></a>
### Description

It declares and defines the procedure as follows.

- PL block (e.g. anonymous block, procedure and function's block, block statement's block )
    - It is one of PL block's item and it declares and defines the procedure.
    - The function declared and defined in a PL block is a nested procedure.
    - Nested procedure is available only within the PL block range.
- Package specification
    - It declares the public procedure of the package.
    - The public procedure of the package is available in the database.
- Package body
    - It defines the public procedure declared in the package specification.
    - It declares and defines the private procedure of the package.
    - The private procedure of the package is available only within the package range.

The usage of the procedure is the same as that of schema-level procedure.

<a id="819dd158642e7b21"></a>
### Examples

- Nested procedure

```
gSQL> 
DECLARE
  PROCEDURE proc1( p1 INTEGER ) IS
  BEGIN
    DBMS_OUTPUT.PUT_LINE( 'p1 = ' || p1 );
  END;
BEGIN
  proc1( 100 );
END;
/

p1 = 100
Anonymous PL block executed.
```

- Package procedure

```
gSQL>  
CREATE OR REPLACE PACKAGE pkg1 AS 
  -- Declare Package Public Function 
  PROCEDURE proc1( p1 INTEGER );
END; 
/ 
 
Package created. 

gSQL>
CREATE OR REPLACE PACKAGE BODY pkg1 AS 
  -- Declare Package Private Function 
  PROCEDURE proc2( p1 INTEGER );
 
  -- Define Package Public Function 
  PROCEDURE proc1( p1 INTEGER ) AS
  BEGIN 
    DBMS_OUTPUT.PUT_LINE( 'p1 of proc1 : ' || p1 );
    
    proc2( p1 * p1 );
  END; 
 
  -- Define Package Private Function 
  PROCEDURE proc2( p1 INTEGER ) AS
  BEGIN
    DBMS_OUTPUT.PUT_LINE( 'p1 of proc2 : ' || p1 );
  END; 
END; 
/ 

Package created.

gSQL> CALL pkg1.proc1( 10 );

p1 of proc1 : 10
p1 of proc2 : 100
Procedure Call complete.
```

<a id="1a3727bb0ded6676"></a>
### Compatibility

It is the same as a schema-level procedure.

<a id="c45d1044bce0c0b8"></a>
### For More Information

Refer to [CREATE PROCEDURE](31-psm-sql-references.md#d439613cbc283235).

<a id="4689eec7814aee0e"></a>
## RAISE Statement

<a id="adb843f0886963c0"></a>
### Function

It explicitly generates a user-defined exception.

<a id="3c04aa5b24b24279"></a>
### Syntax

```
<RAISE Statement> ::= 
    RAISE  <Exception-Name>
    ;
```

<a id="ed5bf3b695b0f1f2"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="42b5179eb27681a3"></a>
### Syntax Rules and Parameters

- A name of exception to be raised should be declared in a PL block to which a raise belongs or in DECLARE clause of a superordinate PL block. However, a predefined exception can be raised without a declaration.
- If a raise statement is used within an exception handler, an exception name can be omitted, in this case, the previous exception is spread to the superordinate block.

<a id="8552063d2bc4bef0"></a>
### Description

If it can not be processed in a PL block in which an exception occurred, then it is spread to the superordinate PL block.  
If an exception to be raised does not exist in a PL block including RAISE statement, nor does exist in all exception handlers within a superordinate PL block, then an error occurs.  
It is spread from a PL block in which RAISE exception occurred to a superordinate PL block until it is processed, and it can not be spread to an exception handler of subordinate PL block.

**Propagating user exception**

<a id="4244c3bcae17b55f"></a>
| Raise exception | Exception  handler  SCOPE | Exception  handler | Whether to spread it  to superordinate |
| --- | --- | --- | --- |
| User exception without error code | Same scope | X | It spreads "unhandled exception" error to a superordinate scope. |
| User exception with error code | Superordinate scope | X | It spreads a user exception. |
| User exception with error code | Same scope | X | Itspreads a user defined error code. |
| User exception with error code | Superordinate scope | X | Itspreads a user defined error code. |

<a id="8ca6b98fb70c37c3"></a>
### Examples

```
gSQL> DECLARE
V1 INTEGER;
exception1   EXCEPTION;
exception100 EXCEPTION;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Step1');
    BEGIN
        RAISE exception1;
        DBMS_OUTPUT.PUT_LINE('Step2');
        EXCEPTION WHEN Exception100 THEN DBMS_OUTPUT.PUT_LINE('in Exception');
    END;
    DBMS_OUTPUT.PUT_LINE('Step3');
    EXCEPTION WHEN Exception1 THEN DBMS_OUTPUT.PUT_LINE('out Exception');
    DBMS_OUTPUT.PUT_LINE('Step4');
END;
/
Step1
out Exception
Step4

Anonymous PL block executed.
```

<a id="a7146c5af1ce4368"></a>
### Compatibility

The SQL standard specifies &lt;handler declaration&gt; and &lt;condition declaration&gt;, but it does not support the syntax.

<a id="090eb5d60d10b9b6"></a>
### For More Information

Refer to the following.

- [Exception Handler](#d647934fd391349d)
- [Exception Declaration](#99e4ba38991da3b6)

<a id="27a37ec216747a75"></a>
## Record Variable Declaration

<a id="c1f9a17ea0bbbb96"></a>
### Function

It declares a record type variable in DECLARE section.

<a id="6b2c215096bfd9ce"></a>
### Syntax

```
<declare record variable> ::=
    variable_name <recordType> 
    ;

<recordType> ::=
     <tableName>%ROWTYPE
   | USER_DEFINED_DATA_TYPE
```

<a id="74e9853a9e2618a8"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="f1f2a22dcf9cde92"></a>
### Syntax Rules and Parameters

- Variable_name
    - It is a name of variable to be declared.
    - The length of the variable name should be shorter than 128 bytes.
    - It should be a unique name within a scope (PL block body).
    - A variable with the same name can be declared in a PL block body of nested subordinate.
    - It should be used in scope_name.variable_name form to correctly use the variables of duplicated declaration.
    - When using a variable of duplicated declaration without specifying the scope name, then a variable of the nearest scope is automatically used. 
- Record_type
    - It can use %ROWTYPE and user-defined recordType.
    - For more information about the declaration of recordType, refer to [User Defined Record Type](22-psm-datatypes.md#67c36e8a2d115d52).

<a id="ab0c138a83f9d120"></a>
### Description

- The declared variable has the following features. 
    - It should be a unique name within a scope (PL block body).
    - A variable with the same name can be declared in a PL block body of nested subordinate.
    - It should be used in scope_name.variable_name form to correctly use the variables of duplicated declaration.
    - When using a variable of duplicated declaration without specifying the scope name, then a variable of the nearest scope is automatically used. 
- The declared variable is used in that scope and in its subordinate scope, but ':' is not added unlike an embedded SQL.
- The used variable is operated as a bind parameter (INOUT) for that SQL or a PSM control statement.

<a id="8bab7276edb162fe"></a>
### Examples

```
gSQL> DECLARE
  TYPE MY_REC1 IS RECORD ( F1 INTEGER, F2 VARCHAR(10) );
  V1 MY_REC1;
BEGIN
  V1.F1 := 1;
  V1.F2 := 'AAA';
  INSERT INTO T1 VALUES( V1.F1, V1.F2 );
END;
/

Anonymous PL block executed.


gSQL> COMMIT;

Commit complete.


gSQL> SELECT * FROM T1;

I1 I2
-- ---
 1 AAA

1 row selected.
```

<a id="f6219a2302630c09"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="1ec88e9f3a1b14ed"></a>
## RETURN Statement

<a id="a359b904443b621d"></a>
### Function

It specifies the value of which a function returns, then terminates the function. A procedure does not specify the return value, but terminates the procedure.

<a id="5ffc346a44572211"></a>
### Syntax

```
<return statement> ::=
    RETURN [ return_value_expr ]
    ;
```

<a id="89f01c20d8132474"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.  
It can not be used in the PL block of the table function.

<a id="17c89012af523774"></a>
### Syntax Rules and Parameters

- Return_value_expr
    - It is an expression of a value to be returned, and it can be specified only when it is a function.

<a id="e8acc6eae20bdb72"></a>
### Description

It terminates a currently performing procedure/ function.  
For a function, if RETURN statement is terminated without being performed, or if RETURN statement does not have return_value_expr, then an error occurs.  
It can not be used in the table function.

<a id="0a2c90ee9c2d427b"></a>
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

<a id="403a1970a0a8fcd0"></a>
### Compatibility

It is specified in the SQL standard, but conformance rules do not exist.

<a id="06f1e071dedbe4f2"></a>
## RETURN TABLE Statement

<a id="e99f5003cc83328d"></a>
### Function

It returns the result set of executing the cursor variable's cursor query or the select statement, then terminates the function.

<a id="0d9f43efaa0db88e"></a>
### Syntax

```
<return table statement> ::= 
    RETURN TABLE ( { <cursor variable name> | <select statement> } ) 
    ;
```

<a id="b7671c59b188705a"></a>
### Invocation and Access Rules

It can be used only in the table function within PSM.   
It can be used only in the body section of a table function block.

<a id="bba5495fef5c62ae"></a>
### Syntax Rules and Parameters

- &lt;cursor variable name&gt;
    - It returns the result set by executing the specified cursor variable's cursor query.
    - The cursor variable should be open.
    - The cursor variable's cursor query should have not been fetched.
    - It allows the cursor variable whose cursor query is the select statement only.
- &lt;select statement&gt;
    - It can use the select statement only.
    - It can not use select for update statement and select into statement.

<a id="65c5c2bbc2cec513"></a>
### Description

It returns the result set of executing the cursor variable's cursor query or select statement specified in RETURN TABLE statement.   
RETURN TABLE statement is available only in the table function.

<a id="0fb61d8b5e73158e"></a>
### Examples

```
gSQL> CREATE TABLE t_score( c_grade INTEGER, c_score INTEGER ); 
 
Table created. 
 
gSQL> INSERT INTO t_score VALUES ( 1 , 98 ) , ( 1 , 97 ) , ( 1 , 99 ), 
                                 ( 2 , 95 ) , ( 2 , 98 ) , ( 2 , 92 ), 
                                 ( 3 , 98 ) , ( 3 , 96 ) , ( 3 , 94 ); 
 
9 rows created. 
 
gSQL> COMMIT; 
 
Commit complete.
```

- Example of using the cursor variable

```
gSQL>  
CREATE FUNCTION func_cursor_variable( p_option VARCHAR ) 
  RETURN TABLE( f_class NUMBER, f_score NUMBER ) 
AS 
  s_cur SYS_REFCURSOR; 
BEGIN 
  IF p_option = 'MIN' THEN 
    OPEN s_cur FOR SELECT c_grade, MIN(c_score) FROM t_score GROUP BY c_grade; 
  ELSIF p_option = 'MAX' THEN 
    OPEN s_cur FOR SELECT c_grade, MAX(c_score) FROM t_score GROUP BY c_grade; 
  ELSIF p_option = 'AVG' THEN 
    OPEN s_cur FOR SELECT c_grade, AVG(c_score) FROM t_score GROUP BY c_grade; 
  ELSE 
    OPEN s_cur FOR SELECT NULL, NULL FROM dual; 
  END IF; 
 
  RETURN TABLE( s_cur ); 
END; 
/ 
 
Function created. 
 
gSQL> COMMIT; 
 
Commit complete. 
 
-- Calculate the lowest score in each grade.
gSQL> SELECT * FROM TABLE( func_cursor_variable( 'MIN' ) ); 
 
F_CLASS F_SCORE 
------- ------- 
      1      97 
      2      92 
      3      94 
 
3 rows selected.
```

- Example of using the select statement

```
gSQL>  
CREATE FUNCTION func_select( p_option VARCHAR ) 
    RETURN TABLE( f_class NUMBER, f_score NUMBER ) 
AS 
BEGIN 
  IF p_option = 'MIN' THEN 
    RETURN TABLE ( SELECT c_grade, MIN(c_score) FROM t_score GROUP BY c_grade ); 
  ELSIF p_option = 'MAX' THEN 
    RETURN TABLE ( SELECT c_grade, MAX(c_score) FROM t_score GROUP BY c_grade ); 
  ELSIF p_option = 'AVG' THEN 
    RETURN TABLE ( SELECT c_grade, AVG(c_score) FROM t_score GROUP BY c_grade ); 
  ELSE 
    RETURN TABLE ( SELECT NULL, NULL FROM dual ); 
  END IF; 
END; 
/ 
 
Function created. 
 
-- Calculate the average score in each grade.
gSQL> SELECT * FROM TABLE( func_select( 'AVG' ) ); 
 
F_CLASS F_SCORE 
------- ------- 
      1      98 
      2      95 
      3      96 
 
3 rows selected.
```

<a id="f88d95c23a55a243"></a>
### Compatibility

The SQL standard describes it in &lt;return statement&gt; statement.  
However, the SQL standard does not define the cursor variable.

<a id="7f96ddb2248e659f"></a>
## RETURNING INTO clause

<a id="d4b9475443619a65"></a>
### Function

The data processed in an insert/ update/ delete is returned to a PSM variable.

<a id="de48566ee6dcb359"></a>
### Syntax

```
<Insert, Delete Returning_into_clause> ::=
      [ RETURN | RETURNING ] { * | { <value_expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]

<Update returning into clause> ::=
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] } INTO Variable [, ...]
```

<a id="9eade0b937c871e2"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="e20bc5f5c5295892"></a>
### Syntax Rules and Parameters

A record type variable can not be used being mixed with other types.

<a id="73632fc9481afc79"></a>
### Description

It stores before/ after record of processing an insert/ update/ delete statement through returning into.

<a id="f5d4ef4b5e9eb72b"></a>
### Examples

```
gSQL> DECLARE
  rec t1%ROWTYPE;
BEGIN
    INSERT INTO t1 VALUES (1, 2, 3) RETURNING * INTO rec ;
    UPDATE T1 SET ROW = rec RETURNING * INTO rec;
    DELETE FROM T1 RETURNING * INTO rec;
END;
/

Anonymous PL block executed.
```

<a id="cde7e0dbb81f47e1"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="a870cb9c0d6274b0"></a>
## Routine Characteristics

<a id="93699dea3968454b"></a>
### Function

It specifies the characteristics of the routine.

<a id="4b987d4d50ddc4a3"></a>
### Syntax

```
<deterministic characteristic> ::=
      DETERMINISTIC
    | NOT DETERMINISTIC

 <null-call clause> ::=
      RETURN NULL ON NULL INPUT
    | CALLED ON NULL INPUT

<SQL-data access indication> ::=
      NO SQL
    | CONTAINS SQL
    | READS SQL DATA
    | MODIFIES SQL DATA
```

<a id="ac01fa2e07d7bbae"></a>
### Invocation and Access Rules

It can be used in the following statements.

- [CREATE FUNCTION](31-psm-sql-references.md#8343c001bfba29fc)
- [CREATE PROCEDURE](31-psm-sql-references.md#d439613cbc283235)
- [Function Declaration and Definition](#515fb4aa2f801dc3)
- [Procedure Declaration and Definition](#6cbc67f75778afa6)

<a id="6f3bc6fb8355a884"></a>
### Syntax Rules and Parameters

<a id="4fd91055d85e49d8"></a>
#### deterministic characteristic

It determines whether to return the same result value if inserting the same parameter whenever executing the routine.

- DETERMINISTIC: If the same parameter value is inserted, then the same result value is returned. 
- NOT DETERMINISTIC: Even though the same parameter value is inserted, the same value is not returned.

If &lt;deterministic characteristic&gt; is omitted, then the default value is NOT DETERMINISTIC.  
&lt;deterministic characteristic&gt; is semantic characteristic, and it can not determine the result of executing &lt;routine body&gt;.   
Therefore, even when it is DETERMINISTIC, if pl statement of routine body is not deterministic, then the different results can be returned for the same parameter.

<a id="1346d25efd175034"></a>
#### null-call clause

It determines whether to execute routine when any of the routine parameter is NULL.

- RETURN NULL ON NULL INPUT: If any of routine parameter is NULL, the routine returns NULL.
- CALLED ON NULL INPUT: It executes the routine and returns the result regardless of whether any of routine parameter is NULL.

<a id="4cd02a2ea23de2cc"></a>
#### SQL-data access indication

&lt;SQL-data access indication&gt; can classifies and indicates &lt;pl statement&gt; which can be executed in the routine.

- NO SQL
    - It does not allow any SQL.
    - This option can be used only when &lt;routine body&gt; is &lt;external body&gt;.
- CONTAINS SQL
    - It allows SQL without READ or WRITE property.
- READS SQL DATA
    - It allows even the READable SQL.
- MODIFIES SQL DATA
    - It allows all SQL.

If &lt;SQL-data access indication&gt; is omitted, then the default value is MODIFIES SQL DATA.

<a id="e5b575409d2aaca1"></a>
<table class="table column_count_5"><caption>Whether pl statement is executable according to SQL-data access indication</caption><thead><tr><th class="to_center to_middle" rowspan="2"><div>pl statement</div></th><th class="to_center" colspan="4"><div>Level Of SQL Data Access</div></th></tr><tr><th class="to_center"><div>NO SQL</div></th><th class="to_center"><div>CONTAINS SQL</div></th><th class="to_center"><div>READS SQL DATA</div></th><th class="to_center"><div>WRITE SQL DATA</div></th></tr></thead><tbody><tr><td class="to_left"><div>Assignment
Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Basic Loop
Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Block Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Call Specification</div></td><td class="to_center"><div>Y</div></td><td class="to_center"><div>Y</div></td><td class="to_center"><div>Y</div></td><td class="to_center"><div>Y</div></td></tr><tr><td class="to_left"><div>Case Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Close Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Collection Method 
Invocation</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Continue 
Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Cursor For Loop
Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Delete Statement 
Extension</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Execute Immediate 
Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Exit Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Fetch Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>For Loop Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Goto Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>If Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Insert Statement
Extension</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Insert Into ... 
Update Statement
Extension</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Null Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Open Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Open For 
Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Procedure Call
Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Raise Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Return Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Return Table
Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Select Into 
Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Sql Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>Update Statement
Extension</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td></tr><tr><td class="to_left"><div>While Loop
Statement</div></td><td class="to_center to_middle"><div></div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td><td class="to_center to_middle"><div>Y</div></td></tr></tbody></table>

<a id="b7af7347122ed5d1"></a>
### Description

It specifies the characteristics of the routine.  
Each characteristic should not be redundant.

<a id="887f617a1dff8b5b"></a>
### Examples

- Example of using routine characteristics

```
gSQL>
CREATE OR REPLACE FUNCTION func1( p1 INTEGER,
                                  p2 INTEGER )
   RETURN INTEGER
   DETERMINISTIC
   RETURN NULL ON NULL INPUT
   CONTAINS SQL
AS
  var1 INTEGER;
BEGIN
  var1 := p1 + p2;
  RETURN var1;
END;
/

Function created.
```

- Example of using &lt;deterministic characteristic&gt;

```
gSQL>
CREATE OR REPLACE FUNCTION func1( p1 INTEGER,
                                  p2 INTEGER )
   RETURN INTEGER
   DETERMINISTIC
AS
  var1 INTEGER;
BEGIN
  var1 := p1 + p2;
  RETURN var1;
END;
/

Function created.

gSQL> SELECT func1( 1 , 1 ) FROM dual;

FUNC1( 1 , 1 )
--------------
             2

1 row selected.

gSQL> SELECT func1( 1 , 1 ) FROM dual;

FUNC1( 1 , 1 )
--------------
             2

1 row selected.
```

- Example of wrong usage of &lt;deterministic characteristic&gt;

```
gSQL>
CREATE OR REPLACE FUNCTION func1( p1 INTEGER,
                                  p2 INTEGER )
   RETURN INTEGER
   DETERMINISTIC
AS
  var1 INTEGER;
BEGIN
  var1 := random( p1, p2 );
  RETURN var1;
END;
/

Function created.

gSQL> SELECT func1( 1 , 10 ) FROM dual;

FUNC1( 1 , 10 )
---------------
              3

1 row selected.

gSQL> SELECT func1( 1 , 10 ) FROM dual;

FUNC1( 1 , 10 )
---------------
              5

1 row selected.
```

- Example of using &lt;null-call clause&gt;

```
gSQL>
CREATE OR REPLACE FUNCTION func1( p1 INTEGER,
                                  p2 INTEGER )
   RETURN INTEGER
   RETURN NULL ON NULL INPUT
AS
  var1 INTEGER;
BEGIN
  var1 := 0;

  IF p1 IS NOT NULL THEN
     var1 := var1 + p1;
  END IF;

  IF p2 IS NOT NULL THEN
     var1 := var1 + p2;
  END IF;

  RETURN var1;
END;
/

Function created.

gSQL> SELECT func1( NULL , 1 ) FROM dual;

FUNC1( NULL , 1 )
-----------------
             null

1 row selected.

gSQL> SELECT func1( 1 , 1 ) FROM dual;

FUNC1( 1 , 1 )
--------------
             2

1 row selected.
```

- Example of using &lt;SQL-data access indication&gt;

```
gSQL>
CREATE OR REPLACE FUNCTION func1( p1 INTEGER,
                                  p2 INTEGER )
   RETURN INTEGER
   CONTAINS SQL
AS
  var1 INTEGER;
BEGIN
  var1 := p1 + p2;
  RETURN var1;
END;
/

Function created.

gSQL> SELECT func1( 1 , 1 ) FROM dual;

FUNC1( 1 , 1 )
--------------
             2

1 row selected.
```

```
gSQL>
CREATE OR REPLACE FUNCTION func1( p1 INTEGER,
                                  p2 INTEGER )
   RETURN INTEGER
   CONTAINS SQL
AS
  var1 INTEGER;
BEGIN
  SELECT c1 INTO var1 FROM t1;
  RETURN var1;
END;
/

ERR-01000(16409): Warning: Routine(FUNC1) has compilation errors : 
(1) at (8:3): ERR-2F000(17130): routine sql data access indicator violated
Function created.
```

<a id="93cfcdc92131fad2"></a>
### Compatibility

The following are supported among &lt;routine characteristic&gt; in SQL standard.

- &lt;deterministic characteristic&gt;
- &lt;null-call clause&gt;
- &lt;SQL-data access indication&gt;

<a id="3f1e8ab44422a0a1"></a>
### For More Information

Refer to the following.

- [CREATE FUNCTION](31-psm-sql-references.md#8343c001bfba29fc)
- [CREATE PROCEDURE](31-psm-sql-references.md#d439613cbc283235)
- [Function Declaration and Definition](#515fb4aa2f801dc3)
- [Procedure Declaration and Definition](#6cbc67f75778afa6)

<a id="4b5bfacd1e2e742f"></a>
## %ROWTYPE Attribute

<a id="5c1d82b54fc068a1"></a>
### Function

When declaring a variable, it defines the structure and type the same as those of a specific table, a specific cursor or a result set of a cursor variable.

<a id="0c84b6b2cf0b4c07"></a>
### Syntax

```
<rowtype attribute> ::=
    <identifier chain> % ROWTYPE
```

<a id="2f1024704b6f1786"></a>
### Invocation and Access Rules

- It can be used only within PSM. (e.g. package, procedure, function)
- It can be used only in the declaration section of a PL block.
- When declaring a variable, it can be used only in &lt;data type&gt; section.
- When declaring a record type field, then it can not be used in &lt;data type&gt; section. (It does not support complex data type.)

<a id="2671e1fddc2f4ff1"></a>
### Syntax Rules and Parameters

- Identifier chains are as follows.
    - The name of table, view, synonym to be referenced, or the name of a cursor or a cursor variable

<a id="94aaf050598654af"></a>
### Description

- Search order of the reference targets 
    - Cursor or cursor variable 
    - Base table, view, or synonym

- Reference scope 
    - When referring by using a row attribute, only name and type of columns in a result set of a table or a cursor is referenced.
    - Therefore, it does not refer to NOT NULL constraint or DEFAULT value settings.

<a id="0b4dec248c930627"></a>
### Examples

```
gSQL> CREATE TABLE T1 ( I1 INTEGER NOT NULL, I2 VARCHAR(10) );

Table created.

gSQL> INSERT INTO T1 VALUES( 123, '1234567890' );

1 row created.


gSQL> COMMIT;

Commit complete.


gSQL> DECLARE
  V1 T1%ROWTYPE;
BEGIN
  SELECT * INTO V1.I1, V1.I2 FROM T1; 
  DBMS_OUTPUT.PUT_LINE( 'V1.I1 = ' || V1.I1 || ' V1.I2 = ' || V1.I2 );
END;
/
V1.I1 = 123 V1.I2 = 1234567890

Anonymous PL block executed.
```

<a id="f1ac9dbdfaf9477c"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="08c1c75dd4095e4d"></a>
## Scalar Variable Declaration

<a id="ae649335a98e6cac"></a>
### Function

It declares a scalar variable in the declaration section.

<a id="f2b47ef0379f2c76"></a>
### Syntax

```
<declare scalar variable> ::=
    variable_name <data type> [ <variable initialize clause> ]
    ;

<variable initialize clause> ::=
      [ NOT NULL ] { DEFAULT | := } <value expression>
```

<a id="ef6263791a94edbd"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="42cadc152f89ca6f"></a>
### Syntax Rules and Parameters

- Variable_name
    - It is a name of variable to be declared.
    - The length of the variable name should be shorter than 128 bytes.
    - It should be a unique name within a scope (PL block body).
    - A variable with the same name can be declared in a PL block body of nested subordinate.
    - It should be used in scope_name.variable_name form to correctly use the variables of duplicated declaration.
    - When using a variable of duplicated declaration without specifying the scope name, then a variable of the nearest scope is automatically used. 
- Data_Type
    - It can use all built-in [Data Type](../part-03-sql-manual/11-sql-elements.md#d31560e2b64a41fa) provided in GOLDILOCKS.
- Value_expression
    - It expresses the initial value to specify in the variable. 
    - It can use all constants and expressions supported by GOLDILOCKS except for multi-row functions.

<a id="6d35c615acff8bfc"></a>
### Description

- The declared variable has the following features. 
    - It should be a unique name within a scope (PL block body).
    - A variable with the same name can be declared in a PL block body of nested subordinate.
    - It should be used in scope_name.variable_name form to correctly use the variables of duplicated declaration.
    - When using a variable of duplicated declaration without specifying the scope name, then a variable of the nearest scope is automatically used. 
- The declared variable is used in that scope and in its subordinate scope, but ':' is not added unlike an embedded SQL.
- The used variable is operated as a bind parameter (INOUT) for that SQL or a PSM control statement.

<a id="d1c5c7089ea5109e"></a>
### Examples

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I2 VARCHAR(10) );

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> DECLARE
V1 INTEGER := 100;
V2 INTEGER := -100;
V3 VARCHAR(10) := 'ABC';
BEGIN
  IF V1 > 50 THEN
    INSERT INTO T1 VALUES ( V1, V3 );
  ELSE
    INSERT INTO T1 VALUES ( V2, V3 );
  END IF;
END;
/

Anonymous PL block executed.

gSQL> SELECT * FROM T1;

 I1 I2 
--- ---
100 ABC

1 row selected.
```

<a id="913c112390289c2a"></a>
### Compatibility

- The differences between &lt;declare scalar variable&gt; statement of GOLDILOCKS and that of SQL standard are as follows. 
    - &lt;SQL variable declaration&gt; of the SQL standard declares a variable in a PL block body (after BEGIN), but GOLDILOCKS declares a variable in a separate declaration section.
    - The SQL standard can declare multiple variables of the same type by using a single DECLARE statement, but GOLDILOCKS can declare only a single variable by using a single statement.
    - The SQL standard uses only DEFAULT syntax when setting the initial value, but GOLDILOCKS can use an assign sign (:=).

<a id="25c07665814250e4"></a>
## SELECT INTO Statement

<a id="9afcc762e6ab1b03"></a>
### Function

A single row is returned through SELECT.

<a id="896b2cfb01a96878"></a>
### Syntax

```
<select statement: single row> ::=
    SELECT [ <hint clause> ] [ <set quantifier> ] <select list>
        INTO <select target list>
        <table expression>
    ;

<select target list> ::=
    variable_name [, ...]
```

<a id="0ffe31f3bd60d017"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="f8d7b088d630357d"></a>
### Syntax Rules and Parameters

The rules are the same as those of a select statement except the rules for INTO clause.

<a id="ba1da05770a26021"></a>
### Description

- SELECT INTO is used to return a single record. 
    - If the number of results is zero, "NO_DATA_FOUND" exception occurs. 
    - If the number of results are two or more, "TOO_MANY_ROWS" exception occurs. 
- The result can be returned through a record type variable of PSM. 
    - When using a record type variable, it can not be used being mixed with other type variables

<a id="4c2bc60f4daec5c5"></a>
### Examples

```
gSQL> CREATE TABLE T1 (c1 VARCHAR(20), c2 VARCHAR(20));

Table created.

gSQL> INSERT INTO T1 VALUES ('AAA', 'BBB'), ('BBB', 'CCC');

2 rows created.

gSQL> DECLARE
  v1 VARCHAR(20);
  v2 VARCHAR(20);
BEGIN
  SELECT * INTO v1, v2 FROM T1 WHERE c1 = 'AAA';
  DBMS_OUTPUT.PUT_LINE('V1=' || v1 || ', v2=' || v2);
END;
/
V1=AAA, v2=BBB

Anonymous PL block executed.
```

<a id="c9c16a9e244320e3"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="78bc0f05c5677702"></a>
## SQLCODE Function

<a id="96310491815a7e9e"></a>
### Function

It returns an error code of a statement which was performed just before in PSM.

<a id="902e7fd2c23675fe"></a>
### Syntax

```
<SQLCODE function> ::= SQLCODE
```

<a id="94f0ff020c2ae377"></a>
### Invocation and Access Rules

It can be used only within PSM.

<a id="29b0cbdaa121c2ae"></a>
### Syntax Rules and Parameters

It does not have a separate argument.

<a id="bb28e93ca551a742"></a>
### Description

It returns an error code of a statement performed in PL/ SQL.  
A user-defined exception which does not assign an error code returns to 1 at the time when it is processed by a handler.   
When the error is completely processed by an exception handler, it returns to 0.

<a id="5d767bd02709c44b"></a>
### Examples

```
gSQL> DECLARE
V1 INTEGER;
BEGIN
    DBMS_OUTPUT.PUT_LINE('SQLCODE=[' || SQLCODE || ']');
    DBMS_OUTPUT.PUT_LINE('SQLERRM=[' || SQLERRM || ']');
END;
/
SQLCODE=[0]
SQLERRM=[[SUNJESOFT][PL/SQL][GOLDILOCKS]successful completion]

Anonymous PL block executed.
```

<a id="47762610730e9ac1"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="1157868335bfdf87"></a>
## SQLERRM Function

<a id="7aebdc002efce13b"></a>
### Function

It returns an error message of a statement which was performed just before in PSM.

<a id="fe82cb9a7b2840fc"></a>
### Syntax

```
<SQLERRM function> ::= SQLERRM
```

<a id="36dc6b95c9a69890"></a>
### Invocation and Access Rules

It can be used only within PSM.

<a id="ed212cf40a6c787a"></a>
### Syntax Rules and Parameters

It does not have a separate argument.

<a id="2ac681a7261a13bf"></a>
### Description

It returns an error message of a statement performed in PL/ SQL.  
A user-defined exception which does not assign an error code returns to a user-defined exception at the time when it is processed by a handler.   
When the error is completely processed by an exception handler, it outputs successful completion message.

<a id="5b0398c8ddcf5965"></a>
### Examples

```
gSQL> DECLARE

V1 INTEGER;
BEGIN
    DBMS_OUTPUT.PUT_LINE('SQLCODE=[' || SQLCODE || ']');
    DBMS_OUTPUT.PUT_LINE('SQLERRM=[' || SQLERRM || ']');
END;
/
SQLCODE=[0]
SQLERRM=[[SUNJESOFT][PL/SQL][GOLDILOCKS]successful completion]

Anonymous PL block executed.
```

<a id="d13abb7c028b4daf"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="12c56388d4e40c1c"></a>
## %TYPE Attribute

<a id="7df85b51dad4234c"></a>
### Function

When declaring a variable or defining a specific field of RECORD type, it defines the type the same as the column of a specific table or another variable.

<a id="f6ca55f9d603685e"></a>
### Syntax

```
<type attribute> ::=
    <identifier chain> % TYPE
```

<a id="b12e7a333d19dd37"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.  
It can be used only for &lt;data type&gt; section when declaring a variable or a field of a record type.

<a id="c4ed8b133bd6c1d8"></a>
### Syntax Rules and Parameters

- Identifier_chain
    - It is the name of a table column to be referenced or of the existing declared variable (or a field of the variable).

<a id="d70bcb790a4795e0"></a>
### Description

<a id="defe9c6c04342970"></a>
#### Reference scope

The reference scope according to the referenced object types are as follows.

- When the referenced object is a column of a table
    - It refers to the data type of the column.
    - It does not refer to a constraint (e.g. NOT NULL) of the column.
    - It does not refer to the default initial value of the column.
- When the referenced object is another variable (or a field of a variable)
    - It refers to the data type of the variable (or a field).
    - It refers to a constraint (NOT NULL) of the variable (or a field).
    - It does not refer to the default initial value of the variable (or a field).
- Search order of the referenced target object is as follows.   
  1. The name of a variable (or a field)  
  2. The name of a column

<a id="7d051d1daeb07a5d"></a>
#### NOT NULL Constraints Variables References

It does not refer to the initial value when referring to NOT NULL attribute variable, so a new initial value should be specified.   
Setting an initial value of a field is not supported when using a type attribute for the field of a current record type variable, so NOT NULL type field can not be referenced.

<a id="df175159e57d8eae"></a>
### Examples

```
gSQL> DECLARE
  V1 NUMBER(5,2) := 100.01;
  V2 V1%TYPE;
BEGIN
  DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
  DBMS_OUTPUT.PUT_LINE( 'V2 = ' || V2 );
END;
/
V1 = 100.01
V2 = 

Anonymous PL block executed.
```

<a id="b2d7b1b69779371d"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="0a1eff9c02b8d066"></a>
## UPDATE Statement Extension

<a id="b664d5361843e242"></a>
### Function

A feature altering a record by using a record type variable is added other than a feature consecutively listing the altering target columns of UNDATE statement in PSM.  
It stores the result by using a record type variable in UPDATE (searched) RETURNING INTO clause in PSM.

<a id="48c403e2fa63206e"></a>
### Syntax

```
<update Extension statement : searched> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        <target-list>
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
        [ <returning into clause> ]
    ;

<update statement: positioned> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        <Target-List>
        WHERE CURRENT OF cursor_name
    ;

<result offset clause> ::=
    OFFSET skip_count [ ROW | ROWS ]


<fetch limit clause> ::=
      <fetch first clause>
    | <limit clause>


<fetch first clause> ::=
    FETCH [ FIRST | NEXT ] [ row_count ] [ ROW ONLY | ROWS ONLY ]


<limit clause>
    LIMIT { fetch_row_count | offset_row_count, fetch_row_count | ALL }

<returning into clause> ::=
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] } INTO Variable [, ...]

<target-List> ::=
        SET <set clause> [, ...]
      | SET ROW = <psm_variable>

<set clause> ::=
      column_name = { <value expression> | DEFAULT }
    | ( column_name [, ...] ) = ( { <value expression> | DEFAULT } [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )
```

<a id="41c7e63e3012380e"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="4aadaf6e38825f83"></a>
### Syntax Rules and Parameters

- &lt;PSM_Variable&gt; to be used in UPDATE SET ROW syntax shoould be a variable declared as a record type.
- &lt;Variable&gt; to be used in UPDATE RETURNING INTO syntax does not need to be a record type.
    - However, if a record type is specified, then it can not be used being mixed with other data type variables nor can two or more record type variables be listed.

<a id="c816232c44c4e758"></a>
### Description

It alters the record or stores the result of RETURNING INTO through a record type variable in PSM.

<a id="5e031e0c0b83f15e"></a>
### Examples

```
gSQL> CREATE TABLE T1 (C1 VARCHAR(20), C2 VARCHAR(20));
Table created.

gSQL> INSERT INTO T1 VALUES ('AAA', 'BBB'), ('BBB', 'CCC'), ('CCC', 'DDD');
3 rows created.


gSQL> DECLARE
    v1 t1%ROWTYPE;  
    v2 t1%ROWTYPE;  
BEGIN

    v1.c1 := '1';
    v1.c2 := '2';

    UPDATE T1 SET ROW = v1 WHERE c1 = 'AAA' RETURNING * INTO v2;
    DBMS_OUTPUT.PUT_LINE('SQL%ROWCOUNT=' || SQL%ROWCOUNT );
    DBMS_OUTPUT.PUT_LINE('v2.c1=' || v2.c1 || ', v2.c2=' || v2.c2);
END;
/
SQL%ROWCOUNT=1
v2.c1=1, v2.c2=2

Anonymous PL block executed.

gSQL> SELECT * FROM T1 ORDER BY C1;

C1  C2
--- ---
1   2
BBB CCC
CCC DDD

3 rows selected.
```

<a id="77f9db840632fd84"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="9abf0ef3a214066f"></a>
## WHILE LOOP Statement

<a id="05851649e3e6740d"></a>
### Function

It performs internal statements during &lt;search condition&gt; returns TRUE value.

<a id="a15ed40816faf1a9"></a>
### Syntax

```
<while loop statement> ::=
    WHILE <search condition>
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="64b672920c6f876e"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="963356dbc196fe9d"></a>
### Syntax Rules and Parameters

- Search conditions are as follows.
    - It is a conditional expression which continues to circle a while loop.
    - It should finally return a boolean type.

<a id="ccd1a1e54095cbf5"></a>
### Description

while loop statement performs an internal statement list as long as the evaluation result of &lt;search condition&gt; is TRUE.

<a id="329e6cb4b0801fe4"></a>
### Examples

```
gSQL> DECLARE
V1 integer := 0;
BEGIN
  WHILE V1 < 10 LOOP
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
    V1 := V1 + 1;
  END LOOP;
END;
/
V1 = 0
V1 = 1
V1 = 2
V1 = 3
V1 = 4
V1 = 5
V1 = 6
V1 = 7
V1 = 8
V1 = 9

Anonymous PL block executed.
```

<a id="d055b0540deda7b6"></a>
### Compatibility

&lt;while loop statement&gt; statement is defined as &lt;while statement&gt; in the SQL standard.   
&lt;while statement&gt; of the SQL standard performs loop statement as DO ... END WHILE, but GOLDILOCKS performs it as LOOP ... END LOOP.

<a id="c3e18405cbc48cce"></a>
### For More Information

Refer to the following.

- [CONTINUE Statement](#02a73511f88bd73d)
- [EXIT Statement](#d41640b5f286a508)
- [GOTO Statement](#82bb91693962eb5e)

---

[← 29. Trigger](29-trigger.md) · [Table of contents](../README.md) · [31. PSM SQL References →](31-psm-sql-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
