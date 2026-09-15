<a id="faa4c37d38851831"></a>

# 53. gloctl

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/faa4c37d38851831)  
> Tag: `26c.1_0_tag`

[← 52. gagent](52-gagent.md) · [Table of contents](../README.md) · [54. Overview →](../part-07-replication/54-overview.md)

<a id="1863208c2c2b4d41"></a>
## Overview of gloctl

<a id="e371e0a687426d64"></a>
### Definition

gloctl is an interactive utility provided by GOLDILOCKS, which provides location to [glocator](51-glocator.md#0e0291a55963f28e) and edits it.  
gloctl communicates with glocator by using User Datagram Protocol (UDP) communication protocol.

<a id="2792218f5f821b73"></a>
### Usage

```
gloctl [options]
```

<a id="c488ca05457c2308"></a>
### Options

<a id="3676f937e38ba1c5"></a>
#### help

<a id="7e0a989f5b8d3d83"></a>
##### Description

It outputs the help message.

<a id="0c1fbf53f310cbd4"></a>
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

<a id="8966da450cc1859d"></a>
#### conf

<a id="f4dca9727322afd3"></a>
##### Description

It sets a [Configuration](#b48cb0e835af3765) file to communicate with glocator.    
If it is not set, $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf is used.

<a id="03426419139db2f1"></a>
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

<a id="c5864732bb3b679d"></a>
#### ip

<a id="ba90e0c0e0006c81"></a>
##### Description

It sets IP address of glocator when starting gloctl. IP set value takes precedence when it is used together with DSN.

<a id="70b021685aa1fde9"></a>
##### Example

```
$ gloctl --ip 127.0.0.1

gLoctl>
```

The port of glocator in the example above is obtained by using DSN default LOCATOR in odbc.ini.

<a id="94eea1effc1efa9a"></a>
#### port

<a id="8b193d5e887a9657"></a>
##### Description

It sets the port of glocator when starting gloctl. The port set value takes precedence when it is used together with DSN.

<a id="f635b940f98d4372"></a>
##### Example

```
$ gloctl --port 42581

gLoctl>
```

IP of glocator in the example above is obtained by using DSN default LOCATOR in odbc.ini.

<a id="4a281e0aa8e11686"></a>
#### import

<a id="fe2a48ffb8a14350"></a>
##### Description

It performs gloctl commands in batch within a file, not an interactive mode.

<a id="75e6955000008569"></a>
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

<a id="0533db5e7648e196"></a>
#### silent

<a id="f40a08a9b721c1d1"></a>
##### Description

It does not output the message of gloctl about the execution.

<a id="323ebed80df81811"></a>
##### Example

```
$ gloctl --silent --import import.txt
```

<a id="e8359a689df4613e"></a>
#### no-copyright

<a id="6b773f6635d90b02"></a>
##### Description

It does not output the message of gloctl's copyright and version about the execution.

<a id="8e92024eaec33f28"></a>
##### Example

```
$ gloctl --no-copyright

gLoctl>
```

<a id="1919a00d4d269238"></a>
## Interactive Command References

<a id="a5484577354bc2d5"></a>
### ADD MEMBER

<a id="0e05e6cb278822f3"></a>
#### Syntax

```
ADD MEMBER {DSN | member_name {'host; port; db_home;'}}
```

<a id="2b353001b8cb84bf"></a>
#### Description

It adds a member to glocator. DSN existing in odbc.ini, a member name, and the required location information should be input.


> 
> - The port is that of glsnr.
> - ADD MEMBER is used to update the information of an existing member. In this case, if the member is in the process of the failover, then the update fails.
> 

<a id="4782c6fc4b579d74"></a>
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

<a id="29947c2efda1adec"></a>
### ADD SERVICE

<a id="b7af9555d7a963db"></a>
#### Syntax

```
ADD SERVICE service_name {'member_name; ... '}
```

<a id="03d44489068be56a"></a>
#### Description

It adds a service to glocator. The node belonging to the service should be managed in [glocator](51-glocator.md#9d0108928f78c3cd), and it is ignored when the same node does not exist in glocator.

<a id="de49d8f55af82bc2"></a>
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

> When describing glocator properties in [odbcinst.ini file](../part-05-developer-manual/34-odbc.md#4b5eb0db7a69a199) and using [glocator](51-glocator.md#0e0291a55963f28e), then gsqlnet and other applications can access one of a server from the service list.

<a id="94fab056803ffdca"></a>
### DROP MEMBER

<a id="1115b926464fe404"></a>
#### Syntax

```
DROP MEMBER member_name
```

<a id="53b7047c9f1b4d5a"></a>
#### Description

It drops a member corresponding to member_name from glocator.

> If a member is in the process of the failover, then the member can not be dropped.

<a id="76a50632a1aacfd9"></a>
#### Example

```
gLoctl> DROP MEMBER G1N2

Drop member succeeded.

gLoctl>
```

<a id="3153b6a9f86c0326"></a>
### DROP SERVICE

<a id="4007f7cb756aa2aa"></a>
#### Syntax

```
DROP MEMBER service_name
```

<a id="e6c6d51301a57674"></a>
#### Description

It drops a service corresponding to service_name from glocator.

<a id="79576e2570d67ded"></a>
#### Example

```
gLoctl> DROP SERVICE S1

Drop service succeeded.

gLoctl>
```

<a id="a84861a80dcad3ab"></a>
### EXPORT

<a id="7f3129147eec12b4"></a>
#### Syntax

```
EXPORT {'FILE'}
```

<a id="d4fda821cfdaf909"></a>
#### Description

It receives the location information from glocator and stores it in a file.

<a id="08fa0d6e4f8107df"></a>
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

<a id="6849c5c11e2b4f3d"></a>
### HELP

<a id="1659a64d2767c75f"></a>
#### Syntax

```
HELP
```

<a id="4147f317ecab839f"></a>
#### Description

It displays the commands list in an interactive mode of gloctl.

<a id="dc04e5ac8a3232a4"></a>
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

<a id="39a6a0f18d953e0c"></a>
### IMPORT

<a id="457ebe1ee1ab12f8"></a>
#### Syntax

```
IMPORT {'FILE'}
```

<a id="e4b2758736537da7"></a>
#### Description

It transfers the location to glocator by using a file in ini form.

<a id="f7b7ea1906dc36eb"></a>
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

<a id="d03100671b1ae6c4"></a>
### QUIT

<a id="81d6cd81403332d3"></a>
#### Description

It quits gloctl.

<a id="dfde19aada27f07f"></a>
#### Syntax

```
QUIT
```

<a id="11f8df8b5f4f0a61"></a>
### SET TIMEOUT

<a id="c5e0cb7960ffcd46"></a>
#### Description

It sets TIMEOUT of glocator.

<a id="71d9b8ff2cb05cea"></a>
#### Syntax

```
SET TIMEOUT {second}
```

<a id="be54f542f3c5ed90"></a>
#### Example

```
gLoctl> set timeout 120

Set timeout.

gLoctl>
```

<a id="45b9b26f5f0b0168"></a>
## Location File

Location file uploads or downloads the location information of a node from gloctl to glocator.

<a id="12356c65d8a391fc"></a>
### Description

Location file format is similar to that of [Data Source Specification](../part-05-developer-manual/34-odbc.md#01f24405dc0a240b) file.

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

<a id="3f38113552e48e14"></a>
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

<a id="b48cb0e835af3765"></a>
## Configuration

The environment file of gloctl is $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf. The environment file should be altered or the environment file should be set with [conf](#8966da450cc1859d) option and restart gloctl, to alter the driving environment for gloctl.

Stop gloctl and alter the driving environment, then restart it to alter the environment of gloctl and to apply it, while gloctl is being executed.

<a id="ef3b2ef042152477"></a>
### PORT

<a id="8b9d8948b6aa61db"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is a port which is used by gloctl. |
| Data type | INT |
| Default value/ range | 44581 / 1024 ~ 49151 |

It sets the port of a socket which is used by gloctl.

<a id="2e6e1e9c3ddae683"></a>
### LOCATOR_HOST

<a id="38356a0616224af6"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is the host address of glocator with which gloctl communicates. |
| Data type | STRING |
| Default value/ range | 127.0.0.1 |

It sets the host address of glocator.

<a id="d47e3e1fdd8a840c"></a>
### LOCATOR_PORT

<a id="3239278a5458f425"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is the port of glocator with which gloctl communicates. |
| Data type | INT |
| Default value/ range | 42581 / 1024 ~ 49151 |

It sets the port of glocator.

<a id="7211c75097ac1c06"></a>
### MESSAGE_TIMEOUT

<a id="d61e5e690e9a791e"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_TIMEOUT |
| Description | It sets the time of which gloctl waits for the response from glocator. (second) |
| Data type | INT |
| Default value/ range | 10 / 0 ~ 2147483647 |

It sets the time of which gloctl waits for the response after transferring a packet to glocator.

---

[← 52. gagent](52-gagent.md) · [Table of contents](../README.md) · [54. Overview →](../part-07-replication/54-overview.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
