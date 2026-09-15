<a id="7c14bcafbb8d27b1"></a>

# 23. PSM Language Element References

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/7c14bcafbb8d27b1)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 22. Using SQLs in PSM](22-using-sqls-in-psm.md) · [전체 목차](../README.md) · [24. PSM SQL References →](24-psm-sql-references.md)

<a id="e607e1afbf5ec88a"></a>
## Assignment Statement

<a id="718222b6bc21444f"></a>
### 기능

PSM block의 내부에서 변수나 out-bind parameter에 값을 저장한다.

<a id="15845f47d43d8353"></a>
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

<a id="8fa3112935944b68"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="1edf0cf07d288e9d"></a>
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

<a id="8aba200fe099706b"></a>
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

<a id="f262e7123c3cfd28"></a>
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

<a id="da1078373bab5b52"></a>
### 호환성

&lt;assignment statement&gt; 구문은 SQL 표준과 비교하여 다음과 같은 차이가 있다.

- SQL 표준의 assignment statement는 singleton variable assignment와 multiple variable assignment를 정의하지만, GOLDILOCKS는 singleton variable assignment 형식만 지원한다. 
- SQL 표준의 assignment statement는 SET 키워드로 시작하지만, GOLDILOCKS는 SET 키워드를 사용하지 않는다. 
- SQL 표준의 assignment statement는 target과 value 사이에 equal operator (=)를 사용하지만, GOLDILOCKS는 := 를 사용한다.

**SQL 표준 호환성**

<a id="d08014798a11935d"></a>
<table><tbody><tr><th align="center">Feature ID</th><th align="center">설명</th><th align="center">지원 여부</th></tr><tr><td align="left">P002</td><td align="left">Computational completeness</td><td align="center">X</td></tr><tr><td align="left">P006</td><td align="left">Multiple assignment</td><td align="center">X</td></tr></tbody></table>

<a id="f1fcc99ad23242ca"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Scalar Variable Declaration](#fd818983e72539e7)
- [Record Variable Declaration](#4bc9c352a656a41c)
- [COLLECTION Variable Declaration](#7fa00b668e21b11c)
- [Cursor Variable Declaration](#e6d4ef5813d5c256)

<a id="7bc0e49d642adbd1"></a>
## Basic LOOP Statement

<a id="cf8854d66fd54a93"></a>
### 기능

GOTO나 EXIT 등이 수행되어 LOOP를 종료하기 전까지 LOOP 내부의 statement들을 반복 수행한다.

<a id="b5320baa298ef72e"></a>
### 구문

```
<basic loop statement> ::=
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="8c5b6232702ee109"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="df1c69ef2b75b272"></a>
### 구문 규칙 및 파라미터

- loop_name
    - &lt;basic loop statement&gt;의 label 이름이다. 
    - Comment의 역할만 하기 때문에 실제 &lt;basic loop statement&gt;의 label 이름과 달라도 무방하다.

<a id="06172d3578444c9b"></a>
### 설명

Basic loop 구문은 LOOP 내부의 statement들을 반복 수행한다.  
Basic loop 구문은 loop 계열 statement이므로 GOTO, EXIT, CONTINUE가 label로 지칭하는 target statement가 될 수 있다.

<a id="1083cf7a65d59849"></a>
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

<a id="b6efa41913e414b2"></a>
### 호환성

&lt;basic loop statement&gt; 구문은 SQL 표준의 &lt;loop statement&gt;와 동일하다.

**SQL 표준 호환성**

<a id="e53bbe413b108bb8"></a>
| Feature ID | 설명 | 지원여부 |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="0fb6dcd248209596"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CONTINUE Statement](#6dc86c314905ec09)
- [EXIT Statement](#c02a4714e78afa89)
- [GOTO Statement](#712fd8282104fa49)

<a id="b678ebcaaabaf1c3"></a>
## Block (BEGIN .. END)

<a id="c55b6f1087e30875"></a>
### 기능

새로운 scope를 생성하며, 변수, 커서, 타입과 exception 등을 정의한다.

<a id="92ad559a662173c9"></a>
### 구문

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

<a id="138eac9f467b03c5"></a>
### 사용 범위 및 접근 권한

PROCEDURE, FUNCTION 또는 anonymous block 내에서만 사용할 수 있다.

<a id="1784604cd4ef2ee5"></a>
### 구문 규칙 및 파라미터

- Variable declaration
    - Block 내에서 사용할 scalar/ record/ array 타입의 변수들을 선언한다
- Cursor variable declaration
    - Block 내에서 사용할 cursor 변수들을 선언한다.
- Cursor declaration
    - Block 내에서 사용할 cursor를 선언한다.
- Type declaration
    - Block 내에서 변수를 선언할 때 사용할 사용자 정의 타입들을 선언한다.
- Exception declaration
    - Exception 처리 구문에서 처리될 exception들을 정의한다.
- Static SQL
    - PSM에서 수행할 수 있는 Data Manipulation Language (DML)과 Data Control Language (DCL)를 가리킨다.
- Dynamic SQL
    - GOLDILOCKS PSM에서 지원하는 동적 질의 처리 관련 구문들을 가리킨다.
- PSM control statement
    - GOLDILOCKS PSM에서 지원하는 각종 flow control 구문들을 가리킨다.

<a id="932968edd44c1540"></a>
### 설명

&lt;psm block&gt;은 PSM의 기본 구성 요소이다.  
Bock은 선언부 (declaration part)와 예외 처리부 (exception handling part)를 가질 수 있다.  
Block은 중첩될 수 있고 중첩된 block은 새로운 하위 변수 scope를 가진다. 상위 block은 하위 block의 변수를 참조할 수 없다.

<a id="de35b685b5b210cf"></a>
### 사용 예

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

<a id="d0db864076e12d09"></a>
### 호환성

SQL 표준의 &lt;compound statement&gt;는 새로운 savepoint를 지정하는 ATOMIC/ NOT ATOMIC 구문을 정의하였지만, GOLDILOCKS는 이를 지원하지 않는다.

**SQL 표준 호환성**

<a id="06ceba783a1870d9"></a>
| Feature ID | 설명 | 비고 |
| --- | --- | --- |
| P002 | Computational completeness | ATOMIC 구문을 지원하지 않는다. |

<a id="5b81d14d18156310"></a>
### 참조

자세한 내용은 [Overview of PSM](17-overview-of-psm.md#27c58eaf6b2077d4)을 참조한다.

<a id="d542d13e5026a54e"></a>
## CASE Statement

<a id="91b6413b224e2615"></a>
### 기능

주어진 여러 조건들 중에 TRUE를 반환하는 조건에 해당하는 statement list를 수행한다.

<a id="1f13ea3078396b74"></a>
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

<a id="0595eaa9f131f38c"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="847e5c75c24d3039"></a>
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

<a id="242d14ebaec8d716"></a>
### 설명

IF 구문과 유사하게 조건들을 평가하여 TRUE를 반환하는 WHEN 절의 statement들을 수행한다.  
순서대로 먼저 나오는 조건식부터 평가하여 해당 조건식이 TRUE인 경우, 그 이후의 조건식들은 평가하지 않는다.  
만일 조건식에 해당하는 경우가 존재하지 않고 ELSE 절이 기술되지 않은 경우에는 에러가 발생한다.

<a id="505920312ce9edec"></a>
### 사용 예

<a id="b0513a523c93235c"></a>
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

<a id="76523b6ed2a537b4"></a>
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

<a id="d3e87011548897b0"></a>
### 호환성

SQL 표준의 CASE 구문은 row 타입 (list 타입) value 간의 비교를 정의하였지만, GOLDILOCKS는 지원하지 않는다  
SQL 표준의 CASE 구문은 &lt;when operand&gt;에 ','로 구분되는 여러 조건들을 리스트로 정의할 수 있지만, GODILOCKS는 지원하지 않는다.

**SQL 표준 호환성**

<a id="6cc31f84eb414ee6"></a>
| Feature ID | 설명 | 비고 |
| --- | --- | --- |
| P002 | Computational completeness | P004, P008을 지원하지 않는다. |
| P004 | Extended CASE statement | - |
| P008 | Comma-separated predicates in simple CASE statement | - |

<a id="e7fbe6f6f64c9346"></a>
## CLOSE Statement

<a id="404e1753aef0fe62"></a>
### 기능

Open 상태인 cursor를 닫는다.

<a id="7cb646ccbbb992eb"></a>
### 구문

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="36a44629880e0f67"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="480acbadb57c7397"></a>
### 구문 규칙 및 파라미터

- cursor_name
    - Close 할 cursor의 이름이다.

<a id="e93790c53f88d491"></a>
### 설명

Open 상태인 cursor를 닫는다.  
Close 된 상태인 cursor는 open 구문을 사용하여 다시 open 할 수 있다.

<a id="6534b48f817986fb"></a>
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

<a id="f2cae7b2885672da"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="840a3fffee90e71c"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [FETCH Statement](#594c76c9a93d727b)
- [OPEN Statement](#70cbb007421a6edc)

<a id="8c381b928b4415ca"></a>
## Collection Method Invocation

<a id="5e1b9d3eb5313480"></a>
### 기능

Collection type의 변수를 탐색할 수 있는 method를 제공한다.

<a id="8f949a59e44c0a00"></a>
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

<a id="ef79f20126abdb2c"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="73d44fa7000e7e89"></a>
### 구문 규칙 및 파라미터

- Collection type으로 선언된 변수에만 사용할 수 있다.
- FIRST, LAST, COUNT는 parameter를 가질 수 없다.
- PRIOR, NEXT, EXISTS, DELETE와 같이 대상을 지정해야 할 경우에는 parameter를 명시해야 한다.
- DELETE의 경우에는 PSM statement와 같이 동작하며 다른 변수로 결과를 반환할 수 없다. (Expression에 사용할 수 없다.)

<a id="38bec2c45d264e41"></a>
### 설명

다음 표를 참조한다.

**함수**

<a id="4a71714a9bc76588"></a>
| 함수명 | 기능 | 반환값 | 인자 필요여부 |
| --- | --- | --- | --- |
| FIRST | 가장 작은 key를 반환한다. | INDEX OF에 지정된 key type | X |
| LAST | 가장 큰 key를 반환한다. | INDEX OF에 지정된 key type | X |
| PRIOR | 입력된 key보다 작은 key를 반환한다. | INDEX OF에 지정된 key type | O |
| NEXT | 입력된 key보다 큰 key를 반환한다. | INDEX OF에 지정된 key type | O |
| COUNT | 저장된 개수를 반환한다. | INTEGER | X |
| DELETE | Key에 해당하는 값을 삭제한다. | N/A | O |
| EXISTS | Key의 존재 유무를 반환한다. | BOOLEAN | O |

<a id="1222e3a84573ba96"></a>
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

<a id="95c37b1a8ed2a20f"></a>
### 참조

자세한 내용은 [COLLECTION Variable Declaration](#7fa00b668e21b11c)을 참조한다.

<a id="7fa00b668e21b11c"></a>
## COLLECTION Variable Declaration

<a id="f4c2921300999436"></a>
### 기능

Collection 변수를 선언한다.

<a id="1d1a1d3d0f00bb7b"></a>
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

<a id="06f45faf0143c037"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 declaration 영역에서만 사용할 수 있다.

<a id="1ad0886e721d4ee8"></a>
### 구문 규칙 및 파라미터

- Type-name
    - 사용자가 사용할 collection type의 이름을 지정한다. 
- Element-type
    - Collection 변수에 저장될 element의 type을 지정한다. 
- Index-type
    - Collection 변수에 저장된 key의 data type을 지정한다.

<a id="95f5942f4ab17491"></a>
### 설명

Collection type을 선언한다.

<a id="9b4337219a142970"></a>
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

<a id="07d843572bc1ca01"></a>
### 호환성

SQL 표준에서는 정의하지 않고 있다.

<a id="b18c75d55cfa1a70"></a>
### 참조

자세한 내용은 [Collection Method Invocation](#8c381b928b4415ca)을 참조한다.

<a id="6dc86c314905ec09"></a>
## CONTINUE Statement

<a id="81080abab1eb74df"></a>
### 기능

현재 진행 중인 statement list의 수행을 중지하고, 상위 loop statement의 다음 iteration을 수행한다.

<a id="15160c299e98764d"></a>
### 구문

```
<continue statement> ::=
    CONTINUE [ label_name ] [ WHEN condition ] 
    ;
```

<a id="2441b6f81eefe944"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

Target label을 가진 statement는 다음 loop 계열 statement 중 하나이어야 한다.  

• basic loop statement  
• for loop statement  
• while statement  
• forall statement

<a id="1b300053018a2c60"></a>
### 구문 규칙 및 파라미터

- Label name
    - identifier chain의 형식을 가질 수 있다.
- Condition
    - 명시된 경우, 해당 조건이 TRUE일 때만 loop statement로 복귀한다.

<a id="2bd299329bfb11a3"></a>
### 설명

현재 진행 중인 statement list의 수행을 중지하고 상위 loop statement로 복귀한다.

Label이 명시되면 해당 label 이름을 가진 상위 loop statement로 복귀한다.  
Label이 명시되어 있지 않으면 가장 가까운 상위 loop statement로 복귀한다.  
같은 label 이름을 가진 여러 개의 상위 statement들이 존재할 경우, 가장 가까운 statement가 선택된다.  
현재 위치에서 visible한 (중첩된 scope 내에 존재하는) loop statement로만 복귀할 수 있다.

조건이 명시되면 해당 조건이 TRUE인 경우에만 복귀한다.  
조건이 명시되지 않으면 무조건 복귀한다.

<a id="d9b00b5e1ba4d03f"></a>
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

<a id="e7d4f0db96407920"></a>
### 호환성

&lt;continue statement&gt; 구문은 SQL 표준의 &lt;iterate statement&gt;와 기능이 유사하다.  
단, &lt;iterate statement&gt; 구문은 WHEN condition 기능을 제공하지 않는다.

<a id="2ae3e9e8c0dc4f7e"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [EXIT Statement](#c02a4714e78afa89)
- [GOTO Statement](#712fd8282104fa49)

<a id="42ffd9ff0aa0ebe6"></a>
## Cursor FOR LOOP Statement

<a id="e4d7c3c841533e67"></a>
### 기능

PSM에서 사용자가 선언한 cursor나 query에 의해 생성된 result의 row 개수만큼 loop를 수행한다.

<a id="b7b4f277b351a37d"></a>
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

<a id="1212f38d2dc29d4c"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PSM 내의 body에서만 사용할 수 있다.

<a id="dabc97b0eb4a6863"></a>
### 구문 규칙 및 파라미터

For~Loop 내에 선언된 변수는 해당 loop scope 내에서만 유효하다. (해당 Cursor For Loop Block Scope 밖에서는 해당 변수를 참조할 수 없다.)

<a id="7afda09688c483c4"></a>
#### Cursor Name을 사용하는 경우

Cursor name을 사용하여 LOOP를 수행할 경우 cursor가 미리 선언되어 있어야 한다.   
Actual param에 대한 자세한 내용은 [OPEN Statement](#70cbb007421a6edc)를 참조한다.

<a id="12211eb27bc9f918"></a>
#### Cursor Query를 사용하는 경우

Select나 returning query와 같이 GOLDILOCKS 내부적으로 implicit cursor로 처리되는 질의만 수행할 수 있다.

<a id="d10e805bb0929d10"></a>
### 설명

Cursor가 생성한 결과 개수만큼 loop를 돌면서 loop 내의 PSM statements를 수행한다.   
LOOP 중에 cursor가 invalid한 상태가 (예: closed) 되면 더 이상 loop를 수행하지 않고 오류로 처리한다.   
Explicit cursor name을 명시할 경우, 해당 cursor가 already opened이면 오류로 처리한다.

FOR LOOP 절에 명시된 cursor의 결과를 반환받는 변수는 자동으로 생성된다. (Cursor의 실행 결과에 의해 반환될 result set의 row type으로 생성된다.)   
다만, 사용자의 cursor query 결과 중 특정 테이블의 column이 아닌 select target expression에 대해 alias 등을 지정하지 않을 경우, 오류가 발생할 수 있다.

<a id="28aebda1e132f4ac"></a>
### 사용 예

<a id="6fb9d707e7415d28"></a>
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

<a id="a5d0d90c5d5beaae"></a>
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

<a id="198b2fe8de81e8aa"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Explicit Cursor Declaration and Definition](#bcf218929fe74018)
- [GOTO Statement](#712fd8282104fa49)
- [EXIT Statement](#c02a4714e78afa89)

<a id="e6d4ef5813d5c256"></a>
## Cursor Variable Declaration

<a id="3655afba0d137772"></a>
### 기능

PSM의 DECLARE section에서 cursor variable을 선언한다.

<a id="64f958c4c637d6d9"></a>
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

<a id="be1f7b9efd10b24b"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PSM의 declaration 영역에서만 사용할 수 있다.

<a id="dc4b195f91f59139"></a>
### 구문 규칙 및 파라미터

Cursor 변수의 초기값 지정이나 assign은 cursor 변수 사이에서만 가능하다.

<a id="fd9597d0da2f2ed0"></a>
### 설명

Cursor variable은 특정 cursor에 종속되지 않는 cursor를 가리키는 일종의 pointer 역할을 한다.

<a id="a3bf94cc52364a26"></a>
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

<a id="d6a1bb11e572fa3b"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [OPEN Statement](#70cbb007421a6edc)
- [FETCH Statement](#594c76c9a93d727b)
- [CLOSE Statement](#e7fbe6f6f64c9346)

<a id="06dfa0a44fbe8de5"></a>
## DELETE Statement Extension

<a id="1612336438aabc95"></a>
### 기능

PSM의 record type 변수를 이용하여 RETURNING INTO 절에 결과를 저장할 수 있다.

<a id="4632879ef9c1c050"></a>
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

<a id="52cf8e48964b1095"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PSM의 body 영역에서만 사용할 수 있다.

<a id="ef58aac6e031c2bb"></a>
### 구문 규칙 및 파라미터

Returning Into를 통해 반환받을 변수의 타입이 record-type인 경우 다른 변수 타입과 섞어서 사용할 수 없다.

<a id="b8378962f13ef447"></a>
### 설명

PSM의 record type 변수를 이용하여 RETURNING INTO 절에 결과를 저장할 수 있다.

<a id="ac7e421591577855"></a>
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

<a id="864abbbc8c8961c9"></a>
### 참조

자세한 내용은 [데이터 삭제](../part-03-sql-manual/12-sql-languages.md#781319f1ae858afa)를 참조한다.

<a id="2d7e16c1ac847601"></a>
## EXCEPTION_INIT Pragma

<a id="cfaaa8d6f46468bf"></a>
### 기능

PL block 내의 internally defined exception을 정의한다.

<a id="1813845dcfade507"></a>
### 구문

```
< PRAGMA EXCEPTION_INIT > ::=
     PRAGMA EXCEPTION_INIT ( <Exception-Name>, <Internal-ErrorCode> ) 
     ;
```

<a id="ff99089cbea60172"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PSM의 declaration 영역에서만 사용할 수 있다

<a id="81260802f9114aaa"></a>
### 구문 규칙 및 파라미터

Predefined exception은 argument로 사용되는 exception name에 사용할 수 없다. (predefined exception name은 선언할 수 없다.)   
동일한 PL BLOCK DECLARE 절에 argument로 사용되는 exception name이 반드시 미리 선언되어야 한다. (다른 BLOCK의 exception name 선언을 참조할 수 없다.)   
&lt;Internal-ErrorCode&gt;는 DB SYSTEM 내에 존재하는 내부 error code이어야 한다. (SUCCESS 코드는 설정할 수 없다.)

<a id="b8d67ca732242ddd"></a>
### 설명

사용자가 DB SYSTEM의 error code에 대응하는 exception name을 명시적으로 선언한다.

<a id="b0ecaf230bcaa01d"></a>
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

<a id="e20cc8d7bcadc6e4"></a>
### 호환성

Error code는 각 벤더마다 다르기 때문에 서로 호환되지 않는다.

<a id="5b2772b99ae06f32"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Exception Declaration](#480c66a8f8725127)
- [Exception Handler](#9f9d440cbf4130a1)

<a id="480c66a8f8725127"></a>
## Exception Declaration

<a id="c3cb3ea4bbb455f4"></a>
### 기능

PL block 내의 exception name을 선언한다.

<a id="46cd57e1b032417d"></a>
### 구문

```
< Exception-Declaration Statement > ::=
     <Exception-Name>  EXCEPTION 
     ;
```

<a id="6c259cfbdfbcb860"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PSM의 declaration 영역에서만 사용할 수 있다.

<a id="d39096a4a7da4a30"></a>
### 구문 규칙 및 파라미터

Predefined exception name은 선언할 수 없다.   
동일한 SCOPE의 DECLARE 절에 중복으로 선언할 수 없다.

<a id="a95cc01a91fa370b"></a>
### 설명

사용자가 명시적으로 exception을 선언한다.

<a id="be09653e99e9cb70"></a>
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

<a id="635b839a78707df1"></a>
### 호환성

표준 SQL의 exception 선언은 다음과 같지만 GOLDILOCKS는 위와 같은 구문을 지원한다.

```
<condition declaration> ::=
DECLARE <condition name> CONDITION [ FOR <sqlstate value> ]
```

<a id="425f8920d2c3bd11"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Exception Declaration](#480c66a8f8725127)
- [EXCEPTION_INIT Pragma](#2d7e16c1ac847601)

<a id="9f9d440cbf4130a1"></a>
## Exception Handler

<a id="ca05f8fb84a406e3"></a>
### 기능

PL/ SQL을 수행하는 중에 발생한 DB SYSTEM 상의 오류로 인한 암묵적 exception이나 사용자가 명시적으로 발생시킨 exception에 대해 정의된 동작을 수행한다.

<a id="fda3e46d470234b7"></a>
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

<a id="93ca70fb7db687f5"></a>
### 사용 범위 및 접근 권한

PL block 내에서 사용할 수 있다.

<a id="13d79ca16636c255"></a>
### 구문 규칙 및 파라미터

Predefined exception인 OTHERS는 OR을 사용하여 다른 exception name과 함께 기술할 수 없다.   
Predefined exception인 OTHERS는 exception handler에 중복으로 기술할 수 없으며 가장 마지막에 기술하여야 한다.

<a id="8a08efd91782047b"></a>
### 설명

<a id="ed2ac0a0f5023a30"></a>
#### Exception 유형

<a id="4fb9e09ffbaca785"></a>
| Type | Definer | Has error | Has name | Raise implicitly | Raise explicitly |
| --- | --- | --- | --- | --- | --- |
| Predefined | System | Yes | Yes | Yes | Optionally |
| User-defined | User | If user assign | If user assign | No | Yes |

Predefined exception은 GOLDILOCKS에서 미리 지정한 exception name과 error code를 갖는다.   
그 외의 exception은 GOLDILOCKS 내부의 오류 코드 이름을 사용자가 predefined exception name과 다르게 설정하는 경우 (internally defined)와 별도의 error code를 지정하지 않고 exception name만 선언하는 경우 (user-defined)로 나누어진다.

<a id="de2e68f29c9be46a"></a>
#### Predefined Exception

**Predefined exception 유형**

<a id="9e721a218448234c"></a>
| 이름 | 설명 |
| --- | --- |
| CASE_NOT_FOUND | CASE WHEN의 모든 조건에 맞지 않거나 ELSE 절이 정의되지 않았다. |
| DUP_VAL_ON_INDEX | INDEX duplicated 오류가 발생하였다. |
| INVALID_CURSOR | Cursor 상태가 올바르지 않다. |
| INVALID_NUMBER | 숫자로 변환할 수 없다. |
| NO_DATA_FOUND | SELECT 문이 0 건의 데이터를 반환한다. |
| ROWTYPE_MISMATCH | 두 개의 RowType 변수의 필드 타입이 서로 다르다. |
| TOO_MANY_ROWS | 두 건 이상의 row를 반환한다. |
| VALUE_ERROR | Type mismatch, invalid casting 같은 error이다. |
| ZERO_DIVIDE | 0으로 나누기를 시도한다. |
| OTHERS | Predefined에 정의되지 않은 오류를 포함한다. |

<a id="1ed8e08322cdba1c"></a>
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

<a id="4bd5a3df2ab7a036"></a>
### 호환성

SQL 표준 문법을 지원하지 않는다.

<a id="f3e947dfaed6d820"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [EXCEPTION_INIT Pragma](#2d7e16c1ac847601)
- [Exception Declaration](#480c66a8f8725127)

<a id="56868d6728d2874b"></a>
## EXECUTE IMMEDIATE Statement

<a id="799b25d4190896a5"></a>
### 기능

PSM 내에서 dynamic SQL을 실행한다.

<a id="bcd2a0a42d8a1ad9"></a>
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

<a id="4e7f49f2eec0338f"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="fb73d27e36d625d3"></a>
### 구문 규칙 및 파라미터

<a id="72c21e7771d6559b"></a>
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

<a id="c55d11fa22e5719b"></a>
#### INTO Clause

Dynamic SQL 수행 결과가 존재하고 marker를 통해 binding된 경우가 아닌 SQL 문의 처리 결과를 반환 받는 경우이다. (내부적으로 implicit cursor fetch 형태이다.)   
구문은 다음과 같다.

```
EXECUTE IMMEDIATE 'SELECT ... FROM .. WHERE ...';
EXECUTE IMMEDIATE 'INSERT ... RETURNING ...';
EXECUTE IMMEDIATE 'UPDATE ... RETURNING ...';
EXECUTE IMMEDIATE 'DELETE ... RETURNING ...';
```

<a id="7664d9a19d8d59c4"></a>
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

<a id="2f19f5060f2aedf0"></a>
#### RETURNING Clause

INSERT/ UPDATE/ DELETE RETURNING INTO 구문이 dynamic SQL로 사용된 경우, GOLDILOCKS는 USING 절에 기술된 변수를 OUT mode로 binding하여 결과를 반환받을 수 있다.   
다른 DBMS와의 호환을 위해 RETURNING INTO 절로도 동일한 결과를 반환받을 수 있다.

<a id="8e9feff9a4eea173"></a>
#### 기타 규칙

- DDL/ DCL은 어떤 BIND 절 (INTO, USING, RETURNING clause)도 사용할 수 없다. 
- INTO 절과 RETURNING INTO 절에는 OUT으로 쓰이기 때문에 별도의 bind type을 지정할 수 없으며 동시에 같이 사용할 수도 없다. 
- IN BIND type은 scalar type 변수만 사용할 수 있다. 
- OUT BIND type은 record type 변수를 사용할 수 있다. 하지만 scalar나 record 타입을 섞어서 동시에 나열할 수는 없다. 
- INTO 절과 USING OUT 또는 RETURNING INTO를 통해 결과를 나누어 받을 수 없다.

<a id="cd4a261508281933"></a>
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

<a id="54e333b98ef6fa58"></a>
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

<a id="c02a4714e78afa89"></a>
## EXIT Statement

<a id="f265dc9d9c03112b"></a>
### 기능

상위 loop statement들 중에서 주어진 label을 가진 loop statement를 탈출하여 그 다음 statement를 수행한다.

<a id="8d38d4a1473a0675"></a>
### 구문

```
<exit statement> ::=
    EXIT [ label_name ] [ WHEN condition ]
    ;
```

<a id="b273b532b1c1fab2"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="a440a0cf1d068398"></a>
### 구문 규칙 및 파라미터

- Label name
    - 탈출할 loop statement의 label 이름이다.
    - Identifier chain 형식을 가질 수 있다.
- Condition
    - 조건을 명시할 경우, 해당 조건이 TRUE일 경우에만 loop statement를 탈출한다.

<a id="3ee0a561bc55e468"></a>
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
- 현재 위치에서 visible 한 (중첩된 scope내에 존재하는) loop statement만 탈출할 수 있다.

- 조건 (condition)이 명시된 경우, 해당 조건이 TRUE인 경우에만 탈출한다.
- 조건이 명시되지 않은 경우, 무조건 탈출한다.

<a id="200c9acc05145056"></a>
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

<a id="8c2679af527b23f6"></a>
### 호환성

SQL 표준에는 존재하지 않는다.

<a id="41aeb261c0513fce"></a>
## Explicit Cursor Attribute

<a id="e86fcac0f654d350"></a>
### 기능

PSM에서 정의된 cursor의 상태값을 반환한다.

<a id="c4b05c007871bccb"></a>
### 구문

```
<Explicit cursor attribute> ::=
    cursor_name '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="10c290d6065fc6ab"></a>
### 사용 범위 및 접근 권한

PSM 내의 body 영역에서만 사용할 수 있다.

<a id="4f18391b53734403"></a>
### 구문 규칙 및 파라미터

- Cursor_name
    - 상태값을 알고 싶은 커서의 이름이다.

<a id="2bcf9c53af165f93"></a>
### 설명

- 주어진 커서의 상태값을 반환한다. 
    - ISOPEN: 현재 커서가 OPEN 상태인지 여부이다.
    - FOUND: 최근 fetch에 의해 데이터가 반환되었는지 여부이다.
    - NOTFOUND: FOUND의 반대이다.
    - ROWCOUNT: 커서가 최근에 OPEN 된 후 fetch 한 record의 개수이다.
- 커서 상태에 따라 다음과 같은 값들을 반환한다.

**수행 시점에 따른 결과**

<a id="afda653bfdc025d3"></a>
| Attribute 이름 | OPEN 전 | OPEN 후 | FETCH 후 | CLOSE 후 |
| --- | --- | --- | --- | --- |
| ISOPEN | FALSE | TRUE | TRUE | FALSE |
| FOUND | NULL | NULL | TRUE/ FALSE | NULL |
| NOTFOUND | NULL | NULL | TRUE/ FALSE | NULL |
| ROWCOUNT | NULL | NULL | N (개수) | NULL |

<a id="b659a39de82442f4"></a>
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

<a id="bccf5675bded0a5c"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="bcf218929fe74018"></a>
## Explicit Cursor Declaration and Definition

<a id="32853e4136df1a80"></a>
### 기능

PSM의 DECLARE section에서 커서를 선언한다.

<a id="145924e45affc8f4"></a>
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

<a id="6296e07558ba4391"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function )   
PL block의 declaration 영역에서만 사용할 수 있다

<a id="aa714523b183945b"></a>
### 구문 규칙 및 파라미터

<a id="c7420917fd4543db"></a>
#### Cursor Name

선언할 커서의 이름이다.  
커서 이름의 길이는 128 바이트보다 작아야 한다.  
해당 scope 내에서 고유한 이름이어야 한다.

<a id="7e103bc958bd2dc6"></a>
#### RowType

커서의 레코드 타입을 정의한다.  
커서를 정의할 때 명시된 select target들의 개수가 같아야 하며, 데이터 타입이 호환되어야 한다.  
Rowtype을 지정하지 않을 경우, cursor를 정의할 때 기술된 select_statement의 SELECT target에 적합한 rowtype이 자동으로 지정된다.

<a id="475f08368f1b6743"></a>
#### Param Name

특정 커서 내에서 parameter를 구별하는 이름이다.  
해당 커서 내에서 고유한 이름이어야 한다.  
만일 참조 가능한 scope 내의 다른 변수와 이름이 같을 경우, 해당 커서의 parameter를 우선적으로 참조한다.

<a id="26aca5e160e948f3"></a>
#### DataType

해당 parameter의 데이터 타입을 지정한다.  
GOLDILOCKS에서 제공하는 모든 built-in 타입과 PSM 내에 정의된 타입을 사용할 수 있다.  
단, built-in 타입에는 범위를 제한하는 구문 (precision/ scale)을 지정할 수 없고 내부적으로 해당 데이터 타입의 최대 범위로 지정된다.

<a id="80651d5efacfde80"></a>
#### Select Statement

커서가 수행할 SELECT 또는 SELECT ... FOR UPDATE 구문을 지정한다.  
SELECT ... INTO 구문은 사용할 수 없다.

<a id="aa74b610ba93088d"></a>
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

<a id="c66e3e0140a278b0"></a>
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

<a id="8f03c18fc3a34074"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="c67f1496d8a436f1"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [OPEN FOR Statement](#e42e171c8ed8be7c)
- [FETCH Statement](#594c76c9a93d727b)
- [CLOSE Statement](#e7fbe6f6f64c9346)

<a id="594c76c9a93d727b"></a>
## FETCH Statement

<a id="0b107bee5fd448de"></a>
### 기능

OPEN 된 cursor의 레코드를 한 건 가져온다.

<a id="bbd016f33bcae212"></a>
### 구문

```
<fetch statement> ::=
    FETCH cursor_name <into clause>
    ;

<into clause> ::=
    INTO { variable [ , variable ] .. | record }
```

<a id="20eb95213a5c706e"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="172969185310ddab"></a>
### 구문 규칙 및 파라미터

- Cursor name
    - Fetch 할 cursor name이다.
- Variable
    - Fetch한 결과 중에 한 개의 column 값을 저장할 scalar 타입의 변수 또는 bind parameter이다.
- Record
    - Fetch한 결과인 한 개의 레코드 전체를 저장할 record 타입의 변수이다.

<a id="4769f8617b3cf3b0"></a>
### 설명

Open 된 커서로부터 레코드 한 개를 fetch하여 INTO 절에 명시된 변수로 값을 복사한다.   
만일 커서가 declaration만 되어 있고 definition 되어 있지 않으면 에러가 발생한다.  
해당 커서는 open 된 상태여야 한다.

INTO 절에 주어진 변수 타입은 fetch된 레코드 결과의 데이터 타입과 서로 호환 가능해야 한다.   
INTO 절에 주어진 변수들의 개수는 커서의 SELECT target 개수와 같아야 한다.   
단, INTO 절에 주어진 변수가 record type일 경우에는 한 개만 명시해야 한다.   
그리고 해당 record 변수의 field 개수는 SELECT target의 개수와 같아야 한다.

Fetch 할 레코드가 없는 상태에서 fetch가 호출되었을 경우, INTO 절의 target 변수 값은 변하지 않는다.

<a id="9075d7b77eae3d30"></a>
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

<a id="64c8c306cb173407"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="a13f822569178f28"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [OPEN Statement](#70cbb007421a6edc)
- [CLOSE Statement](#e7fbe6f6f64c9346)

<a id="287941cf9ced1e16"></a>
## FOR LOOP Statement

<a id="5a256a80b10aa602"></a>
### 기능

Index 변수가 주어진 값 범위를 가지는 동안 index 변수를 1씩 증가시키거나 감소시키면서 (REVERSE)   
내부의 statement들을 수행한다.

<a id="27517d56452701bb"></a>
### 구문

```
<for loop statement> ::=
    FOR index_variable_name IN [ REVERSE ] start_value .. last_value
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="acc5bf79fc4517c9"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="f77c81e09378b613"></a>
### 구문 규칙 및 파라미터

- Index variable name
    - FOR 구문에서 index로 사용할 변수의 이름이며 내부적으로 NATIVE_BIGINT 타입의 변수가 사용된다.
- Start value
    - Index 변수의 초기 값으로써 정수형이어야 한다. 만일 부동 소수점을 가진 숫자를 사용하면 타입을 변환하는 중에 소수점 이하는 버려진다.
- Last value
    - Index 변수의 최종 값으로써 정수형이어야 한다. 만일 부동 소수점을 가진 숫자를 사용하면 타입을 변환하는 중에 소수점 이하는 버려진다.

<a id="a1cdc5497a2f2534"></a>
### 설명

for loop 구문은 index 변수의 값을 start_value로부터 last_value까지 증가시키거나 감소시키면서   
내부의 statement list를 수행한다.

REVERSE를 명시한 경우에는 start_value로부터 1씩 감소하게 되며 index 변수의 값이 last_value보다 작아지게 되면 for loop statement의 실행을 종료한다.  
REVERSE를 명시하지 않으면 index 변수는 start_value 값부터 1씩 증가하고, index 변수의 값이 last_value보다 커지면 for loop statement의 실행을 종료한다.  
REVERSE를 명시하지 않은 상태에서 start_value가 last_value보다 크거나 REVERSE를 명시한 상태에서 start_value가 last_value보다 작으면 내부의 statement list는 수행되지 않는다.

<a id="afdecdf361b0af55"></a>
### 사용 예

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

<a id="e32387497e538591"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="e0a1560b8b0844d6"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CONTINUE Statement](#6dc86c314905ec09)
- [EXIT Statement](#c02a4714e78afa89)
- [GOTO Statement](#712fd8282104fa49)

<a id="f103942d316b303b"></a>
## Function Declaration and Definition

<a id="86030cf2b93dab91"></a>
### 기능

Nested function을 정의한다.

<a id="a5e1091dc35771a1"></a>
### 구문

```
<nested function statement> ::=
    FUNCTION func_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
        RETURN datatype
        { IS | AS } <item_declaration> BEGIN <pl_stmt_list> END
    ;
```

<a id="2aac1482f9bbf4ae"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 declaration 영역에서만 사용할 수 있다.

<a id="de24ea4ce3f9fd50"></a>
### 구문 규칙 및 파라미터

<a id="af800cf169483b9b"></a>
#### func_name

생성할 function의 이름으로써 스키마 내에서 고유한 이름이어야 한다.  
Function 이름의 길이는 128 바이트보다 작아야 한다.

<a id="ce223511d621807a"></a>
#### Param Name

Function이 사용할 인자의 이름을 정의한다.  
각 인자의 이름은 function 내에서 고유한 이름이어야 한다.

<a id="3e2104fb9949ea22"></a>
#### Bind Type

각 인자의 bind type을 설정한다.  
표기하지 않을 경우 기본 타입은 IN 이다.

<a id="96b8f0dd34e0044b"></a>
#### Item Declaration

Function 내부에서 사용될 로컬 변수등의 item을 선언한다.  
PL block에서 선언될 수 있는 모든 item들을 선언할 수 있다.

<a id="e86b61e5bf9c8bf5"></a>
#### PL Stmt List

Function의 body 부분으로써 수행할 PL statement들을 나열한다.

<a id="4a3ea3dabc1174d2"></a>
### 설명

Nested function은 해당 procedure 내에서만 호출할 수 있는 subprogram이다.  
그 외의 사용 방법은 schema-level function과 동일하다.

<a id="34a32ff2529471d0"></a>
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

<a id="594d8907609af9be"></a>
### 호환성

Schema-level function과 동일하다.

<a id="8bbd58fc6ce28f7f"></a>
### 참조

자세한 내용은 [CREATE FUNCTION](24-psm-sql-references.md#04b692603afa84f1)을 참조한다.

<a id="712fd8282104fa49"></a>
## GOTO Statement

<a id="fe1f8f7c6bbce0da"></a>
### 기능

현재 위치에서 접근할 수 있는 statement들 중에 주어진 label을 가진 가장 가까운 statement로 jump를 시도한다.

<a id="03c7fd784a5181c1"></a>
### 구문

```
<goto statement> ::=
    GOTO label_name
    ;
```

<a id="326bb4aa585cd51b"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="27dd3de9b5046fe4"></a>
### 구문 규칙 및 파라미터

- Label_name
    - Jump를 시도할 statement의 label 이름이다.
    - Identifier chain 형식을 가질 수 있다.

<a id="d1832252b4af57f6"></a>
### 설명

해당 label 이름을 가진 statement로 jump하여 수행을 시작한다.  
여러 개의 후보 statement들이 존재할 경우, 가장 가까운 statement로 jump한다.  
현재 위치에서 visible 한 (중첩된 scope 내에 존재하는) statement로만 jump할 수 있다.  
Forward jump와 backward jump 모두 가능하다.

<a id="61b032209a45d544"></a>
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

<a id="8b0eb5223b8f04b4"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="2019133ae02de75b"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [EXIT Statement](#c02a4714e78afa89)
- [CONTINUE Statement](#6dc86c314905ec09)

<a id="a840c60f2fa6fdae"></a>
## IF Statement

<a id="6137f8d50b67817c"></a>
### 기능

주어진 여러 조건들 중에 TRUE를 반환하는 조건에 해당하는 statement list를 수행한다.

<a id="6e2e50714739eba5"></a>
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

<a id="6f9f718ae89020da"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="83e6625eef60e5f2"></a>
### 구문 규칙 및 파라미터

- Search condition
    - boolean 타입으로 최종 평가될 수 있는 표현식이다.
- Executable statement list
    - GOLDILOCKS PSM에서 지원하는 모든 statement 들의 list 이다.

<a id="a24f6c2e5cf43def"></a>
### 설명

CASE 구문과 유사하게 조건들을 평가하여 TRUE를 반환하는 IF, ELSIF 절의 statement list를 수행한다.   
모든 조건들을 만족시키지 못하고 &lt;if statement else clause&gt;가 존재할 경우에는 해당 구문을 수행한다.   
ELSIF 구문들은 순서대로 먼저 나오는 조건식부터 평가하여 해당 조건식이 TRUE인 경우 그 이후의 조건식들은 평가하지 않는다

<a id="f814db412806dc39"></a>
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

<a id="cbab94143a614a32"></a>
### 호환성

&lt;if statement&gt; 구문은 SQL 표준과 구문이 같고 동일하게 동작한다.

**SQL 표준 호환성**

<a id="dab55d711726f22b"></a>
| Feature ID | 설명 | 지원여부 |
| --- | --- | --- |
| P002 | Computational completeness | O |

<a id="3d17fbbecb04f553"></a>
## Implicit Cursor Attribute

<a id="41821ad838622911"></a>
### 기능

PSM에서 정의된 implicit cursor의 상태값을 반환한다.

<a id="eb4f14e6a8714133"></a>
### 구문

```
<Implict cursor attribute> ::=
    SQL '%' { ISOPEN | FOUND | NOTFOUND | ROWCOUNT }
```

<a id="a3839fbf4384bda7"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="ddfad34631297bc1"></a>
### 설명

- 직전에 수행된 SQL 문의 결과를 저장한다.
    - ISOPEN: 현재 커서가 OPEN 상태인지 여부로써 항상 FALSE로 설정된다.
    - FOUND: 직전 SQL 결과에 의해 데이터가 반환 되었는지 여부이다.
    - NOTFOUND: FOUND의 반대이다.
    - ROWCOUNT: 직전 SQL결과에 의해 영향받은 record의 개수이다.

<a id="00420fe50072b406"></a>
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

<a id="3e636b60bab5cb7a"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="2763e9c2c2abb08d"></a>
## INSERT Statement Extension

<a id="378765f6c3ebe202"></a>
### 기능

PSM에서 지원하는 record-type 변수를 VALUES 절에 기술하여 데이터를 입력할 수 있도록 insert statement를 확장한 기능이다.

<a id="8582c4ac49ec6fed"></a>
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

<a id="3ea5afdaea825d23"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.  
EXECUTE IMMEDIATE의 원본 SQL 문에는 PSM insert extension 구문을 사용할 수 없다.

<a id="dfe5e8d3d045b1c5"></a>
### 구문 규칙 및 파라미터

Insert statement의 기본 구문과 동일하게 동작한다. 다만, value item에 기존의 value expression을 괄호에 묶어 연속으로 나열하는 방법 외에 PSM record type 변수를 기술하는 기능이 추가되었다.

Value_Item에 괄호 없이 변수를 사용할 경우 반드시 PSM record type의 변수를 기술해야 한다.   
Insert extension 구문 형태로 사용할 경우 record type이 아닌 변수를 섞어서 사용할 수 없다.

<a id="243e397b076a95f7"></a>
### 설명

일반적인 insert statement 외에 PSM의 record type 변수를 이용하여 record를 저장하거나 returning into를 통해 결과를 받아 온다.   
Insert에 대한 자세한 내용은 다음 예를 참조한다.

<a id="d79c3fb49d282e58"></a>
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

<a id="dc3b815e767faa84"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="b6a3e5f9f88fbaba"></a>
## NULL Statement

<a id="3d749590fbad427c"></a>
### 기능

아무 기능도 없는 statement 이다.

<a id="d99a6379cc8603e5"></a>
### 구문

```
<null statement> ::=
    NULL
    ;
```

<a id="c5338390b753f8f8"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="fa04ef259ffa104e"></a>
### 설명

아무 기능도 하지 않는 statement이며, 주로 특정 위치의 label을 설정하기 위해 사용된다.

<a id="9e4872fb2f169e1f"></a>
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

<a id="6918d896d254003e"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="70cbb007421a6edc"></a>
## OPEN Statement

<a id="aee9892313038ba0"></a>
### 기능

PSM에서 정의된 cursor의 SELECT 구문을 실행한다.

<a id="e90fca6d01c2569a"></a>
### 구문

```
<open statement> ::=
    OPEN cursor_name [ <actual param spec> ]
    ;

<actual param spec> ::=
      ( expression [ , expression ] .. )
```

<a id="9b89f7781845a449"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 body 영역에서만 사용할 수 있다.

<a id="41ef25c9760fe6c7"></a>
### 구문 규칙 및 파라미터

- Cursor_name
    - Open할 커서의 이름이다.

<a id="21dc4c9ee3ce56a4"></a>
### 설명

정의된 커서의 SELECT 또는 SELECT ... FOR UPDATE 구문을 실행한다.  
만일 커서가 declaration만 되어 있고 definition 되어 있지 않을 경우, 에러가 발생한다.   
Actual parameter의 값들은 해당 parameter의 데이터 타입과 서로 호환 가능해야 한다.

Actual parameter의 개수는 커서의 parameter 개수와 같아야 한다.  
만일 커서의 parameter의 개수보다 적을 경우, 나머지 모든 parameter들에 default 값이 명시되어야 한다.

<a id="5059e5814eaeef3c"></a>
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

<a id="2bfea24be36eafbe"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="eee6643130710512"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CLOSE Statement](#e7fbe6f6f64c9346)
- [FETCH Statement](#594c76c9a93d727b)

<a id="e42e171c8ed8be7c"></a>
## OPEN FOR Statement

<a id="196945a04a6f144c"></a>
### 기능

PSM에서 정의된 cursor 변수를 통해 SELECT 구문을 실행하여 한 개의 cursor를 open한다.

<a id="d6c6ee914aeb7fa0"></a>
### 구문

```
<open statement> ::=
    OPEN cursor_variable_name FOR <select_query>
    ;
```

<a id="5f8a5f22751edeae"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="ebd391a43c220881"></a>
### 구문 규칙 및 파라미터

- Cursor_Variable_name
    - cursor_variable의 이름이다.
- Select_query
    - Select query에는 static SQL과 dynamic SQL을 모두 사용할 수 있다.

<a id="809469c80d61497e"></a>
### 설명

정의된 cursor 변수의 SELECT 또는 SELECT ... FOR UPDATE 구문을 실행한다.  
만일 cursor 변수가 이전에 열어둔 커서가 존재하면 해당 커서가 자동으로 close 된다.

<a id="3d67037d55e74803"></a>
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

<a id="a88b744593712a10"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="b9c6934c71e69ebc"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Cursor Variable Declaration](#e6d4ef5813d5c256)
- [FETCH Statement](#594c76c9a93d727b)
- [CLOSE Statement](#e7fbe6f6f64c9346)

<a id="f6a3350c49a11c94"></a>
## Procedure Call

<a id="eab2dbcf2acbf801"></a>
### 기능

사용자 정의 procedure, built-in procedure 또는 nested procedure를 호출한다.

<a id="8334c3eb5ede0b36"></a>
### 구문

```
<Procedure call> ::=
    proc_name [ ( expr { , expr } ... ) ]
    ;
```

<a id="4b9f4d61cc28efc5"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

- 사용자 정의 procedure를 호출할 경우, 해당 procedure에 대한 다음 권한 중 하나가 있어야 한다.
    - EXECUTE PROCEDURE
    - Procedure가 속한 스키마에 대해 (EXECUTE PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
    - EXECUTE ANY PROCEDURE ON DATABASE

<a id="dc9287cc15bbb9a1"></a>
### 구문 규칙 및 파라미터

- Proc_name 
    - 실행할 procedure의 이름으로써 다음과 같은 형태로 사용할 수 있다.

<a id="740835127f7bb7b8"></a>
<table class="table column_count_3"><caption></caption><thead><tr><th class="to_center"><div>형태</div></th><th class="to_center"><div>구문</div></th><th class="to_center"><div>설명</div></th></tr></thead><tbody><tr><td class="to_left to_middle"><div>단일 identifier</div></td><td class="to_middle"><div>procedure_name</div></td><td><div>주어진 이름의 procedure를 호출한다.

검색 순서는 다음과 같다.
1. nested procedure
2. schema-level procedure</div></td></tr><tr><td class="to_left to_middle" rowspan="3"><div>identifier chain</div></td><td><div>label_name.procedure_name</div></td><td><div>nested procedure를 호출한다.</div></td></tr><tr><td><div>schema_name.procedure_name</div></td><td><div>schema-level procedure를 호출한다.</div></td></tr><tr><td><div>package_name.procedure_name</div></td><td><div>built-in procedure를 호출한다.</div></td></tr></tbody></table>

주어진 이름 (proc_name)으로 검색하여 최초로 발견된 procedure에 주어진 인자와 개수 및 타입이 적절하지 않으면 다른 procedure를 찾지 않고 에러를 발생시킨다.

<a id="735f3a1b78e361c1"></a>
### 설명

이전에 정의된 사용자 정의 procedure, built-in procedure 또는 nested procedure를 호출한다.   
호출할 때 default 값이 정의된 인자값은 생략할 수 있다.

OUT 이나 IN-OUT으로 지정된 인자에 procedure 변수나 bind parameter (?, :V1 등)를 사용하면 반환된 값을 얻을 수 있다.

<a id="ccdf501ea003a8be"></a>
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

<a id="8508a1836376d586"></a>
### 호환성

SQL 표준에는 &lt;call statement&gt;를 사용하도록 되어 있다.

<a id="7a92bd254850f3a4"></a>
## Procedure Declaration and Definition

<a id="ea4015a1c1882c49"></a>
### 기능

Nested procedure를 정의한다.

<a id="7a540b30b4bdcc0e"></a>
### 구문

```
<nested procedure statement> ::=
        PROCEDURE proc_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
        { IS | AS } <item_declaration> BEGIN <pl_stmt_list> END
    ;
```

<a id="ff82526cd90ef555"></a>
### 사용 범위 및 접근 권한

PSM declaration section에서 사용할 수 있다.

<a id="d2ed3ebeee1f8765"></a>
### 구문 규칙 및 파라미터

- Proc_name
    - 생성할 procedure의 이름이며, 스키마 내에서 고유한 이름이어야 한다.
    - Procedure 이름의 길이는 128 바이트보다 작아야 한다.
- Param_name
    - Procedure가 사용할 인자의 이름을 정의한다.
    - 각 인자의 이름은 procedure 내에서 고유한 이름이어야 한다.
- Bind_type
    - 각 인자의 bind type을 설정한다. 
    - 표기하지 않을 경우 기본 타입은 'IN'이다.
- Item_declaration
    - Procedure 내부에서 사용될 로컬 변수등의 item을 선언한다.
    - PL block에서 선언될 수 있는 모든 item들을 선언할 수 있다.
- PL Stmt List
    - Procedure의 body 부분으로써 수행할 PL statement들을 나열한다.

<a id="77c8cd37bf51785c"></a>
### 설명

Nested procedure는 해당 procedure 내에서만 호출할 수 있는 subprogram이다.  
그 외의 사용 방법은 schema-level procedure와 동일하다.

<a id="d1d196bcc699a8cf"></a>
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

<a id="2ff491a1c7575de9"></a>
### 호환성

Schema-level procedure와 동일하다.

<a id="0f92f37a4fe25e74"></a>
### 참조

자세한 내용은 [CREATE PROCEDURE](24-psm-sql-references.md#58204d591b990498)를 참조한다.

<a id="c532045529f3bc5f"></a>
## RAISE Statement

<a id="5c03aea7a4ab1ab0"></a>
### 기능

사용자가 정의한 exception을 명시적으로 발생시킨다.

<a id="8e60eb94f468c75e"></a>
### 구문

```
<RAISE Statement> ::= 
    RAISE  <Exception-Name>
    ;
```

<a id="347acc26064f8174"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 body 영역에서만 사용할 수 있다.

<a id="fb8146e3281e92df"></a>
### 구문 규칙 및 파라미터

- Raise 시킬 exception name이 raise가 속한 PL block이나 상위 PL block의 DECLARE 절에 선언되어야 한다. 단, predefined exception은 선언없이 raise할 수 있다. 
- Raise 문이 exception handler 내에서 사용되면 exception name을 생략할 수 있는데 이 경우, 직전 exception이 상위 블럭으로 전파된다.

<a id="7bc98958412abf1f"></a>
### 설명

Exception이 발생한 PL block에서 처리되지 못하면 상위 PL block으로 전파된다.  
Raise 시킬 exception이 RAISE 구문을 포함하는 PL block 및 상위 PL block 내의 모든 exception handler에 존재하지 않을 경우 에러가 발생한다.  
처리될 때까지 RAISE exception이 발생한 PL block부터 상위로 전파되며 하위 PL block의 exception handler로는 전파되지 못한다.

**User exception 전파**

<a id="c5763d4b85cc5def"></a>
| Raise exception | Exception handler  SCOPE | Exception  handler | 상위 전파여부 |
| --- | --- | --- | --- |
| User exception without error code | 동일 scope | X | "unhandled exception" 오류를 상위 scope으로 전파한다. |
| User exception with error code | 상위 scope | X | User exception을 전파한다. |
| User exception with error code | 동일 scope | X | User defined error code를 전파한다. |
| User exception with error code | 상위 scope | X | User defined error code를 전파한다. |

<a id="5822ffb19177f060"></a>
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

<a id="8b518f6aa200bc26"></a>
### 호환성

SQL 표준에는 &lt;handler declaration&gt;과 &lt;condition declaration&gt;은 기술되어 있지만 구문은 지원하지 않는다.

<a id="a7a6c0349d2b3d31"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [Exception Handler](#9f9d440cbf4130a1)
- [Exception Declaration](#480c66a8f8725127)

<a id="4bc9c352a656a41c"></a>
## Record Variable Declaration

<a id="ac98b3ea779a044c"></a>
### 기능

DECLARE 영역에서 record type 변수를 선언한다.

<a id="38a1c50defb28483"></a>
### 구문

```
<declare record variable> ::=
    variable_name <recordType> 
    ;

<recordType> ::=
     <tableName>%ROWTYPE
   | USER_DEFINED_DATA_TYPE
```

<a id="5083c481fffa0aa0"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 declaration 영역에서만 사용할 수 있다.

<a id="e0e51a0ac3a99ca3"></a>
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
    - recordType 선언에 대한 자세한 내용은 [User-defined Record Type](18-psm-datatypes.md#b5920fbcd6dc58b1)을 참조한다.

<a id="453c685a79a5c381"></a>
### 설명

- 선언된 변수는 다음과 같은 특징이 있다.
    - 하나의 scope (PL block body) 내에서 고유한 이름이어야 한다.
    - 중첩된 하위의 PL block body에 동일한 이름의 변수를 선언할 수 있다.
    - 중복 선언된 변수를 명확히 사용하기 위해서는 scope_name.variable_name의 형태로 사용해야 한다.
    - Scope 이름을 명시하지 않고 중복 선언된 변수를 사용할 경우에는 자동으로 가장 가까운 scope의 변수가 사용된다.
- 선언된 변수는 해당 scope와 하위 scope에서 사용되며, embedded SQL에서와 달리 ':' 기호를 붙이지 않는다.
- 사용된 변수는 해당 SQL이나 PSM control statement에 대해 bind parameter (INOUT)로 작동한다.

<a id="4783ae652b5828af"></a>
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

<a id="f451e1432d4aa42c"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="ad03e084b622338e"></a>
## RETURN Statement

<a id="10eae140f23d9504"></a>
### 기능

Function이 반환할 값을 지정한 후 해당 function을 종료한다. Procedure는 반환값을 지정하지 않고 해당 procedure를 종료한다.

<a id="fa8865d335f8844f"></a>
### 구문

```
<return statement> ::=
    RETURN [ return_value_expr ]
    ;
```

<a id="8a802d2fee4e58ea"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 body 영역에서만 사용할 수 있다.

<a id="6d54359165390b08"></a>
### 구문 규칙 및 파라미터

- Return_value_expr
    - 반환할 값의 표현식으로써 function일 경우에만 명시할 수 있다.

<a id="43a206192a4d0207"></a>
### 설명

현재 수행되고 있는 procedure/ function을 종료한다.  
Function의 경우, RETURN 구문이 수행되지 않고 종료되거나, RETURN 구문이 return_value_expr를 가지지 않으면 오류가 발생한다.

<a id="d34973d8b5edd418"></a>
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

<a id="c2fb951e88336bf3"></a>
### 호환성

SQL 표준에는 기술되어 있지만 conformance rule은 존재하지 않는다.

<a id="ddf797e6b9bec724"></a>
## RETURNING INTO clause

<a id="51c37f8c270de83b"></a>
### 기능

Insert/ update/ delete에서 처리된 데이터가 PSM 변수로 반환된다.

<a id="2d25614c5b0d33b9"></a>
### 구문

```
<Insert, Delete Returning_into_clause> ::=
      [ RETURN | RETURNING ] { * | { <value_expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]

<Update returning into clause> ::=
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] } INTO Variable [, ...]
```

<a id="0265e3cd7a2d4b79"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 body 영역에서만 사용할 수 있다.

<a id="c731ae3dd00b504b"></a>
### 구문 규칙 및 파라미터

레코드 타입 변수는 다른 타입과 섞어서 사용할 수 없다.

<a id="1f6a0a6138c0d93f"></a>
### 설명

Insert/ update/ delete 문을 처리한 before/ after record를 returning into를 통해 저장한다.

<a id="43738676c821f8ee"></a>
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

<a id="bc937b3379f6a43a"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="de8faeb73cd44eaa"></a>
## %ROWTYPE Attribute

<a id="b250b2b489a652a7"></a>
### 기능

변수를 선언할 때 특정 테이블 또는 커서나 커서 변수의 result set과 같은 구조와 타입으로 정의한다.

<a id="a62766d5dcb3a6ea"></a>
### 구문

```
<rowtype attribute> ::=
    <identifier chain> % ROWTYPE
```

<a id="0223ca53328909fa"></a>
### 사용 범위 및 접근 권한

- PSM 내에서만 사용할 수 있다. (예: package, procedure, function)
- PL block의 declaration 영역에서만 사용할 수 있다.
- 변수를 선언할 때는 &lt;data type&gt; 부분에만 사용할 수 있다
- 레코드 타입의 필드를 선언할 때는 &lt;data type&gt; 부분에 사용할 수 없다. (complex data type은 지원하지 않는다.)

<a id="03c66a4330e5f412"></a>
### 구문 규칙 및 파라미터

- Identifier chain은 다음과 같다.
    - 참조할 테이블, view, synonym의 이름이나 커서 또는 커서 변수의 이름

<a id="f51829ec8eca20a8"></a>
### 설명

- 참조 대상 검색 순서
    - 커서 혹은 커서 변수 
    - Base table, view, 또는 synonym

- 참조 범위
    - Row attribute를 이용하여 참조할 경우 테이블 또는 커서의 result set에서 column 이름과 타입만 참조한다.
    - 따라서 NOT NULL constraint나 DEFAULT 값 설정 등은 참조하지 않는다.

<a id="5460bff6530e01e9"></a>
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

<a id="880575e0918f3100"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="fd818983e72539e7"></a>
## Scalar Variable Declaration

<a id="9adb44cb7ecdf578"></a>
### 기능

DECLARE 영역에서 scalar 변수를 선언한다.

<a id="13bae022de00ae80"></a>
### 구문

```
<declare scalar variable> ::=
    variable_name <data type> [ <variable initialize clause> ]
    ;

<variable initialize clause> ::=
      [ NOT NULL ] { DEFAULT | := } <value expression>
```

<a id="94b5854c3c582063"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 declaration 영역에서만 사용할 수 있다.

<a id="f88fa9ee220c5831"></a>
### 구문 규칙 및 파라미터

- Variable_name
    - 선언할 변수의 이름이다.
    - 변수 이름의 길이는 128 바이트보다 작아야 한다.
    - 하나의 scope (PL block body) 내에서 고유한 이름이어야 한다.
    - 중첩된 하위의 PL block body에 동일한 이름의 변수를 선언할 수 있다.
    - 중복 선언된 변수를 명확히 사용하기 위해서는 scope_name.variable_name의 형태로 사용해야 한다.
    - Scope 이름을 명시하지 않고 중복 선언된 변수를 사용할 경우에는 자동으로 가장 가까운 scope의 변수가 사용된다.
- Data_Type
    - GOLDILOCKS에서 제공하는 모든 built-in [Data Type](../part-03-sql-manual/11-sql-elements.md#ff81d005bda1af76)들을 사용할 수 있다.
- Value_expression
    - 변수에 지정할 초기값을 표현한다.
    - GOLDILOCKS가 지원하는 모든 상수 및 multi-row 함수들을 제외한 모든 표현식을 사용할 수 있다.

<a id="ba34476627471e91"></a>
### 설명

- 선언된 변수는 다음과 같은 특징이 있다.
    - 하나의 scope (PL block body) 내에서 고유한 이름이어야 한다.
    - 중첩된 하위의 PL block body에 동일한 이름의 변수를 선언할 수 있다.
    - 중복 선언된 변수를 명확히 사용하기 위해서는 scope_name.variable_name의 형태로 사용해야 한다.
    - Scope 이름을 명시하지 않고 중복 선언된 변수를 사용할 경우에는 자동으로 가장 가까운 scope의 변수가 사용된다.
- 선언된 변수는 해당 scope와 하위 scope에서 사용되며, embedded SQL에서와 달리 ':' 기호를 붙이지 않는다.
- 사용된 변수는 해당 SQL이나 PSM control statement에 대해 bind parameter (INOUT)로 작동한다.

<a id="2cd039ecc9180bf1"></a>
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

<a id="d2898847791009af"></a>
### 호환성

- &lt;declare scalar variable&gt; 구문은 SQL 표준과 비교하여 다음과 같은 차이가 있다.
    - SQL 표준의 &lt;SQL variable declaration&gt;은 PL block body 내 (BEGIN 이후)에서 변수를 선언하지만, GOLDILOCKS는 별도의 declaration section에서 선언한다.
    - SQL 표준에서는 한 번의 DECLARE 구문으로 여러 개의 동일한 타입 변수를 선언할 수 있지만, GOLDILOCKS에서는 한 statement로 한 개의 변수만 선언할 수 있다.
    - SQL 표준에서는 초기 값을 세팅할 때 DEFAULT 구문만 사용하지만, GOLDILOCKS는 assign 기호인 :=도 사용할 수 있다.

<a id="472b2e69b3b45f5e"></a>
## SELECT INTO Statement

<a id="30933ace93f6e603"></a>
### 기능

SELECT를 통해 한 개의 row를 반환 받는다.

<a id="c9f59c1b528aa358"></a>
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

<a id="758cf4ac27e1a97c"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 body 영역에서만 사용할 수 있다.

<a id="3a0e4d8d824d89a3"></a>
### 구문 규칙 및 파라미터

INTO 절을 제외한 사항은 select statement와 동일한 규칙을 따른다.

<a id="adb9ca106c658f23"></a>
### 설명

- SELECT INTO는 한 개의 record를 반환받는 용도로 사용한다. 
    - 결과가 0 건인 경우, "NO_DATA_FOUND" exception이 발생한다. 
    - 결과가 두 건 이상인 경우, "TOO_MANY_ROWS" exception이 발생한다. 
- PSM의 record type 변수를 통해 결과를 반환받을 수 있다. 
    - Record type변수를 사용할 경우 다른 타입의 변수와 섞어서 사용할 수 없다.

<a id="f53acdb8e71fc6fb"></a>
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

<a id="e4b261c85724e073"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="5dae88c607af81c9"></a>
## SQLCODE Function

<a id="63c6e19725880d32"></a>
### 기능

PSM에서 수행된 직전 statement의 error code를 반환한다.

<a id="d4c48d490e566328"></a>
### 구문

```
<SQLCODE function> ::= SQLCODE
```

<a id="a04db40a5293f460"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다.

<a id="9852d836d1812af1"></a>
### 구문 규칙 및 파라미터

별도의 argument를 갖지 않는다.

<a id="eb0f0a7aee6b443c"></a>
### 설명

PL/ SQL에서 수행된 statement의 error code를 반환한다.  
Error code를 할당하지 않은 user-defined exception의 경우, handler에 의해 처리되는 시점에 1로 반환된다.  
Exception handler에 의해 오류 처리가 완료되면 0으로 반환된다.

<a id="a910f0771e21c986"></a>
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

<a id="65a901d3d4a5dd2a"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="3b7cf148a615e7e0"></a>
## SQLERRM Function

<a id="34af92cbcc7e15f8"></a>
### 기능

PSM에서 수행된 직전 statement의 error message를 반환한다.

<a id="0821b4295b886763"></a>
### 구문

```
<SQLERRM function> ::= SQLERRM
```

<a id="09e679e933c62d8c"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다.

<a id="bae6e5afd1032a4c"></a>
### 구문 규칙 및 파라미터

별도의 argument를 갖지 않는다.

<a id="d06a1704996b7e9c"></a>
### 설명

PL/ SQL에서 수행된 statement의 error message를 반환한다.  
Error code를 할당하지 않은 user-defined exception의 경우, handler에 의해 처리되는 시점에 user-defined exception으로 반환된다.  
Exception handler에 의해 오류 처리가 완료되면 *successful completion* 메세지를 출력한다.

<a id="3c6915a8142fa83f"></a>
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

<a id="45f0d08fb0c30640"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="5b4b2c1851af2523"></a>
## %TYPE Attribute

<a id="57fd79be68c7812d"></a>
### 기능

변수를 선언할 때나 RECORD 타입의 특정 필드를 정의할 때 그 타입을 특정 테이블의 column 또는 다른 변수와 동일한 타입으로 정의한다.

<a id="ce8accebfd450f67"></a>
### 구문

```
<type attribute> ::=
    <identifier chain> % TYPE
```

<a id="f8033662d11a6109"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)  
PL block의 declaration 영역에서만 사용할 수 있다.  
변수를 선언할 때나 레코드 타입의 필드를 선언할 때 &lt;data type&gt; 부분에만 사용할 수 있다.

<a id="68fab28e5bbb058a"></a>
### 구문 규칙 및 파라미터

- Identifier_chain
    - 참조할 테이블의 column 또는 기존에 선언된 변수 (혹은 변수의 필드)의 이름이다.

<a id="6dac5082c9feb738"></a>
### 설명

<a id="29aa73e7063eb46b"></a>
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
  1. 변수 (또는 필드) 이름  
  2. Column 이름

<a id="abe66628621fa9e4"></a>
#### NOT NULL Constraints 변수 참조

NOT NULL 속성의 변수를 참조할 때는 초기값을 참조하지 않으므로 반드시 새로운 초기값을 지정해야 한다.   
현재 record type 변수의 필드에 대한 type attribute를 사용할 때 필드 초기값 설정을 지원하지 않으므로 NOT NULL 타입의 필드는 참조할 수 없다.

<a id="9e76b216a18dd79e"></a>
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

<a id="e4d41c3a569eeda3"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="93a9268f91985e3d"></a>
## UPDATE Statement Extension

<a id="90cb4ca738f40eeb"></a>
### 기능

PSM에서 UPDATE 문의 갱신 대상 column을 나열하는 방식 외에 추가적으로 record type 변수를 이용하여 레코드를 갱신한다.   
PSM에서 UPDATE (searched) RETURNING INTO 절에 record type 변수를 사용하여 결과를 저장한다.

<a id="cef2baf1a80e1d57"></a>
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

<a id="a46865b5e29ec097"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="1794b5f70c7cb225"></a>
### 구문 규칙 및 파라미터

- UPDATE SET ROW 구문에서 사용할 &lt;PSM_Variable&gt;은 반드시 record type으로 선언된 변수이어야만 한다.
- UPDATE RETURNING INTO 구문에서 사용할 &lt;Variable&gt;은 record type이 아니어도 된다.
    - 단, record type으로 기술한 경우 다른 데이터 타입의 변수와 섞어서 사용하거나 두 개 이상의 record type 변수를 나열할 수 없다.

<a id="533c8d5653332947"></a>
### 설명

PSM에서 record type 변수를 통해 레코드를 갱신하거나 RETURNING INTO의 결과를 저장한다.

<a id="f1f45797aeca81e1"></a>
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

<a id="d2b694bf4c8f33ef"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="46a44ab4f95a5507"></a>
## WHILE LOOP Statement

<a id="f5f05d7fb9967b98"></a>
### 기능

&lt;search condition&gt;이 TRUE 값을 반환하는 동안 내부의 statement들을 수행한다.

<a id="b76b9563713e61ed"></a>
### 구문

```
<while loop statement> ::=
    WHILE <search condition>
    LOOP { <SQL procedure statement> ; }... END LOOP [ loop_name ]
    ;
```

<a id="a109fe10d47506b5"></a>
### 사용 범위 및 접근 권한

PSM 내에서만 사용할 수 있다. (예: package, procedure, function)   
PL block의 body 영역에서만 사용할 수 있다.

<a id="86014ae3e773db6d"></a>
### 구문 규칙 및 파라미터

- Search condition은 다음과 같다.
    - while 루프를 계속 순환하는 조건 표현식이다.
    - 최종적으로 boolean 타입을 반환해야 한다.

<a id="f125231dfc943d81"></a>
### 설명

while loop 구문은 &lt;search condition&gt;의 평가 결과가 TRUE인 동안 내부의 statement list를 수행한다.

<a id="41745ebca5f7bdf0"></a>
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

<a id="8e7d374116f99ce4"></a>
### 호환성

&lt;while loop statement&gt; 구문은 SQL 표준에 &lt;while statement&gt;로 정의되어 있다.  
SQL 표준의 &lt;while statement&gt;는 loop 구문을 DO ... END WHILE로 수행하는 반면에 GOLDILOCKS는 LOOP ... END LOOP로 수행한다.

<a id="0448150d6809f532"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CONTINUE Statement](#6dc86c314905ec09)
- [EXIT Statement](#c02a4714e78afa89)
- [GOTO Statement](#712fd8282104fa49)

---

[← 22. Using SQLs in PSM](22-using-sqls-in-psm.md) · [전체 목차](../README.md) · [24. PSM SQL References →](24-psm-sql-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
