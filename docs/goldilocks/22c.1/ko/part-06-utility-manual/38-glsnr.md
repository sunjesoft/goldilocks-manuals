<a id="bd7e34b22186628b"></a>

# 38. glsnr

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/bd7e34b22186628b)  
> 태그: `22c.1_10_tag`

[← 37. gcreatedb](37-gcreatedb.md) · [전체 목차](../README.md) · [39. gsql/gsqlnet (Interactive SQL Tool) →](39-gsql-gsqlnet-interactive-sql-tool.md)

<a id="b3132afdd4ab20cc"></a>
## glsnr 소개

glsnr은 GOLDILOCKS가 client/ server 환경에서 network를 통해 원격으로 접속할 수 있게 해주는 listener이다. Network를 통해 GOLDILOCKS에 접속하려면 반드시 서버 쪽에 glsnr이 구동되어 있어야 한다.

glsnr은 다음과 같이 사용한다.

```
$ glsnr [options]
```

<a id="70d28cb643e72352"></a>
## Command Option

glsnr을 사용하기 위한 셀 프롬프트 옵션은 다음과 같다.

<a id="7f1d4dd777477b8e"></a>
### --silent

<a id="eba5c3b4979cebaf"></a>
#### 설명

실행에 대한 message를 출력하지 않는다.

<a id="0175571539bb2960"></a>
#### 사용 예

```
$ glsnr --start --silent
```

<a id="a283b04d8b0ba154"></a>
### --start

<a id="badc567cec2bd2a7"></a>
#### 설명

glsnr를 구동한다. 만약 이미 구동중이었으면 에러가 발생한다.

<a id="4720ac7a189e6e06"></a>
#### 사용 예

```
$ glsnr --start
Listener is started successfully.
```

<a id="a11575be4bb50461"></a>
### --stop

<a id="d58dc8b0381f8f0c"></a>
#### 설명

현재 구동 중인 glsnr을 멈춘다.

<a id="3d2a49f96804844a"></a>
#### 사용 예

```
$ glsnr --stop
Listener is stopped.
```

<a id="87193fe50ce09e62"></a>
### --status

<a id="d7256c75059e11e6"></a>
#### 설명

glsnr의 상태 메시지를 출력한다.

<a id="d7a3b6ae4818bf9b"></a>
#### 사용 예

```
$ glsnr --status
Listener is not running.
$ glsnr --start
Listener is started successfully.
$ glsnr --status
Listener process ID : 27880
Listener configuration file : /home/goldilocks/goldilocks_home/conf/goldilocks.listener.conf
Unix Domain Path : /tmp/unix-glsnr.22581
TCP Listen Host : 0.0.0.0, Port : 22581
default C/S mode : Dedicated
Connection Timeout(second) : 100

Listener is running.
```

<a id="6b741fa49a0c9138"></a>
### --home

<a id="e5113748e041cea0"></a>
#### 설명

db home을 설정한다.

<a id="adde7396249878f6"></a>
#### 사용 예

```
$ glsnr --start --home Gliese/home/g1n1_home
Listener is started successfully.
$ glsnr --status

Listener process ID : 20777
Listener configuration file : /home/goldilocks/Gliese/home/g1n1_home/conf/goldilocks.listener.conf
Unix Domain Path : /tmp/unix-glsnr.22581
TCP Listen Host : 0.0.0.0, Port : 22581
default C/S mode : Dedicated
Connection Timeout(second) : 100

Listener is running.
```

<a id="b539d806f7f310dd"></a>
### --help

<a id="f857989817b3896e"></a>
#### 설명

Help message를 출력한다.

<a id="6905cee9d555998b"></a>
#### 사용 예

```
$ glsnr --help
 
Usage:
  glsnr [options]
 
Options:
 
  --silent       don't print message
  --start        start listener
  --stop         stop listener
  --status       show listener status
  --help         show listner help messages
```

<a id="4880ee914e2ccc06"></a>
## Listener Configuration

<a id="af5544574b93c2dd"></a>
### Configuration File 및 환경 변수

glsnr는 configuration을 설정하기 위해 configuration file이나 환경 변수를 사용할 수 있다.

환경 변수를 설정하려면 configuration의 property name에 prefix로 'GOLDILOCKS_'를 추가한 name을 사용한다. 예를 들어 configuration file에 LISTEN_PORT를 설정하면 $GOLDILOCKS_LISTEN_PORT를 지정하는 것과 같은 효과가 있다.

Configuration file의 내용은 환경 변수 설정값보다 우선한다. (즉, 환경 변수는 configuration file이 설정되지 않은 경우에만 적용된다.)

glsnr의 환경 파일은 $GOLDILOCKS_DATA/conf/goldilocks.listener.conf 파일이다. glsnr의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 환경 변수를 설정한 후에 glsnr을 구동한다.

glsnr이 실행되고 있는 상태에서 glsnr의 환경을 바꾸어 적용하려면 glsnr를 stop 시킨 후에 configuration 파일의 내용을 수정하거나 환경 변수를 설정한 후에 다시 start 한다.

glsnr을 stop하면 이미 연결이 완료된 client에는 문제가 없고 새로 연결을 시도하는 client만 실패한다.

<a id="9510f56dedb18ff7"></a>
### LISTEN_PORT

glsnr이 연결을 기다리는 port이다.

<a id="96f78c730fe7f9ac"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LISTEN_PORT |
| 설명 | glsnr이 연결을 기다리는 port이다. |
| Data type | INT |
| 기본값 및 범위 | 22581 / 1024 ~ 49151 |

<a id="2bf2e2d6ef688d4e"></a>
#### 설명

TCP 연결을 원하는 client들은 여기에 지정된 port로 접속을 시도해야 한다.  
Port는 1024부터 49151까지 사용할 수 있다.

<a id="a0797b5226428d19"></a>
### TCP_HOST

glsnr이 연결을 기다리는 NIC의 IP address이다.

<a id="62f8d446207e80c0"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TCP_HOST |
| 설명 | glsnr이 bind 하는 IP address이다. |
| Data type | ip address |
| 기본값 | 0.0.0.0 |

<a id="aa96ad4bc196bc8c"></a>
#### 설명

TCP 연결을 원하는 client들은 여기에 지정된 IP address로 접속을 시도해야 한다. IP address는 IPv4 또는 IPv6 형식을 사용한다.

<a id="21d7223abf86e7b9"></a>
### BACKLOG

Client가 동시에 접속할 경우 glsnr이 동시에 처리할 수 있는 client의 개수이다.

<a id="1e4ab89f6556ca94"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BACKLOG |
| 설명 | glsnr이 연결을 기다릴 수 있는 client의 개수이다. |
| Data type | INT |
| 기본값 및 범위 | 1024 / 1 ~ 32768 |

<a id="008f2a4799720c17"></a>
#### 설명

이 설정값이 client의 동시 접속자 수를 보장해주지는 않는다.

<a id="5466a007d323f6bf"></a>
### DEFAULT_CS_MODE

Client에서 접속 모드를 dedicated나 shared로 선택하지 않았을 경우, 접속 모드를 설정한다.

<a id="50e6349a029c33c4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_CS_MODE |
| 설명 | Default 접속 모드를 설정한다. |
| Data type | String ( dedicated \| shared ) |
| 기본값 | dedicated |

<a id="a97c6a877b1568f2"></a>
#### 설명

- glsnr을 통해 접속하는 Client/ Server (C/S) 모델은 dedicated와 shared라는 두 가지 모드를 지원한다.
- 기본적으로 client 단계에서 dedicated나 shared를 (odbc의 경우는 .odbcini) 선택하여 접속하지만 client에서 설정이 안된 경우에는 DEFAULT_CS_MODE 설정에 따라 접속모드가 결정된다.

<a id="3add93e77acb9d25"></a>
### TCP_VALIDNODE_CHECKING

접속을 시도한 client의 유효성 검증 여부를 설정한다.

<a id="d9cd8259df5ef38f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TCP_VALIDNODE_CHECKING |
| 설명 | Client 유효성 검증 여부를 설정한다. |
| Data type | String ( NO \| INVITED \| EXCLUDED ) |
| 기본값 | NO |

<a id="5682f5b37d41a3bf"></a>
#### 설명

- 이 값이 NO로 설정되면 client를 검증하지 않는다.
- 이 값이 INVITED로 설정되고 TCP_INVITED_FILE에 설정된 파일이 존재하면 TCP_INVITED_FILE에 설정된 파일의 ip address를 가진 client만 유효한 사용자로 설정된다.
- 이 값이 EXCLUDED로 설정되고 TCP_EXCLUDED_FILE에 설정된 파일이 존재하면 TCP_EXCLUDED_FILE에 설정된 파일의 ip address를 가진 client를 제외한 나머지 client들만 유효한 사용자로 설정된다.

<a id="0b2da6dc3ea130c1"></a>
### TCP_INVITED_FILE

TCP_VALIDNODE_CHECKING값이 INVITED인 경우에만 사용된다.

<a id="7520289e24ea7dc5"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TCP_INVITED_FILE |
| 설명 | 유효한 사용자 (IP address) list가 있는 파일이다. |
| Data type | String |
| 기본값 | 'goldilocks.invited.conf' |

<a id="52ef0559c97f33ff"></a>
#### 설명

여기에 설정된 파일이 존재할 경우, 파일에 포함된 사용자 (IP address)만 접속할 수 있다.

<a id="0c0e0906d492b650"></a>
### TCP_EXCLUDED_FILE

TCP_VALIDNODE_CHECKING 값이 EXCLUDED인 경우에만 사용된다.

<a id="7b461233088d8203"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TCP_EXCLUDED_FILE |
| 설명 | 유효하지 않은 사용자 (IP address) list가 있는 파일이다. |
| Data type | String |
| 기본값 | 'goldilocks.excluded.conf' |

<a id="9393109944f4c79f"></a>
#### 설명

여기에 설정된 파일이 존재할 경우, 파일에 포함된 사용자 (IP address)를 제외한 모든 사용자가 접속할 수 있다.

<a id="249b991290524403"></a>
### TIMEOUT

glsnr의 timeout 값이며 단위는 초 (second)이다

<a id="4d530148404c78da"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TIMEOUT |
| 설명 | glsnr의 timeout 이다. |
| Data type | INT |
| 기본값 / 범위 | 100 / ( 0 ~ 2147483647 ) |

<a id="327c93278d20221f"></a>
#### 설명

glsnr에서 client와 통신할 때 client로부터 응답이 없거나 반응이 느린 경우 timeout에 의해 접속이 해제된다.

<a id="13eb64a0ab02beab"></a>
### LISTENER_LOG_DIR

glsnr에서 출력되는 log가 저장되는 디렉토리를 설정한다.

<a id="6955721e6296cd72"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LISTENER_LOG_DIR |
| 설명 | glsnr의 log가 저장되는 디렉토리를 설정한다. |
| Data type | String |
| 기본값 | '&lt;GOLDILOCKS_DATA&gt;/trc' |

<a id="6a9dbc5da0bf9c95"></a>
#### 설명

설정값의 &lt;GOLDILOCKS_DATA&gt;는 환경 변수 $GOLDILOCKS_DATA의 값으로 대체된다.

<a id="20f0c7a1a02a1e7b"></a>
### UDS_DIR

glsnr에서 사용되는 Unix Domain Socket 파일이 저장되는 디렉토리를 설정한다

<a id="e7a6d24d011f7339"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | UDS_DIR |
| 설명 | glsnr에서 사용되는 Unix Domain Socket 파일이 저장되는 디렉토리를 설정한다. |
| Data type | String |
| 기본값 / 범위 | '/tmp' / 최대 60 byte |

<a id="fdc4d406de65747f"></a>
#### 설명

디렉토리의 최대 길이는 60 byte 이내로 설정해야 한다. Unix Domain Socket 파일의 절대 path (디렉토리 + 파일 이름)의 최대 크기는 OS마다 다르지만 보통 100 byte 내외이다. )

---

[← 37. gcreatedb](37-gcreatedb.md) · [전체 목차](../README.md) · [39. gsql/gsqlnet (Interactive SQL Tool) →](39-gsql-gsqlnet-interactive-sql-tool.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
