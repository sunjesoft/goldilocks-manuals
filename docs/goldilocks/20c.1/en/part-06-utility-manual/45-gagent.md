<a id="96fe4e7ee7d3fdd2"></a>

# 45. gagent

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/96fe4e7ee7d3fdd2)  
> Tag: `20c.1_30_tag`

[← 44. glocator](44-glocator.md) · [Table of contents](../README.md) · [46. gloctl →](46-gloctl.md)

<a id="1f3740b05c3637bd"></a>
## Overview of gagent

<a id="069e59f451dd5d42"></a>
### Definition

gagent is a utility communicating with [glocator ](44-glocator.md#19ceb541c706922f) by being executed with each member node in GOLDILOCKS cluster system.

When [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#26f74ad6f85847fb) server property value of the node to which gagent belongs is set to 1 or 2, and the connection between nodes is disconnected so the cluster failover is proceeding, then gagent enquires to glocator the validity of the node to which the gagent belongs.  
For more information, refer to [Cluster Failover](44-glocator.md#c4448c510139171c).

<a id="0c677a924a38aaef"></a>
### Usage

```
gagent [options]
```

<a id="53acc31812d855cc"></a>
### Options

<a id="f91d2dfb7fb80e96"></a>
#### help

<a id="b1a0a2443824fcef"></a>
##### Description

It outputs the help message.

<a id="2d009d9534207ea6"></a>
##### Example

```
$ gagent --help

Usage:
 gagent [options]

Options:

-s  --start                        Start gagent
-t  --stop                         Stop gagent
-u  --status                       Get gagent status
-f  --conf                         Set configure file
-o  --home                         gmaster home path
-l  --silent                       Suppress display message
-r  --no-copyright                 Suppress display copy right and version
-h  --help                         Print help message
```

<a id="af0d175223efd386"></a>
#### start

<a id="88014b89ec8a4bf7"></a>
##### Description

It starts gagent. If gagent having the same home directory already has been started, then an error occurs.

<a id="d271815213179b5c"></a>
##### Example

```
$ gagent --start

gagent is started.
```

<a id="3ac8afd7d9c038dc"></a>
#### stop

<a id="7e390fea186ea79f"></a>
##### Description

It stops gagent which is in operation. The same home directory should be set to stop gagent in operation.

<a id="751930ddfb457991"></a>
##### Example

```
$ gagent --stop

gagent is stopped.
```

<a id="449744560243b91c"></a>
#### status

<a id="47e855054a1d056a"></a>
##### Description

It outputs the status message of gagent which is in operation. The same home directory should be set to check the status of gagent in operation.

<a id="f2e5d113c15e32dc"></a>
##### Example

```
$ gagent --status

gagent(31938) is running.
```

<a id="0296633797eedf3b"></a>
#### conf

<a id="1bba9dce06033641"></a>
##### Description

It sets the configure file when starting gagent.

<a id="f4aac8aa22ba550b"></a>
##### Example

```
$ gagent --start --conf goldilocks.gagent.conf

gagent is started.
```

<a id="cc52f5b4fe818f64"></a>
#### home

<a id="0474cb3c0afa9a02"></a>
##### Description

It sets the server home directory of GOLDILOCKS when starting gagent.  
When a relative path is used, it searchs for the home directory based on &lt;GOLDILOCKS_DATA&gt;.  
&lt;GOLDILOCKS_DATA&gt; is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="302252badbfa4324"></a>
##### Example

```
$ gagent --start --home g1n1_home --conf goldilocks.gagent.conf  

gagent is started.
```

In the example above, gagent is started by setting &lt;GOLDILOCKS_DATA&gt;/g1n1_home to home.

<a id="42fd2c004fe13e8d"></a>
#### silent

<a id="e5b0582fe2470df3"></a>
##### Description

It does not output the message of gagent about the execution.

<a id="92c820b0ba01f33f"></a>
##### Example

```
$ gagent --start --silent
```

<a id="8e63b43ac02f4742"></a>
#### no-copyright

<a id="e9cc901d02dedfa4"></a>
##### Description

It does not output the message of gagent's copyright and version about the execution.

<a id="3ed28becccb2f366"></a>
##### Example

```
$ gagent --start --no-copyright

gagent is started.
```

<a id="c863ae57bd5d1972"></a>
## gagent Configuration

<a id="2f6d1ae16f937f25"></a>
### Configuration File and Environment Variable

gagent can use a file or environment variable to set the configuration.

An environment variable can be set by using the name of which 'AGENT_' is added as a prefix to a configuration property name. For example, setting HOST in the configuration file has the same effect as specifying $AGENT_HOST.

The contents of a configuration file takes precedence over the environment variable setting values.

gagent has $GOLDILOCKS_DATA/conf/goldilocks.gagent.conf file as its environment file. To alter the driving environment of gagent, the file contents should be altered, or gagent should start after setting the environment variables.

<a id="d7ffdb76ed1a72b8"></a>
### Configuration Properties

<a id="36a43813c6b46c21"></a>
#### HOST

<a id="6cd3d93e98fb9626"></a>
| Item | Description |
| --- | --- |
| Name | HOST |
| Description | It is an IP address of which gagent binds. |
| Data type | ip address (ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of which gagent binds for UDP communication.  
It uses an IP address in IP v4 form.

<a id="7fea5e1cff83b5b1"></a>
#### REQUEST_PORT

<a id="b0d661aae5b70836"></a>
| Item | Description |
| --- | --- |
| Name | REQUEST_PORT |
| Description | It is a port which gagent uses for request. |
| Data type | INT |
| Default value/ range | 43581 / 1024~49151 |

It is a port of which gagent uses to request to glocator during tcp communication.  
The port from 1024 to 49151 can be used.

<a id="d82b88c2b34342a6"></a>
#### RESPONSE_PORT

<a id="4d758ea568a3041c"></a>
| Item | Description |
| --- | --- |
| Name | RESPONSE_PORT |
| Description | It is a port which gagent uses for response. |
| Data type | INT |
| Default value/ range | 43582 / 1024~49151 |

It is a port of which gagent uses to receive the response from glocator during tcp communication.  
The port from 1024 to 49151 can be used.

<a id="f944c3bb6cdb20bf"></a>
#### LOCATOR_HOST

<a id="6f73165be045dc5f"></a>
| Item | Description |
| --- | --- |
| Name | LOCATOR_HOST |
| Description | It is an IP address of glocator. |
| Data type | ip address(ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of glocator.

<a id="614b06700a7c19f2"></a>
#### LOCATOR_PORT

<a id="aadb29a08c51a1e2"></a>
| Item | Description |
| --- | --- |
| Name | LOCATOR_PORT |
| Description | It is a port of which glocator waits for Recv. |
| Data type | INT |
| Default value/ range | 42581 / 1024~49151 |

It is the port of glocator of when gagent sends packets to glocator.  
The port from 1024 to 49151 can be used.

<a id="30580d7660073fd8"></a>
#### SYSTEM_LOGGER_DIR

<a id="65e241743c9341a1"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_LOGGER_DIR |
| Description | It is the directory path of gagent trace log file. |
| Data type | String |
| Default value/ range | &lt;GOLDILOCKS_DATA&gt;/trc |

It is the directory path in which system trace log file of gagent is stored. &lt;GOLDILOCKS_DATA&gt; of the default value is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="76eac818aa66fe84"></a>
#### SYSTEM_UDS_DIR

<a id="e48fa806e05cb5ee"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_UDS_DIR |
| Description | It is the directory path of Unix Domain Socket file in gagent. |
| Data type | String |
| Default value/ range | /tmp (Maximum 50 bytes) |

It is the directory path to store Unix Domain Socket file in gagent. The default value is */tmp*. The maximum length of the directory should be set within 50 bytes.

<a id="602b7d8094a5b586"></a>
#### ALTERNATE_LOCATORS

<a id="7b149bd839f4c933"></a>
| Item | Description |
| --- | --- |
| Name | ALTERNATE_LOCATORS |
| Description | It sets the alternate locators. |
| Data Type | String |
| Default value/ range | empty / 0 ~ 1024 |

If glocator set in gagent does not respond, then it proceeds to process the operation by replacing with an alternate locator.

The following is an example of a configure file which used ALTERNATE_LOCATOR.

```
[AGENT]
PORT=43581
LOCATOR_HOST=127.0.0.1
LOCATOR_PORT=42581
ALTERNATE_LOCATORS=(LOCATOR1,LOCATOR2)

[LOCATOR1]
HOST=127.0.0.1
PORT=42582

[LOCATOR2]
HOST=127.0.0.1
PORT=42583
```

<a id="040494b7131e1a40"></a>
#### KEEPALIVE_IDLE_TIME

<a id="66f7cd5453b487df"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_IDLE_TIME |
| Description | tcp keepalive idle time for checking dead client session (sec) |
| Data type | INT |
| Default value/ range | 1 / 1 ~ 16383 |

It is the (idle) duration which the TCP packet is not sent nor is received before sending a keep alive packet. In other words, if TCP packet is not exchanged during the time set in KEEPALIVE_IDLE_TIME, then it performs the keep alive mechanism to detect the dead connection.

<a id="0b60133bb81cd215"></a>
#### KEEPALIVE_COUNT

<a id="30a898be458754da"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_COUNT |
| Description | tcp keepalive check count |
| Data type | INT |
| Default value/ range | 5 / 1 ~ 10 |

It is the number of performing keep alive mechanism.

<a id="d593d7d38d6ba6d3"></a>
#### KEEPALIVE_INTERVAL

<a id="73bb138141218a55"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_INTERVAL |
| Description | tcp keepalive packet interval (sec) |
| Data type | INT |
| Default value/ range | 5 |

It is the time interval to send the keep alive packet.

---

[← 44. glocator](44-glocator.md) · [Table of contents](../README.md) · [46. gloctl →](46-gloctl.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
