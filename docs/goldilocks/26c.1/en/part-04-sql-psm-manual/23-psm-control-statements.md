<a id="ef5980dd9dd05ba7"></a>

# 23. PSM Control Statements

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/ef5980dd9dd05ba7)  
> Tag: `26c.1_0_tag`

[← 22. PSM DataTypes](22-psm-datatypes.md) · [Table of contents](../README.md) · [24. PSM Cursor Statements →](24-psm-cursor-statements.md)

<a id="56a4b551cb2918ec"></a>
## Assignment

It inserts the calculation value of the right expression into the left variable by using assignment operators (':=').

<a id="0f372ee1d1fdb02f"></a>
### Assignment Target

An assignment target is on the left side of the assignment operator, and the following items may exist on it.

- Variables (Including an argument of a procedure or a function except for IN type)
- Bind parameter such as '?' or ':V1' (It can be used only in an anonymous PL block.)

<a id="8ebaf5e9d161fd8b"></a>
### Assigning Expression

An expression available on PSM is on the right side of the assignment operator. Expressions available on a PSM expression is as follows.

- Constant
- All operators, built-in functions or pseudo columns provided by GOLDILOCKS SQL
- Bind parameter bound to IN or IN OUT type (It can be used only in an anonymous PL block.)
- PSM variable
- PSM nested function
- Schema-level function

The following is an example of assignment statement per each type.

```
CREATE OR REPLACE FUNCTION ADD_TEN( A1 INTEGER )
RETURN INTEGER
IS
BEGIN
  RETURN A1 + 10;
END;
/
COMMIT;

DECLARE
  FUNCTION ADD_ONE( A1 INTEGER )
  RETURN INTEGER
  IS
  BEGIN
    RETURN A1 + 1;
  END;
  V_NUM INTEGER;
  V_STR VARCHAR(10);
BEGIN
  V_NUM := 10;                  ❶ Numeric literal
  V_STR := 'ABC';               ❷ String literal
  :V_PARAM := V_STR || 'DEF';   ❸ PSM variable, SQL operator 
  V_NUM := ADD_ONE( 100 ) + ADD_TEN( 1000 );  
                                ❹ Nested function, Schema-level function
END;
/
```

The following expressions can not be used in an PSM expression.

- Column of a table, view or the corresponding object
- SQL objects such as an index, a sequence or a synonym
- Subquery
- Nested procedure
- Schema-level procedure

The following is an example of an error due to a wrong expression.

```
gSQL> CREATE SEQUENCE SEQ1;

Sequence created.

gSQL> COMMIT;

Commit complete.

gSQL> DECLARE
  V1 INTEGER;
BEGIN
  V1 := SEQ1.NEXTVAL;
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (4:9): ERR-42000(16074): sequence number not allowed here
```

To assign an object value of a type which is not available in an PSM expression, use SELECT INTO statement as follows.

```
gSQL> DECLARE
  V1 INTEGER;
BEGIN
  SELECT SEQ1.NEXTVAL INTO V1 FROM DUAL;
END;
/

Anonymous PL block executed.
```

<a id="ddd7db173c33ff01"></a>
### Assignment Compatibility

Even though the statement can use an expression of an assignment statement, it may succeed or fail depending on a target type and the final result type of an expression. The available expression types according to a target type is as follows.

**Assignment compatibility**

<a id="c81247f22e91736d"></a>
| Target type | Final result type of an expression |
| --- | --- |
| Scalar type * Scalar type variable  * A specific field of a record type variable * Scalar element of a collection variable with a key value | It is allowed only when it is a scalar type with a value conversible to a target type. |
| Attribute record type (%ROWTYPE) | It is allowed only when the number of fields are same and each field value is conversible to the field of the corresponding order of a target. |
| User defined record type | Only the exactly same type is allowed. |
| Collection type * Collection type variable whose key value is not specified | Only the exactly same type is allowed. |

Even though the internal structures of user defined record type variables are same, an error occurs if the type names are different.

```
gSQL> DECLARE
  TYPE MY_REC1 IS RECORD ( F1 INTEGER := 1, F2 VARCHAR(10) := 'AAA' );
  TYPE MY_REC2 IS RECORD ( F1 INTEGER := 1, F2 VARCHAR(10) := 'AAA' );
  V1 MY_REC1;
  V2 MY_REC2;
BEGIN
  V2 := V1; 
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (7:9): ERR-HY000(17007): invalid expression
```

Moreover, if a target is an argument variable defined with IN attribute or is a bind parameter bound with IN attribute, an error occurs.

```
gSQL> DECLARE
  FUNCTION ADD_ONE( A1 IN INTEGER )
  RETURN INTEGER
  IS
  BEGIN
    A1 := A1 + 1;
    RETURN A1;
  END;
  V1 INTEGER;
BEGIN
  V1 := ADD_ONE( 10 );
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (6:5): ERR-HY000(17024): (A1) cannot be used as assignment target
```

Assignment compatibility rules are applied same even when assigning the value of an actual parameter to a formal parameter variable while calling a function or a procedure.

<a id="e32e3ee0978f51e4"></a>
## PL Block

A PL block is a basic unit which configures PSM. A PL block can be nested again in another PL block. Items declared within a PL block can be referenced only within the range of its own block (Including subordinate blocks)

<a id="8ddecb36987d62ca"></a>
### PL Block Configuration

A single PL block is divided into the following three parts.   
For more information, refer to [Block (BEGIN .. END)](30-psm-language-element-references.md#acfcdb439eaed2a5).

```
[DECLARE  
❶ Declarative part]
BEGIN 
❷ Statements 
[EXCEPTION
❸ Handlers]
END;
```

<a id="398839cad09efa49"></a>
#### Declarative Part

A declarative part is an area in which a local item to be used within a PL block is declared. If an item such as a local variable to be declared does not exist, then a declarative part is not defined, but it starts from an executable part.

Local items to be declared in a declarative part is as follows.

- Variable (Refer to [PSM DataTypes](22-psm-datatypes.md#2fe90d5805cc1b9e).)
- User defined type
- Cursor
- Nested function or a procedure (Subprogram)
- User defined exception

All names of items declared in a single PL block should be unique regardless of their types. For example, a cursor whose name is the same as a name of a variable can not be declared.

```
gSQL> DECLARE
  C1 INTEGER;
  CURSOR C1 IS SELECT * FROM DUAL;
BEGIN
  OPEN C1;
  FETCH C1 INTO C1;
  CLOSE C1;
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (3:10): ERR-HY000(17027): duplicated identifier
(2) at (5:8): ERR-HY000(17031): mismatch identifier type
(3) at (6:9): ERR-HY000(17031): mismatch identifier type
(4) at (7:9): ERR-HY000(17031): mismatch identifier type
```

However, an item in a subordinate PL block whose name is the same as an item in a superordinate PL block can be declared. In this case, that name means the item found first when exploring from the current location toward the superordinate block.

```
gSQL> <<PP>>
DECLARE    ❶ Parent scope begin
  V1 VARCHAR(10) := 'AAA';
BEGIN
  <<CC>>
  DECLARE  ❷ Child scope begin
    V1 INTEGER := 99;
  BEGIN
    DBMS_OUTPUT.PUT_LINE( 'PP.V1 = ' || PP.V1 ); 
    DBMS_OUTPUT.PUT_LINE( 'CC.V1 = ' || CC.V1 ); 
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 ); 
  END;     ❸ Child scope end
END;       ❹ Parent scope end
/

PP.V1 = AAA
CC.V1 = 99
V1 = 99

Anonymous PL block executed.
```

<a id="145cd0e095c37b2b"></a>
#### Executable Part

In an executable part, a declared items are manipulated and included statements are performed. Statements available in an executable parts are as follows.

- Control Statements (Refer to [PSM Control Statements](#ef5980dd9dd05ba7).)
- Cursor Statements (Refer to [PSM Cursor Statements](24-psm-cursor-statements.md#cca8ab23b64c44dd).)
- SQL Statements (static/ dynamic) (Refer to [Using SQLs In PSM](26-using-sqls-in-psm.md#64082b0803f1502a).)

<a id="141d123bb302ff56"></a>
#### Exception Handling Part

It defines handlers which handles multiple exceptions occurring during the execution.

If an exception occurs during executing several statements in an executable part, then it explores from the location of that PL block to the superordinate PL block to find out whether a handler is registered to handle the exception. If there is the handler, then it performs the contents of that handle, then initializes that exceptional situation.

```
DECLARE
  V1 INTEGER;
BEGIN
  SELECT C1 INTO V1 FROM T1 WHERE C1 = 100;
EXCEPTION 
  WHEN NO_DATA_FOUND THEN
    DBMS_OUTPUT.PUT_LINE('SQL%ISOPEN   = ' || SQL%ISOPEN);
    DBMS_OUTPUT.PUT_LINE('SQL%FOUND    = ' || SQL%FOUND);
    DBMS_OUTPUT.PUT_LINE('SQL%NOTFOUND = ' || SQL%NOTFOUND);
    DBMS_OUTPUT.PUT_LINE('SQL%ROWCOUNT = ' || SQL%ROWCOUNT);
END;
/
```

If an appropriate handler is not found even after exploring to the top-level PL block, then the occurred exception is returned to a caller, and it is terminated.

```
gSQL> DECLARE
  v1 INTEGER;
BEGIN
  v1 := 1/ 0;
END;
/

ERR-HY000(17007): invalid expression : 
  v1 := 1/ 0;
        *
ERROR at line 4:
ERR-22012(12122): divisor is equal to zero
```

For more information about declaration of user defined exception, built-in handler types or installing a handler, refer to [Error Handling](#49dd8ff2244279ba).

<a id="f04dadf601b2cd74"></a>
## NULL Statement

It is used to specify a statement which does not have any role in PSM such as no-op.  
For more information, refer to [NULL Statement](30-psm-language-element-references.md#96d51677cf5459a5).

```
DECLARE
  V1 INTEGER := 1;
BEGIN
  IF V1 < 10 THEN
    V1 := V1 + 1;
  ELSE
    NULL;  -- do nothing
  END IF;
END;
/
```

<a id="c74259cd0e8138c8"></a>
## Testing Conditions

Conditional branch statements perform statements according to true/false of the given condition. GOLDILOCKS PSM provides two conditional branch statements, which are IF and CASE.

<a id="5aa2abf5f3b2ba1f"></a>
### IF

IF statement performs statements which are true among conditions of the given expression. Conditions of an expression can be specified next to IF and ELSIF. If the condition of an expression is true when checking conditions in an order specified when performing, then it performs the statements below THEN clause. If all IF conditions and ELSIF conditions are false, and ELSE clause is specified, then it performs the statements below ELSE clause.

IF statement always ends with END IF keyword.  
For more information, refer to [IF Statement](30-psm-language-element-references.md#8d14b69600360332).

```
DECLARE
V1 INTEGER := 1;
BEGIN
  -- IF COND
  IF V1 > 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'IF COND' );
  ELSIF V1 = 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'ELSIF COND' );
  ELSE
    DBMS_OUTPUT.PUT_LINE( 'ELSE COND' );
  END IF; 

  -- ELSIF COND
  IF V1 = 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'IF COND' );
  ELSIF V1 > 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'ELSIF COND' );
  ELSE
    DBMS_OUTPUT.PUT_LINE( 'ELSE COND' );
  END IF; 

  -- ELSE COND
  IF V1 = 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'IF COND' );
  ELSIF V1 < 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'ELSIF COND' );
  ELSE
    DBMS_OUTPUT.PUT_LINE( 'ELSE COND' );
  END IF; 
END;
/
```

ELSIF clause and ELSE clause are optional, so it may or may not be specified.

When ELSE statement is not specified and any conditions of IF or ELSIF is not true, then it does not perform any statement, but proceeds to the next statement without causing any exception.

<a id="f826deebaf69b8ba"></a>
### CASE

CASE statement selects a single array among arrays of multiple statements such as IF statement, then performs it. CASE statement ends with END CASE keyword, and ELSE clause is optional so it may or may not be specified.

If WHEN clause with an appropriate condition can not be found and ELSE clause is specified, then it  arrays statements below ELSE clause. If an appropriate condition does not exist nor is ELSE clause specified, then CASE_NOT_FOUND exception occurs.  
For more information, refer to [CASE Statement](30-psm-language-element-references.md#f8113628a8bee98f).

WHEN clauses in CASE is evaluated in an specified order, and if an appropriate WHEN clause is found and statements of that WHEN clause are arrayed, then all WHEN clauses after that are ignored.

There are two kinds of CASE statements as follows.

- Simple CASE statement
- Searched CASE statement

<a id="14ae747dee6adb23"></a>
#### Simple CASE Statement

A simple CASE statement arrays statements owned by WHEN clause which has the same value as a selector expression among expressions specified next to WHEN clause by using a selector expression specified next to CASE keyword. Then it ends.

```
DECLARE
V1 VARCHAR(1) := '2';
BEGIN
  CASE V1 WHEN '0' THEN DBMS_OUTPUT.PUT_LINE ('Result = 0');
          WHEN '1' THEN DBMS_OUTPUT.PUT_LINE ('Result = 1');
          WHEN '2' THEN DBMS_OUTPUT.PUT_LINE ('Result = 2');
          ELSE DBMS_OUTPUT.PUT_LINE ('Result = Other');
  END CASE;
END;
/
```

<a id="30cb3fb76aad1399"></a>
#### Searched CASE Statement

A searched CASE statement does not have a selector expression, instead a conditional expression which is evaluated as boolean type per each WHEN clause is specified. When it is executed, it arrays statements owned by the first WHEN clause which is TRUE by evaluating expressions of each WHEN clause. Then it ends.

```
DECLARE
V1 VARCHAR(1) := '2';
BEGIN
  CASE WHEN V1 = 0 THEN DBMS_OUTPUT.PUT_LINE ('Result = 0');
       WHEN V1 = 1 THEN DBMS_OUTPUT.PUT_LINE ('Result = 1');
       WHEN V1 = 2 THEN DBMS_OUTPUT.PUT_LINE ('Result = 2');
       ELSE DBMS_OUTPUT.PUT_LINE ('Result = OTHER');
  END CASE;
END;
/
```

<a id="aac29fd5b836de39"></a>
## Iterative Control

Iterative control statements performs a series of statements several times. GOLDILOCKS PSM provides the following iterative control statements.

- Basic loop
- FOR loop
- WHILE loop

<a id="396074b888bb7fa1"></a>
### Basic Loop

A basic loop statement encloses a series of statements which are to be performed several times with  LOOP and END LOOP keywords. This statement indefinitely performs the inner statements, and it can escape out of the loop by using EXIT or GOTO statements which are sequential control statements.   
For more information, refer to [Basic LOOP Statement](30-psm-language-element-references.md#20e8e5a8347535a1).

The following is an example of escaping from a basic loop which has the closest scope from that location by using EXIT WHEN statement.  
For more information, refer to [EXIT Statement](30-psm-language-element-references.md#d41640b5f286a508).

```
gSQL> DECLARE
  V1 INTEGER := 1;
BEGIN
  LOOP
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
    V1 := V1 + 1;
    EXIT WHEN V1 > 10;   -- Escape Condition
  END LOOP;
END;
/

V1 = 1
V1 = 2
V1 = 3
V1 = 4
V1 = 5
V1 = 6
V1 = 7
V1 = 8
V1 = 9
V1 = 10

Anonymous PL block executed.
```

To escape out of a specific loop when multiple loops are nested, specify a label in front of that loop and specify that label as a target label in EXIT statement.

```
gSQL> DECLARE
  V1 INTEGER := 1;
BEGIN
  <<OUTER_LOOP>>
  LOOP
    <<INNER_LOOP>>
    LOOP
      DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
      V1 := V1 + 1;
      EXIT OUTER_LOOP WHEN V1 > 5;  -- Escape Condition
    END LOOP INNER_LOOP;
    DBMS_OUTPUT.PUT_LINE( 'END OF INNER LOOP' );
    V1 := V1 + 5;
  END LOOP OUTER_LOOP;
  DBMS_OUTPUT.PUT_LINE( 'END OF OUTER LOOP' );
END;
/

V1 = 1
V1 = 2
V1 = 3
V1 = 4
V1 = 5
END OF OUTER LOOP

Anonymous PL block executed.
```

<a id="597cb2682b081288"></a>
### FOR Loop

FOR loop statement repeatedly performs a series of statements as many times as the number of integers of the given scope.  
For more information, refer to [FOR LOOP Statement](30-psm-language-element-references.md#8eb927ba8d4f181c).

A user creates an index variable with the name specified next to FOR keyword.  
Then, it sets the lower bound specified on the left side of a scope operator (..) which is next to IN keyword as an initial value of the index variable. Then, it performs a series of statements by increasing the index variable by 1 per each loop until it becomes the same as the higher bound specified on the right side of a scope operator (..).

```
BEGIN
  FOR I IN 0 .. 2 LOOP
    DBMS_OUTPUT.PUT_LINE( 'I = ' || I );
  END LOOP;
END;
/

I = 0
I = 1
I = 2

Anonymous PL block executed.
```

When REVERSE keyword is specified in front of the scope, it sets the higher bound specified on the right side of a scope operator (..) as an initial value of the index variable. Then, it performs a series of statements by decreasing the index variable by 1 per each loop until it becomes the same as the lower bound specified on the left side of a scope operator (..).

```
BEGIN
  FOR I IN REVERSE 0 .. 2 LOOP
    DBMS_OUTPUT.PUT_LINE( 'I = ' || I );
  END LOOP;
END;
/

I = 2
I = 1
I = 0

Anonymous PL block executed.
```

<a id="d54cc661ab584847"></a>
### WHILE Loop

WHILE loop statement repeatedly performs a series of statements while the given condition is TRUE.  
For more information, refer to [WHILE LOOP Statement](30-psm-language-element-references.md#9abf0ef3a214066f).

```
DECLARE
V1 integer := 0;
BEGIN
  WHILE V1 < 10 LOOP
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
    V1 := V1 + 1;
  END LOOP;
END;
/
```

WHILE loop checks given conditions before performing statements of a body so if the condition is FALSE from the beginning, then it may not perform statements of a body at all.

<a id="a608e3804cdf94e1"></a>
## Sequential Control

Sequential control statements move on which a program is performed from the current performing location to another location.

GOLDILOCKS PSM provides the following three sequential control statements.

- GOTO
- CONTINUE
- EXIT

<a id="200e5a99720a512d"></a>
### GOTO

GOTO statement moves the performing location to the statement in which the given label is. It can be specified in front of any statement which is executable within PSM of a label.  A target label to which GOTO moves can exist before and after the GOTO statement. However, only a visible statement can perform GOTO.  
For more information, refer to [GOTO Statement](30-psm-language-element-references.md#82bb91693962eb5e).

Conditions for a visible statement is as follows.

- Sibling statements located before and after the current performing location
- A superordinate statement of the current location, and sibling statements located before and after that superordinate statement

The following is an example of moving a performing location to a sibling statement of the current location.

```
gSQL> BEGIN

  <<PARENT_PREV>>
  DBMS_OUTPUT.PUT_LINE('PARENT PREV');

  <<PARENT>>
  IF 1 > 0 THEN
    <<SIBLING_PREV>>
    DBMS_OUTPUT.PUT_LINE('SIBLING PREV');

    <<CURRENT_POSITION>>
    GOTO SIBLING_NEXT;

    DBMS_OUTPUT.PUT_LINE('SIBLINGS');
    DBMS_OUTPUT.PUT_LINE('SIBLINGS');

    <<SIBLING_NEXT>>
    DBMS_OUTPUT.PUT_LINE('SIBLING NEXT');
  ELSE
    <<NON_SIBLING>>
    DBMS_OUTPUT.PUT_LINE('NON SIBLING');
  END IF;

  <<PARENT_NEXT>>
  DBMS_OUTPUT.PUT_LINE('PARENT NEXT');

END;
/

PARENT PREV
SIBLING PREV
SIBLING NEXT
PARENT NEXT

Anonymous PL block executed.
```

The following is an example of moving a performing location to a superordinate statement of a current location.

```
gSQL> BEGIN

  <<PARENT_PREV>>
  DBMS_OUTPUT.PUT_LINE('PARENT PREV');

  <<PARENT>>
  IF 1 > 0 THEN
    <<SIBLING_PREV>>
    DBMS_OUTPUT.PUT_LINE('SIBLING PREV');

    <<CURRENT_POSITION>>
    GOTO PARENT_NEXT;

    DBMS_OUTPUT.PUT_LINE('SIBLINGS');
    DBMS_OUTPUT.PUT_LINE('SIBLINGS');

    <<SIBLING_NEXT>>
    DBMS_OUTPUT.PUT_LINE('SIBLING NEXT');
  ELSE
    <<NON_SIBLING>>
    DBMS_OUTPUT.PUT_LINE('NON SIBLING');
  END IF;

  <<PARENT_NEXT>>
  DBMS_OUTPUT.PUT_LINE('PARENT NEXT');

END;
/

PARENT PREV
SIBLING PREV
PARENT NEXT

Anonymous PL block executed.
```

The following is an example of moving a performing location to a statement which is not a sibling, so an error occurs.

```
gSQL> BEGIN

  <<PARENT_PREV>>
  DBMS_OUTPUT.PUT_LINE('PARENT PREV');

  <<PARENT>>
  IF 1 > 0 THEN
    <<SIBLING_PREV>>
    DBMS_OUTPUT.PUT_LINE('SIBLING PREV');

    <<CURRENT_POSITION>>
    GOTO NON_SIBLING;

    DBMS_OUTPUT.PUT_LINE('SIBLINGS');
    DBMS_OUTPUT.PUT_LINE('SIBLINGS');

    <<SIBLING_NEXT>>
    DBMS_OUTPUT.PUT_LINE('SIBLING NEXT');
  ELSE
    <<NON_SIBLING>>
    DBMS_OUTPUT.PUT_LINE('NON SIBLING');
  END IF;

  <<PARENT_NEXT>>
  DBMS_OUTPUT.PUT_LINE('PARENT NEXT');

END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (12:10): ERR-HY000(17010): can not find label name
```

Likewise, when moving a performing location to a statement which is not a superordinate sibling of the current statement, then an error occurs.

GOTO is a good tool to make a PSM program logic flexible. However, like in other languages, if it is used too much, then it may downgrade the readability, so maintenance becomes difficult. Therefore, it is recommended to use loop statements such as FOR or WHILE for an ordinary logics, and use GOTO only when it is necessary.

<a id="a00be9af2e0f2837"></a>
### CONTINUE

CONTINUE statement terminates the current iteration and starts the next iteration within a loop statement such as FOR or WHILE.   
For more information, refer to [CONTINUE Statement](30-psm-language-element-references.md#02a73511f88bd73d).

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
```

If a target label is specified, it starts the next iteration of a loop which has the corresponding label. If it is not specified, it starts the next iteration of the closest (inner) loop.

```
DECLARE
  V1 INTEGER := 1;
BEGIN
  <<AAA>>
  FOR I IN 0..5 LOOP
    <<BBB>>
    WHILE V1 <= 10 LOOP
      DBMS_OUTPUT.PUT_LINE( 'I = ' || I );
      DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
      V1 := V1 + 1;
      IF V1 <= 2 THEN
        CONTINUE BBB;
      ELSE
        EXIT AAA;
      END IF;
    END LOOP BBB;
  END LOOP AAA;
END;
/
```

WHEN clause can be optionally specified in CONTINUE statement. In this case, it terminates the current iteration and starts the next iteration, only when an expression next to WHEN clause is TRUE.

```
DECLARE
  V1 INTEGER :=0 ;
BEGIN
  LOOP
    V1 := V1 + 1;
    CONTINUE WHEN V1 < 5;
    EXIT;
  END LOOP;
END;
/
```

<a id="42eaf65e32717a9f"></a>
### EXIT

EXIT statement escapes the current loop and performs the next statement.  
For more information, refer to [EXIT Statement](30-psm-language-element-references.md#d41640b5f286a508).

```
DECLARE
  V1 INTEGER := 1;
BEGIN
  WHILE V1 <= 10 LOOP
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
    IF V1 > 5 THEN
      EXIT;
    END IF;
    V1 := V1 + 1;
  END LOOP;
END;
/
```

If a target loop is specified, then it escapes a loop which has the corresponding label.

```
DECLARE
  V1 INTEGER := 1;
BEGIN
  <<AAA>>
  FOR I IN 0..5 LOOP
    <<BBB>>
    WHILE V1 <= 10 LOOP
      DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
      IF V1 >= 5 THEN
        EXIT AAA;
      END IF;
      V1 := V1 + 1;
    END LOOP BBB;
  END LOOP AAA;
END;
/
```

WHEN clause can be optionally specified in EXIT statement, like as in CONTINUE statement. In this case, it performs EXIT, only when the given condition is TRUE.

```
DECLARE
  V1 INTEGER := 1;
BEGIN
  <<AAA>>
  FOR I IN 0..5 LOOP
    <<BBB>>
    WHILE V1 <= 10 LOOP
      DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
      EXIT AAA WHEN V1 >= 5;
      V1 := V1 + 1;
    END LOOP BBB;
  END LOOP AAA;
END;
/
```

<a id="49dd8ff2244279ba"></a>
## Error Handling

Errors in PSM are as follows depending on the point of time when it occurs.

- Errors at compile time
- Errors at run time

<a id="d64ecd2c0e4b7297"></a>
### Errors at Compile Time

A compile error outputs an error which occurs during the validation of PSM statement specified in a procedure/function.

A syntax error outputs only the location of the first found syntax error as follows, so a user should compile it again to find out if there are any additional errors.

```
CREATE OR REPLACE PROCEDURE PROC1
IS
BEGIN
  V1 = 1;
  V2 = 1;
END;
/

ERR-42000(40000): syntax error: 
  V1 = 1;
.....^
Error at line 4
```

If a syntax error does not exist, then GOLDILOCKS performs a validation while compiling a PSM statement and the errors occurred in this case are output as follows.

```
CREATE OR REPLACE PROCEDURE PROC1
IS
BEGIN
  V1 := 1;
  V2 := 2;
END;
/

ERR-01000(16409): Warning: Routine definition has compilation errors
ERR-HY000(17032): PSM compilation error : 
(1) at (4:3): ERR-HY000(17006): unknown variable or column name (V1)
(2) at (5:3): ERR-HY000(17006): unknown variable or column name (V2)
Procedure created.
```

Compile errors output the information of errors within the size which is allowed in the error output buffer of GOLDILOCKS. Therefore, some errors may not be output. If so, it is output in the following form to notify that there are errors which are not output.

```
CREATE OR REPLACE PROCEDURE PROC1
IS
BEGIN
V1 := 1;
V2 := 2;
V3 := 2;
V4 := 2;
V5 := 2;
V6 := 2;
V7 := 2;
V8 := 2;
V10 := 2;
END;
/

ERR-01000(16409): Warning: Routine definition has compilation errors
ERR-HY000(17032): PSM compilation error :
(1) at (4:3): ERR-HY000(17006): unknown variable or column name (V1)
(2) at (5:3): ERR-HY000(17006): unknown variable or column name (V2)
(3) at (6:3): ERR-HY000(17006): unknown variable or column name (V3)
(4) at (7:3): ERR-HY000(17006): unknown variable or column name (V4)
(5) at (8:3): ERR-HY000(17006): unknown variable or column name (V5)
(6) at (9:3): ERR-HY000(17006): unknown variable or column name (V6)
(7) at (10:3): ERR-HY000(17006): unknown variable or column name (V7)
2 more errors...
```

An error message is output in the following form.

```
(Index) at (Line_Number : Column_Position): ERR-SQLState( Internal_ErrorCode): Detail_Error_Message
```

- Index
    - It is a sequence of an error occurrence.
- Line_Number
    - It is a location of a line of source in which an error occurred.
- Column_Position
    - It is a location of a column of a source in which an error occurred.
- ERR-SQLState
    - It is a standard SQLState.
- Internal_ErrorCode
    - It is an internal error code.
- Detail_Error_Message
    - It is details of an error message.

<a id="0285aba8cea450ff"></a>
### Errors at Run-time

An error may occur in a PSM statement for various reasons even when PSM is normally executed. In this case, GOLDILOCKS provides an exception handling to help a user to control the error.

The following is an example of an error occurrence at the time of execution. If an error occurs when executing GOLDILOCKS PMS, then it outputs a location of an error, a PSM error and an internal error together. In other words, one or more errors may occur, so all errors should be retrieved from the database through a function such as SQLGetDiagRec if a user wants to find out the exact error message during the development process such as ODBC.

```
DECLARE
  V1 INTEGER;
BEGIN
  V1 := 1 / 0;
END;
/

ERR-HY000(17007): invalid expression : 
  V1 := 1 / 0;
        *
ERROR at line 4:
ERR-22012(12122): divisor is equal to zero
```

If an error occurs at the time of operation, PSM immediately stops the operation and notifies it to a user. However, if a user wants to directly control these errors and keep the program running, the user should perform the exception handling.

The following is an example of definition to run the user program without interruption by performing the exception handling on the location of an error.

```
DECLARE
  V1 INTEGER;
BEGIN
  BEGIN
    V1 := 1 / 0;
  EXCEPTION WHEN OTHERS 
            THEN DBMS_OUTPUT.PUT_LINE('SQLCODE = ' || SQLCODE);
                 DBMS_OUTPUT.PUT_LINE('SQLERRM = ' || SQLERRM);
  END;
  
  DBMS_OUTPUT.PUT_LINE('next code');
END;
/
SQLCODE = -12122
SQLERRM = [SUNJESOFT][PSM][GOLDILOCKS]divisor is equal to zero
next code

Anonymous PL block executed.
```

For more information, refer to [EXCEPTION Handling](#00eb7fcee2f75e35), [SQLCODE Function](30-psm-language-element-references.md#78bc0f05c5677702), [SQLERRM Function](30-psm-language-element-references.md#1157868335bfdf87).

<a id="3ddfc4f6d4cb9606"></a>
### Cursor Attributes

Cursor attributes are attributes (variables) which are provided to display the cursor status specified by a user or to display the inside of the database, while processing PSM.

- Cursors are specified as follows.
    - Implicit cursor
        - It is a cursor which is OPEN/ FETCH/ CLOSE inside of the database when it is required.
    - Explicit cursor
        - It is a cursor which OPEN/ FETCH /CLOSE after when a user explicitly perform declaration/ definition.

<a id="fad182c939dd80f7"></a>
#### Implicit Cursor Attributes

Implicit cursor attributes in PSM is used to find out the processing status of a SQL statement which was proximately performed. Each value of attributes can be used in expressions such as a conditional expression, so a user can control it such as branching logics of a program through that value.   
For more information about attributes, refer to the following table.

**Implicit cursor attributes**

<a id="7baea4717b8e1b96"></a>
| Attribute name | Return type | Description |
| --- | --- | --- |
| ISOPEN | BOOLEAN | It is always FALSE because it is internally closed. |
| FOUND | BOOLEAN | If the data is returned by the previous statement, then it is TRUE. Otherwise, it is FALSE. |
| NOTFOUND | BOOLEAN | It is the opposite value of FOUND. |
| ROWCOUNT | INTEGER | It is the number of rows affected by the previous statement. |

The syntax is used in the following form.

```
SQL%Attribute_name

Attribute_name := ISOPEN | FOUND | NOTFOUND | ROWCOUNT
```

Each attribute can be viewed as the following example.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);
Table created.

gSQL> INSERT INTO T1 VALUES ('Seoul', '24');
1 row created.

gSQL> INSERT INTO T1 VALUES ('Pusan', '44');
1 row created.

gSQL> BEGIN
    UPDATE T1 SET C2 = C2 + 1;
  
    DBMS_OUTPUT.PUT_LINE('ISOPEN   = ' || SQL%ISOPEN );
    DBMS_OUTPUT.PUT_LINE('FOUND    = ' || SQL%FOUND );
    DBMS_OUTPUT.PUT_LINE('NOTFOUND = ' || SQL%NOTFOUND );
    DBMS_OUTPUT.PUT_LINE('ROWCOUNT = ' || SQL%ROWCOUNT );
END;
/
ISOPEN   = FALSE
FOUND    = TRUE
NOTFOUND = FALSE
ROWCOUNT = 2

Anonymous PL block executed.
```

<a id="45aad66202811f2a"></a>
#### Explicit Cursor Attributes

Explicit cursor attributes is used to enquire the status of an explicit cursor.  
For more information about attributes, refer to the following table.

**Cursor attributes**

<a id="04c7c8121c3af856"></a>
| Attributes | Return type | Description |
| --- | --- | --- |
| %ISOPEN | BOOLEAN | It is TRUE only when a cursor is normally open. Otherwise, it is FALSE. |
| %FOUND | BOOLEAN | It is NULL before FETCH, and it is TRUE when FETCH is normally performed. It is FALSE when data does not exist, and it is NULL after CLOSE. |
| %NOTFOUND | BOOLEAN | It is the opposite value of %FOUND. |
| %ROWCOUNT | INTEGER | It is NULL before OPEN, and it is 0 when it is normally OPEN. It increases by 1 whenever FETCH succeeds. |

It is used as follows within PSM.

```
Cursor_Name % Attribute_name
Attribute_name :=  ISOPEN
                 | FOUND
                 | NOTFOUND
                 | ROWCOUNT
```

The following is an example of using an explicit cursor attribute.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);
Table created.

gSQL> INSERT INTO T1 VALUES ('Seoul', '24');
1 row created.

gSQL> INSERT INTO T1 VALUES ('Pusan', '44');
1 row created.

gSQL> DECLARE
  CURSOR C1 IS SELECT * FROM T1;
  v1 c1%ROWTYPE;
BEGIN
```

- Check if the cursor is open through ISOPEN.

```
IF C1%ISOPEN = FALSE
  THEN
      OPEN C1;
  END IF;


  LOOP
      FETCH C1 INTO v1;
```

- Check if there is any more data through NOTFOUND.

```
EXIT WHEN C1%NOTFOUND;
```

- Find out the number of fetched rows through ROWCOUNT.

```
DBMS_OUTPUT.PUT_LINE('COUNT = ' || C1%ROWCOUNT );
  END LOOP;

  CLOSE C1;
  
END;
/
COUNT = 1
COUNT = 2

Anonymous PL block executed.
```

<a id="00eb7fcee2f75e35"></a>
### EXCEPTION Handling

Exceptions within PSM is a definition of various errors occurred while a user is executing PSM. If an error occurs at the time of operation, PSM immediately stops the operation and returns an error to a user. EXCEPTION handling is a function provided to a user to control EXCEPTION situation and keep the program running without interruption.

<a id="27734342138e3256"></a>
#### Exception Handler

An error situation can be controlled through an exception handler defined in PSM BLOCK as follows.

```
DECLARE
  V1 INTEGER;
BEGIN
  BEGIN
    V1 := 1 / 0;
```

- Exception handler

```
EXCEPTION WHEN OTHERS 
            THEN DBMS_OUTPUT.PUT_LINE('SQLCODE = ' || SQLCODE);
                 DBMS_OUTPUT.PUT_LINE('SQLERRM = ' || SQLERRM);
  END;
  
  DBMS_OUTPUT.PUT_LINE('next code');
END;
/
SQLCODE = -12122
SQLERRM = [SUNJESOFT][PSM][GOLDILOCKS]divisor is equal to zero
next code
```

In the example above, the program is stopped by *divide by zero* at the time of execution. However, if an error occurred by an exception handler, then only the corresponding BLOCK stops, but the processing continues from the next location.

An exception handler is specified as follows.

```
BEGIN
EXCEPTION WHEN exception_name, [exception_name, ...] THEN pl_statements;
         [WHEN exception_name, [exception_name, ...] THEN pl_statements;
END
```

- Features of an exception handler are as follows.
    - A single exception handler is specified in BLOCK.
    - One or more Exception_Name can be specified and its operation can be defined within an exception handler.
    - Exception_name within an exception handler should not be duplicate.
    - It is operated only for an error within PL BLOCK SCOPE in which an exception handler is specified.
    - OTHERS indicating all exceptional situations should be unique, and should be specified at last.
    - If an exception handler is normally completed, the previous errors are cleared. Therefore, a user should store them in a separate PSM variable if in need.

An exception in GOLDILOCKS has the following properties.

**EXCEPTION types**

<a id="32e61035d4b7d885"></a>
| Type | Definer | Error code | Name | Raise implicitly | Raise explicitly |
| --- | --- | --- | --- | --- | --- |
| Predefined | Database | O | O | O | Optionally |
| User defined | User | User-defined | User defined | X | O |

> For more information about a predefined exception or a user defined exception provided by GOLDILOCKS, refer to [Exception Declaration](30-psm-language-element-references.md#99e4ba38991da3b6).

<a id="964f50da79b24770"></a>
#### Propagating Exception

If an appropriate exception handler does not exist in the current BLOCK when an exception occurs, then it is propagated to an exception handler of the superordinate BLOCK until the exception is processed.

If an error occurred on LINE_1 in the following code, the result varies upon whether an exception handler operates.

```
BEGIN
  ...
  BEGIN
    LINE_1
    EXCEPTION HANDLER_1
  END;
  LINE_2
  EXCEPTION HANDLER_2
END;
/
```

- When it is processed in EXCEPTION_HANDLER_1
    - If the handler operation is normally completed, then it is performed from LINE_2.
- When an appropriate handler does not exist in EXCEPTION_HANDLER_1
    - It can not perform LINE_2, and the currently occurred EXCEPTION is propagated to EXCEPTION_HANDLER_2.
        - When an appropriate handler exists in EXCEPTION_HANDLER_2, if a handler operation is normally completed, then the program ends. 
        - If a handler does not exist in EXCEPTION_HANDLER_2, the program stops and the currently occurred error is returned to a user.

> If an error occurred in an exception handler which was processing an exception, then the error code is propagated to a superordinate BLOCK.

```
DECLARE
  V1 INTEGER;
  E1 EXCEPTION;
  E2 EXCEPTION;
BEGIN
  BEGIN
    RAISE E1;
  EXCEPTION WHEN E1 THEN V1 := 1 / 0;   ❶ A new error occurs.
  END;

  EXCEPTION WHEN E1 
            THEN DBMS_OUTPUT.PUT_LINE('User Exception');
            WHEN ZERO_DIVIDE           
            THEN DBMS_OUTPUT.PUT_LINE('Zero divide');
END;
/
Zero divide

Anonymous PL block executed.
```

<a id="bfb543cf5efc3a72"></a>
#### User Defined Exception

A user defined exception is an exception used by setting an exception name and an error-code by a user except for a predefined. User defined exception can not implicitly occur, but a user should execute it by explicitly using a RAISE statement.

The following is an example of causing an exception by using a RAISE statement.

```
DECLARE
  V1   INTEGER;
  high EXCEPTION;
  low  EXCEPTION;
BEGIN

  BEGIN
      V1 := 10;

      IF V1 > 10 
      THEN
          RAISE high;
      ELSE
          RAISE low;
      END IF;

  EXCEPTION WHEN high 
            THEN DBMS_OUTPUT.PUT_LINE('High');
            WHEN low
            THEN DBMS_OUTPUT.PUT_LINE('Low');
  END;
END;
/
Low
```

- A user defined exception is processed depending on the following two cases. 
    - When an error-code is set
    - When an error-code is not set

It is operated as follows when a user sets an error code.

```
DECLARE
  V1 INTEGER;
  E1 EXCEPTION;
  PRAGMA EXCEPTION_INIT( E1, -12122);
BEGIN
  BEGIN
    V1 := 1 / 0;
  EXCEPTION WHEN E1
            THEN DBMS_OUTPUT.PUT_LINE('SQLCODE = ' || SQLCODE);
                 DBMS_OUTPUT.PUT_LINE('SQLERRM = ' || SQLERRM);
  END;
END;
/
SQLCODE = -12122
SQLERRM = [SUNJESOFT][PSM][GOLDILOCKS]divisor is equal to zero
```

The ZERO_DIVIDE predefined exception exists, but a user sets a handler by setting an error code as E1 exception. For the program compatibility between vendors with each different error code as above, an exception handler is available of which a user directly resets an error code.

A user defined exception in which an error-code is not set is set as the following error code and message in an exception handler.

```
DECLARE
  V1 INTEGER;
  E1 EXCEPTION;
BEGIN
  BEGIN
    RAISE E1;
  EXCEPTION WHEN E1
            THEN DBMS_OUTPUT.PUT_LINE('SQLCODE = ' || SQLCODE);
                 DBMS_OUTPUT.PUT_LINE('SQLERRM = ' || SQLERRM);
  END;
END;
/
SQLCODE = 1
SQLERRM = [SUNJESOFT][PSM][GOLDILOCKS]User-Defined Exception

Anonymous PL block executed.
```

A propagation process of a user defined exception is the same as that of a predefined exception. However, if an error-code is not set in a user defined exception, it is propagated as unhandled user exception error to the superordinate BLOCK.

```
DECLARE
  V1 INTEGER;
  E1 EXCEPTION;
  E2 EXCEPTION;
BEGIN
  BEGIN
    RAISE E1;
  EXCEPTION WHEN E2
            THEN DBMS_OUTPUT.PUT_LINE('SQLCODE = ' || SQLCODE);
                 DBMS_OUTPUT.PUT_LINE('SQLERRM = ' || SQLERRM);
  END;
END;
/

ERR-HY000(17017): Unhandled user exception : 
    RAISE E1;
          *
ERROR at line 7:
```

An unhandled user exception can be caught by specifying a user defined exception in an exception handler or by using OTHERS which is a predefined exception.

<a id="967605f761dc40d1"></a>
### PRAGMA EXCEPTION_INIT

It is used for a user sets a specific DBMS error code when using a user defined exception. DBMS error codes varies depending on vendors, so it can be used for a compatibility of an exception handler of PSM code.

The syntax is as follows.

```
<PRAGMA EXCEPTION_INIT> ::= 
    PARAGMA EXCEPTION_INIT ( exception_name, internal_errorcode )
```

- Constraints are as follows.
    - exception_name should be declared in advance.
    - exception_name can not use a predefined exception.
    - Only an internal error-code of GOLDILOCKS is available for internal_errorcode.
    - It can not set 0 which means SUCCESS.

The following is an example of handling an exception of when assigning NULL to V1 (the PSM variable to which NOT NULL constraints are applied) by using a user defined exception.

```
DECLARE
  V1 VARCHAR(20) NOT NULL := 10;
  USER_EXCEPT EXCEPTION;
```

- Declare the PSM NOT NULL constraint error as a user defined exception.

```
PRAGMA EXCEPTION_INIT( USER_EXCEPT, -17009 );
BEGIN
```

- Generate a situation of an exception.

```
V1 := NULL;

  EXCEPTION WHEN USER_EXCEPT THEN DBMS_OUTPUT.PUT_LINE('Check Value');
END;
/
Check Value

Anonymous PL block executed.
```

The following error occurs when setting a value that is not an internal error-code of GOLDILOCKS.

```
DECLARE
  E1 EXCEPTION;
  PRAGMA EXCEPTION_INIT( E1, 99999);
BEGIN
    NULL;
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (3:30): ERR-HY000(17021): Invalid error number for PRAGMA EXCEPTION_INIT
```

<a id="e7622408753c83e8"></a>
### DBMS_STANDARD.RAISE_APPLICATION_ERROR

It is used to easily generate an exception through an arbitrary user error code and a message, instead of explicitly defining a user exception. It belongs to a DBMS_STANDARD module, and the routines of this module can be called even when omitting a name of that module.

There are three types of arguments as follows.

**RAISE_APPLICATION_ERROR**

<a id="89cdc474144f04d5"></a>
| Argument | Description |
| --- | --- |
| error_code IN NATIVE_INTEGER | It is a value of an error code to be arbitrarily generated. Only the value within the range of -20000 ~ -20999 can be used. |
| error_message IN VARCHAR(4000) | It is a message to be stored in SQLERRM when an error occurs. |
| stack_flag IN BOOLEAN := FALSE | It is a flag of whether to stack on the existing errors (TRUE), or to replace with all existing errors (FALSE). The default value is FALSE. |

The following is a simple example of using it.

```
CREATE OR REPLACE PROCEDURE PROC1
IS
BEGIN
  RAISE_APPLICATION_ERROR (-20000, 'USER DEFINED ERROR TEST');
END;
/

Procedure created.

BEGIN
  PROC1;
EXCEPTION WHEN OTHERS THEN
  DBMS_OUTPUT.PUT_LINE( 'SQLCODE : ' || SQLCODE || ' SQLERRM : ' || SQLERRM );
END;
/
SQLCODE : -20000 SQLERRM : [SUNJESOFT][PSM][GOLDILOCKS]USER DEFINED ERROR TEST

Anonymous PL block executed.
```

---

[← 22. PSM DataTypes](22-psm-datatypes.md) · [Table of contents](../README.md) · [24. PSM Cursor Statements →](24-psm-cursor-statements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
