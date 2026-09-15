<a id="92eddab9e67d5932"></a>

# 46. gloctl

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/92eddab9e67d5932)  
> Tag: `20c.1_30_tag`

[← 45. gagent](45-gagent.md) · [Table of contents](../README.md) · [47. Overview →](../part-07-replication/47-overview.md)

<a id="6ef1a3b18eb0a6a0"></a>
## Overview of gloctl

<a id="b803e9b02371fbb2"></a>
### Definition

gloctl is an interactive utility provided by GOLDILOCKS, which provides location to [glocator](44-glocator.md#19ceb541c706922f) and edits it.  
gloctl communicates with glocator by using User Datagram Protocol (UDP) communication protocol.

<a id="49a49df78253aa11"></a>
### Usage

```
gloctl [options]
```

<a id="a59363ea0ea1c065"></a>
### Options

<a id="87d6796d6ba9cb6b"></a>
#### help

<a id="19450b85bc7d8dbb"></a>
##### Description

It outputs the help message.

<a id="942607c5706ad9a4"></a>
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

<a id="887185063741c020"></a>
#### conf

<a id="e12f68f0c6b2829c"></a>
##### Description

It sets a [Configuration](#cd50be1c84584e74) file to communicate with glocator.    
If it is not set, $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf is used.

<a id="280155b2c933c7c7"></a>
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

<a id="b7980342b0548195"></a>
#### ip

<a id="07b9b7c7b70cce6c"></a>
##### Description

It sets IP address of glocator when starting gloctl. IP set value takes precedence when it is used together with DSN.

<a id="ab1cd0c877b7f323"></a>
##### Example

```
$ gloctl --ip 127.0.0.1

gLoctl>
```

The port of glocator in the example above is obtained by using DSN default LOCATOR in odbc.ini.

<a id="0f20e004faf20736"></a>
#### port

<a id="3a6d7b674f07da1e"></a>
##### Description

It sets the port of glocator when starting gloctl. The port set value takes precedence when it is used together with DSN.

<a id="61c64db62c2cc4e6"></a>
##### Example

```
$ gloctl --port 42581

gLoctl>
```

IP of glocator in the example above is obtained by using DSN default LOCATOR in odbc.ini.

<a id="b68b6b1ff294593a"></a>
#### import

<a id="45c24bfe4646d67e"></a>
##### Description

It performs gloctl commands in batch within a file, not an interactive mode.

<a id="9fb764fe553f6762"></a>
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

<a id="e7540529b12697b9"></a>
#### silent

<a id="445b7c0e4076defe"></a>
##### Description

It does not output the message of gloctl about the execution.

<a id="d883c33d8ddf18ac"></a>
##### Example

```
$ gloctl --silent --import import.txt
```

<a id="07d35f8928bbd9b6"></a>
#### no-copyright

<a id="45998db8fc6d9022"></a>
##### Description

It does not output the message of gloctl's copyright and version about the execution.

<a id="ebb24481fcbfacc6"></a>
##### Example

```
$ gloctl --no-copyright

gLoctl>
```

<a id="68fab59b2bf9b709"></a>
## Interactive Command References

<a id="7e56611c8d9dcb53"></a>
### ADD MEMBER

<a id="8e75b0d9cafb9132"></a>
#### Syntax

```
ADD MEMBER {DSN | member_name {'host; port; db_home;'}}
```

<a id="6f3fb61a13f9086e"></a>
#### Description

It adds a member to glocator. DSN existing in odbc.ini, a member name, and the required location information should be input.


> 
> - The port is that of glsnr.
> - ADD MEMBER is used to update the information of an existing member. In this case, if the member is in the process of the failover, then the update fails.
> 

<a id="640b764409ad5644"></a>
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

<a id="0655cfcf4fe7eb1c"></a>
### ADD SERVICE

<a id="89b7dbee73536e00"></a>
#### Syntax

```
ADD SERVICE service_name {'member_name; ... '}
```

<a id="4651d55c208db366"></a>
#### Description

It adds a service to glocator. The node belonging to the service should be managed in [glocator](44-glocator.md#b17e41b7469eb8b7), and it is ignored when the same node does not exist in glocator.

<a id="425a53ca3ddee369"></a>
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

> When describing glocator properties in [odbcinst.ini file](../part-05-developer-manual/29-odbc.md#c4c0d16e426df68a) and using [glocator](44-glocator.md#19ceb541c706922f), then gsqlnet and other applications can access one of a server from the service list.

<a id="15c439c52db9978c"></a>
### DROP MEMBER

<a id="e097637af10f9917"></a>
#### Syntax

```
DROP MEMBER member_name
```

<a id="c812002985bec52a"></a>
#### Description

It drops a member corresponding to member_name from glocator.

> If a member is in the process of the failover, then the member can not be dropped.

<a id="23ceb2336ac244e3"></a>
#### Example

```
gLoctl> DROP MEMBER G1N2

Drop member succeeded.

gLoctl>
```

<a id="4b453c4c2c3248b1"></a>
### DROP SERVICE

<a id="db0cde6b6514100c"></a>
#### Syntax

```
DROP MEMBER service_name
```

<a id="e4592e91f64059dd"></a>
#### Description

It drops a service corresponding to service_name from glocator.

<a id="87036b1c68b20a1c"></a>
#### Example

```
gLoctl> DROP SERVICE S1

Drop service succeeded.

gLoctl>
```

<a id="325d8e80daa25b15"></a>
### EXPORT

<a id="c7f5fced8b7aa45a"></a>
#### Syntax

```
EXPORT {'FILE'}
```

<a id="85221d96c3bef74f"></a>
#### Description

It receives the location information from glocator and stores it in a file.

<a id="6352b98728581b1e"></a>
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

<a id="db7cfeb5ce4eab06"></a>
### HELP

<a id="9d941b87e8a928fa"></a>
#### Syntax

```
HELP
```

<a id="8d02ed11687796bb"></a>
#### Description

It displays the commands list in an interactive mode of gloctl.

<a id="a9a6d2ac9fa9ee0e"></a>
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

<a id="5ce65add6b406d63"></a>
### IMPORT

<a id="98b8f25e45a01c72"></a>
#### Syntax

```
IMPORT {'FILE'}
```

<a id="e34fd8e4057898fc"></a>
#### Description

It transfers the location to glocator by using a file in ini form.

<a id="3fed02be6ee5a1bf"></a>
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

<a id="afc11967e2212599"></a>
### QUIT

<a id="2afd588bbc7b7c66"></a>
#### Description

It quits gloctl.

<a id="a3f7f118997deb19"></a>
#### Syntax

```
QUIT
```

<a id="a6101a1c72c2ff99"></a>
### SET TIMEOUT

<a id="2b7aa84b91e9544a"></a>
#### Description

It sets TIMEOUT of glocator.

<a id="7fb35655d983b608"></a>
#### Syntax

```
SET TIMEOUT {second}
```

<a id="7e72ae68e4330935"></a>
#### Example

```
gLoctl> set timeout 120

Set timeout.

gLoctl>
```

<a id="59bc19f489aff598"></a>
## Location File

Location file uploads or downloads the location information of a node from gloctl to glocator.

<a id="c675fe973a33521f"></a>
### Description

Location file format is similar to that of [Data Source Specification](../part-05-developer-manual/29-odbc.md#f3d30a22dc413739) file.

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

<a id="b15a7f2caf62f527"></a>
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

<a id="cd50be1c84584e74"></a>
## Configuration

The environment file of gloctl is $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf. The environment file should be altered or the environment file should be set with [conf](#887185063741c020) option and restart gloctl, to alter the driving environment for gloctl.

Stop gloctl and alter the driving environment, then restart it to alter the environment of gloctl and to apply it, while gloctl is being executed.

<a id="14c88f49cf647c28"></a>
### PORT

<a id="193d75619baf26f8"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is a port which is used by gloctl. |
| Data type | INT |
| Default value/ range | 44581 / 1024 ~ 49151 |

It sets the port of a socket which is used by gloctl.

<a id="7bc03eb1379e6076"></a>
### LOCATOR_HOST

<a id="f40a0942b61baee9"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is the host address of glocator with which gloctl communicates. |
| Data type | STRING |
| Default value/ range | 127.0.0.1 |

It sets the host address of glocator.

<a id="75f49f9d25ca77ed"></a>
### LOCATOR_PORT

<a id="7a80c3f9861cda60"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is the port of glocator with which gloctl communicates. |
| Data type | INT |
| Default value/ range | 42581 / 1024 ~ 49151 |

It sets the port of glocator.

<a id="5066665992126e29"></a>
### MESSAGE_TIMEOUT

<a id="8842798864cd708e"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_TIMEOUT |
| Description | It sets the time of which gloctl waits for the response from glocator. (second) |
| Data type | INT |
| Default value/ range | 10 / 0 ~ 2147483647 |

It sets the time of which gloctl waits for the response after transferring a packet to glocator.

---

[← 45. gagent](45-gagent.md) · [Table of contents](../README.md) · [47. Overview →](../part-07-replication/47-overview.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
