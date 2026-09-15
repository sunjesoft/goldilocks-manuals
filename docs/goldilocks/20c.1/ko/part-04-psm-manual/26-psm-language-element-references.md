<a id="dad9d2d71e9bde63"></a>

# 26. PSM Language Element References

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/dad9d2d71e9bde63)  
> 태그: `20c.1_30_tag`

[← 25. PSM Packages](25-psm-packages.md) · [전체 목차](../README.md) · [27. PSM SQL References →](27-psm-sql-references.md)

<a id="659f810801070ff0"></a>
## Assignment Statement

<a id="7a72ed7c0cf0651e"></a>
### 기능

PSM block의 내부에서 변수나 out-bind parameter에 값을 저장한다.

<a id="69843f4c5d859aaa"></a>
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

<a id="b20fa5213c27fb7d"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="3c0a27ac7421821e"></a>
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

<a id="01613ab14f69d1ab"></a>
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

<a id="6241910d3a7ab51a"></a>
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

<a id="fcba3726f5bccb96"></a>
### 호환성

&lt;assignment statement&gt; 구문은 SQL 표준과 비교하여 다음과 같은 차이가 있다.

- SQL 표준의 &lt;assignment statement&gt;는 &lt;singleton variable assignment&gt;와 &lt;multiple variable assignment&gt;를 정의하지만, GOLDILOCKS는 &lt;singleton variable assignment&gt; 형식만 지원한다. 
- SQL 표준의 &lt;assignment statement&gt;는 SET 키워드로 시작하지만, GOLDILOCKS는 SET 키워드를 사용하지 않는다. 
- SQL 표준의 &lt;assignment statement&gt;는 target과 value 사이에 &lt;equal operator&gt; (=)를 사용하지만, GOLDILOCKS는 := 를 사용한다.

**SQL 표준 호환성**

<a id="d28eca17e06c49d7"></a>
<table><tbody><tr><th align="center">Feature ID</th><th align="center">설명</th><th align="center">지원 여부</th></tr><tr><td align="left">P002</td><td align="left">Computational completeness</td><td align="center">X</td></tr><tr><td align="left">P006</td><td align="left">Multiple assignment</td><td align="center">X</td></tr></tbody></table>

<a id="0b82703f49cc3661"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Scalar Variable Declaration](#585e7c4d2d8c7d11)
- [Record Variable Declaration](#cf3b00514771d5fd)
- [COLLECTION Variable Declaration](#1525308e92506d49)
- [Cursor Variable Declaration](#4c902da2840aaa72)

<a id="b44220cd0e21c3a9"></a>
## Basic LOOP Statement

<a id="7c28ca4ef85461bf"></a>
### 기능

GOTO나 EXIT 등이 수행되어 LOOP를 종료하기 전까지 LOOP 내부의 statement 들을 반복 수행한다.

<a id="5586eac125892135"></a>
### 구문

```
<basic loop statement> ::=
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="faffd7d97d7895c8"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 body 영역에서만 사용할 수 있다.

<a id="5621b1e529e8332b"></a>
### 구문 규칙 및 파라미터

- loop_name
    - &lt;basic loop statement&gt;의 label 이름이다. 
    - Comment의 역할만 하기 때문에 실제 &lt;basic loop statement&gt;의 label 이름과 달라도 무방하다.

<a id="42ffaf698773f41c"></a>
### 설명

Basic loop 구문은 LOOP 내부의 statement들을 반복 수행한다.  
Basic loop 구문은 loop 계열 statement이므로 GOTO, EXIT, CONTINUE가 label로 지칭하는 target statement가 될 수 있다.

<a id="30fd20b805d59ae2"></a>
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

<a id="d20834748d726fe8"></a>
### 호환성

&lt;basic loop statement&gt; 구문은 SQL 표준의 &lt;loop statement&gt;와 동일하다.

**SQL 표준 호환성**

<a id="7586627a3ab18c5c"></a>
| Feature ID | 설명 | 지원여부 |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="f26ad321e6c841f0"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CONTINUE Statement](#ffc467958d2152c5)
- [EXIT Statement](#b8d97bb30e1e9154)
- [GOTO Statement](#d1563db2fb06a6c5)

<a id="935e63becc4b4210"></a>
## Block (BEGIN .. END)

<a id="1c33bcc5fed25db5"></a>
### 기능

새로운 scope를 생성하며, 변수, 커서, 타입과 exception 등을 정의한다.

<a id="d9bbb174bd13c5b4"></a>
### 구문

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

<a id="8539c763c9385dec"></a>
### 사용 범위 및 접근 권한

PROCEDURE, FUNCTION 또는 anonymous block 내에서만 사용할 수 있다.

<a id="09f5834ef7140294"></a>
### 구문 규칙 및 파라미터

- Variable declaration
    - Block 내에서 사용할 scalar/ record/ array 타입의 변수들을 선언한다
- Explicit cursor declaration
    - Block 내에서 사용할 cursor를 선언한다.
- Explicit cursor definition
    - Block 내에서 사용할 cursor를 정의한다.
- Cursor variable declaration
    - Block 내에서 사용할 cursor 변수들을 선언한다.
- Type definition
    - Block 내에서 변수를 선언할 때 사용할 사용자 정의 타입들을 정의한다.
- Exception declaration
    - Block 내에서 사용할 exception들을 선언한다.
- Exception init pragma
    - 사용자가 정의한 exception이 처리할 error code를 설정한다.
- Procedure declaration
    - Block 내에서 사용할 procedure들을 선언한다.
- Procedure definition
    - Block 내에서 사용할 procedure들을 정의한다.
- Function declaration
    - Block 내에서 사용할 function들을 선언한다.
- Function definition
    - Block 내에서 사용할 function들을 정의한다.
- Static SQL
    - PSM에서 수행할 수 있는 Data Manipulation Language (DML)과 Data Control Language (DCL)를 가리킨다.
- Dynamic SQL
    - GOLDILOCKS PSM에서 지원하는 동적 질의 처리 관련 구문들을 가리킨다.
- PSM control statement
    - GOLDILOCKS PSM에서 지원하는 각종 flow control 구문들을 가리킨다.

<a id="71459541defc79b0"></a>
### 설명

&lt;psm block&gt;은 PSM의 기본 구성 요소이다.  
Bock은 선언부 (declaration part)와 예외 처리부 (exception handling part)를 가질 수 있다.  
Block은 중첩될 수 있고 중첩된 block은 새로운 하위 변수 scope를 가진다. 상위 block은 하위 block의 변수를 참조할 수 없다.

<a id="01e4a6db9be89b4a"></a>
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

<a id="b271bccbfcefd99d"></a>
### 호환성

SQL 표준의 &lt;compound statement&gt;는 새로운 savepoint를 지정하는 ATOMIC/ NOT ATOMIC 구문을 정의하였지만, GOLDILOCKS는 이를 지원하지 않는다.

**SQL 표준 호환성**

<a id="bf7836cef0b7bf2f"></a>
| Feature ID | 설명 | 비고 |
| --- | --- | --- |
| P002 | Computational completeness | ATOMIC 구문을 지원하지 않는다. |

<a id="f4d94a9ba27c7f6b"></a>
### 참조

자세한 내용은 [Overview of PSM](19-overview-of-psm.md#f2a60fe45b6c6f70)을 참조한다.

<a id="9e972367a0b53350"></a>
## CASE Statement

<a id="b02557617f7d8c4d"></a>
### 기능

주어진 여러 조건들 중에 TRUE를 반환하는 조건에 해당하는 statement list를 수행한다.

<a id="e3cddd142f4a54e8"></a>
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

<a id="4cc7eb0ce4cb238a"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="a24b05e18cccce1c"></a>
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

<a id="b0f5d7d87faaa9bc"></a>
### 설명

IF 구문과 유사하게 조건들을 평가하여 TRUE를 반환하는 WHEN 절의 statement들을 수행한다.   
순서대로 먼저 나오는 조건식부터 평가하여 해당 조건식이 TRUE인 경우, 그 이후의 조건식들은 평가하지 않는다.   
만일 조건식에 해당하는 경우가 존재하지 않고 ELSE 절이 기술되지 않은 경우에는 에러가 발생한다.

<a id="a29be7558c2afc80"></a>
### 사용 예

<a id="aec9dc2bd2d3e897"></a>
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

<a id="c9bd6a0597bead64"></a>
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

<a id="89e3a3a2fb0b7e58"></a>
### 호환성

SQL 표준의 CASE 구문은 row 타입 (list 타입) value 간의 비교를 정의하였지만, GOLDILOCKS는 지원하지 않는다  
SQL 표준의 CASE 구문은 &lt;when operand&gt;에 ','로 구분되는 여러 조건들을 리스트로 정의할 수 있지만, GODILOCKS는 지원하지 않는다.

**SQL 표준 호환성**

<a id="f5f8c2d7edc07dbb"></a>
| Feature ID | 설명 | 비고 |
| --- | --- | --- |
| P002 | Computational completeness | P004, P008을 지원하지 않는다. |
| P004 | Extended CASE statement | - |
| P008 | Comma-separated predicates in simple CASE statement | - |

<a id="b05f50404c599887"></a>
## CLOSE Statement

<a id="057415c63dd1c1bb"></a>
### 기능

Open 상태인 cursor를 닫는다.

<a id="e8c6dd33dbab0391"></a>
### 구문

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="e8f5dc6f1ea5ac78"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="7f8d836a37883ca9"></a>
### 구문 규칙 및 파라미터

- cursor_name
    - Close 할 cursor의 이름이다.

<a id="83393f1888315073"></a>
### 설명

Open 상태인 cursor를 닫는다.  
Close 된 상태인 cursor는 open 구문을 사용하여 다시 open 할 수 있다.

<a id="01ab01bb70cb4cc2"></a>
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

<a id="83a2fb8f43b0c908"></a>
### 호환성

표준 SQL에 정의되어 있지 않다.

<a id="9f013ea7e0097e57"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [FETCH Statement](#28d6b09490d25cec)
- [OPEN Statement](#50e24b0f75098d4f)

<a id="ce1d9bed3677e61a"></a>
## Collection Method Invocation

<a id="fe88417160622887"></a>
### 기능

Collection type의 변수를 탐색할 수 있는 method를 제공한다.

<a id="f3ccf384839dd0ec"></a>
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

<a id="89e21d450c13756e"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="98dc88d5d760b6da"></a>
### 구문 규칙 및 파라미터

- Collection type으로 선언된 변수에만 사용할 수 있다.
- FIRST, LAST, COUNT는 parameter를 가질 수 없다.
- PRIOR, NEXT, EXISTS, DELETE와 같이 대상을 지정해야 할 경우에는 parameter를 명시해야 한다.
- DELETE의 경우에는 PSM statement와 같이 동작하며 다른 변수로 결과를 반환할 수 없다. (Expression에 사용할 수 없다.)

<a id="b399abebb1338e40"></a>
### 설명

다음 표를 참조한다.

**함수**

<a id="aa2097003ec9c978"></a>
| 함수명 | 기능 | 반환값 | 인자 필요여부 |
| --- | --- | --- | --- |
| FIRST | 가장 작은 key를 반환한다. | INDEX OF에 지정된 key type | X |
| LAST | 가장 큰 key를 반환한다. | INDEX OF에 지정된 key type | X |
| PRIOR | 입력된 key보다 작은 key를 반환한다. | INDEX OF에 지정된 key type | O |
| NEXT | 입력된 key보다 큰 key를 반환한다. | INDEX OF에 지정된 key type | O |
| COUNT | 저장된 개수를 반환한다. | INTEGER | X |
| DELETE | Key에 해당하는 값을 삭제한다. | N/A | O |
| EXISTS | Key의 존재 유무를 반환한다. | BOOLEAN | O |

<a id="10f7354abed9f8ed"></a>
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

<a id="935e2c4bdce3ab52"></a>
### 참조

자세한 내용은 [COLLECTION Variable Declaration](#1525308e92506d49)을 참조한다.

<a id="1525308e92506d49"></a>
## COLLECTION Variable Declaration

<a id="ded38d0aa8b2d78c"></a>
### 기능

Collection 변수를 선언한다.

<a id="94de1a0b97a3956e"></a>
### 구문

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

<a id="7c4f4106eb3f8945"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 declaration 영역에서만 사용할 수 있다.

<a id="d2663fa21359741a"></a>
### 구문 규칙 및 파라미터

- Type-name
    - 사용자가 사용할 collection type의 이름을 지정한다. 
- Element-type
    - Collection 변수에 저장될 element의 type을 지정한다. 
- Index-type
    - Collection 변수에 저장된 key의 data type을 지정한다.

<a id="2c34f8a4fa141161"></a>
### 설명

Collection type을 선언한다.

<a id="7585dafb1205dc00"></a>
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

<a id="8876384657a06220"></a>
### 호환성

SQL 표준에서는 정의하지 않고 있다.

<a id="00aeb23fe81e6401"></a>
### 참조

자세한 내용은 [Collection Method Invocation](#ce1d9bed3677e61a)을 참조한다.

<a id="ffc467958d2152c5"></a>
## CONTINUE Statement

<a id="03ad2457e109a7c5"></a>
### 기능

현재 진행 중인 statement list의 수행을 중지하고, 상위 loop statement의 다음 iteration을 수행한다.

<a id="d606441489984291"></a>
### 구문

```
<continue statement> ::=
    CONTINUE [ label_name ] [ WHEN condition ] 
    ;
```

<a id="4aa9dbc6b2a9cb3c"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

Target label을 가진 statement는 다음 loop 계열 statement 중 하나이어야 한다.  

• basic loop statement  
• for loop statement  
• while statement  
• forall statement

<a id="00609ed2a76bd858"></a>
### 구문 규칙 및 파라미터

- Label name
    - identifier chain의 형식을 가질 수 있다.
- Condition
    - 명시된 경우, 해당 조건이 TRUE일 때만 loop statement로 복귀한다.

<a id="f53ebf8ff6bb4548"></a>
### 설명

현재 진행 중인 statement list의 수행을 중지하고 상위 loop statement로 복귀한다.

Label이 명시되면 해당 label 이름을 가진 상위 loop statement로 복귀한다.  
Label이 명시되어 있지 않으면 가장 가까운 상위 loop statement로 복귀한다.  
같은 label 이름을 가진 여러 개의 상위 statement들이 존재할 경우, 가장 가까운 statement가 선택된다.  
현재 위치에서 visible한 (중첩된 scope 내에 존재하는) loop statement로만 복귀할 수 있다.

조건이 명시되면 해당 조건이 TRUE인 경우에만 복귀한다.  
조건이 명시되지 않으면 무조건 복귀한다.

<a id="00cbf21282ce2759"></a>
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

<a id="ce75ae6fc242538b"></a>
### 호환성

&lt;continue statement&gt; 구문은 SQL 표준의 &lt;iterate statement&gt;와 기능이 유사하다.  
단, &lt;iterate statement&gt; 구문은 WHEN condition 기능은 제공하지 않는다.

<a id="47302af4dc5ef3d1"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [EXIT Statement](#b8d97bb30e1e9154)
- [GOTO Statement](#d1563db2fb06a6c5)

<a id="130aee8cb71b6714"></a>
## Cursor FOR LOOP Statement

<a id="13af6e3b74fc2b9b"></a>
### 기능

PSM에서 사용자가 선언한 cursor나 query에 의해 생성된 result의 row 개수만큼 loop를 수행한다.

<a id="aff1705d1a5af53d"></a>
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

<a id="d7ea44048b066509"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PSM 내의 body에서만 사용할 수 있다.

<a id="7bd1192d91ca029f"></a>
### 구문 규칙 및 파라미터

For~Loop 내에 선언된 변수는 해당 loop scope 내에서만 유효하다. (해당 Cursor For Loop Block Scope 밖에서는 해당 변수를 참조할 수 없다.)

<a id="138b90bd471b8630"></a>
#### Cursor Name을 사용한 경우

Cursor name을 사용하여 LOOP를 수행할 경우 cursor가 미리 선언되어 있어야 한다.   
Actual param에 대한 자세한 내용은 [OPEN Statement](#50e24b0f75098d4f)를 참조한다.

<a id="609943c06eb7f952"></a>
#### Cursor Query를 사용한 경우

Select나 returning query와 같이 GOLDILOCKS 내부적으로 implicit cursor로 처리되는 질의만 수행할 수 있다.

<a id="778234ab903931a4"></a>
### 설명

Cursor가 생성한 결과 개수만큼 loop를 돌면서 loop 내의 PSM statements를 수행한다.   
LOOP 중에 cursor가 invalid한 상태가 (예: closed) 되면 더 이상 loop를 수행하지 않고 오류로 처리한다.   
Explicit cursor name을 명시할 경우, 해당 cursor가 already opened이면 오류로 처리한다.

FOR LOOP 절에 명시된 cursor의 결과를 반환받는 변수는 자동으로 생성된다. (Cursor의 실행 결과에 의해 반환될 result set의 row type으로 생성된다.)   
다만, 사용자의 cursor query 결과 중 특정 테이블의 column이 아닌 select target expression에 대해 alias 등을 지정하지 않을 경우, 오류가 발생할 수 있다.

<a id="b0578a52f2acf4b0"></a>
### 사용 예

<a id="197fd0c561c3c5ae"></a>
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

<a id="8bf88d74e19608e5"></a>
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

<a id="cef1260621e4a80e"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Explicit Cursor Declaration and Definition](#e75d97743ae4a31b)
- [GOTO Statement](#d1563db2fb06a6c5)
- [EXIT Statement](#b8d97bb30e1e9154)

<a id="4c902da2840aaa72"></a>
## Cursor Variable Declaration

<a id="c2aa8a43a8c77268"></a>
### 기능

PSM의 DECLARE section에서 cursor variable을 선언한다.

<a id="58fb3614b76c196c"></a>
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

<a id="131fa0dc6feee2b1"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PSM의 declaration 영역에서만 사용할 수 있다.

<a id="f60be423fbd04d45"></a>
### 구문 규칙 및 파라미터

Cursor 변수의 초기값 지정이나 assign은 cursor 변수 사이에서만 가능하다.

<a id="061625fd922fec4f"></a>
### 설명

Cursor variable은 특정 cursor에 종속되지 않는 cursor를 가리키는 일종의 pointer 역할을 한다.

<a id="19d37b4a07227b1a"></a>
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

<a id="4a61a27b37644aba"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [OPEN Statement](#50e24b0f75098d4f)
- [FETCH Statement](#28d6b09490d25cec)
- [CLOSE Statement](#b05f50404c599887)

<a id="2153f77c710b2000"></a>
## DELETE Statement Extension

<a id="ebf973b25a08a39b"></a>
### 기능

PSM의 record type 변수를 이용하여 RETURNING INTO 절에 결과를 저장할 수 있다.

<a id="f64bd0817abaf5c8"></a>
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

<a id="a0df112f59af6280"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PSM의 body 영역에서만 사용할 수 있다.

<a id="3ab7d2d444254e99"></a>
### 구문 규칙 및 파라미터

Returning Into를 통해 반환받을 변수의 타입이 record-type인 경우 다른 변수 타입과 섞어서 사용할 수 없다.

<a id="cdd554adb9b76ffc"></a>
### 설명

PSM의 record type 변수를 이용하여 RETURNING INTO 절에 결과를 저장할 수 있다.

<a id="4461f0b64b5f9563"></a>
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

<a id="aac69ae9144ce135"></a>
### 참조

자세한 내용은 [데이터 삭제](../part-03-sql-manual/12-sql-languages.md#af357cb29fabde82)를 참조한다.

<a id="eb9c477be3cba8fb"></a>
## EXCEPTION_INIT Pragma

<a id="d5ae7c2ab8679e43"></a>
### 기능

사용자가 정의한 exception이 처리할 error code를 설정한다.

<a id="341b50c87b92669c"></a>
### 구문

```
< PRAGMA EXCEPTION_INIT > ::=
     PRAGMA EXCEPTION_INIT ( <Exception-Name>, <Internal-ErrorCode> ) 
     ;
```

<a id="353f92d7d88617c2"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PSM의 declaration 영역에서만 사용할 수 있다

<a id="ef54a566cb6d098b"></a>
### 구문 규칙 및 파라미터

Predefined exception은 argument로 사용되는 exception name에 사용할 수 없다. (predefined exception name은 선언할 수 없다.)    
동일한 PL BLOCK DECLARE 절에 argument로 사용되는 exception name이 반드시 미리 선언되어야 한다. (다른 BLOCK의 exception name 선언을 참조할 수 없다.)    
&lt;Internal-ErrorCode&gt;는 DB SYSTEM 내에 존재하는 내부 error code이어야 한다. (SUCCESS 코드는 설정할 수 없다.)

<a id="24289afc6ea55cdf"></a>
### 설명

사용자가 DB SYSTEM의 error code에 대응하는 exception name을 명시적으로 선언한다.

<a id="bf84460203236d66"></a>
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

<a id="c84e9b852ca223ec"></a>
### 호환성

Error code는 각 벤더마다 다르기 때문에 서로 호환되지 않는다.

<a id="bfcb088fd42c66b2"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Exception Declaration](#32065477a17d19d2)
- [Exception Handler](#eb05139898a51758)

<a id="32065477a17d19d2"></a>
## Exception Declaration

<a id="aea02c8de29f6fa3"></a>
### 기능

PL block 내의 exception name을 선언한다.

<a id="fe320ddf7f90637e"></a>
### 구문

```
< Exception-Declaration Statement > ::=
     <Exception-Name>  EXCEPTION 
     ;
```

<a id="6dbdbc70f4b68166"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PSM의 declaration 영역에서만 사용할 수 있다.

<a id="83cc5f6aa3a31cfa"></a>
### 구문 규칙 및 파라미터

Predefined exception name은 선언할 수 없다.   
동일한 SCOPE의 DECLARE 절에 중복으로 선언할 수 없다.

<a id="8ee8ce453203ca7e"></a>
### 설명

사용자가 명시적으로 exception을 선언한다.

<a id="525f9a01aca720c3"></a>
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

<a id="a2c96d61a81f87dd"></a>
### 호환성

표준 SQL의 exception 선언은 다음과 같지만 GOLDILOCKS는 위와 같은 구문을 지원한다.

```
<condition declaration> ::=
DECLARE <condition name> CONDITION [ FOR <sqlstate value> ]
```

<a id="1328d8b8a6687099"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Exception Declaration](#32065477a17d19d2)
- [EXCEPTION_INIT Pragma](#eb9c477be3cba8fb)

<a id="eb05139898a51758"></a>
## Exception Handler

<a id="0aec49a2fb500573"></a>
### 기능

PL/ SQL을 수행하는 중에 발생한 DB SYSTEM 상의 오류로 인한 암묵적 exception이나 사용자가 명시적으로 발생시킨 exception에 대해 정의된 동작을 수행한다.

<a id="75e8868196f1bd27"></a>
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

<a id="cedb20273c421f8c"></a>
### 사용 범위 및 접근 권한

PL block 내에서 사용할 수 있다.

<a id="c7ab4a15306193b5"></a>
### 구문 규칙 및 파라미터

Predefined exception인 OTHERS는 OR을 사용하여 다른 exception name과 함께 기술할 수 없다.   
Predefined exception인 OTHERS는 exception handler에 중복으로 기술할 수 없으며 가장 마지막에 기술하여야 한다.

<a id="addff2f881728985"></a>
### 설명

<a id="968249d6bd67aa02"></a>
#### Exception 유형

<a id="b6844425e3dd2da0"></a>
| Type | Definer | Has error | Has name | Raise implicitly | Raise explicitly |
| --- | --- | --- | --- | --- | --- |
| Predefined | System | Yes | Yes | Yes | Optionally |
| User-defined | User | If user assign | If user assign | No | Yes |

Predefined exception은 GOLDILOCKS에서 미리 지정한 exception name과 error code를 갖는다.   
그 외의 exception은 GOLDILOCKS 내부의 오류 코드 이름을 사용자가 predefined exception name과 다르게 설정하는 경우 (internally defined)와 별도의 error code를 지정하지 않고 exception name만 선언하는 경우 (user-defined)로 나누어진다.

<a id="3632fecaeb8201f5"></a>
#### Predefined Exception

**Predefined exception 유형**

<a id="3af0f5c5c8f26954"></a>
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

<a id="04696b2615265a9c"></a>
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

<a id="4209128a564cc795"></a>
### 호환성

SQL 표준 문법을 지원하지 않는다.

<a id="aa89eb35c2ca1376"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [EXCEPTION_INIT Pragma](#eb9c477be3cba8fb)
- [Exception Declaration](#32065477a17d19d2)

<a id="acfad17b43646d05"></a>
## EXECUTE IMMEDIATE Statement

<a id="b9315c1b11627712"></a>
### 기능

PSM 내에서 dynamic SQL을 실행한다.

<a id="512f9ab1d86e7e0b"></a>
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

<a id="605839c8c55abeba"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="aabe2ec721d74dab"></a>
### 구문 규칙 및 파라미터

<a id="291e655dfa561cff"></a>
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

<a id="74d190126d0bc90f"></a>
#### INTO Clause

Dynamic SQL 수행 결과가 존재하고 marker를 통해 binding된 경우가 아닌 SQL 문의 처리 결과를 반환 받는 경우이다. (내부적으로 implicit cursor fetch 형태이다.)   
구문은 다음과 같다.

```
EXECUTE IMMEDIATE 'SELECT ... FROM .. WHERE ...';
EXECUTE IMMEDIATE 'INSERT ... RETURNING ...';
EXECUTE IMMEDIATE 'UPDATE ... RETURNING ...';
EXECUTE IMMEDIATE 'DELETE ... RETURNING ...';
```

<a id="d93ba1e128786794"></a>
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

<a id="eae4c5795bd59992"></a>
#### RETURNING Clause

INSERT/ UPDATE/ DELETE RETURNING INTO 구문이 dynamic SQL로 사용된 경우, GOLDILOCKS는 USING 절에 기술된 변수를 OUT mode로 binding하여 결과를 반환받을 수 있다.   
다른 DBMS와의 호환을 위해 RETURNING INTO 절로도 동일한 결과를 반환받을 수 있다.

<a id="919634f66e16f947"></a>
#### 기타규칙

- DDL/ DCL은 어떤 BIND 절 (INTO, USING, RETURNING clause)도 사용할 수 없다. 
- INTO 절과 RETURNING INTO 절에는 OUT으로 쓰이기 때문에 별도의 bind type을 지정할 수 없으며 동시에 같이 사용할 수도 없다. 
- IN BIND type은 scalar type 변수만 사용할 수 있다. 
- OUT BIND type은 record type 변수를 사용할 수 있다. 하지만 scalar나 record 타입을 섞어서 동시에 나열할 수는 없다. 
- INTO 절과 USING OUT 또는 RETURNING INTO를 통해 결과를 나누어 받을 수 없다.

<a id="478d12368bbd280d"></a>
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

<a id="fa19765e89c357f7"></a>
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

<a id="b8d97bb30e1e9154"></a>
## EXIT Statement

<a id="6091d1117395e7b6"></a>
### 기능

상위 loop statement들 중에서 주어진 label을 가진 loop statement를 탈출하여 그 다음 statement를 수행한다.

<a id="91840fb1282868c1"></a>
### 구문

```
<exit statement> ::=
    EXIT [ label_name ] [ WHEN condition ]
    ;
```

<a id="6ef9374e1791819b"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="857c89f098a7b187"></a>
### 구문 규칙 및 파라미터

- Label name
    - 탈출할 loop statement의 label 이름이다.
    - Identifier chain 형식을 가질 수 있다.
- Condition
    - 조건을 명시할 경우, 해당 조건이 TRUE일 경우에만 loop statement를 탈출한다.

<a id="948a4393d950d684"></a>
### 설명

- 현재 진행중인 statement list 수행을 중단하고 상위 loop statement를 탈출한다.
- Target label을 가진 statement는 다음 loop 계열 statement 중 하나이어야 한다.
    - basic loop statement
    - for loop statement
    - while statement
    - forall statement
- Label이 명시된 경우, 해당 label 명을 가진 상위 loop statement를 탈출한다.
- Label이 명시되지 않은 경우, 가장 가까운 상위 loop statement를 탈출한다.
- 같은 label 명을 가지는 여러 개의 상위 statement들이 존재할 경우, 가장 가까운 statement를 선택한다.
- 현재 위치에서 visible 한 (중첩된 scope 내에 존재하는) loop statement만 탈출할 수 있다.

- 조건 (condition)이 명시된 경우, 해당 조건이 TRUE인 경우에만 탈출한다.
- 조건이 명시되지 않은 경우, 무조건 탈출한다.

<a id="8b1f34dd62b527ce"></a>
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

<a id="1d0b52c6c8ab2154"></a>
### 호환성

SQL 표준에는 존재하지 않는다.

<a id="861fc5146195dcde"></a>
## Explicit Cursor Attribute

<a id="c0ed12f720b93a53"></a>
### 기능

PSM에서 정의된 cursor의 상태값을 반환한다.

<a id="5a59e3be458a4b91"></a>
### 구문

```
<Explicit cursor attribute> ::=
    cursor_name '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="9dabd60e260a2ece"></a>
### 사용 범위 및 접근 권한

PSM 내의 body 영역에서만 사용할 수 있다.

<a id="c2e250ac8e544fa6"></a>
### 구문 규칙 및 파라미터

- Cursor_name
    - 상태값을 알고 싶은 커서의 이름이다.

<a id="8cd514c81c4d5fec"></a>
### 설명

- 주어진 커서의 상태값을 반환한다. 
    - ISOPEN: 현재 커서가 OPEN 상태인지 여부이다.
    - FOUND: 최근 fetch에 의해 데이터가 반환되었는지 여부이다.
    - NOTFOUND: FOUND의 반대이다.
    - ROWCOUNT: 커서가 최근에 OPEN 된 후 fetch 한 record의 개수이다.
- 커서의 상태에 따라 다음과 같은 값을 반환한다.

**수행 시점에 따른 결과표**

<a id="e2e256b2999bcae6"></a>
| Attribute 이름 | OPEN 전 | OPEN 후 | FETCH 후 | CLOSE 후 |
| --- | --- | --- | --- | --- |
| ISOPEN | FALSE | TRUE | TRUE | FALSE |
| FOUND | NULL | NULL | TRUE/ FALSE | NULL |
| NOTFOUND | NULL | NULL | TRUE/ FALSE | NULL |
| ROWCOUNT | NULL | NULL | N (개수) | NULL |

<a id="87529fbdab4023c4"></a>
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

<a id="86ef586458e0381b"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="e75d97743ae4a31b"></a>
## Explicit Cursor Declaration and Definition

<a id="af625e096eabbb80"></a>
### 기능

PSM의 DECLARE section에서 커서를 선언한다.

<a id="eb797acac79cc2bf"></a>
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
    IS select_statement
    ;
```

<a id="a4b57565c23c29d0"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function )   
PL block의 declaration 영역에서만 사용할 수 있다

<a id="de04f0360a8e7c6a"></a>
### 구문 규칙 및 파라미터

<a id="2239f9ab2a3a90b9"></a>
#### Cursor Name

선언할 커서의 이름이다.  
커서 이름의 길이는 128 바이트보다 작아야 한다.  
해당 scope 내에서 고유한 이름이어야 한다.

<a id="4483ff2d7fa9c2e7"></a>
#### RowType

커서의 레코드 타입을 정의한다.  
커서를 정의할 때 명시된 select target들의 개수가 같아야 하며, 데이터 타입이 호환되어야 한다.  
Rowtype을 지정하지 않을 경우, cursor를 정의할 때 기술된 select_statement의 SELECT target에 적합한 rowtype이 자동으로 지정된다.

<a id="27fdfae9900c2068"></a>
#### Param Name

특정 커서 내에서 parameter를 구별하는 이름이다.  
해당 커서 내에서 고유한 이름이어야 한다.  
만일 참조 가능한 scope 내의 다른 변수와 이름이 같을 경우, 해당 커서의 parameter를 우선적으로 참조한다.

<a id="811c9ad482b58002"></a>
#### DataType

해당 parameter의 데이터 타입을 지정한다.   
GOLDILOCKS에서 제공하는 모든 built-in 타입과 PSM 내에 정의된 타입을 사용할 수 있다.   
단, built-in 타입에는 범위를 제한하는 구문 (precision/ scale)을 지정할 수 없고 내부적으로 해당 데이터 타입의 최대 범위로 지정된다.

<a id="970b786849221a9e"></a>
#### Select Statement

커서가 수행할 SELECT 혹은 SELECT ... FOR UPDATE 구문을 지정한다.  
SELECT ... INTO 구문은 사용할 수 없다.

<a id="0b5078e342397f31"></a>
### 설명

- &lt;explicit cursor declaration&gt; 구문은 커서를 선언하거나 정의한다.
    - cursor declaration: 커서의 이름과 포맷만 선언한다.
    - cursor definition: 커서의 이름, 포맷 및 수행할 SELECT 구문까지 상세하게 정의한다.
- explicit cursor는 declaration 후에 definition 하여 사용하거나, declaration 없이 바로 definition 하여 사용할 수 있다. 
- declaration 후 definition 하여 사용할 경우에는 커서의 이름, parameter spec, 레코드 타입 정의가 정확하게 일치해야 한다.
- explicit cursor의 declaration과 definition은 같은 block 내에 존재해야 한다.
- explicit cursor는 해당 cursor가 define 된 block에 진입할 때 생성되며 해당 block에서 나갈 때 자동으로 CLOSE 되고 삭제된다.
- 특정 시점에 생성할 수 있는 explicit cursor의 최대 개수는 'MAXIMUM_NAMED_CURSOR_COUNT' 프로퍼티에 의해 제한된다.
- explicit cursor가 수행하는 SELECT 구문에는 다음 변수들을 사용할 수 있다.
    - 해당 cursor의 parameter
    - declare 시점의 scope에서 참조할 수 있는 모든 PSM 변수 (open 시점의 scope가 아님)
    - 외부 bind parameter (Anonymous PL block의 경우)
- SELECT 구문을 수행하는 explicit cursor는 다음 속성을 갖는다.
    - IN_SENSITIVE (다른 트랜잭션에 의한 변경에 영향받지 않는다.)
    - NON_SCROLLABLE (이전 record를 다시 fetch 할 수 없다.)
    - READ_ONLY (read 연산만 가능하다)
    - WITH-HOLD (COMMIT/ ROLLBACK이 수행되어도 cursor가 자동으로 닫히지 않는다.)
- SELECT ... FOR UPDATE 구문을 수행하는 explicit cursor는 다음과 같은 속성을 갖는다.
    - IN_SENSITIVE (다른 트랜잭션에 의한 변경에 영향받지 않는다.)
    - NON_SCROLLABLE (이전 record를 다시 fetch 할 수 없다.)
    - UPDATABLE (커서의 위치를 통해 UPDATE/ DELETE 할 수 있다.)
    - WITHOUT-HOLD (COMMIT/ ROLLBACK이 수행되면 cursor가 자동으로 닫힌다.)

<a id="2141c492ca2ec048"></a>
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

<a id="143177dc1e5c895d"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="2c93af1351b5939f"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [OPEN FOR Statement](#cacfe58629d4d394)
- [FETCH Statement](#28d6b09490d25cec)
- [CLOSE Statement](#b05f50404c599887)

<a id="28d6b09490d25cec"></a>
## FETCH Statement

<a id="4644e4ee84ed84c3"></a>
### 기능

OPEN 된 cursor의 레코드를 한 건 가져온다.

<a id="fafe9b2d49b286bd"></a>
### 구문

```
<fetch statement> ::=
    FETCH cursor_name <into clause>
    ;

<into clause> ::=
    INTO { variable [ , variable ] .. | record }
```

<a id="e9c29985acddc831"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="8cce18c3963a5768"></a>
### 구문 규칙 및 파라미터

- Cursor name
    - Fetch 할 cursor name이다.
- Variable
    - Fetch한 결과 중에 한 개의 column 값을 저장할 scalar 타입의 변수 또는 bind parameter이다.
- Record
    - Fetch한 결과인 한 개의 레코드 전체를 저장할 record 타입의 변수이다.

<a id="1fb598cc09dabd5f"></a>
### 설명

Open 된 커서로부터 레코드 한 개를 fetch하여 INTO 절에 명시된 변수로 값을 복사한다.   
만일 커서가 declaration만 되어 있고 definition 되어 있지 않으면 에러가 발생한다.  
해당 커서는 open 된 상태여야 한다.

INTO 절에 주어진 변수 타입은 fetch된 레코드 결과의 데이터 타입과 서로 호환 가능해야 한다.   
INTO 절에 주어진 변수들의 개수는 커서의 SELECT target 개수와 같아야 한다.   
단, INTO 절에 주어진 변수가 record type일 경우에는 한 개만 명시해야 한다.   
그리고 해당 record 변수의 field 개수는 SELECT target의 개수와 같아야 한다.

Fetch 할 레코드가 없는 상태에서 fetch가 호출되었을 경우, INTO 절의 target 변수 값은 변하지 않는다.

<a id="7687e363f20c77b9"></a>
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

<a id="0bc2cc14eed4158d"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="7a801d865abd3fa2"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [OPEN Statement](#50e24b0f75098d4f)
- [CLOSE Statement](#b05f50404c599887)

<a id="ecb4cbfd418b6463"></a>
## FOR LOOP Statement

<a id="cff35d5788eefcd8"></a>
### 기능

Index 변수가 주어진 값 범위를 가지는 동안 index 변수를 1씩 증가시키거나 감소시키면서 (REVERSE)   
내부의 statement들을 수행한다.

<a id="a59ff22540b25b34"></a>
### 구문

```
<for loop statement> ::=
    FOR index_variable_name IN [ REVERSE ] lower_bound .. upper_bound
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="692dea5df3a5e88d"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="aed342f34247b529"></a>
### 구문 규칙 및 파라미터

- Index variable name
    - FOR 구문에서 index로 사용할 변수의 이름이며 내부적으로 NATIVE_BIGINT 타입의 변수가 사용된다.
- Lower bound
    - 정수형이어야 하며, 만일 부동 소수점을 가진 숫자를 사용할 경우, 타입 변환 중에 소수점 이하는 반올림한다.
- Upper bound
    - 정수형이어야 하며, 만일 부동 소수점을 가진 숫자를 사용할 경우, 타입 변환 중에 소수점 이하는 반올림한다.

<a id="19f0b01167c137c6"></a>
### 설명

for loop 구문은 index 변수의 값을 증가시키거나 감소시키면서 내부의 statement list를 수행한다.

- REVERSE를 명시한 경우
    - index 변수는 upper_bound 값으로부터 1씩 감소하고, index 변수의 값이 lower_bound보다 작아지게 되면 for loop statement의 실행을 종료한다.
    - upper_bound 값이 lower_bound 값보다 작으면 내부의 statement list는 수행되지 않는다.
- REVERSE를 명시하지 않은 경우
    - index 변수는 lower_bound 값으로부터 1씩 증가하고, index 변수의 값이 upper_bound보다 커지게 되면 for loop statement의 실행을 종료한다.
    - lower_bound 값이 upper_bound 값보다 크면 내부의 statement list는 수행되지 않는다.

<a id="01fe80594b39cdbc"></a>
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

<a id="b2db1a9e2ac75b42"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="b5afccbcb5fe01c2"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CONTINUE Statement](#ffc467958d2152c5)
- [EXIT Statement](#b8d97bb30e1e9154)
- [GOTO Statement](#d1563db2fb06a6c5)

<a id="2ed935a597ae9a78"></a>
## Function Declaration and Definition

<a id="0d581162c7103293"></a>
### 기능

Nested function을 선언하고 정의한다.

<a id="c93104c3972c7734"></a>
### 구문

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

<a id="a3e202535fd0fd6e"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 declaration 영역에서만 사용할 수 있다.

<a id="bc60dc3ac04fd452"></a>
### 구문 규칙 및 파라미터

<a id="7d485ddaaf6b8e2b"></a>
#### func_name

생성할 function의 이름으로써 스키마 내에서 고유한 이름이어야 한다.   
Function 이름의 길이는 128 바이트보다 작아야 한다.

<a id="b8d3437a8937e416"></a>
#### Param Name

Function이 사용할 인자의 이름을 정의한다.  
각 인자의 이름은 function 내에서 고유한 이름이어야 한다.

<a id="9ac9f399b46edf9a"></a>
#### Bind Type

각 인자의 bind type을 설정한다.   
표기하지 않을 경우 기본 타입은 IN 이다.

<a id="1fa4d08359ba2d0f"></a>
#### Item Declaration

Function 내부에서 사용될 로컬 변수등의 item을 선언한다.   
PL block에서 선언될 수 있는 모든 item들을 선언할 수 있다.

<a id="203d9efcc0caa487"></a>
#### PL Stmt List

Function의 body 부분으로써 수행할 PL statement들을 나열한다.

<a id="777cc3790856a77d"></a>
### 설명

Nested function은 해당 procedure 내에서만 호출할 수 있는 subprogram이다.   
그 외의 사용 방법은 schema-level function과 동일하다.

<a id="dd037a69443dd8bf"></a>
### 사용 예

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

<a id="b3286d133a543431"></a>
### 호환성

Schema-level function과 동일하다.

<a id="53c7436f64d66117"></a>
### 참조

자세한 내용은 [CREATE FUNCTION](27-psm-sql-references.md#243dff1382985279)을 참조한다.

<a id="d1563db2fb06a6c5"></a>
## GOTO Statement

<a id="82d08ea834d4cd68"></a>
### 기능

현재 위치에서 접근 가능한 statement들 중에 주어진 label을 가진 가장 가까운 statement로 jump를 시도한다.

<a id="45dcea891c214674"></a>
### 구문

```
<goto statement> ::=
    GOTO label_name
    ;
```

<a id="d8de4c4a4438f6b4"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="1bc8985f5b0933c4"></a>
### 구문 규칙 및 파라미터

- Label_name
    - Jump를 시도할 statement의 label 이름이다.
    - Identifier chain 형식을 가질 수 있다.

<a id="4354751324dc8d6d"></a>
### 설명

해당 label 이름을 가진 statement로 jump하여 수행을 시작한다.  
여러 개의 후보 statement들이 존재할 경우, 가장 가까운 statement로 jump한다.  
현재 위치에서 visible 한 (중첩된 scope 내에 존재하는) statement로만 jump 할 수 있다.  
Forward jump와 backward jump 모두 가능하다.

<a id="2fb2b8016deee81f"></a>
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

<a id="1757d9e85b49fac9"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="d02eb20c9929e9c2"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [EXIT Statement](#b8d97bb30e1e9154)
- [CONTINUE Statement](#ffc467958d2152c5)

<a id="36d45960882ce562"></a>
## IF Statement

<a id="f26a91d3531e0400"></a>
### 기능

주어진 여러 조건들 중에 TRUE를 반환하는 조건에 해당하는 statement list를 수행한다.

<a id="76b51e3cea527fc9"></a>
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

<a id="80f2509982977520"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 body 영역에서만 사용할 수 있다.

<a id="ef5afe36bf915751"></a>
### 구문 규칙 및 파라미터

- Search condition
    - boolean 타입으로 최종 평가될 수 있는 표현식이다.
- Executable statement list
    - GOLDILOCKS PSM에서 지원하는 모든 statement 들의 list 이다.

<a id="7d964bfe7a82ed8b"></a>
### 설명

CASE 구문과 유사하게 조건들을 평가하여 TRUE를 반환하는 IF, ELSIF 절의 statement list를 수행한다.   
모든 조건들을 만족시키지 못하고 &lt;if statement else clause&gt;가 존재할 경우에는 해당 구문을 수행한다.   
ELSIF 구문들은 순서대로 먼저 나오는 조건식부터 평가하여 해당 조건식이 TRUE인 경우 그 이후의 조건식들은 평가하지 않는다

<a id="b5a0bfbd7056700f"></a>
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

<a id="14005dd0dcb52d3c"></a>
### 호환성

&lt;if statement&gt; 구문은 SQL 표준과 구문이 같고 동일하게 동작한다.

**SQL 표준 호환성**

<a id="d5a388dc038f5868"></a>
| Feature ID | 설명 | 지원여부 |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="59bae9b739156c33"></a>
## Implicit Cursor Attribute

<a id="b8f9d90f93164e99"></a>
### 기능

PSM에서 정의된 implicit cursor의 상태값을 반환한다.

<a id="e781d29dbaeef228"></a>
### 구문

```
<Implict cursor attribute> ::=
    SQL '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="063b84d20fcb8600"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="8c1493a6b447f93e"></a>
### 설명

- 직전에 수행된 SQL 문의 결과를 저장한다.
    - ISOPEN: 현재 커서가 OPEN 상태인지 여부로써 항상 FALSE로 설정된다.
    - FOUND: 직전 SQL 결과에 의해 데이터가 반환 되었는지 여부이다.
    - NOTFOUND: FOUND의 반대이다.
    - ROWCOUNT: 직전 SQL결과에 영향받은 record의 개수이다.

<a id="8cbd2f10f9f470bd"></a>
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

<a id="82ae88092f366b2f"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="579299577af7068e"></a>
## INSERT Statement Extension

<a id="162b8d8f90cfd795"></a>
### 기능

PSM에서 지원하는 record-type 변수를 VALUES 절에 기술하여 데이터를 입력할 수 있도록 insert statement를 확장한 기능이다.

<a id="bba2e5392553c5dd"></a>
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
      VALUES <Value_item> [, ...]
      | VALUES psm_record_type_variable [, ...]


<value-Item> ::=
      ( { <value expression> | DEFAULT } [, ...] ) 


<Returning_into_clause> ::=
      [ RETURN | RETURNING ] { * | { <value_expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]
```

<a id="e96cbba4b6a3210f"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 body 영역에서만 사용할 수 있다.  
EXECUTE IMMEDIATE의 원본 SQL 문에는 PSM insert extension 구문을 사용할 수 없다.

<a id="0e8705becf37187d"></a>
### 구문 규칙 및 파라미터

Insert statement의 기본 구문과 동일하게 동작한다. 다만, value item에 기존의 value expression을 괄호에 묶어 연속으로 나열하는 방법 외에 PSM record type 변수를 기술하는 기능이 추가되었다.

Value_Item에 괄호 없이 변수를 사용할 경우 반드시 PSM record type의 변수를 기술해야 한다.  
Insert extension 구문 형태로 사용할 경우 record type이 아닌 변수를 섞어서 사용할 수 없다.

<a id="f3f2eb03b4676042"></a>
### 설명

일반적인 insert statement 외에 PSM의 record type 변수를 이용하여 record를 저장하거나 returning into를 통해 결과를 받아 온다.   
Insert에 대한 자세한 내용은 다음 예를 참조한다.

<a id="ceecaba334740a3d"></a>
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

<a id="aa942abf0a3a1497"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="c11874da2e2d470a"></a>
## NULL Statement

<a id="4d7b4e7faa9f3d04"></a>
### 기능

아무 기능도 없는 statement 이다.

<a id="f8975b45d888a5be"></a>
### 구문

```
<null statement> ::=
    NULL
    ;
```

<a id="cddef4a7700b4f80"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="f312dfaeabdb8e1f"></a>
### 설명

아무 기능도 하지 않는 statement이며, 주로 특정 위치의 label을 설정하기 위해 사용된다.

<a id="7a295a1f279dd11c"></a>
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

<a id="105f03eb5d8e7ce7"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="50e24b0f75098d4f"></a>
## OPEN Statement

<a id="2bd25e88be370ce5"></a>
### 기능

PSM에서 정의된 cursor의 SELECT 구문을 실행한다.

<a id="40ac2950d88de5c0"></a>
### 구문

```
<open statement> ::=
    OPEN cursor_name [ <actual param spec> ]
    ;

<actual param spec> ::=
      ( expression [ , expression ] .. )
```

<a id="6c5039bde112dda4"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="a5cf01fe1107bda5"></a>
### 구문 규칙 및 파라미터

- Cursor_name
    - Open할 커서의 이름이다.

<a id="94f6c1f3378b3ea5"></a>
### 설명

정의된 커서의 SELECT 또는 SELECT ... FOR UPDATE 구문을 실행한다.  
만일 커서가 declaration만 되어 있고 definition 되어 있지 않을 경우, 에러가 발생한다.   
Actual parameter의 값들은 해당 parameter의 데이터 타입과 서로 호환 가능해야 한다.

Actual parameter의 개수는 커서의 parameter 개수와 같아야 한다.  
만일 커서의 parameter 개수보다 적을 경우, 나머지 모든 parameter들에 default 값이 명시되어야 한다.

<a id="e75726413e32c4b9"></a>
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

<a id="b9b4db1c1f376f3d"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="3a574511030316af"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CLOSE Statement](#b05f50404c599887)
- [FETCH Statement](#28d6b09490d25cec)

<a id="cacfe58629d4d394"></a>
## OPEN FOR Statement

<a id="eaebc8c62ace254c"></a>
### 기능

PSM에서 정의된 cursor 변수를 통해 SELECT 구문을 실행하여 한 개의 cursor를 open한다.

<a id="c0f3cd4460257e95"></a>
### 구문

```
<open statement> ::=
    OPEN cursor_variable_name FOR <select_query>
    ;
```

<a id="f25d99a70e1bf684"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="eeacbcf273ba29f9"></a>
### 구문 규칙 및 파라미터

- Cursor_Variable_name
    - cursor_variable의 이름이다.
- Select_query
    - Select query에는 static SQL과 dynamic SQL을 모두 사용할 수 있다.

<a id="f8dad97907c3900b"></a>
### 설명

정의된 cursor 변수의 SELECT 또는 SELECT ... FOR UPDATE 구문을 실행한다.  
만일 cursor 변수가 이전에 열어둔 커서가 존재하면 해당 커서가 자동으로 close 된다.

<a id="c8bfe6d89d181652"></a>
### 사용 예

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

<a id="bf918cdcd79fcaba"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="0c6d6499e31bf5a0"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Cursor Variable Declaration](#4c902da2840aaa72)
- [FETCH Statement](#28d6b09490d25cec)
- [CLOSE Statement](#b05f50404c599887)

<a id="ed784f708895815a"></a>
## Procedure Call

<a id="a62412e179bef373"></a>
### 기능

사용자 정의 procedure, built-in procedure 또는 nested procedure를 호출한다.

<a id="f41eefd25250eff3"></a>
### 구문

```
<Procedure call> ::=
    proc_name [ ( expr { , expr } ... ) ]
    ;
```

<a id="c1a9aebfa602bbcf"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

- 사용자 정의 procedure를 호출할 경우, 해당 procedure에 대한 다음 권한 중 하나가 있어야 한다.
    - EXECUTE PROCEDURE
    - Procedure가 속한 스키마에 대해 (EXECUTE PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
    - EXECUTE ANY PROCEDURE ON DATABASE

<a id="910c1d678b49bc10"></a>
### 구문 규칙 및 파라미터

- Proc_name 
    - 실행할 procedure의 이름으로써 다음과 같은 형태로 사용할 수 있다.

<a id="8b23952f4369f3f2"></a>
<table class="table column_count_3"><caption></caption><thead><tr><th class="to_center"><div>형태</div></th><th class="to_center"><div>구문</div></th><th class="to_center"><div>설명</div></th></tr></thead><tbody><tr><td class="to_left to_middle"><div>단일 identifier</div></td><td class="to_middle"><div>procedure_name</div></td><td><div>주어진 이름의 procedure를 호출한다.

검색 순서는 다음과 같다.
1. nested procedure
2. schema-level procedure</div></td></tr><tr><td class="to_left to_middle" rowspan="3"><div>identifier chain</div></td><td><div>label_name.procedure_name</div></td><td><div>nested procedure를 호출한다.</div></td></tr><tr><td><div>schema_name.procedure_name</div></td><td><div>schema-level procedure를 호출한다.</div></td></tr><tr><td><div>package_name.procedure_name</div></td><td><div>built-in procedure를 호출한다.</div></td></tr></tbody></table>

주어진 이름 (proc_name)으로 검색하여 최초로 발견된 procedure에 주어진 인자와 개수 및 타입이 적절하지 않으면 다른 procedure를 찾지 않고 에러를 발생시킨다.

<a id="ad2f2724241479cb"></a>
### 설명

이전에 정의된 사용자 정의 procedure, built-in procedure 또는 nested procedure를 호출한다.   
호출할 때 default 값이 정의된 인자값은 생략할 수 있다.

OUT이나 IN-OUT으로 지정된 인자에 procedure 변수나 bind parameter (?, :V1 등)를 사용하면 반환된 값을 얻을 수 있다.

<a id="30d80f05ec51894f"></a>
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

<a id="7c8cd316df892373"></a>
### 호환성

SQL 표준에는 &lt;call statement&gt;를 사용하도록 되어 있다.

<a id="c3ec1444b7c9768d"></a>
## Procedure Declaration and Definition

<a id="6d96c841bf9a9203"></a>
### 기능

Nested procedure를 선언하고 정의한다.

<a id="48b13d905556e6f2"></a>
### 구문

```
<nested procedure declaration> ::=
        PROCEDURE proc_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
	;

<nested procedure definition> ::=
        PROCEDURE proc_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
        { IS | AS } <item_declaration> BEGIN <pl_stmt_list> END
    ;
```

<a id="c1e1db477854242d"></a>
### 사용 범위 및 접근 권한

PSM declaration section에서 사용할 수 있다.

<a id="585d42a4b7409f97"></a>
### 구문 규칙 및 파라미터

- Proc_name
    - 생성할 procedure의 이름이며, 스키마 내에서 고유한 이름이어야 한다.
    - Procedure 이름의 길이는 128 바이트보다 작아야 한다.
- Param_name
    - Procedure가 사용할 인자의 이름을 정의한다.
    - 각 인자의 이름은 procedure 내에서 고유한 이름이어야 한다.
- Bind_type
    - 각 인자의 bind type을 설정한다. 
    - 표기하지 않을 경우 기본은 'IN' 이다.
- Item_declaration
    - Procedure 내부에서 사용될 로컬 변수등의 item을 선언한다.
    - PL block에서 선언될 수 있는 모든 item들을 선언할 수 있다.
- PL Stmt List
    - Procedure의 body 부분으로써 수행할 PL statement들을 나열한다.

<a id="5a3611048b0f6f2c"></a>
### 설명

Nested procedure는 해당 procedure 내에서만 호출할 수 있는 subprogram이다.   
그 외의 사용 방법은 schema-level procedure와 동일하다.

<a id="a507732fb72a43a4"></a>
### 사용 예

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

<a id="cdaecef6f821cac8"></a>
### 호환성

Schema-level procedure와 동일하다.

<a id="0349f4b04fc4ce9d"></a>
### 참조

자세한 내용은 [CREATE PROCEDURE](27-psm-sql-references.md#e2d083dd25c36aa9)를 참조한다.

<a id="95bd1cadd5b8b6f2"></a>
## RAISE Statement

<a id="c8c6d4c88988be38"></a>
### 기능

사용자가 정의한 exception을 명시적으로 발생시킨다.

<a id="a78ce596096a2776"></a>
### 구문

```
<RAISE Statement> ::= 
    RAISE  <Exception-Name>
    ;
```

<a id="889417c9de4fa031"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="def92337afa95c36"></a>
### 구문 규칙 및 파라미터

- Raise 시킬 exception name이 raise가 속한 PL block이나 상위 PL block의 DECLARE 절에 선언되어야 한다. 단, predefined exception은 선언없이 raise할 수 있다. 
- Raise 문이 exception handler 내에서 사용되면 exception name을 생략할 수 있는데 이 경우, 직전 exception이 상위 블럭으로 전파된다.

<a id="74c286a958f3aea7"></a>
### 설명

Exception이 발생한 PL block에서 처리되지 못하면 상위 PL block으로 전파된다.  
Raise 시킬 exception이 RAISE 구문을 포함하는 PL block 및 상위 PL block 내의 모든 exception handler에 존재하지 않을 경우 에러가 발생한다.  
처리될 때까지 RAISE exception이 발생한 PL block부터 상위로 전파되며 하위 PL block의 exception handler로는 전파되지 못한다.

**User exception 전파**

<a id="a263d61bc6a7eb4a"></a>
| Raise exception | Exception handler  SCOPE | Exception handler | 상위 전파여부 |
| --- | --- | --- | --- |
| User exception without error code | 동일 scope | X | "unhandled exception" 오류를 상위 scope으로 전파한다. |
| User exception with error code | 상위 scope | X | User exception을 전파한다. |
| User exception with error code | 동일 scope | X | User defined error code를 전파한다. |
| User exception with error code | 상위 scope | X | User defined error code를 전파한다. |

<a id="5445bc73131dfa29"></a>
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

<a id="2f7c606a2e8ecdf7"></a>
### 호환성

SQL 표준에는 &lt;handler declaration&gt;과 &lt;condition declaration&gt;은 기술되어 있지만 구문은 지원하지 않는다.

<a id="f37fff52d9c1689c"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Exception Handler](#eb05139898a51758)
- [Exception Declaration](#32065477a17d19d2)

<a id="cf3b00514771d5fd"></a>
## Record Variable Declaration

<a id="338941b5bc7d2bd0"></a>
### 기능

DECLARE 영역에서 record type 변수를 선언한다.

<a id="82d7b2e1d0d2b49a"></a>
### 구문

```
<declare record variable> ::=
    variable_name <recordType> 
    ;

<recordType> ::=
     <tableName>%ROWTYPE
   | USER_DEFINED_DATA_TYPE
```

<a id="c0b06a6828cb5cfb"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 declaration 영역에서만 사용할 수 있다.

<a id="1e95fe1cc8294f68"></a>
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
    - recordType 선언에 대한 자세한 내용은 [User-defined Record Type](20-psm-datatypes.md#74fb126a1c2b9f42)을 참조한다.

<a id="9bb02090fac4396a"></a>
### 설명

- 선언된 변수는 다음과 같은 특징이 있다.
    - 하나의 scope (PL block body) 내에서 고유한 이름이어야 한다.
    - 중첩된 하위의 PL block body에 동일한 이름의 변수를 선언할 수 있다.
    - 중복 선언된 변수를 명확히 사용하기 위해서는 scope_name.variable_name의 형태로 사용해야 한다.
    - Scope 이름을 명시하지 않고 중복 선언된 변수를 사용할 경우에는 자동으로 가장 가까운 scope의 변수가 사용된다.
- 선언된 변수는 해당 scope와 하위 scope에서 사용되며, embedded SQL에서와 달리 ':' 기호를 붙이지 않는다.
- 사용된 변수는 해당 SQL이나 PSM control statement에 대해 bind parameter (INOUT)로 작동한다.

<a id="fd117144cd94504c"></a>
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

<a id="c6825572b45738d6"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="64048fe1b59f6ec4"></a>
## RETURN Statement

<a id="695186d4d2c89e82"></a>
### 기능

Function이 반환할 값을 지정한 후 해당 function을 종료한다. Procedure는 반환값을 지정하지 않고 해당 procedure를 종료한다.

<a id="c9a6ba82d578d912"></a>
### 구문

```
<return statement> ::=
    RETURN [ return_value_expr ]
    ;
```

<a id="18efcfc03a7ff0f5"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="abb8e43ba4eb32b1"></a>
### 구문 규칙 및 파라미터

- Return_value_expr
    - 반환할 값의 표현식으로써 function일 경우에만 명시할 수 있다.

<a id="ef40102a5e34f7d9"></a>
### 설명

현재 수행되고 있는 procedure/ function을 종료한다.  
Function의 경우, RETURN 구문이 수행되지 않고 종료되거나, RETURN 구문이 return_value_expr를 가지지 않으면 오류가 발생한다.

<a id="0cad48edc17762f8"></a>
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

<a id="fa70e8a50a4edaf5"></a>
### 호환성

SQL 표준에는 기술되어 있지만 conformance rule은 존재하지 않는다.

<a id="90e5fdd6ab1f5b23"></a>
## RETURNING INTO clause

<a id="4c1b742292c68a90"></a>
### 기능

Insert/ update/ delete에서 처리된 데이터가 PSM 변수로 반환된다.

<a id="3261478cdc0b43a0"></a>
### 구문

```
<Insert, Delete Returning_into_clause> ::=
      [ RETURN | RETURNING ] { * | { <value_expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]

<Update returning into clause> ::=
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] } INTO Variable [, ...]
```

<a id="65118df7845c0902"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 body 영역에서만 사용할 수 있다.

<a id="19c530dea2b6a676"></a>
### 구문 규칙 및 파라미터

레코드 타입 변수는 다른 타입과 섞어서 사용할 수 없다.

<a id="047aecc18c92af76"></a>
### 설명

Insert/ update/ delete 문을 처리한 before/ after record를 returning into를 통해 저장한다.

<a id="6dea563bf3395dec"></a>
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

<a id="b98c0927e6528cfc"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="2f0223f236e9008c"></a>
## %ROWTYPE Attribute

<a id="5dc89565420b7066"></a>
### 기능

변수를 선언할 때 특정 테이블 또는 커서나 커서 변수의 result set과 같은 구조와 타입으로 정의한다.

<a id="64427a7392943ffa"></a>
### 구문

```
<rowtype attribute> ::=
    <identifier chain> % ROWTYPE
```

<a id="a2d35674fea84cef"></a>
### 사용 범위 및 접근 권한

- PSM 내에서만 사용할 수 있다. (예: package, procedure, function)
- PL block의 declaration 영역에서만 사용할 수 있다.
- 변수를 선언할 때는 &lt;data type&gt; 부분에만 사용할 수 있다
- 레코드 타입의 필드를 선언할 때는 &lt;data type&gt; 부분에 사용할 수 없다. (complex data type은 지원하지 않는다.)

<a id="3a3f009d869fe336"></a>
### 구문 규칙 및 파라미터

- Identifier chain은 다음과 같다.
    - 참조할 테이블, view, synonym의 이름이나 커서 또는 커서 변수의 이름

<a id="30bac31ffde59b03"></a>
### 설명

- 참조 대상 검색 순서
    - 커서 또는 커서 변수 
    - Base table, view, 또는 synonym

- 참조 범위
    - Row attribute를 이용하여 참조할 경우 테이블 또는 커서의 result set에서 column 이름과 타입만 참조한다.
    - 따라서 NOT NULL constraint나 DEFAULT 값 설정 등은 참조하지 않는다.

<a id="0d0f35500eb42a99"></a>
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

<a id="4b00d3392b96cc2f"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="585e7c4d2d8c7d11"></a>
## Scalar Variable Declaration

<a id="4aa80d8ebf4f37c3"></a>
### 기능

DECLARE 영역에서 scalar 변수를 선언한다.

<a id="22516d6cdee810dd"></a>
### 구문

```
<declare scalar variable> ::=
    variable_name <data type> [ <variable initialize clause> ]
    ;

<variable initialize clause> ::=
      [ NOT NULL ] { DEFAULT | := } <value expression>
```

<a id="63f761f3551c59ac"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 declaration 영역에서만 사용할 수 있다.

<a id="34ca6ac374c7b18b"></a>
### 구문 규칙 및 파라미터

- Variable_name
    - 선언할 변수의 이름이다.
    - 변수 이름의 길이는 128 바이트보다 작아야 한다.
    - 하나의 scope (PL block body) 내에서 고유한 이름이어야 한다.
    - 중첩된 하위의 PL block body에 동일한 이름의 변수를 선언할 수 있다.
    - 중복 선언된 변수를 명확히 사용하기 위해서는 scope_name.variable_name의 형태로 사용해야 한다.
    - Scope 이름을 명시하지 않고 중복 선언된 변수를 사용할 경우에는 자동으로 가장 가까운 scope의 변수가 사용된다.
- Data_Type
    - GOLDILOCKS에서 제공하는 모든 built-in [Data Type](../part-03-sql-manual/11-sql-elements.md#2ec7b2e6f23b520c) 들을 사용할 수 있다.
- Value_expression
    - 변수에 지정할 초기값을 표현한다.
    - GOLDILOCKS가 지원하는 모든 상수 및 multi-row 함수들을 제외한 모든 표현식을 사용할 수 있다.

<a id="1a035b9fcb03e8b5"></a>
### 설명

- 선언된 변수는 다음과 같은 특징이 있다.
    - 하나의 scope (PL block body) 내에서 고유한 이름이어야 한다.
    - 중첩된 하위의 PL block body에 동일한 이름의 변수를 선언할 수 있다.
    - 중복 선언된 변수를 명확히 사용하기 위해서는 scope_name.variable_name의 형태로 사용해야 한다.
    - Scope 이름을 명시하지 않고 중복 선언된 변수를 사용할 경우에는 자동으로 가장 가까운 scope의 변수가 사용된다.
- 선언된 변수는 해당 scope와 하위 scope에서 사용되며, embedded SQL에서와 달리 ':' 기호를 붙이지 않는다.
- 사용된 변수는 해당 SQL이나 PSM control statement에 대해 bind parameter (INOUT)로 작동한다.

<a id="bc02faef9fccad43"></a>
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

<a id="5fbdb4d7f9e17c66"></a>
### 호환성

- &lt;declare scalar variable&gt; 구문은 SQL 표준과 비교하여 다음과 같은 차이가 있다.
    - SQL 표준의 &lt;SQL variable declaration&gt;은 PL block body 내 (BEGIN 이후)에서 변수를 선언하지만, GOLDILOCKS는 별도의 declaration section에서 선언한다.
    - SQL 표준에서는 한 번의 DECLARE 구문으로 여러 개의 동일한 타입 변수를 선언할 수 있지만, GOLDILOCKS에서는 한 개의 statement로 한 개의 변수만 선언할 수 있다.
    - SQL 표준에서는 초기값을 설정할 때 DEFAULT 구문만 사용하지만, GOLDILOCKS는 assign 기호인 :=도 사용할 수 있다.

<a id="1f082bdafdc712d3"></a>
## SELECT INTO Statement

<a id="d7ef0b19136db2ef"></a>
### 기능

SELECT를 통해 한 개의 row를 반환 받는다.

<a id="97e92048c377e9c2"></a>
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

<a id="53328a14dd994b60"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="3e1565d4cdad5e63"></a>
### 구문 규칙 및 파라미터

INTO 절을 제외한 사항은 select statement와 동일한 규칙을 따른다.

<a id="95ba8591f625a403"></a>
### 설명

- SELECT INTO는 한 개의 record를 반환받는 용도로 사용한다. 
    - 결과가 0 건인 경우, "NO_DATA_FOUND" exception이 발생한다. 
    - 결과가 두 건 이상인 경우, "TOO_MANY_ROWS" exception이 발생한다. 
- PSM의 record type 변수를 통해 결과를 반환받을 수 있다. 
    - Record type변수를 사용할 경우 다른 타입의 변수와 섞어서 사용할 수 없다.

<a id="6a8e70f346a85275"></a>
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

<a id="68d4d4c6e92126e9"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="255b6ef6b0f171ac"></a>
## SQLCODE Function

<a id="dcafc6b26d906113"></a>
### 기능

PSM에서 수행된 직전 statement의 error code를 반환한다.

<a id="d8b630731c4fdf4b"></a>
### 구문

```
<SQLCODE function> ::= SQLCODE
```

<a id="0ca24c6e0e5e301a"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다.

<a id="7c17638c086eadd2"></a>
### 구문 규칙 및 파라미터

별도의 argument를 갖지 않는다.

<a id="aca1fc0709252b11"></a>
### 설명

PL/ SQL에서 수행된 statement의 error code를 반환한다.  
Error code를 할당하지 않은 user-defined exception의 경우, handler에 의해 처리되는 시점에 1로 반환된다.  
Exception handler에 의해 오류 처리가 완료되면 0으로 반환된다.

<a id="086b1112322b582d"></a>
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

<a id="e721baba3a510c04"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="454c098c81a6e199"></a>
## SQLERRM Function

<a id="b0d4224ca3da7c1b"></a>
### 기능

PSM에서 수행된 직전 statement의 error message를 반환한다.

<a id="0a9515a984cb4451"></a>
### 구문

```
<SQLERRM function> ::= SQLERRM
```

<a id="7e9b3af80d304b27"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다.

<a id="bf2f87f9b773b101"></a>
### 구문 규칙 및 파라미터

별도의 argument를 갖지 않는다.

<a id="d9af46f07cd5c6a1"></a>
### 설명

PL/ SQL에서 수행된 statement의 error message를 반환한다.  
Error code를 할당하지 않은 user-defined exception의 경우, handler에 의해 처리되는 시점에 user-defined exception으로 반환된다.  
Exception handler에 의해 오류 처리가 완료되면 *successful completion* 메세지를 출력한다.

<a id="e491a1293cabf0f9"></a>
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

<a id="510c3ea33e938bf1"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="2ef00c5393d990b1"></a>
## %TYPE Attribute

<a id="3bf3b30502c58f20"></a>
### 기능

변수를 선언할 때나 RECORD 타입의 특정 필드를 정의할 때 그 타입을 특정 테이블의 column 또는 다른 변수와 동일한 타입으로 정의한다.

<a id="7c3e38fd7885fdd2"></a>
### 구문

```
<type attribute> ::=
    <identifier chain> % TYPE
```

<a id="ce5c5ece1d21a098"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 declaration 영역에서만 사용할 수 있다.  
변수를 선언할 때나 레코드 타입의 필드를 선언할 때 &lt;data type&gt; 부분에만 사용할 수 있다.

<a id="e612d6a69819e27b"></a>
### 구문 규칙 및 파라미터

- Identifier_chain
    - 참조할 테이블의 column 또는 기존에 선언된 변수 (혹은 변수의 필드)의 이름이다.

<a id="856cdef6c81c1516"></a>
### 설명

<a id="a3f02e2ef08b837f"></a>
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

<a id="3e017f9c87dbad10"></a>
#### NOT NULL Constraints 변수 참조

NOT NULL 속성의 변수를 참조할 때는 초기값을 참조하지 않으므로 반드시 새로운 초기값을 지정해야 한다.   
현재 record type 변수의 필드에 대한 type attribute를 사용할 때 필드 초기값 설정을 지원하지 않으므로 NOT NULL 타입의 필드는 참조할 수 없다.

<a id="aa23cc2f25a61a0e"></a>
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

<a id="551b9722d3d73f0e"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="c20ebeede621fc13"></a>
## UPDATE Statement Extension

<a id="a28b8e373151023d"></a>
### 기능

PSM에서 UPDATE 문의 갱신 대상 column을 나열하는 방식 외에 추가적으로 record type 변수를 이용하여 레코드를 갱신한다.   
PSM에서 UPDATE (searched) RETURNING INTO 절에 record type 변수를 사용하여 결과를 저장한다.

<a id="03d4ba2926fe1bfa"></a>
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

<a id="6f99c53fb1d8ba76"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="de823ca681687a3d"></a>
### 구문 규칙 및 파라미터

- UPDATE SET ROW 구문에서 사용할 &lt;PSM_Variable&gt;은 반드시 record type으로 선언된 변수이어야만 한다.
- UPDATE RETURNING INTO 구문에서 사용할 &lt;Variable&gt;은 record type이 아니어도 된다.
    - 단, record type으로 기술한 경우 다른 데이터 타입의 변수와 섞어서 사용하거나 두 개 이상의 record type 변수를 나열할 수 없다.

<a id="50c60fd981035a12"></a>
### 설명

PSM에서 record type 변수를 통해 레코드를 갱신하거나 RETURNING INTO의 결과를 저장한다.

<a id="f6f7fee8d6352f52"></a>
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

<a id="ed1a2827df273766"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="88d89a28984cde15"></a>
## WHILE LOOP Statement

<a id="c28422f237b7e3c9"></a>
### 기능

&lt;search condition&gt;이 TRUE 값을 반환하는 동안 내부의 statement들을 수행한다.

<a id="0e3bf9a8f2616367"></a>
### 구문

```
<while loop statement> ::=
    WHILE <search condition>
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="0e71516c319bcd86"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
&nbsp;PL block의 body 영역에서만 사용할 수 있다.

<a id="c1e61c5b510b4b0f"></a>
### 구문 규칙 및 파라미터

- Search condition은 다음과 같다.
    - while 루프를 계속 순환하는 조건 표현식이다.
    - 최종적으로 boolean 타입을 반환해야 한다.

<a id="84c11330c133a05b"></a>
### 설명

while loop 구문은 &lt;search condition&gt;의 평가 결과가 TRUE인 동안 내부의 statement list를 수행한다.

<a id="6de1dc22df31ba85"></a>
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

<a id="1df9e56c2fa97bf2"></a>
### 호환성

&lt;while loop statement&gt; 구문은 SQL 표준에 &lt;while statement&gt;로 정의되어 있다.  
SQL 표준의 &lt;while statement&gt;는 loop 구문을 DO ... END WHILE로 수행하는 반면에 GOLDILOCKS는 LOOP ... END LOOP로 수행한다.

<a id="92533d93592db4e9"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CONTINUE Statement](#ffc467958d2152c5)
- [EXIT Statement](#b8d97bb30e1e9154)
- [GOTO Statement](#d1563db2fb06a6c5)

---

[← 25. PSM Packages](25-psm-packages.md) · [전체 목차](../README.md) · [27. PSM SQL References →](27-psm-sql-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
