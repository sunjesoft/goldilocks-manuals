<a id="6aa340ae6a2d0c28"></a>

# 46. glocator

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/6aa340ae6a2d0c28)  
> 태그: `21c.1_35_tag`

[← 45. gtrclogger](45-gtrclogger.md) · [전체 목차](../README.md) · [47. gagent →](47-gagent.md)

<a id="a7382e0cb178245c"></a>
## glocator 소개

<a id="953de5175be4a89d"></a>
### 정의

glocator는 GOLDILOCKS cluster system에서 client에게 location을 제공하고 관리하는 유틸리티이다.  
glocator 프로그램은 [gloctl](48-gloctl.md#8776583f97fc3298)를 통해 cluster member 노드들의 location 정보를 제공받는다.  
glocator는 client, gloctl와 UDP 통신을 하고 gagent와 TCP 통신을 한다.

> glocator가 필요로 하는 location 정보는 listener host, listener port, db home path 이며 gloctl을 통해 이 정보들을 제공받는다.

<a id="712f3f7c35dffa25"></a>
### 사용법

```
glocator [options]
```

<a id="925f089d582bb16f"></a>
### Option

<a id="dd46fe96c431b2a7"></a>
#### help

<a id="09775447aee1c1df"></a>
##### 설명

Help 메시지를 출력한다.

<a id="f767a7132f9c8db3"></a>
##### 사용 예

```
$ glocator --help

Usage:
 glocator [options]

Options:

-c  --create       Create glocator environment
-s  --start        Start glocator
-t  --stop         Stop glocator
-f  --conf         Set configure file
-u  --status       Get glocator status
-y  --sync         Synchronize with alternate glocator(BOTH, SOURCE)
-l  --silent       Suppress display message
-r  --no-copyright Suppress display copy right and version
-h  --help         Print help message
```

<a id="3faf88aa8fb28aef"></a>
#### create

<a id="31b51e3620d09602"></a>
##### 설명

glocator의 데이터 파일을 생성한다.

<a id="05c3fdce0447eba0"></a>
##### 사용 예

```
$ glocator --create

glocator is created.
```

> glocator 데이터 파일은 &lt;GOLDILOCKS_DATA&gt;/db 디렉토리에 생성된다.

```
$ ls
README  glocator.dat  system_data.dbf  system_dict.dbf  system_undo.dbf
```

<a id="2ac127ee2f50cd73"></a>
#### start

<a id="a437fe5d4da71f3f"></a>
##### 설명

glocator를 구동한다. 같은 port를 갖는 glocator가 이미 구동 중이라면 에러가 발생한다.

<a id="f179f34916ea6ea4"></a>
##### 사용 예

```
$ glocator --start

glocator is started.
```

<a id="7ba68d0ac65053bc"></a>
#### stop

<a id="b785d638dc298cc5"></a>
##### 설명

구동 중인 glocator를 정지시킨다. 구동 중인 glocator를 멈추려면 같은 port가 설정되어야 한다.

<a id="d1d9e6da8d906774"></a>
##### 사용 예

```
$ glocator --stop

glocator is stopped.
```

<a id="1f59d6ceac0b54c8"></a>
#### conf

<a id="ce0638017bbc4e5e"></a>
##### 설명

glocator를 구동할 때 configure file을 설정한다.

<a id="d9f7d0ed5929b835"></a>
##### 사용 예

```
$ glocator --start --conf goldilocks.glocator.conf

glocator is started.
```

<a id="7ea90021e5d90c4e"></a>
#### status

<a id="8ebbaa879bb3cdfa"></a>
##### 설명

구동 중인 glocator의 상태 메시지를 출력한다. 구동 중인 glocator 상태를 확인하려면 같은 port가 설정 되어야 한다.

<a id="09e8694d1dc3ce00"></a>
##### 사용 예

```
$ glocator --status

Process ID: 26058
Configuration file: goldilocks.glocator.conf
Unix domain path: /tmp/unix-glocator.42581
Udp listen host: 0.0.0.0, Port: 42581
glocator is running.
```

<a id="33a0e611a1a7974d"></a>
#### sync

<a id="4b82ea6d4c291166"></a>
##### 설명

glocator를 구동하기 전에 ALTERNATE_LOCATORS에 설정된 glocator와 데이터를 동기화한다.

데이터 동기화에는 ALTERNATE_LOCATORS에서 데이터를 가지고 오는 SOURCE 방식과 두 glocator를 병합하는 BOTH 방식이 있다.

<a id="70fbea2a1563b8c6"></a>
##### 사용 예

다음은 sync 옵션을 SOURCE 타입으로 사용하여 성공하는 예이다.

```
$ glocator --start --sync SOURCE

glocator is started.
```

다음은 sync 옵션에 실패하는 예이다. configure 파일에 ALTERNATE_LOCATORS 속성 값이 설정되지 않았다.

```
$ glocator --start --sync SOURCE

ERR-HY000(60016): Need more alternate locator host information.
```

다음은 sync 옵션에 실패하는 예이다. ALTERNATE_LOCATORS에 설정된 glocator로부터 응답을 받지 못한 상황이다.

```
$ glocator --start --sync SOURCE

ERR-HY000(60016): Need more alternate locator host information.
```

다음은 sync 옵션에 인자가 주어지지 않았을 때 실패하는 예이다.

```
$ glocator --start --sync

ERR-HY000(11000): Invalid argument
```

<a id="813631d9b8d50572"></a>
#### silent

<a id="9f820304237306b4"></a>
##### 설명

실행에 대한 glocator의 메시지를 출력하지 않는다.

<a id="d77f064701dfc935"></a>
##### 사용 예

```
$ glocator --start --silent
```

<a id="9a4a9ae5df976416"></a>
#### no-copyright

<a id="4c55ae3a2803cb5d"></a>
##### 설명

실행에 대한 glocator의 copy right와 버전 메시지를 출력하지 않는다.

<a id="9d728a28f84dc2e2"></a>
##### 사용 예

```
$ glocator --start --no-copyright

glocator is started.
```

<a id="67d259f9ca60414c"></a>
## glocator 사용

<a id="c9da9ccd6ce0fe31"></a>
### 데이터 파일

glocator를 구동하려면 시작하기 전에 glocator 데이터 파일을 먼저 생성해야 한다.

```
$ glocator --create

glocator is created.
```

glocator 데이터 파일이 저장되는 디렉토리는 configuration [LOCATION_FILE_DIR](#18eea2137031075b)을 수정하여 변경할 수 있다. 기본값은 &lt;GOLDILOCKS_DATA&gt;/db에 생성된다. 데이터 파일은 [LOCATION_FILE_NAME](#4a10c2863918b1de) 을 수정하여 변경할 수 있다. 기본값은 glocator.dat이다.

glocator 데이터 파일의 최대 크기와 초기 크기는 configuration [LOCATION_FILE_MAX_SIZE](#b7f88e07f0b7d298)와 [LOCATION_FILE_SIZE](#fd5fbf501a2a6cff)를 수정하여 변경할 수 있다.

<a id="8e3540ba2e436767"></a>
### CSTARTUP과 CSHUTDOWN

glocator는 GOLDILOCKS 서버의 CSTARTUP과 CSHUTDOWN에 사용될 수 있다.  
이를 위해서는 glocator가 구동 중이고 gsqlnet을 통해 CSTARTUP 또는 CSHUTDOWN 명령을 실행해야 한다.  
다만, gsqlnet을 실행하는 장비의 odbc.ini에 LOCATOR_DSN과 속성값이 설정되어 있어야 한다.    
자세한 내용은 [GOLDILOCKS UNIX ODBC driver 라이브러리](../part-05-developer-manual/31-odbc.md#5d8bd69c9f8d9631)를 참조한다.

다음은 glocator를 사용하기 위해 odbc.ini에 설정한 내용이다.

```
[GOLDILOCKS]
HOST=127.0.0.1
PORT=20101
UID=sys
PWD=gliese
LOCATOR_DSN=GLOCATOR

[GLOCATOR]
HOST=127.0.0.1
PORT=42581
```

> DSN [GLOCATOR]에 FILE 속성이 있으면 glocator 대신 FILE 속성에 명시된 파일을 우선해서 사용하므로 FILE 속성을 제외해야 한다.

CSTARTUP과 CSHUTDOWN 명령을 실행하려면 glocator가 member 노드들에 대한 location 정보를 알고 있어야 한다.

<a id="b2f32a89bf2f41cf"></a>
### 다중화

<a id="422b868544e36d81"></a>
#### 개요

glocator 다중화는 데이터를 일관성있게 유지하여 장애가 발생할 경우 원격 glocator를 사용한 지속적인 서비스를 가능하게 한다.

<a id="37b14d9f540565a5"></a>
#### 설정

다중화를 사용하기 위해 각각의 glocator는 configure file에 ALTERNATE_LOCATORS 속성을 설정해야 한다. ALTERNATE_LOCATORS 속성에는 Locator_name이 설정되어야 하고 설정된 Locator_name은 HOST, PORT 속성과 함께 configure 파일에 기록되어야 한다.

ALTERNATE_LOCATORS 속성은 다음과 같이 설정할 수 있다.

```
[LOCATOR]
ALTERNATE_LOCATORS = (locator_name1,locator_name2)
[locator_name1]
HOST= ip_address
PORT = port_num
[locator_name2]
HOST= ip_address
PORT = port_num
```

다음은 ALTERNATE_LOCATORS 속성을 설정하는 configure 파일의 예이다.

```
[LOCATOR]
PORT=42581
SYNC_RESPONSE_TIMEOUT = 2
SYNC_RETRY_COUNT = 2
LOCATION_FILE_NAME='glocator_1.dat'
ALTERNATE_LOCATORS=(LOCATOR_2,LOCATOR_3)

[LOCATOR_2]
HOST=127.0.0.1
PORT=42582

[LOCATOR_3]
HOST=127.0.0.1
PORT=42583
```


> 
> - [LOCATOR]는 glocator가 기본값으로 읽어들이는 DSN이다.
> - glocator와 관련된 ODBC와 gagent 설정에 대한 자세한 내용은 [odbc.ini 파일](../part-05-developer-manual/31-odbc.md#a8dbbc9962ac8d3d), [ALTERNATE_LOCATORS](47-gagent.md#eab4982f76c0183f)을 참조한다.
> 

<a id="cdaf1b40e9d58a8d"></a>
#### 데이터 동기화

다중화된 glocator를 서비스할 때 데이터는 일관되게 유지되어야 한다. 기존에 작동 중인 glocator가 없을 경우, 모든 glocator는 일반 시작을 하면 된다. 기존에 동작 중인 glocator가 있을 경우, [sync](#33a0e611a1a7974d) 옵션을 사용하여 데이터를 동기화하는 방법으로 alternate glocator를 시작할 수 있다.

[sync](#33a0e611a1a7974d) 옵션에는 glocator 자신의 데이터와 alternate glocator의 데이터를 병합하는 BOTH와 상대 glocator로부터 데이터를 가지고 오는 SOURCE가 있다. glocator의 sync 작업은 glocator와 alternate glocator 사이의 1 : 1 대응 작업이다. 따라서 A, B, C 세 개의 glocator를 다중화하려고 할 때 A와 B가 이미 구동 중이고 C를 BOTH 방식으로 sync하여 구동하면 A 또는 B glocator의 데이터가 서로 다를 수 있다.

서비스 중인 glocator는 변경된 내용만 동기화한다. 패킷 손실 등의 이유로 데이터 동기화에 실패하는 경우 데이터가 서로 다를 수 있다. 이 경우, [gloctl](48-gloctl.md#8776583f97fc3298) 프로그램을 사용하여 해당 glocator에서 직접 데이터를 수정하거나 glocator를 sync 옵션으로 다시 시작할 수 있다.

<a id="5c10f41b662ec0d4"></a>
## 기능

<a id="b8476a5e4f93eb40"></a>
### Connection Service

Cluster 환경에서 특정 노드에 대한 location 정보를 알지 못해도 사용자가 정한 몇 개의 노드 중에 임의로 접속할 수 있도록 service 기능을 제공한다.

Service 기능은 glocator에서 관리하는 노드를 사용자가 임의의 그룹으로 지정하는 것이다. 이 service는 gloctl 프로그램을 사용하여 등록할 수 있다. glocator에서 관리하는 서비스 목록 역시 gloctl 프로그램을 사용하여 확인할 수 있다.

응용 프로그램은 ODBC 드라이버를 사용하여 접속해야 하며 [odbc.ini 파일](../part-05-developer-manual/31-odbc.md#a8dbbc9962ac8d3d)에 LOCATOR_DSN과 LOCATOR_SERVICE 속성을 지정해야 한다.

<a id="cdfefec782e48962"></a>
![locator_service](../assets/images/d6fa3905864b8907.png)

위 그림은 응용 프로그램 (application)이 service s3에 속한 g1n1에 접속한 내용이다. ODBC 드라이버가 service를 이용하여 연결하는 순서는 service에 등록된 노드 순서와 동일하다. 위의 예에서 ODBC 드라이버가 g1n1에 연결하는데 실패하면 다음 순서인 노드 g2n1에 연결을 시도할 것이다.

> Service 기능을 사용하려면 glocator에 노드의 유효한 location 정보가 먼저 입력되어야 한다.

<a id="6ed3d95585114cb6"></a>
### Cluster Failover

glocator는 server가 failover를 진행할 때 도움이 된다.

Server 프로퍼티 [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#b0f8ad4bc44dbe18) 값이 1 또는 2로 설정되고, cluster 환경에서 노드 간에 연결이 끊어져 failover가 발생하면 각 노드는 cluster failover를 진행하여 gagent를 통해 glocator에게 자신의 viability를 질의한다.

질의를 받은 glocator는 연결이 끊어진 두 노드의 viability를 판단하고 질의를 한 gagent에 결과를 전달한다.

Viabilty 결과를 받은 노드는 종료되거나 failover를 진행한다.

> Server의 cluster failover 처리 시간은 여러 프로퍼티와 상관 관계가 있다.   
> Server 프로퍼티 [LOCATOR_QUERY_TIMEOUT](../part-02-administration-manual/10-server-property.md#8d44bdd2f47e6621)는 server가 glocator에게 질의한 후에 응답을 기다리는 시간으로서 기본값은 3초로 설정되어 있다.  
> Server 프로퍼티 [CLUSTER_SPLIT_BRAIN_RETRY_COUNT](../part-02-administration-manual/10-server-property.md#a1df217a5b6ac36a)는 glocator로부터 응답을 받지 못했을 때 다시 질의하는 횟수로서 cluster failover 처리 시간과 관계가 있다. 기본값은 1이다.

<a id="3acd083067bab56b"></a>
## glocator Configuration

<a id="46d8623ef1ef9192"></a>
### Configuration File 및 환경 변수

glocator는 configuration을 설정하기 위해 file 또는 환경 변수를 사용할 수 있다.

환경 변수는 configuration property name에 prefix로 'LOCATOR_'를 추가한 name을 사용하여 지정할 수 있다. 예를 들어 configuration file에 HOST를 설정하면 $LOCATOR_HOST를 지정하는 것과 같은 효과가 있다.

Configuration file 내용은 환경 변수 설정값보다 우선한다.

glocator는 DSN을 [LOCATOR] 기본값으로 하여 configuration file을 읽는다.

glocator는 $GOLDILOCKS_DATA/conf/goldilocks.glocator.conf 파일을 자신의 환경 파일로 가지고 있다. glocator의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 환경 변수를 설정하고 glocator를 구동하면 된다.

<a id="eb66e44ea3e0ce3a"></a>
### Configuration Property

<a id="a147b5a06237d78d"></a>
#### HOST

<a id="af8b099371edbac7"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | HOST |
| 설명 | glocator가 bind 하는 IP address이다. |
| Data type | ip address (ip v4) |
| 기본값/ 범위 | 0.0.0.0 |

glocator가 UDP 통신을 위해 bind하는 IP address이다.   
IP v4 형식의 IP address를 사용한다.

<a id="26f24ffed16325e9"></a>
#### PORT

<a id="08f775262bb54bca"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | glocator가 Recv를 기다리는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 42581 / 1024~49151 |

glocator가 UDP 통신으로 packet을 받는 port이다.   
Port는 1024부터 49151까지 사용할 수 있다.

<a id="250310ba16967d42"></a>
#### WORKER_COUNT

<a id="78eb8845ec39fccf"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | WORKER_COUNT |
| 설명 | Job을 처리하는 thread의 개수이다. |
| Data type | INT |
| 기본값/ 범위 | 1 / 1~8 |

glocator가 client 또는 내부 프로세스로부터 받은 packet을 처리하는 thread의 개수이다.

<a id="489a04c779d6628e"></a>
#### MAX_NODE_COUNT

<a id="a730c10395da62a0"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAX_NODE_COUNT |
| 설명 | 연결 가능한 gagent의 최대 개수이다. |
| Data type | INT |
| 기본값/ 범위 | 64 / 1~8192 |

연결 가능한 gagent의 최대 개수이다.

<a id="fe44beacb57c6bd8"></a>
#### MESSAGE_QUEUE_SIZE

<a id="7c01115d66489923"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MESSAGE_QUEUE_SIZE |
| 설명 | 수신한 packet을 처리하기 전까지 저장하는 queue size이다. |
| Data type | INT |
| 기본값/ 범위 | 33554432 / 10485760~2147483648 |

glocator가 client나 내부 프로세스로부터 받은 packet을 처리하기 전에 저장하는 queue의 size이다.  
Queue에는 packet이 message 단위의 단일 item으로 저장된다.

<a id="478c1891a06c7850"></a>
#### MESSAGE_ALLOCATOR_SIZE

<a id="314775378ac94739"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MESSAGE_ALLOCATOR_SIZE |
| 설명 | Message queue에 저장되는 item을 할당하는 allocator size이다. |
| Data type | INT |
| 기본값/ 범위 | 33554432 / 10485760~2147483648 |

Message queue에 저장되는 item (message)을 할당할 때 사용되는 allocator의 size이다.

<a id="c7d976981a8fcb89"></a>
#### PACKET_ALLOCATOR_SIZE

<a id="b3b263c543b97045"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PACKET_ALLOCATOR_SIZE |
| 설명 | UDP 통신으로 packet을 받을 때 packet을 할당하는 allocator size이다. |
| Data type | INT |
| 기본값/ 범위 | 33554432 / 10485760~2147483648 |

glocator가 packet을 받기 위해 할당하는 buffer를 위한 allocator의 size이다.

<a id="6076294be57b8f29"></a>
#### SYSTEM_LOGGER_DIR

<a id="d26a13ff0787b17f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_LOGGER_DIR |
| 설명 | glocator의 trace log file의 directory path이다. |
| Data type | String |
| 기본값/ 범위 | &lt;GOLDILOCKS_DATA&gt;/trc |

glocator의 system trace log file이 저장되는 directory path이다. 기본값의 &lt;GOLDILOCKS_DATA&gt;는 $GOLDILOCKS_DATA 환경 변수 값으로 대체된다.

<a id="1aa24dc54080de09"></a>
#### SYSTEM_UDS_DIR

<a id="25d94c00c0fefa19"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_UDS_DIR |
| 설명 | glocator에서 사용되는 unix domain socket 파일이 저장되는 directory path이다. |
| Data type | String |
| 기본값/ 범위 | /tmp (최대 60 byte) |

glocator에서 사용되는 unix domain socket 파일이 저장되는 directory path를 설정한다. Directory 최대 길이는 60 byte 이내로 설정해야 한다.

<a id="18eea2137031075b"></a>
#### LOCATION_FILE_DIR

<a id="23728ee71d481092"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATION_FILE_DIR |
| 설명 | glocator에서 사용되는 location 파일이 저장되는 directory path이다. |
| Data type | String |
| 기본값/ 범위 | &lt;GOLDILOCKS_DATA&gt;/db |

glocator에서 사용되는 location 파일이 저장되는 directory path를 설정한다.

<a id="4a10c2863918b1de"></a>
#### LOCATION_FILE_NAME

<a id="5b7f592416f4df4f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATION_FILE_NAME |
| 설명 | glocator에서 사용되는 location 파일 이름이다. |
| Data type | String |
| 기본값/ 범위 | glocator.dat |

glocator에서 사용되는 location 파일 이름을 설정한다.   
기본값은 glocator.dat 이다.

<a id="fd5fbf501a2a6cff"></a>
#### LOCATION_FILE_SIZE

<a id="71a86274a890975f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATION_FILE_SIZE |
| 설명 | Location 파일의 초기 size이다. |
| Data type | Int |
| 기본값/ 범위 | 1048576 / 104576~2147483648 |

glocator에서 사용되는 location 파일의 초기 size를 설정한다.

<a id="b7f88e07f0b7d298"></a>
#### LOCATION_FILE_MAX_SIZE

<a id="acc0ad7079a34a2b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATION_FILE_MAX_SIZE |
| 설명 | Location 파일의 최대 size이다. |
| Data type | Int |
| 기본값/ 범위 | 10485760 / 104576~2147483648 |

glocator에서 사용되는 location 파일의 최대 size를 설정한다.

<a id="042d06bb2ed8d6a2"></a>
#### MESSAGE_TIMEOUT

<a id="4230ffb95475fcd8"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MESSAGE_TIMEOUT |
| 설명 | glocator가 packet을 수신하기 위해 최대로 대기하는 시간을 설정한다. |
| Data type | Int |
| 기본값/ 범위 | 100 / 0 ~2147483648 (second 단위) |

glocator가 packet을 수신하기 위해 최대로 대기하는 시간 (초)을 설정한다. 처리되지 못하고 시간 초과된 packet은 버려진다.

<a id="c847846bfa9efd1a"></a>
#### ALTERNATE_LOCATORS

<a id="a89326b6f6293cf4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ALTERNATE_LOCATORS |
| 설명 | glocator의 alternate locator, 다중화 설정을 한다. |
| Data type | String |
| 기본값/ 범위 | empty / 0 ~ 1024 bytes |

glocator의 [다중화](#b2f32a89bf2f41cf)를 설정한다.

<a id="0a623e2867592bd9"></a>
#### SYNC_RETRY_COUNT

<a id="5ec42fb9c9953a47"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYNC_RETRY_COUNT |
| 설명 | glocator가 alternate locator와의 동기화 작업에 실패할 경우 다시 시도하는 횟수를 설정한다. |
| Data type | Int |
| 기본값/ 범위 | 1 / 0 ~ 5 |

glocator 동기화 작업의 재전달 횟수를 설정한다.

데이터가 변경되었을 때 glocator는 alternate locator에 변경된 데이터를 전달하는데, 데이터를 전달한 후에 응답을 받지 못하면 다시 전달한다.

<a id="418efe8a973b337f"></a>
#### SYNC_RESPONSE_TIMEOUT

<a id="a627d754b172f387"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYNC_RESPONSE_TIMEOUT |
| 설명 | glocator 동기화 작업에 대한 응답 대기 시간을 설정한다. |
| Data type | Int |
| 기본값/ 범위 | 5 / 1 ~ 20 |

glocator가 전달한 동기화 데이터에 대한 응답을 기다리는 시간을 설정한다.

<a id="98bd8449d7d9ef3f"></a>
#### KEEPALIVE_IDLE_TIME

<a id="7a0caf1f645d648e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_IDLE_TIME |
| 설명 | tcp keepalive idle time for checking dead client session (sec) |
| Data type | INT |
| 기본값/ 범위 | 1 / 1 ~ 16383 |

Keep alive packet을 송신하기 전에 TCP 패킷이 송수신 되지 않는 상태로 지속되는 시간 (idle) 이다. 즉, KEEPALIVE_IDLE_TIME에 설정된 초 동안 TCP 패킷 교환이 이루어지지 않으면 dead connection을 감지하기 위해 keep alive mechanism을 수행한다.

<a id="d6f126cbf4c50cab"></a>
#### KEEPALIVE_COUNT

<a id="20902d46486699e9"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_COUNT |
| 설명 | tcp keepalive check count |
| Data type | INT |
| 기본값/ 범위 | 5 / 1 ~ 10 |

Keep alive mechanism을 수행하는 횟수이다.

<a id="304aa4af39a50522"></a>
#### KEEPALIVE_INTERVAL

<a id="37f13c23798f3438"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_INTERVAL |
| 설명 | tcp keepalive packet interval (sec) |
| Data type | INT |
| 기본값/ 범위 | 5 |

Keep alive 패킷을 전송하는 시간 간격이다.

---

[← 45. gtrclogger](45-gtrclogger.md) · [전체 목차](../README.md) · [47. gagent →](47-gagent.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
