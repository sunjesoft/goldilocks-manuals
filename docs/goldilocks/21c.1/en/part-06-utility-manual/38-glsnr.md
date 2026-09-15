<a id="97381bb2ec74e482"></a>

# 38. glsnr

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/97381bb2ec74e482)  
> Tag: `21c.1_35_tag`

[← 37. gcreatedb](37-gcreatedb.md) · [Table of contents](../README.md) · [39. gsql/gsqlnet (Interactive SQL Tool) →](39-gsql-gsqlnet-interactive-sql-tool.md)

<a id="7a37657495855228"></a>
## Overview of glsnr

glsnr is a listener which GOLDILOCKS enables remote access through the network in the client/ server environment. glsnr should be run on the server for the network access to GOLDILOCKS.

glsnr is used as follows.

```
$ glsnr [options]
```

<a id="8d3720266d87aca2"></a>
## Command Options

The followings are cell prompt options for using glsnr.

<a id="4d855e363172c499"></a>
### --silent

<a id="ae8e0e252d023d55"></a>
#### Description

It does not display the message for execution.

<a id="cb019b5d07baaef0"></a>
#### Example

```
$ glsnr --start --silent
```

<a id="fcbb2ef4b6bf11d9"></a>
### --start

<a id="034afe0b7f9d13a8"></a>
#### Description

It starts running glsnr. If glsnr is already running, an error occurs.

<a id="75969bc88a6420c9"></a>
#### Example

```
$ glsnr --start
Listener is started successfully.
```

<a id="84079c334297cf4d"></a>
### --stop

<a id="dd324e8e059ba3db"></a>
#### Description

It stops the currently running glsnr.

<a id="ff2767036aaf90a8"></a>
#### Example

```
$ glsnr --stop
Listener is stopped.
```

<a id="26c405270cbb5450"></a>
### --status

<a id="c76030db3a8ba0d2"></a>
#### Description

It displays the message about glsnr status.

<a id="e8634809553274e2"></a>
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

<a id="e15388ece03ea7eb"></a>
### --home

<a id="cfce6192818a8ac4"></a>
#### Description

It sets db home.

<a id="e8da2afb6238100d"></a>
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

<a id="b7b4af7d959d47d8"></a>
### --help

<a id="98fc079d5c486453"></a>
#### Description

It displays the help message.

<a id="27803e6e7ba5f136"></a>
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

<a id="31f87307c5a3b0b2"></a>
## Listener Configuration

<a id="d25c761d03852933"></a>
### Configuration File and Environment Variables

glsnr uses the configuration file or environment variables for setting the configuration.

The environment variable is specified by using the name which 'GOLDILOCKS_' is added to the property name of the configuration as a prefix. For example, setting the LISTEN_PORT in configuration file is as same as specifying $GOLDILOCKS_LISTEN_PORT.

The contents of configuration file precedes the environment variable settings. (In other words, environment variables are applied only if the configuration file is not set.)

The environment file of glsnr is $GOLDILOCKS_DATA/conf/goldilocks.listener.conf. If the corresponding file is changed or the environment variables are set and glsnr is started to run, then the glsnr driving environment is modified.

If a user want to modify and apply the glsnr environment during running glsnr, a user should stop glsnr and change the content of configuration file or set the environment variable and then restart glsnr.

If a user stops the glsnr, a problem does not occur for the client which is already connected, but the problem occurs when being connected from a new client.

<a id="d59ec8937579bc6b"></a>
### LISTEN_PORT

It is the port on which the glsnr waits for the connection.

<a id="d3ab174a976809fd"></a>
| Item | Description |
| --- | --- |
| Name | LISTEN_PORT |
| Description | It is the port on which the glsnr waits for a connection. |
| Data type | INT |
| Default value/ range | 22581 / 1024 ~ 49151 |

<a id="24be8a8ae3a7e17a"></a>
#### Description

The client who wants a TCP connection should try to connect to the specified port.  
The port is available from 1024 to 49151.

<a id="606b3e49fbc1bb3c"></a>
### TCP_HOST

It is an IP address of NIC of which glsnr waits for the connection.

<a id="bb1af5c65556a18e"></a>
| Item | Description |
| --- | --- |
| Name | TCP_HOST |
| Description | It is the IP address which the glsnr binds. |
| Data type | ip address |
| Default value | 0.0.0.0 |

<a id="04f52b3f7a754c73"></a>
#### Description

The client who wants a TCP connection should access the IP address specified above. The IP address is used in IPv4 or IPv6 format.

<a id="bad99f0feda80089"></a>
### BACKLOG

It is the number of clients which the glsnr can handle when multiple clients simultaneously access.

<a id="b16dc0606c23ad90"></a>
| Item | Description |
| --- | --- |
| Name | BACKLOG |
| Description | It is the number of client of which glsnr waits for the connection. |
| Data type | INT |
| Default value/ range | 1024 / 1 ~ 32768 |

<a id="727a82384dc55042"></a>
#### Description

This setting value does not guarantee the number of concurrent connector of the client.

<a id="61fb8730f635395e"></a>
### DEFAULT_CS_MODE

It sets the access mode when the access mode is not designated as dedicated or shared on the client.

<a id="e5165351c2ac4a6c"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_CS_MODE |
| Description | It sets the default access mode. |
| Data type | String ( dedicated \| shared ) |
| Default value | dedicated |

<a id="f9cc59e5df5a80d8"></a>
#### Description

- The client/ server mode connected via glsnr supports two modes, which are dedicated and shared.
- Generally, the access mode is set as dedicated or shared on the client (It is .odbcini for ODBC), then it accesses. However, if it is not set on the client, the access mode is determined by setting DEFAULT_CS_MODE.

<a id="c737978a2cc12906"></a>
### TCP_VALIDNODE_CHECKING

It sets whether to check the validity of the client attempting to access.

<a id="b10505caf64d8d8c"></a>
| Item | Description |
| --- | --- |
| Name | TCP_VALIDNODE_CHECKING |
| Description | It sets whether to check the client validity. |
| Data type | String ( NO \| INVITED \| EXCLUDED ) |
| Default value | NO |

<a id="20508ff1168e5281"></a>
#### Description

- If the value is set to *NO*, the client validity is not checked. 
- If the value is set to *INVITED* and the file set in TCP_INVITED_FILE exists, then only the client having the IP address of the file set in TCP_INVITED_FILE is set to be valid.
- If the value is set to *EXCLUDED* and the file set in TCP_EXCLUDED_FILE exists, then only the client excluding the client who has IP address of the file set in TCP_EXCLUDED_FILE is set to be valid.

<a id="0244e807f3704859"></a>
### TCP_INVITED_FILE

It is used only when the value of TCP VALIDNODE_CHECKING is *INVITED*.

<a id="5b1f7d6181d33a8c"></a>
| Item | Description |
| --- | --- |
| Name | TCP_INVITED_FILE |
| Description | It is the file with the valid user (IP address) list. |
| Data type | String |
| Default value | 'goldilocks.invited.conf' |

<a id="ea5e40a815300ae1"></a>
#### Description

If the set file exists, only the user (IP address) within the file is allowed to access.

<a id="ebbfadafcb951ac3"></a>
### TCP_EXCLUDED_FILE

It is used only when the value of TCP VALIDNODE_CHECKING is *EXCLUDED*.

<a id="b9dcf472035be605"></a>
| Item | Description |
| --- | --- |
| Name | TCP_EXCLUDED_FILE |
| Description | It is the file with the invalid user (IP address) list. |
| Data type | String |
| Default value | 'goldilocks.excluded.conf' |

<a id="d379f98df13480e5"></a>
#### Description

If the set file exists, anyone except for the user (IP address) within the file is allowed to access.

<a id="da6ab56a3ca9d397"></a>
### TIMEOUT

It is the glsnr timeout value and its unit is second.

<a id="79e25d542c4183a6"></a>
| Item | Description |
| --- | --- |
| Name | TIMEOUT |
| Description | glsnr timeout |
| Data type | INT |
| Default value/ range | 100 / ( 0 ~ 2147483647 ) |

<a id="73e37af9716e6bf0"></a>
#### Description

If the response is too slow or there is not a response from the client when glsnr communicates with the client, the connection is released by the specified timeout.

<a id="df10cc585045d2f1"></a>
### LISTENER_LOG_DIR

It sets the directory which stores the log to be display from the glsnr.

<a id="bd91d26a44ccf32a"></a>
| Item | Description |
| --- | --- |
| Name | LISTENER_LOG_DIR |
| Description | It sets the directory which stores the log of the glsnr. |
| Data type | String |
| Default value | '&lt;GOLDILOCKS_DATA&gt;/trc' |

<a id="204198d893f81698"></a>
#### Description

&lt;GOLDILOCKS_DATA&gt; of the setting value is replaced with the value of the environment variable $GOLDILOCKS_DATA.

<a id="7ae4f6045e0283a4"></a>
### UDS_DIR

It sets the directory in which the Unix Domain Socket file used in glsnr is stored.

<a id="f145c42228b0f0ec"></a>
| Item | Description |
| --- | --- |
| Name | UDS_DIR |
| Description | It sets the directory in which the Unix Domain Socket file used in glsnr is stored. |
| Data type | String |
| Default value/ range | '/tmp' / Maximum 60 byte |

<a id="999e7a239aeb13e4"></a>
#### Description

The maximum length of the directory should be set within 60 bytes. The absolute path of the Unix Domain Socket file (directory name + file name) depends on OS, but usually it is around 100 bytes.

---

[← 37. gcreatedb](37-gcreatedb.md) · [Table of contents](../README.md) · [39. gsql/gsqlnet (Interactive SQL Tool) →](39-gsql-gsqlnet-interactive-sql-tool.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
