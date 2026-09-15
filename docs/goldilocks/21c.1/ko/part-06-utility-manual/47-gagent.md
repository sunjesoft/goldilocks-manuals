<a id="d0c0bebe34955439"></a>

# 47. gagent

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/d0c0bebe34955439)  
> 태그: `21c.1_35_tag`

[← 46. glocator](46-glocator.md) · [전체 목차](../README.md) · [48. gloctl →](48-gloctl.md)

<a id="6490dff9899b0954"></a>
## gagent 소개

<a id="53eea6b609bfdc8c"></a>
### 정의

gagent는 GOLDILOCKS cluster system에서 각 멤버 노드와 함께 실행되어 [glocator](46-glocator.md#6aa340ae6a2d0c28)와 communication 하는 유틸리티이다.

gagent가 속한 노드의 서버 프로퍼티 [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#b0f8ad4bc44dbe18) 값이 1 또는 2로 설정되고 노드 간에 연결이 끊어져서 cluster failover가 진행되면 gagent는 glocator에게 자신이 속한 노드의 viability를 질의한다.   
자세한 내용은 [Cluster Failover](46-glocator.md#6ed3d95585114cb6)를 참조한다.

<a id="787cf3ec3780d54b"></a>
### 사용법

```
gagent [options]
```

<a id="a5d3f3c506e6509b"></a>
### Option

<a id="493e4c5abf9232bf"></a>
#### help

<a id="a0260a4bcc0511b4"></a>
##### 설명

Help 메시지를 출력한다.

<a id="2a9ba55d2337cb55"></a>
##### 사용 예

```
$ gagent --help

Usage:
 gagent [options]

Options:

-s  --start                        Start gagent
-t  --stop                         Stop gagent
-u  --status                       Get gagent status
-f  --conf                         Set configure file
-o  --home                         gmaster home path
-l  --silent                       Suppress display message
-r  --no-copyright                 Suppress display copy right and version
-h  --help                         Print help message
```

<a id="cd1dbd367d8396ca"></a>
#### start

<a id="bb4dc05ede1b2783"></a>
##### 설명

gagent를 구동한다. 같은 home 디렉토리를 갖는 gagent가 이미 구동 중이라면 에러가 발생한다.

<a id="a375bfbd746de674"></a>
##### 사용 예

```
$ gagent --start

gagent is started.
```

<a id="b00a54506ec36132"></a>
#### stop

<a id="1269e11f3a2f51f0"></a>
##### 설명

구동 중인 gagent를 멈추게 한다. 구동 중인 gagent를 멈추려면 동일한 home 디렉토리가 설정되어야 한다.

<a id="5184dfc3c2c3d59c"></a>
##### 사용 예

```
$ gagent --stop

gagent is stopped.
```

<a id="27aaf5f9ba827ce6"></a>
#### status

<a id="00126a690e7ad694"></a>
##### 설명

구동 중인 gagent의 상태 메시지를 출력한다. 구동 중인 gagent 상태를 확인하려면 동일한 home directory가 설정되어야 한다.

<a id="7b9496fc1e43d72f"></a>
##### 사용 예

```
$ gagent --status

gagent(31938) is running.
```

<a id="002bf0d117db63b6"></a>
#### conf

<a id="2e42df7b9fe1a0fc"></a>
##### 설명

gagent를 구동할 때 configure file을 설정한다.

<a id="132a39cd4189d9b3"></a>
##### 사용 예

```
$ gagent --start --conf goldilocks.gagent.conf

gagent is started.
```

<a id="a99f1da4444a4a96"></a>
#### home

<a id="b66a28e1f070dee5"></a>
##### 설명

gagent를 구동할 때 GOLDILOCKS의 서버 홈 디렉토리를 설정한다.   
상대 경로를 사용할 경우 &lt;GOLDILOCKS_DATA&gt;를 기준으로 홈 디렉토리를 찾는다. &lt;GOLDILOCKS_DATA&gt;는 $GOLDILOCKS_DATA 환경 변수의 값으로 대체된다.

<a id="fed5d0aa1d3d71bc"></a>
##### 사용 예

```
$ gagent --start --home g1n1_home --conf goldilocks.gagent.conf  

gagent is started.
```

위의 예에서 gagent는 &lt;GOLDILOCKS_DATA&gt;/g1n1_home을 홈으로 설정하여 구동된다.

<a id="6d7a1d9c09f3ad30"></a>
#### silent

<a id="7e0a7644abdfbe6f"></a>
##### 설명

실행에 대한 gagent의 메시지를 출력하지 않는다.

<a id="4ae3574603d1b0bc"></a>
##### 사용 예

```
$ gagent --start --silent

 Copyright (C) 2010 SUNJESOFT Inc. All rights reserved.
```

<a id="80577d63c8f16766"></a>
#### no-copyright

<a id="920c3066cfde5082"></a>
##### 설명

실행에 대한 gagent의 copy right와 버전 메시지를 출력하지 않는다.

<a id="704942f585f17e93"></a>
##### 사용 예

```
$ gagent --start --no-copyright

gagent is started.
```

<a id="1fe9959f1117e3ff"></a>
## gagent Configuration

<a id="108aba93f0090e60"></a>
### Configuration File 및 환경 변수

gagent는 configuration을 설정하기 위해 file 또는 환경 변수를 사용할 수 있다.

환경 변수는 configuration property name에 prefix로 'AGENT_' 를 추가한 name을 사용하여 지정할 수 있다. 예를 들어 configuration file에 HOST를 설정하면 $AGENT_HOST를 지정하는 것과 같은 효과가 있다.

Configuration file의 내용은 환경 변수 설정값보다 우선한다.

gagent는 $GOLDILOCKS_DATA/conf/goldilocks.gagent.conf 파일을 자신의 환경 파일로 가지고 있다. gagent의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 환경 변수를 설정하고 gagent를 구동하면 된다.

<a id="583f8a779d26ae13"></a>
### Configuration Property

<a id="02125dacd30e50fa"></a>
#### HOST

<a id="7026a5ec2e13a08b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | HOST |
| 설명 | gagent가 bind 하는 IP address이다. |
| Data type | ip address (ip v4) |
| 기본값/ 범위 | 0.0.0.0 |

gagent가 UDP 통신을 위해 bind하는 IP address이다.   
IP v4 형식의 IP address를 사용한다.

<a id="9f55075b61adbb0b"></a>
#### REQUEST_PORT

<a id="3531dc4319789090"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | REQUEST_PORT |
| 설명 | gagent가 request에 사용하는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 43581 / 1024~49151 |

gagent가 tcp 통신을 할 때 glocator에게 request 하는 용도로 사용하는 port이다.   
Port는 1024부터 49151까지 사용할 수 있다.

<a id="eb0182c5d4e7e483"></a>
#### RESPONSE_PORT

<a id="59533d613170baa2"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | RESPONSE_PORT |
| 설명 | gagent가 response에 사용하는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 43582 / 1024~49151 |

gagent가 tcp 통신을 할 때 glocator로부터 response 받는 용도로 사용하는 port이다.   
Port는 1024부터 49151까지 사용할 수 있다.

<a id="e54ed717ffe2c300"></a>
#### LOCATOR_HOST

<a id="c63d8cd220633c4a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATOR_HOST |
| 설명 | glocator의 IP address이다. |
| Data type | ip address(ip v4) |
| 기본값/ 범위 | 0.0.0.0 |

glocator의 IP address이다.

<a id="5cec156a0ca84bb7"></a>
#### LOCATOR_PORT

<a id="03e07c32a2f5dc09"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATOR_PORT |
| 설명 | glocator가 Recv를 기다리는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 42581 / 1024~49151 |

gagent가 glocator에게 packet을 보낼 때 glocator의 port이다.   
Port는 1024부터 49151까지 사용할 수 있다.

<a id="1fe1b00b0fc36f3a"></a>
#### SYSTEM_LOGGER_DIR

<a id="08f275a7677bc0cf"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_LOGGER_DIR |
| 설명 | gagent의 trace log file의 directory path이다. |
| Data type | String |
| 기본값/ 범위 | &lt;GOLDILOCKS_DATA&gt;/trc |

gagent의 system trace log file이 저장되는 directory path이다. 기본값의 &lt;GOLDILOCKS_DATA&gt;는 $GOLDILOCKS_DATA 환경 변수 값으로 대체된다.

<a id="06b11bc644046c52"></a>
#### SYSTEM_UDS_DIR

<a id="3aac43afeef647dc"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_UDS_DIR |
| 설명 | gagent의 Unix Domain Socket file이 저장되는 directory path이다. |
| Data type | String |
| 기본값/ 범위 | /tmp (최대 50 byte) |

gagent의 Unix Domain Socket file이 저장되는 directory path이다. 기본값은 /tmp 이다. Directory 길이는 최대 50 byte까지 설정할 수 있다.

<a id="eab4982f76c0183f"></a>
#### ALTERNATE_LOCATORS

<a id="a6325b18b7069b76"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ALTERNATE_LOCATORS |
| 설명 | alternate locators를 설정한다. |
| Data type | String |
| 기본값/ 범위 | empty / 0 ~ 1024 |

gagent에 설정된 glocator로부터 응답을 받지 못하는 경우, alternate locator로 대체하여 작업을 진행한다.

다음은 ALTERNATE_LOCATOR를 사용한 configure 파일의 예이다.

```
[AGENT]
PORT=43581
LOCATOR_HOST=127.0.0.1
LOCATOR_PORT=42581
ALTERNATE_LOCATORS=(LOCATOR1,LOCATOR2)

[LOCATOR1]
HOST=127.0.0.1
PORT=42582

[LOCATOR2]
HOST=127.0.0.1
PORT=42583
```

<a id="116be3222fd3ac17"></a>
#### KEEPALIVE_IDLE_TIME

<a id="7f7dcbc7064677b8"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_IDLE_TIME |
| 설명 | tcp keepalive idle time for checking dead client session (sec) |
| Data type | INT |
| 기본값/ 범위 | 1 / 1 ~ 16383 |

Keep alive packet을 송신하기 전에 TCP 패킷이 송수신 되지 않는 상태로 지속되는 시간 (idle) 이다. 즉, KEEPALIVE_IDLE_TIME에 설정된 초 동안 TCP 패킷 교환이 이루어지지 않으면 dead connection을 감지하기 위해 keep alive mechanism을 수행한다.

<a id="3d7aa6a8adee8e51"></a>
#### KEEPALIVE_COUNT

<a id="85d6647b7b4c9ee2"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_COUNT |
| 설명 | tcp keepalive check count |
| Data type | INT |
| 기본값/ 범위 | 5 / 1 ~ 10 |

Keep alive mechanism을 수행하는 횟수이다.

<a id="6cc835ae3c782816"></a>
#### KEEPALIVE_INTERVAL

<a id="2c24920e6a22eb03"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_INTERVAL |
| 설명 | tcp keepalive packet interval (sec) |
| Data type | INT |
| 기본값/ 범위 | 5 |

Keep alive 패킷을 전송하는 시간 간격이다.

---

[← 46. glocator](46-glocator.md) · [전체 목차](../README.md) · [48. gloctl →](48-gloctl.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
