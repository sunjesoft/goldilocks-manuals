<a id="93f88cc11d2100c5"></a>

# 48. gloctl

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/93f88cc11d2100c5)  
> 태그: `22c.1_10_tag`

[← 47. gagent](47-gagent.md) · [전체 목차](../README.md) · [49. 개요 →](../part-07-replication/49-개요.md)

<a id="301d4039ce49a2c3"></a>
## gloctl 소개

<a id="7097b6f6aae5091d"></a>
### 정의

gloctl은 GOLDILOCKS에서 제공하는 대화형 유틸리티로써 [glocator](46-glocator.md#68298fc49624d83a)에 location을 제공하고 편집한다.  
gloctl은 User Datagram Protocol (UDP) 통신 프로토콜을 사용하여 glocator와 통신한다.

<a id="09b379e82c3593ca"></a>
### 사용법

```
gloctl [options]
```

<a id="8a2ee3a75bf5aca2"></a>
### Option

<a id="b6beae6d76a35049"></a>
#### help

<a id="cbb227de315c9f7f"></a>
##### 설명

Help 메시지를 출력한다.

<a id="c15d59146ed3b65b"></a>
##### 사용 예

```
$ gloctl --help

Usage:
 gloctl [options]

Options:

-c  --conf         User configure file
-i  --ip           Locator host ip
-p  --port         Locator port number
-o  --import       Import control FILE
-l  --silent       Suppress the display of result message and echoing commands
-r  --no-copyright Suppress display copy right and version
-h  --help         Print help message
```

<a id="bd3d04bf0c41a8e6"></a>
#### conf

<a id="94d4c83366e69fd7"></a>
##### 설명

glocator와 통신하기 위해 [Configuration](#7cddbe49fac5d9a8) 설정 파일을 지정한다.  
지정하지 않을 경우, $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf가 사용된다.

<a id="933839dc255fa305"></a>
##### 사용 예

```
$ gloctl --conf gloctl.conf

gLoctl>
```

- 위의 예에서 사용한 gloctl.conf 파일의 내용은 다음과 같다.

```
[GLOCTL]
# Port number (1024 ~ 49151)
PORT = 44581

# Locator address
LOCATOR_HOST = 127.0.0.1

# Locator port number (1024 ~ 49151)
LOCATOR_PORT = 42581

# Time out to receive message from glocator (second)
# second ( 0 ~ 2147483647 )
MESSAGE_TIMEOUT = 10
```

<a id="946fd257393f8007"></a>
#### ip

<a id="9882765184065817"></a>
##### 설명

gloctl를 구동할 때 glocator의 IP address를 설정한다. DSN과 함께 사용될 때는 IP 설정값이 우선한다.

<a id="5bdf4442f8e55118"></a>
##### 사용 예

```
$ gloctl --ip 127.0.0.1

gLoctl>
```

위의 예에서 glocator의 port는 odbc.ini에서 DSN 기본값 LOCATOR를 이용하여 얻는다.

<a id="49f5ec34cdeaf842"></a>
#### port

<a id="167af81cdaf3f507"></a>
##### 설명

gloctl를 구동할 때 glocator의 port를 설정한다. DSN와 함께 사용될 때는 port 설정값이 우선한다.

<a id="834fb97e4542dbba"></a>
##### 사용 예

```
$ gloctl --port 42581

gLoctl>
```

위의 예에서 glocator의 IP는 odbc.ini에서 DSN 기본값 LOCATOR를 이용하여 얻는다.

<a id="902423db5f74eb95"></a>
#### import

<a id="4d5674b4d358fd50"></a>
##### 설명

대화형 모드가 아닌 파일 내의 gloctl 명령을 batch로 수행한다.

<a id="ada1c04ba115607f"></a>
##### 사용 예

```
$ gloctl --import import.txt

HELP                                                       
QUIT                                                       
IMPORT       {'FILE'}             Upload FILE to locations 
EXPORT       {'FILE'}             Download locations to FILE
ADD MEMBER   {DSN|{member_name {'host; port; db_home;'}}} Add member location      
DROP MEMBER  {member_name}        Drop member location     
SET TIMEOUT  {second}             Set time for session timeout

Add member succeeded.
```

- 위의 예에서 사용한 import.txt의 내용은 다음과 같다.

```
HELP
ADD MEMBER G1N3 'HOST=127.0.0.1;PORT=24581;DB_HOME=g1n3_home;'
```

<a id="01b824547827f21b"></a>
#### silent

<a id="7c2855d98a7cebcd"></a>
##### 설명

실행에 대한 gloctl의 메시지를 출력하지 않는다.

<a id="58752b95560fcb26"></a>
##### 사용 예

```
$ gloctl --silent --import import.txt
```

<a id="647473c6f64e974f"></a>
#### no-copyright

<a id="6f4dee97741c2cdc"></a>
##### 설명

실행에 대한 gloctl의 copy right와 버전 메시지를 출력하지 않는다.

<a id="d6bcb0df5b8d1b29"></a>
##### 사용 예

```
$ gloctl --no-copyright

gLoctl>
```

<a id="9833c8bd798b3ca9"></a>
## Interactive Command Reference

<a id="15dfd98586c827f6"></a>
### ADD MEMBER

<a id="7d5e3aa9a39ec77b"></a>
#### 구문

```
ADD MEMBER {DSN | member_name {'host; port; db_home;'}}
```

<a id="dee5b0de9c18d7de"></a>
#### 설명

glocator에 member 하나를 추가한다. odbc.ini에 존재하는 DSN 또는 member name과 필요한 location 정보를 입력해야 한다.


> 
> - Port는 glsnr의 port이다.
> - ADD MEMBER는 기존 member의 정보를 갱신할 때 사용할 수 있다. 이 때 해당 member가 failover하는 중이라면 갱신에 실패한다.
> 

<a id="5d10c0aa63a8cf4e"></a>
#### 사용 예

odbc.ini의 DSN을 이용하여 ADD MEMBER를 수행한다.

```
gLoctl> ADD MEMBER G1N1

Add member succeeded.

gLoctl>
```

- 다음은 odbc.ini의 내용이다.

```
[G1N1]
HOST=127.0.0.1
PORT=20101
DB_HOME= g1n1_home
LOCATOR_DSN=LOCATOR
```

- Member의 location을 서술하여 추가한다.

```
gLoctl> ADD MEMBER G1N2 'HOST=127.0.0.1; PORT=20201; DB_HOME=g1n2_home;'

Add member succeeded.

gLoctl>
```

<a id="aa199b40ad865d19"></a>
### ADD SERVICE

<a id="d4f5c10ee3dad210"></a>
#### 구문

```
ADD SERVICE service_name {'member_name; ... '}
```

<a id="3c2d4da091b08318"></a>
#### 설명

glocator에 service 하나를 추가한다. Service에 속한 node는 [glocator](46-glocator.md#68298fc49624d83a)에서 관리되어야 하며 glocator에 동일한 node가 없으면 무시된다.

<a id="822cc0de8b3a0020"></a>
#### 사용 예

ADD SERVICE로 service s1을 추가한다.

```
gLoctl> ADD SERVICE S1 'G1N1;G1N2;G2N1'

Add service succeeded.

gLoctl>
```

- 다음은 odbc.ini의 내용이다.

```
[GOLDILOCKS]
HOST=127.0.0.1
PORT=22581
LOCATOR_DSN=LOCATOR
LOCATOR_SERVICE=S1
[LOCATOR]
HOST=127.0.0.1
PORT=42581
```

> [odbc.ini 파일](../part-05-developer-manual/31-odbc.md#6eb05a63d0c64f05)에 glocator 속성을 기술하고 [glocator](46-glocator.md#68298fc49624d83a)를 사용하면 gsqlnet과 기타 응용 프로그램은 service 목록 중 하나의 서버에 접속할 수 있다.

<a id="8d90f514a2720dd2"></a>
### DROP MEMBER

<a id="bdc0341e2966ab4d"></a>
#### 구문

```
DROP MEMBER member_name
```

<a id="e22adccc2132f10a"></a>
#### 설명

member_name에 해당하는 member를 glocator에서 삭제한다.

> 삭제하려는 member가 failover 과정 중에 있다면 삭제할 수 없다.

<a id="41e7d4fcd7735ffd"></a>
#### 사용 예

```
gLoctl> DROP MEMBER G1N2

Drop member succeeded.

gLoctl>
```

<a id="15b7de50df96c8e4"></a>
### DROP SERVICE

<a id="1e3e52880fecb3ce"></a>
#### 구문

```
DROP MEMBER service_name
```

<a id="1979579c59d4ded6"></a>
#### 설명

service_name에 해당하는 service를 glocator에서 삭제한다.

<a id="732e2d0c82cbfc06"></a>
#### 사용 예

```
gLoctl> DROP SERVICE S1

Drop service succeeded.

gLoctl>
```

<a id="92cedd4a57b373c8"></a>
### EXPORT

<a id="e8d8dcf54d9d0e8d"></a>
#### 구문

```
EXPORT {'FILE'}
```

<a id="3bab92caef7af233"></a>
#### 설명

glocator로부터 location 정보를 받아 파일에 저장한다.

<a id="571c48bd0a71ce69"></a>
#### 사용 예

Location.txt라는 파일에 location 정보를 다운로드 한다.

```
gLoctl> EXPORT 'Location.txt'

Export file succeeded.

gLoctl>
```

- 위 예의 Location.txt 파일 내용은 다음과 같다.

```
[G1N1]
PORT = 20101
HOST = 127.0.0.1
DB_HOME = g1n1_home

[G1N3]
PORT = 24581
HOST = 127.0.0.1
DB_HOME = g1n3_home
```

<a id="2df3d321d82d095d"></a>
### HELP

<a id="9f04d92cd6d222c9"></a>
#### 구문

```
HELP
```

<a id="fdeda7c7267cd681"></a>
#### 설명

gloctl의 대화형 모드에서 명령어 목록을 보여준다.

<a id="ababcc3b2ae1192b"></a>
#### 사용 예

```
gLoctl> HELP

HELP
QUIT
IMPORT {'FILE'} Upload FILE to locations
EXPORT {'FILE'} Download locations to FILE
ADD MEMBER {DSN|{member_name {'host; port; db_home;'}}} Add member location
DROP MEMBER {member_name} Drop member location
SET TIMEOUT {second} Set time for session timeout
ADD SERVICE  {service_name {'member_name; ... '} } Add service
DROP SERVICE {service_name}       Drop service 

gLoctl>
```

<a id="e2602233a32fe0de"></a>
### IMPORT

<a id="24d810a478f0c26a"></a>
#### 구문

```
IMPORT {'FILE'}
```

<a id="0078ed2d0e7bba14"></a>
#### 설명

ini 형식의 파일을 이용하여 glocator에 location을 전송한다.

<a id="6102e16de8480515"></a>
#### 사용 예

Location.txt 파일에 있는 내용을 glocator로 보낸다.

```
gLoctl> IMPORT 'Location.txt'

Import file succeeded.

gLoctl>
```

- 위 예의 Location.txt 파일 내용은 다음과 같다.

```
[G1N1]
PORT = 20101
HOST = 127.0.0.1
DB_HOME = g1n1_home

[G1N3]
PORT = 24581
HOST = 127.0.0.1
DB_HOME = g1n3_home
```

<a id="b7ec97954587dde5"></a>
### QUIT

<a id="de4fc336e51826ef"></a>
#### 설명

gloctl을 종료한다.

<a id="ff9b3f022fc235ec"></a>
#### 구문

```
QUIT
```

<a id="73f56e0275323570"></a>
### SET TIMEOUT

<a id="f20c577c96867b7d"></a>
#### 설명

glocator의 TIMEOUT을 설정한다.

<a id="451f5d1632178cb2"></a>
#### 구문

```
SET TIMEOUT {second}
```

<a id="6ad50282079c0a32"></a>
#### 사용 예

```
gLoctl> set timeout 120

Set timeout.

gLoctl>
```

<a id="5ba0729f4f76e0fd"></a>
## Location File

Location file은 gloctl에서 glocator로 노드의 location 정보를 업로드하거나 다운로드한다.

<a id="9006e830f870b831"></a>
### 설명

Location file 형식은 [데이터 원본 스펙](../part-05-developer-manual/31-odbc.md#69d48b50088e0ee1) 파일의 형식과 유사하다.

```
[node_name]
HOST = host_address
PORT = port_no
DB_HOME = db_home_path

[SERVICE]
service_name = node_name {, node_name}*
```

Location file의 location 키워드는 다음 표와 같다.

**Location infornation**

<a id="6bd0bc7011ac122c"></a>
| 키워드 | 설명 |
| --- | --- |
| node_name | 노드 이름이다. |
| HOST | 노드의 IP 주소이다. |
| PORT | 노드에서 실행된 glsnr의 port 번호이다. |
| DB_HOME | 노드의 홈 디렉토리를 설정한다. |

[SERVICE]는 서비스 힌트 목록을 나열하는 고정 키워드이다. glocator에 등록되어 있거나 등록할 서비스 힌트 목록은 SERVICE 키워드 아래에 나열된다.

HOST와 PORT 키워드는 반드시 입력되어야 하며 누락할 경우 에러가 발생한다.

다음은 location file을 구성하는 예이다.

```
[G1N1]
HOST = 192.168.0.101
PORT = 20101
DB_HOME = g1n1_home

[G1N2]
HOST = 192.168.0.102
PORT = 20102
DB_HOME = g1n2_home

[G2N1]
HOST = 192.168.0.201
PORT = 20201
DB_HOME = g2n1_home

[G2N2]
HOST = 192.168.0.202
PORT = 20202
DB_HOME = g2n2_home

[SERVICE]
service_1 = G1N1,G2N1
service_2 = G1N1,G1N2
```

<a id="7cddbe49fac5d9a8"></a>
## Configuration

gloctl의 환경파일은 $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf이다. gloctl의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 [conf](#bd3d04bf0c41a8e6) 옵션으로 환경 파일을 지정하여 gloctl을 구동하면 된다.

gloctl이 실행 중인 상태에서 gloctl의 환경을 변경하여 적용하려면 gloctl을 멈춘 후에 구동 환경을 변경 하고 다시 시작해야 한다.

<a id="a7c39c7adb7c9514"></a>
### PORT

<a id="8ab377ef04b82956"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl이 사용하는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 44581 / 1024 ~ 49151 |

gloctl이 사용하는 소켓의 port를 설정한다.

<a id="efc920294cf29bf3"></a>
### LOCATOR_HOST

<a id="e485aa0a8ed263df"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl과 통신하는 glocator의 host address이다. |
| Data type | STRING |
| 기본값/ 범위 | 127.0.0.1 |

glocator의 host address를 설정한다.

<a id="53a564d06133d913"></a>
### LOCATOR_PORT

<a id="e7e79b166ea9e954"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl과 통신하는 glocator의 port이다. |
| Data type | INT |
| 기본값/ 범위 | 42581 / 1024 ~ 49151 |

glocator의 port를 설정한다.

<a id="89d1aa2106f4a541"></a>
### MESSAGE_TIMEOUT

<a id="f9c10a2af7ebdb59"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MESSAGE_TIMEOUT |
| 설명 | gloctl이 glocator로부터 응답을 기다리는 시간을 설정한다. (second) |
| Data type | INT |
| 기본값/ 범위 | 10 / 0 ~ 2147483647 |

gloctl이 glocator로 패킷을 보낸 후에 응답을 기다리는 시간을 설정한다.

---

[← 47. gagent](47-gagent.md) · [전체 목차](../README.md) · [49. 개요 →](../part-07-replication/49-개요.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
