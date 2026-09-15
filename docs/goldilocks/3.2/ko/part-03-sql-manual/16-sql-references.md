<a id="e2e6df00f51b29a6"></a>

# 16. SQL References

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/e2e6df00f51b29a6)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 15. SQL Tuning](15-sql-tuning.md) · [전체 목차](../README.md) · [17. Overview of PSM →](../part-04-psm-manual/17-overview-of-psm.md)

<a id="2cfef6a9826bdadf"></a>
## ALTER AUDIT POLICY

<a id="dd3240651fbc0e78"></a>
### 기능

Audit policy 객체에 감사 대상을 추가하거나 삭제한다.

<a id="2b0868171976574d"></a>
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

<a id="aa1aa352b30c933c"></a>
### 사용 범위 및 접근 권한

&lt;alter audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="2b4bb84d8b7bdc8e"></a>
### 구문 규칙 및 파라미터

<a id="f61dc1cecc99986f"></a>
#### policy_name

변경할 audit policy 객체의 이름이다.

<a id="051c03c412f48d66"></a>
#### &lt;add_audit_option&gt;

Audit policy에 감사대상을 추가한다.

<a id="de125976f6881c7f"></a>
#### &lt;drop_audit_option&gt;

Audit policy 감사대상에서 삭제한다.

<a id="47343e04a7c30900"></a>
#### &lt;privilege_audit_clause&gt;

자세한 내용은 [CREATE AUDIT POLICY](#676233f209f722e4) 를 참조한다.

<a id="11b9df1a163ca096"></a>
#### &lt;action_audit_clause&gt;

자세한 내용은 [CREATE AUDIT POLICY](#676233f209f722e4) 를 참조한다.

<a id="e9969e077ec05f88"></a>
### 설명

이미 활성화된 audit policy를 변경할 수 있지만 기존 session에는 영향을 주지 않고 새로 생성되는 session에만 영향을 미친다.

> 다음과 같이 ALL 옵션을 DROP 할 경우, 모든 action이 삭제되는 것이 아니라 해당 ALL 옵션만 삭제된다.

```
CREATE AUDIT POLICY p1
       ACTIONS ALL ON u1.t1,
               SELECT ON u1.t1;

ALTER AUDIT POLICY p1 DROP
      ACTIONS ALL ON u1.t1;
```

<a id="c3da2308611c16d4"></a>
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

<a id="e5f86ff169ef31e5"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="25d03bcc65565410"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#676233f209f722e4)
    - [DROP AUDIT POLICY](#c1e1a11e6ac9443a)
    - [ALTER AUDIT POLICY](#2cfef6a9826bdadf)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#c789ab5113d50e70)
    - [NOAUDIT POLICY](#2953451ac097af0c)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#2eb922e8e06a1b57)

- Audit trail 삭제: [ALTER DATABASE CLEAR AUDIT TRAIL](#016c886b7cddf620)

<a id="3d7884550455c0c5"></a>
## ALTER CLUSTER GROUP name ADD MEMBER

<a id="ced6c3d4663bf760"></a>
### 기능

Cluster group에 cluster member를 추가한다.

<a id="48ab09b4e9c6e849"></a>
### 구문

```
<alter cluster group add member statement> ::=
    ALTER CLUSTER GROUP group_name ADD
        <cluster member definition> [, ...]
    ;

<cluster member definition> ::=
    CLUSTER MEMBER member_name <connection attribute>

<connection attribute> ::
    HOST 'address' PORT port_no
```

<a id="fe9ecb1857dce63e"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster group add member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="15cc649bbb6dd087"></a>
### 구문 규칙 및 파라미터

<a id="413d2af717422fb3"></a>
#### group_name

Cluster group의 이름이다.

<a id="fc0e8c2e07ea8a0e"></a>
#### &lt;cluster member definition&gt;

Cluster group에 포함될 cluster member를 정의한다.  
Cluster group은 최대 32 개의 cluster member를 포함할 수 있다.

<a id="81a4351a4077eb62"></a>
#### member_name

Cluster member의 이름이다.  
Cluster member의 이름은 해당 member의 database를 생성할 때 정의한 member의 이름과 동일해야 한다.  
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.  
이름의 길이가 128 바이트보다 작아야 한다.  
Cluster member의 start-up 단계가 OPEN이어야 한다.

<a id="2f47c6f7384b06b3"></a>
#### &lt;connection attribute&gt;

Cluster member간 통신을 위한 연결 정보를 정의한다.  
&lt;connection attribute&gt;는 해당 member의 database를 생성할 때 정의한 HOST, PORT와 동일해야 한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 ip v4 형식을 사용한다. 
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="d0b2b5981661533d"></a>
### 설명

&lt;alter cluster group add member statement&gt; 구문은 table들의 shard를 재배치하지 않는다.  
추가된 cluster member에 shard를 재배치하려면 다음 구문을 수행해야 한다.

- [ALTER DATABASE REBALANCE](#092cbc6985d152fb)
- [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef)

<a id="fc2f29eb68fe5236"></a>
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

<a id="a733b823f9f24b64"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="f30673be7df6c34a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER GROUP](#609ea3458a43136d)
- [DROP CLUSTER GROUP](#d185e21cb13f6ec6)
- [ALTER DATABASE REBALANCE](#092cbc6985d152fb)
- [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef)

<a id="0465132bd7a76761"></a>
## ALTER CLUSTER GROUP name OFFLINE MEMBER

<a id="7613fec15f73da81"></a>
### 기능

Cluster group의 cluster member를 offline 상태로 변경한다.

<a id="dff084ff0fa9d44d"></a>
### 구문

```
<alter cluster group offline member statement> ::=
    ALTER CLUSTER GROUP group_name OFFLINE
        <cluster member definition>
    ;

<cluster member definition> ::=
    CLUSTER MEMBER member_name
    ;
```

<a id="1f67e9382e6dc0dc"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster group offline member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="652668c001a0a489"></a>
### 구문 규칙 및 파라미터

<a id="d45921415eca3fda"></a>
#### group_name

Cluster group의 이름이다.

<a id="f3988edc5241fec0"></a>
#### &lt;cluster member definition&gt;

Cluster group에 포함될 cluster member를 정의한다.  
Cluster group은 최대 32개의 cluster member를 포함할 수 있다.

<a id="b70c210d4a95d3ca"></a>
#### member_name

Cluster member의 이름이다.  
Cluster member의 이름은 해당 member의 database를 생성할 때 정의한 member의 이름과 동일해야 한다.  
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.  
이름의 길이가 128 바이트보다 작아야 한다.  
Cluster member의 start-up 단계가 OPEN이어야 한다.

<a id="f774d0b533910114"></a>
### 설명

&lt;alter cluster group offline member statement&gt; 구문은 table들의 shard를 재배치하지 않는다.

<a id="1af8c49e4c0ab4ac"></a>
### 사용 예

다음은 특정 cluster member를 offline 상태로 변경하는 예이다.

```
gSQL>

ALTER CLUSTER GROUP g1 OFFLINE
    CLUSTER MEMBER g1n3
;
Cluster Group altered.
```

<a id="793761046bd57393"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="fc511214c0eb47da"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER GROUP](#609ea3458a43136d)
- [DROP CLUSTER GROUP](#d185e21cb13f6ec6)
- [ALTER DATABASE REBALANCE](#092cbc6985d152fb)
- [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef)

<a id="b088884e1c158484"></a>
## ALTER CLUSTER LOCATION

<a id="bd21caed0d4ddeee"></a>
### 기능

Cluster location 정보를 수정한다.

<a id="9b2ef85ab162269a"></a>
### 구문

```
<alter cluster location statement> ::=
    ALTER CLUSTER LOCATION member_name 
    <cluster connection attribute>
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="7b3b57233d2b8c64"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster location statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="014296822b214aca"></a>
### 구문 규칙 및 파라미터

<a id="bc07c51e98c8f141"></a>
#### member_name

Cluster member의 이름이다.  
등록된 cluster location 정보에 동일한 cluster member 이름이 존재해야 한다.  
이름의 길이가 128 바이트보다 작아야 한다.

<a id="7ea2da812e5796db"></a>
#### &lt;cluster connection attribute&gt;

Cluster member 간 통신을 위한 연결 정보를 정의한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 ip v4 형식으로 사용한다. 
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="e4d8fd5eafa75995"></a>
### 설명

만약 cluster location의 접속 정보가 변경될 경우에는 cluster member를 제거하거나 재생성할 필요없이 [ALTER CLUSTER LOCATION](#b088884e1c158484)을 이용하여 접속 정보를 변경할 수 있다.

<a id="441515af7e465cce"></a>
### 사용 예

```
gSQL> 
ALTER CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120,
;

Created
```

<a id="f88185b8fa4d504c"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="8c69498e5e9bcef7"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER LOCATION](#60d111e8979eff2d)
- [DROP CLUSTER LOCATION](#f2273de5f0bd9109)

<a id="4877f17dc24787bd"></a>
## ALTER DATABASE ADD LOGFILE

<a id="a64ec64603df9fac"></a>
### 기능

데이터베이스에 로그파일 그룹 또는 로그파일 멤버를 추가한다.

<a id="9bfd6283c6088cb4"></a>
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

<a id="fcc0c901deb89c20"></a>
### 사용 범위 및 접근 권한

&lt;alter database add logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="94dcba608b0532e0"></a>
### 구문 규칙 및 파라미터

<a id="d208bd81d48e2aaf"></a>
#### &lt;alter database add logfile statement&gt;

데이터베이스는 MOUNT 상태여야 한다.

<a id="0426845e05223b56"></a>
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

<a id="c5692c5010aa453f"></a>
#### &lt;add logfile group statement&gt;

새로운 로그파일 그룹을 추가한다.

- CURRENT 로그파일 그룹의 다음 그룹으로 추가된다.
- &lt;group clause&gt; 
    - 데이터베이스에 추가할 로그파일 그룹의 식별자를 지정한다.
    - integer는 존재하지 않는 로그파일 그룹 식별자여야 한다.
    - integer에 해당하는 식별자가 존재할 경우 에러가 발생한다. 
- &lt;size clause&gt; 
    - 파일의 크기는 최소 10 MB ~ 최대 10 GB까지 지정할 수 있다.
    - 파일의 크기는 로그 버퍼 (redo log buffer)의 크기와 지연 로그 버퍼 (pending log buffer) 크기의 합보다 커야 한다.
- 만약 logfile_name이 이미 존재하고 REUSE 옵션을 사용한 경우, 로그 파일 그룹 내의 다른 멤버와 크기가 동일하다면 기존 로그파일을 재사용한다.

<a id="e41e63b54e56e867"></a>
### 설명

새로운 로그파일 그룹과 로그 멤버가 추가되는 경우 controlfile에 저장되므로 향후 controlfile 손상에 대비해 controlfile을 백업하는 것을 권장한다.

<a id="2e80ca0fa1b448b4"></a>
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

<a id="03cd4d3711543a7d"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="eaf8a755a7e31556"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#4877f17dc24787bd)
- [ALTER DATABASE DROP LOGFILE](#c03c2f215d3df668)
- [ALTER DATABASE RENAME LOGFILE](#9baf0d73d32ecb14)

<a id="28784043d5f6199c"></a>
## ALTER DATABASE ARCHIVELOG

<a id="01f1d950a075ee65"></a>
### 기능

데이터베이스의 온라인 로그 파일 archive 설정을 변경한다.

<a id="210ecd4ab95a4a86"></a>
### 구문

```
<alter database archivelog statement> ::=
    ALTER DATABASE { ARCHIVELOG | NOARCHIVELOG }
    ;
```

<a id="aa482866c9e2d33b"></a>
### 사용 범위 및 접근 권한

&lt;alter database archivelog statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="78bc408318cb5e01"></a>
### 구문 규칙 및 파라미터

<a id="5db9c8d06a72f1cc"></a>
#### &lt;alter database archivelog statement&gt;

- 데이터베이스가 MOUNT 상태여야 한다.
- ARCHIVELOG
    - 온라인 로그파일을 archive 한다.
- NOARCHIVELOG
    - 온라인 로그파일을 archive 하지 않는다.

<a id="ef8616c211abd98e"></a>
### 설명

Database를 백업하고 백업을 이용해 복구 (media recovery)하려면 시스템이 ARCHIVELOG 모드로 운용되어야 한다.

<a id="077dca0d4f21dabb"></a>
### 사용 예

다음은 데이터베이스를 archive 모드로 설정하는 예이다.

```
ALTER DATABASE ARCHIVELOG;
```

<a id="a4a7a4d0b36aa2e6"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="5cdd0c345c1cc230"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#65c7e2f31a8e4d5f)
- [ALTER TABLESPACE name BACKUP](#bffdd0e4b8821918)

<a id="65c7e2f31a8e4d5f"></a>
## ALTER DATABASE BACKUP

<a id="598a56f21c9277ca"></a>
### 기능

데이터베이스 전체 백업 (full backup)을 수행하기 위해 백업 상태를 'ACTIVE' 또는 'INACTIVE'로 설정한다. 그리고 데이터베이스 증분 백업 (incremental backup)과 제어 파일 (control file) 백업을 수행한다.

<a id="30cea996ef77f6e7"></a>
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

<a id="3ac72176dd0f5fdd"></a>
### 사용 범위 및 접근 권한

&lt;alter database backup statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="522493639ac00212"></a>
### 구문 규칙 및 파라미터

<a id="9648261df736f16b"></a>
#### &lt;database begin backup clause&gt;

데이터베이스를 전체 백업이 가능한 상태로 설정한다.

- 데이터베이스에서 생성되어 사용 중인 ONLINE 상태의 모든 테이블스페이스를 전체 백업이 가능한 상태로 설정한다. 
- 데이터베이스는 OPEN 상태여야 하고 ARCHIVELOG 모드로 운영되어야 한다.
- BEGIN BACKUP이 시작된 이후에는 다음과 같이 데이터 파일에 쓰기를 요구하는 연산들은 수행할 수 없다.
    - SHUTDOWN NORMAL
    - OFFLINE/ DROP TABLESPACE
    - ADD/ DROP DATAFILE
- 전체 백업의 상태가 ACTIVE인 상태에서 인스턴스가 비정상 종료될 경우, 다시 시작할 때 미디어 복구를 요구할 수도 있다.

<a id="1b6c38f19249433b"></a>
#### &lt;database end backup clause&gt;

데이터베이스를 전체 백업 불가능한 상태로 설정한다.

- 데이터베이스에서 생성되어 사용 중인 ONLINE 상태의 모든 테이블스페이스를 백업 불가능한 상태로 설정한다.
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG 모드로 운영되어야 한다.

<a id="e96d0014cc5b2837"></a>
#### &lt;database incremental backup statement&gt;

- 데이터베이스 증분 백업을 수행한다.
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG로 운영되어야 한다.

<a id="3814a2fc863643b6"></a>
#### &lt;incremental backup option&gt;

- 'integer'는 0 ~ 4 까지 지정할 수 있다.
- LEVEL 0은 CUMULATIVE나 DIFFERENTIAL을 지정할 수 없다.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - 'integer'가 n이면 가장 최근에 LEVEL 0 ~ LEVEL n-1까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - DIFFERENTIAL
        - 'integer'가 n이면 가장 최근에 LEVEL 0 ~ LEVEL n까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - 생략하면 DIFFERENTIAL이 기본으로 지정된다.

<a id="44902791b0e7ef15"></a>
#### &lt;database controlfile backup statement&gt;

- 제어 파일 (controlfile)을 백업한다.
    - 'target_name'의 이름은 1024 바이트보다 작아야 한다. 
    - 'target_name'이 이미 존재하는 경우 연산에 실패한다. 
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG로 운영되고 있어야 한다.

> GOLDILOCKS에서 관리하는 'target_name' 길이는 최대 1024 바이트이지만, OS마다 최대로 허용하는 파일 이름 길이가 다르기 때문에, 실제 생성가능한 'target_name'의 길이는 1024 바이트보다 작을 수 있다.

<a id="b468511b08f403d0"></a>
#### &lt;domain name&gt;

- 구문을 수행할 멤버나 그룹의 이름이다.
- 지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="befd21dbd418a361"></a>
### 설명

Database의 datafile과 controlfile을 백업한다. BEGIN BACKUP을 수행한 후 OS의 파일 복사로 datafile들을 복사하고 나서 END BACKUP을 수행하여 database를 전체 백업한다. 한편, 증분 백업 파일은 하나의 구문으로 BACKUP_DIR_1 property에 설정된 경로에 생성한다.

<a id="bd5c849aa259f4e8"></a>
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

<a id="4b29ec2d2a6bdef0"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="aea1fc6650a5f822"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#bffdd0e4b8821918)
- [ALTER DATABASE RECOVER](#e877de8414d4d237)

<a id="016c886b7cddf620"></a>
## ALTER DATABASE CLEAR AUDIT TRAIL

<a id="85a84d0af476e31f"></a>
### 기능

Audit policy 적용으로 인해 누적된 audit record를 삭제 (purge)한다.

<a id="a1bd5f1039f58145"></a>
### 구문

```
<clear audit trail statement> ::= 
    ALTER DATABASE CLEAR AUDIT TRAIL
;
```

<a id="6ac5049201aaba4c"></a>
### 사용 범위 및 접근 권한

&lt;clear audit trail statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="192edeaf3686a40e"></a>
### 설명

Audit policy를 활성화하면 시간이 지남에 따라 audit trail이 계속 커진다.   
Audit trail을 구성하는 테이블들은 MEM_AUX_TBS 테이블스페이스에 저장되는데 audit trail이 계속 커지지 않도록 해야 한다.

<a id="1bc605fa63cddcdc"></a>
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

<a id="4f21e77692697027"></a>
### 사용 예

다음 구문을 사용하여 audit trail을 삭제 (purge)한다.

```
ALTER DATABASE CLEAR AUDIT TRAIL;
```

<a id="7c0b7b3637a1fc82"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="6013b077fe9e8ef5"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#676233f209f722e4)
    - [DROP AUDIT POLICY](#c1e1a11e6ac9443a)
    - [ALTER AUDIT POLICY](#2cfef6a9826bdadf)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#c789ab5113d50e70)
    - [NOAUDIT POLICY](#2953451ac097af0c)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#2eb922e8e06a1b57)

- Audit trail 삭제:[ALTER DATABASE CLEAR AUDIT TRAIL](#016c886b7cddf620)

<a id="028c9fbaca0d67cf"></a>
## ALTER DATABASE CLEAR PASSWORD HISTORY

<a id="8bfbfa2ef544a9a5"></a>
### 기능

Profile 적용에 따라 누적된 사용자의 비밀번호 변경 이력을 삭제한다.

<a id="9ba29bc81942da56"></a>
### 구문

```
<clear password history statement> ::= 
    ALTER DATABASE CLEAR PASSWORD HISTORY
    ;
```

<a id="70b733032391b428"></a>
### 사용 범위 및 접근 권한

&lt;clear password history statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="5125bf5eb3fdad29"></a>
### 설명

User에 profile을 적용할 때 PASSWORD_REUSE_MAX, PASSWORD_REUSE_TIME의 정책에 따라 사용자의 비밀번호 변경이력이 누적된다.

**변경 이력 관리**

<a id="57f71be295395926"></a>
| PASSWORD_REUSE_MAX | PASSWORD_REUSE_TIME | 변경 이력 관리 |
| --- | --- | --- |
| value | value | Value 범위 내의 변경 이력만 관리하고 범위를 벗어난 변경 이력은 자동으로 삭제한다. |
| value | UNLIMITED | 모든 변경 이력을 검사해야 하므로 변경 이력을 누적할 뿐 제거하지 않는다. |
| UNLIMITED | value | 모든 변경 이력을 검사해야 하므로 변경 이력을 누적할 뿐 제거하지 않는다. |
| UNLIMITED | UNLIMITED | 변경 이력을 검사하지 않으므로 관리도 하지 않는다. |

&lt;clear password history statement&gt; 구문은 누적된 사용자 비밀번호 변경 이력을 삭제한다.

<a id="77dedb7811354773"></a>
### 사용 예

다음은 &lt;clear password history statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE CLEAR PASSWORD HISTORY;

Database altered.

gSQL> COMMIT;

Commit complete.
```

<a id="684ff6c5d0ef9dbc"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="d1caf4a00413987c"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE PROFILE](#208fdfbd422ca37d)
- [CREATE USER](#339657c579ea782f)

<a id="b373416203b1404a"></a>
## ALTER DATABASE DELETE BACKUP

<a id="61683525e9957fa2"></a>
### 기능

증분 백업 (incremental backup)의 백업 정보와 백업 파일을 삭제한다. Database의 모든 증분 백업을 삭제하거나, 더 이상 쓸모 없는 백업 (obsolete backup)을 선택해서 삭제할 수 있다.

<a id="7f38562020222b26"></a>
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

<a id="0addf7256f438ef5"></a>
### 사용 범위 및 접근 권한

&lt;alter database delete backup statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="f371076cc464db6e"></a>
### 구문 규칙 및 파라미터

<a id="c3fdaff3d9232cd1"></a>
#### &lt;alter database delete backup statement&gt;

데이터베이스가 MOUNT 또는 OPEN 상태여야 한다.

<a id="03799ee64dd2c37e"></a>
#### &lt;delete backup list option&gt;

기존 증분 백업들 중에서 삭제할 대상을 선정한다.

- OBSOLETE: 가장 최근의 데이터베이스 'LEVEL 0' 백업 이전에 백업한 데이터베이스 또는 테이블스페이스 백업본들을 삭제 대상으로 선정한다.
- ALL: 전체 증분 백업들을 삭제 대상으로 선정한다.

<a id="803ff6a43a26858a"></a>
#### &lt;including backup file option&gt;

- 생략하면 백업 정보만 제어 파일에서 삭제한다.
- 백업 정보뿐만 아니라 백업 파일들도 함께 삭제한다.

<a id="fb9a69347f5d885c"></a>
### 설명

OBSOLETE 증분 백업 삭제는 가장 최근의 LEVEL 0 데이터베이스 백업 이전의 증분 백업을 삭제한다. 즉, LEVEL 0이 아닌 증분 백업을 수행할 때는 이전에 수행한 증분 백업을 포함하는 증분 백업이 있더라도 삭제하지 않는다. 왜냐하면 증분 백업을 이용한 불완전 복구를 수행할 때 사용될 수 있기 때문이다.

> 증분 백업을 삭제할 때 백업 파일까지 함께 삭제하면 증분 백업 정보를 포함하는 백업된 controlfile을 이용하더라도 복구를 수행할 수 없으므로 주의해야 한다.

<a id="3bb13ba234bbce31"></a>
### 사용 예

다음은 기존 모든 증분 백업들의 백업정보와 백업파일들을 삭제하는 예이다.

```
ALTER DATABASE DELETE ALL BACKUP LIST INCLUING BACKUP FILES;
```

<a id="6a3de15a9338a4fd"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="c8f6ca22792843c7"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#bffdd0e4b8821918)
- [ALTER DATABASE RECOVER](#e877de8414d4d237)

<a id="05f1c6bb77934e8a"></a>
## ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS

<a id="d7d785839752c0f7"></a>
### 기능

모든 inactive cluster member들을 제거한다.

<a id="4ca7cbc39a5ccdb1"></a>
### 구문

```
<alter database drop inactive members statement> ::=
    ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS
    ;
```

<a id="24e264e5769d1d99"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database drop inactive cluster members statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="f63c85b6fb8187c1"></a>
### 설명

모든 inactive cluster member들을 제거한다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우 
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

단, cluster member를 제거할 때 table의 shard가 유실되는 경우에는 inactive cluster member를 제거할 수 없다.

&lt;alter database drop inactive members statement&gt; 구문은 모든 inactive cluster member들이 더 이상 cluster system에 포함될 수 없는 경우에 사용하는 것이 바람직하다.

<a id="4ec93d40b95c308c"></a>
### 사용 예

다음은 &lt;alter database drop inactive members statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="371863230f19f26e"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="8f51c10e5365d1e6"></a>
### 참조

관련 내용은 [ALTER SYSTEM JOIN DATABASE](#1ea465f52dedef18) 를 참조한다.

<a id="c03c2f215d3df668"></a>
## ALTER DATABASE DROP LOGFILE

<a id="02f62009a462cf21"></a>
### 기능

데이터베이스에 존재하는 로그파일 그룹이나 멤버를 제거한다.

<a id="a0f9393e361210bb"></a>
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

<a id="74621b1c5ea11457"></a>
### 사용 범위 및 접근 권한

&lt;alter database drop logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="b5bb957e321b455c"></a>
### 구문 규칙 및 파라미터

<a id="68d12a06ff4eede8"></a>
#### &lt;alter database drop logfile statement&gt;

데이터베이스는 MOUNT 상태여야 한다.  
제거하려는 로그파일이 CURRENT 또는 ACTIVE 상태일 때는 에러가 발생한다.  
제거한 후에 최소 네 개의 로그파일 그룹이 남아 있어야 한다.

<a id="fa6aa996ba4eefda"></a>
#### &lt;drop logfile group statement&gt;

기존의 로그파일 그룹을 제거한다.

- &lt;group clause&gt; 
    - 제거할 로그파일 그룹을 지정한다.
    - integer는 존재하는 로그파일의 식별자여야 한다. 
    - integer가 존재하지 않을 경우 에러가 발생한다.

<a id="3d5d69aee2fe9a7f"></a>
#### &lt;drop logfile member statement&gt;

기존의 로그파일 멤버들을 제거한다.

- &lt;logfile_list&gt;
    - 제거할 로그파일 멤버의 목록이다. 
    - 'logfile_name'은 존재하는 이름이어야 한다. 
    - 'logfile_name'이 존재하지 않을 경우 에러가 발생한다.

<a id="9fd176f30458eb55"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="41e57e48a2606c67"></a>
### 사용 예

다음은 기존 로그파일인 GROUP 3을 제거하는 예이다.

```
ALTER DATABASE DROP LOGFILE GROUP 3;
```

다음은 기존 로그파일인 GROUP 3에서 'logfile1.log'와 'logfile2.log'를 제거하는 예이다.

```
ALTER DATABASE DROP LOGFILE MEMBER 'logfile1.log', 'logfile2.log';
```

<a id="8c265a50fcd21abc"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="69d222ca49d91a19"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#4877f17dc24787bd)
- [ALTER DATABASE RENAME LOGFILE](#9baf0d73d32ecb14)

<a id="23d029dca809fb16"></a>
## ALTER DATABASE MOVE SHARD

<a id="8646c09767949438"></a>
### 기능

특정 cluster group의 모든 table들의 shard를 다른 cluster group으로 재배치한다.

<a id="8e87d70ab14da254"></a>
### 구문

```
<alter database move shard statement> ::=
    ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP src_cluster_group
        TO CLUSTER GROUP dest_cluster_group [ ONLINE | OFFLINE ];
```

<a id="91b3eca8f59413a9"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database move shard statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="835346dba2ce6251"></a>
### 구문 규칙 및 파라미터

<a id="30e84f6a2ad00896"></a>
#### src_cluster_group

테이블의 shard를 이동할 cluster group이다.

<a id="6eb5c14cc241d792"></a>
#### dest_cluster_group

테이블의 shard를 이동시킬 target cluster group이다.

<a id="40c1347da548e4d6"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="b91159b92a688968"></a>
### 설명

다음과 같은 구문을 사용하여 cluster member와 cluster group을 추가할 때 table들의 shard는 재배치하지 않는다.

- [CREATE CLUSTER GROUP](#609ea3458a43136d)
- [ALTER CLUSTER GROUP name ADD MEMBER](#3d7884550455c0c5)

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

특정 테이블의 shard 재배치에 실패하더라도 &lt;alter database move shard statement&gt; 구문은 계속 진행되고 shard 재배치에 성공한 테이블을 rollback 하지 않는다.

따라서 에러에 대해 적절한 조치를 취한 후 &lt;alter database move shard statement&gt; 구문을 다시 수행하면 이미 shard 재배치에 성공한 테이블들은 재배치 대상에 포함되지 않으며, 재배치가 필요한 테이블들의 shard만 재배치한다.

<a id="d1b67511c4990b7c"></a>
### 사용 예

다음은 &lt;alter database move shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP G1 TO CLUSTER GROUP G2;

Database altered.
```

<a id="e3ecb93ca08f56a0"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="5e65fe056800163f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name MOVE SHARD](#ba4cbd044acbe360)
- [CREATE CLUSTER GROUP](#609ea3458a43136d)
- [ALTER CLUSTER GROUP name ADD MEMBER](#3d7884550455c0c5)

<a id="53a28403ac1b476a"></a>
## ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS

<a id="c793f3a6ae284781"></a>
### 기능

모든 inactive cluster member들을 offline 상태로 변경한다. 즉, 해당 cluster member들에 대한 shard map을 offline 상태로 변경한다.

<a id="441dec51684fd17a"></a>
### 구문

```
<alter database offline inactive cluster members statement> ::=
    ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS
    ;
```

<a id="51d14da8fb574df7"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database offline inactive cluster members statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="5eb73236070325d5"></a>
### 구문 규칙 및 파라미터

모든 inactive cluster member들을 offline 상태로 변경한다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

<a id="51846f7875c1c78e"></a>
### 설명

&lt;alter database offline inactive members statement&gt; 구문은 모든 inactive cluster member 들이 더 이상 cluster system에 포함될 수 없는 경우에 사용하는 것이 바람직하다.

Inactive cluster member가 cluster system에 참여할 수 있으면 [ALTER SYSTEM JOIN DATABASE](#1ea465f52dedef18) 구문을 수행하여 cluster system에 포함시킨다.

Offline 상태로 변경된 cluster member는 join 후에 다음 구문을 사용하여 online 상태로 다시 변경할 수 있다

- [ALTER DATABASE REBALANCE](#092cbc6985d152fb)
- [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef)

<a id="691f20a9d9252463"></a>
### 사용 예

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;
```

<a id="6bdbfee52a2adde9"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="d769364eae174286"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER SYSTEM JOIN DATABASE](#1ea465f52dedef18)
- [ALTER DATABASE REBALANCE](#092cbc6985d152fb)
- [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef)

<a id="092cbc6985d152fb"></a>
## ALTER DATABASE REBALANCE

<a id="742fa21bfa36e2d7"></a>
### 기능

모든 table들의 shard를 재배치한다.

<a id="a065ffa6bf8dd186"></a>
### 구문

```
<alter database rebalance statement> ::=
    ALTER DATABASE REBALANCE [ ONLINE | OFFLINE ];
```

<a id="e3a5aabbb92c5780"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database rebalance statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="8b37179f58160e2e"></a>
### 구문 규칙 및 파라미터

<a id="20e7f62a8ad8d4e0"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="2f0f3f116f226497"></a>
### 설명

다음과 같은 구문을 사용하여 cluster member, cluster group을 추가할 때 table들의 shard를 재배치하지 않는다.

- [CREATE CLUSTER GROUP](#609ea3458a43136d)
- [ALTER CLUSTER GROUP name ADD MEMBER](#3d7884550455c0c5)

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

<a id="cc2854522e3e6011"></a>
### 사용 예

다음은 &lt;alter database rebalance statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE REBALANCE;

Database altered.
```

<a id="c2823f874aef4f3b"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="f52728025c33b634"></a>
### 참조

관련 내용은 [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef)를 참조한다.

<a id="4b39c0cd3f8d62c9"></a>
## ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP

<a id="863a1269fbc5a08c"></a>
### 기능

특정 cluster group에 shard가 포함되지 않도록 모든 테이블의 shard를 재배치한다.

<a id="b2ba794470e4a67a"></a>
### 구문

```
<alter database rebalance exclude cluster group statement> ::=
    ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP cluster_group_name [ ONLINE | OFFLINE ];
```

<a id="6bb60c880ceccb5a"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database rebalance exclude cluster group statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="50c6fc20977502bb"></a>
### 구문 규칙 및 파라미터

<a id="d5d0d214260bf926"></a>
#### cluster_group_name

테이블들의 shard를 포함하지 않는 cluster group의 이름이다.  
지정한 cluster group이 유일한 cluster group인 경우 구문을 수행할 수 없다.

<a id="3bb4e3ab4fc0e3dd"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="5167eb722ce5198e"></a>
### 설명

[DROP CLUSTER GROUP](#d185e21cb13f6ec6) 구문을 사용하여 cluster group을 제거하려면 해당 cluster group에 shard가 존재하지 않아야 한다.

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

<a id="86d7668770fada56"></a>
### 사용 예

다음은 &lt;alter database rebalance exclude cluster group statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP g3;

Database altered.
```

<a id="4825a23ff36554ba"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="2c27de9841cc0d82"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP CLUSTER GROUP](#d185e21cb13f6ec6)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#3ed7b9af5c2a9447)

<a id="9baf0d73d32ecb14"></a>
## ALTER DATABASE RENAME LOGFILE

<a id="74274a0b2444e50f"></a>
### 기능

데이터베이스에서 로그파일의 이름을 수정한다.

<a id="c8b23e658224f8a6"></a>
### 구문

```
<alter database rename logfile statement> ::=
    ALTER DATABASE RENAME LOGFILE <logfile_list> TO <logfile_list>
    ;

<logfile_list> ::=
      'logfile_name'
    | <logfile_list> , 'logfile_name'
```

<a id="414878fd4fab063d"></a>
### 사용 범위 및 접근 권한

&lt;alter database rename logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="51ef6788e9a5d874"></a>
### 구문 규칙 및 파라미터

<a id="9fb1c5443937d12a"></a>
#### &lt;alter database rename logfile statement&gt;

- 데이터베이스는 MOUNT 상태여야 한다.
- FROM &lt;logfile_list&gt;
    - 데이터베이스에서 수정할 로그파일들의 이름 목록이다.
- TO &lt;logfile_list&gt;
    - 데이터베이스에서 수정될 로그파일들의 이름 목록이다. 
    - &lt;logfile_list&gt;는 존재하는 파일이어야 한다. 
    - 파일이 존재하지 않을 경우 에러가 발생한다.

<a id="b414354d54617b89"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="c7500d035beb97ca"></a>
### 사용 예

다음은 기존 로그파일 'logfile.log'를 'newlogfile.log'로 변경하는 예이다.

```
ALTER DATABASE RENAME LOGFILE 'logfile.log' TO 'newlogfile.log';
```

<a id="7e7d55064293b48f"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="33df4c94141ca047"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#4877f17dc24787bd)
- [ALTER DATABASE DROP LOGFILE](#c03c2f215d3df668)

<a id="e877de8414d4d237"></a>
## ALTER DATABASE RECOVER

<a id="ab9eb509b32474ce"></a>
### 기능

온라인/ archive log file을 사용하여 데이터베이스 내의 전체 데이터파일 (datafile) 또는 일부 데이터파일을 복구한다.

<a id="90f5cf1a21836237"></a>
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

<a id="709c95e2159860c1"></a>
### 사용 범위 및 접근 권한

&lt;alter database recover statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="c0cbcfb86fb0135b"></a>
### 구문 규칙 및 파라미터

<a id="67b24e675ec85621"></a>
#### &lt;complete database recover statement&gt;

온라인 및 archive log file을 이용하여 데이터베이스의 데이터 파일들을 최신 상태로 복구한다.

- ONLINE 상태의 모든 테이블스페이스를 복구한다. 
- 데이터베이스는 MOUNT 상태여야하고, ARCHIVELOG 모드여야 한다. 
- 필요한 archive log file이 존재하지 않으면 실패한다.

<a id="bad9078d1cdd8949"></a>
#### &lt;datafile recover statement&gt;

Immediate option으로 offline 된 tablespace의 datafile, backup된 datafile 또는 backup 중 장애로 인해 archive logfile을 이용한 복구가 필요한 tablespace의 datafile들을 최신상태로 복구한다.

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

<a id="5f8441bd7f6f3fed"></a>
#### &lt;complete tablespace recover statement&gt;

테이블스페이스의 데이터 파일들을 최신 상태로 복구한다.

- 테이블스페이스를 복구하려면 데이터베이스가 MOUNT 또는 OPEN 상태여야 한다. 
- OPEN 상태에서의 복구는 OFFLINE 상태의 테이블스페이스만 가능하고, MOUNT 상태에서의 복구는 ONLINE/ OFFLINE 상태의 테이블스페이스 모두에 가능하다. 
- 필요한 archive log file이 존재하지 않으면 복구에 실패한다.
- 다음과 같은 경우에는 테이블스페이스 복구 연산이 필요하다.
    - IMMEDIATE로 OFFLINE 된 테이블스페이스
    - 백업된 데이터 파일을 이용해야 하는 경우
    - 전체 백업 중 장애가 발생한 경우

<a id="a2dd0644d7d3449c"></a>
#### &lt;incomplete database recover statement&gt;

<a id="5e2dc4c54fa584fa"></a>
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
    - Deprecated.

<a id="2a21cbac3f00f47d"></a>
##### &lt;interactive incomplete database recover statement&gt;

온라인 및 archive log file을 이용하여 데이터베이스의 데이터 파일들을 최신상태가 아닌 특정 시점까지 사용자와 대화식으로 복구한다.

- ONLINE 상태의 모든 테이블스페이스를 복구한다. 
- 데이터베이스는 MOUNT 상태여야하고, ARCHIVELOG 모드여야 한다. 
- 불완전 복구될 시점 이후의 데이터가 존재하는 데이터파일을 이용하면 실패한다. 
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

<a id="3e04cf25ed98ee80"></a>
### 설명

데이터베이스 불완전 복구는 복구 완료 시점을 한 번에 찾아내기 어려우므로 여러 번 수행하여 원하는 복구 시점을 찾아야 한다. 그런데 불완전 복구가 완료된 후 RESETLOGS 옵션으로 데이터베이스를 기동하면 새로운 데이터베이스가 되기 때문에 archive log file과 온라인 redo log file에 대한 복사본을 만든 후에 불완전 복구를 여러 번 수행해야 한다.

<a id="d22588c5500384f8"></a>
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

<a id="42269ce9928db2c8"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다

<a id="0bdd376d8578c6cd"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#65c7e2f31a8e4d5f)
- [ALTER TABLESPACE name BACKUP](#bffdd0e4b8821918)
- [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#f434c9481edc0db8)

<a id="d6b95b4faa95b7e3"></a>
## ALTER DATABASE REGISTER

<a id="593f95dc49cfa090"></a>
### 기능

복구 불가능한 세그먼트를 데이터베이스에 등록한다.

<a id="972304245a67384d"></a>
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

<a id="16074cf258e64cf6"></a>
### 사용 범위 및 접근 권한

&lt;alter database register statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="1bd7f06bca47476c"></a>
### 구문 규칙 및 파라미터

<a id="24dd4152cad015d2"></a>
#### &lt;alter database register statement&gt;

복구 불가능한 세그먼트를 데이터베이스에 등록한다. 해당 구문은 백업이 존재하지 않고 데이터베이스를 복구할 수 없는 경우, 세그먼트를 더 이상 사용하지 않는다는 가정하에 사용될 수 있다.

- 데이터베이스가 MOUNT 상태여야 한다.
- 등록된 세그먼트 식별자 목록은 재시작할 때 초기화된다.
- 서버 재시작에 성공하면 등록된 세그먼트들이 'UNUSABLE' 상태가 되는데 해당 세그먼트들은 반드시 삭제해야 한다.

<a id="66ae4424b7fdb78b"></a>
#### &lt;segment physical identifier list&gt;

복구 불가능한 세그먼트의 식별자 목록이다.  
• Integer: 8 바이트 정수형의 세그먼트 식별자

<a id="98c46e99dc37b4d7"></a>
### 설명

서버를 비정상 종료하고 재시작할 때 데이터베이스를 복구하는데, 이 때 이전 서비스 단계에서 디스크에 반영되지 못한 페이지들을 복구하기 위해서 REDO 로그들을 이용해 페이지를 다시 수행한다.

REDO 연산을 수행하는 중에 예상하지 못한 실패가 발생한 경우, 이를 무시하고 복구하기 위해 사용될 수 있다.

<a id="4ecfc4e1fb60663f"></a>
### 사용 예

다음은 4028679323648을 식별자로 갖는 세그먼트 복구를 포기하는 예이다.

```
ALTER DATABASE REGISTER IRRECOVERABLE SEGMENT 4028679323648;
```

<a id="747b4bb9fd166295"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="fdd0c078d47df673"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#bffdd0e4b8821918)
- [ALTER DATABASE RECOVER](#e877de8414d4d237)

<a id="2e355a2099dd657d"></a>
## ALTER DATABASE RESET LOCAL CLUSTER MEMBER

<a id="62f96bbe573e9cc0"></a>
### 기능

Local cluster member에서 tablespace 객체를 제외한 부분을 database 생성 시점으로 초기화한다.

<a id="83c9e4f52ada34f9"></a>
### 구문

```
<alter database reset local cluster member statement> ::=
    ALTER DATABASE RESET LOCAL CLUSTER MEMBER
    ;
```

<a id="0937e9dfd97a688a"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

Start-up 과정 중 LOCAL OPEN 단계에서 수행할 수 있다.

&lt;alter database reset local cluster member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="645070a35f2a7a1d"></a>
### 설명

Local cluster member에서 tablespace 객체를 제외한 부분을 database 생성 시점으로 초기화한다.  
Tablespace 객체를 제외하고 사용자가 생성한 모든 객체를 제거한다.

&lt;alter database reset local cluster member statement&gt; 구문은 inactive cluster member를 초기화하고,  
새로운 cluster member를 cluster system에 참여시키기 위해 사용한다.  
Cluster system과 연결이 끊긴 inactive cluster member 들은 다음과 같이 처리할 수 있다.

- Cluster system에 다시 참여할 수 있는 경우 JOIN 구문을 이용하여 참여시킨다. 
    - [ALTER SYSTEM JOIN DATABASE](#1ea465f52dedef18) 
- Cluster system에 다시 참여할 수 없는 경우, DROP 구문을 이용하여 cluster system에서 제외한다. 
    - [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#05f1c6bb77934e8a)

이 때, cluster system에서 제외된 cluster member에 해당하는 장비는 다음 두 가지 방법으로 재사용할 수 있다.

- 방법 1: Local cluster member의 database를 다시 생성한다.
- 방법 2: &lt;alter database reset local cluster member statement&gt; 구문을 이용해 local cluster member를 초기화한다.

방법 2는 방법 1보다 tablespace를 재생성하는 비용을 줄일 수 있다.

<a id="7450e97294fa63c2"></a>
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

<a id="2d7fd9819157ad7a"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="22de0b8ef08c5f17"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER SYSTEM JOIN DATABASE](#1ea465f52dedef18)
- [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#05f1c6bb77934e8a)

<a id="1b826e3e46d1c7bd"></a>
## ALTER DATABASE RESTORE

<a id="5e1ad051e8f8bc7e"></a>
### 기능

증분 백업을 이용하여 데이터베이스나 테이블스페이스 내의 데이터 파일들을 복원한다.

<a id="1d18e2f17c7af33e"></a>
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

<a id="02d97aa88e1ca156"></a>
### 사용 범위 및 접근 권한

alter database restore statement> 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="0853894dcb3dba65"></a>
### 구문 규칙 및 파라미터

<a id="7beb92ba2617614e"></a>
#### &lt;database restore statement&gt;

증분 백업을 사용하여 데이터베이스 내의 데이터 파일들을 복원한다.   
데이터베이스가 MOUNT 상태여야 한다.

<a id="d28d7badb72b6a40"></a>
#### &lt;tablespace restore statement&gt;

증분 백업을 사용하여 테이블스페이스 내의 데이터 파일들을 복원한다.

- 데이터베이스가 MOUNT 또는 OPEN 상태여야 한다.
- OPEN 상태에서는 OFFLINE 상태의 테이블스페이스만 복원할 수 있고, MOUNT 상태에서는 ONLINE/ OFFLINE 상태의 테이블스페이스 모두 복원할 수 있다.

<a id="7e4ac78de1db5643"></a>
#### &lt;controlfile restore statement&gt;

'file_name'을 사용하여 제어파일을 복원한다.

- 데이터베이스가 NOMOUNT 상태여야 한다.
- 'file_name'은 절대 경로를 권장하지만, 만약 상대 경로를 기술한 경우에는 &lt;GOLDILOCKS_HOME&gt;/wal/'file_name'을 이용한다.

<a id="8acc15cd3001778a"></a>
### 설명

전체 백업을 이용한 데이터 파일 복원은 OS 복사 명령으로 백업된 파일을 직접 데이터 파일 경로에 복사하는 방법이다. 증분 백업을 이용한 데이터 파일 복원은 삭제된 데이터 파일이나 이전 데이터 파일들만 복원한다.

<a id="5bbc7b8df953ea95"></a>
### 사용 예

다음은 증분 백업을 사용하여 데이터베이스를 복원하는 예이다.

```
ALTER DATABASE RESTORE;
```

다음은 증분 백업을 사용하여 테이블스페이스를 복원하는 예이다.

```
ALTER DATABASE RESTORE TABLESPACE test_tbs;
```

다음은 LSN이 11123 보다 작은 증분 백업만 사용하여 데이터베이스를 복원하는 예이다.

```
ALTER DATABASE RESTORE UNTIL CHANGE 11123;
```

다음은 controlfile.bak을 사용하여 제어파일을 복원하는 예이다.

```
ALTER DATABASE RESTORE CONTROLFILE FROM 'controlfile.bak'
```

<a id="45343bcbd2715b22"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="a112e05b4f19e023"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#65c7e2f31a8e4d5f)
- [ALTER TABLESPACE name BACKUP](#bffdd0e4b8821918)
- [ALTER DATABASE RECOVER](#e877de8414d4d237)

<a id="459aef51d5183228"></a>
## ALTER INDEX

<a id="bcf119c4b4206171"></a>
### 기능

인덱스 정의를 변경한다.

<a id="447e08b44a8d5936"></a>
### 구문

```
<alter index statement> ::=
      <alter index physical attribute statement>
    | <rename index statement>
    | <aging index statement>
    ;
```

<a id="8f59fd7b56d10348"></a>
### 사용 범위 및 접근 권한

&lt;alter index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="507ec4f6dfbfa228"></a>
### 구문 규칙 및 파라미터

<a id="1dfe35f5e89b0e17"></a>
#### &lt;alter index physical attribute statement&gt;

인덱스의 물리적 속성을 변경한다.  
자세한 내용은 [ALTER INDEX name STORAGE](#7a1d8855e5a3e9c8) 구문을 참조한다.

<a id="8a28b8cb4865b3a3"></a>
#### &lt;rename index statement&gt;

인덱스 이름을 변경한다.  
자세한 내용은 [ALTER INDEX name RENAME TO](#816edfcde4e7f3c5) 구문을 참조한다.

<a id="a994c865c482d735"></a>
#### &lt;aging statement&gt;

인덱스의 빈 페이지를 삭제한다.  
자세한 내용은 [ALTER INDEX name AGING](#b11975734fa34052) 구문을 참조한다.

<a id="013a1b31601da662"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="ddd095ee8a70a853"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="04f4b894be185b54"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="b11975734fa34052"></a>
## ALTER INDEX name AGING

<a id="820ef175d2d1e856"></a>
### 기능

인덱스의 빈 페이지를 삭제한다.

<a id="999a69bd7ec846d6"></a>
### 구문

```
<aging index statement> ::=
    ALTER INDEX index_name AGING
    ;
```

<a id="7d81a90148cec2e7"></a>
### 사용 범위 및 접근 권한

&lt;aging index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="f1ab57fbaf8e3fb9"></a>
### 구문 규칙 및 파라미터

<a id="f3ff07de353f2cd2"></a>
#### index_name

대상 인덱스의 이름이다.

<a id="dd3f1b7c2f7dbcd0"></a>
### 설명

해당 구문은 인덱스 페이지들 중에 모든 키가 삭제된 페이지들을 세그먼트로 반납한다. Aging은 논리적 삭제와 물리적 삭제의 2단계로 진행된다. 논리적 삭제는 인덱스에서 페이지를 지칭하는 연결을 끊는 작업이며 페이지의 마지막 키를 삭제할 당시의 SCN이 시스템의 agable SCN보다 작을 때 수행된다. 이후 물리적 삭제가 이루어지는데 논리적으로 삭제할 때의 SCN이 시스템의 agable SCN보다 작을 때 수행된다.

> 만약 시스템의 agable SCN이 증가하지 않으면 인덱스 AGING 구문이 성공하더라도 빈 페이지가 삭제되지 않을 수 있다.

<a id="fa66d13ee4f1d647"></a>
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

<a id="0567a768b3b777d9"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="f6a0ed39420fda92"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](#ce4afb58f69a16f7)
- [ALTER INDEX](#459aef51d5183228)
- [DROP INDEX](#93a6d0dc40b79b2e)

<a id="7a1d8855e5a3e9c8"></a>
## ALTER INDEX name STORAGE

<a id="fd9df8e9322f9928"></a>
### 기능

인덱스의 물리적 속성을 변경한다.

<a id="ce1480cd9e67fa42"></a>
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

<a id="af88d60fbe42f0df"></a>
### 사용 범위 및 접근 권한

&lt;alter index physical attribute statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="b464f02f66936ee9"></a>
### 구문 규칙 및 파라미터

<a id="a469f1b9b27fd987"></a>
#### index_name

대상 인덱스의 이름이다.

<a id="3e9e19be779c9cff"></a>
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

<a id="1e738c066e414df0"></a>
#### &lt;segment attr clause&gt;

인덱스가 저장될 공간에 대한 정보를 기술한다.

- INITIAL integer 
    - 정의 
        - 인덱스를 생성할 때 초기에 할당할 물리적 공간의 크기를 기술한다. 
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT 크기가 8192 bytes일 경우 'INITIAL 100'은 실제 8192 bytes로 동작한다.) 
        - 이 크기 (TABLESPACE의 EXTENT 크기에 align 된 크기)는 MINEXTENTS의 크기와 같거나 커야 하며, MAXEXTENTS의 크기와 같거나 작아야 한다. 
        - 인덱스 bottom-up 빌드 시에만 적용된다. 
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다. 
    - 생략할 경우, 기본값은 테이블이 속한 TABLESPACE의 EXTENT 하나 크기이다.

- NEXT integer
    - 정의
        - 인덱스의 물리적 공간을 추가할 경우 할당할 물리적 공간의 크기를 기술한다.
        - 이 크기는 테이블이 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다. (예: EXT 크기가 8192 bytes일 경우 'NEXT 100'은 실제 8192 bytes로 동작한다.)
        - NEXT는 현재 인덱스가 사용할 수 있는 남은 공간의 크기 (MAXEXTENTS의 크기에서 현재 사용하고 있는 공간의 크기를 뺀 크기)에 따라 아래와 같이 동작한다.  
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

<a id="7575a73941ae5fa5"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="3fc22af4de50becb"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="93d75068c49041ea"></a>
### 사용 예

다음은 인덱스의 물리적 속성을 변경하는 예이다.

```
gSQL> ALTER INDEX idx_t1_id PCTFREE 10 INITRANS 4 MAXTRANS 8;

Index altered.
```

<a id="cc2f809e229efbb9"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="6b88ca8505e14be5"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](#ce4afb58f69a16f7)
- [ALTER INDEX](#459aef51d5183228)
- [DROP INDEX](#93a6d0dc40b79b2e)

<a id="816edfcde4e7f3c5"></a>
## ALTER INDEX name RENAME TO

<a id="6b0d8682bb6aedc0"></a>
### 기능

인덱스의 이름을 변경한다.

<a id="6d1f08c819e19e3d"></a>
### 구문

```
<rename index statement> ::=
    ALTER INDEX index_name
        RENAME TO new_index_name
    ;
```

<a id="774ff61af93306b2"></a>
### 사용 범위 및 접근 권한

&lt;rename index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="9158598f04d7617c"></a>
### 구문 규칙 및 파라미터

<a id="c8c381a6250e23be"></a>
#### index_name

대상 인덱스의 이름이다.  
스키마 이름을 기술할 수 없으며, 기존 인덱스와 동일한 스키마 이름을 갖는다.

<a id="276f2998199c4c45"></a>
#### new_index_name

새로운 인덱스의 이름이며 스키마 내에서 유일한 인덱스 이름이어야 한다.

<a id="92dbdae0d5101d2e"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="d8bf1ed4a88a2f77"></a>
### 사용 예

다음은 인덱스의 이름을 변경하는 예이다.

```
gSQL> ALTER INDEX t1_idx1 RENAME TO idx_t1_id;

Index altered.
```

<a id="463baa197e005bec"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="4af078eaa409edc3"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](#ce4afb58f69a16f7)
- [ALTER INDEX](#459aef51d5183228)
- [DROP INDEX](#93a6d0dc40b79b2e)

<a id="e26c5af4933c1efe"></a>
## ALTER PROFILE

<a id="d28d8fdd71aea323"></a>
### 기능

비밀번호 관리 방법을 변경한다.

<a id="d3642ec761af52e0"></a>
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

<a id="2e19693a15f5996c"></a>
### 사용 범위 및 접근 권한

&lt;alter profile statement&gt; 구문을 수행하려면 사용자에게 ALTER PROFILE ON DATABASE 권한이 있어야 한다.

<a id="e054eaa9ea80da86"></a>
### 구문 규칙 및 파라미터

<a id="8fb78ec4b985be44"></a>
#### profile_name

변경할 profile의 이름이다.

<a id="b7d4f0e5eb809d63"></a>
#### FAILED_LOGIN_ATTEMPTS

로그인 연속 실패 허용 횟수를 설정한다.  
자세한 내용은 [CREATE PROFILE](#208fdfbd422ca37d) 구문을 참조한다.

<a id="ab1cd49e51e6fc17"></a>
#### PASSWORD_LOCK_TIME

로그인에 연속적으로 실패한 후에 계정이 잠기는 기간 (day)을 설정한다.  
자세한 내용은 [CREATE PROFILE](#208fdfbd422ca37d) 구문을 참조한다.

<a id="b9b746e54748c27d"></a>
#### PASSWORD_LIFE_TIME

비밀번호의 유효 기간 (day)을 설정한다.  
자세한 내용은 [CREATE PROFILE](#208fdfbd422ca37d) 구문을 참조한다.

<a id="d755aba45770dee3"></a>
#### PASSWORD_GRACE_TIME

PASSWORD_LIFE_TIME 이후에 로그인 할 때 비밀번호 만료를 유예하는 기간을 설정한다.  
자세한 내용은 [CREATE PROFILE](#208fdfbd422ca37d) 구문을 참조한다.

<a id="12d6f0e07395baeb"></a>
#### PASSWORD_REUSE_MAX

이전 비밀번호를 재사용하려 할 때 재사용할 수 없는 최근 비밀번호 개수를 명시한다.  
자세한 내용은 [CREATE PROFILE](#208fdfbd422ca37d) 구문을 참조한다.

<a id="03a7e21205927065"></a>
#### PASSWORD_REUSE_TIME

이전 비밀번호를 재사용하기 위해 필요한 경과 기간을 명시한다.  
자세한 내용은 [CREATE PROFILE](#208fdfbd422ca37d) 구문을 참조한다.

<a id="fb5782ab5f527709"></a>
#### PASSWORD_VERIFY_FUNCTION

비밀번호 복잡도 검증 방법을 설정한다.  
자세한 내용은 [CREATE PROFILE](#208fdfbd422ca37d) 구문을 참조한다.

<a id="1c88d03992388922"></a>
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

<a id="4995f952f3b70ed3"></a>
### 호환성

SQL 표준은 profile에 대한 개념을 다루지 않고 있다.

<a id="0ac84325ea05b569"></a>
### 참조

관련 내용은 [DROP PROFILE](#b370f178d1d3dd6a)을 참조한다.

<a id="9fd8a84df33183e1"></a>
## ALTER SEQUENCE

<a id="2c1bc3c806ac6181"></a>
### 기능

시퀀스를 변경한다.

<a id="85455a2555d6e7fd"></a>
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

<a id="66d0a928e779ac6a"></a>
### 사용 범위 및 접근 권한

&lt;alter sequence generator statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 시퀀스의 소유자 
- 시퀀스가 속한 스키마에 대해 (ALTER SEQUENCE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY SEQUENCE ON DATABASE

<a id="4914d0edc1d730a7"></a>
### 구문 규칙 및 파라미터

<a id="de56e23a144cd9fb"></a>
#### sequence_name

변경할 시퀀스의 이름이다.  
schema_name.sequence_name과 같이 시퀀스가 속할 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="64e81a28377c756f"></a>
#### &lt;alter sequence generator restart option&gt;

시퀀스의 다음 값 (NEXT VALUE)을 설정한다.  
단, [CREATE SEQUENCE](#cdaeabbec6dc28f1) 구문에서 정의한 START WITH의 값은 변경하지 않는다.

- RESTART 
    - 값을 명시하지 않을 경우, &lt;sequence generator definition&gt;에서 정의한 START WITH의 값이 시퀀스의 다음 값으로 설정된다. 
- RESTART WITH integer 
    - integer 값을 시퀀스의 다음 값으로 설정한다. 
    - integer 값은 MINVALUE와 MAXVALUE 사이의 값이어야 한다.

&lt;alter sequence generator restart option&gt; 절을 명시하지 않은 경우, 시퀀스의 현재값을 기준으로 시퀀스의 속성을 변경한다.

<a id="9b1b4b3fc259ccd0"></a>
#### &lt;sequence generator increment by option&gt;

시퀀스 번호의 간격을 변경한다.  
다음과 같은 제약과 특징을 갖는다.

- 양수 또는 음수를 사용할 수 있으며, 0은 사용할 수 없다. 
- 간격의 절대값은 MINVALUE와 MAXVALUE의 차이보다 작아야 한다. 
- 양수일 경우 오름차순 시퀀스가 되고 음수일 경우 내림차순 시퀀스가 된다.

<a id="c12f9be6cbf9688b"></a>
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

<a id="fc9d186699d71477"></a>
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

<a id="446d29a6ffb04a41"></a>
#### &lt;sequence generator cycle option&gt;

시퀀스의 값이 최대값 또는 최소값이 되었을 때, 계속 값을 생성할지 여부를 변경한다.

- CYCLE 
    - 오름차순 시퀀스가 최대값이 되었을 때, 최소값부터 다시 생성한다. 
    - 내림차순 시퀀스가 최소값이 되었을 때, 최대값부터 다시 생성한다. 
- NO CYCLE | NOCYCLE 
    - 최대값 또는 최소값이 되었을 때, 시퀀스 값을 생성할 수 없다. 
    - NO CYCLE (SQL 표준)과 NOCYCLE은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다.

<a id="a33e3ade276e6762"></a>
#### &lt;sequence generator cache option&gt;

시퀀스에 신속하게 접근하기 위해 메모리상에 미리 적재할 시퀀스 값의 개수를 정의한다.  
Database를 재구동할 때, 메모리상에 적재한 시퀀스 값은 유실되고 적재한 이후의 값부터 시작된다.

- CACHE integer 
    - CACHE 값은 2와 같거나 커야하고 
    - CYCLE이 존재할 경우 CACHE 값이 CYCLE의 길이보다 크지 않아야 한다. 
        - CYCLE의 길이: CEIL(MAXVALUE - MINVALUE) / ABS(INCREMENT) 
- NO CACHE | NOCACHE 
    - 메모리 상에 시퀀스값을 미리 적재하지 않는다.

<a id="71654f53a61016be"></a>
### 설명

[CREATE SEQUENCE](#cdaeabbec6dc28f1) 구문에서 정의한 시퀀스 속성 중 START WITH는 변경할 수 없다.  
START WITH 속성을 변경하려면 [DROP SEQUENCE](#7debf989c0a88d02) 구문을 수행한 후에 [CREATE SEQUENCE](#cdaeabbec6dc28f1) 구문을 사용하여 다시 생성해야 한다.

<a id="fd9f33e69b1fda85"></a>
### 사용 예

다음은 RESTART 옵션으로 시퀀스 값을 재시작하고 이를 사용하여 ID 값을 새로 부여하는 예이다.

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

<a id="82af4dd269ccd913"></a>
### 호환성

SQL 표준에서는 CACHE/ NO CACHE 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="2d8d44bccb501426"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T176 | Sequence generator support | O |
| T177 | Sequence generator support: simple restart option | O |

<a id="d336016e9e42e44e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE SEQUENCE](#cdaeabbec6dc28f1)
- [DROP SEQUENCE](#7debf989c0a88d02)

<a id="1c3db2ff9085b55f"></a>
## ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

<a id="449ce913ca06481e"></a>
### 기능

세션에서 재사용하기 위해 catching 된 모든 공간들을 해당 tablespace로 반환한다.

<a id="7a985545437411d3"></a>
### 구문

```
<alter session cleanup global temporary segment pool statement> ::=
    ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL
    ;
```

<a id="feb8f8246156468e"></a>
### 설명

수행된 세션에서 segment cache의 segment들만 cleanup한다.

<a id="ec80b77ab4293647"></a>
### 사용 예

다음은 세션 segment cache를 cleanup하는 예이다.

```
gSQL> ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

Session altered.
```

<a id="b45d0329d7ba8ca0"></a>
### 호환성

SQL 표준에서는 global temporary table, global temporary index의 segment cache 개념을 정의하지 않고 있다.

<a id="a57486d0703443b9"></a>
### 참조

관련 내용은 [Global Temporary Table](13-sql-objects.md#7715e064852d7bc8) 을 참조한다.

<a id="824f5c01b1aa6faa"></a>
## ALTER SESSION SET property_name

<a id="a3ead45c49f2f344"></a>
### 기능

세션의 프로퍼티 값을 설정한다.

<a id="bb2c7fda92d72215"></a>
### 구문

```
<alter session set statement> ::=
    ALTER SESSION SET <property name> { = <property value> | TO DEFAULT }
    ;
```

<a id="fda52564d6f6921c"></a>
### 구문 규칙 및 파라미터

<a id="ed87d8e1022d3db2"></a>
#### &lt;property name&gt;

설정할 프로퍼티 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5debfb33dc9cdf97) 장을 참조한다.

<a id="bc7b89eeba1da034"></a>
#### &lt;property value&gt;

설정할 프로퍼티 값이다.

<a id="269e79e80a0c287a"></a>
#### TO DEFAULT

세션 프로퍼티 값을 시스템 프로퍼티 값으로 설정한다.

<a id="561d7efe4ed15d57"></a>
### 설명

각 property에 대한 자세한 설명은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5debfb33dc9cdf97) 장을 참조한다.

<a id="7dbd338cea628c2d"></a>
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

<a id="e7e11b1fbec5da78"></a>
### 호환성

SQL 표준에서는 세션 프로퍼티 개념을 정의하지 않고 있다.

<a id="dfcad9a1f70a3199"></a>
### 참조

관련 내용은 [ALTER SESSION SET property_name](#824f5c01b1aa6faa)을 참조한다.

<a id="a5f0000705e9bf3d"></a>
## ALTER SYSTEM CHECKPOINT

<a id="810f8f073f70dc8d"></a>
### 기능

CHECKPOINT를 수행한다.

<a id="fc5bafd94fb05032"></a>
### 구문

```
<alter system checkpoint statement> ::=
    ALTER SYSTEM CHECKPOINT
    [ AT <domain name> ]
    ;
```

<a id="2d804828a0096d45"></a>
### 사용 범위 및 접근 권한

&lt;alter system checkpoint statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="d9c47c7c10a0b6dd"></a>
### 구문 규칙 및 파라미터

<a id="3041a5bcea076363"></a>
#### &lt;alter system checkpoint statement&gt;

CHECKPOINT는 commit된 트랜잭션들이 변경한 모든 데이터가 디스크에 기록되는 것을 보장하는 연산이다.

- 데이터베이스가 OPEN 상태여야 한다.
- 데이터베이스가 TDS 모드여야 한다.
- 전체 백업이 진행중일 때는 변경된 페이지가 데이터 파일에 기록되지 않고, REDO 로그와 제어파일만 디스크에 기록된다. 만약 이러한 상태에서 서버가 비정상 종료되는 경우에는 미디어 복구를 수행해야 한다.

<a id="e84f9700d3ca2c68"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="9a492e503f7ff7a1"></a>
### 설명

체크포인트 (checkpoint) 연산은 commit 된 트랜잭션들이 변경한 모든 내용을 디스크에 기록함으로써 시스템 장애시 신속한 복구를 가능하게 한다.

<a id="1a1303290c9ae05d"></a>
### 사용 예

다음은 CHECKPOINT를 수행하는 예이다.

```
ALTER SYSTEM CHECKPOINT;
```

<a id="8d3f313b1a940b4b"></a>
### 호환성

SQL 표준에서는 CHECKPOINT 개념을 정의하지 않고 있다.

<a id="31220075f9398edf"></a>
## ALTER SYSTEM CLEANUP PLAN

<a id="1c6eae425e070a54"></a>
### 기능

모든 SQL plan을 정리한다.

<a id="f6e45a254b42a787"></a>
### 구문

```
<alter system cleanup plan statement> ::=
    ALTER SYSTEM CLEANUP PLAN
    [ AT <domain name> ]
    ;
```

<a id="1f69d5e345e6921a"></a>
### 사용 범위 및 접근 권한

&lt;alter system cleanup plan statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="c8a079ca8e4f302b"></a>
### 구문 규칙 및 파라미터

<a id="270dc7efe6eb2583"></a>
#### &lt;alter system cleanup plan statement&gt;

해당 구문 규칙이나 파라미터가 존재하지 않는다.

<a id="6089925ab8e32559"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="ef5224883cdfb13e"></a>
### 설명

캐시되어 있는 모든 SQL plan을 정리한다.   
단, V$SQL_CACHE.REF_COUNT가 0보다 큰 plan (prepare된 statement에서 참조하는 plan)들은 정리 대상에서 제외한다.

<a id="acb7117da53008db"></a>
### 사용 예

다음은 CLEANUP PLAN을 수행하는 예이다.

```
ALTER SYSTEM CLEANUP PLAN;
```

<a id="bd14d9d91a7c4e6e"></a>
### 호환성

SQL 표준에서는 CLEANUP PLAN의 개념을 정의하지 않고 있다.

<a id="98ba2c93e7943236"></a>
## ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER

<a id="9fcf7f593bf40805"></a>
### 기능

복구 불가능한 클러스터 멤버를 지정한다.

<a id="e79daec905bedae5"></a>
### 구문

```
<alter system irrecoverable cluster member statement> ::=
    ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER <domain name>
    ;
```

<a id="035a060dcf38ecf4"></a>
### 사용 범위 및 접근 권한

&lt;alter system irrecoverable cluster member statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="ada2095d76014fc8"></a>
### 구문 규칙 및 파라미터

<a id="89cd13d4947d1fd3"></a>
#### &lt;alter system irrecoverable cluster member statement&gt;

해당 구문 규칙이나 파라미터가 존재하지 않는다.

<a id="24818fabb64f6fbe"></a>
#### &lt;domain name&gt;

복구 불가능한 멤버 이름이다.  
그룹 내의 모든 멤버들을 복구 불가한 멤버로 지정할 수 없다.

<a id="ea4ca526b21e1377"></a>
### 설명

복구 불가능한 멤버로 인해 클러스터 재시작에 실패하는 경우 해당 멤버를 제외하고 시스템을 재시작하기 위해 사용한다. 시스템 재시작에 성공한 후에는 반드시 [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#05f1c6bb77934e8a) 구문을 이용해 해당 멤버를 삭제해야 한다.

<a id="d80ad629c907b895"></a>
### 사용 예

다음은 IRRECOVERABLE CLUSTER MEMBER를 수행하는 예이다.

```
gSQL> ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER g1n1;
```

<a id="e819862aa93f8e56"></a>
### 호환성

SQL 표준에서는 IRRECOVERABLE CLUSTER MEMBER의 개념을 정의하지 않고 있다.

<a id="1ea465f52dedef18"></a>
## ALTER SYSTEM JOIN DATABASE

<a id="eab9145e0c391ea5"></a>
### 기능

비활성화된 특정 cluster member를 cluster system에 다시 포함시킨다.

<a id="8b33f6097ce8ab83"></a>
### 구문

```
<alter system join database statement> ::=
    ALTER SYSTEM JOIN DATABASE 
    ;
```

<a id="d81e31504bb5ecb0"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter system join database statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="0c114227fc997e3f"></a>
### 설명

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우 
- Cluster system에 포함된 cluster member를 구동하지 않고 cluster system start-up을 시도한 경우

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

<a id="bf8ca3e42d6b46b9"></a>
### 사용 예

```
gSQL> ALTER SYSTEM JOIN DATABASE;
```

<a id="124deaf2b594029b"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="1bd18e81b8e2d971"></a>
### 참조

관련 내용은 [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#05f1c6bb77934e8a)를 참조한다.

<a id="f434c9481edc0db8"></a>
## ALTER SYSTEM {MOUNT | OPEN} DATABASE

<a id="9defb8cbdd6d8a07"></a>
### 기능

데이터베이스를 시스템에 마운트하거나 서비스 가능한 상태로 변경한다.

<a id="059d835eec5f8bac"></a>
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

<a id="42381eae3be1fe25"></a>
### 사용 범위 및 접근 권한

&lt;alter system database statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="97cdcb0ed65221a5"></a>
### 구문 규칙 및 파라미터

<a id="43cd0faf50dc7205"></a>
#### &lt;alter system database clause&gt;

- MOUNT DATATABASE
    - 데이터베이스를 시스템에 마운트한다. 
- OPEN DATABASE
    - 데이터베이스를 서비스 가능한 상태로 변경한다.

<a id="dd13023c3fdf8a3e"></a>
#### &lt;open database option&gt;

- READ ONLY/ READ WRITE
    - 읽기 쓰기 모드를 지정하여 데이터베이스를 구동한다.
    - 생략된 경우에는 READ WRITE로 구동된다.
- RESETLOGS/ NORESETLOGS
    - 데이터베이스를 복구한 이후에 온라인 redo log를 유지할지 선택한다.
    - NORESETLOGS는 기존 redo log를 유지하는 반면에 RESETLOGS는 이를 초기화한다.
    - 데이터베이스를 불완전 복구한 경우, 반드시 RESETLOGS를 지정해야 한다.
    - 생략된 경우에는 NORESETLOGS가 기본으로 지정된다.

<a id="3053e481567f4fcc"></a>
#### &lt;database_scope&gt;

- LOCAL
    - LOCAL 영역 서버를 OPEN 단계로 구동한다.
- GLOBAL
    - GLOBAL 영역, 즉 전체 서버를 OPEN 단계로 구동한다.
- Cluster 환경에서 생략된 경우 GLOBAL로 구동 된다.

<a id="9618ee9d159b7392"></a>
### 사용 예

다음은 읽기 전용으로 데이터베이스를 구동하는 예이다.

```
ALTER SYSTEM OPEN DATABASE READ ONLY;
```

다음은 읽기/ 쓰기 모드로 구동하고, online redo log를 초기화하는 예이다.

```
ALTER SYSTEM OPEN DATABASE READ WRITE RESETLOGS;
```

<a id="26392b700225a730"></a>
### 호환성

SQL 표준에서는 데이터베이스의 MOUNT 또는 OPEN에 대한 개념을 정의하지 않고 있다.

<a id="49872a67a5ef35c1"></a>
### 참조

관련 내용은 [ALTER DATABASE RECOVER](#e877de8414d4d237)를 참조한다.

<a id="b6469604d5fddeb1"></a>
## ALTER SYSTEM [KILL | DISCONNECT] SESSION

<a id="d6b299c8b63b88ef"></a>
### 기능

세션을 종료한다.

<a id="ece5b621b3db8dd0"></a>
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

<a id="7096606786c31f30"></a>
### 사용 범위 및 접근 권한

&lt;alter system end session statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="b101c1f65b3c103d"></a>
### 구문 규칙 및 파라미터

<a id="3c430e38767bf1e9"></a>
#### &lt;member_position&gt;

Cluster 환경에서 disconnect/ kill 대상이 되는 세션의 member position 이다.

<a id="3e8c0b5190a10fe3"></a>
#### &lt;session_id&gt;

세션의 ID 이다.

<a id="450c321c3739fde8"></a>
#### &lt;serial#&gt;

세션의 SERIAL NUMBER이다.

<a id="20cc792f14e5b76f"></a>
#### &lt;disconnect_option&gt;

- POST_TRANSACTION: 트랜잭션 완료 후 세션을 종료한다.
- IMMEDIATE: 트랜잭션 완료를 기다리지 않고 바로 세션을 종료한다.

&lt;disconnect_option&gt;이 사용되지 않으면 IMMEDIATE로 작동한다.

<a id="fc4282979ca83eec"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="65690bed32064eac"></a>
### 설명

DISCONNECT SESSION은 POST_TRANSACTION과 IMMEDIATE 옵션을 지정할 수 있으며, POST_TRANSACTION은 현재 실행되는 트랜잭션이 있을 경우 트랜잭션이 끝난 후에 세션을 종료한다. IMMEDIATE는 현재 수행 중인 트랜잭션을 바로 정리한 후에 세션을 종료한다.

KILL SESSION은 해당 세션의 프로세스는 존재하지 않지만 시스템에 남아있는 비정상 세션을 종료한다.

<a id="e1fccef1b5786a75"></a>
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

<a id="ecd4352167c53140"></a>
### 호환성

SQL 표준에서는 정의하지 않고 있다.

<a id="26ff93695df9d6b1"></a>
## ALTER SYSTEM RECONNECT GLOBAL CONNECTION

<a id="e8d58e5e862c6eb1"></a>
### 기능

GLOBAL CONNECTION 형태로 접속한 세션에 재접속할지 여부를 설정한다.

<a id="9d0a1185fd1050ca"></a>
### 구문

```
<alter system reconnect global connection statement> ::=
    ALTER SYSTEM RECONNECT GLOBAL CONNECTION
    ;
```

<a id="531fb89273f17d3c"></a>
### 사용 범위 및 접근 권한

&lt;alter system reconnect global connection statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="c91e8ba99ada878f"></a>
### 설명

GLOBAL CONNECTION 클라이언트의 재접속 여부는 최초 접속할 때 서버로부터 얻은 system 객체의 SCN과 현재 서버의 system 객체의 SCN을 비교하여 결정한다. 해당 구문은 system 객체의 SCN을 상승시켜 클라이언트의 재접속을 유도한다.

해당 구문을 수행한 즉시 클라이언트가 재접속하는 것은 아니다. 클라이언트가 서버에 명령어를 실행할 때 SCN 비교를 통해서 재접속하며 만약 클라이언트에서 모든 멤버로의 연결이 유효하다면 재접속을 시도하지 않는다.

<a id="03ef695bbe51b0ca"></a>
### 사용 예

다음은 해당 구문을 수행하는 예이다.

```
gSQL> ALTER SYSTEM RECONNECT GLOBAL CONNECTION;

System altered.
```

<a id="4e3d726a95fda34b"></a>
### 호환성

SQL 표준에서는 GLOBAL CONNECTION의 개념을 정의하지 않고 있다.

<a id="93ce1895117db4b3"></a>
## ALTER SYSTEM RESET property_name

<a id="d7535787e67e0b13"></a>
### 기능

프로퍼티 파일에서 프로퍼티 값을 삭제한다.

<a id="7f6c98692a3c4bc1"></a>
### 구문

```
<alter system reset statement> ::=
    ALTER SYSTEM { RESET | UNSET } <property name>
        [ SCOPE = { FILE | SPFILE } ]
        [ AT <domain name>]
    ;
```

<a id="21b9ad212c054904"></a>
### 사용 범위 및 접근 권한

&lt;alter system reset statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="8afe3000cdc9f61e"></a>
### 구문 규칙 및 파라미터

<a id="43c6e5157338ef6d"></a>
#### { RESET | UNSET }

RESET과 UNSET은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다.

<a id="cce1f1a7a11ba889"></a>
#### &lt;property name&gt;

삭제할 프로퍼티의 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5debfb33dc9cdf97) 장을 참조한다.

<a id="12074be9bd5b4359"></a>
#### [ SCOPE = { FILE | SPFILE } ]

프로퍼티 파일에서 삭제하는 것이므로 SCOPE=FILE/SPFILE만 사용할 수 있다.

- SCOPE = FILE 
    - FILE과 SPFILE은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다. 
    - 프로퍼티를 FILE에서 삭제하고, 현재 상태에는 적용하지 않는다. 
    - Database를 재구동할 때 변경 사항을 적용한다.

SCOPE 절을 명시하지 않을 경우, 기본값은 SCOPE = FILE 이다.

<a id="46b1fb9567c335d3"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="3a244b747656141c"></a>
### 설명

SCOPE=FILE/SPFILE을 사용하여 프로퍼티를 변경했을 경우, 갱신된 값이 프로퍼티 파일에 저장되고 데이터베이스를 재시작할 때 반영된다.

RESET 할 경우, 프로퍼티 파일에 저장된 해당 갱신값을 파일에서 제거하고 데이터베이스를 재시작할 때 default 값을 사용하도록 한다.

<a id="61b72baf0259f85d"></a>
### 사용 예

다음은 SCOPE=FILE을 사용하여 프로퍼티를 변경하는 예이다.

```
gSQL> ALTER SYSTEM SET PROCESS_MAX_COUNT=128 SCOPE=FILE;

System altered.

gSQL> alter system set DEFAULT_INDEX_LOGGING=YES scope=FILE;

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

gSQL> ALTER SYSTEM RESET DEFAULT_INDEX_LOGGING;

System altered.

gSQL> ALTER SYSTEM UNSET DEFAULT_INDEX_LOGGING;

System altered.
```

<a id="e29a2cd11bb4889b"></a>
### 호환성

SQL 표준에서는 시스템 프로퍼티 개념을 정의하지 않고 있다.

<a id="2f05afe10040135b"></a>
### 참조

관련 내용은 [ALTER SYSTEM SET property_name](#6e2b8dbddba3fab3)을 참조한다.

<a id="6e2b8dbddba3fab3"></a>
## ALTER SYSTEM SET property_name

<a id="b820ea8d0ebd216f"></a>
### 기능

시스템의 프로퍼티 값을 설정한다.

<a id="01420db3fe4bfd1b"></a>
### 구문

```
<alter system set statement> ::=
    ALTER SYSTEM SET <property name> { = <property value> | TO DEFAULT }
        [ DEFERRED ]
        [ SCOPE = [ MEMORY | { FILE | SPFILE } | BOTH ] ]
    [AT <domain name>]
    ;
```

<a id="81613603e8f20332"></a>
### 사용 범위 및 접근 권한

&lt;alter system set statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="4ffac593889ff20f"></a>
### 구문 규칙 및 파라미터

<a id="bb51d14c1d3b430c"></a>
#### &lt;property name&gt;

설정할 프로퍼티의 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5debfb33dc9cdf97) 장을 참조한다.

<a id="143f176989722f9d"></a>
#### &lt;property value&gt;

설정할 프로퍼티의 값이다.

<a id="4ee4bc43e1c530f6"></a>
#### TO DEFAULT

시스템 프로퍼티 값을 시스템을 구동할 당시의 최초값으로 설정한다.

<a id="49c5e6992843c6f0"></a>
#### [ DEFERRED ]

변경된 프로퍼티를 적용할 시점을 정의한다.

- DEFERRED 
    - 현재 SESSION에는 영향을 주지 않고, 새로 생성되는 SESSION에 적용된다. 
    - 프로퍼티의 SYS_MODIFIABLE 속성값이 IMMEDIATE/ DEFERRED일 때 적용 가능하며, 반드시 명시해야 한다. 
    - 프로퍼티의 SYS_MODIFIABLE 속성값이 FALSE인 경우 사용할 수 없다.

프로퍼티의 SYS_MODIFIABLE 속성값이 IMMEDIATE일 경우, DEFERRED를 명시하지 않으면 모든 SESSION에 바로 적용된다.

<a id="13034b0b783ec536"></a>
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

<a id="1f056e20d90b2ce3"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="bb957073fbbf157c"></a>
### 설명

관련 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5debfb33dc9cdf97) 장을 참조한다.

<a id="27583313fb3287f8"></a>
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

<a id="339145fcbc1646b7"></a>
### 호환성

SQL 표준에서는 시스템의 프로퍼티 개념을 정의하지 않고 있다.

<a id="5507d7ede855a623"></a>
### 참조

관련 내용은 [ALTER SYSTEM RESET property_name](#93ce1895117db4b3)을 참조한다.

<a id="4153f6ebf956b981"></a>
## ALTER SYSTEM SWITCH LOGFILE

<a id="7372c4fd80f0deab"></a>
### 기능

데이터베이스 내에 있는 CURRENT 상태의 로그파일을 ACTIVE 상태로 변경한다.

<a id="0629c7446675c605"></a>
### 구문

```
<alter system switch logfile statement> ::=
    ALTER SYSTEM SWITCH LOGFILE
    [ AT <domain name> ]
    ;
```

<a id="f0d6cb09cb3759cb"></a>
### 사용 범위 및 접근 권한

&lt;alter system switch logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="1361f0eae83eaaea"></a>
### 구문 규칙 및 파라미터

<a id="6cf2b33d224b2aa9"></a>
#### &lt;alter system switch logfile statement&gt;

데이터베이스가 MOUNT 또는 OPEN 상태여야 한다.

<a id="450175a3481be547"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="efdc541322bc723b"></a>
### 설명

기본적으로 CURRENT 상태의 로그파일이 다 채워지면 자동으로 로그 스위치가 발생한다. 해당 구문은 특수한 상황에서 강제로 로그 스위치하고자 할 때 사용된다.

<a id="1698ed6b10807195"></a>
### 사용 예

```
ALTER SYSTEM SWITCH LOGFILE;
```

<a id="afe234b9f7b0ebfc"></a>
### 호환성

SQL 표준에서는 LOGFILE에 대한 개념을 정의하지 않고 있다.

<a id="92a63b70e59fd152"></a>
### 참조

관련 내용은 [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#f434c9481edc0db8)를 참조한다.

<a id="16da97b62af765de"></a>
## ALTER TABLE

<a id="ad7c966759281e02"></a>
### 기능

테이블 정의를 변경한다.

<a id="72047ba85ada4b63"></a>
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
    | <split shard statement>
    | <rename shard statement>
    | <read { only | write } statement>
    ;
```

<a id="36c312415a314d98"></a>
### 사용 범위 및 접근 권한

&lt;alter table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="c0a8324f9072607b"></a>
### 구문 규칙 및 파라미터

<a id="8345805ba45b88b8"></a>
#### &lt;alter table physical attribute statement&gt;

테이블의 물리적 속성을 변경한다.  
자세한 내용은 [ALTER TABLE name STORAGE](#f353d2d59cd40842) 구문을 참조한다.

<a id="7ec66e4983a436ea"></a>
#### &lt;rename table statement&gt;

테이블 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME TO](#5b91380c8925c3a4) 구문을 참조한다.

<a id="9634c07723c26d7a"></a>
#### &lt;add column definition&gt;

테이블에 column을 추가한다.  
자세한 내용은 [ALTER TABLE name ADD COLUMN](#c42e27e734cc5c56) 구문을 참조한다.

<a id="766a5047a5b0ffbc"></a>
#### &lt;drop column definition&gt;

테이블에서 column을 삭제한다.  
자세한 내용은 [ALTER TABLE name SET UNUSED COLUMN](#f310a3fb90803c42) 구문을 참조한다.

<a id="dacee7e6eb0b0240"></a>
#### &lt;alter column definition&gt;

테이블 column의 정의를 변경한다.  
자세한 내용은 [ALTER TABLE name ALTER COLUMN](#7b1c675bb7a0aac7) 구문을 참조한다.

<a id="4d4b5c11bf71bf26"></a>
#### &lt;rename column statement&gt;

테이블 column의 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME COLUMN](#5759cb33f6666307) 구문을 참조한다.

<a id="9be3ed418c757dad"></a>
#### &lt;add table constraint definition&gt;

테이블에 제약 조건을 추가한다.  
자세한 내용은 [ALTER TABLE name ADD CONSTRAINT](#8c53ce7b8253f264) 구문을 참조한다.

<a id="6c6e01886eb8587c"></a>
#### &lt;drop table constraint definition&gt;

테이블 제약 조건을 삭제한다.  
자세한 내용은 [ALTER TABLE name DROP CONSTRAINT](#bf6cc14c07dc84dc) 구문을 참조한다.

<a id="907fb3dcb16e2a54"></a>
#### &lt;alter table constraint definition&gt;

테이블의 제약 조건을 변경한다.  
자세한 내용은 [ALTER TABLE name ALTER CONSTRAINT](#0fd66f8da1d1d087) 구문을 참조한다.

<a id="59f616d2633aa95a"></a>
#### &lt;rename table constraint statement&gt;

테이블 제약 조건의 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME CONSTRAINT](#eea8cc70d72eed91) 구문을 참조한다.

<a id="26289f766e390c13"></a>
#### &lt;add table supplemental log statement&gt;

테이블의 데이터가 변경되면 redo log에 부가 정보를 추가하도록 설정한다.  
자세한 내용은 [ALTER TABLE name ADD SUPPLEMENTAL LOG](#e2cd4b70ceeae92d) 구문을 참조한다.

<a id="e3482905cafb8e75"></a>
#### &lt;drop table supplemental log statement&gt;

테이블의 데이터가 변경되면 redo log에 부가 정보를 추가하지 않도록 설정한다.  
자세한 내용은 [ALTER TABLE name DROP SUPPLEMENTAL LOG](#8308658a684ec98a) 구문을 참조한다.

<a id="247d2827f109ee40"></a>
#### &lt;rebalance statement&gt;

Cluster 환경에서 테이블의 shard를 재배치하거나 정합성이 깨진 shard를 동기화하여 정합성을 복구한다.  
자세한 내용은 [ALTER TABLE REBALANCE](#9a20bc4c3fbf08ef) 구문을 참조한다.

<a id="6a04fea477589bd6"></a>
#### &lt;move shard statement&gt;

Cluster 환경에서 테이블의 특정 shard를 특정 cluster group에 재배치한다.  
자세한 내용은 [ALTER TABLE MOVE SHARD](#ba4cbd044acbe360) 구문을 참조한다.

<a id="430c8050ef91fbed"></a>
#### &lt;split shard statement&gt;

Cluster 환경에서 테이블의 특정 shard를 분산하여 특정 cluster group에 재배치한다.  
자세한 내용은 [ALTER TABLE SPLIT SHARD](#9e3df57fd520ef65) 구문을 참조한다.

<a id="26bd1b9c8f3dab76"></a>
#### &lt;rename shard statement&gt;

Cluster 환경에서 테이블의 특정 shard 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME SHARD](#a2da1b506cc85d50) 구문을 참조한다.

<a id="6326cb7682486ee0"></a>
#### &lt;read { only | write } statement&gt;

테이블에 READ ( only | write }을 설정한다.  
자세한 내용은 [ALTER TABLE name READ { ONLY | WRITE }](#0e36db5fd37b58b3) 구문을 참조한다.

<a id="839cee960ee2c079"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="2018f4f6812a0eb7"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="1b6a0cfeab64c04c"></a>
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

<a id="c42e27e734cc5c56"></a>
## ALTER TABLE name ADD COLUMN

<a id="5130e350094cedd6"></a>
### 기능

테이블에 column을 추가한다.

<a id="fc2670d0f2c5ac44"></a>
### 구문

```
<add column definition> ::=
      ALTER TABLE table_name ADD [ COLUMN ] <column definition>
    | ALTER TABLE table_name ADD [ COLUMN ] ( <column definition> [, ...] )
    ;
```

<a id="b8e5b3ada630635e"></a>
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

<a id="f92819ed150de9a5"></a>
### 구문 규칙 및 파라미터

<a id="7d902f1f93a45ca1"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="653521496c388677"></a>
#### ADD [ COLUMN ]

COLUMN 예약어는 생략할 수 있다.

<a id="23a3e8fefb1e1e49"></a>
#### &lt;column definition&gt;

추가할 column을 정의한다.  
자세한 내용은 [CREATE TABLE](#1586c5952309fa38) 구문의 &lt;[column definition&gt;](#69910076524eddf1) 절을 참조한다.  
테이블 내에 동일한 column 이름이 존재하지 않아야 한다.

Column을 정의할 때 DEFAULT 절을 명시할 경우, 모든 row의 기본값을 추가되는 column에 저장한다.  
Column을 정의할 때 &lt;identity column specification&gt; 절을 명시한 경우, 모든 row 각각의 자동 생성값을 추가되는 column에 저장한다.  
Column을 정의할 때 NOT NULL 제약 조건을 함께 명시한 경우, 테이블을 비우거나 DEFALUT 절 또는 &lt;identity column specification&gt; 절을 함께 기술해야 한다.

<a id="dbd58f66be951873"></a>
#### ( &lt;column definition&gt; [, ...] )

다수의 column을 추가한다.  
괄호 내부에 다수의 &lt;column definition&gt;을 나열한다.

<a id="f4dd914e848ca274"></a>
### 설명

추가되는 column은 기존 column들의 뒤에 위치한다.  
DEFAULT 절이나 &lt;identity column specification&gt;을 명시한 경우, 수행시간은 테이블에 존재하는 row의 개수에 비례하여 증가한다.

<a id="b4e80f24cd7e9c99"></a>
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

<a id="df474de59cc5bd74"></a>
### 호환성

SQL 표준에서는 다수의 column definition 추가에 대해 정의하지 않고 있다.

<a id="8dd9deb1f6c8d869"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#16da97b62af765de)
- [ALTER TABLE name SET UNUSED COLUMN](#f310a3fb90803c42)
- [ALTER TABLE name ALTER COLUMN](#7b1c675bb7a0aac7)
- [ALTER TABLE name RENAME COLUMN](#5759cb33f6666307)

<a id="f310a3fb90803c42"></a>
## ALTER TABLE name SET UNUSED COLUMN

<a id="ea6b2196b10e3a9c"></a>
### 기능

테이블 column을 제거한다.

<a id="89d7f881d3e98c5c"></a>
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

<a id="cfc6110d8541790f"></a>
### 사용 범위 및 접근 권한

&lt;drop column definition&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="0fe6675c70e6a281"></a>
### 구문 규칙 및 파라미터

<a id="0db6dbd5b097020b"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="63632c6ba052b488"></a>
#### SET UNUSED [ COLUMN ]

해당 column들을 사용하지 않도록 설정한다.

<a id="2c54d0ded981ed0b"></a>
#### column_name_list

한 개 이상의 삭제될 column 이름이다.

- 예: ALTER TABLE t1 SET UNUSED COLUMN c1 
- 예: ALTER TABLE t1 SET UNUSED COLUMN (c1, c2)

<a id="3060c8feb77feafb"></a>
#### column_name

삭제할 column의 이름이다.  
해당 column을 이용하는 제약 조건과 인덱스도 함께 삭제한다.

<a id="acc9516dc6e0eaeb"></a>
#### drop behavior

생략할 경우, 기본값은 RESTRICT 이다.  
현재는 RESTRICT/ CASCADE가 동일하게 작동한다.

<a id="fa116079574eb57c"></a>
### 설명

SET UNUSED COLUMN은 data를 물리적으로 제거하지 않으므로 row의 개수에 관계없이 일정한 성능을 보장한다.

<a id="27fd17c8a0b1364a"></a>
### 사용 예

다음은 해당 column을 사용하지 않도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 SET UNUSED COLUMN ( addr );

Table altered.
```

<a id="514b0ca3dda06930"></a>
### 호환성

SQL 표준에서는 다음과 같은 절들을 정의하지 않고 있다.

- SET UNUSED 
- CASCADE CONSTRAINTS 
- 다수의 column 나열

**SQL 표준 호환성**

<a id="51365844ad7b0074"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F033 | ALTER TABLE statement: DROP COLUMN clause | X |

<a id="66ac3b4b228a73cb"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#16da97b62af765de)
- [ALTER TABLE name ADD COLUMN](#c42e27e734cc5c56)
- [ALTER TABLE name ALTER COLUMN](#7b1c675bb7a0aac7)
- [ALTER TABLE name RENAME COLUMN](#5759cb33f6666307)

<a id="7b1c675bb7a0aac7"></a>
## ALTER TABLE name ALTER COLUMN

<a id="d6a50b9162217265"></a>
### 기능

Column의 정의를 변경한다.

<a id="aeeadf17bb12f257"></a>
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

<a id="b738c03730bc28df"></a>
### 사용 범위 및 접근 권한

&lt;alter column definition&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="2afdd4a4217fbe4a"></a>
### 구문 규칙 및 파라미터

<a id="f5ef953a6eefd10b"></a>
#### table_name

변경할 테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="c3604b67da19c6b2"></a>
#### ALTER [ COLUMN ]

COLUMN 예약어는 생략할 수 있다.

<a id="ca7c9cf1907f696e"></a>
#### column_name

변경할 column의 이름이다.

<a id="6e5a49024d24c8f8"></a>
#### &lt;set column default clause&gt;

Column의 기본값을 설정한다.  
identity column이 아니어야 한다.

이후에 수행되는 INSERT 구문 등에서 DEFAULT 절을 사용할 경우 설정된 기본값이 사용된다.

DEFAULT expression의 데이터 타입은 column의 데이터 타입과 호환 가능해야 한다.  
타입이 호환되지 않거나 공간이 부족한 경우 INSERT, UPDATE 구문에서 DEFAULT를 사용할 때 에러가 발생한다.

자세한 설명은 [CREATE TABLE](#1586c5952309fa38) 구문의 &lt;[default clause&gt;](#7d047626d6bea974) 절을 참조한다.

<a id="6cf3236b328c49c6"></a>
#### &lt;drop column default clause&gt;

Column의 기본값을 제거한다.  
identity column이 아니어야 한다.  
기본값을 제거하면 INSERT 구문 등에서 DEFAULT 절을 사용할 때 NULL 값으로 설정된다.

<a id="b413b99447ea552d"></a>
#### &lt;set column not null clause&gt;

- SET [CONSTRAINT constraint_name] NOT NULL [ &lt;constraint characteristics&gt; ]
    - Column에 NOT NULL 제약 조건을 설정한다.
    - Column의 값으로 NULL 값을 허용하지 않는다.
    - 해당 column에 NULL 값이 존재하지 않아야 한다.

- [CONSTRAINT constraint_name]을 생략할 경우 자동으로 제약 조건 이름을 부여한다.
- &lt;constraint characteristics&gt;를 생략할 경우, NOT DEFERRABLE INITIALLY IMMEDIATE 속성을 갖는다.
- identity column은 DEFERRABLE 속성을 가질 수 없다.

지연 가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](#8e1fec980aea373d) 구문의 설명을 참조한다.

<a id="34c83d7388aa4fef"></a>
#### &lt;drop column not null clause&gt;

- DROP NOT NULL
    - Column의 NOT NULL 제약 조건을 제거한다.

<a id="76fd82a3da886b7c"></a>
#### &lt;alter column data type clause&gt;

- SET DATA TYPE &lt;data type&gt;
    - Column의 데이터 타입을 변경한다.

> SET DATA TYPE 구문은 자동으로 commit 되는 DDL 구문이다.

동일한 계열간에 타입을 변경할 수 있는데 이 때 다음 조건을 만족해야 한다.

**character string type 변환**

<a id="cc41d87d8f33f40d"></a>
| from \ to | CHAR(n) | VARHCAR(n) | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR(m) | X | X | X |
| VARCHAR(m) | X | n >= m | X |
| LONG VARCHAR | X | X | O |

char length unit을 변경할 경우 다음과 같은 조건을 만족해야 한다.

**character length unit 변환**

<a id="b51f4a5a8ce3a723"></a>
| from \ to | OCTETS | CHARACTERS |
| --- | --- | --- |
| OCTETS | O | O |
| CHARACTERS | X | O |

**binary string type 변환**

<a id="c5539781700c979b"></a>
| from \ to | BINARY(n) | VARBINARY(n) | LONG VARBINARY |
| --- | --- | --- | --- |
| BINARY(m) | X | X | X |
| VARBINARY(m) | X | n >= m | X |
| LONG VARBINARY | X | X | O |

**numeric type**

<a id="19eaaf7819e6bd16"></a>
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

<a id="f253ec06beabb445"></a>
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

**Numeric type들의 NUMBER 표현식**

<a id="ae32224a0523fd0d"></a>
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

<a id="98124f4dd693918a"></a>
| from \ to | NATIVE_SMALLINT | NATIVE_INTEGER | NATIVE_BIGINT | NATIVE_REAL | NATIVE_DOUBLE |
| --- | --- | --- | --- | --- | --- |
| NATIVE_SMALLINT | O | X | X | X | X |
| NATIVE_INTEGER | X | O | X | X | X |
| NATIVE_BIGINT | X | X | O | X | X |
| NATIVE_REAL | X | X | X | O | X |
| NATIVE_DOUBLE | X | X | X | X | O |

**Boolean type의 변환**

<a id="f835c93eac056d10"></a>
| from \ to | BOOLEAN |
| --- | --- |
| BOOLEAN | O |

**Date/ time type의 변환 (TZ: WITH TIME ZONE)**

<a id="2d376d41f0d34795"></a>
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

<a id="39f2df464f612fbf"></a>
| from \ to | YEAR(q) | MONTH(q) | YEAR(q) TO MONTH |
| --- | --- | --- | --- |
| YEAR(p) | q >= p | X | X |
| MONTH(p) | X | q >= p | X |
| YEAR(p) TO MONTH | X | X | q >= p |

**INTERVAL DAY TO TIME 계열의 type 변환 (p,q 가 생략된 경우 2) (f,g 가 생략된 경우 6)**

<a id="bf1443db76568e0b"></a>
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

<a id="7b3b15ff8206c395"></a>
| from \ to | ROWID |
| --- | --- |
| ROWID | O |

<a id="223a70c52c3bec13"></a>
#### &lt;alter identity column specification&gt;

Column의 identity 속성을 변경한다.  
Column은 identity column 이어야 한다.

- SET GENERATED [ ALWAYS | BY DEFAULT ]
    - identity column의 생성 방식을 변경한다. 
    - 자세한 내용은 [CREATE TABLE](#1586c5952309fa38) 구문의 &lt;[identity column specification&gt;](#ac322431fea8d204)을 참조한다. 
- &lt;alter sequence generator restart option&gt; 
    - identity column의 다음 값 (NEXT VALUE)을 변경한다. 
    - 자세한 내용은 [ALTER SEQUENCE](#9fd8a84df33183e1) 구문의 &lt;[alter sequence generator restart option&gt;](#64e81a28377c756f) 절을 참조한다. 
- &lt;basic sequence generator option&gt; 
    - identity column의 속성을 변경한다. 
    - SQL 표준에서는 SET &lt;basic sequence generator option&gt;의 형태로 기술하도록 정의하고 있으나 생략 가능하다. 
    - 자세한 내용은 [ALTER SEQUENCE](#9fd8a84df33183e1) 구문을 참조한다.

<a id="dfaee58d4f98f4f2"></a>
#### &lt;drop identity property clause&gt;

Column의 identity 속성을 제거한다.  
Column은 identity column 이어야 한다.

<a id="15827fbab309c203"></a>
### 설명

SET NOT NULL 절의 null 검사 수행시간은 테이블의 row 개수에 비례한다.

다음과 같은 column은 NULL 값을 허용하지 않는다. 즉, DROP NOT NULL 절을 수행하더라도 다음 조건 중 하나를 만족할 경우 NULL 값을 허용하지 않는다.

- NOT NULL 제약 조건이 있는 column
- Column이 primary key 제약 조건에 포함되는 경우
- Column이 identity column인 경우

SET DEFAULT 절을 이용한 기본값 변경과 &lt;alter identity column specification&gt; 절을 이용한 identity 속성의 변경은 이후에 수행되는 INSERT 또는 UPDATE 구문에 적용된다.

<a id="fd11aab729843272"></a>
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

<a id="15c575375c0f0ad9"></a>
### 호환성

**SQL 표준 호환성**

<a id="44afc846862fd29b"></a>
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

<a id="46f41e7cb0bdfae5"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#16da97b62af765de)
- [ALTER TABLE name ADD COLUMN](#c42e27e734cc5c56)
- [ALTER TABLE name SET UNUSED COLUMN](#f310a3fb90803c42)
- [ALTER TABLE name RENAME COLUMN](#5759cb33f6666307)

<a id="5759cb33f6666307"></a>
## ALTER TABLE name RENAME COLUMN

<a id="8eb303e747436ad4"></a>
### 기능

테이블 column의 이름을 변경한다.

<a id="fbc37c3fa9b8479c"></a>
### 구문

```
<rename column statement> ::=
    ALTER TABLE table_name 
        RENAME COLUMN old_column_name TO new_column_name
    ;
```

<a id="95442b265209fbf0"></a>
### 사용 범위 및 접근 권한

&lt;rename column statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="75f333979a19fb2b"></a>
### 구문 규칙 및 파라미터

<a id="1978fad51c5163e1"></a>
#### table_name

변경할 테이블 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="2bc605b5fa62991b"></a>
#### old_column_name

변경할 column의 기존 이름이다.

<a id="02caf286a1fb2f69"></a>
#### new_column_name

변경할 column의 새로운 이름이다.  
테이블 내에 동일한 column 이름이 존재하지 않아야 한다.

<a id="5d63973876ec6302"></a>
### 설명

Column 이름이 변경되더라도 이전에 해당 column을 기준으로 생성된 index, constraint 등의 객체를 변경할 필요는 없다.

<a id="971922da0d573610"></a>
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

<a id="aba799142c741df5"></a>
### 호환성

SQL 표준에서는 &lt;rename column statement&gt; 구문을 정의하지 않고 있다.

<a id="48516d0b5e8911f5"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#16da97b62af765de)
- [ALTER TABLE name ADD COLUMN](#c42e27e734cc5c56)
- [ALTER TABLE name SET UNUSED COLUMN](#f310a3fb90803c42)
- [ALTER TABLE name ALTER COLUMN](#7b1c675bb7a0aac7)

<a id="8c53ce7b8253f264"></a>
## ALTER TABLE name ADD CONSTRAINT

<a id="9edd0259308635cf"></a>
### 기능

테이블 제약 조건을 추가한다.

<a id="725e3544cabbecef"></a>
### 구문

```
<add table constraint definition> ::=
    ALTER TABLE table_name 
        ADD <table constraint definition>
    ;
```

<a id="6da20de9174c08a1"></a>
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

<a id="d39221f127fa7188"></a>
### 구문 규칙 및 파라미터

<a id="985562b201902ff8"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="4e5900ab9b3a9bc6"></a>
#### &lt;table constraint definition&gt;

추가할 제약 조건을 정의한다.  
NOT NULL 제약 조건은 ALTER TABLE .. ADD CONSTRAINT 구문으로 추가할 수 없으며, 다음 예와 같이 [ALTER TABLE name ALTER COLUMN](#7b1c675bb7a0aac7) 구문을 이용해 정의할 수 있다.

```
ALTER TABLE t1 ALTER COLUMN c1 SET NOT NULL;
```

자세한 내용은 [CREATE TABLE](#1586c5952309fa38) 구문의 &lt;[table constraint definition&gt;](#8faec2bdf9d76b72) 절을 참조한다.

<a id="ad4cd2e5d05dc0bb"></a>
### 설명

Primary key, unique key와 같은 key 제약을 추가할 때 이를 위한 index가 자동으로 생성된다.

<a id="d76f033d50d93e35"></a>
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

다음은 지연 가능한 제약 조건을 추가하는 예이다.

```
gSQL> ALTER TABLE t1 ADD CONSTRAINT t1_uk UNIQUE ( id ) DEFERRABLE INITIALLY DEFERRED;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="0e262b10f21d4712"></a>
### 호환성

**SQL 표준 호환성**

<a id="5731801c4e8e0783"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="27a7d3f3590e69aa"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](#1586c5952309fa38)
- [CREATE INDEX](#ce4afb58f69a16f7)
- [ALTER TABLE](#16da97b62af765de)
- [ALTER TABLE name DROP CONSTRAINT](#bf6cc14c07dc84dc)

<a id="bf6cc14c07dc84dc"></a>
## ALTER TABLE name DROP CONSTRAINT

<a id="0aaf8ecc724b68fd"></a>
### 기능

테이블 제약 조건을 제거한다.

<a id="fb738cda4e958287"></a>
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

<a id="aa2a235f9bfc9191"></a>
### 사용 범위 및 접근 권한

&lt;drop table constraint definition&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 제약 조건의 소유자 
- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="ff766d090f64bf9c"></a>
### 구문 규칙 및 파라미터

<a id="ee064e0e9a2b1d95"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="5caec26ffbbe7709"></a>
#### CONSTRAINT constraint_name

제거할 제약 조건의 이름이다.

<a id="59f7ca0945dc41c4"></a>
#### PRIMARY KEY

테이블의 primary key 제약 조건이다.

<a id="fe774e3c26a19588"></a>
#### UNIQUE( column_name [, ...] )

Column들에 대한 unique 제약 조건이다.

<a id="3f21e665e7b1cf5a"></a>
#### &lt;drop behavior&gt;

생략할 경우, 기본값은 RESTRICT 이다.  
현재는 RESTRICT/ CASCADE가 동일하게 작동한다.

<a id="266c6342bf55ef52"></a>
### 설명

제약 조건의 이름을 사용하지 않고 NOT NULL 제약 조건을 제거하려고 할 경우 [ALTER TABLE name ALTER COLUMN](#7b1c675bb7a0aac7) 구문의 &lt;[drop column not null clause&gt;](#34c83d7388aa4fef) 절을 이용한다.

<a id="286fe84e086990d7"></a>
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

<a id="1b548942a6597e70"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- DROP PRIMARY KEY 
- DROP UNIQUE ( column_name [, ...] ) 
- CASCADE CONSTRAINTS

**SQL 표준 호환성**

<a id="7fbe40cea0eb1eac"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="69ebed7616ae7e30"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#16da97b62af765de)
- [ALTER TABLE name ADD CONSTRAINT](#8c53ce7b8253f264)
- [DROP INDEX](#93a6d0dc40b79b2e)

<a id="0fd66f8da1d1d087"></a>
## ALTER TABLE name ALTER CONSTRAINT

<a id="88263779152685bb"></a>
### 기능

테이블 제약 조건의 특성을 변경한다.

<a id="1d2989ca58e01b1b"></a>
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

<a id="c3370dc6b93e1e5c"></a>
### 사용 범위 및 접근 권한

&lt;alter table constraint definition&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

> Cluster는 지연 가능한 제약 조건을 지원하지 않는다.

<a id="572258edb892bd77"></a>
### 구문 규칙 및 파라미터

<a id="aa6ea83ebc62233e"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="bfadee41ef95a361"></a>
#### &lt;constraint object&gt;

변경할 제약 조건은 다음과 같이 지정할 수 있다.

- CONSTRAINT constraint_name
    - 변경할 제약 조건의 이름이다.
- PRIMARY KEY 
    - 테이블의 PRIMARY KEY 제약 조건이다.
- UNIQUE( column [,...] ) 
    - Column 목록에 부합되는 UNIQUE 제약 조건이다.

<a id="23fae387c3ee5439"></a>
#### DEFERRABLE | NOT DEFERRABLE

제약 조건의 지연 가능 여부를 변경한다.

- DEFERRABLE
    - 제약 조건을 지연가능하도록 변경한다. 
- NOT DEFERRABLE 
    - 제약 조건을 지연가능하지 않도록 변경한다.

<a id="32ea07b0ca6e9112"></a>
#### INITIALLY IMMEDIATE | INITIALLY DEFERRED

제약 조건의 검사시점 초기값을 변경한다.

- INITIALLY IMMEDIATE 
    - DML을 수행할 때 제약 조건을 검사한다.
- INITIALLY DEFERRED 
    - COMMIT을 수행할 때 제약 조건을 검사한다.

NOT DEFERRABLE로 정의된 제약 조건은 INITIALLY DEFERRED로 변경할 수 없다.

<a id="f29ecdb894046397"></a>
### 설명

지연가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](#8e1fec980aea373d) 구문을 참조한다.

<a id="c50a02095c869f93"></a>
### 사용 예

다음은 t1_uk 제약 조건을 지연가능하게 하고 검사시점을 DEFERRED로 설정하는 예이다.

```
gSQL> ALTER TABLE t1 ALTER CONSTRAINT t1_uk DEFERRABLE INITIALLY DEFERRED;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="3dcbca8e4e9ca988"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- ALTER PRIMARY KEY 절
- ALTER UNIQUE(column [,...]) 절

**SQL 표준 호환성**

<a id="2b6310ceaa2270cf"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F492 | Optional table constraint enforcement | X |

<a id="eea8cc70d72eed91"></a>
## ALTER TABLE name RENAME CONSTRAINT

<a id="63ba194a19ac44d4"></a>
### 기능

테이블 제약 조건의 이름을 변경한다.

<a id="c58df75eb0b0b37a"></a>
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

<a id="5d763879c13ae685"></a>
### 사용 범위 및 접근 권한

&lt;rename table constraint statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="8425f019dbafc126"></a>
### 구문 규칙 및 파라미터

<a id="1832c2e6bcbfabb7"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="5ee343006fd35405"></a>
#### &lt;constraint object&gt;

변경할 제약 조건의 기존 이름은 다음과 같이 지정할 수 있다.

- CONSTRAINT constraint_name
    - 변경할 제약 조건의 이름이다.
- PRIMARY KEY
    - 테이블의 PRIMARY KEY 제약 조건이다.
- UNIQUE( column [,...] )
    - Column 목록에 부합되는 UNIQUE 제약 조건이다.

<a id="8ab5c2c8bf5c45f1"></a>
#### new_column_name

변경할 제약 조건의 새로운 이름이다.

<a id="b9b49b5b69796551"></a>
### 설명

Primary key, unique key와 같이 key 제약 조건으로 자동 생성된 index의 이름은 변경되지 않는다. Index 이름은 [ALTER INDEX name RENAME TO](#816edfcde4e7f3c5) 구문을 사용하여 변경해야 한다.

<a id="eecad1243e33e566"></a>
### 사용 예

다음은 테이블의 primary key 제약 조건 이름을 변경하는 예이다.

```
gSQL> ALTER TABLE t1 RENAME PRIMARY KEY TO pk_t1;

Table altered.
```

다음은 제약 조건 이름을 명시하여 테이블의 제약 조건 이름을 변경하는 예이다.

```
gSQL> ALTER TABLE t1 RENAME CONSTRAINT pk_t1 TO t1_pk;

Table altered.
```

<a id="64cfb7c76b0d45b2"></a>
### 호환성

SQL 표준에서는 &lt;rename table constraint statement&gt; 구문을 정의하지 않고 있다.

<a id="0214b688d9869bcb"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#16da97b62af765de)
- [ALTER TABLE name ADD CONSTRAINT](#8c53ce7b8253f264)
- [ALTER TABLE name DROP CONSTRAINT](#bf6cc14c07dc84dc)
- [ALTER TABLE name ALTER CONSTRAINT](#0fd66f8da1d1d087)

<a id="734ad801c6d6f26f"></a>
## ALTER TABLE name ADD GLOBAL SECONDARY INDEX

<a id="50746bc77758c113"></a>
### 기능

테이블에 global secondary index를 생성한다.

<a id="8332786213c62b5d"></a>
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
    | <logging clause> 
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

<logging clause> ::=
      LOGGING
    | NOLOGGING

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="922f2a4b866246f1"></a>
### 사용 범위 및 접근 권한

&lt;alter table add global secondary index definition&gt; 구문은 cluster system에서 정의할 수 있으며 사용자는 다음 조건들을 만족해야 한다.

- 인덱스를 생성할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 인덱스가 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE
    - USAGE TABLESPACE ON DATABASE

<a id="7b117261c3b30cb2"></a>
### 구문 규칙 및 파라미터

<a id="2afc58bb2c8188bf"></a>
#### table_name

인덱스를 생성할 테이블 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="d2419a12aeda4b30"></a>
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

<a id="38232940e01e6448"></a>
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

<a id="df7d0f43a4ed923a"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="1bdcace0c5b9945c"></a>
#### LOGGING | NOLOGGING

인덱스의 리두 로깅 여부를 명시한다.  
명시하지 않을 경우, 기본값은 NOLOGGING 이다.

<a id="6672a6ed86f28665"></a>
#### NOPARALLEL | PARALLEL [ integer ]

인덱스 구축과정에 사용될 thread의 개수를 지정한다.

- NOPARALLEL 
    - 병렬로 인덱스를 구축하지 않는다. 
- PARALLEL [integer] 
    - 병렬로 인덱스를 구축한다. 
    - integer가 생략되거나 0으로 지정된 경우에는 프로퍼티 (INDEX_BUILD_PARALLEL_FACTOR)를 따른다. 
    - integer는 0부터 사용할 수 있으며 최대값은 16이다. 
    - 만약 프로퍼티의 값이 0인 경우에는 최적값을 시스템이 결정한다.
- 명시하지 않을 경우, 기본값은 PARALLEL이다.

<a id="5cf380611b28475e"></a>
#### TABLESPACE tablespace_name

인덱스가 저장될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - LOGGING 인덱스의 tablespace_name은 data tablespace여야 하며 
    - NOLOGGING 인덱스의 tablespace_name은 temporary tablespace 또는 nologging tablespace여야 한다.

- TABLESPACE 절을 생략할 경우,
    - USER의 INDEX TABLESPACE tablespace_name을 지정한 경우
        - 정의한 테이블스페이스를 사용한다.
    - USER의 INDEX TABLESPACE가 NULL인 경우
        - LOGGING 인덱스는 사용자의 기본 데이터 테이블스페이스를 사용하고,
        - NOLOGGING 인덱스는 사용자의 기본 임시 테이블스페이스를 사용한다.

<a id="262bef53d74c78de"></a>
### 설명

Non-deterministic 질의에는 global secondary index가 반드시 필요하다. LOGGING 인덱스와 NOLOGGING 인덱스에는 다음과 같은 trade-off가 있다.

- LOGGING 인덱스
    - 장점: 시스템을 구동할 때 로그를 이용해 인덱스가 자동으로 복구되므로 별도의 구축과정이 없다.
    - 단점: 관련 row를 변경할 때 인덱스 변경 내용을 로그로 기록하여 디스크 IO를 유발한다.
- NOLOGGING 인덱스
    - 장점: 관련 row를 변경할 때 인덱스 변경 내용에 대해 디스크 IO가 발생하지 않는다.
    - 단점: 시스템을 구동할 때 인덱스에 대한 로그 정보가 없어 자동으로 인덱스를 재구축한다.

<a id="12c3cd6b75e946f6"></a>
### 사용 예

다음은 테이블 T1에 global secondary index를 추가하는 예이다.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX;

Table altered.

gSQL> COMMIT;

Commit complete.
```

다음은 logging option으로 테이블 T1의 tablespace USER_DATA_TBS에 global secondary index를 생성하는 예이다.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX LOGGING TABLESPACE USER_DATA_TBS;

Table altered.

gSQL> COMMIT;

Commit complete.
```

다음은 nologging option으로 테이블 T1의 tablespace USER_TEMP_TBS에 global secondary index를 생성하는 예이다.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX NOLOGGING TABLESPACE USER_TEMP_TBS;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="4019daef166061f5"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="c243d16365d57baf"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#1529aa64cdd3a71c)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#ce20ba70a79ed6ee)
- [CREATE TABLE](#1586c5952309fa38)

<a id="1529aa64cdd3a71c"></a>
## ALTER TABLE name DROP GLOBAL SECONDARY INDEX

<a id="f51eee6569d81f22"></a>
### 기능

테이블에서 global secondary index를 제거한다.

<a id="e6b14fdd93897a0b"></a>
### 구문

```
<alter table drop global secondary index definition> ::=
    ALTER TABLE table_name 
        DROP GLOBAL SECONDARY INDEX
    ;
```

<a id="02a02bb4f59fbd16"></a>
### 사용 범위 및 접근 권한

&lt;alter table drop global secondary index definition&gt; 구문은 cluster system에서 정의할 수 있으며 사용자는 다음 조건들을 만족해야 한다.

- 인덱스를 제거할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

<a id="0ffe5fe4f90b75d7"></a>
### 구문 규칙 및 파라미터

<a id="d19498e82225d934"></a>
#### table_name

인덱스를 제거할 테이블 이름이다.

<a id="4bd0684e283c79db"></a>
### 설명

Non-deterministic 질의를 하려면 global secondary index가 반드시 필요하다.

<a id="ff4a566f153e5f2a"></a>
### 사용 예

테이블 T1에서 global secondary index를 제거한다.

```
gSQL> ALTER TABLE T1 DROP GLOBAL SECONDARY INDEX;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="1376e86bfe24a5f5"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="adcc4616c39367ba"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#734ad801c6d6f26f)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#ce20ba70a79ed6ee)

<a id="ce20ba70a79ed6ee"></a>
## ALTER TABLE name ALTER GLOBAL SECONDARY INDEX

<a id="dec173be29582d08"></a>
### 기능

테이블에서 global secondary index의 물리적 속성을 변경한다.

<a id="b0b23e92e57429fb"></a>
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

<a id="f7446aab8cba1ee1"></a>
### 사용 범위 및 접근 권한

&lt;alter table alter global secondary index storage statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="27ea56e1fbad0255"></a>
### 구문 규칙 및 파라미터

<a id="3926ee29bc54dcf2"></a>
#### table_name

인덱스를 생성할 테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="4f529b0d2f549986"></a>
#### &lt;physical attribute clause&gt;

인덱스의 물리적 속성 정보를 정의한다.

- PCTFREE integer 
    - 정의 
        - 페이지 내 key 삽입으로 인한 페이지 분할 빈도를 조절하기 위해 예약된 공간이다.
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

<a id="379b1d15afc8f055"></a>
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
    - 생략할 경우, 기본값은 EXTENT 두개 크기이다.

- MAXSIZE integer
    - 정의
        - 인덱스에서 할당받을 수 있는 최대 공간의 크기이다.
        - 이 값은 MINSIZE의 값과 같거나 커야 한다.
    - 이 크기는 인덱스가 속하는 TABLESPACE의 EXTENT 크기에 align 되어 사용된다.
    - 최소값은 1이고 최대값은 시스템 환경에 따라 다르다.
    - 생략할 경우, 기본값은 EXTENT 크기 * 2147483647 (INT32의 최대 양의 정수)이다.

<a id="296280d3e23e5c0f"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="fe5bc6dd064db7a0"></a>
### 설명

Non-deterministic 질의를 하려면 global secondary index가 반드시 필요하다.

<a id="4f1346388414b651"></a>
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

<a id="d4371473cb4e977c"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="925e902d8e16a720"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#734ad801c6d6f26f)
- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#1529aa64cdd3a71c)

<a id="ba4cbd044acbe360"></a>
## ALTER TABLE name MOVE SHARD

<a id="cb047d9228ca0687"></a>
### 기능

테이블의 특정 shard 또는 특정 cluster group의 전체 shard를 특정 cluster group에 재배치한다.

<a id="5c935553cd1369b7"></a>
### 구문

```
<alter table move shard statement> ::=
    ALTER TABLE table_name MOVE SHARD
        { shard_name_list | FROM CLUSTER GROUP src_cluster_group }
        TO CLUSTER GROUP dest_cluster_group [ ONLINE | OFFLINE ]
    ;
```

<a id="c4a2871c547d8d17"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table move shard statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="bd5bad443eecd00c"></a>
### 구문 규칙 및 파라미터

<a id="dfd129b4f9dc2994"></a>
#### table_name

테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
해당 테이블이 cluster group specific인 경우에만 구문을 수행할 수 있다.

<a id="d8ed34bcd12a9193"></a>
#### shard_name_list

재배치할 shard name 목록이다.  
해당 테이블에 존재하지 않는 shard인 경우 구문을 수행할 수 없다.

<a id="c3cb814b27094481"></a>
#### src_cluster_group

재배치할 특정 cluster group의 이름이다.

<a id="e7c588fd66354176"></a>
#### dest_cluster_group

테이블의 shard를 배치할 target cluster group의 이름이다.  
해당 테이블의 shard가 지정한 cluster group에 이미 존재할 경우 구문을 수행할 수 없다.

<a id="a7b53745538d51d7"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="975afff3307e7b55"></a>
### 설명

테이블의 특정 shard를 특정 cluster group에서 다른 cluster group으로 재배치한다.

특정 cluster group을 제거하려면 테이블의 shard를 재배치한 후에 [DROP CLUSTER GROUP](#d185e21cb13f6ec6) 구문을 수행해야 한다.

모든 테이블의 shard를 특정 cluster group에서 다른 cluster group으로 이동시키는 경우, ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP TO CLUSTER GROUP 구문을 수행한다.

<a id="58ef1daad6998dd3"></a>
### 사용 예

다음은 &lt;alter table move shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 MOVE SHARD shard1, shard2 TO CLUSTER GROUP g3;

Table altered.

gSQL> ALTER TABLE t1 MOVE SHARD FROM CLUSTER GROUP g1 TO CLUSTER GROUP g3;

Table altered.
```

<a id="e962c9ba85a7ce03"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="0fe25401f0a93826"></a>
### 참조

관련 내용은 [ALTER DATABASE MOVE SHARD](#23d029dca809fb16)를 참조한다.

<a id="9a20bc4c3fbf08ef"></a>
## ALTER TABLE name REBALANCE

<a id="a18d96e984fc7789"></a>
### 기능

테이블의 shard를 재배치한다.

<a id="3aa8c98a043e38fb"></a>
### 구문

```
<alter table rebalance statement> ::=
    ALTER TABLE table_name REBALANCE [ ONLINE | OFFLINE ]
    ;
```

<a id="e72f6c93ce0650d1"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table rebalance statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="392d40bc48923700"></a>
### 구문 규칙 및 파라미터

<a id="b944a179e1e14122"></a>
#### table_name

테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="5ad20ba7a6ea9ab6"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="c7950f77ddd2eef4"></a>
### 설명

다음과 같은 구문을 통해 cluster member, cluster group을 추가할 때 table들의 shard는 재배치하지 않는다.

- [CREATE CLUSTER GROUP](#609ea3458a43136d)
- [ALTER CLUSTER GROUP name ADD MEMBER](#3d7884550455c0c5)

추가된 cluster group과 cluster member의 테이블 shard를 재배치하려면 &lt;alter table rebalance statement&gt; 구문을 수행한다. 테이블의 shard가 이미 재배치된 경우, 별도의 재배치 작업 없이 실행에 성공한다.

모든 테이블들의 shard를 재배치하려면 [ALTER DATABASE REBALANCE](#092cbc6985d152fb) 구문을 수행한다.

<a id="d2d90b111ff7089d"></a>
### 사용 예

다음은 &lt;alter table rebalance statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 REBALANCE;

Table altered.
```

<a id="ce0d3c68d80804dd"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="3ed7b9af5c2a9447"></a>
## ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list

<a id="c00a843a3e383171"></a>
### 기능

특정 cluster group에 shard를 포함하지 않도록 테이블의 shard를 재배치한다.

<a id="3c22ad463f5ece35"></a>
### 구문

```
<alter table rebalance exclude cluster group statement> ::=
    ALTER TABLE table_name REBALANCE 
        EXCLUDE CLUSTER GROUP cluster_group_list [ ONLINE | OFFLINE ]
    ;
```

<a id="13294dfb133a07fd"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table rebalance exclude cluster group statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="1faa725c0c1d4b99"></a>
### 구문 규칙 및 파라미터

<a id="c8aab478db7edc7b"></a>
#### table_name

테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
해당 테이블이 cluster-wide인 경우에만 구문을 수행할 수 있다.

<a id="29b8db79c6fb3f71"></a>
#### cluster_group_list

테이블의 shard를 포함하지 않는 cluster group의 list이다.  
재배치에서 제외될 cluster group이 cluster 전체 group인 경우 구문을 수행할 수 없다.

<a id="ca145130fae6015f"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="5a2f8c35a78a0e96"></a>
### 설명

특정 cluster group을 배제하고 테이블의 shard를 재배치한다.  
해당 cluster group에 테이블의 shard가 존재하지 않을 경우, 별도의 재배치 작업없이 성공한다.  
테이블의 shard가 위치한 cluster group을 기준으로 shard를 재배치한다.

특정 cluster group을 제거하려면 테이블의 shard를 재배치한 후 [DROP CLUSTER GROUP](#d185e21cb13f6ec6) 구문을 수행해야 한다.  
모든 테이블들에서 cluster group을 배제하고 shard를 재배치하고자 할 경우, [ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP](#4b39c0cd3f8d62c9)을 수행한다.

<a id="07e662aacf6e2ac6"></a>
### 사용 예

다음은 &lt;alter table rebalance exclude cluster group statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 REBALANCE EXCLUDE CLUSTER GROUP g3;

Table altered.
```

<a id="8767669b956a5f6c"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="9e3df57fd520ef65"></a>
## ALTER TABLE name SPLIT SHARD

<a id="c4978449600f5ea0"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard를 split하여 재배치한다.

<a id="73e73be7e39b82d3"></a>
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

<a id="63483f81bdaedd50"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table split shard statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="05207e34558c981b"></a>
### 구문 규칙 및 파라미터

<a id="252c110d165d7db2"></a>
#### table_name

테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
해당 테이블이 cluster group specific이고 list shard 또는 range shard인 경우에만 구문을 수행할 수 있다.

<a id="91d5679861f5689f"></a>
#### source_shard_name

Split할 원본 shard 이름이다.  
해당 테이블에 shard가 존재하지 않을 경우 구문을 수행할 수 없다.

<a id="164655e4b3106598"></a>
#### &lt;split shard placement&gt;

원본 shard를 split하여 재배치할 대상 shard를 정의한다.

<a id="6aed5100e47a4584"></a>
#### &lt;split shard bound def&gt;

Split 될 대상 shard의 bound를 정의한다.

다음 두 가지 bound def 중 하나로 정의할 수 있다.

- &lt;split list shard def&gt;
- &lt;split range shard def&gt;

<a id="71f9dec309ea4985"></a>
##### &lt;split list shard def&gt;

List shard를 위한 split shard bound를 정의한다.

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

<a id="c6a9f01a760d375e"></a>
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

<a id="df3dd3806c6d493e"></a>
#### dest_group_name

Split 된 shard가 배치될 cluster group의 이름이다.

<a id="272291631b6e0117"></a>
### 설명

특정 테이블의 특정 shard를 분산하여 임의의 cluster group에 배치한다.  
특정 shard에 해당하는 레코드가 많거나 특정 group member에 부하가 편중될 때 shard를 분산하여 레코드와 부하를 분산하기 위해 사용된다.

<a id="d5cf38e8963e5165"></a>
### 사용 예

다음은 &lt;alter table split shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES IN ( 11 ) AT CLUSTER GROUP G2 );

Table altered.

gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES LESS THAN ( 11 ) AT CLUSTER GROUP G2 );


Table altered.
```

<a id="9ca152363e94d2f7"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="7e785edff3d349cd"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#3ed7b9af5c2a9447) 
- [ALTER TABLE name MOVE SHARD](#ba4cbd044acbe360)

<a id="a2da1b506cc85d50"></a>
## ALTER TABLE name RENAME SHARD

<a id="f812e64aa03222a4"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard의 이름을 변경한다.

<a id="729d31c9fb0de0eb"></a>
### 구문

```
<alter table rename shard statement> ::=
    ALTER TABLE table_name 
        RENAME SHARD shard_name TO new_shard_name
    ;
```

<a id="a30a34387fa7b67f"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table rename shard statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="554fd32adc96a931"></a>
### 구문 규칙 및 파라미터

<a id="36111b6d701b8739"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="e7b4f4ca228063d0"></a>
#### shard_name

변경할 shard의 기존 이름이다.  
Shard가 해당 테이블에 존재하지 않을 경우 구문을 수행할 수 없다.

<a id="a21f2acfdd24963a"></a>
#### new_shard_name

변경할 shard의 새 이름이다.  
테이블 내에 동일한 shard 이름이 존재하지 않아야 한다.

<a id="e0a8f3581610a9ca"></a>
### 설명

Hash, range, list 테이블의 특정 shard의 이름을 변경한다. Cloned 테이블에 대해서는 해당 구문을 수행할 수 없다.

<a id="21b65f635a87201e"></a>
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

<a id="d348c973ef8a7634"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="0c8a225f7bc999ce"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#16da97b62af765de)
- [ALTER TABLE name MOVE SHARD](#ba4cbd044acbe360)
- [ALTER TABLE name SPLIT SHARD](#9e3df57fd520ef65)
- [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef)

<a id="0e36db5fd37b58b3"></a>
## ALTER TABLE name READ { ONLY | WRITE }

<a id="13300eb770a84684"></a>
### 기능

테이블에 READ { ONLY | WRITE }을 설정한다.

<a id="f6d3054b40b237f5"></a>
### 구문

```
<alter table read { only | write } statement> :==
     ALTER TABLE table_name
         READ { ONLY | WRITE }
     ;
```

<a id="0761625af7c59b30"></a>
### 사용 범위 및 접근 권한

&lt;alter table read { only | write } statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="04193b09bb34c9d6"></a>
### 구문 규칙 및 파라미터

<a id="28882c02238243a6"></a>
#### table_name

테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="a6363df9bb9affc2"></a>
### 설명

테이블 속성을 READ { ONLY | WRITE } 으로 지정한다.

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

<a id="4ad9ed9a9974bbc4"></a>
### 사용 예

다음은 &lt;alter table read { only | write } statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 READ ONLY;

Table altered.

gSQL> ALTER TABLE t1 READ WRITE;

Table altered.
```

<a id="78ffe49c7960694d"></a>
### 호환성

SQL 표준에서는 &lt;alter table read { only | write } statement&gt; 구문을 정의하지 있지 않다.

<a id="86dc134dcaa15a53"></a>
### 참조

관련 내용은 [ALTER TABLE](#16da97b62af765de)을 참조한다.

<a id="5b91380c8925c3a4"></a>
## ALTER TABLE name RENAME TO

<a id="a775665fff22e55c"></a>
### 기능

테이블의 이름을 변경한다.

<a id="773074d7c963a5ee"></a>
### 구문

```
<rename table statement> ::=
    ALTER TABLE table_name 
        RENAME TO new_table_name
    ;
```

<a id="0888f26661d4da2a"></a>
### 사용 범위 및 접근 권한

&lt;rename table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="7f382b915acd35e8"></a>
### 구문 규칙 및 파라미터

<a id="020490da8c3dbdd0"></a>
#### table_name

테이블의 기존 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="d054bafa9be1f631"></a>
#### new_table_name

테이블의 새 이름이다.  
스키마 내에 동일한 테이블 이름이 존재하지 않아야 한다.

<a id="50db3c1cd3a61395"></a>
### 설명

테이블 이름이 변경되더라도 이를 참조하는 index constraint 등의 객체는 변경할 필요없다.

<a id="ae5bea1c771cfb19"></a>
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

<a id="6fc59a6faeca0ab4"></a>
### 호환성

SQL 표준에서는 &lt;rename table statement&gt; 구문을 정의하지 않고 있다.

<a id="3bf170d7d2139995"></a>
### 참조

관련 내용은 [ALTER TABLE](#16da97b62af765de)을 참조한다.

<a id="f353d2d59cd40842"></a>
## ALTER TABLE name STORAGE

<a id="e260441ac9dad170"></a>
### 기능

테이블의 물리적 속성을 변경한다.

<a id="5223c4ca7de35d9a"></a>
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

<a id="8cd014e7d07679d3"></a>
### 사용 범위 및 접근 권한

&lt;alter table physical attribute statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="a229621220f32660"></a>
### 구문 규칙 및 파라미터

<a id="1163eed4afe8f8dc"></a>
#### table_name

변경할 테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="18dc0413295a56f2"></a>
#### &lt;physical attribute clause&gt;

테이블을 구성하는 page의 물리적 속성을 변경한다.  
이미 할당된 page에는 적용되지 않으며 새로 할당받는 page에 적용된다.  
자세한 설명은 [CREATE TABLE](#1586c5952309fa38) 구문의 &lt;[table physical attribute clause&gt;](#570431608525411e) 절을 참조한다.

<a id="ea64c0487a7d28ff"></a>
#### &lt;segment attr clause&gt;

세그먼트를 구성하는 extent의 물리적 속성을 변경한다.   
이미 할당된 extent에는 적용되지 않으며, 새로 할당받는 extent에 적용된다.

- MAXSIZE integer 
    - 할당될 수 있는 세그먼트 공간의 크기를 변경한다. 
    - 이미 할당되어 있는 공간보다 작은 크기를 지정하면, MAXSIZE가 현재 할당되어 있는 크기로 변경된다.

<a id="4f02bca07b938d0d"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="0e733034fe092ba2"></a>
### 사용 예

다음은 테이블의 물리적 속성을 변경하는 예이다.

```
gSQL> ALTER TABLE t1 PCTFREE 10 PCTUSED 40 STORAGE ( NEXT 10M  MAXSIZE  100M );

Table altered.
```

<a id="097e8854e429c45f"></a>
### 호환성

SQL 표준에서는 테이블의 물리적 속성에 대하여 정의하지 않고 있다.

<a id="9c13df221898e967"></a>
### 참조

관련 내용은 [ALTER TABLE](#16da97b62af765de)을 참조한다.

<a id="e2cd4b70ceeae92d"></a>
## ALTER TABLE name ADD SUPPLEMENTAL LOG

<a id="b423e34ab085f0e5"></a>
### 기능

테이블의 데이터가 변경될 때 테이블에 primary key가 있으면 redo log에 primary key 값을 추가하도록 설정한다.

<a id="e09b77b2e11b64d8"></a>
### 구문

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="b9d7e0ddefbbc91a"></a>
### 사용 범위 및 접근 권한

&lt;add table supplemental log statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="2dd701a4541a2aea"></a>
### 구문 규칙 및 파라미터

<a id="ac2a85b34447c887"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

테이블에 primary key가 존재하지 않더라도 구문을 수행할 수 있다.

<a id="3f42721ed50e0dd3"></a>
### 설명

해당 TABLE에 UPDATE/ DELETE를 수행할 때 SUPPLEMENTAL LOG를 추가로 기록하도록 한다. 기록된 SUPPLEMENTAL LOG는 CDC와 같은 tool 또는 로그를 분석할 때 사용된다.

모든 TABLE의 SUPPLEMENTAL LOG를 기록하려면 *SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY = YES* 로 설정한다.

<a id="1e6cad16ca998e5e"></a>
### 사용 예

다음은 테이블의 data를 변경할 때 redo log에 primary key 값을 추가하도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="ba90a5adfb83e198"></a>
### 호환성

SQL 표준에서는 &lt;add table supplemental log statement&gt;를 다루지 않는다.

<a id="8c9afc6195a63e51"></a>
### 참조

관련 내용은 [ALTER TABLE name DROP SUPPLEMENTAL LOG](#8308658a684ec98a)를 참조한다.

<a id="8308658a684ec98a"></a>
## ALTER TABLE name DROP SUPPLEMENTAL LOG

<a id="75084ba8a9522834"></a>
### 기능

테이블의 데이터가 변경될 때 redo log에 primary key 정보를 남기지 않도록 설정한다.

<a id="74c0bc4ad62da190"></a>
### 구문

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="cd6af24adab72bbe"></a>
### 사용 범위 및 접근 권한

&lt;drop table supplemental log statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="ab1fbd29e01adc02"></a>
### 구문 규칙 및 파라미터

<a id="8374380431168601"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
[ALTER TABLE name ADD SUPPLEMENTAL LOG](#e2cd4b70ceeae92d) 구문을 사용해 설정된 상태여야 한다.

<a id="806ae56c46a1a2fb"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="297602e9cedaa782"></a>
### 사용 예

다음은 테이블의 데이터가 변경되었을 때 redo log에 primary key 정보를 남기지 않도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="e3e4dfe240717055"></a>
### 호환성

SQL 표준에서는 &lt;drop table supplemental log statement&gt;를 다루지 않는다.

<a id="c308f53537323289"></a>
## ALTER TABLESPACE

<a id="788d1b68a7a132bf"></a>
### 기능

테이블스페이스의 정의를 변경한다.

<a id="747f2d8b705931e0"></a>
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

<a id="3570ce4228f29e46"></a>
### 사용 범위 및 접근 권한

&lt;alter tablespace statement&gt; 구문을 수행하려면 사용자에게 database에 대한 ALTER TABLESPACE 권한이 있어야 한다.

<a id="85db90d7c283d251"></a>
### 구문 규칙 및 파라미터

<a id="5d2b56f7f95e721c"></a>
#### &lt;rename tablespace statement&gt;

테이블스페이스의 이름을 변경한다.  
자세한 내용은 [ALTER TABLESPACE name RENAME TO](#5cabc6f820db1edb) 구문을 참조한다.

<a id="1f5770ed56be5ac5"></a>
#### &lt;backup tablespace statement&gt;

테이블스페이스를 백업한다.  
자세한 내용은 [ALTER TABLESPACE name BACKUP](#bffdd0e4b8821918) 구문을 참조한다.

<a id="7a4f628dff766e68"></a>
#### &lt;on-offline tablespace statement&gt;

테이블스페이스의 모든 파일을 online 또는 offline으로 변경한다.  
자세한 내용은 [ALTER TABLESPACE name [ONLINE|OFFLINE]](#8b04971e84942653) 구문을 참조한다.

<a id="8f38172d07d5468e"></a>
#### &lt;add file statement&gt;

테이블스페이스에 파일을 추가한다.  
자세한 내용은 [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#87d9c6ccea9dcd62) 구문을 참조한다.

<a id="cf08aceb88b6b35e"></a>
#### &lt;drop file statement&gt;

테이블스페이스의 파일을 제거한다.  
자세한 내용은 [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#5091cb0b1bd1d67f) 구문을 참조한다.

<a id="7e368b43824c8605"></a>
#### &lt;rename datafile statement&gt;

데이터 테이블스페이스의 데이터 파일 이름을 변경한다.  
자세한 내용은 [ALTER TABLESPACE name RENAME DATAFILE](#7adf9a419c77a0db) 구문을 참조한다.

<a id="8b3517f9659fc5ef"></a>
### 설명

ALTER TABLESPACE 구문은 다른 Data Definition Language (DDL)과 달리 ROLLBACK 할 수 없고 구문을 수행한 transaction이 자동으로 COMMIT 된다.

<a id="b75bec9dc137c93b"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="257fe4f4c96de0e3"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="c143812da4f89d3b"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLESPACE](#df51248e3216ce23)
- [DROP TABLESPACE](#4aecf03632f3116f)

<a id="5cabc6f820db1edb"></a>
## ALTER TABLESPACE name RENAME TO

<a id="6dcc52643f6d925e"></a>
### 기능

테이블스페이스의 이름을 변경한다.

<a id="65838b721176f681"></a>
### 구문

```
<rename tablespace statement> ::=
    ALTER TABLESPACE tablespace_name RENAME TO <new_tablespace_name>
    ;
```

<a id="700b9140e03b407c"></a>
### 사용 범위 및 접근 권한

&lt;rename space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="148628d53c8f354d"></a>
### 구문 규칙 및 파라미터

<a id="16fc18684ad09373"></a>
#### tablespace_name

기존 테이블스페이스의 이름이다.

- Built-in 테이블스페이스의 이름은 변경할 수 없다.
- OFFLINE 테이블스페이스의 이름은 변경할 수 없다.

<a id="581ccd22be674067"></a>
#### new_tablespace_name

새로운 테이블스페이스의 이름이다.

<a id="4c1be4c5045a3771"></a>
### 설명

Tablespace 이름이 변경되더라도 기존에 이미 해당 tablespace에 생성된 table, index 등은 변경할 필요없다.

<a id="3400dbd7509d305b"></a>
### 사용 예

다음은 테이블스페이스의 이름을 변경하는 예이다.

```
gSQL> ALTER TABLESPACE space1 RENAME TO space2;

Tablespace altered.
```

<a id="7df08b80b0b4fa09"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="1f98684517136d2f"></a>
### 참조

관련 내용은 [ALTER TABLESPACE](#c308f53537323289)를 참조한다.

<a id="bffdd0e4b8821918"></a>
## ALTER TABLESPACE name BACKUP

<a id="a01ef94dafc142d2"></a>
### 기능

테이블스페이스를 backup 하기 위해 backup이 가능한 상태와 불가능한 상태로 전환한다.

<a id="c457aed473752ff2"></a>
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

<a id="0414f5e1b5e44c7f"></a>
### 사용 범위 및 접근 권한

&lt;backup space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="37b8f0814a863917"></a>
### 구문 규칙 및 파라미터

<a id="a3179e11e9860b5a"></a>
#### &lt;tablespace begin backup statement&gt;

테이블스페이스를 백업 가능한 상태로 설정한다.

- 생성되어 사용 중인 테이블스페이스를 백업 가능한 상태로 설정한다.
- OFFLINE/ temporary 테이블스페이스의 backup 상태는 전환할 수 없다.

<a id="e4d2abe2ac965a18"></a>
#### tablespace_name

Backup 상태를 전환할 테이블스페이스의 이름이다.

<a id="68359b696387b91a"></a>
#### &lt;tablespace end backup statement&gt;

테이블스페이스를 백업이 불가능한 상태로 설정한다.

<a id="3422eba3bf39c64d"></a>
#### &lt;tablesapce incremental backup statement&gt;

테이블스페이스의 증분 백업을 수행한다.  
데이터베이스가 OPEN 상태이고, ARCHIVELOG로 운영되어야 한다.

<a id="923e6a4a0f985787"></a>
#### &lt;incremental backup option&gt;

- 'integer'는 0 ~ 4 까지 지정할 수 있다.
- 'LEVEL 0'는 CUMULATIVE나 DIFFERENTIAL을 지정할 수 없다.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - 'integer'가 n이면 가장 최근에 'LEVEL 0' ~ 'LEVEL n-1'까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - DIFFERENTIAL
        - 'integer'가 n이면 가장 최근에 'LEVEL 0' ~ 'LEVEL n'까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - 생략되면 DIFFERENTIAL이 기본으로 지정된다.

<a id="16d01ccf09ea23f4"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="0042d0cdfa9864d7"></a>
### 설명

테이블스페이스에 생성된 datafile을 백업한다. 테이블스페이스 전체를 백업하려면 BEGIN BACKUP을 수행한 후 OS의 파일 복사로 datafile들을 복사하고 나서 END BACKUP을 수행한다. 한편, 증분 백업 파일은 하나의 구문으로 BACKUP_DIR_1 property에 설정된 경로에 생성한다.

<a id="c1727bac73ea51fc"></a>
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

<a id="3c9647796f6ab03d"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="f42dc0e811cfd1bb"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#c308f53537323289)
- [ALTER TABLESPACE name [ONLINE|OFFLINE]](#8b04971e84942653)

<a id="8b04971e84942653"></a>
## ALTER TABLESPACE name [ONLINE|OFFLINE]

<a id="bdfc3f8a0742cede"></a>
### 기능

테이블스페이스 상태를 변경한다.

<a id="1a0b270cbb407d1d"></a>
### 구문

```
<on/off tablespace statement> ::=
    ALTER TABLESPACE tablespace_name { ONLINE | OFFLINE [ NORMAL | IMMEIDATE ] }
    [ AT <domain name> ]
    ;
```

<a id="ec01fbb62d37465b"></a>
### 사용 범위 및 접근 권한

&lt;on/off tablespace statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="fd6cc524b9ac6741"></a>
### 구문 규칙 및 파라미터

<a id="b153ced32f227110"></a>
#### ONLINE

OFFLINE 상태의 테이블스페이스를 ONLINE으로 변경한다.

<a id="188ce7388ed9f3b1"></a>
#### OFFLINE NORMAL

ONLINE 상태의 테이블스페이스를 OFFLINE으로 변경한다.

OFFLINE으로 변경된 테이블스페이스는 일관된 (consistent) 상태이기 때문에 ONLINE 상태로 변경할 때 미디어 복구할 필요없다.

> MOUNT 단계에서는 OFFLINE NORMAL을 사용할 수 없다.   
> (단, 이전 인스턴스가 `\`SHUTDOWN NORMAL에 의해서 종료된 경우에는 가능하다.)

<a id="dc6bd5f6fccf5953"></a>
#### OFFLINE IMMEDIATE

ONLINE 상태의 테이블스페이스를 OFFLINE으로 변경한다.

OFFLINE으로 변경된 테이블스페이스는 비일관적인 (inconsistent) 상태이기 때문에, ONLINE 상태로 변경할 때 미디어 복구해야 한다.

> SYSTEM 테이블스페이스는 OFFLINE으로 변경할 수 없다.   
> OFFLINE IMMEDIATE는 미디어 복구를 필요로 하기 때문에 archive log mode에서만 수행할 수 있다.

<a id="10f45b5e61f01a89"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="799773781e340304"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="3a5431ffdf7c8d45"></a>
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

<a id="314bf192860b4fc7"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="b03c33cc176f549b"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#c308f53537323289)
- [ALTER TABLESPACE name BACKUP](#bffdd0e4b8821918)

<a id="87d9c6ccea9dcd62"></a>
## ALTER TABLESPACE name ADD [DATAFILE|MEMORY]

<a id="52cf8f3d4b18c497"></a>
### 기능

테이블스페이스의 공간을 확장한다.

<a id="87fa6be2ad62b8d6"></a>
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
```

<a id="0f06175fa11db39b"></a>
### 사용 범위 및 접근 권한

&lt;add space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="cd743e976307d0e4"></a>
### 구문 규칙 및 파라미터

<a id="60daac0b063bb0ec"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="ecd171e82f64722a"></a>
#### &lt;file specification&gt;

테이블스페이스의 유형에 따라 다음과 같은 구문을 사용해야 한다.

- 메모리 데이터 테이블스페이스 
    - DATAFILE &lt;add datafile clause&gt; 
- 메모리 임시 테이블스페이스 
    - MEMORY &lt;memory clause&gt;

<a id="b48653ae8a816635"></a>
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

<a id="cce007aeea797c25"></a>
#### &lt;memory clause&gt;

- &lt;size clause&gt;
    - 추가할 메모리를 정의한다.

자세한 내용은 [CREATE MEMORY TEMPORARY TABLESPACE](#bb76a8ab84a10ae1) 구문의 &lt;[memory clause&gt;](#64e4be923690a89b)를 참조한다.

<a id="6de0e11f1c08df37"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="0464996024d40a7b"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="f129fd48ac205ab3"></a>
### 사용 예

다음은 테이블스페이스에 data file을 추가하는 예이다.

```
gSQL> ALTER TABLESPACE space1 ADD DATAFILE 'test_file_a2.dbf' SIZE 10M REUSE;

Tablespace altered.
```

<a id="0b88bb415ff3d7f7"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="a56287165cbdb532"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE MEMORY DATA TABLESPACE](#f34525feb7d5edf3)
- [CREATE MEMORY TEMPORARY TABLESPACE](#bb76a8ab84a10ae1)
- [ALTER TABLESPACE](#c308f53537323289)

<a id="5091cb0b1bd1d67f"></a>
## ALTER TABLESPACE name DROP [DATAFILE|MEMORY]

<a id="d0f0174c54517ab9"></a>
### 기능

테이블스페이스의 공간을 축소한다.

<a id="4a186030b4d3cd85"></a>
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

<a id="083f12ae4e36d66a"></a>
### 사용 범위 및 접근 권한

&lt;drop space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="f2cd3d7ac9721948"></a>
### 구문 규칙 및 파라미터

<a id="a071e0d195b07421"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="dd2696ab92224652"></a>
#### &lt;file specification&gt;

테이블스페이스의 유형에 따라 다음과 같은 구문을 사용해야 한다.

- 메모리 데이터 테이블스페이스 
    - DATAFILE 'filename' 
- 메모리 임시 테이블스페이스 
    - MEMORY 'memory_name'

> 오프라인 테이블스페이스의 파일은 삭제할 수 없다.   
> 테이블스페이스의 첫 번째 파일은 삭제할 수 없다.  
> 한 번이라도 사용된 적이 있는 데이터 파일은 삭제할 수 없다.

<a id="ce37c688b17f1967"></a>
#### &lt;domain name&gt;

구문을 수행하는 멤버 및 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="767663107feda38a"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="1f1a4975b2397f94"></a>
### 사용 예

다음은 테이블스페이스의 파일을 제거하는 예이다.

```
gSQL> ALTER TABLESPACE space1 DROP DATAFILE 'test_file_f2.dbf';

Tablespace altered.
```

<a id="b63d51d7ffc6aba6"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="e303237180a47cac"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#c308f53537323289)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#87d9c6ccea9dcd62)
- [ALTER TABLESPACE name RENAME DATAFILE](#7adf9a419c77a0db)

<a id="7adf9a419c77a0db"></a>
## ALTER TABLESPACE name RENAME DATAFILE

<a id="87d4e0a0ecf504db"></a>
### 기능

테이블스페이스를 구성하는 데이터 파일의 이름을 변경한다.

<a id="0eb01940abcd9465"></a>
### 구문

```
<rename datafile statement> ::=
    ALTER TABLESPACE tablespace_name RENAME DATAFILE <filename_list> TO <filename_list>
    ;

    <filename_list> ::= 
        'filename' [ AT <domain name> ] [, ...]
```

<a id="bd778c6e1b864cdd"></a>
### 사용 범위 및 접근 권한

&lt;rename datafile statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

> TDS 모드이면서 데이터베이스가 OPEN인 상태에서는 온라인 테이블스페이스 파일을 변경할 수 없다. (임시 메모리 테이블스페이스는 제외된다.)   
> 변경한 후에도 파일은 반드시 존재해야 한다.

<a id="a684a95533d6d57c"></a>
### 구문 규칙 및 파라미터

<a id="c96ac662920f9f1e"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="e8c4ff1717364381"></a>
#### 'filename'

메모리 임시 테이블스페이스는 'memory_name'을 의미하며, 그 외의 테이블스페이스 종류는 'filename'을 의미한다.

<a id="b70b90ff8af8da5e"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="a55652fe323db796"></a>
### 설명

테이블스페이스 상태에 따라 연산 가능 여부가 결정된다.

- OFFLINE: MOUNT 단계나 OPEN 단계에서 수행 가능하다.
- ONLINE: MOUNT 단계에서만 수행 가능하다.

<a id="0ee8ab769121b7f7"></a>
### 사용 예

다음은 'test.dbf'를 'test1.dbf'로 변경하는 예이다.

```
gSQL> ALTER TABLESPACE TEST_TBS RENAME DATAFILE 'test.dbf' TO 'test1.dbf';

Tablespace altered.
```

<a id="643be66c5348c4d4"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="052e8162d3a9812c"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#c308f53537323289)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#87d9c6ccea9dcd62)
- [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#5091cb0b1bd1d67f)

<a id="c2d86feb760d5ff5"></a>
## ALTER USER

<a id="891db1d70bf93ca6"></a>
### 기능

데이터베이스 사용자 정의를 변경한다.

<a id="4445512cdfcf79d5"></a>
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

<a id="338648c4f13e6c48"></a>
### 사용 범위 및 접근 권한

&lt;alter user statement&gt; 구문을 수행하려면 사용자에게 ALTER USER ON DATABASE 권한이 있어야 한다.  
단, &lt;alter password&gt;는 사용자가 user_identifier와 동일할 경우에 권한 없이 수행할 수 있다.

<a id="e46a08d02e6e212b"></a>
### 구문 규칙 및 파라미터

<a id="b625939ecca1106a"></a>
#### user_identifier

변경할 사용자의 이름이다.

<a id="c5a34fa4fc6905a8"></a>
#### &lt;alter password&gt;

사용자의 password를 변경한다.

- IDENTIFIED BY new_password 
    - 새로운 password로 암호화되어 저장된다. 
    - Password의 길이는 128 byte보다 작아야 한다. 
    - Password는 대소문자를 구별한다.

- REPLACE old_password 
    - ALTER USER ON DATABASE 권한이 있을 경우에는 생략 가능하다. 
    - ALTER USER ON DATABASE 권한이 없을 경우에는 생략할 수 없다. 
        - 사용자와 user_identifier가 동일해야 한다.

<a id="09e79e85fe668fa9"></a>
#### &lt;alter profile&gt;

비밀번호 관리 정책 profile을 변경한다.

- PROFILE profile_name
    - 사용자가 생성한 profile_name을 할당한다.
- PROFILE DEFAULT
    - 기본 profile인 "DEFAULT"를 할당한다.
- PROFILE NULL
    - Profile을 할당하지 않는다.

<a id="756fe5a7db2fd505"></a>
#### &lt;password expire&gt;

사용자의 비밀번호를 만료시킨다.

<a id="8167f9b0049f1126"></a>
#### &lt;account lock&gt;

- ACCOUNT LOCK
    - 사용자 계정을 잠근다. 
- ACCOUNT UNLOCK
    - 계정 잠금을 해제한다.

<a id="693deb397782dd7f"></a>
#### &lt;alter default tablespace&gt;

사용자의 기본 tablespace를 변경한다.  
tablespace_name은 data tablespace여야 한다.

<a id="28bbf036955a4831"></a>
#### &lt;alter temporary tablespace&gt;

사용자의 temporary tablespace를 변경한다.  
tablespace_name은 temporary tablespace여야 한다.

<a id="bf5627bb0f4878fb"></a>
#### &lt;alter index tablespace&gt;

사용자의 index tablespace를 변경한다.

- INDEX TABLESPACE tablespace_name을 지정한다.
    - Data tablespace를 지정한 경우, LOGGING 인덱스여야 한다.
    - Temporary tablespace를 지정한 경우, NOLOGGING 인덱스여야 한다.
- INDEX TABLESPACE NULL
    - Index tablespace를 지정하지 않는다.

<a id="3108d00a5196b93e"></a>
#### &lt;alter schema path&gt;

사용자의 스키마 접근 경로를 변경한다.  
사용자의 SQL 구문에 schema가 명시되지 않았을 경우 스키마 접근 경로는 객체의 naming resolution을 위한 스키마 순서에 따라 결정된다.

스키마 이름이 기존에 스키마 접근 경로에 나열된 스키마 이름과 동일할 경우에는 추가적으로 반영되지 않는다.

다음은 *ALTER USER u1 SCHEMA PATH ( u1, s2, public );* 구문을 수행했을 때 schema에 존재하는 객체의 예이다.

<a id="cb551b319bb29594"></a>
| 스키마 이름 | u1 | s2 | public |
| --- | --- | --- | --- |
| - | t1 | - | t1 |
| - | - | t2 | - |
| - | - | - | t3 |

다음과 같이 u1 사용자가 수행하는 schema가 명시되지 않은 객체의 이름은 SCHEMA PATH에 의해 다음과 같이 해석된다.

- CREATE 구문 
    - CREATE TABLE t1 ( c1 INTEGER ); 
        - 에러: CREATE TABLE u1.t1 ( c1 INTEGER ); 
    - CREATE TABLE t2 ( c1 INTEGER ); 
        - 수행: CREATE TABLE u1.t2 ( c1 INTEGER );

- SELECT 구문 
    - SELECT * FROM t1; 
        - 수행: SELECT * FROM u1.t1; 
    - SELECT * FROM t2; 
        - 수행: SELECT * FROM s2.t2; 
    - SELECT * FROM t3; 
        - 수행: SELECT * FROM public.t3;

<a id="79473b7d7aec2ebe"></a>
#### CURRENT PATH

현재 사용자의 schema path이다.

다음 예와 같이 CURRENT PATH를 이용해 기존의 schema path를 유지하면서 새로운 schema path를 추가할 수 있다.

- u1의 현재 schema path 
    - (u1, public) 
- 구문 수행 
    - ALTER USER u1 SCHEMA PATH ( s1, CURRENT PATH, s2 ); 
- u1의 schema path는 다음과 같이 변경된다. 
    - (s1, u1, public, s2)

<a id="b904fe71839507d5"></a>
#### ALTER USER PUBLIC &lt;alter schema path&gt;

PUBLIC 계정의 schema path를 변경한다.  
PUBLIC 계정의 schema path는 모든 사용자의 schema path에 포함된다.

PUBLIC 계정에 최초로 부여된 schema path는 다음과 같다.

- DICTIONARY_SCHEMA 
- INFORMATION_SCHEMA 
- DEFINITION_SCHEMA 
- PERFORMANCE_VIEW_SCHEMA 
- FIXED_TABLE_SCHEMA

<a id="07137ed01abb7331"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="148f83d4438d674e"></a>
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

<a id="60717b796f53c3fc"></a>
### 호환성

SQL 표준에서 user의 개념은 다루고 있지만 user의 생성, 변경 및 삭제와 관련된 SQL 구문은 정의하지 않고 있다.

<a id="12c92b7a8354cbd5"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE USER](#339657c579ea782f)
- [DROP USER](#d82c6e3b5b385afc)

<a id="a12dee3fdc1d483b"></a>
## ALTER VIEW

<a id="05089cd6fe20035d"></a>
### 기능

View 정의를 변경한다.

<a id="01231f353ef7d0a5"></a>
### 구문

```
<alter view statement> ::=
    ALTER VIEW view_name <alter view action>
    ;

<alter view action> ::=
    COMPILE
```

<a id="6aa7c3e5491138c0"></a>
### 사용 범위 및 접근 권한

&lt;alter view statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 view에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- View가 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="e4433115eac08b8a"></a>
### 구문 규칙 및 파라미터

<a id="4e9a1b4c1f96bb78"></a>
#### view_name

변경할 view의 이름이다.  
schema_name.view_name과 같이 view가 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="39b7f0e70107e593"></a>
#### COMPILE

View를 다시 컴파일한다.  
View column에 부여한 COMMENT는 초기화된다.

<a id="aecc69de789b180b"></a>
### 설명

View가 참조하는 테이블이나 view가 변경되거나 삭제되면 해당 view도 영향을 받는다.

이런 정보는 INFORMATION_SCHEMA.VIEWS를 통해 조회할 수 있다.

- IS_COMPILED column
    - TRUE: View가 정상적으로 생성되었다.
    - FALSE: 에러가 존재하는 상태에서 FORCE 옵션으로 view가 생성되었다.

- IS_AFFECTED column
    - TRUE : View가 참조하는 테이블 또는 view가 변경되었다.
    - FALSE: View가 생성되고 COMPILE 된 후에 view가 참조하는 테이블이나 view가 변경되지 않았다.

<a id="adc406b044a9ce80"></a>
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

<a id="8ec81ab863936cb8"></a>
### 호환성

SQL 표준에서는 &lt;alter view statement&gt; 구문을 정의하지 않고 있다.

<a id="a06015cde3069966"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE VIEW](#69be25aa5896b17e)
- [DROP VIEW](#ae1beb0ccf35bd56)

<a id="70b74c802bcf0f64"></a>
## ANALYZE SYSTEM

<a id="966d904d100bb5cf"></a>
### 기능

시스템의 통계 정보를 제어한다.

<a id="8c1ea2bc716890e5"></a>
### 구문

```
<analyze system statement> ::=
    ANALYZE SYSTEM [ <analyze action> ]
    ;

<analyze action> ::=
      COMPUTE STATISTICS
    | DELETE STATISTICS
```

<a id="db4842f2c44037e6"></a>
### 사용 범위 및 접근 권한

&lt;analyze system statement&gt; 구문을 수행하려면 사용자에게 ANALYZE ANY ON DATABASE 권한이 있어야 한다.

<a id="8c10355bedb005f4"></a>
### 구문 규칙 및 파라미터

<a id="809bafe17165032b"></a>
#### &lt;analyze action&gt;

생략할 경우 기본값은 COMPUTE STATISTICS 이다.

<a id="b5061aa878bb75de"></a>
#### COMPUTE STATISTICS

시스템과 관련된 다음과 같은 통계 정보를 구축한다.

- CPU_OPS (Operations Per Second) 
    - CPU가 초당 처리할 수 있는 operation의 개수이다.

- NETWORK_IOPS (IO operations Per Second) 
    - Cluster인 경우에 유효하다. 
    - 초당 처리할 수 있는 network IO 횟수이다.

<a id="caf6174e6bb1a0ff"></a>
#### DELETE STATISTICS

시스템 통계 정보를 삭제한다.

<a id="98ef3d1b2d077710"></a>
### 설명

구축한 시스템 통계 정보는 질의 처리를 위한 최적화 과정의 비용을 계산하기 위해 사용한다.

<a id="1471c08fa54f95bb"></a>
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

<a id="323925c39051af3e"></a>
### 호환성

SQL 표준에서는 통계 정보에 대한 개념을 정의하지 않고 있다.

<a id="185c43523f9b6da2"></a>
### 참조

관련 내용은 [ANALYZE TABLE](#313298c58633e794)을 참조한다.

<a id="313298c58633e794"></a>
## ANALYZE TABLE

<a id="db43974fe68ed318"></a>
### 기능

테이블의 통계 정보를 제어한다.

<a id="5c1c39876dba9d65"></a>
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

<a id="b54c005bd0806046"></a>
### 사용 범위 및 접근 권한

&lt;analyze table statement&gt; 구문을 수행하려면 사용자에게 ANALYZE ANY ON DATABASE 권한이 있어야 한다.

<a id="f7978a436bc2feb7"></a>
### 구문 규칙 및 파라미터

<a id="1ed6fafbadfeeaf4"></a>
#### table_name

테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="bf6bf2f35ae0b03d"></a>
#### &lt;parallel clause&gt;

분석 과정에서 사용할 thread 개수를 지정한다.  
명시하지 않을 경우, 기본값은 PARALLEL 이다.

- NOPARALLEL
    - 병렬로 분석하지 않는다.

- PARALLEL [thread_count]
    - 병렬로 분석한다.
    - thread_count 값은 0 부터 사용할 수 있으며 최대값은 64 이다.
    - thread_count 값이 0이거나 생략된 경우 시스템의 CPU 개수에 의해 결정된다.

<a id="fe150a54dcf8c4fd"></a>
#### &lt;analyze action&gt;

생략할 경우 기본값은 COMPUTE STATISTICS 이다.

<a id="35cdfb31739e39c2"></a>
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

<a id="c9d8ff287f6a2afd"></a>
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

<a id="b85af7dd349f06e0"></a>
#### ESTIMATE STATISTICS &lt;sample_clause&gt;

지정한 &lt;sample_clause&gt;만큼의 샘플을 사용하여 column과 index의 통계 정보를 구축한다.

- SAMPLE row_count ROWS 
    - 지정한 row 개수만큼 샘플을 사용한다. 
    - row_count는 0보다 큰 양의 정수이다. 
- SAMPLE percentage PERCENT 
    - 지정한 비율만큼 샘플을 사용한다. 
    - Percentage는 1 ~ 99 범위의 양의 정수이다.

샘플링 row의 개수가 [MIN_SAMPLE_ROW_COUNT](../part-02-administration-manual/10-server-property.md#ed54cddaf1645a39) 프로퍼티 값보다 작을 경우 프로퍼티 값을 따른다.

<a id="e94ee02acf466ffd"></a>
#### &lt;for_clause&gt;

생략할 경우, 통계정보 구축이 가능한 모든 column과 모든 인덱스의 통계 정보를 구축한다.

<a id="0aa0912bbab5e3e6"></a>
#### FOR ALL COLUMNS

통계 정보 구축이 가능한 모든 column의 통계 정보를 구축한다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="5ffa71c39b072a1f"></a>
#### FOR ALL INDEXED COLUMNS

인덱스에 포함된 모든 column의 통계 정보를 구축한다.   
그 외 column의 통계 정보는 구축하지 않는다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="f254a9cff85e10de"></a>
#### FOR COLUMNS column_name [, ...]

나열한 column의 통계 정보를 구축한다.   
기술하지 않은 column의 통계 정보는 구축하지 않는다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="820513ad77be07ee"></a>
#### FOR ALL INDEXES

모든 인덱스의 통계 정보를 구축한다.   
Column 통계 정보는 구축하지 않는다.

<a id="950d50fca570b48b"></a>
#### FOR INDEXES index_name [, ...]

나열한 인덱스의 통계 정보를 구축한다.   
기술하지 않은 인덱스의 통계 정보는 구축하지 않는다.   
Column 통계 정보는 구축하지 않는다.

<a id="437a95cd1fe87e40"></a>
#### DELETE STATISTICS

테이블의 통계 정보를 제거한다.

<a id="011658ea69ff7f28"></a>
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

<a id="56c3c658861b247c"></a>
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

<a id="0a22c7d3b01efc4a"></a>
### 호환성

SQL 표준에서는 통계 정보에 대한 개념을 정의하지 않고 있다.

<a id="2419fc8e3f7dbca0"></a>
### 참조

관련 내용은 [ANALYZE SYSTEM](#70b74c802bcf0f64)을 참조한다.

<a id="c789ab5113d50e70"></a>
## AUDIT POLICY

<a id="68cae9d1e6fe8f9b"></a>
### 기능

Audit policy를 활성화한다.

<a id="5abc5e85b2841def"></a>
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

<a id="132ff97397b7820a"></a>
### 사용 범위 및 접근 권한

&lt;audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="2d5051d065dff43e"></a>
### 구문 규칙 및 파라미터

<a id="0ef493a18553630c"></a>
#### policy_name

활성화할 audit policy 객체의 이름이다.  
활성화 된 audit policy는 기존 session에 영향을 미치지 않으며 새로 생성되는 session에만 영향을 준다.

<a id="09d090cdbd8e9e56"></a>
#### &lt;specified_user_option&gt;

감사를 수행할 사용자를 명시한다.     
생략할 경우 모든 사용자에 대해 감사를 수행한다.

동일한 audit policy에 대해 BY 절과 EXCEPT 절을 함께 사용할 수 없다.

- BY user_list: 감사를 수행할 사용자를 특정할 경우 BY 절을 사용한다.
- EXCEPT user_list: 특정 사용자를 배제하고 다른 사용자들을 감사할 경우 EXCEPT 절을 사용한다.

<a id="4df8ce333ae71868"></a>
#### &lt;specified_success_option&gt;

- WHENEVER SUCCESSFUL
    - Action이 성공했을 때 audit record가 생성된다.
- WHENEVER NOT SUCCESSFUL
    - Action이 실패했을 때 audit record가 생성된다.
- 생략할 경우 성공할 경우와 실패할 경우 모두 audit record를 생성한다.

<a id="0df6160a163af252"></a>
### 설명

Audit policy를 활성화하면 기존 session에는 영향을 미치지 않으며 새로 생성되는 session에 대해 감사를 시작한다.

<a id="b4228d45411e4c3e"></a>
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

<a id="79e93dcdbeb77a5e"></a>
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

<a id="95dc1d5c598d5303"></a>
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

다음 예와 같이 NOAUDIT POLICY 구문으로 비활성화한다.

- AUDIT POLICY p1 BY u1, u2;
    - NOAUDIT POLICY p1 BY u1, u2;
- AUDIT POLICY p1;
    - NOAUDIT POLICY p1;
- AUDIT POLICY p1 EXCEPT u1, u2;
    - NOAUDIT POLICY p1;
    - NOAUDIT POLICY 구문에는 EXCEPT option이 없다.

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

<a id="56c86d92d0cfecb2"></a>
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

<a id="36fff2556bad87e3"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="66810a942124ae19"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#676233f209f722e4)
    - [DROP AUDIT POLICY](#c1e1a11e6ac9443a)
    - [ALTER AUDIT POLICY](#2cfef6a9826bdadf)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#c789ab5113d50e70)
    - [NOAUDIT POLICY](#2953451ac097af0c)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#2eb922e8e06a1b57)

- Audit trail 제거: [ALTER DATABASE CLEAR AUDIT TRAIL](#016c886b7cddf620)

<a id="c718855fa5a651b0"></a>
## CLOSE cursor_name

<a id="b5cc89d3b98036e2"></a>
### 기능

커서를 닫는다.

<a id="c7e21042f3db78dd"></a>
### 구문

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="8f069bba918a4e56"></a>
### 구문 규칙 및 파라미터

<a id="d5e760775b352faf"></a>
#### cursor_name

커서가 open 되어 있어야 한다.  
세션 내에서 [DECLARE cursor_name](#c0f5909b51d661a3) 구문으로 선언된 커서이어야 한다.

<a id="8203f5e72d5f7bc7"></a>
### 설명

Cursor는 session 내에 존재하는 객체이고 서로 다른 session의 cursor에 영향을 주지 않는다.

<a id="b7ea6c29e60d942c"></a>
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

<a id="bebe3fbbd5bdd2ec"></a>
### 호환성

**SQL 표준 호환성**

<a id="54913bdaf7c302f9"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic dynamic SQL | O |

<a id="6e0fe657923e89b9"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#c0f5909b51d661a3)
- [OPEN cursor_name](#275ead84ebffb434)
- [FETCH cursor_name](#f8b0914239210b68)

<a id="864dfa43b0df5050"></a>
## COMMENT ON name IS

<a id="426b589018c6536f"></a>
### 기능

객체에 대한 설명을 dictionary에 저장한다.

<a id="90ebb157809218f6"></a>
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

<a id="9959ff9bbfae4bfe"></a>
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
    - Stored procedure/ function의 소유자
    - Stored procedure/ function이 속한 스키마에 대해 CONTROL SCHEMA ON SCHEMA
    - ALTER ANY PROCEDURE ON DATABASE

<a id="9cb5367758c46e93"></a>
### 구문 규칙 및 파라미터

<a id="16298ebf3ac0ccee"></a>
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

Schema object의 경우 schema_name을 기술하지 않으면 구문을 수행하는 사용자의 [Schema Path](13-sql-objects.md#37870b8d44e548dc)에 의해 스키마 이름이 결정된다.

```
COMMENT ON TABLE test_table IS 'test comment'; 
→ COMMENT ON TABLE user_default_schema.test_table IS 'test comment';
```

<a id="d729cd2f4b35999c"></a>
#### 'comment string'

저장할 comment 문장을 기술한다.  
Comment를 삭제하려면 다음과 같이 empty string ('')을 사용한다.

```
COMMENT ON TABLE test_table IS '';
```

Comment string의 길이는 1024 bytes를 초과할 수 없다.

<a id="2d552c05f6b82fb5"></a>
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

각 view에 대한 자세한 내용은 [DICTIONARY_SCHEMA](../part-02-administration-manual/9-database-information.md#ef9643afcec18f44)를 참조한다.

<a id="7bc3ba58870efec7"></a>
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

<a id="ec44400fcc3ff32b"></a>
### 호환성

SQL 표준에는 &lt;comment statement&gt;가 없다.

<a id="75b82fec67e8ca7c"></a>
## COMMIT

<a id="765872bb37c4fbda"></a>
### 기능

현재 트랜잭션을 종료하고 변경된 모든 내용을 영속화한다.

<a id="c8a7dd26dd9d6a03"></a>
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

<a id="40e4f6d67983be77"></a>
### 구문 규칙 및 파라미터

<a id="b86ee799e56a0a67"></a>
#### WORK

동작에 영향을 미치지 않는 예약어이다.

<a id="5374e629ed8c6040"></a>
#### &lt;commit comment clause&gt;

- COMMENT 'comment_string'
    - 트랜잭션을 commit 할 때 트랜잭션에 주석을 지정한다.

<a id="b9384503c0e71448"></a>
#### &lt;commit write clause&gt;

Commit 연산으로 생성된 redo log가 redo log file에 기록될 때까지 기다릴지 여부를 결정한다.

- WAIT
    - Commit 연산으로 생성된 redo log가 redo log file에 기록될 때까지 기다린 후 연산을 종료한다.
- NOWAIT
    - Commit 연산으로 생성된 redo log가 redo log buffer에 기록되면 연산을 종료한다.
- 지정되어 있지 않을 경우, 프로퍼티를 따른다.

<a id="5cca6b062a8bdd1b"></a>
#### &lt;commit force clause&gt;

분산 트랜잭션을 수동으로 commit 할 때 사용한다.

- FORCE 'xid_string'
    - 'xid_string'에 해당하는 분산 트랜잭션을 commit 한다.
    - 'xid_string'은 '*format_id*.*transaction_id*.*branch_id*'로 구성된다.

<a id="248f8e7484ab5143"></a>
### 설명

COMMIT 구문은 트랜잭션 내에서 수행된 다음 구문들을 완료한다.

- Data Manipulation Language (DML) 구문
    - 데이터를 변경하는 INSERT, UPDATE, DELETE 등의 구문
- Data Definition Language (DDL) 구문 
    - 객체의 구조 및 정의를 변경하는 CREATE, DROP, ALTER, TRUNCATE, GRANT, REVOKE 등의 구문

예외적으로, DDL 중에 OS 자원을 다루거나 DATA TYPE을 변경하는 다음 구문들은 자동으로 COMMIT 된다.

- [CREATE TABLESPACE](#df51248e3216ce23)
- [DROP TABLESPACE](#4aecf03632f3116f)
- [ALTER TABLESPACE](#c308f53537323289)
- ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE: &lt;[alter column data type clause&gt;](#76fd82a3da886b7c)

COMMIT을 수행하면 WITHOUT HOLD 옵션으로 열린 커서는 자동으로 닫힌다. 커서에 대한 자세한 내용은 다음의 커서 관련 구문을 참조한다.

- [DECLARE cursor_name](#c0f5909b51d661a3)
- [OPEN cursor_name](#275ead84ebffb434)

트랜잭션이 지연된 (DEFERRED) 제약 조건을 위반하면 COMMIT 구문의 수행은 실패하고 트랜잭션은 ROLLBACK 된다. 지연된 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](#8e1fec980aea373d) 구문의 설명을 참조한다.

<a id="8dad70a6f396e399"></a>
### 사용 예

다음은 INSERT 구문을 수행한 후에 COMMIT을 수행하는 예이다.

```
gSQL> INSERT INTO t1 VALUES ( 1, 'anonymous' );

1 row created.

gSQL> COMMIT WORK COMMENT 'INSERT T1';

Commit complete.
```

<a id="8a92aa16d5675b8e"></a>
### 호환성

**SQL 표준 호환성**

<a id="76b59dd45d1091cf"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T261 | Chained transactions | X |

<a id="c87a4f5196677340"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ROLLBACK](#1476005da98d89d8)
- [SAVEPOINT savepoint_specifier](#e403c1a580ceeb98)

<a id="676233f209f722e4"></a>
## CREATE AUDIT POLICY

<a id="99e2e8ecc896f2b1"></a>
### 기능

Audit policy 객체를 생성한다.  
생성한 audit policy 객체를 활성화하려면 AUDIT POLICY 구문을 수행하여야 한다.

<a id="d9f4051b1649be08"></a>
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

<a id="af98bad6cc67b5e3"></a>
### 사용 범위 및 접근 권한

&lt;audit policy definition&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="fc00c7c5e32e10c7"></a>
### 구문 규칙 및 파라미터

<a id="a4e6cbb66e0fc640"></a>
#### policy_name

생성할 audit policy의 이름이다.

<a id="31d0cba53a18d083"></a>
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

<a id="325cabdb17019888"></a>
#### &lt;action_audit_clause&gt;

특정 객체에 대한 action과 database 전체에 대한 action을 감사한다.

<a id="b020c36f9b24ba4d"></a>
#### &lt;object_action_audit&gt;

<a id="711fe09fc52d4e1f"></a>
##### ALL ON object_name

object_name에 해당하는 객체를 나열할 수 있는 모든 action을 의미한다.

각 객체 유형별로 감사할 수 있는 audit action은 다음 표와 같다.

**객체별 audit action**

<a id="f16db030f217ef86"></a>
| Object type | Action |
| --- | --- |
| Table | ALTER, COMMENT, DELETE, GRANT, INDEX, INSERT, LOCK, RENAME, SELECT, UPDATE |
| View | ALTER, COMMENT, GRANT, SELECT |
| Sequence | ALTER, COMMENT, GRANT, SELECT |
| Stored function/  procedure | ALTER, COMMENT, EXECUTE, GRANT |

<a id="6d8999de83e4cd99"></a>
##### &lt;object_action&gt; ON object_name

특정 object에 대한 개별 action들은 다음과 같이 ON 절을 명시하여 하나씩 나열한다.

```
CREATE AUDIT POLICY p1
       ACTIONS INSERT ON u1.t1
             , DELETE ON u1.t1
             , UPDATE ON u1.t1
;
```

<a id="5396326feca620d0"></a>
##### EXECUTE action 유의 사항

Stored function이나 stored procedure의 EXECUTE action 성공, 실패 여부에 대한 감사는 실제 수행 시점의 수행 가능 여부만으로 판단한다.

- WHENEVER NOT SUCCESSFUL의 경우, stored function/ procedure를 수행할 수 없을 경우에 감사 레코드를 생성한다.
- WHENEVER SUCCESSFUL의 경우, stored function/ procedure 내부의 SQL 구문을 수행하는 중에 에러가 발생하더라도 감사 레코드를 생성한다.
- Stored function/ procedure 내부의 SQL 구문 실패에 대한 감사가 필요할 경우, 해당 SQL 구문을 감사 대상에 포함해야 한다.

<a id="5d22c39a0bdcb0ca"></a>
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

<a id="759e3b0143052b9c"></a>
### 설명

Audit policy 객체는 감사할 대상들을 정의한 객체이다.    
Audit policy를 활성화하려면 AUDIT POLICY 구문을 수행해야 한다.

다수의 audit policy를 정의하고 활성화할 수 있지만, 제한된 개수의 audit policy를 유지하는 것이 바람직하다.    
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

<a id="674003d53b099dc7"></a>
#### Audit Record 생성

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

<a id="d8590d7fe1b45e8c"></a>
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

다음은 위의 예를 모두 합친 audit policy를 정의한 예이다.

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

<a id="7f5f5042b771a756"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="4f429ffe84cfee04"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#676233f209f722e4)
    - [DROP AUDIT POLICY](#c1e1a11e6ac9443a)
    - [ALTER AUDIT POLICY](#2cfef6a9826bdadf)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#c789ab5113d50e70)
    - [NOAUDIT POLICY](#2953451ac097af0c)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#2eb922e8e06a1b57)

- Audit trail 제거: [ALTER DATABASE CLEAR AUDIT TRAIL](#016c886b7cddf620)

<a id="609ea3458a43136d"></a>
## CREATE CLUSTER GROUP

<a id="b0d4b0612f5c08bd"></a>
### 기능

Cluster system에 참여할 cluster group을 생성한다.

<a id="614a2e413e4903ff"></a>
### 구문

```
<cluster group definition> ::=
    CREATE CLUSTER GROUP group_name 
        <cluster member definition> [, ...]
    ;

<cluster member definition> ::=
    CLUSTER MEMBER member_name <connection attribute>

<connection attribute> ::
    HOST 'address' PORT port_no
```

<a id="699122258a5c4ac6"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;cluster group definition&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="5b4efee6648b2216"></a>
### 구문 규칙 및 파라미터

<a id="32564c6ff0cdf3eb"></a>
#### group_name

Cluster group의 이름이다.  
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.  
이름의 길이는 128 바이트보다 작아야 한다.

<a id="31dadd3908ab216b"></a>
#### &lt;cluster member definition&gt;

Cluster group에 포함될 cluster member를 정의한다.  
Cluster group은 cluster member를 최대 32 개까지 포함할 수 있다.  
Cluster system에 최초로 생성하는 cluster group에는 cluster member를 한 개만 정의할 수 있고 자기 자신을 cluster member로 포함해야 한다.

<a id="7910f5d2fb8ee2db"></a>
#### member_name

Cluster member의 이름이다.  
Cluster member 이름은 해당 member의 database를 생성할 때 정의한 member 이름과 동일해야 한다.  
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.  
이름의 길이는 128 바이트보다 작아야 한다.

Cluster member의 start-up 단계는 OPEN 단계여야 한다.

<a id="847eb69fa500c6ed"></a>
#### &lt;connection attribute&gt;

Cluster member간 통신을 위한 연결 정보를 정의한다.  
&lt;connection attribute&gt;는 해당 member의 database를 생성할 때 정의한 HOST, PORT와 동일해야 한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST address는 ip v4 형식으로 사용한다. 
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="2c8bb67cbf5aae72"></a>
### 설명

&lt;cluster group definition&gt; 구문은 table들의 shard를 재배치하지 않는다.

추가된 cluster group에 shard를 재배치하려면 다음 구문을 수행해야 한다.

- [ALTER DATABASE REBALANCE](#092cbc6985d152fb)
- [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef)

<a id="3b4b5aa11d999d00"></a>
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

<a id="528bbf0607044a5b"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="4c63da88d3774566"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP CLUSTER GROUP](#d185e21cb13f6ec6)
- [ALTER CLUSTER GROUP name ADD MEMBER](#3d7884550455c0c5)

<a id="60d111e8979eff2d"></a>
## CREATE CLUSTER LOCATION

<a id="851ab11d4052c9c2"></a>
### 기능

Cluster member의 접속 정보를 생성한다.

<a id="c8079c621dccfa7a"></a>
### 구문

```
<cluster location definition> ::=
    CREATE CLUSTER LOCATION member_name 
    <cluster connection attribute>
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="ee8b93c77bfb2204"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;cluster location definition&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="a39c94a2503c6c1f"></a>
### 구문 규칙 및 파라미터

<a id="657389c40b377fe1"></a>
#### member_name

Cluster member의 이름이다.  
등록된 cluster location 정보에 동일한 cluster member 이름이 존재하지 않아야 한다.  
이름의 길이는 128 바이트보다 작아야 한다.

<a id="6f81f7ae56ddd8b1"></a>
#### &lt;cluster connection attribute&gt;

Cluster member간 통신을 위한 연결 정보를 정의한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST address는 ip v4 형식으로 사용한다. 
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="c9fb731ca096c732"></a>
### 설명

기본적으로 cluster location 정보는 cluster group을 생성하거나 cluster member를 추가할 때 제공되는 접속 정보를 이용하여 자동으로 생성된다. 생성된 정보는 cluster member와 group을 삭제할 때 함께 삭제된다.

만약 cluster location의 접속 정보가 변경되면 cluster member를 삭제하거나 다시 생성할 필요없이 [ALTER CLUSTER LOCATION](#b088884e1c158484)을 이용하여 접속 정보를 변경할 수 있다.

<a id="6add970286d41ae1"></a>
### 사용 예

```
gSQL> 
CREATE CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120,
;

Created
```

<a id="99f21d182763f465"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="65ddba7061ec5680"></a>
### 참조

관련 내용은 [DROP CLUSTER LOCATION](#f2273de5f0bd9109)을 참조한다.

<a id="ce4afb58f69a16f7"></a>
## CREATE INDEX

<a id="de87a52b170b5394"></a>
### 기능

인덱스를 생성한다.

<a id="6e2f21379239c047"></a>
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
    | <logging clause> 
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

<logging clause> ::=
      LOGGING
    | NOLOGGING

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="7a73484ec4a4b647"></a>
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

<a id="1305f62b377b8fa3"></a>
### 구문 규칙 및 파라미터

<a id="3b8e8d614cf09789"></a>
#### UNIQUE

인덱스를 구성하는 column들에 중복 값을 허용하지 않는다.

<a id="5ca28f2e933413f7"></a>
#### index_name

생성할 인덱스의 이름이며, 스키마 내에서 유일해야 한다.  
스키마 이름을 생략할 경우, 참조하는 테이블이 속한 스키마에 인덱스가 생성된다.  
인덱스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="33527a9bec3a4745"></a>
#### table_name

인덱스를 생성할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="d4fbc9a468dccbbf"></a>
#### column_name

인덱스 key로 사용할 column의 이름이다.  
하나 이상의 column을 정의해야 하는데 최대 32 개의 column을 인덱스 key로 사용할 수 있다.

구현 내용에 따라 다음과 같은 제약이 발생할 수 있다.

- 인덱스에 포함되는 column의 데이터 타입이 LONG CHARACTER VARYING, LONG BINARY VARYING 일 경우 인덱스를 생성할 수 없다. 
- Column들의 precision 합계가 page size의 1/2 보다 작아야 생성할 수 있다.

<a id="5e92575177fa93b9"></a>
#### ASC | DESC

Column의 정렬 순서를 명시한다.

- ASC: 오름차순으로 정렬한다. 
- DESC: 내림차순으로 정렬한다. 
- 명시하지 않을 경우, 기본값은 ASC이다.

<a id="6d93b76f629b8e29"></a>
#### NULLS FIRST | NULLS LAST

NULL 값의 정렬 순서를 명시한다.

- NULLS FIRST: NULL이 아닌 값들보다 앞에 위치한다. 
- NULLS LAS : NULL이 아닌 값들보다 뒤에 위치한다. 
- 명시하지 않을 경우, 기본값은 NULLS LAST 이다.

<a id="451526bdc8256203"></a>
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

<a id="5c7a1d8270233d6c"></a>
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

<a id="3f91c160edf92edd"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="7206a381e2047ee0"></a>
#### LOGGING | NOLOGGING

인덱스의 리두 로깅 여부를 명시한다.  
명시하지 않을 경우, 기본값은 NOLOGGING이다.

<a id="634ebe583a94fce1"></a>
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

<a id="ea1b2a95d2d3add6"></a>
#### TABLESPACE tablespace_name

인덱스가 저장될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - LOGGING 인덱스의 tablespace_name은 data tablespace여야 하며 
    - NOLOGGING 인덱스의 tablespace_name은 temporary tablespace 또는 nologging tablespace여야 한다.

- TABLESPACE 절을 생략할 경우,
    - USER의 INDEX TABLESPACE tablespace_name을 지정한 경우
        - 정의한 테이블스페이스를 사용한다.
    - USER의 INDEX TABLESPACE가 NULL인 경우
        - LOGGING 인덱스는 사용자의 기본 데이터 테이블스페이스를 사용하고,
        - NOLOGGING 인덱스는 사용자의 기본 임시 테이블스페이스를 사용한다.

<a id="67d6e5f38db703cc"></a>
### 설명

LOGGING 인덱스와 NOLOGGING 인덱스에는 다음과 같은 trade-off가 있다.

- LOGGING 인덱스
    - 장점: 시스템을 구동할 때 로그를 이용해 인덱스가 자동으로 복구되므로 별도의 구축과정이 없다.
    - 단점: 관련 row를 변경할 때 인덱스 변경 내용을 로그로 기록하여 디스크 IO를 유발한다.
- NOLOGGING 인덱스
    - 장점: 관련 row를 변경할 때 인덱스 변경 내용에 대한 디스크 IO가 발생하지 않는다.
    - 단점: 시스템을 구동할 때 인덱스에 대한 로그 정보가 없어 자동으로 인덱스를 재구축한다.

<a id="4285c2c414d3760c"></a>
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
gSQL> CREATE INDEX idx_t1_id ON t1( id ) LOGGING;

Index created.
```

다음은 인덱스를 병렬로 생성하도록 하는 예이다.

```
gSQL> CREATE INDEX idx_t1_name ON t1( name ) PARALLEL;

Index created.
```

다음은 인덱스를 생성할 때 테이블스페이스를 지정하는 예이다.

```
gSQL> CREATE INDEX idx_t1_name ON t1( name ) NOLOGGING TABLESPACE mem_temp_tbs;

Index created.
```

<a id="d65086ea55fbee91"></a>
### 호환성

SQL 표준에서는 인덱스에 대한 개념을 다루지 않고 있다.

<a id="d4926ad0cfdbf94b"></a>
### 참조

관련 내용은 [DROP INDEX](#93a6d0dc40b79b2e)를 참조한다.

<a id="208fdfbd422ca37d"></a>
## CREATE PROFILE

<a id="5a30ae3c0d9f40a9"></a>
### 기능

Profile을 생성하는 구문으로써 password 관리 방법을 설정할 수 있다.   
User에게 profile을 할당하면 profile에 정의된 방법으로 user의 password를 관리한다.

<a id="86c00c0bfa82195b"></a>
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

<a id="9f66ac726c90587a"></a>
### 사용 범위 및 접근 권한

&lt;profile definition&gt; 구문을 수행하려면 사용자에게 CREATE PROFILE ON DATABASE 권한이 있어야 한다.

<a id="846304aae6782744"></a>
### 구문 규칙 및 파라미터

<a id="c680e1d6090dc76b"></a>
#### profile_name

생성할 profile의 이름을 명시한다.

<a id="4a89bb65d9f23664"></a>
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

<a id="f9c08ecb7ae616e1"></a>
#### FAILED_LOGIN_ATTEMPTS

연속적인 로그인 실패 가능 횟수를 설정한다.  
명시된 횟수를 넘어서면 계정이 잠긴다.

- FAILED_LOGIN_ATTEMPTS integer
    - 값의 범위는 0보다 큰 양의 정수여야 한다. 
- FAILED_LOGIN_ATTEMPTS UNLIMITED
    - 로그인 실패로 인해 계정이 잠기지 않는다.
- FAILED_LOGIN_ATTEMPTS DEFAULT
    - "DEFAULT" profile의 정책을 따른다.

<a id="48d579a2266b87de"></a>
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

<a id="21a5919faf60ceac"></a>
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

<a id="8d9c3e78e5fe46dd"></a>
#### PASSWORD_GRACE_TIME

PASSWORD_LIFE_TIME 이후에 login 했을 때 비밀번호 만료를 유예하는 기간을 설정한다.

- PASSWORD_GRACE_TIME constant_expression 
    - 비밀번호 만료 유예 기간 (day)이다.
    - 기본 단위는 일 (day)이다.
    - 테스트 하기 위해 시 (n/24), 분 (n/1440), 초 (n/86400)를 명시할 수 있다.
    - 값의 범위는 1초 (1/86400) ~ 100000 일이다. 
- PASSWORD_GRACE_TIME UNLIMITED 
    - 비밀번호 만료를 계속 유예한다.
- PASSWORD_GRACE_TIME DEFAULT 
    - "DEFAULT" profile의 정책을 따른다.

비밀번호 유효기간이 지난 후 처음으로 login 하려고 시도할 때부터 PASSWORD_GRACE_TIME이 시작되고, 이 기간동안 비밀번호를 변경하지 않으면 비밀번호가 만료된다.

<a id="5d52b442c6d6ce56"></a>
#### PASSWORD_REUSE_MAX

이전 비밀번호를 재사용하려 할 때 재사용할 수 없는 최근 비밀번호의 개수를 설정한다.

PASSWORD_REUSE_MAX는 PASSWORD_REUSE_TIME과 함께 사용해야 한다.

- PASSWORD_REUSE_MAX integer
    - 값의 범위는 0보다 큰 양의 정수여야 한다. 
- PASSWORD_REUSE_MAX UNLIMITED
    - PASSWORD_REUSE_TIME이 UNLIMITED인 경우, 이전 비밀번호 모두를 재사용할 수 있다.
    - PASSWORD_REUSE_TIME이 UNLIMITED가 아닌 경우, 이전 비밀번호 중 어떤 것도 재사용할 수 없다.
- PASSWORD_REUSE_MAX DEFAULT
    - "DEFAULT" profile의 정책을 따른다.

<a id="0062483de050e35f"></a>
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

<a id="2d7424e68212f6f4"></a>
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

<a id="ea81c930bd004ca1"></a>
##### KISA_VERIFY_FUNCTION

Korea Internet & Security Agency (KISA)의 비밀번호 검증 방법이다.

- 8 글자 이상
- 1 개 이상의 문자
- 1 개 이상의 숫자
- 1 개 이상의 특수 문자

<a id="0450afbc5cefc512"></a>
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

<a id="bdfe40bd157d53f8"></a>
##### ORA12C_STRONG_VERIFY_FUNCTION

Oracle의 ORA12C_STRONG_VERIFY_FUNCTION 비밀번호 검증 방법이다.

- 9 글자 이상
- 2 개 이상의 대문자 
- 2 개 이상의 소문자 
- 2 개 이상의 숫자 
- 2 개 이상의 특수 문자 
- 이전 비밀번호와 적어도 4 글자는 달라야 한다.

<a id="86be3dffbe6d999c"></a>
##### VERIFY_FUNCTION_11G

Oracle의 VERIFY_FUNCTION_11G 비밀번호 검증 방법이다.

- 8 글자 이상
- 1 개 이상의 문자 
- 1 개 이상의 숫자 
- 사용자 이름을 포함하면 안된다. 
- 이전 비밀번호와 적어도 3 글자는 달라야 한다.

<a id="a9abb6a818b8317f"></a>
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

<a id="cef5fe0554d83679"></a>
### 설명

<a id="7471dae06db7bc73"></a>
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

<a id="73c3e0098cd71b4a"></a>
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

<a id="ba2ce826bab484ab"></a>
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

<a id="3ad7fa79ef4dff9a"></a>
#### 비밀번호 재사용 가능 여부

비밀번호 재사용 가능 여부에 영향을 주는 parameter는 다음과 같다.

- PASSWORD_REUSE_MAX
- PASSWORD_REUSE_TIME

두 parameter의 비밀번호 재사용 가능 여부는 다음 표와 같다.

**비밀번호 재사용 가능 조건**

<a id="19ce08e3a241c7f0"></a>
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

<a id="6cdd935f1dd1e838"></a>
| password | password_date | 재사용 가능 여부 |
| --- | --- | --- |
| P#_000001 | 2015-08-01 | 가능 |
| P#_000002 | 2015-08-02 | 가능 |
| P#_000003 | 2015-08-03 | REUSE_MAX 위반 |
| P#_000004 | 2015-08-04 | REUSE_MAX 위반 |
| P#_000005 | 2015-08-05 | REUSE_MAX, REUSE_TIME 위반 |
| P#_000006 | 2015-08-06 | REUSE_MAX, REUSE_TIME 위반 |
| P#_000007 | 2015-08-07 | REUSE_MAX, REUSE_TIME 위반 |

비밀번호 재사용 가능 여부를 검사하기 위해 누적된 비밀번호 변경 이력은 다음 구문을 사용하여 삭제할 수 있다.

```
ALTER DATABASE CLEAR PASSWORD HISTORY;
```

<a id="8d99236c0f311871"></a>
#### DEFAULT profile

Database를 생성할 때 다음과 같은 "DEFAULT" profile을 자동으로 생성한다. 생성하는 "DEFAULT" profile 의 password parameter 정보는 다음과 같다.

**DEFAULT profile의 구성**

<a id="4412b46b9fa7fc1e"></a>
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
    - 10 (FAILED_LOGIN_ATTEMPTS) 번 연속으로 login에 실패할 경우 1일 (PASSWORD_LOCK_TIME) 동안 계정을 잠근다.
- 비밀번호 만료
    - 180일 (PASSWORD_LIFE_TIME)이 경과된 후에 7일 (PASSWORD_GRACE_TIME)의 유예 기간이 지나면 비밀번호가 만료된다.
- 비밀번호 재사용 가능 여부
    - 이전 비밀번호를 재사용할 수 있다.
- 비밀번호 복잡도 검사
    - 검사하지 않는다.

DEFAULT profile은 삭제할 수 없고 다음 구문으로 변경은 가능하다.

```
ALTER PROFILE DEFAULT LIMIT ...
```

<a id="bab427b92e8d78e3"></a>
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

<a id="239a0bb560f76f8f"></a>
### 호환성

SQL 표준은 profile에 대한 개념을 다루지 않고 있다.

<a id="c5c56acfa989eb36"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP PROFILE](#b370f178d1d3dd6a)
- [ALTER PROFILE](#e26c5af4933c1efe)
- [CREATE USER](#339657c579ea782f)
- [ALTER USER](#c2d86feb760d5ff5)
- [ALTER DATABASE CLEAR PASSWORD HISTORY](#028c9fbaca0d67cf)

<a id="d4b396bf1d68ca78"></a>
## CREATE SCHEMA

<a id="69e1f0a39bee736a"></a>
### 기능

스키마를 정의한다.

<a id="27c66088208cc5de"></a>
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

<a id="a2a578ddd782f199"></a>
### 사용 범위 및 접근 권한

&lt;schema definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 스키마를 생성하려면 CREATE SCHEMA ON DATABASE 권한이 있어야 한다.

- &lt;schema element&gt;가 존재할 경우, 각 &lt;schema element&gt; 구문을 수행하기 위한 권한이 있어야 한다.  
  자세한 내용은 다음 각 구문의 *사용 범위 및 접근 권한*을 참조한다.
    - [CREATE TABLE](#1586c5952309fa38) 
    - [CREATE VIEW](#69be25aa5896b17e) 
    - [CREATE INDEX](#ce4afb58f69a16f7) 
    - [CREATE SEQUENCE](#cdaeabbec6dc28f1) 
    - [GRANT privileges TO](#7961f4f3fe98c65c) 
    - [COMMENT ON name IS](#864dfa43b0df5050)

- user_identifier에 해당하는 사용자는 생성한 스키마에 대해 다음과 같은 권한을 갖는다.
    - 생성한 schema_name 스키마의 소유자 
    - &lt;schema element&gt; 절로 생성된 객체의 소유자

- 생성한 스키마에 별도의 권한을 부여하지 않으므로 객체를 생성하려면 적절한 스키마 권한을 부여받아야 한다.  
  스키마 권한의 종류에 대한 내용은 GRANT privileges TO 구문의 [&lt;schema privilege&gt;](#3aa491f1275cabe3)를 참조한다.  
  [사용 예](#d521d50773e5f06f)는 CREATE USER 구문을 참조한다.

<a id="9462273ff9ae6763"></a>
### 구문 규칙 및 파라미터

<a id="e42931ff6ff011db"></a>
#### schema_name

생성할 스키마의 이름이다.  
Database 내에 동일한 스키마 이름이 존재하지 않아야 한다.  
스키마 이름의 길이는 128 바이트보다 작아야 한다.

<a id="e16c8bb9bb23b222"></a>
#### AUTHORIZATION user_identifier

스키마 이름을 생략할 경우, user_identifier와 동일한 이름의 스키마를 생성한다.  
AUTHORIZATION을 지정하지 않을 경우, 구문을 수행한 사용자의 user_identifier가 사용된다.

<a id="6a69e1c37b77c309"></a>
#### schema_name AUTHORIZATION user_identifier

생성할 스키마 이름과 스키마의 소유자를 지정한다.  
소유자는 role이나 PUBLIC이 될 수 없다.

<a id="9fb4760701511954"></a>
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

<a id="adf324a034d63fb8"></a>
### 설명

스키마는 table, view, index, sequence, constraint와 같은 SQL schema 객체들을 논리적으로 분류하는 객체이다.

GOLDILOCKS에서 user와 schema의 관계는 1 : N이다. 즉, user가 소유한 schema가 존재하지 않거나 user가 다수의 schema를 소유할 수 있다.

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

<a id="220ad12be5c2280c"></a>
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

<a id="268be8c28ef98d67"></a>
### 호환성

**SQL 표준 호환성**

<a id="c9f88be5d30a1bf6"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| S071 | SQL paths in function and type name resolution | X |
| F461 | Named character sets | X |
| F171 | Multiple schemas per user | O |
| T332 | Extended roles | X |

<a id="e4add95e9e37b9dd"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP SCHEMA](#c2e1f942afbed8da)
- [CREATE USER](#339657c579ea782f)
- [CREATE TABLE](#1586c5952309fa38)
- [CREATE VIEW](#69be25aa5896b17e)
- [CREATE INDEX](#ce4afb58f69a16f7)
- [CREATE SEQUENCE](#cdaeabbec6dc28f1)
- [GRANT privileges TO](#7961f4f3fe98c65c)
- [COMMENT ON name IS](#864dfa43b0df5050)

<a id="cdaeabbec6dc28f1"></a>
## CREATE SEQUENCE

<a id="886ac54299643003"></a>
### 기능

시퀀스를 생성한다.

<a id="9a6dd520c6cf1498"></a>
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

<a id="173fa69b12496802"></a>
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

<a id="22beb1fcd0d55400"></a>
### 구문 규칙 및 파라미터

<a id="6b614a6bf3e6158a"></a>
#### sequence_name

생성할 시퀀스의 이름이며 스키마 내에서 유일한 이름이어야 한다.  
schema_name.sequence_name과 같이 시퀀스가 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
시퀀스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="4c719231d40892cc"></a>
#### &lt;sequence generator option&gt;

&lt;sequence generator option&gt;을 사용하지 않을 경우 다음 두 문장은 같은 의미를 갖는다.

- CREATE SEQUENCE test_seq; 
- CREATE SEQUENCE test_seq START WITH 1 INCREMENT BY 1 NO MINVALUE NO MAXVALUE NO CYCLE CACHE 20;

<a id="b084b2c450d9b469"></a>
#### &lt;sequence generator start with option&gt;

첫 번째로 생성할 시퀀스 번호를 정의한다.  
오름차순인지 내림차순인지에 따라 다음과 같은 특징을 갖는다.

- 오름차순 시퀀스일 경우 (INCREMENT BY 양수) 
    - 최소값보다 큰 시퀀스 값으로 시작하고자 할 경우에 사용한다. 
    - START WITH 절을 생략할 경우, 기본값은 최소값 (MINVALUE value)이 된다. 
- 내림차순 시퀀스일 경우 (INCREMENT BY 음수) 
    - 최대값보다 작은 시퀀스 값으로 시작하고자 할 경우에 사용한다. 
    - START WITH 절을 생략할 경우, 기본값은 최대값 (MAXVALUE value)이 된다.

<a id="f345415422748c54"></a>
#### &lt;sequence generator increment by option&gt;

시퀀스 번호의 간격을 정의한다.  
다음과 같은 제약 및 특징을 갖는다.

- 양수 또는 음수를 사용할 수 있으며, 0은 사용할 수 없다. 
- 간격의 절대값은 MINVALUE와 MAXVALUE의 차이보다 작아야 한다. 
- 양수일 경우 오름차순 시퀀스가 생성되며 음수일 경우 내림차순 시퀀스가 생성된다. 
- INCREMENT BY 절을 생략할 경우, 기본값은 양수 1 이다.

<a id="8408be30560b338b"></a>
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

<a id="702f1f9f430f2009"></a>
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

<a id="22961786252c90fa"></a>
#### &lt;sequence generator cycle option&gt;

시퀀스의 값이 최대값 또는 최소값이 되었을 때, 계속 값을 생성할지 여부를 명시한다.

- CYCLE 
    - 오름차순 시퀀스가 최대값이 되었을 때, 최소값부터 다시 생성한다. 
    - 내림차순 시퀀스가 최소값이 되었을 때, 최대값부터 다시 생성한다. 
- NO CYCLE | NOCYCLE 
    - 최대값 또는 최소값이 되었을 때, 시퀀스 값을 생성할 수 없다. 
    - NO CYCLE (SQL 표준)과 NOCYCLE은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다. 
- CYCLE과 NO CYCLE을 명시하지 않을 경우, 기본값은 NO CYCLE 이다.

<a id="aed335269dc3747d"></a>
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

<a id="5b4ae2e6d6a66a2a"></a>
### 설명

생성한 시퀀스 객체의 시퀀스 값은 [NEXTVAL](11-sql-elements.md#70c21c39c64fbe45) 함수와 [CURRVAL](11-sql-elements.md#49d99dc28cf285f7) 함수를 이용하여 사용할 수 있다.

시퀀스 값은 트랜잭션 속성을 가지지 않으며, 시퀀스 함수를 사용한 SQL 구문에서 에러가 발생하거나 명시적인 ROLLBACK을 수행하더라도 시퀀스 값은 가장 최신 값을 유지한다.

CURRVAL 함수의 경우, session에서 가장 최근에 호출한 NEXTVAL 값을 반환한다.   
이러한 특성을 이용하면 NEXTVAL을 이용하여 한 번 얻은 시퀀스 값을 다른 SQL 문장에 계속 사용할 수 있다.  단, session에서 NEXTVAL을 호출하지 않은 경우에 CURRVAL를 사용하면 에러가 발생한다.

<a id="44b1431c3be850cf"></a>
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

<a id="15e0c3ee677f7054"></a>
### 호환성

SQL 표준에서는 &lt;sequence generator cache option&gt; 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="61a4c18272e8adb6"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="0fefdc048accd776"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP SEQUENCE](#7debf989c0a88d02)
- [ALTER SEQUENCE](#9fd8a84df33183e1)
- [NEXTVAL](11-sql-elements.md#70c21c39c64fbe45)
- [CURRVAL](11-sql-elements.md#49d99dc28cf285f7)

<a id="63dc86c3ac2b8f57"></a>
## CREATE SYNONYM

<a id="2473ad2d2b5b8683"></a>
### 기능

Synonym을 생성한다. Synonym은 테이블, view, 시퀀스, 또다른 synonym의 대체 이름으로써 이들 대신 다음 구문에서 사용될 수 있다.

- DML: SELECT, INSERT, UPDATE, DELETE, LOCK TABLE, CALL
- DDL: GRANT, REVOKE, COMMENT

<a id="8e1945453cb7f1a8"></a>
### 구문

```
<table definition> ::=    
    CREATE [OR REPLACE] [PUBLIC] SYNONYM [schema_name.]synonym_name 
    FOR [schema_name.]object_name
    ;
```

<a id="99e5f2f3ad7a7c11"></a>
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

<a id="12bacf577657f99f"></a>
### 구문 규칙 및 파라미터

<a id="6f2ab0d5325ca6ab"></a>
#### [ OR REPLACE ]

이미 synonym이 존재할 경우, 기존의 synonym을 대체한다.

<a id="d64a508fa6bd6f29"></a>
#### [ PUBLIC ]

Public synonym을 만들기 위해 명시한다.  
이 절을 생략하면 private synonym이 생성된다.

<a id="c01848b765caa2c4"></a>
#### synonym_name

생성할 synonym의 이름이며, 스키마 내에서 유일한 이름이어야 한다.  
schema_name.synonym_name과 같이 synonym이 소속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
Synonym 이름의 길이는 128 바이트보다 작아야 한다.  
Public synonym은 non-schema 객체이다. 따라서 PUBLIC을 명시하여 public synonym을 생성할 때는 스키마 이름을 명시할 수 없다.

<a id="d8741de936d999c1"></a>
#### object_name

schema_name.object_name과 같이 객체가 소속된 스키마를 명시할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

object_name을 명시할 수 있는 객체 타입은 다음과 같다.

- Table
- View
- Sequence
- 또 다른 synonym

대상 객체의 존재 여부, cycle check, 권한 검사 등은 synonym을 사용한 구문을 수행할 때 실행된다.

<a id="e8cd4faa0a2f620b"></a>
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

<a id="e15674b62be0fbaf"></a>
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

<a id="929399378ad6ec86"></a>
### 호환성

SQL 표준에서는 CREATE SYNONYM 구문을 정의하지 않고 있다.

<a id="d3c323106725e88f"></a>
### 참조

관련 내용은 [DROP SYNONYM](#fb9ded8027c5c9fe)을 참조한다.

<a id="1586c5952309fa38"></a>
## CREATE TABLE

<a id="58194e4abc3b5ece"></a>
### 기능

테이블을 정의한다.

<a id="d6591236b6c5d983"></a>
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
    | <logging clause>


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

<logging clause> ::=
      LOGGING
    | NOLOGGING


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

<a id="1fa54ca5f0de1d1b"></a>
### 사용 범위 및 접근 권한

Database가 standalone 인지 아니면 cluster 인지에 따라 다음과 같은 차이가 있다

- Standalone
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

<a id="2b6fbf1c106c5f4f"></a>
### 구문 규칙 및 파라미터

<a id="6f9dc1adf76a9c6b"></a>
#### table_name

생성할 테이블의 이름이며, 스키마 내에서 유일한 이름이어야 한다.  
schema_name.table_name과 같이 테이블이 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
테이블 이름의 길이는 128 바이트보다 작아야 한다.

<a id="69910076524eddf1"></a>
#### &lt;column definition&gt;

테이블을 구성할 column을 정의한다.  
테이블은 하나 이상의 column에 대한 정의를 포함해야 한다.  
Column의 데이터 타입, 기본값, 자동 생성 값, 제약 조건 등을 기술할 수 있다.

<a id="d8564daddb834619"></a>
#### column_name

테이블을 구성할 column의 이름으로 각 column은 테이블 내에서 유일한 이름을 가져야 한다.  
Column 이름의 길이는 128 바이트보다 작아야 한다.

<a id="43193fcb4b491d07"></a>
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
데이터 타입과 관련한 자세한 내용은 [Data Type](11-sql-elements.md#ff81d005bda1af76) 정의를 참조한다.

<a id="6ab5043305c1d010"></a>
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

<a id="1e61cbf2a5195777"></a>
#### [ &lt;default clause&gt; | &lt;identity column specification&gt; ]

Column의 기본값을 명시한다.  
&lt;default clause&gt;와 &lt;identity column specification&gt;은 함께 사용할 수 없다.  
모두 생략할 경우, 기본값은 NULL이다.

<a id="7d047626d6bea974"></a>
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

타입이 호환되지 않거나 공간이 부족한 경우 INSERT, UPDATE 구문에서 DEFAULT를 사용할 때 다음과 같은 에러가 발생한다.

- CREATE TABLE t1 ( user_name VARCHAR(1) DEFAULT CURRENT_USER ); 
- 예) error: INSERT INTO t1 VALUES (DEFAULT); 
- 예) error: UPDATE t1 SET user_name = DEFAULT;

DEFAULT expression은 모든 built-in 함수를 사용할 수 있지만 다음은 사용할 수 없다.

- 논리연산자 (AND, OR, NOT), 비교 연산자 (=, >, ..)
- Stored function 
- Column 이름 
- Subquery expression

<a id="ac322431fea8d204"></a>
#### &lt;identity column specification&gt;

자동 생성값을 갖는 column을 정의한다.

테이블은 하나의 identity column만 가질 수 있다.  
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

identity column 생성 옵션인 &lt;common sequence generator option&gt;과 &lt;basic sequence generator option&gt;에 대한 자세한 내용은 [CREATE SEQUENCE](#cdaeabbec6dc28f1) 구문을 참조한다.

<a id="de5b1ec1cbcb1936"></a>
#### &lt;column constraint definition&gt;

Column에 대해 다음과 같은 제약 조건을 정의한다.

- NOT NULL 제약 조건 
- UNIQUE 제약 조건 
- PRIMARY KEY 제약 조건

<a id="81a4c99a5e974cc6"></a>
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

<a id="49a080811a6a9f6e"></a>
#### NOT NULL 제약 조건

Column 값으로 NULL 값을 허용하지 않는다.

<a id="bd8096819e29f0cb"></a>
#### UNIQUE 제약 조건

Column 값으로 동일한 값을 허용하지 않는다.  
단, NULL 값은 허용한다.

<a id="ec8549a39d58e16b"></a>
#### PRIMARY KEY 제약 조건

Column 값으로 NULL 값이나 동일한 값을 허용하지 않는다.  
하나의 테이블에 하나의 PRIMARY KEY 제약 조건을 정의할 수 있다.

<a id="5d7387c2de34cdcc"></a>
#### &lt;index name clause&gt;

UNIQUE 제약 조건, PRIMARY KEY 제약 조건을 정의할 때 생성되는 인덱스의 이름을 정의한다.

- INDEX index_name 
    - 제약 조건을 위한 인덱스의 이름을 정의한다. 
    - 스키마 이름과 함께 사용할 수 없으며, 제약 조건과 동일한 스키마에 생성된다.

UNIQUE 제약 조건, PRIMARY KEY 제약 조건을 정의할 때 INDEX 절을 생략할 경우에는 제약 조건에 부합하는 인덱스를 자동으로 생성한다.  
자동 생성되는 인덱스 이름으로는 "constraint_name" + "_INDEX"가 부여된다.

- &lt;index attributes&gt; 
    - 생성할 인덱스의 물리적 속성을 지정한다. 
    - 자세한 내용은 [CREATE INDEX](#ce4afb58f69a16f7) 구문을 참조한다. 
- TABLESPACE index_tablespace_name 
    - 인덱스를 생성할 tablespace를 지정한다. 
    - 자세한 내용은 [CREATE INDEX](#ce4afb58f69a16f7)을 참조한다.

<a id="8faec2bdf9d76b72"></a>
#### &lt;table constraint definition&gt;

- &lt;unique constraint definition&gt;

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

<a id="1541aa5b2c9010b5"></a>
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

<a id="969e7eca34183826"></a>
#### &lt;table sharding strategy&gt;

테이블의 sharding 정책을 정의한다.  
다음과 같은 네 가지 정책 중 하나로 정의할 수 있다.

- &lt;cloned strategy&gt; 
- &lt;hash sharding strategy&gt; 
- &lt;range sharding strategy&gt; 
- &lt;list sharding strategy&gt;

생략할 경우 [DEFAULT_SHARDING](../part-02-administration-manual/10-server-property.md#df566c03eeccec67) 프로퍼티 값에 의해 결정된다.

- DEFAULT_SHARDING 값이 0 인 경우
    - &lt;cloned strategy&gt;
- DEFAULT_SHARDING 값이 1 인 경우
    - &lt;hash sharding strategy&gt;

<a id="6467452600c61cda"></a>
#### &lt;cloned strategy&gt;

테이블의 모든 data를 복제한다.

<a id="0d6f1be1da782980"></a>
#### &lt;clone placement&gt;

Clone의 배치 정책을 정의한다.

- AT CLUSTER WIDE 
    - Cluster system의 모든 cluster group의 모든 cluster member에 clone을 배치한다. 
    - Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef) 구문을 사용하여 clone을 재배치할 수 있다. 
- AT CLUSTER GROUP group_list 
    - 지정한 cluster group들의 모든 cluster member에 clone을 배치한다. 
    - 지정된 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef) 구문을 사용하여 clone을 재배치할 수 있다. 
    - Cluster group 추가는 clone의 재배치에 영향을 주지 않는다.
- 생략할 경우, 기본값은 AT CLUSTER WIDE이다.

<a id="93007f8b4376d3ac"></a>
#### &lt;hash sharding strategy&gt;

테이블 data를 sharding key의 hash 값을 기준으로 shard 분할한다.

<a id="da8f954b117f3ca3"></a>
#### SHARDING BY [HASH] ( column_list )

Hash sharding을 위한 sharding key를 정의한다.

- Column을 32 개까지 나열할 수 있다. 
- 동일한 column은 사용할 수 없다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column은 사용할 수 없다.

<a id="3658b67519a53a63"></a>
#### &lt;hash shard count&gt;

분할할 hash shard의 개수를 정의한다.  
Shard의 개수는 1부터 512까지 정의할 수 있다.  
생략할 경우 기본값은 24이다.

<a id="447f51bdee31050f"></a>
#### &lt;hash shard placement&gt;

Hash shard의 배치 정책을 정의한다.

- AT CLUSTER WIDE 
    - Cluster system의 모든 cluster group의 모든 cluster member에 shard들을 배치한다. 
    - Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef) 구문을 사용하여 shard들을 재배치할 수 있다. 
- AT CLUSTER GROUP group_list 
    - 지정한 cluster group들의 모든 cluster member에 hash shard들을 배치한다. 
    - group_list의 개수는 &lt;hash shard count&gt;의 값과 같거나 작아야 한다. 
    - range shard, list shard와 달리 hash shard는 특정 shard가 배치될 cluster group을 지정할 수 없으며, system이 자동으로 shard들을 배치할 cluster group을 결정한다. 
    - 지정한 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef) 구문을 사용하여 shard를 재배치할 수 있다. 
    - Cluster group 추가는 hash shard의 재배치에 영향을 주지 않는다.
- 생략할 경우, 기본값은 AT CLUSTER WIDE 이다.

<a id="0185c199bb3419e4"></a>
#### &lt;range sharding strategy&gt;

테이블의 data를 sharding key의 범위값을 기준으로 shard 분할한다.

<a id="7066cd78e96aa9ae"></a>
#### SHARDING BY RANGE ( column_list )

Range sharding을 위한 sharding key를 정의한다.

- Column을 32 개까지 나열할 수 있다. 
- 동일한 column은 사용할 수 없다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column은 사용할 수 없다.

<a id="f2819f40e6fb0f6b"></a>
#### &lt;cluster-wide range shard placement&gt;

Range shard들을 cluster system의 모든 cluster group으로 자동으로 배치한다.  
&lt;range shard definition&gt;을 기술하기 전에 AT CLUSTER WIDE 구문을 기술한다.  
Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef) 구문을 사용하여 자동으로 shard 들을 재배치할 수 있다.

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

<a id="4a268efc41859bb1"></a>
#### &lt;group-specific range shard placement&gt;

Range shard들을 지정한 cluster group에 배치한다.  
&lt;range shard definition&gt;과 함께 해당 shard를 배치할 AT CLUSTER GROUP group_name 구문을 기술한다.  
지정한 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.  
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

<a id="c5ebc31779b90c03"></a>
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

- MAX shard를 포함하지 않는 경우 error가 발생한다.

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

<a id="222f3e7909ad7358"></a>
#### &lt;range value clause&gt;

&lt;range value&gt;는 상수값이거나 최대값을 의미하는 MAXVALUE여야 한다.

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

<a id="c13d8e9339583aa5"></a>
#### &lt;list sharding strategy&gt;

테이블 data를 sharding key의 나열값을 기준으로 shard 분할한다.

<a id="af6273d5647f3350"></a>
#### SHARDING BY LIST ( column_name )

List sharding을 위한 sharding key를 정의한다.

- 하나의 column만 사용할 수 있다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column을 사용할 수 없다.

<a id="4674f2b7c869ae11"></a>
#### &lt;cluster-wide list shard placement&gt;

Cluster system의 모든 cluster group에 list shard들을 자동으로 배치한다.  
&lt;list shard definition&gt;을 기술하기 전에 AT CLUSTER WIDE 구문을 기술한다.  
Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.

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

<a id="4fcea6857c1bd616"></a>
#### &lt;group-specific list shard placement&gt;

List shard들을 지정한 cluster group에 배치한다.  
&lt;list shard definition&gt;과 함께 해당 shard를 배치할 AT CLUSTER GROUP group_name 구문을 기술한다.  
지정한 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#9a20bc4c3fbf08ef) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.  
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

<a id="a8c53ab0974a2107"></a>
#### &lt;list shard definition&gt;

LIST list_name 은 테이블 내에서 유일해야 한다.

최대 512개의 &lt;list shard definition&gt;을 정의할 수 있다.  
나열된 &lt;list shard definition&gt;의 모든 &lt;list value&gt; 값이 서로 달라야 한다.

DFFAULT는 나열된 모든 &lt;list value&gt;를 제외한 나머지 값이다.  
DEFAULT는 다른 값과 함께 지정할 수 없다.  
DEFAULT를 포함하는 shard를 DEFAULT shard라고 한다.

DEFAULT shard는 반드시 존재해야 하며, 하나만 존재해야 한다.

- DEFAULT shard를 포함해야 한다.

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

<a id="9dd208dc1998e067"></a>
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

<a id="570431608525411e"></a>
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

<a id="a59a35efcf17dae7"></a>
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

<a id="7ecead360449bc19"></a>
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

<a id="a060362f53e8e30a"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="5b06e8bb513bf223"></a>
#### TABLESPACE tablespace_name

테이블이 저장될 tablespace의 이름을 지정한다.  
TABLESPACE 절을 생략할 경우, 구문을 수행하는 사용자의 기본 tablespace_name을 사용한다.

<a id="168d04bb2f595eca"></a>
#### LOGGING | NOLOGGING

인덱스의 리두 로깅 수행 여부를 명시한다.  
명시하지 않을 경우, 기본값은 NOLOGGING이다.

<a id="c5beea7eec79f03c"></a>
#### TABLESPACE index_tablespace_name

인덱스가 저장될 tablespace의 이름을 지정한다.  
TABLESPACE 절을 생략할 경우, LOGGING 인덱스는 사용자의 기본 데이터 테이블스페이스를 사용하고, NOLOGGING 인덱스는 사용자의 기본 임시 테이블스페이스를 사용한다.

<a id="58275032d55dbe94"></a>
#### &lt;constraint characteristics&gt;

제약 조건의 특성을 정의한다.  
제약 조건을 정의할 때 다음과 같은 특성들을 설정할 수 있다.

- 제약 조건의 지연가능성 ( DEFERRABLE | NOT DEFERRABLE )
- 제약 조건의 검사시점 (&lt;constraint check time&gt; )

&lt;constraint characteristics&gt;를 생략할 경우, NOT DEFERRABLE INITIALLY IMMEDIATE로 설정한다.

<a id="59d300841df31e48"></a>
#### DEFERRABLE | NOT DEFERRABLE

제약 조건을 DML을 수행할 때 검사하지 않고, COMMIT을 수행할 때 검사할 수 있게 지연시킬 수 있는지 여부를 설정한다.

지연 가능한 제약 조건의 검사시점은 [SET CONSTRAINTS](#8e1fec980aea373d) 구문으로 제어한다.

- NOT DEFERRABLE
    - 검사 시점을 지연시킬 수 없으며, INSERT, DELETE, UPDATE 구문을 수행할 때 제약 조건을 검사한다.
- DEFERRABLE
    - 검사 시점을 [SET CONSTRAINTS](#8e1fec980aea373d) 구문으로 제어할 수 있다.
    - SET CONSTRAINTS constraint_name IMMEDIATE
        - DML을 수행할 때 제약 조건을 검사한다.
    - SET CONSTRAINTS constraint_name DEFERRED
        - COMMIT을 수행할 때 제약 조건을 검사한다.
- 명시하지 않을 경우 기본값은 &lt;constraint check time&gt;에 따라 결정된다.
    - INITIALLY IMMEDIATE를 명시한 경우, NOT DEFERRABLE 이다. 
    - INITIALLY DEFERRED를 명시한 경우, DEFERRABLE 이다.
    - &lt;constraint check time&gt;을 명시하지 않은 경우, NOT DEFERRABLE 이다.

<a id="eb4673b6b5cc605b"></a>
#### &lt;constraint check time&gt;

지연 가능한 (DEFERRABLE) 제약 조건일 경우, 검사 시점의 초기값을 설정한다.

- INITIALLY IMMEDIATE
    - DML을 수행할 때 제약 조건을 검사한다.
- INITIALLY DEFERRED
    - COMMIT을 수행할 때 제약 조건을 검사한다.
    - NOT DEFERRABLE과 함께 사용할 수 없다.
- 명시하지 않을 경우, 기본값은 INITIALLY IMMEDIATE 이다.

지연 가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](#8e1fec980aea373d) 구문을 참조한다.

<a id="7b8cc481c35205f4"></a>
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

<a id="a2e66fc6fb58033e"></a>
### 설명

<a id="276006a5c95a954c"></a>
#### 제약 조건의 특성

GOLDILOCKS는 key 제약 조건을 생성할 때 uniqueness 검사를 하기 위해 자동으로 index를 생성한다.

다음과 같은 column은 NULL 값을 허용하지 않는다.

- NOT NULL 제약 조건이 있는 column
- Primary key 제약 조건에 포함되는 column
- Identity column

<a id="4c122402b2a529e1"></a>
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

<a id="0f7d23a191c79bd5"></a>
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

다음은 테이블 생성할 때 column에 제약 조건을 기술하는 예이다.

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

다음은 테이블 생성할 때 여러 column을 포함하는 제약 조건을 기술하는 예이다.

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

다음은 cluster-wide hash sharded table을 정의하는 예이다. 테이블의 데이터가 ps_partkey column의 hash 값에 의해 24개의 shard로 분할되며, 각 shard는 cluster system 전체에 자동으로 배치된다.

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

다음은 group-specific hash sharded table을 정의하는 예이다. 테이블의 데이터가 ps_partkey column의 hash 값에 의해 24개의 shard로 분할되며, 각 shard는 지정한 cluster group g2, g3에 자동으로 배치된다.

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

테이블 T1을 생성한 후에 테이블 T1의 global secondary index를 생성한다.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) )  WITH GLOBAL SECONDARY INDEX;

Table created.
```

테이블 T1을 생성한 후에 테이블 T1의 global secondary index를 tablespace 'USER_DATA_TBS'에 logging option으로 생성한다.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) ) 
      WITH GLOBAL SECONDARY INDEX
      LOGGING TABLESPACE USER_DATA_TBS;

Table created.
```

테이블 T1을 생성한 후에 테이블 T1의 global secondary index를 tablespace 'USER_TEMP_TBS'에 nologging option으로 생성한다.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) ) 
      WITH GLOBAL SECONDARY INDEX
      NOLOGGING TABLESPACE USER_TEMP_TBS;

Table created.
```

<a id="bc0c79310cb4582b"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- TABLESPACE 절, &lt;physical attribute clause&gt; 절 등의 물리적 개념
- SQL 표준은 DEFAULT 절에 연산을 사용할 수 없다.

**SQL 표준 호환성**

<a id="2b9f83bb93ee53c6"></a>
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

<a id="478edce9f35fcaa5"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLE](#44de11d586092a30)
- [ALTER TABLE](#16da97b62af765de)
- [CREATE TABLESPACE](#df51248e3216ce23)
- [CREATE SCHEMA](#d4b396bf1d68ca78)
- [CREATE INDEX](#ce4afb58f69a16f7)
- [CREATE SEQUENCE](#cdaeabbec6dc28f1)
- [SET CONSTRAINTS](#8e1fec980aea373d)
- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#734ad801c6d6f26f)

<a id="35d451a03dc1a47a"></a>
## CREATE TABLE AS SELECT

<a id="75ef1435611394fd"></a>
### 기능

질의 결과로부터 새로운 테이블을 생성한다.

<a id="a7600ca78450b18b"></a>
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

<a id="af27d0a476dde5e1"></a>
### 사용 범위 및 접근 권한

&lt;table definition:AS query expression&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블 생성 권한
    - [CREATE TABLE](#1586c5952309fa38) 구문의 접근 권한을 참조한다.
- SELECT 접근 권한 
    - [SELECT](#c9d76bf073f60db2) 구문의 접근 권한을 참조한다.

<a id="86de9380c977a30f"></a>
### 구문 규칙 및 파라미터

<a id="6aedf43a5ce84720"></a>
#### table_name

생성할 테이블의 이름이다.  
자세한 내용은 [table_name](#6f9dc1adf76a9c6b) 구문을 참조한다.

<a id="80f8733a628767c0"></a>
#### column_name_list

테이블을 구성할 column의 이름으로써 테이블 내에서 유일한 이름이어야 하며, column의 개수는 SELECT 절의 결과 column 개수와 동일해야 한다.   
명시하지 않을 경우, &lt;query expression&gt;의 SELECT 절의 column 이름을 사용한다.

단, SELECT절에 column이 아닌 expression (function, operation, subquery 등)이 오면 alias 또는 column name을 명시해야 한다.

Column 이름의 길이는 128 바이트보다 작아야 한다.

<a id="43d7075f7da820c6"></a>
#### WITH [NO] DATA

WITH DATA가 명시된 경우, SELECT 절의 결과가 생성될 테이블에 INSERT 된다.   
WITH NO DATA가 명시된 경우, SELECT 절의 결과가 생성될 테이블에 INSERT 되지 않는다.   
명시하지 않을 경우, WITH DATA를 명시한 것과 동일하게 작동한다.

<a id="d5b193045ff96a18"></a>
#### other syntax

이 외의 구문 규칙은 [CREATE TABLE](#1586c5952309fa38) 구문의 syntax를 참조한다.

<a id="f18e55aab5e06fe3"></a>
### 설명

CREATE TABLE AS SELECT 구문을 수행할 때 SELECT list에 NOT NULL 제약 조건이 있는 column이 명시된 경우, 새로운 테이블에도 NOT NULL 제약 조건이 생성된다.  단, 지연 가능한 NOT NULL 제약 조건인 경우, 새로운 테이블에는 NOT NULL 제약 조건을 생성하지 않는다.

그러나 명시적으로 NOT NULL 제약 조건을 생성한 것이 아니라, primary key, identity column과 같이 NOT NULL 속성을 가지고 있는 경우에는 새로운 테이블에 NOT NULL 제약 조건을 생성하지 않는다.

<a id="bf1a909af53dd4dd"></a>
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

<a id="acae90d3f19bf7f0"></a>
### 호환성

CREATE TABLE AS SELECT 구문은 SQL 표준을 따른다. 단, 다음은 표준에서 확장된 것이다.

- 표준에서 SELECT 절 밖의 괄호는 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- 표준에서 WITH [NO] DATA 절은 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- GOLDILOCKS의 tablespace 개념은 표준에 없는 확장 개념이다.

**SQL 표준 호환성**

<a id="d3d7a74adb77775a"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T172 | AS subquery clause in table definition | O |

<a id="d040fedbce56adaa"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](#1586c5952309fa38)
- [SELECT](#c9d76bf073f60db2)

<a id="cda0b9b5e565ed2c"></a>
## CREATE GLOBAL TEMPORARY TABLE

<a id="8439ea25f039b658"></a>
### 기능

새로운 global temporary table을 생성한다.

<a id="e1c11b9150426f1b"></a>
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

> &lt;table element&gt;의 정의는 &lt;table_definition&gt;의 정의와 동일하다. 자세한 내용은 [CREATE TABLE](#1586c5952309fa38) 을 참조한다.

<a id="2d7d8eada316311f"></a>
### 사용 범위 및 접근 권한

&lt;global temporary table definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블 생성 권한
    - [CREATE TABLE](#1586c5952309fa38) 구문의 접근 권한을 참조한다.
- SELECT 접근 권한 
    - [SELECT](#c9d76bf073f60db2) 구문의 접근 권한을 참조한다.

<a id="62fe9cb9790cdd8a"></a>
### 구문 규칙 및 파라미터

<a id="25739bc3ec872ff5"></a>
#### table_name

생성할 테이블의 이름이다.  
자세한 내용은 [table_name](#6f9dc1adf76a9c6b) 구문을 참조한다.

<a id="e239765fd915627d"></a>
#### other syntax

이 외의 구문 규칙은 [CREATE TABLE](#1586c5952309fa38) 및 [CREATE TABLE AS SELECT](#35d451a03dc1a47a) 구문의 syntax를 참조한다.

<a id="0b1555c29c1dfa0c"></a>
### 설명

GLOBAL TEMPORARY TABLE은 한 트랜잭션이나 세션이 실행되는 동안 유지될 데이터를 보관하는 용도로 사용하는 임시 테이블이다.  
개발자가 응용 프로그램을 개발할 때 연산 중간 데이터를 잠시 저장하는 변수와 같은 용도로 사용된다.

Global temporary table의 특징은 다음과 같다.

- Global temporary table의 정의는 모든 세션에서 볼 수 있다.
- Global temporary table을 정의할 때는 물리적 공간이 할당되지 않고, 처음으로 insert 할 때 해당 세션에 종속된 실제 공간 (segment)이 할당된다.
- Global temporary table의 데이터는 insert 한 세션이나 트랜잭션에서만 볼 수 있다.
- Global temporary table의 데이터가 저장되는 tablespace는 다음과 같이 결정된다.

<a id="dc55b8ba5e2c69ee"></a>
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

<a id="c8f21f91f9f42e1b"></a>
| Table commit action | 설명 |
| --- | --- |
| ON COMMIT PRESERVE ROWS | COMMIT 되거나 ROLLBACK 되어도 테이블에 남아있는 데이터를 그대로 유지한다. |
| ON COMMIT DELETE ROWS (default) | COMMIT 되거나 ROLLBACK 하는 시점에 테이블에 남아있는 데이터를 모두 삭제한다 (TRUNCATE). |

- 일반 테이블에 대한 대부분의 DDL을 지원한다. (ALTER, TRUNCATE 포함)
    - CLUSTER 관련 구문 (SHARD 및 global secondary index 관련 구문 등)은 지원하지 않는다.
    - 자신의 세션이나 다른 세션에서 현재 사용 중인 global temporary table에 대한 DDL은 오류를 발생시킨다.
    - 사용 중인 모든 세션에서 TRUNCATE TABLE이나 COMMIT 등으로 사용 중인 segment들을 모두 제거한 후에 DDL이 가능해진다.
- 일반 테이블에 대한 모든 DML과 select 구문을 지원한다.
- Global temporary table에 대한 모든 변경 (DML)은 redo log를 남기지 않는다.
- Global temporary table에 대한 모든 변경 (DML)은 undo log를 남기며, TEMP_UNDO_ENABLED 프로퍼티에 따라 undo log의 위치가 결정된다.

<a id="6c03708d71c0aee0"></a>
| TEMP_UNDO_ENABLED 값 | 설명 |
| --- | --- |
| TRUE | Database system의 default temporary tablespace에 undo log가 기록된다. |
| FALSE | Database system의 undo tablespace에 undo log가 기록된다. |

- Global temporary table에 대한 TRUNCATE 명령은 해당 세션의 segment만 truncate 한다.
- 세션이 종료되면 모든 segment들이 TRUNCATE 된 후에 반환된다.

<a id="afa54caaeb15f347"></a>
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

<a id="871ec7e586ee9e11"></a>
### 호환성

CREATE GLOBAL TEMPORARY TABLE과 CREATE GLOBAL TEMPORARY TABLE AS SELECT 구문은 SQL 표준의 &lt;table definition&gt; 정의를 따른다. 단, 다음은 표준에서 확장된 것이다.

- 표준에서 SELECT 절 밖의 괄호는 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- 표준에서 WITH [NO] DATA 절은 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- GOLDILOCKS의 tablespace 개념은 표준에 없는 확장 개념이다.

**SQL 표준 호환성**

<a id="17fb35f2f6300a34"></a>
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

<a id="5ac5f2db992e9f8a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](#1586c5952309fa38)
- [CREATE TABLE AS SELECT](#35d451a03dc1a47a)

<a id="df51248e3216ce23"></a>
## CREATE TABLESPACE

<a id="a74b29e9b865388a"></a>
### 기능

테이블스페이스를 생성한다.

<a id="34e3f93089395455"></a>
### 구문

```
<create tablespace statement> ::=
      <memory data tablespace statement>
    | <memory temporary tablespace statement>
    ;
```

<a id="f6b3094d44e284c4"></a>
### 사용 범위 및 접근 권한

&lt;create tablespace statement&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="3b92889e39433709"></a>
### 구문 규칙 및 파라미터

<a id="9306eed3c92d455d"></a>
#### &lt;memory data tablespace statement&gt;

- [ MEMORY ] TEMPORARY

질의 처리 과정에서 생성되는 중간 결과 등의 임시 객체나 no logging 인덱스를 저장할 메모리 임시 테이블스페이스이다.  
MEMORY 예약어는 생략할 수 있다.

<a id="5d1b53bcedef7723"></a>
#### &lt;memory data tablespace clause&gt;

메모리 데이터의 테이블스페이스를 정의한다.  
자세한 내용은 [CREATE MEMORY DATA TABLESPACE](#f34525feb7d5edf3) 구문을 참조한다.

<a id="75cd7a71c8c69e44"></a>
#### &lt;memory temporary tablespace definition&gt;

메모리의 임시 테이블스페이스를 정의한다.  
자세한 내용은 [CREATE MEMORY TEMPORARY TABLESPACE](#bb76a8ab84a10ae1) 구문을 참조한다.

<a id="0dcc5ae0ccae71c5"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="c1055621897d6051"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="b659ecc62b2c133a"></a>
### 호환성

SQL 표준은 tablespace에 대한 개념을 다루지 않고 있다.

<a id="2c42cef2fd2523e7"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#4aecf03632f3116f)
- [ALTER TABLESPACE](#c308f53537323289)

<a id="f34525feb7d5edf3"></a>
## CREATE MEMORY DATA TABLESPACE

<a id="9cd9e9dc28594def"></a>
### 기능

메모리 데이터의 테이블스페이스를 정의한다.

<a id="33b9d395e88c0ae2"></a>
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

<a id="92333b7ba9762432"></a>
### 사용 범위 및 접근 권한

&lt;memory data tablespace definition&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="ad139c52bc845b81"></a>
### 구문 규칙 및 파라미터

<a id="362df4b9cf8e6e3c"></a>
#### [ MEMORY ] [ DATA ]

테이블, 인덱스 등 영구적인 객체를 저장할 메모리 테이블스페이스이다.  
MEMORY와 DATA 예약어는 생략할 수 있다.

<a id="34c1ea49c3abc040"></a>
#### tablespace_name

생성할 테이블스페이스의 이름이다.  
테이블스페이스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="9ff428eddd0ab1da"></a>
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
        - 데이터 테이블스페이스의 경우 MEMORY_DATA_TABLESPACE_SIZE 프로퍼티에 의해 결정되고 
        - 임시 테이블스페이스의 경우 MEMORY_TEMP_TABLESPACE_SIZE 프로퍼티에 의해 결정된다.

- SIZE &lt;size clause&gt; REUSE 
    - SIZE 절과 REUSE 절을 모두 명시할 경우 filename의 존재 여부에 따라 다음과 같이 작동한다. 
        - 새로운 filename일 경우에는 SIZE 절을 이용해 초기 파일 크기를 지정한다. 
        - 이미 존재하는 filename일 경우에는 기존 파일을 이용하여 SIZE 절의 값으로 크기를 조정한다.

<a id="396187a22708785a"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="63b21e0c799a2de7"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="fd6f1bcc773631a7"></a>
#### ONLINE | OFFLINE

테이블스페이스 ONLINE/ OFFLINE 여부를 설정한다.

- ONLINE은 테이블스페이스를 생성하는 즉시 사용할 수 있는 상태이다. 
- OFFLINE은 사용 불가능한 상태이므로 ONLINE 상태로 변경한 후에 사용할 수 있다.

<a id="7d301bf6650e841c"></a>
#### EXTSIZE &lt;size clause&gt;

테이블스페이스의 extent 크기를 지정한다.

- Extent 크기는 바이트 단위로 기술하며, 다섯 가지 (64 K, 128 K, 256 K, 512 K, 1 M) 중 하나가 선택된다.
- 만약 extent 크기가 64 K ~ 128 K 사이의 값으로 지정되면 128 K로 설정되고, 1 M 이상으로 지정되면 1 M로 설정된다.

<a id="277c5b987a7d2aeb"></a>
### 설명

Data tablespace는 table, index (with LOGGING option) 등의 SQL schema 객체를 저장할 물리적 공간을 제공하는 객체이다.

<a id="d0f643378d7fdf27"></a>
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

<a id="55617331b1130834"></a>
### 호환성

SQL 표준은 테이블스페이스에 대한 개념을 다루지 않고 있다.

<a id="8cf84e6f1830608e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#4aecf03632f3116f)
- [ALTER TABLESPACE](#c308f53537323289)

<a id="bb76a8ab84a10ae1"></a>
## CREATE MEMORY TEMPORARY TABLESPACE

<a id="e02338d95207b702"></a>
### 기능

메모리의 임시 테이블스페이스를 정의한다.

<a id="96c9172acf4b9673"></a>
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

<a id="4660482e110d2434"></a>
### 사용 범위 및 접근 권한

&lt;memory temporary tablespace definition&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="17862e43b4eccb4f"></a>
### 구문 규칙 및 파라미터

<a id="943e38ee2fd0de79"></a>
#### [ MEMORY ] TEMPORARY

질의 처리 과정에서 생성되는 중간 결과 등의 임시 객체나 no logging 인덱스를 저장할 메모리 임시 테이블스페이스이다.  
MEMORY 예약어는 생략할 수 있다.

<a id="cbc4697b164adec8"></a>
#### tablespace_name

생성할 테이블스페이스의 이름이다.  
테이블스페이스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="64e4be923690a89b"></a>
#### &lt;memory clause&gt;

- 'memory_name' 
    - 임시 데이터를 저장할 메모리 이름이다.
    - memory_name은 해당 테이블스페이스 내에서 유일해야 한다.
    - memory_name의 길이는 1024 바이트보다 작아야 한다. 
- SIZE &lt;size clause&gt; 
    - 초기 크기를 지정한다. 
    - 최소 1 M ~ 최대 30 G 까지 지정할 수 있다.

<a id="340fe123acabc210"></a>
#### &lt;size clause&gt;

공유 메모리 공간의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)  
임시 메모리 데이터의 경우 이미지를 파일로 관리하지 않는다.

- K: Kilobytes
- M: Megabytes
- G: Gigabytes
- T: Terabytes

<a id="5e78eb2367a2552b"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="bc857c13f7160ad2"></a>
#### EXTSIZE &lt;size clause&gt;

테이블스페이스의 extent 크기를 지정한다.

- Extent 크기는 바이트 단위로 기술하며, 다섯 가지 (64 K, 128 K, 256 K, 512 K, 1 M) 중 하나가 선택된다. 
- 만약 extent 크기가 64 K ~ 128 K 사이의 값으로 지정되면 128 K로 설정되고, 1 M 이상으로 지정되면 1 M로 설정된다.

<a id="637953f5024589ab"></a>
### 설명

Temporary tablespace는 index (with NOLOGGING option) 등의 SQL schema 객체와, 질의를 처리할 때 sorting, hashing 하기 위한 중간 결과를 저장하는 물리적 공간을 제공하는 객체이다.

<a id="dce3fed1d67e3f91"></a>
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

<a id="3235af02bc2f3af2"></a>
### 호환성

SQL 표준은 테이블스페이스에 대한 개념을 다루지 않고 있다.

<a id="fb1f39978e6f339a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#4aecf03632f3116f)
- [ALTER TABLESPACE](#c308f53537323289)

<a id="339657c579ea782f"></a>
## CREATE USER

<a id="9a3ce4aa68ce6729"></a>
### 기능

데이터베이스 사용자를 정의한다.

<a id="fd02326421de91f2"></a>
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

<a id="2d162a2941f6ad3b"></a>
### 사용 범위 및 접근 권한

&lt;user definition&gt; 구문을 수행하려면 사용자에게 CREATE USER ON DATABASE 권한이 있어야 한다.

생성한 user_identifier 사용자는 &lt;schema clause&gt;로 생성한 스키마의 소유자라는 권한을 갖는다.

> 생성된 user_identifier에는 별도의 권한이 부여되지 않는다.  
> user_identifier 사용자가 접속해서 SQL 구문을 수행하려면 적절한 권한을 부여받아야 한다.

<a id="72980dd570e12364"></a>
### 구문 규칙 및 파라미터

<a id="72eac4a1f2892b1a"></a>
#### user_identifier

생성할 user의 이름이다.  
동일한 사용자 이름 (user_identifier)이나 역할 이름 (role_name)이 존재하지 않아야 한다.  
user_identifier의 길이는 128 byte 보다 작아야 한다.

<a id="1da71f3cc6bf77c0"></a>
#### password

생성할 user의 password로써 암호화되어 저장된다.  
password의 길이는 128 byte보다 작아야 한다.  
password는 영문자로 시작해야 하고 영문자, 숫자, underscore(_), $를 포함할 수 있다.  
그 외의 특수문자를 사용하려면 double-quotation (")으로 묶어야 한다.

<a id="36c35a0860afb262"></a>
#### PROFILE { profile_name | DEFAULT | NULL }

비밀번호 관리 정책의 profile을 할당한다.

- PROFILE profile_name
    - 사용자가 생성한 profile_name을 할당한다.
- PROFILE DEFAULT
    - 기본 profile "DEFAULT"를 할당한다.
- PROFILE NULL
    - Profile을 할당하지 않는다.

PROFILE 절을 생략할 경우, PROFILE NULL과 동일하며 profile이 적용되지 않는다.  
비밀번호 관리 정책에 대한 자세한 내용은 [CREATE PROFILE](#208fdfbd422ca37d)을 참조한다.

<a id="d919c62143ff1dad"></a>
#### PASSWORD EXPIRE

사용자의 비밀번호 유효기간을 만료시킨다.  
사용자가 login 하기 전에 강제로 비밀번호를 변경하도록 하기 위해 사용한다.

<a id="e5937cd42f9fb4e6"></a>
#### ACCOUNT { LOCK | UNLOCK }

- ACCOUNT LOCK
    - 사용자 계정을 잠근다.
- ACCOUNT UNLOCK
    - 계정 잠금을 해제한다.

<a id="42ad3f9650f21fac"></a>
#### DEFAULT TABLESPACE tablespace_name

User가 생성하는 테이블, 인덱스 (LOGGING) 등의 객체가 저장될 기본 TABLESPACE를 지정한다.  
DEFAULT TABLESPACE 절을 생략할 경우, DATABASE를 생성할 때 정의한 default data tablespace (MEM_DATA_TBS)가 지정된다.

<a id="69525f895b0aca17"></a>
#### TEMPORARY TABLESPACE tablespace_name

User가 생성하는 임시 테이블, 인덱스 (NO LOGGING), 질의 처리 과정에서 생성되는 중간 결과들을 저장할 TABLESPACE를 지정한다.  
TEMPORARY TABLESPACE 절을 생략할 경우, DATABASE를 생성할 때 정의한 default temporary tablespace (MEM_TEMP_TBS)가 지정된다.

<a id="c922061f79309211"></a>
#### INDEX TABLESPACE { tablespace_name | NULL }

User가 생성하는 인덱스 객체가 저장되는 기본 TABLESPACE를 지정한다.

- INDEX TABLESPACE tablespace_name 지정
    - Data tablespace를 지정할 경우, LOGGING 인덱스여야 한다.
    - Temporary tablespace를 지정할 경우, NOLOGGING 인덱스여야 한다.

- INDEX TABLESPACE NULL
    - Index tablespace를 지정하지 않는다.

INDEX TABLESPACE 절을 생략할 경우, INDEX TABLESPACE NULL 이다.

<a id="38e72e53627d24e8"></a>
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
사용자가 소유할 스키마는 [CREATE SCHEMA](#d4b396bf1d68ca78) 구문을 사용하여 추가로 생성할 수 있다.

<a id="ea8279defdd4e7d9"></a>
### 설명

User는 권한의 집합으로 구성된 authorization 객체이다.

최초로 &lt;user definition&gt; 구문을 수행할 때 어떠한 권한도 부여받지 않은 user가 생성되고 다음과 같이 적절한 권한을 부여해야 한다.

GOLDILOCKS에서 user와 schema의 관계는 1 : N 이다.  
즉, user가 소유한 schema가 존재하지 않을 수도 있고 다수의 schema를 소유할 수도 있다.

SQL 표준은 user, schema, database 등의 non-schema 객체들의 관계에 대해 명확히 정의하지 않고 있다. 반면, 각 DBMS 들은 다음과 같이 non-schema 객체 간의 관계를 상이하게 정의하고 있다.

> DBMS별 user와 schema 관계   
>   
> • Oracle  
> ° User : schema = 1 : 1의 관계이다.  
>   
> • DB2   
> ° OS user와 동일하다.   
> ° User를 생성하고 삭제하는 별도의 SQL 구문이 없다.   
>   
> • Postgres   
> ° User : schema = 1 : N의 관계이다.   
>   
> • MySQL   
> ° Database : schema = 1 : 1의 관계이다.  
> ° User는 database (schema)의 하위 객체이다.

<a id="d521d50773e5f06f"></a>
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

<a id="0382aa7459977eee"></a>
### 호환성

SQL 표준에서는 user 개념은 다루고 있지만 user 생성 및 삭제와 관련된 SQL 구문은 정의하지 않고 있다.

<a id="91c99d2564107ce2"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP USER](#d82c6e3b5b385afc)
- [ALTER USER](#c2d86feb760d5ff5)
- [CREATE SCHEMA](#d4b396bf1d68ca78)

<a id="69be25aa5896b17e"></a>
## CREATE VIEW

<a id="ab1d1dc6050b34c0"></a>
### 기능

View를 정의한다.

<a id="86435be72c52c089"></a>
### 구문

```
<view definition> ::=
    CREATE [ OR REPLACE ] [ FORCE | NO FORCE ] 
        VIEW view_name [ ( column_name [, ...] ) ]
        AS <query expression>
    ;
```

<a id="c188539f45f08878"></a>
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

<a id="5917f1e5910575b2"></a>
### 구문 규칙 및 파라미터

<a id="a6f57d33bffae8c8"></a>
#### [ OR REPLACE ]

이미 존재하는 view가 있을 경우, 기존의 view를 대체한다.

<a id="63e4c2510be278a2"></a>
#### [ FORCE | NO FORCE ]

- FORCE 
    - &lt;query expression&gt;의 유효성 여부에 관계없이 view를 생성한다. 
- NO FORCE 
    - &lt;query expression&gt;이 유효할 경우 view를 생성한다.
- 기본값은 NO FORCE 이다

<a id="0e8610350b271cb1"></a>
#### view_name

생성할 view의 이름이며, 스키마 내에서 유일한 이름이어야 한다.  
schema_name.view_name과 같이 view가 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
View 이름의 길이는 128 바이트보다 작아야 한다.

<a id="dcc1b285e9780a21"></a>
#### [ ( column_name [, ...] ) ]

View를 구성할 column의 이름을 정의한다.  
각 column의 이름은 view 내에서 고유한 이름이어야 한다.

Column의 개수는 SELECT 절의 결과 column 개수와 동일해야 한다.

Column 이름의 리스트를 생략할 경우, &lt;query expression&gt;의 SELECT 절의 column 이름을 사용한다.

<a id="50d44396e69c7ffd"></a>
##### AS &lt;query expression&gt;

View를 생성하는 [SELECT](#c9d76bf073f60db2) 질의이다.

&lt;query expression&gt;에는 다음과 같은 변수를 포함할 수 없다.

- Host parameter 
- SQL parameter 
- Dynamic parameter 
- Embedded variable 
- SEQUENCE 객체

<a id="4d6cfc4d2c64a4b2"></a>
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

<a id="4b7ea0c17e9eb15f"></a>
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

<a id="f24a35c4c010cea7"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- [ OR REPLACE ] 절 
- [ FORCE | NO FORCE ] 절

**SQL 표준 호환성**

<a id="d2342b11d4aaecb9"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T131 | Recursive query | X |
| F751 | View CHECK enhancements | X |
| S043 | Enhanced reference types | X |
| T111 | Updatable joins, unions, and columns | X |
| F852 | Top-level &lt;order by clause&gt; in views | O |
| F864 | Top-level &lt;result offset clause&gt; in views | O |
| F859 | Top-level &lt;fetch first clause&gt; in views | O |
| S081 | Subtables | X |

<a id="14ce2aaea57f8657"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP VIEW](#ae1beb0ccf35bd56)
- [ALTER VIEW](#a12dee3fdc1d483b)
- [SELECT](#c9d76bf073f60db2)

<a id="c0f5909b51d661a3"></a>
## DECLARE cursor_name

<a id="116f83bc6a7a2845"></a>
### 기능

커서를 선언한다.

<a id="c35c571b3a5bfba1"></a>
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

<a id="5395ae8c740d3d0c"></a>
### 사용 범위 및 접근 권한

statement_name을 사용한 동적 커서 (dynamic cursor)는 embedded SQL에서 사용할 수 있다.

&lt;cursor query&gt;의 유형에 따라 적절한 접근 권한을 가져야 한다.  
접근 권한에 대한 자세한 내용은 다음을 참조한다.

- [SELECT](#c9d76bf073f60db2) 구문의 접근 권한 
- [SELECT .. FOR UPDATE](#3d47d4f6b916da0d) 구문의 접근 권한
- [INSERT INTO name RETURNING](#569eaa09c01382f1) 구문의 접근 권한
- [UPDATE name RETURNING](#5c5251f859c78279) 구문의 접근 권한
- [DELETE FROM name RETURNING](#891b1183e582afc7) 구문의 접근 권한

<a id="638cca60e9a8cac8"></a>
### 구문 규칙 및 파라미터

<a id="fef9baa912c355c3"></a>
#### cursor_name

선언할 커서의 이름이다.  
하나의 session 내에서 고유한 이름이어야 한다.  
커서 이름의 길이는 128 바이트보다 작아야 한다.

<a id="a1a7cb70c08446c0"></a>
#### { FOR | IS }

SQL 표준에서는 구문 키워드로 FOR나 IS 중에 하나를 사용한다.

<a id="aeededff34e55a50"></a>
#### &lt;cursor properties&gt;

커서의 속성을 정의한다.

- &lt;cursor sensitivity&gt;를 명시하지 않은 경우, 기본값은 INSENSITIVE 이다. 
- &lt;cursor scrollability&gt;를 명시하지 않은 경우, 기본값은 NO SCROLL 이다. 
- &lt;cursor holdability&gt;를 명시하지 않은 경우, &lt;cursor updatability&gt;가 기본값을 결정한다.

<a id="0e6c05d08479105a"></a>
#### updatable query

Cursor 속성 중에 SENSITIVE나 FOR UPDATE를 사용하려면 cursor의 query가 base table의 row 변화를 식별하거나 row에 lock을 획득할 수 있는 updatable query 여야 한다.

updatable query는 다음 조건을 모두 만족해야 한다.

- 최상위 query에 DISTINCT가 존재하지 않아야 한다.
    - (X) SELECT DISTINCT * FROM t1;
- 최상위 query에 GROUP BY, HAVING, aggregation function이 존재하지 않아야 한다.
    - (X) SELECT MAX(c1) FROM t1;
- Returning query가 존재하지 않아야 한다.
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

<a id="3908f38d9556f6cd"></a>
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

<a id="44686d48958e9518"></a>
#### &lt;cursor scrollability&gt;

Cursor의 result set을 순차적 또는 비순차적으로 fetch 할 수 있는지 여부를 명시한다.

- NO SCROLL 
    - 순차적 FETCH (FETCH NEXT)만 가능하다. 
- SCROLL 
    - 비순차적 FETCH가 가능하다.
- 명시하지 않을 경우, 기본값은 NO SCROLL이다.

<a id="c7ec97d9ae2be510"></a>
#### &lt;cursor holdability&gt;

Cursor를 OPEN하고 트랜잭션을 commit 한 후에도 cursor가 유지되는지 여부를 설정한다.

- WITH HOLD 
    - 트랜잭션을 COMMIT 해도 cursor가 유지된다. 
    - FOR UPDATE 구문과 함께 사용할 수 없다. 
    - [INSERT INTO name RETURNING](#569eaa09c01382f1) 구문과 함께 사용할 수 없다. 
    - [UPDATE name RETURNING](#5c5251f859c78279) 구문과 함께 사용할 수 없다. 
    - [DELETE FROM name RETURNING](#891b1183e582afc7) 구문과 함께 사용할 수 없다.

- WITHOUT HOLD 
    - 트랜잭션을 COMMIT/ ROLLBACK하면 cursor를 닫는다.

- Rollback과 cursor
    - 트랜잭션을 rollback 할 경우, 트랜잭션에 포함된 cursor를 닫는다.
    - Savepoint까지 rollback하면 savepoint 이후에 생성된 cursor를 닫는다.

- 명시하지 않을 경우, &lt;cursor holdability&gt;의 기본값은 &lt;cursor updatability&gt;에 따라 결정된다.
    - FOR READ ONLY이거나 &lt;cursor updatability&gt;를 명시하지 않은 경우, 기본값은 WITH HOLD 이다. 
    - FOR UPDATE 구문과 함께 사용할 경우, 기본값은 WITHOUT HOLD 이다.

<a id="7fbfbcfb19484098"></a>
#### &lt;odbc cursor type&gt;

ODBC 표준의 cursor 유형으로 SCROLL 속성을 갖는다.

- STATIC CURSOR 
    - SQL 표준의 INSENSITIVE SCROLL과 동일하다. 
    - 비순차적 FETCH가 가능하다. 
    - ODBC 표준의 static scroll cursor이다. 
- KEYSET CURSOR 
    - SQL 표준의 ASENSITIVE SCROLL과 동일하다.
    - ODBC 표준의 keyset-driven scroll cursor이다. 
    - Sensitivity 속성은 다음과 같은 특성에 따라 결정된다.

**FOR [UPDATE / READ ONLY] 구문과 query 유형에 따른 sensitivity**

<a id="0e103ee4c23ecd74"></a>
| Updatability | Query 유형 | Sensitivity |
| --- | --- | --- |
| FOR UPDATE | Updatable query | SENSITIVE |
| FOR UPDATE | Non-updatable query | Query error |
| FOR READ ONLY | Any query | INSENSITIVE |
| N/A | Updatable query | SENSITIVE |
| N/A | Non-updatable query | INSENSITIVE |

<a id="80457d2f8ab55a17"></a>
#### &lt;cursor specification&gt;

Cursor의 대상이 되는 query를 정의한다.  
statement_name을 사용할 경우, query가 정해지지 않은 동적 커서 (dynamic cursor)가 선언되고, &lt;cursor query&gt;를 사용할 경우, query가 정해진 고정 커서 (standing cursor)가 선언된다.

<a id="59f9b3a827f074f5"></a>
#### statement_name

Cursor가 참조할 statement_name이며 embedded SQL에서 사용할 수 있다.

statement_name은 &lt;declare cursor&gt; 구문을 수행하기 전에 존재해야 하며, statement_name이 참조하는 SQL 문장은 [PREPARE statement_name](#ebbfd3f86e32b694) 구문이 준비한 query여야 한다.

Query가 아닐 경우 [OPEN cursor_name](#275ead84ebffb434) 구문을 수행할 때 error가 발생한다.

<a id="fcfb72546e402a52"></a>
#### &lt;cursor query&gt;

Cursor에서 사용할 수 있는 query 유형은 다음 각 구문을 참조한다.

- [SELECT](#c9d76bf073f60db2)
- [SELECT .. FOR UPDATE](#3d47d4f6b916da0d)
- [INSERT INTO name RETURNING](#569eaa09c01382f1)
- [UPDATE name RETURNING](#5c5251f859c78279)
- [DELETE FROM name RETURNING](#891b1183e582afc7)

<a id="859f0c5561e91127"></a>
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

<a id="9dfb2179480dc27f"></a>
#### FOR UPDATE OF …

커서를 OPEN 할 때 lock 획득과 관련된 column을 나열한다.

- FOR UPDATE OF 구문에 나열된 column은
    - &lt;select statement&gt;의 FROM 절에 나열된 table의 갱신 가능한 column이어야 한다. 
    - 나열된 column의 table에 대한 lock을 획득한다. 
- FOR UPDATE만 사용하는 경우에는 
    - &lt;select statement&gt;의 FROM 절에 나열된 table들의 모든 갱신 가능한 column을 나열한 것과 동일한 의미이다. 
    - 모든 column의 table에 대한 lock을 획득한다.

<a id="512d9a53957df11b"></a>
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

<a id="40b644e81d441c2d"></a>
### 설명

Query에 대한 속성을 제어할 때 DECLARE CURSOR 구문과 OPEN, FETCH, CLOSE 구문을 사용할 경우, 서버의 커서를 제어하기 때문에 ODBC statement나 JDBC statement를 이용하여 cursor를 사용하는 경우보다 성능상 부하가 걸린다.

Query를 수행하기 전에 ODBC statement와 JDBC statement를 사용하여 cursor 속성을 제어할 수 있으며, DECLARE CURSOR 구문을 통한 SQL cursor의 속성 제어 방법과 이에 대응하는 ODBC 표준과 JDBC 표준의 cursor 속성 제어 방법은 다음과 같다.

<a id="69426c18490d02a4"></a>
<table class="table column_count_4"><caption>ODBC/ JDBC의 커서 속성 제어 </caption><thead><tr><th class="to_center to_middle"><div>Property 
분류</div></th><th class="to_center to_middle"><div>GOLDILOCKS
cursor property</div></th><th class="to_center to_middle"><div>ODBC 표준의 cursor 속성 설정</div></th><th class="to_center to_middle"><div>JDBC 표준의 cursor 속성 설정</div></th></tr></thead><tbody><tr><td class="to_left to_middle" rowspan="3"><div>Sensitivity</div></td><td class="to_left to_middle"><div>INSENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_INSENSITIVE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle"><div>SENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_SENSITIVE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle"><div>ASENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_UNSPECIFIED, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Scrollability</div></td><td class="to_left to_middle"><div>NO SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_NONSCROLLABLE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle"><div>SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_SCROLLABLE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Holdability</div></td><td class="to_left to_middle"><div>WITHOUT HOLD</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.CLOSE_CURSORS_AT_COMMIT )</div></td></tr><tr><td class="to_left to_middle"><div>WITH HOLD</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.HOLD_CURSORS_OVER_COMMIT )</div></td></tr></tbody></table>

ODBC cursor type에 대응되는 SQL cursor 선언은 다음과 같다.

**ODBC 커서 type에 대응되는 SQL 커서 선언**

<a id="b2841bdab141b510"></a>
| ODBC cursor type | SQL cursor 선언 |
| --- | --- |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, len) | NO SCROLL CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_STATIC, len) | STATIC CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, len) | KEYSET CURSOR |

JDBC cursor type에 대응되는 SQL cursor 선언은 다음과 같다.

**JDBC 커서 type에 대응되는 SQL 커서 선언**

<a id="9393f7e9c44a56f8"></a>
| JDBC cursor type | SQL cursor 선언 |
| --- | --- |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_FORWARD_ONLY, conc, hold ) | INSENSITIVE NO SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_INSENSITIVE, conc, hold ) | INSENSITIVE SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_SENSITIVE, conc, hold ) | SENSITIVE SCROLL CURSOR |

<a id="3b7847fc6d05c623"></a>
### 사용 예

다음은 interactive SQL (gsql)을 사용하여 cursor를 선언하고 사용하는 예이다.

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

<a id="d8efdeb85e455f1a"></a>
### 호환성

&lt;declare cursor&gt; 구문은 SQL 표준과 비교하여 다음과 같은 차이가 있다.

- SQL 표준의 &lt;cursor sensitivity&gt; 기본값은 ASENSITIVE이지만, GOLDILOCKS의 기본값은 INSENSITIVE이다. 
- SQL 표준에서는 다음과 같은 &lt;odbc cursor type&gt;을 다루지 않고 있다. 
    - STATIC CURSOR 
    - KEYSET CURSOR 
- SQL 표준의 &lt;cursor holdability&gt; 기본값은 WITHOUT HOLD이지만, GOLDILOCKS의 기본값은 &lt;cursor updatability&gt;에 따라 다르다. 
- SQL 표준에서는 &lt;cursor query&gt;로 &lt;select statement&gt;만 사용할 수 있지만, GOLDILOCKS는 다음과 같은 returning query를 사용할 수 있다. 
    - [INSERT INTO name RETURNING](#569eaa09c01382f1)
    - [UPDATE name RETURNING](#5c5251f859c78279)
    - [DELETE FROM name RETURNING](#891b1183e582afc7)
- SQL 표준의 &lt;cursor updatability&gt; 기본값은 &lt;select statement&gt;에 따라 결정되지만, GOLDILOCKS의 기본값은 FOR READ ONLY이다. 
- SQL 표준에는 &lt;lock wait mode&gt; 구문이 존재하지 않는다.

**SQL 표준 호환성**

<a id="54ddb08a2f86de43"></a>
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

<a id="85ceec46d438b528"></a>
### 참조

관련 내용은 다음을 참조한다.

- [OPEN cursor_name](#275ead84ebffb434)
- [FETCH cursor_name](#f8b0914239210b68)
- [CLOSE cursor_name](#c718855fa5a651b0)
- [PREPARE statement_name](#ebbfd3f86e32b694)
- [SELECT](#c9d76bf073f60db2)
- [SELECT .. FOR UPDATE](#3d47d4f6b916da0d)
- [INSERT INTO name RETURNING](#569eaa09c01382f1)
- [UPDATE name RETURNING](#5c5251f859c78279)
- [DELETE FROM name RETURNING](#891b1183e582afc7)

<a id="4748cf43648c03f0"></a>
## DELETE FROM

<a id="289f9152f5f5845b"></a>
### 기능

테이블의 row들을 삭제한다.

<a id="997aadb2a9451dd4"></a>
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

<a id="8ed325a1a8960c6c"></a>
### 사용 범위 및 접근 권한

&lt;delete statement: searched&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블에 대해 (DELETE 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (DELETE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DELETE ANY TABLE ON DATABASE

<a id="0f7a62147e916820"></a>
### 구문 규칙 및 파라미터

<a id="326356ded9f3179f"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="548257885ee710a7"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="e1580fe1783ab560"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 삭제한다.  
WHERE 조건을 명시하지 않은 경우, 모든 row를 삭제한다.  
WHERE 조건에 대한 자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 [where clause](#8ffd103d5116485d)를 참조한다.

<a id="38b00933673f992d"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 [offset limit clause](#37f82ae17691b17d)를 참조한다.

<a id="d79ee23d5ac6d452"></a>
#### &lt;fetch limit clause&gt;

Fetch 할 row의 개수를 명시하는 구문으로써 다음 두 가지 방법이 사용된다.

- &lt;fetch first clause&gt; 
    - Fetch 할 row의 개수를 명시한다.
    - 자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 &lt;[fetch first clause&gt;](#5bc4649717039d2f)를 참조한다.
- &lt;limit clause&gt;
    - Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
    - 자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 &lt;[limit clause&gt;](#7e039c5707f8a97b)를 참조한다.

<a id="2b1a4c02b5160c2e"></a>
### 설명

<a id="b9b48253e7f058ae"></a>
#### DELETE 관련 구문들의 차이점

- [DELETE FROM](#4748cf43648c03f0)
    - 조건에 부합하는 다수의 row를 삭제한다. 
    - 예: DELETE FROM t1 WHERE c1 = 0; 
- [DELETE FROM name WHERE CURRENT OF cursor_name](#035958e58b243d9a)
    - Cursor가 현재 가리키는 row를 삭제한다. 
    - 예: DELETE FROM t1 WHERE CURRENT OF cursor; 
- [DELETE FROM name RETURNING](#891b1183e582afc7)
    - 조건을 만족하는 다수의 row를 삭제하며, [SELECT](#c9d76bf073f60db2) 구문과 동일한 방식( SQLFetch() 등의 API )으로 삭제한 row들을 검색할 수 있다. 
    - 예: DELETE FROM t1 WHERE c1 = 0 RETURNING c2; 
- [DELETE FROM name RETURNING .. INTO](#c42062c47dd382ee)
    - 한 건 이하의 row를 삭제할 수 있으며, 삭제한 row가 한 건일 경우 RETURNING INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: DELETE FROM t1 WHERE c1 = 0 RETURNING c2 INTO :v1;

<a id="787bef2865ebb605"></a>
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

<a id="a638670810e0c9df"></a>
### 호환성

SQL 표준은 DELETE 구문에서 다음 절을 정의하지 않고 있다.

- &lt;result offset clause&gt; 
- &lt;fetch limit clause&gt;

**SQL 표준 호환성**

<a id="c7fb58900f9f0b1b"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="74c7b8f8be07c70c"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DELETE FROM name WHERE CURRENT OF cursor_name](#035958e58b243d9a)
- [DELETE FROM name RETURNING](#891b1183e582afc7)
- [DELETE FROM name RETURNING .. INTO](#c42062c47dd382ee)
- [SELECT](#c9d76bf073f60db2)

<a id="891b1183e582afc7"></a>
## DELETE FROM name RETURNING

<a id="648cb196abde4669"></a>
### 기능

테이블의 row들을 삭제하고, 삭제한 row들을 검색한다.

<a id="a9538bb4480c099b"></a>
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

<a id="a6b1eccdb27b466e"></a>
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

<a id="df288f123bc24d4f"></a>
### 구문 규칙 및 파라미터

<a id="270beb3d1b6ca716"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.

<a id="c285f8994555b7e4"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="afd928b758c59d4d"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 삭제한다.  
자세한 내용은 [DELETE FROM](#4748cf43648c03f0) 구문을 참조한다.

<a id="b99ec4048169eaab"></a>
#### &lt;result offset clause&gt;

질의 결과 중에 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#4748cf43648c03f0) 구문을 참조한다.

<a id="bd48bae87134d972"></a>
#### &lt;fetch first clause&gt;

Fetch 할 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#4748cf43648c03f0)구문을 참조한다.

<a id="201e8d6b0dfb0c9a"></a>
#### &lt;limit clause&gt;

Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.  
자세한 내용은 [DELETE FROM](#4748cf43648c03f0) 구문을 참조한다.

<a id="c68f70e90bb43ae8"></a>
#### &lt;returning clause&gt;

삭제된 row들을 결과 집합으로 하고, 이들 중에서 검색할 column을 기술한다.

- RETURNING 절은 DELETE 구문으로 삭제된 row들을 result set으로 하는 결과를 반환한다. 
- &lt;value expression&gt; 
    - SELECT 구문의 &lt;select list&gt;와 동일하지만 aggregation 등을 사용할 수 없다. 
- [[AS] alias_name] 
    - AS 절을 이용해 value expression의 이름을 지정할 수 있다.

RETURN과 RETURNING은 동일한 의미의 키워드이다.

<a id="6733eae5b7366e0c"></a>
### 설명

자세한 내용은 [DELETE 관련 구문들의 차이점](#b9b48253e7f058ae)을 참조한다.

<a id="cf65490bddf40696"></a>
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

<a id="ecafce00bd55f598"></a>
### 호환성

SQL 표준에는 &lt;delete returning query statement&gt; 구문이 존재하지 않는다.

<a id="f85cd2ac01cdb995"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DELETE FROM](#4748cf43648c03f0)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#035958e58b243d9a)
- [DELETE FROM name RETURNING .. INTO](#c42062c47dd382ee)
- [SELECT](#c9d76bf073f60db2)

<a id="c42062c47dd382ee"></a>
## DELETE FROM name RETURNING .. INTO

<a id="b33a0af2674d1e1c"></a>
### 기능

테이블에서 row 하나를 삭제하고, 삭제한 row의 값을 호스트 변수에 얻어온다.

<a id="0437d3090d673c44"></a>
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

<a id="e342de5fae40d000"></a>
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

<a id="c3aee6c3e534d37a"></a>
### 구문 규칙 및 파라미터

<a id="6eddc9543178f1bd"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.

<a id="1676d4bf4bad3c95"></a>
#### [ AS alias_name ]

table_name의 alias이다.

<a id="c1ee640e29cf6825"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 삭제한다.  
자세한 내용은 [DELETE FROM](#4748cf43648c03f0) 구문을 참조한다.

<a id="c8199dfefdff6d36"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#4748cf43648c03f0) 구문을 참조한다.

<a id="235cb5ec2db6118a"></a>
#### &lt;fetch first clause&gt;

Fetch 할 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#4748cf43648c03f0)구문을 참조한다.

<a id="2126e5aacd2e415d"></a>
#### &lt;limit clause&gt;

Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.  
자세한 내용은 [DELETE FROM](#4748cf43648c03f0) 구문을 참조한다.

<a id="06d22fc8d3a68ac4"></a>
#### &lt;returning into clause&gt;

- RETURNING .. AS ..
    - [DELETE FROM name RETURNING](#891b1183e582afc7) 구문의 returning clause를 참조한다.
- INTO variable_name [, ...]
    - INTO 절에 기술된 변수의 개수는 RETURNING 절에 기술된 expression의 개수와 동일해야 한다.

<a id="2e4f0e380d63fc9f"></a>
### 설명

삭제할 row가 하나 이하여야 한다.  
둘 이상의 row가 삭제되면 에러가 발생한다.

자세한 내용은 [DELETE 관련 구문들의 차이점](#b9b48253e7f058ae)을 참조한다.

<a id="f91cc5600c184f02"></a>
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

<a id="5963e45074f9bd41"></a>
### 호환성

SQL 표준에는 &lt;delete returning into statement&gt; 구문이 존재하지 않는다.

<a id="e8133ac1e329cdfa"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DELETE FROM](#4748cf43648c03f0)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#035958e58b243d9a)
- [DELETE FROM name RETURNING](#891b1183e582afc7)
- [SELECT](#c9d76bf073f60db2)

<a id="035958e58b243d9a"></a>
## DELETE FROM name WHERE CURRENT OF cursor_name

<a id="60cd36a5d4e4376b"></a>
### 기능

커서가 가리키는 row 하나를 삭제한다.

<a id="c34a2836268a495c"></a>
### 구문

```
<delete statement: positioned> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        WHERE CURRENT OF cursor_name
    ;
```

<a id="977aaa11b14a4cfc"></a>
### 사용 범위 및 접근 권한

&lt;delete statement: positioned&gt; 구문을 수행하려면 사용자에게 [DELETE FROM](#4748cf43648c03f0) 구문을 수행할 수 있는 권한이 있어야 한다.

<a id="821a3382206bb84a"></a>
### 구문 규칙 및 파라미터

<a id="a87387acea5c1afb"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.

<a id="ed837bcca133e02d"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="47c63be5cfec1a55"></a>
#### cursor_name

cursor_name에 해당하는 커서는 다음 조건을 만족해야 한다.

- OPEN 된 커서여야 한다. ([OPEN cursor_name](#275ead84ebffb434)을 참조한다.) 
- 커서를 이용해 FETCH한 row가 존재해야 한다. ([FETCH cursor_name](#f8b0914239210b68)을 참조한다.) 
- 커서를 위해 사용된 질의가 table_name을 식별할 수 있어야 한다. ([DECLARE cursor_name](#c0f5909b51d661a3)을 참조한다.) 
- table_name에 대해 갱신할 수 있는 커서여야 한다. ([DECLARE cursor_name](#c0f5909b51d661a3)을 참조한다.)

<a id="2ec36c555f454dc0"></a>
### 설명

자세한 내용은 [DELETE 관련 구문들의 차이점](#b9b48253e7f058ae)을 참조한다.

<a id="8ff3f1a23a2a46e2"></a>
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

<a id="8cf00dc53a96d08c"></a>
### 호환성

**SQL 표준 호환성**

<a id="0b398b6642731b53"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| S111 | ONLY in query expressions | X |
| B031 | Basic dynamic SQL | O |

<a id="7cf3d818f5f33732"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#c0f5909b51d661a3)
- [OPEN cursor_name](#275ead84ebffb434)
- [FETCH cursor_name](#f8b0914239210b68)
- [DELETE FROM](#4748cf43648c03f0)
- [DELETE FROM name RETURNING](#891b1183e582afc7)
- [DELETE FROM name RETURNING .. INTO](#c42062c47dd382ee)

<a id="c1e1a11e6ac9443a"></a>
## DROP AUDIT POLICY

<a id="eaf1415eb50231fc"></a>
### 기능

Audit policy를 제거한다.

<a id="84ed7f85111f5b59"></a>
### 구문

```
<drop audit policy statement> ::= 
    DROP AUDIT POLICY [ IF EXISTS ] policy_name
;
```

<a id="5f92c0440b9e28d4"></a>
### 사용 범위 및 접근 권한

&lt;drop audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="ee4bc901bb9919a4"></a>
### 구문 규칙 및 파라미터

<a id="f14fd571eab55d32"></a>
#### IF EXISTS

policy_name이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="c9efaf7ad54b3914"></a>
#### policy_name

제거할 audit policy 객체의 이름이다.

<a id="89f4f3491ec20ce9"></a>
### 설명

이미 활성화된 audit policy 객체는 제거할 수 없다.  이 경우, NOAUDIT POLICY 구문을 이용해 audit policy를 비활성화해야 한다.

<a id="86dc66803ff55c10"></a>
### 사용 예

다음은 audit policy를 제거하는 예이다.

```
DROP AUDIT POLICY policy_table;
```

<a id="289251f5373993f5"></a>
### 호환성

SQL 표준에는 audit policy가 존재하지 않는다.

<a id="08144966e1a76de8"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#676233f209f722e4)
    - [DROP AUDIT POLICY](#c1e1a11e6ac9443a)
    - [ALTER AUDIT POLICY](#2cfef6a9826bdadf)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#c789ab5113d50e70)
    - [NOAUDIT POLICY](#2953451ac097af0c)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#2eb922e8e06a1b57)

- Audit trail 제거: [ALTER DATABASE CLEAR AUDIT TRAIL](#016c886b7cddf620)

<a id="d185e21cb13f6ec6"></a>
## DROP CLUSTER GROUP

<a id="ae87bbcc1dbcda66"></a>
### 기능

Cluster group을 cluster system에서 제거한다.

<a id="ec23b7f1767b33a5"></a>
### 구문

```
<drop cluster group statement> ::=
    DROP CLUSTER GROUP [IF EXISTS] group_name
    ;
```

<a id="ceab9e01abe426be"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.  
&lt;drop cluster group statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="3b01818b0154c160"></a>
### 구문 규칙 및 파라미터

<a id="8e211497569e76e3"></a>
#### [IF EXISTS]

Cluster group이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="16a9124fe1b7a90c"></a>
#### group_name

Cluster group의 이름이다.  
Shard가 존재하지 않는 cluster group을 제거할 수 있다.

<a id="70a0204dbe0d41ad"></a>
### 설명

Cluster group을 제거하더라도 data loss가 발생하지 않는 경우에 해당 cluster group을 제거할 수 있다.

<a id="871576db34933127"></a>
### 사용 예

다음은 cluster group을 제거하는 예이다.

```
gSQL> DROP CLUSTER GROUP g3;

Cluster Group dropped.
```

<a id="ffb4ed38cc243bcb"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="9d13d43938562265"></a>
### 참조

관련 내용은 [CREATE CLUSTER GROUP](#609ea3458a43136d)을 참조한다.

<a id="f2273de5f0bd9109"></a>
## DROP CLUSTER LOCATION

<a id="cffb91b370977e48"></a>
### 기능

Cluster member의 접속 정보를 삭제한다.

<a id="625506e7bded1ba6"></a>
### 구문

```
<drop cluster location statement> ::=
    DROP CLUSTER LOCATION member_name 
    ;
```

<a id="8dfbabc8cff6ba9d"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.  
&lt;drop cluster location statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="0d4566e440b867fb"></a>
### 구문 규칙 및 파라미터

<a id="e2538df5f093e038"></a>
#### member_name

Cluster member의 이름이다.  
등록된 cluster location 정보에 동일한 cluster member 이름이 존재해야 한다.  
이름의 길이는 128 바이트보다 작아야 한다.

<a id="740157cad63e2513"></a>
### 설명

기본적으로 cluster location 정보는 cluster group을 생성할 때나 cluster member를 추가할 때 제공되는 접속 정보를 이용하여 자동으로 생성된다. 생성된 정보는 cluster member나 group을 삭제할 때 함께 삭제된다.

만약 cluster location의 접속 정보가 변경되면 cluster member을 삭제하거나 재생성할 필요없이 [ALTER CLUSTER LOCATION](#b088884e1c158484)을 이용하여 접속 정보를 변경할 수 있다.

<a id="36dc17d664e68a31"></a>
### 사용 예

```
gSQL> 
DROP CLUSTER LOCATION g1n2
;

Created
```

<a id="99c7e03401f8a914"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="f6833c5b8d61c94d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER LOCATION](#60d111e8979eff2d)
- [ALTER CLUSTER LOCATION](#b088884e1c158484)

<a id="93a6d0dc40b79b2e"></a>
## DROP INDEX

<a id="1a8a9dc83e25e054"></a>
### 기능

인덱스를 제거한다.

<a id="9b814b66195820da"></a>
### 구문

```
<drop index statement> ::=
    DROP INDEX [ IF EXISTS ] index_name
    ;
```

<a id="088bb32cd587b0e7"></a>
### 사용 범위 및 접근 권한

&lt;drop index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (DROP INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY INDEX ON DATABASE

<a id="7181098978f42239"></a>
### 구문 규칙 및 파라미터

<a id="aa7e3253314687e7"></a>
#### IF EXISTS

인덱스가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="dbe554f07e8f686b"></a>
#### index_name

삭제할 인덱스의 이름이다.  
schema_name.index_name과 같이 인덱스가 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

UNIQUE 제약 조건, PRIMARY KEY 제약 조건을 위해 생성한 인덱스는 제거할 수 없다.  
위 제약 조건을 위해 생성된 인덱스를 제거하려면 [ALTER TABLE name DROP CONSTRAINT](#bf6cc14c07dc84dc) 구문을 사용하여 관련된 제약 조건을 삭제해야 한다.

<a id="f0fffb5c7fa3a5a9"></a>
### 설명

DROP INDEX와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="8422c58f19727754"></a>
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

<a id="58d9a7d02ab11c56"></a>
### 호환성

SQL 표준에서는 인덱스에 대한 개념을 다루지 않고 있다.

<a id="fcac7d94ed74bad5"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](#ce4afb58f69a16f7)
- [DROP TABLE](#44de11d586092a30)
- [ALTER TABLE name DROP CONSTRAINT](#bf6cc14c07dc84dc)

<a id="b370f178d1d3dd6a"></a>
## DROP PROFILE

<a id="fc1253dec1a63671"></a>
### 기능

Profile을 삭제한다.

<a id="69f22221dff14692"></a>
### 구문

```
<drop profile statement> ::= 
    DROP PROFILE [ IF EXISTS ] profile_name [ CASCADE ] ;
```

<a id="17d0726a2c7fd160"></a>
### 사용 범위 및 접근 권한

&lt;drop profile statement&gt; 구문을 수행하려면 사용자에게 DROP PROFILE ON DATABASE 권한이 있어야 한다.

<a id="19377627d5162e6f"></a>
### 구문 규칙 및 파라미터

<a id="171c693e39a514d7"></a>
#### IF EXISTS

Profile이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="3f099973965ad5da"></a>
#### profile_name

삭제할 profile의 이름을 명시한다.  
DEFAULT profile은 삭제할 수 없다.

<a id="80f1fe25f8a708da"></a>
#### CASCADE

이미 할당받은 사용자들이 존재하는 경우, profile을 삭제하기 위해 반드시 이 절을 명시해야 한다.  
삭제할 profile을 할당받은 사용자들의 profile은 DEFAULT profile로 변경한다.

<a id="3e0f090b22271f3c"></a>
### 사용 예

다음은 CASCADE 구문을 사용하여 profile을 삭제하는 예이다.

```
gSQL> DROP PROFILE prof CASCADE;

Profile dropped.

gSQL> COMMIT;

Commit complete.
```

<a id="fe17a7b6612714bb"></a>
### 호환성

SQL 표준에서는 profile에 대한 개념을 다루지 않고 있다.

<a id="5a4c3855b38f9f4c"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE PROFILE](#208fdfbd422ca37d)
- [ALTER PROFILE](#e26c5af4933c1efe)

<a id="c2e1f942afbed8da"></a>
## DROP SCHEMA

<a id="b4e90c4d8c67346b"></a>
### 기능

스키마를 제거한다.

<a id="79fc44fd428d49da"></a>
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

<a id="ceb238dc353550c9"></a>
### 사용 범위 및 접근 권한

&lt;drop schema statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 스키마의 소유자 
- 해당 스키마에 대해 CONTROL SCHEMA ON SCHEMA 
- DROP SCHEMA ON DATABASE

<a id="661ff3851f4fc07a"></a>
### 구문 규칙 및 파라미터

<a id="cbfd8c2bdc762baa"></a>
#### IF EXISTS

스키마가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="ac400bdecaa47a39"></a>
#### schema_name

제거할 스키마의 이름이다.  
단, database를 생성할 때 자동으로 생성되는 DICTIONARY_SCHEMA, INFORMATION_SCHEMA, PUBLIC과 같은 built-in 스키마는 제거할 수 없다.

<a id="f7f5cbbd435b4748"></a>
#### &lt;drop behavior&gt;

- RESTRICT 
    - Schema 내에 존재하는 객체가 없어야 한다. 
- CASCADE 
    - Schema 내의 모든 객체를 함께 제거한다.
- 생략할 경우, 기본값은 RESTRICT이다.

<a id="d07acf56f223e6f1"></a>
### 설명

DROP SCHEMA와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="4068eb2456924be9"></a>
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

<a id="979521ddbb4a3192"></a>
### 호환성

SQL 표준에서는 IF EXISTS 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="c4e4de72761cf6ac"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |
| F381 | Extended schema manipulation | O |

<a id="9902f666f0abd526"></a>
### 참조

관련 내용은 [CREATE SCHEMA](#d4b396bf1d68ca78)를 참조한다.

<a id="7debf989c0a88d02"></a>
## DROP SEQUENCE

<a id="90437af65bb2d5b5"></a>
### 기능

시퀀스를 제거한다.

<a id="f5977895dd0e8fb7"></a>
### 구문

```
<drop sequence generator statement> ::=
    DROP SEQUENCE [ IF EXISTS ] [schema_name.] sequence_name 
    ;
```

<a id="7709e2eccc5bc77e"></a>
### 사용 범위 및 접근 권한

&lt;drop sequence generator statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 시퀀스의 소유자 
- 시퀀스가 속한 스키마에 대해 (DROP SEQUENCE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY SEQUENCE ON DATABASE

<a id="21b134135dba05c9"></a>
### 구문 규칙 및 파라미터

<a id="e80be49221bc080f"></a>
#### IF EXISTS

시퀀스가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="0a71be59ff5c743f"></a>
#### sequence_name

제거할 시퀀스의 이름이다.  
schema_name.sequence_name과 같이 시퀀스가 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="1b1df3015bff7351"></a>
### 설명

DROP SEQUENCE와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="3673593df3331bc4"></a>
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

<a id="6989bce01421b907"></a>
### 호환성

SQL 표준에서는 IF EXISTS 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="e648a46424a0a996"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="19acdd273f93f741"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE SEQUENCE](#cdaeabbec6dc28f1)
- [ALTER SEQUENCE](#9fd8a84df33183e1)

<a id="fb9ded8027c5c9fe"></a>
## DROP SYNONYM

<a id="a7f036638864d5ec"></a>
### 기능

Synonym을 제거한다.

<a id="ed504a3af17bd852"></a>
### 구문

```
<drop synonym statement> ::=
    DROP [ PUBLIC ] SYNONYM [ IF EXISTS ] [schema_name.]synonym_name
    ;
```

<a id="24f1290d755790d1"></a>
### 사용 범위 및 접근 권한

PUBLIC을 명시하여 public synonym을 제거하려면 DROP PUBLIC SYNONYM ON DATABASE 권한이 있어야 한다.

Private synonym을 제거하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 synonym의 소유자 
- Synonym이 속한 스키마에 대해 (DROP SYNONYM 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY SYNONYM ON DATABASE

<a id="026db82979508a40"></a>
### 구문 규칙 및 파라미터

<a id="49eac2d23be84af4"></a>
#### [ PUBLIC ]

Public synonym을 제거하고자 할 때 명시한다.  
이 절을 생략하면 private synonym이 제거된다.

<a id="389b4a2eca43280d"></a>
#### IF EXISTS

Synonym이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="2dde5ce5f69bdedf"></a>
#### synonym_name

제거할 synonym의 이름이다.  
schema_name.synonym_name과 같이 synonym이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
PUBLIC을 명시한 경우, 스키마 이름을 명시할 수 없다.

<a id="d6efc98719d6ea1d"></a>
### 설명

DROP SYNONYM과 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="91bf4cd6b25e4aa9"></a>
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

<a id="3824ddb1046e2532"></a>
### 호환성

SQL 표준에서는 DROP SYNONYM 구문을 정의하지 않고 있다.

<a id="14e7b5e2d7cd894c"></a>
### 참조

관련 내용은 [CREATE SYNONYM](#63dc86c3ac2b8f57)을 참조한다.

<a id="44de11d586092a30"></a>
## DROP TABLE

<a id="021b2562d352fe8e"></a>
### 기능

테이블을 제거한다.

<a id="b2c9c94be835758a"></a>
### 구문

```
<drop table statement> ::=
    DROP TABLE [ IF EXISTS ] table_name
    [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
    | CASCADE CONSTRAINTS
```

<a id="3b50bc627d97d88a"></a>
### 사용 범위 및 접근 권한

&lt;drop table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블의 소유자 
- 해당 테이블에 대해 CONTROL TABLE ON TABLE 
- 테이블이 속한 스키마에 대해 (DROP TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY TABLE ON DATABASE

<a id="d692cfefbd6f1059"></a>
### 구문 규칙 및 파라미터

<a id="ded99405c098b956"></a>
#### IF EXISTS

테이블이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="f5cc56488bccfe2a"></a>
#### table_name

제거할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

Database를 생성할 때 자동으로 생성되는 다음과 같은 테이블들은 삭제할 수 없다.

- DEFINITION_SCHEMA 스키마의 테이블들 
- FIXED_TABLE_SCHEMA 스키마의 테이블들

테이블에 생성된 제약 조건과 인덱스도 함께 제거한다.

<a id="e9292a5ef08d361f"></a>
#### drop behavior

현재는 RESTRICT/ CASCADE가 동일하게 동작한다.  
생략할 경우, 기본값은 RESTRICT 이다.

<a id="959af389c16db6a5"></a>
### 설명

DROP TABLE과 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="b2b95b5fef6b3bf3"></a>
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

<a id="6020dbe449a02cad"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- IF EXISTS 
- CASCADE CONSTRAINTS

**SQL 표준 호환성**

<a id="f42a7797f4d41047"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |

<a id="80aa469cc803b8c5"></a>
### 참조

관련 내용은 [CREATE TABLE](#1586c5952309fa38)을 참조한다.

<a id="4aecf03632f3116f"></a>
## DROP TABLESPACE

<a id="b9b571de7597c8f5"></a>
### 기능

테이블스페이스를 제거한다.

<a id="f6bd7fedf1fb0b90"></a>
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

<a id="fad6f21ff85c3dad"></a>
### 사용 범위 및 접근 권한

&lt;drop tablespace definition&gt; 구문을 수행하려면 사용자에게 DROP TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="44ecea653b7159f2"></a>
### 구문 규칙 및 파라미터

<a id="245830bfde63c2f1"></a>
#### IF EXISTS

테이블스페이스가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="afc39a7016fb674e"></a>
#### tablespace_name

제거할 테이블스페이스의 이름이다.

Database를 생성할 때 구축되는 다음과 같은 시스템 테이블스페이스는 제거할 수 없다.

- DICTIONARY_TBS : system tablespace for dictionary management 
- MEM_UNDO_TBS : system tablespace for default undo tablespace 
- MEM_DATA_TBS : system tablespace for default user data tablespace 
- MEM_TEMP_TBS : system tablespace for default temporary tablespace

> tablespace_name이 사용자들의 default tablespace로 사용되고 있었다면 tablespace가 제거된 후에는 객체를 위한 공간을 할당받을 수 없다. 따라서 tablespace를 제거한 후에는 [ALTER USER](#c2d86feb760d5ff5) 구문을 사용하여 사용자들의 default tablespace를 변경해 주어야 한다.

<a id="909dff82c5cd23e1"></a>
#### INCLUDING CONTENTS

테이블스페이스에 속하는 객체 (table, index, key constraints)를 삭제한다. 테이블스페이스에 속하는 table을 참조하는 index와 key constraints가 테이블스페이스 외부에 존재할 경우에는 이들도 함께 삭제한다.

INCLUDING CONTENTS 구문을 사용하지 않을 경우에는 테이블스페이스에 속하는 객체가 없어야 한다.

<a id="ba1bc267dc40e3f1"></a>
#### [ { AND | KEEP } DATAFILES ]

테이블스페이스를 구성하는 데이터 파일들을 함께 삭제할지 여부를 지정한다.  
Memory temporary tablespace에는 데이터 파일이 존재하지 않으므로, 해당 절은 무시된다.

- AND DATAFILES 
    - 데이터 파일들을 함께 삭제한다. 
- KEEP DATAFILES 
    - 데이터 파일을 삭제하지 않고 남겨둔다. 
- 명시하지 않을 경우, 기본값은 KEEP DATAFILES 이다.

<a id="35327b7b144bdf5e"></a>
#### drop behavior

현재는 RESTRICT/ CASCADE가 동일하게 동작한다.  
생략할 경우, 기본값은 RESTRICT 이다.

<a id="ecdddda8f85df875"></a>
### 설명

DROP TABLESPACE 구문은 다른 Data Definition Language (DDL)과 달리 ROLLBACK 할 수 없으며, 구문을 수행한 transaction이 자동으로 COMMIT 된다.

<a id="7209ac99e61a4c98"></a>
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

<a id="cb5555332efde6c3"></a>
### 호환성

SQL 표준은 tablespace에 대한 개념을 다루지 않고 있다.

<a id="b5b9466619f0be4a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE MEMORY DATA TABLESPACE](#f34525feb7d5edf3)
- [CREATE MEMORY TEMPORARY TABLESPACE](#bb76a8ab84a10ae1)
- [ALTER TABLESPACE](#c308f53537323289)

<a id="d82c6e3b5b385afc"></a>
## DROP USER

<a id="36f288b17668eae0"></a>
### 기능

데이터베이스 사용자를 제거한다.

<a id="8ad9c534de418f98"></a>
### 구문

```
<drop user statement> ::=
    DROP USER [ IF EXISTS ] user_identifier [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
```

<a id="429523044cd8e006"></a>
### 사용 범위 및 접근 권한

&lt;drop user statement&gt; 구문을 수행하려면 사용자에게 DROP USER ON DATABASE 권한이 있어야 한다.

> user_identifier가 소유한 스키마가 존재하지 않아야 한다.  
> 스키마 제거에 대한 자세한 내용은 [DROP SCHEMA](#c2e1f942afbed8da) 구문을 참조한다.

<a id="f43f86e0298669ff"></a>
### 구문 규칙 및 파라미터

<a id="0f72073c7c3b93f1"></a>
#### IF EXISTS

사용자가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="fd37d09e03f502e1"></a>
#### user_identifier

제거할 데이터베이스 사용자의 이름이다.  
단, database를 생성할 때 자동으로 생성되는 "SYS" 등과 같은 사용자는 제거할 수 없다.

다음과 같이 user_identifier가 생성했으나, 소유자가 아닌 객체는 제거하지 않는다.

- Role 
- Tablespace

<a id="0be3d977ff5601eb"></a>
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

<a id="8d1537f103f138f9"></a>
### 설명

GOLDILOCKS에서 user와 schema의 관계는 1 : N 이다.   
즉, user가 schema를 소유하지 않을 수도 있고, 다수의 schema를 소유할 수도 있다.

User 객체를 제거하려면 user가 소유한 모든 schema를 제거해야 한다.

<a id="a39ba06094b9531c"></a>
### 사용 예

다음은 user가 소유한 모든 schema를 모두 제거한 후 해당 user를 제거하는 예이다.

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

<a id="0a965b096d48a384"></a>
### 호환성

SQL 표준에서는 user의 개념은 다루고 있지만 user의 생성 및 제거와 관련된 SQL 구문은 정의하지 않고 있다.

<a id="e7ed4345cc5b2eca"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE USER](#339657c579ea782f)
- [ALTER USER](#c2d86feb760d5ff5)
- [DROP SCHEMA](#c2e1f942afbed8da)

<a id="ae1beb0ccf35bd56"></a>
## DROP VIEW

<a id="07222f0079806e23"></a>
### 기능

View를 제거한다.

<a id="c33e8daf3283e449"></a>
### 구문

```
<drop view statement> ::=
    DROP VIEW [ IF EXISTS ] view_name
    ;
```

<a id="46ea9264ca36a1cf"></a>
### 사용 범위 및 접근 권한

&lt;drop view statement&gt; 구문을 수행하려면 사용자는 다음 권한 중 하나가 있어야 한다.

- 해당 view의 소유자
- 해당 view에 대해 CONTROL TABLE ON TABLE
- View가 속한 스키마에 대해 (DROP VIEW 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY VIEW ON DATABASE

<a id="56a48dc6ff58ad3c"></a>
### 구문 규칙 및 파라미터

<a id="a6f79551ae2a3474"></a>
#### IF EXISTS

View가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="4888d01483f40781"></a>
#### view_name

제거할 view의 이름이다.  
schema_name.view_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="7b7eae73c67dd526"></a>
### 설명

DROP VIEW와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="c34440e6b6c58b33"></a>
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

<a id="b123b5a173fe0014"></a>
### 호환성

SQL 표준에서는 IF EXISTS 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="6c7c90d0ca4e6bd0"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |

<a id="a67a985d930325f3"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE VIEW](#69be25aa5896b17e)
- [ALTER VIEW](#a12dee3fdc1d483b)

<a id="0220fe9761f46bb1"></a>
## EXECUTE statement_name

<a id="521ab093603caee1"></a>
### 기능

준비된 statement를 수행한다.

<a id="92a8a6de37cc049a"></a>
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

<a id="f52f0dfc9403805b"></a>
### 사용 범위 및 접근 권한

Embedded SQL에서 사용할 수 있다.  
Dynamic SQL 구문의 종류에 부합하는 수행 권한이 있어야 한다.

<a id="cec16a7e317e08b1"></a>
### 구문 규칙 및 파라미터

<a id="ef5aa44237aab6f1"></a>
#### statement_name

준비된 statement의 이름이다.  
[PREPARE statement_name](#ebbfd3f86e32b694) 구문을 사용하여 statement_name을 준비해야 한다.

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

- [DECLARE cursor_name](#c0f5909b51d661a3)
- [OPEN cursor_name](#275ead84ebffb434)
- [FETCH cursor_name](#f8b0914239210b68)
- [CLOSE cursor_name](#c718855fa5a651b0)

질의 결과가 없을 경우, NO DATA로 완료된다.

<a id="8dd3f1b8b8cad5bb"></a>
#### [ &lt;parameter using clause&gt; ] [ &lt;result into clause&gt; ]

&lt;parameter using clause&gt;와 &lt;result into clause&gt;는 순서에 관계없이 기술할 수 있지만 중복해서 기술하지 않아야 한다.

<a id="cd68b208c85d0fe6"></a>
#### &lt;parameter using clause&gt;

statement_name이 참조하는 dynamic SQL 문장에 parameter가 존재할 경우, parameter에 대한 정보를 &lt;using parameter arguments&gt; 절로 명시한다.

<a id="342badebec5e4e8f"></a>
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

<a id="313737b79381a9d9"></a>
#### &lt;result into clause&gt;

statement_name이 참조하는 dynamic SQL 문장이 query일 경우, 결과 column에 대한 정보를 &lt;into result arguments&gt; 절로 명시한다.

결과값이 null인 경우, INDICATOR를 명시하지 않으면 [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] 에러가 발생한다.

<a id="3511215594cff64d"></a>
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

<a id="369a1454537f54c9"></a>
### 설명

statement_name은 embedded SQL 소스 코드에서 precompiler에게 statement를 알려주는 식별자로써, host variable이 아니기 때문에 별도의 type이나 선언이 필요하지 않다. EXECUTE statement_name 구문은 PREPARE statement_name 구문 뒤에 쓰여야 한다.

자세한 내용은 [Embedded Dynamic SQL](../part-05-developer-manual/27-embedded-sql.md#e652d9727ea939cd)을 참조한다.

<a id="2a2aefa86f08d1af"></a>
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

EXECUTE statement_name이 사용된 전체 소스 코드는 [Dynamic Embedded SQL Example Program](../part-05-developer-manual/27-embedded-sql.md#863693205873a3d5)에서 확인할 수 있다.

<a id="44eeff969932890f"></a>
### 호환성

**SQL 표준 호환성**

<a id="8ca68bb3d59256f7"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |
| B032 | Extended dynamic SQL | X |

<a id="f7bdfbae2c9efab0"></a>
### 참조

관련 내용은 다음을 참조한다.

- [PREPARE statement_name](#ebbfd3f86e32b694)
- [DECLARE cursor_name](#c0f5909b51d661a3)
- [OPEN cursor_name](#275ead84ebffb434)
- [FETCH cursor_name](#f8b0914239210b68)
- [CLOSE cursor_name](#c718855fa5a651b0)
- [Embedded Dynamic SQL](../part-05-developer-manual/27-embedded-sql.md#e652d9727ea939cd)

<a id="c9ffd94cba178e21"></a>
## EXECUTE IMMEDIATE 'sql_string'

<a id="7ba5dc23d567d5d0"></a>
### 기능

프로그램 작성 시점에 정의되지 않았던 dynamic SQL 문장을 수행한다.

<a id="a492ee1c4213c53f"></a>
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

<a id="e5ac1914a925ab06"></a>
### 사용 범위 및 접근 권한

Embedded SQL에서 사용할 수 있다.  
Dynamic SQL 구문의 종류에 부합하는 수행 권한이 있어야 한다.

<a id="f86a5584d533369a"></a>
### 구문 규칙 및 파라미터

<a id="a9f9f60c5d1daf82"></a>
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

<a id="66076ef4b663c949"></a>
#### variable_name

variable_name에 대응되는 type은 character string이어야 한다.  
variable_name에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="431fa59cd0c79466"></a>
#### sql statement

sql statement에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="282de3f64b024a61"></a>
### 설명

EXECUTE IMMEDIATE 'sql_string' 구문은 dynamic embedded SQL 응용 프로그램에서 host variable이 없는 non-query SQL에 사용될 수 있다. 별도의 준비과정이 필요하지 않기 때문에, DDL이나 DML 등을 일회성으로 수행하기에 적합하다.

자세한 내용은 [Embedded Dynamic SQL](../part-05-developer-manual/27-embedded-sql.md#e652d9727ea939cd)을 참조한다.

<a id="f2c8157f5db4271b"></a>
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

EXECUTE IMMEDIATE 'sql_string'이 사용된 전체 소스 코드는 [Dynamic Embedded SQL Example Program](../part-05-developer-manual/27-embedded-sql.md#863693205873a3d5)에서 확인할 수 있다.

<a id="0414e88af03b2865"></a>
### 호환성

**SQL 표준 호환성**

<a id="1e6194f843845de3"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |

<a id="6914a7150361d220"></a>
### 참조

관련 내용은 다음을 참조한다.

- [PREPARE statement_name](#ebbfd3f86e32b694)
- [EXECUTE statement_name](#0220fe9761f46bb1)
- [Embedded Dynamic SQL](../part-05-developer-manual/27-embedded-sql.md#e652d9727ea939cd)

<a id="f8b0914239210b68"></a>
## FETCH cursor_name

<a id="561e08efc2613187"></a>
### 기능

커서를 결과 집합의 특정 row에 위치시키고, 해당 row의 값을 호스트 변수에 얻어온다.

<a id="253c154adc205be0"></a>
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

<a id="94ea2ed231dc4ed1"></a>
### 구문 규칙 및 파라미터

<a id="c5b3730e930d2c55"></a>
#### [ FROM ] cursor_name

세션 내에서 open 된 커서이어야 한다.  
FROM은 생략할 수 있다.

<a id="07ba42c0872f7e04"></a>
#### &lt;fetch orientation&gt;

FETCH NEXT 이외의 &lt;fetch orientation&gt;을 사용하려면 scrollable cursor를 사용해야 한다.  
&lt;fetch orientation&gt;을 생략할 경우, 기본값은 NEXT이다.

Open 된 커서는 결과 집합에 대해 아래 그림과 같은 커서 위치 정보를 갖는다.

<a id="ab07cf675ff114fd"></a>
![커서의 위치 정보](../assets/images/608a986ba63d8182.png)

**커서의 위치**

<a id="91b835a656741b3a"></a>
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

<a id="690746c92dd57b44"></a>
#### &lt;result into clause&gt;

&lt;into result arguments&gt;를 사용하여 결과 column을 획득할 변수 정보를 기술한다.

결과값이 null인 경우, INDICATOR를 명시하지 않으면 [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] 에러가 발생한다.

<a id="5cdc40daa257c3ce"></a>
#### &lt;into result arguments&gt;

INTO 절에 기술된 변수의 개수는 커서의 결과 집합의 column 개수와 동일해야 한다.

<a id="afc812459a35f850"></a>
### 설명

FETCH를 수행한 후에 커서 위치가 BEFORE THE FIRST ROW 거나 AFTER THE LAST LOW 인 경우, &lt;fetch orientation&gt;에 입력된 위치값에 관계없이 동일한 위치에 자리한다.

<a id="1568e6ea9fa060c6"></a>
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

<a id="160be1f3205d6d7f"></a>
### 호환성

SQL 표준에서는 &lt;fetch orientation&gt; 중에 CURRENT를 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="5ec30efe1e49b476"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F431 | Read-only scrollable cursors | O |
| B031 | Basic dynamic SQL | O |

<a id="eb120fbbad1029bc"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#c0f5909b51d661a3)
- [OPEN cursor_name](#275ead84ebffb434)
- [CLOSE cursor_name](#c718855fa5a651b0)

<a id="7961f4f3fe98c65c"></a>
## GRANT privileges TO

<a id="9680417ba9589b4d"></a>
### 기능

사용자에게 권한을 부여한다.

<a id="47fb41b9fbe5857d"></a>
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
```

<a id="e9186b6531700e25"></a>
### 구문 규칙 및 파라미터

<a id="357f344fc9deaf09"></a>
#### &lt;grantee&gt;

권한을 부여받을 사용자이다.

- user_identifier 
    - 해당 사용자에게 권한을 부여한다
- PUBLIC 
    - 모든 사용자를 의미하는 authorization 객체이다.

<a id="e7f2009ebf6471d2"></a>
#### WITH GRANT OPTION

Grantee (권한을 부여받은 사용자)가 다른 사용자에게 해당 권한을 부여할 수 있도록 한다.

다음과 같이 동일한 &lt;privilege&gt;에 대한 권한을 부여할 때 WITH GRANT OPTION은 계속 유지된다.

- GRANT SELECT ON t1 TO u1 WITH GRANT OPTION; 
- GRANT SELECT ON t1 TO u1;

<a id="e786e2084fc95103"></a>
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
        - &lt;table privilege&gt;: table의 소유자 
        - &lt;sequence privilege&gt;: sequence의 소유자
        - &lt;procedure privilege&gt;: procedure/ function의 소유자

<a id="e8a5e0aedacbceb0"></a>
#### &lt;database privilege&gt;

데이터베이스 객체에 대한 권한이다.  
[ON DATABASE] 구문은 생략할 수 있다.

database privilege로 정의할 수 있는 database action은 다음과 같다.

- ALL [ PRIVILEGES ] [ON DATABASE] 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 DATABASE에 대해 소유한 모든 권한이다.

**Database privilege**

<a id="5514b806d4ceaa38"></a>
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

<a id="010f08548f153467"></a>
#### &lt;tablespace privilege&gt;

테이블스페이스 객체에 대한 권한이다.

tablespace privilege로 정의할 수 있는 tablespace action은 다음과 같다.

- ALL [ PRIVILEGES ] ON TABLESPACE tablespace_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 TABLESPACE에 대해 소유한 모든 권한이다.

**Tablespace privilege**

<a id="1a604fb13e7a7c79"></a>
| &lt;tablespace action&gt; | 설명 |
| --- | --- |
| CREATE OBJECT | Tablespace에 객체를 생성할 수 있는 권한 |

<a id="3aa491f1275cabe3"></a>
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

<a id="3f54e6c438247b43"></a>
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

<a id="de4e2dc44c90dabd"></a>
#### &lt;table privilege&gt;

테이블 또는 view 객체에 대한 권한이다.  
[TABLE] 구문은 생략할 수 있다.

table privilege로 정의할 수 있는 table action은 다음과 같다.

- ALL [ PRIVILEGES ] ON [TABLE] table_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 TABLE에 대해 소유한 모든 권한이다.

**Table privilege**

<a id="0165567caf296d96"></a>
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

<a id="1535c9d1293d6302"></a>
| &lt;column action&gt; | 설명 |
| --- | --- |
| SELECT (columns) | 해당 column들을 검색할 수 있는 권한 |
| INSERT (columns) | 해당 column들을 포함한 row를 생성할 수 있는 권한 |
| UPDATE (columns) | 해당 column들을 갱신할 수 있는 권한 |
| REFERENCES (columns) | 해당 column들을 참조하는 참조 제약 조건을 생성할 수 있는 권한 |

<a id="297f76199ae58056"></a>
#### &lt;sequence privilege&gt;

시퀀스 객체에 대한 권한이다.

sequence privilege로 정의할 수 있는 sequence action은 다음과 같다.

- ALL [ PRIVILEGES ] ON SEQUENCE sequence_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 SEQUENCE에 대해 소유한 모든 권한이다.

**Sequence privilege**

<a id="1bd1ff02688d7f32"></a>
| &lt;sequence action&gt; | 설명 |
| --- | --- |
| USAGE | 시퀀스를 사용할 수 있는 권한 |

<a id="841736c107eda532"></a>
#### &lt;procedure privilege&gt;

Procedure/ function 객체에 대한 권한이다.

procedure privilege로 정의할 수 있는 action은 다음과 같다.

- ALL [ PRIVILEGES ] ON PROCEDURE procedure_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 procedure/ function에 대해 소유한 모든 권한이다.

**Procedure privilege**

<a id="7f322e3d070fd852"></a>
| &lt;procedure action&gt; | 설명 |
| --- | --- |
| EXECUTE | Procedure/ function을 실행할 수 있는 권한 |

<a id="3a64cfc943334cfb"></a>
### 설명

GRANT privilege와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

Table, sequence 등과 같은 SQL schema object를 생성한 owner는 해당 객체에 대한 권한을 별도로 부여받지 않더라도 일정한 권한을 가진다.   
이에 대한 자세한 설명은 다음과 같은 CREATE 구문을 참조한다.

- [CREATE TABLE](#1586c5952309fa38)
- [CREATE VIEW](#69be25aa5896b17e)
- [CREATE SEQUENCE](#cdaeabbec6dc28f1)
- [ALTER TABLE name ADD COLUMN](#c42e27e734cc5c56)
- [CREATE FUNCTION](../part-04-psm-manual/24-psm-sql-references.md#04b692603afa84f1)
- [CREATE PROCEDURE](../part-04-psm-manual/24-psm-sql-references.md#58204d591b990498)

Schema, tablespace 등과 같은 non-schema object를 생성한 owner에는 해당 객체에 대한 어떤 권한도 자동으로 부여되지 않으므로 별도의 권한을 부여받아야 한다.   
자세한 설명은 다음과 같은 CREATE 구문을 참조한다.

- [CREATE SCHEMA](#d4b396bf1d68ca78)
- [CREATE TABLESPACE](#df51248e3216ce23)
- [CREATE USER](#339657c579ea782f)

<a id="d1d43cb71a9dce0a"></a>
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

다음은 TABLESPACE mem_data_tbs에 객체를 생성할 수 있는 권한을 user u1에 부여하는 예이다.

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

<a id="6a6972fd4c0bf3fb"></a>
### 호환성

SQL 표준에서는 다음 privilege 들을 정의하지 않고 있다.

- &lt;database privilege&gt; 
- &lt;tablespace privilege&gt; 
- &lt;schema privilege&gt;

**SQL 표준 호환성**

<a id="8b5c9f28fb45d588"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| S023 | Basic structured types | X |
| S024 | Enhanced structured types | X |
| S081 | Subtables | X |
| T211 | Basic trigger capability | X |
| T281 | SELECT privilege with column granularity | O |
| T332 | Extended roles | X |
| F731 | INSERT column privileges | O |

<a id="ec011cfa1e08ba00"></a>
### 참조

관련 내용은 다음을 참조한다.

- [REVOKE privileges FROM](#10007ea0946b35a0)
- [CREATE USER](#339657c579ea782f)
- [DROP USER](#d82c6e3b5b385afc)
- [ALTER USER](#c2d86feb760d5ff5)

<a id="3d30a4728f25da9f"></a>
## INSERT INTO

<a id="e2f60d4e6b0fff1b"></a>
### 기능

테이블에 새로운 row들을 생성한다.

<a id="948884daaa179319"></a>
### 구문

```
<insert statement> ::=
    INSERT INTO table_name [ ( column_name [, ...] ) ]
        <insert source>
    ;

<insert source> ::=
      <values clause>
    | <from subquery>
    | <from default>

<values clause> ::=
    VALUES { ( { <value expression> | DEFAULT } [, ...] ) } [, ...]

<from subquery> ::=
    <query expression>

<from default> ::=
    DEFAULT VALUES
```

<a id="34e49ca2a55aac5e"></a>
### 사용 범위 및 접근 권한

&lt;insert statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- INSERT 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Insert 대상이 되는 모든 column에 대해 INSERT(columns) ON TABLE 
    - 테이블에 대해 (INSERT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (INSERT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - INSERT ANY TABLE ON DATABASE

- &lt;from subquery&gt;를 사용할 경우, 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="f3b1d4470558fec2"></a>
### 구문 규칙 및 파라미터

<a id="89730e0d6087dc0a"></a>
#### table_name

Row를 생성할 대상 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="493a9aa30ed82533"></a>
#### [ ( column_name [, ...] ) ]

테이블의 column 이름이다.  
Column 리스트는 생략할 수 있다.  
Column의 개수와 &lt;insert source&gt; 값의 개수는 동일해야 하며, 생략된 column에는 DEFAULT 값을 할당한다.

<a id="2de8a0b5375748f7"></a>
#### &lt;values clause&gt;

대응하는 column에 할당할 값의 리스트이다.

- &lt;value expression&gt; 
    - 대응하는 column에 할당할 값이나 연산식이다.
- DEFAULT 
    - 대응하는 column의 값은 [CREATE TABLE](#1586c5952309fa38) 구문을 통해 정의한 기본값을 사용한다. 
    - 정의하지 않았을 경우 NULL 값이 할당된다.

다음과 같이 다수의 row를 생성할 수 있다.

```
INSERT INTO table_name VALUES ( 1, 'A' ), ( 2, 'B' ), ( 3, 'C' )
```

<a id="8698538e29653cac"></a>
#### &lt;from subquery&gt;

Row들을 생성할 질의이다.  
자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 [query expression](#1c4140d8d3200490) 절을 참조한다.

<a id="61d443756c821629"></a>
#### DEFAULT VALUES

모든 column들을 기본값으로 채운다.

DEFAULT VALUES 절은 다음과 같은 의미이다.

```
VALUES ( DEFAULT, DEFAULT, ..., DEFAULT )
```

<a id="4442fa7b54108d1f"></a>
### 설명

<a id="1d261e9157d264bb"></a>
#### INSERT 관련 구문들의 차이점

- [INSERT INTO](#3d30a4728f25da9f)
    - 테이블에 하나 또는 다수의 row를 생성한다. 
    - 예: INSERT INTO t1 SELECT * FROM t1; 
- [INSERT INTO name RETURNING](#569eaa09c01382f1)
    - 테이블에 하나 또는 다수의 row를 생성하고, 생성한 row들을 SELECT 구문과 동일한 방식 (SQLFetch() 등의 API)으로 검색할 수 있다. 
    - 예: INSERT INTO t1 SELECT * FROM t1 RETURNING c1; 
- [INSERT INTO name RETURNING .. INTO](#c1f0fbbf948ca76c)
    - 한 건 이하의 row를 생성할 수 있으며, 생성한 row가 한 건일 경우 RETURNING INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: INSERT INTO t1 DEFAULT VALUES RETURNING c1 INTO :v1;

<a id="73e312e005743f13"></a>
### 사용 예

다음은 INSERT 구문을 이용해 row 하나를 생성하는 예이다.

```
gSQL> INSERT INTO region VALUES ( 0, 'AFRICA' );

1 row created.
```

다음은 INSERT 구문에서 column의 DEFAULT 값 또는 identity 값을 사용하는 예이다.

```
gSQL> CREATE TABLE region
(
    r_regionkey   BIGINT    GENERATED BY DEFAULT AS IDENTITY
  , r_name        CHAR(25)  DEFAULT 'N/A'
);

Table created.

gSQL> COMMIT;

Commit complete.
```

- 모든 column을 DEFAULT로 입력한다.

```
gSQL> INSERT INTO region DEFAULT VALUES;

1 row created.
```

- 모든 column을 DEFAULT로 입력한다.

```
gSQL> INSERT INTO region VALUES (DEFAULT, DEFAULT);

1 row created.
```

- Column이 생략된 경우 r_name column의 DEFAULT 값을 사용한다.

```
gSQL> INSERT INTO region(r_regionkey) VALUES (-100);

1 row created.
```

- Column이 생략된 경우 r_regionkey column의 identity 값을 사용한다.

```
gSQL> INSERT INTO region(r_name) VALUES ('ASIA');

1 row created.


gSQL> SELECT * FROM region;

R_REGIONKEY R_NAME                   
----------- -------------------------
          1 N/A                      
          2 N/A                      
       -100 N/A                      
          3 ASIA                     

4 rows selected.
```

다음은 VALUES 구문에 다수의 row를 기술하여 생성하는 예이다.

```
gSQL> INSERT INTO region
       VALUES ( 1, 'AFRICA' ),
              ( 2, 'ASIA'   ),
              ( 3, 'EUROPE' );

3 rows created.
```

다음은 subquery를 사용하여 다수의 row를 생성하는 예이다.

```
gSQL> INSERT INTO region SELECT r_regionkey, r_name FROM tmp_region WHERE r_regionkey < 3;

3 rows created.
```

<a id="a80422d5b032ed74"></a>
### 호환성

**SQL 표준 호환성**

<a id="3032f31db890e842"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| F222 | INSERT statement: DEFAULT VALUES clause | O |
| S204 | Enhanced structured types | X |
| S043 | Enhanced reference types | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="3c028526a7ae1f2d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [SELECT](#c9d76bf073f60db2)
- [INSERT INTO name RETURNING](#569eaa09c01382f1)
- [INSERT INTO name RETURNING .. INTO](#c1f0fbbf948ca76c)

<a id="569eaa09c01382f1"></a>
## INSERT INTO name RETURNING

<a id="2598aa38309ad3d5"></a>
### 기능

테이블에 새로운 row를 생성하고, 생성한 row들을 검색한다.

<a id="111ff5e5ab063afa"></a>
### 구문

```
<insert statement> ::=
    INSERT INTO table_name [ ( column_name [, ...] ) ]
        <insert source>
        <returning clause>
    ;

<insert source> ::=
      <values clause>
    | <from subquery>
    | <from default>

<values clause> ::=
    VALUES { ( { <value expression> | DEFAULT } [, ...] ) } [, ...]

<from subquery> ::=
    <query expression>

<from default> ::=
    DEFAULT VALUES

<returning clause> ::=
      [ RETURN | RETURNING ] { * | { <value expression> [ [AS] alias_name ] } [, ...]
```

<a id="298e43c169466418"></a>
### 사용 범위 및 접근 권한

&lt;insert returning query statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- INSERT 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Insert 대상이 되는 모든 column에 대해 INSERT(columns) ON TABLE 
    - 테이블에 대해 (INSERT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (INSERT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - INSERT ANY TABLE ON DATABASE

- &lt;from subquery&gt;를 사용할 경우, 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

- RETURNING 절에 사용된 모든 column에 대해 다음 권한 중 하나가 있어야 한다.
    - RETURNING 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="22537acfb0cc5743"></a>
### 구문 규칙 및 파라미터

<a id="05cb58ccacdda4a4"></a>
#### table_name

Row를 생성할 대상 테이블의 이름이다.

<a id="14623204df8e7654"></a>
#### [ ( column_name [, ...] ) ]

테이블의 column 이름이다.  
자세한 내용은 [INSERT INTO](#3d30a4728f25da9f) 구문을 참조한다.

<a id="f54827fece2b56f0"></a>
#### &lt;values clause&gt;

대응하는 column에 할당할 값의 리스트이다.  
자세한 내용은 [INSERT INTO](#3d30a4728f25da9f) 구문을 참조한다.

<a id="53c78c9d14e316bd"></a>
#### &lt;from subquery&gt;

Row들을 생성할 질의이다.  
자세한 내용은 [INSERT INTO](#3d30a4728f25da9f) 구문을 참조한다.

<a id="f6a7c184a3aa651b"></a>
#### DEFAULT VALUES

모든 column들을 기본값으로 채운다.   
자세한 내용은 [INSERT INTO](#3d30a4728f25da9f) 구문을 참조한다.

<a id="86de6cf641401697"></a>
#### &lt;returning clause&gt;

INSERT 된 row들을 반환한다.

- 생성된 row들을 결과 집합으로 하고, 이들 중 검색할 column을 기술한다. 
    - RETURNING 절은 INSERT 구문으로 삽입된 row들을 결과 집합으로 하는 결과를 반환한다. 
    - &lt;value expression&gt; 
        - SELECT 구문의 &lt;select list&gt;와 동일하지만 aggregation 등을 사용할 수 없다. 
    - [[AS] alias_name] 
        - AS 절을 사용하여 value expression의 이름을 지정할 수 있다.

RETURN과 RETURNING은 동일한 의미의 키워드이다.

<a id="0cdd9a805ed98cca"></a>
### 설명

자세한 내용은 [INSERT 관련 구문들의 차이점](#1d261e9157d264bb)을 참조한다.

<a id="1f588ed09c76e48e"></a>
### 사용 예

다음은 INSERT 구문으로 생성된 column 값을 검색하는 예이다.

```
gSQL> CREATE TABLE region
(
    r_regionkey   BIGINT    GENERATED BY DEFAULT AS IDENTITY
  , r_name        CHAR(25)  DEFAULT 'N/A'
);

Table created.

gSQL> COMMIT;

Commit complete.
```

- 생성된 DEFAULT 값을 RETURNING 하는 경우

```
gSQL> INSERT INTO region VALUES ( DEFAULT, DEFAULT ) RETURNING r_regionkey, r_name;

R_REGIONKEY R_NAME                   
----------- -------------------------
          1 N/A                      

1 row created.
```

- 생략된 column의 값을 RETURNING 하는 경우

```
gSQL> INSERT INTO region(r_name) VALUES ('ASIA') RETURNING r_regionkey;

R_REGIONKEY
-----------
          2

1 row created.
```

다음은 subquery로부터 생성된 row들을 검색하는 예이다.

```
gSQL> INSERT INTO region 
      SELECT r_regionkey, r_name FROM tmp_region WHERE r_regionkey < 3 
      RETURNING r_regionkey, r_name;

R_REGIONKEY R_NAME                   
----------- -------------------------
          0 AFRICA                   
          1 AMERICA                  
          2 ASIA                     

3 rows created.
```

<a id="0ebae175d407bfc6"></a>
### 호환성

SQL 표준에서는 &lt;insert returning query statement&gt; 구문을 정의하지 않고 있다.

<a id="d50abf8a77db12a6"></a>
### 참조

관련 내용은 다음을 참조한다.

- [INSERT INTO](#3d30a4728f25da9f)
- [INSERT INTO name RETURNING .. INTO](#c1f0fbbf948ca76c)

<a id="c1f0fbbf948ca76c"></a>
## INSERT INTO name RETURNING .. INTO

<a id="2ae9066b42870806"></a>
### 기능

테이블에 row 하나를 생성하고, 생성한 row의 값을 호스트 변수에 얻어온다.

<a id="e08d94aaee23ead7"></a>
### 구문

```
<insert statement> ::=
    INSERT INTO table_name [ ( column_name [, ...] ) ]
        <insert source>
        <returning into clause>
    ;

<insert source> ::=
      <values clause>
    | <from subquery>
    | <from default>

<values clause> ::=
    VALUES { ( { <value expression> | DEFAULT } [, ...] ) } [, ...]

<from subquery> ::=
    <query expression>

<from default> ::=
    DEFAULT VALUES

<returning into clause> ::=
      [ RETURN | RETURNING ] { * | { <value expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]
```

<a id="8870681f3bf2e837"></a>
### 사용 범위 및 접근 권한

&lt;insert returning into statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- INSERT 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Insert 대상이 되는 모든 column에 대해 INSERT(columns) ON TABLE 
    - 테이블에 대해 (INSERT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (INSERT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - INSERT ANY TABLE ON DATABASE

- &lt;from subquery&gt;를 사용할 경우, 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

- RETURNING 절에 사용된 모든 column에 대해 다음 권한 중 하나가 있어야 한다.
    - RETURNING 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="6953a4dbb8da34b3"></a>
### 구문 규칙 및 파라미터

<a id="1eef2cecc5850068"></a>
#### table_name

Row를 생성할 대상 테이블의 이름이다.

<a id="1b01877e72acc68e"></a>
#### [ ( column_name [, ...] ) ]

테이블의 column 이름이다.  
자세한 내용은 [INSERT INTO](#3d30a4728f25da9f) 구문을 참조한다.

<a id="b2e0a9380cfa81a7"></a>
#### &lt;values clause&gt;

대응하는 column에 할당할 값의 리스트이다.  
자세한 내용은 [INSERT INTO](#3d30a4728f25da9f) 구문을 참조한다.

<a id="37eb545de1474b50"></a>
#### &lt;from subquery&gt;

Row들을 생성할 질의이다.  
자세한 내용은 [INSERT INTO](#3d30a4728f25da9f) 구문을 참조한다.

<a id="d6f798f5877ea14d"></a>
#### DEFAULT VALUES

모든 column들을 기본값으로 채운다.  
자세한 내용은 [INSERT INTO](#3d30a4728f25da9f) 구문을 참조한다.

<a id="dfb75b55cdba8b2b"></a>
#### &lt;returning clause&gt;

INSERT 된 row를 반환한다.  
[INSERT INTO name RETURNING](#569eaa09c01382f1) 구문의 &lt;[returning clause&gt;](#86de6cf641401697) 절을 참조한다.

<a id="d254f05dac82f145"></a>
##### INTO variable_name [, ...]

INTO 절에 기술된 변수의 개수는 RETURNING 절에 기술된 expression의 개수와 동일해야 한다.  
생성할 row가 한 건 이하여야 한다. Row가 두 건 이상 생성될 경우, 에러가 발생한다.

<a id="4be800d7bb96e672"></a>
### 설명

자세한 내용은 [INSERT 관련 구문들의 차이점](#1d261e9157d264bb)을 참조한다.

<a id="e703b76b3ca61ffd"></a>
### 사용 예

다음은 생성된 row의 값을 호스트 변수에 얻어오는 예이다.

```
gSQL> CREATE TABLE region
(
    r_regionkey   BIGINT    GENERATED BY DEFAULT AS IDENTITY
  , r_name        CHAR(25)  DEFAULT 'N/A'
);

Table created.

gSQL> COMMIT;

Commit complete.
```

- 호스트 변수들을 선언한다.

```
\VAR v_key  BIGINT
\VAR v_name VARCHAR(128)
```

- 생성된 DEFAULT 값을 호스트 변수에 얻어오는 경우

```
gSQL> INSERT INTO region 
      VALUES ( DEFAULT, DEFAULT ) 
      RETURNING r_regionkey, r_name 
      INTO :v_key, :v_name;

V_KEY V_NAME                   
----- -------------------------
    1 N/A                      

1 row created.
```

- 생략된 column의 값을 호스트 변수에 얻어오는 경우

```
gSQL> INSERT INTO region(r_name) 
      VALUES ('ASIA') 
      RETURNING r_regionkey 
      INTO :v_key;

V_KEY
-----
    2

1 row created.
```

<a id="f01e5e4b5a0bd8a2"></a>
### 호환성

SQL 표준은 &lt;insert returning into statement&gt; 구문을 정의하지 않고 있다.

<a id="df415f0121cde5fb"></a>
### 참조

관련 내용은 다음을 참조한다.

- [INSERT INTO](#3d30a4728f25da9f)
- [INSERT INTO name RETURNING](#569eaa09c01382f1)

<a id="a6a53775fc0e6d73"></a>
## LOCK TABLE

<a id="ab5b9a9f91762503"></a>
### 기능

하나 이상의 테이블에 lock을 설정한다.

<a id="915a7cb4f5504b1d"></a>
### 구문

```
<lock table statement> ::=
    LOCK TABLE lock target [, ...] 
    IN <lock mode> MODE [<wait clause>]
    ;

<lock mode> ::=
    SHARE
    | EXCLUSIVE
    | ROW SHARE
    | ROW EXCLUSIVE
    | SHARE ROW EXCLUSIVE


<wait clause> ::=
    NOWAIT
    | WAIT time
```

<a id="c72dc7e1fdfa12d3"></a>
### 사용 범위 및 접근 권한

&lt;lock table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블에 대해 (LOCK 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (LOCK TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- LOCK ANY TABLE ON DATABASE

<a id="4ec101a9ed55e9b4"></a>
### 구문 규칙 및 파라미터

<a id="7ee3900b200c8389"></a>
#### &lt;lock target&gt;

LOCK 대상 테이블을 명시한다.

<a id="90c285363fa30d26"></a>
#### &lt;lock mode&gt;

LOCK mode를 명시한다.

- SHARE 
    - Locked table에 대한 동시성 질의를 허용하지만 테이블 update는 금지한다. 
- EXCLUSIVE 
    - Locked table에 대한 배타적인 질의 처리를 허용한다. 
- ROW SHARE 
    - Locked table에 동시성 접근을 허용하지만 exclusive access를 위한 전체 table locking은 금지한다. 
- ROW EXCLUSIVE 
    - Locked table에 동시성 접근을 허용하지만 exclusive access를 위한 전체 table locking은 금지한다. 
    - ROW EXCLUSIVE mode가 설정되어 있는 경우, SHARE mode의 locking은 거부한다. 
    - ROW EXCLUSIVE mode는 update, insert, delete 할 때 자동으로 부여된다. 
- SHARE ROW EXCLUSIVE 
    - Table 전체를 탐색하거나 다른 사용자에게 table의 row들을 탐색하게 할 때 사용한다. 
    - SHARE mode의 lock이 부여된 table이나 update되고 있는 row들에 다른 사용자가 접근하지 못하도록 한다.

<a id="33390d8836e25da3"></a>
#### &lt;wait clause&gt;

Lock을 획득하기 위한 대기 시간을 명시한다.

- NOWAIT 
    - 대상에 대한 lock 제어를 즉시 획득한다. 
    - 다른 사용자에 의해 이미 lock이 설정된 경우 즉시 제어권을 넘겨받는다. 
        - 이 경우 database가 message를 발생시킨다. 
- WAIT time 
    - Lock을 획득하기 위한 대기 시간을 설정한다.
    - 초 단위이며 0 ~ 1000000000 의 값을 사용할 수 있다.
- 명시하지 않을 경우 lock을 획득할 때까지 무기한 WAIT 하도록 한다.

<a id="6e4a6c7ea5371b12"></a>
### 설명

Transaction을 COMMIT 하거나 ROLLBACK 할 경우 획득한 모든 lock은 자동으로 해제된다. ROLLBACK TO SAVEPOINT 구문을 사용할 경우 해당 savepoint 이후에 획득한 모든 lock이 해제된다.

<a id="1e4a9d3a7bd15da5"></a>
### 사용 예

다음은 다른 transaction이 TABLE t1에 대해 어떠한 변경 연산도 수행할 수 없도록 하는 예이다.

```
gSQL> LOCK TABLE t1 IN EXCLUSIVE MODE;

Table locked.
```

다음은 다수의 table에 LOCK 구문을 수행하는 예이다.

```
gSQL> LOCK TABLE t1, t2 IN EXCLUSIVE MODE;

Table locked.
```

다음은 TABLE t1에 SHARE ROW EXCLUSIVE lock을 획득하는 예이다.

```
gSQL> LOCK TABLE t1 IN SHARE ROW EXCLUSIVE MODE;

Table locked.
```

다음은 해당 TABLE에 즉시 lock을 획득할 수 있을 경우에만 수행할 수 있는 구문이다. Lock을 획득할 수 없을 경우에는 에러가 발생한다.

```
gSQL> LOCK TABLE t1 IN EXCLUSIVE MODE NOWAIT;

Table locked.
```

다음은 lock을 획득하기 위해 10 초 동안 대기하도록 하는 예이다.

```
gSQL> LOCK TABLE t1 IN EXCLUSIVE MODE WAIT 10;

Table locked.
```

<a id="8d42b6efca546e13"></a>
### 호환성

SQL 표준은 lock table에 대한 개념을 다루지 않고 있다.

<a id="d225f3e52547ee80"></a>
### 참조

관련 내용은 다음을 참조한다.

- [COMMIT](#75b82fec67e8ca7c)
- [ROLLBACK](#1476005da98d89d8)

<a id="2953451ac097af0c"></a>
## NOAUDIT POLICY

<a id="4194813f74d76a30"></a>
### 기능

Audit policy를 비활성화한다.

<a id="323307ee2bbff1cf"></a>
### 구문

```
<noaudit policy statement> ::= 
    NOAUDIT POLICY policy_name
    [ <specified_user_option> ]
    ;

<specified_user_option> ::=
      BY user_name [, ...]
```

<a id="347e39d1e660ef9e"></a>
### 사용 범위 및 접근 권한

&lt;noaudit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="211e09c0690e9fc3"></a>
### 구문 규칙 및 파라미터

<a id="cfe66271f8776b48"></a>
#### policy_name

비활성화할 audit policy 객체의 이름이다.  
비활성화 된 audit policy는 기존 session에 영향을 미치지 않으며 새로 생성되는 session에만 영향을 준다.

<a id="648972d2ef3d3db3"></a>
#### &lt;specified_user_option&gt;

감사 대상에서 제외할 사용자를 명시한다.

AUDIT POLICY 구문과 달리 NOAUDIT POLICY 구문에는 EXCEPT 옵션이 없다.

AUDIT POLICY name BY 절을 사용한 경우 NOAUDIT POLICY name BY 구문으로 비활성화해야 하고   
AUDIT POLICY name EXCEPT 절을 사용한 경우 BY 절 없이 NOAUDIT POLICY name 구문으로 비활성화해야 한다.

AUDIT POLICY 구문의 사용 방법에 따라 다음과 같이 NOAUDIT POLICY 구문을 사용하여 해당 옵션을 비활성화해야 한다.

**Audit policy 활성화/ 비활성화**

<a id="f92efa563547a461"></a>
| 유형 | AUDIT POLICY 구문 | NOAUDIT POLICY 구문 |
| --- | --- | --- |
| 전체 사용자 | AUDIT POLICY p1 | NOAUDIT POLICY p1 |
| BY를 사용 | AUDIT POLICY p1 BY u1 | NOAUDIT POLICY p1 BY u1 |
| EXCEPT를 사용 | AUDIT POLICY p1 EXCEPT u1 | NOAUDIT POLICY p1 |

활성화된 모든 user들을 비활성화한 경우, audit policy 객체가 완전히 비활성화된다.

<a id="4fb4ef9a687722da"></a>
### 설명

Audit policy 객체의 활성화 정보는 다음과 같이 조회한다.

```
SELECT policy_name
     , enabled_opt
     , user_name
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';
```

NOAUDIT POLICY 구문은 AUDIT POLICY 지정 방식에 따라 생성된 개별 활성화 정보를 삭제한다.   
위의 질의를 통해 활성화한 정보가 없을 경우, audit policy는 완전히 비활성화된다.

다음과 같이 모든 user를 활성화한 경우, NOAUDIT POLICY BY 절은 영향을 미치지 않는다.

```
AUDIT POLICY p1;
```

- 어떠한 영향도 미치지 않는다.

```
NOAUDIT POLICY p1 BY u1;
```

- 다음과 같이 비활성화해야 한다.

```
NOAUDIT POLICY p1;
```

하나 이상의 user들을 개별적으로 활성화한 경우 AUDIT POLICY 설정 방법에 따라 NOAUDIT POLICY 구문을 사용해야 한다.

<a id="6f87bced45605a66"></a>
#### BY를 이용해 활성화한 경우

다음과 같이 audit policy를 활성화한 경우,

```
AUDIT POLICY p1 WHENEVER NOT SUCCESSFUL;
AUDIT POLICY p1 BY u1;
AUDIT POLICY p1 BY u2;
```

활성화 정보를 조회하면 다음과 같다.

```
SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

POLICY_NAME  ENABLED_OPT  USER_NAME    WHEN_SUCCESS  WHEN_FAILURE
-----------  -----------  ---------    ------------  ------------
P1           BY           ALL USERS    NO            YES
P1           BY           U1           YES           YES
P1           BY           U2           YES           YES
```

다음은 NOAUDIT 구문을 수행하고 활성화 정보를 조회하는 예이다.

```
NOAUDIT POLICY p1;

SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

POLICY_NAME  ENABLED_OPT  USER_NAME    WHEN_SUCCESS    WHEN_FAILURE
-----------  -----------  ---------    ------------    ------------
P1           BY           U1           YES             YES
P1           BY           U2           YES             YES
```

ALL USERS의 failure에 대한 감사가 비활성화되었으며, u1, u2 사용자에 대한 감사는 여전히 활성화되어 있다.

다음과 같이 BY 옵션을 통해 NOAUDIT POLICY 구문을 추가적으로 사용하면 audit policy p1은 완전히 비활성화된다.

```
NOAUDIT POLICY p1 BY u1, u2;

SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

no rows selected.
```

<a id="b3d83b697b48828f"></a>
#### EXCEPT를 이용해 활성화한 경우

다음과 같이 audit policy를 활성화한 경우,

```
AUDIT POLICY p1 EXCEPT u1, sys;
```

활성화 정보를 조회하면 다음과 같다.

```
SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

POLICY_NAME  ENABLED_OPT  USER_NAME    WHEN_SUCCESS    WHEN_FAILURE
-----------  -----------  ---------    ------------    ------------
P1           EXCEPT       U1           YES             YES
P1           EXCEPT       SYS          YES             YES
```

AUDIT POLICY 구문과 달리 NOAUDIT POLICY 구문에는 EXCEPT option이 없으므로 다음과 같이 옵션 없이 구문을 수행한다.

```
NOAUDIT POLICY p1;

SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

no rows selected.
```

즉, EXCEPT 옵션을 이용해 audit policy를 활성화한 경우, NOAUDIT POLICY 구문으로 개별 사용자를 다시 비활성화할 수 없다.

<a id="6e73e84177bb0ab1"></a>
### 사용 예

다음은 전체 사용자를 비활성화한 예이다.

```
NOAUDIT POLICY table_pol;
```

다음은 BY를 사용하여 활성화된 특정 사용자를 비활성화하는 예이다.

```
NOAUDIT POLICY table_pol BY u1;
```

<a id="8013721798bba2c4"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="80ea1b8caf31342a"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#676233f209f722e4)
    - [DROP AUDIT POLICY](#c1e1a11e6ac9443a)
    - [ALTER AUDIT POLICY](#2cfef6a9826bdadf)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#c789ab5113d50e70)
    - [NOAUDIT POLICY](#2953451ac097af0c)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#2eb922e8e06a1b57)

- Audit trail 제거: [ALTER DATABASE CLEAR AUDIT TRAIL](#016c886b7cddf620)

<a id="275ead84ebffb434"></a>
## OPEN cursor_name

<a id="98b092e1fb442ce0"></a>
### 기능

커서를 연다.

<a id="db84b12ef8ad35a9"></a>
### 구문

```
<open statement> ::=
    OPEN cursor_name [ <parameter using clause> ]
    ;

<parameter using clause> ::=
      <using parameter arguments>

<using parameter arguments> ::=
    USING variable_name [, ...]
```

<a id="048a98bb458aed87"></a>
### 사용 범위 및 접근 권한

cursor_name이 [PREPARE statement_name](#ebbfd3f86e32b694) 구문과 [DECLARE cursor_name](#c0f5909b51d661a3) 구문을 사용해 선언한 동적 커서인 경우 embedded SQL에서 사용 가능하다.

cursor_name을 선언한 [DECLARE cursor_name](#c0f5909b51d661a3) 구문에 포함된 &lt;[cursor query&gt;](#fcfb72546e402a52)의 권한과 동일하다.

<a id="c8997a0ca8ddb91d"></a>
### 구문 규칙 및 파라미터

<a id="63c0ace1c70e178d"></a>
#### cursor_name

세션 내에서 [DECLARE cursor_name](#c0f5909b51d661a3) 구문으로 선언된 커서여야 한다.

<a id="eee06a52ed7d03b6"></a>
#### &lt;parameter using clause&gt;

Embedded SQL에서 사용할 수 있다.

&lt;parameter using clause&gt; 구문이 사용될 경우, cursor_name이 [PREPARE statement_name](#ebbfd3f86e32b694) 구문과 [DECLARE cursor_name](#c0f5909b51d661a3) 구문을 이용해 선언한 동적 커서여야 한다.

<a id="3b5bbaabbe18a354"></a>
#### &lt;using parameter arguments&gt;

&lt;using parameter arguments&gt; 구문이 사용될 경우, variable_name의 개수는 [PREPARE statement_name](#ebbfd3f86e32b694) 구문이 참조하는 query 문장에 포함된 parameter의 개수와 동일해야 한다.

variable_name은 나열된 순서에 따라 dynamic parameter에 순서대로 대응된다.

```
{
    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT c1, c2 FROM t1 WHERE c1 IN ( ?, ?, ? )';
    EXEC SQL DECLARE cur1 CURSOR FOR stmt1;
    EXEC SQL OPEN cur1 USING :sValue1, :sValue2, :sValue3;
    ...
    EXEC SQL WHENEVER NOT FOUND DO break;
    for(;;)
    {
        EXEC SQL FETCH cur1 INTO :sC1, :sC2;    
    }
    EXEC SQL WHENEVER NOT FOUND CONTINUE;
    ...
    EXEC SQL CLOSE cur1;    
    ... 
}
```

<a id="d8bb5d1748de2cd3"></a>
### 설명

Cursor는 session 내에서 구별되는 객체이며, 현재 session 내에서 사용되고 있는 cursor는 다른 session에서 사용되고 있는 cursor와 무관하다.

OPEN cursor_name 구문을 사용하려면 [DECLARE cursor_name](#c0f5909b51d661a3) 구문으로 선언된 커서여야 하며, 커서는 닫혀 있는 상태여야 한다.

<a id="833dd557eb87c684"></a>
### 사용 예

다음은 interactive SQL (gsql)에서 cursor를 선언하고 OPEN cursor 구문을 사용하는 예이다.

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

<a id="1b71c372843889c6"></a>
### 호환성

**SQL 표준 호환성**

<a id="6d79a55daf9c6fab"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |

<a id="65908ecc2751da46"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#c0f5909b51d661a3)
- [FETCH cursor_name](#f8b0914239210b68)
- [CLOSE cursor_name](#c718855fa5a651b0)
- [PREPARE statement_name](#ebbfd3f86e32b694)

<a id="ebbfd3f86e32b694"></a>
## PREPARE statement_name

<a id="f7c343ad3d66e5f6"></a>
### 기능

반복 수행을 위한 dynamic SQL 문장을 준비한다.

<a id="0feee36b973a4514"></a>
### 구문

```
<prepare statement> ::=
    PREPARE statement_name FROM <SQL statement variable>
    ;

<SQL statement variable> ::=
      variable_name
    | 'sql statement'
    | "sql statement"
    | sql statement
```

<a id="09a51c75cfde274d"></a>
### 사용 범위 및 접근 권한

Embedded SQL에서 사용할 수 있다.  
Dynamic SQL 구문의 종류에 부합하는 수행 권한이 있어야 한다.

<a id="25ca187d4f506932"></a>
### 구문 규칙 및 파라미터

<a id="5e7d78983b7123df"></a>
#### statement_name

준비할 statement의 이름이다.  
statement 이름의 길이는 128 바이트보다 작아야 한다.  
이후에 수행될 [EXECUTE statement_name](#0220fe9761f46bb1) 구문 또는 [DECLARE cursor_name](#c0f5909b51d661a3) 구문은 statement_name을 참조한다.  
동일한 statement_name이 존재할 경우, 이전에 준비된 dynamic SQL은 삭제된다.

```
{
    ...

    EXEC SQL PREPARE stmt1 FROM 'DELETE FROM t1';
    ...
    EXEC SQL PREPARE stmt1 FROM 'UPDATE t1 SET c1 = c1 + 10';
    ...
}
```

<a id="9ab906b622be79e6"></a>
#### &lt;SQL statement variable&gt;

&lt;SQL statement variable&gt;은 다음과 같이 네 가지 유형으로 사용된다.

- variable_name: SQL이 저장된 변수 
- 'sql statement': Single quote (')로 묶인 SQL 문장 
- "sql statement": Double quote (")로 묶인 SQL 문장 
- sql statement: Quote 없는 SQL 문장

Single-quoted string 내에 문자열 data를 표현하려면 다음과 같이 single quote (')를 두 번 기술한다.

```
{
    ...
    PREPARE stmt_name FROM 'INSERT INTO t1 VALUES ( ''literal data'' )'; 
    ...
}
```

&lt;SQL statement variable&gt;이 참조하는 dynamic SQL 문장은 host 변수 (:var)나 parameter marker (?)를 사용할 수 있다.  
단, quote 없는 SQL 문장을 사용할 경우 parameter marker (?)를 사용할 수 없다.

참조되는 dynamic SQL 문장의 특성에 따라 변수는 input 또는 output dynamic parameter가 된다.  
Dynamic SQL 문장 내에 기술된 dynamic parameter는 변수의 이름이 아무 의미가 없으며 종류에 관계없이 구문에 기술된 순서에 따라 식별된다.

- 예제 1

```
{
    ...
    int sValue1;
    int sValue2;
    ...
    EXEC SQL PREPARE stmt1 FROM 'DELETE FROM t1 WHERE c1 BETWEEN ? AND ?';
    EXEC SQL EXECUTE stmt1 USING :sValue1, :sValue2;   
    ...
}
```

- 모든 parameter marker가 input dynamic parameter이다. 
- 식별 순서 
    - 1번 - BETWEEN ? 
        - Input dynamic parameter 
        - :sValue1 값을 사용한다. 
    - 2번 - AND ? 
        - Input dynamic parameter 
        - :sValue2 값을 사용한다.

- 예제 2

```
{
    ...
    int sValue1;
    int sValue2;
    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT SUM(c2) INTO :v1 FROM t1 WHERE c1 > :v2';
    EXEC SQL EXECUTE stmt1 USING :sValue1, :sValue2;
    ...
}
```

- Input dynamic parameter와 output dynamic parameter가 존재한다. 
- 식별 순서 
    - 1번 - :v1 
        - Output dynamic parameter 
        - :sValue1에 값이 저장된다. 
    - 2번 - :v2 
        - Input dynamic parameter 
        - :sValue2 값을 사용한다.

<a id="a44b848c92c736d0"></a>
#### variable_name

variable_name에 대응하는 type은 character string이어야 한다.  
variable_name에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="3387fad5f23a815b"></a>
#### sql statement

sql statement에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="1698c601752b17ba"></a>
### 설명

PREPARE statement_name FROM sql_string 구문은 EXECUTE나 cursor를 사용하기 위해 SQL 문을 분석한다. statement_name은 embedded SQL 소스 코드에서 precompiler에게 statement를 알려주는 식별자로써 host variable이 아니기 때문에 별도의 type이나 선언이 필요하지 않다.

자세한 내용은 [Embedded Dynamic SQL](../part-05-developer-manual/27-embedded-sql.md#e652d9727ea939cd)을 참조한다.

<a id="58a78468e739daa7"></a>
### 사용 예

다음은 embedded SQL 소스 코드 내에서 PREPARE statement_name를 사용하는 예이다.

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

PREPARE statement_name이 사용된 전체 소스 코드는 [Dynamic Embedded SQL Example Program](../part-05-developer-manual/27-embedded-sql.md#863693205873a3d5)에서 확인할 수 있다.

<a id="a3c79e66178ec393"></a>
### 호환성

**SQL 표준 호환성**

<a id="f659d5c2d96e815d"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |
| B034 | Dynamic specification of cursor attributes | X |

<a id="6adb0cfc87ebe4a9"></a>
### 참조

관련 내용은 다음을 참조한다.

- [EXECUTE statement_name](#0220fe9761f46bb1)
- [DECLARE cursor_name](#c0f5909b51d661a3)
- [EXECUTE IMMEDIATE 'sql_string'](#c9ffd94cba178e21)
- [Embedded Dynamic SQL](../part-05-developer-manual/27-embedded-sql.md#e652d9727ea939cd)

<a id="2a6527afe2020779"></a>
## RELEASE SAVEPOINT savepoint_specifier

<a id="f0ee219d14018d42"></a>
### 기능

저장점을 제거한다.

<a id="a87fd26778dac1d5"></a>
### 구문

```
<release savepoint statement> ::=
    RELEASE SAVEPOINT savepoint_name 
    ;
```

<a id="527f7f5aa9dc35c1"></a>
### 구문 규칙 및 파라미터

<a id="33cf1f1865e235e3"></a>
#### savepoint_name

저장점의 이름으로써 반드시 존재해야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="050fdadc7c6fd177"></a>
### 설명

다수의 savepoint가 정의되어 있을 경우, RELEASE SAVEPOINT savepoint_name 구문을 수행할 때savepoint_name 이후에 정의된 savepoint도 함께 제거된다.

<a id="574a9d51ba47ecd7"></a>
### 사용 예

다음은 savepoint를 제거하는 예이다.

```
gSQL> RELEASE SAVEPOINT sp2;

Savepoint dropped.
```

<a id="52e79d0c9635c510"></a>
### 호환성

**SQL 표준 호환성**

<a id="440c9a989b08d413"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T271 | Savepoints | O |

<a id="fae871b3dcdb8451"></a>
### 참조

관련 내용은 다음을 참조한다.

- [COMMIT](#75b82fec67e8ca7c)
- [ROLLBACK](#1476005da98d89d8)
- [SAVEPOINT savepoint_specifier](#e403c1a580ceeb98)

<a id="10007ea0946b35a0"></a>
## REVOKE privileges FROM

<a id="f0d93f6a74e72bc0"></a>
### 기능

사용자에게 부여된 권한을 취소한다.

<a id="9c24955f9f9760c0"></a>
### 구문

```
<revoke privilege statement> ::=
    REVOKE [ <revoke option extention> ] <privilege>
      FROM <grantee> [, ...]
      [ <revoke behavior> ]
    ;

<revoke option extention> ::=
      GRANT OPTION FOR

<revoke behavior> ::=
      RESTRICT
    | CASCADE
    | CASCADE CONSTRAINTS
```

<a id="c11213b110eacde8"></a>
### 구문 규칙 및 파라미터

<a id="fb72feec2a2456bb"></a>
#### &lt;privilege&gt;

Revokee (권한을 취소당할 사용자)로부터 취소할 권한이다.

Revoker (구문을 수행하는 사용자)는 다음 조건 중 하나를 만족해야 한다.

- Revoker가 revokee에게 부여한 &lt;privilege&gt;의 경우 
    - Revoker가 revokee에게 부여한 &lt;privilege&gt;만 취소한다. 
- Revoker가 ACCESS CONTROL ON DATABASE 권한을 소유한 경우
    - 다른 grantor들이 revokee에게 부여한 &lt;privilege&gt;들을 취소한다.

ALL [PRIVILEGES]를 사용하는 경우, 만족하는 &lt;privilege&gt;가 없더라도 성공한다.

&lt;privilege&gt; 종류에 대한 내용은 [GRANT privileges TO](#7961f4f3fe98c65c) 구문의 &lt;[privilege&gt;](#e786e2084fc95103) 절을 참조한다.

<a id="b371d9ca5ed6b832"></a>
#### &lt;grantee&gt;

권한을 취소당할 사용자이다.

- user_identifier 
    - 해당 사용자의 권한을 취소한다. 
- PUBLIC 
    - 모든 사용자를 의미하는 authorization 객체이다.

<a id="034fb4d80dd7190a"></a>
#### GRANT OPTION FOR

권한에 포함된 WITH GRANT OPTION을 삭제한다.  
Dependent privilege의 WITH GRANT OPTION도 함께 삭제한다.

권한은 그대로 유지된다.

<a id="a43ed31b61a00a8e"></a>
#### &lt;revoke behavior&gt;

- Dependent privilege: WITH GRANT OPTION으로 &lt;privilege&gt;를 부여받은 revokee가 다른 사용자에게 부여한 것과 동일한 &lt;privilege&gt;이다.
- RESTRICT 
    - Dependent privilege가 존재할 경우 revoke 할 수 없다. 
- CASCADE 
    - Dependent privilege도 함께 revoke 한다.
- CASCADE CONSTRAINTS 
    - Dependent privilege도 함께 revoke 한다.
- 생략할 경우, 기본값은 CASCADE 이다.

<a id="8fe406ef1d3081e1"></a>
### 설명

REVOKE privilege와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

다음과 같은 DROP 구문을 수행할 경우, 별도로 REVOKE 구문을 수행하지 않더라도 해당 객체와 관련된 모든 권한 정보가 삭제된다.

- SQL schema object 관련 DROP 구문
    - [DROP TABLE](#44de11d586092a30)
    - [DROP VIEW](#ae1beb0ccf35bd56)
    - [DROP SEQUENCE](#7debf989c0a88d02)
    - [ALTER TABLE name SET UNUSED COLUMN](#f310a3fb90803c42)
    - [DROP FUNCTION](../part-04-psm-manual/24-psm-sql-references.md#2e3b5a779150ed13)
    - [DROP PROCEDURE](../part-04-psm-manual/24-psm-sql-references.md#3808c8dd15ec4e09)

- Non-schema object 관련 DROP 구문
    - [DROP SCHEMA](#c2e1f942afbed8da)
    - [DROP TABLESPACE](#4aecf03632f3116f)
    - [DROP USER](#d82c6e3b5b385afc)

<a id="bc8331652e87e042"></a>
### 사용 예

다음은 table t1에 대한 다수의 권한을 REVOKE하는 예이다.

```
gSQL> REVOKE INSERT, UPDATE, DELETE, LOCK, ALTER, INDEX ON t1 FROM u1;

Revoke succeeded.
```

다음은 모든 사용자를 의미하는 PUBLIC 계정에 부여된 SELECT ON TABLE t1 권한을 REVOKE 하는 예이다. 단, PUBLIC 계정의 권한만 제거될 뿐 특정 사용자에게 명시적으로 부여된 SELECT ON TABLE t1 권한이 제거되는 것은 아니다.

```
gSQL> REVOKE SELECT ON t1 FROM PUBLIC;

Revoke succeeded.
```

다음은 user u1에게 부여된 SELECT ON TABLE t1 권한은 그대로 두고 다른 사용자에게 해당 권한을 부여할 수 있는 GRANT OPTION만 REVOKE하는 예이다.

```
gSQL> REVOKE GRANT OPTION FOR SELECT ON t1 FROM u1;

Revoke succeeded.
```

다음은 RESTRICT 옵션을 이용해 user u1에게 부여한 권한을 REVOKE 하면서 u1이 다른 사용자에게 해당 권한을 부여할 경우 에러가 발생하는 예이다. 이런 dependent privilege들도 함께 제거하려 할 경우 CASCADE 옵션을 사용한다.

```
gSQL> REVOKE SELECT ON t1 FROM u1 RESTRICT;

ERR-2B000(16235): dependent privilege descriptors still exist

gSQL> REVOKE SELECT ON t1 FROM u1 CASCADE;

Revoke succeeded.
```

<a id="0d3bec3a910f549c"></a>
### 호환성

SQL 표준에서는 다음 privilege들을 정의하지 않고 있다.

- &lt;database privilege&gt; 
- &lt;tablespace privilege&gt; 
- &lt;schema privilege&gt;

SQL 표준의 &lt;revoke behavior&gt;와는 다음과 같은 차이가 있다.

- SQL 표준의 기본값은 RESTRICT 이다. 
- SQL 표준에는 CASCADE CONSTRAINTS 가 없다.

**SQL 표준 호환성**

<a id="771323d154b1a3aa"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T311 | Basic roles | X |
| F034 | Extended REVOKE statement | X |
| S081 | Subtables | X |

<a id="f71760755938a910"></a>
### 참조

관련 내용은 다음을 참조한다.

- [GRANT privileges TO](#7961f4f3fe98c65c)
- &lt;[database privilege&gt;](#e8a5e0aedacbceb0)
- &lt;[tablespace privilege&gt;](#010f08548f153467)
- &lt;[schema privilege&gt;](#3aa491f1275cabe3)
- &lt;[table privilege&gt;](#de4e2dc44c90dabd)
- [Column privilege ](#1535c9d1293d6302)
- &lt;[sequence privilege&gt;](#297f76199ae58056)

<a id="1476005da98d89d8"></a>
## ROLLBACK

<a id="f1ddf4212072f63b"></a>
### 기능

트랜잭션을 취소하거나, 저장점 이후의 작업을 취소한다.

<a id="55d9becca00ef661"></a>
### 구문

```
<rollback statement> ::=
    ROLLBACK [ WORK ] [ <rollback force clause> | <savepoint clause> ]
    ;

<rollback force clause> ::=
    FORCE 'xid_string' [ COMMENT 'comment_string' ]

<savepoint clause> ::=
    TO SAVEPOINT savepoint_name
```

<a id="dde6489d616ee327"></a>
### 구문 규칙 및 파라미터

<a id="247c9e55c87f24e0"></a>
#### WORK

동작에 영향을 미치지 않는 예약어이다.

<a id="c358d2679e2f9495"></a>
#### &lt;rollback force clause&gt;

분산 트랜잭션을 수동으로 rollback 할 때 사용한다.

- FORCE 'xid_string'
    - 'xid_string'에 해당하는 분산 트랜잭션을 rollback 한다.
    - 'xid_string'은 'format_id.transaction_id.branch_id'로 구성된다.
- COMMENT 'comment_string'
    - 분산 트랜잭션을 rollback 할 때 트랜잭션에 주석을 명시한다.

<a id="4d0ba478ebaff5af"></a>
#### &lt;savepoint clause&gt;

현재 트랜잭션의 ROLLBACK 범위를 명시한다.

- 명시하지 않은 경우 
    - 현재 트랜잭션의 모든 작업을 취소한다. 
    - 트랜잭션을 종료한다. 
    - 모든 savepoint들을 제거한다. 
    - 모든 lock들을 해제한다.

- TO SAVEPOINT savepoint_name 
    - 현재 트랜잭션에서 savepoint_name 이후의 작업을 취소한다. 
    - 트랜잭션을 종료하지는 않는다. 
    - savepoint_name 이후의 savepoint들을 제거한다. 
    - savepoint_name 이후에 획득한 lock들을 해제한다.

<a id="f381d399fafd378e"></a>
### 설명

ROLLBACK 구문은 트랜잭션 내에서 수행된 다음 구문들을 rollback 한다.

- Data Manipulation Language (DML) 구문
    - 데이터를 변경하는 INSERT, UPDATE, DELETE 등의 구문
- Data Definition Language (DDL) 구문 
    - 객체의 구조 및 정의를 변경하는 CREATE, DROP, ALTER, TRUNCATE, GRANT, REVOKE 등의 구문

예외적으로, DDL 중에 OS 자원을 다루거나 DATA TYPE을 변경하는 다음 구문들은 rollback 되지 않고 구문을 수행할 때 자동으로 COMMIT 된다.

- [CREATE TABLESPACE](#df51248e3216ce23)
- [DROP TABLESPACE](#4aecf03632f3116f)
- [ALTER TABLESPACE](#c308f53537323289)
- ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE: &lt;[alter column data type clause&gt;](#76fd82a3da886b7c)

<a id="e1781fcc1fd43e19"></a>
### 사용 예

다음은 INSERT 구문을 ROLLBACK 하는 예이다.

```
gSQL> INSERT INTO t1 VALUES ( 1, 'anonymous' );

1 row created.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous

1 row selected.

gSQL> ROLLBACK;

Rollback complete.

gSQL> SELECT * FROM t1;

no rows selected.
```

다음은 DROP TABLE 구문을 수행한 후에 이를 ROLLBACK 하는 예이다.

```
gSQL> DROP TABLE t1;

Table dropped.

gSQL> SELECT * FROM t1;

ERR-42000(16040): table or view does not exist : 
SELECT * FROM t1
              *
ERROR at line 1:

gSQL> ROLLBACK;

Rollback complete.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous

1 row selected.
```

<a id="58ec2076b23eac8f"></a>
### 호환성

**SQL 표준 호환성**

<a id="b79728cc3c7ab247"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T271 | Savepoints | O |
| T261 | Chained transactions | X |

<a id="d62417b6d0062a32"></a>
### 참조

관련 내용은 다음을 참조한다.

- [COMMIT](#75b82fec67e8ca7c)
- [SAVEPOINT savepoint_specifier](#e403c1a580ceeb98)

<a id="e403c1a580ceeb98"></a>
## SAVEPOINT savepoint_specifier

<a id="ece918c2679fa19b"></a>
### 기능

저장점을 정의한다.

<a id="8a14c206af0db291"></a>
### 구문

```
<savepoint statement> ::=
    SAVEPOINT savepoint_name 
    ;
```

<a id="d70e21a423278036"></a>
### 구문 규칙 및 파라미터

<a id="b7db5182c23a1e1f"></a>
#### savepoint_name

저장점 이름이다.  
저장점 이름이 기존의 저장점 이름과 중복될 경우 기존의 저장점이 삭제된다.  
이름의 길이는 128 바이트보다 작아야 한다.

<a id="d1bae37bcc375510"></a>
### 설명

정의된 savepoint는 ROLLBACK TO SAVEPOINT 구문 ([ROLLBACK](#1476005da98d89d8) 구문 참조)에서 사용되며, 해당 savepoint까지 수행된 DML, DDL 구문이 철회되고 해당 구문이 획득한 lock도 해제된다.

정의된 savepoint는 transaction을 COMMIT 하거나 ROLLBACK 할 때 자동으로 제거되는데 [RELEASE SAVEPOINT savepoint_specifier](#2a6527afe2020779) 구문을 사용하여 명시적으로 제거할 수도 있다.

<a id="0daf90ed5a9499b0"></a>
### 사용 예

다음은 savepoint를 정의하고 ROLLBACK TO SAVEPOINT 구문을 사용하는 예이다.

```
gSQL> SAVEPOINT sp1;

Savepoint created.

gSQL> INSERT INTO t1 VALUES ( 1, 'anonymous' );

1 row created.

gSQL> SAVEPOINT sp2;

Savepoint created.

gSQL> INSERT INTO t1 VALUES ( 2, 'someone' );

1 row created.

gSQL> SAVEPOINT sp3;

Savepoint created.

gSQL> INSERT INTO t1 VALUES ( 3, 'anyone' );

1 row created.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous
 2 someone  
 3 anyone   

3 rows selected.

gSQL> ROLLBACK TO SAVEPOINT sp3;

Rollback complete.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous
 2 someone  

2 rows selected.

gSQL> ROLLBACK TO SAVEPOINT sp2;

Rollback complete.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous

1 row selected.

gSQL> ROLLBACK TO SAVEPOINT sp1;

Rollback complete.

gSQL> SELECT * FROM t1;

no rows selected.
```

<a id="e938c588e7072e99"></a>
### 호환성

**SQL 표준 호환성**

<a id="9a1eec3aaccb0249"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T271 | Savepoints | O |

<a id="3c91559460a47436"></a>
### 참조

관련 내용은 다음을 참조한다.

- [COMMIT](#75b82fec67e8ca7c)
- [ROLLBACK](#1476005da98d89d8)
- [RELEASE SAVEPOINT savepoint_specifier](#2a6527afe2020779)

<a id="c9d76bf073f60db2"></a>
## SELECT

<a id="1c4140d8d3200490"></a>
### query expression

<a id="92cde69c58be7b45"></a>
#### 기능

하나 이상의 table 또는 view에서 원하는 row를 검색한다.

<a id="4e7623c270f7c740"></a>
#### 구문

```
<query expression> ::=
    <query expression body> [ <order by clause> ] [ <offset limit clause> ]

<query expression body> ::=
      <query term>
    | <set operator>

<query term> ::=
      <query specification>
    | <left paren> <query expression body> [ <order by clause> ] [ <offset limit clause> ] <right paren>
```

<a id="6537d8049c89c359"></a>
#### 사용 범위 및 접근 권한

&lt;query expression&gt; 구문을 수행하려면 사용자가 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나를 가져야 한다.

- 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
- 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- SELECT ANY TABLE ON DATABASE

<a id="e03ba30e868dc647"></a>
#### 구문 규칙 및 파라미터

<a id="79754f61454f49fe"></a>
##### &lt;set operator&gt;

부질의 (subquery) 간의 집합 연산을 수행한다.  
자세한 내용은 [set operator](#96acd09fad234c3f) 절을 참조한다.

<a id="875bff9847ab694b"></a>
##### &lt;query specification&gt;

하나의 부질의 (subquery)를 기술한다.  
자세한 내용은 [query specification](#d8630e2bdbb32181) 절을 참조한다.

<a id="87a682cdcff8a6d1"></a>
##### &lt;order by clause&gt;

검색 결과에 대한 정렬 정보를 기술한다.  
자세한 내용은 [order by clause](#39da5d5114d359af)를 참조한다.

<a id="a348b0d8addfbd88"></a>
##### &lt;offset limit clause&gt;

검색 결과 집합에서 skip 할 row의 개수와 fetch 할 row의 개수를 기술한다.  
자세한 내용은 [offset limit clause](#37f82ae17691b17d)를 참조한다.

<a id="487bb5f1b5a0dda3"></a>
#### 설명

SELECT 구문을 기술하는 것으로써 &lt;order by clause&gt;, &lt;offset limit clause&gt;는 생략할 수 있고 &lt;set operator&gt;를 사용하여 둘 이상의 부질의 (subquery)를 가질 수 있다.

<a id="3219186ad44098c7"></a>
#### 사용 예

다음은 SELECT 구문의 예이다.

```
gSQL> SELECT s_name, s_nation FROM supplier;

S_NAME                    S_NATION     
------------------------- -------------
Supplier#1                FRANCE       
Supplier#2                KOREA        
Supplier#3                GERMANY      
Supplier#4                UNITED STATES
Supplier#5                CANADA       

5 rows selected.
```

다음은 &lt;order by clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT s_name, s_nation FROM supplier ORDER BY s_name DESC;

S_NAME                    S_NATION
------------------------- -------------
Supplier#5                CANADA
Supplier#4                UNITED STATES
Supplier#3                GERMANY
Supplier#2                KOREA
Supplier#1                FRANCE

5 rows selected.
```

다음은 &lt;offset limit clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT s_name, s_nation FROM supplier OFFSET 1;

S_NAME                    S_NATION
------------------------- -------------
Supplier#2                KOREA
Supplier#3                GERMANY
Supplier#4                UNITED STATES
Supplier#5                CANADA

4 rows selected.

gSQL> SELECT s_name, s_nation FROM supplier LIMIT 1; 

S_NAME                    S_NATION
------------------------- --------
Supplier#1                FRANCE  

1 row selected.
```

다음은 &lt;order by clause&gt;와 &lt;offset limit clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT s_name, s_nation FROM supplier ORDER BY s_name DESC OFFSET 3 LIMIT 1; 

S_NAME                    S_NATION
------------------------- --------
Supplier#2                KOREA   

1 row selected.
```

<a id="25a319c39bbde465"></a>
#### 호환성

**SQL 표준 호환성**

<a id="852436c849f14907"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T121 | WITH (excluding RECURSIVE ) in query expression | X |
| T122 | WITH (excluding RECURSIVE ) in subquery | X |
| T131 | Recursive query | X |
| T132 | Recursive query in subquery | X |
| F661 | Simple tables | O |
| F302 | INTERSECT table operator | O |
| F301 | CORRESPONDING in query expressions | X |
| T551 | Optional key words for default syntax | O |
| F304 | EXCEPT ALL table operator | O |
| F850 | Top-level &lt;order by clause&gt;in &lt;query expression&gt; | X |
| F851 | &lt;order by clause&gt;in subqueries | O |
| F855 | Nested &lt;order by clause&gt;in &lt;query expression&gt; | O |
| F856 | Nested &lt;fetch first clause&gt;in &lt;query expression&gt; | X |
| F857 | Top-level &lt;fetch first clause&gt;in &lt;query expression&gt; | X |
| F858 | &lt;fetch first clause&gt;in subqueries | X |
| F860 | dynamic &lt;fetch first row count&gt;in &lt;fetch first clause&gt; | X |
| F861 | Top-level &lt;result offset clause&gt;in &lt;query expression&gt; | O |
| F862 | &lt;result offset clause&gt;in subqueries | O |
| F863 | Nested &lt;result offset clause&gt;in &lt;query expression&gt; | O |
| F865 | dynamic &lt;offset row count&gt;in &lt;result offset clause&gt; | X |
| F866 | FETCH FIRST clause: PERCENT option | X |
| F867 | FETCH FIRST clause: WITH TIES option | X |

<a id="d8630e2bdbb32181"></a>
### query specification

<a id="63ced9a1724a0543"></a>
#### 기능

&lt;table expression&gt; 결과로부터 파생된 table을 기술한다.

<a id="a7ae6e0dd26ebdb8"></a>
#### 구문

```
<query specification> ::=
    SELECT [ <hint clause> ] [ <set quantifier> ] <select list> <table expression>

<set quantifier> ::=
      ALL
    | DISTINCT

<table expression> ::=
      <from clause> [ <where clause> ] [ <group by clause> ] [ <having clause> ]
```

<a id="1af8da38e411379a"></a>
#### 사용 범위 및 접근 권한

&lt;query specification&gt; 구문을 수행하려면 사용자가 다음 조건 중 하나를 만족해야 한다.

- 테이블의 소유자 
- 테이블에 대한 SELECT 권한 
- 테이블이 속한 스키마에 대해 SELECT TABLE, CONTROL TABLE, CONTROL 권한 중 하나를 소유 
- Database에 대한 SELECT TABLE 권한을 소유

<a id="8b5610ef782fa889"></a>
#### 구문 규칙 및 파라미터

<a id="33ae6a844fb39387"></a>
##### &lt;hint clause&gt;

질의 수행에 필요한 힌트를 기술한다.  
자세한 내용은 [hint clause](#a12a3515f3dbcd31)를 참조한다.

<a id="74f5d1a26ff05879"></a>
##### &lt;set quantifier&gt;

질의 결과의 중복 제거 여부를 기술한다.  
생략할 경우, ALL과 동일하게 동작한다.

<a id="07ed07107686e361"></a>
##### &lt;select list&gt;

검색 결과 중 결과로 내보낼 expression들을 기술한다.  
자세한 내용은 [select list](#d37df5771ea1cca7)를 참조한다.

<a id="577e119845407187"></a>
##### &lt;from clause&gt;

검색할 table들을 기술한다.  
자세한 내용은 [from clause](#43529f212b19c0e0)를 참조한다.

<a id="f2240403b4787541"></a>
##### &lt;where clause&gt;

검색 조건을 기술한다.  
자세한 내용은 [where clause](#8ffd103d5116485d)를 참조한다.

<a id="a694f90f85fdb5c3"></a>
##### &lt;group by clause&gt;

검색 결과에 대한 grouping을 기술한다.  
자세한 내용은 [group by clause](#a73fcd9d4ff882ea)를 참조한다.

<a id="a59c01241f886750"></a>
##### &lt;having clause&gt;

Grouping 된 결과에 대한 조건을 기술한다.  
자세한 내용은 [having clause](#d406655ebf1a0fb1)를 참조한다.

<a id="aaf5f219cfac6263"></a>
#### 설명

<a id="03008b2de60bb05f"></a>
##### &lt;hint clause&gt;

&lt;hint clause&gt;는 optimizer가 선택한 실행 계획보다 더 좋은 실행 계획이 있는 경우 사용자가 optimizer에게 더 좋은 실행 계획을 수행하도록 지시하는 구문이다.

GOLDILOCKS의 optimizer는 사용자가 기술한 &lt;hint clause&gt;를 우선 적용한다.   
만약 적용할 수 없을 경우에는 cost 계산을 통해 최적의 실행 계획을 선택한다.

GOLDILOCKS는 &lt;hint clause&gt;에 구문상 에러가 발생하더라도 이를 무시하고 진행하도록 기본 설정되어 있다. &lt;hint clause&gt;에 구문상 에러가 있는지 확인하려면 "HINT_ERROR" property를 *on*으로 설정하고 질의를 수행하도록 한다.

<a id="0ec534f245c399e1"></a>
##### &lt;set quantifier&gt;

&lt;set quantifier&gt;는 &lt;select list&gt;에 기술된 expression들로써 구성된 각 row의 중복 제거 여부를 설정하며 각 set quantifier의 의미는 다음과 같다.

- ALL: 결과 집합에서 중복을 제거하지 않는다.
- DISTINCT: 결과 집합에서 중복을 제거한다.

&lt;set quantifier&gt;는 생략할 수 있는데 생략할 경우, default로 ALL이 설정된 것과 동일하게 동작한다.

<a id="a4e9f47c05af8048"></a>
##### &lt;select list&gt;

&lt;select list&gt;는 결과 집합의 각 row에서 반환할 expression들의 목록을 기술한다. 이 목록은 콤마 (,) 리스트로 구분하여 기술할 수 있으며, &lt;from clause&gt;에 기술한 모든 column들을 기술하고 싶은 경우에는 별표 (*)를 사용한다.

<a id="3f3088c4dbea16e9"></a>
##### &lt;from clause&gt;

&lt;from clause&gt;는 검색할 table 또는 view들을 기술한다.

<a id="47f4471241efb186"></a>
##### &lt;where clause&gt;

&lt;where clause&gt;는 &lt;table expression&gt;으로부터 얻은 결과 집합 중에 원하는 결과만 가져오도록 검색 조건을 기술한다.

<a id="58c903a35c496261"></a>
##### &lt;group by clause&gt;

&lt;group by clause&gt;는 &lt;table expression&gt;으로부터 얻은 결과 집합을 grouping 할 방법을 기술한다.

&lt;group by clause&gt;가 기술된 경우, &lt;select list&gt;에는 group을 결정하는 group key나 group에 속하는 데이터에 대한 집계 함수만 사용할 수 있다.

<a id="5b7a1caa7e776038"></a>
##### &lt;having clause&gt;

&lt;having clause&gt;는 grouping된 결과 집합 중에 원하는 결과만 가져오도록 group에 대한 검색 조건을 기술한다.  
일반적으로 &lt;group by clause&gt;와 함께 사용되며, &lt;group by clause&gt; 없이 사용된 경우 &lt;table expression&gt;에서 반환된 결과 집합 모두가 하나의 group인 &lt;group by clause&gt;가 기술된 것과 동일하게 동작한다.

<a id="c81d94248e89cb2d"></a>
#### 사용 예

다음은 &lt;hint clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT /*+ INDEX_DESC(supplier, supplier_pk_index) */ s_name, s_nation FROM supplier;

S_NAME                    S_NATION
------------------------- -------------
Supplier#5                CANADA
Supplier#4                UNITED STATES
Supplier#3                GERMANY
Supplier#2                KOREA
Supplier#1                FRANCE

5 rows selected.
```

다음은 &lt;set quantifier&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT ALL p_type FROM part;

P_TYPE
------
COPPER
NICKEL
STEEL
NICKEL
STEEL

5 rows selected.

gSQL> SELECT DISTINCT p_type FROM part;

P_TYPE
------
COPPER
STEEL
NICKEL

3 rows selected.
```

다음은 &lt;where clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT p_name, p_brand, p_type, p_size FROM part where p_size < 10;

P_NAME P_BRAND    P_TYPE P_SIZE
------ ---------- ------ ------
Part#1 Brand#1    COPPER      7
Part#2 Brand#1    NICKEL      1

2 rows selected.
```

다음은 &lt;group by clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT ps_partkey, SUM(ps_availqty) FROM partsupp GROUP BY ps_partkey;

PS_PARTKEY SUM(PS_AVAILQTY)
---------- ----------------
         1            11401
         2             8025
         3            13864
         4            11564
         5             8744

5 rows selected.
```

다음은 &lt;having clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT ps_partkey, SUM(ps_availqty) FROM partsupp GROUP BY ps_partkey having SUM(ps_availqty) > 10000;

PS_PARTKEY SUM(PS_AVAILQTY)
---------- ----------------
         1            11401
         3            13864
         4            11564

3 rows selected.
```

<a id="a98474cfa3699062"></a>
#### 호환성

**SQL 표준 호환성**

<a id="a1f1dd6a679451d7"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F801 | Full set function | X |
| T051 | Row types | X |
| T301 | Functional dependencies | X |
| T325 | Qualified SQL parameter references | X |
| T053 | Explicit aliases for all-fields reference | O |
| T285 | Enhanced derived column names | O |

<a id="c5153b680a5c4478"></a>
#### 참조

관련 내용은 [query expression](#1c4140d8d3200490)을 참조한다.

<a id="d37df5771ea1cca7"></a>
### select list

<a id="f49fba19d9833476"></a>
#### 기능

질의 결과로부터 검색할 column을 기술한다.

<a id="a3bd236aa0876050"></a>
#### 구문

```
<select list> ::=
      <asterisk>
    | <select sublist> [ { <comma> <select sublist> } ... ]

<select sublist> ::=
      <derived column>
    | <qualified asterisk>

<qualified asterisk> ::=
      <asterisked identifier chain> <period> <asterisk>

<asterisked identifier chain> ::=
    <asterisked identifier> [ { <period> <asterisked identifier> } ... ]

<derived column> ::=
    <value expression> [ <as clause> ]

<as clause> ::=
    [ AS ] <column name>
```

<a id="7c238e2645570f90"></a>
#### 사용 범위 및 접근 권한

&lt;select list&gt; 구문에 column이나 subquery가 존재할 때 &lt;select list&gt; 구문을 수행하려면 사용자가 column에 대한 접근 권한과 subquery에 존재하는 table 및 column에 대한 접근 권한을 만족해야 한다.

<a id="48f5c497855d112f"></a>
#### 구문 규칙 및 파라미터

<a id="fac5214411c9445a"></a>
##### &lt;select list&gt;

&lt;asterisk&gt;나 &lt;select sublist&gt;를 갖는다.  
&lt;asterisk&gt;는 &lt;select list&gt;에 단독으로만 쓰일 수 있다. 즉, &lt;select sublist&gt;를 기술할 수 없다.  
둘 이상의 &lt;select sublist&gt;를 기술할 경우, 각 &lt;select sublist&gt;를 콤마 (,)로 구분해야 한다.

<a id="a5b9bce2adbdbf86"></a>
##### &lt;select sublist&gt;

&lt;derived column&gt;이나 &lt;qualified asterisk&gt;를 갖는다.  
테이블 하나당 한 개의 &lt;quantified asterisk&gt;만 가질 수 있다.  
&lt;derived column&gt;은 AS를 사용하여 출력 이름을 변경할 수 있으며, AS는 생략할 수 있다.

<a id="48f6ad02e6b3e5f5"></a>
#### 설명

<a id="de0ea593e3c5eb43"></a>
##### &lt;select list&gt;

&lt;select list&gt;는 결과 집합에 포함될 column들을 기술한다. &lt;select list&gt;에 &lt;asterisk&gt;를 기술할 경우, &lt;from clause&gt;에 있는 모든 column들을 select list로 설정하며, &lt;select sublist&gt;를 추가로 기술할 수 없다.

<a id="fec8588a60b57930"></a>
##### &lt;select sublist&gt;

&lt;select sublist&gt;는 &lt;derived column&gt; 또는 &lt;qualified asterisk&gt;를 갖는다. &lt;select sublist&gt;를 둘 이상 기술할 경우에는 반드시 콤마 (,)로 구분해야 한다.

&lt;qualified asterisk&gt;는 특정 table이나 view에 속하는 모든 column들을 select list로 설정하고 &lt;derived column&gt;은 column을 직접 기술하거나 &lt;value expression&gt;을 기술할 수 있다.

&lt;derived column&gt;은 &lt;as clause&gt;를 사용하여 column name을 변경할 수 있으며, 이 때 AS는 생략할 수 있다.

<a id="05a0ff52752f9f36"></a>
##### select list에 설정되는 이름

- &lt;derived column&gt;에 &lt;column name&gt;이 명시된 경우, 해당 이름이 select list 이름으로 설정된다.
- &lt;derived column&gt;에 &lt;column name&gt;이 명시되지 않은 경우, 다음과 같이 select list 이름이 설정된다.
    - &lt;derived column&gt;이 single column reference인 경우 single column의 column name이 select list 이름으로 설정된다.
    - &lt;derived column&gt;이 SQL parameter reference인 경우 SQL parameter의 &lt;SQL parameter name&gt;이 select list 이름으로 설정된다.
    - 그 밖의 경우에는 &lt;derived column&gt;의 column name이 설정되지 않는다.
- &lt;from clause&gt;에 둘 이상의 table이 있고 이 중에 이름이 같은 column이 포함되어 있을 때 이 column을 참조하려면 table name이나 table alias를 반드시 명시해야 한다.

<a id="5b0af31044b19e07"></a>
#### 사용 예

다음은 &lt;asterisk&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT * FROM supplier;

S_SUPPKEY S_NAME                    S_NATION      S_PHONE
--------- ------------------------- ------------- ---------------
        1 Supplier#1                FRANCE        27-918-335-1736
        2 Supplier#2                KOREA         15-679-861-2259
        3 Supplier#3                GERMANY       11-383-516-1199
        4 Supplier#4                UNITED STATES 25-843-787-7479
        5 Supplier#5                CANADA        21-151-690-3663

5 rows selected.
```

다음은 &lt;select sublist&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT revenue.* FROM revenue;

SUPPLIER_NO TOTAL_REVENUE
----------- -------------
          1      11978.64
          2       20321.5
          3      41844.68

3 rows selected.

gSQL> SELECT supplier_no suppno, total_revenue AS TOTAL FROM revenue;

SUPPNO    TOTAL
------ --------
     1 11978.64
     2  20321.5
     3 41844.68

3 rows selected.

gSQL> SELECT 1, revenue.*, CAST( total_revenue AS NATIVE_INTEGER ) TOTAL FROM revenue;

1 SUPPLIER_NO TOTAL_REVENUE TOTAL
- ----------- ------------- -----
1           1      11978.64 11979
1           2       20321.5 20322
1           3      41844.68 41845

3 rows selected.
```

<a id="314fe074a47a8a76"></a>
#### 호환성

&lt;select list&gt;와 달리 SQL 표준에서는 &lt;all fields reference&gt;를 지원한다.

<a id="585a24bff3258655"></a>
#### 참조

관련 내용은 [query specification](#d8630e2bdbb32181)을 참조한다.

<a id="43529f212b19c0e0"></a>
### from clause

<a id="8eb8d1ed8e9561c9"></a>
#### 기능

하나 이상의 table들로부터 파생된 table을 기술한다.

<a id="bcc76025d413660c"></a>
#### 구문

```
<from clause> ::=
    FROM <table reference list>

<table reference list> ::=
    <table reference> [ { , <table reference> } ... ]

<table reference> ::=
      <table factor>
    | <joined table>

<table factor> ::=
    <table primary>

<table primary> ::=
      <table name> [ <cluster domain> ] [ [ AS ] <correlation name> ]
    | <derived table> [ <cluster domain> ] [ [ AS ] <correlation name> [ <left paren> <derived column list> <right paren> ] ]
    | <parenthesized joined table>

<derived table> ::=
    <table subquery>

<parenthesized joined table> ::=
      <left paren> <parenthesized joined table> <right paren>
    | <left paren> <joined table> <right paren>

<derived column list> ::=
    <column name list>

<cluster domain> ::=
    @ <cluster domain name>

<cluster domain name> ::=
      GLOBAL
    | LOCAL
    | LOCAL_OFFLINE
    | <identifier>
```

<a id="d94c721a96de142f"></a>
#### 사용 범위 및 접근 권한

&lt;table reference list&gt;에 기술한 table 또는 view에 대한 접근 권한이 있어야 한다.

<a id="391abb4a316e1cfa"></a>
#### 구문 규칙 및 파라미터

<a id="70e405782aa71cdb"></a>
##### &lt;table reference list&gt;

- &lt;table reference list&gt;에는 한 개 이상의 테이블들을 콤마 (,)를 사용하여 기술할 수 있다.
- 두 개 이상의 테이블이 기술된 경우
    - 테이블은 왼쪽에서 오른쪽 방향으로 평가 (evaluation)된다.
    - &lt;select list&gt;에 *를 기술한 경우 왼쪽 테이블의 column부터 오른쪽 테이블의 column까지 순서대로 &lt;select list&gt;에 매핑된다.

<a id="7a2a011d9cc7fe6a"></a>
##### &lt;table primary&gt;

&lt;correlation name&gt;을 사용하여 별칭 (alias name)을 기술할 수 있다.

&lt;derived table&gt;에는 &lt;table subquery&gt;가 있고 &lt;correlation name&gt;을 이용하여 별칭 (alias name)을 기술할 수 있다.  
&lt;derived table&gt;에 &lt;derived column list&gt;를 기술할 수 있으며, &lt;derived column list&gt;의 &lt;column name&gt; 개수는 &lt;table subquery&gt;에 기술한 &lt;select list&gt;의 target 개수와 동일해야 한다.

&lt;derived table&gt;에 &lt;derived column list&gt;를 기술한 경우 &lt;table subquery&gt;에 기술한 &lt;select list&gt;의 target과 순서대로 1 : 1 매핑된다.  
&lt;derived table&gt;에 &lt;derived column list&gt;를 기술한 경우 해당 &lt;derived table&gt;내 &lt;table subquery&gt;의 &lt;select list&gt;를 참조하려면 반드시 &lt;derived column list&gt;에 기술한 &lt;column name&gt;을 사용하여야 한다.

<a id="11e486b910a67d5d"></a>
##### &lt;correlation name&gt;

&lt;table reference list&gt;에는 동일한 &lt;correlation name&gt;이 두 개 이상 존재할 수 없다.

&lt;table name&gt;이나 &lt;derived table&gt;에 &lt;correlation name&gt;이 기술된 경우 해당 &lt;table name&gt;이나  &lt;derived table&gt;을 참조하려면 반드시 &lt;correlation name&gt;을 사용해야 한다.

&lt;correlation name&gt;을 기술할 때 그 앞의 AS는 생략할 수 있다.

<a id="3cd8f63c18b6b2af"></a>
##### &lt;derived column list&gt;

&lt;derived column list&gt;에는 동일한 &lt;column name&gt;이 두 개 이상 존재할 수 없다.

<a id="48cd43b7c72a9c55"></a>
##### &lt;cluster domain&gt;

- &lt;cluster domain&gt;은 table이나 view, table subquery가 될 수 있지만 괄호로 묶인 joined table은 &lt;cluster domain&gt;이 될 수 없다.
- 구조나 데이터가 변경될 table이나 view에는 &lt;cluster domain&gt;을 기술할 수 없다.
    - 단, [Cluster의 SELECT 처리](12-sql-languages.md#278e1b70335c3f98)가 생성한 데이터 변경 query에는 대상 table에 "@LOCAL"을 기술한다.

<a id="1e7ee85b92762302"></a>
##### &lt;cluster domain name&gt;

Cluster group name이나 cluster member name만이 &lt;cluster domain name&gt;의 &lt;identifier&gt;가 될 수 있다.

<a id="f9ef0de7fde9b581"></a>
#### 설명

<a id="98bc02bc75e34482"></a>
##### &lt;table reference list&gt;

&lt;table reference list&gt;에는 콤마 (,)를 사용하여 두 개 이상의 테이블들을 기술할 수 있다. 두 개 이상의 테이블을 기술하면 해당 테이블들을 왼쪽부터 오른쪽으로 각각 cross join하듯 작동하며 이 때 &lt;where clause&gt;에 두 테이블의 join 조건이 존재하는 경우 해당하는 두 테이블은 &lt;where clause&gt;를 join 조건으로 갖는 inner join처럼 동작한다. 만약 &lt;where clause&gt;에 outer join operator (+)를 사용한 경우, outer join과 동일하게 작동한다.

Outer join operator (+)에 대한 자세한 내용은 [joined table](#084d9757859ddaed) 절의 outer join operator specification을 참조한다.

<a id="fbc801ff90e3b16f"></a>
##### &lt;table reference&gt;

단일 table이나 view, table subquery, joined table 등이 &lt;table reference&gt;가 될 수 있다. Joined table을 제외한 나머지는 correlation name을 가질 수 있다.

Joined table에 대한 자세한 내용은 [joined table](#084d9757859ddaed) 절을 참조한다.

<a id="32d9ddc37adc6b80"></a>
##### &lt;table primary&gt;

Table이나 view, table subquery, 괄호로 묶인 joined table이 &lt;table primary&gt;가 될 수 있다. Table이나 view, table subquery는 correlation name을 가질 수 있는데, 이 때 AS는 생략할 수 있다. Correlation name이 기술될 경우, &lt;select list&gt;나 &lt;where clause&gt;와 같이 해당 table이나 view, table subquery를 참조하는 모든 경우에 correlation name을 사용해야 한다.

Table subquery는 괄호를 이용하여 &lt;derived column list&gt;에 기술할 수 있으며, correlation name과 마찬가지로 해당 table subquery의 column을 참조하는 모든 경우에 &lt;derived column list&gt;에 기술한 이름을 사용하여야 한다. Table subquery에 &lt;derived column list&gt;를 사용하려면 correlation name을 반드시 기술하여야 한다.

괄호로 묶은 joined table은 join 연산에 참여하는 table들의 논리적 join 순서를 기술한다. 이 때 괄호로 묶은 모든 table들에 대한 join이 모두 cross join과 inner join일 경우, optimizer가 join 순서를 변경할 수 있다.

<a id="a04abf76011bd07d"></a>
##### &lt;cluster domain&gt;

&lt;cluster domain&gt;이 생략된 경우 &lt;cluster domain name&gt;으로 GLOBAL을 사용한 것과 동일한 의미를 갖는다.

<a id="fe7851d3ac21e575"></a>
##### &lt;cluster domain name&gt;

&lt;cluster domain name&gt;에 정의된 예약어는 다음과 같은 의미를 가진다.

- GLOBAL
    - 모든 cluster group을 cluster domain으로 선정한다.
- LOCAL
    - 사용자 질의를 수행하는 server만 cluster domain으로 선정한다.
- LOCAL_OFFLINE
    - Domain을 적용할 table이 offline 상태인 경우 사용자 질의를 수행하는 server만 cluster domain으로 선정한다.
    - Online table에 LOCAL_OFFLINE domain을 기술하면 에러가 발생한다.

&lt;cluster domain name&gt;에 &lt;identifier&gt;를 기술한 경우 해당 이름의 cluster group 또는 cluster member를 [Cluster Domain](12-sql-languages.md#acd447d9e42057b7)으로 선정한다.

<a id="3a62d1255adbd62a"></a>
#### 사용 예

다음은 &lt;table name&gt;을 이용하여 단일 table을 검색하는 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, c_nation FROM customer;

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

5 rows selected.
```

다음은 &lt;derived table&gt;을 이용하는 SELECT 구문의 예이다.

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer);

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

5 rows selected.


gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer) AS CUST ("CUSTOMER_NAME", "CUSTOMER_NATION");

CUSTOMER_NAME CUSTOMER_NATION
------------- ---------------
Customer#1    KOREA          
Customer#2    CANADA         
Customer#3    KOREA          
Customer#4    GERMANY        
Customer#5    UNITED STATES  

5 rows selected.
```

다음은 괄호를 이용한 joined table에 대한 SELECT 구문의 예이다.

```
gSQL> SELECT customer.c_name, o_totalprice FROM (customer INNER JOIN orders ON customer.c_custkey = orders.o_custkey);

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#2     46929.18
Customer#4    193846.25
Customer#3     32151.78
Customer#5     144659.2

5 rows selected.
```

다음은 콤마 (,)로 구분한 두 개의 table들을 사용하는 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, o_totalprice FROM customer, orders;

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#1     46929.18
Customer#1    193846.25
Customer#1     32151.78
Customer#1     144659.2
Customer#2    173665.47
Customer#2     46929.18
Customer#2    193846.25
Customer#2     32151.78
Customer#2     144659.2
Customer#3    173665.47
Customer#3     46929.18
Customer#3    193846.25
Customer#3     32151.78
Customer#3     144659.2
Customer#4    173665.47
Customer#4     46929.18
Customer#4    193846.25
Customer#4     32151.78
Customer#4     144659.2

C_NAME     O_TOTALPRICE
---------- ------------
Customer#5    173665.47
Customer#5     46929.18
Customer#5    193846.25
Customer#5     32151.78
Customer#5     144659.2

25 rows selected.
```

다음은 &lt;cluster domain&gt;을 이용하는 SELECT 구문의 예이다.

- GLOBAL 예약어 사용

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer@GLOBAL);

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

5 rows selected.
```

- LOCAL 예약어 사용

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer)@LOCAL;

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA

2 rows selected.
```

- G1이라는 이름의 cluster group name을 사용

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer@G1);

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA

2 rows selected.
```

- G2N1이라는 이름의 cluster member name을 사용

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer@G2N1);

C_NAME     C_NATION
---------- -------------
Customer#3 KOREA
Customer#4 GERMANY

2 rows selected.
```

<a id="1e9be2586ce3f12e"></a>
#### 호환성

SQL 표준은 GOLDILOCKS와 비교하여 다음과 같은 차이가 있다.

- &lt;table factor&gt;에서 &lt;sample clause&gt;를 지원한다.
- &lt;table primary&gt;에서 &lt;lateral derived table&gt;, &lt;collection derived table&gt;, &lt;table function derived table&gt;, &lt;only spec&gt;, &lt;data change delta table&gt;를 지원한다.
    - &lt;lateral derived table&gt;은 &lt;from clause&gt;로 하여금 &lt;lateral derived table&gt;의 subquery 내에서 해당 구문의 왼쪽 테이블들을 참조할 수 있게 한다. (예: select * from dual a, (select * from dual b where a.dummy = b.dummy);)
    - &lt;only spec&gt;은 &lt;from clause&gt;의 hierarchy에 의한 view가 subview의 결과를 포함하지 않도록 한다.
- &lt;table primary&gt;에서 system-versioned table을 지원한다.
- &lt;table primary&gt;에서 &lt;derived column list&gt;를 지원한다.
- &lt;table primary&gt;에서 &lt;transition table name&gt;과 &lt;query name&gt;을 지원한다.
- &lt;derived table&gt;에 대해 &lt;correlation name&gt;이 반드시 존재해야 한다.

<a id="cb415bb08b75752a"></a>
#### 참조

관련 내용은 [subquery](#5ddb0216f95db4a6)를 참조한다.

<a id="084d9757859ddaed"></a>
### joined table

<a id="c37a4fc2dac4fd28"></a>
#### 기능

Cartesian product, inner join, outer join 등에서 파생되는 table을 기술한다.

<a id="a371292091b14a02"></a>
#### 구문

```
<joined table> ::=
      <cross join>
    | <qualified join>
    | <natural join>

<cross join> ::=
    <table reference> CROSS JOIN <table factor>

<qualified join> ::=
    <table reference> [ <join type> ] JOIN <table reference> <join specification>

<natural join> ::=
    <table reference> NATURAL [ <join type> ] JOIN <table factor>

<join specification> ::=
      <join condition>
    | <named columns join>

<join condition> ::=
    ON <search condition>

<named columns join> ::=
    USING ( <join column list> )

<join type> ::=
      INNER
    | { LEFT | RIGHT | FULL } [ OUTER ]

<join column list> ::=
    <column name list>
```

<a id="deb4417aa47682a4"></a>
#### 사용 범위 및 접근 권한

Joined table에 기술된 모든 table 및 view에 대한 접근 권한이 있어야 한다.

<a id="930ed8e8e7f01fe4"></a>
#### 구문 규칙 및 파라미터

<a id="bdac81cd7d0c9690"></a>
##### &lt;cross join&gt;

&lt;join specification&gt;은 &lt;cross join&gt; 위치에 오지 않으며, &lt;cross join&gt;의 오른쪽에는 단일 테이블이나 &lt;table subquery&gt;, 괄호로 묶은 &lt;joined table&gt;이 올 수 있다.

<a id="df560e7ec83c8ebb"></a>
##### &lt;qualified join&gt;

- &lt;join specification&gt;을 반드시 기술해야 한다.
- &lt;join type&gt;은 생략할 수 있는데 생략할 경우 INNER로 처리한다.
- &lt;join type&gt;에서 OUTER는 생략할 수 있다.
- &lt;join type&gt;이 OUTER JOIN인 경우 &lt;join specification&gt;에는 &lt;join condition&gt;만 올 수 있다. (&lt;named columns join&gt;이 오는 경우 에러가 발생한다.)

<a id="e860137a7ab8e7ba"></a>
##### &lt;natural join&gt;

- &lt;join specification&gt;이 오지 않으며, 오른쪽에는 단일 테이블이나 &lt;table subquery&gt;, 괄호로 묶은 &lt;joined table&gt;이 올 수 있다.
- &lt;join type&gt;은 생략할 수 있는데 생략할 경우 INNER로 처리한다.
- &lt;join type&gt;에 OUTER를 지원하지 않는다.
- NATURAL JOIN의 왼쪽 row와 오른쪽 row에 동일한 &lt;column name&gt;이 하나도 없는 경우 &lt;cross join&gt;으로 처리한다.
- NATURAL JOIN의 왼쪽 row와 오른쪽 row에 동일한 &lt;column name&gt;이 있을 경우, USING 구문을 기술한 것과 동일하게 동작한다.
- 대응되는 두 column에 대한 비교 연산이 없으면 에러가 발생한다.

<a id="784eaa2f7eee3cf8"></a>
##### &lt;join specification&gt;

- &lt;join condition&gt;이나 &lt;named columns join&gt; 중에 하나만 기술할 수 있다.
- &lt;named columns join&gt;을 기술한 경우
    - &lt;join column list&gt;에는 반드시 하나 이상의 column name을 기술해야 한다.
    - Column name은 &lt;table name&gt;.&lt;column name&gt;과 같이 기술할 수 없다.
    - &lt;join column list&gt;에 나열된 column들은 JOIN의 왼쪽 row와 오른쪽 row에 반드시 존재해야 하며, 비교 가능해야 한다.
    - &lt;select list&gt;에 *를 사용한 경우 &lt;join column list&gt;에 나열된 column들의 display column name이 해당 column name으로 출력되며, JOIN의 왼쪽 row와 오른쪽 row에서 해당 column은 제외된다.
    - &lt;select list&gt;에 *를 사용한 경우 target은 &lt;join column list&gt;에 기술된 column들, 왼쪽 row들 중에서 &lt;join column list&gt;에 해당되지 않는 column들, 오른쪽 row들 중에서 &lt;join column list&gt;에 해당되지 않는 column들의 순서로 출력된다.
    - 해당 JOIN 구문의 &lt;join column list&gt;에 기술된 column들 중에 왼쪽 row나 오른쪽 row에 해당하는 column은 참조할 수 없다. (즉, &lt;join column list&gt;에 기술된 &lt;column name&gt;은 &lt;table name&gt;.&lt;column name&gt;과 같이 참조할 수 없고, &lt;column name&gt;으로만 참조할 수 있다.)
    - &lt;join column list&gt;에 나열된 column들을 조인 조건으로 처리할 때 각 &lt;column name&gt;에 대하여 &lt;left table name&gt;.&lt;column name&gt; = &lt;right table name&gt;.&lt;column name&gt; 조건이 생성되고 각 &lt;column name&gt;에 대한 조건들을 AND로 처리하는 조건이 생성된다.
    - &lt;select list&gt;에 특정 테이블의 모든 row를 반환하는 '&lt;table name&gt;.*' 구문을 사용할 수 없다.
    - 대응하는 두 column에 대한 비교 연산이 없으면 에러가 발생한다.

<a id="ce3ab55dc4fc6142"></a>
#### 설명

<a id="98b2a6dd475877b7"></a>
##### &lt;cross join&gt;

&lt;cross join&gt;은 왼쪽의 각 row를 오른쪽의 모든 row들과 결합한 결과를 반환한다.

&lt;cross join&gt;에는 join 조건을 명시적으로 기술할 수 없지만, &lt;where clause&gt;를 통해 두 table에 대한 join 조건을 기술할 수 있으며, 이 경우 inner join과 동일하게 동작한다.

<a id="b64759a431f368aa"></a>
##### &lt;qualified join&gt;

&lt;qualified join&gt;은 왼쪽의 각 row들을 오른쪽의 모든 row들과 결합한 후 join 조건을 만족하는 row들만 결과로 반환한다. &lt;where clause&gt;가 존재하면 join 구문을 수행할 때 join 조건을 적용한 결과 row들에 &lt;where clause&gt;의 조건들을 적용한다.

Inner join은 &lt;where clause&gt;에 존재하는 조건들을 join 조건처럼 처리해도 결과가 동일하지만, outer join은 &lt;where clause&gt;에 존재하는 조건들을 join 조건처럼 처리하면 결과가 달라지게 된다.

Left outer join은 왼쪽 row에 대하여 join 조건을 만족하는 오른쪽 row가 있을 경우, 해당 row들을 결합한 row를 결과로 반환하며, join 조건을 만족하는 오른쪽 row가 존재하지 않을 경우 왼쪽 row의 값은 그대로 유지하고 오른쪽 row의 값은 모두 NULL로 채운 row를 결과로 반환한다.

Right outer join은 left outer join과 정확히 반대로 동작한다.

Full outer join은 left outer join의 결과와 함께 join 조건을 만족하지 않는 모든 오른쪽 row에 왼쪽 row의 값을 NULL로 채운 row들을 결과로 반환한다.

<a id="15fc7907351e234a"></a>
##### &lt;natural join&gt;

&lt;natural join&gt;은 join에 참여하는 두 table에서 동일한 이름을 갖는 모든 column들을 각각 equal 조건으로 join 한다. 즉, join에 참여하는 두 table에서 동일한 이름을 갖는 모든 column들을 inner join에서 USING 구문에 기술한 것과 동일하다.

<a id="ba840f3f62f353ed"></a>
##### &lt;join specification&gt;

&lt;join condition&gt;은 join 구문의 왼쪽 row와 오른쪽 row를 조인할 조건을 기술하며, &lt;named columns join&gt;은 왼쪽 row와 오른쪽 row에 대해 동일한 &lt;column name&gt;이 존재하는 경우 이를 나열하여 조인 조건을 기술한다.

<a id="e987aa96bab4ad3d"></a>
#### 사용 예

다음은 &lt;cross join&gt;을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, o_totalprice FROM customer CROSS JOIN orders;

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#1     46929.18
Customer#1    193846.25
Customer#1     32151.78
Customer#1     144659.2
Customer#2    173665.47
Customer#2     46929.18
Customer#2    193846.25
Customer#2     32151.78
Customer#2     144659.2
Customer#3    173665.47
Customer#3     46929.18
Customer#3    193846.25
Customer#3     32151.78
Customer#3     144659.2
Customer#4    173665.47
Customer#4     46929.18
Customer#4    193846.25
Customer#4     32151.78
Customer#4     144659.2

C_NAME     O_TOTALPRICE
---------- ------------
Customer#5    173665.47
Customer#5     46929.18
Customer#5    193846.25
Customer#5     32151.78
Customer#5     144659.2

25 rows selected.
```

다음은 inner join을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, o_totalprice FROM customer INNER JOIN orders ON c_custkey = o_custkey;

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#2     46929.18
Customer#4    193846.25
Customer#3     32151.78
Customer#5     144659.2

5 rows selected.
```

다음은 outer join을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, o_totalprice FROM customer LEFT OUTER JOIN orders ON c_custkey = o_custkey AND o_orderdate < '1996-01-01';

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1         null
Customer#2         null
Customer#3     32151.78
Customer#4    193846.25
Customer#5     144659.2

5 rows selected.

gSQL> SELECT c_name, o_totalprice FROM customer RIGHT OUTER JOIN orders ON c_custkey = o_custkey AND c_nation = 'KOREA';

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
null           46929.18
null          193846.25
Customer#3     32151.78
null           144659.2

5 rows selected.

gSQL> SELECT c_name, o_totalprice FROM customer FULL OUTER JOIN orders ON c_custkey = o_custkey AND c_nation = 'KOREA' AND o_orderdate < '1996-01-01';

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1         null
Customer#2         null
Customer#3     32151.78
Customer#4         null
Customer#5         null
null          173665.47
null           46929.18
null          193846.25
null           144659.2

9 rows selected.
```

다음은 natural join을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, o_totalprice FROM (SELECT c_custkey custkey, c_name FROM customer) NATURAL JOIN (SELECT o_custkey custkey, o_totalprice FROM orders);

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#2     46929.18
Customer#4    193846.25
Customer#3     32151.78
Customer#5     144659.2

5 rows selected.
```

<a id="aecd452767515d05"></a>
#### 호환성

SQL 표준은 GOLDILOCKS와 비교하여 다음과 같은 차이가 있다.

- &lt;qualified join&gt;과 &lt;natural join&gt;에 대하여 &lt;partitioned join table&gt;을 지원한다.
- Outer join에 대하여 USING 구문을 지원한다.
- &lt;natural join&gt;의 &lt;join type&gt;으로 outer join에 대한 type을 지원한다.
- &lt;join condition&gt;에 &lt;set function specification&gt;을 지원한다.

**SQL 표준 호환성**

<a id="205ae8878471faec"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F401 | Extended joined table | O |
| F402 | Named column joins for LOBs, arrays, and multisets | X |
| F403 | Partitioned join tables | X |

<a id="64591413ca4346c2"></a>
#### 참조

관련 내용은 [from clause](#43529f212b19c0e0)를 참조한다.

<a id="8ffd103d5116485d"></a>
### where clause

<a id="47fbc2e20ee626ee"></a>
#### 기능

&lt;from clause&gt; 결과에 &lt;search condition&gt;을 적용한다.

<a id="36c9471d6fd2085b"></a>
#### 구문

```
<where clause> ::=
    WHERE <search condition>
```

<a id="f65a1512a3a1234a"></a>
#### 구문 규칙 및 파라미터

<a id="c6841c6f95d23174"></a>
##### &lt;where clause&gt;

WHERE 키워드 뒤에는 boolean type을 반환하는 &lt;search condition&gt;이 와야 한다.

<a id="bca34dc68b1cbd45"></a>
#### 설명

&lt;where clause&gt;에 대한 자세한 내용은 [Conditions](11-sql-elements.md#4900f8e290fa6cb1)를 참조한다.

<a id="b2783e48c9aef9a7"></a>
#### 사용 예

다음은 &lt;where clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT s_name, s_nation FROM supplier WHERE s_nation = 'KOREA';

S_NAME                    S_NATION
------------------------- --------
Supplier#2                KOREA

1 row selected.

gSQL> SELECT s_name, ps_availqty, ps_supplycost FROM supplier, partsupp WHERE s_nation = 'KOREA' AND s_suppkey = ps_suppkey;

S_NAME                    PS_AVAILQTY PS_SUPPLYCOST
------------------------- ----------- -------------
Supplier#2                       8076        993.49
Supplier#2                       4069        357.84

2 rows selected.
```

<a id="0d30d692873f1f09"></a>
#### 호환성

**SQL 표준 호환성**

<a id="cfc9a8c3f87747a6"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F441 | Extended set function support | O |

<a id="7306cdb9fd458d19"></a>
#### 참조

관련 내용은 [query specification](#d8630e2bdbb32181)을 참조한다.

<a id="a73fcd9d4ff882ea"></a>
### group by clause

<a id="332f75488ef3f539"></a>
#### 기능

이전 구문들이 처리한 결과에 &lt;group by clause&gt;를 적용한 grouped table을 기술한다.

<a id="57d0707f87b78529"></a>
#### 구문

```
<group by clause> ::=
    GROUP BY <grouping element list>

<grouping element list> ::=
    <grouping element> [ { , <grouping element> } ... ]

<grouping element> ::=
      <ordinary grouping set>
    | <empty grouping set>

<ordinary grouping set> ::=
      <grouping column reference>

<grouping column reference> ::=
    <column reference>
    | <value_expression>

<empty grouping set> ::=
    <left paren> <right paren>
```

<a id="8cef17c17517d180"></a>
#### 사용 범위 및 접근 권한

&lt;group by clause&gt;를 수행하기 위해 별도의 접근 권한이 필요한 것은 아니다.

<a id="d75ec53a257ed7d5"></a>
#### 구문 규칙 및 파라미터

<a id="212015ab92fa574f"></a>
##### &lt;ordinary grouping set&gt;

하나 이상의 &lt;grouping column reference&gt;로 구성한다.  
LONG type은 지원하지 않는다.

<a id="da6574563249ab5f"></a>
##### &lt;empty grouping set&gt;

괄호만 사용하여 기술할 수 있으며, 괄호 안에는 어떠한 expression도 쓸 수 없다.

<a id="6e59b6409f300e0e"></a>
#### 설명

<a id="78f52203ba870da3"></a>
##### &lt;grouping element list&gt;

&lt;group by clause&gt;에 기술된 &lt;grouping element&gt;를 순서대로 결합하여 하나의 GROUPING SET로 만드는 grouping을 수행한다. 이 때 GROUPING SET에 존재하는 모든 &lt;grouping element&gt;들의 값이 순서대로 일치하는 group은 동일한 group으로 처리한다.

&lt;group by clause&gt;가 기술된 경우, &lt;select list&gt;에는 &lt;group by clause&gt;에 기술된 column이나 &lt;group by clause&gt;에 기술되어 있지 않는 column 중에 집계 함수에 사용되는 column만 올 수 있다.

<a id="372f00d5290f28e0"></a>
##### &lt;grouping column reference&gt;

&lt;grouping column reference&gt;에는 &lt;column reference&gt;나 &lt;value expression&gt;이 올 수 있다.

&lt;column reference&gt;는 &lt;query specification&gt;의 &lt;from clause&gt;에 속하는 column들만 참조할 수 있으며, 동일한 column 이름이 존재하는 경우 table 이름 등을 사용하여 column 이름을 명확하게 기술하여야 한다.

&lt;value expression&gt;은 &lt;column reference&gt;를 포함한 expression이나 &lt;column reference&gt;를 포함하지 않는 expression으로 구성될 수 있다. 전자의 경우 &lt;column reference&gt;를 사용하여 여러 group으로 구분할 수 있지만, 후자의 경우 &lt;value expression&gt;의 값이 모두 동일한 상수값이기 때문에 모든 레코드가 단일 group으로 구성된다.

&lt;value expression&gt;에 null 값을 기술하는 경우, null 값들은 동일한 값으로 취급되어 모든 레코드가 단일 group으로 구성된다.

<a id="0b6a600c0475cece"></a>
##### &lt;empty grouping set&gt;

&lt;empty grouping set&gt;는 grouping 대상 column이 존재하지 않는다는 의미이다. 따라서, 모든 레코드가 단일 group으로 구성된다.

<a id="8036d89271417ebe"></a>
#### 사용 예

다음은 GROUP BY를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_nation, COUNT(c_name) FROM customer GROUP BY c_nation;

C_NATION      COUNT(C_NAME)
------------- -------------
UNITED STATES             1
CANADA                    1
KOREA                     2
GERMANY                   1

4 rows selected.

gSQL> SELECT COUNT(c_name) FROM customer GROUP BY NULL;

COUNT(C_NAME)
-------------
            5

1 row selected.

gSQL> SELECT COUNT(c_name) FROM customer GROUP BY ();

COUNT(C_NAME)
-------------
            5

1 row selected.
```

<a id="68a6810b3a5c1081"></a>
#### 호환성

**SQL 표준 호환성**

<a id="98d0b05da8db581d"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T431 | Extended grouping capabilities | X |
| T432 | Nested and concatenated GROUPING SETS | X |
| T434 | GROUP BY DISTINCT | X |

<a id="918cd90bacda3458"></a>
#### 참조

관련 내용은 다음을 참조한다.

- [having clause](#d406655ebf1a0fb1)
- [query specification](#d8630e2bdbb32181)

<a id="d406655ebf1a0fb1"></a>
### having clause

<a id="89f8f2e5b75657f9"></a>
#### 기능

&lt;search condition&gt;을 만족하지 않는 group을 제거한 grouped table을 기술한다.

<a id="5c8f46f0632dff23"></a>
#### 구문

```
<having clause> ::=
    HAVING <search condition>
```

<a id="11e059f4bd632a89"></a>
#### 사용 범위 및 접근 권한

&lt;having clause&gt;를 수행하기 위해 별도의 접근 권한이 필요한 것은 아니다.

<a id="be891c318a0806e1"></a>
#### 구문 규칙 및 파라미터

<a id="abe2f63444ee8518"></a>
##### &lt;having clause&gt;

&lt;group by clause&gt;에 기술된 column만 &lt;search condition&gt;에 집계 함수 없이 사용할 수 있다.  
&lt;group by clause&gt;에 기술되지 않은 column은 집계 함수를 사용하여 기술할 수 있다.

<a id="44e965f6002c159e"></a>
#### 설명

<a id="dd3475f1084956fd"></a>
##### &lt;having clause&gt;

&lt;having clause&gt;는 grouping된 데이터들에 대한 검색 조건을 기술한다. 일반적으로 &lt;group by clause&gt;와 같이 사용되며, &lt;group by clause&gt; 없이 &lt;having clause&gt;를 사용할 경우, "GROUP BY ()"가 있는 것으로 간주한다.

&lt;having clause&gt;에는 &lt;group by clause&gt;에 기술된 column만 단독으로 기술할 수 있다. 이 외의 column을 단독으로 기술하려면 집계 함수를 사용해야 한다.

<a id="c75953fd27b48549"></a>
#### 사용 예

다음은 &lt;having clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_nation, COUNT(c_name) FROM customer GROUP BY c_nation HAVING COUNT(c_name) > 1;

C_NATION COUNT(C_NAME)
-------- -------------
KOREA                2

1 row selected.

gSQL> SELECT COUNT(c_name) FROM customer HAVING COUNT(c_name) > 1;

COUNT(C_NAME)
-------------
            5

1 row selected.
```

<a id="917496ddc9e4f580"></a>
#### 호환성

**SQL 표준 호환성**

<a id="e14f6fdcbab61fe2"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T301 | Functional dependencies | O |

<a id="8df567236f174364"></a>
#### 참조

관련 내용은 다음을 참조한다.

- [group by clause](#a73fcd9d4ff882ea)
- [Conditions](11-sql-elements.md#4900f8e290fa6cb1)

<a id="39da5d5114d359af"></a>
### order by clause

<a id="899577b3f7cbd860"></a>
#### 기능

검색 결과의 정렬 순서를 기술한다.

<a id="c44daaebd655c867"></a>
#### 구문

```
<order by clause> ::=
    ORDER BY <sort specification list>

<sort specification list> ::=
    <sort specification> [ { <comma> <sort specification> }... ]

<sort specification> ::=
    <sort key> [ <ordering specification> ] [ <null ordering> ]

<sort key> ::=
    <value expression>

<ordering specification> ::=
      ASC
    | DESC

<null ordering> ::=
      NULLS FIRST
    | NULLS LAST
```

<a id="cd35b1a7aec6e098"></a>
#### 사용 범위 및 접근 권한

정렬을 위해 기술한 sort key에 column이 존재하는 경우 사용자에게 column에 대한 접근 권한이 있어야 한다.

<a id="3f35221d239bc237"></a>
#### 구문 규칙 및 파라미터

<a id="49833116258a3f2c"></a>
##### &lt;order by clause&gt;

- &lt;query specification&gt;의 &lt;select list&gt;에 사용되지 않은 column을 &lt;sort key&gt;로 사용하는 경우, &lt;set quantifier&gt; DISTINCT나 하나 이상의 &lt;set function specification&gt;을 기술할 수 없다.
- 단, 다음과 같은 경우에는 DISTINCT 구문이 기술되었어도 생략할 수 있기 때문에 위의 제약 사항이 적용되지 않는다.
    - &lt;group by clause&gt;나 &lt;having clause&gt;가 기술되지 않았으며, 하나 이상의 &lt;set function specification&gt;을 기술한 경우
    - 하나 이상의 중첩된 &lt;set function specification&gt;를 기술한 경우
- &lt;set operator&gt; 구문에서 &lt;order by clause&gt;를 명시한 경우, 가장 먼저 기술된 &lt;query specification&gt;를 기준으로 &lt;sort key&gt;를 분석한다.

<a id="d3b56244a697a37a"></a>
##### &lt;sort specification list&gt;

&lt;ordering specification&gt;을 명시하지 않은 경우, 기본값은 ASC이다.  
&lt;null ordering&gt;을 명시하지 않은 경우, 기본값은 NULLS LAST이다.

<a id="28a1777973e117c6"></a>
##### &lt;sort key&gt;

- &lt;sort key&gt;의 &lt;value expression&gt;이 scale 0의 양의 정수값이면 그 값을 sort key index로 사용한다.
    - 해당 값에 대응되는 &lt;query specification&gt;의 i 번째 &lt;select sublist&gt;를 sort key로 사용한다.
    - 해당 값에 대응되는 &lt;query specification&gt;의 i 번째 &lt;select sublist&gt;가 존재하지 않는 경우 error를 반환한다.
- Row subquery나 relation subquery는 &lt;value expression&gt;로 지원되지 않는다.
- 그 외의 &lt;value expression&gt;은 sort key로 사용된다.

<a id="3e436bab0d97a02b"></a>
#### 설명

<a id="c3a831b64459a0a7"></a>
##### &lt;order by clause&gt;

&lt;order by clause&gt;는 검색 결과를 정렬하기 위한 방법을 기술한다. &lt;order by clause&gt;에는 &lt;sort key&gt;들을 콤마 (,) 리스트로 나열할 수 있으며, 나열한 순서대로 각 레코드들의 &lt;sort key&gt;를 비교하여 순서대로 정렬한다.

&lt;sort key&gt;에는 오름차순 정렬이나 내림차순 정렬을 지정하는 &lt;ordering specification&gt;을 기술할 수 있는데 생략할 경우에는 오름차순으로 정렬된다. 또한 &lt;sort key&gt;에는 NULL 값과 NULL이 아닌 값의 순서를 &lt;null ordering&gt;을 사용하여 지정할 수 있는데 생략할 경우에는 NULLS LAST로 정렬된다.

&lt;sort key&gt;에 상수값을 기술할 경우 &lt;select list&gt;에서 해당 값의 순번에 위치한 expression을 &lt;sort key&gt;로 간주한다. 그리고 이 때 기술하는 상수값은 0보다 크면서 &lt;select list&gt;에 기술한 expression의 전체 개수와 같거나 작아야 하고 scale은 0이어야 하다.

&lt;sort key&gt;에는 LONG type을 기술할 수 없다.

<a id="a88969c4a223e839"></a>
##### Null value와의 비교

- Null value끼리 비교할 경우에는 동일한 값으로 간주한다.
- Null value와 null value가 아닌 값을 비교할 경우에는 다음 규칙을 따른다.
    - NULLS FIRST이고 ASC인 경우: null value < not null value
    - NULLS LAST이고 ASC인 경우: null value > not null value
    - NULLS FIRST이고 DESC인 경우: null value > not null value
    - NULLS LAST이고 DESC인 경우: null value < not null value
- Null value 비교 결과가 UNKNOWN인 경우, 탐색 순서에 따라 정렬한다.

<a id="50bff23436e15994"></a>
##### 동일한 sort key 값을 가지는 row들의 정렬

Sort key로 구분할 수 없는 row들을 peer라고 하며, peer들은 탐색 순서에 따라 정렬된다.

<a id="ed34bde83b4c3c1b"></a>
##### &lt;sort key&gt;로 사용되는 &lt;aggregation function&gt;

&lt;query specification&gt;에서 &lt;aggregation function&gt;이 사용되거나 &lt;group by clause&gt;가 기술된 경우, &lt;aggregation function&gt;을 &lt;sort key&gt;로 사용할 수 있다. 단, &lt;group by clause&gt;가 기술된 경우에만 중첩된 &lt;aggregation function&gt;을 &lt;sort key&gt;로 사용할 수 있다.

<a id="d6c9cec1f04ebf73"></a>
#### 사용 예

다음은 ORDER BY를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, c_nation FROM customer ORDER BY c_nation;

C_NAME     C_NATION
---------- -------------
Customer#2 CANADA
Customer#4 GERMANY
Customer#1 KOREA
Customer#3 KOREA
Customer#5 UNITED STATES

5 rows selected.

gSQL> SELECT c_name, c_nation FROM customer ORDER BY c_nation DESC;

C_NAME     C_NATION
---------- -------------
Customer#5 UNITED STATES
Customer#1 KOREA
Customer#3 KOREA
Customer#4 GERMANY
Customer#2 CANADA

5 rows selected.

gSQL> SELECT c_name, c_nation FROM customer ORDER BY 2 DESC;

C_NAME     C_NATION     
---------- -------------
Customer#5 UNITED STATES
Customer#1 KOREA        
Customer#3 KOREA        
Customer#4 GERMANY      
Customer#2 CANADA       

5 rows selected.
```

<a id="65684898b69f952b"></a>
#### 호환성

&lt;order by clause&gt;는 SQL 표준과 비교하여 다음과 같은 차이가 있다.

- SQL 표준은 &lt;sort key&gt;의 &lt;value expression&gt;로 &lt;column reference&gt;만 지원한다.
- SQL 표준은 &lt;sort key&gt;의 &lt;value expression&gt;을 sort key index로 사용하지 않는다.

**SQL 표준 호환성**

<a id="97bcb948b5d81853"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F850 | Top-level &lt;order by clause&gt; in &lt;query expression&gt; | X |
| F851 | &lt;order by clause&gt; in subqueries | O |
| F852 | Top-level &lt;order by clause&gt; in views | O |
| F855 | Nested &lt;order by clause&gt; in &lt;query expression&gt; | O |

<a id="77f46dc423011dd9"></a>
#### 참조

관련 내용은 [query expression](#1c4140d8d3200490)을 참조한다.

<a id="37f82ae17691b17d"></a>
### offset limit clause

<a id="20834d25e2a00e2f"></a>
#### 기능

검색 결과 중 skip 할 row의 개수와 fetch 할 row의 개수를 기술한다.

<a id="c8f5a0c736f87d4f"></a>
#### 구문

```
<offset limit clause> ::=
      <result offset clause>
    | <fetch limit clause>
    | <result offset clause> <fetch limit clause>

<result offset clause> ::=
    OFFSET <offset row count> [ { ROW | ROWS } ]

<fetch limit clause> ::=
      <fetch first clause>
    | <limit clause>

<fetch first clause> ::=
    FETCH [ FIRST | NEXT ] [ <fetch row count> ] [ ROW ONLY | ROWS ONLY ]

<limit clause> ::=
    LIMIT { <fetch row count> | <offset row count> , <fetch row count> | ALL }
```

<a id="df73da1061ee434c"></a>
#### 사용 범위 및 접근 권한

&lt;offset limit clause&gt;는 접근 권한을 필요로 하지 않는다.

<a id="a4f6e3f2e19b1c55"></a>
#### 구문 규칙 및 파라미터

<a id="0689e0f6cda4a513"></a>
##### &lt;result offset clause&gt;

- &lt;offset row count&gt; 값은 0과 같거나 큰 양의 정수이어야 한다.
- ROW와 ROWS는 동일한 의미의 키워드로 생략 가능하다.
- 구문을 생략할 경우 OFFSET 0 ROWS 라는 의미이다.

<a id="049162fe8834c0e8"></a>
##### &lt;fetch limit clause&gt;

- 검색 결과 중 skip 할 row의 개수를 명시한다.
- 구문을 생략할 경우 LIMIT ALL 이라는 의미이다.

<a id="5bc4649717039d2f"></a>
##### &lt;fetch first clause&gt;

- Fetch 할 row의 개수를 명시한다.
- &lt;limit clause&gt;와 함께 사용할 수 없다.
- FIRST와 NEXT는 동일한 의미의 키워드로 생략 가능하다.
- &lt;fetch row count&gt; 값은 0 보다 큰 양의 정수이어야 한다.
- ROW ONLY와 ROWS ONLY는 동일한 의미의 키워드로 생략 가능하다.
- &lt;fetch row count&gt;는 생략 가능하며 생략할 경우 그 값은 1이다.

<a id="7e039c5707f8a97b"></a>
##### &lt;limit clause&gt;

- Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너 뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
- &lt;fetch first clause&gt;와 함께 사용할 수 없다.
- LIMIT &lt;fetch row count&gt;로 사용한 경우
    - &lt;fetch row count&gt;는 0보다 큰 양의 정수이어야 한다.
    - 이 구문은 FETCH FIRST &lt;fetch row count&gt; ROWS ONLY와 동일한 의미이다.
- LIMIT &lt;offset row count&gt;, &lt;fetch row count&gt;로 사용한 경우
    - &lt;result offset clause&gt;와 동시에 사용할 수 없다.
    - &lt;offset row count&gt;는 0과 같거나 큰 양의 정수이어야 한다.
    - &lt;fetch row count&gt;는 0보다 큰 양의 정수이어야 한다.
    - 이 구문은 OFFSET &lt;offset row count&gt; ROWS FETCH FIRST &lt;fetch row count&gt; ROWS ONLY와 동일한 의미이다.
- LIMIT ALL로 사용한 경우 fetch 할 row의 개수에 제한이 없다.

<a id="67ff78de06a12f61"></a>
#### 설명

<a id="f3b71a49c8ee61c0"></a>
##### &lt;result offset clause&gt;

검색한 결과 중 &lt;offset row count&gt; 번째의 row부터 사용자에게 보낸다. 만약 &lt;offset row count&gt;가 검색한 결과 row의 개수와 같거나 크면 사용자에게 보내지는 결과의 개수는 0이다.

<a id="2d7ac54630911023"></a>
##### &lt;fetch first clause&gt;

검색한 결과 중에 &lt;fetch row count&gt; 개수만큼만 사용자에게 반환한다.

<a id="c1dc52bf5756c7c1"></a>
##### &lt;limit clause&gt;

LIMIT &lt;fetch_row_count&gt;로 사용된 경우 검색한 결과 중 &lt;fetch row count&gt; 개수만큼만 사용자에게 반환한다.

LIMIT &lt;offset row count&gt;, &lt;fetch row count&gt;로 사용한 경우, 검색한 결과 중 &lt;offset row count&gt; 번째의 row부터 &lt;fetch row count&gt; 개수만큼만 사용자에게 반환한다.

LIMIT ALL로 사용한 경우 개수 제한없이 검색한 결과를 사용자에게 반환한다.

<a id="88e796e8c1020faa"></a>
#### 사용 예

다음은 &lt;result offset clause&gt;을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, c_nation FROM customer OFFSET 1;

C_NAME     C_NATION
---------- -------------
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

4 rows selected.
```

다음은 &lt;fetch first clause&gt;을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, c_nation FROM customer FETCH FIRST ROW ONLY;

C_NAME     C_NATION
---------- --------
Customer#1 KOREA

1 row selected.

gSQL> SELECT c_name, c_nation FROM customer FETCH FIRST 2 ROW ONLY;

C_NAME     C_NATION
---------- --------
Customer#1 KOREA
Customer#2 CANADA

2 rows selected.
```

다음은 &lt;limit clause&gt;을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, c_nation FROM customer LIMIT 1;

C_NAME     C_NATION
---------- --------
Customer#1 KOREA

1 row selected.

gSQL> SELECT c_name, c_nation FROM customer LIMIT 1, 2;

C_NAME     C_NATION
---------- --------
Customer#2 CANADA
Customer#3 KOREA

2 rows selected.

gSQL> SELECT c_name, c_nation FROM customer LIMIT ALL;

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

5 rows selected.
```

다음은 &lt;result offset clause&gt;와 &lt;fetch limit clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, c_nation FROM customer OFFSET 1 FETCH 2;

C_NAME     C_NATION
---------- --------
Customer#2 CANADA
Customer#3 KOREA

2 rows selected.

gSQL> SELECT c_name, c_nation FROM customer OFFSET 1 LIMIT 2;

C_NAME     C_NATION
---------- --------
Customer#2 CANADA
Customer#3 KOREA

2 rows selected.
```

<a id="18bffd30fae3e2c8"></a>
#### 호환성

SQL 표준은 GOLDILOCKS와 비교하여 다음과 같은 차이가 있다.

- ROW나 ROWS를 생략할 수 없다.
- FIRST나 NEXT를 생략할 수 없다.
- &lt;fetch first clause&gt;에 &lt;fetch first percentage&gt;를 지원한다.
    - &lt;fetch first percentage&gt;에서 &lt;simple value specification&gt;은 numeric이면 된다. (즉, 소수점 이하도 허용된다.)
    - &lt;fetch first percentage&gt;를 기술한 경우 해당 값을 &lt;fetch row count&gt;로 변환하여 사용하며, 이 때 변환 공식은 다음과 같다.
        - FRC = CEILING ( FFP * LOCT / 100.0E0 )
        - FFP: &lt;simple value specification&gt;의 값
        - LOCT: 검색 결과의 row 개수
        - FRC: &lt;fetch row count&gt;로 변환된 값
- &lt;fetch first clause&gt;에 WITH TIES를 지원한다.
    - WITH TIES를 기술한 &lt;fetch first clause&gt;를 사용한 경우 반드시 &lt;order by clause&gt;가 존재해야 한다.
    - WITH TIES를 기술한 경우 &lt;order by clause&gt;의 sort key가 모두 동일한 row들의 단위인 peers를 기준으로 &lt;fetch row count&gt; 개수 만큼의 peers들을 반환한다.

> OFFSET and LIMIT 구문   
> • SQL 표준은 OFFSET .. FETCH {FIRST|NEXT} ... 구문을 정의하고 있다.   
> • IBM DB2와 Postgres는 SQL 표준과 동일한 구문을 제공한다.   
> • Postgres와 MySQL은 OFFSET .. LIMIT 구문을 제공한다.   
> • Oracle은 ROWNUM column을 통해 유사한 기능을 수행할 수 있다.

**SQL 표준 호환성**

<a id="f6c3cfba8f79631d"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F861 | Top-level &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| F862 | &lt;result offset clause&gt; in subqueries | O |
| F863 | Nested &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| F864 | Top-level &lt;result offset clause&gt; in views | O |
| F865 | dynamic &lt;offset row count&gt; in &lt;result offset clause&gt; | X |

<a id="96acd09fad234c3f"></a>
### set operator

<a id="7d3ae189f285700a"></a>
#### 기능

부질의 (subquery) 결과들에 대한 집합 (set) 연산을 수행한다.

<a id="735c4e06f20a751f"></a>
#### 구문

```
<set operator> ::=
      <set operator term>
    | <query expression body> UNION [ ALL | DISTINCT ] <set operator term>
    | <query expression body> EXCEPT [ ALL | DISTINCT ] <set operator term>
    | <query expression body> MINUS [ ALL | DISTINCT ] <set operator term>

<set operator term> ::=
      <query term>
    | <set operator term> INTERSECT [ ALL | DISTINCT ] <set operator term>
```

<a id="f0bb7be683364962"></a>
#### 사용 범위 및 접근 권한

&lt;set operator&gt; 구문을 사용하려면 각 &lt;set operator term&gt;에 나타나는 &lt;query expression&gt;에 대한 모든 접근 권한이 있어야 한다.

<a id="31e4e0a2040a7d8a"></a>
#### 구문 규칙 및 파라미터

<a id="405347ae0a145dbd"></a>
##### &lt;set operator&gt;

- 부질의 (subquery) 간의 집합 연산을 기술한다.
- 각 부질의 (subquery)의 &lt;select list&gt; target 개수가 모두 동일해야 하며, 매칭되는 target들은 모두 동일한 data type group에 속해야 한다.
- 첫 번째 부질의 (subquery)의 &lt;select list&gt; target 이름이 &lt;set operator&gt; 결과 target의 대표 이름이 된다.
- 괄호 등을 사용하여 명확하게 수행 순서를 기술하지 않을 경우, 왼쪽에 기술한 부질의 (subquery)부터 오른쪽에 기술한 부질의 (subquery) 순서로 평가하여 처리한다.
- &lt;set operator&gt;의 각 operator는 다음을 의미한다.
    - UNION
        - UNION ALL: 부질의 (subquery) 결과들에서 중복을 제거하지 않고 합집합한다.
        - UNION DISTINCT: 부질의 (subquery) 결과들에서 중복을 제거하여 합집합한다.
        - ALL/ DISTINCT 중 하나도 기술하지 않을 경우, DISTINCT를 기술한 것과 동일하게 동작한다.
    - EXCEPT
        - EXCEPT ALL: 부질의 (subquery) 결과들에서 중복을 제거하지 않고 차집합한다.
        - EXCEPT DISTINCT: 부질의(subquery) 결과들에서 중복을 제거하여 차집합한다.
        - ALL/ DISTINCT 중 하나도 기술하지 않을 경우, DISTINCT를 기술한 것과 동일하게 동작한다.
    - MINUS
        - EXCEPT의 alias로써 EXCEPT와 동일하게 동작한다.
    - INTERSECT
        - INTERSECT ALL: 부질의 (subquery) 결과들에서 중복을 제거하지 않고 교집합한다.
        - INTERSECT DISTINCT: 부질의 (subquery) 결과들에서 중복을 제거하여 교집합한다.
        - ALL/ DISTINCT 중 하나도 기술하지 않을 경우, DISTINCT를 기술한 것과 동일하게 동작한다.

<a id="d52caeb1fdf4f942"></a>
##### &lt;query term&gt;

하나의 부질의 (subquery)를 기술한다.  
자세한 내용은 [query expression](#1c4140d8d3200490) 절을 참조한다.

<a id="7f3b4d2a9769f180"></a>
#### 설명

<a id="3852d13fac1f823e"></a>
##### &lt;set operator&gt;의 ALL과 DISTINCT의 차이

예를 들어 R1과 R2 table의 데이터가 다음과 같을 경우, 각 &lt;set operator&gt;의 결과는 다음과 같다.

- TABLE 데이터
    - R1 TABLE = {1, 1, 1, 2, 2, 2, 3, 4, 4, 5}
    - R2 TABLE = {1, 1, 3, 3, 4}
- SELECT * FROM R1 UNION ALL SELECT * FROM R2;
    - result = {1, 1, 1, 1, 1, 2, 2, 2, 3, 3, 3, 4, 4, 4, 5}
- SELECT * FROM R1 UNION DISTINCT SELECT * FROM R2;
    - result = {1, 2, 3, 4, 5}
- SELECT * FROM R1 MINUS ALL SELECT * FROM R2;
    - result = {1, 2, 2, 2, 4, 5}
- SELECT * FROM R1 MINUS DISTINCT SELECT * FROM R2;
    - result = {2, 5}
- SELECT * FROM R1 INTERSECT ALL SELECT * FROM R2;
    - result = {1, 1, 3, 4}
- SELECT * FROM R1 INTERSECT DISTINCT SELECT * FROM R2;
    - result = {1, 3, 4}

<a id="b266e622ce456c6a"></a>
![SET 연산 결과](../assets/images/18f32a16a608701f.png)

<a id="38f22ccbe5b479ff"></a>
##### 연산자 우선 순위

&lt;set operator&gt;의 연산자 우선순위는 다음과 같다.

- 괄호 ( ) 우선
- INTERSECT 우선 
- UNION, EXCEPT는 left-right로 기술한 순서 우선

<a id="60635ff618fb8cc4"></a>
##### &lt;set operator&gt;의 결과 타입

&lt;set operator&gt; 모든 부질의의 i 번째 column은 동일한 계열의 데이터 타입이어야 하며, [결과 타입 조합 규칙](11-sql-elements.md#08f567244d3c0586)에 따라 결과 타입이 결정된다.  
단, LONG VARCHAR와 LONG VARBINARY 타입은 UNION ALL만 사용할 수 있다.

<a id="867419d56e5dd045"></a>
##### ORDER BY 구문

&lt;set operator&gt;를 ORDER BY와 함께 사용할 때 부질의 간에 column 이름이 다를 경우, 다음과 같이 사용할 수 있다.

- ORDER BY indicator 
    - 결과 column의 순서를 기술한다.   
      SELECT c1 FROM t1   
      UNION ALL   
      SELECT c2 FROM t2   
      ORDER BY 1; 
- ORDER BY left_column_name 
    - 첫 번째 subquery의 column 이름을 기술한다.   
      SELECT c1 FROM t1   
      UNION ALL   
      SELECT c2 FROM t2   
      ORDER BY c1;

<a id="813104dadd671f81"></a>
#### 사용 예

다음은 UNION 연산을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT s_nation nation FROM supplier UNION ALL SELECT c_nation FROM customer;

NATION
-------------
FRANCE
KOREA
GERMANY
UNITED STATES
CANADA
KOREA
CANADA
KOREA
GERMANY
UNITED STATES

10 rows selected.

gSQL> SELECT s_nation nation FROM supplier UNION DISTINCT SELECT c_nation FROM customer;

NATION
-------------
UNITED STATES
CANADA
KOREA
GERMANY
FRANCE

5 rows selected.
```

다음은 EXCEPT 연산을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_nation nation FROM customer EXCEPT ALL SELECT s_nation FROM supplier;

NATION
------
KOREA

1 row selected.

gSQL> SELECT c_nation nation FROM customer EXCEPT DISTINCT SELECT s_nation FROM supplier;

no rows selected.
```

다음은 INTERSECT 연산을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_nation nation FROM customer INTERSECT ALL SELECT s_nation FROM supplier;

NATION
-------------
UNITED STATES
CANADA
KOREA
GERMANY

4 rows selected.

gSQL> SELECT c_nation nation FROM customer INTERSECT DISTINCT SELECT s_nation FROM supplier;

NATION
-------------
UNITED STATES
CANADA
KOREA
GERMANY

4 rows selected.
```

<a id="11bad1909c0462b4"></a>
#### 호환성

&lt;set operator&gt;는 SQL 표준과 비교하여 다음과 같은 차이가 있다.

- SQL 표준에서는 MINUS를 지원하지 않는다.
- SQL 표준에서는 &lt;set operator&gt;와 ORDER BY indicator를 함께 사용할 수 없다. 
- SQL 표준에서는 &lt;set operator&gt;와 ORDER BY column_name이 함께 사용될 경우, 모든 부질의의 column 이름과 동일해야 한다.

**SQL 표준 호환성**

<a id="96edbeee7b4f8bbb"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F302 | INTERSECT table operator | O |
| F301 | CORRESPONDING | X |
| T551 | Optional key words for default syntax | O |
| F304 | EXCEPT ALL table operator | O |

<a id="aa9636921fe3113a"></a>
#### 참조

관련 내용은 [query expression](#1c4140d8d3200490)을 참조한다.

<a id="5ddb0216f95db4a6"></a>
### subquery

<a id="52a850d538df3a28"></a>
#### 기능

&lt;query expression&gt;에서 파생되는 scalar value, row, table 등을 기술한다.

<a id="6f97fc79ecd2afb9"></a>
#### 구문

```
<scalar subquery> ::=
    <subquery>

<row subquery> ::=
    <subquery>

<table subquery> ::=
    <subquery>

<subquery> ::=
    ( <query expression> )
```

<a id="f0842a31a3046368"></a>
#### 사용 범위 및 접근 권한

&lt;subquery&gt;에 존재하는 &lt;query expression&gt;에 대한 접근 권한이 있어야 한다.

<a id="b1f7e019de4b34f2"></a>
#### 구문 규칙 및 파라미터

<a id="b2b5b7eed4dfceb3"></a>
##### &lt;scalar subquery&gt;

- &lt;query expression&gt;에 존재하는 target의 개수는 한 개이어야 한다.
- &lt;query expression&gt;에서 반환된 row의 개수에 따른 결과값은 다음과 같다.
    - 0 개의 row가 반환된 경우, 결과값은 NULL 이다.
    - 한 개의 row가 반환된 경우, 결과값은 해당 row에 포함된 결과값이다.
    - 두 개 이상의 row가 반환된 경우, exception error가 발생한다.

<a id="520ee1f751b0dba9"></a>
##### &lt;row subquery&gt;

- &lt;query expression&gt;에 존재하는 target의 개수는 두 개 이상이어야 한다.
- &lt;query expression&gt;에서 반환된 row의 개수에 따른 결과값은 다음과 같다.
    - 0 개의 row가 반환된 경우, 결과값은 모든 column이 NULL인 row이다.
    - 한 개의 row가 반환된 경우, 결과값은 해당 row이다.
    - 두 개 이상의 row가 반환된 경우, exception error가 발생한다.

<a id="c5f0f185957b3210"></a>
##### &lt;table subquery&gt;

- &lt;query expression&gt;에 존재하는 target의 개수는 한 개 이상이어야 한다.
- &lt;query expression&gt;에서 반환된 row의 개수에 따른 결과값은 다음과 같다.
    - 0 개의 row가 반환된 경우, 결과값은 no rows이다.
    - 한 개 이상의 row가 반환된 경우, 결과값은 해당 row이다.

<a id="a7876fa0457af43c"></a>
#### 설명

<a id="c5fbc496665e0c00"></a>
##### &lt;scalar subquery&gt;

&lt;scalar subquery&gt;는 결과값으로 한 개의 column을 갖는 한 개의 row를 반환하는 subquery이다. &lt;scalar subquery&gt;의 target은 하나만 존재해야 하며, 결과의 data type은 target의 data type을 따른다.

&lt;scalar subquery&gt;는 &lt;select list&gt;의 target에 단독으로 쓰일 수 있으며, 단일 column만 갖는 연산자에 쓰일 수 있다.

<a id="f0fb0691ed4836c3"></a>
##### &lt;row subquery&gt;

&lt;row subquery&gt;는 결과값으로 두 개 이상의 column을 갖는 한 개의 row를 반환하는 subquery이다. &lt;row subquery&gt;의 target은 두 개 이상 존재해야 하며, 결과의 data type은 target들 각각의 data type을 따른다.

&lt;row subquery&gt;는 &lt;select list&gt;의 target에 단독으로 쓰일 수 없으며, 둘 이상의 column을 갖는 row 연산자에만 쓰일 수 있다.

<a id="1707518f75075114"></a>
##### &lt;table subquery&gt;

&lt;table subquery&gt;는 결과값으로 한 개 이상의 column을 갖는 한 개 이상의 row를 반환하는 subquery이다. &lt;table subquery&gt;의 target은 한 개 이상 존재해야 하며, 결과의 data type은 target들 각각의 data type을 따른다.

&lt;table subquery&gt;는 &lt;select list&gt;의 target에 단독으로 쓰일 수 없으며, IN, NOT IN, EXISTS, NOT EXISTS, quantify operator 등의 연산자에 쓰일 수 있다.

<a id="8a5953ced26e23e0"></a>
#### 사용 예

다음은 &lt;scalar subquery&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT (SELECT c_name FROM dual)  FROM customer;

(SELECT C_NAME FROM DUAL)
-------------------------
Customer#1
Customer#2
Customer#3
Customer#4
Customer#5

5 rows selected.

gSQL> SELECT c_name, c_nation FROM customer WHERE c_nation = (SELECT 'CANADA' FROM dual);

C_NAME     C_NATION
---------- --------
Customer#2 CANADA

1 row selected.
```

다음은 &lt;row subquery&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT p_name, p_brand, p_type FROM part WHERE (p_brand, p_type) = (SELECT 'Brand#1', 'NICKEL' FROM dual);

P_NAME P_BRAND    P_TYPE
------ ---------- ------
Part#2 Brand#1    NICKEL

1 row selected.
```

다음은 &lt;table subquery&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT s_name, s_nation FROM supplier WHERE s_nation IN (SELECT c_nation FROM customer);

S_NAME                    S_NATION
------------------------- -------------
Supplier#2                KOREA
Supplier#3                GERMANY
Supplier#4                UNITED STATES
Supplier#5                CANADA

4 rows selected.

gSQL> SELECT * FROM (SELECT s_name, s_nation FROM supplier);

S_NAME                    S_NATION
------------------------- -------------
Supplier#1                FRANCE
Supplier#2                KOREA
Supplier#3                GERMANY
Supplier#4                UNITED STATES
Supplier#5                CANADA

5 rows selected.
```

<a id="e56dc68e2613a58e"></a>
#### 호환성

**SQL 표준 호환성**

<a id="73812bd070278fb5"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F471 | Scalar subquery values | O |
| F641 | Row and table constructors | X |
| T501 | Enhanced EXISTS predicate | O |
| E061-11 | Subqueries in IN predicate | O |
| E061-12 | Subqueries in quantified comparison predicate | O |
| E061-12 | Correlated subqueries | O |

<a id="e538fcc2ef7399cf"></a>
#### 참조

관련 내용은 다음을 참조한다.

- [from clause](#43529f212b19c0e0)
- [where clause](#8ffd103d5116485d)

<a id="a12a3515f3dbcd31"></a>
### hint clause

<a id="cc00539ede5fdf8c"></a>
#### 기능

Query를 수행할 때 사용할 hint를 기술한다.

<a id="bac8028141fe6000"></a>
#### 구문

```
<hint clause> ::=
    /*+ <hint element> [ comment ] [ [ , ] <hint element> [ comment ] ] */

<hint element> ::=
      <access path hints>
    | <join order hints>
    | <join operation hints>
    | <query transformation hints>
    | <other hints>

<access_path_hints> ::=
      FULL( table_name )
    | INDEX( table_name [ , ] [ index_name [ [ , ] index_name ] ] )
    | NO_INDEX( table_name [ , ] [ index_name [ [ , ] index_name ] ] )
    | INDEX_ASC( table_name [ , ] [ index_name [ [ , ] index_name ] ] )
    | INDEX_DESC( table_name [ , ] [ index_name [ [ , ] index_name ] ] )
    | INDEX_COMBINE( table_name [ , ] [ index_name [ [ , ] index_name ] ] )
    | ROWID( table_name )

<join order hints> ::=
      ORDERED
    | ORDERING( table_name [ LEFT | RIGHT ] [ , table_name [ LEFT | RIGHT ] ]
    | LEADING( table_name [ [ , ] table_name ] )

<join operation hints> ::=
      USE_HASH( table_name [ [ , ] table_name ] )
    | NO_USE_HASH( table_name [ [ , ] table_name ] )
    | USE_MERGE( table_name [ [ , ] table_name ] )
    | NO_USE_MERGE( table_name [ [ , ] table_name ] )
    | USE_NL( table_name [ [ , ] table_name ] )
    | NO_USE_NL( table_name [ [ , ] table_name ] )
    | USE_INL( table_name [ [ , ] table_name ] )
    | NO_USE_INL( table_name [ [ , ] table_name ] )

<query transformation hints> ::=
      UNNEST
    | NO_UNNEST
    | NL_SJ
    | NL_ISJ
    | MERGE_SJ
    | HASH_SJ
    | HASH_ISJ
    | HASH_AJ
    | TRANSITIVE_CLOSURE
    | NO_TRANSITIVE_CLOSURE
    | MERGE( view_name ) 
    | NO_MERGE( view_name ) 
    | NO_QUERY_TRANSFORMATION

<other hints> ::=
      PUSH_SUBQ
    | NO_PUSH_SUBQ
```

<a id="d16b77bcebd48826"></a>
#### 사용 범위 및 접근 권한

&lt;hint clause&gt; 구문을 수행하려면 사용자에게 query를 수행할 수 있는 권한이 필요하다.

<a id="83deeadd4b472f81"></a>
#### 구문 규칙 및 파라미터

&lt;hint clause&gt; 사용의 기본 구문 규칙은 다음과 같다.

- &lt;hint clause&gt;에는 공백이나 ','를 이용하여 다수의 &lt;hint element&gt;를 기술할 수 있다.
- 동일한 object에 대한 &lt;hint element&gt;가 둘 이상이고 동시에 적용할 수 없는 경우, 먼저 기술된 &lt;hint element&gt; 하나만 적용된다.
- &lt;hint element&gt;에 구문상 에러가 발생하면 기본적으로 해당 &lt;hint element&gt;를 무시하며, "hint_error" property를 on으로 하면 &lt;hint clause&gt;에 대한 validation error로 처리된다.
- &lt;hint clause&gt;에 기술된 table name은 &lt;from clause&gt;에 기술한 table name (alias name가 기술된 table의 경우 alias name) 중 하나와 일치하여야 한다.
- Table name은 schema name과 함께 기술할 수 없다.
- &lt;hint element&gt;가 올바르게 기술되었더라도 그것을 적용할 수 없는 경우에는 optimizer가 해당 &lt;hint element&gt;를 무시한다.

<a id="3b109f20af749d49"></a>
##### &lt;access_path_hints&gt;

<a id="0b616297164952f8"></a>
###### **FULL**

Optimizer로 하여금 기술한 table에 대하여 table full scan 하도록 지시한다. 이 hint가 기술된 경우, optimizer는 해당 table에 대하여 index scan을 이용한 최적화나 rowid scan을 이용한 최적화, index combine을 이용하는 최적화 등을 고려하지 않는다.

FULL hint를 기술할 때 table name을 반드시 기술해야 하는데 table name은 하나만 기술할 수 있다. 또한 기술된 table name은 &lt;from clause&gt;에 반드시 존재해야 한다.

다음은 T1 table에 대하여 table full scan 하도록 하는 hint를 적용하는 예이다.

- 유형 1: &lt;from clause&gt;에 table name을 기술한 경우

```
SELECT /*+ FULL(T1) */ I1
  FROM T1;
```

- 유형 2: &lt;from clause&gt;에 alias name을 기술한 경우

```
SELECT /*+ FULL(T1_ALIAS) */ I1
  FROM T1 T1_ALIAS;
```

<a id="9985b0661d2ce4ab"></a>
###### **INDEX**

Optimizer로 하여금 기술한 table에 대하여 index scan 하도록 지시한다. 이 hint가 기술된 경우, optimizer는 해당 table에 대하여 table scan을 이용한 최적화나 다른 index에 의한 index scan을 이용한 최적화, rowid scan을 이용한 최적화, index combine을 이용한 최적화 등을 고려하지 않는다.

INDEX hint를 기술할 때는 table name이 &lt;from clause&gt;에 존재해야 하며, index name도 해당 table에 존재하는 index의 이름이어야 한다.

Index name은 하나 이상 기술하거나 생략할 수도 있다. Index name을 생략한 경우에는 해당 table에 속한 모든 index들을 대상으로 한다.

만약 index name을 둘 이상 나열하거나 index가 둘 이상인 table에 대하여 index name을 생략한 경우에는 optimizer가 해당 index들의 index scan cost를 계산하여 최적의 index scan 방법을 선택한다.

다음은 T1 table을 index scan 하도록 hint를 적용한 예이다.

- 유형 1: index name을 하나만 기술한 경우

```
SELECT /*+ INDEX(T1, T1_PK_INDEX) */ I1
  FROM T1;
```

- 유형 2: index name을 둘 이상 기술한 경우

```
SELECT /*+ INDEX(T1, T1_PK_INDEX T1_UNIQUE_INDEX) */ I1
  FROM T1;
```

- 유형 3: index name을 생략한 경우

```
SELECT /*+ INDEX(T1) */ I1
  FROM T1;
```

<a id="e1b0bb3bb22b2d7d"></a>
###### **NO_INDEX**

Optimizer로 하여금 기술한 table에서 index name에 해당하는 index들을 index scan 하지 않도록 지시한다. 이 hint가 기술되면 optimizer는 해당 table에 대하여 기술된 index들에 대해 index scan을 이용하여 최적화하는 것을 고려하지 않는다.

NO_INDEX hint를 기술할 때 table name은 &lt;from clause&gt;에 존재해야 하며, index name도 해당 table에 존재하는 index의 이름이어야 한다.

Index name은 하나 이상 기술하거나 생략할 수도 있으며, index name을 생략한 경우에는 optimizer가 해당 table에 대한 index scan을 고려하지 않는다.

NO_INDEX hint에 기술되지 않은 index들이 존재할 경우, optimizer가 해당 index들의 index scan cost를 계산하고, table scan cost와 rowid scan cost들까지 고려하여 최적의 scan 방법을 선택한다.

다음은 T1 table에 대하여 NO_INDEX hint를 적용한 예이다.

- 유형 1: index name을 하나만 기술한 경우

```
SELECT /*+ NO_INDEX(T1, T1_PK_INDEX) */ I1
  FROM T1;
```

- 유형 2: index name을 둘 이상 기술한 경우

```
SELECT /*+ NO_INDEX(T1, T1_PK_INDEX T1_UNIQUE_INDEX) */ I1
  FROM T1;
```

- 유형 3: index name을 생략한 경우

```
SELECT /*+ NO_INDEX(T1) */ I1
  FROM T1;
```

<a id="4b1ac3db0d67b0d0"></a>
###### **INDEX_ASC**

Optimizer로 하여금 기술한 table에서 ascending index scan 하도록 지시한다. 이 hint가 기술되면 optimizer는 해당 table에 대하여 table scan을 이용한 최적화나 다른 index에 의한 index scan을 이용한 최적화, rowid scan을 이용한 최적화, index combine을 이용한 최적화 등을 고려하지 않는다.

만약 선택된 index scan의 index가 ascending order로 구성되어 있다면 ascending order로, index가 descending order로 구성되어 있다면 descending order로 index를 scan한다.

INDEX_ASC hint에 대한 구문 규칙은 INDEX hint와 동일하다.

<a id="dc4586aa6d998b38"></a>
###### **INDEX_DESC**

Optimizer로 하여금 기술한 table에서 descending index scan 하도록 지시한다. 이 hint가 기술되면 optimizer는 해당 table에 대하여 table scan을 이용한 최적화나 다른 index에 의한 index scan을 이용한 최적화, rowid scan을 이용한 최적화, index combine을 이용한 최적화 등을 고려하지 않는다.

만약 선택된 index scan의 index가 ascending order로 구성되어 있다면 descending order로, index가 descending order로 구성되어 있다면 ascending order로 index를 scan한다.

INDEX_DESC hint에 대한 구문 규칙은 INDEX hint와 동일하다.

<a id="fa2738211f69c1aa"></a>
###### **INDEX_COMBINE**

Optimizer로 하여금 기술한 table에 대해 or 구문을 분리하여 각각 index scan을 수행한 후 결과들을 합치도록 지시한다. 이 hint가 기술되면 index combine을 이용한 최적화를 우선적으로 고려하며, 만약 index combine이 가능하지 않을 경우, table scan이나 index scan, rowid scan 등에 대한 cost를 계산하여 최적의 scan 방법을 선택한다.

INDEX_COMBINE hint를 기술할 때 table name이 &lt;from clause&gt;에 존재해야 하며, index name도 해당 table에 존재하는 index의 이름이어야 한다.

Index name은 하나 이상 기술할 수 있고 생략도 가능하다. Index name을 생략할 경우에는 해당 table에 속한 모든 index들을 대상으로 한다.

INDEX_COMBINE hint를 수행하려면 해당 table을 scan하기 위한 조건에 or 구문이 반드시 존재해야 한다. 만약 or 구문이 존재하지 않으면 optimizer가 해당 hint를 무시하며, 이 경우 table scan, index scan, rowid scan에 대한 cost를 계산하여 최적의 scan 방법을 선택한다.

Index name을 둘 이상 나열하거나 index가 둘 이상인 table에 대하여 index name을 생략할 경우 optimizer가 각 or 구문에 대하여 해당 index들의 index scan cost를 계산하여 최적의 index scan을 선택한다. 따라서 or 구문으로 분리된 조건들에 의해 각각 다른 index를 사용하는 index scan을 선택할 수 있다.

다음은 T1 table을 index combine 하도록 hint를 적용한 예이다.

- 유형 1: index name을 하나만 기술한 경우

```
SELECT /*+ INDEX_COMBINE(T1, T1_PK_INDEX) */ I1
  FROM T1
 WHERE I1 = 1
    OR I1 = 2;
```

- 유형 2: index name을 둘 이상 기술한 경우

```
SELECT /*+ INDEX_COMBINE(T1, T1_PK_INDEX T1_UNIQUE_INDEX) */ I1
  FROM T1
 WHERE I1 = 1
    OR I2 = 2;
```

- 유형 3: index name을 생략한 경우

```
SELECT /*+ INDEX_COMBINE(T1) */ I1
  FROM T1
 WHERE I1 = 1
    OR I2 = 2;
```

- 유형 4: INDEX_COMBINE hint를 적용할 수 없는 경우 (or 구문이 없는 경우)

```
SELECT /*+ INDEX_COMBINE(T1, T1_PK_INDEX) */ I1
  FROM T1
 WHERE I1 = 1;
```

<a id="7bc64711ad9a3b7e"></a>
###### **ROWID**

Optimizer로 하여금 기술한 table에 대하여 rowid scan 하도록 지시한다. 이 hint가 기술되면 rowid scan을 이용한 최적화를 우선적으로 고려하며, 만약 rowid scan이 가능하지 않을 경우, table scan이나 index scan, index combine 등에 대한 cost를 계산하여 최적의 scan 방법을 선택한다.

ROWID hint를 기술할 때 table name을 반드시 기술해야 하는데 table name은 하나만 기술할 수 있다. 또한 기술된 table name은 반드시 &lt;from clause&gt;에 존재해야 한다.

ROWID hint를 수행하려면 해당 table을 scan하기 위한 조건에 ROWID를 이용한 equal 조건이 반드시 존재해야 한다. 만약 존재하지 않으면 optimizer가 해당 hint를 무시하며, 이 경우 table scan과 index scan, index combine에 대한 cost를 계산하여 최적의 scan 방법을 선택한다.

다음은 T1 table을 rowid scan 하도록 hint를 적용한 예이다.

- 유형 1: &lt;from clause&gt;에 table name을 기술한 경우

```
SELECT /*+ ROWID(T1) */ I1
  FROM T1
 WHERE ROWID = 'AAAAAAAAADXAACAAAGAlAAA';
```

- 유형 2: &lt;from clause&gt;에 alias name을 기술한 경우

```
SELECT /*+ ROWID(T1_ALIAS) */ I1
  FROM T1 T1_ALIAS
 WHERE ROWID = 'AAAAAAAAADXAACAAAGAlAAA';
```

- 유형 3: ROWID hint를 적용할 수 없는 경우 (rowid 조건이 없는 경우)

```
SELECT /*+ ROWID(T1) */ I1
  FROM T1
 WHERE I1 = 1;
```

<a id="1765ea529ae7c793"></a>
##### &lt;join_order_hints&gt;

<a id="a63b5a722b8d2d7a"></a>
###### **ORDERED**

Optimizer로 하여금 &lt;from clause&gt;에 기술한 순서대로 table들을 join 하도록 지시한다. 이 hint는 &lt;from clause&gt;에 ','로 구분된 table들을 기술하거나 inner join으로 table들을 기술하는 경우에만 적용할 수 있다.

다음은 T1, T2 table에 대한 join에 ORDERED hint를 적용한 예이다.

- 유형 1: &lt;from clause&gt;에 ','로 구분된 table들을 기술한 경우

```
SELECT /*+ ORDERED */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

- 유형 2: &lt;from clause&gt;에 inner join으로 table들을 기술한 경우

```
SELECT /*+ ORDERED */ *
  FROM T1 INNER JOIN T2 ON T1.I1 = T2.I1;
```

- 유형 3: ORDERED hint를 적용할 수 없는 경우 (outer join인 경우)

```
SELECT /*+ ORDERED */ *
  FROM T1 LEFT OUTER JOIN T2 ON T1.I1 = T2.I1;
```

<a id="1d3960fb908ff5c9"></a>
###### **ORDERING**

Optimizer로 하여금 이 hint에 기술된 table들을 순서대로 join 하도록 지시한다. 이 hint는 &lt;from clause&gt;에 ','로 구분된 table들을 기술하거나 inner join으로 table들을 기술하는 경우에만 적용할 수 있다.

ORDERING hint는 각 table에 위치 지정 옵션을 기술할 수 있는데 첫 번째와 두 번째 table에 대해서는 기술할 수 없고 세 번째 table부터 기술할 수 있다. 첫 번째와 두 번째 table의 위치는 ORDERING hint에 기술된 순서에 따라 결정된다. 위치 지정 옵션에는 LEFT와 RIGHT가 있는데 LEFT는 해당 table을 join의 left node (outer node)에 위치하도록 하며, RIGHT는 해당 table을 join의 right node (inner node)로 위치하도록 한다.

만약 table에 위치 지정 옵션을 기술한 경우, 해당 table은 기술된 위치에 고정된 채로 join을 수행한다. Table에 위치 지정 옵션을 기술하지 않은 경우, optimizer가 해당 table을 left node (outer node)에 배치하는 경우와 right node (inner node)에 배치하는 경우에 대해 각각의 cost를 계산하여 최적의 join 순서를 선택한다.

다음은 T1, T2, T3 table들의 join에 대하여 ORDERING hint를 적용한 예이다.

- 유형 1: &lt;from clause&gt;에 ','로 구분된 table들을 기술한 경우

```
SELECT /*+ ORDERING(T2, T3, T1) */ *
  FROM T1, T2, T3
 WHERE T1.I1 = T2.I1
   AND T2.I2 = T3.I2;
```

- 유형 2: &lt;from clause&gt;에 inner join으로 table들을 기술한 경우

```
SELECT /*+ ORDERING(T2, T3, T1) */ *
  FROM (T1 INNER JOIN T2 ON T1.I1 = T2.I1) INNER JOIN T3 ON T2.I2 = T3.I2;
```

- 유형 3: ORDERING hint에 위치 지정 옵션을 기술한 경우

```
SELECT /*+ ORDERING(T2, T3, T1 LEFT) */ *
  FROM T1, T2, T3
 WHERE T1.I1 = T2.I1
   AND T2.I2 = T3.I2;
```

- 유형 4: ORDERING hint를 적용할 수 없는 경우 (outer join인 경우)

```
SELECT /*+ ORDERING(T1, T2) */ *
  FROM T1 LEFT OUTER JOIN T2 ON T1.I1 = T2.I1;
```

- 유형 5: ORDERING hint에서 위치 지정 옵션을 잘못 사용한 경우 (첫 번째 table에 사용한 경우)

```
SELECT /*+ ORDERING(T2 RIGHT, T3, T1) */ *
  FROM T1, T2, T3
 WHERE T1.I1 = T2.I1
   AND T2.I2 = T3.I2;
```

<a id="fd038160afefba9a"></a>
###### **LEADING**

Optimizer로 하여금 이 hint에 기술된 table들을 순서대로 join 하도록 지시한다. 이 hint는 &lt;from clause&gt;에 ','로 구분된 table들을 기술하거나 inner join으로 table들을 기술하는 경우에만 적용할 수 있다.

LEADING hint는 ORDERING hint와 달리 위치를 지정할 수 없기 때문에 join에 참여하는 table 순서만 지정할 수 있다. 따라서 첫 번째와 두 번째 table은 순서에 따라 각각 left node (outer node)와 right node (inner node)에 배치되며, 세 번째 table부터는 optimizer가 해당 table을 left node (outer node)에 배치하는 경우와 right node (inner node)에 배치하는 경우의 cost를 계산하여 둘 중 더 좋은 위치에 배치한다.

다음은 T1, T2, T3 table들의 join에 대하여 LEADING hint를 적용한 예이다.

- 유형 1: &lt;from clause&gt;에 ','로 구분된 table들을 기술한 경우

```
SELECT /*+ LEADING(T2, T3, T1) */ *
  FROM T1, T2, T3
 WHERE T1.I1 = T2.I1
   AND T2.I2 = T3.I2;
```

- 유형 2: &lt;from clause&gt;에 inner join으로 table들을 기술한 경우

```
SELECT /*+ LEADING(T2, T3, T1) */ *
  FROM (T1 INNER JOIN T2 ON T1.I1 = T2.I1) INNER JOIN T3 ON T2.I2 = T3.I2;
```

- 유형 3: LEADING hint를 적용할 수 없는 경우 (outer join인 경우)

```
SELECT /*+ LEADING(T1, T2) */ *
  FROM T1 LEFT OUTER JOIN T2 ON T1.I1 = T2.I1;
```

<a id="bce12950553ca8b1"></a>
##### &lt;join operation_hints&gt;

<a id="bcd3614e2fa69fa9"></a>
###### **USE_HASH**

Join을 수행할 때 이 hint에 기술한 table이 포함될 경우, optimizer로 하여금 hash join 기법으로 join 하도록 한다. 이 hint는 모든 join type에 적용할 수 있다.

USE_HASH hint에는 하나 이상의 table을 기술해야 하며, 동일한 table을 둘 이상 기술할 수 없다. 이 hint에 기술된 table은 USE_MERGE, USE_NL, USE_INL 등의 hint에 기술되면 안된다. 기술하는 경우 "hint_error" property가 on이면 validation error로 처리되며, off이면 먼저 기술된 hint가 적용된다. 또한 join에 참여하는 두 table에 대하여 각각 다른 join operation hint가 기술되면 left node (outer node)에 기술된 hint가 우선 적용된다.

USE_HASH hint에 기술된 table이 join에 참여하는 경우 join 조건에 hash join이 가능한 조건 (equi-join이어야 하고 비교 가능한 column이어야 함)이 존재해야 한다. 만약 hash join이 가능한 조건이 존재하지 않을 경우, optimizer가 해당 hint를 무시하고 cost 계산을 통해 최적의 join operation을 선택한다.

다음은 T1, T2 table들의 join에 대하여 USE_HASH hint를 적용한 예이다.

- 유형 1: 한 table에 대해서만 join operation hint를 기술한 경우

```
SELECT /*+ USE_HASH(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

- 유형 2: 두 table에 대하여 각각 다른 join operation hint를 기술한 경우  
  (ORDERED hint에 의해 순서가 지정되어 left node (outer node)에 위치한 T1 table에 대한 join operation hint (USE_HASH)가 적용됨)

```
SELECT /*+ ORDERED USE_HASH(T1) USE_MERGE(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

- 유형 3: USE_HASH hint를 적용할 수 없는 경우 (hash join 조건이 없는 경우)

```
SELECT /*+ USE_HASH(T1, T2) */ *
  FROM T1, T2
 WHERE T1.I1 < T2.I1;
```

<a id="0e7d33fd3c957962"></a>
###### **NO_USE_HASH**

Join을 수행할 때 이 hint에 기술한 table이 포함될 경우, optimizer로 하여금 hash join 기법을 제외한 나머지 기법 중 하나를 선택하여 join 하도록 한다. 이 hint는 모든 join type에 적용할 수 있다.

NO_USE_HASH hint에는 하나 이상의 table을 기술해야 하며, 동일한 table을 둘 이상 기술할 수 없다. 이 hint에 기술된 table은 USE_HASH hint를 제외한 다른 join operation hint에 기술할 수 있다. 이 hint에 기술된 table이 USE_HASH hint에 기술되고 "hint_error" property가 on인 경우 validation error로 처리되며, off인 경우 먼저 기술된 hint가 적용된다. 또한 join에 참여하는 두 table에 각각 다른 join operation hint가 기술되면 left node (outer node)에 기술된 hint가 우선 적용된다.

NO_USE_HASH hint에 기술된 table이 join에 참여하는 경우, optimizer가 hash join을 제외한 나머지 join operation 기법들에 대한 cost를 계산하여 그 중 최적의 join operation을 선택한다.

다음은 T1, T2 table들의 join에 대하여 NO_USE_HASH hint를 적용한 예이다.

- 유형 1: 하나의 table에 대해서만 join operation hint를 기술한 경우

```
SELECT /*+ NO_USE_HASH(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

- 유형 2: 두 table에 각각 다른 join operation hint를 기술한 경우  
  (T2 table에 기술한 hint가 적용되어 merge join 처리됨)

```
SELECT /*+ NO_USE_HASH(T1) USE_MERGE(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

<a id="be17c80ad7739972"></a>
###### **USE_MERGE**

Join을 수행할 때 이 hint에 기술한 table이 포함될 경우, optimizer로 하여금 merge join 기법으로 join 하도록 한다. 이 hint는 모든 join type에 적용할 수 있다.

USE_MERGE hint에는 하나 이상의 table을 기술해야 하며, 동일한 table을 둘 이상 기술할 수 없다. 이 hint에 기술된 table은 USE_HASH, USE_NL, USE_INL 등의 hint에 기술되면 안된다. 기술하는 경우 "hint_error" property가 on이면 validation error로 처리되며, off이면 먼저 기술된 hint가 적용된다. 또한 join에 참여하는 두 table에 각각 다른 join operation hint가 기술되면 left node (outer node)에 기술된 hint가 우선 적용된다.

USE_MERGE hint에 기술된 table이 join에 참여하는 경우, join 조건에 merge join이 가능한 조건 (equi-join이어야 하고 비교 가능한 column이어야 함)이 존재해야 하며, 만약 merge join이 가능한 조건이 존재하지 않을 경우, optimizer가 해당 hint를 무시하고 cost를 계산하여 최적의 join operation을 선택한다.

다음은 T1, T2 table들의 join에 대하여 USE_MERGE hint를 적용한 예이다.

- 유형 1: 하나의 table에 대해서만 join operation hint를 기술한 경우

```
SELECT /*+ USE_MERGE(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

- 유형 2: 두 table에 각각 다른 join operation hint를 기술한 경우  
  (ORDERED hint가 순서를 결정하여 left node (outer node)에 위치한 T1 table에 join operation hint (USE_MERGE)가 적용됨)

```
SELECT /*+ ORDERED USE_MERGE(T1) USE_HASH(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

- 유형 3: USE_MERGE hint를 적용할 수 없는 경우 (hash join 조건이 없음)

```
SELECT /*+ USE_MERGE(T1, T2) */ *
  FROM T1, T2
 WHERE T1.I1 < T2.I1;
```

<a id="61b275d975b2238f"></a>
###### **NO_USE_MERGE**

Join을 수행할 때 이 hint에 기술한 table이 포함될 경우, optimizer로 하여금 merge join 기법을 제외한 나머지 기법 중 하나를 선택하여 join 하도록 한다. 이 hint는 모든 join type에 적용할 수 있다.

NO_USE_MERGE hint에는 하나 이상의 table을 기술해야 하며, 동일한 table을 둘 이상 기술할 수 없다. 이 hint에 기술된 table은 USE_MERGE hint를 제외한 다른 join operation hint에 기술할 수 있다. 이 hint에 기술된 table이 USE_MERGE hint에 기술된 경우 "hint_error" property가 on이면 validation error로 처리되며, off이면 먼저 기술된 hint가 적용된다. 또한 join에 참여하는 두 table에 각각 다른 join operation hint가 기술되면 left node (outer node)에 기술된 hint가 우선 적용된다.

NO_USE_MERGE hint에 기술된 table이 join에 참여하는 경우, optimizer가 merge join을 제외한 나머지 join operation 기법들의 cost를 계산하여 최적의 join operation을 선택한다.

다음은 T1, T2 table들의 join에 대하여 NO_USE_MERGE hint를 적용한 예이다.

- 유형 1: 하나의 table에 대해서만 join operation hint를 기술한 경우

```
SELECT /*+ NO_USE_MERGE(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

- 유형 2: 두 table에 각각 다른 join operation hint를 기술한 경우  
  (T2 table에 기술한 hint가 적용되어 hash join 됨)

```
SELECT /*+ NO_USE_MERGE(T1) USE_HASH(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

<a id="79cf57e3396918fc"></a>
###### **USE_NL**

Join을 수행할 때 이 hint에 기술한 table이 포함되면 optimizer로 하여금 nested loops join 기법으로 join하도록 한다. 이 hint는 모든 join type에 적용할 수 있다.

USE_NL hint에는 하나 이상의 table을 기술해야 하며, 동일한 table을 둘 이상 기술할 수 없다. 이 hint에 기술된 table이 USE_HASH, USE_MERGE, USE_INL 등의 hint에 기술되면 안되며, 기술된 경우 "hint_error" property가 on이면 validation error로 처리되며, off이면 먼저 기술된 hint가 적용된다. 또한 join에 참여하는 두 table에 각각 다른 join operation hint가 기술되면 left node (outer node)에 기술된 hint가 우선 적용된다.

Nested loops join은 hash join이나 merge join과 다르게 어떠한 제약도 없이 join할 수 있는 기법이다.

다음은 T1, T2 table들의 join에 대하여 USE_NL hint를 적용한 예이다.

- 유형 1: 하나의 table에 대해서만 join operation hint를 기술한 경우

```
SELECT /*+ USE_NL(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

- 유형 2: 두 table에 각각 다른 join operation hint를 기술한 경우  
  (ORDERED hint가 순서를 결정하여 left node (outer node)에 위치한 T1 table에 join operation hint (USE_NL)가 적용됨)

```
SELECT /*+ ORDERED USE_NL(T1) USE_HASH(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

<a id="65c28b2ddcdb9166"></a>
###### **NO_USE_NL**

Join을 수행할 때 이 hint에 기술한 table이 포함될 경우, optimizer로 하여금 nested loops join 기법을 제외한 나머지 기법 중 하나를 선택하여 join 하도록 한다. 이 hint는 모든 join type에 적용할 수 있다.

NO_USE_NL hint에는 하나 이상의 table을 기술해야 하며, 동일한 table을 둘 이상 기술할 수 없다. 이 hint에 기술된 table은 USE_NL hint를 제외한 다른 join operation hint에도 기술할 수 있다. 이 hint에 기술된 table이 USE_NL hint에 기술된 경우, "hint_error" property가 on이면 validation error로 처리되며, off이면 먼저 기술된 hint가 적용된다. 또한 join에 참여하는 두 table에 각각 다른 join operation hint가 기술되면 left node (outer node)에 기술된 hint가 우선 적용된다.

NO_USE_NL hint에 기술된 table이 join에 참여하는 경우 optimizer가 nested loops join을 제외한 나머지 join operation 기법들의 cost를 계산하여 최적의 join operation을 선택한다. 단, 제약때문에 다른 join operation 기법들을 사용할 수 없는 경우, optimizer가 이 hint를 무시하고 nested loops join을 이용한 기법을 선택한다.

다음은 T1, T2 table들의 join에 대하여 NO_USE_NL hint를 적용한 예이다.

- 유형 1: 하나의 table에 대해서만 join operation hint를 기술한 경우

```
SELECT /*+ NO_USE_NL(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

- 유형 2: 두 table에 각각 다른 join operation hint를 기술한 경우  
  (T2 table에 기술한 hint가 적용되어 hash join 됨)

```
SELECT /*+ NO_USE_NL(T1) USE_HASH(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

- 유형 3: NO_USE_NL hint를 기술하였지만 제약 조건 때문에 hash join과 같은 다른 join operation을 적용할 수 없는 경우 (nested loops join 됨)

```
SELECT /*+ NO_USE_NL(T1) */ *
  FROM T1, T2
 WHERE T1.I1 < T2.I1;
```

<a id="449763b402612e4d"></a>
###### **USE_INL**

Join을 수행할 때 이 hint에 기술한 table이 포함될 경우, optimizer로 하여금 sort instant를 이용한 nested loops join 기법으로 join 하도록 한다. 이 hint는 &lt;from clause&gt;에 ','로 구분된 table들을 기술하거나 inner join으로 table들을 기술하는 경우에만 적용할 수 있다.

USE_INL hint에는 하나 이상의 table을 기술해야 하며, 동일한 table을 둘 이상 기술할 수 없다. 이 hint에 기술된 table은 USE_HASH, USE_MERGE, USE_NL 등의 hint에 기술되면 안되며, 기술하는 경우 "hint_error" property가 on이면 validation error로 처리되며, off이면 먼저 기술된 hint가 적용된다. 또한 join에 참여하는 두 table에 각각 다른 join operation hint가 기술되면 left node (outer node)에 기술된 hint가 우선 적용된다.

Sort instant를 이용한 nested loops join은 sort key가 right node (inner node)의 table에 대한 조인 조건을 만족하는 expression들인 sort instant를 생성하여 join하는 방법이다. 이 때 sort key는 key compare가 가능한 type이어야 한다. 조인 조건에 해당하는 expression들이 모두 key compare가 불가능한 type인 경우, 이 기법은 적용할 수 없다. 이 경우, 다른 join operation 기법들의 cost를 계산하여 최적의 기법을 적용한다.

다음은 T1, T2 table들의 join에 대하여 USE_INL hint를 적용한 예이다.

- 유형 1: 하나의 table에 대해서만 join operation hint를 기술한 경우

```
SELECT /*+ USE_INL(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

- 유형 2: 두 table에 각각 다른 join operation hint를 기술한 경우  
  (ORDERED hint가 순서를 결정하여 left node (outer node)에 위치한 T1 table에 join operation hint (USE_INL)가 적용됨)

```
SELECT /*+ ORDERED USE_INL(T1) USE_HASH(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

<a id="7287e8d27a1861fe"></a>
###### **NO_USE_INL**

Join을 수행할 때 이 hint에 기술한 table이 포함될 경우, optimizer로 하여금 sort instant를 이용한 nested loops join 기법을 제외한 나머지 기법 중 하나를 선택하여 join 하도록 한다. 이 hint는 모든 join type에 적용할 수 있다.

NO_USE_INL hint에는 하나 이상의 table을 기술해야 하며, 동일한 table을 둘 이상 기술할 수 없다. 이 hint에 기술된 table은 USE_INL hint를 제외한 다른 join operation hint에 기술할 수 있다. 이 hint에 기술된 table이 USE_INL hint에 기술된 경우 "hint_error" property가 on이면 validation error로 처리되며, off이면 먼저 기술된 hint가 적용된다. 또한 join에 참여하는 두 table에 각각 다른 join operation hint가 기술되면 left node (outer node)에 기술된 hint가 우선 적용된다.

NO_USE_INL hint에 기술된 table이 join에 참여하는 경우, optimizer가 sort instant를 이용한 nested loops join을 제외한 나머지 join operation 기법들의 cost를 계산하여 최적의 join operation을 선택한다.

다음은 T1, T2 table들의 join에 대하여 NO_USE_INL hint를 적용한 예이다.

- 유형 1: 하나의 table에 대해서만 join operation hint를 기술한 경우

```
SELECT /*+ NO_USE_INL(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

- 유형 2: 두 table에 대하여 각각 다른 join operation hint를 기술한 경우  
  (T2 table에 기술한 hint가 적용되어 hash join 됨)

```
SELECT /*+ NO_USE_INL(T1) USE_HASH(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

<a id="b24fd22def89c0d0"></a>
##### &lt;query_transformation_hints&gt;

<a id="6b99dae0a7b6f2cb"></a>
###### **UNNEST**

Optimizer로 하여금 subquery에 대하여 동일한 결과를 보장하는 join 구문으로 변경하도록 한다. 이는 subquery를 별도로 수행하지 않고 상위 레벨 query와의 join을 이용하여 처리함으로써 subquery가 반복적으로 수행되는 것을 방지한다.

UNNEST hint는 subquery의 &lt;hint clause&gt;에만 기술할 수 있으며 해당 subquery에만 적용될 뿐 하위 subquery들에는 적용되지 않는다. 만약 다수의 subquery가 존재할 때 이를 모두 unnest하고 싶은 경우에는 해당 subquery 모두에 UNNEST hint를 기술하여야 하며, subquery 내부에 존재하는 subquery에 대하여 unnest하고 싶은 경우에는 해당 subquery에 UNNEST hint를 기술하여야 한다.

UNNEST hint가 NO_QUERY_TRANSFORMATION hint와 함께 기술된 경우, NO_QUERY_TRANSFORMATION hint 때문에 UNNEST hint가 무시된다.

UNNEST hint는 NO_UNNEST hint와 동시에 사용할 수 없다. 동시에 사용하는 경우 "hint_error" property를 on으로 설정하면 validation error로 처리되며, off로 설정하면 먼저 기술한 hint가 적용된다.

다음은 UNNEST hint를 이용하여 subquery의 unnesting을 적용한 예이다.

- 유형 1: IN subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ UNNEST */ I1
                 FROM T2 );
```

- 유형 2: UNNEST hint와 NO_QUERY_TRANSFORMATION hint를 기술한 경우  
  (NO_QUERY_TRANSFORMATION hint 때문에 subquery를 unnesting하지 않음)

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ UNNEST NO_QUERY_TRANSFORMATION */ I1
                 FROM T2 );
```

<a id="4c718443514991d7"></a>
###### **NO_UNNEST**

Optimizer로 하여금 subquery를 unnesting을 하지 않고 filter로 처리하도록 한다. 이는 필요할 때마다 매번 subquery를 수행한다.

NO_UNNEST hint는 subquery의 &lt;hint clause&gt;에만 기술할 수 있으며, 해당 subquery에만 적용될 뿐 하위 subquery들에는 적용되지 않는다. 만약 다수의 subquery가 존재할 때 이를 모두 unnest하고 싶지 않은 경우에는 해당 subquery 모두에 NO_UNNEST hint를 기술하여야 하며, subquery 내부에 존재하는 subquery에 대하여 unnest하고 싶지 않은 경우에는 해당 subquery에 NO_UNNEST hint를 기술하여야 한다.

NO_UNNEST hint가 NO_QUERY_TRANSFORMATION hint와 함께 기술된 경우 NO_QUERY_TRANSFORMATION hint 때문에 NO_UNNEST hint가 무시된다.

NO_UNNEST hint는 UNNEST hint와 동시에 사용할 수 없다. 동시에 사용하는 경우 "hint_error" property를 on으로 설정하면 validation error로 처리되며, off로 설정하면 먼저 기술한 hint가 적용된다.

다음은 NO_UNNEST hint를 이용하여 subquery의 no unnesting을 적용한 예이다.

- IN subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ NO_UNNEST */ I1
                 FROM T2 );
```

<a id="80de5b2501b48f00"></a>
###### **NL_SJ**

Optimizer로 하여금 subquery를 nested loops semi join으로 처리하도록 한다. 이는 subquery를 동일한 결과를 갖는 semi join 형태로 풀어낸다.

NL_SJ는 EXISTS, IN, ANY quantify 연산자에 사용할 수 있으며, NOT EXISTS, NOT IN, ALL quantify 연산자에는 사용할 수 없다.

NL_SJ hint는 해당 subquery를 semi join 형태로 풀어내기 때문에 anti-semi join 형태로만 풀릴 수 있는 subquery에 기술한 경우 optimizer가 이 hint를 무시한다.

다음은 NL_SJ hint를 이용하여 subquery를 join 형태로 풀어낸 예이다.

- 유형 1: IN subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ NL_SJ */ I1
                 FROM T2 );
```

- 유형 2: EXISTS subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE EXISTS ( SELECT /*+ NL_SJ */ I1
                  FROM T2
                 WHERE T1.I1 = T2.I1 );
```

- 유형 3: Quantify 연산자의 subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 < ANY ( SELECT /*+ NL_SJ */ I1
                    FROM T2 );
```

- 유형 4: NOT IN subquery에 사용한 경우  
  (anti-semi join으로 풀 수 있는 연산자이므로 hint가 무시됨)

```
SELECT *
  FROM T1
 WHERE I1 NOT IN ( SELECT /*+ NL_SJ */ I1
                     FROM T2 );
```

<a id="262914dea2f5528a"></a>
###### **NL_ISJ**

Optimizer로 하여금 subquery를 nested loops inverted semi join으로 처리하도록 한다. 이는 subquery를 동일한 결과를 갖는 inverted semi join 형태로 풀어낸다.

Inverted semi join은 right node (inner node)에 semi join을 위한 key를 unique sort key로 갖는 sort instant를 생성하여 역으로 left node (outer node)에서 해당 key와 일치하는 레코드를 찾는 semi join 방법이다.

NL_ISJ hint는 right node (inner node)가 semi join을 위한 key와 많이 중복되고, left node (outer node)에서 해당 key로 index scan을 할 수 있는 경우에 유용하다. Optimizer는 semi join을 위한 key를 left node (outer node)에서 index scan 할 수 없는 경우에 hint를 무시한다. 또한, semi join을 위한 key를 key compare 할 수 없는 경우에도 이 hint를 무시한다.

NL_ISJ는 EXISTS, IN, = ANY quantify 연산자에 사용할 수 있고 NOT EXISTS, NOT IN, ALL quantify 연산자 또는 = ANY를 제외한 ANY quantify 연산자에는 사용할 수 없다.

NL_ISJ hint는 해당 subquery를 semi join 형태로 풀어내기 때문에 anti-semi join 형태로만 풀릴 수 있는 subquery에 기술한 경우, optimizer가 이 hint를 무시한다.

다음은 NL_ISJ hint를 이용하여 subquery를 join 형태로 풀어낸 예이다.

- 유형 1: IN subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ NL_ISJ */ I1
                 FROM T2 );
```

- 유형 2: EXISTS subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE EXISTS ( SELECT /*+ NL_ISJ */ I1
                  FROM T2
                 WHERE T1.I1 = T2.I1 );
```

- 유형 3: Quantify 연산자의 subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 = ANY ( SELECT /*+ NL_ISJ */ I1
                    FROM T2 );
```

- 유형 4: NOT IN subquery에 사용한 경우  
  (anti-semi join으로 풀 수 있는 연산자이므로 hint가 무시됨)

```
SELECT *
  FROM T1
 WHERE I1 NOT IN ( SELECT /*+ NL_ISJ */ I1
                     FROM T2 );
```

<a id="22f2ef9f012001a9"></a>
###### **MERGE_SJ**

Optimizer로 하여금 subquery를 merge semi join으로 처리하도록 한다. 이는 subquery를 동일한 결과를 갖는 semi join 형태로 풀어낸다.

MERGE_SJ는 EXISTS, IN, = ANY quantify 연산자에 사용할 수 있고 NOT EXISTS, NOT IN, ALL quantify 연산자, = ANY를 제외한 ANY quantify 연산자에는 사용할 수 없다.

MERGE_SJ hint는 해당 subquery를 semi join 형태로 풀어내기 때문에 anti-semi join 형태로만 풀릴 수 있는 subquery에 기술한 경우, optimizer가 이 hint를 무시한다. 또한, merge semi join에 사용할 key를 key compare 할 수 없는 경우에도 optimizer가 이 hint를 무시한다.

다음은 MERGE_SJ hint를 이용하여 subquery를 join 형태로 풀어낸 예이다.

- 유형 1: IN subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ MERGE_SJ */ I1
                 FROM T2 );
```

- 유형 2: EXISTS subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE EXISTS ( SELECT /*+ MERGE_SJ */ I1
                  FROM T2
                 WHERE T1.I1 = T2.I1 );
```

- 유형 3: Quantify 연산자의 subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 = ANY ( SELECT /*+ MERGE_SJ */ I1
                    FROM T2 );
```

- 유형 4: NOT IN subquery에 사용한 경우  
  (anti-semi join으로 풀 수 있는 연산자이므로 hint가 무시됨)

```
SELECT *
  FROM T1
 WHERE I1 NOT IN ( SELECT /*+ MERGE_SJ */ I1
                     FROM T2 );
```

<a id="0bf0dfeac9cab4ee"></a>
###### **HASH_SJ**

Optimizer로 하여금 subquery를 hash semi join으로 처리하도록 한다. 이는 subquery를 동일한 결과를 갖는 semi join 형태로 풀어낸다.

HASH_SJ는 EXISTS, IN, = ANY quantify 연산자에 사용할 수 있고 NOT EXISTS, NOT IN, ALL quantify 연산자, = ANY를 제외한 ANY quantify 연산자에는 사용할 수 없다.

HASH_SJ hint는 해당 subquery를 semi join 형태로 풀어내기 때문에 anti-semi join 형태로만 풀릴 수 있는 subquery에 기술한 경우 optimizer가 이 hint를 무시한다. 또한, hash semi join에 사용할 key를 key compare 할 수 없는 경우에도 optimizer가 이 hint를 무시한다.

다음은 HASH_SJ hint를 이용하여 subquery를 join 형태로 풀어낸 예이다.

- 유형 1: IN subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ HASH_SJ */ I1
                 FROM T2 );
```

- 유형 2: EXISTS subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE EXISTS ( SELECT /*+ HASH_SJ */ I1
                  FROM T2
                 WHERE T1.I1 = T2.I1 );
```

- 유형 3: Quantify 연산자의 subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 = ANY ( SELECT /*+ HASH_SJ */ I1
                    FROM T2 );
```

- 유형 4: NOT IN subquery에 사용한 경우  
  (anti-semi join으로 풀 수 있는 연산자이므로 hint가 무시됨)

```
SELECT *
  FROM T1
 WHERE I1 NOT IN ( SELECT /*+ HASH_SJ */ I1
                     FROM T2 );
```

<a id="48eddd50aaebdc97"></a>
###### **HASH_ISJ**

Optimizer로 하여금 subquery를 hash inverted semi join으로 처리하도록 한다. 이는 subquery를 동일한 결과를 갖는 inverted semi join 형태로 풀어낸다.

HASH_ISJ hint는 left node (outer node)의 row 개수가 적고, right node (inner node)의 row 개수가 많은 경우에 유용하다. Optimizer는 semi join을 위한 key를 key compare 할 수 없는 경우에 이 hint를 무시한다.

HASH_ISJ는 EXISTS, IN, = ANY quantify 연산자에 사용할 수 있고 NOT EXISTS, NOT IN, ALL quantify 연산자 및 = ANY를 제외한 ANY quantify 연산자에는 사용할 수 없다.

HASH_ISJ hint는 해당 subquery를 semi join 형태로 풀어내기 때문에 anti-semi join 형태로만 풀릴 수 있는 subquery에 기술한 경우 optimizer가 이 hint를 무시한다. 또한, hash semi join에 사용할 key를 key compare 할 수 없는 경우에도 optimizer가 이 hint를 무시한다.

다음은 HASH_ISJ hint를 이용하여 subquery를 join 형태로 풀어낸 예이다.

- 유형 1: IN subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ HASH_ISJ */ I1
                 FROM T2 );
```

- 유형 2: EXISTS subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE EXISTS ( SELECT /*+ HASH_ISJ */ I1
                  FROM T2
                 WHERE T1.I1 = T2.I1 );
```

- 유형 3: Quantify 연산자의 subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 = ANY ( SELECT /*+ HASH_ISJ */ I1
                    FROM T2 );
```

- 유형 4: NOT IN subquery에 사용한 경우  
  (anti-semi join으로 풀 수 있는 연산자이므로 hint가 무시됨)

```
SELECT *
  FROM T1
 WHERE I1 NOT IN ( SELECT /*+ HASH_ISJ */ I1
                     FROM T2 );
```

<a id="a6a526bf66159ce0"></a>
###### **HASH_AJ**

Optimizer로 하여금 subquery를 hash anti-semi join으로 처리하도록 한다. 이는 subquery를 동일한 결과를 갖는 anti-semi join 형태로 풀어낸다.

HASH_AJ는 NOT EXISTS, NOT IN, != ALL quantify 연산자에 사용할 수 있고 EXISTS, IN, ANY quantify 연산자, != ALL quantify 연산자를 제외한 ALL quantify 연산자에는 사용할 수 없다.

HASH_AJ hint는 해당 subquery를 anti-semi join 형태로 풀어내기 때문에 semi join 형태로만 풀릴 수 있는 subquery에 기술한 경우 optimizer가 이 hint를 무시한다. 또한, hash semi join에 사용할 key를 key compare 할 수 없는 경우에도 optimizer가 이 hint를 무시한다.

다음은 HASH_AJ hint를 이용하여 subquery를 join 형태로 풀어낸 예이다.

- 유형 1: NOT IN subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 NOT IN ( SELECT /*+ HASH_AJ */ I1
                     FROM T2 );
```

- 유형 2: NOT EXISTS subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE NOT EXISTS ( SELECT /*+ HASH_AJ */ I1
                      FROM T2
                     WHERE T1.I1 = T2.I1 );
```

- 유형 3: Quantify 연산자의 subquery에 사용한 경우

```
SELECT *
  FROM T1
 WHERE I1 != ALL ( SELECT /*+ HASH_AJ */ I1
                     FROM T2 );
```

- 유형 4: IN subquery에 사용한 경우  
  (semi join으로 풀 수 있는 연산자이므로 hint가 무시됨)

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ HASH_AJ */ I1
                 FROM T2 );
```

<a id="ed7dec3e7e8c9620"></a>
###### **TRANSITIVE_CLOSURE**

A=B 이고 B = C 이면, A=C 이다. 이와 같은 관계를 join predicate에 적용한다.

- 'T1.i1 = T2.i1'과 'T2.i1 = T3.i1'이 'T1.i1 = T3.i1' predicate을 생성한다.  
  하지만 join ordering에 사용되지 않을 경우, 자동으로 삭제 된다.

```
SELECT *
  FROM T1, T2, T3
 WHERE T1.i1 = T2.i1 AND T2.i1 = T3.i1;
```

위 예제에서 join ordering이 ((t1 ⋈ t2) ⋈ t3)일 경우, 'T2.i1 = T3.i1'과 'T1.i1 = T3.i1' 중 선택도가 높은 predicate 하나만 선택된다. Join ordering이 ((t1 ⋈ t3) ⋈ t2)일 경우, 'T1.i1 = T2.i1'과 'T2.i1 = T3.i1' 중 선택도가 높은 predicate 하나만 선택된다.

<a id="04bc545431e03d74"></a>
###### **NO_TRANSITIVE_CLOSURE**

Join transitive closure를 join predicate에 적용하지 않는다.

- 'T1.i1 = T2.i1'과 'T2.i1 = T3.i1'이 'T1.i1 = T3.i1' predicate을 생성하지 않는다.

```
SELECT *
  FROM T1, T2, T3
 WHERE T1.i1 = T2.i1 AND T2.i1 = T3.i1;
```

Join transitive closure가 적용되지 않으므로 'T1.i1 = T3.i1'인 predicate이 없다. 따라서 ((t1 ⋈ t3) ⋈ t2) 과 같은 join ordering이 발생하지 않는다.

<a id="840159e068b8b444"></a>
###### **MERGE**

기술한 view가 simple view merging이 가능하면 이를 적용하도록 optimizer에 지시한다. 이 hint는 기술한 view를 포함하는 상위 query block에 명시해야 한다.

MERGE hint는 &lt;join order hints&gt;, &lt;join operation hints&gt;, &lt;other hints&gt;, TRANSITIVE_CLOSURE/NO_TRANSITIVE hint, NO MERGE hint와 함께 쓰이면 적용 방법이 모호해진다.

따라서 이들 hint들과 MERGE hint가 함께 쓰였을 경우, "hint_error" property가 on 이면 validation error로 처리되며, off 이면 먼저 기술한 hint가 적용된다.

다음은 MERGE hint를 이용하여 simple view merging을 적용한 예이다.

- 유형 1: 하나의 view에 MERGE hint를 기술한 경우, v1이 simple view merging 된다.

```
SELECT /*+ MERGE(v1) */ *
  FROM ( SELECT * FROM t1 ) v1;
```

- 유형 2: 여러 개의 view에 MERGE hint를 기술한 경우, v1, v2만 simple view merging 되고, v3는 simple view merging 되지 않는다.

```
SELECT /*+ MERGE(v1) MERGE(v2) NO_MERGE(v3) */ *
  FROM ( SELECT i1 FROM t1 ) v1, 
       ( SELECT i1 FROM t2 ) v2,     
       ( SELECT i1 FROM t3 ) v3
 WHERE v1.i1 = v2.i1 AND v2.i1 = v3.i1;
```

- 유형 3: &lt;join order hints&gt;와 함께 기술할 경우, simple view merging하면 t3와 t4의 적용 순서와 방향이 모호해진다. 따라서 먼저 명시된 hint 만 적용되고 simple view merging은 수행되지 않는다.

```
SELECT /*+ ORDERING( t1, t2, v1 RIGHT ) MERGE(v1) */ *
  FROM t1, 
       t2,
       ( SELECT * FROM t3, t4 WHERE t3.i1 = t4.i1 ) v1
 WHERE t1.i1 = t2.i1 AND t2.i1 = v1.i1;
→
```

- 유형 4: &lt;join operation hints&gt;와 함께 기술한 경우, simple view merging 하면 hashing 대상 view가 사라진다. 따라서 먼저 명시된 hint만이 적용되고 simple view merging은 수행되지 않는다.

```
SELECT /*+ USE_HASH(v1) MERGE(v1) */ *
  FROM t1, 
       t2,
       ( SELECT * FROM t3, t4 WHERE t3.i1 = t4.i1 ) v1
 WHERE t1.i1 = t2.i1 AND t2.i1 = v1.i1;
```

- 유형 5: &lt;other hints&gt;와 함께 기술할 경우, simple view merging 할 때 view와 상위 query 사이의 other hints 처리가 서로 충돌한다. 따라서 먼저 명시된 hint만 적용되고 simple view merging은 수행되지 않는다.

```
SELECT /*+ PUSH_PRED MERGE(v1) */ *
  FROM ( SELECT /*+ NO_PUSH_PRED */ * FROM t1 WHERE t1.i1 = 1 ) v1
 WHERE v1.i1 = 1;
```

- 유형 6: TRANSITIVE CLOSUE hint와 함께 기술할 경우, simple view merging 할 때 view와 상위 query사이의 other hints 처리가 서로 충돌한다. 따라서 먼저 명시된 hint만이 적용되고 simple view merging은 수행되지 않는다.

```
SELECT /*+ TRANSITIVE_CLOSURE MERGE(v1) */ *
  FROM ( SELECT /*+ NO_TRANSITIVE_CLOSURE */ * 
           FROM t1, t2, t3
          WHERE t1.i1 = t2.i1 AND t2.i1 = t3.i1 ) v1;
```

<a id="312ab6c2d742264b"></a>
###### **NO_MERGE**

기술한 view를 simple view merging 할 수 있더라도 optimizer로 하여금 이를 적용하지 않도록 한다. 이 hint는 기술한 view를 포함하는 상위 query block에 명시해야 한다.

NO_MERGE hint가 &lt;join order hints&gt;, &lt;join operation hints&gt;, &lt;other hints&gt;, TRANSITIVE_CLOSURE/ NO_TRANSITIVE hint, MERGE hint와 함께 쓰일 경우 적용 방법이 모호해진다.

따라서 이들 hint와 NO_MERGE hint가 함께 쓰였을 경우, "hint_error" property가 on 이면 validation error로 처리되고 off 이면 먼저 기술한 hint가 적용된다.

다음은 NO_MERGE hint를 이용하여 simple view merging을 적용하지 않도록 하는 예이다.

- 유형 1: 하나의 view에 NO_MERGE hint를 기술한 경우, v1이 simple view merging 되지 않는다.

```
SELECT /*+ NO_MERGE(v1) */ *
  FROM ( SELECT * FROM t1 ) v1;
```

- 유형 2: 여러 개의 view에 NO_MERGE hint를 기술한 경우, v1, v2만 simple view merging 되고, v3는 simple view merging 되지 않는다.

```
SELECT /*+ MERGE(v1) MERGE(v2) NO_MERGE(v3) */ *
  FROM ( SELECT i1 FROM t1 ) v1, 
       ( SELECT i1 FROM t2 ) v2,     
       ( SELECT i1 FROM t3 ) v3
 WHERE v1.i1 = v2.i1 AND v2.i1 = v3.i1;
```

<a id="be6b057845f1b976"></a>
###### **NO_QUERY_TRANSFORMATION**

Optimizer가 query를 변경하지 않도록 한다. 이 hint를 기술하면 heuristic optimizer나 cost based optimizer 등에서 최적의 성능을 위해 optimizer가 query를 변형하는 과정들이 전혀 수행되지 않는다.

NO_QUERY_TRANSFORMATION hint는 최상위 레벨의 query나 subquery에 기술할 수 있으며, 기술한 query 뿐만 아니라 그 하위의 subquery 모두에 대하여 적용된다

다음은 NO_QUERY_TRANSFORMATION을 이용하여 query를 변형하지 못하도록 한 예이다.

- 유형 1: Subquery에 NO_QUERY_TRANSFORMATION hint를 사용한 경우  
  (Subquery의 query만 변경하지 않음)

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ NO_QUERY_TRANSFORMATION */ I1
                 FROM T2 );
```

- 유형 2: 최상위 query에 NO_QUERY_TRANSFORMATION hint를 사용한 경우  
  (최상위 query와 subquery의 모든 query를 변경하지 않음)

```
SELECT /*+ NO_QUERY_TRANSFORMATION */ *
  FROM T1
 WHERE I1 IN ( SELECT I1
                 FROM T2 );
```

- 유형 3: 최상위 query에 NO_QUERY_TRANSFORMATION hint를 사용하고 subquery에 UNNEST hint를 사용한 경우   
  (Subquery의 UNNEST hint를 무시함)

```
SELECT /*+ NO_QUERY_TRANSFORMATION */ *
  FROM T1
 WHERE I1 IN ( SELECT /*+ UNNEST */ I1
                 FROM T2 );
```

<a id="28e0ee4effb0cded"></a>
##### &lt;other_hints&gt;

<a id="c2d93f321659391b"></a>
###### **PUSH_PRED**

Optimizer로 하여금 single table에 적용 가능한 filter들을 push하도록 한다. 이 hint는 해당 select 구문의 적용 가능한 filter를 single table에 push하여 선행 처리하도록 한다. 해당 힌트는 select로 시작되는 SubQuery들에도 각각 기술할 수 있으며, 각 질의 block 내에서만 적용되고, 하위 SubQuery로 확산되지 않는다.

각 SubQuery들에는 독립적으로 이 힌트를 기술할 수 있으며, 기술하지 않으면 default 값이 적용된다. Default 값은 PUSH_PRED이다.

다음은 PUSH_PRED hint를 이용하여 subquery를 push하는 예이다.

- T1.i1 = 1을 T1 table에 push 하는 경우

```
SELECT /*+ PUSH_PRED */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1
   AND T1.I1 = 1;
```

<a id="b40a733dac192781"></a>
###### **NO_PUSH_PRED**

Optimizer로 하여금 single table에 적용 가능한 filter들을 push하지 못하도록 한다. 이 hint는 해당 select 구문의 적용 가능한 filter를 single table에 push하여 선행 처리되는 것을 막는다. 해당 힌트는 select로 시작되는 SubQuery들에도 각각 기술할 수 있으며, 각 질의 block 내에서만 적용되고, 하위 SubQuery로 확산되지 않는다.

각 SubQuery들에는 독립적으로 이 힌트를 기술할 수 있으며, 기술하지 않으면 default 값이 적용된다. Default 값은 PUSH_PRED이다.

이 hint를 기술했을 때 from절에 join이 존재할 경우, 해당 필터를 처리할 수 있는 가장 하위 join에서 처리된다. 즉, 해당 filter를 처리할 수 있는 single table에서 선행 처리 되는 것을 방지한다. 또한, 이 hint를 기술했을 때 from절에 view가 존재할 경우, 해당 view의 하위로 filter가 push되지 않는다.

다음은 NO_PUSH_PRED hint를 이용하여 filter를 push하는 예이다.

- 유형 1: T1과 T2를 join한 후에 T1.i1 = 1을 수행한다.

```
SELECT /*+ NO_PUSH_PRED */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1
   AND T1.I1 = 1;
```

- 유형 2: View A를 처리한 후에 A.i1 = 1을 수행한다.

```
SELECT /*+ NO_PUSH_PRED */ *
  FROM (SELECT I1 FROM T1) AS A
 WHERE A.I1 = 1;
```

<a id="0fd5a268f6250c12"></a>
###### **PUSH_SUBQ**

Optimizer로 하여금 subquery의 적용 가능한 최하위 노드까지 push하도록 한다. 이 hint는 subquery 상위 레벨의 query가 join으로 구성되어 있을 때 해당 join node 구조의 최상위 node부터 최하위 노드까지 탐색하여 해당 subquery를 처리할 수 있는 node를 찾아서 push 가능한 가장 하위 node에서 subquery를 처리하도록 한다.

PUSH_SUBQ hint는 subquery에만 기술할 수 있으며, 다수의 subquery가 존재할 경우, PUSH_SUBQ hint를 subquery마다 각각 기술해야 한다.

PUSH_SUBQ hint를 기술하지 않으면 optimizer가 cost를 계산하여 가장 cost가 좋은 node에 subquery를 push한다.

다음은 PUSH_SUBQ hint를 이용하여 subquery를 push하는 예이다.

- 유형 1: Subquery를 T1 table에 push 하는 경우

```
SELECT *
  FROM T1, T2
 WHERE T1.I1 = T2.I1
   AND T1.I1 IN ( SELECT /*+ PUSH_SUBQ */ I1
                    FROM T3 );
```

- 유형 2: Subquery를 최상위 node에서만 처리할 수 있는 경우  
  (Subquery를 하위 노드로 push하지 못함)

```
SELECT *
  FROM T1, T2
 WHERE T1.I1 = T2.I1
   AND T1.I1 IN ( SELECT /*+ PUSH_SUBQ */ I1
                    FROM T3
                   WHERE T3.I2 = T1.I2
                     AND T3.I3 = T2.I3 );
```

<a id="f42af91afe2ab5f0"></a>
###### **NO_PUSH_SUBQ**

Optimizer로 하여금 subquery를 하위 노드로 push하지 못하도록 한다. 이 hint는 subquery의 상위 레벨 query가 join으로 구성되어 있을 때 해당 join node 구조의 최상위 node에서 subquery를 처리하도록 한다.

NO_PUSH_SUBQ hint는 subquery에만 기술할 수 있으며, 다수의 subquery가 존재할 경우, NO_PUSH_SUBQ hint를 subquery마다 각각 기술해야 한다.

NO_PUSH_SUBQ hint를 기술하지 않으면 optimizer가 cost를 계산하여 가장 cost가 좋은 node에 subquery를 push한다.

다음은 NO_PUSH_SUBQ hint를 이용하여 subquery를 push하는 예이다.

- T1 table에서 처리 가능한 subquery에 NO_PUSH_SUBQ hint를 사용한 경우  
  (T1 table과 T2 table을 join한 후에 subquery를 수행함)

```
SELECT *
  FROM T1, T2
 WHERE T1.I1 = T2.I1
   AND T1.I1 IN ( SELECT /*+ NO_PUSH_SUBQ */ I1
                    FROM T3 );
```

<a id="986e4380d34f44ff"></a>
###### **USE_GROUP_HASH**

Group by 절이 있는 경우에 grouping 하기 위해 optimizer로 하여금 hash instant를 사용하도록 한다.

USE_GROUP_HASH hint는 group by 절이 있는 구문에만 기술할 수 있으며, 다수의 subquery가 존재할 경우 subquery마다 각각 기술해야 한다.

USE_GROUP_HASH hint를 사용하지 않고 grouping을 위한 group key들이 하위 노드로부터 정렬된 상태일 때는 group node를 사용하는 방법을 고려해야 한다.

다음은 USE_GROUP_HASH hint를 이용하는 예이다.

- T1 table에 group key들로 구성된 index가 존재할 때 USE_GROUP_HASH를 사용한 경우

```
SELECT /*+ USE_GROUP_HASH */ *
  FROM T1
 GROUP BY I1;
```

<a id="b5708d5e61770cfa"></a>
###### **USE_DISTINCT_HASH**

Distinct 절이 있는 경우에 distinct를 수행하기 위해 optimizer로 하여금 hash instant를 사용하도록 한다.

USE_DISTINCT_HASH hint는 group by 절이 있는 구문에만 기술할 수 있으며, 다수의 subquery가 존재할경우 subquery마다 각각 기술해야 한다.

USE_DISTINCT_HASH hint를 사용하지 않고 distinct를 위한 distinct key들이 하위 노드로부터 정렬된 상태일 때는 group node를 사용하는 방법을 고려해야 한다.

다음은 USE_DISTINCT_HASH hint를 이용하는 예이다.

- T1 table에 distinct key들로 구성된 index가 존재할 때 USE_DISTINCT_HASH를 사용한 경우

```
SELECT /*+ USE_DISTINCT_HASH */ I1, I2
  FROM T1;
```

<a id="27e42664eae41b08"></a>
#### 설명

Hint는 사용자가 GOLDILOCKS optimizer에게 SQL 구문을 수행하는 방법을 직접 지시하기 위하여 사용하는 comment이다. GOLDILOCKS optimizer가 실행 계획을 정확히 판단할 수 없는 경우에 사용자가 hint를 사용하여 직접 실행 계획을 선택한다.

GOLDILOCKS optimizer가 실행 계획을 결정할 때는 사용자가 기술한 hint를 최우선으로 선택하게 되며, 만약 사용자가 기술한 hint를 사용할 수 없을 경우 GOLDILOCKS optimizer가 판단해서 결정한다.

사용자가 hint를 사용하면 GOLDILOCKS optimizer가 가능한 사용자의 hint대로 동작하기 때문에 사용자가 GOLDILOCKS optimizer의 SQL구문 실행 계획이 잘못되었다고 판단하는 경우에만 사용할 것을 권장한다.

특히, 동일한 SQL 구문을 반복해서 사용할 때 hint를 사용하면 GOLDILOCKS optimizer는 사용자가 기술한 hint대로 수행한다. 이 경우, 해당 SQL 구문에 포함된 TABLE이나 VIEW의 데이터가 변경되어 다른 실행 계획의 성능 저하를 가져올 수 있으므로 주의한다.

GOLDILOCKS에서 hint는 SELECT, INSERT SELECT, DELETE, UPDATE 등의 구문에 사용할 수 있다. Hint는 각 구문의 키워드 다음 위치에 /*+ 키워드와 */ 키워드를 양 옆에 사용하여 그 사이에 기술한다.

사용자가 잘못된 hint를 기술하거나 동일한 실행 계획에 영향을 미치는 hint를 둘 이상 기술하여 hint가 서로 충돌하는 경우에는 해당 hint를 무시하거나 먼저 기술된 hint를 우선 적용한다. Hint가 잘못 기술되었는지 알고 싶다면 ALTER 구문을 이용하여 HINT_ERROR property를 on으로 설정하고 이용하면 된다.

<a id="ea37803696df5664"></a>
#### 사용 예

다음은 INSERT SELECT, DELETE, UPDATE, SELECT 구문에서 &lt;hint clause&gt;를 사용한 예이다.

- INSERT SELECT 구문에서 사용한 경우

```
gSQL> INSERT INTO T1 SELECT /*+ INDEX(T1, T1_IDX) */ * FROM T1;

1 row created.
```

- SELECT 구문에서 사용한 경우

```
gSQL> SELECT /*+ INDEX(T1, T1_IDX) */ * FROM T1;

I1
--
 1
 1

2 rows selected.
```

- UPDATE 구문에서 사용한 경우

```
gSQL> UPDATE /*+ INDEX(T1, T1_IDX) */ T1 SET I1 = 2;

2 rows updated.
```

- DELETE 구문에서 사용한 경우

```
gSQL> DELETE /*+ INDEX(T1, T1_IDX) */ T1 WHERE I1 = 2;

2 rows deleted.
```

다음은 ALTER 구문을 이용하여 HINT_ERROR property를 on으로 변경한 후에 hint를 잘못 사용한 예이다.

```
gSQL> ALTER SESSION SET HINT_ERROR = ON;

Session altered.

gSQL> SELECT /*+ INDEX(T2, T1_IDX) */ * FROM T1;

ERR-42000(16058): not applicable hint :
SELECT /*+ INDEX(T2, T1_IDX) */ * FROM T1
           *
ERROR at line 1:
```

<a id="821412ebb69aac57"></a>
#### 호환성

SQL 표준에서는 hint를 정의하지 않고 있으며, Oracle 등의 타 벤더에서는 각각 독립적인 형태로 hint를 지원하고 있다.

GOLDILOCKS에서 제공하는 hint는 대부분 Oracle에서 제공하는 hint와 호환되며, GOLDILOCKS에서 제공하는 hint와 동일한 Oracle hint 구문은 Oracle에서도 동일하게 동작한다. 단, INDEX_COMBINE hint는 Oracle과 다른 의미이며 ORDERING hint는 Oracle에서 제공하지 않는다.

<a id="7c885b96ecc9769d"></a>
#### 참조

관련 내용은 [query specification](#d8630e2bdbb32181)을 참조한다.

<a id="3d47d4f6b916da0d"></a>
## SELECT .. FOR UPDATE

<a id="fa9609727617b2e2"></a>
### 기능

SELECT 구문의 결과 집합을 갱신할지 여부를 설정한다.

<a id="add1acba9b72fb6a"></a>
### 구문

```
<select for update statement> ::=
    <query expression>  <updatability clause>
    ;

<updatability clause> ::=
      FOR READ ONLY 
    | FOR UPDATE [ OF <column name list> ] [ <lock wait mode> ]

<lock wait mode> ::=
    | WAIT
    | WAIT second
    | NOWAIT
```

<a id="8eeb4b651ed0f9c7"></a>
### 사용 범위 및 접근 권한

&lt;select for update statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- &lt;query expression&gt; 구문을 수행하려면 구문에 사용된 모든 테이블에 대한 다음 권한 중 하나가 사용자에게 있어야 한다.
    - 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

- FOR UPDATE 구문을 사용할 경우, lock 대상이 되는 테이블에 대한 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (LOCK 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (LOCK TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - LOCK ANY TABLE ON DATABASE

<a id="6ad3f09a042b9bcd"></a>
### 구문 규칙 및 파라미터

<a id="4454264376704e1e"></a>
#### &lt;query expression&gt;

SELECT 구문에 INTO 절이 없어야 한다.

FOR UPDATE를 사용하려면 query가 base table의 row 변화를 식별하거나 row에 lock을 획득할 수 있는 updatable query여야 한다.

Updatable query는 다음 조건을 모두 만족해야 한다.

- 최상위 query에 DISTINCT가 존재하지 않아야 한다.
    - (X) SELECT DISTINCT * FROM t1; 
- 최상위 query에 GROUP BY, HAVING, aggregation function이 존재하지 않아야 한다.
    - (X) SELECT MAX(c1) FROM t1; 
- Set 연산자가 존재하지 않아야 한다. 
    - (X) SELECT * FROM t1 UNION ALL SELECT * FROM t2; 
- FROM 절에 나열된 table 들에 하나 이상의 updatable column이 존재해야 한다. 
    - Join에 포함되는 테이블 중 cross join에 해당되지 않는 테이블의 column은 updatable column이 아니다. 
        - FULL OUTER JOIN은 cross join이 아니다. 
        - NATURAL JOIN 은 cross join이 아니다. 
        - INNER JOIN에 USING 구문이 사용된 경우 cross join이 아니다. 
    - 다음과 같은 table들의 column은 updatable column이 아니다. 
        - Dictionary table, fixed table, performance view 
    - View의 column은 updatable table이 아니다.

SELECT 구문에 대한 자세한 내용은 [query expression](#1c4140d8d3200490)을 참조한다.

<a id="87aea3d140fc5bce"></a>
#### &lt;updatability clause&gt;

결과 집합에 대한 row를 변경할지 여부를 지정한다.

- FOR READ ONLY 
    - 읽기 전용 질의임을 선언한다. 
- FOR UPDATE 
    - 쓰기 가능한 질의임를 선언한다. 
    - 질의를 수행할 때 해당 트랜잭션이 종료될 때까지 다른 트랜잭션에 의해 변경되지 않도록 해당 row 들에 대한 x lock을 획득한다. 
    - &lt;query expression&gt;이 updatable query 여야 한다.

<a id="6bb827c8eeb9177c"></a>
#### FOR UPDATE OF …

질의를 수행할 때 lock 획득과 관련된 column들을 나열한다.

- FOR UPDATE OF 구문에 나열하는 column 
    - &lt;query expression&gt;의 FROM 절에 나열된 table의 갱신 가능한 column이어야 한다. 
    - 나열된 column의 table에 대해 lock을 획득한다. 
- FOR UPDATE만 사용하는 경우 
    - &lt;query expression&gt;의 FROM 절에 나열된 table들의 모든 갱신 가능한 column을 나열한 것과 동일한 의미이다. 
    - 모든 column의 table에 대해 lock을 획득한다.

<a id="460fb79655b9042c"></a>
#### &lt;lock wait mode&gt;

FOR UPDATE 구문과 함께 사용하며, lock 획득 방법을 지정한다.

- WAIT 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock을 획득하며 
    - Lock을 획득할 때까지 대기한다. 
- WAIT second 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock을 획득하며 
    - 지정한 시간동안 lock을 획득하지 못하면 에러가 발생한다. 
    - 초 단위이며 0 ~ 1000000000 까지의 값을 사용할 수 있다. 
- NOWAIT 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock을 획득하며 
    - 즉시 lock을 획득하지 못하면 에러가 발생한다.
- 명시하지 않을 경우, 기본값은 WAIT이다.

<a id="81eba09153e6f39f"></a>
### 설명

SELECT 구문은 transaction의 종료 여부와 관계없이 row에 대한 fetch를 지속할 수 있는 반면에, SELECT .. FOR UPDATE 구문은 row들에 대한 lock을 획득하기 때문에 transaction이 종료되면 fetch 할 수 없다.

> Cursor holdability  
>   
> • WITH HOLD  
>  ° Transaction 종료 여부와 관계없이 fetch를 지속할 수 있다.  
>  ° Fetch across commit 이라고도 한다.  
>   
> • WITHOUT HOLD  
>  ° Transaction이 종료되면 fetch 할 수 없다.

<a id="30fcf555e02a11af"></a>
### 사용 예

다음은 FOR UPDATE 구문을 사용하여 row에 대한 lock을 획득하는 예이다.

```
gSQL> SELECT id, data FROM t1 WHERE id = 3 FOR UPDATE;

ID DATA  
-- ------
 3 data_3

1 row selected.
```

다음과 같이 join과 ORDER BY 구문을 사용하더라도 updatable query이면 FOR UPDATE 구문을 사용할 수 있다.

```
gSQL> SELECT t1.id, t1.name, t2.addr 
        FROM t1, t2
       WHERE t1.id = t2.id
       ORDER BY 1
         FOR UPDATE;

ID NAME    ADDR         
-- ------- -------------
 1 someone somewhere    
 2 anyone  anywhere     
 3 unknown N/A          
 4 leekmo  leekmo's home
 5 mkkim   seoul        

5 rows selected.
```

다음과 같이 updatable query가 아닌 경우에는 FOR UPDATE 구문을 사용할 수 없다.

```
gSQL> SELECT id, COUNT(*)
        FROM t1
       GROUP BY id
         FOR UPDATE;

ERR-42000(16112): query expression is not updatable
```

<a id="41204c921895b968"></a>
### 호환성

SQL 표준에서는 &lt;select for update statement&gt;를 정의하지 않고 있는데, 이는 [DECLARE cursor_name](#c0f5909b51d661a3) 구문을 사용하여 정의할 수 있다.

<a id="f1d3efe9cfddaa45"></a>
## SELECT .. INTO

<a id="858d38ae461e1c69"></a>
### 기능

질의를 통해 row 하나를 검색하고, 검색한 row의 값을 호스트 변수로 얻어온다.

<a id="6ab92fa6dee1e674"></a>
### 구문

```
<select statement: single row> ::=
    SELECT [ <hint clause> ] [ <set quantifier> ] <select list>
        INTO <select target list>
        <table expression>
    ;

<select target list> ::=
    variable_name [, ...]
```

<a id="942621a3fd2ac7af"></a>
### 사용 범위 및 접근 권한

&lt;select statement: single row&gt; 구문을 수행하려면 사용자가 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나를 가져야 한다.

- 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
- 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- SELECT ANY TABLE ON DATABASE

<a id="5c304a9172e743d7"></a>
### 구문 규칙 및 파라미터

<a id="e5cf0b487709f97f"></a>
#### &lt;hint clause&gt;

질의를 수행하기 위한 힌트를 기술한다.  
자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 [hint clause](#a12a3515f3dbcd31)를 참조한다.

<a id="4df2199461623dd1"></a>
#### &lt;set quantifier&gt;

질의 결과에서 중복을 제거할지 여부를 기술한다.  
자세한 내용은 [query specification](#d8630e2bdbb32181) 절을 참조한다.

<a id="79891e101cf0b248"></a>
#### &lt;select list&gt;

질의 결과로부터 검색할 column을 기술한다.  
자세한 내용은 [select list](#d37df5771ea1cca7) 절을 참조한다.

<a id="847b909391884b3f"></a>
#### INTO &lt;select target list&gt;

INTO 절에 기술된 변수의 개수는 &lt;select list&gt;에 기술된 expression의 개수와 동일해야 한다.

<a id="a9bdd149e8f5e307"></a>
#### &lt;table expression&gt;

검색 조건 등 질의 내용을 기술한다.  
자세한 내용은 [query specification](#d8630e2bdbb32181) 절을 참조한다.

<a id="defa3ec9828983de"></a>
### 설명

검색할 row가 한 건 이하여야 한다.  
두 건 이상의 row가 검색될 경우, 에러가 발생한다.

<a id="c6c1d9fb3753d2ac"></a>
#### SELECT 구문들의 차이점

- &lt;select statement&gt;
    - 조건에 부합하는 다수의 row를 검색하고, 검색한 row를 SQLFetch() 등의 API로 검색할 수 있다. 
    - 예: SELECT c1 FROM t1 WHERE c1 > 0; 
- &lt;select statement: single row&gt;
    - 조건에 부합하는 한 건 이하의 row를 검색할 수 있으며, 검색한 row가 한 건일 경우 INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: SELECT c2 INTO :v1 FROM t1 WHERE c1 = 0;

<a id="88b6f8f5c2610880"></a>
### 사용 예

다음은 interactive SQL (gsql)을 사용하여 host 변수에 값을 얻어오는 예이다.

```
gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> SELECT id, data INTO :v_id, :v_data FROM t1 WHERE id = 3;

V_ID V_DATA
---- ------
   3 data_3

1 row selected.
```

<a id="f1d497f1e71e509f"></a>
## SELECT .. INTO .. FOR UPDATE

<a id="281a2cdae0f95f01"></a>
### 기능

질의를 통해 row 하나를 검색하여 갱신을 수행할지 여부를 설정한 후, 검색한 row의 값을 호스트 변수에 얻어온다.

<a id="09f10cd65be73970"></a>
### 구문

```
<select for update statement: single row> ::=
    SELECT [ <hint clause> ] [ <set quantifier> ] <select list>
        INTO <select target list>
        <table expression>  <updatability clause>
    ;

<select target list> ::=
    variable_name [, ...]

<updatability clause> ::=
      FOR READ ONLY 
    | FOR UPDATE [ OF <column name list> ] [ <lock wait mode> ]

<lock wait mode> ::=
    | WAIT
    | WAIT second
    | NOWAIT
```

<a id="0fd39c029fd1483b"></a>
### 사용 범위 및 접근 권한

&lt;select statement: single row&gt; 구문을 수행하려면 사용자에게 구문에 사용된 모든 테이블에 대한 다음 권한 중 하나가 있어야 한다.

- 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
- 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- SELECT ANY TABLE ON DATABASE

FOR UPDATE 구문을 사용할 경우, lock 대상이 되는 테이블에 대해 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (LOCK 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (LOCK TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- LOCK ANY TABLE ON DATABASE

<a id="ba1ecc767ca091a3"></a>
### 구문 규칙 및 파라미터

<a id="62bffcb9e4270e2b"></a>
#### &lt;select for update statement: single row&gt;

FOR UPDATE를 사용하려면 query가 base table의 row 변화를 식별하거나 row에 lock을 획득할 수 있는 updatable query여야 한다.

Updatable query는 다음 조건을 모두 만족해야 한다.

- 최상위 query에 DISTINCT가 존재하지 않아야 한다.
    - (X) SELECT DISTINCT * FROM t1; 
- 최상위 query에 GROUP BY, HAVING, aggregation function이 존재하지 않아야 한다. 
    - (X) SELECT MAX(c1) FROM t1; 
- Set 연산자가 존재하지 않아야 한다. 
    - (X) SELECT * FROM t1 UNION ALL SELECT * FROM t2; 
- FROM 절에 나열된 table들에 하나 이상의 updatable column이 존재해야 한다. 
    - Join에 포함되는 테이블 중 cross join에 해당하지 않는 테이블의 column은 updatable column이 아니다. 
        - FULL OUTER JOIN은 cross join이 아니다. 
        - NATURAL JOIN은 cross join이 아니다. 
        - INNER JOIN에 USING 구문이 사용된 경우 cross join이 아니다. 
    - 다음과 같은 table들의 column은 updatable column이 아니다. 
        - Dictionary table, fixed table, performance view 
    - View의 column은 updatable table이 아니다.

<a id="5c5d8cf86b795e7b"></a>
#### &lt;updatability clause&gt;

결과 집합에 대해 row를 변경할지 여부를 지정한다.

- FOR READ ONLY 
    - 읽기 전용 질의임을 선언한다. 
- FOR UPDATE 
    - 쓰기 가능한 질의임를 선언한다. 
    - 질의를 수행할 때 해당 트랜잭션이 종료될 때까지, 다른 트랜잭션에 의해 변경되지 않도록 해당 row들에 대한 x lock을 획득한다. 
    - &lt;query expression&gt;이 updatable query이어야 한다.

<a id="93fca2eedbdf902f"></a>
#### FOR UPDATE OF …

질의를 수행할 때 lock 획득과 관련된 column을 나열한다.

- FOR UPDATE OF 구문에 나열하는 column 
    - &lt;query expression&gt;의 FROM 절에 나열된 table의 갱신 가능한 column이어야 한다. 
    - 나열된 column의 table에 대해 lock을 획득한다. 
- FOR UPDATE 만 사용하는 경우 
    - &lt;query expression&gt;의 FROM 절에 나열된 table들의 모든 갱신 가능한 column을 나열한 것과 동일한 의미이다. 
    - 모든 column의 table에 대해 lock을 획득한다.

<a id="cd68eb98b29a86c3"></a>
#### &lt;lock wait mode&gt;

FOR UPDATE 구문과 함께 사용하며, lock 획득 방법을 지정한다.

- WAIT 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock을 획득하며 
    - Lock을 획득할 수 있을 때까지 대기한다. 
- WAIT second 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock 을 획득하며 
    - 지정한 시간동안 lock을 획득할 수 없을 경우, 에러가 발생한다. 
    - 초 단위이며 0 ~ 1000000000 까지의 값을 사용할 수 있다. 
- NOWAIT 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock을 획득하며 
    - 즉시 lock을 획득할 수 없을 경우, 에러가 발생한다.
- 명시하지 않을 경우, 기본값은 WAIT 이다.

<a id="bee66bf88a3e9f82"></a>
#### &lt;hint clause&gt;

질의를 수행하기 위한 힌트를 기술한다.  
자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 [hint clause](#a12a3515f3dbcd31) 절을 참조한다.

<a id="33328b620f528e25"></a>
#### &lt;set quantifier&gt;

질의 결과에서 중복을 제거할지 여부를 기술한다.  
자세한 내용은 [query specification](#d8630e2bdbb32181) 절을 참조한다.

<a id="a95b5538f7f3127a"></a>
#### &lt;select list&gt;

질의 결과로부터 검색할 column을 기술한다.  
자세한 내용은 [select list](#d37df5771ea1cca7) 절을 참조한다.

<a id="c4d3e93a77f2d23c"></a>
#### INTO &lt;select target list&gt;

INTO 절에 기술된 변수의 개수는 &lt;select list&gt;에 기술된 expression의 개수와 동일해야 한다.

<a id="4f8da62cbbc75762"></a>
#### &lt;table expression&gt;

검색 조건 등의 질의 내용을 기술한다.  
자세한 내용은 [query specification](#d8630e2bdbb32181) 절을 참조한다.

<a id="75875ce19c323075"></a>
### 설명

검색할 row가 한 건 이하여야 한다.  
두 건 이상의 row가 검색될 경우, 에러가 발생한다.

SELECT 구문은 transaction의 종료 여부와 관계없이 row에 대한 fetch를 지속할 수 있는 반면에, SELECT .. FOR UPDATE 구문은 row들에 대한 lock을 획득하기 때문에 transaction이 종료되면 fetch 할 수 없다.

> Cursor holdability  
> 
> 
> - WITH HOLD
>     - Transaction 종료 여부와 관계없이 fetch를 지속할 수 있다.
>     - Fetch across commit 라고도 한다.
> 
> 
> 
> - WITHOUT HOLD
>     - Transaction이 종료되면 fetch 할 수 없다.
> 

<a id="81f6549ccb512954"></a>
#### SELECT 구문들의 차이점

- &lt;select for update statement&gt;
    - 조건에 부합하는 다수의 row를 검색하여 갱신 수행 여부를 설정하고, 검색한 row를 SQLFetch() 등의 API로 검색할 수 있다. 
    - 예: SELECT c1 FROM t1 WHERE c1 > 0 FOR UPDATE; 
- &lt;select for update statement: single row&gt;
    - 조건에 부합하는 한 건 이하의 row를 검색하여 갱신 수행 여부를 설정하고, 검색한 row가 한 건일 경우 INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: SELECT c2 INTO :v1 FROM t1 WHERE c1 = 0 FOR UPDATE;

<a id="495a0efebb06a3a2"></a>
### 사용 예

다음은 FOR UPDATE 구문을 사용하여 row에 lock을 획득하고, interactive SQL (gsql)을 사용하여 host 변수에 값을 얻어오는 예이다.

```
gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> SELECT id, data INTO :v_id, :v_data FROM t1 WHERE id = 3 FOR UPDATE;

V_ID V_DATA
---- ------
   3 data_3

1 row selected.
```

다음과 같이 join과 ORDER BY 구문을 사용하더라도 updatable query이면 FOR UPDATE 구문을 사용할 수 있다.

```
gSQL> \var v_id   INTEGER
gSQL> \var v_name VARCHAR(128)
gSQL> \var v_addr VARCHAR(128)


gSQL> SELECT t1.id, t1.name, t2.addr 
        INTO :v_id, :v_name, :v_addr
        FROM t1, t2
       WHERE t1.id = t2.id
       ORDER BY 1
       LIMIT 1
         FOR UPDATE;

ID NAME    ADDR         
-- ------- -------------
 1 someone somewhere    

1 row selected.
```

다음과 같이 updatable query가 아닌 경우에는 FOR UPDATE 구문을 사용할 수 없다.

```
gSQL> \var v_id    INTEGER
gSQL> \var v_count INTEGER

gSQL> SELECT id, COUNT(*)
        INTO :v_id, :v_count
        FROM t1
       GROUP BY id
         FOR UPDATE;

ERR-42000(16112): query expression is not updatable
```

<a id="12031ded28878a9a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [SELECT .. FOR UPDATE](#3d47d4f6b916da0d)
- [SELECT .. INTO](#f1d3efe9cfddaa45)

<a id="8e1fec980aea373d"></a>
## SET CONSTRAINTS

<a id="040e45bf99b8eb51"></a>
### 기능

트랜잭션 내에서 지연 가능한 제약 조건들의 검사 시점을 IMMEDIATE 또는 DEFERRED로 설정한다.

<a id="35653b9ce767e2ed"></a>
### 구문

```
<set constraints mode statement> ::=
    SET { CONSTRAINT | CONSTRAINTS } <constraint name list> { DEFERRED | IMMEDIATE }
    ;

<constraint name list> ::=
      ALL
    | <constraint name> [, ...]
```

<a id="69918f383403eb1a"></a>
### 사용 범위 및 접근 권한

SET CONSTRAINTS를 수행하기 위해 별도의 접근 권한이 필요한 것은 아니다.

> Cluster system에서 지원하지 않는다.

<a id="6ca534768085a43d"></a>
### 구문 규칙 및 파라미터

<a id="09975f77b8fb7972"></a>
#### CONSTRAINT | CONSTRAINTS

CONSTRAINT와 CONSTRAINTS는 동일한 의미의 키워드인데 SQL 표준은 CONSTRAINTS 이다.

<a id="6d3d47134dac6621"></a>
#### &lt;constraint name list&gt;

제약 조건 이름 목록을 기술하거나, ALL 키워드를 사용하여 지연 가능한 제약 조건을 모두 명시할 수 있다.  
&lt;constraint name&gt;을 기술할 경우, 제약 조건은 지연 가능해야 한다.  
ALL은 지연 가능한 모든 제약 조건을 의미한다.

<a id="8beff52cbc4a6d3f"></a>
#### DEFERRED | IMMEDIATE

명시된 지연 가능한 제약 조건들의 검사 시점을 설정한다.

- IMMEDIATE
    - DML을 수행할 때 해당 제약 조건들을 검사한다.
    - 트랜잭션이 해당 제약 조건들을 위반할 경우, 에러가 발생한다
- DEFERRED
    - COMMIT을 수행할 때 해당 제약 조건들을 검사한다.

트랜잭션이 진행 중이면, 검사 시점은 현재 트랜잭션에 설정되며, 트랜잭션이 진행 중이 아닌 경우에는 다음 트랜잭션에 설정된다.  
트랜잭션이 종료되면 다음 트랜잭션에 영향을 미치지 않는다.

<a id="e1765cfab3189e6f"></a>
### 설명

<a id="6f620aff48342338"></a>
#### 지연 가능한 제약 조건

지연 가능한 (DEFERRABLE) 제약 조건은 검사 시점을 변경할 수 있다.  
다음은 지연 가능한 제약 조건을 가진 테이블을 생성하고, 데이터를 추가하는 예이다.

```
gSQL> CREATE TABLE t1 
( 
    id   INTEGER, 
    name VARCHAR(128) CONSTRAINT t1_uk UNIQUE 
                      DEFERRABLE INITIALLY IMMEDIATE
);

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> INSERT INTO t1 VALUES ( 1, 'leekmo' );

1 row created.

gSQL> INSERT INTO t1 VALUES ( 2, 'mkkim' );

1 row created.

gSQL> COMMIT;

Commit complete.
```

위의 예에서 name column에 지연 가능한 UNIQUE 제약 조건을 생성하였으며, 초기 검사 시점이 INITIALLY IMMEDIATE로 설정되어 DML을 수행할 때마다 제약 조건을 검사한다.

이 때, 다음과 같이 두 row의 name 값을 서로 교체하려고 하면 검사 시점이 IMMEDIATE라서 모두 제약 조건을 위반하게 된다.

```
gSQL> UPDATE t1 SET name = 'mkkim' WHERE id = 1;

ERR-23000(16057): unique constraint (PUBLIC.T1_UK) violated

gSQL> UPDATE t1 SET name = 'leekmo' WHERE id = 2;

ERR-23000(16057): unique constraint (PUBLIC.T1_UK) violated
```

다음과 같이 검사 시점을 DEFERRED로 변경하면 COMMIT 시점에 제약 조건을 검사하므로 위의 예와 동일한 변경 작업이 모두 성공한다.

```
gSQL> SET CONSTRAINTS t1_uk DEFERRED;

Constraints set.

gSQL> UPDATE t1 SET name = 'mkkim' WHERE id = 1;

1 row updated.

gSQL> UPDATE t1 SET name = 'leekmo' WHERE id = 2;

1 row updated.

gSQL> COMMIT;

Commit complete.
```

검사 시점을 DEFERRED로 설정하면 COMMIT 시점에 제약 조건을 검사하므로 제약 조건을 위반한 상태에서 트랜잭션을 COMMIT 할 경우 다음과 같이 트랜잭션은 실패하고 ROLLBACK 된다.

```
gSQL> SET CONSTRAINTS t1_uk DEFERRED;

Constraints set.

gSQL> INSERT INTO t1 VALUES ( 3, 'leekmo' );

1 row created.

gSQL> COMMIT;

ERR-40002(16291): transaction rollback: integrity constraint violation : PUBLIC.T1_UK(1)
```

<a id="4b6d85d11608d89a"></a>
#### 지연 제약 조건을 위반한 트랜잭션

트랜잭션이 DEFFERED로 설정된 제약 조건을 위반한 상태에서 다음 구문들을 수행할 경우 다음과 같은 에러가 발생한다.

- COMMIT
    - 에러가 발생하고, 트랜잭션이 ROLLBACK 된다.
- SET CONSTRAINTS ALL IMMEDIATE
    - 구문 에러가 발생한다.
- DDL
    - 구문 에러가 발생한다.

COMMIT 할 경우 원치 않는 ROLLBACK이 발생할 수 있으므로, SET CONSTRAINTS ALL IMMEDIATE 구문을 수행하여 트랜잭션이 제약 조건을 위반한 상태인지 확인해야 한다.

```
gSQL> SET CONSTRAINTS t1_uk DEFERRED;

Constraints set.

gSQL> INSERT INTO t1 VALUES ( 3, 'leekmo' );

1 row created.

gSQL> SET CONSTRAINTS ALL IMMEDIATE;

ERR-23000(16038): integrity constraint violation : PUBLIC.T1_UK(1)

gSQL> SELECT * FROM t1 ORDER BY id;

ID NAME  
-- ------
 1 mkkim 
 2 leekmo
 3 leekmo

3 rows selected.

gSQL> UPDATE t1 SET name = 'xcom73' WHERE id = 3;

1 row updated.

gSQL> SET CONSTRAINTS ALL IMMEDIATE;

Constraints set.

gSQL> COMMIT;

Commit complete.
```

<a id="a93ee2239cc6d89e"></a>
#### 트랜잭션 제어 언어

SET CONSTRAINTS 구문은 [SAVEPOINT savepoint_specifier](#e403c1a580ceeb98) 구문과 같이 트랜잭션 진행 중에 사용하는 트랜잭션 제어 언어이다.  
SET CONSTRAINTS 구문에는 COMMIT, ROLLBACK, ROLLBACK TO SAVEPOINT 구문 등의 트랜잭션 제어가 적용된다.

다음은 여러 개의 지연 가능한 제약 조건을 가진 테이블의 예이다.

```
CREATE TABLE t1
(
   id1 INTEGER CONSTRAINT t1_uk1 UNIQUE DEFERRABLE INITIALLY IMMEDIATE,
   id2 INTEGER CONSTRAINT t1_uk2 UNIQUE DEFERRABLE INITIALLY IMMEDIATE,
   id3 INTEGER CONSTRAINT t1_uk3 UNIQUE DEFERRABLE INITIALLY IMMEDIATE
);
```

다음과 같이 트랜잭션이 진행되는 중에 &lt;set constraints mode statement&gt; 구문을 수행할 경우, 각 시점에 따라 지연 가능한 제약 조건들의 검사 시점이 변경된다.

- result: success

```
INSERT INTO t1 VALUES ( 1, 1, 1 );

1 row created.

COMMIT;

Commit complete.
```

- result: success

```
SAVEPOINT sp1;

Savepoint created.
```

- result: success
- t1_uk1 constraint is DEFERRED

```
SET CONSTRAINTS t1_uk1 DEFERRED;

Constraints set.
```

- result: success

```
SAVEPOINT sp2;

Savepoint created.
```

- result: success
- t1_uk1, t1_uk2 constraints are DEFERRED

```
SET CONSTRAINTS t1_uk2 DEFERRED;

Constraints set.
```

- result: success

```
SAVEPOINT sp3;

Savepoint created.
```

- result: success
- ALL constraints are DEFERRED

```
SET CONSTRAINTS ALL DEFERRED;

Constraints set.
```

- result: success

```
SAVEPOINT sp4;

Savepoint created.
```

- result: success
- ALL constraints are IMMEDIATE

```
SET CONSTRAINTS ALL IMMEDIATE;

Constraints set.
```

다음과 같이 ROLLBACK TO SAVEPOINT 구문을 사용하여 트랜잭션을 부분 철회할 경우 SET CONSTRAINTS 구문도 함께 부분 철회되어 검사 시점이 변경된다.

- result: error

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK1) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK2) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK3) violated
```

- result: success
- t1_uk1, t1_uk2 constraints are DEFERRED

```
ROLLBACK TO SAVEPOINT sp4;

Rollback complete.
```

- result: success

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

1 row created.
```

- result: success

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

1 row created.
```

- result: success

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

1 row created.
```

- result: success
- t1_uk1, t1_uk2 constraints are DEFERRED

```
ROLLBACK TO SAVEPOINT sp3;

Rollback complete.
```

- result: success

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

1 row created.
```

- result: success

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

1 row created.
```

- result: error

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK3) violated
```

- result: success
- t1_uk1 constraint is DEFERRED

```
ROLLBACK TO SAVEPOINT sp2;

Rollback complete.
```

- result: success

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

1 row created.
```

- result: error

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK2) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK3) violated
```

- result: success
- all constraint are IMMEDIATE

```
ROLLBACK TO SAVEPOINT sp1;

Rollback complete.
```

- result: error

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK1) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK2) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK3) violated
```

- result: 1 row
- 1 1 1

```
SELECT * FROM t1;

ID1 ID2 ID3
--- --- ---
  1   1   1

1 row selected.
```

트랜잭션을 COMMIT 하거나 ROLLBACK 할 경우, SET CONSTRAINTS 구문의 영향은 종료되며, 모든 지연 가능한 제약 조건들은 제약 조건의 특성으로 설정한 INITIALLY IMMEDIATE 또는 INITIALLY DEFERRED 값을 따른다.

<a id="e6b82b1c8ccab73f"></a>
### 사용 예

다음은 제약 조건 이름을 기술하여 검사 시점을 변경하는 예이다.

```
gSQL> SET CONSTRAINTS t1_uk1 DEFERRED;

Constraints set.
```

다음은 모든 지연 가능한 제약 조건의 검사 시점을 변경하는 예이다.

```
gSQL> SET CONSTRAINTS ALL DEFERRED;

Constraints set.
```

<a id="69677db3cb70052e"></a>
### 호환성

SQL 표준에서는 CONSTRAINT 키워드 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="767b0006469d800e"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F721 | Deferrable constraints | O |

<a id="49a8b2872b1972ef"></a>
### 참조

관련 내용은 다음을 참조한다.

- 제약 조건 생성
    - [CREATE TABLE](#1586c5952309fa38)
    - [ALTER TABLE name ADD CONSTRAINT](#8c53ce7b8253f264)
    - [ALTER TABLE name ADD COLUMN](#c42e27e734cc5c56)
    - [ALTER TABLE name ALTER COLUMN](#7b1c675bb7a0aac7)

- 제약 조건 변경: [ALTER TABLE name ALTER CONSTRAINT](#0fd66f8da1d1d087)

- 제약 조건 검사시점 제어: [SET CONSTRAINTS](#8e1fec980aea373d)

<a id="fc35dac87707c70d"></a>
## SET SESSION AUTHORIZATION user_identifier

<a id="8f570d516ab0a039"></a>
### 기능

Session user와 current user를 변경한다.

<a id="bc379e1d01043b86"></a>
### 구문

```
<set session user identifier statement> ::=
    SET SESSION AUTHORIZATION user_identifier
    ;
```

<a id="01ee64442c3816ef"></a>
### 사용 범위 및 접근 권한

&lt;set session user identifier statement&gt; 구문을 수행하려면 logon 사용자에게 ACCESS CONTROL ON DATABASE 권한이 있어야 한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user 
    - Login 한 user로써 connection을 닫을 때까지 유지된다. 
- Session user 
    - 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다. 
- Current user 
    - 일반적으로 session user와 동일하지만 PSM이나 view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다. 
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="74afd86ed9bd9fd6"></a>
### 구문 규칙 및 파라미터

<a id="70712d35657b6c92"></a>
#### user_identifier

변경할 사용자의 이름이다.

<a id="e2a66577767fe4ba"></a>
### 설명

SET SESSION AUTHORIZATION 구문을 수행한 이후의 모든 구문은 session user를 기준으로 수행되므로, session user에 대한 권한을 검사하고 객체를 생성할 때의 소유자 역시 session user가 된다.

<a id="e16c849c4adc7714"></a>
### 사용 예

다음은 ACCESS CONTROL ON DATABASE 권한을 가진 test 사용자가 session user를 u1 사용자로 변경한 예이다.

```
gSQL> SET SESSION AUTHORIZATION u1;

Session set.

gSQL> SELECT LOGON_USER(), SESSION_USER(), CURRENT_USER FROM dual;

LOGON_USER() SESSION_USER() CURRENT_USER
------------ -------------- ------------
TEST         U1             U1          

1 row selected.
```

<a id="c502ef81f66fef9c"></a>
### 호환성

**SQL 표준 호환성**

<a id="28d128738a3c80b7"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F321 | User authorization | O |

<a id="fddd557277575eef"></a>
## SET SESSION CHARACTERISTICS AS transaction_mode

<a id="a6b5a27e1b411dd6"></a>
### 기능

세션의 트랜잭션 속성을 설정한다.

<a id="4ad684f21b42beec"></a>
### 구문

```
<set session characteristics statement> ::=
    SET SESSION CHARACTERISTICS AS TRANSACTION <transaction_mode>
    ;

<transaction_mode> ::=
    { <transaction_access_mode> | ISOLATION LEVEL < isolation_level > }

<transaction_access_mode> ::=
    READ { ONLY | WRITE }

< isolation_level > ::=
    { READ COMMITTED | SERIALIZABLE }
```

<a id="2e0eaeae2a17b1b8"></a>
### 구문 규칙 및 파라미터

<a id="6024954bdac273b5"></a>
#### &lt;transaction_access_mode&gt;

다음 트랜잭션의 ACCESS MODE 이다.

- READ ONLY 
- READ WRITE

<a id="090e2459ac19e1d3"></a>
#### &lt;isolation_level&gt;

다음 트랜잭션의 ISOLATION LEVEL 이다.

- READ COMMITTED 
- SERIALIZABLE

<a id="663f7fcb94d3cdfc"></a>
### 설명

SET SESSION CHARACTERISTICS은 세션의 트랜잭션 속성을 설정한다. 즉, session 내에서 생성되는 모든 transaction의 속성이 이를 따른다.

참고로 [SET TRANSACTION transaction_mode](#5982821281cecdf0) 구문의 경우, 이후에 수행되는 하나의 transaction 속성만 변경한다.

<a id="f7c81b3bb1bef7b1"></a>
### 사용 예

다음은 session 내에서 생성될 모든 transaction을 READ ONLY로 설정하는 예이다.

```
gSQL> SET SESSION CHARACTERISTICS AS TRANSACTION READ ONLY;

Session set.
```

다음은 session 내에서 생성될 모든 transaction의 isolation level을 READ COMMITTED로 설정하는 예이다.

```
gSQL> SET SESSION CHARACTERISTICS AS TRANSACTION ISOLATION LEVEL READ COMMITTED;

Session set.
```

<a id="f213da5f68bd0564"></a>
### 호환성

**SQL 표준 호환성**

<a id="b078a12965f655be"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F761 | Session management | O |

<a id="5f22b82b72f5adfb"></a>
### 참조

관련 내용은 [SET TRANSACTION transaction_mode](#5982821281cecdf0)를 참조한다.

<a id="a2ab359009eff138"></a>
## SET TIME ZONE

<a id="827da668fbe88418"></a>
### 기능

세션의 TIMEZONE을 설정한다.

<a id="a0f9fddb39fb7cdc"></a>
### 구문

```
<set local time zone statement> ::=
    SET TIME ZONE <set time zone value>
    ;

<set time zone value> ::= 
    { '[+|-]hh:mm' | LOCAL }
```

<a id="40857ee7e124c4f5"></a>
### 구문 규칙 및 파라미터

<a id="039fde7676a26ac1"></a>
#### &lt;set time zone value&gt;

설정할 TIMEZONE 값이다.

- hh:mm: 설정할 TIMEZONE의 GMT OFFSET이다.
    - Offset 값의 범위는 '-14:00' ~ '+14:00' 이다.
- LOCAL: Session을 생성한 시점의 TIME ZONE 이다.
    - Session을 생성할 때의 TIME ZONE은 client OS의 TIME ZONE으로 설정된다.

<a id="3d308bc846226ca6"></a>
### 설명

Session의 time zone을 변경하면 함수 [CURRENT_TIME](11-sql-elements.md#a4e68f37761bd434), [CURRENT_TIMESTAMP](11-sql-elements.md#00166487940f1b96) 등의 결과값에 영향을 미친다.

<a id="a70e3edc52e091e6"></a>
### 사용 예

다음은 session의 time zone을 '+09:00' 으로 변경하는 예이다.

```
gSQL> SET TIME ZONE '+09:00';

Session set.
```

<a id="00eca241b5833f9d"></a>
### 호환성

**SQL 표준 호환성**

<a id="1159fb452074b74a"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F411 | Time zone specification | O |

<a id="5982821281cecdf0"></a>
## SET TRANSACTION transaction_mode

<a id="7b6135f83a5bf2c9"></a>
### 기능

다음 트랜잭션의 속성을 설정한다.

<a id="2b304b45e7875698"></a>
### 구문

```
<set transaction statement> ::=
    SET TRANSACTION <transaction_mode>
    ;

<transaction_mode> ::=
    { <transaction_access_mode> | ISOLATION LEVEL < isolation_level > }

<transaction_access_mode> ::=
    READ { ONLY | WRITE }

< isolation_level > ::=
    { READ COMMITTED | SERIALIZABLE }
```

<a id="4e74d3d023989309"></a>
### 구문 규칙 및 파라미터

<a id="609831a0be8f15bf"></a>
#### &lt;transaction_access_mode&gt;

다음 트랜잭션의 ACCESS MODE 이다.

- READ ONLY 
- READ WRITE

<a id="a5820176307046ff"></a>
#### &lt;isolation_level&gt;

다음 트랜잭션의 ISOLATION LEVEL 이다.

- READ COMMITTED 
- SERIALIZABLE

<a id="e610ae38e9eeec4a"></a>
### 설명

SET TRANSACTION은 다음 트랜잭션의 속성을 설정하며, 다음 트랜잭션이 종료되면 트랜잭션 속성은 기본값으로 복원된다.

<a id="a8b697d7a4cf8980"></a>
### 사용 예

다음에 수행될 transaction을 읽기 전용으로 설정한 예이다.

```
gSQL> SET TRANSACTION READ ONLY;

Transaction set.
```

<a id="60f2005f6e8690f9"></a>
### 호환성

**SQL 표준 호환성**

<a id="9f03c8ac3a1f579e"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T251 | SET TRANSACTION statement: LOCAL option | X |

<a id="3858bf87b7a229f2"></a>
### 참조

관련 내용은 [SET SESSION CHARACTERISTICS AS transaction_mode](#fddd557277575eef)를 참조한다.

<a id="acf08f853a438a0d"></a>
## TRUNCATE TABLE

<a id="bb39eeb5b98562c2"></a>
### 기능

테이블의 모든 row들을 제거한다.

<a id="570d882ae63ffb8d"></a>
### 구문

```
<truncate table statement> ::= 
    TRUNCATE TABLE table_name 
        [ RESTART IDENTITY | CONTINUE IDENTITY ] 
        [ DROP STORAGE | DROP ALL STORAGE ] 
    ;
```

<a id="c723b87bf099f39c"></a>
### 사용 범위 및 접근 권한

&lt;truncate table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블의 소유자 
- 테이블에 대해 CONTROL TABLE ON TABLE 
- 테이블이 속한 스키마에 대해 (DROP TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY TABLE ON DATABASE

<a id="aee5cd7e27fde8b2"></a>
### 구문 규칙 및 파라미터

<a id="3fddd7eb3d0fc5a1"></a>
#### table_name

Row들을 제거할 대상 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="8c8b1de4494cb784"></a>
#### [ RESTART IDENTITY | CONTINUE IDENTITY ]

- RESTART IDENTITY 
    - 자동 생성값을 갖는 column (identity column)이 해당 테이블에 존재할 경우 자동으로 값을 재시작한다. 
- CONTINUE IDENTITY 
    - 자동 생성값을 갖는 column (identity column)이 해당 테이블에 존재할 경우 기존값을 변경하지 않는다.
- 명시하지 않을 경우, 기본값은 CONTINUE IDENTITY이다.

<a id="9c8c90dd7661c748"></a>
#### [ DROP STORAGE | DROP ALL STORAGE ]

- DROP STORAGE 
    - 테이블에 할당된 extent 중에 MINSIZE 만큼만 제외하고 나머지 extent들을 삭제한다.
- DROP ALL STORAGE 
    - 테이블에 할당된 모든 extent 들을 삭제한다.
- 명시하지 않을 경우, 기본값은 DROP STORAGE 이다.

<a id="52f664e55f2d8b0d"></a>
### 설명

TRUNCATE TABLE과 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="fd5a0da9d0d4b1a9"></a>
### 사용 예

다음은 TRUNCATE TABLE 구문을 수행하는 예이다.

```
gSQL> TRUNCATE TABLE t1;

Table truncated.
```

다음은 TRUNCATE TABLE을 수행할 때 identity column 값을 재시작하는 예이다.

```
TRUNCATE TABLE t1 RESTART IDENTITY;

Table truncated.
```

<a id="e928c57544118dd5"></a>
### 호환성

SQL 표준에서는 [ DROP STORAGE | DROP ALL STORAGE ] 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="f5b7c371888e6ee5"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F200 | TRUNCATE TABLE statement | O |
| F202 | TRUNCATE TABLE: identity column restart option | O |

<a id="545d9c2796a3df91"></a>
## UPDATE

<a id="75d03f4d13754004"></a>
### 기능

테이블의 row들을 갱신한다.

<a id="9222ccfc8e87fc42"></a>
### 구문

```
<update statement: searched> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        SET <set clause> [, ...]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
    ;

<set clause> ::=
      column_name = { <value expression> | DEFAULT }
    | ( column_name [, ...] ) = ( { <value expression> | DEFAULT } [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )


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

<a id="3c51b135e932465c"></a>
### 사용 범위 및 접근 권한

&lt;update statement: searched&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- Update 대상인 모든 column에 대해 UPDATE(columns) ON TABLE 
- 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- UPDATE ANY TABLE ON DATABASE

<a id="c707491568996fff"></a>
### 구문 규칙 및 파라미터

<a id="12a038c6de11dafa"></a>
#### table_name

Row를 갱신할 대상 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="0db7936bc40a6ce8"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="a23d784a0a5a38cc"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.

다음과 같은 방법으로 정의할 수 있다.

- column_name = { &lt;value expression&gt; | DEFAULT }

```
UPDATE table_name 
   SET column1 = value1, column2 = value2, column3 = value3
```

- ( column_name [, ...] ) = ( { &lt;value expression&gt; | DEFAULT } [, ...] )

```
UPDATE table_name 
   SET ( column1, column2, column3 ) = ( value1, value2, value3 )
```

- ( column_name [, ...] ) = ( &lt;query expression&gt; )

```
UPDATE table_name 
   SET column1 = ( SELECT max(value1) FROM other_table_name )
```

&lt;query expression&gt;은 row 하나를 생성하는 질의여야 한다.

Column 값으로 DEFAULT를 사용할 경우, [CREATE TABLE](#1586c5952309fa38)을 수행할 때 정의한 기본값 (&lt;[default clause&gt;](#7d047626d6bea974) 참조)을 사용하며, 정의되지 않은 경우에는 NULL 값이 할당된다.

<a id="944ef31127366b95"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 갱신한다.  
WHERE 조건을 명시하지 않을 경우, 모든 row들을 갱신한다.  
WHERE 조건에 대한 자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 [where clause](#8ffd103d5116485d)를 참조한다.

<a id="70162e0a07da0466"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 &lt;[result offset clause&gt;](#0689e0f6cda4a513)를 참조한다.

<a id="c92f6962ab90c7b4"></a>
#### &lt;fetch limit clause&gt;

Fetch 할 row의 개수를 명시하는 구문으로써 다음 두 가지 방법을 사용할 수 있다.

- &lt;fetch first clause&gt; 
    - Fetch 할 row의 개수를 명시한다. 
    - 자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 &lt;[fetch first clause&gt;](#5bc4649717039d2f)를 참조한다.
- &lt;limit clause&gt;
    - Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
    - 자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 &lt;[limit clause&gt;](#7e039c5707f8a97b)를 참조한다.

<a id="3f05a4022d72b540"></a>
### 설명

<a id="4ef25fc85d11414b"></a>
#### UPDATE 관련 구문들의 차이점

- [UPDATE](#545d9c2796a3df91)
    - 조건에 부합하는 다수의 row를 갱신한다. 
    - 예: UPDATE t1 SET c2 = c2 + 1 WHERE c1 > 0; 
- [UPDATE name WHERE CURRENT OF cursor_name](#0c2203e790c21b59)
    - 현재 cursor가 가리키는 row를 갱신한다. 
    - 예: UPDATE t1 WHERE CURRENT OF cursor; 
- [UPDATE name RETURNING](#5c5251f859c78279)
    - 조건에 부합하는 다수의 row를 갱신하며, 갱신한 row들을 [SELECT](#c9d76bf073f60db2) 구문과 동일한 방식 (SQLFetch() 등의 API)으로 검색할 수 있다. 
    - 예: UPDATE t1 SET c2 = c2 + 1 WHERE c1 > 0 RETURNING c2; 
- [UPDATE name RETURNING .. INTO](#9430037a3767eba7)
    - 한 건 이하의 row를 갱신할 수 있으며, 갱신한 row가 한 건일 경우 RETURNING INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: UPDATE t1 SET c2 = c2 + 1 WHERE c1 = 0 RETURNING c2 INTO :v1;

<a id="edad5e09906862c1"></a>
### 사용 예

다음은 조건에 부합하는 다수의 row를 갱신하는 예이다.

```
gSQL> UPDATE lineitem
         SET l_shipdate = CURRENT_DATE
       WHERE l_returnflag = 'R';

5 rows updated.
```

다음은 여러 column의 값을 갱신하는 예이다.

```
gSQL> UPDATE lineitem
         SET l_shipdate   = CURRENT_DATE
           , l_returnflag = 'A'
       WHERE l_returnflag = 'R';

5 rows updated.
```

다음은 여러 column을 괄호로 묶어 갱신하는 예이다.

```
gSQL> UPDATE lineitem
         SET ( l_shipdate  , l_returnflag )
           = ( CURRENT_DATE, 'A' )
       WHERE l_returnflag = 'R';

5 rows updated.
```

다음은 subquery를 사용하여 column의 값을 갱신하는 예이다.

```
gSQL> UPDATE lineitem
         SET l_discount = ( SELECT MAX(l_discount) + 0.01 FROM lineitem )
       WHERE l_returnflag = 'R';

5 rows updated.
```

다음은 OFFSET과 FETCH 절을 사용하여 조건에 부합하는 row들 중 일부만 갱신하는 예이다.

```
gSQL> UPDATE lineitem
         SET l_discount = l_discount + 0.01
       WHERE l_returnflag = 'R'
      OFFSET 3
      FETCH 2;

2 rows updated.
```

<a id="65455b903345b3a9"></a>
### 호환성

SQL 표준은 UPDATE 구문에서 다음 절을 정의하지 않고 있다.

- &lt;result offset clause&gt; 
- &lt;fetch limit clause&gt;

**SQL 표준 호환성**

<a id="25ad99438621732c"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="5c5251f859c78279"></a>
## UPDATE name RETURNING

<a id="7e22a9680a906420"></a>
### 기능

테이블의 row들을 갱신하고, 갱신 전의 row들이나 갱신 후의 row들을 검색한다.

<a id="791a69682c11ff85"></a>
### 구문

```
<update statement: searched> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        SET <set clause> [, ...]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
        <returning clause>

<set clause> ::=
      column_name = { <value expression> | DEFAULT }
    | ( column_name [, ...] ) = ( { <value expression> | DEFAULT } [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )


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
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] }
```

<a id="4a59f78fe0cf7488"></a>
### 사용 범위 및 접근 권한

&lt;update returning query statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- UPDATE 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Update 대상인 모든 column에 대해 UPDATE(columns) ON TABLE 
    - 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - UPDATE ANY TABLE ON DATABASE

- RETURNING 절에 사용된 모든 column에 대해 다음 권한 중 하나가 있어야 한다.
    - RETURNING 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="f5e1f3c8c1331ba9"></a>
### 구문 규칙 및 파라미터

<a id="7b0a578d0231c8cd"></a>
#### table_name

Row를 갱신할 대상 테이블의 이름이다.

<a id="fb0a6bd7d09405b9"></a>
#### [ AS alias_name ]

table_name의 alias이다.

<a id="3c38a26caf4f3760"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.  
자세한 내용은 [UPDATE](#545d9c2796a3df91) 구문을 참조한다.

<a id="092dbc1d79e62e25"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 갱신한다.  
WHERE 조건을 명시하지 않을 경우, 모든 row들을 갱신한다.  
WHERE 조건에 대한 자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 [where clause](#8ffd103d5116485d)를 참조한다.

<a id="dfa7d301ab4d885e"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 &lt;[result offset clause&gt;](#0689e0f6cda4a513)를 참조한다.

<a id="9390e6467442c491"></a>
#### &lt;fetch limit clause&gt;

Fetch 할 row의 개수를 명시하는 구문으로써 다음 두 가지 방법을 사용할 수 있다.

- &lt;fetch first clause&gt; 
    - Fetch 할 row의 개수를 명시한다. 
    - 자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 &lt;[fetch first clause&gt;](#5bc4649717039d2f)를 참조한다.
- &lt;limit clause&gt;
    - Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
    - 자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 &lt;[limit clause&gt;](#7e039c5707f8a97b)를 참조한다.

<a id="9623f4207901148c"></a>
#### &lt;returning clause&gt;

갱신된 row들을 결과 집합으로 하고, 이들 중에서 검색할 column을 기술한다.

- RETURN과 RETURNING은 동일한 의미의 키워드이다. 
- NEW | OLD 
    - NEW: 갱신된 row들 중에 갱신 후 row를 기준으로 검색한다. 
    - OLD: 갱신된 row들 중에 갱신 전 row를 기준으로 검색한다. 
    - 생략할 경우, 기본값은 NEW 이다. 
- &lt;value expression&gt; 
    - SELECT 구문의 &lt;select list&gt;와 동일하지만 aggregation 등을 사용할 수 없다. 
- [ [AS] alias_name] 
    - AS 절을 사용하여 &lt;value expression&gt;의 이름을 지정할 수 있다.

<a id="5b5c6a473829ccff"></a>
### 설명

자세한 내용은 [UPDATE 관련 구문들의 차이점](#4ef25fc85d11414b)을 참조한다.

<a id="5d3173c6571d65ad"></a>
### 사용 예

다음은 RETURNING 절을 사용하여 갱신된 row들의 값을 얻는 예이다.

```
gSQL> UPDATE lineitem 
         SET l_discount = l_discount + 0.01
       WHERE l_returnflag = 'R'
   RETURNING l_orderkey, l_linenumber, l_discount;

L_ORDERKEY L_LINENUMBER L_DISCOUNT
---------- ------------ ----------
         8            1        .07
         9            2        .11
        12            5        .05
        15            1        .03
        16            2        .08

5 rows updated.
```

다음은 RETURNING OLD 절을 사용하여 갱신된 row들의 갱신 전 값을 얻는 예이다.

```
gSQL> UPDATE lineitem 
         SET l_discount = l_discount + 0.01
       WHERE l_returnflag = 'R'
   RETURNING OLD l_orderkey, l_linenumber, l_discount;

L_ORDERKEY L_LINENUMBER L_DISCOUNT
---------- ------------ ----------
         8            1        .06
         9            2         .1
        12            5        .04
        15            1        .02
        16            2        .07

5 rows updated.
```

<a id="498bd49ab29affd4"></a>
### 호환성

SQL 표준에는 &lt;update returning query statement&gt; 구문이 존재하지 않는다.

<a id="9430037a3767eba7"></a>
## UPDATE name RETURNING .. INTO

<a id="2aec6915e41538d4"></a>
### 기능

테이블 row 한 개를 갱신하고, 갱신한 row의 값을 호스트 변수에 얻어온다.

<a id="a2aaae4b9e38623d"></a>
### 구문

```
<update statement: searched> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        SET <set clause> [, ...]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
        <returning into clause>
    ;


<set clause> ::=
      column_name = { <value expression> | DEFAULT }
    | ( column_name [, ...] ) = ( { <value expression> | DEFAULT } [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )


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
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] } INTO variable_name [, ...]
```

<a id="9bd0a7be50552867"></a>
### 사용 범위 및 접근 권한

&lt;update returning query statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- UPDATE 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Update 대상인 모든 column에 대해 UPDATE(columns) ON TABLE 
    - 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - UPDATE ANY TABLE ON DATABASE

- RETURNING 절에 사용된 모든 column에 대해 다음 권한 중 하나가 있어야 한다.
    - RETURNING 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="8231dc3c7770e513"></a>
### 구문 규칙 및 파라미터

<a id="c9c3c94cf5723ac0"></a>
#### table_name

Row를 갱신할 대상 테이블의 이름이다.

<a id="b80aada820440aff"></a>
#### [ AS alias_name ]

table_name의 alias이다.

<a id="94adf89fdcebda70"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.  
자세한 내용은 [UPDATE](#545d9c2796a3df91) 구문을 참조한다.

<a id="7d19d7a70912cfaf"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 갱신한다.  
WHERE 조건을 명시하지 않을 경우, 모든 row들을 갱신한다.  
WHERE 조건에 대한 자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 [where clause](#8ffd103d5116485d)를 참조한다.

<a id="e788dad988c31d67"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 &lt;[result offset clause&gt;](#0689e0f6cda4a513)를 참조한다.

<a id="b0090a924acd213b"></a>
#### &lt;fetch limit clause&gt;

Fetch 할 row의 개수를 명시하는 구문으로써 다음 두 가지 방법을 사용할 수 있다.

- &lt;fetch first clause&gt; 
    - Fetch 할 row의 개수를 명시한다. 
    - 자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 &lt;[fetch first clause&gt;](#5bc4649717039d2f)를 참조한다.
- &lt;limit clause&gt;
    - Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
    - 자세한 내용은 [SELECT](#c9d76bf073f60db2) 구문의 &lt;[limit clause&gt;](#7e039c5707f8a97b)를 참조한다.

<a id="072164b4f6a1b3c9"></a>
#### RETURNING .. AS ..

갱신된 row들을 결과 집합으로 하고, 이들 중에서 검색할 column을 기술한다.  
자세한 내용은 [UPDATE name RETURNING](#5c5251f859c78279) 구문의 &lt;[returning clause&gt;](#9623f4207901148c)를 참조한다.

<a id="528963e8011a1743"></a>
#### INTO variable_name [, ...]

INTO 절에 기술된 변수의 개수는 RETURNING 절에 기술된 expression의 개수와 동일해야 한다.  
갱신할 row가 한 건 이하여야 한다.  
Row가 두 건 이상 갱신될 경우, 에러가 발생한다.

<a id="3555e9049813b90f"></a>
### 설명

자세한 내용은 [UPDATE 관련 구문들의 차이점](#4ef25fc85d11414b)을 참조한다.

<a id="24e8b34b496d1455"></a>
### 사용 예

다음은 갱신한 row의 column 값을 host 변수에 얻어오는 예이다.

- Host 변수를 선언한다.

```
gSQL> \VAR v_discount NUMBER

gSQL> UPDATE lineitem 
         SET l_discount = l_discount + 0.01
       WHERE l_orderkey = 12 AND l_linenumber = 5
   RETURNING l_discount INTO :v_discount;

V_DISCOUNT
----------
       .05

1 row updated.
```

<a id="d943225ae7e1beea"></a>
### 호환성

SQL 표준에는 &lt;update returning into statement&gt; 구문이 존재하지 않는다.

<a id="0c2203e790c21b59"></a>
## UPDATE name WHERE CURRENT OF cursor_name

<a id="eb8029c1fd25e349"></a>
### 기능

커서가 가리키는 row 하나를 갱신한다.

<a id="e75c379f221b50a1"></a>
### 구문

```
<update statement: positioned> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        SET <set clause> [, ...]
        WHERE CURRENT OF cursor_name
    ;
```

<a id="1b86644e207cbdce"></a>
### 사용 범위 및 접근 권한

&lt;update statement: positioned&gt; 구문을 수행하려면 사용자가 다음 조건을 만족해야 한다.

- UPDATE 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Update 대상인 모든 column에 대해 UPDATE(columns) ON TABLE 
    - 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - UPDATE ANY TABLE ON DATABASE

<a id="e3fdfd04da76f0a6"></a>
### 구문 규칙 및 파라미터

<a id="3d799298c8b7ffee"></a>
#### table_name

Row를 갱신할 대상 테이블의 이름이다.

<a id="314fb18cf4141d46"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="325ea7f4e402076c"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.  
자세한 내용은 [UPDATE](#545d9c2796a3df91) 구문을 참조한다.

<a id="b3410d9cccc75aec"></a>
#### cursor_name

cursor_name에 해당하는 커서는 다음 조건들을 만족해야 한다.

- OPEN 된 커서이어야 한다. ([OPEN cursor_name](#275ead84ebffb434) 참조) 
- 커서를 이용해 FETCH 한 row가 있어야 한다. ([FETCH cursor_name](#f8b0914239210b68) 참조) 
- 커서에 사용된 질의가 table_name을 식별할 수 있어야 한다. ([DECLARE cursor_name](#c0f5909b51d661a3) 참조) 
- table_name에 대해 갱신할 수 있는 커서이어야 한다. ([DECLARE cursor_name](#c0f5909b51d661a3) 참조)

<a id="555487207a90eafa"></a>
### 설명

자세한 내용은 [UPDATE 관련 구문들의 차이점](#4ef25fc85d11414b)을 참조한다.

<a id="e1d8e8318609bd9c"></a>
### 사용 예

다음은 interactive SQL (gsql)에서 cursor를 사용하여 &lt;update statement: positioned&gt; 구문을 수행하는 예이다.

- Host 변수를 선언한다.

```
gSQL> \VAR v_discount NUMBER
```

- Cursor를 선언한다.

```
gSQL> DECLARE update_cursor CURSOR FOR 
        SELECT l_discount
          FROM lineitem
         WHERE l_orderkey = 8 AND l_linenumber = 1
           FOR UPDATE;

Cursor declared.
```

- Cursor를 open한다.

```
gSQL> OPEN update_cursor;

Cursor is open.
```

- Row를 fetch한다.

```
gSQL> FETCH update_cursor INTO :v_discount;

V_DISCOUNT
----------
       .06

1 row fetched.
```

- Current row를 update한다.

```
gSQL> UPDATE lineitem 
         SET l_discount = l_discount + 0.01 
       WHERE CURRENT OF update_cursor;

1 row updated.
```

- Cursor를 close한다.

```
gSQL> CLOSE update_cursor;

Cursor closed.

gSQL> COMMIT;

Commit complete.
```

다음은 embedded SQL 프로그램에서 cursor를 사용하여 &lt;update statement: positioned&gt; 구문을 수행하는 예이다.

```
{
    ...
    EXEC SQL BEGIN DECLARE SECTION;
        ...    
        double v_discount;  
        ...   
    EXEC SQL END DECLARE SECTION;
    ...
    EXEC SQL DECLARE update_cursor CURSOR FOR
              SELECT l_discount
                FROM lineitem
               WHERE l_orderkey = 8 AND l_linenumber = 1
                 FOR UPDATE;
    ...
    EXEC SQL OPEN update_cursor;
    ...
    EXEC SQL FETCH NEXT update_cursor INTO :v_discount;
    ...
    EXEC SQL UPDATE lineitem 
                SET l_discount = l_discount + 0.01 
              WHERE CURRENT OF update_cursor;
    ...
    EXEC SQL CLOSE update_cursor;
    ...
    EXEC SQL COMMIT WORK;
    ...
}
```

<a id="f4b74dff6ee3570e"></a>
### 호환성

**SQL 표준 호환성**

<a id="6012b0940ae70d06"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F831 | Full cursor update | O |
| B031 | Basic dynamic SQL | O |

<a id="8c8f95fa430b6f39"></a>
### 참조

관련 내용은 [CLOSE cursor_name](#c718855fa5a651b0)을 참조한다.

---

[← 15. SQL Tuning](15-sql-tuning.md) · [전체 목차](../README.md) · [17. Overview of PSM →](../part-04-psm-manual/17-overview-of-psm.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
