<a id="d0256248798fc649"></a>

# 18. SQL References (A~B)

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/d0256248798fc649)  
> 태그: `22c.1_10_tag`

[← 17. Built-in Function References](17-built-in-function-references.md) · [전체 목차](../README.md) · [19. SQL References (C~G) →](19-sql-references-c-g.md)

<a id="ecf2c4bd73416b17"></a>
## ALTER AUDIT POLICY

<a id="68cbba35f189f287"></a>
### 기능

Audit policy 객체에 감사 대상을 추가하거나 삭제한다.

<a id="e6cc3e3ebdafa71c"></a>
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

<a id="e370c8af19c12742"></a>
### 사용 범위 및 접근 권한

&lt;alter audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="be5cac29f6af411e"></a>
### 구문 규칙 및 파라미터

<a id="9e85aa9ca760232b"></a>
#### policy_name

변경할 audit policy 객체의 이름이다.

<a id="7079b562d416269d"></a>
#### &lt;add_audit_option&gt;

Audit policy에 감사대상을 추가한다.

<a id="6eae54450f7297ca"></a>
#### &lt;drop_audit_option&gt;

Audit policy 감사대상에서 삭제한다.

<a id="40ea6ea7f33140ce"></a>
#### &lt;privilege_audit_clause&gt;

자세한 내용은 [CREATE AUDIT POLICY](19-sql-references-c-g.md#ab7ff9504e3f6183)를 참조한다.

<a id="b84afa4daa41ece1"></a>
#### &lt;action_audit_clause&gt;

자세한 내용은 [CREATE AUDIT POLICY](19-sql-references-c-g.md#ab7ff9504e3f6183)를 참조한다.

<a id="92bd543153842faa"></a>
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

<a id="1b954fd06f53cc69"></a>
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

<a id="f0fda587bb539c5a"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="3703db76c0ec5b6e"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](19-sql-references-c-g.md#ab7ff9504e3f6183)
    - [DROP AUDIT POLICY](19-sql-references-c-g.md#69253535ad827e04)
    - [ALTER AUDIT POLICY](#ecf2c4bd73416b17)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#bdecea76b1665d44)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#f63dd37e5a743f09)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#0f5f6dd722f4b648)

- Audit trail 삭제: [ALTER DATABASE CLEAR AUDIT TRAIL](#7cfd4bf205511a5c)

<a id="4d285ac15daae9e5"></a>
## ALTER CLUSTER GROUP name ADD MEMBER

<a id="54d4dd1e79a27f34"></a>
### 기능

Cluster group에 cluster member를 추가한다.

<a id="200829604e168678"></a>
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

<a id="12037129c6f89b76"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster group add member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="b77157e1ef713270"></a>
### 구문 규칙 및 파라미터

<a id="7d287c2832625212"></a>
#### group_name

Cluster group의 이름이다.

<a id="3ca90adc0ed2f32d"></a>
#### &lt;cluster member definition&gt;

Cluster group에 포함될 cluster member를 정의한다.  
Cluster group은 최대 32 개의 cluster member를 포함할 수 있다.

<a id="3efd40369d4f69a5"></a>
#### member_name

Cluster member의 이름이다.   
Cluster member의 이름은 해당 member의 database를 생성할 때 정의한 member의 이름과 동일해야 한다.   
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.   
이름의 길이가 128 바이트보다 작아야 한다.

Cluster member의 start-up 단계가 GLOBAL OPEN이어야 한다.

<a id="42309c68af8aea41"></a>
#### &lt;connection attribute&gt;

Cluster member간 통신을 위한 연결 정보를 정의한다.   
&lt;connection attribute&gt;는 해당 member의 database를 생성할 때 정의한 HOST, PORT와 동일해야 한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 host name 또는 IPv4 주소를 사용한다. Host name을 사용할 경우 시스템의 첫 번째 IPv4 주소를 사용한다.
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="4c15eebc9361d95c"></a>
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

<a id="e67bcc2c8d997603"></a>
### 설명

&lt;alter cluster group add member statement&gt; 구문은 table들의 shard를 재배치하지 않는다.   
추가된 cluster member에 shard를 재배치하려면 다음 구문을 수행해야 한다.

- [ALTER DATABASE REBALANCE](#f07ba634c9eef9cf)
- [ALTER TABLE name REBALANCE](#149294331f00fde7)

<a id="06efed33e9874708"></a>
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

<a id="50b1af0671a6478d"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="36407bf346081be8"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#420c16ac60aa5c3d)
- [DROP CLUSTER GROUP](19-sql-references-c-g.md#6d9454a76620869e)
- [ALTER DATABASE REBALANCE](#f07ba634c9eef9cf)
- [ALTER TABLE name REBALANCE](#149294331f00fde7)

<a id="2a2456c1bfcbefea"></a>
## ALTER CLUSTER GROUP name OFFLINE MEMBER

<a id="03785d67ee62470c"></a>
### 기능

Cluster group의 cluster member를 offline 상태로 변경한다.

<a id="2085703344d619d0"></a>
### 구문

```
<alter cluster group offline member statement> ::=
    ALTER CLUSTER GROUP group_name OFFLINE CLUSTER MEMBER member_name
    ;
```

<a id="f16f641560187a22"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster group offline member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="3748b754543c1e6f"></a>
### 구문 규칙 및 파라미터

<a id="5fd939d1d48e700c"></a>
#### group_name

Cluster group의 이름이다.

<a id="ca5e417c9a79a261"></a>
#### member_name

Cluster member의 이름이다.   
Cluster member는 group_name의 cluster group에 포함돼 있어야 한다.  
Cluster member가 inactive 상태여야 한다.

<a id="31f8819c5bf204a7"></a>
### 설명

Inactive 상태인 cluster member를 offline 시킨다.

&lt;alter cluster group offline member statement&gt; 구문은 table들의 shard를 재배치하지 않는다.

<a id="03e7d6932e664542"></a>
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

<a id="dceec328deae9054"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="c7ada4e1c6b74464"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#420c16ac60aa5c3d)
- [DROP CLUSTER GROUP](19-sql-references-c-g.md#6d9454a76620869e)
- [ALTER DATABASE REBALANCE](#f07ba634c9eef9cf)
- [ALTER TABLE name REBALANCE](#149294331f00fde7)

<a id="aab1431151951450"></a>
## ALTER CLUSTER LOCATION

<a id="08ced7f5600c0bab"></a>
### 기능

Cluster location 정보를 수정한다.

<a id="02fa4aa85eedaf8f"></a>
### 구문

```
<alter cluster location statement> ::=
    ALTER CLUSTER LOCATION member_name 
    <cluster connection attribute>
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="b282159f6b55d7db"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster location statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="0b9586ae6dc9f88b"></a>
### 구문 규칙 및 파라미터

<a id="95428e366d1dcc3d"></a>
#### member_name

Cluster member의 이름이다.   
등록된 cluster location 정보에 동일한 cluster member 이름이 존재해야 한다.   
이름의 길이가 128 바이트보다 작아야 한다.

<a id="ea4b36d2866061a1"></a>
#### &lt;cluster connection attribute&gt;

Cluster member 간 통신을 위한 연결 정보를 정의한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 host name 또는 IPv4 주소를 사용한다. Host name을 사용할 경우 시스템의 첫 번째 IPv4 주소를 사용한다.
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="0b6771d0b2a18b0b"></a>
### 설명

만약 cluster location의 접속 정보가 변경될 경우에는 cluster member를 제거하거나 재생성할 필요없이 [ALTER CLUSTER LOCATION](#aab1431151951450)을 이용하여 접속 정보를 변경할 수 있다.

<a id="92abcb2ae46afc9c"></a>
### 사용 예

```
gSQL> 
ALTER CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120
;

Location altered.
```

<a id="600b42bb0abc3208"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="23fc594b002dab48"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER LOCATION](19-sql-references-c-g.md#6d43d72d687cc2a6)
- [DROP CLUSTER LOCATION](19-sql-references-c-g.md#3ed6f006ec8fc968)

<a id="b10ab041a772c5ad"></a>
## ALTER DATABASE ADD LOGFILE

<a id="1345ee8e9b6b0341"></a>
### 기능

데이터베이스에 로그파일 그룹 또는 로그파일 멤버를 추가한다.

<a id="0220f85b626ab5ee"></a>
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

<a id="62f518592a0323cf"></a>
### 사용 범위 및 접근 권한

&lt;alter database add logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="9aa44ee023ed4804"></a>
### 구문 규칙 및 파라미터

<a id="9c7a2a8d49dcab13"></a>
#### &lt;alter database add logfile statement&gt;

데이터베이스는 MOUNT 상태여야 한다.

<a id="c3cca1e950f62e11"></a>
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

<a id="29df7e35b67491b0"></a>
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

<a id="4443759220031fe7"></a>
### 설명

새로운 로그파일 그룹 및 로그 멤버가 추가되는 경우 controlfile에 저장되므로 향후 controlfile 손상에 대비해 controlfile을 백업하는 것을 권장한다.

<a id="5afafa739b1404a8"></a>
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

<a id="087c2cac0fb353e9"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="6461a251fcbc9fc1"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#b10ab041a772c5ad)
- [ALTER DATABASE DROP LOGFILE](#dac4bc732742ee95)
- [ALTER DATABASE RENAME LOGFILE](#d3da3ae37eeb2095)

<a id="7f8b32abf0b09406"></a>
## ALTER DATABASE ARCHIVELOG

<a id="6c412856b42c8256"></a>
### 기능

데이터베이스의 온라인 로그파일 archive 설정을 변경한다.

<a id="63272c2095f0221c"></a>
### 구문

```
<alter database archivelog statement> ::=
    ALTER DATABASE { ARCHIVELOG | NOARCHIVELOG }
    ;
```

<a id="10ff3170b37118be"></a>
### 사용 범위 및 접근 권한

&lt;alter database archivelog statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="4a38052f0a615e1a"></a>
### 구문 규칙 및 파라미터

<a id="9f8ef489170b7bba"></a>
#### &lt;alter database archivelog statement&gt;

- 데이터베이스가 MOUNT 상태여야 한다.
- ARCHIVELOG
    - 온라인 로그파일을 archive 한다.
- NOARCHIVELOG
    - 온라인 로그파일을 archive 하지 않는다.

<a id="c939686ee52db941"></a>
### 설명

Database를 백업하고 백업을 이용해 복구 (media recovery)하려면 시스템이 ARCHIVELOG 모드로 운용되어야 한다.

<a id="f74a66f438499d2c"></a>
### 사용 예

다음은 데이터베이스를 archive 모드로 설정하는 예이다.

```
ALTER DATABASE ARCHIVELOG;
```

<a id="a7c867e026a7d468"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="9a80d053bad9a4e8"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#213550987f436d82)
- [ALTER TABLESPACE name BACKUP](#af7c53d2132a4178)

<a id="213550987f436d82"></a>
## ALTER DATABASE BACKUP

<a id="2eedd09673f29342"></a>
### 기능

데이터베이스 전체 백업 (full backup)을 수행하기 위해 백업 상태를 'ACTIVE' 또는 'INACTIVE'로 설정한다. 그리고 데이터베이스 증분 백업 (incremental backup)과 제어 파일 (control file) 백업을 수행한다.

<a id="a56f66e344fe63f6"></a>
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

<a id="7e715e9dc9a96768"></a>
### 사용 범위 및 접근 권한

&lt;alter database backup statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="6cbda104bbeadf68"></a>
### 구문 규칙 및 파라미터

<a id="7ef76c0a77855438"></a>
#### &lt;database begin backup clause&gt;

데이터베이스를 전체 백업이 가능한 상태로 설정한다.

- 데이터베이스에서 생성되어 사용 중인 ONLINE 상태의 모든 테이블스페이스를 전체 백업이 가능한 상태로 설정한다. 
- 데이터베이스는 OPEN 상태여야 하고 ARCHIVELOG 모드로 운영되어야 한다.
- BEGIN BACKUP이 시작된 이후에는 다음과 같이 데이터 파일에 쓰기를 요구하는 연산들은 수행할 수 없다.
    - SHUTDOWN NORMAL
    - OFFLINE/ DROP TABLESPACE
    - ADD/ DROP DATAFILE
- 전체 백업의 상태가 ACTIVE인 상태에서 인스턴스가 비정상 종료될 경우, 다시 시작할 때 미디어 복구를 요구할 수도 있다.

<a id="4c4e885c5d08c125"></a>
#### &lt;database end backup clause&gt;

데이터베이스를 전체 백업 불가능한 상태로 설정한다.

- 데이터베이스에서 생성되어 사용 중인 ONLINE 상태의 모든 테이블스페이스를 백업 불가능한 상태로 설정한다.
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG 모드로 운영되어야 한다.

<a id="954ad2e196fec079"></a>
#### &lt;database incremental backup statement&gt;

- 데이터베이스 증분 백업을 수행한다.
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG로 운영되어야 한다.

<a id="b10120b008cfff1f"></a>
#### &lt;incremental backup option&gt;

- 'integer'는 0 ~ 4 까지 지정할 수 있다.
- LEVEL 0은 CUMULATIVE나 DIFFERENTIAL을 지정할 수 없다.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - 'integer'가 n이면 가장 최근에 LEVEL 0 ~ LEVEL n-1까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - DIFFERENTIAL
        - 'integer'가 n이면 가장 최근에 LEVEL 0 ~ LEVEL n까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - 생략하면 DIFFERENTIAL이 기본으로 지정된다.

<a id="21edda3a5f801ce9"></a>
#### &lt;database controlfile backup statement&gt;

- 제어 파일 (controlfile)을 백업한다.
    - 'target_name'의 이름은 1024 바이트보다 작아야 한다. 
    - 'target_name'이 이미 존재하는 경우 연산에 실패한다. 
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG로 운영되고 있어야 한다.

> GOLDILOCKS에서 관리하는 'target_name' 길이는 최대 1024 바이트이지만, OS마다 최대로 허용하는 파일 이름 길이가 다르기 때문에, 실제 생성가능한 'target_name'의 길이는 1024 바이트보다 작을 수 있다.

<a id="30abd0eb840c8d47"></a>
#### &lt;domain name&gt;

- 구문을 수행할 멤버나 그룹의 이름이다.
- 지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="537e919a69797e10"></a>
### 설명

Database의 datafile과 controlfile을 백업한다. BEGIN BACKUP을 수행한 후 OS의 파일 복사로 datafile들을 복사하고 나서 END BACKUP을 수행하여 database를 전체 백업한다. 한편, 증분 백업 파일은 하나의 구문으로 BACKUP_DIR_1 property에 설정된 경로에 생성한다.

<a id="18f7aff19cfc3147"></a>
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

<a id="ceec8b6b79218e53"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="0382964fda2e7c4c"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#af7c53d2132a4178)
- [ALTER DATABASE RECOVER](#924443216c30d2a6)

<a id="7cfd4bf205511a5c"></a>
## ALTER DATABASE CLEAR AUDIT TRAIL

<a id="032d1f26e484cf56"></a>
### 기능

Audit policy 적용으로 인해 누적된 audit record를 삭제 (purge)한다.

<a id="006a714cf0a9ff1e"></a>
### 구문

```
<clear audit trail statement> ::= 
    ALTER DATABASE CLEAR AUDIT TRAIL
;
```

<a id="7dfe4c8ce113e29f"></a>
### 사용 범위 및 접근 권한

&lt;clear audit trail statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="2dfe791c78310494"></a>
### 설명

Audit policy를 활성화하면 시간이 지남에 따라 audit trail이 계속 커진다.   
Audit trail을 구성하는 테이블들은 MEM_AUX_TBS 테이블스페이스에 저장되는데 audit trail이 계속 커지지 않도록 해야 한다.

<a id="522829a43b5b6df1"></a>
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

<a id="ea5b4d56399f05a1"></a>
### 사용 예

다음 구문을 사용하여 audit trail을 삭제 (purge)한다.

```
ALTER DATABASE CLEAR AUDIT TRAIL;
```

<a id="4f8393cdb0e6e2af"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="bb1d5a9d111650f6"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](19-sql-references-c-g.md#ab7ff9504e3f6183)
    - [DROP AUDIT POLICY](19-sql-references-c-g.md#69253535ad827e04)
    - [ALTER AUDIT POLICY](#ecf2c4bd73416b17)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#bdecea76b1665d44)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#f63dd37e5a743f09)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#0f5f6dd722f4b648)

- Audit trail 삭제: [ALTER DATABASE CLEAR AUDIT TRAIL](#7cfd4bf205511a5c)

<a id="9d473814ea059a2a"></a>
## ALTER DATABASE CLEAR PASSWORD HISTORY

<a id="b9bdf7bb2afda015"></a>
### 기능

Profile 적용에 따라 누적된 사용자의 비밀번호 변경 이력을 삭제한다.

<a id="942e60abaa9bda80"></a>
### 구문

```
<clear password history statement> ::= 
    ALTER DATABASE CLEAR PASSWORD HISTORY
    ;
```

<a id="c1fac2c6f6a12634"></a>
### 사용 범위 및 접근 권한

&lt;clear password history statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="9c9f067c9cc0208b"></a>
### 설명

User에 profile을 적용할 때 PASSWORD_REUSE_MAX, PASSWORD_REUSE_TIME의 정책에 따라 사용자의 비밀번호 변경이력이 누적된다.

**변경 이력 관리**

<a id="f78862f33d6b587b"></a>
| PASSWORD_REUSE_MAX | PASSWORD_REUSE_TIME | 변경 이력 관리 |
| --- | --- | --- |
| value | value | Value 범위 내의 변경 이력만 관리하고 범위를 벗어난 변경 이력은 자동으로 삭제한다. |
| value | UNLIMITED | 모든 변경 이력을 검사해야 하므로 변경 이력을 누적할 뿐 제거하지 않는다. |
| UNLIMITED | value | 모든 변경 이력을 검사해야 하므로 변경 이력을 누적할 뿐 제거하지 않는다. |
| UNLIMITED | UNLIMITED | 변경 이력을 검사하지 않으므로 관리도 하지 않는다. |

&lt;clear password history statement&gt; 구문은 누적된 사용자 비밀번호 변경이력을 삭제한다.

<a id="91ac798a8794428e"></a>
### 사용 예

다음은 &lt;clear password history statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE CLEAR PASSWORD HISTORY;

Database altered.

gSQL> COMMIT;

Commit complete.
```

<a id="8651ed2eb3c9be4b"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="63f902769f231aed"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE PROFILE](19-sql-references-c-g.md#7ed273ad779b6feb)
- [CREATE USER](19-sql-references-c-g.md#bcf4364429be6a9b)

<a id="4f965b5c245db523"></a>
## ALTER DATABASE DATAFILE AUTOEXTEND

<a id="cb93e216e45914ce"></a>
### 기능

디스크 테이블스페이스 데이터 파일의 자동 확장 속성을 변경한다. 자동 확장 속성을 ON으로 변경하면 확장시킬 크기와 데이터 파일의 최대 크기도 변경할 수 있다.

<a id="7af5564f8f70e8e8"></a>
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

<a id="b50418801e962b2c"></a>
### 사용 범위 및 접근 권한

&lt;alter database datafile autoextend statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

데이터 파일 자동 확장 속성은 디스크 테이블스페이스에 한해서만 변경할 수 있다.

<a id="0fbbd4c8dfd256ad"></a>
#### datafile_name

변경할 데이터 파일의 이름을 지정한다.

<a id="b9ccd04453be1c5c"></a>
#### &lt;autoextend clause&gt;

자동 확장 속성을 ON 또는 OFF로 설정한다. ON으로 설정하면 자동 확장 크기와 데이터 파일의 최대 크기를 지정할 수 있다.

<a id="08fae9536431020f"></a>
#### &lt;next size clause&gt;

현재 사용 중인 데이터 파일에 더 이상 사용할 공간이 없을 때 확장할 크기를 지정한다.

<a id="ec9ec25ef79c0d80"></a>
#### &lt;max size clause&gt;

데이터 파일이 확장될 수 있는 최대 크기를 지정한다.

<a id="167f38318209b499"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="55dc614baaa902a6"></a>
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

<a id="c1a3037417910520"></a>
### 호환성

SQL 표준에서는 데이터 파일에 대한 개념을 정의하지 않고 있다.

<a id="10ead946d0cc09ba"></a>
### 참조

관련 내용은 [CREATE DISK DATA TABLESPACE](19-sql-references-c-g.md#fbef49d9231d0d5d)를 참조한다.

<a id="b442380d12a7b286"></a>
## ALTER DATABASE DELETE BACKUP

<a id="aec3859e85e5142a"></a>
### 기능

증분 백업 (incremental backup)의 백업 정보와 백업 파일을 삭제한다. Database의 모든 증분 백업을 삭제하거나, 더 이상 쓸모 없는 백업 (obsolete backup)을 선택해서 삭제할 수 있다.

<a id="c918d004cc109de3"></a>
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

<a id="6e47854b5098c41e"></a>
### 사용 범위 및 접근 권한

&lt;alter database delete backup statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="6557749872135d61"></a>
### 구문 규칙 및 파라미터

<a id="fe1588391bebe448"></a>
#### &lt;alter database delete backup statement&gt;

데이터베이스가 MOUNT 또는 OPEN 상태여야 한다.

<a id="0d854a949f4cadf2"></a>
#### &lt;delete backup list option&gt;

기존 증분 백업들 중에서 삭제할 대상을 선정한다.

- OBSOLETE: 가장 최근의 데이터베이스 'LEVEL 0' 백업 이전에 백업한 데이터베이스 또는 테이블스페이스 백업본들을 삭제 대상으로 선정한다.
- ALL: 전체 증분 백업들을 삭제 대상으로 선정한다.

<a id="df609b6f73efc1eb"></a>
#### &lt;including backup file option&gt;

- 생략되면 백업 정보만 제어 파일에서 삭제한다.
- 백업 정보뿐만 아니라 백업 파일들도 함께 삭제한다.

<a id="26565aea2d890041"></a>
### 설명

OBSOLETE 증분 백업 삭제는 가장 최근의 LEVEL 0 데이터베이스 백업 이전의 증분 백업을 삭제한다. 즉, LEVEL 0이 아닌 증분 백업을 수행할 때는 이전에 수행한 증분 백업을 포함하는 증분 백업이 있더라도 삭제하지 않는다. 왜냐하면 증분 백업을 이용한 불완전 복구를 수행할 때 사용될 수 있기 때문이다.

> 증분 백업을 삭제할 때 백업 파일까지 함께 삭제하면 증분 백업 정보를 포함하는 백업된 controlfile을 이용하더라도 복구를 수행할 수 없으므로 주의해야 한다.

<a id="6077e6188772990b"></a>
### 사용 예

다음은 기존 모든 증분 백업들의 백업정보와 백업파일들을 삭제하는 예이다.

```
ALTER DATABASE DELETE ALL BACKUP LIST INCLUING BACKUP FILES;
```

<a id="955d3cf3072417c4"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="28579a981adbc166"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#af7c53d2132a4178)
- [ALTER DATABASE RECOVER](#924443216c30d2a6)

<a id="67f16d7dae2bf68a"></a>
## ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS

<a id="6cbca56d73cc1a1b"></a>
### 기능

모든 inactive cluster member들을 제거한다.

<a id="a7d238c90904ac26"></a>
### 구문

```
<alter database drop inactive members statement> ::=
    ALTER DATABASE DROP [ FORCE | NO FORCE ] INACTIVE CLUSTER MEMBERS
    ;
```

<a id="2c7224c37a59134d"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database drop inactive cluster members statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="0268daf3421f4b57"></a>
### 구문 규칙 및 파라미터

<a id="103e2adad19e673c"></a>
#### [ FORCE | NO FORCE ]

- FORCE
    - 데이터 유실될 수 있는 경우에도 inactive cluster member들을 제거한다.
- NO FORCE
    - 데이터가 유실될 수 있는 경우에는 inactive cluster member들을 제거할 수 없다.
- 기본값은 NO FORCE 이다.

<a id="31346a5ebd638ce8"></a>
### 설명

모든 inactive cluster member들을 제거한다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우 
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

단, cluster member를 제거할 때 table의 shard가 유실되는 경우에는 inactive cluster member를 제거할 수 없다.

또한, cluster member를 제거할 때 데이터가 유실될 수 있는 경우에는 inactive cluster member를 제거할 수 없다. 제거하려는 inactive cluster member에 속해 있는 table이나 shard의 replica가 해당 cluster group의 다른 멤버들보다 최신 데이터를 가지고 있지 않다는 보장이 있어야 데이터 유실을 방지할 수 있다. 따라서 cloned table의 경우에는 cluster 전체에, sharded table의 경우에는 같은 cluster group에 적어도 하나의 online 멤버가 존재할 경우에 inactive cluster member 제거를 허용한다.

단, cluster group에 online 상태인 cluster member가 없고 inactive cluster member로 인해 서비스가 불가능한 경우에는 데이터 유실을 감수하면서 FORCE 옵션을 통해 inactive cluster member를 제거할 수 있다.

&lt;alter database drop inactive members statement&gt; 구문은 모든 inactive cluster member들이 더 이상 cluster system에 포함될 수 없는 경우에 사용하는 것이 바람직하다.

<a id="eaf0b5101ff50dd6"></a>
### 사용 예

다음은 &lt;alter database drop inactive members statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="ff107c7f6d400e8e"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="8bb9c9d3330575c7"></a>
### 참조

관련 내용은 [ALTER SYSTEM JOIN DATABASE](#8b48c6e044e9469c) 를 참조한다.

<a id="dac4bc732742ee95"></a>
## ALTER DATABASE DROP LOGFILE

<a id="c592fa080d71f67b"></a>
### 기능

데이터베이스에 존재하는 로그파일 그룹이나 멤버를 제거한다.

<a id="5d0bb3e03502929c"></a>
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

<a id="5bfe3cfc5110cf31"></a>
### 사용 범위 및 접근 권한

&lt;alter database drop logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="75afb64b309301f8"></a>
### 구문 규칙 및 파라미터

<a id="c85590f3e4b6567c"></a>
#### &lt;alter database drop logfile statement&gt;

데이터베이스는 MOUNT 상태여야 한다.   
제거하려는 로그파일이 CURRENT 또는 ACTIVE 상태일 때는 에러가 발생한다.   
제거한 후에 최소 네 개의 로그파일 그룹이 남아 있어야 한다.

<a id="e801b1a7851998f6"></a>
#### &lt;drop logfile group statement&gt;

기존의 로그파일 그룹을 제거한다.

- &lt;group clause&gt; 
    - 제거할 로그파일 그룹을 지정한다.
    - integer는 존재하는 로그파일의 식별자여야 한다. 
    - integer가 존재하지 않을 경우 에러가 발생한다.

<a id="2eda6d1327b948f4"></a>
#### &lt;drop logfile member statement&gt;

기존의 로그파일 멤버들을 제거한다.

- &lt;logfile_list&gt;
    - 제거할 로그파일 멤버의 목록이다.
    - 'logfile_name'은 존재하는 이름이어야 한다. 
    - 'logfile_name'이 존재하지 않을 경우 에러가 발생한다.

<a id="720661ab2c4e9914"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="4cce85bb448b6e45"></a>
### 사용 예

다음은 기존 로그파일인 GROUP 3을 제거하는 예이다.

```
ALTER DATABASE DROP LOGFILE GROUP 3;
```

다음은 기존 로그파일인 GROUP 3에서 'logfile1.log'와 'logfile2.log'를 제거하는 예이다.

```
ALTER DATABASE DROP LOGFILE MEMBER 'logfile1.log', 'logfile2.log';
```

<a id="e27136bdf4d9ae38"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="d209137c0cc4633a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#b10ab041a772c5ad)
- [ALTER DATABASE RENAME LOGFILE](#d3da3ae37eeb2095)

<a id="a56d9b8313449047"></a>
## ALTER DATABASE DROP OFFLINE SEGMENTS

<a id="710abfc02218a774"></a>
### 기능

모든 테이블에 대해서 오프라인 된 shard들의 세그먼트를 삭제한다.

<a id="6364cef7f327f2c5"></a>
### 구문

```
<alter database drop offline segments statement> ::=
    ALTER DATABASE DROP OFFLINE SEGMENTS 
    ;
```

<a id="466c9925e0cb8c6a"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database drop offline segments statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="858ea86b52649bf1"></a>
### 설명

모든 테이블에 대해서 오프라인 된 shard들의 세그먼트를 삭제하는데 inactive cluster member가 있어도 수행할 수 있다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우 
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

&lt;alter database drop offline segments statement&gt;는 각 테이블마다 [&lt;alter table drop offline segments statement&gt;](#12188ac1593e923a)를 수행하며 다음과 같은 질의의 합과 동치이다.

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

위 에러 메세지는 다섯 개의 테이블 중에서 한 개의 테이블이 실패했다는 의미이다.

이후 에러에 대해 적절한 조치를 취한 후 &lt;alter database drop offline segments statement&gt; 구문을 다시 수행하면 실패했던 테이블에 대해서만 해당 구문이 다시 수행된다.

에러에 대한 자세한 내용은 구문을 수행한 멤버의 시스템 트레이스 로그 (system.trc)를 참조한다.

<a id="45b1f81da70494c2"></a>
### 사용 예

다음은 &lt;alter database drop offline segments statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE DROP OFFLINE SEGMENTS;

Database altered.
```

<a id="9685097ed133f1b5"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="baa5742aeffa358d"></a>
### 참조

관련 내용은 [ALTER TABLE name DROP OFFLINE SEGMENTS](#12188ac1593e923a)를 참조한다.

<a id="5068226dae906bd2"></a>
## ALTER DATABASE MOVE SHARD

<a id="eb5ff7277f7179af"></a>
### 기능

특정 cluster group의 모든 table들의 shard를 다른 cluster group으로 재배치한다.

<a id="4ce2b01661570a27"></a>
### 구문

```
<alter database move shard statement> ::=
    ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP src_cluster_group
        TO CLUSTER GROUP dest_cluster_group 
       [ ONLINE | OFFLINE ] 
       [ <shard divisor> ] 
       [ <parallel clause> ]
    ;

<shard divisor> ::= 
    SHARD DIVISOR integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="693ae3a7e4f1a088"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database move shard statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="2953593935378715"></a>
### 구문 규칙 및 파라미터

<a id="d0d9a85d615d5c43"></a>
#### src_cluster_group

테이블의 shard를 이동할 cluster group 이다.

<a id="f20121168b736ddd"></a>
#### dest_cluster_group

테이블의 shard를 이동시킬 target cluster group이다.

<a id="2ce5d23ebaf92f35"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="1ff1c822b8df49a0"></a>
#### &lt;shard divisor&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버에 재배치 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, REBALANCE_SHARD_DIVISOR 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="554b774bee95093b"></a>
#### &lt;parallel clause&gt;

테이블 재배치에 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 병렬로 테이블을 재배치하지 않는다.
- PARALLEL [integer] 
    - 병렬로 테이블을 재배치한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="1e79fd166e043f0b"></a>
### 설명

다음과 같은 구문을 사용하여 cluster member와 cluster group을 추가할 때 table들의 shard는 재배치하지 않는다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#420c16ac60aa5c3d)
- [ALTER CLUSTER GROUP name ADD MEMBER](#4d285ac15daae9e5)

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

<a id="8eea899c35232b8f"></a>
### 사용 예

다음은 &lt;alter database move shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP G1 TO CLUSTER GROUP G2;

Database altered.
```

<a id="e1e9c662b3569ffd"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="d30d3846076deadd"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name MOVE SHARD](#a93d376fd2ef5b9b)
- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#420c16ac60aa5c3d)
- [ALTER CLUSTER GROUP name ADD MEMBER](#4d285ac15daae9e5)

<a id="46fc9da08c6b6b44"></a>
## ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS

<a id="bb4638f78a91c35c"></a>
### 기능

모든 inactive cluster member들을 offline 상태로 변경한다. 즉, 해당 cluster member들에 대한 shard map을 offline 상태로 변경한다.

<a id="f62bd6656c9d20fe"></a>
### 구문

```
<alter database offline inactive cluster members statement> ::=
    ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS
    ;
```

<a id="3a954126fabda46f"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database offline inactive cluster members statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="76b250ed84439f09"></a>
### 구문 규칙 및 파라미터

모든 inactive cluster member들을 offline 상태로 변경한다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

<a id="8583632d825399cb"></a>
### 설명

&lt;alter database offline inactive members statement&gt; 구문은 모든 inactive cluster member들이 더 이상 cluster system에 포함될 수 없는 경우에 사용하는 것이 바람직하다.

Inactive cluster member가 cluster system에 참여할 수 있으면 [ALTER SYSTEM JOIN DATABASE](#8b48c6e044e9469c) 구문을 수행하여 cluster system에 포함시킨다.

Offline 상태로 변경된 cluster member는 join 후에 다음 구문을 사용하여 online 상태로 다시 변경할 수 있다

- [ALTER DATABASE REBALANCE](#f07ba634c9eef9cf)
- [ALTER TABLE name REBALANCE](#149294331f00fde7)

<a id="4da81310c4eb4c2e"></a>
### 사용 예

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;
```

<a id="41314c604c27ab0a"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="efd037263b5cc5f8"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER SYSTEM JOIN DATABASE](#8b48c6e044e9469c)
- [ALTER DATABASE REBALANCE](#f07ba634c9eef9cf)
- [ALTER TABLE name REBALANCE](#149294331f00fde7)

<a id="f07ba634c9eef9cf"></a>
## ALTER DATABASE REBALANCE

<a id="4ab1dd9261e5d896"></a>
### 기능

모든 table들의 shard를 재배치한다.

<a id="f95cc7ac69454ec1"></a>
### 구문

```
<alter database rebalance statement> ::=
    ALTER DATABASE REBALANCE
       [ ONLINE | OFFLINE ] 
       [ <shard divisor> ] 
       [ <parallel clause> ]
    ;

<shard divisor> ::= 
    SHARD DIVISOR integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="47c5d4a9135bbe67"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database rebalance statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="647660c71fad098d"></a>
### 구문 규칙 및 파라미터

<a id="a7506e5b596d7327"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="5f9d7ad584c227ce"></a>
#### &lt;shard divisor&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버에 재배치 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, REBALANCE_SHARD_DIVISOR 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="211ff5ce3e621ac6"></a>
#### &lt;parallel clause&gt;

테이블 재배치에 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 병렬로 테이블을 재배치하지 않는다.
- PARALLEL [integer] 
    - 병렬로 테이블을 재배치한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="5682ced12bdff363"></a>
### 설명

다음과 같은 구문을 사용하여 cluster member, cluster group을 추가할 때 table들의 shard를 재배치하지 않는다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#420c16ac60aa5c3d)
- [ALTER CLUSTER GROUP name ADD MEMBER](#4d285ac15daae9e5)

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

<a id="3fde9bb47628e2dc"></a>
### 사용 예

다음은 &lt;alter database rebalance statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE REBALANCE;

Database altered.
```

<a id="d7b8588e180ab112"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="f1b165cb9f415d4b"></a>
### 참조

관련 내용은 [ALTER TABLE name REBALANCE](#149294331f00fde7)를 참조한다.

<a id="66647a34894da55f"></a>
## ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP

<a id="07a10f210a2d40d8"></a>
### 기능

특정 cluster group에 shard가 포함되지 않도록 모든 테이블의 shard를 재배치한다.

<a id="107ead195d722916"></a>
### 구문

```
<alter database rebalance exclude cluster group statement> ::=
    ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP cluster_group_name        
       [ ONLINE | OFFLINE ]        
       [ <shard divisor> ]        
       [ <parallel clause> ]
    ;

<shard divisor> ::= 
    SHARD DIVISOR integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="333769bc29313c31"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database rebalance exclude cluster group statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="1366a9d6c8fc6b08"></a>
### 구문 규칙 및 파라미터

<a id="f6a70e109db65b81"></a>
#### cluster_group_name

테이블들의 shard를 포함하지 않는 cluster group의 이름이다.  
지정한 cluster group이 유일한 cluster group인 경우 구문을 수행할 수 없다.

<a id="95a03ea05906358f"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="fca4166711dbc1fb"></a>
#### &lt;shard divisor&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버에 재배치 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, REBALANCE_SHARD_DIVISOR 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="2276a5d868d98625"></a>
#### &lt;parallel clause&gt;

테이블 재배치에 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 병렬로 테이블을 재배치하지 않는다.
- PARALLEL [integer] 
    - 병렬로 테이블을 재배치한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="628b0dd2ca02ad7f"></a>
### 설명

[DROP CLUSTER GROUP](19-sql-references-c-g.md#6d9454a76620869e) 구문을 사용하여 cluster group을 제거하려면 해당 cluster group에 shard가 존재하지 않아야 한다.

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

<a id="05aa293d9fc62235"></a>
### 사용 예

다음은 &lt;alter database rebalance exclude cluster group statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP g3;

Database altered.
```

<a id="4b5570afcc530cc0"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="04511012039b121a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP CLUSTER GROUP](19-sql-references-c-g.md#6d9454a76620869e)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#21c0fa70c04ce272)

<a id="924443216c30d2a6"></a>
## ALTER DATABASE RECOVER

<a id="f073e9d1e82db22c"></a>
### 기능

온라인/ archive log file을 사용하여 데이터베이스 내의 전체 데이터파일 (datafile) 또는 일부 데이터파일을 복구한다.

<a id="290b778729736eab"></a>
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

<a id="0d4bd9ecf4925980"></a>
### 사용 범위 및 접근 권한

&lt;alter database recover statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="3f5ec01dab59a62a"></a>
### 구문 규칙 및 파라미터

<a id="a946b995803ea2c9"></a>
#### &lt;complete database recover statement&gt;

온라인 및 archive 로그파일을 이용하여 데이터베이스의 데이터 파일들을 최신상태로 복구한다.

- ONLINE 상태의 모든 테이블스페이스를 복구한다. 
- 데이터베이스는 MOUNT 상태여야하고, ARCHIVELOG 모드여야 한다. 
- 필요한 archive log file이 존재하지 않으면 실패한다.

<a id="f2759844b6192b6d"></a>
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

<a id="133626379e2ed8a5"></a>
#### &lt;complete tablespace recover statement&gt;

테이블스페이스의 데이터 파일들을 최신 상태로 복구한다.

- 테이블스페이스를 복구하려면 데이터베이스가 MOUNT 또는 OPEN 상태여야 한다. 
- OPEN 상태에서의 복구는 OFFLINE 상태의 테이블스페이스만 가능하고, MOUNT 상태에서의 복구는 ONLINE/ OFFLINE 상태의 테이블스페이스 모두 가능하다. 
- 필요한 archive log file이 존재하지 않으면 복구에 실패한다.
- 다음과 같은 경우에는 테이블스페이스 복구 연산이 필요하다.
    - IMMEDIATE 로 OFFLINE 된 테이블스페이스
    - 백업된 데이터 파일을 이용해야 하는 경우
    - 전체 백업중 장애가 발생한 경우

<a id="4fe4205cd2574637"></a>
#### &lt;incomplete database recover statement&gt;

<a id="fb646704252f5fb5"></a>
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

<a id="78277dc7d63216d4"></a>
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

<a id="41ef58ebbeeb4d37"></a>
### 설명

데이터베이스 불완전 복구는 복구 완료 시점을 한 번에 찾아내기 어려우므로 여러 번 수행하여 원하는 복구 시점을 찾아야 한다. 그런데 불완전 복구가 완료된 후 RESETLOGS 옵션으로 데이터베이스를 기동하면 새로운 데이터베이스가 되기 때문에 archive log file과 온라인 redo log file에 대한 복사본을 만든 후에 불완전 복구를 여러 번 수행해야 한다.

<a id="958a9cf7a885fb4a"></a>
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

<a id="00bfb9d56b08d234"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="bad2303f74c127b0"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#213550987f436d82)
- [ALTER TABLESPACE name BACKUP](#af7c53d2132a4178)
- [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#02b4e61c7b426491)

<a id="aef6c2166d9cd104"></a>
## ALTER DATABASE REGISTER

<a id="c463b87af9fc0f84"></a>
### 기능

복구 불가능한 세그먼트를 데이터베이스에 등록한다.

<a id="9f00caa1caaa49b5"></a>
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

<a id="1a5ac4ac506f8b78"></a>
### 사용 범위 및 접근 권한

&lt;alter database register statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="d14dafae2b4d7195"></a>
### 구문 규칙 및 파라미터

<a id="bbef6661f0acd538"></a>
#### &lt;alter database register statement&gt;

복구 불가능한 세그먼트를 데이터베이스에 등록한다. 해당 구문은 백업이 존재하지 않고 데이터베이스를 복구할 수 없는 경우, 세그먼트를 더 이상 사용하지 않는다는 가정하에 사용될 수 있다.

- 데이터베이스가 MOUNT 상태여야 한다.
- 등록된 세그먼트 식별자 목록은 재시작할 때 초기화된다.
- 서버 재시작에 성공하면 등록된 세그먼트들이 'UNUSABLE' 상태가 되는데 해당 세그먼트들은 반드시 삭제해야 한다.

<a id="cad6c783a67d530b"></a>
#### &lt;segment physical identifier list&gt;

복구 불가능한 세그먼트의 식별자 목록이다.  
• Integer: 8 바이트 정수형의 세그먼트 식별자

<a id="fa93dde7e301d616"></a>
### 설명

서버를 비정상 종료하고 재시작할 때 데이터베이스를 복구하는데, 이 때 이전 서비스 단계에서 디스크에 반영되지 못한 페이지들을 복구하기 위해서 REDO 로그들을 이용해 페이지를 다시 수행한다.

REDO 연산을 수행하는 중에 예상하지 못한 실패가 발생한 경우, 이를 무시하고 복구하기 위해 사용될 수 있다.

<a id="5f8732025f6c427b"></a>
### 사용 예

다음은 4028679323648을 식별자로 갖는 세그먼트 복구를 포기하는 예이다.

```
ALTER DATABASE REGISTER IRRECOVERABLE SEGMENT 4028679323648;
```

<a id="3b00d8829bd8a1cf"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="8cee99f5ba9d3653"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#af7c53d2132a4178)
- [ALTER DATABASE RECOVER](#924443216c30d2a6)

<a id="bc461c405e500d40"></a>
## ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE

<a id="9ca38e13f2487f13"></a>
### 기능

데이터베이스에서 글로벌 트랜잭션 로그파일의 이름을 수정한다.

<a id="7f9aef128ac22064"></a>
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

<a id="9458f50e1464471c"></a>
### 사용 범위 및 접근 권한

&lt;alter database rename global transaction logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="b2adde41afdef85d"></a>
### 구문 규칙 및 파라미터

<a id="4fcc3afa6fa58085"></a>
#### &lt;alter database rename global transaction logfile statement&gt;

- 데이터베이스는 MOUNT 상태여야 한다.
- source_clause
    - 데이터베이스에서 수정될 글로벌 트랜잭션 로그파일 목록이다.
- target_clause
    - 데이터베이스에서 수정될 글로벌 트랜잭션 로그파일 목록이다.
    - 파일이 존재하지 않을 경우 에러가 발생한다.
    - 경로를 포함한 이름의 길이는 1024 바이트보다 작아야 한다.

<a id="05ebd299dae2d6ae"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="272aa9d241a77b4b"></a>
### 사용 예

다음은 글로벌 트랜잭션 로그파일을 변경하는 예이다.

```
ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE
 'org_commit_0.log', 'org_commit_1.log' TO 'new_commit_0.log', 'new_commit_1.log';
```

<a id="eaef80ab6e8fb3b9"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="3e8c659003861cf1"></a>
### 참조

관련 내용은 [ALTER DATABASE RENAME LOGFILE](#d3da3ae37eeb2095)을 참조한다.

<a id="d3da3ae37eeb2095"></a>
## ALTER DATABASE RENAME LOGFILE

<a id="96f1c70553926997"></a>
### 기능

데이터베이스에서 로그파일의 이름을 수정한다.

<a id="cc917314ba47699b"></a>
### 구문

```
<alter database rename logfile statement> ::=
    ALTER DATABASE RENAME LOGFILE <logfile_list> TO <logfile_list>
    ;

<logfile_list> ::=
      'logfile_name'
    | <logfile_list> , 'logfile_name'
```

<a id="1c7e7c2cff812ccd"></a>
### 사용 범위 및 접근 권한

&lt;alter database rename logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="9f20af1d4137e46b"></a>
### 구문 규칙 및 파라미터

<a id="7c0ff67b933971cb"></a>
#### &lt;alter database rename logfile statement&gt;

- 데이터베이스는 MOUNT 상태여야 한다.
- FROM &lt;logfile_list&gt;
    - 데이터베이스에서 수정할 로그파일들의 이름 목록이다.
- TO &lt;logfile_list&gt;
    - 데이터베이스에서 수정될 로그파일들의 이름 목록이다.
    - &lt;logfile_list&gt;는 존재하는 파일이어야 한다. 
    - 파일이 존재하지 않을 경우 에러가 발생한다.

<a id="d2fd5eaa0667d17e"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="f32499b708d4764a"></a>
### 사용 예

다음은 기존 로그파일 'logfile.log'를 'newlogfile.log'로 변경하는 예이다.

```
ALTER DATABASE RENAME LOGFILE 'logfile.log' TO 'newlogfile.log';
```

<a id="844f9fc73329af10"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="f345761582062cdd"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#b10ab041a772c5ad)
- [ALTER DATABASE DROP LOGFILE](#dac4bc732742ee95)

<a id="23aff049d14e4535"></a>
## ALTER DATABASE RESET LOCAL CLUSTER MEMBER

<a id="7c091df8df6aadc2"></a>
### 기능

Local cluster member에서 tablespace 객체를 제외한 부분을 database 생성 시점으로 초기화한다.

<a id="6ec625597cd853d6"></a>
### 구문

```
<alter database reset local cluster member statement> ::=
    ALTER DATABASE RESET LOCAL CLUSTER MEMBER
    ;
```

<a id="a053408ae12d1d30"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

Start-up 과정 중 LOCAL OPEN 단계에서 수행할 수 있다.

&lt;alter database reset local cluster member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="881e5927e990bf09"></a>
### 설명

Local cluster member에서 tablespace 객체를 제외한 부분을 database 생성 시점으로 초기화한다.  
Tablespace 객체를 제외하고 사용자가 생성한 모든 객체를 제거한다.

&lt;alter database reset local cluster member statement&gt; 구문은 inactive cluster member를 초기화하고,  
새로운 cluster member를 cluster system에 참여시키기 위해 사용한다.  
Cluster system과 연결이 끊긴 inactive cluster member들은 다음과 같이 처리할 수 있다.

- Cluster system에 다시 참여할 수 있는 경우, JOIN 구문을 이용하여 참여시킨다. 
    - [ALTER SYSTEM JOIN DATABASE](#8b48c6e044e9469c) 
- Cluster system에 다시 참여할 수 없는 경우, DROP 구문을 이용하여 cluster system에서 제외한다. 
    - [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#67f16d7dae2bf68a)

이 때, cluster system에서 제외된 cluster member에 해당하는 장비는 다음 두 가지 방법으로 재사용할 수 있다.

- 방법 1: Local cluster member의 database를 다시 생성한다.
- 방법 2: &lt;alter database reset local cluster member statement&gt; 구문을 이용해 local cluster member를 초기화한다.

방법 2는 방법 1보다 tablespace를 재생성하는 비용을 줄일 수 있다.

<a id="024b556f3abf3084"></a>
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

<a id="4a2a243ac1e9dad9"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="878259fb04b82b55"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER SYSTEM JOIN DATABASE](#8b48c6e044e9469c)
- [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#67f16d7dae2bf68a)

<a id="3776af523298373f"></a>
## ALTER DATABASE RESTORE

<a id="0ade4e31a9e2de66"></a>
### 기능

증분 백업을 이용하여 데이터베이스 또는 테이블스페이스 내의 데이터 파일들을 복원한다.

<a id="47ad783a771b94f9"></a>
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

<a id="8c89c362624aa06a"></a>
### 사용 범위 및 접근 권한

&lt;alter database restore statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="e0a820f9b68b1b6a"></a>
### 구문 규칙 및 파라미터

<a id="63ec11fd5ff56dbf"></a>
#### &lt;database restore statement&gt;

증분 백업을 사용하여 데이터베이스 내의 데이터 파일들을 복원한다.   
데이터베이스가 MOUNT 상태여야 한다.

<a id="61783ccf62683c30"></a>
#### &lt;tablespace restore statement&gt;

증분 백업을 사용하여 테이블스페이스 내의 데이터 파일들을 복원한다.

- 데이터베이스가 MOUNT 또는 OPEN 상태여야 한다. 
- OPEN 상태에서는 OFFLINE 상태의 테이블스페이스만 복원할 수 있고, MOUNT 상태에서는 ONLINE/ OFFLINE 상태의 테이블스페이스 모두 복원할 수 있다.

<a id="918ec10e963a3968"></a>
#### &lt;controlfile restore statement&gt;

'file_name'을 사용하여 제어파일을 복원한다.

- 데이터베이스가 NOMOUNT 상태여야 한다.
- 'file_name'은 절대 경로를 권장하지만, 만약 상대 경로를 기술한 경우에는 &lt;GOLDILOCKS_HOME&gt;/wal/'file_name'을 이용한다.

<a id="7d7bca9dc5b04371"></a>
### 설명

전체 백업을 이용한 데이터 파일 복원은 OS 복사 명령으로 백업된 파일을 직접 데이터 파일 경로에 복사하는 방법이다. 증분 백업을 이용한 데이터 파일 복원은 삭제된 데이터 파일이나 이전 데이터 파일들만 복원한다.

<a id="973efcb058c6a0cb"></a>
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

<a id="5bc61249518d10f5"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="dc71e094680b330a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#213550987f436d82)
- [ALTER TABLESPACE name BACKUP](#af7c53d2132a4178)
- [ALTER DATABASE RECOVER](#924443216c30d2a6)

<a id="7358cd448c66ad8b"></a>
## ALTER DATABASE SYNCHRONIZE

<a id="f4f03212bddeade9"></a>
### 기능

모든 테이블의 shard들과 시퀀스들을 원격으로 동기화한다.

<a id="2ac4162b2ea0c8fb"></a>
### 구문

```
<alter database synchronize statement> ::=
    ALTER DATABASE SYNCHRONIZE 
       [ <synchronize target> ] 
       [ ONLINE | OFFLINE ] 
       [ <shard divisor> ] 
       [ <parallel clause> ]
    ;

<synchronize target> ::= 
    TABLE
  | SEQUENCE
  | TABLE AND SEQUENCE
  | SEQUENCE AND TABLE

<shard divisor> ::= 
    SHARD DIVISOR integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="def45e6a096c95bf"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database synchronize statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="4ebe08f70d0e0648"></a>
### 구문 규칙 및 파라미터

<a id="90b633ebd27e74bb"></a>
#### &lt;synchronize target&gt;

동기화 대상 객체를 지정한다.

- TABLE
    - 테이블 객체를 동기화한다.
- SEQUENCE
    - 시퀀스 객체를 동기화한다. 
- TABLE AND SEQUENCE 또는 SEQUENCE AND TABLE
    - 테이블과 시퀀스 객체를 동기화한다.
- 생략할 경우, 기본값은 TABLE AND SEQUENCE 이다.

<a id="358cb0e27ec6881a"></a>
#### [ ONLINE | OFFLINE ]

동기화 수행시 DML을 허용할지 여부를 결정한다

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="e6391dff34630da9"></a>
#### &lt;shard divisor&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버와 동기화 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, REBALANCE_SHARD_DIVISOR 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

&lt;synchronize target&gt;에 SEQUENCE만 지정될 경우, 이는 무시된다.

<a id="663aa8cda793c482"></a>
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

<a id="070e3e7ba22c2124"></a>
### 설명

기존에 배치되어 있는 모든 오프라인된 shard와 시퀀스들을 동기화하고 온라인으로 변경한다. [ALTER DATABASE REBALANCE](#f07ba634c9eef9cf)와는 달리 inactive cluster member가 있어도 수행할 수 있다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우 
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

&lt;alter database synchronize statement&gt;는 각 테이블마다 [&lt;alter table synchronize statement&gt;](#c03af2d66eb7e9c7)를 수행하며 다음과 같은 질의의 합과 동치이다.

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

위 에러 메세지는 다섯 개의 테이블 중에서 한 개의 테이블이 실패했다는 의미이다.

이후 에러에 대해 적절한 조치를 취한 후 &lt;alter database synchronize statement&gt; 구문을 다시 수행하면 실패했던 테이블에 대해서만 진행된다.

자세한 에러는 구문을 수행한 멤버의 시스템 트레이스 로그(system.trc)를 참조한다.

<a id="2583353ace178edb"></a>
### 사용 예

다음은 &lt;alter database synchronize statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE SYNCHRONIZE;

Database altered.
```

<a id="3a8c59f28355c389"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="fcdf20ccf75cd9ad"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE REBALANCE](#f07ba634c9eef9cf)
- [ALTER TABLE name REBALANCE](#149294331f00fde7)

<a id="bb66b410758193b8"></a>
## ALTER INDEX

<a id="8be743c6c8c4cb24"></a>
### 기능

인덱스 정의를 변경한다.

<a id="1c9fd8454916f2e3"></a>
### 구문

```
<alter index statement> ::=
      <alter index physical attribute statement>
    | <rename index statement>
    | <aging index statement>
    | <rebuild index statement>
    | <index coalesce statement>
    ;
```

<a id="8b955914b07be51c"></a>
### 사용 범위 및 접근 권한

&lt;alter index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="bac4e9bdadfc5fb5"></a>
### 구문 규칙 및 파라미터

<a id="fb46dd30c16578fc"></a>
#### &lt;alter index physical attribute statement&gt;

인덱스의 물리적 속성을 변경한다.  
자세한 내용은 [ALTER INDEX name STORAGE](#67de286d3b392ca2) 구문을 참조한다.

<a id="dd884848ac1fd9cb"></a>
#### &lt;rename index statement&gt;

인덱스 이름을 변경한다.  
자세한 내용은 [ALTER INDEX name RENAME TO](#b3aaf811285301ef) 구문을 참조한다.

<a id="e4fb5d743a944256"></a>
#### &lt;aging index statement&gt;

인덱스의 빈 페이지를 삭제한다.  
자세한 내용은 [ALTER INDEX name AGING](#0e6b8d0d021cbc1e) 구문을 참조한다.

<a id="d4830c5b71113342"></a>
#### &lt;rebuild index statement&gt;

인덱스를 재구축한다.  
자세한 내용은 [ALTER INDEX name REBUILD](#fd0259278148017d) 구문을 참조한다.

<a id="967bbeb718f84c5d"></a>
#### &lt;index coalesce statement&gt;

인덱스 단편화를 제거한다.  
자세한 내용은 [ALTER INDEX name COALESCE](#3d86f77f4b086a49) 구문을 참조한다.

<a id="4a4f0403746c3fd5"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="35e280715ed8a30c"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="873a963ec6d3eac7"></a>
### 호환성

SQL 표준에서는 인덱스에 대한 개념을 다루지 않고 있다.

<a id="0e6b8d0d021cbc1e"></a>
## ALTER INDEX name AGING

<a id="fcb390ab89febb8c"></a>
### 기능

인덱스의 빈 페이지를 삭제한다. DML과 동시에 수행할 수 있다.

<a id="c3825e83a114e608"></a>
### 구문

```
<aging index statement> ::=
    ALTER INDEX index_name AGING
    ;
```

<a id="5b03afa8161792b3"></a>
### 사용 범위 및 접근 권한

&lt;aging index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="fb75bc8f73ed1ed1"></a>
### 구문 규칙 및 파라미터

<a id="ebe60594d660b994"></a>
#### index_name

대상 인덱스의 이름이다.

<a id="1ddbed2962c5be8a"></a>
### 설명

해당 구문은 인덱스 페이지들 중에 모든 키가 삭제된 페이지들을 세그먼트로 반납한다. Aging은 논리적 삭제와 물리적 삭제의 2단계로 진행된다. 논리적 삭제는 인덱스에서 페이지를 지칭하는 연결을 끊는 작업인데 페이지의 마지막 키를 삭제할 당시의 SCN이 시스템의 agable SCN보다 작을 때 이 작업이 수행된다. 이 후 물리적 삭제가 이루어지는데 논리적으로 삭제할 때의 SCN이 시스템의 agable SCN 보다 작을 때 이 작업이 수행된다.

> 만약 시스템의 agable SCN이 증가하지 않으면 인덱스 AGING 구문이 성공하더라도 빈 페이지가 삭제되지 않을 수 있다.

<a id="59dd78c00a09bbdd"></a>
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

<a id="2af963b4b2a17fa9"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="b9e54900bc979082"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](19-sql-references-c-g.md#04e7730c239ac562)
- [ALTER INDEX](#bb66b410758193b8)
- [DROP INDEX](19-sql-references-c-g.md#d20adfa902b88837)

<a id="3d86f77f4b086a49"></a>
## ALTER INDEX name COALESCE

<a id="a117d0d250ab53b6"></a>
### 기능

인덱스의 인접한 leaf page들을 병합하여 인덱스의 사용 공간을 줄인다. DML과 동시에 수행할 수 있다.

<a id="db1af1ccadca9d78"></a>
### 구문

```
<index coalesce statement> ::=
    ALTER INDEX index_name COALESCE
    ;
```

<a id="b6f1faddcdf202a8"></a>
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

<a id="48c5a2b763b99bee"></a>
### 구문 규칙 및 파라미터

<a id="eebe9bc8be29b3bf"></a>
#### index_name

대상 인덱스의 이름이다.  
스키마 이름을 명시할 수 있으며, 생략할 경우 사용자의 기본 스키마 이름이 사용된다.

<a id="9a7bf1d35b98260a"></a>
### 설명

<a id="b050cc0a076b3d3e"></a>
![Index coalesce](../assets/images/4e253a6e00870b20.png)

- leaf 페이지들을 순차적으로 탐색하여 병합 가능한 페이지들을 병합하고, 제거된 페이지들을 세그먼트로 반환한다.
- UPDATE/ DELETE 등으로 인해 발생한 leaf 페이지의 단편화 문제를 해결할 수 있다.
- 유효하지 않은 shard와 관련된 key들을 제거하고 shard sequence 제한을 풀어준다.
- 인접한 leaf 페이지들이 병합 가능한 경우에만 동작하므로 단편화 정도가 낮은 상태에서는 효과가 없을 수 있다.
- 인덱스의 단편화 정도가 심한 경우 INDEX REBUILD보다 더 오래 걸릴 수 있다.

**INDEX REBUILD와 비교**

<a id="8d7f199fd0132257"></a>
|  | INDEX REBUILD | INDEX COALESCE |
| --- | --- | --- |
| 인덱스 속성 변경 | 가능 | 불가능 |
| 테이블스페이스 이동 | 가능 | 불가능 |
| 테이블 잠금 | 필요 | 불필요 |
| 수행을 위한 추가 공간 | 필요 | 불필요 |
| 트리 높이 감소 | 가능 | 불가능 |

<a id="39a74f36f8b38f81"></a>
### 사용 예

```
gsql> ALTER INDEX T1X COALESCE;

Index altered.
```

<a id="29e59e9a083ed62d"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="076477af5e9e8d85"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER INDEX](#bb66b410758193b8)
- [ALTER INDEX REBUILD](#fd0259278148017d)

<a id="fd0259278148017d"></a>
## ALTER INDEX name REBUILD

<a id="51bb12faee9bae92"></a>
### 기능

인덱스를 재구축한다.

<a id="b53a8f05c1cf5bae"></a>
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

<a id="081e4dd0d9f355a9"></a>
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

<a id="1918ec7c845c5367"></a>
### 구문 규칙 및 파라미터

<a id="5609a79eb9fffef0"></a>
#### index_name

대상 인덱스의 이름이다.  
스키마 이름을 명시할 수 있으며, 생략할 경우 사용자의 기본 스키마 이름이 사용된다.

<a id="2c4061d572d3ac9e"></a>
#### [ ONLINE | OFFLINE ]

인덱스를 재구축할 때, 해당 테이블에 DML을 허용할지 여부를 결정한다.

- ONLINE
    - INSERT, UPDATE, DELETE를 허용한다.
- OFFLINE
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE이다.

<a id="4ac6d2176b3dca14"></a>
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

<a id="169f07e0daddc8cb"></a>
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

<a id="d6f3eb724728d62f"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="9e6beeb1cf94b521"></a>
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

<a id="e0938dc016041e9e"></a>
#### TABLESPACE tablespace_name

인덱스가 재구축될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - tablespace_name이 data tablespace면 LOGGING 인덱스로 재구축된다.
    - tablespace_name이 temporary tablespace 또는 nologging tablespace면 NOLOGGING 인덱스로 재구축된다.
- TABLESPACE 절을 생략할 경우, 기존 인덱스의 tablespace로 설정된다.

<a id="ad775c62a8eee44a"></a>
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

<a id="bbc5de21fbb6e1e7"></a>
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

<a id="0595784b14bd781a"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="b2ba84eae01bce81"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](19-sql-references-c-g.md#04e7730c239ac562)
- [ALTER INDEX](#bb66b410758193b8)
- [DROP INDEX](19-sql-references-c-g.md#d20adfa902b88837)

<a id="b3aaf811285301ef"></a>
## ALTER INDEX name RENAME TO

<a id="976a909e10ec21d0"></a>
### 기능

인덱스의 이름을 변경한다.

<a id="e9b8b2829bd4439b"></a>
### 구문

```
<rename index statement> ::=
    ALTER INDEX index_name
        RENAME TO new_index_name
    ;
```

<a id="4190650bffc2183e"></a>
### 사용 범위 및 접근 권한

&lt;rename index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="87ba43eddc323cb9"></a>
### 구문 규칙 및 파라미터

<a id="bc3797baa95e5e51"></a>
#### index_name

대상 인덱스의 이름이다.  
스키마 이름을 기술할 수 없으며, 기존 인덱스와 동일한 스키마 이름을 갖는다.

<a id="b346aa0a3ade1ef6"></a>
#### new_index_name

새로운 인덱스의 이름이며 스키마 내에서 유일한 인덱스 이름이어야 한다.

<a id="579fc98c9774f72f"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="236af265167d066d"></a>
### 사용 예

다음은 인덱스의 이름을 변경하는 예이다.

```
gSQL> ALTER INDEX t1_idx1 RENAME TO idx_t1_id;

Index altered.
```

<a id="5a944815928067f8"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="0c7780367850aeb3"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](19-sql-references-c-g.md#04e7730c239ac562)
- [ALTER INDEX](#bb66b410758193b8)
- [DROP INDEX](19-sql-references-c-g.md#d20adfa902b88837)

<a id="67de286d3b392ca2"></a>
## ALTER INDEX name STORAGE

<a id="de67506d6d3222ba"></a>
### 기능

인덱스의 물리적 속성을 변경한다.

<a id="0ea5f892bb7eb0b9"></a>
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

<a id="42af577108c808e3"></a>
### 사용 범위 및 접근 권한

&lt;alter index physical attribute statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="9262e7a7246ee64d"></a>
### 구문 규칙 및 파라미터

<a id="2b837dd99114cd63"></a>
#### index_name

대상 인덱스의 이름이다.

<a id="e65d0d15bf896b64"></a>
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

<a id="bded0b65e108faee"></a>
#### &lt;segment attr clause&gt;

인덱스가 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer 
    - 정의 
        - 인덱스를 생성할 때 초기에 할당할 물리적 공간의 크기를 기술한다. 
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT 크기가 8192 bytes일 경우 'INITIAL 100'은 실제 8192 bytes로 동작한다.) 
        - 이 크기 (TABLESPACE의 EXTENT 크기에 align 된 크기)는 MINEXTENTS의 크기와 같거나 커야 하며, MAXEXTENTS의 크기와 같거나 작아야 한다. 
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
    - EXTENT 두 개 크기보다 작을 경우 EXTENT 두 개 크기로 결정된다.
    - 생략할 경우, 기본값은 32 테라바이트 (35,184,372,088,832) 이다.
    - 32 테라바이트보다 큰 값을 지정하더라도 32 테라바이트로 수정되어 설정된다.
    - 이미 할당되어 있는 공간보다 작은 크기를 지정하면 에러가 발생한다.

<a id="26acd92aea3e2346"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: kilobytes 
- M: megabytes 
- G: gigabytes 
- T: terabytes

<a id="e4654dc935623fb7"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="65eb40238e9b15e5"></a>
### 사용 예

다음은 인덱스의 물리적 속성을 변경하는 예이다.

```
gSQL> ALTER INDEX idx_t1_id PCTFREE 10 INITRANS 4 MAXTRANS 8;

Index altered.
```

<a id="944e21d965e0c455"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="e37692de83226992"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](19-sql-references-c-g.md#04e7730c239ac562)
- [ALTER INDEX](#bb66b410758193b8)
- [DROP INDEX](19-sql-references-c-g.md#d20adfa902b88837)

<a id="aff30be6193ddc88"></a>
## ALTER PROFILE

<a id="1356052f9669fd41"></a>
### 기능

비밀번호 관리 방법을 변경한다.

<a id="6e40b09e48a9ac9d"></a>
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

<a id="1fbefae36e0f91cc"></a>
### 사용 범위 및 접근 권한

&lt;alter profile statement&gt; 구문을 수행하려면 사용자에게 ALTER PROFILE ON DATABASE 권한이 있어야 한다.

<a id="a41ae19f30fc8a64"></a>
### 구문 규칙 및 파라미터

<a id="b036b361ac99a34d"></a>
#### profile_name

변경할 profile의 이름이다.

<a id="92adf4684d17e34b"></a>
#### FAILED_LOGIN_ATTEMPTS

로그인 연속 실패 허용 횟수를 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#7ed273ad779b6feb) 구문을 참조한다.

<a id="29095619190cf29c"></a>
#### PASSWORD_LOCK_TIME

로그인에 연속적으로 실패한 후에 계정이 잠기는 기간 (day)을 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#7ed273ad779b6feb) 구문을 참조한다.

<a id="c12835604f7073f1"></a>
#### PASSWORD_LIFE_TIME

비밀번호의 유효 기간 (day)을 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#7ed273ad779b6feb) 구문을 참조한다.

<a id="629569e629d68593"></a>
#### PASSWORD_GRACE_TIME

PASSWORD_LIFE_TIME 이후에 로그인 할 때 비밀번호 만료를 유예하는 기간을 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#7ed273ad779b6feb) 구문을 참조한다.

<a id="b48f53c589ef5c3d"></a>
#### PASSWORD_REUSE_MAX

이전 비밀번호를 재사용하려 할 때 재사용할 수 없는 최근 비밀번호 개수를 명시한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#7ed273ad779b6feb) 구문을 참조한다.

<a id="d450e45850f85da6"></a>
#### PASSWORD_REUSE_TIME

이전 비밀번호를 재사용하기 위해 필요한 경과 기간을 명시한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#7ed273ad779b6feb) 구문을 참조한다.

<a id="b2ebe874b7dc246f"></a>
#### PASSWORD_VERIFY_FUNCTION

비밀번호 복잡도 검증 방법을 설정한다.  
자세한 내용은 [CREATE PROFILE](19-sql-references-c-g.md#7ed273ad779b6feb) 구문을 참조한다.

<a id="6055767dc689cd7f"></a>
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

<a id="7f2391167063a216"></a>
### 호환성

SQL 표준은 profile에 대한 개념을 다루지 않고 있다.

<a id="075ba2741bac482a"></a>
### 참조

관련 내용은 [DROP PROFILE](19-sql-references-c-g.md#c779f85e72834738)을 참조한다.

<a id="ea63a831fa2ae849"></a>
## ALTER SEQUENCE

<a id="536ecc885aae07a6"></a>
### 기능

시퀀스를 변경한다.

<a id="b4b7d67d3385ab0e"></a>
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

<a id="9dbe6090dec6f4c6"></a>
### 사용 범위 및 접근 권한

&lt;alter sequence generator statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 시퀀스의 소유자 
- 시퀀스가 속한 스키마에 대해 (ALTER SEQUENCE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY SEQUENCE ON DATABASE

<a id="6a8a11412d0b5ad0"></a>
### 구문 규칙 및 파라미터

<a id="990861ef80fbbff8"></a>
#### sequence_name

변경할 시퀀스의 이름이다.  
schema_name.sequence_name과 같이 시퀀스가 속할 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="ed26d8759ea6c85b"></a>
#### &lt;alter sequence generator restart option&gt;

시퀀스의 다음 값 (NEXT VALUE)을 설정한다.  
단, [CREATE SEQUENCE](19-sql-references-c-g.md#971516b46cb8bf8d) 구문에서 정의한 START WITH의 값은 변경하지 않는다.

- RESTART 
    - 값을 명시하지 않을 경우, &lt;sequence generator definition&gt; 에서 정의한 START WITH의 값이 시퀀스의 다음 값으로 설정된다. 
- RESTART WITH integer 
    - integer 값을 시퀀스의 다음 값으로 설정한다. 
    - integer 값은 MINVALUE와 MAXVALUE 사이의 값이어야 한다.

&lt;alter sequence generator restart option&gt; 절을 명시하지 않은 경우, 시퀀스의 현재값을 기준으로 시퀀스의 속성을 변경한다.

<a id="688f7554219e706a"></a>
#### &lt;sequence generator increment by option&gt;

시퀀스 번호의 간격을 변경한다.  
다음과 같은 제약과 특징을 갖는다.

- 양수 또는 음수를 사용할 수 있으며, 0은 사용할 수 없다. 
- 간격의 절대값은 MINVALUE와 MAXVALUE의 차이보다 작아야 한다. 
- 양수일 경우 오름차순 시퀀스가 되고 음수일 경우 내림차순 시퀀스가 된다.

<a id="7051553f4701795c"></a>
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

<a id="c05ec3d8964fcf3c"></a>
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

<a id="a679bc7cb4b99dce"></a>
#### &lt;sequence generator cycle option&gt;

시퀀스의 값이 최대값 또는 최소값이 되었을 때, 계속 값을 생성할지 여부를 변경한다.

- CYCLE 
    - 오름차순 시퀀스가 최대값이 되었을 때, 최소값부터 다시 생성한다. 
    - 내림차순 시퀀스가 최소값이 되었을 때, 최대값부터 다시 생성한다. 
- NO CYCLE | NOCYCLE 
    - 최대값 또는 최소값이 되었을 때, 시퀀스 값을 생성할 수 없다. 
    - NO CYCLE (SQL 표준)과 NOCYCLE은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다.

<a id="e28ef4175ada8777"></a>
#### &lt;sequence generator cache option&gt;

시퀀스에 신속하게 접근하기 위해 메모리상에 미리 적재할 시퀀스 값의 개수를 정의한다.   
Database를 재구동할 때, 메모리상에 적재한 시퀀스 값은 유실되고 적재한 이후의 값부터 시작된다.

- CACHE integer 
    - CACHE 값은 2와 같거나 커야하고 
    - CYCLE이 존재할 경우 CACHE 값이 CYCLE의 길이보다 크지 않아야 한다. 
        - CYCLE의 길이: CEIL(MAXVALUE - MINVALUE) / ABS(INCREMENT) 
- NO CACHE | NOCACHE 
    - 메모리 상에 시퀀스값을 미리 적재하지 않는다.

<a id="a6549834e383b016"></a>
### 설명

[CREATE SEQUENCE](19-sql-references-c-g.md#971516b46cb8bf8d) 구문에서 정의한 시퀀스 속성 중 START WITH는 변경할 수 없다.  
START WITH 속성을 변경하려면 [DROP SEQUENCE](19-sql-references-c-g.md#bd4f615f4aee0c6b) 구문을 수행한 후에 [CREATE SEQUENCE](19-sql-references-c-g.md#971516b46cb8bf8d) 구문을 사용하여 다시 생성해야 한다.

<a id="ae38db169d4ee36f"></a>
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

<a id="90b383ec86eca1b4"></a>
### 호환성

SQL 표준에서는 CACHE/ NO CACHE 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="c0e870bb19654661"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T176 | Sequence generator support | O |
| T177 | Sequence generator support: simple restart option | O |

<a id="0e111a7b39a6c291"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE SEQUENCE](19-sql-references-c-g.md#971516b46cb8bf8d)
- [DROP SEQUENCE](19-sql-references-c-g.md#bd4f615f4aee0c6b)

<a id="928c83bbb08082fb"></a>
## ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

<a id="e368102ce1db6fd4"></a>
### 기능

세션에서 재사용하기 위해 catching 된 모든 공간들을 해당 tablespace로 반환한다.

<a id="a6e7b4d2e7a00cd9"></a>
### 구문

```
<alter session cleanup global temporary segment pool statement> ::=
    ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL
    ;
```

<a id="f7aedb78914be1e1"></a>
### 설명

수행된 세션에서 segment cache의 segment들만 cleanup한다.

<a id="1db8191387170be0"></a>
### 사용 예

다음은 세션 segment cache를 cleanup하는 예이다.

```
gSQL> ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

Session altered.
```

<a id="fbbf13e0a7a8ea6f"></a>
### 호환성

SQL 표준에서는 global temporary table, global temporary index의 segment cache 개념을 정의하지 않고 있다.

<a id="41eb871f7a55bf9d"></a>
### 참조

관련 내용은 [Global Temporary Table](13-sql-objects.md#0f1a1c1fdb7c12e1) 을 참조한다.

<a id="4923f8bcbf518f9e"></a>
## ALTER SESSION SET property_name

<a id="01edc05179d509ef"></a>
### 기능

세션의 프로퍼티 값을 설정한다.

<a id="0190fcfa9b2fe398"></a>
### 구문

```
<alter session set statement> ::=
    ALTER SESSION SET <property name> { = <property value> | TO DEFAULT }
    ;
```

<a id="462b82ad17e18626"></a>
### 구문 규칙 및 파라미터

<a id="16745357641eee56"></a>
#### &lt;property name&gt;

설정할 프로퍼티 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5c4ff2359a15b769) 장을 참조한다.

<a id="c8c7e03abdf7d569"></a>
#### &lt;property value&gt;

설정할 프로퍼티 값이다.

<a id="c164c2822ebac5ee"></a>
#### TO DEFAULT

세션 프로퍼티 값을 시스템 프로퍼티 값으로 설정한다.

<a id="c6d1b71b06f519a5"></a>
### 설명

각 property에 대한 자세한 설명은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5c4ff2359a15b769) 장을 참조한다.

<a id="a24fa0d1032a5fb4"></a>
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

<a id="042c7161b0b09bcc"></a>
### 호환성

SQL 표준에서는 세션 프로퍼티 개념을 정의하지 않고 있다.

<a id="9ea4c9609bbc45b2"></a>
### 참조

관련 내용은 [ALTER SESSION SET property_name](#4923f8bcbf518f9e) 을 참조한다.

<a id="a8b0bfb6c2dcbf1a"></a>
## ALTER SYSTEM CHECKPOINT

<a id="79a6c5d22e1e2c20"></a>
### 기능

CHECKPOINT를 수행한다.

<a id="2d0cc9b04b2284c3"></a>
### 구문

```
<alter system checkpoint statement> ::=
    ALTER SYSTEM CHECKPOINT
    [ AT <domain name> ]
    ;
```

<a id="7ae333f53705f8ca"></a>
### 사용 범위 및 접근 권한

&lt;alter system checkpoint statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="7a6d7189182543c2"></a>
### 구문 규칙 및 파라미터

<a id="94cf9add0a4b6ff8"></a>
#### &lt;alter system checkpoint statement&gt;

CHECKPOINT는 commit 된 트랜잭션들이 변경한 모든 데이터가 디스크에 기록되는 것을 보장하는 연산이다.

- 데이터베이스가 OPEN 상태여야 한다.
- 데이터베이스가 TDS 모드여야 한다.
- 전체 백업이 진행중일 때는 변경된 페이지가 데이터 파일에 기록되지 않고, REDO 로그와 제어파일만 디스크에 기록된다. 만약 이러한 상태에서 서버가 비정상 종료되는 경우에는 미디어 복구를 수행해야 한다.

<a id="acf132e27eb92ea1"></a>
#### &lt;domain name&gt;

- 구문을 수행할 멤버나 그룹의 이름이다.
- 지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="a0f20f56001fe062"></a>
### 설명

체크포인트 (checkpoint) 연산은 commit 된 트랜잭션들이 변경한 모든 내용을 디스크에 기록함으로써 시스템 장애시 신속한 복구를 가능하게 한다.

<a id="6a09488f6bc4441d"></a>
### 사용 예

다음은 CHECKPOINT를 수행하는 예이다.

```
ALTER SYSTEM CHECKPOINT;
```

<a id="828bf77163ae4cd6"></a>
### 호환성

SQL 표준에서는 CHECKPOINT 개념을 정의하지 않고 있다.

<a id="02d72ad1a0327858"></a>
## ALTER SYSTEM CLEANUP BUFFER_CACHE

<a id="1f971591cae51100"></a>
### 기능

Buffer cache에서 free 가능한 모든 buffer page들을 비운다.

<a id="8cb003b49c32b9df"></a>
### 구문

```
<alter system cleanup buffer_cache statement> ::=
    ALTER SYSTEM CLEANUP BUFFER_CACHE
    [ AT <domain name> ]
    ;
```

<a id="490c472bc17420c1"></a>
### 사용 범위 및 접근 권한

&lt;alter system cleanup buffer_cache statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="35f3992cb54b9561"></a>
### 구문 규칙 및 파라미터

<a id="a1a871a3b5ba1090"></a>
#### &lt;alter system cleanup buffer_cache statement&gt;

해당 구문 규칙이나 파라미터가 존재하지 않는다.

<a id="9a59042508dc112a"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="683d624ddb7f57f5"></a>
### 설명

Buffer에 캐시된 free 가능한 모든 buffer page들을 flush하고 free 한다.

> 성능 측정 전에 buffer cache를 비우는 목적으로 사용해야 한다.   
> 운영 중인 서버에서 사용할 경우 성능에 치명적인 영향을 미칠 수 있다.

<a id="751e1d3cb834a21e"></a>
### 사용 예

다음은 CLEANUP BUFFER_CACHE을 수행하는 예이다.

```
ALTER SYSTEM CLEANUP BUFFER_CACHE;
```

<a id="59d2d72cc20e0edf"></a>
### 호환성

SQL 표준에서는 CLEANUP BUFFER_CACHE의 개념을 정의하지 않고 있다.

<a id="bd3004870921a049"></a>
## ALTER SYSTEM CLEANUP PLAN

<a id="378ea7c74d94c856"></a>
### 기능

모든 SQL plan을 정리한다.

<a id="7092e7a9f1337323"></a>
### 구문

```
<alter system cleanup plan statement> ::=
    ALTER SYSTEM CLEANUP PLAN
    [ AT <domain name> ]
    ;
```

<a id="c442d51d431b2c46"></a>
### 사용 범위 및 접근 권한

&lt;alter system cleanup plan statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="69f0e2a30ca7fd46"></a>
### 구문 규칙 및 파라미터

<a id="bcb17ff1df0c01fc"></a>
#### &lt;alter system cleanup plan statement&gt;

해당 구문 규칙이나 파라미터가 존재하지 않는다.

<a id="68f7fb7c41ba2e24"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="761731234daf6e6c"></a>
### 설명

캐시되어 있는 모든 SQL plan을 정리한다.   
단, V$SQL_CACHE.REF_COUNT가 0보다 큰 plan (prepare된 statement에서 참조하는 plan)들은 정리 대상에서 제외한다.

<a id="a529fa2102aa854b"></a>
### 사용 예

다음은 CLEANUP PLAN을 수행하는 예이다.

```
ALTER SYSTEM CLEANUP PLAN;
```

<a id="5340485b39427e9c"></a>
### 호환성

SQL 표준에서는 CLEANUP PLAN의 개념을 정의하지 않고 있다.

<a id="cb6fb5727e351f45"></a>
## ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER

<a id="32741f35b5e53aa1"></a>
### 기능

복구 불가능한 클러스터 멤버를 지정한다.

<a id="20e3b7e0eec030ba"></a>
### 구문

```
<alter system irrecoverable cluster member statement> ::=
    ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER <domain name>
    ;
```

<a id="c7567fe79e73a423"></a>
### 사용 범위 및 접근 권한

&lt;alter system irrecoverable cluster member statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="f94fbf6ab9160c6a"></a>
### 구문 규칙 및 파라미터

<a id="6eda704f5268d365"></a>
#### &lt;alter system irrecoverable cluster member statement&gt;

해당 구문 규칙이나 파라미터가 존재하지 않는다.

<a id="8763ea4abd5b42c2"></a>
#### &lt;domain name&gt;

복구 불가능한 멤버 이름이다.  
그룹 내의 모든 멤버들을 복구 불가한 멤버로 지정할 수 없다.

<a id="0748a190fecd68e2"></a>
### 설명

복구 불가능한 멤버로 인해 클러스터 재시작에 실패하는 경우 해당 멤버를 제외하고 시스템을 재시작하기 위해 사용한다. 시스템 재시작에 성공한 후에는 반드시 [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#67f16d7dae2bf68a) 구문을 이용해 해당 멤버를 삭제해야 한다.

<a id="564edfc3d13ceef3"></a>
### 사용 예

다음은 IRRECOVERABLE CLUSTER MEMBER를 수행하는 예이다.

```
gSQL> ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER g1n1;
```

<a id="e30e523e8f4e9c31"></a>
### 호환성

SQL 표준에서는 IRRECOVERABLE CLUSTER MEMBER의 개념을 정의하지 않고 있다.

<a id="8b48c6e044e9469c"></a>
## ALTER SYSTEM JOIN DATABASE

<a id="cd2801789a8b37b8"></a>
### 기능

비활성화된 특정 cluster member를 cluster system에 다시 포함한다.

<a id="7141af5be7189529"></a>
### 구문

```
<alter system join database statement> ::=
    ALTER SYSTEM JOIN DATABASE 
    ;
```

<a id="499ffefaf87a4a07"></a>
### 사용 범위 및 접근 권한

Cluster system 에서 수행할 수 있다.

&lt;alter system join database statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="2e5169187a7d1dd4"></a>
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

<a id="9201fd3306217b94"></a>
### 사용 예

```
gSQL> ALTER SYSTEM JOIN DATABASE;
```

<a id="a6c3bf89ede48d3c"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="eb38acd567a622f9"></a>
### 참조

관련 내용은 [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#67f16d7dae2bf68a)를 참조한다.

<a id="9c45cb464b6ff803"></a>
## ALTER SYSTEM [KILL | DISCONNECT] SESSION

<a id="46f754cd9b0874ce"></a>
### 기능

세션을 종료한다.

<a id="01189308143dbdb9"></a>
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

<a id="5ab7539063785fb9"></a>
### 사용 범위 및 접근 권한

&lt;alter system end session statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="53175434e02b49c6"></a>
### 구문 규칙 및 파라미터

<a id="c5e23da17f7f2a42"></a>
#### &lt;member_position&gt;

Cluster 환경에서 disconnect/ kill 대상이 되는 세션의 member position 이다.

<a id="0367656ef9d6afb9"></a>
#### &lt;session_id&gt;

세션의 ID 이다.

<a id="36fa5b52dab4efaa"></a>
#### &lt;serial#&gt;

세션의 SERIAL NUMBER 이다.

<a id="46066f9d18eed00a"></a>
#### &lt;disconnect_option&gt;

- POST_TRANSACTION: 트랜잭션 완료 후, 세션을 종료한다.
- IMMEDIATE: 트랜잭션 완료를 기다리지 않고 바로 세션을 종료한다.

&lt;disconnect_option&gt;이 사용되지 않으면 IMMEDIATE로 동작한다.

<a id="2254780d3bee129a"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="c8e3736db7e5aefd"></a>
### 설명

DISCONNECT SESSION은 POST_TRANSACTION과 IMMEDIATE 옵션을 지정할 수 있으며, POST_TRANSACTION은 현재 실행되는 트랜잭션이 있을 경우 트랜잭션이 끝난 후에 세션을 종료한다. IMMEDIATE는 현재 수행 중인 트랜잭션을 바로 정리한 후에 세션을 종료한다.

KILL SESSION은 해당 세션의 프로세스는 존재하지 않지만, 시스템에 남아있는 비정상 세션을 종료한다.

<a id="4b0ebc5609c12fc2"></a>
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

<a id="d8dc7f2ecbc0f0b2"></a>
### 호환성

SQL 표준에서는 정의하지 않고 있다.

<a id="02b4e61c7b426491"></a>
## ALTER SYSTEM {MOUNT | OPEN} DATABASE

<a id="ab3b8e727e28a616"></a>
### 기능

데이터베이스를 시스템에 마운트하거나 서비스 가능한 상태로 변경한다.

<a id="b15270f9ad584e27"></a>
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

<a id="81a361192cac86ec"></a>
### 사용 범위 및 접근 권한

&lt;alter system database statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="b31489f8a596ef42"></a>
### 구문 규칙 및 파라미터

<a id="942d7567fdb9b610"></a>
#### &lt;alter system database clause&gt;

- MOUNT DATATABASE
    - 데이터베이스를 시스템에 마운트한다. 
- OPEN DATABASE
    - 데이터베이스를 서비스 가능한 상태로 변경한다.

<a id="8426e0be4ca62353"></a>
#### &lt;open database option&gt;

- RESETLOGS/ NORESETLOGS
    - 데이터베이스를 복구한 이후에 온라인 redo log를 유지할지 선택한다.
    - NORESETLOGS는 기존 redo log를 유지하는 반면에 RESETLOGS는 이를 초기화한다.
    - 데이터베이스를 불완전 복구한 경우, 반드시 RESETLOGS를 지정해야 한다.
    - 생략된 경우에는 NORESETLOGS가 기본으로 지정된다.

<a id="6cd067df70e02582"></a>
#### &lt;database_scope&gt;

- LOCAL
    - LOCAL 영역 서버를 OPEN 단계로 구동한다.
- GLOBAL
    - GLOBAL 영역, 즉 전체 서버를 OPEN 단계로 구동한다.
- Cluster 환경에서 생략된 경우 GLOBAL로 구동 된다.

<a id="414f83b047d25791"></a>
### 사용 예

다음은 온라인 redo log를 초기화하는 예이다.

```
ALTER SYSTEM OPEN DATABASE RESETLOGS;
```

<a id="b69907bd9c4eea58"></a>
### 호환성

SQL 표준에서는 데이터베이스의 MOUNT 또는 OPEN에 대한 개념을 정의하지 않고 있다.

<a id="c88fe2ef9fa80eac"></a>
### 참조

관련 내용은 [ALTER DATABASE RECOVER](#924443216c30d2a6)를 참조한다.

<a id="3563a066daddd6c0"></a>
## ALTER SYSTEM RECONNECT GLOBAL CONNECTION

<a id="7c2d78cd3271c362"></a>
### 기능

GLOBAL CONNECTION 형태로 접속한 세션에 재접속할지 여부를 설정한다.

<a id="4de7bd98656d36a2"></a>
### 구문

```
<alter system reconnect global connection statement> ::=
    ALTER SYSTEM RECONNECT GLOBAL CONNECTION
    ;
```

<a id="fc8fa27334ec8893"></a>
### 사용 범위 및 접근 권한

&lt;alter system reconnect global connection statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="67a9439eda0789ed"></a>
### 설명

GLOBAL CONNECTION 클라이언트의 재접속 여부는 최초 접속할 때 서버로부터 얻은 system 객체의 SCN과 현재 서버의 system 객체의 SCN을 비교하여 결정한다. 해당 구문은 system 객체의 SCN을 상승시켜 클라이언트의 재접속을 유도한다.

해당 구문을 수행한 즉시 클라이언트가 재접속하는 것은 아니다. 클라이언트가 서버에 명령어를 실행할 때 SCN 비교를 통해서 재접속하며 만약 클라이언트에서 모든 멤버로의 연결이 유효하다면 재접속을 시도하지 않는다.

<a id="c505eebc3c5d5e01"></a>
### 사용 예

다음은 해당 구문을 수행하는 예이다.

```
gSQL> ALTER SYSTEM RECONNECT GLOBAL CONNECTION;

System altered.
```

<a id="035a83110885b38d"></a>
### 호환성

SQL 표준에서는 GLOBAL CONNECTION의 개념을 정의하지 않고 있다.

<a id="08c8f4e9776944d0"></a>
## ALTER SYSTEM RESET property_name

<a id="c366b604bfe0da3d"></a>
### 기능

프로퍼티 파일에서 프로퍼티 값을 삭제한다.

<a id="97179bc35c9173e1"></a>
### 구문

```
<alter system reset statement> ::=
    ALTER SYSTEM { RESET | UNSET } <property name>
        [ SCOPE = { FILE | SPFILE } ]
        [ AT <domain name>]
    ;
```

<a id="f45f0a5bf20f0e18"></a>
### 사용 범위 및 접근 권한

&lt;alter system reset statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="8c7b6a0ff2dec2b8"></a>
### 구문 규칙 및 파라미터

<a id="48b2dea042d8278b"></a>
#### { RESET | UNSET }

RESET과 UNSET은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다.

<a id="c725d88034698ede"></a>
#### &lt;property name&gt;

삭제할 프로퍼티의 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5c4ff2359a15b769) 장을 참조한다.

<a id="ac274f3dc56a2242"></a>
#### [ SCOPE = { FILE | SPFILE } ]

프로퍼티 파일에서 삭제하는 것이므로 SCOPE=FILE/SPFILE만 사용할 수 있다.

- SCOPE = FILE 
    - FILE과 SPFILE은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다. 
    - 프로퍼티를 FILE에서 삭제하고, 현재 상태에는 적용하지 않는다. 
    - Database를 재구동할 때 변경 사항을 적용한다.

SCOPE 절을 명시하지 않을 경우, 기본값은 SCOPE = FILE 이다.

<a id="bc31ef079c2fc8fa"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="be2a44f902364a2f"></a>
### 설명

SCOPE=FILE/SPFILE을 사용하여 프로퍼티를 변경했을 경우, 갱신된 값이 프로퍼티 파일에 저장되고 데이터베이스를 재시작할 때 반영된다.

RESET 할 경우, 프로퍼티 파일에 저장된 해당 프로퍼티 갱신값을 파일에서 제거하고 데이터베이스를 재시작할 때 default 값을 사용하도록 한다.

<a id="1dcd4c34e769dc4a"></a>
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

<a id="6f21492892544789"></a>
### 호환성

SQL 표준에서는 시스템 프로퍼티 개념을 정의하지 않고 있다.

<a id="a733de28c1d5deba"></a>
### 참조

관련 내용은 [ALTER SYSTEM SET property_name](#677a2c760cc67fbc)을 참조한다.

<a id="677a2c760cc67fbc"></a>
## ALTER SYSTEM SET property_name

<a id="97a4df27d60c0282"></a>
### 기능

시스템의 프로퍼티 값을 설정한다.

<a id="d940384a2fea6072"></a>
### 구문

```
<alter system set statement> ::=
    ALTER SYSTEM SET <property name> { = <property value> | TO DEFAULT }
        [ DEFERRED ]
        [ SCOPE = [ MEMORY | { FILE | SPFILE } | BOTH ] ]
    [AT <domain name>]
    ;
```

<a id="33a703b15a4e388a"></a>
### 사용 범위 및 접근 권한

&lt;alter system set statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="515e483eb12aff51"></a>
### 구문 규칙 및 파라미터

<a id="28fa0cb2218e1ee3"></a>
#### &lt;property name&gt;

설정할 프로퍼티의 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5c4ff2359a15b769) 장을 참조한다.

<a id="de1d6881bde8abe5"></a>
#### &lt;property value&gt;

설정할 프로퍼티의 값이다.

<a id="23ae64c024efd1c4"></a>
#### TO DEFAULT

시스템 프로퍼티 값을 시스템을 구동할 당시의 최초값으로 설정한다.

<a id="f3d3473444c66b93"></a>
#### [ DEFERRED ]

변경된 프로퍼티를 적용할 시점을 정의한다.

- DEFERRED 
    - 현재 SESSION에는 영향을 주지 않고, 새로 생성되는 SESSION에 적용된다. 
    - 프로퍼티의 SYS_MODIFIABLE 속성값이 IMMEDIATE/ DEFERRED 일 때 적용 가능하며, 반드시 명시해야 한다. 
    - 프로퍼티의 SYS_MODIFIABLE 속성값이 FALSE인 경우 사용할 수 없다.

프로퍼티의 SYS_MODIFIABLE 속성값이 IMMEDIATE일 경우, DEFERRED를 명시하지 않으면 모든 SESSION에 바로 적용된다.

<a id="14246209a3619234"></a>
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

<a id="4fffc086e2d822f6"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="36af3f968f3506e9"></a>
### 설명

자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5c4ff2359a15b769) 장을 참조한다.

<a id="424375859470bf2b"></a>
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

<a id="675671336fb7c400"></a>
### 호환성

SQL 표준에서는 시스템의 프로퍼티 개념을 정의하지 않고 있다.

<a id="313546b9a5d0796b"></a>
### 참조

관련 내용은 [ALTER SYSTEM RESET property_name](#08c8f4e9776944d0)을 참조한다.

<a id="52da9ec67518ca8f"></a>
## ALTER SYSTEM SWITCH LOGFILE

<a id="e08ecd085025da13"></a>
### 기능

데이터베이스 내에 있는 CURRENT 상태의 로그파일을 ACTIVE 상태로 변경한다.

<a id="c83017262f1dca9f"></a>
### 구문

```
<alter system switch logfile statement> ::=
    ALTER SYSTEM SWITCH LOGFILE
    [ AT <domain name> ]
    ;
```

<a id="316487a460d2513e"></a>
### 사용 범위 및 접근 권한

&lt;alter system switch logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="50543f7e28f63c0e"></a>
### 구문 규칙 및 파라미터

<a id="75d0b9be4493fdec"></a>
#### &lt;alter system switch logfile statement&gt;

데이터베이스가 MOUNT 또는 OPEN 상태여야 한다.

<a id="7bfb601ae2ca7da3"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="69a166e49c622cf5"></a>
### 설명

기본적으로 CURRENT 상태의 로그파일이 다 채워지면 자동으로 로그 스위치가 발생한다. 해당 구문은 특수한 상황에서 강제로 로그 스위치를 하고자 할 때 사용된다.

<a id="07ff399ff25f5ef1"></a>
### 사용 예

```
ALTER SYSTEM SWITCH LOGFILE;
```

<a id="44acd1ad14b5cd7c"></a>
### 호환성

SQL 표준에서는 LOGFILE에 대한 개념을 정의하지 않고 있다.

<a id="ead7ac63050d3732"></a>
### 참조

관련 내용은 [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#02b4e61c7b426491)를 참조한다.

<a id="dbeb5fde894ac5df"></a>
## ALTER TABLE

<a id="a6ced4a33819dcc5"></a>
### 기능

테이블 정의를 변경한다.

<a id="22bd08eda140af9e"></a>
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
    | <move shard statement>
    | <merge shards statement>
    | <split shard statement>
    | <alter table synchronize statement>
    | <rename shard statement>
    | <read { only | write } statement>
    ;
```

<a id="305cedbf924a095c"></a>
### 사용 범위 및 접근 권한

&lt;alter table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="75d35d5ded1c511d"></a>
### 구문 규칙 및 파라미터

<a id="988c1e73a146d00b"></a>
#### &lt;alter table physical attribute statement&gt;

테이블의 물리적 속성을 변경한다.  
자세한 내용은 [ALTER TABLE name STORAGE](#6f64550f92fa2c88) 구문을 참조한다.

<a id="63cc1ba065843ec5"></a>
#### &lt;rename table statement&gt;

테이블 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME TO](#079b6bb5fd726b84) 구문을 참조한다.

<a id="35bc9c2235947f67"></a>
#### &lt;add column definition&gt;

테이블에 column을 추가한다.  
자세한 내용은 [ALTER TABLE name ADD COLUMN](#eccd1f42db335101) 구문을 참조한다.

<a id="d577cec4d07503f7"></a>
#### &lt;drop column definition&gt;

테이블에서 column을 삭제한다.  
자세한 내용은 [ALTER TABLE name SET UNUSED COLUMN](#c309a04b3589e0b4) 구문을 참조한다.

<a id="0d18e4fffe845042"></a>
#### &lt;alter column definition&gt;

테이블 column의 정의를 변경한다.  
자세한 내용은 [ALTER TABLE name ALTER COLUMN](#20641159e3d2762f) 구문을 참조한다.

<a id="ee3df3cf5a998624"></a>
#### &lt;rename column statement&gt;

테이블 column의 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME COLUMN](#76eb6b8299dccb24) 구문을 참조한다.

<a id="dec0e643510f50a6"></a>
#### &lt;add table constraint definition&gt;

테이블에 제약 조건을 추가한다.  
자세한 내용은 [ALTER TABLE name ADD CONSTRAINT](#687f8d2d4bc52b07) 구문을 참조한다.

<a id="03322e1d158bb820"></a>
#### &lt;drop table constraint definition&gt;

테이블의 제약 조건을 삭제한다.  
자세한 내용은 [ALTER TABLE name DROP CONSTRAINT](#f92321716f08611e) 구문을 참조한다.

<a id="0d4ed34a57e6efd6"></a>
#### &lt;alter table constraint definition&gt;

테이블의 제약 조건을 변경한다.  
자세한 내용은 [ALTER TABLE name ALTER CONSTRAINT](#945ef430d7091816) 구문을 참조한다.

<a id="513b88730a8c6db1"></a>
#### &lt;alter table drop offline segments statement&gt;

테이블의 오프라인 된 shard들을 삭제한다.  
자세한 내용은 [ALTER TABLE name DROP OFFLINE SEGMENTS](#12188ac1593e923a) 구문을 참조한다.

<a id="be16e3a63d14a3f0"></a>
#### &lt;rename table constraint statement&gt;

테이블 제약 조건의 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME CONSTRAINT](#f2bbf6bbdf160660) 구문을 참조한다.

<a id="995994a97a023da0"></a>
#### &lt;add table supplemental log statement&gt;

테이블의 데이터가 변경되면 redo log에 부가 정보를 추가하도록 설정한다.  
자세한 내용은 [ALTER TABLE name ADD SUPPLEMENTAL LOG](#ff060f4d10146868) 구문을 참조한다.

<a id="22506e34d7bdb2f6"></a>
#### &lt;drop table supplemental log statement&gt;

테이블의 데이터가 변경되면 redo log에 부가 정보를 추가하지 않도록 설정한다.  
자세한 내용은 [ALTER TABLE name DROP SUPPLEMENTAL LOG](#b598685146fb8525) 구문을 참조한다.

<a id="1c78219f32f69bd1"></a>
#### &lt;rebalance statement&gt;

Cluster 환경에서 테이블의 shard를 재배치하거나 정합성이 깨진 shard를 동기화하여 정합성을 복구한다.  
자세한 내용은 [ALTER TABLE REBALANCE](#149294331f00fde7) 구문을 참조한다.

<a id="8fae64818c02a3ca"></a>
#### &lt;alter table synchronize statement&gt;

Cluster 환경에 이미 배치되어 있는 오프라인 된 shard들을 동기화하여 정합성을 복구한다.  
자세한 내용은 [ALTER TABLE name SYNCHRONIZE](#c03af2d66eb7e9c7) 구문을 참조한다.

<a id="e9a053350780e0f3"></a>
#### &lt;move shard statement&gt;

Cluster 환경에서 테이블의 특정 shard를 특정 cluster group으로 재배치한다.  
자세한 내용은 [ALTER TABLE MOVE SHARD](#a93d376fd2ef5b9b) 구문을 참조한다.

<a id="c0c1504df5629e10"></a>
#### &lt;merge shards statement&gt;

Cluster 환경에서 테이블의 특정 shard들을 병합하여 재배치한다.  
자세한 내용은 [ALTER TABLE name MERGE SHARDS](#17b11ce95124d828) 구문을 참조한다.

<a id="755950c3bffbd8d5"></a>
#### &lt;split shard statement&gt;

Cluster 환경에서 테이블의 특정 shard를 분산하여 특정 cluster group에 재배치한다.  
자세한 내용은 [ALTER TABLE SPLIT SHARD](#6e8d2bde00700ace) 구문을 참조한다.

<a id="ceb3edc96056fc33"></a>
#### &lt;rename shard statement&gt;

Cluster 환경에서 테이블의 특정 shard 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME SHARD](#7ae6adc965bf6c07) 구문을 참조한다.

<a id="c6da9130929c4457"></a>
#### &lt;read { only | write } statement&gt;

테이블에 READ ( only | write }을 설정한다.  
자세한 내용은 [ALTER TABLE name READ { ONLY | WRITE }](#b2ad57535b47fe58) 구문을 참조한다.

<a id="ca4192e307606913"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="f3bb217a963d3026"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="e44711a00d487fcb"></a>
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

<a id="eccd1f42db335101"></a>
## ALTER TABLE name ADD COLUMN

<a id="b28cd3d1666c77a2"></a>
### 기능

테이블에 column을 추가한다.

<a id="e0a6a6c5c2934c1c"></a>
### 구문

```
<add column definition> ::=
      ALTER TABLE table_name ADD [ COLUMN ] <column definition>
    | ALTER TABLE table_name ADD [ COLUMN ] ( <column definition> [, ...] )
    ;
```

<a id="77aa19224fb4622c"></a>
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

<a id="e0c103251430a152"></a>
### 구문 규칙 및 파라미터

<a id="c0eedc51f483a7c1"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="b91adffc0a3a4d40"></a>
#### ADD [ COLUMN ]

COLUMN 예약어는 생략할 수 있다.

<a id="e5ae888f121d1561"></a>
#### &lt;column definition&gt;

추가할 column을 정의한다.  
자세한 내용은 [CREATE TABLE](19-sql-references-c-g.md#060501387611d25a) 구문의 [&lt;column definition&gt;](19-sql-references-c-g.md#7d745366530cb2b2) 절을 참조한다.  
테이블 내에 동일한 column 이름이 존재하지 않아야 한다.

Column을 정의할 때 DEFAULT 절을 명시할 경우, 모든 row의 기본값을 추가되는 column에 저장한다.  
Column을 정의할 때 &lt;identity column specification&gt; 절을 명시한 경우, 모든 row 각각의 자동 생성값을 추가되는 column에 저장한다.   
Column을 정의할 때 NOT NULL 제약 조건을 함께 명시한 경우, 테이블을 비우거나 DEFALUT 절 또는 &lt;identity column specification&gt; 절을 함께 기술해야 한다.

<a id="3990441ca87a4cd3"></a>
#### ( &lt;column definition&gt; [, ...] )

다수의 column을 추가한다.   
괄호 내부에 다수의 &lt;column definition&gt;을 나열한다.

<a id="2f0fd8586b99f5fb"></a>
### 설명

추가되는 column은 기존 column들의 뒤에 위치한다.   
DEFAULT 절이나 &lt;identity column specification&gt;을 명시한 경우, 수행시간은 테이블에 존재하는 row의 개수에 비례하여 증가한다.

<a id="f780e0cf1648ff37"></a>
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

<a id="6ddd60af326948e1"></a>
### 호환성

SQL 표준에서는 다수의 column definition 추가에 대해 정의하지 않고 있다.

<a id="8855bd47bc081b1f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#dbeb5fde894ac5df)
- [ALTER TABLE name SET UNUSED COLUMN](#c309a04b3589e0b4)
- [ALTER TABLE name ALTER COLUMN](#20641159e3d2762f)
- [ALTER TABLE name RENAME COLUMN](#76eb6b8299dccb24)

<a id="687f8d2d4bc52b07"></a>
## ALTER TABLE name ADD CONSTRAINT

<a id="ab7fb0012c5295ab"></a>
### 기능

테이블 제약 조건을 추가한다.

<a id="54c2bfbbef121ed7"></a>
### 구문

```
<add table constraint definition> ::=
    ALTER TABLE table_name 
        ADD <table constraint definition>
    ;
```

<a id="05acb28a59df6956"></a>
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

<a id="a4b1b92d5dbd6873"></a>
### 구문 규칙 및 파라미터

<a id="4fd61d77407da9ce"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="31c898172c846343"></a>
#### &lt;table constraint definition&gt;

추가할 제약 조건을 정의한다.  
NOT NULL 제약 조건은 ALTER TABLE .. ADD CONSTRAINT 구문으로 추가할 수 없으며, 다음 예와 같이 [ALTER TABLE name ALTER COLUMN](#20641159e3d2762f) 구문을 이용해 정의할 수 있다.

```
ALTER TABLE t1 ALTER COLUMN c1 SET NOT NULL;
```

자세한 내용은 [CREATE TABLE](19-sql-references-c-g.md#060501387611d25a) 구문의 [&lt;table constraint definition&gt;](19-sql-references-c-g.md#5d9d3af3b21cbfb2) 절을 참조한다.

<a id="da88fbcad924bb0e"></a>
### 설명

Primary key, unique key와 같은 key 제약을 추가할 때 이를 위한 index가 자동으로 생성된다.

<a id="788adc0483e77b83"></a>
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

<a id="676f2c8f18af24c9"></a>
### 호환성

**SQL 표준 호환성**

<a id="d42e8485c630f173"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="0c1842be57ba7fc0"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](19-sql-references-c-g.md#060501387611d25a)
- [CREATE INDEX](19-sql-references-c-g.md#04e7730c239ac562)
- [ALTER TABLE](#dbeb5fde894ac5df)
- [ALTER TABLE name DROP CONSTRAINT](#f92321716f08611e)

<a id="7d73e98f397bd282"></a>
## ALTER TABLE name ADD GLOBAL SECONDARY INDEX

<a id="543e3869a2b4821d"></a>
### 기능

테이블에 global secondary index를 생성한다.

<a id="7a1ea7402a00ac3d"></a>
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

<a id="c6a2ce0149138660"></a>
### 사용 범위 및 접근 권한

&lt;alter table add global secondary index definition&gt; 구문은 cluster system에서 정의할 수 있으며 사용자는 다음 조건들을 만족해야 한다.

- 인덱스를 생성할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 인덱스가 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE
    - USAGE TABLESPACE ON DATABASE

<a id="cc5d1753e349af38"></a>
### 구문 규칙 및 파라미터

<a id="0069d0a519355305"></a>
#### table_name

인덱스를 생성할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="27ff2d88fa26ee61"></a>
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

<a id="f562efb711300a1d"></a>
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

<a id="6d561fa6a3094638"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="da9396d8d24de088"></a>
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

<a id="ba272d6ec0cc7174"></a>
#### TABLESPACE tablespace_name

인덱스가 저장될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - LOGGING 인덱스로 변경하려면, tablespace_name은 data tablespace여야 하며 
    - NOLOGGING 인덱스로 변경하려면 tablespace_name은 temporary tablespace 또는 nologging tablespace여야 한다.

- TABLESPACE 절을 생략할 경우, 기존 인덱스의 설정을 그대로 따른다.

<a id="e290031ac36e3179"></a>
### 설명

Non-deterministic 질의에는 global secondary index가 반드시 필요하다. LOGGING 인덱스와 NOLOGGING 인덱스에는 다음과 같은 trade-off가 있다

- LOGGING 인덱스
    - 장점: 시스템을 구동할 때 로그를 이용해 인덱스가 자동으로 복구되므로 별도의 구축과정이 없다.
    - 단점: 관련 row를 변경할 때 인덱스 변경 내용을 로그로 기록하여 디스크 IO를 유발한다.
- NOLOGGING 인덱스
    - 장점: 관련 row를 변경할 때 인덱스 변경 내용에 대해 디스크 IO가 발생하지 않는다.
    - 단점: 시스템을 구동할 때 인덱스에 대한 로그 정보가 없어 자동으로 인덱스를 재구축한다.

<a id="b2f813853d81c2d2"></a>
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

<a id="d8e0630c0ae8c94b"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="e5f63afac08cd1cb"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#0779553a5fc95a3a)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#1d1ba8cbac456eee)
- [CREATE TABLE](19-sql-references-c-g.md#060501387611d25a)

<a id="ff060f4d10146868"></a>
## ALTER TABLE name ADD SUPPLEMENTAL LOG

<a id="15df30fb71acb6e0"></a>
### 기능

테이블의 데이터가 변경될 때 테이블에 primary key가 있으면 redo log에 primary key 값을 추가하도록 설정한다.

<a id="99abe6ac1d762339"></a>
### 구문

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="bec641bb334c3db6"></a>
### 사용 범위 및 접근 권한

&lt;add table supplemental log statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="07aa27c1ab849a7e"></a>
### 구문 규칙 및 파라미터

<a id="ca089cb3bbe8735b"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

테이블에 primary key가 존재하지 않더라도 구문을 수행할 수 있다.

<a id="4437cc23e4ef5d8c"></a>
### 설명

해당 TABLE에 UPDATE/ DELETE를 수행할 때 SUPPLEMENTAL LOG를 추가로 기록하도록 한다. 기록된 SUPPLEMENTAL LOG는 CDC와 같은 툴 또는 로그를 분석할 때 사용된다.

모든 TABLE의 SUPPLEMENTAL LOG를 기록하려면 *SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY = YES*로 설정한다.

<a id="66ffe784301fc71d"></a>
### 사용 예

다음은 테이블의 data를 변경할 때 redo log에 primary key 값을 추가하도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="a7c435cbb73f1049"></a>
### 호환성

SQL 표준에서는 &lt;add table supplemental log statement&gt;를 다루지 않는다.

<a id="bc8cde62e72aac4f"></a>
### 참조

관련 내용은 [ALTER TABLE name DROP SUPPLEMENTAL LOG](#b598685146fb8525)를 참조한다.

<a id="20641159e3d2762f"></a>
## ALTER TABLE name ALTER COLUMN

<a id="264973e6de078167"></a>
### 기능

Column의 정의를 변경한다.

<a id="435bda61e02cd016"></a>
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

<a id="f2164372991cbf48"></a>
### 사용 범위 및 접근 권한

&lt;alter column definition&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="f12d1c09aecccde2"></a>
### 구문 규칙 및 파라미터

<a id="d6be08e53328d6cd"></a>
#### table_name

변경할 테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="46cf6faf056937c5"></a>
#### ALTER [ COLUMN ]

COLUMN 예약어는 생략할 수 있다.

<a id="868ef4ffdb8e72e4"></a>
#### column_name

변경할 column의 이름이다.

<a id="5744d017f8645f15"></a>
#### &lt;set column default clause&gt;

Column의 기본값을 설정한다.   
identity column이 아니어야 한다.

이후에 수행되는 INSERT 구문 등에서 DEFAULT 절을 사용할 경우 설정한 기본값이 사용된다.

DEFAULT expression의 데이터 타입은 column의 데이터 타입과 호환 가능해야 한다.   
타입이 호환되지 않거나 expression이 valid 하지 않으면 에러가 발생한다.

자세한 설명은 [CREATE TABLE](19-sql-references-c-g.md#060501387611d25a) 구문의 [&lt;default clause&gt;](19-sql-references-c-g.md#3b1e389e68d3d8cd) 절을 참조한다.

<a id="17709734ee830bf4"></a>
#### &lt;drop column default clause&gt;

Column의 기본값을 제거한다.  
identity column이 아니어야 한다.  
기본값을 제거하면 INSERT 구문 등에서 DEFAULT 절을 사용할 때 NULL 값으로 설정된다.

<a id="c8a7c6ae5045549c"></a>
#### &lt;set column not null clause&gt;

- SET [CONSTRAINT constraint_name] NOT NULL [ &lt;constraint characteristics&gt; ]
    - Column에 NOT NULL 제약 조건을 설정한다.
    - Column의 값으로 NULL 값을 허용하지 않는다.
    - 해당 column에 NULL 값이 존재하지 않아야 한다.

- [CONSTRAINT constraint_name]을 생략할 경우 자동으로 제약 조건 이름을 지정한다.
- &lt;constraint characteristics&gt;를 생략할 경우, NOT DEFERRABLE INITIALLY IMMEDIATE 속성을 갖는다.
- Identity column은 DEFERRABLE 속성을 가질 수 없다.

지연가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](20-sql-references-h-z.md#b39019fd3808ec13) 구문의 설명을 참조한다.

<a id="c4347f0833b102b1"></a>
#### &lt;drop column not null clause&gt;

- DROP NOT NULL
    - Column의 NOT NULL 제약 조건을 제거한다.

<a id="4756ff6c67f21ebc"></a>
#### &lt;alter column data type clause&gt;

- SET DATA TYPE &lt;data type&gt;
    - Column의 데이터 타입을 변경한다.

> SET DATA TYPE 구문은 자동으로 commit 되는 DDL 구문이다.

동일한 계열간에 타입을 변경할 수 있는데 이 때 다음 조건을 만족해야 한다.

**character string type 변환**

<a id="42c42d57c6b1b169"></a>
| from \ to | CHAR(n) | VARHCAR(n) | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR(m) | X | X | X |
| VARCHAR(m) | X | n >= m | X |
| LONG VARCHAR | X | X | O |

char length unit을 변경할 경우 다음과 같은 조건을 만족해야 한다.

**character length unit 변환**

<a id="a35eb9292ccc990e"></a>
| from \ to | OCTETS | CHARACTERS |
| --- | --- | --- |
| OCTETS | O | O |
| CHARACTERS | X | O |

**binary string type 변환**

<a id="bb0d65be1dba31c7"></a>
| from \ to | BINARY(n) | VARBINARY(n) | LONG VARBINARY |
| --- | --- | --- | --- |
| BINARY(m) | X | X | X |
| VARBINARY(m) | X | n >= m | X |
| LONG VARBINARY | X | X | O |

**numeric type**

<a id="2fd6cff856f5f006"></a>
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

<a id="cc2002ceef27c394"></a>
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

<a id="3a4fbf8b5981aa18"></a>
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

<a id="0c9df5ba1c2a3437"></a>
| from \ to | NATIVE_SMALLINT | NATIVE_INTEGER | NATIVE_BIGINT | NATIVE_REAL | NATIVE_DOUBLE |
| --- | --- | --- | --- | --- | --- |
| NATIVE_SMALLINT | O | X | X | X | X |
| NATIVE_INTEGER | X | O | X | X | X |
| NATIVE_BIGINT | X | X | O | X | X |
| NATIVE_REAL | X | X | X | O | X |
| NATIVE_DOUBLE | X | X | X | X | O |

**Boolean type의 변환**

<a id="be3d5d03f86c13ec"></a>
| from \ to | BOOLEAN |
| --- | --- |
| BOOLEAN | O |

**Date/ time type의 변환 (TZ: WITH TIME ZONE)**

<a id="5d73794c6246ae71"></a>
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

<a id="349b6e3b426a7155"></a>
| from \ to | YEAR(q) | MONTH(q) | YEAR(q) TO MONTH |
| --- | --- | --- | --- |
| YEAR(p) | q >= p | X | X |
| MONTH(p) | X | q >= p | X |
| YEAR(p) TO MONTH | X | X | q >= p |

**INTERVAL DAY TO TIME 계열의 type 변환 (p,q 가 생략된 경우 2) (f,g 가 생략된 경우 6)**

<a id="fe440a1572e6a0cd"></a>
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

<a id="233b7d9e35a1862e"></a>
| from \ to | ROWID |
| --- | --- |
| ROWID | O |

<a id="01aa156902a57ace"></a>
#### &lt;alter identity column specification&gt;

Column의 identity 속성을 변경한다.   
Column은 identity column 이어야 한다.

- SET GENERATED [ ALWAYS | BY DEFAULT ]
    - identity column의 생성 방식을 변경한다. 
    - 자세한 내용은 [CREATE TABLE](19-sql-references-c-g.md#060501387611d25a) 구문의 [&lt;identity column specification&gt;](19-sql-references-c-g.md#4bc86294cae245fa)을 참조한다. 
- &lt;alter sequence generator restart option&gt; 
    - identity column의 다음 값 (NEXT VALUE)을 변경한다. 
    - 자세한 내용은 [ALTER SEQUENCE](#ea63a831fa2ae849) 구문의 &lt;[alter sequence generator restart option&gt;](#ed26d8759ea6c85b) 절을 참조한다. 
- &lt;basic sequence generator option&gt; 
    - identity column의 속성을 변경한다. 
    - SQL 표준에서는 SET &lt;basic sequence generator option&gt;의 형태로 기술하도록 정의하고 있으나 생략 가능하다. 
    - 자세한 내용은 [ALTER SEQUENCE](#ea63a831fa2ae849) 구문을 참조한다.

<a id="8008405bf0f4237f"></a>
#### &lt;drop identity property clause&gt;

Column의 identity 속성을 제거한다.   
Column은 identity column 이어야 한다.

<a id="32f037b742c3f9b1"></a>
### 설명

SET NOT NULL 절의 null 검사 수행시간은 테이블의 row 개수에 비례한다.

다음과 같은 column은 NULL 값을 허용하지 않는다. 즉, DROP NOT NULL 절을 수행하더라도 다음 조건 중 하나를 만족할 경우 NULL 값을 허용하지 않는다.

- NOT NULL 제약 조건이 있는 column
- Column이 primary key 제약 조건에 포함되는 경우
- Column이 identity column인 경우

SET DEFAULT 절을 이용한 기본값 변경과 &lt;alter identity column specification&gt; 절을 이용한 identity 속성의 변경은 이후에 수행되는 INSERT 또는 UPDATE 구문에 적용된다.

<a id="d82647fec0f682bd"></a>
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

<a id="b001c6131b55282b"></a>
### 호환성

**SQL 표준 호환성**

<a id="16f1f8a7fc5521d1"></a>
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

<a id="758f399e793917e1"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#dbeb5fde894ac5df)
- [ALTER TABLE name ADD COLUMN](#eccd1f42db335101)
- [ALTER TABLE name SET UNUSED COLUMN](#c309a04b3589e0b4)
- [ALTER TABLE name RENAME COLUMN](#76eb6b8299dccb24)

<a id="945ef430d7091816"></a>
## ALTER TABLE name ALTER CONSTRAINT

<a id="fa77e303690968c0"></a>
### 기능

테이블 제약 조건의 특성을 변경한다.

<a id="6188516f79b6a3cf"></a>
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

<a id="33698176a9e05d36"></a>
### 사용 범위 및 접근 권한

&lt;alter table constraint definition&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

> Cluster는 지연 가능한 제약 조건을 지원하지 않는다.

<a id="03c027c21b60758b"></a>
### 구문 규칙 및 파라미터

<a id="900c23f347f055f9"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="798303959cc69774"></a>
#### &lt;constraint object&gt;

변경할 제약 조건은 다음과 같이 지정할 수 있다.

- CONSTRAINT constraint_name
    - 변경할 제약 조건의 이름이다.
- PRIMARY KEY 
    - 테이블의 PRIMARY KEY 제약 조건이다.
- UNIQUE( column [,...] ) 
    - Column 목록에 부합되는 UNIQUE 제약 조건이다.

<a id="d8826b518f31b492"></a>
#### DEFERRABLE | NOT DEFERRABLE

제약 조건의 지연 가능 여부를 변경한다.

- DEFERRABLE
    - 제약 조건을 지연가능하도록 변경한다. 
- NOT DEFERRABLE 
    - 제약 조건을 지연가능하지 않도록 변경한다.

지연가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](20-sql-references-h-z.md#b39019fd3808ec13) 구문의 설명을 참조한다.

<a id="3203416f68983b7f"></a>
#### INITIALLY IMMEDIATE | INITIALLY DEFERRED

제약 조건의 검사시점 초기값을 변경한다.

- INITIALLY IMMEDIATE 
    - DML을 수행할 때 제약 조건을 검사한다.
- INITIALLY DEFERRED 
    - COMMIT을 수행할 때 제약 조건을 검사한다.

NOT DEFERRABLE로 정의된 제약 조건은 INITIALLY DEFERRED로 변경할 수 없다.

<a id="6f7000f6b144c6bf"></a>
### 설명

지연가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](20-sql-references-h-z.md#b39019fd3808ec13) 구문을 참조한다.

<a id="0c1ded2b14955367"></a>
### 사용 예

다음은 t1_uk 제약 조건을 지연가능하게 하고 검사시점을 DEFERRED로 설정하는 예이다.

```
gSQL> ALTER TABLE t1 ALTER CONSTRAINT t1_uk DEFERRABLE INITIALLY DEFERRED;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="2f64f1b3b277e3a1"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- ALTER PRIMARY KEY 절
- ALTER UNIQUE(column [,...]) 절

**SQL 표준 호환성**

<a id="0521c4a9edccc23c"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F492 | Optional table constraint enforcement | X |

<a id="1d1ba8cbac456eee"></a>
## ALTER TABLE name ALTER GLOBAL SECONDARY INDEX

<a id="2965dd56567ef33e"></a>
### 기능

테이블에서 global secondary index의 물리적 속성을 변경한다.

<a id="0339e3aacc045b31"></a>
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

<a id="32014511b3da40e1"></a>
### 사용 범위 및 접근 권한

&lt;alter table alter global secondary index storage statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="fc8a3947c22d4aa3"></a>
### 구문 규칙 및 파라미터

<a id="2373947e1ed9b830"></a>
#### table_name

인덱스를 생성할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="7f9fe00150d5dd4c"></a>
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

<a id="35de76c89d8e73d3"></a>
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

<a id="3659e3b0b2d380f9"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="7704ff6c85fed379"></a>
### 설명

Non-deterministic 질의를 하려면 global secondary index가 반드시 필요하다.

<a id="6b74f52f9083c7f6"></a>
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

<a id="b86ee5bda56c16bd"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="ac6d6e7395be54cd"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#7d73e98f397bd282)
- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#0779553a5fc95a3a)

<a id="f549758ead72dba5"></a>
## ALTER TABLE name ALTER GLOBAL SECONDARY INDEX COALESCE

<a id="1928ff2336d3b549"></a>
### 기능

Global secondary index의 단편화를 제거한다.

<a id="265c6b464ddfb6fc"></a>
### 구문

```
<global secondary index coalesce statement> ::=
    ALTER TABLE table_name ALTER GLOBAL SECONDARY INDEX COALESCE
    ;
```

<a id="3085a4dec3db7884"></a>
### 사용 범위 및 접근 권한

&lt;global secondary index coalesce statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 인덱스를 재구축할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 인덱스를 재구축할 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE
    - USAGE TABLESPACE ON DATABASE

<a id="a51a6402e16f95fd"></a>
### 구문 규칙 및 파라미터

<a id="85e0ea52c3e49f0d"></a>
#### table_name

대상 테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="a1f6b12728ecf41c"></a>
### 설명

- leaf 페이지들을 순차 탐색하며 병합 가능한 페이지들을 병합하고, 제거된 페이지들을 세그먼트로 반환한다.
- UPDATE / DELETE 등으로 인해 발생한 leaf 페이지의 단편화 문제를 해결할 수 있다.
- 인접한 leaf 페이지들이 병합 가능한 경우만 동작하므로 단편화 정도가 낮은 상태에서는 효과가 없을 수 있다.
- 인덱스의 단편화 정도가 심한 경우 INDEX REBUILD보다 더 오래 걸릴 수 있다.

**INDEX REBUILD와 비교**

<a id="d901b2d1d2237061"></a>
|  | INDEX REBUILD | INDEX COALESCE |
| --- | --- | --- |
| 인덱스 속성 변경 | 가능 | 불가능 |
| 테이블스페이스 이동 | 가능 | 불가능 |
| 테이블 잠금 | 필요 | 불필요 |
| 수행을 위한 추가 공간 | 필요 | 불필요 |
| 트리 높이 감소 | 가능 | 불가능 |

<a id="af44becd874cfd5a"></a>
### 사용 예

테이블 T1의 global secondary index의 단편화를 제거한다.

```
gSQL> ALTER TABLE T1 ALTER GLOBAL SECONDARY INDEX COALESCE;

Table altered.
```

<a id="8dfe72b7e0e0c44d"></a>
### 호환성

SQL 표준은 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="32f85b0ad22a3f6f"></a>
### 참조

관련 내용은 [ALTER TABLE ALTER GLOBAL SECONDARY INDEX REBUILD](#683708e586c10608)를 참조한다.

<a id="683708e586c10608"></a>
## ALTER TABLE name ALTER GLOBAL SECONDARY INDEX REBUILD

<a id="df9a5a2551c07ed2"></a>
### 기능

Global secondary index를 재구축한다.

<a id="56170ab1cd62b4f5"></a>
### 구문

```
<global secondary index rebuild statement> ::=
    ALTER TABLE table_name ALTER GLOBAL SECONDARY INDEX REBUILD
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

<a id="81b1df8711c15131"></a>
### 사용 범위 및 접근 권한

&lt;global secondary index rebuild statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 인덱스를 재구축할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 인덱스를 재구축할 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE
    - USAGE TABLESPACE ON DATABASE

<a id="71a3956cea42983d"></a>
### 구문 규칙 및 파라미터

<a id="d6310b2fc1138943"></a>
#### table_name

인덱스를 재구축할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="9b56898058d70a04"></a>
#### [ ONLINE | OFFLINE ]

인덱스를 재구축할 때, 해당 테이블에 DML을 허용할지 여부를 결정한다.

- ONLINE
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE이다.

<a id="bd558c7455b4ea48"></a>
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

<a id="1d6bc38eaae7b7dd"></a>
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

<a id="bccaec42010f03bd"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="334b88582c74989c"></a>
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

<a id="0c9835461e35be12"></a>
#### TABLESPACE tablespace_name

인덱스가 재구축될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - tablespace_name이 data tablespace면 LOGGING 인덱스로 재구축된다.
    - tablespace_name이 temporary tablespace 또는 nologging tablespace면 NOLOGGING 인덱스로 재구축된다.
- TABLESPACE 절을 생략할 경우, 기존 인덱스의 tablespace로 설정된다.

<a id="2115d7c08117c285"></a>
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

<a id="a66d2790e4245c09"></a>
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

<a id="c8a45654c8ba0aed"></a>
### 호환성

SQL 표준은 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="d96f122c07529cb1"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#7d73e98f397bd282)
- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#0779553a5fc95a3a)
- [ALTER INDEX name REBUILD](#fd0259278148017d)

<a id="f92321716f08611e"></a>
## ALTER TABLE name DROP CONSTRAINT

<a id="fa779ac0698cf920"></a>
### 기능

테이블 제약 조건을 제거한다.

<a id="2cb4cbac815738a6"></a>
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

<a id="cdfb1beec29ec0b8"></a>
### 사용 범위 및 접근 권한

&lt;drop table constraint definition&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 제약 조건의 소유자 
- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="94f0983402da6b47"></a>
### 구문 규칙 및 파라미터

<a id="7a80cb2832eef070"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="694cbb7d9cf296fa"></a>
#### CONSTRAINT constraint_name

제거할 제약 조건의 이름이다.

<a id="f5fd6fd84dca4dc1"></a>
#### PRIMARY KEY

테이블의 primary key 제약 조건이다.

<a id="5f36ceddd1728d21"></a>
#### UNIQUE( column_name [, ...] )

Column들에 대한 unique 제약 조건이다.

<a id="420736765b2fae7a"></a>
#### &lt;drop behavior&gt;

생략할 경우, 기본값은 RESTRICT 이다.   
현재는 RESTRICT/ CASCADE가 동일하게 작동한다.

<a id="4b4b6c0be512c83d"></a>
### 설명

제약 조건의 이름을 사용하지 않고 NOT NULL 제약 조건을 제거하려고 할 경우 [ALTER TABLE name ALTER COLUMN](#20641159e3d2762f) 구문의 &lt;[drop column not null clause&gt;](#c4347f0833b102b1) 절을 이용한다.

<a id="eafbbae88243bb5f"></a>
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

<a id="1cf5d67274c175f5"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- DROP PRIMARY KEY 
- DROP UNIQUE ( column_name [, ...] ) 
- CASCADE CONSTRAINTS

**SQL 표준 호환성**

<a id="e91844fb422da5d7"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="0e5a42bd5eaaf08a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#dbeb5fde894ac5df)
- [ALTER TABLE name ADD CONSTRAINT](#687f8d2d4bc52b07)
- [DROP INDEX](19-sql-references-c-g.md#d20adfa902b88837)

<a id="0779553a5fc95a3a"></a>
## ALTER TABLE name DROP GLOBAL SECONDARY INDEX

<a id="0b0716d978a252a9"></a>
### 기능

테이블에서 global secondary index를 제거한다.

<a id="d16dd50093b3b360"></a>
### 구문

```
<alter table drop global secondary index definition> ::=
    ALTER TABLE table_name 
        DROP GLOBAL SECONDARY INDEX
    ;
```

<a id="e2cc04041ceb3ec5"></a>
### 사용 범위 및 접근 권한

&lt;alter table drop global secondary index definition&gt; 구문은 cluster system에서 정의할 수 있으며 사용자는 다음 조건들을 만족해야 한다.

- 인덱스를 제거할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

<a id="ce83debbdc6d3624"></a>
### 구문 규칙 및 파라미터

<a id="1ae02c3f1f691a05"></a>
#### table_name

인덱스를 제거할 테이블 이름이다.

<a id="4dcdac7bac3bed43"></a>
### 설명

Non-deterministic 질의를 하려면 global secondary index가 반드시 필요하다.

<a id="ed1625f532509158"></a>
### 사용 예

테이블 T1에서 global secondary index를 제거한다.

```
gSQL> ALTER TABLE T1 DROP GLOBAL SECONDARY INDEX;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="128765960cb39f8e"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="bf31063a467d9f87"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#7d73e98f397bd282)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#1d1ba8cbac456eee)

<a id="12188ac1593e923a"></a>
## ALTER TABLE name DROP OFFLINE SEGMENTS

<a id="0d0f6d2a069a4662"></a>
### 기능

오프라인 된 shard들의 세그먼트를 삭제한다.

<a id="f5d7d6cf2a12a690"></a>
### 구문

```
<alter table drop offline segments statement> ::=
    ALTER TABLE table_name 
        DROP OFFLINE SEGMENTS    
;
```

<a id="cff2a687ea19203e"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table drop offline segments statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="5e39bcd3d62be656"></a>
### 구문 규칙 및 파라미터

<a id="2575a1061bf5b8ac"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="5107efbbbc8a31d2"></a>
### 설명

오프라인 된 shard들의 세그먼트를 삭제한다.

&lt;alter table drop offline segments statement&gt;는 inactive cluster member가 있어도 수행할 수 있다.

다음 조건들을 만족하지 못하면 실패한다.

- Cloned 테이블의 세그먼트들을 삭제하려면 클러스터 시스템 내에서 적어도 하나의 멤버에 cloned 테이블의 온라인 replica가 존재해야 한다.
- Sharded 테이블의 세그먼트들을 삭제하려면 그룹 당 적어도 하나의 멤버에 해당 sharded 테이블의 온라인 replica가 존재해야 한다.

예를 들어 sharded 테이블 t1의 cluster group G3에 있는 모든 replica들이 오프라인 상태일 경우 다음과 같은 에러가 발생한다.

```
gSQL> ALTER TABLE t1 DROP OFFLINE SEGMENTS;

ERR-42000(16361): sharded table "PUBLIC"."T1" must be accessible to at least one member of group 'G3'
```

모든 테이블들에 대해서 수행하려면 [&lt;alter database drop offline segments statement&gt;](#a56d9b8313449047) 구문을 사용한다.

<a id="b01c348b9c20047c"></a>
### 사용 예

다음은 테이블 t1에 대해 &lt;alter table drop offline segments statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 DROP OFFLINE SEGMENTS;

Table altered.
```

<a id="17f9490f4c2c5f46"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="ae3ac7fc8dcba6ff"></a>
### 참조

관련 내용은 [ALTER DATABASE DROP OFFLINE SEGMENTS](#a56d9b8313449047)를 참조한다.

<a id="b598685146fb8525"></a>
## ALTER TABLE name DROP SUPPLEMENTAL LOG

<a id="777a5ce01dc16691"></a>
### 기능

테이블의 데이터가 변경될 때 redo log에 primary key 정보를 남기지 않도록 설정한다.

<a id="4d30602c458b1af9"></a>
### 구문

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="219d6c022bc69fcb"></a>
### 사용 범위 및 접근 권한

&lt;drop table supplemental log statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="c04dd098605c0408"></a>
### 구문 규칙 및 파라미터

<a id="c4a660e2eac11043"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
[ALTER TABLE name ADD SUPPLEMENTAL LOG](#ff060f4d10146868) 구문을 사용해 설정된 상태여야 한다

<a id="c3ad0094710d1f20"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="589ceea258c870c8"></a>
### 사용 예

다음은 테이블의 데이터가 변경되었을 때 redo log에 primary key 정보를 남기지 않도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="6094c4caf2ba5d4a"></a>
### 호환성

SQL 표준에서는 &lt;drop table supplemental log statement&gt;를 다루지 않는다.

<a id="17b11ce95124d828"></a>
## ALTER TABLE name MERGE SHARDS

<a id="7df038afa5f2f816"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard들을 merge 하여 재배치한다.

<a id="8e009634e9caf94a"></a>
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

<a id="9e051a5ef9ceca0b"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table merge shards statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="f4705c55cfcb1fe6"></a>
### 구문 규칙 및 파라미터

<a id="a68f25fc98c9a3d6"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
해당 테이블이 cluster-specific이고 list shard 또는 range shard인 경우에만 구문을 수행할 수 있다.

<a id="91b300a7b10bf4fb"></a>
#### &lt;source shard list&gt;

Merge 할 원본 shard들의 list 이다.  
List에서 지정한 shard가 해당 테이블에 반드시 존재해야 한다.

<a id="eb8383ae51e96013"></a>
#### source_shard_name

Merge 할 원본 shard의 이름이다.  
해당 테이블에 존재하지 않는 shard인 경우 구문을 수행할 수 없다.

<a id="5a727e3f03b72d7a"></a>
#### start_shard_name

Merge 할 범위 중 시작 shard의 이름이다.   
Range shard에서만 사용된다.

<a id="7855b7ce668fbc94"></a>
#### end_shard_name

Merge 할 범위 중 마지막 shard의 이름이다.  
Range shard에서만 사용된다.

<a id="c00b3488636c143c"></a>
#### dest_shard_name

대상 shard의 이름이다.

<a id="9bd97f21e23a99f3"></a>
#### &lt;dest shard placement&gt;

대상 shard가 배치될 cluster group의 이름이다.  
해당 구문이 생략된 경우, dest_shard_name이 &lt;source shard list&gt;에 포함되어 있어야 한다.

<a id="7aa76277ace4abad"></a>
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

<a id="143cf2f46d32d75d"></a>
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

<a id="5d100b5d77207c75"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="3eeece9ca23c8c97"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name MOVE SHARD](#a93d376fd2ef5b9b)
- [ALTER TABLE name SPLIT SHARD](#6e8d2bde00700ace)

<a id="a93d376fd2ef5b9b"></a>
## ALTER TABLE name MOVE SHARD

<a id="8d06ad0f94c18311"></a>
### 기능

테이블의 특정 shard 또는 특정 cluster group의 전체 shard를 특정 cluster group에 재배치한다.

<a id="c7e0565e81c49b35"></a>
### 구문

```
<alter table move shard statement> ::=
    ALTER TABLE table_name MOVE SHARD
        { shard_name_list | FROM CLUSTER GROUP src_cluster_group }
        TO CLUSTER GROUP dest_cluster_group 
       [ ONLINE | OFFLINE ] 
       [ <shard divisor> ] 
       [ <parallel clause> ]
    ;

<shard divisor> ::= 
    SHARD DIVISOR integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="c84215862f7f136c"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table move shard statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="138f4f3a4ecf5466"></a>
### 구문 규칙 및 파라미터

<a id="4f78b9ed94ed9577"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
해당 테이블이 cluster group specific인 경우에만 구문을 수행할 수 있다.

<a id="f32dc17733d3cdcb"></a>
#### shard_name_list

재배치할 shard name 목록이다.  
해당 테이블에 존재하지 않는 shard인 경우 구문을 수행할 수 없다.

<a id="1c1aaf2cbfa5524d"></a>
#### src_cluster_group

재배치할 특정 cluster group의 이름이다.

<a id="e3782521fb16fbdc"></a>
#### dest_cluster_group

테이블의 shard를 배치할 target cluster group의 이름이다.  
해당 테이블의 shard가 지정한 cluster group에 이미 존재할 경우 구문을 수행할 수 없다.

<a id="4bd6b592b99856a4"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="7d447c1e24b6599f"></a>
#### &lt;shard divisor&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버에 재배치 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, REBALANCE_SHARD_DIVISOR 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="dd2ded344bf432f4"></a>
#### &lt;parallel clause&gt;

테이블 재배치에 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 병렬로 테이블을 재배치하지 않는다.
- PARALLEL [integer] 
    - 병렬로 테이블을 재배치한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="cf2319402bb5003f"></a>
### 설명

테이블의 특정 shard를 특정 cluster group에서 다른 cluster group으로 재배치한다.

특정 cluster group을 제거하려면 테이블의 shard를 재배치한 후에 [DROP CLUSTER GROUP](19-sql-references-c-g.md#6d9454a76620869e) 구문을 수행해야 한다.

모든 테이블의 shard를 특정 cluster group에서 다른 cluster group으로 이동시키는 경우, ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP TO CLUSTER GROUP 구문을 수행한다.

CLONED 테이블이거나 CLUSTER WIDE로 설정된 테이블의 경우 에러가 발생하면서 실패할 수 있다.

<a id="f2cebb6866dee4a7"></a>
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

<a id="3d246df083b3155a"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="bf2a310a5a750566"></a>
### 참조

관련 내용은 [ALTER DATABASE MOVE SHARD](#5068226dae906bd2)를 참조한다.

<a id="b2ad57535b47fe58"></a>
## ALTER TABLE name READ { ONLY | WRITE }

<a id="1c68026d95878515"></a>
### 기능

테이블에 READ { ONLY | WRITE }을 설정한다.

<a id="903450d0ba61fb2c"></a>
### 구문

```
<alter table read { only | write } statement> :==
     ALTER TABLE table_name
         READ { ONLY | WRITE }
     ;
```

<a id="afcb4b25ef1dada8"></a>
### 사용 범위 및 접근 권한

&lt;alter table read { only | write } statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="c8d50bff47d558a6"></a>
### 구문 규칙 및 파라미터

<a id="d23660184d2f4891"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="1b210b5c8e059fc3"></a>
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

<a id="337da82df718ce2b"></a>
### 사용 예

다음은 &lt;alter table read { only | write } statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 READ ONLY;

Table altered.

gSQL> ALTER TABLE t1 READ WRITE;

Table altered.
```

<a id="415fa5876463f48d"></a>
### 호환성

SQL 표준에서는 &lt;alter table read { only | write } statement&gt; 구문을 정의하지 있지 않다.

<a id="559213b63e8e6826"></a>
### 참조

관련 내용은 [ALTER TABLE](#dbeb5fde894ac5df)을 참조한다.

<a id="149294331f00fde7"></a>
## ALTER TABLE name REBALANCE

<a id="16ac0177545fbb46"></a>
### 기능

테이블의 shard를 재배치한다.

<a id="ab86b1907bc1ccbc"></a>
### 구문

```
<alter table rebalance statement> ::=
    ALTER TABLE table_name REBALANCE 
       [ ONLINE | OFFLINE ] 
       [ <shard divisor> ] 
       [ <parallel clause> ]
    ;

<shard divisor> ::= 
    SHARD DIVISOR integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="3460af63169c0cd4"></a>
### 사용 범위 및 접근 권한

Cluster system 에서 수행할 수 있다.

&lt;alter table rebalance statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="80ba5e802fed89db"></a>
### 구문 규칙 및 파라미터

<a id="29cdf97397ee3abb"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="900b791fcaa8efa7"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="1d8102ecad3efdd5"></a>
#### &lt;shard divisor&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버에 재배치 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, REBALANCE_SHARD_DIVISOR 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="587fefde0c7e8894"></a>
#### &lt;parallel clause&gt;

테이블 재배치에 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 병렬로 테이블을 재배치하지 않는다.
- PARALLEL [integer] 
    - 병렬로 테이블을 재배치한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="2dfdf8deb9321a34"></a>
### 설명

다음과 같은 구문을 통해 cluster member, cluster group을 추가할 때 table들의 shard는 재배치하지 않는다.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#420c16ac60aa5c3d)
- [ALTER CLUSTER GROUP name ADD MEMBER](#4d285ac15daae9e5)

추가된 cluster group과 cluster member의 테이블 shard를 재배치하려면 &lt;alter table rebalance statement&gt; 구문을 수행한다. 테이블의 shard 가 이미 재배치된 경우, 별도의 재배치 작업없이 성공한다.

모든 테이블들의 shard를 재배치하려면 [ALTER DATABASE REBALANCE](#f07ba634c9eef9cf) 구문을 수행한다.

<a id="02cee5b832347d5f"></a>
### 사용 예

다음은 &lt;alter table rebalance statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 REBALANCE;

Table altered.
```

<a id="1d424b69093b6aeb"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="21c0fa70c04ce272"></a>
## ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list

<a id="eba1cd5d911a6f37"></a>
### 기능

특정 cluster group에 shard를 포함하지 않도록 테이블의 shard를 재배치한다.

<a id="2249088b784532c5"></a>
### 구문

```
<alter table rebalance exclude cluster group statement> ::=
    ALTER TABLE table_name REBALANCE 
        EXCLUDE CLUSTER GROUP cluster_group_list 
       [ ONLINE | OFFLINE ] 
       [ <shard divisor> ] 
       [ <parallel clause> ]
    ;

<shard divisor> ::= 
    SHARD DIVISOR integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="6c38f6639ddf463b"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table rebalance exclude cluster group statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="a11a5626ac43956c"></a>
### 구문 규칙 및 파라미터

<a id="f2692680d7aea68d"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
해당 테이블이 cluster-wide인 경우에만 구문을 수행할 수 있다.

<a id="d9a25368a3a9b00a"></a>
#### cluster_group_list

테이블의 shard를 포함하지 않는 cluster group의 list이다.   
재배치에서 제외될 cluster group이 cluster 전체 group인 경우 구문을 수행할 수 없다.

<a id="06de742479d5b0d0"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE 를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE 를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="655ec464039d9cea"></a>
#### &lt;shard divisor&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버에 재배치 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, REBALANCE_SHARD_DIVISOR 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="073a4e3f23f6fc68"></a>
#### &lt;parallel clause&gt;

테이블 재배치에 사용할 thread의 개수를 지정한다.

- NOPARALLEL
    - 병렬로 테이블을 재배치하지 않는다.
- PARALLEL [integer] 
    - 병렬로 테이블을 재배치한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="0c701de69ed22ef0"></a>
### 설명

특정 cluster group을 배제하고 테이블의 shard를 재배치한다.   
해당 cluster group에 테이블의 shard가 존재하지 않을 경우, 별도의 재배치 작업없이 성공한다.   
테이블의 shard가 위치한 cluster group을 기준으로 shard를 재배치한다.

특정 cluster group을 제거하려면 테이블의 shard를 재배치한 후에 [DROP CLUSTER GROUP](19-sql-references-c-g.md#6d9454a76620869e) 구문을 수행해야 한다.  
모든 테이블들에서 cluster group을 배제하고 shard를 재배치하고자 할 경우, [ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP](#66647a34894da55f)을 수행한다.

<a id="53886365566cf156"></a>
### 사용 예

다음은 &lt;alter table rebalance exclude cluster group statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 REBALANCE EXCLUDE CLUSTER GROUP g3;

Table altered.
```

<a id="23d5da90b1b9e084"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="76eb6b8299dccb24"></a>
## ALTER TABLE name RENAME COLUMN

<a id="62a73609f33ac9bd"></a>
### 기능

테이블 column의 이름을 변경한다.

<a id="aa4884dc5aba6d81"></a>
### 구문

```
<rename column statement> ::=
    ALTER TABLE table_name 
        RENAME COLUMN old_column_name TO new_column_name
    ;
```

<a id="7444093991ecc2d7"></a>
### 사용 범위 및 접근 권한

&lt;rename column statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="87c154b36d997235"></a>
### 구문 규칙 및 파라미터

<a id="a9656f2ea17d8674"></a>
#### table_name

변경할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="76b8f74db2a9826c"></a>
#### old_column_name

변경할 column의 기존 이름이다.

<a id="7a56112bf40f1a4e"></a>
#### new_column_name

변경할 column의 새로운 이름이다.   
테이블 내에 동일한 column 이름이 존재하지 않아야 한다.

<a id="9f80b8672d7f43d7"></a>
### 설명

Column 이름이 변경되더라도 이전에 해당 column을 기준으로 생성된 index, constraint 등의 객체를 변경할 필요는 없다.

<a id="c3dd7a71fcfedf5e"></a>
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

<a id="f5c4f6daad9341c3"></a>
### 호환성

SQL 표준에서는 &lt;rename column statement&gt; 구문을 정의하지 않고 있다.

<a id="16007fb621efa473"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#dbeb5fde894ac5df)
- [ALTER TABLE name ADD COLUMN](#eccd1f42db335101)
- [ALTER TABLE name SET UNUSED COLUMN](#c309a04b3589e0b4)
- [ALTER TABLE name ALTER COLUMN](#20641159e3d2762f)

<a id="f2bbf6bbdf160660"></a>
## ALTER TABLE name RENAME CONSTRAINT

<a id="96cb3550f6662045"></a>
### 기능

테이블 제약 조건의 이름을 변경한다.

<a id="566c5462852b46d0"></a>
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

<a id="bb505c017aa0d60b"></a>
### 사용 범위 및 접근 권한

&lt;rename table constraint statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="538a0b5f252fad01"></a>
### 구문 규칙 및 파라미터

<a id="459a555b20457364"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="d2cde72f4c09bdd6"></a>
#### &lt;constraint object&gt;

변경할 제약 조건의 기존 이름은 다음과 같이 지정할 수 있다.

- CONSTRAINT constraint_name
    - 변경할 제약 조건의 이름이다.
- PRIMARY KEY
    - 테이블의 PRIMARY KEY 제약 조건이다.
- UNIQUE( column [,...] )
    - Column 목록에 부합되는 UNIQUE 제약 조건이다.

<a id="61f48605fcd18369"></a>
#### new_column_name

변경할 제약 조건의 새로운 이름이다.

<a id="3b082b1dcd0fe54c"></a>
### 설명

Primary key, unique key와 같이 key 제약 조건으로 자동 생성된 index의 이름은 변경되지 않는다. Index 이름은 [ALTER INDEX name RENAME TO](#b3aaf811285301ef) 구문을 사용하여 변경해야 한다.

<a id="7a58109fe1b79883"></a>
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

<a id="50c18d3ee6bb4acb"></a>
### 호환성

SQL 표준에서는 &lt;rename table constraint statement&gt; 구문을 정의하지 않고 있다.

<a id="662663735e6ee10a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#dbeb5fde894ac5df)
- [ALTER TABLE name ADD CONSTRAINT](#687f8d2d4bc52b07)
- [ALTER TABLE name DROP CONSTRAINT](#f92321716f08611e)
- [ALTER TABLE name ALTER CONSTRAINT](#945ef430d7091816)

<a id="7ae6adc965bf6c07"></a>
## ALTER TABLE name RENAME SHARD

<a id="366624795818cc20"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard의 이름을 변경한다.

<a id="3a672a3f8cbcc267"></a>
### 구문

```
<alter table rename shard statement> ::=
    ALTER TABLE table_name 
        RENAME SHARD shard_name TO new_shard_name
    ;
```

<a id="9e8494ed6641e69b"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table rename shard statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="d383225d5919d95e"></a>
### 구문 규칙 및 파라미터

<a id="c3a96c2cc723837a"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="360ef94da324388a"></a>
#### shard_name

변경할 shard의 기존 이름이다.   
Shard가 해당 테이블에 존재하지 않을 경우 구문을 수행할 수 없다.

<a id="7478441af059e3c5"></a>
#### new_shard_name

변경할 shard의 새 이름이다.   
테이블 내에 동일한 shard 이름이 존재하지 않아야 한다.

<a id="cd849e5706092361"></a>
### 설명

Hash, range, list 테이블의 특정 shard의 이름을 변경한다. Cloned 테이블에 대해서는 해당 구문을 수행할 수 없다.

<a id="277638503f10cb5a"></a>
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

<a id="942710415eb03666"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="6ae2a88b165703cc"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#dbeb5fde894ac5df)
- [ALTER TABLE name MOVE SHARD](#a93d376fd2ef5b9b)
- [ALTER TABLE name SPLIT SHARD](#6e8d2bde00700ace)
- [ALTER TABLE name REBALANCE](#149294331f00fde7)

<a id="079b6bb5fd726b84"></a>
## ALTER TABLE name RENAME TO

<a id="77c27a009ecf3d7a"></a>
### 기능

테이블의 이름을 변경한다.

<a id="05db81bd5ff49f16"></a>
### 구문

```
<rename table statement> ::=
    ALTER TABLE table_name 
        RENAME TO new_table_name
    ;
```

<a id="f645d1999b3a11b0"></a>
### 사용 범위 및 접근 권한

&lt;rename table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="5ab1402ae75b7585"></a>
### 구문 규칙 및 파라미터

<a id="1ed16e754d019f72"></a>
#### table_name

테이블의 기존 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="30d0bf4a81eeda0e"></a>
#### new_table_name

테이블의 새 이름이다.   
스키마 내에 동일한 테이블 이름이 존재하지 않아야 한다.

<a id="6fa61077c52a446e"></a>
### 설명

테이블 이름이 변경되더라도 이를 참조하는 index constraint 등의 객체는 변경할 필요없다.

<a id="149bc6cba8da187c"></a>
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

<a id="b5a5cbf221d916f5"></a>
### 호환성

SQL 표준에서는 &lt;rename table statement&gt; 구문을 정의하지 않고 있다.

<a id="c1df8629fb6c54a8"></a>
### 참조

관련 내용은 [ALTER TABLE](#dbeb5fde894ac5df)을 참조한다.

<a id="c309a04b3589e0b4"></a>
## ALTER TABLE name SET UNUSED COLUMN

<a id="e141eecaa332a648"></a>
### 기능

테이블 column을 제거한다.

<a id="41dbda703068c562"></a>
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

<a id="f4f5f132f86a1854"></a>
### 사용 범위 및 접근 권한

&lt;drop column definition&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="3c743a6082c59550"></a>
### 구문 규칙 및 파라미터

<a id="1108439c4d318deb"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="2f8ab101f9fd2dc1"></a>
#### SET UNUSED [ COLUMN ]

해당 column들을 사용하지 않도록 설정한다.

<a id="76939fd649b19794"></a>
#### column_name_list

한 개 이상의 삭제될 column 이름이다.

- 예: ALTER TABLE t1 SET UNUSED COLUMN c1 
- 예: ALTER TABLE t1 SET UNUSED COLUMN (c1, c2)

<a id="80c24b6a8c634eea"></a>
#### column_name

삭제할 column의 이름이다.   
해당 column을 이용하는 제약 조건과 인덱스도 함께 삭제한다.

<a id="bdd66a3501d776f5"></a>
#### drop behavior

생략할 경우, 기본값은 RESTRICT 이다.   
현재는 RESTRICT/ CASCADE가 동일하게 작동한다.

<a id="b03ccefdc1eb6361"></a>
### 설명

SET UNUSED COLUMN은 data를 물리적으로 제거하지 않으므로 row의 개수에 관계없이 일정한 성능을 보장한다.

<a id="22d599aca2475546"></a>
### 사용 예

다음은 해당 column을 사용하지 않도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 SET UNUSED COLUMN ( addr );

Table altered.
```

<a id="98702f0b3035ecb8"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- SET UNUSED 
- CASCADE CONSTRAINTS 
- 다수의 column 나열

**SQL 표준 호환성**

<a id="b6af653e1467e609"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F033 | ALTER TABLE statement: DROP COLUMN clause | X |

<a id="6c2f0ad5e452b084"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#dbeb5fde894ac5df)
- [ALTER TABLE name ADD COLUMN](#eccd1f42db335101)
- [ALTER TABLE name ALTER COLUMN](#20641159e3d2762f)
- [ALTER TABLE name RENAME COLUMN](#76eb6b8299dccb24)

<a id="6e8d2bde00700ace"></a>
## ALTER TABLE name SPLIT SHARD

<a id="31e417868b33f5b3"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard를 split하여 재배치한다.

<a id="78a078bb8a6360ec"></a>
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

<a id="e202af955c443c5c"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table split shard statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="3528b8a445b28723"></a>
### 구문 규칙 및 파라미터

<a id="218d3e36fd8fc894"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
해당 테이블이 cluster group specific이고 list shard 또는 range shard인 경우에만 구문을 수행할 수 있다.

<a id="9cab0caffdd61d33"></a>
#### source_shard_name

Split할 원본 shard 이름이다.   
해당 테이블에 shard가 존재하지 않을 경우 구문을 수행할 수 없다.

<a id="b38b94267d585bc9"></a>
#### &lt;split shard placement&gt;

원본 shard를 split하여 재배치할 대상 shard를 정의한다.

<a id="eb9b090716e49919"></a>
#### &lt;split shard bound def&gt;

split될 대상 shard의 bound를 정의한다.

다음 두 가지 bound def 중 하나로 정의할 수 있다.

- &lt;split list shard def&gt;
- &lt;split range shard def&gt;

<a id="354e9484fd375ed9"></a>
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

<a id="79eea0f2c4208cd9"></a>
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

<a id="e471cfa1ee2efee3"></a>
#### dest_group_name

Split 된 shard가 배치될 cluster group의 이름이다.

<a id="76aad4b4b9a379ee"></a>
### 설명

특정 테이블의 특정 shard를 분산하여 임의의 cluster group에 배치한다.  
특정 shard에 해당하는 레코드가 많거나 특정 group member에 부하가 편중될 때 shard를 분산하여 레코드와 부하를 분산하기 위해 사용된다.

<a id="c492d6f7acd59d07"></a>
### 사용 예

다음은 &lt;alter table split shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES IN ( 11 ) AT CLUSTER GROUP G2 );

Table altered.

gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES LESS THAN ( 11 ) AT CLUSTER GROUP G2 );


Table altered.
```

<a id="39d41cbfc501b352"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="e386370ffe75b547"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name REBALANCE](#149294331f00fde7)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#21c0fa70c04ce272) 
- [ALTER TABLE name MOVE SHARD](#a93d376fd2ef5b9b)
- [ALTER TABLE name MERGE SHARDS](#17b11ce95124d828)

<a id="6f64550f92fa2c88"></a>
## ALTER TABLE name STORAGE

<a id="2424989e17967c55"></a>
### 기능

테이블의 물리적 속성을 변경한다.

<a id="e90c53a56ce10d51"></a>
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

<a id="90c2d9238b4e146c"></a>
### 사용 범위 및 접근 권한

&lt;alter table physical attribute statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="4538f9d92478a0a9"></a>
### 구문 규칙 및 파라미터

<a id="14e5023c448e5e17"></a>
#### table_name

변경할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="ae37957bc90c3231"></a>
#### &lt;physical attribute clause&gt;

테이블을 구성하는 page의 물리적 속성을 변경한다.  
이미 할당된 page에는 적용되지 않으며 새로 할당받는 page에 적용된다.  
자세한 설명은 [CREATE TABLE](19-sql-references-c-g.md#060501387611d25a) 구문의 [&lt;table physical attribute clause&gt;](19-sql-references-c-g.md#337e3e2fbd13ebdc) 절을 참조한다.

<a id="668b30ae0284a0e5"></a>
#### &lt;segment attr clause&gt;

세그먼트를 구성하는 extent의 물리적 속성을 변경한다.   
이미 할당된 extent에는 적용되지 않으며, 새로 할당받는 extent에 적용된다.

- MAXSIZE integer 
    - 할당될 수 있는 세그먼트 공간의 크기를 변경한다. 
    - 이미 할당되어 있는 공간보다 작은 크기를 지정하면 에러가 발생한다.

<a id="be54819c5961ae65"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="70d56ce895426231"></a>
### 사용 예

다음은 테이블의 물리적 속성을 변경하는 예이다.

```
gSQL> ALTER TABLE t1 PCTFREE 10 PCTUSED 40 STORAGE ( NEXT 10M  MAXSIZE  100M );

Table altered.
```

<a id="b82794419e3ddd2c"></a>
### 호환성

SQL 표준에서는 테이블의 물리적 속성에 대하여 정의하지 않고 있다.

<a id="35e98395e6af2724"></a>
### 참조

관련 내용은 [ALTER TABLE](#dbeb5fde894ac5df)을 참조한다.

<a id="c03af2d66eb7e9c7"></a>
## ALTER TABLE name SYNCHRONIZE

<a id="f9c0bca04a9c376d"></a>
### 기능

기존에 배치되어 있는 테이블의 shard들을 원격으로 동기화한다.

<a id="2a6f99c0fae93dd5"></a>
### 구문

```
<alter table synchronize statement> ::=
    ALTER TABLE table_name SYNCHRONIZE 
       [ ONLINE | OFFLINE ] 
       [ <shard divisor> ] 
       [ <parallel clause> ]
    ;

<shard divisor> ::= 
    SHARD DIVISOR integer

<parallel clause> ::=
    NOPARALLEL
  | PARALLEL [ integer ]
```

<a id="815b0b2293858f89"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table synchronize statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="09e1b46ae48e1e1c"></a>
### 구문 규칙 및 파라미터

<a id="d1ac956e6a65f3b1"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="4505d7e3a8df161f"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 동기화할 때 DML을 허용할지 여부를 결정한다

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="22f9dc056438ed04"></a>
#### &lt;shard divisor&gt;

shard의 partition 개수를 지정한다.

- partition 개수 만큼 shard를 분할하여 원격 서버와 동기화 한다. 
- integer는 0부터 사용할 수 있으며 최대값은 1000이다.
- 생략할 경우, REBALANCE_SHARD_DIVISOR 프로퍼티를 따른다.
- integer가 parallel integer 보다 작은 경우에는 parallel integer와 같은 값으로 보정된다.

<a id="1203f9ae7e9cacfb"></a>
#### &lt;parallel clause&gt;

테이블을 동기화할 때 사용할 thread 개수를 지정한다.

- NOPARALLEL
    - 테이블을 병렬로 동기화하지 않는다.
- PARALLEL [integer] 
    - 테이블을 병렬로 동기화한다. 
    - integer는 0부터 사용할 수 있으며 최대값은 64이다. 
    - integer가 생략된 경우는 0이다. 
    - integer가 0인 경우에는 시스템이 최적값을 결정한다.

<a id="7899ccb8921d3e6a"></a>
### 설명

테이블 동기화는 기존에 배치되어 있는 오프라인 된 shard들을 동기화하여 정합성을 복구한다. [&lt;alter table rebalance statement&gt;](#149294331f00fde7)와는 달리 inactive cluster member가 있어도 수행할 수 있다.

다음 조건들을 만족하지 못하면 실패한다.

- Cloned 테이블의 shard들을 동기화 하려면 클러스터 시스템 내에서 적어도 하나의 멤버에 cloned 테이블의 온라인 replica가 존재해야 한다.
- Sharded 테이블의 shard들을 동기화 하려면 그룹 당 적어도 하나의 멤버에 해당 sharded 테이블의 온라인 replica가 존재해야 한다.

예를 들어 sharded 테이블 t1의 cluster group G3에 있는 모든 replica들이 오프라인 상태일 경우 다음과 같은 에러가 발생한다.

```
gSQL> ALTER TABLE t1 SYNCHRONIZE;

ERR-42000(16546): sharded table "PUBLIC"."T1" must have at least one online replica of group 'G3'
```

모든 테이블들의 shard를 동기화하려면 [&lt;alter database synchronize statement&gt;](#7358cd448c66ad8b)를 수행한다.

<a id="4ebae4599a27a607"></a>
### 사용 예

다음은 테이블 t1에 대해서 &lt;alter table synchronize statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 SYNCHRONIZE;

Table altered.
```

<a id="aec617e749b18a93"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="8b18eb3f445c48b1"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#dbeb5fde894ac5df)
- [ALTER TABLE name REBALANCE](#149294331f00fde7)
- [ALTER DATABASE SYNCHRONIZE](#7358cd448c66ad8b)

<a id="e50680549a4cafe3"></a>
## ALTER TABLESPACE

<a id="b9e8514ca365a605"></a>
### 기능

테이블스페이스의 정의를 변경한다.

<a id="5e319b68aff02eba"></a>
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

<a id="1c4587a02c66f6b3"></a>
### 사용 범위 및 접근 권한

&lt;alter tablespace statement&gt; 구문을 수행하려면 사용자에게 database에 대한 ALTER TABLESPACE 권한이 있어야 한다.

<a id="0058d7c474381b89"></a>
### 구문 규칙 및 파라미터

<a id="5b4052300b2788ba"></a>
#### &lt;rename tablespace statement&gt;

테이블스페이스의 이름을 변경한다.  
자세한 내용은 [ALTER TABLESPACE name RENAME TO](#34212132a1ef93f1) 구문을 참조한다.

<a id="32bd040ef715b2f3"></a>
#### &lt;backup tablespace statement&gt;

테이블스페이스를 백업한다.  
자세한 내용은 [ALTER TABLESPACE name BACKUP](#af7c53d2132a4178) 구문을 참조한다.

<a id="849e05836853ef14"></a>
#### &lt;on-offline tablespace statement&gt;

테이블스페이스의 모든 파일을 online 또는 offline으로 변경한다.  
자세한 내용은 [ALTER TABLESPACE name [ONLINE|OFFLINE]](#ecd840aaa27cb6b1) 구문을 참조한다.

<a id="5aa06103e134c9d5"></a>
#### &lt;add file statement&gt;

테이블스페이스에 파일을 추가한다.  
자세한 내용은 [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#3e855076351fa5c9) 구문을 참조한다.

<a id="efff67bec88a1212"></a>
#### &lt;drop file statement&gt;

테이블스페이스의 파일을 제거한다.  
자세한 내용은 [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#c4555abd12b44a7b) 구문을 참조한다.

<a id="90533b00210fc977"></a>
#### &lt;rename datafile statement&gt;

데이터 테이블스페이스의 데이터 파일 이름을 변경한다.  
자세한 내용은 [ALTER TABLESPACE name RENAME DATAFILE](#1e33e3f9ea894d62) 구문을 참조한다.

<a id="5032a516f3d4b36b"></a>
### 설명

ALTER TABLESPACE 구문은 다른 Data Definition Language (DDL)과 달리 ROLLBACK 할 수 없고 구문을 수행한 transaction이 자동으로 COMMIT 된다.

<a id="f3628610120f752e"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="7e5d7349baa97196"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="55be62090d303c1a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLESPACE](19-sql-references-c-g.md#c81940ba4a84752c)
- [DROP TABLESPACE](19-sql-references-c-g.md#0905e5b2ffc06135)

<a id="3e855076351fa5c9"></a>
## ALTER TABLESPACE name ADD [DATAFILE|MEMORY]

<a id="7d74c351e78fd5c6"></a>
### 기능

테이블스페이스의 공간을 확장한다.

<a id="51719b10cb130470"></a>
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

<a id="5b03741244fa3eaa"></a>
### 사용 범위 및 접근 권한

&lt;add space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="8c99f509ad45a224"></a>
### 구문 규칙 및 파라미터

<a id="3ac31141cb265785"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="e1735208d544e735"></a>
#### &lt;file specification&gt;

테이블스페이스의 유형에 따라 다음과 같은 구문을 사용해야 한다.

- 메모리 데이터 테이블스페이스 
    - DATAFILE &lt;add datafile clause&gt; 
- 메모리 임시 테이블스페이스 
    - MEMORY &lt;memory clause&gt;

<a id="efe26d2649f4f9e5"></a>
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

<a id="a3b7f0bf062ac0c0"></a>
#### &lt;memory clause&gt;

- &lt;size clause&gt;
    - 추가할 메모리를 정의한다.

자세한 내용은 [CREATE MEMORY TEMPORARY TABLESPACE](19-sql-references-c-g.md#101999ca47732e9f) 구문의 [&lt;memory clause&gt;](19-sql-references-c-g.md#ca249eb4444df6f6)를 참조한다.

<a id="b3360518d06f3914"></a>
#### &lt;autoextend clause&gt;

디스크 테이블스페이스의 데이터 파일이 추가될 때 자동 확장 속성을 설정한다. 자동 확장 속성을 ON 또는 OFF로 설정한다. ON으로 설정하면 자동 확장 크기와 데이터 파일의 최대 크기를 지정할 수 있다.

<a id="1e8af79cd64dc63e"></a>
#### &lt;next size clause&gt;

현재 사용 중인 데이터 파일에 더 이상 사용할 공간이 없을 때 확장할 크기를 지정한다.

<a id="36eabd9f626c941c"></a>
#### &lt;max size clause&gt;

데이터 파일이 확장될 수 있는 최대 크기를 지정한다.

<a id="065589d1359b92d2"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="e0686a318f094899"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="b5622f997dbbc7f8"></a>
### 사용 예

다음은 테이블스페이스에 data file을 추가하는 예이다.

```
gSQL> ALTER TABLESPACE space1 ADD DATAFILE 'test_file_a2.dbf' SIZE 10M REUSE;

Tablespace altered.
```

<a id="244ce12017914786"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="6f56ec45c4891625"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE MEMORY DATA TABLESPACE](19-sql-references-c-g.md#5dc8246fbc0a52e1)
- [CREATE MEMORY TEMPORARY TABLESPACE](19-sql-references-c-g.md#101999ca47732e9f)
- [ALTER TABLESPACE](#e50680549a4cafe3)

<a id="af7c53d2132a4178"></a>
## ALTER TABLESPACE name BACKUP

<a id="0515a2dea18b64b0"></a>
### 기능

테이블스페이스를 backup 하기 위해 backup이 가능한 상태와 불가능한 상태로 전환한다.

<a id="864cfff774ec7002"></a>
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

<a id="67fd1acef0b9b2f3"></a>
### 사용 범위 및 접근 권한

&lt;backup space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="c1596085aace246b"></a>
### 구문 규칙 및 파라미터

<a id="e688ddc7b3cad329"></a>
#### &lt;tablespace begin backup statement&gt;

테이블스페이스를 백업 가능한 상태로 설정한다.

- 생성되어 사용 중인 테이블스페이스를 백업 가능한 상태로 설정한다.
- OFFLINE/ temporary 테이블스페이스는 backup 상태는 전환할 수 없다.

<a id="957b9271a37f0481"></a>
#### tablespace_name

Backup 상태를 전환할 테이블스페이스의 이름이다.

<a id="c3adefef81b0571f"></a>
#### &lt;tablespace end backup statement&gt;

테이블스페이스를 백업이 불가능한 상태로 설정한다.

<a id="7ead19ffdb1964f7"></a>
#### &lt;tablesapce incremental backup statement&gt;

테이블스페이스의 증분 백업을 수행한다.  
데이터베이스가 OPEN 상태이고, ARCHIVELOG로 운영되어야 한다.

<a id="655bd3896bd7f3ce"></a>
#### &lt;incremental backup option&gt;

- 'integer'는 0 ~ 4 까지 지정할 수 있다.
- 'LEVEL 0'는 CUMULATIVE나 DIFFERENTIAL을 지정할 수 없다.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - 'integer'가 n이면 가장 최근에 'LEVEL 0' ~ 'LEVEL n-1'까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - DIFFERENTIAL
        - 'integer'가 n이면 가장 최근에 'LEVEL 0' ~ 'LEVEL n'까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - 생략되면 DIFFERENTIAL이 기본으로 지정된다.

<a id="bf501b83c2f0dd5d"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="5627dc141f813af1"></a>
### 설명

테이블스페이스에 생성된 datafile을 백업한다. 테이블스페이스 전체를 백업하려면 BEGIN BACKUP을 수행한 후 OS의 파일 복사로 datafile들을 복사하고 나서 END BACKUP을 수행한다. 한편, 증분 백업 파일은 하나의 구문으로 BACKUP_DIR_1 property에 설정된 경로에 생성한다.

<a id="9cebc4328911b3ad"></a>
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

<a id="00a2873855f6dc08"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="3de3e747f87ea421"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#e50680549a4cafe3)
- [ALTER TABLESPACE name [ONLINE|OFFLINE]](#ecd840aaa27cb6b1)

<a id="c4555abd12b44a7b"></a>
## ALTER TABLESPACE name DROP [DATAFILE|MEMORY]

<a id="fba2f2c518109b31"></a>
### 기능

테이블스페이스의 공간을 축소한다.

<a id="be3ec9d8567c1819"></a>
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

<a id="45a55c3d0acad6eb"></a>
### 사용 범위 및 접근 권한

&lt;drop space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="efd777ff50d84f3a"></a>
### 구문 규칙 및 파라미터

<a id="94efe214c018ea75"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="261689bb0c049d64"></a>
#### &lt;file specification&gt;

테이블스페이스의 유형에 따라 다음과 같은 구문을 사용해야 한다.

- 메모리 데이터 테이블스페이스 
    - DATAFILE 'filename' 
- 메모리 임시 테이블스페이스 
    - MEMORY 'memory_name'

> 오프라인 테이블스페이스의 파일은 삭제할 수 없다.   
> 테이블스페이스의 첫 번째 파일은 삭제할 수 없다.  
> 한 번이라도 사용된 적이 있는 데이터 파일은 삭제할 수 없다.

<a id="b45a23499ee10c13"></a>
#### &lt;domain name&gt;

구문을 수행하는 멤버 및 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="876c7fd61da119b8"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="b00805e5ab194cb7"></a>
### 사용 예

다음은 테이블스페이스의 파일을 제거하는 예이다.

```
gSQL> ALTER TABLESPACE space1 DROP DATAFILE 'test_file_f2.dbf';

Tablespace altered.
```

<a id="31b3b91ff94f81f6"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="9ede1e5241250f9b"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#e50680549a4cafe3)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#3e855076351fa5c9)
- [ALTER TABLESPACE name RENAME DATAFILE](#1e33e3f9ea894d62)

<a id="ecd840aaa27cb6b1"></a>
## ALTER TABLESPACE name [ONLINE|OFFLINE]

<a id="759833be5e920a44"></a>
### 기능

테이블스페이스 상태를 변경한다.

<a id="382e6d48b19fad6b"></a>
### 구문

```
<on/off tablespace statement> ::=
    ALTER TABLESPACE tablespace_name { ONLINE | OFFLINE [ NORMAL | IMMEIDATE ] }
    [ AT <domain name> ]
    ;
```

<a id="d939ce4360241f58"></a>
### 사용 범위 및 접근 권한

&lt;on/off tablespace statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="0e0a0847ea753e0c"></a>
### 구문 규칙 및 파라미터

<a id="cd1744de0f9673c1"></a>
#### ONLINE

OFFLINE 상태의 테이블스페이스를 ONLINE으로 변경한다.

<a id="8e5832c35ee1b4fd"></a>
#### OFFLINE NORMAL

ONLINE 상태의 테이블스페이스를 OFFLINE으로 변경한다.

OFFLINE으로 변경된 테이블스페이스는 일관된 (consistent) 상태이기 때문에 ONLINE 상태로 변경할 때 미디어 복구할 필요없다.

> MOUNT 단계에서는 OFFLINE NORMAL을 사용할 수 없다.   
> (단, 이전 인스턴스가 `\`SHUTDOWN NORMAL에 의해서 종료된 경우에는 가능하다.)

<a id="79763bcf3ce57724"></a>
#### OFFLINE IMMEDIATE

ONLINE 상태의 테이블스페이스를 OFFLINE으로 변경한다.

OFFLINE으로 변경된 테이블스페이스는 비일관적인 (inconsistent) 상태이기 때문에, ONLINE 상태로 변경할 때 미디어 복구해야 한다.

> SYSTEM 테이블스페이스는 OFFLINE으로 변경할 수 없다.   
> OFFLINE IMMEDIATE는 미디어 복구를 필요로 하기 때문에 archive log mode에서만 수행할 수 있다.

<a id="46ce8db4340ae286"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="42808eb752a69b17"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="b15fe8dd789504ac"></a>
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

<a id="3d125e271144d983"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="54995173d14b3286"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#e50680549a4cafe3)
- [ALTER TABLESPACE name BACKUP](#af7c53d2132a4178)

<a id="1e33e3f9ea894d62"></a>
## ALTER TABLESPACE name RENAME DATAFILE

<a id="22d97ba4b6f4f8e2"></a>
### 기능

테이블스페이스를 구성하는 데이터 파일의 이름을 변경한다.

<a id="21f9ed2188ef8a45"></a>
### 구문

```
<rename datafile statement> ::=
    ALTER TABLESPACE tablespace_name RENAME DATAFILE <filename_list> TO <filename_list>
    ;

    <filename_list> ::= 
        'filename' [ AT <domain name> ] [, ...]
```

<a id="2398a00807831b88"></a>
### 사용 범위 및 접근 권한

&lt;rename datafile statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

> TDS 모드이면서 데이터베이스가 OPEN인 상태에서는 온라인 테이블스페이스 파일을 변경할 수 없다. (임시 메모리 테이블스페이스는 제외된다.)   
> 변경한 후에도 파일은 반드시 존재해야 한다.

<a id="c2ef70c96a6b9ce8"></a>
### 구문 규칙 및 파라미터

<a id="2bfbf80931d1ef5a"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="75444f10f08b607f"></a>
#### 'filename'

메모리 임시 테이블스페이스는 'memory_name'을 의미하며, 그 외의 테이블스페이스 종류는 'filename'을 의미한다.

<a id="44672b3e0cd3ef50"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="2b59469905c17aed"></a>
### 설명

테이블스페이스 상태에 따라 연산 가능 여부가 결정된다.

- OFFLINE: MOUNT 단계나 OPEN 단계에서 수행 가능하다.
- ONLINE: MOUNT 단계에서만 수행 가능하다.

<a id="95cc2c5b4293e4c7"></a>
### 사용 예

다음은 'test.dbf'를 'test1.dbf'로 변경하는 예이다.

```
gSQL> ALTER TABLESPACE TEST_TBS RENAME DATAFILE 'test.dbf' TO 'test1.dbf';

Tablespace altered.
```

<a id="612b692287a8ddda"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="2b3476639673f71d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#e50680549a4cafe3)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#3e855076351fa5c9)
- [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#c4555abd12b44a7b)

<a id="34212132a1ef93f1"></a>
## ALTER TABLESPACE name RENAME TO

<a id="fdbc4cb752bc7c8f"></a>
### 기능

테이블스페이스의 이름을 변경한다.

<a id="9e0d0b7d7405a360"></a>
### 구문

```
<rename tablespace statement> ::=
    ALTER TABLESPACE tablespace_name RENAME TO <new_tablespace_name>
    ;
```

<a id="4576f27528991d81"></a>
### 사용 범위 및 접근 권한

&lt;rename space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="6787b1f895663dba"></a>
### 구문 규칙 및 파라미터

<a id="86318c2d1dd0bc72"></a>
#### tablespace_name

기존 테이블스페이스의 이름이다.

- Built-in 테이블스페이스의 이름은 변경할 수 없다.
- OFFLINE 테이블스페이스의 이름은 변경할 수 없다.

<a id="2b61c13ae806e2de"></a>
#### new_tablespace_name

새로운 테이블스페이스의 이름이다.

<a id="44799b437863bbca"></a>
### 설명

Tablespace 이름이 변경되더라도 기존에 이미 해당 tablespace에 생성된 table, index 등은 변경할 필요없다.

<a id="6cb2f47703d4ec85"></a>
### 사용 예

다음은 테이블스페이스의 이름을 변경하는 예이다.

```
gSQL> ALTER TABLESPACE space1 RENAME TO space2;

Tablespace altered.
```

<a id="82abb44585ef9aae"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="c10ab9f1597e23fd"></a>
### 참조

관련 내용은 [ALTER TABLESPACE](#e50680549a4cafe3)를 참조한다.

<a id="7fcf3795e062819a"></a>
## ALTER USER

<a id="fb63c1a3de198866"></a>
### 기능

데이터베이스 사용자 정의를 변경한다.

<a id="9cfbfaa3439b9b00"></a>
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

<a id="1b69ec733250da23"></a>
### 사용 범위 및 접근 권한

&lt;alter user statement&gt; 구문을 수행하려면 사용자에게 ALTER USER ON DATABASE 권한이 있어야 한다.  
단, &lt;alter password&gt;는 사용자가 user_identifier와 동일할 경우에 권한 없이 수행할 수 있다.

<a id="111d59c2ebec03d4"></a>
### 구문 규칙 및 파라미터

<a id="c229acfea86f10bd"></a>
#### user_identifier

변경할 사용자의 이름이다.

<a id="1be1bdf554ee0213"></a>
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

<a id="a368f0d7c136fd3e"></a>
#### &lt;alter profile&gt;

비밀번호 관리 정책을 위한 profile을 변경한다.

- PROFILE profile_name
    - 사용자가 생성한 profile_name을 할당한다.
- PROFILE DEFAULT
    - 기본 profile인 "DEFAULT"를 할당한다.
- PROFILE NULL
    - Profile을 할당하지 않는다.

<a id="b8ae1964f568a802"></a>
#### &lt;password expire&gt;

사용자의 비밀번호를 만료시킨다.

<a id="bd90d992d8298a78"></a>
#### &lt;account lock&gt;

- ACCOUNT LOCK
    - 사용자 계정을 잠근다. 
- ACCOUNT UNLOCK
    - 계정 잠금을 해제한다.

<a id="2198184f361c2cce"></a>
#### &lt;alter default tablespace&gt;

사용자의 기본 tablespace를 변경한다.   
tablespace_name은 data tablespace여야 한다.

<a id="8b3979ee75c69c13"></a>
#### &lt;alter temporary tablespace&gt;

사용자의 temporary tablespace를 변경한다.   
tablespace_name은 temporary tablespace여야 한다.

<a id="b55f3422e807dbd1"></a>
#### &lt;alter index tablespace&gt;

사용자의 index tablespace를 변경한다.

- INDEX TABLESPACE tablespace_name을 지정한다.
    - Data tablespace를 지정한 경우, LOGGING 인덱스가 된다.
    - Temporary tablespace를 지정한 경우, NOLOGGING 인덱스가 된다.
- INDEX TABLESPACE NULL
    - Index tablespace를 지정하지 않는다.

<a id="e8c219f0dfe536c4"></a>
#### &lt;alter schema path&gt;

사용자의 스키마 접근 경로를 변경한다.   
사용자의 SQL 구문에 schema가 명시되지 않았을 경우 스키마 접근 경로는 객체의 naming resolution을 위한 스키마 순서에 따라 결정된다.

스키마 이름이 기존에 스키마 접근 경로에 나열된 스키마 이름과 동일할 경우에는 추가적으로 반영되지 않는다.

다음은 *ALTER USER u1 SCHEMA PATH ( u1, s2, public );* 구문을 수행했을 때 schema에 존재하는 객체의 예이다.

<a id="0aeeb5734b11e242"></a>
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

<a id="0c5fde78cdf7f035"></a>
#### CURRENT PATH

현재 사용자의 schema path 이다.

다음 예와 같이 CURRENT PATH를 이용해 기존의 schema path를 유지하면서 새로운 schema path를 추가할 수 있다.

- u1의 현재 schema path 
    - (u1, public) 
- 구문 수행 
    - ALTER USER u1 SCHEMA PATH ( s1, CURRENT PATH, s2 ); 
- u1의 schema path는 다음과 같이 변경된다. 
    - (s1, u1, public, s2)

<a id="dc4196565564a761"></a>
#### ALTER USER PUBLIC &lt;alter schema path&gt;

PUBLIC 계정의 schema path를 변경한다.   
PUBLIC 계정의 schema path는 모든 사용자의 schema path에 포함된다.

PUBLIC 계정에 최초로 부여된 schema path는 다음과 같다.

- DICTIONARY_SCHEMA 
- INFORMATION_SCHEMA 
- DEFINITION_SCHEMA 
- PERFORMANCE_VIEW_SCHEMA 
- FIXED_TABLE_SCHEMA

<a id="901db284580146e3"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="63afdc91dcbaada3"></a>
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

<a id="7c08edcc4cb5d370"></a>
### 호환성

SQL 표준에서 user의 개념은 다루고 있지만 user의 생성, 변경 및 삭제와 관련된 SQL 구문은 정의하지 않고 있다.

<a id="3ad8b12f6ce918a2"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE USER](19-sql-references-c-g.md#bcf4364429be6a9b)
- [DROP USER](19-sql-references-c-g.md#c4934ee399839206)

<a id="f911f10e438cdcf6"></a>
## ALTER VIEW

<a id="2507341afc91dd9f"></a>
### 기능

View 정의를 변경한다.

<a id="505d48f40a7df260"></a>
### 구문

```
<alter view statement> ::=
    ALTER VIEW view_name <alter view action>
    ;

<alter view action> ::=
    COMPILE
```

<a id="be3709d8946b75f0"></a>
### 사용 범위 및 접근 권한

&lt;alter view statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 view에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- View가 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="d6df9122f3fde7ed"></a>
### 구문 규칙 및 파라미터

<a id="9b9c2e6c701236c2"></a>
#### view_name

변경할 view의 이름이다.  
schema_name.view_name과 같이 view가 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="ade032bd70ae7783"></a>
#### COMPILE

View를 다시 컴파일한다.   
View column에 부여한 COMMENT는 초기화된다.

<a id="a339c3b2d126b92b"></a>
### 설명

View가 참조하는 테이블이나 view가 변경되거나 삭제되면 해당 view도 영향을 받는다.

이런 정보는 INFORMATION_SCHEMA.VIEWS를 통해 조회할 수 있다.

- IS_COMPILED column
    - TRUE: View가 정상적으로 생성되었다.
    - FALSE: 에러가 존재하는 상태에서 FORCE 옵션으로 view가 생성되었다.

- IS_AFFECTED column
    - TRUE : View가 참조하는 테이블 또는 view가 변경되었다.
    - FALSE: View가 생성되고 COMPILE 된 후에 view가 참조하는 테이블이나 view가 변경되지 않았다.

<a id="ac40c464de99ef13"></a>
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

<a id="770441becc082223"></a>
### 호환성

SQL 표준에서는 &lt;alter view statement&gt; 구문을 정의하지 않고 있다.

<a id="826ba145c59b5886"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE VIEW](19-sql-references-c-g.md#6f697c93c59acd84)
- [DROP VIEW](19-sql-references-c-g.md#7271de5cbf690942)

<a id="0c76eff97ad44993"></a>
## ANALYZE SYSTEM

<a id="6b263dbc78b1067c"></a>
### 기능

시스템의 통계 정보를 제어한다.

<a id="97870e61fce2e5e7"></a>
### 구문

```
<analyze system statement> ::=
    ANALYZE SYSTEM [ <analyze action> ]
    ;

<analyze action> ::=
      COMPUTE STATISTICS
    | DELETE STATISTICS
```

<a id="c11c146b60878636"></a>
### 사용 범위 및 접근 권한

&lt;analyze system statement&gt; 구문을 수행하려면 사용자에게 ANALYZE ANY ON DATABASE 권한이 있어야 한다.

<a id="8a2eebb9b5dea65c"></a>
### 구문 규칙 및 파라미터

<a id="66ad61f845cfef5d"></a>
#### &lt;analyze action&gt;

생략할 경우 기본값은 COMPUTE STATISTICS 이다.

<a id="23f05a5a93f0978f"></a>
#### COMPUTE STATISTICS

시스템과 관련된 다음과 같은 통계 정보를 구축한다.

- CPU_OPS (Operations Per Second) 
    - CPU가 초당 처리할 수 있는 operation의 개수이다.

- NETWORK_IOPS (IO operations Per Second) 
    - Cluster인 경우에 유효하다. 
    - 초당 처리할 수 있는 network IO 횟수이다.

- BUFFER_MISS_PERCENT
    - 디스크 buffer miss 확률

<a id="2aa1b02386bbc718"></a>
#### DELETE STATISTICS

시스템 통계 정보를 삭제한다.

<a id="dae9cc4ce04f2b6f"></a>
### 설명

구축한 시스템 통계 정보는 질의 처리를 위한 최적화 과정의 비용을 계산하기 위해 사용한다.

<a id="7fcb8a1c043f8960"></a>
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

<a id="b16478be76412ee4"></a>
### 호환성

SQL 표준에서는 통계 정보에 대한 개념을 정의하지 않고 있다.

<a id="0ba319d672f6481d"></a>
### 참조

관련 내용은 [ANALYZE TABLE](#1513e1fe777d56bb)을 참조한다.

<a id="1513e1fe777d56bb"></a>
## ANALYZE TABLE

<a id="3f87eeb5a3a52966"></a>
### 기능

테이블의 통계 정보를 제어한다.

<a id="c43057e4665395b5"></a>
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

<a id="8c2ccfc527eb4db5"></a>
### 사용 범위 및 접근 권한

&lt;analyze table statement&gt; 구문을 수행하려면 사용자에게 ANALYZE ANY ON DATABASE 권한이 있어야 한다.

<a id="d4e80647e389dc63"></a>
### 구문 규칙 및 파라미터

<a id="fb99470cede700cd"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="8a6c9b5a0dcf079e"></a>
#### &lt;parallel clause&gt;

분석 과정에서 사용할 thread 개수를 지정한다.   
명시하지 않을 경우, 기본값은 PARALLEL 이다.

- NOPARALLEL
    - 병렬로 분석하지 않는다.

- PARALLEL [thread_count]
    - 병렬로 분석한다.
    - thread_count 값은 0 부터 사용할 수 있으며 최대값은 64 이다.
    - thread_count 값이 0이거나 생략된 경우 시스템의 CPU 개수에 의해 결정된다.

<a id="9476b9cb98205cf8"></a>
#### &lt;analyze action&gt;

생략할 경우 기본값은 COMPUTE STATISTICS 이다.

<a id="7df896f6d558b50a"></a>
#### COMPUTE STATISTICS

전수 검사를 통해 테이블과 관련된 다음과 같은 통계 정보를 구축한다.

- Table 통계정보 
    - Row count
    - Page 개수 
- 각 column의 통계 정보 
    - 서로 다른 값의 개수 
    - NULL 값의 개수 
    - 값의 평균 길이 
    - 최소값 
    - 최대값 
- Index 통계정보 
    - 서로 다른 key의 개수
    - Page 개수
    - Leaf page 개수
    - Tree level
    - 인덱스 군집도 (clustering factor)

Column의 data type에 따라 구축하는 통계 정보는 다음과 같다.

**Data type에 따라 구축된 통계 정보**

<a id="f6557572a6714aa8"></a>
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

<a id="179495e33b22a663"></a>
#### ESTIMATE STATISTICS &lt;sample_clause&gt;

지정한 &lt;sample_clause&gt;만큼의 샘플을 사용하여 column과 index의 통계 정보를 구축한다.

- SAMPLE row_count ROWS 
    - 지정한 row 개수만큼 샘플을 사용한다. 
    - row_count는 0보다 큰 양의 정수이다. 
- SAMPLE percentage PERCENT 
    - 지정한 비율만큼 샘플을 사용한다. 
    - Percentage는 1 ~ 99 범위의 양의 정수이다.

샘플링 row의 개수가 [MIN_SAMPLE_ROW_COUNT](../part-02-administration-manual/10-server-property.md#257deba70585568a) 프로퍼티 값보다 작을 경우 프로퍼티 값을 따른다.

<a id="ab71817f2852824b"></a>
#### &lt;for_clause&gt;

생략할 경우, 통계정보 구축이 가능한 모든 column과 모든 인덱스의 통계 정보를 구축한다.

<a id="354297eafb055e86"></a>
#### FOR ALL COLUMNS

통계 정보 구축이 가능한 모든 column의 통계 정보를 구축한다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="3fab3aae4a5bcbc6"></a>
#### FOR ALL INDEXED COLUMNS

인덱스에 포함된 모든 column의 통계 정보를 구축한다.   
그 외 column의 통계 정보는 구축하지 않는다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="01f4aee2eb9e74b8"></a>
#### FOR COLUMNS column_name [, ...]

나열한 column의 통계 정보를 구축한다.   
기술하지 않은 column의 통계 정보는 구축하지 않는다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="a6b4333a160482ac"></a>
#### FOR ALL INDEXES

모든 인덱스의 통계 정보를 구축한다.   
Column 통계 정보는 구축하지 않는다.

<a id="ea5f1b97496042f7"></a>
#### FOR INDEXES index_name [, ...]

나열한 인덱스의 통계 정보를 구축한다.   
기술하지 않은 인덱스의 통계 정보는 구축하지 않는다.   
Column 통계 정보는 구축하지 않는다.

<a id="8bf494944fbbd780"></a>
#### DELETE STATISTICS

테이블의 통계 정보를 제거한다.

<a id="690c8b3452d4926e"></a>
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

<a id="475711658c64af91"></a>
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

<a id="a13fff8641e3e50b"></a>
### 호환성

SQL 표준에서는 통계 정보에 대한 개념을 정의하지 않고 있다.

<a id="95c39e41e2e8c13a"></a>
### 참조

관련 내용은 [ANALYZE SYSTEM](#0c76eff97ad44993)을 참조한다.

<a id="bdecea76b1665d44"></a>
## AUDIT POLICY

<a id="0277413865a0afc9"></a>
### 기능

Audit policy를 활성화한다.

<a id="e409ac98f46ca605"></a>
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

<a id="737de7a358d7b9a1"></a>
### 사용 범위 및 접근 권한

&lt;audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="d6c84107ce23261e"></a>
### 구문 규칙 및 파라미터

<a id="52fcc7bcf04c3b9e"></a>
#### policy_name

활성화할 audit policy 객체의 이름이다.   
활성화 된 audit policy는 기존 session에 영향을 미치지 않으며 새로 생성되는 session에만 영향을 준다.

<a id="85063f7374cbe3b6"></a>
#### &lt;specified_user_option&gt;

감사를 수행할 사용자를 명시한다.     
생략할 경우 모든 사용자에 대해 감사를 수행한다.

동일한 audit policy에 대해 BY 절과 EXCEPT 절을 함께 사용할 수 없다.

- BY user_list: 감사를 수행할 사용자를 특정할 경우 BY 절을 사용한다.
- EXCEPT user_list: 특정 사용자를 배제하고 다른 사용자들을 감사할 경우 EXCEPT 절을 사용한다.

<a id="2260ee226eef9534"></a>
#### &lt;specified_success_option&gt;

- WHENEVER SUCCESSFUL
    - Action이 성공했을 때 audit record가 생성된다.
- WHENEVER NOT SUCCESSFUL
    - Action이 실패했을 때 audit record가 생성된다.
- 생략할 경우 성공할 경우와 실패할 경우 모두 audit record를 생성한다.

<a id="3d2b00389d08365f"></a>
### 설명

Audit policy를 활성화하면 기존 session에는 영향을 미치지 않으며 새로 생성되는 session에 대해 감사를 시작한다.

<a id="21fad286132906db"></a>
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

<a id="52643fa919340006"></a>
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

<a id="6a32a6b56ae97791"></a>
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

<a id="efb7a5b68e30827a"></a>
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

<a id="d1e1c736dfb5326b"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="970264c67fb5afbc"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](19-sql-references-c-g.md#ab7ff9504e3f6183)
    - [DROP AUDIT POLICY](19-sql-references-c-g.md#69253535ad827e04)
    - [ALTER AUDIT POLICY](#ecf2c4bd73416b17)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#bdecea76b1665d44)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#f63dd37e5a743f09)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#0f5f6dd722f4b648)

- Audit trail 소거: [ALTER DATABASE CLEAR AUDIT TRAIL](#7cfd4bf205511a5c)

---

[← 17. Built-in Function References](17-built-in-function-references.md) · [전체 목차](../README.md) · [19. SQL References (C~G) →](19-sql-references-c-g.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
