<a id="6c0d3b246860ad61"></a>

# 31. PSM SQL References

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/6c0d3b246860ad61)  
> 태그: `26c.1_0_tag`

[← 30. PSM Language Element References](30-psm-language-element-references.md) · [전체 목차](../README.md) · [32. Built-in Package →](32-built-in-package.md)

<a id="69bb017860d2aedf"></a>
## ALTER FUNCTION

<a id="a1b6c82726ed4225"></a>
### 기능

Function을 recompile 한다.

<a id="0e0c4f4708bba7ce"></a>
### 구문

```
<alter function statement> ::=
    ALTER FUNCTION function_name COMPILE
    ;
```

<a id="df5522075d1db594"></a>
### 사용 범위 및 접근 권한

&lt;alter function statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 function의 소유자 
- Function이 속한 스키마에 대해 (ALTER PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY PROCEDURE ON DATABASE

<a id="c6b4d44803f8f5de"></a>
### 구문 규칙 및 파라미터

<a id="ac23c227b398fa82"></a>
#### function_name

Compile 할 function의 이름이다.  
schema_name.func_name과 같이 function이 속한 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="27bdae1cedc11394"></a>
### 설명

지정된 schema-level function을 recompile 한다.

<a id="5d2a8e4f4351ad87"></a>
### 사용 예

```
gSQL> ALTER FUNCTION FUNC1 COMPILE;

Function altered.
```

<a id="c291ea030eacd1f0"></a>
### 호환성

SQL 표준에서는 CREATE를 수행할 때 지정된 characteristic들을 변경하는 구문이고, GOLDILOCKS에서는 function의 plan을 다시 생성하는 구문이다.

**SQL 표준 호환성**

<a id="6bda7b2ad3b31aa5"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="10d106f3bae1231e"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE FUNCTION](#8f6d3c41338c889a)
- [DROP FUNCTION](#799b77ea31fecf81)

<a id="9412a5205d4edae2"></a>
## ALTER PACKAGE

<a id="7e90b3fdbdb650d4"></a>
### 기능

Package를 recompile 한다.

<a id="68a52e2ced48e3bb"></a>
### 구문

```
<alter package statement> ::=
    ALTER PACKAGE package_name <package compile clause>
    ;

<package compile clause> ::=
    COMPILE [PACKAGE|SPECIFICATION|BODY]
```

<a id="c1fc027d7fc4199c"></a>
### 사용 범위 및 접근 권한

&lt;alter package statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 package의 소유자 
- Package가 속한 스키마에 대해 (ALTER PACKAGE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY PACKAGE ON DATABASE

<a id="642aa7cdf4d94563"></a>
### 구문 규칙 및 파라미터

<a id="f008dbe22de1b29b"></a>
#### package_name

Compile 할 package의 이름이다.  
schema_name.package_name과 같이 package가 속한 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="e964d0b7bc215a80"></a>
#### &lt;package compile clause&gt;

Package를 compile 할 대상을 지정한다.  
만약 대상을 생략하면, PACKAGE를 지정한 것과 동일하게 package specification 과 package body 전체가 recompile 된다.

- PACKAGE
    - Package specification과 body를 모두 recompile 한다.
- SPECIFICATION
    - Package specification만 recompile 한다.
- BODY
    - Package body만 recompile 한다.

<a id="369492979753e395"></a>
### 설명

지정된 package를 recompile 한다.  
Compile 된 package의 실행 code는 plan cache에 저장된다.

<a id="85d0776532f1aa97"></a>
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

<a id="54845c0f72a3004c"></a>
### 호환성

SQL 표준에서는 ALTER MODULE 구문이다.

<a id="a667d30104b6bdc3"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE](#5f9bdd6eb052f51f)
- [CREATE PACKAGE BODY](#4af32611ea712290)
- [DROP PACKAGE](#561079b3305fcaea)

<a id="fedcce74e6accc1d"></a>
## ALTER PROCEDURE

<a id="302c6d8202e71485"></a>
### 기능

Procedure를 recompile 한다.

<a id="5cd7e950b6b675b0"></a>
### 구문

```
<alter procedure statement> ::=
    ALTER PROCEDURE proc_name COMPILE
    ;
```

<a id="7debc4c0e0b09d37"></a>
### 사용 범위 및 접근 권한

&lt;alter procedure statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 procedure의 소유자 
- Procedure가 속한 스키마에 대해 (ALTER PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY PROCEDURE ON DATABASE

<a id="bbce5ad196a28036"></a>
### 구문 규칙 및 파라미터

<a id="271be190163e6848"></a>
#### proc_name

Compile할 procedure의 이름이다.   
schema_name.proc_name과 같이 procedure가 속한 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="74e8f3896ffcd988"></a>
### 설명

지정된 schema-level procedure를 recompile 한다.

<a id="8a10bb236265386f"></a>
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

<a id="2e829b7efceb217a"></a>
### 호환성

SQL 표준에서는 CREATE를 수행할 때 지정된 characteristic들을 변경하는 구문이고, GOLDILOCKS에서는 procedure의 plan을 다시 생성하는 구문이다.

**SQL 표준 호환성**

<a id="be2d364be08762e9"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="c4a097a0dc78c845"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PROCEDURE](#48b6178f1f6cd4cb)
- [DROP PROCEDURE](#47bed13ab733e3a0)

<a id="7ef86e0333181a4e"></a>
## ALTER TRIGGER name COMPILE

<a id="5ebb67f8661b4caa"></a>
### 기능

Trigger를 recompile 한다.

<a id="d90b09dfb2357cb0"></a>
### 구문

```
<alter trigger compile statement> ::=
    ALTER TRIGGER <trigger name> COMPILE
    ;
```

<a id="0f56046b94138ca4"></a>
### 사용 범위 및 접근 권한

&lt;alter trigger compile statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 trigger의 소유자
- Trigger가 속한 스키마에 대해 (ALTER TRIGGER 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TRIGGER ON DATABASE

<a id="922e2d047d0ac6ba"></a>
### 구문 규칙 및 파라미터

<a id="349fbd33e408a079"></a>
#### &lt;trigger name&gt;

Compile할 trigger의 이름이다.  
schema_name.trigger_name과 같이 trigger가 속한 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="5e80cb09038573b5"></a>
### 설명

명시한 trigger를 recompile한다.

<a id="512df7ce2ecd2682"></a>
### 사용 예

```
-- Orders table이 update 될 때, orders의 변경 상태를 order_status_history에 기록하는 trigger이다.
gSQL> 
CREATE OR REPLACE TRIGGER trg_orders_status_audit
AFTER UPDATE OF status ON orders
REFERENCING OLD ROW AS o_row
            NEW ROW AS n_row            
FOR EACH ROW
BEGIN
  INSERT INTO order_status_history VALUES( o_row.order_id,
                                           o_row.status,
                                           n_row.status,
                                           SYSDATE );
END;
/

ERR-01000(16659): Warning: trigger "PUBLIC"."TRG_ORDERS_STATUS_AUDIT" has compilation errors : 
(1) at (8:3): ERR-42000(16040): table or view does not exist
Trigger created.

-- Trigger가 invalid 하여 UPDATE 구문이 실패
gSQL>
UPDATE orders
   SET status = 'Shipped', updated_at = SYSDATE
 WHERE order_id = 1;

ERR-0W000(17134): TRIGGER(TRG_ORDERS_STATUS_AUDIT) compilation error : 
(1) at (4:3): ERR-42000(16040): table or view does not exist

-- Trigger에서 참조하는 order_status_history table 생성
gSQL>
CREATE TABLE order_status_history( order_id   NUMBER,
                                   old_status VARCHAR2(20),
                                   new_status VARCHAR2(20),
                                   changed_at DATE );

Table created.

-- Trigger를 recompile 하여 상태 확인
gSQL> ALTER TRIGGER trg_orders_status_audit COMPILE;

Trigger altered.

-- 정상적으로 orders table에 대해 UPDATE 수행
gSQL>
UPDATE orders
   SET status = 'Shipped', updated_at = SYSDATE
 WHERE order_id = 1;

1 row updated.

gSQL> SELECT * FROM order_status_history;

ORDER_ID OLD_STATUS     NEW_STATUS CHANGED_AT
-------- -------------- ---------- ----------
       1 Order Received Shipped    2025-08-12

1 row selected.
```

<a id="2ac0632a0b2bdf1d"></a>
### 호환성

SQL 표준에는 정의되어 있지 않다.

<a id="5df5de8a9945701d"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE TRIGGER](#c36270132fc5138d)
- [DROP TRIGGER](#405a8fa6b4a11ae3)

<a id="f14d8e926a633165"></a>
## ALTER TRIGGER name ENABLE/DISABLE

<a id="7d4efeff62bc2d2c"></a>
### 기능

Trigger 활성화 여부를 변경한다.

<a id="fc0729f0058c548e"></a>
### 구문

```
<alter trigger enforcement statement> ::=
    ALTER TRIGGER <trigger name> <trigger enforcement>
    ;

<trigger enforcement> ::=
      { ENABLE | ENFORCED }
    | { DISABLE | NOT ENFORCED }
```

<a id="a501a3d1b309b5c9"></a>
### 사용 범위 및 접근 권한

&lt;alter trigger enforcement statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 trigger의 소유자
- Trigger가 속한 스키마에 대해 (ALTER TRIGGER 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TRIGGER ON DATABASE

<a id="12fa0c66f728028e"></a>
### 구문 규칙 및 파라미터

<a id="d1505a5466237377"></a>
#### &lt;trigger name&gt;

활성화 상태를 변경하려는 trigger의 이름이다.  
schema_name.trigger_name과 같이 trigger가 속한 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="f07091073e151ea2"></a>
#### &lt;trigger enforcement&gt;

ENABLE 과 ENFORCED 는 동일한 의미이다.  
DISABLE 과 NOT ENFORCED 는 동일한 의미이다.

- ENABLE
    - Event table에 DML 발생 시 trigger를 활성화한다.
- DISABLE
    - Event table에 DML 발생 시 trigger를 비활성화한다.

<a id="3317bd23407482ca"></a>
### 설명

Trigger 활성화 여부를 변경한다.

<a id="0f3282e76124c7e6"></a>
### 사용 예

- Trigger 비활성화 예

```
-- Invalid한 trigger 생성
gSQL>
CREATE OR REPLACE TRIGGER trg_orders_status_audit
AFTER UPDATE OF status ON orders
REFERENCING OLD ROW AS o_row
            NEW ROW AS n_row            
FOR EACH ROW
BEGIN
  INSERT INTO order_status_history VALUES( o_row.order_id,
                                           o_row.status,
                                           n_row.status,
                                           SYSDATE );
END;
/

ERR-01000(16659): Warning: trigger "PUBLIC"."TRG_ORDERS_STATUS_AUDIT" has compilation errors : 
(1) at (7:3): ERR-42000(16040): table or view does not exist
Trigger created.

-- Trigger가 invalid 하여 UPDATE 구문이 실패
gSQL> 
UPDATE orders
   SET status = 'Shipped', updated_at = SYSDATE
 WHERE order_id = 1;

ERR-0W000(17134): TRIGGER(TRG_ORDERS_STATUS_AUDIT) compilation error : 
(1) at (4:3): ERR-42000(16040): table or view does not exist

-- Trigger 비활성화
gSQL> ALTER TRIGGER trg_orders_status_audit DISABLE;

Trigger altered.

-- UPDATE 수행 성공
gSQL> UPDATE orders
   SET status = 'Shipped', updated_at = SYSDATE
 WHERE order_id = 1;

1 row updated.
```

- Trigger 활성화 예

```
-- 비활성화 상태인 invalid trigger 생성
gSQL>
CREATE OR REPLACE TRIGGER trg_orders_status_audit
AFTER UPDATE OF status ON orders
REFERENCING OLD ROW AS o_row
            NEW ROW AS n_row
FOR EACH ROW
DISABLE
BEGIN
  INSERT INTO order_status_history VALUES (o_row.order_id, o_row.status, n_row.status, SYSDATE);
END;
/

ERR-01000(16659): Warning: trigger "PUBLIC"."TRG_ORDERS_STATUS_AUDIT" has compilation errors : 
(1) at (8:3): ERR-42000(16040): table or view does not exist
Trigger created.

-- 생성 시 trigger가 비활성화 되어 있어서 실행되지 않음
gSQL>
UPDATE orders
   SET status = 'Processing Order', updated_at = SYSDATE
 WHERE order_id = 1;

1 row updated.

gSQL> SELECT * FROM order_status_history;

no rows selected.

-- Trigger에서 참조하는 order_status_history table 생성
gSQL>
CREATE TABLE order_status_history( order_id   NUMBER,
                                   old_status VARCHAR2(20),
                                   new_status VARCHAR2(20),
                                   changed_at DATE );

Table created.

-- Trigger를 recompile 하여 상태 확인
gSQL> ALTER TRIGGER trg_orders_status_audit COMPILE;

Trigger altered.

-- Trigger 활성화
gSQL> ALTER TRIGGER trg_orders_status_audit ENABLE;

Trigger altered.

-- UPDATE 에 대한 trigger 수행
gSQL>
UPDATE orders
   SET status = 'Shipped', updated_at = SYSDATE
 WHERE order_id = 1;

1 row updated.

gSQL> SELECT * FROM order_status_history;

ORDER_ID OLD_STATUS       NEW_STATUS CHANGED_AT
-------- ---------------- ---------- ----------
       1 Processing Order Shipped    2025-08-12

1 row selected.
```

<a id="eea36a403de8bbac"></a>
### 호환성

SQL 표준에는 정의되어 있지 않다.

<a id="669684d24e675f57"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE TRIGGER](#c36270132fc5138d)
- [DROP TRIGGER](#405a8fa6b4a11ae3)

<a id="ae1a37f358aeb5db"></a>
## ALTER TRIGGER name RENAME TO

<a id="ad5bbbe1bbd6effb"></a>
### 기능

Trigger 이름을 변경한다.

<a id="aefcd1761b5e9160"></a>
### 구문

```
<alter trigger rename statement> ::=
    ALTER TRIGGER <trigger name> RENAME <new trigger name>
    ;
```

<a id="0cc26e99404b46f5"></a>
### 사용 범위 및 접근 권한

&lt;alter trigger rename statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 trigger의 소유자
- Trigger가 속한 스키마에 대해 (ALTER TRIGGER 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TRIGGER ON DATABASE

<a id="c28a98782a01cce8"></a>
### 구문 규칙 및 파라미터

<a id="ba848d3318c67f34"></a>
#### &lt;trigger name&gt;

변경하려는 trigger의 이름이다.  
schema_name.trigger_name과 같이 trigger가 속한 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="415cdb622f75a455"></a>
#### &lt;new trigger name&gt;

변경하려는 trigger의 이름으로서 스키마 내에서 고유해야 한다.  
새 trigger 이름의 길이는 128 바이트보다 작아야 한다.

<a id="8ad2383142adbde3"></a>
### 설명

명시된 trigger의 이름을 변경한다.

<a id="830a16feed516af3"></a>
### 사용 예

```
gSQL> ALTER TRIGGER t1 RENAME TO new_t1;

Trigger altered.
```

<a id="0ed746cb7246ca32"></a>
### 호환성

SQL 표준에는 정의되어 있지 않다.

<a id="5a24aa8dcf6c34f6"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE TRIGGER](#c36270132fc5138d)
- [DROP TRIGGER](#405a8fa6b4a11ae3)

<a id="0b77efd04b5af863"></a>
## CALL Statement

<a id="812567f77c9f7bef"></a>
### 기능

Schema level procedure나 function을 수행한다.

<a id="43af39f5381ebec7"></a>
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

<a id="e34d03d0b9b30385"></a>
### 사용 범위 및 접근 권한

&lt;call statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다

- 해당 procedure에 대한 EXECUTE 권한
- Procedure가 속한 schema에 대해 (EXECUTE PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- EXECUTE ANY PROCEDURE ON DATABASE

<a id="bb2fa3135ec86f29"></a>
### 구문 규칙 및 파라미터

<a id="6fcea61f478799ee"></a>
#### proc_name

실행할 procedure/ function의 이름이다   
schema_name.proc_name과 같이 procedure가 속한 schema를 포함할 수 있다.

<a id="6d583295ef0eb81b"></a>
#### value_expr

procedure에 전달할 인자값을 표현한다.  
'?' 나 ':V1'과 같은 bind parameter를 사용할 수도 있다.

<a id="cbeacb79802c7712"></a>
### 설명

명시된 인자들을 사용하여 schema level SQL procedure나 function을 실행한다.

&lt;sql call statement&gt; 형식 중에 function은 INTO 절 다음에 host variable 표현이나 dynamic bind parameter (?)를 사용하여 결과값을 반환한다.

&lt;odbc procedure call escape sequence&gt; 형식은 ODBC/ JDBC 등에서 PROCEDURE를 호출하기 위한   
표준 구문이며, GOLDILOCKS는 이 구문을 server에서 지원한다. (gsql 등의 tool에서도 사용 가능하다.)  
Function은 앞에 assign 표현( ? = )을 사용하여 결과값을 반환한다.

<a id="833fe37fdd02ece2"></a>
### 사용 예

<a id="1c6c2f616639ce11"></a>
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

<a id="b5f0d86889720958"></a>
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

<a id="4fabaa0ccb4a5594"></a>
### 호환성

SQL 표준에서는 PROCEDURE에 대한 호출만 가능하여 [INTO] 절 이하를 정의하지 않고 있다.

<a id="8f6d3c41338c889a"></a>
## CREATE FUNCTION

<a id="004f3460f66a1d6f"></a>
### 기능

Schema level function을 정의한다.

<a id="e01c8c46ef388428"></a>
### 구문

```
<create function statement> ::= 
        CREATE [ OR REPLACE ] FUNCTION <function name> 
        [ ( <parameter list> ) ]
        <return clause>
        [ <function option list> ]
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

<function option list> ::=
      <function option> [ ... ]

<function option> ::=
      <invoker rights clause>
    | <function characteristics>

<invoker rights clause> ::=
      AUTHID CURRENT_USER 
    | AUTHID DEFINER

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

<a id="b2d3cdfb7e6e9b64"></a>
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

<a id="072b9d84ae7bcd92"></a>
### 구문 규칙 및 파라미터

<a id="3a8ae6cf78a467c7"></a>
#### OR REPLACE

이미 function이 존재할 경우, 기존의 function을 새로운 function으로 대체한다.

<a id="ff422a6bbf8860c9"></a>
#### function name

생성할 function의 이름으로서, 스키마 내에서 고유해야 한다.  
schema_name.function_name과 같이 function이 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
function 이름의 길이는 128 바이트보다 작아야 한다.

<a id="f2f2d79b3ff49848"></a>
#### parameter name

Function의 parameter 이름을 정의한다.  
각 parameter 이름은 function 내에서 고유해야 한다.  
즉, function의 parameter와 PL item은 동일한 이름을 가질 수 없다.  
Parameter 이름의 길이는 128 바이트보다 작아야 한다.  
하나의 function에서 사용할 수 있는 parameter의 최대 개수에는 제한이 없다.

<a id="af8ff8a268d11f5c"></a>
#### parameter mode

각 parameter mode를 설정한다.  
Parameter mode에는 IN, OUT, IN OUT이 있다.  
Parameter mode를 명시하지 않을 경우, 기본 mode는 IN이다.

<a id="f969f1734de75083"></a>
#### parameter default

Parameter의 기본값이다.  
Parameter default가 명시된 parameter는 function을 실행할 때 생략할 수 있다.  
Parameter를 명시하지 않고 생략할 경우, parameter를 정의할 때 명시한 &lt;value expression&gt;을 기본값으로 가진다.  
&lt;value expression&gt;의 datatype은 parameter의 datatype이어야 한다.  
&lt;parameter default&gt;를 가진 parameter 이후에 정의되는 모든 parameter에는 &lt;parameter default&gt;가 있어야 한다.

<a id="d51fa3c938fb212d"></a>
#### return clause

Function의 반환 형태를 정의한다.  
&lt;return clause&gt;에서는 다음과 같이 정의된다.

- RETURN &lt;datatype&gt;
    - Function에서 반환하는 반환값의 datatype을 정의한다.
- RETURN TABLE ( &lt;table function column list&gt; )
    - 반환하는 결과 집합의 table type을 정의한다.

<a id="7a18721998886461"></a>
#### table function column list

Table function이 반환하는 결과 집합의 column 이름이다.  
Column 이름의 길이는 128 바이트보다 작아야 한다.  
Column 개수에는 제한이 없다.  
각 column 이름은 &lt;table function column list&gt;에서 고유하다.  
Column 이름은 parameter 및 declare item 이름과 동일할 수 있다.  
&lt;table function column list&gt;에 정의된 column은 function의 PL block 내에서 참조할 수 없다.

<a id="1ddd809b8a86bf66"></a>
#### invoker rights clause

Function을 실행 시 참조하는 객체의 이름 해석과 권한을 생성자 (DEFINER)의 관점으로 수행할지 실행하는 사용자 (CURRENT_USER)의 관점으로 수행할지 명시한다.

- AUTHID CURRENT_USER: Function을 실행하는 도중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되고 수행된다.
- AUTHID DEFINER: Function을 실행하는 도중에 수행되는 SQL들은 definer의 authorization에 따라 해석되고 수행된다.

&lt;invoker rights clause&gt;을 생략하면 기본값은 AUTHID DEFINER이다.

<a id="f85395ec3a8cb708"></a>
#### function characteristics

&lt;function characteristics&gt;은 function의 특성을 명시한다.  
동일한 특성에 대해서 중복은 허용하지 않는다.  
자세한 설명은 [Routine Characteristics](30-psm-language-element-references.md#904f272f8d216420)를 참조한다.

<a id="4d2a7846a6c5ce1d"></a>
#### routine body

- SQL body
    - 자세한 설명은 [Block (BEGIN .. END)](30-psm-language-element-references.md#b5f1979bc247ce01)을 참고한다.
- external body
    - 자세한 설명은 [Call Specification](30-psm-language-element-references.md#1663813aaf9c3eb4)을 참고한다.
- Function의 &lt;routine body&gt;에는 '?'나 ':V1'과 같은 bind parameter를 사용할 수 없다.

<a id="5d577b5965a6475e"></a>
### 설명

Schema-level SQL function을 정의한다. 생성된 function은 모든 expression에서 호출될 수 있다.

Function의 정의는 INFORMATION_SCHEMA의 ROUTINES 테이블에서 확인할 수 있다. Function의 parameter들에 대한 정의는 INFORMATION_SCHEMA의 PARAMETERS 테이블에서 확인할 수 있다.

관련 객체들이 존재하지 않아 function이 일시적으로 불완전해졌을 경우, [ALTER FUNCTION](#69bb017860d2aedf) 구문으로 plan 생성을 다시 시도해볼 수 있다.

생성된 function은 [DROP FUNCTION](#799b77ea31fecf81) 구문을 사용하여 제거할 수 있다.  
Function의 최대 생성 개수에는 제한이 없으므로 저장 공간에 문제가 없는 한 계속 생성할 수 있다.

<a id="cc8314666d8970c7"></a>
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

<a id="f6ede4bc61855bfa"></a>
### 호환성

SQL 표준에서는 OR REPLACE 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="37353d1264fd3e31"></a>
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
| B122 | Routine language C | O |
| B123 | Routine language COBOL | X |
| B124 | Routine language Fortran | X |
| B125 | Routine language MUMPS | X |
| B126 | Routine language Pascal | X |
| B127 | Routine language PL/I | X |
| B128 | Routine language SQL | O |
| B129 | Routine language Ada: VARCHAR and NUMERIC support | X |

<a id="a9c8c550aefc23f0"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [DROP FUNCTION](#799b77ea31fecf81)
- [ALTER FUNCTION](#69bb017860d2aedf)

<a id="e6a29c79119e1af1"></a>
## CREATE LIBRARY

<a id="eaf94e8a8d71b7f4"></a>
### 기능

C언어 프로그램의 shared library와 관련된 스키마 객체인 library를 생성한다.

<a id="1719785f40b2997f"></a>
### 구문

```
<create library statement> ::=
      CREATE [ OR REPLACE ] LIBRARY <library name> 
      { IS | AS }
      '<file path name>';
```

<a id="e20c3de80a2d2bb5"></a>
### 사용 범위 및 접근 권한

&lt;create library statement&gt; 구문을 수행하려면 사용자가 다음 조건을 만족해야 한다.

- Library를 생성하려면 다음 권한 중 하나가 있어야 한다.
    - Library가 속한 스키마에 대해 (CREATE LIBRARY 또는 CONTROL SCHEMA) ON SCHEMA
    - CREATE ANY PACKAGE ON DATABASE
- OR REPLACE 절을 명시할 경우, 기존 library를 제거하려면 다음 조건 중 하나를 만족해야 한다.
    - 해당 library의 소유자
    - Library가 속한 스키마에 대해 (DROP LIBRARY 또는 CONTROL SCHEMA) ON SCHEMA
- 구문을 수행한 사용자는 생성한 library의 소유자이다.

<a id="239941789337db71"></a>
### 구문 규칙 및 파라미터

<a id="a902382f194e7227"></a>
#### OR REPLACE

이미 Library가 존재할 경우, 기존의 Library를 대체한다.

<a id="965532e1dfd9868a"></a>
#### library name

생성하고자 하는 library의 이름이며, schema 내에서 유일한 이름이어야 한다.  
schema_name.library_name과 같이 library가 속할 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
Library 이름의 길이는 128 바이트보다 작아야 한다.

<a id="64bbf87b9e77bb26"></a>
#### file path name

C언어 프로그램의 shared library의 이름 또는 full path를 명시할 수 있다.

Library를 생성할 때 file 이름만 명시한 경우, 해당 파일은 반드시 EXTLIB_DIR 프로퍼티에 설정된 폴더에 위치해야 한다. 반면, full_path를 명시한 경우에는 해당 path에 있는 shared library를 실행한다.

Cluster system에서 사용할 경우, 각 노드에서 동일한 shared library 파일을 관리해야 한다.

<a id="da675e1fb0c41356"></a>
### 설명

C언어 프로그램의 shared library와 관련된 스키마 객체인 library를 생성한다.  
Library는 [Call Specification](30-psm-language-element-references.md#1663813aaf9c3eb4)에서 호출된다.  
생성된 library는 [DROP LIBRARY](#11be420b5d5517c9) 구문을 사용하여 제거할 수 있다.

<a id="ad6ce2df016206f4"></a>
### 사용 예

- file 이름만 명시

```
gSQL>
CREATE LIBRARY lib1 AS 'add.so';
/

Library created.
```

- full path와 file 이름 명시

```
gSQL>
CREATE LIBRARY lib2 AS '/home/user1/files/add.so';
/

Library created.
```

<a id="345426f5260e3468"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="1ecaa80be1d57702"></a>
### 참조

자세한 내용은 [DROP LIBRARY](#11be420b5d5517c9)를 참조한다.

<a id="5f9bdd6eb052f51f"></a>
## CREATE PACKAGE

<a id="b0c00522977518c1"></a>
### 기능

Package 내에서 사용될 public item들에 대한 spec을 정의한다.

<a id="31f79245607ff7ff"></a>
### 구문

```
<create package statement> ::=
      CREATE [ OR REPLACE ] PACKAGE <package name>
      [ <invoker rights clause> ]
      { IS | AS }
      <declare item> 
      END [ <package name> ]
      ;

<invoker rights clause> ::=
      AUTHID CURRENT_USER 
    | AUTHID DEFINER

<declare item> ::=
      <variable declaration>
    | <type definition>
    | <explicit cursor declaration>
    | <explicit cursor definition>
    | <exception declaration>
    | <exception init pragma>
    | <procedure declaration>
    | <function declaration>
```

<a id="e9e54b5ab1cbcdee"></a>
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

<a id="1e834f025218de89"></a>
### 구문 규칙 및 파라미터

<a id="35e5d8b65c44eb56"></a>
#### OR REPLACE

이미 package가 존재할 경우, 기존의 package specification을 대체한다.

<a id="8d22705f3c6c0d80"></a>
#### PACKAGE NAME

생성할 package의 이름이며, schema 내에서 유일한 이름이어야 한다.   
schema_name.package_name과 같이 package가 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
Package 이름의 길이는 128 바이트보다 작아야 한다.

<a id="2981e124055fbc4a"></a>
#### invoker rights clause

Package를 실행 시 참조하는 객체의 이름 해석 및 권한을 생성자 (DEFINER)의 관점으로 수행할지 실행하는 사용자 (CURRENT_USER)의 관점으로 수행할지 명시한다.

- AUTHID CURRENT_USER: Package를 실행하는 도중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되고 수행된다.
- AUTHID DEFINER: Package를 실행하는 도중에 수행되는 SQL들은 definer의 authorization에 따라 해석되고 수행된다.

&lt;invoker rights clause&gt;을 생략하면 기본값은 AUTHID DEFINER이다.

<a id="6b4482a1cab571bc"></a>
#### declare item

Package 외부에서 접근 가능한 item을 선언한다. 이를 public package item이라고 한다.  
Package Spec에서 선언한 function과 procedure는 반드시 create package body 구문에서 정의해야 한다.  
Package Spec에서 SQL 없이 선언만 된 Explicit Cursor는 반드시 create package body 구문에서 정의해야 한다.  
선언할 수 있는 item에 대한 자세한 내용은 [Block (BEGIN .. END)](30-psm-language-element-references.md#b5f1979bc247ce01)의 [declare item](30-psm-language-element-references.md#a423847e65761397)을 참조한다.

<a id="b8f1a33037a9bb07"></a>
### 설명

Schema-level package specification을 생성한다.  
Package 생성 정보는 INFORMATION_SCHEMA.MODULES 테이블에서 확인할 수 있다.  
Package 내의 공개된 각 procedure 및 function 목록은 INFORMATION_SCHEMA.ROUTINES 테이블에서 확인할 수 있다.  
Package 내의 공개된 각 procedure 및 function의 parameter들에 대한 정의는 INFORMATION_SCHEMA.PARAMETERS 테이블에서 확인할 수 있다.

생성된 package의 모든 public package item은 다른 PSM 객체나 anonymous block에서 참조할 수 있다.

Package가 참조하는 객체의 상태가 변경되어 package가 invalid 상태가 되었다면, 아래의 구문으로 recompile이 가능하다.

- ALTER PACKAGE &lt;package name&gt; COMPILE
- ALTER PACKAGE &lt;package name&gt; COMPILE SPECIFICATION

<a id="5ba12cccb8cd66b0"></a>
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

<a id="58dbc3f838628d0f"></a>
### 호환성

SQL 표준에서는 CREATE MODULE 구문이다.

<a id="e66a904ba46c6da8"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE BODY](#4af32611ea712290)
- [DROP PACKAGE](#561079b3305fcaea)
- [ALTER PACKAGE](#9412a5205d4edae2)

<a id="4af32611ea712290"></a>
## CREATE PACKAGE BODY

<a id="6f8b9e443573f029"></a>
### 기능

Package 내에서 사용될 procedure, function 및 커서들에 대한 정의를 생성한다.

<a id="cc3d0e8420615d09"></a>
### 구문

```
<create package body statement> ::=
      CREATE [ OR REPLACE ] PACKAGE BODY <package name>
      { IS | AS }
      <declare item>
      [ <initialization part> ]
      END [ <package name> ]
      ;

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

<initialization part> ::=
      BEGIN
      <pl statement list>
      [ <exception block> ]
```

<a id="e6c4ee722cb5a07d"></a>
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

<a id="35011c822bd76b84"></a>
### 구문 규칙 및 파라미터

<a id="f464ed0b038fe4e4"></a>
#### OR REPLACE

Package body가 이미 존재할 경우, 기존의 package body definition을 대체한다.

<a id="23bf39f49f97f3d5"></a>
#### PACKAGE NAME

생성할 package body의 이름이며, package spec 생성에 사용된 동일한 이름을 사용해야 한다. schema 내에서 유일한 이름이어야 한다.   
schema_name.package_name 과 같이 package가 속할 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
Package 이름의 길이는 128 바이트보다 작아야 한다.

<a id="90787fdb1e177a8c"></a>
#### declare item

Package body에서 사용할 item을 선언한다. 이를 private package item이라고 한다.  
private package item은 public package item과 중복된 이름을 가질 수 없다.  
Package spec에서 선언된 routine들은 반드시 package body에서 정의해야 한다.  
Package spec에서 SQL 없이 선언만 된 커서들은 반드시 package body에 정의해야 한다.  
선언할 수 있는 item에 대한 자세한 내용은 [Block (BEGIN .. END)](30-psm-language-element-references.md#b5f1979bc247ce01)에서 [declare item](30-psm-language-element-references.md#a423847e65761397)을 참조한다.

<a id="e4d9bc91dc345438"></a>
#### Initialization Part

Package instance 생성 과정에서 내부 변수등의 초기화를 위해 한 번만 수행되는 구문들을 기술한다.  
각 구문에 대한 자세한 설명은 [Block (BEGIN .. END)](30-psm-language-element-references.md#b5f1979bc247ce01)의 [pl statement](30-psm-language-element-references.md#47489c93a40729ce)를 참조한다.

<a id="53923a49d1b53170"></a>
### 설명

Schema-level package body를 생성한다.   
Package body의 생성 정보는 INFORMATION_SCHEMA.MODULE_BODY 테이블에서 확인할 수 있다.

생성된 package body에서 선언한 private package item은 다른 PSM 객체나 anonymous block에서 참조할 수 없다.

Package body가 참조하는 객체의 상태가 변경되어 package body가 invalid 상태가 되었다면, 아래의 구문으로 recompile이 가능하다.

- ALTER PACKAGE &lt;package name&gt; COMPILE
- ALTER PACKAGE &lt;package name&gt; COMPILE BODY

생성된 package body는 아래의 구문으로 삭제할 수 있다.

- DROP PACKAGE &lt;package name&gt;
- DROP PACKAGE BODY &lt;package name&gt;

<a id="f61e0ec2d2fccf0e"></a>
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

<a id="491d7417152968b2"></a>
### 호환성

SQL 표준에는 정의되어 있지 않다.

<a id="05ca0fda1af9bb1c"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE](#5f9bdd6eb052f51f)
- [DROP PACKAGE](#561079b3305fcaea)
- [ALTER PACKAGE](#9412a5205d4edae2)

<a id="48b6178f1f6cd4cb"></a>
## CREATE PROCEDURE

<a id="ca1ab848a5000d46"></a>
### 기능

Schema-level procedure를 정의한다.

<a id="55380e86e236d77a"></a>
### 구문

```
<create procedure statement> ::= 
        CREATE [ OR REPLACE ] PROCEDURE <procedure name> 
        [ ( <parameter list> ) ]
        [ <procedure option list> ]
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

<procedure option list> ::=
      <procedure option> [ ... ]

<procedure option> ::=
      <invoker rights clause>
    | <procedure characteristics>

<invoker rights clause> ::=
      AUTHID CURRENT_USER 
    | AUTHID DEFINER

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

<a id="03318a526e739ea4"></a>
### 사용 범위 및 접근 권한

&lt;create procedure statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- Procedure를 생성하려면 다음 권한 중 하나가 있어야 한다.
    - Procedure가 속한 스키마에 대해 (CREATE PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
    - CREATE ANY PROCEDURE ON DATABASE
- OR REPLACE 절을 사용할 때 이미 procedure가 존재할 경우, 기존 procedure를 제거할 수 있는 다음 권한 중 하나가 있어야 한다.
    - 해당 procedure의 소유자
    - Procedure가 속한 스키마에 대해 (DROP PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
    - DROP ANY PROCEDURE ON DATABASE
- 구문을 수행한 사용자는 생성한 procedure의 소유자이다.

<a id="7fd4dd7386e37cee"></a>
### 구문 규칙 및 파라미터

<a id="cac6472b1aecd681"></a>
#### OR REPLACE

이미 procedure가 존재할 경우, 기존의 procedure를 새로운 procedure로 대체한다.

<a id="2b32bf8a7f0f30a0"></a>
#### procedure name

생성할 procedure의 이름으로서 스키마 내에서 고유해야 한다.  
schema_name.procedure_name과 같이 procedure가 속할 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
procedure 이름의 길이는 128 바이트보다 작아야 한다.

<a id="1a18e228ccb072c0"></a>
#### parameter name

Procedure의 parameter 이름을 정의한다.  
각 parameter 이름은 procedure 내에서 고유해야 한다.  
즉, procedure의 parameter와 PL item은 동일한 이름을 가질 수 없다.  
parameter 이름의 길이는 128 바이트보다 작아야 한다.  
하나의 procedure에서 사용할 수 있는 parameter의 최대 개수에는 제한이 없다.

<a id="01c19654421520d6"></a>
#### parameter mode

각 parameter mode를 설정한다.  
Parameter mode에는 IN, OUT, IN OUT이 있다.  
Parameter mode를 명시하지 않을 경우, 기본 mode는 IN이다.

<a id="aa2a26f74bef1d4a"></a>
#### parameter default

Parameter의 기본값이다.  
Parameter default가 명시된 parameter는 procedure 실행할 때 생략할 수 있다.  
Parameter를 명시하지 않고 생략할 경우, parameter를 정의할 때 명시한 &lt;value expression&gt;을 기본값으로 가진다.  
&lt;value expression&gt;의 datatype은 parameter의 datatype이어야 한다.  
&lt;parameter default&gt;를 가진 parameter 이후에 정의되는 모든 parameter에는 &lt;parameter default&gt;가 있어야 한다.

<a id="9e1dc65848bd52a1"></a>
#### invoker rights clause

Procedure를 실행할 때 참조하는 객체의 이름 해석 및 권한을 생성자 (DEFINER)의 관점으로 수행할지 실행하는 사용자 (CURRENT_USER)의 관점으로 수행할지 명시한다.

- AUTHID CURRENT_USER: Procedure를 실행하는 도중에 수행되는 SQL들은 invoker의 authorization에 따라 해석되고 수행된다.
- AUTHID DEFINER: Procedure를 실행하는 도중에 수행되는 SQL들은 definer의 authorization에 따라 해석되고 수행된다.

&lt;invoker rights clause&gt;을 생략하면 기본값은 AUTHID DEFINER이다.

<a id="f04e3e3acd5b9e5a"></a>
#### procedure characteristics

&lt;procedure characteristics&gt;은 procedure의 특성을 명시한다.  
동일한 특성에 대해서 중복은 허용하지 않는다.  
자세한 설명은 [Routine Characteristics](30-psm-language-element-references.md#904f272f8d216420)를 참고한다.

<a id="1283749d8b08f77a"></a>
#### routine body

- SQL body
    - 자세한 설명은 [Block (BEGIN .. END)](30-psm-language-element-references.md#b5f1979bc247ce01)을 참고한다.
- external body
    - 자세한 설명은 [Call Specification](30-psm-language-element-references.md#1663813aaf9c3eb4)을 참고한다.
- Procedure의 &lt;routine body&gt;에는 '?'나 ':V1'과 같은 bind parameter를 사용할 수 없다.

<a id="89224e3cc5799db3"></a>
### 설명

Schema-level SQL procedure를 정의한다. 생성된 procedure는 CALL 구문, anonymous block, 또는 다른 procedure/ function에서 호출될 수 있다.

Procedure의 정의는 INFORMATION_SCHEMA의 ROUTINES 테이블에서 확인할 수 있다. Procedure의 parameter들에 대한 정의는 INFORMATION_SCHEMA의 PARAMETERS 테이블에서 확인할 수 있다.

관련 객체들이 존재하지 않아 procedure가 일시적으로 불완전해졌을 경우, [ALTER PROCEDURE](#fedcce74e6accc1d) 구문으로 plan 생성을 다시 시도해볼 수 있다.

생성된 procedure는 [DROP PROCEDURE](#47bed13ab733e3a0) 구문을 사용하여 제거할 수 있다.  
Procedure의 최대 생성 개수에는 제한이 없으므로 저장 공간에 문제가 없는 한 계속 생성할 수 있다.

<a id="5b6e545bea422f5b"></a>
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

<a id="8e07a2d13cd1a694"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="2f01b2b14687a28b"></a>
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
| B122 | Routine language C | O |
| B123 | Routine language COBOL | X |
| B124 | Routine language Fortran | X |
| B125 | Routine language MUMPS | X |
| B126 | Routine language Pascal | X |
| B127 | Routine language PL/I | X |
| B128 | Routine language SQL | O |
| B129 | Routine language Ada: VARCHAR and NUMERIC support | X |

<a id="fe9d4146fd8822ba"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [DROP PROCEDURE](#47bed13ab733e3a0)
- [ALTER PROCEDURE](#fedcce74e6accc1d)

<a id="c36270132fc5138d"></a>
## CREATE TRIGGER

<a id="a0c296267a429a6f"></a>
### 기능

Trigger를 생성한다.

<a id="a7a4cf4effae0956"></a>
### 구문

```
<create trigger statement> ::=
      CREATE [ OR REPLACE ] TRIGGER <trigger name>
      <trigger action time>
      <trigger event list> ON <table name>
      [ REFERENCING <transition table or variable list> ]
      <triggered action>
      ;

<trigger action time> ::=
        BEFORE 
      | AFTER

<trigger event list> ::=
      <trigger event> [ OR <trigger event> [ ... ] ]

<trigger event> ::=
        INSERT
      | DELETE
      | UPDATE [ OF <trigger column list> ]

<trigger column list> ::=
      <column name list> 

<column name list> ::=
     <column name> [ { <comma> <column name> }... ]

<transition table or variable list> ::=
        OLD [ ROW ] [ AS ] <old transition variable name>
      | NEW [ ROW ] [ AS ] <new transition variable name>
      | OLD TABLE [ AS ] <old transition table name>
      | NEW TABLE [ AS ] <new transition table name>

<triggered action> ::=
        [ FOR EACH { ROW | STATEMENT } ]
        [ <trigger enforcement> ]
        [ <triggered when clause> ]
        <trigger body>

<trigger enforcement> ::=
        ENABLE
      | DISABLE
      | ENFORCED
      | NOT ENFORCED

<triggered when clause> ::=
      WHEN <left paren> <search condition> <right paren>

<trigger body> ::= 
        <PSM block>
      | CALL <procedure name>
```

<a id="76259fecc15a5970"></a>
### 사용 범위 및 접근 권한

&lt;create trigger statement&gt; 구문을 수행하려면  사용자가 다음 조건들을 만족해야 한다.

- Trigger를 생성하려면 다음 권한 중 하나가 있어야 한다.
    - Trigger가 속한 스키마에 대해 (CREATE TRIGGER 또는 CONTROL SCHEMA) ON SCHEMA
    - CREATE ANY TRIGGER ON DATABASE
- OR REPLACE 절을 사용할 때 이미 trigger가 존재할 경우, 기존 trigger를 제거할 수 있는 다음 권한 중 하나가 있어야 한다.
    - 해당 trigger의 소유자
    - Trigger가 속한 스키마에 대해 (DROP TRIGGER 또는 CONTROL SCHEMA) ON SCHEMA
    - DROP ANY TRIGGER ON DATABASE
- Trigger는 table에 대해 TRIGGER 권한이 있어야 한다.
    - 구문을 수행한 사용자는 생성한 trigger의 소유자이다.

<a id="c843d1b3204df277"></a>
### 구문 규칙 및 파라미터

<a id="4358b9d7c1aa18b9"></a>
#### OR REPLACE

기존에 동일한 trigger가 존재할 경우, 기존 trigger를 새로운 trigger로 대체한다.

<a id="d589702ef8bf8466"></a>
#### &lt;trigger name&gt;

생성할 trigger의 이름으로서, 스키마 내에서 고유해야 한다.  
schema_name.trigger_name과 같이 trigger가 속할 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
Trigger 이름의 길이는 128 바이트보다 작아야 한다.

<a id="9bec3f2da4a22509"></a>
#### &lt;trigger action time&gt;

Trigger가 수행되는 시점을 정의한다.

- BEFORE
    - DML이 수행되기 전에 trigger가 수행된다.
- AFTER
    - DML을 수행한 후에 trigger가 수행된다.

<a id="67799c1f20fc61a3"></a>
#### &lt;trigger event&gt;

Event table에서 발생한 DML에 따라 trigger 실행 여부를 결정한다.  
하나 이상의 &lt;trigger event&gt;를 지정할 수 있다.  
동일한 &lt;trigger event&gt;를 중복해서 지정할 수 없다.

&lt;trigger event&gt;의 종류는 다음과 같다.

- INSERT
    - 지정된 event table에서 INSERT 문이 수행되면 trigger가 실행된다.
- UPDATE [ OF &lt;trigger column list&gt; ]
    - 지정된 event table에서 UPDATE 문이 수행되면 trigger가 실행된다.
    - OF &lt;trigger column list&gt;를 지정하면, 명시된 column이 UPDATE 될 때만 trigger가 실행된다.
- DELETE
    - 지정된 event table에서 DELETE 문이 수행되면 trigger가 실행된다.

<a id="05039cdbb4733301"></a>
#### &lt;trigger column list&gt;

지정된 특정 column이 UPDATE 될 때만 trigger가 실행되도록 설정하는 구문이다.  
Column 이름은 중복해서 지정할 수 없다.  
명시된 모든 column은 event table에 실제로 존재해야 한다.

<a id="303038f7be18002c"></a>
#### &lt;table name&gt;

Trigger가 감지할 DML 이벤트의 대상이 되는 base table 객체의 이름이다.  
Base table 이름에는 schema_name.table_name과 같이 스키마 이름을 지정할 수 있다.  
스키마 이름을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름을 사용한다.

<a id="9500b8779a7cc92c"></a>
#### REFERENCING &lt;transition table or variable list&gt;

REFERENCING transition table과 transition variable은 trigger에서 DML 수행 전후의 데이터를 참조하기 위해 사용된다.

REFERENCING 구문 뒤에는 다음과 같이 선언할 수 있으며, 중복 선언은 허용되지 않는다.

- OLD transition table
    - UPDATE 또는 DELETE가 수행되기 이전의 원본 데이터를 참조할 수 있는 임시 테이블이다.
- NEW transition table
    - INSERT 또는 UPDATE가 수행된 이후의 새로운 데이터를 참조할 수 있는 임시 테이블이다.
- OLD transition variable
    - UPDATE 또는 DELETE가 수행되기 이전의 개별 row 데이터를 참조할 수 있는 변수이다.
- NEW transition variable
    - INSERT 또는 UPDATE가 수행된 이후의 개별 row 데이터를 참조할 수 있는 변수이다.

OLD transition table, NEW transition table, OLD transition variable, NEW transition variable 이름은 중복해서 지정할 수 없다.  
사용자가 선언한 transition table 또는 transition varible은 &lt;triggered action&gt; 내에서만 사용할 수 있다.

- Transition table
    - DML 수행으로 변경된 row들의 집합을 table 형태로 제공한다.
    - BEFORE trigger에서는 선언할 수 없다.
    - 다중 이벤트 trigger에서는 선언할 수 없다.
- Transition variable
    - Statement trigger에서는 선언할 수 없다.
    - &lt;trigger event&gt;가 INSERT인 trigger에서는 OLD transition variable을 선언할 수 없다.
    - &lt;trigger event&gt;가 DELETE인 trigger에서는 NEW transition variable을 선언할 수 없다.
    - INSERT를 포함하는 다중 이벤트 trigger에서 INSERT 실행으로 trigger가 발생하는 경우, OLD transition variable은 NULL이다.
    - DELETE를 포함하는 다중 이벤트 trigger에서 DELETE 실행으로 trigger가 발생하는 경우, NEW transition variable은 NULL이다.

<a id="695127ac610b44bd"></a>
#### FOR EACH ROW/ FOR EACH STATEMENT

Trigger의 실행 단위를 지정한다.  
별도로 지정하지 않으면, 기본적으로 FOR EACH STATEMENT로 동작한다.

- FOR EACH ROW
    - DML 실행에 영향을 받은 각 row 마다 실행된다.
- FOR EACH STATEMENT
    - DML이 실행될 때 한 번만 실행된다.

<a id="66499016d89f7fc5"></a>
#### &lt;trigger enforcement&gt;

Trigger를 활성화된 상태로 생성할지, 비활성화된 상태로 생성할지를 지정한다.  
별도로 지정하지 않으면 trigger는 기본적으로 활성화된 상태로 생성된다.

ENABLE 과 ENFORCED 는 동일한 의미이다.  
DISABLE 과 NOT ENFORCED 는 동일한 의미이다.

- ENABLE
    - Event table에서 DML이 발생할 경우 trigger를 활성화한다.
    - DML event 발생 시 trigger가 실행된다.
- DISABLE
    - Event table에서 DML이 발생할 경우, trigger를 비활성화한다.
    - DML event 발생 시 trigger가 실행되지 않는다.

<a id="a768c4bde926a4a1"></a>
#### &lt;triggered when clause&gt;

Trigger 실행 여부를 제어하는 조건절을 지정한다.

&lt;triggered when clause&gt;의 결과가 true이면 trigger가 실행되고, false이면 실행되지 않는다.  
&lt;triggered when clause&gt;를 지정하지 않으면 trigger는 항상 실행된다.

&lt;triggered when clause&gt;의 expression에서 function을 사용할 수 있으나, 해당 function은 MODIFIES SQL DATA 속성을 가져서는 안 된다.

<a id="9e6014df244637a9"></a>
#### &lt;trigger body&gt;

Trigger가 실행할 구문을 정의한다.  
이는 PSM block 또는 CALL 구문으로 구성된다.

<a id="ac9a2acd5dbe6c5b"></a>
### 설명

Trigger를 정의하면, 지정된 base table에서 DML event가 발생할 때 해당 trigger가 실행된다.  
Trigger의 정의는 INFORMATION_SCHEMA의 TRIGGERS 테이블에서 확인할 수 있다.

관련 객체가 변경되어 trigger가 invalid 상태가 된 경우, ALTER TRIGGER .. COMPILE 구문을 사용하여 recompile 할 수 있다.

또한, ALTER TRIGGER .. RENAME 구문을 통해 생성된 trigger의 이름을 변경할 수 있다.

아래 구문을 실행하여 trigger의 활성화 상태를 변경할 수 있다.

- ALTER TRIGGER .. ENABLE
- ALTER TRIGGER .. ENFORCED
    - Trigger를 활성화 상태로 변경한다.
- ALTER TRIGGER .. DISABLE
- ALTER TRIGGER .. NOT ENFORCED
    - Trigger를 비활성화 상태로 변경한다.

생성된 trigger는 DROP TRIGGER 구문을 사용하여 제거할 수 있다.  
또한, event table 객체가 제거되면 해당 trigger도 함께 제거된다.

<a id="5608718fd14d6648"></a>
### 사용 예

- Trigger 생성 및 실행 예
    - Table 생성

```
-- 시스템 로그 테이블
gSQL>
CREATE TABLE system_log( log_time   DATE,
                         action     VARCHAR2(100),
                         table_name VARCHAR2(50) );

Table created.

-- 주문 상태 이력 테이블
gSQL>
CREATE TABLE order_status_history( order_id   NUMBER,
                                   old_status VARCHAR2(20),
                                   new_status VARCHAR2(20),
                                   changed_at DATE );

Table created.

-- 관리자 알림 테이블
gSQL>
CREATE TABLE admin_notifications( message    VARCHAR2(200),
                                  created_at DATE );

Table created.

-- ORDERS 테이블
gSQL>
CREATE TABLE orders( order_id    NUMBER PRIMARY KEY,
                     customer_id NUMBER,
                     amount      NUMBER,
                     status      VARCHAR2(20),
                     created_at  DATE,
                     updated_at  DATE );

Table created.
```

    - Trigger 생성

```
-- DML 시도 logging
gSQL>
CREATE OR REPLACE TRIGGER trg_orders_check_before_stmt
BEFORE INSERT OR UPDATE OR DELETE ON orders
DECLARE 
  dml_event VARCHAR(10);
BEGIN
  IF INSERTING THEN
    dml_event := 'INSERT';
  END IF;

  IF UPDATING THEN
    dml_event := 'UPDATE';
  END IF;

  IF DELETING THEN
    dml_event := 'DELETE';
  END IF;

  INSERT INTO system_log VALUES( SYSDATE, dml_event, 'ORDERS' );
END;
/

Trigger created.

-- INSERT 시 created_at 자동 설정
gSQL>
CREATE OR REPLACE TRIGGER trg_orders_set_created_at
BEFORE INSERT ON orders
REFERENCING NEW ROW AS n_row
FOR EACH ROW
BEGIN
  n_row.created_at := NVL(n_row.created_at, SYSDATE);
END;
/

Trigger created.

-- 상태 변경 시 이력 저장
gSQL>
CREATE OR REPLACE TRIGGER trg_orders_status_audit
AFTER UPDATE OF status ON orders
REFERENCING OLD ROW AS o_row
            NEW ROW AS n_row            
FOR EACH ROW
WHEN( o_row.status IS DISTINCT FROM n_row.status )
BEGIN
  INSERT INTO order_status_history VALUES (o_row.order_id, o_row.status, n_row.status, SYSDATE);
END;
/

Trigger created.

-- 상태 변경 후 알림
gSQL> 
CREATE OR REPLACE TRIGGER trg_orders_bulk_update_log
AFTER UPDATE ON orders
BEGIN
  INSERT INTO admin_notifications VALUES ('Order status in the ORDERS table has been updated.', SYSDATE);
END;
/

Trigger created.
```

    - DML 수행

```
-- INSERT 시 BEFORE STATEMENT, BEFORE ROW 트리거 동작
gSQL> 
INSERT INTO orders (order_id, customer_id, amount, status)
VALUES (1, 1001, 50000, 'Order Received ');

1 row created.

gSQL> SELECT * FROM system_log;

LOG_TIME   ACTION TABLE_NAME
---------- ------ ----------
2025-08-08 INSERT ORDERS    

1 row selected.
  
gSQL> SELECT * FROM orders;

ORDER_ID CUSTOMER_ID AMOUNT STATUS          CREATED_AT UPDATED_AT
-------- ----------- ------ --------------- ---------- ----------
       1        1001  50000 Order Received  2025-08-13 null       

1 row selected.

-- UPDATE 시 BEFORE STATEMENT, AFTER ROW, AFTER STATEMENT 트리거 동작
gSQL> 
UPDATE orders
   SET status = 'Shipped', updated_at = SYSDATE
 WHERE order_id = 1;

1 row updated.

gSQL> SELECT * FROM system_log;

LOG_TIME   ACTION TABLE_NAME
---------- ------ ----------
2025-08-08 INSERT ORDERS    
2025-08-08 UPDATE ORDERS    

2 rows selected.

gSQL> SELECT * FROM order_status_history;

ORDER_ID OLD_STATUS      NEW_STATUS CHANGED_AT
-------- --------------- ---------- ----------
       1 Order Received  Shipped    2025-08-13

1 row selected.

gSQL> SELECT * FROM admin_notifications;

MESSAGE                                            CREATED_AT
-------------------------------------------------- ----------
Order status in the ORDERS table has been updated. 2025-08-13

1 row selected.

gSQL> SELECT * FROM orders;

ORDER_ID CUSTOMER_ID AMOUNT STATUS  CREATED_AT UPDATED_AT
-------- ----------- ------ ------- ---------- ----------
       1        1001  50000 Shipped 2025-08-13 2025-08-13

1 row selected.
```

- &lt;trigger body&gt; 에 CALL 구문을 사용한 예
    - Table 생성

```
gSQL>
CREATE TABLE employees( emp_id NUMBER PRIMARY KEY,
                        name   VARCHAR2(50),
                        salary NUMBER );

Table created.

gSQL> INSERT INTO employees VALUES (1001, 'Alice', 5000);

1 row created.

gSQL> INSERT INTO employees VALUES (1002, 'Bob', 6000);

1 row created.

gSQL> COMMIT;

Commit complete.

gSQL>
CREATE TABLE audit_log( EMP_ID     NUMBER,
                        OLD_SALARY NUMBER,
                        NEW_SALARY NUMBER,
                        CHANGED_AT TIMESTAMP );

Table created.
```

    - Procedure 및 trigger 생성

```
gSQL>
CREATE OR REPLACE PROCEDURE log_salary_change(
		 p_emp_id     IN NUMBER,
         p_old_salary IN NUMBER,
         p_new_salary IN NUMBER )
AS
BEGIN
  INSERT INTO audit_log VALUES( p_emp_id,
                                p_old_salary,
                                p_new_salary,
                                SYSTIMESTAMP );
END;
/

Procedure created.

gSQL>
CREATE OR REPLACE TRIGGER trg_log_salary_change
AFTER UPDATE OF salary ON employees
REFERENCING OLD ROW AS o_row
            NEW ROW AS n_row
FOR EACH ROW
CALL log_salary_change( o_row.emp_id, o_row.salary, n_row.salary );
/

Trigger created.
```

    - DML 수행

```
gSQL>
UPDATE employees
   SET salary = 5500
 WHERE emp_id = 1001;

1 row updated.

gSQL> SELECT * FROM audit_log;

EMP_ID OLD_SALARY NEW_SALARY CHANGED_AT                
------ ---------- ---------- --------------------------
  1001       5000       5500 2025-08-08 17:21:35.522820

1 row selected.
```

- &lt;triggered when clause&gt; 사용 예
    - Table 생성

```
gSQL>
CREATE TABLE employees( emp_id INTEGER PRIMARY KEY,
                        name   VARCHAR(100),
                        salary INTEGER );

Table created.

gSQL> INSERT INTO employees VALUES( 101, 'Alice', 8000 );

1 row created.

gSQL> COMMIT;

Commit complete.

gSQL>
CREATE TABLE salary_log( emp_id     INTEGER,
                         old_salary INTEGER, 
                         new_salary INTEGER,
                         log_time   TIMESTAMP );

Table created.

gSQL> COMMIT;

Commit complete.
```

    - Trigger 생성

```
gSQL>
CREATE OR REPLACE TRIGGER trg_log_high_salary
AFTER UPDATE ON employees
REFERENCING OLD ROW AS o_row 
            NEW ROW AS n_row
FOR EACH ROW
WHEN( n_row.salary >= 10000 AND n_row.salary > o_row.salary )
BEGIN
  INSERT INTO salary_log VALUES( o_row.emp_id,
                                 o_row.salary,
                                 n_row.salary,
                                 CURRENT_TIMESTAMP );
END;
/

Trigger created.
```

    - DML 수행 시 trigger 동작

```
-- WHEN 절 조건을 만족하지 않는 경우 → Trigger 본문이 실행되지 않음
gSQL> UPDATE employees SET salary = 9000;

1 row updated.

gSQL> SELECT * FROM salary_log;

no rows selected.
```

```
-- WHEN 절 조건을 만족하는 경우 → Trigger 본문이 실행됨
gSQL> UPDATE employees SET salary = 12000;

1 row updated.

gSQL> SELECT * FROM salary_log;

EMP_ID OLD_SALARY NEW_SALARY LOG_TIME                  
------ ---------- ---------- --------------------------
   101       8000      12000 2025-08-08 17:39:38.391413

1 row selected.
```

<a id="18c04e92cf4b3c7f"></a>
### 호환성

**SQL 표준 호환성**

<a id="95ed281934a71530"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T200 | Trigger DDL | O |
| T211 | Basic trigger capability | O |
| T212 | Enhanced trigger capability | O |
| T213 | INSTEAD OF triggers | X |
| T214 | BEFORE triggers | O |
| T215 | AFTER triggers | O |
| T216 | Ability to require true search condition before trigger is invoked | O |
| T217 | TRIGGER privilege | O |
| T218 | Multiple triggers for the same event executed in the order created | O |

<a id="0ae64b63c3189659"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [ALTER TRIGGER name COMPILE](#7ef86e0333181a4e)
- [ALTER TRIGGER name ENABLE/DISABLE](#f14d8e926a633165)
- [ALTER TRIGGER name RENAME TO](#ae1a37f358aeb5db)
- [ALTER TABLE name SET TRIGGER ORDER](../part-03-sql-manual/18-sql-references-a-b.md#e99539acedd7cb13)
- [DROP TRIGGER](#405a8fa6b4a11ae3)
- [DROP TABLE](../part-03-sql-manual/19-sql-references-c-g.md#cdb39a166c5e9daf)

<a id="799b77ea31fecf81"></a>
## DROP FUNCTION

<a id="9ab89b689647b701"></a>
### 기능

Function을 제거한다.

<a id="0f6670e4c8dcbaea"></a>
### 구문

```
<drop function statement> ::=
    DROP FUNCTION [ IF EXISTS ] func_name
    ;
```

<a id="4565253abab1900f"></a>
### 사용 범위 및 접근 권한

&lt;drop function statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 function의 소유자
- Function이 속한 스키마에 대해 (DROP PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY PROCEDURE ON DATABASE

<a id="06165b6c1b257465"></a>
### 구문 규칙 및 파라미터

<a id="d70ae2a2cab6e4b8"></a>
#### IF EXISTS

Function이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="40ae1bc56f0a0595"></a>
#### FUNC NAME

제거할 function의 이름이다.   
schema_name.func_name과 같이 function이 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="5e5e8e3cdb2ce216"></a>
### 설명

지정된 schema-level function을 제거한다.

<a id="3ba2aab702d1c56f"></a>
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

<a id="964645d18f1fbc0d"></a>
### 호환성

SQL 표준은 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="e37605e1cfa49316"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="215cfc6200311777"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE FUNCTION](#8f6d3c41338c889a)
- [ALTER FUNCTION](#69bb017860d2aedf)

<a id="11be420b5d5517c9"></a>
## DROP LIBRARY

<a id="04bebf341867f6c3"></a>
### 기능

Library를 제거한다.

<a id="cc1b5c82db8b9853"></a>
### 구문

```
<drop library statement> ::=
    DROP LIBRARY [ IF EXISTS ] <library name>
    ;
```

<a id="4e554605513b2469"></a>
### 사용 범위 및 접근 권한

&lt;drop library statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 library의 소유자
- library가 속한 스키마에 대해 DROP LIBRARY ON SCHEMA 또는 CONTROL SCHEMA ON SCHEMA
- DROP ANY LIBRARY ON DATABASE

<a id="fd27f41d42b568c8"></a>
### 구문 규칙 및 파라미터

<a id="1518d80b873a3781"></a>
#### IF EXISTS

Library가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="36d0b2c6c0cb4ed7"></a>
#### library name

제거할 library의 이름이다.  
&lt;schema name&gt;.&lt;library name&gt;과 같이 library가 속한 스키마를 정의할 수 있다.  
&lt;schema name&gt;을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="8b626e784309e97e"></a>
### 설명

지정된 library를 제거한다.

<a id="72bab769ca95ed47"></a>
### 사용 예

```
gSQL>
CREATE LIBRARY lib1 AS 'add.so';
/

Library created.

gSQL> DROP LIBRARY lib1;

Library dropped.

gSQL> DROP LIBRARY IF EXISTS lib2;

Library dropped.
```

<a id="084dba7823797724"></a>
### 호환성

SQL 표준에 정의되어 있지 않다.

<a id="8bb5b7e5934b5671"></a>
### 참조

자세한 내용은 [CREATE LIBRARY](#e6a29c79119e1af1)를 참조한다.

<a id="561079b3305fcaea"></a>
## DROP PACKAGE

<a id="0aeb131718f5fb31"></a>
### 기능

Package (body만 또는 spec/ body 모두)를 제거한다.

<a id="402f879679c87187"></a>
### 구문

```
<drop package statement> ::=
    DROP PACKAGE [BODY] [ IF EXISTS ] package_name
    ;
```

<a id="966898513f7da622"></a>
### 사용 범위 및 접근 권한

&lt;drop package statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 package의 소유자 
- Package가 속한 스키마에 대해 (DROP PACKAGE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY PACKAGE ON DATABASE

<a id="5e19297b20be2456"></a>
### 구문 규칙 및 파라미터

<a id="7c51aa94d591d6b2"></a>
#### BODY

주어진 이름을 가진 package의 body 객체만 제거한다. *BODY* 라는 키워드를 명시하지 않은 경우 package specification과 body를 모두 삭제한다.

<a id="07f0f9c64a561890"></a>
#### IF EXISTS

Package가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="1b2d3a92c5b63813"></a>
#### PACKAGE NAME

제거할 package의 이름이다.   
schema_name.package_name 과 같이 package가 소속한 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="9a5b52ca190834f0"></a>
### 설명

지정된 package object를 제거한다.

<a id="6d6cbb35746acca1"></a>
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

<a id="cefbb985f7c306f1"></a>
### 호환성

SQL 표준에서는 DRO MODULE 구문이다.

<a id="4a711c883e1ecd40"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PACKAGE](#5f9bdd6eb052f51f)
- [CREATE PACKAGE BODY](#4af32611ea712290)
- [ALTER PACKAGE](#9412a5205d4edae2)

<a id="47bed13ab733e3a0"></a>
## DROP PROCEDURE

<a id="ad6a4020ed2de224"></a>
### 기능

Procedure를 제거한다.

<a id="4b1aad31303bfed2"></a>
### 구문

```
<drop procedure statement> ::=
    DROP PROCEDURE [ IF EXISTS ] proc_name
    ;
```

<a id="e8e9913915dad244"></a>
### 사용 범위 및 접근 권한

&lt;drop procedure statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 procedure의 소유자
- Procedure가 속한 스키마에 대해 (DROP PROCEDURE 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY PROCEDURE ON DATABASE

<a id="26c7b4ce7acdcc72"></a>
### 구문 규칙 및 파라미터

<a id="528c2176b291bafa"></a>
#### IF EXISTS

Procedure가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="a935aea7e6d9bd07"></a>
#### PROC NAME

제거할 procedure의 이름이다.   
schema_name.proc_name과 같이 procedure가 속한 스키마를 정의할 수 있다. schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="771524310eaebf15"></a>
### 설명

지정된 schema-level procedure를 제거한다.

<a id="23ad906f3eacba66"></a>
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

<a id="9be51cf36e5cbca5"></a>
### 호환성

SQL 표준은 다음과 같은 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="dbd2b53f9fede051"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |
| S024 | Enhanced structured types | X |

<a id="dbe0138c7e50d0ea"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE PROCEDURE](#48b6178f1f6cd4cb)
- [ALTER PROCEDURE](#fedcce74e6accc1d)

<a id="405a8fa6b4a11ae3"></a>
## DROP TRIGGER

<a id="f3c0f791a5caf7d4"></a>
### 기능

Trigger를 제거한다.

<a id="96a8b07465794757"></a>
### 구문

```
<drop trigger statement> ::=
    DROP TRIGGER [ IF EXISTS ] <trigger name>
    ;
```

<a id="e0d2d1c8cd2d346c"></a>
### 사용 범위 및 접근 권한

&lt;drop trigger statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 trigger의 소유자
- Trigger가 속한 스키마에 대해 (DROP TRIGGER 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY TRIGGER ON DATABASE

<a id="d018325aebce36a5"></a>
### 구문 규칙 및 파라미터

<a id="8a3c3f2cee0b382b"></a>
#### IF EXISTS

Trigger가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="09d4987f926ec611"></a>
#### &lt;trigger name&gt;

제거할 trigger 이름이다.  
schema_name.trigger_name과 같이 trigger가 속한 스키마를 정의할 수 있다.  
schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="8f62fc21a08b6d64"></a>
### 설명

명시된 trigger를 제거한다.  
또한, [DROP TABLE](../part-03-sql-manual/19-sql-references-c-g.md#cdb39a166c5e9daf)로 event table이 제거되면 해당 trigger도 함께 제거된다.

<a id="4394741cfa7fe90e"></a>
### 사용 예

```
gSQL>
CREATE OR REPLACE TRIGGER trg_orders_status_audit
AFTER UPDATE OF status ON orders
REFERENCING OLD ROW AS o_row
            NEW ROW AS n_row            
FOR EACH ROW
WHEN( o_row.status IS DISTINCT FROM n_row.status )
BEGIN
  INSERT INTO order_status_history VALUES (o_row.order_id, o_row.status, n_row.status, SYSDATE);
END;
/

Trigger created.

gSQL> DROP TRIGGER trg_orders_status_audit;

Trigger dropped.
```

<a id="1b0b9be92438ebc4"></a>
### 호환성

**SQL 표준 호환성**

<a id="070c77b42c49db85"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T200 | Trigger DDL | O |

<a id="cdcb3812e462eae0"></a>
### 참조

자세한 내용은 다음을 참조한다.

- [CREATE TRIGGER](#c36270132fc5138d)
- [ALTER TRIGGER name COMPILE](#7ef86e0333181a4e)
- [ALTER TRIGGER name ENABLE/DISABLE](#f14d8e926a633165)
- [ALTER TRIGGER name RENAME TO](#ae1a37f358aeb5db)
- [DROP TABLE](../part-03-sql-manual/19-sql-references-c-g.md#cdb39a166c5e9daf)

---

[← 30. PSM Language Element References](30-psm-language-element-references.md) · [전체 목차](../README.md) · [32. Built-in Package →](32-built-in-package.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
