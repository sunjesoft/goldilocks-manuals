<a id="2b8d81e59155cb4c"></a>

# 24. PSM SQL References

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/2b8d81e59155cb4c)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 23. PSM Language Element References](23-psm-language-element-references.md) · [전체 목차](../README.md) · [25. ODBC →](../part-05-developer-manual/25-odbc.md)

<a id="f58959c250c9a4ad"></a>
## ALTER FUNCTION

<a id="9f4221d0975c7973"></a>
### 기능

Function을 다시 compile 한다.

<a id="6b31fc070112d234"></a>
### 구문

```
<alter function statement> ::=
    ALTER FUNCTION function_name COMPILE
    ;
```

<a id="b54e5579a873e731"></a>
### 사용 범위 및 접근 권한

&lt;alter function statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 function의 소유자
- Function이 속한 스키마에 대해 (ALTER PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY PROCEDURE ON DATABASE

<a id="ee3403f4b19aad66"></a>
### 구문 규칙 및 파라미터

- Function name
    - Compile 할 function의 이름이다.
    - schema_name.func_name과 같이 function이 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="0e60a608a1520604"></a>
### 설명

지정된 schema-level function을 다시 compile 한다.

<a id="2d0ede78d7079cc9"></a>
### 사용 예

```
gSQL> ALTER FUNCTION FUNC1 COMPILE;

Function altered.
```

<a id="90249b3550a4b8b0"></a>
### 호환성

SQL 표준에서는 CREATE를 수행할 때 지정된 characteristic들을 변경하는 구문이고, GOLDILOCKS에서는 function의 plan을 다시 생성하는 구문이다.

**SQL 표준 호환성**

<a id="bfbc445d58dde55a"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="c9b85ddf1a4cf897"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE FUNCTION](#04b692603afa84f1)
- [DROP FUNCTION](#2e3b5a779150ed13)

<a id="3cf929d08a31e4c0"></a>
## ALTER PROCEDURE

<a id="9691d1e62a7b20c0"></a>
### 기능

Procedure를 다시 compile 한다.

<a id="bc722e5cbaca7e39"></a>
### 구문

```
<alter procedure statement> ::=
    ALTER PROCEDURE proc_name COMPILE
    ;
```

<a id="bbfca584226b7507"></a>
### 사용 범위 및 접근 권한

&lt;alter procedure statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 procedure의 소유자 
- Procedure가 속한 스키마에 대해 (ALTER PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY PROCEDURE ON DATABASE

<a id="f3616549980913d9"></a>
### 구문 규칙 및 파라미터

- Proc name
    - Compile할 procedure의 이름이다. 
    - schema_name.proc_name과 같이 procedure가 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="4e37d6a9f41abde4"></a>
### 설명

지정된 schema-level procedure를 다시 compile 한다.

<a id="97b166d539e68d0f"></a>
### 사용 예

```
gSQL> CREATE OR REPLACE PROCEDURE PROC1( A1 INTEGER )
IS
BEGIN
  INSERT INTO T1 VALUES( A1 );
END;
/

ERR-01000(16409): Warning: Routine definition has compilation errors
ERR-HY000(17032): PSM compilation error : 
(1) at (5:15): ERR-17053: schema or table object does not exist
Procedure created.

gSQL> CALL PROC1(1);

ERR-HY000(17032): PSM compilation error : 
(1) at (5:15): ERR-17053: schema or table object does not exist

gSQL> CREATE TABLE T1( I1 INTEGER );

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> ALTER PROCEDURE PROC1 COMPILE;

Procedure altered.

gSQL> COMMIT;

Commit complete.

gSQL> CALL PROC1(2);

Procedure Call complete.

gSQL> SELECT * FROM T1;

I1
--
 2

1 row selected.
```

<a id="3c843d2213729b0d"></a>
### 호환성

SQL 표준에서는 CREATE를 수행할 때 지정된 characteristic들을 변경하는 구문이고, GOLDILOCKS에서는 procedure의 plan을 다시 생성하는 구문이다.

**SQL 표준 호환성**

<a id="863253dc1a6b7242"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="8461bb78751dd793"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PROCEDURE](#58204d591b990498)
- [DROP PROCEDURE](#3808c8dd15ec4e09)

<a id="8813dc15c2cee530"></a>
## CALL Statement

<a id="c6d477de8c8a8bc5"></a>
### 기능

Schema-level procedure나 function을 수행한다.

<a id="0987cbf19e582717"></a>
### 구문

```
<call statement> ::= 
    <sql call statement> | <odbc procedure call escape sequence>
    ;

<sql call statement> ::=
    CALL proc_name [ ( value_expr [ , value_expr ] .. ) ]  [ INTO { '?' | { host_param [ indicator_param ] } } ]

<odbc procedure call escape sequence> ::=
    '{' [ ? = ] CALL proc_name [ ( value_expr [ , value_expr ] .. ) ] '}'
```

<a id="0627b71ef6ae4b1b"></a>
### 사용 범위 및 접근 권한

&lt;call statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다

- 해당 procedure에 대한 EXECUTE 권한
- Procedure가 속한 schema에 대해 (EXECUTE PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- EXECUTE ANY PROCEDURE ON DATABASE

<a id="1f98a43807055057"></a>
### 구문 규칙 및 파라미터

- proc_name
    - 실행할 procedure/ function의 이름이다 
    - Schema_name.Proc_name과 같이 procedure가 속한 schema를 포함할 수 있다. 
- value_expr
    - Procedure에 전달한 인자값을 표현한다. '?'나 ':V1'과 같은 bind parameter를 사용할 수도 있다.

<a id="d7c316f99cc1a2b8"></a>
### 설명

명시된 인자들을 사용하여 schema-level SQL procedure나 function을 실행한다.

&lt;sql call statement&gt; 형식 중에 function은 INTO 절 다음에 host variable 표현이나 dynamic bind parameter (?)를 사용하여 결과값을 반환한다.

&lt;odbc procedure call escape sequence&gt; 형식은 ODBC/ JDBC 등에서 PROCEDURE를 호출하기 위한   
표준 구문이며, GOLDILOCKS는 이 구문을 server에서 지원한다. (gsql 등의 tool에서도 사용 가능하다.)  
Function은 앞에 assign 표현( ? = )을 사용하여 결과값을 반환한다.

<a id="0091555743c26884"></a>
### 사용 예

<a id="4e9b42ce440535ea"></a>
#### Call Procedure

```
gSQL> CREATE OR REPLACE PROCEDURE PROC1
(
  A1 INTEGER
)
IS
BEGIN
  DBMS_OUTPUT.PUT_LINE('A1=' || A1);
END;
/

Procedure created.

gSQL> \var v1 INTEGER;
gSQL> \exec :v1 := 123;
gSQL> CALL PROC1(:v1);
A1=123

Procedure Call complete.
```

<a id="8e391c8a1df22e20"></a>
#### Call Function

```
CREATE OR REPLACE FUNCTION FUNC1
(
  A1 INTEGER
)
RETURN INTEGER
IS
BEGIN
    return A1;
END;
/

Function created.


gSQL> \var v1 INTEGER;
gSQL> \var v2 INTEGER;
gSQL> \exec :v1 := 123;
gSQL> CALL FUNC1(:v1) INTO :v2;
Procedure Call complete.

gSQL> \print v2;
 V2
---
123
```

<a id="0fa5cb0afe5c5556"></a>
### 호환성

SQL 표준에서는 PROCEDURE에 대한 호출만 가능하여 [INTO] 절 이하를 정의하지 않고 있다.

<a id="04b692603afa84f1"></a>
## CREATE FUNCTION

<a id="d769ec788fff087c"></a>
### 기능

Schema-level function을 정의한다.

<a id="c4b11c5b49c618cc"></a>
### 구문

```
<create procedure statement> ::=
    CREATE [ OR REPLACE ]  
        FUNCTION func_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
        RETURN datatype
        [ <func_characteristics> ]
        { IS | AS } <item_declaration> BEGIN <pl_stmt_list> END
    ;

<func_characteristics> ::=
    DETERMINISTIC | AUTHID CURRENT_USER | AUTHID DEFINER
```

<a id="d8d09a1a76ed1879"></a>
### 사용 범위 및 접근 권한

&lt;create function statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- Function을 생성하기 위해 다음 권한 중 하나가 있어야 한다.
    - Function이 속한 스키마에 대해 (CREATE PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
    - CREATE ANY PROCEDURE ON DATABASE 
- OR REPLACE 절을 사용할 때 이미 function이 존재할 경우, 기존 function을 제거할 수 있는 다음 권한 중 하나가 있어야 한다.
    - 해당 function의 소유자
    - Function이 속한 스키마에 대해 (DROP PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
    - DROP ANY PROCEDURE ON DATABASE
- 구문을 수행한 사용자는 생성한 function의 소유자이다.

<a id="b50ce1fc07c04681"></a>
### 구문 규칙 및 파라미터

<a id="4437456e1482a1c7"></a>
#### OR REPLACE

이미 function이 존재할 경우, 기존의 function을 대체한다.

<a id="5c652414a6419adb"></a>
#### FUNCTION NAME

생성할 function의 이름으로써 스키마 내에서 고유한 이름이어야 한다.  
schema_name.func_name과 같이 function이 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
Function 이름의 길이는 128 바이트보다 작아야 한다.

<a id="ff94742a90979d1e"></a>
#### PARAM NAME

Function이 사용할 인자의 이름을 정의한다.   
각 인자의 이름은 function 내에서 고유한 이름이어야 한다.  
각 인자 이름의 길이는 128 바이트보다 작아야 한다.  
하나의 function에 사용할 수 있는 인자의 최대 개수에는 제한이 없다.

<a id="d981e9ebdca240fb"></a>
#### Bind Type

각 인자의 bind type을 설정한다.   
표기하지 않을 경우 기본 타입은 IN 이다.

<a id="fa674f76497ba81c"></a>
#### Func_Characteristics

Function 수행 옵션을 정의한다. 같은 항목에 대해서는 한 번만 기술해야 한다.

- DETERMINISTIC: 동일한 인자값들이 입력될 경우 해당 function은 항상 동일한 결과값을 반환한다.
- AUTHID CURRENT_USER: Function을 실행하는 중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되고 수행된다.
- AUTHID DEFINER: Function을 실행하는 중에 수행되는 SQL들은 definer의 authorization에 따라 해석되고 수행된다.

<a id="8563c3c730b271ba"></a>
#### Item Declaration

Function 내부에서 사용될 로컬 변수등의 item을 선언한다.  
PL block에서 선언될 수 있는 모든 item들을 선언할 수 있다.

<a id="9320e9a9446e726e"></a>
#### PL Stmt List

Function의 body 부분으로써 수행할 PL statement들을 나열한다.  
Function의 내부에서는 '?'나 ':V1'과 같은 bind parameter를 사용할 수 없다.

<a id="1dabecd981e7883b"></a>
### 설명

Schema-level SQL function을 정의한다. 생성된 function은 모든 expression에서 호출될 수 있다.

Function의 정의는 INFORMATION_SCHEMA의 ROUTINES 테이블에서 확인할 수 있다. Function의 parameter들에 대한 정의는 INFORMATION_SCHEMA의 PARAMETERS 테이블에서 확인할 수 있다.

관련 객체들이 존재하지 않아 function이 일시적으로 불완전해졌을 경우, &lt;alter function&gt; 구문으로 plan을 다시 생성하려 시도해볼 수 있다.

생성된 function은 &lt;drop function&gt; 구문을 사용하여 제거할 수 있다.  
Function의 최대 생성 개수에는 제한이 없으므로 저장 공간에 문제가 없는 한 계속 생성할 수 있다.

<a id="16fc0821375e70dd"></a>
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

<a id="1ea6f6f7a7a84ba9"></a>
### 호환성

SQL 표준에서는 OR REPLACE 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="947c65007fdb6ca0"></a>
| Feature ID | 설명 | 지원여부 |
| --- | --- | --- |
| T471 | Result sets return value | X |
| T341 | Overloading of SQL-invoked functions and SQL-invoked procedures | X |
| S023 | Basic structured types | X |
| S241 | Transform functions | X |
| S024 | Enhanced structured types | X |
| T571 | Array-returning external SQL-invoked functions | X |
| T572 | Multiset-returning external SQL-invoked functions | X |
| S201 | SQL routines on arrays | X |
| S202 | SQL-invoked routines on multisets | X |
| T323 | Explicit security for external routines | X |
| S231 | Structured type locators | X |
| S232 | Array locators | X |
| S233 | Multiset locators | X |
| T041 | Basic LOB data type support | X |
| S027 | Create method by specific method name | X |
| T041 | Basic LOB data type support | X |
| T324 | Explicit security for SQL routines | O |
| T326 | Table functions | X |
| T651 | SQL-schema statements in SQL routines | X |
| T652 | SQL-dynamic statements in SQL routines | O |
| T653 | SQL-schema statements in external routines | X |
| T654 | SQL-dynamic statements in external routines | X |
| T655 | Cyclically dependent routines | X |
| T272 | Enhanced savepoint management | X |
| T522 | Default values for IN parameters of SQL-invoked procedures | O |
| B121 | Routine language Ada | X |
| B122 | Routine language C | X |
| B123 | Routine language COBOL | X |
| B124 | Routine language Fortran | X |
| B125 | Routine language MUMPS | X |
| B126 | Routine language Pascal | X |
| B127 | Routine language PL/I | X |
| B128 | Routine language SQL | O |
| B129 | Routine language Ada: VARCHAR and NUMERIC support | X |

<a id="f83520e2c4f00792"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [DROP FUNCTION](#2e3b5a779150ed13)
- [ALTER FUNCTION](#f58959c250c9a4ad)

<a id="58204d591b990498"></a>
## CREATE PROCEDURE

<a id="0489fb0c4dd430af"></a>
### 기능

Schema-level procedure를 정의한다.

<a id="fd9083f2b9f5709a"></a>
### 구문

```
<create procedure statement> ::=
    CREATE [ OR REPLACE ]  
        PROCEDURE proc_name [ ( { param_name [IN|OUT|INOUT] datatype [ { := | DEFAULT } init_expr ] } [, ...] ) ]
        [ <proc_characteristics> ]
        { IS | AS } <item_declaration> BEGIN <pl_stmt_list> END
    ;

<proc_characteristics> ::=
    AUTHID CURRENT_USER | AUTHID DEFINER
```

<a id="9b1a6b9d429126f5"></a>
### 사용 범위 및 접근 권한

&lt;create procedure statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- Procedure를 생성하기 위해 다음 권한 중 하나가 있어야 한다.
    - Procedure가 속한 스키마에 대해 (CREATE PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
    - CREATE ANY PROCEDURE ON DATABASE
- OR REPLACE 절을 사용할 때 이미 procedure가 존재할 경우, 기존 procedure를 제거할 수 있는 다음 권한 중 하나가 있어야 한다.
    - 해당 procedure의 소유자
    - Procedure가 속한 스키마에 대해 (DROP PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
    - DROP ANY PROCEDURE ON DATABASE
- 구문을 수행한 사용자는 생성한 procedure의 소유자이다.

<a id="5b76df1d3f65089d"></a>
### 구문 규칙 및 파라미터

<a id="0fec289255f06d32"></a>
#### [ OR REPLACE ]

이미 procedure가 존재할 경우, 기존의 procedure를 대체한다.

<a id="56bc977bdb8abc88"></a>
#### PROC NAME

생성할 procedure의 이름으로써 스키마 내에서 고유한 이름이어야 한다.  
schema_name.proc_name과 같이 procedure가 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
Procedure 이름의 길이는 128 바이트보다 작아야 한다.

<a id="76e95cca1368587d"></a>
#### PARAM NAME

Procedure가 사용할 인자의 이름을 정의한다.   
각 인자의 이름은 procedure 내에서 고유한 이름이어야 한다.  
각 인자 이름의 길이는 128 바이트보다 작아야 한다.  
하나의 procedure에 사용할 수 있는 인자의 최대 개수에는 제한이 없다.

<a id="b28afe9d1268e671"></a>
#### Bind Type

각 인자의 bind type을 설정한다.   
표기하지 않을 경우 기본 타입은 IN이다.

<a id="281ef0e80ac2cf51"></a>
#### proc_characteristics

Procedure 수행 옵션을 정의한다. 같은 항목에 대해서는 한 번만 기술해야 한다.

- AUTHID CURRENT_USER: Procedure를 실행하는 중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되고 수행된다.
- AUTHID DEFINER: Procedure를 실행하는 중에 수행되는 SQL들은 definer의 authorization에 따라 해석되고 수행된다.

<a id="e8a566fe06af1053"></a>
#### item declaration

Procedure 내부에서 사용될 로컬 변수등의 item을 선언한다.  
PL block에서 선언될 수 있는 모든 item들을 선언할 수 있다.

<a id="4ea81d8c0c96d03e"></a>
#### PL Stmt List

Procedure의 body 부분으로써 수행할 PL statement들을 나열한다.  
Procedure의 내부에서는 '?'나 ':V1'과 같은 bind parameter를 사용할 수 없다.

<a id="0377f29c3dcb1555"></a>
### 설명

Schema-level SQL procedure를 정의한다. 생성된 procedure는 CALL 구문, anonymous block, 또는 다른 procedure/ function에서 호출될 수 있다.

Procedure의 정의는 INFORMATION_SCHEMA의 ROUTINES 테이블에서 확인할 수 있다. Procedure의 parameter들에 대한 정의는 INFORMATION_SCHEMA의 PARAMETERS 테이블에서 확인할 수 있다.

관련 객체들이 존재하지 않아 procedure가 일시적으로 불완전해졌을 경우, &lt;alter procedure&gt; 구문으로 plan을 다시 생성하려 시도해볼 수 있다.

생성된 procedure는 &lt;drop procedure&gt; 구문을 사용하여 제거할 수 있다.  
Procedure의 최대 생성 개수에는 제한이 없으므로 저장 공간에 문제가 없는 한 계속 생성할 수 있다.

<a id="f2ad0c302eb40887"></a>
### 사용 예

```
gSQL> CREATE OR REPLACE PROCEDURE PROC1( A1 INTEGER, A2 INTEGER )

  IS
    V1 INTEGER;
  BEGIN

    SELECT COUNT(*)
      INTO V1
      FROM T1
      WHERE T1.I1 >= A1 AND T1.I1 <= A2;

    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
  END;
  /

Procedure created.
```

<a id="2f9a2283606903c4"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="97b1e061f7125175"></a>
| Feature ID | 설명 | 지원여부 |
| --- | --- | --- |
| T471 | Result sets return value | X |
| T341 | Overloading of SQL-invoked functions and SQL-invoked procedures | X |
| S023 | Basic structured types | X |
| S241 | Transform functions | X |
| S024 | Enhanced structured types | X |
| T571 | Array-returning external SQL-invoked functions | X |
| T572 | Multiset-returning external SQL-invoked functions | X |
| S201 | SQL routines on arrays | X |
| S202 | SQL-invoked routines on multisets | X |
| T323 | Explicit security for external routines | X |
| S231 | Structured type locators | X |
| S232 | Array locators | X |
| S233 | Multiset locators | X |
| T041 | Basic LOB data type support | X |
| S027 | Create method by specific method name | X |
| T041 | Basic LOB data type support | X |
| T324 | Explicit security for SQL routines | O |
| T326 | Table functions | X |
| T651 | SQL-schema statements in SQL routines | X |
| T652 | SQL-dynamic statements in SQL routines | O |
| T653 | SQL-schema statements in external routines | X |
| T654 | SQL-dynamic statements in external routines | X |
| T655 | Cyclically dependent routines | X |
| T272 | Enhanced savepoint management | X |
| T522 | Default values for IN parameters of SQL-invoked procedures | O |
| B121 | Routine language Ada | X |
| B122 | Routine language C | X |
| B123 | Routine language COBOL | X |
| B124 | Routine language Fortran | X |
| B125 | Routine language MUMPS | X |
| B126 | Routine language Pascal | X |
| B127 | Routine language PL/I | X |
| B128 | Routine language SQL | O |
| B129 | Routine language Ada: VARCHAR and NUMERIC support | X |

<a id="ad2d4df307da0d51"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [DROP PROCEDURE](#3808c8dd15ec4e09)
- [ALTER PROCEDURE](#3cf929d08a31e4c0)

<a id="2e3b5a779150ed13"></a>
## DROP FUNCTION

<a id="b54f6eb7e36e75c1"></a>
### 기능

Function을 제거한다.

<a id="0c8df4467b51e7a0"></a>
### 구문

```
<drop function statement> ::=
    DROP FUNCTION [ IF EXISTS ] func_name
    ;
```

<a id="a3b7c300cbcc8454"></a>
### 사용 범위 및 접근 권한

&lt;drop function statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 function의 소유자
- Function이 속한 스키마에 대해 (DROP PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY PROCEDURE ON DATABASE

<a id="559482be024fa577"></a>
### 구문 규칙 및 파라미터

<a id="8d03de973f60a2b8"></a>
#### IF EXISTS

Function이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="9f762a1c2a54f369"></a>
#### FUNC NAME

제거할 function의 이름이다.  
schema_name.func_name과 같이 function이 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="8b9fa57364a63c3a"></a>
### 설명

지정된 schema-level function을 제거한다.

<a id="e8c6c438e1863e56"></a>
### 사용 예

```
gSQL> CREATE OR REPLACE FUNCTION FUNC1
RETURN INTEGER
 IS
    V1 INTEGER;
  BEGIN
    V1 := 10;
    RETURN V1;
  END;
  /

Function created.


COMMIT;

Commit complete.
gSQL> DROP FUNCTION FUNC1;

Function dropped.
```

<a id="7e29e1a0e9672a63"></a>
### 호환성

SQL 표준은 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="8a9da4229c2ce627"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="721add94d6fe4bd3"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE FUNCTION](#04b692603afa84f1)
- [ALTER FUNCTION](#f58959c250c9a4ad)

<a id="3808c8dd15ec4e09"></a>
## DROP PROCEDURE

<a id="809a6f546c571204"></a>
### 기능

Procedure를 제거한다.

<a id="9fe6f49e0d71fe60"></a>
### 구문

```
<drop procedure statement> ::=
    DROP PROCEDURE [ IF EXISTS ] proc_name
    ;
```

<a id="8b41b5896141f3b3"></a>
### 사용 범위 및 접근 권한

&lt;drop procedure statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 procedure의 소유자
- Procedure가 속한 스키마에 대해 (DROP PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY PROCEDURE ON DATABASE

<a id="7716cccb3584bd76"></a>
### 구문 규칙 및 파라미터

<a id="4849d266feb900ee"></a>
#### IF EXISTS

Procedure가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="6063153d8f365db4"></a>
#### PROC NAME

제거할 procedure의 이름이다.  
schema_name.proc_name과 같이 procedure가 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="8ab957a04b95d108"></a>
### 설명

지정된 schema-level procedure를 제거한다.

<a id="cb46e44e7d7b3f54"></a>
### 사용 예

```
gSQL> CREATE OR REPLACE PROCEDURE PROC1( A1 INTEGER, A2 INTEGER )
  IS
    V1 INTEGER;
  BEGIN

    SELECT COUNT(*)
      INTO V1
      FROM T1
      WHERE T1.I1 >= A1 AND T1.I1 <= A2;

    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
  END;
  /

Procedure created.


COMMIT;

Commit complete.


gSQL> DROP PROCEDURE PROC1;

Procedure dropped.
```

<a id="b4955904ff7ac706"></a>
### 호환성

SQL 표준은 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="c71e6e2d98a261aa"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="5362f4225eb9e7b1"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PROCEDURE](#58204d591b990498)
- [ALTER PROCEDURE](#3cf929d08a31e4c0)

---

[← 23. PSM Language Element References](23-psm-language-element-references.md) · [전체 목차](../README.md) · [25. ODBC →](../part-05-developer-manual/25-odbc.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
