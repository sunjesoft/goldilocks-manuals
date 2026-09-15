<a id="ce1b1ef775e02ceb"></a>

# 52. gagent

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/ce1b1ef775e02ceb)  
> Tag: `26c.1_0_tag`

[← 51. glocator](51-glocator.md) · [Table of contents](../README.md) · [53. gloctl →](53-gloctl.md)

<a id="4ac97b00a512e355"></a>
## Overview of gagent

<a id="46fff30db778f292"></a>
### Definition

gagent is a utility communicating with [glocator ](51-glocator.md#0e0291a55963f28e) by being executed with each member node in GOLDILOCKS cluster system.

When [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#77027a79e36b9077) server property value of the node to which gagent belongs is set to 1 or 2, and the connection between nodes is disconnected so the cluster failover is proceeding, then gagent enquires to glocator the validity of the node to which the gagent belongs.  
For more information, refer to [Cluster Failover](51-glocator.md#e6961f973f6c391e).

<a id="c1f1eb1ee6f39c70"></a>
### Usage

```
gagent [options]
```

<a id="21bb6e1409b0e436"></a>
### Options

<a id="195376e4e9f9635a"></a>
#### help

<a id="87bf3ea557a74c13"></a>
##### Description

It outputs the help message.

<a id="ea329438a77e2006"></a>
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

<a id="fb00ddf8dd764d9d"></a>
#### start

<a id="1847d3d0c8fe6840"></a>
##### Description

It starts gagent. If gagent having the same home directory already has been started, then an error occurs.

<a id="74c26d001a05c574"></a>
##### Example

```
$ gagent --start

gagent is started.
```

<a id="be1cc48feafd0b21"></a>
#### stop

<a id="e93f8cedd75567bd"></a>
##### Description

It stops gagent which is in operation. The same home directory should be set to stop gagent in operation.

<a id="72e68acb64d9eaa4"></a>
##### Example

```
$ gagent --stop

gagent is stopped.
```

<a id="2e37e762b710c390"></a>
#### status

<a id="a9a3495f2b9ddaa3"></a>
##### Description

It outputs the status message of gagent which is in operation. The same home directory should be set to check the status of gagent in operation.

<a id="3baf3b6b44688dab"></a>
##### Example

```
$ gagent --status

gagent(31938) is running.
```

<a id="ca4d0e867cbb94fa"></a>
#### conf

<a id="2b8fdd8ca3df68ed"></a>
##### Description

It sets the configure file when starting gagent.

<a id="d0803c07c574dd89"></a>
##### Example

```
$ gagent --start --conf goldilocks.gagent.conf

gagent is started.
```

<a id="3ddf45d282203e6e"></a>
#### home

<a id="63461d2828929e11"></a>
##### Description

It sets the server home directory of GOLDILOCKS when starting gagent.  
When a relative path is used, it searchs for the home directory based on &lt;GOLDILOCKS_DATA&gt;.  
&lt;GOLDILOCKS_DATA&gt; is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="ef3a23ad3dd1f59d"></a>
##### Example

```
$ gagent --start --home g1n1_home --conf goldilocks.gagent.conf  

gagent is started.
```

In the example above, gagent is started by setting &lt;GOLDILOCKS_DATA&gt;/g1n1_home to home.

<a id="3465960e91f22cdc"></a>
#### silent

<a id="e4e476eaeaf6ebce"></a>
##### Description

It does not output the message of gagent about the execution.

<a id="c162b3b1fb1de744"></a>
##### Example

```
$ gagent --start --silent
```

<a id="790ff99556aba65b"></a>
#### no-copyright

<a id="baad5e3855b4a749"></a>
##### Description

It does not output the message of gagent's copyright and version about the execution.

<a id="4b21fc1fc31fa183"></a>
##### Example

```
$ gagent --start --no-copyright

gagent is started.
```

<a id="139a4c31fd64949c"></a>
## gagent Configuration

<a id="f67bf6458de53150"></a>
### Configuration File and Environment Variable

gagent can use a file or environment variable to set the configuration.

An environment variable can be set by using the name of which 'AGENT_' is added as a prefix to a configuration property name. For example, setting HOST in the configuration file has the same effect as specifying $AGENT_HOST.

The contents of a configuration file takes precedence over the environment variable setting values.

gagent has $GOLDILOCKS_DATA/conf/goldilocks.gagent.conf file as its environment file. To alter the driving environment of gagent, the file contents should be altered, or gagent should start after setting the environment variables.

<a id="7f998d6c6be97f0b"></a>
### Configuration Properties

<a id="c5ef9dfbcac4e9c7"></a>
#### HOST

<a id="193a3e9ff08f1acc"></a>
| Item | Description |
| --- | --- |
| Name | HOST |
| Description | It is an IP address of which gagent binds. |
| Data type | ip address (ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of which gagent binds for UDP communication.  
It uses an IP address in IP v4 form.

<a id="b84478ff9d457451"></a>
#### REQUEST_PORT

<a id="b2b56b61cc137b7d"></a>
| Item | Description |
| --- | --- |
| Name | REQUEST_PORT |
| Description | It is a port which gagent uses for request. |
| Data type | INT |
| Default value/ range | 43581 / 1024~49151 |

It is a port of which gagent uses to request to glocator during tcp communication.  
The port from 1024 to 49151 can be used.

<a id="d86d310f55d2dea1"></a>
#### RESPONSE_PORT

<a id="f952a5f4264e76fc"></a>
| Item | Description |
| --- | --- |
| Name | RESPONSE_PORT |
| Description | It is a port which gagent uses for response. |
| Data type | INT |
| Default value/ range | 43582 / 1024~49151 |

It is a port of which gagent uses to receive the response from glocator during tcp communication.  
The port from 1024 to 49151 can be used.

<a id="bc3c6d58adddcb61"></a>
#### LOCATOR_HOST

<a id="7b2a79fcb75ea759"></a>
| Item | Description |
| --- | --- |
| Name | LOCATOR_HOST |
| Description | It is an IP address of glocator. |
| Data type | ip address(ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of glocator.

<a id="258409ad4fb58ee4"></a>
#### LOCATOR_PORT

<a id="002f11e6369b621a"></a>
| Item | Description |
| --- | --- |
| Name | LOCATOR_PORT |
| Description | It is a port of which glocator waits for Recv. |
| Data type | INT |
| Default value/ range | 42581 / 1024~49151 |

It is the port of glocator of when gagent sends packets to glocator.  
The port from 1024 to 49151 can be used.

<a id="50b5ac4cb52def6d"></a>
#### SYSTEM_LOGGER_DIR

<a id="1e8c8a57b04a0871"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_LOGGER_DIR |
| Description | It is the directory path of gagent trace log file. |
| Data type | String |
| Default value/ range | &lt;GOLDILOCKS_DATA&gt;/trc |

It is the directory path in which system trace log file of gagent is stored. &lt;GOLDILOCKS_DATA&gt; of the default value is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="648e22cf658f39cf"></a>
#### SYSTEM_UDS_DIR

<a id="6c1dae7b8debf85e"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_UDS_DIR |
| Description | It is the directory path which stores Unix Domain Socket file of gagent. |
| Data type | String |
| Default value/ range | /tmp (Maximum 50 bytes) |

It is the directory path which stores Unix Domain Socket file of gagent. The default value is /tmp. The directory length can be set up to 50 bytes.

<a id="bb1e499f25842748"></a>
#### ALTERNATE_LOCATOR

<a id="6dca0807104a503d"></a>
| Item | Description |
| --- | --- |
| Name | ALTERNATE_LOCATOR |
| Description | It sets the alternate locator. |
| Data Type | String |
| Default value/ range | empty / 0 ~ 1024 |

If the connection to the glocator set in the gagent is disconnected, it will connect to the alternate locator to continue operations. When the glocator is replicated and the gagent attempts to connect to a substitute glocator, it will be redirected to connect to the master.

The following is an example of a configure file which used ALTERNATE_LOCATOR.

```
[AGENT]
REQUEST_PORT=43581
RESPONSE_PORT=43581
LOCATOR_HOST=127.0.0.1
LOCATOR_PORT=42581
ALTERNATE_LOCATOR=LOCATOR1

[LOCATOR1]
HOST=127.0.0.1
PORT=42582
```

<a id="caf33a06389d0cb8"></a>
#### KEEPALIVE_IDLE_TIME

<a id="c2adca8fd7d721e9"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_IDLE_TIME |
| Description | tcp keepalive idle time for checking dead client session (sec) |
| Data type | INT |
| Default value/ range | 1 / 1 ~ 16383 |

It is the (idle) duration which the TCP packet is not sent nor is received before sending a keep alive packet. In other words, if TCP packet is not exchanged during the time set in KEEPALIVE_IDLE_TIME, then it performs the keep alive mechanism to detect the dead connection.

<a id="6c34218fa01ce64e"></a>
#### KEEPALIVE_COUNT

<a id="dda4ca2e323269f3"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_COUNT |
| Description | tcp keepalive check count |
| Data type | INT |
| Default value/ range | 5 / 1 ~ 10 |

It is the number of performing keep alive mechanism.

<a id="2693583a76ba0a16"></a>
#### KEEPALIVE_INTERVAL

<a id="dcf8ebcd480a3fd2"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_INTERVAL |
| Description | tcp keepalive packet interval (sec) |
| Data type | INT |
| Default value/ range | 5 |

It is the time interval to send the keep alive packet.

---

[← 51. glocator](51-glocator.md) · [Table of contents](../README.md) · [53. gloctl →](53-gloctl.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
