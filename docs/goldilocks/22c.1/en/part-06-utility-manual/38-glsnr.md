<a id="bcb878d48ad1518c"></a>

# 38. glsnr

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/bcb878d48ad1518c)  
> Tag: `22c.1_10_tag`

[← 37. gcreatedb](37-gcreatedb.md) · [Table of contents](../README.md) · [39. gsql/gsqlnet (Interactive SQL Tool) →](39-gsql-gsqlnet-interactive-sql-tool.md)

<a id="77a5f676fb55b5a7"></a>
## Overview of glsnr

glsnr is a listener which GOLDILOCKS enables remote access through the network in the client/ server environment. glsnr should be run on the server for the network access to GOLDILOCKS.

glsnr is used as follows.

```
$ glsnr [options]
```

<a id="dd16df4fd1665cf0"></a>
## Command Options

The followings are cell prompt options for using glsnr.

<a id="a0e9ec4a1336b3be"></a>
### --silent

<a id="eb264b642b8830ed"></a>
#### Description

It does not display the message for execution.

<a id="f4fc3d8ec734cac3"></a>
#### Example

```
$ glsnr --start --silent
```

<a id="3a6cd77e53acb61a"></a>
### --start

<a id="1d7feb1d8c3af21d"></a>
#### Description

It starts running glsnr. If glsnr is already running, an error occurs.

<a id="b520f43b22588cc0"></a>
#### Example

```
$ glsnr --start
Listener is started successfully.
```

<a id="7a8af37c2262c4b3"></a>
### --stop

<a id="d2758f56215b476b"></a>
#### Description

It stops the currently running glsnr.

<a id="5d0669e20cf57bff"></a>
#### Example

```
$ glsnr --stop
Listener is stopped.
```

<a id="1a4cad10c025fc1c"></a>
### --status

<a id="a089de7e0e87747a"></a>
#### Description

It displays the message about glsnr status.

<a id="820b9996edcd980d"></a>
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

<a id="82e0974d9e57afb6"></a>
### --home

<a id="53d5e6cb05a1dffa"></a>
#### Description

It sets db home.

<a id="78e307e1944eab31"></a>
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

<a id="039aefa524534520"></a>
### --help

<a id="c4695671d9a7253c"></a>
#### Description

It displays the help message.

<a id="28c4d2acf4db5c94"></a>
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

<a id="366aa29b15bee42f"></a>
## Listener Configuration

<a id="18f9448d40970c5d"></a>
### Configuration File and Environment Variables

glsnr uses the configuration file or environment variables for setting the configuration.

The environment variable is specified by using the name which 'GOLDILOCKS_' is added to the property name of the configuration as a prefix. For example, setting the LISTEN_PORT in configuration file is as same as specifying $GOLDILOCKS_LISTEN_PORT.

The contents of configuration file precedes the environment variable settings. (In other words, environment variables are applied only if the configuration file is not set.)

The environment file of glsnr is $GOLDILOCKS_DATA/conf/goldilocks.listener.conf. If the corresponding file is changed or the environment variables are set and glsnr is started to run, then the glsnr driving environment is modified.

If a user want to modify and apply the glsnr environment during running glsnr, a user should stop glsnr and change the content of configuration file or set the environment variable and then restart glsnr.

If a user stops the glsnr, a problem does not occur for the client which is already connected, but the problem occurs when being connected from a new client.

<a id="638ce2f07da3df36"></a>
### LISTEN_PORT

It is the port on which the glsnr waits for the connection.

<a id="5308d9d958557a16"></a>
| Item | Description |
| --- | --- |
| Name | LISTEN_PORT |
| Description | It is the port on which the glsnr waits for a connection. |
| Data type | INT |
| Default value/ range | 22581 / 1024 ~ 49151 |

<a id="4c1dc1b9f9d0c906"></a>
#### Description

The client who wants a TCP connection should try to connect to the specified port.  
The port is available from 1024 to 49151.

<a id="ae266305e4c90c2e"></a>
### TCP_HOST

It is an IP address of NIC of which glsnr waits for the connection.

<a id="4b7ee1400e9a9e05"></a>
| Item | Description |
| --- | --- |
| Name | TCP_HOST |
| Description | It is the IP address which the glsnr binds. |
| Data type | ip address |
| Default value | 0.0.0.0 |

<a id="0706ee3998abbf81"></a>
#### Description

The client who wants a TCP connection should access the IP address specified above. The IP address is used in IPv4 or IPv6 format.

<a id="0bcde2d66c54fa34"></a>
### BACKLOG

It is the number of clients which the glsnr can handle when multiple clients simultaneously access.

<a id="63b5ff4afb4da944"></a>
| Item | Description |
| --- | --- |
| Name | BACKLOG |
| Description | It is the number of client of which glsnr waits for the connection. |
| Data type | INT |
| Default value/ range | 1024 / 1 ~ 32768 |

<a id="8dffd4d5f26132ac"></a>
#### Description

This setting value does not guarantee the number of concurrent connector of the client.

<a id="b269b411fc35370e"></a>
### DEFAULT_CS_MODE

It sets the access mode when the access mode is not designated as dedicated or shared on the client.

<a id="d738a3d06374120d"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_CS_MODE |
| Description | It sets the default access mode. |
| Data type | String ( dedicated \| shared ) |
| Default value | dedicated |

<a id="855ba0d49a9c5bf0"></a>
#### Description

- The client/ server mode connected via glsnr supports two modes, which are dedicated and shared.
- Generally, the access mode is set as dedicated or shared on the client (It is .odbcini for ODBC), then it accesses. However, if it is not set on the client, the access mode is determined by setting DEFAULT_CS_MODE.

<a id="25f38f72295f0e74"></a>
### TCP_VALIDNODE_CHECKING

It sets whether to check the validity of the client attempting to access.

<a id="adc7d2202407b3ba"></a>
| Item | Description |
| --- | --- |
| Name | TCP_VALIDNODE_CHECKING |
| Description | It sets whether to check the client validity. |
| Data type | String ( NO \| INVITED \| EXCLUDED ) |
| Default value | NO |

<a id="c8e335feb967210a"></a>
#### Description

- If the value is set to *NO*, the client validity is not checked. 
- If the value is set to *INVITED* and the file set in TCP_INVITED_FILE exists, then only the client having the IP address of the file set in TCP_INVITED_FILE is set to be valid.
- If the value is set to *EXCLUDED* and the file set in TCP_EXCLUDED_FILE exists, then only the client excluding the client who has IP address of the file set in TCP_EXCLUDED_FILE is set to be valid.

<a id="00c8675c8929fca8"></a>
### TCP_INVITED_FILE

It is used only when the value of TCP VALIDNODE_CHECKING is *INVITED*.

<a id="d927d92245452743"></a>
| Item | Description |
| --- | --- |
| Name | TCP_INVITED_FILE |
| Description | It is the file with the valid user (IP address) list. |
| Data type | String |
| Default value | 'goldilocks.invited.conf' |

<a id="d287c903bea5d7e3"></a>
#### Description

If the set file exists, only the user (IP address) within the file is allowed to access.

<a id="5e52d269e9a7ce06"></a>
### TCP_EXCLUDED_FILE

It is used only when the value of TCP VALIDNODE_CHECKING is *EXCLUDED*.

<a id="c0937d17aa1cbccf"></a>
| Item | Description |
| --- | --- |
| Name | TCP_EXCLUDED_FILE |
| Description | It is the file with the invalid user (IP address) list. |
| Data type | String |
| Default value | 'goldilocks.excluded.conf' |

<a id="a886c12806203794"></a>
#### Description

If the set file exists, anyone except for the user (IP address) within the file is allowed to access.

<a id="2d64cdbed71ac274"></a>
### TIMEOUT

It is the glsnr timeout value and its unit is second.

<a id="cb2b61380e1a0cc1"></a>
| Item | Description |
| --- | --- |
| Name | TIMEOUT |
| Description | glsnr timeout |
| Data type | INT |
| Default value/ range | 100 / ( 0 ~ 2147483647 ) |

<a id="f921f78636a4c588"></a>
#### Description

If the response is too slow or there is not a response from the client when glsnr communicates with the client, the connection is released by the specified timeout.

<a id="9cb1c588a12d35ee"></a>
### LISTENER_LOG_DIR

It sets the directory which stores the log to be display from the glsnr.

<a id="78f4d13392329a2d"></a>
| Item | Description |
| --- | --- |
| Name | LISTENER_LOG_DIR |
| Description | It sets the directory which stores the log of the glsnr. |
| Data type | String |
| Default value | '&lt;GOLDILOCKS_DATA&gt;/trc' |

<a id="f8364e4ba40ff928"></a>
#### Description

&lt;GOLDILOCKS_DATA&gt; of the setting value is replaced with the value of the environment variable $GOLDILOCKS_DATA.

<a id="e64b44d5d109d100"></a>
### UDS_DIR

It sets the directory in which the Unix Domain Socket file used in glsnr is stored.

<a id="f609a6b328e7ce64"></a>
| Item | Description |
| --- | --- |
| Name | UDS_DIR |
| Description | It sets the directory in which the Unix Domain Socket file used in glsnr is stored. |
| Data type | String |
| Default value/ range | '/tmp' / Maximum 60 byte |

<a id="eb5470354310712d"></a>
#### Description

The maximum length of the directory should be set within 60 bytes. The absolute path of the Unix Domain Socket file (directory name + file name) depends on OS, but usually it is around 100 bytes.

---

[← 37. gcreatedb](37-gcreatedb.md) · [Table of contents](../README.md) · [39. gsql/gsqlnet (Interactive SQL Tool) →](39-gsql-gsqlnet-interactive-sql-tool.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
