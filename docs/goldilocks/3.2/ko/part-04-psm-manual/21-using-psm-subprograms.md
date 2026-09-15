<a id="bae13494e9e94331"></a>

# 21. Using PSM Subprograms

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/bae13494e9e94331)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 20. PSM Cursor Statements](20-psm-cursor-statements.md) · [전체 목차](../README.md) · [22. Using SQLs in PSM →](22-using-sqls-in-psm.md)

<a id="0f89567a6ca545a2"></a>
## Anonymous PL Block

Anonymous PL block은 PSM 구문을 database에 저장하지 않고 일회성으로 실행하기 위한 SQL 구문이다. GOLDILOCKS에서 제공하는 정규 SQL 중 하나이기 때문에, GOLDILOCKS에서 제공하는 ODBC, JDBC 혹은 precompiler에서도 다른 SQL과 동일하게 사용할 수 있다. 문법은 일반 basic block 구문과 동일하다.  
자세한 내용은 [Block (BEGIN .. END)](23-psm-language-element-references.md#b678ebcaaabaf1c3)를 참조한다.

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

<a id="140d8ff4e652defb"></a>
| Interface | 사용 시 주의사항 |
| --- | --- |
| 공통 | Schema-level procedure나 함수와 달리 bind parameter를 사용할 수 있다. Prepare-execute 방식도 지원한다. |
| ODBC | 일반 SQL과 완전히 동일하게 사용된다. |
| JDBC | IN-OUT이나 OUT 속성의 bind parameter를 가진 경우에는 [CallableStatement](../part-05-developer-manual/26-jdbc.md#9065b7c6bbdb2bf7) 클래스를 사용해야 한다. |
| precompiler (gpec) | 특별한 유의사항이 없다. |
| Interactive Command Tool (gsql) | Anonymous PL block을 입력한 후에 '/'&lt;Enter&gt; 를 입력하여 구문의 종료를 알려야 한다. |

<a id="80193f70a588e60a"></a>
## Nested Procedure

Nested procedure는 특정 PL block 내부에 선언된 procedure 타입의 subprogram이다. Nested procedure는 선언된 PL block과 그 하위에서만 참조 가능한 scope를 가진다.   
자세한 내용은 [Procedure Declaration and Definition](23-psm-language-element-references.md#7a92bd254850f3a4)을 참조한다.

```
DECLARE
  PROCEDURE PROC1( A1 INTEGER )  ❶ Define nested procedure
    IS   
    BEGIN
      DBMS_OUTPUT.PUT_LINE( 'A1 = ' || A1 );
    END; 
BEGIN
  PROC1( 100 );  ❷ Call nested procedure
END;
/
```

Nested subprogram 내부에서 사용 가능한 item들은 다음과 같다.

- Nested subprogram의 인자 (argument) 변수
- Nested subprogram이 정의된 PL block과 그 상위 scope에 정의된 변수와 각종 item들 (type, cursor,...)
- Anonymous PL block의 경우에는 bind parameter (예: '?', ':V1' 등)

Nested procedure는 forward declaration을 지원하기 때문에 declare와 define 구문을 따로 기술할 수 있다. 이를 이용하면 두 개의 nested procedure 사이에 상호 호출할 수 있는 로직을 구현할 수 있다.

```
gSQL> DECLARE

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

GOLDILOCKS PSM은 무한대의 상호참조를 방지하기 위해 최대 Child Statement Depth를 50개로 제한하고 있다. 이를 초과하면 다음과 같은 오류가 발생한다. (Nested function, schema-level procedure/ function 에 동일하게 적용된다.)

```
gSQL> DECLARE
  PROCEDURE PROC1( A1 INTEGER );  ❶ declare proc1
  PROCEDURE PROC2( A1 INTEGER )   ❷ define  proc2
  IS
  BEGIN
    DBMS_OUTPUT.PUT_LINE( 'A1 = ' || A1 );
    PROC1( A1 -1 );
  END;
  PROCEDURE PROC1( A1 INTEGER )  ❸ define  proc1
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

<a id="2009d1c740b1279c"></a>
## Nested Function

Nested function은 nested procedure와 동일하지만 함수 형태를 가지는 subprogram이다.  
자세한 내용은 [Function Declaration and Definition](23-psm-language-element-references.md#f103942d316b303b)을 참조한다.

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

<a id="b982b013dfaaf53b"></a>
## Schema-level Procedure

Schema-level subprogram은 database에 저장되는 이름을 가진 SQL 객체이다. Schema-level procedure는 procedure 형태의 schema-level subprogram이다.

<a id="945a23617c3d8ebe"></a>
### 생성

Schema-level procedure는 다음과 같이 생성된다. 필요할 경우, 인자들의 타입에 precision과 scale 값을 명시해야 한다.   
자세한 내용은 [CREATE PROCEDURE](24-psm-sql-references.md#58204d591b990498)를 참조한다.

```
CREATE OR REPLACE PROCEDURE PROC1( A1 INTEGER, A2 INTEGER )
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

생성된 schema-level procedure에 대한 정보는 INFORMATION_SCHEMA.ROUTINES 테이블로 확인할 수 있다.   
자세한 내용은 [ROUTINES](../part-02-administration-manual/9-database-information.md#f64133e59afa66f0)를 참조한다

```
gSQL> SELECT SPECIFIC_NAME, ROUTINE_DEFINITION
  FROM  INFORMATION_SCHEMA.ROUTINES
  WHERE SPECIFIC_NAME = 'PROC1';

SPECIFIC_NAME ROUTINE_DEFINITION                                   
------------- -----------------------------------------------------
PROC1         PROCEDURE "PUBLIC"."PROC1" ( A1 INTEGER, A2 INTEGER )
              IS                                                   
                V1 INTEGER;                                        
              BEGIN                                                
                SELECT COUNT(*)                                    
                  INTO V1                                          
                  FROM T1                                          
                  WHERE T1.I1 >= A1 AND T1.I1 <= A2;               
                DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );             
              END;                                                 
                                                                   

1 row selected.
```

인자 (argument)에 대한 정보는 INFORMATION_SCHEMA.PARAMETERS 테이블로 확인할 수 있다.  
자세한 내용은 [PARAMETERS](../part-02-administration-manual/9-database-information.md#a98b52f73aada557)를 참조한다.

```
gSQL> SELECT P.PARAMETER_NAME, P.ORDINAL_POSITION
  FROM  INFORMATION_SCHEMA.ROUTINES     R,
        INFORMATION_SCHEMA.PARAMETERS   P
  WHERE R.SPECIFIC_NAME = 'PROC1'
    AND R.SPECIFIC_SCHEMA = P.SPECIFIC_SCHEMA
    AND R.SPECIFIC_NAME = P.SPECIFIC_NAME
  ORDER BY P.ORDINAL_POSITION;

PARAMETER_NAME ORDINAL_POSITION
-------------- ----------------
A1                            1
A2                            2

2 rows selected.
```

<a id="447ecd053cc9878e"></a>
### 사용

Schema-level procedure는 다른 PSM의 내부 구문이나 CALL 구문에 의해 사용된다.  
다른 PSM 구문은 nested procedure와 같은 형식으로 schema-level procedure를 호출한다.

```
gSQL> BEGIN
  PROC1( 2, 4 ); ❶ call schema-level procedure
END;
/

V1 = 3

Anonymous PL block executed.
```

주어진 PSM을 실행하는 SQL인 CALL 구문은 다음과 같이 실행된다.    
자세한 내용은 [CALL Statement](24-psm-sql-references.md#8813dc15c2cee530)를 참조한다.

```
gSQL> CALL PROC1( 2, 4 );
V1 = 3

Procedure Call complete.
```

ODBC나 JDBC에서 사용하는 procedure call escape sequence를 지원하기 위해 procedure에 대한 다음 구문을 지원한다.

```
{ CALL procedure_name( param1, param2, ... ) }
```

Procedure call escape sequence 구문은 일반 SQL처럼 사용할 수 있다.

```
gSQL> { CALL PROC1(2, 4) };
V1 = 3

Procedure Call complete.
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

<a id="7104ca4c80bfb928"></a>
### 제거

Schema-level procedure는 다음과 같이 DROP PROCEDURE 구문으로 제거한다.  
자세한 내용은 [DROP PROCEDURE](24-psm-sql-references.md#3808c8dd15ec4e09)를 참조한다.

```
DROP PROCEDURE PROC1;
```

GOLDILOCKS의 다른 DROP 구문들처럼 IF EXISTS 구문도 지원한다.

```
DROP PROCEDURE IF EXISTS PROC1;
```

<a id="cee2de4addec07ab"></a>
### Recompile

Schema-level subprogram 내부에서 참조된 객체가 변경되면 해당 subprogram도 영향을 받아 실행 플랜을 다시 생성해야 할 수도 있다.

<a id="5319d92793f3820d"></a>
#### 선언부나 인자에서 참조된 객체

선언부의 각종 item을 정의하거나 인자 타입을 정의할 때 사용된 객체가 변경되면 procedure의 플랜이 자동으로 recompile 된다.

- %TYPE, %ROWTYPE에 사용된 객체
- Explicit cursor 정의 구문에 사용된 객체

객체가 변경된 후 처음으로 해당 procedure가 수행되면 다음 순서에 따라 자동으로 플랜을 다시 생성한다.

1. Plan cache로부터 해당 procedure의 플랜을 가져온다
2. 해당 플랜의 객체 리스트를 validation하는 중에 변경된 객체를 찾는다.
3. 현재 플랜을 discard 시키고, dictionary에 저장된 procedure 정의 구문으로부터 새로운 플랜을 생성한다.
4. 새로 생성된 플랜을 plan cache에 등록한다.
5. 플랜을 실행한다.

<a id="8509d64f2926af99"></a>
#### Body의 SQL에서 참조된 객체

Procedure의 플랜에는 body에 사용된 SQL의 플랜이 저장되지 않고 SQL text만 저장된 상태이다. Procedure를 실행할 때 해당 SQL 구문을 실시간으로 compile 하여 플랜을 생성한 후 수행한다. 따라서 body 내에서 사용된 SQL 객체는 procedure의 플랜 자체에 영향을 주지 않는다.

단, 객체가 변경되면 procedure의 기존 interface인 바인드 개수나 타입이 변경되거나 column이 삭제될 수 있으므로 procedure까지 적절하게 변경하지 않으면 실행할 때 오류가 발생할 수 있다.

<a id="2b406bdbc6df1ac5"></a>
## Schema-level Function

Schema-level function은 expression 내에서 사용되는 함수 형태의 schema-level subprogram이다.

<a id="f3fef0b27c64e470"></a>
### 생성

Schema-level function은 다음과 같이 생성된다. 필요할 경우, 인자들의 타입에 precision과 scale 값을 명시해야 한다.   
자세한 내용은 [CREATE FUNCTION](24-psm-sql-references.md#04b692603afa84f1)을 참조한다.

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

생성된 schema-level function은 procedure와 마찬가지로 INFORMATION_SCHEMA.ROUTINES와 INFORMATION_SCHEMA.PARAMETERS 테이블에서 확인할 수 있다.

<a id="7315ae7316e8adb2"></a>
### 사용

Schema-level function은 일반 SQL이나 PSM 내의 SQL 객체가 사용될 수 있는 모든 expression에서 사용할 수 있다.

```
gSQL> SELECT FUNC1( 2, 4 ) FROM DUAL;

FUNC1( 2, 4 )
-------------
            3

1 row selected.
```

PSM 내에서도 다음과 같이 사용된다.

```
gSQL> DECLARE
  V1 INTEGER;
BEGIN
  V1 := FUNC1( 2, 4 );
  DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
END;
/

V1 = 3

Anonymous PL block executed.
```

다음과 같이 CALL 구문을 이용하여 수행할 수 있다.  
자세한 내용은 [CALL Statement](24-psm-sql-references.md#8813dc15c2cee530)를 참조한다.

```
gSQL> \var V1 INTEGER
gSQL> CALL FUNC1( 2, 4 ) INTO :V1;

Procedure Call complete.

gSQL> \print V1

V1
--
 3
```

Schema-level procedure와 마찬가지로 procedure call escape sequence 구문도 지원한다.

```
{ ? = CALL function_name( param1, param2, ... ) }
```

```
gSQL> { :V1 = CALL FUNC1( 2, 4 ) };

Procedure Call complete.

gSQL> \print V1

V1
--
 3
```

<a id="e3213beb0a42423b"></a>
### 제거

Schema-level function은 다음과 같이 DROP FUNCTION 구문으로 제거한다.  
자세한 내용은 [DROP FUNCTION](24-psm-sql-references.md#2e3b5a779150ed13)을 참조한다.

```
gSQL> DROP FUNCTION FUNC1;

Function dropped.
```

<a id="8f651ec08e28d0d6"></a>
## Built-in Procedures

GOLDILOCKS PSM은 procedure와 function을 구현할 때 디버깅하거나 exception을 처리하기 위해 다음과 같은 built-in procedure들을 제공한다.

**Built-in procedures**

<a id="e9a58830bd463a41"></a>
| Procedure | 기능 |
| --- | --- |
| DBMS_OUTPUT.ENABLE(   buffer_size IN NATIVE_INTEGER := 20000 ) | 주어진 버퍼 크기로 메시지 로깅 기능을 활성화 한다.  만일 버퍼 크기가 주어지지 않으면 디폴트로 20000 byte로 설정된다. 기존에 이미 활성화 되어 있으면 모든 메시지를 버리고 새로 버퍼를 생성한다. |
| DBMS_OUTPUT.DISABLE | 메시지 로깅 기능을 비활성화 한다. 기존에 로깅된 모든 메시지는 버려진다. |
| DBMS_OUTPUT.SET_LOG(   file_path IN VARCHAR(4000) ) | 메시지를 로깅할 때 주어진 경로에 있는 파일에도 동시에 출력한다. 만일 상대 경로 (첫 글자가 /가 아닌 경우)로 주어지면 &lt;SYSTEM_LOGGER_DIR&gt; 프로퍼티에 해당하는 디렉토리 아래에서 대상 파일을 찾는다. |
| DBMS_OUTPUT.PUT_LINE(  item IN VARCHAR(4000) ) | 주어진 expression으로 만들어진 메시지를 버퍼에 저장한다. |
| DBMS_OUTPUT.GET_LINE(  line OUT VARCHAR(4000),  status OUT NATIVE_INTEGER ) | 버퍼에 저장된 메시지들 중에 아직 읽지 않은 가장 오래된 메시지를 한 줄 반환한다. 메시지가 존재하면 status는 0을 반환하고 없으면 1을 반환한다. |
| DBMS_STANDARD.RAISE_APPLICATION_ERROR( error_code IN NATIVE_INTEGER, error_message IN VARCHAR(4000), stack_flag IN BOOLEAN := FALSE ) | 임의의 사용자 exception을 발생시킨다. error_code는 -20000 ~ -20999 사이의 값이어야 하며, TRUE일 경우에는 마지막 stack_flag 인자가 기존 error 들 위에 주어진 에러를 쌓고 FALSE이면 해당 에러가 모든 에러를 대체 (replace)한다 (생략할 수 있고 이 경우 default는 FALSE이다.). |

```
gSQL> DECLARE
V1 VARCHAR(1024);
V2 INTEGER;
BEGIN
  DBMS_OUTPUT.ENABLE(2000);
  DBMS_OUTPUT.PUT_LINE('TEST MSG');
  DBMS_OUTPUT.GET_LINE( V1, V2);
  DBMS_OUTPUT.PUT_LINE('V1 = ' || v1);
  DBMS_OUTPUT.PUT_LINE('V2 = ' || v2);
END;
/

V1 = TEST MSG

V2 = 0

Anonymous PL block executed.
```

메시지 로깅 기능은 세션별로 관리되며, GOLDILOCKS의 interactive command tool인 gsql에서는 serveroutput 옵션으로 메시지 로깅 기능을 켜고 끌 수 있다. PSM을 수행한 후에 메시지 버퍼에 내용이 있으면 모두 자동으로 출력된다.

```
gSQL> \set serveroutput on
gSQL> \var msg VARCHAR(4000)
gSQL> \var status NATIVE_INTEGER
gSQL> CALL DBMS_OUTPUT.PUT_LINE( 'aaa' );
aaa

Procedure Call complete.

gSQL> CALL DBMS_OUTPUT.PUT_LINE( 'bbb' );
bbb

Procedure Call complete.

gSQL> CALL DBMS_OUTPUT.GET_LINE( :msg, :status );

Procedure Call complete.

gSQL> \print msg

MSG 
----
null

gSQL> \print status

STATUS
------
     1
```

---

[← 20. PSM Cursor Statements](20-psm-cursor-statements.md) · [전체 목차](../README.md) · [22. Using SQLs in PSM →](22-using-sqls-in-psm.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
