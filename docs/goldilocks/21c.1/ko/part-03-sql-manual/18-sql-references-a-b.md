<a id="067b3cf49e911d60"></a>

# 18. SQL References (A~B)

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/067b3cf49e911d60)  
> 태그: `21c.1_35_tag`

[← 17. Built-in Function References](17-built-in-function-references.md) · [전체 목차](../README.md) · [19. SQL References (C~G) →](19-sql-references-c-g.md)

<a id="00bbcaab72bbb158"></a>
## ALTER AUDIT POLICY

<a id="33478d0bcc62d661"></a>
### 기능

Audit policy 객체에 감사 대상을 추가하거나 삭제한다.

<a id="b9762cd0a4786a3b"></a>
### 구문

```
<alter audit policy statement> ::= 
    ALTER AUDIT POLICY policy_name
    { <add_audit_option> | <drop_audit_option> }
    ;

<add_audit_option> ::=
    ADD { <privilege_audit_clause> |  <action_audit_clause> | <privilege_audit_clause> <action_audit_clause> }

<drop_audit_option> ::=
    DROP { <privilege_audit_clause> |  <action_audit_clause> | <privilege_audit_clause> <action_audit_clause> }


<privilege_audit_clause> ::=
    PRIVILEGES <database_privilege> [, ...]

<action_audit_clause> ::=
    ACTIONS { <object_action_audit> | <system_action_audit> } [, ...]

<object_action_audit> ::=
      ALL ON [schema_name.]object_name
    | <object_action> ON [schema_name.]object_name

<system_action_audit> ::=
      ALL
    | <system_action>
```

<a id="9a3a5e19e15986af"></a>
### 사용 범위 및 접근 권한

&lt;alter audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="3f447a82f7dec5c0"></a>
### 구문 규칙 및 파라미터

<a id="6c053467b8a30a4b"></a>
#### policy_name

변경할 audit policy 객체의 이름이다.

<a id="cf6b7c8ff33ab729"></a>
#### &lt;add_audit_option&gt;

Audit policy에 감사대상을 추가한다.

<a id="8cb2ae4331919773"></a>
#### &lt;drop_audit_option&gt;

Audit policy 감사대상에서 삭제한다.

<a id="1b3ce537a9f0dcd6"></a>
#### &lt;privilege_audit_clause&gt;

자세한 내용은 [CREATE AUDIT POLICY](19-sql-references-c-g.md#72600ff3c559dfb5)를 참조한다.

<a id="ddfaa772b87158d2"></a>
#### &lt;action_audit_clause&gt;

자세한 내용은 [CREATE AUDIT POLICY](19-sql-references-c-g.md#72600ff3c559dfb5)를 참조한다.

<a id="112d308d645c5646"></a>
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

<a id="9773cd2f504ed7c4"></a>
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

<a id="7341adff09db27ad"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="d0ab05e2067de87e"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](19-sql-references-c-g.md#72600ff3c559dfb5)
    - [DROP AUDIT POLICY](19-sql-references-c-g.md#1aaa5b1766ff2d59)
    - [ALTER AUDIT POLICY](#00bbcaab72bbb158)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#213cd4dbcc8bc668)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#15b6d2d5678734fb)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#18a54cc95a024f6e)

- Audit trail 삭제: [ALTER DATABASE CLEAR AUDIT TRAIL](#7098d8b3ccdebf40)

<a id="2aa692a04102ad1a"></a>
## ALTER CLUSTER GROUP name ADD MEMBER

<a id="470c69b4ef381f53"></a>
### 기능

Cluster group에 cluster member를 추가한다.

<a id="cbf337d300c1260b"></a>
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

<a id="4fe61196e05f7566"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster group add member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="af6be47288162221"></a>
### 구문 규칙 및 파라미터

<a id="72764ae82f1b9469"></a>
#### group_name

Cluster group의 이름이다.

<a id="cd43085b444a889e"></a>
#### &lt;cluster member definition&gt;

Cluster group에 포함될 cluster member를 정의한다.  
Cluster group은 최대 32 개의 cluster member를 포함할 수 있다.

<a id="1319aa99acbde267"></a>
#### member_name

Cluster member의 이름이다.   
Cluster member의 이름은 해당 member의 database를 생성할 때 정의한 member의 이름과 동일해야 한다.   
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.   
이름의 길이가 128 바이트보다 작아야 한다.

Cluster member의 start-up 단계가 GLOBAL OPEN이어야 한다.

<a id="dee35e0854516a33"></a>
#### &lt;connection attribute&gt;

Cluster member간 통신을 위한 연결 정보를 정의한다.   
&lt;connection attribute&gt;는 해당 member의 database를 생성할 때 정의한 HOST, PORT와 동일해야 한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 ip v4 형식을 사용한다. 
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="d81143bc46970c8f"></a>
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

<a id="0ceb5d3cbe1c8186"></a>
### 설명

&lt;alter cluster group add member statement&gt; 구문은 table들의 shard를 재배치하지 않는다.   
추가된 cluster member에 shard를 재배치하려면 다음 구문을 수행해야 한다.

- [ALTER DATABASE REBALANCE](#be8f993bb3ff62bc)
- [ALTER TABLE name REBALANCE](#1af19281915840f1)

<a id="c8687fc8f3ba471f"></a>
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

<a id="b495c3f9a284c96a"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="f096c814505dab2b"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#8e2b3a3076fcfb3e)
- [DROP CLUSTER GROUP](19-sql-references-c-g.md#8bcf309cea211dc8)
- [ALTER DATABASE REBALANCE](#be8f993bb3ff62bc)
- [ALTER TABLE name REBALANCE](#1af19281915840f1)

<a id="db0d7e893427ddd6"></a>
## ALTER CLUSTER GROUP name OFFLINE MEMBER

<a id="b245690c09fc4e31"></a>
### 기능

Cluster group의 cluster member를 offline 상태로 변경한다.

<a id="1f34f447995f756c"></a>
### 구문

```
<alter cluster group offline member statement> ::=
    ALTER CLUSTER GROUP group_name OFFLINE CLUSTER MEMBER member_name
    ;
```

<a id="0797bbf9f6e1612e"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster group offline member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="b994699480b243ef"></a>
### 구문 규칙 및 파라미터

<a id="24307de1c05754ee"></a>
#### group_name

Cluster group의 이름이다.

<a id="a6698a2205df3768"></a>
#### member_name

Cluster member의 이름이다.   
Cluster member는 group_name의 cluster group에 포함돼 있어야 한다.  
Cluster member가 inactive 상태여야 한다.

<a id="0ade4209ab9407ce"></a>
### 설명

Inactive 상태인 cluster member를 offline시킨다.

&lt;alter cluster group offline member statement&gt; 구문은 table들의 shard를 재배치하지 않는다.

<a id="724b94b970836540"></a>
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

<a id="99ecb9b6fab6de4a"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="fb4ab369a5780982"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#8e2b3a3076fcfb3e)
- [DROP CLUSTER GROUP](19-sql-references-c-g.md#8bcf309cea211dc8)
- [ALTER DATABASE REBALANCE](#be8f993bb3ff62bc)
- [ALTER TABLE name REBALANCE](#1af19281915840f1)

<a id="ba7b493d6f702d6f"></a>
## ALTER CLUSTER LOCATION

<a id="083fc43a2a56b685"></a>
### 기능

Cluster location 정보를 수정한다.

<a id="618f5db0d7fd285c"></a>
### 구문

```
<alter cluster location statement> ::=
    ALTER CLUSTER LOCATION member_name 
    <cluster connection attribute>
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="1dbcd0cfa38f4dcf"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster location statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="cccacb6717d159fd"></a>
### 구문 규칙 및 파라미터

<a id="b801a5c0f21d73de"></a>
#### member_name

Cluster member의 이름이다.   
등록된 cluster location 정보에 동일한 cluster member 이름이 존재해야 한다.   
이름의 길이가 128 바이트보다 작아야 한다.

<a id="f84a8582ff1e2a4e"></a>
#### &lt;cluster connection attribute&gt;

Cluster member 간 통신을 위한 연결 정보를 정의한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 ip v4 형식으로 사용한다. 
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="adb648360a5cc8f2"></a>
### 설명

만약 cluster location의 접속 정보가 변경될 경우에는 cluster member를 제거하거나 재생성할 필요없이 [ALTER CLUSTER LOCATION](#ba7b493d6f702d6f)을 이용하여 접속 정보를 변경할 수 있다.

<a id="09fe6e03af348613"></a>
### 사용 예

```
gSQL> 
ALTER CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120
;

altered.
```

<a id="621acad77e705650"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="fbfb6b34b5a369ba"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER LOCATION](19-sql-references-c-g.md#677b16ec3653271c)
- [DROP CLUSTER LOCATION](19-sql-references-c-g.md#28783969fbe8714a)

<a id="3c10e4add82b29c6"></a>
## ALTER DATABASE ADD LOGFILE

<a id="1f54c71cfd0d506a"></a>
### 기능

데이터베이스에 로그파일 그룹 또는 로그파일 멤버를 추가한다.

<a id="95324e26d1f97804"></a>
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

<a id="e48da67f3a34584a"></a>
### 사용 범위 및 접근 권한

&lt;alter database add logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="31c9fe34ede0b86b"></a>
### 구문 규칙 및 파라미터

<a id="2fcef63a3c5933b7"></a>
#### &lt;alter database add logfile statement&gt;

데이터베이스는 MOUNT 상태여야 한다.

<a id="c1d2257a6c125c45"></a>
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

<a id="1f187f21c2c89cf8"></a>
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

<a id="5e3a2b1c2433b9f7"></a>
### 설명

새로운 로그파일 그룹 및 로그 멤버가 추가되는 경우 controlfile에 저장되므로 향후 controlfile 손상에 대비해 controlfile을 백업하는 것을 권장한다.

<a id="9fbf85b9797f6893"></a>
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

<a id="35c9e2311834ee06"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="a77d073216504a5a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#3c10e4add82b29c6)
- [ALTER DATABASE DROP LOGFILE](#ae139293d7bcd6f4)
- [ALTER DATABASE RENAME LOGFILE](#1b93c0c90b2452f9)

<a id="48ae0aa4fc2a7224"></a>
## ALTER DATABASE ARCHIVELOG

<a id="c3978243aa96abe8"></a>
### 기능

데이터베이스의 온라인 로그파일 archive 설정을 변경한다.

<a id="0d204caf5da8ffc1"></a>
### 구문

```
<alter database archivelog statement> ::=
    ALTER DATABASE { ARCHIVELOG | NOARCHIVELOG }
    ;
```

<a id="373f68f2ad424de0"></a>
### 사용 범위 및 접근 권한

&lt;alter database archivelog statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="5539b988182061ce"></a>
### 구문 규칙 및 파라미터

<a id="e2eaba206d72b31c"></a>
#### &lt;alter database archivelog statement&gt;

- 데이터베이스가 MOUNT 상태여야 한다.
- ARCHIVELOG
    - 온라인 로그파일을 archive 한다.
- NOARCHIVELOG
    - 온라인 로그파일을 archive 하지 않는다.

<a id="2052596e54732a08"></a>
### 설명

Database를 백업하고 백업을 이용해 복구 (media recovery)하려면 시스템이 ARCHIVELOG 모드로 운용되어야 한다.

<a id="1b2d1a674440c6c2"></a>
### 사용 예

다음은 데이터베이스를 archive 모드로 설정하는 예이다.

```
ALTER DATABASE ARCHIVELOG;
```

<a id="3c40e71284df4e1b"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="17bf18e41e8f8340"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#7c06bf1cb158127b)
- [ALTER TABLESPACE name BACKUP](#9835448e7383ecdf)

<a id="7c06bf1cb158127b"></a>
## ALTER DATABASE BACKUP

<a id="34b7b20e20897cf6"></a>
### 기능

데이터베이스 전체 백업 (full backup)을 수행하기 위해 백업 상태를 'ACTIVE' 또는 'INACTIVE'로 설정한다. 그리고 데이터베이스 증분 백업 (incremental backup)과 제어 파일 (control file) 백업을 수행한다.

<a id="ade72fbe3291abd7"></a>
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
        <incremental backup option> [ AT <domain name> ]    ;

<incremental backup option> ::=
      LEVEL integer [ CUMULATIVE | DIFFERENTIAL ]

<database controlfile backup statement> ::=
    ALTER DATABASE BACKUP CONTROLFILE TO 'target_name'
        [ AT <domain name> ]    ;
```

<a id="42a4e5da569c42bf"></a>
### 사용 범위 및 접근 권한

&lt;alter database backup statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="a4ed5c549075ec33"></a>
### 구문 규칙 및 파라미터

<a id="601c5f551795bbfd"></a>
#### &lt;database begin backup clause&gt;

데이터베이스를 전체 백업이 가능한 상태로 설정한다.

- 데이터베이스에서 생성되어 사용 중인 ONLINE 상태의 모든 테이블스페이스를 전체 백업이 가능한 상태로 설정한다. 
- 데이터베이스는 OPEN 상태여야 하고 ARCHIVELOG 모드로 운영되어야 한다.
- BEGIN BACKUP이 시작된 이후에는 다음과 같이 데이터 파일에 쓰기를 요구하는 연산들은 수행할 수 없다.
    - SHUTDOWN NORMAL
    - OFFLINE/ DROP TABLESPACE
    - ADD/ DROP DATAFILE
- 전체 백업의 상태가 ACTIVE인 상태에서 인스턴스가 비정상 종료될 경우, 다시 시작할 때 미디어 복구를 요구할 수도 있다.

<a id="3027bcb7bc5577bd"></a>
#### &lt;database end backup clause&gt;

데이터베이스를 전체 백업 불가능한 상태로 설정한다.

- 데이터베이스에서 생성되어 사용 중인 ONLINE 상태의 모든 테이블스페이스를 백업 불가능한 상태로 설정한다.
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG 모드로 운영되어야 한다.

<a id="6e5fe669d251b60d"></a>
#### &lt;database incremental backup statement&gt;

- 데이터베이스 증분 백업을 수행한다.
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG로 운영되어야 한다.

<a id="bce130c02d2d8acb"></a>
#### &lt;incremental backup option&gt;

- 'integer'는 0 ~ 4 까지 지정할 수 있다.
- LEVEL 0은 CUMULATIVE나 DIFFERENTIAL을 지정할 수 없다.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - 'integer'가 n이면 가장 최근에 LEVEL 0 ~ LEVEL n-1까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - DIFFERENTIAL
        - 'integer'가 n이면 가장 최근에 LEVEL 0 ~ LEVEL n까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - 생략하면 DIFFERENTIAL이 기본으로 지정된다.

<a id="876283eb013bd627"></a>
#### &lt;database controlfile backup statement&gt;

- 제어 파일 (controlfile)을 백업한다.
    - 'target_name'의 이름은 1024 바이트보다 작아야 한다. 
    - 'target_name'이 이미 존재하는 경우 연산에 실패한다. 
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG로 운영되고 있어야 한다.

> GOLDILOCKS에서 관리하는 'target_name' 길이는 최대 1024 바이트이지만, OS마다 최대로 허용하는 파일 이름 길이가 다르기 때문에, 실제 생성가능한 'target_name'의 길이는 1024 바이트보다 작을 수 있다.

<a id="52ec567774a753c5"></a>
#### &lt;domain name&gt;

- 구문을 수행할 멤버나 그룹의 이름이다.
- 지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="2d52ddfadc7e9c41"></a>
### 설명

Database의 datafile과 controlfile을 백업한다. BEGIN BACKUP을 수행한 후 OS의 파일 복사로 datafile들을 복사하고 나서 END BACKUP을 수행하여 database를 전체 백업한다. 한편, 증분 백업 파일은 하나의 구문으로 BACKUP_DIR_1 property에 설정된 경로에 생성한다.

<a id="d93c7d32b2425e0a"></a>
### 사용 예

다음은 전체 백업 상태를 ACTIVE로 설정하는 예이다.

```
ALTER DATABASE BEGIN BACkUP;
```

다음은 전체 백업 상태를 INACTIVE로 설정하는 예이다.

```
ALTER DATABASE END BACkUP;
```

다음은 DIFFERENTIAL을 사용하여 LEVEL 1의 증분 백업을 만드는 예이다.

```
ALTER DATABASE BACKUP INCREMENTAL LEVEL 1 DIFFERENTIAL;
```

다음은 controlfile에 대해 'controlfile.bak' 백업 파일을 만드는 예이다. 절대 경로가 포함되지 않으면 LOG_DIR property에 설정된 경로에 백업 파일을 생성한다.

```
ALTER DATABASE BACKUP CONTROLFILE TO 'controlfile.bak';
```

<a id="66dc9f940872c972"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="524afd0b9f285dfe"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#9835448e7383ecdf)
- [ALTER DATABASE RECOVER](#c133e118c29e1673)

<a id="7098d8b3ccdebf40"></a>
## ALTER DATABASE CLEAR AUDIT TRAIL

<a id="e2dc9ba48754069a"></a>
### 기능

Audit policy 적용으로 인해 누적된 audit record를 삭제 (purge)한다.

<a id="c059cd7946f82e5a"></a>
### 구문

```
<clear audit trail statement> ::= 
    ALTER DATABASE CLEAR AUDIT TRAIL
;
```

<a id="faae6775d0b3bc94"></a>
### 사용 범위 및 접근 권한

&lt;clear audit trail statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="6bacbd0184f29c8a"></a>
### 설명

Audit policy를 활성화하면 시간이 지남에 따라 audit trail이 계속 커진다.   
Audit trail을 구성하는 테이블들은 MEM_AUX_TBS 테이블스페이스에 저장되는데 audit trail이 계속 커지지 않도록 해야 한다.

<a id="9e32474d55e3c9d2"></a>
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

<a id="b105c7c0dddd0c1a"></a>
### 사용 예

다음 구문을 사용하여 audit trail을 삭제 (purge)한다.

```
ALTER DATABASE CLEAR AUDIT TRAIL;
```

<a id="8cd163e8b89c6e11"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="0923ecae5ab8cf01"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](19-sql-references-c-g.md#72600ff3c559dfb5)
    - [DROP AUDIT POLICY](19-sql-references-c-g.md#1aaa5b1766ff2d59)
    - [ALTER AUDIT POLICY](#00bbcaab72bbb158)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#213cd4dbcc8bc668)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#15b6d2d5678734fb)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#18a54cc95a024f6e)

- Audit trail 삭제: [ALTER DATABASE CLEAR AUDIT TRAIL](#7098d8b3ccdebf40)

<a id="d574b13dcc907e21"></a>
## ALTER DATABASE CLEAR PASSWORD HISTORY

<a id="792221ff9014fff2"></a>
### 기능

Profile 적용에 따라 누적된 사용자의 비밀번호 변경 이력을 삭제한다.

<a id="7db04287937923e1"></a>
### 구문

```
<clear password history statement> ::= 
    ALTER DATABASE CLEAR PASSWORD HISTORY
    ;
```

<a id="6c7160e870f8501d"></a>
### 사용 범위 및 접근 권한

&lt;clear password history statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="152d3376a1311a91"></a>
### 설명

User에 profile을 적용할 때 PASSWORD_REUSE_MAX, PASSWORD_REUSE_TIME의 정책에 따라 사용자의 비밀번호 변경이력이 누적된다.

**변경 이력 관리**

<a id="9527ac5e29829d18"></a>
| PASSWORD_REUSE_MAX | PASSWORD_REUSE_TIME | 변경 이력 관리 |
| --- | --- | --- |
| value | value | Value 범위 내의 변경 이력만 관리하고 범위를 벗어난 변경 이력은 자동으로 삭제한다. |
| value | UNLIMITED | 모든 변경 이력을 검사해야 하므로 변경 이력을 누적할 뿐 제거하지 않는다. |
| UNLIMITED | value | 모든 변경 이력을 검사해야 하므로 변경 이력을 누적할 뿐 제거하지 않는다. |
| UNLIMITED | UNLIMITED | 변경 이력을 검사하지 않으므로 관리도 하지 않는다. |

&lt;clear password history statement&gt; 구문은 누적된 사용자 비밀번호 변경이력을 삭제한다.

<a id="dc71a4dc3dc97ae1"></a>
### 사용 예

다음은 &lt;clear password history statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE CLEAR PASSWORD HISTORY;

Database altered.

gSQL> COMMIT;

Commit complete.
```

<a id="aba74853b4a90775"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="73b46be63c408a65"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE PROFILE](19-sql-references-c-g.md#f421f468f014cc7b)
- [CREATE USER](19-sql-references-c-g.md#f516f713c62659c7)

<a id="6c1dc4fd490b9850"></a>
## ALTER DATABASE DATAFILE AUTOEXTEND

<a id="6a4d2a5aae62971a"></a>
### 기능

디스크 테이블스페이스 데이터 파일의 자동 확장 속성을 변경한다. 자동 확장 속성을 ON으로 변경하면 확장시킬 크기와 데이터 파일의 최대 크기도 변경할 수 있다.

<a id="098dda025a2bfe63"></a>
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

<a id="308df75d6e06b871"></a>
### 사용 범위 및 접근 권한

&lt;alter database datafile autoextend statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

데이터 파일 자동 확장 속성은 디스크 테이블스페이스에 한해서만 변경할 수 있다.

<a id="97c5aaba066ae88e"></a>
#### datafile_name

변경할 데이터 파일의 이름을 지정한다.

<a id="57da47ecaac0c0e5"></a>
#### &lt;autoextend clause&gt;

자동 확장 속성을 ON 또는 OFF로 설정한다. ON으로 설정하면 자동 확장 크기와 데이터 파일의 최대 크기를 지정할 수 있다.

<a id="4f692e86ed1ec5b1"></a>
#### &lt;next size clause&gt;

현재 사용 중인 데이터 파일에 더 이상 사용할 공간이 없을 때 확장할 크기를 지정한다.

<a id="7485a4c3dc8c34f3"></a>
#### &lt;max size clause&gt;

데이터 파일이 확장될 수 있는 최대 크기를 지정한다.

<a id="d88770f92ef752ec"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="2186432aa0259edb"></a>
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

<a id="ad35a30fe527750d"></a>
### 호환성

SQL 표준에서는 데이터 파일에 대한 개념을 정의하지 않고 있다.

<a id="9ee40891795c34b7"></a>
### 참조

관련 내용은 [CREATE DISK DATA TABLESPACE](19-sql-references-c-g.md#2cadf771c7ba93ae)를 참조한다.

<a id="b19db34bfd1301f1"></a>
## ALTER DATABASE DELETE BACKUP

<a id="ec2cfa3d162e2b16"></a>
### 기능

증분 백업 (incremental backup)의 백업 정보와 백업 파일을 삭제한다. Database의 모든 증분 백업을 삭제하거나, 더 이상 쓸모 없는 백업 (obsolete backup)을 선택해서 삭제할 수 있다.

<a id="82839899bc2ad0bc"></a>
### 구문

```
<alter database delete backup statement> ::=
    ALTER DATABASE DELETE <delete backup list option> 
        BACKUP LIST [ <including backup file option> ]
    ;

<delete backup list option> ::=
      OBSOLETE
    | ALL

<including backup file option> ::=
    INCLUDING BACKUP FILES
```

<a id="9e3f18939c960b06"></a>
### 사용 범위 및 접근 권한

&lt;alter database delete backup statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="3b5faccf914c6c97"></a>
### 구문 규칙 및 파라미터

<a id="22dfda39bf9244c3"></a>
#### &lt;alter database delete backup statement&gt;

데이터베이스가 MOUNT 또는 OPEN 상태여야 한다.

<a id="7fb41d33cc841084"></a>
#### &lt;delete backup list option&gt;

기존 증분 백업들 중에서 삭제할 대상을 선정한다.

- OBSOLETE: 가장 최근의 데이터베이스 'LEVEL 0' 백업 이전에 백업한 데이터베이스 또는 테이블스페이스 백업본들을 삭제 대상으로 선정한다.
- ALL: 전체 증분 백업들을 삭제 대상으로 선정한다.

<a id="804946e7c3797023"></a>
#### &lt;including backup file option&gt;

- 생략되면 백업 정보만 제어 파일에서 삭제한다.
- 백업 정보뿐만 아니라 백업 파일들도 함께 삭제한다.

<a id="53dadc80415beeca"></a>
### 설명

OBSOLETE 증분 백업 삭제는 가장 최근의 LEVEL 0 데이터베이스 백업 이전의 증분 백업을 삭제한다. 즉, LEVEL 0이 아닌 증분 백업을 수행할 때는 이전에 수행한 증분 백업을 포함하는 증분 백업이 있더라도 삭제하지 않는다. 왜냐하면 증분 백업을 이용한 불완전 복구를 수행할 때 사용될 수 있기 때문이다.

> 증분 백업을 삭제할 때 백업 파일까지 함께 삭제하면 증분 백업 정보를 포함하는 백업된 controlfile을 이용하더라도 복구를 수행할 수 없으므로 주의해야 한다.

<a id="0e291a033951e98b"></a>
### 사용 예

다음은 기존 모든 증분 백업들의 백업정보와 백업파일들을 삭제하는 예이다.

```
ALTER DATABASE DELETE ALL BACKUP LIST INCLUING BACKUP FILES;
```

<a id="b8d2e7bda5afa718"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="af7cb843ac356742"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#9835448e7383ecdf)
- [ALTER DATABASE RECOVER](#c133e118c29e1673)

<a id="4097c0f933c6e040"></a>
## ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS

<a id="e6ccabe5f5aa2826"></a>
### 기능

모든 inactive cluster member들을 제거한다.

<a id="8a639e5fd15dbc03"></a>
### 구문

```
<alter database drop inactive members statement> ::=
    ALTER DATABASE DROP [ FORCE | NO FORCE ] INACTIVE CLUSTER MEMBERS
    ;
```

<a id="0840e2ed448b8bc6"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database drop inactive cluster members statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="6a73425ee43a6e4e"></a>
### 구문 규칙 및 파라미터

<a id="16781ec19390e73d"></a>
#### [ FORCE | NO FORCE ]

- FORCE
    - 데이터 유실될 수 있는 경우에도 inactive cluster member들을 제거한다.
- NO FORCE
    - 데이터가 유실될 수 있는 경우에는 inactive cluster member들을 제거할 수 없다.
- 기본값은 NO FORCE 이다.

<a id="0c3dfa9f5d348b5b"></a>
### 설명

모든 inactive cluster member들을 제거한다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우 
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

단, cluster member를 제거할 때 table의 shard가 유실되는 경우에는 inactive cluster member를 제거할 수 없다.

또한, cluster member를 제거할 때 데이터가 유실될 수 있는 경우에는 inactive cluster member를 제거할 수 없다. 제거하려는 inactive cluster member에 속해 있는 table이나 shard의 replica가 해당 cluster group의 다른 멤버들보다 최신 데이터를 가지고 있지 않다는 보장이 있어야 데이터 유실을 방지할 수 있다. 따라서 cloned table의 경우에는 cluster 전체에, sharded table의 경우에는 같은 cluster group에 적어도 하나의 online 멤버가 존재할 경우에 inactive cluster member 제거를 허용한다.

단, cluster group에 online 상태인 cluster member가 없고 inactive cluster member로 인해 서비스가 불가능한 경우에는 데이터 유실을 감수하면서 FORCE 옵션을 통해 inactive cluster member를 제거할 수 있다.

&lt;alter database drop inactive members statement&gt; 구문은 모든 inactive cluster member들이 더 이상 cluster system에 포함될 수 없는 경우에 사용하는 것이 바람직하다.

<a id="fda6d71be6618a83"></a>
### 사용 예

다음은 &lt;alter database drop inactive members statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="e58e9bc7abb3bd41"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="649f2fa55fe5c6fc"></a>
### 참조

관련 내용은 [ALTER SYSTEM JOIN DATABASE](#a4c3515652081fcc) 를 참조한다.

<a id="ae139293d7bcd6f4"></a>
## ALTER DATABASE DROP LOGFILE

<a id="301603fe88f8fcdd"></a>
### 기능

데이터베이스에 존재하는 로그파일 그룹이나 멤버를 제거한다.

<a id="262a5ef11c189813"></a>
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

<a id="85327028f7dcfeec"></a>
### 사용 범위 및 접근 권한

&lt;alter database drop logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="9e4443acd3b81bd3"></a>
### 구문 규칙 및 파라미터

<a id="6bbcb875c156c26e"></a>
#### &lt;alter database drop logfile statement&gt;

데이터베이스는 MOUNT 상태여야 한다.   
제거하려는 로그파일이 CURRENT 또는 ACTIVE 상태일 때는 에러가 발생한다.   
제거한 후에 최소 네 개의 로그파일 그룹이 남아 있어야 한다.

<a id="c7f72dd8b8f77b94"></a>
#### &lt;drop logfile group statement&gt;

기존의 로그파일 그룹을 제거한다.

- &lt;group clause&gt; 
    - 제거할 로그파일 그룹을 지정한다.
    - integer는 존재하는 로그파일의 식별자여야 한다. 
    - integer가 존재하지 않을 경우 에러가 발생한다.

<a id="57df76aa02cc84b2"></a>
#### &lt;drop logfile member statement&gt;

기존의 로그파일 멤버들을 제거한다.

- &lt;logfile_list&gt;
    - 제거할 로그파일 멤버의 목록이다.
    - 'logfile_name'은 존재하는 이름이어야 한다. 
    - 'logfile_name'이 존재하지 않을 경우 에러가 발생한다.

<a id="17a936cc74c4186e"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="49278fe93d646b24"></a>
### 사용 예

다음은 기존 로그파일인 GROUP 3을 제거하는 예이다.

```
ALTER DATABASE DROP LOGFILE GROUP 3;
```

다음은 기존 로그파일인 GROUP 3에서 'logfile1.log'와 'logfile2.log'를 제거하는 예이다.

```
ALTER DATABASE DROP LOGFILE MEMBER 'logfile1.log', 'logfile2.log';
```

<a id="707d564eda2ce60f"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="eceb1429fd5da2d0"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#3c10e4add82b29c6)
- [ALTER DATABASE RENAME LOGFILE](#1b93c0c90b2452f9)

<a id="0f4d5cb0f887a9b9"></a>
## ALTER DATABASE MOVE SHARD

<a id="0913d20d4ab0b85b"></a>
### 기능

특정 cluster group의 모든 table들의 shard를 다른 cluster group으로 재배치한다.

<a id="757c45ab07ba50e0"></a>
### 구문

```
<alter database move shard statement> ::=
    ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP src_cluster_group
        TO CLUSTER GROUP dest_cluster_group [ ONLINE | OFFLINE ];
```

<a id="9daffbab91069dcb"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database move shard statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="38b1dee855529c1c"></a>
### 구문 규칙 및 파라미터

<a id="67b91c6640d124a9"></a>
#### src_cluster_group

테이블의 shard를 이동할 cluster group 이다.

<a id="6f97709d27248ac5"></a>
#### dest_cluster_group

테이블의 shard를 이동시킬 target cluster group이다.

<a id="97d81cf946a3f522"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="1a09d30e00917ee2"></a>
### 설명

다음과 같은 구문을 사용하여 cluster member와 cluster group을 추가할 때 table들의 shard는 재배치하지 않는다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#8e2b3a3076fcfb3e)
- [ALTER CLUSTER GROUP name ADD MEMBER](#2aa692a04102ad1a)

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

CLONED 테이블이거나 CLUSTER WIDE로 설정된 테이블을 제외한 모든 테이블들을 위와 같이 수행한다. 특정 테이블의 shard 재배치에 실패하더라도 &lt;alter database move shard statement&gt; 구문은 계속 진행되고 shard 재배치에 성공한 테이블을 rollback 하지 않는다.

따라서 에러에 대해 적절한 조치를 취한 후 &lt;alter database move shard statement&gt; 구문을 다시 수행하면 이미 shard 재배치에 성공한 테이블들은 재배치 대상에 포함되지 않으며, 재배치가 필요한 테이블들의 shard만 재배치한다.

<a id="129100cf90f9950e"></a>
### 사용 예

다음은 &lt;alter database move shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP G1 TO CLUSTER GROUP G2;

Database altered.
```

<a id="6866e341447c4adc"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="3c55fecca08bfedc"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name MOVE SHARD](#9c686a45aebb93a8)
- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#8e2b3a3076fcfb3e)
- [ALTER CLUSTER GROUP name ADD MEMBER](#2aa692a04102ad1a)

<a id="6c69ff257b5bdfeb"></a>
## ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS

<a id="888ef9a448037a41"></a>
### 기능

모든 inactive cluster member들을 offline 상태로 변경한다. 즉, 해당 cluster member들에 대한 shard map을 offline 상태로 변경한다.

<a id="ff7864167772cec8"></a>
### 구문

```
<alter database offline inactive cluster members statement> ::=
    ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS
    ;
```

<a id="098b3a9a9e2d3534"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database offline inactive cluster members statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="fc30ec695d5eb533"></a>
### 구문 규칙 및 파라미터

모든 inactive cluster member들을 offline 상태로 변경한다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

<a id="9fbaade1689c3ce0"></a>
### 설명

&lt;alter database offline inactive members statement&gt; 구문은 모든 inactive cluster member들이 더 이상 cluster system에 포함될 수 없는 경우에 사용하는 것이 바람직하다.

Inactive cluster member가 cluster system에 참여할 수 있으면 [ALTER SYSTEM JOIN DATABASE](#a4c3515652081fcc) 구문을 수행하여 cluster system에 포함시킨다.

Offline 상태로 변경된 cluster member는 join 후에 다음 구문을 사용하여 online 상태로 다시 변경할 수 있다

- [ALTER DATABASE REBALANCE](#be8f993bb3ff62bc)
- [ALTER TABLE name REBALANCE](#1af19281915840f1)

<a id="6fec46ab0bc8fcff"></a>
### 사용 예

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;
```

<a id="4987dae8af1e6c13"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="ec6aa186949e9a02"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER SYSTEM JOIN DATABASE](#a4c3515652081fcc)
- [ALTER DATABASE REBALANCE](#be8f993bb3ff62bc)
- [ALTER TABLE name REBALANCE](#1af19281915840f1)

<a id="be8f993bb3ff62bc"></a>
## ALTER DATABASE REBALANCE

<a id="508aa2b8ea5e5a4b"></a>
### 기능

모든 table들의 shard를 재배치한다.

<a id="41ea115ebcb764dc"></a>
### 구문

```
<alter database rebalance statement> ::=
    ALTER DATABASE REBALANCE [ ONLINE | OFFLINE ];
```

<a id="7114f9bfa53df133"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database rebalance statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="11c2ea093b257fbe"></a>
### 구문 규칙 및 파라미터

<a id="a0d79c2d652c67d1"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="e5b8e7a0a0ab5c52"></a>
### 설명

다음과 같은 구문을 사용하여 cluster member, cluster group을 추가할 때 table들의 shard를 재배치하지 않는다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#8e2b3a3076fcfb3e)
- [ALTER CLUSTER GROUP name ADD MEMBER](#2aa692a04102ad1a)

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

<a id="c765b741955a131d"></a>
### 사용 예

다음은 &lt;alter database rebalance statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE REBALANCE;

Database altered.
```

<a id="b25285349b116ca3"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="e785d33d582a7640"></a>
### 참조

관련 내용은 [ALTER TABLE name REBALANCE](#1af19281915840f1)를 참조한다.

<a id="d31035a48497afcf"></a>
## ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP

<a id="602edfd447628e37"></a>
### 기능

특정 cluster group에 shard가 포함되지 않도록 모든 테이블의 shard를 재배치한다.

<a id="2a30f50ae7b6bc08"></a>
### 구문

```
<alter database rebalance exclude cluster group statement> ::=
    ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP cluster_group_name [ ONLINE | OFFLINE ];
```

<a id="b57b4983b0bac579"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database rebalance exclude cluster group statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="e5ce796501c3a1da"></a>
### 구문 규칙 및 파라미터

<a id="30ec6ded619f571a"></a>
#### cluster_group_name

테이블들의 shard를 포함하지 않는 cluster group의 이름이다.  
지정한 cluster group이 유일한 cluster group인 경우 구문을 수행할 수 없다.

<a id="57c3e7002f3771db"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="8ecc1529b8d5cc9e"></a>
### 설명

[DROP CLUSTER GROUP](19-sql-references-c-g.md#8bcf309cea211dc8) 구문을 사용하여 cluster group을 제거하려면 해당 cluster group에 shard가 존재하지 않아야 한다.

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

<a id="e85418a5ab4cd799"></a>
### 사용 예

다음은 &lt;alter database rebalance exclude cluster group statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP g3;

Database altered.
```

<a id="064fc657bbde6a2f"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="625c8a6a412343d8"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP CLUSTER GROUP](19-sql-references-c-g.md#8bcf309cea211dc8)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#1271c86ed9218a0f)

<a id="c133e118c29e1673"></a>
## ALTER DATABASE RECOVER

<a id="33602c5fa6493a91"></a>
### 기능

온라인/ archive log file을 사용하여 데이터베이스 내의 전체 데이터파일 (datafile) 또는 일부 데이터파일을 복구한다.

<a id="1c18597ffa778de5"></a>
### 구문

```
<alter database recover statement> ::=
      <complete database recover statement>
    | <datafile recover statement>
    | <complete tablespace recover statement>
    | <incomplete database recover statement>
    ;

<complete database recover statement> ::=
    ALTER DATABASE RECOVER

<datafile recover statement> ::=
    ALTER DATABASE RECOVER DATAFILE <datafile recovery clause>

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

<incomplete database recover statement> ::=
      <batch incomplete recovery statement>
    | <interactive incomplete recovery statement>
    ;

<batch incomplete recovery statement> ::=
    ALTER DATABASE RECOVER <until clause> [<using backup controlfile option>]
    
<until clause> ::=
      UNTIL CHANGE integer

<using backup controlfile option> ::=
    USING BACKUP CONTROLFILE

<interactive incomplete recovery statement> ::=
    ALTER DATABASE <incomplete recovery option> [<using backup controlfile option>]

<incomplete recovery option> ::=
      BEGIN INCOMPLETE RECOVERY
    | END INCOMPLETE RECOVERY
    | RECOVER 'logfile name'
    | RECOVER AUTOMATICALLY
    | RECOVER SUGGESTION
    ;
```

<a id="d174ddc0d4d6efe1"></a>
### 사용 범위 및 접근 권한

&lt;alter database recover statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="dac71ffd457a59bb"></a>
### 구문 규칙 및 파라미터

<a id="7924e2d347604a57"></a>
#### &lt;complete database recover statement&gt;

온라인 및 archive 로그파일을 이용하여 데이터베이스의 데이터 파일들을 최신 상태로 복구한다.

- ONLINE 상태의 모든 테이블스페이스를 복구한다. 
- 데이터베이스는 MOUNT 상태여야하고, ARCHIVELOG 모드여야 한다. 
- 필요한 archive log file이 존재하지 않으면 실패한다.

<a id="f0487aa50170a456"></a>
#### &lt;datafile recover statement&gt;

Immediate option으로 offline 된 tablespace의 datafile, backup 된 datafile 또는 backup 도중에 장애가 발생하여 archive logfile을 이용한 복구가 필요한 tablespace의 datafile들을 최신상태로 복구한다.

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

<a id="024c32f670e408a8"></a>
#### &lt;complete tablespace recover statement&gt;

테이블스페이스의 데이터 파일들을 최신 상태로 복구한다.

- 테이블스페이스를 복구하려면 데이터베이스가 MOUNT 또는 OPEN 상태여야 한다. 
- OPEN 상태에서의 복구는 OFFLINE 상태의 테이블스페이스만 가능하고, MOUNT 상태에서의 복구는 ONLINE/ OFFLINE 상태의 테이블스페이스 모두 가능하다. 
- 필요한 archive log file이 존재하지 않으면 복구에 실패한다.
- 다음과 같은 경우에는 테이블스페이스 복구 연산이 필요하다.
    - IMMEDIATE 로 OFFLINE 된 테이블스페이스
    - 백업된 데이터 파일을 이용해야 하는 경우
    - 전체 백업중 장애가 발생한 경우

<a id="f9568a94b119c215"></a>
#### &lt;incomplete database recover statement&gt;

<a id="f88f21bbf0a37ec8"></a>
##### &lt;batch incomplete database recover statement&gt;

온라인 및 archive log file을 이용하여 데이터베이스의 데이터 파일들을 최신상태가 아닌 특정 시점까지 일괄 복구한다.

- ONLINE 상태의 모든 테이블스페이스를 복구한다. 
- 데이터베이스는 MOUNT 상태여야하고, ARCHIVELOG 모드여야 한다. 
- 불완전 복구될 시점 이후의 데이터가 존재하는 데이터 파일을 이용하면 실패한다. 
- 불완전 복구가 완료되면 반드시 RESETLOGS로 데이터베이스를 OPEN 해야 한다. 
- &lt;until clause&gt; 
    - 불완전 복구될 특정 시점이다.
    - UNTIL CHANGE: 로그 단위로 불완전 복구 시점을 지정한다. 
- &lt;using backup controlfile&gt; 
    - Deprecated

<a id="cd8b3b242f4e36f7"></a>
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
- &lt;using backup controlfile&gt; 
    - Deprecated

<a id="9db83315ad5f94c4"></a>
### 설명

데이터베이스 불완전 복구는 복구 완료 시점을 한 번에 찾아내기 어려우므로 여러 번 수행하여 원하는 복구 시점을 찾아야 한다. 그런데 불완전 복구가 완료된 후 RESETLOGS 옵션으로 데이터베이스를 기동하면 새로운 데이터베이스가 되기 때문에 archive log file과 온라인 redo log file에 대한 복사본을 만든 후에 불완전 복구를 여러 번 수행해야 한다.

<a id="0b685366981a50c7"></a>
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

다음은 복구 가능한 archive log file까지만 복구하는 대화식 불완전 복구의 예이다.

```
ALTER DATABASE BEGIN INCOMPLETE RECOVERY;
ALTER DATABASE RECOVER AUTOMATICALLY;
ALTER DATABASE END INCOMPLETE RECOVERY;
```

<a id="42c44325dd78f6f4"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="27388f861ee109aa"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#7c06bf1cb158127b)
- [ALTER TABLESPACE name BACKUP](#9835448e7383ecdf)
- [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#c9672eb1d1318175)

<a id="1645dd1fd6e204dd"></a>
## ALTER DATABASE REGISTER

<a id="e62dd9889c01871a"></a>
### 기능

복구 불가능한 세그먼트를 데이터베이스에 등록한다.

<a id="895d5cc9d829453e"></a>
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

<a id="5ef42252e21900df"></a>
### 사용 범위 및 접근 권한

&lt;alter database register statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="2c93f6965686c663"></a>
### 구문 규칙 및 파라미터

<a id="c85247d2fc763f0d"></a>
#### &lt;alter database register statement&gt;

복구 불가능한 세그먼트를 데이터베이스에 등록한다. 해당 구문은 백업이 존재하지 않고 데이터베이스를 복구할 수 없는 경우, 세그먼트를 더 이상 사용하지 않는다는 가정하에 사용될 수 있다.

- 데이터베이스가 MOUNT 상태여야 한다.
- 등록된 세그먼트 식별자 목록은 재시작할 때 초기화된다.
- 서버 재시작에 성공하면 등록된 세그먼트들이 'UNUSABLE' 상태가 되는데 해당 세그먼트들은 반드시 삭제해야 한다.

<a id="0a5b00314c3f8335"></a>
#### &lt;segment physical identifier list&gt;

복구 불가능한 세그먼트의 식별자 목록이다.  
• Integer: 8 바이트 정수형의 세그먼트 식별자

<a id="d06c754f4ed339aa"></a>
### 설명

서버를 비정상 종료하고 재시작할 때 데이터베이스를 복구하는데, 이 때 이전 서비스 단계에서 디스크에 반영되지 못한 페이지들을 복구하기 위해서 REDO 로그들을 이용해 페이지를 다시 수행한다.

REDO 연산을 수행하는 중에 예상하지 못한 실패가 발생한 경우, 이를 무시하고 복구하기 위해 사용될 수 있다.

<a id="7c41af35f10318c9"></a>
### 사용 예

다음은 4028679323648을 식별자로 갖는 세그먼트 복구를 포기하는 예이다.

```
ALTER DATABASE REGISTER IRRECOVERABLE SEGMENT 4028679323648;
```

<a id="b8aedd2b450eadc0"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="d3265b4e5ac15ff5"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#9835448e7383ecdf)
- [ALTER DATABASE RECOVER](#c133e118c29e1673)

<a id="1b93c0c90b2452f9"></a>
## ALTER DATABASE RENAME LOGFILE

<a id="ed90016377eb30ef"></a>
### 기능

데이터베이스에서 로그파일의 이름을 수정한다.

<a id="ee809643351b1227"></a>
### 구문

```
<alter database rename logfile statement> ::=
    ALTER DATABASE RENAME LOGFILE <logfile_list> TO <logfile_list>
    ;

<logfile_list> ::=
      'logfile_name'
    | <logfile_list> , 'logfile_name'
```

<a id="ba2521cdf7907373"></a>
### 사용 범위 및 접근 권한

&lt;alter database rename logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="46524b0c92a48892"></a>
### 구문 규칙 및 파라미터

<a id="1c2b81266998d53f"></a>
#### &lt;alter database rename logfile statement&gt;

- 데이터베이스는 MOUNT 상태여야 한다.
- FROM &lt;logfile_list&gt;
    - 데이터베이스에서 수정할 로그파일들의 이름 목록이다.
- TO &lt;logfile_list&gt;
    - 데이터베이스에서 수정될 로그파일들의 이름 목록이다.
    - &lt;logfile_list&gt;는 존재하는 파일이어야 한다. 
    - 파일이 존재하지 않을 경우 에러가 발생한다.

<a id="d338efefa5ac0887"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="2568a45a34068c77"></a>
### 사용 예

다음은 기존 로그파일 'logfile.log'를 'newlogfile.log'로 변경하는 예이다.

```
ALTER DATABASE RENAME LOGFILE 'logfile.log' TO 'newlogfile.log';
```

<a id="64cfcedf9f002acd"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="4e8d7773ca163550"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#3c10e4add82b29c6)
- [ALTER DATABASE DROP LOGFILE](#ae139293d7bcd6f4)

<a id="060da0c4f8e4ebb1"></a>
## ALTER DATABASE RESET LOCAL CLUSTER MEMBER

<a id="5d362e6f33592778"></a>
### 기능

Local cluster member에서 tablespace 객체를 제외한 부분을 database 생성 시점으로 초기화한다.

<a id="349baf4c1a3cace1"></a>
### 구문

```
<alter database reset local cluster member statement> ::=
    ALTER DATABASE RESET LOCAL CLUSTER MEMBER
    ;
```

<a id="9ed3f8b16aa085ba"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

Start-up 과정 중 LOCAL OPEN 단계에서 수행할 수 있다.

&lt;alter database reset local cluster member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="44a1263de49eed6f"></a>
### 설명

Local cluster member에서 tablespace 객체를 제외한 부분을 database 생성 시점으로 초기화한다.  
Tablespace 객체를 제외하고 사용자가 생성한 모든 객체를 제거한다.

&lt;alter database reset local cluster member statement&gt; 구문은 inactive cluster member를 초기화하고,  
새로운 cluster member를 cluster system에 참여시키기 위해 사용한다.  
Cluster system과 연결이 끊긴 inactive cluster member들은 다음과 같이 처리할 수 있다.

- Cluster system에 다시 참여할 수 있는 경우, JOIN 구문을 이용하여 참여시킨다. 
    - [ALTER SYSTEM JOIN DATABASE](#a4c3515652081fcc) 
- Cluster system에 다시 참여할 수 없는 경우, DROP 구문을 이용하여 cluster system에서 제외한다. 
    - [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#4097c0f933c6e040)

이 때, cluster system에서 제외된 cluster member에 해당하는 장비는 다음 두 가지 방법으로 재사용할 수 있다.

- 방법 1: Local cluster member의 database를 다시 생성한다.
- 방법 2: &lt;alter database reset local cluster member statement&gt; 구문을 이용해 local cluster member를 초기화한다.

방법 2는 방법 1보다 tablespace를 재생성하는 비용을 줄일 수 있다.

<a id="840ff031368a5308"></a>
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

<a id="2d7407c5ca52362f"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="f403a5b9d5627029"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER SYSTEM JOIN DATABASE](#a4c3515652081fcc)
- [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#4097c0f933c6e040)

<a id="3653f51ee6300690"></a>
## ALTER DATABASE RESTORE

<a id="cd423df2f35d3012"></a>
### 기능

증분 백업을 이용하여 데이터베이스 또는 테이블스페이스 내의 데이터 파일들을 복원한다.

<a id="74cd0265ac2050eb"></a>
### 구문

```
<alter database restore statement> ::=
      <database restore statement>
    | <tablespace restore statement>
    | <controlfile restore statement>
    ;

<database restore statement> ::=
    ALTER DATABASE RESTORE [ <until clause> ]

<until clause> ::=
    UNTIL CHANGE integer

<tablespace restore statement> ::=
    ALTER DATABASE RESTORE TABLESPACE tablespace_name

<controlfile restore statement> ::=
    ALTER DATABASE RESTORE CONTROLFILE FROM 'file_name'
```

<a id="11b9c7bf75a916a8"></a>
### 사용 범위 및 접근 권한

alter database restore statement> 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="88e15cc824a81ab8"></a>
### 구문 규칙 및 파라미터

<a id="9d63463eabed6608"></a>
#### &lt;database restore statement&gt;

증분 백업을 사용하여 데이터베이스 내의 데이터 파일들을 복원한다.   
데이터베이스가 MOUNT 상태여야 한다.

<a id="a09d02212a594963"></a>
#### &lt;tablespace restore statement&gt;

증분 백업을 사용하여 테이블스페이스 내의 데이터 파일들을 복원한다.

- 데이터베이스가 MOUNT 또는 OPEN 상태여야 한다. 
- OPEN 상태에서는 OFFLINE 상태의 테이블스페이스만 복원할 수 있고, MOUNT 상태에서는 ONLINE/ OFFLINE 상태의 테이블스페이스 모두 복원할 수 있다.

<a id="bf2459cf267d506f"></a>
#### &lt;controlfile restore statement&gt;

'file_name'을 사용하여 제어파일을 복원한다.

- 데이터베이스가 NOMOUNT 상태여야 한다.
- 'file_name'은 절대 경로를 권장하지만, 만약 상대 경로를 기술한 경우에는 &lt;GOLDILOCKS_HOME&gt;/wal/'file_name'을 이용한다.

<a id="4d5a8a8b18d15b9f"></a>
### 설명

전체 백업을 이용한 데이터 파일 복원은 OS 복사 명령으로 백업된 파일을 직접 데이터 파일 경로에 복사하는 방법이다. 증분 백업을 이용한 데이터 파일 복원은 삭제된 데이터 파일이나 이전 데이터 파일들만 복원한다.

<a id="67704d39da46fcbb"></a>
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

<a id="cc7aeabc5ee6fe7b"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="3ec13e41c3d0d87d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#7c06bf1cb158127b)
- [ALTER TABLESPACE name BACKUP](#9835448e7383ecdf)
- [ALTER DATABASE RECOVER](#c133e118c29e1673)

<a id="ab87dcfc878756dd"></a>
## ALTER INDEX

<a id="257861ece0e6ebdc"></a>
### 기능

인덱스 정의를 변경한다.

<a id="14d9baba913e6690"></a>
### 구문

```
<alter index statement> ::=
      <alter index physical attribute statement>
    | <rename index statement>
    | <aging index statement>
    | <rebuild statement>
    ;
```

<a id="fae84d757112eea5"></a>
### 사용 범위 및 접근 권한

&lt;alter index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="21c1052f6fc2290f"></a>
### 구문 규칙 및 파라미터

<a id="7b15f0ad25c592ea"></a>
#### &lt;alter index physical attribute statement&gt;

인덱스의 물리적 속성을 변경한다.  
자세한 내용은 [ALTER INDEX name STORAGE](#4d98b3e2468854ef) 구문을 참조한다.

<a id="442b5a201f0a53a5"></a>
#### &lt;rename index statement&gt;

인덱스 이름을 변경한다.  
자세한 내용은 [ALTER INDEX name RENAME TO](#f0f556a04ad6636a) 구문을 참조한다.

<a id="99f2802e0a70e982"></a>
#### &lt;aging statement&gt;

인덱스의 빈 페이지를 삭제한다.  
자세한 내용은 [ALTER INDEX name AGING](#6f2c01509684f641) 구문을 참조한다.

<a id="d11b9551f546a241"></a>
#### &lt;rebuild statement&gt;

인덱스를 재구축한다.  
자세한 내용은 [ALTER INDEX name REBUILD](#a53bb774e5265424) 구문을 참조한다.

<a id="9e111e4ddc91dca7"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="1d368d93cf8e7017"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="2dd0a3b005d64966"></a>
### 호환성

SQL 표준에서는 인덱스에 대한 개념을 다루지 않고 있다.

<a id="6f2c01509684f641"></a>
## ALTER INDEX name AGING

<a id="97d15217e8cf474a"></a>
### 기능

인덱스의 빈 페이지를 삭제한다.

<a id="4cc5419e231e6521"></a>
### 구문

```
<aging index statement> ::=
    ALTER INDEX index_name AGING
    ;
```

<a id="497790305db975d3"></a>
### 사용 범위 및 접근 권한

&lt;aging index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="38b5b0f212318b60"></a>
### 구문 규칙 및 파라미터

<a id="0c750fbd91a1e275"></a>
#### index_name

대상 인덱스의 이름이다.

<a id="c94f149e8ce4648f"></a>
### 설명

해당 구문은 인덱스 페이지들 중에 모든 키가 삭제된 페이지들을 세그먼트로 반납한다. Aging은 논리적 삭제와 물리적 삭제의 2단계로 진행된다. 논리적 삭제는 인덱스에서 페이지를 지칭하는 연결을 끊는 작업이며 페이지의 마지막 키를 삭제할 당시의 SCN이 시스템의 agable SCN보다 작을 때 수행된다. 이후 물리적 삭제가 이루어지는데 논리적으로 삭제할 때의 SCN이 시스템의 agable SCN보다 작을 때 수행된다.

> 만약 시스템의 agable SCN이 증가하지 않으면 인덱스 AGING 구문이 성공하더라도 빈 페이지가 삭제되지 않을 수 있다.

<a id="e2a4107e82ee26a9"></a>
### 사용 예

다음은 인덱스를 aging하는 예이다.

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

<a id="bea00c8b0a0f3e34"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="2cb44c7829d96e43"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](19-sql-references-c-g.md#8e0637af857026b6)
- [ALTER INDEX](#ab87dcfc878756dd)
- [DROP INDEX](19-sql-references-c-g.md#f6216a28e7e3e011)

<a id="a53bb774e5265424"></a>
## ALTER INDEX name REBUILD

<a id="5e9ae7428d70fafb"></a>
### 기능

인덱스를 재구축한다.

<a id="8a62a03a2c69c5a1"></a>
### 구문

```
<rebuild index statement> ::=
    ALTER INDEX index_name REBUILD
        [ ONLINE | OFFLINE ]
        [ <index attributes> [...] ]
        [ TABLESPACE tablespace_name ]
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
    | MINSIZE <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="85e30b518764a085"></a>
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

<a id="16b09ccfc575d8d8"></a>
### 구문 규칙 및 파라미터

<a id="0e30125731a3448e"></a>
#### index_name

대상 인덱스의 이름이다.  
스키마 이름을 명시할 수 있으며, 생략할 경우 사용자의 기본 스키마 이름이 사용된다.

<a id="3b12b72111ca6236"></a>
#### [ ONLINE | OFFLINE ]

인덱스를 재구축할 때, 해당 테이블에 DML을 허용할지 여부를 결정한다.

- ONLINE
    - INSERT, UPDATE, DELETE를 허용한다.
- OFFLINE
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE이다.

<a id="fc0360429f11a3df"></a>
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

<a id="90f0fcc96e98a94f"></a>
#### &lt;segment attr clause&gt;

인덱스가 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer
    - 정의
        - 인덱스를 생성할 때 초기에 할당할 물리적 공간의 크기를 기술한다.
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT 크기가 8192 bytes일 경우 'INITIAL 100'은 실제 8192 bytes로 작동한다.)
        - 이 크기 (TABLESPACE의 EXTENT 크기에 align 된 크기)는 MINEXTENTS의 크기와 같거나 커야 하며, MAXEXTENTS의 크기와 같거나 작아야 한다.
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

- MINSIZE integer
    - 정의
        - 인덱스에서 유지해야 할 최소 공간의 크기이다.
        - 이 값은 MAXSIZE의 값과 같거나 작아야 한다.
    - 이 크기는 인덱스가 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - EXTENT 두 개 크기보다 작을 경우 EXTENT 두 개 크기로 결정된다.
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

- MAXSIZE integer
    - 정의
        - 인덱스에서 할당받을 수 있는 최대 공간의 크기이다.
        - 이 값은 MINSIZE의 값과 같거나 커야 한다.
    - 이 크기는 인덱스가 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

<a id="b397b33b58365019"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="d1a098e7bc7d9a8e"></a>
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

<a id="3fe0a5adf67c2684"></a>
#### TABLESPACE tablespace_name

인덱스가 재구축될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - tablespace_name이 data tablespace면 LOGGING 인덱스로 재구축된다.
    - tablespace_name이 temporary tablespace 또는 nologging tablespace면 NOLOGGING 인덱스로 재구축된다.
- TABLESPACE 절을 생략할 경우, 기존 인덱스의 tablespace로 설정된다.

<a id="abb0d617091afe47"></a>
### 설명

- 인덱스 단편화 제거
    - 인덱스에 DML이 빈번하게 수행되는 경우, 인덱스 페이지에 단편화가 발생할 수 있다. 유효한 데이터에 비해 트리가 지나치게 커진 경우, 인덱스 용량은 커지고 성능은 하락한다. 이 경우 인덱스를 재구축하면 인덱스 페이지의 단편화를 해결하여 인덱스 용량을 줄이고 인덱스의 성능을 회복할 수 있다.
- 인덱스의 테이블스페이스 변경
    - 기존에 생성된 인덱스의 테이블스페이스를 변경할 수 있다.
    - 단, 테이블스페이스의 TEMPORARY 여부에 따라 로깅 여부를 적절하게 설정해주어야 한다.
- 인덱스의 로깅 설정 변경
    - LOGGING 인덱스로 변경하려면, data tablespace를 TABLESPACE 옵션에 지정해줘야 한다.
    - NOLOGGING 인덱스로 변경하려면, temporary tablespace 또는 nologging tablespace를 TABLESPACE 옵션에 지정해줘야 한다.

<a id="ad17c478a9c6a47b"></a>
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

<a id="69ec22742a90acb2"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="13f7d1a9b02d87e3"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](19-sql-references-c-g.md#8e0637af857026b6)
- [ALTER INDEX](#ab87dcfc878756dd)
- [DROP INDEX](19-sql-references-c-g.md#f6216a28e7e3e011)

<a id="f0f556a04ad6636a"></a>
## ALTER INDEX name RENAME TO

<a id="1d3b2fa2be5d0e28"></a>
### 기능

인덱스의 이름을 변경한다.

<a id="b1946406bf370d39"></a>
### 구문

```
<rename index statement> ::=
    ALTER INDEX index_name
        RENAME TO new_index_name
    ;
```

<a id="d5701bc4c5146359"></a>
### 사용 범위 및 접근 권한

&lt;rename index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="1448f163494bcbe4"></a>
### 구문 규칙 및 파라미터

<a id="d26fbdc51418819c"></a>
#### index_name

대상 인덱스의 이름이다.  
스키마 이름을 기술할 수 없으며, 기존 인덱스와 동일한 스키마 이름을 갖는다.

<a id="9b74f799463aa4e1"></a>
#### new_index_name

새로운 인덱스의 이름이며 스키마 내에서 유일한 인덱스 이름이어야 한다.

<a id="d5a8afabe4d57d9d"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="48983ac5122a43cc"></a>
### 사용 예

다음은 인덱스의 이름을 변경하는 예이다.

```
gSQL> ALTER INDEX t1_idx1 RENAME TO idx_t1_id;

Index altered.
```

<a id="c5deae731dc88d97"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="0c234b83bae04544"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](19-sql-references-c-g.md#8e0637af857026b6)
- [ALTER INDEX](#ab87dcfc878756dd)
- [DROP INDEX](19-sql-references-c-g.md#f6216a28e7e3e011)

<a id="4d98b3e2468854ef"></a>
## ALTER INDEX name STORAGE

<a id="8416b858c2fc9afc"></a>
### 기능

인덱스의 물리적 속성을 변경한다.

<a id="38205da918636bb2"></a>
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
    | MINSIZE <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]
```

<a id="076fbb096ee3234c"></a>
### 사용 범위 및 접근 권한

&lt;alter index physical attribute statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="275170bef1e6eca3"></a>
### 구문 규칙 및 파라미터

<a id="e7c6807e50fbd375"></a>
#### index_name

대상 인덱스의 이름이다.

<a id="b307817577fb9959"></a>
#### &lt;physical attribute clause&gt;

인덱스의 물리적 속성 정보를 정의한다.

- PCTFREE integer 
    - 정의 
        - 페이지 내에 key 삽입으로 인한 페이지 분할 빈도를 조절하기 위해 예약된 공간이다. 
        - 인덱스 bottom-up 빌드 시에만 적용된다. 
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

<a id="167b2975dc30e446"></a>
#### &lt;segment attr clause&gt;

인덱스가 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer 
    - 정의 
        - 인덱스를 생성할 때 초기에 할당할 물리적 공간의 크기를 기술한다. 
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT 크기가 8192 bytes일 경우 'INITIAL 100'은 실제 8192 bytes로 동작한다.) 
        - 이 크기 (TABLESPACE의 EXTENT 크기에 align 된 크기)는 MINEXTENTS의 크기와 같거나 커야 하며, MAXEXTENTS의 크기와 같거나 작아야 한다. 
        - 인덱스 bottom-up 빌드 시에만 적용된다. 
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

- MINSIZE integer 
    - 정의 
        - 인덱스에서 유지해야할 최소 공간의 크기이다. 
        - 이 값은 MAXSIZE의 값과 같거나 작아야 한다. 
    - 이 크기는 인덱스가 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. 
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다. 
    - EXTENT 두 개 크기보다 작을 경우 EXTENT 두 개 크기로 결정된다.

- MAXSIZE integer 
    - 정의 
        - 인덱스에서 할당받을 수 있는 최대 공간의 크기이다. 
        - 이 값은 MINSIZE의 값과 같거나 커야 한다. 
    - 이 크기는 인덱스가 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. 
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다. 
    - 생략할 경우, 기본값은 EXTENT 크기 * 2147483647 (INT32의 최대 양의 정수)이다.

<a id="23750eba4e41f010"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: kilobytes 
- M: megabytes 
- G: gigabytes 
- T: terabytes

<a id="1fe3904f2b49bfb6"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="7ca9b1183ee2f734"></a>
### 사용 예

다음은 인덱스의 물리적 속성을 변경하는 예이다.

```
gSQL> ALTER INDEX idx_t1_id PCTFREE 10 INITRANS 4 MAXTRANS 8;

Index altered.
```

<a id="d48a8195697d0d3d"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="57d7a46886f98e07"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](19-sql-references-c-g.md#8e0637af857026b6)
- [ALTER INDEX](#ab87dcfc878756dd)
- [DROP INDEX](19-sql-references-c-g.md#f6216a28e7e3e011)

<a id="e94dd9982f8bc8d7"></a>
## ALTER PROFILE

<a id="a4fc286002b3ce83"></a>
### 기능

비밀번호 관리 방법을 변경한다.

<a id="dd929b22f1dfc505"></a>
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

<a id="07bcd81472869169"></a>
### 사용 범위 및 접근 권한

&lt;alter profile statement&gt; 구문을 수행하려면 사용자에게 ALTER PROFILE ON DATABASE 권한이 있어야 한다.

<a id="5d36ff9be87733aa"></a>
### 구문 규칙 및 파라미터

<a id="1346c5e0b400e7d6"></a>
#### profile_name

변경할 profile의 이름이다.

<a id="1c87760044613f6b"></a>
#### FAILED_LOGIN_ATTEMPTS

로그인 연속 실패 허용 횟수를 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#f421f468f014cc7b) 구문을 참조한다.

<a id="4eb164380835cac8"></a>
#### PASSWORD_LOCK_TIME

로그인에 연속적으로 실패한 후에 계정이 잠기는 기간 (day)을 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#f421f468f014cc7b) 구문을 참조한다.

<a id="8dcc7d6cbb90ecdd"></a>
#### PASSWORD_LIFE_TIME

비밀번호의 유효 기간 (day)을 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#f421f468f014cc7b) 구문을 참조한다.

<a id="9b7adba7a1706377"></a>
#### PASSWORD_GRACE_TIME

PASSWORD_LIFE_TIME 이후에 로그인 할 때 비밀번호 만료를 유예하는 기간을 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#f421f468f014cc7b) 구문을 참조한다.

<a id="d134b68246107e5f"></a>
#### PASSWORD_REUSE_MAX

이전 비밀번호를 재사용하려 할 때 재사용할 수 없는 최근 비밀번호 개수를 명시한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#f421f468f014cc7b) 구문을 참조한다.

<a id="ba298c1c0aa51bba"></a>
#### PASSWORD_REUSE_TIME

이전 비밀번호를 재사용하기 위해 필요한 경과 기간을 명시한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#f421f468f014cc7b) 구문을 참조한다.

<a id="ef6cec3175c4e703"></a>
#### PASSWORD_VERIFY_FUNCTION

비밀번호 복잡도 검증 방법을 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#f421f468f014cc7b) 구문을 참조한다.

<a id="68892eebcf5888c7"></a>
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

<a id="f9bb6a5cbb5ae046"></a>
### 호환성

SQL 표준은 profile에 대한 개념을 다루지 않고 있다.

<a id="2f4fb3e9c87e3309"></a>
### 참조

관련 내용은 [DROP PROFILE](19-sql-references-c-g.md#4a92f0bfc9e51c58)을 참조한다.

<a id="3df2c32d366ffd24"></a>
## ALTER SEQUENCE

<a id="eb344ac57b49ec62"></a>
### 기능

시퀀스를 변경한다.

<a id="0a4ee6e5a658efc5"></a>
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

<a id="518179e4a58a6e3a"></a>
### 사용 범위 및 접근 권한

&lt;alter sequence generator statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 시퀀스의 소유자 
- 시퀀스가 속한 스키마에 대해 (ALTER SEQUENCE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY SEQUENCE ON DATABASE

<a id="63820d923bb3053a"></a>
### 구문 규칙 및 파라미터

<a id="e8ffd8ebf5a99bc0"></a>
#### sequence_name

변경할 시퀀스의 이름이다.  
schema_name.sequence_name과 같이 시퀀스가 속할 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="64922dce03434d29"></a>
#### &lt;alter sequence generator restart option&gt;

시퀀스의 다음 값 (NEXT VALUE)을 설정한다.  
단, [CREATE SEQUENCE](19-sql-references-c-g.md#0466abe24a740737) 구문에서 정의한 START WITH의 값은 변경하지 않는다.

- RESTART 
    - 값을 명시하지 않을 경우, &lt;sequence generator definition&gt; 에서 정의한 START WITH의 값이 시퀀스의 다음 값으로 설정된다. 
- RESTART WITH integer 
    - integer 값을 시퀀스의 다음 값으로 설정한다. 
    - integer 값은 MINVALUE와 MAXVALUE 사이의 값이어야 한다.

&lt;alter sequence generator restart option&gt; 절을 명시하지 않은 경우, 시퀀스의 현재값을 기준으로 시퀀스의 속성을 변경한다.

<a id="10e72beb3cd72191"></a>
#### &lt;sequence generator increment by option&gt;

시퀀스 번호의 간격을 변경한다.  
다음과 같은 제약과 특징을 갖는다.

- 양수 또는 음수를 사용할 수 있으며, 0은 사용할 수 없다. 
- 간격의 절대값은 MINVALUE와 MAXVALUE의 차이보다 작아야 한다. 
- 양수일 경우 오름차순 시퀀스가 되고 음수일 경우 내림차순 시퀀스가 된다.

<a id="abf9a71a63c57c88"></a>
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

<a id="7bd2ed948b6f6a4f"></a>
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

<a id="4b5b28257806ac99"></a>
#### &lt;sequence generator cycle option&gt;

시퀀스의 값이 최대값 또는 최소값이 되었을 때, 계속 값을 생성할지 여부를 변경한다.

- CYCLE 
    - 오름차순 시퀀스가 최대값이 되었을 때, 최소값부터 다시 생성한다. 
    - 내림차순 시퀀스가 최소값이 되었을 때, 최대값부터 다시 생성한다. 
- NO CYCLE | NOCYCLE 
    - 최대값 또는 최소값이 되었을 때, 시퀀스 값을 생성할 수 없다. 
    - NO CYCLE (SQL 표준)과 NOCYCLE은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다.

<a id="b51d72741b798178"></a>
#### &lt;sequence generator cache option&gt;

시퀀스에 신속하게 접근하기 위해 메모리상에 미리 적재할 시퀀스 값의 개수를 정의한다.   
Database를 재구동할 때, 메모리상에 적재한 시퀀스 값은 유실되고 적재한 이후의 값부터 시작된다.

- CACHE integer 
    - CACHE 값은 2와 같거나 커야하고 
    - CYCLE이 존재할 경우 CACHE 값이 CYCLE의 길이보다 크지 않아야 한다. 
        - CYCLE의 길이: CEIL(MAXVALUE - MINVALUE) / ABS(INCREMENT) 
- NO CACHE | NOCACHE 
    - 메모리 상에 시퀀스값을 미리 적재하지 않는다.

<a id="885c04fb0231a592"></a>
### 설명

[CREATE SEQUENCE](19-sql-references-c-g.md#0466abe24a740737) 구문에서 정의한 시퀀스 속성 중 START WITH는 변경할 수 없다.  
START WITH 속성을 변경하려면 [DROP SEQUENCE](19-sql-references-c-g.md#4693b77a7e62cf8a) 구문을 수행한 후에 [CREATE SEQUENCE](19-sql-references-c-g.md#0466abe24a740737) 구문을 사용하여 다시 생성해야 한다.

<a id="fb42566e8001b13a"></a>
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

<a id="8727ac06800b779e"></a>
### 호환성

SQL 표준에서는 CACHE/ NO CACHE 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="a19a3d78928d9ff0"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T176 | Sequence generator support | O |
| T177 | Sequence generator support: simple restart option | O |

<a id="c18d496381ef1c11"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE SEQUENCE](19-sql-references-c-g.md#0466abe24a740737)
- [DROP SEQUENCE](19-sql-references-c-g.md#4693b77a7e62cf8a)

<a id="1972e723d30330e8"></a>
## ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

<a id="3a4de6fac1a23eda"></a>
### 기능

세션에서 재사용하기 위해 catching 된 모든 공간들을 해당 tablespace로 반환한다.

<a id="7ecd60e4d350d686"></a>
### 구문

```
<alter session cleanup global temporary segment pool statement> ::=
    ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL
    ;
```

<a id="1ef92212aaec5faf"></a>
### 설명

수행된 세션에서 segment cache의 segment들만 cleanup한다.

<a id="32c79636821d3ee1"></a>
### 사용 예

다음은 세션 segment cache를 cleanup하는 예이다.

```
gSQL> ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

Session altered.
```

<a id="28499d17bad0ff8c"></a>
### 호환성

SQL 표준에서는 global temporary table, global temporary index의 segment cache 개념을 정의하지 않고 있다.

<a id="e2dfeacefaaf4171"></a>
### 참조

관련 내용은 [Global Temporary Table](13-sql-objects.md#c509ee8f36dcf11f) 을 참조한다.

<a id="a0d698a8bdefa8ba"></a>
## ALTER SESSION SET property_name

<a id="206d9d788a39084f"></a>
### 기능

세션의 프로퍼티 값을 설정한다.

<a id="c04cc552323ed351"></a>
### 구문

```
<alter session set statement> ::=
    ALTER SESSION SET <property name> { = <property value> | TO DEFAULT }
    ;
```

<a id="dd1514d26dcd372a"></a>
### 구문 규칙 및 파라미터

<a id="2caa905b16cd02fe"></a>
#### &lt;property name&gt;

설정할 프로퍼티 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#4752291cb768d51a) 장을 참조한다.

<a id="3de131acf21bca87"></a>
#### &lt;property value&gt;

설정할 프로퍼티 값이다.

<a id="410baada1d67a5af"></a>
#### TO DEFAULT

세션 프로퍼티 값을 시스템 프로퍼티 값으로 설정한다.

<a id="313b0bc75923eb03"></a>
### 설명

각 property에 대한 자세한 설명은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#4752291cb768d51a) 장을 참조한다.

<a id="6372c0418ea33ac7"></a>
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

<a id="2568e335b5cef52c"></a>
### 호환성

SQL 표준에서는 세션 프로퍼티 개념을 정의하지 않고 있다.

<a id="d2f4c7d67b326bb3"></a>
### 참조

관련 내용은 [ALTER SESSION SET property_name](#a0d698a8bdefa8ba) 을 참조한다.

<a id="4c7e15d7de148473"></a>
## ALTER SYSTEM CHECKPOINT

<a id="8e1ddefaf90c355f"></a>
### 기능

CHECKPOINT를 수행한다.

<a id="a101633c3c864618"></a>
### 구문

```
<alter system checkpoint statement> ::=
    ALTER SYSTEM CHECKPOINT
    [ AT <domain name> ]
    ;
```

<a id="7520091d01cec148"></a>
### 사용 범위 및 접근 권한

&lt;alter system checkpoint statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="78b04e24ce435efc"></a>
### 구문 규칙 및 파라미터

<a id="0ed77c1163c41329"></a>
#### &lt;alter system checkpoint statement&gt;

CHECKPOINT는 commit 된 트랜잭션들이 변경한 모든 데이터가 디스크에 기록되는 것을 보장하는 연산이다.

- 데이터베이스가 OPEN 상태여야 한다.
- 데이터베이스가 TDS 모드여야 한다.
- 전체 백업이 진행중일 때는 변경된 페이지가 데이터 파일에 기록되지 않고, REDO 로그와 제어파일만 디스크에 기록된다. 만약 이러한 상태에서 서버가 비정상 종료되는 경우에는 미디어 복구를 수행해야 한다.

<a id="b51b5414dbd1b182"></a>
#### &lt;domain name&gt;

- 구문을 수행할 멤버나 그룹의 이름이다.
- 지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="f7baa31a5b99db23"></a>
### 설명

체크포인트 (checkpoint) 연산은 commit 된 트랜잭션들이 변경한 모든 내용을 디스크에 기록함으로써 시스템 장애시 신속한 복구를 가능하게 한다.

<a id="c9e344c105f02253"></a>
### 사용 예

다음은 CHECKPOINT를 수행하는 예이다.

```
ALTER SYSTEM CHECKPOINT;
```

<a id="c0b66a467a41fd79"></a>
### 호환성

SQL 표준에서는 CHECKPOINT 개념을 정의하지 않고 있다.

<a id="310c12736fe8c7ec"></a>
## ALTER SYSTEM CLEANUP BUFFER_CACHE

<a id="003bcfa6a257aba7"></a>
### 기능

Buffer cache에서 free 가능한 모든 buffer page들을 비운다.

<a id="7ffac65dea57f92e"></a>
### 구문

```
<alter system cleanup buffer_cache statement> ::=
    ALTER SYSTEM CLEANUP BUFFER_CACHE
    [ AT <domain name> ]
    ;
```

<a id="d0175da9aee9eb75"></a>
### 사용 범위 및 접근 권한

&lt;alter system cleanup buffer_cache statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="e74b9700bdae8b07"></a>
### 구문 규칙 및 파라미터

<a id="ccadc61f16e319a2"></a>
#### &lt;alter system cleanup buffer_cache statement&gt;

해당 구문 규칙이나 파라미터가 존재하지 않는다.

<a id="06115e72298e97e5"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="4c33b84f74aef66d"></a>
### 설명

Buffer에 캐시된 free 가능한 모든 buffer page들을 flush하고 free 한다.

> 성능 측정 전에 buffer cache를 비우는 목적으로 사용해야 한다.   
> 운영 중인 서버에서 사용할 경우 성능에 치명적인 영향을 미칠 수 있다.

<a id="1213d83706c7814d"></a>
### 사용 예

다음은 CLEANUP BUFFER_CACHE을 수행하는 예이다.

```
ALTER SYSTEM CLEANUP BUFFER_CACHE;
```

<a id="5e26e1a84c2ed71a"></a>
### 호환성

SQL 표준에서는 CLEANUP BUFFER_CACHE의 개념을 정의하지 않고 있다.

<a id="854a34cd9f7c0148"></a>
## ALTER SYSTEM CLEANUP PLAN

<a id="8a131c62b5931951"></a>
### 기능

모든 SQL plan을 정리한다.

<a id="05c81361bcddc089"></a>
### 구문

```
<alter system cleanup plan statement> ::=
    ALTER SYSTEM CLEANUP PLAN
    [ AT <domain name> ]
    ;
```

<a id="a45a97cf24ebc969"></a>
### 사용 범위 및 접근 권한

&lt;alter system cleanup plan statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="115ef21664813690"></a>
### 구문 규칙 및 파라미터

<a id="6156341f3b9abcd1"></a>
#### &lt;alter system cleanup plan statement&gt;

해당 구문 규칙이나 파라미터가 존재하지 않는다.

<a id="6dfa4edd8efa021e"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="ab0f161b754fc226"></a>
### 설명

캐시되어 있는 모든 SQL plan을 정리한다.   
단, V$SQL_CACHE.REF_COUNT가 0보다 큰 plan (prepare된 statement에서 참조하는 plan)들은 정리 대상에서 제외한다.

<a id="7cd640eb35bb23ba"></a>
### 사용 예

다음은 CLEANUP PLAN을 수행하는 예이다.

```
ALTER SYSTEM CLEANUP PLAN;
```

<a id="c0b112b53df4eee4"></a>
### 호환성

SQL 표준에서는 CLEANUP PLAN의 개념을 정의하지 않고 있다.

<a id="8f040f2958739eba"></a>
## ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER

<a id="3f264fb4e08c6be8"></a>
### 기능

복구 불가능한 클러스터 멤버를 지정한다.

<a id="d1b8c21c82d830ab"></a>
### 구문

```
<alter system irrecoverable cluster member statement> ::=
    ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER <domain name>
    ;
```

<a id="4c9ca959e7abb5a7"></a>
### 사용 범위 및 접근 권한

&lt;alter system irrecoverable cluster member statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="8b5a723de1b008ec"></a>
### 구문 규칙 및 파라미터

<a id="e755bcb67448dd71"></a>
#### &lt;alter system irrecoverable cluster member statement&gt;

해당 구문 규칙이나 파라미터가 존재하지 않는다.

<a id="75b5db7789ce6e39"></a>
#### &lt;domain name&gt;

복구 불가능한 멤버 이름이다.  
그룹 내의 모든 멤버들을 복구 불가한 멤버로 지정할 수 없다.

<a id="929d214c6bbfd5bb"></a>
### 설명

복구 불가능한 멤버로 인해 클러스터 재시작에 실패하는 경우 해당 멤버를 제외하고 시스템을 재시작하기 위해 사용한다. 시스템 재시작에 성공한 후에는 반드시 [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#4097c0f933c6e040) 구문을 이용해 해당 멤버를 삭제해야 한다.

<a id="6cad5b26e0ae280c"></a>
### 사용 예

다음은 IRRECOVERABLE CLUSTER MEMBER를 수행하는 예이다.

```
gSQL> ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER g1n1;
```

<a id="20f71eef219fcc76"></a>
### 호환성

SQL 표준에서는 IRRECOVERABLE CLUSTER MEMBER의 개념을 정의하지 않고 있다.

<a id="a4c3515652081fcc"></a>
## ALTER SYSTEM JOIN DATABASE

<a id="2c948bf9b95f2824"></a>
### 기능

비활성화된 특정 cluster member를 cluster system에 다시 포함한다.

<a id="ff2d5040b216014e"></a>
### 구문

```
<alter system join database statement> ::=
    ALTER SYSTEM JOIN DATABASE 
    ;
```

<a id="44be6ca3cfccadd5"></a>
### 사용 범위 및 접근 권한

Cluster system 에서 수행할 수 있다.

&lt;alter system join database statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="31da67cb29369705"></a>
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

&lt;alter database drop inactive cluster member statement&gt; 구문을 수행하면 모든 inactive cluster member가 cluster system에서 제거되므로, DROP 하기 전에 참여 가능한 모든 inactive cluster member 를 cluster system에 포함시켜야 한다.

<a id="a8c960459e07b4d2"></a>
### 사용 예

```
gSQL> ALTER SYSTEM JOIN DATABASE;
```

<a id="2a1559344e81e8af"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="2f5e9c6311c00118"></a>
### 참조

관련 내용은 [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#4097c0f933c6e040)를 참조한다.

<a id="afb0ef77e1e6af85"></a>
## ALTER SYSTEM [KILL | DISCONNECT] SESSION

<a id="8952d17cb54da432"></a>
### 기능

세션을 종료한다.

<a id="9a0668164f822bb6"></a>
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

<a id="0a6be6e72b723234"></a>
### 사용 범위 및 접근 권한

&lt;alter system end session statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="f1c8ecc5dad0a249"></a>
### 구문 규칙 및 파라미터

<a id="47349d7df337592f"></a>
#### &lt;member_position&gt;

Cluster 환경에서 disconnect/ kill 대상이 되는 세션의 member position 이다.

<a id="77a46e5fc1253aba"></a>
#### &lt;session_id&gt;

세션의 ID 이다.

<a id="00dac386f5caae62"></a>
#### &lt;serial#&gt;

세션의 SERIAL NUMBER 이다.

<a id="63bff0b2fea51aa1"></a>
#### &lt;disconnect_option&gt;

- POST_TRANSACTION: 트랜잭션 완료 후, 세션을 종료한다.
- IMMEDIATE: 트랜잭션 완료를 기다리지 않고 바로 세션을 종료한다.

&lt;disconnect_option&gt;이 사용되지 않으면 IMMEDIATE로 동작한다.

<a id="891462cf902d0dbb"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="b14e0b2894e02840"></a>
### 설명

DISCONNECT SESSION은 POST_TRANSACTION과 IMMEDIATE 옵션을 지정할 수 있으며, POST_TRANSACTION은 현재 실행되는 트랜잭션이 있을 경우 트랜잭션이 끝난 후에 세션을 종료한다. IMMEDIATE는 현재 수행 중인 트랜잭션을 바로 정리한 후에 세션을 종료한다.

KILL SESSION은 해당 세션의 프로세스는 존재하지 않지만, 시스템에 남아있는 비정상 세션을 종료한다.

<a id="e37ec303b54d3986"></a>
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

<a id="b71ccda3a49144c1"></a>
### 호환성

SQL 표준에서는 정의하지 않고 있다.

<a id="c9672eb1d1318175"></a>
## ALTER SYSTEM {MOUNT | OPEN} DATABASE

<a id="863aeb0d17983c5b"></a>
### 기능

데이터베이스를 시스템에 마운트하거나 서비스 가능한 상태로 변경한다.

<a id="29c94cbbcf051e40"></a>
### 구문

```
<alter system database statement> ::=
    ALTER SYSTEM <alter system database clause>
    ;

<alter system database clause> ::= 
      MOUNT DATABASE
    | OPEN [ <database_scope> ] DATABASE [ <open_database_option> ]

<open_database_option> ::=
      READ WRITE [ NORESETLOGS | RESETLOGS ]
    | READ ONLY

<database_scope> ::=
	  LOCAL
    | GLOBAL
```

<a id="9a49ef0d11798b8a"></a>
### 사용 범위 및 접근 권한

&lt;alter system database statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="a1b1fa4c313b58c6"></a>
### 구문 규칙 및 파라미터

<a id="659af6e0bb5fdcd3"></a>
#### &lt;alter system database clause&gt;

- MOUNT DATATABASE
    - 데이터베이스를 시스템에 마운트한다. 
- OPEN DATABASE
    - 데이터베이스를 서비스 가능한 상태로 변경한다.

<a id="626f23bd7b38ec41"></a>
#### &lt;open database option&gt;

- READ ONLY/ READ WRITE
    - 읽기 쓰기 모드를 지정하여 데이터베이스를 구동한다.
    - 생략된 경우에는 READ WRITE로 구동된다.
- RESETLOGS/ NORESETLOGS
    - 데이터베이스를 복구한 이후에 온라인 redo log를 유지할지 선택한다.
    - NORESETLOGS는 기존 redo log를 유지하는 반면에 RESETLOGS는 이를 초기화한다.
    - 데이터베이스를 불완전 복구한 경우, 반드시 RESETLOGS를 지정해야 한다.
    - 생략된 경우에는 NORESETLOGS가 기본으로 지정된다.

<a id="08452968b77604f7"></a>
#### &lt;database_scope&gt;

- LOCAL
    - LOCAL 영역 서버를 OPEN 단계로 구동한다.
- GLOBAL
    - GLOBAL 영역, 즉 전체 서버를 OPEN 단계로 구동한다.
- Cluster 환경에서 생략된 경우 GLOBAL로 구동 된다.

<a id="cd8594c3d1ee0d0b"></a>
### 사용 예

다음은 읽기 전용으로 데이터베이스를 구동하는 예이다.

```
ALTER SYSTEM OPEN DATABASE READ ONLY;
```

다음은 읽기/쓰기 모드로 구동하고, 온라인 redo log를 초기화하는 예이다.

```
ALTER SYSTEM OPEN DATABASE READ WRITE RESETLOGS;
```

<a id="f52d103fb3cc7a72"></a>
### 호환성

SQL 표준에서는 데이터베이스의 MOUNT 또는 OPEN에 대한 개념을 정의하지 않고 있다.

<a id="0ebd626f04c680dc"></a>
### 참조

관련 내용은 [ALTER DATABASE RECOVER](#c133e118c29e1673)를 참조한다.

<a id="09eb285fab941169"></a>
## ALTER SYSTEM RECONNECT GLOBAL CONNECTION

<a id="7e75bc20e2ebe5a5"></a>
### 기능

GLOBAL CONNECTION 형태로 접속한 세션에 재접속할지 여부를 설정한다.

<a id="a235dfa2b4b2eca6"></a>
### 구문

```
<alter system reconnect global connection statement> ::=
    ALTER SYSTEM RECONNECT GLOBAL CONNECTION
    ;
```

<a id="0ad7abe35dc80843"></a>
### 사용 범위 및 접근 권한

&lt;alter system reconnect global connection statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="ab1c31d6f1f873a0"></a>
### 설명

GLOBAL CONNECTION 클라이언트의 재접속 여부는 최초 접속할 때 서버로부터 얻은 system 객체의 SCN과 현재 서버의 system 객체의 SCN을 비교하여 결정한다. 해당 구문은 system 객체의 SCN을 상승시켜 클라이언트의 재접속을 유도한다.

해당 구문을 수행한 즉시 클라이언트가 재접속하는 것은 아니다. 클라이언트가 서버에 명령어를 실행할 때 SCN 비교를 통해서 재접속하며 만약 클라이언트에서 모든 멤버로의 연결이 유효하다면 재접속을 시도하지 않는다.

<a id="1f4514bf709bd719"></a>
### 사용 예

다음은 해당 구문을 수행하는 예이다.

```
gSQL> ALTER SYSTEM RECONNECT GLOBAL CONNECTION;

System altered.
```

<a id="0d2def395a99168a"></a>
### 호환성

SQL 표준에서는 GLOBAL CONNECTION의 개념을 정의하지 않고 있다.

<a id="9be42615a3dca0b0"></a>
## ALTER SYSTEM RESET property_name

<a id="d87a95f4ff6c86f4"></a>
### 기능

프로퍼티 파일에서 프로퍼티 값을 삭제한다.

<a id="8412c9f2a346c90d"></a>
### 구문

```
<alter system reset statement> ::=
    ALTER SYSTEM { RESET | UNSET } <property name>
        [ SCOPE = { FILE | SPFILE } ]
        [ AT <domain name>]
    ;
```

<a id="cd08731c15ec0841"></a>
### 사용 범위 및 접근 권한

&lt;alter system reset statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="0131f755ccc52fc1"></a>
### 구문 규칙 및 파라미터

<a id="a8aa5780275e0076"></a>
#### { RESET | UNSET }

RESET과 UNSET은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다.

<a id="ad9b11e21780ea23"></a>
#### &lt;property name&gt;

삭제할 프로퍼티의 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#4752291cb768d51a) 장을 참조한다.

<a id="0c08c4e468006e3d"></a>
#### [ SCOPE = { FILE | SPFILE } ]

프로퍼티 파일에서 삭제하는 것이므로 SCOPE=FILE/SPFILE만 사용할 수 있다.

- SCOPE = FILE 
    - FILE과 SPFILE은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다. 
    - 프로퍼티를 FILE에서 삭제하고, 현재 상태에는 적용하지 않는다. 
    - Database를 재구동할 때 변경 사항을 적용한다.

SCOPE 절을 명시하지 않을 경우, 기본값은 SCOPE = FILE 이다.

<a id="56d6900aadf15196"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="df5b6f0412f639e6"></a>
### 설명

SCOPE=FILE/SPFILE을 사용하여 프로퍼티를 변경했을 경우, 갱신된 값이 프로퍼티 파일에 저장되고 데이터베이스를 재시작할 때 반영된다.

RESET 할 경우, 프로퍼티 파일에 저장된 해당 프로퍼티 갱신값을 파일에서 제거하고 데이터베이스를 재시작할 때 default 값을 사용하도록 한다.

<a id="41a2ba0a8e5da487"></a>
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

<a id="69015d5cb7f7215c"></a>
### 호환성

SQL 표준에서는 시스템 프로퍼티 개념을 정의하지 않고 있다.

<a id="5c1472987e7344d8"></a>
### 참조

관련 내용은 [ALTER SYSTEM SET property_name](#af037c637cf5ed8e)을 참조한다.

<a id="af037c637cf5ed8e"></a>
## ALTER SYSTEM SET property_name

<a id="cb35a450f45de7cf"></a>
### 기능

시스템의 프로퍼티 값을 설정한다.

<a id="0a1e68e01e1245bf"></a>
### 구문

```
<alter system set statement> ::=
    ALTER SYSTEM SET <property name> { = <property value> | TO DEFAULT }
        [ DEFERRED ]
        [ SCOPE = [ MEMORY | { FILE | SPFILE } | BOTH ] ]
    [AT <domain name>]
    ;
```

<a id="378c03d7f445f6ce"></a>
### 사용 범위 및 접근 권한

&lt;alter system set statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="69b723a2ce3758d6"></a>
### 구문 규칙 및 파라미터

<a id="d2fa147260365199"></a>
#### &lt;property name&gt;

설정할 프로퍼티의 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#4752291cb768d51a) 장을 참조한다.

<a id="64cd0b1c1cb06bef"></a>
#### &lt;property value&gt;

설정할 프로퍼티의 값이다.

<a id="522daa0ca0c1dfbb"></a>
#### TO DEFAULT

시스템 프로퍼티 값을 시스템을 구동할 당시의 최초값으로 설정한다.

<a id="5008ba465290f92d"></a>
#### [ DEFERRED ]

변경된 프로퍼티를 적용할 시점을 정의한다.

- DEFERRED 
    - 현재 SESSION에는 영향을 주지 않고, 새로 생성되는 SESSION에 적용된다. 
    - 프로퍼티의 SYS_MODIFIABLE 속성값이 IMMEDIATE/ DEFERRED 일 때 적용 가능하며, 반드시 명시해야 한다. 
    - 프로퍼티의 SYS_MODIFIABLE 속성값이 FALSE인 경우 사용할 수 없다.

프로퍼티의 SYS_MODIFIABLE 속성값이 IMMEDIATE일 경우, DEFERRED를 명시하지 않으면 모든 SESSION에 바로 적용된다.

<a id="8b16f5c568b5d0b1"></a>
#### [ SCOPE = [ MEMORY | { FILE | SPFILE } | BOTH ] ]

시스템 프로퍼티 변경에 영향을 받는 범위를 정의한다.

- SCOPE = MEMORY 
    - 변경 사항이 현재 상태에만 적용되며, database를 다시 구동할 경우 해당 값은 없어진다. 
- SCOPE = FILE 
    - FILE과 SPFILE은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다. 
    - 변경 사항을 FILE에 저장하고 현재 상태에는 적용하지 않는다. 
    - Database를 다시 구동할 때 변경을 적용한다. 
- SCOPE = BOTH 
    - 변경 사항을 FILE에 저장하고 현재 상태에도 적용한다.

SCOPE 절을 명시하지 않을 경우, 기본값은 SCOPE = MEMORY 이다.   
프로퍼티의 SYS_MODIFIABLE 속성값이 FALSE인 경우에는 반드시 SCOPE=FILE/SPFILE이라고 명시해야 한다.

<a id="c37f1ef123f16b25"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="ce72745d939df177"></a>
### 설명

자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#4752291cb768d51a) 장을 참조한다.

<a id="5b6e8ea51b4ef296"></a>
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

<a id="1b41e6e81eee3da8"></a>
### 호환성

SQL 표준에서는 시스템의 프로퍼티 개념을 정의하지 않고 있다.

<a id="86c66ccbeccb9227"></a>
### 참조

관련 내용은 [ALTER SYSTEM RESET property_name](#9be42615a3dca0b0)을 참조한다.

<a id="7c8ca8d8eb08351e"></a>
## ALTER SYSTEM SWITCH LOGFILE

<a id="dbe1dc78a559c764"></a>
### 기능

데이터베이스 내에 있는 CURRENT 상태의 로그파일을 ACTIVE 상태로 변경한다.

<a id="c6117a9236bd2804"></a>
### 구문

```
<alter system switch logfile statement> ::=
    ALTER SYSTEM SWITCH LOGFILE
    [ AT <domain name> ]
    ;
```

<a id="78a9e265ec7bfc37"></a>
### 사용 범위 및 접근 권한

&lt;alter system switch logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="79f3b59b2f46add6"></a>
### 구문 규칙 및 파라미터

<a id="6481ad4a87546470"></a>
#### &lt;alter system switch logfile statement&gt;

데이터베이스가 MOUNT 또는 OPEN 상태여야 한다.

<a id="bfd98d5d4a19fbc0"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="1e1f6dd07cfdf1a9"></a>
### 설명

기본적으로 CURRENT 상태의 로그파일이 다 채워지면 자동으로 로그 스위치가 발생한다. 해당 구문은 특수한 상황에서 강제로 로그 스위치를 하고자 할 때 사용된다.

<a id="7fb7441ddb27082e"></a>
### 사용 예

```
ALTER SYSTEM SWITCH LOGFILE;
```

<a id="a6641e2f2df26022"></a>
### 호환성

SQL 표준에서는 LOGFILE에 대한 개념을 정의하지 않고 있다.

<a id="c40fafdcd778b7be"></a>
### 참조

관련 내용은 [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#c9672eb1d1318175)를 참조한다.

<a id="9f06fbbb97531643"></a>
## ALTER TABLE

<a id="20fa536194cf1ae1"></a>
### 기능

테이블 정의를 변경한다.

<a id="0eed515ac2e15e40"></a>
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
    | <rename table constraint statement>
    | <add table supplemental log statement>
    | <drop table supplemental log statement>
    | <rebalance statement>
    | <move shard statement>
    | <merge shards statement>
    | <split shard statement>
    | <rename shard statement>
    | <read { only | write } statement>
    ;
```

<a id="703d3c2b446f4c4d"></a>
### 사용 범위 및 접근 권한

&lt;alter table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="c8df9afcaca09dc0"></a>
### 구문 규칙 및 파라미터

<a id="3a41210fa725118c"></a>
#### &lt;alter table physical attribute statement&gt;

테이블의 물리적 속성을 변경한다.  
자세한 내용은 [ALTER TABLE name STORAGE](#0f561051f6241863) 구문을 참조한다.

<a id="fcddb28395f510f0"></a>
#### &lt;rename table statement&gt;

테이블 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME TO](#10ba5f9aa422b796) 구문을 참조한다.

<a id="8708f56e448fcff7"></a>
#### &lt;add column definition&gt;

테이블에 column을 추가한다.  
자세한 내용은 [ALTER TABLE name ADD COLUMN](#9c4e0674f148ec34) 구문을 참조한다.

<a id="f19822a6b0d08c55"></a>
#### &lt;drop column definition&gt;

테이블에서 column을 삭제한다.  
자세한 내용은 [ALTER TABLE name SET UNUSED COLUMN](#5f868f55c17ee27a) 구문을 참조한다.

<a id="a7ea3df6997de25a"></a>
#### &lt;alter column definition&gt;

테이블 column의 정의를 변경한다.  
자세한 내용은 [ALTER TABLE name ALTER COLUMN](#958ead64c53defaa) 구문을 참조한다.

<a id="c3f2100a5ff3fb98"></a>
#### &lt;rename column statement&gt;

테이블 column의 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME COLUMN](#c0b57d0d67fde202) 구문을 참조한다.

<a id="608d44209d672052"></a>
#### &lt;add table constraint definition&gt;

테이블에 제약 조건을 추가한다.  
자세한 내용은 [ALTER TABLE name ADD CONSTRAINT](#6284b68cf4965435) 구문을 참조한다.

<a id="d21b073e82eaeafd"></a>
#### &lt;drop table constraint definition&gt;

테이블의 제약 조건을 삭제한다.  
자세한 내용은 [ALTER TABLE name DROP CONSTRAINT](#e1b50caa384abdca) 구문을 참조한다.

<a id="b773e871e7d31932"></a>
#### &lt;alter table constraint definition&gt;

테이블의 제약 조건을 변경한다.  
자세한 내용은 [ALTER TABLE name ALTER CONSTRAINT](#d1c73efb2139f581) 구문을 참조한다.

<a id="1fcdd2e544b58ea7"></a>
#### &lt;rename table constraint statement&gt;

테이블 제약 조건의 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME CONSTRAINT](#8d97143aba702151) 구문을 참조한다.

<a id="feed92efedf9166d"></a>
#### &lt;add table supplemental log statement&gt;

테이블의 데이터가 변경되면 redo log에 부가 정보를 추가하도록 설정한다.  
자세한 내용은 [ALTER TABLE name ADD SUPPLEMENTAL LOG](#e2d0b8e135a69236) 구문을 참조한다.

<a id="0c054ca22a2a6ebd"></a>
#### &lt;drop table supplemental log statement&gt;

테이블의 데이터가 변경되면 redo log에 부가 정보를 추가하지 않도록 설정한다.  
자세한 내용은 [ALTER TABLE name DROP SUPPLEMENTAL LOG](#b1fbf93f7c4076ac) 구문을 참조한다.

<a id="8781f734ab1e0228"></a>
#### &lt;rebalance statement&gt;

Cluster 환경에서 테이블의 shard를 재배치하거나 정합성이 깨진 shard를 동기화하여 정합성을 복구한다.  
자세한 내용은 [ALTER TABLE REBALANCE](#1af19281915840f1) 구문을 참조한다.

<a id="c7eea5f7ef2d3d3a"></a>
#### &lt;move shard statement&gt;

Cluster 환경에서 테이블의 특정 shard를 특정 cluster group으로 재배치한다.  
자세한 내용은 [ALTER TABLE MOVE SHARD](#9c686a45aebb93a8) 구문을 참조한다.

<a id="dd5987cc6af2f41e"></a>
#### &lt;merge shards statement&gt;

Cluster 환경에서 테이블의 특정 shard들을 병합하여 재배치한다.  
자세한 내용은 [ALTER TABLE name MERGE SHARDS](#0a6b98451b0f3978) 구문을 참조한다.

<a id="62e2c456841f3f0f"></a>
#### &lt;split shard statement&gt;

Cluster 환경에서 테이블의 특정 shard를 분산하여 특정 cluster group에 재배치한다.  
자세한 내용은 [ALTER TABLE SPLIT SHARD](#83a7cd15da189d05) 구문을 참조한다.

<a id="2b6dcb38e7b04e73"></a>
#### &lt;rename shard statement&gt;

Cluster 환경에서 테이블의 특정 shard 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME SHARD](#c559c185c217fc7e) 구문을 참조한다.

<a id="c080f1bade26c20e"></a>
#### &lt;read { only | write } statement&gt;

테이블에 READ ( only | write }을 설정한다.  
자세한 내용은 [ALTER TABLE name READ { ONLY | WRITE }](#10420ab5cb23ccdb) 구문을 참조한다.

<a id="f567de6b900ba332"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="18f1f98ef160035f"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="6c58f86e021bb7cc"></a>
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

<a id="9c4e0674f148ec34"></a>
## ALTER TABLE name ADD COLUMN

<a id="558ce10998a6f6f0"></a>
### 기능

테이블에 column을 추가한다.

<a id="c9d11863da259c42"></a>
### 구문

```
<add column definition> ::=
      ALTER TABLE table_name ADD [ COLUMN ] <column definition>
    | ALTER TABLE table_name ADD [ COLUMN ] ( <column definition> [, ...] )
    ;
```

<a id="3fe8e4fd5b72692e"></a>
### 사용 범위 및 접근 권한

&lt;add column definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블을 변경하려면 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - ALTER ANY TABLE ON DATABASE

- Column을 추가할 때 제약 조건을 함께 명시했다면, 다음과 같이 제약 조건을 생성할 수 있는 조건을 만족해야 한다.
    - 제약 조건이 생성될 스키마에 대해 다음 권한 중 하나가 있어야 한다. 
        - 해당 스키마에 대해 (ADD CONSTRAINT 또는 CONTROL SCHEMA) ON SCHEMA 
        - ALTER ANY TABLE ON DATABASE 
    - 생성할 제약 조건이 key 제약 조건일 경우, 인덱스가 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다. 
        - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
        - USAGE TABLESPACE ON DATABASE

- 해당 테이블의 소유자는 추가된 column에 대해 다음과 같은 권한을 갖는다.
    - 추가된 모든 column에 대한 권한 
        - SELECT(columns) ON TABLE WITH GRANT OPTION 
        - INSERT(columns) ON TABLE WITH GRANT OPTION 
        - UPDATE(columns) ON TABLE WITH GRANT OPTION 
        - REFERENCES(columns) ON TABLE WITH GRANT OPTION 
    - 함께 생성한 제약 조건에 대한 권한 
        - 제약 조건의 소유자 
        - 제약 조건과 함께 생성된 인덱스의 소유자

<a id="670fc0d65949c205"></a>
### 구문 규칙 및 파라미터

<a id="8e50cbb709beedd2"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="2fca2804400b7ee4"></a>
#### ADD [ COLUMN ]

COLUMN 예약어는 생략할 수 있다.

<a id="75709cc880a7977e"></a>
#### &lt;column definition&gt;

추가할 column을 정의한다.  
자세한 내용은 [CREATE TABLE](19-sql-references-c-g.md#66fde705300657e5) 구문의 [&lt;column definition&gt;](19-sql-references-c-g.md#c900b5532bd27960) 절을 참조한다.  
테이블 내에 동일한 column 이름이 존재하지 않아야 한다.

Column을 정의할 때 DEFAULT 절을 명시할 경우, 모든 row의 기본값을 추가되는 column에 저장한다.  
Column을 정의할 때 &lt;identity column specification&gt; 절을 명시한 경우, 모든 row 각각의 자동 생성값을 추가되는 column에 저장한다.   
Column을 정의할 때 NOT NULL 제약 조건을 함께 명시한 경우, 테이블을 비우거나 DEFALUT 절 또는 &lt;identity column specification&gt; 절을 함께 기술해야 한다.

<a id="c8e30dffc9133e40"></a>
#### ( &lt;column definition&gt; [, ...] )

다수의 column을 추가한다.   
괄호 내부에 다수의 &lt;column definition&gt;을 나열한다.

<a id="b8fb253c0770865c"></a>
### 설명

추가되는 column은 기존 column들의 뒤에 위치한다.   
DEFAULT 절이나 &lt;identity column specification&gt;을 명시한 경우, 수행시간은 테이블에 존재하는 row의 개수에 비례하여 증가한다.

<a id="12d7c24e4c009f1a"></a>
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

<a id="c53c10536a5a81ec"></a>
### 호환성

SQL 표준에서는 다수의 column definition 추가에 대해 정의하지 않고 있다.

<a id="549ee32dd96a10bb"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#9f06fbbb97531643)
- [ALTER TABLE name SET UNUSED COLUMN](#5f868f55c17ee27a)
- [ALTER TABLE name ALTER COLUMN](#958ead64c53defaa)
- [ALTER TABLE name RENAME COLUMN](#c0b57d0d67fde202)

<a id="6284b68cf4965435"></a>
## ALTER TABLE name ADD CONSTRAINT

<a id="76d895405f6b0eab"></a>
### 기능

테이블 제약 조건을 추가한다.

<a id="e05c0a037adf86b8"></a>
### 구문

```
<add table constraint definition> ::=
    ALTER TABLE table_name 
        ADD <table constraint definition>
    ;
```

<a id="59a847e3ece7808f"></a>
### 사용 범위 및 접근 권한

&lt;add table constraint definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 제약 조건을 생성할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - ALTER ANY TABLE ON DATABASE

- 제약 조건이 생성될 스키마에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 스키마에 대해 (ADD CONSTRAINT 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 생성할 제약 조건이 key 제약 조건일 경우, 인덱스가 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
    - USAGE TABLESPACE ON DATABASE

- 생성한 제약 조건의 소유자는 다음과 같이 결정된다.
    - 제약 조건이 속한 스키마의 소유자
    - 제약 조건이 속한 스키마가 PUBLIC 일 경우, 구문을 수행한 사용자

> Cluster system에서 PRIMARY KEY와 UNIQUE 제약 조건은 모든 sharding key를 포함해야 한다.

<a id="574e8dd9d8cbf464"></a>
### 구문 규칙 및 파라미터

<a id="5ba9d224f9832f70"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="14203482bf10fd08"></a>
#### &lt;table constraint definition&gt;

추가할 제약 조건을 정의한다.  
NOT NULL 제약 조건은 ALTER TABLE .. ADD CONSTRAINT 구문으로 추가할 수 없으며, 다음 예와 같이 [ALTER TABLE name ALTER COLUMN](#958ead64c53defaa) 구문을 이용해 정의할 수 있다.

```
ALTER TABLE t1 ALTER COLUMN c1 SET NOT NULL;
```

자세한 내용은 [CREATE TABLE](19-sql-references-c-g.md#66fde705300657e5) 구문의 [&lt;table constraint definition&gt;](19-sql-references-c-g.md#f133717800abbac2) 절을 참조한다.

<a id="8fe42b13b55e9b76"></a>
### 설명

Primary key, unique key와 같은 key 제약을 추가할 때 이를 위한 index가 자동으로 생성된다.

<a id="506bc46b3738620c"></a>
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

<a id="7e6bde771d60b565"></a>
### 호환성

**SQL 표준 호환성**

<a id="174b0c7dc8fff902"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="1f423e59eb34ec5d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](19-sql-references-c-g.md#66fde705300657e5)
- [CREATE INDEX](19-sql-references-c-g.md#8e0637af857026b6)
- [ALTER TABLE](#9f06fbbb97531643)
- [ALTER TABLE name DROP CONSTRAINT](#e1b50caa384abdca)

<a id="1c36bfba15f57bda"></a>
## ALTER TABLE name ADD GLOBAL SECONDARY INDEX

<a id="1c36c2a11c680acf"></a>
### 기능

테이블에 global secondary index를 생성한다.

<a id="d3115dfdc1b0303b"></a>
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
    | MINSIZE <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="c3f873907f1b0814"></a>
### 사용 범위 및 접근 권한

&lt;alter table add global secondary index definition&gt; 구문은 cluster system에서 정의할 수 있으며 사용자는 다음 조건들을 만족해야 한다.

- 인덱스를 생성할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 인덱스가 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE
    - USAGE TABLESPACE ON DATABASE

<a id="9c55d4f394a4ceec"></a>
### 구문 규칙 및 파라미터

<a id="c0b22490c3420681"></a>
#### table_name

인덱스를 생성할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="6f55741adde3ee93"></a>
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

<a id="8cd864c4eeb48a36"></a>
#### &lt;segment attr clause&gt;

인덱스가 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer
    - 정의
        - 인덱스를 생성할 때 초기에 할당할 물리적 공간의 크기를 기술한다.
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT 크기가 8192 bytes일 경우 'INITIAL 100'은 실제 8192 bytes로 작동한다.)
        - 이 크기 (TABLESPACE의 EXTENT 크기에 align 된 크기)는 MINEXTENTS의 크기와 같거나 커야 하며, MAXEXTENTS의 크기와 같거나 작아야 한다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기본값은 인덱스가 속한 TABLESPACE의 EXTENT 하나 크기이다.

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
        - 인덱스에서 유지해야 할 최소 공간의 크기이다.
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

<a id="8e08c3b7646f779c"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="0665f433fb640422"></a>
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

<a id="c446baadbf32cb10"></a>
#### TABLESPACE tablespace_name

인덱스가 저장될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - LOGGING 인덱스로 변경하려면, tablespace_name은 data tablespace여야 하며 
    - NOLOGGING 인덱스로 변경하려면 tablespace_name은 temporary tablespace 또는 nologging tablespace여야 한다.

- TABLESPACE 절을 생략할 경우, 기존 인덱스의 설정을 그대로 따른다.

<a id="cac47e440d989bf1"></a>
### 설명

Non-deterministic 질의에는 global secondary index가 반드시 필요하다. LOGGING 인덱스와 NOLOGGING 인덱스에는 다음과 같은 trade-off가 있다

- LOGGING 인덱스
    - 장점: 시스템을 구동할 때 로그를 이용해 인덱스가 자동으로 복구되므로 별도의 구축과정이 없다.
    - 단점: 관련 row를 변경할 때 인덱스 변경 내용을 로그로 기록하여 디스크 IO를 유발한다.
- NOLOGGING 인덱스
    - 장점: 관련 row를 변경할 때 인덱스 변경 내용에 대해 디스크 IO가 발생하지 않는다.
    - 단점: 시스템을 구동할 때 인덱스에 대한 로그 정보가 없어 자동으로 인덱스를 재구축한다.

<a id="4159e86d1ad42dd4"></a>
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

<a id="9b4e0c4a67a5bc1b"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="e8360db0954668a3"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#4072f36ce518c112)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#61ebd0ca6a377889)
- [CREATE TABLE](19-sql-references-c-g.md#66fde705300657e5)

<a id="e2d0b8e135a69236"></a>
## ALTER TABLE name ADD SUPPLEMENTAL LOG

<a id="379b9563972d1f70"></a>
### 기능

테이블의 데이터가 변경될 때 테이블에 primary key가 있으면 redo log에 primary key 값을 추가하도록 설정한다.

<a id="14d0ab6e92dc5ac7"></a>
### 구문

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="0a2ee91c29bccb30"></a>
### 사용 범위 및 접근 권한

&lt;add table supplemental log statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="f1d727693ed9ae23"></a>
### 구문 규칙 및 파라미터

<a id="ba3bc765fbfbd3bd"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

테이블에 primary key가 존재하지 않더라도 구문을 수행할 수 있다.

<a id="064e8ad22b71f081"></a>
### 설명

해당 TABLE에 UPDATE/ DELETE를 수행할 때 SUPPLEMENTAL LOG를 추가로 기록하도록 한다. 기록된 SUPPLEMENTAL LOG는 CDC와 같은 툴 또는 로그를 분석할 때 사용된다.

모든 TABLE의 SUPPLEMENTAL LOG를 기록하려면 *SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY = YES* 로 설정한다.

<a id="68764a9299810d07"></a>
### 사용 예

다음은 테이블의 data를 변경할 때 redo log에 primary key 값을 추가하도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="5d67a28de57a6baa"></a>
### 호환성

SQL 표준에서는 &lt;add table supplemental log statement&gt;를 다루지 않는다.

<a id="7016b60e9c60e0a0"></a>
### 참조

관련 내용은 [ALTER TABLE name DROP SUPPLEMENTAL LOG](#b1fbf93f7c4076ac)를 참조한다.

<a id="958ead64c53defaa"></a>
## ALTER TABLE name ALTER COLUMN

<a id="e73995caba7cf8e5"></a>
### 기능

Column의 정의를 변경한다.

<a id="a5f60cbd18152204"></a>
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
      [ NOT ] DEFERRABLE [ <constraint check time> ]
    | <constraint check time> [ [ NOT ] DEFERRABLE ]

<constraint check time> ::=
      INITIALLY DEFERRED 
    | INITIALLY IMMEDIATE

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

<a id="7dfdffc238b6791a"></a>
### 사용 범위 및 접근 권한

&lt;alter column definition&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="da80af62e6c1e4ae"></a>
### 구문 규칙 및 파라미터

<a id="9d600aa705d9fb93"></a>
#### table_name

변경할 테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="4f09a73516530c30"></a>
#### ALTER [ COLUMN ]

COLUMN 예약어는 생략할 수 있다.

<a id="48cce21b8e093315"></a>
#### column_name

변경할 column의 이름이다.

<a id="e07147a7324b85cc"></a>
#### &lt;set column default clause&gt;

Column의 기본값을 설정한다.   
identity column이 아니어야 한다.

이후에 수행되는 INSERT 구문 등에서 DEFAULT 절을 사용할 경우 설정한 기본값이 사용된다.

DEFAULT expression의 데이터 타입은 column의 데이터 타입과 호환 가능해야 한다.   
타입이 호환되지 않거나 expression이 valid 하지 않으면 에러가 발생한다.

자세한 설명은 [CREATE TABLE](19-sql-references-c-g.md#66fde705300657e5) 구문의 [&lt;default clause&gt;](19-sql-references-c-g.md#fb28203ff120409d) 절을 참조한다.

<a id="c8b5325572e7f437"></a>
#### &lt;drop column default clause&gt;

Column의 기본값을 제거한다.  
identity column이 아니어야 한다.  
기본값을 제거하면 INSERT 구문 등에서 DEFAULT 절을 사용할 때 NULL 값으로 설정된다.

<a id="355eb372c9cf9f05"></a>
#### &lt;set column not null clause&gt;

- SET [CONSTRAINT constraint_name] NOT NULL [ &lt;constraint characteristics&gt; ]
    - Column에 NOT NULL 제약 조건을 설정한다.
    - Column의 값으로 NULL 값을 허용하지 않는다.
    - 해당 column에 NULL 값이 존재하지 않아야 한다.

- [CONSTRAINT constraint_name]을 생략할 경우 자동으로 제약 조건 이름을 지정한다.
- &lt;constraint characteristics&gt;를 생략할 경우, NOT DEFERRABLE INITIALLY IMMEDIATE 속성을 갖는다.
- Identity column은 DEFERRABLE 속성을 가질 수 없다.

지연가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](20-sql-references-h-z.md#2e96c033f710d10f) 구문의 설명을 참조한다.

<a id="e268a247c4074d69"></a>
#### &lt;drop column not null clause&gt;

- DROP NOT NULL
    - Column의 NOT NULL 제약 조건을 제거한다.

<a id="e929e7d1df23593f"></a>
#### &lt;alter column data type clause&gt;

- SET DATA TYPE &lt;data type&gt;
    - Column의 데이터 타입을 변경한다.

> SET DATA TYPE 구문은 자동으로 commit 되는 DDL 구문이다.

동일한 계열간에 타입을 변경할 수 있는데 이 때 다음 조건을 만족해야 한다.

**character string type 변환**

<a id="76808ae4e6db9783"></a>
| from \ to | CHAR(n) | VARHCAR(n) | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR(m) | X | X | X |
| VARCHAR(m) | X | n >= m | X |
| LONG VARCHAR | X | X | O |

char length unit을 변경할 경우 다음과 같은 조건을 만족해야 한다.

**character length unit 변환**

<a id="78ae1209b2c56a20"></a>
| from \ to | OCTETS | CHARACTERS |
| --- | --- | --- |
| OCTETS | O | O |
| CHARACTERS | X | O |

**binary string type 변환**

<a id="c0da21922aab36a1"></a>
| from \ to | BINARY(n) | VARBINARY(n) | LONG VARBINARY |
| --- | --- | --- | --- |
| BINARY(m) | X | X | X |
| VARBINARY(m) | X | n >= m | X |
| LONG VARBINARY | X | X | O |

**numeric type**

<a id="16f6bfcb101a25f4"></a>
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

<a id="762cc835a25ea87e"></a>
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

<a id="832b2986e689985c"></a>
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

<a id="720dcfaca39067c9"></a>
| from \ to | NATIVE_SMALLINT | NATIVE_INTEGER | NATIVE_BIGINT | NATIVE_REAL | NATIVE_DOUBLE |
| --- | --- | --- | --- | --- | --- |
| NATIVE_SMALLINT | O | X | X | X | X |
| NATIVE_INTEGER | X | O | X | X | X |
| NATIVE_BIGINT | X | X | O | X | X |
| NATIVE_REAL | X | X | X | O | X |
| NATIVE_DOUBLE | X | X | X | X | O |

**Boolean type의 변환**

<a id="e20aa015e668a968"></a>
| from \ to | BOOLEAN |
| --- | --- |
| BOOLEAN | O |

**Date/ time type의 변환 (TZ: WITH TIME ZONE)**

<a id="7bcb2194cf833929"></a>
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

<a id="1486d4fb8bd4001f"></a>
| from \ to | YEAR(q) | MONTH(q) | YEAR(q) TO MONTH |
| --- | --- | --- | --- |
| YEAR(p) | q >= p | X | X |
| MONTH(p) | X | q >= p | X |
| YEAR(p) TO MONTH | X | X | q >= p |

**INTERVAL DAY TO TIME 계열의 type 변환 (p,q 가 생략된 경우 2) (f,g 가 생략된 경우 6)**

<a id="44913a3089917d0e"></a>
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

<a id="eb63e0f1a9e33ca9"></a>
| from \ to | ROWID |
| --- | --- |
| ROWID | O |

<a id="2752dfbb85ee4993"></a>
#### &lt;alter identity column specification&gt;

Column의 identity 속성을 변경한다.   
Column은 identity column 이어야 한다.

- SET GENERATED [ ALWAYS | BY DEFAULT ]
    - identity column의 생성 방식을 변경한다. 
    - 자세한 내용은 [CREATE TABLE](19-sql-references-c-g.md#66fde705300657e5) 구문의 [&lt;identity column specification&gt;](19-sql-references-c-g.md#b0d3a504f09267ed)을 참조한다. 
- &lt;alter sequence generator restart option&gt; 
    - identity column의 다음 값 (NEXT VALUE)을 변경한다. 
    - 자세한 내용은 [ALTER SEQUENCE](#3df2c32d366ffd24) 구문의 &lt;[alter sequence generator restart option&gt;](#64922dce03434d29) 절을 참조한다. 
- &lt;basic sequence generator option&gt; 
    - identity column의 속성을 변경한다. 
    - SQL 표준에서는 SET &lt;basic sequence generator option&gt;의 형태로 기술하도록 정의하고 있으나 생략 가능하다. 
    - 자세한 내용은 [ALTER SEQUENCE](#3df2c32d366ffd24) 구문을 참조한다.

<a id="001e89f6ac2361a7"></a>
#### &lt;drop identity property clause&gt;

Column의 identity 속성을 제거한다.   
Column은 identity column 이어야 한다.

<a id="94f8770e90082958"></a>
### 설명

SET NOT NULL 절의 null 검사 수행시간은 테이블의 row 개수에 비례한다.

다음과 같은 column은 NULL 값을 허용하지 않는다. 즉, DROP NOT NULL 절을 수행하더라도 다음 조건 중 하나를 만족할 경우 NULL 값을 허용하지 않는다.

- NOT NULL 제약 조건이 있는 column
- Column이 primary key 제약 조건에 포함되는 경우
- Column이 identity column인 경우

SET DEFAULT 절을 이용한 기본값 변경과 &lt;alter identity column specification&gt; 절을 이용한 identity 속성의 변경은 이후에 수행되는 INSERT 또는 UPDATE 구문에 적용된다.

<a id="f542625b65ed5a67"></a>
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

<a id="9634cd4a07129088"></a>
### 호환성

**SQL 표준 호환성**

<a id="51d6246521d26fbb"></a>
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

<a id="f2fe0f573ce9fe00"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#9f06fbbb97531643)
- [ALTER TABLE name ADD COLUMN](#9c4e0674f148ec34)
- [ALTER TABLE name SET UNUSED COLUMN](#5f868f55c17ee27a)
- [ALTER TABLE name RENAME COLUMN](#c0b57d0d67fde202)

<a id="d1c73efb2139f581"></a>
## ALTER TABLE name ALTER CONSTRAINT

<a id="cec43274d8464b1c"></a>
### 기능

테이블 제약 조건의 특성을 변경한다.

<a id="d7cccd182225f0b4"></a>
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
      [ NOT ] DEFERRABLE [ <constraint check time> ] 
    | <constraint check time> [ [ NOT ] DEFERRABLE ] 

<constraint check time> ::=
      INITIALLY DEFERRED 
    | INITIALLY IMMEDIATE
```

<a id="abc80fd78a815cac"></a>
### 사용 범위 및 접근 권한

&lt;alter table constraint definition&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

> Cluster는 지연 가능한 제약 조건을 지원하지 않는다.

<a id="4079191e06d0f51e"></a>
### 구문 규칙 및 파라미터

<a id="6e38dfbe9ef49b01"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="9d2f29153493ebad"></a>
#### &lt;constraint object&gt;

변경할 제약 조건은 다음과 같이 지정할 수 있다.

- CONSTRAINT constraint_name
    - 변경할 제약 조건의 이름이다.
- PRIMARY KEY 
    - 테이블의 PRIMARY KEY 제약 조건이다.
- UNIQUE( column [,...] ) 
    - Column 목록에 부합되는 UNIQUE 제약 조건이다.

<a id="574415475be62c8f"></a>
#### DEFERRABLE | NOT DEFERRABLE

제약 조건의 지연 가능 여부를 변경한다.

- DEFERRABLE
    - 제약 조건을 지연가능하도록 변경한다. 
- NOT DEFERRABLE 
    - 제약 조건을 지연가능하지 않도록 변경한다.

지연가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](20-sql-references-h-z.md#2e96c033f710d10f) 구문의 설명을 참조한다.

<a id="c015b9ff6e825840"></a>
#### INITIALLY IMMEDIATE | INITIALLY DEFERRED

제약 조건의 검사시점 초기값을 변경한다.

- INITIALLY IMMEDIATE 
    - DML을 수행할 때 제약 조건을 검사한다.
- INITIALLY DEFERRED 
    - COMMIT을 수행할 때 제약 조건을 검사한다.

NOT DEFERRABLE로 정의된 제약 조건은 INITIALLY DEFERRED로 변경할 수 없다.

<a id="a9248ca4629eed8e"></a>
### 설명

지연가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](20-sql-references-h-z.md#2e96c033f710d10f) 구문을 참조한다.

<a id="f1d3922d4c6587d9"></a>
### 사용 예

다음은 t1_uk 제약 조건을 지연가능하게 하고 검사시점을 DEFERRED로 설정하는 예이다.

```
gSQL> ALTER TABLE t1 ALTER CONSTRAINT t1_uk DEFERRABLE INITIALLY DEFERRED;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="837dc0682f11b322"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- ALTER PRIMARY KEY 절
- ALTER UNIQUE(column [,...]) 절

**SQL 표준 호환성**

<a id="d8521a466977f4de"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F492 | Optional table constraint enforcement | X |

<a id="61ebd0ca6a377889"></a>
## ALTER TABLE name ALTER GLOBAL SECONDARY INDEX

<a id="b5b04674b5ed5692"></a>
### 기능

테이블에서 global secondary index의 물리적 속성을 변경한다.

<a id="e003911eb5a666f9"></a>
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
    | MINSIZE <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]
```

<a id="726376319778e06a"></a>
### 사용 범위 및 접근 권한

&lt;alter table alter global secondary index storage statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="3a955b7a63ac8750"></a>
### 구문 규칙 및 파라미터

<a id="df8bece9482b2548"></a>
#### table_name

인덱스를 생성할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="880d1385ef67891f"></a>
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

<a id="b33bb59d5b725c6e"></a>
#### &lt;segment attr clause&gt;

인덱스가 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer
    - 정의
        - 인덱스를 생성할 때 초기에 할당할 물리적 공간의 크기를 기술한다.
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT 크기가 8192 bytes일 경우 'INITIAL 100'은 실제 8192 bytes로 작동한다.)
        - 이 크기 (TABLESPACE의 EXTENT 크기에 align 된 크기)는 MINEXTENTS의 크기와 같거나 커야 하며, MAXEXTENTS의 크기와 같거나 작아야 한다.
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

- MINSIZE integer
    - 정의
        - 인덱스에서 유지해야할 최소 공간의 크기이다.
        - 이 값은 MAXSIZE의 값과 같거나 작아야 한다.
    - 이 크기는 인덱스가 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - EXTENT 두 개 크기보다 작을 경우 EXTENT 두 개 크기로 결정된다.
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

- MAXSIZE integer
    - 정의
        - 인덱스에서 할당받을 수 있는 최대 공간의 크기이다.
        - 이 값은 MINSIZE의 값과 같거나 커야 한다.
    - 이 크기는 인덱스가 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

<a id="b5fc10c596ef897a"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="46d4969f0679c2ae"></a>
### 설명

Non-deterministic 질의를 하려면 global secondary index가 반드시 필요하다.

<a id="adbead8d6fc2343a"></a>
### 사용 예

테이블 T1의 global secondary index가 사용할 최대 크기를 100 Mbyte로 변경한다.

```
gSQL> ALTER TABLE T1 ALTER GLOBAL SECONDARY INDEX STORAGE( MAXSIZE 100M );

Table altered.

gSQL> COMMIT;

Commit complete.
```

테이블 T1의 global secondary index가 사용할 INITRANS, MAXTRANS 값을 2와 4로 변경한다.

```
gSQL> ALTER TABLE T1 ALTER GLOBAL SECONDARY INDEX INITRANS 2 MAXTRANS 4;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="5f38169bf67d343b"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="390efb4372ec179f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#1c36bfba15f57bda)
- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#4072f36ce518c112)

<a id="e1b50caa384abdca"></a>
## ALTER TABLE name DROP CONSTRAINT

<a id="d021967916147035"></a>
### 기능

테이블 제약 조건을 제거한다.

<a id="ac06e3bd6d4a4cea"></a>
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

<a id="13d47106fd7fb6c7"></a>
### 사용 범위 및 접근 권한

&lt;drop table constraint definition&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 제약 조건의 소유자 
- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="2070cdc7b70aae76"></a>
### 구문 규칙 및 파라미터

<a id="19d0320bcd9a638a"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="eb0efacf2a876822"></a>
#### CONSTRAINT constraint_name

제거할 제약 조건의 이름이다.

<a id="85667446c82ba725"></a>
#### PRIMARY KEY

테이블의 primary key 제약 조건이다.

<a id="928893e1d9bf91db"></a>
#### UNIQUE( column_name [, ...] )

Column들에 대한 unique 제약 조건이다.

<a id="28a67b515ca38cb9"></a>
#### &lt;drop behavior&gt;

생략할 경우, 기본값은 RESTRICT 이다.   
현재는 RESTRICT/ CASCADE가 동일하게 작동한다.

<a id="9a9f92b981339c52"></a>
### 설명

제약 조건의 이름을 사용하지 않고 NOT NULL 제약 조건을 제거하려고 할 경우 [ALTER TABLE name ALTER COLUMN](#958ead64c53defaa) 구문의 &lt;[drop column not null clause&gt;](#e268a247c4074d69) 절을 이용한다.

<a id="7943a6b4280c0423"></a>
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

<a id="ceeba89f8884933a"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- DROP PRIMARY KEY 
- DROP UNIQUE ( column_name [, ...] ) 
- CASCADE CONSTRAINTS

**SQL 표준 호환성**

<a id="9a0f8ea522968009"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="d27def8980007a2a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#9f06fbbb97531643)
- [ALTER TABLE name ADD CONSTRAINT](#6284b68cf4965435)
- [DROP INDEX](19-sql-references-c-g.md#f6216a28e7e3e011)

<a id="4072f36ce518c112"></a>
## ALTER TABLE name DROP GLOBAL SECONDARY INDEX

<a id="0c1f921d3d42bcad"></a>
### 기능

테이블에서 global secondary index를 제거한다.

<a id="91d5de4bc02c6391"></a>
### 구문

```
<alter table drop global secondary index definition> ::=
    ALTER TABLE table_name 
        DROP GLOBAL SECONDARY INDEX
    ;
```

<a id="903f75aa98cb266b"></a>
### 사용 범위 및 접근 권한

&lt;alter table drop global secondary index definition&gt; 구문은 cluster system에서 정의할 수 있으며 사용자는 다음 조건들을 만족해야 한다.

- 인덱스를 제거할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

<a id="308cdbf5d61f9c28"></a>
### 구문 규칙 및 파라미터

<a id="cc167827df440a0b"></a>
#### table_name

인덱스를 제거할 테이블 이름이다.

<a id="743ca4cb87905ace"></a>
### 설명

Non-deterministic 질의를 하려면 global secondary index가 반드시 필요하다.

<a id="78694eb395ae9d2f"></a>
### 사용 예

테이블 T1에서 global secondary index를 제거한다.

```
gSQL> ALTER TABLE T1 DROP GLOBAL SECONDARY INDEX;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="84ad578f6c19c66c"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="2281ce3ab0f1704b"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#1c36bfba15f57bda)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#61ebd0ca6a377889)

<a id="b1fbf93f7c4076ac"></a>
## ALTER TABLE name DROP SUPPLEMENTAL LOG

<a id="a614d91b79fd6d39"></a>
### 기능

테이블의 데이터가 변경될 때 redo log에 primary key 정보를 남기지 않도록 설정한다.

<a id="eb69f8d78f01be73"></a>
### 구문

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="55fb9a7465f79aed"></a>
### 사용 범위 및 접근 권한

&lt;drop table supplemental log statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="7d3fc11fa72aca1e"></a>
### 구문 규칙 및 파라미터

<a id="abcd34e7873932c3"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
[ALTER TABLE name ADD SUPPLEMENTAL LOG](#e2d0b8e135a69236) 구문을 사용해 설정된 상태여야 한다

<a id="26ac9baa04d65dcf"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="e554fb524a32e818"></a>
### 사용 예

다음은 테이블의 데이터가 변경되었을 때 redo log에 primary key 정보를 남기지 않도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="f6de2570eba73cf3"></a>
### 호환성

SQL 표준에서는 &lt;drop table supplemental log statement&gt;를 다루지 않는다.

<a id="0a6b98451b0f3978"></a>
## ALTER TABLE name MERGE SHARDS

<a id="54a6a64297827f52"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard들을 merge 하여 재배치한다.

<a id="74acbca007ccdb22"></a>
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

<a id="adecae418da6c887"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table merge shards statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="02a7cbaabd7a8995"></a>
### 구문 규칙 및 파라미터

<a id="c69c2ffdfb1eff39"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
해당 테이블이 cluster-specific이고 list shard 또는 range shard인 경우에만 구문을 수행할 수 있다.

<a id="a3bdf1d1c9300843"></a>
#### &lt;source shard list&gt;

Merge 할 원본 shard들의 list 이다.  
List에서 지정한 shard가 해당 테이블에 반드시 존재해야 한다.

<a id="f03f6b9cd3520222"></a>
#### source_shard_name

Merge 할 원본 shard의 이름이다.  
해당 테이블에 존재하지 않는 shard인 경우 구문을 수행할 수 없다.

<a id="c0f8c91059906580"></a>
#### start_shard_name

Merge 할 범위 중 시작 shard의 이름이다.   
Range shard에서만 사용된다.

<a id="a0254f971c5a473a"></a>
#### end_shard_name

Merge 할 범위 중 마지막 shard의 이름이다.  
Range shard에서만 사용된다.

<a id="d35a73b5b5f94367"></a>
#### dest_shard_name

대상 shard의 이름이다.

<a id="d84a27291e93b0f0"></a>
#### &lt;dest shard placement&gt;

대상 shard가 배치될 cluster group의 이름이다.  
해당 구문이 생략된 경우, dest_shard_name이 &lt;source shard list&gt;에 포함되어 있어야 한다.

<a id="ab5aaf1415a4aa48"></a>
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

<a id="ba8e454de338bc6f"></a>
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

<a id="2715eb1400d1a581"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="338f1f75cf15a73c"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name MOVE SHARD](#9c686a45aebb93a8)
- [ALTER TABLE name SPLIT SHARD](#83a7cd15da189d05)

<a id="9c686a45aebb93a8"></a>
## ALTER TABLE name MOVE SHARD

<a id="20822d558efb4fe0"></a>
### 기능

테이블의 특정 shard 또는 특정 cluster group의 전체 shard를 특정 cluster group에 재배치한다.

<a id="271e847183f8800e"></a>
### 구문

```
<alter table move shard statement> ::=
    ALTER TABLE table_name MOVE SHARD
        { shard_name_list | FROM CLUSTER GROUP src_cluster_group }
        TO CLUSTER GROUP dest_cluster_group [ ONLINE | OFFLINE ]
    ;
```

<a id="ae307d71da7c91b2"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table move shard statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="3a93990c775d3e4e"></a>
### 구문 규칙 및 파라미터

<a id="8a312ada25c9d29c"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
해당 테이블이 cluster group specific인 경우에만 구문을 수행할 수 있다.

<a id="a4c393fca8bd1858"></a>
#### shard_name_list

재배치할 shard name 목록이다.  
해당 테이블에 존재하지 않는 shard인 경우 구문을 수행할 수 없다.

<a id="e413543691a539cc"></a>
#### src_cluster_group

재배치할 특정 cluster group의 이름이다.

<a id="16b9d6e85d6ad95a"></a>
#### dest_cluster_group

테이블의 shard를 배치할 target cluster group의 이름이다.  
해당 테이블의 shard가 지정한 cluster group에 이미 존재할 경우 구문을 수행할 수 없다.

<a id="97e3c95a294a4ba6"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="1db542783d95395c"></a>
### 설명

테이블의 특정 shard를 특정 cluster group에서 다른 cluster group으로 재배치한다.

특정 cluster group을 제거하려면 테이블의 shard를 재배치한 후에 [DROP CLUSTER GROUP](19-sql-references-c-g.md#8bcf309cea211dc8) 구문을 수행해야 한다.

모든 테이블의 shard를 특정 cluster group에서 다른 cluster group으로 이동시키는 경우, ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP TO CLUSTER GROUP 구문을 수행한다.

CLONED 테이블이거나 CLUSTER WIDE로 설정된 테이블의 경우 에러가 발생하면서 실패할 수 있다.

<a id="1520c0695ca488d4"></a>
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

<a id="3d4a7a0b2f53c29c"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="6faeecce86eb08d5"></a>
### 참조

관련 내용은 [ALTER DATABASE MOVE SHARD](#0f4d5cb0f887a9b9)를 참조한다.

<a id="10420ab5cb23ccdb"></a>
## ALTER TABLE name READ { ONLY | WRITE }

<a id="6f4c3d1765b9affa"></a>
### 기능

테이블에 READ { ONLY | WRITE }을 설정한다.

<a id="738b6de86b05b016"></a>
### 구문

```
<alter table read { only | write } statement> :==
     ALTER TABLE table_name
         READ { ONLY | WRITE }
     ;
```

<a id="e3e36261eb32e9ea"></a>
### 사용 범위 및 접근 권한

&lt;alter table read { only | write } statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="fb233c357c0db57e"></a>
### 구문 규칙 및 파라미터

<a id="44763ec7bafdc7f1"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="e85a0da975263219"></a>
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

<a id="fc4ed5913c763a2d"></a>
### 사용 예

다음은 &lt;alter table read { only | write } statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 READ ONLY;

Table altered.

gSQL> ALTER TABLE t1 READ WRITE;

Table altered.
```

<a id="185faf892a5bcc3f"></a>
### 호환성

SQL 표준에서는 &lt;alter table read { only | write } statement&gt; 구문을 정의하지 있지 않다.

<a id="ce214b2f6255fc37"></a>
### 참조

관련 내용은 [ALTER TABLE](#9f06fbbb97531643)을 참조한다.

<a id="1af19281915840f1"></a>
## ALTER TABLE name REBALANCE

<a id="ea62184d102fd90a"></a>
### 기능

테이블의 shard를 재배치한다.

<a id="3e85a5558fd9345c"></a>
### 구문

```
<alter table rebalance statement> ::=
    ALTER TABLE table_name REBALANCE [ ONLINE | OFFLINE ]
    ;
```

<a id="7500e8dcc742656d"></a>
### 사용 범위 및 접근 권한

Cluster system 에서 수행할 수 있다.

&lt;alter table rebalance statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="860298b3663c5955"></a>
### 구문 규칙 및 파라미터

<a id="90ea41f1e2a6a156"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="f61b3befe1a61dd6"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="9a6477fae1063f5d"></a>
### 설명

다음과 같은 구문을 통해 cluster member, cluster group을 추가할 때 table들의 shard는 재배치하지 않는다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#8e2b3a3076fcfb3e)
- [ALTER CLUSTER GROUP name ADD MEMBER](#2aa692a04102ad1a)

추가된 cluster group과 cluster member의 테이블 shard를 재배치하려면 &lt;alter table rebalance statement&gt; 구문을 수행한다. 테이블의 shard 가 이미 재배치된 경우, 별도의 재배치 작업없이 성공한다.

모든 테이블들의 shard를 재배치하려면 [ALTER DATABASE REBALANCE](#be8f993bb3ff62bc) 구문을 수행한다.

<a id="2cf7892562d83fb0"></a>
### 사용 예

다음은 &lt;alter table rebalance statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 REBALANCE;

Table altered.
```

<a id="ca5c2fd189b66fe4"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="1271c86ed9218a0f"></a>
## ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list

<a id="4c49b979ff081867"></a>
### 기능

특정 cluster group에 shard를 포함하지 않도록 테이블의 shard를 재배치한다.

<a id="06b29fdab4f69a8f"></a>
### 구문

```
<alter table rebalance exclude cluster group statement> ::=
    ALTER TABLE table_name REBALANCE 
        EXCLUDE CLUSTER GROUP cluster_group_list [ ONLINE | OFFLINE ]
    ;
```

<a id="8a77b3e45836f6aa"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table rebalance exclude cluster group statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="8b50f3f1992496e4"></a>
### 구문 규칙 및 파라미터

<a id="ef457892026a05ae"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
해당 테이블이 cluster-wide인 경우에만 구문을 수행할 수 있다.

<a id="4e6b5b2d4aad7304"></a>
#### cluster_group_list

테이블의 shard를 포함하지 않는 cluster group의 list이다.   
재배치에서 제외될 cluster group이 cluster 전체 group인 경우 구문을 수행할 수 없다.

<a id="b8cd82f9bb7de8ed"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE 를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE 를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="0c11cf6fed363bdf"></a>
### 설명

특정 cluster group을 배제하고 테이블의 shard를 재배치한다.   
해당 cluster group에 테이블의 shard가 존재하지 않을 경우, 별도의 재배치 작업없이 성공한다.   
테이블의 shard가 위치한 cluster group을 기준으로 shard를 재배치한다.

특정 cluster group을 제거하려면 테이블의 shard를 재배치한 후에 [DROP CLUSTER GROUP](19-sql-references-c-g.md#8bcf309cea211dc8) 구문을 수행해야 한다.  
모든 테이블들에서 cluster group을 배제하고 shard를 재배치하고자 할 경우, [ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP](#d31035a48497afcf)을 수행한다.

<a id="64c6c0c3271ff36c"></a>
### 사용 예

다음은 &lt;alter table rebalance exclude cluster group statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 REBALANCE EXCLUDE CLUSTER GROUP g3;

Table altered.
```

<a id="cfca838f1422717f"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="954002d6c303e39b"></a>
## ALTER TABLE name REBUILD GLOBAL SECONDARY INDEX

<a id="d2c31c9f3c6cd727"></a>
### 기능

Global secondary index를 재구축한다.

<a id="098baa093cd768ad"></a>
### 구문

```
<rebuild global secondary index statement> ::=
    ALTER TABLE table_name REBUILD GLOBAL SECONDARY INDEX
        [ ONLINE | OFFLINE ]
        [ <index attributes> [...] ]
        [ TABLESPACE tablespace_name ]
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
    | MINSIZE <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="25e612628b6cb782"></a>
### 사용 범위 및 접근 권한

&lt;rebuild global secondary index statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 인덱스를 재구축할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 인덱스를 재구축할 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE
    - USAGE TABLESPACE ON DATABASE

<a id="eb0e69fd8054a379"></a>
### 구문 규칙 및 파라미터

<a id="b5528d6d64635bcd"></a>
#### table_name

인덱스를 재구축할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="d2418145292a0451"></a>
#### [ ONLINE | OFFLINE ]

인덱스를 재구축할 때, 해당 테이블에 DML을 허용할지 여부를 결정한다.

- ONLINE
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE이다.

<a id="d0ff8e0923b198e6"></a>
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

<a id="8202d3c48202c832"></a>
#### &lt;segment attr clause&gt;

인덱스가 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer
    - 정의
        - 인덱스를 재구축할 때 초기에 할당할 물리적 공간의 크기를 기술한다.
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT 크기가 8192 bytes일 경우 'INITIAL 100'은 실제 8192 bytes로 작동한다.)
        - 이 크기 (TABLESPACE의 EXTENT 크기에 align 된 크기)는 MINEXTENTS의 크기와 같거나 커야 하며, MAXEXTENTS의 크기와 같거나 작아야 한다.
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

- MINSIZE integer
    - 정의
        - 인덱스에서 유지해야할 최소 공간의 크기이다.
        - 이 값은 MAXSIZE의 값과 같거나 작아야 한다.
    - 이 크기는 인덱스가 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - EXTENT 두 개 크기보다 작을 경우 EXTENT 두 개 크기로 결정된다.
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

- MAXSIZE integer
    - 정의
        - 인덱스에서 할당받을 수 있는 최대 공간의 크기이다.
        - 이 값은 MINSIZE의 값과 같거나 커야 한다.
    - 이 크기는 인덱스가 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기존 인덱스에 설정된 값을 사용한다.

<a id="811b7b8e07c03093"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="bd282392a87e4aa3"></a>
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

<a id="924b3e2a5f48bfdf"></a>
#### TABLESPACE tablespace_name

인덱스가 재구축될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - tablespace_name이 data tablespace면 LOGGING 인덱스로 재구축된다.
    - tablespace_name이 temporary tablespace 또는 nologging tablespace면 NOLOGGING 인덱스로 재구축된다.
- TABLESPACE 절을 생략할 경우, 기존 인덱스의 tablespace로 설정된다.

<a id="ce6c0b114a7dd000"></a>
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

<a id="9508fc995dc954d3"></a>
### 사용 예

테이블 T1의 global secondary index를 재구축한다.

```
gSQL> ALTER TABLE T1 REBUILD GLOBAL SECONDARY INDEX;
```

테이블 T1의 global secondary index의 tablespace와 logging 설정을 변경한다.

```
gSQL> ALTER TABLE T1 REBUILD GLOBAL SECONDARY INDEX TABLESPACE MEM_DATA_TBS;

gSQL> ALTER TABLE T1 REBUILD GLOBAL SECONDARY INDEX TABLESPACE MEM_TEMP_TBS;
```

<a id="7f9ba026201ad5fb"></a>
### 호환성

SQL 표준은 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="4735ff9d6895a4ce"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#1c36bfba15f57bda)
- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#4072f36ce518c112)
- [ALTER INDEX name REBUILD](#a53bb774e5265424)

<a id="c0b57d0d67fde202"></a>
## ALTER TABLE name RENAME COLUMN

<a id="84a5fb8a6f54e902"></a>
### 기능

테이블 column의 이름을 변경한다.

<a id="823089f8514daf2b"></a>
### 구문

```
<rename column statement> ::=
    ALTER TABLE table_name 
        RENAME COLUMN old_column_name TO new_column_name
    ;
```

<a id="eaa2fc44db95e2fe"></a>
### 사용 범위 및 접근 권한

&lt;rename column statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="be27ee3ed5e6b312"></a>
### 구문 규칙 및 파라미터

<a id="92ad327673a7f383"></a>
#### table_name

변경할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="a36566f8060bf137"></a>
#### old_column_name

변경할 column의 기존 이름이다.

<a id="3b8a95976213c58a"></a>
#### new_column_name

변경할 column의 새로운 이름이다.   
테이블 내에 동일한 column 이름이 존재하지 않아야 한다.

<a id="097344beb8215be1"></a>
### 설명

Column 이름이 변경되더라도 이전에 해당 column을 기준으로 생성된 index, constraint 등의 객체를 변경할 필요는 없다.

<a id="5104134aaf500bde"></a>
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

<a id="f1914fdcb4001118"></a>
### 호환성

SQL 표준에서는 &lt;rename column statement&gt; 구문을 정의하지 않고 있다.

<a id="2f371597454a7266"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#9f06fbbb97531643)
- [ALTER TABLE name ADD COLUMN](#9c4e0674f148ec34)
- [ALTER TABLE name SET UNUSED COLUMN](#5f868f55c17ee27a)
- [ALTER TABLE name ALTER COLUMN](#958ead64c53defaa)

<a id="8d97143aba702151"></a>
## ALTER TABLE name RENAME CONSTRAINT

<a id="056bc60c2755c2f9"></a>
### 기능

테이블 제약 조건의 이름을 변경한다.

<a id="592bffed2f5fbebb"></a>
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

<a id="fc9bef4d771cce5a"></a>
### 사용 범위 및 접근 권한

&lt;rename table constraint statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="5f492c27a7d27615"></a>
### 구문 규칙 및 파라미터

<a id="0c90c0f375dd2aa2"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="e50ee229520a44a4"></a>
#### &lt;constraint object&gt;

변경할 제약 조건의 기존 이름은 다음과 같이 지정할 수 있다.

- CONSTRAINT constraint_name
    - 변경할 제약 조건의 이름이다.
- PRIMARY KEY
    - 테이블의 PRIMARY KEY 제약 조건이다.
- UNIQUE( column [,...] )
    - Column 목록에 부합되는 UNIQUE 제약 조건이다.

<a id="50eca850553efd5b"></a>
#### new_column_name

변경할 제약 조건의 새로운 이름이다.

<a id="560193c45fff344b"></a>
### 설명

Primary key, unique key와 같이 key 제약 조건으로 자동 생성된 index의 이름은 변경되지 않는다. Index 이름은 [ALTER INDEX name RENAME TO](#f0f556a04ad6636a) 구문을 사용하여 변경해야 한다.

<a id="6c2a91d72e9b3a70"></a>
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

<a id="1153b32843a9e296"></a>
### 호환성

SQL 표준에서는 &lt;rename table constraint statement&gt; 구문을 정의하지 않고 있다.

<a id="d24f5d064fecf7a6"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#9f06fbbb97531643)
- [ALTER TABLE name ADD CONSTRAINT](#6284b68cf4965435)
- [ALTER TABLE name DROP CONSTRAINT](#e1b50caa384abdca)
- [ALTER TABLE name ALTER CONSTRAINT](#d1c73efb2139f581)

<a id="c559c185c217fc7e"></a>
## ALTER TABLE name RENAME SHARD

<a id="bba3db025b44328d"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard의 이름을 변경한다.

<a id="b2f816e2b315c26f"></a>
### 구문

```
<alter table rename shard statement> ::=
    ALTER TABLE table_name 
        RENAME SHARD shard_name TO new_shard_name
    ;
```

<a id="5a8e49dac404baf5"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table rename shard statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="82e10ea18077c977"></a>
### 구문 규칙 및 파라미터

<a id="c1664d3eea2ad087"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="569753b8e8dc8f6c"></a>
#### shard_name

변경할 shard의 기존 이름이다.   
Shard가 해당 테이블에 존재하지 않을 경우 구문을 수행할 수 없다.

<a id="38f7a6cfd153510c"></a>
#### new_shard_name

변경할 shard의 새 이름이다.   
테이블 내에 동일한 shard 이름이 존재하지 않아야 한다.

<a id="672f4c3aaeaa02e6"></a>
### 설명

Hash, range, list 테이블의 특정 shard의 이름을 변경한다. Cloned 테이블에 대해서는 해당 구문을 수행할 수 없다.

<a id="36a8d26e33f7369a"></a>
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

<a id="e4f2327302823bb8"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="350e68ec576132e0"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#9f06fbbb97531643)
- [ALTER TABLE name MOVE SHARD](#9c686a45aebb93a8)
- [ALTER TABLE name SPLIT SHARD](#83a7cd15da189d05)
- [ALTER TABLE name REBALANCE](#1af19281915840f1)

<a id="10ba5f9aa422b796"></a>
## ALTER TABLE name RENAME TO

<a id="77ba9e512fb69a49"></a>
### 기능

테이블의 이름을 변경한다.

<a id="8559c52d33caa1ee"></a>
### 구문

```
<rename table statement> ::=
    ALTER TABLE table_name 
        RENAME TO new_table_name
    ;
```

<a id="344c527e82108747"></a>
### 사용 범위 및 접근 권한

&lt;rename table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="e6dbbbb3b2505813"></a>
### 구문 규칙 및 파라미터

<a id="a46cae8a9994937b"></a>
#### table_name

테이블의 기존 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="63d102b253189242"></a>
#### new_table_name

테이블의 새 이름이다.   
스키마 내에 동일한 테이블 이름이 존재하지 않아야 한다.

<a id="649d5e0602bb4628"></a>
### 설명

테이블 이름이 변경되더라도 이를 참조하는 index constraint 등의 객체는 변경할 필요없다.

<a id="b734ec3a2548525b"></a>
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

<a id="d4e80f6f762240ef"></a>
### 호환성

SQL 표준에서는 &lt;rename table statement&gt; 구문을 정의하지 않고 있다.

<a id="861188f54dce26b6"></a>
### 참조

관련 내용은 [ALTER TABLE](#9f06fbbb97531643)을 참조한다.

<a id="5f868f55c17ee27a"></a>
## ALTER TABLE name SET UNUSED COLUMN

<a id="eb065875cb25e042"></a>
### 기능

테이블 column을 제거한다.

<a id="50eefd93f8049c38"></a>
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

<a id="ac21549502a24ca3"></a>
### 사용 범위 및 접근 권한

&lt;drop column definition&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="758caeb1dffd9a44"></a>
### 구문 규칙 및 파라미터

<a id="48fe0c1176b2fb37"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="5188a2eaacfbe184"></a>
#### SET UNUSED [ COLUMN ]

해당 column들을 사용하지 않도록 설정한다.

<a id="d5227371c5135674"></a>
#### column_name_list

한 개 이상의 삭제될 column 이름이다.

- 예: ALTER TABLE t1 SET UNUSED COLUMN c1 
- 예: ALTER TABLE t1 SET UNUSED COLUMN (c1, c2)

<a id="733f7dae44d44e9f"></a>
#### column_name

삭제할 column의 이름이다.   
해당 column을 이용하는 제약 조건과 인덱스도 함께 삭제한다.

<a id="fd7869f506ad56cc"></a>
#### drop behavior

생략할 경우, 기본값은 RESTRICT 이다.   
현재는 RESTRICT/ CASCADE가 동일하게 작동한다.

<a id="0f2fc92e1e08dba5"></a>
### 설명

SET UNUSED COLUMN은 data를 물리적으로 제거하지 않으므로 row의 개수에 관계없이 일정한 성능을 보장한다.

<a id="228189772a24ea78"></a>
### 사용 예

다음은 해당 column을 사용하지 않도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 SET UNUSED COLUMN ( addr );

Table altered.
```

<a id="bcd68cf0fbcb5742"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- SET UNUSED 
- CASCADE CONSTRAINTS 
- 다수의 column 나열

**SQL 표준 호환성**

<a id="06b65ae053ad2aec"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F033 | ALTER TABLE statement: DROP COLUMN clause | X |

<a id="d1cfec3670a405b0"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#9f06fbbb97531643)
- [ALTER TABLE name ADD COLUMN](#9c4e0674f148ec34)
- [ALTER TABLE name ALTER COLUMN](#958ead64c53defaa)
- [ALTER TABLE name RENAME COLUMN](#c0b57d0d67fde202)

<a id="83a7cd15da189d05"></a>
## ALTER TABLE name SPLIT SHARD

<a id="b907ef55cb6ab220"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard를 split하여 재배치한다.

<a id="ccedf6b0ba7f201c"></a>
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

<a id="79e31455f7cc98a7"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table split shard statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="69177dc8482e54b2"></a>
### 구문 규칙 및 파라미터

<a id="f5722c1846b417c9"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
해당 테이블이 cluster group specific이고 list shard 또는 range shard인 경우에만 구문을 수행할 수 있다.

<a id="712b86d9d6e11dd3"></a>
#### source_shard_name

Split할 원본 shard 이름이다.   
해당 테이블에 shard가 존재하지 않을 경우 구문을 수행할 수 없다.

<a id="8ac037d882738f86"></a>
#### &lt;split shard placement&gt;

원본 shard를 split하여 재배치할 대상 shard를 정의한다.

<a id="7bafad7fca889b51"></a>
#### &lt;split shard bound def&gt;

split될 대상 shard의 bound를 정의한다.

다음 두 가지 bound def 중 하나로 정의할 수 있다.

- &lt;split list shard def&gt;
- &lt;split range shard def&gt;

<a id="a683ccc8cab4dcff"></a>
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

<a id="ad1f849102a8d0aa"></a>
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

<a id="36bca118a08643a8"></a>
#### dest_group_name

Split 된 shard가 배치될 cluster group의 이름이다.

<a id="a359f1f43440d28c"></a>
### 설명

특정 테이블의 특정 shard를 분산하여 임의의 cluster group에 배치한다.  
특정 shard에 해당하는 레코드가 많거나 특정 group member에 부하가 편중될 때 shard를 분산하여 레코드와 부하를 분산하기 위해 사용된다.

<a id="586d47a2eaa207e5"></a>
### 사용 예

다음은 &lt;alter table split shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES IN ( 11 ) AT CLUSTER GROUP G2 );

Table altered.

gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES LESS THAN ( 11 ) AT CLUSTER GROUP G2 );


Table altered.
```

<a id="7e86ba02ebdd070b"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="e6aee560078ec05a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name REBALANCE](#1af19281915840f1)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#1271c86ed9218a0f) 
- [ALTER TABLE name MOVE SHARD](#9c686a45aebb93a8)
- [ALTER TABLE name MERGE SHARDS](#0a6b98451b0f3978)

<a id="0f561051f6241863"></a>
## ALTER TABLE name STORAGE

<a id="e89808c36b7a2ce7"></a>
### 기능

테이블의 물리적 속성을 변경한다.

<a id="5a3ef14118ad7ae6"></a>
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
    | MINSIZE <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]
```

<a id="cc977e48f1681be8"></a>
### 사용 범위 및 접근 권한

&lt;alter table physical attribute statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="dc98eddc69461525"></a>
### 구문 규칙 및 파라미터

<a id="a63a8440840a70db"></a>
#### table_name

변경할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="21bddd8de3f81db2"></a>
#### &lt;physical attribute clause&gt;

테이블을 구성하는 page의 물리적 속성을 변경한다.  
이미 할당된 page에는 적용되지 않으며 새로 할당받는 page에 적용된다.  
자세한 설명은 [CREATE TABLE](19-sql-references-c-g.md#66fde705300657e5) 구문의 [&lt;table physical attribute clause&gt;](19-sql-references-c-g.md#565670570ebe15ff) 절을 참조한다.

<a id="612c460bbfab28b7"></a>
#### &lt;segment attr clause&gt;

세그먼트를 구성하는 extent의 물리적 속성을 변경한다.   
이미 할당된 extent에는 적용되지 않으며, 새로 할당받는 extent에 적용된다.

- MAXSIZE integer 
    - 할당될 수 있는 세그먼트 공간의 크기를 변경한다. 
    - 이미 할당되어 있는 공간보다 작은 크기를 지정하면, MAXSIZE가 현재 할당되어 있는 크기로 변경된다.

<a id="2bf6d824669f24d0"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="5371edd9d2bc74c0"></a>
### 사용 예

다음은 테이블의 물리적 속성을 변경하는 예이다.

```
gSQL> ALTER TABLE t1 PCTFREE 10 PCTUSED 40 STORAGE ( NEXT 10M  MAXSIZE  100M );

Table altered.
```

<a id="66e04ecbc105f6f8"></a>
### 호환성

SQL 표준에서는 테이블의 물리적 속성에 대하여 정의하지 않고 있다.

<a id="9bb3ed853e5e5e7d"></a>
### 참조

관련 내용은 [ALTER TABLE](#9f06fbbb97531643)을 참조한다.

<a id="7c3ae65b4798a999"></a>
## ALTER TABLESPACE

<a id="830df2b98da6785e"></a>
### 기능

테이블스페이스의 정의를 변경한다.

<a id="2c4a7249decc9196"></a>
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

<a id="ba1be08b1fce7672"></a>
### 사용 범위 및 접근 권한

&lt;alter tablespace statement&gt; 구문을 수행하려면 사용자에게 database에 대한 ALTER TABLESPACE 권한이 있어야 한다.

<a id="bfc6967a327696de"></a>
### 구문 규칙 및 파라미터

<a id="275e31ea6100bfb4"></a>
#### &lt;rename tablespace statement&gt;

테이블스페이스의 이름을 변경한다.  
자세한 내용은 [ALTER TABLESPACE name RENAME TO](#15b885476099f170) 구문을 참조한다.

<a id="9f877004bbfc786c"></a>
#### &lt;backup tablespace statement&gt;

테이블스페이스를 백업한다.  
자세한 내용은 [ALTER TABLESPACE name BACKUP](#9835448e7383ecdf) 구문을 참조한다.

<a id="8dfe4a2c7902e609"></a>
#### &lt;on-offline tablespace statement&gt;

테이블스페이스의 모든 파일을 online 또는 offline으로 변경한다.  
자세한 내용은 [ALTER TABLESPACE name [ONLINE|OFFLINE]](#7efb10590ea42838) 구문을 참조한다.

<a id="59fcb529775ec085"></a>
#### &lt;add file statement&gt;

테이블스페이스에 파일을 추가한다.  
자세한 내용은 [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#a2b661263866c629) 구문을 참조한다.

<a id="00161bf317337e99"></a>
#### &lt;drop file statement&gt;

테이블스페이스의 파일을 제거한다.  
자세한 내용은 [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#c6f42c41dbeae054) 구문을 참조한다.

<a id="96fa63c4933922e0"></a>
#### &lt;rename datafile statement&gt;

데이터 테이블스페이스의 데이터 파일 이름을 변경한다.  
자세한 내용은 [ALTER TABLESPACE name RENAME DATAFILE](#1bd2b61de5cf8ce9) 구문을 참조한다.

<a id="6a43b9abe737166b"></a>
### 설명

ALTER TABLESPACE 구문은 다른 Data Definition Language (DDL)과 달리 ROLLBACK 할 수 없고 구문을 수행한 transaction이 자동으로 COMMIT 된다.

<a id="a5c068f53d2ccd0e"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="7767781e14eda6b5"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="19623280ac6470a9"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLESPACE](19-sql-references-c-g.md#9425404264bb2534)
- [DROP TABLESPACE](19-sql-references-c-g.md#0ccb2cbcfd412a42)

<a id="a2b661263866c629"></a>
## ALTER TABLESPACE name ADD [DATAFILE|MEMORY]

<a id="0e75e2138c6f9bad"></a>
### 기능

테이블스페이스의 공간을 확장한다.

<a id="48bbd95e78cf038f"></a>
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

<a id="b989979b3e4bd955"></a>
### 사용 범위 및 접근 권한

&lt;add space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="41f81a470bccbe87"></a>
### 구문 규칙 및 파라미터

<a id="e26df4bc2e8c1269"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="b50757488cf15eeb"></a>
#### &lt;file specification&gt;

테이블스페이스의 유형에 따라 다음과 같은 구문을 사용해야 한다.

- 메모리 데이터 테이블스페이스 
    - DATAFILE &lt;add datafile clause&gt; 
- 메모리 임시 테이블스페이스 
    - MEMORY &lt;memory clause&gt;

<a id="6f168b58466928ee"></a>
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

<a id="49d8830c47ae07b4"></a>
#### &lt;memory clause&gt;

- &lt;size clause&gt;
    - 추가할 메모리를 정의한다.

자세한 내용은 [CREATE MEMORY TEMPORARY TABLESPACE](19-sql-references-c-g.md#54c1cb4e7c65e722) 구문의 [&lt;memory clause&gt;](19-sql-references-c-g.md#1c1d3262027fc36b)를 참조한다.

<a id="d7e0e710ef048c04"></a>
#### &lt;autoextend clause&gt;

디스크 테이블스페이스의 데이터 파일이 추가될 때 자동 확장 속성을 설정한다. 자동 확장 속성을 ON 또는 OFF로 설정한다. ON으로 설정하면 자동 확장 크기와 데이터 파일의 최대 크기를 지정할 수 있다.

<a id="9ba02f63845c37df"></a>
#### &lt;next size clause&gt;

현재 사용 중인 데이터 파일에 더 이상 사용할 공간이 없을 때 확장할 크기를 지정한다.

<a id="b0d4698afebb2999"></a>
#### &lt;max size clause&gt;

데이터 파일이 확장될 수 있는 최대 크기를 지정한다.

<a id="2981fadc84e92b8a"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="1f4db4e85d4da19c"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="6fa68240cc0c405e"></a>
### 사용 예

다음은 테이블스페이스에 data file을 추가하는 예이다.

```
gSQL> ALTER TABLESPACE space1 ADD DATAFILE 'test_file_a2.dbf' SIZE 10M REUSE;

Tablespace altered.
```

<a id="d68312ac037c846e"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="b0ffb52dbaf88162"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE MEMORY DATA TABLESPACE](19-sql-references-c-g.md#86993cea38f6279a)
- [CREATE MEMORY TEMPORARY TABLESPACE](19-sql-references-c-g.md#54c1cb4e7c65e722)
- [ALTER TABLESPACE](#7c3ae65b4798a999)

<a id="9835448e7383ecdf"></a>
## ALTER TABLESPACE name BACKUP

<a id="5e074b7a7e4a698b"></a>
### 기능

테이블스페이스를 backup 하기 위해 backup이 가능한 상태와 불가능한 상태로 전환한다.

<a id="b4e53943e4974bb6"></a>
### 구문

```
<backup tablespace statement> ::=
      <tablespace begin backup statement>
    | <tablespace end backup statement>
    | <tablespace incremental backup statement>    
    ;

<tablespace begin backup statement> ::=
    ALTER TABLESPACE tablespace_name BEGIN BACKUP [AT <domain_name>]
    ;

<tablespace end backup statement> ::=
    ALTER TABLESPACE tablespace_name END BACKUP [AT <domain_name>]
    ;

<tablesapce incremental backup statement> ::=
    ALTER TABLESPACE tablespace_name 
        BACKUP INCREMENTAL <incremental backup option> [AT <domain_name>]    ;

<incremental backup option> ::=
      LEVEL integer [ CUMULATIVE | DIFFERENTIAL ]
```

<a id="2e2deb8fcfbb67ac"></a>
### 사용 범위 및 접근 권한

&lt;backup space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="80765d17b900fcdb"></a>
### 구문 규칙 및 파라미터

<a id="a33a0b0d06ea0f70"></a>
#### &lt;tablespace begin backup statement&gt;

테이블스페이스를 백업 가능한 상태로 설정한다.

- 생성되어 사용 중인 테이블스페이스를 백업 가능한 상태로 설정한다.
- OFFLINE/ temporary 테이블스페이스는 backup 상태는 전환할 수 없다.

<a id="a53a02f536370fcf"></a>
#### tablespace_name

Backup 상태를 전환할 테이블스페이스의 이름이다.

<a id="6ac86be5cc9390d9"></a>
#### &lt;tablespace end backup statement&gt;

테이블스페이스를 백업이 불가능한 상태로 설정한다.

<a id="63ba1bae1049b168"></a>
#### &lt;tablesapce incremental backup statement&gt;

테이블스페이스의 증분 백업을 수행한다.  
데이터베이스가 OPEN 상태이고, ARCHIVELOG로 운영되어야 한다.

<a id="d60b203553ae6979"></a>
#### &lt;incremental backup option&gt;

- 'integer'는 0 ~ 4 까지 지정할 수 있다.
- 'LEVEL 0'는 CUMULATIVE나 DIFFERENTIAL을 지정할 수 없다.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - 'integer'가 n이면 가장 최근에 'LEVEL 0' ~ 'LEVEL n-1'까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - DIFFERENTIAL
        - 'integer'가 n이면 가장 최근에 'LEVEL 0' ~ 'LEVEL n'까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - 생략되면 DIFFERENTIAL이 기본으로 지정된다.

<a id="3f58b1957aaf5613"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="243c7ad614b7d35b"></a>
### 설명

테이블스페이스에 생성된 datafile을 백업한다. 테이블스페이스 전체를 백업하려면 BEGIN BACKUP을 수행한 후 OS의 파일 복사로 datafile들을 복사하고 나서 END BACKUP을 수행한다. 한편, 증분 백업 파일은 하나의 구문으로 BACKUP_DIR_1 property에 설정된 경로에 생성한다.

<a id="5ed053003c8b31bb"></a>
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

<a id="fcc9a4b4ffabb43f"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="73c5ed6a7255b0a8"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#7c3ae65b4798a999)
- [ALTER TABLESPACE name [ONLINE|OFFLINE]](#7efb10590ea42838)

<a id="c6f42c41dbeae054"></a>
## ALTER TABLESPACE name DROP [DATAFILE|MEMORY]

<a id="a2ece91f272613a9"></a>
### 기능

테이블스페이스의 공간을 축소한다.

<a id="42c40f0d165763b6"></a>
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

<a id="7a98bb55b6e03907"></a>
### 사용 범위 및 접근 권한

&lt;drop space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="a55e9039698aee49"></a>
### 구문 규칙 및 파라미터

<a id="0462b1461fa121de"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="ce8ad1aece91da29"></a>
#### &lt;file specification&gt;

테이블스페이스의 유형에 따라 다음과 같은 구문을 사용해야 한다.

- 메모리 데이터 테이블스페이스 
    - DATAFILE 'filename' 
- 메모리 임시 테이블스페이스 
    - MEMORY 'memory_name'

> 오프라인 테이블스페이스의 파일은 삭제할 수 없다.   
> 테이블스페이스의 첫 번째 파일은 삭제할 수 없다.  
> 한 번이라도 사용된 적이 있는 데이터 파일은 삭제할 수 없다.

<a id="71a7e7cd25959060"></a>
#### &lt;domain name&gt;

구문을 수행하는 멤버 및 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="393bb622ab29dd0a"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="c2e0ab1a0c6adf6a"></a>
### 사용 예

다음은 테이블스페이스의 파일을 제거하는 예이다.

```
gSQL> ALTER TABLESPACE space1 DROP DATAFILE 'test_file_f2.dbf';

Tablespace altered.
```

<a id="a425b68bdd6b48a7"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="ac663bd874748595"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#7c3ae65b4798a999)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#a2b661263866c629)
- [ALTER TABLESPACE name RENAME DATAFILE](#1bd2b61de5cf8ce9)

<a id="7efb10590ea42838"></a>
## ALTER TABLESPACE name [ONLINE|OFFLINE]

<a id="27fd23e4df126465"></a>
### 기능

테이블스페이스 상태를 변경한다.

<a id="a3e712e895dabdfe"></a>
### 구문

```
<on/off tablespace statement> ::=
    ALTER TABLESPACE tablespace_name { ONLINE | OFFLINE [ NORMAL | IMMEIDATE ] }
    [ AT <domain name> ]
    ;
```

<a id="ec211c7331ef77f3"></a>
### 사용 범위 및 접근 권한

&lt;on/off tablespace statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="7088ab3fb0864924"></a>
### 구문 규칙 및 파라미터

<a id="8cbc2e36b6597900"></a>
#### ONLINE

OFFLINE 상태의 테이블스페이스를 ONLINE으로 변경한다.

<a id="967d10c52408f1f1"></a>
#### OFFLINE NORMAL

ONLINE 상태의 테이블스페이스를 OFFLINE으로 변경한다.

OFFLINE으로 변경된 테이블스페이스는 일관된 (consistent) 상태이기 때문에 ONLINE 상태로 변경할 때 미디어 복구할 필요없다.

> MOUNT 단계에서는 OFFLINE NORMAL을 사용할 수 없다.   
> (단, 이전 인스턴스가 `\`SHUTDOWN NORMAL에 의해서 종료된 경우에는 가능하다.)

<a id="7ed55fdf072a4304"></a>
#### OFFLINE IMMEDIATE

ONLINE 상태의 테이블스페이스를 OFFLINE으로 변경한다.

OFFLINE으로 변경된 테이블스페이스는 비일관적인 (inconsistent) 상태이기 때문에, ONLINE 상태로 변경할 때 미디어 복구해야 한다.

> SYSTEM 테이블스페이스는 OFFLINE으로 변경할 수 없다.   
> OFFLINE IMMEDIATE는 미디어 복구를 필요로 하기 때문에 archive log mode에서만 수행할 수 있다.

<a id="54c1ccfaa1211c58"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="20c6eee8ff57e886"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="a765281a3167d569"></a>
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

<a id="45173c6eae9e4801"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="66f94fed56d1d8c3"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#7c3ae65b4798a999)
- [ALTER TABLESPACE name BACKUP](#9835448e7383ecdf)

<a id="1bd2b61de5cf8ce9"></a>
## ALTER TABLESPACE name RENAME DATAFILE

<a id="82e7b75216d62bbc"></a>
### 기능

테이블스페이스를 구성하는 데이터 파일의 이름을 변경한다.

<a id="b111c221d63bcce4"></a>
### 구문

```
<rename datafile statement> ::=
    ALTER TABLESPACE tablespace_name RENAME DATAFILE <filename_list> TO <filename_list>
    ;

    <filename_list> ::= 
        'filename' [ AT <domain name> ] [, ...]
```

<a id="841175c3d8795934"></a>
### 사용 범위 및 접근 권한

&lt;rename datafile statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

> TDS 모드이면서 데이터베이스가 OPEN인 상태에서는 온라인 테이블스페이스 파일을 변경할 수 없다. (임시 메모리 테이블스페이스는 제외된다.)   
> 변경한 후에도 파일은 반드시 존재해야 한다.

<a id="02fdde6c8efe7da7"></a>
### 구문 규칙 및 파라미터

<a id="07887696fa50b510"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="46c6f89412bb00b5"></a>
#### 'filename'

메모리 임시 테이블스페이스는 'memory_name'을 의미하며, 그 외의 테이블스페이스 종류는 'filename'을 의미한다.

<a id="4abe615acb5e9e2a"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="57d6440e33198bce"></a>
### 설명

테이블스페이스 상태에 따라 연산 가능 여부가 결정된다.

- OFFLINE: MOUNT 단계나 OPEN 단계에서 수행 가능하다.
- ONLINE: MOUNT 단계에서만 수행 가능하다.

<a id="1f7e0a884d315d28"></a>
### 사용 예

다음은 'test.dbf'를 'test1.dbf'로 변경하는 예이다.

```
gSQL> ALTER TABLESPACE TEST_TBS RENAME DATAFILE 'test.dbf' TO 'test1.dbf';

Tablespace altered.
```

<a id="7f6e7eb3213a9136"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="0b122cb2604e4c07"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#7c3ae65b4798a999)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#a2b661263866c629)
- [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#c6f42c41dbeae054)

<a id="15b885476099f170"></a>
## ALTER TABLESPACE name RENAME TO

<a id="36e2c01cbd632a12"></a>
### 기능

테이블스페이스의 이름을 변경한다.

<a id="1d674dcda8ae1b08"></a>
### 구문

```
<rename tablespace statement> ::=
    ALTER TABLESPACE tablespace_name RENAME TO <new_tablespace_name>
    ;
```

<a id="deafd64ef70a537b"></a>
### 사용 범위 및 접근 권한

&lt;rename space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="4fb4285b4758776f"></a>
### 구문 규칙 및 파라미터

<a id="57cea354f1559f02"></a>
#### tablespace_name

기존 테이블스페이스의 이름이다.

- Built-in 테이블스페이스의 이름은 변경할 수 없다.
- OFFLINE 테이블스페이스의 이름은 변경할 수 없다.

<a id="a752ff8c6309dadc"></a>
#### new_tablespace_name

새로운 테이블스페이스의 이름이다.

<a id="5643956e147eb8a7"></a>
### 설명

Tablespace 이름이 변경되더라도 기존에 이미 해당 tablespace에 생성된 table, index 등은 변경할 필요없다.

<a id="583c3f9f230389e7"></a>
### 사용 예

다음은 테이블스페이스의 이름을 변경하는 예이다.

```
gSQL> ALTER TABLESPACE space1 RENAME TO space2;

Tablespace altered.
```

<a id="4e57b8cd45b28a16"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="3713ff943227b26c"></a>
### 참조

관련 내용은 [ALTER TABLESPACE](#7c3ae65b4798a999)를 참조한다.

<a id="648c7792f8549c18"></a>
## ALTER USER

<a id="4b1dbbf5651d18c4"></a>
### 기능

데이터베이스 사용자 정의를 변경한다.

<a id="ae8f1cdce922cdb5"></a>
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

<a id="e1a23693122d5d9e"></a>
### 사용 범위 및 접근 권한

&lt;alter user statement&gt; 구문을 수행하려면 사용자에게 ALTER USER ON DATABASE 권한이 있어야 한다.  
단, &lt;alter password&gt;는 사용자가 user_identifier와 동일할 경우에 권한 없이 수행할 수 있다.

<a id="f05c693f628bf5e3"></a>
### 구문 규칙 및 파라미터

<a id="0772c44216959a01"></a>
#### user_identifier

변경할 사용자의 이름이다.

<a id="fc86a20b0d414071"></a>
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

<a id="a169c5586ed069a3"></a>
#### &lt;alter profile&gt;

비밀번호 관리 정책을 위한 profile을 변경한다.

- PROFILE profile_name
    - 사용자가 생성한 profile_name을 할당한다.
- PROFILE DEFAULT
    - 기본 profile인 "DEFAULT"를 할당한다.
- PROFILE NULL
    - Profile을 할당하지 않는다.

<a id="2253eb01ef9757f1"></a>
#### &lt;password expire&gt;

사용자의 비밀번호를 만료시킨다.

<a id="4b89b4d62c3663b3"></a>
#### &lt;account lock&gt;

- ACCOUNT LOCK
    - 사용자 계정을 잠근다. 
- ACCOUNT UNLOCK
    - 계정 잠금을 해제한다.

<a id="27e5e9d5f9eb3961"></a>
#### &lt;alter default tablespace&gt;

사용자의 기본 tablespace를 변경한다.   
tablespace_name은 data tablespace여야 한다.

<a id="2e798658d291876f"></a>
#### &lt;alter temporary tablespace&gt;

사용자의 temporary tablespace를 변경한다.   
tablespace_name은 temporary tablespace여야 한다.

<a id="44146350a191d700"></a>
#### &lt;alter index tablespace&gt;

사용자의 index tablespace를 변경한다.

- INDEX TABLESPACE tablespace_name을 지정한다.
    - Data tablespace를 지정한 경우, LOGGING 인덱스가 된다.
    - Temporary tablespace를 지정한 경우, NOLOGGING 인덱스가 된다.
- INDEX TABLESPACE NULL
    - Index tablespace를 지정하지 않는다.

<a id="40b5ae511895702b"></a>
#### &lt;alter schema path&gt;

사용자의 스키마 접근 경로를 변경한다.   
사용자의 SQL 구문에 schema가 명시되지 않았을 경우 스키마 접근 경로는 객체의 naming resolution을 위한 스키마 순서에 따라 결정된다.

스키마 이름이 기존에 스키마 접근 경로에 나열된 스키마 이름과 동일할 경우에는 추가적으로 반영되지 않는다.

다음은 *ALTER USER u1 SCHEMA PATH ( u1, s2, public );* 구문을 수행했을 때 schema에 존재하는 객체의 예이다.

<a id="58ef391ac82384ca"></a>
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

<a id="b0a6f284bab5d9e6"></a>
#### CURRENT PATH

현재 사용자의 schema path 이다.

다음 예와 같이 CURRENT PATH를 이용해 기존의 schema path를 유지하면서 새로운 schema path를 추가할 수 있다.

- u1의 현재 schema path 
    - (u1, public) 
- 구문 수행 
    - ALTER USER u1 SCHEMA PATH ( s1, CURRENT PATH, s2 ); 
- u1의 schema path는 다음과 같이 변경된다. 
    - (s1, u1, public, s2)

<a id="b17886d08bcb45ef"></a>
#### ALTER USER PUBLIC &lt;alter schema path&gt;

PUBLIC 계정의 schema path를 변경한다.   
PUBLIC 계정의 schema path는 모든 사용자의 schema path에 포함된다.

PUBLIC 계정에 최초로 부여된 schema path는 다음과 같다.

- DICTIONARY_SCHEMA 
- INFORMATION_SCHEMA 
- DEFINITION_SCHEMA 
- PERFORMANCE_VIEW_SCHEMA 
- FIXED_TABLE_SCHEMA

<a id="c5622ac2e40fda17"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="01d89e7c4787f0ae"></a>
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

<a id="9a767e52b592f3e4"></a>
### 호환성

SQL 표준에서 user의 개념은 다루고 있지만 user의 생성, 변경 및 삭제와 관련된 SQL 구문은 정의하지 않고 있다.

<a id="687e4ac8ef1ce8fb"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE USER](19-sql-references-c-g.md#f516f713c62659c7)
- [DROP USER](19-sql-references-c-g.md#a6f0bdba7a87d9c4)

<a id="a1de7597c5662129"></a>
## ALTER VIEW

<a id="d3911bdd01218f16"></a>
### 기능

View 정의를 변경한다.

<a id="71156b5d45d5fca9"></a>
### 구문

```
<alter view statement> ::=
    ALTER VIEW view_name <alter view action>
    ;

<alter view action> ::=
    COMPILE
```

<a id="7b918dd0d91cfd21"></a>
### 사용 범위 및 접근 권한

&lt;alter view statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 view에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- View가 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="b2a87ca5ea8b0954"></a>
### 구문 규칙 및 파라미터

<a id="7c813497cf8cad18"></a>
#### view_name

변경할 view의 이름이다.  
schema_name.view_name과 같이 view가 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="de907b56ffe68b73"></a>
#### COMPILE

View를 다시 컴파일한다.   
View column에 부여한 COMMENT는 초기화된다.

<a id="083aeff890e37420"></a>
### 설명

View가 참조하는 테이블이나 view가 변경되거나 삭제되면 해당 view도 영향을 받는다.

이런 정보는 INFORMATION_SCHEMA.VIEWS를 통해 조회할 수 있다.

- IS_COMPILED column
    - TRUE: View가 정상적으로 생성되었다.
    - FALSE: 에러가 존재하는 상태에서 FORCE 옵션으로 view가 생성되었다.

- IS_AFFECTED column
    - TRUE : View가 참조하는 테이블 또는 view가 변경되었다.
    - FALSE: View가 생성되고 COMPILE 된 후에 view가 참조하는 테이블이나 view가 변경되지 않았다.

<a id="592060a119c2dd46"></a>
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

<a id="3e80a2b14ec03cb2"></a>
### 호환성

SQL 표준에서는 &lt;alter view statement&gt; 구문을 정의하지 않고 있다.

<a id="00fac8c9e4497676"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE VIEW](19-sql-references-c-g.md#c6a48c56234057a1)
- [DROP VIEW](19-sql-references-c-g.md#9ad6c24b5f2fb86f)

<a id="34622e4780114792"></a>
## ANALYZE SYSTEM

<a id="047faa2d202b4164"></a>
### 기능

시스템의 통계 정보를 제어한다.

<a id="cbfd6bac26451296"></a>
### 구문

```
<analyze system statement> ::=
    ANALYZE SYSTEM [ <analyze action> ]
    ;

<analyze action> ::=
      COMPUTE STATISTICS
    | DELETE STATISTICS
```

<a id="08ef946e29f00733"></a>
### 사용 범위 및 접근 권한

&lt;analyze system statement&gt; 구문을 수행하려면 사용자에게 ANALYZE ANY ON DATABASE 권한이 있어야 한다.

<a id="3a8ae02d215d77e7"></a>
### 구문 규칙 및 파라미터

<a id="0a2500807a2e914a"></a>
#### &lt;analyze action&gt;

생략할 경우 기본값은 COMPUTE STATISTICS 이다.

<a id="f172716484ee0de2"></a>
#### COMPUTE STATISTICS

시스템과 관련된 다음과 같은 통계 정보를 구축한다.

- CPU_OPS (Operations Per Second) 
    - CPU가 초당 처리할 수 있는 operation의 개수이다.

- NETWORK_IOPS (IO operations Per Second) 
    - Cluster인 경우에 유효하다. 
    - 초당 처리할 수 있는 network IO 횟수이다.

<a id="67de01c34d864639"></a>
#### DELETE STATISTICS

시스템 통계 정보를 삭제한다.

<a id="a2adb44edd656f60"></a>
### 설명

구축한 시스템 통계 정보는 질의 처리를 위한 최적화 과정의 비용을 계산하기 위해 사용한다.

<a id="5e79205373671bc4"></a>
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

 CPU_OPS NETWORK_IOPS NETWORK_BUFSIZE LAST_ANALYZED             
-------- ------------ --------------- --------------------------
53000412         2914           65536 2017-03-30 16:49:42.200000

1 row selected.
```

<a id="e0f9409a921748a6"></a>
### 호환성

SQL 표준에서는 통계 정보에 대한 개념을 정의하지 않고 있다.

<a id="80fb614687505bee"></a>
### 참조

관련 내용은 [ANALYZE TABLE](#327c57ea5d5cc931)을 참조한다.

<a id="327c57ea5d5cc931"></a>
## ANALYZE TABLE

<a id="6d42718195dd2f55"></a>
### 기능

테이블의 통계 정보를 제어한다.

<a id="cc9c1e12f6df179e"></a>
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
      COMPUTE STATISTICS [ <for_clause> ]
    | ESTIMATE STATISTICS <sample_clause> [ <for_clause> ]
    | DELETE STATISTICS

<sample_clause>
      SAMPLE row_count ROWS
    | SAMPLE percentage PERCENT

<for_clause>
      FOR ALL COLUMNS
    | FOR ALL INDEXED COLUMNS
    | FOR COLUMNS column_name [, ...]
    | FOR ALL INDEXES
    | FOR INDEXES index_name [, ...]
```

<a id="e1ccebe70c7c4a97"></a>
### 사용 범위 및 접근 권한

&lt;analyze table statement&gt; 구문을 수행하려면 사용자에게 ANALYZE ANY ON DATABASE 권한이 있어야 한다.

<a id="4af71e82673ecec5"></a>
### 구문 규칙 및 파라미터

<a id="3c463dbb9e986614"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="dbb5af09e2ea771c"></a>
#### &lt;parallel clause&gt;

분석 과정에서 사용할 thread 개수를 지정한다.   
명시하지 않을 경우, 기본값은 PARALLEL 이다.

- NOPARALLEL
    - 병렬로 분석하지 않는다.

- PARALLEL [thread_count]
    - 병렬로 분석한다.
    - thread_count 값은 0 부터 사용할 수 있으며 최대값은 64 이다.
    - thread_count 값이 0이거나 생략된 경우 시스템의 CPU 개수에 의해 결정된다.

<a id="72989fe6af543875"></a>
#### &lt;analyze action&gt;

생략할 경우 기본값은 COMPUTE STATISTICS 이다.

<a id="07eeac603d13dacd"></a>
#### COMPUTE STATISTICS

전수 검사를 통해 테이블과 관련된 다음과 같은 통계 정보를 구축한다.

- Table 통계정보 
    - Row count 
- 각 column의 통계 정보 
    - 서로 다른 값의 개수 
    - NULL 값의 개수 
    - 값의 평균 길이 
    - 최소값 
    - 최대값 
- Index 통계정보 
    - 서로 다른 key의 개수

Column의 data type에 따라 구축하는 통계 정보는 다음과 같다.

**Data type에 따라 구축된 통계 정보**

<a id="5527d4bd46ee82c1"></a>
| Data type | NUM_DISTINCT | NUM_NULLS | AVG_LENGTH | MIN/MAX |
| --- | --- | --- | --- | --- |
| BOOLEAN | O | O | O | X |
| NATIVE_SMALLINT | O | O | O | O |
| NATIVE_INTEGER | O | O | O | O |
| NATIVE_BIGINT | O | O | O | O |
| NATIVE_REAL | O | O | O | O |
| NATIVE_DOUBLE | O | O | O | O |
| NUMBER | O | O | O | O |
| NUMERIC | O | O | O | O |
| FLOAT | O | O | O | O |
| CHAR(n) | O | O | O | 64 bytes 이하인  경우에 구축된다. |
| VARCHAR(n) | O | O | O | 64 bytes 이하인  경우에 구축된다. |
| LONG VARCHAR | X | X | X | X |
| BINARY | O | O | O | X |
| VARBINARY | O | O | O | X |
| LONG VARBINARY | X | X | X | X |
| DATE | O | O | O | O |
| TIME | O | O | O | O |
| TIMESTAMP | O | O | O | O |
| INTERVAL | O | O | O | O |
| ROWID | O | O | O | X |

<a id="bf963fca6d67c247"></a>
#### ESTIMATE STATISTICS &lt;sample_clause&gt;

지정한 &lt;sample_clause&gt;만큼의 샘플을 사용하여 column과 index의 통계 정보를 구축한다.

- SAMPLE row_count ROWS 
    - 지정한 row 개수만큼 샘플을 사용한다. 
    - row_count는 0보다 큰 양의 정수이다. 
- SAMPLE percentage PERCENT 
    - 지정한 비율만큼 샘플을 사용한다. 
    - Percentage는 1 ~ 99 범위의 양의 정수이다.

샘플링 row의 개수가 [MIN_SAMPLE_ROW_COUNT](../part-02-administration-manual/10-server-property.md#6ae84702cb5ce557) 프로퍼티 값보다 작을 경우 프로퍼티 값을 따른다.

<a id="d462fcf7fcd86ad5"></a>
#### &lt;for_clause&gt;

생략할 경우, 통계정보 구축이 가능한 모든 column과 모든 인덱스의 통계 정보를 구축한다.

<a id="a14b1fa4246322ab"></a>
#### FOR ALL COLUMNS

통계 정보 구축이 가능한 모든 column의 통계 정보를 구축한다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="74bbf7277ed27ef9"></a>
#### FOR ALL INDEXED COLUMNS

인덱스에 포함된 모든 column의 통계 정보를 구축한다.   
그 외 column의 통계 정보는 구축하지 않는다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="65460d072e9043d4"></a>
#### FOR COLUMNS column_name [, ...]

나열한 column의 통계 정보를 구축한다.   
기술하지 않은 column의 통계 정보는 구축하지 않는다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="fb87215c7cf37851"></a>
#### FOR ALL INDEXES

모든 인덱스의 통계 정보를 구축한다.   
Column 통계 정보는 구축하지 않는다.

<a id="e19ade353954c6c0"></a>
#### FOR INDEXES index_name [, ...]

나열한 인덱스의 통계 정보를 구축한다.   
기술하지 않은 인덱스의 통계 정보는 구축하지 않는다.   
Column 통계 정보는 구축하지 않는다.

<a id="29fcc6b7a98f5256"></a>
#### DELETE STATISTICS

테이블의 통계 정보를 제거한다.

<a id="a3a33d53aa71475f"></a>
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

<a id="f42cfa4eb5da13f0"></a>
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

<a id="2b8c78421c727eda"></a>
### 호환성

SQL 표준에서는 통계 정보에 대한 개념을 정의하지 않고 있다.

<a id="92c48d43cc151910"></a>
### 참조

관련 내용은 [ANALYZE SYSTEM](#34622e4780114792)을 참조한다.

<a id="213cd4dbcc8bc668"></a>
## AUDIT POLICY

<a id="a0e9b357811cc48b"></a>
### 기능

Audit policy를 활성화한다.

<a id="20ef5e22f20f0968"></a>
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

<a id="97c5efa6a8443bc2"></a>
### 사용 범위 및 접근 권한

&lt;audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="b7ad2a20dd63d1ba"></a>
### 구문 규칙 및 파라미터

<a id="de3bc16a220438b2"></a>
#### policy_name

활성화할 audit policy 객체의 이름이다.   
활성화 된 audit policy는 기존 session에 영향을 미치지 않으며 새로 생성되는 session에만 영향을 준다.

<a id="963c774775c70bd9"></a>
#### &lt;specified_user_option&gt;

감사를 수행할 사용자를 명시한다.     
생략할 경우 모든 사용자에 대해 감사를 수행한다.

동일한 audit policy에 대해 BY 절과 EXCEPT 절을 함께 사용할 수 없다.

- BY user_list: 감사를 수행할 사용자를 특정할 경우 BY 절을 사용한다.
- EXCEPT user_list: 특정 사용자를 배제하고 다른 사용자들을 감사할 경우 EXCEPT 절을 사용한다.

<a id="63c7362f9b0bbc94"></a>
#### &lt;specified_success_option&gt;

- WHENEVER SUCCESSFUL
    - Action이 성공했을 때 audit record가 생성된다.
- WHENEVER NOT SUCCESSFUL
    - Action이 실패했을 때 audit record가 생성된다.
- 생략할 경우 성공할 경우와 실패할 경우 모두 audit record를 생성한다.

<a id="88cd6d486c7d2ab7"></a>
### 설명

Audit policy를 활성화하면 기존 session에는 영향을 미치지 않으며 새로 생성되는 session에 대해 감사를 시작한다.

<a id="b6d108aea1f460e1"></a>
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

<a id="fc9cd9b173a7849e"></a>
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

<a id="04b6da0b9e28a956"></a>
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

<a id="18c4294461858b84"></a>
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

<a id="6313b5f97ee2b6dc"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="5dbd1893c3c0be4a"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](19-sql-references-c-g.md#72600ff3c559dfb5)
    - [DROP AUDIT POLICY](19-sql-references-c-g.md#1aaa5b1766ff2d59)
    - [ALTER AUDIT POLICY](#00bbcaab72bbb158)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#213cd4dbcc8bc668)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#15b6d2d5678734fb)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#18a54cc95a024f6e)

- Audit trail 소거: [ALTER DATABASE CLEAR AUDIT TRAIL](#7098d8b3ccdebf40)

---

[← 17. Built-in Function References](17-built-in-function-references.md) · [전체 목차](../README.md) · [19. SQL References (C~G) →](19-sql-references-c-g.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
