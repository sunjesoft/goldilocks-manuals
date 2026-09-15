<a id="cfdd4261bac8bef9"></a>

# 43. glsnr

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/cfdd4261bac8bef9)  
> Tag: `26c.1_0_tag`

[← 42. gcreatedb](42-gcreatedb.md) · [Table of contents](../README.md) · [44. gsql/gsqlnet (Interactive SQL Tool) →](44-gsql-gsqlnet-interactive-sql-tool.md)

<a id="b1c92cc0b4612d13"></a>
## Overview of glsnr

glsnr is a listener which GOLDILOCKS enables remote access through the network in the client/ server environment. glsnr should be run on the server for the network access to GOLDILOCKS.

glsnr is used as follows.

```
$ glsnr [options]
```

<a id="dee9ddc43e9b932e"></a>
## Command Option

The following are cell prompt options for using glsnr.

<a id="f3036bcd8f6fb481"></a>
### --silent

<a id="d52c70f27f3071b7"></a>
#### Description

It does not display the message for execution.

<a id="ed536d389e91c876"></a>
#### Example

```
$ glsnr --start --silent
```

<a id="c7ae4a3c6ee534ca"></a>
### --start

<a id="fb709dbd9452392b"></a>
#### Description

It starts running glsnr. If glsnr is already running, an error occurs.

<a id="fc6baa2cbb64111a"></a>
#### Example

```
$ glsnr --start
Listener is started successfully.
```

<a id="bb2300ddf293b7e0"></a>
### --stop

<a id="c18d2573fa293897"></a>
#### Description

It stops the currently running glsnr.

<a id="ac8e6d7c69a96871"></a>
#### Example

```
$ glsnr --stop
Listener is stopped.
```

<a id="40d6e36ff43253f4"></a>
### --status

<a id="23dd5388975b5f13"></a>
#### Description

It displays the message about glsnr status.

<a id="74c52f37d1415529"></a>
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

<a id="8c0a5415c2a8372a"></a>
### --home

<a id="896b3addfa64fe39"></a>
#### Description

It sets db home.

<a id="07d71d76d2d1d40a"></a>
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

<a id="da82e14fa96c8e2f"></a>
### --help

<a id="eb1544dd0f5170a5"></a>
#### Description

It displays the help message.

<a id="dec577b3b00c5d8c"></a>
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

<a id="5249f5eb6dfc9943"></a>
## Listener Configuration

<a id="d670265b344472bf"></a>
### Configuration File and Environment Variables

glsnr uses the configuration file or environment variables for setting the configuration.

The environment variable is specified by using the name which 'GOLDILOCKS_' is added to the property name of the configuration as a prefix. For example, setting the LISTEN_PORT in configuration file is the same as specifying $GOLDILOCKS_LISTEN_PORT.

The contents of configuration file precedes the environment variable settings. (In other words, environment variables are applied only if the configuration file is not set.)

The environment file of glsnr is $GOLDILOCKS_DATA/conf/goldilocks.listener.conf. If the corresponding file is changed or the environment variables are set and glsnr is started to run, then the glsnr driving environment is modified.

If a user want to modify and apply the glsnr environment during running glsnr, a user should stop glsnr and change the content of configuration file or set the environment variable and then restart glsnr.

If a user stops the glsnr, a problem does not occur for the client which is already connected, but the problem occurs when being connected from a new client.

<a id="01f5e8f3d7d0e9b6"></a>
### LISTEN_PORT

It is the port on which the glsnr waits for the connection.

<a id="75d31e4398cc79e2"></a>
| Item | Description |
| --- | --- |
| Name | LISTEN_PORT |
| Description | It is the port on which the glsnr waits for a connection. |
| Data type | INT |
| Default value/ range | 22581 / 1024 ~ 49151 |

<a id="d9dbc94d7d9e5d44"></a>
#### Description

The client who wants a TCP connection should try to connect to the specified port.  
The port is available from 1024 to 49151.

<a id="920aceb29460bd01"></a>
### TCP_HOST

It is an IP address of NIC of which glsnr waits for the connection.

<a id="158a120dbc0b8c68"></a>
| Item | Description |
| --- | --- |
| Name | TCP_HOST |
| Description | It is the IP address which the glsnr binds. |
| Data type | ip address |
| Default value | 0.0.0.0 |

<a id="16fd3ad333c53701"></a>
#### Description

The client who wants a TCP connection should access the IP address specified above. The IP address is used in IPv4 or IPv6 format.

<a id="439b690c4deef6da"></a>
### BACKLOG

It is the number of clients which the glsnr can handle when multiple clients simultaneously access.

<a id="0b38d6b45e19f146"></a>
| Item | Description |
| --- | --- |
| Name | BACKLOG |
| Description | It is the number of client of which glsnr waits for the connection. |
| Data type | INT |
| Default value/ range | 1024 / 1 ~ 32768 |

<a id="579b111286b4bd29"></a>
#### Description

This setting value does not guarantee the number of concurrent connector of the client.

<a id="29c081a5751a3873"></a>
### DEFAULT_CS_MODE

It sets the access mode when the access mode is not designated as dedicated or shared on the client.

<a id="29081e03651daf94"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_CS_MODE |
| Description | It sets the default access mode. |
| Data type | String ( dedicated \| shared ) |
| Default value | dedicated |

<a id="2c56e3a9084d738d"></a>
#### Description

- The client/ server mode connected via glsnr supports two modes, which are dedicated and shared.
- Generally, the access mode is set as dedicated or shared on the client (It is .odbc.ini for ODBC), then it accesses. However, if it is not set on the client, the access mode is determined by setting DEFAULT_CS_MODE.

<a id="d4accf8ce3c450e0"></a>
### TCP_VALIDNODE_CHECKING

It sets whether to check the validity of the client attempting to access.

<a id="f9319a0b195908f0"></a>
| Item | Description |
| --- | --- |
| Name | TCP_VALIDNODE_CHECKING |
| Description | It sets whether to check the client validity. |
| Data type | String ( NO \| INVITED \| EXCLUDED ) |
| Default value | NO |

<a id="a0d71e30cbf6e1b2"></a>
#### Description

- If the value is set to *NO*, the client validity is not checked. 
- If the value is set to *INVITED* and the file set in TCP_INVITED_FILE exists, then only the client having the IP address of the file set in TCP_INVITED_FILE is set to be valid.
- If the value is set to *EXCLUDED* and the file set in TCP_EXCLUDED_FILE exists, then only the client excluding the client who has IP address of the file set in TCP_EXCLUDED_FILE is set to be valid.

<a id="9f822e87405abc1a"></a>
### TCP_INVITED_FILE

It is used only when the value of TCP VALIDNODE_CHECKING is *INVITED*.

<a id="38a796a0724b1573"></a>
| Item | Description |
| --- | --- |
| Name | TCP_INVITED_FILE |
| Description | It is the file with the valid user (IP address) list. |
| Data type | String |
| Default value | 'goldilocks.invited.conf' |

<a id="8c3a23b2121da78c"></a>
#### Description

If the set file exists, only the user (IP address) within the file is allowed to access.

<a id="2b82689ed3c1b62c"></a>
### TCP_EXCLUDED_FILE

It is used only when the value of TCP VALIDNODE_CHECKING is *EXCLUDED*.

<a id="4a373eef5d369b0d"></a>
| Item | Description |
| --- | --- |
| Name | TCP_EXCLUDED_FILE |
| Description | It is the file with the invalid user (IP address) list. |
| Data type | String |
| Default value | 'goldilocks.excluded.conf' |

<a id="1d7e6744cd12b022"></a>
#### Description

If the set file exists, anyone except for the user (IP address) within the file is allowed to access.

<a id="3f93eaa3d6a22d75"></a>
### TIMEOUT

It is the glsnr timeout value and its unit is second.

<a id="f63245526ddb6c4f"></a>
| Item | Description |
| --- | --- |
| Name | TIMEOUT |
| Description | glsnr timeout |
| Data type | INT |
| Default value/ range | 100 / ( 0 ~ 2147483647 ) |

<a id="97854376a9c5a619"></a>
#### Description

If the response is too slow or there is not a response from the client when glsnr communicates with the client, the connection is released by the specified timeout.

<a id="f9d1e7936f70396d"></a>
### LISTENER_LOG_DIR

It sets the directory which stores the log to be display from the glsnr.

<a id="9f2298584c3b30f4"></a>
| Item | Description |
| --- | --- |
| Name | LISTENER_LOG_DIR |
| Description | It sets the directory which stores the log of the glsnr. |
| Data type | String |
| Default value | '&lt;GOLDILOCKS_DATA&gt;/trc' |

<a id="e111c9e0cf96cec1"></a>
#### Description

&lt;GOLDILOCKS_DATA&gt; of the setting value is replaced with the value of the environment variable $GOLDILOCKS_DATA.

<a id="72124bd4f3028bdc"></a>
### UDS_DIR

It sets the directory in which the Unix Domain Socket file used in glsnr is stored.

<a id="256c4d56ccd3308a"></a>
| Item | Description |
| --- | --- |
| Name | UDS_DIR |
| Description | It sets the directory in which the Unix Domain Socket file used in glsnr is stored. |
| Data type | String |
| Default value/ range | '/tmp' / Maximum 60 byte |

<a id="3c1a8bdcccb02624"></a>
#### Description

The maximum length of the directory should be set within 60 bytes. The absolute path of the Unix Domain Socket file (directory name + file name) depends on OS, but usually it is around 100 bytes.

---

[← 42. gcreatedb](42-gcreatedb.md) · [Table of contents](../README.md) · [44. gsql/gsqlnet (Interactive SQL Tool) →](44-gsql-gsqlnet-interactive-sql-tool.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
