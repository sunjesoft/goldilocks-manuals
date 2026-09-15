<a id="708c98b86a7a162f"></a>

# 30. PSM Language Element References

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/708c98b86a7a162f)  
> 태그: `26c.1_0_tag`

[← 29. Trigger](29-trigger.md) · [전체 목차](../README.md) · [31. PSM SQL References →](31-psm-sql-references.md)

<a id="672c105425c0f8ed"></a>
## Assignment Statement

<a id="4f2cfae0f66a3005"></a>
### 기능

PSM block의 내부에서 변수나 out-bind parameter에 값을 저장한다.

<a id="23a632b123eb35aa"></a>
### 구문

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

<a id="f5bb513ccec96655"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="fb09dce161500665"></a>
### 구문 규칙 및 파라미터

- collection_variable
    - DECLARE 영역에서 선언된 COLLECTION 타입의 변수 이름이다.
- index
    - collection_variable의 element들 중에서 한 개를 고를 key 값이다.
- cursor_variable
    - DECLARE 영역에서 선언된 cursor 이름이다.
- host_variable
    - PSM을 호출하는 곳에서 전달된 out 또는 in-out 타입의 client-side 변수 이름이다.
- indicator_variable
    - host_variable의 NULL 값을 체크하고 실제 값의 길이를 알아내기 위한 indicator 변수의 이름이다.
- record_variable
    - DECLARE 영역에서 이미 선언된 RECORD 타입의 변수 이름이다.
- field_name
    - RECORD 타입의 변수에 포함된 필드 중 한 개의 이름이다.
- scalar_variable
    - DECLARE 영역에서 이미 선언된 일반 scalar 타입의 변수 이름이다.

<a id="c5a5d03bb19f349c"></a>
### 설명

Assignment 문의 target은 외부의 bind parameter와 내부의 PSM 변수로 나뉜다.

- 외부 parameter 
    - Host variable 
    - Host cursor variable 
- 내부 변수 
    - Out 타입 함수 인자 
    - 내부에서 선언된 변수 
        - Scalar/ record/ multi-set 타입 
        - Record 타입 변수의 특정 필드 
        - Multi-set 타입 변수의 특정 element

Procedure/ function parameter를 제외한 모든 변수는 scope를 지정하는 이름을 가질 수 있다.

<a id="285b8cccb6793078"></a>
### 사용 예

다음은 &lt;assignment statement&gt;를 사용하는 예이다.

- PSM 내부 변수에 대한 assignment

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

- Host variable에 대한 assignment

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

<a id="6c1db3d56c424f73"></a>
### 호환성

&lt;assignment statement&gt; 구문은 SQL 표준과 비교하여 다음과 같은 차이가 있다.

- SQL 표준의 &lt;assignment statement&gt;는 &lt;singleton variable assignment&gt;와 &lt;multiple variable assignment&gt;를 정의하지만, GOLDILOCKS는 &lt;singleton variable assignment&gt; 형식만 지원한다. 
- SQL 표준의 &lt;assignment statement&gt;는 SET 키워드로 시작하지만, GOLDILOCKS는 SET 키워드를 사용하지 않는다. 
- SQL 표준의 &lt;assignment statement&gt;는 target과 value 사이에 &lt;equal operator&gt; (=)를 사용하지만, GOLDILOCKS는 := 를 사용한다.

**SQL 표준 호환성**

<a id="db346f831e326f61"></a>
<table><tbody><tr><th align="center">Feature ID</th><th align="center">설명</th><th align="center">지원 여부</th></tr><tr><td align="left">P002</td><td align="left">Computational completeness</td><td align="center">X</td></tr><tr><td align="left">P006</td><td align="left">Multiple assignment</td><td align="center">X</td></tr></tbody></table>

<a id="f3de320964d735f3"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Scalar Variable Declaration](#34027540ee4588ec)
- [Record Variable Declaration](#4209175b58e67025)
- [COLLECTION Variable Declaration](#a4387f0fa0f4d9b3)
- [Cursor Variable Declaration](#5c050768d81529dc)

<a id="1c43bddc54c05d9e"></a>
## Basic LOOP Statement

<a id="90f116811abdcc55"></a>
### 기능

GOTO나 EXIT 등이 수행되어 LOOP를 종료하기 전까지 LOOP 내부의 statement 들을 반복 수행한다.

<a id="df3e860f4cdfec71"></a>
### 구문

```
<basic loop statement> ::=
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="e8d0d929b37b6276"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 body 영역에서만 사용할 수 있다.

<a id="253c08cc73ddb464"></a>
### 구문 규칙 및 파라미터

- loop_name
    - &lt;basic loop statement&gt;의 label 이름이다. 
    - Comment의 역할만 하기 때문에 실제 &lt;basic loop statement&gt;의 label 이름과 달라도 무방하다.

<a id="d3cf1ad2e89d6c5b"></a>
### 설명

Basic loop 구문은 LOOP 내부의 statement들을 반복 수행한다.  
Basic loop 구문은 loop 계열 statement이므로 GOTO, EXIT, CONTINUE가 label로 지칭하는 target statement가 될 수 있다.

<a id="fcc44cc3e271f22d"></a>
### 사용 예

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

<a id="8d459f1b812acd32"></a>
### 호환성

&lt;basic loop statement&gt; 구문은 SQL 표준의 &lt;loop statement&gt;와 동일하다.

**SQL 표준 호환성**

<a id="f88ce251e1ee02fe"></a>
| Feature ID | 설명 | 지원여부 |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="3fa08452636e2305"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CONTINUE Statement](#35f5b1376cc629d4)
- [EXIT Statement](#46c4e6cb4d956122)
- [GOTO Statement](#b8ae5382c6d22723)

<a id="b5f1979bc247ce01"></a>
## Block (BEGIN .. END)

<a id="c62cc16d9d2808b6"></a>
### 기능

변수, type, cursor, exception을 정의하고 실행하고자 하는 pl statement를 그룹화한다.

<a id="b08e1650b1d1a8ac"></a>
### 구문

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

<a id="09e9b03623efd1b3"></a>
### 사용 범위 및 접근 권한

PROCEDURE, FUNCTION, PACKAGE BODY 또는 anonymous block 내에서만 사용할 수 있다.

<a id="e4c7e659bf8f074f"></a>
### 구문 규칙 및 파라미터

<a id="dbcc98f13b24fd34"></a>
#### &lt;&lt; label name &gt;&gt;

label 이름은 block에 대한 고유 식별자로써 선언되지 않는 식별자이다.  
label 이름의 길이는 128 바이트보다 작아야 한다.

<a id="a423847e65761397"></a>
#### declare item

- Variable declaration
    - 변수를 선언하며, 선언 가능한 변수의 datatype은 다음과 같다.
        - scalar type
        - record type
        - associate array type
        - reference cursor type
- Type definition
    - 사용자 정의 타입을 정의한다.
        - record type
        - associate array type
        - reference cursor type
- Explicit cursor declaration
    - explicit cursor를 선언한다.
- Explicit cursor definition
    - explicit cursor를 정의한다.
- Exception declaration
    - exception 변수를 선언한다.
- Exception init pragma
    - 사용자가 선언한 exception 변수를 GOLDILOCKS의 error code와 매칭한다.
- Procedure declaration
    - procedure를 선언한다.
- Procedure definition
    - procedure를 정의한다.
- Function declaration
    - function을 선언한다.
- Function definition
    - function을 정의한다.

<a id="7738e3ddca012000"></a>
#### body

&lt;PSM block&gt;을 실행하기 시작하는 부분이다.  
&lt;body&gt;는 실행 가능한 &lt;pl statement list&gt;와 예외 핸들링을 위한 &lt;exception block&gt;로 구성된다.

<a id="47489c93a40729ce"></a>
#### pl statement

- assignment statement
    - [Assignment Statement](#672c105425c0f8ed)를 참고한다.
- basic loop statement
    - [Basic LOOP Statement](#1c43bddc54c05d9e)를 참고한다.
- block statement
    - [Block (BEGIN .. END)](#b5f1979bc247ce01)를 참고한다.
- case statement
    - [CASE Statement](#956a63a0902eb2e7)를 참고한다.
- close statement
    - [CLOSE Statement](#c59c992edb95f702)를 참고한다.
- collection method invocation
    - [Collection Method Invocation](#f66d6875e2355066)를 참고한다.
- continue statement
    - [CONTINUE Statement](#35f5b1376cc629d4)를 참고한다.
- cursor for loop statement
    - [Cursor FOR LOOP Statement](#eef32c75f82eb81f)를 참고한다.
- delete statement extension
    - [DELETE Statement Extension](#b7ff64cf994a5599)를 참고한다.
- execute immediate statement
    - [EXECUTE IMMEDIATE Statement](#527305bdfcd7c7ed)를 참고한다.
- exit statement
    - [EXIT Statement](#46c4e6cb4d956122)를 참고한다.
- fetch statement
    - [FETCH Statement](#2be71b2c548c858e)를 참고한다.
- for loop statement
    - [FOR LOOP Statement](#a6f1fcb87e2ef564)를 참고한다.
- goto statement
    - [GOTO Statement](#b8ae5382c6d22723)를 참고한다.
- if statement
    - [IF Statement](#31f7c6e0b61ab3c0)를 참고한다.
- insert statement extension
    - [INSERT Statement Extension](#bad4432950ae600a)를 참고한다.
- insert into ... update statement extension
    - [INSERT INTO ... UPDATE Statement Extension](#b4fbf41981dfde9d)를 참고한다.
- merge statement extension
    - [MERGE Statement Extension](#85537b9e6eef66cf)를 참고한다.
- null statement
    - [NULL Statement](#9fc84cbdae0a92d9)를 참고한다.
- open statement
    - [OPEN Statement](#80c65120562ef0bf)를 참고한다.
- open for statement
    - [OPEN FOR Statement](#eb4bf8bad6641506)를 참고한다.
- procedure call statement
    - [Procedure Call](#b7f71090c8dcbf03)을 참고한다.
- raise statement
    - [RAISE Statement](#4f0dcdacbd73881e)를 참고한다.
- return statement
    - [RETURN Statement](#14c7507ca43ee90a)를 참고한다.
- return table statement
    - [RETURN TABLE Statement](#47b0754ff8d5c167)를 참고한다.
- select into statement
    - [SELECT INTO Statement](#ae316b261e4e6598)를 참고한다.
- sql statement
    - savepoint statement
        - [SAVEPOINT savepoint_specifier](../part-03-sql-manual/20-sql-references-h-z.md#903816d217929cbc)를 참고한다.
    - release savepoint statement
        - [RELEASE SAVEPOINT savepoint_specifier](../part-03-sql-manual/20-sql-references-h-z.md#820eff57a94d3af0)를 참고한다.
    - rollback statement
        - [ROLLBACK](../part-03-sql-manual/20-sql-references-h-z.md#1ba3b433854d9411)를 참고한다.
    - commit statement
        - [COMMIT](../part-03-sql-manual/19-sql-references-c-g.md#9d9942a1324d8ced)를 참고한다.
    - lock table statement
        - [LOCK TABLE](../part-03-sql-manual/20-sql-references-h-z.md#aa7af8e829d2f1c4)를 참고한다.
- update statement extension
    - [UPDATE Statement Extension](#eef0130cc744e99e)를 참고한다.
- while loop statement
    - [WHILE LOOP Statement](#ec75086399351674)를 참고한다.

<a id="5c6ac26f9bf17c13"></a>
#### exception block

&lt;psm block&gt;은 실행 도중에 발생한 예외 상황을 핸들링한다.  
&lt;exception&gt;은 GOLDILOCKS에서 정의한 predefined exception 또는 사용자가 정의한 exception의 이름이다.  
지정된 예외가 발생하면 해당되는 &lt;pl statement list&gt;가 실행된다.

<a id="d739df51ce046945"></a>
### 설명

&lt;psm block&gt;은 PSM의 기본 구성 요소이다.  
Bock은 선언부 (declaration part)와 예외 처리부 (exception handling part)를 가질 수 있다.  
Block은 중첩될 수 있고 중첩된 block은 새로운 하위 변수 scope를 가진다. 상위 block은 하위 block의 변수를 참조할 수 없다.

<a id="b74b906685f2600d"></a>
### 사용 예

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

<a id="a4edc7a10c4786cb"></a>
### 호환성

SQL 표준의 &lt;compound statement&gt;는 새로운 savepoint를 지정하는 ATOMIC/ NOT ATOMIC 구문을 정의하였지만, GOLDILOCKS는 이를 지원하지 않는다.

**SQL 표준 호환성**

<a id="108019ef6d666a30"></a>
| Feature ID | 설명 | 비고 |
| --- | --- | --- |
| P002 | Computational completeness | ATOMIC 구문을 지원하지 않는다. |

<a id="8465899ec77b17ec"></a>
### 참조

자세한 내용은 [Overview of PSM](21-overview-of-psm.md#9a780ad10c33a6fa)을 참조한다.

<a id="1663813aaf9c3eb4"></a>
## Call Specification

<a id="7b6e7d6646bcc465"></a>
### 기능

PSM에서 호출할 수 있도록 C로 작성한 프로그램의 function 이름, parameter의 데이터 타입 및 RETURN의 데이터 타입에 대응하는 정보를 매핑한다.

<a id="6f983e50778fb316"></a>
### 구문

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

<a id="c4d64b88f2b90802"></a>
### 사용 범위 및 접근 권한

&lt;library clause&gt; 에서 library를 사용하기 위해서는 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 library에 대한 EXECUTE 권한
- Library가 속한 schema에 대해 ( EXECUTE LIBRARY 또는 CONTROL SCHEMA ) ON SCHEMA
- EXECUTE ANY LIBRARY ON DATABASE

<a id="e2ab0b9c159e247b"></a>
### 구문 규칙 및 파라미터

<a id="b5bc6d82355fcc6b"></a>
#### LANGUAGE C

C 언어로 작성한 외부 프로그램이다.

<a id="4223e76051333359"></a>
#### LIBRARY &lt;library name&gt;

[CREATE LIBRARY](31-psm-sql-references.md#e6a29c79119e1af1) 구문으로 생성한 library 객체의 이름이다.  
&lt;schema_name&gt;.&lt;library name&gt;처럼 schema를 명시할 수 있다.

<a id="b3a4c7d1b9107bec"></a>
#### NAME &lt;double_quote_string&gt;

C로 작성한 프로그램의 함수 이름을 표시한다.  
"" 사이에 명시되는 함수 이름은 128 바이트보다 작아야 한다.

<a id="3c3c9e9fa084d312"></a>
#### external parameter

Procedure나 Function의 Parameter와 External C function의 parameter의 데이터 타입을 매핑한다.

- CONTEXT
    - external C function에서 exception, 메모리 할당에 대한 액세스를 할 수 있다.
- parameter name
    - Procedure나 Function의 parameter 이름이다.
    - Procedure나 Function에 명시된 parameter는 모두 명시해야 한다.
    - Function의 RETURN은 마지막에 명시해야 한다.
- property
    - INDICATOR
        - parameter나 return의 값에 대한 NULL 여부를 표시할 수 있도록 지원하는 property이다.
        - indicator 변수가 SQL_NULL_DATA이면, 대응되는 parameter나 return의 값은 NULL이다.
        - indicator 변수가 SQL_NULL_DATA이 아니면, 대응되는 parameter나 return의 값은 NULL이 아니다.
    - LENGTH
        - String 또는 RAW 타입의 parameter나 RETURN의 현재의 길이를 나타낸다.
        - IN Parameter의 경우, LENGTH는 값으로 전달된다.
        - OUT, IN OUT Parameter와 RETURN의 경우는 pointer로 전달된다.
    - MAXLEN
        - String 또는 RAW 타입의 parameter나 RETURN의 최대 길이를 나타낸다.
        - IN, OUT, IN OUT Parameter와 RETURN 모두 값으로 전달된다.
- BY REFERENCE
    - C 함수의 parameter가 pointer 형일 때, Routine의 IN Parameter에 BY REFERENCE 구문을 지정하여 전달한다.
- external datatype
    - SQL Parameter의 datatype과 External Parameter의 datatype을 매핑한다.
    - 자세한 정보는 [External Routine](28-external-routine.md#5edbddf52d93deaf)의 [Parameter Data Type Mapping](28-external-routine.md#465f6e945fc60a47)을 참조한다.

<a id="37a0e6a83f928a62"></a>
### 설명

&lt;call specification&gt; 구문은 External C function 이름, parameter의 데이터타입 및 RETURN의 데이터타입에 대응하는 정보를 맵핑한다.

&lt;call specification&gt; 은 아래의 구문에서 사용할 수 있다.

- [CREATE FUNCTION](31-psm-sql-references.md#8f6d3c41338c889a)
- [CREATE PROCEDURE](31-psm-sql-references.md#48b6178f1f6cd4cb)
- [CREATE PACKAGE](31-psm-sql-references.md#5f9bdd6eb052f51f)
- [CREATE PACKAGE BODY](31-psm-sql-references.md#4af32611ea712290)

PL/SQL Block의 &lt;body&gt;에서는 사용할 수 없다.

<a id="145fa3bd5f6e4e5d"></a>
### 사용 예

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

<a id="540fcf00c445aa6e"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.   
SQL 표준에서 &lt;external body reference&gt;의 기능과 유사하다.

<a id="7c9b7dbf0a44b859"></a>
### 참조

자세한 내용은 [External Routine](28-external-routine.md#5edbddf52d93deaf)을 참조한다.

<a id="956a63a0902eb2e7"></a>
## CASE Statement

<a id="3b7ed8771a132cee"></a>
### 기능

주어진 여러 조건들 중에 TRUE를 반환하는 조건에 해당하는 statement list를 수행한다.

<a id="2cc6fd867316228f"></a>
### 구문

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

<a id="ec29207a13b9fd11"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="6485c4f5dd4968df"></a>
### 구문 규칙 및 파라미터

- Case operand
    - Scalar 값으로 평가될 수 있는 모든 표현식이다.
    - 단, subquery 구문은 포함할 수 없다.
- When operand
    - &lt;case operand&gt;와 같은지 비교할 표현식이다.
    - Subquery 구문은 포함할 수 없다
- Search condition
    - &lt;searched case statement&gt;에서 평가하여 TRUE인 경우에 실행할 조건식이다.
    - Subquery 구문은 포함할 수 없다.
- Executable statement list
    - PSM 내에서 수행할 수 있는 모든 statement 리스트이다.

<a id="677fea8c4de4b7df"></a>
### 설명

IF 구문과 유사하게 조건들을 평가하여 TRUE를 반환하는 WHEN 절의 statement들을 수행한다.   
순서대로 먼저 나오는 조건식부터 평가하여 해당 조건식이 TRUE인 경우, 그 이후의 조건식들은 평가하지 않는다.   
만일 조건식에 해당하는 경우가 존재하지 않고 ELSE 절이 기술되지 않은 경우에는 에러가 발생한다.

<a id="261fb800cf1779a8"></a>
### 사용 예

<a id="6623f2e99f6529de"></a>
#### Simple CASE 사용

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

<a id="0d93e1c15a540d87"></a>
#### Searched CASE 사용

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

<a id="d809fbcebd5e4881"></a>
### 호환성

SQL 표준의 CASE 구문은 row 타입 (list 타입) value 간의 비교를 정의하였지만, GOLDILOCKS는 지원하지 않는다  
SQL 표준의 CASE 구문은 &lt;when operand&gt;에 ','로 구분되는 여러 조건들을 리스트로 정의할 수 있지만, GODILOCKS는 지원하지 않는다.

**SQL 표준 호환성**

<a id="c6bf78c2f72a7d63"></a>
| Feature ID | 설명 | 비고 |
| --- | --- | --- |
| P002 | Computational completeness | P004, P008을 지원하지 않는다. |
| P004 | Extended CASE statement | - |
| P008 | Comma-separated predicates in simple CASE statement | - |

<a id="c59c992edb95f702"></a>
## CLOSE Statement

<a id="9fd5781f7405d812"></a>
### 기능

Open 상태인 cursor를 닫는다.

<a id="fa447d9112ecf4b4"></a>
### 구문

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="0e303cb97ac4e53b"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="87e51fd51e119c0b"></a>
### 구문 규칙 및 파라미터

- cursor_name
    - Close 할 cursor의 이름이다.

<a id="3f6e67fba3c0bd2e"></a>
### 설명

Open 상태인 cursor를 닫는다.  
Close 된 상태인 cursor는 open 구문을 사용하여 다시 open 할 수 있다.

<a id="35e64afed58d222f"></a>
### 사용 예

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

<a id="8c6d206c3d83c54d"></a>
### 호환성

표준 SQL에 정의되어 있지 않다.

<a id="d4428715f4658de8"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [FETCH Statement](#2be71b2c548c858e)
- [OPEN Statement](#80c65120562ef0bf)

<a id="f66d6875e2355066"></a>
## Collection Method Invocation

<a id="72ed309ecb49c7a9"></a>
### 기능

Collection type의 변수를 탐색할 수 있는 method를 제공한다.

<a id="bfd11407ba947431"></a>
### 구문

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

<a id="1c7bce5776104568"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="257de46b8daba427"></a>
### 구문 규칙 및 파라미터

- Collection type으로 선언된 변수에만 사용할 수 있다.
- FIRST, LAST, COUNT는 parameter를 가질 수 없다.
- PRIOR, NEXT, EXISTS, DELETE와 같이 대상을 지정해야 할 경우에는 parameter를 명시해야 한다.
- DELETE의 경우에는 PSM statement와 같이 동작하며 다른 변수로 결과를 반환할 수 없다. (Expression에 사용할 수 없다.)

<a id="62c7878946a8a5e9"></a>
### 설명

다음 표를 참조한다.

**함수**

<a id="42ee9e0891a0f983"></a>
| 함수명 | 기능 | 반환값 | 인자 필요여부 |
| --- | --- | --- | --- |
| FIRST | 가장 작은 key를 반환한다. | INDEX OF에 지정된 key type | X |
| LAST | 가장 큰 key를 반환한다. | INDEX OF에 지정된 key type | X |
| PRIOR | 입력된 key보다 작은 key를 반환한다. | INDEX OF에 지정된 key type | O |
| NEXT | 입력된 key보다 큰 key를 반환한다. | INDEX OF에 지정된 key type | O |
| COUNT | 저장된 개수를 반환한다. | INTEGER | X |
| DELETE | Key에 해당하는 값을 삭제한다. | N/A | O |
| EXISTS | Key의 존재 유무를 반환한다. | BOOLEAN | O |

<a id="1a491001e9b2cc9a"></a>
### 사용 예

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

<a id="3b6784af32b2b486"></a>
### 참조

자세한 내용은 [COLLECTION Variable Declaration](#a4387f0fa0f4d9b3)을 참조한다.

<a id="a4387f0fa0f4d9b3"></a>
## COLLECTION Variable Declaration

<a id="c4e69e0a4af5a026"></a>
### 기능

Collection 변수를 선언한다.

<a id="f7862c22cb3a1bb2"></a>
### 구문

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

<a id="1669deaa6f0635ae"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 declaration 영역에서만 사용할 수 있다.

<a id="2f92e29c7bddc173"></a>
### 구문 규칙 및 파라미터

- Type-name
    - 사용자가 사용할 collection type의 이름을 지정한다. 
- Element-type
    - Collection 변수에 저장될 element의 type을 지정한다. 
- Index-type
    - Collection 변수에 저장된 key의 data type을 지정한다.

<a id="49d4a0cd88cca792"></a>
### 설명

Collection type을 선언한다.

<a id="2676a3bf6eac079a"></a>
### 사용 예

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

<a id="457bc413da7e34bb"></a>
### 호환성

SQL 표준에서는 정의하지 않고 있다.

<a id="776de061b238a08d"></a>
### 참조

자세한 내용은 [Collection Method Invocation](#f66d6875e2355066)을 참조한다.

<a id="35f5b1376cc629d4"></a>
## CONTINUE Statement

<a id="4cb7d13bcc7bb632"></a>
### 기능

현재 진행 중인 statement list의 수행을 중지하고, 상위 loop statement의 다음 iteration을 수행한다.

<a id="0327e11460f71840"></a>
### 구문

```
<continue statement> ::=
    CONTINUE [ label_name ] [ WHEN condition ] 
    ;
```

<a id="9678f394932c851d"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

Target label을 가진 statement는 다음 loop 계열 statement 중 하나이어야 한다.  

• basic loop statement  
• for loop statement  
• while statement  
• forall statement

<a id="20d95d54dcd3c6f4"></a>
### 구문 규칙 및 파라미터

- Label name
    - identifier chain의 형식을 가질 수 있다.
- Condition
    - 명시된 경우, 해당 조건이 TRUE일 때만 loop statement로 복귀한다.

<a id="884f01f7e8ba3eaf"></a>
### 설명

현재 진행 중인 statement list의 수행을 중지하고 상위 loop statement로 복귀한다.

Label이 명시되면 해당 label 이름을 가진 상위 loop statement로 복귀한다.  
Label이 명시되어 있지 않으면 가장 가까운 상위 loop statement로 복귀한다.  
같은 label 이름을 가진 여러 개의 상위 statement들이 존재할 경우, 가장 가까운 statement가 선택된다.  
현재 위치에서 visible한 (중첩된 scope 내에 존재하는) loop statement로만 복귀할 수 있다.

조건이 명시되면 해당 조건이 TRUE인 경우에만 복귀한다.  
조건이 명시되지 않으면 무조건 복귀한다.

<a id="97ff86068331a523"></a>
### 사용 예

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

<a id="b3f2d1957d992c96"></a>
### 호환성

&lt;continue statement&gt; 구문은 SQL 표준의 &lt;iterate statement&gt;와 기능이 유사하다.  
단, &lt;iterate statement&gt; 구문은 WHEN condition 기능은 제공하지 않는다.

<a id="570430c0a5ab5501"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [EXIT Statement](#46c4e6cb4d956122)
- [GOTO Statement](#b8ae5382c6d22723)

<a id="eef32c75f82eb81f"></a>
## Cursor FOR LOOP Statement

<a id="29655d4f3a736ecb"></a>
### 기능

PSM에서 사용자가 선언한 cursor나 query에 의해 생성된 result의 row 개수만큼 loop를 수행한다.

<a id="5ffdbd9f85164fb2"></a>
### 구문

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

<a id="df09298de01cfc04"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PSM 내의 body에서만 사용할 수 있다.

<a id="7deb67303c5d88f9"></a>
### 구문 규칙 및 파라미터

For~Loop 내에 선언된 변수는 해당 loop scope 내에서만 유효하다. (해당 Cursor For Loop Block Scope 밖에서는 해당 변수를 참조할 수 없다.)

<a id="7f0a5b76c2150692"></a>
#### Cursor Name을 사용한 경우

Cursor name을 사용하여 LOOP를 수행할 경우 cursor가 미리 선언되어 있어야 한다.   
Actual param에 대한 자세한 내용은 [OPEN Statement](#80c65120562ef0bf)를 참조한다.

<a id="fa6e3952262809aa"></a>
#### Cursor Query를 사용한 경우

Select나 returning query와 같이 GOLDILOCKS 내부적으로 implicit cursor로 처리되는 질의만 수행할 수 있다.

<a id="ff8b9235eb384361"></a>
### 설명

Cursor가 생성한 결과 개수만큼 loop를 돌면서 loop 내의 PSM statements를 수행한다.   
LOOP 중에 cursor가 invalid한 상태가 (예: closed) 되면 더 이상 loop를 수행하지 않고 오류로 처리한다.   
explicit cursor name을 명시할 경우, 해당 cursor가 already opened이면 오류로 처리한다.

FOR LOOP 절에 명시된 cursor의 결과를 반환받는 변수는 자동으로 생성된다. (Cursor의 실행 결과에 의해 반환될 result set의 row type으로 생성된다.)   
다만, 사용자의 cursor query 결과 중 특정 테이블의 column이 아닌 select target expression에 대해 alias 등을 지정하지 않을 경우, 오류가 발생할 수 있다.

<a id="d71ccaddb86c0d4f"></a>
### 사용 예

<a id="6bd4a0ba1f0791a6"></a>
#### Explicit Cursor 사용

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

<a id="d7fae6d5625bea5b"></a>
#### Cursor Query 사용

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

<a id="7a1aca92b813724f"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Explicit Cursor Declaration and Definition](#38239d8f6bc69d14)
- [GOTO Statement](#b8ae5382c6d22723)
- [EXIT Statement](#46c4e6cb4d956122)

<a id="5c050768d81529dc"></a>
## Cursor Variable Declaration

<a id="9d744078e4bd6ac8"></a>
### 기능

PSM의 DECLARE section에서 cursor variable을 선언한다.

<a id="c03f6fd142c35eb5"></a>
### 구문

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

<a id="aebb603dbb2b4977"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PSM의 declaration 영역에서만 사용할 수 있다.

<a id="900714b60db6972f"></a>
### 구문 규칙 및 파라미터

Cursor 변수의 초기값 지정이나 assign은 cursor 변수 사이에서만 가능하다.

<a id="5b65d67162bbac36"></a>
### 설명

Cursor variable은 특정 cursor에 종속되지 않는 cursor를 가리키는 일종의 pointer 역할을 한다.

<a id="72082f9d17ed169c"></a>
### 사용 예

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

<a id="c93cfb2032f238ec"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [OPEN Statement](#80c65120562ef0bf)
- [FETCH Statement](#2be71b2c548c858e)
- [CLOSE Statement](#c59c992edb95f702)

<a id="b7ff64cf994a5599"></a>
## DELETE Statement Extension

<a id="f1eb5189a59c6360"></a>
### 기능

PSM의 record type 변수를 이용하여 RETURNING INTO 절에 결과를 저장할 수 있다.

<a id="93445ff80ddfd787"></a>
### 구문

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

<a id="cf95d91710159830"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PSM의 body 영역에서만 사용할 수 있다.

<a id="5c1074824fec6a1b"></a>
### 구문 규칙 및 파라미터

Returning Into를 통해 반환받을 변수의 타입이 record-type인 경우 다른 변수 타입과 섞어서 사용할 수 없다.

<a id="63d06b761f17491e"></a>
### 설명

PSM의 record type 변수를 이용하여 RETURNING INTO 절에 결과를 저장할 수 있다.

<a id="1ca691892fa9862f"></a>
### 사용 예

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

<a id="0c068916017dda77"></a>
### 참조

자세한 내용은 [데이터 삭제](../part-03-sql-manual/12-sql-languages.md#17f901533d85742b)를 참조한다.

<a id="9ff32551693259b1"></a>
## EXCEPTION_INIT Pragma

<a id="ad290a3a95eaf914"></a>
### 기능

사용자가 정의한 exception이 처리할 error code를 설정한다.

<a id="6a73ca58f4446d16"></a>
### 구문

```
< PRAGMA EXCEPTION_INIT > ::=
     PRAGMA EXCEPTION_INIT ( <Exception-Name>, <Internal-ErrorCode> ) 
     ;
```

<a id="138f3fd98b6ca6c2"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PSM의 declaration 영역에서만 사용할 수 있다

<a id="bb8151c731e4f5cd"></a>
### 구문 규칙 및 파라미터

Predefined exception은 argument로 사용되는 exception name에 사용할 수 없다. (predefined exception name은 선언할 수 없다.)    
동일한 PL BLOCK DECLARE 절에 argument로 사용되는 exception name이 반드시 미리 선언되어야 한다. (다른 BLOCK의 exception name 선언을 참조할 수 없다.)    
&lt;Internal-ErrorCode&gt;는 DB SYSTEM 내에 존재하는 내부 error code이어야 한다. (SUCCESS 코드는 설정할 수 없다.)

<a id="518d1fbeba630cb1"></a>
### 설명

사용자가 DB SYSTEM의 error code에 대응하는 exception name을 명시적으로 선언한다.

<a id="071e499d0bbeb342"></a>
### 사용 예

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

<a id="c6cc5bcd1afed364"></a>
### 호환성

Error code는 각 벤더마다 다르기 때문에 서로 호환되지 않는다.

<a id="97b47df93d28f0ba"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Exception Declaration](#9bf4ef42c50667c4)
- [Exception Handler](#086edc92697ae2b8)

<a id="9bf4ef42c50667c4"></a>
## Exception Declaration

<a id="192795eb58af72e1"></a>
### 기능

PL block 내의 exception name을 선언한다.

<a id="46c4bf5083283cea"></a>
### 구문

```
< Exception-Declaration Statement > ::=
     <Exception-Name>  EXCEPTION 
     ;
```

<a id="c7c7a8e5364c709f"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PSM의 declaration 영역에서만 사용할 수 있다.

<a id="5338bf5c11e226d5"></a>
### 구문 규칙 및 파라미터

Predefined exception name은 선언할 수 없다.   
동일한 SCOPE의 DECLARE 절에 중복으로 선언할 수 없다.

<a id="41a3c3fa7e1e299a"></a>
### 설명

사용자가 명시적으로 exception을 선언한다.

<a id="40628ce60df75a7f"></a>
### 사용 예

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

<a id="12df5f5815cee89d"></a>
### 호환성

표준 SQL의 exception 선언은 다음과 같지만 GOLDILOCKS는 위와 같은 구문을 지원한다.

```
<condition declaration> ::=
DECLARE <condition name> CONDITION [ FOR <sqlstate value> ]
```

<a id="475e0051841b7f78"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Exception Declaration](#9bf4ef42c50667c4)
- [EXCEPTION_INIT Pragma](#9ff32551693259b1)

<a id="086edc92697ae2b8"></a>
## Exception Handler

<a id="f5241a1630957f71"></a>
### 기능

PL/ SQL을 수행하는 중에 발생한 DB SYSTEM 상의 오류로 인한 암묵적 exception이나 사용자가 명시적으로 발생시킨 exception에 대해 정의된 동작을 수행한다.

<a id="42344a155d387240"></a>
### 구문

```
< Exception Handler Statement > ::=
       EXCEPTION < Exception_When_List >
       ;

< Exception_When_List > ::=
       WHEN < Exception_Name_List > THEN <excutable statement list>  [ WHEN OTHERS THEN <excutable statement list> ]

< Exception_Name_List > ::= 
        <Exception_Name> [ { OR <Exception_Name> }... ]
```

<a id="6d90ea9fbf120c5e"></a>
### 사용 범위 및 접근 권한

PL block 내에서 사용할 수 있다.

<a id="e414cf2a97f8a5e1"></a>
### 구문 규칙 및 파라미터

Predefined exception인 OTHERS는 OR을 사용하여 다른 exception name과 함께 기술할 수 없다.   
Predefined exception인 OTHERS는 exception handler에 중복으로 기술할 수 없으며 가장 마지막에 기술하여야 한다.

<a id="1bd93d192e6cca3e"></a>
### 설명

<a id="c46f05aaac692d81"></a>
#### Exception 유형

<a id="5996a5e361dcec0e"></a>
| Type | Definer | Has error | Has name | Raise implicitly | Raise explicitly |
| --- | --- | --- | --- | --- | --- |
| Predefined | System | Yes | Yes | Yes | Optionally |
| User-defined | User | If user assign | If user assign | No | Yes |

Predefined exception은 GOLDILOCKS에서 미리 지정한 exception name과 error code를 갖는다.   
그 외의 exception은 GOLDILOCKS 내부의 오류 코드 이름을 사용자가 predefined exception name과 다르게 설정하는 경우 (internally defined)와 별도의 error code를 지정하지 않고 exception name만 선언하는 경우 (user-defined)로 나누어진다.

<a id="b84232e49b7d220a"></a>
#### Predefined Exception

**Predefined exception 유형**

<a id="0a21cc2dd7c33668"></a>
| 이름 | 설명 |
| --- | --- |
| CASE_NOT_FOUND | CASE WHEN의 모든 조건에 맞지 않거나 ELSE 절이 정의되지 않았다. |
| DUP_VAL_ON_INDEX | INDEX duplicated 오류가 발생하였다. |
| INVALID_CURSOR | Cursor의 상태가 올바르지 않다. |
| INVALID_NUMBER | 숫자로 변환할 수 없다. |
| NO_DATA_FOUND | SELECT 문이 0 건의 데이터를 반환한다. |
| ROWTYPE_MISMATCH | 두 개의 RowType 변수의 필드 타입이 서로 다르다. |
| TOO_MANY_ROWS | 두 건 이상의 row를 반환한다. |
| VALUE_ERROR | Type mismatch, invalid casting 같은 error이다. |
| ZERO_DIVIDE | 0으로 나누기를 시도한다. |
| OTHERS | Predefined에 정의되지 않은 오류를 포함한다. |

<a id="a0196443bd5312c3"></a>
### 사용 예

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

<a id="d59d6d7c7d03414c"></a>
### 호환성

SQL 표준 문법을 지원하지 않는다.

<a id="2c05d341fdbfac2a"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [EXCEPTION_INIT Pragma](#9ff32551693259b1)
- [Exception Declaration](#9bf4ef42c50667c4)

<a id="527305bdfcd7c7ed"></a>
## EXECUTE IMMEDIATE Statement

<a id="0cf4aa1c77145408"></a>
### 기능

PSM 내에서 dynamic SQL을 실행한다.

<a id="1668197fab2b6dad"></a>
### 구문

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

<a id="c354b2ab1965b85a"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="5db4afe684088f72"></a>
### 구문 규칙 및 파라미터

<a id="e8ddc7e15ccd4e40"></a>
#### Dynamic SQL

- single_quote_string: Single quote (')로 묶인 SQL 문장이다. (double_quote_string은 PSM 내에서 변수로 인식된다.)
- PSM-variable: PSM에서 사용되는 변수 내에 저장된 SQL 문장이다.

다음은 수행하려는 SQL 문장 내에 quote를 사용하여 데이터를 표현하는 예이다.

```
EXECUTE IMMEDIATE 'INSERT INTO t1 VALUES ( ''Tom'' ) '; -- Tom 
EXECUTE IMMEDIATE 'INSERT INTO t1 VALUES ( ''Tom''''House'') '; -- Tom'House
EXECUTE IMMEDIATE 'INSERT INTO t1 VALUES ( ''''''Tom'') ';   -- 'Tom
EXECUTE IMMEDIATE 'INSERT INTO t1 VALUES ( CHR(39) || ''TOM'' ) '; -- 'Tom
```

Dynamic SQL 내의 사용자가 변수를 입력할 부분에는 ? 또는 :V1과 같은 표기 (marker)를 사용한다.  
Dynamic SQL 내에 기술되는 SQL 문장은 유효한 문장이어야 한다.

<a id="f9dee243f36dc073"></a>
#### INTO Clause

Dynamic SQL 수행 결과가 존재하고 marker를 통해 binding된 경우가 아닌 SQL 문의 처리 결과를 반환 받는 경우이다. (내부적으로 implicit cursor fetch 형태이다.)   
구문은 다음과 같다.

```
EXECUTE IMMEDIATE 'SELECT ... FROM .. WHERE ...';
EXECUTE IMMEDIATE 'INSERT ... RETURNING ...';
EXECUTE IMMEDIATE 'UPDATE ... RETURNING ...';
EXECUTE IMMEDIATE 'DELETE ... RETURNING ...';
```

<a id="24826422369abdda"></a>
#### USING Clause

Dynamic SQL에 입력 변수를 사용할 경우 그 개수만큼 USING (IN 생략 가능)절에 변수나 표현식을 나열한다.  
Dynamic SQL 수행 결과가 존재할 경우 결과 column의 개수만큼 USING OUT 절에 변수를 나열한다. (결과를 INTO 절로 반환하는 경우)  
USING OUT을 이용하여 다음 구문에 결과를 반환할 수 있다.

```
EXECUTE IMMEDIATE 'SELECT x, y, z INTO :v1, :v2, :v3 ...';
EXECUTE IMMEDIATE 'INSERT INTO ...  RETURNING C1, C2 INTO :V1, :V2';
EXECUTE IMMEDIATE 'UPDATE T1 SET .. RETURNING C1, C2 INTO :V1, :V2';
EXECUTE IMMEDIATE 'DELETE FROM ...  RETURNING C1, C2 INTO :V1, :V2';
```

<a id="43e897c4d769d11c"></a>
#### RETURNING Clause

INSERT/ UPDATE/ DELETE RETURNING INTO 구문이 dynamic SQL로 사용된 경우, GOLDILOCKS는 USING 절에 기술된 변수를 OUT mode로 binding하여 결과를 반환받을 수 있다.   
다른 DBMS와의 호환을 위해 RETURNING INTO 절로도 동일한 결과를 반환받을 수 있다.

<a id="c9f6abe26085c11c"></a>
#### 기타규칙

- DDL/ DCL은 어떤 BIND 절 (INTO, USING, RETURNING clause)도 사용할 수 없다. 
- INTO 절과 RETURNING INTO 절에는 OUT으로 쓰이기 때문에 별도의 bind type을 지정할 수 없으며 동시에 같이 사용할 수도 없다. 
- IN BIND type은 scalar type 변수만 사용할 수 있다. 
- OUT BIND type은 record type 변수를 사용할 수 있다. 하지만 scalar나 record 타입을 섞어서 동시에 나열할 수는 없다. 
- INTO 절과 USING OUT 또는 RETURNING INTO를 통해 결과를 나누어 받을 수 없다.

<a id="cef28e57d658aaad"></a>
### 설명

- Dynamic SQL이 결과를 INTO 절에 기술된 변수로 반환하는 경우 
    - 두 건 이상의 결과를 반환하는 질의는 TOO_MANY_ROWS exception을 발생시킨다. 
    - 결과가 0 건인 경우 NO_DATA_FOUND exception을 발생시킨다. 
- Dynamic SQL이 결과를 USING이나 RETURNING 절에 기술된 변수로 반환하는 경우 
    - ARRAY가 아닌 변수가 두 건 이상 반환되면 TOO_MANY_ROWS exception이 발생한다. 
    - 결과가 0 건이면 오류가 발생하지 않는다. 
- DDL/ DCL이 implicit cursor SQL%Attribute 변수들을 수행한 결과는 다음과 같다. 
    - SQL%ROWCOUNT = 0 
    - SQL%ISOPEN = FALSE
    - SQL%FOUND = FALSE 
    - SQL%NOTFOUND = TRUE 
- 그 외의 dynamic SQL은 해당 SQL 문의 처리 결과에 맞는 SQL%Attribute 값을 저장한다.

<a id="116b1ab848181986"></a>
### 사용 예

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

<a id="46c4e6cb4d956122"></a>
## EXIT Statement

<a id="42ce9494d801e6e1"></a>
### 기능

상위 loop statement들 중에서 주어진 label을 가진 loop statement를 탈출하여 그 다음 statement를 수행한다.

<a id="466c6a86efbe5210"></a>
### 구문

```
<exit statement> ::=
    EXIT [ label_name ] [ WHEN condition ]
    ;
```

<a id="4730576538d133f6"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="550f207a8fb6709a"></a>
### 구문 규칙 및 파라미터

- Label name
    - 탈출할 loop statement의 label 이름이다.
    - Identifier chain 형식을 가질 수 있다.
- Condition
    - 조건을 명시할 경우, 해당 조건이 TRUE일 경우에만 loop statement를 탈출한다.

<a id="8500e537585932fd"></a>
### 설명

- 현재 진행중인 statement list 수행을 중단하고 상위 loop statement를 탈출한다.
- Target label을 가진 statement는 다음 loop 계열 statement 중 하나이어야 한다.
    - basic loop statement
    - for loop statement
    - while statement
- Label이 명시된 경우, 해당 label 명을 가진 상위 loop statement를 탈출한다.
- Label이 명시되지 않은 경우, 가장 가까운 상위 loop statement를 탈출한다.
- 같은 label 명을 가지는 여러 개의 상위 statement들이 존재할 경우, 가장 가까운 statement를 선택한다.
- 현재 위치에서 visible 한 (중첩된 scope 내에 존재하는) loop statement만 탈출할 수 있다.

- 조건 (condition)이 명시된 경우, 해당 조건이 TRUE인 경우에만 탈출한다.
- 조건이 명시되지 않은 경우, 무조건 탈출한다.

<a id="ea410b4756914908"></a>
### 사용 예

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

<a id="e873cfb02ee3f1e5"></a>
### 호환성

SQL 표준에는 존재하지 않는다.

<a id="0a964560bfaa44d6"></a>
## Explicit Cursor Attribute

<a id="353ab102807ac36e"></a>
### 기능

PSM에서 정의된 cursor의 상태값을 반환한다.

<a id="3da4c48d75c9ec52"></a>
### 구문

```
<Explicit cursor attribute> ::=
    cursor_name '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="e96838f101335fea"></a>
### 사용 범위 및 접근 권한

PSM 내의 body 영역에서만 사용할 수 있다.

<a id="483179cb56f121e5"></a>
### 구문 규칙 및 파라미터

- Cursor_name
    - 상태값을 알고 싶은 커서의 이름이다.

<a id="60d2e6e180293bb3"></a>
### 설명

- 주어진 커서의 상태값을 반환한다. 
    - ISOPEN: 현재 커서가 OPEN 상태인지 여부이다.
    - FOUND: 최근 fetch에 의해 데이터가 반환되었는지 여부이다.
    - NOTFOUND: FOUND의 반대이다.
    - ROWCOUNT: 커서가 최근에 OPEN 된 후 fetch 한 record의 개수이다.
- 커서의 상태에 따라 다음과 같은 값을 반환한다.

**수행 시점에 따른 결과표**

<a id="164be47e7b65414c"></a>
| Attribute 이름 | OPEN 전 | OPEN 후 | FETCH 후 | CLOSE 후 |
| --- | --- | --- | --- | --- |
| ISOPEN | FALSE | TRUE | TRUE | FALSE |
| FOUND | NULL | NULL | TRUE/ FALSE | NULL |
| NOTFOUND | NULL | NULL | TRUE/ FALSE | NULL |
| ROWCOUNT | NULL | NULL | N (개수) | NULL |

<a id="af7b501479e15722"></a>
### 사용 예

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

<a id="f56f5a746efb749c"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="38239d8f6bc69d14"></a>
## Explicit Cursor Declaration and Definition

<a id="d5264f7b16ffa746"></a>
### 기능

PSM의 DECLARE section에서 커서를 선언한다.

<a id="8c03c3658d3d99a8"></a>
### 구문

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

<a id="acebc63cfd6e5d25"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function )   
PL block의 declaration 영역에서만 사용할 수 있다

<a id="996b62034b0797c7"></a>
### 구문 규칙 및 파라미터

<a id="bdbb475d19a8f43a"></a>
#### Cursor Name

선언할 커서의 이름이다.  
커서 이름의 길이는 128 바이트보다 작아야 한다.  
해당 scope 내에서 고유한 이름이어야 한다.

<a id="7fb4db71d56e8bff"></a>
#### RowType

커서의 레코드 타입을 정의한다.  
커서를 정의할 때 명시된 select target들의 개수가 같아야 하며, 데이터 타입이 호환되어야 한다.  
Rowtype을 지정하지 않을 경우, cursor를 정의할 때 기술된 select_statement의 SELECT target에 적합한 rowtype이 자동으로 지정된다.

<a id="6287943c2bec6146"></a>
#### Param Name

특정 커서 내에서 parameter를 구별하는 이름이다.  
해당 커서 내에서 고유한 이름이어야 한다.  
만일 참조 가능한 scope 내의 다른 변수와 이름이 같을 경우, 해당 커서의 parameter를 우선적으로 참조한다.

<a id="de4d3b5e05491f7d"></a>
#### DataType

해당 parameter의 데이터 타입을 지정한다.   
GOLDILOCKS에서 제공하는 모든 built-in 타입과 PSM 내에 정의된 타입을 사용할 수 있다.   
단, built-in 타입에는 범위를 제한하는 구문 (precision/ scale)을 지정할 수 없고 내부적으로 해당 데이터 타입의 최대 범위로 지정된다.

<a id="9040d4ab98441334"></a>
#### Cursor Query

- Cursor가 수행할 수 있는 query는 다음과 같다.
    - Select 구문
    - Select For Update 구문
    - Insert Returning 구문
    - Update Returning 구문
    - Delete Returning 구문
- SELECT INTO 구문은 사용할 수 없다.

<a id="a8acaacf49ce635c"></a>
### 설명

- &lt;explicit cursor declaration&gt; 구문은 커서를 선언하거나 정의한다.
    - cursor declaration: 커서의 이름과 포맷만 선언한다.
    - cursor definition: 커서의 이름, 포맷 및 수행할 SELECT 구문까지 상세하게 정의한다.
- explicit cursor는 declaration 후에 definition 하여 사용하거나, declaration 없이 바로 definition 하여 사용할 수 있다. 
- declaration 후 definition 하여 사용할 경우에는 커서의 이름, parameter spec, 레코드 타입 정의가 정확하게 일치해야 한다.
- explicit cursor의 declaration과 definition은 같은 block 내에 존재해야 한다.
- explicit cursor는 해당 cursor가 define 된 block에 진입할 때 생성되며 해당 block에서 나갈 때 자동으로 CLOSE 되고 삭제된다.
- 특정 시점에 생성할 수 있는 explicit cursor의 최대 개수는 'MAXIMUM_NAMED_CURSOR_COUNT' 프로퍼티에 의해 제한된다.
- explicit cursor가 수행하는 &lt;cursor query&gt;에는 다음 변수들을 사용할 수 있다.
    - 해당 cursor의 parameter
    - declare 시점의 scope에서 참조할 수 있는 모든 PSM 변수 (open 시점의 scope가 아님)
    - 외부 bind parameter (Anonymous PL block의 경우)
- 사용자가 지정한 &lt;cursor query&gt;를 수행하는 explicit cursor는 다음과 같은 속성을 갖는다.
    - IN_SENSITIVE (다른 트랜잭션에 의한 변경에 영향받지 않는다.)
    - NON_SCROLLABLE (이전 record를 다시 fetch 할 수 없다.)
    - READ_ONLY (Read 연산만 가능하다)
    - WITH-HOLD (COMMIT/ ROLLBACK이 수행되어도 cursor가 자동으로 닫히지 않는다.)

<a id="2a6a6265d8f8a81c"></a>
### 사용 예

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

<a id="72956f027ac8e7da"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="023431892154fc2e"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [OPEN FOR Statement](#eb4bf8bad6641506)
- [FETCH Statement](#2be71b2c548c858e)
- [CLOSE Statement](#c59c992edb95f702)

<a id="2be71b2c548c858e"></a>
## FETCH Statement

<a id="0ced0743e0d1c7ce"></a>
### 기능

OPEN 된 cursor의 레코드를 한 건 가져온다.

<a id="a5783b8673759eb2"></a>
### 구문

```
<fetch statement> ::=
    FETCH cursor_name <into clause>
    ;

<into clause> ::=
    INTO { variable [ , variable ] .. | record }
```

<a id="a84ef235c3c09fce"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="bc0d4c355efa7bb6"></a>
### 구문 규칙 및 파라미터

- Cursor name
    - Fetch 할 cursor name이다.
- Variable
    - Fetch한 결과 중에 한 개의 column 값을 저장할 scalar 타입의 변수 또는 bind parameter이다.
- Record
    - Fetch한 결과인 한 개의 레코드 전체를 저장할 record 타입의 변수이다.

<a id="e9c737ec19fd483f"></a>
### 설명

Open 된 커서로부터 레코드 한 개를 fetch하여 INTO 절에 명시된 변수로 값을 복사한다.   
만일 커서가 declaration만 되어 있고 definition 되어 있지 않으면 에러가 발생한다.  
해당 커서는 open 된 상태여야 한다.

INTO 절에 주어진 변수 타입은 fetch된 레코드 결과의 데이터 타입과 서로 호환 가능해야 한다.   
INTO 절에 주어진 변수들의 개수는 커서의 SELECT target 개수와 같아야 한다.   
단, INTO 절에 주어진 변수가 record type일 경우에는 한 개만 명시해야 한다.   
그리고 해당 record 변수의 field 개수는 SELECT target의 개수와 같아야 한다.

Fetch 할 레코드가 없는 상태에서 fetch가 호출되었을 경우, INTO 절의 target 변수 값은 변하지 않는다.

<a id="9e6e75f27c6d97f0"></a>
### 사용 예

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

<a id="ff41959e96e68580"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="5162730f87ad0492"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [OPEN Statement](#80c65120562ef0bf)
- [CLOSE Statement](#c59c992edb95f702)

<a id="a6f1fcb87e2ef564"></a>
## FOR LOOP Statement

<a id="7c89f9a7d32f0216"></a>
### 기능

Index 변수가 주어진 값 범위를 가지는 동안 index 변수를 1씩 증가시키거나 감소시키면서 (REVERSE)   
내부의 statement들을 수행한다.

<a id="abf57afd3abe9727"></a>
### 구문

```
<for loop statement> ::=
    FOR index_variable_name IN [ REVERSE ] lower_bound .. upper_bound
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="72aef8620376b33e"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="2a5d3c42ffc9ebb3"></a>
### 구문 규칙 및 파라미터

- Index variable name
    - FOR 구문에서 index로 사용할 변수의 이름이며 내부적으로 NATIVE_BIGINT 타입의 변수가 사용된다.
- Lower bound
    - 정수형이어야 하며, 만일 부동 소수점을 가진 숫자를 사용할 경우, 타입 변환 중에 소수점 이하는 반올림한다.
- Upper bound
    - 정수형이어야 하며, 만일 부동 소수점을 가진 숫자를 사용할 경우, 타입 변환 중에 소수점 이하는 반올림한다.

<a id="8b3418391ae56130"></a>
### 설명

for loop 구문은 index 변수의 값을 증가시키거나 감소시키면서 내부의 statement list를 수행한다.

- REVERSE를 명시한 경우
    - index 변수는 upper_bound 값으로부터 1씩 감소하고, index 변수의 값이 lower_bound보다 작아지게 되면 for loop statement의 실행을 종료한다.
    - upper_bound 값이 lower_bound 값보다 작으면 내부의 statement list는 수행되지 않는다.
- REVERSE를 명시하지 않은 경우
    - index 변수는 lower_bound 값으로부터 1씩 증가하고, index 변수의 값이 upper_bound보다 커지게 되면 for loop statement의 실행을 종료한다.
    - lower_bound 값이 upper_bound 값보다 크면 내부의 statement list는 수행되지 않는다.

<a id="fa590bdebc9de001"></a>
### 사용 예

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

<a id="4e753424a8b87a53"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="bf8a82cce0cad5b1"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CONTINUE Statement](#35f5b1376cc629d4)
- [EXIT Statement](#46c4e6cb4d956122)
- [GOTO Statement](#b8ae5382c6d22723)

<a id="2a34bffbc503ec12"></a>
## Function Declaration and Definition

<a id="d32d754cb3f36394"></a>
### 기능

Function을 선언하고 정의한다.

<a id="ff87aab9c4b6d1bf"></a>
### 구문

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

<a id="77e4c625a571d7c5"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 declaration 영역에서만 사용할 수 있다.

<a id="4056e3fb4d673dff"></a>
### 구문 규칙 및 파라미터

<a id="05d24e2ecc1832c5"></a>
#### function name

PL block 내에 생성할 function의 이름으로써 PL block 내에서 고유한 이름이어야 한다.  
즉, PL block에 선언한 PL item과 function은 동일한 이름을 가질 수 없다.  
Function 이름의 길이는 128 바이트보다 작아야 한다.

<a id="61db56a50c3e7680"></a>
#### parameter name

Function의 parameter 이름을 정의한다.  
각 parameter는 function 내에서 고유한 이름을 가진다.  
즉, function의 parameter와 PL item은 동일한 이름을 가질 수 없다.  
Parameter 이름의 길이는 128 바이트보다 작아야 한다.  
하나의 function에서 사용할 수 있는 parameter의 최대 개수에는 제한이 없다.

<a id="01b825bc838a4229"></a>
#### parameter mode

각 parameter mode를 설정한다.  
Parameter mode에는 IN, OUT, IN OUT이 있다.  
Parameter mode를 명시하지 않을 경우, 기본 mode는 IN이다.

<a id="4a28272a64f0bdd2"></a>
#### parameter default

Parameter의 기본값이다.  
Parameter default가 명시된 parameter는 function을 실행할 때 생략할 수 있다.  
Parameter를 명시하지 않고 생략할 경우, parameter를 정의할 때 명시한 &lt;value expression&gt;을 기본값으로 가진다.  
&lt;value expression&gt;의 datatype은 parameter의 datatype이어야 한다.  
&lt;parameter default&gt;를 가진 parameter 이후에 정의되는 모든 parameter에는 &lt;parameter default&gt;가 있어야 한다.

<a id="b6f5bf9a4f38055b"></a>
#### return clause

Function의 반환 형태를 정의한다.   
&lt;return clause&gt;에서는 다음과 같이 정의된다.

- RETURN &lt;datatype&gt;
    - Function에서 반환하는 반환값의 datatype을 정의한다.
- RETURN TABLE ( &lt;table function column list&gt; )
    - 반환하는 결과 집합의 table type을 정의한다.

<a id="5d90a4fb05db8db2"></a>
#### table function column list

Table function이 반환하는 결과 집합의 column 이름이다.   
Column 이름의 길이는 128 바이트보다 작아야 한다.  
Column 개수에는 제한이 없다.  
각 column 이름은 &lt;table function column list&gt;에서 고유하다.  
Column 이름은 parameter 및 declare item 이름과 동일할 수 있다.  
&lt;table function column list&gt;에 정의된 column은 function의 PL block 내에서 참조할 수 없다.

<a id="2d7a39081a2230f9"></a>
#### function characteristics

&lt;function characteristics&gt;은 function의 특성을 명시한다.  
동일한 특성에 대해서 중복은 허용하지 않는다.  
자세한 설명은 [Routine Characteristics](#904f272f8d216420) 를 참고한다.

<a id="21c29ada5fc47b76"></a>
#### routine body

- SQL body
    - 자세한 설명은 [Block (BEGIN .. END)](#b5f1979bc247ce01)을 참조한다.
- external body
    - 자세한 설명은 [Call Specification](#1663813aaf9c3eb4)을 참조한다.

<a id="9e1b56e9c4a04d03"></a>
### 설명

Function은 다음과 같이 선언하고 정의한다.

- PL block (예 : anonymous block, procedure 및 function의 block, block statement의 block )
    - PL block의 item 중 하나로써 function을 선언하고 정의한다.
    - PL block에 선언 및 정의된 function을 nested function이라고 한다.
    - Nested function은 PL block 범위 내에서만 사용할 수 있다.
- Package specification
    - Package의 public function을 선언한다.
    - Package의 public function은 database 내에서 사용할 수 있다.
- Package body
    - Package specification에 선언된 public function을 정의한다.
    - Package의 private function을 선언하고 정의한다.
    - Package의 private function은 package 범위 내에서만 사용할 수 있다.

Function의 사용 방법은 schema-level function과 동일하다.

<a id="d309b1a8e629ae64"></a>
### 사용 예

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

<a id="c3bcd992ae91f552"></a>
### 호환성

Schema-level function과 동일하다.

<a id="35935e4aed9680bf"></a>
### 참조

자세한 내용은 [CREATE FUNCTION](31-psm-sql-references.md#8f6d3c41338c889a)을 참조한다.

<a id="b8ae5382c6d22723"></a>
## GOTO Statement

<a id="1a5fee7415fe86bb"></a>
### 기능

현재 위치에서 접근 가능한 statement들 중에 주어진 label을 가진 가장 가까운 statement로 jump를 시도한다.

<a id="ed2cf4df7668bdb5"></a>
### 구문

```
<goto statement> ::=
    GOTO label_name
    ;
```

<a id="df199a3c58bad0bd"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="f2ac24b3cd431085"></a>
### 구문 규칙 및 파라미터

- Label_name
    - Jump를 시도할 statement의 label 이름이다.
    - Identifier chain 형식을 가질 수 있다.

<a id="10918106bb967bf2"></a>
### 설명

해당 label 이름을 가진 statement로 jump하여 수행을 시작한다.  
여러 개의 후보 statement들이 존재할 경우, 가장 가까운 statement로 jump한다.  
현재 위치에서 visible 한 (중첩된 scope 내에 존재하는) statement로만 jump 할 수 있다.  
Forward jump와 backward jump 모두 가능하다.

<a id="5953238732e9c98e"></a>
### 사용 예

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

<a id="2762daf26fcb1e2c"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="ffe35cc5b0a66d77"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [EXIT Statement](#46c4e6cb4d956122)
- [CONTINUE Statement](#35f5b1376cc629d4)

<a id="31f7c6e0b61ab3c0"></a>
## IF Statement

<a id="cfff365b9dbc628d"></a>
### 기능

주어진 여러 조건들 중에 TRUE를 반환하는 조건에 해당하는 statement list를 수행한다.

<a id="9aa4599b53ab9c4d"></a>
### 구문

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

<a id="0b0a6640dada69d1"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 body 영역에서만 사용할 수 있다.

<a id="d8a8e2d7f0e7c9c4"></a>
### 구문 규칙 및 파라미터

- Search condition
    - boolean 타입으로 최종 평가될 수 있는 표현식이다.
- Executable statement list
    - GOLDILOCKS PSM에서 지원하는 모든 statement 들의 list 이다.

<a id="86a2c4d1b34d0d49"></a>
### 설명

CASE 구문과 유사하게 조건들을 평가하여 TRUE를 반환하는 IF, ELSIF 절의 statement list를 수행한다.   
모든 조건들을 만족시키지 못하고 &lt;if statement else clause&gt;가 존재할 경우에는 해당 구문을 수행한다.   
ELSIF 구문들은 순서대로 먼저 나오는 조건식부터 평가하여 해당 조건식이 TRUE인 경우 그 이후의 조건식들은 평가하지 않는다

<a id="07f1b3b6feb4771a"></a>
### 사용 예

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

<a id="6dd874034c1dd2ff"></a>
### 호환성

&lt;if statement&gt; 구문은 SQL 표준과 구문이 같고 동일하게 동작한다.

**SQL 표준 호환성**

<a id="220f6fb500eaf670"></a>
| Feature ID | 설명 | 지원여부 |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="e02399b5355c89ce"></a>
## Implicit Cursor Attribute

<a id="09097c57efca6c31"></a>
### 기능

PSM에서 정의된 implicit cursor의 상태값을 반환한다.

<a id="255ca00e57f5b83a"></a>
### 구문

```
<Implict cursor attribute> ::=
    SQL '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="bc5e8dc5dac8136a"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="9abbb47e942d0a60"></a>
### 설명

- 직전에 수행된 SQL 문의 결과를 저장한다.
    - ISOPEN: 현재 커서가 OPEN 상태인지 여부로써 항상 FALSE로 설정된다.
    - FOUND: 직전 SQL 결과에 의해 데이터가 반환 되었는지 여부이다.
    - NOTFOUND: FOUND의 반대이다.
    - ROWCOUNT: 직전 SQL결과에 영향받은 record의 개수이다.

<a id="ef3883e8000da341"></a>
### 사용 예

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

<a id="a570fc78cfeb469a"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="bad4432950ae600a"></a>
## INSERT Statement Extension

<a id="b099574d25c9bc34"></a>
### 기능

PSM에서 지원하는 record-type 변수를 VALUES 절에 기술하여 데이터를 입력할 수 있도록 insert statement를 확장한 기능이다.

<a id="75afe999f2bd6d9f"></a>
### 구문

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

<a id="a53677c6749728ae"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 body 영역에서만 사용할 수 있다.  
EXECUTE IMMEDIATE의 원본 SQL 문에는 PSM insert extension 구문을 사용할 수 없다.

<a id="9d721d7b2a48d52e"></a>
### 구문 규칙 및 파라미터

Insert statement의 기본 구문과 동일하게 동작한다. 다만, value item에 기존의 value expression을 괄호에 묶어 연속으로 나열하는 방법 외에 PSM record type 변수를 기술하는 기능이 추가되었다.

Value_Item에 괄호 없이 변수를 사용할 경우 반드시 PSM record type의 변수를 기술해야 한다.  
Insert extension 구문 형태로 사용할 경우 record type이 아닌 변수를 섞어서 사용할 수 없다.

<a id="d8adbe13d790d005"></a>
### 설명

일반적인 insert statement 외에 PSM의 record type 변수를 이용하여 record를 저장하거나 returning into를 통해 결과를 받아 온다.   
Insert에 대한 자세한 내용은 다음 예를 참조한다.

<a id="17b4cb1fa12695db"></a>
### 사용 예

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

<a id="c95e01404d138eb2"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="b4fbf41981dfde9d"></a>
## INSERT INTO ... UPDATE Statement Extension

<a id="c5f4530f8d37b9cf"></a>
### 기능

Insert into .. update statement에서 확장된 기능이다. PSM에서 지원하는 record type 변수를 values clause에 기술하여 테이블에 새로운 row를 생성하거나, set clause에 기술하여 row를 갱신한다.

<a id="457896f9179b56c2"></a>
### 구문

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

<a id="0e8c66f328ab30ef"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: procedure, function, package )  
PL block의 body 영역에서만 사용할 수 있다.

<a id="4c8efbb858476c00"></a>
### 구문 규칙 및 파라미터

- &lt;values clause&gt;
    - Value item에 기존의 value expression을 괄호로 묶어 연속으로 나열하는 방법 외에 PSM record type 변수를 기술하는 기능이 추가되었다.
    - Value item에 괄호 없이 변수를 사용할 경우 반드시 PSM record type의 변수를 기술해야 한다.
    - Value item을 확장하여 작성할 경우, record type이 아닌 변수를 섞어서 사용할 수 없다.
- &lt;target list&gt; 
    - SET ROW 구문에서 사용하는 &lt;PSM_Variable&gt;은 반드시 record type으로 선언된 변수여야 한다.
- &lt;returning into clause&gt;
    - RETURNING INTO 구문에서 사용할 &lt;Variable&gt;은 record type이 아니어도 된다. 단, record type으로 기술한 경우 다른 데이터 타입의 변수와 섞어서 사용하거나 두 개 이상의 record type 변수를 나열할 수 없다.

<a id="474c75ab232c254e"></a>
### 설명

Upsert statement의 returning into 구문은 insert가 수행되면 insert 된 결과를 저장하고, update가 수행되면 update 된 결과를 저장한다.

<a id="c32137e425434370"></a>
### 사용 예

- insert 수행

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

- update 수행

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

- insert 수행 시 returning 구문

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

- update 수행 시 returning 구문

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

<a id="1f934469443a55b8"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="85537b9e6eef66cf"></a>
## Merge Statement Extension

<a id="eff8f1cbdb5a7121"></a>
### 기능

Merge Statement를 확장한 기능으로 PSM에서 지원하는 변수들을 활용하여 테이블의 레코드를 조건에 맞게 insert, update 또는 delete 한다.

<a id="26f7fe308d974a4d"></a>
### 구문

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

<a id="c7e100aa8c739bf4"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="fcae6899e92289cd"></a>
### 구문 규칙 및 파라미터

기본적으로 Merge Statement의 구문의 규칙과 동일하지만 아래 사항이 추가되었다.

- &lt;merge update&gt;
    - UPDATE SET ROW 구문에서 PSM record type variable을 사용하여 row 단위로 업데이트 가능하다.
- &lt;merge insert&gt;
    - INSERT VALUES 에서 괄호 없이 변수를 사용하는 경우, PSM record type variable를 기술하여 데이터를 삽입한다.

<a id="df68d8e82fca85d1"></a>
### 설명

PSM에서 지원하는 record type variable을 사용할 수 있도록 merge statement를 확장한 구문이다.  
자세한 내용은 [Merge Statement](../part-03-sql-manual/20-sql-references-h-z.md#bc136bf193bf403b)를 참조한다.

<a id="26592ae9325f7fdc"></a>
### 사용 예

- PSM에서 지원하는 record type variable을 사용하는 merge 구문의 예

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

<a id="5b568d569cbfa6b5"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="9fc84cbdae0a92d9"></a>
## NULL Statement

<a id="7d6c622afe9400c0"></a>
### 기능

아무 기능도 없는 statement 이다.

<a id="26c952bd6380543f"></a>
### 구문

```
<null statement> ::=
    NULL
    ;
```

<a id="ee57a0eef2496274"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="e3ce980f16b84639"></a>
### 설명

아무 기능도 하지 않는 statement이며, 주로 특정 위치의 label을 설정하기 위해 사용된다.

<a id="010330b6ce4ce0e5"></a>
### 사용 예

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

<a id="f4570d746e0f58ee"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="80c65120562ef0bf"></a>
## OPEN Statement

<a id="06273868f0f3fa85"></a>
### 기능

PSM에서 정의된 cursor의 SELECT 구문을 실행한다.

<a id="1a53d4ca44dbdaf4"></a>
### 구문

```
<open statement> ::=
    OPEN cursor_name [ <actual param spec> ]
    ;

<actual param spec> ::=
      ( expression [ , expression ] .. )
```

<a id="7be11af70af6725b"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="1f8e0befc84e6778"></a>
### 구문 규칙 및 파라미터

- Cursor_name
    - Open할 커서의 이름이다.

<a id="1b8176c21b0dafe2"></a>
### 설명

정의된 커서의 SELECT 또는 SELECT ... FOR UPDATE 구문을 실행한다.  
만일 커서가 declaration만 되어 있고 definition 되어 있지 않을 경우, 에러가 발생한다.   
Actual parameter의 값들은 해당 parameter의 데이터 타입과 서로 호환 가능해야 한다.

Actual parameter의 개수는 커서의 parameter 개수와 같아야 한다.  
만일 커서의 parameter 개수보다 적을 경우, 나머지 모든 parameter들에 default 값이 명시되어야 한다.

<a id="15809cee974ea734"></a>
### 사용 예

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

<a id="e0e2cab42201f457"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="33789d8d6c45644e"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CLOSE Statement](#c59c992edb95f702)
- [FETCH Statement](#2be71b2c548c858e)

<a id="eb4bf8bad6641506"></a>
## OPEN FOR Statement

<a id="9a56d4fe776c27da"></a>
### 기능

PSM에서 정의된 cursor 변수를 통해 SELECT 구문을 실행하여 한 개의 cursor를 open한다.

<a id="104aa1dcb9a76ecf"></a>
### 구문

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

<a id="a56666968d1b07b7"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="4737ce38d48e55ad"></a>
### 구문 규칙 및 파라미터

- &lt;cursor_variable_name&gt;
    - cursor variable의 이름이다.
- &lt;cursor_query&gt;
    - cursor query는 static cursor query와 dynamic cursor query 모두 사용할 수 있다.
    - cursor query는 다음과 같은 구문이 가능하다.
        - select 구문
        - select for update 구문
        - insert returning 구문
        - update returning 구문
        - delete returning 구문
    - Dynamic cursor query는 single quote (')로 sql을 묶거나 psm variable에 sql을 저장하여 사용한다.
    - Dynamic cursor query로 작성할 때 using 절을 사용할 수 있다.
- &lt;using_clause&gt;
    - Dynamic cursor query를 작성할 때 bind variable이 있을 경우, bind variable의 개수만큼 using 절에 variable이나 expression을 나열한다.
    - Using 절의 variable은 IN/ OUT/ IN OUT의 bind type을 명시할 수 있다. Dynamic cursor query를 작성할 때 bind type은 bind variable의 bind type과 일치해야 한다.
    - Using 절의 variable의 bind type은 생략할 수 있는데 생략할 경우 default bind type은 IN이다.

<a id="95cbd184181d4d81"></a>
### 설명

정의된 cursor variable의 cursor query를 실행한다.   
만일 cursor variable이 이전에 open 된 상태라면 자동으로 close 한 후에 reopen 하여 실행한다.

<a id="2d33760463acb5ef"></a>
### 사용 예

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

- Dynamic Cursor Query와 Using Clause

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

<a id="eb01812f0dc465c0"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="187099f356f0d22c"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Cursor Variable Declaration](#5c050768d81529dc)
- [FETCH Statement](#2be71b2c548c858e)
- [CLOSE Statement](#c59c992edb95f702)

<a id="b7f71090c8dcbf03"></a>
## Procedure Call

<a id="3aa3f10ba3e53c15"></a>
### 기능

사용자 정의 procedure, built-in procedure 또는 nested procedure를 호출한다.

<a id="a5c330d7671f4f99"></a>
### 구문

```
<Procedure call> ::=
    proc_name [ ( expr { , expr } ... ) ]
    ;
```

<a id="fc8f651733c38f06"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

- 사용자 정의 procedure를 호출할 경우, 해당 procedure에 대한 다음 권한 중 하나가 있어야 한다.
    - EXECUTE PROCEDURE
    - Procedure가 속한 스키마에 대해 (EXECUTE PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
    - EXECUTE ANY PROCEDURE ON DATABASE

<a id="76790bc902875e5a"></a>
### 구문 규칙 및 파라미터

- Proc_name 
    - 실행할 procedure의 이름으로써 다음과 같은 형태로 사용할 수 있다.

<a id="557b91b6bb5725ab"></a>
<table class="table column_count_3"><caption></caption><thead><tr><th class="to_center"><div>형태</div></th><th class="to_center"><div>구문</div></th><th class="to_center"><div>설명</div></th></tr></thead><tbody><tr><td class="to_left to_middle"><div>단일 identifier</div></td><td class="to_middle"><div>procedure_name</div></td><td><div>주어진 이름의 procedure를 호출한다.

검색 순서는 다음과 같다.
1. nested procedure
2. schema-level procedure</div></td></tr><tr><td class="to_left to_middle" rowspan="3"><div>identifier chain</div></td><td><div>label_name.procedure_name</div></td><td><div>nested procedure를 호출한다.</div></td></tr><tr><td><div>schema_name.procedure_name</div></td><td><div>schema-level procedure를 호출한다.</div></td></tr><tr><td><div>package_name.procedure_name</div></td><td><div>built-in procedure를 호출한다.</div></td></tr></tbody></table>

주어진 이름 (proc_name)으로 검색하여 최초로 발견된 procedure에 주어진 인자와 개수 및 타입이 적절하지 않으면 다른 procedure를 찾지 않고 에러를 발생시킨다.

<a id="ceb7f0212c91b825"></a>
### 설명

이전에 정의된 사용자 정의 procedure, built-in procedure 또는 nested procedure를 호출한다.   
호출할 때 default 값이 정의된 인자 값은 생략할 수 있다.

OUT이나 IN-OUT으로 지정된 인자에 procedure 변수나 bind parameter (?, :V1 등)를 사용하면 반환된 값을 얻을 수 있다.

<a id="17a4f56b04117fc5"></a>
### 사용 예

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

<a id="8851ccf46858eba5"></a>
### 호환성

SQL 표준에는 &lt;call statement&gt;를 사용하도록 되어 있다.

<a id="b5a477999d1596c4"></a>
## Procedure Declaration and Definition

<a id="aec4148f793f9164"></a>
### 기능

Procedure를 선언하고 정의한다.

<a id="b887260d49d2eb56"></a>
### 구문

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

<a id="1ca4487e4b8b3672"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 declaration 영역에서만 사용할 수 있다.

<a id="91beecbf262cc5be"></a>
### 구문 규칙 및 파라미터

<a id="f9b59aa9c640d05f"></a>
#### procedure name

PL block 내에 생성할 procedure의 이름으로써 PL block 내에서 고유한 이름이어야 한다.  
즉, PL block에 선언한 PL Item과 procedure은 동일한 이름을 가질 수 없다.  
Procedure 이름의 길이는 128 바이트보다 작아야 한다.

<a id="decef132b4e51a68"></a>
#### parameter name

Procedure의 parameter 이름을 정의한다.  
각 parameter는 procedure 내에서 고유한 이름을 가진다.  
즉, procedure의 parameter와 PL item은 동일한 이름을 가질 수 없다.  
Parameter 이름의 길이는 128 바이트보다 작아야 한다.  
하나의 procedure에서 사용할 수 있는 parameter의 최대 개수에는 제한이 없다.

<a id="bde5e0c01b9f8fae"></a>
#### parameter mode

각 parameter mode를 설정한다.  
Parameter mode에는 IN, OUT, IN OUT이 있다.  
Parameter mode를 명시하지 않을 경우, 기본 mode는 IN이다.

<a id="37ce59290eefe3cd"></a>
#### parameter default

Parameter의 기본값이다.  
Parameter default가 명시된 parameter는 procedure 실행할 때 생략할 수 있다.  
Parameter를 명시하지 않고 생략할 경우, parameter를 정의할 때 명시한 &lt;value expression&gt;을 기본값으로 가진다.  
&lt;value expression&gt;의 datatype은 parameter의 datatype이어야 한다.  
&lt;parameter default&gt;를 가진 parameter 이후에 정의되는 모든 parameter에는 모두 &lt;parameter default&gt;가 있어야 한다.

<a id="d7dc1bdf81322f10"></a>
#### procedure characteristics

&lt;procedure characteristics&gt;은 procedure의 특성을 명시한다.  
동일한 특성에 대해서 중복은 허용하지 않는다.  
자세한 설명은 [Routine Characteristics](#904f272f8d216420)를 참고한다.

<a id="9dffa1439b954958"></a>
#### routine body

- &lt;SQL body&gt;
    - 자세한 설명은 [Block (BEGIN .. END)](#b5f1979bc247ce01)을 참고한다.
- &lt;external body&gt;
    - 자세한 설명은 [Call Specification](#1663813aaf9c3eb4)을 참고한다.

<a id="c1e8cbaf5488991b"></a>
### 설명

Procedure는 다음과 같이 선언하고 정의한다.

- PL block (예 : anonymous block, procedure 및 function의 block, block statement의 block)
    - PL block의 item 중 하나로써 procedure를 선언하고 정의한다.
    - PL block에 선언 및 정의된 procedure를 nested procedure라고 한다.
    - Nested procedure는 PL block 범위 내에서만 사용할 수 있다.
- Package specification
    - Package의 public procedure를 선언한다.
    - Package의 public procedure는 database 내에서 사용할 수 있다.
- Package body
    - Package specification에 선언된 public procedure를 정의한다.
    - Package의 private procedure를 선언하고 정의한다.
    - Package의 private procedure는 package 범위 내에서만 사용할 수 있다.

Procedure의 사용 방법은 schema-level procedure와 동일하다.

<a id="0e091ff01b484a65"></a>
### 사용 예

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

<a id="4fbc3a9ef52dfc1a"></a>
### 호환성

Schema-level procedure와 동일하다.

<a id="86f79ce60e01d9a3"></a>
### 참조

자세한 내용은 [CREATE PROCEDURE](31-psm-sql-references.md#48b6178f1f6cd4cb)를 참조한다.

<a id="4f0dcdacbd73881e"></a>
## RAISE Statement

<a id="02c1f1daad2e0961"></a>
### 기능

사용자가 정의한 exception을 명시적으로 발생시킨다.

<a id="8f583fae6201051e"></a>
### 구문

```
<RAISE Statement> ::= 
    RAISE  <Exception-Name>
    ;
```

<a id="55ccb11a53a9497a"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="0dc67e937779ecc9"></a>
### 구문 규칙 및 파라미터

- Raise 시킬 exception name이 raise가 속한 PL block이나 상위 PL block의 DECLARE 절에 선언되어야 한다. 단, predefined exception은 선언없이 raise할 수 있다. 
- Raise 문이 exception handler 내에서 사용되면 exception name을 생략할 수 있는데 이 경우, 직전 exception이 상위 블럭으로 전파된다.

<a id="6e2e8db18130835f"></a>
### 설명

Exception이 발생한 PL block에서 처리되지 못하면 상위 PL block으로 전파된다.  
Raise 시킬 exception이 RAISE 구문을 포함하는 PL block 및 상위 PL block 내의 모든 exception handler에 존재하지 않을 경우 에러가 발생한다.  
처리될 때까지 RAISE exception이 발생한 PL block부터 상위로 전파되며 하위 PL block의 exception handler로는 전파되지 못한다.

**User exception 전파**

<a id="3fe650e31dde8f93"></a>
| Raise exception | Exception handler  SCOPE | Exception handler | 상위 전파여부 |
| --- | --- | --- | --- |
| User exception without error code | 동일 scope | X | "unhandled exception" 오류를 상위 scope으로 전파한다. |
| User exception with error code | 상위 scope | X | User exception을 전파한다. |
| User exception with error code | 동일 scope | X | User defined error code를 전파한다. |
| User exception with error code | 상위 scope | X | User defined error code를 전파한다. |

<a id="93e6c0b633c7ef4a"></a>
### 사용 예

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

<a id="cade7405e14296de"></a>
### 호환성

SQL 표준에는 &lt;handler declaration&gt;과 &lt;condition declaration&gt;은 기술되어 있지만 구문은 지원하지 않는다.

<a id="25bdf0a5e1e2a742"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Exception Handler](#086edc92697ae2b8)
- [Exception Declaration](#9bf4ef42c50667c4)

<a id="4209175b58e67025"></a>
## Record Variable Declaration

<a id="f25800e77609e523"></a>
### 기능

DECLARE 영역에서 record type 변수를 선언한다.

<a id="3299b78e47426b31"></a>
### 구문

```
<declare record variable> ::=
    variable_name <recordType> 
    ;

<recordType> ::=
     <tableName>%ROWTYPE
   | USER_DEFINED_DATA_TYPE
```

<a id="acaaed26e98407ec"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 declaration 영역에서만 사용할 수 있다.

<a id="2035cd6d4e163447"></a>
### 구문 규칙 및 파라미터

- Variable_name
    - 선언할 변수의 이름이다.
    - 변수 이름의 길이는 128 바이트보다 작아야 한다.
    - 하나의 scope (PL block body) 내에서 고유한 이름이어야 한다.
    - 중첩된 하위의 PL block body에서는 같은 이름의 변수를 선언할 수 있다.
    - 중복 선언된 변수를 명확히 사용하기 위해서는 scope_name.variable_name의 형태로 사용해야 한다.
    - Scope 이름을 명시하지 않고 중복 선언된 변수를 사용할 경우에는 자동으로 가장 가까운 scope의 변수가 사용된다.
- Record_type
    - %ROWTYPE 및 사용자가 정의한 recordType을 사용할 수 있다.
    - recordType 선언에 대한 자세한 내용은 [User-defined Record Type](22-psm-datatypes.md#0d8015878f2dc30c)을 참조한다.

<a id="e7865d1b2f640f30"></a>
### 설명

- 선언된 변수는 다음과 같은 특징이 있다.
    - 하나의 scope (PL block body) 내에서 고유한 이름이어야 한다.
    - 중첩된 하위의 PL block body에 동일한 이름의 변수를 선언할 수 있다.
    - 중복 선언된 변수를 명확히 사용하기 위해서는 scope_name.variable_name의 형태로 사용해야 한다.
    - Scope 이름을 명시하지 않고 중복 선언된 변수를 사용할 경우에는 자동으로 가장 가까운 scope의 변수가 사용된다.
- 선언된 변수는 해당 scope와 하위 scope에서 사용되며, embedded SQL에서와 달리 ':' 기호를 붙이지 않는다.
- 사용된 변수는 해당 SQL이나 PSM control statement에 대해 bind parameter (INOUT)로 작동한다.

<a id="85d315b8f546331c"></a>
### 사용 예

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

<a id="60d0a63977b76f61"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="14c7507ca43ee90a"></a>
## RETURN Statement

<a id="ae2443e6c9f8f99a"></a>
### 기능

Function이 반환할 값을 지정한 후 해당 function을 종료한다. Procedure는 반환값을 지정하지 않고 해당 procedure를 종료한다.

<a id="c2d4d698f8bf74c9"></a>
### 구문

```
<return statement> ::=
    RETURN [ return_value_expr ]
    ;
```

<a id="f033c9702a33082a"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.  
Table function의 PL block에서는 사용할 수 없다.

<a id="aeb2ea54a6e01dbd"></a>
### 구문 규칙 및 파라미터

- Return_value_expr
    - 반환할 값의 표현식으로써 function일 경우에만 명시할 수 있다.

<a id="ff6d82d30c7c928a"></a>
### 설명

현재 수행되고 있는 procedure/ function을 종료한다.  
Function의 경우, RETURN 구문이 수행되지 않고 종료되거나, RETURN 구문이 return_value_expr를 가지지 않으면 오류가 발생한다.  
Table function에서는 사용할 수 없다.

<a id="ab75f06651d78bf6"></a>
### 사용 예

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

<a id="2447022ae93e02ad"></a>
### 호환성

SQL 표준에는 기술되어 있지만 conformance rule은 존재하지 않는다.

<a id="47b0754ff8d5c167"></a>
## RETURN TABLE Statement

<a id="baa21c0a31c1f58d"></a>
### 기능

Cursor variable의 cursor query나 select statement를 실행한 결과 집합을 반환한 후에 function을 종료한다.

<a id="f63a69556e2923b2"></a>
### 구문

```
<return table statement> ::= 
    RETURN TABLE ( { <cursor variable name> | <select statement> } ) 
    ;
```

<a id="b7f130965e72aaf8"></a>
### 사용 범위 및 접근 권한

PSM 내 table function에서만 사용할 수 있다.  
Table function block의 body 영역에서만 사용할 수 있다.

<a id="c3d6575feeba3540"></a>
### 구문 규칙 및 파라미터

- &lt;cursor variable name&gt;
    - 명시한 cursor variable의 cursor query를 실행하여 결과 집합을 반환한다.
    - Cursor variable은 open 되어 있어야 한다.
    - Cursor variable의 cursor query는 fetch를 수행한 적이 없어야 한다.
    - Cursor query가 select statement인 cursor variable만 허용한다.
- &lt;select statement&gt;
    - select statement만 사용할 수 있다.
    - select for update statement, select into statement는 사용할 수 없다.

<a id="b112cdf594593857"></a>
### 설명

RETURN TABLE 구문에 명시된 cursor variable의 cursor query 또는 select statement를 수행한 결과 집합을 반환한다.   
RETURN TABLE 구문은 table function에서만 사용할 수 있다.

<a id="f7b3132a22551d56"></a>
### 사용 예

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

- cursor variable 사용 예

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
 
-- 각 학년의 최하점을 구하라 
gSQL> SELECT * FROM TABLE( func_cursor_variable( 'MIN' ) ); 
 
F_CLASS F_SCORE 
------- ------- 
      1      97 
      2      92 
      3      94 
 
3 rows selected.
```

- select statement 사용 예

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
 
-- 각 학년의 평균을 구하라 
gSQL> SELECT * FROM TABLE( func_select( 'AVG' ) ); 
 
F_CLASS F_SCORE 
------- ------- 
      1      98 
      2      95 
      3      96 
 
3 rows selected.
```

<a id="7cf21ff30f21922d"></a>
### 호환성

SQL 표준에는 &lt;return statement&gt; 구문에 기술되어 있다.  
단, SQL 표준에서는 cursor variable에 대해 정의하지 않고 있다.

<a id="ba7729d710616866"></a>
## RETURNING INTO clause

<a id="6fd0c2fce99fd3f5"></a>
### 기능

Insert/ update/ delete에서 처리된 데이터가 PSM 변수로 반환된다.

<a id="2722fa768fd870eb"></a>
### 구문

```
<Insert, Delete Returning_into_clause> ::=
      [ RETURN | RETURNING ] { * | { <value_expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]

<Update returning into clause> ::=
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] } INTO Variable [, ...]
```

<a id="ac13b959b845cad2"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 body 영역에서만 사용할 수 있다.

<a id="ad16dc8111fb2471"></a>
### 구문 규칙 및 파라미터

레코드 타입 변수는 다른 타입과 섞어서 사용할 수 없다.

<a id="c291b2856c36cfd3"></a>
### 설명

Insert/ update/ delete 문을 처리한 before/ after record를 returning into를 통해 저장한다.

<a id="5bd0e6746ad94ef0"></a>
### 사용 예

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

<a id="6335cb23a650a3a7"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="904f272f8d216420"></a>
## Routine Characteristics

<a id="58a6cadd5af32e88"></a>
### 기능

Routine의 특성을 명시한다.

<a id="47beb46457e17fd5"></a>
### 구문

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

<a id="e690f922e3e40ee0"></a>
### 사용 범위 및 접근 권한

아래의 구문에서 사용 가능하다.

- [CREATE FUNCTION](31-psm-sql-references.md#8f6d3c41338c889a)
- [CREATE PROCEDURE](31-psm-sql-references.md#48b6178f1f6cd4cb)
- [Function Declaration and Definition](#2a34bffbc503ec12)
- [Procedure Declaration and Definition](#b5a477999d1596c4)

<a id="6fe4f381f80c52bd"></a>
### 구문 규칙 및 파라미터

<a id="9b79e8c7ce7f7633"></a>
#### deterministic characteristic

Routine이 실행될 때마다 동일한 parameter 값을 입력하면 동일한 결과값을 반환하는지 여부를 지정한다.

- DETERMINISTIC: 동일한 parameter 값을 입력하면 동일한 결과값을 반환한다.
- NOT DETERMINISTIC: 동일한 parameter 값을 입력해도 동일한 결과값을 반환하지 않는다.

&lt;deterministic characteristic&gt;을 생략하면 기본값은 NOT DETERMINISTIC이다.  
&lt;deterministic characteristic&gt;은 의미적인 특성으로 &lt;routine body&gt;의 실행결과까지 판단할 수 없다.  
따라서 DETERMINISTIC이어도 routine body의 pl statement가 deterministic 하지 않다면 동일한 parameter에 대해서 다른 결과가 반환될 수 있다.

<a id="6ca0d63c8caffc50"></a>
#### null-call clause

routine의 parameter 중 하나라도 NULL이 입력되었을 경우 routine 실행 여부를 판단한다.

- RETURN NULL ON NULL INPUT: routine의 parameter 중 하나라도 NULL이 입력되었다면 routine은 NULL을 반환한다.
- CALLED ON NULL INPUT: routine의 parameter 중 하나라도 NULL이 입력되었는지에 상관없이 routine을 실행하여 결과를 반환한다.

<a id="eea1671567d10d6f"></a>
#### SQL-data access indication

&lt;SQL-data access indication&gt;은 routine에서 실행할 수 있는 &lt;pl statement&gt;를 분류하여 지정할 수 있다.

- NO SQL
    - 모든 SQL을 허용하지 않는다.
    - &lt;routine body&gt;가 &lt;external body&gt; 일 때만 사용할 수 있는 옵션이다.
- CONTAINS SQL
    - READ 또는 WRITE 속성이 없는 SQL만 허용한다.
- READS SQL DATA
    - READ가 가능한 SQL까지 허용한다.
- MODIFIES SQL DATA
    - 모든 SQL을 허용한다.

&lt;SQL-data access indication&gt;를 생략하면 기본값은 MODIFIES SQL DATA이다.

<a id="f55504deb2ab0a75"></a>
<table class="table column_count_5"><caption>SQL-data access indication에 따른 pl statement 실행 가능 여부</caption><thead><tr><th class="to_center to_middle" rowspan="2"><div>pl statement</div></th><th class="to_center" colspan="4"><div>Level Of SQL Data Access</div></th></tr><tr><th class="to_center"><div>NO SQL</div></th><th class="to_center"><div>CONTAINS SQL</div></th><th class="to_center"><div>READS SQL DATA</div></th><th class="to_center"><div>WRITE SQL DATA</div></th></tr></thead><tbody><tr><td class="to_left"><div>Assignment
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

<a id="2148477ccaf04922"></a>
### 설명

Routine의 특성을 명시한다.  
각각의 특성은 중복해서 명시할 수 없다.

<a id="71750413d0476241"></a>
### 사용 예

- Routine Characteristics 사용 예

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

- &lt;deterministic characteristic&gt; 사용 예

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

- &lt;deterministic characteristic&gt; 의 잘못된 사용 예

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

- &lt;null-call clause&gt; 사용 예

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

- &lt;SQL-data access indication&gt; 사용 예

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

<a id="a21ff95cd6881109"></a>
### 호환성

SQL 표준에 있는 &lt;routine characteristic&gt;들 중에 다음을 지원한다.

- &lt;deterministic characteristic&gt;
- &lt;null-call clause&gt;
- &lt;SQL-data access indication&gt;

<a id="f61d9c5700069209"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE FUNCTION](31-psm-sql-references.md#8f6d3c41338c889a)
- [CREATE PROCEDURE](31-psm-sql-references.md#48b6178f1f6cd4cb)
- [Function Declaration and Definition](#2a34bffbc503ec12)
- [Procedure Declaration and Definition](#b5a477999d1596c4)

<a id="597c0cca94e4ebaa"></a>
## %ROWTYPE Attribute

<a id="6a07699c79a3fb6e"></a>
### 기능

변수를 선언할 때 특정 테이블 또는 커서나 커서 변수의 result set과 같은 구조와 타입으로 정의한다.

<a id="2ab6045de38d4dcd"></a>
### 구문

```
<rowtype attribute> ::=
    <identifier chain> % ROWTYPE
```

<a id="48ea46da5d7fcd23"></a>
### 사용 범위 및 접근 권한

- PSM 내에서만 사용할 수 있다. (예: package, procedure, function)
- PL block의 declaration 영역에서만 사용할 수 있다.
- 변수를 선언할 때는 &lt;data type&gt; 부분에만 사용할 수 있다
- 레코드 타입의 필드를 선언할 때는 &lt;data type&gt; 부분에 사용할 수 없다. (complex data type은 지원하지 않는다.)

<a id="9ab82ef17da87f65"></a>
### 구문 규칙 및 파라미터

- Identifier chain은 다음과 같다.
    - 참조할 테이블, view, synonym의 이름이나 커서 또는 커서 변수의 이름

<a id="3eb8f7fc9d3cc88f"></a>
### 설명

- 참조 대상 검색 순서
    - 커서 또는 커서 변수 
    - Base table, view, 또는 synonym

- 참조 범위
    - Row attribute를 이용하여 참조할 경우 테이블 또는 커서의 result set에서 column 이름과 타입만 참조한다.
    - 따라서 NOT NULL constraint나 DEFAULT 값 설정 등은 참조하지 않는다.

<a id="4ddc417ce34ad474"></a>
### 사용 예

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

<a id="5c0a6571081c90d6"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="34027540ee4588ec"></a>
## Scalar Variable Declaration

<a id="e004c54d1c4b5c39"></a>
### 기능

DECLARE 영역에서 scalar 변수를 선언한다.

<a id="ce899d202f1e7eb0"></a>
### 구문

```
<declare scalar variable> ::=
    variable_name <data type> [ <variable initialize clause> ]
    ;

<variable initialize clause> ::=
      [ NOT NULL ] { DEFAULT | := } <value expression>
```

<a id="3b6c844b936b8f4e"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 declaration 영역에서만 사용할 수 있다.

<a id="ed5c88cd48ab434c"></a>
### 구문 규칙 및 파라미터

- Variable_name
    - 선언할 변수의 이름이다.
    - 변수 이름의 길이는 128 바이트보다 작아야 한다.
    - 하나의 scope (PL block body) 내에서 고유한 이름이어야 한다.
    - 중첩된 하위의 PL block body에 동일한 이름의 변수를 선언할 수 있다.
    - 중복 선언된 변수를 명확히 사용하기 위해서는 scope_name.variable_name의 형태로 사용해야 한다.
    - Scope 이름을 명시하지 않고 중복 선언된 변수를 사용할 경우에는 자동으로 가장 가까운 scope의 변수가 사용된다.
- Data_Type
    - GOLDILOCKS에서 제공하는 모든 built-in [Data Type](../part-03-sql-manual/11-sql-elements.md#0e511565dcb79955) 들을 사용할 수 있다.
- Value_expression
    - 변수에 지정할 초기값을 표현한다.
    - GOLDILOCKS가 지원하는 모든 상수 및 multi-row 함수들을 제외한 모든 표현식을 사용할 수 있다.

<a id="c9e4a373a9647873"></a>
### 설명

- 선언된 변수는 다음과 같은 특징이 있다.
    - 하나의 scope (PL block body) 내에서 고유한 이름이어야 한다.
    - 중첩된 하위의 PL block body에 동일한 이름의 변수를 선언할 수 있다.
    - 중복 선언된 변수를 명확히 사용하기 위해서는 scope_name.variable_name의 형태로 사용해야 한다.
    - Scope 이름을 명시하지 않고 중복 선언된 변수를 사용할 경우에는 자동으로 가장 가까운 scope의 변수가 사용된다.
- 선언된 변수는 해당 scope와 하위 scope에서 사용되며, embedded SQL에서와 달리 ':' 기호를 붙이지 않는다.
- 사용된 변수는 해당 SQL이나 PSM control statement에 대해 bind parameter (INOUT)로 작동한다.

<a id="7358cc0db2eaaf16"></a>
### 사용 예

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

<a id="d870fd1bf18f013d"></a>
### 호환성

- &lt;declare scalar variable&gt; 구문은 SQL 표준과 비교하여 다음과 같은 차이가 있다.
    - SQL 표준의 &lt;SQL variable declaration&gt;은 PL block body 내 (BEGIN 이후)에서 변수를 선언하지만, GOLDILOCKS는 별도의 declaration section에서 선언한다.
    - SQL 표준에서는 한 번의 DECLARE 구문으로 여러 개의 동일한 타입 변수를 선언할 수 있지만, GOLDILOCKS에서는 한 개의 statement로 한 개의 변수만 선언할 수 있다.
    - SQL 표준에서는 초기값을 설정할 때 DEFAULT 구문만 사용하지만, GOLDILOCKS는 assign 기호인 :=도 사용할 수 있다.

<a id="ae316b261e4e6598"></a>
## SELECT INTO Statement

<a id="eb1165fcddf3e272"></a>
### 기능

SELECT를 통해 한 개의 row를 반환 받는다.

<a id="109113a9349987dc"></a>
### 구문

```
<select statement: single row> ::=
    SELECT [ <hint clause> ] [ <set quantifier> ] <select list>
        INTO <select target list>
        <table expression>
    ;

<select target list> ::=
    variable_name [, ...]
```

<a id="52cc61e7c9853f0b"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="4f5066aa26130303"></a>
### 구문 규칙 및 파라미터

INTO 절을 제외한 사항은 select statement와 동일한 규칙을 따른다.

<a id="64848c0a592e26e5"></a>
### 설명

- SELECT INTO는 한 개의 record를 반환받는 용도로 사용한다. 
    - 결과가 0 건인 경우, "NO_DATA_FOUND" exception이 발생한다. 
    - 결과가 두 건 이상인 경우, "TOO_MANY_ROWS" exception이 발생한다. 
- PSM의 record type 변수를 통해 결과를 반환받을 수 있다. 
    - Record type변수를 사용할 경우 다른 타입의 변수와 섞어서 사용할 수 없다.

<a id="513f1c75bf888d76"></a>
### 사용 예

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

<a id="d0d0865ff7b64333"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="26bb4a7fe3335316"></a>
## SQLCODE Function

<a id="47adf64ecac41e93"></a>
### 기능

PSM에서 수행된 직전 statement의 error code를 반환한다.

<a id="34cfc7abe840c3b2"></a>
### 구문

```
<SQLCODE function> ::= SQLCODE
```

<a id="eeb2b1e22beb44a1"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다.

<a id="397dd8179fe75c43"></a>
### 구문 규칙 및 파라미터

별도의 argument를 갖지 않는다.

<a id="cd7def04d90543fb"></a>
### 설명

PL/ SQL에서 수행된 statement의 error code를 반환한다.  
Error code를 할당하지 않은 user-defined exception의 경우, handler에 의해 처리되는 시점에 1로 반환된다.  
Exception handler에 의해 오류 처리가 완료되면 0으로 반환된다.

<a id="13348bcc89c936af"></a>
### 사용 예

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

<a id="7b44b472cbf5c7e6"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="914b98e98643416e"></a>
## SQLERRM Function

<a id="eb712e261019f945"></a>
### 기능

PSM에서 수행된 직전 statement의 error message를 반환한다.

<a id="468328671ebf639e"></a>
### 구문

```
<SQLERRM function> ::= SQLERRM
```

<a id="cda79037d4afbd8e"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다.

<a id="9dfe258ba6d64acf"></a>
### 구문 규칙 및 파라미터

별도의 argument를 갖지 않는다.

<a id="90c274c3d2bd92df"></a>
### 설명

PL/ SQL에서 수행된 statement의 error message를 반환한다.  
Error code를 할당하지 않은 user-defined exception의 경우, handler에 의해 처리되는 시점에 user-defined exception으로 반환된다.  
Exception handler에 의해 오류 처리가 완료되면 *successful completion* 메시지를 출력한다.

<a id="49456e74d359c9dd"></a>
### 사용 예

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

<a id="b718648c4e663463"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="2924b9b7c25af3ed"></a>
## %TYPE Attribute

<a id="39990259d000d5bf"></a>
### 기능

변수를 선언할 때나 RECORD 타입의 특정 필드를 정의할 때 그 타입을 특정 테이블의 column 또는 다른 변수와 동일한 타입으로 정의한다.

<a id="11803ae6a21f41d8"></a>
### 구문

```
<type attribute> ::=
    <identifier chain> % TYPE
```

<a id="b0c575f7f47cbce1"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 declaration 영역에서만 사용할 수 있다.  
변수를 선언할 때나 레코드 타입의 필드를 선언할 때 &lt;data type&gt; 부분에만 사용할 수 있다.

<a id="620c4e63811f27be"></a>
### 구문 규칙 및 파라미터

- Identifier_chain
    - 참조할 테이블의 column 또는 기존에 선언된 변수 (혹은 변수의 필드)의 이름이다.

<a id="8f3d44d73cbf922e"></a>
### 설명

<a id="95599bcd4f10c0d7"></a>
#### 참조 범위

참조된 객체 타입에 따른 참조 범위는 다음과 같다.

- 참조된 객체가 테이블의 column일 때
    - Column의 데이터 타입을 참조한다.
    - Column의 constraint (예: NOT NULL)는 참조하지 않는다.
    - Column의 기본 초기값은 참조하지 않는다.
- 참조된 객체가 다른 변수 (또는 변수의 필드)일 때
    - 변수 (또는 필드)의 데이터 타입을 참조한다.
    - 변수 (또는 필드)의 constraint (NOT NULL)를 참조한다.
    - 변수 (또는 필드)의 기본 초기값은 참조하지 않는다.
- 참조 대상 객체의 검색 순서는 다음과 같다.  
  1. 변수 (혹은 필드) 이름  
  2. Column 이름

<a id="364b34838d02c923"></a>
#### NOT NULL Constraints 변수 참조

NOT NULL 속성의 변수를 참조할 때는 초기값을 참조하지 않으므로 반드시 새로운 초기값을 지정해야 한다.   
현재 record type 변수의 필드에 대한 type attribute를 사용할 때 필드 초기값 설정을 지원하지 않으므로 NOT NULL 타입의 필드는 참조할 수 없다.

<a id="f08bb3e25725fe02"></a>
### 사용 예

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

<a id="052bfac8d2085b7f"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="eef0130cc744e99e"></a>
## UPDATE Statement Extension

<a id="475d6d7aa5d4dc51"></a>
### 기능

PSM에서 UPDATE 문의 갱신 대상 column을 나열하는 방식 외에 추가적으로 record type 변수를 이용하여 레코드를 갱신한다.   
PSM에서 UPDATE (searched) RETURNING INTO 절에 record type 변수를 사용하여 결과를 저장한다.

<a id="212ccbd50d38a2d6"></a>
### 구문

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

<a id="f16603a6866c6c89"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="cfb787f31a7a3ddc"></a>
### 구문 규칙 및 파라미터

- UPDATE SET ROW 구문에서 사용할 &lt;PSM_Variable&gt;은 반드시 record type으로 선언된 변수이어야만 한다.
- UPDATE RETURNING INTO 구문에서 사용할 &lt;Variable&gt;은 record type이 아니어도 된다.
    - 단, record type으로 기술한 경우 다른 데이터 타입의 변수와 섞어서 사용하거나 두 개 이상의 record type 변수를 나열할 수 없다.

<a id="3105585bc686bcf1"></a>
### 설명

PSM에서 record type 변수를 통해 레코드를 갱신하거나 RETURNING INTO의 결과를 저장한다.

<a id="a6dde7eaa541185d"></a>
### 사용 예

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

<a id="48dfc024608f4bac"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="ec75086399351674"></a>
## WHILE LOOP Statement

<a id="042fdd224a225bc3"></a>
### 기능

&lt;search condition&gt;이 TRUE 값을 반환하는 동안 내부의 statement들을 수행한다.

<a id="ba7292f68bbbeaa5"></a>
### 구문

```
<while loop statement> ::=
    WHILE <search condition>
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="d184552dd7b9a38d"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
&nbsp;PL block의 body 영역에서만 사용할 수 있다.

<a id="f09a0dc95a0e3a36"></a>
### 구문 규칙 및 파라미터

- Search condition은 다음과 같다.
    - while 루프를 계속 순환하는 조건 표현식이다.
    - 최종적으로 boolean 타입을 반환해야 한다.

<a id="bed40f00a065fc11"></a>
### 설명

while loop 구문은 &lt;search condition&gt;의 평가 결과가 TRUE인 동안 내부의 statement list를 수행한다.

<a id="d971cde9184dc91a"></a>
### 사용 예

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

<a id="99af706f315b60f0"></a>
### 호환성

&lt;while loop statement&gt; 구문은 SQL 표준에 &lt;while statement&gt;로 정의되어 있다.  
SQL 표준의 &lt;while statement&gt;는 loop 구문을 DO ... END WHILE로 수행하는 반면에 GOLDILOCKS는 LOOP ... END LOOP로 수행한다.

<a id="524adf24cd2f8c77"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CONTINUE Statement](#35f5b1376cc629d4)
- [EXIT Statement](#46c4e6cb4d956122)
- [GOTO Statement](#b8ae5382c6d22723)

---

[← 29. Trigger](29-trigger.md) · [전체 목차](../README.md) · [31. PSM SQL References →](31-psm-sql-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
