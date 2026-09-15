<a id="0fd87486f960aa01"></a>

# 36. glsnr

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/0fd87486f960aa01)  
> Tag: `20c.1_30_tag`

[← 35. gcreatedb](35-gcreatedb.md) · [Table of contents](../README.md) · [37. gsql/gsqlnet (Interactive SQL Tool) →](37-gsql-gsqlnet-interactive-sql-tool.md)

<a id="8fb28958c158693b"></a>
## Overview of glsnr

glsnr is a listener which GOLDILOCKS enables remote access through the network in the client/ server environment. glsnr should be run on the server for the network access to GOLDILOCKS.

glsnr is used as follows.

```
$ glsnr [options]
```

<a id="827451120790da11"></a>
## Command Options

The followings are cell prompt options for using glsnr.

<a id="815b95d82268cb6e"></a>
### --silent

<a id="9f40e6d9fb4c3e66"></a>
#### Description

It does not display the message for execution.

<a id="b48f043ec4a001ea"></a>
#### Example

```
$ glsnr --start --silent
```

<a id="99537212e52fa831"></a>
### --start

<a id="74a7acd15a14c5a0"></a>
#### Description

It starts running glsnr. If glsnr is already running, an error occurs.

<a id="400ffc655717f762"></a>
#### Example

```
$ glsnr --start
Listener is started successfully.
```

<a id="08499f0e2fe3f70f"></a>
### --stop

<a id="b97b33d2f0b4fd97"></a>
#### Description

It stops the currently running glsnr.

<a id="d97d5a0a1174fcae"></a>
#### Example

```
$ glsnr --stop
Listener is stopped.
```

<a id="792ce6e6488b4a75"></a>
### --status

<a id="b0b47ba757addb91"></a>
#### Description

It displays the message about glsnr status.

<a id="de687e63b33dfe15"></a>
#### Example

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

<a id="21930c28787c4077"></a>
### --home

<a id="4e644323a205c3b4"></a>
#### Description

It sets db home.

<a id="b6ecad8485a56def"></a>
#### Example

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

<a id="dd9747befb554b08"></a>
### --help

<a id="8a0a02a3e826df43"></a>
#### Description

It displays the help message.

<a id="33bb01d53aa4cb54"></a>
#### Example

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

<a id="a2344449349927b4"></a>
## Listener Configuration

<a id="da3d43e903ab8058"></a>
### Configuration File and Environment Variables

glsnr uses the configuration file or environment variables for setting the configuration.

The environment variable is specified by using the name which 'GOLDILOCKS_' is added to the property name of the configuration as a prefix. For example, setting the LISTEN_PORT in configuration file is as same as specifying $GOLDILOCKS_LISTEN_PORT.

The contents of configuration file precedes the environment variable settings. (In other words, environment variables are applied only if the configuration file is not set.)

The environment file of glsnr is $GOLDILOCKS_DATA/conf/goldilocks.listener.conf. If the corresponding file is changed or the environment variables are set and glsnr is started to run, then the glsnr driving environment is modified.

If a user want to modify and apply the glsnr environment during running glsnr, a user should stop glsnr and change the content of configuration file or set the environment variable and then restart glsnr.

If a user stops the glsnr, a problem does not occur for the client which is already connected, but the problem occurs when being connected from a new client.

<a id="893d0343e94ccc14"></a>
### LISTEN_PORT

It is the port on which the glsnr waits for the connection.

<a id="54766ee259601764"></a>
| Item | Description |
| --- | --- |
| Name | LISTEN_PORT |
| Description | It is the port on which the glsnr waits for a connection. |
| Data type | INT |
| Default value/ range | 22581 / 1024 ~ 49151 |

<a id="1e6763c5fd71131f"></a>
#### Description

The client who wants a TCP connection should try to connect to the specified port.  
The port is available from 1024 to 49151.

<a id="2a8376b021eb2bca"></a>
### TCP_HOST

It is an IP address of NIC of which glsnr waits for the connection.

<a id="690460e20551c745"></a>
| Item | Description |
| --- | --- |
| Name | TCP_HOST |
| Description | It is the IP address which the glsnr binds. |
| Data type | ip address (ip v4) |
| Default value | 0.0.0.0 |

<a id="b767db5eb71e671d"></a>
#### Description

The client who wants a TCP connection should access the IP address specified above. The IP address is used in ip v4 format.

<a id="94b9db92da9a27d2"></a>
### BACKLOG

It is the number of clients which the glsnr can handle when multiple clients simultaneously access.

<a id="6dfc13da5e6f92e0"></a>
| Item | Description |
| --- | --- |
| Name | BACKLOG |
| Description | It is the number of client of which glsnr waits for the connection. |
| Data type | INT |
| Default value/ range | 1024 / 1 ~ 32768 |

<a id="482f165e6197009f"></a>
#### Description

This setting value does not guarantee the number of concurrent connector of the client.

<a id="a47b6c4ddd44e4a1"></a>
### DEFAULT_CS_MODE

It sets the access mode when the access mode is not designated as dedicated or shared on the client.

<a id="c688319c250103f4"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_CS_MODE |
| Description | It sets the default access mode. |
| Data type | String ( dedicated \| shared ) |
| Default value | dedicated |

<a id="14c508d8beca236f"></a>
#### Description

- The client/ server mode connected via glsnr supports two modes, which are dedicated and shared.
- Generally, the access mode is set as dedicated or shared on the client (It is .odbcini for ODBC), then it accesses. However, if it is not set on the client, the access mode is determined by setting DEFAULT_CS_MODE.

<a id="5c0548bb6b9dadb7"></a>
### TCP_VALIDNODE_CHECKING

It sets whether to check the validity of the client attempting to access.

<a id="bd29a39619b738c4"></a>
| Item | Description |
| --- | --- |
| Name | TCP_VALIDNODE_CHECKING |
| Description | It sets whether to check the client validity. |
| Data type | String ( NO \| INVITED \| EXCLUDED ) |
| Default value | NO |

<a id="51756b554cf1c70b"></a>
#### Description

- If the value is set to *NO*, the client validity is not checked. 
- If the value is set to *INVITED* and the file set in TCP_INVITED_FILE exists, then only the client having the IP address of the file set in TCP_INVITED_FILE is set to be valid.
- If the value is set to *EXCLUDED* and the file set in TCP_EXCLUDED_FILE exists, then only the client excluding the client who has IP address of the file set in TCP_EXCLUDED_FILE is set to be valid.

<a id="aaca8275e402a5ec"></a>
### TCP_INVITED_FILE

It is used only when the value of TCP VALIDNODE_CHECKING is *INVITED*.

<a id="d48652640fa63f56"></a>
| Item | Description |
| --- | --- |
| Name | TCP_INVITED_FILE |
| Description | It is the file with the valid user (IP address) list. |
| Data type | String |
| Default value | 'goldilocks.invited.conf' |

<a id="31258645753e9ec8"></a>
#### Description

If the set file exists, only the user (IP address) within the file is allowed to access.

<a id="8ae864897963773a"></a>
### TCP_EXCLUDED_FILE

It is used only when the value of TCP VALIDNODE_CHECKING is *EXCLUDED*.

<a id="75b09796286a6c3e"></a>
| Item | Description |
| --- | --- |
| Name | TCP_EXCLUDED_FILE |
| Description | It is the file with the invalid user (IP address) list. |
| Data type | String |
| Default value | 'goldilocks.excluded.conf' |

<a id="336a6a958cad3808"></a>
#### Description

If the set file exists, anyone except for the user (IP address) within the file is allowed to access.

<a id="061b8847500e8ec2"></a>
### TIMEOUT

It is the glsnr timeout value and its unit is second.

<a id="c9b87f6dfc5bda36"></a>
| Item | Description |
| --- | --- |
| Name | TIMEOUT |
| Description | glsnr timeout |
| Data type | INT |
| Default value/ range | 100 / ( 0 ~ 2147483647 ) |

<a id="6a3f16e362bf697f"></a>
#### Description

If the response is too slow or there is not a response from the client when glsnr communicates with the client, the connection is released by the specified timeout.

<a id="19593d22c9b848ae"></a>
### LISTENER_LOG_DIR

It sets the directory which stores the log to be display from the glsnr.

<a id="943d24d7654e510e"></a>
| Item | Description |
| --- | --- |
| Name | LISTENER_LOG_DIR |
| Description | It sets the directory which stores the log of the glsnr. |
| Data type | String |
| Default value | '&lt;GOLDILOCKS_DATA&gt;/trc' |

<a id="a07302ed7d49aeb7"></a>
#### Description

&lt;GOLDILOCKS_DATA&gt; of the setting value is replaced with the value of the environment variable $GOLDILOCKS_DATA.

<a id="b3ca2e2707f96626"></a>
### UDS_DIR

It sets the directory in which the Unix Domain Socket file used in glsnr is stored.

<a id="45148af7ac865215"></a>
| Item | Description |
| --- | --- |
| Name | UDS_DIR |
| Description | It sets the directory in which the Unix Domain Socket file used in glsnr is stored. |
| Data type | String |
| Default value/ range | '/tmp' / Maximum 60 byte |

<a id="373598f15f133236"></a>
#### Description

The maximum length of the directory should be set within 60 bytes. The absolute path of the Unix Domain Socket file (directory name + file name) depends on OS, but usually it is around 100 bytes.

---

[← 35. gcreatedb](35-gcreatedb.md) · [Table of contents](../README.md) · [37. gsql/gsqlnet (Interactive SQL Tool) →](37-gsql-gsqlnet-interactive-sql-tool.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
