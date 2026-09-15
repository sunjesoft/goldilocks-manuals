<a id="8776583f97fc3298"></a>

# 48. gloctl

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/8776583f97fc3298)  
> 태그: `21c.1_35_tag`

[← 47. gagent](47-gagent.md) · [전체 목차](../README.md) · [49. 개요 →](../part-07-replication/49-개요.md)

<a id="148d849384d14d15"></a>
## gloctl 소개

<a id="cd008a1359dab200"></a>
### 정의

gloctl은 GOLDILOCKS에서 제공하는 대화형 유틸리티로써 [glocator](46-glocator.md#6aa340ae6a2d0c28)에 location을 제공하고 편집한다.  
gloctl은 User Datagram Protocol (UDP) 통신 프로토콜을 사용하여 glocator와 통신한다.

<a id="f4bd27b09c05ba57"></a>
### 사용법

```
gloctl [options]
```

<a id="868d1fa0bbfafcbe"></a>
### Option

<a id="65fb48e6ecb4fd90"></a>
#### help

<a id="61b49b0c75e3bad1"></a>
##### 설명

Help 메시지를 출력한다.

<a id="0166d8cfd238c678"></a>
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

<a id="0d365eb9610ded2e"></a>
#### conf

<a id="5179347790a29f0c"></a>
##### 설명

glocator와 통신하기 위해 [Configuration](#d8dcb7002d6afa87) 설정 파일을 지정한다.  
지정하지 않을 경우, $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf가 사용된다.

<a id="76c5ffea199b966a"></a>
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

<a id="194cc8fcef7fd36c"></a>
#### ip

<a id="44a07e1fd768aba9"></a>
##### 설명

gloctl를 구동할 때 glocator의 IP address를 설정한다. DSN과 함께 사용될 때는 IP 설정값이 우선한다.

<a id="f6d30763bbc33165"></a>
##### 사용 예

```
$ gloctl --ip 127.0.0.1

gLoctl>
```

위의 예에서 glocator의 port는 odbc.ini에서 DSN 기본값 LOCATOR를 이용하여 얻는다.

<a id="8afcd0b5b8b61c85"></a>
#### port

<a id="3ce28aa1b12d9889"></a>
##### 설명

gloctl를 구동할 때 glocator의 port를 설정한다. DSN와 함께 사용될 때는 port 설정값이 우선한다.

<a id="efb4a6f92d65fd7c"></a>
##### 사용 예

```
$ gloctl --port 42581

gLoctl>
```

위의 예에서 glocator의 IP는 odbc.ini에서 DSN 기본값 LOCATOR를 이용하여 얻는다.

<a id="6741657e65448ef7"></a>
#### import

<a id="31bba997497eaa8d"></a>
##### 설명

대화형 모드가 아닌 파일 내의 gloctl 명령을 batch로 수행한다.

<a id="e2229ddef4065d8b"></a>
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

<a id="e2fc1b673415a1cb"></a>
#### silent

<a id="94cb1f33a5832d36"></a>
##### 설명

실행에 대한 gloctl의 메시지를 출력하지 않는다.

<a id="265354ad695c9279"></a>
##### 사용 예

```
$ gloctl --silent --import import.txt
```

<a id="ed133e4a9ff2f62f"></a>
#### no-copyright

<a id="d8bd313cb440f3c7"></a>
##### 설명

실행에 대한 gloctl의 copy right와 버전 메시지를 출력하지 않는다.

<a id="5e578d4bcae8e9b2"></a>
##### 사용 예

```
$ gloctl --no-copyright

gLoctl>
```

<a id="55cd455c51d764f2"></a>
## Interactive Command Reference

<a id="65785b04d9ace1d5"></a>
### ADD MEMBER

<a id="7bd4a21d7f3b9c35"></a>
#### 구문

```
ADD MEMBER {DSN | member_name {'host; port; db_home;'}}
```

<a id="fe68e70bf44a5a68"></a>
#### 설명

glocator에 member 하나를 추가한다. odbc.ini에 존재하는 DSN 또는 member name과 필요한 location 정보를 입력해야 한다.


> 
> - Port는 glsnr의 port이다.
> - ADD MEMBER는 기존 member의 정보를 갱신할 때 사용할 수 있다. 이 때 해당 member가 failover하는 중이라면 갱신에 실패한다.
> 

<a id="c48ebc10e331d3e2"></a>
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

<a id="ddf86e4664e92e55"></a>
### ADD SERVICE

<a id="903431764ca52181"></a>
#### 구문

```
ADD SERVICE service_name {'member_name; ... '}
```

<a id="98d70aeccb6ba9d3"></a>
#### 설명

glocator에 service 하나를 추가한다. Service에 속한 node는 [glocator](46-glocator.md#6aa340ae6a2d0c28)에서 관리되어야 하며 glocator에 동일한 node가 없으면 무시된다.

<a id="36fc6f2f28b125d6"></a>
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

> [odbc.ini 파일](../part-05-developer-manual/31-odbc.md#a8dbbc9962ac8d3d)에 glocator 속성을 기술하고 [glocator](46-glocator.md#6aa340ae6a2d0c28)를 사용하면 gsqlnet과 기타 응용 프로그램은 service 목록 중 하나의 서버에 접속할 수 있다.

<a id="672040dc1fd835c2"></a>
### DROP MEMBER

<a id="7a9eaa8c7dae0581"></a>
#### 구문

```
DROP MEMBER member_name
```

<a id="575ccf507c65b81f"></a>
#### 설명

member_name에 해당하는 member를 glocator에서 삭제한다.

> 삭제하려는 member가 failover 과정 중에 있다면 삭제할 수 없다.

<a id="b40d0d2456bf2d07"></a>
#### 사용 예

```
gLoctl> DROP MEMBER G1N2

Drop member succeeded.

gLoctl>
```

<a id="648027be26eacfc2"></a>
### DROP SERVICE

<a id="88765a8145bb61ee"></a>
#### 구문

```
DROP MEMBER service_name
```

<a id="914fc73ba78eeaa5"></a>
#### 설명

service_name에 해당하는 service를 glocator에서 삭제한다.

<a id="dca97bb0f9257099"></a>
#### 사용 예

```
gLoctl> DROP SERVICE S1

Drop service succeeded.

gLoctl>
```

<a id="296d6e95f4957b31"></a>
### EXPORT

<a id="984fcc1e3788f23e"></a>
#### 구문

```
EXPORT {'FILE'}
```

<a id="17989cddb0291ada"></a>
#### 설명

glocator로부터 location 정보를 받아 파일에 저장한다.

<a id="90ed9fda93e5ff37"></a>
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

<a id="10b6956602731838"></a>
### HELP

<a id="901a2edce6eeeb8e"></a>
#### 구문

```
HELP
```

<a id="bebe0609ad7e3edd"></a>
#### 설명

gloctl의 대화형 모드에서 명령어 목록을 보여준다.

<a id="6334b931e01ac075"></a>
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

<a id="58f010d440c6413a"></a>
### IMPORT

<a id="657f5774b63adc46"></a>
#### 구문

```
IMPORT {'FILE'}
```

<a id="8388e04548925884"></a>
#### 설명

ini 형식의 파일을 이용하여 glocator에 location을 전송한다.

<a id="92c47a0d1f776886"></a>
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

<a id="a757b59cddf71c3c"></a>
### QUIT

<a id="6732bd8d6d6cfe4b"></a>
#### 설명

gloctl을 종료한다.

<a id="3393df6d80429c15"></a>
#### 구문

```
QUIT
```

<a id="6a5ddf97da12dc00"></a>
### SET TIMEOUT

<a id="e1c9cf5aedaec52b"></a>
#### 설명

glocator의 TIMEOUT을 설정한다.

<a id="e73260e8466f849a"></a>
#### 구문

```
SET TIMEOUT {second}
```

<a id="3213dc886f06611f"></a>
#### 사용 예

```
gLoctl> set timeout 120

Set timeout.

gLoctl>
```

<a id="b90af0416b437fa1"></a>
## Location File

Location file은 gloctl에서 glocator로 노드의 location 정보를 업로드하거나 다운로드한다.

<a id="a3617cac430ad10d"></a>
### 설명

Location file 형식은 [데이터 원본 스펙](../part-05-developer-manual/31-odbc.md#966daee79e73f6aa) 파일의 형식과 유사하다.

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

<a id="e3221c5451e23514"></a>
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

<a id="d8dcb7002d6afa87"></a>
## Configuration

gloctl의 환경파일은 $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf이다. gloctl의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 [conf](#0d365eb9610ded2e) 옵션으로 환경 파일을 지정하여 gloctl을 구동하면 된다.

gloctl이 실행 중인 상태에서 gloctl의 환경을 변경하여 적용하려면 gloctl을 멈춘 후에 구동 환경을 변경 하고 다시 시작해야 한다.

<a id="69ee6e9b8d3904d4"></a>
### PORT

<a id="b6a5c337aa73afe3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl이 사용하는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 44581 / 1024 ~ 49151 |

gloctl이 사용하는 소켓의 port를 설정한다.

<a id="577bf6a9c033621e"></a>
### LOCATOR_HOST

<a id="952450b4fd8e1a2c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl과 통신하는 glocator의 host address이다. |
| Data type | STRING |
| 기본값/ 범위 | 127.0.0.1 |

glocator의 host address를 설정한다.

<a id="7fc82be6bcbca11e"></a>
### LOCATOR_PORT

<a id="ecb43ec3b39dfd9e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl과 통신하는 glocator의 port이다. |
| Data type | INT |
| 기본값/ 범위 | 42581 / 1024 ~ 49151 |

glocator의 port를 설정한다.

<a id="35791db8382f9775"></a>
### MESSAGE_TIMEOUT

<a id="a3fd09627776be51"></a>
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
