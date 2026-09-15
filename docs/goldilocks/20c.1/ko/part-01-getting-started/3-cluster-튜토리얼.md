<a id="0147cc02b4568a2f"></a>

# 3. Cluster 튜토리얼

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/0147cc02b4568a2f)  
> 태그: `20c.1_30_tag`

[← 2. 튜토리얼](2-튜토리얼.md) · [전체 목차](../README.md) · [4. What's New →](4-what-s-new.md)

<a id="a3a9a8c201efd92b"></a>
## GOLDILOCKS Cluster System 관리

본 장에서는 다수의 GOLDILOCKS database를 이용하여 cluster system을 구성하고 관리하기 위한 기반 지식에 대해 설명한다. 본 장의 내용은 standalone database와 비교하여 cluster system에 추가된 부분이나 cluster system만 가지는 특징 위주로 설명하였으므로 이를 이해하기 위해서는 standalone database에 대한 튜토리얼을 사전에 숙지해야 한다.

<a id="08fcba1b93372368"></a>
### Overview

GOLDILOCKS는 앞서 살펴본 바와 같이 단독 (standalone) database로 구성하여 사용할 수 있을 뿐만 아니라 다수의 database를 하나의 클러스터 (cluster)로 묶은 다음 서비스에 적합한 data 분배 정책을 사용자가 직접 선택하여 사용할 수도 있다. 즉, GOLDILOCKS cluster system을 사용하면 사용자가 대용량 데이터를 다수의 서버에 원하는 방식으로 분산하여 처리할 수 있으므로 서비스 가용성이 높아지고 병렬처리를 통해 처리량이 개선된다.

GOLDILOCKS cluster system은 하나 이상의 cluster group으로 구성되며 하나의 cluster group은 하나 이상의 cluster member로 구성된다. 별도의 응용 프로그램 server나 meta server를 필요로 하지 않으며 응용 프로그램들은 data server에 해당하는 cluster member에 접속하여 동작한다. 동일한 cluster group에 소속된 cluster member들은 동일한 data 복제본 (replica)을 유지한다.

GOLDILOCKS database를 standalone으로 사용할지 또는 cluster system으로 사용할지 여부는 각 노드의 database를 생성할 때 미리 결정해야 한다. 만약 cluster system으로 사용하려면 사용자가 각 노드에서 database를 생성할 때 cluster 관련 옵션을 추가해야 한다.

<a id="60ae0f8bbeaca9ba"></a>
### 프로퍼티 설정

Cluster system을 구축하기 위한 각종 프로퍼티들은 standalone database로 사용할 때와 마찬가지로 각 서버의 $GOLDILOCKS_DATA/conf/goldilocks.property.conf 파일에 기술되어 있다. Cluster system을 구성하여 사용하더라도 각각의 database를 위한 TBS (tablespace), LOG, CONTROL FILE 등에 관한 주요 프로퍼티는 standalone과 동일한 방식으로 설정하면 된다. 단, 동일한 서버에서 다수의 database를 생성하여 cluster system으로 구성할 때는 각 파일들의 PATH와 port 등이 cluster member 간에 중복되지 않게 유의해야 한다.

다음은 cluster system을 구성할 때 고려해야 하는 주요 프로퍼티 항목과 설명이다.

**주요 프로퍼티**

<a id="21931a2bcc43be15"></a>
| 프로퍼티 | 설명 | 기본값 |
| --- | --- | --- |
| SYSTEM_TABLESPACE_DIR | 시스템 TBS들이 저장되는 디렉토리 경로이다. 해당 경로에는 다음과 같은 TBS들이 설치된다. * DICTIONARY_TBS * MEM_DATA_TBS * MEM_UNDO_TBS * MEM_TEMP_TBS * MEM_TRANS_TBS | ‘&lt;GOLDILOCKS_DATA&gt;/db’ |
| SYSTEM_MEMORY_DICT_TABLESPACE_SIZE | 딕셔너리 테이블스페이스의 크기이다. | 256M |
| SYSTEM_MEMORY_DATA_TABLESPACE_SIZE | 데이터 테이블스페이스의 크기이다. | 200M |
| SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE | Undo 테이블스페이스의 크기이다. | 32M |
| LOG_DIR | 기본 로그 디렉토리 경로이다. | ‘&lt;GOLDILOCKS_DATA&gt;/wal’ |
| SYSTEM_LOGGER_DIR | 시스템 로그 디렉토리 경로이다. | ‘&lt;GOLDILOCKS_DATA&gt;/trc’ |
| CONTROL_FILE_COUNT | 컨트롤 파일의 개수이다. | 2 |
| CONTROL_FILE_0 | 첫 번째 컨트롤 파일의 경로이다. | '&lt;GOLDILOCKS_DATA&gt;/wal/control_0.ctl' |
| CONTROL_FILE_1 | 두 번째 컨트롤 파일의 경로이다. | '&lt;GOLDILOCKS_DATA&gt;/wal/control_1.ctl' |
| LOCAL_CLUSTER_MEMBER | Local 서버가 cluster system 내에서 사용할 cluster member의 이름이다. | ‘G1N1’ |
| LOCAL_CLUSTER_MEMBER_HOST | Local 서버의 host name이다. | '127.0.0.1' |
| LOCAL_CLUSTER_MEMBER_PORT | Local 서버가 cluster system 내에서 통신하기 위해 사용할 TCP listen port이다. | 10101 |

Cluster member 이름과 host-port 조합은 cluster system 내에서 유일해야 한다. 위의 프로퍼티 설정을 생략하려면 각 노드에서 gcreatedb를 이용하여 database를 생성할 때 --member, --host, --port 옵션을 이용하여 해당 정보를 부여한다. 프로퍼티 또는 gcreatedb 옵션을 통해 부여된 member 정보는 내부적으로 $GOLDILOCKS_DATA/wal/location.ctl 파일에 저장되어 관리된다.

프로퍼티를 변경하려면 text 프로퍼티 파일 ($GOLDILOCKS_DATA/conf/goldilocks.properties.conf)을 변경하거나 환경 변수에 GOLDILOCKS_&lt;property_name&gt; 형태의 변수를 새로 정의하면 된다. 프로퍼티 파일에 설정된 값이 환경 변수에 설정된 값보다 우선한다.

<a id="61d91996f55bc6aa"></a>
### Background 프로세스

GOLDILOCKS cluster system은 각 member 노드에 instance를 관리하기 위한 background 프로세스(gmaster)를 가지고 있다. 각 노드의 gmaster는 내부적으로 여러 개의 system thread로 구성되어 있고 대부분의 thread는 standalone과 동일하지만 다음과 같은 system thread들이 cluster system 관리를 위해 추가되었다.

다음의 thread들은 cluster 모드로 생성된 database를 시작할 경우에만 기동된다.

- Cluster recover thread: Cluster system에서 global transaction을 복구한다.
- Failover thread: Cluster system에서 특정 노드나 네트워크에 장애가 발생했을 때 장애 member에 대한 offline 및 coordinator 재선정과 같은 failover를 처리한다.

다음은 GOLDILOCKS를 cluster system으로 구성하여 사용할 경우에 추가적으로 기동되는 프로세스들이다.

- cdispatcher: Cluster 패킷의 송수신 및 세션 관리 등을 담당한다.
- cserver: 자신이 속한 member 노드의 database 변경 및 조회 연산을 수행한다.

GOLDILOCKS cluster system에서는 각 member 노드 간에 복잡한 cluster protocol 통신이 필요한데 cluster dispatcher (cdispatcher)는 이를 위해 네트워크 통신 컨텍스트 관리 및 패킷 분배 메커니즘을 효율적으로 수행하는 프로세스이다. 또한, heartbeat 등을 통해 cluster 세션의 유효성을 지속적으로 모니터링하는 역할을 수행하기도 한다.

Cluster system에서는 특정 노드 (driver 노드)에서 수행하는 SQL이 대상 테이블의 sharding 정책을 참고하여 원격 member 노드에 data를 저장하거나 해당 노드에 저장된 data를 조회해야 할 때가 있다. 이 때 각 member 노드에서는 원격으로부터의 이런 요청을 수행하여 결과를 반환하는 프로세스가 필요한데 이러한 역할을 수행하는 프로세스가 cserver이다.

<a id="0448145e58e51c69"></a>
### Client 프로세스

Standalone과 마찬가지로 사용자는 cluster system에서도 Client/ Server (C/S) 모델과 Direct Access (D/A) 모델을 모두 사용할 수 있다. 다만 cluster system의 각 member 노드는 자신만의 listener를 가지고 있으므로 client 프로그램은 (C/S 모드로 사용 시) 접속하고자 하는 cluster member의 listen port를 사전에 인지하고 있어야 한다. Cluster system의 어떤 노드에 접속하든 사용자는 standalone database와 동일하게 다양한 형태의 transaction을 처리할 수 있다.

그 밖에 signal handling이나 connection에 대한 cleanup, 각종 공유 자원 해제 등은 standalone과 cluster system에서 동일한 방식으로 처리된다.

<a id="4bc59343bfb61f1f"></a>
### Instance의 메모리 구조

GOLDILOCKS cluster system은 다수의 shared-nothing database를 cluster system이라는 하나의 관리 단위로 묶어서 사용하기 위한 것이다. 따라서 각 cluster member 노드의 메모리 사용 방식은 standalone과 매우 유사하다. 각 member 노드가 사용하는 메모리 크기는 자신의 프로퍼티 파일에 지정된 관련 프로퍼티들에 의해 결정된다. Static 영역은 standalone과 동일하게 database를 운용하기 위한 instance 기본 정보들과 각 session, statement 및 transaction 정보들, redo log buffer, dictionary cache 정보, 그리고 그 외 여러가지 운용 정보들을 담고 있다. 이런 기본 운용 정보 외에 location 정보와 cluster session 정보 등과 같은 cluster system 관리를 위한 추가 정보들이 저장된다.

테이블스페이스 영역은 각 테이블스페이스의 내용을 담은 page frame들과 이를 제어하기 위한 Page Control Header (PCH)들로 구성되어 있다.

응용 프로그램 프로세스의 메모리는 connect 할 때 attach한 instance 메모리 이외에 프로세스 단위로 공유하는 ODBC environment와 여러 ODBC handle들, 그리고 bind 정보 등과 같은 기타 정보들을 포함하고 있는 heap 메모리 영역을 추가적으로 포함하고 있다.

<a id="4428264b91dad4bb"></a>
### Cluster System 시작과 종료

GOLDILOCKS system을 시작하려면 사전에 각 member 노드에 instance를 생성 (gcreatedb)한 후에 cluster group과 cluster member를 등록해야 한다. 이후 gsql과 gsqlnet을 통해 sysdba role을 이용하여 system을 시작하고 종료할 수 있다.

C/S 모델의 dedicated 모드에서 GOLDILOCKS cluster system을 시작하거나 종료하려고 할 경우, 즉 gsqlnet 을 이용하고자 할 경우에는 [listener](../part-06-utility-manual/36-glsnr.md#c15dd351977c833f)가 실행되어 있어야 한다.

C/S 모델의 shared 모드에서는 GOLDILOCKS cluster system을 시작하거나 종료할 수 없다.

```
% gsql --as sysdba

Enter user-name: sys
Enter password: 

Connected to an idle instance.

gSQL>
```

GOLDILOCKS cluster system은 다음과 같은 startup phase를 갖는다. Standalone과 비교할 때 OPEN 상태가 LOCAL OPEN과 GLOBAL OPEN 상태로 세분화되었다.

- NOMOUNT
    - GOLDILOCKS instance를 관리하는 데몬인 gmaster 프로세스를 띄운다
- MOUNT
    - $GOLDILOCKS_DATA 환경 변수를 이용하여 프로퍼티들과 복구를 위한 control file을 읽어들인다.
- LOCAL OPEN
    - Data file들로부터 테이블스페이스의 내용을 로딩한 후에 redo log file들을 이용하여 복구하고 in-doubt global transaction을 복구하며 no-logging index들을 새로 build하고 dictionary cache를 생성한다.
- OPEN (GLOBAL OPEN)
    - 각 cluster member 간의 cluster session을 연결하고 shard map 등을 정리하며 글로벌 관리자 (global coordinator) 및 그룹 관리자 (group coordinator)를 선정한 후, 최종적으로 사용자의 서비스 접속을 기다린다.

GOLDILOCKS cluster system을 시작하거나 종료하기 위해서는 기본적으로 다음과 같은 사전 작업을 통해 cluster system 환경을 구성해 두어야 한다. gcreatedb를 이용하여 각 member database를 생성할 때 member 이름, host 주소, port 번호를 고유하게 부여할 경우, 각 노드의 property 설정 과정을 생략할 수 있다.

- Property 설정: 각 member 노드에서 사용할 property file을 수정한다.
- Database 생성: gcreatedb를 통해 각 member 노드에 database를 생성한다.
- Cluster group 생성 및 member 추가: Cluster system을 구성할 group과 member를 추가한다.
- Listener 기동: gsqlnet을 이용하기 위해서는 각 노드에서 listener를 미리 기동해 두어야 한다.

다음 구문을 사용하여 cluster group과 member를 생성한다.

- [ALTER CLUSTER GROUP name ADD MEMBER](../part-03-sql-manual/18-sql-references.md#72ed23526a0c9e3b)
- [CREATE CLUSTER GROUP](../part-03-sql-manual/18-sql-references.md#dd23e8e2eae3991d)

- Database 생성: 각 노드에서 수행

```
% gcreatedb --cluster --db_name='goldilocks' --member='g1n1' \
    --host='192.168.0.11' --port 10110
% gcreatedb --cluster --db_name='goldilocks' --member='g1n2' \
    --host='192.168.0.12' --port 10120
```

- Cluster group과 member 생성: 한 노드에서 수행한다. 생성 및 추가될 cluster member의 startup 단계는 GLOBAL OPEN이어야 한다.

```
gSQL> create cluster group g1 cluster member g1n1 
        host '192.168.0.11' port 10110;
gSQL> alter cluster group g1 add cluster member g1n2 
        host '192.168.0.12' port 10120;
```

위와 같이 GOLDILOCKS cluster system 구성을 완료하면 다음 두 가지 방법을 이용하여 cluster system 전체를 시작하거나 종료할 수 있다.

- 각 member 노드에 접속하여 하나씩 시작하고 종료하는 방법
    - `\`startup 및 `\`shutdown 명령을 이용한다.
- 하나의 member 노드에서 전체 member 노드를 동시에 시작하고 종료하는 방법
    - gsqlnet을 통해 접속한 후에 `\`cstartup 및 `\`cshutdown 명령을 이용한다.

다음은 위의 첫 번째 방법대로 각 member 노드에 접속하여 cluster system을 기동하는 예이다. `\`startup 명령은 중간 과정없이 곧바로 LOCAL OPEN 단계까지 진입할 때 사용하며, 이는 `\`startup nomount, alter system mount database, alter system open local database의 세 단계로 분리하여 수행할 수도 있다.

`\`startup을 통해 각 노드에서 LOCAL OPEN 단계까지 기동한 후, 최종적으로 하나의 노드에 접속하여 GLOBAL OPEN 단계까지 기동하면 된다.

- LOCAL OPEN까지 startup: 각 member 노드에서 수행한다.

```
% gsql sys gliese --as sysdba
  gSQL> \startup
  Startup success.
```

- OPEN까지 startup: 한 노드에서 수행한다.

```
% gsql sys gliese --as sysdba
  gSQL> alter system open global database;
  System altered.
```

Cluster system에 포함된 노드의 개수가 많을 경우에 위의 첫 번째 방법으로 startup을 진행하면 운영자 작업에 부담이 될 수 있다. Cluster system이 종료된 후 재기동할 경우, 모든 member 노드에서 startup 할 때마다 LOCAL OPEN까지의 작업 과정을 수행해야 하기 때문이다. 운영상의 편의를 위해 다음과 같이 간단한 방법으로 모든 member를 한 번에 startup 할 수 있다.

- GLOBAL OPEN까지 startup: 한 노드에서 수행한다.

```
% gsqlnet sys gliese --as sysdba
  gSQL> \cstartup
  Startup success.
```


> 
> - `\`cstartup 및 `\`cshutdown 명령어는 gsqlnet에서만 수행 가능하며 gsql에서는 지원하지 않는다. 그리고 기동하려는 모든 member 노드에 listener가 사전에 기동되어 있어야 한다.
> 
> 
> 
> - 하나의 물리적 노드에서 다수의 member가 포함된 GOLDILOCKS cluster system을 구축하고자 할 경우에는 각 database를 생성할 때 home directory 및 member 이름, cluster port 정보가 중복되지 않도록 주의해야 한다.
> 

GOLDILOCKS system이 종료되면 각 member 노드에서 관리 데몬 프로세스인 gmaster가 종료되어 더 이상의 접속이나 기타 database 작업을 수행할 수 없다.

GOLDILOCKS cluster system의 종료 모드에는 다음과 같은 두 가지 종류가 있다.

- NORMAL: 새로운 session의 접속을 차단하고 현재 접속된 모든 session이 종료될 때까지 기다린 후에 checkpoint를 수행하고 instance를 내린다.
- ABORT: 접속 중인 session들의 상태와 관계없이 gmaster를 즉시 종료시켜 instance를 내린다.

다음과 같이 gsql을 이용하여 `\shutdown` 명령을 수행하면 접속한 member의 노드만 종료된다.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \shutdown normal

Shutdown success

gSQL>
```

Cluster system에 속한 모든 member를 한 번에 종료시키고자 할 경우에는 다음과 같이 gsqlnet의 `\`cshutdown 명령을 이용한다. normal 옵션은 생략할 수 있다.

```
% gsqlnet sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \cshutdown normal

Shutdown success

gSQL>
```

> `\`cshutdown을 수행할 때 abort 옵션을 사용할 경우, 모든 member 노드들에 대해 gmaster를 강제로 종료시키므로 `\`cstartup을 이용하여 다시 기동할 때는 종료 시점의 노드 상태에 따라 일부 member 노드가 cluster system 참여 (join)에 실패할 수도 있다. 물론 다음에 살펴볼 join 명령어와 rebalance 과정을 통해 다시 참여시킬 수는 있지만 특별한 경우를 제외하고는 되도록 `\`cshutdown normal을 이용하여 종료하는 것이 안전하다.

Cluster system에 속한 하나의 member 노드 또는 일부의 member 노드를 종료하거나 시작하고자 할 경우에는 다음 과정을 따른다. 다음은 cluster member 노드 중에 G1N2라는 이름을 가진 member 노드만 재시작한 후에 cluster system에 다시 참여시키는 과정이다.

```
% gsql sys gliese --as sysdba --dsn=g1n2

Connected to GOLDILOCKS Database.

gSQL> \shutdown normal

Shutdown success

gSQL> \startup

Startup success

gSQL> alter system join database;

System altered.
```

Transaction이 발생하는 상황에서 member 노드를 종료할 경우, 해당 노드를 재시작한 후에 cluster system 에 다시 참여 (join) 시키려면 변경이 발생한 테이블들에 대한 리밸런싱 (rebalancing) 작업이 필요할 수 있다. 만약 리밸런싱 작업을 수행하지 않으면 driver 노드에서 수행하는 transaction이 리밸런싱되지 않은 테이블에 대한 변경을 수행할 때 실패할 수 있다.

리밸런싱 작업이란 테이블의 데이터 분배 정책 및 속성 정보를 member 노드간에 동기화하고, 테이블 데이터를 데이터 분배 정책에 따라 각 member 노드에 다시 분할 저장하는 일련의 과정이다.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \shutdown normal

Shutdown success

gSQL> \startup

Startup success

gSQL> alter system join database;

ERR-42000(16405): some tables in the database need to be rebalanced
System altered.

gSQL> alter database rebalance;

Database altered.
```

<a id="24017062f641fdf7"></a>
## GOLDILOCKS 설치와 Database 생성

GOLDILOCKS cluster system에 포함될 member database 설치 및 생성 방법은 standalone과 대부분 동일하다. 다음 database 설치 및 생성 과정에서는 standalone과 비교하여 cluster system만 가지는 특징과 방법상의 차이를 설명한다.

<a id="48ca60754045358d"></a>
### GOLDILOCKS Package 구성

GOLDILOCKS cluster system을 구성하기 위해 사용하는 package는 standalone database를 구성하기 위한 것과 동일하다. 다만 dictionary와 performance view 등을 생성하기 위한 스크립트는 standalone과 cluster 용이 다음과 같이 분리되어 있으므로 database를 생성한 후에는 반드시 각각의 용도에 맞는 스크립트를 이용하여 생성해야 한다.

Standalone database를 위한 스크립트는 $GOLDILOCKS_HOME/admin/standalone 디렉토리 아래에 위치하고 cluster system을 위한 스크립트는 $GOLDILOCKS_HOME/admin/cluster 디렉토리 아래에 위치한다.

**admin/ standalone 디렉토리**

<a id="2468f140182c3223"></a>
| 파일 이름 | 설명 |
| --- | --- |
| README | read me |
| DictionarySchema.sql | Dictionary schema 생성 스크립트 |
| InformationSchema.sql | Information schema 생성 스크립트 |
| PerformanceViewSchema.sql | PerformanceView schema 생성 스크립트 |

**admin/ cluster 디렉토리**

<a id="2f214a7a481607b0"></a>
| 파일 이름 | 설명 |
| --- | --- |
| README | read me |
| DictionarySchema.sql | Dictionary schema 생성 스크립트 |
| InformationSchema.sql | Information schema 생성 스크립트 |
| PerformanceViewSchema.sql | PerformanceView schema 생성 스크립트 |

<a id="0d922e80e53c09dc"></a>
### GOLDILOCKS Software 설치

Cluster system에 포함되는 모든 member 노드에 GOLDILOCKS software를 설치해야 하며 설치 방법은 standalone과 동일하다. 커널 파라미터의 설정 및 확인 방법, 환경 변수 설정 방법은 standalone과 동일하므로 해당 튜토리얼을 참고한다.

이 때, cluster member 노드 각각에 대한 property 설정이나 database 이름, database 버전, character set, time zone 등의 설정이 동일해야만 cluster system을 정상적으로 구성할 수 있다.

<a id="0712261b9a4f9eea"></a>
### Database 생성

Cluster system을 구성하는 각 member 노드에서 database를 생성하려면 standalone과 마찬가지로 gcreatedb utility를 사용한다.

다음은 cluster database를 생성할 때만 사용되는 gcreatedb 옵션이다. 이외의 옵션은 standalone과 동일하다.

**gcreatedb 인자**

<a id="99ab7fbd8dc865ed"></a>
| 실행 인자 | 설명 |
| --- | --- |
| --cluster | Cluster database라는 것을 나타낸다. 생략할 경우, standalone database를 생성한다. |
| --member | Cluster system 내에서 사용할 local database의 member 이름이다. 생략할 경우, LOCAL_CLUSTER_MEMBER 프로퍼티에 설정된 값을 사용한다. |
| --host | Cluster system member 간에 통신하기 위해 사용할 local member의 IP address이다. 생략할 경우, LOCAL_CLUSTER_MEMBER_HOST 프로퍼티에 설정된 값을 사용한다. |
| --port | Cluster system member 간에 통신하기 위해 사용할 local member의 TCP listen port이다. 생략할 경우, LOCAL_CLUSTER_MEMBER_PORT 프로퍼티에 설정된 값을 사용한다. |

다음은 cluster system에서 사용될 데이터베이스를 생성하는 예이다.

```
[SHELL]> gcreatedb --cluster
Database created

[SHELL]> gcreatedb --cluster --member=G1N1
Database created

[SHELL]> gcreatedb --cluster --member=G1N1 --host=127.0.0.1 --port 10101
Database created

[SHELL]> gcreatedb --cluster                         \
                   --db_name="TEST_DB"               \
                   --home=$GOLDILOCKS_DATA           \
                   --host=127.0.0.1                  \
                   --port=10101                      \
                   --db_comment="g1n1 db comment"    \
                   --timezone="+09:00"               \
                   --character_set="UHC"             \
                   --char_length_units="OCTETS"
Database created

[SHELL]> ls $GOLDILOCKS_DATA/db
system_data.dbf  system_dict.dbf  system_trans.dbf system_undo.dbf
```

<a id="fb4f7da0e9ef7b86"></a>
### Dictionary Schema 정보 구축

Standalone과 마찬가지로 cluster system을 정상적으로 사용하기 위해서는 dictionary 스키마 정보를 구축해야 한다. 아래 스키마들을 구축하지 않을 경우 객체의 구조 정보를 획득하는 ODBC, JDBC의 catalog API (예: SQLTables() 함수 등)들이 오작동하여 third party tool들과 연동하지 않을 수 있으므로 database를 생성한 후에 반드시 구축해 주어야 한다.

Cluster system에서 스키마를 구축할 때는 되도록 cluster group과 member를 모두 생성한 후에 작업하는 것이 좋다. 이처럼 cluster system 구성을 완료한 후에는 하나의 member 노드에 접속하여 생성 스크립트를 수행할 때, GOLDILOCKS에서 자동으로 모든 member 노드에 스키마를 생성하기 때문이다.

- DICTIONARY_SCHEMA: DBA_*, ALL_*, USER_* 등의 객체 정보를 조회하는 view와 table로 구성된다.
- INFORMATION_SCHEMA: SQL 표준의 INFORMATION_SCHEMA에 포함되는 view와 table로 구성된다.
- PERFORMANCE_VIEW_SCHEMA: Fixed table들의 정보를 조합하여 시스템 정보를 조회하는 view로 구성된다.

다음은 cluster system 용 스크립트를 이용하여 스키마들을 구축하는 방법을 보여준다. 위에서 언급한대로 GLOBAL OPEN 상태에서 하나의 member 노드에 접속하여 수행하면 된다.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/DictionarySchema.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/InformationSchema.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/PerformanceViewSchema.sql
```

위에서 구축한 스키마 정보를 이용하여 cluster system의 다양한 구조 정보들을 조회할 수 있는데, 조회 할 때 객체 뒤에 group 및 member 이름을 부여하여 사용자가 조회하고 싶은 노드의 정보만 쉽게 추출할 수 있는 것이 standalone과의 차이이다.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL> select origin_member_name, stat_name, stat_value
    2   from gv$system_mem_stat
    3  where stat_name = 'PLAN_CACHE_TOTAL_SIZE';

ORIGIN_MEMBER_NAME STAT_NAME             STAT_VALUE
------------------ --------------------- ----------
G1N1               PLAN_CACHE_TOTAL_SIZE   17844952
G2N2               PLAN_CACHE_TOTAL_SIZE   16796288
G2N1               PLAN_CACHE_TOTAL_SIZE   16796288
G1N2               PLAN_CACHE_TOTAL_SIZE   16796288
G3N1               PLAN_CACHE_TOTAL_SIZE   16796288
G3N2               PLAN_CACHE_TOTAL_SIZE   16796288

6 rows selected.

gSQL> select origin_member_name, stat_name, stat_value
    2   from gv$system_mem_stat@g1n2
    3  where stat_name = 'PLAN_CACHE_TOTAL_SIZE';

ORIGIN_MEMBER_NAME STAT_NAME             STAT_VALUE
------------------ --------------------- ----------
G1N2               PLAN_CACHE_TOTAL_SIZE   16796288

1 row selected.

gSQL> select origin_member_name, stat_name, stat_value
    2   from gv$system_mem_stat@g1
    3  where stat_name = 'PLAN_CACHE_TOTAL_SIZE';

ORIGIN_MEMBER_NAME STAT_NAME             STAT_VALUE
------------------ --------------------- ----------
G1N1               PLAN_CACHE_TOTAL_SIZE   17844952
G1N2               PLAN_CACHE_TOTAL_SIZE   16796288

2 row selected.
```

<a id="e040681fcf69fbe8"></a>
## Schema Object 관리

Schema object는 사용자가 생성한 논리적 구조물들이다. GOLDILOCKS cluster system은 table, index, global sequence와 같은 객체를 지원한다. 본 장에서는 standalone과 비교하여 cluster system이 가지는 각 schema object들의 특징을 살펴 보고, 이를 효율적으로 관리하기 위한 방법을 설명한다.

<a id="14e9291573e8bd74"></a>
### 테이블 관리

GOLDILOCKS cluster system에서 테이블을 생성할 경우, 사용자는 다음 네 가지 sharding 정책 중 하나를 옵션으로 지정할 수 있다. Sharding 정책은 cluster system에서 테이블의 data를 각 cluster group에 어떤 방식으로 분배하여 저장할지를 결정한다. 이는 cluster system에서만 지정할 수 있는 옵션이며 database 를 standalone으로 생성할 경우에는 사용할 수 없다.

- Cloned strategy
    - 테이블의 모든 data를 동일하게 복제한다.
- Hash sharding strategy
    - Sharding key의 hash 값을 기준으로 테이블 data를 분배한다.
- Range sharding strategy
    - Sharding key의 범위 (range)값을 기준으로 테이블 data를 분배한다.
- List sharding strategy
    - Sharding key의 나열 (list)값을 기준으로 테이블 data를 분배한다.

테이블 생성에 대한 자세한 내용은 [CREATE TABLE](../part-03-sql-manual/18-sql-references.md#9b82da6d66aabe8c) 구문과 [Cluster Table과 Shard](../part-03-sql-manual/14-cluster-objects.md#87224b8141b8a713) 개념을 참조한다.

Sharding 정책 옵션을 생략할 경우 [DEFAULT_SHARDING](../part-02-administration-manual/10-server-property.md#e144387380cfccfa) 프로퍼티에 의해 결정된다. DEFAULT_SHARDING 의 기본값은 0으로써 cloned table을 생성한다.

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
);
```

위와 같이 사용자가 sharding 정책을 부여하지 않은 채 테이블을 생성할 경우, GOLDILOCKS cluster system은 내부적으로 다음과 같은 구문으로 테이블을 생성한다.

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
)
    CLONED
    AT CLUSTER WIDE
;
```

> Hash/ range/ list sharded table의 경우 제약 조건을 생성할 때 PRIMARY KEY, UNIQUE 제약 조건이 sharding key를 포함하도록 해야 한다.

<a id="0f3be88c3746bed6"></a>
#### Cloned Strategy

테이블 data를 특정한 조건에 의해 분할하는 것이 아니라 모든 data를 복제하는 방식이다. Data 복제 대상은 cluster system 내의 모든 노드일 수도 있고 특정 cluster group만 지정할 수도 있다. 즉, 지정한 cluster group의 cluster member 들에 복제본 (clone)을 배치하는 정책이다.

- AT CLUSTER WIDE 
    - Cluster system의 모든 cluster group의 모든 cluster member에 clone을 배치한다. 
    - Cluster group과 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](../part-03-sql-manual/18-sql-references.md#1c3e42a41b2d2965) 구문을 통해 clone을 재배치할 수 있다. 
- AT CLUSTER GROUP group_list 
    - 지정한 cluster group들의 모든 cluster member에 clone을 배치한다. 
    - 지정된 cluster group에 cluster member를 추가할 때 [ALTER TABLE name REBALANCE](../part-03-sql-manual/18-sql-references.md#1c3e42a41b2d2965) 구문을 통해 clone을 재배치할 수 있다. 
    - Cluster group 추가는 clone 재배치에 영향을 주지 않는다.

옵션을 생략할 경우, 기본값은 AT CLUSTER WIDE로 자동 지정된다.

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
) 
CLONED 
AT CLUSTER WIDE;
```

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
) 
CLONED 
AT CLUSTER GROUP G1, G2;
```

<a id="bc3fc4d76ec144c0"></a>
#### Hash Sharding Strategy

Sharding key로 지정된 column의 hash 값에 따라 테이블 data를 분배하는 정책이다.

Hash sharding 정책을 사용하려면 다음과 같은 조건에 맞게 sharding key를 지정해야 한다.

- Column을 32 개까지 나열할 수 있다. 
- 동일한 column은 사용할 수 없다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column은 사용할 수 없다.

```
CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) )
    SHARDING BY HASH(id);
```

위와 같이 hash sharding과 관련된 옵션들을 생략할 경우, GOLDILOCKS system은 다음과 같은 구문으로 해석한다.

```
CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) )
    SHARDING BY HASH(id)
    SHARD COUNT 24
    AT CLUSTER WIDE;
```

테이블 row들은 id column의 해시값을 기준으로 24 개의 shard 중 하나에 분배되며, 24 개의 shard는 cluster system 전체에 골고루 배치된다. 자세한 내용은 [Cluster Table과 Shard](../part-03-sql-manual/14-cluster-objects.md#87224b8141b8a713)를 참조한다.

<a id="63bf6a1bee702946"></a>
#### Range Sharding Strategy

테이블 data를 sharding key로 지정된 column의 범위 값에 따라 분배하는 정책이다. 각 범위 값에 따라 구분된 shard들을 특정 group에 지정하여 배치할 수도 있고 CLUSTER WIDE하게 배치할 수도 있다.

다음은 sharding key column 값의 범위에 따라 여섯 개의 range shard를 정의한 후, 이를 CLUSTER WIDE 하게 분배하기 위한 테이블 생성 구문이다. 만일 테이블을 생성한 후에 cluster group이 추가될 경우, REBALANCE 기능을 이용하여 추가된 group을 포함한 shard의 재배치 작업을 수행할 수 있다.

- Range sharded table을 생성한다.
- 기존 cluster group인 (g1, g2, g3)에 여섯 개의 shard들을 배치한다.

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
- 생성된 g4를 포함하여 (g1, g2, g3, g4) cluster group에 여섯 개의 shard들을 재배치한다.

```
ALTER TABLE t1 REBALANCE;
```

다음은 sharding key column 값의 범위에 따라 정의되는 range shard들을 특정 cluster group에만 배치하도록 지정하는 구문의 예이다. 즉, 200,000 보다 작은 범위 값을 가지는 shard s1은 cluster group g1에 배치되고, s2는 cluster group g2에 배치되며, shard s3는 g3에 배치된다. 이처럼 range shard 별로 cluster group을 지정하여 생성한 테이블의 경우에는 이후 cluster group이 추가되더라도 REBALANCE 기능을 통해 shard를 재배치할 수 없다.

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
- 새로 생성한 cluster group g4에는 shard가 배치되지 않는다.

```
ALTER TABLE t1 REBALANCE;
```

Range sharding key를 지정하기 위해 고려해야 하는 조건은 다음과 같다.

- Column은 32 개까지 나열할 수 있다. 
- 동일한 column은 사용할 수 없다. 
- LONG VARCHAR, LONG VARBINARY 타입의 column은 사용할 수 없다.

<a id="909cc6bfedad02fa"></a>
#### List Sharding Strategy

테이블 data를 sharding key로 지정된 column의 나열 (list) 값에 따라 분배하는 정책이다. Range sharding 정책과 마찬가지로 각 shard들을 특정 group에 지정하여 분배할 수도 있고 CLUSTER WIDE하게 분배되도록 할 수도 있다.

List sharding 정책에서 sharding key를 지정하기 위한 조건은 다음과 같다.

- 하나의 column만 사용할 수 있다.
- LONG VARCHAR, LONG VARBINARY 타입의 column은 사용할 수 없다.

다음은 생성되는 list shard들을 CLUSTER WIDE하게 배치되도록 테이블을 생성하는 구문의 예이다. 테이블을 생성한 후에 추가되는 cluster group을 포함하여 shard를 재배치하기 위해 REBALANCE 기능을 사용할 수 있다.

- List sharded table을 생성한다.
- 기존 cluster group인 (g1, g2, g3)에 다섯 개의 shard들을 배치한다.

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
- 추가된 g4를 포함하여 (g1, g2, g3, g4) cluster group에 다섯 개의 shard들을 재배치한다.

```
ALTER TABLE city REBALANCE;
```

다음은 sharding key column 값의 나열 값에 따라 정의되는 list shard들을 특정 cluster group에만 배치되도록 지정하는 구문의 예이다. 이후 cluster group이 추가되더라도 REBALANCE 기능을 통해 shard를 재배치할 수 없다.

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
- 생성된 cluster group g4에 shard가 배치되지 않는다.

```
ALTER TABLE city REBALANCE;
```

<a id="b64fbef6b6505d2c"></a>
### 인덱스 관리

<a id="4822f3e02dc20fb3"></a>
#### Global Secondary Index

Cluster system에는 다수의 member 노드가 존재하고 테이블의 레코드들은 sharding 정책에 따라 각 member 노드에 분할 또는 복제 저장된다. Standalone 시스템의 경우 레코드가 저장될 때 해당 database 에 고유한 값 (Row Identifier: RID)을 함께 저장하여 레코드에 대한 유일성을 보장하는데, 이 경우 cluster system 환경에서 각 노드들의 값이 중복될 가능성이 있기 때문에 유일성을 보장할 수 없다.

따라서 cluster system 전체에서 레코드의 유일성을 보장하기 위해 global RID (GRID)가 추가되었다. 레코드에 대한 GRID 값은 레코드가 갱신되더라도 변경되지 않고 cluster system 환경에서 특정 레코드의 유일성을 항상 보장한다.

Global secondary index는 cluster system 환경에서 레코드들의 GRID 값을 빠르게 검색할 수 있도록 key로 구성한 B-tree 인덱스이다.

사용자는 테이블을 생성할 때 global secondary index의 생성 여부를 [DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION](../part-02-administration-manual/10-server-property.md#7f1c0835161cb0bd)을 통해 선택할 수 있고 테이블을 생성한 후에 생성된 global secondary index를 삭제하거나 다시 생성할 수도 있다. global secondary index는 테이블당 한 개만 생성할 수 있다.

테이블에 대한 non-deterministic 질의를 수행하기 위해서는 global secondary index가 반드시 필요하고, 만약 테이블에 global secondary index가 없을 경우 non-deterministic 질의는 다음과 같이 실패한다.

```
gSQL> DELETE FROM T1 LIMIT 1;

ERR-42000(16423): does not support non-deterministic DML in the cluster system : global secondary index expected
```

테이블의 global secondary index 생성 여부를 확인하고 싶을 경우에는 다음과 같이 USER_GSI_PLACE 딕셔너리를 조회하거나, ALL_GSI_PLACE 및 DBA_GSI_PLACE 딕셔너리를 조회한다.

```
gSQL> CREATE TABLE T1( I1 INTEGER );

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT * 
    2   FROM USER_GSI_PLACE@LOCAL
    3  WHERE TABLE_NAME = 'T1';

TABLE_SCHEMA TABLE_NAME GROUP_ID GROUP_NAME MEMBER_ID MEMBER_NAME MEMBER_OFFLINE
------------ ---------- -------- ---------- --------- ----------- --------------
BLOCKS
------
PUBLIC       T1                1 G1                 1 G1N1        FALSE         
    64
PUBLIC       T1                1 G1                 2 G1N2        FALSE         
  null

2 rows selected.

gSQL> DROP TABLE T1;

Table dropped.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT * 
    2   FROM USER_GSI_PLACE@LOCAL
    3  WHERE TABLE_NAME = 'T1';

no rows selected.
```

<a id="d54acab476d5bff7"></a>
### Global 시퀀스

GOLDILOCKS cluster system은 사용자가 지정한 조건에 부합하는 시퀀스 값들의 집합을 다수의 member 노드가 공유하여 사용할 수 있도록 기존의 시퀀스 객체를 확장한 global 시퀀스 객체를 제공한다. 즉, cluster system에서 사용자가 시퀀스를 생성하면 내부적으로 global 시퀀스 객체가 자동으로 생성되며 이후 각 member 노드에서 NEXTVAL을 호출할 때 해당 global 객체로부터 특정한 범위의 시퀀스 값들을 할당받아 사용한다. 다음과 같이 기본적인 생성 및 사용 방법은 standalone의 시퀀스와 같다.

```
gSQL> CREATE SEQUENCE global_user_seq START WITH 1000 INCREMENT BY 1 NOCACHE NOCYCLE; 

Sequence created.

gSQL> SELECT global_user_seq.NEXTVAL FROM dual;

NEXTVAL
-------
      1

1 row selected.

gSQL> DROP SEQUENCE global_user_seq;

Sequence dropped.
```

Standalone에서 사용되는 시퀀스와 마찬가지로 global 시퀀스 객체에서도 cache size를 생성 옵션으로 지정할 수 있는데, 이는 global 시퀀스 객체로부터 몇 개의 시퀀스 값들을 획득하여 local cache에 적재해둘 것인지를 의미한다. 다음은 cache size를 5로 지정하여 global 시퀀스 객체를 생성하였을 때 각 member 노드의 local cache 상황과 NEXTVAL 호출 시의 반환값을 정리한 것이다.

```
gSQL> CREATE SEQUENCE seq START WITH 1 CACHE 5; 

Sequence created.
```

<a id="abaa151c0ae23634"></a>
<table class="table column_count_5"><caption> </caption><thead><tr><th class="to_center to_middle" rowspan="2"><div>Member 이름</div></th><th class="to_center to_middle" rowspan="2"><div>NEXTVAL 결과</div></th><th class="to_center" colspan="2"><div>Local Cache 잔여 시퀀스 개수</div></th><th class="to_center to_middle" rowspan="2"><div>설명</div></th></tr><tr><th class="to_center"><div>G1N1</div></th><th class="to_center"><div>G1N2</div></th></tr></thead><tbody><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>1</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_middle"><div>From Global Object
(Alloc 1 ~ 5)</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>2</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>2</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>6</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_middle"><div>From Global Object
(Alloc 6 ~ 10)</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>7</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>8</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>2</div></td><td class="to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>9</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>1</div></td><td class="to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>10</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>11</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_middle"><div>From Global Object
(Alloc 11 ~ 15)</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>12</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_center to_middle"><div>1</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>5</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>16</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_left to_middle"><div>From Global Object
(Alloc 16 ~ 20)</div></td></tr></tbody></table>

위의 표에서 G1N1과 G1N2가 global 시퀀스 객체로부터 각 2 회씩, 총 4 회에 걸쳐 시퀀스 값들을 할당받았다. 시퀀스를 생성할 때 CACHE 옵션값을 5로 지정하였으므로 global 객체로부터 할당받을 때는 시퀀스 값들을 다섯 개씩 할당받았다. 이렇게 member 노드가 할당받은 다섯 개의 시퀀스 값들을 자신의 local cache에 보관해둔 후 NEXTVAL을 호출할 때마다 하나씩 반환한다.

- G1N1
    - 첫 번째 NEXTVAL을 호출하면 global 시퀀스 객체로부터 다섯 개 (1~5)의 시퀀스 값들을 할당받는다. 
    - 한 개는 NEXTVAL의 결과로 제공하고 나머지 네 개의 값들은 자신의 local cache에 쌓아둔다.
    - 이 후 호출되는 NEXTVAL은 local cache에 적재해둔 시퀀스 값들을 차례로 반환한다.
- G1N2
    - 첫 번째 NEXTVAL을 호출하면 G1N1에서 이미 할당받은 범위 직후의 시퀀스 값들 (6~10)을 할당받는다.
    - 6은 NEXTVAL의 결과로 제공하고 나머지 네 개의 값들 (7~10)은 자신의 local cache에 쌓아둔다.
    - 이후 호출되는 NEXTVAL은 local cache에 적재해 둔 시퀀스 값들을 반환한다.
    - Local cache가 소진되어 다시 global 시퀀스 객체로부터 다섯 개 (11~15)의 시퀀스 값들을 할당받는다.
- G1N1
    - Local cache가 소진되어 G1N2에서 최종으로 할당받은 시퀀스 값 직후의 다섯 개 (16~20) 시퀀스 값들을 할당받는다.

모든 member 노드는 자신의 노드에서 NEXTVAL을 호출한 적이 없거나, 이미 할당받은 시퀀스 값들을 모두 소진할 경우 반드시 global 시퀀스 객체로부터 CACHE 크기 만큼의 시퀀스를 할당받는다. 따라서 시퀀스 값을 빠른 속도로 획득해야 하는 시스템의 경우, 시퀀스를 생성할 때 CACHE 크기를 적절한 크기로 설정하여 지나치게 빈번한 할당작업이 발생하지 않도록 해야 한다. 왜냐하면 global 시퀀스 객체로부터 시퀀스를 할당받을 때는 standalone database에서와 달리 네트워크 통신 비용이 발생하기 때문이다.

Local cache에 쌓아 둔 시퀀스 값들은 시스템 장애 및 운영자 작업 등의 이유로 database가 재기동되면 다시 사용할 수 없다. 재기동 후에는 첫 번째 NEXTVAL을 호출할 때 global 시퀀스 객체로부터 다시 시퀀스 값들을 할당받는다. 따라서 시퀀스를 생성할 때 부여하는 CACHE 크기는 장애가 발생했을 때 유실될 수 있는 시퀀스 값들의 범위를 의미하기도 하므로 응답 성능 뿐만 아니라 유실 범위를 고려하여 적절한 크기로 설정해야 한다.

Cluster system에서는 특정 노드를 기준으로 NEXTVAL 호출의 결과값이 연속적이지 않을 수 있다. 위의 예에서 G1N1 노드가 NEXTVAL을 호출할 때 반환되는 시퀀스 값이 연속적이지 않은 것을 볼 수 있다. 첫 번째로 할당받은 시퀀스 (1~5) 값들을 소진한 후에 두 번째로 할당받은 값의 범위가 16 ~ 20 이므로 사용자는 5의 다음 시퀀스 값으로 16을 반환받는다. 이는 하나의 global 시퀀스 pool을 다수의 노드가 경쟁적으로 할당받아 사용하는 방식이기 때문이다.

기존의 standalone database 용 시퀀스와 비교하여 global 시퀀스 객체의 특징과 제약 사항은 다음과 같다.

- ALTER SEQUENCE 구문에서 INCREMENT BY 옵션을 사용하여 부호를 변경할 수 없다. (크기는 변경할 수 있다.)
- CYCLE 옵션을 사용할 경우에는 전체 시퀀스 pool의 크기에 따라 member 노드 간에 중복된 값이 반환될 수 있다. 따라서 CYCLE 옵션이 필요한 경우에는 INCREMENT BY 및 CACHE SIZE, cluster member 노드 개수를 고려하여 시퀀스 pool을 충분히 크게 생성해두도록 한다.
- 장애 상황이 아닌 경우라도 특정 member 노드를 기준으로 반환되는 시퀀스 값이 연속적이지 않을 수 있다. 물론, 하나의 member 노드만 NEXTVAL을 호출하는 경우에는 연속적인 시퀀스 값을 얻을 수 있다.
- NOCACHE일 경우에는 CACHE SIZE가 1이므로 local cache에 추가적인 시퀀스 값들을 쌓아두지 않는다. 이 경우, NEXTVAL을 호출할 때마다 global 시퀀스 객체로부터 매번 시퀀스를 한 개씩 할당받게 되어 네트워크 비용이 증가하므로 성능이 상당히 하락할 수 있다.
- 시퀀스 생성 및 변경, 삭제는 기본적으로 AUTO COMMIT으로 동작한다.
- ALTER 구문에 의해 CACHE 및 INCREMENT 크기가 변경될 경우, 모든 노드의 local cache에 쌓인 시퀀스 값들이 모두 리셋된다. 즉, 이후 NEXTVAL을 호출할 때 다시 global 시퀀스 객체로부터 새로운 시퀀스 집합을 할당받아야 한다.

<a id="f806a9e0719abc12"></a>
## GOLDILOCKS 프로퍼티

GOLDILOCKS cluster system에서 사용할 수 있는 주요 프로퍼티는 다음과 같다.

<a id="34eaa5bac9241812"></a>
| 이름 | 설명 |
| --- | --- |
| LOCAL_CLUSTER_MEMBER | Member 이름 |
| LOCAL_CLUSTER_MEMBER_HOST | Cluster session 접속용 host address |
| LOCAL_CLUSTER_MEMBER_PORT | Cluster session 접속용 port |
| CDISPATCHER_THREADS | Cluster dispatcher thread 개수 |
| CSERVERS | Cluster server 프로세스 개수 |
| CLUSTER_DATA_SYNC_SERVERS | Replica data 동기화를 위한 cluster server 프로세스 개수 |

GOLDILOCKS cluster system에서 각 프로퍼티는 다음과 같이 두 가지의 변경 가능한 범위 (scope)를 가진다.

- LOCAL: 전체 member의 프로퍼티 값을 변경하거나 특정 member에 한정하여 프로퍼티 값을 변경할 수 있다.
- GLOBAL: 특정 member에 한정하여 프로퍼티 값을 변경할 수 없고 반드시 cluster system 내의 모든 member에 적용해야 한다.

예를 들어 PRIVATE_STATIC_AREA_SIZE 프로퍼티의 경우 다음과 같이 LOCAL 범위까지 변경이 가능하다는 것을 알 수 있으므로 (IS_GLOBAL column = FALSE), alter system set 구문을 통해 전체 member 노드 값을 변경하거나 특정 member를 지정하여 그 값을 변경할 수 있다. alter system set 구문 뒤에 AT 절을 추가하지 않을 경우 cluster system의 모든 member에 적용한다는 의미이다.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL> select origin_member_name, property_name, property_value, is_global
    2   from gv$property
    3  where property_name = 'PRIVATE_STATIC_AREA_SIZE';

ORIGIN_MEMBER_NAME PROPERTY_NAME            PROPERTY_VALUE IS_GLOBAL
------------------ ------------------------ -------------- ---------
G1N1               PRIVATE_STATIC_AREA_SIZE 104857600      FALSE    
G1N2               PRIVATE_STATIC_AREA_SIZE 104857600      FALSE    

2 rows selected.

gSQL> alter system set private_static_area_size = 200000000 at g1n2;

System altered.

gSQL> select origin_member_name, property_name, property_value, is_global
    2   from gv$property
    3  where property_name = 'PRIVATE_STATIC_AREA_SIZE';

ORIGIN_MEMBER_NAME PROPERTY_NAME            PROPERTY_VALUE IS_GLOBAL
------------------ ------------------------ -------------- ---------
G1N1               PRIVATE_STATIC_AREA_SIZE 104857600      FALSE    
G1N2               PRIVATE_STATIC_AREA_SIZE 200000000      FALSE    

2 rows selected.

gSQL> alter system set private_static_area_size = 300000000;

System altered.

gSQL> select origin_member_name, property_name, property_value, is_global
    2   from gv$property
    3  where property_name = 'PRIVATE_STATIC_AREA_SIZE';

ORIGIN_MEMBER_NAME PROPERTY_NAME            PROPERTY_VALUE IS_GLOBAL
------------------ ------------------------ -------------- ---------
G1N1               PRIVATE_STATIC_AREA_SIZE 300000000      FALSE    
G1N2               PRIVATE_STATIC_AREA_SIZE 300000000      FALSE    

2 rows selected.
```

반면에 DDL_AUTOCOMMIT의 경우에는 다음과 같이 변경 가능한 범위가 GLOBAL이므로 alter system set 구문에 AT 절을 이용하여 특정 member를 지정할 경우 에러가 발생한다.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL> select origin_member_name, property_name, property_value, is_global
    2   from gv$property
    3  where property_name = 'DDL_AUTOCOMMIT';

ORIGIN_MEMBER_NAME PROPERTY_NAME  PROPERTY_VALUE IS_GLOBAL
------------------ -------------- -------------- ---------
G1N1               DDL_AUTOCOMMIT NO             TRUE     
G1N2               DDL_AUTOCOMMIT NO             TRUE     

2 rows selected.

gSQL> alter system set ddl_autocommit = false at g1n2;

ERR-42000(16398): the domain of property does not match with domain 'G1N2' : 
alter system set ddl_autocommit = false at g1n2
                                           *
ERROR at line 1:

gSQL> alter system set ddl_autocommit = false;

System altered.

gSQL> select origin_member_name, property_name, property_value, is_global
    2   from gv$property
    3  where property_name = 'DDL_AUTOCOMMIT';

ORIGIN_MEMBER_NAME PROPERTY_NAME  PROPERTY_VALUE IS_GLOBAL
------------------ -------------- -------------- ---------
G1N1               DDL_AUTOCOMMIT NO             TRUE     
G1N2               DDL_AUTOCOMMIT NO             TRUE     

2 rows selected.
```

---

[← 2. 튜토리얼](2-튜토리얼.md) · [전체 목차](../README.md) · [4. What's New →](4-what-s-new.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
