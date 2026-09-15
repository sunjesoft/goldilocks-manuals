<a id="7294e10acec21070"></a>

# 48. gloctl

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/7294e10acec21070)  
> Tag: `22c.1_10_tag`

[← 47. gagent](47-gagent.md) · [Table of contents](../README.md) · [49. Overview →](../part-07-replication/49-overview.md)

<a id="aea8168e0da011e1"></a>
## Overview of gloctl

<a id="ca4840fce89677ec"></a>
### Definition

gloctl is an interactive utility provided by GOLDILOCKS, which provides location to [glocator](46-glocator.md#4e23705d562834a7) and edits it.  
gloctl communicates with glocator by using User Datagram Protocol (UDP) communication protocol.

<a id="666427d6c664d37d"></a>
### Usage

```
gloctl [options]
```

<a id="c6a5d8bcd86c47ff"></a>
### Options

<a id="cd69c56a22c217fa"></a>
#### help

<a id="72b25ba0b28d1733"></a>
##### Description

It outputs the help message.

<a id="7973eb77b5464fe2"></a>
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

<a id="89da820492557a61"></a>
#### conf

<a id="144de9896464f6bd"></a>
##### Description

It sets a [Configuration](#9c975473961a849c) file to communicate with glocator.    
If it is not set, $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf is used.

<a id="f95e6436db9c6ea6"></a>
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

<a id="e52597d755ccf88e"></a>
#### ip

<a id="1c995a155d2362b8"></a>
##### Description

It sets IP address of glocator when starting gloctl. IP set value takes precedence when it is used together with DSN.

<a id="945692be38ba9b04"></a>
##### Example

```
$ gloctl --ip 127.0.0.1

gLoctl>
```

The port of glocator in the example above is obtained by using DSN default LOCATOR in odbc.ini.

<a id="cb302776183789b3"></a>
#### port

<a id="0a4b0e3436e66c80"></a>
##### Description

It sets the port of glocator when starting gloctl. The port set value takes precedence when it is used together with DSN.

<a id="033f1716ab863666"></a>
##### Example

```
$ gloctl --port 42581

gLoctl>
```

IP of glocator in the example above is obtained by using DSN default LOCATOR in odbc.ini.

<a id="6fc8dff0299cf03c"></a>
#### import

<a id="7fac96bf7637a661"></a>
##### Description

It performs gloctl commands in batch within a file, not an interactive mode.

<a id="5a279536bd589437"></a>
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

<a id="8609a6d4054bfc16"></a>
#### silent

<a id="e11fcbd882a439c8"></a>
##### Description

It does not output the message of gloctl about the execution.

<a id="58d4488e50af5e15"></a>
##### Example

```
$ gloctl --silent --import import.txt
```

<a id="993722f11ca07e3e"></a>
#### no-copyright

<a id="c56ccf537b9c85b7"></a>
##### Description

It does not output the message of gloctl's copyright and version about the execution.

<a id="7481c09f89f8b0ce"></a>
##### Example

```
$ gloctl --no-copyright

gLoctl>
```

<a id="51058486517feaca"></a>
## Interactive Command References

<a id="399a47ea0c9ce38f"></a>
### ADD MEMBER

<a id="50c029351c2b2c35"></a>
#### Syntax

```
ADD MEMBER {DSN | member_name {'host; port; db_home;'}}
```

<a id="dbbd7061df59570f"></a>
#### Description

It adds a member to glocator. DSN existing in odbc.ini, a member name, and the required location information should be input.


> 
> - The port is that of glsnr.
> - ADD MEMBER is used to update the information of an existing member. In this case, if the member is in the process of the failover, then the update fails.
> 

<a id="5c7914ae90fe9fdc"></a>
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

<a id="f5f6b4c2a89662ed"></a>
### ADD SERVICE

<a id="7e7f506b3a4aeefd"></a>
#### Syntax

```
ADD SERVICE service_name {'member_name; ... '}
```

<a id="6b52918759beeb5b"></a>
#### Description

It adds a service to glocator. The node belonging to the service should be managed in [glocator](46-glocator.md#450832b1e88fed4c), and it is ignored when the same node does not exist in glocator.

<a id="f3dedf3ec269f743"></a>
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

> When describing glocator properties in [odbcinst.ini file](../part-05-developer-manual/31-odbc.md#3b5d5e22e73ccd55) and using [glocator](46-glocator.md#4e23705d562834a7), then gsqlnet and other applications can access one of a server from the service list.

<a id="557c6ba888b81333"></a>
### DROP MEMBER

<a id="d061e7a5083ce0d8"></a>
#### Syntax

```
DROP MEMBER member_name
```

<a id="acfb621189f8a669"></a>
#### Description

It drops a member corresponding to member_name from glocator.

> If a member is in the process of the failover, then the member can not be dropped.

<a id="2221a318f5ef007a"></a>
#### Example

```
gLoctl> DROP MEMBER G1N2

Drop member succeeded.

gLoctl>
```

<a id="8527272a3af697c9"></a>
### DROP SERVICE

<a id="600e507a52437379"></a>
#### Syntax

```
DROP MEMBER service_name
```

<a id="b9e189fcf8b5301f"></a>
#### Description

It drops a service corresponding to service_name from glocator.

<a id="dfa80a2467047e91"></a>
#### Example

```
gLoctl> DROP SERVICE S1

Drop service succeeded.

gLoctl>
```

<a id="7751d55229894e25"></a>
### EXPORT

<a id="77b9e6edaae2b50a"></a>
#### Syntax

```
EXPORT {'FILE'}
```

<a id="8799e2bcb10f0baa"></a>
#### Description

It receives the location information from glocator and stores it in a file.

<a id="9deb8c4819f0e6ee"></a>
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

<a id="2cc5ba308d9e46a1"></a>
### HELP

<a id="5efa007ebeb36a28"></a>
#### Syntax

```
HELP
```

<a id="46ea80f43639b0b4"></a>
#### Description

It displays the commands list in an interactive mode of gloctl.

<a id="a905b0afc0b14da4"></a>
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

<a id="dceefadacb0d0ef5"></a>
### IMPORT

<a id="08f1ea17292aa5f7"></a>
#### Syntax

```
IMPORT {'FILE'}
```

<a id="962b5ba62d1f8c61"></a>
#### Description

It transfers the location to glocator by using a file in ini form.

<a id="5ee3c7dc334964fd"></a>
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

<a id="71d3fd37d92a71b9"></a>
### QUIT

<a id="a4c29d126cc72fae"></a>
#### Description

It quits gloctl.

<a id="efb0ee1ddab7d6d8"></a>
#### Syntax

```
QUIT
```

<a id="30b366e08de378ba"></a>
### SET TIMEOUT

<a id="3b30d85a9575645c"></a>
#### Description

It sets TIMEOUT of glocator.

<a id="a82b7c534ee9fa6b"></a>
#### Syntax

```
SET TIMEOUT {second}
```

<a id="35a43594ea870aee"></a>
#### Example

```
gLoctl> set timeout 120

Set timeout.

gLoctl>
```

<a id="5e07a8bdc4a14642"></a>
## Location File

Location file uploads or downloads the location information of a node from gloctl to glocator.

<a id="40690b5c4a6c2b3e"></a>
### Description

Location file format is similar to that of [Data Source Specification](../part-05-developer-manual/31-odbc.md#eac29c4c236beb90) file.

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

<a id="1ba0c4459421a907"></a>
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

<a id="9c975473961a849c"></a>
## Configuration

The environment file of gloctl is $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf. The environment file should be altered or the environment file should be set with [conf](#89da820492557a61) option and restart gloctl, to alter the driving environment for gloctl.

Stop gloctl and alter the driving environment, then restart it to alter the environment of gloctl and to apply it, while gloctl is being executed.

<a id="bb61514ec7329a7b"></a>
### PORT

<a id="21d9f15f949f2443"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is a port which is used by gloctl. |
| Data type | INT |
| Default value/ range | 44581 / 1024 ~ 49151 |

It sets the port of a socket which is used by gloctl.

<a id="a2db5e9aecbbaa80"></a>
### LOCATOR_HOST

<a id="093923d1c89270c4"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is the host address of glocator with which gloctl communicates. |
| Data type | STRING |
| Default value/ range | 127.0.0.1 |

It sets the host address of glocator.

<a id="e8f4084d093533b9"></a>
### LOCATOR_PORT

<a id="789216c8e7e61104"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is the port of glocator with which gloctl communicates. |
| Data type | INT |
| Default value/ range | 42581 / 1024 ~ 49151 |

It sets the port of glocator.

<a id="1b93759c21a78ae0"></a>
### MESSAGE_TIMEOUT

<a id="fb492d7862816954"></a>
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
