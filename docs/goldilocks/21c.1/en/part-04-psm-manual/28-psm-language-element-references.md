<a id="90ad387e2b068e4b"></a>

# 28. PSM Language Element References

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/90ad387e2b068e4b)  
> Tag: `21c.1_35_tag`

[← 27. PSM Packages](27-psm-packages.md) · [Table of contents](../README.md) · [29. PSM SQL References →](29-psm-sql-references.md)

<a id="0fd8fe5f37b973c8"></a>
## Assignment Statement

<a id="1d1a6bfb29d71c43"></a>
### Function

Within a PSM block, it stores a value in a variable or in an out-bind parameter.

<a id="7369e131a77e3fdf"></a>
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

<a id="381a1cb4e65e65d8"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="e74d8aab49aaee29"></a>
### Syntax Rules and Parameters

- collection_variable
    - It is the variable name of COLLECTION type declared in DECLARE section.
- index
    - It is the key value which selects an element among elements of collection_variable.
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

<a id="89727e339040b789"></a>
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

<a id="5a0c708303353644"></a>
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

<a id="d8d7d450e9647581"></a>
### Compatibility

The differences between an assignment statement of GOLDILOCKS and that of SQL standard are as follows.

- An assignment statement of the SQL standard defines a singleton variable assignment and a multiple variable assignment, but GOLDILOCKS supports only a singleton variable assignment. 
- An assignment statement of the SQL standard starts with SET keyword, but GOLDILOCKS does not use SET keyword. 
- An assignment statement of the SQL standard uses an equal operator (=) between a target and a value, but GOLDILOCKS uses :=.

**SQL standard compatibility**

<a id="0ea99d7fe4eba50f"></a>
<table><tbody><tr><th align="center">Feature ID</th><th align="center">Description</th><th align="center">Compatibility</th></tr><tr><td align="left">P002</td><td align="left">Computational completeness</td><td align="center">X</td></tr><tr><td align="left">P006</td><td align="left">Multiple assignment</td><td align="center">X</td></tr></tbody></table>

<a id="95c13282b52637d2"></a>
### For More Information

Refer to the followings.

- [Scalar Variable Declaration](#7a7ebe9111f23494)
- [Record Variable Declaration](#de972a22510fc190)
- [COLLECTION Variable Declaration](#22369b32e3fd7e83)
- [Cursor Variable Declaration](#cab0833568619d01)

<a id="fd312ea63b41c8df"></a>
## Basic LOOP Statement

<a id="f94175e4dc0a0c01"></a>
### Function

It repeatedly performs statements within LOOP until the LOOP is terminated by performing GOTO or EXIT.

<a id="d11f8c721ef8fabb"></a>
### Syntax

```
<basic loop statement> ::=
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="171fc6ee14d50a39"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="b83a026df8ddd1f5"></a>
### Syntax Rules and Parameters

- loop_name
    - It is the label name of &lt;basic loop statement&gt;. 
    - Its role is only a comment, so it does not matter even when it is different from the real label name of &lt;basic loop statement&gt;.

<a id="a53d9e30a1c805e8"></a>
### Description

A basic loop statement is repeatedly performs statements within LOOP.  
A basic loop statement is a loop-family statement, so it can be a target statement which GOTO, EXIT, and CONTINUE indicates as a label.

<a id="f3b00ee64cf2e329"></a>
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

<a id="da50c316b4d38189"></a>
### Compatibility

&lt;basic loop statement&gt; statement is as same as &lt;loop statement&gt; of the SQL standard.

**SQL standard compatibility**

<a id="e24dd9efe2cd6379"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="57a5328d0bafc0b4"></a>
### For More Information

Refer to the followings.

- [CONTINUE Statement](#563c79564c66425f)
- [EXIT Statement](#bcad655e91a81cf4)
- [GOTO Statement](#fa8dbf1bbd497d90)

<a id="ac661ad806550306"></a>
## Block (BEGIN .. END)

<a id="b4e394eb2162d3ab"></a>
### Function

It creates a new scope and defines a variable, a cursor, a type and an exception.

<a id="5079cdafc399d7ec"></a>
### Syntax

```
<PSM block> ::=
    [ DECLARE <declare item>... ] BEGIN <SQL procedure statement list> END
    ;

<declare item> ::=
    <variable declaration>
    | <explicit cursor declaration>
    | <explicit cursor definition>
    | <cursor variable declaration>
    | <type definition>
    | <exception declaration>
    | <exception init pragma>
    | <procedure declaration>
    | <procedure definition>
    | <function declaration>
    | <function definition>

<executable statement list> ::=
    [ <label list> ] { <SQL procedure statement> ; }...

<label list> ::=
    { << identifier >>  }...

<SQL procedure statement>
      <PSM Static SQL>
    | <PSM Dynamic SQL>
    | <PSM Control Statement>
```

<a id="30c310cd46539354"></a>
### Invocation and Access Rules

It can be used only within PROCEDURE, FUNCTION or an anonymous block.

<a id="91e37c5048732cdf"></a>
### Syntax Rules and Parameters

- Variable declaration
    - It declares scalar/ record/ array type variables which are to be used in a block.
- Explicit cursor declaration
    - It declares cursors which are to to be used in a block.
- Explicit cursor definition
    - It defines cursors which are to be used in a block.
- Cursor variable declaration
    - It declares a cursor variable to be used in a block.
- Type definition
    - It defines user-defined types which are to be used when declaring variables in a block.
- Exception declaration
    - It defines exceptions to be used in a block.
- Exception init pragma
    - It sets the error code which is to be processed by a user-defined exception. 
- Procedure declaration
    - It declares procedures to be used in a block.
- Procedure definition
    - It defines procedures to be used in a block.
- Function declaration
    - It declares functions to be used in a block.
- Function definition
    - It defines functions to be used in a block.
- Static SQL
    - It indicates Data Manipulation Language (DML) and Data Control Language (DCL) which can be performed in PSM.
- Dynamic SQL
    - It indicates statements related to dynamic query processing supported by GOLDILOCKS PSM.
- PSM Control Statement
    - It indicates various flow control statements supported by GOLDILOCKS PSM.

<a id="2b69568e2c7d4066"></a>
### Description

&lt;psm block&gt; is a basic component of PSM.  
A block can have a declaration part and a exception handling part.  
A block can be duplicated, and the duplicated block has a new subordinate variable scope. A superordinate block can not refer to a variable in a subordinate block.

<a id="4e7e74ae9998d082"></a>
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

<a id="49cf67460f652500"></a>
### Compatibility

&lt;compound statement&gt; of the SQL standard defines ATOMIC /NOT ATOMIC statement which specifies a new savepoint, but GOLDILOCKS does not support it.

**SQL standard compatibility**

<a id="4e2ac4fb8225c59a"></a>
| Feature ID | Description | Remarks |
| --- | --- | --- |
| P002 | Computational completeness | It does not support ATOMIC statement. |

<a id="711d7bbd07b30fe1"></a>
### For More Information

Refer to [Overview of PSM](21-overview-of-psm.md#d2fa247bc25e05a7).

<a id="b66bcb3b838b7ba0"></a>
## CASE Statement

<a id="5300127902952885"></a>
### Function

It performs a statement list satisfying conditions which returns TRUE among given conditions.

<a id="99bd64870ae06921"></a>
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

<a id="92e471aad0fbbc3e"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="c4c7d851c7e2fe86"></a>
### Syntax Rules and Parameters

- Case operand
    - They are all expressions which can be evaluated with a scalar value. 
    - However, it can not include a subquery statement.
- When operand
    - It is an expression to compare whether it is as same as &lt;case operand&gt;.
    - However, it can not include a subquery statement.
- Search condition
    - It is a conditional expression to be performed when the evaluation result of &lt;searched case statement&gt; is TRUE.
    - However, it can not include a subquery statement.
- Executable statement list
    - It is a list of all statements which can be performed within PSM.

<a id="fae3186516192732"></a>
### Description

It performs statements in WHEN clause returning TRUE by evaluating conditions like as IF statement.  
It evaluates conditional expressions in order, and stops evaluating after finding the TRUE conditional clause.  
If the case satisfying the condition does not exist and ELSE clause is not specified, then an error occurs.

<a id="1898e9c74eb8d2ff"></a>
### Examples

<a id="9182adfa464c3670"></a>
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

<a id="c6ac66b4a3c3d00b"></a>
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

<a id="31456fe42dbd3b95"></a>
### Compatibility

CASE statement of the SQL standard defines the comparison of row type (list type) values, but GOLDILOCKS does not support it.  
CASE statement of the SQL standard can define multiple conditions in a list in &lt;when operand&gt; by delimiting them with ',', but GODILOCKS does not support it.

**SQL stantard compatibility**

<a id="b72250b46349c7af"></a>
| Feature ID | Description | Remarks |
| --- | --- | --- |
| P002 | Computational completeness | It does not support P004, P008. |
| P004 | Extended CASE statement | - |
| P008 | Comma-separated predicates in simple CASE statement | - |

<a id="01dc464a2fb89d38"></a>
## CLOSE Statement

<a id="fddbe1c77fe4074c"></a>
### Function

It closes an open cursor.

<a id="5cbd606d92651724"></a>
### Syntax

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="5f77abd24ce0121d"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="71107c35b715c5f0"></a>
### Syntax Rules and Parameters

- cursor_name
    - It is the name of a cursor to be closed.

<a id="b131cee77b8db378"></a>
### Description

It closes an open cursor.  
A closed cursor can be opened again by using an open statement.

<a id="64da9b813e1d3d9b"></a>
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

<a id="a01faf591e3a2274"></a>
### Compatibility

The SQL standard does not define it.

<a id="157b989a854c3a0f"></a>
### For More Information

Refer to the followings.

- [FETCH Statement](#9465148be3936598)
- [OPEN Statement](#9a0949219879d581)

<a id="eaaeb271f6d40333"></a>
## Collection Method Invocation

<a id="2acb96f77086bac1"></a>
### Function

It provides a method which can explores a collection type variable.

<a id="576b8ba189931c5d"></a>
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

<a id="3360f0286b9913c9"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="d637d900fdadc12d"></a>
### Syntax Rules and Parameters

- It can be used only in a variable declared as a collection type.
- FIRST, LAST, COUNT can not have a parameter.
- A parameter should be specified when an object should be specified such as PRIOR, NEXT, EXISTS, DELETE.
- DELETE is operated as same as PSM statement, and it can not return a different variable as a result. (It can not be used in an expression.)

<a id="21df5b92a3d15bc2"></a>
### Description

Refer to the following table.

**Function**

<a id="bd860249be251bb9"></a>
| Name | Function | Return value | Whether to  require an argument |
| --- | --- | --- | --- |
| FIRST | It returns the smallest key. | A key type specified in INDEX OF | X |
| LAST | It returns the biggest key. | A key type specified in INDEX OF | X |
| PRIOR | It returns a key smaller than the input key. | A key type specified in INDEX OF | O |
| NEXT | It returns a key bigger than the input key. | A key type specified in INDEX OF | O |
| COUNT | It returns the stored count. | INTEGER | X |
| DELETE | It deletes a value corresponding to a key. | N/A | O |
| EXISTS | It returns whether a key exists or not. | BOOLEAN | O |

<a id="202242bd723e8260"></a>
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

<a id="596ce8f9d4d35ecc"></a>
### For More Information

Refer to [COLLECTION Variable Declaration](#22369b32e3fd7e83).

<a id="22369b32e3fd7e83"></a>
## COLLECTION Variable Declaration

<a id="7c20f9c8af6982bb"></a>
### Function

It declares a collection variable.

<a id="757d197a0a70f12e"></a>
### Syntax

```
<declare record variable> ::=
    variable_name <collectionType> 
    ;
 
<Collection Type Definition> ::=
    TYPE <Type-Name> IS TABLE OF <Element-Type> INDEX BY <Index-Type>
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

<a id="f87eb4b92eec766f"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="95644f16fd6720d1"></a>
### Syntax Rules and Parameters

- Type-name
    - It specifies the name of a collection type to be used by a user.
- Element-type
    - It specifies the type of an element to be stored in a collection variable. 
- Index-type
    - It specifies the data type of a key stored in a collection variable.

<a id="24e18cd291460081"></a>
### Description

It declares a collection type.

<a id="a454bf522c6af223"></a>
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

<a id="fd13790589701606"></a>
### Compatibility

The SQL standard does not define it.

<a id="cc39725f0f8cfade"></a>
### For More Information

Refer to [Collection Method Invocation](#eaaeb271f6d40333).

<a id="563c79564c66425f"></a>
## CONTINUE Statement

<a id="4a540fa789e07c85"></a>
### Function

It stops currently performing statement list, and performs the next iteration of a superordinate loop statement.

<a id="37834ca5651aa746"></a>
### Syntax

```
<continue statement> ::=
    CONTINUE [ label_name ] [ WHEN condition ] 
    ;
```

<a id="a333ef2e910b43bd"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

A statement with a target label should be one of the following loop family statements.  

• basic loop statement  
• for loop statement  
• while statement  
• forall statement

<a id="2d9c5dc6ba8e159e"></a>
### Syntax Rules and Parameters

- Label name
    - It can have an identifier chain form.
- Condition
    - If it is specified, it returns to a loop statement only when the condition is TRUE.

<a id="d12374afec4ba62d"></a>
### Description

It stops currently performing statement list, and returns to the superordinate loop statement.

If a label is specified, it returns to the superordinate loop statement of the label name.  
If a label is not specified, it returns to the nearest superordinate loop statement.  
If multiple superordinate loop statements with the same names exist, then the nearest statement is selected.  
It can return to a loop statement (exist in a nested scope) which is visible in the current location.

If a condition is specified, then it returns only when the condition is TRUE.  
If a condition is not specified, then it definitely returns.

<a id="1d4040e172aefb63"></a>
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

<a id="c97b43468d256d04"></a>
### Compatibility

&lt;continue statement&gt; statement is similar to &lt;iterate statement&gt; of the SQL standard.  
However, &lt;iterate statement&gt; statement does not provide WHEN condition feature.

<a id="6f8e5abfa1efbe7b"></a>
### For More Information

Refer to the followings.

- [EXIT Statement](#bcad655e91a81cf4)
- [GOTO Statement](#fa8dbf1bbd497d90)

<a id="68a17ca30220d4d1"></a>
## Cursor FOR LOOP Statement

<a id="96925c78b3dabcca"></a>
### Function

It performs loops as many times as the number of rows in the result created by a query or a cursor declared by a user in PSM.

<a id="14c5362e6e7cb1b3"></a>
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

<a id="fe62187f40d75f33"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body of PSM.

<a id="b6c165463ad08411"></a>
### Syntax Rules and Parameters

The variable declared within For~Loop is valid only within that loop scope. (The variable can not be referenced from outside of that Cursor For Loop Block Scope)

<a id="967ce4880ea1c645"></a>
#### When Using Cursor Name

A cursor should already have been declared before performing LOOP by using a cursor name.   
For more information about an actual param, refer to [OPEN Statement](#9a0949219879d581).

<a id="185c20e5efbf7fd0"></a>
#### When Using Cursor Query

It can perform only the query which can be internally processed by using an implicit cursor in GOLDILOCKS such as a select and a returning query.

<a id="987a41993dd299de"></a>
### Description

It performs PSM statements within a loop by turning around loops as many time as the number of results created by a cursor.   
If a cursor becomes invalid (e.g. closed) during LOOP, it does not perform the loop and it processes itas an error.   
If an explicit cursor name is specified and the corresponding cursor is already opened, then it is processed as an error.

The variable to which a result of the cursor specified in FOR LOOP clause is returned is automatically created. (It is created as a row type of the result set to be returned by an execution result of a cursor.)   
However, if an alias for a select target expression which is not a column of a specific table among results of a user cursor query is not specified, then an error may occur.

<a id="d73ae424508cf14b"></a>
### Examples

<a id="7a3090662d2aedb0"></a>
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

<a id="3330858dbb35813d"></a>
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

<a id="ef7e441a32aa82ca"></a>
### For More Information

Refer to the followings.

- [Explicit Cursor Declaration and Definition](#e2ae86aeed2e1869)
- [GOTO Statement](#fa8dbf1bbd497d90)
- [EXIT Statement](#bcad655e91a81cf4)

<a id="cab0833568619d01"></a>
## Cursor Variable Declaration

<a id="6852b3887a9c2257"></a>
### Function

It declares a cursor variable in DECLARE section of PSM.

<a id="7d72b188bae5ace1"></a>
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

<a id="728957958e6cf30f"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of PSM.

<a id="34db59c99fbab632"></a>
### Syntax Rules and Parameters

Specifying the initial value of a cursor variable or assigning a cursor variable is allowed only between cursor variables.

<a id="f5d4e592160fc63c"></a>
### Description

A cursor variable is operated like as a pointer indicating a cursor which is not dependent on a specific cursor.

<a id="54aa19761ddf2818"></a>
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

<a id="58234da9d047bf88"></a>
### For More Information

Refer to the followings.

- [OPEN Statement](#9a0949219879d581)
- [FETCH Statement](#9465148be3936598)
- [CLOSE Statement](#01dc464a2fb89d38)

<a id="ba401bd2d026690c"></a>
## DELETE Statement Extension

<a id="c23bee4e2c5b3ff3"></a>
### Function

It can store the result in RETURNING INTO clause by using a record type variable of PSM.

<a id="0963aef557bd30c3"></a>
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

<a id="9a01909c8e5ccbd9"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of PSM.

<a id="09c6d7d22df92ef4"></a>
### Syntax Rules and Parameters

If a variable to be returned through RETURNING INTO is a record type, then it can not be used by mixing together with a different variable type.

<a id="0bc23b5c3da5dd5b"></a>
### Description

It can store the result in RETURNING INTO clause by using a record type variable of PSM.

<a id="e63532eb663d5f91"></a>
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

<a id="8501e49fbce568cd"></a>
### For More Information

Refer to [Deleting Data](../part-03-sql-manual/12-sql-languages.md#1d595e9bf0a41d8a).

<a id="168590e071e4a16e"></a>
## EXCEPTION_INIT Pragma

<a id="d47e5af96bbea5de"></a>
### Function

It sets the error code which is to be processed by a user-defined exception.

<a id="601bb62be7996624"></a>
### Syntax

```
< PRAGMA EXCEPTION_INIT > ::=
     PRAGMA EXCEPTION_INIT ( <Exception-Name>, <Internal-ErrorCode> ) 
     ;
```

<a id="bfba772b17e58517"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of PSM.

<a id="6b3a9c99a6025578"></a>
### Syntax Rules and Parameters

A predefined exception can not be used in an exception name which is used as an argument. (A predefined exception name can not be declared.)   
An exception name which is used as an argument in the same PL block DECLARE clause should be declared in advance. (Declaration of an exception name in different BLOCK can not be referenced.)   
&lt;Internal-ErrorCode&gt; should be an internal error code existing within DB SYSTEM. (SUCCESS code can not be set.

<a id="a0e5c8ed7b72c3fd"></a>
### Description

A user explicitly declares an exception name corresponding to an error code of DB SYSTEM.

<a id="b0c490a428e85013"></a>
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

<a id="a57159d2e90462d7"></a>
### Compatibility

Error codes are different each other according to a vendor, so it is not compatible each other.

<a id="ad8f06606a92a92c"></a>
### For More Information

Refer to the followings.

- [Exception Declaration](#a3204b1ac8bda008)
- [Exception Handler](#3aa0250e83e64ba4)

<a id="a3204b1ac8bda008"></a>
## Exception Declaration

<a id="f0476b72ed8877ff"></a>
### Function

It declares an exception name within a PL block.

<a id="a46f4c4ec732f93c"></a>
### Syntax

```
< Exception-Declaration Statement > ::=
     <Exception-Name>  EXCEPTION 
     ;
```

<a id="0519c704f5decbc2"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of PSM.

<a id="b6cfb9959f27df86"></a>
### Syntax Rules and Parameters

It can not declare a predefined exception name.   
Duplicated declarations are not allowed in DECLARE clause of the same SCOPE.

<a id="eef0ff841056b667"></a>
### Description

A user explicitly declares an exception.

<a id="bfa4c176e170a725"></a>
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

<a id="c752dbcafa101e76"></a>
### Compatibility

An exception declaration of the standard SQL is as follows, but GOLDILOCKS supports the syntax as above.

```
<condition declaration> ::=
DECLARE <condition name> CONDITION [ FOR <sqlstate value> ]
```

<a id="54cd8d341af429dc"></a>
### For More Information

Refer to the followings.

- [Exception Declaration](#a3204b1ac8bda008)
- [EXCEPTION_INIT Pragma](#168590e071e4a16e)

<a id="3aa0250e83e64ba4"></a>
## Exception Handler

<a id="24855c01a1750abf"></a>
### Function

It performs an operation defined for an exception which is explicitly occurred by a user or an operation defined for an implicit error due to a DB SYSTEM error occurred during performing PL/ SQL.

<a id="d341fad2bd58dcbe"></a>
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

<a id="e3d65531686afd88"></a>
### Invocation and Access Rules

It can be used within a PL block.

<a id="bb7f9d3dd0cf19c3"></a>
### Syntax Rules and Parameters

OTHERS (predefined exception) can not be specified together with another exception name by using OR.  
Duplicated specifying of OTHERS (predefined exception) is not allowed in an exception handler, and OTHERS should be specified at the last.

<a id="b529094f1472903a"></a>
### Description

<a id="387607fb627c081b"></a>
#### Exception Types

<a id="5e32e6adabc9086d"></a>
| Type | Definer | Has error | Has name | Raise implicitly | Raise explicitly |
| --- | --- | --- | --- | --- | --- |
| Predefined | System | Yes | Yes | Yes | Optionally |
| User-defined | User | If user assign | If user assign | No | Yes |

A predefined exception has an exception name and an error code which are specified in advance in GOLDILOCKS.  
Other exceptions are classified into an internally defined exception and a user-defined exception. An internally defined exception is that a user sets the internal error code name of GOLDILOCKS differently from a  predefined exception name, and a user-defined exception is that only the exception name is declared without specifying a separate error code.

<a id="c8073bdf8a5b0e28"></a>
#### Predefined Exception

**Predefined exception type**

<a id="5bccc9fe6b5320cc"></a>
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

<a id="c8472874be6dc6bb"></a>
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

<a id="c4ad8b5e58dbcd63"></a>
### Compatibility

It does not support the SQL standard grammar.

<a id="a3af450720229ef2"></a>
### For More Information

Refer to the followings.

- [EXCEPTION_INIT Pragma](#168590e071e4a16e)
- [Exception Declaration](#a3204b1ac8bda008)

<a id="ebc3b02f3a91e9a5"></a>
## EXECUTE IMMEDIATE Statement

<a id="27dfb0ed339fd4f4"></a>
### Function

It executes a dynamic SQL within PSM.

<a id="953e5ceedb664ca9"></a>
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

<a id="0cfbf9317c3a7302"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="2fad81ad587d7936"></a>
### Syntax Rules and Parameters

<a id="44ea5776e62c8fc0"></a>
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

<a id="82d718399028b127"></a>
#### INTO Clause

The result of performing a dynamic SQL exists, and it is not bound through a marker, but the result of processing an SQL statement is returned. (It is internally a form of an implicit cursor fetch.)   
The syntax is as follows.

```
EXECUTE IMMEDIATE 'SELECT ... FROM .. WHERE ...';
EXECUTE IMMEDIATE 'INSERT ... RETURNING ...';
EXECUTE IMMEDIATE 'UPDATE ... RETURNING ...';
EXECUTE IMMEDIATE 'DELETE ... RETURNING ...';
```

<a id="f9c21bf863cd99cf"></a>
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

<a id="8c07e72bf23e4272"></a>
#### RETURNING Clause

If INSERT/UPDATE/DELETE RETURNING INTO statement is used as a dynamic SQL, the result is returned by binding a variable  specified in USING clause in OUT-mode in GOLDILOCKS.  
The same result can be returned by using RETURNING-INTO clause for the compatibility with other DBMS.

<a id="5d1ebcd0a9afc0ea"></a>
#### Other Rules

- DDL/ DCL can not use any BIND clause. (INTO, USING, RETURNING clause)
- It is used as OUT in INTO clause and RETURNING INTO clause, so a separate bind type can not be specified nor it be simultaneously used together. 
- IN BIND type can use only a scalar type variable. 
- OUT BIND type can use a record type variable, but a scalar type or a record type can not be listed being mixed together.
- A result can not be returned being divided through INTO clause and USING OUT or RETURNING INTO.

<a id="fca20b26b8ef501d"></a>
### Description

- If a dynamic SQL returns the result as a variable specified in INTO clause 
    - A query returning two or more results causes TOO_MANY_ROWS exception. 
    - If the result is zero, it causes NO_DATA_FOUND exception. 
- If a dynamic SQL returns the result as a variable specified in USING or RETURNING clause
    - If two or more variables which are not ARRAY are returned, it causes TOO_MANY_ROWS exception. 
    - If the result is zero, an error does not occur. 
- The followings are results of which DDL/ DCL performs implicit cursor SQL%Attribute variables.
    - SQL%ROWCOUNT = 0 
    - SQL%ISOPEN = FALSE
    - SQL%FOUND = FALSE 
    - SQL%NOTFOUND = TRUE 
- Other dynamic SQLs store SQL%Attribute values corresponding to the processing results of that SQL statement.

<a id="aadee7b2bd819c7e"></a>
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

<a id="bcad655e91a81cf4"></a>
## EXIT Statement

<a id="61570c43c655198b"></a>
### Function

It exits a loop statement which has the given label among superordinate loop statements, then performs the next statement.

<a id="495f10b0f2d5960a"></a>
### Syntax

```
<exit statement> ::=
    EXIT [ label_name ] [ WHEN condition ]
    ;
```

<a id="a813c30b2fd08bf3"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="39ec41fb944202bd"></a>
### Syntax Rules and Parameters

- Label name
    - It is a label name of a loop statement to be exited.
    - It can be in an identifier chain form.
- Condition
    - If a condition is specified, then it can exit a loop statement only when that condition is TRUE.

<a id="3a24c126bba1fb85"></a>
### Description

- It stops currently performing statement list and exits a superordinate loop statement.
- A statement with a target label should be one of the following loop family statements.
    - basic loop statement
    - for loop statement
    - while statement
    - forall statement
- If a label is specified, then it exits a superordinate loop statement which has that label name.
- If a label is not specified, then it exits the nearest superordinate loop statement.
- If multiple superordinate loop statements with the same label names exist, then the nearest statement is selected.
- It can exit only a loop statement (exist in a nested scope) which is visible in the current location.

- If a condition is specified, then it exits only when the condition is TRUE.
- If a condition is not specified, then it definitely exits.

<a id="a9519fa0f4e1f76c"></a>
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

<a id="a075a6610536d8ee"></a>
### Compatibility

It does not exist in the SQL standard.

<a id="cba1f5afd345be5f"></a>
## Explicit Cursor Attribute

<a id="2693642da239fa39"></a>
### Function

It returns the status value of a cursor defined in PSM.

<a id="d4a521907c387509"></a>
### Syntax

```
<Explicit cursor attribute> ::=
    cursor_name '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="2171f0145ae5b7c1"></a>
### Invocation and Access Rules

It can be used only in the body section of PSM.

<a id="2549a10614f27613"></a>
### Syntax Rules and Parameters

- Cursor_name
    - It is the name of a cursor whose status value is to be obtained.

<a id="14e9576a2bcebff2"></a>
### Description

- It returns the status value of a given cursor.
    - ISOPEN: It is whether the current cursor is OPEN.
    - FOUND: It is whether the data is returned by the recent fetch.
    - NOTFOUND: It is an opposite of FOUND.
    - ROWCOUNT: It is the number of fetched records after the cursor is recently OPEN.
- The following values are returned according to the cursor status.

**Results according to the performing moment**

<a id="ba4115e3ce62a0fe"></a>
| Attribute name | Before OPEN | After OPEN | After FETCH | After CLOSE |
| --- | --- | --- | --- | --- |
| ISOPEN | FALSE | TRUE | TRUE | FALSE |
| FOUND | NULL | NULL | TRUE/FALSE | NULL |
| NOTFOUND | NULL | NULL | TRUE/FALSE | NULL |
| ROWCOUNT | NULL | NULL | N (the number) | NULL |

<a id="b900771fcdb13ef7"></a>
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

<a id="5a9c06d1dba44703"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="e2ae86aeed2e1869"></a>
## Explicit Cursor Declaration and Definition

<a id="82194cab8c771c79"></a>
### Function

It declares a cursor in DECLARE section of PSM.

<a id="c8b76dab58e17e6e"></a>
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
    IS select_statement
    ;
```

<a id="f51a03f083f1e556"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="555f81170b50c3c0"></a>
### Syntax Rules and Parameters

<a id="abba836b3edc4166"></a>
#### Cursor Name

It is a cursor name to be declared.   
The length of a cursor name should be shorter than 128 bytes.  
It should be a unique name in that scope.

<a id="6eab078014d0ab0b"></a>
#### RowType

It defines a record type of a cursor.  
The number of select targets specified when defining a cursor should be same, and the data type should be compatible.  
If a rowtype is not specified, then a rowtype which is appropriate to a SELECT target of select_statement specified when defining a cursor is automatically specified.

<a id="df3a33226ad2dcad"></a>
#### Param Name

It is a name which distinguishes parameters within a specific cursor.  
It should be a unique name in that cursor.  
If the name is as same as a name of another variable which can be referenced within a scope, then a parameter of that cursor is preferentially referenced.

<a id="6e62bf9d7ced746d"></a>
#### DataType

It specifies the data type of the corresponding parameter.  
It can use all built-in types provided by GOLDILOCKS and types defined within PSM.  
However, a statement which restricts a scope (precision/ scale) can not be specified in a built-in type, but it is internally specified as the maximum scope of the corresponding data type.

<a id="0d1f10fb546b45e9"></a>
#### Select Statement

It specifies SELECT or SELECT ... FOR UPDATE statement which is to be performed by a cursor.  
It can not use SELECT ... INTO statement.

<a id="9045a8db03525290"></a>
### Description

- &lt;explicit cursor declaration&gt; statement declares or defines a cursor.
    - Cursor declaration: It declares only a name and format of a cursor.
    - Cursor definition: It detailedly defines a name, format of a cursor and SELECT statement to be performed. 
- An explicit cursor is used by defining it after declaration. or it can be used by defining it without a declaration.
- When using an explicit cursor by defining it after declaration, then the cursor name, the parameter specification and the record type definition should exactly match.
- A declaration and a definition of an explicit cursor should exist in the same block.
- An explicit cursor is created when the cursor enters the defined block, and it is automatically CLOSEd and deleted when it exits the block.
- 'MAXIMUM_NAMED_CURSOR_COUNT' property restricts the maximum number of explicit cursors which can be created in a specific time.
- The following variables can be used in SELECT statement performed by an explicit cursor.
    - Parameter of the cursor
    - All PSM variables which can be referenced in a scope at the time of declaration. (It is not a scope of the time of open.)
    - External bind parameter (in case of an anonymous PL block)
- An explicit cursor performing SELECT statement has the following properties.
    - IN_SENSITIVE (Changes by another transaction do not affect it.)
    - NON_SCROLLABLE (It can not fetch the previous record again.)
    - READ_ONLY (Only a read operation is available.)
    - WITH-HOLD (A cursor is not automatically closed even though COMMIT/ ROLLBACK is performed.)
- An explicit cursor performing SELECT ... FOR UPDATE statement has the following properties.
    - IN_SENSITIVE (Changes by another transaction do not affect it.)
    - NON_SCROLLABLE (It can not fetch the previous record again.)
    - UPDATABLE (It can UPDATE/DELETE through a cursor location.)
    - WITHOUT-HOLD (A cursor is automatically closed when COMMIT/ ROLLBACK is performed.)

<a id="235782022a5a77c1"></a>
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
  CURSOR C1( A1 INTEGER, A2 VARCHAR ) RETURN T1%ROWTYPE IS SELECT * FROM T1 WHERE I1 = A1 AND I2 = A2;
  V1 T1%ROWTYPE;
BEGIN
  OPEN C1( 2, 'BBB' );
  FETCH C1 INTO V1;
  DBMS_OUTPUT.PUT_LINE( 'V1.I1 = ' || V1.I1 || ' V1.I2 = ' || V1.I2 );

  CLOSE C1;
END;
/

V1.I1 = 2 V1.I2 = BBB

Anonymous PL block executed.
```

<a id="61c8c8ee016a2cac"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="c97aa3ab97cc705e"></a>
### For More Information

Refer to the followings.

- [OPEN FOR Statement](#6d4cf3147f1dedd7)
- [FETCH Statement](#9465148be3936598)
- [CLOSE Statement](#01dc464a2fb89d38)

<a id="9465148be3936598"></a>
## FETCH Statement

<a id="13e70cbfcc2ea6c1"></a>
### Function

It fetches a single record of OPEN cursor.

<a id="3cf1903ba36a0f0d"></a>
### Syntax

```
<fetch statement> ::=
    FETCH cursor_name <into clause>
    ;

<into clause> ::=
    INTO { variable [ , variable ] .. | record }
```

<a id="50cc04f2c61695f4"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="09cfaa4651b97eec"></a>
### Syntax Rules and Parameters

- Cursor name
    - It is a cursor name to be fetched.
- Variable
    - It is a scalar type variable or a bind parameter which stores a column value among the fetch results.
- Record
    - It is a record type variable to store the entire single record of which is the fetch result.

<a id="7421dbb78891686a"></a>
### Description

It fetches a record from an open cursor, then copies the value to a variable specified in INTO clause.   
If a cursor is declared only but not defined, then an error occurs.  
The cursor should be open.

A variable type given to INTO clause should be compatible with a data type of the fetched record result.  
The number of variables given to INTO clause should be as same as the number of the cursor's SELECT targets.  
However, if a variable given in INTO clause is a record type, then only a single variable should be specified.  
Also, the number of the record variable fields should be as same as the number of SELECT targets.

If a fetch is called when a record to be fetched does not exist, then the value of target variables in INTO clause is not altered.

<a id="3ec8bf43cfb49407"></a>
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

<a id="74e5f8038373b69f"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="f8c26d6a5f5a6b4b"></a>
### For More Information

Refer to the followings.

- [OPEN Statement](#9a0949219879d581)
- [CLOSE Statement](#01dc464a2fb89d38)

<a id="b3eb5133530f8cd3"></a>
## FOR LOOP Statement

<a id="ee0e56eb906724e9"></a>
### Function

As long as an index variable has the given value scope, it performs internal statements by increasing or reversing the index variable by 1.

<a id="ff795c3a804be2b4"></a>
### Syntax

```
<for loop statement> ::=
    FOR index_variable_name IN [ REVERSE ] lower_bound .. upper_bound
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="cf95ef17e572de5a"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="806ddc38f7a46648"></a>
### Syntax Rules and Parameters

- Index variable name
    - It is a variable name to be used as an index in FOR statement. Internally, NATIVE_BIGINT type variable is used.
- Lower bound
    - It should be an integer type. If a number with a floating point is used, then the number below decimal point is rounded up while converting the type. 
- Upper bound
    - It should be an integer type. If a number with a floating point is used, then the number below decimal point is rounded up while converting the type.

<a id="90d64445157d1987"></a>
### Description

*for loop* statement performs an internal statement list by increasing or decreasing the index variable value.

- If REVERSE is specified
    - an index variable is decreased by 1 from upper_bound value, and it terminates execution of *for loop* statement when the index variable value becomes smaller than lower_bound.
    - If upper_bound value is smaller than lower_bound then an internal statement list is not performed.
- If REVERSE is not specified
    - an index variable is increased by 1 from lower_bound, and it terminates execution of *for loop* statement when the index variable value becomes bigger than upper_bound.
    - If lower_bound value is bigger than upper_bound, then an internal statement list is not performed.

<a id="1a00e81e94f1850b"></a>
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

<a id="96a30965397204d3"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="48f032507c6ef843"></a>
### For More Information

Refer to the followings.

- [CONTINUE Statement](#563c79564c66425f)
- [EXIT Statement](#bcad655e91a81cf4)
- [GOTO Statement](#fa8dbf1bbd497d90)

<a id="c51a4fc9ada0cf91"></a>
## Function Declaration and Definition

<a id="6ae93a60b2d55be7"></a>
### Function

It declares and defines a nested function.

<a id="ee317f8967991fb1"></a>
### Syntax

```
<nested function declaration> ::=
    FUNCTION func_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
        RETURN datatype
	;

<nested function definition> ::=
    FUNCTION func_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
        RETURN datatype
        { IS | AS } <item_declaration> BEGIN <pl_stmt_list> END
    ;
```

<a id="5dd0328740a9fcc7"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="1b70116560222c40"></a>
### Syntax Rules and Parameters

<a id="1774f1d6798bf6e9"></a>
#### func_name

It is a name of function to be created, and it should be a unique name in a schema.  
The length of a function name should be shorter than 128 bytes.

<a id="0da3d9a96f750d67"></a>
#### Param Name

It defines a name of an argument to be used in a function.  
The name of each argument should be unique in a function.

<a id="87ae6f5be49de9cf"></a>
#### Bind Type

It specifies a bind type of each argument.  
If it is not specified, the default type is *IN*.

<a id="ec0effecb28ee5c9"></a>
#### Item Declaration

It declares items such as a local variable to be used within a function.  
It can declare all items which can be declared in a PL block.

<a id="3378dfa9da32446b"></a>
#### PL Stmt List

It is a body section of a function, and it lists PL statements to be performed.

<a id="a893e64cf2c60b3b"></a>
### Description

A nested function is a sub program which can be called only within the corresponding procedure.  
Other usages are as same as those of a schema-level function.

<a id="6eed94b22b9b8630"></a>
### Examples

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
  V1 := FUNC1( 10 );
  DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
END;
/
V1 = 100

Anonymous PL block executed.
```

<a id="47aaa4c9e7279753"></a>
### Compatibility

It is as same as a schema-level function.

<a id="552a29793afb2624"></a>
### For More Information

Refer to [CREATE FUNCTION](29-psm-sql-references.md#7acaf940b774cb75).

<a id="fa8dbf1bbd497d90"></a>
## GOTO Statement

<a id="d016b51fb8dd36c3"></a>
### Function

It tries to jump into the nearest statement which has a given label among statements accessible from the current location.

<a id="2b518bffa9f27ff3"></a>
### Syntax

```
<goto statement> ::=
    GOTO label_name
    ;
```

<a id="bd21077bd00cd5bc"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="c78641074883b6f8"></a>
### Syntax Rules and Parameters

- Label_name
    - It is a label name of a statement in which is to be jumped.
    - It can be in an identifier chain form.

<a id="81de9b3b6aba8e5f"></a>
### Description

It starts performing by jumping into a statement which has the corresponding label name.  
If multiple candidate statements exist, then it jumps into the nearest statement.  
It can jump only to a statement (exist in a nested scope) which is visible in the current location.  
Both forward jump and backward jump are possible.

<a id="033efe759a29f6df"></a>
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

<a id="422b614f636c44a2"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="09c97626cbefb182"></a>
### For More Information

Refer to the followings.

- [EXIT Statement](#bcad655e91a81cf4)
- [CONTINUE Statement](#563c79564c66425f)

<a id="da8dce561b100a86"></a>
## IF Statement

<a id="ea56d8e57590a1bf"></a>
### Function

It performs a statement list corresponding to the condition returning TRUE among the given conditions.

<a id="7e5c103c2a2add88"></a>
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

<a id="aa319917fecb8de4"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="8a6326d0c0bba15b"></a>
### Syntax Rules and Parameters

- Search condition
    - It is an expression which can be finally evaluated as a boolean type.
- Executable statement list
    - It is a list of all statements supported by GOLDILOCKS PSM.

<a id="e9e4fca1f6c96fcb"></a>
### Description

Like as CASE statement, it performs statement lists of IF, ELSIF clauses returning TRUE by evaluating conditions.  
If it can not satisfy any condition and &lt;if statement else clause&gt; exists, then it performs the corresponding statement.   
ELSIF clauses evaluates conditional expressions in order, and stops evaluating after finding the TRUE conditional clause.

<a id="8b1f8cb65d184ecc"></a>
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

<a id="a60a8cd7e8871b5a"></a>
### Compatibility

&lt;if statement&gt; statement is as same as a syntax and an operation of the SQL standard.

**SQL standard compatibility**

<a id="1740973b9fd4bcd5"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="dffe47642cb6ba01"></a>
## Implicit Cursor Attribute

<a id="5f290a0a0e13031b"></a>
### Function

It returns the status value of an implicit cursor defined in PSM.

<a id="d56fd0202fd5f282"></a>
### Syntax

```
<Implicit cursor attribute> ::=
    SQL '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="01ce7fb4c7984100"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="3d4eb2d86b44beac"></a>
### Description

- It stores the result of SQL statement which was executed just before. 
    - ISOPEN: It is whether the cursor is OPEN, and it is always set to FALSE.
    - FOUND: It is whether the data is returned by the SQL result of just before. 
    - NOTFOUND: It is an opposite of FOUND.
    - ROWCOUNT: It is the number of records affected by the SQL result of just before.

<a id="e17eeabaa3601197"></a>
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

<a id="a41968db35f643ee"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="86a65b6f5f170ad8"></a>
## INSERT Statement Extension

<a id="462a76aa643a93fc"></a>
### Function

It is an extended feature of an insert statement to input data by specifying record type variable supported in PSM in VALUES clause.

<a id="d613d43712155f93"></a>
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
      VALUES <Value_item> [, ...]
      | VALUES psm_record_type_variable [, ...]


<value-Item> ::=
      ( { <value expression> | DEFAULT } [, ...] ) 


<Returning_into_clause> ::=
      [ RETURN | RETURNING ] { * | { <value_expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]
```

<a id="8c83aeb1a2e140b3"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.  
A PSM insert extension statement can not be used in an original SQL statement of EXECUTE IMMEDIATE.

<a id="4fc6f40bc9794c45"></a>
### Syntax Rules and Parameters

It is operated as same as the basic syntax of an insert statement. However, a feature specifying PSM record type variables are added other than a feature consecutively listing existing value expressions in parentheses in value item.

A PSM record type variable should be specified when using a variable without parentheses in Value_Item.   
When using it in an insert extension statement form, a variable which is not a record type can not be used being mixed.

<a id="91967f58e474763a"></a>
### Description

It stores a record by using a record type variable of PSM other than a general insert statement, or obtains a result through returning into.   
For more information about insert, refer to the following example.

<a id="0e14637eb36af5de"></a>
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

<a id="75415492a5d780f2"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="117144a92f8c2772"></a>
## INSERT INTO ... UPDATE Statement Extension

<a id="47c9b53f5802058a"></a>
### Function

It is the extended function of *insert into .. update* statement. It creates a new row in a table by specifying the record type variable supported by PSM in a values clause, or updates the row by specifying the variable in a set clause.

<a id="4444ffc9974aa224"></a>
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
      VALUES <Value_item> [, ...]
      | VALUES psm_record_type_variable [, ...]

<value-Item> ::=
      ( { <value expression> | DEFAULT } [, ...] ) 

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

<a id="f37f11a794239d4f"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. procedure, function, package)  
It can be used only in the body section of a PL block.

<a id="5ba5fd1b807ef67f"></a>
### Syntax Rules and Parameters

- &lt;values clause&gt;
    - The function specifying PSM record type variable other than consecutively listing existing value expressions in parentheses in the value item has been added. 
    - PSM record type variable should be specified when using the variable without parentheses in the value item.
    - When describing by extending the value item, then the variable other than the record type variable is not allowed.
- &lt;target list&gt; 
    - &lt;PSM_Variable&gt; used in SET ROW statement should be the variable declared as the record type.
- &lt;returning into clause&gt;
    - &lt;Variable&gt; used in RETURNING INTO statement does not need to be a record type. However, if it is specified as a record type, then it can not be used together with other data type variables nor can list two or more record type variables.

<a id="77d84d64c610b0a8"></a>
### Description

Returning into statement in an upsert statement stores the inserted result when insert is executed, and it stores the updated result when update is executed.

<a id="dd8bafeed708826b"></a>
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

<a id="cc8a5829d8ed2122"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="6a84eba346868192"></a>
## NULL Statement

<a id="ee9c743cf1acebe4"></a>
### Function

It is a statement without any feature.

<a id="db987a67d50fc9e1"></a>
### Syntax

```
<null statement> ::=
    NULL
    ;
```

<a id="149ffbeaed77511b"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="5e1c08449636063a"></a>
### Description

It is a statement without any feature, and used to set a label of a specific location.

<a id="b28395af94a5d846"></a>
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

<a id="a51c3869b2e493a7"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="9a0949219879d581"></a>
## OPEN Statement

<a id="97dc9166b754ed7a"></a>
### Function

It executes SELECT statement of a cursor defined in PSM.

<a id="8799d81ae2b35384"></a>
### Syntax

```
<open statement> ::=
    OPEN cursor_name [ <actual param spec> ]
    ;

<actual param spec> ::=
      ( expression [ , expression ] .. )
```

<a id="cce96e442c333f71"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="3c8298490034f8aa"></a>
### Syntax Rules and Parameters

- Cursor_name
    - It is the name of a cursor to be opened.

<a id="1c2c8ddb49b5abec"></a>
### Description

It executes SELECT or SELECT ... FOR UPDATE statement of a defined cursor.  
If a cursor is declared only but is not defined, then an error occurs.  
Values of actual parameters should be compatible with the data type of those parameters.

The number of actual parameters should be same as the number of parameters of a cursor.  
If it is smaller than the number of parameters of a cursor, then the default value should be specified in all other parameters.

<a id="537c0b4237cf59e0"></a>
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

<a id="85e606c7c198d055"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="96add47705fbef0b"></a>
### For More Information

Refer to the followings.

- [CLOSE Statement](#01dc464a2fb89d38)
- [FETCH Statement](#9465148be3936598)

<a id="6d4cf3147f1dedd7"></a>
## OPEN FOR Statement

<a id="ea7d6e34c5a85147"></a>
### Function

It opens a single cursor by executing SELECT statement through a cursor variable defined in PSM.

<a id="a7d2a50823fd6e15"></a>
### Syntax

```
<open statement> ::=
    OPEN cursor_variable_name FOR <select_query>
    ;
```

<a id="907535a2abb76a32"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="ee6876f69874c7fe"></a>
### Syntax Rules and Parameters

- Cursor_Variable_name
    - It is a name of cursor_variable.
- Select_query
    - A select query can use both a static SQL and a dynamic SQL.

<a id="a9dc22d5d2f36ff0"></a>
### Description

It executes SELECT or SELECT ... FOR UPDATE statement of a defined cursor variable.  
If a cursor previously opened by a cursor variable exists, then that cursor is automatically closed.

<a id="b5dac8f3dfffe0d6"></a>
### Examples

```
gSQL> CREATE TABLE T1 (c1 INTEGER, c2 INTEGER, c3 INTEGER);
Table created.

gSQL> INSERT INTO T1 VALUES (1, 1, 1);
1 row created.
gSQL> INSERT INTO T1 VALUES (2, 2, 2);
1 row created.
gSQL> INSERT INTO T1 VALUES (3, 3, 3);
1 row created.
gSQL> INSERT INTO T1 VALUES (4, 4, 4);

gSQL> DECLARE
cv SYS_REFCURSOR;
rec t1%ROWTYPE;
BEGIN
  OPEN cv FOR SELECT * FROM T1;
  DBMS_OUTPUT.PUT_LINE('After Open> CV%ISOPEN=' || CV%ISOPEN);
  LOOP
      FETCH cv INTO rec;
      EXIT WHEN CV%NOTFOUND;

      DBMS_OUTPUT.PUT_LINE('C1=' || rec.c1 || ', C2=' || rec.c2 || ', c3=' || rec.c3 || ', RowCount=' || cv%rowcount);
  END LOOP;
  CLOSE cv;

  DBMS_OUTPUT.PUT_LINE('After Close> CV%ISOPEN=' || CV%ISOPEN);
END;
/
After Open> CV%ISOPEN=TRUE
C1=1, C2=1, c3=1, RowCount=1
C1=2, C2=2, c3=2, RowCount=2
C1=3, C2=3, c3=3, RowCount=3
C1=4, C2=4, c3=4, RowCount=4
After Close> CV%ISOPEN=FALSE

Anonymous PL block executed.
```

<a id="c67082c35cc0894d"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="a03cf04cafd1dc89"></a>
### For More Information

Refer to the followings.

- [Cursor Variable Declaration](#cab0833568619d01)
- [FETCH Statement](#9465148be3936598)
- [CLOSE Statement](#01dc464a2fb89d38)

<a id="d91f48815131a981"></a>
## Procedure Call

<a id="bc9156d69e3ba73f"></a>
### Function

It calls a user-defined procedure, a built-in procedure or a nested procedure.

<a id="046171919d9e73e3"></a>
### Syntax

```
<Procedure call> ::=
    proc_name [ ( expr { , expr } ... ) ]
    ;
```

<a id="c5f9b5dabcce2ae5"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

- The following privileges for the corresponding procedure are required to call the user-defined procedure. 
    - EXECUTE PROCEDURE
    - (EXECUTE PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
    - EXECUTE ANY PROCEDURE ON DATABASE

<a id="25210ffd532ed2f5"></a>
### Syntax Rules and Parameters

- Proc_name
    - It is a name of a procedure to be executed, and it is used in the following format.

<a id="7bd963ff85a75f29"></a>
<table class="table column_count_3"><caption></caption><thead><tr><th class="to_center"><div>Format</div></th><th class="to_center"><div>Syntax</div></th><th class="to_center"><div>Description</div></th></tr></thead><tbody><tr><td class="to_left to_middle"><div>Single identifier</div></td><td class="to_middle"><div>procedure_name</div></td><td><div>It calls the procedure of the given name.

It is searched in the following order.
1. nested procedure
2. schema-level procedure</div></td></tr><tr><td class="to_left to_middle" rowspan="3"><div>identifier chain</div></td><td><div>label_name.procedure_name</div></td><td><div>It calls a nested procedure.</div></td></tr><tr><td><div>schema_name.procedure_name</div></td><td><div>It calls a schema-level procedure.</div></td></tr><tr><td><div>package_name.procedure_name</div></td><td><div>It calls a built-in procedure.</div></td></tr></tbody></table>

If the given the number and type of arguments which were given in the procedure found first are wrong when searching with the given name (proc_name), then it does not search for another procedure but causes an error.

<a id="9f3a85911d199f63"></a>
### Description

It calls a user-defined procedure, a built-in procedure or a nested procedure which was defined an advance.  
The argument value in which the default value is defined can be omitted when calling.

When using a procedure variable or bind parameter (?, :V1) in an argument which were defines as OUT or IN-OUT, then the returned value is obtained.

<a id="01ee87a20806be95"></a>
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

<a id="e4ee96ab8105b5c9"></a>
### Compatibility

The SQL standard requires to use &lt;call statement&gt;.

<a id="809e9ea8094fa81a"></a>
## Procedure Declaration and Definition

<a id="2c0913676099ce8d"></a>
### Function

It declares and defines a nested procedure.

<a id="b36a949d0a9f7ae9"></a>
### Syntax

```
<nested procedure declaration> ::=
        PROCEDURE proc_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
	;

<nested procedure definition> ::=
        PROCEDURE proc_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
        { IS | AS } <item_declaration> BEGIN <pl_stmt_list> END
    ;
```

<a id="ea1cecda84b0543d"></a>
### Invocation and Access Rules

It can be used in PSM declaration section.

<a id="69e69c46079c6e40"></a>
### Syntax Rules and Parameters

- Proc_name
    - It is a name of a procedure to be created, and it should be a unique name in a schema.
    - The length of a procedure name should be shorter than 128 bytes.
- Param_name
    - It defines a name of an argument to be used by a procedure.
    - A name of each argument should be unique in a procedure.
- Bind_type
    - It specifies a bind type of each argument.
    - If it is not specified, the default type is 'IN'.
- Item_declaration
    - It declares items such as a local variable to be used within a procedure.
    - It can declare all items which can be declared in a PL block.
- PL Stmt list
    - It is a body section of a procedure, and it lists PL statements to be performed.

<a id="e58cd41123fa395a"></a>
### Description

A nested procedure is a sub program which can be called only within the corresponding procedure.  
Other usages are as same as those of a schema-level procedure.

<a id="cb46069f316e5974"></a>
### Examples

```
gSQL> DECLARE
  PROCEDURE PROC1( A1 INTEGER )
    IS
    BEGIN
      DBMS_OUTPUT.PUT_LINE( 'A1 = ' || A1 );
    END;
BEGIN
  PROC1( 100 );
END;
/
A1 = 100

Anonymous PL block executed.
```

<a id="6e65253377a2715e"></a>
### Compatibility

It is as same as a schema-level procedure.

<a id="4383f2243461f027"></a>
### For More Information

Refer to [CREATE PROCEDURE](29-psm-sql-references.md#c4195b7175b4b1f4).

<a id="7587422a7c5635da"></a>
## RAISE Statement

<a id="1c1729e2516421a7"></a>
### Function

It explicitly generates a user-defined exception.

<a id="aedd969a9583d17d"></a>
### Syntax

```
<RAISE Statement> ::= 
    RAISE  <Exception-Name>
    ;
```

<a id="fa0b920a8467eb21"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="4e7e0fab4a05088c"></a>
### Syntax Rules and Parameters

- A name of exception to be raised should be declared in a PL block to which a raise belongs or in DECLARE clause of a superordinate PL block. However, a predefined exception can be raised without a declaration.
- If a raise statement is used within an exception handler, an exception name can be omitted, in this case, the previous exception is spread to the superordinate block.

<a id="021053775c89c919"></a>
### Description

If it can not be processed in a PL block in which an exception occured, then it is spread to the superordinate PL block.  
If an exception to be raised does not exist in a PL block including RAISE statement, nor does exist in all exception handlers within a superordinate PL block, then an error occurs.  
It is spread from a PL block in which RAISE exception occurred to a superordinate PL block until it is processed, and it can not be spread to an exception handler of subordinate PL block.

**Propagating user exception**

<a id="116257466ca4a455"></a>
| Raise exception | Exception  handler  SCOPE | Exception  handler | Whether to spread it  to superordinate |
| --- | --- | --- | --- |
| User exception without error code | Same scope | X | It spreads "unhandled exception" error to a superordinate scope. |
| User exception with error code | Superordinate scope | X | It spreads a user exception. |
| User exception with error code | Same scope | X | Itspreads a user defined error code. |
| User exception with error code | Superordinate scope | X | Itspreads a user defined error code. |

<a id="cf19cf41ba578b1c"></a>
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

<a id="f605d18df0133189"></a>
### Compatibility

The SQL standard specifies &lt;handler declaration&gt; and &lt;condition declaration&gt;, but it does not support the syntax.

<a id="8bcad4d5fb146543"></a>
### For More Information

Refer to the followings.

- [Exception Handler](#3aa0250e83e64ba4)
- [Exception Declaration](#a3204b1ac8bda008)

<a id="de972a22510fc190"></a>
## Record Variable Declaration

<a id="224f83b88df65d71"></a>
### Function

It declares a record type variable in DECLARE section.

<a id="71d8efd5f6679bc1"></a>
### Syntax

```
<declare record variable> ::=
    variable_name <recordType> 
    ;

<recordType> ::=
     <tableName>%ROWTYPE
   | USER_DEFINED_DATA_TYPE
```

<a id="23c5077fa8cc5c62"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="c50fb27c771de6dc"></a>
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
    - For more information about the declaration of recordType, refer to [User Defined Record Type](22-psm-datatypes.md#6ffbb5b56611eb22).

<a id="bbd3ef7bf2518a20"></a>
### Description

- The declared variable has the following features. 
    - It should be a unique name within a scope (PL block body).
    - A variable with the same name can be declared in a PL block body of nested subordinate.
    - It should be used in scope_name.variable_name form to correctly use the variables of duplicated declaration.
    - When using a variable of duplicated declaration without specifying the scope name, then a variable of the nearest scope is automatically used. 
- The declared variable is used in that scope and in its subordinate scope, but ':' is not added unlike an embedded SQL.
- The used variable is operated as a bind parameter (INOUT) for that SQL or a PSM control statement.

<a id="1bddc14882cd4c5b"></a>
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

<a id="7d9adf649ce55356"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="8d1f568501900f9a"></a>
## RETURN Statement

<a id="760359cdeb7aa0a1"></a>
### Function

It specifies the value of which a function returns, then terminates the function. A procedure does not specify the return value, but terminates the procedure.

<a id="cefbbad7c4d47c3a"></a>
### Syntax

```
<return statement> ::=
    RETURN [ return_value_expr ]
    ;
```

<a id="ee0aea2af8b15e0a"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="f97418634a298fcb"></a>
### Syntax Rules and Parameters

- Return_value_expr
    - It is an expression of a value to be returned, and it can be specified only when it is a function.

<a id="d65cc0da7e4c32af"></a>
### Description

It terminates a currently performing procedure/ function.  
For a function, if RETURN statement is terminated without being performed, or if RETURN statement does not have return_value_expr, then an error occurs.

<a id="6479ab801d4fe955"></a>
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

<a id="1cbb43caca2918d3"></a>
### Compatibility

It is specified in the SQL standard, but conformance rules do not exist.

<a id="f2eebc3dad425451"></a>
## RETURNING INTO clause

<a id="d0756c6dd65d9316"></a>
### Function

The data processed in an insert/ update/ delete is returned to a PSM variable.

<a id="f44399d3c2d882ca"></a>
### Syntax

```
<Insert, Delete Returning_into_clause> ::=
      [ RETURN | RETURNING ] { * | { <value_expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]

<Update returning into clause> ::=
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] } INTO Variable [, ...]
```

<a id="134dd8e824651076"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="8f75a86805f2866c"></a>
### Syntax Rules and Parameters

A record type variable can not be used being mixed with other types.

<a id="29f51aea1978153d"></a>
### Description

It stores before/ after record of processing an insert/ update/ delete statement through returning into.

<a id="a30a10ac8c3a7ad8"></a>
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

<a id="42d90a17d4308796"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="c03a1a2af0559c90"></a>
## %ROWTYPE Attribute

<a id="b7e0af437df4d6ee"></a>
### Function

When declaring a variable, it defines the structure and type as same as those of a specific table, a specific cursor or a result set of a cursor variable.

<a id="865755ef56658cf8"></a>
### Syntax

```
<rowtype attribute> ::=
    <identifier chain> % ROWTYPE
```

<a id="e67f527eba7bb2f0"></a>
### Invocation and Access Rules

- It can be used only within PSM. (e.g. package, procedure, function)
- It can be used only in the declaration section of a PL block.
- When declaring a variable, it can be used only in &lt;data type&gt; section.
- When declaring a record type field, then it can not be used in &lt;data type&gt; section. (It does not support complex data type.)

<a id="ebc6dee8ec122003"></a>
### Syntax Rules and Parameters

- Identifier chains are as follows.
    - The name of table, view, synonym to be referenced, or the name of a cursor or a cursor variable

<a id="feb09df65402aca6"></a>
### Description

- Search order of the reference targets 
    - Cursor or cursor variable 
    - Base table, view, or synonym

- Reference scope 
    - When referring by using a row attribute, only name and type of columns in a result set of a table or a cursor is referenced.
    - Therefore, it does not refer to NOT NULL constraint or DEFAULT value settings.

<a id="ce4c329688205700"></a>
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

<a id="708595c16b606406"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="7a7ebe9111f23494"></a>
## Scalar Variable Declaration

<a id="1f44db364f0597fb"></a>
### Function

It declares a scalar variable in the declaration section.

<a id="f1fa80d1ae2eb5f4"></a>
### Syntax

```
<declare scalar variable> ::=
    variable_name <data type> [ <variable initialize clause> ]
    ;

<variable initialize clause> ::=
      [ NOT NULL ] { DEFAULT | := } <value expression>
```

<a id="9826aa09197d9e1f"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="d1e758955b4e8442"></a>
### Syntax Rules and Parameters

- Variable_name
    - It is a name of variable to be declared.
    - The length of the variable name should be shorter than 128 bytes.
    - It should be a unique name within a scope (PL block body).
    - A variable with the same name can be declared in a PL block body of nested subordinate.
    - It should be used in scope_name.variable_name form to correctly use the variables of duplicated declaration.
    - When using a variable of duplicated declaration without specifying the scope name, then a variable of the nearest scope is automatically used. 
- Data_Type
    - It can use all built-in [Data Type](../part-03-sql-manual/11-sql-elements.md#0bcfff149f5e9259) provided in GOLDILOCKS.
- Value_expression
    - It expresses the initial value to specify in the variable. 
    - It can use all constants and expressions supported by GOLDILOCKS except for multi-row functions.

<a id="6199ea2f65b48d46"></a>
### Description

- The declared variable has the following features. 
    - It should be a unique name within a scope (PL block body).
    - A variable with the same name can be declared in a PL block body of nested subordinate.
    - It should be used in scope_name.variable_name form to correctly use the variables of duplicated declaration.
    - When using a variable of duplicated declaration without specifying the scope name, then a variable of the nearest scope is automatically used. 
- The declared variable is used in that scope and in its subordinate scope, but ':' is not added unlike an embedded SQL.
- The used variable is operated as a bind parameter (INOUT) for that SQL or a PSM control statement.

<a id="103d13ee4de6636e"></a>
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

<a id="c6c788d518da133f"></a>
### Compatibility

- The differences between &lt;declare scalar variable&gt; statement of GOLDILOCKS and that of SQL standard are as follows. 
    - &lt;SQL variable declaration&gt; of the SQL standard declares a variable in a PL block body (after BEGIN), but GOLDILOCKS declares a variable in a separate declaration section.
    - The SQL standard can declare multiple variables of the same type by using a single DECLARE statement, but GOLDILOCKS can declare only a single variable by using a single statement.
    - The SQL standard uses only DEFAULT syntax when setting the initial value, but GOLDILOCKS can use an assign sign (:=).

<a id="efa1448f1bdf27c5"></a>
## SELECT INTO Statement

<a id="5fc523b78d9ecaeb"></a>
### Function

A single row is returned through SELECT.

<a id="fb41b76f238c99f0"></a>
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

<a id="7a8b831442adfb2c"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="f6fca8f922b21594"></a>
### Syntax Rules and Parameters

The rules are as same as those of a select statement except the rules for INTO clause.

<a id="3526ef412cdbaf75"></a>
### Description

- SELECT INTO is used to return a single record. 
    - If the number of results is zero, "NO_DATA_FOUND" exception occurs. 
    - If the number of results are two or more, "TOO_MANY_ROWS" exception occurs. 
- The result can be returned through a record type variable of PSM. 
    - When using a record type variable, it can not be used being mixed with other type variables

<a id="9fd60ad7d4f198c4"></a>
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

<a id="5fb5d1614671cc64"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="f983d26cbc71bfaa"></a>
## SQLCODE Function

<a id="0a2403dde913b002"></a>
### Function

It returns an error code of a statement which was performed just before in PSM.

<a id="cadf5015f06b8aaf"></a>
### Syntax

```
<SQLCODE function> ::= SQLCODE
```

<a id="c4ee1181c413a089"></a>
### Invocation and Access Rules

It can be used only within PSM.

<a id="b8837d720ad73c0d"></a>
### Syntax Rules and Parameters

It does not have a separate argument.

<a id="8a9ae354165c5a13"></a>
### Description

It returns an error code of a statement performed in PL/ SQL.  
A user-defined exception which does not assign an error code returns to 1 at the time when it is processed by a handler.   
When the error is completely processed by an exception handler, it returns to 0.

<a id="775b5f3b03c4f187"></a>
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

<a id="1ce765a909ffb9f4"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="56ecea6ef4d591b9"></a>
## SQLERRM Function

<a id="808f53f0a6707c35"></a>
### Function

It returns an error message of a statement which was performed just before in PSM.

<a id="47da3269a2e67866"></a>
### Syntax

```
<SQLERRM function> ::= SQLERRM
```

<a id="7dc9bebb262d93d9"></a>
### Invocation and Access Rules

It can be used only within PSM.

<a id="0941f0a20eea6904"></a>
### Syntax Rules and Parameters

It does not have a separate argument.

<a id="6f2e11332942e93f"></a>
### Description

It returns an error message of a statement performed in PL/ SQL.  
A user-defined exception which does not assign an error code returns to a user-defined exception at the time when it is processed by a handler.   
When the error is completely processed by an exception handler, it outputs successful completion message.

<a id="143513cb884586ab"></a>
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

<a id="5ea5571b44c32b00"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="cb62e24f1a8295ac"></a>
## %TYPE Attribute

<a id="e147326ec68953fd"></a>
### Function

When declaring a variable or defining a specific field of RECORD type, it defines the type as same as the column of a specific table or another variable.

<a id="966afe89646856c1"></a>
### Syntax

```
<type attribute> ::=
    <identifier chain> % TYPE
```

<a id="486c0f01fc31117a"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.  
It can be used only for &lt;data type&gt; section when declaring a variable or a field of a record type.

<a id="e89e04a33458a0d2"></a>
### Syntax Rules and Parameters

- Identifier_chain
    - It is the name of a table column to be referenced or of the existing declared variable (or a field of the variable).

<a id="7b3b16f576727e5a"></a>
### Description

<a id="9e215901ddcb6832"></a>
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

<a id="a7bdd2b3e0456291"></a>
#### NOT NULL Constraints Variables References

It does not refer to the initial value when referring to NOT NULL attribute variable, so a new initial value should be specified.   
Setting an initial value of a field is not supported when using a type attribute for the field of a current record type variable, so NOT NULL type field can not be referenced.

<a id="ee3ab24c28487611"></a>
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

<a id="078676c01dfc8b90"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="b070c9a5248efa9f"></a>
## UPDATE Statement Extension

<a id="a56eeecea8b36d3b"></a>
### Function

A feature altering a record by using a record type variable is added other than a feature consecutively listing the altering target columns of UNDATE statement in PSM.  
It stores the result by using a record type variable in UPDATE (searched) RETURNING INTO clause in PSM.

<a id="b2430502e99ea23b"></a>
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

<a id="71606516eccc91be"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="df4a0c8d7da8140b"></a>
### Syntax Rules and Parameters

- &lt;PSM_Variable&gt; to be used in UPDATE SET ROW syntax shoould be a variable declared as a record type.
- &lt;Variable&gt; to be used in UPDATE RETURNING INTO syntax does not need to be a record type.
    - However, if a record type is specified, then it can not be used being mixed with other data type variables nor can two or more record type variables be listed.

<a id="3a23261ea06973da"></a>
### Description

It alters the record or stores the result of RETURNING INTO through a record type variable in PSM.

<a id="2ef100a4458d78be"></a>
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

<a id="a192bd7e23adb608"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="057cf5db41935654"></a>
## WHILE LOOP Statement

<a id="65a426812c6b3195"></a>
### Function

It performs internal statements during &lt;search condition&gt; returns TRUE value.

<a id="f9d81490993cb8d8"></a>
### Syntax

```
<while loop statement> ::=
    WHILE <search condition>
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="fc647360d42b5879"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="daf2b1454346f814"></a>
### Syntax Rules and Parameters

- Search conditions are as follows.
    - It is a conditional expression which continues to circle a while loop.
    - It should finally return a boolean type.

<a id="8576a7666be30919"></a>
### Description

while loop statement performs an internal statement list as long as the evaluation result of &lt;search condition&gt; is TRUE.

<a id="d3f090fe73988efe"></a>
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

<a id="f686834d03fcaf7f"></a>
### Compatibility

&lt;while loop statement&gt; statement is defined as &lt;while statement&gt; in the SQL standard.   
&lt;while statement&gt; of the SQL standard performs loop statement as DO ... END WHILE, but GOLDILOCKS performs it as LOOP ... END LOOP.

<a id="d96eb22c15b2e964"></a>
### For More Information

Refer to the followings.

- [CONTINUE Statement](#563c79564c66425f)
- [EXIT Statement](#bcad655e91a81cf4)
- [GOTO Statement](#fa8dbf1bbd497d90)

---

[← 27. PSM Packages](27-psm-packages.md) · [Table of contents](../README.md) · [29. PSM SQL References →](29-psm-sql-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
