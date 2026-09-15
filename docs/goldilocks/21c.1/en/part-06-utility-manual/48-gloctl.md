<a id="a4f051a64cd67b11"></a>

# 48. gloctl

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/a4f051a64cd67b11)  
> Tag: `21c.1_35_tag`

[← 47. gagent](47-gagent.md) · [Table of contents](../README.md) · [49. Overview →](../part-07-replication/49-overview.md)

<a id="0008ba79a41d8f50"></a>
## Overview of gloctl

<a id="5a2321f033d0f2a6"></a>
### Definition

gloctl is an interactive utility provided by GOLDILOCKS, which provides location to [glocator](46-glocator.md#be082a202d51c996) and edits it.  
gloctl communicates with glocator by using User Datagram Protocol (UDP) communication protocol.

<a id="d341eaf775c21cc5"></a>
### Usage

```
gloctl [options]
```

<a id="dda35b641653abb3"></a>
### Options

<a id="4c50bed4cf6c84c7"></a>
#### help

<a id="46b79e41f92bb7b6"></a>
##### Description

It outputs the help message.

<a id="024c4ba12977964b"></a>
##### Example

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

<a id="ca02dbba7c3c6100"></a>
#### conf

<a id="3c68cfa8ff90e66c"></a>
##### Description

It sets a [Configuration](#5c024f91d0f88cb4) file to communicate with glocator.    
If it is not set, $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf is used.

<a id="d3326d5341c2346f"></a>
##### Example

```
$ gloctl --conf gloctl.conf

gLoctl>
```

- The contents of gloctl.conf file above is as follows.

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

<a id="1835a55f96afa433"></a>
#### ip

<a id="2beefdf6ea38b3f9"></a>
##### Description

It sets IP address of glocator when starting gloctl. IP set value takes precedence when it is used together with DSN.

<a id="48c7e193b27edbc1"></a>
##### Example

```
$ gloctl --ip 127.0.0.1

gLoctl>
```

The port of glocator in the example above is obtained by using DSN default LOCATOR in odbc.ini.

<a id="b2aeeae2f34c2c8e"></a>
#### port

<a id="3d4e8b6754c15b5a"></a>
##### Description

It sets the port of glocator when starting gloctl. The port set value takes precedence when it is used together with DSN.

<a id="9b7ab744dd717ecf"></a>
##### Example

```
$ gloctl --port 42581

gLoctl>
```

IP of glocator in the example above is obtained by using DSN default LOCATOR in odbc.ini.

<a id="9a0357e6b4e6b170"></a>
#### import

<a id="fa94195461f67b7e"></a>
##### Description

It performs gloctl commands in batch within a file, not an interactive mode.

<a id="6044e38268c95345"></a>
##### Example

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

- The contents of import.txt above is as follows.

```
HELP
ADD MEMBER G1N3 'HOST=127.0.0.1;PORT=24581;DB_HOME=g1n3_home;'
```

<a id="acb7ac43029a31a2"></a>
#### silent

<a id="786a380813c6da26"></a>
##### Description

It does not output the message of gloctl about the execution.

<a id="9628fe9b2d0f2d7d"></a>
##### Example

```
$ gloctl --silent --import import.txt
```

<a id="60aa164ec82ac54e"></a>
#### no-copyright

<a id="c6be378970fe75a9"></a>
##### Description

It does not output the message of gloctl's copyright and version about the execution.

<a id="88c4f86c97609121"></a>
##### Example

```
$ gloctl --no-copyright

gLoctl>
```

<a id="863aca30a7a2b1b1"></a>
## Interactive Command References

<a id="cfd438cf4489caf5"></a>
### ADD MEMBER

<a id="70cb394d2f87e7ab"></a>
#### Syntax

```
ADD MEMBER {DSN | member_name {'host; port; db_home;'}}
```

<a id="c2eb2b30f1578c51"></a>
#### Description

It adds a member to glocator. DSN existing in odbc.ini, a member name, and the required location information should be input.


> 
> - The port is that of glsnr.
> - ADD MEMBER is used to update the information of an existing member. In this case, if the member is in the process of the failover, then the update fails.
> 

<a id="0e31854dc30ae732"></a>
#### Example

ADD MEMBER by using DSN of odbc.ini.

```
gLoctl> ADD MEMBER G1N1

Add member succeeded.

gLoctl>
```

- The contents of odbc.ini is as follows.

```
[G1N1]
HOST=127.0.0.1
PORT=20101
DB_HOME= g1n1_home
LOCATOR_DSN=LOCATOR
```

- Describe the location of a member, and add it.

```
gLoctl> ADD MEMBER G1N2 'HOST=127.0.0.1; PORT=20201; DB_HOME=g1n2_home;'

Add member succeeded.

gLoctl>
```

<a id="b991737097b80c38"></a>
### ADD SERVICE

<a id="2a6c99a2875988d1"></a>
#### Syntax

```
ADD SERVICE service_name {'member_name; ... '}
```

<a id="746e2f1f1757eb56"></a>
#### Description

It adds a service to glocator. The node belonging to the service should be managed in [glocator](46-glocator.md#5c6d9f818741f0f3), and it is ignored when the same node does not exist in glocator.

<a id="2025dfdfca1cfa93"></a>
#### Example

Add the service *s1* by using ADD SERVICE.

```
gLoctl> ADD SERVICE S1 'G1N1;G1N2;G2N1'

Add service succeeded.

gLoctl>
```

- The contents of odbc.ini is as follows.

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

> When describing glocator properties in [odbcinst.ini file](../part-05-developer-manual/31-odbc.md#72da8d36ac2819cb) and using [glocator](46-glocator.md#be082a202d51c996), then gsqlnet and other applications can access one of a server from the service list.

<a id="d426b4f74653ba7a"></a>
### DROP MEMBER

<a id="2fddcf63ae6f6ab9"></a>
#### Syntax

```
DROP MEMBER member_name
```

<a id="3a4a4bc16f160645"></a>
#### Description

It drops a member corresponding to member_name from glocator.

> If a member is in the process of the failover, then the member can not be dropped.

<a id="f88b7f2c953e9b9c"></a>
#### Example

```
gLoctl> DROP MEMBER G1N2

Drop member succeeded.

gLoctl>
```

<a id="a16937e531ee80f1"></a>
### DROP SERVICE

<a id="c63a5e5471b244f6"></a>
#### Syntax

```
DROP MEMBER service_name
```

<a id="91b676d2915a39d3"></a>
#### Description

It drops a service corresponding to service_name from glocator.

<a id="6195620a4ce9488c"></a>
#### Example

```
gLoctl> DROP SERVICE S1

Drop service succeeded.

gLoctl>
```

<a id="f9c481c12bd12ad1"></a>
### EXPORT

<a id="cbb3216a4cd57637"></a>
#### Syntax

```
EXPORT {'FILE'}
```

<a id="5a34c7710c4a0fe0"></a>
#### Description

It receives the location information from glocator and stores it in a file.

<a id="af6eaad0b5c0ec51"></a>
#### Example

Download the location information in Location.txt file.

```
gLoctl> EXPORT 'Location.txt'

Export file succeeded.

gLoctl>
```

- The contents of Location.txt above is as follows.

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

<a id="bd4b6bee3057ce80"></a>
### HELP

<a id="b0f0ac05a0db7cbb"></a>
#### Syntax

```
HELP
```

<a id="01b5d95c97eb4c3d"></a>
#### Description

It displays the commands list in an interactive mode of gloctl.

<a id="289ecc22df8e7026"></a>
#### Example

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

<a id="b3930e15af694305"></a>
### IMPORT

<a id="9861b6c8b4224e46"></a>
#### Syntax

```
IMPORT {'FILE'}
```

<a id="cb79def57b020e8d"></a>
#### Description

It transfers the location to glocator by using a file in ini form.

<a id="9f10625edb4d16d1"></a>
#### Example

It transfers the contents in Location.txt to glocator.

```
gLoctl> IMPORT 'Location.txt'

Import file succeeded.

gLoctl>
```

- The contents of Location.txt above is as follows.

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

<a id="c59f2ec75d5d1132"></a>
### QUIT

<a id="a7a9cc4904747543"></a>
#### Description

It quits gloctl.

<a id="18bc30cfa48b9c57"></a>
#### Syntax

```
QUIT
```

<a id="4ebfa9d4bc077cfe"></a>
### SET TIMEOUT

<a id="e7d240f82c23ed18"></a>
#### Description

It sets TIMEOUT of glocator.

<a id="22a7cee969b2060f"></a>
#### Syntax

```
SET TIMEOUT {second}
```

<a id="e7508985053e33b8"></a>
#### Example

```
gLoctl> set timeout 120

Set timeout.

gLoctl>
```

<a id="5a93eeebc4b5377a"></a>
## Location File

Location file uploads or downloads the location information of a node from gloctl to glocator.

<a id="256963c86a42aada"></a>
### Description

Location file format is similar to that of [Data Source Specification](../part-05-developer-manual/31-odbc.md#29f8ddb0cb57dea1) file.

```
[node_name]
HOST = host_address
PORT = port_no
DB_HOME = db_home_path

[SERVICE]
service_name = node_name {, node_name}*
```

Location keywords of Location file are as follows.

**Location infornation**

<a id="6a0c6d42589e8498"></a>
| Keyword | Description |
| --- | --- |
| node_name | It is the name of a node. |
| HOST | It is the IP address of a node. |
| PORT | It is the port number of glsnr which was executed in a node. |
| DB_HOME | It sets the home directory of a node. |

[SERVICE] is a fixed keyword which lists the service hints. Service hints which are registered or to be registered in glocator are listed below SERVICE keyword.

HOST and PORT keywords should be input, and an error occurs if they are omitted.

The following is an example of configuring a location file.

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

<a id="5c024f91d0f88cb4"></a>
## Configuration

The environment file of gloctl is $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf. The environment file should be altered or the environment file should be set with [conf](#ca02dbba7c3c6100) option and restart gloctl, to alter the driving environment for gloctl.

Stop gloctl and alter the driving environment, then restart it to alter the environment of gloctl and to apply it, while gloctl is being executed.

<a id="9fd8f192d3007948"></a>
### PORT

<a id="01c21beb03f1ac5c"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is a port which is used by gloctl. |
| Data type | INT |
| Default value/ range | 44581 / 1024 ~ 49151 |

It sets the port of a socket which is used by gloctl.

<a id="96b568b5f3676f73"></a>
### LOCATOR_HOST

<a id="7245c66dad2d9e53"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is the host address of glocator with which gloctl communicates. |
| Data type | STRING |
| Default value/ range | 127.0.0.1 |

It sets the host address of glocator.

<a id="5cd8759c3ff76adf"></a>
### LOCATOR_PORT

<a id="8f3b0883f7c44f73"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is the port of glocator with which gloctl communicates. |
| Data type | INT |
| Default value/ range | 42581 / 1024 ~ 49151 |

It sets the port of glocator.

<a id="e93b1282422f83e2"></a>
### MESSAGE_TIMEOUT

<a id="5bd83b8b35be5eca"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_TIMEOUT |
| Description | It sets the time of which gloctl waits for the response from glocator. (second) |
| Data type | INT |
| Default value/ range | 10 / 0 ~ 2147483647 |

It sets the time of which gloctl waits for the response after transferring a packet to glocator.

---

[← 47. gagent](47-gagent.md) · [Table of contents](../README.md) · [49. Overview →](../part-07-replication/49-overview.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
