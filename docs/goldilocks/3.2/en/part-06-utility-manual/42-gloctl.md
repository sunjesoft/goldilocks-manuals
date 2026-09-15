<a id="58c6a5230940f6f1"></a>

# 42. gloctl

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/58c6a5230940f6f1)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 41. gagent](41-gagent.md) · [Table of contents](../README.md) · [43. Overview →](../part-07-replication/43-overview.md)

<a id="387aabf9d82371e9"></a>
## Overview of gloctl

<a id="324a1c9f7e1ed876"></a>
### Definition

gloctl is an interactive utility provided by GOLDILOCKS, which provides location to [glocator](40-glocator.md#787a6a38e78fc2e9) and edits it.  
gloctl communicates with glocator by using User Datagram Protocol (UDP) communication protocol.

<a id="6c6667660bb38faa"></a>
### Usage

```
gloctl [options]
```

<a id="14306c6dbc3dbc26"></a>
### Options

<a id="fb5c44258174277b"></a>
#### help

<a id="9c7372dd9b31d69c"></a>
##### Description

It outputs the help message.

<a id="dd3915587fc1bf72"></a>
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

<a id="7d196d890c9896b1"></a>
#### conf

<a id="fcda55937f93dc3f"></a>
##### Description

It sets a [Configuration](#e8e424fcc3f5e607) file to communicate with glocator.    
If it is not set, $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf is used.

<a id="9d3b74ccdc51db0f"></a>
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

<a id="95d18bc86b72cbd8"></a>
#### ip

<a id="b32b4633f7df876c"></a>
##### Description

It sets IP address of glocator when starting gloctl. IP set value takes precedence when it is used together with DSN.

<a id="ee3a249a0bc6a2c5"></a>
##### Example

```
$ gloctl --ip 127.0.0.1

gLoctl>
```

The port of glocator in the example above is obtained by using DSN default LOCATOR in odbc.ini.

<a id="b9ea8c51733bb5d3"></a>
#### port

<a id="495bc1b60207dbc9"></a>
##### Description

It sets the port of glocator when starting gloctl. The port set value takes precedence when it is used together with DSN.

<a id="d56c39e3682eded9"></a>
##### Example

```
$ gloctl --port 42581

gLoctl>
```

IP of glocator in the example above is obtained by using DSN default LOCATOR in odbc.ini.

<a id="00622256e903b829"></a>
#### import

<a id="80b57a54621fa355"></a>
##### Description

It performs gloctl commands in batch within a file, not an interactive mode.

<a id="1b64bee8da755a3e"></a>
##### Example

```
$ gloctl --import import.txt

HELP                                                       
QUIT                                                       
IMPORT       {'FILE'}             Upload FILE to locations 
EXPORT       {'FILE'}             Download locations to FILE
ADD MEMBER   {DSN|{member_name {'host; port; db_home; agent_port;'}}} Add member location      
DROP MEMBER  {member_name}        Drop member location     
SET TIMEOUT  {second}             Set time for session timeout


Add member succeeded.
```

- The contents of import.txt above is as follows.

```
HELP
ADD MEMBER G1N3 'HOST=127.0.0.1;PORT=24581;DB_HOME=g1n3_home;AGENT_PORT= 44581;'
```

<a id="48a8998adf78eae1"></a>
#### silent

<a id="6e7d642b79964585"></a>
##### Description

It does not output the message of gloctl about the execution.

<a id="cb85a13aa4d1df51"></a>
##### Example

```
$ gloctl --silent --import import.txt
```

<a id="dce94bd2e6bc5e1c"></a>
#### no-copyright

<a id="5baa632f2c06c263"></a>
##### Description

It does not output the message of gloctl's copyright and version about the execution.

<a id="234080cae27b0220"></a>
##### Example

```
$ gloctl --no-copyright

gLoctl>
```

<a id="7f8a64cd9a67c5fa"></a>
## Interactive Command References

<a id="45f9caab3408d49b"></a>
### ADD MEMBER

<a id="8bfa8fa6cf913b66"></a>
#### Syntax

```
ADD MEMBER {DSN | member_name {'host; port; db_home; agent_port;'}}
```

<a id="1d423d0787ebf17c"></a>
#### Description

It adds a member to glocator. DSN existing in odbc.ini, a member name, and the required location information should be input.


> 
> - The port is that of glsnr.
> - ADD MEMBER is used to update the information of an existing member. In this case, if the member is in the process of the failover, then the update fails.
> 

<a id="1913148ceda02c86"></a>
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
AGENT_PORT=43581
LOCATOR_DSN=LOCATOR
```

- Describe the location of a member, and add it.

```
gLoctl> ADD MEMBER G1N2 'HOST=127.0.0.1; PORT=20201; DB_HOME=g1n2_home; AGENT_PORT= 43581'

Add member succeeded.

gLoctl>
```

<a id="e32d6c47e356b225"></a>
### ADD SERVICE

<a id="c132ec2d9698928d"></a>
#### Syntax

```
ADD SERVICE service_name {'member_name; ... '}
```

<a id="b9367f258639658c"></a>
#### Description

It adds a service to glocator. The node belonging to the service should be managed in [glocator](40-glocator.md#806ed1d0a43526e5), and it is ignored when the same node does not exist in glocator.

<a id="bae47d57e27cfacb"></a>
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

> When describing glocator properties in [odbcinst.ini file](../part-05-developer-manual/25-odbc.md#94ffe1b916f26010) and using [glocator](40-glocator.md#787a6a38e78fc2e9), then gsqlnet and other applications can access one of a server from the service list.

<a id="c2171487ab63a47f"></a>
### DROP MEMBER

<a id="d5df228566f527f6"></a>
#### Syntax

```
DROP MEMBER member_name
```

<a id="f1d1e4eb7f1dcf3e"></a>
#### Description

It drops a member corresponding to member_name from glocator.

> If a member is in the process of the failover, then the member can not be dropped.

<a id="6ba9f16b4ee3268a"></a>
#### Example

```
gLoctl> DROP MEMBER G1N2

Drop member succeeded.

gLoctl>
```

<a id="e171381f30d2908f"></a>
### DROP SERVICE

<a id="99275233b8a109b6"></a>
#### Syntax

```
DROP MEMBER service_name
```

<a id="2681c7d545d97bf5"></a>
#### Description

It drops a service corresponding to service_name from glocator.

<a id="939965988bef58bb"></a>
#### Example

```
gLoctl> DROP SERVICE S1

Drop service succeeded.

gLoctl>
```

<a id="787f8003390e3695"></a>
### EXPORT

<a id="0d01b671385ad8d3"></a>
#### Syntax

```
EXPORT {'FILE'}
```

<a id="56c5a16da5b3dc37"></a>
#### Description

It receives the location information from glocator and stores it in a file.

<a id="d89592cfd727d383"></a>
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
AGENT_PORT = 0
HOST = 127.0.0.1
DB_HOME = g1n1_home

[G1N3]
PORT = 24581
AGENT_PORT = 44581
HOST = 127.0.0.1
DB_HOME = g1n3_home
```

<a id="6a7c84acb8abc20b"></a>
### HELP

<a id="db460916e95ec575"></a>
#### Syntax

```
HELP
```

<a id="e88ead9d94af800c"></a>
#### Description

It displays the commands list in an interactive mode of gloctl.

<a id="f92f763f52861ad9"></a>
#### Example

```
gLoctl> HELP

HELP
QUIT
IMPORT {'FILE'} Upload FILE to locations
EXPORT {'FILE'} Download locations to FILE
ADD MEMBER {DSN|{member_name {'host; port; db_home; agent_port;'}}} Add member location
DROP MEMBER {member_name} Drop member location
SET TIMEOUT {second} Set time for session timeout
ADD SERVICE  {service_name {'member_name; ... '} } Add service
DROP SERVICE {service_name}       Drop service 

gLoctl>
```

<a id="5ba6657b393032bd"></a>
### IMPORT

<a id="631463392c5071b0"></a>
#### Syntax

```
IMPORT {'FILE'}
```

<a id="f12cc39485c42ba1"></a>
#### Description

It transfers the location to glocator by using a file in ini form.

<a id="1f1e77e24453bbe1"></a>
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
AGENT_PORT = 0
HOST = 127.0.0.1
DB_HOME = g1n1_home

[G1N3]
PORT = 24581
AGENT_PORT = 44581
HOST = 127.0.0.1
DB_HOME = g1n3_home
```

<a id="7fdb192c1741cb7a"></a>
### QUIT

<a id="cb603a22ab543382"></a>
#### Description

It quits gloctl.

<a id="642fd5491e4b5526"></a>
#### Syntax

```
QUIT
```

<a id="ad6a1d4e9a23aca8"></a>
### SET TIMEOUT

<a id="9aa3c811db1f0b06"></a>
#### Description

It sets TIMEOUT of glocator.

<a id="a93378cb716144f6"></a>
#### Syntax

```
SET TIMEOUT {second}
```

<a id="081bf8c0d430aed9"></a>
#### Example

```
gLoctl> set timeout 120

Set timeout.

gLoctl>
```

<a id="533f3f1f47ce5bf5"></a>
## Location File

Location file uploads or downloads the location information of a node from gloctl to glocator.

<a id="024bfe2fd3201cf2"></a>
### Description

Location file format is similar to that of [Data Source Specification](../part-05-developer-manual/25-odbc.md#7447ef8729f3aeac) file.

```
[node_name]
HOST = host_address
PORT = port_no
DB_HOME = db_home_path
AGENT_PORT = agent_port_no 

[SERVICE]
service_name = node_name {, node_name}*
```

Location keywords of Location file are as follows.

**Location infornation**

<a id="c0979ca798b7cb11"></a>
| Keyword | Description |
| --- | --- |
| node_name | It is the name of a node. |
| HOST | It is the IP address of a node. |
| PORT | It is the port number of glsnr which was executed in a node. |
| DB_HOME | It sets the home directory of a node. |
| AGENT_PORT | It is the port number of gagent which was executed in a node. |

[SERVICE] is a fixed keyword which lists the service hints. Service hints which are registered or to be registered in glocator are listed below SERVICE keyword.

HOST and PORT keywords should be input, and an error occurs if they are omitted.

The following is an example of configuring a location file.

```
[G1N1]
HOST = 192.168.0.101
PORT = 20101
DB_HOME = g1n1_home
AGENT_PORT = 40101

[G1N2]
HOST = 192.168.0.102
PORT = 20102
DB_HOME = g1n2_home
AGENT_PORT = 40102

[G2N1]
HOST = 192.168.0.201
PORT = 20201
DB_HOME = g2n1_home
AGENT_PORT = 40201

[G1N2]
HOST = 192.168.0.202
PORT = 20202
DB_HOME = g2n1_home
AGENT_PORT = 40202


[SERVICE]
service_1 = G1N1,G2N1
service_2 = G1N1,G1N2
```

<a id="e8e424fcc3f5e607"></a>
## Configuration

The environment file of gloctl is $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf. The environment file should be altered or the environment file should be set with [conf](#7d196d890c9896b1) option and restart gloctl, to alter the driving environment for gloctl.

Stop gloctl and alter the driving environment, then restart it to alter the environment of gloctl and to apply it, while gloctl is being executed.

<a id="4d3d9e587066f98d"></a>
### PORT

<a id="6ca1418c7624abbe"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is a port which is used by gloctl. |
| Data type | INT |
| Default value/ range | 44581 / 1024 ~ 49151 |

It sets the port of a socket which is used by gloctl.

<a id="461b7f3aa37a9590"></a>
### LOCATOR_HOST

<a id="e24490ea3612b76d"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is the host address of glocator with which gloctl communicates. |
| Data type | STRING |
| Default value/ range | 127.0.0.1 |

It sets the host address of glocator.

<a id="7ecc992d37652e19"></a>
### LOCATOR_PORT

<a id="ebfb61d6bd716983"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is the port of glocator with which gloctl communicates. |
| Data type | INT |
| Default value/ range | 42581 / 1024 ~ 49151 |

It sets the port of glocator.

<a id="429ea7bcfbfe50f8"></a>
### MESSAGE_TIMEOUT

<a id="d523eea288edab2f"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_TIMEOUT |
| Description | It sets the time of which gloctl waits for the response from glocator. (second) |
| Data type | INT |
| Default value/ range | 10 / 0 ~ 2147483647 |

It sets the time of which gloctl waits for the response after transferring a packet to glocator.

---

[← 41. gagent](41-gagent.md) · [Table of contents](../README.md) · [43. Overview →](../part-07-replication/43-overview.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
