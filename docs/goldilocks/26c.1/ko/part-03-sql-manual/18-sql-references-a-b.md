<a id="7e5e0c9e12e61d15"></a>

# 18. SQL References (A~B)

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/7e5e0c9e12e61d15)  
> 태그: `26c.1_0_tag`

[← 17. Built-in Function References](17-built-in-function-references.md) · [전체 목차](../README.md) · [19. SQL References (C~G) →](19-sql-references-c-g.md)

<a id="e6d664ed42cb125a"></a>
## ALTER AUDIT POLICY

<a id="d8fd8ab1a34b5ff4"></a>
### 기능

Audit policy 객체에 감사 대상을 추가하거나 삭제한다.

<a id="9b09cbbafe608920"></a>
### 구문

```
<alter audit policy statement> ::= 
    ALTER AUDIT POLICY policy_name
    { <add_audit_option> | <drop_audit_option> }
    ;

<add_audit_option> ::=
    ADD { <privilege_audit_clause> | <role_audit_clause> | <action_audit_clause> } [, ...]

<drop_audit_option> ::=
    DROP { <privilege_audit_clause> | <role_audit_clause> | <action_audit_clause> } [, ...]


<privilege_audit_clause> ::=
    PRIVILEGES <database_privilege> [, ...]

<role_audit_clause> ::=
    ROLES <role_name> [, ...]

<action_audit_clause> ::=
    ACTIONS { <object_action_audit> | <system_action_audit> } [, ...]

<object_action_audit> ::=
      ALL ON [schema_name.]object_name
    | <object_action> ON [schema_name.]object_name

<system_action_audit> ::=
      ALL
    | <system_action>
```

<a id="0005f830cd8dc10c"></a>
### 사용 범위 및 접근 권한

&lt;alter audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="6e2610d55402dcc7"></a>
### 구문 규칙 및 파라미터

<a id="83e889ebabd7f861"></a>
#### policy_name

변경할 audit policy 객체의 이름이다.

<a id="7ce3f65733c2b099"></a>
#### &lt;add_audit_option&gt;

Audit policy에 감사대상을 추가한다.

<a id="2f4e04ad23097276"></a>
#### &lt;drop_audit_option&gt;

Audit policy 감사대상에서 삭제한다.

<a id="e96621e9c3f8ceff"></a>
#### &lt;privilege_audit_clause&gt;

자세한 내용은 [CREATE AUDIT POLICY](19-sql-references-c-g.md#079c12405d0687f7)를 참조한다.

<a id="7de23c4ca346e198"></a>
#### &lt;role_audit_clause&gt;

자세한 내용은 [CREATE AUDIT POLICY](19-sql-references-c-g.md#079c12405d0687f7)를 참조한다.

<a id="890420654f5934c6"></a>
#### &lt;action_audit_clause&gt;

자세한 내용은 [CREATE AUDIT POLICY](19-sql-references-c-g.md#079c12405d0687f7)를 참조한다.

<a id="0775a64708c620d4"></a>
### 설명

이미 활성화된 audit policy를 변경할 수 있지만 기존 session에는 영향을 미치지 않고 새로 생성되는 session에만 영향을 미친다.

> 다음과 같이 ALL 옵션을 DROP 할 경우, 모든 action이 삭제되는 것이 아니라 해당 ALL 옵션만 삭제된다.

```
CREATE AUDIT POLICY p1
       ACTIONS ALL ON u1.t1,
               SELECT ON u1.t1;

ALTER AUDIT POLICY p1 DROP
      ACTIONS ALL ON u1.t1;
```

<a id="118785cc1e41f228"></a>
### 사용 예

다음은 audit policy에 새로운 audit option을 추가하는 예이다.

```
ALTER AUDIT POLICY policy_dml
      ADD ACTIONS SELECT ON u1.t1;
```

다음은 audit policy에서 audit option을 삭제하는 예이다.

```
ALTER AUDIT POLICY policy_dml
      DROP ACTIONS SELECT ON u1.t1;
```

<a id="54ee2fe494ab180d"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="1b63f951961b0cef"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](19-sql-references-c-g.md#079c12405d0687f7)
    - [DROP AUDIT POLICY](19-sql-references-c-g.md#5665b185fc830eaa)
    - [ALTER AUDIT POLICY](#e6d664ed42cb125a)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#c26186987b5864cf)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#2a39421bd3a74134)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#28a87ad95b910b03)

- Audit trail 삭제: [ALTER DATABASE CLEAR AUDIT TRAIL](#f4b53fa2e7dce2b7)

<a id="1b3565c76f35ea0a"></a>
## ALTER CLUSTER GROUP name ADD MEMBER

<a id="8f61a60447844c93"></a>
### 기능

Cluster group에 cluster member를 추가한다.

<a id="ea089fb3a929f5c5"></a>
### 구문

```
<alter cluster group add member statement> ::=
    ALTER CLUSTER GROUP group_name ADD
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

<a id="bff51a5dbb04d493"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster group add member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="ef3eb05a944daef2"></a>
### 구문 규칙 및 파라미터

<a id="abd3b30065d27dca"></a>
#### group_name

Cluster group의 이름이다.

<a id="550b7d9b67e7f34b"></a>
#### &lt;cluster member definition&gt;

Cluster group에 포함될 cluster member를 정의한다.  
Cluster group은 최대 32 개의 cluster member를 포함할 수 있다.

<a id="e7af8719fd67660b"></a>
#### member_name

Cluster member의 이름이다.   
Cluster member의 이름은 해당 member의 database를 생성할 때 정의한 member의 이름과 동일해야 한다.   
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.   
이름의 길이가 128 바이트보다 작아야 한다.

Cluster member의 start-up 단계가 GLOBAL OPEN이어야 한다.

<a id="0b462c23a0f9a881"></a>
#### &lt;connection attribute&gt;

Cluster member간 통신을 위한 연결 정보를 정의한다.   
&lt;connection attribute&gt;는 해당 member의 database를 생성할 때 정의한 HOST, PORT와 동일해야 한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 host name 또는 IPv4 주소를 사용한다. Host name을 사용할 경우 시스템의 첫 번째 IPv4 주소를 사용한다.
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="eb995d3602881c4c"></a>
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

<a id="7363832ae37359c9"></a>
### 설명

&lt;alter cluster group add member statement&gt; 구문은 table들의 shard를 재배치하지 않는다.   
추가된 cluster member에 shard를 재배치하려면 다음 구문을 수행해야 한다.

- [ALTER DATABASE REBALANCE](#045abf2d149b6478)
- [ALTER TABLE name REBALANCE](#4dcbc8cc43487ef2)

<a id="9c11000f75bbdfb6"></a>
### 사용 예

다음은 cluster group에 두 개의 cluster member를 추가하는 예이다.

```
gSQL>
ALTER CLUSTER GROUP g1 ADD
    CLUSTER MEMBER g1n3 HOST '192.168.0.13' PORT 10130,
    CLUSTER MEMBER g1n4 HOST '192.168.0.14' PORT 10140
;

Cluster Group altered.
```

다음은 비어있는 member position을 cluster member position으로 지정하는 예이다.

```
ALTER CLUSTER GROUP g2 ADD
    CLUSTER MEMBER g2n1 HOST '192.168.0.21' PORT 10210 POSITION 4
;
```

<a id="0428c74523368c03"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="b93864bf19de09d7"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#cb13f01b6a67d24a)
- [DROP CLUSTER GROUP](19-sql-references-c-g.md#d4612fb5786bb45f)
- [ALTER DATABASE REBALANCE](#045abf2d149b6478)
- [ALTER TABLE name REBALANCE](#4dcbc8cc43487ef2)

<a id="289417401c1c26b1"></a>
## ALTER CLUSTER GROUP name OFFLINE MEMBER

<a id="5cfaa45d2015ccd9"></a>
### 기능

Cluster group의 cluster member를 offline 상태로 변경한다.

<a id="ec8b13ca2f057530"></a>
### 구문

```
<alter cluster group offline member statement> ::=
    ALTER CLUSTER GROUP group_name OFFLINE CLUSTER MEMBER member_name
    ;
```

<a id="9ba31563e3978571"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster group offline member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="f30efb77278792d4"></a>
### 구문 규칙 및 파라미터

<a id="2829612bacde276b"></a>
#### group_name

Cluster group의 이름이다.

<a id="13d699db2bf91055"></a>
#### member_name

Cluster member의 이름이다.   
Cluster member는 group_name의 cluster group에 포함돼 있어야 한다.  
Cluster member가 inactive 상태여야 한다.

<a id="26150c4eb2bf5a23"></a>
### 설명

Inactive 상태인 cluster member를 offline 시킨다.

&lt;alter cluster group offline member statement&gt; 구문은 table들의 shard를 재배치하지 않는다.

<a id="f3a0697bcf318156"></a>
### 사용 예

Inactive 상태가 아닌 cluster member를 offline으로 변경하려 하면 다음과 같은 오류가 발생한다.

```
gSQL>

ALTER CLUSTER GROUP g1 OFFLINE CLUSTER MEMBER g1n2;

ERR-42000(16417): active member 'G1N2' cannot be offlined
```

다음은 특정 cluster member를 offline 상태로 변경하는 예이다.

```
gSQL>

ALTER CLUSTER GROUP g1 OFFLINE
    CLUSTER MEMBER g1n3
;
Cluster Group altered.
```

<a id="d179189daba77dab"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="bd651183fa0b0aea"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#cb13f01b6a67d24a)
- [DROP CLUSTER GROUP](19-sql-references-c-g.md#d4612fb5786bb45f)
- [ALTER DATABASE REBALANCE](#045abf2d149b6478)
- [ALTER TABLE name REBALANCE](#4dcbc8cc43487ef2)

<a id="48af3f039b7c7dd9"></a>
## ALTER CLUSTER LOCATION

<a id="2fc10184ad4ddded"></a>
### 기능

Cluster location 정보를 수정한다.

<a id="e8c0ac50e760b8c5"></a>
### 구문

```
<alter cluster location statement> ::=
    ALTER CLUSTER LOCATION member_name 
    <cluster connection attribute>
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="420b6c1cd461ce45"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster location statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="5a344f4e672b7bee"></a>
### 구문 규칙 및 파라미터

<a id="34d2c4398555d377"></a>
#### member_name

Cluster member의 이름이다.   
등록된 cluster location 정보에 동일한 cluster member 이름이 존재해야 한다.   
이름의 길이가 128 바이트보다 작아야 한다.

<a id="140c1a8ec061c331"></a>
#### &lt;cluster connection attribute&gt;

Cluster member 간 통신을 위한 연결 정보를 정의한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 host name 또는 IPv4 주소를 사용한다. Host name을 사용할 경우 시스템의 첫 번째 IPv4 주소를 사용한다.
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="00bc3c8fe6042b1c"></a>
### 설명

만약 cluster location의 접속 정보가 변경될 경우에는 cluster member를 제거하거나 재생성할 필요없이 [ALTER CLUSTER LOCATION](#48af3f039b7c7dd9)을 이용하여 접속 정보를 변경할 수 있다.

<a id="5f50242c0ff4e300"></a>
### 사용 예

```
gSQL> 
ALTER CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120
;

Location altered.
```

<a id="6f27c841d92a9ef5"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="fc840f80f71ad883"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER LOCATION](19-sql-references-c-g.md#67290c5932bd9838)
- [DROP CLUSTER LOCATION](19-sql-references-c-g.md#572d8870897e75c3)

<a id="975c069a4f386a7c"></a>
## ALTER DATABASE ADD LOGFILE

<a id="ba30075f26a7e8be"></a>
### 기능

데이터베이스에 로그파일 그룹 또는 로그파일 멤버를 추가한다.

<a id="4a61f93c8049a067"></a>
### 구문

```
<alter database add logfile statement> ::=
      <add logfile member statement> 
    | <add logfile group statement>
    ;

<add logfile member statement> ::=
    ALTER DATABASE ADD LOGFILE MEMBER <add logfile clause> [, ...] TO 
        <group clause>

<add logfile group statement> ::=
    ALTER DATABASE ADD LOGFILE <group clause> ( 'logfile_name' ) 
        <size clause> [ REUSE ]

<group clause> ::=
    GROUP integer

<add logfile clause> ::=
    'logfile_name' [ REUSE ]

<size clause> ::=
    integer [ M | G ]
```

<a id="835e069e8c3822ce"></a>
### 사용 범위 및 접근 권한

&lt;alter database add logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="bf849304fc0b4b7d"></a>
### 구문 규칙 및 파라미터

<a id="7588e11ce2fd014a"></a>
#### &lt;alter database add logfile statement&gt;

데이터베이스는 MOUNT 상태여야 한다.

<a id="1a0751f6fa6157db"></a>
#### &lt;add logfile member statement&gt;

기존의 로그파일 그룹에 로그 멤버를 추가한다.

- &lt;add logfile clause&gt; 
    - 'logfile_name'은 로그파일 그룹에 추가할 로그파일 멤버의 파일이름이다.
    - 파일이 존재하지 않으면 새로운 파일을 생성한다. 
    - 'logfile_name'의 길이는 1024 바이트보다 작아야 한다. 
- &lt;group clause&gt; 
    - 데이터베이스에 추가할 로그파일 그룹의 식별자를 지정한다.
    - integer는 존재하는 로그파일 그룹의 식별자여야 한다.
    - integer에 해당하는 식별자가 존재하지 않을 경우에는 에러가 발생한다.

<a id="a24baa95155f2eb7"></a>
#### &lt;add logfile group statement&gt;

새로운 로그파일 그룹을 추가한다.

- CURRENT 로그파일 그룹의 다음 그룹으로 추가된다.
- &lt;group clause&gt; 
    - 데이터베이스에 추가할 로그파일 그룹의 식별자를 지정한다.
    - integer는 존재하지 않는 로그파일 그룹 식별자여야 한다.
    - integer에 해당하는 식별자가 존재할 경우 에러가 발생한다. 
- &lt;size clause&gt; 
    - 파일의 크기는 최소 20 MB ~ 최대 120 GB 까지 지정할 수 있다.
    - 파일의 크기는 로그버퍼 (redo log buffer)의 크기와 지연로그버퍼 (pending log buffer) 크기의 합보다 커야 한다.
- 만약 logfile_name이 이미 존재하고 REUSE 옵션을 사용한 경우, 로그파일 그룹 내의 다른 멤버와 크기가 동일하다면 기존 로그파일을 재사용한다.

<a id="04b61df710f7fc0e"></a>
### 설명

새로운 로그파일 그룹 및 로그 멤버가 추가되는 경우 controlfile에 저장되므로 향후 controlfile 손상에 대비해 controlfile을 백업하는 것을 권장한다.

<a id="d088c07bd48d6414"></a>
### 사용 예

다음은 기존 로그파일인 GROUP 3에 두 개의 로그파일 멤버를 추가하는 예이다.

```
ALTER DATABASE ADD LOGFILE MEMBER 'logfile1.log', 'logfile2.log' TO GROUP 3;
```

다음은 로그파일 크기가 100 M이고 로그파일 이름이 'logfile1.log'인 새로운 로그파일 GROUP 4를 데이터베이스에 추가하는 예이다.

```
ALTER DATABASE ADD LOGFILE GROUP 4 ( 'logfile1.log' ) SIZE 100M;
```

> 로그 그룹을 추가할 때는 한 개의 로그파일을 사용해야 하고 이미 존재하는 그룹에 다수의 로그 파일을 멤버로 추가할 수 있다.

<a id="aba33c137da849e9"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="d131816de6e98d6c"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#975c069a4f386a7c)
- [ALTER DATABASE DROP LOGFILE](#512d71b4f3b2f884)
- [ALTER DATABASE RENAME LOGFILE](#0e0424376b3a0ab9)

<a id="052eab7887cba477"></a>
## ALTER DATABASE ARCHIVELOG

<a id="3694dd48afa5b89f"></a>
### 기능

데이터베이스의 온라인 로그파일 archive 설정을 변경한다.

<a id="5622f483aea1a266"></a>
### 구문

```
<alter database archivelog statement> ::=
    ALTER DATABASE { ARCHIVELOG | NOARCHIVELOG }
    ;
```

<a id="6c25ffb613040cf8"></a>
### 사용 범위 및 접근 권한

&lt;alter database archivelog statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="0ba2ea7277d93a0e"></a>
### 구문 규칙 및 파라미터

<a id="7e6a61f31be1522c"></a>
#### &lt;alter database archivelog statement&gt;

- 데이터베이스가 MOUNT 상태여야 한다.
- ARCHIVELOG
    - 온라인 로그파일을 archive 한다.
- NOARCHIVELOG
    - 온라인 로그파일을 archive 하지 않는다.

<a id="657d967342ee88bb"></a>
### 설명

Database를 백업하고 백업을 이용해 복구 (media recovery)하려면 시스템이 ARCHIVELOG 모드로 운용되어야 한다.

<a id="81d5203bf0c7526b"></a>
### 사용 예

다음은 데이터베이스를 archive 모드로 설정하는 예이다.

```
ALTER DATABASE ARCHIVELOG;
```

<a id="253a1fbbf16e7b88"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="b0746f3b1d9a88fe"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#93565f80d30924b0)
- [ALTER TABLESPACE name BACKUP](#7b6fbab7bad894d2)

<a id="93565f80d30924b0"></a>
## ALTER DATABASE BACKUP

<a id="d4cb15a36b611645"></a>
### 기능

전체 데이터베이스를 백업한다.

백업 가능한 대상에는 데이터 파일 (datafile)과 제어 파일 (control file)이 있으며 그중 데이터 파일은 전체 백업 (full backup)과 증분 백업 (incremental backup) 방식으로 백업 가능하다.

<a id="15ec6736171e839b"></a>
### 구문

```
<alter database backup statement> ::=
      <database begin backup statement>
    | <database end backup statement>
    | <database incremental backup statement>
    | <database controlfile backup statement>
    ;

<database begin backup statement> ::=
    ALTER DATABASE BEGIN BACKUP [ AT <domain name> ]
    ;

<database end backup statement> ::=
    ALTER DATABASE END BACKUP [ AT <domain name> ]
    ;


<database incremental backup statement> ::=
    ALTER DATABASE BACKUP INCREMENTAL
        <incremental backup option> [ FORMAT 'format string' ] 
        [ PIECE integer ] [ <parallel clause> ] [ AT <domain name> ];

<incremental backup option> ::=
      LEVEL integer [ CUMULATIVE | DIFFERENTIAL ]

<database controlfile backup statement> ::=
    ALTER DATABASE BACKUP CONTROLFILE TO 'target_name'
        [ AT <domain name> ]    ;


<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="b9f389d2cb9d0601"></a>
### 사용 범위 및 접근 권한

&lt;alter database backup statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="ee34f9ca24b73e41"></a>
### 구문 규칙 및 파라미터

<a id="fd14e040538683a1"></a>
#### &lt;database begin backup clause&gt;

데이터베이스를 전체 백업이 가능한 상태로 설정한다.

- 데이터베이스에서 생성되어 사용 중인 ONLINE 상태의 모든 테이블스페이스를 전체 백업이 가능한 상태로 설정한다. 
- 데이터베이스는 OPEN 상태여야 하고 ARCHIVELOG 모드로 운영되어야 한다.
- BEGIN BACKUP이 시작된 이후에는 다음과 같이 데이터 파일에 쓰기를 요구하는 연산들은 수행할 수 없다.
    - SHUTDOWN NORMAL
    - OFFLINE/ DROP TABLESPACE
    - ADD/ DROP DATAFILE
- 전체 백업의 상태가 ACTIVE인 상태에서 인스턴스가 비정상 종료될 경우, 다시 시작할 때 미디어 복구를 요구할 수도 있다.

<a id="4cce0e079bd1d79d"></a>
#### &lt;database end backup clause&gt;

데이터베이스를 전체 백업 불가능한 상태로 설정한다.

- 데이터베이스에서 생성되어 사용 중인 ONLINE 상태의 모든 테이블스페이스를 백업 불가능한 상태로 설정한다.
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG 모드로 운영되어야 한다.

<a id="f124715cb5808c63"></a>
#### &lt;database incremental backup statement&gt;

- 데이터베이스 증분 백업을 수행한다.
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG로 운영되어야 한다.

<a id="25e370481d3760af"></a>
#### &lt;incremental backup option&gt;

- 'integer'는 0 ~ 4 까지 지정할 수 있다.
- LEVEL 0은 CUMULATIVE나 DIFFERENTIAL을 지정할 수 없다.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - 'integer'가 n이면 가장 최근에 LEVEL 0 ~ LEVEL n-1까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - DIFFERENTIAL
        - 'integer'가 n이면 가장 최근에 LEVEL 0 ~ LEVEL n까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - 생략하면 DIFFERENTIAL이 기본으로 지정된다.

<a id="0b562864c044d0fd"></a>
#### FORMAT 'format string'

- backup 파일 이름의 형식을 지정한다.
- 'format string' 내에 format specifier 를 사용할 수 있다. 
- FORMAT 을 지정하지 않은 경우는 'database_D%T_T%t_L%l_Q%q_P%p.inc' 를 format string 으로 사용한다.
- format specifier
    - %d: 데이터베이스 시그니쳐
    - %q: 백업 순차 번호
    - %l: 백업 레벨
    - %t: 시간(HHMMSS)
    - %m: 클러스터 멤버 이름
    - %g: 클러스터 그룹 이름
    - %D: 요일(DD)
    - %M: 월(MM)
    - %p: 백업 파일의 조각(Piece) 번호
    - %T: 날짜(YYYYMMDD)
    - %Y: 년(YYYY)
    - %%: Percent(%) 문자

<a id="6de23d587b87de41"></a>
#### PIECE integer

- 분할될 백업 파일의 개수를 지정한다.
- 'format string' 에 %p 가 포함되어 있지 않으면 지정된 integer 값은 무시하고 1 값을 갖는다.

<a id="e51ae2ca49f251a0"></a>
#### &lt;parallel clause&gt;

백업시 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 병렬로 백업을 수행하지 않는다.
- PARALLEL [integer] 
    - 병렬로 백업을 수행한다. 
    - integer는 1부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 1이다. 
- 명시하지 않을 경우, 기본값은 NOPARALLEL이다.
- 대상 datafile 의 총 개수가 integer 보다 작은 경우는 datafile 개수만큼 병렬로 수행한다. 
- PIECE 의 개수가 병렬 개수보다 작은 경우는 PIECE 개수 만큼 병렬로 처리한다.

<a id="f0b26fa36eaad958"></a>
#### &lt;database controlfile backup statement&gt;

- 제어 파일 (controlfile)을 백업한다.
    - 'target_name'의 이름은 1024 바이트보다 작아야 한다. 
    - 'target_name'이 이미 존재하는 경우 연산에 실패한다. 
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG로 운영되고 있어야 한다.

> GOLDILOCKS에서 관리하는 'target_name' 길이는 최대 1024 바이트이지만, OS마다 최대로 허용하는 파일 이름 길이가 다르기 때문에, 실제 생성가능한 'target_name'의 길이는 1024 바이트보다 작을 수 있다.

<a id="a8b4ae5a8f6014e5"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="71622157d3daee62"></a>
### 설명

Database의 datafile과 controlfile을 백업한다.  
BEGIN BACKUP을 수행한 후, OS의 파일 복사 기능을 사용해 datafile들을 복사하고, END BACKUP을 수행하여 전체 백업을 완료한다.  
한편, 증분 백업 파일은 하나의 명령어로 BACKUP_DIR_1 property에 설정된 경로에 생성된다.

<a id="0a509458add3ab26"></a>
### 사용 예

다음은 전체 백업 상태를 ACTIVE로 설정하는 예이다.

```
ALTER DATABASE BEGIN BACkUP;
```

다음은 전체 백업 상태를 INACTIVE로 설정하는 예이다.

```
ALTER DATABASE END BACkUP;
```

다음은 DIFFERENTIAL을 사용하여 LEVEL 1의 증분 백업을 수행하는 예이다.

```
ALTER DATABASE BACKUP INCREMENTAL LEVEL 1 DIFFERENTIAL;
```

다음은 controlfile에 대해 'controlfile.bak' 백업 파일을 만드는 예이다. 절대 경로가 포함되지 않은 경우, LOG_DIR property에 설정된 경로에 백업 파일을 생성한다.

```
ALTER DATABASE BACKUP CONTROLFILE TO 'controlfile.bak';
```

다음은 네 개의 thread로 증분 백업을 수행하는 예로써 날짜와 조각 번호로 구성된 네 개의 backup 파일이 만들어진다.

```
ALTER DATABASE BACKUP INCREMENTAL LEVEL 0 FORMAT 'backup_%T_%p' PIECE 4 PARALLEL 4;
```

<a id="25bb10ce70fe1e87"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="f70e43c17b85f13f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#7b6fbab7bad894d2)
- [ALTER DATABASE RECOVER](#233fbcf85decd22e)

<a id="f4b53fa2e7dce2b7"></a>
## ALTER DATABASE CLEAR AUDIT TRAIL

<a id="ec7f2c9cca14bb0c"></a>
### 기능

Audit policy 적용으로 인해 누적된 audit record를 삭제 (purge)한다.

<a id="bdb4ab0559102401"></a>
### 구문

```
<clear audit trail statement> ::= 
    ALTER DATABASE CLEAR AUDIT TRAIL
        [ AT <domain name> ]
    ;
```

<a id="bf827c09085b3858"></a>
### 사용 범위 및 접근 권한

&lt;clear audit trail statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="b5913fc2c4eb0dae"></a>
### 구문 규칙 및 파라미터

<a id="9d875b37666e27a3"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="249273e03991a49a"></a>
### 설명

Audit policy를 활성화하면 시간이 지남에 따라 audit trail이 계속 커진다.   
Audit trail을 구성하는 테이블들은 MEM_AUX_TBS 테이블스페이스에 저장되는데 audit trail이 계속 커지지 않도록 해야 한다.

<a id="2637a8a5fdadc662"></a>
### Audit Trail 저장

필요에 따라 audit trail 을 저장하려면 다음과 같은 절차에 따라 저장한 후에 audit trail을 삭제해야 한다.

- 최초로 수행할 때

```
CREATE TABLE backup_audit_trail AS SELECT * FROM AUDIT_TRAIL;
COMMIT;
```

- 반복해서 수행할 때

```
INSERT INTO backup_audit_trail SELECT * FROM AUDIT_TRAIL;
COMMIT;
```

- Audit trail을 삭제할 때

```
ALTER DATABASE CLEAR AUDIT TRAIL;
```

<a id="eabdd64a5ab8c70e"></a>
### 사용 예

다음 구문을 사용하여 audit trail을 삭제 (purge)한다.

```
ALTER DATABASE CLEAR AUDIT TRAIL;
```

<a id="33818f77e31abbc5"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="a3159905271b2cf8"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](19-sql-references-c-g.md#079c12405d0687f7)
    - [DROP AUDIT POLICY](19-sql-references-c-g.md#5665b185fc830eaa)
    - [ALTER AUDIT POLICY](#e6d664ed42cb125a)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#c26186987b5864cf)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#2a39421bd3a74134)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#28a87ad95b910b03)

- Audit trail 삭제: [ALTER DATABASE CLEAR AUDIT TRAIL](#f4b53fa2e7dce2b7)

<a id="9fcd6b011e0fb566"></a>
## ALTER DATABASE CLEAR PASSWORD HISTORY

<a id="7c0e9b4a7c83dba2"></a>
### 기능

Profile 적용에 따라 누적된 사용자의 비밀번호 변경 이력을 삭제한다.

<a id="211850765dbe9c78"></a>
### 구문

```
<clear password history statement> ::= 
    ALTER DATABASE CLEAR PASSWORD HISTORY
        [ AT <domain name> ]
    ;
```

<a id="b7079a37a24691a8"></a>
### 사용 범위 및 접근 권한

&lt;clear password history statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="80921f1fc3ae8fd6"></a>
### 구문 규칙 및 파라미터

<a id="1d6e98a8d14db658"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="40542f71b515013c"></a>
### 설명

User에 profile을 적용할 때 PASSWORD_REUSE_MAX, PASSWORD_REUSE_TIME의 정책에 따라 사용자의 비밀번호 변경이력이 누적된다.

**변경 이력 관리**

<a id="d730019b32ccfce0"></a>
| PASSWORD_REUSE_MAX | PASSWORD_REUSE_TIME | 변경 이력 관리 |
| --- | --- | --- |
| value | value | Value 범위 내의 변경 이력만 관리하고 범위를 벗어난 변경 이력은 자동으로 삭제한다. |
| value | UNLIMITED | 모든 변경 이력을 검사해야 하므로 변경 이력을 누적할 뿐 제거하지 않는다. |
| UNLIMITED | value | 모든 변경 이력을 검사해야 하므로 변경 이력을 누적할 뿐 제거하지 않는다. |
| UNLIMITED | UNLIMITED | 변경 이력을 검사하지 않으므로 관리도 하지 않는다. |

&lt;clear password history statement&gt; 구문은 누적된 사용자 비밀번호 변경이력을 삭제한다.

<a id="9ace8441aa9cbf3a"></a>
### 사용 예

다음은 &lt;clear password history statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE CLEAR PASSWORD HISTORY;

Database altered.

gSQL> COMMIT;

Commit complete.
```

<a id="5e0bbbce374e9138"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="b55dc5fd9417aa2b"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE PROFILE](19-sql-references-c-g.md#46ce60330a91c0ff)
- [CREATE USER](19-sql-references-c-g.md#96a76bb7ce13b574)

<a id="49be208ada17c239"></a>
## ALTER DATABASE DATAFILE AUTOEXTEND

<a id="38fac157f4ee76eb"></a>
### 기능

디스크 테이블스페이스 데이터 파일의 자동 확장 속성을 변경한다. 자동 확장 속성을 ON으로 변경하면 확장시킬 크기와 데이터 파일의 최대 크기도 변경할 수 있다.

<a id="fff0c4ddb4a34ce8"></a>
### 구문

```
<alter database datafile autoextend statement> ::= 
    ALTER DATABASE DATAFILE datafile_name <autoextend clause>
        [ AT <domain name> ]
    ;

<autoextend clause>
    AUTOEXTEND { ON [ <next size clause> ] [ <max size clause> ] | OFF }

<next size clause>
    NEXT <size clause>

<max size clause>
    MAXSIZE { <size clause> | UNLIMITED }
```

<a id="8e8d2e18fb37120e"></a>
### 사용 범위 및 접근 권한

&lt;alter database datafile autoextend statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

데이터 파일 자동 확장 속성은 디스크 테이블스페이스에 한해서만 변경할 수 있다.

<a id="4fafd73460e73699"></a>
#### datafile_name

변경할 데이터 파일의 이름을 지정한다.

<a id="b21f83bf3b79465d"></a>
#### &lt;autoextend clause&gt;

자동 확장 속성을 ON 또는 OFF로 설정한다. ON으로 설정하면 자동 확장 크기와 데이터 파일의 최대 크기를 지정할 수 있다.

<a id="549b31a56e8ed2d6"></a>
#### &lt;next size clause&gt;

현재 사용 중인 데이터 파일에 더 이상 사용할 공간이 없을 때 확장할 크기를 지정한다.

<a id="2e401f92e8f9721d"></a>
#### &lt;max size clause&gt;

데이터 파일이 확장될 수 있는 최대 크기를 지정한다.

<a id="c42e40f4c6a946bb"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="5745980e105978eb"></a>
### 사용 예

다음은 데이터파일의 자동 확장 속성과 자동 확장 크기, 데이터 파일 크기를 변경하는 예이다.

```
gSQL> ALTER DATABASE DATAFILE 'DISK_TBS.dbf' AUTOEXTEND OFF;

Database altered.

gSQL> ALTER DATABASE DATAFILE 'DISK_TBS.dbf' AUTOEXTEND ON;

Database altered.

gSQL> ALTER DATABASE DATAFILE 'DISK_TBS.dbf' AUTOEXTEND ON NEXT 20M;

Database altered.

gSQL> ALTER DATABASE DATAFILE 'DISK_TBS.dbf' AUTOEXTEND ON MAXSIZE 1G;

Database altered.

gSQL> ALTER DATABASE DATAFILE 'DISK_TBS.dbf' AUTOEXTEND ON 20M MAXSIZE 1G;

Database altered.
```

<a id="ab72460c6d821e1a"></a>
### 호환성

SQL 표준에서는 데이터 파일에 대한 개념을 정의하지 않고 있다.

<a id="38c82128f4956563"></a>
### 참조

관련 내용은 [CREATE DISK DATA TABLESPACE](19-sql-references-c-g.md#827d82aef7b7dbc7)를 참조한다.

<a id="d1c1804d37182cca"></a>
## ALTER DATABASE DELETE BACKUP

<a id="915202be5337fb85"></a>
### 기능

증분 백업 (incremental backup)의 백업 정보와 백업 파일을 삭제한다. Database의 모든 증분 백업을 삭제하거나, 더 이상 쓸모 없는 백업 (obsolete backup)을 선택해서 삭제할 수 있다.

<a id="f6c2e48f40beb476"></a>
### 구문

```
<alter database delete backup statement> ::=
    ALTER DATABASE DELETE <delete backup list option> 
        BACKUP LIST [ <including backup file option> ]
        [ AT <domain name> ]
    ;

<delete backup list option> ::=
      OBSOLETE
    | ALL

<including backup file option> ::=
    INCLUDING BACKUP FILES
```

<a id="598307b2efdb84ce"></a>
### 사용 범위 및 접근 권한

&lt;alter database delete backup statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="0f0b0d48f90ebc60"></a>
### 구문 규칙 및 파라미터

<a id="816ff73b78ad9743"></a>
#### &lt;alter database delete backup statement&gt;

데이터베이스가 MOUNT 또는 OPEN 상태여야 한다.

<a id="0b943c1de49e5554"></a>
#### &lt;delete backup list option&gt;

기존 증분 백업들 중에서 삭제할 대상을 선정한다.

- OBSOLETE: 가장 최근의 데이터베이스 'LEVEL 0' 백업 이전에 백업한 데이터베이스 또는 테이블스페이스 백업본들을 삭제 대상으로 선정한다.
- ALL: 전체 증분 백업들을 삭제 대상으로 선정한다.

<a id="8526d4539cbeeea6"></a>
#### &lt;including backup file option&gt;

- 생략되면 백업 정보만 제어 파일에서 삭제한다.
- 백업 정보뿐만 아니라 백업 파일들도 함께 삭제한다.

<a id="59669e85ecf06dab"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="1a364ac895ef46af"></a>
### 설명

OBSOLETE 증분 백업 삭제는 가장 최근의 LEVEL 0 데이터베이스 백업 이전의 증분 백업을 삭제한다. 즉, LEVEL 0이 아닌 증분 백업을 수행할 때는 이전에 수행한 증분 백업을 포함하는 증분 백업이 있더라도 삭제하지 않는다. 왜냐하면 증분 백업을 이용한 불완전 복구를 수행할 때 사용될 수 있기 때문이다.

> 증분 백업을 삭제할 때 백업 파일까지 함께 삭제하면 증분 백업 정보를 포함하는 백업된 controlfile을 이용하더라도 복구를 수행할 수 없으므로 주의해야 한다.

<a id="ff74686bdaeefe75"></a>
### 사용 예

다음은 기존 모든 증분 백업들의 백업정보와 백업파일들을 삭제하는 예이다.

```
ALTER DATABASE DELETE ALL BACKUP LIST INCLUING BACKUP FILES;
```

<a id="bb0feb64e04793c5"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="078e85303a27ab3b"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#7b6fbab7bad894d2)
- [ALTER DATABASE RECOVER](#233fbcf85decd22e)

<a id="acda1646acf53fd8"></a>
## ALTER DATABASE DISABLE CHANGE TRACKING

<a id="343ebbad1086173b"></a>
### 기능

디스크 테이블스페이스의 데이터 변경 사항 추적 기능을 비활성화 한다.

<a id="b585db93b649e824"></a>
### 구문

```
<alter database disable change tracking statement> ::=
    ALTER DATABASE DISABLE CHANGE TRACKING
        [ AT <domain name> ]
    ;
```

<a id="678793f0e9f970e5"></a>
### 사용 범위 및 접근 권한

&lt;alter database disable change tracking statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="45f485201ef204ab"></a>
### 구문 규칙 및 파라미터

데이터베이스가 MOUNT 또는 OPEN 상태여야 한다.

<a id="cd58bcdbbe4fa78f"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="7db2baad25e2fbdd"></a>
### 설명

디스크 테이블스페이스에 대한 증분 백업 수행 시, 백업 대상 페이지 관리 기능을 비활성화 한다.

> CHANGE TRACKING을 비활성화하면, 디스크 테이블스페이스에 대한 증분 백업 수행 시 백업 대상을 판단하기 위해 모든 페이지를 스캔해야 한다. 이로 인해 백업 수행 시간이 길어지고, 결과적으로 서비스에 영향을 줄 수 있으므로 주의해야 한다.

<a id="eac97b215c9dacbd"></a>
### 사용 예

다음은 CHANGE TRACKING 을 비활성화 하는 예이다.

```
ALTER DATABASE DISABLE CHANGE TRACKING;
```

<a id="9e6a48976c207284"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="ae464debfe5c4e93"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ENABLE CHANGE TRACKING](#0624629171efe118)
- [ALTER DATABASE RENAME CHANGE TRACKING FILE](#86093b65db0319c4)

<a id="8ce707cabe9dc37a"></a>
## ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS

<a id="e61c3601530988a8"></a>
### 기능

모든 inactive cluster member들을 제거한다.

<a id="fb0d92f807f78614"></a>
### 구문

```
<alter database drop inactive members statement> ::=
    ALTER DATABASE DROP [ FORCE | NO FORCE ] INACTIVE CLUSTER MEMBERS
    ;
```

<a id="436fcfa4a6ca2efb"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database drop inactive cluster members statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="f898b77ce8e4cd2f"></a>
### 구문 규칙 및 파라미터

<a id="535a1df4f45d29c3"></a>
#### [ FORCE | NO FORCE ]

- FORCE
    - 데이터 유실될 수 있는 경우에도 inactive cluster member들을 제거한다.
- NO FORCE
    - 데이터가 유실될 수 있는 경우에는 inactive cluster member들을 제거할 수 없다.
- 기본값은 NO FORCE 이다.

<a id="2739ec70f91d5f99"></a>
### 설명

모든 inactive cluster member들을 제거한다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우 
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

단, cluster member를 제거할 때 table의 shard가 유실되는 경우에는 inactive cluster member를 제거할 수 없다.

또한, cluster member를 제거할 때 데이터가 유실될 수 있는 경우에는 inactive cluster member를 제거할 수 없다. 제거하려는 inactive cluster member에 속해 있는 table이나 shard의 replica가 해당 cluster group의 다른 멤버들보다 최신 데이터를 가지고 있지 않다는 보장이 있어야 데이터 유실을 방지할 수 있다. 따라서 cloned table의 경우에는 cluster 전체에, sharded table의 경우에는 같은 cluster group에 적어도 하나의 online 멤버가 존재할 경우에 inactive cluster member 제거를 허용한다.

단, cluster group에 online 상태인 cluster member가 없고 inactive cluster member로 인해 서비스가 불가능한 경우에는 데이터 유실을 감수하면서 FORCE 옵션을 통해 inactive cluster member를 제거할 수 있다.

&lt;alter database drop inactive members statement&gt; 구문은 모든 inactive cluster member들이 더 이상 cluster system에 포함될 수 없는 경우에 사용하는 것이 바람직하다.

<a id="8eaad14e94d93c77"></a>
### 사용 예

다음은 &lt;alter database drop inactive members statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="fa0992b72e6377c3"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="aab5712375889f42"></a>
### 참조

관련 내용은 [ALTER SYSTEM JOIN DATABASE](#d64c686b2011e181) 를 참조한다.

<a id="512d71b4f3b2f884"></a>
## ALTER DATABASE DROP LOGFILE

<a id="7ba1462666387903"></a>
### 기능

데이터베이스에 존재하는 로그파일 그룹이나 멤버를 제거한다.

<a id="520b82cf94535632"></a>
### 구문

```
<alter database drop logfile statement> ::=
      <drop logfile group statement>
    | <drop logfile member statement>
    ;

<drop logfile group statement> ::=
    ALTER DATABASE DROP LOGFILE <group clause>

<group clause> ::=
    GROUP integer

<drop logfile member statement> ::=
    ALTER DATABASE DROP LOGFILE MEMBER <logfile_list>

<logfile_list> ::=
      'logfile_name'
    | <logfile_list> , 'logfile_name'
```

<a id="aa57a8cb83dc8475"></a>
### 사용 범위 및 접근 권한

&lt;alter database drop logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="381554367212cc4c"></a>
### 구문 규칙 및 파라미터

<a id="9d192118eca81c4f"></a>
#### &lt;alter database drop logfile statement&gt;

데이터베이스는 MOUNT 상태여야 한다.   
제거하려는 로그파일이 CURRENT 또는 ACTIVE 상태일 때는 에러가 발생한다.   
제거한 후에 최소 네 개의 로그파일 그룹이 남아 있어야 한다.

<a id="b7fea7e555634b46"></a>
#### &lt;drop logfile group statement&gt;

기존의 로그파일 그룹을 제거한다.

- &lt;group clause&gt; 
    - 제거할 로그파일 그룹을 지정한다.
    - integer는 존재하는 로그파일의 식별자여야 한다. 
    - integer가 존재하지 않을 경우 에러가 발생한다.

<a id="7f4fdf929c22fb81"></a>
#### &lt;drop logfile member statement&gt;

기존의 로그파일 멤버들을 제거한다.

- &lt;logfile_list&gt;
    - 제거할 로그파일 멤버의 목록이다.
    - 'logfile_name'은 존재하는 이름이어야 한다. 
    - 'logfile_name'이 존재하지 않을 경우 에러가 발생한다.

<a id="ed8e765205322216"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="30a3f6c1f9e579bf"></a>
### 사용 예

다음은 기존 로그파일인 GROUP 3을 제거하는 예이다.

```
ALTER DATABASE DROP LOGFILE GROUP 3;
```

다음은 기존 로그파일인 GROUP 3에서 'logfile1.log'와 'logfile2.log'를 제거하는 예이다.

```
ALTER DATABASE DROP LOGFILE MEMBER 'logfile1.log', 'logfile2.log';
```

<a id="1376b116a384c6ab"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="9adef2236c356d76"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#975c069a4f386a7c)
- [ALTER DATABASE RENAME LOGFILE](#0e0424376b3a0ab9)

<a id="68248209f3b43891"></a>
## ALTER DATABASE DROP OFFLINE SEGMENTS

<a id="b1af2063434db6a2"></a>
### 기능

모든 테이블에 대해서 오프라인 된 shard들의 세그먼트를 삭제한다.

<a id="bfa4480d22546f9b"></a>
### 구문

```
<alter database drop offline segments statement> ::=
    ALTER DATABASE DROP OFFLINE SEGMENTS 
    ;
```

<a id="051c8951b122314d"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database drop offline segments statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="efaec5dbd84eacb0"></a>
### 설명

모든 테이블에 대해서 오프라인 된 shard들의 세그먼트를 삭제하는데 inactive cluster member가 있어도 수행할 수 있다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우 
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

&lt;alter database drop offline segments statement&gt;는 각 테이블마다 [&lt;alter table drop offline segments statement&gt;](#122c923f4ef34146)를 수행하며 다음과 같은 질의의 합과 동치이다.

```
ALTER TABLE t1 DROP OFFLINE SEGMENTS;
COMMIT;
ALTER TABLE t2 DROP OFFLINE SEGMENTS;
COMMIT;
ALTER TABLE t3 DROP OFFLINE SEGMENTS;
COMMIT;

...

ALTER TABLE tn DROP OFFLINE SEGMENTS;
COMMIT;
```

&lt;alter database drop offline segments statement&gt;는 특정 테이블에서 에러가 발생하더라도 종료되지 않고 다음 테이블에 대해 계속 진행되며 다음과 같은 경고와 함께 성공한다.

```
gSQL> ALTER DATABASE DROP OFFLINE SEGMENTS;

ERR-42000(16553): of the total '5' tables, '1' tables failed to drop offline segments
Database altered.
```

위 에러 메시지는 다섯 개의 테이블 중에서 한 개의 테이블이 실패했다는 의미이다.

이후 에러에 대해 적절한 조치를 취한 후 &lt;alter database drop offline segments statement&gt; 구문을 다시 수행하면 실패했던 테이블에 대해서만 해당 구문이 다시 수행된다.

에러에 대한 자세한 내용은 구문을 수행한 멤버의 시스템 트레이스 로그 (system.trc)를 참조한다.

<a id="9601c59e603b70ca"></a>
### 사용 예

다음은 &lt;alter database drop offline segments statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE DROP OFFLINE SEGMENTS;

Database altered.
```

<a id="50d5eaad92a32925"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="1fa25f57349c3844"></a>
### 참조

관련 내용은 [ALTER TABLE name DROP OFFLINE SEGMENTS](#122c923f4ef34146)를 참조한다.

<a id="8888ca9668cd1e67"></a>
## ALTER DATABASE DROP UNUSABLE SEGMENTS

<a id="3c6694a32e535ca0"></a>
### 기능

데이터베이스에 존재하는 모든 테이블 중, 오프라인 상태인 replica들의 unusable 세그먼트를 삭제한다.

<a id="29bf51ff10333107"></a>
### 구문

```
<alter database drop unusable segments statement> ::=
    ALTER DATABASE DROP UNUSABLE SEGMENTS 
    ;
```

<a id="9f97d69d61171edf"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database drop unusable segments statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="3da16fecb1b5a3bd"></a>
### 설명

&lt;alter database drop unusable segments statement&gt;는 각 테이블에 대해 [&lt;alter table drop unusable segments statement&gt;](#436fa49da2672327)를 수행하며, 이는 아래 질의들을 모두 수행한 것과 동일한 효과를 갖는다.

```
ALTER TABLE t1 DROP UNUSABLE SEGMENTS;
COMMIT;
ALTER TABLE t2 DROP UNUSABLE SEGMENTS;
COMMIT;
ALTER TABLE t3 DROP UNUSABLE SEGMENTS;
COMMIT;

...

ALTER TABLE tn DROP UNUSABLE SEGMENTS;
COMMIT;
```

&lt;alter database drop unusable segments statement&gt;는 특정 테이블에서 에러가 발생하더라도 종료되지 않고 다음 테이블에 대해 계속 진행되며 다음과 같은 경고와 함께 성공한다.

```
gSQL> ALTER DATABASE DROP UNUSABLE SEGMENTS;

ERR-42000(16553): of the total '5' tables, '1' tables failed to drop offline segments
Database altered.
```

위 에러 메시지는 다섯 개의 테이블 중에서 한 개의 테이블이 실패했다는 의미이다.

이후 에러에 대해 적절한 조치를 취한 후 &lt;alter database drop unusable segments statement&gt; 구문을 다시 수행하면 실패했던 테이블에 대해서만 해당 구문이 적용된다.

에러에 대한 자세한 내용은 구문을 수행한 멤버의 시스템 트레이스 로그 (system.trc)를 참조한다.

이 구문은 inactive member가 있어도 수행할 수 있다.

<a id="bec1db3cdcecde74"></a>
### 사용 예

다음은 &lt;alter database drop unusable segments statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE DROP UNUSABLE SEGMENTS;

Database altered.
```

<a id="d9ad57a5d354e710"></a>
### 호환성

SQL 표준에서는 unusable 세그먼트에 대한 개념을 정의하지 않고 있다.

<a id="a08b991ce5c55377"></a>
### 참조

관련 내용은 [ALTER TABLE name DROP UNUSABLE SEGMENTS](#436fa49da2672327)를 참조한다.

<a id="0624629171efe118"></a>
## ALTER DATABASE ENABLE CHANGE TRACKING

<a id="9f2b7cd3a792ad4d"></a>
### 기능

디스크 테이블스페이스의 데이터 변경 사항 추적 기능을 활성화 한다.

<a id="c59c1966ea371579"></a>
### 구문

```
<alter database enable change tracking statement> ::=
    ALTER DATABASE ENABLE CHANGE TRACKING
        [ USING FILE 'file_name' REUSE ]
        [ AT <domain name> ]
    ;
```

<a id="0f523a02aba99fa3"></a>
### 사용 범위 및 접근 권한

&lt;alter database enable change tracking statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="4e3c5f29f29fac39"></a>
### 구문 규칙 및 파라미터

<a id="e5183c72f489c1bf"></a>
#### &lt;alter database enable change tracking statement&gt;

데이터베이스가 MOUNT 또는 OPEN 상태여야 한다.   
CHANGE TRACKING 기능은 비활성화된 상태여야 한다.

- USING FILE 'file_name'
    - CHANGE TRACKING을 활성화할 때 'file_name'으로 지정된 파일을 사용한다.
    - 파일을 지정하지 않으면, [CHANGE_TRACKING_FILE](../part-02-administration-manual/10-server-property.md#4f436a868b271594) 프로퍼티에 설정된 파일 이름을 사용한다.
- 'file_name'
    - 'file_name' 이 절대 경로가 아닐 경우, [SYSTEM_TABLESPACE_DIR](../part-02-administration-manual/10-server-property.md#ec376b6168ad435d) 프로퍼티에 설정된 경로와 합쳐진 경로를 따른다.
- REUSE
    - 파일이 이미 존재할 경우 REUSE 절을 사용한다.
    - 파일이 존재하지 않을 경우에는 새로운 파일을 생성한다.

<a id="e0d6ff00dcfc13e3"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="db9f6f2ccc4e1c0a"></a>
### 설명

디스크 테이블스페이스에 대한 증분 백업 수행 시, 백업 대상 페이지 관리 기능을 활성화 한다.

<a id="de46d599c89586de"></a>
### 사용 예

다음은 CHANGE TRACKING 을 활성화 하는 예이다.

```
ALTER DATABASE ENABLE CHANGE TRACKING;
```

<a id="8c6e9853b3037be5"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="e5a56547e00b800f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE DISABLE CHANGE TRACKING](#acda1646acf53fd8)
- [ALTER DATABASE RENAME CHANGE TRACKING FILE](#86093b65db0319c4)

<a id="4752ea45b3668af4"></a>
## ALTER DATABASE MOVE SHARD

<a id="73d1f3f38727d164"></a>
### 기능

특정 cluster group의 모든 table들의 shard를 다른 cluster group으로 재배치한다.

<a id="5821a56c9427104f"></a>
### 구문

```
<alter database move shard statement> ::=
    ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP src_cluster_group
        TO CLUSTER GROUP dest_cluster_group 
       [ ONLINE | OFFLINE ] 
       [ LOGGING | NOLOGGING ] 
       [ <scan partition> ] 
       [ <parallel clause> ]
    ;

<scan partition> ::= 
    SCAN PARTITION integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="b526ca70e3b5c15e"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database move shard statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="d4c6b5db600411f0"></a>
### 구문 규칙 및 파라미터

<a id="a3d0b53b2e17f727"></a>
#### src_cluster_group

테이블의 shard를 이동할 cluster group 이다.

<a id="974bf573df49a0bb"></a>
#### dest_cluster_group

테이블의 shard를 이동시킬 target cluster group이다.

<a id="8a7960472e6188fb"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="ac91bf8eff1aa950"></a>
#### [ LOGGING | NOLOGGING ]

테이블의 shard를 재배치할 때, 테이블 동기화 과정에서 기록되는 로그의 양을 지정한다.

- LOGGING
    - 테이블 동기화 과정에서 모든 로그를 기록한다.
- NOLOGGING
    - 테이블 동기화 과정에서 최소한의 로그만 기록한다.
- 생략할 경우, 기본값은 LOGGING 이다.

> NOLOGGING 옵션을 사용하면 redo log가 기록되지 않는다. 따라서 move shard 수행 후 서버가 비정상적으로 종료되면 해당 테이블은 unusable 상태가 된다. 이를 방지하려면 move shard 수행 후 CHECKPOINT 구문을 실행해야 한다.

<a id="fc70509123acfd8a"></a>
#### &lt;scan partition&gt;

Shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버에 재배치 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, ONLINE_DDL_SCAN_PARTITION 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="385f5c93063d1f9a"></a>
#### &lt;parallel clause&gt;

테이블 재배치에 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 테이블을 병렬로 재배치하지 않는다.
- PARALLEL [integer] 
    - 테이블을 병렬로 재배치한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="06d1b7a795b9a5aa"></a>
### 설명

다음과 같은 구문을 사용하여 cluster member와 cluster group을 추가할 때 table들의 shard는 재배치하지 않는다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#cb13f01b6a67d24a)
- [ALTER CLUSTER GROUP name ADD MEMBER](#1b3565c76f35ea0a)

Cluster group과 cluster member를 추가할 때 재배치되지 않은 모든 테이블들의 shard를 재배치하려면 &lt;alter database rebalance statement&gt; 구문을 수행한다.

Shard를 재배치하지 않은 테이블들에 대해 &lt;alter database move shard statement&gt; 구문을 수행하는 것은 다음과 같은 의미이다.

```
ALTER TABLE t1 MOVE SHARD FROM CLUSTER GROUP src_group TO CLUSTER GROUP dest_group;
COMMIT;
ALTER TABLE t2 MOVE SHARD FROM CLUSTER GROUP src_group TO CLUSTER GROUP dest_group;
COMMIT;
ALTER TABLE t3 MOVE SHARD FROM CLUSTER GROUP src_group TO CLUSTER GROUP dest_group;
COMMIT;
...
...
ALTER TABLE t_n MOVE SHARD FROM CLUSTER GROUP src_group TO CLUSTER GROUP dest_group;
COMMIT;
```

CLONED 테이블이거나 CLUSTER WIDE로 설정된 테이블을 제외한 모든 테이블들을 위와 같이 수행한다. 특정 테이블이 shard 재배치에 실패하더라도 &lt;alter database move shard statement&gt; 구문은 계속 진행되고 shard 재배치에 성공한 테이블을 rollback 하지 않는다.

따라서 에러에 대해 적절한 조치를 취한 후 &lt;alter database move shard statement&gt; 구문을 다시 수행하면 이미 shard 재배치에 성공한 테이블들은 재배치 대상에 포함되지 않으며, 재배치가 필요한 테이블들의 shard만 재배치한다.

<a id="912091773893ad27"></a>
### 사용 예

다음은 &lt;alter database move shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP G1 TO CLUSTER GROUP G2;

Database altered.
```

<a id="2c221b2312048b9a"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="c1c69dd8c8ca506a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name MOVE SHARD](#b64b6ca52ad7b811)
- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#cb13f01b6a67d24a)
- [ALTER CLUSTER GROUP name ADD MEMBER](#1b3565c76f35ea0a)

<a id="98259b572214ad92"></a>
## ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS

<a id="05789d6f8c118ab1"></a>
### 기능

모든 inactive cluster member들을 offline 상태로 변경한다. 즉, 해당 cluster member들에 대한 shard map을 offline 상태로 변경한다.

<a id="d4f90741c6636a2c"></a>
### 구문

```
<alter database offline inactive cluster members statement> ::=
    ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS
    ;
```

<a id="b7c7993885905cd5"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database offline inactive cluster members statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="080b4da464dd1f4a"></a>
### 구문 규칙 및 파라미터

모든 inactive cluster member들을 offline 상태로 변경한다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

<a id="c5226afc934bf543"></a>
### 설명

&lt;alter database offline inactive members statement&gt; 구문은 모든 inactive cluster member들이 더 이상 cluster system에 포함될 수 없는 경우에 사용하는 것이 바람직하다.

Inactive cluster member가 cluster system에 참여할 수 있으면 [ALTER SYSTEM JOIN DATABASE](#d64c686b2011e181) 구문을 수행하여 cluster system에 포함시킨다.

Offline 상태로 변경된 cluster member는 join 후에 다음 구문을 사용하여 online 상태로 다시 변경할 수 있다

- [ALTER DATABASE REBALANCE](#045abf2d149b6478)
- [ALTER TABLE name REBALANCE](#4dcbc8cc43487ef2)

<a id="18f786807cc9958b"></a>
### 사용 예

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;
```

<a id="c9e678efd9f861b5"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="57ec1b8b5b7d2599"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER SYSTEM JOIN DATABASE](#d64c686b2011e181)
- [ALTER DATABASE REBALANCE](#045abf2d149b6478)
- [ALTER TABLE name REBALANCE](#4dcbc8cc43487ef2)

<a id="045abf2d149b6478"></a>
## ALTER DATABASE REBALANCE

<a id="a90892621bb25c0b"></a>
### 기능

모든 table들의 shard를 재배치한다.

<a id="52170417d593a637"></a>
### 구문

```
<alter database rebalance statement> ::=
    ALTER DATABASE REBALANCE
       [ ONLINE | OFFLINE ] 
       [ LOGGING | NOLOGGING ]
       [ <scan partition> ] 
       [ <parallel clause> ]
    ;

<scan partition> ::= 
    SCAN PARTITION integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="25eea99c1e3478a1"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database rebalance statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="1f094351c86c050d"></a>
### 구문 규칙 및 파라미터

<a id="0d8b5d3ca3f0f078"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="b149fec695d3319e"></a>
#### [ LOGGING | NOLOGGING ]

테이블의 shard를 재배치할 때, 테이블 동기화 과정에서 기록되는 로그의 양을 지정한다.

- LOGGING
    - 테이블 동기화 과정에서 모든 로그를 기록한다.
- NOLOGGING
    - 테이블 동기화 과정에서 최소한의 로그만 기록한다.
- 생략할 경우, 기본값은 LOGGING 이다.

> NOLOGGING 옵션을 사용하면 redo log가 기록되지 않는다. 따라서 rebalance 수행 후 서버가 비정상적으로 종료되면 해당 테이블은 unusable 상태가 된다. 이를 방지하려면 rebalance 수행 후 CHECKPOINT 구문을 실행해야 한다.

<a id="f6dab1e454724657"></a>
#### &lt;scan partition&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버에 재배치 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, ONLINE_DDL_SCAN_PARTITION 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="3a39dcffad0444ad"></a>
#### &lt;parallel clause&gt;

테이블 재배치에 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 테이블을 병렬로 재배치하지 않는다.
- PARALLEL [integer] 
    - 테이블을 병렬로 재배치한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="170ea22b5d501edf"></a>
### 설명

다음과 같은 구문을 사용하여 cluster member, cluster group을 추가할 때 table들의 shard를 재배치하지 않는다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#cb13f01b6a67d24a)
- [ALTER CLUSTER GROUP name ADD MEMBER](#1b3565c76f35ea0a)

추가된 cluster group과 cluster member에 재배치하지 않은 모든 테이블들의 shard를 재배치하기 위해 &lt;alter database rebalance statement&gt; 구문을 수행한다.

Shard를 재배치하지 않은 테이블들에 대해 &lt;alter database rebalance statement&gt; 구문을 수행하는 것은 다음과 같은 의미이다.

```
ALTER TABLE t1 REBALANCE;
COMMIT;
ALTER TABLE t2 REBALANCE;
COMMIT;
ALTER TABLE t3 REBALANCE;
COMMIT;
...
...
ALTER TABLE t_n REBALANCE;
COMMIT;
```

특정 테이블의 shard 재배치에 실패하더라도 &lt;alter database rebalance statement&gt; 구문은 계속 진행되며 shard 재배치에 성공한 테이블을 rollback 하지 않는다.

따라서 에러에 대해 적절한 조치를 취한 후 &lt;alter database rebalance statement&gt; 구문을 재수행할 경우 이미 shard 재배치에 성공한 테이블들은 재배치 대상에 포함되지 않으며, 재배치가 필요한 테이블들의 shard만 재배치한다.

<a id="7afbdf50b53052c2"></a>
### 사용 예

다음은 &lt;alter database rebalance statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE REBALANCE;

Database altered.
```

<a id="d177c4728aadab15"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="4bf5dcc1a196af1a"></a>
### 참조

관련 내용은 [ALTER TABLE name REBALANCE](#4dcbc8cc43487ef2)를 참조한다.

<a id="b2d27be01aaaa9b7"></a>
## ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP

<a id="b90009ec72a04f52"></a>
### 기능

특정 cluster group에 shard가 포함되지 않도록 모든 테이블의 shard를 재배치한다.

<a id="dff59d28f9df77db"></a>
### 구문

```
<alter database rebalance exclude cluster group statement> ::=
    ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP cluster_group_name        
       [ ONLINE | OFFLINE ]        
       [ LOGGING | NOLOGGING ]        
       [ <scan partition> ]        
       [ <parallel clause> ]
    ;

<scan partition> ::= 
    SCAN PARTITION integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="ac45ade1c1461f7c"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database rebalance exclude cluster group statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="3b69eadf8aa9d619"></a>
### 구문 규칙 및 파라미터

<a id="f0039b31aac3ee2d"></a>
#### cluster_group_name

테이블들의 shard를 포함하지 않는 cluster group의 이름이다.  
지정한 cluster group이 유일한 cluster group인 경우 구문을 수행할 수 없다.

<a id="427888390c58c50a"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="c15d0a3b737b3154"></a>
#### [ LOGGING | NOLOGGING ]

테이블의 shard를 재배치할 때, 테이블 동기화 과정에서 기록되는 로그의 양을 지정한다.

- LOGGING
    - 테이블 동기화 과정에서 모든 로그를 기록한다.
- NOLOGGING
    - 테이블 동기화 과정에서 최소한의 로그만 기록한다.
- 생략할 경우, 기본값은 LOGGING 이다.

> NOLOGGING 옵션을 사용하면 redo log가 기록되지 않는다. 따라서 rebalance 수행 후 서버가 비정상적으로 종료되면 해당 테이블은 unusable 상태가 된다. 이를 방지하려면 rebalance 수행 후 CHECKPOINT 구문을 실행해야 한다.

<a id="195e6813b1fd1687"></a>
#### &lt;scan partition&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버에 재배치 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, ONLINE_DDL_SCAN_PARTITION 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="4033f91b35d6ee1b"></a>
#### &lt;parallel clause&gt;

테이블 재배치에 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 테이블을 병렬로 재배치하지 않는다.
- PARALLEL [integer] 
    - 테이블을 병렬로 재배치한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="ae5115d8eed7303b"></a>
### 설명

[DROP CLUSTER GROUP](19-sql-references-c-g.md#d4612fb5786bb45f) 구문을 사용하여 cluster group을 제거하려면 해당 cluster group에 shard가 존재하지 않아야 한다.

해당 cluster group이 shard를 포함하지 않도록 하기 위해 &lt;alter database rebalance exclude cluster group statement&gt; 구문을 수행한다. 해당 cluster group의 shard를 포함한 테이블들에 대해 &lt;alter database rebalance exclude cluster group statement&gt; 구문을 수행하는 것은 다음과 같은 의미이다.

```
ALTER TABLE t1 REBALANCE EXCLUDE CLUSTER GROUP g3;
COMMIT;
ALTER TABLE t2 REBALANCE EXCLUDE CLUSTER GROUP g3;
COMMIT;
ALTER TABLE t3 REBALANCE EXCLUDE CLUSTER GROUP g3;
COMMIT;
...
...
ALTER TABLE t_n REBALANCE EXCLUDE CLUSTER GROUP g3;
COMMIT;
```

저장 공간 부족 등으로 인해 &lt;alter database rebalance exclude cluster group statement&gt; 구문이 실패한 경우, shard 배제에 성공한 테이블은 rollback 하지 않는다.

따라서 에러에 대해 적절한 조치를 취한 후 &lt;alter database rebalance exclude cluster group statement&gt; 구문을 다시 수행하면 이미 shard 배제에 성공한 테이블들은 재배치 대상에 포함되지 않으며, 재배치가 필요한 테이블들의 shard만 배제하고 재배치한다.

<a id="857ee4bc4a0bb32a"></a>
### 사용 예

다음은 &lt;alter database rebalance exclude cluster group statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP g3;

Database altered.
```

<a id="e6e07a718a7af84f"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="b32bda028afd43cc"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP CLUSTER GROUP](19-sql-references-c-g.md#d4612fb5786bb45f)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#5f2f7d4e4bdedbe5)

<a id="233fbcf85decd22e"></a>
## ALTER DATABASE RECOVER

<a id="a6a1437a51770068"></a>
### 기능

온라인/ archive log file을 사용하여 데이터베이스 내의 전체 데이터파일 (datafile) 또는 일부 데이터파일을 복구한다.

<a id="7c26dbad55a44215"></a>
### 구문

```
<alter database recover statement> ::=
      <complete database recover statement>
    | <datafile recover statement>
    | <complete tablespace recover statement>
    | <incomplete database recover statement>
    ;

<complete database recover statement> ::=
    ALTER DATABASE RECOVER [<recovery slaves clause>]

<datafile recover statement> ::=
    ALTER DATABASE RECOVER DATAFILE
        <datafile recovery clause>
        [ <recovery slaves clause> ]
        [ AT <domain name> ]

<datafile recovery clause> ::=
    <datafile recovery object> [, ...]

<datafile recovery object> ::=
    'datafile_name' [<recovery using backup option>] [recovery corruption option>]

<recovery using backup option> ::=
    USING BACKUP 'backup_datafile_name'

<recovery corruption option> ::=
    CORRUPTION

<complete tablespace recover statement> ::=
    ALTER DATABASE RECOVER TABLESPACE tablespace_name
        [ <recovery slaves clause> ]
        [ AT <domain name> ]

<incomplete database recover statement> ::=
      <batch incomplete recovery statement>
    | <interactive incomplete recovery statement>
    ;

<batch incomplete recovery statement> ::=
    ALTER DATABASE RECOVER <until clause> [<recovery slaves clause>]
    
<until clause> ::=
      UNTIL CHANGE integer
    | UNTIL CHANGE SCN scn_format
    | UNTIL TIME datetime_format

<using backup controlfile option> ::=
    USING BACKUP CONTROLFILE

<interactive incomplete recovery statement> ::=
    ALTER DATABASE <incomplete recovery option>

<incomplete recovery option> ::=
      BEGIN INCOMPLETE RECOVERY [<recovery slaves clause>]
    | END INCOMPLETE RECOVERY
    | RECOVER 'logfile name'
    | RECOVER AUTOMATICALLY
    | RECOVER SUGGESTION
    ;
<datafile recovery clause> ::=
    <datafile recovery object> [, ...]

<recovery slaves clause> ::=
      NOPARALLEL
    | PARALLEL [integer]
```

<a id="3401bb60cbf7ed6b"></a>
### 사용 범위 및 접근 권한

&lt;alter database recover statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="e9077775e562defb"></a>
### 구문 규칙 및 파라미터

<a id="c3a0abed93e5a301"></a>
#### &lt;complete database recover statement&gt;

온라인 및 archive 로그파일을 이용하여 데이터베이스의 데이터 파일들을 최신상태로 복구한다.

- ONLINE 상태의 모든 테이블스페이스를 복구한다. 
- 데이터베이스는 MOUNT 상태여야하고, ARCHIVELOG 모드여야 한다. 
- 필요한 archive log file이 존재하지 않으면 실패한다.

<a id="f46dd40e76194036"></a>
#### &lt;datafile recover statement&gt;

Immediate option으로 offline 된 tablespace의 datafile, backup 된 datafile 또는 backup 도중에 장애가 발생하여 archive logfile을 이용한 복구가 필요한 tablespace의 datafile들을 최신 상태로 복구한다.

- Datafile은 MOUNT phase 또는 OPEN phase에서 복구할 수 있다.
- OPEN phase에서의 복구는 OFFLINE 상태의 tablespace의 datafile만 가능하고, MOUNT phase에서의 복구는 ONLINE/ OFFLINE 상태의 datafile 모두 가능하다.
- 필요한 archive logfile이 존재하지 않으면 복구에 실패한다.
- &lt;datafile recovery clause&gt; 
    - 복구할 한 개 이상의 datafile object list를 기술한다.
- &lt;datafile recovery object&gt;
    - 복구할 datafile 이름과 복구 옵션을 설정한다.
- &lt;recovery using backup option&gt;
    - 복구할 datafile의 backup datafile 이름을 설정한다.
- &lt;recovery corruption option&gt;
    - 복구할 datafile에서 corrupt 된 page만 복구할지 여부를 설정한다.

<a id="a283cc549201d315"></a>
#### &lt;complete tablespace recover statement&gt;

테이블스페이스의 데이터 파일들을 최신 상태로 복구한다.

- 테이블스페이스를 복구하려면 데이터베이스가 MOUNT 또는 OPEN 상태여야 한다. 
- OPEN 상태에서의 복구는 OFFLINE 상태의 테이블스페이스만 가능하고, MOUNT 상태에서의 복구는 ONLINE/ OFFLINE 상태의 테이블스페이스 모두 가능하다. 
- 필요한 archive log file이 존재하지 않으면 복구에 실패한다.
- 다음과 같은 경우에는 테이블스페이스 복구 연산이 필요하다.
    - IMMEDIATE 로 OFFLINE 된 테이블스페이스
    - 백업된 데이터 파일을 이용해야 하는 경우
    - 전체 백업중 장애가 발생한 경우

<a id="f8ed76701edf5879"></a>
#### &lt;incomplete database recover statement&gt;

<a id="945676b612f19a0a"></a>
##### &lt;batch incomplete database recover statement&gt;

온라인 및 archive log file을 이용하여 데이터베이스의 데이터 파일들을 최신상태가 아닌 특정 시점까지 일괄 복구한다.

- ONLINE 상태의 모든 테이블스페이스를 복구한다. 
- 데이터베이스는 MOUNT 상태여야하고, ARCHIVELOG 모드여야 한다. 
- 불완전 복구될 시점 이후의 데이터가 존재하는 데이터 파일을 이용하면 실패한다. 
- 불완전 복구가 완료되면 반드시 RESETLOGS로 데이터베이스를 OPEN 해야 한다. 
- &lt;until clause&gt; 
    - 불완전 복구될 특정 시점이다.
    - UNTIL CHANGE: 로그 단위로 불완전 복구 시점을 지정한다.
    - UNTIL CHANGE SCN: SCN 단위로 불완전 복구 시점을 지정한다.
    - UNTIL TIME: datetime 단위로 불완전 복구 시점을 지정한다.
- scn_format
    - 불완전 복구 완료 scn을 'gcn.dcn.lcn' format으로 표시한다.
    - gcn: global change number(BIGINT)
    - dcn: domain change number(BIGINT)
    - lcn: local change number(BIGINT)
    - gcn과 dcn은 클러스터 환경에서만 유효하다.
    - gcn은 BIGINT type만 사용할 수 있다.
    - dcn과 lcn은 BIGINT type과 '*'를 사용할 수 있으며, '*'는 infinite를 의미한다.
    - dcn이 BIGINT인 경우, lcn은 null을 사용할 수 없고, BIGINT type 또는 '*'를 사용해야 한다.
    - dcn이 '*' 인 경우, lcn은 반드시 null 이어야 한다.
- datetime_format
    - 불완전 복구 완료 시각을 'YYYY-MM-DD HH24:MI:SS[.[FF6]]' format으로 표시한다.
    - YYYY: 년
    - MM: 월
    - DD: 일
    - HH24: 시간
    - MI: 분
    - SS: 초
    - FF6: 밀리초

<a id="11e3ac8e0c14cd99"></a>
##### &lt;interactive incomplete database recover statement&gt;

온라인 및 archive log file을 이용하여 데이터베이스의 데이터 파일들을 최신상태가 아닌 특정 시점까지 사용자와 대화식으로 복구한다.

- ONLINE 상태의 모든 테이블스페이스를 복구한다. 
- 데이터베이스는 MOUNT 상태여야하고, ARCHIVELOG 모드여야 한다. 
- 불완전 복구될 특정 시점 이후 데이터가 존재하는 데이터 파일을 이용하면 실패한다. 
- 불완전 복구가 완료되면 반드시 RESETLOGS로 데이터베이스를 OPEN 해야 한다. 
- &lt;incomplete recovery option&gt;
    - 로그 파일 단위로 대화식 불완전 복구를 수행하기 위한 옵션이다.
    - BEGIN INCOMPLETE RECOVERY: 불완전 복구를 시작한다.
    - END INCOMPLETE RECOVERY: 불완전 복구를 종료한다.
    - RECOVER 'logfile name': 복구를 수행할 로그 파일을 사용자가 직접 설정한다.
    - RECOVER AUTOMATICALLY: 복구 가능한 모든 archive log file을 복구한다.
    - RECOVER SUGGESTION: 시스템이 추천한 복구를 위해 필요한 archive log file을 복구한다.

<a id="913cd8233d004d7e"></a>
#### &lt;recovery slaves clause&gt;

병렬 복구에 참여하는 slave 개수를 지정한다. 만약 &lt;recovery slaves clause&gt;가 생략된 경우에는 [RECOVERY_SLAVES](../part-02-administration-manual/10-server-property.md#0f33ffc599e55ae7) 프로퍼티에 설정된 값을 따른다.

- NOPARALLEL
    - Slave thread 없이 master thread 만으로 복구를 수행한다.
- PARALLEL [integer] 
    - 병렬로 복구를 수행한다.
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우에는 [RECOVERY_SLAVES](../part-02-administration-manual/10-server-property.md#0f33ffc599e55ae7) 프로퍼티에 설정된 값을 따른다.
    - integer가 0인 경우는 NOPARALLEL과 같다.

불완전 복구의 BEGIN INCOMPLETE RECOVERY를 수행할 때 &lt;recovery slaves clause&gt;가 지정된 경우에는 이후 RECOVER 구문에서 BEGIN INCOMPLETE RECOVERY를 수행할 때 지정된 값을 사용하여 데이터베이스를 병렬 복구한다.

<a id="032939116b0b84b2"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="17e27095b488714b"></a>
### 설명

데이터베이스 불완전 복구는 복구 완료 시점을 한 번에 찾아내기 어려우므로 여러 번 수행하여 원하는 복구 시점을 찾아야 한다. 그런데 불완전 복구가 완료된 후 RESETLOGS 옵션으로 데이터베이스를 기동하면 새로운 데이터베이스가 되기 때문에 archive log file과 온라인 redo log file에 대한 복사본을 만든 후에 불완전 복구를 여러 번 수행해야 한다.

<a id="66f24300fc954d9e"></a>
### 사용 예

다음은 전체 데이터베이스를 완전 복구하는 예이다.

```
ALTER DATABASE RECOVER;
```

다음은 데이터 파일을 복구하는 예이다.

```
ALTER DATABASE RECOVER DATAFILE 'test.dbf';
```

다음은 테이블스페이스를 복구하는 예이다.

```
ALTER DATABASE RECOVER TABLESPACE test_tbs;
```

다음은 LSN이 11123인 지점까지 전체 데이터베이스를 불완전 복구하는 예이다.

```
ALTER DATABASE RECOVER UNTIL CHANGE 11123;
```

다음은 SCN 이 '100.10.1000', '100.10.*', '100.*'인 지점까지 전체 데이터베이스를 불완전 복구하는 예이다.

```
ALTER DATABASE RECOVER UNTIL SCN '100.10.1000';
```

'*'는 infinite를 의미한다.   
dcn이 '*' 로 설정된 경우, 지정된 gcn 보다 크지 않은 모든 log를 복구한다.   
lcn이 '*' 로 설정된 경우, 지정된 gcn과 dcn 보다 크지 않은 모든 log를 복구한다.

```
ALTER DATABASE RECOVER UNTIL SCN '100.10.1000';
ALTER DATABASE RECOVER UNTIL SCN '100.10.*';
ALTER DATABASE RECOVER UNTIL SCN '100.*';
```

다음은 datetime 이 '2026-03-09 16:38:35.148078'인 지점까지 전체 데이터베이스를 불완전 복구하는 예이다.

```
ALTER DATABASE RECOVER UNTIL TIME '2026-03-09 16:38:35.148078';
```

다음은 복구 가능한 archive log file까지만 복구하는 대화식 불완전 복구의 예이다.

```
ALTER DATABASE BEGIN INCOMPLETE RECOVERY;
ALTER DATABASE RECOVER AUTOMATICALLY;
ALTER DATABASE END INCOMPLETE RECOVERY;
```

<a id="dd751f3b453cf1f2"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="0fe65e3adbcf1406"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#93565f80d30924b0)
- [ALTER TABLESPACE name BACKUP](#7b6fbab7bad894d2)
- [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#cbf215370461aa13)

<a id="a996ea8c8491c041"></a>
## ALTER DATABASE REGISTER

<a id="32d5889d89b41080"></a>
### 기능

복구 불가능한 세그먼트를 데이터베이스에 등록한다.

<a id="41db2d61d5012225"></a>
### 구문

```
<alter database register statement> ::=
    ALTER DATABASE REGISTER IRRECOVERALBE SEGMENT 
        <segment physical identifier list>
    ;

<segment physical identifier list> ::=
      integer
    | <segment physical identifier list> , integer
```

<a id="81a7c8e165a81e02"></a>
### 사용 범위 및 접근 권한

&lt;alter database register statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="18acbb8566428c90"></a>
### 구문 규칙 및 파라미터

<a id="33f00f4ad0eec289"></a>
#### &lt;alter database register statement&gt;

복구 불가능한 세그먼트를 데이터베이스에 등록한다. 해당 구문은 백업이 존재하지 않고 데이터베이스를 복구할 수 없는 경우, 세그먼트를 더 이상 사용하지 않는다는 가정하에 사용될 수 있다.

- 데이터베이스가 MOUNT 상태여야 한다.
- 등록된 세그먼트 식별자 목록은 재시작할 때 초기화된다.
- 서버 재시작에 성공하면 등록된 세그먼트들이 'UNUSABLE' 상태가 되는데 해당 세그먼트들은 반드시 삭제해야 한다.

<a id="687a452aaca23b77"></a>
#### &lt;segment physical identifier list&gt;

복구 불가능한 세그먼트의 식별자 목록이다.  
• Integer: 8 바이트 정수형의 세그먼트 식별자

<a id="9ba44810a2f2b5b0"></a>
### 설명

서버를 비정상 종료하고 재시작할 때 데이터베이스를 복구하는데, 이 때 이전 서비스 단계에서 디스크에 반영되지 못한 페이지들을 복구하기 위해서 REDO 로그들을 이용해 페이지를 다시 수행한다.

REDO 연산을 수행하는 중에 예상하지 못한 실패가 발생한 경우, 이를 무시하고 복구하기 위해 사용될 수 있다.

<a id="e292422496a62a62"></a>
### 사용 예

다음은 4028679323648을 식별자로 갖는 세그먼트 복구를 포기하는 예이다.

```
ALTER DATABASE REGISTER IRRECOVERABLE SEGMENT 4028679323648;
```

<a id="ca9534c15b6be9be"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="2c7c548d973e332b"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#7b6fbab7bad894d2)
- [ALTER DATABASE RECOVER](#233fbcf85decd22e)

<a id="86093b65db0319c4"></a>
## ALTER DATABASE RENAME CHANGE TRACKING FILE

<a id="8df309ba5dc01cfd"></a>
### 기능

Change tracking 파일의 이름을 변경한다.

<a id="1f67b6642c115b59"></a>
### 구문

```
<rename change tracking file statement> ::=
    ALTER DATABASE RENAME CHANGE TRACKING FILE 'file_name'
    ;
```

<a id="aee93e95808f0cb5"></a>
### 사용 범위 및 접근 권한

&lt;rename change tracking file statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="9b23d2dbbf3d44cb"></a>
### 구문 규칙 및 파라미터

<a id="a766f398fa05db2d"></a>
#### &lt;rename change tracking file statement&gt;

- 데이터베이스가 MOUNT 상태여야 한다.
- Change tracking 이 활성화되어 있는 상태여야 한다.

<a id="045892bb14177dcd"></a>
#### 'file_name'

- Change tracking 파일의 이름을 지정한다. 
- 절대 경로가 아니라면 SYSTEM_TABLESPACE_DIR 프로퍼티와 병합된 경로를 따른다.

<a id="1885a6ac1848127a"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="ee93451ef09d1cf2"></a>
### 사용 예

다음은 change tracking 파일의 이름을 변경하는 예이다.

```
gSQL> ALTER DATABASE RENAME CHANGE TRACKING FILE 'new_change_tracking.ctf';

Database altered.
```

<a id="3f2b46c5918ad43d"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="afe6ece46b6cea32"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ENABLE CHANGE TRACKING](#0624629171efe118)
- [ALTER DATABASE DISABLE CHANGE TRACKING](#acda1646acf53fd8)

<a id="99bcbcc9f4d63ec3"></a>
## ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE

<a id="18b81a57f2f74257"></a>
### 기능

데이터베이스에서 글로벌 트랜잭션 로그파일의 이름을 수정한다.

<a id="b00e2cb8bd8ac778"></a>
### 구문

```
<alter database rename global transaction logfile statement> ::=
    ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE <source_clause>
       TO <target_clause>
    ;

<source_clause> ::= <logfile_list>

<target_clause> ::= <logfile_list>

<logfile_list> ::=
      'logfile_name'
    | <logfile_list>, 'logfile_name'
```

<a id="42f06eb434d8b732"></a>
### 사용 범위 및 접근 권한

&lt;alter database rename global transaction logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="61a44a4c4043501f"></a>
### 구문 규칙 및 파라미터

<a id="7bb28148be125700"></a>
#### &lt;alter database rename global transaction logfile statement&gt;

- 데이터베이스는 MOUNT 상태여야 한다.
- source_clause
    - 데이터베이스에서 수정될 글로벌 트랜잭션 로그파일 목록이다.
- target_clause
    - 데이터베이스에서 수정될 글로벌 트랜잭션 로그파일 목록이다.
    - 파일이 존재하지 않을 경우 에러가 발생한다.
    - 경로를 포함한 이름의 길이는 1024 바이트보다 작아야 한다.

<a id="75ab813d3c6680d8"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="b7c30194a3fd8b4b"></a>
### 사용 예

다음은 글로벌 트랜잭션 로그파일을 변경하는 예이다.

```
ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE
 'org_commit_0.log', 'org_commit_1.log' TO 'new_commit_0.log', 'new_commit_1.log';
```

<a id="08d2a0b0e0ff41ab"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="ec06665244e104a1"></a>
### 참조

관련 내용은 [ALTER DATABASE RENAME LOGFILE](#0e0424376b3a0ab9)을 참조한다.

<a id="0e0424376b3a0ab9"></a>
## ALTER DATABASE RENAME LOGFILE

<a id="bb17195b1a56be4a"></a>
### 기능

데이터베이스에서 로그파일의 이름을 수정한다.

<a id="28db7728f54fa414"></a>
### 구문

```
<alter database rename logfile statement> ::=
    ALTER DATABASE RENAME LOGFILE <logfile_list> TO <logfile_list>
    ;

<logfile_list> ::=
      'logfile_name'
    | <logfile_list> , 'logfile_name'
```

<a id="30dd159fbc55eb15"></a>
### 사용 범위 및 접근 권한

&lt;alter database rename logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="ece4d33353a8fc7a"></a>
### 구문 규칙 및 파라미터

<a id="0ec3de6d3b3b439b"></a>
#### &lt;alter database rename logfile statement&gt;

- 데이터베이스는 MOUNT 상태여야 한다.
- FROM &lt;logfile_list&gt;
    - 데이터베이스에서 수정할 로그파일들의 이름 목록이다.
- TO &lt;logfile_list&gt;
    - 데이터베이스에서 수정될 로그파일들의 이름 목록이다.
    - &lt;logfile_list&gt;는 존재하는 파일이어야 한다. 
    - 파일이 존재하지 않을 경우 에러가 발생한다.

<a id="565b889493bca0d4"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="b6001a71ad6861a8"></a>
### 사용 예

다음은 기존 로그파일 'logfile.log'를 'newlogfile.log'로 변경하는 예이다.

```
ALTER DATABASE RENAME LOGFILE 'logfile.log' TO 'newlogfile.log';
```

<a id="7741b7c8267e0550"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="ac4d7b1f1be8ed68"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#975c069a4f386a7c)
- [ALTER DATABASE DROP LOGFILE](#512d71b4f3b2f884)

<a id="9c0a4f742c9210c5"></a>
## ALTER DATABASE RESET LOCAL CLUSTER MEMBER

<a id="435c22bdb8bf79c2"></a>
### 기능

Local cluster member에서 tablespace 객체를 제외한 부분을 database 생성 시점으로 초기화한다.

<a id="4694496d6077fe07"></a>
### 구문

```
<alter database reset local cluster member statement> ::=
    ALTER DATABASE RESET LOCAL CLUSTER MEMBER
    ;
```

<a id="15dc9ca535884f2e"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

Start-up 과정 중 LOCAL OPEN 단계에서 수행할 수 있다.

&lt;alter database reset local cluster member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="575c3e845003fb33"></a>
### 설명

Local cluster member에서 tablespace 객체를 제외한 부분을 database 생성 시점으로 초기화한다.  
Tablespace 객체를 제외하고 사용자가 생성한 모든 객체를 제거한다.

&lt;alter database reset local cluster member statement&gt; 구문은 inactive cluster member를 초기화하고,  
새로운 cluster member를 cluster system에 참여시키기 위해 사용한다.  
Cluster system과 연결이 끊긴 inactive cluster member들은 다음과 같이 처리할 수 있다.

- Cluster system에 다시 참여할 수 있는 경우, JOIN 구문을 이용하여 참여시킨다. 
    - [ALTER SYSTEM JOIN DATABASE](#d64c686b2011e181) 
- Cluster system에 다시 참여할 수 없는 경우, DROP 구문을 이용하여 cluster system에서 제외한다. 
    - [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#8ce707cabe9dc37a)

이 때, cluster system에서 제외된 cluster member에 해당하는 장비는 다음 두 가지 방법으로 재사용할 수 있다.

- 방법 1: Local cluster member의 database를 다시 생성한다.
- 방법 2: &lt;alter database reset local cluster member statement&gt; 구문을 이용해 local cluster member를 초기화한다.

방법 2는 방법 1보다 tablespace를 재생성하는 비용을 줄일 수 있다.

<a id="4020975818ab55c7"></a>
### 사용 예

다음은 cluster system에서 제외된 local cluster member를 LOCAL OPEN 단계까지 구동한 후, &lt;alter database reset local cluster member statement&gt; 구문을 이용해 초기화하는 예이다.

```
gSQL> \startup nomount

Startup success


gSQL> ALTER SYSTEM MOUNT DATABASE;

System altered.


gSQL> ALTER SYSTEM OPEN LOCAL DATABASE;

System altered.

gSQL> ALTER DATABASE RESET LOCAL CLUSTER MEMBER;

Database altered.
```

<a id="d7fbaae05c88a0ca"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="ca2569a6f665e785"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER SYSTEM JOIN DATABASE](#d64c686b2011e181)
- [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#8ce707cabe9dc37a)

<a id="60ea018060bd0c35"></a>
## ALTER DATABASE RESTORE

<a id="adca41164a267718"></a>
### 기능

증분 백업을 이용하여 데이터베이스 또는 테이블스페이스 내의 데이터 파일들을 복원한다.

<a id="59c4bef73bb6a2ab"></a>
### 구문

```
<alter database restore statement> ::=
      <database restore statement>
    | <tablespace restore statement>
    | <controlfile restore statement>
    ;

<database restore statement> ::=
    ALTER DATABASE RESTORE [ <until clause> ] [ <parallel clause> ]

<until clause> ::=
    UNTIL CHANGE integer

<tablespace restore statement> ::=
    ALTER DATABASE RESTORE TABLESPACE tablespace_name 
        [ <parallel clause> ] [ AT <domain name> ]


<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]

<controlfile restore statement> ::=
    ALTER DATABASE RESTORE CONTROLFILE FROM 'file_name'
```

<a id="85bce9b5c26238e1"></a>
### 사용 범위 및 접근 권한

alter database restore statement> 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="067f378b2f23bf91"></a>
### 구문 규칙 및 파라미터

<a id="cabf25fbefc5360d"></a>
#### &lt;database restore statement&gt;

증분 백업을 사용하여 데이터베이스 내의 데이터 파일들을 복원한다.   
데이터베이스가 MOUNT 상태여야 한다.

<a id="5806ff590bd198db"></a>
#### &lt;tablespace restore statement&gt;

증분 백업을 사용하여 테이블스페이스 내의 데이터 파일들을 복원한다.

- 데이터베이스가 MOUNT 또는 OPEN 상태여야 한다. 
- OPEN 상태에서는 OFFLINE 상태의 테이블스페이스만 복원할 수 있고, MOUNT 상태에서는 ONLINE/ OFFLINE 상태의 테이블스페이스 모두 복원할 수 있다.

<a id="ff382b76e4c0cf47"></a>
#### &lt;parallel clause&gt;

복원시 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 병렬로 복원을 수행하지 않는다.
- PARALLEL [integer]
    - 병렬로 복원을 수행한다.
    - integer는 1부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 1이다. 
- 명시하지 않을 경우, 기본값은 NOPARALLEL이다.

<a id="f0cdb81e7921676e"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="96b955cb44857c85"></a>
#### &lt;controlfile restore statement&gt;

'file_name'을 사용하여 제어파일을 복원한다.

- 데이터베이스가 NOMOUNT 상태여야 한다.
- 'file_name'은 절대 경로를 권장하지만, 만약 상대 경로를 기술한 경우에는 &lt;GOLDILOCKS_HOME&gt;/wal/'file_name'을 이용한다.

<a id="c90f595d41ac0109"></a>
### 설명

전체 백업을 이용한 데이터 파일 복원은 OS 복사 명령으로 백업된 파일을 직접 데이터 파일 경로에 복사하는 방법이다. 증분 백업을 이용한 데이터 파일 복원은 삭제된 데이터 파일이나 이전 데이터 파일들만 복원한다.

<a id="8f0b487b187c5a33"></a>
### 사용 예

다음은 증분 백업을 사용하여 데이터베이스를 복원하는 예이다.

```
ALTER DATABASE RESTORE;
```

다음은 증분 백업을 사용하여 테이블스페이스를 복원하는 예이다.

```
ALTER DATABASE RESTORE TABLESPACE test_tbs;
```

다음은 LSN이 11123보다 작은 증분 백업만 사용하여 데이터베이스를 복원하는 예이다.

```
ALTER DATABASE RESTORE UNTIL CHANGE 11123;
```

다음은 controlfile.bak을 사용하여 제어파일을 복원하는 예이다.

```
ALTER DATABASE RESTORE CONTROLFILE FROM 'controlfile.bak'
```

다음은 네 개의 thread로 database를 복원하는 예이다.

```
ALTER DATABASE RESTORE PARALLEL 4;
```

<a id="611716194d95808c"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="c2c705352c864229"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#93565f80d30924b0)
- [ALTER TABLESPACE name BACKUP](#7b6fbab7bad894d2)
- [ALTER DATABASE RECOVER](#233fbcf85decd22e)

<a id="1620340d3358eb5b"></a>
## ALTER DATABASE SYNCHRONIZE

<a id="6740200fb7f0f633"></a>
### 기능

모든 테이블의 shard들과 시퀀스들을 원격으로 동기화한다.

<a id="2f780d63e5329f20"></a>
### 구문

```
<alter database synchronize statement> ::=
    ALTER DATABASE SYNCHRONIZE 
       [ <synchronize target> ] 
       [ ONLINE | OFFLINE ] 
       [ LOGGING | NOLOGGING ] 
       [ <scan partition> ] 
       [ <parallel clause> ]
    ;

<synchronize target> ::= 
    TABLE
  | SEQUENCE
  | TABLE AND SEQUENCE
  | SEQUENCE AND TABLE

<scan partition> ::= 
    SCAN PARTITION integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="53b0a138a2f03c13"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database synchronize statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="6ff4c6fcf75da793"></a>
### 구문 규칙 및 파라미터

<a id="dcc5465cdda5eff6"></a>
#### &lt;synchronize target&gt;

동기화 대상 객체를 지정한다.

- TABLE
    - 테이블 객체를 동기화한다.
- SEQUENCE
    - 시퀀스 객체를 동기화한다. 
- TABLE AND SEQUENCE 또는 SEQUENCE AND TABLE
    - 테이블과 시퀀스 객체를 동기화한다.
- 생략할 경우, 기본값은 TABLE AND SEQUENCE 이다.

<a id="6b43101c5a3671bf"></a>
#### [ ONLINE | OFFLINE ]

동기화 수행시 DML을 허용할지 여부를 결정한다

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="709825c3a758e49e"></a>
#### [ LOGGING | NOLOGGING ]

테이블 동기화 과정에서 기록되는 로그의 양을 지정한다.

- LOGGING
    - 테이블 동기화 과정에서 모든 로그를 기록한다.
- NOLOGGING
    - 테이블 동기화 과정에서 최소한의 로그만 기록한다.
- 생략할 경우, 기본값은 LOGGING 이다.

> NOLOGGING 옵션을 사용하면 redo log가 기록되지 않는다. 따라서 move shard 수행 후 서버가 비정상적으로 종료되면 해당 테이블은 unusable 상태가 된다. 이를 방지하려면 synchronize 수행 후 CHECKPOINT 구문을 실행해야 한다.

<a id="ef4586aed6771148"></a>
#### &lt;scan partition&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버와 동기화 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, ONLINE_DDL_SCAN_PARTITION 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

&lt;synchronize target&gt;에 SEQUENCE만 지정될 경우, 이는 무시된다.

<a id="9bcf648ebe0195b2"></a>
#### &lt;parallel clause&gt;

테이블을 동기화할 때 사용할 thread 개수를 지정한다.

- NOPARALLEL
    - 테이블을 병렬로 동기화하지 않는다.
- PARALLEL [integer] 
    - 테이블을 병렬로 동기화한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

&lt;synchronize target&gt;에 SEQUENCE만 지정될 경우, 이는 무시된다.

<a id="13d40c719fcd1d15"></a>
### 설명

기존에 배치되어 있는 모든 오프라인된 shard와 시퀀스들을 동기화하고 온라인으로 변경한다. [ALTER DATABASE REBALANCE](#045abf2d149b6478)와는 달리 inactive cluster member가 있어도 수행할 수 있다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우 
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

&lt;alter database synchronize statement&gt;는 각 테이블마다 [&lt;alter table synchronize statement&gt;](#baf7d0e8598b3f6a)를 수행하며 다음과 같은 질의의 합과 동치이다.

```
ALTER TABLE t1 SYNCHRONIZE;
COMMIT;
ALTER TABLE t2 SYNCHRONIZE;
COMMIT;
ALTER TABLE t3 SYNCHRONIZE;
COMMIT;

...

ALTER TABLE tn SYNCHRONIZE;
COMMIT;
```

&lt;alter database synchronize statement&gt;는 특정 테이블을 동기화하는 도중에 에러가 발생하더라도 종료하지 않고 다음 테이블의 동기화를 진행하며 다음과 같은 경고와 함께 성공한다.

```
gSQL> ALTER DATABASE SYNCHRONIZE;

ERR-42000(16555): of the total '5' tables, '1' tables failed to synchronize
Database altered.
```

위 에러 메시지는 다섯 개의 테이블 중에서 한 개의 테이블이 실패했다는 의미이다.

이후 에러에 대해 적절한 조치를 취한 후 &lt;alter database synchronize statement&gt; 구문을 다시 수행하면 실패했던 테이블에 대해서만 진행된다.

자세한 에러는 구문을 수행한 멤버의 시스템 트레이스 로그(system.trc)를 참조한다.

<a id="34b38d3ccaf60f70"></a>
### 사용 예

다음은 &lt;alter database synchronize statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE SYNCHRONIZE;

Database altered.
```

<a id="a6b68fbf75792813"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="4242b99555a02743"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE REBALANCE](#045abf2d149b6478)
- [ALTER TABLE name REBALANCE](#4dcbc8cc43487ef2)

<a id="73ef1debf9756149"></a>
## ALTER INDEX

<a id="103c9b9091910190"></a>
### 기능

인덱스 정의를 변경한다.

<a id="e6d9aeca0293a7e8"></a>
### 구문

```
<alter index statement> ::=
      <alter index physical attribute statement>
    | <rename index statement>
    | <aging index statement>
    | <rebuild index statement>
    | <index coalesce statement>
    | <alter index enforcement>
    ;
```

<a id="91ad40ece8c46b8b"></a>
### 사용 범위 및 접근 권한

&lt;alter index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="892693a6051040f9"></a>
### 구문 규칙 및 파라미터

<a id="e37d3165c36cd160"></a>
#### &lt;alter index physical attribute statement&gt;

인덱스의 물리적 속성을 변경한다.  
자세한 내용은 [ALTER INDEX name STORAGE](#ba7154f8d22befe2) 구문을 참조한다.

<a id="275318f339cf0de2"></a>
#### &lt;rename index statement&gt;

인덱스 이름을 변경한다.  
자세한 내용은 [ALTER INDEX name RENAME TO](#ce4a5d821138cd3a) 구문을 참조한다.

<a id="e4eb2086c50668e6"></a>
#### &lt;aging index statement&gt;

인덱스의 빈 페이지를 삭제한다.  
자세한 내용은 [ALTER INDEX name AGING](#511bd0353b36d0df) 구문을 참조한다.

<a id="777937ce77bd0e08"></a>
#### &lt;rebuild index statement&gt;

인덱스를 재구축한다.  
자세한 내용은 [ALTER INDEX name REBUILD](#56aed70ce2b90a69) 구문을 참조한다.

<a id="65d6af40f4286fa3"></a>
#### &lt;index coalesce statement&gt;

인덱스 단편화를 제거한다.  
자세한 내용은 [ALTER INDEX name COALESCE](#ba3aecf4b34c844b) 구문을 참조한다.

<a id="35334fbf2ed6e374"></a>
#### &lt;alter index enforcement&gt;

인덱스를 활성화 또는 비활성화 한다.  
자세한 내용은 [ALTER INDEX name ENABLE/DISABLE](#8c8f90f0415b3a2e) 구문을 참조한다.

<a id="c592eaa6bff5e3c7"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="1a70406bdc822237"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="28ebbb2b124279c2"></a>
### 호환성

SQL 표준에서는 인덱스에 대한 개념을 다루지 않고 있다.

<a id="511bd0353b36d0df"></a>
## ALTER INDEX name AGING

<a id="60c5bd1956552b6f"></a>
### 기능

인덱스의 빈 페이지를 삭제한다. DML과 동시에 수행할 수 있다.

<a id="2719a68d7d754aba"></a>
### 구문

```
<aging index statement> ::=
    ALTER INDEX index_name AGING
        [ AT <domain name> ]
    ;
```

<a id="6688d83e140aca7f"></a>
### 사용 범위 및 접근 권한

&lt;aging index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="fcb870df083c2691"></a>
### 구문 규칙 및 파라미터

<a id="f4824fc67037cec6"></a>
#### index_name

대상 인덱스의 이름이다.

<a id="b11a0d10e8dd6162"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="a9fad6db15e6ca8f"></a>
### 설명

해당 구문은 인덱스 페이지들 중에 모든 키가 삭제된 페이지들을 세그먼트로 반납한다. Aging은 논리적 삭제와 물리적 삭제라는 두 단계로 진행된다. 논리적 삭제는 인덱스에서 페이지를 지칭하는 연결을 끊는 작업인데 페이지의 마지막 키를 삭제할 당시의 SCN이 시스템의 agable SCN보다 작을 때 이 작업이 수행된다. 이 후 물리적 삭제가 이루어지는데 논리적으로 삭제할 때의 SCN이 시스템의 agable SCN 보다 작을 때 이 작업이 수행된다.

> 만약 시스템의 agable SCN이 증가하지 않으면 인덱스 AGING 구문이 성공하더라도 빈 페이지가 삭제되지 않을 수 있다.

<a id="4f91926e9b7f8372"></a>
### 사용 예

다음은 인덱스를 aging 하는 예이다.

```
gSQL> select index_name, empty_blocks from user_indexes where index_name = 'T1X';

INDEX_NAME EMPTY_BLOCKS
---------- ------------
T1X                   2

1 row selected.

gSQL> alter index t1x aging;

Index altered.

gSQL> select index_name, empty_blocks from user_indexes where index_name = 'T1X';

INDEX_NAME EMPTY_BLOCKS
---------- ------------
T1X                   0

1 row selected.
```

<a id="5ca175e8daebfb00"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="9ca2b6286a283956"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](19-sql-references-c-g.md#1b99962ed891aa4f)
- [ALTER INDEX](#73ef1debf9756149)
- [DROP INDEX](19-sql-references-c-g.md#d01836ffe196ec14)

<a id="ba3aecf4b34c844b"></a>
## ALTER INDEX name COALESCE

<a id="13ab20e4bdd87fc0"></a>
### 기능

인덱스의 인접한 leaf page들을 병합하여 인덱스의 사용 공간을 줄인다. DML과 동시에 수행할 수 있다.

<a id="60fd735f3e259476"></a>
### 구문

```
<index coalesce statement> ::=
    ALTER INDEX index_name COALESCE
        [ AT <domain name> ]
    ;
```

<a id="5dd98390fe9c59f4"></a>
### 사용 범위 및 접근 권한

&lt;index coalesce statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

인덱스가 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="814a1633684f6b37"></a>
### 구문 규칙 및 파라미터

<a id="21b80a3cb8811f68"></a>
#### index_name

대상 인덱스의 이름이다.  
스키마 이름을 명시할 수 있으며, 생략할 경우 사용자의 기본 스키마 이름이 사용된다.

<a id="1a224b6fd79a4ba2"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="3517a986096ff49f"></a>
### 설명

<a id="b7521cb300cc0f3b"></a>
![Index coalesce](../assets/images/8576bc649e4c83df.png)

- leaf 페이지들을 순차적으로 탐색하여 병합 가능한 페이지들을 병합하고, 제거된 페이지들을 세그먼트로 반환한다.
- UPDATE/ DELETE 등으로 인해 발생한 leaf 페이지의 단편화 문제를 해결할 수 있다.
- 유효하지 않은 shard와 관련된 key들을 제거하고 shard sequence 제한을 풀어준다.
- 인접한 leaf 페이지들이 병합 가능한 경우에만 동작하므로 단편화 정도가 낮은 상태에서는 효과가 없을 수 있다.
- 인덱스의 단편화 정도가 심한 경우 INDEX REBUILD보다 더 오래 걸릴 수 있다.

**INDEX REBUILD와 비교**

<a id="5441ec93dd1a2f05"></a>
|  | INDEX REBUILD | INDEX COALESCE |
| --- | --- | --- |
| 인덱스 속성 변경 | 가능 | 불가능 |
| 테이블스페이스 이동 | 가능 | 불가능 |
| 테이블 잠금 | 필요 | 불필요 |
| 수행을 위한 추가 공간 | 필요 | 불필요 |
| 트리 높이 감소 | 가능 | 불가능 |

<a id="67148316eda4da82"></a>
### 사용 예

```
gsql> ALTER INDEX T1X COALESCE;

Index altered.
```

<a id="d4195b2ef28c871c"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="5537ffe5312998df"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER INDEX](#73ef1debf9756149)
- [ALTER INDEX name REBUILD](#56aed70ce2b90a69)

<a id="8c8f90f0415b3a2e"></a>
## ALTER INDEX name ENABLE/DISABLE

<a id="98f9105c064f7ac2"></a>
### 기능

인덱스를 활성화 또는 비활성화 한다.

<a id="601dbb3aaf5ee9b5"></a>
### 구문

```
<alter index enforcement> ::=
    ALTER INDEX index_name <index enforcement>
    ;

<index enforcement> ::=
      { ENABLE | ENFORCED }
    | { DISABLE | NOT ENFORCED }
```

<a id="af57448f4eeff11e"></a>
### 사용 범위 및 접근 권한

&lt;alter index enforcement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자
- 인덱스가 속한 테이블의 소유자
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY INDEX ON DATABASE

<a id="510a2be4b0ce8f6c"></a>
### 구문 규칙 및 파라미터

<a id="a80f1a0caf52c36f"></a>
#### index_name

대상 인덱스의 이름이다.  
스키마 이름을 명시할 수 있으며, 생략할 경우 사용자의 기본 스키마 이름이 사용된다.

<a id="505b9b1fae2b8162"></a>
#### &lt;index enforcement&gt;

ENABLE 과 ENFORCED 는 동일한 의미이다.  
DISABLE 과 NOT ENFORCED 는 동일한 의미이다.

- ENABLE
    - Index 를 구축하고 활성화한다.
- DISABLE
    - Index 를 비활성화한다.
    - Index 가 사용하던 extent 를 모두 반납한다.
    - DML과 SELECT 에서 해당 index 를 사용하지 않는다.

<a id="aa0cf47546836389"></a>
### 설명

Key constraint를 구성하기 위해 생성한 index 는 ALTER CONSTRAINT 구문을 사용하여 관리해야 한다.

```
CREATE TABLE t1 ( pk INTEGER PRIMARY KEY );
COMMIT;

gSQL> \desc t1

COLUMN_NAME TYPE         IS_NULLABLE
----------- ------------ -----------
PK          NUMBER(10,0) FALSE      

INDEX_NAME           TABLESPACE_NAME INDEX_TYPE IS_UNIQUE COLUMNS
-------------------- --------------- ---------- --------- -------
T1_PRIMARY_KEY_INDEX MEM_TEMP_TBS    BTREE      TRUE      PK     

CONSTRAINT_NAME CONSTRAINT_TYPE ASSOCIATED_INDEX     COLUMNS
--------------- --------------- -------------------- -------
T1_PRIMARY_KEY  PRIMARY KEY     T1_PRIMARY_KEY_INDEX PK

gSQL> ALTER INDEX T1_PRIMARY_KEY_INDEX DISABLE;
ERR-42000(16050): cannot modify index used for enforcement of unique/primary/foreign key : 
ALTER INDEX T1_PRIMARY_KEY_INDEX DISABLE
            *
ERROR at line 1:

gSQL> ALTER TABLE t1 ALTER CONSTRAINT t1_primary_key NOT ENFORCED;
Table altered.
```

<a id="eb708243a970d6a3"></a>
### 사용 예

인덱스를 비활성화한다.

```
CREATE TABLE t1 ( c1 INTEGER );
CREATE INDEX idx1 ON t1(c1);

gSQL> ALTER INDEX idx1 DISABLE;
Index altered.
```

<a id="7f4c40b0ef3bf74e"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="b11b2400b97c242f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER INDEX](#73ef1debf9756149)
- [ALTER TABLE name ALTER CONSTRAINT](#75005eef58445700)

<a id="56aed70ce2b90a69"></a>
## ALTER INDEX name REBUILD

<a id="0b0a036342036393"></a>
### 기능

인덱스를 재구축한다.

<a id="e9ee452c1d6e40ba"></a>
### 구문

```
<rebuild index statement> ::=
    ALTER INDEX index_name REBUILD
        [ ONLINE | OFFLINE ]
        [ <index attributes> [...] ]
        [ TABLESPACE tablespace_name ]
        [ AT <domain name> ]
    ;

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

<size clause> ::=
      integer [ K | M | G | T ]

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="839f402906f8a25c"></a>
### 사용 범위 및 접근 권한

&lt;rebuild index statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

인덱스가 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="8b85f7fdf3170ddd"></a>
### 구문 규칙 및 파라미터

<a id="51d6cd606a7d87aa"></a>
#### index_name

대상 인덱스의 이름이다.  
스키마 이름을 명시할 수 있으며, 생략할 경우 사용자의 기본 스키마 이름이 사용된다.

<a id="0e085ceab7623010"></a>
#### [ ONLINE | OFFLINE ]

인덱스를 재구축할 때, 해당 테이블에 DML을 허용할지 여부를 결정한다.

- ONLINE
    - INSERT, UPDATE, DELETE를 허용한다.
- OFFLINE
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE이다.

<a id="a03531561ee5c541"></a>
#### &lt;physical attribute clause&gt;

인덱스의 물리적 속성 정보를 정의한다.

- PCTFREE integer 
    - 정의 
        - 페이지 내 key 삽입으로 인한 페이지 분할 빈도를 조절하기 위해 예약된 공간이다.
    - 0에서 99까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

- INITRANS integer 
    - 정의 
        - 페이지에 동시 접근할 수 있는 초기 트랜잭션의 개수이다. 
        - 인덱스에 접근하는 사용자의 수가 적을 경우에는 INITRANS를 낮게 설정하고, 동시에 접근하는 사용자가 많을 경우에는 INITRANS를 높게 설정한다. 
        - 필요한 경우 설정된 MAXTRANS까지 자동으로 늘어난다. 
    - 1 부터 32 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

- MAXTRANS integer 
    - 정의 
        - 페이지에 동시 접근할 수 있는 트랜잭션의 최대 개수이다. 
    - 1 부터 32 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

<a id="edebca6ed15adde0"></a>
#### &lt;segment attr clause&gt;

인덱스가 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer
    - 정의
        - 인덱스를 생성할 때 초기에 할당할 물리적 공간의 크기를 기술한다.
        - integer 값이 EXTENT 두 개 이하인 경우, extent 두 개 크기로 설정된다.
        - integer 값이 EXTENT 두 개 보다 큰 경우, TABLESPACE의 EXTENT 크기에 맞춰 (aligned) 설정된다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

- NEXT integer
    - 정의
        - 인덱스에 물리적 공간을 추가할 경우 할당할 물리적 공간의 크기를 기술한다.
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT크기가 8192 bytes일 경우 'NEXT 100'은 실제 8192 bytes로 작동한다.)
        - NEXT는 현재 인덱스가 사용할 수 있는 남은 공간의 크기 (MAXEXTENTS의 크기에서 현재 사용하고 있는 공간의 크기를 뺀 크기)에 따라 다음과 같이 작동한다.  
      - 남은 공간의 크기가 0인 경우 더 이상 공간을 확장하지 못한다.  
      - 남은 공간의 크기가 0보다 크고 NEXT보다 작은 경우 남은 공간의 크기만큼 할당한다.  
      - 남은 공간의 크기가 NEXT 보다 클 경우 NEXT의 크기만큼 할당한다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

<a id="027d6d9480bbf36e"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="dde8770f1c93d708"></a>
#### NOPARALLEL | PARALLEL [ integer ]

인덱스가 재구축되는 동안 사용될 thread의 개수를 지정한다.

- NOPARALLEL 
    - 인덱스를 병렬로 재구축하지 않는다. 
- PARALLEL [integer] 
    - 인덱스를 병렬로 재구축한다. 
    - integer가 생략되거나 0으로 지정된 경우에는 INDEX_BUILD_PARALLEL_FACTOR 프로퍼티를 따른다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - 만약 integer나 프로퍼티의 값이 0인 경우에는 시스템이 최적값을 결정한다.
- 명시하지 않을 경우, 기본값은 NOPARALLEL이다.

<a id="99cfed40ef74258a"></a>
#### TABLESPACE tablespace_name

인덱스가 재구축될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - tablespace_name이 data tablespace면 LOGGING 인덱스로 재구축된다.
    - tablespace_name이 temporary tablespace 또는 nologging tablespace면 NOLOGGING 인덱스로 재구축된다.
- TABLESPACE 절을 생략할 경우, 기존 인덱스의 tablespace로 설정된다.

<a id="964e79575d4746cb"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.  
&lt;index attributes&gt; 와 함께 사용할 수 없다.

<a id="ed13c139cf95e95c"></a>
### 설명

- 인덱스 단편화 제거
    - 인덱스에 DML이 빈번하게 수행되는 경우, 인덱스 페이지에 단편화가 발생할 수 있다. 유효한 데이터에 비해 트리가 지나치게 커진 경우, 인덱스 용량은 커지고 성능은 하락한다. 이 경우 인덱스를 재구축하면 인덱스 페이지의 단편화를 해결하여 인덱스 용량을 줄이고 인덱스의 성능을 회복할 수 있다.
- 인덱스의 테이블스페이스 변경
    - 기존에 생성된 인덱스의 테이블스페이스를 변경할 수 있다.
    - 단, 테이블스페이스의 TEMPORARY 여부에 따라 로깅 여부를 적절하게 설정해주어야 한다.
- 인덱스의 로깅 설정 변경
    - LOGGING 인덱스로 변경하려면, data tablespace를 TABLESPACE 옵션에 지정해줘야 한다.
    - NOLOGGING 인덱스로 변경하려면, temporary tablespace 또는 nologging tablespace를 TABLESPACE 옵션에 지정해줘야 한다.
- 유효하지 않은 shard 관련 key들을 제거
    - Shard가 변경되는 작업을 수행한 경우, 변경되기 전 shard와 관련된 key들이 인덱스에 남아있을 수 있다. 이것들을 제거하지 않고 쌓아두면 shard sequence exceed 에러가 발생할 수 있다. 이 문제는 shard가 빈번하게 변경되는 경우에 발생하는데, 인덱스를 재구축하는 방식으로 해결할 수 있다.

<a id="356909bdabeb7813"></a>
### 사용 예

다음은 인덱스의 로깅 설정과 테이블스페이스를 변경하는 예이다.

```
gsql> SELECT INDEX_NAME, TABLESPACE_NAME FROM INDEXES AS IDX, TABLESPACES AS TBS WHERE IDX.TABLESPACE_ID = TBS.TABLESPACE_ID AND IDX.INDEX_NAME = 'T1X';

INDEX_NAME TABLESPACE_NAME
---------- ---------------
T1X        MEM_TEMP_TBS   

1 row selected.

gsql> ALTER INDEX T1X REBUILD TABLESPACE MEM_DATA_TBS;

SELECT INDEX_NAME, TABLESPACE_NAME FROM INDEXES AS IDX, TABLESPACES AS TBS WHERE IDX.TABLESPACE_ID = TBS.TABLESPACE_ID AND IDX.INDEX_NAME = 'T1X';

INDEX_NAME TABLESPACE_NAME
---------- ---------------
T1X        MEM_DATA_TBS   

1 row selected.
```

<a id="54b4b44a90db3244"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="285b9f54a92ce85f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](19-sql-references-c-g.md#1b99962ed891aa4f)
- [ALTER INDEX](#73ef1debf9756149)
- [DROP INDEX](19-sql-references-c-g.md#d01836ffe196ec14)

<a id="ce4a5d821138cd3a"></a>
## ALTER INDEX name RENAME TO

<a id="bf0409f362311222"></a>
### 기능

인덱스의 이름을 변경한다.

<a id="50147b87a730bc2c"></a>
### 구문

```
<rename index statement> ::=
    ALTER INDEX index_name
        RENAME TO new_index_name
    ;
```

<a id="654fe664d37e84c3"></a>
### 사용 범위 및 접근 권한

&lt;rename index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="7cf857f126cf6bf1"></a>
### 구문 규칙 및 파라미터

<a id="d89d624acdd0b4a0"></a>
#### index_name

대상 인덱스의 이름이다.  
스키마 이름을 기술할 수 없으며, 기존 인덱스와 동일한 스키마 이름을 갖는다.

<a id="6100397b0356758c"></a>
#### new_index_name

새로운 인덱스의 이름이며 스키마 내에서 유일한 인덱스 이름이어야 한다.

<a id="d59b18a78061f745"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="418898ca31662c63"></a>
### 사용 예

다음은 인덱스의 이름을 변경하는 예이다.

```
gSQL> ALTER INDEX t1_idx1 RENAME TO idx_t1_id;

Index altered.
```

<a id="910ddb106027a0aa"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="fd52a98447a9d8fc"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](19-sql-references-c-g.md#1b99962ed891aa4f)
- [ALTER INDEX](#73ef1debf9756149)
- [DROP INDEX](19-sql-references-c-g.md#d01836ffe196ec14)

<a id="ba7154f8d22befe2"></a>
## ALTER INDEX name STORAGE

<a id="1991b0ca643fb4f2"></a>
### 기능

인덱스의 물리적 속성을 변경한다.

<a id="c10c3447b50522c5"></a>
### 구문

```
<alter index physical attribute statement> ::=
    ALTER INDEX index_name
    | <physical attribute clause>
    | [ STORAGE ( <segment attr clause> [...] ) ]
    ;

<physical attribute clause> ::=
      PCTFREE integer
    | INITRANS integer
    | MAXTRANS integer

<segment attr clause> ::=
      INITIAL <size_clause>
    | NEXT <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]
```

<a id="f590a2add31405e8"></a>
### 사용 범위 및 접근 권한

&lt;alter index physical attribute statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="aa74ac2144f68fe8"></a>
### 구문 규칙 및 파라미터

<a id="732d6e9136a96193"></a>
#### index_name

대상 인덱스의 이름이다.

<a id="a7ae965f99f24260"></a>
#### &lt;physical attribute clause&gt;

인덱스의 물리적 속성 정보를 정의한다.

- PCTFREE integer 
    - 정의 
        - 페이지 내에 key 삽입으로 인한 페이지 분할 빈도를 조절하기 위해 예약된 공간이다. 
        - 인덱스 bottom-up 빌드시에만 적용된다. 
    - 0 에서 99 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기본값은 DEFAULT_INDEX_PCTFREE property에 설정된 값을 사용한다.

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

<a id="90b5ceb2f5bdd16f"></a>
#### &lt;segment attr clause&gt;

인덱스가 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer 
    - 정의 
        - 인덱스를 생성할 때 초기에 할당할 물리적 공간의 크기를 기술한다. 
        - integer 값이 EXTENT 두 개 이하인 경우, extent 두 개 크기로 설정된다.
        - integer 값이 EXTENT 두 개 보다 큰 경우, TABLESPACE의 EXTENT 크기에 맞춰 (aligned) 설정된다.
        - 인덱스 bottom-up 빌드시에만 적용된다. 
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.

- NEXT integer
    - 정의
        - 인덱스의 물리적 공간을 추가할 경우 할당할 물리적 공간의 크기를 기술한다.
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT 크기가 8192 bytes일 경우 'NEXT 100'은 실제 8192 bytes로 동작한다.)
        - NEXT는 현재 인덱스가 사용할 수 있는 남은 공간의 크기 (MAXEXTENTS의 크기에서 현재 사용하고 있는 공간의 크기를 뺀 크기)에 따라 아래와 같이 동작한다.  
      - 남은 공간의 크기가 0인 경우 더 이상 공간을 확장하지 못한다.  
      - 남은 공간의 크기가 0보다 크고 NEXT보다 작은 경우 남은 공간의 크기만큼 할당한다.  
      - 남은 공간의 크기가 NEXT 보다 클 경우 NEXT의 크기만큼 할당한다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.

<a id="337216328c64cba1"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: kilobytes 
- M: megabytes 
- G: gigabytes 
- T: terabytes

<a id="c8ee486b82be7556"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="7dfadd89d11a9fa3"></a>
### 사용 예

다음은 인덱스의 물리적 속성을 변경하는 예이다.

```
gSQL> ALTER INDEX idx_t1_id PCTFREE 10 INITRANS 4 MAXTRANS 8;

Index altered.
```

<a id="b6dcd8121cdf84f9"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="0313f71702a96146"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](19-sql-references-c-g.md#1b99962ed891aa4f)
- [ALTER INDEX](#73ef1debf9756149)
- [DROP INDEX](19-sql-references-c-g.md#d01836ffe196ec14)

<a id="5acd39cd4aba40d6"></a>
## ALTER PROFILE

<a id="51f1a66d614953e3"></a>
### 기능

비밀번호 관리 방법을 변경한다.

<a id="02356a59d729777a"></a>
### 구문

```
<alter profile statement> ::= 
    ALTER PROFILE profile_name LIMIT 
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

<a id="1b33f907907e01b8"></a>
### 사용 범위 및 접근 권한

&lt;alter profile statement&gt; 구문을 수행하려면 사용자에게 ALTER PROFILE ON DATABASE 권한이 있어야 한다.

<a id="084c900569dd2dfe"></a>
### 구문 규칙 및 파라미터

<a id="fb4d0e8ca5e8d293"></a>
#### profile_name

변경할 profile의 이름이다.

<a id="06dfc84be90bbb8d"></a>
#### FAILED_LOGIN_ATTEMPTS

로그인 연속 실패 허용 횟수를 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#46ce60330a91c0ff) 구문을 참조한다.

<a id="ee71ba51c8f0f2a5"></a>
#### PASSWORD_LOCK_TIME

로그인에 연속적으로 실패한 후에 계정이 잠기는 기간 (day)을 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#46ce60330a91c0ff) 구문을 참조한다.

<a id="7a62b3d30c17fdcb"></a>
#### PASSWORD_LIFE_TIME

비밀번호의 유효 기간 (day)을 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#46ce60330a91c0ff) 구문을 참조한다.

<a id="2eeb325dffb03f18"></a>
#### PASSWORD_GRACE_TIME

PASSWORD_LIFE_TIME 이후에 로그인 할 때 비밀번호 만료를 유예하는 기간을 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#46ce60330a91c0ff) 구문을 참조한다.

<a id="c06afb3e36658830"></a>
#### PASSWORD_REUSE_MAX

이전 비밀번호를 재사용하려 할 때 재사용할 수 없는 최근 비밀번호 개수를 명시한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#46ce60330a91c0ff) 구문을 참조한다.

<a id="8471a3d2f2c20a60"></a>
#### PASSWORD_REUSE_TIME

이전 비밀번호를 재사용하기 위해 필요한 경과 기간을 명시한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#46ce60330a91c0ff) 구문을 참조한다.

<a id="4ba967c0e4c54276"></a>
#### PASSWORD_VERIFY_FUNCTION

비밀번호 복잡도 검증 방법을 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#46ce60330a91c0ff) 구문을 참조한다.

<a id="9932504b038a464e"></a>
### 사용 예

다음은 계정 잠금을 제어하기 위해 profile을 변경하는 예이다.

```
gSQL> ALTER PROFILE prof1 LIMIT
        FAILED_LOGIN_ATTEMPTS 3
        PASSWORD_LOCK_TIME 3;

Profile altered.

gSQL> COMMIT;

Commit complete.
```

다음은 비밀번호 만료를 제어하기 위해 profile을 변경하는 예이다

```
gSQL> ALTER PROFILE prof1 LIMIT
        PASSWORD_LIFE_TIME 90 
        PASSWORD_GRACE_TIME 7;

Profile altered.

gSQL> COMMIT;

Commit complete.
```

다음은 비밀번호 재사용 여부를 제어하기 위해 profile을 변경하는 예이다.

```
gSQL> ALTER PROFILE prof1 LIMIT
        PASSWORD_REUSE_MAX  DEFAULT
        PASSWORD_REUSE_TIME DEFAULT;

Profile altered.

gSQL> COMMIT;

Commit complete.
```

다음은 비밀번호 복잡도 검사를 제어하기 위해 profile을 변경하는 예이다.

```
gSQL> ALTER PROFILE prof1 LIMIT
        PASSWORD_VERIFY_FUNCTION KISA_VERIFY_FUNCTION;

Profile altered.

gSQL> COMMIT;

Commit complete.
```

<a id="04369f74d5d316c0"></a>
### 호환성

SQL 표준은 profile에 대한 개념을 다루지 않고 있다.

<a id="e762114e6fa7f16c"></a>
### 참조

관련 내용은 [DROP PROFILE](19-sql-references-c-g.md#6f593da79c49a927)을 참조한다.

<a id="8163a1ba93288c58"></a>
## ALTER SEQUENCE

<a id="690dccdb37bdd82c"></a>
### 기능

시퀀스를 변경한다.

<a id="7096f8a9f06bb88a"></a>
### 구문

```
<alter sequence generator statement> ::=
    ALTER SEQUENCE sequence_name <alter sequence generator options>
    ;

<alter sequence generator options> ::=
    <alter sequence generator option> [, ...]

<alter sequence generator option> ::=
      <alter sequence generator restart option>
    | <basic sequence generator option>

<alter sequence generator restart option> ::=
    RESTART [ WITH integer ]

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

<a id="f41884d575f979d5"></a>
### 사용 범위 및 접근 권한

&lt;alter sequence generator statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 시퀀스의 소유자 
- 시퀀스가 속한 스키마에 대해 (ALTER SEQUENCE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY SEQUENCE ON DATABASE

<a id="5eb721694148c5d4"></a>
### 구문 규칙 및 파라미터

<a id="00bf6cdce1f36a4c"></a>
#### sequence_name

변경할 시퀀스의 이름이다.  
schema_name.sequence_name과 같이 시퀀스가 속할 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="76329740529bd55e"></a>
#### &lt;alter sequence generator restart option&gt;

시퀀스의 다음 값 (NEXT VALUE)을 설정한다.  
단, [CREATE SEQUENCE](19-sql-references-c-g.md#00dc9608bfdd1466) 구문에서 정의한 START WITH의 값은 변경하지 않는다.

- RESTART 
    - 값을 명시하지 않을 경우, &lt;sequence generator definition&gt; 에서 정의한 START WITH의 값이 시퀀스의 다음 값으로 설정된다. 
- RESTART WITH integer 
    - integer 값을 시퀀스의 다음 값으로 설정한다. 
    - integer 값은 MINVALUE와 MAXVALUE 사이의 값이어야 한다.

&lt;alter sequence generator restart option&gt; 절을 명시하지 않은 경우, 시퀀스의 현재값을 기준으로 시퀀스의 속성을 변경한다.

<a id="117acd0b1e380a12"></a>
#### &lt;sequence generator increment by option&gt;

시퀀스 번호의 간격을 변경한다.  
다음과 같은 제약과 특징을 갖는다.

- 양수 또는 음수를 사용할 수 있으며, 0은 사용할 수 없다. 
- 간격의 절대값은 MINVALUE와 MAXVALUE의 차이보다 작아야 한다. 
- 양수일 경우 오름차순 시퀀스가 되고 음수일 경우 내림차순 시퀀스가 된다.

<a id="46037b9822e4d57d"></a>
#### &lt;sequence generator maxvalue option&gt;

시퀀스로 생성할 수 있는 최대값을 변경한다.   
단, MAXVALUE의 값이 시퀀스의 현재값보다 작지 않아야 한다.

- MAXVALUE integer 
    - 최대값의 범위는 64bit 정수의 최소값 (−9,223,372,036,854,775,808)에서 64bit 정수의 최대값(+9,223,372,036,854,775,807) 까지이다.
    - START WITH의 값과 같거나 크고, MINVALUE 값보다 커야 한다. 
- NO MAXVALUE | NOMAXVALUE 
    - 최대값을 다음과 같이 변경한다. 
        - 오름차순 시퀀스일 경우, 64 bit 정수의 최대값 (+9,223,372,036,854,775,807)이 된다. 
        - 내림차순 시퀀스일 경우, -1이 된다. 
        - NO MAXVALUE (SQL 표준)와 NOMAXVALUE는 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다.

<a id="60c99135ed113d5a"></a>
#### &lt;sequence generator minvalue option&gt;

시퀀스로 생성할 수 있는 최소값을 변경한다.   
단, MINVALUE의 값이 시퀀스의 현재값보다 크지 않아야 한다.

- MINVALUE integer 
    - 최소값의 범위는 64 bit 정수의 최소값 (−9,223,372,036,854,775,808)에서 64 bit 정수의 최대값(+9,223,372,036,854,775,807) 까지이다.
    - START WITH의 값과 같거나 작고, MAXVALUE 값보다 작아야 한다. 
- NO MINVALUE | NOMINVALUE 
    - 최소값을 다음과 같이 변경한다. 
        - 오름차순 시퀀스일 경우, 1이 된다. 
        - 내림차순 시퀀스일 경우, 64 bit 정수의 최소값 (−9,223,372,036,854,775,808)이 된다. 
    - NO MINVALUE (SQL 표준)와 NOMINVALUE는 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다.

<a id="f89d2ea41e40d16e"></a>
#### &lt;sequence generator cycle option&gt;

시퀀스의 값이 최대값 또는 최소값이 되었을 때, 계속 값을 생성할지 여부를 변경한다.

- CYCLE 
    - 오름차순 시퀀스가 최대값이 되었을 때, 최소값부터 다시 생성한다. 
    - 내림차순 시퀀스가 최소값이 되었을 때, 최대값부터 다시 생성한다. 
- NO CYCLE | NOCYCLE 
    - 최대값 또는 최소값이 되었을 때, 시퀀스 값을 생성할 수 없다. 
    - NO CYCLE (SQL 표준)과 NOCYCLE은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다.

<a id="aa4028ec780796e4"></a>
#### &lt;sequence generator cache option&gt;

시퀀스에 신속하게 접근하기 위해 메모리상에 미리 적재할 시퀀스 값의 개수를 정의한다.   
Database를 재구동할 때, 메모리상에 적재한 시퀀스 값은 유실되고 적재한 이후의 값부터 시작된다.

- CACHE integer 
    - CACHE 값은 2와 같거나 커야하고 
    - CYCLE이 존재할 경우 CACHE 값이 CYCLE의 길이보다 크지 않아야 한다. 
        - CYCLE의 길이: CEIL(MAXVALUE - MINVALUE) / ABS(INCREMENT) 
- NO CACHE | NOCACHE 
    - 메모리 상에 시퀀스값을 미리 적재하지 않는다.

<a id="02d5794c0f45dae0"></a>
### 설명

[CREATE SEQUENCE](19-sql-references-c-g.md#00dc9608bfdd1466) 구문에서 정의한 시퀀스 속성 중 START WITH는 변경할 수 없다.  
START WITH 속성을 변경하려면 [DROP SEQUENCE](19-sql-references-c-g.md#a567fca70147b0b5) 구문을 수행한 후에 [CREATE SEQUENCE](19-sql-references-c-g.md#00dc9608bfdd1466) 구문을 사용하여 다시 생성해야 한다.

<a id="7ada12a98806d389"></a>
### 사용 예

다음은 RESTART 옵션으로 시퀀스 값을 재시작하고 이를 이용하여 ID 값을 새로 부여하는 예이다.

```
gSQL> SELECT id, name FROM t1 ORDER BY 1;

 ID NAME  
--- ------
 10 leekmo
 42 mkkim 
 51 jhkim 
172 ehpark

4 rows selected.


gSQL> ALTER SEQUENCE seq1 RESTART;

Sequence altered.


gSQL> UPDATE t1 SET id = seq1.NEXTVAL;

4 rows updated.


gSQL> SELECT id, name FROM t1 ORDER BY 1;

ID NAME  
-- ------
 1 leekmo
 2 mkkim 
 3 jhkim 
 4 ehpark

4 rows selected.
```

<a id="7bd30c6a0a0b83b1"></a>
### 호환성

SQL 표준에서는 CACHE/ NO CACHE 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="1007f4428657d0fc"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T176 | Sequence generator support | O |
| T177 | Sequence generator support: simple restart option | O |

<a id="a622696ef1a21eed"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE SEQUENCE](19-sql-references-c-g.md#00dc9608bfdd1466)
- [DROP SEQUENCE](19-sql-references-c-g.md#a567fca70147b0b5)

<a id="c7baf28afdb23d47"></a>
## ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

<a id="6d717ccc12fd74ad"></a>
### 기능

세션에서 재사용하기 위해 catching 된 모든 공간들을 해당 tablespace로 반환한다.

<a id="9ff3a280c0dc380c"></a>
### 구문

```
<alter session cleanup global temporary segment pool statement> ::=
    ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL
    ;
```

<a id="00058efe1ba8887c"></a>
### 설명

수행된 세션에서 segment cache의 segment들만 cleanup한다.

<a id="d9cfb79718b2cda5"></a>
### 사용 예

다음은 세션 segment cache를 cleanup하는 예이다.

```
gSQL> ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

Session altered.
```

<a id="0d409632482105fd"></a>
### 호환성

SQL 표준에서는 global temporary table, global temporary index의 segment cache 개념을 정의하지 않고 있다.

<a id="a08a258894e3186c"></a>
### 참조

관련 내용은 [Global Temporary Table](13-sql-objects.md#997b0933993a63f4) 을 참조한다.

<a id="2a4ad434eedabea8"></a>
## ALTER SESSION SET property_name

<a id="58190045f72ce5c1"></a>
### 기능

세션의 프로퍼티 값을 설정한다.

<a id="84991c6fc6d51b4c"></a>
### 구문

```
<alter session set statement> ::=
    ALTER SESSION SET <property name> { = <property value> | TO DEFAULT }
    ;
```

<a id="3b1fa72076a57df0"></a>
### 구문 규칙 및 파라미터

<a id="c255daed1d675a46"></a>
#### &lt;property name&gt;

설정할 프로퍼티 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#e95fbf953ce3e17d) 장을 참조한다.

<a id="68c6cacc809de56c"></a>
#### &lt;property value&gt;

설정할 프로퍼티 값이다.

<a id="ecfabeb17f6c8649"></a>
#### TO DEFAULT

세션 프로퍼티 값을 시스템 프로퍼티 값으로 설정한다.

<a id="85e2903a0e490f4e"></a>
### 설명

각 property에 대한 자세한 설명은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#e95fbf953ce3e17d) 장을 참조한다.

<a id="6c71e7219c90d025"></a>
### 사용 예

다음은 HINT_ERROR 속성을 설정하여 hint 구문에 오류가 있을 경우 에러가 발생하는 예이다.

```
gSQL> ALTER SESSION SET HINT_ERROR = ON;

Session altered.

gSQL> SELECT /*+ INDEX( t1, invalid_index ) */ name FROM t1 WHERE id = 1;

ERR-42000(16058): not applicable hint : 
SELECT /*+ INDEX( t1, invalid_index ) */ name FROM t1 WHERE id = 1
           *
ERROR at line 1:
```

다음은 세션 프로퍼티 값을 시스템 프로퍼티의 값으로 설정하는 예이다.

```
gSQL> ALTER SESSION SET HINT_ERROR TO DEFAULT;

Session altered.
```

<a id="3066ed73bdd17b53"></a>
### 호환성

SQL 표준에서는 세션 프로퍼티 개념을 정의하지 않고 있다.

<a id="2720ddc65c652637"></a>
### 참조

관련 내용은 [ALTER SESSION SET property_name](#2a4ad434eedabea8) 을 참조한다.

<a id="a9639e899e14c803"></a>
## ALTER SYSTEM CANCEL SESSION

<a id="7898029a57c620e6"></a>
### 기능

세션에서 수행되고 있는 작업을 취소한다.

<a id="6b7711b42fa35b30"></a>
### 구문

```
<alter system cancel session statement> ::=
      ALTER SYSTEM CANCEL SESSION [<member_position>,] <session_id>,
          <serial#> [AT <domain_name>]
    ;
```

<a id="7b061959298c9049"></a>
### 사용 범위 및 접근 권한

&lt;alter system cancel session statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="1ce86d2e39de0ae2"></a>
### 구문 규칙 및 파라미터

<a id="4fec15647e36bc01"></a>
#### &lt;member_position&gt;

Cluster database에서만 유효한 구문이다.  
Cancel 대상이 되는 세션의 member position 이다.

<a id="092fc6292be43b4a"></a>
#### &lt;session_id&gt;

세션의 ID 이다.

<a id="ff92744a9a354856"></a>
#### &lt;serial#&gt;

세션의 SERIAL NUMBER 이다.

<a id="c49bb386823d821a"></a>
#### &lt;domain name&gt;

Cluster database에서만 유효한 구문이다.  
구문을 수행할 멤버나 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="6fc1427a17c063a6"></a>
### 설명

CANCEL SESSION은 driver session에만 적용되고 system session이나 cluster session에는 적용되지 않는다.  
만약 system session이나 cluster session에 해당 구문을 수행하면 다음과 같은 에러가 발생한다.

```
gSQL> ALTER SYSTEM CANCEL SESSION 1,1;

ERR-42000(16603): system session cannot be canceled
```

<a id="57f16aea24f50524"></a>
### 사용 예

다음은 &lt;alter system cancel session statement&gt; 구문을 수행하는 예이다.

```
gSQL> SELECT USER_NAME, SESSION_ID, SERIAL_NO, SESSION_STATUS, PROGRAM_NAME FROM V$SESSION WHERE USER_NAME = 'TEST';

USER_NAME SESSION_ID SERIAL_NO SESSION_STATUS PROGRAM_NAME
--------- ---------- --------- -------------- ------------
TEST              28        10 CONNECTED      gsql        
TEST              29         1 CONNECTED      gsqlnet     

2 rows selected.

gSQL> ALTER SYSTEM CANCEL SESSION 28, 10;

System altered.
```

<a id="cb8e035c8d45232b"></a>
### 호환성

SQL 표준에서는 ALTER SYSTEM CANCEL SESSION 구문을 정의하지 않고 있다.

<a id="c8f23e33be79fc47"></a>
## ALTER SYSTEM CHECKPOINT

<a id="d4e817b145965633"></a>
### 기능

CHECKPOINT를 수행한다.

<a id="7a551105aea0e096"></a>
### 구문

```
<alter system checkpoint statement> ::=
    ALTER SYSTEM CHECKPOINT
    [ AT <domain name> ]
    ;
```

<a id="1dd79e33e19265fe"></a>
### 사용 범위 및 접근 권한

&lt;alter system checkpoint statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="49a8c6baa21bd28d"></a>
### 구문 규칙 및 파라미터

<a id="d4f7fc538cd8ebba"></a>
#### &lt;alter system checkpoint statement&gt;

CHECKPOINT는 commit 된 트랜잭션들이 변경한 모든 데이터가 디스크에 기록되는 것을 보장하는 연산이다.

- 데이터베이스가 OPEN 상태여야 한다.
- 데이터베이스가 TDS 모드여야 한다.
- 전체 백업이 진행중일 때는 변경된 페이지가 데이터 파일에 기록되지 않고, REDO 로그와 제어파일만 디스크에 기록된다. 만약 이러한 상태에서 서버가 비정상 종료되는 경우에는 미디어 복구를 수행해야 한다.

<a id="dc6f4f354a006372"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="9dd76113132b511a"></a>
### 설명

체크포인트 (checkpoint) 연산은 commit 된 트랜잭션들이 변경한 모든 내용을 디스크에 기록함으로써 시스템 장애시 신속한 복구를 가능하게 한다.

<a id="23b405f6c06e68b8"></a>
### 사용 예

다음은 CHECKPOINT를 수행하는 예이다.

```
ALTER SYSTEM CHECKPOINT;
```

<a id="287230b35a3d7a08"></a>
### 호환성

SQL 표준에서는 CHECKPOINT 개념을 정의하지 않고 있다.

<a id="7929e935d5c84bc4"></a>
## ALTER SYSTEM CLEANUP BUFFER_CACHE

<a id="faa14f59241351d6"></a>
### 기능

Buffer cache에서 free 가능한 모든 buffer page들을 비운다.

<a id="084b5f16f864ef4a"></a>
### 구문

```
<alter system cleanup buffer_cache statement> ::=
    ALTER SYSTEM CLEANUP BUFFER_CACHE
    [ AT <domain name> ]
    ;
```

<a id="feb1d03da87e7764"></a>
### 사용 범위 및 접근 권한

&lt;alter system cleanup buffer_cache statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="94612af0bb53c904"></a>
### 구문 규칙 및 파라미터

<a id="bca74d7a6e0063b8"></a>
#### &lt;alter system cleanup buffer_cache statement&gt;

해당 구문 규칙이나 파라미터가 존재하지 않는다.

<a id="da71a2b06cff8705"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="1786b92ea8d21fdd"></a>
### 설명

Buffer에 캐시된 free 가능한 모든 buffer page들을 flush하고 free 한다.

> 성능 측정 전에 buffer cache를 비우는 목적으로 사용해야 한다.   
> 운영 중인 서버에서 사용할 경우 성능에 치명적인 영향을 미칠 수 있다.

<a id="5561071ef80b033b"></a>
### 사용 예

다음은 CLEANUP BUFFER_CACHE을 수행하는 예이다.

```
ALTER SYSTEM CLEANUP BUFFER_CACHE;
```

<a id="4e92a9b0e4bef31f"></a>
### 호환성

SQL 표준에서는 CLEANUP BUFFER_CACHE의 개념을 정의하지 않고 있다.

<a id="de7bb7d02b361c49"></a>
## ALTER SYSTEM CLEANUP PLAN

<a id="8f10b5ea0b54ff6e"></a>
### 기능

모든 SQL plan을 정리한다.

<a id="0c60089dd0b0e582"></a>
### 구문

```
<alter system cleanup plan statement> ::=
    ALTER SYSTEM CLEANUP PLAN
    [ AT <domain name> ]
    ;
```

<a id="52da430792a94cb3"></a>
### 사용 범위 및 접근 권한

&lt;alter system cleanup plan statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="10b4098fe7e2f184"></a>
### 구문 규칙 및 파라미터

<a id="4c0f1029944e3d0c"></a>
#### &lt;alter system cleanup plan statement&gt;

해당 구문 규칙이나 파라미터가 존재하지 않는다.

<a id="6037d742b61d3e38"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="8107918a571e3550"></a>
### 설명

캐시되어 있는 모든 SQL plan을 삭제한다.

<a id="c354ffffa6cd2ec1"></a>
### 사용 예

다음은 CLEANUP PLAN을 수행하는 예이다.

```
ALTER SYSTEM CLEANUP PLAN;
```

<a id="0ff5e55230eb01f6"></a>
### 호환성

SQL 표준에서는 CLEANUP PLAN의 개념을 정의하지 않고 있다.

<a id="882fa4fbc63a5fde"></a>
## ALTER SYSTEM FLUSH LOGS

<a id="cdc4ae951838a6ad"></a>
### 기능

데이터베이스 로그 버퍼에 저장된 redo log를 로그 파일에 기록하도록 요청한다.

<a id="edc2cf88ab20a738"></a>
### 구문

```
<alter system flush flush logs statement> ::=
    ALTER SYSTEM FLUSH LOGS [ AT domain_name ]
    ;
```

<a id="357591e733dade25"></a>
### 사용 범위 및 접근 권한

&lt;alter system flush logs statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="85e77b07eecaf664"></a>
### 구문 규칙 및 파라미터

<a id="366341c14b57c504"></a>
#### &lt;alter system flush logs statement&gt;

트랜잭션들이 생성한 로그를 로그 파일에 기록하도록 요청한다.

- 데이터베이스가 OPEN 상태여야 한다.

<a id="5ebf1a84cd2dd6da"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="c899491709662999"></a>
### 설명

로그 버퍼에 기록된 redo log를 online log file에 기록하도록 요청하고, 기록이 완료될 때까지 대기한다.   
로그 기록이 완료되어야 하는 경우에 사용한다.

<a id="dd808c61b2caf031"></a>
### 사용 예

다음은 FLUSH LOGS를 수행하는 예이다.

```
ALTER SYSTEM FLUSH LOGS;
```

<a id="86cb38a6fb462bb6"></a>
### 호환성

SQL 표준에서는 FLUSH LOGS의 개념을 정의하지 않고 있다.

<a id="2751a9e856140404"></a>
## ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER

<a id="e00f2e6bee9fd5cb"></a>
### 기능

복구 불가능한 클러스터 멤버를 지정한다.

<a id="770483173c6ae178"></a>
### 구문

```
<alter system irrecoverable cluster member statement> ::=
    ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER <domain name>
    ;
```

<a id="aec2c89ee506e4d6"></a>
### 사용 범위 및 접근 권한

&lt;alter system irrecoverable cluster member statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="5ad8576d7b959b06"></a>
### 구문 규칙 및 파라미터

<a id="039689cf0bfa5dcf"></a>
#### &lt;alter system irrecoverable cluster member statement&gt;

데이터베이스는 MOUNT 상태여야 한다.

<a id="fc33b3065e146223"></a>
#### &lt;domain name&gt;

복구 불가능한 멤버 이름이다.  
그룹 내의 모든 멤버들을 복구 불가한 멤버로 지정할 수 없다.

<a id="90ee21a4c8fa663d"></a>
### 설명

복구 불가능한 멤버로 인해 클러스터 재시작에 실패하는 경우 해당 멤버를 제외하고 시스템을 재시작하기 위해 사용한다. 시스템 재시작에 성공한 후에는 반드시 [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#8ce707cabe9dc37a) 구문을 이용해 해당 멤버를 삭제해야 한다.

이 구문은 PREPARE 상태의 global transaction (in-doubt transaction) 이 COMMIT 여부를 결정하기 위해 원격 멤버에 상태 정보를 요청했으나, 해당 멤버가 복구 불가능한 상태여서 COMMIT 여부를 판단할 수 없는 경우에, 그 멤버를 제외하고 COMMIT 여부를 판단하기 위해 사용된다.

<a id="73b82b31dca30a74"></a>
### 사용 예

다음은 여섯 개의 노드 중 하나가 복구 불가능한 상태이고, 나머지 다섯 개 노드의 트랜잭션 상태가 PREPARE일 때, 로컬의 startup 단계를 올리면 에러가 발생하는 예이다.

```
gSQL> ALTER SYSTEM OPEN LOCAL DATABASE;

ERR-HY000(56013): cannot resolve in-doubt transaction '0.1.45613060' because '1' members of the total '5' remote cluster members were disconnected - connection map was '011110'
```

만일 이 상태에서 복구 불가능한 멤버를 제외하고 startup 하려면 다음과 같이 수행한다.

```
gSQL> ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER G3N2;

System altered.

gSQL> ALTER SYSTEM OPEN LOCAL DATABASE;

System altered.
```

<a id="9d87837f0a71ef24"></a>
### 호환성

SQL 표준에서는 IRRECOVERABLE CLUSTER MEMBER의 개념을 정의하지 않고 있다.

<a id="d64c686b2011e181"></a>
## ALTER SYSTEM JOIN DATABASE

<a id="f588662faa7458f3"></a>
### 기능

비활성화된 특정 cluster member를 cluster system에 다시 포함한다.

<a id="4f27e7bebb80b87a"></a>
### 구문

```
<alter system join database statement> ::=
    ALTER SYSTEM JOIN DATABASE 
    ;
```

<a id="71a7bf658016d1b7"></a>
### 사용 범위 및 접근 권한

Cluster system 에서 수행할 수 있다.

&lt;alter system join database statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="c40d73ae110f16c3"></a>
### 설명

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우
- Cluster system에 포함된 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

특정 cluster member가 inactive인 상태에서 해당 member를 다음과 같은 절차를 거쳐 cluster system에 포함시킬 수 있다.

- 구동되지 않은 cluster member를 local open 단계로 구동한다.

```
$ gsql sys gliese --as sysdba --dsn=G3N2
gSQL> \startup
```

- &lt;alter system join database statement&gt; 구문을 사용하여 cluster system에 포함시킨다.

```
$ gsql sys gliese --as sysdba --dsn=G3N2
gSQL> ALTER SYSTEM JOIN DATABASE;
```

&lt;alter system join database statement&gt; 구문은 local open으로 구동된 inactive cluster member를 shutdown 하지 않고 cluster system에 참여시키려고 할 때 사용한다.

Inactive cluster member가 다시 cluster system에 참여하려면 cluster system과 inactive cluster member의 database 상태가 동일해야 한다.

Cluster system에서 database를 변경하는 트랜잭션이 완료된 후에는 inactive cluster member가 cluster system에 다시 참여할 수 없다.

다수의 inactive cluster member가 존재하는 경우, cluster system을 정상적으로 운영하기 위해 다음과 같은 순서로 inactive cluster member를 정리해야 한다.

1. Cluster system에 참여할 수 있는 inactive cluster member를 JOIN 한다.

```
gSQL> ALTER SYSTEM JOIN DATABASE;
```

2. Cluster system에 참여할 수 없는 inactive cluster member들을 DROP 한다.

```
gSQL> ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS;
```

&lt;alter database drop inactive cluster member statement&gt; 구문을 수행하면 모든 inactive cluster member가 cluster system에서 제거되므로, DROP 하기 전에 참여 가능한 모든 inactive cluster member를 cluster system에 포함시켜야 한다.

&lt;alter system join database statement&gt; 구문은 사용자 테이블들을 하나씩 online 상태로 변경한다.   
하지만 모든 테이블을 online 상태로 전환하지 못할 경우, 다음과 같은 warning 메시지를 출력한다.

```
gSQL> ALTER SYSTEM JOIN DATABASE;

ERR-42000(16405): of the total '5' tables in the database, '2' tables need to be rebalanced : 
  concurrent execution : 0 
  inactive member      : 0 
  replica usablility   : 0 
  offline tablespace   : 0 
  low table scn        : 2 
  others               : 0
```

각 warning 메시지의 의미는 다음과 같다:

- concurrent execution
    - 다른 세션과의 동시성 문제로 인해 실패한 경우
- inactive member
    - 모든 active member 의 replica 가 offline 상태이고 inactive member 가 존재하는 경우
- replica usability
    - Local replica 가 unusable 상태이거나
    - 모든 active member 의 replica 들이 unusable 상태인 경우
- offline tablespace 
    - Local replica 가 오프라인 된 tablespace 에 만들어진 경우
- low table scn
    - 로컬 테이블의 scn이 원격 테이블보다 작은 경우
- others
    - 위에 명시된 원인 외의 기타 사유

<a id="8f18503c3c0b3c2f"></a>
### 사용 예

```
gSQL> ALTER SYSTEM JOIN DATABASE;
```

<a id="53707ea8baabfb2e"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="522317c2e5cc240f"></a>
### 참조

관련 내용은 [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#8ce707cabe9dc37a)를 참조한다.

<a id="864ac81bb69e4ec0"></a>
## ALTER SYSTEM [KILL | DISCONNECT] SESSION

<a id="ec168d61d5b4c878"></a>
### 기능

세션을 종료한다.

<a id="ce4ef33734b6091b"></a>
### 구문

```
<alter system end session statement> ::=
      ALTER SYSTEM DISCONNECT SESSION [<member_position>,] <session_id>,
          <serial#> [<disconnect_option>] [AT <domain_name>]
    |  ALTER SYSTEM KILL SESSION [<member_position>,] 
           <session_id>, <serial#>  [AT <domain_name>]    ;

<disconnect_option> ::=
      POST_TRANSACTION
    | IMMEDIATE
```

<a id="6e4d54c9e5235c81"></a>
### 사용 범위 및 접근 권한

&lt;alter system end session statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="88462f96d33345c8"></a>
### 구문 규칙 및 파라미터

<a id="e812151358d929f1"></a>
#### &lt;member_position&gt;

Cluster 환경에서 disconnect/ kill 대상이 되는 세션의 member position 이다.

<a id="84861cb1d5dff0d6"></a>
#### &lt;session_id&gt;

세션의 ID 이다.

<a id="ac1d10b4a290008d"></a>
#### &lt;serial#&gt;

세션의 SERIAL NUMBER 이다.

<a id="0779a3a1d104f541"></a>
#### &lt;disconnect_option&gt;

- POST_TRANSACTION: 트랜잭션 완료 후, 세션을 종료한다.
- IMMEDIATE: 트랜잭션 완료를 기다리지 않고 바로 세션을 종료한다.

&lt;disconnect_option&gt;이 사용되지 않으면 IMMEDIATE로 동작한다.

<a id="41f3a32a76b6d9f6"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="6fa448520ca4fcc2"></a>
### 설명

DISCONNECT SESSION은 POST_TRANSACTION과 IMMEDIATE 옵션을 지정할 수 있으며, POST_TRANSACTION은 현재 실행되는 트랜잭션이 있을 경우 트랜잭션이 끝난 후에 세션을 종료한다. IMMEDIATE는 현재 수행 중인 트랜잭션을 바로 정리한 후에 세션을 종료한다.

KILL SESSION은 해당 세션의 프로세스는 존재하지 않지만, 시스템에 남아있는 비정상 세션을 종료한다.

<a id="48ec70c8bf87bc5b"></a>
### 사용 예

```
gSQL> SELECT USER_NAME, SESSION_ID, SERIAL_NO, SESSION_STATUS, PROGRAM_NAME FROM V$SESSION WHERE USER_NAME = 'TEST';

USER_NAME SESSION_ID SERIAL_NO SESSION_STATUS PROGRAM_NAME
--------- ---------- --------- -------------- ------------
TEST              62        49 CONNECTED      gsql        
TEST              65       109 CONNECTED      gsqlnet     
TEST              66       130 CONNECTED      gsql        

3 rows selected.

gSQL> ALTER SYSTEM DISCONNECT SESSION 65, 109;

System altered.
```

<a id="961861249a4e5d3d"></a>
### 호환성

SQL 표준에서는 정의하지 않고 있다.

<a id="cbf215370461aa13"></a>
## ALTER SYSTEM {MOUNT | OPEN} DATABASE

<a id="d466ae64c48bcfe3"></a>
### 기능

데이터베이스를 시스템에 마운트하거나 서비스 가능한 상태로 변경한다.

<a id="e9c2fce2d3cce58b"></a>
### 구문

```
<alter system database statement> ::=
    ALTER SYSTEM <alter system database clause>
    ;

<alter system database clause> ::= 
      MOUNT DATABASE
    | OPEN [ <database_scope> ] DATABASE [ <open_database_option> ]

<open_database_option> ::=
      NORESETLOGS
    | RESETLOGS

<database_scope> ::=
	  LOCAL
    | GLOBAL
```

<a id="0c67046c0364d56c"></a>
### 사용 범위 및 접근 권한

&lt;alter system database statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="639348809dbbbb14"></a>
### 구문 규칙 및 파라미터

<a id="6b2c804d09ecc899"></a>
#### &lt;alter system database clause&gt;

- MOUNT DATATABASE
    - 데이터베이스를 시스템에 마운트한다. 
- OPEN DATABASE
    - 데이터베이스를 서비스 가능한 상태로 변경한다.

<a id="9d5dda8e5e9a2597"></a>
#### &lt;open database option&gt;

- RESETLOGS/ NORESETLOGS
    - 데이터베이스를 복구한 이후에 온라인 redo log를 유지할지 선택한다.
    - NORESETLOGS는 기존 redo log를 유지하는 반면에 RESETLOGS는 이를 초기화한다.
    - 데이터베이스를 불완전 복구한 경우, 반드시 RESETLOGS를 지정해야 한다.
    - 생략된 경우에는 NORESETLOGS가 기본으로 지정된다.

<a id="c5c010a72e03ea58"></a>
#### &lt;database_scope&gt;

- LOCAL
    - LOCAL 영역 서버를 OPEN 단계로 구동한다.
- GLOBAL
    - GLOBAL 영역, 즉 전체 서버를 OPEN 단계로 구동한다.
- Cluster 환경에서 생략된 경우 GLOBAL로 구동 된다.

<a id="d0f744041dbd1145"></a>
### 사용 예

다음은 온라인 redo log를 초기화하는 예이다.

```
ALTER SYSTEM OPEN DATABASE RESETLOGS;
```

<a id="731037e96df307f5"></a>
### 호환성

SQL 표준에서는 데이터베이스의 MOUNT 또는 OPEN에 대한 개념을 정의하지 않고 있다.

<a id="021a09f08b1d65c1"></a>
### 참조

관련 내용은 [ALTER DATABASE RECOVER](#233fbcf85decd22e)를 참조한다.

<a id="e7de24004dd647b5"></a>
## ALTER SYSTEM RECONNECT GLOBAL CONNECTION

<a id="d169dfca8338b851"></a>
### 기능

GLOBAL CONNECTION 형태로 접속한 세션에 재접속할지 여부를 설정한다.

<a id="c9fb2f27ac78cc26"></a>
### 구문

```
<alter system reconnect global connection statement> ::=
    ALTER SYSTEM RECONNECT GLOBAL CONNECTION
    ;
```

<a id="ceb2b61a53043d0e"></a>
### 사용 범위 및 접근 권한

&lt;alter system reconnect global connection statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="fa03e49c6599b16d"></a>
### 설명

GLOBAL CONNECTION 클라이언트의 재접속 여부는 최초 접속할 때 서버로부터 얻은 system 객체의 SCN과 현재 서버의 system 객체의 SCN을 비교하여 결정한다. 해당 구문은 system 객체의 SCN을 상승시켜 클라이언트의 재접속을 유도한다.

해당 구문을 수행한 즉시 클라이언트가 재접속하는 것은 아니다. 클라이언트가 서버에 명령어를 실행할 때 SCN 비교를 통해서 재접속하며 만약 클라이언트에서 모든 멤버로의 연결이 유효하다면 재접속을 시도하지 않는다.

<a id="251864a84f812a8c"></a>
### 사용 예

다음은 해당 구문을 수행하는 예이다.

```
gSQL> ALTER SYSTEM RECONNECT GLOBAL CONNECTION;

System altered.
```

<a id="1141899b67b2cd8b"></a>
### 호환성

SQL 표준에서는 GLOBAL CONNECTION의 개념을 정의하지 않고 있다.

<a id="922972ea95cf99e3"></a>
## ALTER SYSTEM RESET property_name

<a id="f492e0f65ca41119"></a>
### 기능

프로퍼티 파일에서 프로퍼티 값을 삭제한다.

<a id="4f711655193d9879"></a>
### 구문

```
<alter system reset statement> ::=
    ALTER SYSTEM { RESET | UNSET } <property name>
        [ SCOPE = { FILE | SPFILE } ]
        [ AT <domain name>]
    ;
```

<a id="902a86b02bab283c"></a>
### 사용 범위 및 접근 권한

&lt;alter system reset statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="f57f44d43ce5768e"></a>
### 구문 규칙 및 파라미터

<a id="ccc7208464cb20cd"></a>
#### { RESET | UNSET }

RESET과 UNSET은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다.

<a id="3e7d17af6c44b2ba"></a>
#### &lt;property name&gt;

삭제할 프로퍼티의 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#e95fbf953ce3e17d) 장을 참조한다.

<a id="1891d7bd4b45dacc"></a>
#### [ SCOPE = { FILE | SPFILE } ]

프로퍼티 파일에서 삭제하는 것이므로 SCOPE=FILE/SPFILE만 사용할 수 있다.

- SCOPE = FILE 
    - FILE과 SPFILE은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다. 
    - 프로퍼티를 FILE에서 삭제하고, 현재 상태에는 적용하지 않는다. 
    - Database를 재구동할 때 변경 사항을 적용한다.

SCOPE 절을 명시하지 않을 경우, 기본값은 SCOPE = FILE 이다.

<a id="dbeea3c922412089"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="589940a16f241dee"></a>
### 설명

SCOPE=FILE/SPFILE을 사용하여 프로퍼티를 변경했을 경우, 갱신된 값이 프로퍼티 파일에 저장되고 데이터베이스를 재시작할 때 반영된다.

RESET 할 경우, 프로퍼티 파일에 저장된 해당 프로퍼티 갱신값을 파일에서 제거하고 데이터베이스를 재시작할 때 default 값을 사용하도록 한다.

<a id="f98aa0a77a95f5fa"></a>
### 사용 예

다음은 SCOPE=FILE을 사용하여 프로퍼티를 변경하는 예이다.

```
gSQL> ALTER SYSTEM SET PROCESS_MAX_COUNT=128 SCOPE=FILE;

System altered.
```

다음은 위에서 변경한 프로퍼티를 삭제하는 예이다.

```
gSQL> ALTER SYSTEM RESET PROCESS_MAX_COUNT SCOPE=FILE;

System altered.

gSQL> ALTER SYSTEM RESET PROCESS_MAX_COUNT SCOPE=SPFILE;

System altered.

gSQL> ALTER SYSTEM RESET PROCESS_MAX_COUNT;

System altered.

gSQL> ALTER SYSTEM UNSET PROCESS_MAX_COUNT;

System altered.
```

<a id="281ae8b6c5c93c6b"></a>
### 호환성

SQL 표준에서는 시스템 프로퍼티 개념을 정의하지 않고 있다.

<a id="572d96062e6dda5f"></a>
### 참조

관련 내용은 [ALTER SYSTEM SET property_name](#d0c54353bc77cbe4)을 참조한다.

<a id="d0c54353bc77cbe4"></a>
## ALTER SYSTEM SET property_name

<a id="118ecae11d23f724"></a>
### 기능

시스템의 프로퍼티 값을 설정한다.

<a id="a08f3186a206ece6"></a>
### 구문

```
<alter system set statement> ::=
    ALTER SYSTEM SET <property name> { = <property value> | TO DEFAULT }
        [ DEFERRED ]
        [ SCOPE = [ MEMORY | { FILE | SPFILE } | BOTH ] ]
    [AT <domain name>]
    ;
```

<a id="0bb9f87d9ca8aeae"></a>
### 사용 범위 및 접근 권한

&lt;alter system set statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="3539ef05971e09df"></a>
### 구문 규칙 및 파라미터

<a id="460fc2ad01858f0a"></a>
#### &lt;property name&gt;

설정할 프로퍼티의 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#e95fbf953ce3e17d) 장을 참조한다.

<a id="110f1f5abbcc91ce"></a>
#### &lt;property value&gt;

설정할 프로퍼티의 값이다.

<a id="c7eb2f38831618ea"></a>
#### TO DEFAULT

시스템 프로퍼티 값을 시스템을 구동할 당시의 최초값으로 설정한다.

<a id="5eaabf9e96096a9b"></a>
#### [ DEFERRED ]

변경된 프로퍼티를 적용할 시점을 정의한다.

- DEFERRED 
    - 현재 SESSION에는 영향을 주지 않고, 새로 생성되는 SESSION에 적용된다. 
    - 프로퍼티의 SYS_MODIFIABLE 속성값이 IMMEDIATE/ DEFERRED 일 때 적용 가능하며, 반드시 명시해야 한다. 
    - 프로퍼티의 SYS_MODIFIABLE 속성값이 FALSE인 경우 사용할 수 없다.

프로퍼티의 SYS_MODIFIABLE 속성값이 IMMEDIATE일 경우, DEFERRED를 명시하지 않으면 모든 SESSION에 바로 적용된다.

<a id="dd832580779cc96e"></a>
#### [ SCOPE = [ MEMORY | { FILE | SPFILE } | BOTH ] ]

시스템 프로퍼티 변경에 영향을 받는 범위를 정의한다.

- SCOPE = MEMORY 
    - 변경 사항이 현재 상태에만 적용되며, database를 다시 구동할 경우 해당 값은 없어진다. 
- SCOPE = FILE 
    - FILE과 SPFILE은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다. 
    - 변경 사항을 FILE에 저장하고 현재 상태에는 적용하지 않는다. 
    - Database를 다시 구동할 때 변경 사항을 적용한다. 
- SCOPE = BOTH 
    - 변경 사항을 FILE에 저장하고 현재 상태에도 적용한다.

SCOPE 절을 명시하지 않을 경우, 기본값은 SCOPE = MEMORY 이다.   
프로퍼티의 SYS_MODIFIABLE 속성값이 FALSE인 경우에는 반드시 SCOPE=FILE/SPFILE이라고 명시해야 한다.

<a id="2fbc22f3d7420fac"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="eed3bb2f9d6c0af4"></a>
### 설명

자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#e95fbf953ce3e17d) 장을 참조한다.

<a id="68b27e51693981d6"></a>
### 사용 예

다음은 SYS_MODIFIABLE 속성이 DEFERRED인 프로퍼티를 변경하는 예이다.

```
gSQL> ALTER SYSTEM SET HINT_ERROR = ON;

ERR-22000(13019): Invalid property modify mode.(HINT_ERROR)

gSQL> ALTER SYSTEM SET HINT_ERROR = ON DEFERRED;

System altered.
```

다음은 SYS_MODIFIABLE 속성이 FALSE인 프로퍼티를 변경하는 예이다.

```
gSQL> ALTER SYSTEM SET PROCESS_MAX_COUNT=128;

ERR-22000(13018): Specified property cannot be modified with this SCOPE option.(PROCESS_MAX_COUNT)

gSQL> ALTER SYSTEM SET PROCESS_MAX_COUNT=128 SCOPE=FILE;

System altered.
```

다음은 변경된 속성을 session 접속 당시의 default 값으로 변경하는 예이다.

```
gSQL> ALTER SYSTEM SET TRANSACTION_COMMIT_WRITE_MODE=0;

System altered.

gSQL> ALTER SYSTEM SET TRANSACTION_COMMIT_WRITE_MODE TO DEFAULT;

System altered.

gSQL> ALTER SYSTEM SET TRANSACTION_COMMIT_WRITE_MODE TO DEFAULT DEFERRED;

System altered.
```

<a id="90bbe2dd3cac2eba"></a>
### 호환성

SQL 표준에서는 시스템의 프로퍼티 개념을 정의하지 않고 있다.

<a id="93822e892b45bffd"></a>
### 참조

관련 내용은 [ALTER SYSTEM RESET property_name](#922972ea95cf99e3)을 참조한다.

<a id="3e74ff8636ece361"></a>
## ALTER SYSTEM SWITCH LOGFILE

<a id="45e8ebe78d2748f4"></a>
### 기능

데이터베이스 내에 있는 CURRENT 상태의 로그파일을 ACTIVE 상태로 변경한다.

<a id="8196d3b936681e29"></a>
### 구문

```
<alter system switch logfile statement> ::=
    ALTER SYSTEM SWITCH LOGFILE
    [ AT <domain name> ]
    ;
```

<a id="2cefba6f684ac7ad"></a>
### 사용 범위 및 접근 권한

&lt;alter system switch logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="85efbd8f32f36e3b"></a>
### 구문 규칙 및 파라미터

<a id="62ff4ff146b448bb"></a>
#### &lt;alter system switch logfile statement&gt;

데이터베이스가 MOUNT 또는 OPEN 상태여야 한다.

<a id="cc16e60d1e55e3c8"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="105be19fe4706a45"></a>
### 설명

기본적으로 CURRENT 상태의 로그파일이 다 채워지면 자동으로 로그 스위치가 발생한다. 해당 구문은 특수한 상황에서 강제로 로그 스위치를 하고자 할 때 사용된다.

<a id="fbffcaac6bd69532"></a>
### 사용 예

```
ALTER SYSTEM SWITCH LOGFILE;
```

<a id="a61c640982d8f507"></a>
### 호환성

SQL 표준에서는 LOGFILE에 대한 개념을 정의하지 않고 있다.

<a id="42d37241eb9b2f5c"></a>
### 참조

관련 내용은 [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#cbf215370461aa13)를 참조한다.

<a id="1085f15b7d6e9700"></a>
## ALTER TABLE

<a id="d5b3bc82307792f1"></a>
### 기능

테이블 정의를 변경한다.

<a id="99e93888c74b076a"></a>
### 구문

```
<alter table statement> ::=
      <alter table physical attribute statement>
    | <rename table statement>
    | <add column definition>
    | <drop column definition>
    | <alter column definition>
    | <rename column statement>
    | <add table constraint definition>
    | <drop table constraint definition>
    | <alter table constraint definition>
    | <alter table drop offline segments statement>
    | <rename table constraint statement>
    | <add table supplemental log statement>
    | <drop table supplemental log statement>
    | <rebalance statement>
    | <alter table reorganize statement>
    | <move shard statement>
    | <merge shards statement>
    | <split shard statement>
    | <alter table synchronize statement>
    | <rename shard statement>
    | <read { only | write } statement>
    ;
```

<a id="b86c427801e8c65e"></a>
### 사용 범위 및 접근 권한

&lt;alter table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="91d1cd5a414bd97b"></a>
### 구문 규칙 및 파라미터

<a id="9536cdeeb5c78a3f"></a>
#### &lt;alter table physical attribute statement&gt;

테이블의 물리적 속성을 변경한다.  
자세한 내용은 [ALTER TABLE name STORAGE](#e0bd18124d55324a) 구문을 참조한다.

<a id="c7de0a3ae9105867"></a>
#### &lt;rename table statement&gt;

테이블 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME TO](#81ef596f170298aa) 구문을 참조한다.

<a id="f7e314486fa8e21f"></a>
#### &lt;add column definition&gt;

테이블에 column을 추가한다.  
자세한 내용은 [ALTER TABLE name ADD COLUMN](#5bf457087cd2404f) 구문을 참조한다.

<a id="526cc4fc50c592dc"></a>
#### &lt;drop column definition&gt;

테이블에서 column을 삭제한다.  
자세한 내용은 [ALTER TABLE name SET UNUSED COLUMN](#2389dc92f034f678) 구문을 참조한다.

<a id="846d59f6d75b0aa9"></a>
#### &lt;alter column definition&gt;

테이블 column의 정의를 변경한다.  
자세한 내용은 [ALTER TABLE name ALTER COLUMN](#0892c59a03976f71) 구문을 참조한다.

<a id="a77d978ca2a09d58"></a>
#### &lt;rename column statement&gt;

테이블 column의 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME COLUMN](#61e1f15efa661ac2) 구문을 참조한다.

<a id="61671dc20b16cea9"></a>
#### &lt;add table constraint definition&gt;

테이블에 제약 조건을 추가한다.  
자세한 내용은 [ALTER TABLE name ADD CONSTRAINT](#b1bf02c95ebfb66d) 구문을 참조한다.

<a id="e3affdd4bcee3a1e"></a>
#### &lt;drop table constraint definition&gt;

테이블의 제약 조건을 삭제한다.  
자세한 내용은 [ALTER TABLE name DROP CONSTRAINT](#098f7063d2ae708c) 구문을 참조한다.

<a id="0d6201d6e8358a89"></a>
#### &lt;alter table constraint definition&gt;

테이블의 제약 조건을 변경한다.  
자세한 내용은 [ALTER TABLE name ALTER CONSTRAINT](#75005eef58445700) 구문을 참조한다.

<a id="9a805ca67b061aa5"></a>
#### &lt;alter table drop offline segments statement&gt;

테이블의 오프라인 된 shard들을 삭제한다.  
자세한 내용은 [ALTER TABLE name DROP OFFLINE SEGMENTS](#122c923f4ef34146) 구문을 참조한다.

<a id="6257a2aaf6846633"></a>
#### &lt;rename table constraint statement&gt;

테이블 제약 조건의 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME CONSTRAINT](#662d1bdaf11f8e22) 구문을 참조한다.

<a id="370ebd3609f2d489"></a>
#### &lt;add table supplemental log statement&gt;

테이블의 데이터가 변경되면 redo log에 부가 정보를 추가하도록 설정한다.  
자세한 내용은 [ALTER TABLE name ADD SUPPLEMENTAL LOG](#26bd68efcb7d74f4) 구문을 참조한다.

<a id="2d2aaa465a24f460"></a>
#### &lt;drop table supplemental log statement&gt;

테이블의 데이터가 변경되면 redo log에 부가 정보를 추가하지 않도록 설정한다.  
자세한 내용은 [ALTER TABLE name DROP SUPPLEMENTAL LOG](#b80519a1cdd40ae4) 구문을 참조한다.

<a id="630bf0ea327b80ba"></a>
#### &lt;rebalance statement&gt;

Cluster 환경에서 테이블의 shard를 재배치하거나 정합성이 깨진 shard를 동기화하여 정합성을 복구한다.  
자세한 내용은 [ALTER TABLE REBALANCE](#4dcbc8cc43487ef2) 구문을 참조한다.

<a id="b8dd04947a244392"></a>
#### &lt;alter table reorganize statement&gt;

테이블을 물리적으로 재구성한다.  
자세한 내용은 [ALTER TABLE name REORGANIZE](#b33b38d54cfadfd0) 구문을 참조한다.

<a id="d888213229a4e08c"></a>
#### &lt;alter table synchronize statement&gt;

Cluster 환경에 이미 배치되어 있는 오프라인 된 shard들을 동기화하여 정합성을 복구한다.  
자세한 내용은 [ALTER TABLE name SYNCHRONIZE](#baf7d0e8598b3f6a) 구문을 참조한다.

<a id="605cb8d29df45bd1"></a>
#### &lt;move shard statement&gt;

Cluster 환경에서 테이블의 특정 shard를 특정 cluster group으로 재배치한다.  
자세한 내용은 [ALTER TABLE MOVE SHARD](#b64b6ca52ad7b811) 구문을 참조한다.

<a id="e5e673f1e7e126c5"></a>
#### &lt;merge shards statement&gt;

Cluster 환경에서 테이블의 특정 shard들을 병합하여 재배치한다.  
자세한 내용은 [ALTER TABLE name MERGE SHARDS](#c5810c8b8fddc31e) 구문을 참조한다.

<a id="c6cdd9dfc542460d"></a>
#### &lt;split shard statement&gt;

Cluster 환경에서 테이블의 특정 shard를 분산하여 특정 cluster group에 재배치한다.  
자세한 내용은 [ALTER TABLE SPLIT SHARD](#e5ce6718ce23e4e6) 구문을 참조한다.

<a id="11e78ba7f79373ae"></a>
#### &lt;rename shard statement&gt;

Cluster 환경에서 테이블의 특정 shard 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME SHARD](#0976d6b11dbb86a3) 구문을 참조한다.

<a id="a096d3e2009ffed7"></a>
#### &lt;read { only | write } statement&gt;

테이블에 READ ( only | write }을 설정한다.  
자세한 내용은 [ALTER TABLE name READ { ONLY | WRITE }](#9f7366fab122ef37) 구문을 참조한다.

<a id="68cb6fc1d50a9983"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="f0faa310b6ff8057"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="99481221f357292f"></a>
### 호환성

SQL 표준에서는 다음과 같은 구문을 정의하지 않고 있다.

- &lt;alter table physical attribute statement&gt; 
- &lt;rename table statement&gt; 
- &lt;rename column statement&gt; 
- &lt;rename table constraint statement&gt;
- &lt;add table supplemental log statement&gt; 
- &lt;drop table supplemental log statement&gt;
- &lt;rebalance statement&gt;
- &lt;move shard statement&gt;
- &lt;split shard statement&gt;
- &lt;rename shard statement&gt;
- &lt;read { only | write } statement&gt;

<a id="5bf457087cd2404f"></a>
## ALTER TABLE name ADD COLUMN

<a id="5c1e4f7293284a0e"></a>
### 기능

테이블에 column을 추가한다.

<a id="dc07e2e1e7f2e589"></a>
### 구문

```
<add column definition> ::=
      ALTER TABLE table_name ADD [ COLUMN ] <column definition>
    | ALTER TABLE table_name ADD [ COLUMN ] ( <column definition> [, ...] )
    ;
```

<a id="14b16200dbfd1a9b"></a>
### 사용 범위 및 접근 권한

&lt;add column definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블을 변경하려면 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - ALTER ANY TABLE ON DATABASE

- Column을 추가할 때 제약 조건을 함께 명시했다면, 다음과 같이 제약 조건을 생성할 수 있는 조건을 만족해야 한다.
    - 제약 조건이 생성될 스키마에 대해 다음 권한 중 하나가 있어야 한다. 
        - 해당 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
        - ALTER ANY TABLE ON DATABASE 
    - 생성할 제약 조건이 key 제약 조건일 경우, 인덱스가 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다. 
        - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
        - USAGE TABLESPACE ON DATABASE
    - 생성할 제약 조건이 FOREIGN KEY 제약 조건일 경우 다음 권한 중 하나가 있어야 한다.
        - referenced table 에 대해 REFERENCES
        - 각 referenced column 에 대해 REFERENCES
        - referenced table 이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
        - ALTER ANY TABLE ON DATABASE

- 해당 테이블의 소유자는 추가된 column에 대해 다음과 같은 권한을 갖는다.
    - 추가된 모든 column에 대한 권한 
        - SELECT(columns) ON TABLE WITH GRANT OPTION 
        - INSERT(columns) ON TABLE WITH GRANT OPTION 
        - UPDATE(columns) ON TABLE WITH GRANT OPTION 
        - REFERENCES(columns) ON TABLE WITH GRANT OPTION 
    - 함께 생성한 제약 조건에 대한 권한 
        - 제약 조건의 소유자 
        - 제약 조건과 함께 생성된 인덱스의 소유자

<a id="de88c3201229f054"></a>
### 구문 규칙 및 파라미터

<a id="a5360c56dbeff494"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="13ec2d9c32d0c7d8"></a>
#### ADD [ COLUMN ]

COLUMN 예약어는 생략할 수 있다.

<a id="6daa54dfb3c6279c"></a>
#### &lt;column definition&gt;

추가할 column을 정의한다.  
자세한 내용은 [CREATE TABLE](19-sql-references-c-g.md#ce6ecbcf1ea593ea) 구문의 [&lt;column definition&gt;](19-sql-references-c-g.md#cbbbc16b08b9d034) 절을 참조한다.  
테이블 내에 동일한 column 이름이 존재하지 않아야 한다.

Column을 정의할 때 DEFAULT 절을 명시할 경우, 모든 row의 기본값을 추가되는 column에 저장한다.  
Column을 정의할 때 &lt;identity column specification&gt; 절을 명시한 경우, 모든 row 각각의 자동 생성값을 추가되는 column에 저장한다.   
Column을 정의할 때 NOT NULL 제약 조건을 함께 명시한 경우, 테이블을 비우거나 DEFALUT 절 또는 &lt;identity column specification&gt; 절을 함께 기술해야 한다.

<a id="a8bce7d0996cc9b0"></a>
#### ( &lt;column definition&gt; [, ...] )

다수의 column을 추가한다.   
괄호 내부에 다수의 &lt;column definition&gt;을 나열한다.

<a id="d0239a63f080f262"></a>
### 설명

추가되는 column은 기존 column들의 뒤에 위치한다.   
DEFAULT 절이나 &lt;identity column specification&gt;을 명시한 경우, 수행시간은 테이블에 존재하는 row의 개수에 비례하여 증가한다.

<a id="e6a13763ef0b5ae4"></a>
### 사용 예

다음은 하나의 column을 추가하는 예이다.

```
gSQL> ALTER TABLE region ADD COLUMN r_new_comment VARCHAR(152);

Table altered.
```

다음은 다수의 column을 추가하는 예이다.

```
gSQL> ALTER TABLE partsupp ADD COLUMN ( 
   ps_retailprice NUMERIC(12,2), 
   ps_acctbal NUMERIC(12,2), ps_mktsegment  CHAR(10) );

Table altered.
```

다음은 identity column과 DEFAULT 절을 갖는 column을 추가하는 예이다.

```
gSQL> ALTER TABLE region ADD COLUMN ( 
    r_regionkey INTEGER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    r_comment   VARCHAR(152) DEFAULT 'N/A' );

Table altered.

gSQL> SELECT r_regionkey, r_name, r_comment FROM region;

R_REGIONKEY R_NAME                    R_COMMENT
----------- ------------------------- ---------
          1 AFRICA                    N/A      
          2 AMERICA                   N/A      
          3 ASIA                      N/A      
          4 EUROPE                    N/A      
          5 MIDDLE EAST               N/A      

5 rows selected.
```

다음은 지연가능한 제약 조건을 가지는 column을 추가하는 예이다.

```
gSQL> ALTER TABLE t1 ADD COLUMN ( id INTEGER CONSTRAINT t1_uk UNIQUE DEFERRABLE );

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="2292fed273e8d27b"></a>
### 호환성

SQL 표준에서는 다수의 column definition 추가에 대해 정의하지 않고 있다.

<a id="5106c34d6df59d2f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#1085f15b7d6e9700)
- [ALTER TABLE name SET UNUSED COLUMN](#2389dc92f034f678)
- [ALTER TABLE name ALTER COLUMN](#0892c59a03976f71)
- [ALTER TABLE name RENAME COLUMN](#61e1f15efa661ac2)

<a id="b1bf02c95ebfb66d"></a>
## ALTER TABLE name ADD CONSTRAINT

<a id="af0519dd2a408f46"></a>
### 기능

테이블 제약 조건을 추가한다.

<a id="4cc108afa914b166"></a>
### 구문

```
<add table constraint definition> ::=
    ALTER TABLE table_name 
        ADD <table constraint definition>
    ;
```

<a id="d3f84ca621a9d9a7"></a>
### 사용 범위 및 접근 권한

&lt;add table constraint definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 제약 조건을 생성할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - ALTER ANY TABLE ON DATABASE

- 제약 조건이 생성될 스키마에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 생성할 제약 조건이 key 제약 조건일 경우, 인덱스가 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
    - USAGE TABLESPACE ON DATABASE

- 생성할 제약 조건이 FOREIGN KEY 제약 조건일 경우 다음 권한 중 하나가 있어야 한다.
    - referenced table 에 대해 REFERENCES
    - 각 referenced column 에 대해 REFERENCES
    - referenced table 이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 생성한 제약 조건의 소유자는 다음과 같이 결정된다.
    - 제약 조건이 속한 스키마의 소유자
    - 제약 조건이 속한 스키마가 PUBLIC 일 경우, 구문을 수행한 사용자

> Cluster system에서 PRIMARY KEY와 UNIQUE 제약 조건은 모든 sharding key를 포함해야 한다.

<a id="1c35280531273ef8"></a>
### 구문 규칙 및 파라미터

<a id="d9e7fda899162fca"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="c32c50a195e472ff"></a>
#### &lt;table constraint definition&gt;

추가할 제약 조건을 정의한다.  
NOT NULL 제약 조건은 ALTER TABLE .. ADD CONSTRAINT 구문으로 추가할 수 없으며, 다음 예와 같이 [ALTER TABLE name ALTER COLUMN](#0892c59a03976f71) 구문을 이용해 정의할 수 있다.

```
ALTER TABLE t1 ALTER COLUMN c1 SET NOT NULL;
```

자세한 내용은 [CREATE TABLE](19-sql-references-c-g.md#ce6ecbcf1ea593ea) 구문의 [&lt;table constraint definition&gt;](19-sql-references-c-g.md#2643d121c1e0846b) 절을 참조한다.

<a id="484c8e5a46d27f45"></a>
### 설명

Primary key, unique key와 같은 key 제약을 추가할 때 이를 위한 index가 자동으로 생성된다.

<a id="ba98f7aaddf038ab"></a>
### 사용 예

다음은 테이블에 primary key 제약 조건을 추가하는 예이다.

```
gSQL> ALTER TABLE t1 ADD PRIMARY KEY ( id );

Table altered.
```

다음은 테이블에 primary key 제약 조건을 추가할 때 제약 조건 이름을 명시하는 예이다.

```
gSQL> ALTER TABLE t1 ADD CONSTRAINT t1_pk PRIMARY KEY ( id );

Table altered.
```

다음은 지연가능한 제약 조건을 추가하는 예이다.

```
gSQL> ALTER TABLE t1 ADD CONSTRAINT t1_uk UNIQUE ( id ) DEFERRABLE INITIALLY DEFERRED;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="18721efc42bc9fe5"></a>
### 호환성

**SQL 표준 호환성**

<a id="65639aa7a0c59f24"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="dc9f9b87d055abdf"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](19-sql-references-c-g.md#ce6ecbcf1ea593ea)
- [CREATE INDEX](19-sql-references-c-g.md#1b99962ed891aa4f)
- [ALTER TABLE](#1085f15b7d6e9700)
- [ALTER TABLE name DROP CONSTRAINT](#098f7063d2ae708c)

<a id="ef80852f02ba2cc6"></a>
## ALTER TABLE name ADD GLOBAL SECONDARY INDEX

<a id="8dab32d760c2ebc6"></a>
### 기능

테이블에 global secondary index를 생성한다.

<a id="f7ad5dbbf05247ee"></a>
### 구문

```
<alter table add global secondary index definition> ::=
    ALTER TABLE table_name 
        ADD GLOBAL SECONDARY INDEX
        [ <index attributes> [...] ] [ TABLESPACE tablespace_name ]
    ;

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

<size clause> ::=
      integer [ K | M | G | T ]

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="f296ee7b5ed0257e"></a>
### 사용 범위 및 접근 권한

&lt;alter table add global secondary index definition&gt; 구문은 cluster system에서 정의할 수 있으며 사용자는 다음 조건들을 만족해야 한다.

- 인덱스를 생성할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 인덱스가 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE
    - USAGE TABLESPACE ON DATABASE

<a id="b6a472d867b59f3d"></a>
### 구문 규칙 및 파라미터

<a id="35a38c0ee29699e7"></a>
#### table_name

인덱스를 생성할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="ed87fce6ec297a23"></a>
#### &lt;physical attribute clause&gt;

인덱스의 물리적 속성 정보를 정의한다.

- PCTFREE integer
    - 정의
        - 페이지 내 key 삽입으로 인한 페이지 분할 빈도를 조절하기 위해 예약된 공간이다.
        - 인덱스 bottom-up 빌드 시에만 적용된다.
    - 0에서 99까지의 값을 사용할 수 있다.
    - 생략할 경우, 기본값은 DEFAULT_INDEX_PCTFREE property에 설정된 값을 사용한다.

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

<a id="0d76f79c5ab2e86b"></a>
#### &lt;segment attr clause&gt;

인덱스가 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer
    - 정의
        - 인덱스를 생성할 때 초기에 할당할 물리적 공간의 크기를 기술한다.
        - integer 값이 EXTENT 두 개 이하인 경우, extent 두 개 크기로 설정된다.
        - integer 값이 EXTENT 두 개 보다 큰 경우, TABLESPACE의 EXTENT 크기에 맞춰 (aligned) 설정된다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기본값은 인덱스가 속한 TABLESPACE의 EXTENT 두 개 크기이다.

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

<a id="11a1a4127344a39e"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="ae0b719204a38e24"></a>
#### NOPARALLEL | PARALLEL [ integer ]

인덱스 구축과정에 사용될 thread의 개수를 지정한다.

- NOPARALLEL 
    - 병렬로 인덱스를 구축하지 않는다. 
- PARALLEL [integer] 
    - 병렬로 인덱스를 구축한다. 
    - integer가 생략되거나 0으로 지정된 경우에는 프로퍼티 (INDEX_BUILD_PARALLEL_FACTOR)를 따른다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - 만약 integer나 프로퍼티의 값이 0인 경우에는 최적값을 시스템이 결정한다.
- 명시하지 않을 경우, 기본값은 NOPARALLEL이다.

<a id="b0aacad7dd361bfe"></a>
#### TABLESPACE tablespace_name

인덱스가 저장될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - LOGGING 인덱스로 변경하려면, tablespace_name은 data tablespace여야 하며 
    - NOLOGGING 인덱스로 변경하려면 tablespace_name은 temporary tablespace 또는 nologging tablespace여야 한다.

- TABLESPACE 절을 생략할 경우, 기존 인덱스의 설정을 그대로 따른다.

<a id="400312fda1d6e6fb"></a>
### 설명

Non-deterministic 질의에는 global secondary index가 반드시 필요하다. LOGGING 인덱스와 NOLOGGING 인덱스에는 다음과 같은 trade-off가 있다

- LOGGING 인덱스
    - 장점: 시스템을 구동할 때 로그를 이용해 인덱스가 자동으로 복구되므로 별도의 구축과정이 없다.
    - 단점: 관련 row를 변경할 때 인덱스 변경 내용을 로그로 기록하여 디스크 IO를 유발한다.
- NOLOGGING 인덱스
    - 장점: 관련 row를 변경할 때 인덱스 변경 내용에 대해 디스크 IO가 발생하지 않는다.
    - 단점: 시스템을 구동할 때 인덱스에 대한 로그 정보가 없어 자동으로 인덱스를 재구축한다.

<a id="8c9480518043f255"></a>
### 사용 예

다음은 테이블 T1에 global secondary index를 추가하는 예이다.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX;

Table altered.

gSQL> COMMIT;

Commit complete.
```

다음은 테이블 T1의 tablespace USER_DATA_TBS에 global secondary index를 logging index로 생성하는 예이다.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX TABLESPACE USER_DATA_TBS;

Table altered.

gSQL> COMMIT;

Commit complete.
```

다음은 테이블 T1의 tablespace USER_TEMP_TBS에 global secondary index를 nologging index로 생성하는 예이다.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX TABLESPACE USER_TEMP_TBS;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="fbb7fcaf232efbec"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="6a5d987e3bf794d8"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#2bbf4303b4825280)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#71b8f952e7d629e8)
- [CREATE TABLE](19-sql-references-c-g.md#ce6ecbcf1ea593ea)

<a id="26bd68efcb7d74f4"></a>
## ALTER TABLE name ADD SUPPLEMENTAL LOG

<a id="7a9230f9a7b76aea"></a>
### 기능

테이블의 데이터가 변경될 때 테이블에 primary key가 있으면 redo log에 primary key 값을 추가하도록 설정한다.

<a id="9585a93e5d49baf2"></a>
### 구문

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="d0ca106be742931a"></a>
### 사용 범위 및 접근 권한

&lt;add table supplemental log statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="2032ba4c4335a47e"></a>
### 구문 규칙 및 파라미터

<a id="cd8391e744337e39"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

테이블에 primary key가 존재하지 않더라도 구문을 수행할 수 있다.

<a id="5de260567115758f"></a>
### 설명

해당 TABLE에 UPDATE/ DELETE를 수행할 때 SUPPLEMENTAL LOG를 추가로 기록하도록 한다. 기록된 SUPPLEMENTAL LOG는 CDC와 같은 툴 또는 로그를 분석할 때 사용된다.

모든 TABLE의 SUPPLEMENTAL LOG를 기록하려면 *SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY = YES*로 설정한다.

<a id="bc18bfa813782bb5"></a>
### 사용 예

다음은 테이블의 data를 변경할 때 redo log에 primary key 값을 추가하도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="1e74b82da14f7acd"></a>
### 호환성

SQL 표준에서는 &lt;add table supplemental log statement&gt;를 다루지 않고 있다.

<a id="1dae8ba47e98c550"></a>
### 참조

관련 내용은 [ALTER TABLE name DROP SUPPLEMENTAL LOG](#b80519a1cdd40ae4)를 참조한다.

<a id="0892c59a03976f71"></a>
## ALTER TABLE name ALTER COLUMN

<a id="67e59ef57041fc1a"></a>
### 기능

Column의 정의를 변경한다.

<a id="861f05ad42beb48a"></a>
### 구문

```
<alter column definition> ::=
    ALTER TABLE table_name 
        ALTER [ COLUMN ] column_name <alter column action>

<alter column action> ::=

      <set column default clause>
    | <drop column default clause>
    | <set column not null clause>
    | <drop column not null clause>
    | <alter column data type clause>
    | <alter identity column specification>
    | <drop identity property clause>    
    ;

<set column default clause> ::=
    SET DEFAULT <default option>

<drop column default clause> ::=
    DROP DEFAULT

<set column not null clause> ::=
    SET [ CONSTRAINT constraint_name ] NOT NULL [ <constraint characteristics> ]


<constraint characteristics> ::=
      [ NOT ] DEFERRABLE [ <constraint check time> ] [ <constraint enforcement> ]
    | <constraint check time> [ [ NOT ] DEFERRABLE ] [ <constraint enforcement> ]
    | [ <constraint enforcement> ]

<constraint check time> ::=
      INITIALLY DEFERRED 
    | INITIALLY IMMEDIATE

<constraint enforcement> ::=
    [NOT] ENFORCED

<drop column not null clause> ::=
    DROP NOT NULL

<alter column data type clause> ::=
    SET DATA TYPE <data type> 

<alter identity column specification> ::=
     <set identity column generation clause> [ <alter identity column option> ... ]
   | <alter identity column option> ...

<set identity column generation clause> ::=
   SET GENERATED { ALWAYS | BY DEFAULT }

<alter identity column option> ::=
     <alter sequence generator restart option>
   | [ SET ] <basic sequence generator option>

<alter sequence generator restart option> ::=
    RESTART [ WITH integer ]

<basic sequence generator option> ::=
      <sequence generator increment by option>
    | <sequence generator maxvalue option>
    | <sequence generator minvalue option>
    | <sequence generator cycle option>
    | <sequence generator cache option>

<drop identity property clause> ::=
    DROP IDENTITY
```

<a id="5dfa095e2dcf2ec8"></a>
### 사용 범위 및 접근 권한

&lt;alter column definition&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="6f7817208d225fdb"></a>
### 구문 규칙 및 파라미터

<a id="23b3e1ba3c80fbfb"></a>
#### table_name

변경할 테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="65f7aa9e1a99e7cf"></a>
#### ALTER [ COLUMN ]

COLUMN 예약어는 생략할 수 있다.

<a id="b267f5cc86d932d8"></a>
#### column_name

변경할 column의 이름이다.

<a id="f75e90ece6ddab55"></a>
#### &lt;set column default clause&gt;

Column의 기본값을 설정한다.   
identity column이 아니어야 한다.

이후에 수행되는 INSERT 구문 등에서 DEFAULT 절을 사용할 경우 설정한 기본값이 사용된다.

DEFAULT expression의 데이터 타입은 column의 데이터 타입과 호환 가능해야 한다.   
타입이 호환되지 않거나 expression이 valid 하지 않으면 에러가 발생한다.

자세한 설명은 [CREATE TABLE](19-sql-references-c-g.md#ce6ecbcf1ea593ea) 구문의 [&lt;default clause&gt;](19-sql-references-c-g.md#092150e3dd719845) 절을 참조한다.

<a id="44c9e1f2bb264d07"></a>
#### &lt;drop column default clause&gt;

Column의 기본값을 제거한다.  
identity column이 아니어야 한다.  
기본값을 제거하면 INSERT 구문 등에서 DEFAULT 절을 사용할 때 NULL 값으로 설정된다.

<a id="a1e58850b35f2bad"></a>
#### &lt;set column not null clause&gt;

- SET [CONSTRAINT constraint_name] NOT NULL [ &lt;constraint characteristics&gt; ]
    - Column에 NOT NULL 제약 조건을 설정한다.
    - Column의 값으로 NULL 값을 허용하지 않는다.
    - 해당 column에 NULL 값이 존재하지 않아야 한다.

- [CONSTRAINT constraint_name]을 생략할 경우 자동으로 제약 조건 이름을 지정한다.
- &lt;constraint characteristics&gt;를 생략할 경우, NOT DEFERRABLE INITIALLY IMMEDIATE 속성을 갖는다.
- Identity column은 DEFERRABLE 속성을 가질 수 없다.

지연가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](20-sql-references-h-z.md#b6ece05278d045fb) 구문의 설명을 참조한다.

<a id="a870c65aa3078ece"></a>
#### &lt;drop column not null clause&gt;

- DROP NOT NULL
    - Column의 NOT NULL 제약 조건을 제거한다.

<a id="c3cbf4f521dbd868"></a>
#### &lt;alter column data type clause&gt;

- SET DATA TYPE &lt;data type&gt;
    - Column의 데이터 타입을 변경한다.

> SET DATA TYPE 구문은 자동으로 commit 되는 DDL 구문이다.

동일한 계열간에 타입을 변경할 수 있는데 이 때 다음 조건을 만족해야 한다.

**character string type 변환**

<a id="df8bae55a66ef713"></a>
| from \ to | CHAR(n) | VARHCAR(n) | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR(m) | X | X | X |
| VARCHAR(m) | X | n >= m | X |
| LONG VARCHAR | X | X | O |

char length unit을 변경할 경우 다음과 같은 조건을 만족해야 한다.

**character length unit 변환**

<a id="1c5da177df810f33"></a>
| from \ to | OCTETS | CHARACTERS |
| --- | --- | --- |
| OCTETS | O | O |
| CHARACTERS | X | O |

**binary string type 변환**

<a id="03d896219bcbcaec"></a>
| from \ to | BINARY(n) | VARBINARY(n) | LONG VARBINARY |
| --- | --- | --- | --- |
| BINARY(m) | X | X | X |
| VARBINARY(m) | X | n >= m | X |
| LONG VARBINARY | X | X | O |

**numeric type**

<a id="bcd6e84a088f5f3d"></a>
| from \ to | SMALLINT | INTEGER | BIGINT | NUMERIC | NUMERIC(q) | NUMERIC(q,t) | NUMBER(q) | NUMBER(q,t) | REAL | DOUBLE PRECISION | FLOAT | FLOAT(q) | NUMBER |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SMALLINT | O | O | O | O | q >= 5 | q >= 5  t >= 0  (q-t) >= 5 | q >= 5 | q >= 5  t >= 0  (q-t) >= 5 | O | O | O | ddc(q) >= 5 | O |
| INTEGER | X | O | O | O | q >= 10 | q >= 10  t >= 0  (q-t) >= 10 | q >= 10 | q >= 10  t >= 0  (q-t) >= 10 | X | O | O | ddc(q) >= 10 | O |
| BIGINT | X | X | O | O | q >= 19 | q >= 19  t >= 0  (q-t) >= 19 | q >= 19 | q >= 19  t >= 0  (q-t) >= 19 | X | X | O | ddc(q) >= 19 | O |
| NUMERIC | X | X | X | O | q == 38 | q == 38  t == 0 | q == 38 | q == 38  t == 0 | X | X | O | ddc(q) == 38 | O |
| NUMERIC(p) | 5 >= p | 10 >= p | 19 >= p | O | q >= p | q >= p  t >= 0  (q-t) >= p | q >= p | q >= p  t >= 0  (q-t) >= p | 8 >= p | 16 >= p | O | ddc(q) >= p | O |
| NUMERIC(p,s) | 5 >= p  0 >= s  5 >= (p-s) | 10 >= p  0 >= s  10 >= (p-s) | 19 >= p  0 >= s 19 >= (p-s) | 38 >= p  0 >= s  38 >= (p-s) | q >= p  0 >= s  q >= (p-s) | q >= p  t >= s  (q-t) >= (p-s) | q >= p  0 >= s  q >= (p-s) | q >= p  t >= s  (q-t) >= (p-s) | 8 >= p | 16 >= p | O | ddc(q) >= p | O |
| NUMBER(p) | 5 >= p | 10 >= p | 19 >= p | O | q >= p | q >= p  t >= 0  (q-t) >= p | q >= p | q >= p  t >= 0 (q-t) >= p | 8 >= p | 16 >= p | O | ddc(q) >= p | O |
| NUMBER(p,s) | 5 >= p  0 >= s  5 >= (p-s) | 10 >= p 0 >= s 10 >= (p-s) | 19 >= p  0 >= s  19 >= (p-s) | 38 >= p  0 >= s 3 8 >= (p-s) | q >= p  0 >= s  q >= (p-s) | q >= p  t >= s  (q-t) >= (p-s) | q >= p  0 >= s  q >= (p-s) | q >= p  t >= s (q-t) >= (p-s) | 8 >= p | 16 >= p | O | ddc(q) >= p | O |
| REAL | X | X | X | X | X | X | X | X | O | O | O | ddc(q) >= 8 | O |
| DOUBLE PRECISION | X | X | X | X | X | X | X | X | X | O | O | ddc(q) >= 16 | O |
| FLOAT | X | X | X | X | X | X | X | X | X | X | O | ddc(q) == 38 | O |
| FLOAT(p) | X | X | X | X | X | X | X | X | 8 >= ddc(p) | 16 >= ddc(p) | O | ddc(q) >= ddc(p) | O |
| NUMBER | X | X | X | X | X | X | X | X | X | - | O | ddc(q) == 38 | O |

FLOAT(p)에 대한 ddc (decimal digit count) 값은 다음과 같다.

**ddc (decimal digit count) 값**

<a id="7f3ba401cffe454c"></a>
| FLOAT(p) | ddc(p) |
| --- | --- |
| 1 ~ 3 | 1 |
| 4 ~ 6 | 2 |
| 7 ~ 9 | 3 |
| 10 ~ 13 | 4 |
| 14 ~ 16 | 5 |
| 17 ~ 19 | 6 |
| 20 ~ 23 | 7 |
| 24 ~ 26 | 8 |
| 27 ~ 29 | 9 |
| 30 ~ 33 | 10 |
| 34 ~ 36 | 11 |
| 37 ~ 39 | 12 |
| 40 ~ 43 | 13 |
| 44 ~ 46 | 14 |
| 47 ~ 49 | 15 |
| 50 ~ 53 | 16 |
| 54 ~ 56 | 17 |
| 57 ~ 59 | 18 |
| 60 ~ 63 | 19 |
| 64 ~ 66 | 20 |
| 67 ~ 69 | 21 |
| 70 ~ 73 | 22 |
| 74 ~ 76 | 23 |
| 77 ~ 79 | 24 |
| 80 ~ 83 | 25 |
| 84 ~ 86 | 26 |
| 87 ~ 89 | 27 |
| 90 ~ 93 | 28 |
| 94 ~ 96 | 29 |
| 97 ~ 99 | 30 |
| 100 ~ 103 | 31 |
| 104 ~ 106 | 32 |
| 107 ~ 109 | 33 |
| 110 ~ 113 | 34 |
| 114 ~ 116 | 35 |
| 117 ~ 119 | 36 |
| 120 ~ 123 | 37 |
| 124 ~ 126 | 38 |

참고로 모든 numeric type은 동일한 구조로 관리되며, 각 numeric type은 다음과 같은 NUMBER(p,s) 표현식과 동일하다.

**Numeric type 들의 NUMBER 표현식**

<a id="671b1e9cf7ca45bb"></a>
| Numeric type | NUMBER(p,s) 표현식 |
| --- | --- |
| SMALLINT | NUMBER(5,0) |
| INTEGER | NUMBER(10,0) |
| BIGINT | NUMBER(19,0) |
| NUMERIC | NUMBER(38,0) |
| NUMERIC(p) | NUMBER(p,0) |
| NUMERIC(p,s) | NUMBER(p,s) |
| NUMBER(p) | NUMBER(p,0) |
| NUMBER(p,s) | NUMBER(p,s) |
| REAL | NUMBER(8,N/A) <= FLOAT(24) |
| DOUBLE PRECISION | NUMBER(16,N/A) <= FLOAT(53) |
| FLOAT | NUMBER(38,N/A) <= FLOAT(126) |
| FLOAT(p) | NUMBER( ddc(p), N/A ) |
| NUMBER | NUMBER(38, N/A ) |

Native 숫자형은 C 언어의 숫자형 타입과 동일한 데이터 타입이며 서로 다른 타입으로 변환할 수 없다.

**Native 숫자형의 변환**

<a id="1645636ac5446d0d"></a>
| from \ to | NATIVE_SMALLINT | NATIVE_INTEGER | NATIVE_BIGINT | NATIVE_REAL | NATIVE_DOUBLE |
| --- | --- | --- | --- | --- | --- |
| NATIVE_SMALLINT | O | X | X | X | X |
| NATIVE_INTEGER | X | O | X | X | X |
| NATIVE_BIGINT | X | X | O | X | X |
| NATIVE_REAL | X | X | X | O | X |
| NATIVE_DOUBLE | X | X | X | X | O |

**Boolean type의 변환**

<a id="5133ea3bf44e5672"></a>
| from \ to | BOOLEAN |
| --- | --- |
| BOOLEAN | O |

**Date/ time type의 변환 (TZ: WITH TIME ZONE)**

<a id="cd1c28a08a5e65a9"></a>
| from \ to | DATE | TIME | TIME(g) | TIME TZ | TIME(g) TZ | TIMESTAMP | TIMESTAMP(g) | TIMESTAMP TZ | TIMESTAMP(g) TZ |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DATE | O | X | X | X | X | X | X | X | X |
| TIME | X | O | g >= 6 | X | X | X | X | X | X |
| TIME(f) | X | 6 >= f | g >= f | X | X | X | X | X | X |
| TIME TZ | X | X | X | O | g >= 6 | X | X | X | X |
| TIME(f) TZ | X | X | X | 6 >= f | g >= f | X | X | X | X |
| TIMESTAMP | X | X | X | X | X | O | g >= 6 | X | X |
| TIMESTAMP(f) | X | X | X | X | X | 6 >= f | g >= f | X | X |
| TIMESTAMP TZ | X | X | X | X | X | X | X | O | g >= 6 |
| TIMESTAMP(f) TZ | X | X | X | X | X | X | X | 6 >= f | g >= f |

**INTERVAL YEAR TO MONTH 계열의 type 변환 (p,q 가 생략된 경우 2)**

<a id="393269949d9c0ee5"></a>
| from \ to | YEAR(q) | MONTH(q) | YEAR(q) TO MONTH |
| --- | --- | --- | --- |
| YEAR(p) | q >= p | X | X |
| MONTH(p) | X | q >= p | X |
| YEAR(p) TO MONTH | X | X | q >= p |

**INTERVAL DAY TO TIME 계열의 type 변환 (p,q 가 생략된 경우 2) (f,g 가 생략된 경우 6)**

<a id="37a83102bf669e0b"></a>
| from \ to | DAY(q) | HOUR(q) | MINUTE(q) | SECOND(q,g) | DAY(q) TO HOUR | DAY(q) TO MINUTE | DAY(q) TO SECOND(g) | HOUR(q) TO MINUTE | HOUR(q) TO SECOND(g) | MINUTE(q) TO SECOND(g) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DAY(p) | q >= p | X | X | X | X | X | X | X | X | X |
| HOUR(p) | X | q >= p | X | X | X | X | X | X | X | X |
| MINUTE(p) | X | X | q >= p | X | X | X | X | X | X | X |
| SECOND(p,f) | X | X | X | q >= p  g >= f | X | X | X | X | X | X |
| DAY(p) TO HOUR | X | X | X | X | q >= p | X | X | X | X | X |
| DAY(p) TO MINUTE | X | X | X | X | X | q >= p | X | X | X | X |
| DAY(p) TO SECOND(f) | X | X | X | X | X | X | q >= p g >= f | X | X | X |
| HOUR(p) TO MINUTE | X | X | X | X | X | X | X | q >= p | X | X |
| HOUR(p) TO SECOND(f) | X | X | X | X | X | X | X | X | q >= p  g >= f | X |
| MINUTE(p) TO SECOND(f) | X | X | X | X | X | X | X | X | X | q >= p  g >= f |

**ROWID type**

<a id="6f86a12b17deb806"></a>
| from \ to | ROWID |
| --- | --- |
| ROWID | O |

<a id="8346327752432a31"></a>
#### &lt;alter identity column specification&gt;

Column의 identity 속성을 변경한다.   
Column은 identity column 이어야 한다.

- SET GENERATED [ ALWAYS | BY DEFAULT ]
    - identity column의 생성 방식을 변경한다. 
    - 자세한 내용은 [CREATE TABLE](19-sql-references-c-g.md#ce6ecbcf1ea593ea) 구문의 [&lt;identity column specification&gt;](19-sql-references-c-g.md#6aa5dd364ecefc88)을 참조한다. 
- &lt;alter sequence generator restart option&gt; 
    - identity column의 다음 값 (NEXT VALUE)을 변경한다. 
    - 자세한 내용은 [ALTER SEQUENCE](#8163a1ba93288c58) 구문의 &lt;[alter sequence generator restart option&gt;](#76329740529bd55e) 절을 참조한다. 
- &lt;basic sequence generator option&gt; 
    - identity column의 속성을 변경한다. 
    - SQL 표준에서는 SET &lt;basic sequence generator option&gt;의 형태로 기술하도록 정의하고 있으나 생략 가능하다. 
    - 자세한 내용은 [ALTER SEQUENCE](#8163a1ba93288c58) 구문을 참조한다.

<a id="05129798b563ab75"></a>
#### &lt;drop identity property clause&gt;

Column의 identity 속성을 제거한다.   
Column은 identity column 이어야 한다.

<a id="c86004b0abb6f59e"></a>
### 설명

SET NOT NULL 절의 null 검사 수행시간은 테이블의 row 개수에 비례한다.

다음과 같은 column은 NULL 값을 허용하지 않는다. 즉, DROP NOT NULL 절을 수행하더라도 다음 조건 중 하나를 만족할 경우 NULL 값을 허용하지 않는다.

- NOT NULL 제약 조건이 있는 column
- Column이 primary key 제약 조건에 포함되는 경우
- Column이 identity column인 경우

SET DEFAULT 절을 이용한 기본값 변경과 &lt;alter identity column specification&gt; 절을 이용한 identity 속성의 변경은 이후에 수행되는 INSERT 또는 UPDATE 구문에 적용된다.

<a id="aec85a09175057b4"></a>
### 사용 예

다음은 column에 DEFAULT 속성을 설정하는 예이다.

```
gSQL> ALTER TABLE region ALTER COLUMN r_comment SET DEFAULT 'N/A';

Table altered.
```

다음은 column의 DEFAULT 속성을 제거하는 예이다.

```
gSQL> ALTER TABLE region ALTER COLUMN r_comment DROP DEFAULT;

Table altered.
```

다음은 column에 NOT NULL 제약 조건을 설정하는 예이다.

```
gSQL> ALTER TABLE region ALTER COLUMN r_regionkey SET NOT NULL;

Table altered.
```

다음은 column의 NOT NULL 제약 조건을 제거하는 예이다.

```
gSQL> ALTER TABLE region ALTER COLUMN r_regionkey DROP NOT NULL;

Table altered.
```

다음은 column의 data type 크기를 확장하는 예이다.

```
gSQL> ALTER TABLE region ALTER COLUMN r_comment SET DATA TYPE VARCHAR(512);

Table altered.
```

다음은 identity column의 다음 값을 다시 시작하는 예이다.

```
gSQL> ALTER TABLE region ALTER COLUMN r_regionkey RESTART;

Table altered.
```

다음은 column의 identity 속성을 제거하는 예이다.

```
gSQL> ALTER TABLE region ALTER COLUMN r_regionkey DROP IDENTITY;

Table altered.
```

<a id="6b64c0b5bcae8094"></a>
### 호환성

**SQL 표준 호환성**

<a id="3bbbbef8c47f8258"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | X |
| F382 | Alter column data type | O |
| F383 | Set column not null clause | O |
| F384 | Drop identity property value | O |
| F385 | Drop column generation expression clause | X |
| F386 | Set identity column generation clause | O |
| S043 | Enhanced reference types | X |
| T174 | Identity columns | O |
| T178 | Identity columns: simple restart option | O |

<a id="d68bd57bd8466da9"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#1085f15b7d6e9700)
- [ALTER TABLE name ADD COLUMN](#5bf457087cd2404f)
- [ALTER TABLE name SET UNUSED COLUMN](#2389dc92f034f678)
- [ALTER TABLE name RENAME COLUMN](#61e1f15efa661ac2)

<a id="75005eef58445700"></a>
## ALTER TABLE name ALTER CONSTRAINT

<a id="5e380a1336180570"></a>
### 기능

테이블 제약 조건의 특성을 변경한다.

<a id="143927c8dc5e924a"></a>
### 구문

```
<alter table constraint definition> ::=
    ALTER TABLE table_name 
        ALTER <constraint object> <constraint characteristics>
    ;

<constraint object> ::=
      CONSTRAINT constraint_name
    | PRIMARY KEY 
    | UNIQUE ( column_name [, ...] ) 

<constraint characteristics> ::=
      [ NOT ] DEFERRABLE [ <constraint check time> ] [ <constraint enforcement> ]
    | <constraint check time> [ [ NOT ] DEFERRABLE ] [ <constraint enforcement> ]
    | <constraint enforcement>

<constraint check time> ::=
      INITIALLY DEFERRED 
    | INITIALLY IMMEDIATE

<constraint enforcement> ::=
    [NOT] ENFORCED
```

<a id="eb845b8d51f58d1e"></a>
### 사용 범위 및 접근 권한

&lt;alter table constraint definition&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

> Cluster는 지연 가능한 제약 조건을 지원하지 않는다.

<a id="40a4d9556511490e"></a>
### 구문 규칙 및 파라미터

<a id="c8e58b1e0ad7a5e5"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="07ea5e6b6a9bb3a9"></a>
#### &lt;constraint object&gt;

변경할 제약 조건은 다음과 같이 지정할 수 있다.

- CONSTRAINT constraint_name
    - 변경할 제약 조건의 이름이다.
- PRIMARY KEY 
    - 테이블의 PRIMARY KEY 제약 조건이다.
- UNIQUE( column [,...] ) 
    - Column 목록에 부합되는 UNIQUE 제약 조건이다.

<a id="6bd183b844550470"></a>
#### DEFERRABLE | NOT DEFERRABLE

제약 조건의 지연 가능 여부를 변경한다.

- DEFERRABLE
    - 제약 조건을 지연가능하도록 변경한다. 
- NOT DEFERRABLE 
    - 제약 조건을 지연가능하지 않도록 변경한다.

지연가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](20-sql-references-h-z.md#b6ece05278d045fb) 구문의 설명을 참조한다.

<a id="4a843b2cb45936fd"></a>
#### INITIALLY IMMEDIATE | INITIALLY DEFERRED

제약 조건의 검사시점 초기값을 변경한다.

- INITIALLY IMMEDIATE 
    - DML을 수행할 때 제약 조건을 검사한다.
- INITIALLY DEFERRED 
    - COMMIT을 수행할 때 제약 조건을 검사한다.

NOT DEFERRABLE로 정의된 제약 조건은 INITIALLY DEFERRED로 변경할 수 없다.

<a id="f2cad6a5b871b931"></a>
#### [NOT] ENFORCED

제약 조건을 활성화 또는 비활성화 한다.

- ENFORCED
    - 제약 조건을 활성화한다.
- NOT ENFORCED
    - 제약 조건을 비활성화한다.

<a id="28aac641e26d0da4"></a>
### 설명

지연가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](20-sql-references-h-z.md#b6ece05278d045fb) 구문을 참조한다.

<a id="83fc3562c1b5744d"></a>
### 사용 예

다음은 t1_uk 제약 조건을 지연가능하게 하고 검사시점을 DEFERRED로 설정하는 예이다.

```
gSQL> ALTER TABLE t1 ALTER CONSTRAINT t1_uk DEFERRABLE INITIALLY DEFERRED;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="1bd00caf1ed215aa"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- ALTER PRIMARY KEY 절
- ALTER UNIQUE(column [,...]) 절

**SQL 표준 호환성**

<a id="02a589599b65ee98"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F492 | Optional table constraint enforcement | O |

<a id="71b8f952e7d629e8"></a>
## ALTER TABLE name ALTER GLOBAL SECONDARY INDEX

<a id="a31904fdb1bc56f6"></a>
### 기능

테이블에서 global secondary index의 물리적 속성을 변경한다.

<a id="52a28fcaeeb9ddfe"></a>
### 구문

```
<alter table alter global secondary index storage statement> ::=
    ALTER TABLE table_name ALTER GLOBAL SECONDARY INDEX
      <physical attribute clause>
    | [ STORAGE ( <segment attr clause> [...] ) ]
    ;

<physical attribute clause> ::=
      PCTFREE integer
    | INITRANS integer
    | MAXTRANS integer

<segment attr clause> ::=
      INITIAL <size_clause>
    | NEXT <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]
```

<a id="d519633642ef2629"></a>
### 사용 범위 및 접근 권한

&lt;alter table alter global secondary index storage statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="8fff74a15b5b16d8"></a>
### 구문 규칙 및 파라미터

<a id="7aa0d030c390353c"></a>
#### table_name

인덱스를 생성할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="72fdeb3671607034"></a>
#### &lt;physical attribute clause&gt;

인덱스의 물리적 속성 정보를 정의한다.

- PCTFREE integer 
    - 정의 
        - 페이지 내 key 삽입으로 인한 페이지 분할 빈도를 조절하기 위해 예약된 공간이다.
    - 0 에서 99 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기존 인덱스의 설정값을 사용한다.

- INITRANS integer 
    - 정의 
        - 페이지에 동시 접근할 수 있는 초기 트랜잭션의 개수이다. 
        - 인덱스에 접근하는 사용자의 수가 적을 경우에는 INITRANS를 낮게 설정하고, 동시에 접근하는 사용자가 많을 경우에는 INITRANS를 높게 설정한다. 
        - 필요한 경우 설정된 MAXTRANS까지 자동으로 늘어난다. 
    - 1 부터 32 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기존 인덱스의 설정값을 사용한다.

- MAXTRANS integer 
    - 정의 
        - 페이지에 동시 접근할 수 있는 트랜잭션의 최대 개수이다. 
    - 1 부터 32 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기존 인덱스의 설정값을 사용한다.

<a id="bdc7a10c86f61fa0"></a>
#### &lt;segment attr clause&gt;

인덱스가 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer
    - 정의
        - 인덱스를 생성할 때 초기에 할당할 물리적 공간의 크기를 기술한다.
        - integer 값이 EXTENT 두 개 이하인 경우, extent 두 개 크기로 설정된다.
        - integer 값이 EXTENT 두 개 보다 큰 경우, TABLESPACE의 EXTENT 크기에 맞춰 (aligned) 설정된다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기존 인덱스의 설정값을 사용한다.

- NEXT integer
    - 정의
        - 인덱스의 물리적 공간을 추가할 경우 할당할 물리적 공간의 크기를 기술한다.
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT크기가 8192 bytes일 경우 'NEXT 100'은 실제 8192 bytes로 작동한다.)
        - NEXT는 현재 인덱스가 사용할 수 있는 남은 공간의 크기 (MAXEXTENTS의 크기에서 현재 사용하고 있는 공간의 크기를 뺀 크기)에 따라 다음과 같이 작동한다.  
      - 남은 공간의 크기가 0인 경우 더 이상 공간을 확장하지 못한다.  
      - 남은 공간의 크기가 0보다 크고 NEXT보다 작은 경우 남은 공간의 크기만큼 할당한다.  
      - 남은 공간의 크기가 NEXT 보다 클 경우 NEXT의 크기만큼 할당한다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기존 인덱스의 설정값을 사용한다.

<a id="cab022d816c11061"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="56772d7226d53eb7"></a>
### 설명

Non-deterministic 질의를 하려면 global secondary index가 반드시 필요하다.

<a id="0fd863522b2ea285"></a>
### 사용 예

테이블 T1의 global secondary index가 사용할 INITRANS, MAXTRANS 값을 2와 4로 변경한다.

```
gSQL> ALTER TABLE T1 ALTER GLOBAL SECONDARY INDEX INITRANS 2 MAXTRANS 4;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="0522d1ab4af33f35"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="6473f193163cb133"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#ef80852f02ba2cc6)
- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#2bbf4303b4825280)

<a id="fa4377aabfd6b41b"></a>
## ALTER TABLE name ALTER GLOBAL SECONDARY INDEX AGING

<a id="f315352d49d2a829"></a>
### 기능

Global secondary index 의 빈 페이지를 삭제한다.   
DML과 동시에 수행할 수 있다.

<a id="49291b994f7ad6a1"></a>
### 구문

```
<global secondary index aging statement> ::=
    ALTER TABLE table_name ALTER GLOBAL SECONDARY INDEX AGING
        [ AT <domain name> ]
    ;
```

<a id="7bd79814a35636c3"></a>
### 사용 범위 및 접근 권한

&lt;global secondary index aging statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE
    - USAGE TABLESPACE ON DATABASE

<a id="1679eb8c4f3aef8e"></a>
### 구문 규칙 및 파라미터

<a id="d4bf5fe688aab2c4"></a>
#### table_name

대상 테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="16d195ac2ad7c110"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="673f3d682dea3c1b"></a>
### 설명

이 구문은 인덱스 페이지 중 모든 키가 삭제된 페이지를 세그먼트로 반환한다.   
Aging은 논리적 삭제와 물리적 삭제라는 두 단계로 진행된다.

- 논리적 삭제는 인덱스에서 해당 페이지를 가리키는 연결을 끊는 작업이다. 페이지의 마지막 키가 삭제된 시점의 SCN이 시스템의 agable SCN보다 작은 경우에 수행된다.
- 물리적 삭제는 논리적으로 삭제된 페이지를 세그먼트에 반납하는 작업이다. 논리적 삭제 시점의 SCN이 시스템의 agable SCN 보다 작은 경우에 수행된다.

> 시스템의 agable SCN이 증가하지 않으면, INDEX AGING 구문이 성공하더라도 빈 페이지가 삭제되지 않을 수 있다.

<a id="fe1dd6f390831abb"></a>
### 사용 예

다음은 global secondary index를 aging 하는 예이다.

```
gSQL> select table_name, empty_blocks from user_global_secondary_indexes where table_name = 'T1';

TABLE_NAME EMPTY_BLOCKS
---------- ------------
T1                    2

1 row selected.

gSQL> alter table t1 alter global secondary index aging;

Table altered.

gSQL> select table_name, empty_blocks from user_global_secondary_indexes where table_name = 'T1';

TABLE_NAME EMPTY_BLOCKS
---------- ------------
T1                    0

1 row selected.
```

<a id="676b6ca2c2250fc9"></a>
### 호환성

SQL 표준은 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="339f3f931df89fc0"></a>
### 참조

관련 내용은 [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX REBUILD](#5941392c8f076e6f)를 참조한다.

<a id="ea78d0d51ae40ba7"></a>
## ALTER TABLE name ALTER GLOBAL SECONDARY INDEX COALESCE

<a id="c5a1fff33244f984"></a>
### 기능

Global secondary index의 단편화를 제거한다.

<a id="f8356b28261d0e77"></a>
### 구문

```
<global secondary index coalesce statement> ::=
    ALTER TABLE table_name ALTER GLOBAL SECONDARY INDEX COALESCE
        [ AT <domain name> ]
    ;
```

<a id="29d9ab3af61286fd"></a>
### 사용 범위 및 접근 권한

&lt;global secondary index coalesce statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 인덱스를 재구축할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 인덱스를 재구축할 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE
    - USAGE TABLESPACE ON DATABASE

<a id="499e7d6411aa3900"></a>
### 구문 규칙 및 파라미터

<a id="f6b5870e642f07ed"></a>
#### table_name

대상 테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="c50fa267dfce6e67"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="ba027469819cc0cc"></a>
### 설명

- leaf 페이지들을 순차 탐색하며 병합 가능한 페이지들을 병합하고, 제거된 페이지들을 세그먼트로 반환한다.
- UPDATE / DELETE 등으로 인해 발생한 leaf 페이지의 단편화 문제를 해결할 수 있다.
- 인접한 leaf 페이지들이 병합 가능한 경우만 동작하므로 단편화 정도가 낮은 상태에서는 효과가 없을 수 있다.
- 인덱스의 단편화 정도가 심한 경우 INDEX REBUILD보다 더 오래 걸릴 수 있다.

**INDEX REBUILD와 비교**

<a id="283c4ce04aa07c40"></a>
|  | INDEX REBUILD | INDEX COALESCE |
| --- | --- | --- |
| 인덱스 속성 변경 | 가능 | 불가능 |
| 테이블스페이스 이동 | 가능 | 불가능 |
| 테이블 잠금 | 필요 | 불필요 |
| 수행을 위한 추가 공간 | 필요 | 불필요 |
| 트리 높이 감소 | 가능 | 불가능 |

<a id="ea3a4e3f6507be78"></a>
### 사용 예

테이블 T1의 global secondary index의 단편화를 제거한다.

```
gSQL> ALTER TABLE T1 ALTER GLOBAL SECONDARY INDEX COALESCE;

Table altered.
```

<a id="4206309b05036a2c"></a>
### 호환성

SQL 표준은 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="ceada9edb03f08ca"></a>
### 참조

관련 내용은 [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX REBUILD](#5941392c8f076e6f)를 참조한다.

<a id="5941392c8f076e6f"></a>
## ALTER TABLE name ALTER GLOBAL SECONDARY INDEX REBUILD

<a id="f0cd0a49c5428693"></a>
### 기능

Global secondary index를 재구축한다.

<a id="a8bc5dd084ff289f"></a>
### 구문

```
<global secondary index rebuild statement> ::=
    ALTER TABLE table_name ALTER GLOBAL SECONDARY INDEX REBUILD
        [ ONLINE | OFFLINE ]
        [ <index attributes> [...] ]
        [ TABLESPACE tablespace_name ]
        [ AT <domain name> ]
    ;

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

<size clause> ::=
      integer [ K | M | G | T ]

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="497aeb281e9d06da"></a>
### 사용 범위 및 접근 권한

&lt;global secondary index rebuild statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 인덱스를 재구축할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 인덱스를 재구축할 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE
    - USAGE TABLESPACE ON DATABASE

<a id="72346210ecd6f436"></a>
### 구문 규칙 및 파라미터

<a id="29561d6dc2eef8e7"></a>
#### table_name

인덱스를 재구축할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="ac1fac5ec7a95983"></a>
#### [ ONLINE | OFFLINE ]

인덱스를 재구축할 때, 해당 테이블에 DML을 허용할지 여부를 결정한다.

- ONLINE
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE이다.

<a id="185d7bac7429ff45"></a>
#### &lt;physical attribute clause&gt;

인덱스의 물리적 속성 정보를 정의한다.

- PCTFREE integer 
    - 정의 
        - 페이지 내 key 삽입으로 인한 페이지 분할 빈도를 조절하기 위해 예약된 공간이다.
    - 0 에서 99 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

- INITRANS integer 
    - 정의 
        - 페이지에 동시 접근할 수 있는 초기 트랜잭션의 개수이다. 
        - 인덱스에 접근하는 사용자의 수가 적을 경우에는 INITRANS를 낮게 설정하고, 동시에 접근하는 사용자가 많을 경우에는 INITRANS를 높게 설정한다. 
        - 필요한 경우 설정된 MAXTRANS까지 자동으로 늘어난다. 
    - 1 부터 32 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

- MAXTRANS integer 
    - 정의 
        - 페이지에 동시 접근할 수 있는 트랜잭션의 최대 개수이다. 
    - 1 부터 32 까지의 값을 사용할 수 있다. 
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

<a id="784f79539b573bf0"></a>
#### &lt;segment attr clause&gt;

인덱스가 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer
    - 정의
        - 인덱스를 재구축할 때 초기에 할당할 물리적 공간의 크기를 기술한다.
        - integer 값이 EXTENT 두 개 이하인 경우, extent 두 개 크기로 설정된다.
        - integer 값이 EXTENT 두 개 보다 큰 경우, TABLESPACE의 EXTENT 크기에 맞춰 (aligned) 설정된다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

- NEXT integer
    - 정의
        - 인덱스의 물리적 공간을 추가할 경우 할당할 물리적 공간의 크기를 기술한다.
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT크기가 8192 bytes일 경우 'NEXT 100'은 실제 8192 bytes로 작동한다.)
        - NEXT는 현재 인덱스가 사용할 수 있는 남은 공간의 크기 (MAXEXTENTS의 크기에서 현재 사용하고 있는 공간의 크기를 뺀 크기)에 따라 다음과 같이 작동한다.  
      - 남은 공간의 크기가 0인 경우 더 이상 공간을 확장하지 못한다.  
      - 남은 공간의 크기가 0보다 크고 NEXT보다 작은 경우 남은 공간의 크기만큼 할당한다.  
      - 남은 공간의 크기가 NEXT 보다 클 경우 NEXT의 크기만큼 할당한다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

<a id="748f82ca3eab81a5"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="62e5c59208728054"></a>
#### NOPARALLEL | PARALLEL [ integer ]

인덱스 재구축되는 동안 사용될 thread의 개수를 지정한다.

- NOPARALLEL 
    - 인덱스를 병렬로 재구축하지 않는다. 
- PARALLEL [integer] 
    - 인덱스를 병렬로 재구축한다. 
    - integer가 생략되거나 0으로 지정된 경우에는 INDEX_BUILD_PARALLEL_FACTOR 프로퍼티를 따른다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - 만약 integer나 프로퍼티의 값이 0인 경우에는 시스템이 최적값을 결정한다.
- 명시하지 않을 경우, 기본값은 NOPARALLEL이다.

<a id="e423d319d417fc35"></a>
#### TABLESPACE tablespace_name

인덱스가 재구축될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - tablespace_name이 data tablespace면 LOGGING 인덱스로 재구축된다.
    - tablespace_name이 temporary tablespace 또는 nologging tablespace면 NOLOGGING 인덱스로 재구축된다.
- TABLESPACE 절을 생략할 경우, 기존 인덱스의 tablespace로 설정된다.

<a id="56eb15f6aff0b689"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.  
&lt;index attributes&gt; 와 함께 사용할 수 없다.

<a id="999fa968af85e2fd"></a>
### 설명

- 인덱스 단편화 제거
    - 인덱스에 update DML이 빈번하게 수행되는 경우, 인덱스 페이지에 단편화가 발생할 수 있다. 유효한 데이터에 비해 트리가 지나치게 커진 경우, 인덱스의 용량은 커지고 성능은 하락한다. 이 경우, 인덱스를 재구축하면 인덱스 페이지의 단편화를 해결하여 인덱스 용량을 줄이고 성능을 회복할 수 있다.
- 인덱스의 테이블스페이스 변경
    - 기존에 생성된 인덱스의 테이블스페이스를 변경할 수 있다.
    - 단, 테이블스페이스의 TEMPORARY 여부에 따라 로깅 여부를 적절하게 설정해주어야 한다.
- 인덱스의 로깅 설정 변경
    - TABLESPACE 옵션을 사용하여 이미 생성된 인덱스의 로깅 설정을 변경할 수 있다.
    - LOGGING 인덱스로 변경하려는 경우, data tablespace를 TABLESPACE 옵션에 지정해줘야 한다.
    - NOLOGGING 인덱스로 변경하려는 경우, temporary tablespace 또는 nologging tablespace를 TABLESPACE 옵션에 지정해줘야 한다.

<a id="bdaa3b703affb9bc"></a>
### 사용 예

테이블 T1의 global secondary index를 재구축한다.

```
gSQL> ALTER TABLE T1 ALTER GLOBAL SECONDARY INDEX REBUILD;
```

테이블 T1의 global secondary index의 tablespace와 logging 설정을 변경한다.

```
gSQL> ALTER TABLE T1 ALTER GLOBAL SECONDARY INDEX REBUILD TABLESPACE MEM_DATA_TBS;

gSQL> ALTER TABLE T1 ALTER GLOBAL SECONDARY INDEX REBUILD TABLESPACE MEM_TEMP_TBS;
```

<a id="e7141cda5adb90b6"></a>
### 호환성

SQL 표준은 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="edb697cf884fc347"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#ef80852f02ba2cc6)
- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#2bbf4303b4825280)
- [ALTER INDEX name REBUILD](#56aed70ce2b90a69)

<a id="098f7063d2ae708c"></a>
## ALTER TABLE name DROP CONSTRAINT

<a id="44611587bc7de648"></a>
### 기능

테이블 제약 조건을 제거한다.

<a id="80cfa9ee57f357ad"></a>
### 구문

```
<drop table constraint definition> ::=
    ALTER TABLE table_name 
        DROP <constraint object>
        [ <drop behavior> ]
    ;

<constraint object> ::=
      CONSTRAINT constraint_name
    | PRIMARY KEY 
    | UNIQUE ( column_name [, ...] ) 

<drop behavior> ::=
      RESTRICT
    | CASCADE
    | CASCADE CONSTRAINTS
```

<a id="e5fe1d651119ef0e"></a>
### 사용 범위 및 접근 권한

&lt;drop table constraint definition&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 제약 조건의 소유자 
- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="d28dcd1814d9e594"></a>
### 구문 규칙 및 파라미터

<a id="4e1a0493bdee5fd6"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="e48f972ab8d758ec"></a>
#### CONSTRAINT constraint_name

제거할 제약 조건의 이름이다.

<a id="c84fc7e001e4ec34"></a>
#### PRIMARY KEY

테이블의 primary key 제약 조건이다.

<a id="a69342b9516ffdce"></a>
#### UNIQUE( column_name [, ...] )

Column들에 대한 unique 제약 조건이다.

<a id="6b8400b2125bef3f"></a>
#### &lt;drop behavior&gt;

생략할 경우, 기본값은 RESTRICT 이다.

CASCADE 와 CASCADE CONSTRAINTS 는 동일한 의미이다.

제거할 constraint 가 PRIMARY KEY 나 UNIQUE 이고 해당 constraint 를 참조하는 FOREIGN KEY 가 존재할 경우, CASCADE 또는 CASCADE CONSTRAINTS 를 명시해야 한다.

<a id="614f11b72a529b2e"></a>
### 설명

제약 조건의 이름을 사용하지 않고 NOT NULL 제약 조건을 제거하려고 할 경우 [ALTER TABLE name ALTER COLUMN](#0892c59a03976f71) 구문의 &lt;[drop column not null clause&gt;](#a870c65aa3078ece) 절을 이용한다.

FOREIGN KEY는 constraint name 을 지정하여 삭제해야 한다.

```
CREATE TABLE parent ( pk INTEGER PRIMARY KEY );
CREATE TABLE child ( fk INTEGER REFERENCES parent(pk) );
COMMIT;

gSQL> ALTER TABLE child DROP FOREIGN KEY;
ERR-42000(40000): syntax error: 
ALTER TABLE child DROP FOREIGN KEY
                       ^     ^
Error at line 1

gSQL>
SELECT constraint_name
  FROM information_schema.referential_constraints
 WHERE constraint_table_name = 'CHILD'
;

CONSTRAINT_NAME                          
-----------------------------------------
CHILD_FOREIGN_KEY_FK_REFERENCES_PARENT_PK
1 row selected.

gSQL> ALTER TABLE child DROP CONSTRAINT CHILD_FOREIGN_KEY_FK_REFERENCES_PARENT_PK;
Table altered.
```

<a id="20f31ad44dd87a53"></a>
### 사용 예

다음은 테이블의 primary key 제약 조건을 제거하는 예이다.

```
gSQL> ALTER TABLE t1 DROP PRIMARY KEY;

Table altered.
```

다음은 제약 조건 이름을 명시하여 테이블의 제약 조건을 제거하는 예이다.

```
gSQL> ALTER TABLE t1 DROP CONSTRAINT t1_pk;

Table altered.
```

<a id="e0ec1dee1c50364c"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- DROP PRIMARY KEY 
- DROP UNIQUE ( column_name [, ...] ) 
- CASCADE CONSTRAINTS

**SQL 표준 호환성**

<a id="5179e4be967337ba"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="ea30e9c059afb121"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#1085f15b7d6e9700)
- [ALTER TABLE name ADD CONSTRAINT](#b1bf02c95ebfb66d)
- [DROP INDEX](19-sql-references-c-g.md#d01836ffe196ec14)

<a id="2bbf4303b4825280"></a>
## ALTER TABLE name DROP GLOBAL SECONDARY INDEX

<a id="f29a6688a1f4b8a6"></a>
### 기능

테이블에서 global secondary index를 제거한다.

<a id="5102ef38df0132a8"></a>
### 구문

```
<alter table drop global secondary index definition> ::=
    ALTER TABLE table_name 
        DROP GLOBAL SECONDARY INDEX
    ;
```

<a id="bc9a1757dbe239b7"></a>
### 사용 범위 및 접근 권한

&lt;alter table drop global secondary index definition&gt; 구문은 cluster system에서 정의할 수 있으며 사용자는 다음 조건들을 만족해야 한다.

- 인덱스를 제거할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

<a id="8a643a64f307d7d5"></a>
### 구문 규칙 및 파라미터

<a id="0949073d4e221f65"></a>
#### table_name

인덱스를 제거할 테이블 이름이다.

<a id="5f022d08a0c4fd47"></a>
### 설명

Non-deterministic 질의를 하려면 global secondary index가 반드시 필요하다.

<a id="950163bf0347911f"></a>
### 사용 예

테이블 T1에서 global secondary index를 제거한다.

```
gSQL> ALTER TABLE T1 DROP GLOBAL SECONDARY INDEX;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="e7c9bf195bd3e7ba"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="152dada7f4798d0b"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#ef80852f02ba2cc6)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#71b8f952e7d629e8)

<a id="122c923f4ef34146"></a>
## ALTER TABLE name DROP OFFLINE SEGMENTS

<a id="8fea64b458b80ade"></a>
### 기능

오프라인 된 shard들의 세그먼트를 삭제한다.

<a id="33517f3ef37cd5e1"></a>
### 구문

```
<alter table drop offline segments statement> ::=
    ALTER TABLE table_name 
        DROP OFFLINE SEGMENTS    
;
```

<a id="42d5fed9b2d3ffd1"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table drop offline segments statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="ded10b92b6af824a"></a>
### 구문 규칙 및 파라미터

<a id="9fb3c7fe3f1251c5"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="aa4bdc91f3fdffcb"></a>
### 설명

오프라인 된 shard들의 세그먼트를 삭제한다.

&lt;alter table drop offline segments statement&gt;는 inactive cluster member가 있어도 수행할 수 있다.

다음 조건들을 만족하지 못하면 실패한다.

- Cloned 테이블의 세그먼트들을 삭제하려면 클러스터 시스템 내에서 적어도 하나의 멤버에 cloned 테이블의 온라인 replica가 존재해야 한다.
- Sharded 테이블의 세그먼트들을 삭제하려면 그룹 당 적어도 하나의 멤버에 해당 sharded 테이블의 온라인 replica가 존재해야 한다.

예를 들어 sharded 테이블 t1의 cluster group G3에 있는 모든 replica들이 오프라인 상태일 경우 다음과 같은 에러가 발생한다.

```
gSQL> ALTER TABLE t1 DROP OFFLINE SEGMENTS;

ERR-42000(16361): sharded table "PUBLIC"."T1" must have at least one usable replica of group 'G3'
```

모든 테이블들에 대해서 수행하려면 [&lt;alter database drop offline segments statement&gt;](#68248209f3b43891) 구문을 사용한다.

<a id="60ce4bf2aef828e9"></a>
### 사용 예

다음은 테이블 t1에 대해 &lt;alter table drop offline segments statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 DROP OFFLINE SEGMENTS;

Table altered.
```

<a id="9acdf27a034ccfca"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="97b0d828e41f834b"></a>
### 참조

관련 내용은 [ALTER DATABASE DROP OFFLINE SEGMENTS](#68248209f3b43891)를 참조한다.

<a id="436fa49da2672327"></a>
## ALTER TABLE name DROP UNUSABLE SEGMENTS

<a id="0716d755ba7314b4"></a>
### 기능

오프라인 된 replica 들의 세그먼트 중에 unusable 세그먼트를 삭제한다.

<a id="4b5d91a5d5b848ed"></a>
### 구문

```
<alter table drop unusable segments statement> ::=
    ALTER TABLE table_name 
        DROP UNUSABLE SEGMENTS    
;
```

<a id="fb004947441d5578"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table drop unusable segments statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="3d49530783112ace"></a>
### 구문 규칙 및 파라미터

<a id="cbe0c8dcec17e4d9"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="11a258fad9e8840f"></a>
### 설명

Unusable 세그먼트는 더 이상 사용할 수 없는 세그먼트를 의미하며, 다음과 같은 상황에서 생성될 수 있다.

- 특정 세그먼트가 복구 불가능한 상태로 판단되어 [&lt;alter database register statement&gt;](#a996ea8c8491c041)에 의해 등록된 경우
- 로깅 없이 append insert 를 수행한 후, 서버가 checkpoint 없이 비정상 종료된 경우

이 구문은 inactive cluster member가 있어도 수행할 수 있다.

[&lt;alter table drop offline segments statement&gt;](#122c923f4ef34146)와는 달리 온라인 상태의 replica 가 없어도 실행할 수 있다.

모든 테이블들에 대해 동일한 작업을 수행하려면 [&lt;alter database drop offline segments statement&gt;](#68248209f3b43891) 구문을 사용한다.

<a id="6c921de1644af5f9"></a>
### 사용 예

다음은 테이블 t1에 대해 &lt;alter table drop unusable segments statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 DROP UNUSABLE SEGMENTS;

Table altered.
```

<a id="5f795ec1130cf890"></a>
### 호환성

SQL 표준에서는 unusable 세그먼트에 대한 개념을 정의하지 않고 있다.

<a id="354874517a20b86c"></a>
### 참조

관련 내용은 [ALTER TABLE name DROP OFFLINE SEGMENTS](#122c923f4ef34146)를 참조한다.

<a id="b80519a1cdd40ae4"></a>
## ALTER TABLE name DROP SUPPLEMENTAL LOG

<a id="c5b5c8b249ff8421"></a>
### 기능

테이블의 데이터가 변경될 때 redo log에 primary key 정보를 남기지 않도록 설정한다.

<a id="6e37d8d1ec4e7b6d"></a>
### 구문

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="8214d9b1a7a52073"></a>
### 사용 범위 및 접근 권한

&lt;drop table supplemental log statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="37a6fb25105c674a"></a>
### 구문 규칙 및 파라미터

<a id="ec7a7c5ecb98e608"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
[ALTER TABLE name ADD SUPPLEMENTAL LOG](#26bd68efcb7d74f4) 구문을 사용해 설정된 상태여야 한다

<a id="46c20961a6b80c1d"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="992393bf2cb09ca3"></a>
### 사용 예

다음은 테이블의 데이터가 변경되었을 때 redo log에 primary key 정보를 남기지 않도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="f7c548598ebbb990"></a>
### 호환성

SQL 표준에서는 &lt;drop table supplemental log statement&gt;를 다루지 않고 있다.

<a id="c5810c8b8fddc31e"></a>
## ALTER TABLE name MERGE SHARDS

<a id="b66c5b33b983da17"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard들을 merge 하여 재배치한다.

<a id="9ded58476e69a363"></a>
### 구문

```
<alter table merge shards statement> ::=
    ALTER TABLE table_name MERGE SHARDS <source shard list> 
       INTO dest_shard_name [ <dest shard placement> ]
    ;

<source shard list> ::= 
    source_shard_name [, ...]
  | start_shard_name TO end_shard_name

<dest shard placement> ::=
    AT CLUSTER GROUP dest_group_name
```

<a id="19264bb5e4c9188a"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table merge shards statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="5f72bf4852edbce5"></a>
### 구문 규칙 및 파라미터

<a id="e09379ad50f065d6"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
해당 테이블이 cluster-specific이고 list shard 또는 range shard인 경우에만 구문을 수행할 수 있다.

<a id="0c0d1d498a551099"></a>
#### &lt;source shard list&gt;

Merge 할 원본 shard들의 list 이다.  
List에서 지정한 shard가 해당 테이블에 반드시 존재해야 한다.

<a id="520db57e03eb3b90"></a>
#### source_shard_name

Merge 할 원본 shard의 이름이다.  
해당 테이블에 존재하지 않는 shard인 경우 구문을 수행할 수 없다.

<a id="adb785110f618009"></a>
#### start_shard_name

Merge 할 범위 중 시작 shard의 이름이다.   
Range shard에서만 사용된다.

<a id="67f3314d78fdf92b"></a>
#### end_shard_name

Merge 할 범위 중 마지막 shard의 이름이다.  
Range shard에서만 사용된다.

<a id="ad2fa812281f993d"></a>
#### dest_shard_name

대상 shard의 이름이다.

<a id="e7520d21dbaff5c2"></a>
#### &lt;dest shard placement&gt;

대상 shard가 배치될 cluster group의 이름이다.  
해당 구문이 생략된 경우, dest_shard_name이 &lt;source shard list&gt;에 포함되어 있어야 한다.

<a id="27e148b743c820c8"></a>
### 설명

특정 테이블의 특정 shard들을 merge 하여 임의의 cluster group에 배치한다.

- Standalone database에서는 수행할 수 없다.
- Hash sharded table이나 cloned table에는 수행할 수 없다.
- Cluster wide로 생성한 table에는 수행할 수 없다.
- Merge가 진행되는 동안 source shard들에 대한 DML은 수행할 수 없다. 
- Range shard의 경우에는 merge 할 원본 shard의 시작과 끝을 지정할 수 있다.
- Merge 할 원본 shard들은 range shard 또는 list shard에 나열할 수 있다.  
  다만 이 경우, range shard에 나열된 shard들은 모두 이웃한 shard 여야만 한다.

다음은 range sharded 테이블에 나열형으로 인접하지 않은 shard를 merge 하려고 할 때 발생하는 에러이다.

```
CREATE TABLE t1( i1 INTEGER ) 
    SHARDING BY RANGE (i1)
    SHARD shard1 VALUES LESS THAN ( 200 )      AT CLUSTER GROUP G1,
    SHARD shard2 VALUES LESS THAN ( 400 )      AT CLUSTER GROUP G2,
    SHARD shard3 VALUES LESS THAN ( MAXVALUE ) AT CLUSTER GROUP G3
;

Table created.

ALTER TABLE t1 MERGE SHARDS shard1, shard3 INTO shard4 AT CLUSTER GROUP G2;

ERR-42000(16488): shards being merged are not adjacent : 
ALTER TABLE t1 MERGE SHARDS shard1, shard3 INTO shard4 AT CLUSTER GROUP G2
                                    *
ERROR at line 1:
```

<a id="ee1b9c1bee6cbffa"></a>
### 사용 예

다음은 나열형으로 SHARD를 merge 하는 예이다.

```
gSQL> ALTER TABLE t1 MERGE SHARDS shard1, shard2, shard3 INTO shard4 AT CLUSTER GROUP G2;

Table altered
```

다음은 범위형으로 SHARD를 병합하는 예이다.

```
gSQL> ALTER TABLE t1 MERGE SHARDS shard1 TO shard3 INTO shard4 AT CLUSTER GROUP G2;

Table altered
```

<a id="9025812396f41cea"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="82d5032a42e4968f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name MOVE SHARD](#b64b6ca52ad7b811)
- [ALTER TABLE name SPLIT SHARD](#e5ce6718ce23e4e6)

<a id="b64b6ca52ad7b811"></a>
## ALTER TABLE name MOVE SHARD

<a id="41afece56be92ee1"></a>
### 기능

테이블의 특정 shard 또는 특정 cluster group의 전체 shard를 특정 cluster group에 재배치한다.

<a id="47143b166efbb7c8"></a>
### 구문

```
<alter table move shard statement> ::=
    ALTER TABLE table_name MOVE SHARD
        { shard_name_list | FROM CLUSTER GROUP src_cluster_group }
        TO CLUSTER GROUP dest_cluster_group 
       [ ONLINE | OFFLINE ] 
       [ LOGGING | NOLOGGING ] 
       [ <scan partition> ] 
       [ <parallel clause> ]
    ;

<scan partition> ::= 
    SCAN PARTITION integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="21e8d622c1c9d6c3"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table move shard statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="65702c54bb1241ed"></a>
### 구문 규칙 및 파라미터

<a id="c83b97343a2e482a"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
해당 테이블이 cluster group specific인 경우에만 구문을 수행할 수 있다.

<a id="f5ef857b9df9c933"></a>
#### shard_name_list

재배치할 shard name 목록이다.  
해당 테이블에 존재하지 않는 shard인 경우 구문을 수행할 수 없다.

<a id="5d8cf953686b7d0e"></a>
#### src_cluster_group

재배치할 특정 cluster group의 이름이다.

<a id="6fdb2d76e36a6f16"></a>
#### dest_cluster_group

테이블의 shard를 배치할 target cluster group의 이름이다.  
해당 테이블의 shard가 지정한 cluster group에 이미 존재할 경우 구문을 수행할 수 없다.

<a id="cae7f4c0922ab773"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="dc5e8aac89be389e"></a>
#### [ LOGGING | NOLOGGING ]

테이블의 shard를 재배치할 때, 테이블 동기화 과정에서 기록되는 로그의 양을 지정한다.

- LOGGING
    - 테이블 동기화 과정에서 모든 로그를 기록한다.
- NOLOGGING
    - 테이블 동기화 과정에서 최소한의 로그만 기록한다.
- 생략할 경우, 기본값은 LOGGING 이다.

> NOLOGGING 옵션을 사용하면 redo log가 기록되지 않는다. 따라서 move shard 수행 후 서버가 비정상적으로 종료되면 해당 테이블은 unusable 상태가 된다. 이를 방지하려면 move shard 수행 후 CHECKPOINT 구문을 실행해야 한다.

<a id="9fb9934613ea66b1"></a>
#### &lt;scan partition&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버에 재배치 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, ONLINE_DDL_SCAN_PARTITION 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="75a21ef7037557a0"></a>
#### &lt;parallel clause&gt;

테이블 재배치에 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 테이블을 병렬로 재배치하지 않는다.
- PARALLEL [integer] 
    - 테이블을 병렬로 재배치한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="d2954b644bbeb73d"></a>
### 설명

테이블의 특정 shard를 특정 cluster group에서 다른 cluster group으로 재배치한다.

특정 cluster group을 제거하려면 테이블의 shard를 재배치한 후에 [DROP CLUSTER GROUP](19-sql-references-c-g.md#d4612fb5786bb45f) 구문을 수행해야 한다.

모든 테이블의 shard를 특정 cluster group에서 다른 cluster group으로 이동시키는 경우, ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP TO CLUSTER GROUP 구문을 수행한다.

CLONED 테이블이거나 CLUSTER WIDE로 설정된 테이블의 경우 에러가 발생하면서 실패할 수 있다.

<a id="1c2d9f960e3deee6"></a>
### 사용 예

다음은 &lt;alter table move shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 MOVE SHARD shard1, shard2 TO CLUSTER GROUP g3;

Table altered.

gSQL> ALTER TABLE t1 MOVE SHARD FROM CLUSTER GROUP g1 TO CLUSTER GROUP g3;

Table altered.
```

다음은 CLONED 테이블과 CLUSTER WIDE로 설정된 테이블이 move shard에 실패하는 예이다.

```
gSQL> CREATE TABLE T1 ( C1 INTEGER ) SHARDING BY RANGE (C1)
         AT CLUSTER WIDE
         SHARD s1 VALUES LESS THAN (10),                                      
         SHARD s2 VALUES LESS THAN (MAXVALUE);

Table created.

gSQL> ALTER TABLE T1 MOVE SHARD s1 TO CLUSTER GROUP g2;

ERR-42000(16440): cannot execute on cluster wide sharded tables

gSQL> CREATE TABLE T2 ( C1 INTEGER ) CLONED AT CLUSTER GROUP g1, g2;

Table created.

gSQL> ALTER TABLE T2 MOVE SHARD FROM CLUSTER GROUP g1 TO CLUSTER GROUP g3;

ERR-42000(16437): cannot execute on cloned tables
```

<a id="abc1a8705bd2fce0"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="5ac16648916b5964"></a>
### 참조

관련 내용은 [ALTER DATABASE MOVE SHARD](#4752ea45b3668af4)를 참조한다.

<a id="ce8f360419a55df6"></a>
## ALTER TABLE name OFFLINE INACTIVE CLUSTER MEMBERS

<a id="9c305981f593188a"></a>
### 기능

테이블의 cluster member 정보에서 모든 inactive cluster member 를 offline 상태로 변경한다. 즉, 해당 cluster member 의 shard map 을 offline 상태로 변경한다.

<a id="e6e520f499ce07ad"></a>
### 구문

```
<alter table offline inactive cluster members statement> ::=
    ALTER TABLE table_name OFFLINE INACTIVE CLUSTER MEMBERS
    ;
```

<a id="fc694b0f3799662a"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table offline inactive cluster members statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="dfb9e350616f09d3"></a>
### 구문 규칙 및 파라미터

<a id="46316fbd09e5e5b4"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="35af2bcd96bdbaf7"></a>
### 설명

테이블의 shard가 존재하는 모든 inactive cluster member 가 더 이상 cluster member 에 포함될 수 없는 경우에 사용한다.

또한, inactive cluster member가 cluster system에 다시 join 하려면 모든 멤버에서 offline 상태여야 한다.

비활성화된 cluster member 에 대해 database의 모든 테이블을 offline 상태로 변경하려면 [&lt;alter database offline inactive cluster members&gt;](#98259b572214ad92) 구문을 수행한다.

<a id="b35bff5f17b507e3"></a>
### 사용 예

다음은 테이블 t1에 대해 &lt;alter table offline inactive cluster members statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 OFFLINE INACTIVE CLUSTER MEMBERS;

Table altered.
```

<a id="5c8afb2415015a19"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="d834d728f2c4e160"></a>
### 참조

관련 내용은 [ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS](#98259b572214ad92)를 참조한다.

<a id="9f7366fab122ef37"></a>
## ALTER TABLE name READ { ONLY | WRITE }

<a id="0c17693d15f1ecfa"></a>
### 기능

테이블에 READ { ONLY | WRITE }을 설정한다.

<a id="56dd54979b346eff"></a>
### 구문

```
<alter table read { only | write } statement> :==
     ALTER TABLE table_name
         READ { ONLY | WRITE }
     ;
```

<a id="c6db9836cc55ff8d"></a>
### 사용 범위 및 접근 권한

&lt;alter table read { only | write } statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="a84cdeae92db6acb"></a>
### 구문 규칙 및 파라미터

<a id="6e8e65d5847bda52"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="921a703ca2f538ae"></a>
### 설명

테이블의 속성을 READ { ONLY | WRITE } 으로 지정한다.

READ ONLY로 지정하면 SELECT .. FOR UPDATE 구문, 테이블의 데이터가 변경되는 DML 또는 DDL 구문들을 사용할 수 없다. 반면, 테이블의 데이터가 변경이 되지 않는 DDL 구문은 허용한다.

> READ ONLY로 지정할 때 허용하지 않는 SQL 구문
> 
> - INSERT, UPDATE, DELETE
> - TRUNCATE
> - SELECT .. FOR UPDATE
> - ALTER TABLE RENAME/DROP COLUMN
> - ALTER TABLE SET COLUMN UNUSED
> 
>   
> READ ONLY로 지정할 때 허용하는 SQL 구문
> 
> - SELECT
> - CREATE/ALTER/DROP INDEX
> - ALTER TABLE ADD/ALTER COLUMN
> - ALTER TABLE ADD/ALTER/RENAME/DROP CONSTRAINT
> - ALTER TABLE for physical property changes
> - ALTER TABLE DROP UNUSED COLUMNS
> - ALTER TABLE RENAME TO
> - DROP TABLE
> - ALTER TABLE ADD/DROP SUPPLEMENTAL LOG
> - LOCK TABLE
> 

<a id="e142158a1298367e"></a>
### 사용 예

다음은 &lt;alter table read { only | write } statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 READ ONLY;

Table altered.

gSQL> ALTER TABLE t1 READ WRITE;

Table altered.
```

<a id="6b091f9bd42079fa"></a>
### 호환성

SQL 표준에서는 &lt;alter table read { only | write } statement&gt; 구문을 정의하지 있지 않다.

<a id="0dc36a63e9e0d9a6"></a>
### 참조

관련 내용은 [ALTER TABLE](#1085f15b7d6e9700)을 참조한다.

<a id="4dcbc8cc43487ef2"></a>
## ALTER TABLE name REBALANCE

<a id="0c743b51869bbd6d"></a>
### 기능

테이블의 shard를 재배치한다.

<a id="0f31582baa22238e"></a>
### 구문

```
<alter table rebalance statement> ::=
    ALTER TABLE table_name REBALANCE 
       [ ONLINE | OFFLINE ] 
       [ LOGGING | NOLOGGING ]
       [ <scan partition> ] 
       [ <parallel clause> ]
    ;

<scan partition> ::= 
    SCAN PARTITION integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="efc32d68b3791216"></a>
### 사용 범위 및 접근 권한

Cluster system 에서 수행할 수 있다.

&lt;alter table rebalance statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="eca0dae57baf9d77"></a>
### 구문 규칙 및 파라미터

<a id="dfed41781dd65b33"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="b5347faa81fad582"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="34dec27d37306939"></a>
#### [ LOGGING | NOLOGGING ]

테이블의 shard를 재배치할 때, 테이블 동기화 과정에서 기록되는 로그의 양을 지정한다.

- LOGGING
    - 테이블 동기화 과정에서 모든 로그를 기록한다.
- NOLOGGING
    - 테이블 동기화 과정에서 최소한의 로그만 기록한다.
- 생략할 경우, 기본값은 LOGGING 이다.

> NOLOGGING 옵션을 사용하면 redo log가 기록되지 않는다. 따라서 rebalance 수행 후 서버가 비정상적으로 종료되면 해당 테이블은 unusable 상태가 된다. 이를 방지하려면 rebalance 수행 후 CHECKPOINT 구문을 실행해야 한다.

<a id="b85f36c240fbae0c"></a>
#### &lt;scan partition&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버에 재배치 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, ONLINE_DDL_SCAN_PARTITION 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="adb7634e03e08988"></a>
#### &lt;parallel clause&gt;

테이블 재배치에 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 테이블을 병렬로 재배치하지 않는다.
- PARALLEL [integer] 
    - 테이블을 병렬로 재배치한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="d8aa80eb0d519634"></a>
### 설명

다음과 같은 구문을 통해 cluster member, cluster group을 추가할 때 table들의 shard는 재배치하지 않는다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#cb13f01b6a67d24a)
- [ALTER CLUSTER GROUP name ADD MEMBER](#1b3565c76f35ea0a)

추가된 cluster group과 cluster member의 테이블 shard를 재배치하려면 &lt;alter table rebalance statement&gt; 구문을 수행한다. 테이블의 shard 가 이미 재배치된 경우, 별도의 재배치 작업없이 성공한다.

모든 테이블들의 shard를 재배치하려면 [ALTER DATABASE REBALANCE](#045abf2d149b6478) 구문을 수행한다.

<a id="4d3a60b0765f1d89"></a>
### 사용 예

다음은 &lt;alter table rebalance statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 REBALANCE;

Table altered.
```

<a id="36612e304c55d785"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="5f2f7d4e4bdedbe5"></a>
## ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list

<a id="e6f5f3a0b91c05a6"></a>
### 기능

특정 cluster group에 shard를 포함하지 않도록 테이블의 shard를 재배치한다.

<a id="32d5dd0493289ee5"></a>
### 구문

```
<alter table rebalance exclude cluster group statement> ::=
    ALTER TABLE table_name REBALANCE 
        EXCLUDE CLUSTER GROUP cluster_group_list 
       [ ONLINE | OFFLINE ] 
       [ LOGGING | NOLOGGING ]
       [ <scan partition> ] 
       [ <parallel clause> ]
    ;

<scan partition> ::= 
    SCAN PARTITION integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="43cdf2d848e7bfa1"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table rebalance exclude cluster group statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="017332d8b916dcac"></a>
### 구문 규칙 및 파라미터

<a id="fd1c0ca986c8620a"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
해당 테이블이 cluster-wide인 경우에만 구문을 수행할 수 있다.

<a id="bfad07bffaf8faad"></a>
#### cluster_group_list

테이블의 shard를 포함하지 않는 cluster group의 list이다.   
재배치에서 제외될 cluster group이 cluster 전체 group인 경우 구문을 수행할 수 없다.

<a id="53cdc52879868adc"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE 를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE 를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="8471bba6b6a577f4"></a>
#### [ LOGGING | NOLOGGING ]

테이블의 shard를 재배치할 때, 테이블 동기화 과정에서 기록되는 로그의 양을 지정한다.

- LOGGING
    - 테이블 동기화 과정에서 모든 로그를 기록한다.
- NOLOGGING
    - 테이블 동기화 과정에서 최소한의 로그만 기록한다.
- 생략할 경우, 기본값은 LOGGING 이다.

> NOLOGGING 옵션을 사용하면 redo log가 기록되지 않는다. 따라서 rebalance 수행 후 서버가 비정상적으로 종료되면 해당 테이블은 unusable 상태가 된다. 이를 방지하려면 rebalance 수행 후 CHECKPOINT 구문을 실행해야 한다.

<a id="d68dfec8159b6aaa"></a>
#### &lt;scan partition&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버에 재배치 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, ONLINE_DDL_SCAN_PARTITION 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="71a8b28ac9f75f30"></a>
#### &lt;parallel clause&gt;

테이블 재배치에 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 테이블을 병렬로 재배치하지 않는다.
- PARALLEL [integer] 
    - 테이블을 병렬로 재배치한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="24d2d1d23a525d40"></a>
### 설명

특정 cluster group을 배제하고 테이블의 shard를 재배치한다.   
해당 cluster group에 테이블의 shard가 존재하지 않을 경우, 별도의 재배치 작업없이 성공한다.   
테이블의 shard가 위치한 cluster group을 기준으로 shard를 재배치한다.

특정 cluster group을 제거하려면 테이블의 shard를 재배치한 후에 [DROP CLUSTER GROUP](19-sql-references-c-g.md#d4612fb5786bb45f) 구문을 수행해야 한다.  
모든 테이블들에서 cluster group을 배제하고 shard를 재배치하고자 할 경우, [ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP](#b2d27be01aaaa9b7)을 수행한다.

<a id="7be0965c7e8209dc"></a>
### 사용 예

다음은 &lt;alter table rebalance exclude cluster group statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 REBALANCE EXCLUDE CLUSTER GROUP g3;

Table altered.
```

<a id="92f602f69a4563d7"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="61e1f15efa661ac2"></a>
## ALTER TABLE name RENAME COLUMN

<a id="ad1fd7662d6b3d37"></a>
### 기능

테이블 column의 이름을 변경한다.

<a id="4111e3761fe8850a"></a>
### 구문

```
<rename column statement> ::=
    ALTER TABLE table_name 
        RENAME COLUMN old_column_name TO new_column_name
    ;
```

<a id="ee5de37838aff9f8"></a>
### 사용 범위 및 접근 권한

&lt;rename column statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="c03e1bbbcf8137f7"></a>
### 구문 규칙 및 파라미터

<a id="066dc5a67a9c228f"></a>
#### table_name

변경할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="0d4a151a2ff63ead"></a>
#### old_column_name

변경할 column의 기존 이름이다.

<a id="4b5e13e73c9f5827"></a>
#### new_column_name

변경할 column의 새로운 이름이다.   
테이블 내에 동일한 column 이름이 존재하지 않아야 한다.

<a id="79efc34023bd642d"></a>
### 설명

Column 이름이 변경되더라도 이전에 해당 column을 기준으로 생성된 index, constraint 등의 객체를 변경할 필요는 없다.

Column 이름이 변경되더라도, CHECK 제약 조건의 의미는 다음과 같이 그대로 유지된다.

```
CREATE TABLE t1 ( c1 INTEGER, c2 INTEGER,
                  CONSTRAINT t1_check CHECK ( c1 > c2 ) );

gSQL>
SELECT constraint_name, check_clause
  FROM information_schema.check_constraints
 WHERE constraint_table = 'T1';

CONSTRAINT_NAME CHECK_CLAUSE        
--------------- --------------------
T1_CHECK        CHECK( "C1" > "C2" )

1 row selected.

gSQL> INSERT INTO t1 VALUES ( 1, 2 );
ERR-23000(16665): check constraint "PUBLIC"."T1_CHECK" violated

gSQL> ALTER TABLE t1 RENAME COLUMN c1 TO tmp;
Table altered.

gSQL> INSERT INTO t1 VALUES ( 1, 2 );
ERR-23000(16665): check constraint "PUBLIC"."T1_CHECK" violated

gSQL> ALTER TABLE t1 RENAME COLUMN c2 TO c1;
Table altered.

gSQL> INSERT INTO t1 VALUES ( 1, 2 );
ERR-23000(16665): check constraint "PUBLIC"."T1_CHECK" violated

gSQL> ALTER TABLE t1 RENAME COLUMN tmp TO c2;
Table altered.

gSQL> INSERT INTO t1 VALUES ( 1, 2 );
ERR-23000(16665): check constraint "PUBLIC"."T1_CHECK" violated

gSQL>
SELECT constraint_name, check_clause
  FROM information_schema.check_constraints
 WHERE constraint_table = 'T1';

CONSTRAINT_NAME CHECK_CLAUSE        
--------------- --------------------
T1_CHECK        CHECK( "C2" > "C1" )

1 row selected.
```

<a id="d494702835db3cf4"></a>
### 사용 예

다음은 두 개의 column 이름인 col_1과 col_2를 서로 바꾸는 예이다.

```
gSQL> ALTER TABLE t1 RENAME COLUMN col_1 TO col_temp;

Table altered.

gSQL> ALTER TABLE t1 RENAME COLUMN col_2 TO col_1;

Table altered.

gSQL> ALTER TABLE t1 RENAME COLUMN col_temp TO col_2;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="7ec15a4ac2b0428e"></a>
### 호환성

SQL 표준에서는 &lt;rename column statement&gt; 구문을 정의하지 않고 있다.

<a id="f6f544bdcdb764ee"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#1085f15b7d6e9700)
- [ALTER TABLE name ADD COLUMN](#5bf457087cd2404f)
- [ALTER TABLE name SET UNUSED COLUMN](#2389dc92f034f678)
- [ALTER TABLE name ALTER COLUMN](#0892c59a03976f71)

<a id="662d1bdaf11f8e22"></a>
## ALTER TABLE name RENAME CONSTRAINT

<a id="d4c1ee18c6069f55"></a>
### 기능

테이블 제약 조건의 이름을 변경한다.

<a id="ed34e5682b0f6f64"></a>
### 구문

```
<rename table constraint statement> ::=
    ALTER TABLE table_name 
        RENAME <constraint object> TO new_constraint_name
    ;

<constraint object> ::=
      CONSTRAINT constraint_name
    | PRIMARY KEY 
    | UNIQUE ( column_name [, ...] )
```

<a id="0771ef4f724e9ce5"></a>
### 사용 범위 및 접근 권한

&lt;rename table constraint statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="922255fa5c36bcbf"></a>
### 구문 규칙 및 파라미터

<a id="15c241e1f666becb"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="8290e9b702da7e9a"></a>
#### &lt;constraint object&gt;

변경할 제약 조건의 기존 이름은 다음과 같이 지정할 수 있다.

- CONSTRAINT constraint_name
    - 변경할 제약 조건의 이름이다.
- PRIMARY KEY
    - 테이블의 PRIMARY KEY 제약 조건이다.
- UNIQUE( column [,...] )
    - Column 목록에 부합되는 UNIQUE 제약 조건이다.

<a id="701274ff0aac32ec"></a>
#### new_column_name

변경할 제약 조건의 새로운 이름이다.

<a id="3b032074952c8af3"></a>
### 설명

Primary key, unique key와 같이 key 제약 조건으로 자동 생성된 index의 이름은 변경되지 않는다. Index 이름은 [ALTER INDEX name RENAME TO](#ce4a5d821138cd3a) 구문을 사용하여 변경해야 한다.

<a id="1e463ad1ea9c91f2"></a>
### 사용 예

다음은 테이블의 primary key 제약 조건의 이름을 변경하는 예이다.

```
gSQL> ALTER TABLE t1 RENAME PRIMARY KEY TO pk_t1;

Table altered.
```

다음은 제약 조건 이름을 명시하여 테이블의 제약 조건 이름을 변경하는 예이다.

```
gSQL> ALTER TABLE t1 RENAME CONSTRAINT pk_t1 TO t1_pk;

Table altered.
```

<a id="dfb8f1831171f8b5"></a>
### 호환성

SQL 표준에서는 &lt;rename table constraint statement&gt; 구문을 정의하지 않고 있다.

<a id="ac361a1f7d1adcba"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#1085f15b7d6e9700)
- [ALTER TABLE name ADD CONSTRAINT](#b1bf02c95ebfb66d)
- [ALTER TABLE name DROP CONSTRAINT](#098f7063d2ae708c)
- [ALTER TABLE name ALTER CONSTRAINT](#75005eef58445700)

<a id="0976d6b11dbb86a3"></a>
## ALTER TABLE name RENAME SHARD

<a id="ea7f8def7fcc4656"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard의 이름을 변경한다.

<a id="5b4c1fd2de109076"></a>
### 구문

```
<alter table rename shard statement> ::=
    ALTER TABLE table_name 
        RENAME SHARD shard_name TO new_shard_name
    ;
```

<a id="02887d8802522696"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table rename shard statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="0cdb7d3b027bf3eb"></a>
### 구문 규칙 및 파라미터

<a id="b645bc14af29f27e"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="9bbb2fb1e62aa5b4"></a>
#### shard_name

변경할 shard의 기존 이름이다.   
Shard가 해당 테이블에 존재하지 않을 경우 구문을 수행할 수 없다.

<a id="a57c730f4a0ce759"></a>
#### new_shard_name

변경할 shard의 새 이름이다.   
테이블 내에 동일한 shard 이름이 존재하지 않아야 한다.

<a id="ae04b667e0d41843"></a>
### 설명

Hash, range, list 테이블의 특정 shard의 이름을 변경한다. Cloned 테이블에 대해서는 해당 구문을 수행할 수 없다.

<a id="f97411883105784c"></a>
### 사용 예

다음은 &lt;alter table rename shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t_range RENAME SHARD r_01 TO r_new_01;

Table altered.

gSQL> ALTER TABLE t_list RENAME SHARD l_01 TO l_new_01;

Table altered.

gSQL> ALTER TABLE t_hash RENAME SHARD shard_000000 TO h_new_00;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="2b9ee4eb4a345b1e"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="204b2c1c3299452f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#1085f15b7d6e9700)
- [ALTER TABLE name MOVE SHARD](#b64b6ca52ad7b811)
- [ALTER TABLE name SPLIT SHARD](#e5ce6718ce23e4e6)
- [ALTER TABLE name REBALANCE](#4dcbc8cc43487ef2)

<a id="81ef596f170298aa"></a>
## ALTER TABLE name RENAME TO

<a id="fd961932504df312"></a>
### 기능

테이블의 이름을 변경한다.

<a id="6c65ee18fa6f62ba"></a>
### 구문

```
<rename table statement> ::=
    ALTER TABLE table_name 
        RENAME TO new_table_name
    ;
```

<a id="a89d8a819fd5b589"></a>
### 사용 범위 및 접근 권한

&lt;rename table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="5f29b42331afe32a"></a>
### 구문 규칙 및 파라미터

<a id="2e4b06ce9084d87e"></a>
#### table_name

변경할 테이블의 이름이다.    
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="67a610f1ce5dfcfc"></a>
#### new_table_name

테이블의 새 이름이다.   
스키마 내에 동일한 테이블 이름이 존재하지 않아야 한다.

<a id="ea9bc82a2faee194"></a>
### 설명

테이블 이름이 변경되더라도 이를 참조하는 index constraint 등의 객체는 변경할 필요없다.

<a id="06c804b38e1e1440"></a>
### 사용 예

다음은 두 테이블 t1, t2의 이름을 서로 바꾸는 예이다.

```
gSQL> ALTER TABLE t1 RENAME TO t_temp;

Table altered.

gSQL> ALTER TABLE t2 RENAME TO t1;

Table altered.

gSQL> ALTER TABLE t_temp RENAME TO t2;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="89739dcb54d08a7a"></a>
### 호환성

SQL 표준에서는 &lt;rename table statement&gt; 구문을 정의하지 않고 있다.

<a id="88d6f4aaa33a59ba"></a>
### 참조

관련 내용은 [ALTER TABLE](#1085f15b7d6e9700)을 참조한다.

<a id="b33b38d54cfadfd0"></a>
## ALTER TABLE name REORGANIZE

<a id="53e0e59f0d0413b6"></a>
### 기능

테이블을 물리적으로 재구성한다.

<a id="f5ad0ee258281322"></a>
### 구문

```
<alter table reorganize statement> ::=
    ALTER TABLE table_name REORGANIZE 
       [ LOGGING| NOLOGGING ] 
       [ ONLINE | OFFLINE ] 
       [ <scan partition> ] 
       [ <parallel clause> ]
       [ AT <domain name> ]
    ;

<scan partition> ::=
    SCAN PARTITION integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="8b9046ada0da71ab"></a>
### 사용 범위 및 접근 권한

&lt;alter table reorganize statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="1b548ad0b4a85cd4"></a>
### 구문 규칙 및 파라미터

<a id="ed2f47079f6c0d30"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="6e713bcc42094978"></a>
#### [ LOGGING | NOLOGGING ]

테이블을 재구성할 때 redo log를 기록할지 여부를 결정한다.

- LOGGING 
    - Redo log를 기록한다. 
- NOLOGGING 
    - Redo log를 기록하지 않는다.
- 생략할 경우, 기본값은 LOGGING 이다.

> NOLOGGING 옵션을 사용하면 redo log가 기록되지 않는다. 따라서 reorganize 수행 후 서버가 비정상적으로 종료되면 해당 테이블은 unusable 상태가 된다. 이를 방지하려면 reorganize 수행 후 CHECKPOINT 구문을 실행해야 한다.

<a id="3603e8897ff334c9"></a>
#### [ ONLINE | OFFLINE ]

테이블을 재구성할 때 DML을 허용할지 여부를 결정한다

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="f8609183b99b6ca5"></a>
#### &lt;scan partition&gt;

주어진 개수만큼 테이블을 분할하여 새로운 테이블에 동기화 한다.

- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, ONLINE_DDL_SCAN_PARTITION 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="1fb8cc0690d3c165"></a>
#### &lt;parallel clause&gt;

테이블 재구성할 때 사용할 thread 개수를 지정한다.

- NOPARALLEL
    - 테이블을 병렬로 재배치하지 않는다.
- PARALLEL [integer] 
    - 테이블을 병렬로 재배치한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="68c5cad8fee1b6fd"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.   
Cluster database 전용 옵션이다.

<a id="f9d90e203b9dc3fb"></a>
### 설명

테이블 재구성 (Table Reorganization)은 테이블의 물리적 구조를 재배치하여 질의 성능을 향상시키거나 저장 공간을 최적화하는 작업이다.  
테이블 페이지 내의 빈 공간을 제거함으로써 테이블의 물리적 크기를 줄일 수 있다.

테이블 재구성의 특징은 다음과 같다.

- 테이블과 관련된 인덱스도 함께 재구성된다. (단, DISABLE/UNUSABLE 상태의 인덱스는 제외된다.)
- OPEN 이상의 단계에서만 재구성을 수행할 수 있다.
- 재구성 대상 member는 inactive member 가 아니어야 한다. 
- READ ONLY 테이블에도 수행할 수 있다. 
- IMMUTABLE 테이블에도 수행할 수 있다.
- Recyclebin 에 있는 테이블에도 수행할 수 있다.


> 
> - 다음 조건을 충족하지 못할 경우 재구성은 실패한다.
>     - 테이블 또는 관련 인덱스가 ONLINE 테이블스페이스에 존재해야 한다.
>     - 테이블은 USABLE 또는 ONLINE 상태여야 한다.
> - 재구성은 기존에 사용하던 공간을 재활용하지 않고, 새로운 세그먼트를 생성하여 데이터를 복사하는 방식으로 진행된다. 따라서 추가 공간이 필요하며, 필요한 공간의 최대 크기는 기존 테이블이 사용하던 공간의 크기와 같다.
> 

<a id="bbf45b173048728b"></a>
### 사용 예

다음은 &lt;alter table reorganize statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 REORGANIZE;

Table altered.
```

<a id="fead40774ffaa08e"></a>
### 호환성

SQL 표준에서는 reorganize 에 대한 개념을 정의하지 않고 있다.

<a id="b3055349d40e2a5d"></a>
### 참조

관련 내용은 [ALTER TABLE](#1085f15b7d6e9700)을 참조한다.

<a id="e99539acedd7cb13"></a>
## ALTER TABLE name SET TRIGGER ORDER

<a id="dc65eeb22970391b"></a>
### 기능

Table 에 생성한 trigger 들의 실행 순서를 변경한다.

<a id="b25700669bf2381a"></a>
### 구문

```
<alter table set trigger order statement> ::=
    ALTER TABLE <table_name> SET TRIGGER ORDER <trigger_name> [, ...]
    ;
```

<a id="2ec0c03f2f19b610"></a>
### 사용 범위 및 접근 권한

&lt;alter table set trigger order statement&gt; 구문을 실행하기 위해 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="c987fdddc3ec51d5"></a>
### 구문 규칙 및 파라미터

<a id="7107aa0bf8e78a25"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="b95c25e73024749d"></a>
#### &lt;trigger name&gt; [, ... ]

나열된 모든 trigger 들은 다음 조건을 만족해야 한다.

- &lt;table name&gt; 에 생성된 trigger 여야 한다.
- action timing( BEFORE / AFTER ) 이 동일해야 한다.
- action orientation( FOR EACH ROW / FOR EACH STATEMENT ) 이 동일해야 한다.

<a id="d15b7200ae23d3ae"></a>
### 설명

예를 들어, 테이블 t1 에 대해 다음과 같은 순서로 AFTER STATEMENT trigger 들이 생성된 경우,

- 생성 순서: trg1, trg2, trg3, trg4, trg5
- 실행 순서: trg1, trg2, trg3, trg4, trg5

ALTER TABLE t1 SET TRIGGER ORDER 구문을 사용하면 trigger 들의 실행 순서를 다음과 같이 변경할 수 있다.

- ALTER TABLE t1 SET TRIGGER ORDER trg3
    - Trigger를 하나만 기술한 경우
    - 실행 순서 : trg3, trg1, trg2, trg4, trg5
- ALTER TABLE t1 SET TRIGGER ORDER trg1, trg3, trg5
    - Trigger 중 일부만 기술한 경우
    - 실행 순서 : trg1, trg3, trg5, trg2, trg4
- ALTER TABLE t1 SET TRIGGER ORDER trg5, trg4, trg3, trg2, trg1
    - 모든 trigger를 기술한 경우
    - 실행 순서 : trg5, trg4, trg3, trg2, trg1

<a id="5227d33bfc77f5a6"></a>
### 사용 예

현재 테이블에 생성된 trigger 의 실행 순서가 다음과 같을 때

```
gSQL>
SELECT action_timing
     , action_orientation
     , action_order
     , trigger_name
  FROM information_schema.triggers
 WHERE event_object_table = 'T1'
 ORDER BY action_order;

ACTION_TIMING ACTION_ORIENTATION ACTION_ORDER TRIGGER_NAME
------------- ------------------ ------------ ------------
AFTER         STATEMENT                     1 TRG1        
AFTER         STATEMENT                     2 TRG2        
AFTER         STATEMENT                     3 TRG3        
AFTER         STATEMENT                     4 TRG4        
AFTER         STATEMENT                     5 TRG5        

5 rows selected.
```

&lt;alter table set trigger order statement&gt; 구문을 실행하면 trigger 의 실행 순서가 다음과 같이 변경된다.

```
gSQL> ALTER TABLE t1 SET TRIGGER ORDER trg5, trg4, trg3, trg2, trg1;

Table Altered

gSQL>
SELECT action_timing
     , action_orientation
     , trigger_name
     , action_order
  FROM information_schema.triggers
 WHERE event_object_table = 'T1'
 ORDER BY action_order;

ACTION_TIMING ACTION_ORIENTATION ACTION_ORDER TRIGGER_NAME
------------- ------------------ ------------ ------------
AFTER         STATEMENT                     1 TRG5        
AFTER         STATEMENT                     2 TRG4        
AFTER         STATEMENT                     3 TRG3        
AFTER         STATEMENT                     4 TRG2        
AFTER         STATEMENT                     5 TRG1        

5 rows selected.
```

<a id="d068cb8a67a975e1"></a>
### 호환성

SQL 표준에는 trigger 들의 실행 순서를 변경하는 구문이 존재하지 않는다.

<a id="2389dc92f034f678"></a>
## ALTER TABLE name SET UNUSED COLUMN

<a id="283d392aca724d46"></a>
### 기능

테이블 column을 제거한다.

<a id="2b669d1029c6376f"></a>
### 구문

```
<drop column definition> ::=
    ALTER TABLE table_name <drop column clause>
    ;

<drop column clause> ::=
      SET UNUSED [ COLUMN ] <column_name_list> [ <drop behavior> ]

<column name list> ::=
      column_name
    | ( column_name [, ...] )

<drop behavior> ::=
      RESTRICT
    | CASCADE
    | CASCADE CONSTRAINTS
```

<a id="501174ae3161bd65"></a>
### 사용 범위 및 접근 권한

&lt;drop column definition&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="815df6d2b3c80a01"></a>
### 구문 규칙 및 파라미터

<a id="06dcebc10b8d4087"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="5a647aa6d79ba494"></a>
#### SET UNUSED [ COLUMN ]

해당 column들을 사용하지 않도록 설정한다.

<a id="27346bc206a6fb44"></a>
#### column_name_list

한 개 이상의 삭제될 column 이름이다.

- 예: ALTER TABLE t1 SET UNUSED COLUMN c1 
- 예: ALTER TABLE t1 SET UNUSED COLUMN (c1, c2)

<a id="211860a86871d75e"></a>
#### column_name

삭제할 column의 이름이다.

해당 column 을 포함하는 인덱스도 함께 삭제한다.

```
CREATE INDEX idx1 ON t1(c1, c2);

--# idx1 인덱스도 함께 삭제
ALTER TABLE t1 SET UNUSED COLUMN (c1);
```

해당 column 들로 구성된 제약 조건도 함께 삭제한다.

```
CREATE TABLE t1 ( c1 INTEGER PRIMARY KEY
                , c2 INTEGER );

--# primary key 도 함께 삭제
ALTER TABLE t1 SET UNUSED COLUMN (c1);
```

해당 column 을 명시한 trigger 도 함께 삭제한다.

```
CREATE TRIGGER trigger1
    AFTER UPDATE OF c1 ON t1
BEGIN
    NULL;
END;
/

--# update of trigger 도 함께 삭제
ALTER TABLE t1 SET UNUSED COLUMN (c1);
```

<a id="f4e6c298f804ff6b"></a>
#### drop behavior

생략할 경우, 기본값은 RESTRICT 이다.

CASCADE 와 CASCADE CONSTRAINTS 는 동일한 의미이다.

제거 대상 column과 다른 column을 함께 포함하는 제약 조건이 존재할 경우, CASCADE CONSTRAINTS 를 명시해야 한다.

```
CREATE TABLE t1 ( c1 INTEGER
                , c2 INTEGER
                , UNIQUE(c1, c2) );

--# error
ALTER TABLE t1 SET UNUSED COLUMN c1;

--# success
ALTER TABLE t1 SET UNUSED COLUMN c1 CASCADE CONSTRAINTS;
```

Column을 제거할 때 함께 제거되는 제약 조건을 참조하는 FOREIGN KEY 가 존재할 경우, CASCADE CONSTRAINTS 를 명시해야 한다.

```
CREATE TABLE parent ( pk INTEGER PRIMARY KEY
                    , c1 INTEGER );

CREATE TABLE child ( fk INTEGER REFERENCES parent(pk) 
                   , c2 INTEGER );

--# error
ALTER TABLE parent SET UNUSED COLUMN ( pk );

--# success
ALTER TABLE parent SET UNUSED COLUMN ( pk ) CASCADE CONSTRAINTS;
```

<a id="ecf8043da25cf3ca"></a>
### 설명

SET UNUSED COLUMN은 data를 물리적으로 제거하지 않으므로 row의 개수에 관계없이 일정한 성능을 보장한다.

<a id="039d74ee3ba629df"></a>
### 사용 예

다음은 해당 column을 사용하지 않도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 SET UNUSED COLUMN ( addr );

Table altered.
```

<a id="b1ac7dc1b8176637"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- SET UNUSED 
- CASCADE CONSTRAINTS 
- 다수의 column 나열

**SQL 표준 호환성**

<a id="6f3f9ea876109c81"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F033 | ALTER TABLE statement: DROP COLUMN clause | X |

<a id="0c3f7162d363afa0"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#1085f15b7d6e9700)
- [ALTER TABLE name ADD COLUMN](#5bf457087cd2404f)
- [ALTER TABLE name ALTER COLUMN](#0892c59a03976f71)
- [ALTER TABLE name RENAME COLUMN](#61e1f15efa661ac2)

<a id="e5ce6718ce23e4e6"></a>
## ALTER TABLE name SPLIT SHARD

<a id="23ca2f6026b4147d"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard를 split하여 재배치한다.

<a id="f147cca94c8c101b"></a>
### 구문

```
<alter table split shard statement> ::=
    ALTER TABLE table_name SPLIT SHARD source_shard_name
        INTO ( <split shard placement> [, ...] )
    ;

<split shard placement> ::=
    <split shard bound def> AT CLUSTER GROUP dest_group_name

<split shard bound def> ::=
    <split list shard def>
  | <split range shard def>

<split list shard def> :=
    SHARD dest_shard_name VALUES IN ( <split list value clause> )

<split list value clause> :=
    <split list value> [, ...]

<split list value> :=
    constant
  | NULL

<split range shard def> :=
    SHARD dest_shard_name VALUES LESS THAN ( <split range value clause> )

<split range value clause> :=
    <split range value> [, ...]

<split range value> :=
    constant
```

<a id="07420b69024ae173"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table split shard statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="a7b718b170c4b2fa"></a>
### 구문 규칙 및 파라미터

<a id="838289c85b568853"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
해당 테이블이 cluster group specific이고 list shard 또는 range shard인 경우에만 구문을 수행할 수 있다.

<a id="4b453437294152ac"></a>
#### source_shard_name

Split할 원본 shard 이름이다.   
해당 테이블에 shard가 존재하지 않을 경우 구문을 수행할 수 없다.

<a id="63f840ac75c78995"></a>
#### &lt;split shard placement&gt;

원본 shard를 split하여 재배치할 대상 shard를 정의한다.

<a id="5075f5bb41384c7c"></a>
#### &lt;split shard bound def&gt;

Split 될 대상 shard의 bound를 정의한다.

다음 두 가지 bound def 중 하나로 정의할 수 있다.

- &lt;split list shard def&gt;
- &lt;split range shard def&gt;

<a id="48995ef91c5b0d31"></a>
##### &lt;split list shard def&gt;

list shard를 위한 split shard bound를 정의한다.

- dest_shard_name
    - 대상 shard 이름이다.

- &lt;split list value clause&gt;
    - &lt;split list value&gt;는 상수값이어야 한다.
    - &lt;split list value&gt;는 NULL 값을 사용할 수 없다.
    - &lt;split list value&gt;는 DEFAULT를 사용할 수 없다.
    - S1 : ( 1, 11, 21, 31, NULL ) SPLIT SHARD S1 INTO ( &lt;split list value clause&gt; .. )
        - (O) SHARD S11 VALUES IN ( 1 )
        - (O) SHARD S11 VALUES IN ( 1, NULL ) 
        - (O) SHARD S11 VALUES IN ( 1, 11, 21, 31 ) 
        - (X) SHARD S11 VALUES IN ( 2 ) 
        - (X) SHARD S11 VALUES IN ( DEFAULT ) 
        - (X) SHARD S11 VALUES IN ( 1, 11, 21, 31, NULL )

<a id="f80ae5cfded55cb4"></a>
##### &lt;split range shard def&gt;

Range shard를 위한 split shard bound를 정의한다.

- &lt;split range value clause&gt;
    - &lt;split list value&gt;는 상수값이어야 한다.
    - &lt;split list value&gt;는 NULL 값을 사용할 수 없다.
    - &lt;split list value&gt;는 MAXVALUE를 사용할 수 없다.
    - S1 : ( 100, 100 ), S2 : ( 50, 50 ) SPLIT SHARD S1 INTO ( &lt;split range value clause&gt; .. )
        - (O) SHARD S11 VALUES IN ( 50, 100 )
        - (O) SHARD S11 VALUES IN ( 100, 50 )
        - (O) SHARD S11 VALUES IN ( 60, 60 )
        - (X) SHARD S11 VALUES IN ( 50, NULL )
        - (X) SHARD S11 VALUES IN ( 50, 50 )
        - (X) SHARD S11 VALUES IN ( 100, 100 )
        - (X) SHARD S11 VALUES IN ( 100, 110 )
        - (X) SHARD S11 VALUES IN ( MAXVALUE, 100 )

<a id="26e43f770fad458e"></a>
#### dest_group_name

Split 된 shard가 배치될 cluster group의 이름이다.

<a id="e534f5f4996d258a"></a>
### 설명

특정 테이블의 특정 shard를 분산하여 임의의 cluster group에 배치한다.  
특정 shard에 해당하는 레코드가 많거나 특정 group member에 부하가 편중될 때 shard를 분산하여 레코드와 부하를 분산하기 위해 사용된다.

<a id="e9696f57b6569944"></a>
### 사용 예

다음은 &lt;alter table split shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES IN ( 11 ) AT CLUSTER GROUP G2 );

Table altered.

gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES LESS THAN ( 11 ) AT CLUSTER GROUP G2 );


Table altered.
```

<a id="1b560c2178a101d2"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="b08237acba30b6ea"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name REBALANCE](#4dcbc8cc43487ef2)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#5f2f7d4e4bdedbe5) 
- [ALTER TABLE name MOVE SHARD](#b64b6ca52ad7b811)
- [ALTER TABLE name MERGE SHARDS](#c5810c8b8fddc31e)

<a id="e0bd18124d55324a"></a>
## ALTER TABLE name STORAGE

<a id="7905504f245765e6"></a>
### 기능

테이블의 물리적 속성을 변경한다.

<a id="3fd667d8ed7275b0"></a>
### 구문

```
<alter table physical attribute statement> ::=
    ALTER TABLE table_name 
      [ <physical attribute clause> ]
    | [ STORAGE ( <segment attr clause> [...] ) ]
    ;

<physical attribute clause> ::=
      PCTFREE integer
    | PCTUSED integer
    | INITRANS integer
    | MAXTRANS integer

<segment attr clause> ::=
    NEXT <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]
```

<a id="7bb6e2f373aadda0"></a>
### 사용 범위 및 접근 권한

&lt;alter table physical attribute statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="ce0d053bc280f23c"></a>
### 구문 규칙 및 파라미터

<a id="c2b330ee9a4ea431"></a>
#### table_name

변경할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="f989839502906230"></a>
#### &lt;physical attribute clause&gt;

테이블을 구성하는 page의 물리적 속성을 변경한다.  
이미 할당된 page에는 적용되지 않으며 새로 할당받는 page에 적용된다.  
자세한 설명은 [CREATE TABLE](19-sql-references-c-g.md#ce6ecbcf1ea593ea) 구문의 [&lt;table physical attribute clause&gt;](19-sql-references-c-g.md#7cd1675c4bbc6095) 절을 참조한다.

<a id="610d126019e27ac5"></a>
#### &lt;segment attr clause&gt;

세그먼트를 구성하는 extent의 물리적 속성을 변경한다.   
이미 할당된 extent에는 적용되지 않으며, 새로 할당받는 extent에 적용된다.

- MAXSIZE integer 
    - 할당될 수 있는 세그먼트 공간의 크기를 변경한다. 
    - 이미 할당되어 있는 공간보다 작은 크기를 지정하면 에러가 발생한다.

<a id="6dc44fb639825161"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="0fa1c98479791a56"></a>
### 사용 예

다음은 테이블의 물리적 속성을 변경하는 예이다.

```
gSQL> ALTER TABLE t1 PCTFREE 10 PCTUSED 40 STORAGE ( NEXT 10M  MAXSIZE  100M );

Table altered.
```

<a id="13d8c2fc10a4120b"></a>
### 호환성

SQL 표준에서는 테이블의 물리적 속성에 대하여 정의하지 않고 있다.

<a id="40f74ffed6c0676b"></a>
### 참조

관련 내용은 [ALTER TABLE](#1085f15b7d6e9700)을 참조한다.

<a id="baf7d0e8598b3f6a"></a>
## ALTER TABLE name SYNCHRONIZE

<a id="db20ab2425bf3fc1"></a>
### 기능

기존에 배치되어 있는 테이블의 shard들을 원격으로 동기화한다.

<a id="4302ef45553d2ebf"></a>
### 구문

```
<alter table synchronize statement> ::=
    ALTER TABLE table_name SYNCHRONIZE 
       [ ONLINE | OFFLINE ] 
       [ LOGGING | NOLOGGING ]
       [ <scan partition> ] 
       [ <parallel clause> ]
    ;

<scan partition> ::= 
    SCAN PARTITION integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="bb674d661d431f65"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table synchronize statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="1efb686cc7fc83e7"></a>
### 구문 규칙 및 파라미터

<a id="0fba457bb277f3aa"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="814f801a7065270a"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 동기화할 때 DML을 허용할지 여부를 결정한다

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="e316596023049982"></a>
#### [ LOGGING | NOLOGGING ]

테이블을 동기화하는 동안 기록되는 로그의 양을 지정한다.

- LOGGING
    - 테이블 동기화 과정에서 모든 로그를 기록한다.
- NOLOGGING
    - 테이블 동기화 과정에서 최소한의 로그만 기록한다.
- 생략할 경우, 기본값은 LOGGING 이다.

> NOLOGGING 옵션을 사용하면 redo log가 기록되지 않는다. 따라서 synchronize 수행 후 서버가 비정상적으로 종료되면 해당 테이블은 unusable 상태가 된다. 이를 방지하려면 synchronize 후에 CHECKPOINT 구문을 수행해야 한다.

<a id="58f0a9340f48b9e7"></a>
#### &lt;scan partition&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버와 동기화 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, ONLINE_DDL_SCAN_PARTITION 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="a799ff1bbc6c36e4"></a>
#### &lt;parallel clause&gt;

테이블을 동기화할 때 사용할 thread 개수를 지정한다.

- NOPARALLEL
    - 테이블을 병렬로 동기화하지 않는다.
- PARALLEL [integer] 
    - 테이블을 병렬로 동기화한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="777ba4d17d1af6f0"></a>
### 설명

테이블 동기화는 기존에 배치되어 있는 오프라인 된 shard들을 동기화하여 정합성을 복구한다. [&lt;alter table rebalance statement&gt;](#4dcbc8cc43487ef2)와는 달리 inactive cluster member가 있어도 수행할 수 있다.

다음 조건들을 만족하지 못하면 실패한다.

- Cloned 테이블의 shard들을 동기화 하려면 클러스터 시스템 내에서 적어도 하나의 멤버에 cloned 테이블의 온라인 replica가 존재해야 한다.
- Sharded 테이블의 shard들을 동기화 하려면 그룹 당 적어도 하나의 멤버에 해당 sharded 테이블의 온라인 replica가 존재해야 한다.

예를 들어 sharded 테이블 t1의 cluster group G3에 있는 모든 replica들이 오프라인 상태일 경우 다음과 같은 에러가 발생한다.

```
gSQL> ALTER TABLE t1 SYNCHRONIZE;

ERR-42000(16546): sharded table "PUBLIC"."T1" must have at least one online replica of group 'G3'
```

모든 테이블들의 shard를 동기화하려면 [&lt;alter database synchronize statement&gt;](#1620340d3358eb5b)를 수행한다.

<a id="66417fecd08bc4e2"></a>
### 사용 예

다음은 테이블 t1에 대해서 &lt;alter table synchronize statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 SYNCHRONIZE;

Table altered.
```

<a id="39813f4777f337d3"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="422e23229dcb126f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#1085f15b7d6e9700)
- [ALTER TABLE name REBALANCE](#4dcbc8cc43487ef2)
- [ALTER DATABASE SYNCHRONIZE](#1620340d3358eb5b)

<a id="903acda421fae3cd"></a>
## ALTER TABLE name USABLE

<a id="6f9f3ed6e5ab8d25"></a>
### 기능

unusable 상태의 테이블을 usable 상태로 변경한다.

<a id="b58d79804eda7fd6"></a>
### 구문

```
<alter table usable statement> ::=
    ALTER TABLE table_name USABLE 
    ;
```

<a id="6b6726108f92eda8"></a>
### 사용 범위 및 접근 권한

Cluster system 또는 standalone system 에서 수행할 수 있다.

&lt;alter table usable statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="1beb00b4864bb163"></a>
### 구문 규칙 및 파라미터

<a id="f8439636d3dbb7e8"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="a8616b9cfdb27316"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다. 

<a id="211ef1c0281a70fa"></a>
### 설명

unusable 상태의 테이블을 usable 상태로 변경한다.  
이미 usable 상태인 경우에도 정상적으로 성공한 것으로 판단한다.  
usable 상태로 변경할 때 테이블과 연관된 인덱스들을 모두 rebuild 한다.  
단, offline 상태의 tablespace 에 저장된 인덱스는 rebuild 하지 않는다.

unusable 상태의 테이블은 다음과 같은 경우에 생성될 수 있다.

- nologging 으로 append insert 실행 후, checkpoint 없이 shutdown abort 를 실행한 경우
- nologging 으로 append insert 실행 후, 이전에 백업한 데이터 파일을 이용하여 복구한 경우
- [ALTER DATABASE REGISTER](#a996ea8c8491c041) 구문으로 테이블을 IRRECOVERABLE SEGMENT로 등록한 후 데이터베이스를 startup 한 경우

&lt;alter table usable statement&gt; 는 inactive cluster member가 있는 경우에도 수행할 수 있다.  
다만, 테이블에 저장된 페이지 중에 논리적으로 손상된 페이지가 있으면 구문은 실패하며, 다음과 같은 오류가 발생한다.

```
gSQL> ALTER TABLE t1 USABLE;

ERR-42000(16677): unable to set table to 'usable' state due to remaining corrupted pages.
```

<a id="6506da583c911a6e"></a>
### 사용 예

다음은 &lt;alter table usable statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 USABLE;

Table altered.
```

<a id="c6646178c42c311b"></a>
### 호환성

SQL 표준에서는 usable 세그먼트에 대한 개념을 정의하지 않고 있다.

<a id="7d3341dc7c3f738f"></a>
## ALTER TABLESPACE

<a id="3bd9e2dc84905992"></a>
### 기능

테이블스페이스의 정의를 변경한다.

<a id="bd5d9b6ec4351b22"></a>
### 구문

```
<alter tablespace statement> ::=
      <rename tablespace statement>
    | <backup tablespace statement>
    | <on/offline tablespace statement>
    | <add file statement>
    | <drop file statement>
    | <rename datafile statement>
    ;
```

<a id="85644740169d294e"></a>
### 사용 범위 및 접근 권한

&lt;alter tablespace statement&gt; 구문을 수행하려면 사용자에게 database에 대한 ALTER TABLESPACE 권한이 있어야 한다.

<a id="50b1af3ef7959525"></a>
### 구문 규칙 및 파라미터

<a id="23076639bad7c799"></a>
#### &lt;rename tablespace statement&gt;

테이블스페이스의 이름을 변경한다.  
자세한 내용은 [ALTER TABLESPACE name RENAME TO](#79748f2c18df2386) 구문을 참조한다.

<a id="4f277b780451fc8a"></a>
#### &lt;backup tablespace statement&gt;

테이블스페이스를 백업한다.  
자세한 내용은 [ALTER TABLESPACE name BACKUP](#7b6fbab7bad894d2) 구문을 참조한다.

<a id="65b3d6b1e1d2703f"></a>
#### &lt;on-offline tablespace statement&gt;

테이블스페이스의 모든 파일을 online 또는 offline으로 변경한다.  
자세한 내용은 [ALTER TABLESPACE name [ONLINE|OFFLINE]](#b9a7e09545483657) 구문을 참조한다.

<a id="a219ad3f198cfff6"></a>
#### &lt;add file statement&gt;

테이블스페이스에 파일을 추가한다.  
자세한 내용은 [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#0ed6c4c98eaca683) 구문을 참조한다.

<a id="f6fa14c39aaec875"></a>
#### &lt;drop file statement&gt;

테이블스페이스의 파일을 제거한다.  
자세한 내용은 [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#c60287410089cc6b) 구문을 참조한다.

<a id="ae5eb46425c24bed"></a>
#### &lt;rename datafile statement&gt;

데이터 테이블스페이스의 데이터 파일 이름을 변경한다.  
자세한 내용은 [ALTER TABLESPACE name RENAME DATAFILE](#53130577648dcf50) 구문을 참조한다.

<a id="1983473a158d038d"></a>
### 설명

ALTER TABLESPACE 구문은 다른 Data Definition Language (DDL)과 달리 ROLLBACK 할 수 없고 구문을 수행한 transaction이 자동으로 COMMIT 된다.

<a id="7cb4da7a76d7c577"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="9141eeb32d6b8afc"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="7b3227db8ff6256a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLESPACE](19-sql-references-c-g.md#6b51bf8a71edc61b)
- [DROP TABLESPACE](19-sql-references-c-g.md#6f8b24f831f2bd7f)

<a id="0ed6c4c98eaca683"></a>
## ALTER TABLESPACE name ADD [DATAFILE|MEMORY]

<a id="faa767d07ef744c9"></a>
### 기능

테이블스페이스의 공간을 확장한다.

<a id="93ba3b9d9b399381"></a>
### 구문

```
<add space statement> ::=
    ALTER TABLESPACE tablespace_name ADD <space specification>
        [AT <domain name>]
    ;

<space specification> ::=
      MEMORY <memory clause> [, ...]
    | DATAFILE <add datafile clause> [, ...]

<size clause> ::=
    integer [ K | M | G | T ]

<memory clause> 
     'memory_name' { SIZE <size clause> }

<add datafile clause> ::=
     'filename' 
        { SIZE <size clause> | REUSE | SIZE <size clause> REUSE }
        [ <autoextend clause> ]

<autoextend clause>
    AUTOEXTEND { ON [ <next size clause> ] [ <max size clause> ] | OFF }

<next size clause>
    NEXT <size clause>

<max size clause>
    MAXSIZE { <size clause> | UNLIMITED }
```

<a id="8e11fdcbc362d246"></a>
### 사용 범위 및 접근 권한

&lt;add space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="7d260c45c5b1eaaf"></a>
### 구문 규칙 및 파라미터

<a id="9dfcb8cda37d7d68"></a>
#### &lt;add space statement&gt;

테이블스페이스에 공간을 추가한다.

- OFFLINE 테이블스페이스에는 공간을 추가할 수 없다.

<a id="2a8094f158ef86a9"></a>
#### tablespace_name

공간을 추가할 테이블스페이스의 이름이다.

<a id="e5c97d0e92291953"></a>
#### &lt;file specification&gt;

테이블스페이스의 유형에 따라 다음과 같은 구문을 사용해야 한다.

- 메모리 데이터 테이블스페이스 
    - DATAFILE &lt;add datafile clause&gt; 
- 메모리 임시 테이블스페이스 
    - MEMORY &lt;memory clause&gt;

<a id="be8abd18e9efda59"></a>
#### &lt;add datafile clause&gt;

추가할 메모리 데이터 파일을 정의한다.

- 'filename' 
    - 데이터를 저장 관리할 파일의 이름이다. 
    - 메모리 데이터에 대한 체크포인트 이미지를 저장할 공간이다. 
    - filename은 새로운 파일이거나 이미 존재하는 파일일 수 있다. 
    - filename의 길이는 1024 바이트보다 작아야 한다.

- SIZE &lt;size clause&gt; 
    - 새로운 파일일 경우 SIZE 절을 이용해 초기 크기를 지정한다. 
    - 파일이 이미 존재할 경우 에러가 발생한다. 
    - 파일의 크기는 최소 1 M ~ 최대 30 G 까지 지정할 수 있다.

- REUSE 
    - 이미 존재하는 파일일 경우 REUSE 절을 이용한다. 
    - 파일이 존재하지 않을 경우 새로운 파일을 생성한다. 
    - 새로 생성되는 파일의 사이즈는 
        - 데이터 테이블스페이스의 경우 MEMORY_DATA_TABLESPACE_SIZE 프로퍼티에 의해 결정되고 
        - 임시 테이블스페이스의 경우 MEMORY_TEMP_TABLESPACE_SIZE 프로퍼티에 의해 결정된다.

- SIZE &lt;size clause&gt; REUSE 
    - SIZE 절과 REUSE 절을 모두 명시할 경우 filename의 존재 여부에 따라 다음과 같이 작동한다. 
        - 새로운 filename일 경우 SIZE 절을 이용해 초기 파일 크기를 지정한다. 
        - 이미 존재하는 filename일 경우 기존 파일을 이용하여 SIZE 절의 값으로 크기를 조정한다.

<a id="7859dc6683799445"></a>
#### &lt;memory clause&gt;

- &lt;size clause&gt;
    - 추가할 메모리를 정의한다.

자세한 내용은 [CREATE MEMORY TEMPORARY TABLESPACE](19-sql-references-c-g.md#702566e5b0c8aa29) 구문의 [&lt;memory clause&gt;](19-sql-references-c-g.md#a18dcfe739652b0d)를 참조한다.

<a id="9c7e9992b343be0b"></a>
#### &lt;autoextend clause&gt;

디스크 테이블스페이스의 데이터 파일이 추가될 때 자동 확장 속성을 설정한다. 자동 확장 속성을 ON 또는 OFF로 설정한다. ON으로 설정하면 자동 확장 크기와 데이터 파일의 최대 크기를 지정할 수 있다.

<a id="b3c6ec75fa9c9e6f"></a>
#### &lt;next size clause&gt;

현재 사용 중인 데이터 파일에 더 이상 사용할 공간이 없을 때 확장할 크기를 지정한다.

<a id="9e942a83e0163a77"></a>
#### &lt;max size clause&gt;

데이터 파일이 확장될 수 있는 최대 크기를 지정한다.

<a id="ed2c1d29ad027d71"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="cc8ddd86c3da4aa7"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="f03863ed81785b72"></a>
### 사용 예

다음은 테이블스페이스에 data file을 추가하는 예이다.

```
gSQL> ALTER TABLESPACE space1 ADD DATAFILE 'test_file_a2.dbf' SIZE 10M REUSE;

Tablespace altered.
```

<a id="bfdb889c39b6bcbc"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="0c22e717207aef70"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE MEMORY DATA TABLESPACE](19-sql-references-c-g.md#89b908fb6ee8dd25)
- [CREATE MEMORY TEMPORARY TABLESPACE](19-sql-references-c-g.md#702566e5b0c8aa29)
- [ALTER TABLESPACE](#7d3341dc7c3f738f)

<a id="7b6fbab7bad894d2"></a>
## ALTER TABLESPACE name BACKUP

<a id="4c8fc5692f4678cd"></a>
### 기능

테이블스페이스를 backup 하기 위해 backup이 가능한 상태와 불가능한 상태로 전환한다.

<a id="22a91e59097bb0c2"></a>
### 구문

```
<backup tablespace statement> ::=
      <tablespace begin backup statement>
    | <tablespace end backup statement>
    | <tablespace incremental backup statement>    
    ;

<tablespace begin backup statement> ::=
    ALTER TABLESPACE tablespace_name BEGIN BACKUP [AT <domain_name>];

<tablespace end backup statement> ::=
    ALTER TABLESPACE tablespace_name END BACKUP [AT <domain_name>];

<tablesapce incremental backup statement> ::=
    ALTER TABLESPACE tablespace_name 
        BACKUP INCREMENTAL <incremental backup option> 
           [ FORMAT 'format string' ] [ PIECE integer ] 
           [ <parallel clause> ] [AT <domain_name>];

<incremental backup option> ::=
      LEVEL integer [ CUMULATIVE | DIFFERENTIAL ]

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="c4938a51ae869616"></a>
### 사용 범위 및 접근 권한

&lt;backup space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="d0a67c833ddb0ea6"></a>
### 구문 규칙 및 파라미터

<a id="3e3fcc5ba9b86aef"></a>
#### &lt;tablespace begin backup statement&gt;

테이블스페이스를 백업 가능한 상태로 설정한다.

- 생성되어 사용 중인 테이블스페이스를 백업 가능한 상태로 설정한다.
- OFFLINE/ temporary 테이블스페이스는 backup 상태는 전환할 수 없다.

<a id="e9d542dde8318047"></a>
#### tablespace_name

Backup 상태를 전환할 테이블스페이스의 이름이다.

<a id="0db381bfe7541261"></a>
#### &lt;tablespace end backup statement&gt;

테이블스페이스를 백업이 불가능한 상태로 설정한다.

<a id="470ecd3809792f94"></a>
#### &lt;tablesapce incremental backup statement&gt;

테이블스페이스의 증분 백업을 수행한다.  
데이터베이스가 OPEN 상태이고, ARCHIVELOG로 운영되어야 한다.

<a id="634dac65148fccfc"></a>
#### &lt;incremental backup option&gt;

- 'integer'는 0 ~ 4 까지 지정할 수 있다.
- 'LEVEL 0'는 CUMULATIVE나 DIFFERENTIAL을 지정할 수 없다.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - 'integer'가 n이면 가장 최근에 'LEVEL 0' ~ 'LEVEL n-1'까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - DIFFERENTIAL
        - 'integer'가 n이면 가장 최근에 'LEVEL 0' ~ 'LEVEL n'까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - 생략되면 DIFFERENTIAL이 기본으로 지정된다.

<a id="2720ad51362b3aa8"></a>
#### FORMAT 'format string'

- backup 파일 이름의 형식을 지정한다.
- 'format string' 내에 format specifier 를 사용할 수 있다. 
- FORMAT 을 지정하지 않은 경우는 'tablespace_D%T_T%t_L%l_Q%q_P%p.inc' 를 format string 으로 사용한다.
- format specifier
    - %d : 데이터베이스 시그니쳐
    - %q : 백업 순차 번호
    - %l : 백업 레벨
    - %t : 시간(HHMMSS)
    - %m : 클러스터 멤버 이름
    - %g : 클러스터 그룹 이름
    - %D : 요일(DD)
    - %M : 월(MM)
    - %N : 테이블스페이스 이름
    - %p : 백업 파일의 조각(Piece) 번호
    - %T : 날짜(YYYYMMDD)
    - %Y : 년(YYYY)
    - %% : Percent(%) 문자

<a id="353dc1ff2de503b9"></a>
#### PIECE integer

- 분할될 백업 파일의 개수를 지정한다.
- 'format string' 에 %p 가 포함되어 있지 않으면 지정된 integer 값은 무시하고 1 값을 갖는다.

<a id="fe1d6e58a0da9c1a"></a>
#### &lt;parallel clause&gt;

백업시 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 병렬로 백업을 수행하지 않는다.
- PARALLEL [integer] 
    - 병렬로 백업을 수행한다. 
    - integer는 1부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 1이다. 
- 명시하지 않을 경우, 기본값은 NOPARALLEL이다.
- 대상 datafile 의 총 개수가 integer 보다 작은 경우는 datafile 개수만큼 병렬로 수행한다. 
- PIECE 의 개수가 병렬 개수보다 작은 경우는 PIECE 개수 만큼 병렬로 처리한다.

<a id="8952b15d3ee415df"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="58cef53220f64595"></a>
### 설명

테이블스페이스에 생성된 datafile을 백업한다. 테이블스페이스 전체를 백업하려면 BEGIN BACKUP을 수행한 후 OS의 파일 복사 기능을 사용하여 datafile들을 복사하고 나서 END BACKUP을 수행한다. 한편, 증분 백업 파일은 하나의 구문으로 BACKUP_DIR_1 property에 설정된 경로에 생성한다.

<a id="71f6da05405c020e"></a>
### 사용 예

다음은 DICTIONARY_TBS 테이블스페이스의 전체 백업 상태를 'ACTIVE'로 설정하는 예이다.

```
ALTER TABLESPACE DICTIONARY_TBS BEGIN BACKUP;
```

다음은 DICTIONARY_TBS 테이블스페이스의 전체 백업 상태를 'INACTIVE'로 설정하는 예이다.

```
ALTER TABLESPACE DICTIONARY_TBS END BACKUP;
```

다음은 DICTIONARY_TBS 테이블스페이스의 LEVEL 0 증분 백업을 만드는 예이다.

```
ALTER TABLESPACE DICTIONARY_TBS BACKUP INCREMENTAL LEVEL 0;
```

다음은 네 개의 thread로 backup을 수행하는 예로써 테이블스페이스 이름과 날짜와 조각 번호로 구성된 네 개의 backup 파일이 만들어진다.

```
ALTER TABLESPACE DICTIONARY_TBS BACKUP INCREMENTAL LEVEL 0 FORMAT 'backup_%N_%T_%p' PIECE 4 PARALLEL 4;
```

<a id="e07b5909f608549f"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="e163a85478e2b5d3"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#7d3341dc7c3f738f)
- [ALTER TABLESPACE name [ONLINE|OFFLINE]](#b9a7e09545483657)

<a id="c60287410089cc6b"></a>
## ALTER TABLESPACE name DROP [DATAFILE|MEMORY]

<a id="68b0718174b5fc25"></a>
### 기능

테이블스페이스의 공간을 축소한다.

<a id="4bd04c996806cdfe"></a>
### 구문

```
<drop space statement> ::=
    ALTER TABLESPACE tablespace_name DROP <file specification>
    [ AT <domain name> ]
    ;

<file specification> ::=
      DATAFILE 'filename' 
    | MEMORY 'memory_name'
```

<a id="327ac7c1722d00b7"></a>
### 사용 범위 및 접근 권한

&lt;drop space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="a6291888a1d00144"></a>
### 구문 규칙 및 파라미터

<a id="ad4d1eeda61d4034"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="e75c6df911b06933"></a>
#### &lt;file specification&gt;

테이블스페이스의 유형에 따라 다음과 같은 구문을 사용해야 한다.

- 메모리 데이터 테이블스페이스 
    - DATAFILE 'filename' 
- 메모리 임시 테이블스페이스 
    - MEMORY 'memory_name'

> 오프라인 테이블스페이스의 파일은 삭제할 수 없다.   
> 테이블스페이스의 첫 번째 파일은 삭제할 수 없다.  
> 한 번이라도 사용된 적이 있는 데이터 파일은 삭제할 수 없다.

<a id="b323c11b3f75b9ea"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="ff567b5021fd2248"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="32def295a4133914"></a>
### 사용 예

다음은 테이블스페이스의 파일을 제거하는 예이다.

```
gSQL> ALTER TABLESPACE space1 DROP DATAFILE 'test_file_f2.dbf';

Tablespace altered.
```

<a id="f26ae12f9aac6a4b"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="e18dc154d96bf957"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#7d3341dc7c3f738f)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#0ed6c4c98eaca683)
- [ALTER TABLESPACE name RENAME DATAFILE](#53130577648dcf50)

<a id="b9a7e09545483657"></a>
## ALTER TABLESPACE name [ONLINE|OFFLINE]

<a id="e23232146085b841"></a>
### 기능

테이블스페이스 상태를 변경한다.

<a id="564b85cbe09f2fb1"></a>
### 구문

```
<on/off tablespace statement> ::=
    ALTER TABLESPACE tablespace_name { ONLINE | OFFLINE [ NORMAL | IMMEIDATE ] }
    [ AT <domain name> ]
    ;
```

<a id="2c1b154c01ead8a8"></a>
### 사용 범위 및 접근 권한

&lt;on/off tablespace statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="599c25880607d647"></a>
### 구문 규칙 및 파라미터

<a id="e76edbfad2fddb17"></a>
#### ONLINE

OFFLINE 상태의 테이블스페이스를 ONLINE으로 변경한다.

<a id="9935c1a668c002e2"></a>
#### OFFLINE NORMAL

ONLINE 상태의 테이블스페이스를 OFFLINE으로 변경한다.

OFFLINE으로 변경된 테이블스페이스는 일관된 (consistent) 상태이기 때문에 ONLINE 상태로 변경할 때 미디어 복구할 필요없다.

> MOUNT 단계에서는 OFFLINE NORMAL을 사용할 수 없다.

<a id="305cb358127115de"></a>
#### OFFLINE IMMEDIATE

ONLINE 상태의 테이블스페이스를 OFFLINE으로 변경한다.

OFFLINE으로 변경된 테이블스페이스는 비일관적인 (inconsistent) 상태이기 때문에, ONLINE 상태로 변경할 때 미디어 복구해야 한다.

> SYSTEM 테이블스페이스는 OFFLINE으로 변경할 수 없다.   
> OFFLINE IMMEDIATE는 미디어 복구를 필요로 하기 때문에 archive log mode에서만 수행할 수 있다.

<a id="3f23edb7b63913cf"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="62c37b7755293a34"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

> 클러스터 데이터베이스에서 OPEN 단계 이상일 경우, 테이블스페이스를 OFFLINE으로 전환하려면 해당 테이블스페이스에 포함된 모든 테이블이 OFFLINE 상태여야 한다.  
>  따라서, 해당 구문을 수행하기 전에 반드시 [ALTER TABLESPACE name OFFLINE TABLES](#02160699e5a8a735) 명령을 먼저 실행해야 한다.

<a id="140294147c120c3d"></a>
### 사용 예

다음은 테이블스페이스를 OFFLINE으로 설정하는 예이다.

```
gSQL> ALTER TABLESPACE space1 OFFLINE;

Tablespace altered.
```

다음은 MOUNT 단계에서 테이블스페이스에 OFFLINE NORMAL을 수행하여 실패하는 예이다.

```
gSQL> ALTER TABLESPACE space1 OFFLINE;

ERR-42000(16290): OFFLINE NORMAL is only allowed if the database is in OPEN phase : 
ALTER TABLESPACE space1 OFFLINE
                 *
ERROR at line 1:

gSQL> ALTER TABLESPACE space1 OFFLINE NORMAL;

ERR-42000(16290): OFFLINE NORMAL is only allowed if the database is in OPEN phase : 
ALTER TABLESPACE space1 OFFLINE NORMAL
                 *
ERROR at line 1:
```

<a id="617610bfc182491c"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="e72528024b732ab4"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#7d3341dc7c3f738f)
- [ALTER TABLESPACE name BACKUP](#7b6fbab7bad894d2)

<a id="02160699e5a8a735"></a>
## ALTER TABLESPACE name OFFLINE TABLES

<a id="310e3f495c931b5d"></a>
### 기능

테이블스페이스와 관련된 테이블들을 offline 상태로 변경한다.

<a id="a83365f71768ad43"></a>
### 구문

```
<alter tablespace offline tables statement> ::=
    ALTER TABLESPACE tablespace_name OFFLINE TABLES [ <domain name> ]
    ;
```

<a id="fe326328b67dd5c2"></a>
### 사용 범위 및 접근 권한

Cluster system 에서 수행할 수 있다.

&lt;alter tablespace offline tables statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="fa7670441666cc46"></a>
### 구문 규칙 및 파라미터

<a id="18e632f6ff67c55c"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="c04e498b5cc7fb7d"></a>
### 설명

&lt;alter tablespace offline tables statement&gt; 구문은 클러스터 데이터베이스이고 OPEN 단계에서는 [ALTER TABLESPACE tablesapce_name OFFLINE](#b9a7e09545483657)을 실행하기 전에 반드시 수행해야 하는 구문이다.

해당 구문을 먼저 수행하지 않고 TABLESPACE OFFLINE 을 실행하면 다음과 같은 에러가 발생한다.

```
gSQL> ALTER TABLESPACE space1 OFFLINE;

ERR-42000(16632): tables related to tablespace 'SPACE1' must be offline
```

Offline 상태로 변경되는 테이블들은 다음과 같다.

- 테이블스페이스에 저장된 테이블들 
- 테이블스페이스에 저장된 인덱스들이 속한 테이블들

&lt;alter tablespace offline tables statement&gt;는 inactive member가 있어도 수행할 수 있다.

<a id="9d3b58b7db117154"></a>
### 사용 예

다음은 &lt;alter tablespace offline tables statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLESAPCE space1 OFFLINE TABLES;

Tablespace altered.
```

<a id="1ec39889d30742e9"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="f89d360c67ee66ac"></a>
### 참조

관련 내용은 [ALTER TABLESPACE name [ONLINE|OFFLINE]](#b9a7e09545483657)을 참조한다.

<a id="53130577648dcf50"></a>
## ALTER TABLESPACE name RENAME DATAFILE

<a id="f071b9a2cc3db803"></a>
### 기능

테이블스페이스를 구성하는 데이터 파일의 이름을 변경한다.

<a id="0e9732581a971495"></a>
### 구문

```
<rename datafile statement> ::=
    ALTER TABLESPACE tablespace_name RENAME DATAFILE <filename_list> TO <filename_list>
    ;

    <filename_list> ::= 
        'filename' [ AT <domain name> ] [, ...]
```

<a id="bf4cfd0f66a8bac4"></a>
### 사용 범위 및 접근 권한

&lt;rename datafile statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

> TDS 모드이면서 데이터베이스가 OPEN인 상태에서는 온라인 테이블스페이스 파일을 변경할 수 없다. (임시 메모리 테이블스페이스는 제외된다.)   
> 변경한 후에도 파일은 반드시 존재해야 한다.

<a id="19778a7ad6676e7e"></a>
### 구문 규칙 및 파라미터

<a id="563271855cc04bda"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="64f6b45fc52d2e16"></a>
#### 'filename'

메모리 임시 테이블스페이스는 'memory_name'을 의미하며, 그 외의 테이블스페이스 종류는 'filename'을 의미한다.

<a id="891bb5fc5f33ee01"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="81ef98a6f0cd32d7"></a>
### 설명

테이블스페이스 상태에 따라 연산 가능 여부가 결정된다.

- OFFLINE: MOUNT 단계나 OPEN 단계에서 수행 가능하다.
- ONLINE: MOUNT 단계에서만 수행 가능하다.

<a id="dc562f28f5c88f95"></a>
### 사용 예

다음은 'test.dbf'를 'test1.dbf'로 변경하는 예이다.

```
gSQL> ALTER TABLESPACE TEST_TBS RENAME DATAFILE 'test.dbf' TO 'test1.dbf';

Tablespace altered.
```

<a id="32b61e076438fee6"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="99278b26858fa4cc"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#7d3341dc7c3f738f)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#0ed6c4c98eaca683)
- [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#c60287410089cc6b)

<a id="79748f2c18df2386"></a>
## ALTER TABLESPACE name RENAME TO

<a id="91fbcb4819cb1d19"></a>
### 기능

테이블스페이스의 이름을 변경한다.

<a id="92973825fdc85736"></a>
### 구문

```
<rename tablespace statement> ::=
    ALTER TABLESPACE tablespace_name RENAME TO <new_tablespace_name>
    ;
```

<a id="39951b7af2beb851"></a>
### 사용 범위 및 접근 권한

&lt;rename space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="c3e312fd68b49511"></a>
### 구문 규칙 및 파라미터

<a id="39aa3ab3dd0d1b2c"></a>
#### tablespace_name

기존 테이블스페이스의 이름이다.

- Built-in 테이블스페이스의 이름은 변경할 수 없다.
- OFFLINE 테이블스페이스의 이름은 변경할 수 없다.

<a id="b1afa8da54263952"></a>
#### new_tablespace_name

새로운 테이블스페이스의 이름이다.

<a id="047cd3401fdca85c"></a>
### 설명

Tablespace 이름이 변경되더라도 기존에 이미 해당 tablespace에 생성된 table, index 등은 변경할 필요없다.

<a id="b44f1a1b607b0026"></a>
### 사용 예

다음은 테이블스페이스의 이름을 변경하는 예이다.

```
gSQL> ALTER TABLESPACE space1 RENAME TO space2;

Tablespace altered.
```

<a id="1107b42f1e2f327a"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="ef8ba1f3df6656e6"></a>
### 참조

관련 내용은 [ALTER TABLESPACE](#7d3341dc7c3f738f)를 참조한다.

<a id="993785b9050b5d8a"></a>
## ALTER USER

<a id="34323cd3c2fdf0cc"></a>
### 기능

데이터베이스 사용자 정의를 변경한다.

<a id="071587d6de1d523a"></a>
### 구문

```
<alter user statement> ::=
      ALTER USER user_identifier <alter user action>
    | ALTER USER PUBLIC <alter schema path>
    ;

<alter user action> ::=
      <alter password>
    | <alter profile>
    | <password expire>
    | <account lock>
    | <alter default tablespace>
    | <alter temporary tablespace>
    | <alter index tablespace>
    | <alter schema path>

<alter password> ::=
    IDENTIFIED BY new_password [ REPLACE old_password ]

<alter profile> ::=
    PROFILE { profile_name | DEFAULT | NULL }

<password expire> ::=
    PASSWORD EXPIRE

<account lock> ::=
    ACCOUNT { LOCK | UNLOCK }

<alter default tablespace> ::=
    DEFAULT TABLESPACE tablespace_name

<alter temporary tablespace> ::=
    TEMPORARY TABLESPACE tablespace_name

<alter index tablespace> ::=
    INDEX TABLESPACE { tablespace_name | NULL }

<alter schema path> ::=
    SCHEMA PATH ( { schema_name | CURRENT PATH } [, ...] )
```

<a id="5d82600ad256c6ec"></a>
### 사용 범위 및 접근 권한

&lt;alter user statement&gt; 구문을 수행하려면 사용자에게 ALTER USER ON DATABASE 권한이 있어야 한다.  
단, &lt;alter password&gt;는 사용자가 user_identifier와 동일할 경우에 권한 없이 수행할 수 있다.

<a id="6d8de803b30483fe"></a>
### 구문 규칙 및 파라미터

<a id="08ed712e2a21241e"></a>
#### user_identifier

변경할 사용자의 이름이다.

<a id="a3a3ed9f004387d5"></a>
#### &lt;alter password&gt;

사용자의 password를 변경한다.

- IDENTIFIED BY new_password 
    - 새로운 password로 암호화되어 저장된다. 
    - password의 길이는 128 byte보다 작아야 한다. 
    - password는 대소문자를 구별한다.

- REPLACE old_password 
    - ALTER USER ON DATABASE 권한이 있을 경우에는 생략 가능하다. 
    - ALTER USER ON DATABASE 권한이 없을 경우에는 생략할 수 없다. 
        - 사용자와 user_identifier가 동일해야 한다.

<a id="32cde4c83e84bf23"></a>
#### &lt;alter profile&gt;

비밀번호 관리 정책을 위한 profile을 변경한다.

- PROFILE profile_name
    - 사용자가 생성한 profile_name을 할당한다.
- PROFILE DEFAULT
    - 기본 profile인 "DEFAULT"를 할당한다.
- PROFILE NULL
    - Profile을 할당하지 않는다.

<a id="e2a39256ac55faa0"></a>
#### &lt;password expire&gt;

사용자의 비밀번호를 만료시킨다.

<a id="a748c4589bb00ecc"></a>
#### &lt;account lock&gt;

- ACCOUNT LOCK
    - 사용자 계정을 잠근다. 
- ACCOUNT UNLOCK
    - 계정 잠금을 해제한다.

<a id="b1f78de47fb62d07"></a>
#### &lt;alter default tablespace&gt;

사용자의 기본 tablespace를 변경한다.   
tablespace_name은 data tablespace여야 한다.

<a id="9f959969d3c1d57d"></a>
#### &lt;alter temporary tablespace&gt;

사용자의 temporary tablespace를 변경한다.   
tablespace_name은 temporary tablespace여야 한다.

<a id="895e859ea4b95306"></a>
#### &lt;alter index tablespace&gt;

사용자의 index tablespace를 변경한다.

- INDEX TABLESPACE tablespace_name을 지정한다.
    - Data tablespace를 지정한 경우, LOGGING 인덱스가 된다.
    - Temporary tablespace를 지정한 경우, NOLOGGING 인덱스가 된다.
- INDEX TABLESPACE NULL
    - Index tablespace를 지정하지 않는다.

<a id="3eeea41c7cc11e80"></a>
#### &lt;alter schema path&gt;

사용자의 스키마 접근 경로를 변경한다.   
사용자의 SQL 구문에 schema가 명시되지 않았을 경우 스키마 접근 경로는 객체의 naming resolution을 위한 스키마 순서에 따라 결정된다.

스키마 이름이 기존에 스키마 접근 경로에 나열된 스키마 이름과 동일할 경우에는 추가적으로 반영되지 않는다.

다음은 *ALTER USER u1 SCHEMA PATH ( u1, s2, public );* 구문을 수행했을 때 schema에 존재하는 객체의 예이다.

<a id="5e59e441b640c178"></a>
| 스키마 이름 | u1 | s2 | public |
| --- | --- | --- | --- |
| - | t1 | - | t1 |
| - | - | t2 | - |
| - | - | - | t3 |

다음과 같이 u1 사용자가 수행하는 schema가 명시되지 않은 객체의 이름은 SCHEMA PATH에 의해 다음과 같이 해석된다.

- CREATE 구문 
    - CREATE TABLE t1 ( c1 INTEGER ); 
        - 에러 : CREATE TABLE u1.t1 ( c1 INTEGER ); 
    - CREATE TABLE t2 ( c1 INTEGER ); 
        - 수행 : CREATE TABLE u1.t2 ( c1 INTEGER );

- SELECT 구문 
    - SELECT * FROM t1; 
        - 수행 : SELECT * FROM u1.t1; 
    - SELECT * FROM t2; 
        - 수행 : SELECT * FROM s2.t2; 
    - SELECT * FROM t3; 
        - 수행 : SELECT * FROM public.t3;

<a id="1c05f6c34a954c0d"></a>
#### CURRENT PATH

현재 사용자의 schema path 이다.

다음 예와 같이 CURRENT PATH를 이용해 기존의 schema path를 유지하면서 새로운 schema path를 추가할 수 있다.

- u1의 현재 schema path 
    - (u1, public) 
- 구문 수행 
    - ALTER USER u1 SCHEMA PATH ( s1, CURRENT PATH, s2 ); 
- u1의 schema path는 다음과 같이 변경된다. 
    - (s1, u1, public, s2)

<a id="03da169b02077487"></a>
#### ALTER USER PUBLIC &lt;alter schema path&gt;

PUBLIC 계정의 schema path를 변경한다.   
PUBLIC 계정의 schema path는 모든 사용자의 schema path에 포함된다.

PUBLIC 계정에 최초로 부여된 schema path는 다음과 같다.

- DICTIONARY_SCHEMA 
- INFORMATION_SCHEMA 
- DEFINITION_SCHEMA 
- PERFORMANCE_VIEW_SCHEMA 
- FIXED_TABLE_SCHEMA

<a id="41a8e640b523f21a"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="6d04121cd176c7de"></a>
### 사용 예

다음은 사용자의 password를 변경하는 예이다.

```
gSQL> ALTER USER u1 IDENTIFIED BY new_password;

User altered.
```

다음의 사용자에게 profile을 할당하는 예이다.

```
gSQL> ALTER USER u1 PROFILE prof1;

User altered.

gSQL> COMMIT;

Commit complete.
```

다음은 사용자의 profile을 제거하는 예이다.

```
gSQL> ALTER USER u1 PROFILE NULL;

User altered.

gSQL> COMMIT;

Commit complete.
```

다음은 사용자의 비밀번호를 만료시키는 예이다.

```
gSQL> ALTER USER u1 PASSWORD EXPIRE;

User altered.

gSQL> COMMIT;

Commit complete.
```

다음은 사용자의 계정잠금을 해제하는 예이다.

```
gSQL> ALTER USER u1 ACCOUNT UNLOCK;

User altered.

gSQL> COMMIT;

Commit complete.
```

다음은 사용자의 DEFAULT TABLESPACE를 변경하는 예이다.

```
gSQL> ALTER USER u1 DEFAULT TABLESPACE mem_data_tbs;

User altered.
```

다음은 사용자의 TEMPORARY TABLESPACE를 변경하는 예이다.

```
gSQL> ALTER USER u1 TEMPORARY TABLESPACE mem_temp_tbs;

User altered.
```

다음은 사용자의 INDEX TABLESPACE를 변경하는 예이다.

```
gSQL> ALTER USER u1 INDEX TABLESPACE mem_temp_tbs;

User altered.
```

다음은 사용자의 schema path를 변경하는 예이다.

```
gSQL> ALTER USER u1 SCHEMA PATH ( s1, CURRENT PATH );

User altered.
```

<a id="ae99da82aaaed432"></a>
### 호환성

SQL 표준에서 user의 개념은 다루고 있지만 user의 생성, 변경 및 삭제와 관련된 SQL 구문은 정의하지 않고 있다.

<a id="4359df0cc041e8fe"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE USER](19-sql-references-c-g.md#96a76bb7ce13b574)
- [DROP USER](19-sql-references-c-g.md#19e745a811890279)

<a id="3f52c3484a9235a7"></a>
## ALTER VIEW

<a id="11e4bedaebf590a2"></a>
### 기능

View 정의를 변경한다.

<a id="32de0c834a3b4c2b"></a>
### 구문

```
<alter view statement> ::=
    ALTER VIEW view_name <alter view action>
    ;

<alter view action> ::=
    COMPILE
```

<a id="ea51ff00b7120121"></a>
### 사용 범위 및 접근 권한

&lt;alter view statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 view에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- View가 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="f43d7ae6f0485e65"></a>
### 구문 규칙 및 파라미터

<a id="cac11bd5ed4c7639"></a>
#### view_name

변경할 view의 이름이다.  
schema_name.view_name과 같이 view가 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="a749cb8dd77bc535"></a>
#### COMPILE

View를 다시 컴파일한다.   
View column에 부여한 COMMENT는 초기화된다.

<a id="10fb22d1ed2b6a1b"></a>
### 설명

View가 참조하는 테이블이나 view가 변경되거나 삭제되면 해당 view도 영향을 받는다.

이런 정보는 INFORMATION_SCHEMA.VIEWS를 통해 조회할 수 있다.

- IS_COMPILED column
    - TRUE: View가 정상적으로 생성되었다.
    - FALSE: 에러가 존재하는 상태에서 FORCE 옵션으로 view가 생성되었다.

- IS_AFFECTED column
    - TRUE : View가 참조하는 테이블 또는 view가 변경되었다.
    - FALSE: View가 생성되고 COMPILE 된 후에 view가 참조하는 테이블이나 view가 변경되지 않았다.

<a id="ad54a53febce5964"></a>
### 사용 예

다음은 view가 참조하는 table 변경에 영향을 받은 view를 COMPILE 하는 예이다.

```
gSQL> SELECT TABLE_NAME, IS_AFFECTED 
        FROM INFORMATION_SCHEMA.VIEWS 
       WHERE TABLE_SCHEMA = 'PUBLIC'
         AND TABLE_NAME = 'V1';

TABLE_NAME IS_AFFECTED
---------- -----------
V1         TRUE       

1 row selected.


gSQL> ALTER VIEW v1 COMPILE;

View altered.

COMMIT;

Commit complete.

gSQL> SELECT TABLE_NAME, IS_AFFECTED 
        FROM INFORMATION_SCHEMA.VIEWS 
       WHERE TABLE_SCHEMA = 'PUBLIC'
         AND TABLE_NAME = 'V1';

TABLE_NAME IS_AFFECTED
---------- -----------
V1         FALSE      

1 row selected.
```

<a id="6251ce99ba0d30c3"></a>
### 호환성

SQL 표준에서는 &lt;alter view statement&gt; 구문을 정의하지 않고 있다.

<a id="c00306a938dcea11"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE VIEW](19-sql-references-c-g.md#c89fc59cace74235)
- [DROP VIEW](19-sql-references-c-g.md#cad962c71dd7d5e3)

<a id="ceffc94d9a4e4c0a"></a>
## ANALYZE SYSTEM

<a id="4c4f65ece747d626"></a>
### 기능

시스템의 통계 정보를 제어한다.

<a id="37ddd2987a29b3cc"></a>
### 구문

```
<analyze system statement> ::=
    ANALYZE SYSTEM [ <analyze action> ]
    ;

<analyze action> ::=
      COMPUTE STATISTICS
    | DELETE STATISTICS
```

<a id="c037f901b37b5ddd"></a>
### 사용 범위 및 접근 권한

&lt;analyze system statement&gt; 구문을 수행하려면 사용자에게 ANALYZE ANY ON DATABASE 권한이 있어야 한다.

<a id="eabb7b3fe645884f"></a>
### 구문 규칙 및 파라미터

<a id="384ff198d4b299dd"></a>
#### &lt;analyze action&gt;

생략할 경우 기본값은 COMPUTE STATISTICS 이다.

<a id="ff1794ddf2ad4079"></a>
#### COMPUTE STATISTICS

시스템과 관련된 다음과 같은 통계 정보를 구축한다.

- CPU_OPS (Operations Per Second) 
    - CPU가 초당 처리할 수 있는 operation의 개수이다.

- NETWORK_IOPS (IO operations Per Second) 
    - Cluster인 경우에 유효하다. 
    - 초당 처리할 수 있는 network IO 횟수이다.

- BUFFER_MISS_PERCENT
    - 디스크 buffer miss 확률이다.

<a id="453750983c6631be"></a>
#### DELETE STATISTICS

시스템 통계 정보를 삭제한다.

<a id="64126ae1c4e9e249"></a>
### 설명

구축한 시스템 통계 정보는 질의 처리를 위한 최적화 과정의 비용을 계산하기 위해 사용한다.

<a id="b26684b696d7f97a"></a>
### 사용 예

다음은 &lt;analyze system statement&gt; 구문을 사용하여 시스템 통계 정보를 구축하는 예이다.

```
gSQL> ANALYZE SYSTEM COMPUTE STATISTICS;

analyzed.
```

다음은 구축된 시스템 통계 정보를 조회하는 예이다.

```
gSQL> 
SELECT * FROM DBA_STAT_SYSTEM;

 CPU_OPS NETWORK_IOPS NETWORK_BUFSIZE BUFFER_MISS_PERCENT LAST_ANALYZED             
-------- ------------ --------------- ------------------- ---------------------------
53000412         2914           65536                  99  2017-03-30 16:49:42.200000

1 row selected.
```

<a id="e9d2d9bdaf13ebc0"></a>
### 호환성

SQL 표준에서는 통계 정보에 대한 개념을 정의하지 않고 있다.

<a id="b7837866be300e6f"></a>
### 참조

관련 내용은 [ANALYZE TABLE](#2c58b21ce5cb8f13)을 참조한다.

<a id="2c58b21ce5cb8f13"></a>
## ANALYZE TABLE

<a id="f4643777298c866d"></a>
### 기능

테이블의 통계 정보를 제어한다.

<a id="44121cece0cefb20"></a>
### 구문

```
<analyze table statement> ::=
    ANALYZE TABLE table_name
    [ <parallel clause> ]
    [ <analyze action> ]
    ;

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [thread_count]

<analyze action> ::=
      COMPUTE STATISTICS [ <for_clause> | <for_clause_extension> ]
    | ESTIMATE STATISTICS <sample_clause> [ <for_clause> | <for_clause_extension> ]
    | DELETE STATISTICS
    | DELETE STATISTICS <for_clause_extension>

<sample_clause>
      SAMPLE row_count ROWS
    | SAMPLE percentage PERCENT

<for_clause>
      FOR ALL COLUMNS
    | FOR ALL INDEXED COLUMNS
    | FOR COLUMNS column_name [, ...]
    | FOR ALL INDEXES
    | FOR INDEXES index_name [, ...]

<for_clause_extension>
    FOR COLUMN GROUPS( column_name [, ...] )
```

<a id="cbf6e6023a855845"></a>
### 사용 범위 및 접근 권한

&lt;analyze table statement&gt; 구문을 수행하려면 사용자에게 ANALYZE ANY ON DATABASE 권한이 있어야 한다.

<a id="3d70073fa1571b5a"></a>
### 구문 규칙 및 파라미터

<a id="19112d626a348988"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="e8ce2125e60c492e"></a>
#### &lt;parallel clause&gt;

분석 과정에서 사용할 thread 개수를 지정한다.   
명시하지 않을 경우, 기본값은 PARALLEL 이다.

- NOPARALLEL
    - 병렬로 분석하지 않는다.

- PARALLEL [thread_count]
    - 병렬로 분석한다.
    - thread_count 값은 0 부터 사용할 수 있으며 최대값은 64 이다.
    - thread_count 값이 0이거나 생략된 경우 시스템의 CPU 개수에 의해 결정된다.

<a id="ff52b0431577be36"></a>
#### &lt;analyze action&gt;

생략할 경우 기본값은 COMPUTE STATISTICS 이다.

<a id="cbd5ef60b91e53d2"></a>
#### COMPUTE STATISTICS

전수 검사를 통해 테이블과 관련된 다음과 같은 통계 정보를 구축한다.

- Table 통계 정보 
    - Row count
    - Page 개수 
- 각 column의 통계 정보 
    - 서로 다른 값의 개수 
    - NULL 값의 개수 
    - 값의 평균 길이 
    - 최소값 
    - 최대값
    - Height-balanced histogram
        - [HISTOGRAM_BALANCE_BUCKET_COUNT](../part-02-administration-manual/10-server-property.md#0646042872327a32) 프로퍼티를 활성화할 경우에 구축되는 정보이다.
        - 생성할 balance bucket 개수는 HISTOGRAM_BALANCE_BUCKET_COUNT (권장값: 20)에 따라 결정된다.
    - Frequency histogram
        - [HISTOGRAM_FREQUENCY_BUCKET_COUNT](../part-02-administration-manual/10-server-property.md#ef42f2f75da19f94) 프로퍼티를 활성화할 경우에 구축되는 정보이다.
        - 생성할 frequency bucket 개수가 HISTOGRAM_FREQUENCY_BUCKET_COUNT (권장값: 20)보다 클 경우에는 구축되지 않는다.
- Index 통계 정보 
    - 서로 다른 key의 개수
    - Page 개수
    - Leaf page 개수
    - Tree level
    - 인덱스 군집도 (clustering factor)

Column의 data type에 따라 구축하는 통계 정보는 다음과 같다.

**Data type에 따라 구축된 통계 정보**

<a id="e853c0706450fc51"></a>
| Data type | NUM_DISTINCT | NUM_NULLS | AVG_LENGTH | MIN/MAX | Height-balanced Histogram | Frequency  Histogram |
| --- | --- | --- | --- | --- | --- | --- |
| BOOLEAN | O | O | O | X | X | O |
| NATIVE_SMALLINT | O | O | O | O | O | O |
| NATIVE_INTEGER | O | O | O | O | O | O |
| NATIVE_BIGINT | O | O | O | O | O | O |
| NATIVE_REAL | O | O | O | O | O | O |
| NATIVE_DOUBLE | O | O | O | O | O | O |
| NUMBER | O | O | O | O | O | O |
| NUMERIC | O | O | O | O | O | O |
| FLOAT | O | O | O | O | O | O |
| CHAR(n) | O | O | O | 64 bytes 이하인  경우에 구축된다. | 64 bytes 이하인 경우에 구축된다. | 64 bytes 이하인 경우에 구축된다. |
| VARCHAR(n) | O | O | O | 64 bytes 이하인  경우에 구축된다. | 64 bytes 이하인 경우에 구축된다. | 64 bytes 이하인 경우에 구축된다. |
| LONG VARCHAR | X | X | X | X | X | X |
| BINARY | O | O | O | X | X | X |
| VARBINARY | O | O | O | X | X | X |
| LONG VARBINARY | X | X | X | X | X | X |
| DATE | O | O | O | O | O | O |
| TIME | O | O | O | O | O | O |
| TIMESTAMP | O | O | O | O | O | O |
| INTERVAL | O | O | O | O | O | O |
| ROWID | O | O | O | X | X | X |

<a id="de6042db19449aa3"></a>
#### ESTIMATE STATISTICS &lt;sample_clause&gt;

지정한 &lt;sample_clause&gt;만큼의 샘플을 사용하여 column과 index의 통계 정보를 구축한다.

- SAMPLE row_count ROWS 
    - 지정한 row 개수만큼 샘플을 사용한다. 
    - row_count는 0보다 큰 양의 정수이다. 
- SAMPLE percentage PERCENT 
    - 지정한 비율만큼 샘플을 사용한다. 
    - Percentage는 1 ~ 99 범위의 양의 정수이다.

샘플링 row의 개수가 [MIN_SAMPLE_ROW_COUNT](../part-02-administration-manual/10-server-property.md#254c80b8b5f8dc20) 프로퍼티 값보다 작을 경우 프로퍼티 값을 따른다.

<a id="7b7707c29993a868"></a>
#### &lt;for_clause&gt;

생략할 경우, 통계정보 구축이 가능한 모든 column과 모든 인덱스의 통계 정보를 구축한다.

<a id="965a58a123e000f5"></a>
#### FOR ALL COLUMNS

통계 정보 구축이 가능한 모든 column의 통계 정보를 구축한다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="35ac4f0d5a473f3f"></a>
#### FOR ALL INDEXED COLUMNS

인덱스에 포함된 모든 column의 통계 정보를 구축한다.   
그 외 column의 통계 정보는 구축하지 않는다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="6ff65afb1c495bf5"></a>
#### FOR COLUMNS column_name [, ...]

나열한 column의 통계 정보를 구축한다.   
기술하지 않은 column의 통계 정보는 구축하지 않는다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="b08e4c83ddce81d6"></a>
#### FOR ALL INDEXES

모든 인덱스의 통계 정보를 구축한다.   
Column 통계 정보는 구축하지 않는다.

<a id="07066fbee5574ad9"></a>
#### FOR INDEXES index_name [, ...]

나열한 인덱스의 통계 정보를 구축한다.   
기술하지 않은 인덱스의 통계 정보는 구축하지 않는다.   
Column 통계 정보는 구축하지 않는다.

<a id="40e1577e417000de"></a>
#### FOR COLUMN GROUPS ( column_name [, ...] )

해당 구문은 COLUMN GROUP 조합의 NUM_DISTINCT 값을 구축한다.

예를 들어 item 테이블에 ( i_company, i_brand ) column들이 있을 경우에, i_brand column의 'I-PHONE' 값은 i_company column의 'APPLE' 값에 대한 dependency가 매우 강하다.

FOR COLUMN GROUPS( i_company, i_brand )의 통계정보를 구축하면 optimizer가 다음과 같은 질의를 분석하는데 도움이 된다.

```
SELECT * 
  FROM item, sales, ...
 WHERE i_brand = 'I-PHONE'
   AND i_company = 'APPLE' 
   AND i_item_id = s_item_id
   AND ...
```

- 사용자가 FOR COLUMN GROUPS를 명시한 경우에만 구축한다.
    - (O) ANALYZE TABLE item COMPUTE STATISTICS FOR COLUMN GROUPS ( i_company, i_brand );
- 다음과 같이 순서만 바꾼 column의 조합은 위와 동일한 COLUMN GROUP 이므로 생성할 수 없다.
    - (X) ANALYZE TABLE item COMPUTE STATISTICS FOR COLUMN GROUPS ( i_brand, i_company );
- 동일한 column을 기술할 수 없다.
    - (X) ANALYZE TABLE item COMPUTE STATISTICS FOR COLUMN GROUPS ( i_company, i_brand, i_company );
- 조합할 수 있는 column의 개수는 2~4 개이다.
    - (X) ANALYZE TABLE item COMPUTE STATISTICS FOR COLUMN GROUPS ( i_category );
    - (X) ANALYZE TABLE item COMPUTE STATISTICS FOR COLUMN GROUPS ( i_category, i_class, i_company, i_brand, i_size, i_type );

<a id="45f250e300464394"></a>
#### DELETE STATISTICS

테이블의 통계 정보를 제거한다.

<a id="0aed1a23cac844d5"></a>
#### DELETE STATISTICS FOR COLUMN GROUPS ( column_name [, ...] )

지정한 COLUMN GROUP 통계 정보를 제거한다.

<a id="1ca8b688de1784de"></a>
### 설명

테이블 통계 정보는 질의 최적화의 정확도에 영향을 미치는 매우 중요한 정보이다.

통계 정보 구축시간은 테이블의 데이터 양에 비례하므로, 데이터 양이 많을 경우 샘플링을 사용하여 통계 정보를 구축하거나 질의에 영향을 미치는 주요 정보에 대해서만 통계 정보를 구축하는 것이 바람직하다.

- 다음은 샘플링을 사용하여 통계 정보를 구축하는 예이다.

```
ANALYZE TABLE lineitem ESTIMATE STATISTICS SAMPLE 10 PERCENT;
```

- 다음은 주요 column과 인덱스에 대해서만 통계 정보를 구축하는 예이다.

```
ANALYZE TABLE lineitem COMPUTE STATISTICS FOR ALL INDEXED COLUMNS;
ANALYZE TABLE lineitem COMPUTE STATISTICS FOR ALL INDEXES;
```

<a id="bfb8cd6cef186d49"></a>
### 사용 예

다음은 전수 검사를 통해 통계 정보를 구축하는 예이다.

```
gSQL> ANALYZE TABLE orders;

Table analyzed.
```

다음은 구축된 테이블 통계 정보를 조회하는 예이다.

```
gSQL>
SELECT 
       TABLE_NAME
     , NUM_ROWS
  FROM
       DICTIONARY_SCHEMA.USER_TABLES
 WHERE
       TABLE_SCHEMA = 'PUBLIC'
   AND TABLE_NAME   = 'ORDERS'
;

TABLE_NAME NUM_ROWS
---------- --------
ORDERS      1500000

1 row selected.


gSQL>
SELECT 
       TABLE_NAME
     , COLUMN_NAME
     , NUM_DISTINCT
     , NUM_NULLS
     , LOW_VALUE
     , HIGH_VALUE
  FROM
       DICTIONARY_SCHEMA.USER_TAB_COLUMNS
 WHERE
       TABLE_SCHEMA = 'PUBLIC'
   AND TABLE_NAME   = 'ORDERS'
;

TABLE_NAME COLUMN_NAME     NUM_DISTINCT NUM_NULLS LOW_VALUE           HIGH_VALUE         
---------- --------------- ------------ --------- ------------------- -------------------
ORDERS     O_ORDERKEY           1500000         0 1                   6000000            
ORDERS     O_CUSTKEY              99996         0 1                   149999             
ORDERS     O_ORDERSTATUS              3         0 F                   P                  
ORDERS     O_TOTALPRICE         1464556         0 857.71              555285.16          
ORDERS     O_ORDERDATE             2406         0 1992-01-01 00:00:00 1998-08-02 00:00:00
ORDERS     O_ORDERPRIORITY            5         0 1-URGENT            5-LOW              
ORDERS     O_CLERK                 1000         0 Clerk#000000001     Clerk#000001000    
ORDERS     O_SHIPPRIORITY             1         0 0                   0                  
ORDERS     O_COMMENT            1482071         0 null                null               

9 rows selected.

gSQL>
SELECT 
       TABLE_NAME
     , INDEX_NAME
     , DISTINCT_KEYS
  FROM
       DICTIONARY_SCHEMA.USER_INDEXES
 WHERE
       TABLE_SCHEMA = 'PUBLIC'
   AND TABLE_NAME   = 'ORDERS'
;

TABLE_NAME INDEX_NAME        DISTINCT_KEYS
---------- ----------------- -------------
ORDERS     ORDERS_PK_INDEX         1500000
ORDERS     ORDERS_CUSTKEY_FK         99996

2 rows selected.
```

<a id="7e988a22dca8007a"></a>
### 호환성

SQL 표준에서는 통계 정보에 대한 개념을 정의하지 않고 있다.

<a id="d42d345d42eb4711"></a>
### 참조

관련 내용은 [ANALYZE SYSTEM](#ceffc94d9a4e4c0a)을 참조한다.

<a id="c26186987b5864cf"></a>
## AUDIT POLICY

<a id="1b2215eb6d065f08"></a>
### 기능

Audit policy를 활성화한다.

<a id="24274b228bf073cf"></a>
### 구문

```
<audit policy statement> ::= 
    AUDIT POLICY policy_name
    [ <specified_user_option> ]
    [ <specified_success_option> ]
    ;

<specified_user_option> ::=
      BY user_name [, ...]
    | EXCEPT user_name [, ...]

<specified_success_option> ::=
      WHENEVER SUCCESSFUL
    | WHENEVER NOT SUCCESSFUL
```

<a id="cacc8b2088ebadfd"></a>
### 사용 범위 및 접근 권한

&lt;audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="6a89d2c67fd2e836"></a>
### 구문 규칙 및 파라미터

<a id="b111deea08c3a11a"></a>
#### policy_name

활성화할 audit policy 객체의 이름이다.   
활성화 된 audit policy는 기존 session에 영향을 미치지 않으며 새로 생성되는 session에만 영향을 준다.

<a id="500c03bebd456f1b"></a>
#### &lt;specified_user_option&gt;

감사를 수행할 사용자를 명시한다.     
생략할 경우 모든 사용자에 대해 감사를 수행한다.

동일한 audit policy에 대해 BY 절과 EXCEPT 절을 함께 사용할 수 없다.

- BY user_list: 감사를 수행할 사용자를 특정할 경우 BY 절을 사용한다.
- EXCEPT user_list: 특정 사용자를 배제하고 다른 사용자들을 감사할 경우 EXCEPT 절을 사용한다.

<a id="b82753b352c43a0c"></a>
#### &lt;specified_success_option&gt;

- WHENEVER SUCCESSFUL
    - Action이 성공했을 때 audit record가 생성된다.
- WHENEVER NOT SUCCESSFUL
    - Action이 실패했을 때 audit record가 생성된다.
- 생략할 경우 성공할 경우와 실패할 경우 모두 audit record를 생성한다.

<a id="00b9a96c69b3aba1"></a>
### 설명

Audit policy를 활성화하면 기존 session에는 영향을 미치지 않으며 새로 생성되는 session에 대해 감사를 시작한다.

<a id="55139d4fb4738c68"></a>
#### Audit Record 조회

감사 조건에 부합할 경우 audit record를 생성하는데 다음과 같이 DICTIONARY_SCHEMA.AUDIT_TRAIL view를 통해 조회할 수 있다.

```
SELECT logon_user
     , event_timestamp
     , action_name
     , object_name 
     , sql_text
  FROM audit_trail
 WHERE policy_name = 'P1'
;
```

일반 사용자가 AUDIT_TRAIL을 조회하려면 SELECT 권한을 부여받아야 한다.

```
GRANT SELECT ON DICTIONARY_SCHEMA.AUDTI_TRAIL TO user_name;
```

<a id="e0f2e28146eb69fe"></a>
#### Audit Policy 정보 조회

Audit policy 객체 정보는 DICTIONARY_SCHEMA.AUDIT_POLICY_OPTIONS view를 통해 조회할 수 있다.

```
SELECT policy_name
     , audit_option
     , object_schema
     , object_name
  FROM audit_policy_options
;
```

Audit policy 객체들의 활성화 정보는 DICTIONARY_SCHEMA.AUDIT_POLICY_ENABLED view를 통해 조회할 수 있다.

```
SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
;
```

<a id="decd9ca3df13a5ff"></a>
#### BY 절과 EXCEPT 절 사용 시 유의사항

동일한 audit policy에 대해 다수의 AUDIT POLICY BY 절을 사용할 경우, user들의 집합을 활성화한다.   
즉, 다음 두 예는 동일한 의미이다.

- 예제 1: u1, u2에 대해 p1 audit policy를 활성화한다.

```
AUDIT POLICY p1 BY u1;
AUDIT POLICY p1 BY u2;
```

- 예제 2: u1, u2에 대해 p1 audit policy를 활성화한다.

```
AUDIT POLICY p1 BY u1, u2;
```

동일한 audit policy에 대해 다수의 AUDIT POLICY EXCEPT 절을 사용할 경우, 마지막 AUDIT POLICY 구문만 유효하다.   
즉, 다음 두 예는 다른 의미이다.

- 예제 1: 마지막 구문만 유효하며 u2를 배제하고 p1 audit policy를 활성화한다.

```
AUDIT POLICY p1 EXCEPT u1;
AUDIT POLICY p1 EXCEPT u2;
```

- 예제 2: u1과 u2를 배제하고 p1 audit policy를 활성화한다.

```
AUDIT POLICY p1 EXCEPT u1, u2;
```

같은 audit policy에 대해 BY와 EXCEPT를 함께 사용할 수 없다.

- BY 절로 audit policy가 활성화된 경우 이후에 BY 절만 사용할 수 있다.

```
AUDIT POLICY p1 BY u1;
```

    - Error

```
AUDIT POLICY p1 EXCEPT u2;
```

- EXCEPT 절로 audit policy가 활성화 된 경우 이후에 EXCEPT 절만 사용할 수 있다.

```
AUDIT POLICY p1 EXCEPT u1;
```

    - Error: by all users에 해당한다.

```
AUDIT POLICY p1;
```

BY로 활성화된 audit policy를 EXCEPT로 전환하거나 EXCEPT로 활성화된 audit policy를 BY로 전환하려면 먼저 활성화된 audit policy를 비활성화 한 후에 전환해야 한다.

다음 예와 같이 NOAUDIT POLICY 구문으로 비활성해야 한다.

- AUDIT POLICY p1 BY u1, u2;
    - NOAUDIT POLICY p1 BY u1, u2;
- AUDIT POLICY p1;
    - NOAUDIT POLICY p1;
- AUDIT POLICY p1 EXCEPT u1, u2;
    - NOAUDIT POLICY p1;
    - NOAUDIT POLICY 구문은 EXCEPT option 이 없다.

BY 절과 함께 사용하는 WHENEVER 절은 누적된다.

다음 두 예는 동일한 의미이다.

- 예제 1: 성공/ 실패와 관계없이 audit record를 생성한다.

```
AUDIT POLICY p1 BY u1 WHENEVER SUCCESSFUL;
AUDIT POLICY p1 BY u1 WHENEVER NOT SUCCESSFUL;
```

- 예제 2: 성공/ 실패와 관계없이 audit record를 생성한다.

```
AUDIT POLICY p1 BY u1;
```

WHENEVER 절이 EXCEPT 절과 함께 사용되면 마지막 WHENEVER 절만 유효하다.

다음 두 예는 서로 다른 의미이다.

- 예제 1: 실패할 경우 audit record를 생성한다.

```
AUDIT POLICY p1 EXCEPT u1 WHENEVER SUCCESSFUL;
AUDIT POLICY p1 EXCEPT u1 WHENEVER NOT SUCCESSFUL;
```

- 예제 2: 성공/ 실패와 관계없이 audit record를 생성한다.

```
AUDIT POLICY p1 EXCEPT u1;
```

<a id="0df7b90f49163503"></a>
### 사용 예

다음은 모든 사용자에 대해 audit policy를 활성화하는 예이다.

```
AUDIT POLICY table_pol;
```

다음 질의를 통해 활성화 정보를 확인할 수 있다.

```
SELECT policy_name
     , enabled_opt
     , user_name
  FROM audit_policy_enabled
 WHERE policy_name = 'TABLE_POL';

POLICY_NAME  ENABLED_OPT  USER_NAME
-----------  -----------  ---------
TABLE_POL    BY           ALL USERS
```

다음은 특정 사용자들을 한정하여 audit policy를 활성화하는 예이다.

```
AUDIT POLICY dml_pol BY u1, u2;
```

다음은 특정 사용자를 배제하여 audit policy를 활성화하는 예이다.

```
AUDIT POLICY read_seq_pol EXCEPT sys;
```

다음은 특정 사용자가 SQL 구문에 실패한 경우를 감사하는 예이다.

```
AUDIT POLICY delete_pol BY u1 WHENEVER NOT SUCCESSFUL;
```

<a id="96b9e315a18d7f91"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="ab1efdd2dc292a6a"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](19-sql-references-c-g.md#079c12405d0687f7)
    - [DROP AUDIT POLICY](19-sql-references-c-g.md#5665b185fc830eaa)
    - [ALTER AUDIT POLICY](#e6d664ed42cb125a)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#c26186987b5864cf)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#2a39421bd3a74134)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#28a87ad95b910b03)

- Audit trail 소거: [ALTER DATABASE CLEAR AUDIT TRAIL](#f4b53fa2e7dce2b7)

---

[← 17. Built-in Function References](17-built-in-function-references.md) · [전체 목차](../README.md) · [19. SQL References (C~G) →](19-sql-references-c-g.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
