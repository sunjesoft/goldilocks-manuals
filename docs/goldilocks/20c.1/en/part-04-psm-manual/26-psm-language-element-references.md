<a id="9cd160b708abe9a9"></a>

# 26. PSM Language Element References

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/9cd160b708abe9a9)  
> Tag: `20c.1_30_tag`

[← 25. PSM Packages](25-psm-packages.md) · [Table of contents](../README.md) · [27. PSM SQL References →](27-psm-sql-references.md)

<a id="23378deb32d0a5ca"></a>
## Assignment Statement

<a id="f02cd853934ae46e"></a>
### Function

Within a PSM block, it stores a value in a variable or in an out-bind parameter.

<a id="415d14bcac02bef4"></a>
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

<a id="5443ac6e76884f3a"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="b02caeb61464da19"></a>
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

<a id="96c321a33af5eff1"></a>
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

<a id="4da0e5dde07e2576"></a>
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

<a id="c541bfb2f8e8a01b"></a>
### Compatibility

The differences between an assignment statement of GOLDILOCKS and that of SQL standard are as follows.

- An assignment statement of the SQL standard defines a singleton variable assignment and a multiple variable assignment, but GOLDILOCKS supports only a singleton variable assignment. 
- An assignment statement of the SQL standard starts with SET keyword, but GOLDILOCKS does not use SET keyword. 
- An assignment statement of the SQL standard uses an equal operator (=) between a target and a value, but GOLDILOCKS uses :=.

**SQL standard compatibility**

<a id="d6e85ea69410144b"></a>
<table><tbody><tr><th align="center">Feature ID</th><th align="center">Description</th><th align="center">Compatibility</th></tr><tr><td align="left">P002</td><td align="left">Computational completeness</td><td align="center">X</td></tr><tr><td align="left">P006</td><td align="left">Multiple assignment</td><td align="center">X</td></tr></tbody></table>

<a id="69082b795da71b8a"></a>
### For More Information

Refer to the followings.

- [Scalar Variable Declaration](#83596969c1723ddf)
- [Record Variable Declaration](#faf219dd6bfddb69)
- [COLLECTION Variable Declaration](#66d86f7b03ed7ed5)
- [Cursor Variable Declaration](#a942b98d82b238d0)

<a id="6d5c566be5857d96"></a>
## Basic LOOP Statement

<a id="8e5918d5606e782e"></a>
### Function

It repeatedly performs statements within LOOP until the LOOP is terminated by performing GOTO or EXIT.

<a id="cc1d5908cb6b2024"></a>
### Syntax

```
<basic loop statement> ::=
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="f26a9b182ada68db"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="1c7782c29ce0acb4"></a>
### Syntax Rules and Parameters

- loop_name
    - It is the label name of &lt;basic loop statement&gt;. 
    - Its role is only a comment, so it does not matter even when it is different from the real label name of &lt;basic loop statement&gt;.

<a id="457edf39cff7a041"></a>
### Description

A basic loop statement is repeatedly performs statements within LOOP.  
A basic loop statement is a loop-family statement, so it can be a target statement which GOTO, EXIT, and CONTINUE indicates as a label.

<a id="028b5f537185d9b1"></a>
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

<a id="576c3ad3fd8bf6bb"></a>
### Compatibility

&lt;basic loop statement&gt; statement is as same as &lt;loop statement&gt; of the SQL standard.

**SQL standard compatibility**

<a id="3a922e2929f99d52"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="d76fa33a5a63a359"></a>
### For More Information

Refer to the followings.

- [CONTINUE Statement](#36b9610f45b5b1ab)
- [EXIT Statement](#720bf4f5443c1fb7)
- [GOTO Statement](#bf2dbc5e809bdc36)

<a id="27fce0c2a91f696a"></a>
## Block (BEGIN .. END)

<a id="23e226b924c0075d"></a>
### Function

It creates a new scope and defines a variable, a cursor, a type and an exception.

<a id="24e51a252129e0a7"></a>
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

<a id="e0eaafc6ae68e666"></a>
### Invocation and Access Rules

It can be used only within PROCEDURE, FUNCTION or an anonymous block.

<a id="435d79c4690c2d29"></a>
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

<a id="5e0f7e276de48d48"></a>
### Description

&lt;psm block&gt; is a basic component of PSM.  
A block can have a declaration part and a exception handling part.  
A block can be duplicated, and the duplicated block has a new subordinate variable scope. A superordinate block can not refer to a variable in a subordinate block.

<a id="38aabc90e9409267"></a>
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

<a id="65c89d25e047b066"></a>
### Compatibility

&lt;compound statement&gt; of the SQL standard defines ATOMIC /NOT ATOMIC statement which specifies a new savepoint, but GOLDILOCKS does not support it.

**SQL standard compatibility**

<a id="c58d8faf5aac25ed"></a>
| Feature ID | Description | Remarks |
| --- | --- | --- |
| P002 | Computational completeness | It does not support ATOMIC statement. |

<a id="59f2b7c4ef3fbb8a"></a>
### For More Information

Refer to [Overview of PSM](19-overview-of-psm.md#2d83252f81a40d12).

<a id="3c256bb60bdaf4da"></a>
## CASE Statement

<a id="5fb8ba36ab4fce21"></a>
### Function

It performs a statement list satisfying conditions which returns TRUE among given conditions.

<a id="cf39f19034167133"></a>
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

<a id="2c5ab3da2e28dd85"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="befb98a5b1a44def"></a>
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

<a id="5f0170cda56a727c"></a>
### Description

It performs statements in WHEN clause returning TRUE by evaluating conditions like as IF statement.  
It evaluates conditional expressions in order, and stops evaluating after finding the TRUE conditional clause.  
If the case satisfying the condition does not exist and ELSE clause is not specified, then an error occurs.

<a id="4025466769ee0319"></a>
### Examples

<a id="c276c0685ba6b6bf"></a>
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

<a id="b5c03ef21d91077b"></a>
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

<a id="645cf3aec0cf4dd5"></a>
### Compatibility

CASE statement of the SQL standard defines the comparison of row type (list type) values, but GOLDILOCKS does not support it.  
CASE statement of the SQL standard can define multiple conditions in a list in &lt;when operand&gt; by delimiting them with ',', but GODILOCKS does not support it.

**SQL stantard compatibility**

<a id="5901a296e854c31b"></a>
| Feature ID | Description | Remarks |
| --- | --- | --- |
| P002 | Computational completeness | It does not support P004, P008. |
| P004 | Extended CASE statement | - |
| P008 | Comma-separated predicates in simple CASE statement | - |

<a id="a22a74d6c1f26261"></a>
## CLOSE Statement

<a id="64db22c811bfa842"></a>
### Function

It closes an open cursor.

<a id="e5c3b710cbef7c40"></a>
### Syntax

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="620bd2842d648cd4"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="4969e3877ec07ffe"></a>
### Syntax Rules and Parameters

- cursor_name
    - It is the name of a cursor to be closed.

<a id="b92e9d0afd17eb19"></a>
### Description

It closes an open cursor.  
A closed cursor can be opened again by using an open statement.

<a id="ab4acbc38fcb44de"></a>
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

<a id="29e18b62fa7052b4"></a>
### Compatibility

The SQL standard does not define it.

<a id="d1632064e865b69d"></a>
### For More Information

Refer to the followings.

- [FETCH Statement](#a0132e08e778a43b)
- [OPEN Statement](#00e17a7455906cd5)

<a id="275b5cad4eff8e44"></a>
## Collection Method Invocation

<a id="de42a2fcfa3bd616"></a>
### Function

It provides a method which can explores a collection type variable.

<a id="230e2cc87b91a751"></a>
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

<a id="ac4bc51df6830bd8"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="d4b26599032ffdd7"></a>
### Syntax Rules and Parameters

- It can be used only in a variable declared as a collection type.
- FIRST, LAST, COUNT can not have a parameter.
- A parameter should be specified when an object should be specified such as PRIOR, NEXT, EXISTS, DELETE.
- DELETE is operated as same as PSM statement, and it can not return a different variable as a result. (It can not be used in an expression.)

<a id="e47135cbbb00808c"></a>
### Description

Refer to the following table.

**Function**

<a id="f9ddbcfda5f1f53e"></a>
| Name | Function | Return value | Whether to  require an argument |
| --- | --- | --- | --- |
| FIRST | It returns the smallest key. | A key type specified in INDEX OF | X |
| LAST | It returns the biggest key. | A key type specified in INDEX OF | X |
| PRIOR | It returns a key smaller than the input key. | A key type specified in INDEX OF | O |
| NEXT | It returns a key bigger than the input key. | A key type specified in INDEX OF | O |
| COUNT | It returns the stored count. | INTEGER | X |
| DELETE | It deletes a value corresponding to a key. | N/A | O |
| EXISTS | It returns whether a key exists or not. | BOOLEAN | O |

<a id="d68c19740fcd4d47"></a>
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

<a id="52df5e9cb6aa2cb8"></a>
### For More Information

Refer to [COLLECTION Variable Declaration](#66d86f7b03ed7ed5).

<a id="66d86f7b03ed7ed5"></a>
## COLLECTION Variable Declaration

<a id="709b8f0804f9e033"></a>
### Function

It declares a collection variable.

<a id="2e692deb788a6ca9"></a>
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

<a id="7271bf60224b7280"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="ce60ff27a5a92cbf"></a>
### Syntax Rules and Parameters

- Type-name
    - It specifies the name of a collection type to be used by a user.
- Element-type
    - It specifies the type of an element to be stored in a collection variable. 
- Index-type
    - It specifies the data type of a key stored in a collection variable.

<a id="ca7e0b4500668de8"></a>
### Description

It declares a collection type.

<a id="a3e89a9e4b593a0c"></a>
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

<a id="6285ccbbf83b190d"></a>
### Compatibility

The SQL standard does not define it.

<a id="263280aaa3eb6979"></a>
### For More Information

Refer to [Collection Method Invocation](#275b5cad4eff8e44).

<a id="36b9610f45b5b1ab"></a>
## CONTINUE Statement

<a id="b710e9617b4e7217"></a>
### Function

It stops currently performing statement list, and performs the next iteration of a superordinate loop statement.

<a id="d58500e7e566d437"></a>
### Syntax

```
<continue statement> ::=
    CONTINUE [ label_name ] [ WHEN condition ] 
    ;
```

<a id="5a7e4c234509b5fa"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

A statement with a target label should be one of the following loop family statements.  

• basic loop statement  
• for loop statement  
• while statement  
• forall statement

<a id="233c4546502326da"></a>
### Syntax Rules and Parameters

- Label name
    - It can have an identifier chain form.
- Condition
    - If it is specified, it returns to a loop statement only when the condition is TRUE.

<a id="7d3be8e13b6d771f"></a>
### Description

It stops currently performing statement list, and returns to the superordinate loop statement.

If a label is specified, it returns to the superordinate loop statement of the label name.  
If a label is not specified, it returns to the nearest superordinate loop statement.  
If multiple superordinate loop statements with the same names exist, then the nearest statement is selected.  
It can return to a loop statement (exist in a nested scope) which is visible in the current location.

If a condition is specified, then it returns only when the condition is TRUE.  
If a condition is not specified, then it definitely returns.

<a id="a10acf83f1a345b3"></a>
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

<a id="0574713718b3ef16"></a>
### Compatibility

&lt;continue statement&gt; statement is similar to &lt;iterate statement&gt; of the SQL standard.  
However, &lt;iterate statement&gt; statement does not provide WHEN condition feature.

<a id="a6ca32aa217165af"></a>
### For More Information

Refer to the followings.

- [EXIT Statement](#720bf4f5443c1fb7)
- [GOTO Statement](#bf2dbc5e809bdc36)

<a id="268880c518a70e6a"></a>
## Cursor FOR LOOP Statement

<a id="52366ae65e3c44aa"></a>
### Function

It performs loops as many times as the number of rows in the result created by a query or a cursor declared by a user in PSM.

<a id="47a0e5dbe9eba634"></a>
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

<a id="64d1b614e6d55ecf"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body of PSM.

<a id="d3216f67ac7fda21"></a>
### Syntax Rules and Parameters

The variable declared within For~Loop is valid only within that loop scope. (The variable can not be referenced from outside of that Cursor For Loop Block Scope)

<a id="3d52da1d974955ce"></a>
#### When Using Cursor Name

A cursor should already have been declared before performing LOOP by using a cursor name.   
For more information about an actual param, refer to [OPEN Statement](#00e17a7455906cd5).

<a id="077117194efa1862"></a>
#### When Using Cursor Query

It can perform only the query which can be internally processed by using an implicit cursor in GOLDILOCKS such as a select and a returning query.

<a id="8f41751efda975cf"></a>
### Description

It performs PSM statements within a loop by turning around loops as many time as the number of results created by a cursor.   
If a cursor becomes invalid (e.g. closed) during LOOP, it does not perform the loop and it processes itas an error.   
If an explicit cursor name is specified and the corresponding cursor is already opened, then it is processed as an error.

The variable to which a result of the cursor specified in FOR LOOP clause is returned is automatically created. (It is created as a row type of the result set to be returned by an execution result of a cursor.)   
However, if an alias for a select target expression which is not a column of a specific table among results of a user cursor query is not specified, then an error may occur.

<a id="b49db8280c65fa03"></a>
### Examples

<a id="894cbf77c856ef97"></a>
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

<a id="5b104d49cdf8e5e9"></a>
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

<a id="b202a393a3becb1a"></a>
### For More Information

Refer to the followings.

- [Explicit Cursor Declaration and Definition](#84b0782f2864e7fb)
- [GOTO Statement](#bf2dbc5e809bdc36)
- [EXIT Statement](#720bf4f5443c1fb7)

<a id="a942b98d82b238d0"></a>
## Cursor Variable Declaration

<a id="8f31e9bd12c763c5"></a>
### Function

It declares a cursor variable in DECLARE section of PSM.

<a id="cfb41725c198a758"></a>
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

<a id="28b0f448d66b812e"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of PSM.

<a id="e61be707e68bff0b"></a>
### Syntax Rules and Parameters

Specifying the initial value of a cursor variable or assigning a cursor variable is allowed only between cursor variables.

<a id="e5d735566bc1a2f6"></a>
### Description

A cursor variable is operated like as a pointer indicating a cursor which is not dependent on a specific cursor.

<a id="9e91c04886f81853"></a>
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

<a id="00e4ef428236a6da"></a>
### For More Information

Refer to the followings.

- [OPEN Statement](#00e17a7455906cd5)
- [FETCH Statement](#a0132e08e778a43b)
- [CLOSE Statement](#a22a74d6c1f26261)

<a id="9ddb02d81bd78be1"></a>
## DELETE Statement Extension

<a id="20d2cfb7d4502e46"></a>
### Function

It can store the result in RETURNING INTO clause by using a record type variable of PSM.

<a id="ab01ecd8ad01b0f4"></a>
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

<a id="bef77d611ade9e14"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of PSM.

<a id="bea899e9a7cd1417"></a>
### Syntax Rules and Parameters

If a variable to be returned through RETURNING INTO is a record type, then it can not be used by mixing together with a different variable type.

<a id="1a109845e70b426f"></a>
### Description

It can store the result in RETURNING INTO clause by using a record type variable of PSM.

<a id="dbf84c06567afca6"></a>
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

<a id="51dbe354a22db3b3"></a>
### For More Information

Refer to [Deleting Data](../part-03-sql-manual/12-sql-languages.md#5a5e245fa2ba040c).

<a id="4494a23879b154cf"></a>
## EXCEPTION_INIT Pragma

<a id="94d5414fccc88a62"></a>
### Function

It sets the error code which is to be processed by a user-defined exception.

<a id="63d64ee8d7293ae2"></a>
### Syntax

```
< PRAGMA EXCEPTION_INIT > ::=
     PRAGMA EXCEPTION_INIT ( <Exception-Name>, <Internal-ErrorCode> ) 
     ;
```

<a id="c65ad4b2274dbf0c"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of PSM.

<a id="cadca841d245bcca"></a>
### Syntax Rules and Parameters

A predefined exception can not be used in an exception name which is used as an argument. (A predefined exception name can not be declared.)   
An exception name which is used as an argument in the same PL block DECLARE clause should be declared in advance. (Declaration of an exception name in different BLOCK can not be referenced.)   
&lt;Internal-ErrorCode&gt; should be an internal error code existing within DB SYSTEM. (SUCCESS code can not be set.

<a id="ea21e82d7cae04f2"></a>
### Description

A user explicitly declares an exception name corresponding to an error code of DB SYSTEM.

<a id="020f0d24b0ebf35c"></a>
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

<a id="2e3e642bbb2b87a9"></a>
### Compatibility

Error codes are different each other according to a vendor, so it is not compatible each other.

<a id="fe4219e083771506"></a>
### For More Information

Refer to the followings.

- [Exception Declaration](#c4071779e371468d)
- [Exception Handler](#ff744ae389c5dbfb)

<a id="c4071779e371468d"></a>
## Exception Declaration

<a id="bf0fe413edd8f8b4"></a>
### Function

It declares an exception name within a PL block.

<a id="2b178cda4a94f779"></a>
### Syntax

```
< Exception-Declaration Statement > ::=
     <Exception-Name>  EXCEPTION 
     ;
```

<a id="1d5afd7c05828436"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of PSM.

<a id="ee1e6c6fb68fefc4"></a>
### Syntax Rules and Parameters

It can not declare a predefined exception name.   
Duplicated declarations are not allowed in DECLARE clause of the same SCOPE.

<a id="4bfad8af6a49f74a"></a>
### Description

A user explicitly declares an exception.

<a id="d3321ccd0dd7a6f0"></a>
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

<a id="cdb3f29376ee8608"></a>
### Compatibility

An exception declaration of the standard SQL is as follows, but GOLDILOCKS supports the syntax as above.

```
<condition declaration> ::=
DECLARE <condition name> CONDITION [ FOR <sqlstate value> ]
```

<a id="fc0e002cd453297a"></a>
### For More Information

Refer to the followings.

- [Exception Declaration](#c4071779e371468d)
- [EXCEPTION_INIT Pragma](#4494a23879b154cf)

<a id="ff744ae389c5dbfb"></a>
## Exception Handler

<a id="d9d6ee5fc0891aa0"></a>
### Function

It performs an operation defined for an exception which is explicitly occurred by a user or an operation defined for an implicit error due to a DB SYSTEM error occurred during performing PL/ SQL.

<a id="05bfb8caf2186f07"></a>
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

<a id="9131eaf9d5054781"></a>
### Invocation and Access Rules

It can be used within a PL block.

<a id="287dc8bad762be3a"></a>
### Syntax Rules and Parameters

OTHERS (predefined exception) can not be specified together with another exception name by using OR.  
Duplicated specifying of OTHERS (predefined exception) is not allowed in an exception handler, and OTHERS should be specified at the last.

<a id="e52bf7b599e7cb24"></a>
### Description

<a id="44058a26d4380e71"></a>
#### Exception Types

<a id="57f4616c92f18a09"></a>
| Type | Definer | Has error | Has name | Raise implicitly | Raise explicitly |
| --- | --- | --- | --- | --- | --- |
| Predefined | System | Yes | Yes | Yes | Optionally |
| User-defined | User | If user assign | If user assign | No | Yes |

A predefined exception has an exception name and an error code which are specified in advance in GOLDILOCKS.  
Other exceptions are classified into an internally defined exception and a user-defined exception. An internally defined exception is that a user sets the internal error code name of GOLDILOCKS differently from a  predefined exception name, and a user-defined exception is that only the exception name is declared without specifying a separate error code.

<a id="24431e4bf5d1b14e"></a>
#### Predefined Exception

**Predefined exception type**

<a id="587eed0a4827b3ba"></a>
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

<a id="d5faebb8d009d9df"></a>
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

<a id="ca66ac038e759c5d"></a>
### Compatibility

It does not support the SQL standard grammar.

<a id="a1eefb575b111a28"></a>
### For More Information

Refer to the followings.

- [EXCEPTION_INIT Pragma](#4494a23879b154cf)
- [Exception Declaration](#c4071779e371468d)

<a id="fadb749bee6122ee"></a>
## EXECUTE IMMEDIATE Statement

<a id="7258279654ec70a8"></a>
### Function

It executes a dynamic SQL within PSM.

<a id="8289f8e6fde02ed5"></a>
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

<a id="54ad7db65bb2733c"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="75030074802480ae"></a>
### Syntax Rules and Parameters

<a id="d8676f50f9a1f8d9"></a>
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

<a id="9a9c4fd7a10e1917"></a>
#### INTO Clause

The result of performing a dynamic SQL exists, and it is not bound through a marker, but the result of processing an SQL statement is returned. (It is internally a form of an implicit cursor fetch.)   
The syntax is as follows.

```
EXECUTE IMMEDIATE 'SELECT ... FROM .. WHERE ...';
EXECUTE IMMEDIATE 'INSERT ... RETURNING ...';
EXECUTE IMMEDIATE 'UPDATE ... RETURNING ...';
EXECUTE IMMEDIATE 'DELETE ... RETURNING ...';
```

<a id="0594c1ff4cea37b5"></a>
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

<a id="b20a394fe9586c26"></a>
#### RETURNING Clause

If INSERT/UPDATE/DELETE RETURNING INTO statement is used as a dynamic SQL, the result is returned by binding a variable  specified in USING clause in OUT-mode in GOLDILOCKS.  
The same result can be returned by using RETURNING-INTO clause for the compatibility with other DBMS.

<a id="d4c01320e086f9ef"></a>
#### Other Rules

- DDL/ DCL can not use any BIND clause. (INTO, USING, RETURNING clause)
- It is used as OUT in INTO clause and RETURNING INTO clause, so a separate bind type can not be specified nor it be simultaneously used together. 
- IN BIND type can use only a scalar type variable. 
- OUT BIND type can use a record type variable, but a scalar type or a record type can not be listed being mixed together.
- A result can not be returned being divided through INTO clause and USING OUT or RETURNING INTO.

<a id="05fcd301619b77f3"></a>
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

<a id="fa61e5d604ad0902"></a>
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

<a id="720bf4f5443c1fb7"></a>
## EXIT Statement

<a id="6b61b56dc6ae8533"></a>
### Function

It exits a loop statement which has the given label among superordinate loop statements, then performs the next statement.

<a id="3bcb60e3a6352627"></a>
### Syntax

```
<exit statement> ::=
    EXIT [ label_name ] [ WHEN condition ]
    ;
```

<a id="382317c0b5ea0f2a"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="66b13e54ba17d6cb"></a>
### Syntax Rules and Parameters

- Label name
    - It is a label name of a loop statement to be exited.
    - It can be in an identifier chain form.
- Condition
    - If a condition is specified, then it can exit a loop statement only when that condition is TRUE.

<a id="aabdeaaa10d7db5e"></a>
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

<a id="c944a9e01831f90c"></a>
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

<a id="42baf4b88eb2fe2b"></a>
### Compatibility

It does not exist in the SQL standard.

<a id="f92582fa0d3213d5"></a>
## Explicit Cursor Attribute

<a id="2e274ed397d5c417"></a>
### Function

It returns the status value of a cursor defined in PSM.

<a id="42559345e786412f"></a>
### Syntax

```
<Explicit cursor attribute> ::=
    cursor_name '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="8a6a0ab2637ff576"></a>
### Invocation and Access Rules

It can be used only in the body section of PSM.

<a id="9b1d3139d59b99f6"></a>
### Syntax Rules and Parameters

- Cursor_name
    - It is the name of a cursor whose status value is to be obtained.

<a id="f73f12187f254bf0"></a>
### Description

- It returns the status value of a given cursor.
    - ISOPEN: It is whether the current cursor is OPEN.
    - FOUND: It is whether the data is returned by the recent fetch.
    - NOTFOUND: It is an opposite of FOUND.
    - ROWCOUNT: It is the number of fetched records after the cursor is recently OPEN.
- The following values are returned according to the cursor status.

**Results according to the performing moment**

<a id="51fc6a7babb50959"></a>
| Attribute name | Before OPEN | After OPEN | After FETCH | After CLOSE |
| --- | --- | --- | --- | --- |
| ISOPEN | FALSE | TRUE | TRUE | FALSE |
| FOUND | NULL | NULL | TRUE/FALSE | NULL |
| NOTFOUND | NULL | NULL | TRUE/FALSE | NULL |
| ROWCOUNT | NULL | NULL | N (the number) | NULL |

<a id="8eeb0b2bb13204cb"></a>
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

<a id="c5440611d2215bd9"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="84b0782f2864e7fb"></a>
## Explicit Cursor Declaration and Definition

<a id="8d2e0f0b45b877de"></a>
### Function

It declares a cursor in DECLARE section of PSM.

<a id="202c7defab95d722"></a>
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

<a id="db9ed69b447fc684"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="a8dce4e3b95fc446"></a>
### Syntax Rules and Parameters

<a id="d4672e7098929589"></a>
#### Cursor Name

It is a cursor name to be declared.   
The length of a cursor name should be shorter than 128 bytes.  
It should be a unique name in that scope.

<a id="9aee60d1463561d0"></a>
#### RowType

It defines a record type of a cursor.  
The number of select targets specified when defining a cursor should be same, and the data type should be compatible.  
If a rowtype is not specified, then a rowtype which is appropriate to a SELECT target of select_statement specified when defining a cursor is automatically specified.

<a id="4d2a174e20e2b3b8"></a>
#### Param Name

It is a name which distinguishes parameters within a specific cursor.  
It should be a unique name in that cursor.  
If the name is as same as a name of another variable which can be referenced within a scope, then a parameter of that cursor is preferentially referenced.

<a id="495ef7eae91aa74d"></a>
#### DataType

It specifies the data type of the corresponding parameter.  
It can use all built-in types provided by GOLDILOCKS and types defined within PSM.  
However, a statement which restricts a scope (precision/ scale) can not be specified in a built-in type, but it is internally specified as the maximum scope of the corresponding data type.

<a id="03443dc9bf68dc2a"></a>
#### Select Statement

It specifies SELECT or SELECT ... FOR UPDATE statement which is to be performed by a cursor.  
It can not use SELECT ... INTO statement.

<a id="84a38545888dd9bc"></a>
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

<a id="07e0130d5b14e057"></a>
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

<a id="7a64d340d242c1f9"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="7a40bab2a2c84014"></a>
### For More Information

Refer to the followings.

- [OPEN FOR Statement](#3f84a73a5bba8b2c)
- [FETCH Statement](#a0132e08e778a43b)
- [CLOSE Statement](#a22a74d6c1f26261)

<a id="a0132e08e778a43b"></a>
## FETCH Statement

<a id="47143302ad4bc1fb"></a>
### Function

It fetches a single record of OPEN cursor.

<a id="e43dfe9315c4acd6"></a>
### Syntax

```
<fetch statement> ::=
    FETCH cursor_name <into clause>
    ;

<into clause> ::=
    INTO { variable [ , variable ] .. | record }
```

<a id="9acde0de9ef5fd4d"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="1aaeac0a4caa787b"></a>
### Syntax Rules and Parameters

- Cursor name
    - It is a cursor name to be fetched.
- Variable
    - It is a scalar type variable or a bind parameter which stores a column value among the fetch results.
- Record
    - It is a record type variable to store the entire single record of which is the fetch result.

<a id="852d270c51bb3276"></a>
### Description

It fetches a record from an open cursor, then copies the value to a variable specified in INTO clause.   
If a cursor is declared only but not defined, then an error occurs.  
The cursor should be open.

A variable type given to INTO clause should be compatible with a data type of the fetched record result.  
The number of variables given to INTO clause should be as same as the number of the cursor's SELECT targets.  
However, if a variable given in INTO clause is a record type, then only a single variable should be specified.  
Also, the number of the record variable fields should be as same as the number of SELECT targets.

If a fetch is called when a record to be fetched does not exist, then the value of target variables in INTO clause is not altered.

<a id="bc820a299c8edc49"></a>
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

<a id="0a5c33372f32f2aa"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="f02c5c9c67dbbb48"></a>
### For More Information

Refer to the followings.

- [OPEN Statement](#00e17a7455906cd5)
- [CLOSE Statement](#a22a74d6c1f26261)

<a id="dab44995bc36b8f3"></a>
## FOR LOOP Statement

<a id="60573f0382d889b0"></a>
### Function

As long as an index variable has the given value scope, it performs internal statements by increasing or reversing the index variable by 1.

<a id="48154e635302f0b0"></a>
### Syntax

```
<for loop statement> ::=
    FOR index_variable_name IN [ REVERSE ] lower_bound .. upper_bound
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="43f283e0e495f33b"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="88075999d3ce93cc"></a>
### Syntax Rules and Parameters

- Index variable name
    - It is a variable name to be used as an index in FOR statement. Internally, NATIVE_BIGINT type variable is used.
- Lower bound
    - It should be an integer type. If a number with a floating point is used, then the number below decimal point is rounded up while converting the type. 
- Upper bound
    - It should be an integer type. If a number with a floating point is used, then the number below decimal point is rounded up while converting the type.

<a id="cd37c6aeee5f11a4"></a>
### Description

*for loop* statement performs an internal statement list by increasing or decreasing the index variable value.

- If REVERSE is specified
    - an index variable is decreased by 1 from upper_bound value, and it terminates execution of *for loop* statement when the index variable value becomes smaller than lower_bound.
    - If upper_bound value is smaller than lower_bound then an internal statement list is not performed.
- If REVERSE is not specified
    - an index variable is increased by 1 from lower_bound, and it terminates execution of *for loop* statement when the index variable value becomes bigger than upper_bound.
    - If lower_bound value is bigger than upper_bound, then an internal statement list is not performed.

<a id="39f9448f40128836"></a>
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

<a id="e9b0c6dda7d60844"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="75a2d793f92801c5"></a>
### For More Information

Refer to the followings.

- [CONTINUE Statement](#36b9610f45b5b1ab)
- [EXIT Statement](#720bf4f5443c1fb7)
- [GOTO Statement](#bf2dbc5e809bdc36)

<a id="33a80d3472392324"></a>
## Function Declaration and Definition

<a id="e2c31688041425f5"></a>
### Function

It declares and defines a nested function.

<a id="580b1a5dec098051"></a>
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

<a id="465f3a4ed4851f5d"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="1dedc3e3e6240d6f"></a>
### Syntax Rules and Parameters

<a id="171baf4c01159b2b"></a>
#### func_name

It is a name of function to be created, and it should be a unique name in a schema.  
The length of a function name should be shorter than 128 bytes.

<a id="84e0fbad5ea807c8"></a>
#### Param Name

It defines a name of an argument to be used in a function.  
The name of each argument should be unique in a function.

<a id="a8d4f2d6e713c832"></a>
#### Bind Type

It specifies a bind type of each argument.  
If it is not specified, the default type is *IN*.

<a id="440501cca0b3a6ca"></a>
#### Item Declaration

It declares items such as a local variable to be used within a function.  
It can declare all items which can be declared in a PL block.

<a id="b25b88698e791ceb"></a>
#### PL Stmt List

It is a body section of a function, and it lists PL statements to be performed.

<a id="b0fbba7aff3b39aa"></a>
### Description

A nested function is a sub program which can be called only within the corresponding procedure.  
Other usages are as same as those of a schema-level function.

<a id="c4c3c287c252ef06"></a>
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

<a id="bfaf701a075db02e"></a>
### Compatibility

It is as same as a schema-level function.

<a id="c8a5c3813ef324bf"></a>
### For More Information

Refer to [CREATE FUNCTION](27-psm-sql-references.md#d8170858a1ff601a).

<a id="bf2dbc5e809bdc36"></a>
## GOTO Statement

<a id="328356b71fd2e363"></a>
### Function

It tries to jump into the nearest statement which has a given label among statements accessible from the current location.

<a id="ffdeb2c11fe90793"></a>
### Syntax

```
<goto statement> ::=
    GOTO label_name
    ;
```

<a id="add8a7854ad6139e"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="f7ddb88b773a030b"></a>
### Syntax Rules and Parameters

- Label_name
    - It is a label name of a statement in which is to be jumped.
    - It can be in an identifier chain form.

<a id="3e87fa533745c7cf"></a>
### Description

It starts performing by jumping into a statement which has the corresponding label name.  
If multiple candidate statements exist, then it jumps into the nearest statement.  
It can jump only to a statement (exist in a nested scope) which is visible in the current location.  
Both forward jump and backward jump are possible.

<a id="63cbaf73f2eac2df"></a>
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

<a id="f85d154f33d6317a"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="f48476ec9555fd39"></a>
### For More Information

Refer to the followings.

- [EXIT Statement](#720bf4f5443c1fb7)
- [CONTINUE Statement](#36b9610f45b5b1ab)

<a id="6ec0fea929a8c872"></a>
## IF Statement

<a id="29bca9c1f0c62764"></a>
### Function

It performs a statement list corresponding to the condition returning TRUE among the given conditions.

<a id="f0331e5029c4866a"></a>
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

<a id="f479bb9a95841cdf"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="371bdce29d8c3917"></a>
### Syntax Rules and Parameters

- Search condition
    - It is an expression which can be finally evaluated as a boolean type.
- Executable statement list
    - It is a list of all statements supported by GOLDILOCKS PSM.

<a id="8f82d2f95eb289df"></a>
### Description

Like as CASE statement, it performs statement lists of IF, ELSIF clauses returning TRUE by evaluating conditions.  
If it can not satisfy any condition and &lt;if statement else clause&gt; exists, then it performs the corresponding statement.   
ELSIF clauses evaluates conditional expressions in order, and stops evaluating after finding the TRUE conditional clause.

<a id="e06f75c6f2a34046"></a>
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

<a id="745caf0b0768fcd3"></a>
### Compatibility

&lt;if statement&gt; statement is as same as a syntax and an operation of the SQL standard.

**SQL standard compatibility**

<a id="429c1ad527dffe7a"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="5e35f89e032a75f9"></a>
## Implicit Cursor Attribute

<a id="6020f10e4e5158b3"></a>
### Function

It returns the status value of an implicit cursor defined in PSM.

<a id="24f5025f064f8dd4"></a>
### Syntax

```
<Implicit cursor attribute> ::=
    SQL '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="e150f00c6ac898d6"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="2692bd80d485617e"></a>
### Description

- It stores the result of SQL statement which was executed just before. 
    - ISOPEN: It is whether the cursor is OPEN, and it is always set to FALSE.
    - FOUND: It is whether the data is returned by the SQL result of just before. 
    - NOTFOUND: It is an opposite of FOUND.
    - ROWCOUNT: It is the number of records affected by the SQL result of just before.

<a id="0812b95cef127d1e"></a>
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

<a id="7126102818019cca"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="cc2ac86a442f3acd"></a>
## INSERT Statement Extension

<a id="dff05bf99b534779"></a>
### Function

It is an extended feature of an insert statement to input data by specifying record type variable supported in PSM in VALUES clause.

<a id="3ce07454ada8a840"></a>
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

<a id="247f2d2337572271"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.  
A PSM insert extension statement can not be used in an original SQL statement of EXECUTE IMMEDIATE.

<a id="7e6f526ce274f952"></a>
### Syntax Rules and Parameters

It is operated as same as the basic syntax of an insert statement. However, a feature specifying PSM record type variables are added other than a feature consecutively listing existing value expressions in parentheses in value item.

A PSM record type variable should be specified when using a variable without parentheses in Value_Item.   
When using it in an insert extension statement form, a variable which is not a record type can not be used being mixed.

<a id="6b05d0aee0062500"></a>
### Description

It stores a record by using a record type variable of PSM other than a general insert statement, or obtains a result through returning into.   
For more information about insert, refer to the following example.

<a id="cc03a642956f5c1f"></a>
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

<a id="56f4b09e1c9c8cd0"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="d99e3499a1fdd177"></a>
## NULL Statement

<a id="bda5e81d9552184e"></a>
### Function

It is a statement without any feature.

<a id="0c10eeb9761a2293"></a>
### Syntax

```
<null statement> ::=
    NULL
    ;
```

<a id="c6b0c2c34090805e"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="02fb947fd40b6c89"></a>
### Description

It is a statement without any feature, and used to set a label of a specific location.

<a id="2c102f000d75f6c3"></a>
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

<a id="9023d0fbef76206c"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="00e17a7455906cd5"></a>
## OPEN Statement

<a id="94d2e1f9576d618a"></a>
### Function

It executes SELECT statement of a cursor defined in PSM.

<a id="990b5d23a35e5b22"></a>
### Syntax

```
<open statement> ::=
    OPEN cursor_name [ <actual param spec> ]
    ;

<actual param spec> ::=
      ( expression [ , expression ] .. )
```

<a id="cf80d041c80d3105"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="a4b0327366930a5d"></a>
### Syntax Rules and Parameters

- Cursor_name
    - It is the name of a cursor to be opened.

<a id="ab32a67159aa1955"></a>
### Description

It executes SELECT or SELECT ... FOR UPDATE statement of a defined cursor.  
If a cursor is declared only but is not defined, then an error occurs.  
Values of actual parameters should be compatible with the data type of those parameters.

The number of actual parameters should be same as the number of parameters of a cursor.  
If it is smaller than the number of parameters of a cursor, then the default value should be specified in all other parameters.

<a id="259503778d911876"></a>
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

<a id="07eb24d8a4c84aa1"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="fc342a436e3981e5"></a>
### For More Information

Refer to the followings.

- [CLOSE Statement](#a22a74d6c1f26261)
- [FETCH Statement](#a0132e08e778a43b)

<a id="3f84a73a5bba8b2c"></a>
## OPEN FOR Statement

<a id="0b435da4e5a80207"></a>
### Function

It opens a single cursor by executing SELECT statement through a cursor variable defined in PSM.

<a id="bdadbc8584437cc6"></a>
### Syntax

```
<open statement> ::=
    OPEN cursor_variable_name FOR <select_query>
    ;
```

<a id="6fba50ebbc52fa74"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="130a1462f3d9042a"></a>
### Syntax Rules and Parameters

- Cursor_Variable_name
    - It is a name of cursor_variable.
- Select_query
    - A select query can use both a static SQL and a dynamic SQL.

<a id="214d5c530574f84e"></a>
### Description

It executes SELECT or SELECT ... FOR UPDATE statement of a defined cursor variable.  
If a cursor previously opened by a cursor variable exists, then that cursor is automatically closed.

<a id="f3ec10e80b6e564c"></a>
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

<a id="4350c22db1a04214"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="ca2160523391ec94"></a>
### For More Information

Refer to the followings.

- [Cursor Variable Declaration](#a942b98d82b238d0)
- [FETCH Statement](#a0132e08e778a43b)
- [CLOSE Statement](#a22a74d6c1f26261)

<a id="0b7e4b591307be2c"></a>
## Procedure Call

<a id="ae2601b2166777e0"></a>
### Function

It calls a user-defined procedure, a built-in procedure or a nested procedure.

<a id="3b616e9389c1401b"></a>
### Syntax

```
<Procedure call> ::=
    proc_name [ ( expr { , expr } ... ) ]
    ;
```

<a id="dc2eb6869d343aab"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

- The following privileges for the corresponding procedure are required to call the user-defined procedure. 
    - EXECUTE PROCEDURE
    - (EXECUTE PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
    - EXECUTE ANY PROCEDURE ON DATABASE

<a id="4cf92fe1c72b8aea"></a>
### Syntax Rules and Parameters

- Proc_name
    - It is a name of a procedure to be executed, and it is used in the following format.

<a id="43db02207313bd55"></a>
<table class="table column_count_3"><caption></caption><thead><tr><th class="to_center"><div>Format</div></th><th class="to_center"><div>Syntax</div></th><th class="to_center"><div>Description</div></th></tr></thead><tbody><tr><td class="to_left to_middle"><div>Single identifier</div></td><td class="to_middle"><div>procedure_name</div></td><td><div>It calls the procedure of the given name.

It is searched in the following order.
1. nested procedure
2. schema-level procedure</div></td></tr><tr><td class="to_left to_middle" rowspan="3"><div>identifier chain</div></td><td><div>label_name.procedure_name</div></td><td><div>It calls a nested procedure.</div></td></tr><tr><td><div>schema_name.procedure_name</div></td><td><div>It calls a schema-level procedure.</div></td></tr><tr><td><div>package_name.procedure_name</div></td><td><div>It calls a built-in procedure.</div></td></tr></tbody></table>

If the given the number and type of arguments which were given in the procedure found first are wrong when searching with the given name (proc_name), then it does not search for another procedure but causes an error.

<a id="ef3bb332f1a8d925"></a>
### Description

It calls a user-defined procedure, a built-in procedure or a nested procedure which was defined an advance.  
The argument value in which the default value is defined can be omitted when calling.

When using a procedure variable or bind parameter (?, :V1) in an argument which were defines as OUT or IN-OUT, then the returned value is obtained.

<a id="09a8259a45dfcd4e"></a>
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

<a id="c2c048f49a2e3a0a"></a>
### Compatibility

The SQL standard requires to use &lt;call statement&gt;.

<a id="222ac8bbdacc7f59"></a>
## Procedure Declaration and Definition

<a id="cefd6472aeb4fa80"></a>
### Function

It declares and defines a nested procedure.

<a id="8009b41f427a5d61"></a>
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

<a id="e332c9f2394ed857"></a>
### Invocation and Access Rules

It can be used in PSM declaration section.

<a id="c7852e9ec0f9a5dd"></a>
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

<a id="d85d2e17c09febe6"></a>
### Description

A nested procedure is a sub program which can be called only within the corresponding procedure.  
Other usages are as same as those of a schema-level procedure.

<a id="93ef50090a87ad5b"></a>
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

<a id="e25909d93252e1f6"></a>
### Compatibility

It is as same as a schema-level procedure.

<a id="3e8c2a7a71834c82"></a>
### For More Information

Refer to [CREATE PROCEDURE](27-psm-sql-references.md#5d4ca7cc7bd25c89).

<a id="b35809a47e0b8e62"></a>
## RAISE Statement

<a id="2593591e5bf7f6f0"></a>
### Function

It explicitly generates a user-defined exception.

<a id="8e5c5860f8f0363a"></a>
### Syntax

```
<RAISE Statement> ::= 
    RAISE  <Exception-Name>
    ;
```

<a id="43333c49ee56b64e"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="b116360c10406aaf"></a>
### Syntax Rules and Parameters

- A name of exception to be raised should be declared in a PL block to which a raise belongs or in DECLARE clause of a superordinate PL block. However, a predefined exception can be raised without a declaration.
- If a raise statement is used within an exception handler, an exception name can be omitted, in this case, the previous exception is spread to the superordinate block.

<a id="1e17e7a2125ff4bd"></a>
### Description

If it can not be processed in a PL block in which an exception occured, then it is spread to the superordinate PL block.  
If an exception to be raised does not exist in a PL block including RAISE statement, nor does exist in all exception handlers within a superordinate PL block, then an error occurs.  
It is spread from a PL block in which RAISE exception occurred to a superordinate PL block until it is processed, and it can not be spread to an exception handler of subordinate PL block.

**Propagating user exception**

<a id="3899bf19b163c141"></a>
| Raise exception | Exception  handler  SCOPE | Exception  handler | Whether to spread it  to superordinate |
| --- | --- | --- | --- |
| User exception without error code | Same scope | X | It spreads "unhandled exception" error to a superordinate scope. |
| User exception with error code | Superordinate scope | X | It spreads a user exception. |
| User exception with error code | Same scope | X | Itspreads a user defined error code. |
| User exception with error code | Superordinate scope | X | Itspreads a user defined error code. |

<a id="949770433cf716bb"></a>
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

<a id="027d1b92ae40c73b"></a>
### Compatibility

The SQL standard specifies &lt;handler declaration&gt; and &lt;condition declaration&gt;, but it does not support the syntax.

<a id="8d2b5e30b3ba0511"></a>
### For More Information

Refer to the followings.

- [Exception Handler](#ff744ae389c5dbfb)
- [Exception Declaration](#c4071779e371468d)

<a id="faf219dd6bfddb69"></a>
## Record Variable Declaration

<a id="34150bac0deaf0af"></a>
### Function

It declares a record type variable in DECLARE section.

<a id="4438a80fb41acb75"></a>
### Syntax

```
<declare record variable> ::=
    variable_name <recordType> 
    ;

<recordType> ::=
     <tableName>%ROWTYPE
   | USER_DEFINED_DATA_TYPE
```

<a id="5a41c206c5e5e7d3"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="fd13789b3f111ed7"></a>
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
    - For more information about the declaration of recordType, refer to [User Defined Record Type](20-psm-datatypes.md#3da76a459ef80b8a).

<a id="75c47c5bbd0de503"></a>
### Description

- The declared variable has the following features. 
    - It should be a unique name within a scope (PL block body).
    - A variable with the same name can be declared in a PL block body of nested subordinate.
    - It should be used in scope_name.variable_name form to correctly use the variables of duplicated declaration.
    - When using a variable of duplicated declaration without specifying the scope name, then a variable of the nearest scope is automatically used. 
- The declared variable is used in that scope and in its subordinate scope, but ':' is not added unlike an embedded SQL.
- The used variable is operated as a bind parameter (INOUT) for that SQL or a PSM control statement.

<a id="c5f74f867b7f482d"></a>
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

<a id="167d5518acfb8900"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="c66ae725022ccae9"></a>
## RETURN Statement

<a id="33c6eaeaa9c98787"></a>
### Function

It specifies the value of which a function returns, then terminates the function. A procedure does not specify the return value, but terminates the procedure.

<a id="067be9a76073d0ce"></a>
### Syntax

```
<return statement> ::=
    RETURN [ return_value_expr ]
    ;
```

<a id="e273de68e6833aad"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="9b7836ef522cba5e"></a>
### Syntax Rules and Parameters

- Return_value_expr
    - It is an expression of a value to be returned, and it can be specified only when it is a function.

<a id="23db3e7d8008cd22"></a>
### Description

It terminates a currently performing procedure/ function.  
For a function, if RETURN statement is terminated without being performed, or if RETURN statement does not have return_value_expr, then an error occurs.

<a id="b147c64fce7b286e"></a>
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

<a id="1c4913252f6a5607"></a>
### Compatibility

It is specified in the SQL standard, but conformance rules do not exist.

<a id="4fa1b64b32acf502"></a>
## RETURNING INTO clause

<a id="6add4b7f66667c3b"></a>
### Function

The data processed in an insert/ update/ delete is returned to a PSM variable.

<a id="b942d7bcc189e2c9"></a>
### Syntax

```
<Insert, Delete Returning_into_clause> ::=
      [ RETURN | RETURNING ] { * | { <value_expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]

<Update returning into clause> ::=
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] } INTO Variable [, ...]
```

<a id="7d27b611156dfab9"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="8ea547c9520fad0c"></a>
### Syntax Rules and Parameters

A record type variable can not be used being mixed with other types.

<a id="ff012e26b67a7eee"></a>
### Description

It stores before/ after record of processing an insert/ update/ delete statement through returning into.

<a id="b4542880c6847ec8"></a>
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

<a id="9abe67835f974ba0"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="1f7504159c9f47b0"></a>
## %ROWTYPE Attribute

<a id="423c86d8cc96bcf3"></a>
### Function

When declaring a variable, it defines the structure and type as same as those of a specific table, a specific cursor or a result set of a cursor variable.

<a id="6ed15abb0c825dda"></a>
### Syntax

```
<rowtype attribute> ::=
    <identifier chain> % ROWTYPE
```

<a id="55f882b1ed1c3ad6"></a>
### Invocation and Access Rules

- It can be used only within PSM. (e.g. package, procedure, function)
- It can be used only in the declaration section of a PL block.
- When declaring a variable, it can be used only in &lt;data type&gt; section.
- When declaring a record type field, then it can not be used in &lt;data type&gt; section. (It does not support complex data type.)

<a id="59f8c0a06c2ef12d"></a>
### Syntax Rules and Parameters

- Identifier chains are as follows.
    - The name of table, view, synonym to be referenced, or the name of a cursor or a cursor variable

<a id="6aa0e9667776dda1"></a>
### Description

- Search order of the reference targets 
    - Cursor or cursor variable 
    - Base table, view, or synonym

- Reference scope 
    - When referring by using a row attribute, only name and type of columns in a result set of a table or a cursor is referenced.
    - Therefore, it does not refer to NOT NULL constraint or DEFAULT value settings.

<a id="c7b6471e16eacffc"></a>
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

<a id="2be8e8355c7dc0a5"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="83596969c1723ddf"></a>
## Scalar Variable Declaration

<a id="a2d81e4ad04e8e46"></a>
### Function

It declares a scalar variable in the declaration section.

<a id="cacfa1f3da2e063f"></a>
### Syntax

```
<declare scalar variable> ::=
    variable_name <data type> [ <variable initialize clause> ]
    ;

<variable initialize clause> ::=
      [ NOT NULL ] { DEFAULT | := } <value expression>
```

<a id="0c3481de7abe081c"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="4b1f71e5393b5ef1"></a>
### Syntax Rules and Parameters

- Variable_name
    - It is a name of variable to be declared.
    - The length of the variable name should be shorter than 128 bytes.
    - It should be a unique name within a scope (PL block body).
    - A variable with the same name can be declared in a PL block body of nested subordinate.
    - It should be used in scope_name.variable_name form to correctly use the variables of duplicated declaration.
    - When using a variable of duplicated declaration without specifying the scope name, then a variable of the nearest scope is automatically used. 
- Data_Type
    - It can use all built-in [Data Type](../part-03-sql-manual/11-sql-elements.md#e7178d2ff000b62c) provided in GOLDILOCKS.
- Value_expression
    - It expresses the initial value to specify in the variable. 
    - It can use all constants and expressions supported by GOLDILOCKS except for multi-row functions.

<a id="0d3421e9f6565375"></a>
### Description

- The declared variable has the following features. 
    - It should be a unique name within a scope (PL block body).
    - A variable with the same name can be declared in a PL block body of nested subordinate.
    - It should be used in scope_name.variable_name form to correctly use the variables of duplicated declaration.
    - When using a variable of duplicated declaration without specifying the scope name, then a variable of the nearest scope is automatically used. 
- The declared variable is used in that scope and in its subordinate scope, but ':' is not added unlike an embedded SQL.
- The used variable is operated as a bind parameter (INOUT) for that SQL or a PSM control statement.

<a id="61ea8f172f6b8dc2"></a>
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

<a id="8198109e374036fc"></a>
### Compatibility

- The differences between &lt;declare scalar variable&gt; statement of GOLDILOCKS and that of SQL standard are as follows. 
    - &lt;SQL variable declaration&gt; of the SQL standard declares a variable in a PL block body (after BEGIN), but GOLDILOCKS declares a variable in a separate declaration section.
    - The SQL standard can declare multiple variables of the same type by using a single DECLARE statement, but GOLDILOCKS can declare only a single variable by using a single statement.
    - The SQL standard uses only DEFAULT syntax when setting the initial value, but GOLDILOCKS can use an assign sign (:=).

<a id="ce44bf92ad201603"></a>
## SELECT INTO Statement

<a id="6cb46570b2e4b517"></a>
### Function

A single row is returned through SELECT.

<a id="d1edf6e9afaeea3a"></a>
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

<a id="b23ceceb257c2721"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="7e547d2398291584"></a>
### Syntax Rules and Parameters

The rules are as same as those of a select statement except the rules for INTO clause.

<a id="5d75b5a3e4b09894"></a>
### Description

- SELECT INTO is used to return a single record. 
    - If the number of results is zero, "NO_DATA_FOUND" exception occurs. 
    - If the number of results are two or more, "TOO_MANY_ROWS" exception occurs. 
- The result can be returned through a record type variable of PSM. 
    - When using a record type variable, it can not be used being mixed with other type variables

<a id="bce2e5343c8da98a"></a>
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

<a id="d405637a226e1921"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="88e194880b00d785"></a>
## SQLCODE Function

<a id="90710125fbc35e27"></a>
### Function

It returns an error code of a statement which was performed just before in PSM.

<a id="546b044e4c11ca82"></a>
### Syntax

```
<SQLCODE function> ::= SQLCODE
```

<a id="aa10c3c8d2545cad"></a>
### Invocation and Access Rules

It can be used only within PSM.

<a id="3f6a2e0cbb966c0c"></a>
### Syntax Rules and Parameters

It does not have a separate argument.

<a id="0b82aa8f4ec8e91a"></a>
### Description

It returns an error code of a statement performed in PL/ SQL.  
A user-defined exception which does not assign an error code returns to 1 at the time when it is processed by a handler.   
When the error is completely processed by an exception handler, it returns to 0.

<a id="775c2afa1a061578"></a>
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

<a id="2dd93e6f41e8cc4e"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="95c19edfa7029573"></a>
## SQLERRM Function

<a id="5ee341faa461075a"></a>
### Function

It returns an error message of a statement which was performed just before in PSM.

<a id="9d4b61c440830fed"></a>
### Syntax

```
<SQLERRM function> ::= SQLERRM
```

<a id="a966b54b230143c2"></a>
### Invocation and Access Rules

It can be used only within PSM.

<a id="a81279fcb46f5664"></a>
### Syntax Rules and Parameters

It does not have a separate argument.

<a id="c4ada1c5e6bbb019"></a>
### Description

It returns an error message of a statement performed in PL/ SQL.  
A user-defined exception which does not assign an error code returns to a user-defined exception at the time when it is processed by a handler.   
When the error is completely processed by an exception handler, it outputs successful completion message.

<a id="863e6cff62b32f29"></a>
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

<a id="505beb8dc2b50d74"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="634cedf8214d979a"></a>
## %TYPE Attribute

<a id="ffd434f9bba098b3"></a>
### Function

When declaring a variable or defining a specific field of RECORD type, it defines the type as same as the column of a specific table or another variable.

<a id="a89198fea5b095a3"></a>
### Syntax

```
<type attribute> ::=
    <identifier chain> % TYPE
```

<a id="9d89bcb29e137392"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.  
It can be used only for &lt;data type&gt; section when declaring a variable or a field of a record type.

<a id="979ca51cebbc6938"></a>
### Syntax Rules and Parameters

- Identifier_chain
    - It is the name of a table column to be referenced or of the existing declared variable (or a field of the variable).

<a id="3ff23d4abc349605"></a>
### Description

<a id="e25e3c2cabdb917e"></a>
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

<a id="50c8bb2de16ef904"></a>
#### NOT NULL Constraints Variables References

It does not refer to the initial value when referring to NOT NULL attribute variable, so a new initial value should be specified.   
Setting an initial value of a field is not supported when using a type attribute for the field of a current record type variable, so NOT NULL type field can not be referenced.

<a id="ae269957e67d80bd"></a>
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

<a id="c52a5e2dc5238508"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="39a83aa49a584479"></a>
## UPDATE Statement Extension

<a id="b618a1f5e54a97c1"></a>
### Function

A feature altering a record by using a record type variable is added other than a feature consecutively listing the altering target columns of UNDATE statement in PSM.  
It stores the result by using a record type variable in UPDATE (searched) RETURNING INTO clause in PSM.

<a id="2301307bc25a843f"></a>
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

<a id="36631137ee6ffbae"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="bd235547516cc60c"></a>
### Syntax Rules and Parameters

- &lt;PSM_Variable&gt; to be used in UPDATE SET ROW syntax shoould be a variable declared as a record type.
- &lt;Variable&gt; to be used in UPDATE RETURNING INTO syntax does not need to be a record type.
    - However, if a record type is specified, then it can not be used being mixed with other data type variables nor can two or more record type variables be listed.

<a id="ddb118ece9fb102e"></a>
### Description

It alters the record or stores the result of RETURNING INTO through a record type variable in PSM.

<a id="f40fda5f1d9f3845"></a>
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

<a id="af441d7aef61b83c"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="34a1e3a9c8ec9595"></a>
## WHILE LOOP Statement

<a id="1e61712e1a6a6df8"></a>
### Function

It performs internal statements during &lt;search condition&gt; returns TRUE value.

<a id="9b538d1093a3888e"></a>
### Syntax

```
<while loop statement> ::=
    WHILE <search condition>
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="9f9e8bd587c0eb46"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="68f3f94f59db66d0"></a>
### Syntax Rules and Parameters

- Search conditions are as follows.
    - It is a conditional expression which continues to circle a while loop.
    - It should finally return a boolean type.

<a id="f194c1f3fb69ff92"></a>
### Description

while loop statement performs an internal statement list as long as the evaluation result of &lt;search condition&gt; is TRUE.

<a id="3b92deaa1b919d94"></a>
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

<a id="1dcd7821c81b2e19"></a>
### Compatibility

&lt;while loop statement&gt; statement is defined as &lt;while statement&gt; in the SQL standard.   
&lt;while statement&gt; of the SQL standard performs loop statement as DO ... END WHILE, but GOLDILOCKS performs it as LOOP ... END LOOP.

<a id="3cd1d247be6300a3"></a>
### For More Information

Refer to the followings.

- [CONTINUE Statement](#36b9610f45b5b1ab)
- [EXIT Statement](#720bf4f5443c1fb7)
- [GOTO Statement](#bf2dbc5e809bdc36)

---

[← 25. PSM Packages](25-psm-packages.md) · [Table of contents](../README.md) · [27. PSM SQL References →](27-psm-sql-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
