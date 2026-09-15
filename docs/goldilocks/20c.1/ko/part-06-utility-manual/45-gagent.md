<a id="8fc6cc08b617f1a5"></a>

# 45. gagent

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/8fc6cc08b617f1a5)  
> 태그: `20c.1_30_tag`

[← 44. glocator](44-glocator.md) · [전체 목차](../README.md) · [46. gloctl →](46-gloctl.md)

<a id="e18ef894338a158f"></a>
## gagent 소개

<a id="a5e81f8c261d64cd"></a>
### 정의

gagent는 GOLDILOCKS cluster system에서 각 멤버 노드와 함께 실행되어 [glocator](44-glocator.md#d00263d8ce9e1ce2)와 communication 하는 유틸리티이다.

gagent가 속한 노드의 서버 프로퍼티 [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#e29c13f6b906efd3) 값이 1 또는 2로 설정되고 노드 간에 연결이 끊어져서 cluster failover가 진행되면 gagent는 glocator에게 자신이 속한 노드의 viability를 질의한다.   
자세한 내용은 [Cluster Failover](44-glocator.md#df480f16964700c7)를 참조한다.

<a id="77200b24d98e884b"></a>
### 사용법

```
gagent [options]
```

<a id="ada44d0d61084850"></a>
### Option

<a id="a52b1721c0dd2f04"></a>
#### help

<a id="b217021e29078038"></a>
##### 설명

Help 메시지를 출력한다.

<a id="7bdd15dc0ba3074f"></a>
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

<a id="ae43a9e54aa770f4"></a>
#### start

<a id="61ba4b7d3dae5ff4"></a>
##### 설명

gagent를 구동한다. 같은 home 디렉토리를 갖는 gagent가 이미 구동 중이라면 에러가 발생한다.

<a id="a551a9a761b167ee"></a>
##### 사용 예

```
$ gagent --start

gagent is started.
```

<a id="7c5144d42da26ce6"></a>
#### stop

<a id="5fc2ef02c8d612a6"></a>
##### 설명

구동 중인 gagent를 멈추게 한다. 구동 중인 gagent를 멈추려면 동일한 home 디렉토리가 설정되어야 한다.

<a id="d93804975430eb8f"></a>
##### 사용 예

```
$ gagent --stop

gagent is stopped.
```

<a id="62ed3b3a822d0da3"></a>
#### status

<a id="0526782be671193e"></a>
##### 설명

구동 중인 gagent의 상태 메시지를 출력한다. 구동 중인 gagent 상태를 확인하려면 동일한 home directory가 설정되어야 한다.

<a id="225fe428a6bfd60a"></a>
##### 사용 예

```
$ gagent --status

gagent(31938) is running.
```

<a id="77f52b1548235de3"></a>
#### conf

<a id="8ba65bf1e0262de7"></a>
##### 설명

gagent를 구동할 때 configure file을 설정한다.

<a id="b3b962e252d77a07"></a>
##### 사용 예

```
$ gagent --start --conf goldilocks.gagent.conf

gagent is started.
```

<a id="4b73edbdd02b9ab2"></a>
#### home

<a id="4280d14a9aa1e2b6"></a>
##### 설명

gagent를 구동할 때 GOLDILOCKS의 서버 홈 디렉토리를 설정한다.   
상대 경로를 사용할 경우 &lt;GOLDILOCKS_DATA&gt;를 기준으로 홈 디렉토리를 찾는다. &lt;GOLDILOCKS_DATA&gt;는 $GOLDILOCKS_DATA 환경 변수의 값으로 대체된다.

<a id="e81124e04b76e3e5"></a>
##### 사용 예

```
$ gagent --start --home g1n1_home --conf goldilocks.gagent.conf  

gagent is started.
```

위의 예에서 gagent는 &lt;GOLDILOCKS_DATA&gt;/g1n1_home을 홈으로 설정하여 구동된다.

<a id="dfec647fd35bb591"></a>
#### silent

<a id="6c68595eccfcb99b"></a>
##### 설명

실행에 대한 gagent의 메시지를 출력하지 않는다.

<a id="c1178470d9188acc"></a>
##### 사용 예

```
$ gagent --start --silent

 Copyright (C) 2010 SUNJESOFT Inc. All rights reserved.
```

<a id="a9bcc825a17fcf60"></a>
#### no-copyright

<a id="d4498f9b53aab401"></a>
##### 설명

실행에 대한 gagent의 copy right와 버전 메시지를 출력하지 않는다.

<a id="9fcb60acfb79ebe6"></a>
##### 사용 예

```
$ gagent --start --no-copyright

gagent is started.
```

<a id="c306d5ff4f7da7f7"></a>
## gagent Configuration

<a id="3dbaae474272aacc"></a>
### Configuration File 및 환경 변수

gagent는 configuration을 설정하기 위해 file 또는 환경 변수를 사용할 수 있다.

환경 변수는 configuration property name에 prefix로 'AGENT_' 를 추가한 name을 사용하여 지정할 수 있다. 예를 들어 configuration file에 HOST를 설정하면 $AGENT_HOST를 지정하는 것과 같은 효과가 있다.

Configuration file의 내용은 환경 변수 설정값보다 우선한다.

gagent는 $GOLDILOCKS_DATA/conf/goldilocks.gagent.conf 파일을 자신의 환경 파일로 가지고 있다. gagent의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 환경 변수를 설정하고 gagent를 구동하면 된다.

<a id="2d29fd154ebbd3d1"></a>
### Configuration Property

<a id="17994f05500d8932"></a>
#### HOST

<a id="85196227b428cfd3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | HOST |
| 설명 | gagent가 bind 하는 IP address이다. |
| Data type | ip address (ip v4) |
| 기본값/ 범위 | 0.0.0.0 |

gagent가 UDP 통신을 위해 bind하는 IP address이다.   
IP v4 형식의 IP address를 사용한다.

<a id="151b0a59fb95b2a3"></a>
#### REQUEST_PORT

<a id="cc94f32eccc8e05c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | REQUEST_PORT |
| 설명 | gagent가 request에 사용하는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 43581 / 1024~49151 |

gagent가 tcp 통신을 할 때 glocator에게 request 하는 용도로 사용하는 port이다.   
Port는 1024부터 49151까지 사용할 수 있다.

<a id="d25274fee4c8d5bb"></a>
#### RESPONSE_PORT

<a id="04c8d64a1efc31c6"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | RESPONSE_PORT |
| 설명 | gagent가 response에 사용하는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 43582 / 1024~49151 |

gagent가 tcp 통신을 할 때 glocator로부터 response 받는 용도로 사용하는 port이다.   
Port는 1024부터 49151까지 사용할 수 있다.

<a id="a16e6380062163ba"></a>
#### LOCATOR_HOST

<a id="ba052917c33a471c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATOR_HOST |
| 설명 | glocator의 IP address이다. |
| Data type | ip address(ip v4) |
| 기본값/ 범위 | 0.0.0.0 |

glocator의 IP address이다.

<a id="20dbd1860fa0db34"></a>
#### LOCATOR_PORT

<a id="9459a7dde0d8ee4a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATOR_PORT |
| 설명 | glocator가 Recv를 기다리는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 42581 / 1024~49151 |

gagent가 glocator에게 packet을 보낼 때 glocator의 port이다.   
Port는 1024부터 49151까지 사용할 수 있다.

<a id="6ff74c163d7a3215"></a>
#### SYSTEM_LOGGER_DIR

<a id="95f95f8d2c2468b3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_LOGGER_DIR |
| 설명 | gagent의 trace log file의 directory path이다. |
| Data type | String |
| 기본값/ 범위 | &lt;GOLDILOCKS_DATA&gt;/trc |

gagent의 system trace log file이 저장되는 directory path이다. 기본값의 &lt;GOLDILOCKS_DATA&gt;는 $GOLDILOCKS_DATA 환경 변수 값으로 대체된다.

<a id="7e27aeec9c8aa752"></a>
#### SYSTEM_UDS_DIR

<a id="de2077ccd67097bf"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_UDS_DIR |
| 설명 | gagent의 Unix Domain Socket file의 directory path이다. |
| Data type | String |
| 기본값/ 범위 | /tmp (최대 50 byte) |

gagent의 Unix Domain Socket file이 저장되는 directory path이다. 기본값은 /tmp 이다. Directory의 최대 길이는 50 byte 이내로 설정해야 한다.

<a id="4198fe58392d6106"></a>
#### ALTERNATE_LOCATORS

<a id="199b97f388de34b9"></a>
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

<a id="8a1039afdef7040e"></a>
#### KEEPALIVE_IDLE_TIME

<a id="5354ba9ac984315d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_IDLE_TIME |
| 설명 | tcp keepalive idle time for checking dead client session (sec) |
| Data type | INT |
| 기본값/ 범위 | 1 / 1 ~ 16383 |

Keep alive packet을 송신하기 전에 TCP 패킷이 송수신 되지 않는 상태로 지속되는 시간 (idle) 이다. 즉, KEEPALIVE_IDLE_TIME에 설정된 초 동안 TCP 패킷 교환이 이루어지지 않으면 dead connection을 감지하기 위해 keep alive mechanism을 수행한다.

<a id="f81b5dcb1d9abece"></a>
#### KEEPALIVE_COUNT

<a id="b8fa9b0a6b56c685"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_COUNT |
| 설명 | tcp keepalive check count |
| Data type | INT |
| 기본값/ 범위 | 5 / 1 ~ 10 |

Keep alive mechanism을 수행하는 횟수이다.

<a id="15018094cc453738"></a>
#### KEEPALIVE_INTERVAL

<a id="0d6d82f9a2b07ec9"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_INTERVAL |
| 설명 | tcp keepalive packet interval (sec) |
| Data type | INT |
| 기본값/ 범위 | 5 |

Keep alive 패킷을 전송하는 시간 간격이다.

---

[← 44. glocator](44-glocator.md) · [전체 목차](../README.md) · [46. gloctl →](46-gloctl.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
