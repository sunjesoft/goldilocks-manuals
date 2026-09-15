<a id="2620aace3f721d2c"></a>

# 25. Using PSM Subprograms

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/2620aace3f721d2c)  
> 태그: `26c.1_0_tag`

[← 24. PSM Cursor Statements](24-psm-cursor-statements.md) · [전체 목차](../README.md) · [26. Using SQLs in PSM →](26-using-sqls-in-psm.md)

<a id="44acdc467f14d65d"></a>
## Anonymous PL Block

Anonymous PL block은 PSM 구문을 database에 저장하지 않고 일회성으로 실행하기 위한 SQL 구문이다. GOLDILOCKS에서 제공하는 정규 SQL 중 하나이기 때문에, GOLDILOCKS에서 제공하는 ODBC, JDBC 또는 precompiler에서도 다른 SQL과 동일하게 사용할 수 있다. 문법은 일반 basic block 구문과 동일하다.  
자세한 내용은 [Block (BEGIN .. END)](30-psm-language-element-references.md#b5f1979bc247ce01)을 참조한다.

```
<<Label>> ❶ (optional)
DECLARE   ❷ (optional)
❸ declare items (variables, cursors, types, ...) (optional)
BEGIN     ❹ (required)
❺ PSM statements to execute (required)
EXCEPTION ❻ Exception Handling Part (optional)
END;
```

Anonymous PL block을 사용할 때는 다음과 같은 점에 유의해야 한다.

<a id="d54799919090d2da"></a>
| Interface | 사용 시 주의사항 |
| --- | --- |
| 공통 | Schema-level procedure나 함수와 달리 bind parameter를 사용할 수 있다. Prepare-execute 방식도 지원한다. |
| ODBC | 일반 SQL과 완전히 동일하게 사용된다. |
| JDBC | IN-OUT이나 OUT 속성의 bind parameter를 가진 경우에는 [CallableStatement](../part-05-developer-manual/35-jdbc.md#3a2a3e4056d23255) 클래스를 사용해야 한다. |
| precompiler (gpec) | 특별한 유의사항이 없다. |
| Interactive Command Tool (gsql) | Anonymous PL block을 입력한 후에 '/'&lt;Enter&gt; 를 입력하여 구문의 종료를 알려야 한다. |

<a id="b412820c5cde3f17"></a>
## Nested Procedure

Nested procedure는 특정 PL block 내부에 선언된 procedure 타입의 subprogram이다. Nested procedure는 선언된 PL block과 그 하위에서만 참조 가능한 scope를 가진다.   
자세한 내용은 [Procedure Declaration and Definition](30-psm-language-element-references.md#b5a477999d1596c4)을 참조한다.

Nested procedure는 &lt;SQL body&gt; 또는 &lt;external body&gt;로 선언 가능하다.  
&lt;SQL body&gt;는 PL Item을 선언하고, 이를 참조할 수 있는 &lt;pl statement&gt;를 선언할 수 있다.  
&lt;external body&gt;는 external routine을 실행하기 위한 정보를 명시하고, external routine을 실행할 수 있다.

```
DECLARE
  PROCEDURE PROC1( A1 INTEGER )  ❶ Define nested procedure
  IS
    VAR1 INTEGER;                ❷ <SQL Body>
  BEGIN                        
    VAR1 := A1;
    DBMS_OUTPUT.PUT_LINE( 'VAR1 = ' || VAR1 );
  END; 
BEGIN
  PROC1( 100 );                  ❸ Call nested procedure
END;
/
```

```
DECLARE
  var1 NATIVE_INTEGER;
   
  PROCEDURE proc1( p1 NATIVE_INTEGER,             ❶ Define nested procedure
                   p2 NATIVE_INTEGER,
                   p3 OUT NATIVE_INTEGER ) AS
  LANGUAGE C                                      ❷ <external body>
  LIBRARY lib NAME "add"
  PARAMETERS( p1 INT , 
              p2 INT , 
              p3 INT );
BEGIN
  proc1( 5 , 3 , var1 );                          ❸ Call nested procedure
  DBMS_OUTPUT.PUT_LINE ( var1 );
END;
/
```

Nested subprogram의 &lt;SQL body&gt; 내부에서 사용 가능한 item들은 다음과 같다.

- Nested subprogram의 인자 (argument) 변수
- Nested subprogram이 정의된 PL block과 그 상위 scope에 정의된 변수와 각종 item들 (type, cursor,...)
- Anonymous PL block의 경우에는 bind parameter (예: '?', ':V1' 등)

&lt;external body&gt;인 nested procedure는 external routine을 호출할 수 있다.

```
#include <stdio.h>

void add( int a , int b , int * c)
{
    *c = a + b;
}
```

```
gSQL>
create library lib as 'add.so';
/

Library created.

gSQL>
DECLARE
  var1 NATIVE_INTEGER;
   
  PROCEDURE proc1( p1 NATIVE_INTEGER, 
                   p2 NATIVE_INTEGER,
                   p3 OUT NATIVE_INTEGER ) AS
  LANGUAGE C
  LIBRARY lib NAME "add"
  PARAMETERS( p1 INT , 
              p2 INT , 
              p3 INT );
BEGIN
  proc1( 5 , 3 , var1 );
  DBMS_OUTPUT.PUT_LINE ( var1 );
END;
/

8
Anonymous PL block executed.
```

Nested procedure는 forward declaration을 지원하기 때문에 declare와 define 구문을 따로 기술할 수 있다.

다음은 declare와 define 구문을 따로 기술하여 두 개의 nested procedure 사이에 상호 호출할 수 있는 로직을 구현한 예이다.

```
gSQL>
DECLARE
  PROCEDURE PROC1( A1 INTEGER );  ❶ declare proc1

  PROCEDURE PROC2( A1 INTEGER )   ❷ define  proc2
  IS
  BEGIN
    IF A1 > 0 THEN
      DBMS_OUTPUT.PUT_LINE( '(proc2)A1 = ' || A1 );
      PROC1( A1 -1 );  ❸ call proc1
    END IF;
  END; 

  PROCEDURE PROC1( A1 INTEGER )   ❹ define  proc1
  IS
  BEGIN
    IF A1 > 0 THEN
      DBMS_OUTPUT.PUT_LINE( '(proc1)A1 = ' || A1 );
      PROC2( A1 -1 );  ❺ call proc2
    END IF;
  END; 
BEGIN
  PROC1(5);  ❻ call proc1
END;
/
 
(proc1)A1 = 5
(proc2)A1 = 4
(proc1)A1 = 3
(proc2)A1 = 2
(proc1)A1 = 1

Anonymous PL block executed.
```

GOLDILOCKS PSM은 무한대의 상호참조를 방지하기 위해 최대 child statement depth를 50 개로 제한하고 있다. 이를 초과하면 다음과 같은 오류가 발생한다. (Nested function, schema-level procedure/ function에 동일하게 적용된다.)

```
gSQL> DECLARE
  PROCEDURE PROC1( A1 INTEGER );  ❶ declare proc1
  PROCEDURE PROC2( A1 INTEGER )   ❷ define  proc2
  IS
  BEGIN
    DBMS_OUTPUT.PUT_LINE( 'A1 = ' || A1 );
    PROC1( A1 -1 );
  END;
  PROCEDURE PROC1( A1 INTEGER )   ❸ define  proc1
  IS
  BEGIN
    DBMS_OUTPUT.PUT_LINE( 'A1 = ' || A1 );
    PROC2( A1 -1 );
  END;
BEGIN
  PROC1(100);
END;
/

ERR-42000(16411): maximum number of recursive SQL levels (50) exceeded.
```

다음은 declare와 define 구문을 따로 기술하여 &lt;external body&gt; nested procedure를 &lt;SQL body&gt; nested procedure에서 호출하는 로직을 구현한 예이다.

```
gSQL>
DECLARE
  PROCEDURE proc1( p1 NATIVE_INTEGER,
                   p2 NATIVE_INTEGER,
                   p3 OUT NATIVE_INTEGER );          ❶ declare proc1
 
  PROCEDURE proc2( p1 NATIVE_INTEGER ) AS            ❷ define  proc2
    var1 NATIVE_INTEGER;
  BEGIN
    PROC1( p1 , p1 - 1 , var1 );                     ❸ call proc1
    DBMS_OUTPUT.PUT_LINE( 'proc2 :: p1 = ' || p1 ||
                          ' , var1 = ' || var1 );
  END; 
       
  PROCEDURE proc1( p1 NATIVE_INTEGER,                ❹ define  proc1
                   p2 NATIVE_INTEGER,
                   p3 OUT NATIVE_INTEGER ) AS
  LANGUAGE C
  LIBRARY lib NAME "add"
  PARAMETERS( p1 INT , 
              p2 INT , 
              p3 INT );
BEGIN
  PROC2(5);                                          ❺ call proc2
END;
/

proc2 :: p1 = 5 , var1 = 9
Anonymous PL block executed.
```

<a id="56834962b8512d67"></a>
## Nested Function

Nested function은 nested procedure와 동일하지만 함수 형태를 가지는 subprogram이다.  
자세한 내용은 [Function Declaration and Definition](30-psm-language-element-references.md#2a34bffbc503ec12)을 참조한다.

- &lt;SQL body&gt;인 nested function

```
gSQL> 
DECLARE
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

- &lt;external body&gt;인 nested function

```
#include <stdio.h>

int add( int a , int b )
{
    return a + b;
}
```

```
gSQL>
create library lib as 'add.so';
/

Library created.

gSQL>
DECLARE
  var1 NATIVE_INTEGER;
   
  FUNCTION func1( p1 NATIVE_INTEGER,
                  p2 NATIVE_INTEGER )
    RETURN NATIVE_INTEGER AS
  LANGUAGE C
  LIBRARY lib NAME "add"
  PARAMETERS( p1 INT , 
              p2 INT , 
              RETURN INT );
BEGIN
  var1 := func1( 2 , 8 );
  DBMS_OUTPUT.PUT_LINE ( var1 );
END;
/

10
Anonymous PL block executed.
```

Nested function은 visible scope 내에 있는 모든 PSM expression에서 사용할 수 있지만, SQL 구문 안에서는 사용할 수 없다.

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
  SELECT FUNC1(10) INTO V1 FROM DUAL;
  DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (10:3): ERR-HY000(17079): a nested function not allowed in executing SQL
```

<a id="ad20c43fbf64d578"></a>
## Schema-level Procedure

Schema-level subprogram은 database에 저장되는 이름을 가진 SQL 객체이다. Schema-level procedure는 procedure 형태의 schema-level subprogram이다.

<a id="c919ca2bd26b5ad8"></a>
### 생성

Schema-level procedure는 다음과 같이 생성된다. 필요할 경우, 인자들의 타입에 precision과 scale 값을 명시해야 한다.   
Schema-level procedure의 &lt;routine body&gt;의 형식은 &lt;SQL body&gt; 또는 &lt;external body&gt;이다.  
자세한 내용은 [CREATE PROCEDURE](31-psm-sql-references.md#48b6178f1f6cd4cb)를 참조한다.

- &lt;SQL body&gt;인 schema-level procedure

```
gSQL>
CREATE OR REPLACE PROCEDURE sqlbody_proc( a1 INTEGER, a2 INTEGER )
IS  
  v1 INTEGER;
BEGIN
  SELECT COUNT(*)
    INTO v1
    FROM t1
    WHERE t1.i1 >= a1 AND t1.i1 <= a2; 

  DBMS_OUTPUT.PUT_LINE( 'v1 = ' || v1 );
END;
/

Procedure created.
```

- &lt;external body&gt;인 schema-level procedure

```
gSQL>
CREATE OR REPLACE PROCEDURE externalbody_proc( p1 NATIVE_INTEGER,
                                               p2 NATIVE_INTEGER,
                                               p3 OUT NATIVE_INTEGER ) AS
LANGUAGE C
LIBRARY lib NAME "add"
PARAMETERS( p1 INT , 
            p2 INT , 
            p3 INT );
/

Procedure created.
```

생성된 schema-level procedure에 대한 정보는 INFORMATION_SCHEMA.ROUTINES 테이블로 확인할 수 있다.  
자세한 내용은 [ROUTINES](../part-02-administration-manual/9-database-information.md#78ef3c3234db2c9b)를 참조한다.

```
gSQL>
SELECT specific_name,
       routine_body,
       routine_definition
  FROM information_schema.routines
 WHERE specific_name IN ( 'SQLBODY_PROC' , 'EXTERNALBODY_PROC' );

SPECIFIC_NAME     ROUTINE_BODY
----------------- ------------
ROUTINE_DEFINITION                                                       
-------------------------------------------------------------------------
EXTERNALBODY_PROC EXTERNAL    
PROCEDURE "PUBLIC"."EXTERNALBODY_PROC" ( p1 NATIVE_INTEGER,              
                                               p2 NATIVE_INTEGER,        
                                               p3 OUT NATIVE_INTEGER ) AS
LANGUAGE C                                                               
LIBRARY lib NAME "add"                                                   
PARAMETERS( p1 INT ,                                                     
            p2 INT ,                                                     
            p3 INT );                                                    
                                                                         
SQLBODY_PROC      SQL         
PROCEDURE "PUBLIC"."SQLBODY_PROC" ( a1 INTEGER, a2 INTEGER )             
IS                                                                       
  v1 INTEGER;                                                            
BEGIN                                                                    
  SELECT COUNT(*)                                                        
    INTO v1                                                              
    FROM t1                                                              
    WHERE t1.i1 >= a1 AND t1.i1 <= a2;                                   
                                                                         
  DBMS_OUTPUT.PUT_LINE( 'v1 = ' || v1 );                                 
END;                                                                     
                                                                         

2 rows selected.
```

INFORMATION_SCHEMA.ROUTINES 테이블에서 external routine에 관련된 정보를 확인할 수 있다.

```
gSQL> 
SELECT specific_name,
       external_name,
       external_c_function,
       external_language,
       library_schema,
       library_name
  FROM information_schema.routines
 WHERE specific_name = 'EXTERNALBODY_PROC';

SPECIFIC_NAME     EXTERNAL_NAME EXTERNAL_C_FUNCTION                   
----------------- ------------- --------------------------------------
EXTERNAL_LANGUAGE LIBRARY_SCHEMA LIBRARY_NAME
----------------- -------------- ------------
EXTERNALBODY_PROC add           void add( int P1 , int P2 , int * P3 )
C                 PUBLIC         LIB         

1 row selected.
```

인자 (argument)에 대한 정보는 INFORMATION_SCHEMA.PARAMETERS 테이블로 확인할 수 있다.  
자세한 내용은 [PARAMETERS](../part-02-administration-manual/9-database-information.md#998fdaedd0d0e2dd)를 참조한다.

```
gSQL> 
SELECT r.specific_name,
       p.parameter_name,
       p.ordinal_position
  FROM information_schema.routines r,
       information_schema.parameters p
 WHERE r.specific_name IN ( 'SQLBODY_PROC' , 'EXTERNALBODY_PROC' )
   AND r.specific_schema = p.specific_schema
   AND r.specific_name = p.specific_name
 ORDER BY p.parameter_name,
          p.ordinal_position;

SPECIFIC_NAME     PARAMETER_NAME ORDINAL_POSITION
----------------- -------------- ----------------
SQLBODY_PROC      A1                            1
SQLBODY_PROC      A2                            2
EXTERNALBODY_PROC P1                            1
EXTERNALBODY_PROC P2                            2
EXTERNALBODY_PROC P3                            3

5 rows selected.
```

<a id="fbd4903a9efabe3f"></a>
### 사용

Schema-level procedure는 다른 PSM의 내부 구문이나 CALL 구문에 의해 사용된다.  
다른 PSM 구문은 nested procedure와 같은 형식으로 schema-level procedure를 호출한다.

```
gSQL>
BEGIN
  sqlbody_proc( 2 , 4 );     ❶ call schema-level procedure with <SQL body>
END;
/

v1 = 3
Anonymous PL block executed.
```

```
gSQL>
DECLARE
  var1 NATIVE_INTEGER;
BEGIN
  externalbody_proc( 2 , 4 , var1 ); 
                        ❶ call schema-level procedure with <external body>
  DBMS_OUTPUT.PUT_LINE( 'var1 = ' || var1 );
END;
/

var1 = 6
Anonymous PL block executed.
```

주어진 PSM을 실행하는 SQL인 CALL 구문은 다음과 같이 실행된다.  
자세한 내용은 [CALL Statement](31-psm-sql-references.md#0b77efd04b5af863)를 참조한다.

```
gSQL> CALL sqlbody_proc( 2, 4 );
V1 = 3

Procedure Call complete.
```

```
gSQL> \var a NATIVE_INTEGER

gSQL> CALL externalbody_proc( 2, 4 , :a );

Procedure Call complete.

gSQL> \print a

A
-
6
```

ODBC나 JDBC에서 사용하는 procedure call escape sequence를 지원하기 위해 procedure에 대한 다음 구문을 지원한다.

```
{ CALL procedure_name( param1, param2, ... ) }
```

Procedure call escape sequence 구문은 일반 SQL처럼 사용할 수 있다.

```
gSQL> { CALL sqlbody_proc(2, 4) };
V1 = 3

Procedure Call complete.
```

```
gSQL> \var a NATIVE_INTEGER

gSQL> { CALL externalbody_proc( 2 , 4 , :a ) };

Procedure Call complete.

gSQL> \print a

A
-
6
```

GOLDILOCKS의 interactive command tool인 gsql은 tool 자체 명령어인 `\`EXEC를 통한 procedure 수행을 지원하지 않는다.

Schema-level procedure는 실행 시 권한에 대한 다음 옵션을 명시할 수 있다. Definer가 아닌 사용자가 이 옵션들에 따라 PSM내의 SQL을 수행하면 해당 사용자의 schema-path 정의에 따라 서로 다른 schema의 이름이 같은 테이블을 참조할 수도 있다. (Item을 선언할 때 사용된 객체명 (예: T1%ROWTYPE)은 항상 definer로 해석된다.)

- AUTHID DEFINER (default): 해당 procedure를 작성한 사용자로 변경된 후 수행된다.
- AUTHID CURRENT_USER: 수행하는 사용자를 변경하지 않고 현재 사용자에 의해 수행된다.

```
CREATE OR REPLACE PROCEDURE "PROC1"( A1 INTEGER, A2 INTEGER )
AUTHID CURRENT_USER
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
```

<a id="ac537851cfe67908"></a>
### 제거

Schema-level procedure는 다음 DROP PROCEDURE 구문으로 제거한다.  
자세한 내용은 [DROP PROCEDURE](31-psm-sql-references.md#47bed13ab733e3a0)를 참조한다.

```
DROP PROCEDURE PROC1;
```

GOLDILOCKS의 다른 DROP 구문들처럼 IF EXISTS 구문도 지원한다.

```
DROP PROCEDURE IF EXISTS PROC1;
```

<a id="455ede7f9ff3fbb5"></a>
### Recompile

Schema-level subprogram 내부에서 참조된 객체가 변경되면 해당 subprogram도 영향을 받아 실행 플랜을 다시 생성해야 할 수도 있다.

<a id="1043b87f96f9a3d1"></a>
#### 인자 또는 &lt;SQL body&gt;의 선언부에서 참조된 객체

선언부의 각종 item을 정의하거나 인자 타입을 정의할 때 사용된 객체가 변경되면 procedure의 플랜이 자동으로 recompile 된다.

- %TYPE, %ROWTYPE에 사용된 객체
- Explicit cursor 정의 구문에 사용된 객체

객체가 변경된 후 처음으로 해당 procedure가 수행되면 다음 순서에 따라 자동으로 플랜을 다시 생성한다.

1. Plan cache로부터 해당 procedure의 플랜을 가져온다
2. 해당 플랜의 객체 리스트를 validation하는 중에 변경된 객체를 찾는다.
3. 현재 플랜을 discard 하고, dictionary에 저장된 procedure 정의 구문으로부터 새로운 플랜을 생성한다.
4. 새로 생성된 플랜을 plan cache에 등록한다.
5. 플랜을 실행한다.

<a id="76c914baf8df8983"></a>
#### &lt;SQL body&gt;의 &lt;pl statement&gt; 중 SQL에서 참조된 객체

Procedure의 플랜에는 body에 사용된 SQL의 플랜이 저장되지 않고 SQL text만 저장된 상태이다. Procedure를 실행할 때 해당 SQL 구문을 실시간으로 compile 하여 플랜을 생성한 후 수행한다. 따라서 body 내에서 사용된 SQL 객체는 procedure의 플랜 자체에 영향을 주지 않는다.

단, 객체가 변경되면 procedure의 기존 interface인 바인드 개수나 타입이 변경되거나 column이 삭제될 수 있으므로 procedure까지 적절하게 변경하지 않으면 실행할 때 오류가 발생할 수 있다.

<a id="8101418a5d08669f"></a>
#### &lt;external body&gt;에서 참조하는 library 객체

&lt;external body&gt;에서 참조하는 library 객체가 변경되면 procedure의 플랜이 자동으로 recompile 된다. 단 사용자가 external routine을 변경하더라도 procedure는 recompile 하지 않는다. 데이터베이스는 외부에서 호출되는 shared library가 변경되는 것을 자동으로 감지하지 못한다.

<a id="13e57b9ee3a45f86"></a>
## Schema-level Function

Schema-level function은 expression 내에서 사용되는 함수 형태의 schema-level subprogram이다.

<a id="03f7cd29f0050fda"></a>
### 생성

Schema-level function은 다음과 같이 생성된다. 필요할 경우, 인자들의 타입에 precision과 scale 값을 명시해야 한다.   
Schema-level function의 &lt;routine body&gt;의 형식은 &lt;SQL body&gt; 또는 &lt;external body&gt;이다.  
자세한 내용은 [CREATE FUNCTION](31-psm-sql-references.md#8f6d3c41338c889a)을 참조한다.

- &lt;SQL body&gt;인 schema-level function

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

- &lt;external body&gt;인 schema-level function

```
gSQL>
CREATE FUNCTION func1( p1 NATIVE_INTEGER,
                       p2 NATIVE_INTEGER )
  RETURN NATIVE_INTEGER AS
LANGUAGE C
LIBRARY lib NAME "add"
PARAMETERS( p1 INT , 
            p2 INT , 
            RETURN INT );

Function created.
```

생성된 schema-level function은 procedure와 마찬가지로 INFORMATION_SCHEMA.ROUTINES와 INFORMATION_SCHEMA.PARAMETERS 테이블에서 확인할 수 있다.

<a id="ff4ecda931149ead"></a>
### 사용

Schema-level function은 일반 SQL이나 PSM 내의 SQL 객체가 사용될 수 있는 모든 expression에서 사용할 수 있다.

```
gSQL> SELECT sqlbody_func( 2 , 4 ) FROM dual;

SQLBODY_FUNC( 2 , 4 )
---------------------
                    3

1 row selected.
```

```
gSQL> SELECT externalbody_func( 2 , 4 ) FROM dual;

EXTERNALBODY_FUNC( 2 , 4 )
--------------------------
                         6

1 row selected.
```

PSM 내에서도 다음과 같이 사용된다.

```
gSQL>
DECLARE
  v1 INTEGER;
BEGIN
  v1 := sqlbody_func( 2, 4 );
  DBMS_OUTPUT.PUT_LINE( 'v1 = ' || v1 );
END;
/

v1 = 3
Anonymous PL block executed.
```

```
gSQL>
DECLARE
  v1 NATIVE_INTEGER;
BEGIN
  v1 := externalbody_func( 2, 4 );
  DBMS_OUTPUT.PUT_LINE( 'v1 = ' || v1 );
END;
/

v1 = 6
Anonymous PL block executed.
```

다음과 같이 CALL 구문을 이용하여 수행할 수 있다.  

자세한 내용은 [CALL Statement](31-psm-sql-references.md#0b77efd04b5af863)를 참조한다.

```
gSQL> \var v1 INTEGER

gSQL> CALL sqlbody_func( 2 , 4 ) INTO :v1;

Procedure Call complete.

gSQL> \print v1

V1
--
 3
```

```
gSQL> \var v1 NATIVE_INTEGER

gSQL> CALL externalbody_func( 2 , 4 ) INTO :v1;

Procedure Call complete.

gSQL> \print v1

V1
--
 6
```

Schema-level procedure와 마찬가지로 procedure call escape sequence 구문도 지원한다.

```
{ ? = CALL function_name( param1, param2, ... ) }
```

```
gSQL> \var v1 INTEGER

gSQL> { :v1 = CALL sqlbody_func( 2 , 4 ) };

Procedure Call complete.

gSQL> \print v1

V1
--
 3
```

```
gSQL> \var v1 NATIVE_INTEGER

gSQL> { :v1 = CALL externalbody_func( 2 , 4 ) };

Procedure Call complete.

gSQL> \print v1

V1
--
 6
```

<a id="d670aeea553c5d6e"></a>
### 제거

Schema-level function은 다음 DROP FUNCTION 구문으로 제거한다.  
자세한 내용은 [DROP FUNCTION](31-psm-sql-references.md#799b77ea31fecf81)을 참조한다.

```
gSQL> DROP FUNCTION FUNC1;

Function dropped.
```

---

[← 24. PSM Cursor Statements](24-psm-cursor-statements.md) · [전체 목차](../README.md) · [26. Using SQLs in PSM →](26-using-sqls-in-psm.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
