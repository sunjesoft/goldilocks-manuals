<a id="0873a1beb9ce89e9"></a>

# 29. PSM SQL References

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/0873a1beb9ce89e9)  
> 태그: `21c.1_35_tag`

[← 28. PSM Language Element References](28-psm-language-element-references.md) · [전체 목차](../README.md) · [30. Database Connection →](../part-05-developer-manual/30-database-connection.md)

<a id="4a233e56b1d5a850"></a>
## ALTER FUNCTION

<a id="7fe6c0bfc30eb2eb"></a>
### 기능

Function을 recompile 한다.

<a id="96eb52c1051d22b9"></a>
### 구문

```
<alter function statement> ::=
    ALTER FUNCTION function_name COMPILE
    ;
```

<a id="cb4803ebd7d1a476"></a>
### 사용 범위 및 접근 권한

&lt;alter function statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 function의 소유자 
- Function이 속한 스키마에 대해 (ALTER PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY PROCEDURE ON DATABASE

<a id="fa3375c56b61ac5b"></a>
### 구문 규칙 및 파라미터

- Function name
    - Compile 할 function의 이름이다.
    - schema_name.func_name과 같이 function이 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="44bba7cecb507c47"></a>
### 설명

지정된 schema-level function을 recompile 한다.

<a id="650dd0026c11f6dd"></a>
### 사용 예

```
gSQL> ALTER FUNCTION FUNC1 COMPILE;

Function altered.
```

<a id="b0157c8562fc657a"></a>
### 호환성

SQL 표준에서는 CREATE를 수행할 때 지정된 characteristic들을 변경하는 구문이고, GOLDILOCKS에서는 function의 plan을 다시 생성하는 구문이다.

**SQL 표준 호환성**

<a id="261fcda235c9ffb3"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="19a36ab749429650"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE FUNCTION](#b61457de314b7c25)
- [DROP FUNCTION](#302ce45389b0c042)

<a id="79590a8bb98ab401"></a>
## ALTER PACKAGE

<a id="4e642cc7d602f1c0"></a>
### 기능

Package를 recompile 한다.

<a id="0fbfba2b75aab4cb"></a>
### 구문

```
<alter package statement> ::=
    ALTER PACKAGE package_name <package compile clause>
    ;

<package compile clause> ::=
    COMPILE [PACKAGE|SPECIFICATION|BODY]
```

<a id="db850234535dcb12"></a>
### 사용 범위 및 접근 권한

&lt;alter package statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 package의 소유자 
- Package가 속한 스키마에 대해 (ALTER PACKAGE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY PACKAGE ON DATABASE

<a id="af4e6a76654b3b51"></a>
### 구문 규칙 및 파라미터

- Package name
    - Compile 할 package의 이름이다.
    - schema_name.package_name과 같이 package가 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

- Package compile clause
    - PACKAGE: Specification과 body를 모두 recompile 한다. (Default)
    - SPECIFICATION: Specification만 recompile 한다.
    - BODY: Body만 recompile 한다.

<a id="c2950dc7d3d2dc70"></a>
### 설명

지정된 package를 recompile 한다.  
Compile 된 package의 실행 code는 plan cache에 저장된다.

<a id="21175f896d3e87b4"></a>
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

<a id="2a64843637fa18dc"></a>
### 호환성

SQL 표준에서는 ALTER MODULE 구문이다.

<a id="5e2de756cc80b773"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE](#0d9d8dee923fa8cc)
- [CREATE PACKAGE BODY](#4f6f51debfad92af)
- [DROP PACKAGE](#8bf46b82b6d20c86)

<a id="d57c066e0b07c711"></a>
## ALTER PROCEDURE

<a id="eece9df310291eb0"></a>
### 기능

Procedure를 recompile 한다.

<a id="bf7d3655f72dd7e5"></a>
### 구문

```
<alter procedure statement> ::=
    ALTER PROCEDURE proc_name COMPILE
    ;
```

<a id="2c6c04f4c813c0c9"></a>
### 사용 범위 및 접근 권한

&lt;alter procedure statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 procedure의 소유자 
- Procedure가 속한 스키마에 대해 (ALTER PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY PROCEDURE ON DATABASE

<a id="a6607864d6d069e8"></a>
### 구문 규칙 및 파라미터

- Proc name
    - Compile할 procedure의 이름이다. 
    - schema_name.proc_name과 같이 procedure가 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="43804a41d8bc67d9"></a>
### 설명

지정된 schema-level procedure를 recompile 한다.

<a id="be85997150e7f853"></a>
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

<a id="71a1ce7b5f481533"></a>
### 호환성

SQL 표준에서는 CREATE를 수행할 때 지정된 characteristic들을 변경하는 구문이고, GOLDILOCKS에서는 procedure의 plan을 다시 생성하는 구문이다.

**SQL 표준 호환성**

<a id="bc3ad58468199130"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="55206e0c69442b04"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PROCEDURE](#40ffb9d35e667f94)
- [DROP PROCEDURE](#ef39e4353f26ce85)

<a id="3b527e0c9c507e62"></a>
## CALL Statement

<a id="dfb6a382060e55cc"></a>
### 기능

Schema level procedure나 function을 수행한다.

<a id="7eb70e8855970dba"></a>
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

<a id="0c5c51217d8f338c"></a>
### 사용 범위 및 접근 권한

&lt;call statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다

- 해당 procedure에 대한 EXECUTE 권한
- Procedure가 속한 schema에 대해 (EXECUTE PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- EXECUTE ANY PROCEDURE ON DATABASE

<a id="45456d8ccb7bd273"></a>
### 구문 규칙 및 파라미터

- proc_name
    - 실행할 procedure/ function의 이름이다 
    - Schema_name.Proc_name과 같이 procedure가 속한 schema를 포함할 수 있다. 
- value_expr
    - Procedure에 전달할 인자값을 표현한다. '?' 나 ':V1'과 같은 bind parameter를 사용할 수도 있다.

<a id="8e8a7ba92f91335e"></a>
### 설명

명시된 인자들을 사용하여 schema level SQL procedure나 function을 실행한다.

&lt;sql call statement&gt; 형식 중에 function은 INTO 절 다음에 host variable 표현이나 dynamic bind parameter (?)를 사용하여 결과값을 반환한다.

&lt;odbc procedure call escape sequence&gt; 형식은 ODBC/ JDBC 등에서 PROCEDURE를 호출하기 위한   
표준 구문이며, GOLDILOCKS는 이 구문을 server에서 지원한다. (gsql 등의 tool에서도 사용 가능하다.)  
Function은 앞에 assign 표현( ? = )을 사용하여 결과값을 반환한다.

<a id="69af54107bf6cbd5"></a>
### 사용 예

<a id="f1bd9d6c45b1a0b1"></a>
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

<a id="19f4f8b0c0479535"></a>
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

<a id="b9d62f728e7554fb"></a>
### 호환성

SQL 표준에서는 PROCEDURE에 대한 호출만 가능하여 [INTO] 절 이하를 정의하지 않고 있다.

<a id="b61457de314b7c25"></a>
## CREATE FUNCTION

<a id="f79632dc86643339"></a>
### 기능

Schema level function을 정의한다.

<a id="87d79dbef7a0cdb0"></a>
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

<a id="98639f163e94f177"></a>
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

<a id="01719b6cc0ff2ff9"></a>
### 구문 규칙 및 파라미터

<a id="09195fc318c16b67"></a>
#### OR REPLACE

이미 function이 존재할 경우, 기존의 function을 대체한다.

<a id="0d46489ce81b2062"></a>
#### FUNCTION NAME

생성할 function의 이름으로써 스키마 내에서 고유한 이름이어야 한다.  
schema_name.func_name과 같이 function이 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
Function 이름의 길이는 128 바이트보다 작아야 한다.

<a id="d5b67eec99e2952f"></a>
#### PARAM NAME

Function이 사용할 인자의 이름을 정의한다.  
각 인자의 이름은 function 내에서 고유한 이름이어야 한다.  
각 인자 이름의 길이는 128 바이트보다 작아야 한다.  
하나의 function에 사용할 수 있는 인자의 최대 개수에는 제한이 없다.

<a id="6df132f0e2c93587"></a>
#### Bind Type

각 인자의 bind type을 설정한다.   
표기하지 않을 경우 기본 타입은 IN 이다.

<a id="70d3a90e12bc05d3"></a>
#### Func_Characteristics

Function 수행 옵션을 정의한다. 같은 항목에 대해서는 한 번만 기술해야 한다.

- DETERMINISTIC: 동일한 인자값들이 입력될 경우 해당 function은 항상 동일한 결과값을 반환한다.
- AUTHID CURRENT_USER: Function을 실행하는 중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되고 수행된다.
- AUTHID DEFINER: Function을 실행하는 중에 수행되는 SQL들은 definer의 authorization에 따라 해석되고 수행된다.

<a id="b637259828bddb77"></a>
#### Item Declaration

Function 내부에서 사용될 로컬 변수등의 item을 선언한다.   
PL block에서 선언될 수 있는 모든 item들을 선언할 수 있다.

<a id="f0fa504627e72033"></a>
#### PL Stmt List

Function의 body 부분으로써 수행할 PL statement들을 나열한다.   
Function의 내부에서는 '?'나 ':V1'과 같은 bind parameter를 사용할 수 없다.

<a id="b9e499298965afdc"></a>
### 설명

Schema-level SQL function을 정의한다. 생성된 function은 모든 expression에서 호출될 수 있다.

Function의 정의는 INFORMATION_SCHEMA의 ROUTINES 테이블에서 확인할 수 있다. Function의 parameter들에 대한 정의는 INFORMATION_SCHEMA의 PARAMETERS 테이블에서 확인할 수 있다.

관련 객체들이 존재하지 않아 function이 일시적으로 불완전해졌을 경우, &lt;alter function&gt; 구문으로 plan을 다시 생성하려 시도해볼 수 있다.

생성된 function은 &lt;drop function&gt; 구문을 사용하여 제거할 수 있다.  
Function의 최대 생성 개수에는 제한이 없으므로 저장 공간에 문제가 없는 한 계속 생성할 수 있다.

<a id="c7f48aa289c664ad"></a>
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

<a id="95d64061e722597f"></a>
### 호환성

SQL 표준에서는 OR REPLACE 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="66b278448550c570"></a>
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

<a id="a3c497312eb564ba"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [DROP FUNCTION](#302ce45389b0c042)
- [ALTER FUNCTION](#4a233e56b1d5a850)

<a id="0d9d8dee923fa8cc"></a>
## CREATE PACKAGE

<a id="8b4a2dcc4c60141b"></a>
### 기능

Package 내에서 사용될 public item들에 대한 spec을 정의한다.

<a id="0116af15cb5048f4"></a>
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

<a id="6e1990a7538defd8"></a>
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

<a id="d17adede361a7cff"></a>
### 구문 규칙 및 파라미터

<a id="7dd43c7c2600922e"></a>
#### OR REPLACE

이미 package가 존재할 경우, 기존의 package specification을 대체한다.

<a id="675929c2bbc0188f"></a>
#### PACKAGE NAME

생성할 package의 이름이며, schema 내에서 유일한 이름이어야 한다.   
schema_name.package_name과 같이 package가 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
Package 이름의 길이는 128 바이트보다 작아야 한다.

<a id="969d8f7f4f38f5df"></a>
#### Package Characteristics

Package를 수행하는 옵션을 정의한다. 같은 항목에 대해서는 한 번만 기술해야 한다.

- AUTHID CURRENT_USER: Package 내의 item들이 실행되는 도중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되어 수행된다. 
- AUTHID DEFINER: Package 내의 item들이 실행되는 도중에 수행되는 SQL들은 definer의 authorization에 따라 해석되어 수행된다.

<a id="31f7760556d755f0"></a>
#### Item Declaration

Package 외부에서 접근 가능한 public 변수, type, 커서, 커서 변수, function spec, procedure spec을 선언한다.   
Package 내의 function과 procedure는 반드시 create package body 구문을 통해 정의되어야 한다.   
Package 내에서 SQL 없이 선언만 된 커서는 반드시 create package body 구문을 통해 정의되어야 한다.   
또한 package 내의 function, procedure, 커서의 argument와 반환 타입들은 body 구문 내에 정의된 것과 일치해야 한다.

<a id="db50e776b0d60538"></a>
### 설명

Schema-level package specification을 생성한다.   
생성된 package의 모든 public item은 다른 procedure/ function/ package/ anonymous block 들에 의해 참조될 수 있다.

Package 생성 정보는 DEFINITION_SCHEMA나 INFORMATION_SCHEMA의 MODULES 테이블에서 확인할 수 있다.   
Package 내의 공개된 각 procedure/ function 목록은 DEFINITION_SCHEMA나 INFORMATION_SCHEMA 의 ROUTINES 테이블에서 확인할 수 있다.   
Package 내의 공개된 각 procedure/ function의 parameter들에 대한 정의는 DEFINITION_SCHEMA나 INFORMATION_SCHEMA의 PARAMETERS 테이블에서 확인할 수 있다.   
공개되지 않은 procedure/ function은 MODULE_BODY 테이블에서 확인할 수 있다.   
Package 내의 procedure/ function 변수가 참조하는 object들의 정보가 일시적으로 불완전해졌을 경우, &lt;alter package&gt; 구문으로 recompile을 시도해 볼 수 있다.

<a id="3349f3ec85b18518"></a>
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

<a id="c27609ca9505c4ee"></a>
### 호환성

SQL 표준에서는 CREATE MODULE 구문이다.

<a id="51d4c8e54ff59a3b"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE BODY](#4f6f51debfad92af)
- [DROP PACKAGE](#8bf46b82b6d20c86)
- [ALTER PACKAGE](#79590a8bb98ab401)

<a id="4f6f51debfad92af"></a>
## CREATE PACKAGE BODY

<a id="14fe54187c3dad08"></a>
### 기능

Package 내에서 사용될 procedure/ function/ 커서들에 대한 정의를 생성한다.

<a id="6f3ce3f8cbe3f00a"></a>
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

<a id="272bebca8cf3d377"></a>
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

<a id="6ea98e1903bc842b"></a>
### 구문 규칙 및 파라미터

<a id="3cd106370591d511"></a>
#### OR REPLACE

Package body가 이미 존재할 경우, 기존의 package body definition을 대체한다.

<a id="dfe020c6385b0a1d"></a>
#### PACKAGE NAME

생성할 package body의 이름이며, package spec 생성에 사용된 동일한 이름을 사용해야 한다. schema 내에서 유일한 이름이어야 한다.   
schema_name.package_name 과 같이 package가 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
Package 이름의 길이는 128 바이트보다 작아야 한다.

<a id="907cf770ea083799"></a>
#### Item Declaration

Package body 내에서 사용할 PSM identifier들 (변수, type, 커서, function spec, procedure spec, exception 등)을 선언한다.   
Package spec 내에 선언된 routine들은 반드시 package body에서 정의되어야 한다.   
Package spec 내에서 SQL 없이 선언만 된 커서들은 반드시 package body에 정의되어야 한다.   
또한 package 내의 function, procedure, 커서의 argument 및 반환 타입들은 body 구문 내에 정의된 것과 일치해야 한다.

<a id="9a49f7461182ef94"></a>
#### Initialization Part

Package instance 생성 과정에서 내부 변수등의 초기화를 위해 한 번만 수행되는 구문들을 기술한다.

<a id="4c4cce9a7fa5dc64"></a>
### 설명

Schema-level package body를 생성한다.   
생성된 package body의 모든 private item은 다른 procedure/ function/ package/ anonymous block 들에 의해 참조될 수 없고 해당 package body 내에서만 사용된다.

Package body의 생성 정보는 DEFINITION_SCHEMA나 INFORMATION_SCHEMA의 MODULE_BODY 테이블에서 확인할 수 있다.   
Package body 내의 각 private item들의 목록은 DEFINITION_SCHEMA나 INFORMATION_SCHEMA에서 확인할 수 없다.   
Package 내의 procedure/ function/ 변수가 참조하는 object들의 정보가 일시적으로 불완전해졌을 경우, &lt;alter package body&gt; 구문으로 recompile을 시도해 볼 수 있다.

생성된 package body는 &lt;drop package&gt;나 &lt;drop package body&gt; 구문으로 삭제할 수 있다.

<a id="4866412c8d24ce68"></a>
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

<a id="ca8e58b5acd01cbd"></a>
### 호환성

SQL 표준에는 정의되어 있지 않다.

<a id="76560f09ce995351"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE](#0d9d8dee923fa8cc)
- [DROP PACKAGE](#8bf46b82b6d20c86)
- [ALTER PACKAGE](#79590a8bb98ab401)

<a id="40ffb9d35e667f94"></a>
## CREATE PROCEDURE

<a id="0cdde1cf04fd14b2"></a>
### 기능

Schema-level procedure를 정의한다.

<a id="b6d2926a2b31ff3b"></a>
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

<a id="63a14fc1f45982f6"></a>
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

<a id="3aae1aba75a6f476"></a>
### 구문 규칙 및 파라미터

<a id="63c7af543f7e9360"></a>
#### [ OR REPLACE ]

이미 procedure가 존재할 경우, 기존의 procedure를 대체한다.

<a id="1dbbd9e0f469164f"></a>
#### PROC NAME

생성할 procedure의 이름으로써 스키마 내에서 고유한 이름이어야 한다.  
schema_name.proc_name과 같이 procedure가 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
Procedure 이름의 길이는 128 바이트보다 작아야 한다.

<a id="66090175ff28e007"></a>
#### PARAM NAME

Procedure가 사용할 인자의 이름을 정의한다.   
각 인자의 이름은 procedure 내에서 고유한 이름이어야 한다.   
각 인자 이름의 길이는 128 바이트보다 작아야 한다.   
하나의 procedure에 사용할 수 있는 인자의 최대 개수에는 제한이 없다.

<a id="3fcdff113d48974a"></a>
#### Bind Type

각 인자의 bind type을 설정한다.   
표기하지 않을 경우 기본 타입은 IN이다.

<a id="39df9d561983570a"></a>
#### proc_characteristics

Procedure 수행 옵션을 정의한다. 같은 항목에 대해서는 한 번만 기술해야 한다.

- AUTHID CURRENT_USER: Procedure를 실행하는 중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되고 수행된다.
- AUTHID DEFINER: Procedure를 실행하는 중에 수행되는 SQL들은 definer의 authorization에 따라 해석되고 수행된다.

<a id="a3280b08f2423710"></a>
#### item declaration

프로시져 내부에서 사용될 로컬 변수등의 item을 선언한다.  
PL block에서 선언될 수 있는 모든 item들을 선언할 수 있다.

<a id="fd7e1b9e80130046"></a>
#### PL Stmt List

Procedure의 body 부분으로써 수행할 PL statement들을 나열한다.   
Procedure의 내부에서는 '?'나 ':V1'과 같은 bind parameter를 사용할 수 없다.

<a id="3bc02e3bcd3759dd"></a>
### 설명

Schema-level SQL procedure를 정의한다. 생성된 procedure는 CALL 구문, anonymous block, 또는 다른 procedure/ function에서 호출될 수 있다.

Procedure의 정의는 INFORMATION_SCHEMA의 ROUTINES 테이블에서 확인할 수 있다.   
Procedure의 parameter들에 대한 정의는 INFORMATION_SCHEMA의 PARAMETERS 테이블에서 확인할 수 있다.

관련 객체들이 존재하지 않아 procedure가 일시적으로 불완전해졌을 경우, &lt;alter procedure&gt; 구문으로 plan을 다시 생성하려 시도해볼 수 있다.

생성된 procedure는 &lt;drop procedure&gt; 구문을 사용하여 제거할 수 있다.  
Procedure의 최대 생성 개수에는 제한이 없으므로 저장 공간에 문제가 없는 한 계속 생성할 수 있다.

<a id="6d914f5309cae183"></a>
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

<a id="065c08ed75e8d603"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="ac89dba098384c05"></a>
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

<a id="611e343ca3791b2d"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [DROP PROCEDURE](#ef39e4353f26ce85)
- [ALTER PROCEDURE](#d57c066e0b07c711)

<a id="302ce45389b0c042"></a>
## DROP FUNCTION

<a id="970f457c10caab69"></a>
### 기능

Function을 제거한다.

<a id="8e8aa0ee667f6c8d"></a>
### 구문

```
<drop function statement> ::=
    DROP FUNCTION [ IF EXISTS ] func_name
    ;
```

<a id="1de7199f3a408efc"></a>
### 사용 범위 및 접근 권한

&lt;drop function statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 function의 소유자
- Function이 속한 스키마에 대해 (DROP PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY PROCEDURE ON DATABASE

<a id="5b08aa897b7d9f59"></a>
### 구문 규칙 및 파라미터

<a id="0c56202ecde2dd64"></a>
#### IF EXISTS

Function이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="00ffa1ffe7dee3b1"></a>
#### FUNC NAME

제거할 function의 이름이다.   
schema_name.func_name과 같이 function이 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="b53d5b2ea481d9a5"></a>
### 설명

지정된 schema-level function을 제거한다.

<a id="3511d0887da3104c"></a>
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

<a id="6219abc947152fbf"></a>
### 호환성

SQL 표준은 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="9e6c1f123ca9ff88"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="acc80ac6ba2a6711"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE FUNCTION](#b61457de314b7c25)
- [ALTER FUNCTION](#4a233e56b1d5a850)

<a id="8bf46b82b6d20c86"></a>
## DROP PACKAGE

<a id="a2e40c4f83835f40"></a>
### 기능

Package (body만 또는 spec/ body 모두)를 제거한다.

<a id="e69953f3cc2d5816"></a>
### 구문

```
<drop package statement> ::=
    DROP PACKAGE [BODY] [ IF EXISTS ] package_name
    ;
```

<a id="436ce25a4a8158a0"></a>
### 사용 범위 및 접근 권한

&lt;drop package statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 package의 소유자 
- Package가 속한 스키마에 대해 (DROP PACKAGE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY PACKAGE ON DATABASE

<a id="365ccd0ab482c89d"></a>
### 구문 규칙 및 파라미터

<a id="0d60a55c3b16e717"></a>
#### BODY

주어진 이름을 가진 package의 body 객체만 제거한다. *BODY* 라는 키워드를 명시하지 않은 경우 package specification과 body를 모두 삭제한다.

<a id="b0408ebf39c8f333"></a>
#### IF EXISTS

Package가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="ff97abb2bd2f6bab"></a>
#### PACKAGE NAME

제거할 package의 이름이다.   
schema_name.package_name 과 같이 package가 소속한 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="efcf808ecaf26307"></a>
### 설명

지정된 package object를 제거한다.

<a id="1d4ae4eb54cdd181"></a>
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

<a id="834e988722bef338"></a>
### 호환성

SQL 표준에서는 DRO MODULE 구문이다.

<a id="23523debd8ea6396"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE](#0d9d8dee923fa8cc)
- [CREATE PACKAGE BODY](#4f6f51debfad92af)
- [ALTER PACKAGE](#79590a8bb98ab401)

<a id="ef39e4353f26ce85"></a>
## DROP PROCEDURE

<a id="2ca1d3ab6c7b437c"></a>
### 기능

Procedure를 제거한다.

<a id="5c79c66197b30a39"></a>
### 구문

```
<drop procedure statement> ::=
    DROP PROCEDURE [ IF EXISTS ] proc_name
    ;
```

<a id="99c6ca1c9c3cae20"></a>
### 사용 범위 및 접근 권한

&lt;drop procedure statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 procedure의 소유자
- Procedure가 속한 스키마에 대해 (DROP PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY PROCEDURE ON DATABASE

<a id="2729fc01e6ef6395"></a>
### 구문 규칙 및 파라미터

<a id="98ccdf382f8b5d3c"></a>
#### IF EXISTS

Procedure가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="588550edbd27660d"></a>
#### PROC NAME

제거할 procedure의 이름이다.   
schema_name.proc_name과 같이 procedure가 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="606678239f9bcc06"></a>
### 설명

지정된 schema-level procedure를 제거한다.

<a id="73cda249972763ed"></a>
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

<a id="d25955b4993f8c22"></a>
### 호환성

SQL 표준은 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="791ff131d33bc9c0"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="55180f470b048bee"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PROCEDURE](#40ffb9d35e667f94)
- [ALTER PROCEDURE](#d57c066e0b07c711)

---

[← 28. PSM Language Element References](28-psm-language-element-references.md) · [전체 목차](../README.md) · [30. Database Connection →](../part-05-developer-manual/30-database-connection.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
