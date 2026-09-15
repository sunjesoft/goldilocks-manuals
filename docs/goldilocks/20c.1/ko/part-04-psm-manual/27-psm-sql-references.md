<a id="4cfd7c52f438581e"></a>

# 27. PSM SQL References

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/4cfd7c52f438581e)  
> 태그: `20c.1_30_tag`

[← 26. PSM Language Element References](26-psm-language-element-references.md) · [전체 목차](../README.md) · [28. Database Connection →](../part-05-developer-manual/28-database-connection.md)

<a id="44ac55a48dad006a"></a>
## ALTER FUNCTION

<a id="80810b573bb7e741"></a>
### 기능

Function을 recompile 한다.

<a id="bf8a198d8d81a06c"></a>
### 구문

```
<alter function statement> ::=
    ALTER FUNCTION function_name COMPILE
    ;
```

<a id="58c434f682954add"></a>
### 사용 범위 및 접근 권한

&lt;alter function statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 function의 소유자 
- Function이 속한 스키마에 대해 (ALTER PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY PROCEDURE ON DATABASE

<a id="ba6644f8e1d05eac"></a>
### 구문 규칙 및 파라미터

- Function name
    - Compile 할 function의 이름이다.
    - schema_name.func_name과 같이 function이 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="5791cf4c53cc857b"></a>
### 설명

지정된 schema-level function을 recompile 한다.

<a id="06a7fb8ca38485e8"></a>
### 사용 예

```
gSQL> ALTER FUNCTION FUNC1 COMPILE;

Function altered.
```

<a id="e35b0e23c752c503"></a>
### 호환성

SQL 표준에서는 CREATE를 수행할 때 지정된 characteristic들을 변경하는 구문이고, GOLDILOCKS에서는 function의 plan을 다시 생성하는 구문이다.

**SQL 표준 호환성**

<a id="da4f9c6e8a03c392"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="c5cb075551a44a10"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE FUNCTION](#243dff1382985279)
- [DROP FUNCTION](#399ca1e28092268f)

<a id="d832fc93cc42dd95"></a>
## ALTER PACKAGE

<a id="136f5400415ca43a"></a>
### 기능

Package를 recompile 한다.

<a id="ffe0ddbdf5d0b9b9"></a>
### 구문

```
<alter package statement> ::=
    ALTER PACKAGE package_name <package compile clause>
    ;

<package compile clause> ::=
    COMPILE [PACKAGE|SPECIFICATION|BODY]
```

<a id="d996fb656e7c04a7"></a>
### 사용 범위 및 접근 권한

&lt;alter package statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 package의 소유자 
- Package가 속한 스키마에 대해 (ALTER PACKAGE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY PACKAGE ON DATABASE

<a id="763f50f6cf936f75"></a>
### 구문 규칙 및 파라미터

- Package name
    - Compile 할 package의 이름이다.
    - schema_name.package_name과 같이 package가 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

- Package compile clause
    - PACKAGE: Specification과 body를 모두 recompile 한다. (Default)
    - SPECIFICATION: Specification만 recompile 한다.
    - BODY: Body만 recompile 한다.

<a id="fe1ecc3144e68310"></a>
### 설명

지정된 package를 recompile 한다.  
Compile 된 package의 실행 code는 plan cache에 저장된다.

<a id="e37af944c0e6351f"></a>
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

<a id="ecb9a264ce634c38"></a>
### 호환성

SQL 표준에서는 ALTER MODULE 구문이다.

<a id="9394b8a11b73f12e"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE](#6aabbd4af8bb049b)
- [CREATE PACKAGE BODY](#be7bb0a00a34c743)
- [DROP PACKAGE](#6d701903dec1e955)

<a id="7ae8df29fbc9e0ae"></a>
## ALTER PROCEDURE

<a id="0b19fddeda6e63d8"></a>
### 기능

Procedure를 recompile 한다.

<a id="fe2c7a4bc71b0076"></a>
### 구문

```
<alter procedure statement> ::=
    ALTER PROCEDURE proc_name COMPILE
    ;
```

<a id="4acd12f09afe5bb4"></a>
### 사용 범위 및 접근 권한

&lt;alter procedure statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 procedure의 소유자 
- Procedure가 속한 스키마에 대해 (ALTER PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY PROCEDURE ON DATABASE

<a id="0c687a013f724ca6"></a>
### 구문 규칙 및 파라미터

- Proc name
    - Compile할 procedure의 이름이다. 
    - schema_name.proc_name과 같이 procedure가 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="28860f56b2e4e628"></a>
### 설명

지정된 schema-level procedure를 recompile 한다.

<a id="34d85900c9aceed4"></a>
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

<a id="7b5d9a4bcc1ae026"></a>
### 호환성

SQL 표준에서는 CREATE를 수행할 때 지정된 characteristic들을 변경하는 구문이고, GOLDILOCKS에서는 procedure의 plan을 다시 생성하는 구문이다.

**SQL 표준 호환성**

<a id="2bed9294b0cd30db"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="db48d36579ec0474"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PROCEDURE](#e2d083dd25c36aa9)
- [DROP PROCEDURE](#d133d98fe19742b0)

<a id="7bcf573258b09647"></a>
## CALL Statement

<a id="e8529dc64a0d87dc"></a>
### 기능

Schema level procedure나 function을 수행한다.

<a id="e3acf165964b9fba"></a>
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

<a id="9a5d1718e288e449"></a>
### 사용 범위 및 접근 권한

&lt;call statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다

- 해당 procedure에 대한 EXECUTE 권한
- Procedure가 속한 schema에 대해 (EXECUTE PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- EXECUTE ANY PROCEDURE ON DATABASE

<a id="9e214234650ac159"></a>
### 구문 규칙 및 파라미터

- proc_name
    - 실행할 procedure/ function의 이름이다 
    - Schema_name.Proc_name과 같이 procedure가 속한 schema를 포함할 수 있다. 
- value_expr
    - Procedure에 전달할 인자값을 표현한다. '?' 나 ':V1'과 같은 bind parameter를 사용할 수도 있다.

<a id="5381678c2205be96"></a>
### 설명

명시된 인자들을 사용하여 schema level SQL procedure나 function을 실행한다.

&lt;sql call statement&gt; 형식 중에 function은 INTO 절 다음에 host variable 표현이나 dynamic bind parameter (?)를 사용하여 결과값을 반환한다.

&lt;odbc procedure call escape sequence&gt; 형식은 ODBC/ JDBC 등에서 PROCEDURE를 호출하기 위한   
표준 구문이며, GOLDILOCKS는 이 구문을 server에서 지원한다. (gsql 등의 tool에서도 사용 가능하다.)  
Function은 앞에 assign 표현( ? = )을 사용하여 결과값을 반환한다.

<a id="9423479ec137b62e"></a>
### 사용 예

<a id="7dc1117c29bc963f"></a>
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

<a id="7b475ed7187ad2e2"></a>
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

<a id="2ef8682e3c0cc157"></a>
### 호환성

SQL 표준에서는 PROCEDURE에 대한 호출만 가능하여 [INTO] 절 이하를 정의하지 않고 있다.

<a id="243dff1382985279"></a>
## CREATE FUNCTION

<a id="752c61dc99ffec53"></a>
### 기능

Schema level function을 정의한다.

<a id="c8f5825385da8b95"></a>
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

<a id="f9c0f96c35b734c2"></a>
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

<a id="a4507527763c43b4"></a>
### 구문 규칙 및 파라미터

<a id="4917189afc191f2a"></a>
#### OR REPLACE

이미 function이 존재할 경우, 기존의 function을 대체한다.

<a id="28df45a8b8cb94a9"></a>
#### FUNCTION NAME

생성할 function의 이름으로써 스키마 내에서 고유한 이름이어야 한다.  
schema_name.func_name과 같이 function이 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
Function 이름의 길이는 128 바이트보다 작아야 한다.

<a id="a47112050a344910"></a>
#### PARAM NAME

Function이 사용할 인자의 이름을 정의한다.  
각 인자의 이름은 function 내에서 고유한 이름이어야 한다.  
각 인자 이름의 길이는 128 바이트보다 작아야 한다.  
하나의 function에 사용할 수 있는 인자의 최대 개수에는 제한이 없다.

<a id="9e153c69cb8283ae"></a>
#### Bind Type

각 인자의 bind type을 설정한다.   
표기하지 않을 경우 기본 타입은 IN 이다.

<a id="c9a817d58f84769b"></a>
#### Func_Characteristics

Function 수행 옵션을 정의한다. 같은 항목에 대해서는 한 번만 기술해야 한다.

- DETERMINISTIC: 동일한 인자값들이 입력될 경우 해당 function은 항상 동일한 결과값을 반환한다.
- AUTHID CURRENT_USER: Function을 실행하는 중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되고 수행된다.
- AUTHID DEFINER: Function을 실행하는 중에 수행되는 SQL들은 definer의 authorization에 따라 해석되고 수행된다.

<a id="c212fe28c7332d95"></a>
#### Item Declaration

Function 내부에서 사용될 로컬 변수등의 item을 선언한다.   
PL block에서 선언될 수 있는 모든 item들을 선언할 수 있다.

<a id="656aac9fef0a7ce1"></a>
#### PL Stmt List

Function의 body 부분으로써 수행할 PL statement들을 나열한다.   
Function의 내부에서는 '?'나 ':V1'과 같은 bind parameter를 사용할 수 없다.

<a id="981a58092a2c4610"></a>
### 설명

Schema-level SQL function을 정의한다. 생성된 function은 모든 expression에서 호출될 수 있다.

Function의 정의는 INFORMATION_SCHEMA의 ROUTINES 테이블에서 확인할 수 있다. Function의 parameter들에 대한 정의는 INFORMATION_SCHEMA의 PARAMETERS 테이블에서 확인할 수 있다.

관련 객체들이 존재하지 않아 function이 일시적으로 불완전해졌을 경우, &lt;alter function&gt; 구문으로 plan을 다시 생성하려 시도해볼 수 있다.

생성된 function은 &lt;drop function&gt; 구문을 사용하여 제거할 수 있다.  
Function의 최대 생성 개수에는 제한이 없으므로 저장 공간에 문제가 없는 한 계속 생성할 수 있다.

<a id="5fcdffd7b45c7667"></a>
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

<a id="01d90babdecd3870"></a>
### 호환성

SQL 표준에서는 OR REPLACE 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="f95e4179f8807eb3"></a>
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

<a id="335208ecd4fcb1cf"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [DROP FUNCTION](#399ca1e28092268f)
- [ALTER FUNCTION](#44ac55a48dad006a)

<a id="6aabbd4af8bb049b"></a>
## CREATE PACKAGE

<a id="cfcdca9cd9ee6089"></a>
### 기능

Package 내에서 사용될 public item들에 대한 spec을 정의한다.

<a id="cde8f7c6bc3ab234"></a>
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

<a id="6a27b6182bcd2cc5"></a>
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

<a id="a110608e7d65cb8b"></a>
### 구문 규칙 및 파라미터

<a id="8f19789b6ac8a92c"></a>
#### OR REPLACE

이미 package가 존재할 경우, 기존의 package specification을 대체한다.

<a id="8fd79bdd36c8669b"></a>
#### PACKAGE NAME

생성할 package의 이름이며, schema 내에서 유일한 이름이어야 한다.   
schema_name.package_name과 같이 package가 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
Package 이름의 길이는 128 바이트보다 작아야 한다.

<a id="ff91f5f86c9cebac"></a>
#### Package Characteristics

Package를 수행하는 옵션을 정의한다. 같은 항목에 대해서는 한 번만 기술해야 한다.

- AUTHID CURRENT_USER: Package 내의 item들이 실행되는 도중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되어 수행된다. 
- AUTHID DEFINER: Package 내의 item들이 실행되는 도중에 수행되는 SQL들은 definer의 authorization에 따라 해석되어 수행된다.

<a id="11b27f76a71ca7ed"></a>
#### Item Declaration

Package 외부에서 접근 가능한 public 변수, type, 커서, 커서 변수, function spec, procedure spec을 선언한다.   
Package 내의 function과 procedure는 반드시 create package body 구문을 통해 정의되어야 한다.   
Package 내에서 SQL 없이 선언만 된 커서는 반드시 create package body 구문을 통해 정의되어야 한다.   
또한 package 내의 function, procedure, 커서의 argument와 반환 타입들은 body 구문 내에 정의된 것과 일치해야 한다.

<a id="8175937fbb4e8f80"></a>
### 설명

Schema-level package specification을 생성한다.   
생성된 package의 모든 public item은 다른 procedure/ function/ package/ anonymous block 들에 의해 참조될 수 있다.

Package 생성 정보는 DEFINITION_SCHEMA나 INFORMATION_SCHEMA의 MODULES 테이블에서 확인할 수 있다.   
Package 내의 공개된 각 procedure/ function 목록은 DEFINITION_SCHEMA나 INFORMATION_SCHEMA 의 ROUTINES 테이블에서 확인할 수 있다.   
Package 내의 공개된 각 procedure/ function의 parameter들에 대한 정의는 DEFINITION_SCHEMA나 INFORMATION_SCHEMA의 PARAMETERS 테이블에서 확인할 수 있다.   
공개되지 않은 procedure/ function은 MODULE_BODY 테이블에서 확인할 수 있다.   
Package 내의 procedure/ function 변수가 참조하는 object들의 정보가 일시적으로 불완전해졌을 경우, &lt;alter package&gt; 구문으로 recompile을 시도해 볼 수 있다.

<a id="379f432eecfb59e4"></a>
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

<a id="850d1191a10cd7c4"></a>
### 호환성

SQL 표준에서는 CREATE MODULE 구문이다.

<a id="ca4df35f2530b30a"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE BODY](#be7bb0a00a34c743)
- [DROP PACKAGE](#6d701903dec1e955)
- [ALTER PACKAGE](#d832fc93cc42dd95)

<a id="be7bb0a00a34c743"></a>
## CREATE PACKAGE BODY

<a id="98d1ca38bcc4e8b9"></a>
### 기능

Package 내에서 사용될 procedure/ function/ 커서들에 대한 정의를 생성한다.

<a id="3945e3e13ed13c09"></a>
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

<a id="e931edb751ef8cf5"></a>
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

<a id="988979d5c33ccc01"></a>
### 구문 규칙 및 파라미터

<a id="658e12d92c387fd5"></a>
#### OR REPLACE

Package body가 이미 존재할 경우, 기존의 package body definition을 대체한다.

<a id="cc483e656d32de7e"></a>
#### PACKAGE NAME

생성할 package body의 이름이며, package spec 생성에 사용된 동일한 이름을 사용해야 한다. schema 내에서 유일한 이름이어야 한다.   
schema_name.package_name 과 같이 package가 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
Package 이름의 길이는 128 바이트보다 작아야 한다.

<a id="fa57a91378d7fb40"></a>
#### Item Declaration

Package body 내에서 사용할 PSM identifier들 (변수, type, 커서, function spec, procedure spec, exception 등)을 선언한다.   
Package spec 내에 선언된 routine들은 반드시 package body에서 정의되어야 한다.   
Package spec 내에서 SQL 없이 선언만 된 커서들은 반드시 package body에 정의되어야 한다.   
또한 package 내의 function, procedure, 커서의 argument 및 반환 타입들은 body 구문 내에 정의된 것과 일치해야 한다.

<a id="aef28247877fde0f"></a>
#### Initialization Part

Package instance 생성 과정에서 내부 변수등의 초기화를 위해 한 번만 수행되는 구문들을 기술한다.

<a id="c61d54129b90e116"></a>
### 설명

Schema-level package body를 생성한다.   
생성된 package body의 모든 private item은 다른 procedure/ function/ package/ anonymous block 들에 의해 참조될 수 없고 해당 package body 내에서만 사용된다.

Package body의 생성 정보는 DEFINITION_SCHEMA나 INFORMATION_SCHEMA의 MODULE_BODY 테이블에서 확인할 수 있다.   
Package body 내의 각 private item들의 목록은 DEFINITION_SCHEMA나 INFORMATION_SCHEMA에서 확인할 수 없다.   
Package 내의 procedure/ function/ 변수가 참조하는 object들의 정보가 일시적으로 불완전해졌을 경우, &lt;alter package body&gt; 구문으로 recompile을 시도해 볼 수 있다.

생성된 package body는 &lt;drop package&gt;나 &lt;drop package body&gt; 구문으로 삭제할 수 있다.

<a id="c6b14527831804b1"></a>
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

<a id="c1fa54853d5c36f3"></a>
### 호환성

SQL 표준에는 정의되어 있지 않다.

<a id="6e773bf0325814bc"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE](#6aabbd4af8bb049b)
- [DROP PACKAGE](#6d701903dec1e955)
- [ALTER PACKAGE](#d832fc93cc42dd95)

<a id="e2d083dd25c36aa9"></a>
## CREATE PROCEDURE

<a id="246f7c459c3c2cd3"></a>
### 기능

Schema-level procedure를 정의한다.

<a id="72568addae449830"></a>
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

<a id="1eede24452683d41"></a>
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

<a id="b3d07fac4d7a54f9"></a>
### 구문 규칙 및 파라미터

<a id="fb328cc7d7d81b98"></a>
#### [ OR REPLACE ]

이미 procedure가 존재할 경우, 기존의 procedure를 대체한다.

<a id="3a121e5c5d5b877d"></a>
#### PROC NAME

생성할 procedure의 이름으로써 스키마 내에서 고유한 이름이어야 한다.  
schema_name.proc_name과 같이 procedure가 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
Procedure 이름의 길이는 128 바이트보다 작아야 한다.

<a id="4621839e33487109"></a>
#### PARAM NAME

Procedure가 사용할 인자의 이름을 정의한다.   
각 인자의 이름은 procedure 내에서 고유한 이름이어야 한다.   
각 인자 이름의 길이는 128 바이트보다 작아야 한다.   
하나의 procedure에 사용할 수 있는 인자의 최대 개수에는 제한이 없다.

<a id="053e2b5145d1082d"></a>
#### Bind Type

각 인자의 bind type을 설정한다.   
표기하지 않을 경우 기본 타입은 IN이다.

<a id="c9e9b459c987ed17"></a>
#### proc_characteristics

Procedure 수행 옵션을 정의한다. 같은 항목에 대해서는 한 번만 기술해야 한다.

- AUTHID CURRENT_USER: Procedure를 실행하는 중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되고 수행된다.
- AUTHID DEFINER: Procedure를 실행하는 중에 수행되는 SQL들은 definer의 authorization에 따라 해석되고 수행된다.

<a id="cfa3ee119c06cc2c"></a>
#### item declaration

프로시져 내부에서 사용될 로컬 변수등의 item을 선언한다.  
PL block에서 선언될 수 있는 모든 item들을 선언할 수 있다.

<a id="c99789a11f45f568"></a>
#### PL Stmt List

Procedure의 body 부분으로써 수행할 PL statement들을 나열한다.   
Procedure의 내부에서는 '?'나 ':V1'과 같은 bind parameter를 사용할 수 없다.

<a id="1e2660308d1d8de6"></a>
### 설명

Schema-level SQL procedure를 정의한다. 생성된 procedure는 CALL 구문, anonymous block, 또는 다른 procedure/ function에서 호출될 수 있다.

Procedure의 정의는 INFORMATION_SCHEMA의 ROUTINES 테이블에서 확인할 수 있다.   
Procedure의 parameter들에 대한 정의는 INFORMATION_SCHEMA의 PARAMETERS 테이블에서 확인할 수 있다.

관련 객체들이 존재하지 않아 procedure가 일시적으로 불완전해졌을 경우, &lt;alter procedure&gt; 구문으로 plan을 다시 생성하려 시도해볼 수 있다.

생성된 procedure는 &lt;drop procedure&gt; 구문을 사용하여 제거할 수 있다.  
Procedure의 최대 생성 개수에는 제한이 없으므로 저장 공간에 문제가 없는 한 계속 생성할 수 있다.

<a id="87808b28a5f75c49"></a>
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

<a id="554f60f6f165ac46"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="71aa94d010ae9672"></a>
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

<a id="3aa991e2dd01475c"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [DROP PROCEDURE](#d133d98fe19742b0)
- [ALTER PROCEDURE](#7ae8df29fbc9e0ae)

<a id="399ca1e28092268f"></a>
## DROP FUNCTION

<a id="ce7d77b2348d5349"></a>
### 기능

Function을 제거한다.

<a id="54c06954e7612867"></a>
### 구문

```
<drop function statement> ::=
    DROP FUNCTION [ IF EXISTS ] func_name
    ;
```

<a id="33bbf92bdde690f3"></a>
### 사용 범위 및 접근 권한

&lt;drop function statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 function의 소유자
- Function이 속한 스키마에 대해 (DROP PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY PROCEDURE ON DATABASE

<a id="c53ec5023c3dfdd8"></a>
### 구문 규칙 및 파라미터

<a id="34eec3366e3ba661"></a>
#### IF EXISTS

Function이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="0d312db15e9fe5be"></a>
#### FUNC NAME

제거할 function의 이름이다.   
schema_name.func_name과 같이 function이 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="c6e316ce7bec23d1"></a>
### 설명

지정된 schema-level function을 제거한다.

<a id="6458c73be7630f7b"></a>
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

<a id="f8f5fa5da2692847"></a>
### 호환성

SQL 표준은 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="3634e9c6b4b14060"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="3f31cd4ebdd0b34a"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE FUNCTION](#243dff1382985279)
- [ALTER FUNCTION](#44ac55a48dad006a)

<a id="6d701903dec1e955"></a>
## DROP PACKAGE

<a id="b459b8a6665bbcbe"></a>
### 기능

Package (body만 또는 spec/ body 모두)를 제거한다.

<a id="837187ba007c057c"></a>
### 구문

```
<drop package statement> ::=
    DROP PACKAGE [BODY] [ IF EXISTS ] package_name
    ;
```

<a id="44db8bf0d727cdf4"></a>
### 사용 범위 및 접근 권한

&lt;drop package statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 package의 소유자 
- Package가 속한 스키마에 대해 (DROP PACKAGE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY PACKAGE ON DATABASE

<a id="4245f4bfd1a83225"></a>
### 구문 규칙 및 파라미터

<a id="a3d412616dc05f76"></a>
#### BODY

주어진 이름을 가진 package의 body 객체만 제거한다. *BODY* 라는 키워드를 명시하지 않은 경우 package specification과 body를 모두 삭제한다.

<a id="e7ca65ba8162b7a3"></a>
#### IF EXISTS

Package가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="dee34a44c1854b90"></a>
#### PACKAGE NAME

제거할 package의 이름이다.   
schema_name.package_name 과 같이 package가 소속한 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="e3cc6bec26fa2797"></a>
### 설명

지정된 package object를 제거한다.

<a id="1ff5841486e113ba"></a>
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

<a id="fafdfa0d0bc0dddf"></a>
### 호환성

SQL 표준에서는 DRO MODULE 구문이다.

<a id="12d2ddde9da0b454"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE](#6aabbd4af8bb049b)
- [CREATE PACKAGE BODY](#be7bb0a00a34c743)
- [ALTER PACKAGE](#d832fc93cc42dd95)

<a id="d133d98fe19742b0"></a>
## DROP PROCEDURE

<a id="c15ad011bb105dfc"></a>
### 기능

Procedure를 제거한다.

<a id="290114d74b69b145"></a>
### 구문

```
<drop procedure statement> ::=
    DROP PROCEDURE [ IF EXISTS ] proc_name
    ;
```

<a id="b72ee7065680bedb"></a>
### 사용 범위 및 접근 권한

&lt;drop procedure statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 procedure의 소유자
- Procedure가 속한 스키마에 대해 (DROP PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY PROCEDURE ON DATABASE

<a id="7282d368f84aa426"></a>
### 구문 규칙 및 파라미터

<a id="f3d63094b78da848"></a>
#### IF EXISTS

Procedure가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="8c8f799120b2cb6d"></a>
#### PROC NAME

제거할 procedure의 이름이다.   
schema_name.proc_name과 같이 procedure가 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="8d42cda594436a7e"></a>
### 설명

지정된 schema-level procedure를 제거한다.

<a id="a7052409a438b0d3"></a>
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

<a id="1bae465f12fcd4cf"></a>
### 호환성

SQL 표준은 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="6698d22de8f6ddd0"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="f79fd5cddda10836"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PROCEDURE](#e2d083dd25c36aa9)
- [ALTER PROCEDURE](#7ae8df29fbc9e0ae)

---

[← 26. PSM Language Element References](26-psm-language-element-references.md) · [전체 목차](../README.md) · [28. Database Connection →](../part-05-developer-manual/28-database-connection.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
