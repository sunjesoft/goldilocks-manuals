<a id="2d3664800a88193b"></a>

# 32. glsnr

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/2d3664800a88193b)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 31. gcreatedb](31-gcreatedb.md) · [전체 목차](../README.md) · [33. gsql/gsqlnet (Interactive SQL Tool) →](33-gsql-gsqlnet-interactive-sql-tool.md)

<a id="b5cef47a8474f2b9"></a>
## glsnr 소개

glsnr은 GOLDILOCKS가 client/ server 환경에서 network를 통해 원격으로 접속할 수 있게 해주는 listener이다. Network를 통해 GOLDILOCKS에 접속하려면 반드시 서버 쪽에 glsnr이 구동되어 있어야 한다.

glsnr은 다음과 같이 사용한다.

```
$ glsnr [options]
```

<a id="a27fe5bf45987806"></a>
## Command Option

glsnr을 사용하기 위한 셀 프롬프트 옵션은 다음과 같다.

<a id="3ace76488a101517"></a>
### --silent

<a id="679b82b66f7f388b"></a>
#### 설명

실행에 대한 message를 출력하지 않는다.

<a id="0534dadac0100cf3"></a>
#### 사용 예

```
$ glsnr --start --silent
```

<a id="63c2ba581012d0ab"></a>
### --start

<a id="92dc85ddfcbea1fe"></a>
#### 설명

glsnr을 구동한다. 만약 이미 구동중이었으면 에러가 발생한다.

<a id="eb9ef234673925d2"></a>
#### 사용 예

```
$ glsnr --start
Listener is started successfully.
```

<a id="815ab210632a64e3"></a>
### --stop

<a id="b7cce48976dffd62"></a>
#### 설명

현재 구동 중인 glsnr을 멈춘다.

<a id="c1d759a0921ed1a5"></a>
#### 사용 예

```
$ glsnr --stop
Listener is stopped.
```

<a id="10a69982cdc61741"></a>
### --status

<a id="65ace2fcd1e7fc84"></a>
#### 설명

glsnr의 상태 메시지를 출력한다.

<a id="7f02f454050a2540"></a>
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

<a id="09afc7f49865c92d"></a>
### --home

<a id="89aca67c187ac81c"></a>
#### 설명

db home을 설정한다.

<a id="b15c6eb79d1e7ecc"></a>
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

<a id="066a5012d1b3bbb9"></a>
### --help

<a id="1a4a59d1b94d6143"></a>
#### 설명

Help message를 출력한다.

<a id="43e677ee6681e35d"></a>
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

<a id="8cb47a809a2031c5"></a>
## Listener Configuration

<a id="7f7fe639c79b7c34"></a>
### Configuration File 및 환경 변수

glsnr은 configuration을 설정하기 위해 configuration file이나 환경 변수를 사용할 수 있다.

환경 변수를 설정하려면 configuration의 property name에 prefix로 'GOLDILOCKS_'를 추가한 name을 사용한다. 예를 들어 configuration file에 LISTEN_PORT를 설정하면 $GOLDILOCKS_LISTEN_PORT를 지정하는 것과 같은 효과가 있다.

Configuration file의 내용은 환경 변수 설정값보다 우선한다. (즉, 환경 변수는 configuration file이 설정되지 않은 경우에만 적용된다.)

glsnr의 환경 파일은 $GOLDILOCKS_DATA/conf/goldilocks.listener.conf 파일이다. glsnr의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 환경 변수를 설정한 후에 glsnr을 구동한다.

glsnr이 실행되고 있는 상태에서 glsnr의 환경을 바꾸어 적용하려면 glsnr을 stop 시킨 후에 configuration 파일의 내용을 수정하거나 환경 변수를 설정한 후에 다시 start 한다.

glsnr을 stop하면 이미 연결이 완료된 client에는 문제가 없고 새로 연결을 시도하는 client만 실패한다.

<a id="efd62539683af7db"></a>
### LISTEN_PORT

glsnr이 연결을 기다리는 port이다.

<a id="5614edb8d8e1470a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LISTEN_PORT |
| 설명 | glsnr이 연결을 기다리는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 22581 / 1024 ~ 49151 |

<a id="9f5e3998dcf498b4"></a>
#### 설명

TCP 연결을 원하는 client들은 여기에 지정된 port로 접속을 시도해야 한다.  
Port는 1024부터 49151까지 사용할 수 있다.

<a id="55b532faeac04d29"></a>
### TCP_HOST

glsnr이 연결을 기다리는 NIC의 IP address이다.

<a id="dc61cf7af333ee53"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TCP_HOST |
| 설명 | glsnr이 bind 하는 IP address이다. |
| Data type | ip address (ip v4) |
| 기본값 | 0.0.0.0 |

<a id="142dd84ac45e9c77"></a>
#### 설명

TCP 연결을 원하는 client들은 여기에 지정된 IP address로 접속을 시도해야 한다. IP address는 ip v4 형식을 사용한다.

<a id="28e81264e5786acb"></a>
### BACKLOG

Client가 동시에 접속할 경우 glsnr이 동시에 처리할 수 있는 client의 개수이다.

<a id="be659e263fa4abb9"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BACKLOG |
| 설명 | glsnr이 연결을 기다릴 수 있는 client의 개수이다. |
| Data type | INT |
| 기본값 및 범위 | 1024 / 1 ~ 32768 |

<a id="7f868d1900fe53c9"></a>
#### 설명

이 설정값이 client의 동시 접속자 수를 보장해주지는 않는다.

<a id="8c0aad94a4fea1d7"></a>
### DEFAULT_CS_MODE

Client에서 접속 모드를 dedicated나 shared로 선택하지 않았을 경우, 접속 모드를 설정한다.

<a id="0787d51b7736da3c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_CS_MODE |
| 설명 | Default 접속 모드를 설정한다. |
| Data type | String ( dedicated \| shared ) |
| 기본값 | dedicated |

<a id="e744d6ab93d00abe"></a>
#### 설명

- glsnr을 통해 접속하는 Client/ Server (C/S) 모델은 dedicated와 shared라는 두 가지 모드를 지원한다.
- 기본적으로 client 단계에서 dedicated나 shared를 (odbc의 경우는 .odbcini) 선택하여 접속하지만 client에서 설정이 안된 경우에는 DEFAULT_CS_MODE 설정에 따라 접속모드가 결정된다.

<a id="9297944f9134e44f"></a>
### TCP_VALIDNODE_CHECKING

접속을 시도한 client의 유효성 검증 여부를 설정한다.

<a id="8fecbb02cced777d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TCP_VALIDNODE_CHECKING |
| 설명 | Client 유효성 검증 여부를 설정한다. |
| Data type | String ( NO \| INVITED \| EXCLUDED ) |
| 기본값 | NO |

<a id="e7c5648ea476b115"></a>
#### 설명

- 이 값이 NO로 설정되면 client를 검증하지 않는다.
- 이 값이 INVITED로 설정되고 TCP_INVITED_FILE에 설정된 파일이 존재하면 TCP_INVITED_FILE에 설정된 파일의 ip address를 가진 client만 유효한 사용자로 설정된다.
- 이 값이 "EXCLUDED"로 설정되고 TCP_EXCLUDED_FILE에 설정된 파일이 존재하면 TCP_EXCLUDED_FILE에 설정된 파일의 ip address를 가진 client를 제외한 나머지 client들만 유효한 사용자로 설정된다.

<a id="5c0c975402d7b283"></a>
### TCP_INVITED_FILE

TCP_VALIDNODE_CHECKING 값이 INVITED인 경우에만 사용된다.

<a id="395d364378de47e2"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TCP_INVITED_FILE |
| 설명 | 유효한 사용자 (IP address) list가 있는 파일이다. |
| Data type | String |
| 기본값 | 'goldilocks.invited.conf' |

<a id="657f744fd7eded4b"></a>
#### 설명

여기에 설정된 파일이 존재할 경우, 파일에 포함된 사용자 (IP address)만 접속할 수 있다.

<a id="f31643df4447dd65"></a>
### TCP_EXCLUDED_FILE

TCP_VALIDNODE_CHECKING 값이 EXCLUDED인 경우에만 사용된다.

<a id="0aaee185cd231a8f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TCP_EXCLUDED_FILE |
| 설명 | 유효하지 않은 사용자 (IP address) list가 있는 파일이다. |
| Data type | String |
| 기본값 | 'goldilocks.excluded.conf' |

<a id="3e9c4d8f13ab56a2"></a>
#### 설명

여기에 설정된 파일이 존재할 경우, 파일에 포함된 사용자 (IP address)를 제외한 모든 사용자가 접속할 수 있다.

<a id="ac7e745cd63e1d9c"></a>
### TIMEOUT

glsnr의 timeout 값이며 단위는 초 (second)이다

<a id="58c8f431d11c2fe5"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TIMEOUT |
| 설명 | glsnr의 timeout 이다. |
| Data type | INT |
| 기본값/ 범위 | 100 / ( 0 ~ 2147483647 ) |

<a id="966806db73571f56"></a>
#### 설명

glsnr에서 client와 통신할 때 client로부터 응답이 없거나 반응이 느린 경우 timeout에 의해 접속이 해제된다.

<a id="69570fadbd46379f"></a>
### LISTENER_LOG_DIR

glsnr에서 출력되는 log가 저장되는 디렉토리를 설정한다.

<a id="e42fed8128fff997"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LISTENER_LOG_DIR |
| 설명 | glsnr의 log가 저장되는 디렉토리를 설정한다. |
| Data type | String |
| 기본값 | '&lt;GOLDILOCKS_DATA&gt;/trc' |

<a id="ed7d2746f96483bb"></a>
#### 설명

설정값의 &lt;GOLDILOCKS_DATA&gt;는 환경 변수 $GOLDILOCKS_DATA 값으로 대체된다.

<a id="3bf8cb9614d5c918"></a>
### UDS_DIR

glsnr에서 사용되는 Unix Domain Socket 파일이 저장되는 디렉토리를 설정한다

<a id="45bd10abea7b3e70"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | UDS_DIR |
| 설명 | glsnr에서 사용되는 Unix Domain Socket 파일이 저장되는 디렉토리를 설정한다. |
| Data type | String |
| 기본값/ 범위 | '/tmp' / 최대 60 byte |

<a id="39be4b6425561172"></a>
#### 설명

디렉토리의 최대 길이는 60 byte 이내로 설정해야 한다. Unix Domain Socket 파일의 절대 path (디렉토리 + 파일 이름)의 최대 크기는 OS마다 다르지만 보통 100 byte 내외이다.

---

[← 31. gcreatedb](31-gcreatedb.md) · [전체 목차](../README.md) · [33. gsql/gsqlnet (Interactive SQL Tool) →](33-gsql-gsqlnet-interactive-sql-tool.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
