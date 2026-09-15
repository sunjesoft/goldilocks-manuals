<a id="f41b6aa6080197e3"></a>

# 18. SQL References

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/f41b6aa6080197e3)  
> 태그: `20c.1_30_tag`

[← 17. Built-in Function References](17-built-in-function-references.md) · [전체 목차](../README.md) · [19. Overview of PSM →](../part-04-psm-manual/19-overview-of-psm.md)

<a id="241fd4b15c525c5a"></a>
## ALTER AUDIT POLICY

<a id="e16d0936d990678b"></a>
### 기능

Audit policy 객체에 감사 대상을 추가하거나 삭제한다.

<a id="bf5f8ff067872124"></a>
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

<a id="7c5a13abe0122a27"></a>
### 사용 범위 및 접근 권한

&lt;alter audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="c0ee7ce186a1db71"></a>
### 구문 규칙 및 파라미터

<a id="e4cb7696e88f08eb"></a>
#### policy_name

변경할 audit policy 객체의 이름이다.

<a id="f27cb945e66d6998"></a>
#### &lt;add_audit_option&gt;

Audit policy에 감사대상을 추가한다.

<a id="06ce7a45b0d72bb8"></a>
#### &lt;drop_audit_option&gt;

Audit policy 감사대상에서 삭제한다.

<a id="3c2cb8cbee6a7f7f"></a>
#### &lt;privilege_audit_clause&gt;

자세한 내용은 [CREATE AUDIT POLICY](#09b3895daf4991da)를 참조한다.

<a id="bb841124bd9b5e38"></a>
#### &lt;action_audit_clause&gt;

자세한 내용은 [CREATE AUDIT POLICY](#09b3895daf4991da)를 참조한다.

<a id="824ea44a700b9a4c"></a>
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

<a id="af73b4dae5e0f751"></a>
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

<a id="ba5cc37c31d85cc6"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="0aaa19ff00ed40bc"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#09b3895daf4991da)
    - [DROP AUDIT POLICY](#4c985d8424a9c9e1)
    - [ALTER AUDIT POLICY](#241fd4b15c525c5a)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#8c7812c0671b6a25)
    - [NOAUDIT POLICY](#f4896aa89ec963af)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#6c787a4b953e8625)

- Audit trail 삭제: [ALTER DATABASE CLEAR AUDIT TRAIL](#d0a56f6310b7a28c)

<a id="72ed23526a0c9e3b"></a>
## ALTER CLUSTER GROUP name ADD MEMBER

<a id="658ca138d6206f08"></a>
### 기능

Cluster group에 cluster member를 추가한다.

<a id="177dee61dfba3597"></a>
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

<a id="4cd02ee1c707032d"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster group add member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="05025fdcb4ec7af0"></a>
### 구문 규칙 및 파라미터

<a id="3b4fe9b70b270fc2"></a>
#### group_name

Cluster group의 이름이다.

<a id="49e901e886fe65e9"></a>
#### &lt;cluster member definition&gt;

Cluster group에 포함될 cluster member를 정의한다.  
Cluster group은 최대 32 개의 cluster member를 포함할 수 있다.

<a id="342ffef844e14870"></a>
#### member_name

Cluster member의 이름이다.   
Cluster member의 이름은 해당 member의 database를 생성할 때 정의한 member의 이름과 동일해야 한다.   
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.   
이름의 길이가 128 바이트보다 작아야 한다.

Cluster member의 start-up 단계가 GLOBAL OPEN이어야 한다.

<a id="c0fecb96c4e8a7ac"></a>
#### &lt;connection attribute&gt;

Cluster member간 통신을 위한 연결 정보를 정의한다.   
&lt;connection attribute&gt;는 해당 member의 database를 생성할 때 정의한 HOST, PORT와 동일해야 한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 ip v4 형식을 사용한다. 
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="4e85584046e80de7"></a>
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

<a id="996ae96588a88b51"></a>
### 설명

&lt;alter cluster group add member statement&gt; 구문은 table들의 shard를 재배치하지 않는다.   
추가된 cluster member에 shard를 재배치하려면 다음 구문을 수행해야 한다.

- [ALTER DATABASE REBALANCE](#48a2899b3f507f9f)
- [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965)

<a id="e50fb56a83293b6d"></a>
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

<a id="9a29e10dc8a340d5"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="c80b45b9e318d768"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER GROUP](#dd23e8e2eae3991d)
- [DROP CLUSTER GROUP](#e491103ba644ea1a)
- [ALTER DATABASE REBALANCE](#48a2899b3f507f9f)
- [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965)

<a id="52c14a825b5adc8f"></a>
## ALTER CLUSTER GROUP name OFFLINE MEMBER

<a id="00e0c5fa491a523d"></a>
### 기능

Cluster group의 cluster member를 offline 상태로 변경한다.

<a id="74f54b9b4ecbe185"></a>
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

<a id="8d0e991e31ced073"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster group offline member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="72fcadfe0e3f49a4"></a>
### 구문 규칙 및 파라미터

<a id="f0dd410f676c6530"></a>
#### group_name

Cluster group의 이름이다.

<a id="2a3e650d0ebbb8a8"></a>
#### &lt;cluster member definition&gt;

Cluster group에 포함될 cluster member를 정의한다.  
Cluster group은 최대 32 개의 cluster member를 포함할 수 있다.

<a id="f323f32db61c2986"></a>
#### member_name

Cluster member의 이름이다.   
Cluster member는 group_name의 cluster group에 포함돼 있어야 한다.  
Cluster member가 inactive 상태여야 한다.

<a id="45c000bbde6bd83f"></a>
### 설명

&lt;alter cluster group offline member statement&gt; 구문은 table들의 shard를 재배치하지 않는다.

<a id="24a8d45457c54ab3"></a>
### 사용 예

다음은 특정 cluster member를 offline 상태로 변경하는 예이다.

```
gSQL>

ALTER CLUSTER GROUP g1 OFFLINE
    CLUSTER MEMBER g1n3
;
Cluster Group altered.
```

<a id="a6bf85d190d92554"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="52d2507159e9aaac"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER GROUP](#dd23e8e2eae3991d)
- [DROP CLUSTER GROUP](#e491103ba644ea1a)
- [ALTER DATABASE REBALANCE](#48a2899b3f507f9f)
- [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965)

<a id="8193ea3b3b99d43b"></a>
## ALTER CLUSTER LOCATION

<a id="1ea89a8318e3adc2"></a>
### 기능

Cluster location 정보를 수정한다.

<a id="54578015795aa7b5"></a>
### 구문

```
<alter cluster location statement> ::=
    ALTER CLUSTER LOCATION member_name 
    <cluster connection attribute>
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="92a1041080c5aed5"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter cluster location statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="e45eabe86d6914cc"></a>
### 구문 규칙 및 파라미터

<a id="a5ec36397a4f9b22"></a>
#### member_name

Cluster member의 이름이다.   
등록된 cluster location 정보에 동일한 cluster member 이름이 존재해야 한다.   
이름의 길이가 128 바이트보다 작아야 한다.

<a id="0f18c1adf78c35f8"></a>
#### &lt;cluster connection attribute&gt;

Cluster member 간 통신을 위한 연결 정보를 정의한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 ip v4 형식으로 사용한다. 
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="ec1144bdabc9180b"></a>
### 설명

만약 cluster location의 접속 정보가 변경될 경우에는 cluster member를 제거하거나 재생성할 필요없이 [ALTER CLUSTER LOCATION](#8193ea3b3b99d43b)을 이용하여 접속 정보를 변경할 수 있다.

<a id="1f32d5478a450888"></a>
### 사용 예

```
gSQL> 
ALTER CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120
;

altered.
```

<a id="848d8171d759d9ef"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="f8ab5d3d38f0bd72"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER LOCATION](#c88dc891576217eb)
- [DROP CLUSTER LOCATION](#8d977b885f9df018)

<a id="1bb9e8840b302b97"></a>
## ALTER DATABASE ADD LOGFILE

<a id="d591609ef187f465"></a>
### 기능

데이터베이스에 로그파일 그룹 또는 로그파일 멤버를 추가한다.

<a id="183bb8adcc347845"></a>
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

<a id="c4f53589d49b2c50"></a>
### 사용 범위 및 접근 권한

&lt;alter database add logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="652715811edc684d"></a>
### 구문 규칙 및 파라미터

<a id="e6e9b0f479e7f641"></a>
#### &lt;alter database add logfile statement&gt;

데이터베이스는 MOUNT 상태여야 한다.

<a id="9d6c7016db6e8d85"></a>
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

<a id="7b8ad1002b7f6a53"></a>
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

<a id="c39e8110c61ec4dd"></a>
### 설명

새로운 로그파일 그룹 및 로그 멤버가 추가되는 경우 controlfile에 저장되므로 향후 controlfile 손상에 대비해 controlfile을 백업하는 것을 권장한다.

<a id="ee56411b6f38b9f4"></a>
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

<a id="407ef45a2f861633"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="ab0fb67402e443d5"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#1bb9e8840b302b97)
- [ALTER DATABASE DROP LOGFILE](#36106c490d8bf76f)
- [ALTER DATABASE RENAME LOGFILE](#9691ec461f59ba6a)

<a id="651e8451c4e3feb6"></a>
## ALTER DATABASE ARCHIVELOG

<a id="d95c49b63685e9ec"></a>
### 기능

데이터베이스의 온라인 로그파일 archive 설정을 변경한다.

<a id="3fcce7268cffec00"></a>
### 구문

```
<alter database archivelog statement> ::=
    ALTER DATABASE { ARCHIVELOG | NOARCHIVELOG }
    ;
```

<a id="210aff8adc7b9855"></a>
### 사용 범위 및 접근 권한

&lt;alter database archivelog statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="ce480ff273f96e3f"></a>
### 구문 규칙 및 파라미터

<a id="62677942ca673177"></a>
#### &lt;alter database archivelog statement&gt;

- 데이터베이스가 MOUNT 상태여야 한다.
- ARCHIVELOG
    - 온라인 로그파일을 archive 한다.
- NOARCHIVELOG
    - 온라인 로그파일을 archive 하지 않는다.

<a id="c7402a5abed14541"></a>
### 설명

Database를 백업하고 백업을 이용해 복구 (media recovery)하려면 시스템이 ARCHIVELOG 모드로 운용되어야 한다.

<a id="e015e61a35d23c41"></a>
### 사용 예

다음은 데이터베이스를 archive 모드로 설정하는 예이다.

```
ALTER DATABASE ARCHIVELOG;
```

<a id="be62a9f1167acad3"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="07587069edfa8c04"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#f6306e58c561105b)
- [ALTER TABLESPACE name BACKUP](#5c95f68797fd85d7)

<a id="f6306e58c561105b"></a>
## ALTER DATABASE BACKUP

<a id="a0c316cca364baae"></a>
### 기능

데이터베이스 전체 백업 (full backup)을 수행하기 위해 백업 상태를 'ACTIVE' 또는 'INACTIVE'로 설정한다. 그리고 데이터베이스 증분 백업 (incremental backup)과 제어 파일 (control file) 백업을 수행한다.

<a id="48340a26c501b17b"></a>
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

<a id="bdba3aa1a069f2f5"></a>
### 사용 범위 및 접근 권한

&lt;alter database backup statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="91fec854a0bacfd6"></a>
### 구문 규칙 및 파라미터

<a id="935864a891959730"></a>
#### &lt;database begin backup clause&gt;

데이터베이스를 전체 백업이 가능한 상태로 설정한다.

- 데이터베이스에서 생성되어 사용 중인 ONLINE 상태의 모든 테이블스페이스를 전체 백업이 가능한 상태로 설정한다. 
- 데이터베이스는 OPEN 상태여야 하고 ARCHIVELOG 모드로 운영되어야 한다.
- BEGIN BACKUP이 시작된 이후에는 다음과 같이 데이터 파일에 쓰기를 요구하는 연산들은 수행할 수 없다.
    - SHUTDOWN NORMAL
    - OFFLINE/ DROP TABLESPACE
    - ADD/ DROP DATAFILE
- 전체 백업의 상태가 ACTIVE인 상태에서 인스턴스가 비정상 종료될 경우, 다시 시작할 때 미디어 복구를 요구할 수도 있다.

<a id="55638a152bea2a69"></a>
#### &lt;database end backup clause&gt;

데이터베이스를 전체 백업 불가능한 상태로 설정한다.

- 데이터베이스에서 생성되어 사용 중인 ONLINE 상태의 모든 테이블스페이스를 백업 불가능한 상태로 설정한다.
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG 모드로 운영되어야 한다.

<a id="5e5018ad79fb999b"></a>
#### &lt;database incremental backup statement&gt;

- 데이터베이스 증분 백업을 수행한다.
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG로 운영되어야 한다.

<a id="1ccfc94070c46767"></a>
#### &lt;incremental backup option&gt;

- 'integer'는 0 ~ 4 까지 지정할 수 있다.
- LEVEL 0은 CUMULATIVE나 DIFFERENTIAL을 지정할 수 없다.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - 'integer'가 n이면 가장 최근에 LEVEL 0 ~ LEVEL n-1까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - DIFFERENTIAL
        - 'integer'가 n이면 가장 최근에 LEVEL 0 ~ LEVEL n까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - 생략하면 DIFFERENTIAL이 기본으로 지정된다.

<a id="9796c3b12d7209c5"></a>
#### &lt;database controlfile backup statement&gt;

- 제어 파일 (controlfile)을 백업한다.
    - 'target_name'의 이름은 1024 바이트보다 작아야 한다. 
    - 'target_name'이 이미 존재하는 경우 연산에 실패한다. 
- 데이터베이스는 OPEN 상태여야 하고, ARCHIVELOG로 운영되고 있어야 한다.

> GOLDILOCKS에서 관리하는 'target_name' 길이는 최대 1024 바이트이지만, OS마다 최대로 허용하는 파일 이름 길이가 다르기 때문에, 실제 생성가능한 'target_name'의 길이는 1024 바이트보다 작을 수 있다.

<a id="c3cdb2c8e7b8f80d"></a>
#### &lt;domain name&gt;

- 구문을 수행할 멤버나 그룹의 이름이다.
- 지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="5697913069847e35"></a>
### 설명

Database의 datafile과 controlfile을 백업한다. BEGIN BACKUP을 수행한 후 OS의 파일 복사로 datafile들을 복사하고 나서 END BACKUP을 수행하여 database를 전체 백업한다. 한편, 증분 백업 파일은 하나의 구문으로 BACKUP_DIR_1 property에 설정된 경로에 생성한다.

<a id="7aa94cfb3ee91c45"></a>
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

<a id="f545abb439eb5f48"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="bda9b193df20fa46"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#5c95f68797fd85d7)
- [ALTER DATABASE RECOVER](#2e60420db9e1864f)

<a id="d0a56f6310b7a28c"></a>
## ALTER DATABASE CLEAR AUDIT TRAIL

<a id="d00419fda3a63e92"></a>
### 기능

Audit policy 적용으로 인해 누적된 audit record를 삭제 (purge)한다.

<a id="b4c0c558af0283eb"></a>
### 구문

```
<clear audit trail statement> ::= 
    ALTER DATABASE CLEAR AUDIT TRAIL
;
```

<a id="a53a4dc6592b95c8"></a>
### 사용 범위 및 접근 권한

&lt;clear audit trail statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="c82be9052ea096de"></a>
### 설명

Audit policy를 활성화하면 시간이 지남에 따라 audit trail이 계속 커진다.   
Audit trail을 구성하는 테이블들은 MEM_AUX_TBS 테이블스페이스에 저장되는데 audit trail이 계속 커지지 않도록 해야 한다.

<a id="fecfa3b6ddaa04d6"></a>
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

<a id="83014271e1b5f4dd"></a>
### 사용 예

다음 구문을 사용하여 audit trail을 삭제 (purge)한다.

```
ALTER DATABASE CLEAR AUDIT TRAIL;
```

<a id="f1d45fc470d94376"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="28bc7eee6f89e19d"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#09b3895daf4991da)
    - [DROP AUDIT POLICY](#4c985d8424a9c9e1)
    - [ALTER AUDIT POLICY](#241fd4b15c525c5a)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#8c7812c0671b6a25)
    - [NOAUDIT POLICY](#f4896aa89ec963af)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#6c787a4b953e8625)

- Audit trail 삭제: [ALTER DATABASE CLEAR AUDIT TRAIL](#d0a56f6310b7a28c)

<a id="23aa4348abd416d5"></a>
## ALTER DATABASE CLEAR PASSWORD HISTORY

<a id="57a45bd8ab797de9"></a>
### 기능

Profile 적용에 따라 누적된 사용자의 비밀번호 변경 이력을 삭제한다.

<a id="0d3639c3ef61b577"></a>
### 구문

```
<clear password history statement> ::= 
    ALTER DATABASE CLEAR PASSWORD HISTORY
    ;
```

<a id="cf220fd644b7b001"></a>
### 사용 범위 및 접근 권한

&lt;clear password history statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="fdc3d590abb52026"></a>
### 설명

User에 profile을 적용할 때 PASSWORD_REUSE_MAX, PASSWORD_REUSE_TIME의 정책에 따라 사용자의 비밀번호 변경이력이 누적된다.

**변경 이력 관리**

<a id="a651ab5d1b73c639"></a>
| PASSWORD_REUSE_MAX | PASSWORD_REUSE_TIME | 변경 이력 관리 |
| --- | --- | --- |
| value | value | Value 범위 내의 변경 이력만 관리하고 범위를 벗어난 변경 이력은 자동으로 삭제한다. |
| value | UNLIMITED | 모든 변경 이력을 검사해야 하므로 변경 이력을 누적할 뿐 제거하지 않는다. |
| UNLIMITED | value | 모든 변경 이력을 검사해야 하므로 변경 이력을 누적할 뿐 제거하지 않는다. |
| UNLIMITED | UNLIMITED | 변경 이력을 검사하지 않으므로 관리도 하지 않는다. |

&lt;clear password history statement&gt; 구문은 누적된 사용자 비밀번호 변경이력을 삭제한다.

<a id="cd8f48d5c1dc95f3"></a>
### 사용 예

다음은 &lt;clear password history statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE CLEAR PASSWORD HISTORY;

Database altered.

gSQL> COMMIT;

Commit complete.
```

<a id="678ad90938cd75fd"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="19818a81f986d826"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE PROFILE](#aaba451f0d7d6289)
- [CREATE USER](#8e5920c927752802)

<a id="39b6d764690f3b61"></a>
## ALTER DATABASE DATAFILE AUTOEXTEND

<a id="4365d8aa5a1af50d"></a>
### 기능

디스크 테이블스페이스 데이터 파일의 자동 확장 속성을 변경한다. 자동 확장 속성을 ON으로 변경하면 확장시킬 크기와 데이터 파일의 최대 크기도 변경할 수 있다.

<a id="481b424e16a5a1ea"></a>
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

<a id="e2f112fecb34d54b"></a>
### 사용 범위 및 접근 권한

&lt;alter database datafile autoextend statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

데이터 파일 자동 확장 속성은 디스크 테이블스페이스에 한해서만 변경할 수 있다.

<a id="0a171ec91bd83f52"></a>
#### datafile_name

변경할 데이터 파일의 이름을 지정한다.

<a id="3c8de874a2935343"></a>
#### &lt;autoextend clause&gt;

자동 확장 속성을 ON 또는 OFF로 설정한다. ON으로 설정하면 자동 확장 크기와 데이터 파일의 최대 크기를 지정할 수 있다.

<a id="848dddc65c2bad10"></a>
#### &lt;next size clause&gt;

현재 사용 중인 데이터 파일에 더 이상 사용할 공간이 없을 때 확장할 크기를 지정한다.

<a id="4c28f8e0365938c2"></a>
#### &lt;max size clause&gt;

데이터 파일이 확장될 수 있는 최대 크기를 지정한다.

<a id="76e09e4e630e88d9"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="a6c49d38a19b33d1"></a>
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

<a id="6adb3cf24b4341cc"></a>
### 호환성

SQL 표준에서는 데이터 파일에 대한 개념을 정의하지 않고 있다.

<a id="89c3f84a6c115583"></a>
### 참조

관련 내용은 [CREATE DISK DATA TABLESPACE](#f9d7ec4af5a3302c)를 참조한다.

<a id="24fa3bfc96889571"></a>
## ALTER DATABASE DELETE BACKUP

<a id="2269a92e021d79a6"></a>
### 기능

증분 백업 (incremental backup)의 백업 정보와 백업 파일을 삭제한다. Database의 모든 증분 백업을 삭제하거나, 더 이상 쓸모 없는 백업 (obsolete backup)을 선택해서 삭제할 수 있다.

<a id="722e77d5fa2412ee"></a>
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

<a id="ba91e0fb1b05da71"></a>
### 사용 범위 및 접근 권한

&lt;alter database delete backup statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="5d0a9afb195b5b2a"></a>
### 구문 규칙 및 파라미터

<a id="87635a0eee2c00d1"></a>
#### &lt;alter database delete backup statement&gt;

데이터베이스가 MOUNT 또는 OPEN 상태여야 한다.

<a id="c4a37068172ddb55"></a>
#### &lt;delete backup list option&gt;

기존 증분 백업들 중에서 삭제할 대상을 선정한다.

- OBSOLETE: 가장 최근의 데이터베이스 'LEVEL 0' 백업 이전에 백업한 데이터베이스 또는 테이블스페이스 백업본들을 삭제 대상으로 선정한다.
- ALL: 전체 증분 백업들을 삭제 대상으로 선정한다.

<a id="952721dc60533fbb"></a>
#### &lt;including backup file option&gt;

- 생략되면 백업 정보만 제어 파일에서 삭제한다.
- 백업 정보뿐만 아니라 백업 파일들도 함께 삭제한다.

<a id="87d659000ceb3069"></a>
### 설명

OBSOLETE 증분 백업 삭제는 가장 최근의 LEVEL 0 데이터베이스 백업 이전의 증분 백업을 삭제한다. 즉, LEVEL 0이 아닌 증분 백업을 수행할 때는 이전에 수행한 증분 백업을 포함하는 증분 백업이 있더라도 삭제하지 않는다. 왜냐하면 증분 백업을 이용한 불완전 복구를 수행할 때 사용될 수 있기 때문이다.

> 증분 백업을 삭제할 때 백업 파일까지 함께 삭제하면 증분 백업 정보를 포함하는 백업된 controlfile을 이용하더라도 복구를 수행할 수 없으므로 주의해야 한다.

<a id="9875a85726c73df8"></a>
### 사용 예

다음은 기존 모든 증분 백업들의 백업정보와 백업파일들을 삭제하는 예이다.

```
ALTER DATABASE DELETE ALL BACKUP LIST INCLUING BACKUP FILES;
```

<a id="31391cf168276087"></a>
### 호환성

SQL 표준은 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="8a93e35930379b81"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#5c95f68797fd85d7)
- [ALTER DATABASE RECOVER](#2e60420db9e1864f)

<a id="4c6f8df475e24e0c"></a>
## ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS

<a id="57075880cf3ad469"></a>
### 기능

모든 inactive cluster member들을 제거한다.

<a id="123cd65e7f77478b"></a>
### 구문

```
<alter database drop inactive members statement> ::=
    ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS
    ;
```

<a id="9a45449e137b2abd"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database drop inactive cluster members statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="44344c6d5ab9d18f"></a>
### 설명

모든 inactive cluster member들을 제거한다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우 
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

단, cluster member를 제거할 때 table의 shard가 유실되는 경우에는 inactive cluster member를 제거할 수 없다.

&lt;alter database drop inactive members statement&gt; 구문은 모든 inactive cluster member들이 더 이상 cluster system에 포함될 수 없는 경우에 사용하는 것이 바람직하다.

<a id="508b098dd0065f1b"></a>
### 사용 예

다음은 &lt;alter database drop inactive members statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="fca09805601e9a72"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="a01625fc52733903"></a>
### 참조

관련 내용은 [ALTER SYSTEM JOIN DATABASE](#5a78b6da246beb5a) 를 참조한다.

<a id="36106c490d8bf76f"></a>
## ALTER DATABASE DROP LOGFILE

<a id="804507fa97e65246"></a>
### 기능

데이터베이스에 존재하는 로그파일 그룹이나 멤버를 제거한다.

<a id="a681b6f3594f9098"></a>
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

<a id="2943212a846e29c1"></a>
### 사용 범위 및 접근 권한

&lt;alter database drop logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="844cb60ec27491db"></a>
### 구문 규칙 및 파라미터

<a id="fc9854923ab7fedc"></a>
#### &lt;alter database drop logfile statement&gt;

데이터베이스는 MOUNT 상태여야 한다.   
제거하려는 로그파일이 CURRENT 또는 ACTIVE 상태일 때는 에러가 발생한다.   
제거한 후에 최소 네 개의 로그파일 그룹이 남아 있어야 한다.

<a id="7312827586c262c6"></a>
#### &lt;drop logfile group statement&gt;

기존의 로그파일 그룹을 제거한다.

- &lt;group clause&gt; 
    - 제거할 로그파일 그룹을 지정한다.
    - integer는 존재하는 로그파일의 식별자여야 한다. 
    - integer가 존재하지 않을 경우 에러가 발생한다.

<a id="92b10adaae7a8546"></a>
#### &lt;drop logfile member statement&gt;

기존의 로그파일 멤버들을 제거한다.

- &lt;logfile_list&gt;
    - 제거할 로그파일 멤버의 목록이다.
    - 'logfile_name'은 존재하는 이름이어야 한다. 
    - 'logfile_name'이 존재하지 않을 경우 에러가 발생한다.

<a id="fd2ae3f4ef22217e"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="26bb7307a86b8413"></a>
### 사용 예

다음은 기존 로그파일인 GROUP 3을 제거하는 예이다.

```
ALTER DATABASE DROP LOGFILE GROUP 3;
```

다음은 기존 로그파일인 GROUP 3에서 'logfile1.log'와 'logfile2.log'를 제거하는 예이다.

```
ALTER DATABASE DROP LOGFILE MEMBER 'logfile1.log', 'logfile2.log';
```

<a id="a88f22c5c90df25f"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="e899befdf579e775"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#1bb9e8840b302b97)
- [ALTER DATABASE RENAME LOGFILE](#9691ec461f59ba6a)

<a id="da8877ea32a04f66"></a>
## ALTER DATABASE MOVE SHARD

<a id="d0dc66d74ec51f43"></a>
### 기능

특정 cluster group의 모든 table들의 shard를 다른 cluster group으로 재배치한다.

<a id="6fc6bd7cdd2feb24"></a>
### 구문

```
<alter database move shard statement> ::=
    ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP src_cluster_group
        TO CLUSTER GROUP dest_cluster_group [ ONLINE | OFFLINE ];
```

<a id="2d88a4ac387b6706"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database move shard statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="38b09902d25511d0"></a>
### 구문 규칙 및 파라미터

<a id="dfadb7bb539ad45b"></a>
#### src_cluster_group

테이블의 shard를 이동할 cluster group 이다.

<a id="a3bc32910fc708ba"></a>
#### dest_cluster_group

테이블의 shard를 이동시킬 target cluster group이다.

<a id="958912b4119b9fb6"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="6fee3ce964fb885d"></a>
### 설명

다음과 같은 구문을 사용하여 cluster member와 cluster group을 추가할 때 table들의 shard는 재배치하지 않는다.

- [CREATE CLUSTER GROUP](#dd23e8e2eae3991d)
- [ALTER CLUSTER GROUP name ADD MEMBER](#72ed23526a0c9e3b)

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

<a id="7a05c9ead73bddbc"></a>
### 사용 예

다음은 &lt;alter database move shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP G1 TO CLUSTER GROUP G2;

Database altered.
```

<a id="e506622a9803b8fd"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="de3c738628eb7358"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name MOVE SHARD](#5179ebc66a584d79)
- [CREATE CLUSTER GROUP](#dd23e8e2eae3991d)
- [ALTER CLUSTER GROUP name ADD MEMBER](#72ed23526a0c9e3b)

<a id="0398a908126ff22a"></a>
## ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS

<a id="bc7dfd93c6d0be5a"></a>
### 기능

모든 inactive cluster member들을 offline 상태로 변경한다. 즉, 해당 cluster member들에 대한 shard map을 offline 상태로 변경한다.

<a id="65388d41c335b9f8"></a>
### 구문

```
<alter database offline inactive cluster members statement> ::=
    ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS
    ;
```

<a id="b774e35d4a96cd29"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database offline inactive cluster members statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="fed4d7808f538d04"></a>
### 구문 규칙 및 파라미터

모든 inactive cluster member들을 offline 상태로 변경한다.

Cluster member의 inactive 상태는 cluster system과 연결되어 있지 않은 상태로서 다음과 같은 상황에서 발생한다.

- 운영 중인 cluster system에서 해당 cluster member에 장애가 발생한 경우
- 해당 cluster member를 구동하지 않고 cluster system의 start-up을 시도한 경우

<a id="18897cd2afb4b666"></a>
### 설명

&lt;alter database offline inactive members statement&gt; 구문은 모든 inactive cluster member들이 더 이상 cluster system에 포함될 수 없는 경우에 사용하는 것이 바람직하다.

Inactive cluster member가 cluster system에 참여할 수 있으면 [ALTER SYSTEM JOIN DATABASE](#5a78b6da246beb5a) 구문을 수행하여 cluster system에 포함시킨다.

Offline 상태로 변경된 cluster member는 join 후에 다음 구문을 사용하여 online 상태로 다시 변경할 수 있다

- [ALTER DATABASE REBALANCE](#48a2899b3f507f9f)
- [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965)

<a id="0c8d465d43f1813d"></a>
### 사용 예

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;
```

<a id="b038d0fe0bad0de6"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="a7fbcb6516252b9f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER SYSTEM JOIN DATABASE](#5a78b6da246beb5a)
- [ALTER DATABASE REBALANCE](#48a2899b3f507f9f)
- [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965)

<a id="48a2899b3f507f9f"></a>
## ALTER DATABASE REBALANCE

<a id="97681228529f4bb3"></a>
### 기능

모든 table들의 shard를 재배치한다.

<a id="a4ea7918b3ace6f5"></a>
### 구문

```
<alter database rebalance statement> ::=
    ALTER DATABASE REBALANCE [ ONLINE | OFFLINE ];
```

<a id="a519122508997b06"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database rebalance statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="e9486d6a8ac28afb"></a>
### 구문 규칙 및 파라미터

<a id="064f454e36b29fec"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="512a704c13c8bf2c"></a>
### 설명

다음과 같은 구문을 사용하여 cluster member, cluster group을 추가할 때 table들의 shard를 재배치하지 않는다.

- [CREATE CLUSTER GROUP](#dd23e8e2eae3991d)
- [ALTER CLUSTER GROUP name ADD MEMBER](#72ed23526a0c9e3b)

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

<a id="c0d73be30e00aba0"></a>
### 사용 예

다음은 &lt;alter database rebalance statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE REBALANCE;

Database altered.
```

<a id="4d90267ce10b493d"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="b27deb301dc0765b"></a>
### 참조

관련 내용은 [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965)를 참조한다.

<a id="103f334bdbeb3455"></a>
## ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP

<a id="777531f8fe523c78"></a>
### 기능

특정 cluster group에 shard가 포함되지 않도록 모든 테이블의 shard를 재배치한다.

<a id="8f190679377c9a45"></a>
### 구문

```
<alter database rebalance exclude cluster group statement> ::=
    ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP cluster_group_name [ ONLINE | OFFLINE ];
```

<a id="6f18b1390569a8d3"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter database rebalance exclude cluster group statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="f4a58308cf120e0f"></a>
### 구문 규칙 및 파라미터

<a id="dc22e329eb356a84"></a>
#### cluster_group_name

테이블들의 shard를 포함하지 않는 cluster group의 이름이다.  
지정한 cluster group이 유일한 cluster group인 경우 구문을 수행할 수 없다.

<a id="64e3b3c6c701e1ae"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="cc277eabffdad529"></a>
### 설명

[DROP CLUSTER GROUP](#e491103ba644ea1a) 구문을 사용하여 cluster group을 제거하려면 해당 cluster group에 shard가 존재하지 않아야 한다.

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

<a id="bbabb6c52fe0c9c0"></a>
### 사용 예

다음은 &lt;alter database rebalance exclude cluster group statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP g3;

Database altered.
```

<a id="a3e01a2750f984bf"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="9db0096f92444ae8"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP CLUSTER GROUP](#e491103ba644ea1a)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#1baf8de768cb0d19)

<a id="2e60420db9e1864f"></a>
## ALTER DATABASE RECOVER

<a id="90f32d83fbc9c814"></a>
### 기능

온라인/ archive log file을 사용하여 데이터베이스 내의 전체 데이터파일 (datafile) 또는 일부 데이터파일을 복구한다.

<a id="5a64bfe0e6216f56"></a>
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

<a id="3f15645d1b47c89d"></a>
### 사용 범위 및 접근 권한

&lt;alter database recover statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="84bbc7e29d67c459"></a>
### 구문 규칙 및 파라미터

<a id="e2a189a340015136"></a>
#### &lt;complete database recover statement&gt;

온라인 및 archive 로그파일을 이용하여 데이터베이스의 데이터 파일들을 최신 상태로 복구한다.

- ONLINE 상태의 모든 테이블스페이스를 복구한다. 
- 데이터베이스는 MOUNT 상태여야하고, ARCHIVELOG 모드여야 한다. 
- 필요한 archive log file이 존재하지 않으면 실패한다.

<a id="b6e27db0d6a39d53"></a>
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

<a id="76cd2fc546274ece"></a>
#### &lt;complete tablespace recover statement&gt;

테이블스페이스의 데이터 파일들을 최신 상태로 복구한다.

- 테이블스페이스를 복구하려면 데이터베이스가 MOUNT 또는 OPEN 상태여야 한다. 
- OPEN 상태에서의 복구는 OFFLINE 상태의 테이블스페이스만 가능하고, MOUNT 상태에서의 복구는 ONLINE/ OFFLINE 상태의 테이블스페이스 모두 가능하다. 
- 필요한 archive log file이 존재하지 않으면 복구에 실패한다.
- 다음과 같은 경우에는 테이블스페이스 복구 연산이 필요하다.
    - IMMEDIATE 로 OFFLINE 된 테이블스페이스
    - 백업된 데이터 파일을 이용해야 하는 경우
    - 전체 백업중 장애가 발생한 경우

<a id="e8e23eb06d0e2d82"></a>
#### &lt;incomplete database recover statement&gt;

<a id="d2401df284f70b1f"></a>
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

<a id="9dce56923e1163ae"></a>
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

<a id="0fbdf8b949f9c989"></a>
### 설명

데이터베이스 불완전 복구는 복구 완료 시점을 한 번에 찾아내기 어려우므로 여러 번 수행하여 원하는 복구 시점을 찾아야 한다. 그런데 불완전 복구가 완료된 후 RESETLOGS 옵션으로 데이터베이스를 기동하면 새로운 데이터베이스가 되기 때문에 archive log file과 온라인 redo log file에 대한 복사본을 만든 후에 불완전 복구를 여러 번 수행해야 한다.

<a id="f8e67092bea26f0c"></a>
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

<a id="7038c4090a0680ed"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="34c37ff96ea15f35"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#f6306e58c561105b)
- [ALTER TABLESPACE name BACKUP](#5c95f68797fd85d7)
- [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#f9fc4d123ed9181c)

<a id="85b498c49bcc12c8"></a>
## ALTER DATABASE REGISTER

<a id="861c2d6bdd20f6fd"></a>
### 기능

복구 불가능한 세그먼트를 데이터베이스에 등록한다.

<a id="57e9ed2adc7976ba"></a>
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

<a id="0dfc9d2f6051b107"></a>
### 사용 범위 및 접근 권한

&lt;alter database register statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="3f8aa796a3cdd43e"></a>
### 구문 규칙 및 파라미터

<a id="0d33a2abbaa7e07b"></a>
#### &lt;alter database register statement&gt;

복구 불가능한 세그먼트를 데이터베이스에 등록한다. 해당 구문은 백업이 존재하지 않고 데이터베이스를 복구할 수 없는 경우, 세그먼트를 더 이상 사용하지 않는다는 가정하에 사용될 수 있다.

- 데이터베이스가 MOUNT 상태여야 한다.
- 등록된 세그먼트 식별자 목록은 재시작할 때 초기화된다.
- 서버 재시작에 성공하면 등록된 세그먼트들이 'UNUSABLE' 상태가 되는데 해당 세그먼트들은 반드시 삭제해야 한다.

<a id="e360c9c3008fcfb5"></a>
#### &lt;segment physical identifier list&gt;

복구 불가능한 세그먼트의 식별자 목록이다.  
• Integer: 8 바이트 정수형의 세그먼트 식별자

<a id="e498786c0f077300"></a>
### 설명

서버를 비정상 종료하고 재시작할 때 데이터베이스를 복구하는데, 이 때 이전 서비스 단계에서 디스크에 반영되지 못한 페이지들을 복구하기 위해서 REDO 로그들을 이용해 페이지를 다시 수행한다.

REDO 연산을 수행하는 중에 예상하지 못한 실패가 발생한 경우, 이를 무시하고 복구하기 위해 사용될 수 있다.

<a id="aa3f036a432a38f5"></a>
### 사용 예

다음은 4028679323648을 식별자로 갖는 세그먼트 복구를 포기하는 예이다.

```
ALTER DATABASE REGISTER IRRECOVERABLE SEGMENT 4028679323648;
```

<a id="8a71c35d97b0856e"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="6e4f11532723d6d1"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE name BACKUP](#5c95f68797fd85d7)
- [ALTER DATABASE RECOVER](#2e60420db9e1864f)

<a id="9691ec461f59ba6a"></a>
## ALTER DATABASE RENAME LOGFILE

<a id="30def5b25eb55418"></a>
### 기능

데이터베이스에서 로그파일의 이름을 수정한다.

<a id="8f0494e5c432fb0d"></a>
### 구문

```
<alter database rename logfile statement> ::=
    ALTER DATABASE RENAME LOGFILE <logfile_list> TO <logfile_list>
    ;

<logfile_list> ::=
      'logfile_name'
    | <logfile_list> , 'logfile_name'
```

<a id="f489dcc80951ff45"></a>
### 사용 범위 및 접근 권한

&lt;alter database rename logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="0345a607e7c12b7a"></a>
### 구문 규칙 및 파라미터

<a id="3a4d43f4496c074a"></a>
#### &lt;alter database rename logfile statement&gt;

- 데이터베이스는 MOUNT 상태여야 한다.
- FROM &lt;logfile_list&gt;
    - 데이터베이스에서 수정할 로그파일들의 이름 목록이다.
- TO &lt;logfile_list&gt;
    - 데이터베이스에서 수정될 로그파일들의 이름 목록이다.
    - &lt;logfile_list&gt;는 존재하는 파일이어야 한다. 
    - 파일이 존재하지 않을 경우 에러가 발생한다.

<a id="f7823109ed8953bd"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="7c310d2c95450034"></a>
### 사용 예

다음은 기존 로그파일 'logfile.log'를 'newlogfile.log'로 변경하는 예이다.

```
ALTER DATABASE RENAME LOGFILE 'logfile.log' TO 'newlogfile.log';
```

<a id="d3e4711396785810"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="f54c53d9aa88811d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE ADD LOGFILE](#1bb9e8840b302b97)
- [ALTER DATABASE DROP LOGFILE](#36106c490d8bf76f)

<a id="00c55783ca905023"></a>
## ALTER DATABASE RESET LOCAL CLUSTER MEMBER

<a id="5d25ab572cf8d477"></a>
### 기능

Local cluster member에서 tablespace 객체를 제외한 부분을 database 생성 시점으로 초기화한다.

<a id="37d26db8742241f5"></a>
### 구문

```
<alter database reset local cluster member statement> ::=
    ALTER DATABASE RESET LOCAL CLUSTER MEMBER
    ;
```

<a id="a5a55c43f00eedc9"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

Start-up 과정 중 LOCAL OPEN 단계에서 수행할 수 있다.

&lt;alter database reset local cluster member statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="0324d734a305138f"></a>
### 설명

Local cluster member에서 tablespace 객체를 제외한 부분을 database 생성 시점으로 초기화한다.  
Tablespace 객체를 제외하고 사용자가 생성한 모든 객체를 제거한다.

&lt;alter database reset local cluster member statement&gt; 구문은 inactive cluster member를 초기화하고,  
새로운 cluster member를 cluster system에 참여시키기 위해 사용한다.  
Cluster system과 연결이 끊긴 inactive cluster member들은 다음과 같이 처리할 수 있다.

- Cluster system에 다시 참여할 수 있는 경우, JOIN 구문을 이용하여 참여시킨다. 
    - [ALTER SYSTEM JOIN DATABASE](#5a78b6da246beb5a) 
- Cluster system에 다시 참여할 수 없는 경우, DROP 구문을 이용하여 cluster system에서 제외한다. 
    - [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#4c6f8df475e24e0c)

이 때, cluster system에서 제외된 cluster member에 해당하는 장비는 다음 두 가지 방법으로 재사용할 수 있다.

- 방법 1: Local cluster member의 database를 다시 생성한다.
- 방법 2: &lt;alter database reset local cluster member statement&gt; 구문을 이용해 local cluster member를 초기화한다.

방법 2는 방법 1보다 tablespace를 재생성하는 비용을 줄일 수 있다.

<a id="8e65d59d29078239"></a>
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

<a id="14536fea0dcfd70b"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="f31d9046ea882b7d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER SYSTEM JOIN DATABASE](#5a78b6da246beb5a)
- [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#4c6f8df475e24e0c)

<a id="1905dbe34e65c587"></a>
## ALTER DATABASE RESTORE

<a id="20c47204a9b55dd9"></a>
### 기능

증분 백업을 이용하여 데이터베이스 또는 테이블스페이스 내의 데이터 파일들을 복원한다.

<a id="d46e0fd06e3eed80"></a>
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

<a id="6f4b36474bb9358f"></a>
### 사용 범위 및 접근 권한

alter database restore statement> 구문을 수행하려면 사용자에게 ALTER DATABASE ON DATABASE 권한이 있어야 한다.

<a id="31a503b1d310259f"></a>
### 구문 규칙 및 파라미터

<a id="5507a9ab3f51538f"></a>
#### &lt;database restore statement&gt;

증분 백업을 사용하여 데이터베이스 내의 데이터 파일들을 복원한다.   
데이터베이스가 MOUNT 상태여야 한다.

<a id="e8459cbdb5568acf"></a>
#### &lt;tablespace restore statement&gt;

증분 백업을 사용하여 테이블스페이스 내의 데이터 파일들을 복원한다.

- 데이터베이스가 MOUNT 또는 OPEN 상태여야 한다. 
- OPEN 상태에서는 OFFLINE 상태의 테이블스페이스만 복원할 수 있고, MOUNT 상태에서는 ONLINE/ OFFLINE 상태의 테이블스페이스 모두 복원할 수 있다.

<a id="35c994d377c6b12e"></a>
#### &lt;controlfile restore statement&gt;

'file_name'을 사용하여 제어파일을 복원한다.

- 데이터베이스가 NOMOUNT 상태여야 한다.
- 'file_name'은 절대 경로를 권장하지만, 만약 상대 경로를 기술한 경우에는 &lt;GOLDILOCKS_HOME&gt;/wal/'file_name'을 이용한다.

<a id="0b1d83cec87b143e"></a>
### 설명

전체 백업을 이용한 데이터 파일 복원은 OS 복사 명령으로 백업된 파일을 직접 데이터 파일 경로에 복사하는 방법이다. 증분 백업을 이용한 데이터 파일 복원은 삭제된 데이터 파일이나 이전 데이터 파일들만 복원한다.

<a id="3de80dc61a4c8b08"></a>
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

<a id="a2bc3f70188aced0"></a>
### 호환성

SQL 표준에서는 ALTER DATABASE 구문을 정의하지 않고 있다.

<a id="70dd48f1cd427e60"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER DATABASE BACKUP](#f6306e58c561105b)
- [ALTER TABLESPACE name BACKUP](#5c95f68797fd85d7)
- [ALTER DATABASE RECOVER](#2e60420db9e1864f)

<a id="90ee0a3fcc3d995c"></a>
## ALTER INDEX

<a id="b3d61a6624b418f0"></a>
### 기능

인덱스 정의를 변경한다.

<a id="71bbbf36301e48ed"></a>
### 구문

```
<alter index statement> ::=
      <alter index physical attribute statement>
    | <rename index statement>
    | <aging index statement>
    | <rebuild statement>
    ;
```

<a id="cc3fff2c0c9d41b3"></a>
### 사용 범위 및 접근 권한

&lt;alter index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="c0e6afe42a06dc8e"></a>
### 구문 규칙 및 파라미터

<a id="3cebb99770130560"></a>
#### &lt;alter index physical attribute statement&gt;

인덱스의 물리적 속성을 변경한다.  
자세한 내용은 [ALTER INDEX name STORAGE](#64eb8c9b0ab41e80) 구문을 참조한다.

<a id="d1c9e3fc86ee9579"></a>
#### &lt;rename index statement&gt;

인덱스 이름을 변경한다.  
자세한 내용은 [ALTER INDEX name RENAME TO](#0908608fc2f457cb) 구문을 참조한다.

<a id="dd45f4321ef76c43"></a>
#### &lt;aging statement&gt;

인덱스의 빈 페이지를 삭제한다.  
자세한 내용은 [ALTER INDEX name AGING](#497a042a5d2691d3) 구문을 참조한다.

<a id="f98cf2e950dde303"></a>
#### &lt;rebuild statement&gt;

인덱스를 재구축한다.  
자세한 내용은 [ALTER INDEX name REBUILD](#0c9fcc7fd3031814) 구문을 참조한다.

<a id="e6f3022372c25a33"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="e487f7fbdbaa9948"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="7b985df20ff82140"></a>
### 호환성

SQL 표준에서는 인덱스에 대한 개념을 다루지 않고 있다.

<a id="497a042a5d2691d3"></a>
## ALTER INDEX name AGING

<a id="7664155d814daea9"></a>
### 기능

인덱스의 빈 페이지를 삭제한다.

<a id="6ce86204343ce848"></a>
### 구문

```
<aging index statement> ::=
    ALTER INDEX index_name AGING
    ;
```

<a id="4fcc2f77aebd41e9"></a>
### 사용 범위 및 접근 권한

&lt;aging index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="bc4ed4c455b18d50"></a>
### 구문 규칙 및 파라미터

<a id="85e6d7ed11e40b47"></a>
#### index_name

대상 인덱스의 이름이다.

<a id="dc6ddc80593c91a3"></a>
### 설명

해당 구문은 인덱스 페이지들 중에 모든 키가 삭제된 페이지들을 세그먼트로 반납한다. Aging은 논리적 삭제와 물리적 삭제의 2단계로 진행된다. 논리적 삭제는 인덱스에서 페이지를 지칭하는 연결을 끊는 작업이며 페이지의 마지막 키를 삭제할 당시의 SCN이 시스템의 agable SCN보다 작을 때 수행된다. 이후 물리적 삭제가 이루어지는데 논리적으로 삭제할 때의 SCN이 시스템의 agable SCN보다 작을 때 수행된다.

> 만약 시스템의 agable SCN이 증가하지 않으면 인덱스 AGING 구문이 성공하더라도 빈 페이지가 삭제되지 않을 수 있다.

<a id="245b8e471558800d"></a>
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

<a id="2e96febaf0e704d1"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="945094af7917fd05"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](#9d2795ea1fc7b4c6)
- [ALTER INDEX](#90ee0a3fcc3d995c)
- [DROP INDEX](#8921114ccac5a25e)

<a id="0c9fcc7fd3031814"></a>
## ALTER INDEX name REBUILD

<a id="ebefc3685d643145"></a>
### 기능

인덱스를 재구축한다.

<a id="c315fb6e54f0b091"></a>
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

<a id="852eb05a587e932f"></a>
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

<a id="e0a97da8ad71cc0b"></a>
### 구문 규칙 및 파라미터

<a id="adaab09b517e2de7"></a>
#### index_name

대상 인덱스의 이름이다.  
스키마 이름을 명시할 수 있으며, 생략할 경우 사용자의 기본 스키마 이름이 사용된다.

<a id="b72ef83c438119de"></a>
#### [ ONLINE | OFFLINE ]

인덱스를 재구축할 때, 해당 테이블에 DML을 허용할지 여부를 결정한다.

- ONLINE
    - INSERT, UPDATE, DELETE를 허용한다.
- OFFLINE
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE이다.

<a id="629d127dd28dbdb8"></a>
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

<a id="1f5af9fcca6140f0"></a>
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

<a id="10a4d0ba7316192a"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="f86212ea53767418"></a>
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

<a id="1d8235db684d2f79"></a>
#### TABLESPACE tablespace_name

인덱스가 재구축될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - tablespace_name이 data tablespace면 LOGGING 인덱스로 재구축된다.
    - tablespace_name이 temporary tablespace 또는 nologging tablespace면 NOLOGGING 인덱스로 재구축된다.
- TABLESPACE 절을 생략할 경우, 기존 인덱스의 tablespace로 설정된다.

<a id="f4e5a3980a7bd3cb"></a>
### 설명

- 인덱스 단편화 제거
    - 인덱스에 DML이 빈번하게 수행되는 경우, 인덱스 페이지에 단편화가 발생할 수 있다. 유효한 데이터에 비해 트리가 지나치게 커진 경우, 인덱스 용량은 커지고 성능은 하락한다. 이 경우 인덱스를 재구축하면 인덱스 페이지의 단편화를 해결하여 인덱스 용량을 줄이고 인덱스의 성능을 회복할 수 있다.
- 인덱스의 테이블스페이스 변경
    - 기존에 생성된 인덱스의 테이블스페이스를 변경할 수 있다.
    - 단, 테이블스페이스의 TEMPORARY 여부에 따라 로깅 여부를 적절하게 설정해주어야 한다.
- 인덱스의 로깅 설정 변경
    - LOGGING 인덱스로 변경하려면, data tablespace를 TABLESPACE 옵션에 지정해줘야 한다.
    - NOLOGGING 인덱스로 변경하려면, temporary tablespace 또는 nologging tablespace를 TABLESPACE 옵션에 지정해줘야 한다.

<a id="2a5c0c32d81778cb"></a>
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

<a id="90408e6e5ceead4d"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="98d82b03b5aac543"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](#9d2795ea1fc7b4c6)
- [ALTER INDEX](#90ee0a3fcc3d995c)
- [DROP INDEX](#8921114ccac5a25e)

<a id="0908608fc2f457cb"></a>
## ALTER INDEX name RENAME TO

<a id="774e067bda573614"></a>
### 기능

인덱스의 이름을 변경한다.

<a id="fe6bbe3901153257"></a>
### 구문

```
<rename index statement> ::=
    ALTER INDEX index_name
        RENAME TO new_index_name
    ;
```

<a id="24f5e2cdfafa5850"></a>
### 사용 범위 및 접근 권한

&lt;rename index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="ab5705cfd21d2d8e"></a>
### 구문 규칙 및 파라미터

<a id="f6e246d6c5ba75a7"></a>
#### index_name

대상 인덱스의 이름이다.  
스키마 이름을 기술할 수 없으며, 기존 인덱스와 동일한 스키마 이름을 갖는다.

<a id="55b3b5fb63354581"></a>
#### new_index_name

새로운 인덱스의 이름이며 스키마 내에서 유일한 인덱스 이름이어야 한다.

<a id="c3d9f756b8eba352"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="c72bdcfb5eaa9958"></a>
### 사용 예

다음은 인덱스의 이름을 변경하는 예이다.

```
gSQL> ALTER INDEX t1_idx1 RENAME TO idx_t1_id;

Index altered.
```

<a id="e27c5177b16607eb"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="152f5a4d7d7bc4fa"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](#9d2795ea1fc7b4c6)
- [ALTER INDEX](#90ee0a3fcc3d995c)
- [DROP INDEX](#8921114ccac5a25e)

<a id="64eb8c9b0ab41e80"></a>
## ALTER INDEX name STORAGE

<a id="1435abbeea680bb0"></a>
### 기능

인덱스의 물리적 속성을 변경한다.

<a id="79227c9faad4e328"></a>
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

<a id="2c2cbe2ce53706c8"></a>
### 사용 범위 및 접근 권한

&lt;alter index physical attribute statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (ALTER INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY INDEX ON DATABASE

<a id="31ad9c3ca32dd999"></a>
### 구문 규칙 및 파라미터

<a id="188e2eb05bbf50a6"></a>
#### index_name

대상 인덱스의 이름이다.

<a id="284b4c5aabfa7bb2"></a>
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

<a id="0ef88a930bb453f6"></a>
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

<a id="c71e9b8a5fb7c7b3"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: kilobytes 
- M: megabytes 
- G: gigabytes 
- T: terabytes

<a id="8b0477d73fb8a60e"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="6255114d97b50cc3"></a>
### 사용 예

다음은 인덱스의 물리적 속성을 변경하는 예이다.

```
gSQL> ALTER INDEX idx_t1_id PCTFREE 10 INITRANS 4 MAXTRANS 8;

Index altered.
```

<a id="e331e0ae4236439c"></a>
### 호환성

SQL 표준은 인덱스에 대한 개념을 다루지 않고 있다.

<a id="2e6e4058789309d8"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](#9d2795ea1fc7b4c6)
- [ALTER INDEX](#90ee0a3fcc3d995c)
- [DROP INDEX](#8921114ccac5a25e)

<a id="707c01f0b15f9ab0"></a>
## ALTER PROFILE

<a id="596aa4d2592071ef"></a>
### 기능

비밀번호 관리 방법을 변경한다.

<a id="4c56fc2ea31edcb1"></a>
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

<a id="3c0d8e8cb107f49c"></a>
### 사용 범위 및 접근 권한

&lt;alter profile statement&gt; 구문을 수행하려면 사용자에게 ALTER PROFILE ON DATABASE 권한이 있어야 한다.

<a id="9745ff9e7c1e04cc"></a>
### 구문 규칙 및 파라미터

<a id="632dea01ce345edd"></a>
#### profile_name

변경할 profile의 이름이다.

<a id="13c57da009fe4255"></a>
#### FAILED_LOGIN_ATTEMPTS

로그인 연속 실패 허용 횟수를 설정한다.  
자세한 내용은 [CREATE PROFILE](#aaba451f0d7d6289) 구문을 참조한다.

<a id="989bc08cca6365ea"></a>
#### PASSWORD_LOCK_TIME

로그인에 연속적으로 실패한 후에 계정이 잠기는 기간 (day)을 설정한다.  
자세한 내용은 [CREATE PROFILE](#aaba451f0d7d6289) 구문을 참조한다.

<a id="45130b6be8d85823"></a>
#### PASSWORD_LIFE_TIME

비밀번호의 유효 기간 (day)을 설정한다.  
자세한 내용은 [CREATE PROFILE](#aaba451f0d7d6289) 구문을 참조한다.

<a id="ee7136adab32e7b9"></a>
#### PASSWORD_GRACE_TIME

PASSWORD_LIFE_TIME 이후에 로그인 할 때 비밀번호 만료를 유예하는 기간을 설정한다.  
자세한 내용은 [CREATE PROFILE](#aaba451f0d7d6289) 구문을 참조한다.

<a id="6aeda14f3571ae6a"></a>
#### PASSWORD_REUSE_MAX

이전 비밀번호를 재사용하려 할 때 재사용할 수 없는 최근 비밀번호 개수를 명시한다.  
자세한 내용은 [CREATE PROFILE](#aaba451f0d7d6289) 구문을 참조한다.

<a id="66cd299bfc2adc0d"></a>
#### PASSWORD_REUSE_TIME

이전 비밀번호를 재사용하기 위해 필요한 경과 기간을 명시한다.  
자세한 내용은 [CREATE PROFILE](#aaba451f0d7d6289) 구문을 참조한다.

<a id="44ba9eec60dd86d0"></a>
#### PASSWORD_VERIFY_FUNCTION

비밀번호 복잡도 검증 방법을 설정한다.  
자세한 내용은 [CREATE PROFILE](#aaba451f0d7d6289) 구문을 참조한다.

<a id="8f1b93ee7a3d644b"></a>
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

<a id="3fd4e73ebe1fde0c"></a>
### 호환성

SQL 표준은 profile에 대한 개념을 다루지 않고 있다.

<a id="408d6826661f893e"></a>
### 참조

관련 내용은 [DROP PROFILE](#317a2852ef6da864)을 참조한다.

<a id="ebac80e511ac5859"></a>
## ALTER SEQUENCE

<a id="fa5436f45b6f3cc0"></a>
### 기능

시퀀스를 변경한다.

<a id="eb63359a45861702"></a>
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

<a id="ae389d3de44607e1"></a>
### 사용 범위 및 접근 권한

&lt;alter sequence generator statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 시퀀스의 소유자 
- 시퀀스가 속한 스키마에 대해 (ALTER SEQUENCE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY SEQUENCE ON DATABASE

<a id="8d909732aa8e832b"></a>
### 구문 규칙 및 파라미터

<a id="970281f131be06a6"></a>
#### sequence_name

변경할 시퀀스의 이름이다.  
schema_name.sequence_name과 같이 시퀀스가 속할 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="07e03eaaef5a0cdd"></a>
#### &lt;alter sequence generator restart option&gt;

시퀀스의 다음 값 (NEXT VALUE)을 설정한다.  
단, [CREATE SEQUENCE](#2eb16f80ff00b702) 구문에서 정의한 START WITH의 값은 변경하지 않는다.

- RESTART 
    - 값을 명시하지 않을 경우, &lt;sequence generator definition&gt; 에서 정의한 START WITH의 값이 시퀀스의 다음 값으로 설정된다. 
- RESTART WITH integer 
    - integer 값을 시퀀스의 다음 값으로 설정한다. 
    - integer 값은 MINVALUE와 MAXVALUE 사이의 값이어야 한다.

&lt;alter sequence generator restart option&gt; 절을 명시하지 않은 경우, 시퀀스의 현재값을 기준으로 시퀀스의 속성을 변경한다.

<a id="e52eab26364f9b9b"></a>
#### &lt;sequence generator increment by option&gt;

시퀀스 번호의 간격을 변경한다.  
다음과 같은 제약과 특징을 갖는다.

- 양수 또는 음수를 사용할 수 있으며, 0은 사용할 수 없다. 
- 간격의 절대값은 MINVALUE와 MAXVALUE의 차이보다 작아야 한다. 
- 양수일 경우 오름차순 시퀀스가 되고 음수일 경우 내림차순 시퀀스가 된다.

<a id="b371dfe13add1536"></a>
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

<a id="5fd202449631cd4f"></a>
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

<a id="3092bb90d2781d57"></a>
#### &lt;sequence generator cycle option&gt;

시퀀스의 값이 최대값 또는 최소값이 되었을 때, 계속 값을 생성할지 여부를 변경한다.

- CYCLE 
    - 오름차순 시퀀스가 최대값이 되었을 때, 최소값부터 다시 생성한다. 
    - 내림차순 시퀀스가 최소값이 되었을 때, 최대값부터 다시 생성한다. 
- NO CYCLE | NOCYCLE 
    - 최대값 또는 최소값이 되었을 때, 시퀀스 값을 생성할 수 없다. 
    - NO CYCLE (SQL 표준)과 NOCYCLE은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다.

<a id="ab45bd891f63eb50"></a>
#### &lt;sequence generator cache option&gt;

시퀀스에 신속하게 접근하기 위해 메모리상에 미리 적재할 시퀀스 값의 개수를 정의한다.   
Database를 재구동할 때, 메모리상에 적재한 시퀀스 값은 유실되고 적재한 이후의 값부터 시작된다.

- CACHE integer 
    - CACHE 값은 2와 같거나 커야하고 
    - CYCLE이 존재할 경우 CACHE 값이 CYCLE의 길이보다 크지 않아야 한다. 
        - CYCLE의 길이: CEIL(MAXVALUE - MINVALUE) / ABS(INCREMENT) 
- NO CACHE | NOCACHE 
    - 메모리 상에 시퀀스값을 미리 적재하지 않는다.

<a id="4d1ef87cb265eab3"></a>
### 설명

[CREATE SEQUENCE](#2eb16f80ff00b702) 구문에서 정의한 시퀀스 속성 중 START WITH는 변경할 수 없다.  
START WITH 속성을 변경하려면 [DROP SEQUENCE](#8c2068e78d2e75d6) 구문을 수행한 후에 [CREATE SEQUENCE](#2eb16f80ff00b702) 구문을 사용하여 다시 생성해야 한다.

<a id="da6afdfc299a5273"></a>
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

<a id="ea4e5359d05db4b0"></a>
### 호환성

SQL 표준에서는 CACHE/ NO CACHE 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="b0735d4a024bf245"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T176 | Sequence generator support | O |
| T177 | Sequence generator support: simple restart option | O |

<a id="f8949f34623c796e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE SEQUENCE](#2eb16f80ff00b702)
- [DROP SEQUENCE](#8c2068e78d2e75d6)

<a id="abcf1394381770e3"></a>
## ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

<a id="57496390157d4ef6"></a>
### 기능

세션에서 재사용하기 위해 catching 된 모든 공간들을 해당 tablespace로 반환한다.

<a id="eed195985b54d46e"></a>
### 구문

```
<alter session cleanup global temporary segment pool statement> ::=
    ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL
    ;
```

<a id="4adc3bb73a3f5c82"></a>
### 설명

수행된 세션에서 segment cache의 segment들만 cleanup한다.

<a id="411c6146b95b8595"></a>
### 사용 예

다음은 세션 segment cache를 cleanup하는 예이다.

```
gSQL> ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

Session altered.
```

<a id="879a5172345957d9"></a>
### 호환성

SQL 표준에서는 global temporary table, global temporary index의 segment cache 개념을 정의하지 않고 있다.

<a id="66b09666c3f8592e"></a>
### 참조

관련 내용은 [Global Temporary Table](13-sql-objects.md#c77c3cc72479afba) 을 참조한다.

<a id="4b18743f121b279d"></a>
## ALTER SESSION SET property_name

<a id="67dbfb0dc11dfec3"></a>
### 기능

세션의 프로퍼티 값을 설정한다.

<a id="0a7a341537f135f3"></a>
### 구문

```
<alter session set statement> ::=
    ALTER SESSION SET <property name> { = <property value> | TO DEFAULT }
    ;
```

<a id="ba741baae93e916a"></a>
### 구문 규칙 및 파라미터

<a id="222ba988b6dc959a"></a>
#### &lt;property name&gt;

설정할 프로퍼티 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5892e8fc0b188208) 장을 참조한다.

<a id="47773e720d85383a"></a>
#### &lt;property value&gt;

설정할 프로퍼티 값이다.

<a id="5f606a990db07ebc"></a>
#### TO DEFAULT

세션 프로퍼티 값을 시스템 프로퍼티 값으로 설정한다.

<a id="f834520283c9d85c"></a>
### 설명

각 property에 대한 자세한 설명은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5892e8fc0b188208) 장을 참조한다.

<a id="3923c66cc72b9235"></a>
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

<a id="26f849d54f136bf6"></a>
### 호환성

SQL 표준에서는 세션 프로퍼티 개념을 정의하지 않고 있다.

<a id="e11ad43acaaef9c0"></a>
### 참조

관련 내용은 [ALTER SESSION SET property_name](#4b18743f121b279d) 을 참조한다.

<a id="f537f3a18b12d31a"></a>
## ALTER SYSTEM CHECKPOINT

<a id="43701adc30fbf492"></a>
### 기능

CHECKPOINT를 수행한다.

<a id="c3341a3b75331020"></a>
### 구문

```
<alter system checkpoint statement> ::=
    ALTER SYSTEM CHECKPOINT
    [ AT <domain name> ]
    ;
```

<a id="163f715287b7b5be"></a>
### 사용 범위 및 접근 권한

&lt;alter system checkpoint statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="a65a1d996acc28f5"></a>
### 구문 규칙 및 파라미터

<a id="44149fb7c192004d"></a>
#### &lt;alter system checkpoint statement&gt;

CHECKPOINT는 commit 된 트랜잭션들이 변경한 모든 데이터가 디스크에 기록되는 것을 보장하는 연산이다.

- 데이터베이스가 OPEN 상태여야 한다.
- 데이터베이스가 TDS 모드여야 한다.
- 전체 백업이 진행중일 때는 변경된 페이지가 데이터 파일에 기록되지 않고, REDO 로그와 제어파일만 디스크에 기록된다. 만약 이러한 상태에서 서버가 비정상 종료되는 경우에는 미디어 복구를 수행해야 한다.

<a id="28bc1894f7b5ae78"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="5a372ce0870d6686"></a>
### 설명

체크포인트 (checkpoint) 연산은 commit 된 트랜잭션들이 변경한 모든 내용을 디스크에 기록함으로써 시스템 장애시 신속한 복구를 가능하게 한다.

<a id="accab27c8fd7eae5"></a>
### 사용 예

다음은 CHECKPOINT를 수행하는 예이다.

```
ALTER SYSTEM CHECKPOINT;
```

<a id="dddb28df2cdaf8d4"></a>
### 호환성

SQL 표준에서는 CHECKPOINT 개념을 정의하지 않고 있다.

<a id="149cfe4dd51fd012"></a>
## ALTER SYSTEM CLEANUP BUFFER_CACHE

<a id="676b4f5c2a9ceacd"></a>
### 기능

Buffer cache에서 free 가능한 모든 buffer page들을 비운다.

<a id="4f63a5f28e4c85e6"></a>
### 구문

```
<alter system cleanup buffer_cache statement> ::=
    ALTER SYSTEM CLEANUP BUFFER_CACHE
    [ AT <domain name> ]
    ;
```

<a id="41e351920b40dcf3"></a>
### 사용 범위 및 접근 권한

&lt;alter system cleanup buffer_cache statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="913e441400385e6f"></a>
### 구문 규칙 및 파라미터

<a id="d066e9ec4c6ccc69"></a>
#### &lt;alter system cleanup buffer_cache statement&gt;

해당 구문 규칙이나 파라미터가 존재하지 않는다.

<a id="f7ac60d257209541"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="9a7c5feb21eb6048"></a>
### 설명

Buffer에 캐시된 free 가능한 모든 buffer page들을 flush하고 free 한다.

> 성능 측정 전에 buffer cache를 비우는 목적으로 사용해야 한다.   
> 운영 중인 서버에서 사용할 경우 성능에 치명적인 영향을 미칠 수 있다.

<a id="6319c6977d70deac"></a>
### 사용 예

다음은 CLEANUP BUFFER_CACHE을 수행하는 예이다.

```
ALTER SYSTEM CLEANUP BUFFER_CACHE;
```

<a id="f49c3d5d82a3ba14"></a>
### 호환성

SQL 표준에서는 CLEANUP BUFFER_CACHE의 개념을 정의하지 않고 있다.

<a id="5128a58fea3e9942"></a>
## ALTER SYSTEM CLEANUP PLAN

<a id="81b0c928de6b1e7f"></a>
### 기능

모든 SQL plan을 정리한다.

<a id="604c89f4219a1dd7"></a>
### 구문

```
<alter system cleanup plan statement> ::=
    ALTER SYSTEM CLEANUP PLAN
    [ AT <domain name> ]
    ;
```

<a id="f9a806888375dbc5"></a>
### 사용 범위 및 접근 권한

&lt;alter system cleanup plan statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="b8a0c39f415ac636"></a>
### 구문 규칙 및 파라미터

<a id="a8c2089b89313ed2"></a>
#### &lt;alter system cleanup plan statement&gt;

해당 구문 규칙이나 파라미터가 존재하지 않는다.

<a id="3a87ee661dfaf174"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="6caeaa67d4452280"></a>
### 설명

캐시되어 있는 모든 SQL plan을 정리한다.   
단, V$SQL_CACHE.REF_COUNT가 0보다 큰 plan (prepare된 statement에서 참조하는 plan)들은 정리 대상에서 제외한다.

<a id="2078773658e1413a"></a>
### 사용 예

다음은 CLEANUP PLAN을 수행하는 예이다.

```
ALTER SYSTEM CLEANUP PLAN;
```

<a id="a91c306518554f1c"></a>
### 호환성

SQL 표준에서는 CLEANUP PLAN의 개념을 정의하지 않고 있다.

<a id="ca43914f3c6067d6"></a>
## ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER

<a id="5b0eb65952375a63"></a>
### 기능

복구 불가능한 클러스터 멤버를 지정한다.

<a id="f182dd1cf3b3ac13"></a>
### 구문

```
<alter system irrecoverable cluster member statement> ::=
    ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER <domain name>
    ;
```

<a id="4a31944feb6e81cf"></a>
### 사용 범위 및 접근 권한

&lt;alter system irrecoverable cluster member statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="d16e0bb9b6ea0739"></a>
### 구문 규칙 및 파라미터

<a id="97c87d2c39dee8a9"></a>
#### &lt;alter system irrecoverable cluster member statement&gt;

해당 구문 규칙이나 파라미터가 존재하지 않는다.

<a id="c776554cf43b7c5c"></a>
#### &lt;domain name&gt;

복구 불가능한 멤버 이름이다.  
그룹 내의 모든 멤버들을 복구 불가한 멤버로 지정할 수 없다.

<a id="a2f6a90389fa875d"></a>
### 설명

복구 불가능한 멤버로 인해 클러스터 재시작에 실패하는 경우 해당 멤버를 제외하고 시스템을 재시작하기 위해 사용한다. 시스템 재시작에 성공한 후에는 반드시 [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#4c6f8df475e24e0c) 구문을 이용해 해당 멤버를 삭제해야 한다.

<a id="0e1b0e6a0780fe3a"></a>
### 사용 예

다음은 IRRECOVERABLE CLUSTER MEMBER를 수행하는 예이다.

```
gSQL> ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER g1n1;
```

<a id="adbc0941cf9b02ad"></a>
### 호환성

SQL 표준에서는 IRRECOVERABLE CLUSTER MEMBER의 개념을 정의하지 않고 있다.

<a id="5a78b6da246beb5a"></a>
## ALTER SYSTEM JOIN DATABASE

<a id="b90960c386ac84b3"></a>
### 기능

비활성화된 특정 cluster member를 cluster system에 다시 포함한다.

<a id="c2707e258fba85e3"></a>
### 구문

```
<alter system join database statement> ::=
    ALTER SYSTEM JOIN DATABASE 
    ;
```

<a id="20d310a2fa415fd9"></a>
### 사용 범위 및 접근 권한

Cluster system 에서 수행할 수 있다.

&lt;alter system join database statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="160f85fb17b1b3f0"></a>
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

<a id="72e30a67339be207"></a>
### 사용 예

```
gSQL> ALTER SYSTEM JOIN DATABASE;
```

<a id="57841d854c8dc68c"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="1a75f5fddfcedd88"></a>
### 참조

관련 내용은 [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#4c6f8df475e24e0c)를 참조한다.

<a id="3a477be27663df5b"></a>
## ALTER SYSTEM [KILL | DISCONNECT] SESSION

<a id="4232d5f5dd207180"></a>
### 기능

세션을 종료한다.

<a id="9f7dfe0c62834ebf"></a>
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

<a id="955dc49a9aff7e0a"></a>
### 사용 범위 및 접근 권한

&lt;alter system end session statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="5dfb111cac9dcd2c"></a>
### 구문 규칙 및 파라미터

<a id="2e4eeb3d9ac4a262"></a>
#### &lt;member_position&gt;

Cluster 환경에서 disconnect/ kill 대상이 되는 세션의 member position 이다.

<a id="faf5bc7533994918"></a>
#### &lt;session_id&gt;

세션의 ID 이다.

<a id="42583c3634065e03"></a>
#### &lt;serial#&gt;

세션의 SERIAL NUMBER 이다.

<a id="5d64e08c33bf71ce"></a>
#### &lt;disconnect_option&gt;

- POST_TRANSACTION: 트랜잭션 완료 후, 세션을 종료한다.
- IMMEDIATE: 트랜잭션 완료를 기다리지 않고 바로 세션을 종료한다.

&lt;disconnect_option&gt;이 사용되지 않으면 IMMEDIATE로 동작한다.

<a id="18c5c257d4507db9"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="8a863231bd2a9413"></a>
### 설명

DISCONNECT SESSION은 POST_TRANSACTION과 IMMEDIATE 옵션을 지정할 수 있으며, POST_TRANSACTION은 현재 실행되는 트랜잭션이 있을 경우 트랜잭션이 끝난 후에 세션을 종료한다. IMMEDIATE는 현재 수행 중인 트랜잭션을 바로 정리한 후에 세션을 종료한다.

KILL SESSION은 해당 세션의 프로세스는 존재하지 않지만, 시스템에 남아있는 비정상 세션을 종료한다.

<a id="444516a2647831d1"></a>
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

<a id="9d10e8497c7502e2"></a>
### 호환성

SQL 표준에서는 정의하지 않고 있다.

<a id="f9fc4d123ed9181c"></a>
## ALTER SYSTEM {MOUNT | OPEN} DATABASE

<a id="d33e3d7e09b00a67"></a>
### 기능

데이터베이스를 시스템에 마운트하거나 서비스 가능한 상태로 변경한다.

<a id="4bf9cf741fa76bb0"></a>
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

<a id="add0654dd38325f1"></a>
### 사용 범위 및 접근 권한

&lt;alter system database statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="2863cd411f56dfb7"></a>
### 구문 규칙 및 파라미터

<a id="d090a965c9d0ea6d"></a>
#### &lt;alter system database clause&gt;

- MOUNT DATATABASE
    - 데이터베이스를 시스템에 마운트한다. 
- OPEN DATABASE
    - 데이터베이스를 서비스 가능한 상태로 변경한다.

<a id="8cd443e353d861cd"></a>
#### &lt;open database option&gt;

- READ ONLY/ READ WRITE
    - 읽기 쓰기 모드를 지정하여 데이터베이스를 구동한다.
    - 생략된 경우에는 READ WRITE로 구동된다.
- RESETLOGS/ NORESETLOGS
    - 데이터베이스를 복구한 이후에 온라인 redo log를 유지할지 선택한다.
    - NORESETLOGS는 기존 redo log를 유지하는 반면에 RESETLOGS는 이를 초기화한다.
    - 데이터베이스를 불완전 복구한 경우, 반드시 RESETLOGS를 지정해야 한다.
    - 생략된 경우에는 NORESETLOGS가 기본으로 지정된다.

<a id="bf446cb592c783c3"></a>
#### &lt;database_scope&gt;

- LOCAL
    - LOCAL 영역 서버를 OPEN 단계로 구동한다.
- GLOBAL
    - GLOBAL 영역, 즉 전체 서버를 OPEN 단계로 구동한다.
- Cluster 환경에서 생략된 경우 GLOBAL로 구동 된다.

<a id="353de0332906bd87"></a>
### 사용 예

다음은 읽기 전용으로 데이터베이스를 구동하는 예이다.

```
ALTER SYSTEM OPEN DATABASE READ ONLY;
```

다음은 읽기/쓰기 모드로 구동하고, 온라인 redo log를 초기화하는 예이다.

```
ALTER SYSTEM OPEN DATABASE READ WRITE RESETLOGS;
```

<a id="36cc3eee1ebd307d"></a>
### 호환성

SQL 표준에서는 데이터베이스의 MOUNT 또는 OPEN에 대한 개념을 정의하지 않고 있다.

<a id="60861bb512f745c8"></a>
### 참조

관련 내용은 [ALTER DATABASE RECOVER](#2e60420db9e1864f)를 참조한다.

<a id="ea4b400849367ba5"></a>
## ALTER SYSTEM RECONNECT GLOBAL CONNECTION

<a id="96a4ac53167a7422"></a>
### 기능

GLOBAL CONNECTION 형태로 접속한 세션에 재접속할지 여부를 설정한다.

<a id="6f274bfa29b2843f"></a>
### 구문

```
<alter system reconnect global connection statement> ::=
    ALTER SYSTEM RECONNECT GLOBAL CONNECTION
    ;
```

<a id="e87607992f701eab"></a>
### 사용 범위 및 접근 권한

&lt;alter system reconnect global connection statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="c66809fd1f7cb8bc"></a>
### 설명

GLOBAL CONNECTION 클라이언트의 재접속 여부는 최초 접속할 때 서버로부터 얻은 system 객체의 SCN과 현재 서버의 system 객체의 SCN을 비교하여 결정한다. 해당 구문은 system 객체의 SCN을 상승시켜 클라이언트의 재접속을 유도한다.

해당 구문을 수행한 즉시 클라이언트가 재접속하는 것은 아니다. 클라이언트가 서버에 명령어를 실행할 때 SCN 비교를 통해서 재접속하며 만약 클라이언트에서 모든 멤버로의 연결이 유효하다면 재접속을 시도하지 않는다.

<a id="c9e5c98fdcd98d58"></a>
### 사용 예

다음은 해당 구문을 수행하는 예이다.

```
gSQL> ALTER SYSTEM RECONNECT GLOBAL CONNECTION;

System altered.
```

<a id="5f28ba450a027169"></a>
### 호환성

SQL 표준에서는 GLOBAL CONNECTION의 개념을 정의하지 않고 있다.

<a id="6f09e8a1c2c4db67"></a>
## ALTER SYSTEM RESET property_name

<a id="3dd42e0279c3749a"></a>
### 기능

프로퍼티 파일에서 프로퍼티 값을 삭제한다.

<a id="231d0027430c2bc0"></a>
### 구문

```
<alter system reset statement> ::=
    ALTER SYSTEM { RESET | UNSET } <property name>
        [ SCOPE = { FILE | SPFILE } ]
        [ AT <domain name>]
    ;
```

<a id="53223fff6752df1c"></a>
### 사용 범위 및 접근 권한

&lt;alter system reset statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="cb94cfb960c49df1"></a>
### 구문 규칙 및 파라미터

<a id="1e55057644b631e0"></a>
#### { RESET | UNSET }

RESET과 UNSET은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다.

<a id="6d6b50f72b7d24c1"></a>
#### &lt;property name&gt;

삭제할 프로퍼티의 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5892e8fc0b188208) 장을 참조한다.

<a id="24a195074eaa1f2b"></a>
#### [ SCOPE = { FILE | SPFILE } ]

프로퍼티 파일에서 삭제하는 것이므로 SCOPE=FILE/SPFILE만 사용할 수 있다.

- SCOPE = FILE 
    - FILE과 SPFILE은 동일한 의미의 예약어이므로 어떤 것을 사용해도 무방하다. 
    - 프로퍼티를 FILE에서 삭제하고, 현재 상태에는 적용하지 않는다. 
    - Database를 재구동할 때 변경 사항을 적용한다.

SCOPE 절을 명시하지 않을 경우, 기본값은 SCOPE = FILE 이다.

<a id="fd06de311d3641b4"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="615bb409a2e47bd3"></a>
### 설명

SCOPE=FILE/SPFILE을 사용하여 프로퍼티를 변경했을 경우, 갱신된 값이 프로퍼티 파일에 저장되고 데이터베이스를 재시작할 때 반영된다.

RESET 할 경우, 프로퍼티 파일에 저장된 해당 프로퍼티 갱신값을 파일에서 제거하고 데이터베이스를 재시작할 때 default 값을 사용하도록 한다.

<a id="0101d8ce36552b71"></a>
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

<a id="bf70291f0312ad63"></a>
### 호환성

SQL 표준에서는 시스템 프로퍼티 개념을 정의하지 않고 있다.

<a id="9de79594db052ff4"></a>
### 참조

관련 내용은 [ALTER SYSTEM SET property_name](#daca16c30923690a)을 참조한다.

<a id="daca16c30923690a"></a>
## ALTER SYSTEM SET property_name

<a id="e53ad98802d50723"></a>
### 기능

시스템의 프로퍼티 값을 설정한다.

<a id="78854729dc03fb30"></a>
### 구문

```
<alter system set statement> ::=
    ALTER SYSTEM SET <property name> { = <property value> | TO DEFAULT }
        [ DEFERRED ]
        [ SCOPE = [ MEMORY | { FILE | SPFILE } | BOTH ] ]
    [AT <domain name>]
    ;
```

<a id="7e9a86ea85add75b"></a>
### 사용 범위 및 접근 권한

&lt;alter system set statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="e9f4a95d2add4e0c"></a>
### 구문 규칙 및 파라미터

<a id="050881a232ef29a5"></a>
#### &lt;property name&gt;

설정할 프로퍼티의 이름이다.  
자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5892e8fc0b188208) 장을 참조한다.

<a id="3a2486142be6cc22"></a>
#### &lt;property value&gt;

설정할 프로퍼티의 값이다.

<a id="ad2b7587838f5adf"></a>
#### TO DEFAULT

시스템 프로퍼티 값을 시스템을 구동할 당시의 최초값으로 설정한다.

<a id="37021458c470bd1d"></a>
#### [ DEFERRED ]

변경된 프로퍼티를 적용할 시점을 정의한다.

- DEFERRED 
    - 현재 SESSION에는 영향을 주지 않고, 새로 생성되는 SESSION에 적용된다. 
    - 프로퍼티의 SYS_MODIFIABLE 속성값이 IMMEDIATE/ DEFERRED 일 때 적용 가능하며, 반드시 명시해야 한다. 
    - 프로퍼티의 SYS_MODIFIABLE 속성값이 FALSE인 경우 사용할 수 없다.

프로퍼티의 SYS_MODIFIABLE 속성값이 IMMEDIATE일 경우, DEFERRED를 명시하지 않으면 모든 SESSION에 바로 적용된다.

<a id="2c7e39c7a4ab6b00"></a>
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

<a id="146073c64680c4e5"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="5876f5687c081ce1"></a>
### 설명

자세한 내용은 Database Administration 매뉴얼의 [Server Property](../part-02-administration-manual/10-server-property.md#5892e8fc0b188208) 장을 참조한다.

<a id="2b74d8537a86921b"></a>
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

<a id="3f6050f45f386f53"></a>
### 호환성

SQL 표준에서는 시스템의 프로퍼티 개념을 정의하지 않고 있다.

<a id="573254262b24f7bb"></a>
### 참조

관련 내용은 [ALTER SYSTEM RESET property_name](#6f09e8a1c2c4db67)을 참조한다.

<a id="b5b3c583477146bf"></a>
## ALTER SYSTEM SWITCH LOGFILE

<a id="2545c6262f727475"></a>
### 기능

데이터베이스 내에 있는 CURRENT 상태의 로그파일을 ACTIVE 상태로 변경한다.

<a id="48185ae8691bfe30"></a>
### 구문

```
<alter system switch logfile statement> ::=
    ALTER SYSTEM SWITCH LOGFILE
    [ AT <domain name> ]
    ;
```

<a id="e4edecdddb7b103c"></a>
### 사용 범위 및 접근 권한

&lt;alter system switch logfile statement&gt; 구문을 수행하려면 사용자에게 ALTER SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="6c17e1fb524f0049"></a>
### 구문 규칙 및 파라미터

<a id="03bc901def4d34ec"></a>
#### &lt;alter system switch logfile statement&gt;

데이터베이스가 MOUNT 또는 OPEN 상태여야 한다.

<a id="120ac46d8002bfc0"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="5485d4badf8b8b67"></a>
### 설명

기본적으로 CURRENT 상태의 로그파일이 다 채워지면 자동으로 로그 스위치가 발생한다. 해당 구문은 특수한 상황에서 강제로 로그 스위치를 하고자 할 때 사용된다.

<a id="82b73181ea8ed839"></a>
### 사용 예

```
ALTER SYSTEM SWITCH LOGFILE;
```

<a id="b297cdeca150fd81"></a>
### 호환성

SQL 표준에서는 LOGFILE에 대한 개념을 정의하지 않고 있다.

<a id="31a40360ca43606d"></a>
### 참조

관련 내용은 [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#f9fc4d123ed9181c)를 참조한다.

<a id="79ce4cebdf753797"></a>
## ALTER TABLE

<a id="254bde5d85864ec6"></a>
### 기능

테이블 정의를 변경한다.

<a id="58ddbe504f7a7b8b"></a>
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

<a id="33f65652f53392e9"></a>
### 사용 범위 및 접근 권한

&lt;alter table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="49c637932babbe47"></a>
### 구문 규칙 및 파라미터

<a id="994844f75d07907e"></a>
#### &lt;alter table physical attribute statement&gt;

테이블의 물리적 속성을 변경한다.  
자세한 내용은 [ALTER TABLE name STORAGE](#54f34f813a8b169d) 구문을 참조한다.

<a id="72cd5bb199d9741e"></a>
#### &lt;rename table statement&gt;

테이블 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME TO](#9214266d4110406d) 구문을 참조한다.

<a id="aa46f59b2b94abaf"></a>
#### &lt;add column definition&gt;

테이블에 column을 추가한다.  
자세한 내용은 [ALTER TABLE name ADD COLUMN](#435e25d60c5f411d) 구문을 참조한다.

<a id="2bad9e6bf0e55067"></a>
#### &lt;drop column definition&gt;

테이블에서 column을 삭제한다.  
자세한 내용은 [ALTER TABLE name SET UNUSED COLUMN](#d571baf9c1ff887c) 구문을 참조한다.

<a id="643a6cf19b890d26"></a>
#### &lt;alter column definition&gt;

테이블 column의 정의를 변경한다.  
자세한 내용은 [ALTER TABLE name ALTER COLUMN](#f9d752692bc80a55) 구문을 참조한다.

<a id="3f130d08884d7017"></a>
#### &lt;rename column statement&gt;

테이블 column의 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME COLUMN](#93414efa5f655240) 구문을 참조한다.

<a id="3763c1b082639b8b"></a>
#### &lt;add table constraint definition&gt;

테이블에 제약 조건을 추가한다.  
자세한 내용은 [ALTER TABLE name ADD CONSTRAINT](#01291e4c7e6b5226) 구문을 참조한다.

<a id="fa7acac50f6d4a42"></a>
#### &lt;drop table constraint definition&gt;

테이블의 제약 조건을 삭제한다.  
자세한 내용은 [ALTER TABLE name DROP CONSTRAINT](#ee7de4b9dadd1b3a) 구문을 참조한다.

<a id="39ac10578cb8fc67"></a>
#### &lt;alter table constraint definition&gt;

테이블의 제약 조건을 변경한다.  
자세한 내용은 [ALTER TABLE name ALTER CONSTRAINT](#e11c16dd8992ad1d) 구문을 참조한다.

<a id="326a2550f5e09490"></a>
#### &lt;rename table constraint statement&gt;

테이블 제약 조건의 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME CONSTRAINT](#d90eeeee87655756) 구문을 참조한다.

<a id="6fd9c44a77f7fbde"></a>
#### &lt;add table supplemental log statement&gt;

테이블의 데이터가 변경되면 redo log에 부가 정보를 추가하도록 설정한다.  
자세한 내용은 [ALTER TABLE name ADD SUPPLEMENTAL LOG](#078edcb58e225f27) 구문을 참조한다.

<a id="15a634b7149237c5"></a>
#### &lt;drop table supplemental log statement&gt;

테이블의 데이터가 변경되면 redo log에 부가 정보를 추가하지 않도록 설정한다.  
자세한 내용은 [ALTER TABLE name DROP SUPPLEMENTAL LOG](#7609890ce27c2ea8) 구문을 참조한다.

<a id="95497fd984819099"></a>
#### &lt;rebalance statement&gt;

Cluster 환경에서 테이블의 shard를 재배치하거나 정합성이 깨진 shard를 동기화하여 정합성을 복구한다.  
자세한 내용은 [ALTER TABLE REBALANCE](#1c3e42a41b2d2965) 구문을 참조한다.

<a id="758d6e00ce0d0f61"></a>
#### &lt;move shard statement&gt;

Cluster 환경에서 테이블의 특정 shard를 특정 cluster group으로 재배치한다.  
자세한 내용은 [ALTER TABLE MOVE SHARD](#5179ebc66a584d79) 구문을 참조한다.

<a id="949d9956112fcb78"></a>
#### &lt;merge shards statement&gt;

Cluster 환경에서 테이블의 특정 shard들을 병합하여 재배치한다.  
자세한 내용은 [ALTER TABLE name MERGE SHARDS](#c29d9bc11c0a25f8) 구문을 참조한다.

<a id="49567c6aa75a9d1a"></a>
#### &lt;split shard statement&gt;

Cluster 환경에서 테이블의 특정 shard를 분산하여 특정 cluster group에 재배치한다.  
자세한 내용은 [ALTER TABLE SPLIT SHARD](#2846df311597b7a0) 구문을 참조한다.

<a id="9e540ad4cd4bd960"></a>
#### &lt;rename shard statement&gt;

Cluster 환경에서 테이블의 특정 shard 이름을 변경한다.  
자세한 내용은 [ALTER TABLE name RENAME SHARD](#5da03ed3f3bb106e) 구문을 참조한다.

<a id="e5bf3b95cfe4097e"></a>
#### &lt;read { only | write } statement&gt;

테이블에 READ ( only | write }을 설정한다.  
자세한 내용은 [ALTER TABLE name READ { ONLY | WRITE }](#03545c34a95d7d04) 구문을 참조한다.

<a id="980df749fb0d1ce2"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="d3c98b005db3625e"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="b8b314a6d1c7f585"></a>
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

<a id="435e25d60c5f411d"></a>
## ALTER TABLE name ADD COLUMN

<a id="5d932cefff5524fa"></a>
### 기능

테이블에 column을 추가한다.

<a id="e517e96ca0559dd8"></a>
### 구문

```
<add column definition> ::=
      ALTER TABLE table_name ADD [ COLUMN ] <column definition>
    | ALTER TABLE table_name ADD [ COLUMN ] ( <column definition> [, ...] )
    ;
```

<a id="e65991ab7c03bf64"></a>
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

<a id="d168f21eb96af391"></a>
### 구문 규칙 및 파라미터

<a id="fc62a366f075194c"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="03315688fd94dc67"></a>
#### ADD [ COLUMN ]

COLUMN 예약어는 생략할 수 있다.

<a id="77b9575508133b28"></a>
#### &lt;column definition&gt;

추가할 column을 정의한다.  
자세한 내용은 [CREATE TABLE](#9b82da6d66aabe8c) 구문의 &lt;[column definition&gt;](#2540b5ecf509674a) 절을 참조한다.  
테이블 내에 동일한 column 이름이 존재하지 않아야 한다.

Column을 정의할 때 DEFAULT 절을 명시할 경우, 모든 row의 기본값을 추가되는 column에 저장한다.  
Column을 정의할 때 &lt;identity column specification&gt; 절을 명시한 경우, 모든 row 각각의 자동 생성값을 추가되는 column에 저장한다.   
Column을 정의할 때 NOT NULL 제약 조건을 함께 명시한 경우, 테이블을 비우거나 DEFALUT 절 또는 &lt;identity column specification&gt; 절을 함께 기술해야 한다.

<a id="bb02e9d3fec7ad8d"></a>
#### ( &lt;column definition&gt; [, ...] )

다수의 column을 추가한다.   
괄호 내부에 다수의 &lt;column definition&gt;을 나열한다.

<a id="98259de6e0951094"></a>
### 설명

추가되는 column은 기존 column들의 뒤에 위치한다.   
DEFAULT 절이나 &lt;identity column specification&gt;을 명시한 경우, 수행시간은 테이블에 존재하는 row의 개수에 비례하여 증가한다.

<a id="5a006c0fdf5d9adb"></a>
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

<a id="240d349b3d84a98f"></a>
### 호환성

SQL 표준에서는 다수의 column definition 추가에 대해 정의하지 않고 있다.

<a id="e463b905b23799af"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#79ce4cebdf753797)
- [ALTER TABLE name SET UNUSED COLUMN](#d571baf9c1ff887c)
- [ALTER TABLE name ALTER COLUMN](#f9d752692bc80a55)
- [ALTER TABLE name RENAME COLUMN](#93414efa5f655240)

<a id="01291e4c7e6b5226"></a>
## ALTER TABLE name ADD CONSTRAINT

<a id="0bcf06a810d8594c"></a>
### 기능

테이블 제약 조건을 추가한다.

<a id="b4fb4558ea44c5d3"></a>
### 구문

```
<add table constraint definition> ::=
    ALTER TABLE table_name 
        ADD <table constraint definition>
    ;
```

<a id="a4f95fd9f38b4234"></a>
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

<a id="873d2b34dba4fe11"></a>
### 구문 규칙 및 파라미터

<a id="dd7b4ef5f67635b8"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="10f30ce440b7c20e"></a>
#### &lt;table constraint definition&gt;

추가할 제약 조건을 정의한다.  
NOT NULL 제약 조건은 ALTER TABLE .. ADD CONSTRAINT 구문으로 추가할 수 없으며, 다음 예와 같이 [ALTER TABLE name ALTER COLUMN](#f9d752692bc80a55) 구문을 이용해 정의할 수 있다.

```
ALTER TABLE t1 ALTER COLUMN c1 SET NOT NULL;
```

자세한 내용은 [CREATE TABLE](#9b82da6d66aabe8c) 구문의 &lt;[table constraint definition&gt;](#60ba581d44970aee) 절을 참조한다.

<a id="23408afa8266a616"></a>
### 설명

Primary key, unique key와 같은 key 제약을 추가할 때 이를 위한 index가 자동으로 생성된다.

<a id="1c6c94ebacc59498"></a>
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

<a id="457bcee94a0c751f"></a>
### 호환성

**SQL 표준 호환성**

<a id="0582905927c4bc46"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="5470243fba9ac8b6"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](#9b82da6d66aabe8c)
- [CREATE INDEX](#9d2795ea1fc7b4c6)
- [ALTER TABLE](#79ce4cebdf753797)
- [ALTER TABLE name DROP CONSTRAINT](#ee7de4b9dadd1b3a)

<a id="c41a3550730b3ad2"></a>
## ALTER TABLE name ADD GLOBAL SECONDARY INDEX

<a id="246df7c32695db1e"></a>
### 기능

테이블에 global secondary index를 생성한다.

<a id="cadadffd9b7dc8cb"></a>
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

<a id="84f8a5867353cf6e"></a>
### 사용 범위 및 접근 권한

&lt;alter table add global secondary index definition&gt; 구문은 cluster system에서 정의할 수 있으며 사용자는 다음 조건들을 만족해야 한다.

- 인덱스를 생성할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 인덱스가 생성될 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE
    - USAGE TABLESPACE ON DATABASE

<a id="5895311dc4c67bd0"></a>
### 구문 규칙 및 파라미터

<a id="00355e298add9436"></a>
#### table_name

인덱스를 생성할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="1b21f6e42e6f93ca"></a>
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

<a id="d84900f5c9ecd7d8"></a>
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

<a id="928b21ae03c8ae0d"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="efae095660fed429"></a>
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

<a id="0430e5de7af3fda0"></a>
#### TABLESPACE tablespace_name

인덱스가 저장될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - LOGGING 인덱스로 변경하려면, tablespace_name은 data tablespace여야 하며 
    - NOLOGGING 인덱스로 변경하려면, tablespace_name은 temporary tablespace 또는 nologging tablespace여야 한다.

- TABLESPACE 절을 생략할 경우, 기존 인덱스의 설정을 그대로 따른다.

<a id="53878e3386650ebf"></a>
### 설명

Non-deterministic 질의에는 global secondary index가 반드시 필요하다. LOGGING 인덱스와 NOLOGGING 인덱스에는 다음과 같은 trade-off가 있다

- LOGGING 인덱스
    - 장점: 시스템을 구동할 때 로그를 이용해 인덱스가 자동으로 복구되므로 별도의 구축과정이 없다.
    - 단점: 관련 row를 변경할 때 인덱스 변경 내용을 로그로 기록하여 디스크 IO를 유발한다.
- NOLOGGING 인덱스
    - 장점: 관련 row를 변경할 때 인덱스 변경 내용에 대해 디스크 IO가 발생하지 않는다.
    - 단점: 시스템을 구동할 때 인덱스에 대한 로그 정보가 없어 자동으로 인덱스를 재구축한다.

<a id="989abce82044c288"></a>
### 사용 예

다음은 테이블 T1에 global secondary index를 추가하는 예이다.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX;

Table altered.

gSQL> COMMIT;

Commit complete.
```

다음은 테이블 T1의 tablespace USER_DATA_TBS에 global secondary index를 logging 인덱스로 생성하는 예이다.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX TABLESPACE USER_DATA_TBS;

Table altered.

gSQL> COMMIT;

Commit complete.
```

다음은 테이블 T1의 tablespace USER_TEMP_TBS에 global secondary index를 nologging 인덱스로 생성하는 예이다.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX TABLESPACE USER_TEMP_TBS;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="592ef7d3ae2613ff"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="79d76ff85a8dd7f2"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#cad9ba4018feb93c)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#5936e806c49b1c04)
- [CREATE TABLE](#9b82da6d66aabe8c)

<a id="078edcb58e225f27"></a>
## ALTER TABLE name ADD SUPPLEMENTAL LOG

<a id="90e7613df331e064"></a>
### 기능

테이블의 데이터가 변경될 때 테이블에 primary key가 있으면 redo log에 primary key 값을 추가하도록 설정한다.

<a id="32fbfe624e6f59eb"></a>
### 구문

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="761ebe9efdd60bee"></a>
### 사용 범위 및 접근 권한

&lt;add table supplemental log statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="3fc41a14282a02de"></a>
### 구문 규칙 및 파라미터

<a id="fd04edea5023801d"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

테이블에 primary key가 존재하지 않더라도 구문을 수행할 수 있다.

<a id="90970eee4fc82e81"></a>
### 설명

해당 TABLE에 UPDATE/ DELETE를 수행할 때 SUPPLEMENTAL LOG를 추가로 기록하도록 한다. 기록된 SUPPLEMENTAL LOG는 CDC와 같은 툴 또는 로그를 분석할 때 사용된다.

모든 TABLE의 SUPPLEMENTAL LOG를 기록하려면 *SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY = YES* 로 설정한다.

<a id="bb585c9a33c7c7a9"></a>
### 사용 예

다음은 테이블의 data를 변경할 때 redo log에 primary key 값을 추가하도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="f386cb8215ad567c"></a>
### 호환성

SQL 표준에서는 &lt;add table supplemental log statement&gt;를 다루지 않는다.

<a id="97e83ab78fb07453"></a>
### 참조

관련 내용은 [ALTER TABLE name DROP SUPPLEMENTAL LOG](#7609890ce27c2ea8)를 참조한다.

<a id="f9d752692bc80a55"></a>
## ALTER TABLE name ALTER COLUMN

<a id="d7fe756d276ce8f4"></a>
### 기능

Column의 정의를 변경한다.

<a id="df9e634c0e62f7c6"></a>
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

<a id="6cd89b8e9c3fab9a"></a>
### 사용 범위 및 접근 권한

&lt;alter column definition&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="9a0670efe723da6f"></a>
### 구문 규칙 및 파라미터

<a id="cb9b7c41da8d5d52"></a>
#### table_name

변경할 테이블 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="114b7caed867bcf3"></a>
#### ALTER [ COLUMN ]

COLUMN 예약어는 생략할 수 있다.

<a id="9e7f1188f2fb7735"></a>
#### column_name

변경할 column의 이름이다.

<a id="a4a3e0439cdb26cd"></a>
#### &lt;set column default clause&gt;

Column의 기본값을 설정한다.   
identity column이 아니어야 한다.

이후에 수행되는 INSERT 구문 등에서 DEFAULT 절을 사용할 경우 설정한 기본값이 사용된다.

DEFAULT expression의 데이터 타입은 column의 데이터 타입과 호환 가능해야 한다.   
타입이 호환되지 않거나 공간이 부족한 경우 INSERT, UPDATE 구문에서 DEFAULT를 사용할 때 에러가 발생한다.

자세한 설명은 [CREATE TABLE](#9b82da6d66aabe8c) 구문의 &lt;[default clause&gt;](#c7016df1b3063520) 절을 참조한다.

<a id="57cfa5305ceb641c"></a>
#### &lt;drop column default clause&gt;

Column의 기본값을 제거한다.  
identity column이 아니어야 한다.  
기본값을 제거하면 INSERT 구문 등에서 DEFAULT 절을 사용할 때 NULL 값으로 설정된다.

<a id="d8a6992e3adb2751"></a>
#### &lt;set column not null clause&gt;

- SET [CONSTRAINT constraint_name] NOT NULL [ &lt;constraint characteristics&gt; ]
    - Column에 NOT NULL 제약 조건을 설정한다.
    - Column의 값으로 NULL 값을 허용하지 않는다.
    - 해당 column에 NULL 값이 존재하지 않아야 한다.

- [CONSTRAINT constraint_name]을 생략할 경우 자동으로 제약 조건 이름을 지정한다.
- &lt;constraint characteristics&gt;를 생략할 경우, NOT DEFERRABLE INITIALLY IMMEDIATE 속성을 갖는다.
- Identity column은 DEFERRABLE 속성을 가질 수 없다.

지연가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](#0ec9d72169df1ed8) 구문의 설명을 참조한다.

<a id="2385e57d0a9a2c74"></a>
#### &lt;drop column not null clause&gt;

- DROP NOT NULL
    - Column의 NOT NULL 제약 조건을 제거한다.

<a id="d66887582dde4234"></a>
#### &lt;alter column data type clause&gt;

- SET DATA TYPE &lt;data type&gt;
    - Column의 데이터 타입을 변경한다.

> SET DATA TYPE 구문은 자동으로 commit 되는 DDL 구문이다.

동일한 계열간에 타입을 변경할 수 있는데 이 때 다음 조건을 만족해야 한다.

**character string type 변환**

<a id="cb7a0b5df9b2d3dc"></a>
| from \ to | CHAR(n) | VARHCAR(n) | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR(m) | X | X | X |
| VARCHAR(m) | X | n >= m | X |
| LONG VARCHAR | X | X | O |

char length unit을 변경할 경우 다음과 같은 조건을 만족해야 한다.

**character length unit 변환**

<a id="520d594ebe80aa4d"></a>
| from \ to | OCTETS | CHARACTERS |
| --- | --- | --- |
| OCTETS | O | O |
| CHARACTERS | X | O |

**binary string type 변환**

<a id="094a1088a36d36bd"></a>
| from \ to | BINARY(n) | VARBINARY(n) | LONG VARBINARY |
| --- | --- | --- | --- |
| BINARY(m) | X | X | X |
| VARBINARY(m) | X | n >= m | X |
| LONG VARBINARY | X | X | O |

**numeric type**

<a id="41c63634e1567785"></a>
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

<a id="ff3795d991ba4e17"></a>
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

<a id="cc57ba7e79b0fc20"></a>
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

<a id="c685b58bd918f910"></a>
| from \ to | NATIVE_SMALLINT | NATIVE_INTEGER | NATIVE_BIGINT | NATIVE_REAL | NATIVE_DOUBLE |
| --- | --- | --- | --- | --- | --- |
| NATIVE_SMALLINT | O | X | X | X | X |
| NATIVE_INTEGER | X | O | X | X | X |
| NATIVE_BIGINT | X | X | O | X | X |
| NATIVE_REAL | X | X | X | O | X |
| NATIVE_DOUBLE | X | X | X | X | O |

**Boolean type의 변환**

<a id="2bffe3e4e141e152"></a>
| from \ to | BOOLEAN |
| --- | --- |
| BOOLEAN | O |

**Date/ time type의 변환 (TZ: WITH TIME ZONE)**

<a id="33d9cdaa457456fd"></a>
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

<a id="83f4a8769bfc4b06"></a>
| from \ to | YEAR(q) | MONTH(q) | YEAR(q) TO MONTH |
| --- | --- | --- | --- |
| YEAR(p) | q >= p | X | X |
| MONTH(p) | X | q >= p | X |
| YEAR(p) TO MONTH | X | X | q >= p |

**INTERVAL DAY TO TIME 계열의 type 변환 (p,q 가 생략된 경우 2) (f,g 가 생략된 경우 6)**

<a id="5a1ae4c4603a6582"></a>
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

<a id="3624c3253cdc249a"></a>
| from \ to | ROWID |
| --- | --- |
| ROWID | O |

<a id="57a8836c0f20cb4c"></a>
#### &lt;alter identity column specification&gt;

Column의 identity 속성을 변경한다.   
Column은 identity column 이어야 한다.

- SET GENERATED [ ALWAYS | BY DEFAULT ]
    - identity column의 생성 방식을 변경한다. 
    - 자세한 내용은 [CREATE TABLE](#9b82da6d66aabe8c) 구문의 &lt;[identity column specification&gt;](#550e853cb83ff15c)을 참조한다. 
- &lt;alter sequence generator restart option&gt; 
    - identity column의 다음 값 (NEXT VALUE)을 변경한다. 
    - 자세한 내용은 [ALTER SEQUENCE](#ebac80e511ac5859) 구문의 &lt;[alter sequence generator restart option&gt;](#07e03eaaef5a0cdd) 절을 참조한다. 
- &lt;basic sequence generator option&gt; 
    - identity column의 속성을 변경한다. 
    - SQL 표준에서는 SET &lt;basic sequence generator option&gt;의 형태로 기술하도록 정의하고 있으나 생략 가능하다. 
    - 자세한 내용은 [ALTER SEQUENCE](#ebac80e511ac5859) 구문을 참조한다.

<a id="4d28116305d3f038"></a>
#### &lt;drop identity property clause&gt;

Column의 identity 속성을 제거한다.   
Column은 identity column 이어야 한다.

<a id="edfa446b1c279bd3"></a>
### 설명

SET NOT NULL 절의 null 검사 수행시간은 테이블의 row 개수에 비례한다.

다음과 같은 column은 NULL 값을 허용하지 않는다. 즉, DROP NOT NULL 절을 수행하더라도 다음 조건 중 하나를 만족할 경우 NULL 값을 허용하지 않는다.

- NOT NULL 제약 조건이 있는 column
- Column이 primary key 제약 조건에 포함되는 경우
- Column이 identity column인 경우

SET DEFAULT 절을 이용한 기본값 변경과 &lt;alter identity column specification&gt; 절을 이용한 identity 속성의 변경은 이후에 수행되는 INSERT 또는 UPDATE 구문에 적용된다.

<a id="be4e5c9c54465afc"></a>
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

<a id="cc9ceed80430b030"></a>
### 호환성

**SQL 표준 호환성**

<a id="ed50a8a22b48963a"></a>
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

<a id="d8538d931260045a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#79ce4cebdf753797)
- [ALTER TABLE name ADD COLUMN](#435e25d60c5f411d)
- [ALTER TABLE name SET UNUSED COLUMN](#d571baf9c1ff887c)
- [ALTER TABLE name RENAME COLUMN](#93414efa5f655240)

<a id="e11c16dd8992ad1d"></a>
## ALTER TABLE name ALTER CONSTRAINT

<a id="2668d737e036c727"></a>
### 기능

테이블 제약 조건의 특성을 변경한다.

<a id="d7be0eae71b28e7e"></a>
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

<a id="bab22937bcd5dca7"></a>
### 사용 범위 및 접근 권한

&lt;alter table constraint definition&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

> Cluster는 지연 가능한 제약 조건을 지원하지 않는다.

<a id="aa4a45beaab35e30"></a>
### 구문 규칙 및 파라미터

<a id="8be258e6a1ee8d8c"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="52acdf5077877978"></a>
#### &lt;constraint object&gt;

변경할 제약 조건은 다음과 같이 지정할 수 있다.

- CONSTRAINT constraint_name
    - 변경할 제약 조건의 이름이다.
- PRIMARY KEY 
    - 테이블의 PRIMARY KEY 제약 조건이다.
- UNIQUE( column [,...] ) 
    - Column 목록에 부합되는 UNIQUE 제약 조건이다.

<a id="42be70edbec31891"></a>
#### DEFERRABLE | NOT DEFERRABLE

제약 조건의 지연 가능 여부를 변경한다.

- DEFERRABLE
    - 제약 조건을 지연가능하도록 변경한다. 
- NOT DEFERRABLE 
    - 제약 조건을 지연가능하지 않도록 변경한다.

지연가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](#0ec9d72169df1ed8) 구문의 설명을 참조한다.

<a id="ccb8c99eb45055c7"></a>
#### INITIALLY IMMEDIATE | INITIALLY DEFERRED

제약 조건의 검사시점 초기값을 변경한다.

- INITIALLY IMMEDIATE 
    - DML을 수행할 때 제약 조건을 검사한다.
- INITIALLY DEFERRED 
    - COMMIT을 수행할 때 제약 조건을 검사한다.

NOT DEFERRABLE로 정의된 제약 조건은 INITIALLY DEFERRED로 변경할 수 없다.

<a id="bb6a9fa408a074c0"></a>
### 설명

지연가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](#0ec9d72169df1ed8) 구문을 참조한다.

<a id="55fae90add4a9302"></a>
### 사용 예

다음은 t1_uk 제약 조건을 지연가능하게 하고 검사시점을 DEFERRED로 설정하는 예이다.

```
gSQL> ALTER TABLE t1 ALTER CONSTRAINT t1_uk DEFERRABLE INITIALLY DEFERRED;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="ddadbeb1b76b6d97"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- ALTER PRIMARY KEY 절
- ALTER UNIQUE(column [,...]) 절

**SQL 표준 호환성**

<a id="55b759433b4dc81d"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F492 | Optional table constraint enforcement | X |

<a id="5936e806c49b1c04"></a>
## ALTER TABLE name ALTER GLOBAL SECONDARY INDEX

<a id="7fcca1629be7a540"></a>
### 기능

테이블에서 global secondary index의 물리적 속성을 변경한다.

<a id="2ec7aa6fbe865729"></a>
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

<a id="bf805ff87fb8f49c"></a>
### 사용 범위 및 접근 권한

&lt;alter table alter global secondary index storage statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="54e36fa64dda53cc"></a>
### 구문 규칙 및 파라미터

<a id="1e171c36824554e1"></a>
#### table_name

인덱스를 생성할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="091c7089c6fdfa7a"></a>
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

<a id="443c042af6448924"></a>
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

<a id="49ccf204ef08b75d"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="b62a55a16a696a10"></a>
### 설명

Non-deterministic 질의를 하려면 global secondary index가 반드시 필요하다.

<a id="e8bd6230e4242a5b"></a>
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

<a id="eef66d046803fa01"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="39411c5e638a860a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#c41a3550730b3ad2)
- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#cad9ba4018feb93c)

<a id="ee7de4b9dadd1b3a"></a>
## ALTER TABLE name DROP CONSTRAINT

<a id="9445595572d80c79"></a>
### 기능

테이블 제약 조건을 제거한다.

<a id="a59ad4b01bf32ec3"></a>
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

<a id="8788159f99d5c016"></a>
### 사용 범위 및 접근 권한

&lt;drop table constraint definition&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 제약 조건의 소유자 
- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="aaa395dbbac563a6"></a>
### 구문 규칙 및 파라미터

<a id="74f6e910f9e11753"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="7fdf7711b424de58"></a>
#### CONSTRAINT constraint_name

제거할 제약 조건의 이름이다.

<a id="c945403a3e76d468"></a>
#### PRIMARY KEY

테이블의 primary key 제약 조건이다.

<a id="30911125a89234c0"></a>
#### UNIQUE( column_name [, ...] )

Column들에 대한 unique 제약 조건이다.

<a id="f68dae4e83e9f975"></a>
#### &lt;drop behavior&gt;

생략할 경우, 기본값은 RESTRICT 이다.   
현재는 RESTRICT/ CASCADE가 동일하게 작동한다.

<a id="98072b9d88ac51ea"></a>
### 설명

제약 조건의 이름을 사용하지 않고 NOT NULL 제약 조건을 제거하려고 할 경우 [ALTER TABLE name ALTER COLUMN](#f9d752692bc80a55) 구문의 &lt;[drop column not null clause&gt;](#2385e57d0a9a2c74) 절을 이용한다.

<a id="beaaa77b5c7f3ad2"></a>
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

<a id="1c11381b1adef539"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- DROP PRIMARY KEY 
- DROP UNIQUE ( column_name [, ...] ) 
- CASCADE CONSTRAINTS

**SQL 표준 호환성**

<a id="1a98eb5a02d934a2"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="274288840f767a2f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#79ce4cebdf753797)
- [ALTER TABLE name ADD CONSTRAINT](#01291e4c7e6b5226)
- [DROP INDEX](#8921114ccac5a25e)

<a id="cad9ba4018feb93c"></a>
## ALTER TABLE name DROP GLOBAL SECONDARY INDEX

<a id="c30c9e93f7a1b090"></a>
### 기능

테이블에서 global secondary index를 제거한다.

<a id="6f26541f9fff417d"></a>
### 구문

```
<alter table drop global secondary index definition> ::=
    ALTER TABLE table_name 
        DROP GLOBAL SECONDARY INDEX
    ;
```

<a id="9dbc9950703f3ca2"></a>
### 사용 범위 및 접근 권한

&lt;alter table drop global secondary index definition&gt; 구문은 cluster system에서 정의할 수 있으며 사용자는 다음 조건들을 만족해야 한다.

- 인덱스를 제거할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

<a id="aafb74ef8c19a504"></a>
### 구문 규칙 및 파라미터

<a id="6bf95252872876fa"></a>
#### table_name

인덱스를 제거할 테이블 이름이다.

<a id="9e7ff325058630c0"></a>
### 설명

Non-deterministic 질의를 하려면 global secondary index가 반드시 필요하다.

<a id="231aefec382de392"></a>
### 사용 예

테이블 T1에서 global secondary index를 제거한다.

```
gSQL> ALTER TABLE T1 DROP GLOBAL SECONDARY INDEX;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="404130f05c3a7364"></a>
### 호환성

SQL 표준에서는 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="f0212adc4e1f3da9"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#c41a3550730b3ad2)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#5936e806c49b1c04)

<a id="7609890ce27c2ea8"></a>
## ALTER TABLE name DROP SUPPLEMENTAL LOG

<a id="939eae02c3639bf5"></a>
### 기능

테이블의 데이터가 변경될 때 redo log에 primary key 정보를 남기지 않도록 설정한다.

<a id="5173340ace28d54c"></a>
### 구문

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="359fecf9ca5180b4"></a>
### 사용 범위 및 접근 권한

&lt;drop table supplemental log statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="619705914516e77e"></a>
### 구문 규칙 및 파라미터

<a id="29618cd09168b718"></a>
#### table_name

변경할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
[ALTER TABLE name ADD SUPPLEMENTAL LOG](#078edcb58e225f27) 구문을 사용해 설정된 상태여야 한다

<a id="f288d42145032e3d"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="387ac0a72dfa540b"></a>
### 사용 예

다음은 테이블의 데이터가 변경되었을 때 redo log에 primary key 정보를 남기지 않도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="e1ad5c923ba4db73"></a>
### 호환성

SQL 표준에서는 &lt;drop table supplemental log statement&gt;를 다루지 않는다.

<a id="c29d9bc11c0a25f8"></a>
## ALTER TABLE name MERGE SHARDS

<a id="8d25da5417d6b546"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard들을 merge 하여 재배치한다.

<a id="3162abec0d5ff526"></a>
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

<a id="66124ea6b338094f"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table merge shards statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="265bb5586723a447"></a>
### 구문 규칙 및 파라미터

<a id="4bed8e72a1b6eaca"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
해당 테이블이 cluster-specific이고 list shard 또는 range shard인 경우에만 구문을 수행할 수 있다.

<a id="3b84a1757535a9b6"></a>
#### &lt;source shard list&gt;

Merge 할 원본 shard들의 list 이다.  
List에서 지정한 shard가 해당 테이블에 반드시 존재해야 한다.

<a id="d4923be1ebdb668c"></a>
#### source_shard_name

Merge 할 원본 shard의 이름이다.  
해당 테이블에 존재하지 않는 shard인 경우 구문을 수행할 수 없다.

<a id="b6bac939b735703d"></a>
#### start_shard_name

Merge 할 범위 중 시작 shard의 이름이다.   
Range shard에서만 사용된다.

<a id="da8d0b2f72ff4160"></a>
#### end_shard_name

Merge 할 범위 중 마지막 shard의 이름이다.  
Range shard에서만 사용된다.

<a id="f1e8ac49e700ba3c"></a>
#### dest_shard_name

대상 shard의 이름이다.

<a id="526b5d4237cc4a40"></a>
#### &lt;dest shard placement&gt;

대상 shard가 배치될 cluster group의 이름이다.  
해당 구문이 생략된 경우, dest_shard_name이 &lt;source shard list&gt;에 포함되어 있어야 한다.

<a id="5e9339d1afd33930"></a>
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

<a id="8876c1486fbdd941"></a>
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

<a id="efe1ad5ee3974d9f"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="5f40d1a09ea96a98"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name MOVE SHARD](#5179ebc66a584d79)
- [ALTER TABLE name SPLIT SHARD](#2846df311597b7a0)

<a id="5179ebc66a584d79"></a>
## ALTER TABLE name MOVE SHARD

<a id="ac031f45496a2c05"></a>
### 기능

테이블의 특정 shard 또는 특정 cluster group의 전체 shard를 특정 cluster group에 재배치한다.

<a id="ee66dbb873384d6f"></a>
### 구문

```
<alter table move shard statement> ::=
    ALTER TABLE table_name MOVE SHARD
        { shard_name_list | FROM CLUSTER GROUP src_cluster_group }
        TO CLUSTER GROUP dest_cluster_group [ ONLINE | OFFLINE ]
    ;
```

<a id="3f73b6c538879a1a"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table move shard statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="90eeeef59b13a710"></a>
### 구문 규칙 및 파라미터

<a id="67ed801d00f28847"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
해당 테이블이 cluster group specific인 경우에만 구문을 수행할 수 있다.

<a id="53de0947b9d63501"></a>
#### shard_name_list

재배치할 shard name 목록이다.  
해당 테이블에 존재하지 않는 shard인 경우 구문을 수행할 수 없다.

<a id="5945ea0867c10341"></a>
#### src_cluster_group

재배치할 특정 cluster group의 이름이다.

<a id="a54392add5f09977"></a>
#### dest_cluster_group

테이블의 shard를 배치할 target cluster group의 이름이다.  
해당 테이블의 shard가 지정한 cluster group에 이미 존재할 경우 구문을 수행할 수 없다.

<a id="c84026c5a1741a56"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="ac9cbca164c5dbe2"></a>
### 설명

테이블의 특정 shard를 특정 cluster group에서 다른 cluster group으로 재배치한다.

특정 cluster group을 제거하려면 테이블의 shard를 재배치한 후에 [DROP CLUSTER GROUP](#e491103ba644ea1a) 구문을 수행해야 한다.

모든 테이블의 shard를 특정 cluster group에서 다른 cluster group으로 이동시키는 경우, ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP TO CLUSTER GROUP 구문을 수행한다.

<a id="8482eb21792ab4ed"></a>
### 사용 예

다음은 &lt;alter table move shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 MOVE SHARD shard1, shard2 TO CLUSTER GROUP g3;

Table altered.

gSQL> ALTER TABLE t1 MOVE SHARD FROM CLUSTER GROUP g1 TO CLUSTER GROUP g3;

Table altered.
```

<a id="c17fcf8f40586dd1"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="6ddad60d51da2abd"></a>
### 참조

관련 내용은 [ALTER DATABASE MOVE SHARD](#da8877ea32a04f66)를 참조한다.

<a id="03545c34a95d7d04"></a>
## ALTER TABLE name READ { ONLY | WRITE }

<a id="a8d03df3765e0207"></a>
### 기능

테이블에 READ { ONLY | WRITE }을 설정한다.

<a id="3ef6ef2a9676fe9c"></a>
### 구문

```
<alter table read { only | write } statement> :==
     ALTER TABLE table_name
         READ { ONLY | WRITE }
     ;
```

<a id="6e1d6264413dda4f"></a>
### 사용 범위 및 접근 권한

&lt;alter table read { only | write } statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="43585852f988a774"></a>
### 구문 규칙 및 파라미터

<a id="0967fcff64002f22"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="d754caf34ebb94a4"></a>
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

<a id="becbaa3a331103f4"></a>
### 사용 예

다음은 &lt;alter table read { only | write } statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 READ ONLY;

Table altered.

gSQL> ALTER TABLE t1 READ WRITE;

Table altered.
```

<a id="8dc457be48a09a8d"></a>
### 호환성

SQL 표준에서는 &lt;alter table read { only | write } statement&gt; 구문을 정의하지 있지 않다.

<a id="683e256d1ae86be1"></a>
### 참조

관련 내용은 [ALTER TABLE](#79ce4cebdf753797)을 참조한다.

<a id="1c3e42a41b2d2965"></a>
## ALTER TABLE name REBALANCE

<a id="4fa3425b0f2f9d40"></a>
### 기능

테이블의 shard를 재배치한다.

<a id="573a11d686f9480b"></a>
### 구문

```
<alter table rebalance statement> ::=
    ALTER TABLE table_name REBALANCE [ ONLINE | OFFLINE ]
    ;
```

<a id="36fc2dcaba650314"></a>
### 사용 범위 및 접근 권한

Cluster system 에서 수행할 수 있다.

&lt;alter table rebalance statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="c1ec2af06f0ca704"></a>
### 구문 규칙 및 파라미터

<a id="9661d70a4534519d"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="0106265231b9df7d"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다

- ONLINE 
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="57d06fc15fd70679"></a>
### 설명

다음과 같은 구문을 통해 cluster member, cluster group을 추가할 때 table들의 shard는 재배치하지 않는다.

- [CREATE CLUSTER GROUP](#dd23e8e2eae3991d)
- [ALTER CLUSTER GROUP name ADD MEMBER](#72ed23526a0c9e3b)

추가된 cluster group과 cluster member의 테이블 shard를 재배치하려면 &lt;alter table rebalance statement&gt; 구문을 수행한다. 테이블의 shard 가 이미 재배치된 경우, 별도의 재배치 작업없이 성공한다.

모든 테이블들의 shard를 재배치하려면 [ALTER DATABASE REBALANCE](#48a2899b3f507f9f) 구문을 수행한다.

<a id="7c969bb67805451a"></a>
### 사용 예

다음은 &lt;alter table rebalance statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 REBALANCE;

Table altered.
```

<a id="cd5aa989fef66670"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="1baf8de768cb0d19"></a>
## ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list

<a id="24f8b1883e4f2c6f"></a>
### 기능

특정 cluster group에 shard를 포함하지 않도록 테이블의 shard를 재배치한다.

<a id="c6ef2e0a56908ce4"></a>
### 구문

```
<alter table rebalance exclude cluster group statement> ::=
    ALTER TABLE table_name REBALANCE 
        EXCLUDE CLUSTER GROUP cluster_group_list [ ONLINE | OFFLINE ]
    ;
```

<a id="efe540783ed87f59"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table rebalance exclude cluster group statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="aba8a90ca2c191ff"></a>
### 구문 규칙 및 파라미터

<a id="09c2645c79534f70"></a>
#### table_name

테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
해당 테이블이 cluster-wide인 경우에만 구문을 수행할 수 있다.

<a id="af85986e5f85ce34"></a>
#### cluster_group_list

테이블의 shard를 포함하지 않는 cluster group의 list이다.   
재배치에서 제외될 cluster group이 cluster 전체 group인 경우 구문을 수행할 수 없다.

<a id="dcaea174d0ffa0c8"></a>
#### [ ONLINE | OFFLINE ]

테이블의 shard를 재배치할 때 DML을 허용할지 여부를 결정한다.

- ONLINE 
    - INSERT, UPDATE, DELETE 를 허용한다. 
- OFFLINE 
    - INSERT, UPDATE, DELETE 를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE 이다.

<a id="5b36117380e596f8"></a>
### 설명

특정 cluster group을 배제하고 테이블의 shard를 재배치한다.   
해당 cluster group에 테이블의 shard가 존재하지 않을 경우, 별도의 재배치 작업없이 성공한다.   
테이블의 shard가 위치한 cluster group을 기준으로 shard를 재배치한다.

특정 cluster group을 제거하려면 테이블의 shard를 재배치한 후에 [DROP CLUSTER GROUP](#e491103ba644ea1a) 구문을 수행해야 한다.  
모든 테이블들에서 cluster group을 배제하고 shard를 재배치하고자 할 경우, [ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP](#103f334bdbeb3455)을 수행한다.

<a id="563172b24d1f26d0"></a>
### 사용 예

다음은 &lt;alter table rebalance exclude cluster group statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 REBALANCE EXCLUDE CLUSTER GROUP g3;

Table altered.
```

<a id="c7417fadaebd7d22"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="8569879417a60655"></a>
## ALTER TABLE name REBUILD GLOBAL SECONDARY INDEX

<a id="01ad18cfebd6c908"></a>
### 기능

Global secondary index를 재구축한다.

<a id="5c710e04e06cec44"></a>
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

<a id="ee80844900c93464"></a>
### 사용 범위 및 접근 권한

&lt;rebuild global secondary index statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 인덱스를 재구축할 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - ALTER ANY TABLE ON DATABASE

- 인덱스를 재구축할 테이블스페이스에 대해 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE
    - USAGE TABLESPACE ON DATABASE

<a id="9cdae3a648b87438"></a>
### 구문 규칙 및 파라미터

<a id="42164f8cb7b17977"></a>
#### table_name

인덱스를 재구축할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="b2c6fd430c7cac21"></a>
#### [ ONLINE | OFFLINE ]

인덱스를 재구축할 때, 해당 테이블에 DML을 허용할지 여부를 결정한다.

- ONLINE
    - INSERT, UPDATE, DELETE를 허용한다. 
- OFFLINE
    - INSERT, UPDATE, DELETE를 허용하지 않는다.
- 생략할 경우, 기본값은 ONLINE이다.

<a id="4b367322cff4c61a"></a>
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

<a id="77cb781655bd0e1b"></a>
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

<a id="58b33874f671e308"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="1c9c3db675376b35"></a>
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

<a id="68da49825fb67ade"></a>
#### TABLESPACE tablespace_name

인덱스가 재구축될 tablespace의 이름을 지정한다.

- tablespace_name을 지정할 경우
    - tablespace_name이 data tablespace면 LOGGING 인덱스로 재구축된다.
    - tablespace_name이 temporary tablespace 또는 nologging tablespace면 NOLOGGING 인덱스로 재구축된다.
- TABLESPACE 절을 생략할 경우, 기존 인덱스의 tablespace로 설정된다.

<a id="52d8529f4b7220e6"></a>
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

<a id="438d09a2d4e9c1d3"></a>
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

<a id="00ac18d7d82c8438"></a>
### 호환성

SQL 표준은 global secondary index에 대한 개념을 다루지 않고 있다.

<a id="a7a7ec21896d6cce"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#c41a3550730b3ad2)
- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#cad9ba4018feb93c)
- [ALTER INDEX name REBUILD](#0c9fcc7fd3031814)

<a id="93414efa5f655240"></a>
## ALTER TABLE name RENAME COLUMN

<a id="52ba78eb2fefb3f8"></a>
### 기능

테이블 column의 이름을 변경한다.

<a id="1c11db6e2ba5b011"></a>
### 구문

```
<rename column statement> ::=
    ALTER TABLE table_name 
        RENAME COLUMN old_column_name TO new_column_name
    ;
```

<a id="5b22c6092a0ff58b"></a>
### 사용 범위 및 접근 권한

&lt;rename column statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="b86311f7a5d1b6a8"></a>
### 구문 규칙 및 파라미터

<a id="8144bb9b9bc3aafc"></a>
#### table_name

변경할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="b224b19c3fd72847"></a>
#### old_column_name

변경할 column의 기존 이름이다.

<a id="e0ab414a7924dd52"></a>
#### new_column_name

변경할 column의 새로운 이름이다.   
테이블 내에 동일한 column 이름이 존재하지 않아야 한다.

<a id="317458c52e49f26f"></a>
### 설명

Column 이름이 변경되더라도 이전에 해당 column을 기준으로 생성된 index, constraint 등의 객체를 변경할 필요는 없다.

<a id="84ec972850264a8b"></a>
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

<a id="2b873adc13505603"></a>
### 호환성

SQL 표준에서는 &lt;rename column statement&gt; 구문을 정의하지 않고 있다.

<a id="dba61d3d3636cf82"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#79ce4cebdf753797)
- [ALTER TABLE name ADD COLUMN](#435e25d60c5f411d)
- [ALTER TABLE name SET UNUSED COLUMN](#d571baf9c1ff887c)
- [ALTER TABLE name ALTER COLUMN](#f9d752692bc80a55)

<a id="d90eeeee87655756"></a>
## ALTER TABLE name RENAME CONSTRAINT

<a id="4c75d58e562c65f9"></a>
### 기능

테이블 제약 조건의 이름을 변경한다.

<a id="321cccac20599c46"></a>
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

<a id="cf939b028ab11b65"></a>
### 사용 범위 및 접근 권한

&lt;rename table constraint statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA
- ALTER ANY TABLE ON DATABASE

<a id="b6b39ee0d832906b"></a>
### 구문 규칙 및 파라미터

<a id="91b0c4801cae255b"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="8d13fa0201cb518e"></a>
#### &lt;constraint object&gt;

변경할 제약 조건의 기존 이름은 다음과 같이 지정할 수 있다.

- CONSTRAINT constraint_name
    - 변경할 제약 조건의 이름이다.
- PRIMARY KEY
    - 테이블의 PRIMARY KEY 제약 조건이다.
- UNIQUE( column [,...] )
    - Column 목록에 부합되는 UNIQUE 제약 조건이다.

<a id="0e87d79d6a445e07"></a>
#### new_column_name

변경할 제약 조건의 새로운 이름이다.

<a id="7840ca702ca326d2"></a>
### 설명

Primary key, unique key와 같이 key 제약 조건으로 자동 생성된 index의 이름은 변경되지 않는다. Index 이름은 [ALTER INDEX name RENAME TO](#0908608fc2f457cb) 구문을 사용하여 변경해야 한다.

<a id="e7b2e5f2620be40e"></a>
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

<a id="aa6ec0adc9693aba"></a>
### 호환성

SQL 표준에서는 &lt;rename table constraint statement&gt; 구문을 정의하지 않고 있다.

<a id="fba9645b59b9acd2"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#79ce4cebdf753797)
- [ALTER TABLE name ADD CONSTRAINT](#01291e4c7e6b5226)
- [ALTER TABLE name DROP CONSTRAINT](#ee7de4b9dadd1b3a)
- [ALTER TABLE name ALTER CONSTRAINT](#e11c16dd8992ad1d)

<a id="5da03ed3f3bb106e"></a>
## ALTER TABLE name RENAME SHARD

<a id="593f3620d71e4ab3"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard의 이름을 변경한다.

<a id="000009c27c4b5752"></a>
### 구문

```
<alter table rename shard statement> ::=
    ALTER TABLE table_name 
        RENAME SHARD shard_name TO new_shard_name
    ;
```

<a id="bd99be1202a27aa0"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table rename shard statement&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="8d308efa14ef279c"></a>
### 구문 규칙 및 파라미터

<a id="8068d9552435e943"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="c90723e848c31ccf"></a>
#### shard_name

변경할 shard의 기존 이름이다.   
Shard가 해당 테이블에 존재하지 않을 경우 구문을 수행할 수 없다.

<a id="0818028549107c72"></a>
#### new_shard_name

변경할 shard의 새 이름이다.   
테이블 내에 동일한 shard 이름이 존재하지 않아야 한다.

<a id="859415e08cf87940"></a>
### 설명

Hash, range, list 테이블의 특정 shard의 이름을 변경한다. Cloned 테이블에 대해서는 해당 구문을 수행할 수 없다.

<a id="8cc1e6405488857d"></a>
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

<a id="48366af0da508fb7"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="79f622569669a892"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#79ce4cebdf753797)
- [ALTER TABLE name MOVE SHARD](#5179ebc66a584d79)
- [ALTER TABLE name SPLIT SHARD](#2846df311597b7a0)
- [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965)

<a id="9214266d4110406d"></a>
## ALTER TABLE name RENAME TO

<a id="6dd30421bcabe30e"></a>
### 기능

테이블의 이름을 변경한다.

<a id="b1adbb7072a22356"></a>
### 구문

```
<rename table statement> ::=
    ALTER TABLE table_name 
        RENAME TO new_table_name
    ;
```

<a id="6b71189e719b1c53"></a>
### 사용 범위 및 접근 권한

&lt;rename table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="10b22ff88f5960b2"></a>
### 구문 규칙 및 파라미터

<a id="6fa5db682e0366f6"></a>
#### table_name

테이블의 기존 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="db22d09df18a6589"></a>
#### new_table_name

테이블의 새 이름이다.   
스키마 내에 동일한 테이블 이름이 존재하지 않아야 한다.

<a id="baea5c746b3aca3c"></a>
### 설명

테이블 이름이 변경되더라도 이를 참조하는 index constraint 등의 객체는 변경할 필요없다.

<a id="cddbd457f39c843b"></a>
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

<a id="7b12f3127be940cf"></a>
### 호환성

SQL 표준에서는 &lt;rename table statement&gt; 구문을 정의하지 않고 있다.

<a id="e03ca3384f6cd403"></a>
### 참조

관련 내용은 [ALTER TABLE](#79ce4cebdf753797)을 참조한다.

<a id="d571baf9c1ff887c"></a>
## ALTER TABLE name SET UNUSED COLUMN

<a id="65dfc091eb7386b6"></a>
### 기능

테이블 column을 제거한다.

<a id="14b28ea1c4032417"></a>
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

<a id="41a893c0b5282997"></a>
### 사용 범위 및 접근 권한

&lt;drop column definition&gt; 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="ee9d2866e0da14d6"></a>
### 구문 규칙 및 파라미터

<a id="91488ab15ad40f66"></a>
#### table_name

변경할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="9e151cf9754de15e"></a>
#### SET UNUSED [ COLUMN ]

해당 column들을 사용하지 않도록 설정한다.

<a id="6723f4dee8d23f76"></a>
#### column_name_list

한 개 이상의 삭제될 column 이름이다.

- 예: ALTER TABLE t1 SET UNUSED COLUMN c1 
- 예: ALTER TABLE t1 SET UNUSED COLUMN (c1, c2)

<a id="6a3e918b10a88207"></a>
#### column_name

삭제할 column의 이름이다.   
해당 column을 이용하는 제약 조건과 인덱스도 함께 삭제한다.

<a id="617aeba0fff8671d"></a>
#### drop behavior

생략할 경우, 기본값은 RESTRICT 이다.   
현재는 RESTRICT/ CASCADE가 동일하게 작동한다.

<a id="7e9d99b4ed1e23b8"></a>
### 설명

SET UNUSED COLUMN은 data를 물리적으로 제거하지 않으므로 row의 개수에 관계없이 일정한 성능을 보장한다.

<a id="299f94a114eed770"></a>
### 사용 예

다음은 해당 column을 사용하지 않도록 설정하는 예이다.

```
gSQL> ALTER TABLE t1 SET UNUSED COLUMN ( addr );

Table altered.
```

<a id="c2adfddfd58e76aa"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- SET UNUSED 
- CASCADE CONSTRAINTS 
- 다수의 column 나열

**SQL 표준 호환성**

<a id="33eab322eb19768d"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F033 | ALTER TABLE statement: DROP COLUMN clause | X |

<a id="a47ee5d0a6a37587"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE](#79ce4cebdf753797)
- [ALTER TABLE name ADD COLUMN](#435e25d60c5f411d)
- [ALTER TABLE name ALTER COLUMN](#f9d752692bc80a55)
- [ALTER TABLE name RENAME COLUMN](#93414efa5f655240)

<a id="2846df311597b7a0"></a>
## ALTER TABLE name SPLIT SHARD

<a id="f30c9988856764d5"></a>
### 기능

Cluster 환경에서 테이블의 특정 shard를 split하여 재배치한다.

<a id="a713cff1d710ea7c"></a>
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

<a id="a03ef772ba83ab7d"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;alter table split shard statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="e3fdf9b1e1c78bcd"></a>
### 구문 규칙 및 파라미터

<a id="211c58e40c94bc1d"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
해당 테이블이 cluster group specific이고 list shard 또는 range shard인 경우에만 구문을 수행할 수 있다.

<a id="0b9c851dd311d7a2"></a>
#### source_shard_name

Split할 원본 shard 이름이다.   
해당 테이블에 shard가 존재하지 않을 경우 구문을 수행할 수 없다.

<a id="2d72c4a059638a44"></a>
#### &lt;split shard placement&gt;

원본 shard를 split하여 재배치할 대상 shard를 정의한다.

<a id="c825a50848adcc96"></a>
#### &lt;split shard bound def&gt;

split될 대상 shard의 bound를 정의한다.

다음 두 가지 bound def 중 하나로 정의할 수 있다.

- &lt;split list shard def&gt;
- &lt;split range shard def&gt;

<a id="e1814dfeb23ed059"></a>
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

<a id="a606b13bdf7d8570"></a>
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

<a id="e4528f1052862bdc"></a>
#### dest_group_name

Split 된 shard가 배치될 cluster group의 이름이다.

<a id="547cec963946c7ac"></a>
### 설명

특정 테이블의 특정 shard를 분산하여 임의의 cluster group에 배치한다.  
특정 shard에 해당하는 레코드가 많거나 특정 group member에 부하가 편중될 때 shard를 분산하여 레코드와 부하를 분산하기 위해 사용된다.

<a id="b30ce99e3f217c4b"></a>
### 사용 예

다음은 &lt;alter table split shard statement&gt; 구문을 수행하는 예이다.

```
gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES IN ( 11 ) AT CLUSTER GROUP G2 );

Table altered.

gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES LESS THAN ( 11 ) AT CLUSTER GROUP G2 );


Table altered.
```

<a id="9ecacc3b4d361721"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="844368edbb120151"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#1baf8de768cb0d19) 
- [ALTER TABLE name MOVE SHARD](#5179ebc66a584d79)
- [ALTER TABLE name MERGE SHARDS](#c29d9bc11c0a25f8)

<a id="54f34f813a8b169d"></a>
## ALTER TABLE name STORAGE

<a id="ebf66301fac87fe3"></a>
### 기능

테이블의 물리적 속성을 변경한다.

<a id="acc70d036501bab4"></a>
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

<a id="9936f66d8a9bc211"></a>
### 사용 범위 및 접근 권한

&lt;alter table physical attribute statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="bf82c4981a45fe3f"></a>
### 구문 규칙 및 파라미터

<a id="aada5663e36495b1"></a>
#### table_name

변경할 테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="8090d4dc0574dfdb"></a>
#### &lt;physical attribute clause&gt;

테이블을 구성하는 page의 물리적 속성을 변경한다.  
이미 할당된 page에는 적용되지 않으며 새로 할당받는 page에 적용된다.  
자세한 설명은 [CREATE TABLE](#9b82da6d66aabe8c) 구문의 &lt;[table physical attribute clause&gt;](#bba3a2da997925a8) 절을 참조한다.

<a id="fe0133d52a049b7e"></a>
#### &lt;segment attr clause&gt;

세그먼트를 구성하는 extent의 물리적 속성을 변경한다.   
이미 할당된 extent에는 적용되지 않으며, 새로 할당받는 extent에 적용된다.

- MAXSIZE integer 
    - 할당될 수 있는 세그먼트 공간의 크기를 변경한다. 
    - 이미 할당되어 있는 공간보다 작은 크기를 지정하면, MAXSIZE가 현재 할당되어 있는 크기로 변경된다.

<a id="d2a8245fde862b46"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="173686f0e1c3e96b"></a>
### 사용 예

다음은 테이블의 물리적 속성을 변경하는 예이다.

```
gSQL> ALTER TABLE t1 PCTFREE 10 PCTUSED 40 STORAGE ( NEXT 10M  MAXSIZE  100M );

Table altered.
```

<a id="5d950137da2e12ef"></a>
### 호환성

SQL 표준에서는 테이블의 물리적 속성에 대하여 정의하지 않고 있다.

<a id="c7bc47213cc6b2d5"></a>
### 참조

관련 내용은 [ALTER TABLE](#79ce4cebdf753797)을 참조한다.

<a id="bf506f295181b38d"></a>
## ALTER TABLESPACE

<a id="ef64e1a95b50e08e"></a>
### 기능

테이블스페이스의 정의를 변경한다.

<a id="830dd498b1da23aa"></a>
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

<a id="7733145dade3a95f"></a>
### 사용 범위 및 접근 권한

&lt;alter tablespace statement&gt; 구문을 수행하려면 사용자에게 database에 대한 ALTER TABLESPACE 권한이 있어야 한다.

<a id="084325d19de49e8c"></a>
### 구문 규칙 및 파라미터

<a id="f8842301a1edc0d5"></a>
#### &lt;rename tablespace statement&gt;

테이블스페이스의 이름을 변경한다.  
자세한 내용은 [ALTER TABLESPACE name RENAME TO](#d955f08f445fb965) 구문을 참조한다.

<a id="41474a18afb6cd81"></a>
#### &lt;backup tablespace statement&gt;

테이블스페이스를 백업한다.  
자세한 내용은 [ALTER TABLESPACE name BACKUP](#5c95f68797fd85d7) 구문을 참조한다.

<a id="309ab7ff3679b9b8"></a>
#### &lt;on-offline tablespace statement&gt;

테이블스페이스의 모든 파일을 online 또는 offline으로 변경한다.  
자세한 내용은 [ALTER TABLESPACE name [ONLINE|OFFLINE]](#501dd7429c17f768) 구문을 참조한다.

<a id="a31064f2c8d791de"></a>
#### &lt;add file statement&gt;

테이블스페이스에 파일을 추가한다.  
자세한 내용은 [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#c9983dcbc2b77c83) 구문을 참조한다.

<a id="c83c4c632f1eab04"></a>
#### &lt;drop file statement&gt;

테이블스페이스의 파일을 제거한다.  
자세한 내용은 [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#e004cab1dc94f9c0) 구문을 참조한다.

<a id="15a969ade5fce916"></a>
#### &lt;rename datafile statement&gt;

데이터 테이블스페이스의 데이터 파일 이름을 변경한다.  
자세한 내용은 [ALTER TABLESPACE name RENAME DATAFILE](#ab6203181b2f50fe) 구문을 참조한다.

<a id="436e0225b04139a3"></a>
### 설명

ALTER TABLESPACE 구문은 다른 Data Definition Language (DDL)과 달리 ROLLBACK 할 수 없고 구문을 수행한 transaction이 자동으로 COMMIT 된다.

<a id="80e8d042e0e32b23"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="bc7781d9995d3409"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="2f8e5098b91d8450"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLESPACE](#53b7fdb5c5a23059)
- [DROP TABLESPACE](#703c847167e78d53)

<a id="c9983dcbc2b77c83"></a>
## ALTER TABLESPACE name ADD [DATAFILE|MEMORY]

<a id="89296218e4d8c2b5"></a>
### 기능

테이블스페이스의 공간을 확장한다.

<a id="b8a5960b364af3ec"></a>
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

<a id="31e2d6daeee057e5"></a>
### 사용 범위 및 접근 권한

&lt;add space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="44d7bcce437932b2"></a>
### 구문 규칙 및 파라미터

<a id="6042753ad6c75fb7"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="12d13b889c50bf3f"></a>
#### &lt;file specification&gt;

테이블스페이스의 유형에 따라 다음과 같은 구문을 사용해야 한다.

- 메모리 데이터 테이블스페이스 
    - DATAFILE &lt;add datafile clause&gt; 
- 메모리 임시 테이블스페이스 
    - MEMORY &lt;memory clause&gt;

<a id="b555f7b4da03e833"></a>
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

<a id="5fbf9d0a0c3c4322"></a>
#### &lt;memory clause&gt;

- &lt;size clause&gt;
    - 추가할 메모리를 정의한다.

자세한 내용은 [CREATE MEMORY TEMPORARY TABLESPACE](#bcdcadc8e58b6578) 구문의 &lt;[memory clause&gt;](#53e59b4ae7574a57)를 참조한다.

<a id="05b423378f6239ad"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="ebd602a3bde71e89"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="20f68ee8dfac986b"></a>
### 사용 예

다음은 테이블스페이스에 data file을 추가하는 예이다.

```
gSQL> ALTER TABLESPACE space1 ADD DATAFILE 'test_file_a2.dbf' SIZE 10M REUSE;

Tablespace altered.
```

<a id="da3d9e65761bb769"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="d3a7297f66777d4e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE MEMORY DATA TABLESPACE](#e61b814a9f21f32f)
- [CREATE MEMORY TEMPORARY TABLESPACE](#bcdcadc8e58b6578)
- [ALTER TABLESPACE](#bf506f295181b38d)

<a id="5c95f68797fd85d7"></a>
## ALTER TABLESPACE name BACKUP

<a id="8a97b3720147d4b8"></a>
### 기능

테이블스페이스를 backup 하기 위해 backup이 가능한 상태와 불가능한 상태로 전환한다.

<a id="1615a0a2eab2e629"></a>
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

<a id="bcfb9a0790a19e5a"></a>
### 사용 범위 및 접근 권한

&lt;backup space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="c1e68ccdd96bc9e8"></a>
### 구문 규칙 및 파라미터

<a id="3e0e524ace9785b1"></a>
#### &lt;tablespace begin backup statement&gt;

테이블스페이스를 백업 가능한 상태로 설정한다.

- 생성되어 사용 중인 테이블스페이스를 백업 가능한 상태로 설정한다.
- OFFLINE/ temporary 테이블스페이스는 backup 상태는 전환할 수 없다.

<a id="48b1d84224fb06d5"></a>
#### tablespace_name

Backup 상태를 전환할 테이블스페이스의 이름이다.

<a id="5c01d61f89f855c2"></a>
#### &lt;tablespace end backup statement&gt;

테이블스페이스를 백업이 불가능한 상태로 설정한다.

<a id="e1b601c58e6e2a7b"></a>
#### &lt;tablesapce incremental backup statement&gt;

테이블스페이스의 증분 백업을 수행한다.  
데이터베이스가 OPEN 상태이고, ARCHIVELOG로 운영되어야 한다.

<a id="9dc6b9ea789d4e01"></a>
#### &lt;incremental backup option&gt;

- 'integer'는 0 ~ 4 까지 지정할 수 있다.
- 'LEVEL 0'는 CUMULATIVE나 DIFFERENTIAL을 지정할 수 없다.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - 'integer'가 n이면 가장 최근에 'LEVEL 0' ~ 'LEVEL n-1'까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - DIFFERENTIAL
        - 'integer'가 n이면 가장 최근에 'LEVEL 0' ~ 'LEVEL n'까지 백업한 이후 변경된 모든 페이지들을 백업한다.
    - 생략되면 DIFFERENTIAL이 기본으로 지정된다.

<a id="efda5a58af4dd841"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="883afb25c78ba7af"></a>
### 설명

테이블스페이스에 생성된 datafile을 백업한다. 테이블스페이스 전체를 백업하려면 BEGIN BACKUP을 수행한 후 OS의 파일 복사로 datafile들을 복사하고 나서 END BACKUP을 수행한다. 한편, 증분 백업 파일은 하나의 구문으로 BACKUP_DIR_1 property에 설정된 경로에 생성한다.

<a id="f1fefbeadac55b50"></a>
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

<a id="64765d6423d41f83"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="4e89a4aaf0d4bb7e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#bf506f295181b38d)
- [ALTER TABLESPACE name [ONLINE|OFFLINE]](#501dd7429c17f768)

<a id="e004cab1dc94f9c0"></a>
## ALTER TABLESPACE name DROP [DATAFILE|MEMORY]

<a id="06410d34392d50eb"></a>
### 기능

테이블스페이스의 공간을 축소한다.

<a id="42676674db2d2e0f"></a>
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

<a id="4766df19765643ad"></a>
### 사용 범위 및 접근 권한

&lt;drop space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="40ccf2b8f44e0706"></a>
### 구문 규칙 및 파라미터

<a id="b367e88b37c5dc5c"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="3d647c481566dfed"></a>
#### &lt;file specification&gt;

테이블스페이스의 유형에 따라 다음과 같은 구문을 사용해야 한다.

- 메모리 데이터 테이블스페이스 
    - DATAFILE 'filename' 
- 메모리 임시 테이블스페이스 
    - MEMORY 'memory_name'

> 오프라인 테이블스페이스의 파일은 삭제할 수 없다.   
> 테이블스페이스의 첫 번째 파일은 삭제할 수 없다.  
> 한 번이라도 사용된 적이 있는 데이터 파일은 삭제할 수 없다.

<a id="76a54ef1942ac453"></a>
#### &lt;domain name&gt;

구문을 수행하는 멤버 및 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="81df3a23db5058fc"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="21b041cfe6df185d"></a>
### 사용 예

다음은 테이블스페이스의 파일을 제거하는 예이다.

```
gSQL> ALTER TABLESPACE space1 DROP DATAFILE 'test_file_f2.dbf';

Tablespace altered.
```

<a id="b86461f9ec956301"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="0e95426f48e9c86e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#bf506f295181b38d)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#c9983dcbc2b77c83)
- [ALTER TABLESPACE name RENAME DATAFILE](#ab6203181b2f50fe)

<a id="501dd7429c17f768"></a>
## ALTER TABLESPACE name [ONLINE|OFFLINE]

<a id="069eccfb88f02711"></a>
### 기능

테이블스페이스 상태를 변경한다.

<a id="6620c38a167e1e76"></a>
### 구문

```
<on/off tablespace statement> ::=
    ALTER TABLESPACE tablespace_name { ONLINE | OFFLINE [ NORMAL | IMMEIDATE ] }
    [ AT <domain name> ]
    ;
```

<a id="85e546c7940836b0"></a>
### 사용 범위 및 접근 권한

&lt;on/off tablespace statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="49b7b32de0a6417c"></a>
### 구문 규칙 및 파라미터

<a id="9b1519a35ea53018"></a>
#### ONLINE

OFFLINE 상태의 테이블스페이스를 ONLINE으로 변경한다.

<a id="cd256f4a46e19b2c"></a>
#### OFFLINE NORMAL

ONLINE 상태의 테이블스페이스를 OFFLINE으로 변경한다.

OFFLINE으로 변경된 테이블스페이스는 일관된 (consistent) 상태이기 때문에 ONLINE 상태로 변경할 때 미디어 복구할 필요없다.

> MOUNT 단계에서는 OFFLINE NORMAL을 사용할 수 없다.   
> (단, 이전 인스턴스가 `\`SHUTDOWN NORMAL에 의해서 종료된 경우에는 가능하다.)

<a id="755c05b24200e7c4"></a>
#### OFFLINE IMMEDIATE

ONLINE 상태의 테이블스페이스를 OFFLINE으로 변경한다.

OFFLINE으로 변경된 테이블스페이스는 비일관적인 (inconsistent) 상태이기 때문에, ONLINE 상태로 변경할 때 미디어 복구해야 한다.

> SYSTEM 테이블스페이스는 OFFLINE으로 변경할 수 없다.   
> OFFLINE IMMEDIATE는 미디어 복구를 필요로 하기 때문에 archive log mode에서만 수행할 수 있다.

<a id="d09f7cdd3e85da17"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="3335ed875ad2eae8"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="deed282a0df9621a"></a>
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

<a id="e93a635047ab34ba"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="94db338e9bcefae5"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#bf506f295181b38d)
- [ALTER TABLESPACE name BACKUP](#5c95f68797fd85d7)

<a id="ab6203181b2f50fe"></a>
## ALTER TABLESPACE name RENAME DATAFILE

<a id="fd666f9b532e75b9"></a>
### 기능

테이블스페이스를 구성하는 데이터 파일의 이름을 변경한다.

<a id="01862417da69d4ab"></a>
### 구문

```
<rename datafile statement> ::=
    ALTER TABLESPACE tablespace_name RENAME DATAFILE <filename_list> TO <filename_list>
    ;

    <filename_list> ::= 
        'filename' [ AT <domain name> ] [, ...]
```

<a id="f38cf76a21144c00"></a>
### 사용 범위 및 접근 권한

&lt;rename datafile statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

> TDS 모드이면서 데이터베이스가 OPEN인 상태에서는 온라인 테이블스페이스 파일을 변경할 수 없다. (임시 메모리 테이블스페이스는 제외된다.)   
> 변경한 후에도 파일은 반드시 존재해야 한다.

<a id="8123ad7adc5fe23d"></a>
### 구문 규칙 및 파라미터

<a id="28a00e50b9eb7e3b"></a>
#### tablespace_name

변경할 테이블스페이스의 이름이다.

<a id="5fbf1b6da48b2b55"></a>
#### 'filename'

메모리 임시 테이블스페이스는 'memory_name'을 의미하며, 그 외의 테이블스페이스 종류는 'filename'을 의미한다.

<a id="7fc4e5f816ec8e71"></a>
#### &lt;domain name&gt;

구문을 수행할 멤버나 그룹의 이름이다.   
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="cb59afbd0673e88c"></a>
### 설명

테이블스페이스 상태에 따라 연산 가능 여부가 결정된다.

- OFFLINE: MOUNT 단계나 OPEN 단계에서 수행 가능하다.
- ONLINE: MOUNT 단계에서만 수행 가능하다.

<a id="d58d22dc1a5ca63f"></a>
### 사용 예

다음은 'test.dbf'를 'test1.dbf'로 변경하는 예이다.

```
gSQL> ALTER TABLESPACE TEST_TBS RENAME DATAFILE 'test.dbf' TO 'test1.dbf';

Tablespace altered.
```

<a id="932d7aff1c8bf5ea"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="b400ba302b4ad2a8"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ALTER TABLESPACE](#bf506f295181b38d)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#c9983dcbc2b77c83)
- [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#e004cab1dc94f9c0)

<a id="d955f08f445fb965"></a>
## ALTER TABLESPACE name RENAME TO

<a id="1514d3e631f0917e"></a>
### 기능

테이블스페이스의 이름을 변경한다.

<a id="55b2c7a1c0d5d03c"></a>
### 구문

```
<rename tablespace statement> ::=
    ALTER TABLESPACE tablespace_name RENAME TO <new_tablespace_name>
    ;
```

<a id="fd20a37921db62d2"></a>
### 사용 범위 및 접근 권한

&lt;rename space statement&gt; 구문을 수행하려면 사용자에게 ALTER TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="28e96e22b8e8f79e"></a>
### 구문 규칙 및 파라미터

<a id="aeea538e18e73336"></a>
#### tablespace_name

기존 테이블스페이스의 이름이다.

- Built-in 테이블스페이스의 이름은 변경할 수 없다.
- OFFLINE 테이블스페이스의 이름은 변경할 수 없다.

<a id="ab59f99a8f5813dc"></a>
#### new_tablespace_name

새로운 테이블스페이스의 이름이다.

<a id="b87a2e6551f32bb3"></a>
### 설명

Tablespace 이름이 변경되더라도 기존에 이미 해당 tablespace에 생성된 table, index 등은 변경할 필요없다.

<a id="40b68b32f1a6cd8f"></a>
### 사용 예

다음은 테이블스페이스의 이름을 변경하는 예이다.

```
gSQL> ALTER TABLESPACE space1 RENAME TO space2;

Tablespace altered.
```

<a id="2fef73e4a8356387"></a>
### 호환성

SQL 표준에서는 테이블스페이스 개념을 정의하지 않고 있다.

<a id="3065dd290ac39008"></a>
### 참조

관련 내용은 [ALTER TABLESPACE](#bf506f295181b38d)를 참조한다.

<a id="268a4621fc85878c"></a>
## ALTER USER

<a id="c6e6f7a7d6e11970"></a>
### 기능

데이터베이스 사용자 정의를 변경한다.

<a id="7379061610eee2fc"></a>
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

<a id="7190935b2e77831f"></a>
### 사용 범위 및 접근 권한

&lt;alter user statement&gt; 구문을 수행하려면 사용자에게 ALTER USER ON DATABASE 권한이 있어야 한다.  
단, &lt;alter password&gt;는 사용자가 user_identifier와 동일할 경우에 권한 없이 수행할 수 있다.

<a id="4278cf22e8006d45"></a>
### 구문 규칙 및 파라미터

<a id="1b30b5c118c542ab"></a>
#### user_identifier

변경할 사용자의 이름이다.

<a id="350a53ec2bb50d40"></a>
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

<a id="e2515bc087f1e98b"></a>
#### &lt;alter profile&gt;

비밀번호 관리 정책을 위한 profile을 변경한다.

- PROFILE profile_name
    - 사용자가 생성한 profile_name을 할당한다.
- PROFILE DEFAULT
    - 기본 profile인 "DEFAULT"를 할당한다.
- PROFILE NULL
    - Profile을 할당하지 않는다.

<a id="3fc7da4875625ba5"></a>
#### &lt;password expire&gt;

사용자의 비밀번호를 만료시킨다.

<a id="38162e1263473ecf"></a>
#### &lt;account lock&gt;

- ACCOUNT LOCK
    - 사용자 계정을 잠근다. 
- ACCOUNT UNLOCK
    - 계정 잠금을 해제한다.

<a id="29ad9a5349e8d429"></a>
#### &lt;alter default tablespace&gt;

사용자의 기본 tablespace를 변경한다.   
tablespace_name은 data tablespace여야 한다.

<a id="7f150ea234ca8ed7"></a>
#### &lt;alter temporary tablespace&gt;

사용자의 temporary tablespace를 변경한다.   
tablespace_name은 temporary tablespace여야 한다.

<a id="f751db67cc6a7747"></a>
#### &lt;alter index tablespace&gt;

사용자의 index tablespace를 변경한다.

- INDEX TABLESPACE tablespace_name을 지정한다.
    - Data tablespace를 지정한 경우, LOGGING 인덱스가 된다.
    - Temporary tablespace를 지정한 경우, NOLOGGING 인덱스가 된다.
- INDEX TABLESPACE NULL
    - Index tablespace를 지정하지 않는다.

<a id="a13866ec08833984"></a>
#### &lt;alter schema path&gt;

사용자의 스키마 접근 경로를 변경한다.   
사용자의 SQL 구문에 schema가 명시되지 않았을 경우 스키마 접근 경로는 객체의 naming resolution을 위한 스키마 순서에 따라 결정된다.

스키마 이름이 기존에 스키마 접근 경로에 나열된 스키마 이름과 동일할 경우에는 추가적으로 반영되지 않는다.

다음은 *ALTER USER u1 SCHEMA PATH ( u1, s2, public );* 구문을 수행했을 때 schema에 존재하는 객체의 예이다.

<a id="e9c67d5b25578e3f"></a>
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

<a id="ad11b4a3ea4b0dde"></a>
#### CURRENT PATH

현재 사용자의 schema path 이다.

다음 예와 같이 CURRENT PATH를 이용해 기존의 schema path를 유지하면서 새로운 schema path를 추가할 수 있다.

- u1의 현재 schema path 
    - (u1, public) 
- 구문 수행 
    - ALTER USER u1 SCHEMA PATH ( s1, CURRENT PATH, s2 ); 
- u1의 schema path는 다음과 같이 변경된다. 
    - (s1, u1, public, s2)

<a id="6186c3ff912f7a98"></a>
#### ALTER USER PUBLIC &lt;alter schema path&gt;

PUBLIC 계정의 schema path를 변경한다.   
PUBLIC 계정의 schema path는 모든 사용자의 schema path에 포함된다.

PUBLIC 계정에 최초로 부여된 schema path는 다음과 같다.

- DICTIONARY_SCHEMA 
- INFORMATION_SCHEMA 
- DEFINITION_SCHEMA 
- PERFORMANCE_VIEW_SCHEMA 
- FIXED_TABLE_SCHEMA

<a id="404ef08c652aeb6e"></a>
### 설명

각 구문별 사용 규칙을 참조한다.

<a id="8145cf7189d5d02a"></a>
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

<a id="318484bc1ffb981d"></a>
### 호환성

SQL 표준에서 user의 개념은 다루고 있지만 user의 생성, 변경 및 삭제와 관련된 SQL 구문은 정의하지 않고 있다.

<a id="b28c5620ead3126d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE USER](#8e5920c927752802)
- [DROP USER](#886267e56d7bc6a6)

<a id="96b15c85b467a50c"></a>
## ALTER VIEW

<a id="e9089a64d8673f8d"></a>
### 기능

View 정의를 변경한다.

<a id="a8d166bd97e5f15f"></a>
### 구문

```
<alter view statement> ::=
    ALTER VIEW view_name <alter view action>
    ;

<alter view action> ::=
    COMPILE
```

<a id="0fed614765ebbdd8"></a>
### 사용 범위 및 접근 권한

&lt;alter view statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 view에 대해 (ALTER 또는 CONTROL TABLE) ON TABLE 
- View가 속한 스키마에 대해 (ALTER TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- ALTER ANY TABLE ON DATABASE

<a id="2416b3329b89b597"></a>
### 구문 규칙 및 파라미터

<a id="20fe9808e1c6e087"></a>
#### view_name

변경할 view의 이름이다.  
schema_name.view_name과 같이 view가 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="77009faf5362ba48"></a>
#### COMPILE

View를 다시 컴파일한다.   
View column에 부여한 COMMENT는 초기화된다.

<a id="7b4dc820d1d634a8"></a>
### 설명

View가 참조하는 테이블이나 view가 변경되거나 삭제되면 해당 view도 영향을 받는다.

이런 정보는 INFORMATION_SCHEMA.VIEWS를 통해 조회할 수 있다.

- IS_COMPILED column
    - TRUE: View가 정상적으로 생성되었다.
    - FALSE: 에러가 존재하는 상태에서 FORCE 옵션으로 view가 생성되었다.

- IS_AFFECTED column
    - TRUE : View가 참조하는 테이블 또는 view가 변경되었다.
    - FALSE: View가 생성되고 COMPILE 된 후에 view가 참조하는 테이블이나 view가 변경되지 않았다.

<a id="197d705bf411dc9d"></a>
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

<a id="8ff679042986d662"></a>
### 호환성

SQL 표준에서는 &lt;alter view statement&gt; 구문을 정의하지 않고 있다.

<a id="64b939be3560e888"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE VIEW](#a71e7cc52f1eefb4)
- [DROP VIEW](#01da7763edf4f3e5)

<a id="73eda964c57a6d05"></a>
## ANALYZE SYSTEM

<a id="e6276956de77a6f0"></a>
### 기능

시스템의 통계 정보를 제어한다.

<a id="d75b9e8a5bc9facb"></a>
### 구문

```
<analyze system statement> ::=
    ANALYZE SYSTEM [ <analyze action> ]
    ;

<analyze action> ::=
      COMPUTE STATISTICS
    | DELETE STATISTICS
```

<a id="c5d3ab1dbb681a0c"></a>
### 사용 범위 및 접근 권한

&lt;analyze system statement&gt; 구문을 수행하려면 사용자에게 ANALYZE ANY ON DATABASE 권한이 있어야 한다.

<a id="60442f15326c3ac9"></a>
### 구문 규칙 및 파라미터

<a id="0b3deaf5e87636d6"></a>
#### &lt;analyze action&gt;

생략할 경우 기본값은 COMPUTE STATISTICS 이다.

<a id="6da0e59b6790bd9a"></a>
#### COMPUTE STATISTICS

시스템과 관련된 다음과 같은 통계 정보를 구축한다.

- CPU_OPS (Operations Per Second) 
    - CPU가 초당 처리할 수 있는 operation의 개수이다.

- NETWORK_IOPS (IO operations Per Second) 
    - Cluster인 경우에 유효하다. 
    - 초당 처리할 수 있는 network IO 횟수이다.

<a id="c86a26c006f2c475"></a>
#### DELETE STATISTICS

시스템 통계 정보를 삭제한다.

<a id="3063a38715f0073d"></a>
### 설명

구축한 시스템 통계 정보는 질의 처리를 위한 최적화 과정의 비용을 계산하기 위해 사용한다.

<a id="2ae53600edcd50f1"></a>
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

<a id="27d7f165bd2fb7fa"></a>
### 호환성

SQL 표준에서는 통계 정보에 대한 개념을 정의하지 않고 있다.

<a id="9f9cbd79898fbfce"></a>
### 참조

관련 내용은 [ANALYZE TABLE](#d6e173b64ebe5b6c)을 참조한다.

<a id="d6e173b64ebe5b6c"></a>
## ANALYZE TABLE

<a id="4f7cc0246655a0eb"></a>
### 기능

테이블의 통계 정보를 제어한다.

<a id="f7312c08f9751ca1"></a>
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

<a id="c2691067c0a20e25"></a>
### 사용 범위 및 접근 권한

&lt;analyze table statement&gt; 구문을 수행하려면 사용자에게 ANALYZE ANY ON DATABASE 권한이 있어야 한다.

<a id="36a7eae3bc36a1b6"></a>
### 구문 규칙 및 파라미터

<a id="965bd7fe8400c4e6"></a>
#### table_name

테이블 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="28fccac0458da4dd"></a>
#### &lt;parallel clause&gt;

분석 과정에서 사용할 thread 개수를 지정한다.   
명시하지 않을 경우, 기본값은 PARALLEL 이다.

- NOPARALLEL
    - 병렬로 분석하지 않는다.

- PARALLEL [thread_count]
    - 병렬로 분석한다.
    - thread_count 값은 0 부터 사용할 수 있으며 최대값은 64 이다.
    - thread_count 값이 0이거나 생략된 경우 시스템의 CPU 개수에 의해 결정된다.

<a id="d52387ce840dcc2c"></a>
#### &lt;analyze action&gt;

생략할 경우 기본값은 COMPUTE STATISTICS 이다.

<a id="9a3dd76d955777ba"></a>
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

<a id="e855ee3987d8b46e"></a>
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

<a id="13ee2d9dd37c2991"></a>
#### ESTIMATE STATISTICS &lt;sample_clause&gt;

지정한 &lt;sample_clause&gt;만큼의 샘플을 사용하여 column과 index의 통계 정보를 구축한다.

- SAMPLE row_count ROWS 
    - 지정한 row 개수만큼 샘플을 사용한다. 
    - row_count는 0보다 큰 양의 정수이다. 
- SAMPLE percentage PERCENT 
    - 지정한 비율만큼 샘플을 사용한다. 
    - Percentage는 1 ~ 99 범위의 양의 정수이다.

샘플링 row의 개수가 [MIN_SAMPLE_ROW_COUNT](../part-02-administration-manual/10-server-property.md#e85de78158d7e20a) 프로퍼티 값보다 작을 경우 프로퍼티 값을 따른다.

<a id="d6cba9ebfdb700e6"></a>
#### &lt;for_clause&gt;

생략할 경우, 통계정보 구축이 가능한 모든 column과 모든 인덱스의 통계 정보를 구축한다.

<a id="a8c35e4f00218d35"></a>
#### FOR ALL COLUMNS

통계 정보 구축이 가능한 모든 column의 통계 정보를 구축한다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="81dd6f953e9c1627"></a>
#### FOR ALL INDEXED COLUMNS

인덱스에 포함된 모든 column의 통계 정보를 구축한다.   
그 외 column의 통계 정보는 구축하지 않는다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="df04ad420a4532e6"></a>
#### FOR COLUMNS column_name [, ...]

나열한 column의 통계 정보를 구축한다.   
기술하지 않은 column의 통계 정보는 구축하지 않는다.   
인덱스 통계 정보는 구축하지 않는다.

<a id="728b10d744cac378"></a>
#### FOR ALL INDEXES

모든 인덱스의 통계 정보를 구축한다.   
Column 통계 정보는 구축하지 않는다.

<a id="9aa67a25a7e77663"></a>
#### FOR INDEXES index_name [, ...]

나열한 인덱스의 통계 정보를 구축한다.   
기술하지 않은 인덱스의 통계 정보는 구축하지 않는다.   
Column 통계 정보는 구축하지 않는다.

<a id="4840a393f9b4dfb6"></a>
#### DELETE STATISTICS

테이블의 통계 정보를 제거한다.

<a id="b30a0fc3d19e1d2f"></a>
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

<a id="cffde063f673bd4e"></a>
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

<a id="694a2bad165b4e12"></a>
### 호환성

SQL 표준에서는 통계 정보에 대한 개념을 정의하지 않고 있다.

<a id="1bc58c181e32175e"></a>
### 참조

관련 내용은 [ANALYZE SYSTEM](#73eda964c57a6d05)을 참조한다.

<a id="8c7812c0671b6a25"></a>
## AUDIT POLICY

<a id="ca8db6f2becd0886"></a>
### 기능

Audit policy를 활성화한다.

<a id="09ae0169404e1aea"></a>
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

<a id="45b27ca92b1a0ad9"></a>
### 사용 범위 및 접근 권한

&lt;audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="165c6517ae1ae04a"></a>
### 구문 규칙 및 파라미터

<a id="fe907f5a5dba5a77"></a>
#### policy_name

활성화할 audit policy 객체의 이름이다.   
활성화 된 audit policy는 기존 session에 영향을 미치지 않으며 새로 생성되는 session에만 영향을 준다.

<a id="04c53a57a4bed376"></a>
#### &lt;specified_user_option&gt;

감사를 수행할 사용자를 명시한다.     
생략할 경우 모든 사용자에 대해 감사를 수행한다.

동일한 audit policy에 대해 BY 절과 EXCEPT 절을 함께 사용할 수 없다.

- BY user_list: 감사를 수행할 사용자를 특정할 경우 BY 절을 사용한다.
- EXCEPT user_list: 특정 사용자를 배제하고 다른 사용자들을 감사할 경우 EXCEPT 절을 사용한다.

<a id="00fcfb779cfd473b"></a>
#### &lt;specified_success_option&gt;

- WHENEVER SUCCESSFUL
    - Action이 성공했을 때 audit record가 생성된다.
- WHENEVER NOT SUCCESSFUL
    - Action이 실패했을 때 audit record가 생성된다.
- 생략할 경우 성공할 경우와 실패할 경우 모두 audit record를 생성한다.

<a id="eba53d7dbb4e35c3"></a>
### 설명

Audit policy를 활성화하면 기존 session에는 영향을 미치지 않으며 새로 생성되는 session에 대해 감사를 시작한다.

<a id="ebac646dad51a1fa"></a>
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

<a id="2f5ccef53daf500f"></a>
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

<a id="6a726a8faacb8af2"></a>
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

<a id="e67db850fd9695f4"></a>
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

<a id="d850f8ed3c112d19"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="b8c857471d55b540"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#09b3895daf4991da)
    - [DROP AUDIT POLICY](#4c985d8424a9c9e1)
    - [ALTER AUDIT POLICY](#241fd4b15c525c5a)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#8c7812c0671b6a25)
    - [NOAUDIT POLICY](#f4896aa89ec963af)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#6c787a4b953e8625)

- Audit trail 소거: [ALTER DATABASE CLEAR AUDIT TRAIL](#d0a56f6310b7a28c)

<a id="38584f03f4e1823e"></a>
## CLOSE cursor_name

<a id="1449e221c227a441"></a>
### 기능

커서를 닫는다.

<a id="c4b4582443ea337f"></a>
### 구문

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="76bd4733f9080102"></a>
### 구문 규칙 및 파라미터

<a id="dc399dd4e5d303c6"></a>
#### cursor_name

커서가 open 되어 있어야 한다.  
세션 내에서 [DECLARE cursor_name](#45b9d98474d5f09d) 구문으로 선언된 커서이어야 한다.

<a id="3e45a3489023d806"></a>
### 설명

Cursor는 session 내에 존재하는 객체이고 서로 다른 session의 cursor에 영향을 주지 않는다.

<a id="0286949f21aa07c7"></a>
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

<a id="2ef574bd37e7e5a1"></a>
### 호환성

**SQL 표준 호환성**

<a id="6b9a38effb17e637"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic dynamic SQL | O |

<a id="00939237862d9e59"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#45b9d98474d5f09d)
- [OPEN cursor_name](#ee8cdd33c43f9c76)
- [FETCH cursor_name](#bafc38978b00122c)

<a id="9dee57a337c9ae81"></a>
## COMMENT ON name IS

<a id="9f3c3bc7b1ba6b61"></a>
### 기능

객체에 대한 설명을 dictionary에 저장한다.

<a id="5c748f63b076fa76"></a>
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

<a id="0e0eae72e6ccbf22"></a>
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

<a id="5151cf5e1dc959bc"></a>
### 구문 규칙 및 파라미터

<a id="da9d8627d273a3f3"></a>
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

Schema object의 경우 schema_name을 기술하지 않으면 구문을 수행하는 사용자의 [Schema Path](13-sql-objects.md#af5f5168830f70fb)에 의해 스키마 이름이 결정된다.

```
COMMENT ON TABLE test_table IS 'test comment'; 
→ COMMENT ON TABLE user_default_schema.test_table IS 'test comment';
```

<a id="a90d71ff8a442562"></a>
#### 'comment string'

저장할 comment 문장을 기술한다.   
Comment를 삭제하려면 다음과 같이 empty string ('')을 사용한다.

```
COMMENT ON TABLE test_table IS '';
```

comment string의 길이는 1024 bytes를 초과할 수 없다.

<a id="30dc6d59b51e5e68"></a>
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

각 view에 대한 자세한 내용은 [DICTIONARY_SCHEMA](../part-02-administration-manual/9-database-information.md#26ad9a84eb1934b9)를 참조한다.

<a id="064bdd1975141402"></a>
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

<a id="6f71ad4e684ccd99"></a>
### 호환성

SQL 표준에는 &lt;comment statement&gt;가 없다.

<a id="4d322680eba93c4a"></a>
## COMMIT

<a id="dbe561d8a9f9ddff"></a>
### 기능

현재 트랜잭션을 종료하고, 변경된 모든 내용을 영속화한다.

<a id="977b13ae5c4fc54f"></a>
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

<a id="c9db86ebd74d1ef0"></a>
### 구문 규칙 및 파라미터

<a id="276989de1cf76be7"></a>
#### WORK

동작에 영향을 미치지 않는 예약어이다.

<a id="dd6351a7880759eb"></a>
#### &lt;commit comment clause&gt;

- COMMENT 'comment_string'
    - 트랜잭션을 commit 할 때 트랜잭션에 주석을 지정한다.

<a id="5ae80062262e55b0"></a>
#### &lt;commit write clause&gt;

Commit 연산으로 생성된 redo log가 redo log file에 기록될 때까지 기다릴지 여부를 결정한다.

- WAIT
    - commit 연산에 의해서 생성된 redo log가 redo log file에 기록될 때까지 기다린 후 연산을 종료한다.
- NOWAIT
    - commit 연산에 의해서 생성된 redo log가 redo log 버퍼에 기록되면 연산을 종료한다.
- 지정되어 있지 않을 경우, 프로퍼티를 따른다.

<a id="cbff87ecc27288bc"></a>
#### &lt;commit force clause&gt;

분산 트랜잭션을 수동으로 commit 할 때 사용한다.

- FORCE 'xid_string'
    - 'xid_string'에 해당하는 분산 트랜잭션을 commit 한다.
    - 'xid_string'은 '*format_id*.*transaction_id*.*branch_id*'로 구성된다.

<a id="a324a4e46ed3ea41"></a>
### 설명

COMMIT 구문은 트랜잭션 내에서 수행된 다음 구문들을 완료한다.

- Data Manipulation Language (DML) 구문
    - 데이터를 변경하는 INSERT, UPDATE, DELETE 등의 구문
- Data Definition Language (DDL) 구문 
    - 객체의 구조 및 정의를 변경하는 CREATE, DROP, ALTER, TRUNCATE, GRANT, REVOKE 등의 구문

예외적으로, DDL 중에 OS 자원을 다루거나 DATA TYPE을 변경하는 다음 구문들은 자동으로 COMMIT 된다.

- [CREATE TABLESPACE](#53b7fdb5c5a23059)
- [DROP TABLESPACE](#703c847167e78d53)
- [ALTER TABLESPACE](#bf506f295181b38d)
- ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE: &lt;[alter column data type clause&gt;](#d66887582dde4234)

COMMIT을 수행하면 WITHOUT HOLD 옵션으로 열린 커서는 자동으로 닫힌다. 커서에 대한 자세한 내용은 다음의 커서 관련 구문을 참조한다.

- [DECLARE cursor_name](#45b9d98474d5f09d)
- [OPEN cursor_name](#ee8cdd33c43f9c76)

트랜잭션이 지연된 (DEFERRED) 제약 조건을 위반하면 COMMIT 구문의 수행은 실패하고 트랜잭션은 ROLLBACK 된다. 지연된 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](#0ec9d72169df1ed8) 구문의 설명을 참조한다.

<a id="0a0ee5b937b1590b"></a>
### 사용 예

다음은 INSERT 구문을 수행한 후에 COMMIT을 수행하는 예이다.

```
gSQL> INSERT INTO t1 VALUES ( 1, 'anonymous' );

1 row created.

gSQL> COMMIT WORK COMMENT 'INSERT T1';

Commit complete.
```

<a id="5931dbcdd97c2ba4"></a>
### 호환성

**SQL 표준 호환성**

<a id="1b0a7824170b4916"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T261 | Chained transactions | X |

<a id="35f25c5568779914"></a>
### 참조

관련 내용은 다음을 참조한다.

- [ROLLBACK](#eaa6143895b543a3)
- [SAVEPOINT savepoint_specifier](#f7bc15577098099a)

<a id="09b3895daf4991da"></a>
## CREATE AUDIT POLICY

<a id="52484fe5545ef37c"></a>
### 기능

Audit policy 객체를 생성한다.   
생성한 audit policy 객체를 활성화하려면 AUDIT POLICY 구문을 수행하여야 한다.

<a id="d66281eca303ee7a"></a>
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

<a id="2f7eee183b12ccab"></a>
### 사용 범위 및 접근 권한

&lt;audit policy definition&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="ab8df531761db5db"></a>
### 구문 규칙 및 파라미터

<a id="606b3c15c59d936b"></a>
#### policy_name

생성할 audit policy의 이름이다.

<a id="780a125e7367cf76"></a>
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

<a id="c781c9b2dd9a16e6"></a>
#### &lt;action_audit_clause&gt;

특정 객체에 대한 action과 database 전체에 대한 action을 감사한다.

<a id="0f457303df1a2eec"></a>
#### &lt;object_action_audit&gt;

<a id="d4c0a0d530e24135"></a>
##### ALL ON object_name

object_name에 해당하는 객체에 대해 나열할 수 있는 모든 action을 의미한다.

각 객체 유형별로 감사할 수 있는 audit action은 다음 표와 같다.

**객체별 audit action**

<a id="735449713aa28d28"></a>
| Object type | Action |
| --- | --- |
| Table | ALTER, COMMENT, DELETE, GRANT, INDEX, INSERT, LOCK, RENAME, SELECT, UPDATE |
| View | ALTER, COMMENT, GRANT, SELECT |
| Sequence | ALTER, COMMENT, GRANT, SELECT |
| Stored function/  procedure | ALTER, COMMENT, EXECUTE, GRANT |

<a id="8ed0befd35668ba6"></a>
##### &lt;object_action&gt; ON object_name

특정 object에 대한 개별 action들은 다음과 같이 ON 절을 명시하여 하나씩 나열한다.

```
CREATE AUDIT POLICY p1
       ACTIONS INSERT ON u1.t1
             , DELETE ON u1.t1
             , UPDATE ON u1.t1
;
```

<a id="c176a8785d487087"></a>
##### EXECUTE action 유의 사항

Stored function이나 stored procedure의 EXECUTE action 성공, 실패 여부에 대한 감사는 실제 수행 시점의 수행 가능 여부만으로 판단한다.

- WHENEVER NOT SUCCESSFUL의 경우, stored function/ procedure를 수행할 수 없을 경우에 감사 레코드를 생성한다.
- WHENEVER SUCCESSFUL의 경우, stored function/ procedure 내부의 SQL 구문을 수행하는 중에 에러가 발생하더라도 감사 레코드를 생성한다.
- Stored function/ procedure 내부의 SQL 구문 실패에 대한 감사가 필요할 경우, 해당 SQL 구문을 감사 대상에 포함해야 한다.

<a id="8043026f80537422"></a>
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

<a id="ecba0836b6f96cca"></a>
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

<a id="f173b9af95820c53"></a>
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

<a id="05a3f83cf27117de"></a>
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

<a id="2946f40ad53718f7"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="5264030adf6e606f"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#09b3895daf4991da)
    - [DROP AUDIT POLICY](#4c985d8424a9c9e1)
    - [ALTER AUDIT POLICY](#241fd4b15c525c5a)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#8c7812c0671b6a25)
    - [NOAUDIT POLICY](#f4896aa89ec963af)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#6c787a4b953e8625)

- Audit trail 소거: [ALTER DATABASE CLEAR AUDIT TRAIL](#d0a56f6310b7a28c)

<a id="dd23e8e2eae3991d"></a>
## CREATE CLUSTER GROUP

<a id="a88fcf80fa945cb8"></a>
### 기능

Cluster system에 참여할 cluster group을 생성한다.

<a id="4fca2fc03c28fbeb"></a>
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

<a id="fc54d40d410d83cb"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;cluster group definition&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="4532c33d7052accc"></a>
### 구문 규칙 및 파라미터

<a id="c656d48e085430b1"></a>
#### group_name

Cluster group의 이름이다.   
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="8a6292259b597ac5"></a>
#### &lt;cluster member definition&gt;

Cluster group에 포함될 cluster member를 정의한다.  
Cluster group은 cluster member를 최대 32 개까지 포함할 수 있다.  
Cluster system에 최초로 생성하는 cluster group에는 cluster member를 한 개만 정의할 수 있고 자기 자신을 cluster member로 포함해야 한다.

<a id="61fd3d206207b374"></a>
#### member_name

Cluster member의 이름이다.   
Cluster member 이름은 해당 member의 database를 생성할 때 정의한 member 이름과 동일해야 한다.  
동일한 cluster group, cluster member 이름이 존재하지 않아야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

Cluster member의 start-up 단계는 GLOBAL OPEN 단계여야 한다.

<a id="f6c16de6e399dee9"></a>
#### &lt;connection attribute&gt;

Cluster member간 통신을 위한 연결 정보를 정의한다.   
&lt;connection attribute&gt;는 해당 member의 database를 생성할 때 정의한 HOST, PORT와 동일해야 한다.  
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST address는 ip v4 형식으로 사용한다. 
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="0e04f9c3041f6e59"></a>
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

<a id="8ed824cc3b51d2d5"></a>
### 설명

&lt;cluster group definition&gt; 구문은 table들의 shard를 재배치하지 않는다.

추가된 cluster group에 shard를 재배치하려면 다음 구문을 수행해야 한다.

- [ALTER DATABASE REBALANCE](#48a2899b3f507f9f)
- [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965)

<a id="7ee0860b1f22244d"></a>
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

<a id="e16472da7d3887a7"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="012772bb223fb01b"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP CLUSTER GROUP](#e491103ba644ea1a)
- [ALTER CLUSTER GROUP name ADD MEMBER](#72ed23526a0c9e3b)

<a id="c88dc891576217eb"></a>
## CREATE CLUSTER LOCATION

<a id="5bc51f554dfe0174"></a>
### 기능

Cluster member의 접속 정보를 생성한다.

<a id="f82b21d5bb5f02fb"></a>
### 구문

```
<cluster location definition> ::=
    CREATE CLUSTER LOCATION member_name 
    <cluster connection attribute>
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="0c96fb76a31c7a39"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.

&lt;cluster location definition&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="8419bd335720266d"></a>
### 구문 규칙 및 파라미터

<a id="69092e881cc937ac"></a>
#### member_name

Cluster member의 이름이다.   
등록된 cluster location 정보에 동일한 cluster member 이름이 존재하지 않아야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="fa91692a849c21c8"></a>
#### &lt;cluster connection attribute&gt;

Cluster member간 통신을 위한 연결 정보를 정의한다.   
HOST와 PORT 조합은 cluster system 내에서 유일해야 한다.

- HOST 'address'는 ip v4 형식으로 사용한다. 
- PORT port_no는 1024 ~ 49151 범위의 값이어야 한다.

<a id="fffcaf3a04c5f769"></a>
### 설명

기본적으로 cluster location 정보는 cluster group을 생성하거나 cluster member를 추가할 때 제공되는 접속 정보를 이용하여 자동으로 생성된다. 생성된 정보는 cluster member와 group을 삭제할 때 함께 삭제된다.

만약 cluster location의 접속 정보가 변경되면 cluster member를 삭제하거나 다시 생성할 필요없이 [ALTER CLUSTER LOCATION](#8193ea3b3b99d43b)을 이용하여 접속 정보를 변경할 수 있다.

<a id="c7af169040f28671"></a>
### 사용 예

```
gSQL> 
CREATE CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120,
;

Created
```

<a id="a1a847ff586628d2"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="3b8fab2b90a14f98"></a>
### 참조

관련 내용은 [DROP CLUSTER LOCATION](#8d977b885f9df018)을 참조한다.

<a id="f9d7ec4af5a3302c"></a>
## CREATE DISK DATA TABLESPACE

<a id="7cbdcf4442ee1b14"></a>
### 기능

디스크 데이터 테이블스페이스를 정의한다.

<a id="0550c7cde8f993e6"></a>
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

<a id="a489026907f3532f"></a>
### 사용 범위 및 접근 권한

&lt;disk data tablespace definition&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="b95c7f81067b8d68"></a>
### 구문 규칙 및 파라미터

<a id="1f3af180459ecfb1"></a>
#### tablespace_name

생성할 테이블스페이스의 이름이다.  
테이블스페이스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="30e2653a1cc52031"></a>
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

<a id="e3312fb1a149ee57"></a>
#### &lt;autoextend clause&gt;

자동 확장 속성을 ON 또는 OFF로 설정한다. ON으로 설정할 경우 자동 확장 크기와 데이터파일의 최대 크기를 지정할 수 있다.

<a id="4bd495176466f107"></a>
#### &lt;next size clause&gt;

현재 사용 중인 데이터 파일에 더 이상 사용할 공간이 없을 때 확장할 크기를 지정한다.

<a id="3f114e4cf3a5ce71"></a>
#### &lt;max size clause&gt;

데이터 파일이 확장될 수 있는 최대 크기를 지정한다.

<a id="87ca074880d28c7b"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (명시하지 않을 경우 bytes 단위이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="32f858f7ea55b5fb"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="d1bff9da1bea663c"></a>
#### ONLINE | OFFLINE

테이블스페이스 ONLINE/ OFFLINE 여부를 설정한다.

- ONLINE은 테이블스페이스를 생성하는 즉시 사용할 수 있는 상태이다. 
- OFFLINE은 사용 불가능한 상태이므로 ONLINE 상태로 변경한 후에 사용할 수 있다.

<a id="78891bebcafe6dfd"></a>
#### EXTSIZE &lt;size clause&gt;

테이블스페이스의 extent 크기를 지정한다.

- Extent 크기는 바이트 단위로 기술하며, 다섯 가지 (64 K, 128 K, 256 K, 512 K, 1 M) 중 하나가 선택된다.
- 만약 extent 크기가 64 K ~ 128 K 사이의 값으로 지정되면 128 K로 설정되고, 1 M 이상으로 지정되면 1 M로 설정된다.

<a id="af04614e0419f364"></a>
### 설명

Data tablespace는 table, index (LOGGING) 등의 SQL schema 객체를 저장할 물리적 공간을 제공하는 객체이다.

<a id="73c900426b1fcd32"></a>
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

<a id="7ec09cc6728f36fa"></a>
### 호환성

SQL 표준에서는 테이블스페이스에 대한 개념을 다루지 않고 있다.

<a id="1aee0f62f567d4bd"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#703c847167e78d53)
- [ALTER TABLESPACE](#bf506f295181b38d)
- [ALTER DATABASE DATAFILE AUTOEXTEND](#39b6d764690f3b61)

<a id="4b5286bf474b7abc"></a>
## CREATE GLOBAL TEMPORARY TABLE

<a id="b784ab180abb8933"></a>
### 기능

새로운 global temporary table을 생성한다.

<a id="fcb2c1525893c95c"></a>
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

> &lt;table element&gt;의 정의는 &lt;table_definition&gt;의 정의와 동일하다. 자세한 내용은 [CREATE TABLE](#9b82da6d66aabe8c) 을 참조한다.

<a id="de70eeb4a1c238bf"></a>
### 사용 범위 및 접근 권한

&lt;global temporary table definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블 생성 권한
    - [CREATE TABLE](#9b82da6d66aabe8c) 구문의 접근 권한을 참조한다.
- SELECT 접근 권한 
    - [SELECT](#93101dc44f4e210d) 구문의 접근의 권한을 참조한다.

<a id="2428d1b8ab608134"></a>
### 구문 규칙 및 파라미터

<a id="fe6a847995abbff5"></a>
#### table_name

생성할 테이블의 이름이다.  
자세한 내용은 [table_name](#8493c0c7b3751bac) 구문을 참조한다.

<a id="c8857c088158e336"></a>
#### other syntax

이 외의 구문 규칙은 [CREATE TABLE](#9b82da6d66aabe8c) 및 [CREATE TABLE AS SELECT](#9386417aa2e45722) 구문의 syntax를 참조한다.

<a id="f48ab90b8d072abd"></a>
### 설명

GLOBAL TEMPORARY TABLE은 한 트랜잭션이나 세션이 실행되는 동안 유지될 데이터를 보관하는 용도로 사용하는 임시 테이블이다.  
개발자가 응용 프로그램을 개발할 때 연산 중간 데이터를 잠시 저장하는 변수와 같은 용도로 사용된다.

Global temporary table의 특징은 다음과 같다.

- Global temporary table의 정의는 모든 세션에서 볼 수 있다.
- Global temporary table을 정의할 때는 물리적 공간이 할당되지 않고, 처음으로 insert 할 때 해당 세션에 종속된 실제 공간 (segment)이 할당된다.
- Global temporary table의 데이터는 insert 한 세션이나 트랜잭션에서만 볼 수 있다.
- Global temporary table의 데이터가 저장되는 tablespace는 다음과 같이 결정된다.

<a id="51087366659f26a2"></a>
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

<a id="1537f6965c36c6df"></a>
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

<a id="1596a67bbd96eec3"></a>
| TEMP_UNDO_ENABLED 값 | 설명 |
| --- | --- |
| TRUE | Database system의 default temporary tablespace에 undo log가 기록된다. |
| FALSE | Database system의 undo tablespace에 undo log가 기록된다. |

- Global temporary table에 대한 TRUNCATE 명령은 해당 세션의 segment만 truncate 한다.
- 세션이 종료되면 모든 segment들이 TRUNCATE 된 후에 반환된다.

<a id="dd200c7877309b86"></a>
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

<a id="b453e2bbebe6d73b"></a>
### 호환성

CREATE GLOBAL TEMPORARY TABLE 및 CREATE GLOBAL TEMPORARY TABLE AS SELECT 구문은 SQL 표준의 &lt;table definition&gt; 정의를 따른다. 단, 다음은 표준에서 확장된 것이다.

- 표준에서 SELECT 절 밖의 괄호는 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- 표준에서 WITH [NO] DATA 절은 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- GOLDILOCKS의 tablespace 개념은 표준에 없는 확장 개념이다.

**SQL 표준 호환성**

<a id="03d061c51a031dc8"></a>
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

<a id="0ed9db01631c4272"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](#9b82da6d66aabe8c)
- [CREATE TABLE AS SELECT](#9386417aa2e45722)

<a id="b117dfcc7b364512"></a>
## CREATE IMMUTABLE TABLE

<a id="c0e82e8901788ee1"></a>
### 기능

새로운 immutable table을 생성한다.

<a id="402a6c4aa62d02b3"></a>
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

> &lt;table element&gt;, &lt;table sharding strategy&gt;, &lt;table attribute clause&gt;, &lt;table global secondary index clause&gt;의 정의는 &lt;table_definition&gt;의 정의와 동일하다. 자세한 내용은 [CREATE TABLE](#9b82da6d66aabe8c)을 참조한다.

<a id="a7874203373fe987"></a>
### 사용 범위 및 접근 권한

&lt;immutable table definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블 생성 권한
    - [CREATE TABLE](#9b82da6d66aabe8c) 구문의 접근 권한을 참조한다.
- SELECT 접근 권한 
    - [SELECT](#93101dc44f4e210d) 구문의 접근 권한을 참조한다.

<a id="69cfc1b62817b676"></a>
### 구문 규칙 및 파라미터

<a id="cf819f4b68837480"></a>
#### table_name

생성할 테이블의 이름이며, 스키마 내에서 고유한 이름이어야 한다.  
schema_name.table_name과 같이 테이블이 소속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
테이블 이름의 길이는 128 바이트보다 작아야 한다.

<a id="29e645c93caa6870"></a>
#### 기타 구문 규칙

이 외의 구문 규칙은 [CREATE TABLE](#9b82da6d66aabe8c)과 [CREATE TABLE AS SELECT](#9386417aa2e45722) 구문의 syntax를 참조한다.

<a id="72f1f3292932efa0"></a>
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

<a id="2aa4e99becd00278"></a>
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

<a id="5f6e4cf6025aa0e8"></a>
### 호환성

SQL 표준에서는 CREATE IMMUTABLE TABLE 구문과 CREATE IMMUTABLE TABLE AS SELECT 구문을 다루지 않고 있다.

<a id="71387daec5f87a73"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](#9b82da6d66aabe8c)
- [CREATE TABLE AS SELECT](#9386417aa2e45722)

<a id="9d2795ea1fc7b4c6"></a>
## CREATE INDEX

<a id="ac5cda2e628271bd"></a>
### 기능

인덱스를 생성한다.

<a id="b2e9767b77205fb9"></a>
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

<a id="0bb523d3d1da9730"></a>
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

<a id="68be1fdbe40a7d1b"></a>
### 구문 규칙 및 파라미터

<a id="8ac0138328970f2f"></a>
#### UNIQUE

인덱스를 구성하는 column들에 중복 값을 허용하지 않는다.

<a id="2d8b80ae8f12419d"></a>
#### index_name

생성할 인덱스의 이름이며, 스키마 내에서 유일해야 한다.  
스키마 이름을 생략할 경우, 참조하는 테이블이 속한 스키마에 인덱스가 생성된다.  
인덱스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="d37a2bb60a40babc"></a>
#### table_name

인덱스를 생성할 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="8e1881a90fe03144"></a>
#### column_name

인덱스 key로 사용할 column의 이름이다.  
하나 이상의 column을 정의해야 하는데 최대 32 개의 column을 인덱스 key로 사용할 수 있다.

구현 내용에 따라 다음과 같은 제약이 발생할 수 있다.

- 인덱스에 포함되는 column의 데이터 타입이 LONG CHARACTER VARYING, LONG BINARY VARYING 일 경우 인덱스를 생성할 수 없다. 
- Column들의 precision 합계가 1200 바이트보다 작은 경우에만 인덱스를 생성할 수 있다.

<a id="626cb58ea83e4acc"></a>
#### ASC | DESC

Column의 정렬 순서를 명시한다.

- ASC: 오름차순으로 정렬한다. 
- DESC: 내림차순으로 정렬한다. 
- 명시하지 않을 경우, 기본값은 ASC 이다.

<a id="a144a27364652f31"></a>
#### NULLS FIRST | NULLS LAST

NULL 값의 정렬 순서를 명시한다.

- NULLS FIRST: NULL이 아닌 값들보다 앞에 위치한다. 
- NULLS LAST: NULL이 아닌 값들보다 뒤에 위치한다. 
- 명시하지 않을 경우, 기본값은 NULLS LAST 이다.

<a id="a0dd685633e3f717"></a>
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

<a id="9481ba30cdf0be9a"></a>
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

<a id="35a45cfae9e12ccc"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="f630e77c39969eba"></a>
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

<a id="24f4d7808b8ff5b7"></a>
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

<a id="5c9dcb9948cc717b"></a>
### 설명

LOGGING 인덱스와 NOLOGGING 인덱스에는 다음과 같은 trade-off가 있다.

- LOGGING 인덱스
    - 장점: 시스템을 구동할 때 로그를 이용해 인덱스가 자동으로 복구되므로 별도의 구축과정이 없다.
    - 단점: 관련 row를 변경할 때 인덱스 변경 내용을 로그로 기록하여 디스크 IO를 유발한다.
- NOLOGGING 인덱스
    - 장점: 관련 row를 변경할 때 인덱스 변경 내용에 대한 디스크 IO가 발생하지 않는다.
    - 단점: 시스템을 구동할 때 인덱스에 대한 로그 정보가 없어 자동으로 인덱스를 재구축한다.

<a id="441d948ab4543799"></a>
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

<a id="c9365068e4485aea"></a>
### 호환성

SQL 표준에서는 인덱스에 대한 개념을 다루지 않고 있다.

<a id="a43a3912fe7e2977"></a>
### 참조

관련 내용은 [DROP INDEX](#8921114ccac5a25e)를 참조한다.

<a id="e61b814a9f21f32f"></a>
## CREATE MEMORY DATA TABLESPACE

<a id="4eb0fafbdd97612c"></a>
### 기능

메모리 데이터의 테이블스페이스를 정의한다.

<a id="64b69d880d922811"></a>
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

<a id="498a02b1ac904146"></a>
### 사용 범위 및 접근 권한

&lt;memory data tablespace definition&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="f890a4ae7271c852"></a>
### 구문 규칙 및 파라미터

<a id="0e40c4e08da1b0c1"></a>
#### [ MEMORY ] [ DATA ]

테이블, 인덱스 등 영구적인 객체를 저장할 메모리 테이블스페이스이다.  
MEMORY와 DATA 예약어는 생략할 수 있다.

<a id="f3c6431b4d2c6cb6"></a>
#### tablespace_name

생성할 테이블스페이스의 이름이다.  
테이블스페이스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="00e24d278fb50c7e"></a>
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

<a id="0a64bdeb512110fc"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="7db102ae8477d7c4"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="70c2cd58af137b00"></a>
#### ONLINE | OFFLINE

테이블스페이스 ONLINE/ OFFLINE 여부를 설정한다.

- ONLINE은 테이블스페이스를 생성하는 즉시 사용할 수 있는 상태이다. 
- OFFLINE은 사용 불가능한 상태이므로 ONLINE 상태로 변경한 후에 사용할 수 있다.

<a id="e9c04f3d46ea6579"></a>
#### EXTSIZE &lt;size clause&gt;

테이블스페이스의 extent 크기를 지정한다.

- Extent 크기는 바이트 단위로 기술하며, 다섯 가지 (64 K, 128 K, 256 K, 512 K, 1 M) 중 하나가 선택된다.
- 만약 extent 크기가 64 K ~ 128 K 사이의 값으로 지정되면 128 K로 설정되고, 1 M 이상으로 지정되면 1 M로 설정된다.

<a id="b8f78e10bffb9b8c"></a>
### 설명

Data tablespace는 table, index (LOGGING) 등의 SQL schema 객체를 저장할 물리적 공간을 제공하는 객체이다.

<a id="d1e959101bef0938"></a>
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

<a id="9eb91971889ed5fc"></a>
### 호환성

SQL 표준은 테이블스페이스에 대한 개념을 다루지 않고 있다.

<a id="95bbacdc9f9587ba"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#703c847167e78d53)
- [ALTER TABLESPACE](#bf506f295181b38d)

<a id="bcdcadc8e58b6578"></a>
## CREATE MEMORY TEMPORARY TABLESPACE

<a id="5ae577577da72e9a"></a>
### 기능

메모리 임시 테이블스페이스를 정의한다.

<a id="1401742e4adb23ab"></a>
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

<a id="66d20d5b9cc0c7f9"></a>
### 사용 범위 및 접근 권한

&lt;memory temporary tablespace definition&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="41453190b6f4ba5f"></a>
### 구문 규칙 및 파라미터

<a id="495222a19e4b9d02"></a>
#### [ MEMORY ] TEMPORARY

질의 처리 과정에서 생성되는 중간 결과 등의 임시 객체나 no logging 인덱스를 저장할 메모리 임시 테이블스페이스이다.  
MEMORY 예약어는 생략할 수 있다.

<a id="e92c9bf645ebb15c"></a>
#### tablespace_name

생성할 테이블스페이스의 이름이다.  
테이블스페이스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="53e59b4ae7574a57"></a>
#### &lt;memory clause&gt;

- 'memory_name' 
    - 임시 데이터를 저장할 메모리 이름이다. 
    - memory_name은 해당 테이블스페이스 내에서 유일해야 한다. 
    - memory_name의 길이는 1024 바이트보다 작아야 한다. 
- SIZE &lt;size clause&gt; 
    - 초기 크기를 지정한다. 
    - 최소 1 M ~ 최대 30 G 까지 지정할 수 있다.

<a id="1370cb4631bc393c"></a>
#### &lt;size clause&gt;

공유 메모리 공간의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)  
임시 메모리 데이터의 경우 이미지를 파일로 관리하지 않는다.

- K: Kilobytes
- M: Megabytes
- G: Gigabytes
- T: Terabytes

<a id="6d84698fd6199788"></a>
#### &lt;domain_name&gt;

구문을 수행할 멤버나 그룹의 이름이다.  
지정하지 않은 경우에는 모든 그룹에 수행된다.

<a id="e8c2df2b5a02c5c1"></a>
#### EXTSIZE &lt;size clause&gt;

테이블스페이스의 extent 크기를 지정한다.

- Extent 크기는 바이트 단위로 기술하며, 다섯 가지 (64 K, 128 K, 256 K, 512 K, 1 M) 중 하나가 선택된다. 
- 만약 extent 크기가 64 K ~ 128 K 사이의 값으로 지정되면 128 K로 설정되고, 1 M 이상으로 지정되면 1 M로 설정된다.

<a id="35d0fe2f1612d28d"></a>
### 설명

Temporary tablespace는 index(NOLOGGING) 등의 SQL schema 객체와, 질의를 처리할 때 sorting/ hashing 하기 위한 중간 결과를 저장하는 물리적 공간을 제공하는 객체이다.

<a id="d0ecdf1eb7fd37f8"></a>
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

<a id="c4c9e7731b3abe6b"></a>
### 호환성

SQL 표준은 테이블스페이스에 대한 개념을 다루지 않고 있다.

<a id="61e5ed96af27929f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#703c847167e78d53)
- [ALTER TABLESPACE](#bf506f295181b38d)

<a id="aaba451f0d7d6289"></a>
## CREATE PROFILE

<a id="11b7eb8f5b2ef39f"></a>
### 기능

Profile을 생성하는 구문으로써 password 관리 방법을 설정할 수 있다.   
User에게 profile을 할당하면 profile에 정의된 방법으로 user의 password를 관리한다.

<a id="91fe4a22662bc995"></a>
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

<a id="d34d711cad94e106"></a>
### 사용 범위 및 접근 권한

&lt;profile definition&gt; 구문을 수행하려면 사용자에게 CREATE PROFILE ON DATABASE 권한이 있어야 한다.

<a id="ddd93fc3f70d3808"></a>
### 구문 규칙 및 파라미터

<a id="2658068b0eb50331"></a>
#### profile_name

생성할 profile의 이름을 명시한다.

<a id="929d25e8e2df05bc"></a>
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

<a id="3d98eaa909eb7e14"></a>
#### FAILED_LOGIN_ATTEMPTS

연속적인 로그인 실패 가능 횟수를 설정한다.   
명시된 횟수를 넘어서면 계정이 잠긴다.

- FAILED_LOGIN_ATTEMPTS integer
    - 값의 범위는 0보다 큰 양의 정수여야 한다. 
- FAILED_LOGIN_ATTEMPTS UNLIMITED
    - 로그인 실패로 인해 계정이 잠기지 않는다.
- FAILED_LOGIN_ATTEMPTS DEFAULT
    - "DEFAULT" profile의 정책을 따른다.

<a id="5f38683356ce92dc"></a>
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

<a id="03693bbc9eaccbe8"></a>
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

<a id="4504ea06979c3663"></a>
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

<a id="24076bd1fbdf0839"></a>
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

<a id="52ac880b5791f612"></a>
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

<a id="19f1ea0461acd25b"></a>
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

<a id="d8099360911b0dc9"></a>
##### KISA_VERIFY_FUNCTION

Korea Internet & Security Agency (KISA)의 비밀번호 검증 방법이다.

- 8 글자 이상
- 1 개 이상의 문자
- 1 개 이상의 숫자
- 1 개 이상의 특수 문자

<a id="22db0deb19b477f9"></a>
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

<a id="f3d0a6bad097d16d"></a>
##### ORA12C_STRONG_VERIFY_FUNCTION

Oracle의 ORA12C_STRONG_VERIFY_FUNCTION 비밀번호 검증 방법이다.

- 9 글자 이상
- 2 개 이상의 대문자 
- 2 개 이상의 소문자 
- 2 개 이상의 숫자 
- 2 개 이상의 특수 문자 
- 이전 비밀번호와 적어도 4 글자는 달라야 한다.

<a id="29b5ae17f2a53f2c"></a>
##### VERIFY_FUNCTION_11G

Oracle의 VERIFY_FUNCTION_11G 비밀번호 검증 방법이다.

- 8 글자 이상
- 1 개 이상의 문자 
- 1 개 이상의 숫자 
- 사용자 이름을 포함하면 안된다. 
- 이전 비밀번호와 적어도 3 글자는 달라야 한다.

<a id="f26680610c57ebee"></a>
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

<a id="6600409ffe02f29d"></a>
### 설명

<a id="e97b20a3f3eb9df6"></a>
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

<a id="93d6f4c4c6e36863"></a>
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

<a id="92413727f36ed7d6"></a>
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

<a id="1ad6bc309292ba0a"></a>
#### 비밀번호 재사용 가능 여부

비밀번호 재사용 가능 여부에 영향을 주는 parameter는 다음과 같다.

- PASSWORD_REUSE_MAX
- PASSWORD_REUSE_TIME

두 parameter의 비밀번호 재사용 가능 여부는 다음 표와 같다.

**비밀번호 재사용 가능 조건**

<a id="27ed2c9f14d4b8d2"></a>
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

<a id="fc1dbf44be5b4b36"></a>
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

<a id="1856a33f47d84d43"></a>
#### DEFAULT profile

Database를 생성할 때 다음과 같은 "DEFAULT" profile을 자동으로 생성한다. 생성하는 "DEFAULT" profile 의 password parameter 정보는 다음과 같다.

**DEFAULT profile의 구성**

<a id="66fb4c14efaa706d"></a>
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

<a id="4dea300a5485289a"></a>
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

<a id="d501de8342c12de1"></a>
### 호환성

SQL 표준은 profile에 대한 개념을 다루지 않고 있다.

<a id="c3b632a7fb430079"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP PROFILE](#317a2852ef6da864)
- [ALTER PROFILE](#707c01f0b15f9ab0)
- [CREATE USER](#8e5920c927752802)
- [ALTER USER](#268a4621fc85878c)
- [ALTER DATABASE CLEAR PASSWORD HISTORY](#23aa4348abd416d5)

<a id="587f9a1c3687c699"></a>
## CREATE SCHEMA

<a id="cf4a68ce080562ad"></a>
### 기능

스키마를 정의한다.

<a id="50f81af7be5afa45"></a>
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

<a id="1f598bf451e39a9f"></a>
### 사용 범위 및 접근 권한

&lt;schema definition&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 스키마를 생성하려면 CREATE SCHEMA ON DATABASE 권한이 있어야 한다.

- &lt;schema element&gt;가 존재할 경우, 각 &lt;schema element&gt; 구문을 수행하기 위한 권한이 있어야 한다.  
  자세한 내용은 다음 각 구문의 *사용 범위 및 접근 권한*을 참조한다.
    - [CREATE TABLE](#9b82da6d66aabe8c) 
    - [CREATE VIEW](#a71e7cc52f1eefb4) 
    - [CREATE INDEX](#9d2795ea1fc7b4c6)
    - [CREATE SEQUENCE](#2eb16f80ff00b702)
    - [GRANT privileges TO](#81c5198ff0096dcc)
    - [COMMENT ON name IS](#9dee57a337c9ae81)

- user_identifier에 해당하는 사용자는 생성한 스키마에 대해 다음과 같은 권한을 갖는다.
    - 생성한 schema_name 스키마의 소유자 
    - &lt;schema element&gt; 절로 생성된 객체의 소유자

- 생성한 스키마에 별도의 권한을 부여하지 않으므로 객체를 생성하려면 적절한 스키마 권한을 부여받아야 한다.  
  스키마 권한의 종류에 대한 내용은 GRANT privileges TO 구문의 [&lt;schema privilege&gt;](#a966ecd031ab1081)를 참조한다.  
  사용 예는 CREATE USER 구문의 [사용 예](#36e07080c1971324)를 참조한다.

<a id="0360281fbe9e37a8"></a>
### 구문 규칙 및 파라미터

<a id="1c5f741b8ebc21d1"></a>
#### schema_name

생성할 스키마의 이름이다.  
Database 내에 동일한 스키마 이름이 존재하지 않아야 한다.  
스키마 이름의 길이는 128 바이트보다 작아야 한다.

<a id="4f781a1f754c27b9"></a>
#### AUTHORIZATION user_identifier

스키마 이름을 생략할 경우, user_identifier와 동일한 이름의 스키마를 생성한다.   
AUTHORIZATION을 지정하지 않을 경우, 구문을 수행한 사용자의 user_identifier가 사용된다.

<a id="65fde8dc0332d058"></a>
#### schema_name AUTHORIZATION user_identifier

생성할 스키마 이름과 스키마의 소유자를 지정한다.   
소유자는 role이나 PUBLIC이 될 수 없다.

<a id="d2a88204b3e8b75c"></a>
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

<a id="53a7eb1b57914c91"></a>
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

<a id="d1fdb5c14e8d57c4"></a>
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

<a id="6c236ad5f5600926"></a>
### 호환성

**SQL 표준 호환성**

<a id="f37852e84c996fa2"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| S071 | SQL paths in function and type name resolution | X |
| F461 | Named character sets | X |
| F171 | Multiple schemas per user | O |
| T332 | Extended roles | X |

<a id="ab2a8cbd517af7dc"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP SCHEMA](#1197651d9b38835b)
- [CREATE USER](#8e5920c927752802)
- [CREATE TABLE](#9b82da6d66aabe8c)
- [CREATE VIEW](#a71e7cc52f1eefb4)
- [CREATE INDEX](#9d2795ea1fc7b4c6)
- [CREATE SEQUENCE](#2eb16f80ff00b702)
- [GRANT privileges TO](#81c5198ff0096dcc)
- [COMMENT ON name IS](#9dee57a337c9ae81)

<a id="2eb16f80ff00b702"></a>
## CREATE SEQUENCE

<a id="37d86ea17616938d"></a>
### 기능

시퀀스를 생성한다.

<a id="cd454e5f814bf921"></a>
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

<a id="e000485bb47eef5b"></a>
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

<a id="6ced74f302e03a5b"></a>
### 구문 규칙 및 파라미터

<a id="9f49e651bfddfadb"></a>
#### sequence_name

생성할 시퀀스의 이름이며 스키마 내에서 유일한 이름이어야 한다.  
schema_name.sequence_name과 같이 시퀀스가 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
시퀀스 이름의 길이는 128 바이트보다 작아야 한다.

<a id="edb9476776440d10"></a>
#### &lt;sequence generator option&gt;

&lt;sequence generator option&gt;을 사용하지 않을 경우 다음 두 문장은 같은 의미를 갖는다.

- CREATE SEQUENCE test_seq; 
- CREATE SEQUENCE test_seq START WITH 1 INCREMENT BY 1 NO MINVALUE NO MAXVALUE NO CYCLE CACHE 20;

<a id="795b2fe20870d587"></a>
#### &lt;sequence generator start with option&gt;

첫 번째로 생성할 시퀀스 번호를 정의한다.   
오름차순인지 내림차순인지에 따라 다음과 같은 특징을 갖는다.

- 오름차순 시퀀스일 경우 (INCREMENT BY 양수) 
    - 최소값보다 큰 시퀀스 값으로 시작하고자 할 경우에 사용한다. 
    - START WITH 절을 생략할 경우, 기본값은 최소값 (MINVALUE value)이 된다. 
- 내림차순 시퀀스일 경우 (INCREMENT BY 음수) 
    - 최대값보다 작은 시퀀스 값으로 시작하고자 할 경우에 사용한다. 
    - START WITH 절을 생략할 경우, 기본값은 최대값 (MAXVALUE value)이 된다.

<a id="ff9a4be1f93f86af"></a>
#### &lt;sequence generator increment by option&gt;

시퀀스 번호의 간격을 정의한다.   
다음과 같은 제약 및 특징을 갖는다.

- 양수 또는 음수를 사용할 수 있으며, 0은 사용할 수 없다. 
- 간격의 절대값은 MINVALUE와 MAXVALUE의 차이보다 작아야 한다. 
- 양수일 경우 오름차순 시퀀스가 생성되며 음수일 경우 내림차순 시퀀스가 생성된다. 
- INCREMENT BY 절을 생략할 경우, 기본값은 양수 1 이다.

<a id="839225aed9813aae"></a>
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

<a id="387f702360316375"></a>
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

<a id="6629b78a38ba7f4e"></a>
#### &lt;sequence generator cycle option&gt;

시퀀스의 값이 최대값 또는 최소값이 되었을 때, 계속 값을 생성할지 여부를 명시한다.

- CYCLE 
    - 오름차순 시퀀스가 최대값이 되었을 때, 최소값부터 다시 생성한다. 
    - 내림차순 시퀀스가 최소값이 되었을 때, 최대값부터 다시 생성한다. 
- NO CYCLE | NOCYCLE 
    - 최대값 또는 최소값이 되었을 때, 시퀀스 값을 생성할 수 없다. 
    - NO CYCLE (SQL 표준) 과 NOCYCLE 은 동일한 의미의 예약어로 어떤 것을 사용해도 무방하다. 
- CYCLE과 NO CYCLE을 명시하지 않을 경우, 기본값은 NO CYCLE 이다.

<a id="551673524c6d3072"></a>
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

<a id="36fe154eaf7add90"></a>
### 설명

생성한 시퀀스 객체의 시퀀스 값은 [NEXTVAL](17-built-in-function-references.md#c73afcf37cccda71) 함수와 [CURRVAL](17-built-in-function-references.md#6b00b628498e23d6) 함수를 이용하여 사용할 수 있다.

시퀀스 값은 트랜잭션 속성을 가지지 않으며, 시퀀스 함수를 사용한 SQL 구문에서 에러가 발생하거나 명시적인 ROLLBACK을 수행하더라도 시퀀스 값은 가장 최신 값을 유지한다.

CURRVAL 함수의 경우, session에서 가장 최근에 호출한 NEXTVAL 값을 반환한다.   
이러한 특성을 이용하면 NEXTVAL을 이용하여 한 번 얻은 시퀀스 값을 다른 SQL 문장에 계속 사용할 수 있다.  단, session에서 NEXTVAL을 호출하지 않은 경우에 CURRVAL를 사용하면 에러가 발생한다.

<a id="855730e01fb455a1"></a>
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

<a id="71ce1e16b6209e47"></a>
### 호환성

SQL 표준에서는 &lt;sequence generator cache option&gt; 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="8ac4a57297b65ff2"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="4a3e8f85a3ecbeda"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP SEQUENCE](#8c2068e78d2e75d6)
- [ALTER SEQUENCE](#ebac80e511ac5859)
- [NEXTVAL](17-built-in-function-references.md#c73afcf37cccda71)
- [CURRVAL](17-built-in-function-references.md#6b00b628498e23d6)

<a id="f32eb8a1d0dbc720"></a>
## CREATE SYNONYM

<a id="c1ae1b279e64b256"></a>
### 기능

Synonym을 생성한다. Synonym은 테이블, view, 시퀀스, 또다른 synonym의 대체 이름으로써 이들 대신 다음 구문에서 사용될 수 있다.

- DML: SELECT, INSERT, UPDATE, DELETE, LOCK TABLE, CALL
- DDL: GRANT, REVOKE, COMMENT

<a id="ca48b7c9fae694c3"></a>
### 구문

```
<synonym definition> ::=    
    CREATE [OR REPLACE] [PUBLIC] SYNONYM [schema_name.]synonym_name 
    FOR [schema_name.]object_name
    ;
```

<a id="e71ea3c5ac4ba0f0"></a>
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

<a id="14675dcff5c07db5"></a>
### 구문 규칙 및 파라미터

<a id="75289b2329e73cbf"></a>
#### [ OR REPLACE ]

이미 synonym이 존재할 경우, 기존의 synonym을 대체한다.

<a id="b6ed7ae7a6fe956e"></a>
#### [ PUBLIC ]

Public synonym을 만들기 위해 명시한다.   
이 절을 생략하면 private synonym이 생성된다.

<a id="435647ecc5e230f9"></a>
#### synonym_name

생성할 synonym의 이름이며, 스키마 내에서 유일한 이름이어야 한다.   
schema_name.synonym_name과 같이 synonym이 소속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
Synonym 이름의 길이는 128 바이트보다 작아야 한다.   
Public synonym은 non-schema 객체이다. 따라서 PUBLIC을 명시하여 public synonym을 생성할 때는 스키마 이름을 명시할 수 없다.

<a id="6c9eba152859c2c1"></a>
#### object_name

schema_name.object_name과 같이 객체가 소속된 스키마를 명시할 수 있으며, schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

object_name을 명시할 수 있는 객체 타입은 다음과 같다.

- Table
- View
- Sequence
- 또 다른 synonym

대상 객체의 존재 여부, cycle check, 권한 검사 등은 synonym을 사용한 구문을 수행할 때 실행된다.

<a id="9342a861cb40ff93"></a>
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

<a id="402272f8e82b30fc"></a>
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

<a id="ad45503e0a9a33b9"></a>
### 호환성

SQL 표준에서는 CREATE SYNONYM 구문을 정의하지 않고 있다.

<a id="2f152aa4b93f2153"></a>
### 참조

관련 내용은 [DROP SYNONYM](#c4938ba3825fd271)을 참조한다.

<a id="9b82da6d66aabe8c"></a>
## CREATE TABLE

<a id="977236c7505435cb"></a>
### 기능

테이블을 정의한다.

<a id="c0d9e475e41ba609"></a>
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

<a id="10b496ed224b9b9a"></a>
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

<a id="ae360c3f73e16b17"></a>
### 구문 규칙 및 파라미터

<a id="8493c0c7b3751bac"></a>
#### table_name

생성할 테이블의 이름이며, 스키마 내에서 유일한 이름이어야 한다.   
schema_name.table_name과 같이 테이블이 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
테이블 이름의 길이는 128 바이트보다 작아야 한다.

<a id="2540b5ecf509674a"></a>
#### &lt;column definition&gt;

테이블을 구성할 column을 정의한다.   
테이블은 하나 이상의 column에 대한 정의를 포함해야 한다.   
Column의 데이터 타입, 기본값, 자동 생성 값, 제약 조건 등을 기술할 수 있다.

<a id="6765335dfc69a9ea"></a>
#### column_name

테이블을 구성할 column의 이름으로 각 column은 테이블 내에서 유일한 이름을 가져야 한다.   
Column 이름의 길이는 128 바이트보다 작아야 한다.

<a id="16d8c42d61d5620a"></a>
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
데이터 타입과 관련한 자세한 내용은 [Data Type](11-sql-elements.md#2ec7b2e6f23b520c) 정의를 참조한다.

<a id="70cbba64cceae632"></a>
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

<a id="2a83fda9b0a0f04e"></a>
#### [ &lt;default clause&gt; | &lt;identity column specification&gt; ]

Column의 기본값을 명시한다.   
&lt;default clause&gt;와 &lt;identity column specification&gt;은 함께 사용할 수 없다.   
모두 생략할 경우, 기본값은 NULL이다.

<a id="c7016df1b3063520"></a>
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

<a id="550e853cb83ff15c"></a>
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

identity column 생성 옵션인 &lt;common sequence generator option&gt;과 &lt;basic sequence generator option&gt;에 대한 자세한 내용은 [CREATE SEQUENCE](#2eb16f80ff00b702) 구문을 참조한다.

<a id="f7cf5c1d6d364623"></a>
#### &lt;column constraint definition&gt;

Column에 대해 다음과 같은 제약 조건을 정의한다.

- NOT NULL 제약 조건 
- UNIQUE 제약 조건 
- PRIMARY KEY 제약 조건

<a id="b9362dff55f8d462"></a>
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

<a id="16937ab8a01e3033"></a>
#### NOT NULL 제약 조건

Column 값으로 NULL 값을 허용하지 않는다.

<a id="d9dcfa6e32ad4a86"></a>
#### UNIQUE 제약 조건

Column 값으로 동일한 값을 허용하지 않는다.   
단, NULL 값은 허용한다.

<a id="34d2aa846dcf32a4"></a>
#### PRIMARY KEY 제약 조건

Column 값으로 NULL 값이나 동일한 값을 허용하지 않는다.   
하나의 테이블에 하나의 PRIMARY KEY 제약 조건을 정의할 수 있다.

<a id="fb043e6b9a778eda"></a>
#### &lt;index name clause&gt;

UNIQUE 제약 조건, PRIMARY KEY 제약 조건을 정의할 때 생성되는 인덱스의 이름을 정의한다.

- INDEX index_name 
    - 제약 조건을 위한 인덱스의 이름을 정의한다. 
    - 스키마 이름과 함께 사용할 수 없으며, 제약 조건과 동일한 스키마에 생성된다.

UNIQUE 제약 조건, PRIMARY KEY 제약 조건을 정의할 때 INDEX 절을 생략할 경우에는 제약 조건에 부합하는 인덱스를 자동으로 생성한다.  
자동 생성되는 인덱스 이름으로는 "constraint_name" + "_INDEX"가 부여된다.

- &lt;index attributes&gt; 
    - 생성할 인덱스의 물리적 속성을 지정한다. 
    - 자세한 내용은 [CREATE INDEX](#9d2795ea1fc7b4c6) 구문을 참조한다. 
- TABLESPACE index_tablespace_name 
    - 인덱스를 생성할 tablespace 를 지정한다. 
    - 자세한 내용은 [CREATE INDEX](#9d2795ea1fc7b4c6) 을 참조한다.

<a id="60ba581d44970aee"></a>
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

<a id="28b3e93903bb1438"></a>
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

<a id="1361844dbaa1d259"></a>
#### &lt;table sharding strategy&gt;

테이블의 sharding 정책을 정의한다.   
다음과 같은 네 가지 정책 중 하나로 정의할 수 있다.

- &lt;cloned strategy&gt; 
- &lt;hash sharding strategy&gt; 
- &lt;range sharding strategy&gt; 
- &lt;list sharding strategy&gt;

생략할 경우 [DEFAULT_SHARDING](../part-02-administration-manual/10-server-property.md#e144387380cfccfa) 프로퍼티 값에 의해 결정된다.

- DEFAULT_SHARDING 값이 0 인 경우
    - &lt;cloned strategy&gt;
- DEFAULT_SHARDING 값이 1 인 경우
    - &lt;hash sharding strategy&gt;

<a id="702361e16a87b63d"></a>
#### &lt;cloned strategy&gt;

테이블의 모든 data를 복제한다.

<a id="6467970e843ee453"></a>
#### &lt;clone placement&gt;

Clone의 배치 정책을 정의한다.

- AT CLUSTER WIDE 
    - Cluster system의 모든 cluster group의 모든 cluster member에 clone을 배치한다. 
    - Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965) 구문을 사용하여 clone을 재배치할 수 있다. 
- AT CLUSTER GROUP group_list 
    - 지정한 cluster group들의 모든 cluster member에 clone을 배치한다. 
    - 지정된 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965) 구문을 사용하여 clone을 재배치할 수 있다. 
    - Cluster group 추가는 clone의 재배치에 영향을 주지 않는다.
- 생략할 경우, 기본값은 AT CLUSTER WIDE이다.

<a id="12930426f7bdf4aa"></a>
#### &lt;hash sharding strategy&gt;

테이블의 data를 sharding key의 hash 값을 기준으로 shard를 분할한다.

<a id="48130d38eb44c02a"></a>
#### SHARDING BY [HASH] ( column_list )

Hash sharding을 위한 sharding key를 정의한다.

- Column을 32 개까지 나열할 수 있다. 
- 동일한 column은 사용할 수 없다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column은 사용할 수 없다.

<a id="737e8e25dfcc4434"></a>
#### &lt;hash shard count&gt;

분할할 hash shard의 개수를 정의한다.   
Shard의 개수는 1부터 512까지 정의할 수 있다.   
생략할 경우 기본값은 24이다.

<a id="b99221280831efc2"></a>
#### &lt;hash shard placement&gt;

Hash shard의 배치 정책을 정의한다.

- AT CLUSTER WIDE 
    - Cluster system의 모든 cluster group의 모든 cluster member에 shard 들을 배치한다. 
    - Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965) 구문을 사용하여 shard들을 재배치할 수 있다. 
- AT CLUSTER GROUP group_list 
    - 지정한 cluster group들의 모든 cluster member에 hash shard들을 배치한다. 
    - group_list의 개수는 &lt;hash shard count&gt;의 값과 같거나 작아야 한다. 
    - range shard, list shard와 달리 hash shard는 특정 shard가 배치될 cluster group을 지정할 수 없으며, system이 자동으로 shard 들을 배치할 cluster group을 결정한다. 
    - 지정한 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965) 구문을 사용하여 shard를 재배치할 수 있다. 
    - Cluster group 추가는 hash shard의 재배치에 영향을 주지 않는다.
- 생략할 경우, 기본값은 AT CLUSTER WIDE 이다.

<a id="8dc9063931f6e129"></a>
#### &lt;range sharding strategy&gt;

테이블의 data를 sharding key의 범위값을 기준으로 shard 분할한다.

<a id="09ec1f20147dd1d7"></a>
#### SHARDING BY RANGE ( column_list )

Range sharding을 위한 sharding key를 정의한다.

- Column을 32 개까지 나열할 수 있다. 
- 동일한 column은 사용할 수 없다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column은 사용할 수 없다.

<a id="fc7e5fcde2e1b20f"></a>
#### &lt;cluster-wide range shard placement&gt;

Range shard들을 cluster system의 모든 cluster group으로 자동으로 배치한다.  
&lt;range shard definition&gt;을 기술하기 전에 AT CLUSTER WIDE 구문을 기술한다.  
Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.

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

<a id="3f107aaf65a2b6b0"></a>
#### &lt;group-specific range shard placement&gt;

Range shard들을 지정한 cluster group에 배치한다.  
&lt;range shard definition&gt;과 함께 해당 shard를 배치할 AT CLUSTER GROUP group_name 구문을 기술한다.  
지정한 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.  
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

<a id="8825d826cf0bb19a"></a>
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

<a id="063189db4b99848b"></a>
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

<a id="1f72adcb0062f4aa"></a>
#### &lt;list sharding strategy&gt;

테이블의 data를 sharding key 의 나열값을 기준으로 shard를 분할한다.

<a id="192724de29c63884"></a>
#### SHARDING BY LIST ( column_name )

List sharding을 위한 sharding key를 정의한다.

- 하나의 column만 사용할 수 있다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column을 사용할 수 없다.

<a id="10add02209df7fb5"></a>
#### &lt;cluster-wide list shard placement&gt;

Cluster system의 모든 cluster group에 list shard들을 자동으로 배치한다.  
&lt;list shard definition&gt;을 기술하기 전에 AT CLUSTER WIDE 구문을 기술한다.  
Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.

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

<a id="f1095a843b97c1f3"></a>
#### &lt;group-specific list shard placement&gt;

List shard들을 지정한 cluster group에 배치한다.  
&lt;list shard definition&gt;과 함께 해당 shard를 배치할 AT CLUSTER GROUP group_name 구문을 기술한다.  
지정한 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](#1c3e42a41b2d2965) 구문을 사용하여 자동으로 shard들을 재배치할 수 있다.  
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

<a id="0c3923e6a04584c6"></a>
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

<a id="c5f6e80d423e5378"></a>
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

<a id="bba3a2da997925a8"></a>
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

<a id="1971accdf6471c31"></a>
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

<a id="9d5c6e9d942ee185"></a>
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

<a id="7477c885f79948fe"></a>
#### &lt;size clause&gt;

파일의 바이트 크기를 명시한다. (단위를 기술하지 않을 경우 bytes이다.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="ce86dc6d83dea9b6"></a>
#### TABLESPACE tablespace_name

테이블이 저장될 tablespace의 이름을 지정한다.   
TABLESPACE 절을 생략할 경우, 구문을 수행하는 사용자의 기본 tablespace_name을 사용한다.

<a id="8e148767d94f541a"></a>
#### TABLESPACE index_tablespace_name

인덱스가 저장될 tablespace의 이름을 지정한다.   
TABLESPACE 절을 생략할 경우, 사용자의 인덱스 테이블스페이스를 사용한다.  
사용자의 인덱스 테이블스페이스가 NULL인 경우, DISK 테이블은 사용자의 데이터 테이블스페이스를 사용하고 MEMORY 테이블은 사용자의 기본 임시 테이블스페이스를 사용한다.

<a id="93e3b02b5f956aa1"></a>
#### &lt;constraint characteristics&gt;

제약 조건의 특성을 정의한다.   
제약 조건을 정의할 때 다음과 같은 특성들을 설정할 수 있다.

- 제약 조건의 지연가능성 ( DEFERRABLE | NOT DEFERRABLE )
- 제약 조건의 검사시점 ( &lt;constraint check time&gt; )

&lt;constraint characteristics&gt;를 생략할 경우, NOT DEFERRABLE INITIALLY IMMEDIATE로 설정한다.

<a id="0b01696aa05aa192"></a>
#### DEFERRABLE | NOT DEFERRABLE

제약 조건을 DML을 수행할 때 검사하지 않고, COMMIT을 수행할 때 검사할 수 있게 지연시킬 수 있는지 여부를 설정한다.

지연 가능한 제약 조건의 검사시점은 [SET CONSTRAINTS](#0ec9d72169df1ed8) 구문으로 제어한다.

- NOT DEFERRABLE
    - 검사 시점을 지연시킬 수 없으며, INSERT, DELETE, UPDATE 구문을 수행할 때 제약 조건을 검사한다.
- DEFERRABLE
    - 검사 시점을 [SET CONSTRAINTS](#0ec9d72169df1ed8) 구문으로 제어할 수 있다.
    - SET CONSTRAINTS constraint_name IMMEDIATE
        - DML을 수행할 때 제약 조건을 검사한다.
    - SET CONSTRAINTS constraint_name DEFERRED
        - COMMIT을 수행할 때 제약 조건을 검사한다.
- 명시하지 않을 경우 기본값은 &lt;constraint check time&gt;에 따라 결정된다.
    - INITIALLY IMMEDIATE를 명시한 경우, NOT DEFERRABLE 이다.
    - INITIALLY DEFERRED를 명시한 경우, DEFERRABLE 이다.
    - &lt;constraint check time&gt;을 명시하지 않은 경우, NOT DEFERRABLE 이다.

<a id="3d8fb1d22498cbfa"></a>
#### &lt;constraint check time&gt;

지연가능한 (DEFERRABLE) 제약 조건일 경우, 검사 시점의 초기값을 설정한다.

- INITIALLY IMMEDIATE
    - DML을 수행할 때 제약 조건을 검사한다.
- INITIALLY DEFERRED
    - COMMIT을 수행할 때 제약 조건을 검사한다.
    - NOT DEFERRABLE과 함께 사용할 수 없다.
- 명시하지 않을 경우, 기본값은 INITIALLY IMMEDIATE 이다.

지연 가능한 제약 조건에 대한 자세한 내용은 [SET CONSTRAINTS](#0ec9d72169df1ed8) 구문을 참조한다.

<a id="60dd9b464b7e21e3"></a>
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

<a id="a1a36877d229ab26"></a>
### 설명

<a id="f5da3d48b2b70c80"></a>
#### 제약 조건의 특성

GOLDILOCKS는 key 제약 조건을 생성할 때 uniqueness 검사를 하기 위해 자동으로 index를 생성한다.

다음과 같은 column은 NULL 값을 허용하지 않는다.

- NOT NULL 제약 조건이 있는 column
- Primary key 제약 조건에 포함되는 column
- Identity column

<a id="d5e88092b85b593b"></a>
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

<a id="c901069120fca50f"></a>
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

<a id="deaa1ea7751cc730"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- TABLESPACE 절, &lt;physical attribute clause&gt; 절 등의 물리적 개념
- SQL 표준은 DEFAULT 절에 연산을 사용할 수 없다.

**SQL 표준 호환성**

<a id="0bff09c2b6e1c596"></a>
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

<a id="25387e43b551a1c1"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLE](#2481c7252f63dc1c)
- [ALTER TABLE](#79ce4cebdf753797)
- [CREATE TABLESPACE](#53b7fdb5c5a23059)
- [CREATE SCHEMA](#587f9a1c3687c699)
- [CREATE INDEX](#9d2795ea1fc7b4c6)
- [CREATE SEQUENCE](#2eb16f80ff00b702)
- [SET CONSTRAINTS](#0ec9d72169df1ed8)
- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#c41a3550730b3ad2)

<a id="9386417aa2e45722"></a>
## CREATE TABLE AS SELECT

<a id="b18770cde84152e0"></a>
### 기능

질의 결과로부터 새로운 테이블을 생성한다.

<a id="0e35b3cfefd1b743"></a>
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

<a id="063da0a81bb98c90"></a>
### 사용 범위 및 접근 권한

&lt;table definition:AS query expression&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 테이블 생성 권한
    - [CREATE TABLE](#9b82da6d66aabe8c) 구문의 접근 권한을 참조한다.
- SELECT 접근 권한 
    - [SELECT](#93101dc44f4e210d) 구문의 접근 권한을 참조한다.

<a id="422bbb9144976f49"></a>
### 구문 규칙 및 파라미터

<a id="536a80f2ecd2c131"></a>
#### table_name

생성할 테이블의 이름이다.  
자세한 내용은 [table_name](#8493c0c7b3751bac) 구문을 참조한다.

<a id="a97db5f5b0c1c803"></a>
#### column_name_list

테이블을 구성할 column의 이름으로써 테이블 내에서 유일한 이름이어야 하며, column의 개수는 SELECT 절의 결과 column 개수와 동일해야 한다.   
명시하지 않을 경우, &lt;query expression&gt;의 SELECT 절의 column 이름을 사용한다.

단, SELECT절에 column이 아닌 expression (function, operation, subquery 등)이 오면 alias 또는 column name을 명시해야 한다.

Column 이름의 길이는 128 바이트보다 작아야 한다.

<a id="e3c6dbbb0c111f08"></a>
#### WITH [NO] DATA

WITH DATA가 명시된 경우, SELECT 절의 결과가 생성될 테이블에 INSERT 된다.    
WITH NO DATA가 명시된 경우, SELECT 절의 결과가 생성될 테이블에 INSERT 되지 않는다.    
명시하지 않을 경우, WITH DATA를 명시한 것과 동일하게 작동한다.

<a id="c17c856deb2832d0"></a>
#### other syntax

이 외의 구문 규칙은 [CREATE TABLE](#9b82da6d66aabe8c) 구문의 syntax를 참조한다.

<a id="8591a7e65ac49051"></a>
### 설명

CREATE TABLE AS SELECT 구문을 수행할 때 SELECT list에 NOT NULL 제약 조건이 있는 column이 명시된 경우, 새로운 테이블에도 NOT NULL 제약 조건이 생성된다.  단, 지연 가능한 NOT NULL 제약 조건인 경우, 새로운 테이블에는 NOT NULL 제약 조건을 생성하지 않는다.

그러나 명시적으로 NOT NULL 제약 조건을 생성한 것이 아니라, primary key, identity column과 같이 NOT NULL 속성을 가지고 있는 경우에는 새로운 테이블에 NOT NULL 제약 조건을 생성하지 않는다.

<a id="4586a894f6782389"></a>
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

<a id="c8dd5cd1efc9f1ba"></a>
### 호환성

CREATE TABLE AS SELECT 구문은 SQL 표준을 따른다. 단, 다음은 표준에서 확장된 것이다.

- 표준에서 SELECT 절 밖의 괄호는 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- 표준에서 WITH [NO] DATA 절은 필수이다. 그러나 GOLDILOCKS에서는 선택 사항이다.
- GOLDILOCKS의 tablespace 개념은 표준에 없는 확장 개념이다.

**SQL 표준 호환성**

<a id="92f3ee74973cc269"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T172 | AS subquery clause in table definition | O |

<a id="9650784f9a2698c5"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE TABLE](#9b82da6d66aabe8c)
- [SELECT](#93101dc44f4e210d)

<a id="53b7fdb5c5a23059"></a>
## CREATE TABLESPACE

<a id="327be11c917648a4"></a>
### 기능

테이블스페이스를 생성한다.

<a id="e53ed3643c73e623"></a>
### 구문

```
<create tablespace statement> ::=
      <memory data tablespace statement>
    | <memory temporary tablespace statement>
    ;
```

<a id="3c3568fd03cae710"></a>
### 사용 범위 및 접근 권한

&lt;create tablespace statement&gt; 구문을 수행하려면 사용자에게 CREATE TABLESPACE ON DATABASE 권한이 있어야 한다.

구문을 수행한 사용자는 생성한 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 권한을 갖는다.

생성한 테이블스페이스에 객체를 생성하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블스페이스에 대해 CREATE OBJECT ON TABLESPACE 
- USAGE TABLESPACE ON DATABASE

<a id="cd4f4299604d9503"></a>
### 구문 규칙 및 파라미터

<a id="596cd88f62cd36fe"></a>
#### &lt;memory data tablespace statement&gt;

- [ MEMORY ] TEMPORARY

질의 처리 과정에서 생성되는 중간 결과 등의 임시 객체나 no logging 인덱스를 저장할 메모리 임시 테이블스페이스이다.  
MEMORY 예약어는 생략할 수 있다.

<a id="1ec33728568c2a3c"></a>
#### &lt;memory data tablespace clause&gt;

메모리 데이터의 테이블스페이스를 정의한다.  
자세한 내용은 [CREATE MEMORY DATA TABLESPACE](#e61b814a9f21f32f) 구문을 참조한다.

<a id="369849280443a4c0"></a>
#### &lt;memory temporary tablespace definition&gt;

메모리의 임시 테이블스페이스를 정의한다.  
자세한 내용은 [CREATE MEMORY TEMPORARY TABLESPACE](#bcdcadc8e58b6578) 구문을 참조한다.

<a id="b206900d21c89fd1"></a>
### 설명

각 세부 구문의 설명을 참조한다.

<a id="81b5b6c851924ade"></a>
### 사용 예

각 세부 구문의 사용 예를 참조한다.

<a id="8d14a31ba0eb9eae"></a>
### 호환성

SQL 표준은 tablespace에 대한 개념을 다루지 않고 있다.

<a id="456ff42f8c91e7d0"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP TABLESPACE](#703c847167e78d53)
- [ALTER TABLESPACE](#bf506f295181b38d)

<a id="8e5920c927752802"></a>
## CREATE USER

<a id="e08cf1655d225059"></a>
### 기능

데이터베이스 사용자를 정의한다.

<a id="9633a8b6f9c7da44"></a>
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

<a id="6b22afbef04dc14b"></a>
### 사용 범위 및 접근 권한

&lt;user definition&gt; 구문을 수행하려면 사용자에게 CREATE USER ON DATABASE 권한이 있어야 한다.

생성한 user_identifier 사용자는 &lt;schema clause&gt;로 생성한 스키마의 소유자라는 권한을 갖는다.

> 생성된 user_identifier에는 별도의 권한이 부여되지 않는다.  
> user_identifier 사용자가 접속해서 SQL 구문을 수행하려면 적절한 권한을 부여받아야 한다.

<a id="a0071e17052109c3"></a>
### 구문 규칙 및 파라미터

<a id="5598641d3925c130"></a>
#### user_identifier

생성할 user의 이름이다.  
동일한 사용자 이름 (user_identifier)이나 역할 이름 (role_name)이 존재하지 않아야 한다.  
user_identifier의 길이는 128 byte 보다 작아야 한다.

<a id="05edfce1d799d5b7"></a>
#### password

생성할 user의 password로써 암호화되어 저장된다.  
password의 길이는 128 byte보다 작아야 한다.  
password는 대소문자를 구별한다.  
password는 영문자로 시작해야 하고 영문자, 숫자, underscore(_), $를 포함할 수 있다.  
그 외의 특수문자를 사용하려면 double-quotation (")으로 묶어야 한다.

<a id="32b94ce8c8b933a4"></a>
#### PROFILE { profile_name | DEFAULT | NULL }

비밀번호 관리 정책을 위한 profile을 할당한다.

- PROFILE profile_name
    - 사용자가 생성한 profile_name을 할당한다.
- PROFILE DEFAULT
    - 기본 profile "DEFAULT"를 할당한다.
- PROFILE NULL
    - Profile을 할당하지 않는다.

PROFILE 절을 생략할 경우, PROFILE NULL과 동일하며 profile이 적용되지 않는다.  
비밀번호 관리 정책에 대한 자세한 내용은 [CREATE PROFILE](#aaba451f0d7d6289) 을 참조한다.

<a id="ac8230499117c2fc"></a>
#### PASSWORD EXPIRE

사용자의 비밀번호 유효기간을 만료시킨다.  
사용자가 login 하기 전에 강제로 비밀번호를 변경하도록 하기 위해 사용한다.

<a id="78cd4ff0de19ea0f"></a>
#### ACCOUNT { LOCK | UNLOCK }

- ACCOUNT LOCK
    - 사용자 계정을 잠근다.
- ACCOUNT UNLOCK
    - 계정 잠금을 해제한다.

<a id="472564024feb058f"></a>
#### DEFAULT TABLESPACE tablespace_name

User가 생성하는 테이블, 인덱스 (LOGGING) 등의 객체가 저장될 기본 TABLESPACE를 지정한다.  
DEFAULT TABLESPACE 절을 생략할 경우, DATABASE를 생성할 때 정의한 default data tablespace (MEM_DATA_TBS)가 지정된다.

<a id="358ff234ca924c21"></a>
#### TEMPORARY TABLESPACE tablespace_name

User가 생성하는 임시 테이블, 인덱스 (NO LOGGING), 질의 처리 과정에서 생성되는 중간 결과들을 저장할 TABLESPACE를 지정한다.  
TEMPORARY TABLESPACE 절을 생략할 경우, DATABASE를 생성할 때 정의한 default temporary tablespace (MEM_TEMP_TBS)가 지정된다.

<a id="3241251ff8d7075b"></a>
#### INDEX TABLESPACE { tablespace_name | NULL }

User가 생성하는 인덱스 객체가 저장되는 기본 TABLESPACE를 지정한다.

- INDEX TABLESPACE tablespace_name 지정
    - Data tablespace를 지정할 경우, LOGGING 인덱스가 된다.
    - Temporary tablespace를 지정할 경우, NOLOGGING 인덱스가 된다.

- INDEX TABLESPACE NULL
    - Index tablespace을 지정하지 않는다.

INDEX TABLESPACE 절을 생략할 경우, INDEX TABLESPACE NULL 이다.

<a id="871bfb80d3199e11"></a>
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
사용자가 소유할 스키마는 [CREATE SCHEMA](#587f9a1c3687c699) 구문을 사용하여 추가로 생성할 수 있다.

<a id="d8c1452ed7ce3f0f"></a>
### 설명

User는 권한의 집합으로 구성된 authorization 객체이다.

최초로 &lt;user definition&gt; 구문을 수행할 때 어떠한 권한도 부여받지 않은 user가 생성되고 다음과 같이 적절한 권한을 부여해야 한다.

GOLDILOCKS에서 user와 schema의 관계는 1 : N 이다.  
즉, user가 소유한 schema가 존재하지 않을 수도 있고 다수의 schema를 소유할 수도 있다.

SQL 표준은 user, schema, database 등의 non-schema 객체들의 관계에 대해 명확히 정의하지 않고 있다. 반면, 각 DBMS 들은 다음과 같이 non-schema 객체 간의 관계를 상이하게 정의하고 있다.

> DBMS별 user와 schema 관계   
> 
> 
> - Oracle
>     - User : schema = 1 : 1의 관계이다.
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
>     - User : schema = 1 : N의 관계이다. 
> 
> 
> 
> - MySQL 
>     - Database : schema = 1 : 1의 관계이다.
>     - User는 database (schema)의 하위 객체이다.
> 

<a id="36e07080c1971324"></a>
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

<a id="115e4c00aa225b74"></a>
### 호환성

SQL 표준에서는 user 개념은 다루고 있지만 user 생성 및 삭제와 관련된 SQL 구문은 정의하지 않고 있다.

<a id="b61a4df403c0eb96"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP USER](#886267e56d7bc6a6)
- [ALTER USER](#268a4621fc85878c)
- [CREATE SCHEMA](#587f9a1c3687c699)

<a id="a71e7cc52f1eefb4"></a>
## CREATE VIEW

<a id="337bf0ad2b3b944a"></a>
### 기능

View를 정의한다.

<a id="f57a52b5e429c785"></a>
### 구문

```
<view definition> ::=
    CREATE [ OR REPLACE ] [ FORCE | NO FORCE ] 
        VIEW view_name [ ( column_name [, ...] ) ]
        AS <query expression>
    ;
```

<a id="dcc3950c76c7fb56"></a>
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

<a id="a2b8982797f06563"></a>
### 구문 규칙 및 파라미터

<a id="fafe960fd4e6c8b0"></a>
#### [ OR REPLACE ]

이미 존재하는 view가 있을 경우, 기존의 view를 대체한다.

<a id="be9b661a8620952f"></a>
#### [ FORCE | NO FORCE ]

- FORCE 
    - &lt;query expression&gt;의 유효성 여부에 관계없이 view를 생성한다. 
- NO FORCE 
    - &lt;query expression&gt;이 유효할 경우 view를 생성한다.
- 기본값은 NO FORCE 이다

<a id="803095a2c62e51cf"></a>
#### view_name

생성할 view의 이름이며, 스키마 내에서 유일한 이름이어야 한다.   
schema_name.view_name과 같이 view가 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우,구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
View 이름의 길이는 128 바이트보다 작아야 한다.

<a id="dfe801532cc9420b"></a>
#### [ ( column_name [, ...] ) ]

View를 구성할 column의 이름을 정의한다.   
각 column의 이름은 view 내에서 고유한 이름이어야 한다.

Column의 개수는 SELECT 절의 결과 column 개수와 동일해야 한다.

Column 이름의 리스트를 생략할 경우, &lt;query expression&gt;의 SELECT 절의 column 이름을 사용한다.

<a id="931604114f345b74"></a>
##### AS &lt;query expression&gt;

View를 생성하는 [SELECT](#93101dc44f4e210d) 질의이다.

&lt;query expression&gt;에는 다음과 같은 변수를 포함할 수 없다.

- Host parameter 
- SQL parameter 
- Dynamic parameter 
- Embedded variable 
- SEQUENCE 객체

<a id="15c3faf8b2a5cd9c"></a>
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

<a id="3e60ec0647d69191"></a>
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

<a id="7b0a1185d2afd00e"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- [ OR REPLACE ] 절 
- [ FORCE | NO FORCE ] 절

**SQL 표준 호환성**

<a id="ce03c9faf20e9bfe"></a>
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

<a id="0bf93b3301a18d27"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DROP VIEW](#01da7763edf4f3e5)
- [ALTER VIEW](#96b15c85b467a50c)
- [SELECT](#93101dc44f4e210d)

<a id="45b9d98474d5f09d"></a>
## DECLARE cursor_name

<a id="77a784bc7909f4f0"></a>
### 기능

커서를 선언한다.

<a id="0e26cd60df601cbe"></a>
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

<a id="22d76bbf5808f3b7"></a>
### 사용 범위 및 접근 권한

statement_name을 사용한 동적 커서 (dynamic cursor)는 embedded SQL에서 사용할 수 있다.

&lt;cursor query&gt;의 유형에 따라 적절한 접근 권한을 가져야 한다.   
접근 권한에 대한 자세한 내용은 다음을 참조한다.

- [SELECT](#93101dc44f4e210d) 구문의 접근 권한
- [SELECT .. FOR UPDATE](#04b98fd332b9b4a3) 구문의 접근 권한
- [INSERT INTO name RETURNING](#71ce6ee2aa40a318) 구문의 접근 권한
- [UPDATE name RETURNING](#f05414d90d7bfdb9) 구문의 접근 권한
- [DELETE FROM name RETURNING](#acc473d63dda2275) 구문의 접근 권한

<a id="ae4030d06d5c89d5"></a>
### 구문 규칙 및 파라미터

<a id="c56a13b2e238c64c"></a>
#### cursor_name

선언할 커서의 이름이다.   
하나의 session 내에서 고유한 이름이어야 한다.   
커서 이름의 길이는 128 바이트보다 작아야 한다.

<a id="dbf013d33f373316"></a>
#### { FOR | IS }

SQL 표준에서는 구문 키워드로 FOR나 IS 중에 하나를 사용한다.

<a id="4ae606ff664742a8"></a>
#### &lt;cursor properties&gt;

커서의 속성을 정의한다.

- &lt;cursor sensitivity&gt;를 명시하지 않은 경우, 기본값은 INSENSITIVE 이다. 
- &lt;cursor scrollability&gt;를 명시하지 않은 경우, 기본값은 NO SCROLL 이다. 
- &lt;cursor holdability&gt;를 명시하지 않은 경우, &lt;cursor updatability&gt;가 기본값을 결정한다.

<a id="abb93c82d2a7578e"></a>
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

<a id="f76caa142ae92d08"></a>
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

<a id="6f9a8f7b06caaa66"></a>
#### &lt;cursor scrollability&gt;

Cursor의 result set을 순차적 또는 비순차적으로 fetch 할 수 있는지 여부를 명시한다.

- NO SCROLL 
    - 순차적 FETCH (FETCH NEXT)만 가능하다. 
- SCROLL 
    - 비순차적 FETCH가 가능하다.
- 명시하지 않을 경우, 기본값은 NO SCROLL이다.

<a id="e7059778b63bf5f8"></a>
#### &lt;cursor holdability&gt;

Cursor를 OPEN하고 트랜잭션을 commit 한 후에도 cursor가 유지되는지 여부를 설정한다.

- WITH HOLD 
    - 트랜잭션을 COMMIT 해도 cursor가 유지된다. 
    - FOR UPDATE 구문과 함께 사용할 수 없다. 
    - [INSERT INTO name RETURNING](#71ce6ee2aa40a318) 구문과 함께 사용할 수 없다. 
    - [UPDATE name RETURNING](#f05414d90d7bfdb9) 구문과 함께 사용할 수 없다. 
    - [DELETE FROM name RETURNING](#acc473d63dda2275) 구문과 함께 사용할 수 없다.

- WITHOUT HOLD 
    - 트랜잭션을 COMMIT/ ROLLBACK하면 cursor를 닫는다.

- Rollback과 cursor
    - 트랜잭션을 rollback 할 경우, 트랜잭션에 포함된 cursor를 닫는다.
    - Savepoint까지 rollback하면 savepoint 이후에 생성된 cursor를 닫는다.

- 명시하지 않을 경우, &lt;cursor holdability&gt;의 기본값은 &lt;cursor updatability&gt;에 따라 결정된다.
    - FOR READ ONLY이거나 &lt;cursor updatability&gt;를 명시하지 않은 경우, 기본값은 WITH HOLD 이다. 
    - FOR UPDATE 구문과 함께 사용할 경우, 기본값은 WITHOUT HOLD 이다.

<a id="7ee8662ea75d66e8"></a>
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

<a id="cc7b0e07d2f5d8df"></a>
| Updatability | Query 유형 | Sensitivity |
| --- | --- | --- |
| FOR UPDATE | Updatable query | SENSITIVE |
| FOR UPDATE | Non-updatable query | Query error |
| FOR READ ONLY | Any query | INSENSITIVE |
| N/A | Updatable query | SENSITIVE |
| N/A | Non-updatable query | INSENSITIVE |

<a id="79f896554c949d4b"></a>
#### &lt;cursor specification&gt;

Cursor의 대상이 되는 query를 정의한다.   
statement_name을 사용할 경우, query가 정해지지 않은 동적 커서 (dynamic cursor)가 선언되고, &lt;cursor query&gt;를 사용할 경우, query가 정해진 고정 커서 (standing cursor)가 선언된다.

<a id="fe397a086c27ea89"></a>
#### statement_name

Cursor가 참조할 statement_name이며 embedded SQL에서 사용할 수 있다.

statement_name은 &lt;declare cursor&gt; 구문을 수행하기 전에 존재해야 하며, statement_name이 참조하는 SQL 문장은 [PREPARE statement_name](#80b37906c80e6402) 구문이 준비한 query여야 한다.

Query가 아닐 경우 [OPEN cursor_name](#ee8cdd33c43f9c76) 구문을 수행할 때 error가 발생한다.

<a id="64ab907686666d41"></a>
#### &lt;cursor query&gt;

Cursor에서 사용할 수 있는 query 유형은 다음 각 구문을 참조한다.

- [SELECT](#93101dc44f4e210d)
- [SELECT .. FOR UPDATE](#04b98fd332b9b4a3)
- [INSERT INTO name RETURNING](#71ce6ee2aa40a318)
- [UPDATE name RETURNING](#f05414d90d7bfdb9)
- [DELETE FROM name RETURNING](#acc473d63dda2275)

<a id="1cf7d64fd12cbf86"></a>
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

<a id="e6c3798f0a2880aa"></a>
#### FOR UPDATE OF …

커서를 OPEN 할 때 lock 획득과 관련된 column을 나열한다.

- FOR UPDATE OF 구문에 나열된 column은
    - &lt;select statement&gt;의 FROM 절에 나열된 table의 갱신 가능한 column이어야 한다. 
    - 나열된 column의 table에 대한 lock을 획득한다. 
- FOR UPDATE만 사용하는 경우에는 
    - &lt;select statement&gt;의 FROM 절에 나열된 table들의 모든 갱신 가능한 column을 나열한 것과 동일한 의미이다. 
    - 모든 column의 table에 대한 lock을 획득한다.

<a id="accbda8972e0355d"></a>
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

<a id="c2aa239e7a2c1d58"></a>
### 설명

Query에 대한 속성을 제어할 때 DECLARE CURSOR 구문과 OPEN, FETCH, CLOSE 구문을 사용할 경우, 서버의 커서를 제어하기 때문에 ODBC statement나 JDBC statement를 이용하여 cursor를 사용하는 경우보다 성능상 부하가 걸린다.

Query를 수행하기 전에 ODBC statement와 JDBC statement를 이용해 cursor 속성을 제어할 수 있으며, DECLARE CURSOR 구문을 통한 SQL cursor의 속성 제어 방법과 이에 대응하는 ODBC 표준과 JDBC 표준의 cursor 속성 제어 방법은 다음과 같다.

<a id="f264f84a7c26a533"></a>
<table class="table column_count_4"><caption>ODBC/ JDBC의 커서 속성 제어 </caption><thead><tr><th class="to_center to_middle"><div>Property
분류</div></th><th class="to_center to_middle"><div>GOLDILOCKS
cursor property</div></th><th class="to_center to_middle"><div>ODBC 표준의 cursor 속성 설정</div></th><th class="to_center to_middle"><div>JDBC 표준의 cursor 속성 설정</div></th></tr></thead><tbody><tr><td class="to_left to_middle" rowspan="3"><div>Sensitivity</div></td><td class="to_left to_middle"><div>INSENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_INSENSITIVE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle"><div>SENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_SENSITIVE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle"><div>ASENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_UNSPECIFIED, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Scrollability</div></td><td class="to_left to_middle"><div>NO SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_NONSCROLLABLE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle"><div>SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_SCROLLABLE, len)</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Holdability</div></td><td class="to_left to_middle"><div>WITHOUT HOLD</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.CLOSE_CURSORS_AT_COMMIT )</div></td></tr><tr><td class="to_left to_middle"><div>WITH HOLD</div></td><td class="to_left to_middle"><div>설정할 수 없음</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.HOLD_CURSORS_OVER_COMMIT )</div></td></tr></tbody></table>

ODBC cursor type에 대응되는 SQL cursor 선언은 다음과 같다.

**ODBC 커서 type에 대응되는 SQL 커서 선언**

<a id="4f733cab83bfbfc6"></a>
| ODBC cursor type | SQL cursor 선언 |
| --- | --- |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, len) | NO SCROLL CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_STATIC, len) | STATIC CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, len) | KEYSET CURSOR |

JDBC cursor type에 대응되는 SQL cursor 선언은 다음과 같다.

**JDBC 커서 type에 대응되는 SQL 커서 선언**

<a id="6e929bd95ef4b1fb"></a>
| JDBC cursor type | SQL cursor 선언 |
| --- | --- |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_FORWARD_ONLY, conc, hold ) | INSENSITIVE NO SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_INSENSITIVE, conc, hold ) | INSENSITIVE SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_SENSITIVE, conc, hold ) | SENSITIVE SCROLL CURSOR |

<a id="1bddae9c32922f98"></a>
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

<a id="19a957ee77fb7d06"></a>
### 호환성

&lt;declare cursor&gt; 구문은 SQL 표준과 비교하여 다음과 같은 차이가 있다.

- SQL 표준의 &lt;cursor sensitivity&gt; 기본값은 ASENSITIVE이지만, GOLDILOCKS의 기본값은 INSENSITIVE이다. 
- SQL 표준에서는 다음과 같은 &lt;odbc cursor type&gt;을 다루지 않고 있다. 
    - STATIC CURSOR 
    - KEYSET CURSOR 
- SQL 표준의 &lt;cursor holdability&gt; 기본값은 WITHOUT HOLD이지만, GOLDILOCKS의 기본값은 &lt;cursor updatability&gt;에 따라 다르다. 
- SQL 표준에서는 &lt;cursor query&gt;로 &lt;select statement&gt;만 사용할 수 있지만, GOLDILOCKS는 다음과 같은 returning query를 사용할 수 있다. 
    - [INSERT INTO name RETURNING](#71ce6ee2aa40a318)
    - [UPDATE name RETURNING](#f05414d90d7bfdb9)
    - [DELETE FROM name RETURNING](#acc473d63dda2275)
- SQL 표준의 &lt;cursor updatability&gt; 기본값은 &lt;select statement&gt;에 따라 결정되지만, GOLDILOCKS의 기본값은 FOR READ ONLY이다. 
- SQL 표준에는 &lt;lock wait mode&gt; 구문이 존재하지 않는다.

**SQL 표준 호환성**

<a id="498b5d7acd3501c5"></a>
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

<a id="8c5f9f728388c374"></a>
### 참조

관련 내용은 다음을 참조한다.

- [OPEN cursor_name](#ee8cdd33c43f9c76)
- [FETCH cursor_name](#bafc38978b00122c)
- [CLOSE cursor_name](#38584f03f4e1823e)
- [PREPARE statement_name](#80b37906c80e6402)
- [SELECT](#93101dc44f4e210d)
- [SELECT .. FOR UPDATE](#04b98fd332b9b4a3)
- [INSERT INTO name RETURNING](#71ce6ee2aa40a318)
- [UPDATE name RETURNING](#f05414d90d7bfdb9)
- [DELETE FROM name RETURNING](#acc473d63dda2275)

<a id="dc15cd536dd459be"></a>
## DELETE FROM

<a id="dc0fe2e68017a7a4"></a>
### 기능

테이블의 row들을 삭제한다.

<a id="0b4edb470b408bdb"></a>
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

<a id="1ecb8b5078468244"></a>
### 사용 범위 및 접근 권한

&lt;delete statement: searched&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블에 대해 (DELETE 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (DELETE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DELETE ANY TABLE ON DATABASE

<a id="2f3961eb9f5a01bc"></a>
### 구문 규칙 및 파라미터

<a id="de31b6dc158e2070"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="0a7756e26a400b47"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="e075240e044a61dd"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 삭제한다.  
WHERE 조건을 명시하지 않은 경우, 모든 row를 삭제한다.  
WHERE 조건의 자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 [where clause](#21c50afccf7f4c56)를 참조한다.

<a id="0e0cb3d1d6646f9c"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 [offset limit clause](#2e8423d8813ebc76)를 참조한다.

<a id="bff55be5fddb0b83"></a>
#### &lt;fetch limit clause&gt;

Fetch 할 row의 개수를 명시하는 구문으로써 다음 두 가지 방법이 사용된다.

- &lt;fetch first clause&gt;
    - Fetch 할 row의 개수를 명시한다.
    - 자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 &lt;[fetch first clause&gt;](#a9aa8a6af48851ad)를 참조한다.
- &lt;limit clause&gt;
    - Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
    - 자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 &lt;[limit clause&gt;](#a9e285c38ace622d)를 참조한다.

<a id="e9b6d466486cf341"></a>
### 설명

<a id="31ec05640e1454f7"></a>
#### DELETE 관련 구문들의 차이점

- [DELETE FROM](#dc15cd536dd459be)
    - 조건에 부합하는 다수의 row를 삭제한다. 
    - 예: DELETE FROM t1 WHERE c1 = 0; 
- [DELETE FROM name WHERE CURRENT OF cursor_name](#b3ff03382448adb2)
    - Cursor가 현재 가리키는 row를 삭제한다. 
    - 예: DELETE FROM t1 WHERE CURRENT OF cursor; 
- [DELETE FROM name RETURNING](#acc473d63dda2275)
    - 조건에 부합하는 다수의 row를 삭제하며, [SELECT](#93101dc44f4e210d) 구문과 동일한 방식( SQLFetch() 등의 API )으로 삭제한 row들을 검색할 수 있다. 
    - 예: DELETE FROM t1 WHERE c1 = 0 RETURNING c2; 
- [DELETE FROM name RETURNING .. INTO](#9a7940989e5a74ce)
    - 한 건 이하의 row를 삭제할 수 있으며, 삭제한 row가 한 건일 경우 RETURNING INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: DELETE FROM t1 WHERE c1 = 0 RETURNING c2 INTO :v1;

<a id="75556db5a00e1e1a"></a>
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

<a id="44cec8ef08eaa308"></a>
### 호환성

SQL 표준은 DELETE 구문에서 다음 절을 정의하지 않고 있다.

- &lt;result offset clause&gt; 
- &lt;fetch limit clause&gt;

**SQL 표준 호환성**

<a id="7d2e780d0b9405c1"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="8a9439566df9a245"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DELETE FROM name WHERE CURRENT OF cursor_name](#b3ff03382448adb2)
- [DELETE FROM name RETURNING](#acc473d63dda2275)
- [DELETE FROM name RETURNING .. INTO](#9a7940989e5a74ce)
- [SELECT](#93101dc44f4e210d)

<a id="acc473d63dda2275"></a>
## DELETE FROM name RETURNING

<a id="d9bd868cbe3126e8"></a>
### 기능

테이블의 row들을 삭제하고, 삭제한 row들을 검색한다.

<a id="df4fe1abb753ed52"></a>
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

<a id="d1d50f9ebb623f0d"></a>
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

<a id="459e70365369e8d8"></a>
### 구문 규칙 및 파라미터

<a id="faea7806bdf377c2"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.

<a id="275c7b08af34dea0"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="277d30767d74e8a5"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 삭제한다.  
자세한 내용은 [DELETE FROM](#dc15cd536dd459be) 구문을 참조한다.

<a id="0db7557f8cb44e27"></a>
#### &lt;result offset clause&gt;

질의 결과 중에 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#dc15cd536dd459be) 구문을 참조한다.

<a id="ec802e284dc6db83"></a>
#### &lt;fetch first clause&gt;

Fetch 할 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#dc15cd536dd459be) 구문을 참조한다.

<a id="5be94d9bf53ec55e"></a>
#### &lt;limit clause&gt;

Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.  
자세한 내용은 [DELETE FROM](#dc15cd536dd459be) 구문을 참조한다.

<a id="f4a79d9aedac5863"></a>
#### &lt;returning clause&gt;

삭제된 row들을 결과 집합으로 하고, 이들 중에서 검색할 column을 기술한다.

- RETURNING 절은 DELETE 구문으로 삭제된 row들을 result set으로 하는 결과를 반환한다. 
- &lt;value expression&gt; 
    - SELECT 구문의 &lt;select list&gt;와 동일하지만 aggregation 등을 사용할 수 없다. 
- [[AS] alias_name] 
    - AS 절을 이용해 value expression의 이름을 지정할 수 있다.

RETURN과 RETURNING은 동일한 의미의 키워드이다.

<a id="7516945a69f6813a"></a>
### 설명

자세한 내용은 [DELETE 관련 구문들의 차이점](#31ec05640e1454f7)을 참조한다.

<a id="6f8462a23e6c7a03"></a>
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

<a id="aef3d0b617822337"></a>
### 호환성

SQL 표준에는 &lt;delete returning query statement&gt; 구문이 존재하지 않는다.

<a id="22769b1d72618cb1"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DELETE FROM](#dc15cd536dd459be)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#b3ff03382448adb2)
- [DELETE FROM name RETURNING .. INTO](#9a7940989e5a74ce)
- [SELECT](#93101dc44f4e210d)

<a id="9a7940989e5a74ce"></a>
## DELETE FROM name RETURNING .. INTO

<a id="6f28fc3db452b5b6"></a>
### 기능

테이블에서 row 하나를 삭제하고, 삭제한 row의 값을 호스트 변수에 얻어온다.

<a id="1d1d1cffae6a4219"></a>
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

<a id="751295a89ee9fbfc"></a>
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

<a id="f8efec16cc36200c"></a>
### 구문 규칙 및 파라미터

<a id="fa18b189fbbfd8d0"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.

<a id="457f70a09f5a0a92"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="14a0b82a2b2f2a70"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 삭제한다.  
자세한 내용은 [DELETE FROM](#dc15cd536dd459be) 구문을 참조한다.

<a id="5d44f6ce1b211eb0"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#dc15cd536dd459be) 구문을 참조한다.

<a id="4f66294831471f92"></a>
#### &lt;fetch first clause&gt;

Fetch 할 row의 개수를 명시한다.  
자세한 내용은 [DELETE FROM](#dc15cd536dd459be) 구문을 참조한다.

<a id="4ec2cef07e8e3bff"></a>
#### &lt;limit clause&gt;

Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.  
자세한 내용은 [DELETE FROM](#dc15cd536dd459be) 구문을 참조한다.

<a id="84c393b73982e604"></a>
#### &lt;returning into clause&gt;

- RETURNING .. AS ..
    - [DELETE FROM name RETURNING](#acc473d63dda2275) 구문의 returning clause를 참조한다.
- INTO variable_name [, ...]
    - INTO 절에 기술된 변수의 개수는 RETURNING 절에 기술된 expression의 개수와 동일해야 한다.

<a id="8550043af07cbe63"></a>
### 설명

삭제할 row가 하나 이하여야 한다.   
둘 이상의 row가 삭제되면 에러가 발생한다.

자세한 내용은 [DELETE 관련 구문들의 차이점](#31ec05640e1454f7)을 참조한다.

<a id="5bc3ca1a2019c8cf"></a>
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

<a id="d9a718683b25eddb"></a>
### 호환성

SQL 표준에는 &lt;delete returning into statement&gt; 구문이 존재하지 않는다.

<a id="f0c38081e35d881a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DELETE FROM](#dc15cd536dd459be)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#b3ff03382448adb2)
- [DELETE FROM name RETURNING](#acc473d63dda2275)
- [SELECT](#93101dc44f4e210d)

<a id="b3ff03382448adb2"></a>
## DELETE FROM name WHERE CURRENT OF cursor_name

<a id="4b56c331f0a34dd9"></a>
### 기능

커서가 가리키는 row 하나를 삭제한다.

<a id="3381cbb486351bd7"></a>
### 구문

```
<delete statement: positioned> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        WHERE CURRENT OF cursor_name
    ;
```

<a id="a906ad30cfffa123"></a>
### 사용 범위 및 접근 권한

&lt;delete statement: positioned&gt; 구문을 수행하려면 사용자에게 [DELETE FROM](#dc15cd536dd459be) 구문을 수행할 수 있는 권한이 있어야 한다.

<a id="cc8485680805e029"></a>
### 구문 규칙 및 파라미터

<a id="90358e411b11f773"></a>
#### table_name

Row를 삭제할 대상 테이블의 이름이다.

<a id="67cd4fa4489f9a08"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="ca62da6f7ab1054e"></a>
#### cursor_name

cursor_name에 해당하는 커서는 다음 조건을 만족해야 한다.

- OPEN 된 커서여야 한다. ([OPEN cursor_name](#ee8cdd33c43f9c76)을 참조한다.) 
- 커서를 이용해 FETCH 한 row가 존재해야 한다. ([FETCH cursor_name](#bafc38978b00122c)을 참조한다.) 
- 커서를 위해 사용된 질의가 table_name을 식별할 수 있어야 한다. ([DECLARE cursor_name](#45b9d98474d5f09d)을 참조한다.) 
- table_name에 대해 갱신할 수 있는 커서여야 한다. ([DECLARE cursor_name](#45b9d98474d5f09d)을 참조한다.)

<a id="5d4c7848772518fb"></a>
### 설명

자세한 내용은 [DELETE 관련 구문들의 차이점](#31ec05640e1454f7)을 참조한다.

<a id="4a1c7e12d00a469b"></a>
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

<a id="ffe6c1deff1aeb8b"></a>
### 호환성

**SQL 표준 호환성**

<a id="8370893b50b430a5"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| S111 | ONLY in query expressions | X |
| B031 | Basic dynamic SQL | O |

<a id="447c29d7debd3b2f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#45b9d98474d5f09d)
- [OPEN cursor_name](#ee8cdd33c43f9c76)
- [FETCH cursor_name](#bafc38978b00122c)
- [DELETE FROM](#dc15cd536dd459be)
- [DELETE FROM name RETURNING](#acc473d63dda2275)
- [DELETE FROM name RETURNING .. INTO](#9a7940989e5a74ce)

<a id="4c985d8424a9c9e1"></a>
## DROP AUDIT POLICY

<a id="56b84bf81fb011d2"></a>
### 기능

Audit policy를 제거한다.

<a id="8cd90ff5b079ecf5"></a>
### 구문

```
<drop audit policy statement> ::= 
    DROP AUDIT POLICY [ IF EXISTS ] policy_name
;
```

<a id="2a2004dd04307644"></a>
### 사용 범위 및 접근 권한

&lt;drop audit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="a7d1bb474c18ebb2"></a>
### 구문 규칙 및 파라미터

<a id="ed000039d2b537bc"></a>
#### IF EXISTS

policy_name이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="20ef527420e71a39"></a>
#### policy_name

제거할 audit policy 객체의 이름이다.

<a id="1f76496ec49960b0"></a>
### 설명

이미 활성화된 audit policy 객체는 제거할 수 없다. 이 경우, NOAUDIT POLICY 구문을 이용해 audit policy를 비활성화해야 한다.

<a id="2849ecf9c0aafecf"></a>
### 사용 예

다음은 audit policy를 제거하는 예이다.

```
DROP AUDIT POLICY policy_table;
```

<a id="1163578b400b0866"></a>
### 호환성

SQL 표준에는 audit policy가 존재하지 않는다.

<a id="a7c4240249e57f15"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#09b3895daf4991da)
    - [DROP AUDIT POLICY](#4c985d8424a9c9e1)
    - [ALTER AUDIT POLICY](#241fd4b15c525c5a)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#8c7812c0671b6a25)
    - [NOAUDIT POLICY](#f4896aa89ec963af)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#6c787a4b953e8625)

- Audit trail 소거: [ALTER DATABASE CLEAR AUDIT TRAIL](#d0a56f6310b7a28c)

<a id="e491103ba644ea1a"></a>
## DROP CLUSTER GROUP

<a id="4503122ef8908202"></a>
### 기능

Cluster group을 cluster system에서 제거한다.

<a id="81af2764d9d0b6a1"></a>
### 구문

```
<drop cluster group statement> ::=
    DROP CLUSTER GROUP [IF EXISTS] group_name
    ;
```

<a id="a78fd9b41979de55"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.   
&lt;drop cluster group statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="74022258fd6f2643"></a>
### 구문 규칙 및 파라미터

<a id="d19189c894843b6c"></a>
#### [IF EXISTS]

Cluster group이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="adf9e82d4fa535ae"></a>
#### group_name

Cluster group의 이름이다.   
Shard가 존재하지 않는 cluster group을 제거할 수 있다.

<a id="17a58b9abecb3c56"></a>
### 설명

Cluster group을 제거하더라도 data loss가 발생하지 않는 경우에 해당 cluster group을 제거할 수 있다.  
단, global coordinator를 포함하는 group을 제거하려 할 경우, 에러가 발생할 수 있다.

<a id="a5d4e105e8d5f630"></a>
### 사용 예

다음은 cluster group을 제거하는 예이다.

```
gSQL> DROP CLUSTER GROUP g3;

Cluster Group dropped.
```

<a id="efa07acc179f539b"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="119eac5259ced899"></a>
### 참조

관련 내용은 [CREATE CLUSTER GROUP](#dd23e8e2eae3991d)을 참조한다.

<a id="8d977b885f9df018"></a>
## DROP CLUSTER LOCATION

<a id="46d9df2d5f85697a"></a>
### 기능

Cluster member의 접속 정보를 삭제한다.

<a id="14e9edba3eb899bd"></a>
### 구문

```
<drop cluster location statement> ::=
    DROP CLUSTER LOCATION member_name 
    ;
```

<a id="0a600952c7816412"></a>
### 사용 범위 및 접근 권한

Cluster system에서 수행할 수 있다.   
&lt;drop cluster location statement&gt; 구문을 수행하려면 사용자에게 ADMINISTRATION ON DATABASE 권한이 있어야 한다.

<a id="4f7655bcc43fa9e7"></a>
### 구문 규칙 및 파라미터

<a id="9b3ac3c26b0bb473"></a>
#### member_name

Cluster member의 이름이다.   
등록된 cluster location 정보에 동일한 cluster member 이름이 존재해야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="9ad750b00c576831"></a>
### 설명

기본적으로 cluster location 정보는 cluster group을 생성할 때나 cluster member를 추가할 때 제공되는 접속 정보를 이용하여 자동으로 생성된다. 생성된 정보는 cluster member나 group을 삭제할 때 함께 삭제된다.

만약 cluster location의 접속 정보가 변경되면 cluster member을 삭제하거나 재생성할 필요없이 [ALTER CLUSTER LOCATION](#8193ea3b3b99d43b) 을 이용하여 접속 정보를 변경할 수 있다.

<a id="7c11a813b1d8f999"></a>
### 사용 예

```
gSQL> 
DROP CLUSTER LOCATION g1n2
;

Created
```

<a id="e9cf840b9764bf55"></a>
### 호환성

SQL 표준에서는 cluster에 대한 개념을 정의하지 않고 있다.

<a id="1e800825fd558857"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE CLUSTER LOCATION](#c88dc891576217eb)
- [ALTER CLUSTER LOCATION](#8193ea3b3b99d43b)

<a id="8921114ccac5a25e"></a>
## DROP INDEX

<a id="d983b1390508ca01"></a>
### 기능

인덱스를 제거한다.

<a id="7a12cfbd39481976"></a>
### 구문

```
<drop index statement> ::=
    DROP INDEX [ IF EXISTS ] index_name
    ;
```

<a id="af8d6b92eb8b4629"></a>
### 사용 범위 및 접근 권한

&lt;drop index statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 인덱스의 소유자 
- 인덱스가 속한 테이블의 소유자 
- 인덱스가 속한 테이블에 대해 CONTROL TABLE ON TABLE 
- 인덱스가 속한 스키마에 대해 (DROP INDEX 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY INDEX ON DATABASE

<a id="f40c6589c106fd4c"></a>
### 구문 규칙 및 파라미터

<a id="04de1a0719966a5c"></a>
#### IF EXISTS

인덱스가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="cfa2ccb05d914c8b"></a>
#### index_name

삭제할 인덱스의 이름이다.   
schema_name.index_name과 같이 인덱스가 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

UNIQUE 제약 조건, PRIMARY KEY 제약 조건을 위해 생성한 인덱스는 제거할 수 없다.  
위 제약 조건을 위해 생성된 인덱스를 제거하려면 [ALTER TABLE name DROP CONSTRAINT](#ee7de4b9dadd1b3a) 구문을 사용하여 관련된 제약 조건을 삭제해야 한다.

<a id="1836ee87b59d54e4"></a>
### 설명

DROP INDEX와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="1e1f19b9a87f62be"></a>
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

<a id="d0895350d9db7ad6"></a>
### 호환성

SQL 표준에서는 인덱스에 대한 개념을 다루지 않고 있다.

<a id="f88f21c27aabe65d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE INDEX](#9d2795ea1fc7b4c6)
- [DROP TABLE](#2481c7252f63dc1c)
- [ALTER TABLE name DROP CONSTRAINT](#ee7de4b9dadd1b3a)

<a id="317a2852ef6da864"></a>
## DROP PROFILE

<a id="336cd4b4ba3e9ab8"></a>
### 기능

Profile을 삭제한다.

<a id="b068514c3d1134ee"></a>
### 구문

```
<drop profile statement> ::= 
    DROP PROFILE [ IF EXISTS ] profile_name [ CASCADE ] ;
```

<a id="7455b12fb2bff020"></a>
### 사용 범위 및 접근 권한

&lt;drop profile statement&gt; 구문을 수행하려면 사용자에게 DROP PROFILE ON DATABASE 권한이 있어야 한다.

<a id="f9d224440b56a063"></a>
### 구문 규칙 및 파라미터

<a id="03fc78b77642b8c5"></a>
#### IF EXISTS

Profile이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="e22b3e4c1f3ebead"></a>
#### profile_name

삭제할 profile의 이름을 명시한다.   
DEFAULT profile은 삭제할 수 없다.

<a id="8d24852717375528"></a>
#### CASCADE

이미 할당받은 사용자들이 존재하는 경우, profile을 삭제하기 위해 반드시 이 절을 명시해야 한다.   
삭제할 profile을 할당받은 사용자들의 profile은 DEFAULT profile로 변경한다.

<a id="06e340df41138d7a"></a>
### 사용 예

다음은 CASCADE 구문을 사용하여 profile을 삭제하는 예이다.

```
gSQL> DROP PROFILE prof CASCADE;

Profile dropped.

gSQL> COMMIT;

Commit complete.
```

<a id="fc011fcd8fe25f3d"></a>
### 호환성

SQL 표준에서는 profile에 대한 개념을 다루지 않고 있다.

<a id="590472966fba7f0f"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE PROFILE](#aaba451f0d7d6289)
- [ALTER PROFILE](#707c01f0b15f9ab0)

<a id="1197651d9b38835b"></a>
## DROP SCHEMA

<a id="11f919e8d51a710b"></a>
### 기능

스키마를 제거한다.

<a id="f8ef8f5c4b70c848"></a>
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

<a id="75cedf2f750fabfc"></a>
### 사용 범위 및 접근 권한

&lt;drop schema statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 스키마의 소유자 
- 해당 스키마에 대해 CONTROL SCHEMA ON SCHEMA 
- DROP SCHEMA ON DATABASE

<a id="c42f62c0adf48907"></a>
### 구문 규칙 및 파라미터

<a id="666c034aca9c13f3"></a>
#### IF EXISTS

스키마가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="4a291b48495cfc17"></a>
#### schema_name

제거할 스키마의 이름이다.   
단, database를 생성할 때 자동으로 생성되는 DICTIONARY_SCHEMA, INFORMATION_SCHEMA, PUBLIC과 같은 built-in 스키마는 제거할 수 없다.

<a id="97b7f49a34e92b6c"></a>
#### &lt;drop behavior&gt;

- RESTRICT 
    - Schema 내에 존재하는 객체가 없어야 한다. 
- CASCADE 
    - Schema 내의 모든 객체를 함께 제거한다.
- 생략할 경우, 기본값은 RESTRICT이다.

<a id="d391de7fc095bc9e"></a>
### 설명

DROP SCHEMA와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다. 이 때, 제거하는 스키마에 포함된 휴지통 객체들도 제거된다.

<a id="fca8e947bb479688"></a>
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

<a id="02b3ac65e5327ea7"></a>
### 호환성

SQL 표준에서는 IF EXISTS 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="aad6fc8882a2f526"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |
| F381 | Extended schema manipulation | O |

<a id="1e2b526b3444198e"></a>
### 참조

관련 내용은 [CREATE SCHEMA](#587f9a1c3687c699)를 참조한다.

<a id="8c2068e78d2e75d6"></a>
## DROP SEQUENCE

<a id="0f466e83b5f0e252"></a>
### 기능

시퀀스를 제거한다.

<a id="b8956dc968f1bb3b"></a>
### 구문

```
<drop sequence generator statement> ::=
    DROP SEQUENCE [ IF EXISTS ] [schema_name.] sequence_name 
    ;
```

<a id="fc976d373389ffd8"></a>
### 사용 범위 및 접근 권한

&lt;drop sequence generator statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 시퀀스의 소유자 
- 시퀀스가 속한 스키마에 대해 (DROP SEQUENCE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY SEQUENCE ON DATABASE

<a id="5674716a2afdaadd"></a>
### 구문 규칙 및 파라미터

<a id="edd15f9fa1fc4d50"></a>
#### IF EXISTS

시퀀스가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="2b129012ddc32e99"></a>
#### sequence_name

제거할 시퀀스의 이름이다.   
schema_name.sequence_name과 같이 시퀀스가 속할 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="52c9d4127c279a09"></a>
### 설명

DROP SEQUENCE와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="2db56ce6be4e359a"></a>
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

<a id="4d8e39925e3d082f"></a>
### 호환성

SQL 표준에서는 IF EXISTS 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="9ad614b1f1848cd3"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="d76f571266921874"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE SEQUENCE](#2eb16f80ff00b702)
- [ALTER SEQUENCE](#ebac80e511ac5859)

<a id="c4938ba3825fd271"></a>
## DROP SYNONYM

<a id="2b3d92d52a6d7b35"></a>
### 기능

Synonym을 제거한다.

<a id="f040d45916d0250d"></a>
### 구문

```
<drop synonym statement> ::=
    DROP [ PUBLIC ] SYNONYM [ IF EXISTS ] [schema_name.]synonym_name
    ;
```

<a id="1b20406c4b732f4f"></a>
### 사용 범위 및 접근 권한

PUBLIC을 명시하여 public synonym을 제거하려면 DROP PUBLIC SYNONYM ON DATABASE 권한이 있어야 한다.

Private synonym을 제거하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 synonym의 소유자 
- Synonym이 속한 스키마에 대해 (DROP SYNONYM 또는 CONTROL SCHEMA) ON SCHEMA
- DROP ANY SYNONYM ON DATABASE

<a id="45d64570ae18b909"></a>
### 구문 규칙 및 파라미터

<a id="827b1b6789b2648d"></a>
#### [ PUBLIC ]

Public synonym을 제거하고자 할 때 명시한다.   
이 절을 생략하면 private synonym이 제거된다.

<a id="30db03342980f76b"></a>
#### IF EXISTS

Synonym이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="7e017a52b3a7276a"></a>
#### synonym_name

제거할 synonym의 이름이다.  
schema_name.synonym_name과 같이 synonym이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.   
PUBLIC을 명시한 경우, 스키마 이름을 명시할 수 없다.

<a id="2af3fb4042696633"></a>
### 설명

DROP SYNONYM과 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="a5cb9e7e65be8d6f"></a>
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

<a id="bdbe2281e04fd26c"></a>
### 호환성

SQL 표준에서는 DROP SYNONYM 구문을 정의하지 않고 있다.

<a id="7b94c8f2c82dcdb6"></a>
### 참조

관련 내용은 [CREATE SYNONYM](#f32eb8a1d0dbc720)을 참조한다.

<a id="2481c7252f63dc1c"></a>
## DROP TABLE

<a id="c977c4bb94447dc5"></a>
### 기능

테이블을 제거한다.

> 휴지통 기능이 활성화되어 있을 경우, 테이블이 즉시 제거되지 않고 휴지통에 보관된다.

<a id="1d279f69812bfd28"></a>
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

<a id="484fd72a51cdbed3"></a>
### 사용 범위 및 접근 권한

&lt;drop table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블의 소유자 
- 해당 테이블에 대해 CONTROL TABLE ON TABLE 
- 테이블이 속한 스키마에 대해 (DROP TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY TABLE ON DATABASE

<a id="5fc7cfbf216c6ae8"></a>
### 구문 규칙 및 파라미터

<a id="e48375fbcd1e7d2e"></a>
#### IF EXISTS

테이블이 존재하지 않더라도 에러가 발생하지 않는다.

<a id="90f1a90101542749"></a>
#### table_name

제거할 테이블의 이름이다.   
schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

Database를 생성할 때 자동으로 생성되는 다음과 같은 테이블들은 삭제할 수 없다.

- DEFINITION_SCHEMA 스키마의 테이블들 
- FIXED_TABLE_SCHEMA 스키마의 테이블들

테이블에 생성된 제약 조건과 인덱스도 함께 제거한다.

<a id="4429a32a9d8a4b7e"></a>
#### drop behavior

현재는 RESTRICT/ CASCADE가 동일하게 동작한다.   
생략할 경우, 기본값은 RESTRICT 이다.

<a id="801d627d727e5f2b"></a>
#### purge

휴지통 기능이 활성화된 경우에도 테이블을 휴지통에 보관하지 않고 즉시 제거한다.

<a id="b85f8323339e9b6b"></a>
### 설명

DROP TABLE과 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="1c98f5d28362c0a3"></a>
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

<a id="2891689ba18af986"></a>
### 호환성

SQL 표준에서는 다음과 같은 절을 정의하지 않고 있다.

- IF EXISTS 
- CASCADE CONSTRAINTS

**SQL 표준 호환성**

<a id="fa44510bb247a275"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |

<a id="7743deb78fb37aa6"></a>
### 참조

관련 내용은 [CREATE TABLE](#9b82da6d66aabe8c)을 참조한다.

<a id="703c847167e78d53"></a>
## DROP TABLESPACE

<a id="d2fdaed66024dd25"></a>
### 기능

테이블스페이스를 제거한다.

<a id="40f63bad316efa45"></a>
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

<a id="1c68d4e2990155d2"></a>
### 사용 범위 및 접근 권한

&lt;drop tablespace definition&gt; 구문을 수행하려면 사용자에게 DROP TABLESPACE ON DATABASE 권한이 있어야 한다.

<a id="33f3ad4121341b8f"></a>
### 구문 규칙 및 파라미터

<a id="b566e9ad9b99e851"></a>
#### IF EXISTS

테이블스페이스가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="9679a08ab9c8cb6c"></a>
#### tablespace_name

제거할 테이블스페이스의 이름이다.

Database를 생성할 때 구축되는 다음과 같은 시스템 테이블스페이스는 제거할 수 없다.

- DICTIONARY_TBS: system tablespace for dictionary management 
- MEM_UNDO_TBS: system tablespace for default undo tablespace 
- MEM_DATA_TBS: system tablespace for default user data tablespace 
- MEM_TEMP_TBS: system tablespace for default temporary tablespace

> tablespace_name이 사용자들의 default tablespace로 사용되고 있었다면 tablespace가 제거된 후에는 객체를 위한 공간을 할당받을 수 없다. 따라서 tablespace를 제거한 후에 [ALTER USER](#268a4621fc85878c) 구문을 사용하여 사용자들의 default tablespace를 변경해 주어야 한다.

<a id="b86b4d02cba4eccb"></a>
#### INCLUDING CONTENTS

테이블스페이스에 속하는 객체 (table, index, key constraints)를 삭제한다. 테이블스페이스에 속하는 table을 참조하는 index와 key constraints가 테이블스페이스 외부에 존재할 경우에는 이들도 함께 삭제한다.

INCLUDING CONTENTS 구문을 사용하지 않을 경우에는 테이블스페이스에 속하는 객체가 없어야 한다.

<a id="3154f058a23b2ab8"></a>
#### [ { AND | KEEP } DATAFILES ]

테이블스페이스를 구성하는 데이터 파일들을 함께 삭제할지 여부를 지정한다.   
Memory temporary tablespace에는 데이터 파일이 존재하지 않으므로, 해당 절은 무시된다.

- AND DATAFILES 
    - 데이터 파일들을 함께 삭제한다. 
- KEEP DATAFILES 
    - 데이터 파일을 삭제하지 않고 남겨둔다. 
- 명시하지 않을 경우, 기본값은 KEEP DATAFILES 이다.

<a id="9f530517fcdc1bd5"></a>
#### drop behavior

현재는 RESTRICT/ CASCADE가 동일하게 동작한다.   
생략할 경우, 기본값은 RESTRICT 이다.

<a id="2f1e5911bfb5fa4c"></a>
### 설명

다른 Data Definition Language (DDL)과 달리 DROP TABLESPACE 구문은 ROLLBACK 할 수 없으며, 구문을 수행한 transaction이 자동으로 COMMIT 된다. 이 때 제거하는 테이블스페이스에 포함된 휴지통 객체들도 함께 제거된다.

<a id="1bef9084f53aa9a9"></a>
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

<a id="04e6ad8fbf3254a4"></a>
### 호환성

SQL 표준은 tablespace에 대한 개념을 다루지 않고 있다.

<a id="4231d3635b51918e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE MEMORY DATA TABLESPACE](#e61b814a9f21f32f)
- [CREATE MEMORY TEMPORARY TABLESPACE](#bcdcadc8e58b6578)
- [ALTER TABLESPACE](#bf506f295181b38d)

<a id="886267e56d7bc6a6"></a>
## DROP USER

<a id="99773a3bce3d68be"></a>
### 기능

데이터베이스 사용자를 제거한다.

<a id="ee7ba2f3f3e6eee3"></a>
### 구문

```
<drop user statement> ::=
    DROP USER [ IF EXISTS ] user_identifier [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
```

<a id="fe1690216ec2a17e"></a>
### 사용 범위 및 접근 권한

&lt;drop user statement&gt; 구문을 수행하려면 사용자에게 DROP USER ON DATABASE 권한이 있어야 한다.

> user_identifier가 소유한 스키마가 존재하지 않아야 한다.  
> 스키마 제거에 대한 자세한 내용은 [DROP SCHEMA](#1197651d9b38835b) 구문을 참조한다.

<a id="c5d820ed9d084b72"></a>
### 구문 규칙 및 파라미터

<a id="baaf2e556d14f018"></a>
#### IF EXISTS

사용자가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="3ef65d6bb44976c7"></a>
#### user_identifier

제거할 데이터베이스 사용자의 이름이다.   
단, database를 생성할 때 자동으로 생성되는 "SYS" 등과 같은 사용자는 제거할 수 없다.

다음과 같이 user_identifier가 생성했으나, 소유자가 아닌 객체는 제거하지 않는다.

- Role 
- Tablespace

<a id="47bfc130bc5c1875"></a>
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

<a id="b2fb80680fd116e8"></a>
### 설명

GOLDILOCKS에서 user와 schema의 관계는 1 : N 이다.   
즉, user가 schema를 소유하지 않을 수도 있고, 다수의 schema를 소유할 수도 있다.

User 객체를 제거하려면 user가 소유한 모든 schema를 제거해야 한다. 이 때, 제거하는 user 객체의 휴지통 객체들도 함께 제거된다.

<a id="6b0c1aba77f722f0"></a>
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

<a id="73f61290df3a3a13"></a>
### 호환성

SQL 표준에서는 user의 개념은 다루고 있지만 user의 생성 및 제거와 관련된 SQL 구문은 정의하지 않고 있다.

<a id="6b579877374d7e06"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE USER](#8e5920c927752802)
- [ALTER USER](#268a4621fc85878c)
- [DROP SCHEMA](#1197651d9b38835b)

<a id="01da7763edf4f3e5"></a>
## DROP VIEW

<a id="cc5cc7a1fd5b908d"></a>
### 기능

View를 제거한다.

<a id="2214a1803fb413cf"></a>
### 구문

```
<drop view statement> ::=
    DROP VIEW [ IF EXISTS ] view_name
    ;
```

<a id="e7b5ed505d7d3c38"></a>
### 사용 범위 및 접근 권한

&lt;drop view statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 view의 소유자 
- 해당 view에 대해 CONTROL TABLE ON TABLE 
- View가 속한 스키마에 대해 (DROP VIEW 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY VIEW ON DATABASE

<a id="6b754dd8dff1578e"></a>
### 구문 규칙 및 파라미터

<a id="9ddbe54f62306892"></a>
#### IF EXISTS

View가 존재하지 않더라도 에러가 발생하지 않는다.

<a id="ec5044642b43c593"></a>
#### view_name

제거할 view의 이름이다.   
schema_name.view_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="009eca4fc01fd879"></a>
### 설명

DROP VIEW와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="61f6002ea807b87a"></a>
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

<a id="63ca0785c4739eca"></a>
### 호환성

SQL 표준에서는 IF EXISTS 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="04624c554bad1731"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |

<a id="a8127ad394d13555"></a>
### 참조

관련 내용은 다음을 참조한다.

- [CREATE VIEW](#a71e7cc52f1eefb4)
- [ALTER VIEW](#96b15c85b467a50c)

<a id="6884ae114f6016e7"></a>
## EXECUTE IMMEDIATE 'sql_string'

<a id="8baaf3f4d40682cd"></a>
### 기능

프로그램 작성 시점에 정의되지 않았던 dynamic SQL 문장을 수행한다.

<a id="36f959ba33a2c1b1"></a>
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

<a id="d005ede6ab9e0fef"></a>
### 사용 범위 및 접근 권한

Embedded SQL에서 사용할 수 있다.   
Dynamic SQL 구문의 종류에 부합하는 수행 권한이 있어야 한다.

<a id="fe859984adaa01a5"></a>
### 구문 규칙 및 파라미터

<a id="d64c994cea473537"></a>
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

<a id="d0ab106d77dba6d1"></a>
#### variable_name

variable_name에 대응되는 type은 character string이어야 한다.   
variable_name에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="b6b1f77a6ebd48c4"></a>
#### sql statement

sql statement에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="7d89e6bd51fc2a90"></a>
### 설명

EXECUTE IMMEDIATE 'sql_string' 구문은 dynamic embedded SQL 응용 프로그램에서 host variable이 없는 non-query SQL에 사용될 수 있다. 별도의 준비과정이 필요하지 않기 때문에, DDL이나 DML 등을 일회성으로 수행하기에 적합하다.

자세한 내용은 [Embedded Dynamic SQL](../part-05-developer-manual/31-embedded-sql.md#bab9699b12f1bf0c)을 참조한다.

<a id="5ae7868f29efcfce"></a>
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

EXECUTE IMMEDIATE 'sql_string'이 사용된 전체 소스 코드는 [Dynamic Embedded SQL Example Program](../part-05-developer-manual/31-embedded-sql.md#039c8b6c9e7d5cad)에서 확인할 수 있다.

<a id="a765c36e9ec9ccd3"></a>
### 호환성

**SQL 표준 호환성**

<a id="704d2d0782c85c62"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |

<a id="d0948df05fc753e1"></a>
### 참조

관련 내용은 다음을 참조한다.

- [PREPARE statement_name](#80b37906c80e6402)
- [EXECUTE statement_name](#8174e55f7b6737f1)
- [Embedded Dynamic SQL](../part-05-developer-manual/31-embedded-sql.md#bab9699b12f1bf0c)

<a id="8174e55f7b6737f1"></a>
## EXECUTE statement_name

<a id="268c081efd576a9f"></a>
### 기능

준비된 statement를 수행한다.

<a id="4cb010ddec774945"></a>
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

<a id="4d3722af0b9905fc"></a>
### 사용 범위 및 접근 권한

Embedded SQL에서 사용할 수 있다.   
Dynamic SQL 구문의 종류에 부합하는 수행 권한이 있어야 한다.

<a id="016b161b0d1e2a55"></a>
### 구문 규칙 및 파라미터

<a id="0baa7e4af9d4cb20"></a>
#### statement_name

준비된 statement의 이름이다.  
[PREPARE statement_name](#80b37906c80e6402) 구문을 사용하여 statement_name을 준비해야 한다.

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

- [DECLARE cursor_name](#45b9d98474d5f09d)
- [OPEN cursor_name](#ee8cdd33c43f9c76)
- [FETCH cursor_name](#bafc38978b00122c)
- [CLOSE cursor_name](#38584f03f4e1823e)

질의 결과가 없을 경우, NO DATA로 완료된다.

<a id="a98712eee369f138"></a>
#### [ &lt;parameter using clause&gt; ] [ &lt;result into clause&gt; ]

&lt;parameter using clause&gt;와 &lt;result into clause&gt;는 순서에 관계없이 기술할 수 있지만 중복해서 기술하지 않아야 한다.

<a id="31332fbe019bfd6d"></a>
#### &lt;parameter using clause&gt;

statement_name이 참조하는 dynamic SQL 문장에 parameter가 존재할 경우, parameter에 대한 정보를 &lt;using parameter arguments&gt; 절로 명시한다.

<a id="52d0b235c2aa0ba1"></a>
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

<a id="13b1347e6bc0190b"></a>
#### &lt;result into clause&gt;

statement_name이 참조하는 dynamic SQL 문장이 query일 경우, 결과 column에 대한 정보를 &lt;into result arguments&gt; 절로 명시한다.

결과값이 null인 경우, INDICATOR를 명시하지 않으면 [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] 에러가 발생한다.

<a id="b516e4b384f39da3"></a>
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

<a id="cd0fc04dc6707333"></a>
### 설명

statement_name은 embedded SQL 소스 코드에서 precompiler에게 statement를 알려주는 식별자로써 host variable이 아니기 때문에 별도의 type이나 선언이 필요하지 않다. EXECUTE statement_name 구문은 PREPARE statement_name 구문 뒤에 쓰여야 한다.

자세한 내용은 [Embedded Dynamic SQL](../part-05-developer-manual/31-embedded-sql.md#bab9699b12f1bf0c)을 참조한다.

<a id="8067ae9e7b148182"></a>
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

EXECUTE statement_name이 사용된 전체 소스 코드는 [Dynamic Embedded SQL Example Program](../part-05-developer-manual/31-embedded-sql.md#039c8b6c9e7d5cad)에서 확인할 수 있다.

<a id="3b142bddfc9e95c6"></a>
### 호환성

**SQL 표준 호환성**

<a id="f769f3a96d5eb259"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic dynamic SQL | O |
| B032 | Extended dynamic SQL | X |

<a id="684ab0a3ad24bbeb"></a>
### 참조

관련 내용은 다음을 참조한다.

- [PREPARE statement_name](#80b37906c80e6402)
- [DECLARE cursor_name](#45b9d98474d5f09d)
- [OPEN cursor_name](#ee8cdd33c43f9c76)
- [FETCH cursor_name](#bafc38978b00122c)
- [CLOSE cursor_name](#38584f03f4e1823e)
- [Embedded Dynamic SQL](../part-05-developer-manual/31-embedded-sql.md#bab9699b12f1bf0c)

<a id="bafc38978b00122c"></a>
## FETCH cursor_name

<a id="62e2dfb8cb1c2e5c"></a>
### 기능

커서를 결과 집합의 특정 row에 위치시키고, 해당 row의 값을 호스트 변수에 얻어온다.

<a id="2d800bc0a04f7a09"></a>
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

<a id="6833137256790eba"></a>
### 구문 규칙 및 파라미터

<a id="abec53b4a8f52955"></a>
#### [ FROM ] cursor_name

세션 내에서 open 된 커서이어야 한다.   
FROM은 생략할 수 있다.

<a id="7fa7ed8620fd06ca"></a>
#### &lt;fetch orientation&gt;

FETCH NEXT 이외의 &lt;fetch orientation&gt;을 사용하려면 scrollable cursor를 사용해야 한다.   
&lt;fetch orientation&gt;을 생략할 경우, 기본값은 NEXT이다.

Open 된 커서는 결과 집합에 대해 아래 그림과 같은 커서 위치 정보를 갖는다.

<a id="1bcb6fc5f31a9872"></a>
![커서의 위치 정보](../assets/images/f2e882d0a60b3aa8.png)

**커서의 위치**

<a id="a7191e9bc2f062d3"></a>
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

<a id="e336afd0b9c4b9d0"></a>
#### &lt;result into clause&gt;

&lt;into result arguments&gt;를 사용하여 결과 column을 획득할 변수 정보를 기술한다.

결과값이 null 인 경우, INDICATOR를 명시하지 않으면 [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] 에러가 발생한다.

<a id="ad52da43bf6f048d"></a>
#### &lt;into result arguments&gt;

INTO 절에 기술된 변수의 개수는 커서의 결과 집합의 column 개수와 동일해야 한다.

<a id="4a3e87c14fb41322"></a>
### 설명

FETCH를 수행한 후에 커서 위치가 BEFORE THE FIRST ROW 거나 AFTER THE LAST LOW 인 경우, &lt;fetch orientation&gt;에 입력된 위치값에 관계없이 동일한 위치에 자리한다.

<a id="c47fc0271bbbb5f6"></a>
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

<a id="0adb8db89c641d90"></a>
### 호환성

SQL 표준에서는 &lt;fetch orientation&gt; 중에 CURRENT를 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="b49d1085b9ee0e7f"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F431 | Read-only scrollable cursors | O |
| B031 | Basic dynamic SQL | O |

<a id="75cc1fae5a6f7fff"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#45b9d98474d5f09d)
- [OPEN cursor_name](#ee8cdd33c43f9c76)
- [CLOSE cursor_name](#38584f03f4e1823e)

<a id="68eab71c0033b21e"></a>
## FLASHBACK TABLE

<a id="d9a2168567da519f"></a>
### 기능

휴지통에 보관되어 있는 테이블 객체를 복구한다.

<a id="4a335aaf645fcbb2"></a>
### 구문

```
<flashback table statement> ::=
    FLASHBACK TABLE table_name
    TO BEFORE DROP [ RENAME TO new_table_name ]
    ;
```

<a id="9f9efabee7f1af83"></a>
### 사용 범위 및 접근 권한

&lt;flashback table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블의 소유자 
- 해당 테이블에 대해 CONTROL TABLE ON TABLE 
- 테이블이 속한 스키마에 대해 (DROP TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY TABLE ON DATABASE

<a id="47798b1edf97dff0"></a>
### 구문 규칙 및 파라미터

<a id="7d839c7fe5c2d745"></a>
#### table_name

휴지통에 저장된 객체의 이름 또는 제거된 테이블의 이름이다.  
제거된 테이블 이름에는 schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있으며 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="4bb8f8f4d2a39fc3"></a>
#### new_table_name

복구되는 테이블의 새로운 이름이다.  
스키마 내에 동일한 테이블 이름이 존재하지 않아야 한다.

<a id="2712d8e54955e37d"></a>
### 설명

휴지통에 저장된 객체 이름이나 제거된 테이블의 이름을 사용하여 휴지통에 보관되어 있는 테이블 객체를 복구한다. 만약 제거된 테이블과 중복된 이름이 있는 경우 가장 최신의 테이블 객체를 복구한다.

복구하려는 테이블 객체의 이름이 존재하면 에러가 발생하는데 RENAME TO 절을 사용하여 새로운 테이블 이름으로 복구할 수 있다. 복구된 테이블의 제약 조건과 인덱스는 제거되기 전의 이름으로 복구되는데 만약 제거되기 전의 제약 조건 및 인덱스와 동일한 이름이 이미 존재할 경우, 휴지통에 저장된 이름으로 복구된다.

다른 Data Definition Language (DDL)과 달리 FLASHBACK TABLE 구문은 ROLLBACK 할 수 없으며, 구문을 수행한 transaction이 자동으로 COMMIT 된다.

<a id="b33ff173e771bbb4"></a>
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

<a id="87701edfc2ea4d7d"></a>
### 호환성

SQL 표준에서는 &lt;flashback table statement&gt;를 다루지 않고 있다.

<a id="238a051497659364"></a>
### 참조

관련 내용은 다음을 참조한다.

- [테이블의 휴지통 관리](13-sql-objects.md#16ee3ebcea216f4f)
- [PURGE](#79aef06d7d731846)

<a id="81c5198ff0096dcc"></a>
## GRANT privileges TO

<a id="29f5097f551a1c9e"></a>
### 기능

사용자에게 권한을 부여한다.

<a id="529d77ec54f5c118"></a>
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

<a id="08a7b446ca155ea8"></a>
### 구문 규칙 및 파라미터

<a id="eec39786d8cf8d6e"></a>
#### &lt;grantee&gt;

권한을 부여받을 사용자이다.

- user_identifier 
    - 해당 사용자에게 권한을 부여한다
- PUBLIC 
    - 모든 사용자를 의미하는 authorization 객체이다.

<a id="99f0ecea8afe067b"></a>
#### WITH GRANT OPTION

Grantee (권한을 부여받은 사용자)가 다른 사용자에게 해당 권한을 부여할 수 있도록 한다.

다음과 같이 동일한 &lt;privilege&gt;에 대한 권한을 부여할 때 WITH GRANT OPTION은 계속 유지된다.

- GRANT SELECT ON t1 TO u1 WITH GRANT OPTION; 
- GRANT SELECT ON t1 TO u1;

<a id="a61c0ddbefa20757"></a>
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

<a id="0813e2a457c183b8"></a>
#### &lt;database privilege&gt;

데이터베이스 객체에 대한 권한이다.  
[ON DATABASE] 구문은 생략할 수 있다.

database privilege로 정의할 수 있는 database action은 다음과 같다.

- ALL [ PRIVILEGES ] [ON DATABASE] 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 DATABASE에 대해 소유한 모든 권한이다.

**Database privilege**

<a id="66db0b79ade34d1f"></a>
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
| PURGE DBA_RECYCLEBIN | Database의 모든 휴지통을 제거할 수 있는 권한 |

<a id="6d0298372e1d6e5d"></a>
#### &lt;tablespace privilege&gt;

테이블스페이스 객체에 대한 권한이다.

tablespace privilege로 정의할 수 있는 tablespace action은 다음과 같다.

- ALL [ PRIVILEGES ] ON TABLESPACE tablespace_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 TABLESPACE에 대해 소유한 모든 권한이다.

**Tablespace privilege**

<a id="f026d2a4d3049ba7"></a>
| &lt;tablespace action&gt; | 설명 |
| --- | --- |
| CREATE OBJECT | Tablespace에 객체를 생성할 수 있는 권한 |

<a id="a966ecd031ab1081"></a>
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

<a id="ed4c7f80b9aea75b"></a>
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

<a id="8e4126f97ea2eda4"></a>
#### &lt;table privilege&gt;

테이블 또는 view 객체에 대한 권한이다.  
[TABLE] 구문은 생략할 수 있다.

table privilege로 정의할 수 있는 table action은 다음과 같다.

- ALL [ PRIVILEGES ] ON [TABLE] table_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 TABLE에 대해 소유한 모든 권한이다.

**Table privilege**

<a id="3202322975b0b05a"></a>
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

<a id="af1ba097ff33dd40"></a>
| &lt;column action&gt; | 설명 |
| --- | --- |
| SELECT (columns) | 해당 column들을 검색할 수 있는 권한 |
| INSERT (columns) | 해당 column들을 포함한 row를 생성할 수 있는 권한 |
| UPDATE (columns) | 해당 column들을 갱신할 수 있는 권한 |
| REFERENCES (columns) | 해당 column들을 참조하는 참조 제약 조건을 생성할 수 있는 권한 |

<a id="3dc09e0d99924ed3"></a>
#### &lt;sequence privilege&gt;

시퀀스 객체에 대한 권한이다.

sequence privilege로 정의할 수 있는 sequence action은 다음과 같다.

- ALL [ PRIVILEGES ] ON SEQUENCE sequence_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 SEQUENCE에 대해 소유한 모든 권한이다.

**Sequence privilege**

<a id="953d36236a3d2e3b"></a>
| &lt;sequence action&gt; | 설명 |
| --- | --- |
| USAGE | 시퀀스를 사용할 수 있는 권한 |

<a id="092315b848b2a81c"></a>
#### &lt;procedure privilege&gt;

Procedure/ function 객체에 대한 권한이다.

procedure privilege로 정의할 수 있는 action은 다음과 같다.

- ALL [ PRIVILEGES ] ON PROCEDURE procedure_name 
    - Grantor (구문을 수행하는 사용자)가 WITH GRANT OPTION을 사용하여 해당 procedure/ function에 대해 소유한 모든 권한이다.

**Procedure privilege**

<a id="f99a7b15dde883a8"></a>
| &lt;procedure action&gt; | 설명 |
| --- | --- |
| EXECUTE | Procedure/ function을 실행할 수 있는 권한 |

<a id="9075945dffa1306c"></a>
### 설명

GRANT privilege와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

Table, sequence 등과 같은 SQL schema object를 생성한 owner는 해당 객체에 대한 권한을 별도로 부여받지 않더라도 일정한 권한을 가진다.   
이에 대한 자세한 설명은 다음과 같은 CREATE 구문을 참조한다.

- [CREATE TABLE](#9b82da6d66aabe8c)
- [CREATE VIEW](#a71e7cc52f1eefb4)
- [CREATE SEQUENCE](#2eb16f80ff00b702)
- [ALTER TABLE name ADD COLUMN](#435e25d60c5f411d)
- [CREATE FUNCTION](../part-04-psm-manual/27-psm-sql-references.md#243dff1382985279)
- [CREATE PROCEDURE](../part-04-psm-manual/27-psm-sql-references.md#e2d083dd25c36aa9)

Schema, tablespace 등과 같은 non-schema object를 생성한 owner에는 해당 객체에 대한 어떤 권한도 자동으로 부여되지 않으므로 별도의 권한을 부여받아야 한다.   
자세한 설명은 다음과 같은 CREATE 구문을 참조한다.

- [CREATE SCHEMA](#587f9a1c3687c699)
- [CREATE TABLESPACE](#53b7fdb5c5a23059)
- [CREATE USER](#8e5920c927752802)

<a id="7d6b5a5c1276e649"></a>
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

<a id="068856661a8bc265"></a>
### 호환성

SQL 표준에서는 다음 privilege들을 정의하지 않고 있다.

- &lt;database privilege&gt; 
- &lt;tablespace privilege&gt; 
- &lt;schema privilege&gt;

**SQL 표준 호환성**

<a id="2d3dafb9bc19d609"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| S023 | Basic structured types | X |
| S024 | Enhanced structured types | X |
| S081 | Subtables | X |
| T211 | Basic trigger capability | X |
| T281 | SELECT privilege with column granularity | O |
| T332 | Extended Roles | X |
| F731 | INSERT column privileges | O |

<a id="e0233d225dc7f8c6"></a>
### 참조

관련 내용은 다음을 참조한다.

- [REVOKE privileges FROM](#e3a10d989cb175f3)
- [CREATE USER](#8e5920c927752802)
- [DROP USER](#886267e56d7bc6a6)
- [ALTER USER](#268a4621fc85878c)

<a id="f7aecaaad34d188f"></a>
## INSERT INTO

<a id="835046348a3fac5a"></a>
### 기능

테이블에 새로운 row들을 생성한다.

<a id="895f01282f650369"></a>
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

<a id="5d2427e2b5d943cd"></a>
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

<a id="78ec3edc472fe231"></a>
### 구문 규칙 및 파라미터

<a id="1ff641fd851c5faf"></a>
#### table_name

Row를 생성할 대상 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="1879939d41c71ff7"></a>
#### [ ( column_name [, ...] ) ]

테이블의 column 이름이다.   
Column 리스트는 생략할 수 있다.   
Column의 개수와 &lt;insert source&gt; 값의 개수는 동일해야 하며, 생략된 column에는 DEFAULT 값을 할당한다.

<a id="41490b4379a7c7c3"></a>
#### &lt;values clause&gt;

대응하는 column에 할당할 값의 리스트이다.

- &lt;value expression&gt; 
    - 대응하는 column에 할당할 값이나 연산식이다. 
- DEFAULT 
    - 대응하는 column의 값은 [CREATE TABLE](#9b82da6d66aabe8c) 구문을 통해 정의한 기본값을 사용한다. 
    - 정의하지 않았을 경우 NULL 값이 할당된다.

다음과 같이 다수의 row를 생성할 수 있다.

```
INSERT INTO table_name VALUES ( 1, 'A' ), ( 2, 'B' ), ( 3, 'C' )
```

<a id="1cf1a169fed092bb"></a>
#### &lt;from subquery&gt;

Row들을 생성할 질의이다.  
자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 [query expression](#83a1bf13756be069) 절을 참조한다.

<a id="211c7bd397bb7f91"></a>
#### DEFAULT VALUES

모든 column들을 기본값으로 채운다.

DEFAULT VALUES 절은 다음과 같은 의미이다.

```
VALUES ( DEFAULT, DEFAULT, ..., DEFAULT )
```

<a id="348b766e9941fcf0"></a>
### 설명

<a id="922629d68f4a6506"></a>
#### INSERT 관련 구문들의 차이점

- [INSERT INTO](#f7aecaaad34d188f)
    - 테이블에 하나 또는 다수의 row를 생성한다. 
    - 예: INSERT INTO t1 SELECT * FROM t1; 
- [INSERT INTO name RETURNING](#71ce6ee2aa40a318)
    - 테이블에 하나 또는 다수의 row를 생성하고, 생성한 row들을 SELECT 구문과 동일한 방식 (SQLFetch() 등의 API)으로 검색할 수 있다. 
    - 예: INSERT INTO t1 SELECT * FROM t1 RETURNING c1; 
- [INSERT INTO name RETURNING .. INTO](#52c48e84ccf07d95)
    - 한 건 이하의 row를 생성할 수 있으며, 생성한 row가 한 건일 경우 RETURNING INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: INSERT INTO t1 DEFAULT VALUES RETURNING c1 INTO :v1;

<a id="027b4d2a50992e84"></a>
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

<a id="13d7a572cfdb1f91"></a>
### 호환성

**SQL 표준 호환성**

<a id="7d867aab80f37c70"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| F222 | INSERT statement: DEFAULT VALUES clause | O |
| S204 | Enhanced structured types | X |
| S043 | Enhanced reference types | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="88a027f07e4f567d"></a>
### 참조

관련 내용은 다음을 참조한다.

- [SELECT](#93101dc44f4e210d)
- [INSERT INTO name RETURNING](#71ce6ee2aa40a318)
- [INSERT INTO name RETURNING .. INTO](#52c48e84ccf07d95)

<a id="71ce6ee2aa40a318"></a>
## INSERT INTO name RETURNING

<a id="5c237d23847c0570"></a>
### 기능

테이블에 새로운 row를 생성하고, 생성한 row들을 검색한다.

<a id="05fbb1aa069123b2"></a>
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

<a id="3bf439f6d21ee359"></a>
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

<a id="e5afea47238fe3ac"></a>
### 구문 규칙 및 파라미터

<a id="60e2b17819324928"></a>
#### table_name

Row를 생성할 대상 테이블의 이름이다.

<a id="b631f64c6744b831"></a>
#### [ ( column_name [, ...] ) ]

테이블의 column 이름이다.  
자세한 내용은 [INSERT INTO](#f7aecaaad34d188f) 구문을 참조한다.

<a id="9df9a415adcdd503"></a>
#### &lt;values clause&gt;

대응하는 column에 할당할 값의 리스트이다.  
자세한 내용은 [INSERT INTO](#f7aecaaad34d188f) 구문을 참조한다.

<a id="d8de9d4c8d7196c8"></a>
#### &lt;from subquery&gt;

Row들을 생성할 질의이다.  
자세한 내용은 [INSERT INTO](#f7aecaaad34d188f) 구문을 참조한다.

<a id="4d4d3fc5b301c7b8"></a>
#### DEFAULT VALUES

모든 column들을 기본값으로 채운다.   
자세한 내용은 [INSERT INTO](#f7aecaaad34d188f) 구문을 참조한다.

<a id="2167b5e89e42da73"></a>
#### &lt;returning clause&gt;

INSERT 된 row들을 반환한다.

- 생성된 row들을 결과 집합으로 하고, 이들 중 검색할 column을 기술한다. 
    - RETURNING 절은 INSERT 구문으로 삽입된 row들을 결과 집합으로 하는 결과를 반환한다. 
    - &lt;value expression&gt; 
        - SELECT 구문의 &lt;select list&gt;와 동일하지만 aggregation 등을 사용할 수 없다. 
    - [[AS] alias_name] 
        - AS 절을 사용하여 value expression의 이름을 지정할 수 있다.

RETURN과 RETURNING은 동일한 의미의 키워드이다.

<a id="f1ddaa19dd043bbf"></a>
### 설명

자세한 내용은 [INSERT 관련 구문들의 차이점](#922629d68f4a6506)을 참조한다.

<a id="f95cfbe49f868184"></a>
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

<a id="828d3cb6b1105678"></a>
### 호환성

SQL 표준에서는 &lt;insert returning query statement&gt; 구문을 정의하지 않고 있다.

<a id="b3827a64fb958269"></a>
### 참조

관련 내용은 다음을 참조한다.

- [INSERT INTO](#f7aecaaad34d188f)
- [INSERT INTO name RETURNING .. INTO](#52c48e84ccf07d95)

<a id="52c48e84ccf07d95"></a>
## INSERT INTO name RETURNING .. INTO

<a id="f5b1d7654a64fb53"></a>
### 기능

테이블에 row 하나를 생성하고, 생성한 row의 값을 호스트 변수에 얻어온다.

<a id="5723b3d13939c0ce"></a>
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

<a id="74fbbc6d01c73d4a"></a>
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

<a id="a02de91ace5711d0"></a>
### 구문 규칙 및 파라미터

<a id="2cd43eecda374921"></a>
#### table_name

Row를 생성할 대상 테이블의 이름이다.

<a id="c8d3efbbca057be0"></a>
#### [ ( column_name [, ...] ) ]

테이블의 column 이름이다.  
자세한 내용은 [INSERT INTO](#f7aecaaad34d188f) 구문을 참조한다.

<a id="76b45850a49e9ccf"></a>
#### &lt;values clause&gt;

대응하는 column에 할당할 값의 리스트이다.  
자세한 내용은 [INSERT INTO](#f7aecaaad34d188f) 구문을 참조한다.

<a id="319990f25b1f3383"></a>
#### &lt;from subquery&gt;

Row들을 생성할 질의이다.  
자세한 내용은 [INSERT INTO](#f7aecaaad34d188f) 구문을 참조한다.

<a id="37cc9289080b2b6e"></a>
#### DEFAULT VALUES

모든 column들을 기본값으로 채운다.  
자세한 내용은 [INSERT INTO](#f7aecaaad34d188f) 구문을 참조한다.

<a id="a456ba2c03495f25"></a>
#### &lt;returning clause&gt;

INSERT 된 row를 반환한다.  
[INSERT INTO name RETURNING](#71ce6ee2aa40a318) 구문의 &lt;[returning clause&gt;](#2167b5e89e42da73) 절을 참조한다.

<a id="1c6a019d7f3933fe"></a>
##### INTO variable_name [, ...]

INTO 절에 기술된 변수의 개수는 RETURNING 절에 기술된 expression의 개수와 동일해야 한다.   
생성할 row가 한 건 이하여야 한다. Row가 두 건 이상 생성될 경우, 에러가 발생한다.

<a id="24dc06ca5f04667e"></a>
### 설명

자세한 내용은 [INSERT 관련 구문들의 차이점](#922629d68f4a6506)을 참조한다.

<a id="1d1a286a398ab1c1"></a>
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

<a id="301af6bfceab170b"></a>
### 호환성

SQL 표준은 &lt;insert returning into statement&gt; 구문을 정의하지 않고 있다.

<a id="5d109877e27c0747"></a>
### 참조

관련 내용은 다음을 참조한다.

- [INSERT INTO](#f7aecaaad34d188f)
- [INSERT INTO name RETURNING](#71ce6ee2aa40a318)

<a id="b16d2620c2af8fbf"></a>
## LOCK TABLE

<a id="a71d32b517326c4e"></a>
### 기능

하나 이상의 테이블에 lock을 설정한다.

<a id="f19c716413f5f022"></a>
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

<a id="7301701e277970aa"></a>
### 사용 범위 및 접근 권한

&lt;lock table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블에 대해 (LOCK 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (LOCK TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- LOCK ANY TABLE ON DATABASE

<a id="55480525121c3f35"></a>
### 구문 규칙 및 파라미터

<a id="c21f7646ce27cb4d"></a>
#### &lt;lock target&gt;

LOCK 대상 테이블을 명시한다.

<a id="5f91efba12a33c3f"></a>
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

<a id="0bf02bf28c44e245"></a>
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

<a id="0a13f5ac1208e0dc"></a>
### 설명

Transaction을 COMMIT 하거나 ROLLBACK 할 경우 획득한 모든 lock은 자동으로 해제된다. ROLLBACK TO SAVEPOINT 구문을 사용할 경우 해당 savepoint 이후에 획득한 모든 lock이 해제된다.

<a id="cb3567a3f88e0c13"></a>
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

<a id="73e07ab777fb59cc"></a>
### 호환성

SQL 표준은 lock table에 대한 개념을 다루지 않고 있다.

<a id="fa470cf6218b9f91"></a>
### 참조

관련 내용은 다음을 참조한다.

- [COMMIT](#4d322680eba93c4a)
- [ROLLBACK](#eaa6143895b543a3)

<a id="f4896aa89ec963af"></a>
## NOAUDIT POLICY

<a id="abddf5cd83aae34c"></a>
### 기능

Audit policy를 비활성화한다.

<a id="e71dc6fa792c3158"></a>
### 구문

```
<noaudit policy statement> ::= 
    NOAUDIT POLICY policy_name
    [ <specified_user_option> ]
    ;

<specified_user_option> ::=
      BY user_name [, ...]
```

<a id="2a47c235a03ce4b7"></a>
### 사용 범위 및 접근 권한

&lt;noaudit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="d58ef76431d3ca27"></a>
### 구문 규칙 및 파라미터

<a id="1cc4707c413faa6f"></a>
#### policy_name

비활성화할 audit policy 객체의 이름이다.   
비활성화 된 audit policy는 기존 session에 영향을 미치지 않으며 새로 생성되는 session에만 영향을 준다.

<a id="c17bfde71e1cbe83"></a>
#### &lt;specified_user_option&gt;

감사 대상에서 제외할 사용자를 명시한다.

AUDIT POLICY 구문과 달리 NOAUDIT POLICY 구문에는 EXCEPT 옵션이 없다.

AUDIT POLICY name BY 절을 사용한 경우 NOAUDIT POLICY name BY 구문으로 비활성화하며   
AUDIT POLICY name EXCEPT 절을 사용한 경우 BY 절 없이 NOAUDIT POLICY name 구문으로 비활성화해야 한다.

AUDIT POLICY 구문의 사용 방법에 따라 다음과 같이 NOAUDIT POLICY 구문을 사용하여 해당 옵션을 비활성화해야 한다.

**Audit policy 활성화/ 비활성화**

<a id="72b01fad2d1df593"></a>
| 유형 | AUDIT POLICY 구문 | NOAUDIT POLICY 구문 |
| --- | --- | --- |
| 전체 사용자 | AUDIT POLICY p1 | NOAUDIT POLICY p1 |
| BY를 사용 | AUDIT POLICY p1 BY u1 | NOAUDIT POLICY p1 BY u1 |
| EXCEPT를 사용 | AUDIT POLICY p1 EXCEPT u1 | NOAUDIT POLICY p1 |

활성화된 모든 user들을 비활성화한 경우, audit policy 객체가 완전히 비활성화된다.

<a id="cd5a032d59a709d5"></a>
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

<a id="3b9e35c0840a3bf2"></a>
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

<a id="750ded33843a8863"></a>
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

<a id="518e519a60f0b1bb"></a>
### 사용 예

다음은 전체 사용자를 비활성화한 예이다.

```
NOAUDIT POLICY table_pol;
```

다음은 BY를 사용하여 활성화된 특정 사용자를 비활성화하는 예이다.

```
NOAUDIT POLICY table_pol BY u1;
```

<a id="c1dd92e7cfbc1b24"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="c950db8cfef2e341"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](#09b3895daf4991da)
    - [DROP AUDIT POLICY](#4c985d8424a9c9e1)
    - [ALTER AUDIT POLICY](#241fd4b15c525c5a)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](#8c7812c0671b6a25)
    - [NOAUDIT POLICY](#f4896aa89ec963af)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#6c787a4b953e8625)

- Audit trail 제거: [ALTER DATABASE CLEAR AUDIT TRAIL](#d0a56f6310b7a28c)

<a id="ee8cdd33c43f9c76"></a>
## OPEN cursor_name

<a id="9c369c3bacf5e206"></a>
### 기능

커서를 연다.

<a id="b72807788584d7ee"></a>
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

<a id="fc1ac3c1a4c560c1"></a>
### 사용 범위 및 접근 권한

cursor_name이 [PREPARE statement_name](#80b37906c80e6402) 구문과 [DECLARE cursor_name](#45b9d98474d5f09d) 구문을 사용해 선언한 동적 커서인 경우 embedded SQL에서 사용 가능하다.

cursor_name을 선언한 [DECLARE cursor_name](#45b9d98474d5f09d) 구문에 포함된 &lt;[cursor query&gt;](#64ab907686666d41)의 권한과 동일하다.

<a id="ef352ebfe637bb3a"></a>
### 구문 규칙 및 파라미터

<a id="8f0319ae5a9396dd"></a>
#### cursor_name

세션 내에서 [DECLARE cursor_name](#45b9d98474d5f09d) 구문으로 선언된 커서이어야 한다.

<a id="92984377c32226ce"></a>
#### &lt;parameter using clause&gt;

Embedded SQL에서 사용할 수 있다.

&lt;parameter using clause&gt; 구문이 사용될 경우, cursor_name이 [PREPARE statement_name](#80b37906c80e6402) 구문과 [DECLARE cursor_name](#45b9d98474d5f09d) 구문을 이용해 선언한 동적 커서여야 한다.

<a id="8a70ecff097bb010"></a>
#### &lt;using parameter arguments&gt;

&lt;using parameter arguments&gt; 구문이 사용될 경우, variable_name의 개수는 [PREPARE statement_name](#80b37906c80e6402) 구문이 참조하는 query 문장에 포함된 parameter의 개수와 동일해야 한다.

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

<a id="1bcb6204e7e456ae"></a>
### 설명

Cursor는 session 내에서 구별되는 객체이며, 현재 session 내에서 사용되고 있는 cursor는 다른 session에서 사용되고 있는 cursor와 무관하다.

OPEN cursor_name 구문을 사용하려면 [DECLARE cursor_name](#45b9d98474d5f09d) 구문으로 선언된 커서여야 하며, 커서는 닫혀 있는 상태여야 한다.

<a id="4ed9b0229a87c4f3"></a>
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

<a id="86a2ed668b78546a"></a>
### 호환성

**SQL 표준 호환성**

<a id="783ea3bfe65608d3"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic dynamic SQL | O |

<a id="5c287a3813c98789"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](#45b9d98474d5f09d)
- [FETCH cursor_name](#bafc38978b00122c)
- [CLOSE cursor_name](#38584f03f4e1823e)
- [PREPARE statement_name](#80b37906c80e6402)

<a id="80b37906c80e6402"></a>
## PREPARE statement_name

<a id="02d66ee0f9053134"></a>
### 기능

반복 수행을 위한 dynamic SQL 문장을 준비한다.

<a id="041b9a9d2fd04ce7"></a>
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

<a id="67b7bd818c0405b3"></a>
### 사용 범위 및 접근 권한

Embedded SQL에서 사용할 수 있다.  
Dynamic SQL 구문의 종류에 부합하는 수행 권한이 있어야 한다.

<a id="e70b691add8132ad"></a>
### 구문 규칙 및 파라미터

<a id="5285ddf65c3f0b72"></a>
#### statement_name

준비할 statement의 이름이다.  
statement 이름의 길이는 128 바이트보다 작아야 한다.  
이후에 수행될 [EXECUTE statement_name](#8174e55f7b6737f1) 구문 또는 [DECLARE cursor_name](#45b9d98474d5f09d) 구문은 statement_name을 참조한다.  
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

<a id="b3bb3ea6bf548b7d"></a>
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
        - input dynamic parameter 
        - :sValue1 값을 사용한다. 
    - 2번 - AND ? 
        - input dynamic parameter 
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

- input dynamic parameter와 output dynamic parameter가 존재한다. 
- 식별 순서 
    - 1번 - :v1 
        - output dynamic parameter 
        - :sValue1에 값이 저장된다. 
    - 2번 - :v2 
        - input dynamic parameter 
        - :sValue2 값을 사용한다.

<a id="2fecc78beccc48c7"></a>
#### variable_name

variable_name에 대응하는 type은 character string이어야 한다.   
variable_name에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="a553b900a5efc4c7"></a>
#### sql statement

sql statement에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="e221b706e13b5691"></a>
### 설명

PREPARE statement_name FROM sql_string 구문은 EXECUTE나 cursor를 사용하기 위해 SQL 문을 분석한다. statement_name은 embedded SQL 소스 코드에서 precompiler에게 statement를 알려주는 식별자로써 host variable이 아니기 때문에 별도의 type이나 선언이 필요하지 않다.

자세한 내용은 [Embedded Dynamic SQL](../part-05-developer-manual/31-embedded-sql.md#bab9699b12f1bf0c)을 참조한다.

<a id="7c1fac8aa6887cc6"></a>
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

PREPARE statement_name이 사용된 전체 소스 코드는 [Dynamic Embedded SQL Example Program](../part-05-developer-manual/31-embedded-sql.md#039c8b6c9e7d5cad)에서 확인할 수 있다.

<a id="5ae8e1ee251d0a24"></a>
### 호환성

**SQL 표준 호환성**

<a id="093b2cbf36551048"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |
| B034 | Dynamic specification of cursor attributes | X |

<a id="c0b107d868a71b9a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [EXECUTE statement_name](#8174e55f7b6737f1)
- [DECLARE cursor_name](#45b9d98474d5f09d)
- [EXECUTE IMMEDIATE 'sql_string'](#6884ae114f6016e7)
- [Embedded Dynamic SQL](../part-05-developer-manual/31-embedded-sql.md#bab9699b12f1bf0c)

<a id="79aef06d7d731846"></a>
## PURGE

<a id="de84c78558908255"></a>
### 기능

휴지통에 저장되어 있는 객체들을 영구적으로 제거한다.

<a id="08b072d99d7579df"></a>
### 구문

```
<purge statement> :==
    PURGE <purge action>
    ;

<purge action> :==
     TABLE table_name
   | INDEX index_name
   | CONSTRAINT constraint_name
   | TABLESPACE tablespace_name [ USER user_name ]
   | RECYCLEBIN 
   | USER_RECYCLEBIN
   | DBA_RECYCLEBIN
```

<a id="7b8b8876ae368db4"></a>
### 사용 범위 및 접근 권한

&lt;purge statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블의 소유자 
- 해당 테이블에 대해 CONTROL TABLE ON TABLE 
- 테이블이 속한 스키마에 대해 (DROP TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY TABLE ON DATABASE

<a id="020ec88011f65922"></a>
### 구문 규칙 및 파라미터

<a id="5c9953b9fd2a0238"></a>
#### table_name

휴지통에 저장된 객체 이름 또는 제거된 테이블의 이름이다.  
제거된 테이블의 이름에는 schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
테이블과 관련된 인덱스와 제약 조건들도 함께 제거된다.

<a id="9586029e906baf20"></a>
#### index_name

휴지통에 저장된 객체 이름 또는 제거된 인덱스의 이름이다.  
schema_name.index_name과 같이 인덱스가 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
제약 조건으로 생성된 key 인덱스는 제약 조건으로 삭제해야 한다.

<a id="a8efabef1d069718"></a>
#### constraint_name

휴지통에 저장된 객체 이름 또는 삭제된 제약 조건의 이름이다.

<a id="b0417e9aa1ec2a8c"></a>
#### tablespace_name

테이블스페이스의 이름이다.  
USER를 지정할 때는 DROP ANY TABLE ON DATABASE 권한이 필요하다.

<a id="d27a7bf508f602a2"></a>
#### user_name

사용자의 이름이다.

<a id="9c831990b923a269"></a>
#### recyclebin

user_recyclebin의 alias 이다.

<a id="3c26a15bb1bafcfa"></a>
#### user_recyclebin

사용자가 소유한 휴지통을 모두 제거한다.

<a id="e982d68aebd5d3a2"></a>
#### dba_recyclebin

데이터베이스의 모든 휴지통을 제거한다.  
PURGE DBA_RECYCLEBIN ON DATABASE 권한이 필요하다.

<a id="c7bd49b7385f7a58"></a>
### 설명

휴지통에 저장된 객체 이름이나 제거된 테이블의 이름을 사용하여 휴지통에 보관되어 있는 객체들을 영구적으로 제거한다. 만약 제거 대상 테이블과 동일한 이름의 테이블이 있는 경우, 가장 오래된 객체를 제거한다.

사용자가 소유한 휴지통 객체에서 테이블스페이스를 지정하여 테이블스페이스에 포함된 객체들을 제거할 수 있는데 이 때 사용자를 지정하면 해당 사용자의 명시된 테이블스페이스에 포함된 객체들만 제거할 수 있다.

PURGE TABLE, INDEX, CONSTRAINT 구문은 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다. 반면 PURGE TABLESPACE, RECYCLEBIN, DBA_RECYCLEBIN 구문은 ROLLBACK 할 수 없으며, 구문을 수행한 트랜잭션이 자동으로 COMMIT 된다.

<a id="00ca32989143d2aa"></a>
### 사용 예

다음은 휴지통에 저장된 테이블을 제거하는 예이다.

```
gSQL> SELECT OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

OBJECT_NAME                          ORIGINAL_NAME        OBJECT_TYPE
------------------------------------ -------------------- -----------
BIN$135B9908166111EA9C5C835D3E4BBBF7 T1                   TABLE      
BIN$135B993A166111EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY       CONSTRAINT 
BIN$135B991C166111EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY_INDEX INDEX      
BIN$135B9926166111EA9C5C835D3E4BBBF7 T1_IDX1              INDEX      

4 rows selected.

gSQL> PURGE TABLE t1;

Table purged.
```

다음은 휴지통에 저장된 인덱스를 제거하는 예이다.

```
gSQL> SELECT OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

OBJECT_NAME                          ORIGINAL_NAME        OBJECT_TYPE
------------------------------------ -------------------- -----------
BIN$135B9908166111EA9C5C835D3E4BBBF7 T1                   TABLE      
BIN$135B993A166111EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY       CONSTRAINT 
BIN$135B991C166111EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY_INDEX INDEX      
BIN$135B9926166111EA9C5C835D3E4BBBF7 T1_IDX1              INDEX      

4 rows selected.

gSQL> PURGE INDEX t1_idx1;

Index purged.
```

다음은 휴지통에 저장된 제약 조건을 제거하는 예이다.

```
gSQL> SELECT OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

OBJECT_NAME                          ORIGINAL_NAME        OBJECT_TYPE
------------------------------------ -------------------- -----------
BIN$135B9908166111EA9C5C835D3E4BBBF7 T1                   TABLE      
BIN$135B993A166111EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY       CONSTRAINT 
BIN$135B991C166111EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY_INDEX INDEX      

3 rows selected.

gSQL> PURGE CONSTRAINT t1_primary_key;

Constraints purged.
```

다음은 휴지통에 저장된 테이블스페이스에 포함된 객체들을 제거하는 예이다.

```
gSQL> SELECT OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE, TABLESPACE_NAME FROM USER_RECYCLEBIN;

OBJECT_NAME                          ORIGINAL_NAME OBJECT_TYPE TABLESPACE_NAME
------------------------------------ ------------- ----------- ---------------
BIN$02C76B24166311EA9C5C835D3E4BBBF7 T1            TABLE       MEM_DATA_TBS   

1 row selected.

gSQL> PURGE TABLESPACE MEM_DATA_TBS;

Tablespace purged.
```

다음은 사용자가 소유한 휴지통을 모두 제거하는 예이다.

```
gSQL> SELECT OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

OBJECT_NAME                          ORIGINAL_NAME        OBJECT_TYPE
------------------------------------ -------------------- -----------
BIN$64F6BFFC166311EA9C5C835D3E4BBBF7 T1                   TABLE      
BIN$64F6C042166311EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY       CONSTRAINT 
BIN$64F6C010166311EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY_INDEX INDEX      
BIN$64F6C024166311EA9C5C835D3E4BBBF7 T1_IDX1              INDEX      

4 rows selected.

gSQL> PURGE USER_RECYCLEBIN;

Recyclebin purged.
```

다음은 시스템의 모든 휴지통을 제거하는 예이다.

```
gSQL> SELECT OWNER, OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

OWNER OBJECT_NAME                          ORIGINAL_NAME        OBJECT_TYPE
----- ------------------------------------ -------------------- -----------
TEST  BIN$F0FB26F0166311EAA7C5D51B86D72AB6 T1                   TABLE      
TEST  BIN$F0FB272C166311EAA7C5D51B86D72AB6 T1_PRIMARY_KEY       CONSTRAINT 
TEST  BIN$F0FB2704166311EAA7C5D51B86D72AB6 T1_PRIMARY_KEY_INDEX INDEX      
TEST  BIN$F0FB2718166311EAA7C5D51B86D72AB6 T1_IDX1              INDEX      

4 rows selected.

gSQL> PURGE DBA_RECYCLEBIN;

DBA Recyclebin purged.
```

<a id="6e21e1356f799be7"></a>
### 호환성

SQL 표준에서는 &lt;purge statement&gt;를 다루지 않고 있다.

<a id="46776a57aebeff85"></a>
### 참조

관련 내용은 다음을 참조한다.

- [테이블의 휴지통 관리](13-sql-objects.md#16ee3ebcea216f4f)
- [FLASHBACK TABLE](#68eab71c0033b21e)

<a id="4c33a156d51adb72"></a>
## RELEASE SAVEPOINT savepoint_specifier

<a id="9b1ed6a56cc8638c"></a>
### 기능

저장점을 제거한다.

<a id="22a0c8782bf33339"></a>
### 구문

```
<release savepoint statement> ::=
    RELEASE SAVEPOINT savepoint_name 
    ;
```

<a id="112349fa9ed0232f"></a>
### 구문 규칙 및 파라미터

<a id="cf8a08de5dbffb6a"></a>
#### savepoint_name

저장점의 이름으로써 반드시 존재해야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="65c5e7f5a449d4cf"></a>
### 설명

다수의 savepoint가 정의되어 있을 경우, RELEASE SAVEPOINT savepoint_name 구문을 수행할 때savepoint_name 이후에 정의된 savepoint도 함께 제거된다.

<a id="4af5fc703337410b"></a>
### 사용 예

다음은 savepoint를 제거하는 예이다.

```
gSQL> RELEASE SAVEPOINT sp2;

Savepoint dropped.
```

<a id="0f67a5d63d33547d"></a>
### 호환성

**SQL 표준 호환성**

<a id="ad07e969270c947d"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T271 | Savepoints | O |

<a id="2584a94102cfe5d9"></a>
### 참조

관련 내용은 다음을 참조한다.

- [COMMIT](#4d322680eba93c4a)
- [ROLLBACK](#eaa6143895b543a3)
- [SAVEPOINT savepoint_specifier](#f7bc15577098099a)

<a id="e3a10d989cb175f3"></a>
## REVOKE privileges FROM

<a id="f033b7895c9284ef"></a>
### 기능

사용자에게 부여된 권한을 취소한다.

<a id="c9c21660ba5a3513"></a>
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

<a id="6e9e37d1b7a248d3"></a>
### 구문 규칙 및 파라미터

<a id="4427ca10e6f2fc46"></a>
#### &lt;privilege&gt;

Revokee (권한을 취소당할 사용자)로부터 취소할 권한이다.

Revoker (구문을 수행하는 사용자)는 다음 조건 중 하나를 만족해야 한다.

- Revoker가 revokee에게 부여한 &lt;privilege&gt;의 경우 
    - Revoker가 revokee에게 부여한 &lt;privilege&gt;만 취소한다. 
- Revoker가 ACCESS CONTROL ON DATABASE 권한을 소유한 경우
    - 다른 grantor들이 revokee에게 부여한 &lt;privilege&gt;들을 취소한다.

ALL [PRIVILEGES]를 사용하는 경우, 만족하는 &lt;privilege&gt;가 없더라도 성공한다.

&lt;privilege&gt; 종류에 대한 내용은 [GRANT privileges TO](#81c5198ff0096dcc) 구문의 &lt;[privilege&gt;](#a61c0ddbefa20757) 절을 참조한다.

<a id="4f5af71e0fd12e9f"></a>
#### &lt;grantee&gt;

권한을 취소당할 사용자이다.

- user_identifier 
    - 해당 사용자의 권한을 취소한다. 
- PUBLIC 
    - 모든 사용자를 의미하는 authorization 객체이다.

<a id="bb609dfc03fa33c3"></a>
#### GRANT OPTION FOR

권한에 포함된 WITH GRANT OPTION을 삭제한다.   
Dependent privilege의 WITH GRANT OPTION도 함께 삭제한다.

권한은 그대로 유지된다.

<a id="e0de42b1e21a1848"></a>
#### &lt;revoke behavior&gt;

- Dependent privilege: WITH GRANT OPTION으로 &lt;privilege&gt;를 부여받은 revokee가 다른 사용자에게 부여한 것과 동일한 &lt;privilege&gt;이다.
- RESTRICT 
    - Dependent privilege가 존재할 경우 revoke 할 수 없다. 
- CASCADE 
    - Dependent privilege도 함께 revoke 한다.
- CASCADE CONSTRAINTS 
    - Dependent privilege도 함께 revoke 한다.
- 생략할 경우, 기본값은 CASCADE 이다.

<a id="0604d42830a254a7"></a>
### 설명

REVOKE privilege와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

다음과 같은 DROP 구문을 수행할 경우, 별도로 REVOKE 구문을 수행하지 않더라도 해당 객체와 관련된 모든 권한 정보가 삭제된다.

- SQL schema object 관련 DROP 구문
    - [DROP TABLE](#2481c7252f63dc1c)
    - [DROP VIEW](#01da7763edf4f3e5)
    - [DROP SEQUENCE](#8c2068e78d2e75d6)
    - [ALTER TABLE name SET UNUSED COLUMN](#d571baf9c1ff887c)
    - [DROP FUNCTION](../part-04-psm-manual/27-psm-sql-references.md#399ca1e28092268f)
    - [DROP PROCEDURE](../part-04-psm-manual/27-psm-sql-references.md#d133d98fe19742b0)

- Non-schema object 관련 DROP 구문
    - [DROP SCHEMA](#1197651d9b38835b)
    - [DROP TABLESPACE](#703c847167e78d53)
    - [DROP USER](#886267e56d7bc6a6)

<a id="672be6a83419a4ac"></a>
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

<a id="a30a9d5a531c63a3"></a>
### 호환성

SQL 표준에서는 다음 privilege들을 정의하지 않고 있다.

- &lt;database privilege&gt; 
- &lt;tablespace privilege&gt; 
- &lt;schema privilege&gt;

SQL 표준의 &lt;revoke behavior&gt;와는 다음과 같은 차이가 있다.

- SQL 표준의 기본값은 RESTRICT 이다. 
- SQL 표준은 CASCADE CONSTRAINTS 가 없다.

**SQL 표준 호환성**

<a id="2e8cb5f5c7231d02"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T311 | Basic roles | X |
| F034 | Extended REVOKE statement | X |
| S081 | Subtables | X |

<a id="a95f3c75e885e481"></a>
### 참조

관련 내용은 다음을 참조한다.

- [GRANT privileges TO](#81c5198ff0096dcc)
- &lt;[database privilege&gt;](#0813e2a457c183b8)
- &lt;[tablespace privilege&gt;](#6d0298372e1d6e5d)
- &lt;[schema privilege&gt;](#a966ecd031ab1081)
- &lt;[table privilege&gt;](#8e4126f97ea2eda4)
- [Column privilege ](#af1ba097ff33dd40)
- &lt;[sequence privilege&gt;](#3dc09e0d99924ed3)

<a id="eaa6143895b543a3"></a>
## ROLLBACK

<a id="71d362e6cfbf4f4a"></a>
### 기능

트랜잭션을 취소하거나, 저장점 이후의 작업을 취소한다.

<a id="7324f5155c834b0c"></a>
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

<a id="0dca149ffbe67af1"></a>
### 구문 규칙 및 파라미터

<a id="58e6d87f3bf7a10c"></a>
#### WORK

동작에 영향을 미치지 않는 예약어이다.

<a id="c1e8d7f60aecd63b"></a>
#### &lt;rollback force clause&gt;

분산 트랜잭션을 수동으로 rollback 할 때 사용한다.

- FORCE 'xid_string'
    - 'xid_string'에 해당하는 분산 트랜잭션을 rollback 한다.
    - 'xid_string'은 'format_id.transaction_id.branch_id'로 구성된다.
- COMMENT 'comment_string'
    - 분산 트랜잭션을 rollback 할 때 트랜잭션에 주석을 지정한다.

<a id="af7598d63c2c0365"></a>
#### &lt;savepoint clause&gt;

현재 트랜잭션의 ROLLBACK 범위를 명시한다.

- 명시하지 않은 경우 
    - 현재 트랜잭션의 모든 작업을 취소한다. 
    - 트랜잭션을 종료한다. 
    - 모든 savepoint 들을 제거한다. 
    - 모든 lock 들을 해제한다.

- TO SAVEPOINT savepoint_name 
    - 현재 트랜잭션에서 savepoint_name 이후의 작업을 취소한다. 
    - 트랜잭션을 종료하지는 않는다. 
    - savepoint_name 이후의 savepoint 들을 제거한다. 
    - savepoint_name 이후에 획득한 lock 들을 해제한다.

<a id="59501e1dadd63d86"></a>
### 설명

ROLLBACK 구문은 트랜잭션 내에서 수행된 다음 구문들을 rollback 한다.

- Data Manipulation Language (DML) 구문
    - 데이터를 변경하는 INSERT, UPDATE, DELETE 등의 구문
- Data Definition Language (DDL) 구문 
    - 객체의 구조 및 정의를 변경하는 CREATE, DROP, ALTER, TRUNCATE, GRANT, REVOKE 등의 구문

예외적으로, DDL 중에 OS 자원을 다루거나 DATA TYPE을 변경하는 다음 구문들은 rollback 되지 않고 구문을 수행할 때 자동으로 COMMIT 된다.

- [CREATE TABLESPACE](#53b7fdb5c5a23059)
- [DROP TABLESPACE](#703c847167e78d53)
- [ALTER TABLESPACE](#bf506f295181b38d)
- ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE: &lt;[alter column data type clause&gt;](#d66887582dde4234)

<a id="aac2991ccecd48f9"></a>
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

<a id="3c29e1e024f2d928"></a>
### 호환성

**SQL 표준 호환성**

<a id="5b99dc9b8d63af60"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T271 | Savepoints | O |
| T261 | Chained transactions | X |

<a id="a8a3e49a76c7fd1b"></a>
### 참조

관련 내용은 다음을 참조한다.

- [COMMIT](#4d322680eba93c4a)
- [SAVEPOINT savepoint_specifier](#f7bc15577098099a)

<a id="f7bc15577098099a"></a>
## SAVEPOINT savepoint_specifier

<a id="d43d74598bf82126"></a>
### 기능

저장점을 정의한다.

<a id="3a1230eb96db0b3b"></a>
### 구문

```
<savepoint statement> ::=
    SAVEPOINT savepoint_name 
    ;
```

<a id="2ca096c6812e92a3"></a>
### 구문 규칙 및 파라미터

<a id="92e0706afdb6a8fc"></a>
#### savepoint_name

저장점 이름이다.   
저장점 이름이 기존의 저장점 이름과 중복될 경우 기존의 저장점이 삭제된다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="d34db1c55faa2d66"></a>
### 설명

정의한 savepoint는 ROLLBACK TO SAVEPOINT 구문 ([ROLLBACK](#eaa6143895b543a3) 구문 참조)에서 사용되며, 해당 savepoint까지 수행된 DML, DDL 구문이 철회되고 해당 구문이 획득한 lock도 해제된다.

정의한 savepoint는 transaction을 COMMIT 하거나 ROLLBACK 할 때 자동으로 제거되는데 [RELEASE SAVEPOINT savepoint_specifier](#4c33a156d51adb72) 구문을 사용하여 명시적으로 제거할 수도 있다.

<a id="3a8273aaa671539c"></a>
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

<a id="144eb569a81f486f"></a>
### 호환성

**SQL 표준 호환성**

<a id="7563c3845df73a1c"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T271 | Savepoints | O |

<a id="40d8202e46559e42"></a>
### 참조

관련 내용은 다음을 참조한다.

- [COMMIT](#4d322680eba93c4a)
- [ROLLBACK](#eaa6143895b543a3)
- [RELEASE SAVEPOINT savepoint_specifier](#4c33a156d51adb72)

<a id="93101dc44f4e210d"></a>
## SELECT

<a id="83a1bf13756be069"></a>
### query expression

<a id="9e43ce438c3053e4"></a>
#### 기능

하나 이상의 table 또는 view에서 원하는 row를 검색한다.

<a id="a62a71a69be0d49e"></a>
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

<a id="1b62e72bae1344e5"></a>
#### 사용 범위 및 접근 권한

&lt;query expression&gt; 구문을 수행하려면 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나를 가져야 한다.

- 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
- 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- SELECT ANY TABLE ON DATABASE

<a id="3a36330b101408c8"></a>
#### 구문 규칙 및 파라미터

<a id="c3f81b5c049b094c"></a>
##### &lt;set operator&gt;

부질의 (subquery) 간의 집합 연산을 수행한다.  
자세한 내용은 [set operator](#72ceb9751f3faad0) 절을 참조한다.

<a id="c4d7be32f306eabb"></a>
##### &lt;query specification&gt;

하나의 부질의 (subquery)를 기술한다.  
자세한 내용은 [query specification](#b2068000ef8bfb23) 절을 참조한다.

<a id="9767adbdb210e038"></a>
##### &lt;order by clause&gt;

검색 결과에 대한 정렬 정보를 기술한다.  
자세한 내용은 [order by clause](#755bc92d9f68eb02)를 참조한다.

<a id="5bd6c27e4dbc9e19"></a>
##### &lt;offset limit clause&gt;

검색 결과 집합에서 skip 할 row의 개수와 fetch 할 row의 개수를 기술한다.  
자세한 내용은 [offset limit clause](#2e8423d8813ebc76)를 참조한다.

<a id="61be6af996fd5f13"></a>
#### 설명

SELECT 구문으로 query를 기술한다.  
&lt;order by clause&gt;, &lt;offset limit clause&gt;는 생략할 수 있다.  
&lt;set operator&gt;를 사용하여 둘 이상의 부질의 (subquery)를 가질 수 있다.

<a id="175fd1f2094b3b9a"></a>
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

<a id="05d47055b2bd6889"></a>
#### 호환성

**SQL 표준 호환성**

<a id="07e2af2ebdb472be"></a>
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

<a id="b2068000ef8bfb23"></a>
### query specification

<a id="d6faa2f6037e7a01"></a>
#### 기능

&lt;table expression&gt; 결과로부터 파생된 table을 기술한다.

<a id="c0f5a4b773e2d39b"></a>
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

<a id="7da7fce30e8cbc4e"></a>
#### 사용 범위 및 접근 권한

&lt;query specification&gt; 구문을 수행하려면 다음 조건 중 하나를 만족해야 한다.

- 테이블의 소유자 
- 테이블에 대한 SELECT 권한 
- 테이블이 속한 스키마에 대해 SELECT TABLE, CONTROL TABLE, CONTROL 권한 중 하나를 소유 
- Database에 대한 SELECT TABLE 권한을 소유

<a id="9d0fe64ca542e61a"></a>
#### 구문 규칙 및 파라미터

<a id="94b293040089785d"></a>
##### &lt;hint clause&gt;

질의 수행에 필요한 힌트를 기술한다.  
자세한 내용은 [SQL Hint](15-sql-tuning.md#68e2aa9f8a1e31e4)를 참조한다.

<a id="086644f1a7523a36"></a>
##### &lt;set quantifier&gt;

질의 결과의 중복 제거 여부를 기술한다.  
생략할 경우, ALL과 동일하게 동작한다.

<a id="7c431f5e68cf36f4"></a>
##### &lt;select list&gt;

질의 결과로부터 검색할 column을 기술한다.  
자세한 내용은 [select list](#df8abc1a6f23e3cc)를 참조한다.

<a id="9341bff66be43abc"></a>
##### &lt;from clause&gt;

검색할 table들을 기술한다.  
자세한 내용은 [from clause](#f9a5b2d81f65a8aa)를 참조한다.

<a id="c36c9adb12a26343"></a>
##### &lt;where clause&gt;

검색 조건을 기술한다.  
자세한 내용은 [where clause](#21c50afccf7f4c56)를 참조한다.

<a id="6081e35358901659"></a>
##### &lt;group by clause&gt;

검색 결과에 대한 grouping을 기술한다.  
자세한 내용은 [group by clause](#ba90ae370cb956ae)를 참조한다.

<a id="47a1bc13cbb69117"></a>
##### &lt;having clause&gt;

Grouping 된 결과에 대한 조건을 기술한다.  
자세한 내용은 [having clause](#57d0f6a864936181)를 참조한다.

<a id="a7313652bc383f70"></a>
#### 설명

<a id="233903147274d4d8"></a>
##### &lt;hint clause&gt;

&lt;hint clause&gt;는 사용자가 optimizer에게 SQL 구문 수행 방법을 직접 지시하기 위해 사용하는 comment이다.

GOLDILOCKS의 optimizer는 사용자가 기술한 &lt;hint clause&gt;를 우선 적용한다.  
만약 적용할 수 없을 경우에는 cost 계산을 통해 최적의 실행 계획을 선택한다.

GOLDILOCKS는 기본적으로 &lt;hint clause&gt;에 구문상 에러가 발생하더라도 이를 무시하도록 설정되어 있다. &lt;hint clause&gt;에 구문상 에러가 있는지 확인하려면 [HINT_ERROR](../part-02-administration-manual/10-server-property.md#d0d6276280d2ca4e) property를 on으로 설정하고 질의를 수행하도록 한다

<a id="dd59754dbee056c0"></a>
##### &lt;set quantifier&gt;

&lt;set quantifier&gt;는 &lt;select list&gt; expression들로 구성된 결과 집합에서 중복을 제거할지 여부를 설정한다.

- ALL: 결과 집합에서 중복을 제거하지 않는다.
- DISTINCT: 결과 집합에서 중복을 제거한다.
- 생략할 경우, ALL을 기술한 것과 동일하게 동작한다.

<a id="94db31e2090b3d24"></a>
##### &lt;select list&gt;

질의 결과로부터 검색할 column을 기술한다.  
이 목록은 콤마 (,) 리스트로 구분하여 기술한다.  
&lt;from clause&gt;에 기술한 모든 column들을 기술하고 싶은 경우에는 별표 (*)를 사용한다.

<a id="e86beb400db4fc83"></a>
##### &lt;from clause&gt;

&lt;from clause&gt;는 검색할 table 또는 view들을 기술한다.

<a id="08a114b56798e7c4"></a>
##### &lt;where clause&gt;

&lt;where clause&gt;는 &lt;from clause&gt;로부터 얻은 결과 집합 중에 원하는 결과만 가져오도록 검색 조건을 기술한다.

<a id="7d3fdece55cceb90"></a>
##### &lt;group by clause&gt;

&lt;group by clause&gt;는 &lt;where clause&gt;를 적용한 결과 집합의 grouping 방법을 기술한다.

&lt;group by clause&gt;가 기술된 경우, &lt;select list&gt;에 올 수 있는 expression은 다음과 같다.

- 상수
- group by에 기술된 expression
- group by에 기술된 expression의 연산식
- group에 속하는 expression에 대한 집계 함수

<a id="2b41758c559f5084"></a>
##### &lt;having clause&gt;

&lt;having clause&gt;는 grouping된 결과 집합에 대한 검색 조건을 기술한다.  
일반적으로 &lt;group by clause&gt;와 함께 사용된다.

<a id="31e90c787b4555d8"></a>
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

<a id="8923637749a7c4de"></a>
#### 호환성

**SQL 표준 호환성**

<a id="39d724bf57998c08"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F801 | Full set function | X |
| T051 | Row types | X |
| T301 | Functional dependencies | X |
| T325 | Qualified SQL parameter references | X |
| T053 | Explicit aliases for all-fields reference | O |
| T285 | Enhanced derived column names | O |

<a id="183a5f3e9705c536"></a>
#### 참조

관련 내용은 [query expression](#83a1bf13756be069)을 참조한다.

<a id="df8abc1a6f23e3cc"></a>
### select list

<a id="fc81f7f9e3dae285"></a>
#### 기능

질의 결과로부터 검색할 column을 기술한다.

<a id="8030916f0afb2dab"></a>
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

<a id="b301976359fdd1a1"></a>
#### 사용 범위 및 접근 권한

&lt;select list&gt; 구문에 column이나 subquery가 존재할 때 다음을 만족해야 한다.

- column에 대한 접근 권한
- subquery에 존재하는 table 및 column에 대한 접근 권한

<a id="79a645a9367ab3b3"></a>
#### 구문 규칙 및 파라미터

<a id="7abacbaae95c47e4"></a>
##### &lt;select list&gt;

&lt;asterisk&gt;나 &lt;select sublist&gt;를 갖는다.

<a id="8a1897d7a1393803"></a>
##### &lt;asterisk&gt;

- &lt;asterisk&gt;는 &lt;select list&gt;에 단독으로만 쓰일 수 있다.
    - (O) SELECT * FROM t1;
    - (X) SELECT *, c1 FROM t1;

<a id="e4906a8de14b8bdb"></a>
##### &lt;select sublist&gt;

- &lt;derived column&gt; 또는 &lt;qualified asterisk&gt;를 갖는다.
    - SELECT c1, c2 FROM t1;
    - SELECT t1.* FROM t1;
- &lt;derived column&gt;은 AS를 사용하여 출력 이름을 변경할 수 있으며, AS는 생략할 수 있다.
    - SELECT c1 AS col1, c2 AS col2 AS FROM t1;
    - SELECT c1 col1, c2 col2 FROM t1;
- 둘 이상의 &lt;select sublist&gt;를 기술할 경우, 각 &lt;select sublist&gt;를 콤마 (,)로 구분해야 한다.
    - (O) SELECT c1, c2 FROM t1;
    - (O) SELECT c1, c2, t1.* FROM t1;
    - (X) SELECT c1 c2 FROM t1;
        - c2는 ALIAS로 처리
    - (X) SELECT c1 c2 c3 FROM t1;

<a id="ce8d6287d4c09cff"></a>
#### 설명

<a id="d976b43db37e67ad"></a>
##### &lt;select list&gt;

&lt;select list&gt;는 결과 집합에 포함될 column들을 기술한다.

<a id="e8b8687af83c5a56"></a>
##### &lt;asterisk&gt;

&lt;asterisk&gt;는 &lt;from clause&gt;에 있는 모든 column들을 select list로 설정한다.

<a id="955817dc9a810f4e"></a>
##### &lt;select sublist&gt;

&lt;select sublist&gt;는 &lt;derived column&gt; 또는 &lt;qualified asterisk&gt;를 갖는다.

- &lt;qualified asterisk&gt;
    - 특정 table이나 view에 속하는 모든 column들을 select list로 설정한다.
- &lt;derived column&gt;
    - column 또는 &lt;value expression&gt;을 기술할 수 있다.
    - &lt;as clause&gt;를 사용하여 column name을 변경할 수 있으며, 이 때 AS는 생략할 수 있다.
    - &lt;from clause&gt;에 동일한 column name을 가진 테이블들이 있는 경우, 이 column을 참조하기 위해서는 table name이나 table alias를 반드시 명시해야 한다.
        - SELECT t1.c1, t2.c1 FROM t1, t2;
        - SELECT a.c1, b.c1 FROM t1 a, t2 b;

&lt;select sublist&gt;를 둘 이상 기술할 경우에는 반드시 콤마 (,)로 구분하여야 한다.

<a id="095e9fec44638432"></a>
##### select list에 설정되는 이름

- &lt;derived column&gt;에 &lt;column name&gt;이 명시된 경우, 해당 이름이 select list 이름으로 설정된다.
    - SELECT i1 AS name FROM t1;
- &lt;derived column&gt;에 &lt;column name&gt;이 명시되지 않은 경우
    - &lt;derived column&gt;이 single column reference인 경우
        - Single column이 가진 column name이 select list 이름으로 설정된다.
        - SELECT i1 FROM t1;
    - &lt;derived column&gt;이 column이 아닌 expression인 경우
        - Select list 이름이 설정되지 않는다.
        - SELECT i1 + 100 FROM t1;
        - CREATE TABLE AS SELECT 구문에 쓰일 경우, column name을 기술해야 한다.
        - CREATE TABLE t2 AS SELECT i1 + 100 AS sum_i1 FROM t1;

<a id="a08bdf23ecbf0f27"></a>
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

<a id="e8c8cb97ea5ea00e"></a>
#### 호환성

<a id="42b39467ad2afe91"></a>
#### 참조

관련 내용은 [query specification](#b2068000ef8bfb23)을 참조한다.

<a id="f9a5b2d81f65a8aa"></a>
### from clause

<a id="aa64620ca725bfb0"></a>
#### 기능

하나 이상의 table들로부터 파생된 table을 기술한다.

<a id="b1f0f84bbd80ede4"></a>
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

<a id="c5860dfb9126d696"></a>
#### 사용 범위 및 접근 권한

&lt;table reference list&gt;에 기술한 table 또는 view에 대한 접근 권한이 있어야 한다.

<a id="c6a16e08b63f4430"></a>
#### 구문 규칙 및 파라미터

<a id="2fdd8c084a3b6608"></a>
##### &lt;table reference list&gt;

- &lt;table reference list&gt;에는 한 개 이상의 테이블들을 콤마 (,)를 이용하여 기술할 수 있다.
- 두 개 이상의 테이블이 기술된 경우
    - 테이블은 왼쪽에서 오른쪽 방향으로 평가 (evaluation)된다.
    - &lt;select list&gt;에 *를 기술한 경우 왼쪽 테이블의 column부터 오른쪽 테이블의 column까지 순서대로 &lt;select list&gt;에 매핑된다.

<a id="da4d34b26576bd3c"></a>
##### &lt;table primary&gt;

- &lt;correlation name&gt;을 사용하여 별칭 (alias name)을 기술할 수 있다.
    - SELECT * FROM t1 AS a, t2 AS b;
    - SELECT * FROM ( SELECT i1 FROM t1 ) AS a;

- &lt;derived table&gt;, 즉 &lt;table subquery&gt;는
    - &lt;correlation name&gt;을 이용하여 별칭 (alias name)을 기술할 수 있다.
        - SELECT * FROM ( SELECT i1, i2, i3 FROM t1 ) AS a;
    - &lt;derived column list&gt;를 기술할 수 있다.
        - SELECT * FROM ( SELECT i1, i2, i3 FROM t1 ) AS a( col1, col2, col3 );
        - &lt;derived column list&gt;의 &lt;column name&gt; 개수는 &lt;table subquery&gt;에 기술한 &lt;select list&gt;의 target 개수와 동일해야 한다.
        - &lt;table subquery&gt;에 기술한 &lt;select list&gt;의 target과 순서대로 1 : 1 매핑된다.
        - 해당 &lt;derived table&gt; 내 &lt;table subquery&gt;의 &lt;select list&gt;를 참조하려면 반드시 &lt;derived column list&gt;에 기술한 &lt;column name&gt;을 사용해야 한다.

```
SELECT col1, col2 
FROM ( SELECT i1, i2 FROM t1 ) AS a( col1, col2 ) 
WHERE col1 = 1 AND col2 = 1;
```

<a id="fbfac842f0304c91"></a>
##### &lt;correlation name&gt;

- &lt;table reference list&gt;에는 동일한 &lt;correlation name&gt;이 두 개 이상 존재할 수 없다.
- &lt;correlation name&gt;이 기술된 경우 해당 &lt;table name&gt;이나 &lt;derived table&gt;을 참조하려면 반드시 &lt;correlation name&gt;을 이용하여야 한다.
    - SELECT a.i1 FROM t1 AS a WHERE a.i1 > 3;
    - (X) SELECT t1.i1 FROM t1 AS a WHERE t1.i1 > 3;
- &lt;correlation name&gt;을 기술할 때 그 앞의 AS는 생략할 수 있다.
    - SELECT a.i1 FROM t1 a;

<a id="48cdae7741d3fe28"></a>
##### &lt;derived column list&gt;

&lt;derived column list&gt;에는 동일한 &lt;column name&gt;이 두 개 이상 존재할 수 없다.

<a id="1cde9b53b91282c4"></a>
##### &lt;cluster domain&gt;

- &lt;cluster domain&gt;은 table이나 view, table subquery를 대상으로 기술할 수 있다.
    - SELECT * FROM t1@G1;
    - &lt;parenthesized joined table&gt;에는 기술할 수 없다.
        - (X) SELECT * FROM ( t1 INNER JOIN t2 ON t1.sk = t2.sk )@G2;
- 구조나 데이터가 변경될 table이나 view에는 &lt;cluster domain&gt;을 기술할 수 없다.
    - (X) DELETE FROM t2@GLOBAL;
    - (X) UPDATE t1@GLOBAL SET i1 = 1;
    - (X) INSERT INTO t1@GLOBAL VALUES ( 1, 10 );
    - (X) SELECT * FROM t1@GLOBAL FOR UPDATE;
    - (X) CREATE INDEX t1_idx ON t1@GLOBAL( i1 );

<a id="a9ca5527172d6631"></a>
##### &lt;cluster domain name&gt;

&lt;cluster domain name&gt;의 &lt;identifier&gt;에는 cluster group name이나 cluster member name이 올 수 있다.

- cluster group name 
    - SELECT * FROM t1@G1;
- cluster member name
    - SELECT * FROM t1@G1N1;

<a id="c388c2c3311e4042"></a>
#### 설명

<a id="ba841b5b5ab66dca"></a>
##### &lt;table reference list&gt;

&lt;table reference list&gt;에는 콤마 (,)를 사용하여 두 개 이상의 테이블들을 기술할 수 있다.

- 두 개 이상의 테이블을 기술하면 해당 테이블들을 왼쪽에서 오른쪽으로 각각 cross join하듯 작동한다.
    - SELECT * FROM t1, t2;
    - &lt;=&gt; SELECT * FROM t1 CROSS JOIN t2;
- &lt;where clause&gt;에 두 테이블의 join 조건이 존재할 경우, &lt;where clause&gt;를 join 조건으로 갖는 inner join처럼 동작한다. 
    - SELECT * FROM t1, t2 WHERE t1.I1 = t2.I1;
    - &lt;=&gt; SELECT * FROM t1 INNER JOIN t2 ON t1.i1 = t2.i1;
- &lt;where clause&gt;에 outer join operator (+)를 사용한 경우, outer join과 동일하게 작동한다.
    - Outer join operator (+)에 대한 자세한 내용은 [OUTER JOIN](12-sql-languages.md#58c00fa9e075c8d3) 절을 참조한다.

<a id="f82133878c418c0e"></a>
##### &lt;table reference&gt;

단일 table이나 view, table subquery, joined table 등이 &lt;table reference&gt;가 될 수 있다. Joined table을 제외한 나머지는 correlation name을 가질 수 있다.

Joined table에 대한 자세한 내용은 [joined table](#91d75501707e7c41) 절을 참고한다.

<a id="1c4563372b8e72c6"></a>
##### &lt;table primary&gt;

Table이나 view, table subquery, &lt;parenthesized joined table&gt;이 &lt;table primary&gt;가 될 수 있다.

Table이나 view, table subquery는 correlation name을 가질 수 있는데, 이 때 AS는 생략할 수 있다. Correlation name이 기술된 경우, &lt;select list&gt;나 &lt;where clause&gt;와 같이 해당 table이나 view, table subquery를 참조하는 모든 경우에 correlation name을 사용해야 한다.

Table subquery는 &lt;derived column list&gt;를 기술할 수 있으며, correlation name과 마찬가지로 해당 table subquery의 column을 참조하는 모든 경우에 &lt;derived column list&gt;에 기술한 이름을 사용하여야 한다. Table subquery에 &lt;derived column list&gt;를 사용하려면 correlation name을 반드시 기술해야 한다.

&lt;parenthesized joined table&gt;은 join 연산에 참여하는 table들의 논리적 join 순서를 기술한다. 이 때 괄호로 묶은 모든 table들에 대한 join이 모두 cross join과 inner join일 경우, optimizer가 join 순서를 변경할 수 있다.

<a id="7d4c55b76f8922e5"></a>
##### &lt;cluster domain&gt;

&lt;cluster domain&gt;이 생략된 경우 &lt;cluster domain name&gt;으로 GLOBAL을 사용한 것과 동일한 의미를 갖는다.  
자세한 내용은 [Cluster Domain](12-sql-languages.md#e260b84c79c55126)을 참조한다.

<a id="6a8c286a4965e9e7"></a>
##### &lt;cluster domain name&gt;

&lt;cluster domain name&gt;에 정의된 예약어는 다음과 같은 의미를 가진다.

- GLOBAL
    - 모든 cluster group을 cluster domain으로 선정한다.
- LOCAL
    - 사용자 질의를 수행하는 server만 cluster domain으로 선정한다.
        - G2N1에서 다음 질의를 수행할 때, G2N1의 데이터를 가지고 온다.
        - SELECT * FROM t1@LOCAL;
- LOCAL_OFFLINE
    - Offline 상태의 table 데이터를 조회하기 위해 사용자 질의를 수행하는 server만 cluster domain으로 선정한다.
        - G2N1에서 다음 질의를 수행할 때, offline table T1의 G2N1의 데이터를 가져온다.
        - SELECT * FROM t1@LOCAL_OFFLINE;
    - Online table에 LOCAL_OFFLINE domain을 기술하면 에러가 발생한다.

&lt;cluster domain name&gt;에 &lt;identifier&gt;를 기술한 경우 해당 이름의 cluster group 또는 cluster member를 [Cluster Domain](12-sql-languages.md#e260b84c79c55126)으로 선정한다.

<a id="12b33658cd665d83"></a>
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

<a id="e018fcb303c7c7ef"></a>
#### 호환성

<a id="1211e4ac47a553cd"></a>
#### 참조

관련 내용은 [subquery](#fce639de96024211)를 참조한다.

<a id="91d75501707e7c41"></a>
### joined table

<a id="51bc3e78100dd0b6"></a>
#### 기능

Cartesian product, inner join, outer join 등에서 파생되는 table을 기술한다.

<a id="696f3570c852b1a1"></a>
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

<a id="1b3e37fca3240be0"></a>
#### 사용 범위 및 접근 권한

joined table에 기술된 모든 table 및 view에 대한 접근 권한이 있어야 한다.

<a id="f9d9d388a3ad0133"></a>
#### 구문 규칙 및 파라미터

<a id="bebbd1a6491e0337"></a>
##### &lt;cross join&gt;

Join 조건을 명시하는 &lt;join specification&gt;은 &lt;cross join&gt; 위치에 오지 않는다.  
&lt;cross join&gt;의 오른쪽에는 단일 테이블이나 &lt;table subquery&gt;, &lt;parenthesized joined table&gt;이 올 수 있다.

<a id="000ca66fc1e19117"></a>
##### &lt;qualified join&gt;

- Join 조건을 명시하는 &lt;join specification&gt;을 반드시 기술해야 한다.
    - SELECT * FROM t1 INNER JOIN t2 ON t1.i1 = t2.i1;
    - SELECT * FROM t1 INNER JOIN t2 USING ( i1 );
- &lt;join type&gt;은 생략할 수 있는데 생략할 경우 INNER로 처리한다.
    - SELECT * FROM t1 JOIN t2 ON t1.i1 = t2.i1;
    - &lt;=&gt; SELECT * FROM t1 INNER JOIN t2 ON t1.i1 = t2.i1;
- &lt;join type&gt;에서 OUTER는 생략할 수 있다.
    - SELECT * FROM t1 LEFT JOIN t2 ON t1.i1 = t2.i1;
    - &lt;=&gt; SELECT * FROM t1 LEFT OUTER JOIN t2 ON t1.i1 = t2.i1;
- &lt;join type&gt;이 OUTER JOIN인 경우 &lt;join specification&gt;에는 &lt;join condition&gt;만 올 수 있다. 
    - SELECT * FROM t1 FULL OUTER JOIN t2 ON t1.i1 = t2.i1;
    - (X) SELECT * FROM t1 FULL OUTER JOIN t2 USING ( i1 );

<a id="33a3a47f7d032d3a"></a>
##### &lt;natural join&gt;

- Join 조건을 명시하는 &lt;join specification&gt;은 &lt;natural join&gt; 위치에 오지 않는다.
- &lt;natural join&gt; 오른쪽에는 단일 테이블이나 &lt;table subquery&gt;, &lt;parenthesized joined table&gt;이 올 수 있다.
- &lt;join type&gt;은 생략할 수 있는데 생략할 경우 INNER로 처리한다.
    - SELECT * FROM t1 NATURAL JOIN t2;
    - &lt;=&gt; SELECT * FROM t1 NATURAL INNER JOIN t2;
- &lt;join type&gt;에 OUTER를 지원하지 않는다.
    - (X) SELECT * FROM t1 NATURAL LEFT OUTER JOIN t2;
- NATURAL JOIN의 왼쪽 row와 오른쪽 row에 동일한 &lt;column name&gt;이 하나도 없는 경우 &lt;cross join&gt;으로 처리한다.
    - t1( c1 INTEGER, c2 INTEGER );
    - t2( c3 INTEGER, c4 INTEGER );
    - SELECT * FROM t1 NATURAL INNER JOIN t2;
    - &lt;=&gt; SELECT * FROM t1 CROSS JOIN t2;
- NATURAL JOIN의 왼쪽 row와 오른쪽 row에 동일한 &lt;column name&gt;이 있을 경우, USING 구문을 기술한 것과 동일하게 동작한다.
    - t1( c1 INTEGER, c2 INTEGER );
    - t2( c2 INTEGER, c3 INTEGER );
    - SELECT * FROM t1 NATURAL INNER JOIN t2;
    - &lt;=&gt; SELECT * FROM t1 INNER JOIN t2 USING( c2 );

<a id="8527e9df528d7ca5"></a>
##### &lt;join specification&gt;

- &lt;join condition&gt;이나 &lt;named columns join&gt; 중에 하나만 기술할 수 있다.
    - &lt;join condition&gt;
        - SELECT * FROM t1 INNER JOIN t2 ON t1.i1 = t2.i1;
    - &lt;named columns join&gt;
        - SELECT * FROM t1 INNER JOIN t2 USING ( i1 );
- &lt;named columns join&gt;을 기술한 경우
    - &lt;join column list&gt;에는 반드시 하나 이상의 column name을 기술해야 한다.
        - SELECT * FROM t1 INNER JOIN t2 USING ( i1 );
    - Column name은 &lt;table name&gt;.&lt;column name&gt;과 함께 기술할 수 없다.
        - (X) SELECT * FROM t1 INNER JOIN t2 USING ( t1.i1 );
    - &lt;join column list&gt;에 나열된 column들이 JOIN의 왼쪽 row와 오른쪽 row에 반드시 존재해야 하며, 비교 가능해야 한다.
        - t1( c1 INTEGER, c2 INTEGER );
        - t2( c2 INTEGER, c3 INTEGER );
        - SELECT * FROM t1 INNER JOIN t2 USING ( c2 );
    - &lt;select list&gt;에 *를 사용한 경우의 레코드 구성  
      1) &lt;join column list&gt;에 기술된 column들   
      2) 왼쪽 row들 중에서 &lt;join column list&gt;에 해당되지 않는 column들  
      3) 오른쪽 row들 중에서 &lt;join column list&gt;에 해당되지 않는 column들
        - t1( c1 INTEGER, c2 INTEGER );
        - t2( c2 INTEGER, c3 INTEGER );
        - SELECT * FROM t1 INNER JOIN t2 USING ( c2 );
        - 레코드 구성 : C2, C1, C3
    - &lt;join column list&gt;에 기술된 &lt;column name&gt;은 &lt;table name&gt;.&lt;column name&gt;과 함께 참조할 수 없고, &lt;column name&gt;으로만 참조할 수 있다.
        - SELECT c2 FROM t1 INNER JOIN t2 USING ( c2 ) WHERE c2 > 3;
        - (X) SELECT t1.c2 FROM t1 INNER JOIN t2 USING ( c2 );
        - (X) SELECT * FROM t1 INNER JOIN t2 USING ( c2 ) WHERE t1.c2 > 3;
    - &lt;join column list&gt;의 조인 조건 처리
        - &lt;join column list&gt;에 나열된 각 column 들에 대하여
        - &lt;left table name&gt;.&lt;column name&gt; = &lt;right table name&gt;.&lt;column name&gt; 조건이 생성되고
        - 각 &lt;column name&gt;에 대한 조건들을 AND로 처리하는 조건이 생성된다.
        - t1( c1 INTEGER, c2 INTEGER );
        - t2( c1 INTEGER, c2 INTEGER );
        - SELECT * FROM t1 INNER JOIN t2 USING ( c1, c2 );
        - 조인 조건: t1.c1 = t2.c1 AND t1.c2 = t2.c2
    - &lt;select list&gt;에는 특정 테이블의 모든 column을 반환하는 &lt;table name&gt;.* 구문을 사용할 수 없다.
        - (X) SELECT t1.*, t2.* FROM t1 INNER JOIN t2 USING ( c1, c2 );

<a id="b01f5400c1e8bb54"></a>
#### 설명

<a id="4700317ecd14d49d"></a>
##### &lt;cross join&gt;

&lt;cross join&gt;은 왼쪽의 각 row를 오른쪽의 모든 row들과 결합한 결과를 반환한다.

```
T1 ( 1, 1 ), ( 2, 2 )
T2 ( 2, 2 ), ( 3, 3 )

gSQL> SELECT * FROM t1 CROSS JOIN t2;
C1 C2 C1 C2
-- -- -- --
 1  1  2  2
 1  1  3  3
 2  2  2  2
 2  2  3  3
4 rows selected.
```

&lt;cross join&gt;에는 join 조건을 명시적으로 기술할 수 없지만, &lt;where clause&gt;를 통해 두 table에 대한 join 조건을 기술할 수 있으며, 이 경우 inner join과 동일하게 동작한다.  
• SELECT * FROM t1 CROSS JOIN t2 WHERE t1.c1 = t2.c1;  
• &lt;=&gt; SELECT * FROM t1 INNER JOIN t2 ON t1.c1 = t2.c1;

```
T1 ( 1, 1 ), ( 2, 2 )
T2 ( 2, 2 ), ( 3, 3 )

gSQL> SELECT * FROM t1 CROSS JOIN t2 WHERE t1.c1 = t2.c1;
C1 C2 C1 C2
-- -- -- --
 2  2  2  2
1 row selected.
```

<a id="66d49976a515813c"></a>
##### &lt;qualified join&gt;

&lt;qualified join&gt;은 왼쪽의 각 row들을 오른쪽의 모든 row들과 결합한 후 join 조건을 만족하는 row들만 결과로 반환한다.

&lt;table expression&gt;에 &lt;where clause&gt;가 존재할 경우, &lt;qualified join&gt;의 결과 집합에 &lt;where clause&gt; 조건들을 적용한다.

Inner join은 &lt;where clause&gt;에 존재하는 조건들을 join 조건처럼 처리해도 결과가 동일하지만, outer join은 &lt;where clause&gt;에 존재하는 조건들을 join 조건처럼 처리하면 결과가 달라진다.

- **INNER JOIN:** 

```
t1 ( 1, 1 ), ( 2, 2 ), ( 3, 3 ), ( 4, 4 ), ( 5, 5 )
t2 ( 2, 2 ), ( 3, 3 )
```

- ON 절에만 조건이 있는 경우

```
gSQL> SELECT * FROM t1 INNER JOIN t2 ON t1.c1 = t2.c1 AND t1.c2 = t2.c2;
C1 C2 C1 C2
-- -- -- --
 2  2  2  2
 3  3  3  3
2 rows selected.
```

- ON 절과 WHERE 절에 조건이 있는 경우 
    - JOIN 조건 ON t1.c1 = t2.c1을 적용한 결과 집합에 WHERE 조건 t1.c2 = t2.c2를 적용

```
gSQL> SELECT * FROM t1 INNER JOIN t2 ON t1.c1 = t2.c1 WHERE t1.c2 = t2.c2;
C1 C2 C1 C2
-- -- -- --
 2  2  2  2
 3  3  3  3
2 rows selected.
```

    - JOIN 조건 ON t1.c1 = t2.c1을 적용한 결과 집합 → WHERE 조건 t1.c2 = t2.c2를 적용

```
( 2,  2,    2,    2 )                        ( 2,  2,    2,    2 )
  ( 3,  3,    3,    3 )                   →   ( 3,  3,    3,    3 )
```

- **OUTER JOIN:** 

```
t1 ( 1, 1 ), ( 2, 2 ), ( 3, 3 ), ( 4, 4 ), ( 5, 5 )
t2 ( 2, 2 ), ( 3, 3 )
```

- ON 절에만 조건이 있는 경우

```
gSQL> SELECT * FROM t1 LEFT OUTER JOIN t2 ON t1.c1 = t2.c1 AND t1.c2 = t2.c2;
C1 C2   C1   C2
-- -- ---- ----
 1  1 null null
 2  2    2    2
 3  3    3    3
 4  4 null null
 5  5 null null
5 rows selected.
```

- ON 절과 WHERE 절에 조건이 있는 경우 
    - JOIN 조건 ON t1.c1 = t2.c1을 적용한 결과 집합에 WHERE 조건 t1.c2 = t2.c2를 적용

```
gSQL> SELECT * FROM t1 LEFT OUTER JOIN t2 ON t1.c1 = t2.c1 WHERE t1.c2 = t2.c2;
C1 C2 C1 C2
-- -- -- --
 2  2  2  2
 3  3  3  3
2 rows selected.
```

    - JOIN 조건 ON t1.c1 = t2.c1을 적용한 결과 집합 → WHERE 조건 t1.c2 = t2.c2를 적용

```
( 1,  1, null, null )
  ( 2,  2,    2,    2 )                        ( 2,  2,    2,    2 )
  ( 3,  3,    3,    3 )                   →   ( 3,  3,    3,    3 ) 
  ( 4,  4, null, null )
  ( 5,  5, null, null )
```

Left outer join은 왼쪽 row에 대한 join 조건을 만족하는 오른쪽 row가 있을 경우, 해당 row들을 결합한 row를 결과로 반환한다. Join 조건을 만족하는 오른쪽 row가 존재하지 않을 경우, 왼쪽 row의 값은 그대로 유지하고 오른쪽 row의 값은 모두 NULL로 채운 row를 결과로 반환한다.

- **LEFT OUTER JOIN:** 

```
t1 ( 1, 1 ), ( 2, 2 )
t2 ( 2, 2 ), ( 3, 3 )

gSQL> SELECT * FROM t1 LEFT OUTER JOIN t2 ON t1.c1 = t2.c1;
C1 C2   C1   C2
-- -- ---- ----
 1  1 null null
 2  2    2    2
2 rows selected.
```

Right outer join은 left outer join과 정확히 반대로 동작한다.

```
RIGHT OUTER JOIN

t1 ( 1, 1 ), ( 2, 2 )
t2 ( 2, 2 ), ( 3, 3 )

gSQL> SELECT * FROM t1 RIGHT OUTER JOIN t2 ON t1.c1 = t2.c1;
  C1   C2 C1 C2
---- ---- -- --
   2    2  2  2
null null  3  3
2 rows selected.
```

Full outer join은 left outer join의 결과와 함께 join 조건을 만족하지 않는 모든 오른쪽 row에 대해 왼쪽 row의 값을 NULL로 채운 row들을 결과로 반환한다.

```
FULL OUTER JOIN

t1 ( 1, 1 ), ( 2, 2 )
t2 ( 2, 2 ), ( 3, 3 )

gSQL> SELECT * FROM t1 FULL OUTER JOIN t2 ON t1.c1 = t2.c1;
  C1   C2   C1   C2
---- ---- ---- ----
   1    1 null null
   2    2    2    2
null null    3    3
3 rows selected.
```

<a id="b24cdc74bebefb7e"></a>
##### &lt;natural join&gt;

&lt;natural join&gt;은 join에 참여하는 두 table에서 동일한 이름을 갖는 모든 column들을 각각 equal 조건으로 join 한다. 즉, join에 참여하는 두 table에서 동일한 이름을 갖는 모든 column들을 inner join에서 USING 구문에 기술한 것과 동일하다.

```
t1 ( C1 INTEGER, C2 INTEGER )
t2 ( C1 INTEGER, C3 INTEGER )

t1 ( 1, 10 ), ( 2, 20 ), ( 3, 30 )
t2 ( 1, 100 ), ( 2, 200 ), ( 3, 300 )

gSQL> SELECT * FROM t1 NATURAL JOIN t2; 
C1 C2  C3
-- -- ---
 1 10 100
 2 20 200
 3 30 300
3 rows selected.

gSQL> SELECT * FROM t1 INNER JOIN t2 USING ( c1 );
C1 C2  C3
-- -- ---
 1 10 100
 2 20 200
 3 30 300
3 rows selected.
```

<a id="9876507bf6021c58"></a>
##### &lt;join specification&gt;

조인 조건을 기술한다.  
&lt;join condition&gt;은 join 구문의 왼쪽 row와 오른쪽 row를 조인할 조건을 기술한다.  
&lt;named columns join&gt;은 왼쪽 row와 오른쪽 row에 대해 동일한 &lt;column name&gt;이 존재하는 경우 이를 나열하여 조인 조건을 기술한다.

```
t1 ( C1 INTEGER, C2 INTEGER )
t2 ( C1 INTEGER, C3 INTEGER )

t1 ( 1, 10 ), ( 2, 20 ), ( 3, 30 )
t2 ( 1, 100 ), ( 2, 200 ), ( 3, 300 )

• <join condition>
gSQL> SELECT * FROM t1 INNER JOIN t2 ON t1.c1 = t2.c1;
C1 C2 C1  C3
-- -- -- ---
 1 10  1 100
 2 20  2 200
 3 30  3 300
3 rows selected.

• <named columns join>
gSQL> SELECT * FROM t1 INNER JOIN t2 USING ( c1 );
C1 C2  C3
-- -- ---
 1 10 100
 2 20 200
 3 30 300
3 rows selected.
```

<a id="ee3c3202c6614eb9"></a>
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

<a id="f99286f1f9730645"></a>
#### 호환성

**SQL 표준 호환성**

<a id="c2915b1ed438cc51"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F401 | Extended joined table | O |
| F402 | Named column joins for LOBs, arrays, and multisets | X |
| F403 | Partitioned join tables | X |

<a id="d9b9d6527a6d2f57"></a>
#### 참조

관련 내용은 [from clause](#f9a5b2d81f65a8aa)를 참조한다.

<a id="21c50afccf7f4c56"></a>
### where clause

<a id="27a3ac2ccf23f3e0"></a>
#### 기능

&lt;from clause&gt; 결과에 &lt;search condition&gt;을 적용한다.

<a id="fcd3658ca485621f"></a>
#### 구문

```
<where clause> ::=
    WHERE <search condition>
```

<a id="a543ed7c94c713a9"></a>
#### 구문 규칙 및 파라미터

<a id="550bbb32c98a3f71"></a>
##### &lt;where clause&gt;

WHERE 키워드 뒤에는 boolean type을 반환하는 &lt;search condition&gt;이 와야 한다.

<a id="fd599076cdf6e1a5"></a>
#### 설명

&lt;where clause&gt;에 대한 자세한 내용은 [Conditions](11-sql-elements.md#7eb55c6cc8416c9a)을 참고한다.

<a id="c787a9c818b3928a"></a>
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

<a id="625450d7db702236"></a>
#### 호환성

**SQL 표준 호환성**

<a id="679dfc98c043a3f1"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F441 | Extended set function support | O |

<a id="c305149861ca9edf"></a>
#### 참조

관련 내용은 [query specification](#b2068000ef8bfb23)을 참조한다.

<a id="ba90ae370cb956ae"></a>
### group by clause

<a id="6eef4f3e6135f708"></a>
#### 기능

이전 구문들이 처리한 결과에 &lt;group by clause&gt;를 적용한 grouped table을 기술한다.

<a id="a4fc38c05d71da67"></a>
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

<a id="bd56a814e87d819d"></a>
#### 사용 범위 및 접근 권한

&lt;group by clause&gt;를 수행하기 위해 별도의 접근 권한이 필요한 것은 아니다.

<a id="ad6e0ed11e08190e"></a>
#### 구문 규칙 및 파라미터

<a id="422f5693fcb3e4a9"></a>
##### &lt;ordinary grouping set&gt;

하나 이상의 &lt;grouping column reference&gt;로 구성한다.  
LONG type (LONG VARCHAR, LONG VARBINARY)은 지원하지 않는다.  

• SELECT c1, sum(c2) FROM t1 GROUP BY c1;  
• SELECT sum(c1) FROM t1 GROUP BY NULL;

<a id="31b203dc41e5920c"></a>
##### &lt;empty grouping set&gt;

괄호만 사용하여 기술할 수 있다.

• SELECT sum(c1) FROM t1 GROUP BY ();

<a id="8d07466154f3d19d"></a>
#### 설명

<a id="75f42cc95d4dcc09"></a>
##### &lt;grouping element list&gt;

&lt;group by clause&gt;에 기술된 &lt;grouping element list&gt;를 하나의 GROUPING SET으로 만드는 grouping을 수행한다. GROUPING SET에 존재하는 모든 &lt;grouping element&gt;들과 값이 일치하면 동일한 group으로 처리한다.

- &lt;group by clause&gt;가 기술된 경우 &lt;select list&gt;에는 다음과 같은 표현식이 올 수 있다.
    - 상수
    - &lt;group by clause&gt;에 기술된 &lt;grouping column reference&gt;
    - &lt;group by clause&gt;에 기술된 &lt;grouping column reference&gt;가 포함된 연산식
    - &lt;group by clause&gt;에 기술되어 있지 않은 column의 집계 함수
    - SELECT c1, sum(c2) FROM t1 GROUP BY c1;

<a id="ce4ad2f83d71ff34"></a>
##### &lt;grouping column reference&gt;

&lt;grouping column reference&gt;에는 &lt;column reference&gt; 또는 &lt;value expression&gt;이 올 수 있다.

- &lt;column reference&gt;
    - &lt;query specification&gt;의 &lt;from clause&gt;에 속하는 column들만 참조할 수 있다.
        - SELECT c1 FROM t1 GROUP BY c1;
    - 동일한 column 이름이 존재하는 경우 table 이름 등을 사용하여 column 이름을 명확하게 기술하여야 한다.
        - SELECT t1.c1, t2.c1 FROM t1, t2 GROUP BY t1.c1, t2.c1;

- &lt;value expression&gt;
    - &lt;column reference&gt;를 포함하는 expression 이다.
        - &lt;column reference&gt;를 사용하여 여러 group으로 구분할 수 있다.
        - SELECT sum(c2) FROM t1 GROUP BY c1 + 10;
    - &lt;column reference&gt;를 포함하지 않는 expression 이다.
        - &lt;value expression&gt;의 값이 모두 동일한 상수값이기 때문에 모든 레코드가 단일 group으로 구성된다.
        - &lt;value expression&gt;에 null 값을 기술할 경우, null 값들은 동일한 값으로 취급되어 모든 레코드가 단일 group으로 구성된다.
        - SELECT sum(c1), sum(c2) FROM t1 GROUP BY NULL;

<a id="d3d2d4084daf9d21"></a>
##### &lt;empty grouping set&gt;

&lt;empty grouping set&gt;의 모든 레코드는 단일 group으로 구성된다.  
• SELECT sum(c1), sum(c2) FROM t1 GROUP BY ();

<a id="c229465d73723483"></a>
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

<a id="0ca4555f1753ecfc"></a>
#### 호환성

**SQL 표준 호환성**

<a id="1c1f3b372fc7b91c"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T431 | Extended grouping capabilities | X |
| T432 | Nested and concatenated GROUPING SETS | X |
| T434 | GROUP BY DISTINCT | X |

<a id="268849a08c28ba7b"></a>
#### 참조

관련 내용은 다음을 참조한다.

- [having clause](#57d0f6a864936181)
- [query specification](#b2068000ef8bfb23)

<a id="57d0f6a864936181"></a>
### having clause

<a id="82af78168e59a726"></a>
#### 기능

&lt;search condition&gt;을 만족하지 않는 group을 제거한 grouped table을 기술한다.

<a id="6245aad430d859f1"></a>
#### 구문

```
<having clause> ::=
    HAVING <search condition>
```

<a id="5235998c46f5a7ba"></a>
#### 사용 범위 및 접근 권한

&lt;having clause&gt;를 수행하기 위해 별도의 접근 권한이 필요한 것은 아니다.

<a id="54043839ad83b909"></a>
#### 구문 규칙 및 파라미터

<a id="a3e5299f90664c3e"></a>
##### &lt;having clause&gt;

- &lt;group by clause&gt;에 기술된 &lt;grouping column reference&gt;만 &lt;search condition&gt;에 집계 함수 없이 사용할 수 있다.
    - SELECT c1, sum(c2) FROM t1 GROUP BY c1 HAVING c1 > 3;
- &lt;group by clause&gt;에 기술되지 않은 column은 집계 함수를 사용하여 기술할 수 있다.
    - SELECT c1, sum(c2) FROM t1 GROUP BY c1 HAVING sum(c2) > 100;

<a id="266eaaa18642b6f5"></a>
#### 설명

<a id="97058193db480bbc"></a>
##### &lt;having clause&gt;

&lt;having clause&gt;는 grouping 된 데이터들에 대한 검색 조건을 기술한다.

일반적으로 &lt;group by clause&gt;와 함께 사용되며, &lt;group by clause&gt; 없이 &lt;having clause&gt;를 사용할 경우에는 &lt;empty grouping set&gt;이 있는 것으로 간주한다.

- SELECT sum(c1), sum(c2) FROM t1 HAVING sum(c1) > 0;
- &lt;=&gt; SELECT sum(c1), sum(c2) FROM t1 GROUP BY () HAVING sum(c1) > 0;

&lt;having clause&gt;에는 &lt;group by clause&gt;에 기술된 &lt;grouping column reference&gt;를 기술할 수 있다.  
&lt;group by clause&gt;에 기술되지 않은 column은 집계 함수를 사용하여 기술할 수 있다.

- SELECT c1, sum(c2) FROM t1 GROUP BY c1 HAVING c1 > 3 AND sum(c2) > 100;

<a id="4bb34f5ed3bca5f2"></a>
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

<a id="5548b5a2854c011d"></a>
#### 호환성

**SQL 표준 호환성**

<a id="4e788ea830b430ce"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T301 | Functional dependencies | O |

<a id="45affd90b4321edd"></a>
#### 참조

관련 내용은 다음을 참조한다.

- [group by clause](#ba90ae370cb956ae)
- [Conditions](11-sql-elements.md#7eb55c6cc8416c9a)

<a id="755bc92d9f68eb02"></a>
### order by clause

<a id="01a79fcb1a2e8d79"></a>
#### 기능

검색 결과의 정렬 순서를 기술한다.

<a id="34d79c2848b28202"></a>
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

<a id="938dd1e7646689b3"></a>
#### 사용 범위 및 접근 권한

정렬하기 위해 기술한 &lt;sort key&gt;에 column이 존재하는 경우 column에 대한 접근 권한이 있어야 한다.

<a id="de735689b1ec74e5"></a>
#### 구문 규칙 및 파라미터

<a id="e366cf6df693648c"></a>
##### &lt;order by clause&gt;

- &lt;query specification&gt;에 &lt;set quantifier&gt; DISTINCT가 기술된 경우, &lt;sort key&gt;에는 &lt;select list&gt;에 기술된 expression만 올 수 있다.
    - SELECT DISTINCT c1, c2 FROM t1 ORDER BY c1;
    - (X) SELECT DISTINCT c1, c2 FROM t1 ORDER BY c5;
- &lt;query specification&gt;의 &lt;select list&gt;에 하나 이상의 &lt;set function specification&gt;을 기술한 경우, &lt;sort key&gt;에는 &lt;select list&gt;에 기술된 expression만 올 수 있다.
    - SELECT c1, sum(c2) FROM t1 GROUP BY c1 ORDER BY c1;
    - (X) SELECT c1, sum(c2) FROM t1 GROUP BY c1 ORDER BY c5;
- &lt;set operator&gt; 구문에 &lt;order by clause&gt;를 명시한 경우, 가장 먼저 기술된 &lt;query specification&gt;을 기준으로 &lt;sort key&gt;를 분석한다.
    - SELECT c1, c2 FROM t1 UNION SELECT i1, i2 FROM t3 ORDER BY c1, c2;
    - (X) SELECT c1, c2 FROM t1 UNION SELECT i1, i2 FROM t3 ORDER BY i1, i2;

<a id="9e7a7fa8c35feb58"></a>
##### &lt;sort specification list&gt;

- &lt;ordering specification&gt;
    - ASC
    - DESC
    - 명시하지 않은 경우, 기본값은 ASC이다. 
- &lt;null ordering&gt;
    - NULLS FIRST
    - NULLS LAST
    - 명시하지 않은 경우, 기본값은 NULLS LAST이다.

<a id="a4d1da29c35aa6e2"></a>
##### &lt;sort key&gt;

- &lt;sort key&gt;의 &lt;value expression&gt;이 양의 정수값이면 그 값을 sort key index로 사용한다.
    - 해당 값에 대응되는 &lt;query specification&gt;의 i 번째 &lt;select sublist&gt;를 sort key로 사용한다.
        - SELECT c1, c2 FROM t1 ORDER BY 1;
        - C1을 sort key로 정렬한다.
    - 해당 값에 대응되는 &lt;query specification&gt;의 i 번째 &lt;select sublist&gt;가 존재하지 않는 경우 error를 반환한다.
        - (X) SELECT c1, c2 FROM t1 ORDER BY 3;
- Row subquery나 relation subquery는 &lt;value expression&gt;로 지원되지 않는다.
    - (X) SELECT c1, c2 FROM t1 ORDER BY ( SELECT i1, i2 FROM t2 FETCH FIRST ROW ONLY );
    - T2에 여러 개의 레코드가 존재한다.
        - (X) SELECT c1, c2 FROM t1 ORDER BY ( SELECT i1 FROM t2 );
- 이 외의 &lt;value expression&gt;은 sort key로 사용된다.

<a id="85c5e7e3a2204989"></a>
#### 설명

<a id="d4d1eb24047e0dcb"></a>
##### &lt;order by clause&gt;

&lt;order by clause&gt;는 검색 결과를 정렬하는 방법을 기술한다.

&lt;order by clause&gt;에는 &lt;sort key&gt;들을 콤마 (,) 리스트로 나열할 수 있으며, 나열한 순서대로 각 레코드들의 &lt;sort key&gt;를 비교하여 순서대로 정렬한다.

```
SELECT c1, c2 FROM t1 ORDER BY c1, c2;
```

&lt;sort key&gt;에는 오름차순 정렬 또는 내림차순 정렬을 지정할 수 있는 &lt;ordering specification&gt;을 기술할 수 있는데 생략할 경우에는 오름차순으로 정렬된다.

```
gSQL> SELECT c1 FROM t1;
C1
--
 2
 3
 1
3 rows selected.
```

- 오름 차순 ( ASC )

```
gSQL> SELECT c1 FROM t1 ORDER BY c1;
C1
--
 1
 2
 3
3 rows selected.

gSQL> SELECT c1 FROM t1 ORDER BY c1 ASC;
C1
--
 1
 2
 3
3 rows selected.
```

- 내림 차순 ( DESC )

```
gSQL> SELECT c1 FROM t1 ORDER BY c1 DESC;
C1
--
 3
 2
 1
3 rows selected.
```

&lt;sort key&gt;에는 NULL 값과 NULL이 아닌 값의 순서를 &lt;null ordering&gt;을 사용하여 지정할 수 있는데 생략할 경우에는 NULLS LAST로 정렬된다.

```
gSQL> SELECT c1 FROM t1;
  C1
----
   2
null
   1
3 rows selected.
```

- NULLS LAST

```
gSQL> SELECT c1 FROM t1 ORDER BY c1;    
  C1
----
   1
   2
null
3 rows selected.

gSQL> SELECT c1 FROM t1 ORDER BY c1 NULLS LAST;
  C1
----
   1
   2
null
3 rows selected.
```

- NULLS FIRST

```
gSQL> SELECT c1 FROM t1 ORDER BY c1 NULLS FIRST;
  C1
----
null
   1
   2
3 rows selected.
```

&lt;sort key&gt;에 상수값을 기술할 경우 &lt;select list&gt;에서 해당 값의 순번에 위치한 expression을 &lt;sort key&gt;로 간주한다. 그리고 이 때 기술하는 상수값은 0보다 큰 정수이며, &lt;select list&gt;에 기술한 expression의 전체 개수와 같거나 작아야 한다.

```
gSQL> SELECT c1 FROM t1 ORDER BY 1;
  C1
----
   1
   2
null
3 rows selected.
```

&lt;sort key&gt;에는 LONG type ( LONG VARCHAR, LONG VARBINARY )을 기술할 수 없다.

<a id="743c64faf7bc3b7a"></a>
##### null value와의 비교

- Null value끼리 비교할 경우에는 동일한 값으로 간주한다.
- Null value와 null value가 아닌 값을 비교할 경우에는 다음 규칙을 따른다.
    - NULLS FIRST이고 ASC인 경우: null value < not null value
    - NULLS LAST이고 ASC인 경우: null value > not null value
    - NULLS FIRST이고 DESC인 경우: null value > not null value
    - NULLS LAST이고 DESC인 경우: null value < not null value
- Null value 비교 결과가 UNKNOWN인 경우, 탐색 순서에 따라 정렬한다.

<a id="b7095eac203a5559"></a>
##### 동일한 sort key 값을 가지는 row들의 정렬

Sort key로 구분할 수 없는 row들을 peer라고 하며, peer들은 탐색 순서에 따라 정렬된다.

<a id="acf30bb317b0a03c"></a>
##### &lt;sort key&gt;로 사용되는 &lt;aggregation function&gt;

&lt;query specification&gt;에서 &lt;aggregation function&gt;이 사용되거나 &lt;group by clause&gt;가 기술된 경우, &lt;aggregation function&gt;을 &lt;sort key&gt;로 사용할 수 있다.  
단, &lt;group by clause&gt;가 기술된 경우에만 중첩된 &lt;aggregation function&gt;을 &lt;sort key&gt;로 사용할 수 있다.

```
gSQL> SELECT c1, c2 FROM t1;
C1 C2
-- --
 2  1
 3  5
 1  2
 2 10
 3 10
5 rows selected.

gSQL> SELECT sum(c1) FROM t1 ORDER BY sum(c1);
SUM(C1)
-------
     11
1 row selected.

gSQL> SELECT c1, sum(c2) FROM t1 GROUP BY c1 ORDER BY sum(c2);
C1 SUM(C2)
-- -------
 1       2
 2      11
 3      15
3 rows selected.

gSQL> SELECT sum(c1) FROM t1 GROUP BY c1 ORDER BY sum(sum(c1));
SUM(C1)
-------
      6
1 row selected.
```

<a id="8dda87cd47ce4926"></a>
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

<a id="6e6b06ebd7a4455a"></a>
#### 호환성

**SQL 표준 호환성**

<a id="55b62e951fdba449"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F850 | Top-level &lt;order by clause&gt; in &lt;query expression&gt; | X |
| F851 | &lt;order by clause&gt; in subqueries | O |
| F852 | Top-level &lt;order by clause&gt; in views | O |
| F855 | Nested &lt;order by clause&gt; in &lt;query expression&gt; | O |

<a id="795568aabd8ba562"></a>
#### 참조

관련 내용은 [query expression](#83a1bf13756be069)을 참조한다.

<a id="2e8423d8813ebc76"></a>
### offset limit clause

<a id="faddaaeff5690f61"></a>
#### 기능

검색 결과에 대하여 skip 할 row의 개수와 fetch 할 row의 개수를 기술한다.

<a id="33a00fe1d3261d41"></a>
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

<a id="4d3fd4dea293af48"></a>
#### 사용 범위 및 접근 권한

&lt;offset limit clause&gt;는 접근 권한을 필요로 하지 않는다.

<a id="19e3966706beb4c9"></a>
#### 구문 규칙 및 파라미터

<a id="64416617baf7cfc8"></a>
##### &lt;result offset clause&gt;

- &lt;offset row count&gt; 값은 0과 같거나 큰 양의 정수이어야 한다.
- ROW와 ROWS는 동일한 의미의 키워드로 생략 가능하다.
- 구문을 생략할 경우 OFFSET 0 ROWS 라는 의미이다.

<a id="1d0f1af3d683c221"></a>
##### &lt;fetch limit clause&gt;

- 검색 결과 중 fetch 할 row의 개수를 명시한다.
- 구문을 생략할 경우 LIMIT ALL 이라는 의미이다.

<a id="a9aa8a6af48851ad"></a>
##### &lt;fetch first clause&gt;

- Fetch 할 row의 개수를 명시한다.
- &lt;limit clause&gt;와 함께 사용할 수 없다.
- FIRST와 NEXT는 동일한 의미의 키워드로써 생략할 수 있다.
- ROW ONLY와 ROWS ONLY는 동일한 의미의 키워드로써 생략할 수 있다.
- &lt;fetch row count&gt; 
    - 0 보다 큰 양의 정수이어야 한다.
    - 생략 가능하며 생략할 경우 그 값은 1이다.

<a id="a9e285c38ace622d"></a>
##### &lt;limit clause&gt;

- Fetch 할 row의 개수를 지정한다.
- 질의 결과 중 skip 할 row의 개수와 fetch 할 row의 개수를 동시에 지정할 수 있다.
- &lt;fetch first clause&gt;와 함께 사용할 수 없다.
- LIMIT &lt;fetch row count&gt;로 사용한 경우
    - &lt;fetch row count&gt;는 0보다 큰 양의 정수이어야 한다.
    - 이 구문은 FETCH FIRST &lt;fetch row count&gt; ROWS ONLY와 동일한 의미이다.
- LIMIT &lt;offset row count&gt;, &lt;fetch row count&gt;로 사용한 경우
    - &lt;result offset clause&gt;와 동시에 사용할 수 없다.
    - &lt;offset row count&gt;는 0과 같거나 큰 양의 정수이어야 한다.
    - &lt;fetch row count&gt;는 0보다 큰 양의 정수이어야 한다.
    - 이 구문은 OFFSET &lt;offset row count&gt; ROWS FETCH FIRST &lt;fetch row count&gt; ROWS ONLY과 동일한 의미이다.
- LIMIT ALL로 사용한 경우 fetch 할 row의 개수에 제한이 없다.

<a id="da0f11ac98611409"></a>
#### 설명

<a id="e9cf0723de0c4fc3"></a>
##### &lt;result offset clause&gt;

검색한 결과 중에 &lt;offset row count&gt; 번 째 row부터 fetch 한다. 만일 &lt;offset row count&gt;가 검색한 결과가 row의 개수와 같거나 크면 fetch row 개수는 0이다.

```
gSQL> SELECT c1 FROM t1;
C1
--
 1
 2
 3
3 rows selected.

gSQL> SELECT c1 FROM t1 OFFSET 1;
C1
--
 2
 3
2 rows selected.

gSQL> SELECT c1 FROM t1 OFFSET 3;
no rows selected.
```

<a id="ce647f6a3d07e6a8"></a>
##### &lt;fetch first clause&gt;

검색한 결과 중에 &lt;fetch row count&gt; 개수만큼만 fetch한다.

```
gSQL> SELECT c1 FROM t1;
C1
--
 1
 2
 3
3 rows selected.

gSQL> SELECT c1 FROM t1 FETCH FIRST 2 ROWS ONLY;
C1
--
 1
 2
2 rows selected.
```

<a id="4b1d3668754fc383"></a>
##### &lt;limit clause&gt;

LIMIT &lt;fetch_row_count&gt;를 사용한 경우, 검색한 결과 중에 &lt;fetch row count&gt; 개수만큼만 fetch한다.

LIMIT &lt;offset row count&gt;, &lt;fetch row count&gt;를 사용한 경우, 검색한 결과 중에 &lt;offset row count&gt;번째 row부터 &lt;fetch row count&gt; 개수만큼만 fetch한다.

LIMIT ALL을 사용한 경우 개수 제한없이 검색한 결과를 fetch한다.

```
gSQL> SELECT c1 FROM t1;
C1
--
 1
 2
 3
3 rows selected.

• LIMIT <fetch_row_count>
gSQL> SELECT c1 FROM t1 LIMIT 2;
C1
--
 1
 2
2 rows selected.

• LIMIT <offset row count>, <fetch_row_count>
gSQL> SELECT c1 FROM t1 LIMIT 1, 1;
C1
--
 2
1 row selected.

• LIMIT ALL
gSQL> SELECT c1 FROM t1 LIMIT ALL;
C1
--
 1
 2
 3
3 rows selected.
```

<a id="ad1b17c5de1a80eb"></a>
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

다음은 &lt;result offset clause&gt;과 &lt;fetch limit clause&gt;를 사용한 SELECT 구문의 예이다.

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

<a id="a81e70d14147ec95"></a>
#### 호환성

**SQL 표준 호환성**

<a id="eb2ff5553daebda1"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F861 | Top-level &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| F862 | &lt;result offset clause&gt; in subqueries | O |
| F863 | Nested &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| F864 | Top-level &lt;result offset clause&gt; in views | O |
| F865 | dynamic &lt;offset row count&gt; in &lt;result offset clause&gt; | X |

<a id="72ceb9751f3faad0"></a>
### set operator

<a id="680eca0da2badb9e"></a>
#### 기능

부질의 (subquery) 결과들에 대한 집합 (set) 연산을 수행한다.

<a id="d3040f2315cd8397"></a>
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

<a id="045e168f537fbb1a"></a>
#### 사용 범위 및 접근 권한

&lt;set operator&gt; 구문을 사용하려면 각 &lt;set operator term&gt;에 나타나는 &lt;query expression&gt;에 대한 접근 권한이 있어야 한다.

<a id="46b617b408b06c02"></a>
#### 구문 규칙 및 파라미터

<a id="4273b8f26d421623"></a>
##### &lt;set operator&gt;

- 부질의 (subquery) 간의 집합 연산을 기술한다.
- 각 부질의 (subquery)의 &lt;select list&gt; target 개수가 모두 동일해야 하며, 매칭되는 target들은 모두 동일한 data type group에 속해야 한다.
- 첫 번째 부질의 (subquery)의 &lt;select list&gt; target 이름이 &lt;set operator&gt; 결과 target의 대표 이름이 된다.
    - gSQL> SELECT c1 AS NAME FROM t1 UNION SELECT i1 FROM t2;  
      NAME  
      ----  
      1  
      2  
      2 rows selected.
- 괄호 등을 사용하여 명확하게 수행 순서를 기술하지 않을 경우, 왼쪽에 기술한 부질의 (subquery)에서 오른쪽에 기술한 부질의 (subquery) 순서로 평가하여 처리한다.
- &lt;set operator&gt;의 각 operator는 다음을 의미한다.
    - UNION
        - UNION ALL: 부질의 (subquery) 결과들에서 중복을 제거하지 않고 합집합으로 처리한다.
        - UNION DISTINCT: 부질의 (subquery) 결과들에서 중복을 제거하여 합집합으로 처리한다.
        - ALL/ DISTINCT 중 하나도 기술하지 않을 경우, DISTINCT를 기술한 것과 동일하게 동작한다.
    - EXCEPT
        - EXCEPT ALL: 부질의 (subquery) 결과들에서 중복을 제거하지 않고 차집합으로 처리한다.
        - EXCEPT DISTINCT: 부질의 (subquery) 결과들에서 중복을 제거하여 차집합으로 처리한다.
        - ALL/ DISTINCT 중 하나도 기술하지 않을 경우, DISTINCT를 기술한 것과 동일하게 동작한다.
    - MINUS
        - EXCEPT의 alias로서 EXCEPT와 동일하게 동작한다.
    - INTERSECT
        - INTERSECT ALL: 부질의 (subquery) 결과들에서 중복을 제거하지 않고 교집합으로 처리한다.
        - INTERSECT DISTINCT: 부질의 (subquery) 결과들에서 중복을 제거하여 교집합으로 처리한다.
        - ALL/ DISTINCT 중 하나도 기술하지 않을 경우, DISTINCT를 기술한 것과 동일하게 동작한다.

<a id="4b9ee2a074e49dc1"></a>
##### &lt;query term&gt;

하나의 부질의 (subquery)를 기술한다.  
자세한 내용은 [query expression](#83a1bf13756be069) 절을 참조한다.

<a id="cf280f239a053efb"></a>
#### 설명

<a id="4c1ef5f10162b141"></a>
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

<a id="e3856f3ccb47f68e"></a>
![SET 연산 결과](../assets/images/3068bde6f97a5ccd.png)

<a id="6ae13ec8f885449e"></a>
##### 연산자 우선 순위

&lt;set operator&gt;의 연산자 우선순위는 다음과 같다.

- 괄호 ( ) 우선 
- INTERSECT 우선 
- UNION, EXCEPT는 left-right로 기술한 순서 우선

<a id="664b2df56c2c2bd3"></a>
##### &lt;set operator&gt;의 결과 타입

&lt;set operator&gt; 모든 부질의의 i 번째 column은 동일한 계열의 데이터 타입이어야 하며, [결과 타입 조합 규칙](11-sql-elements.md#933953bbf127dad3)에 따라 결과 타입이 결정된다.  
단, LONG VARCHAR와 LONG VARBINARY 타입은 UNION ALL만 사용할 수 있다.

<a id="cb6147a2eed8fc41"></a>
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

<a id="8ca6b6d7ed63d030"></a>
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

<a id="c1e4a9565b6ea31e"></a>
#### 호환성

**SQL 표준 호환성**

<a id="66027c234ad81fcf"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F302 | INTERSECT table operator | O |
| F301 | CORRESPONDING | X |
| T551 | Optional key words for default syntax | O |
| F304 | EXCEPT ALL table operator | O |

<a id="788b7a878d2c8238"></a>
#### 참조

관련 내용은 [query expression](#83a1bf13756be069)을 참조한다.

<a id="fce639de96024211"></a>
### subquery

<a id="75b56415a042804b"></a>
#### 기능

&lt;query expression&gt;에서 파생되는 scalar value, row, table 등을 기술한다.

<a id="54645db9e4869022"></a>
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

<a id="fa0988fffc3df2f1"></a>
#### 사용 범위 및 접근 권한

&lt;subquery&gt;에 존재하는 &lt;query expression&gt;에 대한 접근 권한이 있어야 한다.

<a id="57b6db0a178ab78e"></a>
#### 구문 규칙 및 파라미터

<a id="f58e930df2827e1c"></a>
##### &lt;scalar subquery&gt;

- &lt;query expression&gt;에 존재하는 target의 개수는 한 개이어야 한다.
- &lt;query expression&gt;에서 반환된 row의 개수에 따른 결과값은 다음과 같다.
    - 0 개의 row가 반환된 경우, 결과값은 NULL 이다.
    - 한 개의 row가 반환된 경우, 결과값은 해당 row에 포함된 결과값이다.
    - 두 개이상의 row가 반환된 경우, exception error가 발생한다.

<a id="9b1d1c954ecb1081"></a>
##### &lt;row subquery&gt;

- &lt;query expression&gt;에 존재하는 target의 개수는 두 개 이상이어야 한다.
- &lt;query expression&gt;에서 반환된 row의 개수에 따른 결과값은 다음과 같다.
    - 0 개의 row가 반환된 경우, 결과값은 모든 column이 NULL인 row이다.
    - 한 개의 row가 반환된 경우, 결과값은 해당 row이다.
    - 두 개 이상의 row가 반환된 경우, exception error가 발생한다.

<a id="005624c03467a861"></a>
##### &lt;table subquery&gt;

- &lt;query expression&gt;에 존재하는 target의 개수는 한 개 이상이어야 한다.
- &lt;query expression&gt;에서 반환된 row의 개수에 따른 결과값은 다음과 같다.
    - 0 개의 row가 반환된 경우, 결과값은 no rows이다.
    - 한 개 이상의 row가 반환된 경우, 결과값은 해당 row이다.

<a id="4244e9ce9e5313d5"></a>
#### 설명

<a id="8c0d9f8f426d38ff"></a>
##### &lt;scalar subquery&gt;

&lt;scalar subquery&gt;는 결과값으로 한 개의 column을 갖는 한 개의 row를 반환하는 subquery이다. &lt;scalar subquery&gt;의 target은 하나만 존재해야 하며, 결과의 data type은 target의 data type을 따른다.

&lt;scalar subquery&gt;는 &lt;select list&gt;의 target에 단독으로 쓰일 수 있으며, 단일 column만 갖는 연산자에 쓰일 수 있다.

<a id="5e4a56478d35b0e9"></a>
##### &lt;row subquery&gt;

&lt;row subquery&gt;는 결과값으로 두 개 이상의 column을 갖는 한 개의 row를 반환하는 subquery이다. &lt;row subquery&gt;의 target은 두 개 이상 존재해야 하며, 결과의 data type은 target들 각각의 data type을 따른다.

&lt;row subquery&gt;는 &lt;select list&gt;의 target에 단독으로 쓰일 수 없으며, 둘 이상의 column을 갖는 row 연산자에만 쓰일 수 있다.

<a id="5d3a98e12bfe69c7"></a>
##### &lt;table subquery&gt;

&lt;table subquery&gt;는 결과값으로 한 개 이상의 column을 갖는 한 개 이상의 row를 반환하는 subquery이다. &lt;table subquery&gt;의 target은 한 개 이상 존재해야 하며, 결과의 data type은 target들 각각의 data type을 따른다.

&lt;table subquery&gt;는 &lt;select list&gt;의 target에 단독으로 쓰일 수 없으며, IN, NOT IN, EXISTS, NOT EXISTS, quantify operator 등의 연산자에 쓰일 수 있다.

<a id="533cdfd754277d3c"></a>
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

<a id="3d364ad5aee7a87c"></a>
#### 호환성

**SQL 표준 호환성**

<a id="f26b28cdff3aefe8"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F471 | Scalar subquery values | O |
| F641 | Row and table constructors | X |
| T501 | Enhanced EXISTS predicate | O |
| E061-11 | Subqueries in IN predicate | O |
| E061-12 | Subqueries in quantified comparison predicate | O |
| E061-12 | Correlated subqueries | O |

<a id="ff29f21d84dc7455"></a>
#### 참조

관련 내용은 다음을 참조한다.

- [from clause](#f9a5b2d81f65a8aa)
- [where clause](#21c50afccf7f4c56)

<a id="18aca4d715cae99a"></a>
### hint clause

Query를 수행할 때 사용할 hint를 기술한다.  
자세한 내용은 [SQL Hint](15-sql-tuning.md#68e2aa9f8a1e31e4)를 참조한다.

<a id="04b98fd332b9b4a3"></a>
## SELECT .. FOR UPDATE

<a id="7d26e0b81312191c"></a>
### 기능

SELECT 구문의 결과 집합을 갱신할지 여부를 설정한다.

<a id="ea08fe0994941692"></a>
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

<a id="ba168c6d56b427af"></a>
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

<a id="efa685b37c465774"></a>
### 구문 규칙 및 파라미터

<a id="8bf0c71dd122640d"></a>
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

SELECT 구문에 대한 자세한 내용은 [query expression](#83a1bf13756be069)을 참조한다.

<a id="2d09fe846e6bf747"></a>
#### &lt;updatability clause&gt;

결과 집합에 대한 row를 변경할지 여부를 지정한다.

- FOR READ ONLY 
    - 읽기 전용 질의임을 선언한다. 
- FOR UPDATE 
    - 쓰기 가능한 질의임를 선언한다. 
    - 질의를 수행할 때 해당 트랜잭션이 종료될 때까지 다른 트랜잭션에 의해 변경되지 않도록 해당 row 들에 대한 x lock을 획득한다. 
    - &lt;query expression&gt;이 updatable query 여야 한다.

<a id="23fefb7dbd3681e1"></a>
#### FOR UPDATE OF …

질의를 수행할 때 lock 획득과 관련된 column들을 나열한다.

- FOR UPDATE OF 구문에 나열하는 column 
    - &lt;query expression&gt;의 FROM 절에 나열된 table의 갱신 가능한 column이어야 한다. 
    - 나열된 column의 table에 대해 lock을 획득한다. 
- FOR UPDATE만 사용하는 경우 
    - &lt;query expression&gt;의 FROM 절에 나열된 table들의 모든 갱신 가능한 column을 나열한 것과 동일한 의미이다. 
    - 모든 column의 table에 대해 lock을 획득한다.

<a id="41594f61523c5eee"></a>
#### &lt;lock wait mode&gt;

FOR UPDATE 구문과 함께 사용하며, lock 획득 방법을 지정한다.

- WAIT 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock을 획득하며 
    - Lock을 획득할 수 있을 때까지 대기한다. 
- WAIT second 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock을 획득하며 
    - 지정한 시간동안 lock을 획득할 수 없을 경우, 에러가 발생한다. 
    - 초 단위이며 0 ~ 1000000000 까지의 값을 사용할 수 있다. 
- NOWAIT 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock을 획득하며 
    - 즉시 lock을 획득할 수 없을 경우, 에러가 발생한다.
- 명시하지 않을 경우, 기본값은 WAIT이다.

<a id="3f2b0c47418cc167"></a>
### 설명

SELECT 구문은 transaction의 종료 여부와 관계없이 row에 대한 fetch를 지속할 수 있는 반면에, SELECT .. FOR UPDATE 구문은 row들에 대한 lock을 획득하기 때문에 transaction이 종료되면 fetch 할 수 없다.

> Cursor holdability  
> 
> 
> - WITH HOLD
>     - Transaction 종료 여부와 관계없이 fetch를 지속할 수 있다.
>     - Fetch across commit 이라고도 한다.
> 
> 
> 
> - WITHOUT HOLD
>     - Transaction이 종료되면 fetch 할 수 없다.
> 

<a id="933ff08e648c29cb"></a>
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

<a id="005777e7ab451e76"></a>
### 호환성

SQL 표준에서는 &lt;select for update statement&gt;를 정의하지 않고 있는데, 이는 [DECLARE cursor_name](#45b9d98474d5f09d) 구문을 사용하여 정의할 수 있다.

<a id="a345298536f40392"></a>
## SELECT .. INTO

<a id="88a49b7a29818550"></a>
### 기능

질의를 통해 row 하나를 검색하고, 검색한 row의 값을 호스트 변수로 얻어온다.

<a id="d10c593e5026cfae"></a>
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

<a id="c090b7e3ceac234b"></a>
### 사용 범위 및 접근 권한

&lt;select statement: single row&gt; 구문을 수행하려면 사용자에게 구문에 사용된 모든 테이블에 대한 다음 권한 중 하나가 있어야 한다.

- 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
- 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- SELECT ANY TABLE ON DATABASE

<a id="49bfc9b83e7d51f1"></a>
### 구문 규칙 및 파라미터

<a id="9da6dad2d8edbd09"></a>
#### &lt;hint clause&gt;

질의를 수행하기 위한 힌트를 기술한다.  
자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 [hint clause](#18aca4d715cae99a) 절을 참조한다.

<a id="33b698cfa59c2b03"></a>
#### &lt;set quantifier&gt;

질의 결과에서 중복을 제거할지 여부를 기술한다.  
자세한 내용은 [query specification](#b2068000ef8bfb23) 절을 참조한다.

<a id="4f512982cb70b35d"></a>
#### &lt;select list&gt;

질의 결과로부터 검색할 column을 기술한다.  
자세한 내용은 [select list](#df8abc1a6f23e3cc) 절을 참조한다.

<a id="914579ce411ed379"></a>
#### INTO &lt;select target list&gt;

INTO 절에 기술된 변수의 개수는 &lt;select list&gt;에 기술된 expression의 개수와 동일해야 한다.

<a id="b918c1628e51cd2a"></a>
#### &lt;table expression&gt;

검색 조건 등 질의 내용을 기술한다.  
자세한 내용은 [query specification](#b2068000ef8bfb23) 절을 참조한다.

<a id="a570d7e7b77bdcca"></a>
### 설명

검색할 row가 한 건 이하여야 한다.   
두 건 이상의 row가 검색될 경우, 에러가 발생한다.

<a id="ed7cbaf52a133ea2"></a>
#### SELECT 구문들의 차이점

- &lt;select statement&gt;
    - 조건에 부합하는 다수의 row를 검색하고, 검색한 row를 SQLFetch() 등의 API로 검색할 수 있다. 
    - 예: SELECT c1 FROM t1 WHERE c1 > 0; 
- &lt;select statement: single row&gt;
    - 조건에 부합하는 한 건 이하의 row를 검색할 수 있으며, 검색한 row가 한 건일 경우 INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: SELECT c2 INTO :v1 FROM t1 WHERE c1 = 0;

<a id="528adf5dc668977f"></a>
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

<a id="7fdc38fa2da19dfc"></a>
## SELECT .. INTO .. FOR UPDATE

<a id="ff56cac766a6e1bd"></a>
### 기능

질의를 통해 row 하나를 검색하여 갱신을 수행할지 여부를 설정한 후, 검색한 row의 값을 호스트 변수에 얻어온다.

<a id="f0a0022e0f1cd0b5"></a>
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

<a id="edcbda536813fece"></a>
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

<a id="be33026ff16bdd4e"></a>
### 구문 규칙 및 파라미터

<a id="3469cc74e3ca3115"></a>
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

<a id="a8bc6db245a30ba0"></a>
#### &lt;updatability clause&gt;

결과 집합에 대해 row를 변경할지 여부를 지정한다.

- FOR READ ONLY 
    - 읽기 전용 질의임을 선언한다. 
- FOR UPDATE 
    - 쓰기 가능한 질의임를 선언한다. 
    - 질의를 수행할 때 해당 트랜잭션이 종료될 때까지, 다른 트랜잭션에 의해 변경되지 않도록 해당 row들에 대한 x lock을 획득한다. 
    - &lt;query expression&gt;이 updatable query이어야 한다.

<a id="4b5e76719c3510ed"></a>
#### FOR UPDATE OF …

질의를 수행할 때 lock 획득과 관련된 column을 나열한다.

- FOR UPDATE OF 구문에 나열하는 column 
    - &lt;query expression&gt;의 FROM 절에 나열된 table의 갱신 가능한 column이어야 한다. 
    - 나열된 column의 table에 대해 lock을 획득한다. 
- FOR UPDATE 만 사용하는 경우 
    - &lt;query expression&gt;의 FROM 절에 나열된 table들의 모든 갱신 가능한 column을 나열한 것과 동일한 의미이다. 
    - 모든 column의 table에 대해 lock을 획득한다.

<a id="9937e67a700f9315"></a>
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

<a id="38768ddc45def171"></a>
#### &lt;hint clause&gt;

질의를 수행하기 위한 힌트를 기술한다.  
자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 [hint clause](#18aca4d715cae99a) 절을 참조한다.

<a id="eb44e5974a91f4aa"></a>
#### &lt;set quantifier&gt;

질의 결과에서 중복을 제거할지 여부를 기술한다.  
자세한 내용은 [query specification](#b2068000ef8bfb23) 절을 참조한다.

<a id="8d9bc6bd63a99155"></a>
#### &lt;select list&gt;

질의 결과로부터 검색할 column을 기술한다.  

자세한 내용은 [select list](#df8abc1a6f23e3cc) 절을 참조한다.

<a id="99c307d4ad616fa0"></a>
#### INTO &lt;select target list&gt;

INTO 절에 기술된 변수의 개수는 &lt;select list&gt; 에 기술된 expression의 개수와 동일해야 한다.

<a id="f707ab335fd72f89"></a>
#### &lt;table expression&gt;

검색 조건 등의 질의 내용을 기술한다.  
자세한 내용은 [query specification](#b2068000ef8bfb23) 절을 참조한다.

<a id="75115e57545c38ab"></a>
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

<a id="f381dae043cbdd72"></a>
#### SELECT 구문들의 차이점

- &lt;select for update statement&gt;
    - 조건에 부합하는 다수의 row를 검색하여 갱신 수행 여부를 설정하고, 검색한 row를 SQLFetch() 등의 API로 검색할 수 있다. 
    - 예: SELECT c1 FROM t1 WHERE c1 > 0 FOR UPDATE; 
- &lt;select for update statement: single row&gt;
    - 조건에 부합하는 한 건 이하의 row를 검색하여 갱신 수행 여부를 설정하고, 검색한 row가 한 건일 경우 INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: SELECT c2 INTO :v1 FROM t1 WHERE c1 = 0 FOR UPDATE;

<a id="90d7950785aebc16"></a>
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

<a id="b03c31ee2ed3a9e1"></a>
### 참조

관련 내용은 다음을 참조한다.

- [SELECT .. FOR UPDATE](#04b98fd332b9b4a3)
- [SELECT .. INTO](#a345298536f40392)

<a id="0ec9d72169df1ed8"></a>
## SET CONSTRAINTS

<a id="74400080a960ebbc"></a>
### 기능

트랜잭션 내에서 지연가능한 제약 조건들의 검사 시점을 IMMEDIATE 또는 DEFERRED로 설정한다.

<a id="37b8392d47376060"></a>
### 구문

```
<set constraints mode statement> ::=
    SET { CONSTRAINT | CONSTRAINTS } <constraint name list> { DEFERRED | IMMEDIATE }
    ;

<constraint name list> ::=
      ALL
    | <constraint name> [, ...]
```

<a id="a8d4c8a0d9e959b7"></a>
### 사용 범위 및 접근 권한

SET CONSTRAINTS를 수행하기 위해 별도의 접근 권한이 필요한 것은 아니다.

> Cluster system에서 지원하지 않는다.

<a id="1b5263b4dd3ecc88"></a>
### 구문 규칙 및 파라미터

<a id="8202bec0d683e094"></a>
#### CONSTRAINT | CONSTRAINTS

CONSTRAINT와 CONSTRAINTS는 동일한 의미의 키워드인데 SQL 표준은 CONSTRAINTS 이다.

<a id="bf6fa3dbb951b45e"></a>
#### &lt;constraint name list&gt;

제약 조건 이름 목록을 기술하거나, ALL 키워드를 사용하여 지연 가능한 제약 조건을 모두 명시할 수 있다.   
&lt;constraint name&gt;을 기술할 경우, 제약 조건은 지연 가능해야 한다.   
ALL은 지연 가능한 모든 제약 조건을 의미한다.

<a id="813adedcd5298625"></a>
#### DEFERRED | IMMEDIATE

명시한 지연 가능한 제약 조건들의 검사 시점을 설정한다.

- IMMEDIATE
    - DML을 수행할 때 해당 제약 조건들을 검사한다.
    - 트랜잭션이 해당 제약 조건들을 위반할 경우, 에러가 발생한다
- DEFERRED
    - COMMIT을 수행할 때 해당 제약 조건들을 검사한다.

트랜잭션이 진행 중이면, 검사 시점은 현재 트랜잭션에 설정되며, 트랜잭션이 진행 중이 아닌 경우에는 다음 트랜잭션에 설정된다.   
트랜잭션이 종료되면 다음 트랜잭션에 영향을 미치지 않는다.

<a id="7ecfca22383f654e"></a>
### 설명

<a id="277c1bae694efdd5"></a>
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

<a id="a0601401a32e94a6"></a>
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

<a id="33f4f458591a9127"></a>
#### 트랜잭션 제어 언어

SET CONSTRAINTS 구문은 [SAVEPOINT savepoint_specifier](#f7bc15577098099a) 구문과 같이 트랜잭션 진행 중에 사용하는 트랜잭션 제어 언어이다.  
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

<a id="60dc2187eb0b8ceb"></a>
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

<a id="012b8a0a199a322e"></a>
### 호환성

SQL 표준에서는 CONSTRAINT 키워드 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="24f8e85fef170580"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F721 | Deferrable constraints | O |

<a id="a823bba4a6b9123d"></a>
### 참조

관련 내용은 다음을 참조한다.

- 제약 조건 생성
    - [CREATE TABLE](#9b82da6d66aabe8c)
    - [ALTER TABLE name ADD CONSTRAINT](#01291e4c7e6b5226)
    - [ALTER TABLE name ADD COLUMN](#435e25d60c5f411d)
    - [ALTER TABLE name ALTER COLUMN](#f9d752692bc80a55)

- 제약 조건 변경: [ALTER TABLE name ALTER CONSTRAINT](#e11c16dd8992ad1d)

- 제약 조건 검사시점 제어: [SET CONSTRAINTS](#0ec9d72169df1ed8)

<a id="f764bc65dcc3237c"></a>
## SET SESSION AUTHORIZATION user_identifier

<a id="5f770917e850ce9a"></a>
### 기능

Session user와 current user를 변경한다.

<a id="0d621783fd76e883"></a>
### 구문

```
<set session user identifier statement> ::=
    SET SESSION AUTHORIZATION user_identifier
    ;
```

<a id="46bc108355735b89"></a>
### 사용 범위 및 접근 권한

&lt;set session user identifier statement&gt; 구문을 수행하려면 logon 사용자에게 ACCESS CONTROL ON DATABASE 권한이 있어야 한다.

사용자 정보는 다음과 같은 세가지 형태로 관리된다.

- Logon user 
    - Login 한 user로써 connection을 닫을 때까지 유지된다. 
- Session user 
    - 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다. 
- Current user 
    - 일반적으로 session user와 동일하지만 PSM이나 view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다. 
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="8eb9b89dc7062c19"></a>
### 구문 규칙 및 파라미터

<a id="4c542819bcb6e4fd"></a>
#### user_identifier

변경할 사용자의 이름이다.

<a id="8510e63711b4c82c"></a>
### 설명

SET SESSION AUTHORIZATION 구문을 수행한 이후의 모든 구문은 session user를 기준으로 수행되므로, session user에 대한 권한을 검사하고 객체를 생성할 때의 소유자 역시 session user가 된다.

<a id="6b7805e1781d2d44"></a>
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

<a id="3d009bf4bcfcf6c4"></a>
### 호환성

**SQL 표준 호환성**

<a id="2275aa4af08fe244"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F321 | User authorization | O |

<a id="00e02ba4f4d47f2e"></a>
## SET SESSION CHARACTERISTICS AS transaction_mode

<a id="f21b0e812743ecfa"></a>
### 기능

세션의 트랜잭션 속성을 설정한다.

<a id="7d750a0ea8219bb0"></a>
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

<a id="6997bc0ffcde45fd"></a>
### 구문 규칙 및 파라미터

<a id="4fae91537328a068"></a>
#### &lt;transaction_access_mode&gt;

다음 트랜잭션의 ACCESS MODE 이다.

- READ ONLY 
- READ WRITE

<a id="23badb33d8165fe6"></a>
#### &lt;isolation_level&gt;

다음 트랜잭션의 ISOLATION LEVEL 이다.

- READ COMMITTED 
- SERIALIZABLE

<a id="b26917216862d18c"></a>
### 설명

SET SESSION CHARACTERISTICS은 세션의 트랜잭션 속성을 설정한다. 즉, session 내에서 생성되는 모든 transaction의 속성이 이를 따른다.

참고로 [SET TRANSACTION transaction_mode](#601ab9d8c9936395) 구문의 경우, 이후에 수행되는 하나의 transaction 속성만 변경한다.

<a id="6c8df04b24b36a68"></a>
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

<a id="edac6649f7e524aa"></a>
### 호환성

**SQL 표준 호환성**

<a id="44a42340b798657a"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F761 | Session management | O |

<a id="dfd0797072c4776d"></a>
### 참조

관련 내용은 [SET TRANSACTION transaction_mode](#601ab9d8c9936395)를 참조한다.

<a id="3a36b7319499c89a"></a>
## SET TIME ZONE

<a id="071c247db7077cf5"></a>
### 기능

세션의 TIMEZONE을 설정한다.

<a id="f8c86e6946e82b68"></a>
### 구문

```
<set local time zone statement> ::=
    SET TIME ZONE <set time zone value>
    ;

<set time zone value> ::= 
    { '[+|-]hh:mm' | LOCAL }
```

<a id="7278929364a5afd8"></a>
### 구문 규칙 및 파라미터

<a id="53382540c74f304b"></a>
#### &lt;set time zone value&gt;

설정할 TIMEZONE 값이다.

- hh:mm: 설정할 TIMEZONE의 GMT OFFSET 이다.
    - Offset 값의 범위는 '-14:00' ~ '+14:00' 이다.
- LOCAL: Session을 생성한 시점의 TIME ZONE 이다.
    - Session을 생성할 때의 TIME ZONE은 client OS의 TIME ZONE으로 설정된다.

<a id="3bfb2ad3d81b8c90"></a>
### 설명

Session의 time zone을 변경하면 함수 [CURRENT_TIME](17-built-in-function-references.md#6f0c3028f6461836), [CURRENT_TIMESTAMP](17-built-in-function-references.md#d8795b1505198a32) 등의 결과값에 영향을 미친다.

<a id="e18a868a751db5ad"></a>
### 사용 예

다음은 session의 time zone을 '+09:00' 으로 변경하는 예이다.

```
gSQL> SET TIME ZONE '+09:00';

Session set.
```

<a id="0ed6beea25d7e087"></a>
### 호환성

**SQL 표준 호환성**

<a id="fa0ebb1263de77bd"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F411 | Time zone specification | O |

<a id="601ab9d8c9936395"></a>
## SET TRANSACTION transaction_mode

<a id="6de7abd924362406"></a>
### 기능

다음 트랜잭션의 속성을 설정한다.

<a id="10ecdbe6c6b02ebf"></a>
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

<a id="d546436cc6344b9f"></a>
### 구문 규칙 및 파라미터

<a id="d27cbd2338aa139f"></a>
#### &lt;transaction_access_mode&gt;

다음 트랜잭션의 ACCESS MODE 이다.

- READ ONLY 
- READ WRITE

<a id="9d9b38dda9a64196"></a>
#### &lt;isolation_level&gt;

다음 트랜잭션의 ISOLATION LEVEL 이다.

- READ COMMITTED 
- SERIALIZABLE

<a id="b4f744badfd57bde"></a>
### 설명

SET TRANSACTION은 다음 트랜잭션의 속성을 설정하며, 다음 트랜잭션이 종료되면 트랜잭션 속성은 기본값으로 복원된다.

<a id="f65d1b30bee9b61f"></a>
### 사용 예

다음에 수행될 transaction을 읽기 전용으로 설정한 예이다.

```
gSQL> SET TRANSACTION READ ONLY;

Transaction set.
```

<a id="e6de00b7f6bf0db5"></a>
### 호환성

**SQL 표준 호환성**

<a id="26e4c34728df5383"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T251 | SET TRANSACTION statement: LOCAL option | X |

<a id="1329aeb3c9895a8c"></a>
### 참조

관련 내용은 [SET SESSION CHARACTERISTICS AS transaction_mode](#00e02ba4f4d47f2e)를 참조한다.

<a id="939f94f77e66a231"></a>
## TRUNCATE TABLE

<a id="d3329cf70b977268"></a>
### 기능

테이블의 모든 row들을 제거한다.

<a id="1b568c3ffb2578f7"></a>
### 구문

```
<truncate table statement> ::= 
    TRUNCATE TABLE table_name 
        [ RESTART IDENTITY | CONTINUE IDENTITY ] 
        [ DROP STORAGE | DROP ALL STORAGE ] 
    ;
```

<a id="34a265aac3715099"></a>
### 사용 범위 및 접근 권한

&lt;truncate table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블의 소유자 
- 테이블에 대해 CONTROL TABLE ON TABLE 
- 테이블이 속한 스키마에 대해 (DROP TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY TABLE ON DATABASE

<a id="907853563ee8842d"></a>
### 구문 규칙 및 파라미터

<a id="26089fb0dc484b8f"></a>
#### table_name

Row들을 제거할 대상 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="e9e3f8f3d9582a6c"></a>
#### [ RESTART IDENTITY | CONTINUE IDENTITY ]

- RESTART IDENTITY 
    - 자동 생성값을 갖는 column (identity column)이 해당 테이블에 존재할 경우 자동으로 값을 재시작한다. 
- CONTINUE IDENTITY 
    - 자동 생성값을 갖는 column (identity column)이 해당 테이블에 존재할 경우 기존값을 변경하지 않는다.
- 명시하지 않을 경우, 기본값은 CONTINUE IDENTITY이다.

<a id="5cb1abc2eb4a2c06"></a>
#### [ DROP STORAGE | DROP ALL STORAGE ]

- DROP STORAGE 
    - 테이블에 할당된 extent 중에 MINSIZE 만큼만 제외하고 나머지 extent들을 제거한다.
- DROP ALL STORAGE 
    - 테이블에 할당된 모든 extent 들을 제거한다.
- 명시하지 않을 경우, 기본값은 DROP STORAGE 이다.

<a id="e7c821b8e93d42ca"></a>
### 설명

TRUNCATE TABLE과 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

<a id="a2da936d91c55a6f"></a>
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

<a id="8e8ca8612cc37c64"></a>
### 호환성

SQL 표준에서는 [ DROP STORAGE | DROP ALL STORAGE ] 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="7cf9d2b8e851d0a0"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F200 | TRUNCATE TABLE statement | O |
| F202 | TRUNCATE TABLE: identity column restart option | O |

<a id="43a8287f83dce60b"></a>
## UPDATE

<a id="4959da0c0a6ba67f"></a>
### 기능

테이블의 row들을 갱신한다.

<a id="7d58e66728c6793c"></a>
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

<a id="8313bedcfc38b3bf"></a>
### 사용 범위 및 접근 권한

&lt;update statement: searched&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- Update 대상인 모든 column에 대해 UPDATE(columns) ON TABLE 
- 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- UPDATE ANY TABLE ON DATABASE

<a id="9d39672c9151eb0e"></a>
### 구문 규칙 및 파라미터

<a id="c934af0913a2fd8e"></a>
#### table_name

Row를 갱신할 대상 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="289f634e2c2bed8b"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="5e1cab1a04f4ea4a"></a>
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

Column 값으로 DEFAULT를 사용할 경우, [CREATE TABLE](#9b82da6d66aabe8c)을 수행할 때 정의한 기본값 (&lt;[default clause&gt;](#c7016df1b3063520) 참조)을 사용하며, 정의되지 않은 경우에는 NULL 값이 할당된다.

<a id="21d7dc323a5d6e5c"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 갱신한다.  
WHERE 조건을 명시하지 않을 경우, 모든 row들을 갱신한다.  
WHERE 조건에 대한 자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 [where clause](#21c50afccf7f4c56)를 참조한다.

<a id="68746260f5073d17"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 &lt;[result offset clause&gt;](#64416617baf7cfc8)를 참조한다.

<a id="63c3fd6fa2e34df0"></a>
#### &lt;fetch limit clause&gt;

Fetch 할 row 의 개수를 명시하는 구문으로 두 가지 방법이 가능하다.

- &lt;fetch first clause&gt; 
    - Fetch 할 row의 개수를 명시한다.
    - 자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 &lt;[fetch first clause&gt;](#a9aa8a6af48851ad)를 참조한다.
- &lt;limit clause&gt;
    - Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
    - 자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 &lt;[limit clause&gt;](#a9e285c38ace622d)를 참조한다.

<a id="9f582e6b05ada5a3"></a>
### 설명

<a id="e0cf76cef0f03646"></a>
#### UPDATE 관련 구문들의 차이점

- [UPDATE](#43a8287f83dce60b)
    - 조건에 부합하는 다수의 row를 갱신한다. 
    - 예: UPDATE t1 SET c2 = c2 + 1 WHERE c1 > 0; 
- [UPDATE name WHERE CURRENT OF cursor_name](#76b352fc38bb3b49)
    - 현재 cursor가 가리키는 row를 갱신한다. 
    - 예: UPDATE t1 WHERE CURRENT OF cursor; 
- [UPDATE name RETURNING](#f05414d90d7bfdb9)
    - 조건에 부합하는 다수의 row를 갱신하며, 갱신한 row들을 [SELECT](#93101dc44f4e210d) 구문과 동일한 방식 (SQLFetch() 등의 API)으로 검색할 수 있다. 
    - 예: UPDATE t1 SET c2 = c2 + 1 WHERE c1 > 0 RETURNING c2; 
- [UPDATE name RETURNING .. INTO](#422b753d8ea6394c)
    - 한 건 이하의 row를 갱신할 수 있으며, 갱신한 row가 한 건일 경우 RETURNING INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: UPDATE t1 SET c2 = c2 + 1 WHERE c1 = 0 RETURNING c2 INTO :v1;

<a id="79ead3a92182aef7"></a>
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

<a id="acaef5c7cd154643"></a>
### 호환성

SQL 표준은 UPDATE 구문에서 다음 절을 정의하지 않고 있다.

- &lt;result offset clause&gt; 
- &lt;fetch limit clause&gt;

**SQL 표준 호환성**

<a id="00fa5bc0bc94e7cd"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="f05414d90d7bfdb9"></a>
## UPDATE name RETURNING

<a id="42d25a90cf199695"></a>
### 기능

테이블의 row들을 갱신하고, 갱신 전의 row들이나 갱신 후의 row들을 검색한다.

<a id="105c734ba1e27fd1"></a>
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

<a id="07fa6a1e575e8aff"></a>
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

<a id="88111776865b17bc"></a>
### 구문 규칙 및 파라미터

<a id="73be4fdbe1413e5d"></a>
#### table_name

Row를 갱신할 대상 테이블의 이름이다.

<a id="89fe96dc8f3bddc8"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="90aef36d5b7c0827"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.  
자세한 내용은 [UPDATE](#43a8287f83dce60b) 구문을 참조한다.

<a id="3d49442b29535ceb"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 갱신한다.  
WHERE 조건을 명시하지 않을 경우, 모든 row들을 갱신한다.  
WHERE 조건에 대한 자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 [where clause](#21c50afccf7f4c56)를 참조한다.

<a id="65385b1451887e32"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 &lt;[result offset clause&gt;](#64416617baf7cfc8)를 참조한다.

<a id="24fc2d99ccc38e9a"></a>
#### &lt;fetch limit clause&gt;

Fetch 할 row의 개수를 명시하는 구문으로써 다음 두 가지 방법을 사용할 수 있다.

- &lt;fetch first clause&gt; 
    - Fetch 할 row의 개수를 명시한다. 
    - 자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 &lt;[fetch first clause&gt;](#a9aa8a6af48851ad)를 참조한다.
- &lt;limit clause&gt;
    - Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
    - 자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 &lt;[limit clause&gt;](#a9e285c38ace622d)를 참조한다.

<a id="80d192429e989fb0"></a>
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

<a id="163605fdf180c3ec"></a>
### 설명

자세한 내용은 [UPDATE 관련 구문들의 차이점](#e0cf76cef0f03646)을 참조한다.

<a id="d882e63257b00428"></a>
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

<a id="1569850002c71208"></a>
### 호환성

SQL 표준에는 &lt;update returning query statement&gt; 구문이 존재하지 않는다.

<a id="422b753d8ea6394c"></a>
## UPDATE name RETURNING .. INTO

<a id="e1ae8e4b71b6f030"></a>
### 기능

테이블 row 한 개를 갱신하고, 갱신한 row의 값을 호스트 변수에 얻어온다.

<a id="4f70f57fb11c6f49"></a>
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

<a id="17a886b577325df3"></a>
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

<a id="8f7fba6482cfe4d4"></a>
### 구문 규칙 및 파라미터

<a id="e2ed7a55e290d676"></a>
#### table_name

Row를 갱신할 대상 테이블의 이름이다.

<a id="277a310b6a8899c9"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="17eef9a5b8df6d38"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.  
자세한 내용은 [UPDATE](#43a8287f83dce60b) 구문을 참조한다.

<a id="1c635976da18d53a"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 갱신한다.  
WHERE 조건을 명시하지 않을 경우, 모든 row들을 갱신한다.  
WHERE 조건에 대한 자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 [where clause](#21c50afccf7f4c56)를 참조한다.

<a id="dcc10b5fd31d8aff"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 &lt;[result offset clause&gt;](#64416617baf7cfc8)를 참조한다.

<a id="3e9163b1e6242817"></a>
#### &lt;fetch limit clause&gt;

Fetch 할 row의 개수를 명시하는 구문으로써 다음 두 가지 방법을 사용할 수 있다.

- &lt;fetch first clause&gt; 
    - Fetch 할 row의 개수를 명시한다. 
    - 자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 &lt;[fetch first clause&gt;](#a9aa8a6af48851ad)를 참조한다.
- &lt;limit clause&gt;
    - Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
    - 자세한 내용은 [SELECT](#93101dc44f4e210d) 구문의 &lt;[limit clause&gt;](#a9e285c38ace622d)를 참조한다.

<a id="d584c9acec658d15"></a>
#### RETURNING .. AS ..

갱신된 row들을 결과 집합으로 하고, 이들 중에서 검색할 column을 기술한다.  
자세한 내용은 [UPDATE name RETURNING](#f05414d90d7bfdb9) 구문의 &lt;[returning clause&gt;](#80d192429e989fb0)를 참조한다.

<a id="8eb38548d2bb98e7"></a>
#### INTO variable_name [, ...]

INTO 절에 기술된 변수의 개수는 RETURNING 절에 기술된 expression의 개수와 동일해야 한다.   
갱신할 row가 한 건 이하여야 한다.   
Row가 두 건 이상 갱신될 경우, 에러가 발생한다.

<a id="336a19d6fb14d7cd"></a>
### 설명

자세한 내용은 [UPDATE 관련 구문들의 차이점](#e0cf76cef0f03646)을 참조한다.

<a id="9f1c971d03043064"></a>
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

<a id="5c40d52d42280063"></a>
### 호환성

SQL 표준에는 &lt;update returning into statement&gt; 구문이 존재하지 않는다.

<a id="76b352fc38bb3b49"></a>
## UPDATE name WHERE CURRENT OF cursor_name

<a id="3c6800a62c3425de"></a>
### 기능

커서가 가리키는 row 하나를 갱신한다.

<a id="8c2c789a7d396dd0"></a>
### 구문

```
<update statement: positioned> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        SET <set clause> [, ...]
        WHERE CURRENT OF cursor_name
    ;
```

<a id="db2dd78920035e3b"></a>
### 사용 범위 및 접근 권한

&lt;update statement: positioned&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- UPDATE 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Update 대상인 모든 column에 대해 UPDATE(columns) ON TABLE 
    - 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - UPDATE ANY TABLE ON DATABASE

<a id="f8b94566f41f342a"></a>
### 구문 규칙 및 파라미터

<a id="0abef578f4eba1ba"></a>
#### table_name

Row를 갱신할 대상 테이블의 이름이다.

<a id="e2fb0742d1263d32"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="b33770c59d315dfb"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.  
자세한 내용은 [UPDATE](#43a8287f83dce60b) 구문을 참조한다.

<a id="f664cdff7594ec8b"></a>
#### cursor_name

cursor_name에 해당하는 커서는 다음 조건들을 만족해야 한다.

- OPEN 된 커서이어야 한다. ([OPEN cursor_name](#ee8cdd33c43f9c76) 참조) 
- 커서를 이용해 FETCH 한 row가 있어야 한다. ([FETCH cursor_name](#bafc38978b00122c) 참조) 
- 커서에 사용된 질의가 table_name을 식별할 수 있어야 한다. ([DECLARE cursor_name](#45b9d98474d5f09d) 참조) 
- table_name에 대해 갱신할 수 있는 커서이어야 한다. ([DECLARE cursor_name](#45b9d98474d5f09d) 참조)

<a id="b3c85f713dce77ef"></a>
### 설명

자세한 내용은 [UPDATE 관련 구문들의 차이점](#e0cf76cef0f03646)을 참조한다.

<a id="486674d77c96ae7f"></a>
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

<a id="71e3849b8135f967"></a>
### 호환성

**SQL 표준 호환성**

<a id="60ec7bec4b72d4ea"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F831 | Full cursor update | O |
| B031 | Basic dynamic SQL | O |

<a id="df295809735ae2db"></a>
### 참조

관련 내용은 [CLOSE cursor_name](#38584f03f4e1823e)을 참조한다.

---

[← 17. Built-in Function References](17-built-in-function-references.md) · [전체 목차](../README.md) · [19. Overview of PSM →](../part-04-psm-manual/19-overview-of-psm.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
