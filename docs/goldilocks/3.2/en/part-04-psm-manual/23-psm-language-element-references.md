<a id="40b1eaa6c8dd2508"></a>

# 23. PSM Language Element References

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/40b1eaa6c8dd2508)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 22. Using SQLs in PSM](22-using-sqls-in-psm.md) · [Table of contents](../README.md) · [24. PSM SQL References →](24-psm-sql-references.md)

<a id="1e25a441752ecddd"></a>
## Assignment Statement

<a id="152a974ef6a3abd3"></a>
### Function

Within a PSM block, it stores a value in a variable or in an out-bind parameter.

<a id="fdd3b564fb412378"></a>
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

<a id="4669be66e99aa97b"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="744d04f708707438"></a>
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

<a id="aced953481edfcff"></a>
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

<a id="7d866e5736bb7913"></a>
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

<a id="6c21b87c07a7f300"></a>
### Compatibility

The differences between an assignment statement of GOLDILOCKS and that of SQL standard are as follows.

- An assignment statement of the SQL standard defines a singleton variable assignment and a multiple variable assignment, but GOLDILOCKS supports only a singleton variable assignment. 
- An assignment statement of the SQL standard starts with SET keyword, but GOLDILOCKS does not use SET keyword. 
- An assignment statement of the SQL standard uses an equal operator (=) between a target and a value, but GOLDILOCKS uses :=.

**SQL standard compatibility**

<a id="3f99625cb8e6a846"></a>
<table><tbody><tr><th align="center">Feature ID</th><th align="center">Description</th><th align="center">Compatibility</th></tr><tr><td align="left">P002</td><td align="left">Computational completeness</td><td align="center">X</td></tr><tr><td align="left">P006</td><td align="left">Multiple assignment</td><td align="center">X</td></tr></tbody></table>

<a id="58d9967478a71eab"></a>
### For More Information

Refer to the followings.

- [Scalar Variable Declaration](#e161bee464ce9dec)
- [Record Variable Declaration](#ecb0da914795aa6a)
- [COLLECTION Variable Declaration](#183f1ba7cf5ec0be)
- [Cursor Variable Declaration](#6646917a8f23fc7a)

<a id="6b50d1aa237bd79e"></a>
## Basic LOOP Statement

<a id="6df466e1e44cd0da"></a>
### Function

It repeatedly performs statements within LOOP until the LOOP is terminated by performing GOTO or EXIT.

<a id="4a83abf242bdef0a"></a>
### Syntax

```
<basic loop statement> ::=
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="0701e595d736a639"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="13bbba54b1da4d00"></a>
### Syntax Rules and Parameters

- loop_name
    - It is the label name of &lt;basic loop statement&gt;. 
    - Its role is only a comment, so it does not matter even when it is different from the real label name of &lt;basic loop statement&gt;.

<a id="e2c4b4b2845ffc75"></a>
### Description

A basic loop statement is repeatedly performs statements within LOOP.  
A basic loop statement is a loop-family statement, so it can be a target statement which GOTO, EXIT, and CONTINUE indicates as a label.

<a id="239174415e0a3460"></a>
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

<a id="121d69fb2d462cca"></a>
### Compatibility

&lt;basic loop statement&gt; statement is as same as &lt;loop statement&gt; of the SQL standard.

**SQL standard compatibility**

<a id="21f1b74e28aaf6c4"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="72ead1f40a45eb30"></a>
### For More Information

Refer to the followings.

- [CONTINUE Statement](#faa14b048c02a9d8)
- [EXIT Statement](#a731ceab668854e0)
- [GOTO Statement](#af558f11d17a2a2a)

<a id="1fb0f1b90439c409"></a>
## Block (BEGIN .. END)

<a id="5efa6fb9d38d1855"></a>
### Function

It creates a new scope and defines a variable, a cursor, a type and an exception.

<a id="814e764247d1b0fe"></a>
### Syntax

```
<PSM block> ::=
    [ DECLARE <declare item>... ] BEGIN <SQL procedure statement list> END
    ;

<declare item> ::=
    <variable declaration>
    | <explicit cursor declaration>
    | <cursor variable declaration>
    | <type declaration>
    | <exception decalration>

<executable statement list> ::=
    [ <label list> ] { <SQL procedure statement> ; }...

<label list> ::=
    { << identifier >>  }...

<SQL procedure statement>
      <PSM Static SQL>
    | <PSM Dynamic SQL>
    | <PSM Control Statement>
```

<a id="d77561e7c4075b14"></a>
### Invocation and Access Rules

It can be used only within PROCEDURE, FUNCTION or an anonymous block.

<a id="3b77f7d8e9837bfc"></a>
### Syntax Rules and Parameters

- Variable declaration
    - It declares scalar/ record/ array type variables which are to be used in a block.
- Cursor variable declaration
    - It declares a cursor variable to be used in a block.
- Cursor declaration
    - It declares a cursor to be used in a block.
- Type declaration
    - It declares user defined types to be used when declaring a variable within a block.
- Exception declaration
    - It defines exceptions to be processed in an exception processing statement. 
- Static SQL
    - It indicates Data Manipulation Language (DML) and Data Control Language (DCL) which can be performed in PSM.
- Dynamic SQL
    - It indicates statements related to dynamic query processing supported by GOLDILOCKS PSM.
- PSM Control Statement
    - It indicates various flow control statements supported by GOLDILOCKS PSM.

<a id="993e63e3be9656e5"></a>
### Description

&lt;psm block&gt; is a basic component of PSM.  
A block can have a declaration part and a exception handling part.  
A block can be duplicated, and the duplicated block has a new subordinate variable scope. A superordinate block can not refer to a variable in a subordinate block.

<a id="8bc73fe833b6597f"></a>
### Examples

```
gSQL> <<MAIN>>
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

<a id="e4d0fd561997ef88"></a>
### Compatibility

&lt;compound statement&gt; of the SQL standard defines ATOMIC /NOT ATOMIC statement which specifies a new savepoint, but GOLDILOCKS does not support it.

**SQL standard compatibility**

<a id="c1d6e1edad2b54ab"></a>
| Feature ID | Description | Remarks |
| --- | --- | --- |
| P002 | Computational completeness | It does not support ATOMIC statement. |

<a id="130abfca464549d6"></a>
### For More Information

Refer to [Overview of PSM](17-overview-of-psm.md#c8a5addde6ef3dc8).

<a id="727ec69ff2109c7b"></a>
## CASE Statement

<a id="eb25e09a1ebc0a7b"></a>
### Function

It performs a statement list satisfying conditions which returns TRUE among given conditions.

<a id="a9080c7fb73542c0"></a>
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

<a id="6e4fe718f41c1b98"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="955d9db8f4a981d8"></a>
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

<a id="0f20195b18ede339"></a>
### Description

It performs statements in WHEN clause returning TRUE by evaluating conditions like as IF statement.  
It evaluates conditional expressions in order, and stops evaluating after finding the TRUE conditional clause.  
If the case satisfying the condition does not exist and ELSE clause is not specified, then an error occurs.

<a id="51a2a381ea038e78"></a>
### Examples

<a id="ec08afafa785c6e1"></a>
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

<a id="0434fc88b6d184c7"></a>
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

<a id="11307c73fd5a15b1"></a>
### Compatibility

CASE statement of the SQL standard defines the comparison of row type (list type) values, but GOLDILOCKS does not support it.  
CASE statement of the SQL standard can define multiple conditions in a list in &lt;when operand&gt; by delimiting them with ',', but GODILOCKS does not support it.

**SQL stantard compatibility**

<a id="cbc6e787ef0d1429"></a>
| Feature ID | Description | Remarks |
| --- | --- | --- |
| P002 | Computational completeness | It does not support P004, P008. |
| P004 | Extended CASE statement | - |
| P008 | Comma-separated predicates in simple CASE statement | - |

<a id="9a94c6cb1ad85bd0"></a>
## CLOSE Statement

<a id="ad191e7b807a1fb8"></a>
### Function

It closes an open cursor.

<a id="a216e19b9186c60d"></a>
### Syntax

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="129901c44a565fb0"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="a4673a4e4998da86"></a>
### Syntax Rules and Parameters

- cursor_name
    - It is the name of a cursor to be closed.

<a id="95e071bd88f595ca"></a>
### Description

It closes an open cursor.  
A closed cursor can be opened again by using an open statement.

<a id="65fb96f0a4429c2e"></a>
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

<a id="a4d4cbb02874380f"></a>
### Compatibility

The SQL standard does not define it.

<a id="048c9bfdcb073035"></a>
### For More Information

Refer to the followings.

- [FETCH Statement](#d0a634aca82150c3)
- [OPEN Statement](#808e637f278daebb)

<a id="1133f99827091ec0"></a>
## Collection Method Invocation

<a id="494b6a6853e2fad6"></a>
### Function

It provides a method which can explores a collection type variable.

<a id="60c652956425874a"></a>
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

<a id="1e2a130dec9275ba"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="0d905de200d3dbd0"></a>
### Syntax Rules and Parameters

- It can be used only in a variable declared as a collection type.
- FIRST, LAST, COUNT can not have a parameter.
- A parameter should be specified when an object should be specified such as PRIOR, NEXT, EXISTS, DELETE.
- DELETE is operated as same as PSM statement, and it can not return a different variable as a result. (It can not be used in an expression.)

<a id="e417e8e6a7b4b8ce"></a>
### Description

Refer to the following table.

**Function**

<a id="1e98b1a5f543e7a7"></a>
| Name | Function | Return value | Whether to  require an argument |
| --- | --- | --- | --- |
| FIRST | It returns the smallest key. | A key type specified in INDEX OF | X |
| LAST | It returns the biggest key. | A key type specified in INDEX OF | X |
| PRIOR | It returns a key smaller than the input key. | A key type specified in INDEX OF | O |
| NEXT | It returns a key bigger than the input key. | A key type specified in INDEX OF | O |
| COUNT | It returns the stored count. | INTEGER | X |
| DELETE | It deletes a value corresponding to a key. | N/A | O |
| EXISTS | It returns whether a key exists or not. | BOOLEAN | O |

<a id="54964fc8b7094bb3"></a>
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

<a id="d27f94ecb57fe757"></a>
### For More Information

Refer to [COLLECTION Variable Declaration](#183f1ba7cf5ec0be).

<a id="183f1ba7cf5ec0be"></a>
## COLLECTION Variable Declaration

<a id="7f4afe8472641555"></a>
### Function

It declares a collection variable.

<a id="6970cb9e7cffa50f"></a>
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

<a id="91ccc028e1a146e7"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="c782eb16bc7fad50"></a>
### Syntax Rules and Parameters

- Type-name
    - It specifies the name of a collection type to be used by a user.
- Element-type
    - It specifies the type of an element to be stored in a collection variable. 
- Index-type
    - It specifies the data type of a key stored in a collection variable.

<a id="87455348029442db"></a>
### Description

It declares a collection type.

<a id="4bde09ce43742f1f"></a>
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

<a id="5e17fca9df60de05"></a>
### Compatibility

The SQL standard does not define it.

<a id="5565183c41fa5ab8"></a>
### For More Information

Refer to [Collection Method Invocation](#1133f99827091ec0).

<a id="faa14b048c02a9d8"></a>
## CONTINUE Statement

<a id="f0990c7b66cbf5c8"></a>
### Function

It stops currently performing statement list, and performs the next iteration of a superordinate loop statement.

<a id="c8854ba7f6d17545"></a>
### Syntax

```
<continue statement> ::=
    CONTINUE [ label_name ] [ WHEN condition ] 
    ;
```

<a id="e4e51a98d8d64436"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

A statement with a target label should be one of the following loop family statements.  

• basic loop statement  
• for loop statement  
• while statement  
• forall statement

<a id="bcb1dba6491bbcd9"></a>
### Syntax Rules and Parameters

- Label name
    - It can have an identifier chain form.
- Condition
    - If it is specified, it returns to a loop statement only when the condition is TRUE.

<a id="87b5296ad9f70873"></a>
### Description

It stops currently performing statement list, and returns to the superordinate loop statement.

If a label is specified, it returns to the superordinate loop statement of the label name.  
If a label is not specified, it returns to the nearest superordinate loop statement.  
If multiple superordinate loop statements with the same names exist, then the nearest statement is selected.  
It can return to a loop statement (exist in a nested scope) which is visible in the current location.

If a condition is specified, then it returns only when the condition is TRUE.  
If a condition is not specified, then it definitely returns.

<a id="daf7d419f80151f1"></a>
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

<a id="b7ad412b06e30515"></a>
### Compatibility

&lt;continue statement&gt; statement is similar to &lt;iterate statement&gt; of the SQL standard.  
However, &lt;iterate statement&gt; statement does not provide WHEN condition feature.

<a id="2e0770ad907096f9"></a>
### For More Information

Refer to the followings.

- [EXIT Statement](#a731ceab668854e0)
- [GOTO Statement](#af558f11d17a2a2a)

<a id="120a4dd20d8ec2c6"></a>
## Cursor FOR LOOP Statement

<a id="89343d95cdc8a7a8"></a>
### Function

It performs loops as many times as the number of rows in the result created by a query or a cursor declared by a user in PSM.

<a id="b16da304305e30fd"></a>
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

<a id="daa5c60c6731dce6"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body of PSM.

<a id="c0d57d10a174e969"></a>
### Syntax Rules and Parameters

The variable declared within For~Loop is valid only within that loop scope. (The variable can not be referenced from outside of that Cursor For Loop Block Scope)

<a id="5cff822165cb0296"></a>
#### When Using Cursor Name

A cursor should already have been declared before performing LOOP by using a cursor name.   
For more information about an actual param, refer to [OPEN Statement](#808e637f278daebb).

<a id="e019a05e84dc7b1b"></a>
#### When Using Cursor Query

It can perform only the query which can be internally processed by using an implicit cursor in GOLDILOCKS such as a select and a returning query.

<a id="062a961865088cbe"></a>
### Description

It performs PSM statements within a loop by turning around loops as many time as the number of results created by a cursor.   
If a cursor becomes invalid (e.g. closed) during LOOP, it does not perform the loop and it processes itas an error.   
If an explicit cursor name is specified and the corresponding cursor is already opened, then it is processed as an error.

The variable to which a result of the cursor specified in FOR LOOP clause is returned is automatically created. (It is created as a row type of the result set to be returned by an execution result of a cursor.)   
However, if an alias for a select target expression which is not a column of a specific table among results of a user cursor query is not specified, then an error may occur.

<a id="81ce64235d596e95"></a>
### Examples

<a id="3f3e2d9a771ad2cd"></a>
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

<a id="f00d738adce705f8"></a>
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

<a id="ffd7efea11df90e3"></a>
### For More Information

Refer to the followings.

- [Explicit Cursor Declaration and Definition](#df6df449bca94eb7)
- [GOTO Statement](#af558f11d17a2a2a)
- [EXIT Statement](#a731ceab668854e0)

<a id="6646917a8f23fc7a"></a>
## Cursor Variable Declaration

<a id="304a726112f23bdc"></a>
### Function

It declares a cursor variable in DECLARE section of PSM.

<a id="324c2a8625c568bf"></a>
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

<a id="f7498af3ac322251"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of PSM.

<a id="f8c32dfafcab07a6"></a>
### Syntax Rules and Parameters

Specifying the initial value of a cursor variable or assigning a cursor variable is allowed only between cursor variables.

<a id="a9db97693182015c"></a>
### Description

A cursor variable is operated like as a pointer indicating a cursor which is not dependent on a specific cursor.

<a id="eb543bccde614684"></a>
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

<a id="7dc8e209f4d59d0a"></a>
### For More Information

Refer to the followings.

- [OPEN Statement](#808e637f278daebb)
- [FETCH Statement](#d0a634aca82150c3)
- [CLOSE Statement](#9a94c6cb1ad85bd0)

<a id="c15f9db57962191e"></a>
## DELETE Statement Extension

<a id="7ccbfe6626460d50"></a>
### Function

It can store the result in RETURNING INTO clause by using a record type variable of PSM.

<a id="d9d7998f0c1e9d3b"></a>
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

<a id="5bb5b1e7ad405f4c"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of PSM.

<a id="1c20bb16bed7f2c7"></a>
### Syntax Rules and Parameters

If a variable to be returned through RETURNING INTO is a record type, then it can not be used by mixing together with a different variable type.

<a id="8fde544c889653ff"></a>
### Description

It can store the result in RETURNING INTO clause by using a record type variable of PSM.

<a id="f9e5c4729b91d80c"></a>
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

<a id="ad1e20423ac88fd7"></a>
### For More Information

Refer to [Deleting Data](../part-03-sql-manual/12-sql-languages.md#913a00f7ba6f8e8b).

<a id="0efc00412525aa0d"></a>
## EXCEPTION_INIT Pragma

<a id="016dbb6223c493a8"></a>
### Function

It defines an internally defined exception within a PL block.

<a id="c36c3a17a9e98c25"></a>
### Syntax

```
< PRAGMA EXCEPTION_INIT > ::=
     PRAGMA EXCEPTION_INIT ( <Exception-Name>, <Internal-ErrorCode> ) 
     ;
```

<a id="a0ceb0658adbf3da"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of PSM.

<a id="70bfb771281548b3"></a>
### Syntax Rules and Parameters

A predefined exception can not be used in an exception name which is used as an argument. (A predefined exception name can not be declared.)   
An exception name which is used as an argument in the same PL block DECLARE clause should be declared in advance. (Declaration of an exception name in different BLOCK can not be referenced.)   
&lt;Internal-ErrorCode&gt; should be an internal error code existing within DB SYSTEM. (SUCCESS code can not be set.

<a id="c3ddbc141428b364"></a>
### Description

A user explicitly declares an exception name corresponding to an error code of DB SYSTEM.

<a id="282edea0c6a4e0da"></a>
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

<a id="dbb3280d692387cd"></a>
### Compatibility

Error codes are different each other according to a vendor, so it is not compatible each other.

<a id="c5cd7169f0fb38e4"></a>
### For More Information

Refer to the followings.

- [Exception Declaration](#ff6694cbaab4485d)
- [Exception Handler](#3bb0bb4e64d040ee)

<a id="ff6694cbaab4485d"></a>
## Exception Declaration

<a id="7a58c817f68a2141"></a>
### Function

It declares an exception name within a PL block.

<a id="12f9a0b4a8c9ae6d"></a>
### Syntax

```
< Exception-Declaration Statement > ::=
     <Exception-Name>  EXCEPTION 
     ;
```

<a id="05224ef1c51e62f9"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of PSM.

<a id="431d003ffb0eea9b"></a>
### Syntax Rules and Parameters

It can not declare a predefined exception name.   
Duplicated declarations are not allowed in DECLARE clause of the same SCOPE.

<a id="dcad2d66da8a7688"></a>
### Description

A user explicitly declares an exception.

<a id="268def1cff1b4043"></a>
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

<a id="4ba642ea38d87ea2"></a>
### Compatibility

An exception declaration of the standard SQL is as follows, but GOLDILOCKS supports the syntax as above.

```
<condition declaration> ::=
DECLARE <condition name> CONDITION [ FOR <sqlstate value> ]
```

<a id="625585020dda8d18"></a>
### For More Information

Refer to the followings.

- [Exception Declaration](#ff6694cbaab4485d)
- [EXCEPTION_INIT Pragma](#0efc00412525aa0d)

<a id="3bb0bb4e64d040ee"></a>
## Exception Handler

<a id="24fc96d02a272111"></a>
### Function

It performs an operation defined for an exception which is explicitly occurred by a user or an operation defined for an implicit error due to a DB SYSTEM error occurred during performing PL/ SQL.

<a id="2b54554b039a7ba0"></a>
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

<a id="289812899d149003"></a>
### Invocation and Access Rules

It can be used within a PL block.

<a id="10d00630ad9f100f"></a>
### Syntax Rules and Parameters

OTHERS (predefined exception) can not be specified together with another exception name by using OR.  
Duplicated specifying of OTHERS (predefined exception) is not allowed in an exception handler, and OTHERS should be specified at the last.

<a id="93335ae12a13d962"></a>
### Description

<a id="b458169584d43773"></a>
#### Exception Types

<a id="e1a75e9a76d5acfa"></a>
| Type | Definer | Has error | Has name | Raise implicitly | Raise explicitly |
| --- | --- | --- | --- | --- | --- |
| Predefined | System | Yes | Yes | Yes | Optionally |
| User-defined | User | If user assign | If user assign | No | Yes |

A predefined exception has an exception name and an error code which are specified in advance in GOLDILOCKS.  
Other exceptions are classified into an internally defined exception and a user-defined exception. An internally defined exception is that a user sets the internal error code name of GOLDILOCKS differently from a  predefined exception name, and a user-defined exception is that only the exception name is declared without specifying a separate error code.

<a id="85a7401f10e25e30"></a>
#### Predefined Exception

**Predefined exception type**

<a id="8a3235c3555b4074"></a>
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

<a id="9f3a26072aa51946"></a>
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

<a id="b17e2be30f3e1eb9"></a>
### Compatibility

It does not support the SQL standard grammar.

<a id="6e62b5082147fa6e"></a>
### For More Information

Refer to the followings.

- [EXCEPTION_INIT Pragma](#0efc00412525aa0d)
- [Exception Declaration](#ff6694cbaab4485d)

<a id="514a111028d257d2"></a>
## EXECUTE IMMEDIATE Statement

<a id="59a581c80ba77520"></a>
### Function

It executes a dynamic SQL within PSM.

<a id="2f5938af52e5a103"></a>
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

<a id="dbdc9bf125a6c8eb"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="c8f0d744f34c147c"></a>
### Syntax Rules and Parameters

<a id="ce09b8fdf293c659"></a>
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

<a id="279d4b460d80d9ad"></a>
#### INTO Clause

The result of performing a dynamic SQL exists, and it is not bound through a marker, but the result of processing an SQL statement is returned. (It is internally a form of an implicit cursor fetch.)   
The syntax is as follows.

```
EXECUTE IMMEDIATE 'SELECT ... FROM .. WHERE ...';
EXECUTE IMMEDIATE 'INSERT ... RETURNING ...';
EXECUTE IMMEDIATE 'UPDATE ... RETURNING ...';
EXECUTE IMMEDIATE 'DELETE ... RETURNING ...';
```

<a id="6882cee85a2ea40c"></a>
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

<a id="1ff6ac2e0c9e7d32"></a>
#### RETURNING Clause

If INSERT/UPDATE/DELETE RETURNING INTO statement is used as a dynamic SQL, the result is returned by binding a variable  specified in USING clause in OUT-mode in GOLDILOCKS.  
The same result can be returned by using RETURNING-INTO clause for the compatibility with other DBMS.

<a id="176e7ed6a4717f7a"></a>
#### Other Rules

- DDL/ DCL can not use any BIND clause. (INTO, USING, RETURNING clause)
- It is used as OUT in INTO clause and RETURNING INTO clause, so a separate bind type can not be specified nor it be simultaneously used together. 
- IN BIND type can use only a scalar type variable. 
- OUT BIND type can use a record type variable, but a scalar type or a record type can not be listed being mixed together.
- A result can not be returned being divided through INTO clause and USING OUT or RETURNING INTO.

<a id="3f2bd94ab1ec39f3"></a>
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

<a id="8a22b14903edb31c"></a>
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

<a id="a731ceab668854e0"></a>
## EXIT Statement

<a id="c888af259055811d"></a>
### Function

It exits a loop statement which has the given label among superordinate loop statements, then performs the next statement.

<a id="8fbeef9a7151bfdd"></a>
### Syntax

```
<exit statement> ::=
    EXIT [ label_name ] [ WHEN condition ]
    ;
```

<a id="25b6a5c989929b18"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="7dc6e2aeea3095fb"></a>
### Syntax Rules and Parameters

- Label name
    - It is a label name of a loop statement to be exited.
    - It can be in an identifier chain form.
- Condition
    - If a condition is specified, then it can exit a loop statement only when that condition is TRUE.

<a id="751ff412bada22b4"></a>
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

<a id="16291f001c401b88"></a>
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

<a id="07577c5599074df2"></a>
### Compatibility

It does not exist in the SQL standard.

<a id="ce56797facdcd3fc"></a>
## Explicit Cursor Attribute

<a id="87d80af3ba72f3a8"></a>
### Function

It returns the status value of a cursor defined in PSM.

<a id="5615c2c778a91241"></a>
### Syntax

```
<Explicit cursor attribute> ::=
    cursor_name '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="80a542e196ffe158"></a>
### Invocation and Access Rules

It can be used only in the body section of PSM.

<a id="1241bd976f579266"></a>
### Syntax Rules and Parameters

- Cursor_name
    - It is the name of a cursor whose status value is to be obtained.

<a id="c1acd811d14e35b4"></a>
### Description

- It returns the status value of a given cursor.
    - ISOPEN: It is whether the current cursor is OPEN.
    - FOUND: It is whether the data is returned by the recent fetch.
    - NOTFOUND: It is an opposite of FOUND.
    - ROWCOUNT: It is the number of fetched records after the cursor is recently OPEN.
- The following values are returned according to the cursor status.

**Results according to the performing moment**

<a id="42803d8f80a1c049"></a>
| Attribute name | Before OPEN | After OPEN | After FETCH | After CLOSE |
| --- | --- | --- | --- | --- |
| ISOPEN | FALSE | TRUE | TRUE | FALSE |
| FOUND | NULL | NULL | TRUE/FALSE | NULL |
| NOTFOUND | NULL | NULL | TRUE/FALSE | NULL |
| ROWCOUNT | NULL | NULL | N (the number) | NULL |

<a id="b30d1982d610e399"></a>
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

<a id="9d3d4ffb9f4b918e"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="df6df449bca94eb7"></a>
## Explicit Cursor Declaration and Definition

<a id="d7e609b73a2d2132"></a>
### Function

It declares a cursor in DECLARE section of PSM.

<a id="61e521d8d92a3974"></a>
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

<a id="cf893e9917ed4128"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="436bfd280a1ddd84"></a>
### Syntax Rules and Parameters

<a id="d1144a2c4a7d3438"></a>
#### Cursor Name

It is a cursor name to be declared.   
The length of a cursor name should be shorter than 128 bytes.  
It should be a unique name in that scope.

<a id="e28e95d93f8ef5e3"></a>
#### RowType

It defines a record type of a cursor.  
The number of select targets specified when defining a cursor should be same, and the data type should be compatible.  
If a rowtype is not specified, then a rowtype which is appropriate to a SELECT target of select_statement specified when defining a cursor is automatically specified.

<a id="fbc6ea5c07a5f030"></a>
#### Param Name

It is a name which distinguishes parameters within a specific cursor.  
It should be a unique name in that cursor.  
If the name is as same as a name of another variable which can be referenced within a scope, then a parameter of that cursor is preferentially referenced.

<a id="d85684b62a8918f0"></a>
#### DataType

It specifies the data type of the corresponding parameter.  
It can use all built-in types provided by GOLDILOCKS and types defined within PSM.  
However, a statement which restricts a scope (precision/ scale) can not be specified in a built-in type, but it is internally specified as the maximum scope of the corresponding data type.

<a id="c38245a9dcc146db"></a>
#### Select Statement

It specifies SELECT or SELECT ... FOR UPDATE statement which is to be performed by a cursor.  
It can not use SELECT ... INTO statement.

<a id="a6dddf88d4673988"></a>
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

<a id="46a3d51ec20f1927"></a>
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

<a id="9abe2808256aa4be"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="3105f1701e076a84"></a>
### For More Information

Refer to the followings.

- [OPEN FOR Statement](#68fe3a5ddf93af86)
- [FETCH Statement](#d0a634aca82150c3)
- [CLOSE Statement](#9a94c6cb1ad85bd0)

<a id="d0a634aca82150c3"></a>
## FETCH Statement

<a id="489e772d22c39ddf"></a>
### Function

It fetches a single record of OPEN cursor.

<a id="b4269e76268a8c9e"></a>
### Syntax

```
<fetch statement> ::=
    FETCH cursor_name <into clause>
    ;

<into clause> ::=
    INTO { variable [ , variable ] .. | record }
```

<a id="9e08b6b7b3c4d97c"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="f68c374898e56655"></a>
### Syntax Rules and Parameters

- Cursor name
    - It is a cursor name to be fetched.
- Variable
    - It is a scalar type variable or a bind parameter which stores a column value among the fetch results.
- Record
    - It is a record type variable to store the entire single record of which is the fetch result.

<a id="6aec1229f1abe338"></a>
### Description

It fetches a record from an open cursor, then copies the value to a variable specified in INTO clause.   
If a cursor is declared only but not defined, then an error occurs.  
The cursor should be open.

A variable type given to INTO clause should be compatible with a data type of the fetched record result.  
The number of variables given to INTO clause should be as same as the number of the cursor's SELECT targets.  
However, if a variable given in INTO clause is a record type, then only a single variable should be specified.  
Also, the number of the record variable fields should be as same as the number of SELECT targets.

If a fetch is called when a record to be fetched does not exist, then the value of target variables in INTO clause is not altered.

<a id="caddeb5460dc4a53"></a>
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

<a id="d41c413749ed6e62"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="c0c0b77de0396d2c"></a>
### For More Information

Refer to the followings.

- [OPEN Statement](#808e637f278daebb)
- [CLOSE Statement](#9a94c6cb1ad85bd0)

<a id="b5afa65ada57870e"></a>
## FOR LOOP Statement

<a id="1e8716e05bf71b44"></a>
### Function

As long as an index variable has the given value scope, it performs internal statements by increasing or reversing the index variable by 1.

<a id="2f268497211cda3d"></a>
### Syntax

```
<for loop statement> ::=
    FOR index_variable_name IN [ REVERSE ] start_value .. last_value
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="750d5989a1fc273e"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="d492cfd00391bd6f"></a>
### Syntax Rules and Parameters

- Index variable name
    - It is a variable name to be used as an index in FOR statement. Internally, NATIVE_BIGINT type variable is used.
- Start value
    - It is a start value of an index variable, and it should be an integer type. If a number with a floating point is used, then the number below decimal point is truncated while converting the type. 
- Last value
    - It is the last value of an index variable, and it should be an integer type. If a number with a floating point is used, then the number below decimal point is rounded down while converting the type.

<a id="b7b6a40c278cfc32"></a>
### Description

*for loop* statement performs an internal statement list by increasing or decreasing the index variable value from start_value to last_value.

If REVERSE is specified, an index variable value is decreased by 1 from start_value, and it terminates execution of *for loop* statement when the variable value becomes smaller than last_value.  
If REVERSE is not specified, an index variable is increased by 1 from start_value, and it terminates execution of *for loop* statement when the variable value becomes bigger than last_value.  
If start_value is bigger than last_value when REVERSE is not specified, or if start_value is smaller than last_value when REVERSE is specified, then an internal statement list is not performed.

<a id="e0658f6968ae6b8f"></a>
### Examples

```
gSQL> BEGIN
  FOR I IN 0 .. 10 LOOP
    DBMS_OUTPUT.PUT_LINE( 'I = ' || I );
  END LOOP;
END;
/
2 3 4 5 6 I = 0
I = 1
I = 2
I = 3
I = 4
I = 5
I = 6
I = 7
I = 8
I = 9
I = 10

Anonymous PL block executed.
```

<a id="a839a1a2202a314c"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="68f490c732ada1fd"></a>
### For More Information

Refer to the followings.

- [CONTINUE Statement](#faa14b048c02a9d8)
- [EXIT Statement](#a731ceab668854e0)
- [GOTO Statement](#af558f11d17a2a2a)

<a id="107b542ef38c3e58"></a>
## Function Declaration and Definition

<a id="a57bb9a70305458d"></a>
### Function

It defines a nested function.

<a id="2df10e412a857e77"></a>
### Syntax

```
<nested function statement> ::=
    FUNCTION func_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
        RETURN datatype
        { IS | AS } <item_declaration> BEGIN <pl_stmt_list> END
    ;
```

<a id="120a0f03d856539a"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="21e318e2455a7eec"></a>
### Syntax Rules and Parameters

<a id="57197209b8b89634"></a>
#### func_name

It is a name of function to be created, and it should be a unique name in a schema.  
The length of a function name should be shorter than 128 bytes.

<a id="532d6e35fd86f699"></a>
#### Param Name

It defines a name of an argument to be used in a function.  
The name of each argument should be unique in a function.

<a id="5ab2f0ff69196aa8"></a>
#### Bind Type

It specifies a bind type of each argument.  
If it is not specified, the default type is *IN*.

<a id="7e461f8590c60851"></a>
#### Item Declaration

It declares items such as a local variable to be used within a function.  
It can declare all items which can be declared in a PL block.

<a id="c3e67bbca320cc86"></a>
#### PL Stmt List

It is a body section of a function, and it lists PL statements to be performed.

<a id="fd5ff6834e3fb982"></a>
### Description

A nested function is a sub program which can be called only within the corresponding procedure.  
Other usages are as same as those of a schema-level function.

<a id="8d05d46c207fc91a"></a>
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

<a id="5fa802cf53fd62a1"></a>
### Compatibility

It is as same as a schema-level function.

<a id="7db1b97c98ef2a60"></a>
### For More Information

Refer to [CREATE FUNCTION](24-psm-sql-references.md#21b6c80060dfcc44).

<a id="af558f11d17a2a2a"></a>
## GOTO Statement

<a id="25ff2831c45d05ad"></a>
### Function

It tries to jump into the nearest statement which has a given label among statements accessible from the current location.

<a id="ba157208ea381cdb"></a>
### Syntax

```
<goto statement> ::=
    GOTO label_name
    ;
```

<a id="fa182d20794ddefe"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="b3cc202e38d5ea2a"></a>
### Syntax Rules and Parameters

- Label_name
    - It is a label name of a statement in which is to be jumped.
    - It can be in an identifier chain form.

<a id="a12387fe660ae7b8"></a>
### Description

It starts performing by jumping into a statement which has the corresponding label name.  
If multiple candidate statements exist, then it jumps into the nearest statement.  
It can jump only to a statement (exist in a nested scope) which is visible in the current location.  
Both forward jump and backward jump are possible.

<a id="1dae089858201f4b"></a>
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

<a id="f69891d3fa3c3860"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="d62290464da5e427"></a>
### For More Information

Refer to the followings.

- [EXIT Statement](#a731ceab668854e0)
- [CONTINUE Statement](#faa14b048c02a9d8)

<a id="e1ad89c3f3094655"></a>
## IF Statement

<a id="00cf749bba8bc5b7"></a>
### Function

It performs a statement list corresponding to the condition returning TRUE among the given conditions.

<a id="c8e52bf7fdbbfa69"></a>
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

<a id="b5fb16b95b3a94a4"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)   
It can be used only in the body section of a PL block.

<a id="15711c140bddaf49"></a>
### Syntax Rules and Parameters

- Search condition
    - It is an expression which can be finally evaluated as a boolean type.
- Executable statement list
    - It is a list of all statements supported by GOLDILOCKS PSM.

<a id="c3508b80a42171d2"></a>
### Description

Like as CASE statement, it performs statement lists of IF, ELSIF clauses returning TRUE by evaluating conditions.  
If it can not satisfy any condition and &lt;if statement else clause&gt; exists, then it performs the corresponding statement.   
ELSIF clauses evaluates conditional expressions in order, and stops evaluating after finding the TRUE conditional clause.

<a id="c9bec894a993d2a6"></a>
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

<a id="6221c0264c225f8b"></a>
### Compatibility

&lt;if statement&gt; statement is as same as a syntax and an operation of the SQL standard.

**SQL standard compatibility**

<a id="eb13ca33857b05c8"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="488615a3d957a5e5"></a>
## Implicit Cursor Attribute

<a id="bc5e2087b8fa9b12"></a>
### Function

It returns the status value of an implicit cursor defined in PSM.

<a id="ab9a648c0bb72d4a"></a>
### Syntax

```
<Implicit cursor attribute> ::=
    SQL '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="300823e13ed9f873"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="cd9d6d4e7e8b315e"></a>
### Description

- It stores the result of SQL statement which was executed just before. 
    - ISOPEN: It is whether the cursor is OPEN, and it is always set to FALSE.
    - FOUND: It is whether the data is returned by the SQL result of just before. 
    - NOTFOUND: It is an opposite of FOUND.
    - ROWCOUNT: It is the number of records affected by the SQL result of just before.

<a id="656298b7e047c5d5"></a>
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

<a id="8a1b62e18ec70abf"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="a4059a45edf8694e"></a>
## INSERT Statement Extension

<a id="5469eaeb95ebdec2"></a>
### Function

It is an extended feature of an insert statement to input data by specifying record type variable supported in PSM in VALUES clause.

<a id="d9ea8654cbdb4411"></a>
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

<a id="ee3078be8f427ad9"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.  
A PSM insert extension statement can not be used in an original SQL statement of EXECUTE IMMEDIATE.

<a id="c2b74fb290cba844"></a>
### Syntax Rules and Parameters

It is operated as same as the basic syntax of an insert statement. However, a feature specifying PSM record type variables are added other than a feature consecutively listing existing value expressions in parentheses in value item.

A PSM record type variable should be specified when using a variable without parentheses in Value_Item.   
When using it in an insert extension statement form, a variable which is not a record type can not be used being mixed.

<a id="f38812f347ab45f9"></a>
### Description

It stores a record by using a record type variable of PSM other than a general insert statement, or obtains a result through returning into.   
For more information about insert, refer to the following example.

<a id="2b0e3978c167e33a"></a>
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

<a id="2181aa154b121e87"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="a4d67d4521fb5529"></a>
## NULL Statement

<a id="0214bdee0968aaff"></a>
### Function

It is a statement without any feature.

<a id="8b10206c7a71432d"></a>
### Syntax

```
<null statement> ::=
    NULL
    ;
```

<a id="6088cfbfac2f1ab2"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="91c37f381cc0afbd"></a>
### Description

It is a statement without any feature, and used to set a label of a specific location.

<a id="14a44d8315c54cf0"></a>
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

<a id="fc1a7599b99c125b"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="808e637f278daebb"></a>
## OPEN Statement

<a id="120fa05fdddf5c4a"></a>
### Function

It executes SELECT statement of a cursor defined in PSM.

<a id="27054ad93988cc4f"></a>
### Syntax

```
<open statement> ::=
    OPEN cursor_name [ <actual param spec> ]
    ;

<actual param spec> ::=
      ( expression [ , expression ] .. )
```

<a id="00b7745e79a3e052"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="9a49172c11d33925"></a>
### Syntax Rules and Parameters

- Cursor_name
    - It is the name of a cursor to be opened.

<a id="9bf9bbbbb70c5e25"></a>
### Description

It executes SELECT or SELECT ... FOR UPDATE statement of a defined cursor.  
If a cursor is declared only but is not defined, then an error occurs.  
Values of actual parameters should be compatible with the data type of those parameters.

The number of actual parameters should be same as the number of parameters of a cursor.  
If it is smaller than the number of parameters of a cursor, then the default value should be specified in all other parameters.

<a id="34a3a352561e7ff5"></a>
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

<a id="0f2b6c27f054e6b7"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="f6b6364cbba64f3f"></a>
### For More Information

Refer to the followings.

- [CLOSE Statement](#9a94c6cb1ad85bd0)
- [FETCH Statement](#d0a634aca82150c3)

<a id="68fe3a5ddf93af86"></a>
## OPEN FOR Statement

<a id="34baa45603f858f6"></a>
### Function

It opens a single cursor by executing SELECT statement through a cursor variable defined in PSM.

<a id="f7e653d56c45b5f4"></a>
### Syntax

```
<open statement> ::=
    OPEN cursor_variable_name FOR <select_query>
    ;
```

<a id="1bc6316bc40b5b96"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="db7df8c2ecd0e00b"></a>
### Syntax Rules and Parameters

- Cursor_Variable_name
    - It is a name of cursor_variable.
- Select_query
    - A select query can use both a static SQL and a dynamic SQL.

<a id="d272449c80587808"></a>
### Description

It executes SELECT or SELECT ... FOR UPDATE statement of a defined cursor variable.  
If a cursor previously opened by a cursor variable exists, then that cursor is automatically closed.

<a id="a850fdb95829296e"></a>
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

<a id="a788b857296da0b8"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="d92d6c888297a3f9"></a>
### For More Information

Refer to the followings.

- [Cursor Variable Declaration](#6646917a8f23fc7a)
- [FETCH Statement](#d0a634aca82150c3)
- [CLOSE Statement](#9a94c6cb1ad85bd0)

<a id="4b18099f3667efac"></a>
## Procedure Call

<a id="c52febc6123cfb13"></a>
### Function

It calls a user-defined procedure, a built-in procedure or a nested procedure.

<a id="447b463ae29683c4"></a>
### Syntax

```
<Procedure call> ::=
    proc_name [ ( expr { , expr } ... ) ]
    ;
```

<a id="e008809f1b1c9b57"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

- The following privileges for the corresponding procedure are required to call the user-defined procedure. 
    - EXECUTE PROCEDURE
    - (EXECUTE PROCEDURE or CONTROL SCHEMA) ON SCHEMA for the schema to which the procedure belongs
    - EXECUTE ANY PROCEDURE ON DATABASE

<a id="edfc1b5c96259f60"></a>
### Syntax Rules and Parameters

- Proc_name
    - It is a name of a procedure to be executed, and it is used in the following format.

<a id="fa0b9d230849892a"></a>
<table class="table column_count_3"><caption></caption><thead><tr><th class="to_center"><div>Format</div></th><th class="to_center"><div>Syntax</div></th><th class="to_center"><div>Description</div></th></tr></thead><tbody><tr><td class="to_left to_middle"><div>Single identifier</div></td><td class="to_middle"><div>procedure_name</div></td><td><div>It calls the procedure of the given name.

It is searched in the following order.
1. nested procedure
2. schema-level procedure</div></td></tr><tr><td class="to_left to_middle" rowspan="3"><div>identifier chain</div></td><td><div>label_name.procedure_name</div></td><td><div>It calls a nested procedure.</div></td></tr><tr><td><div>schema_name.procedure_name</div></td><td><div>It calls a schema-level procedure.</div></td></tr><tr><td><div>package_name.procedure_name</div></td><td><div>It calls a built-in procedure.</div></td></tr></tbody></table>

If the given the number and type of arguments which were given in the procedure found first are wrong when searching with the given name (proc_name), then it does not search for another procedure but causes an error.

<a id="685faff95268eb0e"></a>
### Description

It calls a user-defined procedure, a built-in procedure or a nested procedure which was defined an advance.   
The argument value in which the default value is defined can be omitted when calling.

When using a procedure variable or bind parameter (?, :V1) in an argument which were defines as OUT or IN-OUT, then the returned value is obtained.

<a id="c85a34ce44ce07e9"></a>
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

<a id="b97835e2414f9409"></a>
### Compatibility

The SQL standard requires to use &lt;call statement&gt;.

<a id="80de2a6bc0ab0324"></a>
## Procedure Declaration and Definition

<a id="e7fa42e16988f340"></a>
### Function

It defines a nested procedure.

<a id="2d3e95c9ccefc942"></a>
### Syntax

```
<nested procedure statement> ::=
        PROCEDURE proc_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
        { IS | AS } <item_declaration> BEGIN <pl_stmt_list> END
    ;
```

<a id="f88ceb0b4c8d230d"></a>
### Invocation and Access Rules

It can be used in PSM declaration section.

<a id="697b0a0fb698aeb9"></a>
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

<a id="47777e60408fc702"></a>
### Description

A nested procedure is a sub program which can be called only within the corresponding procedure.  
Other usages are as same as those of a schema-level procedure.

<a id="324243e756b557a5"></a>
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

<a id="62e6e352e5d76838"></a>
### Compatibility

It is as same as a schema-level procedure.

<a id="0614ce75efba4573"></a>
### For More Information

Refer to [CREATE PROCEDURE](24-psm-sql-references.md#730491b1fd9dfcc3).

<a id="9e9b63bee16d55b7"></a>
## RAISE Statement

<a id="f578c12a213ab667"></a>
### Function

It explicitly generates a user-defined exception.

<a id="78bf3d674a820e97"></a>
### Syntax

```
<RAISE Statement> ::= 
    RAISE  <Exception-Name>
    ;
```

<a id="1bc05dc81c08b503"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="e72b6df9f4751c9d"></a>
### Syntax Rules and Parameters

- A name of exception to be raised should be declared in a PL block to which a raise belongs or in DECLARE clause of a superordinate PL block. However, a predefined exception can be raised without a declaration.
- If a raise statement is used within an exception handler, an exception name can be omitted, in this case, the previous exception is spread to the superordinate block.

<a id="ef6c7ec4654901db"></a>
### Description

If it can not be processed in a PL block in which an exception occured, then it is spread to the superordinate PL block.  
If an exception to be raised does not exist in a PL block including RAISE statement, nor does exist in all exception handlers within a superordinate PL block, then an error occurs.  
It is spread from a PL block in which RAISE exception occurred to a superordinate PL block until it is processed, and it can not be spread to an exception handler of subordinate PL block.

**Propagating user exception**

<a id="3882dd2c0c03ed24"></a>
| Raise exception | Exception  handler  SCOPE | Exception  handler | Whether to spread it  to superordinate |
| --- | --- | --- | --- |
| User exception without error code | Same scope | X | It spreads "unhandled exception" error to a superordinate scope. |
| User exception with error code | Superordinate scope | X | It spreads a user exception. |
| User exception with error code | Same scope | X | Itspreads a user defined error code. |
| User exception with error code | Superordinate scope | X | Itspreads a user defined error code. |

<a id="19ee17f143b51708"></a>
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

<a id="5bb835bf4bc40983"></a>
### Compatibility

The SQL standard specifies &lt;handler declaration&gt; and &lt;condition declaration&gt;, but it does not support the syntax.

<a id="f5b5c8ec06d8e902"></a>
### For More Information

Refer to the followings.

- [Exception Handler](#3bb0bb4e64d040ee)
- [Exception Declaration](#ff6694cbaab4485d)

<a id="ecb0da914795aa6a"></a>
## Record Variable Declaration

<a id="ed03aa352b45fd63"></a>
### Function

It declares a record type variable in DECLARE section.

<a id="3c7fdc4284361f61"></a>
### Syntax

```
<declare record variable> ::=
    variable_name <recordType> 
    ;

<recordType> ::=
     <tableName>%ROWTYPE
   | USER_DEFINED_DATA_TYPE
```

<a id="8a9da3171b086634"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="8e9b6ab72179d574"></a>
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
    - For more information about the declaration of recordType, refer to [User Defined Record Type](18-psm-datatypes.md#a7fe2678730e2a7f).

<a id="9c8ead80c9d7f9b4"></a>
### Description

- The declared variable has the following features. 
    - It should be a unique name within a scope (PL block body).
    - A variable with the same name can be declared in a PL block body of nested subordinate.
    - It should be used in scope_name.variable_name form to correctly use the variables of duplicated declaration.
    - When using a variable of duplicated declaration without specifying the scope name, then a variable of the nearest scope is automatically used. 
- The declared variable is used in that scope and in its subordinate scope, but ':' is not added unlike an embedded SQL.
- The used variable is operated as a bind parameter (INOUT) for that SQL or a PSM control statement.

<a id="b44edc1823ba152e"></a>
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

<a id="979655eaf860758a"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="45271719d4bbd1f6"></a>
## RETURN Statement

<a id="2620d7919bf64df2"></a>
### Function

It specifies the value of which a function returns, then terminates the function. A procedure does not specify the return value, but terminates the procedure.

<a id="278970ffd432afd2"></a>
### Syntax

```
<return statement> ::=
    RETURN [ return_value_expr ]
    ;
```

<a id="7f1cd2b5e6455d59"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="772facba9309b5e3"></a>
### Syntax Rules and Parameters

- Return_value_expr
    - It is an expression of a value to be returned, and it can be specified only when it is a function.

<a id="6097e7156df79c32"></a>
### Description

It terminates a currently performing procedure/ function.  
For a function, if RETURN statement is terminated without being performed, or if RETURN statement does not have return_value_expr, then an error occurs.

<a id="a8388903f3ef3e72"></a>
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

<a id="1f9936889509b6f9"></a>
### Compatibility

It is specified in the SQL standard, but conformance rules do not exist.

<a id="4a01bc7bf9cbffb4"></a>
## RETURNING INTO clause

<a id="64438e06ef8223f3"></a>
### Function

The data processed in an insert/ update/ delete is returned to a PSM variable.

<a id="553ae972d8605d4c"></a>
### Syntax

```
<Insert, Delete Returning_into_clause> ::=
      [ RETURN | RETURNING ] { * | { <value_expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]

<Update returning into clause> ::=
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] } INTO Variable [, ...]
```

<a id="612c9f813b7babf6"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="5c5dda862136869d"></a>
### Syntax Rules and Parameters

A record type variable can not be used being mixed with other types.

<a id="e240823a16786848"></a>
### Description

It stores before/ after record of processing an insert/ update/ delete statement through returning into.

<a id="b0e9edadd842c656"></a>
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

<a id="b201ea7f13c631cd"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="181edde49e8c3cba"></a>
## %ROWTYPE Attribute

<a id="557dce09c37b0288"></a>
### Function

When declaring a variable, it defines the structure and type as same as those of a specific table, a specific cursor or a result set of a cursor variable.

<a id="d4d1d358cae72f9c"></a>
### Syntax

```
<rowtype attribute> ::=
    <identifier chain> % ROWTYPE
```

<a id="1eb2f13718faeaf6"></a>
### Invocation and Access Rules

- It can be used only within PSM. (e.g. package, procedure, function)
- It can be used only in the declaration section of a PL block.
- When declaring a variable, it can be used only in &lt;data type&gt; section.
- When declaring a record type field, then it can not be used in &lt;data type&gt; section. (It does not support complex data type.)

<a id="1c2eeb5a5e1cd5b7"></a>
### Syntax Rules and Parameters

- Identifier chains are as follows.
    - The name of table, view, synonym to be referenced, or the name of a cursor or a cursor variable

<a id="a7d239fe4cacd312"></a>
### Description

- Search order of the reference targets 
    - Cursor or cursor variable 
    - Base table, view, or synonym

- Reference scope 
    - When referring by using a row attribute, only name and type of columns in a result set of a table or a cursor is referenced.
    - Therefore, it does not refer to NOT NULL constraint or DEFAULT value settings.

<a id="7eb7afc03e20857f"></a>
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

<a id="9957b79ae927ffe8"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="e161bee464ce9dec"></a>
## Scalar Variable Declaration

<a id="6340d2c232275faa"></a>
### Function

It declares a scalar variable in the declaration section.

<a id="e16b42715c3de04d"></a>
### Syntax

```
<declare scalar variable> ::=
    variable_name <data type> [ <variable initialize clause> ]
    ;

<variable initialize clause> ::=
      [ NOT NULL ] { DEFAULT | := } <value expression>
```

<a id="ee249c68ed7a85c5"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.

<a id="47ed5f05f2a11c20"></a>
### Syntax Rules and Parameters

- Variable_name
    - It is a name of variable to be declared.
    - The length of the variable name should be shorter than 128 bytes.
    - It should be a unique name within a scope (PL block body).
    - A variable with the same name can be declared in a PL block body of nested subordinate.
    - It should be used in scope_name.variable_name form to correctly use the variables of duplicated declaration.
    - When using a variable of duplicated declaration without specifying the scope name, then a variable of the nearest scope is automatically used. 
- Data_Type
    - It can use all built-in [Data Type](../part-03-sql-manual/11-sql-elements.md#9ebaf6ccb06f475d) provided in GOLDILOCKS.
- Value_expression
    - It expresses the initial value to specify in the variable. 
    - It can use all constants and expressions supported by GOLDILOCKS except for multi-row functions.

<a id="6c7e4719a24eeef5"></a>
### Description

- The declared variable has the following features. 
    - It should be a unique name within a scope (PL block body).
    - A variable with the same name can be declared in a PL block body of nested subordinate.
    - It should be used in scope_name.variable_name form to correctly use the variables of duplicated declaration.
    - When using a variable of duplicated declaration without specifying the scope name, then a variable of the nearest scope is automatically used. 
- The declared variable is used in that scope and in its subordinate scope, but ':' is not added unlike an embedded SQL.
- The used variable is operated as a bind parameter (INOUT) for that SQL or a PSM control statement.

<a id="464861de418b507f"></a>
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

<a id="2cd84a6bf744e64a"></a>
### Compatibility

- The differences between &lt;declare scalar variable&gt; statement of GOLDILOCKS and that of SQL standard are as follows. 
    - &lt;SQL variable declaration&gt; of the SQL standard declares a variable in a PL block body (after BEGIN), but GOLDILOCKS declares a variable in a separate declaration section.
    - The SQL standard can declare multiple variables of the same type by using a single DECLARE statement, but GOLDILOCKS can declare only a single variable by using a single statement.
    - The SQL standard uses only DEFAULT syntax when setting the initial value, but GOLDILOCKS can use an assign sign (:=).

<a id="60a897b6bb05acd9"></a>
## SELECT INTO Statement

<a id="9ac080d469c55134"></a>
### Function

A single row is returned through SELECT.

<a id="58d8d362e7c0c30f"></a>
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

<a id="742893d8a2495fc9"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="e5a5251a343db576"></a>
### Syntax Rules and Parameters

The rules are as same as those of a select statement except the rules for INTO clause.

<a id="033b4f30257adb33"></a>
### Description

- SELECT INTO is used to return a single record. 
    - If the number of results is zero, "NO_DATA_FOUND" exception occurs. 
    - If the number of results are two or more, "TOO_MANY_ROWS" exception occurs. 
- The result can be returned through a record type variable of PSM. 
    - When using a record type variable, it can not be used being mixed with other type variables

<a id="9fc00a98658e0179"></a>
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

<a id="25b3e0251a582049"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="8eeb557805b4b907"></a>
## SQLCODE Function

<a id="3f56b0e96ff5145b"></a>
### Function

It returns an error code of a statement which was performed just before in PSM.

<a id="05e2b6e9575f5c69"></a>
### Syntax

```
<SQLCODE function> ::= SQLCODE
```

<a id="1d678535b14fbe83"></a>
### Invocation and Access Rules

It can be used only within PSM.

<a id="71a3d44c9019d41d"></a>
### Syntax Rules and Parameters

It does not have a separate argument.

<a id="246f6a886f043838"></a>
### Description

It returns an error code of a statement performed in PL/ SQL.  
A user-defined exception which does not assign an error code returns to 1 at the time when it is processed by a handler.   
When the error is completely processed by an exception handler, it returns to 0.

<a id="4ba82681a3bd9e6b"></a>
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

<a id="d3bc14a0dc25e7a8"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="b5843de956f7afb7"></a>
## SQLERRM Function

<a id="5d5a4fea3305632c"></a>
### Function

It returns an error message of a statement which was performed just before in PSM.

<a id="0ab95d9e2d3689ec"></a>
### Syntax

```
<SQLERRM function> ::= SQLERRM
```

<a id="72ba9713146a615a"></a>
### Invocation and Access Rules

It can be used only within PSM.

<a id="53f4f3de579a678e"></a>
### Syntax Rules and Parameters

It does not have a separate argument.

<a id="b36a14bbcdde5ce1"></a>
### Description

It returns an error message of a statement performed in PL/ SQL.  
A user-defined exception which does not assign an error code returns to a user-defined exception at the time when it is processed by a handler.   
When the error is completely processed by an exception handler, it outputs successful completion message.

<a id="3ffcb4e171880fc8"></a>
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

<a id="537faf1c401f05e5"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="201856225882202d"></a>
## %TYPE Attribute

<a id="2d184ca9796f4913"></a>
### Function

When declaring a variable or defining a specific field of RECORD type, it defines the type as same as the column of a specific table or another variable.

<a id="72daeca9139b658d"></a>
### Syntax

```
<type attribute> ::=
    <identifier chain> % TYPE
```

<a id="77e6cecb528a26ac"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the declaration section of a PL block.  
It can be used only for &lt;data type&gt; section when declaring a variable or a field of a record type.

<a id="cd67eaa2ca896eb7"></a>
### Syntax Rules and Parameters

- Identifier_chain
    - It is the name of a table column to be referenced or of the existing declared variable (or a field of the variable).

<a id="dffa7a00b8fa385c"></a>
### Description

<a id="30a80b38514cc72b"></a>
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

<a id="8130a088ace0c533"></a>
#### NOT NULL Constraints Variables References

It does not refer to the initial value when referring to NOT NULL attribute variable, so a new initial value should be specified.   
Setting an initial value of a field is not supported when using a type attribute for the field of a current record type variable, so NOT NULL type field can not be referenced.

<a id="f38f2fde50aa7aa8"></a>
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

<a id="652f3b166e754275"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="74a0364cfe45d490"></a>
## UPDATE Statement Extension

<a id="589b964b30a2cbfc"></a>
### Function

A feature altering a record by using a record type variable is added other than a feature consecutively listing the altering target columns of UNDATE statement in PSM.  
It stores the result by using a record type variable in UPDATE (searched) RETURNING INTO clause in PSM.

<a id="d5c706adcd104d0c"></a>
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

<a id="64ffd66b8da62d09"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="a443b1012664aaca"></a>
### Syntax Rules and Parameters

- &lt;PSM_Variable&gt; to be used in UPDATE SET ROW syntax shoould be a variable declared as a record type.
- &lt;Variable&gt; to be used in UPDATE RETURNING INTO syntax does not need to be a record type.
    - However, if a record type is specified, then it can not be used being mixed with other data type variables nor can two or more record type variables be listed.

<a id="95db405d5e776a8c"></a>
### Description

It alters the record or stores the result of RETURNING INTO through a record type variable in PSM.

<a id="5f8d6d60dbcd6c75"></a>
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

<a id="926e840317b6e703"></a>
### Compatibility

It is not defined in the SQL standard.

<a id="29967ced3a732acb"></a>
## WHILE LOOP Statement

<a id="df263107e17fea05"></a>
### Function

It performs internal statements during &lt;search condition&gt; returns TRUE value.

<a id="71b950006dbf3216"></a>
### Syntax

```
<while loop statement> ::=
    WHILE <search condition>
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="b463a77f7eea475f"></a>
### Invocation and Access Rules

It can be used only within PSM. (e.g. package, procedure, function)  
It can be used only in the body section of a PL block.

<a id="c74e4f9cd99730de"></a>
### Syntax Rules and Parameters

- Search conditions are as follows.
    - It is a conditional expression which continues to circle a while loop.
    - It should finally return a boolean type.

<a id="98d35209498ed6e2"></a>
### Description

while loop statement performs an internal statement list as long as the evaluation result of &lt;search condition&gt; is TRUE.

<a id="38d1867e479b78d9"></a>
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

<a id="9d294a602e275521"></a>
### Compatibility

&lt;while loop statement&gt; statement is defined as &lt;while statement&gt; in the SQL standard.   
&lt;while statement&gt; of the SQL standard performs loop statement as DO ... END WHILE, but GOLDILOCKS performs it as LOOP ... END LOOP.

<a id="2b866784aa636b06"></a>
### For More Information

Refer to the followings.

- [CONTINUE Statement](#faa14b048c02a9d8)
- [EXIT Statement](#a731ceab668854e0)
- [GOTO Statement](#af558f11d17a2a2a)

---

[← 22. Using SQLs in PSM](22-using-sqls-in-psm.md) · [Table of contents](../README.md) · [24. PSM SQL References →](24-psm-sql-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
