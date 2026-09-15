<a id="1e13e512ac2b31a0"></a>

# 19. SQL References (C~G)

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/1e13e512ac2b31a0)  
> 태그: `21c.1_35_tag`

[← 18. SQL References (A~B)](18-sql-references-a-b.md) · [전체 목차](../README.md) · [20. SQL References (H~Z) →](20-sql-references-h-z.md)

<a id="b7cf28b5122d5efa"></a>
## CLOSE cursor_name

<a id="5401538f6d4dfacd"></a>
### 기능

커서를 닫는다.

<a id="92596b3b0776251b"></a>
### 구문

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="c74a94764ae95f0f"></a>
### 구문 규칙 및 파라미터

<a id="c5f90243b6e24fca"></a>
#### cursor_name

커서가 open 되어 있어야 한다.  
세션 내에서 [DECLARE cursor_name](#f41bd2e5b923c676) 구문으로 선언된 커서이어야 한다.

<a id="8239d7dfd89ee175"></a>
### 설명

Cursor는 session 내에 존재하는 객체이고 서로 다른 session의 cursor에 영향을 주지 않는다.

<a id="ce99fef5621f48a7"></a>
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

<a id="f6d815d461c9b3a4"></a>
### 호환성

**SQL 표준 호환성**

<a id="9d5dcbdef77c65bc"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic dynamic SQL | O |

<a id="337ce0642eb6f01d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#f41bd2e5b923c676)
- [OPEN cursor_name](20-sql-references-h-z.md#6047f0ea5db92a56)
- [FETCH cursor_name](#1662729a681bc4cc)

<a id="7c5772ac3aa2f438"></a>
## COMMENT ON name IS

<a id="5a32d1d9a05dc9c1"></a>
### 기능

객체에 대한 설명을 dictionary에 저장한다.

<a id="9666cbfa939a4a77"></a>
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

<a id="9095b3d4ffb6963a"></a>
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

<a id="bd73c9153cfd69a6"></a>
### 구문 규칙 및 파라미터

<a id="65fe382b9d4dfdb7"></a>
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

Schema object의 경우 schema_name을 기술하지 않으면 구문을 수행하는 사용자의 [Schema Path](13-sql-objects.md#09c78ad335415e57)에 의해 스키마 이름이 결정된다.

```
COMMENT ON TABLE test_table IS 'test comment'; 
→ COMMENT ON TABLE user_default_schema.test_table IS 'test comment';
```

<a id="92d310fb1df3cfe8"></a>
#### 'comment string'

저장할 comment 문장을 기술한다.   
Comment를 삭제하려면 다음과 같이 empty string ('')을 사용한다.

```
COMMENT ON TABLE test_table IS '';
```

comment string의 길이는 1024 bytes를 초과할 수 없다.

<a id="ff33169a30dd035b"></a>
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

각 view에 대한 자세한 내용은 [DICTIONARY_SCHEMA](../part-02-administration-manual/9-database-information.md#609d4fb26acaef21)를 참조한다.

<a id="0893c10f5e093a03"></a>
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

<a id="8cb495705cdf36d4"></a>
### 호환성

SQL 표준에는 &lt;comment statement&gt;가 없다.

<a id="4ba013db6a784eae"></a>
## COMMIT

<a id="c5299aed593db97a"></a>
### 기능

현재 트랜잭션을 종료하고, 변경된 모든 내용을 영속화한다.

<a id="083bbcf2b7e4485d"></a>
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

<a id="d1ac2729d39bdfd3"></a>
### 구문 규칙 및 파라미터

<a id="69ff6797c86f9a8f"></a>
#### WORK

동작에 영향을 미치지 않는 예약어이다.

<a id="274e111d32b2738c"></a>
#### &lt;commit comment clause&gt;

- COMMENT 'comment_string'
    - 트랜잭션을 commit 할 때 트랜잭션에 주석을 지정한다.

<a id="ce8fefea4dc0e126"></a>
#### &lt;commit write clause&gt;

Commit 연산으로 생성된 redo log가 redo log file에 기록될 때까지 기다릴지 여부를 결정한다.

- WAIT
    - commit 연산에 의해서 생성된 redo log가 redo log file에 기록될 때까지 기다린 후 연산을 종료한다.
- NOWAIT
    - commit 연산에 의해서 생성된 redo log가 redo log 버퍼에 기록되면 연산을 종료한다.
- 지정되어 있지 않을 경우, 프로퍼티를 따른다.

<a id="d2939acb0ac75233"></a>
#### &lt;commit force clause&gt;

분산 트랜잭션을 수동으로 commit 할 때 사용한다.

- FORCE 'xid_string'
    - 'xid_string'에 해당하는 분산 트랜잭션을 commit 한다.
    - 'xid_string'은 '*format_id*.*transaction_id*.*branch_id*'로 구성된다.

<a id="b8ef788c9b3df536"></a>
### 설명

COMMIT 구문은 트랜잭션 내에서 수행된 다음 구문들을 완료한다.

- Data Manipulation Language (DML) 구문
    - 데이터를 변경하는 INSERT, UPDATE, DELETE 등의 구문
- Data Definition Language (DDL) 구문 
    - 객체의 구조 및 정의를 변경하는 CREATE, DROP, ALTER, TRUNCATE, GRANT, REVOKE 등의 구문

예외적으로, DDL 중에 OS 자원을 다루거나 DATA TYPE을 변경하는 다음 구문들은 자동으로 COMMIT 된다.

- [CREATE TABLESPACE](#9425404264bb2534)
- [DROP TABLESPACE](#0ccb2cbcfd412a42)
- [ALTER TABLESPACE](18-sql-references-a-b.md#7c3ae65b4798a999)
- ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE: [&lt;alter column data type clause&gt;](18-sql-references-a-b.md#e929e7d1df23593f)

COMMIT을 수행하면 WITHOUT HOLD 옵션으로 열린 커서는 자동으로 닫힌다. 커서에 대한 자세한 내용은 다음의 커서 관련 구문을 참조한다.

- [DECLARE cursor_name](#f41bd2e5b923c676)
- [OPEN cursor_name](20-sql-references-h-z.md#6047f0ea5db92a56)

트랜잭션이 지연된 (DEFERRED) 제약 조건을 위반하면 COMMIT 구문의 수행은 실패하고 트랜잭션은 ROLLBACK 된다. 지연된 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](20-sql-references-h-z.md#2e96c033f710d10f) 구문의 설명을 참조한다.

<a id="582dc5b05400f848"></a>
### 사용 예

다음은 INSERT 구문을 수행한 후에 COMMIT을 수행하는 예이다.

```
gSQL> INSERT INTO t1 VALUES ( 1, 'anonymous' );

1 row created.

gSQL> COMMIT WORK COMMENT 'INSERT T1';

Commit complete.
```

<a id="9248e382fa275cc9"></a>
### 호환성

**SQL 표준 호환성**

<a id="13309bd3d56ce720"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T261 | Chained transactions | X |

<a id="ae6ac4e0371a97a8"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ROLLBACK](20-sql-references-h-z.md#380bfae0e9193b31)
- [SAVEPOINT savepoint_specifier](20-sql-references-h-z.md#e0fec21d41f8ac77)

<a id="72600ff3c559dfb5"></a>
## CREATE AUDIT POLICY

<a id="152d17736b3c8708"></a>
### 기능

Audit policy 객체를 생성한다.   
생성한 audit policy 객체를 활성화하려면 AUDIT POLICY 구문을 수행하여야 한다.

<a id="96d0bdf4ef39670e"></a>
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

<a id="d5a1259910dbe606"></a>
### 사용 범위 및 접근 권한

&lt;audit policy definition&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="c1155dd9cbd54f32"></a>
### 구문 규칙 및 파라미터

<a id="931f904019cb6f3f"></a>
#### policy_name

생성할 audit policy의 이름이다.

<a id="d3db92c5e1c5111f"></a>
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

<a id="64c756bf31b1dc93"></a>
#### &lt;action_audit_clause&gt;

특정 객체에 대한 action과 database 전체에 대한 action을 감사한다.

<a id="e8486e5998d2c627"></a>
#### &lt;object_action_audit&gt;

<a id="604a6bdf78e73d5c"></a>
##### ALL ON object_name

object_name에 해당하는 객체에 대해 나열할 수 있는 모든 action을 의미한다.

각 객체 유형별로 감사할 수 있는 audit action은 다음 표와 같다.

**객체별 audit action**

<a id="0a906760fc3f57ad"></a>
| Object type | Action |
| --- | --- |
| Table | ALTER, COMMENT, DELETE, GRANT, INDEX, INSERT, LOCK, RENAME, SELECT, UPDATE |
| View | ALTER, COMMENT, GRANT, SELECT |
| Sequence | ALTER, COMMENT, GRANT, SELECT |
| Stored function/  procedure | ALTER, COMMENT, EXECUTE, GRANT |

<a id="aa32787718630991"></a>
##### &lt;object_action&gt; ON object_name

특정 object에 대한 개별 action들은 다음과 같이 ON 절을 명시하여 하나씩 나열한다.

```
CREATE AUDIT POLICY p1
       ACTIONS INSERT ON u1.t1
             , DELETE ON u1.t1
             , UPDATE ON u1.t1
;
```

<a id="6f85ed6bed22189b"></a>
##### EXECUTE action 유의 사항

Stored function이나 stored procedure의 EXECUTE action 성공, 실패 여부에 대한 감사는 실제 수행 시점의 수행 가능 여부만으로 판단한다.

- WHENEVER NOT SUCCESSFUL의 경우, stored function/ procedure를 수행할 수 없을 경우에 감사 레코드를 생성한다.
- WHENEVER SUCCESSFUL의 경우, stored function/ procedure 내부의 SQL 구문을 수행하는 중에 에러가 발생하더라도 감사 레코드를 생성한다.
- Stored function/ procedure 내부의 SQL 구문 실패에 대한 감사가 필요할 경우, 해당 SQL 구문을 감사 대상에 포함해야 한다.

<a id="9ababee2535a2b93"></a>
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

<a id="ac5caaeead5a06a0"></a>
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

<a id="a545de0a6c1c7a99"></a>
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

<a id="11f46a2e48142eef"></a>
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

<a id="56cae69797dee723"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="fa53705252d5eca4"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#72600ff3c559dfb5)
    - [DROP AUDIT POLICY](#1aaa5b1766ff2d59)
    - [ALTER AUDIT POLICY](18-sql-references-a-b.md#00bbcaab72bbb158)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](18-sql-references-a-b.md#213cd4dbcc8bc668)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#15b6d2d5678734fb)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#18a54cc95a024f6e)

- Audit trail 소거: [ALTER DATABASE CLEAR AUDIT TRAIL](18-sql-references-a-b.md#7098d8b3ccdebf40)

<a id="8e2b3a3076fcfb3e"></a>
## CREATE CLUSTER GROUP

<a id="3ec1df46ed44567f"></a>
### 기능

Cluster system에 참여할 cluster group을 생성한다.

<a id="acc49c8f8df825e8"></a>
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

<a id="7451cc4c906d3017"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;cluster group definition&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="f34487d2b5a879b2"></a>
### 구문 규칙 및 파라미터

<a id="e5d28a11de5dc5b3"></a>
#### group_name

Cluster group의 이름이다.   
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="e0cdd6b28321a921"></a>
#### &lt;cluster member definition&gt;

Cluster group에 포함될 cluster member를 정의한다.  
Cluster group은 cluster member를 최대 32 개까지 포함할 수 있다.  
Cluster system에 최초로 생성하는 cluster group에는 cluster member를 한 개만 정의할 수 있고 자기 자신을 cluster member로 포함해야 한다.

<a id="15ef81013019347e"></a>
#### member_name

Cluster member의 이름이다.   
Cluster member 이름은 해당 member의 database를 생성할 때 정의한 member 이름과 동일해야 한다.  
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

Cluster member의 start-up 단계는 GLOBAL OPEN 단계여야 한다.

<a id="37f5d53568c68866"></a>
#### &lt;connection attribute&gt;

Cluster member간 통신을 위한 연결 정보를 정의한다.   
&lt;connection attribute&gt;는 해당 member의 database를 생성할 때 정의한 HOST, PORT와 동일해야 한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST address는 ip v4 형식으로 사용한다. 
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="905e5eb8c59e1573"></a>
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

<a id="6947f8f56cf9938b"></a>
### 설명

&lt;cluster group definition&gt; 구문은 table들의 shard를 재배치하지 않는다.

추가된 cluster group에 shard를 재배치하려면 다음 구문을 수행해야 한다.

- [ALTER DATABASE REBALANCE](18-sql-references-a-b.md#be8f993bb3ff62bc)
- [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#1af19281915840f1)

<a id="85cfc5c6e48ed436"></a>
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

<a id="f8cf234ae9149cc2"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="fa76a9d7b24c4d7f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP CLUSTER GROUP](#8bcf309cea211dc8)
- [ALTER CLUSTER GROUP name ADD MEMBER](18-sql-references-a-b.md#2aa692a04102ad1a)

<a id="677b16ec3653271c"></a>
## CREATE CLUSTER LOCATION

<a id="c76f8641a45eda34"></a>
### 기능

Cluster member의 접속 정보를 생성한다.

<a id="4a74a9d0b5e4b68c"></a>
### 구문

```
<cluster location definition> ::=
    CREATE CLUSTER LOCATION member_name 
    <cluster connection attribute>
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="e1dfbd23b94152d8"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;cluster location definition&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="8e2928cd2303964a"></a>
### 구문 규칙 및 파라미터

<a id="d9f3d82ba39ba5fb"></a>
#### member_name

Cluster member의 이름이다.   
등록된 cluster location 정보에 동일한 cluster member 이름이 존재하지 않아야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="892136588a333100"></a>
#### &lt;cluster connection attribute&gt;

Cluster member간 통신을 위한 연결 정보를 정의한다.   
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 ip v4 형식으로 사용한다. 
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="c214a102f1d89a12"></a>
### 설명

기본적으로 cluster location 정보는 cluster group을 생성하거나 cluster member를 추가할 때 제공되는 접속 정보를 이용하여 자동으로 생성된다. 생성된 정보는 cluster member와 group을 삭제할 때 함께 삭제된다.

만약 cluster location의 접속 정보가 변경되면 cluster member를 삭제하거나 다시 생성할 필요없이 [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#ba7b493d6f702d6f)을 이용하여 접속 정보를 변경할 수 있다.

<a id="8b948eaa0f0c0a79"></a>
### 사용 예

```
gSQL> 
CREATE CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120,
;

Created
```

<a id="6a6747f00e3b7067"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="2eec7afad21b55c7"></a>
### 참조

관련 내용은 [DROP CLUSTER LOCATION](#28783969fbe8714a)을 참조한다.

<a id="2cadf771c7ba93ae"></a>
## CREATE DISK DATA TABLESPACE

<a id="adcd7e2e865a477e"></a>
### 기능

디스크 데이터 테이블스페이스를 정의한다.

<a id="174b519356fdc38b"></a>
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

<a id="2fa3d5cbfef61d90"></a>
### 사용 범위 및 접근 권한

&lt;disk data tablespace definition&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="0e054e1a72815ac4"></a>
### 구문 규칙 및 파라미터

<a id="8e0a6d082f581a46"></a>
#### tablespace_name

생성할 테이블스페이스의 이름이다.  
테이블스페이스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="8bdbcf8e71fac150"></a>
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

<a id="ba5308a8467473b2"></a>
#### &lt;autoextend clause&gt;

자동 확장 속성을 ON 또는 OFF로 설정한다. ON으로 설정할 경우 자동 확장 크기와 데이터파일의 최대 크기를 지정할 수 있다.

<a id="070b32ae0a5c3b4d"></a>
#### &lt;next size clause&gt;

현재 사용 중인 데이터 파일에 더 이상 사용할 공간이 없을 때 확장할 크기를 지정한다.

<a id="c08410a3841c1c38"></a>
#### &lt;max size clause&gt;

데이터 파일이 확장될 수 있는 최대 크기를 지정한다.

<a id="f205b9db1daabfb0"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (명시하지 않을 경우 bytes 단위이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="0a28076c68c19393"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="aec79ec8bb7c7f31"></a>
#### ONLINE | OFFLINE

테이블스페이스 ONLINE/ OFFLINE 여부를 설정한다.

- ONLINE은 테이블스페이스를 생성하는 즉시 사용할 수 있는 상태이다. 
- OFFLINE은 사용 불가능한 상태이므로 ONLINE 상태로 변경한 후에 사용할 수 있다.

<a id="e589eb6cf883e1a9"></a>
#### EXTSIZE &lt;size clause&gt;

테이블스페이스의 extent 크기를 지정한다.

- Extent 크기는 바이트 단위로 기술하며, 다섯 가지 (64 K, 128 K, 256 K, 512 K, 1 M) 중 하나가 선택된다.
- 만약 extent 크기가 64 K ~ 128 K 사이의 값으로 지정되면 128 K로 설정되고, 1 M 이상으로 지정되면 1 M로 설정된다.

<a id="98bbdb3f8a26501b"></a>
### 설명

Data tablespace는 table, index (LOGGING) 등의 SQL schema 객체를 저장할 물리적 공간을 제공하는 객체이다.

<a id="3d86b41f1d1edf0a"></a>
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

<a id="f08ca799cedb7f3d"></a>
### 호환성

SQL 표준에서는 테이블스페이스에 대한 개념을 다루지 않고 있다.

<a id="2ab2a37acbfb7995"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#0ccb2cbcfd412a42)
- [ALTER TABLESPACE](18-sql-references-a-b.md#7c3ae65b4798a999)
- [ALTER DATABASE DATAFILE AUTOEXTEND](18-sql-references-a-b.md#6c1dc4fd490b9850)

<a id="48c45f88dede7653"></a>
## CREATE GLOBAL TEMPORARY TABLE

<a id="4cee413ef884f180"></a>
### 기능

새로운 global temporary table을 생성한다.

<a id="8214635731688e56"></a>
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

> &lt;table element&gt;의 정의는 &lt;table_definition&gt;의 정의와 동일하다. 자세한 내용은 [CREATE TABLE](#66fde705300657e5) 을 참조한다.

<a id="65e97cd06d00c55a"></a>
### 사용 범위 및 접근 권한

&lt;global temporary table definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블 생성 권한
    - [CREATE TABLE](#66fde705300657e5) 구문의 접근 권한을 참조한다.
- SELECT 접근 권한 
    - [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5) 구문의 접근의 권한을 참조한다.

<a id="4a363bbe28a8268f"></a>
### 구문 규칙 및 파라미터

<a id="359b3b92a8be98d8"></a>
#### table_name

생성할 테이블의 이름이다.  
자세한 내용은 [table_name](#b6ba1413e43e572e) 구문을 참조한다.

<a id="0e55c520bc8c1fe0"></a>
#### other syntax

이 외의 구문 규칙은 [CREATE TABLE](#66fde705300657e5) 및 [CREATE TABLE AS SELECT](#a8bce0d0a242157d) 구문의 syntax를 참조한다.

<a id="d0e7e39dfceb2170"></a>
### 설명

GLOBAL TEMPORARY TABLE은 한 트랜잭션이나 세션이 실행되는 동안 유지될 데이터를 보관하는 용도로 사용하는 임시 테이블이다.  
개발자가 응용 프로그램을 개발할 때 연산 중간 데이터를 잠시 저장하는 변수와 같은 용도로 사용된다.

Global temporary table의 특징은 다음과 같다.

- Global temporary table의 정의는 모든 세션에서 볼 수 있다.
- Global temporary table을 정의할 때는 물리적 공간이 할당되지 않고, 처음으로 insert 할 때 해당 세션에 종속된 실제 공간 (segment)이 할당된다.
- Global temporary table의 데이터는 insert 한 세션이나 트랜잭션에서만 볼 수 있다.
- Global temporary table의 데이터가 저장되는 tablespace는 다음과 같이 결정된다.

<a id="8955257ec485ea48"></a>
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

<a id="92cc50499fb80ecb"></a>
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

<a id="6657c60c20f32c45"></a>
| TEMP_UNDO_ENABLED 값 | 설명 |
| --- | --- |
| TRUE | Database system의 default temporary tablespace에 undo log가 기록된다. |
| FALSE | Database system의 undo tablespace에 undo log가 기록된다. |

- Global temporary table에 대한 TRUNCATE 명령은 해당 세션의 segment만 truncate 한다.
- 세션이 종료되면 모든 segment들이 TRUNCATE 된 후에 반환된다.

<a id="1849e27d4e7090af"></a>
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

<a id="945c2bbc803ad6b9"></a>
### 호환성

CREATE GLOBAL TEMPORARY TABLE 및 CREATE GLOBAL TEMPORARY TABLE AS SELECT 구문은 SQL 표준의 &lt;table definition&gt; 정의를 따른다. 단, 다음은 표준에서 확장된 것이다.

- 표준에서 SELECT 절 밖의 괄호는 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- 표준에서 WITH [NO] DATA 절은 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- GOLDILOCKS의 tablespace 개념은 표준에 없는 확장 개념이다.

**SQL 표준 호환성**

<a id="4dfddf6150b551a3"></a>
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

<a id="851a2e4cbe74a37a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](#66fde705300657e5)
- [CREATE TABLE AS SELECT](#a8bce0d0a242157d)

<a id="3d8fd81a2aaba60c"></a>
## CREATE IMMUTABLE TABLE

<a id="10f5da9c6d4b9c81"></a>
### 기능

새로운 immutable table을 생성한다.

<a id="780179ed237a7992"></a>
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

> &lt;table element&gt;, &lt;table sharding strategy&gt;, &lt;table attribute clause&gt;, &lt;table global secondary index clause&gt;의 정의는 &lt;table_definition&gt;의 정의와 동일하다. 자세한 내용은 [CREATE TABLE](#66fde705300657e5)을 참조한다.

<a id="af8eb0cfa7cc172a"></a>
### 사용 범위 및 접근 권한

&lt;immutable table definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블 생성 권한
    - [CREATE TABLE](#66fde705300657e5) 구문의 접근 권한을 참조한다.
- SELECT 접근 권한 
    - [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5) 구문의 접근 권한을 참조한다.

<a id="92459e182de559c6"></a>
### 구문 규칙 및 파라미터

<a id="177fea9358c500a7"></a>
#### table_name

생성할 테이블의 이름이며, 스키마 내에서 고유한 이름이어야 한다.  
schema_name.table_name과 같이 테이블이 소속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
테이블 이름의 길이는 128 바이트보다 작아야 한다.

<a id="af3822920e3b0e9d"></a>
#### 기타 구문 규칙

이 외의 구문 규칙은 [CREATE TABLE](#66fde705300657e5)과 [CREATE TABLE AS SELECT](#a8bce0d0a242157d) 구문의 syntax를 참조한다.

<a id="cbb75727c6a21e15"></a>
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

<a id="f487ea02f565d661"></a>
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

<a id="13ac14bc26977832"></a>
### 호환성

SQL 표준에서는 CREATE IMMUTABLE TABLE 구문과 CREATE IMMUTABLE TABLE AS SELECT 구문을 다루지 않고 있다.

<a id="ee01e2dcc4a8e56e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](#66fde705300657e5)
- [CREATE TABLE AS SELECT](#a8bce0d0a242157d)

<a id="8e0637af857026b6"></a>
## CREATE INDEX

<a id="098a5acaad6ecc0f"></a>
### 기능

인덱스를 생성한다.

<a id="13add1fa081030cb"></a>
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

<a id="251dde8f069ba56e"></a>
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

<a id="6978ed4dd6665b94"></a>
### 구문 규칙 및 파라미터

<a id="95ff5723e48a4c96"></a>
#### UNIQUE

인덱스를 구성하는 column들에 중복 값을 허용하지 않는다.

<a id="b49fa85aa151ef6a"></a>
#### index_name

생성할 인덱스의 이름이며, 스키마 내에서 유일해야 한다.  
스키마 이름을 생략할 경우, 참조하는 테이블이 속한 스키마에 인덱스가 생성된다.  
인덱스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="ac6b363a13ef1422"></a>
#### table_name

인덱스를 생성할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="34f5eef24ca84790"></a>
#### column_name

인덱스 key로 사용할 column의 이름이다.  
하나 이상의 column을 정의해야 하는데 최대 32 개의 column을 인덱스 key로 사용할 수 있다.

구현 내용에 따라 다음과 같은 제약이 발생할 수 있다.

- 인덱스에 포함되는 column의 데이터 타입이 LONG CHARACTER VARYING, LONG BINARY VARYING 일 경우 인덱스를 생성할 수 없다. 
- Column들의 precision 합계가 1200 바이트보다 작은 경우에만 인덱스를 생성할 수 있다.

<a id="bb8576f0e665ea52"></a>
#### ASC | DESC

Column의 정렬 순서를 명시한다.

- ASC: 오름차순으로 정렬한다. 
- DESC: 내림차순으로 정렬한다. 
- 명시하지 않을 경우, 기본값은 ASC 이다.

<a id="eacd9c093e672869"></a>
#### NULLS FIRST | NULLS LAST

NULL 값의 정렬 순서를 명시한다.

- NULLS FIRST: NULL이 아닌 값들보다 앞에 위치한다. 
- NULLS LAST: NULL이 아닌 값들보다 뒤에 위치한다. 
- 명시하지 않을 경우, 기본값은 NULLS LAST 이다.

<a id="debddc2e0e1356f2"></a>
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
        - 인덱스에 접근하는 사용자의 수가 적을 경우에는 INITRANS를 낮게 설정하고, 동시 접근하는 사용자가 많을 경우에는 INITRANS를 높게 설정한다. 
        - 필요한 경우 설정된 MAXTRANS까지 자동으로 늘어난다. 
    - 1 부터 32 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기본값은 4 이다.

- MAXTRANS integer 
    - 정의 
        - 페이지에 동시 접근할 수 있는 트랜잭션의 최대 개수이다. 
    - 1 부터 32 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기본값은 8 이다.

<a id="a83aae6aed74af0d"></a>
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
    - 생략할 경우, 기본값은 EXTENT 크기 * 2147483647 (INT32의 최대 양의 정수)이다.

<a id="1a2d0059998a509d"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="47bacc5de73ab8dd"></a>
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

<a id="69120d9206e88c6a"></a>
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

<a id="33b6d381968a2509"></a>
### 설명

LOGGING 인덱스와 NOLOGGING 인덱스에는 다음과 같은 trade-off가 있다.

- LOGGING 인덱스
    - 장점: 시스템을 구동할 때 로그를 이용해 인덱스가 자동으로 복구되므로 별도의 구축과정이 없다.
    - 단점: 관련 row를 변경할 때 인덱스 변경 내용을 로그로 기록하여 디스크 IO를 유발한다.
- NOLOGGING 인덱스
    - 장점: 관련 row를 변경할 때 인덱스 변경 내용에 대한 디스크 IO가 발생하지 않는다.
    - 단점: 시스템을 구동할 때 인덱스에 대한 로그 정보가 없어 자동으로 인덱스를 재구축한다.

<a id="86f1960bb6684144"></a>
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

<a id="b85b4e86c09aef01"></a>
### 호환성

SQL 표준에서는 인덱스에 대한 개념을 다루지 않고 있다.

<a id="a2213de1aa4dbd38"></a>
### 참조

관련 내용은 [DROP INDEX](#f6216a28e7e3e011)를 참조한다.

<a id="86993cea38f6279a"></a>
## CREATE MEMORY DATA TABLESPACE

<a id="11c0ea9022280120"></a>
### 기능

메모리 데이터의 테이블스페이스를 정의한다.

<a id="5d3d8040159a1767"></a>
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

<a id="6d3881379501dfca"></a>
### 사용 범위 및 접근 권한

&lt;memory data tablespace definition&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="a992d40664a13952"></a>
### 구문 규칙 및 파라미터

<a id="721599ecdfad6e59"></a>
#### [ MEMORY ] [ DATA ]

테이블, 인덱스 등 영구적인 객체를 저장할 메모리 테이블스페이스이다.  
MEMORY와 DATA 예약어는 생략할 수 있다.

<a id="2a35ff68c5981771"></a>
#### tablespace_name

생성할 테이블스페이스의 이름이다.  
테이블스페이스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="8cbbb6093a3bd7a9"></a>
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

<a id="ad055e3c50bdca99"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="b4aa53b9fe063a74"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="62856a48ba38555a"></a>
#### ONLINE | OFFLINE

테이블스페이스 ONLINE/ OFFLINE 여부를 설정한다.

- ONLINE은 테이블스페이스를 생성하는 즉시 사용할 수 있는 상태이다. 
- OFFLINE은 사용 불가능한 상태이므로 ONLINE 상태로 변경한 후에 사용할 수 있다.

<a id="b489842042abc1f1"></a>
#### EXTSIZE &lt;size clause&gt;

테이블스페이스의 extent 크기를 지정한다.

- Extent 크기는 바이트 단위로 기술하며, 다섯 가지 (64 K, 128 K, 256 K, 512 K, 1 M) 중 하나가 선택된다.
- 만약 extent 크기가 64 K ~ 128 K 사이의 값으로 지정되면 128 K로 설정되고, 1 M 이상으로 지정되면 1 M로 설정된다.

<a id="1d35268b4786aa1c"></a>
### 설명

Data tablespace는 table, index (LOGGING) 등의 SQL schema 객체를 저장할 물리적 공간을 제공하는 객체이다.

<a id="48dfa0d0cf35c41e"></a>
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

<a id="e2575fb6cb3b2883"></a>
### 호환성

SQL 표준은 테이블스페이스에 대한 개념을 다루지 않고 있다.

<a id="306c220b365686c9"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#0ccb2cbcfd412a42)
- [ALTER TABLESPACE](18-sql-references-a-b.md#7c3ae65b4798a999)

<a id="54c1cb4e7c65e722"></a>
## CREATE MEMORY TEMPORARY TABLESPACE

<a id="a1a30fe4721af7c5"></a>
### 기능

메모리 임시 테이블스페이스를 정의한다.

<a id="3f7d3be688e2d7dc"></a>
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

<a id="dc850e9233e28d15"></a>
### 사용 범위 및 접근 권한

&lt;memory temporary tablespace definition&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="f4907148ce0bfa28"></a>
### 구문 규칙 및 파라미터

<a id="71b643f8dce8821b"></a>
#### [ MEMORY ] TEMPORARY

질의 처리 과정에서 생성되는 중간 결과 등의 임시 객체나 no logging 인덱스를 저장할 메모리 임시 테이블스페이스이다.  
MEMORY 예약어는 생략할 수 있다.

<a id="240195cf4f5de3ce"></a>
#### tablespace_name

생성할 테이블스페이스의 이름이다.  
테이블스페이스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="1c1d3262027fc36b"></a>
#### &lt;memory clause&gt;

- 'memory_name' 
    - 임시 데이터를 저장할 메모리 이름이다. 
    - memory_name은 해당 테이블스페이스 내에서 유일해야 한다. 
    - memory_name의 길이는 1024 바이트보다 작아야 한다. 
- SIZE &lt;size clause&gt; 
    - 초기 크기를 지정한다. 
    - 최소 1 M ~ 최대 30 G 까지 지정할 수 있다.

<a id="957f88c14c10c53e"></a>
#### &lt;size clause&gt;

공유 메모리 공간의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)  
임시 메모리 데이터의 경우 이미지를 파일로 관리하지 않는다.

- K: Kilobytes
- M: Megabytes
- G: Gigabytes
- T: Terabytes

<a id="54feb0bfed706f7f"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="7db4b8658ad72b7a"></a>
#### EXTSIZE &lt;size clause&gt;

테이블스페이스의 extent 크기를 지정한다.

- Extent 크기는 바이트 단위로 기술하며, 다섯 가지 (64 K, 128 K, 256 K, 512 K, 1 M) 중 하나가 선택된다. 
- 만약 extent 크기가 64 K ~ 128 K 사이의 값으로 지정되면 128 K로 설정되고, 1 M 이상으로 지정되면 1 M로 설정된다.

<a id="b0a433fc69bc1ba0"></a>
### 설명

Temporary tablespace는 index (NOLOGGING) 등의 SQL schema 객체와, 질의를 처리할 때 sorting/ hashing 하기 위한 중간 결과를 저장하는 물리적 공간을 제공하는 객체이다.

<a id="3dda9b89ff5dc2eb"></a>
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

<a id="e7b7016164c493c2"></a>
### 호환성

SQL 표준은 테이블스페이스에 대한 개념을 다루지 않고 있다.

<a id="514e6fe0e61be74e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#0ccb2cbcfd412a42)
- [ALTER TABLESPACE](18-sql-references-a-b.md#7c3ae65b4798a999)

<a id="f421f468f014cc7b"></a>
## CREATE PROFILE

<a id="db2f280ea082ec2c"></a>
### 기능

Profile을 생성하는 구문으로써 password 관리 방법을 설정할 수 있다.   
User에게 profile을 할당하면 profile에 정의된 방법으로 user의 password를 관리한다.

<a id="9125a4070a339ee8"></a>
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

<a id="940ffbf042fea807"></a>
### 사용 범위 및 접근 권한

&lt;profile definition&gt; 구문을 수행하려면 사용자에게 CREATE PROFILE ON DATABASE 권한이 있어야 한다.

<a id="ce8eb0567e610da4"></a>
### 구문 규칙 및 파라미터

<a id="9b1b3a1c626126ce"></a>
#### profile_name

생성할 profile의 이름을 명시한다.

<a id="40db350c0380c0ad"></a>
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

<a id="5a792e290943b818"></a>
#### FAILED_LOGIN_ATTEMPTS

연속적인 로그인 실패 가능 횟수를 설정한다.   
명시된 횟수를 넘어서면 계정이 잠긴다.

- FAILED_LOGIN_ATTEMPTS integer
    - 값의 범위는 0보다 큰 양의 정수여야 한다. 
- FAILED_LOGIN_ATTEMPTS UNLIMITED
    - 로그인 실패로 인해 계정이 잠기지 않는다.
- FAILED_LOGIN_ATTEMPTS DEFAULT
    - "DEFAULT" profile의 정책을 따른다.

<a id="701de834caca4c1c"></a>
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

<a id="6617d50ee3a8b538"></a>
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

<a id="b96aca593cfa668f"></a>
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

<a id="85165051864c9c05"></a>
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

<a id="4e2ca216481cbc0f"></a>
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

<a id="1dbeb8915781b608"></a>
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

<a id="dc182289916fc3c1"></a>
##### KISA_VERIFY_FUNCTION

Korea Internet & Security Agency (KISA)의 비밀번호 검증 방법이다.

- 8 글자 이상
- 1 개 이상의 문자
- 1 개 이상의 숫자
- 1 개 이상의 특수 문자

<a id="2dcaeb5aafe0a4cd"></a>
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

<a id="d4f64c14e2b50a3e"></a>
##### ORA12C_STRONG_VERIFY_FUNCTION

Oracle의 ORA12C_STRONG_VERIFY_FUNCTION 비밀번호 검증 방법이다.

- 9 글자 이상
- 2 개 이상의 대문자 
- 2 개 이상의 소문자 
- 2 개 이상의 숫자 
- 2 개 이상의 특수 문자 
- 이전 비밀번호와 적어도 4 글자는 달라야 한다.

<a id="6a6c82134c0f5ac3"></a>
##### VERIFY_FUNCTION_11G

Oracle의 VERIFY_FUNCTION_11G 비밀번호 검증 방법이다.

- 8 글자 이상
- 1 개 이상의 문자 
- 1 개 이상의 숫자 
- 사용자 이름을 포함하면 안된다. 
- 이전 비밀번호와 적어도 3 글자는 달라야 한다.

<a id="0beaeda6c98fc138"></a>
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

<a id="e87689f2064fcbb0"></a>
### 설명

<a id="f9121c886ff23525"></a>
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

<a id="12600e4272ff255c"></a>
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

<a id="77cae420e38a2003"></a>
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

<a id="c1d1e4347db314df"></a>
#### 비밀번호 재사용 가능 여부

비밀번호 재사용 가능 여부에 영향을 주는 parameter는 다음과 같다.

- PASSWORD_REUSE_MAX
- PASSWORD_REUSE_TIME

두 parameter의 비밀번호 재사용 가능 여부는 다음 표와 같다.

**비밀번호 재사용 가능 조건**

<a id="4f3ae6174fda9a20"></a>
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

<a id="6a91c8f78fefba27"></a>
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

<a id="11db9883bf2bafeb"></a>
#### DEFAULT profile

Database를 생성할 때 다음과 같은 "DEFAULT" profile을 자동으로 생성한다. 생성하는 "DEFAULT" profile 의 password parameter 정보는 다음과 같다.

**DEFAULT profile의 구성**

<a id="468dbedd11ae2be3"></a>
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

<a id="3e8cd31722932094"></a>
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

<a id="34f45a6ee9be8d09"></a>
### 호환성

SQL 표준은 profile에 대한 개념을 다루지 않고 있다.

<a id="2c8b2a828e82c068"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP PROFILE](#4a92f0bfc9e51c58)
- [ALTER PROFILE](18-sql-references-a-b.md#e94dd9982f8bc8d7)
- [CREATE USER](#f516f713c62659c7)
- [ALTER USER](18-sql-references-a-b.md#648c7792f8549c18)
- [ALTER DATABASE CLEAR PASSWORD HISTORY](18-sql-references-a-b.md#d574b13dcc907e21)

<a id="e1a750bc16ba12f6"></a>
## CREATE SCHEMA

<a id="fee8781e5ba3f7e9"></a>
### 기능

스키마를 정의한다.

<a id="fc370afa817ff222"></a>
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

<a id="c1b6fff6a61aad62"></a>
### 사용 범위 및 접근 권한

&lt;schema definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 스키마를 생성하려면 CREATE SCHEMA ON DATABASE 권한이 있어야 한다.

- &lt;schema element&gt;가 존재할 경우, 각 &lt;schema element&gt; 구문을 수행하기 위한 권한이 있어야 한다.  
  자세한 내용은 다음 각 구문의 *사용 범위 및 접근 권한*을 참조한다.
    - [CREATE TABLE](#66fde705300657e5) 
    - [CREATE VIEW](#c6a48c56234057a1) 
    - [CREATE INDEX](#8e0637af857026b6)
    - [CREATE SEQUENCE](#0466abe24a740737)
    - [GRANT privileges TO](#71c467631eb14f4c)
    - [COMMENT ON name IS](#7c5772ac3aa2f438)

- user_identifier에 해당하는 사용자는 생성한 스키마에 대해 다음과 같은 권한을 갖는다.
    - 생성한 schema_name 스키마의 소유자 
    - &lt;schema element&gt; 절로 생성된 객체의 소유자

- 생성한 스키마에 별도의 권한을 부여하지 않으므로 객체를 생성하려면 적절한 스키마 권한을 부여받아야 한다.  
  스키마 권한의 종류에 대한 내용은 GRANT privileges TO 구문의 [&lt;schema privilege&gt;](#44834e7fe60ac953)를 참조한다.  
  사용 예는 CREATE USER 구문의 [사용 예](#8499538b1d421f77)를 참조한다.

<a id="cde3eb5914483a2d"></a>
### 구문 규칙 및 파라미터

<a id="7e43e0d4df2a955e"></a>
#### schema_name

생성할 스키마의 이름이다.  
Database 내에 동일한 스키마 이름이 존재하지 않아야 한다.  
스키마 이름의 길이는 128 바이트보다 작아야 한다.

<a id="c4e741aedb5f2f69"></a>
#### AUTHORIZATION user_identifier

스키마 이름을 생략할 경우, user_identifier와 동일한 이름의 스키마를 생성한다.   
AUTHORIZATION을 지정하지 않을 경우, 구문을 수행한 사용자의 user_identifier가 사용된다.

<a id="fd957ef721e0aed5"></a>
#### schema_name AUTHORIZATION user_identifier

생성할 스키마 이름과 스키마의 소유자를 지정한다.   
소유자는 role이나 PUBLIC이 될 수 없다.

<a id="9bc4202c6e1b5029"></a>
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

<a id="8657b47df970d4db"></a>
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

<a id="b35b4ae4eb9b9ed1"></a>
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

<a id="d8171051a2e6aa46"></a>
### 호환성

**SQL 표준 호환성**

<a id="eecaf9c236421cb9"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| S071 | SQL paths in function and type name resolution | X |
| F461 | Named character sets | X |
| F171 | Multiple schemas per user | O |
| T332 | Extended roles | X |

<a id="8b7948cfeb04d955"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP SCHEMA](#e0d28b672c65ac71)
- [CREATE USER](#f516f713c62659c7)
- [CREATE TABLE](#66fde705300657e5)
- [CREATE VIEW](#c6a48c56234057a1)
- [CREATE INDEX](#8e0637af857026b6)
- [CREATE SEQUENCE](#0466abe24a740737)
- [GRANT privileges TO](#71c467631eb14f4c)
- [COMMENT ON name IS](#7c5772ac3aa2f438)

<a id="0466abe24a740737"></a>
## CREATE SEQUENCE

<a id="05778ebf76087999"></a>
### 기능

시퀀스를 생성한다.

<a id="dc7f6a8e21bfe409"></a>
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

<a id="65ca230ac653ad56"></a>
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

<a id="262ff8246027ebab"></a>
### 구문 규칙 및 파라미터

<a id="f1e1a8f5874afec7"></a>
#### sequence_name

생성할 시퀀스의 이름이며 스키마 내에서 유일한 이름이어야 한다.  
schema_name.sequence_name과 같이 시퀀스가 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
시퀀스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="65dc070574af3e7e"></a>
#### &lt;sequence generator option&gt;

&lt;sequence generator option&gt;을 사용하지 않을 경우 다음 두 문장은 같은 의미를 갖는다.

- CREATE SEQUENCE test_seq; 
- CREATE SEQUENCE test_seq START WITH 1 INCREMENT BY 1 NO MINVALUE NO MAXVALUE NO CYCLE CACHE 20;

<a id="e445da959af18612"></a>
#### &lt;sequence generator start with option&gt;

첫 번째로 생성할 시퀀스 번호를 정의한다.   
오름차순인지 내림차순인지에 따라 다음과 같은 특징을 갖는다.

- 오름차순 시퀀스일 경우 (INCREMENT BY 양수) 
    - 최소값보다 큰 시퀀스 값으로 시작하고자 할 경우에 사용한다. 
    - START WITH 절을 생략할 경우, 기본값은 최소값 (MINVALUE value)이 된다. 
- 내림차순 시퀀스일 경우 (INCREMENT BY 음수) 
    - 최대값보다 작은 시퀀스 값으로 시작하고자 할 경우에 사용한다. 
    - START WITH 절을 생략할 경우, 기본값은 최대값 (MAXVALUE value)이 된다.

<a id="9bb8550295d5b66b"></a>
#### &lt;sequence generator increment by option&gt;

시퀀스 번호의 간격을 정의한다.   
다음과 같은 제약 및 특징을 갖는다.

- 양수 또는 음수를 사용할 수 있으며, 0은 사용할 수 없다. 
- 간격의 절대값은 MINVALUE와 MAXVALUE의 차이보다 작아야 한다. 
- 양수일 경우 오름차순 시퀀스가 생성되며 음수일 경우 내림차순 시퀀스가 생성된다. 
- INCREMENT BY 절을 생략할 경우, 기본값은 양수 1 이다.

<a id="e874cdac115ea2a8"></a>
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

<a id="5d2c9740a71c2fe6"></a>
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

<a id="aa46c9ea83653c98"></a>
#### &lt;sequence generator cycle option&gt;

시퀀스의 값이 최대값 또는 최소값이 되었을 때, 계속 값을 생성할지 여부를 명시한다.

- CYCLE 
    - 오름차순 시퀀스가 최대값이 되었을 때, 최소값부터 다시 생성한다. 
    - 내림차순 시퀀스가 최소값이 되었을 때, 최대값부터 다시 생성한다. 
- NO CYCLE | NOCYCLE 
    - 최대값 또는 최소값이 되었을 때, 시퀀스 값을 생성할 수 없다. 
    - NO CYCLE (SQL 표준) 과 NOCYCLE 은 동일한 의미의 예약어로 어떤 것을 사용해도 무방하다. 
- CYCLE과 NO CYCLE을 명시하지 않을 경우, 기본값은 NO CYCLE 이다.

<a id="f9bdd9928ef1d142"></a>
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

<a id="dbf46839a668806c"></a>
### 설명

생성한 시퀀스 객체의 시퀀스 값은 [NEXTVAL](17-built-in-function-references.md#d36ad8ad2fda2581) 함수와 [CURRVAL](17-built-in-function-references.md#aec74f0a0f494b5c) 함수를 이용하여 사용할 수 있다.

시퀀스 값은 트랜잭션 속성을 가지지 않으며, 시퀀스 함수를 사용한 SQL 구문에서 에러가 발생하거나 명시적인 ROLLBACK을 수행하더라도 시퀀스 값은 가장 최신 값을 유지한다.

CURRVAL 함수의 경우, session에서 가장 최근에 호출한 NEXTVAL 값을 반환한다.   
이러한 특성을 이용하면 NEXTVAL을 이용하여 한 번 얻은 시퀀스 값을 다른 SQL 문장에 계속 사용할 수 있다.  단, session에서 NEXTVAL을 호출하지 않은 경우에 CURRVAL를 사용하면 에러가 발생한다.

<a id="f0a25ccc0f3fb9d3"></a>
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

<a id="aa2cdc432d208f4a"></a>
### 호환성

SQL 표준에서는 &lt;sequence generator cache option&gt; 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="0487d24b3f96b8d9"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="4c0ade5ca30dfe55"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP SEQUENCE](#4693b77a7e62cf8a)
- [ALTER SEQUENCE](18-sql-references-a-b.md#3df2c32d366ffd24)
- [NEXTVAL](17-built-in-function-references.md#d36ad8ad2fda2581)
- [CURRVAL](17-built-in-function-references.md#aec74f0a0f494b5c)

<a id="734a2d8ce3896204"></a>
## CREATE SYNONYM

<a id="15d3d7554ac4f0da"></a>
### 기능

Synonym을 생성한다. Synonym은 테이블, view, 시퀀스, 또다른 synonym의 대체 이름으로써 이들 대신 다음 구문에서 사용될 수 있다.

- DML: SELECT, INSERT, UPDATE, DELETE, LOCK TABLE, CALL
- DDL: GRANT, REVOKE, COMMENT

<a id="6685ebcc8b5050be"></a>
### 구문

```
<table definition> ::=    
    CREATE [OR REPLACE] [PUBLIC] SYNONYM [schema_name.]synonym_name 
    FOR [schema_name.]object_name
    ;
```

<a id="11815b84a99ed730"></a>
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

<a id="6a54a5c3ce667095"></a>
### 구문 규칙 및 파라미터

<a id="78fa95881cc30b8c"></a>
#### [ OR REPLACE ]

이미 synonym이 존재할 경우, 기존의 synonym을 대체한다.

<a id="d6646b8af8d68aac"></a>
#### [ PUBLIC ]

Public synonym을 만들기 위해 명시한다.   
이 절을 생략하면 private synonym이 생성된다.

<a id="6f8ddc10b157f3f9"></a>
#### synonym_name

생성할 synonym의 이름이며, 스키마 내에서 유일한 이름이어야 한다.   
schema_name.synonym_name과 같이 synonym이 소속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
Synonym 이름의 길이는 128 바이트보다 작아야 한다.   
Public synonym은 non-schema 객체이다. 따라서 PUBLIC을 명시하여 public synonym을 생성할 때는 스키마 이름을 명시할 수 없다.

<a id="e81d14276edbad32"></a>
#### object_name

schema_name.object_name과 같이 객체가 소속된 스키마를 명시할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

object_name을 명시할 수 있는 객체 타입은 다음과 같다.

- Table
- View
- Sequence
- 또 다른 synonym

대상 객체의 존재 여부, cycle check, 권한 검사 등은 synonym을 사용한 구문을 수행할 때 실행된다.

<a id="61dab746835e0faa"></a>
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

<a id="2aa56682f645e967"></a>
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

<a id="e2144ce2d91335dc"></a>
### 호환성

SQL 표준에서는 CREATE SYNONYM 구문을 정의하지 않고 있다.

<a id="aa040771872ff167"></a>
### 참조

관련 내용은 [DROP SYNONYM](#140ff3d497836df4)을 참조한다.

<a id="66fde705300657e5"></a>
## CREATE TABLE

<a id="e0c4a0fc852d25c0"></a>
### 기능

테이블을 정의한다.

<a id="6135e59f132ebe39"></a>
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

<a id="a4135fb21e1c7a9b"></a>
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

<a id="a1873d5b3a3633ff"></a>
### 구문 규칙 및 파라미터

<a id="b6ba1413e43e572e"></a>
#### table_name

생성할 테이블의 이름이며, 스키마 내에서 유일한 이름이어야 한다.   
schema_name.table_name과 같이 테이블이 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
테이블 이름의 길이는 128 바이트보다 작아야 한다.

<a id="c900b5532bd27960"></a>
#### &lt;column definition&gt;

테이블을 구성할 column을 정의한다.   
테이블은 하나 이상의 column에 대한 정의를 포함해야 한다.   
Column의 데이터 타입, 기본값, 자동 생성 값, 제약 조건 등을 기술할 수 있다.

<a id="a67da8ad1676c537"></a>
#### column_name

테이블을 구성할 column의 이름으로 각 column은 테이블 내에서 유일한 이름을 가져야 한다.   
Column 이름의 길이는 128 바이트보다 작아야 한다.

<a id="6a1e8bcaf9c9ac5f"></a>
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
데이터 타입과 관련한 자세한 내용은 [Data Type](11-sql-elements.md#8bd9f5c161f4f4d1) 정의를 참조한다.

<a id="a20fdcfcfd55fca2"></a>
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

<a id="0bb0f66b48950c25"></a>
#### [ &lt;default clause&gt; | &lt;identity column specification&gt; ]

Column의 기본값을 명시한다.   
&lt;default clause&gt;와 &lt;identity column specification&gt;은 함께 사용할 수 없다.   
모두 생략할 경우, 기본값은 NULL이다.

<a id="fb28203ff120409d"></a>
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

<a id="b0d3a504f09267ed"></a>
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

identity column 생성 옵션인 &lt;common sequence generator option&gt;과 &lt;basic sequence generator option&gt;에 대한 자세한 내용은 [CREATE SEQUENCE](#0466abe24a740737) 구문을 참조한다.

<a id="02b759c04f674cba"></a>
#### &lt;column constraint definition&gt;

Column에 대해 다음과 같은 제약 조건을 정의한다.

- NOT NULL 제약 조건 
- UNIQUE 제약 조건 
- PRIMARY KEY 제약 조건

<a id="f101fa199ea3fe08"></a>
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

<a id="5c506138d6573823"></a>
#### NOT NULL 제약 조건

Column 값으로 NULL 값을 허용하지 않는다.

<a id="34f4c18088aaac96"></a>
#### UNIQUE 제약 조건

Column 값으로 동일한 값을 허용하지 않는다.   
단, NULL 값은 허용한다.

<a id="7e0b3dde202d442a"></a>
#### PRIMARY KEY 제약 조건

Column 값으로 NULL 값이나 동일한 값을 허용하지 않는다.   
하나의 테이블에 하나의 PRIMARY KEY 제약 조건을 정의할 수 있다.

<a id="da6d8fa609b21efe"></a>
#### &lt;index name clause&gt;

UNIQUE 제약 조건, PRIMARY KEY 제약 조건을 정의할 때 생성되는 인덱스의 이름을 정의한다.

- INDEX index_name 
    - 제약 조건을 위한 인덱스의 이름을 정의한다. 
    - 스키마 이름과 함께 사용할 수 없으며, 제약 조건과 동일한 스키마에 생성된다.

UNIQUE 제약 조건, PRIMARY KEY 제약 조건을 정의할 때 INDEX 절을 생략할 경우에는 제약 조건에 부합하는 인덱스를 자동으로 생성한다.  
자동 생성되는 인덱스 이름으로는 "constraint_name" + "_INDEX"가 부여된다.

- &lt;index attributes&gt; 
    - 생성할 인덱스의 물리적 속성을 지정한다. 
    - 자세한 내용은 [CREATE INDEX](#8e0637af857026b6) 구문을 참조한다. 
- TABLESPACE index_tablespace_name 
    - 인덱스를 생성할 tablespace 를 지정한다. 
    - 자세한 내용은 [CREATE INDEX](#8e0637af857026b6) 을 참조한다.

<a id="f133717800abbac2"></a>
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

<a id="d06425d0ced16615"></a>
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

<a id="f4e691c3bbb652cd"></a>
#### &lt;table sharding strategy&gt;

테이블의 sharding 정책을 정의한다.   
다음과 같은 네 가지 정책 중 하나로 정의할 수 있다.

- &lt;cloned strategy&gt; 
- &lt;hash sharding strategy&gt; 
- &lt;range sharding strategy&gt; 
- &lt;list sharding strategy&gt;

생략할 경우 [DEFAULT_SHARDING](../part-02-administration-manual/10-server-property.md#23503fafcc828415) 프로퍼티 값에 의해 결정된다.

- DEFAULT_SHARDING 값이 0 인 경우
    - &lt;cloned strategy&gt;
- DEFAULT_SHARDING 값이 1 인 경우
    - &lt;hash sharding strategy&gt;

<a id="2e68746c88cf41ec"></a>
#### &lt;cloned strategy&gt;

테이블의 모든 data를 복제한다.

<a id="c9c8e4c0e4e66b73"></a>
#### &lt;clone placement&gt;

Clone의 배치 정책을 정의한다.

- AT CLUSTER WIDE 
    - Cluster system의 모든 cluster group의 모든 cluster member에 clone을 배치한다. 
    - Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#1af19281915840f1) 구문을 사용하여 clone을 재배치할 수 있다. 
- AT CLUSTER GROUP group_list 
    - 지정한 cluster group들의 모든 cluster member에 clone을 배치한다. 
    - 지정된 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#1af19281915840f1) 구문을 사용하여 clone을 재배치할 수 있다. 
    - Cluster group 추가는 clone의 재배치에 영향을 주지 않는다.
- 생략할 경우, 기본값은 AT CLUSTER WIDE이다.

<a id="6bfe8777e58d2e0f"></a>
#### &lt;hash sharding strategy&gt;

테이블의 data를 sharding key의 hash 값을 기준으로 shard를 분할한다.

<a id="79eefa9da8072137"></a>
#### SHARDING BY [HASH] ( column_list )

Hash sharding을 위한 sharding key를 정의한다.

- Column을 32 개까지 나열할 수 있다. 
- 동일한 column은 사용할 수 없다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column은 사용할 수 없다.

<a id="508ae4687f9f9e66"></a>
#### &lt;hash shard count&gt;

분할할 hash shard의 개수를 정의한다.   
Shard의 개수는 1부터 512까지 정의할 수 있다.   
생략할 경우 기본값은 24이다.

<a id="54c9b29eb97a81de"></a>
#### &lt;hash shard placement&gt;

Hash shard의 배치 정책을 정의한다.

- AT CLUSTER WIDE 
    - Cluster system의 모든 cluster group의 모든 cluster member에 shard 들을 배치한다. 
    - Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#1af19281915840f1) 구문을 사용하여 shard들을 재배치할 수 있다. 
- AT CLUSTER GROUP group_list 
    - 지정한 cluster group들의 모든 cluster member에 hash shard들을 배치한다. 
    - group_list의 개수는 &lt;hash shard count&gt;의 값과 같거나 작아야 한다. 
    - range shard, list shard와 달리 hash shard는 특정 shard가 배치될 cluster group을 지정할 수 없으며, system이 자동으로 shard 들을 배치할 cluster group을 결정한다. 
    - 지정한 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#1af19281915840f1) 구문을 사용하여 shard를 재배치할 수 있다. 
    - Cluster group 추가는 hash shard의 재배치에 영향을 주지 않는다.
- 생략할 경우, 기본값은 AT CLUSTER WIDE 이다.

<a id="ed567e09a9dfe6e8"></a>
#### &lt;range sharding strategy&gt;

테이블의 data를 sharding key의 범위값을 기준으로 shard 분할한다.

<a id="eaf1b7ad42be0c27"></a>
#### SHARDING BY RANGE ( column_list )

Range sharding을 위한 sharding key를 정의한다.

- Column을 32 개까지 나열할 수 있다. 
- 동일한 column은 사용할 수 없다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column은 사용할 수 없다.

<a id="492a06d8df50b6fb"></a>
#### &lt;cluster-wide range shard placement&gt;

Range shard들을 cluster system의 모든 cluster group으로 자동으로 배치한다.  
&lt;range shard definition&gt;을 기술하기 전에 AT CLUSTER WIDE 구문을 기술한다.  
Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#1af19281915840f1) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.

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

<a id="2cc7e3d1ecf81d75"></a>
#### &lt;group-specific range shard placement&gt;

Range shard들을 지정한 cluster group에 배치한다.  
&lt;range shard definition&gt;과 함께 해당 shard를 배치할 AT CLUSTER GROUP group_name 구문을 기술한다.  
지정한 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#1af19281915840f1) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.  
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

<a id="72c23c087df6d29f"></a>
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

<a id="3004f814956e5fc6"></a>
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

<a id="149871a18d8c9be8"></a>
#### &lt;list sharding strategy&gt;

테이블의 data를 sharding key 의 나열값을 기준으로 shard를 분할한다.

<a id="c14ba1246baabeb7"></a>
#### SHARDING BY LIST ( column_name )

List sharding을 위한 sharding key를 정의한다.

- 하나의 column만 사용할 수 있다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column을 사용할 수 없다.

<a id="b843495edd832711"></a>
#### &lt;cluster-wide list shard placement&gt;

Cluster system의 모든 cluster group에 list shard들을 자동으로 배치한다.  
&lt;list shard definition&gt;을 기술하기 전에 AT CLUSTER WIDE 구문을 기술한다.  
Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#1af19281915840f1) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.

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

<a id="7ccfb278ee1e4e73"></a>
#### &lt;group-specific list shard placement&gt;

List shard들을 지정한 cluster group에 배치한다.  
&lt;list shard definition&gt;과 함께 해당 shard를 배치할 AT CLUSTER GROUP group_name 구문을 기술한다.  
지정한 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#1af19281915840f1) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.  
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

<a id="5369646d0930f19b"></a>
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

<a id="9e010d5aa8ab187d"></a>
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

<a id="565670570ebe15ff"></a>
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

<a id="ca1143e799186787"></a>
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

<a id="bb17e1348146089a"></a>
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
    - 생략할 경우, 기본값은 EXTENT 크기 * 2147483647 (INT32의 최대 양의 정수)이다.

<a id="1d3a1344b7a4a6da"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="1cd496445ad4b8cc"></a>
#### TABLESPACE tablespace_name

테이블이 저장될 tablespace의 이름을 지정한다.   
TABLESPACE 절을 생략할 경우, 구문을 수행하는 사용자의 기본 tablespace_name을 사용한다.

<a id="c606562c7540bd90"></a>
#### TABLESPACE index_tablespace_name

인덱스가 저장될 tablespace의 이름을 지정한다.   
TABLESPACE 절을 생략할 경우, 사용자의 인덱스 테이블스페이스를 사용한다.  
사용자의 인덱스 테이블스페이스가 NULL인 경우, DISK 테이블은 사용자의 데이터 테이블스페이스를 사용하고 MEMORY 테이블은 사용자의 기본 임시 테이블스페이스를 사용한다.

<a id="b2bf0d3413c04fc2"></a>
#### &lt;constraint characteristics&gt;

제약 조건의 특성을 정의한다.   
제약 조건을 정의할 때 다음과 같은 특성들을 설정할 수 있다.

- 제약 조건의 지연가능성 ( DEFERRABLE | NOT DEFERRABLE )
- 제약 조건의 검사시점 ( &lt;constraint check time&gt; )

&lt;constraint characteristics&gt;를 생략할 경우, NOT DEFERRABLE INITIALLY IMMEDIATE로 설정한다.

<a id="5d19a48e5bd3eb15"></a>
#### DEFERRABLE | NOT DEFERRABLE

제약 조건을 DML을 수행할 때 검사하지 않고, COMMIT을 수행할 때 검사할 수 있게 지연시킬 수 있는지 여부를 설정한다.

지연 가능한 제약 조건의 검사시점은 [SET CONSTRAINTS](20-sql-references-h-z.md#2e96c033f710d10f) 구문으로 제어한다.

- NOT DEFERRABLE
    - 검사 시점을 지연시킬 수 없으며, INSERT, DELETE, UPDATE 구문을 수행할 때 제약 조건을 검사한다.
- DEFERRABLE
    - 검사 시점을 [SET CONSTRAINTS](20-sql-references-h-z.md#2e96c033f710d10f) 구문으로 제어할 수 있다.
    - SET CONSTRAINTS constraint_name IMMEDIATE
        - DML을 수행할 때 제약 조건을 검사한다.
    - SET CONSTRAINTS constraint_name DEFERRED
        - COMMIT을 수행할 때 제약 조건을 검사한다.
- 명시하지 않을 경우 기본값은 &lt;constraint check time&gt;에 따라 결정된다.
    - INITIALLY IMMEDIATE를 명시한 경우, NOT DEFERRABLE 이다.
    - INITIALLY DEFERRED를 명시한 경우, DEFERRABLE 이다.
    - &lt;constraint check time&gt;을 명시하지 않은 경우, NOT DEFERRABLE 이다.

<a id="b9142b2495142202"></a>
#### &lt;constraint check time&gt;

지연가능한 (DEFERRABLE) 제약 조건일 경우, 검사 시점의 초기값을 설정한다.

- INITIALLY IMMEDIATE
    - DML을 수행할 때 제약 조건을 검사한다.
- INITIALLY DEFERRED
    - COMMIT을 수행할 때 제약 조건을 검사한다.
    - NOT DEFERRABLE과 함께 사용할 수 없다.
- 명시하지 않을 경우, 기본값은 INITIALLY IMMEDIATE 이다.

지연 가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](20-sql-references-h-z.md#2e96c033f710d10f) 구문을 참조한다.

<a id="bce47426ca2b194e"></a>
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

<a id="134dd076bf0d34ec"></a>
### 설명

<a id="4bbf941322b744b7"></a>
#### 제약 조건의 특성

GOLDILOCKS는 key 제약 조건을 생성할 때 uniqueness 검사를 하기 위해 자동으로 index를 생성한다.

다음과 같은 column은 NULL 값을 허용하지 않는다.

- NOT NULL 제약 조건이 있는 column
- Primary key 제약 조건에 포함되는 column
- Identity column

<a id="79abdef111c8519b"></a>
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

<a id="cf6ecdde8a6dd78c"></a>
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

<a id="0c1599dfebbe1503"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- TABLESPACE 절, &lt;physical attribute clause&gt; 절 등의 물리적 개념
- SQL 표준은 DEFAULT 절에 연산을 사용할 수 없다.

**SQL 표준 호환성**

<a id="706294696639f5ab"></a>
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

<a id="a3f1df317726457e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLE](#a964ea8a5781b06d)
- [ALTER TABLE](18-sql-references-a-b.md#9f06fbbb97531643)
- [CREATE TABLESPACE](#9425404264bb2534)
- [CREATE SCHEMA](#e1a750bc16ba12f6)
- [CREATE INDEX](#8e0637af857026b6)
- [CREATE SEQUENCE](#0466abe24a740737)
- [SET CONSTRAINTS](20-sql-references-h-z.md#2e96c033f710d10f)
- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](18-sql-references-a-b.md#1c36bfba15f57bda)

<a id="a8bce0d0a242157d"></a>
## CREATE TABLE AS SELECT

<a id="d3a00020c9de0a34"></a>
### 기능

질의 결과로부터 새로운 테이블을 생성한다.

<a id="7f5eaa5176b3018f"></a>
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

<a id="ba99a7e8b077dba1"></a>
### 사용 범위 및 접근 권한

&lt;table definition:AS query expression&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블 생성 권한
    - [CREATE TABLE](#66fde705300657e5) 구문의 접근 권한을 참조한다.
- SELECT 접근 권한 
    - [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5) 구문의 접근 권한을 참조한다.

<a id="3aa742fc92d71bcb"></a>
### 구문 규칙 및 파라미터

<a id="32127ff9a45cc959"></a>
#### table_name

생성할 테이블의 이름이다.  
자세한 내용은 [table_name](#b6ba1413e43e572e) 구문을 참조한다.

<a id="7eab27f6048c58cd"></a>
#### column_name_list

테이블을 구성할 column의 이름으로써 테이블 내에서 유일한 이름이어야 하며, column의 개수는 SELECT 절의 결과 column 개수와 동일해야 한다.   
명시하지 않을 경우, &lt;query expression&gt;의 SELECT 절의 column 이름을 사용한다.

단, SELECT절에 column이 아닌 expression (function, operation, subquery 등)이 오면 alias 또는 column name을 명시해야 한다.

Column 이름의 길이는 128 바이트보다 작아야 한다.

<a id="10af9aa257e43e83"></a>
#### WITH [NO] DATA

WITH DATA가 명시된 경우, SELECT 절의 결과가 생성될 테이블에 INSERT 된다.    
WITH NO DATA가 명시된 경우, SELECT 절의 결과가 생성될 테이블에 INSERT 되지 않는다.    
명시하지 않을 경우, WITH DATA를 명시한 것과 동일하게 작동한다.

<a id="2975ce825de9f47f"></a>
#### other syntax

이 외의 구문 규칙은 [CREATE TABLE](#66fde705300657e5) 구문의 syntax를 참조한다.

<a id="8df9696ca687134f"></a>
### 설명

CREATE TABLE AS SELECT 구문을 수행할 때 SELECT list에 NOT NULL 제약 조건이 있는 column이 명시된 경우, 새로운 테이블에도 NOT NULL 제약 조건이 생성된다.  단, 지연 가능한 NOT NULL 제약 조건인 경우, 새로운 테이블에는 NOT NULL 제약 조건을 생성하지 않는다.

그러나 명시적으로 NOT NULL 제약 조건을 생성한 것이 아니라, primary key, identity column과 같이 NOT NULL 속성을 가지고 있는 경우에는 새로운 테이블에 NOT NULL 제약 조건을 생성하지 않는다.

<a id="1a878bfbb1180e32"></a>
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

<a id="82cd1b7733b6234c"></a>
### 호환성

CREATE TABLE AS SELECT 구문은 SQL 표준을 따른다. 단, 다음은 표준에서 확장된 것이다.

- 표준에서 SELECT 절 밖의 괄호는 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- 표준에서 WITH [NO] DATA 절은 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- GOLDILOCKS의 tablespace 개념은 표준에 없는 확장 개념이다.

**SQL 표준 호환성**

<a id="c132e6f334ce2c17"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T172 | AS subquery clause in table definition | O |

<a id="33f4d3605831cb9e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](#66fde705300657e5)
- [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5)

<a id="9425404264bb2534"></a>
## CREATE TABLESPACE

<a id="a1ac54acd2d02526"></a>
### 기능

테이블스페이스를 생성한다.

<a id="6e89f55697d46662"></a>
### 구문

```
<create tablespace statement> ::=
      <memory data tablespace statement>
    | <memory temporary tablespace statement>
    ;
```

<a id="c4d6b705c0481440"></a>
### 사용 범위 및 접근 권한

&lt;create tablespace statement&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="0a063265d6b993c8"></a>
### 구문 규칙 및 파라미터

<a id="6fb91112bff79802"></a>
#### &lt;memory data tablespace statement&gt;

- [ MEMORY ] TEMPORARY

질의 처리 과정에서 생성되는 중간 결과 등의 임시 객체나 no logging 인덱스를 저장할 메모리 임시 테이블스페이스이다.  
MEMORY 예약어는 생략할 수 있다.

<a id="26e298aeaa0c8035"></a>
#### &lt;memory data tablespace clause&gt;

메모리 데이터의 테이블스페이스를 정의한다.  
자세한 내용은 [CREATE MEMORY DATA TABLESPACE](#86993cea38f6279a) 구문을 참조한다.

<a id="6b2ba6af4da21a6d"></a>
#### &lt;memory temporary tablespace definition&gt;

메모리의 임시 테이블스페이스를 정의한다.  
자세한 내용은 [CREATE MEMORY TEMPORARY TABLESPACE](#54c1cb4e7c65e722) 구문을 참조한다.

<a id="538874383f756a3c"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="6b279dffaa44b7b1"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="d725fb2c75e94663"></a>
### 호환성

SQL 표준은 tablespace에 대한 개념을 다루지 않고 있다.

<a id="10eb0fe0a77c0492"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#0ccb2cbcfd412a42)
- [ALTER TABLESPACE](18-sql-references-a-b.md#7c3ae65b4798a999)

<a id="f516f713c62659c7"></a>
## CREATE USER

<a id="cd87f062797643aa"></a>
### 기능

데이터베이스 사용자를 정의한다.

<a id="2393398cb5e20c0e"></a>
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

<a id="69afcd3b8380459c"></a>
### 사용 범위 및 접근 권한

&lt;user definition&gt; 구문을 수행하려면 사용자에게 CREATE USER ON DATABASE 권한이 있어야 한다.

생성한 user_identifier 사용자는 &lt;schema clause&gt;로 생성한 스키마의 소유자라는 권한을 갖는다.

> 생성된 user_identifier에는 별도의 권한이 부여되지 않는다.  
> user_identifier 사용자가 접속해서 SQL 구문을 수행하려면 적절한 권한을 부여받아야 한다.

<a id="ef96a9ee4801159d"></a>
### 구문 규칙 및 파라미터

<a id="f8e1be026915126d"></a>
#### user_identifier

생성할 user의 이름이다.  
동일한 사용자 이름 (user_identifier)이나 역할 이름 (role_name)이 존재하지 않아야 한다.  
user_identifier의 길이는 128 byte 보다 작아야 한다.

<a id="64448bbdf1789eb0"></a>
#### password

생성할 user의 password로써 암호화되어 저장된다.  
password의 길이는 128 byte보다 작아야 한다.  
password는 대소문자를 구별한다.  
password는 영문자로 시작해야 하고 영문자, 숫자, underscore(_), $를 포함할 수 있다.  
그 외의 특수문자를 사용하려면 double-quotation (")으로 묶어야 한다.

<a id="3a5ba8071fe20408"></a>
#### PROFILE { profile_name | DEFAULT | NULL }

비밀번호 관리 정책을 위한 profile을 할당한다.

- PROFILE profile_name
    - 사용자가 생성한 profile_name을 할당한다.
- PROFILE DEFAULT
    - 기본 profile "DEFAULT"를 할당한다.
- PROFILE NULL
    - Profile을 할당하지 않는다.

PROFILE 절을 생략할 경우, PROFILE NULL과 동일하며 profile이 적용되지 않는다.  
비밀번호 관리 정책에 대한 자세한 내용은 [CREATE PROFILE](#f421f468f014cc7b) 을 참조한다.

<a id="16892aecf128d615"></a>
#### PASSWORD EXPIRE

사용자의 비밀번호 유효기간을 만료시킨다.  
사용자가 login 하기 전에 강제로 비밀번호를 변경하도록 하기 위해 사용한다.

<a id="a3606856326fbc2e"></a>
#### ACCOUNT { LOCK | UNLOCK }

- ACCOUNT LOCK
    - 사용자 계정을 잠근다.
- ACCOUNT UNLOCK
    - 계정 잠금을 해제한다.

<a id="d8a3d7667c7fa5e3"></a>
#### DEFAULT TABLESPACE tablespace_name

User가 생성하는 테이블, 인덱스 (LOGGING) 등의 객체가 저장될 기본 TABLESPACE를 지정한다.  
DEFAULT TABLESPACE 절을 생략할 경우, DATABASE를 생성할 때 정의한 default data tablespace (MEM_DATA_TBS)가 지정된다.

<a id="6624696088563448"></a>
#### TEMPORARY TABLESPACE tablespace_name

User가 생성하는 임시 테이블, 인덱스 (NO LOGGING), 질의 처리 과정에서 생성되는 중간 결과들을 저장할 TABLESPACE를 지정한다.  
TEMPORARY TABLESPACE 절을 생략할 경우, DATABASE를 생성할 때 정의한 default temporary tablespace (MEM_TEMP_TBS)가 지정된다.

<a id="5bc953a5e0392300"></a>
#### INDEX TABLESPACE { tablespace_name | NULL }

User가 생성하는 인덱스 객체가 저장되는 기본 TABLESPACE를 지정한다.

- INDEX TABLESPACE tablespace_name 지정
    - Data tablespace를 지정할 경우, LOGGING 인덱스가 된다.
    - Temporary tablespace를 지정할 경우, NOLOGGING 인덱스가 된다.

- INDEX TABLESPACE NULL
    - Index tablespace을 지정하지 않는다.

INDEX TABLESPACE 절을 생략할 경우, INDEX TABLESPACE NULL 이다.

<a id="ddec22063c5d1729"></a>
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
사용자가 소유할 스키마는 [CREATE SCHEMA](#e1a750bc16ba12f6) 구문을 사용하여 추가로 생성할 수 있다.

<a id="cde2e30107cfe21a"></a>
### 설명

User는 권한의 집합으로 구성된 authorization 객체이다.

최초로 &lt;user definition&gt; 구문을 수행할 때 어떠한 권한도 부여받지 않은 user가 생성되고 다음과 같이 적절한 권한을 부여해야 한다.

GOLDILOCKS에서 user와 schema의 관계는 1 : N 이다.  
즉, user가 소유한 schema가 존재하지 않을 수도 있고 다수의 schema를 소유할 수도 있다.

SQL 표준은 user, schema, database 등의 non-schema 객체들의 관계에 대해 명확히 정의하지 않고 있다. 반면, 각 DBMS 들은 다음과 같이 non-schema 객체 간의 관계를 상이하게 정의하고 있다.

> DBMS별 user와 schema 관계   
>   
> • Oracle  
> ∘ User : schema = 1 : 1의 관계이다.  
>   
> • DB2   
> ∘ OS user와 동일하다.   
> ∘ User를 생성하고 삭제하는 별도의 SQL 구문이 없다.   
>   
> • Postgres   
> ∘ User : schema = 1 : N의 관계이다.   
>   
> • MySQL   
> ∘ Database : schema = 1 : 1의 관계이다.  
> ∘ User는 database (schema)의 하위 객체이다.

<a id="8499538b1d421f77"></a>
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

<a id="5c5bdec5cab8c202"></a>
### 호환성

SQL 표준에서는 user 개념은 다루고 있지만 user 생성 및 삭제와 관련된 SQL 구문은 정의하지 않고 있다.

<a id="c4da62efbe2acccd"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP USER](#a6f0bdba7a87d9c4)
- [ALTER USER](18-sql-references-a-b.md#648c7792f8549c18)
- [CREATE SCHEMA](#e1a750bc16ba12f6)

<a id="c6a48c56234057a1"></a>
## CREATE VIEW

<a id="7ebac612d7cd2fc1"></a>
### 기능

View를 정의한다.

<a id="165c2b8958a53022"></a>
### 구문

```
<view definition> ::=
    CREATE [ OR REPLACE ] [ FORCE | NO FORCE ] 
        VIEW view_name [ ( column_name [, ...] ) ]
        AS <query expression>
    ;
```

<a id="0f4a616118d525ea"></a>
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

<a id="8d548f3737f92915"></a>
### 구문 규칙 및 파라미터

<a id="bcf6d59ed58bc998"></a>
#### [ OR REPLACE ]

이미 존재하는 view가 있을 경우, 기존의 view를 대체한다.

<a id="48072d81bc21c073"></a>
#### [ FORCE | NO FORCE ]

- FORCE 
    - &lt;query expression&gt;의 유효성 여부에 관계없이 view를 생성한다. 
- NO FORCE 
    - &lt;query expression&gt;이 유효할 경우 view를 생성한다.
- 기본값은 NO FORCE 이다

<a id="7755302c5f8a4579"></a>
#### view_name

생성할 view의 이름이며, 스키마 내에서 유일한 이름이어야 한다.   
schema_name.view_name과 같이 view가 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우,구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
View 이름의 길이는 128 바이트보다 작아야 한다.

<a id="cbbcc7e8966e3f50"></a>
#### [ ( column_name [, ...] ) ]

View를 구성할 column의 이름을 정의한다.   
각 column의 이름은 view 내에서 고유한 이름이어야 한다.

Column의 개수는 SELECT 절의 결과 column 개수와 동일해야 한다.

Column 이름의 리스트를 생략할 경우, &lt;query expression&gt;의 SELECT 절의 column 이름을 사용한다.

<a id="cbab976d1366329c"></a>
##### AS &lt;query expression&gt;

View를 생성하는 [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5) 질의이다.

&lt;query expression&gt;에는 다음과 같은 변수를 포함할 수 없다.

- Host parameter 
- SQL parameter 
- Dynamic parameter 
- Embedded variable 
- SEQUENCE 객체

<a id="51844c96559cb227"></a>
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

<a id="7b2a068debd8f522"></a>
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

<a id="e7d36c8241300300"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- [ OR REPLACE ] 절 
- [ FORCE | NO FORCE ] 절

**SQL 표준 호환성**

<a id="1bf696f79421bc57"></a>
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

<a id="a16b0597ec46aee1"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP VIEW](#9ad6c24b5f2fb86f)
- [ALTER VIEW](18-sql-references-a-b.md#a1de7597c5662129)
- [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5)

<a id="f41bd2e5b923c676"></a>
## DECLARE cursor_name

<a id="7a037e178aaa426b"></a>
### 기능

커서를 선언한다.

<a id="5f249cb416e6218f"></a>
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

<a id="834ca07f8212ced4"></a>
### 사용 범위 및 접근 권한

statement_name을 사용한 동적 커서 (dynamic cursor)는 embedded SQL에서 사용할 수 있다.

&lt;cursor query&gt;의 유형에 따라 적절한 접근 권한을 가져야 한다.   
접근 권한에 대한 자세한 내용은 다음을 참조한다.

- [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5) 구문의 접근 권한
- [SELECT .. FOR UPDATE](20-sql-references-h-z.md#efdca3ec1b8b28d9) 구문의 접근 권한
- [INSERT INTO name RETURNING](20-sql-references-h-z.md#b7be21943ea082ab) 구문의 접근 권한
- [UPDATE name RETURNING](20-sql-references-h-z.md#cba95fe5c27e5189) 구문의 접근 권한
- [DELETE FROM name RETURNING](#fdf991741942b8a1) 구문의 접근 권한

<a id="f3018f925fe66150"></a>
### 구문 규칙 및 파라미터

<a id="3cf0fac211ad299c"></a>
#### cursor_name

선언할 커서의 이름이다.   
하나의 session 내에서 고유한 이름이어야 한다.   
커서 이름의 길이는 128 바이트보다 작아야 한다.

<a id="1bcab308d36d243d"></a>
#### { FOR | IS }

SQL 표준에서는 구문 키워드로 FOR나 IS 중에 하나를 사용한다.

<a id="87b8ffd5fd9bb165"></a>
#### &lt;cursor properties&gt;

커서의 속성을 정의한다.

- &lt;cursor sensitivity&gt;를 명시하지 않은 경우, 기본값은 INSENSITIVE 이다. 
- &lt;cursor scrollability&gt;를 명시하지 않은 경우, 기본값은 NO SCROLL 이다. 
- &lt;cursor holdability&gt;를 명시하지 않은 경우, &lt;cursor updatability&gt;가 기본값을 결정한다.

<a id="24ed01f6999ce55f"></a>
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

<a id="69c7ee5bc267dae2"></a>
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

<a id="8ddc5b224d82dcef"></a>
#### &lt;cursor scrollability&gt;

Cursor의 result set을 순차적 또는 비순차적으로 fetch 할 수 있는지 여부를 명시한다.

- NO SCROLL 
    - 순차적 FETCH (FETCH NEXT)만 가능하다. 
- SCROLL 
    - 비순차적 FETCH가 가능하다.
- 명시하지 않을 경우, 기본값은 NO SCROLL이다.

<a id="2ad3a9556abd3bc3"></a>
#### &lt;cursor holdability&gt;

Cursor를 OPEN하고 트랜잭션을 commit 한 후에도 cursor가 유지되는지 여부를 설정한다.

- WITH HOLD 
    - 트랜잭션을 COMMIT 해도 cursor가 유지된다. 
    - FOR UPDATE 구문과 함께 사용할 수 없다. 
    - [INSERT INTO name RETURNING](20-sql-references-h-z.md#b7be21943ea082ab) 구문과 함께 사용할 수 없다. 
    - [UPDATE name RETURNING](20-sql-references-h-z.md#cba95fe5c27e5189) 구문과 함께 사용할 수 없다. 
    - [DELETE FROM name RETURNING](#fdf991741942b8a1) 구문과 함께 사용할 수 없다.
    - table commit action이 ON COMMIT DELETE ROWS인 global temporary table을 포함하는 질의에는 사용할 수 없다.

- WITHOUT HOLD 
    - 트랜잭션을 COMMIT/ ROLLBACK하면 cursor를 닫는다.

- Rollback과 cursor
    - 트랜잭션을 rollback 할 경우, 트랜잭션에 포함된 cursor를 닫는다.
    - Savepoint까지 rollback하면 savepoint 이후에 생성된 cursor를 닫는다.

- 명시하지 않을 경우, &lt;cursor holdability&gt;의 기본값은 &lt;cursor updatability&gt;에 따라 결정된다.
    - FOR READ ONLY이거나 &lt;cursor updatability&gt;를 명시하지 않은 경우, 기본값은 WITH HOLD 이다. 
    - FOR UPDATE 구문과 함께 사용할 경우, 기본값은 WITHOUT HOLD 이다.

<a id="2fb32042a90314c4"></a>
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

<a id="6880abe0932e4b9c"></a>
| Updatability | Query 유형 | Sensitivity |
| --- | --- | --- |
| FOR UPDATE | Updatable query | SENSITIVE |
| FOR UPDATE | Non-updatable query | Query error |
| FOR READ ONLY | Any query | INSENSITIVE |
| N/A | Updatable query | SENSITIVE |
| N/A | Non-updatable query | INSENSITIVE |

<a id="4b85433ba639c36b"></a>
#### &lt;cursor specification&gt;

Cursor의 대상이 되는 query를 정의한다.   
statement_name을 사용할 경우, query가 정해지지 않은 동적 커서 (dynamic cursor)가 선언되고, &lt;cursor query&gt;를 사용할 경우, query가 정해진 고정 커서 (standing cursor)가 선언된다.

<a id="06a8d9cdf893ef85"></a>
#### statement_name

Cursor가 참조할 statement_name이며 embedded SQL에서 사용할 수 있다.

statement_name은 &lt;declare cursor&gt; 구문을 수행하기 전에 존재해야 하며, statement_name이 참조하는 SQL 문장은 [PREPARE statement_name](20-sql-references-h-z.md#15a93f4582b0cd5f) 구문이 준비한 query여야 한다.

Query가 아닐 경우 [OPEN cursor_name](20-sql-references-h-z.md#6047f0ea5db92a56) 구문을 수행할 때 error가 발생한다.

<a id="c1e70734a7e34e56"></a>
#### &lt;cursor query&gt;

Cursor에서 사용할 수 있는 query 유형은 다음 각 구문을 참조한다.

- [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5)
- [SELECT .. FOR UPDATE](20-sql-references-h-z.md#efdca3ec1b8b28d9)
- [INSERT INTO name RETURNING](20-sql-references-h-z.md#b7be21943ea082ab)
- [UPDATE name RETURNING](20-sql-references-h-z.md#cba95fe5c27e5189)
- [DELETE FROM name RETURNING](#fdf991741942b8a1)

<a id="a45a992f4710f235"></a>
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

<a id="458b151012407bdf"></a>
#### FOR UPDATE OF …

커서를 OPEN 할 때 lock 획득과 관련된 column을 나열한다.

- FOR UPDATE OF 구문에 나열된 column은
    - &lt;select statement&gt;의 FROM 절에 나열된 table의 갱신 가능한 column이어야 한다. 
    - 나열된 column의 table에 대한 lock을 획득한다. 
- FOR UPDATE만 사용하는 경우에는 
    - &lt;select statement&gt;의 FROM 절에 나열된 table들의 모든 갱신 가능한 column을 나열한 것과 동일한 의미이다. 
    - 모든 column의 table에 대한 lock을 획득한다.

<a id="0c8b13d08bcfd51e"></a>
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

<a id="ac1d0b399f36545a"></a>
### 설명

Query에 대한 속성을 제어할 때 DECLARE CURSOR 구문과 OPEN, FETCH, CLOSE 구문을 사용할 경우, 서버의 커서를 제어하기 때문에 ODBC statement나 JDBC statement를 이용하여 cursor를 사용하는 경우보다 성능상 부하가 걸린다.

Query를 수행하기 전에 ODBC statement와 JDBC statement를 이용해 cursor 속성을 제어할 수 있으며, DECLARE CURSOR 구문을 통한 SQL cursor의 속성 제어 방법과 이에 대응하는 ODBC 표준과 JDBC 표준의 cursor 속성 제어 방법은 다음과 같다.

<a id="d35ff47f6b19caa2"></a>
<table class="table column_count_4"><caption>ODBC/ JDBC의 커서 속성 제어 </caption><thead><tr><th class="to_center to_middle"><div>Property
분류</div></th><th class="to_center to_middle"><div>GOLDILOCKS
cursor property</div></th><th class="to_center to_middle"><div>ODBC 표준의 cursor 속성 설정</div></th><th class="to_center to_middle"><div>JDBC 표준의 cursor 속성 설정</div></th></tr></thead><tbody><tr><td class="to_left to_middle" rowspan="3"><div>Sensitivity</div></td><td class="to_left to_middle"><div>INSENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_INSENSITIVE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle"><div>SENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_SENSITIVE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle"><div>ASENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_UNSPECIFIED, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Scrollability</div></td><td class="to_left to_middle"><div>NO SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_NONSCROLLABLE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle"><div>SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_SCROLLABLE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Holdability</div></td><td class="to_left to_middle"><div>WITHOUT HOLD</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.CLOSE_CURSORS_AT_COMMIT )</div></td></tr><tr><td class="to_left to_middle"><div>WITH HOLD</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.HOLD_CURSORS_OVER_COMMIT )</div></td></tr></tbody></table>

ODBC cursor type에 대응되는 SQL cursor 선언은 다음과 같다.

**ODBC 커서 type에 대응되는 SQL 커서 선언**

<a id="e3283f5b99615233"></a>
| ODBC cursor type | SQL cursor 선언 |
| --- | --- |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, len) | NO SCROLL CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_STATIC, len) | STATIC CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, len) | KEYSET CURSOR |

JDBC cursor type에 대응되는 SQL cursor 선언은 다음과 같다.

**JDBC 커서 type에 대응되는 SQL 커서 선언**

<a id="6182569f048506e1"></a>
| JDBC cursor type | SQL cursor 선언 |
| --- | --- |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_FORWARD_ONLY, conc, hold ) | INSENSITIVE NO SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_INSENSITIVE, conc, hold ) | INSENSITIVE SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_SENSITIVE, conc, hold ) | SENSITIVE SCROLL CURSOR |

<a id="5733937ec2a66256"></a>
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

<a id="ced02b558e35ebca"></a>
### 호환성

&lt;declare cursor&gt; 구문은 SQL 표준과 비교하여 다음과 같은 차이가 있다.

- SQL 표준의 &lt;cursor sensitivity&gt; 기본값은 ASENSITIVE이지만, GOLDILOCKS의 기본값은 INSENSITIVE이다. 
- SQL 표준에서는 다음과 같은 &lt;odbc cursor type&gt;을 다루지 않고 있다. 
    - STATIC CURSOR 
    - KEYSET CURSOR 
- SQL 표준의 &lt;cursor holdability&gt; 기본값은 WITHOUT HOLD이지만, GOLDILOCKS의 기본값은 &lt;cursor updatability&gt;에 따라 다르다. 
- SQL 표준에서는 &lt;cursor query&gt;로 &lt;select statement&gt;만 사용할 수 있지만, GOLDILOCKS는 다음과 같은 returning query를 사용할 수 있다. 
    - [INSERT INTO name RETURNING](20-sql-references-h-z.md#b7be21943ea082ab)
    - [UPDATE name RETURNING](20-sql-references-h-z.md#cba95fe5c27e5189)
    - [DELETE FROM name RETURNING](#fdf991741942b8a1)
- SQL 표준의 &lt;cursor updatability&gt; 기본값은 &lt;select statement&gt;에 따라 결정되지만, GOLDILOCKS의 기본값은 FOR READ ONLY이다. 
- SQL 표준에는 &lt;lock wait mode&gt; 구문이 존재하지 않는다.

**SQL 표준 호환성**

<a id="12f99e0f290e9b70"></a>
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

<a id="55fb8cb19ca294cd"></a>
### 참조

관련 내용은 다음을 참조한다.

- [OPEN cursor_name](20-sql-references-h-z.md#6047f0ea5db92a56)
- [FETCH cursor_name](#1662729a681bc4cc)
- [CLOSE cursor_name](#b7cf28b5122d5efa)
- [PREPARE statement_name](20-sql-references-h-z.md#15a93f4582b0cd5f)
- [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5)
- [SELECT .. FOR UPDATE](20-sql-references-h-z.md#efdca3ec1b8b28d9)
- [INSERT INTO name RETURNING](20-sql-references-h-z.md#b7be21943ea082ab)
- [UPDATE name RETURNING](20-sql-references-h-z.md#cba95fe5c27e5189)
- [DELETE FROM name RETURNING](#fdf991741942b8a1)

<a id="e74baad76dc01616"></a>
## DELETE FROM

<a id="8cba6409c1acb7fd"></a>
### 기능

테이블의 row들을 삭제한다.

<a id="821f08d428c1e743"></a>
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

<a id="24e4e0cdcd71545d"></a>
### 사용 범위 및 접근 권한

&lt;delete statement: searched&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블에 대해 (DELETE 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (DELETE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DELETE ANY TABLE ON DATABASE

<a id="3db0bdabae6192a8"></a>
### 구문 규칙 및 파라미터

<a id="ea29dde786ae6d90"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="0eb6272b015927d0"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="0f97a0be86937e5e"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 삭제한다.  
WHERE 조건을 명시하지 않은 경우, 모든 row를 삭제한다.  
WHERE 조건의 자세한 내용은 [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5) 구문의 [where clause](20-sql-references-h-z.md#18a0f95903788200)를 참조한다.

<a id="a67655784787ec83"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5) 구문의 [offset limit clause](20-sql-references-h-z.md#d71e29f430201f4a)를 참조한다.

<a id="a4f0f6951dd82136"></a>
#### &lt;fetch limit clause&gt;

Fetch 할 row의 개수를 명시하는 구문으로써 다음 두 가지 방법이 사용된다.

- &lt;fetch first clause&gt;
    - Fetch 할 row의 개수를 명시한다.
    - 자세한 내용은 [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5) 구문의 [&lt;fetch first clause&gt;](20-sql-references-h-z.md#25f7fd8f4c4446be)를 참조한다.
- &lt;limit clause&gt;
    - Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
    - 자세한 내용은 [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5) 구문의 [&lt;limit clause&gt;](20-sql-references-h-z.md#4e4ec2179ea01277)를 참조한다.

<a id="8562f9dcfce6b366"></a>
### 설명

<a id="c0746351ce80bbe2"></a>
#### DELETE 관련 구문들의 차이점

- [DELETE FROM](#e74baad76dc01616)
    - 조건에 부합하는 다수의 row를 삭제한다. 
    - 예: DELETE FROM t1 WHERE c1 = 0; 
- [DELETE FROM name WHERE CURRENT OF cursor_name](#3c267e8e7d7ca8c9)
    - Cursor가 현재 가리키는 row를 삭제한다. 
    - 예: DELETE FROM t1 WHERE CURRENT OF cursor; 
- [DELETE FROM name RETURNING](#fdf991741942b8a1)
    - 조건에 부합하는 다수의 row를 삭제하며, [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5) 구문과 동일한 방식( SQLFetch() 등의 API )으로 삭제한 row들을 검색할 수 있다. 
    - 예: DELETE FROM t1 WHERE c1 = 0 RETURNING c2; 
- [DELETE FROM name RETURNING .. INTO](#0f38e9dfac27052e)
    - 한 건 이하의 row를 삭제할 수 있으며, 삭제한 row가 한 건일 경우 RETURNING INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: DELETE FROM t1 WHERE c1 = 0 RETURNING c2 INTO :v1;

<a id="28e0f06da14f2bc2"></a>
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

<a id="8376d90a8a97b789"></a>
### 호환성

SQL 표준은 DELETE 구문에서 다음 절을 정의하지 않고 있다.

- &lt;result offset clause&gt; 
- &lt;fetch limit clause&gt;

**SQL 표준 호환성**

<a id="a712fca7f36ca3e3"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="106c9a7135fa2ba1"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DELETE FROM name WHERE CURRENT OF cursor_name](#3c267e8e7d7ca8c9)
- [DELETE FROM name RETURNING](#fdf991741942b8a1)
- [DELETE FROM name RETURNING .. INTO](#0f38e9dfac27052e)
- [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5)

<a id="fdf991741942b8a1"></a>
## DELETE FROM name RETURNING

<a id="eebeb0cc7f9b0625"></a>
### 기능

테이블의 row들을 삭제하고, 삭제한 row들을 검색한다.

<a id="ff0a4d6160367be1"></a>
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

<a id="ddf855a09eea526a"></a>
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

<a id="12e1f2a52a8b537b"></a>
### 구문 규칙 및 파라미터

<a id="a67507fa2c7fc272"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.

<a id="89fa5b0c58b955d9"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="7e4a9f64c7d9d208"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 삭제한다.  
자세한 내용은 [DELETE FROM](#e74baad76dc01616) 구문을 참조한다.

<a id="86e0ad7ff557d342"></a>
#### &lt;result offset clause&gt;

질의 결과 중에 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#e74baad76dc01616) 구문을 참조한다.

<a id="fbe1d5b2b59b98dd"></a>
#### &lt;fetch first clause&gt;

Fetch 할 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#e74baad76dc01616) 구문을 참조한다.

<a id="d7007da8a7317477"></a>
#### &lt;limit clause&gt;

Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.  
자세한 내용은 [DELETE FROM](#e74baad76dc01616) 구문을 참조한다.

<a id="44f923c20ae7b4d6"></a>
#### &lt;returning clause&gt;

삭제된 row들을 결과 집합으로 하고, 이들 중에서 검색할 column을 기술한다.

- RETURNING 절은 DELETE 구문으로 삭제된 row들을 result set으로 하는 결과를 반환한다. 
- &lt;value expression&gt; 
    - SELECT 구문의 &lt;select list&gt;와 동일하지만 aggregation 등을 사용할 수 없다. 
- [[AS] alias_name] 
    - AS 절을 이용해 value expression의 이름을 지정할 수 있다.

RETURN과 RETURNING은 동일한 의미의 키워드이다.

<a id="2fde14b8709b0c87"></a>
### 설명

자세한 내용은 [DELETE 관련 구문들의 차이점](#c0746351ce80bbe2)을 참조한다.

<a id="4881fd05a55685e0"></a>
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

<a id="b2c3fa1f59e77e3e"></a>
### 호환성

SQL 표준에는 &lt;delete returning query statement&gt; 구문이 존재하지 않는다.

<a id="9ef79bc5bfe2b602"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DELETE FROM](#e74baad76dc01616)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#3c267e8e7d7ca8c9)
- [DELETE FROM name RETURNING .. INTO](#0f38e9dfac27052e)
- [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5)

<a id="0f38e9dfac27052e"></a>
## DELETE FROM name RETURNING .. INTO

<a id="13f91000f1fdf501"></a>
### 기능

테이블에서 row 하나를 삭제하고, 삭제한 row의 값을 호스트 변수에 얻어온다.

<a id="b702a7f16e171b21"></a>
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

<a id="94af9543fc91120f"></a>
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

<a id="748f113172ed7a82"></a>
### 구문 규칙 및 파라미터

<a id="6770347d2d217d9a"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.

<a id="61c9f04b216dda7e"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="379aa16927c79405"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 삭제한다.  
자세한 내용은 [DELETE FROM](#e74baad76dc01616) 구문을 참조한다.

<a id="afbe60cf01630099"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#e74baad76dc01616) 구문을 참조한다.

<a id="33baa20dd3eab479"></a>
#### &lt;fetch first clause&gt;

Fetch 할 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#e74baad76dc01616) 구문을 참조한다.

<a id="c28b83473db9fdad"></a>
#### &lt;limit clause&gt;

Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.  
자세한 내용은 [DELETE FROM](#e74baad76dc01616) 구문을 참조한다.

<a id="b029a885f8d3b181"></a>
#### &lt;returning into clause&gt;

- RETURNING .. AS ..
    - [DELETE FROM name RETURNING](#fdf991741942b8a1) 구문의 returning clause를 참조한다.
- INTO variable_name [, ...]
    - INTO 절에 기술된 변수의 개수는 RETURNING 절에 기술된 expression의 개수와 동일해야 한다.

<a id="a316574a2928a724"></a>
### 설명

삭제할 row가 하나 이하여야 한다.   
둘 이상의 row가 삭제되면 에러가 발생한다.

자세한 내용은 [DELETE 관련 구문들의 차이점](#c0746351ce80bbe2)을 참조한다.

<a id="6602ce06d6176bea"></a>
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

<a id="015d26aed18755a1"></a>
### 호환성

SQL 표준에는 &lt;delete returning into statement&gt; 구문이 존재하지 않는다.

<a id="295e93b814811877"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DELETE FROM](#e74baad76dc01616)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#3c267e8e7d7ca8c9)
- [DELETE FROM name RETURNING](#fdf991741942b8a1)
- [SELECT](20-sql-references-h-z.md#8aabf2491a1309d5)

<a id="3c267e8e7d7ca8c9"></a>
## DELETE FROM name WHERE CURRENT OF cursor_name

<a id="57504e8b02e34755"></a>
### 기능

커서가 가리키는 row 하나를 삭제한다.

<a id="8f56a067c75a7207"></a>
### 구문

```
<delete statement: positioned> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        WHERE CURRENT OF cursor_name
    ;
```

<a id="179e03e1592a1e83"></a>
### 사용 범위 및 접근 권한

&lt;delete statement: positioned&gt; 구문을 수행하려면 사용자에게 [DELETE FROM](#e74baad76dc01616) 구문을 수행할 수 있는 권한이 있어야 한다.

<a id="5dc4ad75c1761821"></a>
### 구문 규칙 및 파라미터

<a id="25ef46ee44ecd63e"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.

<a id="99bb6ddfc0a948be"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="cf9d0c42fc2c7e3c"></a>
#### cursor_name

cursor_name에 해당하는 커서는 다음 조건을 만족해야 한다.

- OPEN 된 커서여야 한다. ([OPEN cursor_name](20-sql-references-h-z.md#6047f0ea5db92a56)을 참조한다.) 
- 커서를 이용해 FETCH 한 row가 존재해야 한다. ([FETCH cursor_name](#1662729a681bc4cc)을 참조한다.) 
- 커서를 위해 사용된 질의가 table_name을 식별할 수 있어야 한다. ([DECLARE cursor_name](#f41bd2e5b923c676)을 참조한다.) 
- table_name에 대해 갱신할 수 있는 커서여야 한다. ([DECLARE cursor_name](#f41bd2e5b923c676)을 참조한다.)

<a id="2edc827241ad8caa"></a>
### 설명

자세한 내용은 [DELETE 관련 구문들의 차이점](#c0746351ce80bbe2)을 참조한다.

<a id="fdca92f3f8de5dc2"></a>
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

<a id="6b6a3197df0b64cd"></a>
### 호환성

**SQL 표준 호환성**

<a id="f03ecce3144057f2"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| S111 | ONLY in query expressions | X |
| B031 | Basic dynamic SQL | O |

<a id="210ba63f14c7ee4c"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#f41bd2e5b923c676)
- [OPEN cursor_name](20-sql-references-h-z.md#6047f0ea5db92a56)
- [FETCH cursor_name](#1662729a681bc4cc)
- [DELETE FROM](#e74baad76dc01616)
- [DELETE FROM name RETURNING](#fdf991741942b8a1)
- [DELETE FROM name RETURNING .. INTO](#0f38e9dfac27052e)

<a id="1aaa5b1766ff2d59"></a>
## DROP AUDIT POLICY

<a id="6b9353fabe01736f"></a>
### 기능

Audit policy를 제거한다.

<a id="d5d6c42db845e620"></a>
### 구문

```
<drop audit policy statement> ::= 
    DROP AUDIT POLICY [ IF EXISTS ] policy_name
;
```

<a id="1f9e19b85553ea7a"></a>
### 사용 범위 및 접근 권한

&lt;drop audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="7647f00b09720356"></a>
### 구문 규칙 및 파라미터

<a id="942ad57a58e806cc"></a>
#### IF EXISTS

policy_name이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="55ec698d7603b4df"></a>
#### policy_name

제거할 audit policy 객체의 이름이다.

<a id="302fa73088fb63e8"></a>
### 설명

이미 활성화된 audit policy 객체는 제거할 수 없다. 이 경우, NOAUDIT POLICY 구문을 이용해 audit policy를 비활성화해야 한다.

<a id="4d31a6fffdcb4c41"></a>
### 사용 예

다음은 audit policy를 제거하는 예이다.

```
DROP AUDIT POLICY policy_table;
```

<a id="e4cb5753aea9008c"></a>
### 호환성

SQL 표준에는 audit policy가 존재하지 않는다.

<a id="fdfcd2f8e4273f8e"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#72600ff3c559dfb5)
    - [DROP AUDIT POLICY](#1aaa5b1766ff2d59)
    - [ALTER AUDIT POLICY](18-sql-references-a-b.md#00bbcaab72bbb158)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](18-sql-references-a-b.md#213cd4dbcc8bc668)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#15b6d2d5678734fb)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#18a54cc95a024f6e)

- Audit trail 소거: [ALTER DATABASE CLEAR AUDIT TRAIL](18-sql-references-a-b.md#7098d8b3ccdebf40)

<a id="8bcf309cea211dc8"></a>
## DROP CLUSTER GROUP

<a id="6cb7951d7e8ee406"></a>
### 기능

Cluster group을 cluster system에서 제거한다.

<a id="6dca7a85253da4df"></a>
### 구문

```
<drop cluster group statement> ::=
    DROP CLUSTER GROUP [IF EXISTS] group_name
    ;
```

<a id="71e1248ca84c0f14"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.   
&lt;drop cluster group statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="e2aa24aa2f365726"></a>
### 구문 규칙 및 파라미터

<a id="eb1d3cbe61480fa8"></a>
#### [IF EXISTS]

Cluster group이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="9f448a0e69ed4371"></a>
#### group_name

Cluster group의 이름이다.   
Shard가 존재하지 않는 cluster group을 제거할 수 있다.

<a id="d9640d896441eb17"></a>
### 설명

Cluster group을 제거하더라도 data loss가 발생하지 않는 경우에 해당 cluster group을 제거할 수 있다.  
단, global coordinator를 포함하는 group을 제거하려 할 경우, 에러가 발생할 수 있다.

<a id="623d3a0433aa6c78"></a>
### 사용 예

다음은 cluster group을 제거하는 예이다.

```
gSQL> DROP CLUSTER GROUP g3;

Cluster Group dropped.
```

<a id="762b668a5c607088"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="e88e69c1f2ae4e4f"></a>
### 참조

관련 내용은 [CREATE CLUSTER GROUP](#8e2b3a3076fcfb3e)을 참조한다.

<a id="28783969fbe8714a"></a>
## DROP CLUSTER LOCATION

<a id="4c4cfb3e646b1a6c"></a>
### 기능

Cluster member의 접속 정보를 삭제한다.

<a id="3c1117d9f35ee361"></a>
### 구문

```
<drop cluster location statement> ::=
    DROP CLUSTER LOCATION member_name 
    ;
```

<a id="592a122f295b4228"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.   
&lt;drop cluster location statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="eb108c966592fd6e"></a>
### 구문 규칙 및 파라미터

<a id="9bd8505448ba492c"></a>
#### member_name

Cluster member의 이름이다.   
등록된 cluster location 정보에 동일한 cluster member 이름이 존재해야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="729e8d80e5a6e27a"></a>
### 설명

기본적으로 cluster location 정보는 cluster group을 생성할 때나 cluster member를 추가할 때 제공되는 접속 정보를 이용하여 자동으로 생성된다. 생성된 정보는 cluster member나 group을 삭제할 때 함께 삭제된다.

만약 cluster location의 접속 정보가 변경되면 cluster member을 삭제하거나 재생성할 필요없이 [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#ba7b493d6f702d6f) 을 이용하여 접속 정보를 변경할 수 있다.

<a id="73f65b53e8dca56d"></a>
### 사용 예

```
gSQL> 
DROP CLUSTER LOCATION g1n2
;

Created
```

<a id="edd3b85b2f4353f2"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="9a606d21567a2dbf"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER LOCATION](#677b16ec3653271c)
- [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#ba7b493d6f702d6f)

<a id="f6216a28e7e3e011"></a>
## DROP INDEX

<a id="52f7c739c5d56ecc"></a>
### 기능

인덱스를 제거한다.

<a id="9f1c2b26772fc600"></a>
### 구문

```
<drop index statement> ::=
    DROP INDEX [ IF EXISTS ] index_name
    ;
```

<a id="22d086c3f28ab0ec"></a>
### 사용 범위 및 접근 권한

&lt;drop index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (DROP INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY INDEX ON DATABASE

<a id="5f7ff1d78fb663cf"></a>
### 구문 규칙 및 파라미터

<a id="f80846a3a0403f78"></a>
#### IF EXISTS

인덱스가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="987345cfa77e8d67"></a>
#### index_name

삭제할 인덱스의 이름이다.   
schema_name.index_name과 같이 인덱스가 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

UNIQUE 제약 조건, PRIMARY KEY 제약 조건을 위해 생성한 인덱스는 제거할 수 없다.  
위 제약 조건을 위해 생성된 인덱스를 제거하려면 [ALTER TABLE name DROP CONSTRAINT](18-sql-references-a-b.md#e1b50caa384abdca) 구문을 사용하여 관련된 제약 조건을 삭제해야 한다.

<a id="7b0bb28c80641244"></a>
### 설명

DROP INDEX와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="70871f5a60b512bf"></a>
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

<a id="32301fe61031b1f9"></a>
### 호환성

SQL 표준에서는 인덱스에 대한 개념을 다루지 않고 있다.

<a id="93b8f699f66bd04e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](#8e0637af857026b6)
- [DROP TABLE](#a964ea8a5781b06d)
- [ALTER TABLE name DROP CONSTRAINT](18-sql-references-a-b.md#e1b50caa384abdca)

<a id="4a92f0bfc9e51c58"></a>
## DROP PROFILE

<a id="fe69b9b9f4940ae2"></a>
### 기능

Profile을 삭제한다.

<a id="cb8c528ebc54e998"></a>
### 구문

```
<drop profile statement> ::= 
    DROP PROFILE [ IF EXISTS ] profile_name [ CASCADE ] ;
```

<a id="5908baa8f2ad9266"></a>
### 사용 범위 및 접근 권한

&lt;drop profile statement&gt; 구문을 수행하려면 사용자에게 DROP PROFILE ON DATABASE 권한이 있어야 한다.

<a id="6d94fb8245516678"></a>
### 구문 규칙 및 파라미터

<a id="750a2f5d4e739eef"></a>
#### IF EXISTS

Profile이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="f178598a980cb65f"></a>
#### profile_name

삭제할 profile의 이름을 명시한다.   
DEFAULT profile은 삭제할 수 없다.

<a id="9fed37e692e260f6"></a>
#### CASCADE

이미 할당받은 사용자들이 존재하는 경우, profile을 삭제하기 위해 반드시 이 절을 명시해야 한다.   
삭제할 profile을 할당받은 사용자들의 profile은 DEFAULT profile로 변경한다.

<a id="e3487901c1024264"></a>
### 사용 예

다음은 CASCADE 구문을 사용하여 profile을 삭제하는 예이다.

```
gSQL> DROP PROFILE prof CASCADE;

Profile dropped.

gSQL> COMMIT;

Commit complete.
```

<a id="2d79a67753c31588"></a>
### 호환성

SQL 표준에서는 profile에 대한 개념을 다루지 않고 있다.

<a id="91355b4093cd84cf"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE PROFILE](#f421f468f014cc7b)
- [ALTER PROFILE](18-sql-references-a-b.md#e94dd9982f8bc8d7)

<a id="e0d28b672c65ac71"></a>
## DROP SCHEMA

<a id="fcd93b794b483760"></a>
### 기능

스키마를 제거한다.

<a id="caa5bd8b4280c745"></a>
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

<a id="6f4e39dad1655318"></a>
### 사용 범위 및 접근 권한

&lt;drop schema statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 스키마의 소유자 
- 해당 스키마에 대해 CONTROL SCHEMA ON SCHEMA 
- DROP SCHEMA ON DATABASE

<a id="6d9206835ff9795d"></a>
### 구문 규칙 및 파라미터

<a id="ead0cf5b7f9b0242"></a>
#### IF EXISTS

스키마가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="53aff909f705a30b"></a>
#### schema_name

제거할 스키마의 이름이다.   
단, database를 생성할 때 자동으로 생성되는 DICTIONARY_SCHEMA, INFORMATION_SCHEMA, PUBLIC과 같은 built-in 스키마는 제거할 수 없다.

<a id="8ce6ad8d0e1f00f4"></a>
#### &lt;drop behavior&gt;

- RESTRICT 
    - Schema 내에 존재하는 객체가 없어야 한다. 
- CASCADE 
    - Schema 내의 모든 객체를 함께 제거한다.
- 생략할 경우, 기본값은 RESTRICT이다.

<a id="d96964d7d2884a88"></a>
### 설명

DROP SCHEMA와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다. 이 때, 제거하는 스키마에 포함된 휴지통 객체들도 제거된다.

<a id="f5e65d9fdab37568"></a>
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

<a id="7665c62a693dba46"></a>
### 호환성

SQL 표준에서는 IF EXISTS 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="3b1cfabc8534c482"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |
| F381 | Extended schema manipulation | O |

<a id="72488e26574bcbb8"></a>
### 참조

관련 내용은 [CREATE SCHEMA](#e1a750bc16ba12f6)를 참조한다.

<a id="4693b77a7e62cf8a"></a>
## DROP SEQUENCE

<a id="2f1d7ec5ed1b8c0f"></a>
### 기능

시퀀스를 제거한다.

<a id="1306f93ab5348a7f"></a>
### 구문

```
<drop sequence generator statement> ::=
    DROP SEQUENCE [ IF EXISTS ] [schema_name.] sequence_name 
    ;
```

<a id="5bb6b65ecaabf9ce"></a>
### 사용 범위 및 접근 권한

&lt;drop sequence generator statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 시퀀스의 소유자 
- 시퀀스가 속한 스키마에 대해 (DROP SEQUENCE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY SEQUENCE ON DATABASE

<a id="17084d16b0302bca"></a>
### 구문 규칙 및 파라미터

<a id="1308a12aa9aa9a9b"></a>
#### IF EXISTS

시퀀스가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="e50ff5ed328a5d30"></a>
#### sequence_name

제거할 시퀀스의 이름이다.   
schema_name.sequence_name과 같이 시퀀스가 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="1faf0f3dfa4598fe"></a>
### 설명

DROP SEQUENCE와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="9811fd63c599cae1"></a>
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

<a id="056441b889ce9549"></a>
### 호환성

SQL 표준에서는 IF EXISTS 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="a360d72af23bf04f"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="42dd1b6f22f35d11"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE SEQUENCE](#0466abe24a740737)
- [ALTER SEQUENCE](18-sql-references-a-b.md#3df2c32d366ffd24)

<a id="140ff3d497836df4"></a>
## DROP SYNONYM

<a id="8e0fc12b4c2a31b1"></a>
### 기능

Synonym을 제거한다.

<a id="3066d0b8420e7bb2"></a>
### 구문

```
<drop synonym statement> ::=
    DROP [ PUBLIC ] SYNONYM [ IF EXISTS ] [schema_name.]synonym_name
    ;
```

<a id="ac46a7aa1b1fa113"></a>
### 사용 범위 및 접근 권한

PUBLIC을 명시하여 public synonym을 제거하려면 DROP PUBLIC SYNONYM ON DATABASE 권한이 있어야 한다.

Private synonym을 제거하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 synonym의 소유자 
- Synonym이 속한 스키마에 대해 (DROP SYNONYM 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY SYNONYM ON DATABASE

<a id="19d941162e859f3a"></a>
### 구문 규칙 및 파라미터

<a id="9f10d880eca2dd38"></a>
#### [ PUBLIC ]

Public synonym을 제거하고자 할 때 명시한다.   
이 절을 생략하면 private synonym이 제거된다.

<a id="2a83ca8b97c74ab8"></a>
#### IF EXISTS

Synonym이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="56973907d8c9367d"></a>
#### synonym_name

제거할 synonym의 이름이다.  
schema_name.synonym_name과 같이 synonym이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
PUBLIC을 명시한 경우, 스키마 이름을 명시할 수 없다.

<a id="741f589fc6371393"></a>
### 설명

DROP SYNONYM과 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="8a3877e5ff188608"></a>
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

<a id="57100ddd0e3a102d"></a>
### 호환성

SQL 표준에서는 DROP SYNONYM 구문을 정의하지 않고 있다.

<a id="12d02976c2b2afe0"></a>
### 참조

관련 내용은 [CREATE SYNONYM](#734a2d8ce3896204)을 참조한다.

<a id="a964ea8a5781b06d"></a>
## DROP TABLE

<a id="1b9dbf414c3d4e62"></a>
### 기능

테이블을 제거한다.

> 휴지통 기능이 활성화되어 있을 경우, 테이블이 즉시 제거되지 않고 휴지통에 보관된다.

<a id="6b13fd4ca2b3ac22"></a>
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

<a id="3fbf543616a0905a"></a>
### 사용 범위 및 접근 권한

&lt;drop table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블의 소유자 
- 해당 테이블에 대해 CONTROL TABLE ON TABLE 
- 테이블이 속한 스키마에 대해 (DROP TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY TABLE ON DATABASE

<a id="24f91986233df076"></a>
### 구문 규칙 및 파라미터

<a id="12dc88c133679470"></a>
#### IF EXISTS

테이블이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="3c3689f1583ef49f"></a>
#### table_name

제거할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

Database를 생성할 때 자동으로 생성되는 다음과 같은 테이블들은 삭제할 수 없다.

- DEFINITION_SCHEMA 스키마의 테이블들 
- FIXED_TABLE_SCHEMA 스키마의 테이블들

테이블에 생성된 제약 조건과 인덱스도 함께 제거한다.

<a id="72132afd4568ce12"></a>
#### drop behavior

현재는 RESTRICT/ CASCADE가 동일하게 동작한다.   
생략할 경우, 기본값은 RESTRICT 이다.

<a id="ac4e5dc489961a25"></a>
#### purge

휴지통 기능이 활성화된 경우에도 테이블을 휴지통에 보관하지 않고 즉시 제거한다.

<a id="83ba3e38ae4b7f46"></a>
### 설명

DROP TABLE과 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="b1bb107f75c84d39"></a>
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

<a id="8c515a6396a3ce40"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- IF EXISTS 
- CASCADE CONSTRAINTS

**SQL 표준 호환성**

<a id="36b57a096760021a"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |

<a id="2a6dae8cfe2de8c3"></a>
### 참조

관련 내용은 [CREATE TABLE](#66fde705300657e5)을 참조한다.

<a id="0ccb2cbcfd412a42"></a>
## DROP TABLESPACE

<a id="2175c0c4202ce617"></a>
### 기능

테이블스페이스를 제거한다.

<a id="0520c3eff0446cd1"></a>
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

<a id="2ee2b32a96aca8b6"></a>
### 사용 범위 및 접근 권한

&lt;drop tablespace definition&gt; 구문을 수행하려면 사용자에게 DROP TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="d2db180c1d247dd3"></a>
### 구문 규칙 및 파라미터

<a id="46ef2dc9d7a41cec"></a>
#### IF EXISTS

테이블스페이스가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="7a74572fde27b909"></a>
#### tablespace_name

제거할 테이블스페이스의 이름이다.

Database를 생성할 때 구축되는 다음과 같은 시스템 테이블스페이스는 제거할 수 없다.

- DICTIONARY_TBS: system tablespace for dictionary management 
- MEM_UNDO_TBS: system tablespace for default undo tablespace 
- MEM_DATA_TBS: system tablespace for default user data tablespace 
- MEM_TEMP_TBS: system tablespace for default temporary tablespace

> tablespace_name이 사용자들의 default tablespace로 사용되고 있었다면 tablespace가 제거된 후에는 객체를 위한 공간을 할당받을 수 없다. 따라서 tablespace를 제거한 후에 [ALTER USER](18-sql-references-a-b.md#648c7792f8549c18) 구문을 사용하여 사용자들의 default tablespace를 변경해 주어야 한다.

<a id="4e774003b0e01f83"></a>
#### INCLUDING CONTENTS

테이블스페이스에 속하는 객체 (table, index, key constraints)를 삭제한다. 테이블스페이스에 속하는 table을 참조하는 index와 key constraints가 테이블스페이스 외부에 존재할 경우에는 이들도 함께 삭제한다.

INCLUDING CONTENTS 구문을 사용하지 않을 경우에는 테이블스페이스에 속하는 객체가 없어야 한다.

<a id="7b8ec924c6eb8722"></a>
#### [ { AND | KEEP } DATAFILES ]

테이블스페이스를 구성하는 데이터 파일들을 함께 삭제할지 여부를 지정한다.   
Memory temporary tablespace에는 데이터 파일이 존재하지 않으므로, 해당 절은 무시된다.

- AND DATAFILES 
    - 데이터 파일들을 함께 삭제한다. 
- KEEP DATAFILES 
    - 데이터 파일을 삭제하지 않고 남겨둔다. 
- 명시하지 않을 경우, 기본값은 KEEP DATAFILES 이다.

<a id="e060122afa332f90"></a>
#### drop behavior

현재는 RESTRICT/ CASCADE가 동일하게 동작한다.   
생략할 경우, 기본값은 RESTRICT 이다.

<a id="8961120490cef027"></a>
### 설명

다른 Data Definition Language (DDL)과 달리 DROP TABLESPACE 구문은 ROLLBACK 할 수 없으며, 구문을 수행한 transaction이 자동으로 COMMIT 된다. 이 때 제거하는 테이블스페이스에 포함된 휴지통 객체들도 함께 제거된다.

<a id="cdf653bf8a74e065"></a>
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

<a id="0fbabbb48c7d3d39"></a>
### 호환성

SQL 표준은 tablespace에 대한 개념을 다루지 않고 있다.

<a id="977ceea52f46b6d9"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE MEMORY DATA TABLESPACE](#86993cea38f6279a)
- [CREATE MEMORY TEMPORARY TABLESPACE](#54c1cb4e7c65e722)
- [ALTER TABLESPACE](18-sql-references-a-b.md#7c3ae65b4798a999)

<a id="a6f0bdba7a87d9c4"></a>
## DROP USER

<a id="b005e8b23eb0de6f"></a>
### 기능

데이터베이스 사용자를 제거한다.

<a id="16e382240d413b58"></a>
### 구문

```
<drop user statement> ::=
    DROP USER [ IF EXISTS ] user_identifier [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
```

<a id="70c864f97269077a"></a>
### 사용 범위 및 접근 권한

&lt;drop user statement&gt; 구문을 수행하려면 사용자에게 DROP USER ON DATABASE 권한이 있어야 한다.

> user_identifier가 소유한 스키마가 존재하지 않아야 한다.  
> 스키마 제거에 대한 자세한 내용은 [DROP SCHEMA](#e0d28b672c65ac71) 구문을 참조한다.

<a id="09318eb4f4b473ac"></a>
### 구문 규칙 및 파라미터

<a id="9ee10f7b33afdac2"></a>
#### IF EXISTS

사용자가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="0f5c6dbb9294a1c6"></a>
#### user_identifier

제거할 데이터베이스 사용자의 이름이다.   
단, database를 생성할 때 자동으로 생성되는 "SYS" 등과 같은 사용자는 제거할 수 없다.

다음과 같이 user_identifier가 생성했으나, 소유자가 아닌 객체는 제거하지 않는다.

- Role 
- Tablespace

<a id="3e491b0e3e95b58e"></a>
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

<a id="17d22d65dafaab2a"></a>
### 설명

GOLDILOCKS에서 user와 schema의 관계는 1 : N 이다.  
즉, user가 schema를 소유하지 않을 수도 있고, 다수의 schema를 소유할 수도 있다.

User 객체를 제거하려면 user가 소유한 모든 schema를 제거해야 한다. 이 때, 제거하는 user 객체의 휴지통 객체들도 함께 제거된다.

<a id="232139ba15f92a35"></a>
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

<a id="c5eb5c1f07a4c2ca"></a>
### 호환성

SQL 표준에서는 user의 개념은 다루고 있지만 user의 생성 및 제거와 관련된 SQL 구문은 정의하지 않고 있다.

<a id="7b262ac2cf7ef335"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE USER](#f516f713c62659c7)
- [ALTER USER](18-sql-references-a-b.md#648c7792f8549c18)
- [DROP SCHEMA](#e0d28b672c65ac71)

<a id="9ad6c24b5f2fb86f"></a>
## DROP VIEW

<a id="3a4d287d79aec9a7"></a>
### 기능

View를 제거한다.

<a id="59bae063733013cc"></a>
### 구문

```
<drop view statement> ::=
    DROP VIEW [ IF EXISTS ] view_name
    ;
```

<a id="4fb5ef289bc7ae37"></a>
### 사용 범위 및 접근 권한

&lt;drop view statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 view의 소유자 
- 해당 view에 대해 CONTROL TABLE ON TABLE 
- View가 속한 스키마에 대해 (DROP VIEW 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY VIEW ON DATABASE

<a id="75310dfd8988f47a"></a>
### 구문 규칙 및 파라미터

<a id="533c3838a3ff6dcf"></a>
#### IF EXISTS

View가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="3dc44434c9f6a9dc"></a>
#### view_name

제거할 view의 이름이다.   
schema_name.view_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="d8105ca63b32e956"></a>
### 설명

DROP VIEW와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="f0b7f52946cfdddc"></a>
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

<a id="3263ef300f33587e"></a>
### 호환성

SQL 표준에서는 IF EXISTS 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="3a0b3da7124abd6a"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |

<a id="a8a923e3648facf0"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE VIEW](#c6a48c56234057a1)
- [ALTER VIEW](18-sql-references-a-b.md#a1de7597c5662129)

<a id="f6203088a925d605"></a>
## EXECUTE IMMEDIATE 'sql_string'

<a id="8e9b80aee0c80c65"></a>
### 기능

프로그램 작성 시점에 정의되지 않았던 dynamic SQL 문장을 수행한다.

<a id="18bc1654619a2793"></a>
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

<a id="729904ad865ce67c"></a>
### 사용 범위 및 접근 권한

Embedded SQL에서 사용할 수 있다.   
Dynamic SQL 구문의 종류에 부합하는 수행 권한이 있어야 한다.

<a id="29195a15529547c9"></a>
### 구문 규칙 및 파라미터

<a id="095f501af59fb61e"></a>
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

<a id="f4b842f1e0e192cc"></a>
#### variable_name

variable_name에 대응되는 type은 character string이어야 한다.   
variable_name에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="1221441c2518eb76"></a>
#### sql statement

sql statement에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="25e82b5b0d0b54bb"></a>
### 설명

EXECUTE IMMEDIATE 'sql_string' 구문은 dynamic embedded SQL 응용 프로그램에서 host variable이 없는 non-query SQL에 사용될 수 있다. 별도의 준비과정이 필요하지 않기 때문에, DDL이나 DML 등을 일회성으로 수행하기에 적합하다.

자세한 내용은 [Embedded Dynamic SQL](../part-05-developer-manual/33-embedded-sql.md#3bcaf0db5a2e1afe)을 참조한다.

<a id="d5b5638500f96393"></a>
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

EXECUTE IMMEDIATE 'sql_string'이 사용된 전체 소스 코드는 [Dynamic Embedded SQL Example Program](../part-05-developer-manual/33-embedded-sql.md#07d8d62652087b23)에서 확인할 수 있다.

<a id="ca46c851ce7df93f"></a>
### 호환성

**SQL 표준 호환성**

<a id="c52dd3d2fbe88b35"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |

<a id="d9a0fb2ec60adda5"></a>
### 참조

관련 내용은 다음을 참조한다.

- [PREPARE statement_name](20-sql-references-h-z.md#15a93f4582b0cd5f)
- [EXECUTE statement_name](#308a84b7c4dcf6c7)
- [Embedded Dynamic SQL](../part-05-developer-manual/33-embedded-sql.md#3bcaf0db5a2e1afe)

<a id="308a84b7c4dcf6c7"></a>
## EXECUTE statement_name

<a id="8f315efa09137443"></a>
### 기능

준비된 statement를 수행한다.

<a id="a94e5e03dfdb2352"></a>
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

<a id="e930b8f607423b12"></a>
### 사용 범위 및 접근 권한

Embedded SQL에서 사용할 수 있다.   
Dynamic SQL 구문의 종류에 부합하는 수행 권한이 있어야 한다.

<a id="476fb25c005d6834"></a>
### 구문 규칙 및 파라미터

<a id="3a31d8dfec90c2a1"></a>
#### statement_name

준비된 statement의 이름이다.  
[PREPARE statement_name](20-sql-references-h-z.md#15a93f4582b0cd5f) 구문을 사용하여 statement_name을 준비해야 한다.

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

- [DECLARE cursor_name](#f41bd2e5b923c676)
- [OPEN cursor_name](20-sql-references-h-z.md#6047f0ea5db92a56)
- [FETCH cursor_name](#1662729a681bc4cc)
- [CLOSE cursor_name](#b7cf28b5122d5efa)

질의 결과가 없을 경우, NO DATA로 완료된다.

<a id="093b3301ead7a8e1"></a>
#### [ &lt;parameter using clause&gt; ] [ &lt;result into clause&gt; ]

&lt;parameter using clause&gt;와 &lt;result into clause&gt;는 순서에 관계없이 기술할 수 있지만 중복해서 기술하지 않아야 한다.

<a id="8ab55a10b1178c15"></a>
#### &lt;parameter using clause&gt;

statement_name이 참조하는 dynamic SQL 문장에 parameter가 존재할 경우, parameter에 대한 정보를 &lt;using parameter arguments&gt; 절로 명시한다.

<a id="2c004b61e906d757"></a>
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

<a id="8db8bc08465c760d"></a>
#### &lt;result into clause&gt;

statement_name이 참조하는 dynamic SQL 문장이 query일 경우, 결과 column에 대한 정보를 &lt;into result arguments&gt; 절로 명시한다.

결과값이 null인 경우, INDICATOR를 명시하지 않으면 [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] 에러가 발생한다.

<a id="817e0c8419d2ee52"></a>
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

<a id="57d635c21f844201"></a>
### 설명

statement_name은 embedded SQL 소스 코드에서 precompiler에게 statement를 알려주는 식별자로써 host variable이 아니기 때문에 별도의 type이나 선언이 필요하지 않다. EXECUTE statement_name 구문은 PREPARE statement_name 구문 뒤에 쓰여야 한다.

자세한 내용은 [Embedded Dynamic SQL](../part-05-developer-manual/33-embedded-sql.md#3bcaf0db5a2e1afe)을 참조한다.

<a id="7d9f4859c202ddd9"></a>
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

EXECUTE statement_name이 사용된 전체 소스 코드는 [Dynamic Embedded SQL Example Program](../part-05-developer-manual/33-embedded-sql.md#07d8d62652087b23)에서 확인할 수 있다.

<a id="58c41019736bcf22"></a>
### 호환성

**SQL 표준 호환성**

<a id="ca9595018da8c541"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic dynamic SQL | O |
| B032 | Extended dynamic SQL | X |

<a id="4e126e840505240f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [PREPARE statement_name](20-sql-references-h-z.md#15a93f4582b0cd5f)
- [DECLARE cursor_name](#f41bd2e5b923c676)
- [OPEN cursor_name](20-sql-references-h-z.md#6047f0ea5db92a56)
- [FETCH cursor_name](#1662729a681bc4cc)
- [CLOSE cursor_name](#b7cf28b5122d5efa)
- [Embedded Dynamic SQL](../part-05-developer-manual/33-embedded-sql.md#3bcaf0db5a2e1afe)

<a id="1662729a681bc4cc"></a>
## FETCH cursor_name

<a id="bbe84d76120c3e05"></a>
### 기능

커서를 결과 집합의 특정 row에 위치시키고, 해당 row의 값을 호스트 변수에 얻어온다.

<a id="64d4223138f59904"></a>
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

<a id="7495dad7426576c3"></a>
### 구문 규칙 및 파라미터

<a id="90ad92a980790665"></a>
#### [ FROM ] cursor_name

세션 내에서 open 된 커서이어야 한다.   
FROM은 생략할 수 있다.

<a id="c2d73dd10679b4ce"></a>
#### &lt;fetch orientation&gt;

FETCH NEXT 이외의 &lt;fetch orientation&gt;을 사용하려면 scrollable cursor를 사용해야 한다.   
&lt;fetch orientation&gt;을 생략할 경우, 기본값은 NEXT이다.

Open 된 커서는 결과 집합에 대해 아래 그림과 같은 커서 위치 정보를 갖는다.

<a id="d953f8ad9e3f8206"></a>
![커서의 위치 정보](../assets/images/68b8d90f6c9879cb.png)

**커서의 위치**

<a id="473703f16f2abe25"></a>
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

<a id="8719a0ea9b821056"></a>
#### &lt;result into clause&gt;

&lt;into result arguments&gt;를 사용하여 결과 column을 획득할 변수 정보를 기술한다.

결과값이 null 인 경우, INDICATOR를 명시하지 않으면 [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] 에러가 발생한다.

<a id="c1665862bf0cb437"></a>
#### &lt;into result arguments&gt;

INTO 절에 기술된 변수의 개수는 커서의 결과 집합의 column 개수와 동일해야 한다.

<a id="e48a3e51e3d328ae"></a>
### 설명

FETCH를 수행한 후에 커서 위치가 BEFORE THE FIRST ROW 거나 AFTER THE LAST LOW 인 경우, &lt;fetch orientation&gt;에 입력된 위치값에 관계없이 동일한 위치에 자리한다.

<a id="121175975e59d8e4"></a>
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

<a id="283649d58460358c"></a>
### 호환성

SQL 표준에서는 &lt;fetch orientation&gt; 중에 CURRENT를 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="6ac357a175a39487"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F431 | Read-only scrollable cursors | O |
| B031 | Basic dynamic SQL | O |

<a id="cdb804d1f31ff225"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#f41bd2e5b923c676)
- [OPEN cursor_name](20-sql-references-h-z.md#6047f0ea5db92a56)
- [CLOSE cursor_name](#b7cf28b5122d5efa)

<a id="5d9931bd0c2d4487"></a>
## FLASHBACK TABLE

<a id="794b13b1b5c6fde8"></a>
### 기능

휴지통에 보관되어 있는 테이블 객체를 복구한다.

<a id="270d9e50561757b7"></a>
### 구문

```
<flashback table statement> ::=
    FLASHBACK TABLE table_name
    TO BEFORE DROP [ RENAME TO new_table_name ]
    ;
```

<a id="67cdcc16ddce33e0"></a>
### 사용 범위 및 접근 권한

&lt;flashback table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블의 소유자 
- 해당 테이블에 대해 CONTROL TABLE ON TABLE 
- 테이블이 속한 스키마에 대해 (DROP TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY TABLE ON DATABASE

<a id="d4f1e9c9b4b3febf"></a>
### 구문 규칙 및 파라미터

<a id="7e9b650f7460a2dd"></a>
#### table_name

휴지통에 저장된 객체의 이름 또는 제거된 테이블의 이름이다.  
제거된 테이블 이름에는 schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="2261a8df1b067333"></a>
#### new_table_name

복구되는 테이블의 새로운 이름이다.  
스키마 내에 동일한 테이블 이름이 존재하지 않아야 한다.

<a id="f4bc31b3c5ca3404"></a>
### 설명

휴지통에 저장된 객체 이름이나 제거된 테이블의 이름을 사용하여 휴지통에 보관되어 있는 테이블 객체를 복구한다. 만약 제거된 테이블과 중복된 이름이 있는 경우 가장 최신의 테이블 객체를 복구한다.

복구하려는 테이블 객체의 이름이 존재하면 에러가 발생하는데 RENAME TO 절을 사용하여 새로운 테이블 이름으로 복구할 수 있다. 복구된 테이블의 제약 조건과 인덱스는 제거되기 전의 이름으로 복구되는데 만약 제거되기 전의 제약 조건 및 인덱스와 동일한 이름이 이미 존재할 경우, 휴지통에 저장된 이름으로 복구된다.

다른 Data Definition Language (DDL)과 달리 FLASHBACK TABLE 구문은 ROLLBACK 할 수 없으며, 구문을 수행한 transaction이 자동으로 COMMIT 된다.

<a id="b333b9a4c98f5e28"></a>
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

<a id="7794f46094a74fc9"></a>
### 호환성

SQL 표준에서는 &lt;flashback table statement&gt;를 다루지 않고 있다.

<a id="76d1d3093b0dd281"></a>
### 참조

관련 내용은 다음을 참조한다.

- [테이블 휴지통 관리](13-sql-objects.md#d3fa3a0647deb3e7)
- [PURGE](20-sql-references-h-z.md#52b106c8d22979cb)

<a id="71c467631eb14f4c"></a>
## GRANT privileges TO

<a id="24eee167fbcc81ed"></a>
### 기능

사용자에게 권한을 부여한다.

<a id="e08020c9f626b9fe"></a>
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

<a id="d67aa5d70ae87b99"></a>
### 구문 규칙 및 파라미터

<a id="7319275b24c17edb"></a>
#### &lt;grantee&gt;

권한을 부여받을 사용자이다.

- user_identifier 
    - 해당 사용자에게 권한을 부여한다
- PUBLIC 
    - 모든 사용자를 의미하는 authorization 객체이다.

<a id="bda63b9fa3ec7967"></a>
#### WITH GRANT OPTION

Grantee (권한을 부여받은 사용자)가 다른 사용자에게 해당 권한을 부여할 수 있도록 한다.

다음과 같이 동일한 &lt;privilege&gt;에 대한 권한을 부여할 때 WITH GRANT OPTION은 계속 유지된다.

- GRANT SELECT ON t1 TO u1 WITH GRANT OPTION; 
- GRANT SELECT ON t1 TO u1;

<a id="31020b5af2c92eec"></a>
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

<a id="5380bdccad1a1d10"></a>
#### &lt;database privilege&gt;

데이터베이스 객체에 대한 권한이다.  
[ON DATABASE] 구문은 생략할 수 있다.

database privilege로 정의할 수 있는 database action은 다음과 같다.

- ALL [ PRIVILEGES ] [ON DATABASE] 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 DATABASE에 대해 소유한 모든 권한이다.

**Database privilege**

<a id="b177424cd867f415"></a>
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

<a id="0b8860169f235967"></a>
#### &lt;tablespace privilege&gt;

테이블스페이스 객체에 대한 권한이다.

tablespace privilege로 정의할 수 있는 tablespace action은 다음과 같다.

- ALL [ PRIVILEGES ] ON TABLESPACE tablespace_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 TABLESPACE에 대해 소유한 모든 권한이다.

**Tablespace privilege**

<a id="cb91eb6b6da164d5"></a>
| &lt;tablespace action&gt; | 설명 |
| --- | --- |
| CREATE OBJECT | Tablespace에 객체를 생성할 수 있는 권한 |

<a id="44834e7fe60ac953"></a>
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

<a id="368db4ca02409a5f"></a>
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

<a id="6b3a4237ef8ac821"></a>
#### &lt;table privilege&gt;

테이블 또는 view 객체에 대한 권한이다.  
[TABLE] 구문은 생략할 수 있다.

table privilege로 정의할 수 있는 table action은 다음과 같다.

- ALL [ PRIVILEGES ] ON [TABLE] table_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 TABLE에 대해 소유한 모든 권한이다.

**Table privilege**

<a id="9483d5694e05107f"></a>
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

<a id="4d6769545ee544a2"></a>
| &lt;column action&gt; | 설명 |
| --- | --- |
| SELECT (columns) | 해당 column들을 검색할 수 있는 권한 |
| INSERT (columns) | 해당 column들을 포함한 row를 생성할 수 있는 권한 |
| UPDATE (columns) | 해당 column들을 갱신할 수 있는 권한 |
| REFERENCES (columns) | 해당 column들을 참조하는 참조 제약 조건을 생성할 수 있는 권한 |

<a id="63fd66c28f263bee"></a>
#### &lt;sequence privilege&gt;

시퀀스 객체에 대한 권한이다.

sequence privilege로 정의할 수 있는 sequence action은 다음과 같다.

- ALL [ PRIVILEGES ] ON SEQUENCE sequence_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 SEQUENCE에 대해 소유한 모든 권한이다.

**Sequence privilege**

<a id="593ced82380a1238"></a>
| &lt;sequence action&gt; | 설명 |
| --- | --- |
| USAGE | 시퀀스를 사용할 수 있는 권한 |

<a id="98a01b79f59f2d7f"></a>
#### &lt;procedure privilege&gt;

Procedure/ function 객체에 대한 권한이다.

procedure privilege로 정의할 수 있는 action은 다음과 같다.

- ALL [ PRIVILEGES ] ON PROCEDURE procedure_name 
    - WITH GRANT OPTION을 사용하여 grantor (구문을 수행하는 사용자)에게 부여된 해당 procedure/ function에 대한 모든 권한이다.

**Procedure privilege**

<a id="c1edf6cb90db1b18"></a>
| &lt;procedure action&gt; | 설명 |
| --- | --- |
| EXECUTE | Procedure/ function을 실행할 수 있는 권한 |

<a id="75d5c9b3c3a02680"></a>
#### &lt;package privilege&gt;

Package 객체에 대한 권한이다.

package privilege로 정의할 수 있는 action은 다음과 같다.

- ALL [ PRIVILEGES ] ON PACKAGE package_name 
    - WITH GRANT OPTION을 사용하여 grantor (구문을 수행하는 사용자)에게 부여된 해당 package에 대한 모든 권한이다.

**Package privilege**

<a id="028f1a4a4e56db9e"></a>
| &lt;package action&gt; | 설명 |
| --- | --- |
| EXECUTE | Package를 실행할 수 있는 권한 |

<a id="a88f9a48d4683ca2"></a>
### 설명

GRANT privilege와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

Table, sequence 등과 같은 SQL schema object를 생성한 owner는 해당 객체에 대한 권한을 별도로 부여받지 않더라도 일정한 권한을 가진다.   
이에 대한 자세한 설명은 다음과 같은 CREATE 구문을 참조한다.

- [CREATE TABLE](#66fde705300657e5)
- [CREATE VIEW](#c6a48c56234057a1)
- [CREATE SEQUENCE](#0466abe24a740737)
- [ALTER TABLE name ADD COLUMN](18-sql-references-a-b.md#9c4e0674f148ec34)
- [CREATE FUNCTION](../part-04-psm-manual/29-psm-sql-references.md#b61457de314b7c25)
- [CREATE PROCEDURE](../part-04-psm-manual/29-psm-sql-references.md#40ffb9d35e667f94) 
- [CREATE PACKAGE](../part-04-psm-manual/29-psm-sql-references.md#0d9d8dee923fa8cc)

Schema, tablespace 등과 같은 non-schema object를 생성한 owner에는 해당 객체에 대한 어떤 권한도 자동으로 부여되지 않으므로 별도의 권한을 부여받아야 한다.   
자세한 설명은 다음과 같은 CREATE 구문을 참조한다.

- [CREATE SCHEMA](#e1a750bc16ba12f6)
- [CREATE TABLESPACE](#9425404264bb2534)
- [CREATE USER](#f516f713c62659c7)

<a id="6295a25be66daa17"></a>
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

<a id="ea2c53459d22cd18"></a>
### 호환성

SQL 표준에서는 다음 privilege들을 정의하지 않고 있다.

- &lt;database privilege&gt; 
- &lt;tablespace privilege&gt; 
- &lt;schema privilege&gt;

**SQL 표준 호환성**

<a id="8f5fd4b99ede930d"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| S023 | Basic structured types | X |
| S024 | Enhanced structured types | X |
| S081 | Subtables | X |
| T211 | Basic trigger capability | X |
| T281 | SELECT privilege with column granularity | O |
| T332 | Extended Roles | X |
| F731 | INSERT column privileges | O |

<a id="d0f519546983986c"></a>
### 참조

관련 내용은 다음을 참조한다.

- [REVOKE privileges FROM](20-sql-references-h-z.md#ce8d81642df96287)
- [CREATE USER](#f516f713c62659c7)
- [DROP USER](#a6f0bdba7a87d9c4)
- [ALTER USER](18-sql-references-a-b.md#648c7792f8549c18)

---

[← 18. SQL References (A~B)](18-sql-references-a-b.md) · [전체 목차](../README.md) · [20. SQL References (H~Z) →](20-sql-references-h-z.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
