<a id="db977ac39c3f704e"></a>

# 29. PSM SQL References

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/db977ac39c3f704e)  
> 태그: `22c.1_10_tag`

[← 28. PSM Language Element References](28-psm-language-element-references.md) · [전체 목차](../README.md) · [30. Database Connection →](../part-05-developer-manual/30-database-connection.md)

<a id="83d8af0ea46d316a"></a>
## ALTER FUNCTION

<a id="8ea545f10e12af39"></a>
### 기능

Function을 recompile 한다.

<a id="ce07ab02d7124b61"></a>
### 구문

```
<alter function statement> ::=
    ALTER FUNCTION function_name COMPILE
    ;
```

<a id="17413394443eb463"></a>
### 사용 범위 및 접근 권한

&lt;alter function statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 function의 소유자 
- Function이 속한 스키마에 대해 (ALTER PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY PROCEDURE ON DATABASE

<a id="8744a23b70768475"></a>
### 구문 규칙 및 파라미터

- Function name
    - Compile 할 function의 이름이다.
    - schema_name.func_name과 같이 function이 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="4c972e034c579db1"></a>
### 설명

지정된 schema-level function을 recompile 한다.

<a id="145c947123487ef0"></a>
### 사용 예

```
gSQL> ALTER FUNCTION FUNC1 COMPILE;

Function altered.
```

<a id="6b73776748268584"></a>
### 호환성

SQL 표준에서는 CREATE를 수행할 때 지정된 characteristic들을 변경하는 구문이고, GOLDILOCKS에서는 function의 plan을 다시 생성하는 구문이다.

**SQL 표준 호환성**

<a id="52056aba9e1ed3be"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="c6298849f4ce0e2a"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE FUNCTION](#ab87224881e1ecca)
- [DROP FUNCTION](#84b30fac2e4fd826)

<a id="768c9e07a5ad8128"></a>
## ALTER PACKAGE

<a id="a85722d98aca3e79"></a>
### 기능

Package를 recompile 한다.

<a id="2653fa0adb7e5f12"></a>
### 구문

```
<alter package statement> ::=
    ALTER PACKAGE package_name <package compile clause>
    ;

<package compile clause> ::=
    COMPILE [PACKAGE|SPECIFICATION|BODY]
```

<a id="dad621bff5626739"></a>
### 사용 범위 및 접근 권한

&lt;alter package statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 package의 소유자 
- Package가 속한 스키마에 대해 (ALTER PACKAGE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY PACKAGE ON DATABASE

<a id="df00d8201fbb6cf3"></a>
### 구문 규칙 및 파라미터

- Package name
    - Compile 할 package의 이름이다.
    - schema_name.package_name과 같이 package가 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

- Package compile clause
    - PACKAGE: Specification과 body를 모두 recompile 한다. (Default)
    - SPECIFICATION: Specification만 recompile 한다.
    - BODY: Body만 recompile 한다.

<a id="fdf76f4417d67565"></a>
### 설명

지정된 package를 recompile 한다.  
Compile 된 package의 실행 code는 plan cache에 저장된다.

<a id="3b22e53fdbba7e9b"></a>
### 사용 예

```
ALTER PACKAGE PKG1 COMPILE;
Package altered.
```

```
ALTER PACKAGE PKG1 COMPILE PACKAGE;
Package altered.
```

```
ALTER PACKAGE PKG1 COMPILE BODY;
Package altered.
```

<a id="02917d9872c1d427"></a>
### 호환성

SQL 표준에서는 ALTER MODULE 구문이다.

<a id="083a1b9c86b26efd"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE](#4e52d18bdace4911)
- [CREATE PACKAGE BODY](#46afadecf904ef1c)
- [DROP PACKAGE](#fc386565c607973f)

<a id="30c9f7e23906d0e1"></a>
## ALTER PROCEDURE

<a id="dd74abc4e6572add"></a>
### 기능

Procedure를 recompile 한다.

<a id="652abc9652f84ef3"></a>
### 구문

```
<alter procedure statement> ::=
    ALTER PROCEDURE proc_name COMPILE
    ;
```

<a id="df1f2db81f7469c1"></a>
### 사용 범위 및 접근 권한

&lt;alter procedure statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 procedure의 소유자 
- Procedure가 속한 스키마에 대해 (ALTER PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY PROCEDURE ON DATABASE

<a id="251399efb1a5b921"></a>
### 구문 규칙 및 파라미터

- Proc name
    - Compile할 procedure의 이름이다. 
    - schema_name.proc_name과 같이 procedure가 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="d68151854bcf908c"></a>
### 설명

지정된 schema-level procedure를 recompile 한다.

<a id="87f8c353a89abfaa"></a>
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

<a id="397b77b628a77b95"></a>
### 호환성

SQL 표준에서는 CREATE를 수행할 때 지정된 characteristic들을 변경하는 구문이고, GOLDILOCKS에서는 procedure의 plan을 다시 생성하는 구문이다.

**SQL 표준 호환성**

<a id="28325d79f0408543"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="69a9a9d338b557d6"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PROCEDURE](#cb8dd48d60714ba7)
- [DROP PROCEDURE](#d4f590ab9ed9207b)

<a id="4d37fd7827c46acf"></a>
## CALL Statement

<a id="2b18ea23154b4f4a"></a>
### 기능

Schema level procedure나 function을 수행한다.

<a id="724f955fc515f877"></a>
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

<a id="6155956711eca385"></a>
### 사용 범위 및 접근 권한

&lt;call statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다

- 해당 procedure에 대한 EXECUTE 권한
- Procedure가 속한 schema에 대해 (EXECUTE PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- EXECUTE ANY PROCEDURE ON DATABASE

<a id="05ac19c2d294f1e5"></a>
### 구문 규칙 및 파라미터

- proc_name
    - 실행할 procedure/ function의 이름이다 
    - Schema_name.Proc_name과 같이 procedure가 속한 schema를 포함할 수 있다. 
- value_expr
    - Procedure에 전달할 인자값을 표현한다. '?' 나 ':V1'과 같은 bind parameter를 사용할 수도 있다.

<a id="b18399cc34fc98f5"></a>
### 설명

명시된 인자들을 사용하여 schema level SQL procedure나 function을 실행한다.

&lt;sql call statement&gt; 형식 중에 function은 INTO 절 다음에 host variable 표현이나 dynamic bind parameter (?)를 사용하여 결과값을 반환한다.

&lt;odbc procedure call escape sequence&gt; 형식은 ODBC/ JDBC 등에서 PROCEDURE를 호출하기 위한   
표준 구문이며, GOLDILOCKS는 이 구문을 server에서 지원한다. (gsql 등의 tool에서도 사용 가능하다.)  
Function은 앞에 assign 표현( ? = )을 사용하여 결과값을 반환한다.

<a id="4d652735354de549"></a>
### 사용 예

<a id="f06080f3a0343945"></a>
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

<a id="24b6bc946b3ed3cd"></a>
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

<a id="3c2cba210ba83404"></a>
### 호환성

SQL 표준에서는 PROCEDURE에 대한 호출만 가능하여 [INTO] 절 이하를 정의하지 않고 있다.

<a id="ab87224881e1ecca"></a>
## CREATE FUNCTION

<a id="5f9e1a3a5a8cb136"></a>
### 기능

Schema level function을 정의한다.

<a id="3ad9a4677bffebe3"></a>
### 구문

```
<create function statement> ::= 
    CREATE [ OR REPLACE ] FUNCTION <function name> [ ( <parameter list> ) ]
       <return clause> 
       [ <function characteristics> ] 
       { IS | AS }  
       <item declaration>  
       BEGIN 
       <pl statement list> 
       END [ <function name> ]
    ; 

<parameter list> ::= 
      <parameter name> [ <parameter mode> ] <datatype> [ <parameter default> ] [ , ... ] 
 
<parameter mode> ::= 
      IN 
    | OUT 
    | IN OUT 
 
<parameter default> ::= 
      { := | DEFAULT } <value expression> 
 
<return clause> ::= 
      RETURN <datatype> 
    | RETURN TABLE ( <table function column list> ) 
 
<table function column list> ::=  
      <column name> <datatype> [ , ... ] 
 
<function characteristics> ::= 
      DETERMINISTIC 
    | AUTHID CURRENT_USER 
    | AUTHID DEFINER
```

<a id="0917d940ca1439f3"></a>
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

<a id="84fabec41df9d78f"></a>
### 구문 규칙 및 파라미터

<a id="3123af56cbf2f2ec"></a>
#### OR REPLACE

이미 function이 존재할 경우, 기존의 function을 새로운 function으로 대체한다.

<a id="3220f94cf4cfbaa7"></a>
#### function name

생성할 function의 이름으로써 스키마 내에서 고유한 이름이어야 한다.  
schema_name.function_name과 같이 function이 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
function 이름의 길이는 128 바이트보다 작아야 한다.

<a id="e0be1ee0b083dabf"></a>
#### parameter name

Function의 parameter 이름을 정의한다.  
각 parameter 이름은 function 내에서 고유해야 한다.  
즉, function의 parameter와 PL item은 동일한 이름을 가질 수 없다.  
Parameter 이름의 길이는 128 바이트보다 작아야 한다.  
하나의 function에서 사용할 수 있는 parameter의 최대 개수에는 제한이 없다.

<a id="acb8f8290dca406e"></a>
#### parameter mode

각 parameter mode를 설정한다.  
Parameter mode에는 IN, OUT, IN OUT이 있다.  
Parameter mode를 명시하지 않을 경우, 기본 mode는 IN이다.

<a id="4833d9f352551777"></a>
#### parameter default

Parameter의 기본값이다.  
Parameter default가 명시된 parameter는 function 실행할 때 생략할 수 있다.  
Parameter를 명시하지 않고 생략할 경우, parameter를 정의할 때 명시한 &lt;value expression&gt;을 기본값으로 가진다.  
&lt;value expression&gt;의 datatype은 parameter의 datatype이어야 한다.  
&lt;parameter default&gt;를 가진 parameter 이후에 정의되는 모든 parameter에는 &lt;parameter default&gt;가 있어야 한다.

<a id="59f36887c4d3edff"></a>
#### return clause

Function의 반환 형태를 정의한다.  
&lt;return clause&gt;에서는 다음과 같이 정의된다.

- RETURN &lt;datatype&gt;
    - Function에서 반환하는 반환값의 datatype을 정의한다.
- RETURN TABLE ( &lt;table function column list&gt; )
    - 반환하는 결과 집합의 table type을 정의한다.

<a id="00f9da1420ebe768"></a>
#### table function column list

Table function이 반환하는 결과 집합의 column 이름이다.  
Column 이름의 길이는 128 바이트보다 작아야 한다.  
Column 개수에는 제한이 없다.  
각 column 이름은 &lt;table function column list&gt;에서 고유하다.  
Column 이름은 parameter 및 declare item 이름과 동일할 수 있다.  
&lt;table function column list&gt;에 정의된 column은 function의 PL block 내에서 참조할 수 없다.

<a id="26ac46a078c32cd0"></a>
#### function characteristics

Function 수행 옵션을 정의한다. 같은 항목에 대해서는 한 번만 기술해야 한다.

- DETERMINISTIC: 동일한 인자값들이 입력될 경우 해당 function은 항상 동일한 결과값을 반환한다.
- AUTHID CURRENT_USER: Function을 실행하는 도중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되고 수행된다.
- AUTHID DEFINER: Function을 실행하는 도중에 수행되는 SQL들은 definer의 authorization에 따라 해석되고 수행된다.

<a id="9926006d174d3732"></a>
#### Item Declaration

Function 내부에서 사용될 로컬 변수 등의 item을 선언한다.   
PL block에서 선언가능한 모든 item들을 선언할 수 있다.

<a id="627cbaffca2d7be8"></a>
#### PL Stmt List

Function의 body 부분으로써 수행할 PL statement들을 나열한다.   
Function의 내부에는 '?'나 ':V1'과 같은 bind parameter를 사용할 수 없다.

<a id="6faf1435631a5126"></a>
### 설명

Schema-level SQL function을 정의한다. 생성된 function은 모든 expression에서 호출될 수 있다.

Function의 정의는 INFORMATION_SCHEMA의 ROUTINES 테이블에서 확인할 수 있다. Function의 parameter들에 대한 정의는 INFORMATION_SCHEMA의 PARAMETERS 테이블에서 확인할 수 있다.

관련 객체들이 존재하지 않아 function이 일시적으로 불완전해졌을 경우, [ALTER FUNCTION](#83d8af0ea46d316a) 구문으로 plan 생성을 다시 시도해볼 수 있다.

생성된 function은 [DROP FUNCTION](#84b30fac2e4fd826) 구문을 사용하여 제거할 수 있다.  
Function의 최대 생성 개수에는 제한이 없으므로 저장 공간에 문제가 없는 한 계속 생성할 수 있다.

<a id="51feca88cec149f3"></a>
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

<a id="df385575e057075e"></a>
### 호환성

SQL 표준에서는 OR REPLACE 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="2bb45f96e8233af0"></a>
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
| T326 | Table functions | O |
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

<a id="e0d19b4e78273328"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [DROP FUNCTION](#84b30fac2e4fd826)
- [ALTER FUNCTION](#83d8af0ea46d316a)

<a id="4e52d18bdace4911"></a>
## CREATE PACKAGE

<a id="f7d53f7624fa1248"></a>
### 기능

Package 내에서 사용될 public item들에 대한 spec을 정의한다.

<a id="8089f4ee922bef0f"></a>
### 구문

```
<create package statement> ::=
    CREATE [ OR REPLACE ]  
        PACKAGE package_name 
        [ <package_characteristics> ]
        { IS | AS }
       <item_declaration> 
    END
    ;

<package_characteristics> ::=
    AUTHID CURRENT_USER | AUTHID DEFINER

<item_declaration> ::=    <variable declaration> 
                        | <cursor declaration>
                        | <user-defined type declaration> 
                        | <function declaration> 
                        | <procedure declaration> 
                        | <user exception declaration>
                        | <cursor definition>
```

<a id="824ffd64e61335c2"></a>
### 사용 범위 및 접근 권한

&lt;create package statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- Package를 생성하려면 다음 권한 중 하나가 있어야 한다.
    - Package가 속한 스키마에 대해 (CREATE PACKAGE 또는 CONTROL SCHEMA) ON SCHEMA
    - CREATE ANY PACKAGE ON DATABASE
- OR REPLACE 절을 사용할 때 이미 package가 존재할 경우, 기존 package를 제거할 수 있는 다음 권한 중 하나가 있어야 한다.
    - 해당 package의 소유자
    - Package가 속한 스키마에 대해 (DROP PACKAGE 또는 CONTROL SCHEMA) ON SCHEMA
**DROP ANY PACKAGE ON DATABASE
- 구문을 수행한 사용자는 생성한 package의 소유자이다.

<a id="e9b62c84f2336cc0"></a>
### 구문 규칙 및 파라미터

<a id="79d970463106e5f0"></a>
#### OR REPLACE

이미 package가 존재할 경우, 기존의 package specification을 대체한다.

<a id="137ca71f9aabf87b"></a>
#### PACKAGE NAME

생성할 package의 이름이며, schema 내에서 유일한 이름이어야 한다.   
schema_name.package_name과 같이 package가 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
Package 이름의 길이는 128 바이트보다 작아야 한다.

<a id="999ee60f22b7f7ba"></a>
#### Package Characteristics

Package를 수행하는 옵션을 정의한다. 같은 항목에 대해서는 한 번만 기술해야 한다.

- AUTHID CURRENT_USER: Package 내의 item들이 실행되는 도중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되어 수행된다. 
- AUTHID DEFINER: Package 내의 item들이 실행되는 도중에 수행되는 SQL들은 definer의 authorization에 따라 해석되어 수행된다.

<a id="f5695074a1107b5c"></a>
#### Item Declaration

Package 외부에서 접근 가능한 public 변수, type, 커서, 커서 변수, function spec, procedure spec을 선언한다.   
Package 내의 function과 procedure는 반드시 create package body 구문을 통해 정의되어야 한다.   
Package 내에서 SQL 없이 선언만 된 커서는 반드시 create package body 구문을 통해 정의되어야 한다.   
또한 package 내의 function, procedure, 커서의 argument와 반환 타입들은 body 구문 내에 정의된 것과 일치해야 한다.

<a id="08d5040f8c72d4c2"></a>
### 설명

Schema-level package specification을 생성한다.   
생성된 package의 모든 public item은 다른 procedure/ function/ package/ anonymous block 들에 의해 참조될 수 있다.

Package 생성 정보는 DEFINITION_SCHEMA나 INFORMATION_SCHEMA의 MODULES 테이블에서 확인할 수 있다.   
Package 내의 공개된 각 procedure/ function 목록은 DEFINITION_SCHEMA나 INFORMATION_SCHEMA 의 ROUTINES 테이블에서 확인할 수 있다.   
Package 내의 공개된 각 procedure/ function의 parameter들에 대한 정의는 DEFINITION_SCHEMA나 INFORMATION_SCHEMA의 PARAMETERS 테이블에서 확인할 수 있다.   
공개되지 않은 procedure/ function은 MODULE_BODY 테이블에서 확인할 수 있다.   
Package 내의 procedure/ function 변수가 참조하는 object들의 정보가 일시적으로 불완전해졌을 경우, &lt;alter package&gt; 구문으로 recompile을 시도해 볼 수 있다.

<a id="0379baaf3a00ec5c"></a>
### 사용 예

```
CREATE OR REPLACE PACKAGE PKG1
IS
  V1 INTEGER;
  PROCEDURE PROC1;
  FUNCTION FUNC1 RETURN INTEGER;
END;
/

Package created.
```

<a id="07c545ad643fa8cf"></a>
### 호환성

SQL 표준에서는 CREATE MODULE 구문이다.

<a id="e6eab7b69f1b3127"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE BODY](#46afadecf904ef1c)
- [DROP PACKAGE](#fc386565c607973f)
- [ALTER PACKAGE](#768c9e07a5ad8128)

<a id="46afadecf904ef1c"></a>
## CREATE PACKAGE BODY

<a id="d28f1f4eae40a5fe"></a>
### 기능

Package 내에서 사용될 procedure/ function/ 커서들에 대한 정의를 생성한다.

<a id="23e54c64828555b4"></a>
### 구문

```
<create package body statement> ::=
    CREATE [ OR REPLACE ] PACKAGE BODY package_name 
    { IS | AS } 
       <item_declaration> 
       <cursor_definition> 
       <routine_definition>
    [ BEGIN <initialization part> ]
    END
    ;

<item_declaration> ::=    VARIABLE_DECLARATION 
                        | CURSOR_DECLARATION
                        | USER_DEFINED_TYPE_DEFINITION 
                        | FUNCTION_DECLARATION 
                        | PROCEDURE_DECLARATION  
                        | USER_EXCEPTION_DECLARATION

<routine_definition> ::= FUNCTION_DEFINITION
                       | PROCEDURE_DEFINITION

<initialization part> ::= <pl_stmt_list>
```

<a id="bedba3b4a6cc0961"></a>
### 사용 범위 및 접근 권한

&lt;create package body statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- Package body를 생성하려면 다음 권한 중 하나가 있어야 한다.
    - Package가 속한 스키마에 대해 (CREATE PACKAGE 또는 CONTROL SCHEMA) ON SCHEMA
    - CREATE ANY PACKAGE ON DATABASE
- Package spec이 이미 정의되어 있는 상태이어야 한다.
- OR REPLACE 절을 사용할 때 package body가 이미 존재할 경우, 기존 package를 제거할 수 있는 다음 권한 중 하나가 있어야 한다.
    - 해당 package의 소유자
    - Package가 속한 스키마에 대해 (DROP PACKAGE 또는 CONTROL SCHEMA) ON SCHEMA
    - DROP ANY PACKAGE ON DATABASE
- 구문을 수행한 사용자는 생성한 package의 소유자이다.

<a id="2128d4b60ccca9de"></a>
### 구문 규칙 및 파라미터

<a id="29c84e8a58d4deb7"></a>
#### OR REPLACE

Package body가 이미 존재할 경우, 기존의 package body definition을 대체한다.

<a id="38392d81be8847a9"></a>
#### PACKAGE NAME

생성할 package body의 이름이며, package spec 생성에 사용된 동일한 이름을 사용해야 한다. schema 내에서 유일한 이름이어야 한다.   
schema_name.package_name 과 같이 package가 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
Package 이름의 길이는 128 바이트보다 작아야 한다.

<a id="c2bd4498c9dc4212"></a>
#### Item Declaration

Package body 내에서 사용할 PSM identifier들 (변수, type, 커서, function spec, procedure spec, exception 등)을 선언한다.   
Package spec 내에 선언된 routine들은 반드시 package body에서 정의되어야 한다.   
Package spec 내에서 SQL 없이 선언만 된 커서들은 반드시 package body에 정의되어야 한다.   
또한 package 내의 function, procedure, 커서의 argument 및 반환 타입들은 body 구문 내에 정의된 것과 일치해야 한다.

<a id="2463df7bfb05bb1d"></a>
#### Initialization Part

Package instance 생성 과정에서 내부 변수등의 초기화를 위해 한 번만 수행되는 구문들을 기술한다.

<a id="7718a7e804143bfa"></a>
### 설명

Schema-level package body를 생성한다.   
생성된 package body의 모든 private item은 다른 procedure/ function/ package/ anonymous block 들에 의해 참조될 수 없고 해당 package body 내에서만 사용된다.

Package body의 생성 정보는 DEFINITION_SCHEMA나 INFORMATION_SCHEMA의 MODULE_BODY 테이블에서 확인할 수 있다.   
Package body 내의 각 private item들의 목록은 DEFINITION_SCHEMA나 INFORMATION_SCHEMA에서 확인할 수 없다.   
Package 내의 procedure/ function/ 변수가 참조하는 object들의 정보가 일시적으로 불완전해졌을 경우, &lt;alter package body&gt; 구문으로 recompile을 시도해 볼 수 있다.

생성된 package body는 &lt;drop package&gt;나 &lt;drop package body&gt; 구문으로 삭제할 수 있다.

<a id="e71cc1b2402bab6b"></a>
### 사용 예

```
CREATE OR REPLACE PACKAGE PKG1
IS
  V1 INTEGER;
  PROCEDURE PROC1;
  FUNCTION FUNC1 RETURN INTEGER;
END;
/

Package created.

CREATE OR REPLACE PACKAGE BODY PKG1
IS
  FUNCTION FUNC1 RETURN INTEGER
  IS
  BEGIN
      RETURN V1;
  END;

  PROCEDURE PROC1
  IS
  BEGIN
      IF V1 IS NULL
      THEN
          V1 := 10;
      ELSE
          V1 := V1 + 10;
      END IF;
  END;

END;
/

Package created.
```

<a id="7ce56091dfb8cbf9"></a>
### 호환성

SQL 표준에는 정의되어 있지 않다.

<a id="7eea3ecfb620d839"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE](#4e52d18bdace4911)
- [DROP PACKAGE](#fc386565c607973f)
- [ALTER PACKAGE](#768c9e07a5ad8128)

<a id="cb8dd48d60714ba7"></a>
## CREATE PROCEDURE

<a id="4bd28b45407c1a2a"></a>
### 기능

Schema-level procedure를 정의한다.

<a id="f0cc971c31a4666e"></a>
### 구문

```
<create procedure statement> ::=
      CREATE [ OR REPLACE ] PROCEDURE <procedure name> [ ( <parameter list> ) ]
      { IS | AS } 
      <item declaration>  
      BEGIN
      <pl statement list> 
      END [ <procedure name> ]
      ;
 
<parameter list> ::= 
      <parameter name> [ <parameter mode> ] <datatype> [ <parameter default> ] [ , ... ] 

<parameter mode> ::= 
      IN 
    | OUT 
    | IN OUT 
 
<parameter default> ::= 
      { := | DEFAULT } <value expression> 

<procedure characteristics> ::= 
      AUTHID CURRENT_USER 
    | AUTHID DEFINER
```

<a id="1537af54b903064e"></a>
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

<a id="2758a63a380e061d"></a>
### 구문 규칙 및 파라미터

<a id="ee4d92a796a687ac"></a>
#### OR REPLACE

이미 procedure가 존재할 경우, 기존의 procedure를 새로운 procedure로 대체한다.

<a id="4aaa1e3989bc4947"></a>
#### procedure name

생성할 procedure의 이름으로써 스키마 내에서 고유한 이름이어야 한다.  
schema_name.procedure_name과 같이 procedure가 속할 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
procedure 이름의 길이는 128 바이트보다 작아야 한다.

<a id="f124a3e09819d224"></a>
#### parameter name

Procedure의 parameter 이름을 정의한다.  
각 parameter 이름은 procedure 내에서 고유해야 한다.  
즉, procedure의 parameter와 PL item은 동일한 이름을 가질 수 없다.  
parameter 이름의 길이는 128 바이트보다 작아야 한다.  
하나의 procedure에서 사용할 수 있는 parameter의 최대 개수에는 제한이 없다.

<a id="c46e54b98c915450"></a>
#### parameter mode

각 parameter mode를 설정한다.  
Parameter mode에는 IN, OUT, IN OUT이 있다.  
Parameter mode를 명시하지 않을 경우, 기본 mode는 IN이다.

<a id="92118dff5e3be00b"></a>
#### parameter default

Parameter의 기본값이다.  
Parameter default가 명시된 parameter는 procedure 실행할 때 생략할 수 있다.  
Parameter를 명시하지 않고 생략할 경우, parameter를 정의할 때 명시한 &lt;value expression&gt;을 기본값으로 가진다.  
&lt;value expression&gt;의 datatype은 parameter의 datatype이어야 한다.  
&lt;parameter default&gt;를 가진 parameter 이후에 정의되는 모든 parameter에는 &lt;parameter default&gt;가 있어야 한다.

<a id="e4cee8839ddb2f65"></a>
#### procedure characteristics

Procedure 수행 옵션을 정의한다. 같은 항목에 대해서는 한 번만 기술해야 한다.

- AUTHID CURRENT_USER: Procedure를 실행하는 도중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되고 수행된다.
- AUTHID DEFINER: Procedure를 실행하는 도중에 수행되는 SQL들은 definer의 authorization에 따라 해석되고 수행된다.

<a id="7dca80e9fa37427b"></a>
#### Item Declaration

Procedure 내부에서 사용될 로컬 변수 등의 item을 선언한다.  
PL block에서 선언가능한 모든 item들을 선언할 수 있다.

<a id="fc47a54be9a935c2"></a>
#### PL Stmt List

Procedure의 body 부분으로써 수행할 PL statement들을 나열한다.   
Procedure의 내부에는 '?'나 ':V1'과 같은 bind parameter를 사용할 수 없다.

<a id="90e548af0e352bb4"></a>
### 설명

Schema-level SQL procedure를 정의한다. 생성된 procedure는 CALL 구문, anonymous block, 또는 다른 procedure/ function에서 호출될 수 있다.

Procedure의 정의는 INFORMATION_SCHEMA의 ROUTINES 테이블에서 확인할 수 있다. Procedure의 parameter들에 대한 정의는 INFORMATION_SCHEMA의 PARAMETERS 테이블에서 확인할 수 있다.

관련 객체들이 존재하지 않아 procedure가 일시적으로 불완전해졌을 경우, [ALTER PROCEDURE](#30c9f7e23906d0e1) 구문으로 plan 생성을 다시 시도해볼 수 있다.

생성된 procedure는 [DROP PROCEDURE](#d4f590ab9ed9207b) 구문을 사용하여 제거할 수 있다.  
Procedure의 최대 생성 개수에는 제한이 없으므로 저장 공간에 문제가 없는 한 계속 생성할 수 있다.

<a id="d10093b3ff4ddb50"></a>
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

<a id="20a785741a7f5289"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="4c8ded0b82102cd9"></a>
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
| T326 | Table functions | O |
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

<a id="aef8b687eff1527e"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [DROP PROCEDURE](#d4f590ab9ed9207b)
- [ALTER PROCEDURE](#30c9f7e23906d0e1)

<a id="84b30fac2e4fd826"></a>
## DROP FUNCTION

<a id="75528dca9b10919e"></a>
### 기능

Function을 제거한다.

<a id="918a7959384f65e1"></a>
### 구문

```
<drop function statement> ::=
    DROP FUNCTION [ IF EXISTS ] func_name
    ;
```

<a id="5e502a3e84752019"></a>
### 사용 범위 및 접근 권한

&lt;drop function statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 function의 소유자
- Function이 속한 스키마에 대해 (DROP PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY PROCEDURE ON DATABASE

<a id="0c9aa1bb4bc1cc7a"></a>
### 구문 규칙 및 파라미터

<a id="f78920c588f7e93f"></a>
#### IF EXISTS

Function이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="9f42fda2236a309e"></a>
#### FUNC NAME

제거할 function의 이름이다.   
schema_name.func_name과 같이 function이 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="df0f5e0defb6da0e"></a>
### 설명

지정된 schema-level function을 제거한다.

<a id="57fa08877e42331c"></a>
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

<a id="2d177440d235f15d"></a>
### 호환성

SQL 표준은 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="c6c3f9ccf14a200d"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="59c35b953ebfda9b"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE FUNCTION](#ab87224881e1ecca)
- [ALTER FUNCTION](#83d8af0ea46d316a)

<a id="fc386565c607973f"></a>
## DROP PACKAGE

<a id="47363f3f68f7ddc1"></a>
### 기능

Package (body만 또는 spec/ body 모두)를 제거한다.

<a id="deed3c583728a840"></a>
### 구문

```
<drop package statement> ::=
    DROP PACKAGE [BODY] [ IF EXISTS ] package_name
    ;
```

<a id="eea407679b27270b"></a>
### 사용 범위 및 접근 권한

&lt;drop package statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 package의 소유자 
- Package가 속한 스키마에 대해 (DROP PACKAGE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY PACKAGE ON DATABASE

<a id="4fcc789622cca6b4"></a>
### 구문 규칙 및 파라미터

<a id="3dfdfece28c62ba2"></a>
#### BODY

주어진 이름을 가진 package의 body 객체만 제거한다. *BODY* 라는 키워드를 명시하지 않은 경우 package specification과 body를 모두 삭제한다.

<a id="9f4f2a39844c88bd"></a>
#### IF EXISTS

Package가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="9819d1dde369e598"></a>
#### PACKAGE NAME

제거할 package의 이름이다.   
schema_name.package_name 과 같이 package가 소속한 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="24729ce305f990f9"></a>
### 설명

지정된 package object를 제거한다.

<a id="1ae34e42089ac56c"></a>
### 사용 예

```
CREATE PACKAGE PKG1
  IS
    V1 INTEGER;
    FUNCTION FUNC1 (A1 INTEGER) RETURN INTEGER;
  END;
  /

Package created.

DROP PACKAGE IF EXISTS PKG1;

Package dropped.
```

<a id="b8c868351d4c2f8a"></a>
### 호환성

SQL 표준에서는 DRO MODULE 구문이다.

<a id="68a2704767fc8184"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE](#4e52d18bdace4911)
- [CREATE PACKAGE BODY](#46afadecf904ef1c)
- [ALTER PACKAGE](#768c9e07a5ad8128)

<a id="d4f590ab9ed9207b"></a>
## DROP PROCEDURE

<a id="e25123a54f6e960b"></a>
### 기능

Procedure를 제거한다.

<a id="45e3722508ec060d"></a>
### 구문

```
<drop procedure statement> ::=
    DROP PROCEDURE [ IF EXISTS ] proc_name
    ;
```

<a id="2c466509cf721b95"></a>
### 사용 범위 및 접근 권한

&lt;drop procedure statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 procedure의 소유자
- Procedure가 속한 스키마에 대해 (DROP PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY PROCEDURE ON DATABASE

<a id="0bfe3db1cf2d475e"></a>
### 구문 규칙 및 파라미터

<a id="ea304060b7964dbe"></a>
#### IF EXISTS

Procedure가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="3fefa28170695f96"></a>
#### PROC NAME

제거할 procedure의 이름이다.   
schema_name.proc_name과 같이 procedure가 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="e5ef39f053d62955"></a>
### 설명

지정된 schema-level procedure를 제거한다.

<a id="2542df3522430fcf"></a>
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

<a id="e50bc1de66bcdd12"></a>
### 호환성

SQL 표준은 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="5d7f280e0ea4c295"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="06840c2db9b2b8c8"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PROCEDURE](#cb8dd48d60714ba7)
- [ALTER PROCEDURE](#30c9f7e23906d0e1)

---

[← 28. PSM Language Element References](28-psm-language-element-references.md) · [전체 목차](../README.md) · [30. Database Connection →](../part-05-developer-manual/30-database-connection.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
