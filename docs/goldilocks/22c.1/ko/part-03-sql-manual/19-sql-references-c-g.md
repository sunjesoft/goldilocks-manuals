<a id="015ea2ab23f76892"></a>

# 19. SQL References (C~G)

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/015ea2ab23f76892)  
> 태그: `22c.1_10_tag`

[← 18. SQL References (A~B)](18-sql-references-a-b.md) · [전체 목차](../README.md) · [20. SQL References (H~Z) →](20-sql-references-h-z.md)

<a id="b130e0aa9376fe9d"></a>
## CLOSE cursor_name

<a id="af51e736b9e00b75"></a>
### 기능

커서를 닫는다.

<a id="f660a44d94d014e5"></a>
### 구문

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="3a122169cd6c46b1"></a>
### 구문 규칙 및 파라미터

<a id="6e8cd17c12f380b5"></a>
#### cursor_name

커서가 open 되어 있어야 한다.  
세션 내에서 [DECLARE cursor_name](#f94895843614f7cc) 구문으로 선언된 커서이어야 한다.

<a id="42db221bb354d408"></a>
### 설명

Cursor는 session 내에 존재하는 객체이고 서로 다른 session의 cursor에 영향을 주지 않는다.

<a id="01b32b1df4cbb62d"></a>
### 사용 예

다음은 interactive SQL tool (gsql)을 사용하여 커서를 DECLARE, OPEN, FETCH, CLOSE 하는 예이다.

```
gSQL> DECLARE cur1 CURSOR FOR SELECT id, data FROM t1;

Cursor declared.

gSQL> OPEN cur1;

Cursor is open.

gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.


gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   2 data_2

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

no rows fetched.

gSQL> CLOSE cur1;

Cursor closed.
```

<a id="2a8af108d52a9f40"></a>
### 호환성

**SQL 표준 호환성**

<a id="863aceb009ccb809"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic dynamic SQL | O |

<a id="94ecc0c2438879cd"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#f94895843614f7cc)
- [OPEN cursor_name](20-sql-references-h-z.md#afdd7cb54cc78da0)
- [FETCH cursor_name](#47babe65e4397c2a)

<a id="7db59ad470875e46"></a>
## COMMENT ON name IS

<a id="97755484f727bdad"></a>
### 기능

객체에 대한 설명을 dictionary에 저장한다.

<a id="dc01b0d9c2033553"></a>
### 구문

```
<comment statement> ::=
    COMMENT ON <comment object> IS 'comment string'
    ;

<comment object> ::=
      CLUSTER GROUP group_name
    | CLUSTER MEMBER member_name
    | DATABASE
    | PROFILE profile_name
    | AUDIT POLICY policy_name
    | AUTHORIZATION user_name
    | TABLESPACE tablespace_name
    | SCHEMA schema_name
    | TABLE [schema_name].table_name
    | COLUMN [schema_name].table_name.column_name
    | INDEX [schema_name].index_name
    | SEQUENCE [schema_name].sequence_name
    | CONSTRAINT [schema_name].constraint_name
    | PROCEDURE [schema_name].procedure_name
```

<a id="e4ae12d6245fe4ff"></a>
### 사용 범위 및 접근 권한

&lt;comment statement&gt; 구문을 수행하려면 각 객체에 대하여 다음과 같이 권한을 변경해야 한다.

- CLUSTER GROUP
    - ALTER SYSTEM ON DATABASE
- CLUSTER MEMBER
    - ALTER SYSTEM ON DATABASE
- DATABASE 
    - ALTER DATABASE ON DATABASE 
- PROFILE
    - ALTER PROFILE ON DATABASE
- AUDIT POLICY
    - AUDIT SYSTEM ON DATABASE
- AUTHORIZATION (user) 
    - ALTER USER ON DATABASE 
- AUTHORIZATION (role) 
    - ALTER ROLE ON DATABASE 
- TABLESPACE 
    - ALTER TABLESPACE ON DATABASE 
- SCHEMA: 다음 권한 중 하나가 있어야 한다. 
    - 스키마의 소유자 
    - 스키마에 대해 CONTROL SCHEMA ON SCHEMA 
    - ALTER SCHEMA ON DATABASE 
- TABLE: 다음 권한 중 하나가 있어야 한다. 
    - 테이블의 소유자 
    - 테이블에 대해 CONTROL TABLE ON TABLE 
    - 테이블이 속한 스키마에 대해 CONTROL SCHEMA ON SCHEMA 
    - ALTER ANY TABLE ON DATABASE 
- COLUMN: 다음 권한 중 하나가 있어야 한다. 
    - Column이 속한 테이블의 소유자 
    - Column이 속한 테이블에 대해 CONTROL TABLE ON TABLE 
    - Column이 속한 테이블의 스키마에 대해 CONTROL SCHEMA ON SCHEMA 
    - ALTER ANY TABLE ON DATABASE 
- INDEX: 다음 권한 중 하나가 있어야 한다. 
    - 인덱스의 소유자 
    - 인덱스가 속한 스키마에 대해 CONTROL SCHEMA ON SCHEMA 
    - ALTER ANY INDEX ON DATABASE 
- SEQUENCE 
    - 시퀀스의 소유자 
    - 시퀀스가 속한 스키마에 대해 CONTROL SCHEMA ON SCHEMA 
    - ALTER ANY SEQUENCE ON DATABASE 
- CONSTRAINT 
    - 제약 조건의 소유자 
    - 제약 조건이 속한 스키마에 대해 CONTROL SCHEMA ON SCHEMA 
    - ALTER ANY TABLE ON DATABASE
- PROCEDURE
    - Stored procedure/ function 의 소유자
    - Stored procedure/ function 이 속한 스키마에 대해 CONTROL SCHEMA ON SCHEMA
    - ALTER ANY PROCEDURE ON DATABASE

<a id="a84da72a22065392"></a>
### 구문 규칙 및 파라미터

<a id="2ae19d03f80f678e"></a>
#### &lt;comment object&gt;

설명을 저장할 대상 객체로써 다음과 같은 database 객체에 대한 comment를 저장할 수 있다.

- Cluster object
    - CLUSTER GROUP
    - CLUSTER MEMBER 
- Non-schema object 
    - DATABASE 
    - PROFILE
    - AUDIT POLICY
    - AUTHORIZATION (User or Role) 
    - TABLESPACE 
    - SCHEMA 
- Schema object 
    - TABLE 또는 VIEW 
    - COLUMN 
    - INDEX 
    - SEQUENCE 
    - CONSTRAINT
    - PROCEDURE 또는 FUNCTION

Schema object의 경우 schema_name을 기술하지 않으면 구문을 수행하는 사용자의 [Schema Path](13-sql-objects.md#b122e879a44d92f6)에 의해 스키마 이름이 결정된다.

```
COMMENT ON TABLE test_table IS 'test comment'; 
→ COMMENT ON TABLE user_default_schema.test_table IS 'test comment';
```

<a id="aaf2b11d4310f60c"></a>
#### 'comment string'

저장할 comment 문장을 기술한다.   
Comment를 삭제하려면 다음과 같이 empty string ('')을 사용한다.

```
COMMENT ON TABLE test_table IS '';
```

comment string의 길이는 1024 bytes를 초과할 수 없다.

<a id="fac7e0885e3c4ef4"></a>
### 설명

다음 dictionary view의 COMMENTS column으로부터 객체 유형별 정보를 확인할 수 있다.

- Cluster objects
    - CLUSTER GROUP & CLUSTER MEMBER
        - DICTIONARY_SCHEMA.DBA_CLUSTER_COMMENTS view
- Non-schema objects
    - DATABASE
        - DICTIONARY_SCHEMA.ALL_NONSCHEMA_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_NONSCHEMA_COMMENTS view
    - PROFILE
        - DICTIONARY_SCHEMA.DBA_NONSCHEMA_COMMENTS view
    - AUDIT POLICY
        - DICTIONARY_SCHEMA.AUDIT_POLICIES view
    - USER
        - DICTIONARY_SCHEMA.ALL_NONSCHEMA_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_NONSCHEMA_COMMENTS view
    - TABLESPACE
        - DICTIONARY_SCHEMA.ALL_NONSCHEMA_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_NONSCHEMA_COMMENTS view
    - SCHEMA
        - DICTIONARY_SCHEMA.ALL_NONSCHEMA_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_NONSCHEMA_COMMENTS view
- SQL schema objects
    - TABLE
        - DICTIONARY_SCHEMA.USER_TAB_COMMENTS view
        - DICTIONARY_SCHEMA.ALL_TAB_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_TAB_COMMENTS view
    - VIEW
        - DICTIONARY_SCHEMA.USER_TAB_COMMENTS view
        - DICTIONARY_SCHEMA.ALL_TAB_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_TAB_COMMENTS view
    - COLUMN
        - DICTIONARY_SCHEMA.USER_COL_COMMENTS view
        - DICTIONARY_SCHEMA.ALL_COL_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_COL_COMMENTS view
    - INDEX
        - DICTIONARY_SCHEMA.USER_INDEXES view
        - DICTIONARY_SCHEMA.ALL_INDEXES view
        - DICTIONARY_SCHEMA.DBA_INDEXES view
    - SEQUENCE
        - DICTIONARY_SCHEMA.USER_SEQUENCES view
        - DICTIONARY_SCHEMA.ALL_SEQUENCES view
        - DICTIONARY_SCHEMA.DBA_SEQUENCES view
    - CONSTRAINT
        - DICTIONARY_SCHEMA.USER_CONSTRAINTS view
        - DICTIONARY_SCHEMA.ALL_CONSTRAINTS view
        - DICTIONARY_SCHEMA.DBA_CONSTRAINTS view
    - PROCEDURE & FUNCTION
        - DICTIONARY_SCHEMA.USER_PROCEDURES view
        - DICTIONARY_SCHEMA.ALL_PROCEDURES view
        - DICTIONARY_SCHEMA.DBA_PROCEDURES view

각 view에 대한 자세한 내용은 [DICTIONARY_SCHEMA](../part-02-administration-manual/9-database-information.md#2b3b5c7a34c5140e)를 참조한다.

<a id="7e98922f1255d5fb"></a>
### 사용 예

다음은 테이블에 주석을 작성하는 예이다.

```
gSQL> COMMENT ON TABLE t1 IS 'test comment on table t1';

Comment created.
```

다음은 column에 주석을 작성하는 예이다.

```
gSQL> COMMENT ON COLUMN t1.id IS 'test comment on column t1.id';

Comment created.
```

다음은 스키마에 주석을 작성하는 예이다.

```
gSQL> COMMENT ON SCHEMA s1 IS 'test comment on schema s1';

Comment created.
```

<a id="79639e67f5acbd30"></a>
### 호환성

SQL 표준에는 &lt;comment statement&gt;가 없다.

<a id="584ccbb69a281847"></a>
## COMMIT

<a id="89f1dac8fcff19c3"></a>
### 기능

현재 트랜잭션을 종료하고, 변경된 모든 내용을 영속화한다.

<a id="2a7cc9b1535f3e21"></a>
### 구문

```
<commit statement> ::=
    COMMIT [ WORK ] 
       [ [ <commit comment clause> ] [ <commit write clause> ] |
         [ <commit force clause> ] [ <commit comment clause> ] ]
    ;

<commit comment clause> ::=
      COMMENT 'comment_string'

<commit write clause> ::=
      WRITE [ WAIT | NOWAIT ]

<commit force clause> ::=
    FORCE 'xid_string'
```

<a id="906c255d25a49f2d"></a>
### 구문 규칙 및 파라미터

<a id="03cc02729d543616"></a>
#### WORK

동작에 영향을 미치지 않는 예약어이다.

<a id="4422419fe680c190"></a>
#### &lt;commit comment clause&gt;

- COMMENT 'comment_string'
    - 트랜잭션을 commit 할 때 트랜잭션에 주석을 지정한다.

<a id="ecd168863728a02f"></a>
#### &lt;commit write clause&gt;

Commit 연산으로 생성된 redo log가 redo log file에 기록될 때까지 기다릴지 여부를 결정한다.

- WAIT
    - commit 연산에 의해서 생성된 redo log가 redo log file에 기록될 때까지 기다린 후 연산을 종료한다.
- NOWAIT
    - commit 연산에 의해서 생성된 redo log가 redo log 버퍼에 기록되면 연산을 종료한다.
- 지정되어 있지 않을 경우, 프로퍼티를 따른다.

<a id="d52be75d621821e5"></a>
#### &lt;commit force clause&gt;

분산 트랜잭션을 수동으로 commit 할 때 사용한다.

- FORCE 'xid_string'
    - 'xid_string'에 해당하는 분산 트랜잭션을 commit 한다.
    - 'xid_string'은 '*format_id*.*transaction_id*.*branch_id*'로 구성된다.

<a id="240c2e894caa8520"></a>
### 설명

COMMIT 구문은 트랜잭션 내에서 수행된 다음 구문들을 완료한다.

- Data Manipulation Language (DML) 구문
    - 데이터를 변경하는 INSERT, UPDATE, DELETE 등의 구문
- Data Definition Language (DDL) 구문 
    - 객체의 구조 및 정의를 변경하는 CREATE, DROP, ALTER, TRUNCATE, GRANT, REVOKE 등의 구문

예외적으로, DDL 중에 OS 자원을 다루거나 DATA TYPE을 변경하는 다음 구문들은 자동으로 COMMIT 된다.

- [CREATE TABLESPACE](#c81940ba4a84752c)
- [DROP TABLESPACE](#0905e5b2ffc06135)
- [ALTER TABLESPACE](18-sql-references-a-b.md#e50680549a4cafe3)
- ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE: [&lt;alter column data type clause&gt;](18-sql-references-a-b.md#4756ff6c67f21ebc)

COMMIT을 수행하면 WITHOUT HOLD 옵션으로 열린 커서는 자동으로 닫힌다. 커서에 대한 자세한 내용은 다음의 커서 관련 구문을 참조한다.

- [DECLARE cursor_name](#f94895843614f7cc)
- [OPEN cursor_name](20-sql-references-h-z.md#afdd7cb54cc78da0)

트랜잭션이 지연된 (DEFERRED) 제약 조건을 위반하면 COMMIT 구문의 수행은 실패하고 트랜잭션은 ROLLBACK 된다. 지연된 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](20-sql-references-h-z.md#b39019fd3808ec13) 구문의 설명을 참조한다.

<a id="f833f92d983494ee"></a>
### 사용 예

다음은 INSERT 구문을 수행한 후에 COMMIT을 수행하는 예이다.

```
gSQL> INSERT INTO t1 VALUES ( 1, 'anonymous' );

1 row created.

gSQL> COMMIT WORK COMMENT 'INSERT T1';

Commit complete.
```

<a id="4b8e805057da2f52"></a>
### 호환성

**SQL 표준 호환성**

<a id="f0d6d6ad5abfe790"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T261 | Chained transactions | X |

<a id="20cd86a91c17579f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ROLLBACK](20-sql-references-h-z.md#6ca73e32555cc74b)
- [SAVEPOINT savepoint_specifier](20-sql-references-h-z.md#e01fdff113a62fc1)

<a id="ab7ff9504e3f6183"></a>
## CREATE AUDIT POLICY

<a id="a126d51f090b5444"></a>
### 기능

Audit policy 객체를 생성한다.   
생성한 audit policy 객체를 활성화하려면 AUDIT POLICY 구문을 수행하여야 한다.

<a id="98898d9e109ff3d5"></a>
### 구문

```
<audit policy definition> ::= 
    CREATE AUDIT POLICY policy_name
    { <privilege_audit_clause> |  <action_audit_clause> | <privilege_audit_clause> <action_audit_clause> }
    ; 

<privilege_audit_clause> ::=
    PRIVILEGES <database_privilege> [, ...]

<action_audit_clause> ::=
    ACTIONS { <object_action_audit> | <system_action_audit> } [, ...]

<object_action_audit> ::=
      ALL ON [schema_name.]object_name
    | <object_action> ON [schema_name.]object_name

<system_action_audit> ::=
      ALL
    | DDL
    | <system_action>
```

<a id="465aa0c4c124c318"></a>
### 사용 범위 및 접근 권한

&lt;audit policy definition&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="6174aa3edbe6ef70"></a>
### 구문 규칙 및 파라미터

<a id="87d30d014578c12a"></a>
#### policy_name

생성할 audit policy의 이름이다.

<a id="0d3bfa6c2229e96a"></a>
#### &lt;privilege_audit_clause&gt;

권한 감사는 database privilege를 이용해 SQL 구문을 성공적으로 수행한 경우를 감사한다.   
특정 사용자가 database privilege를 이용해 SQL 구문을 수행하는 것을 감사할 수 있으며, database의 소유자인 SYS 사용자에 대해서는 권한 감사 기록을 남기지 않는다.

다음은 u1 사용자에게 SELECT ANY TABLE 권한을 부여하고 audit policy를 활성화하는 예이다.

```
CREATE AUDIT POLICY p1 
       PRIVILEGES SELECT ANY TABLE;

AUDIT POLICY p1;
```

사용자 u1이 다음과 같은 SQL 구문을 수행할 경우 권한 감사가 다르게 동작한다.

- SELECT * FROM u1.t1;
    - u1.t1 테이블의 소유자 권한으로 SQL 구문을 수행하여 audit record를 생성하지 않는다.
- SELECT * FROM u2.t1;
    - SELECT ANY TABLE 권한으로 SQL 구문을 수행하여 audit record를 생성한다.

권한 감사에 기술할 수 있는 &lt;database_privilege&gt;는 다음 질의로 조회할 수 있다.

```
SELECT PRIVILEGE_NAME FROM V$AUDITABLE_DB_PRIVILEGES;
```

<a id="73b27c00205ff9cf"></a>
#### &lt;action_audit_clause&gt;

특정 객체에 대한 action과 database 전체에 대한 action을 감사한다.

<a id="721e08014057d13b"></a>
#### &lt;object_action_audit&gt;

<a id="b662d2f3c00d21d1"></a>
##### ALL ON object_name

object_name에 해당하는 객체에 대해 나열할 수 있는 모든 action을 의미한다.

각 객체 유형별로 감사할 수 있는 audit action은 다음 표와 같다.

**객체별 audit action**

<a id="b83fb376fb77d601"></a>
| Object type | Action |
| --- | --- |
| Table | ALTER, COMMENT, DELETE, GRANT, INDEX, INSERT, LOCK, RENAME, SELECT, UPDATE |
| View | ALTER, COMMENT, GRANT, SELECT |
| Sequence | ALTER, COMMENT, GRANT, SELECT |
| Stored function/  procedure | ALTER, COMMENT, EXECUTE, GRANT |

<a id="e35c8289a248361c"></a>
##### &lt;object_action&gt; ON object_name

특정 object에 대한 개별 action들은 다음과 같이 ON 절을 명시하여 하나씩 나열한다.

```
CREATE AUDIT POLICY p1
       ACTIONS INSERT ON u1.t1
             , DELETE ON u1.t1
             , UPDATE ON u1.t1
;
```

<a id="ea4f63b9395df8ed"></a>
##### EXECUTE action 유의 사항

Stored function이나 stored procedure의 EXECUTE action 성공, 실패 여부에 대한 감사는 실제 수행 시점의 수행 가능 여부만으로 판단한다.

- WHENEVER NOT SUCCESSFUL의 경우, stored function/ procedure를 수행할 수 없을 경우에 감사 레코드를 생성한다.
- WHENEVER SUCCESSFUL의 경우, stored function/ procedure 내부의 SQL 구문을 수행하는 중에 에러가 발생하더라도 감사 레코드를 생성한다.
- Stored function/ procedure 내부의 SQL 구문 실패에 대한 감사가 필요할 경우, 해당 SQL 구문을 감사 대상에 포함해야 한다.

<a id="94956be8627ace39"></a>
#### &lt;system_action_audit&gt;

특정 객체와 관계없이 database에 발생하는 system action을 감사한다.

- &lt;system_action&gt;

유효한 system action은 다음 질의로 조회할 수 있다.

```
SELECT ACTION_NAME FROM V$AUDITABLE_SYSTEM_ACTIONS;
```

- ALL

모든 system action을 의미한다.

- DDL

모든 Data Definition Language (DDL) 구문을 의미한다.

<a id="f37cf139243e484f"></a>
### 설명

Audit policy 객체는 감사할 대상들을 정의한 객체이다.    
Audit policy를 활성화하기 위해서는 AUDIT POLICY 구문을 수행해야 한다.

다수의 audit policy 를 정의하고 활성화할 수 있지만, 제한된 개수의 audit policy를 유지하는 것이 바람직하다.    
여러 개의 작은 policy 조각들을 묶어 소수의 policy group으로 만드는 것이 바람직하다.

생성한 audit policy 객체의 옵션 정보는 다음과 같이 AUDIT_POLICY_OPTIONS view를 통해 조회할 수 있다.

```
SELECT audit_option
     , audit_option_type
     , object_schema
     , object_name
  FROM audit_policy_options
 WHERE policy_name = 'P1'
;

AUDIT_OPTION AUDIT_OPTION_TYPE OBJECT_SCHEMA  OBJECT_NAME
------------ ----------------- -------------- ------------
DELETE	     OBJECT ACTION     U1	      T1
INSERT	     OBJECT ACTION     U1	      T1
UPDATE	     OBJECT ACTION     U1	      T1
```

<a id="3db96addd538fe84"></a>
#### Audit Record의 생성

여러 감사 조건에 부합하는 action이 발생할 경우, 한 개 이상의 audit record를 생성한다.

다음과 같이 유사한 audit option을 나열한 경우 하나의 audit record를 생성한다.

- Audit policy 정의

```
CREATE AUDIT POLICY p1
       PRIVILEGES SELECT ANY TABLE
       ACTIONS SELECT;

AUDIT POLICY p1;
```

- Audit action 수행

```
SELECT * FROM other_user.t1;
```

다음과 같이 서로 다른 audit option을 나열한 경우 두 개의 audit record를 생성한다.

- Audit policy 정의

```
CREATE AUDIT POLICY p1
       ACTIONS SELECT ON u1.t1
             , SELECT ON u2.t2;

AUDIT POLICY p1;
```

- Audit action 수행

```
SELECT COUNT(*) FROM u1.t1 A, u2.t2 B WHERE A.id = B.id;
```

다음과 같이 동일한 action에 대해 여러 audit policy를 활성화한 경우, 두 개의 audit record를 생성한다.

- Audit policy 정의

```
CREATE AUDIT POLICY p1
       PRIVILEGES SELECT ANY TABLE;
AUDIT POLICY p1;

CREATE AUDIT POLICY p2
       ACTIONS SELECT;
AUDIT POLICY p2;
```

- Audit action 수행

```
SELECT * FROM other.t1;
```

<a id="6d7b27ca6eb42064"></a>
### 사용 예

다음은 권한을 감사하는 audit policy를 정의하는 예이다.

```
CREATE AUDIT POLICY policy_table
       PRIVILEGES CREATE ANY TABLE
                , DROP ANY TABLE
;
```

다음은 객체에 대한 action을 감사하는 audit policy를 정의하는 예이다.

```
CREATE AUDIT POLICY policy_dml
       ACTIONS INSERT ON u1.t1
             , DELETE ON u1.t1
             , UPDATE ON u1.t1
             , ALL    ON u1.t2
;
```

다음은 system action을 감사하는 audit policy를 정의하는 예이다.

```
CREATE AUDIT POLICY policy_drop
       ACTIONS DROP TABLE, TRUNCATE TABLE
;
```

다음은 위의 예를 모두 합친 audit policy를 정의하는 예이다.

```
CREATE AUDIT POLICY policy_group
       PRIVILEGES CREATE ANY TABLE
                , DROP ANY TABLE
       ACTIONS INSERT ON u1.t1
             , DELETE ON u1.t1
             , UPDATE ON u1.t1
             , ALL    ON u1.t2
             , DROP TABLE
             , TRUNCATE TABLE
;
```

<a id="c8a35b0bd3f01e7c"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="9c921d9b8d129ba9"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#ab7ff9504e3f6183)
    - [DROP AUDIT POLICY](#69253535ad827e04)
    - [ALTER AUDIT POLICY](18-sql-references-a-b.md#ecf2c4bd73416b17)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](18-sql-references-a-b.md#bdecea76b1665d44)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#f63dd37e5a743f09)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#0f5f6dd722f4b648)

- Audit trail 소거: [ALTER DATABASE CLEAR AUDIT TRAIL](18-sql-references-a-b.md#7cfd4bf205511a5c)

<a id="420c16ac60aa5c3d"></a>
## CREATE CLUSTER GROUP

<a id="d79e5bab7432e5c9"></a>
### 기능

Cluster system에 참여할 cluster group을 생성한다.

<a id="117819ff9aa91bcb"></a>
### 구문

```
<cluster group definition> ::=
    CREATE CLUSTER GROUP group_name 
        <cluster member definition> [, ...]
    ;

<cluster member definition> ::=
    CLUSTER MEMBER member_name <connection attribute> [<member position>]

<connection attribute> ::=
    HOST 'address' PORT port_no

<member position> ::=
    POSITION DEFAULT
  | POSITION MAX
  | POSITION number
```

<a id="f910f0edc95f01e3"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;cluster group definition&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="0bdec6b23f766434"></a>
### 구문 규칙 및 파라미터

<a id="00e474368ab66c4a"></a>
#### group_name

Cluster group의 이름이다.   
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="2dc8a272b512caaf"></a>
#### &lt;cluster member definition&gt;

Cluster group에 포함될 cluster member를 정의한다.  
Cluster group은 cluster member를 최대 32 개까지 포함할 수 있다.  
Cluster system에 최초로 생성하는 cluster group에는 cluster member를 한 개만 정의할 수 있고 자기 자신을 cluster member로 포함해야 한다.

<a id="6b688e2a3adf2c10"></a>
#### member_name

Cluster member의 이름이다.   
Cluster member 이름은 해당 member의 database를 생성할 때 정의한 member 이름과 동일해야 한다.  
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

Cluster member의 start-up 단계는 GLOBAL OPEN 단계여야 한다.

<a id="6c16c2b92099da83"></a>
#### &lt;connection attribute&gt;

Cluster member간 통신을 위한 연결 정보를 정의한다.   
&lt;connection attribute&gt;는 해당 member의 database를 생성할 때 정의한 HOST, PORT와 동일해야 한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 host name 또는 IPv4 주소를 사용한다. Host name을 사용할 경우 시스템의 첫 번째 IPv4 주소를 사용한다.
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="2ae5ec59f60f9f38"></a>
#### &lt;member position&gt;

Cluster member의 position number를 지정한다.

- POSITION DEFAULT
    - 시스템이 자동으로 position number를 지정한다.
- POSITION MAX
    - 빈 position number가 있더라도 새로운 member position number를 지정한다.
    - 가장 큰 member position 보다 큰 값을 지정한다.
- POSITION number
    - number에 해당하는 position number를 지정한다.
    - 해당 position number는 cluster system 내에서 고유해야 한다.
    - 해당 position number는 비어있는 position number이면서 가장 큰 position number와 같거나 작아야 한다.
- 생략할 경우, 기본값은 POSITION DEFAULT 이다.

Cluster member의 member_position 정보는 DBA_CLUSTER view를 통해 조회할 수 있다.

```
SELECT member_name, member_id, member_position FROM dba_cluster;
```

예를 들어 다음과 같은 position number가 사용되고 있는 경우,

- G1N1: 0
- G1N2: 1
- G2N2: 3
- G3N2: 5

각 옵션에 따라, 다음과 같은 값을 지정한다.

- POSITION DEFAULT
    - 비어있는 값인 2를 지정한다.
- POSITION MAX
    - 새로운 position number 값인 6을 지정한다.
- POSITION 3
    - 중복되므로 error 이다.
- POSITION 4
    - position number 4를 지정한다.

<a id="8222a17e3e59d215"></a>
### 설명

&lt;cluster group definition&gt; 구문은 table들의 shard를 재배치하지 않는다.

추가된 cluster group에 shard를 재배치하려면 다음 구문을 수행해야 한다.

- [ALTER DATABASE REBALANCE](18-sql-references-a-b.md#f07ba634c9eef9cf)
- [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#149294331f00fde7)

<a id="d2bd4e7a3dd1b140"></a>
### 사용 예

다음은 두 개의 cluster member로 구성된 cluster group을 생성하는 예이다.

```
gSQL> 
CREATE CLUSTER GROUP g1
    CLUSTER MEMBER g1n1 HOST '192.168.0.11' PORT 10110
;

Cluster Group created.

gSQL>
ALTER CLUSTER GROUP g1
    ADD CLUSTER MEMBER g1n2 HOST '192.168.0.12' PORT 10120
;

Cluster Group altered.

gSQL> 
CREATE CLUSTER GROUP g2
    CLUSTER MEMBER g2n1 HOST '192.168.0.21' PORT 10210,
    CLUSTER MEMBER g2n2 HOST '192.168.0.22' PORT 10220
;

Cluster Group created.
```

<a id="f8ccf6cb6a412973"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="bb3f00f2829cca11"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP CLUSTER GROUP](#6d9454a76620869e)
- [ALTER CLUSTER GROUP name ADD MEMBER](18-sql-references-a-b.md#4d285ac15daae9e5)

<a id="6d43d72d687cc2a6"></a>
## CREATE CLUSTER LOCATION

<a id="8200d1d570e11e6c"></a>
### 기능

Cluster member의 접속 정보를 생성한다.

<a id="8f5c1fe76579b2ad"></a>
### 구문

```
<cluster location definition> ::=
    CREATE CLUSTER LOCATION member_name 
    <cluster connection attribute>
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="75fd19e0b42fbfbc"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;cluster location definition&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="a4717d91841a2d8b"></a>
### 구문 규칙 및 파라미터

<a id="7b299ac5128a961e"></a>
#### member_name

Cluster member의 이름이다.   
등록된 cluster location 정보에 동일한 cluster member 이름이 존재하지 않아야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="4b1738333d3e1bfc"></a>
#### &lt;cluster connection attribute&gt;

Cluster member간 통신을 위한 연결 정보를 정의한다.   
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 host name 또는 IPv4 주소를 사용한다. Host name을 사용할 경우 시스템의 첫 번째 IPv4 주소를 사용한다.
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="2a56779ace09c6a0"></a>
### 설명

기본적으로 cluster location 정보는 cluster group을 생성하거나 cluster member를 추가할 때 제공되는 접속 정보를 이용하여 자동으로 생성된다. 생성된 정보는 cluster member와 group을 삭제할 때 함께 삭제된다.

만약 cluster location의 접속 정보가 변경되면 cluster member를 삭제하거나 다시 생성할 필요없이 [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#aab1431151951450)을 이용하여 접속 정보를 변경할 수 있다.

<a id="bc0a0abbd49158e3"></a>
### 사용 예

```
gSQL> 
CREATE CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120,
;

Created
```

<a id="647e2020df706d8c"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="dfdee59ee975b334"></a>
### 참조

관련 내용은 [DROP CLUSTER LOCATION](#3ed6f006ec8fc968)을 참조한다.

<a id="fbef49d9231d0d5d"></a>
## CREATE DISK DATA TABLESPACE

<a id="b32e0df17d55280e"></a>
### 기능

디스크 데이터 테이블스페이스를 정의한다.

<a id="ec3d290c01e31e20"></a>
### 구문

```
<disk data tablespace statement> ::=
    CREATE DISK [ DATA ] TABLESPACE tablespace_name
        DATAFILE <disk datafile clause> [, ...]
        [ <data tablespace management clause> [, ...] ]

<disk datafile clause> ::=
     'filename' 
        [ SIZE <size clause> | REUSE | SIZE <size clause> REUSE ]
        [ <autoextend clause> ]
        [ AT <domain_name> ]

<autoextend clause>
    AUTOEXTEND { ON [ <next size clause> ] [ <max size clause> ] | OFF }

<next size clause>
    NEXT <size clause>

<max size clause>
    MAXSIZE { <size clause> | UNLIMITED }

<size clause> ::=
    integer [ K | M | G | T ]

<data tablespace management clause> ::=
      { ONLINE | OFFLINE }
    | EXTSIZE <size clause>
```

<a id="1bffbc4676d5012f"></a>
### 사용 범위 및 접근 권한

&lt;disk data tablespace definition&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="2ec83e6c2fc5fd0d"></a>
### 구문 규칙 및 파라미터

<a id="5f07964c8b955357"></a>
#### tablespace_name

생성할 테이블스페이스의 이름이다.  
테이블스페이스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="e5686ff7c727596d"></a>
#### &lt;disk datafile clause&gt;

- 'filename' 
    - 데이터를 저장 관리할 파일의 이름이다.
    - 디스크 테이블스페이스에 생성된 테이블, 인덱스 페이지들이 저장될 공간이다.
    - filename은 새로운 파일이거나 이미 존재하는 파일이다.
    - filename의 길이는 1024 바이트보다 작아야 한다.

- SIZE &lt;size clause&gt; 
    - 새로운 파일일 경우 SIZE 절을 이용해 초기 크기를 지정한다. 
    - 파일이 존재할 경우 에러가 발생한다. 
    - 파일의 크기는 최소 1 M ~ 최대 30 G 까지 지정할 수 있다.

- REUSE 
    - 이미 존재하는 파일일 경우 REUSE 절을 이용한다. 
    - 파일이 존재하지 않을 경우 새로운 파일을 생성한다.
    - 새로 생성되는 파일의 크기는 USER_DATA_TABLESPACE_SIZE 프로퍼티에 의해 결정된다.

- SIZE &lt;size clause&gt; REUSE 
    - SIZE 절과 REUSE 절을 모두 명시할 경우 filename의 존재 여부에 따라 다음과 같이 작동한다. 
        - 새로운 filename일 경우에는 SIZE 절을 이용하여 초기 파일 크기를 지정한다. 
        - 이미 존재하는 filename일 경우에는 기존 파일을 이용하여 SIZE 절의 값으로 크기를 조정한다.

<a id="34f62eb22297a907"></a>
#### &lt;autoextend clause&gt;

자동 확장 속성을 ON 또는 OFF로 설정한다. ON으로 설정할 경우 자동 확장 크기와 데이터파일의 최대 크기를 지정할 수 있다.

<a id="d9df6cb1fba37ae1"></a>
#### &lt;next size clause&gt;

현재 사용 중인 데이터 파일에 더 이상 사용할 공간이 없을 때 확장할 크기를 지정한다.

<a id="9bb0a620d6bc5944"></a>
#### &lt;max size clause&gt;

데이터 파일이 확장될 수 있는 최대 크기를 지정한다.

<a id="7b62aa0d77289fcd"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (명시하지 않을 경우 bytes 단위이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="5ca3e6de4f5b3472"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="d8eb351738d20875"></a>
#### ONLINE | OFFLINE

테이블스페이스 ONLINE/ OFFLINE 여부를 설정한다.

- ONLINE은 테이블스페이스를 생성하는 즉시 사용할 수 있는 상태이다. 
- OFFLINE은 사용 불가능한 상태이므로 ONLINE 상태로 변경한 후에 사용할 수 있다.

<a id="cfec643eb76790b8"></a>
#### EXTSIZE &lt;size clause&gt;

테이블스페이스의 extent 크기를 지정한다.

- Extent 크기는 바이트 단위로 기술하며, 여섯 가지 (64 K, 128 K, 256 K, 512 K, 1 M, 2 M) 중 하나가 선택된다.
- 만약 extent 크기가 64 K ~ 128 K 사이의 값으로 지정되면 128 K로 설정되고, 2 M 이상으로 지정되면 2 M로 설정된다.

<a id="a25641681fd4bfb3"></a>
### 설명

Data tablespace는 table, index (LOGGING) 등의 SQL schema 객체를 저장할 물리적 공간을 제공하는 객체이다.

<a id="63959eb1e9cfc6a5"></a>
### 사용 예

다음은 disk data tablespace를 생성하는 예이다.

```
gSQL> CREATE DISK TABLESPACE space1 DATAFILE 'test_file_1.dbf' SIZE 10M REUSE;

Tablespace created.
```

다음은 다수의 data file로 구성된 tablespace를 생성하는 예이다.

```
gSQL> CREATE DISK TABLESPACE space1 
             DATAFILE 'test_file_3_1.dbf' SIZE 10M REUSE,
                      'test_file_3_2.dbf' SIZE 10M REUSE;

Tablespace created.
```

<a id="154aee425bb9b94e"></a>
### 호환성

SQL 표준에서는 테이블스페이스에 대한 개념을 다루지 않고 있다.

<a id="a1540e7785eb71cc"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#0905e5b2ffc06135)
- [ALTER TABLESPACE](18-sql-references-a-b.md#e50680549a4cafe3)
- [ALTER DATABASE DATAFILE AUTOEXTEND](18-sql-references-a-b.md#4f965b5c245db523)

<a id="120b6288f4526728"></a>
## CREATE GLOBAL TEMPORARY TABLE

<a id="562d1ade5cd253d0"></a>
### 기능

새로운 global temporary table을 생성한다.

<a id="f35361c6260d2dc3"></a>
### 구문

```
<global temporary table definition> ::=
    CREATE GLOBAL TEMPORARY TABLE table_name
        ( <table element> [, ...] )
        [ <table commit action clause> ]
        [ TABLESPACE tablespace_name ]
    ;

<global temporary table definition: AS query expression> ::=
    CREATE GLOBAL TEMPORARY TABLE table_name 
        [ TABLESPACE tablespace_name ]
        AS <query expression> [ WITH [ NO ] DATA ]
    ;

<table commit action clause> ::=
    ON COMMIT { PRESERVE | DELETE } ROWS
```

> &lt;table element&gt;의 정의는 &lt;table_definition&gt;의 정의와 동일하다. 자세한 내용은 [CREATE TABLE](#060501387611d25a) 을 참조한다.

<a id="185b85dca49d7fd1"></a>
### 사용 범위 및 접근 권한

&lt;global temporary table definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블 생성 권한
    - [CREATE TABLE](#060501387611d25a) 구문의 접근 권한을 참조한다.
- SELECT 접근 권한 
    - [SELECT](20-sql-references-h-z.md#a8ad8e667688877b) 구문의 접근의 권한을 참조한다.

<a id="82c36ef72b597070"></a>
### 구문 규칙 및 파라미터

<a id="59f10ccd6480365d"></a>
#### table_name

생성할 테이블의 이름이다.  
자세한 내용은 [table_name](#d83b67dfcf8ea14b) 구문을 참조한다.

<a id="d6d481a85021f105"></a>
#### other syntax

이 외의 구문 규칙은 [CREATE TABLE](#060501387611d25a) 및 [CREATE TABLE AS SELECT](#bd342487ebebfc2b) 구문의 syntax를 참조한다.

<a id="c0791b2b0d4db252"></a>
### 설명

GLOBAL TEMPORARY TABLE은 한 트랜잭션이나 세션이 실행되는 동안 유지될 데이터를 보관하는 용도로 사용하는 임시 테이블이다.  
개발자가 응용 프로그램을 개발할 때 연산 중간 데이터를 잠시 저장하는 변수와 같은 용도로 사용된다.

Global temporary table의 특징은 다음과 같다.

- Global temporary table의 정의는 모든 세션에서 볼 수 있다.
- Global temporary table을 정의할 때는 물리적 공간이 할당되지 않고, 처음으로 insert 할 때 해당 세션에 종속된 실제 공간 (segment)이 할당된다.
- Global temporary table의 데이터는 insert 한 세션이나 트랜잭션에서만 볼 수 있다.
- Global temporary table의 데이터가 저장되는 tablespace는 다음과 같이 결정된다.

<a id="a8056b055588d806"></a>
| Tablespace 명시 여부 | Table이 생성되는 tablespace |
| --- | --- |
| Tablespace를 명시한다. | 명시된 tablespace에 생성된다. |
| Tablespace를 명시하지 않는다. | 현재 세션 사용자의 default temporary tablespace에 생성된다. |

- Global temporary table에 대한 인덱스는 대응하는 테이블과 같은 세션에 종속되며 지속기간 역시 해당 테이블과 같다.
- Global temporary table에 대한 view를 정의할 수 있다.
- Global temporary table에 대해 테이블의 cluster 관련 특성을 기술하는 &lt;table sharding strategy&gt; 구문이나 &lt;table global secondary index clause&gt;구문을 지정할 수 없다.
- Global temporary table에 대해 테이블의 물리적 특징을 기술하는 &lt;table attribute clause&gt;나 인덱스의 물리적 특징을 기술하는 &lt;index attribute clause&gt;를 지정할 수 없다.
- Global temporary table을 base table로 하여 생성되는 index들에는 인덱스의 물리적 특징을 기술하는 &lt;index attribute clause&gt;를 지정할 수 없다.
- &lt;table commit action clause&gt;에 의해 transaction이 종료될 경우, 남아있는 데이터의 처리 방법을 결정할 수 있다.

<a id="52269e71e118e558"></a>
| Table commit action | 설명 |
| --- | --- |
| ON COMMIT PRESERVE ROWS | COMMIT 되거나 ROLLBACK 되어도 테이블에 남아있는 데이터를 그대로 유지한다. |
| ON COMMIT DELETE ROWS(default) | COMMIT 되거나 ROLLBACK 하는 시점에 테이블에 남아있는 데이터를 모두 삭제한다 (TRUNCATE). |

- 일반 테이블에 대한 대부분의 DDL을 지원한다. (ALTER, TRUNCATE 포함)
    - CLUSTER 관련 구문 (SHARD 및 global secondary index 관련 구문 등)은 지원하지 않는다.
    - 자신의 세션이나 다른 세션에서 현재 사용 중인 global temporary table에 대한 DDL은 오류를 발생시킨다.
    - 사용 중인 모든 세션에서 TRUNCATE TABLE이나 COMMIT 등으로 사용 중인 segment들을 모두 제거한 후에 DDL이 가능해진다.
- 일반 테이블에 대한 모든 DML과 select 구문을 지원한다.
- Global temporary table에 대한 모든 변경 (DML)은 redo log를 남기지 않는다.
- Global temporary table에 대한 모든 변경 (DML)은 undo log를 남기며, TEMP_UNDO_ENABLED 프로퍼티에 따라 undo log의 위치가 결정된다.

<a id="fe74369a3433e878"></a>
| TEMP_UNDO_ENABLED 값 | 설명 |
| --- | --- |
| TRUE | Database system의 default temporary tablespace에 undo log가 기록된다. |
| FALSE | Database system의 undo tablespace에 undo log가 기록된다. |

- Global temporary table에 대한 TRUNCATE 명령은 해당 세션의 segment만 truncate 한다.
- 세션이 종료되면 모든 segment들이 TRUNCATE 된 후에 반환된다.

<a id="1d72f81ec8530c82"></a>
### 사용 예

다음은 CREATE GLOBAL TEMPORARY TABLE 구문을 실행하는 예이다.

```
gSQL> CREATE  GLOBAL TEMPORARY TABLE SESSION_TABLE1(
        COL1    CHAR(10)
       ,COL2    VARCHAR2(20)
       ,COL3    NUMBER(10)
)   ON  COMMIT  DELETE ROWS;

Table created.
```

다음은 CREATE GLOBAL TEMPORARY TABLE ... AS SELECT 구문을 실행하는 예이다.

```
gSQL> CREATE  GLOBAL TEMPORARY TABLE SESSION_TABLE2
    ON  COMMIT  PRESERVE ROWS
    AS  SELECT  *
          FROM  EMPLOYEES;

Table created.
```

<a id="405429ad91821093"></a>
### 호환성

CREATE GLOBAL TEMPORARY TABLE 및 CREATE GLOBAL TEMPORARY TABLE AS SELECT 구문은 SQL 표준의 &lt;table definition&gt; 정의를 따른다. 단, 다음은 표준에서 확장된 것이다.

- 표준에서 SELECT 절 밖의 괄호는 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- 표준에서 WITH [NO] DATA 절은 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- GOLDILOCKS의 tablespace 개념은 표준에 없는 확장 개념이다.

**SQL 표준 호환성**

<a id="061cf1636a46a240"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T171 | LIKE clause in table definition | X |
| T172 | AS subquery clause in table definition | O |
| F531 | Temporary tables | X |
| S051 | Create table of type | X |
| S043 | Enhanced reference types | X |
| S081 | Subtables | X |
| T173 | Extended LIKE clause in table definition | X |
| T180 | System-versioned tables | X |
| F692 | Extended collation support | X |
| T174 | Identity columns | O |
| T175 | Generated columns | X |
| S071 | SQL paths in function and type name resolution | X |
| F321 | User authorization | O |
| T322 | Extended roles | X |
| F762 | CURRENT_CATALOG | O |
| F763 | CURRENT_SCHEMA | O |

<a id="2e6a991da78b1159"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](#060501387611d25a)
- [CREATE TABLE AS SELECT](#bd342487ebebfc2b)

<a id="137776deb9c26df9"></a>
## CREATE IMMUTABLE TABLE

<a id="4a8ab02fcb083ccd"></a>
### 기능

새로운 immutable table을 생성한다.

<a id="3827efd68438f5a6"></a>
### 구문

```
<immutable table definition> ::=
    CREATE IMMUTABLE TABLE table_name
        ( <table element> [, ...] )
        [ <table sharding strategy> ]
        [ <table attribute clause> [...] ]
        [ TABLESPACE tablespace_name ]
        [ <table global secondary index clause> ]
    ;

<immutable table definition: AS query expression> ::=
    CREATE IMMUTABLE TABLE table_name
        [ ( column_name [, ...] ) ]
        [ <table sharding strategy> ]
        [ <table attribute clause> [, ...] ]
        [ TABLESPACE tablespace_name ]
        [ <table global secondary index clause> ]
        AS <query expression> [ WITH [ NO ] DATA ]
    ;
```

> &lt;table element&gt;, &lt;table sharding strategy&gt;, &lt;table attribute clause&gt;, &lt;table global secondary index clause&gt;의 정의는 &lt;table_definition&gt;의 정의와 동일하다. 자세한 내용은 [CREATE TABLE](#060501387611d25a)을 참조한다.

<a id="672102aac3407fa6"></a>
### 사용 범위 및 접근 권한

&lt;immutable table definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블 생성 권한
    - [CREATE TABLE](#060501387611d25a) 구문의 접근 권한을 참조한다.
- SELECT 접근 권한 
    - [SELECT](20-sql-references-h-z.md#a8ad8e667688877b) 구문의 접근 권한을 참조한다.

<a id="1b71813e71d6afdb"></a>
### 구문 규칙 및 파라미터

<a id="be427784a5577f8d"></a>
#### table_name

생성할 테이블의 이름이며, 스키마 내에서 고유한 이름이어야 한다.  
schema_name.table_name과 같이 테이블이 소속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
테이블 이름의 길이는 128 바이트보다 작아야 한다.

<a id="e27a6c3fd2b69ee4"></a>
#### 기타 구문 규칙

이 외의 구문 규칙은 [CREATE TABLE](#060501387611d25a)과 [CREATE TABLE AS SELECT](#bd342487ebebfc2b) 구문의 syntax를 참조한다.

<a id="af9825c14bb2244c"></a>
### 설명

Immutable table은 저장된 레코드의 변경 및 삭제를 불가능하게 할 뿐만 아니라 테이블 자체도 삭제하지 못하도록 하기 위한 용도로 사용된다.

> 사용자, 스키마, 테이블스페이스, 클러스터 그룹을 삭제할 경우 immutable table도 삭제할 수 있다.

> Immutable table로 생성했을 때 허용되지 않는 SQL 구문
> 
> - UPDATE
> - DELETE
> - ALTER TABLE RENAME/DROP COLUMN
> - ALTER TABLE SET UNUSED COLUMN
> - ALTER TABLE DROP UNUSED COLUMNS
> - ALTER TABLE RENAME TO
> - TRUNCATE TABLE
> - DROP TABLE
> 
>   
> Immutable table로 생성했을 때 허용되는 SQL 구문
> 
> - INSERT
> - SELECT
> - SELECT .. FOR UPDATE
> - CREATE/ALTER/DROP INDEX
> - ALTER TABLE ADD/ALTER COLUMN
> - ALTER TABLE ADD/ALTER/RENAME/DROP CONSTRAINT
> - ALTER TABLE for physical property changes
> - ALTER TABLE ADD/DROP SUPPLEMENTAL LOG
> - LOCK TABLE
> - ALTER TABLE .. ADD/ALTER/DROP GLOBAL SECONDARY INDEX
> - ALTER DATABASE MOVE SHARD
> - ALTER TABLE .. MOVE SHARD
> - ALTER TABLE .. SPLIT SHARD
> - ALTER TABLE .. MERGE SHARD
> - DROP TABLESPACE
> - DROP SCHEMA
> - DROP USER
> - DROP CLUSTER GROUP
> 

<a id="34465f1089f0f09d"></a>
### 사용 예

다음은 CREATE IMMUTABLE TABLE 구문을 실행하는 예이다.

```
gSQL> CREATE IMMUTABLE TABLE t1
(
    id INTEGER PRIMARY KEY,
    name VARCHAR(128),
    addr VARCHAR(128)
);

Table created.
```

다음은 CREATE IMMUTABLE TABLE ... AS SELECT 구문을 실행하는 예이다.

```
gSQL> CREATE IMMUTABLE TABLE T2
       AS SELECT *
             FROM T1;

Table created.
```

<a id="c86450a8bae2d6bb"></a>
### 호환성

SQL 표준에서는 CREATE IMMUTABLE TABLE 구문과 CREATE IMMUTABLE TABLE AS SELECT 구문을 다루지 않고 있다.

<a id="aca499d14a8af173"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](#060501387611d25a)
- [CREATE TABLE AS SELECT](#bd342487ebebfc2b)

<a id="04e7730c239ac562"></a>
## CREATE INDEX

<a id="bbab999e0cee65f2"></a>
### 기능

인덱스를 생성한다.

<a id="afaaffaf0f2d8be7"></a>
### 구문

```
<index definition> ::=
    CREATE [ UNIQUE ] INDEX index_name
        ON table_name ( <index column element> [, ...] )
        [ <index attributes> [...] ]
        [ TABLESPACE tablespace_name ]
    ;

<index column element> ::=
    column_name [ ASC | DESC ] [ NULLS FIRST | NULLS LAST ]

<index attributes> ::=
      <physical attribute clause>
    | STORAGE ( <segment attr clause> [...] )
    | <parallel clause> 

<physical attribute clause> ::=
      PCTFREE integer
    | INITRANS integer
    | MAXTRANS integer

<segment attr clause> ::=
      INITIAL <size_clause>
    | NEXT <size_clause>
    | MINSIZE <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="12d3d3efe291d15c"></a>
### 사용 범위 및 접근 권한

&lt;index definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 인덱스를 생성할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (INDEX 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 CONTROL SCHEMA ON SCHEMA 
    - CREATE ANY INDEX ON DATABASE

- 인덱스가 생성될 스키마에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 스키마에 대해 (CREATE INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
    - CREATE ANY INDEX ON DATABASE

- 인덱스가 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
    - USAGE TABLESPACE ON DATABASE

- 인덱스의 소유자는 다음과 같이 결정된다.
    - 인덱스가 속한 스키마의 소유자
    - 인덱스가 속한 스키마가 PUBLIC인 경우, 구문을 수행한 사용자

> Cluster에서 unique index는 모든 sharding key를 포함해야 한다.

<a id="e7599de536fe8c8e"></a>
### 구문 규칙 및 파라미터

<a id="b9f4ad45ff529a08"></a>
#### UNIQUE

인덱스를 구성하는 column들에 중복 값을 허용하지 않는다.

<a id="f89d5963e2b77398"></a>
#### index_name

생성할 인덱스의 이름이며, 스키마 내에서 유일해야 한다.  
스키마 이름을 생략할 경우, 참조하는 테이블이 속한 스키마에 인덱스가 생성된다.  
인덱스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="3d1e28a776c23b00"></a>
#### table_name

인덱스를 생성할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="aa480eea4eafcbb1"></a>
#### column_name

인덱스 key로 사용할 column의 이름이다.  
하나 이상의 column을 정의해야 하는데 최대 32 개의 column을 인덱스 key로 사용할 수 있다.

구현 내용에 따라 다음과 같은 제약이 발생할 수 있다.

- 인덱스에 포함되는 column의 데이터 타입이 LONG CHARACTER VARYING, LONG BINARY VARYING 일 경우 인덱스를 생성할 수 없다. 
- Column들의 precision 합계가 1200 바이트보다 작은 경우에만 인덱스를 생성할 수 있다.

<a id="a94584156e6edbbe"></a>
#### ASC | DESC

Column의 정렬 순서를 명시한다.

- ASC: 오름차순으로 정렬한다. 
- DESC: 내림차순으로 정렬한다. 
- 명시하지 않을 경우, 기본값은 ASC 이다.

<a id="9443587a3531c6c5"></a>
#### NULLS FIRST | NULLS LAST

NULL 값의 정렬 순서를 명시한다.

- NULLS FIRST: NULL이 아닌 값들보다 앞에 위치한다. 
- NULLS LAST: NULL이 아닌 값들보다 뒤에 위치한다. 
- 명시하지 않을 경우, 기본값은 NULLS LAST 이다.

<a id="b61e6b62a60b685d"></a>
#### &lt;physical attribute clause&gt;

인덱스의 물리적 속성 정보를 정의한다.

- PCTFREE integer 
    - 정의 
        - 페이지 내 key 삽입으로 인한 페이지 분할 빈도를 조절하기 위해 예약된 공간이다.
        - 인덱스 bottom-up 빌드 시에만 적용된다. 
    - 0 에서 99 까지의 값을 사용할 수 있다. 
    - 생략할 경우, DEFAULT_INDEX_PCTFREE property에 설정된 값을 사용한다.

- INITRANS integer 
    - 정의 
        - 페이지에 동시 접근할 수 있는 초기 트랜잭션의 개수이다. 
        - 인덱스에 접근하는 사용자의 수가 적을 경우에는 INITRANS를 낮게 설정하고, 동시에 접근하는 사용자가 많을 경우에는 INITRANS를 높게 설정한다. 
        - 필요한 경우 설정된 MAXTRANS까지 자동으로 늘어난다. 
    - 1 부터 32 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기본값은 4 이다.

- MAXTRANS integer 
    - 정의 
        - 페이지에 동시 접근할 수 있는 트랜잭션의 최대 개수이다. 
    - 1 부터 32 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기본값은 8 이다.

<a id="7b9c222e58ba3170"></a>
#### &lt;segment attr clause&gt;

인덱스가 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer
    - 정의
        - 인덱스를 생성할 때 초기에 할당할 물리적 공간의 크기를 기술한다.
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT 크기가 8192 bytes일 경우 'INITIAL 100'은 실제 8192 bytes로 작동한다.)
        - 이 크기 (TABLESPACE의 EXTENT 크기에 align 된 크기)는 MINEXTENTS의 크기와 같거나 커야 하며, MAXEXTENTS의 크기와 같거나 작아야 한다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기본값은 테이블이 속한 TABLESPACE의 EXTENT 하나 크기이다.

- NEXT integer
    - 정의
        - 인덱스의 물리적 공간을 추가할 경우 할당할 물리적 공간의 크기를 기술한다.
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT크기가 8192 bytes일 경우 'NEXT 100'은 실제 8192 bytes로 작동한다.)
        - NEXT는 현재 인덱스가 사용할 수 있는 남은 공간의 크기 (MAXEXTENTS의 크기에서 현재 사용하고 있는 공간의 크기를 뺀 크기)에 따라 다음과 같이 작동한다.  
      - 남은 공간의 크기가 0인 경우 더 이상 공간을 확장하지 못한다.  
      - 남은 공간의 크기가 0보다 크고 NEXT보다 작은 경우 남은 공간의 크기만큼 할당한다.  
      - 남은 공간의 크기가 NEXT 보다 클 경우 NEXT의 크기만큼 할당한다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기본값은 인덱스가 속한 TABLESPACE의 EXTENT 하나 크기이다.

- MINSIZE integer
    - 정의
        - 인덱스에서 유지해야할 최소 공간의 크기이다.
        - 이 값은 MAXSIZE의 값과 같거나 작아야 한다.
    - 이 크기는 인덱스가 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - EXTENT 두 개 크기보다 작을 경우 EXTENT 두 개 크기로 결정된다.
    - 생략할 경우, 기본값은 EXTENT 두 개 크기이다.

- MAXSIZE integer
    - 정의
        - 인덱스에서 할당받을 수 있는 최대 공간의 크기이다.
        - 이 값은 MINSIZE의 값과 같거나 커야 한다.
    - 이 크기는 인덱스가 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기본값은 32 테라바이트 (35,184,372,088,832) 이다.
    - 32 테라바이트보다 큰 값을 지정하더라도 32 테라바이트로 수정되어 설정된다.

<a id="60db88ddcde873db"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="108e02e847a9eee2"></a>
#### NOPARALLEL | PARALLEL [ integer ]

인덱스 구축과정에서 사용될 thread 개수를 지정한다.

- NOPARALLEL 
    - 인덱스를 병렬로 구축하지 않는다. 
- PARALLEL [integer] 
    - 인덱스를 병렬로 구축한다. 
    - integer가 생략되거나 0으로 지정된 경우에는 프로퍼티 (INDEX_BUILD_PARALLEL_FACTOR)를 따른다. 
    - integer는 0 부터 사용할 수 있으며 최대값은 16이다. 
    - 만약 프로퍼티의 값이 0인 경우에는 시스템이 최적값을 결정한다.
- 명시하지 않을 경우, 기본값은 PARALLEL이다.

<a id="4da0990e9f207bd4"></a>
#### TABLESPACE tablespace_name

인덱스가 저장될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - tablespace_name이 data tablespace면 LOGGING 인덱스가 생성된다.
    - tablespace_name이 temporary tablespace 또는 nologging tablespace면 NOLOGGING 인덱스가 생성된다.

- TABLESPACE 절을 생략할 경우,
    - USER의 INDEX TABLESPACE tablespace_name을 지정한 경우
        - 정의한 테이블스페이스를 사용한다.
    - USER의 INDEX TABLESPACE가 NULL인 경우
        - DISK 테이블의 인덱스는 사용자의 기본 데이터 테이블스페이스를 사용한다.
        - MEMORY 테이블의 인덱스는 사용자의 기본 임시 테이블스페이스를 사용한다.

<a id="f5cdbb68ff0c8a5f"></a>
### 설명

LOGGING 인덱스와 NOLOGGING 인덱스에는 다음과 같은 trade-off가 있다.

- LOGGING 인덱스
    - 장점: 시스템을 구동할 때 로그를 이용해 인덱스가 자동으로 복구되므로 별도의 구축과정이 없다.
    - 단점: 관련 row를 변경할 때 인덱스 변경 내용을 로그로 기록하여 디스크 IO를 유발한다.
- NOLOGGING 인덱스
    - 장점: 관련 row를 변경할 때 인덱스 변경 내용에 대한 디스크 IO가 발생하지 않는다.
    - 단점: 시스템을 구동할 때 인덱스에 대한 로그 정보가 없어 자동으로 인덱스를 재구축한다.

<a id="28f6d1c2e11f8c95"></a>
### 사용 예

다음은 unique index를 생성하는 예이다.

```
gSQL> CREATE UNIQUE INDEX idx_t1_id ON t1( id );

Index created.
```

다음은 다수의 column에 대해 인덱스를 생성하는 예이다.

```
gSQL> CREATE INDEX idx_t1_id_name ON t1( id, name );

Index created.
```

다음은 인덱스 column의 정렬 순서를 지정하는 예이다.

```
gSQL> CREATE INDEX idx_t1_dept_id ON t1( dept_id DESC );

Index created.
```

다음은 인덱스 column의 NULL 값 정렬 순서를 지정하는 예이다.

```
gSQL> CREATE INDEX idx_t1_name ON t1( name NULLS FIRST );

Index created.
```

다음은 인덱스가 저장될 공간에 대한 정보를 설정하는 예이다.

```
gSQL> CREATE INDEX idx_t1_id ON t1( id )
             STORAGE ( INITIAL 10M NEXT 1M MINSIZE 10M MAXSIZE 100M );

Index created.
```

다음은 인덱스에 대해 리두 로깅을 생성하도록 하는 예이다.

```
gSQL> CREATE INDEX idx_t1_id ON t1( id );

Index created.
```

다음은 인덱스를 병렬로 생성하도록 하는 예이다.

```
gSQL> CREATE INDEX idx_t1_name ON t1( name ) PARALLEL;

Index created.
```

다음은 인덱스를 생성할 때 테이블스페이스를 지정하는 예이다.

```
gSQL> CREATE INDEX idx_t1_name ON t1( name ) TABLESPACE mem_temp_tbs;

Index created.
```

<a id="8344c78e1a69049e"></a>
### 호환성

SQL 표준에서는 인덱스에 대한 개념을 다루지 않고 있다.

<a id="1ddfea2f53775a3f"></a>
### 참조

관련 내용은 [DROP INDEX](#d20adfa902b88837)를 참조한다.

<a id="5dc8246fbc0a52e1"></a>
## CREATE MEMORY DATA TABLESPACE

<a id="f396fe40a9345e32"></a>
### 기능

메모리 데이터의 테이블스페이스를 정의한다.

<a id="ef5b9e19209a5afb"></a>
### 구문

```
<memory data tablespace statement> ::=
    CREATE [ MEMORY ] [ DATA ] TABLESPACE tablespace_name
        DATAFILE <memory datafile clause> [, ...]
        [ <data tablespace management clause> [, ...] ]

<memory datafile clause> ::=
     'filename' 
        [ SIZE <size clause> | REUSE | SIZE <size clause> REUSE ]
        [ AT <domain_name> ]
<size clause> ::=
    integer [ K | M | G | T ]

<data tablespace management clause> ::=
      { ONLINE | OFFLINE }
    | EXTSIZE <size clause>
```

<a id="2300b659562ceb37"></a>
### 사용 범위 및 접근 권한

&lt;memory data tablespace definition&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="278a8f64eb3db6b2"></a>
### 구문 규칙 및 파라미터

<a id="586eafb06fb90ae7"></a>
#### [ MEMORY ] [ DATA ]

테이블, 인덱스 등 영구적인 객체를 저장할 메모리 테이블스페이스이다.  
MEMORY와 DATA 예약어는 생략할 수 있다.

<a id="dd3a96eff719e010"></a>
#### tablespace_name

생성할 테이블스페이스의 이름이다.  
테이블스페이스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="40bb70837599672c"></a>
#### &lt;memory datafile clause&gt;

- 'filename' 
    - 데이터를 저장 관리할 파일의 이름이다.
    - 메모리 데이터에 대한 체크포인트 이미지를 저장할 공간이다.
    - filename은 새로운 파일이거나 이미 존재하는 파일이다.
    - filename의 길이는 1024 바이트보다 작아야 한다.

- SIZE &lt;size clause&gt; 
    - 새로운 파일일 경우 SIZE 절을 이용해 초기 크기를 지정한다. 
    - 파일이 존재할 경우 에러가 발생한다. 
    - 파일의 크기는 최소 1 M ~ 최대 30 G 까지 지정할 수 있다.

- REUSE 
    - 이미 존재하는 파일일 경우 REUSE 절을 이용한다. 
    - 파일이 존재하지 않을 경우 새로운 파일을 생성한다. 
    - 새로 생성되는 파일의 크기는 
        - 데이터 테이블스페이스의 경우 USER_DATA_TABLESPACE_SIZE 프로퍼티에 의해 결정되고 
        - 임시 테이블스페이스의 경우 USER_TEMP_TABLESPACE_SIZE 프로퍼티에 의해 결정된다.

- SIZE &lt;size clause&gt; REUSE 
    - SIZE 절과 REUSE 절을 모두 명시할 경우 filename의 존재 여부에 따라 다음과 같이 작동한다. 
        - 새로운 filename일 경우에는 SIZE 절을 이용해 초기 파일 크기를 지정한다. 
        - 이미 존재하는 filename일 경우에는 기존 파일을 이용하여 SIZE 절의 값으로 크기를 조정한다.

<a id="eb631d7dc6d90216"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="b99647786aef0c69"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="4641eddda701f2d3"></a>
#### ONLINE | OFFLINE

테이블스페이스 ONLINE/ OFFLINE 여부를 설정한다.

- ONLINE은 테이블스페이스를 생성하는 즉시 사용할 수 있는 상태이다. 
- OFFLINE은 사용 불가능한 상태이므로 ONLINE 상태로 변경한 후에 사용할 수 있다.

<a id="d3f329d3e28d101b"></a>
#### EXTSIZE &lt;size clause&gt;

테이블스페이스의 extent 크기를 지정한다.

- Extent 크기는 바이트 단위로 기술하며, 여섯 가지 (64 K, 128 K, 256 K, 512 K, 1 M, 2 M) 중 하나가 선택된다.
- 만약 extent 크기가 64 K ~ 128 K 사이의 값으로 지정되면 128 K로 설정되고, 2 M 이상으로 지정되면 2 M로 설정된다.

<a id="007a5439b47a62e3"></a>
### 설명

Data tablespace는 table, index (LOGGING) 등의 SQL schema 객체를 저장할 물리적 공간을 제공하는 객체이다.

<a id="5b1da198fbbaaac6"></a>
### 사용 예

다음은 memory data tablespace를 생성하는 예이다.

```
gSQL> CREATE TABLESPACE space1 DATAFILE 'test_file_1.dbf' SIZE 10M REUSE;

Tablespace created.
```

다음은 다수의 data file로 구성된 tablespace를 생성하는 예이다.

```
gSQL> CREATE TABLESPACE space1 
             DATAFILE 'test_file_3_1.dbf' SIZE 10M REUSE,
                      'test_file_3_2.dbf' SIZE 10M REUSE;

Tablespace created.
```

<a id="a0abaf50b255c7a8"></a>
### 호환성

SQL 표준은 테이블스페이스에 대한 개념을 다루지 않고 있다.

<a id="007796d75fbb0031"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#0905e5b2ffc06135)
- [ALTER TABLESPACE](18-sql-references-a-b.md#e50680549a4cafe3)

<a id="101999ca47732e9f"></a>
## CREATE MEMORY TEMPORARY TABLESPACE

<a id="9c7d45599575e0dc"></a>
### 기능

메모리 임시 테이블스페이스를 정의한다.

<a id="5a1c4be6797eef92"></a>
### 구문

```
<memory temporary tablespace statement> ::=
    CREATE [ MEMORY ] TEMPORARY TABLESPACE tablespace_name
        MEMORY <memory clause> [, ...]
        <temporary tablespace management clause>

<memory clause> 
     'memory_name' { SIZE <size clause> } [ AT <domain_name> ]

<temporary tablespace management clause> ::=
    EXTSIZE <size clause>
```

<a id="54e6fc58ebcfe394"></a>
### 사용 범위 및 접근 권한

&lt;memory temporary tablespace definition&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="a7dbf9f92622d8c8"></a>
### 구문 규칙 및 파라미터

<a id="37cda5e0f140f11b"></a>
#### [ MEMORY ] TEMPORARY

질의 처리 과정에서 생성되는 중간 결과 등의 임시 객체나 no logging 인덱스를 저장할 메모리 임시 테이블스페이스이다.  
MEMORY 예약어는 생략할 수 있다.

<a id="4756cf5c06805f1b"></a>
#### tablespace_name

생성할 테이블스페이스의 이름이다.  
테이블스페이스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="ca249eb4444df6f6"></a>
#### &lt;memory clause&gt;

- 'memory_name' 
    - 임시 데이터를 저장할 메모리 이름이다. 
    - memory_name은 해당 테이블스페이스 내에서 유일해야 한다. 
    - memory_name의 길이는 1024 바이트보다 작아야 한다. 
- SIZE &lt;size clause&gt; 
    - 초기 크기를 지정한다. 
    - 최소 1 M ~ 최대 30 G 까지 지정할 수 있다.

<a id="4a461da77534ce61"></a>
#### &lt;size clause&gt;

공유 메모리 공간의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)  
임시 메모리 데이터의 경우 이미지를 파일로 관리하지 않는다.

- K: Kilobytes
- M: Megabytes
- G: Gigabytes
- T: Terabytes

<a id="fd178b997807b0ed"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="0575eca3cc1cbc0e"></a>
#### EXTSIZE &lt;size clause&gt;

테이블스페이스의 extent 크기를 지정한다.

- Extent 크기는 바이트 단위로 기술하며, 여섯 가지 (64 K, 128 K, 256 K, 512 K, 1 M, 2 M) 중 하나가 선택된다. 
- 만약 extent 크기가 64 K ~ 128 K 사이의 값으로 지정되면 128 K로 설정되고, 2 M 이상으로 지정되면 2 M로 설정된다.

<a id="0dfe33a77711b73d"></a>
### 설명

Temporary tablespace는 index (NOLOGGING) 등의 SQL schema 객체와, 질의를 처리할 때 sorting/ hashing 하기 위한 중간 결과를 저장하는 물리적 공간을 제공하는 객체이다.

<a id="0fdc140d5f4716ac"></a>
### 사용 예

다음은 temporary tablespace를 생성하는 예이다.

```
gSQL> CREATE TEMPORARY TABLESPACE temp_space1 MEMORY 'test_memory_1' SIZE 10M;

Tablespace created.
```

다음은 다수의 메모리 공간을 갖는 temporary tablespace를 생성하는 예이다.

```
gSQL> CREATE TEMPORARY TABLESPACE temp_space1 
             MEMORY 'test_memory_3_1' SIZE 10M,
                    'test_memory_3_2' SIZE 10M;

Tablespace created.
```

<a id="a0421321cef36dd1"></a>
### 호환성

SQL 표준은 테이블스페이스에 대한 개념을 다루지 않고 있다.

<a id="8d0c1a986108fd1a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#0905e5b2ffc06135)
- [ALTER TABLESPACE](18-sql-references-a-b.md#e50680549a4cafe3)

<a id="7ed273ad779b6feb"></a>
## CREATE PROFILE

<a id="fe7a5ce6f1445b94"></a>
### 기능

Profile을 생성하는 구문으로써 password 관리 방법을 설정할 수 있다.   
User에게 profile을 할당하면 profile에 정의된 방법으로 user의 password를 관리한다.

<a id="021707b8bff0e796"></a>
### 구문

```
<profile definition> ::=

    CREATE PROFILE profile_name LIMIT 
    { <password_parameters>, ...}
    ; 

<password parameters> ::= 
      FAILED_LOGIN_ATTEMPTS { integer | UNLIMITED | DEFAULT }
    | PASSWORD_LOCK_TIME  { password_parameter_number_interval | UNLIMITED | DEFAULT }
    | PASSWORD_LIFE_TIME  { password_parameter_number_interval | UNLIMITED | DEFAULT }
    | PASSWORD_GRACE_TIME { password_parameter_number_interval | UNLIMITED | DEFAULT }
    | PASSWORD_REUSE_MAX  { integer | UNLIMITED | DEFAULT }
    | PASSWORD_REUSE_TIME { password_parameter_number_interval | UNLIMITED | DEFAULT }
    | PASSWORD_VERIFY_FUNCTION { <verify_policy> | NULL | DEFAULT }

<verify_policy> ::= 
      KISA_VERIFY_FUNCTION
    | ORA12C_VERIFY_FUNCTION
    | ORA12C_STRONG_VERIFY_FUNCTION
    | VERIFY_FUNCTION_11G 
    | VERIFY_FUNCTION

<password_parameter_number_interval> ::=
   integer 
 | integer / integer
```

<a id="cd99a2f17f6b6117"></a>
### 사용 범위 및 접근 권한

&lt;profile definition&gt; 구문을 수행하려면 사용자에게 CREATE PROFILE ON DATABASE 권한이 있어야 한다.

<a id="41ed158b5c27d9f7"></a>
### 구문 규칙 및 파라미터

<a id="bc23998d1f605a47"></a>
#### profile_name

생성할 profile의 이름을 명시한다.

<a id="65ee5a58b12acdd0"></a>
#### password_parameters

비밀번호 관리를 위한 parameter들을 설정한다.

- 다음과 같은 parameter를 설정할 수 있다.
    - FAILED_LOGIN_ATTEMPTS
    - PASSWORD_LOCK_TIME
    - PASSWORD_LIFE_TIME
    - PASSWORD_GRACE_TIME
    - PASSWORD_REUSE_MAX
    - PASSWORD_REUSE_TIME
    - PASSWORD_VERIFY_FUNCTION

생략한 parameter는 "DEFAULT" profile의 정책을 따른다.

<a id="061863a4355c18b7"></a>
#### FAILED_LOGIN_ATTEMPTS

연속적인 로그인 실패 가능 횟수를 설정한다.   
명시된 횟수를 넘어서면 계정이 잠긴다.

- FAILED_LOGIN_ATTEMPTS integer
    - 값의 범위는 0보다 큰 양의 정수여야 한다. 
- FAILED_LOGIN_ATTEMPTS UNLIMITED
    - 로그인 실패로 인해 계정이 잠기지 않는다.
- FAILED_LOGIN_ATTEMPTS DEFAULT
    - "DEFAULT" profile의 정책을 따른다.

<a id="ce90dd9fb9deefbf"></a>
#### PASSWORD_LOCK_TIME

연속적인 login 실패 후 계정이 잠기는 기간 (day)을 설정한다.

- PASSWORD_LOCK_TIME constant_expression
    - 잠금이 지속되는 기간 (day)이다.
    - 기본 단위는 일 (day)이다.
    - 테스트하기 위해 시 (n/24), 분 (n/1440), 초 (n/86400)를 명시할 수 있다.
    - 값의 범위는 1초 (1/86400) ~ 100000 일이다.
- PASSWORD_LOCK_TIME UNLIMITED
    - 계정이 잠길 경우 ALTER USER user_name ACCOUNT UNLOCK 구문을 수행하기 전까지 잠금이 해제되지 않는다.
- PASSWORD_LOCK_TIME DEFAULT
    - "DEFAULT" profile의 정책을 따른다.

<a id="f4c130c7597b9bfa"></a>
#### PASSWORD_LIFE_TIME

비밀번호의 유효 기간 (day)을 설정한다.

- PASSWORD_LIFE_TIME constant_expression 
    - 비밀번호의 유효 기간 (day)이다.
    - 기본 단위는 일 (day)이다.
    - 테스트하기 위해 시 (n/24), 분 (n/1440), 초 (n/86400)를 명시할 수 있다.
    - 값의 범위는 1초 (1/86400) ~ 100000 일이다. 
- PASSWORD_LIFE_TIME UNLIMITED 
    - 비밀번호의 만료 기간이 없다.
- PASSWORD_LIFE_TIME DEFAULT
    - "DEFAULT" profile의 정책을 따른다.

<a id="d1a46ca126438376"></a>
#### PASSWORD_GRACE_TIME

PASSWORD_LIFE_TIME 이후에 login 했을 때 비밀번호 만료를 유예하는 기간을 설정한다.

- PASSWORD_GRACE_TIME constant_expression 
    - 비밀번호 만료 유예 기간 (day)이다.
    - 기본 단위는 일 (day)이다.
    - 테스트하기 위해 시 (n/24), 분 (n/1440), 초 (n/86400)를 명시할 수 있다.
    - 값의 범위는 1초 (1/86400) ~ 100000 일이다. 
- PASSWORD_GRACE_TIME UNLIMITED 
    - 비밀번호 만료를 계속 유예한다.
- PASSWORD_GRACE_TIME DEFAULT 
    - "DEFAULT" profile의 정책을 따른다.

비밀번호 유효기간이 지난 후 처음으로 login 하려고 시도할 때부터 PASSWORD_GRACE_TIME이 시작되고, 이 기간동안 비밀번호를 변경하지 않으면 비밀번호가 만료된다.

<a id="f63d9d367ce79f38"></a>
#### PASSWORD_REUSE_MAX

이전 비밀번호를 재사용하려 할 때 재사용할 수 없는 최근 비밀번호 개수를 설정한다.

PASSWORD_REUSE_MAX는 PASSWORD_REUSE_TIME과 함께 사용해야 한다.

- PASSWORD_REUSE_MAX integer
    - 값의 범위는 0보다 큰 양의 정수여야 한다. 
- PASSWORD_REUSE_MAX UNLIMITED
    - PASSWORD_REUSE_TIME이 UNLIMITED인 경우, 이전 비밀번호 모두를 재사용할 수 있다.
    - PASSWORD_REUSE_TIME이 UNLIMITED가 아닌 경우, 이전 비밀번호 중 어떤 것도 재사용할 수 없다.
- PASSWORD_REUSE_MAX DEFAULT
    - "DEFAULT" profile의 정책을 따른다.

<a id="6009103890c9b7e6"></a>
#### PASSWORD_REUSE_TIME

이전 비밀번호를 재사용하려 할 때, 해당 비밀번호를 재사용할 수 없는 기간을 설정한다.

PASSWORD_REUSE_TIME은 PASSWORD_REUSE_MAX와 함께 사용해야 한다.

- PASSWORD_REUSE_TIME constant_expression 
    - 해당 비밀번호를 재사용할 수 없는 기간 (day)이다.
    - 기본 단위는 일 (day)이다.
    - 테스트 하기 위해 시 (n/24), 분 (n/1440), 초 (n/86400)를 명시할 수 있다.
    - 값의 범위는 1초 (1/86400) ~ 100000 일이다. 
- PASSWORD_REUSE_TIME UNLIMITED
    - PASSWORD_REUSE_MAX가 UNLIMITED인 경우, 이전 비밀번호 모두를 재사용할 수 있다. 
    - PASSWORD_REUSE_MAX가 UNLIMITED가 아닌 경우, 이전 비밀번호 중 어떤 것도 재사용할 수 없다. 
- PASSWORD_REUSE_TIME DEFAULT
    - "DEFAULT" profile의 정책을 따른다.

<a id="6118385512e0db08"></a>
#### PASSWORD_VERIFY_FUNCTION

비밀번호 복잡도 검증 방법을 설정한다.

- PASSWORD_VERIFY_FUNCTION null
    - 비밀번호 복잡도를 검증하지 않는다. 
- PASSWORD_VERIFY_FUNCTION DEFAULT
    - "DEFAULT" profile의 정책을 따른다. 
- PASSWORD_VERIFY_FUNCTION &lt;verify policy&gt;
    - 다음과 같이 비밀번호 복잡도 검증 방법을 지정할 수 있다.
        - KISA_VERIFY_FUNCTION
        - ORA12C_VERIFY_FUNCTION
        - ORA12C_STRONG_VERIFY_FUNCTION
        - VERIFY_FUNCTION_11G 
        - VERIFY_FUNCTION

<a id="f541dc1ed2a4960f"></a>
##### KISA_VERIFY_FUNCTION

Korea Internet & Security Agency (KISA)의 비밀번호 검증 방법이다.

- 8 글자 이상
- 1 개 이상의 문자
- 1 개 이상의 숫자
- 1 개 이상의 특수 문자

<a id="9821d00faa1791ac"></a>
##### ORA12C_VERIFY_FUNCTION

Oracle의 ORA12C_VERIFY_FUNCTION 비밀번호 검증 방법이다.

- 8 글자 이상 
- 1 개 이상의 문자 
- 1 개 이상의 숫자 
- database name을 포함하면 안된다. 
- 사용자 이름 또는 거꾸로 된 사용자 이름을 포함하면 안된다. 
- goldilocks를 포함하면 안된다. 
- oracle을 포함하면 안된다. 
- 다음과 같이 단순한 비밀번호는 사용할 수 없다. 
    - welcome1, database1, account1, user1234, password1, oracle123, computer1, abcdefg1, change_on_intall 
- 이전 비밀번호와 적어도 3 글자는 달라야 한다.

<a id="a62d645d26cf71f9"></a>
##### ORA12C_STRONG_VERIFY_FUNCTION

Oracle의 ORA12C_STRONG_VERIFY_FUNCTION 비밀번호 검증 방법이다.

- 9 글자 이상
- 2 개 이상의 대문자 
- 2 개 이상의 소문자 
- 2 개 이상의 숫자 
- 2 개 이상의 특수 문자 
- 이전 비밀번호와 적어도 4 글자는 달라야 한다.

<a id="a852fb2df1a32086"></a>
##### VERIFY_FUNCTION_11G

Oracle의 VERIFY_FUNCTION_11G 비밀번호 검증 방법이다.

- 8 글자 이상
- 1 개 이상의 문자 
- 1 개 이상의 숫자 
- 사용자 이름을 포함하면 안된다. 
- 이전 비밀번호와 적어도 3 글자는 달라야 한다.

<a id="3280ca9f510b8d02"></a>
##### VERIFY_FUNCTION

Oracle의 VERIFY_FUNCTION 비밀번호 검증 방법이다.

- 사용자 이름과 같으면 안된다. 
- 4 글자 이상 
- 1 개 이상의 문자
- 1 개 이상의 숫자 
- 1 개 이상의 특수문자 
- 다음과 같이 단순한 비밀번호는 사용할 수 없다. 
    - welcome, database, account, user, password, oracle, computer, abcd
- 이전 비밀번호와 적어도 3 글자는 달라야 한다.

<a id="02bf04456cd7476d"></a>
### 설명

<a id="7ab8f8c8f33c31ce"></a>
#### 계정 잠금

계정 잠금에 영향을 주는 parameter는 다음과 같다.

- FAILED_LOGIN_ATTEMPTS
- PASSWORD_LOCK_TIME

예를 들어 다음과 같은 profile과 user를 생성할 경우

```
CREATE PROFILE prof LIMIT
    FAILED_LOGIN_ATTEMPTS 4
    PASSWORD_LOCK_TIME 30;

ALTER USER u1 PROFILE prof;
```

u1 사용자의 login 실패횟수가 네 번을 초과할 경우 30일 동안 계정이 잠긴다.   
그리고 30일이 지나면 계정 잠금이 해제된다.

PASSWORD_LOCK_TIME이 UNLIMITED면, ALTER USER 구문을 사용하여 계정을 명시적으로 잠금 해제해주어야 한다.

```
ALTER USER user1 ACCOUNT UNLOCK;
```

<a id="6ecfca77b2f17aee"></a>
#### 비밀번호 만료

비밀번호 만료에 영향을 주는 parameter는 다음과 같다.

- PASSWORD_LIFE_TIME
- PASSWORD_GRACE_TIME

비밀번호는 다음과 같은 순서로 만료된다.

1. 비밀번호 설정
** 비밀번호가 변경된 순간부터 PASSWORD_LIFE_TIME만큼 경과된 기간이 비밀번호 만료 시점으로 설정된다.
** 비밀번호가 만료된 상태는 OPEN이며, 정상적으로 login 할 수 있다.

2. 만료 시점 이후에 login할 경우
** Login에는 성공하지만 비밀번호의 만료 상태가 EXPIRED (GRACE)가 되며 다음과 같은 warning이 발생한다.
*** ERR-28000(16310): The password will expire in n days
*** ERR-28000(16311): The password will expire soon
*** SQL 표준에서는 password expire 개념을 다루지 않고 있다.
*** 28000은 authentication warning 또는 error의 SQL 표준 상태코드이며, (16310, 16311)은 GOLDILOCKS error code이다.
** Login한 순간부터 PASSWORD_GRACE_TIME만큼 경과된 기간이 비밀번호의 만료 시점으로 재설정된다.

3. 유예기간 이후에 login할 경우
** 비밀번호 만료 상태가 EXPIRED 되어 login 할 수 없으며 다음과 같은 error가 발생한다.
*** ERR-28000(16312): The password has expired
*** SQL 표준에서는 password expire 개념을 다루지 않고 있다.
*** 28000은 authentication warning 또는 error의 SQL 표준 상태코드이며, (16312)는 GOLDILOCKS error code이다.
*** Program을 사용하여 password 재입력을 제어하려면 16312 값의 GOLDILOCKS internal error code를 사용해야 한다.

**비밀번호 만료 상태 전이**

<a id="a2a8a3873951f6f2"></a>
| 단계 | 시점 | Login 성공 여부 | 계정 상태 |
| --- | --- | --- | --- |
| 1 | 비밀번호 변경 | Success | OPEN |
| 2 | PASSWORD_LIFE_TIME 경과 | Success with warning | EXPIRED(GRACE) |
| 3 | PASSWORD_GRACE_TIME 경과 | Error | EXPIRED |

다음 예제를 참조한다.

```
CREATE PROFILE prof LIMIT
   PASSWORD_LIFE_TIME 90
   PASSWORD_GRACE_TIME 3;

ALTER USER u1 PROFILE prof;
```

위 예에서 사용자 u1은 90일이 지난 후 login에 성공하지만 3일 안에 비밀번호가 만료된다는 경고 메시지를 받는다.

3일 안에 비밀번호를 변경하지 않으면 비밀번호는 만료된다.  
비밀번호가 만료되면, login 할 때 새로운 비밀번호를 입력하라는 메시지를 받고 계정 접근이 거부된다.

<a id="1778c7e9c0bd4ec9"></a>
#### 비밀번호 재사용 가능 여부

비밀번호 재사용 가능 여부에 영향을 주는 parameter는 다음과 같다.

- PASSWORD_REUSE_MAX
- PASSWORD_REUSE_TIME

두 parameter의 비밀번호 재사용 가능 여부는 다음 표와 같다.

**비밀번호 재사용 가능 조건**

<a id="c5a6183e005c9e76"></a>
| PASSWORD_REUSE_MAX | PASSWORD_REUSE_TIME | 재사용 가능 조건 |
| --- | --- | --- |
| value | value | PASSWORD_REUSE_TIME과 PASSWORD_REUSE_MAX 조건을 만족해야 한다. |
| value | UNLIMITED | 항상 불가 |
| UNLIMITED | value | 항상 불가 |
| UNLIMITED | UNLIMITED | 항상 가능 |

다음과 같은 profile을 생성한 경우

```
CREATE PROFILE prof LIMIT
   PASSWORD_REUSE_MAX 5
   PASSWORD_REUSE_TIME 3;
```

최근 다섯 개 비밀번호와 최근 3일 이내에 변경한 비밀번호는 재사용할 수 없다.

사용자 u1의 비밀번호 변경 이력이 다음과 같을 경우 현재 비밀번호가 P#_000007이고, 현재 날짜가 2015-08-08 이면 기존 비밀번호의 재사용 가능 여부는 다음과 같다.

**재사용 가능 여부 예**

<a id="a4521595ef558902"></a>
| password | password_date | 재사용 가능 여부 |
| --- | --- | --- |
| P#_000001 | 2015-08-01 | 가능 |
| P#_000002 | 2015-08-02 | 가능 |
| P#_000003 | 2015-08-03 | REUSE_MAX 위배 |
| P#_000004 | 2015-08-04 | REUSE_MAX 위배 |
| P#_000005 | 2015-08-05 | REUSE_MAX, REUSE_TIME 위배 |
| P#_000006 | 2015-08-06 | REUSE_MAX, REUSE_TIME 위배 |
| P#_000007 | 2015-08-07 | REUSE_MAX, REUSE_TIME 위배 |

비밀번호 재사용 가능 여부를 검사하기 위해 누적된 비밀번호 변경 이력은 다음 구문을 사용하여 삭제할 수 있다.

```
ALTER DATABASE CLEAR PASSWORD HISTORY;
```

<a id="8e5a067173144f69"></a>
#### DEFAULT profile

Database를 생성할 때 다음과 같은 "DEFAULT" profile을 자동으로 생성한다. 생성하는 "DEFAULT" profile 의 password parameter 정보는 다음과 같다.

**DEFAULT profile의 구성**

<a id="8f8d83e079d9b777"></a>
| Parameter | Value |
| --- | --- |
| FAILED_LOGIN_ATTEMPTS | 10 |
| PASSWORD_LOCK_TIME | 1 |
| PASSWORD_LIFE_TIME | 180 |
| PASSWORD_GRACE_TIME | 7 |
| PASSWORD_REUSE_MAX | UNLIMITED |
| PASSWORD_REUSE_TIME | UNLIMITED |
| PASSWORD_VERIFY_FUNCTION | NULL |

"DEFAULT" profile의 기본값들은 다음과 같은 특성을 갖는다.

- 계정 잠금
    - 10 (FAILED_LOGIN_ATTEMPTS) 번 연속으로 login에 실패할 경우, 1일 (PASSWORD_LOCK_TIME) 동안 계정을 잠근다.
- 비밀번호 만료
    - 180일 (PASSWORD_LIFE_TIME)이 경과된 후에 7일 (PASSWORD_GRACE_TIME) 간의 유예 기간이 지나면 비밀번호가 만료된다.
- 비밀번호 재사용 가능 여부
    - 이전 비밀번호를 재사용할 수 있다.
- 비밀번호 복잡도 검사
    - 검사하지 않는다.

DEFAULT profile은 삭제할 수 없고 다음 구문으로 변경은 가능하다.

```
ALTER PROFILE DEFAULT LIMIT ...
```

<a id="5db9aa123f27e313"></a>
### 사용 예

다음은 계정 잠금을 제어하는 profile을 생성하는 예이다. 세 번 연속 login에 실패할 경우 3 일동안 계정을 잠근다.

```
gSQL> CREATE PROFILE prof1 LIMIT
        FAILED_LOGIN_ATTEMPTS 3
        PASSWORD_LOCK_TIME 3;

Profile created.

gSQL> COMMIT;

Commit complete.
```

다음은 비밀번호 만료를 제어하는 profile을 생성하는 예이다. 비밀번호의 유효기간은 90 일이며 7 일간의 유예기간을 갖는다.

```
gSQL> CREATE PROFILE prof1 LIMIT
        PASSWORD_LIFE_TIME 90 
        PASSWORD_GRACE_TIME 7;

Profile created.

gSQL> COMMIT;

Commit complete.
```

다음은 비밀번호 재사용 여부를 제어하는 profile을 생성하는 예이다. 다음 예에서는 비밀번호를 변경할 때 이전 비밀번호를 검사하지 않는다.

```
gSQL> CREATE PROFILE prof1 LIMIT
        PASSWORD_REUSE_MAX  DEFAULT
        PASSWORD_REUSE_TIME DEFAULT;

Profile created.

gSQL> COMMIT;

Commit complete.
```

다음은 비밀번호 복잡도 검사를 제어하는 profile을 생성하는 예이다.

```
gSQL> CREATE PROFILE prof1 LIMIT
        PASSWORD_VERIFY_FUNCTION KISA_VERIFY_FUNCTION;

Profile created.

gSQL> COMMIT;

Commit complete.
```

다음은 모든 parameter를 설정하여 profile을 생성하는 예이다.

```
gSQL> CREATE PROFILE prof1 LIMIT
        FAILED_LOGIN_ATTEMPTS 3
        PASSWORD_LOCK_TIME 3
        PASSWORD_LIFE_TIME 90 
        PASSWORD_GRACE_TIME 7
        PASSWORD_REUSE_MAX  DEFAULT
        PASSWORD_REUSE_TIME DEFAULT
        PASSWORD_VERIFY_FUNCTION KISA_VERIFY_FUNCTION;

Profile created.

gSQL> COMMIT;

Commit complete.
```

<a id="ea41c56bdabe9b88"></a>
### 호환성

SQL 표준은 profile에 대한 개념을 다루지 않고 있다.

<a id="604ac6b9a9da0b38"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP PROFILE](#c779f85e72834738)
- [ALTER PROFILE](18-sql-references-a-b.md#aff30be6193ddc88)
- [CREATE USER](#bcf4364429be6a9b)
- [ALTER USER](18-sql-references-a-b.md#7fcf3795e062819a)
- [ALTER DATABASE CLEAR PASSWORD HISTORY](18-sql-references-a-b.md#9d473814ea059a2a)

<a id="b5816864e0a0ee57"></a>
## CREATE SCHEMA

<a id="02b02345441a9c8e"></a>
### 기능

스키마를 정의한다.

<a id="569ce2b091b1387e"></a>
### 구문

```
<schema definition> ::=
    CREATE SCHEMA <schema name clause>
        [ <schema element> [...] ]
    ;

<schema name clause> ::=
      schema_name
    | AUTHORIZATION user_identifier
    | schema_name AUTHORIZATION user_identifier

<schema element> ::=
      <table definition>
    | <view definition>
    | <index definition>
    | <sequence generator definition>
    | <grant privilege statement>
    | <comment statement>
```

<a id="047f05c95c62a516"></a>
### 사용 범위 및 접근 권한

&lt;schema definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 스키마를 생성하려면 CREATE SCHEMA ON DATABASE 권한이 있어야 한다.

- &lt;schema element&gt;가 존재할 경우, 각 &lt;schema element&gt; 구문을 수행하기 위한 권한이 있어야 한다.  
  자세한 내용은 다음 각 구문의 *사용 범위 및 접근 권한*을 참조한다.
    - [CREATE TABLE](#060501387611d25a) 
    - [CREATE VIEW](#6f697c93c59acd84) 
    - [CREATE INDEX](#04e7730c239ac562)
    - [CREATE SEQUENCE](#971516b46cb8bf8d)
    - [GRANT privileges TO](#2efe38e72e090afb)
    - [COMMENT ON name IS](#7db59ad470875e46)

- user_identifier에 해당하는 사용자는 생성한 스키마에 대해 다음과 같은 권한을 갖는다.
    - 생성한 schema_name 스키마의 소유자 
    - &lt;schema element&gt; 절로 생성된 객체의 소유자

- 생성한 스키마에 별도의 권한을 부여하지 않으므로 객체를 생성하려면 적절한 스키마 권한을 부여받아야 한다.  
  스키마 권한의 종류에 대한 내용은 GRANT privileges TO 구문의 [&lt;schema privilege&gt;](#f8b7678b048960ab)를 참조한다.  
  사용 예는 CREATE USER 구문의 [사용 예](#6d2486f2b56e5add)를 참조한다.

<a id="409c128ca1a444ad"></a>
### 구문 규칙 및 파라미터

<a id="a1e8ff5b1eed652b"></a>
#### schema_name

생성할 스키마의 이름이다.  
Database 내에 동일한 스키마 이름이 존재하지 않아야 한다.  
스키마 이름의 길이는 128 바이트보다 작아야 한다.

<a id="bc0a5efa7ddfa3e2"></a>
#### AUTHORIZATION user_identifier

스키마 이름을 생략할 경우, user_identifier와 동일한 이름의 스키마를 생성한다.   
AUTHORIZATION을 지정하지 않을 경우, 구문을 수행한 사용자의 user_identifier가 사용된다.

<a id="a01845107fd8e76c"></a>
#### schema_name AUTHORIZATION user_identifier

생성할 스키마 이름과 스키마의 소유자를 지정한다.   
소유자는 role이나 PUBLIC이 될 수 없다.

<a id="e220c7976f7120c8"></a>
#### &lt;schema element&gt;

스키마를 생성할 때 스키마 내에 함께 생성할 객체를 정의한다.   
schema_element는 나열된 순서대로 실행되며, comma (,) 없이 공백으로만 구분한다.   
생성하는 스키마와 이름이 다른 스키마에는 객체를 정의할 수 없다.

- &lt;grant privilege statement&gt; 구문은 다음 &lt;privilege&gt;에 대해서만 기술할 수 있다.
    - &lt;schema privilege&gt; 
    - &lt;table privilege&gt; 
    - &lt;sequence privilege&gt;

- &lt;comment statement&gt; 구문은 다음 객체에 대해서만 기술할 수 있다.
    - SCHEMA schema_name 
    - TABLE [schema_name].table_name 
    - COLUMN [schema_name].table_name.column_name 
    - INDEX [schema_name].index_name 
    - SEQUENCE [schema_name].sequence_name 
    - CONSTRAINT [schema_name].constraint_name

<a id="0e329da48d4cb06d"></a>
### 설명

스키마는 table, view, index, sequence, constraint와 같은 SQL schema 객체들을 논리적으로 분류하는 객체이다.

GOLDILOCKS에서 user와 schema의 관계는 1 : N 이다. 즉, user가 소유한 schema가 존재하지 않거나 user가 다수의 schema를 소유할 수 있다.

SQL 표준에서는 user, schema, database와 같은 non-schema 객체들의 관계를 명확히 정의하고 있지 않으며, 각 DBMS들은 다음과 같이 non-schema 객체간의 관계를 상이하게 정의하고 있다.

> DBMS에서 user와 schema의 관계   
> 
> 
> - Oracle
>     - User : schema = 1 : 1 
> 
> 
> 
> - DB2 
>     - User : schema = 1 : N 
> 
> 
> 
> - Postgres 
>     - User : schema = 1 : N 
> 
> 
> 
> - MySQL 
>     - Database : schema = 1 : 1 
>     - User는 database (schema)의 하위 객체이다.
> 

<a id="69bd2e1ed34a8249"></a>
### 사용 예

다음은 schema를 생성하는 예이다.

```
gSQL> CREATE SCHEMA s1;

Schema created.
```

다음은 schema를 생성하고 schema의 소유자를 지정하는 예이다.

```
gSQL> CREATE SCHEMA s1 AUTHORIZATION test;

Schema created.
```

다음은 schema와 schema에 속한 객체들을 함께 생성하는 예이다.

```
gSQL> CREATE SCHEMA s1 
             CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) )
             CREATE INDEX idx_t1_id ON t1 ( id )
             COMMENT ON TABLE t1 IS 'comment on s1.t1'
;

Schema created.
```

<a id="34aee7c00c2e6a90"></a>
### 호환성

**SQL 표준 호환성**

<a id="b5241e749ea0f27e"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| S071 | SQL paths in function and type name resolution | X |
| F461 | Named character sets | X |
| F171 | Multiple schemas per user | O |
| T332 | Extended roles | X |

<a id="2400c80dac7f305c"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP SCHEMA](#e766128ab8947c2f)
- [CREATE USER](#bcf4364429be6a9b)
- [CREATE TABLE](#060501387611d25a)
- [CREATE VIEW](#6f697c93c59acd84)
- [CREATE INDEX](#04e7730c239ac562)
- [CREATE SEQUENCE](#971516b46cb8bf8d)
- [GRANT privileges TO](#2efe38e72e090afb)
- [COMMENT ON name IS](#7db59ad470875e46)

<a id="971516b46cb8bf8d"></a>
## CREATE SEQUENCE

<a id="e2eabe8ca2776dbe"></a>
### 기능

시퀀스를 생성한다.

<a id="4a2635ff12b2f117"></a>
### 구문

```
<sequence generator definition> ::=
    CREATE SEQUENCE [schema_name.] sequence_name 
        [ <sequence generator option> [, ...] ]
    ;

<sequence generator option> ::=
      <sequence generator start with option> 
    | <basic sequence generator option>

<sequence generator start with option> ::=
    START WITH integer

<basic sequence generator option> ::=
      <sequence generator increment by option>
    | <sequence generator maxvalue option>
    | <sequence generator minvalue option>
    | <sequence generator cycle option>
    | <sequence generator cache option>

<sequence generator increment by option> ::=
    INCREMENT BY integer

<sequence generator maxvalue option> ::=
      MAXVALUE integer
    | (NO MAXVALUE | NOMAXVALUE)

<sequence generator minvalue option> ::=
      MINVALUE integer
    | (NO MINVALUE | NOMINVALUE)

<sequence generator cycle option> ::=
      CYCLE 
    | (NO CYCLE | NOCYCLE)

<sequence generator cache option> ::=
      CACHE integer
    | (NO CACHE | NOCACHE)
```

<a id="e4d385fc08d92df2"></a>
### 사용 범위 및 접근 권한

&lt;sequence generator definition&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.  
• 시퀀스가 속한 스키마에 대해 (CREATE SEQUENCE 또는 CONTROL SCHEMA) ON SCHEMA   
• CREATE ANY SEQUENCE ON DATABASE

시퀀스의 소유자는 다음과 같이 결정된다.   
• 시퀀스가 속한 스키마의 소유자   
• 시퀀스가 속한 스키마가 PUBLIC 인 경우, 구문을 수행한 사용자

시퀀스 소유자는 USAGE ON SEQUENCE WITH GRANT OPTION 권한을 갖는다.

생성한 시퀀스를 사용하려면 사용자에게 다음 권한 중 하나가 있어야 한다.  
• 해당 시퀀스에 대해 USAGE ON SEQUENCE   
• 시퀀스가 속한 스키마에 대해 (USAGE SEQUENCE 또는 CONTROL SCHEMA) ON SCHEMA   
• USAGE ANY SEQUENCE ON DATABASE

<a id="0a8432d9484a3f3f"></a>
### 구문 규칙 및 파라미터

<a id="2e9817788017adda"></a>
#### sequence_name

생성할 시퀀스의 이름이며 스키마 내에서 유일한 이름이어야 한다.  
schema_name.sequence_name과 같이 시퀀스가 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
시퀀스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="1fb7c2dde8c786da"></a>
#### &lt;sequence generator option&gt;

&lt;sequence generator option&gt;을 사용하지 않을 경우 다음 두 문장은 같은 의미를 갖는다.

- CREATE SEQUENCE test_seq; 
- CREATE SEQUENCE test_seq START WITH 1 INCREMENT BY 1 NO MINVALUE NO MAXVALUE NO CYCLE CACHE 20;

<a id="26f54f44d7e91ddc"></a>
#### &lt;sequence generator start with option&gt;

첫 번째로 생성할 시퀀스 번호를 정의한다.   
오름차순인지 내림차순인지에 따라 다음과 같은 특징을 갖는다.

- 오름차순 시퀀스일 경우 (INCREMENT BY 양수) 
    - 최소값보다 큰 시퀀스 값으로 시작하고자 할 경우에 사용한다. 
    - START WITH 절을 생략할 경우, 기본값은 최소값 (MINVALUE value)이 된다. 
- 내림차순 시퀀스일 경우 (INCREMENT BY 음수) 
    - 최대값보다 작은 시퀀스 값으로 시작하고자 할 경우에 사용한다. 
    - START WITH 절을 생략할 경우, 기본값은 최대값 (MAXVALUE value)이 된다.

<a id="b57ff404d1b58ef9"></a>
#### &lt;sequence generator increment by option&gt;

시퀀스 번호의 간격을 정의한다.   
다음과 같은 제약 및 특징을 갖는다.

- 양수 또는 음수를 사용할 수 있으며, 0은 사용할 수 없다. 
- 간격의 절대값은 MINVALUE와 MAXVALUE의 차이보다 작아야 한다. 
- 양수일 경우 오름차순 시퀀스가 생성되며 음수일 경우 내림차순 시퀀스가 생성된다. 
- INCREMENT BY 절을 생략할 경우, 기본값은 양수 1 이다.

<a id="b0db8227e61b2a72"></a>
#### &lt;sequence generator maxvalue option&gt;

시퀀스로 생성할 수 있는 최대값을 정의한다.

- MAXVALUE integer 
    - 최대값의 범위는 64 bit 정수의 최소값 (−9,223,372,036,854,775,808)에서 64 bit 정수의 최대값(+9,223,372,036,854,775,807) 사이인데
    - START WITH의 값과 같거나 크고, MINVALUE 값보다 커야 한다. 
- NO MAXVALUE | NOMAXVALUE 
    - 최대값은 다음과 같이 정의한다. 
        - 오름차순 시퀀스일 경우, 64 bit 정수의 최대값 (+9,223,372,036,854,775,807)이다. 
        - 내림차순 시퀀스일 경우, -1 이다. 
    - NO MAXVALUE (SQL 표준)와 NOMAXVALUE는 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다. 
- MAXVALUE 와 NO MAXVALUE를 명시하지 않을 경우, 기본값은 NO MAXVALUE 이다.

<a id="a2b95da9a9cd0413"></a>
#### &lt;sequence generator minvalue option&gt;

시퀀스로 생성할 수 있는 최소값을 정의한다.

- MINVALUE integer 
    - 최소값의 범위는 64 bit 정수의 최소값 (−9,223,372,036,854,775,808)에서 64bit 정수의 최대값(+9,223,372,036,854,775,807) 사이인데
    - START WITH의 값과 같거나 작고, MAXVALUE 값보다 작아야 한다. 
- NO MINVALUE | NOMINVALUE 
    - 최소값은 다음과 같이 정의한다. 
        - 오름차순 시퀀스일 경우, 1 이다. 
        - 내림차순 시퀀스일 경우, 64 bit 정수의 최소값 (−9,223,372,036,854,775,808) 이다. 
    - NO MINVALUE (SQL 표준)와 NOMINVALUE는 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다. 
- MINVALUE와 NO MINVALUE를 명시하지 않을 경우, 기본값은 NO MINVALUE 이다.

<a id="c1d43743a27f61c3"></a>
#### &lt;sequence generator cycle option&gt;

시퀀스의 값이 최대값 또는 최소값이 되었을 때, 계속 값을 생성할지 여부를 명시한다.

- CYCLE 
    - 오름차순 시퀀스가 최대값이 되었을 때, 최소값부터 다시 생성한다. 
    - 내림차순 시퀀스가 최소값이 되었을 때, 최대값부터 다시 생성한다. 
- NO CYCLE | NOCYCLE 
    - 최대값 또는 최소값이 되었을 때, 시퀀스 값을 생성할 수 없다. 
    - NO CYCLE (SQL 표준) 과 NOCYCLE 은 동일한 의미의 예약어로 어떤 것을 사용해도 무방하다. 
- CYCLE과 NO CYCLE을 명시하지 않을 경우, 기본값은 NO CYCLE 이다.

<a id="f7a7413a21e8bb1e"></a>
#### &lt;sequence generator cache option&gt;

시퀀스에 빠르게 접근하기 위해 메모리상에 미리 적재할 시퀀스 값의 개수를 정의한다.   
Database를 재구동할 때 메모리상에 적재한 시퀀스 값은 유실되며 적재한 이후의 값부터 시작된다.

- CACHE integer 
    - CACHE 값은 2와 같거나 커야 하며, 
    - CYCLE이 존재할 경우 CACHE 값은 CYCLE의 길이보다 크지 않아야 한다.
        - CYCLE의 길이: CEIL(MAXVALUE - MINVALUE) / ABS(INCREMENT) 
- NO CACHE | NOCACHE 
    - 메모리 상에 시퀀스값을 미리 적재하지 않는다. 
- CACHE/ NO CACHE를 명시하지 않을 경우, 기본값은 CACHE 20 이다.

<a id="286458bdb461a163"></a>
### 설명

생성한 시퀀스 객체의 시퀀스 값은 [NEXTVAL](17-built-in-function-references.md#2c7bda07cb754833) 함수와 [CURRVAL](17-built-in-function-references.md#c26d63f93f4c6a17) 함수를 이용하여 사용할 수 있다.

시퀀스 값은 트랜잭션 속성을 가지지 않으며, 시퀀스 함수를 사용한 SQL 구문에서 에러가 발생하거나 명시적인 ROLLBACK을 수행하더라도 시퀀스 값은 가장 최신 값을 유지한다.

CURRVAL 함수의 경우, session에서 가장 최근에 호출한 NEXTVAL 값을 반환한다.   
이러한 특성을 이용하면 NEXTVAL을 이용하여 한 번 얻은 시퀀스 값을 다른 SQL 문장에 계속 사용할 수 있다.  단, session에서 NEXTVAL을 호출하지 않은 경우에 CURRVAL를 사용하면 에러가 발생한다.

<a id="de9aa641b24f62bb"></a>
### 사용 예

다음과 같이 시퀀스 옵션을 정의하지 않은 seq1 객체는 seq2 객체와 동일한 의미의 오름차순 시퀀스이다.

```
gSQL> CREATE SEQUENCE seq1;

Sequence created.


gSQL> CREATE SEQUENCE seq2 START WITH 1 INCREMENT BY 1 NO MINVALUE NO MAXVALUE NO CYCLE CACHE 20;

Sequence created.
```

다음은 홀수값을 생성하는 시퀀스이다.

```
gSQL> CREATE SEQUENCE seq1 START WITH 1 INCREMENT BY 2;

Sequence created.
```

다음은 0 부터 시작하여 1000 까지 반복적으로 짝수를 생성하는 시퀀스를 생성하는 예이다.

```
gSQL> CREATE SEQUENCE seq1 START WITH 0 MINVALUE 0 MAXVALUE 1000 INCREMENT BY 2 CYCLE;

Sequence created.
```

다음은 -1 부터 시작하는 내림차순 시퀀스를 생성하는 예이다.

```
gSQL> CREATE SEQUENCE seq1 INCREMENT BY -1;

Sequence created.
```

<a id="852e461aabc77686"></a>
### 호환성

SQL 표준에서는 &lt;sequence generator cache option&gt; 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="1233b5bc2fdea57d"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="89a90557205be41d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP SEQUENCE](#bd4f615f4aee0c6b)
- [ALTER SEQUENCE](18-sql-references-a-b.md#ea63a831fa2ae849)
- [NEXTVAL](17-built-in-function-references.md#2c7bda07cb754833)
- [CURRVAL](17-built-in-function-references.md#c26d63f93f4c6a17)

<a id="5ede806fa2325e7c"></a>
## CREATE SYNONYM

<a id="f66ddbb0d38432d9"></a>
### 기능

Synonym을 생성한다. Synonym은 테이블, view, 시퀀스, 또다른 synonym의 대체 이름으로써 이들 대신 다음 구문에서 사용될 수 있다.

- DML: SELECT, INSERT, UPDATE, DELETE, LOCK TABLE, CALL
- DDL: GRANT, REVOKE, COMMENT

<a id="559bf81f4a5fb424"></a>
### 구문

```
<table definition> ::=    
    CREATE [OR REPLACE] [PUBLIC] SYNONYM [schema_name.]synonym_name 
    FOR [schema_name.]object_name
    ;
```

<a id="a7af2f75f873c9b3"></a>
### 사용 범위 및 접근 권한

&lt;synonym definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- PUBLIC을 명시하여 public synonym을 생성하려면 CREATE PUBLIC SYNONYM ON DATABASE 권한이 있어야 한다.

- Public synonym의 소유자는 PUBLIC이며, 생성한 사용자는 아무런 권한을 갖지 않는다.

- Private synonym을 생성하려면 다음 권한 중 하나가 있어야 한다.
    - 해당 스키마에 대해 (CREATE SYNONYM 또는 CONTROL SCHEMA) ON SCHEMA
    - CREATE ANY SYNONYM ON DATABASE

- Private synonym의 소유자는 다음과 같이 결정된다.
    - Private synonym이 속한 스키마의 소유자
    - Private synonym이 속한 스키마가 PUBLIC인 경우, 구문을 수행한 사용자

- Synonym을 생성했어도 기본 객체에 대한 권한이 없으면, 해당 synonym을 사용한 구문을 실행할 수 없다.

- 또한 synonym에 권한을 승인하면 synonym이 지칭하는 기본 객체에 대한 권한이 부여되므로 권한을 승인할 때 주의해야 한다.

<a id="047ab9243f9fbf66"></a>
### 구문 규칙 및 파라미터

<a id="ff854378db9ff4a6"></a>
#### [ OR REPLACE ]

이미 synonym이 존재할 경우, 기존의 synonym을 대체한다.

<a id="f13761a640bc4fbe"></a>
#### [ PUBLIC ]

Public synonym을 만들기 위해 명시한다.   
이 절을 생략하면 private synonym이 생성된다.

<a id="ec789c0893b59cb1"></a>
#### synonym_name

생성할 synonym의 이름이며, 스키마 내에서 유일한 이름이어야 한다.   
schema_name.synonym_name과 같이 synonym이 소속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
Synonym 이름의 길이는 128 바이트보다 작아야 한다.   
Public synonym은 non-schema 객체이다. 따라서 PUBLIC을 명시하여 public synonym을 생성할 때는 스키마 이름을 명시할 수 없다.

<a id="83bad32ed3baee78"></a>
#### object_name

schema_name.object_name과 같이 객체가 소속된 스키마를 명시할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

object_name을 명시할 수 있는 객체 타입은 다음과 같다.

- Table
- View
- Sequence
- 또 다른 synonym

대상 객체의 존재 여부, cycle check, 권한 검사 등은 synonym을 사용한 구문을 수행할 때 실행된다.

<a id="1b5935d5001a12e9"></a>
### 설명

Synonym은 테이블, view, 시퀀스, 다른 synonym의 대체 이름이다.

Synonym을 생성해서 사용하면 기본 객체가 변경되더라도 응용 프로그램 수정 없이 synonym만 재정의 해서 사용하면 되기 때문에 매우 편리하다. 또한 객체의 실제 이름과 스키마를 숨김처리해서 데이터베이스 보안을 개선할 수도 있고, 객체의 긴 이름을 사용하기 쉬운 짧은 이름으로 변경하여 사용성을 높일 수도 있다.

Synonym은 말 그대로 대체 이름이기 때문에, 이를 생성했다고 해서 synonym을 이용하여 해당 객체에 접근할 수는 없다. 해당 객체에 대한 적절한 권한이 있어야만 접근할 수 있다.

Synonym을 사용하여 구문을 수행할 때 객체는 다음과 같은 순서로 접근한다.

1. 해당 이름의 테이블을 찾는다.
2. 테이블이 없을 경우, 해당 이름의 private synonym을 찾는다.
3. Private synonym이 없을 경우, 해당 이름의 public synonym을 찾는다.

```
gSQL> CREATE PUBLIC SYNONYM syn1 FOR u1.t1;

Synonym created.

gSQL> CREATE PUBLIC SYNONYM syn2 FOR syn1;

Synonym created.

gSQL> SELECT * FROM syn2;
```

위 SELECT 구문 예제에서 객체 접근 순서는 다음과 같다.

1. syn2 테이블을 검색하였으나 해당 테이블이 없다.
2. syn2 private synonym을 검색하였으나 해당 synonym이 없다.
3. syn2 public synonym을 검색하여 해당 synonym을 찾았다.
    1. syn1 테이블을 검색하였으나 해당 테이블이 없다.
    2. syn1 private synonym을 검색하였으나 해당 synonym이 없다.
    3. syn1 public synonym을 검색하여 해당 synonym을 찾았다.
        1. u1.t1 테이블을 검색하여 찾았다.

<a id="e0bfdd9d693794a6"></a>
### 사용 예

다음은 private synonym을 생성하는 예이다.

```
gSQL> CREATE SYNONYM MyEmp FOR branch.Employee;

Synonym created.


gSQL> SELECT * FROM MyEmp;
```

다음은 public synonym을 생성하는 예이다.

```
gSQL> CREATE PUBLIC SYNONYM MainEmp FOR main.Employee;

Synonym created.


gSQL> SELECT * FROM MainEmp;
```

<a id="6d83b5f033bbe73b"></a>
### 호환성

SQL 표준에서는 CREATE SYNONYM 구문을 정의하지 않고 있다.

<a id="1d04097442bd31f3"></a>
### 참조

관련 내용은 [DROP SYNONYM](#4f8e6238e2b175b7)을 참조한다.

<a id="060501387611d25a"></a>
## CREATE TABLE

<a id="b995e2b4ea40b81a"></a>
### 기능

테이블을 정의한다.

<a id="17e5b2fd0514414d"></a>
### 구문

```
<table definition> ::=
    CREATE TABLE table_name
        ( <table element> [, ...] )
        [ <table sharding strategy> ]
        [ <table attribute clause> [...] ]
        [ TABLESPACE tablespace_name ]
        [ <table global secondary index clause> ]
    ;

<table element> ::=
      <column definition>
    | <table constraint definition>

<column definition> ::=
    column_name <data type> 
        [ <default clause> | <identity column specification> ]
        [ <column constraint definition> ]

<data type> ::=
      <character string type>
    | <binary string type>
    | <numeric type>
    | <boolean type>
    | <datetime type>
    | <interval type>

<character string type> ::=
      CHARACTER [ ( integer [ <character length units> ] ) ]
    | CHAR [ ( integer [ <character length units> ] ) ]
    | CHARACTER VARYING ( integer [ <character length units> ] )
    | CHAR VARYING ( integer [ <character length units> ] )
    | VARCHAR ( integer [ <character length units> ] )
    | CHARACTER LONG VARYING
    | LONG VARCHAR
  
<character length units> ::=
      CHARACTERS
    | CHAR
    | OCTETS
    | BYTE

<binary string type> ::=
      BINARY [ ( length ) ]
    | BINARY VARYING ( length )
    | VARBINARY ( length )
    | LONG BINARY VARYING
    | LONG VARBINARY

<numeric type> ::=
      <exact numeric type>
    | <approximate numeric type>
    | <native numeric type>

<exact numeric type> ::=
      NUMERIC [ ( precision [, scale ] ) ]
    | SMALLINT
    | INTEGER
    | INT
    | BIGINT

<approximate numeric type> ::=
    | FLOAT [ ( precision ) ]
    | REAL
    | DOUBLE PRECISION

<native numeric type> ::=
      NATIVE_SMALLINT
    | NATIVE_INTEGER
    | NATIVE_BIGINT
    | NATIVE_REAL
    | NATIVE_DOUBLE

<boolean type> ::=
    BOOLEAN

<datetime type> ::=
      DATE
    | TIME [ ( time_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
    | TIMESTAMP [ ( timestamp_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]

<interval type> ::=
    INTERVAL <interval qualifier>

<interval qualifier> ::=
      <non-second primary datetime field> [ ( interval_leading_field_precision ) ]
          TO { <non-second primary datetime field> | SECOND [ ( interval_fractional_seconds_precision ) ] }
    | <non-second primary datetime field> [ ( interval_leading_field_precision ) ]
    | SECOND [ ( interval_leading_field_precision [, interval_fractional_seconds_precision ] ) ]

<non-second primary datetime field> ::=
      YEAR
    | MONTH
    | DAY
    | HOUR
    | MINUTE

<default clause> ::=
    DEFAULT <default option>

<default option> ::=
      constant
    | NULL
    | expression

<identity column specification> ::=
    GENERATED { ALWAYS | BY DEFAULT } AS IDENTITY 
    [ ( <common sequence generator option> [, ...] ) ]

<common sequence generator option> ::=
      START WITH integer_constant
    | <basic sequence generator option>

<basic sequence generator option> ::=
      INCREMENT BY integer_constant 
    | { MAXVALUE integer_constant | NO MAXVALUE }
    | { MINVALUE integer_constant | NO MINVALUE }
    | { CYCLE | NO CYCLE }
    | { CACHE integer_constant | NO CACHE }

<column constraint definition> ::=
    [ CONSTRAINT constraint_name ] <column constraint> [ <constraint characteristics> ]

<column constraint> ::=
      NOT NULL
    | { UNIQUE | PRIMARY KEY } [ <index name clause> [ <index attributes> ] [ TABLESPACE index_tablespace_name ] ]

<index name clause> ::=
    INDEX index_name

<index attributes> ::=
      <index physical attribute clause>
    | STORAGE ( <segment attr clause> [...] )


<table constraint definition> ::=
    [ CONSTRAINT constraint_name ] <table constraint> [ <constraint characteristics> ]

<table constraint> ::=
      <unique constraint definition> [ <index name clause> [ <index attributes> ] [ TABLESPACE index_tablespace_name ] ]

<unique constraint definition> ::=
    { UNIQUE | PRIMARY KEY } ( <key column element> [, ...] )

<key column element> ::=
    column_name [ ASC | DESC ] [ NULLS FIRST | NULLS LAST ]


<table sharding strategy> ::=
      <cloned strategy>
    | <hash sharding strategy>
    | <range sharding strategy>
    | <list sharding strategy>

<cloned strategy> ::=
    CLONED [ <clone placement> ]

<clone placement> ::=
      AT CLUSTER WIDE
    | AT CLUSTER GROUP group_list

<hash sharding strategy> ::=
    SHARDING BY [HASH] ( column_list )
    [ <hash shard count> ]
    [ <hash shard placement> ]

<hash shard count> ::=
    SHARD COUNT integer

<hash shard placement> ::=
      AT CLUSTER WIDE
    | AT CLUSTER GROUP group_list

<range sharding strategy> ::=
    SHARDING BY RANGE ( column_list )
    { <cluster-wide range shard placement> | <group-specific range shard placement> }

<cluster-wide range shard placement> ::=
    AT CLUSTER WIDE
    <range shard definition> [, ...]

<group-specific range shard placement> ::=
    <group-specific range shard definition> [, ...]

<group-specific range shard definition> ::=
    <range shard definition> AT CLUSTER GROUP group_name

<range shard definition> ::=
    SHARD range_name VALUES LESS THAN ( <range value clause> )

<range value clause> ::=
    <range value> [, ...]

<range value> ::=
      constant
    | MAXVALUE

<list sharding strategy> ::=
    SHARDING BY LIST ( column_name )
    { <cluster-wide list shard placement> | <group-specific list shard placement> }

<cluster-wide list shard placement> ::=
    AT CLUSTER WIDE
    <list shard definition> [, ...]

<group-specific list shard placement> ::=
    <group-specific list shard definition> [, ...]

<group-specific list shard definition> ::=
    <list shard definition> AT CLUSTER GROUP group_name

<list shard definition> ::=
      SHARD shard_name VALUES IN ( <list value clause> )

<list value clause> ::=
    <list value> [, ...]

<list value> ::=
      constant
    | NULL
    | DEFAULT


<table attribute clause> ::=
      [ <table physical attribute clause> ]
    | [ STORAGE ( <segment attr clause> [...] ) ]

<table physical attribute clause> ::=
      PCTFREE integer
    | PCTUSED integer
    | INITRANS integer
    | MAXTRANS integer

<index physical attribute clause> ::=
      PCTFREE integer
    | INITRANS integer
    | MAXTRANS integer

<segment attr clause> ::=
      INITIAL <size_clause>
    | NEXT <size_clause>
    | MINSIZE <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]


<constraint characteristics> ::=
      [ NOT ] DEFERRABLE [ <constraint check time> ]
    | <constraint check time> [ [ NOT ] DEFERRABLE ]

<constraint check time> ::=
      INITIALLY DEFERRED 
    | INITIALLY IMMEDIATE

<table global secondary index clause> ::=
      WITH GLOBAL SECONDARY INDEX [ <index attributes> [...] ] [ TABLESPACE tablespace_name ]
    |  WITHOUT GLOBAL SECONDARY INDEX
```

<a id="1c9e32a88e257b5d"></a>
### 사용 범위 및 접근 권한

Database가 stand-alone 인지 아니면 cluster 인지에 따라 다음과 같은 차이가 있다.

- Stand-alone
    - &lt;table sharding strategy&gt;를 정의할 수 없다.
    - &lt;table global secondary index clause&gt;를 정의할 수 없다.
- Cluster
    - UNIQUE, PRIMARY KEY 제약 조건을 정의할 때 모든 sharding key를 포함해야 한다.
    - 지연가능한 제약 조건을 정의할 수 없다.

&lt;table definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블이 생성될 스키마에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 스키마에 대해 (CREATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - CREATE ANY TABLE ON DATABASE

- 테이블이 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
    - USAGE TABLESPACE ON DATABASE

- 함께 생성한 제약 조건이 있을 경우, 제약 조건이 생성될 스키마에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 스키마에 대해 (ADD CONSTRAINT 또는 CONTROL SCHEMA) ON SCHEMA 
    - ALTER ANY TABLE ON DATABASE

- 함께 생성한 제약 조건이 key 제약 조건일 경우, 인덱스가 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
    - USAGE TABLESPACE ON DATABASE

- 테이블의 소유자는 다음과 같이 결정된다.
    - 테이블이 속한 스키마의 소유자
    - 테이블이 속한 스키마가 PUBLIC일 경우, 구문을 수행한 사용자

- 테이블 소유자는 생성한 테이블에 대해 다음과 같은 권한을 갖는다.
    - 해당 테이블에 대한 권한 
        - SELECT ON TABLE WITH GRANT OPTION 
        - INSERT ON TABLE WITH GRANT OPTION 
        - UPDATE ON TABLE WITH GRANT OPTION 
        - DELETE ON TABLE WITH GRANT OPTION 
        - TRIGGER ON TABLE WITH GRANT OPTION 
        - REFERENCES ON TABLE WITH GRANT OPTION 
        - LOCK ON TABLE WITH GRANT OPTION 
        - INDEX ON TABLE WITH GRANT OPTION 
        - ALTER ON TABLE WITH GRANT OPTION 
    - 해당 테이블의 모든 column에 대한 권한 
        - SELECT(columns) ON TABLE WITH GRANT OPTION 
        - INSERT(columns) ON TABLE WITH GRANT OPTION 
        - UPDATE(columns) ON TABLE WITH GRANT OPTION 
        - REFERENCES(columns) ON TABLE WITH GRANT OPTION 
    - 함께 생성한 제약 조건에 대한 권한 
        - 제약 조건의 소유자 
        - 제약 조건과 함께 생성된 인덱스의 소유자

&lt;table sharding strategy&gt; 구문은 cluster system에서 사용할 수 있다.

<a id="243b2f8adf97c455"></a>
### 구문 규칙 및 파라미터

<a id="d83b67dfcf8ea14b"></a>
#### table_name

생성할 테이블의 이름이며, 스키마 내에서 유일한 이름이어야 한다.   
schema_name.table_name과 같이 테이블이 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
테이블 이름의 길이는 128 바이트보다 작아야 한다.

<a id="7d745366530cb2b2"></a>
#### &lt;column definition&gt;

테이블을 구성할 column을 정의한다.   
테이블은 하나 이상의 column에 대한 정의를 포함해야 한다.   
Column의 데이터 타입, 기본값, 자동 생성 값, 제약 조건 등을 기술할 수 있다.

<a id="0c91c4d542f99920"></a>
#### column_name

테이블을 구성할 column의 이름으로 각 column은 테이블 내에서 유일한 이름을 가져야 한다.   
Column 이름의 길이는 128 바이트보다 작아야 한다.

<a id="a73302f778a3d3c9"></a>
#### &lt;data type&gt;

- &lt;character string type&gt; 
- &lt;binary string type&gt; 
- &lt;numeric type&gt; 
- &lt;exact numeric type&gt; 
- &lt;approximate numeric type&gt; 
- &lt;boolean type&gt; 
- &lt;datetime type&gt; 
- &lt;interval type&gt; 
- &lt;interval qualifier&gt; 
- &lt;non-second primary datetime field&gt;

Column의 데이터 타입을 정의한다.  
자동 생성 값을 갖는 (&lt;identity column specification&gt;) column을 정의할 경우, SMALLINT, INTEGER, BIGINT 타입 중 하나의 데이터 타입을 사용해야 한다.  
데이터 타입과 관련한 자세한 내용은 [Data Type](11-sql-elements.md#e0bf6effdba79789) 정의를 참조한다.

<a id="c06883f281ad85bc"></a>
#### &lt;character length units&gt;

Character 타입의 문자 하나당 길이 단위를 지정한다.

- CHARACTERS/ CHAR는 문자 하나의 최대 byte만큼을 문자 하나의 길이로 지정한다. 따라서 한글과 같은 multi-bytes 문자 하나의 길이도 1로 처리한다.
- OCTETS/ BYTE는 1 byte를 문자 하나의 길이로 지정한다. 따라서 한글과 같은 multi-bytes 문자 하나의 길이는 multi-bytes로 처리한다.
- 생략할 경우 database를 생성할 때 사용된 CHAR_LENGTH_UNITS 속성값을 따른다.

SQL 표준의 기본값은 CHARACTERS이다.

> 다른 DBMS의 char length unit 기본값은 다음과 같다.
> 
> - Oracle, DB2: OCTETS
> - MS-SQL, MySQL, PostgreSQL: CHARACTERS
> 

<a id="51ad92642f22e5a9"></a>
#### [ &lt;default clause&gt; | &lt;identity column specification&gt; ]

Column의 기본값을 명시한다.   
&lt;default clause&gt;와 &lt;identity column specification&gt;은 함께 사용할 수 없다.   
모두 생략할 경우, 기본값은 NULL이다.

<a id="3b1e389e68d3d8cd"></a>
#### &lt;default clause&gt;

DEFAULT 절은 INSERT, UPDATE와 같은 구문에 DEFAULT가 명시되거나 해당 column 이름이 생략될 경우에 사용할 기본값을 정의한다.

- DEFAULT 절이 사용되는 경우 
    - 예: CREATE TABLE t1 ( id INTEGER, name VARCHAR(32) DEFAULT 'anonymous' ); 
    - Column이 생략된 경우 
        - INSERT INTO t1(id) VALUES ( 1 ); 
        - INSERT INTO t1(id) SELECT id FROM other_table; 
    - DEFAULT를 명시한 경우 
        - INSERT INTO t1 DEFAULT VALUES; 
        - INSERT INTO t1 VALUES ( 2, DEFAULT ); 
        - UPDATE t1 SET name = DEFAULT;

DEFAULT expression의 데이터 타입은 column의 데이터 타입과 호환 가능해야 한다.  
타입이 호환되지 않거나 expression이 valid 하지 않으면 에러가 발생한다.

```
--# result: error
CREATE TABLE t1 ( c1 INTEGER DEFAULT 1 / 0 );

ERR-22012(12122): divisor is equal to zero


--# result: success
CREATE TABLE t1 ( c1 INTEGER DEFAULT 1 / 1 );

Table created.
```

DEFAULT expression은 모든 built-in 함수를 사용할 수 있지만 다음은 사용할 수 없다.

- 논리연산자 (AND, OR, NOT), 비교 연산자 (=, >, ..)
- Stored function 
- Column 이름 
- Subquery expression

<a id="4bc86294cae245fa"></a>
#### &lt;identity column specification&gt;

자동 생성값을 갖는 column을 정의한다.

테이블은 하나의 identity column 만 가질 수 있다.  
NOT NULL 제약 조건을 명시하지 않아도 identity column은 not nullable column이 된다.

&lt;identity column specification&gt; 절은 DEFAULT 절과 함께 기술할 수 없다.  
&lt;identity column specification&gt; 절은 DEFAULT 절과 마찬가지로 INSERT, UPDATE 구문에서 DEFAULT를 명시하거나 해당 column 이름이 생략될 경우에 사용할 기본값을 정의한다.

생성 방식은 다음과 같이 정의된다.

- GENERATED BY DEFAULT AS IDENTITY   
  사용자가 값을 지정한 경우 이를 적용하나, DEFAULT 절과 같이 기본값이 사용되어야 하는 경우 자동값을 생성한다. 
    - CREATE TABLE t1 ( id INTEGER GENERATED BY DEFAULT AS IDENTITY, name VARCHAR(32) ); 
    - (O) INSERT INTO t1 VALUES ( 12345, 'GOLDILOCKS'); 
        - 사용자가 지정한 값(12345) 를 입력한다.
    - (O) INSERT INTO t1(name) VALUES ( 'GOLDILOCKS'); 
        - id column에 자동 생성값이 입력된다.
    - (O) INSERT INTO t1(id, name) SELECT other_id, other_name FROM other_table;
        - 사용자가 지정한 값을 입력한다.
    - (O) INSERT INTO t1(name) SELECT other_name FROM other_table;
        - id column에 자동 생성값이 입력된다.
    - (O) UPDATE t1 SET id = 10000 WHERE id = 12345;
        - 사용자가 지정한 값을 입력한다.
    - (O) UPDATE t1 SET id = DEFAULT WHERE id = 12345;
        - id column에 자동 생성값이 입력된다.

- GENERATED ALWAYS AS IDENTITY  
  사용자가 값을 지정할 수 없으며, DEFAULT 절과 같이 기본값을 생성할 수 있어야 한다. 
    - CREATE TABLE t1 ( id INTEGER GENERATED ALWAYS AS IDENTITY, name VARCHAR(32) ); 
    - (X) INSERT INTO t1 VALUES ( 12345, 'GOLDILOCKS'); 
        - 에러, 사용자가 값을 지정할 수 없다.
    - (O) INSERT INTO t1(name) VALUES ( 'GOLDILOCKS' ); 
        - id column에 자동 생성값이 입력된다.
    - (X) INSERT INTO t1(id, name) SELECT other_id, other_name FROM other_table;
        - 에러, 사용자가 값을 지정할 수 없다.
    - (O) INSERT INTO t1(name) SELECT other_name FROM other_table;
        - id column에 자동 생성값이 입력된다.
    - (X) UPDATE t1 SET id = 10000 WHERE id = 12345;
        - 에러, 사용자가 값을 지정할 수 없다.
    - (O) UPDATE t1 SET id = DEFAULT WHERE id = 12345;
        - id column에 자동 생성값이 입력된다.

identity column 생성 옵션인 &lt;common sequence generator option&gt;과 &lt;basic sequence generator option&gt;에 대한 자세한 내용은 [CREATE SEQUENCE](#971516b46cb8bf8d) 구문을 참조한다.

<a id="c20696a8daaed7d8"></a>
#### &lt;column constraint definition&gt;

Column에 대해 다음과 같은 제약 조건을 정의한다.

- NOT NULL 제약 조건 
- UNIQUE 제약 조건 
- PRIMARY KEY 제약 조건

<a id="795257f3eec58cd6"></a>
#### constraint_name

제약 조건의 이름이며 생략 가능하다.

constraint_name을 생략할 경우 다음과 같은 형태로 제약 조건 이름을 자동으로 설정한다. 자동 생성하는 이름이 중복될 경우, constraint_name을 명시적으로 부여해야 한다.

- NOT NULL 제약 조건 
    - "table_name" + "_" + "NOT_NULL" + "_" + "column_name" 
- UNIQUE 제약 조건 
    - "table_name" + "_" + "UNIQUE" + "_" + "column_name" 
- PRIMARY KEY 제약 조건 
    - "table_name" + "_" + "PRIMARY_KEY"

제약 조건의 이름은 128 바이트보다 작아야 한다.

<a id="02b4d28e02f84925"></a>
#### NOT NULL 제약 조건

Column 값으로 NULL 값을 허용하지 않는다.

<a id="47421604bddea579"></a>
#### UNIQUE 제약 조건

Column 값으로 동일한 값을 허용하지 않는다.   
단, NULL 값은 허용한다.

<a id="c444c89c6d7c5245"></a>
#### PRIMARY KEY 제약 조건

Column 값으로 NULL 값이나 동일한 값을 허용하지 않는다.   
하나의 테이블에 하나의 PRIMARY KEY 제약 조건을 정의할 수 있다.

<a id="5efa3bbe89afed69"></a>
#### &lt;index name clause&gt;

UNIQUE 제약 조건, PRIMARY KEY 제약 조건을 정의할 때 생성되는 인덱스의 이름을 정의한다.

- INDEX index_name 
    - 제약 조건을 위한 인덱스의 이름을 정의한다. 
    - 스키마 이름과 함께 사용할 수 없으며, 제약 조건과 동일한 스키마에 생성된다.

UNIQUE 제약 조건, PRIMARY KEY 제약 조건을 정의할 때 INDEX 절을 생략할 경우에는 제약 조건에 부합하는 인덱스를 자동으로 생성한다.  
자동 생성되는 인덱스 이름으로는 "constraint_name" + "_INDEX"가 부여된다.

- &lt;index attributes&gt; 
    - 생성할 인덱스의 물리적 속성을 지정한다. 
    - 자세한 내용은 [CREATE INDEX](#04e7730c239ac562) 구문을 참조한다. 
- TABLESPACE index_tablespace_name 
    - 인덱스를 생성할 tablespace 를 지정한다. 
    - 자세한 내용은 [CREATE INDEX](#04e7730c239ac562) 을 참조한다.

<a id="5d9d3af3b21cbfb2"></a>
#### &lt;table constraint definition&gt;

&lt;unique constraint definition&gt;

- 테이블을 정의할 때의 제약 조건은 구문 내의 위치에 따라 두 가지 방법으로 나뉜다.
    - Column을 정의할 때 column 제약 정의 (&lt;column constraint definition&gt;)를 사용하여 하나의 column에 대한 제약 조건을 기술할 수 있다.
    - 이에 반해, 테이블 제약 정의 (&lt;table constraint definition&gt;)는 column 정의와 별도로 기술할 수 있으며, 하나 이상의 column에 대한 제약 조건을 기술할 수 있다.

테이블 제약 정의는 column 제약 정의와 비교하여 다음과 같은 구문상의 차이가 있다.

- NOT NULL 제약 
    - 테이블 제약 정의를 통해 명시할 수 없다. 
- Column 제약 정의와 달리 column을 명시해야 한다. 
    - UNIQUE 제약 &lt;unique constraint definition&gt; 
        - UNIQUE ( column_name [, ...] ) 
    - PRIMARY KEY 제약 &lt;unique constraint definition&gt; 
        - PRIMARY KEY ( column_name [, ...] )

<a id="6570eeb04be922e3"></a>
#### key column element

Key 대상이 되는 column을 지정한다.

- Column name 
    - Key를 생성할 column 이름이다.
- ASC | DESC 
    - ASC: 오름차순으로 정렬한다. 
    - DESC: 내림차순으로 정렬한다. 
    - 명시하지 않을 경우, 기본값은 ASC 이다. 
- NULLS FIRST | NULLS LAST 
    - NULLS FIRST: NULL이 아닌 값들보다 앞에 위치한다. 
    - NULLS LAST: NULL이 아닌 값들보다 뒤에 위치한다. 
    - 명시하지 않을 경우, 기본값은 NULLS LAST 이다.

<a id="a909ac87ebe36e25"></a>
#### &lt;table sharding strategy&gt;

테이블의 sharding 정책을 정의한다.   
다음과 같은 네 가지 정책 중 하나로 정의할 수 있다.

- &lt;cloned strategy&gt; 
- &lt;hash sharding strategy&gt; 
- &lt;range sharding strategy&gt; 
- &lt;list sharding strategy&gt;

생략할 경우 [DEFAULT_SHARDING](../part-02-administration-manual/10-server-property.md#e967b037fd858e4a) 프로퍼티 값에 의해 결정된다.

- DEFAULT_SHARDING 값이 0 인 경우
    - &lt;cloned strategy&gt;
- DEFAULT_SHARDING 값이 1 인 경우
    - &lt;hash sharding strategy&gt;

<a id="a47526873cf2f56b"></a>
#### &lt;cloned strategy&gt;

테이블의 모든 data를 복제한다.

<a id="15445a82bc02ba68"></a>
#### &lt;clone placement&gt;

Clone의 배치 정책을 정의한다.

- AT CLUSTER WIDE 
    - Cluster system의 모든 cluster group의 모든 cluster member에 clone을 배치한다. 
    - Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#149294331f00fde7) 구문을 사용하여 clone을 재배치할 수 있다. 
- AT CLUSTER GROUP group_list 
    - 지정한 cluster group들의 모든 cluster member에 clone을 배치한다. 
    - 지정된 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#149294331f00fde7) 구문을 사용하여 clone을 재배치할 수 있다. 
    - Cluster group 추가는 clone의 재배치에 영향을 주지 않는다.
- 생략할 경우, 기본값은 AT CLUSTER WIDE이다.

<a id="56d9a8b3dd930feb"></a>
#### &lt;hash sharding strategy&gt;

테이블의 data를 sharding key의 hash 값을 기준으로 shard를 분할한다.

<a id="452685c633bb410b"></a>
#### SHARDING BY [HASH] ( column_list )

Hash sharding을 위한 sharding key를 정의한다.

- Column을 32 개까지 나열할 수 있다. 
- 동일한 column은 사용할 수 없다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column은 사용할 수 없다.

<a id="751bd9c0196fe9c7"></a>
#### &lt;hash shard count&gt;

분할할 hash shard의 개수를 정의한다.   
Shard의 개수는 1부터 512까지 정의할 수 있다.   
생략할 경우 기본값은 24이다.

<a id="b3e5c088636f767e"></a>
#### &lt;hash shard placement&gt;

Hash shard의 배치 정책을 정의한다.

- AT CLUSTER WIDE 
    - Cluster system의 모든 cluster group의 모든 cluster member에 shard 들을 배치한다. 
    - Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#149294331f00fde7) 구문을 사용하여 shard들을 재배치할 수 있다. 
- AT CLUSTER GROUP group_list 
    - 지정한 cluster group들의 모든 cluster member에 hash shard들을 배치한다. 
    - group_list의 개수는 &lt;hash shard count&gt;의 값과 같거나 작아야 한다. 
    - range shard, list shard와 달리 hash shard는 특정 shard가 배치될 cluster group을 지정할 수 없으며, system이 자동으로 shard 들을 배치할 cluster group을 결정한다. 
    - 지정한 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#149294331f00fde7) 구문을 사용하여 shard를 재배치할 수 있다. 
    - Cluster group 추가는 hash shard의 재배치에 영향을 주지 않는다.
- 생략할 경우, 기본값은 AT CLUSTER WIDE 이다.

<a id="874d0ae982cc9588"></a>
#### &lt;range sharding strategy&gt;

테이블의 data를 sharding key의 범위값을 기준으로 shard 분할한다.

<a id="755ef702bb886ab9"></a>
#### SHARDING BY RANGE ( column_list )

Range sharding을 위한 sharding key를 정의한다.

- Column을 32 개까지 나열할 수 있다. 
- 동일한 column은 사용할 수 없다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column은 사용할 수 없다.

<a id="d2d49b2d8b5e5eed"></a>
#### &lt;cluster-wide range shard placement&gt;

Range shard들을 cluster system의 모든 cluster group으로 자동으로 배치한다.  
&lt;range shard definition&gt;을 기술하기 전에 AT CLUSTER WIDE 구문을 기술한다.  
Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#149294331f00fde7) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.

- Range sharded table을 생성한다.
- 기존 cluster group인 g1, g2, g3에 여섯 개의 shard들을 배치한다.

```
CREATE TABLE t1 
(
   id   INTEGER,
   name VARCHAR(32)
)
SHARDING BY RANGE (id)
    AT CLUSTER WIDE
    SHARD s1 VALUES LESS THAN ( 200000 ),
    SHARD s2 VALUES LESS THAN ( 400000 ),
    SHARD s3 VALUES LESS THAN ( 500000 ),
    SHARD s4 VALUES LESS THAN ( 600000 ),
    SHARD s5 VALUES LESS THAN ( 800000 ),
    SHARD s6 VALUES LESS THAN ( MAXVALUE )
;
```

- Cluster group을 추가한다.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- Range shard를 재배치한다.
- 추가된 g4를 포함하여 cluster group g1, g2, g3, g4에 여섯 개의 shard들을 재배치한다.

```
ALTER TABLE t1 REBALANCE;
```

<a id="c3b3471fc906c4d5"></a>
#### &lt;group-specific range shard placement&gt;

Range shard들을 지정한 cluster group에 배치한다.  
&lt;range shard definition&gt;과 함께 해당 shard를 배치할 AT CLUSTER GROUP group_name 구문을 기술한다.  
지정한 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#149294331f00fde7) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.  
Cluster group 추가는 range shard의 재배치에 영향을 주지 않는다.

- Range sharded table을 생성한다.
- 각 range shard들을 지정한 cluster group에 배치한다.

```
CREATE TABLE t1 
(
   id   INTEGER,
   name VARCHAR(32)
)
SHARDING BY RANGE (id)
    SHARD s1 VALUES LESS THAN ( 200000 )   AT CLUSTER GROUP g1,
    SHARD s2 VALUES LESS THAN ( 400000 )   AT CLUSTER GROUP g2,
    SHARD s3 VALUES LESS THAN ( 500000 )   AT CLUSTER GROUP g3,
    SHARD s4 VALUES LESS THAN ( 600000 )   AT CLUSTER GROUP g2,
    SHARD s5 VALUES LESS THAN ( 800000 )   AT CLUSTER GROUP g3,
    SHARD s6 VALUES LESS THAN ( MAXVALUE ) AT CLUSTER GROUP g1
;
```

- Cluster group을 추가한다.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- Range shard를 재배치한다.
- 새로 생성한 cluster group g4 에는 shard가 배치되지 않는다

```
ALTER TABLE t1 REBALANCE;
```

<a id="6090eeb1cbea9bd0"></a>
#### &lt;range shard definition&gt;

SHARD range_name은 테이블 내에서 유일해야 한다.

최대 512 개의 &lt;range shard definition&gt;을 정의할 수 있다.

나열된 &lt;range shard definition&gt;은 &lt;range value clause&gt;의 순서로 정렬되며 서로 다른 &lt;range value clause&gt;를 사용해야 한다.

모든 값을 MAXVALUE로 정의한 &lt;range shard definition&gt;을 MAX shard라 한다.   
MAX shard는 반드시 존재해야 하며, 하나만 존재해야 한다.

- MAX shard를 포함해야 한다.

```
gSQL>
CREATE TABLE t1 
(
   id INTEGER,
   name VARCHAR(32)
)
SHARDING BY RANGE (id)
   AT CLUSTER WIDE
   SHARD s1 VALUES LESS THAN ( 100000 ),
   SHARD s2 VALUES LESS THAN ( 200000 ),
   SHARD s3 VALUES LESS THAN ( MAXVALUE )
;

Table created.
```

- MAX shard 를 포함하지 않은 경우 error가 발생한다.

```
gSQL>
CREATE TABLE t1 
(
   id INTEGER,
   name VARCHAR(32)
)
SHARDING BY RANGE (id)
   AT CLUSTER WIDE
   SHARD s1 VALUES LESS THAN ( 100000 ),
   SHARD s2 VALUES LESS THAN ( 200000 ),
   SHARD s3 VALUES LESS THAN ( 300000 )
;

ERR-42000(16377): MAX shard not defined : 
   SHARD s3 VALUES LESS THAN ( 300000 )
   *
ERROR at line 10:
```

<a id="3229af9595a82ce9"></a>
#### &lt;range value clause&gt;

&lt;range value&gt;는 상수값이거나 최대값을 의미하는 MAXVALUE 여야 한다.

NULL 값은 &lt;range value&gt;로 사용할 수 없다.

- (O) SHARD s1 VALUES LESS THAN ( 1 ) 
- (O) SHARD s2 VALUES LESS THAN ( 1 + 1 ) 
- (O) SHARD s3 VALUES LESS THAN ( MAXVALUE ) 
- (X) SHARD s4 VALUES LESS THAN ( SYSDATE ) 
- (X) SHARD s5 VALUES LESS THAN ( NULL )

MAXVALUE는 다른 값보다 항상 큰 값을 의미하며 null 값을 포함한다.

Sharding key가 여러 개인 경우 MAXVALUE 이후에는 MAXVALUE만 지정할 수 있다.

- (O) SHARD s1 VALUES LESS THAN ( 100, MAXVALUE ) 
- (X) SHARD s2 VALUES LESS THAN ( MAXVALUE, 100 ) 
- (O) SHARD s3 VALUES LESS THAN ( MAXVALUE, MAXVALUE )

다수의 column을 사용하여 sharding key를 정의한 경우 다음 SHARD s3와 같이 모든 값을 MAXVALUE 로 나열한 MAX shard가 반드시 하나만 존재해야 한다.

```
CREATE TABLE t1 
(
   id INTEGER,
   name VARCHAR(32)
)
SHARDING BY RANGE (id, name)
   AT CLUSTER WIDE
   SHARD s1 VALUES LESS THAN ( 100000, MAXVALUE ),
   SHARD s2 VALUES LESS THAN ( 200000, 20000 ),
   SHARD s3 VALUES LESS THAN ( MAXVALUE, MAXVALUE )
;
```

<a id="7dad47bf8622e0ee"></a>
#### &lt;list sharding strategy&gt;

테이블의 data를 sharding key 의 나열값을 기준으로 shard를 분할한다.

<a id="f17267f8588e5b48"></a>
#### SHARDING BY LIST ( column_name )

List sharding을 위한 sharding key를 정의한다.

- 하나의 column만 사용할 수 있다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column을 사용할 수 없다.

<a id="06661aa2c668fca8"></a>
#### &lt;cluster-wide list shard placement&gt;

Cluster system의 모든 cluster group에 list shard들을 자동으로 배치한다.  
&lt;list shard definition&gt;을 기술하기 전에 AT CLUSTER WIDE 구문을 기술한다.  
Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#149294331f00fde7) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.

- List sharded table을 생성한다.
- 기존 cluster group인 g1, g2, g3에 다섯 개의 shard들을 배치한다.

```
CREATE TABLE city 
(
   id   INTEGER,
   name VARCHAR(32)
)
SHARDING BY LIST (name)
    AT CLUSTER WIDE
    SHARD s1 VALUES IN ( 'SEOUL' ),
    SHARD s2 VALUES IN ( 'PUSAN', 'ULSAN', 'DAEGU' ),
    SHARD s3 VALUES IN ( 'DAEJEON', 'GWANGJU' ),
    SHARD s4 VALUES IN ( 'ANSAN', 'GOYANG' ),
    SHARD s5 VALUES IN ( DEFAULT )
;
```

- Cluster group을 추가한다.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- List shard를 재배치한다.
- 추가된 g4를 포함하여 g1, g2, g3, g4 cluster group에 다섯 개의 shard들을 재배치한다.

```
ALTER TABLE t1 REBALANCE;
```

<a id="d7d6c4c49bec1c95"></a>
#### &lt;group-specific list shard placement&gt;

List shard들을 지정한 cluster group에 배치한다.  
&lt;list shard definition&gt;과 함께 해당 shard를 배치할 AT CLUSTER GROUP group_name 구문을 기술한다.  
지정한 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#149294331f00fde7) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.  
Cluster group 추가는 list shard의 재배치에 영향을 주지 않는다.

- List sharded table을 생성한다.
- 각 list shard를 지정한 cluster group에 배치한다.

```
CREATE TABLE city 
(
   id   INTEGER,
   name VARCHAR(32)
)
SHARDING BY LIST (name)
    SHARD s1 VALUES IN ( 'SEOUL' )                   AT CLUSTER GROUP g1,
    SHARD s2 VALUES IN ( 'PUSAN', 'ULSAN', 'DAEGU' ) AT CLUSTER GROUP g2,
    SHARD s3 VALUES IN ( 'DAEJEON', 'GWANGJU' )      AT CLUSTER GROUP g3,
    SHARD s4 VALUES IN ( 'ANSAN', 'GOYANG' )         AT CLUSTER GROUP g2,
    SHARD s5 VALUES IN ( DEFAULT )                   AT CLUSTER GROUP g1
;
```

- Cluster group을 추가한다.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- List shard를 재배치한다.
- 추가한 cluster group g4에 shard가 배치되지 않는다.

```
ALTER TABLE t1 REBALANCE;
```

<a id="d5d6b8837ddd675a"></a>
#### &lt;list shard definition&gt;

LIST list_name은 테이블 내에서 유일해야 한다.

최대 512개의 &lt;list shard definition&gt;을 정의할 수 있다.   
나열된 &lt;list shard definition&gt;의 모든 &lt;list value&gt; 값이 서로 달라야 한다.

DFFAULT는 나열된 모든 &lt;list value&gt;를 제외한 나머지 값이다.   
DEFAULT는 다른 값과 함께 지정할 수 없다.   
DEFAULT를 포함하는 shard를 DEFAULT shard라고 한다.

DEFAULT shard는 반드시 존재해야 하며, 하나만 존재해야 한다.

- DEFAULT shard 를 포함해야 함

```
gSQL>
CREATE TABLE t1 
(
   category INTEGER,
   name     VARCHAR(32)
)
SHARDING BY LIST (category)
   AT CLUSTER WIDE
   SHARD s1 VALUES IN ( 1, 3, 5, 7 ),
   SHARD s2 VALUES IN ( 2, 4, 6, 8 ),
   SHARD s3 VALUES IN ( DEFAULT )
;

Table created.
```

- DEFAULT shard를 포함하지 않는 경우 error가 발생한다.

```
gSQL>

CREATE TABLE t1 
(
   category INTEGER,
   name     VARCHAR(32)
)
SHARDING BY LIST (category)
   AT CLUSTER WIDE
   SHARD s1 VALUES IN ( 1, 3, 5, 7 ),
   SHARD s2 VALUES IN ( 2, 4, 6, 8 ),
   SHARD s3 VALUES IN ( 9, 10 )
;

ERR-42000(16385): DEFAULT shard not defined : 
   SHARD s3 VALUES IN ( 9, 10 )
   *
ERROR at line 10:
```

<a id="7ce63252c05d338e"></a>
#### &lt;list value clause&gt;

&lt;list value&gt;는 상수값이어야 한다.   
NULL 값이나 DEFAULT를 &lt;list value&gt;로 사용할 수 있다.

DEFAULT는 다른 값과 함께 지정할 수 없다.

- (O) SHARD s1 VALUES IN ( 1, 1 + 1, 3, 4 ) 
- (O) SHARD s2 VALUES IN ( 5, 6, 7, NULL ) 
- (O) SHARD s3 VALUES IN ( DEFAULT ) 
- (X) SHARD s4 VALUES IN ( DEFAULT, 8, 9, 10 ) 
- (X) SHARD s5 VALUES IN ( current_timestamp, systimestamp ) 
- (X) SHARD s6 VALUES IN ( c1, c2 )

<a id="337e3e2fbd13ebdc"></a>
#### &lt;table physical attribute clause&gt;

테이블의 물리적 속성 정보를 정의한다.

- PCTFREE integer 
    - 정의 
        - 페이지 내에서 row를 수정하거나 업데이트 할 때 행 크기가 증가될 것에 대비하여 예약된 공간이다.
        - 초기에는 이 공간을 제외하고 입력된다. 
        - PCTFREE가 부족하면 데이터를 수정하거나 업데이트 할 때 행 이전 (ROW MIGRATION)이 발생한다.
    - 0 에서 99 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기본값은 10이다.

- PCTUSED integer 
    - 정의 
        - 새로운 row가 페이지에 추가되기 전에 row 데이터와 오버헤드에 대해 사용될 수 있는 페이지의 최소 퍼센트이다. 
        - 즉, 기존 데이터의 수정이나 삭제 등으로 인해 PCTUSED보다 값이 작아지면 이 페이지들에 한하여 입력이 가능하다. 
    - 0 에서 99 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기본값은 40 이다.

- INITRANS integer 
    - 정의 
        - 페이지에 동시 접근할 수 있는 초기 트랜잭션의 개수이다. 
        - 인덱스에 접근하는 사용자의 수가 적을 경우에는 INITRANS를 낮게 설정하고, 동시에 접근하는 사용자가 많을 경우에는 INITRANS를 높게 설정한다. 
        - 필요한 경우 설정된 MAXTRANS까지 자동으로 늘어난다. 
    - 1 부터 32 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기본값은 4 다.

- MAXTRANS integer 
    - 정의 
        - 페이지에 동시 접근할 수 있는 트랜잭션의 최대 개수이다. 
    - 1 부터 32 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기본값은 8 이다.

<a id="a79130b399fe55ed"></a>
#### &lt;index physical attribute clause&gt;

인덱스의 물리적 속성 정보를 정의한다.

- PCTFREE integer 
    - 정의 
        - 페이지 내 key 삽입으로 인한 페이지 분할 빈도를 조절하기 위해 예약된 공간이다.
        - 인덱스 bottom-up 빌드 시에만 적용된다. 
    - 0 에서 99 까지의 값을 사용할 수 있다. 
    - 생략할 경우, DEFAULT_INDEX_PCTFREE property에 설정된 값을 사용한다.
- INITRANS integer 
    - &lt;table physical attribute clause&gt;의 INITRANS와 동일하다. 
- MAXTRANS integer 
    - &lt;table physical attribute clause&gt;의 MAXTRANS와 동일하다.

<a id="cc5bfd802473f6d4"></a>
#### &lt;segment attr clause&gt;

테이블이 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer 
    - 정의 
        - 테이블을 생성할 때 초기에 할당할 물리적 공간의 크기를 기술한다. 
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT 크기가 8192 bytes일 경우 'INITIAL 100'은 실제 8192 bytes로 작동한다.) 
        - 이 크기 (TABLESPACE의 EXTENT 크기에 align 된 크기)는 MINEXTENTS의 크기와 같거나 커야 하며, MAXEXTENTS의 크기와 같거나 작아야 한다. 
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다. 
    - 생략할 경우, 기본값은 테이블이 속한 TABLESPACE의 EXTENT 하나 크기이다.

- NEXT integer
    - 정의
        - 테이블의 물리적 공간을 추가할 경우 할당할 물리적 공간의 크기를 기술한다.
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT크기가 8192 bytes일 경우 'NEXT 100'은 실제 8192 bytes로 작동한다.)
        - NEXT는 현재 테이블이 사용할 수 있는 남은 공간의 크기 (MAXEXTENTS의 크기에서 현재 사용하고 있는 공간의 크기를 뺀 크기)에 따라 아래와 같이 작동한다.  
      - 남은 공간의 크기가 0인 경우 더 이상 공간을 확장하지 못한다.  
      - 남은 공간의 크기가 0보다 크고 NEXT보다 작은 경우 남은 공간의 크기만큼 할당한다.  
      - 남은 공간의 크기가 NEXT 보다 클 경우 NEXT의 크기만큼 할당한다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기본값은 테이블이 속한 TABLESPACE의 EXTENT 하나 크기이다.

- MINSIZE integer 
    - 정의 
        - 테이블에서 유지해야할 최소 공간의 크기이다. 
        - 이 값은 MAXSIZE의 값과 같거나 작아야 한다. 
    - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. 
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다. 
    - EXTENT 두 개의 크기보다 작을 경우 EXTENT 두 개 크기로 결정된다. 
    - 생략할 경우, 기본값은 EXTENT 두 개 크기이다.

- MAXSIZE integer 
    - 정의 
        - 테이블에서 할당받을 수 있는 최대 공간의 크기이다. 
        - 이 값은 MINSIZE의 값과 같거나 커야 한다. 
    - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. 
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다. 
    - 생략할 경우, 기본값은 32 테라바이트 (35,184,372,088,832) 이다.
    - 32 테라바이트보다 큰 값을 지정하더라도 32 테라바이트로 수정되어 설정된다.

<a id="a48d3b47584dbd75"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="996f5c052f9d7975"></a>
#### TABLESPACE tablespace_name

테이블이 저장될 tablespace의 이름을 지정한다.   
TABLESPACE 절을 생략할 경우, 구문을 수행하는 사용자의 기본 tablespace_name을 사용한다.

<a id="f6d7f5d1c5e3ce72"></a>
#### TABLESPACE index_tablespace_name

인덱스가 저장될 tablespace의 이름을 지정한다.   
TABLESPACE 절을 생략할 경우, 사용자의 인덱스 테이블스페이스를 사용한다.  
사용자의 인덱스 테이블스페이스가 NULL인 경우, DISK 테이블은 사용자의 데이터 테이블스페이스를 사용하고 MEMORY 테이블은 사용자의 기본 임시 테이블스페이스를 사용한다.

<a id="e0059aeb7cfa56d1"></a>
#### &lt;constraint characteristics&gt;

제약 조건의 특성을 정의한다.   
제약 조건을 정의할 때 다음과 같은 특성들을 설정할 수 있다.

- 제약 조건의 지연가능성 ( DEFERRABLE | NOT DEFERRABLE )
- 제약 조건의 검사시점 ( &lt;constraint check time&gt; )

&lt;constraint characteristics&gt;를 생략할 경우, NOT DEFERRABLE INITIALLY IMMEDIATE로 설정한다.

<a id="bfde74e2641dd946"></a>
#### DEFERRABLE | NOT DEFERRABLE

제약 조건을 DML을 수행할 때 검사하지 않고, COMMIT을 수행할 때 검사할 수 있게 지연시킬 수 있는지 여부를 설정한다.

지연 가능한 제약 조건의 검사시점은 [SET CONSTRAINTS](20-sql-references-h-z.md#b39019fd3808ec13) 구문으로 제어한다.

- NOT DEFERRABLE
    - 검사 시점을 지연시킬 수 없으며, INSERT, DELETE, UPDATE 구문을 수행할 때 제약 조건을 검사한다.
- DEFERRABLE
    - 검사 시점을 [SET CONSTRAINTS](20-sql-references-h-z.md#b39019fd3808ec13) 구문으로 제어할 수 있다.
    - SET CONSTRAINTS constraint_name IMMEDIATE
        - DML을 수행할 때 제약 조건을 검사한다.
    - SET CONSTRAINTS constraint_name DEFERRED
        - COMMIT을 수행할 때 제약 조건을 검사한다.
- 명시하지 않을 경우 기본값은 &lt;constraint check time&gt;에 따라 결정된다.
    - INITIALLY IMMEDIATE를 명시한 경우, NOT DEFERRABLE 이다.
    - INITIALLY DEFERRED를 명시한 경우, DEFERRABLE 이다.
    - &lt;constraint check time&gt;을 명시하지 않은 경우, NOT DEFERRABLE 이다.

<a id="ad240eaf02f41a8a"></a>
#### &lt;constraint check time&gt;

지연가능한 (DEFERRABLE) 제약 조건일 경우, 검사 시점의 초기값을 설정한다.

- INITIALLY IMMEDIATE
    - DML을 수행할 때 제약 조건을 검사한다.
- INITIALLY DEFERRED
    - COMMIT을 수행할 때 제약 조건을 검사한다.
    - NOT DEFERRABLE과 함께 사용할 수 없다.
- 명시하지 않을 경우, 기본값은 INITIALLY IMMEDIATE 이다.

지연 가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](20-sql-references-h-z.md#b39019fd3808ec13) 구문을 참조한다.

<a id="48fabb9b705791d1"></a>
#### &lt;table global secondary index clause&gt;

테이블의 global secondary index를 정의한다.

- WITH GLOBAL SECONDARY INDEX [ &lt;index attributes&gt; [...] ] [ TABLESPACE tablespace_name ]
    - Cluster system 환경에서 테이블을 생성할 때 global secondary index를 생성한다.
    - &lt;index attribute&gt;
        - Global secondary index의 index attribute를 설정한다.
    - TABLESPACE tablespace_name
        - Global secondary index를 생성할 tablespace를 지정한다.
- WITHOUT GLOBAL SECONDARY INDEX
    - Cluster system 환경에서 테이블을 생성할 때 global secondary index를 생성하지 않도록 한다.

<a id="394f0783f0d75745"></a>
### 설명

<a id="0230b995a1f3bada"></a>
#### 제약 조건의 특성

GOLDILOCKS는 key 제약 조건을 생성할 때 uniqueness 검사를 하기 위해 자동으로 index를 생성한다.

다음과 같은 column은 NULL 값을 허용하지 않는다.

- NOT NULL 제약 조건이 있는 column
- Primary key 제약 조건에 포함되는 column
- Identity column

<a id="88977701340c9516"></a>
#### Cluster Table

Cluster 환경에서 테이블은 다음 중 하나의 sharding 정책으로 데이터를 관리한다.

- Cloned table
    - 테이블의 모든 data를 복제하여 cluster system에 배치한다.
- Hash sharded table
    - 테이블의 data를 sharding key의 해쉬 (hash) 값을 기준으로 여러 개의 shard로 분할하여 cluster system에 배치한다.
- Range sharded table
    - 테이블의 data를 sharding key의 범위 (range) 값을 기준으로 여러 개의 shard로 분할하여 cluster system에 배치한다.
- List sharded table
    - 테이블의 data를 sharding key의 나열 (list) 값을 기준으로 여러 개의 shard로 분할하여 cluster system 에 배치한다.

테이블을 생성할 때 다음을 고려하여 sharding 정책을 결정한다. Cluster system 상에서 운영되는 테이블들은 그 특성에 따라 code table과 fact table로 구분할 수 있다.

- Code table 
    - 제품 목록, 공급자 목록 등과 같이 데이터의 변경이 적으며 데이터 양이 적은 테이블 
    - Fact table과 함께 자주 참조되는 테이블 
- Fact table 
    - 거래 내역, 통화 내역 등과 같이 데이터의 변경이 많으며 데이터 양이 많은 테이블 
    - 데이터 양이 많아 sharding이 필요한 테이블

Code table에는 &lt;cloned strategy&gt;가 바람직하며, fact table의 경우 테이블의 접근 패턴에 따라 &lt;table sharding strategy&gt;를 결정해야 한다.

<a id="5999243f954d1587"></a>
### 사용 예

다음은 일반 테이블을 생성하는 예이다.

```
gSQL> CREATE TABLE region
(
    r_regionkey   INTEGER
  , r_name        CHAR(25)
  , r_comment     VARCHAR(152)
);

Table created.
```

다음은 테이블을 생성할 때 column에 제약 조건을 기술하는 예이다.

```
gSQL> CREATE TABLE supplier
(
    s_suppkey     INTEGER PRIMARY KEY
  , s_name        CHAR(25) NOT NULL
  , s_address     VARCHAR(40)
  , s_nationkey   INTEGER
  , s_phone       CHAR(15)
  , s_acctbal     NUMERIC(12,2)
  , s_comment     VARCHAR(101)
);

Table created.
```

다음은 테이블을 생성할 때 여러 column을 포함하는 제약 조건을 기술하는 예이다.

```
gSQL> CREATE TABLE partsupp
(
    ps_partkey    INTEGER
  , ps_suppkey    INTEGER
  , ps_availqty   INTEGER
  , ps_supplycost NUMERIC(12,2)    
  , ps_comment    VARCHAR(199)
  , CONSTRAINT ps_unique_key UNIQUE(ps_partkey, ps_suppkey)
);

Table created.
```

다음은 테이블을 생성할 때 지연 가능 여부를 포함한 제약 조건을 기술하는 예이다.

```
gSQL> CREATE TABLE t1 
( 
    id     NUMBER        PRIMARY KEY 
                         NOT DEFERRABLE INITIALLY IMMEDIATE
  , name   VARCHAR(128)  CONSTRAINT t1_nn NOT NULL 
                         DEFERRABLE INITIALLY IMMEDIATE
  , addr   VARCHAR(1024) 
  , CONSTRAINT t1_uk UNIQUE ( id, name ) 
                     DEFERRABLE INITIALLY DEFERRED
);

Table created.

gSQL> COMMIT;

Commit complete.
```

다음은 테이블을 생성할 때 자동 생성값과 기본값을 갖는 column들을 기술하는 예이다.

```
CREATE TABLE customer
(
    c_custkey     INTEGER   GENERATED BY DEFAULT AS IDENTITY
  , c_name        VARCHAR(25)
  , c_address     VARCHAR(40) DEFAULT 'N/A'
  , c_nationkey   INTEGER
  , c_phone       CHAR(15)
  , c_acctbal     NUMERIC(12,2)
  , c_mktsegment  CHAR(10)
  , c_comment     VARCHAR(117)
);

Table created.
```

다음은 테이블을 생성할 때 저장될 tablespace를 지정하는 예이다.

```
gSQL> CREATE TABLE lineitem
(
    l_orderkey      INTEGER
  , l_partkey       INTEGER
  , l_suppkey       INTEGER
  , l_linenumber    INTEGER
  , l_quantity      NUMERIC(12,2)
  , l_extendedprice NUMERIC(12,2)
  , l_discount      NUMERIC(12,2)
  , l_tax           NUMERIC(12,2)
  , l_returnflag    CHAR(1)
  , l_linestatus    CHAR(1)
  , l_shipdate      DATE
  , l_commitdate    DATE
  , l_receiptdate   DATE
  , l_shipinstruct  CHAR(25)
  , l_shipmode      CHAR(10)
  , l_comment       VARCHAR(44)
  , PRIMARY KEY (l_orderkey, l_linenumber) INDEX lineitem_pk_idx TABLESPACE mem_temp_tbs
) TABLESPACE mem_data_tbs;

Table created.
```

다음은 cluster-wide cloned table을 정의하는 예이다. 테이블의 data를 cluster system 전체에 복제하여 배치한다.

```
gSQL>
CREATE TABLE region
(
    r_regionkey   INTEGER
  , r_name        CHAR(25)
  , r_comment     VARCHAR(152)
)
CLONED
AT CLUSTER WIDE
;

Table created.
```

다음은 group-specific cloned table을 정의하는 예이다. 테이블의 데이터는 사용자가 지정한 g1, g2 cluster group에 복제하여 배치한다.

```
gSQL> 
CREATE TABLE region
(
    r_regionkey   INTEGER
  , r_name        CHAR(25)
  , r_comment     VARCHAR(152)
)
CLONED
AT CLUSTER GROUP g1, g2
;

Table created.
```

다음은 cluster-wide hash sharded table을 정의하는 예이다. 테이블의 데이터가 ps_partkey column의 hash 값에 의해 24 개의 shard로 분할되며 각 shard는 cluster system 전체에 자동으로 배치된다.

```
gSQL>
CREATE TABLE partsupp
(
    ps_partkey    INTEGER
  , ps_suppkey    INTEGER
  , ps_availqty   INTEGER
  , ps_supplycost NUMERIC(12,2)    
  , ps_comment    VARCHAR(199)
)
SHARDING BY HASH ( ps_partkey )
SHARD COUNT 24
AT CLUSTER WIDE
;

Table created.
```

다음은 group-specific hash sharded table을 정의하는 예이다. 테이블의 데이터가 ps_partkey column의 hash 값에 의해 24 개의 shard로 분할되며 각 shard는 지정한 cluster group g2, g3에 자동으로 배치된다.

```
gSQL>
CREATE TABLE partsupp
(
    ps_partkey    INTEGER
  , ps_suppkey    INTEGER
  , ps_availqty   INTEGER
  , ps_supplycost NUMERIC(12,2)    
  , ps_comment    VARCHAR(199)
)
SHARDING BY HASH ( ps_partkey )
SHARD COUNT 24
AT CLUSTER GROUP g2, g3
;

Table created.
```

다음은 cluster-wide range sharded table을 정의하는 예이다. 테이블 데이터가 D_ID column의 range 값을 기준으로 여덟 개의 shard로 분할되고, 각 shard가 cluster system 전체에 자동으로 배치된다.

```
gSQL>
CREATE TABLE DISTRICT (
    D_ID        INTEGER, 
    D_W_ID      INTEGER, 
    D_NAME      VARCHAR(10), 
    D_STREET_1  VARCHAR(20), 
    D_STREET_2  VARCHAR(20), 
    D_CITY      VARCHAR(20), 
    D_STATE     CHAR(2), 
    D_ZIP       CHAR(9), 
    D_TAX       NUMERIC(4,4), 
    D_YTD       NUMERIC(15,2), 
    D_NEXT_O_ID INTEGER,

    PRIMARY KEY (D_W_ID, D_ID) INDEX DISTRICT_PK_IDX
) 
    SHARDING BY RANGE (D_ID)
    AT CLUSTER WIDE
    SHARD s1 VALUES LESS THAN ( 100 ),
    SHARD s2 VALUES LESS THAN ( 200 ),
    SHARD s3 VALUES LESS THAN ( 300 ),
    SHARD s4 VALUES LESS THAN ( 400 ),
    SHARD s5 VALUES LESS THAN ( 500 ),
    SHARD s6 VALUES LESS THAN ( 600 ),
    SHARD s7 VALUES LESS THAN ( 700 ),
    SHARD s8 VALUES LESS THAN ( MAXVALUE );
;

Table created.
```

다음은 group-specific range sharded table을 정의하는 예이다. 테이블 데이터는 NO_D_ID column의 range 값을 기준으로 세 개의 range 값으로 분할되고, s1 shard는 g1 cluster group에, s2 shard는 g2 cluster group에 그리고 s3 shard는 g3 cluster group에 각각 지정되어 배치된다.

```
gSQL>
CREATE TABLE NEW_ORDER
(
    NO_O_ID INTEGER,
    NO_D_ID INTEGER,
    NO_W_ID INTEGER,

    PRIMARY KEY(NO_W_ID, NO_D_ID, NO_O_ID) INDEX NEW_ORDER_PK_IDX
) 
    SHARDING BY RANGE (NO_D_ID)
    SHARD s1 VALUES LESS THAN ( 5 )        AT CLUSTER GROUP g1,
    SHARD s2 VALUES LESS THAN ( 8 )        AT CLUSTER GROUP g2,
    SHARD s3 VALUES LESS THAN ( MAXVALUE ) AT CLUSTER GROUP g3
;

Table created.
```

다음은 cluster-wide list sharded table을 정의하는 예이다. List shard가 city column을 기준으로 다섯 개로 분할되고, 각 shard는 cluster system 전체에 자동으로 배치된다.

```
gSQL>
CREATE TABLE t1 
(
    id   INTEGER
  , name VARCHAR(32)
  , city VARCHAR(128) 
) 
   SHARDING BY LIST (city)
      AT CLUSTER WIDE
      SHARD s1 VALUES IN ( 'seoul' ),
      SHARD s2 VALUES IN ( 'busan', 'ulsan' ),
      SHARD s3 VALUES IN ( 'suwon', 'ansan', 'osan' ),
      SHARD s4 VALUES IN ( 'goyang', 'paju', 'guri' ),
      SHARD s5 VALUES IN ( DEFAULT )            
;

Table created.
```

다음은 group-specific list sharded table을 정의하는 예이다. List shard가 city column을 기준으로 다섯 개로 분할되고, 각 shard는 지정된 cluster group에 배치된다.

```
gSQL>
CREATE TABLE t1 
(
    id   INTEGER
  , name VARCHAR(32)
  , city VARCHAR(128) 
) 
   SHARDING BY LIST (city)
      SHARD s1 VALUES IN ( 'seoul' )                  AT CLUSTER GROUP g1,
      SHARD s2 VALUES IN ( 'busan', 'ulsan' )         AT CLUSTER GROUP g2,
      SHARD s3 VALUES IN ( 'suwon', 'ansan', 'osan' ) AT CLUSTER GROUP g1,
      SHARD s4 VALUES IN ( 'goyang', 'paju', 'guri' ) AT CLUSTER GROUP g2,
      SHARD s5 VALUES IN ( DEFAULT )                  AT CLUSTER GROUP g3
;

Table created.
```

Global secondary index 없이 테이블 T1을 생성한다.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) )  WITHOUT GLOBAL SECONDARY INDEX;

Table created.
```

테이블 T1을 생성하고, 테이블 T1의 global secondary index를 생성한다.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) )  WITH GLOBAL SECONDARY INDEX;

Table created.
```

테이블 T1을 생성한 후에 테이블 T1의 global secondary index를 tablespace USER_DATA_TBS에 logging index로 생성한다.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) ) 
      WITH GLOBAL SECONDARY INDEX
      TABLESPACE USER_DATA_TBS;

Table created.
```

테이블 T1을 생성한 후에 테이블 T1의 global secondary index를 tablespace USER_TEMP_TBS에 nologging index로 생성한다.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) ) 
      WITH GLOBAL SECONDARY INDEX
      TABLESPACE USER_TEMP_TBS;

Table created.
```

<a id="7f9fef77745a8cf7"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- TABLESPACE 절, &lt;physical attribute clause&gt; 절 등의 물리적 개념
- SQL 표준은 DEFAULT 절에 연산을 사용할 수 없다.

**SQL 표준 호환성**

<a id="71564015118c385c"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T171 | LIKE clause in table definition | X |
| F531 | Temporary tables | X |
| S051 | Create table of type | X |
| S043 | Enhanced reference types | X |
| S081 | Subtables | X |
| T173 | Extended LIKE clause in table definition | X |
| T180 | System-versioned tables | X |
| F692 | Extended collation support | X |
| T174 | Identity columns | O |
| T175 | Generated columns | X |
| S071 | SQL paths in function and type name resolution | X |
| F321 | User authorization | O |
| T322 | Extended roles | X |
| F762 | CURRENT_CATALOG | O |
| F763 | CURRENT_SCHEMA | O |

<a id="0d8ef13c1fd1d5d6"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLE](#528ddb8580a6edc6)
- [ALTER TABLE](18-sql-references-a-b.md#dbeb5fde894ac5df)
- [CREATE TABLESPACE](#c81940ba4a84752c)
- [CREATE SCHEMA](#b5816864e0a0ee57)
- [CREATE INDEX](#04e7730c239ac562)
- [CREATE SEQUENCE](#971516b46cb8bf8d)
- [SET CONSTRAINTS](20-sql-references-h-z.md#b39019fd3808ec13)
- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](18-sql-references-a-b.md#7d73e98f397bd282)

<a id="bd342487ebebfc2b"></a>
## CREATE TABLE AS SELECT

<a id="f8bbacc203016fd8"></a>
### 기능

질의 결과로부터 새로운 테이블을 생성한다.

<a id="f282d76f81b2b68a"></a>
### 구문

```
<table definition: AS query expression> ::=
    CREATE TABLE table_name 
        [ ( column_name [, ...] ) ]
        [ <table sharding strategy> ]
        [ <table attribute clause> [, ...] ]
        [ TABLESPACE tablespace_name ]
        [ <table global secondary index clause> ]
        AS <query expression> [ WITH [ NO ] DATA ]
    ;

<table sharding strategy> ::=
      <cloned strategy>
    | <hash sharding strategy>
    | <range sharding strategy>
    | <list sharding strategy>

<cloned strategy> ::=
    CLONED [ <clone placement> ]

<clone placement> ::=
      AT CLUSTER WIDE
    | AT CLUSTER GROUP group_list

<hash sharding strategy> ::=
    SHARDING BY [HASH] ( column_list )
    [ <hash shard count> ]
    [ <hash shard placement> ]

<hash shard count> ::=
    SHARD COUNT integer

<hash shard placement> ::=
      AT CLUSTER WIDE
    | AT CLUSTER GROUP group_list

<range sharding strategy> ::=
    SHARDING BY RANGE ( column_list )
    { <cluster-wide range shard placement> | <group-specific range shard placement> }

<cluster-wide range shard placement> ::=
    AT CLUSTER WIDE
    <range shard definition> [, ...]

<group-specific range shard placement> ::=
    <group-specific range shard definition> [, ...]

<group-specific range shard definition> ::=
    <range shard definition> AT CLUSTER GROUP group_name

<range shard definition> ::=
    SHARD range_name VALUES LESS THAN ( <range value clause> )

<range value clause> ::=
    <range value> [, ...]

<range value> ::=
      constant
    | MAXVALUE

<list sharding strategy> ::=
    SHARDING BY LIST ( column_name )
    { <cluster-wide list shard placement> | <group-specific list shard placement> }

<cluster-wide list shard placement> ::=
    AT CLUSTER WIDE
    <list shard definition> [, ...]

<group-specific list shard placement> ::=
    <group-specific list shard definition> [, ...]

<group-specific list shard definition> ::=
    <list shard definition> AT CLUSTER GROUP group_name

<list shard definition> ::=
      SHARD shard_name VALUES IN ( <list value clause> )

<list value clause> ::=
    <list value> [, ...]

<list value> ::=
      constant
    | NULL
    | DEFAULT


<table attribute clause> ::=
      [ <table physical attribute clause> ]
    | [ STORAGE ( <segment attr clause> [...] ) ]

<table physical attribute clause> ::=
      PCTFREE integer
    | PCTUSED integer
    | INITRANS integer
    | MAXTRANS integer

<index physical attribute clause> ::=
      PCTFREE integer
    | INITRANS integer
    | MAXTRANS integer

<segment attr clause> ::=
      INITIAL <size_clause>
    | NEXT <size_clause>
    | MINSIZE <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]

<table global secondary index clause> ::=
      WITH GLOBAL SECONDARY INDEX [ <index attributes> [...] ] [ TABLESPACE tablespace_name ]
    |  WITHOUT GLOBAL SECONDARY INDEX
```

<a id="e48d9d5c4695dc0a"></a>
### 사용 범위 및 접근 권한

&lt;table definition:AS query expression&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블 생성 권한
    - [CREATE TABLE](#060501387611d25a) 구문의 접근 권한을 참조한다.
- SELECT 접근 권한 
    - [SELECT](20-sql-references-h-z.md#a8ad8e667688877b) 구문의 접근 권한을 참조한다.

<a id="ad040c699a62c8cb"></a>
### 구문 규칙 및 파라미터

<a id="8314e6d567b3ab7c"></a>
#### table_name

생성할 테이블의 이름이다.  
자세한 내용은 [table_name](#d83b67dfcf8ea14b) 구문을 참조한다.

<a id="cad82601e3095149"></a>
#### column_name_list

테이블을 구성할 column의 이름으로써 테이블 내에서 유일한 이름이어야 하며, column의 개수는 SELECT 절의 결과 column 개수와 동일해야 한다.   
명시하지 않을 경우, &lt;query expression&gt;의 SELECT 절의 column 이름을 사용한다.

단, SELECT절에 column이 아닌 expression (function, operation, subquery 등)이 오면 alias 또는 column name을 명시해야 한다.

Column 이름의 길이는 128 바이트보다 작아야 한다.

<a id="9623f4cc120bf8ad"></a>
#### WITH [NO] DATA

WITH DATA가 명시된 경우, SELECT 절의 결과가 생성될 테이블에 INSERT 된다.    
WITH NO DATA가 명시된 경우, SELECT 절의 결과가 생성될 테이블에 INSERT 되지 않는다.    
명시하지 않을 경우, WITH DATA를 명시한 것과 동일하게 작동한다.

<a id="308aac5196e90e30"></a>
#### other syntax

이 외의 구문 규칙은 [CREATE TABLE](#060501387611d25a) 구문의 syntax를 참조한다.

<a id="335a55af77c176e6"></a>
### 설명

CREATE TABLE AS SELECT 구문을 수행할 때 SELECT list에 NOT NULL 제약 조건이 있는 column이 명시된 경우, 새로운 테이블에도 NOT NULL 제약 조건이 생성된다. 단, 지연 가능한 NOT NULL 제약 조건인 경우, 새로운 테이블에는 NOT NULL 제약 조건을 생성하지 않는다.

그러나 명시적으로 NOT NULL 제약 조건을 생성한 것이 아니라, primary key, identity column과 같이 NOT NULL 속성을 가지고 있는 경우에는 새로운 테이블에 NOT NULL 제약 조건을 생성하지 않는다.

<a id="be2e6f7a28f59011"></a>
### 사용 예

다음은 CREATE TABLE AS SELECT 구문을 실행하는 예이다.

```
gSQL> CREATE TABLE recent_orders 
                AS SELECT order_id, order_item, order_date
                   FROM orders 
                   WHERE order_date >= '2015-03-03'
Table created.
```

다음은 column 이름을 명시하는 예이다.

```
gSQL> CREATE TABLE recent_orders ( order_id, order_item, order_date )
                AS SELECT order_id, order_item, order_date
                   FROM orders 
                   WHERE order_date >= '2015-03-03'
Table created.
```

다음은 SELECT list에 함수가 있는 경우의 예이다.

```
gSQL> CREATE TABLE recent_orders ( order_date, order_count )
                AS SELECT order_date, COUNT(*) 
                   FROM orders 
                   WHERE order_date >= '2015-03-03'
                   GROUP BY order_date;
Table created.
```

다음은 WITH DATA가 있는 경우의 예이다.

```
gSQL>CREATE TABLE orders 
( 
    order_id   NUMBER        
  , order_item VARCHAR(128)  
  , order_date DATE
);
gSQL> COMMIT;
gSQL> INSERT INTO orders VALUES ( 1, 'Pen', '2010-01-01' );
gSQL> INSERT INTO orders VALUES ( 2, 'Book', '2015-03-03' );
gSQL> COMMIT;
gSQL> CREATE TABLE recent_orders
                AS SELECT order_id, order_item, order_date 
                   FROM orders 
                   WHERE order_date >= '2015-03-03'
      WITH DATA;
Table created.
gSQL> SELECT COUNT(*) FROM recent_orders;

COUNT(*)
--------
       1

1 row selected.
```

다음은 WITH NO DATA가 있는 경우의 예이다.

```
gSQL>CREATE TABLE orders 
( 
    order_id   NUMBER        
  , order_item VARCHAR(128)  
  , order_date DATE
);
gSQL> COMMIT;
gSQL> INSERT INTO orders VALUES ( 1, 'Pen', '2010-01-01' );
gSQL> INSERT INTO orders VALUES ( 2, 'Book', '2015-03-03' );
gSQL> COMMIT;
gSQL> CREATE TABLE recent_orders
                AS SELECT order_id, order_item, order_date 
                   FROM orders 
                   WHERE order_date >= '2015-03-03'
      WITH NO DATA;
Table created.
gSQL> SELECT COUNT(*) FROM recent_orders;

COUNT(*)
--------
       0

1 row selected.
```

<a id="c5ae852939bcf506"></a>
### 호환성

CREATE TABLE AS SELECT 구문은 SQL 표준을 따른다. 단, 다음은 표준에서 확장된 것이다.

- 표준에서 SELECT 절 밖의 괄호는 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- 표준에서 WITH [NO] DATA 절은 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- GOLDILOCKS의 tablespace 개념은 표준에 없는 확장 개념이다.

**SQL 표준 호환성**

<a id="7780ad56b5e3b6e6"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T172 | AS subquery clause in table definition | O |

<a id="b6bbb4b73636e432"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](#060501387611d25a)
- [SELECT](20-sql-references-h-z.md#a8ad8e667688877b)

<a id="c81940ba4a84752c"></a>
## CREATE TABLESPACE

<a id="bd0280f64019f3f9"></a>
### 기능

테이블스페이스를 생성한다.

<a id="7ddb613d159aee92"></a>
### 구문

```
<create tablespace statement> ::=
      <memory data tablespace statement>
    | <memory temporary tablespace statement>
    ;
```

<a id="5614bb8eb7855dbe"></a>
### 사용 범위 및 접근 권한

&lt;create tablespace statement&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="c9dc2c449f53d559"></a>
### 구문 규칙 및 파라미터

<a id="49b0e8e4c70bd6ce"></a>
#### &lt;memory data tablespace statement&gt;

- [ MEMORY ] TEMPORARY

질의 처리 과정에서 생성되는 중간 결과 등의 임시 객체나 no logging 인덱스를 저장할 메모리 임시 테이블스페이스이다.  
MEMORY 예약어는 생략할 수 있다.

<a id="0dc83ca13189e0a4"></a>
#### &lt;memory data tablespace clause&gt;

메모리 데이터의 테이블스페이스를 정의한다.  
자세한 내용은 [CREATE MEMORY DATA TABLESPACE](#5dc8246fbc0a52e1) 구문을 참조한다.

<a id="17f227285170a90c"></a>
#### &lt;memory temporary tablespace definition&gt;

메모리의 임시 테이블스페이스를 정의한다.  
자세한 내용은 [CREATE MEMORY TEMPORARY TABLESPACE](#101999ca47732e9f) 구문을 참조한다.

<a id="a1aa85f0dd395d11"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="a6f1f5af6cd74107"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="cff966bbbc704b49"></a>
### 호환성

SQL 표준은 tablespace에 대한 개념을 다루지 않고 있다.

<a id="b1ebd3c9ca8382ab"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#0905e5b2ffc06135)
- [ALTER TABLESPACE](18-sql-references-a-b.md#e50680549a4cafe3)

<a id="bcf4364429be6a9b"></a>
## CREATE USER

<a id="d508afefe4214695"></a>
### 기능

데이터베이스 사용자를 정의한다.

<a id="c6979312b1a013ad"></a>
### 구문

```
<user definition> ::=
    CREATE USER user_identifier IDENTIFIED BY password
    [ PROFILE { profile_name | DEFAULT | NULL } ]
    [ PASSWORD EXPIRE ]
    [ ACCOUNT { LOCK | UNLOCK } ]
    [ DEFAULT TABLESPACE tablespace_name ]
    [ TEMPORARY TABLESPACE tablespace_name ]
    [ INDEX TABLESPACE { tablespace_name | NULL } ]
    [ <schema clause> ]
    ;

<schema clause> ::=
      WITH SCHEMA [schema_name]
    | WITHOUT SCHEMA
```

<a id="329fff9653198254"></a>
### 사용 범위 및 접근 권한

&lt;user definition&gt; 구문을 수행하려면 사용자에게 CREATE USER ON DATABASE 권한이 있어야 한다.

생성한 user_identifier 사용자는 &lt;schema clause&gt;로 생성한 스키마의 소유자라는 권한을 갖는다.

> 생성된 user_identifier에는 별도의 권한이 부여되지 않는다.  
> user_identifier 사용자가 접속해서 SQL 구문을 수행하려면 적절한 권한을 부여받아야 한다.

<a id="bf3afc6f9f3d0dbd"></a>
### 구문 규칙 및 파라미터

<a id="22174bbfa31dc33e"></a>
#### user_identifier

생성할 user의 이름이다.  
동일한 사용자 이름 (user_identifier)이나 역할 이름 (role_name)이 존재하지 않아야 한다.  
user_identifier의 길이는 128 byte 보다 작아야 한다.

<a id="de0d676e854ebd82"></a>
#### password

생성할 user의 password로써 암호화되어 저장된다.  
password의 길이는 128 byte보다 작아야 한다.  
password는 대소문자를 구별한다.  
password는 영문자로 시작해야 하고 영문자, 숫자, underscore(_), $를 포함할 수 있다.  
그 외의 특수문자를 사용하려면 double-quotation (")으로 묶어야 한다.

<a id="ecbfb6895df2958d"></a>
#### PROFILE { profile_name | DEFAULT | NULL }

비밀번호 관리 정책을 위한 profile을 할당한다.

- PROFILE profile_name
    - 사용자가 생성한 profile_name을 할당한다.
- PROFILE DEFAULT
    - 기본 profile "DEFAULT"를 할당한다.
- PROFILE NULL
    - Profile을 할당하지 않는다.

PROFILE 절을 생략할 경우, PROFILE NULL과 동일하며 profile이 적용되지 않는다.  
비밀번호 관리 정책에 대한 자세한 내용은 [CREATE PROFILE](#7ed273ad779b6feb) 을 참조한다.

<a id="36a886da8c55c8b3"></a>
#### PASSWORD EXPIRE

사용자의 비밀번호 유효기간을 만료시킨다.  
사용자가 login 하기 전에 강제로 비밀번호를 변경하도록 하기 위해 사용한다.

<a id="55ad19cc5569a56e"></a>
#### ACCOUNT { LOCK | UNLOCK }

- ACCOUNT LOCK
    - 사용자 계정을 잠근다.
- ACCOUNT UNLOCK
    - 계정 잠금을 해제한다.

<a id="8ebd73102fcee9a3"></a>
#### DEFAULT TABLESPACE tablespace_name

User가 생성하는 테이블, 인덱스 (LOGGING) 등의 객체가 저장될 기본 TABLESPACE를 지정한다.  
DEFAULT TABLESPACE 절을 생략할 경우, DATABASE를 생성할 때 정의한 default data tablespace (MEM_DATA_TBS)가 지정된다.

<a id="d1a7e4f833d91054"></a>
#### TEMPORARY TABLESPACE tablespace_name

User가 생성하는 임시 테이블, 인덱스 (NO LOGGING), 질의 처리 과정에서 생성되는 중간 결과들을 저장할 TABLESPACE를 지정한다.  
TEMPORARY TABLESPACE 절을 생략할 경우, DATABASE를 생성할 때 정의한 default temporary tablespace (MEM_TEMP_TBS)가 지정된다.

<a id="36109690b61f00d9"></a>
#### INDEX TABLESPACE { tablespace_name | NULL }

User가 생성하는 인덱스 객체가 저장되는 기본 TABLESPACE를 지정한다.

- INDEX TABLESPACE tablespace_name 지정
    - Data tablespace를 지정할 경우, LOGGING 인덱스가 된다.
    - Temporary tablespace를 지정할 경우, NOLOGGING 인덱스가 된다.

- INDEX TABLESPACE NULL
    - Index tablespace을 지정하지 않는다.

INDEX TABLESPACE 절을 생략할 경우, INDEX TABLESPACE NULL 이다.

<a id="1797158047a76a68"></a>
#### &lt;schema clause&gt;

User가 기본적으로 사용할 스키마를 생성한다.  
Database 내에 동일한 스키마 이름이 존재하지 않아야 한다.

- WITH SCHEMA [schema_name] 
    - schema_name을 부여하지 않을 경우, user_identifier와 동일한 이름의 스키마가 생성된다. 
    - User의 SCHEMA PATH는 다음과 같이 설정된다. 
        - schema_name, PUBLIC 
- WITHOUT SCHEMA 
    - User가 소유할 스키마를 생성하지 않는다. 
    - User의 SCHEMA PATH는 PUBLIC으로 설정된다.

&lt;schema clause&gt;를 명시하지 않을 경우, 기본값은 WITH SCHEMA이고 user_identifier와 동일한 이름의 스키마가 생성된다.  
사용자가 소유할 스키마는 [CREATE SCHEMA](#b5816864e0a0ee57) 구문을 사용하여 추가로 생성할 수 있다.

<a id="f4065438e7fd5f54"></a>
### 설명

User는 권한의 집합으로 구성된 authorization 객체이다.

최초로 &lt;user definition&gt; 구문을 수행할 때 어떠한 권한도 부여받지 않은 user가 생성되고 다음과 같이 적절한 권한을 부여해야 한다.

GOLDILOCKS에서 user와 schema의 관계는 1 : N 이다.  
즉, user가 schema를 소유하지 않을 수도 있고, 다수의 schema를 소유할 수도 있다.

SQL 표준은 user, schema, database 등의 non-schema 객체들의 관계에 대해 명확히 정의하지 않고 있다. 반면, 각 DBMS 들은 다음과 같이 non-schema 객체 간의 관계를 상이하게 정의하고 있다.

> DBMS별 user와 schema 관계   
> 
> 
> - Oracle
>     - User : schema = 1 : 1 관계이다.
> 
> 
> 
> - DB2 
>     - OS user와 동일하다. 
>     - User를 생성하고 삭제하는 별도의 SQL 구문이 없다. 
> 
> 
> 
> - Postgres 
>     - User : schema = 1 : N 관계이다. 
> 
> 
> 
> - MySQL 
>     - Database : schema = 1 : 1 관계이다.
>     - User는 database (schema)의 하위 객체이다.
> 

<a id="6d2486f2b56e5add"></a>
### 사용 예

사용자를 생성하고 생성한 사용자가 객체를 생성하고 데이터를 조작하도록 하려면 다음과 같이 권한을 부여해야 한다.

다음은 사용자를 생성하고 그 사용자에게 권한을 부여하는 예이다.

• Create a user.

```
gSQL> CREATE USER u1 IDENTIFIED BY u1_password
             DEFAULT   TABLESPACE mem_data_tbs
             TEMPORARY TABLESPACE mem_temp_tbs
             INDEX TABLESPACE NULL;

User created.

gSQL> COMMIT;

Commit complete.
```

• Grant database privileges.

```
gSQL> GRANT CREATE SESSION ON DATABASE TO u1;

Grant succeeded.

COMMIT;

Commit complete.
```

• Grant schema privileges.

```
GRANT CREATE TABLE, CREATE VIEW, CREATE INDEX, CREATE SEQUENCE, ADD CONSTRAINT 
      ON SCHEMA u1 TO u1;

Grant succeeded.

COMMIT;

Commit complete.
```

• Grant tablespace privileges.

```
GRANT CREATE OBJECT ON TABLESPACE mem_data_tbs TO u1;

Grant succeeded.

GRANT CREATE OBJECT ON TABLESPACE mem_temp_tbs TO u1;

Grant succeeded.

COMMIT;

Commit complete.
```

다음은 사용자가 객체를 생성하는 예이다.

• It needs CREATE SESSION ON DATABASE.

```
gSQL> \connect u1 u1_password
```

• It needs CREATE TABLE ON SCHEMA u1.   
• It needs CREATE OBJECT ON TABLESPACE mem_data_tbs.

```
gSQL> CREATE TABLE u1.t1 ( c1 INTEGER, c2 INTEGER ) TABLESPACE mem_data_tbs;

Table created.

gSQL> COMMIT;
```

• It needs CREATE INDEX ON SCHEMA u1.   
• It needs CREATE OBJECT ON TABLESPACE mem_temp_tbs.

```
gSQL> CREATE INDEX u1.idx ON t1 (c2) TABLESPACE mem_temp_tbs;

Index created.

gSQL> COMMIT;
```

• It needs ADD CONSTRAINT ON SCHEMA u1.

```
gSQL> ALTER TABLE t1 ADD CONSTRAINT u1.t1_pk PRIMARY KEY (c1) ;

Table altered.

gSQL> COMMIT;
```

• It needs CREATE SEQUENCE ON SCHEMA u1.

```
gSQL> CREATE SEQUENCE u1.seq;

Sequence created.

gSQL> COMMIT;

gSQL> INSERT INTO u1.t1 VALUES ( u1.seq.NEXTVAL, u1.seq.NEXTVAL );

1 row created

gSQL> COMMIT;
```

<a id="3e7a5a2b79eb7c59"></a>
### 호환성

SQL 표준에서는 user 개념은 다루고 있지만 user 생성 및 삭제와 관련된 SQL 구문은 정의하지 않고 있다.

<a id="2bb22810e1ecfe32"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP USER](#c4934ee399839206)
- [ALTER USER](18-sql-references-a-b.md#7fcf3795e062819a)
- [CREATE SCHEMA](#b5816864e0a0ee57)

<a id="6f697c93c59acd84"></a>
## CREATE VIEW

<a id="89c1f3473485b0ba"></a>
### 기능

View를 정의한다.

<a id="cbdfdf37999e0591"></a>
### 구문

```
<view definition> ::=
    CREATE [ OR REPLACE ] [ FORCE | NO FORCE ] 
        VIEW view_name [ ( column_name [, ...] ) ]
        AS <query expression>
    ;
```

<a id="ac8cdc64dd9e1a1e"></a>
### 사용 범위 및 접근 권한

&lt;view definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- View를 생성하기 위해 다음 권한 중 하나가 있어야 한다.
    - View가 속한 스키마에 대해 (CREATE VIEW 또는 CONTROL SCHEMA) ON SCHEMA 
    - CREATE ANY VIEW ON DATABASE

- OR REPLACE 절을 사용할 때 이미 view가 존재할 경우, 기존 view를 제거할 수 있는 다음 권한 중 하나가 필요하다.
    - 해당 view의 소유자 
    - 해당 view에 대해 CONTROL TABLE ON TABLE 
    - View가 속한 스키마에 대해 (DROP VIEW 또는 CONTROL SCHEMA) ON SCHEMA 
    - DROP ANY VIEW ON DATABASE

- &lt;query expression&gt; 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

- 생성한 view의 소유자는 다음과 같이 결정된다.
    - View가 속한 스키마의 소유자
    - View가 속한 스키마가 PUBLIC인 경우, 구문을 수행한 사용자

- View의 소유자는 생성한 view에 대해 다음과 같은 권한을 갖는다.
    - SELECT ON TABLE WITH GRANT OPTION 
    - INSERT ON TABLE WITH GRANT OPTION 
    - UPDATE ON TABLE WITH GRANT OPTION 
    - DELETE ON TABLE WITH GRANT OPTION 
    - TRIGGER ON TABLE 
    - LOCK ON TABLE WITH GRANT OPTION 
    - ALTER ON TABLE WITH GRANT OPTION

<a id="0980380298d5cac6"></a>
### 구문 규칙 및 파라미터

<a id="943c955218f3836e"></a>
#### [ OR REPLACE ]

이미 존재하는 view가 있을 경우, 기존의 view를 대체한다.

<a id="1c8db584f881bb05"></a>
#### [ FORCE | NO FORCE ]

- FORCE 
    - &lt;query expression&gt;의 유효성 여부에 관계없이 view를 생성한다. 
- NO FORCE 
    - &lt;query expression&gt;이 유효할 경우 view를 생성한다.
- 기본값은 NO FORCE 이다

<a id="a0a80a28bc3d15d5"></a>
#### view_name

생성할 view의 이름이며, 스키마 내에서 유일한 이름이어야 한다.   
schema_name.view_name과 같이 view가 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우,구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
View 이름의 길이는 128 바이트보다 작아야 한다.

<a id="b8ed73d24ebb2cff"></a>
#### [ ( column_name [, ...] ) ]

View를 구성할 column의 이름을 정의한다.   
각 column의 이름은 view 내에서 고유한 이름이어야 한다.

Column의 개수는 SELECT 절의 결과 column 개수와 동일해야 한다.

Column 이름의 리스트를 생략할 경우, &lt;query expression&gt;의 SELECT 절의 column 이름을 사용한다.

<a id="87e79449269b53f7"></a>
##### AS &lt;query expression&gt;

View를 생성하는 [SELECT](20-sql-references-h-z.md#a8ad8e667688877b) 질의이다.

&lt;query expression&gt;에는 다음과 같은 변수를 포함할 수 없다.

- Host parameter 
- SQL parameter 
- Dynamic parameter 
- Embedded variable 
- SEQUENCE 객체

<a id="04054a2b5348c5dd"></a>
### 설명

View는 질의에 이름을 부여한 객체로써 table과 유사한 방식으로 사용할 수 있다.

View를 포함하는 질의를 수행할 때 해당 view는 view 정의에 포함된 질의로 해석된다. 예를 들어, 다음과 같이 view가 참조하는 table이 변경되면 view 정의에 포함된 asterisk (*) 등은 변경된 table 정보에 따라 자동으로 재해석된다.

```
gSQL> CREATE VIEW v1 AS SELECT * FROM t1;
gSQL> COMMIT;
gSQL> SELECT * FROM v1;

ID NAME     
-- ---------
 1 leekmo   
 2 mkkim    
 3 egonspace

3 rows selected.

gSQL> ALTER TABLE t1 ADD COLUMN ( dept_id  INTEGER,  addr  VARCHAR(1024) );
gSQL> COMMIT;

gSQL> select * from v1;

ID NAME      DEPT_ID ADDR
-- --------- ------- ----
 1 leekmo       null null
 2 mkkim        null null
 3 egonspace    null null

3 rows selected.
```

FORCE 옵션을 사용하여 질의에 에러가 존재하는 상태로 view를 생성하거나, view가 참조하는 테이블이나 view가 변경 또는 제거되었을 경우 해당 view에 영향을 미친다.

이런 정보는 INFORMATION_SCHEMA.VIEWS 정보로부터 조회할 수 있다.

- IS_COMPILED column
    - TRUE: View가 정상적으로 생성되었다.
    - FALSE: FORCE 옵션을 사용하여 에러가 존재하는 상태에서 view가 생성되었다.
- IS_AFFECTED column
    - TRUE: View가 참조하는 테이블 또는 view가 변경되었다.
    - FALSE: View를 생성하고 COMPILE한 후에 view가 참조하는 테이블이나 view가 변경되지 않았다.

View의 최대 생성 개수와 view 내부에 생성 가능한 최대 column 개수에는 제한이 없으므로 저장 공간에 문제가 없는 한 계속 생성할 수 있다.

<a id="277eb7f037aba43d"></a>
### 사용 예

다음은 view를 생성하는 예이다.

```
gSQL> CREATE VIEW v1 AS SELECT * FROM t1 WHERE dept_id = 101;

View created.
```

다음은 view를 정의하면서 column 이름을 정의하는 예이다.

```
gSQL> CREATE VIEW v1 ( v_id, v_name )
          AS SELECT id, name FROM t1 WHERE dept_id = 101;

View created.
```

다음은 기존 view가 있을 경우 REPLACE 옵션을 사용하여 이를 제거하고 새로 view를 생성하는 예이다.

```
gSQL> CREATE OR REPLACE VIEW v1(id, name) 
             AS SELECT id, name FROM t1;

View created.
```

다음은 view가 참조하는 객체가 존재하지 않더라도 FORCE 옵션을 사용하여 해당 view를 강제로 생성하는 예이다.

```
gSQL> CREATE FORCE VIEW v1 
          AS SELECT * FROM t1 WHERE dept_id = 101;

ERR-01000(16243): Warning: View created with compilation errors
ERR-42000(16040): table or view does not exist : 
    AS SELECT * FROM t1 WHERE dept_id = 101
                     *
ERROR at line 2:

View created.
```

<a id="129903ae28932e99"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- [ OR REPLACE ] 절 
- [ FORCE | NO FORCE ] 절

**SQL 표준 호환성**

<a id="4b3a96c2f933f3fb"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T131 | Recursive query | O |
| F751 | View CHECK enhancements | X |
| S043 | Enhanced reference types | X |
| T111 | Updatable joins, unions, and columns | X |
| F852 | Top-level &lt;order by clause&gt; in views | O |
| F864 | Top-level &lt;result offset clause&gt; in views | O |
| F859 | Top-level &lt;fetch first clause&gt; in views | O |
| S081 | Subtables | X |

<a id="bd6356c39cdd9fd8"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP VIEW](#7271de5cbf690942)
- [ALTER VIEW](18-sql-references-a-b.md#f911f10e438cdcf6)
- [SELECT](20-sql-references-h-z.md#a8ad8e667688877b)

<a id="f94895843614f7cc"></a>
## DECLARE cursor_name

<a id="86bb12ff94d3d14d"></a>
### 기능

커서를 선언한다.

<a id="8d0d7c4456cccaea"></a>
### 구문

```
<declare cursor> ::=
    DECLARE cursor_name <cursor properties> { FOR | IS } <cursor specification>
    ;

<cursor properties> ::=
      [ <cursor sensitivity> ] [ <cursor scrollability>] ] CURSOR [ <cursor holdability> ] 
    | [ <odbc cursor type] CURSOR [ <cursor holdability> ] 

<cursor sensitivity> ::=
      INSENSITIVE
    | SENSITIVE
    | ASENSITIVE

<cursor scrollability> ::=
      NO SCROLL
    | SCROLL

<cursor holdability> ::=
      WITH HOLD
    | WITHOUT HOLD

<odbc cursor type> ::=
      STATIC
    | KEYSET

<cursor specification> ::=
      statement_name
    | <cursor query>  [ <updatability clause> ]

<cursor query> ::=
      <select statement>
    | <insert returning query statement>
    | <update returning query statement>
    | <delete returning query statement>

<updatability clause> ::=
      FOR READ ONLY 
    | FOR UPDATE [ OF <column name list> ] [ <lock wait mode> ]

<lock wait mode> ::=
    | WAIT
    | WAIT second
    | NOWAIT
```

<a id="d040b47dd17c8029"></a>
### 사용 범위 및 접근 권한

statement_name을 사용한 동적 커서 (dynamic cursor)는 embedded SQL에서 사용할 수 있다.

&lt;cursor query&gt;의 유형에 따라 적절한 접근 권한을 가져야 한다.   
접근 권한에 대한 자세한 내용은 다음을 참조한다.

- [SELECT](20-sql-references-h-z.md#a8ad8e667688877b) 구문의 접근 권한
- [SELECT .. FOR UPDATE](20-sql-references-h-z.md#408bf76827c0124d) 구문의 접근 권한
- [INSERT INTO name RETURNING](20-sql-references-h-z.md#fa1c045c9265d800) 구문의 접근 권한
- [UPDATE name RETURNING](20-sql-references-h-z.md#454971ec810f0e4a) 구문의 접근 권한
- [DELETE FROM name RETURNING](#a590c1dc7a8fa0b1) 구문의 접근 권한

<a id="271dfa545209b85f"></a>
### 구문 규칙 및 파라미터

<a id="2cb8e371089a25ad"></a>
#### cursor_name

선언할 커서의 이름이다.   
하나의 session 내에서 고유한 이름이어야 한다.   
커서 이름의 길이는 128 바이트보다 작아야 한다.

<a id="7f868117692f871f"></a>
#### { FOR | IS }

SQL 표준에서는 구문 키워드로 FOR나 IS 중에 하나를 사용한다.

<a id="c6cf6d215f35f20e"></a>
#### &lt;cursor properties&gt;

커서의 속성을 정의한다.

- &lt;cursor sensitivity&gt;를 명시하지 않은 경우, 기본값은 INSENSITIVE 이다. 
- &lt;cursor scrollability&gt;를 명시하지 않은 경우, 기본값은 NO SCROLL 이다. 
- &lt;cursor holdability&gt;를 명시하지 않은 경우, &lt;cursor updatability&gt;가 기본값을 결정한다.

<a id="465fc40788936382"></a>
#### updatable query

Cursor 속성 중에 SENSITIVE나 FOR UPDATE를 사용하려면 cursor의 query가 base table의 row 변화를 식별하거나 row에 lock을 획득할 수 있는 updatable query 여야 한다.

updatable query는 다음 조건을 모두 만족해야 한다.

- 최상위 query에 DISTINCT가 존재하지 않아야 한다.
    - (X) SELECT DISTINCT * FROM t1;
- 최상위 query에 GROUP BY, HAVING, aggregation function이 존재하지 않아야 한다.
    - (X) SELECT MAX(c1) FROM t1;
- Returning query가 아니어야 한다.
    - (X) DELETE FROM t1 RETURNING c1;
- Set 연산자가 존재하지 않아야 한다.
    - (X) SELECT * FROM t1 UNION ALL SELECT * FROM t2;
- FROM 절에 나열된 table 들에 하나 이상의 updatable column이 존재해야 한다.
    - Join에 포함되는 테이블 중 cross join에 해당하지 않는 테이블의 column은 updatable column이 아니다.
        - FULL OUTER JOIN은 cross join이 아니다.
        - NATURAL JOIN은 cross join이 아니다.
        - INNER JOIN에 USING 구문이 사용되면 cross join이 아니다.
    - 다음과 같은 table들의 column은 updatable column이 아니다.
        - Dictionary table, fixed table, performance view
    - View의 column은 updatable table이 아니다.

<a id="75bdbf4ce896eeb8"></a>
#### &lt;cursor sensitivity&gt;

커서를 운용할 때 query 결과에 영향을 미치는 다음과 같은 데이터 변화를 볼 수 있는지 여부를 설정한다.

- INSENSITIVE 
    - 커서 운용 중에 변경된 데이터 내용을 감지할 수 없다. 
- SENSITIVE 
    - &lt;cursor query&gt;가 updatable query여야 한다. 
    - 커서와 동일한 트랜잭션에서 변경 (UPDATE), 삭제 (DELETE)된 데이터를 감지한다. 
    - 다른 트랜잭션의 COMMIT을 통해 변경 (UPDATE), 삭제 (DELETE)된 데이터를 감지한다. 
- ASENSITIVE 
    - &lt;cursor query&gt;의 유형에 따라 INSENSITIVE인지 SENSITIVE인지가 결정된다. 
        - updatable query인 경우, SENSITIVE이다.
        - updatable query가 아닌 경우, INSENSITIVE이다.
- 명시하지 않을 경우, 기본값은 INSENSITIVE이다.

<a id="b65b8e4da9df708a"></a>
#### &lt;cursor scrollability&gt;

Cursor의 result set을 순차적 또는 비순차적으로 fetch 할 수 있는지 여부를 명시한다.

- NO SCROLL 
    - 순차적 FETCH (FETCH NEXT)만 가능하다. 
- SCROLL 
    - 비순차적 FETCH가 가능하다.
- 명시하지 않을 경우, 기본값은 NO SCROLL이다.

<a id="463eb5f8a2dc940c"></a>
#### &lt;cursor holdability&gt;

Cursor를 OPEN하고 트랜잭션을 commit 한 후에도 cursor가 유지되는지 여부를 설정한다.

- WITH HOLD 
    - 트랜잭션을 COMMIT 해도 cursor가 유지된다. 
    - FOR UPDATE 구문과 함께 사용할 수 없다. 
    - [INSERT INTO name RETURNING](20-sql-references-h-z.md#fa1c045c9265d800) 구문과 함께 사용할 수 없다. 
    - [UPDATE name RETURNING](20-sql-references-h-z.md#454971ec810f0e4a) 구문과 함께 사용할 수 없다. 
    - [DELETE FROM name RETURNING](#a590c1dc7a8fa0b1) 구문과 함께 사용할 수 없다.
    - table commit action이 ON COMMIT DELETE ROWS인 global temporary table을 포함하는 질의에는 사용할 수 없다.

- WITHOUT HOLD 
    - 트랜잭션을 COMMIT/ ROLLBACK하면 cursor를 닫는다.

- Rollback과 cursor
    - 트랜잭션을 rollback 할 경우, 트랜잭션에 포함된 cursor를 닫는다.
    - Savepoint까지 rollback하면 savepoint 이후에 생성된 cursor를 닫는다.

- 명시하지 않을 경우, &lt;cursor holdability&gt;의 기본값은 &lt;cursor updatability&gt;에 따라 결정된다.
    - FOR READ ONLY이거나 &lt;cursor updatability&gt;를 명시하지 않은 경우, 기본값은 WITH HOLD 이다. 
    - FOR UPDATE 구문과 함께 사용할 경우, 기본값은 WITHOUT HOLD 이다.

<a id="11397aa1b6234a19"></a>
#### &lt;odbc cursor type&gt;

ODBC 표준의 cursor 유형으로 SCROLL 속성을 갖는다.

- STATIC CURSOR 
    - SQL 표준의 INSENSITIVE SCROLL과 동일하다. 
    - 비순차적 FETCH가 가능하다. 
    - ODBC 표준의 static scroll cursor 이다. 
- KEYSET CURSOR 
    - SQL 표준의 ASENSITIVE SCROLL과 동일하다.
    - ODBC 표준의 keyset-driven scroll cursor 이다. 
    - Sensitivity 속성은 다음과 같은 특성에 따라 결정된다.

**FOR [UPDATE / READ ONLY] 구문과 query 유형에 따른 sensitivity 결정**

<a id="3aabcca2c72ca96a"></a>
| Updatability | Query 유형 | Sensitivity |
| --- | --- | --- |
| FOR UPDATE | Updatable query | SENSITIVE |
| FOR UPDATE | Non-updatable query | Query error |
| FOR READ ONLY | Any query | INSENSITIVE |
| N/A | Updatable query | SENSITIVE |
| N/A | Non-updatable query | INSENSITIVE |

<a id="60cf4114557c4ade"></a>
#### &lt;cursor specification&gt;

Cursor의 대상이 되는 query를 정의한다.   
statement_name을 사용할 경우, query가 정해지지 않은 동적 커서 (dynamic cursor)가 선언되고, &lt;cursor query&gt;를 사용할 경우, query가 정해진 고정 커서 (standing cursor)가 선언된다.

<a id="3fbf36db6294c948"></a>
#### statement_name

Cursor가 참조할 statement_name이며 embedded SQL에서 사용할 수 있다.

statement_name은 &lt;declare cursor&gt; 구문을 수행하기 전에 존재해야 하며, statement_name이 참조하는 SQL 문장은 [PREPARE statement_name](20-sql-references-h-z.md#a3d45ff2e9b51c9a) 구문이 준비한 query여야 한다.

Query가 아닐 경우 [OPEN cursor_name](20-sql-references-h-z.md#afdd7cb54cc78da0) 구문을 수행할 때 error가 발생한다.

<a id="1617cf78dbb6b991"></a>
#### &lt;cursor query&gt;

Cursor에서 사용할 수 있는 query 유형은 다음 각 구문을 참조한다.

- [SELECT](20-sql-references-h-z.md#a8ad8e667688877b)
- [SELECT .. FOR UPDATE](20-sql-references-h-z.md#408bf76827c0124d)
- [INSERT INTO name RETURNING](20-sql-references-h-z.md#fa1c045c9265d800)
- [UPDATE name RETURNING](20-sql-references-h-z.md#454971ec810f0e4a)
- [DELETE FROM name RETURNING](#a590c1dc7a8fa0b1)

<a id="cb158b5f49507d82"></a>
#### &lt;updatability clause&gt;

Cursor를 이용해 row를 변경할지 여부를 명시한다.

- FOR READ ONLY 
    - 읽기 전용 커서를 선언한다. 
- FOR UPDATE 
    - 쓰기 가능한 커서를 선언한다. 
    - 커서를 open 할 때 해당 트랜잭션이 종료될 때까지, 다른 트랜잭션이 변경할 수 없도록 해당 row 들에 대한 x lock을 획득한다. 
    - WITH HOLD 구문과 함께 사용할 수 없다. 
    - &lt;cursor query&gt;가 updatable query여야 한다.
- 명시하지 않을 경우, 기본값은 FOR READ ONLY이다.

<a id="b14c8a03e46b0aa4"></a>
#### FOR UPDATE OF …

커서를 OPEN 할 때 lock 획득과 관련된 column을 나열한다.

- FOR UPDATE OF 구문에 나열된 column은
    - &lt;select statement&gt;의 FROM 절에 나열된 table의 갱신 가능한 column이어야 한다. 
    - 나열된 column의 table에 대한 lock을 획득한다. 
- FOR UPDATE만 사용하는 경우에는 
    - &lt;select statement&gt;의 FROM 절에 나열된 table들의 모든 갱신 가능한 column을 나열한 것과 동일한 의미이다. 
    - 모든 column의 table에 대한 lock을 획득한다.

<a id="0a0584c4db838695"></a>
#### &lt;lock wait mode&gt;

FOR UPDATE 구문과 함께 사용하며, lock 획득 방법을 지정한다.

- WAIT 
    - 커서를 OPEN 할 때 질의 결과의 모든 row들에 대한 lock을 획득한다. 
    - Lock을 획득할 수 있을 때까지 대기한다. 
- WAIT second 
    - 커서를 OPEN 할 때 질의 결과의 모든 row 들에 대한 lock을 획득한다. 
    - 지정된 시간 안에 lock을 획득하지 못하면 에러가 발생한다. 
    - 초 단위이며 0 ~ 1000000000 까지의 값을 사용할 수 있다. 
- NOWAIT 
    - 커서를 OPEN 할 때 질의 결과의 모든 row들에 대한 lock을 획득한다. 
    - 즉시 lock을 획득하지 못하면 에러가 발생한다.
- 명시하지 않을 경우, 기본값은 WAIT 이다.

<a id="c63a88ae0de89cda"></a>
### 설명

Query에 대한 속성을 제어할 때 DECLARE CURSOR 구문과 OPEN, FETCH, CLOSE 구문을 사용할 경우, 서버의 커서를 제어하기 때문에 ODBC statement나 JDBC statement를 이용하여 cursor를 사용하는 경우보다 성능상 부하가 걸린다.

Query를 수행하기 전에 ODBC statement와 JDBC statement를 이용해 cursor 속성을 제어할 수 있으며, DECLARE CURSOR 구문을 통한 SQL cursor의 속성 제어 방법과 이에 대응하는 ODBC 표준과 JDBC 표준의 cursor 속성 제어 방법은 다음과 같다.

<a id="acad1d7598990548"></a>
<table class="table column_count_4"><caption>ODBC/ JDBC의 커서 속성 제어 </caption><thead><tr><th class="to_center to_middle"><div>Property
분류</div></th><th class="to_center to_middle"><div>GOLDILOCKS
cursor property</div></th><th class="to_center to_middle"><div>ODBC 표준의 cursor 속성 설정</div></th><th class="to_center to_middle"><div>JDBC 표준의 cursor 속성 설정</div></th></tr></thead><tbody><tr><td class="to_left to_middle" rowspan="3"><div>Sensitivity</div></td><td class="to_left to_middle"><div>INSENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_INSENSITIVE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle"><div>SENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_SENSITIVE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle"><div>ASENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_UNSPECIFIED, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Scrollability</div></td><td class="to_left to_middle"><div>NO SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_NONSCROLLABLE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle"><div>SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_SCROLLABLE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Holdability</div></td><td class="to_left to_middle"><div>WITHOUT HOLD</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.CLOSE_CURSORS_AT_COMMIT )</div></td></tr><tr><td class="to_left to_middle"><div>WITH HOLD</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.HOLD_CURSORS_OVER_COMMIT )</div></td></tr></tbody></table>

ODBC cursor type에 대응되는 SQL cursor 선언은 다음과 같다.

**ODBC 커서 type에 대응되는 SQL 커서 선언**

<a id="c679f8c3848fe855"></a>
| ODBC cursor type | SQL cursor 선언 |
| --- | --- |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, len) | NO SCROLL CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_STATIC, len) | STATIC CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, len) | KEYSET CURSOR |

JDBC cursor type에 대응되는 SQL cursor 선언은 다음과 같다.

**JDBC 커서 type에 대응되는 SQL 커서 선언**

<a id="fb916fe4b60e94ae"></a>
| JDBC cursor type | SQL cursor 선언 |
| --- | --- |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_FORWARD_ONLY, conc, hold ) | INSENSITIVE NO SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_INSENSITIVE, conc, hold ) | INSENSITIVE SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_SENSITIVE, conc, hold ) | SENSITIVE SCROLL CURSOR |

<a id="2353512b787a4fae"></a>
### 사용 예

다음은 interactive sql (gsql)을 사용하여 cursor를 선언하고 사용하는 예이다.

```
gSQL> DECLARE cur1 CURSOR FOR SELECT id, data FROM t1;

Cursor declared.

gSQL> OPEN cur1;

Cursor is open.

gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   2 data_2

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   4 data_4

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

no rows fetched.

gSQL> CLOSE cur1;

Cursor closed.
```

다음은 KEYSET 커서를 선언하고 순차적으로 검색한 후, UPDATE, DELETE 구문에 대한 transaction이 완료된 후에 이를 역방향으로 검색하는 예이다.

```
gSQL> DECLARE cur_keyset KEYSET CURSOR FOR SELECT id, data FROM t1;

Cursor declared.

gSQL> OPEN cur_keyset;

Cursor is open.

gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> FETCH NEXT cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.


gSQL> FETCH NEXT cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   2 data_2

1 row fetched.

gSQL> FETCH NEXT cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH NEXT cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   4 data_4

1 row fetched.

gSQL> FETCH NEXT cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH NEXT cur_keyset INTO :v_id, :v_data;

no rows fetched.

gSQL> UPDATE t1 SET data = 'new data_2' WHERE id = 2;

1 row updated.

gSQL> COMMIT;

Commit complete.

gSQL> DELETE FROM t1 WHERE id = 4;

1 row deleted.

gSQL> COMMIT;

Commit complete.

gSQL> FETCH PRIOR cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.


gSQL> FETCH PRIOR cur_keyset INTO :v_id, :v_data;

no rows fetched.


gSQL> FETCH PRIOR cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH PRIOR cur_keyset INTO :v_id, :v_data;

V_ID V_DATA    
---- ----------
   2 new data_2

1 row fetched.

gSQL> FETCH PRIOR cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> CLOSE cur_keyset;

Cursor closed.
```

다음은 SCROLL 커서를 선언하고 fetch orientation을 통해 커서를 사용하는 예이다.

```
gSQL> DECLARE cur_scroll SCROLL CURSOR FOR SELECT id, data FROM t1;

Cursor declared.

gSQL> OPEN cur_scroll;

Cursor is open.

gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> FETCH LAST cur_scroll INTO :v_id, :v_data;
V_ID V_DATA
---- ------
   5 data_5

1 row fetched.


gSQL> FETCH PRIOR cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   4 data_4

1 row fetched.


gSQL> FETCH FIRST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.


gSQL> FETCH ABSOLUTE 3 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.


gSQL> FETCH RELATIVE -1 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   2 data_2

1 row fetched.


gSQL> FETCH ABSOLUTE 3 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> CLOSE cur_scroll;

Cursor closed.
```

<a id="acc9e8adc0a67b7f"></a>
### 호환성

&lt;declare cursor&gt; 구문은 SQL 표준과 비교하여 다음과 같은 차이가 있다.

- SQL 표준의 &lt;cursor sensitivity&gt; 기본값은 ASENSITIVE이지만, GOLDILOCKS의 기본값은 INSENSITIVE이다. 
- SQL 표준에서는 다음과 같은 &lt;odbc cursor type&gt;을 다루지 않고 있다. 
    - STATIC CURSOR 
    - KEYSET CURSOR 
- SQL 표준의 &lt;cursor holdability&gt; 기본값은 WITHOUT HOLD이지만, GOLDILOCKS의 기본값은 &lt;cursor updatability&gt;에 따라 다르다. 
- SQL 표준에서는 &lt;cursor query&gt;로 &lt;select statement&gt;만 사용할 수 있지만, GOLDILOCKS는 다음과 같은 returning query를 사용할 수 있다. 
    - [INSERT INTO name RETURNING](20-sql-references-h-z.md#fa1c045c9265d800)
    - [UPDATE name RETURNING](20-sql-references-h-z.md#454971ec810f0e4a)
    - [DELETE FROM name RETURNING](#a590c1dc7a8fa0b1)
- SQL 표준의 &lt;cursor updatability&gt; 기본값은 &lt;select statement&gt;에 따라 결정되지만, GOLDILOCKS의 기본값은 FOR READ ONLY이다. 
- SQL 표준에는 &lt;lock wait mode&gt; 구문이 존재하지 않는다.

**SQL 표준 호환성**

<a id="1e89ac86f18f7700"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F831 | Full cursor update | O |
| T231 | Sensitive cursors | O |
| F791 | Insensitive cursors | O |
| F431 | Read-only scrollable cursors | O |
| T471 | Result sets return value | X |
| T551 | Optional key words for default syntax | O |
| T111 | Updatable joins, unions, and columns | X |
| B031 | Basic dynamic SQL | O |

<a id="02fd0c6503d543c0"></a>
### 참조

관련 내용은 다음을 참조한다.

- [OPEN cursor_name](20-sql-references-h-z.md#afdd7cb54cc78da0)
- [FETCH cursor_name](#47babe65e4397c2a)
- [CLOSE cursor_name](#b130e0aa9376fe9d)
- [PREPARE statement_name](20-sql-references-h-z.md#a3d45ff2e9b51c9a)
- [SELECT](20-sql-references-h-z.md#a8ad8e667688877b)
- [SELECT .. FOR UPDATE](20-sql-references-h-z.md#408bf76827c0124d)
- [INSERT INTO name RETURNING](20-sql-references-h-z.md#fa1c045c9265d800)
- [UPDATE name RETURNING](20-sql-references-h-z.md#454971ec810f0e4a)
- [DELETE FROM name RETURNING](#a590c1dc7a8fa0b1)

<a id="7f39572a92faf235"></a>
## DELETE FROM

<a id="0258a22014e82f06"></a>
### 기능

테이블의 row들을 삭제한다.

<a id="0dfca23a0ce6f2d5"></a>
### 구문

```
<delete statement: searched> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
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
```

<a id="0c9405d1c9f4b58b"></a>
### 사용 범위 및 접근 권한

&lt;delete statement: searched&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블에 대해 (DELETE 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (DELETE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DELETE ANY TABLE ON DATABASE

<a id="0e17b08143a326ac"></a>
### 구문 규칙 및 파라미터

<a id="aac70eb09154b1b3"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="115a683775cb2cda"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="46db67d62bed5434"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 삭제한다.  
WHERE 조건을 명시하지 않은 경우, 모든 row를 삭제한다.  
WHERE 조건의 자세한 내용은 [SELECT](20-sql-references-h-z.md#a8ad8e667688877b) 구문의 [where clause](20-sql-references-h-z.md#a7097ec4495ecaf2)를 참조한다.

<a id="52205d62757a4309"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [SELECT](20-sql-references-h-z.md#a8ad8e667688877b) 구문의 [offset limit clause](20-sql-references-h-z.md#fe18ee55c139acb6)를 참조한다.

<a id="3597613f901974ef"></a>
#### &lt;fetch limit clause&gt;

Fetch 할 row의 개수를 명시하는 구문으로써 다음 두 가지 방법이 사용된다.

- &lt;fetch first clause&gt;
    - Fetch 할 row의 개수를 명시한다.
    - 자세한 내용은 [SELECT](20-sql-references-h-z.md#a8ad8e667688877b) 구문의 [&lt;fetch first clause&gt;](20-sql-references-h-z.md#26e6224bf36a08ef)를 참조한다.
- &lt;limit clause&gt;
    - Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
    - 자세한 내용은 [SELECT](20-sql-references-h-z.md#a8ad8e667688877b) 구문의 [&lt;limit clause&gt;](20-sql-references-h-z.md#f276e0fc5fa670aa)를 참조한다.

<a id="dbae1e07438a8b38"></a>
### 설명

<a id="734a7b62cf3172d0"></a>
#### DELETE 관련 구문들의 차이점

- [DELETE FROM](#7f39572a92faf235)
    - 조건에 부합하는 다수의 row를 삭제한다. 
    - 예: DELETE FROM t1 WHERE c1 = 0; 
- [DELETE FROM name WHERE CURRENT OF cursor_name](#cdf1bbc13ec2cca1)
    - Cursor가 현재 가리키는 row를 삭제한다. 
    - 예: DELETE FROM t1 WHERE CURRENT OF cursor; 
- [DELETE FROM name RETURNING](#a590c1dc7a8fa0b1)
    - 조건에 부합하는 다수의 row를 삭제하며, [SELECT](20-sql-references-h-z.md#a8ad8e667688877b) 구문과 동일한 방식( SQLFetch() 등의 API )으로 삭제한 row들을 검색할 수 있다. 
    - 예: DELETE FROM t1 WHERE c1 = 0 RETURNING c2; 
- [DELETE FROM name RETURNING .. INTO](#aa5058d5295cd427)
    - 한 건 이하의 row를 삭제할 수 있으며, 삭제한 row가 한 건일 경우 RETURNING INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: DELETE FROM t1 WHERE c1 = 0 RETURNING c2 INTO :v1;

<a id="1d0d75dbbfb8a22b"></a>
### 사용 예

다음은 DELETE 구문의 예이다.

```
gSQL> DELETE FROM t1 WHERE id > 3;

2 rows deleted.
```

다음은 &lt;result offset clause&gt;와 &lt;fetch first clause&gt;를 이용하여 조건을 만족하는 row들 중 일부 row들을 (두 건) 건너뛰고 일부 row들만 (두 건) 삭제하는 예이다.

```
gSQL> DELETE FROM t1 OFFSET 2 FETCH 2;

2 rows deleted.


gSQL> SELECT * FROM t1 ORDER BY 1;

ID DATA  
-- ------
 1 data_1
 2 data_2
 5 data_5

3 rows selected.
```

<a id="879cf3671e653db2"></a>
### 호환성

SQL 표준은 DELETE 구문에서 다음 절을 정의하지 않고 있다.

- &lt;result offset clause&gt; 
- &lt;fetch limit clause&gt;

**SQL 표준 호환성**

<a id="ce7fa56317650952"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="c455d5a5f2e91f1d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DELETE FROM name WHERE CURRENT OF cursor_name](#cdf1bbc13ec2cca1)
- [DELETE FROM name RETURNING](#a590c1dc7a8fa0b1)
- [DELETE FROM name RETURNING .. INTO](#aa5058d5295cd427)
- [SELECT](20-sql-references-h-z.md#a8ad8e667688877b)

<a id="a590c1dc7a8fa0b1"></a>
## DELETE FROM name RETURNING

<a id="74cf5c6407ac7ada"></a>
### 기능

테이블의 row들을 삭제하고, 삭제한 row들을 검색한다.

<a id="2f12d7c5e2bb552f"></a>
### 구문

```
<delete returning query statement> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
        <returning clause>
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

<returning clause> ::=
    { RETURN | RETURNING } { * | { <value expression> [ [AS] alias_name] } [, ...] }
```

<a id="f0c70bd4c3b9ac5d"></a>
### 사용 범위 및 접근 권한

&lt;delete returning query statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- DELETE 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - 테이블에 대해 (DELETE 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (DELETE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - DELETE ANY TABLE ON DATABASE

- RETURNING 절에 사용된 모든 column에 대해 다음 권한 중 하나가 있어야 한다.
    - RETURNING 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="d810cb222c9738c2"></a>
### 구문 규칙 및 파라미터

<a id="62ee517de9dc1509"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.

<a id="eea51443c41aa7a5"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="d8dcfcc2e557c4f0"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 삭제한다.  
자세한 내용은 [DELETE FROM](#7f39572a92faf235) 구문을 참조한다.

<a id="f510f357c166d5bf"></a>
#### &lt;result offset clause&gt;

질의 결과 중에 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#7f39572a92faf235) 구문을 참조한다.

<a id="aaf5739417f4f90c"></a>
#### &lt;fetch first clause&gt;

Fetch 할 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#7f39572a92faf235) 구문을 참조한다.

<a id="68a4713a87039e47"></a>
#### &lt;limit clause&gt;

Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.  
자세한 내용은 [DELETE FROM](#7f39572a92faf235) 구문을 참조한다.

<a id="f3447923e0711b67"></a>
#### &lt;returning clause&gt;

삭제된 row들을 결과 집합으로 하고, 이들 중에서 검색할 column을 기술한다.

- RETURNING 절은 DELETE 구문으로 삭제된 row들을 result set으로 하는 결과를 반환한다. 
- &lt;value expression&gt; 
    - SELECT 구문의 &lt;select list&gt;와 동일하지만 aggregation 등을 사용할 수 없다. 
- [[AS] alias_name] 
    - AS 절을 이용해 value expression의 이름을 지정할 수 있다.

RETURN과 RETURNING은 동일한 의미의 키워드이다.

<a id="9b9c3528e3f3c987"></a>
### 설명

자세한 내용은 [DELETE 관련 구문들의 차이점](#734a7b62cf3172d0)을 참조한다.

<a id="1038bb492d141bfc"></a>
### 사용 예

다음은 조건을 만족하는 row들을 삭제하고 삭제한 row들을 검색하는 예이다.

```
gSQL> DELETE FROM t1 WHERE id > 3 RETURNING *;

ID DATA  
-- ------
 4 data_4
 5 data_5

2 rows deleted.
```

다음은 RETURNING 절에 연산을 사용하여 삭제한 row들의 정보를 조회하는 예이다.

```
gSQL> DELETE FROM t1 
             WHERE id > 3 
             RETURNING 'ID: ' || id || ', DATA: ' || data AS id_data;

ID_DATA            
-------------------
ID: 4, DATA: data_4
ID: 5, DATA: data_5

2 rows deleted.
```

<a id="d8b9fb1db0cef8f7"></a>
### 호환성

SQL 표준에는 &lt;delete returning query statement&gt; 구문이 존재하지 않는다.

<a id="4abe2a07cc991c7f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DELETE FROM](#7f39572a92faf235)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#cdf1bbc13ec2cca1)
- [DELETE FROM name RETURNING .. INTO](#aa5058d5295cd427)
- [SELECT](20-sql-references-h-z.md#a8ad8e667688877b)

<a id="aa5058d5295cd427"></a>
## DELETE FROM name RETURNING .. INTO

<a id="7ff6a0c7ee9fda13"></a>
### 기능

테이블에서 row 하나를 삭제하고, 삭제한 row의 값을 호스트 변수에 얻어온다.

<a id="bc910758193a900c"></a>
### 구문

```
<delete returning query statement> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
        <returning into clause>
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

<a id="ff26ca646cb18352"></a>
### 사용 범위 및 접근 권한

&lt;delete returning into statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- DELETE 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - 테이블에 대해 (DELETE 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (DELETE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - DELETE ANY TABLE ON DATABASE

- RETURNING 절에 사용된 모든 column에 대해 다음 권한 중 하나가 있어야 한다.
    - RETURNING 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="0ff291c205db142a"></a>
### 구문 규칙 및 파라미터

<a id="a2e9a0daa186e421"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.

<a id="0f48101dc3420796"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="0a852f0a71ea91e6"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 삭제한다.  
자세한 내용은 [DELETE FROM](#7f39572a92faf235) 구문을 참조한다.

<a id="795a7039024bdc40"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#7f39572a92faf235) 구문을 참조한다.

<a id="522315199082984e"></a>
#### &lt;fetch first clause&gt;

Fetch 할 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#7f39572a92faf235) 구문을 참조한다.

<a id="c829d4b39b4f784c"></a>
#### &lt;limit clause&gt;

Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.  
자세한 내용은 [DELETE FROM](#7f39572a92faf235) 구문을 참조한다.

<a id="85c1b29a102c7663"></a>
#### &lt;returning into clause&gt;

- RETURNING .. AS ..
    - [DELETE FROM name RETURNING](#a590c1dc7a8fa0b1) 구문의 returning clause를 참조한다.
- INTO variable_name [, ...]
    - INTO 절에 기술된 변수의 개수는 RETURNING 절에 기술된 expression의 개수와 동일해야 한다.

<a id="ef8b0973ef0ae606"></a>
### 설명

삭제할 row가 하나 이하여야 한다.   
둘 이상의 row가 삭제되면 에러가 발생한다.

자세한 내용은 [DELETE 관련 구문들의 차이점](#734a7b62cf3172d0)을 참조한다.

<a id="443e99fe52888e87"></a>
### 사용 예

다음은 interactive SQL (gsql)에서 row를 삭제하고 삭제된 row의 값을 호스트 변수에 얻어오는 예이다.

```
gSQL> \var v_id    INTEGER
gSQL> \var v_data  VARCHAR(128)

gSQL> DELETE FROM t1 WHERE id = 3 RETURNING id, data INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row deleted.
```

<a id="5ae808b16fdf1149"></a>
### 호환성

SQL 표준에는 &lt;delete returning into statement&gt; 구문이 존재하지 않는다.

<a id="6296c3728f128e2e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DELETE FROM](#7f39572a92faf235)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#cdf1bbc13ec2cca1)
- [DELETE FROM name RETURNING](#a590c1dc7a8fa0b1)
- [SELECT](20-sql-references-h-z.md#a8ad8e667688877b)

<a id="cdf1bbc13ec2cca1"></a>
## DELETE FROM name WHERE CURRENT OF cursor_name

<a id="dfbcda6affdde789"></a>
### 기능

커서가 가리키는 row 하나를 삭제한다.

<a id="48c9a86f73d8567e"></a>
### 구문

```
<delete statement: positioned> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        WHERE CURRENT OF cursor_name
    ;
```

<a id="88e1e24736c200ac"></a>
### 사용 범위 및 접근 권한

&lt;delete statement: positioned&gt; 구문을 수행하려면 사용자에게 [DELETE FROM](#7f39572a92faf235) 구문을 수행할 수 있는 권한이 있어야 한다.

<a id="ebabb92245dca6a7"></a>
### 구문 규칙 및 파라미터

<a id="d38a856c0f0215be"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.

<a id="1154ecc63e2327f7"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="629d7fc52f8480cc"></a>
#### cursor_name

cursor_name에 해당하는 커서는 다음 조건을 만족해야 한다.

- OPEN 된 커서여야 한다. ([OPEN cursor_name](20-sql-references-h-z.md#afdd7cb54cc78da0)을 참조한다.) 
- 커서를 이용해 FETCH 한 row가 존재해야 한다. ([FETCH cursor_name](#47babe65e4397c2a)을 참조한다.) 
- 커서를 위해 사용된 질의가 table_name을 식별할 수 있어야 한다. ([DECLARE cursor_name](#f94895843614f7cc)을 참조한다.) 
- table_name에 대해 갱신할 수 있는 커서여야 한다. ([DECLARE cursor_name](#f94895843614f7cc)을 참조한다.)

<a id="b7137e9e8f9006f3"></a>
### 설명

자세한 내용은 [DELETE 관련 구문들의 차이점](#734a7b62cf3172d0)을 참조한다.

<a id="d5d03f1587abedd3"></a>
### 사용 예

다음은 interactive SQL (gsql)에서 FOR UPDATE 커서를 선언하고 그 커서를 이용해 row를 삭제하는 예이다.

```
gSQL> DECLARE cur1 CURSOR FOR SELECT id, data FROM t1 FOR UPDATE;

Cursor declared.


gSQL> OPEN cur1;

Cursor is open.


gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   2 data_2

1 row fetched.

gSQL> DELETE FROM t1 WHERE CURRENT OF cur1;

1 row deleted.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   4 data_4

1 row fetched.

gSQL> DELETE FROM t1 WHERE CURRENT OF cur1;

1 row deleted.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

no rows fetched.

gSQL> CLOSE cur1;

Cursor closed.

gSQL> SELECT id, data FROM t1 ORDER BY 1;

ID DATA  
-- ------
 1 data_1
 3 data_3
 5 data_5

3 rows selected.
```

<a id="1030a65534c47432"></a>
### 호환성

**SQL 표준 호환성**

<a id="884a4a7d61ab2e3b"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| S111 | ONLY in query expressions | X |
| B031 | Basic dynamic SQL | O |

<a id="d01930303aa8e821"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#f94895843614f7cc)
- [OPEN cursor_name](20-sql-references-h-z.md#afdd7cb54cc78da0)
- [FETCH cursor_name](#47babe65e4397c2a)
- [DELETE FROM](#7f39572a92faf235)
- [DELETE FROM name RETURNING](#a590c1dc7a8fa0b1)
- [DELETE FROM name RETURNING .. INTO](#aa5058d5295cd427)

<a id="69253535ad827e04"></a>
## DROP AUDIT POLICY

<a id="9b3cb80caec158a3"></a>
### 기능

Audit policy를 제거한다.

<a id="d66dec4d7e2a7842"></a>
### 구문

```
<drop audit policy statement> ::= 
    DROP AUDIT POLICY [ IF EXISTS ] policy_name
;
```

<a id="c9848d48478cd40a"></a>
### 사용 범위 및 접근 권한

&lt;drop audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="e4ce2501ae72d18e"></a>
### 구문 규칙 및 파라미터

<a id="15b2f535365b03fa"></a>
#### IF EXISTS

policy_name이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="6fd956446aa5dd8f"></a>
#### policy_name

제거할 audit policy 객체의 이름이다.

<a id="c0cf26200c85a689"></a>
### 설명

이미 활성화된 audit policy 객체는 제거할 수 없다. 이 경우, NOAUDIT POLICY 구문을 이용해 audit policy를 비활성화해야 한다.

<a id="180e6ea8ca35bd6c"></a>
### 사용 예

다음은 audit policy를 제거하는 예이다.

```
DROP AUDIT POLICY policy_table;
```

<a id="8cfa9d084ce8f240"></a>
### 호환성

SQL 표준에는 audit policy가 존재하지 않는다.

<a id="2b0bfe6259712d6c"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#ab7ff9504e3f6183)
    - [DROP AUDIT POLICY](#69253535ad827e04)
    - [ALTER AUDIT POLICY](18-sql-references-a-b.md#ecf2c4bd73416b17)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](18-sql-references-a-b.md#bdecea76b1665d44)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#f63dd37e5a743f09)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#0f5f6dd722f4b648)

- Audit trail 소거: [ALTER DATABASE CLEAR AUDIT TRAIL](18-sql-references-a-b.md#7cfd4bf205511a5c)

<a id="6d9454a76620869e"></a>
## DROP CLUSTER GROUP

<a id="f369bb0773b43777"></a>
### 기능

Cluster group을 cluster system에서 제거한다.

<a id="511a6695f42651d3"></a>
### 구문

```
<drop cluster group statement> ::=
    DROP CLUSTER GROUP [IF EXISTS] group_name
    ;
```

<a id="3e5ccb5af919155d"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.   
&lt;drop cluster group statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="a94807422dd4aa39"></a>
### 구문 규칙 및 파라미터

<a id="30850b6eaf9e2d5a"></a>
#### [IF EXISTS]

Cluster group이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="840cee918718639d"></a>
#### group_name

Cluster group의 이름이다.   
Shard가 존재하지 않는 cluster group을 제거할 수 있다.

<a id="98effbaf7414887c"></a>
### 설명

Cluster group을 제거하더라도 data loss가 발생하지 않는 경우에 해당 cluster group을 제거할 수 있다.

> 대상 cluster group의 모든 멤버가 inactive 상태여야만 한다.   
> 그렇지 않을 경우, 다음과 같은 에러가 발생한다.

```
gSQL> DROP CLUSTER GROUP g3;

ERR-42000(16582): there are active cluster members in the target cluster group 'G3'
```

<a id="debfdd39f288b233"></a>
### 사용 예

다음은 cluster group을 제거하는 예이다.

```
gSQL> DROP CLUSTER GROUP g3;

Cluster Group dropped.
```

<a id="cb73cbf33c1e6d9f"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="e4bc5c7804f5aa8e"></a>
### 참조

관련 내용은 [CREATE CLUSTER GROUP](#420c16ac60aa5c3d)을 참조한다.

<a id="3ed6f006ec8fc968"></a>
## DROP CLUSTER LOCATION

<a id="db5f82de523725c1"></a>
### 기능

Cluster member의 접속 정보를 삭제한다.

<a id="20ca6eab0b19791b"></a>
### 구문

```
<drop cluster location statement> ::=
    DROP CLUSTER LOCATION member_name 
    ;
```

<a id="35f4f9b723ed0f8e"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.   
&lt;drop cluster location statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="665f6c6d55b0276e"></a>
### 구문 규칙 및 파라미터

<a id="555a922a70b158ad"></a>
#### member_name

Cluster member의 이름이다.   
등록된 cluster location 정보에 동일한 cluster member 이름이 존재해야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="0acaa9a7e587b06e"></a>
### 설명

기본적으로 cluster location 정보는 cluster group을 생성할 때나 cluster member를 추가할 때 제공되는 접속 정보를 이용하여 자동으로 생성된다. 생성된 정보는 cluster member나 group을 삭제할 때 함께 삭제된다.

만약 cluster location의 접속 정보가 변경되면 cluster member을 삭제하거나 재생성할 필요없이 [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#aab1431151951450) 을 이용하여 접속 정보를 변경할 수 있다.

<a id="d4a22ccb033e9a72"></a>
### 사용 예

```
gSQL> 
DROP CLUSTER LOCATION g1n2
;

Created
```

<a id="ad832a4c91a89234"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="3ea6be10f9c7c58e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER LOCATION](#6d43d72d687cc2a6)
- [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#aab1431151951450)

<a id="d20adfa902b88837"></a>
## DROP INDEX

<a id="d64a8129f563021b"></a>
### 기능

인덱스를 제거한다.

<a id="9bd948b61251bbea"></a>
### 구문

```
<drop index statement> ::=
    DROP INDEX [ IF EXISTS ] index_name
    ;
```

<a id="f305608cfe276ffc"></a>
### 사용 범위 및 접근 권한

&lt;drop index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (DROP INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY INDEX ON DATABASE

<a id="c563ae9877254a68"></a>
### 구문 규칙 및 파라미터

<a id="c9b9809514d49e42"></a>
#### IF EXISTS

인덱스가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="9a4db389a01c5acf"></a>
#### index_name

삭제할 인덱스의 이름이다.   
schema_name.index_name과 같이 인덱스가 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

UNIQUE 제약 조건, PRIMARY KEY 제약 조건을 위해 생성한 인덱스는 제거할 수 없다.  
위 제약 조건을 위해 생성된 인덱스를 제거하려면 [ALTER TABLE name DROP CONSTRAINT](18-sql-references-a-b.md#f92321716f08611e) 구문을 사용하여 관련된 제약 조건을 삭제해야 한다.

<a id="9dea712cd6464057"></a>
### 설명

DROP INDEX와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="402fffde6877f3ec"></a>
### 사용 예

다음은 인덱스를 삭제하는 예이다.

```
gSQL> DROP INDEX idx_t1_id;

Index dropped.
```

다음은 IF EXISTS 구문을 사용하여 인덱스가 존재하지 않더라도 에러가 발생하지 않도록 하는 예이다.

```
gSQL> DROP INDEX IF EXISTS not_exist_index;

Index dropped.
```

<a id="9abffef04aa62877"></a>
### 호환성

SQL 표준에서는 인덱스에 대한 개념을 다루지 않고 있다.

<a id="687260b5f119a044"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](#04e7730c239ac562)
- [DROP TABLE](#528ddb8580a6edc6)
- [ALTER TABLE name DROP CONSTRAINT](18-sql-references-a-b.md#f92321716f08611e)

<a id="c779f85e72834738"></a>
## DROP PROFILE

<a id="558e5631efcfbdbe"></a>
### 기능

Profile을 삭제한다.

<a id="343b31f2a5097482"></a>
### 구문

```
<drop profile statement> ::= 
    DROP PROFILE [ IF EXISTS ] profile_name [ CASCADE ] ;
```

<a id="f2cacd5ed429dcbf"></a>
### 사용 범위 및 접근 권한

&lt;drop profile statement&gt; 구문을 수행하려면 사용자에게 DROP PROFILE ON DATABASE 권한이 있어야 한다.

<a id="112afa2c2975d2c5"></a>
### 구문 규칙 및 파라미터

<a id="36f8338512f0700d"></a>
#### IF EXISTS

Profile이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="2e7e0a1533f60af6"></a>
#### profile_name

삭제할 profile의 이름을 명시한다.   
DEFAULT profile은 삭제할 수 없다.

<a id="7649a642aef502e5"></a>
#### CASCADE

이미 할당받은 사용자들이 존재하는 경우, profile을 삭제하기 위해 반드시 이 절을 명시해야 한다.   
삭제할 profile을 할당받은 사용자들의 profile은 DEFAULT profile로 변경한다.

<a id="21f2428be7f29eb1"></a>
### 사용 예

다음은 CASCADE 구문을 사용하여 profile을 삭제하는 예이다.

```
gSQL> DROP PROFILE prof CASCADE;

Profile dropped.

gSQL> COMMIT;

Commit complete.
```

<a id="4d299eaae04240be"></a>
### 호환성

SQL 표준에서는 profile에 대한 개념을 다루지 않고 있다.

<a id="86325535668e97e6"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE PROFILE](#7ed273ad779b6feb)
- [ALTER PROFILE](18-sql-references-a-b.md#aff30be6193ddc88)

<a id="e766128ab8947c2f"></a>
## DROP SCHEMA

<a id="7a470d220c501c1b"></a>
### 기능

스키마를 제거한다.

<a id="12e0aa59c58b231e"></a>
### 구문

```
<drop schema statement> ::=
    DROP SCHEMA [ IF EXISTS ] schema_name
        [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
```

<a id="7cd6c372b97295ee"></a>
### 사용 범위 및 접근 권한

&lt;drop schema statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 스키마의 소유자 
- 해당 스키마에 대해 CONTROL SCHEMA ON SCHEMA 
- DROP SCHEMA ON DATABASE

<a id="936d6aa00beae339"></a>
### 구문 규칙 및 파라미터

<a id="f719613f2f1389a9"></a>
#### IF EXISTS

스키마가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="4c4ec71938adfe1a"></a>
#### schema_name

제거할 스키마의 이름이다.   
단, database를 생성할 때 자동으로 생성되는 DICTIONARY_SCHEMA, INFORMATION_SCHEMA, PUBLIC과 같은 built-in 스키마는 제거할 수 없다.

<a id="a691eae7a649ced8"></a>
#### &lt;drop behavior&gt;

- RESTRICT 
    - Schema 내에 존재하는 객체가 없어야 한다. 
- CASCADE 
    - Schema 내의 모든 객체를 함께 제거한다.
- 생략할 경우, 기본값은 RESTRICT이다.

<a id="42d7e1108029c666"></a>
### 설명

DROP SCHEMA와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다. 이 때, 제거하는 스키마에 포함된 휴지통 객체들도 제거된다.

<a id="46a38d8ce1ed7613"></a>
### 사용 예

다음은 schema와 schema 내에 존재하는 모든 객체를 함께 제거하는 예이다.

```
gSQL> DROP SCHEMA s1 CASCADE;

Schema dropped.
```

다음은 IF EXISTS 구문을 사용하여 schema가 존재하지 않더라도 에러가 발생하지 않도록 하는 예이다.

```
gSQL> DROP SCHEMA IF EXISTS not_exist_schema;

Schema dropped.
```

<a id="2132fd2e0c80f248"></a>
### 호환성

SQL 표준에서는 IF EXISTS 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="1de3a65bc416f874"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |
| F381 | Extended schema manipulation | O |

<a id="b95b744e7fb0edba"></a>
### 참조

관련 내용은 [CREATE SCHEMA](#b5816864e0a0ee57)를 참조한다.

<a id="bd4f615f4aee0c6b"></a>
## DROP SEQUENCE

<a id="08975036e658c92b"></a>
### 기능

시퀀스를 제거한다.

<a id="acd0263fded32e74"></a>
### 구문

```
<drop sequence generator statement> ::=
    DROP SEQUENCE [ IF EXISTS ] [schema_name.] sequence_name 
    ;
```

<a id="fb2529b353f14c55"></a>
### 사용 범위 및 접근 권한

&lt;drop sequence generator statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 시퀀스의 소유자 
- 시퀀스가 속한 스키마에 대해 (DROP SEQUENCE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY SEQUENCE ON DATABASE

<a id="a22d9c3cd92630dc"></a>
### 구문 규칙 및 파라미터

<a id="1ddfe6351c89782a"></a>
#### IF EXISTS

시퀀스가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="2580477bd8bdc66b"></a>
#### sequence_name

제거할 시퀀스의 이름이다.   
schema_name.sequence_name과 같이 시퀀스가 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="0444a5066d1cdcc2"></a>
### 설명

DROP SEQUENCE와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="b8ffcf759f578101"></a>
### 사용 예

다음은 sequence를 제거하는 예이다.

```
gSQL> DROP SEQUENCE seq1;

Sequence dropped.
```

다음은 IF EXISTS 구문을 사용하여 시퀀스가 존재하지 않더라도 에러가 발생하지 않도록 하는 예이다.

```
gSQL> DROP SEQUENCE invalid_sequence;

ERR-42000(16044): sequence does not exist : 
DROP SEQUENCE invalid_sequence
              *
ERROR at line 1:


gSQL> DROP SEQUENCE IF EXISTS invalid_sequence;

Sequence dropped.
```

<a id="7a8bd3b4edd849a8"></a>
### 호환성

SQL 표준에서는 IF EXISTS 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="15a5ebe434c8d96d"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="949c0a9d2b2eae2c"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE SEQUENCE](#971516b46cb8bf8d)
- [ALTER SEQUENCE](18-sql-references-a-b.md#ea63a831fa2ae849)

<a id="4f8e6238e2b175b7"></a>
## DROP SYNONYM

<a id="abd0df3967134da6"></a>
### 기능

Synonym을 제거한다.

<a id="eecc957d5c84f329"></a>
### 구문

```
<drop synonym statement> ::=
    DROP [ PUBLIC ] SYNONYM [ IF EXISTS ] [schema_name.]synonym_name
    ;
```

<a id="721dbe27b4e3a21e"></a>
### 사용 범위 및 접근 권한

PUBLIC을 명시하여 public synonym을 제거하려면 DROP PUBLIC SYNONYM ON DATABASE 권한이 있어야 한다.

Private synonym을 제거하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 synonym의 소유자 
- Synonym이 속한 스키마에 대해 (DROP SYNONYM 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY SYNONYM ON DATABASE

<a id="cebf6736708729e2"></a>
### 구문 규칙 및 파라미터

<a id="61e0c4b271c599b6"></a>
#### [ PUBLIC ]

Public synonym을 제거하고자 할 때 명시한다.   
이 절을 생략하면 private synonym이 제거된다.

<a id="48def2d5626c0fb3"></a>
#### IF EXISTS

Synonym이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="abeab50e8d54acf5"></a>
#### synonym_name

제거할 synonym의 이름이다.  
schema_name.synonym_name과 같이 synonym이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
PUBLIC을 명시한 경우, 스키마 이름을 명시할 수 없다.

<a id="46b3c4e17233a797"></a>
### 설명

DROP SYNONYM과 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="93514d44e2eefcc4"></a>
### 사용 예

다음은 private synonym을 제거하는 예이다.

```
gSQL> DROP SYNONYM MyEmp;

Synonym dropped.
```

다음은 public synonym을 제거하는 예이다.

```
gSQL> DROP PUBLIC SYNONYM MainEmp;

Synonym dropped.
```

<a id="f530ed61ac777dfe"></a>
### 호환성

SQL 표준에서는 DROP SYNONYM 구문을 정의하지 않고 있다.

<a id="3c06b4f8fc7619f2"></a>
### 참조

관련 내용은 [CREATE SYNONYM](#5ede806fa2325e7c)을 참조한다.

<a id="528ddb8580a6edc6"></a>
## DROP TABLE

<a id="ab7d21f20fd2569b"></a>
### 기능

테이블을 제거한다.

> 휴지통 기능이 활성화되어 있을 경우, 테이블이 즉시 제거되지 않고 휴지통에 보관된다.

<a id="b4ccc60dd8d969b3"></a>
### 구문

```
<drop table statement> ::=
    DROP TABLE [ IF EXISTS ] table_name
    [ <drop behavior> ]
    [ PURGE ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
    | CASCADE CONSTRAINTS
```

<a id="e2d0541adc7f50ee"></a>
### 사용 범위 및 접근 권한

&lt;drop table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블의 소유자 
- 해당 테이블에 대해 CONTROL TABLE ON TABLE 
- 테이블이 속한 스키마에 대해 (DROP TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY TABLE ON DATABASE

<a id="d4452d6db8fb83a9"></a>
### 구문 규칙 및 파라미터

<a id="2f4b2ec049fa1a00"></a>
#### IF EXISTS

테이블이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="cfa0d81a295dfb0a"></a>
#### table_name

제거할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

Database를 생성할 때 자동으로 생성되는 다음과 같은 테이블들은 삭제할 수 없다.

- DEFINITION_SCHEMA 스키마의 테이블들 
- FIXED_TABLE_SCHEMA 스키마의 테이블들

테이블에 생성된 제약 조건과 인덱스도 함께 제거한다.

<a id="efada5835d2362c0"></a>
#### drop behavior

현재는 RESTRICT/ CASCADE가 동일하게 동작한다.   
생략할 경우, 기본값은 RESTRICT 이다.

<a id="770563263d9aa55b"></a>
#### purge

휴지통 기능이 활성화된 경우에도 테이블을 휴지통에 보관하지 않고 즉시 제거한다.

<a id="063f3566716eaa09"></a>
### 설명

DROP TABLE과 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="7c5e7dce90ec9936"></a>
### 사용 예

다음은 일반 테이블을 제거하는 예이다.

```
gSQL> DROP TABLE region;

Table dropped.
```

다음과 같이 IF EXISTS 구문을 사용하면 테이블이 존재하지 않더라도 에러가 발생하지 않는다.

```
gSQL> DROP TABLE IF EXISTS invalid_table;

Table dropped.
```

다음은 DROP 된 테이블을 ROLLBACK 하는 예이다.

```
gSQL> SELECT r_regionkey, r_name FROM region;

R_REGIONKEY R_NAME                   
----------- -------------------------
          0 AFRICA                   
          1 AMERICA                  
          2 ASIA                     
          3 EUROPE                   
          4 MIDDLE EAST              

5 rows selected.


gSQL> DROP TABLE region;

Table dropped.


gSQL> SELECT r_regionkey, r_name FROM region;

ERR-42000(16040): table or view does not exist : 
SELECT r_regionkey, r_name FROM region
                                *
ERROR at line 1:


gSQL> ROLLBACK;

Rollback complete.


gSQL> SELECT r_regionkey, r_name FROM region;

R_REGIONKEY R_NAME                   
----------- -------------------------
          0 AFRICA                   
          1 AMERICA                  
          2 ASIA                     
          3 EUROPE                   
          4 MIDDLE EAST              

5 rows selected.
```

<a id="1b9dad2596a81ad8"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- IF EXISTS 
- CASCADE CONSTRAINTS

**SQL 표준 호환성**

<a id="dbbb0714a02e51f3"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |

<a id="9fc255e5ee91092a"></a>
### 참조

관련 내용은 [CREATE TABLE](#060501387611d25a)을 참조한다.

<a id="0905e5b2ffc06135"></a>
## DROP TABLESPACE

<a id="39ace2cf535cfd2c"></a>
### 기능

테이블스페이스를 제거한다.

<a id="4328d7647dad37bc"></a>
### 구문

```
<drop tablespace statement> ::=
    DROP TABLESPACE [ IF EXISTS ] tablespace_name
        [ INCLUDING CONTENTS ]
        [ { AND | KEEP } DATAFILES ]
        [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
    | CASCADE CONSTRAINTS
```

<a id="9082fa6367313077"></a>
### 사용 범위 및 접근 권한

&lt;drop tablespace definition&gt; 구문을 수행하려면 사용자에게 DROP TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="80c033ac5de4393f"></a>
### 구문 규칙 및 파라미터

<a id="e3d1ff054f5bf320"></a>
#### IF EXISTS

테이블스페이스가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="7fb7d23e6e6faf22"></a>
#### tablespace_name

제거할 테이블스페이스의 이름이다.

Database를 생성할 때 구축되는 다음과 같은 시스템 테이블스페이스는 제거할 수 없다.

- DICTIONARY_TBS: system tablespace for dictionary management 
- MEM_UNDO_TBS: system tablespace for default undo tablespace 
- MEM_DATA_TBS: system tablespace for default user data tablespace 
- MEM_TEMP_TBS: system tablespace for default temporary tablespace

> tablespace_name이 사용자들의 default tablespace로 사용되고 있었다면 tablespace가 제거된 후에는 객체를 위한 공간을 할당받을 수 없다. 따라서 tablespace를 제거한 후에 [ALTER USER](18-sql-references-a-b.md#7fcf3795e062819a) 구문을 사용하여 사용자들의 default tablespace를 변경해 주어야 한다.

<a id="64e29b2b05fbf305"></a>
#### INCLUDING CONTENTS

테이블스페이스에 속하는 객체 (table, index, key constraints)를 삭제한다. 테이블스페이스에 속하는 table을 참조하는 index와 key constraints가 테이블스페이스 외부에 존재할 경우에는 이들도 함께 삭제한다.

INCLUDING CONTENTS 구문을 사용하지 않을 경우에는 테이블스페이스에 속하는 객체가 없어야 한다.

<a id="6821c931ca967167"></a>
#### [ { AND | KEEP } DATAFILES ]

테이블스페이스를 구성하는 데이터 파일들을 함께 삭제할지 여부를 지정한다.   
Memory temporary tablespace에는 데이터 파일이 존재하지 않으므로, 해당 절은 무시된다.

- AND DATAFILES 
    - 데이터 파일들을 함께 삭제한다. 
- KEEP DATAFILES 
    - 데이터 파일을 삭제하지 않고 남겨둔다. 
- 명시하지 않을 경우, 기본값은 KEEP DATAFILES 이다.

<a id="c6c30a6a50fd0619"></a>
#### drop behavior

현재는 RESTRICT/ CASCADE가 동일하게 동작한다.   
생략할 경우, 기본값은 RESTRICT 이다.

<a id="cf55ab96a1adbee3"></a>
### 설명

다른 Data Definition Language (DDL)과 달리 DROP TABLESPACE 구문은 ROLLBACK 할 수 없으며, 구문을 수행한 transaction이 자동으로 COMMIT 된다. 이 때 제거하는 테이블스페이스에 포함된 휴지통 객체들도 함께 제거된다.

<a id="3da3b0e35833b6ee"></a>
### 사용 예

다음은 tablespace와 함께 tablespace에 존재하는 모든 객체와 tablespace를 구성하는 모든 data file을 삭제하는 예이다.

```
gSQL> DROP TABLESPACE space1 INCLUDING CONTENTS AND DATAFILES CASCADE CONSTRAINTS;

Tablespace dropped.
```

다음은 IF EXISTS 구문을 사용하여 tablespace가 존재하지 않더라도 에러가 발생하지 않도록 하는 예이다.

```
gSQL> DROP TABLESPACE IF EXISTS not_exist_tablespace;

Tablespace dropped.
```

<a id="8c21a81981dbef69"></a>
### 호환성

SQL 표준은 tablespace에 대한 개념을 다루지 않고 있다.

<a id="dcb03db832fd83a2"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE MEMORY DATA TABLESPACE](#5dc8246fbc0a52e1)
- [CREATE MEMORY TEMPORARY TABLESPACE](#101999ca47732e9f)
- [ALTER TABLESPACE](18-sql-references-a-b.md#e50680549a4cafe3)

<a id="c4934ee399839206"></a>
## DROP USER

<a id="c55f8404281294c4"></a>
### 기능

데이터베이스 사용자를 제거한다.

<a id="54fd0c8f617e3752"></a>
### 구문

```
<drop user statement> ::=
    DROP USER [ IF EXISTS ] user_identifier [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
```

<a id="b9bedae4b4cfb02d"></a>
### 사용 범위 및 접근 권한

&lt;drop user statement&gt; 구문을 수행하려면 사용자에게 DROP USER ON DATABASE 권한이 있어야 한다.

> user_identifier가 소유한 스키마가 존재하지 않아야 한다.  
> 스키마 제거에 대한 자세한 내용은 [DROP SCHEMA](#e766128ab8947c2f) 구문을 참조한다.

<a id="d7e64004d4744ef8"></a>
### 구문 규칙 및 파라미터

<a id="988b1048878df466"></a>
#### IF EXISTS

사용자가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="c00d925d610ab3ff"></a>
#### user_identifier

제거할 데이터베이스 사용자의 이름이다.   
단, database를 생성할 때 자동으로 생성되는 "SYS" 등과 같은 사용자는 제거할 수 없다.

다음과 같이 user_identifier가 생성했으나, 소유자가 아닌 객체는 제거하지 않는다.

- Role 
- Tablespace

<a id="5bd07800dad046ae"></a>
#### &lt;drop behavior&gt;

- RESTRICT 
    - User가 소유한 다음과 같은 SQL schema object가 존재하지 않아야 한다.
        - Table, view 
        - Index 
        - Sequence 
        - Table constraint 
- CASCADE 
    - User가 소유한 다음과 같은 SQL schema object를 모두 제거한다. 
        - Table, view 
        - Index 
        - Sequence 
        - Table constraint
- 생략할 경우, 기본값은 RESTRICT 이다.

> DBMS에서 user와 schema의 관계   
> 
> 
> - Oracle
>     - User : schema = 1 : 1 
>     - CASCADE 할 때 schema도 함께 제거한다. 
> 
> 
> 
> - DB2 
>     - OS user와 동일하다. 
>     - User를 생성하고 제거하는 별도의 SQL 구문이 없다. 
> 
> 
> 
> - Postgres 
>     - User : schema = 1 : N
>     - CASCADE 옵션이 없으며 user가 소유한 모든 객체와 다른 사용자에게 부여한 모든 권한을 제거해야 user를 제거할 수 있다. 
> 
> 
> 
> - MySQL 
>     - Database : schema = 1 : 1
>     - User는 database (schema)의 하위 객체이며, CASCADE 옵션이 존재하지 않는다.
> 

<a id="7430f17ba4bec4bf"></a>
### 설명

GOLDILOCKS에서 user와 schema의 관계는 1 : N 이다.   
즉, user가 schema를 소유하지 않을 수도 있고, 다수의 schema를 소유할 수도 있다.

User 객체를 제거하려면 user가 소유한 모든 schema를 제거해야 한다. 이 때, 제거하는 user 객체의 휴지통 객체들도 함께 제거된다.

<a id="ea156f06af5ade99"></a>
### 사용 예

다음은 user가 소유한 모든 schema를 제거한 후 해당 user를 제거하는 예이다.

```
gSQL> DROP SCHEMA u1 CASCADE;

Schema dropped.

gSQL> DROP USER u1 CASCADE;

User dropped.
```

다음은 IF EXISTS 구문을 사용하여 user가 존재하지 않더라도 에러가 발생하지 않도록 하는 예이다.

```
gSQL> DROP USER IF EXISTS not_exist_user;

User dropped.
```

<a id="7a8e6c682f3821a8"></a>
### 호환성

SQL 표준에서는 user의 개념은 다루고 있지만 user의 생성 및 제거와 관련된 SQL 구문은 정의하지 않고 있다.

<a id="ba9645fdf8415f2c"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE USER](#bcf4364429be6a9b)
- [ALTER USER](18-sql-references-a-b.md#7fcf3795e062819a)
- [DROP SCHEMA](#e766128ab8947c2f)

<a id="7271de5cbf690942"></a>
## DROP VIEW

<a id="5fcad3f37c1fe826"></a>
### 기능

View를 제거한다.

<a id="e57cb5c4bc8de3a3"></a>
### 구문

```
<drop view statement> ::=
    DROP VIEW [ IF EXISTS ] view_name
    ;
```

<a id="d65f40959942524d"></a>
### 사용 범위 및 접근 권한

&lt;drop view statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 view의 소유자 
- 해당 view에 대해 CONTROL TABLE ON TABLE 
- View가 속한 스키마에 대해 (DROP VIEW 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY VIEW ON DATABASE

<a id="9e88b2f5aa5afbad"></a>
### 구문 규칙 및 파라미터

<a id="1139854ce0f6f95f"></a>
#### IF EXISTS

View가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="fa9a6827fa971dfe"></a>
#### view_name

제거할 view의 이름이다.   
schema_name.view_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="6efa07f9913b56be"></a>
### 설명

DROP VIEW와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="bf94e09de030c8b2"></a>
### 사용 예

다음은 view를 제거하는 예이다.

```
gSQL> DROP VIEW v1;

View dropped.
```

다음은 IF EXISTS 구문을 사용하여 view가 존재하지 않더라도 에러가 발생하지 않도록 하는 예이다.

```
gSQL> DROP VIEW IF EXISTS not_exist_view;

View dropped.
```

<a id="21c4cd3ff1b14c1c"></a>
### 호환성

SQL 표준에서는 IF EXISTS 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="082045e0cff9d064"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |

<a id="a8c345f519403d71"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE VIEW](#6f697c93c59acd84)
- [ALTER VIEW](18-sql-references-a-b.md#f911f10e438cdcf6)

<a id="460d0af355f8583e"></a>
## EXECUTE IMMEDIATE 'sql_string'

<a id="f6cae651e3e07d39"></a>
### 기능

프로그램 작성 시점에 정의되지 않았던 dynamic SQL 문장을 수행한다.

<a id="2c8b109cfef22faa"></a>
### 구문

```
<execute immediate statement> ::=
    EXECUTE IMMEDIATE <SQL statement variable>
    ;

<SQL statement variable> ::=
      variable_name
    | 'sql statement'
    | "sql statement"
    | sql statement
```

<a id="b554a9777542d243"></a>
### 사용 범위 및 접근 권한

Embedded SQL에서 사용할 수 있다.   
Dynamic SQL 구문의 종류에 부합하는 수행 권한이 있어야 한다.

<a id="eafb82080f638d9b"></a>
### 구문 규칙 및 파라미터

<a id="4fd9dbac9a2eda16"></a>
#### &lt;SQL statement variable&gt;

&lt;SQL statement variable&gt;이 참조하는 dynamic SQL 문장은 host variable (:var)이나 parameter marker (?)를 사용할 수 없다.

다음과 같은 네 가지 유형의 &lt;SQL statement variable&gt;을 사용할 수 있다.

- variable_name: SQL이 저장된 변수 
- 'sql statement': Single quote (')로 묶인 SQL 문장 
- "sql statement": Double quote (")로 묶인 SQL 문장 
- sql statement: Quote 없는 SQL 문장

Single-quoted string 내에 문자열 data를 표현하려면 다음과 같이 single quote (')를 두 번 기술해야 한다.

```
{
    ...
    EXEC SQL EXECUTE IMMEDIATE 'INSERT INTO t1 VALUES ( ''literal data'' )'; 
    ...
}
```

SQL 문장이 질의 결과를 갖는 query인 경우, 수행에는 성공하지만 그 결과는 얻을 수 없다.

<a id="54a82f1c3be578d2"></a>
#### variable_name

variable_name에 대응되는 type은 character string이어야 한다.   
variable_name에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="3c9fa82c9dbb3d9f"></a>
#### sql statement

sql statement에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="58a359630079ada4"></a>
### 설명

EXECUTE IMMEDIATE 'sql_string' 구문은 dynamic embedded SQL 응용 프로그램에서 host variable이 없는 non-query SQL에 사용될 수 있다. 별도의 준비과정이 필요하지 않기 때문에, DDL이나 DML 등을 일회성으로 수행하기에 적합하다.

자세한 내용은 [Embedded Dynamic SQL](../part-05-developer-manual/33-embedded-sql.md#8a6b778c3ec6ed54)을 참조한다.

<a id="6ed6684dd74a0b39"></a>
### 사용 예

다음은 EXECUTE IMMEDIATE 'sql_string'이 embedded SQL 소스 코드 내에서 사용되는 예이다.

```
{
    ...
    sprintf(sSqlStmt, "INSERT INTO EMP_RND\n"
            "SELECT *\n"
            "FROM   EMP\n"
            "WHERE  JOB = 'RND'\n" );
    EXEC SQL EXECUTE IMMEDIATE :sSqlStmt;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    ...
}
```

EXECUTE IMMEDIATE 'sql_string'이 사용된 전체 소스 코드는 [Dynamic Embedded SQL Example Program](../part-05-developer-manual/33-embedded-sql.md#57b2bba64c05273e)에서 확인할 수 있다.

<a id="400b9c81fba143a2"></a>
### 호환성

**SQL 표준 호환성**

<a id="10259f38864328c1"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |

<a id="883f26a1c1317f74"></a>
### 참조

관련 내용은 다음을 참조한다.

- [PREPARE statement_name](20-sql-references-h-z.md#a3d45ff2e9b51c9a)
- [EXECUTE statement_name](#0f32cf28eca2fe23)
- [Embedded Dynamic SQL](../part-05-developer-manual/33-embedded-sql.md#8a6b778c3ec6ed54)

<a id="0f32cf28eca2fe23"></a>
## EXECUTE statement_name

<a id="10d0c680f6934de6"></a>
### 기능

준비된 statement를 수행한다.

<a id="5a308d4d4d0ab235"></a>
### 구문

```
<execute statement> ::=
    EXECUTE statement_name [ <parameter using clause> ] [ <result into clause> ]
    ;

<parameter using clause> ::=
      <using parameter arguments>

<using parameter arguments> ::=
    USING variable_name [, ...]

<result into clause> ::=
      <into result arguments>

<into result arguments> ::=
    INTO variable_name [, ...]
```

<a id="73950e0de2130f96"></a>
### 사용 범위 및 접근 권한

Embedded SQL에서 사용할 수 있다.   
Dynamic SQL 구문의 종류에 부합하는 수행 권한이 있어야 한다.

<a id="11aa1a15abe9dae2"></a>
### 구문 규칙 및 파라미터

<a id="2dd0bdc525d9a90a"></a>
#### statement_name

준비된 statement의 이름이다.  
[PREPARE statement_name](20-sql-references-h-z.md#a3d45ff2e9b51c9a) 구문을 사용하여 statement_name을 준비해야 한다.

statement_name이 참조하는 dynamic SQL 문장이 dynamic parameter를 포함하고 있는 경우, &lt;parameter using clause&gt;를 명시해야 한다.

```
{
    ...
    EXEC SQL PREPARE stmt1 FROM 'DELETE FROM t1 WHERE c1 > ?';
    EXEC SQL EXECUTE stmt1 USING :sValue;
    ...
}
```

```
{

    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT COUNT(*) INTO :v1 FROM t1';
    EXEC SQL EXECUTE stmt1 USING :sValue;
    ...
}
```

statement_name이 참조하는 dynamic SQL 문장이 query이거나 결과가 존재하는 stored function일 경우, &lt;result into clause&gt;를 명시해야 한다.

```
{
    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT COUNT(*) FROM t1';
    EXEC SQL EXECUTE stmt1 INTO :sValue;
    ...
}
```

질의가 여러 건인 경우 정상적으로 수행되지만 결과는 최초 한 건만 얻을 수 있다.   
여러 건의 결과를 얻기 위해서는 다음과 같은 커서 관련 구문을 사용해야 한다.

- [DECLARE cursor_name](#f94895843614f7cc)
- [OPEN cursor_name](20-sql-references-h-z.md#afdd7cb54cc78da0)
- [FETCH cursor_name](#47babe65e4397c2a)
- [CLOSE cursor_name](#b130e0aa9376fe9d)

질의 결과가 없을 경우, NO DATA로 완료된다.

<a id="0b9431fdeea822cd"></a>
#### [ &lt;parameter using clause&gt; ] [ &lt;result into clause&gt; ]

&lt;parameter using clause&gt;와 &lt;result into clause&gt;는 순서에 관계없이 기술할 수 있지만 중복해서 기술하지 않아야 한다.

<a id="8f0a00723cd088cd"></a>
#### &lt;parameter using clause&gt;

statement_name이 참조하는 dynamic SQL 문장에 parameter가 존재할 경우, parameter에 대한 정보를 &lt;using parameter arguments&gt; 절로 명시한다.

<a id="e433a1b9b055d212"></a>
#### &lt;using parameter arguments&gt;

&lt;using parameter arguments&gt; 구문이 사용될 경우, variable_name의 개수는 statement_name이 참조하는 dynamic SQL 문장에 포함된 parameter의 개수와 동일해야 한다.

나열된 variable_name은 기술된 순서대로 dynamic parameter 순서에 대응된다.

```
{

    ...
    EXEC SQL PREPARE stmt1 FROM 'DELETE FROM t1 WHERE c1 IN ( ?, ?, ? )';
    EXEC SQL EXECUTE stmt1 USING :sValue1, :sValue2, :sValue3;
    ... 
}
```

<a id="2ca06e5d5f3e1e1c"></a>
#### &lt;result into clause&gt;

statement_name이 참조하는 dynamic SQL 문장이 query일 경우, 결과 column에 대한 정보를 &lt;into result arguments&gt; 절로 명시한다.

결과값이 null인 경우, INDICATOR를 명시하지 않으면 [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] 에러가 발생한다.

<a id="9392b4581121b418"></a>
#### &lt;into result arguments&gt;

&lt;into result arguments&gt; 구문이 사용될 경우, variable_name의 개수는 statement_name이 참조하는 dynamic SQL 문장의 결과 column 개수와 동일해야 한다.

나열된 variable_name은 기술된 순서대로 dynamic parameter 순서에 대응된다.

```
{

    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT MIN(salary), MAX(salary), AVG(salary) FROM employee';
    EXEC SQL EXECUTE stmt1 INTO :sMinValue, :sMaxValue, :sAvgValue;
    ... 
}
```

<a id="3047c7cd43827bbc"></a>
### 설명

statement_name은 embedded SQL 소스 코드에서 precompiler에게 statement를 알려주는 식별자로써 host variable이 아니기 때문에 별도의 type이나 선언이 필요하지 않다. EXECUTE statement_name 구문은 PREPARE statement_name 구문 뒤에 쓰여야 한다.

자세한 내용은 [Embedded Dynamic SQL](../part-05-developer-manual/33-embedded-sql.md#8a6b778c3ec6ed54)을 참조한다.

<a id="374329984b5b5815"></a>
### 사용 예

다음은 EXECUTE statement_name이 embedded SQL 소스 코드에서 사용되는 예이다.

```
{
    ...
    sprintf( sUpdateSql, "UPDATE EMP SET sal = sal * :v1 WHERE JOB = 'SALES'");
    EXEC SQL PREPARE UPDATE_STMT FROM :sUpdateSql;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }

    sRatio = 1.1;
    EXEC SQL EXECUTE UPDATE_STMT USING :sRatio;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    ...
}
```

EXECUTE statement_name이 사용된 전체 소스 코드는 [Dynamic Embedded SQL Example Program](../part-05-developer-manual/33-embedded-sql.md#57b2bba64c05273e)에서 확인할 수 있다.

<a id="61d82e91eb11bc76"></a>
### 호환성

**SQL 표준 호환성**

<a id="cae73a3c1988812f"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic dynamic SQL | O |
| B032 | Extended dynamic SQL | X |

<a id="658529814fda308f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [PREPARE statement_name](20-sql-references-h-z.md#a3d45ff2e9b51c9a)
- [DECLARE cursor_name](#f94895843614f7cc)
- [OPEN cursor_name](20-sql-references-h-z.md#afdd7cb54cc78da0)
- [FETCH cursor_name](#47babe65e4397c2a)
- [CLOSE cursor_name](#b130e0aa9376fe9d)
- [Embedded Dynamic SQL](../part-05-developer-manual/33-embedded-sql.md#8a6b778c3ec6ed54)

<a id="47babe65e4397c2a"></a>
## FETCH cursor_name

<a id="a8b5a84317d8951a"></a>
### 기능

커서를 결과 집합의 특정 row에 위치시키고, 해당 row의 값을 호스트 변수에 얻어온다.

<a id="1988ac0dd0de7282"></a>
### 구문

```
<fetch statement> ::=
    FETCH [ <fetch orientation> ] [ FROM ] cursor_name 
        <result into clause>
    ;

<fetch orientation> ::=
      NEXT
    | PRIOR
    | FIRST
    | LAST
    | CURRENT
    | ABSOLUTE position
    | RELATIVE position

<result into clause> ::=
      <into result arguments>

<into result arguments> ::=
    INTO variable_name [, ...]
```

<a id="5129d568014dbfbc"></a>
### 구문 규칙 및 파라미터

<a id="b09eb1e3fe80a05d"></a>
#### [ FROM ] cursor_name

세션 내에서 open 된 커서이어야 한다.   
FROM은 생략할 수 있다.

<a id="9b30b6416be764c5"></a>
#### &lt;fetch orientation&gt;

FETCH NEXT 이외의 &lt;fetch orientation&gt;을 사용하려면 scrollable cursor를 사용해야 한다.   
&lt;fetch orientation&gt;을 생략할 경우, 기본값은 NEXT이다.

Open 된 커서는 결과 집합에 대해 아래 그림과 같은 커서 위치 정보를 갖는다.

<a id="d7d0791c8c300f19"></a>
![커서의 위치 정보](../assets/images/6ebb8f5d9ab52da6.png)

**커서의 위치**

<a id="526da3384b2ba085"></a>
| 커서의 위치 | 설명 |
| --- | --- |
| BEFORE THE FIRST ROW | 결과 집합의 첫 번째 row의 이전 위치에 있는 상태로써 OPEN 시점의 위치도 이에 해당한다. |
| ON A CERTAIN ROW | FETCH를 통해 결과 집합의 특정 row에 위치한 상태이다. |
| AFTER THE LAST ROW | 결과 집합의 마지막 row 이후의 위치에 있는 상태이다. |

현재 커서의 위치를 기준으로 각 &lt;fetch orientation&gt;은 다음과 같이 동작한다.

- NEXT: 현재 위치의 다음 row를 검색한다.
- PRIOR: 현재 위치의 이전 row를 검색한다. 
- FIRST: 결과 집합의 첫 번째 row를 검색한다. 
- LAST: 결과 집합의 마지막 row를 검색한다. 
- CURRENT: 현재 위치의 row를 검색한다. 
- ABSOLUTE position 
    - 결과 집합에서 position의 위치에 해당하는 row를 검색한다. 
    - Position 값이 음수일 경우 AFTER THE LAST ROW로부터 이전의 위치에 해당하는 row를 검색한다. 
- RELATIVE position 
    - 현재 위치에서 position만큼 떨어진 위치에 해당하는 row를 검색한다.

<a id="424995e3b9b748f9"></a>
#### &lt;result into clause&gt;

&lt;into result arguments&gt;를 사용하여 결과 column을 획득할 변수 정보를 기술한다.

결과값이 null 인 경우, INDICATOR를 명시하지 않으면 [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] 에러가 발생한다.

<a id="000f804c02b5b951"></a>
#### &lt;into result arguments&gt;

INTO 절에 기술된 변수의 개수는 커서의 결과 집합의 column 개수와 동일해야 한다.

<a id="31ed9f748f340bf9"></a>
### 설명

FETCH를 수행한 후에 커서 위치가 BEFORE THE FIRST ROW 거나 AFTER THE LAST LOW 인 경우, &lt;fetch orientation&gt;에 입력된 위치값에 관계없이 동일한 위치에 자리한다.

<a id="1a7931e22838baeb"></a>
### 사용 예

다음은 interactive SQL (gsql)에서 SCROLL 커서를 선언하고, 다양한 &lt;fetch orientation&gt;의 동작을 보여주는 예이다.

```
gSQL> DECLARE cur_scroll SCROLL CURSOR FOR SELECT id, data FROM t1;

Cursor declared.

gSQL> OPEN cur_scroll;

Cursor is open.

gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> FETCH NEXT cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH NEXT cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   2 data_2

1 row fetched.

gSQL> FETCH PRIOR cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH PRIOR cur_scroll INTO :v_id, :v_data;

no rows fetched.

gSQL> FETCH FIRST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH FIRST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH LAST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH LAST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH FIRST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH CURRENT cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH LAST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH CURRENT cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH ABSOLUTE 3 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH CURRENT cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH ABSOLUTE 1 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH ABSOLUTE -1 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH ABSOLUTE 6 cur_scroll INTO :v_id, :v_data;

no rows fetched.

gSQL> FETCH ABSOLUTE -6 cur_scroll INTO :v_id, :v_data;

no rows fetched.

gSQL> FETCH ABSOLUTE 3 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH ABSOLUTE -3 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH RELATIVE 1 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   4 data_4

1 row fetched.

gSQL> FETCH RELATIVE -1 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH RELATIVE 5 cur_scroll INTO :v_id, :v_data;

no rows fetched.

gSQL> FETCH RELATIVE -5 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> CLOSE cur_scroll;

Cursor closed.
```

<a id="2a10b1fe991b6a46"></a>
### 호환성

SQL 표준에서는 &lt;fetch orientation&gt; 중에 CURRENT를 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="09c5e25085d06692"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F431 | Read-only scrollable cursors | O |
| B031 | Basic dynamic SQL | O |

<a id="2c80bdccb8ab124d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#f94895843614f7cc)
- [OPEN cursor_name](20-sql-references-h-z.md#afdd7cb54cc78da0)
- [CLOSE cursor_name](#b130e0aa9376fe9d)

<a id="26a6cc4b84f3c4ee"></a>
## FLASHBACK TABLE

<a id="d995ff3592c2b5dc"></a>
### 기능

휴지통에 보관되어 있는 테이블 객체를 복구한다.

<a id="9e54566ca582b9ef"></a>
### 구문

```
<flashback table statement> ::=
    FLASHBACK TABLE table_name
    TO BEFORE DROP [ RENAME TO new_table_name ]
    ;
```

<a id="2c4bb73c1ab5e238"></a>
### 사용 범위 및 접근 권한

&lt;flashback table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블의 소유자 
- 해당 테이블에 대해 CONTROL TABLE ON TABLE 
- 테이블이 속한 스키마에 대해 (DROP TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY TABLE ON DATABASE

<a id="9ac5577287bfe645"></a>
### 구문 규칙 및 파라미터

<a id="dd6b1c6e8cac6023"></a>
#### table_name

휴지통에 저장된 객체의 이름 또는 제거된 테이블의 이름이다.  
제거된 테이블 이름에는 schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="4512efcdfac6cf1d"></a>
#### new_table_name

복구되는 테이블의 새로운 이름이다.  
스키마 내에 동일한 테이블 이름이 존재하지 않아야 한다.

<a id="f9560414153bb13c"></a>
### 설명

휴지통에 저장된 객체 이름이나 제거된 테이블의 이름을 사용하여 휴지통에 보관되어 있는 테이블 객체를 복구한다. 만약 제거된 테이블과 중복된 이름이 있는 경우 가장 최신의 테이블 객체를 복구한다.

복구하려는 테이블 객체의 이름이 존재하면 에러가 발생하는데 RENAME TO 절을 사용하여 새로운 테이블 이름으로 복구할 수 있다. 복구된 테이블의 제약 조건과 인덱스는 제거되기 전의 이름으로 복구되는데 만약 제거되기 전의 제약 조건 및 인덱스와 동일한 이름이 이미 존재할 경우, 휴지통에 저장된 이름으로 복구된다.

다른 Data Definition Language (DDL)과 달리 FLASHBACK TABLE 구문은 ROLLBACK 할 수 없으며, 구문을 수행한 transaction이 자동으로 COMMIT 된다.

<a id="8581d9bab0ea229c"></a>
### 사용 예

다음은 휴지통에 저장된 객체 이름으로 테이블을 복구하는 예이다.

```
gSQL> SELECT SCHEMA_NAME, OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

SCHEMA_NAME OBJECT_NAME                          ORIGINAL_NAME OBJECT_TYPE
----------- ------------------------------------ ------------- -----------
PUBLIC      BIN$106A4F90165D11EA9C5C835D3E4BBBF7 T1            TABLE      

1 row selected.

gSQL> FLASHBACK TABLE "BIN$106A4F90165D11EA9C5C835D3E4BBBF7" TO BEFORE DROP;

Flashback complete.
```

다음은 제거되기 전 테이블의 이름으로 휴지통에서 복구하는 예이다.

```
gSQL> SELECT SCHEMA_NAME, OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

SCHEMA_NAME OBJECT_NAME                          ORIGINAL_NAME OBJECT_TYPE
----------- ------------------------------------ ------------- -----------
PUBLIC      BIN$106A4F90165D11EA9C5C835D3E4BBBF7 T1            TABLE      

gSQL> FLASHBACK TABLE T1 TO BEFORE DROP;

Flashback complete.
```

<a id="9fda294368d34340"></a>
### 호환성

SQL 표준에서는 &lt;flashback table statement&gt;를 다루지 않고 있다.

<a id="b0aff277cb3cfe70"></a>
### 참조

관련 내용은 다음을 참조한다.

- [테이블 휴지통 관리](13-sql-objects.md#243206ba1e62a6ec)
- [PURGE](20-sql-references-h-z.md#5af8b25b43a30381)

<a id="2efe38e72e090afb"></a>
## GRANT privileges TO

<a id="388d5a10ac0aa825"></a>
### 기능

사용자에게 권한을 부여한다.

<a id="e002f83b91e16c27"></a>
### 구문

```
<grant privilege statement> ::=
    GRANT <privilege> TO <grantee> [, ...]
        [ WITH GRANT OPTION ]
    ;

<grantee> ::=
      PUBLIC
    | user_identifier
    ;
    
<privilege> ::=
      <database privilege>
    | <tablespace privilege>
    | <schema privilege>
    | <table privilege>
    | <sequence privilege>
    | <procedure privilege>

<database privilege> ::=
      ALL [ PRIVILEGES ] [ON DATABASE]
    | <database action> [, ...] [ON DATABASE]

<database action> ::=
      ADMINISTRATION
    | ANALYZE ANY 
    | ALTER DATABASE
    | ALTER SYSTEM
    | AUDIT SYSTEM
    | ACCESS CONTROL
    | CREATE SESSION
    | CREATE PROFILE
    | ALTER PROFILE
    | DROP PROFILE 
    | CREATE USER
    | ALTER USER
    | DROP USER 
    | CREATE ROLE
    | ALTER ROLE
    | DROP ROLE
    | CREATE TABLESPACE
    | ALTER TABLESPACE
    | DROP TABLESPACE
    | USAGE TABLESPACE
    | CREATE SCHEMA
    | ALTER SCHEMA
    | DROP SCHEMA
    | CREATE PUBLIC SYNONYM
    | DROP PUBLIC SYNONYM
    | CREATE ANY TABLE
    | ALTER ANY TABLE
    | DROP ANY TABLE
    | SELECT ANY TABLE
    | INSERT ANY TABLE
    | DELETE ANY TABLE
    | UPDATE ANY TABLE
    | LOCK ANY TABLE
    | CREATE ANY VIEW
    | DROP ANY VIEW
    | CREATE ANY SEQUENCE
    | ALTER ANY SEQUENCE
    | DROP ANY SEQUENCE
    | USAGE ANY SEQUENCE
    | CREATE ANY INDEX
    | ALTER ANY INDEX
    | DROP ANY INDEX
    | CREATE ANY SYNONYM
    | DROP ANY SYNONYM
    | CREATE ANY PROCEDURE
    | ALTER ANY PROCEDURE
    | DROP ANY PROCEDURE
    | EXECUTE ANY PROCEDURE
    | CREATE ANY PACKAGE
    | ALTER ANY PACKAGE
    | DROP ANY PACKAGE
    | EXECUTE ANY PACKAGE
    | PURGE DBA_RECYCLEBIN

<tablespace privilege> ::=
      ALL [ PRIVILEGES ] ON TABLESPACE tablespace_name
    | <tablespace action> [, ...] ON TABLESPACE tablespace_name

<tablespace action> ::=
    CREATE OBJECT

<schema privilege> ::=
      ALL [ PRIVILEGES ] ON SCHEMA schema_name
    | <schema action> [, ...] [ON SCHEMA schema_name]

<schema action> ::=
      CONTROL SCHEMA
    | CREATE TABLE
    | ALTER TABLE 
    | DROP TABLE
    | SELECT TABLE
    | INSERT TABLE
    | DELETE TABLE
    | UPDATE TABLE
    | LOCK TABLE
    | CREATE VIEW
    | DROP VIEW
    | CREATE SEQUENCE
    | ALTER SEQUENCE
    | DROP SEQUENCE
    | USAGE SEQUENCE
    | CREATE INDEX
    | ALTER INDEX
    | DROP INDEX
    | ADD CONSTRAINT
    | CREATE SYNONYM
    | DROP SYNONYM
    | CREATE PROCEDURE
    | ALTER PROCEDURE
    | DROP PROCEDURE
    | EXECUTE PROCEDURE
    | CREATE PACKAGE
    | ALTER PACKAGE
    | DROP PACKAGE
    | EXECUTE PACKAGE

<table privilege> ::=
      ALL [ PRIVILEGES ] ON [TABLE] table_name
    | { <table action> | <column action> } [, ...] ON [TABLE] table_name

<table action> ::=
      CONTROL TABLE
    | SELECT
    | INSERT
    | UPDATE
    | DELETE
    | REFERENCES
    | LOCK
    | INDEX
    | ALTER

<column action> ::=
      SELECT ( column_name [, ...] )
    | INSERT ( column_name [, ...] )
    | UPDATE ( column_name [, ...] )
    | REFERENCES ( column_name [, ...] )

<sequence privilege> ::=
      ALL [ PRIVILEGES ] ON SEQUENCE sequence_name
    | <sequence action> ON SEQUENCE sequence_name

<sequence action> ::=
    USAGE

<procedure privilege> ::=
      ALL [ PRIVILEGES ] ON PROCEDURE procedure_name
    | <procedure action> ON PROCEDURE procedure_name

<procedure action> ::=
    EXECUTE

<package privilege> ::=
      ALL [ PRIVILEGES ] ON PACKAGE package_name
    | <package action> ON PACKAGE package_name

<package action> ::=
    EXECUTE
```

<a id="df2454293941c635"></a>
### 구문 규칙 및 파라미터

<a id="65063ca363830f80"></a>
#### &lt;grantee&gt;

권한을 부여받을 사용자이다.

- user_identifier 
    - 해당 사용자에게 권한을 부여한다
- PUBLIC 
    - 모든 사용자를 의미하는 authorization 객체이다.

<a id="4c33174a1d7b00e4"></a>
#### WITH GRANT OPTION

Grantee (권한을 부여받은 사용자)가 다른 사용자에게 해당 권한을 부여할 수 있도록 한다.

다음과 같이 동일한 &lt;privilege&gt;에 대한 권한을 부여할 때 WITH GRANT OPTION은 계속 유지된다.

- GRANT SELECT ON t1 TO u1 WITH GRANT OPTION; 
- GRANT SELECT ON t1 TO u1;

<a id="fc2600cd77964586"></a>
#### &lt;privilege&gt;

Grantee (권한을 부여받는 사용자)에게 부여할 권한이다.

Grantor (구문을 수행하는 사용자)는 다음 조건 중 하나를 만족해야 한다.

- Grantor가 WITH GRANT OPTION을 사용하여 해당 &lt;privilege&gt;를 소유한다.
    - Grantor는 구문을 수행하는 사용자가 된다. 
- Grantor가 ACCESS CONTROL ON DATABASE 권한을 소유한다.
    - Grantor는 객체의 소유자가 된다. 
        - &lt;database privilege&gt;: _SYSTEM 계정 
        - &lt;tablespace privilege&gt;: _SYSTEM 계정 
        - &lt;schema privilege&gt;: _SYSTEM 계정 
        - &lt;table privilege&gt;: table 의 소유자 
        - &lt;sequence privilege&gt;: sequence 의 소유자
        - &lt;procedure privilege&gt;: procedure/ function의 소유자
        - &lt;package privilege&gt;: package의 소유자

<a id="c4a45f155fc8d645"></a>
#### &lt;database privilege&gt;

데이터베이스 객체에 대한 권한이다.  
[ON DATABASE] 구문은 생략할 수 있다.

database privilege로 정의할 수 있는 database action은 다음과 같다.

- ALL [ PRIVILEGES ] [ON DATABASE] 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 DATABASE에 대해 소유한 모든 권한이다.

**Database privilege**

<a id="124b36e886c4b08e"></a>
| &lt;database action&gt; | 설명 |
| --- | --- |
| ADMINISTRATION | 서버 구동, 종료 권한 |
| ALTER DATABASE | ALTER DATABASE 구문을 수행할 수 있는 권한 |
| ALTER SYSTEM | ALTER SYSTEM 구문을 수행할 수 있는 권한 |
| AUDIT SYSTEM | Audit policy를 제어할 수 있는 권한 |
| ACCESS CONTROL | 모든 권한을 제어할 수 있는 권한 |
| CREATE SESSION | Database에 접속할 수 있는 권한 |
| CREATE PROFILE | Database에 profile을 생성할 수 있는 권한 |
| ALTER PROFILE | Database의 모든 profile을 변경할 수 있는 권한 |
| DROP PROFILE | Database의 모든 profile을 제거할 수 있는 권한 |
| CREATE USER | Database에 user를 생성할 수 있는 권한 |
| ALTER USER | Database의 모든 user를 변경할 수 있는 권한 |
| DROP USER | Database의 모든 user를 제거할 수 있는 권한 |
| CREATE ROLE | Database에 role을 생성할 수 있는 권한 |
| ALTER ROLE | Database의 모든 role을 변경할 수 있는 권한 |
| DROP ROLE | Database의 모든 role을 제거할 수 있는 권한 |
| CREATE TABLESPACE | Database에 tablespace를 생성할 수 있는 권한 |
| ALTER TABLESPACE | Database의 모든 tablespace를 변경할 수 있는 권한 |
| DROP TABLESPACE | Database의 모든 tablespace를 제거할 수 있는 권한 |
| USAGE TABLESPACE | Database의 모든 tablespace를 사용할 수 있는 권한 |
| CREATE SCHEMA | Database에 스키마를 생성할 수 있는 권한 |
| ALTER SCHEMA | Database의 모든 스키마를 변경할 수 있는 권한 |
| DROP SCHEMA | Database의 모든 스키마를 제거할 수 있는 권한 |
| CREATE PUBLIC SYNONYM | Database에 PUBLIC SYNONYM을 생성할 수 있는 권한 |
| DROP PUBLIC SYNONYM | Database의 모든 PUBLIC SYNONYM을 제거할 수 있는 권한 |
| CREATE ANY TABLE | Database의 모든 스키마에 테이블을 생성할 수 있는 권한 |
| ALTER ANY TABLE | Database의 모든 테이블을 변경할 수 있는 권한 |
| DROP ANY TABLE | Database의 모든 테이블을 제거할 수 있는 권한 |
| SELECT ANY TABLE | Database의 모든 테이블의 row를 검색할 수 있는 권한 |
| INSERT ANY TABLE | Database의 모든 테이블에 row를 생성할 수 있는 권한 |
| DELETE ANY TABLE | Database의 모든 테이블의 row를 삭제할 수 있는 권한 |
| UPDATE ANY TABLE | Database의 모든 테이블의 row를 갱신할 수 있는 권한 |
| LOCK ANY TABLE | Database의 모든 테이블에 LOCK 구문을 수행할 수 있는 권한 |
| CREATE ANY VIEW | Database의 모든 스키마에 view를 생성할 수 있는 권한 |
| DROP ANY VIEW | Database의 모든 view를 제거할 수 있는 권한 |
| CREATE ANY SEQUENCE | Database의 모든 스키마에 시퀀스를 생성할 수 있는 권한 |
| ALTER ANY SEQUENCE | Database의 모든 시퀀스를 변경할 수 있는 권한 |
| DROP ANY SEQUENCE | Database의 모든 시퀀스를 제거할 수 있는 권한 |
| USAGE ANY SEQUENCE | Database의 모든 시퀀스를 사용할 수 있는 권한 |
| CREATE ANY INDEX | Database의 모든 스키마에 인덱스를 생성할 수 있는 권한 |
| ALTER ANY INDEX | Database의 모든 인덱스를 변경할 수 있는 권한 |
| DROP ANY INDEX | Database의 모든 인덱스를 제거할 수 있는 권한 |
| CREATE ANY SYNONYM | Database의 모든 synonym을 생성할 수 있는 권한 |
| DROP ANY SYNONYM | Database의 모든 synonym을 제거할 수 있는 권한 |
| CREATE ANY PROCEDURE | Database의 모든 스키마에 procedure/ function을 생성할 수 있는 권한 |
| ALTER ANY PROCEDURE | Database의 모든 procedure/ function을 변경할 수 있는 권한 |
| DROP ANY PROCEDURE | Database의 모든 procedure/ function을 제거할 수 있는 권한 |
| EXECUTE ANY PROCEDURE | Database의 모든 procedure/ function을 수행할 수 있는 권한 |
| CREATE ANY PACKAGE | Database의 모든 스키마에 package를 생성할 수 있는 권한 |
| ALTER ANY PACKAGE | Database의 모든 package을 변경할 수 있는 권한 |
| DROP ANY PACKAGE | Database의 모든 package을 제거할 수 있는 권한 |
| EXECUTE ANY PACKAGE | Database의 모든 package을 수행할 수 있는 권한 |
| PURGE DBA_RECYCLEBIN | Database의 모든 휴지통을 제거할 수 있는 권한 |

<a id="bcb0739bd8f3d71c"></a>
#### &lt;tablespace privilege&gt;

테이블스페이스 객체에 대한 권한이다.

tablespace privilege로 정의할 수 있는 tablespace action은 다음과 같다.

- ALL [ PRIVILEGES ] ON TABLESPACE tablespace_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 TABLESPACE에 대해 소유한 모든 권한이다.

**Tablespace privilege**

<a id="813836fb043aa835"></a>
| &lt;tablespace action&gt; | 설명 |
| --- | --- |
| CREATE OBJECT | Tablespace에 객체를 생성할 수 있는 권한 |

<a id="f8b7678b048960ab"></a>
#### &lt;schema privilege&gt;

스키마 객체에 대한 권한이다.

- [ON SCHEMA schema_name] 생략 여부 
    - &lt;grantee&gt;가 다수일 경우 [ON SCHEMA schema_name] 구문을 생략할 수 없다. 
    - ALL [PRIVILEGES]를 사용할 경우 [ON SCHEMA schema_name] 구문을 생략할 수 없다. 
    - [ON SCHEMA schema_name] 구문을 생략할 경우 &lt;grantee&gt;는 하나의 user_identifier만 사용할 수 있으며, &lt;grantee&gt;의 스키마 검색 경로 중 첫 번째 스키마에 대한 권한을 부여한다.

schema privilege로 정의할 수 있는 schema action은 다음과 같다.

- ALL [ PRIVILEGES ] ON SCHEMA schema_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 SCHEMA에 대해 소유한 모든 권한이다.

**Schema privilege**

<a id="7e8efced92716988"></a>
| &lt;schema action&gt; | 설명 |
| --- | --- |
| CONTROL SCHEMA | 해당 스키마에 대한 모든 권한 |
| CREATE TABLE | 스키마에 테이블을 생성할 수 있는 권한 |
| ALTER TABLE | 스키마의 모든 테이블을 변경할 수 있는 권한 |
| DROP TABLE | 스키마의 모든 테이블을 제거할 수 있는 권한 |
| SELECT TABLE | 스키마의 모든 테이블의 row를 검색할 수 있는 권한 |
| INSERT TABLE | 스키마의 모든 테이블의 row를 생성할 수 있는 권한 |
| DELETE TABLE | 스키마의 모든 테이블의 row를 삭제할 수 있는 권한 |
| UPDATE TABLE | 스키마의 모든 테이블의 row를 갱신할 수 있는 권한 |
| LOCK TABLE | 스키마의 모든 테이블에 LOCK 구문을 수행할 수 있는 권한 |
| CREATE VIEW | 스키마에 view를 생성할 수 있는 권한 |
| DROP VIEW | 스키마의 모든 view를 제거할 수 있는 권한 |
| CREATE SEQUENCE | 스키마에 시퀀스를 생성할 수 있는 권한 |
| ALTER SEQUENCE | 스키마의 모든 시퀀스를 변경할 수 있는 권한 |
| DROP SEQUENCE | 스키마의 모든 시퀀스를 제거할 수 있는 권한 |
| USAGE SEQUENCE | 스키마의 모든 시퀀스를 사용할 수 있는 권한 |
| CREATE INDEX | 스키마에 인덱스를 생성할 수 있는 권한 |
| ALTER INDEX | 스키마의 모든 인덱스를 변경할 수 있는 권한 |
| DROP INDEX | 스키마의 모든 인덱스를 제거할 수 있는 권한 |
| ADD CONSTRAINT | 스키마에 제약 조건을 생성할 수 있는 권한 |
| CREATE SYNONYM | 스키마에 synonym을 생성할 수 있는 권한 |
| DROP SYNONYM | 스키마의 모든 synonym을 제거할 수 있는 권한 |
| CREATE PROCEDURE | 스키마에 procedure/ function을 생성할 수 있는 권한 |
| ALTER PROCEDURE | 스키마의 모든 procedure/ function을 변경할 수 있는 권한 |
| DROP PROCEDURE | 스키마의 모든 procedure/ function을 제거할 수 있는 권한 |
| EXECUTE PROCEDURE | 스키마의 모든 procedure/ function을 수행할 수 있는 권한 |
| CREATE PACKAGE | 스키마에 package를 생성할 수 있는 권한 |
| ALTER PACKAGE | 스키마의 모든 package를 변경할 수 있는 권한 |
| DROP PACKAGE | 스키마의 모든 package를 제거할 수 있는 권한 |
| EXECUTE PACKAGE | 스키마의 모든 package를 수행할 수 있는 권한 |

<a id="bfd45d6aa34bdaf8"></a>
#### &lt;table privilege&gt;

테이블 또는 view 객체에 대한 권한이다.  
[TABLE] 구문은 생략할 수 있다.

table privilege로 정의할 수 있는 table action은 다음과 같다.

- ALL [ PRIVILEGES ] ON [TABLE] table_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 TABLE에 대해 소유한 모든 권한이다.

**Table privilege**

<a id="67fef3adff18aae7"></a>
| &lt;table action&gt; | 설명 |
| --- | --- |
| CONTROL TABLE | 해당 테이블에 대한 모든 권한 |
| SELECT | 테이블의 row를 검색할 수 있는 권한 |
| INSERT | 테이블의 row를 생성할 수 있는 권한 |
| UPDATE | 테이블의 row를 갱신할 수 있는 권한 |
| DELETE | 테이블의 row를 삭제할 수 있는 권한 |
| REFERENCES | 해당 테이블을 참조하는 참조 제약 조건을 생성할 수 있는 권한 |
| LOCK | 테이블에 LOCK 구문을 수행할 수 있는 권한 |
| INDEX | 테이블에 인덱스를 생성할 수 있는 권한 |
| ALTER | 테이블을 변경할 수 있는 권한 |

SELECT, INSERT, UPDATE, REFERENCES의 경우, 테이블의 모든 column에 추가적으로 권한을 부여한다.

table privilege로 정의할 수 있는 column action은 다음과 같다. 단, column action은 base table에만 적용된다.

**Column privilege**

<a id="ea1e38cb47a28318"></a>
| &lt;column action&gt; | 설명 |
| --- | --- |
| SELECT (columns) | 해당 column들을 검색할 수 있는 권한 |
| INSERT (columns) | 해당 column들을 포함한 row를 생성할 수 있는 권한 |
| UPDATE (columns) | 해당 column들을 갱신할 수 있는 권한 |
| REFERENCES (columns) | 해당 column들을 참조하는 참조 제약 조건을 생성할 수 있는 권한 |

<a id="3e1ffe5f3018eb71"></a>
#### &lt;sequence privilege&gt;

시퀀스 객체에 대한 권한이다.

sequence privilege로 정의할 수 있는 sequence action은 다음과 같다.

- ALL [ PRIVILEGES ] ON SEQUENCE sequence_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 SEQUENCE에 대해 소유한 모든 권한이다.

**Sequence privilege**

<a id="01fd91de926a2005"></a>
| &lt;sequence action&gt; | 설명 |
| --- | --- |
| USAGE | 시퀀스를 사용할 수 있는 권한 |

<a id="902b4f31e0686a88"></a>
#### &lt;procedure privilege&gt;

Procedure/ function 객체에 대한 권한이다.

procedure privilege로 정의할 수 있는 action은 다음과 같다.

- ALL [ PRIVILEGES ] ON PROCEDURE procedure_name 
    - WITH GRANT OPTION을 사용하여 grantor (구문을 수행하는 사용자)에게 부여된 해당 procedure/ function에 대한 모든 권한이다.

**Procedure privilege**

<a id="d603d408fe08cab6"></a>
| &lt;procedure action&gt; | 설명 |
| --- | --- |
| EXECUTE | Procedure/ function을 실행할 수 있는 권한 |

<a id="630b908fc1392d39"></a>
#### &lt;package privilege&gt;

Package 객체에 대한 권한이다.

package privilege로 정의할 수 있는 action은 다음과 같다.

- ALL [ PRIVILEGES ] ON PACKAGE package_name 
    - WITH GRANT OPTION을 사용하여 grantor (구문을 수행하는 사용자)에게 부여된 해당 package에 대한 모든 권한이다.

**Package privilege**

<a id="8b632f4c407db8e3"></a>
| &lt;package action&gt; | 설명 |
| --- | --- |
| EXECUTE | Package를 실행할 수 있는 권한 |

<a id="a13e80c73549a4d5"></a>
### 설명

GRANT privilege와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

Table, sequence 등과 같은 SQL schema object를 생성한 owner는 해당 객체에 대한 권한을 별도로 부여받지 않더라도 일정한 권한을 가진다.   
이에 대한 자세한 설명은 다음과 같은 CREATE 구문을 참조한다.

- [CREATE TABLE](#060501387611d25a)
- [CREATE VIEW](#6f697c93c59acd84)
- [CREATE SEQUENCE](#971516b46cb8bf8d)
- [ALTER TABLE name ADD COLUMN](18-sql-references-a-b.md#eccd1f42db335101)
- [CREATE FUNCTION](../part-04-psm-manual/29-psm-sql-references.md#ab87224881e1ecca)
- [CREATE PROCEDURE](../part-04-psm-manual/29-psm-sql-references.md#cb8dd48d60714ba7) 
- [CREATE PACKAGE](../part-04-psm-manual/29-psm-sql-references.md#4e52d18bdace4911)

Schema, tablespace 등과 같은 non-schema object를 생성한 owner에는 해당 객체에 대한 어떤 권한도 자동으로 부여되지 않으므로 별도의 권한을 부여받아야 한다.   
자세한 설명은 다음과 같은 CREATE 구문을 참조한다.

- [CREATE SCHEMA](#b5816864e0a0ee57)
- [CREATE TABLESPACE](#c81940ba4a84752c)
- [CREATE USER](#bcf4364429be6a9b)

<a id="a33e921491ebfacc"></a>
### 사용 예

다음은 user u1에 SELECT ON TABLE t1 권한을 부여하는 예이다.

```
gSQL> GRANT SELECT ON t1 TO u1;

Grant succeeded.
```

다음은 모든 사용자를 의미하는 PUBLIC 계정에 SELECT ON TABLE t1 권한을 부여하는 예이다.

```
gSQL> GRANT SELECT ON t1 TO PUBLIC;

Grant succeeded.
```

다음은 user u1이 WITH GRANT OPTION을 사용하여 다른 user에게 해당 권한을 부여하는 예이다.

```
gSQL> GRANT SELECT ON t1 TO u1 WITH GRANT OPTION;

Grant succeeded.
```

다음은 구문을 수행하는 사용자가 WITH GRANT OPTION을 사용하여 TABLE t1 객체에 대해 소유한 모든 권한을 user u1에게 부여하는 예이다.

```
gSQL> GRANT ALL PRIVILEGES ON TABLE t1 TO u1;

Grant succeeded.
```

다음은 database에 접속할 수 있는 CREATE SESSION ON DATABASE 권한을 부여하는 예이다.

```
gSQL> GRANT CREATE SESSION ON DATABASE TO u1;

Grant succeeded.
```

다음은 SCHEMA s1에 table, view, index, sequence, constraint 객체를 생성할 수 있는 다수의 권한을 user u1에게 부여하는 예이다.

```
gSQL> GRANT CREATE TABLE, CREATE VIEW, CREATE INDEX, CREATE SEQUENCE, ADD CONSTRAINT ON SCHEMA s1 TO u1;

Grant succeeded.
```

다음은 TABLESPACE mem_data_tbs에 객체를 생성할 수 있는 권한을 user u1에게 부여하는 예이다.

```
gSQL> GRANT CREATE OBJECT ON TABLESPACE mem_data_tbs TO u1;

Grant succeeded.
```

다음은 TABLE t1의 일부 column을 조회할 수 있는 권한을 user u1에 부여하는 예이다.

```
gSQL> GRANT SELECT( id, name ) ON TABLE t1 TO u1;

Grant succeeded.
```

다음은 SEQUENCE seq1에 대해 NEXTVAL(), CURRVAL() 함수를 사용할 수 있는 권한을 user u1에 부여하는 예이다.

```
gSQL> GRANT USAGE ON SEQUENCE seq1 TO u1;

Grant succeeded.
```

<a id="678757f7d09349c1"></a>
### 호환성

SQL 표준에서는 다음 privilege들을 정의하지 않고 있다.

- &lt;database privilege&gt; 
- &lt;tablespace privilege&gt; 
- &lt;schema privilege&gt;

**SQL 표준 호환성**

<a id="e5de9babf839fb24"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| S023 | Basic structured types | X |
| S024 | Enhanced structured types | X |
| S081 | Subtables | X |
| T211 | Basic trigger capability | X |
| T281 | SELECT privilege with column granularity | O |
| T332 | Extended Roles | X |
| F731 | INSERT column privileges | O |

<a id="5a95c6f13d0d855d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [REVOKE privileges FROM](20-sql-references-h-z.md#d05351446dbd3673)
- [CREATE USER](#bcf4364429be6a9b)
- [DROP USER](#c4934ee399839206)
- [ALTER USER](18-sql-references-a-b.md#7fcf3795e062819a)

---

[← 18. SQL References (A~B)](18-sql-references-a-b.md) · [전체 목차](../README.md) · [20. SQL References (H~Z) →](20-sql-references-h-z.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
