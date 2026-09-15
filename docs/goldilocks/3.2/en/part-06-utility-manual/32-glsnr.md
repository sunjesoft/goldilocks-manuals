<a id="8f33d71f4cb9fdd1"></a>

# 32. glsnr

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/8f33d71f4cb9fdd1)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 31. gcreatedb](31-gcreatedb.md) · [Table of contents](../README.md) · [33. gsql/gsqlnet (Interactive SQL Tool) →](33-gsql-gsqlnet-interactive-sql-tool.md)

<a id="64afe67277f99772"></a>
## Overview of glsnr

glsnr is a listener which GOLDILOCKS enables remote access through the network in the client/ server environment. glsnr should be run on the server for the network access to GOLDILOCKS.

glsnr is used as follows.

```
$ glsnr [options]
```

<a id="125cdd20fa44995c"></a>
## Command Options

The followings are cell prompt options for using glsnr.

<a id="7d4c6b3f3ba30b20"></a>
### --silent

<a id="25075b16f322ebb2"></a>
#### Description

It does not display the message for execution.

<a id="d6f7f729ed1a2469"></a>
#### Example

```
$ glsnr --start --silent
```

<a id="d377f9cb6df5ac75"></a>
### --start

<a id="466d16251b2bfa3c"></a>
#### Description

It starts running glsnr. If glsnr is already running, an error occurs.

<a id="2f2fa45bd3e03a06"></a>
#### Example

```
$ glsnr --start
Listener is started successfully.
```

<a id="5e4caaf7991967bb"></a>
### --stop

<a id="c192c17d405bf5f6"></a>
#### Description

It stops the currently running glsnr.

<a id="5b5c51c6fa44d24e"></a>
#### Example

```
$ glsnr --stop
Listener is stopped.
```

<a id="ca5303e9df3b09fd"></a>
### --status

<a id="44fcb85e66b3a30a"></a>
#### Description

It displays the message about glsnr status.

<a id="7ce90ef8ecc938ff"></a>
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

<a id="47c2132428658481"></a>
### --home

<a id="d5fffe40d3c9dc9e"></a>
#### Description

It sets db home.

<a id="8542a3a6cb4eec4c"></a>
#### Example

```
$ glsnr --start --home Gliese/home/g1n1_home
Listener is started successfully.
$ glsnr --status

Listener process ID : 20777
Listener configuration file : /home/goldilocsk/Gliese/home/g1n1_home/conf/goldilocks.listener.conf
Unix Domain Path : /tmp/unix-glsnr.22581
TCP Listen Host : 0.0.0.0, Port : 22581
default C/S mode : Dedicated
Connection Timeout(second) : 100

Listener is running.
```

<a id="c891a85cee8bcf41"></a>
### --help

<a id="5cbc8629d7d64e1c"></a>
#### Description

It displays the help message.

<a id="28dd972036a0bf43"></a>
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

<a id="89657c5620585252"></a>
## Listener Configuration

<a id="53586c47b6d7a126"></a>
### Configuration File and Environment Variables

glsnr uses the configuration file or environment variables for setting the configuration.

The environment variable is specified by using the name which 'GOLDILOCKS_' is added to the property name of the configuration as a prefix. For example, setting the LISTEN_PORT in configuration file is as same as specifying $GOLDILOCKS_LISTEN_PORT.

The contents of configuration file precedes the environment variable settings. (In other words, environment variables are applied only if the configuration file is not set.)

The environment file of glsnr is $GOLDILOCKS_DATA/conf/goldilocks.listener.conf. If the corresponding file is changed or the environment variables are set and glsnr is started to run, then the glsnr driving environment is modified.

If a user want to modify and apply the glsnr environment during running glsnr, a user should stop glsnr and change the content of configuration file or set the environment variable and then restart glsnr.

If a user stops the glsnr, a problem does not occur for the client which is already connected, but the problem occurs when being connected from a new client.

<a id="6eeee6f51a2e7fc8"></a>
### LISTEN_PORT

It is the port on which the glsnr waits for the connection.

<a id="2d666e3f13121538"></a>
| Item | Description |
| --- | --- |
| Name | LISTEN_PORT |
| Description | It is the port on which the glsnr waits for a connection. |
| Data type | INT |
| Default value/ range | 22581 / 1024 ~ 49151 |

<a id="8ab2fe4bb798d14c"></a>
#### Description

The client who wants a TCP connection should try to connect to the specified port.  
The port is available from 1024 to 49151.

<a id="4c4fbd7ec60b5663"></a>
### TCP_HOST

It is an IP address of NIC of which glsnr waits for the connection.

<a id="93c93967dde4a155"></a>
| Item | Description |
| --- | --- |
| Name | TCP_HOST |
| Description | It is the IP address which the glsnr binds. |
| Data type | ip address (ip v4) |
| Default value | 0.0.0.0 |

<a id="26814b7c9acb5b42"></a>
#### Description

The client who wants a TCP connection should access the IP address specified above. The IP address is used in ip v4 format.

<a id="0d386150dbece54d"></a>
### BACKLOG

It is the number of clients which the glsnr can handle when multiple clients simultaneously access.

<a id="35d40a3a24ed980e"></a>
| Item | Description |
| --- | --- |
| Name | BACKLOG |
| Description | It is the number of client of which glsnr waits for the connection. |
| Data type | INT |
| Default value/ range | 1024 / 1 ~ 32768 |

<a id="e22bc27b1e4cb7b7"></a>
#### Description

This setting value does not guarantee the number of concurrent connector of the client.

<a id="65fb7cbea4a772ea"></a>
### DEFAULT_CS_MODE

It sets the access mode when the access mode is not designated as dedicated or shared on the client.

<a id="2d9a3ebdeb62f427"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_CS_MODE |
| Description | It sets the default access mode. |
| Data type | String ( dedicated \| shared ) |
| Default value | dedicated |

<a id="aa9c17e2d02c6f06"></a>
#### Description

- The client/ server mode connected via glsnr supports two modes, which are dedicated and shared.
- Generally, the access mode is set as dedicated or shared on the client (It is .odbcini for ODBC), then it accesses. However, if it is not set on the client, the access mode is determined by setting DEFAULT_CS_MODE.

<a id="ada7f33d5265611d"></a>
### TCP_VALIDNODE_CHECKING

It sets whether to check the validity of the client attempting to access.

<a id="1fcb54c7d92ca92a"></a>
| Item | Description |
| --- | --- |
| Name | TCP_VALIDNODE_CHECKING |
| Description | It sets whether to check the client validity. |
| Data type | String ( NO \| INVITED \| EXCLUDED ) |
| Default value | NO |

<a id="dec8f12aecbd765a"></a>
#### Description

- If the value is set to *NO*, the client validity is not checked. 
- If the value is set to *INVITED* and the file set in TCP_INVITED_FILE exists, then only the client having the IP address of the file set in TCP_INVITED_FILE is set to be valid.
- If the value is set to *EXCLUDED* and the file set in TCP_EXCLUDED_FILE exists, then only the client excluding the client who has IP address of the file set in TCP_EXCLUDED_FILE is set to be valid.

<a id="e089d8f93e5fed72"></a>
### TCP_INVITED_FILE

It is used only when the value of TCP VALIDNODE_CHECKING is *INVITED*.

<a id="143b08c646c872f9"></a>
| Item | Description |
| --- | --- |
| Name | TCP_INVITED_FILE |
| Description | It is the file with the valid user (IP address) list. |
| Data type | String |
| Default value | 'goldilocks.invited.conf' |

<a id="43ff6efde89a5013"></a>
#### Description

If the set file exists, only the user (IP address) within the file is allowed to access.

<a id="34f8c4b0aa017224"></a>
### TCP_EXCLUDED_FILE

It is used only when the value of TCP VALIDNODE_CHECKING is *EXCLUDED*.

<a id="6fb91ff9e480307d"></a>
| Item | Description |
| --- | --- |
| Name | TCP_EXCLUDED_FILE |
| Description | It is the file with the invalid user (IP address) list. |
| Data type | String |
| Default value | 'goldilocks.excluded.conf' |

<a id="b462fa08483b6888"></a>
#### Description

If the set file exists, anyone except for the user (IP address) within the file is allowed to access.

<a id="7fe3623a9b8034cf"></a>
### TIMEOUT

It is the glsnr timeout value and its unit is second.

<a id="53d213b0d8a3deb0"></a>
| Item | Description |
| --- | --- |
| Name | TIMEOUT |
| Description | glsnr timeout |
| Data type | INT |
| Default value/ range | 100 / ( 0 ~ 2147483647 ) |

<a id="c90bba5e2de88ad4"></a>
#### Description

If the response is too slow or there is not a response from the client when glsnr communicates with the client, the connection is released by the specified timeout.

<a id="90016f83126fa996"></a>
### LISTENER_LOG_DIR

It sets the directory which stores the log to be display from the glsnr.

<a id="b26102e169081034"></a>
| Item | Description |
| --- | --- |
| Name | LISTENER_LOG_DIR |
| Description | It sets the directory which stores the log of the glsnr. |
| Data type | String |
| Default value | '&lt;GOLDILOCKS_DATA&gt;/trc' |

<a id="8300c6dab63f3e01"></a>
#### Description

&lt;GOLDILOCKS_DATA&gt; of the setting value is replaced with the value of the environment variable $GOLDILOCKS_DATA.

<a id="0200fb4722be0126"></a>
### UDS_DIR

It sets the directory in which the Unix Domain Socket file used in glsnr is stored.

<a id="ae20ea38bc482ab4"></a>
| Item | Description |
| --- | --- |
| Name | UDS_DIR |
| Description | It sets the directory in which the Unix Domain Socket file used in glsnr is stored. |
| Data type | String |
| Default value/ range | '/tmp' / Maximum 60 byte |

<a id="3ab2f2edc02d4b72"></a>
#### Description

The maximum length of the directory should be set within 60 bytes. The absolute path of the Unix Domain Socket file (directory name + file name) depends on OS, but usually it is around 100 bytes.

---

[← 31. gcreatedb](31-gcreatedb.md) · [Table of contents](../README.md) · [33. gsql/gsqlnet (Interactive SQL Tool) →](33-gsql-gsqlnet-interactive-sql-tool.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
