<a id="5579fde13ef1fca2"></a>

# 47. gagent

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/5579fde13ef1fca2)  
> Tag: `22c.1_10_tag`

[← 46. glocator](46-glocator.md) · [Table of contents](../README.md) · [48. gloctl →](48-gloctl.md)

<a id="8164473b1bc31099"></a>
## Overview of gagent

<a id="08a5ad10d2961395"></a>
### Definition

gagent is a utility communicating with [glocator ](46-glocator.md#4e23705d562834a7) by being executed with each member node in GOLDILOCKS cluster system.

When [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#be19510d2caed4c1) server property value of the node to which gagent belongs is set to 1 or 2, and the connection between nodes is disconnected so the cluster failover is proceeding, then gagent enquires to glocator the validity of the node to which the gagent belongs.  
For more information, refer to [Cluster Failover](46-glocator.md#2ecdbe2e2c100d4c).

<a id="9049deffc1cdde7e"></a>
### Usage

```
gagent [options]
```

<a id="a7a4bc8a61ad31c5"></a>
### Options

<a id="47739e02f9f4a767"></a>
#### help

<a id="3ee7b5f048e08fb4"></a>
##### Description

It outputs the help message.

<a id="2f8dde5d397e01bc"></a>
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

<a id="63b1bc6cabeb4001"></a>
#### start

<a id="6a3a8e00ff65630f"></a>
##### Description

It starts gagent. If gagent having the same home directory already has been started, then an error occurs.

<a id="cf650c98b1bdf252"></a>
##### Example

```
$ gagent --start

gagent is started.
```

<a id="b54a441bc86a2ac7"></a>
#### stop

<a id="69b88dbab01c9bb1"></a>
##### Description

It stops gagent which is in operation. The same home directory should be set to stop gagent in operation.

<a id="d59c0f4b70a6a430"></a>
##### Example

```
$ gagent --stop

gagent is stopped.
```

<a id="bd4e05ac1e56a99f"></a>
#### status

<a id="d1bb2e7b45f242b6"></a>
##### Description

It outputs the status message of gagent which is in operation. The same home directory should be set to check the status of gagent in operation.

<a id="9265e372c9f51e67"></a>
##### Example

```
$ gagent --status

gagent(31938) is running.
```

<a id="98ef6424bbad69f3"></a>
#### conf

<a id="c304333e7403c55f"></a>
##### Description

It sets the configure file when starting gagent.

<a id="c984fb2736f158f4"></a>
##### Example

```
$ gagent --start --conf goldilocks.gagent.conf

gagent is started.
```

<a id="2bc7e9d6babb273f"></a>
#### home

<a id="0e977d38556549ed"></a>
##### Description

It sets the server home directory of GOLDILOCKS when starting gagent.  
When a relative path is used, it searchs for the home directory based on &lt;GOLDILOCKS_DATA&gt;.  
&lt;GOLDILOCKS_DATA&gt; is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="7e8aec09df1b1666"></a>
##### Example

```
$ gagent --start --home g1n1_home --conf goldilocks.gagent.conf  

gagent is started.
```

In the example above, gagent is started by setting &lt;GOLDILOCKS_DATA&gt;/g1n1_home to home.

<a id="44a3ab986e10c175"></a>
#### silent

<a id="373131e562315d38"></a>
##### Description

It does not output the message of gagent about the execution.

<a id="4f180fcf6c64055e"></a>
##### Example

```
$ gagent --start --silent
```

<a id="b8f6c64c5ccce74b"></a>
#### no-copyright

<a id="268776b20267cacd"></a>
##### Description

It does not output the message of gagent's copyright and version about the execution.

<a id="2e92c4539ba08957"></a>
##### Example

```
$ gagent --start --no-copyright

gagent is started.
```

<a id="089ab253ce374183"></a>
## gagent Configuration

<a id="0b18cd99d15145a2"></a>
### Configuration File and Environment Variable

gagent can use a file or environment variable to set the configuration.

An environment variable can be set by using the name of which 'AGENT_' is added as a prefix to a configuration property name. For example, setting HOST in the configuration file has the same effect as specifying $AGENT_HOST.

The contents of a configuration file takes precedence over the environment variable setting values.

gagent has $GOLDILOCKS_DATA/conf/goldilocks.gagent.conf file as its environment file. To alter the driving environment of gagent, the file contents should be altered, or gagent should start after setting the environment variables.

<a id="e82249ec06686c14"></a>
### Configuration Properties

<a id="bef5d47fd5b4c226"></a>
#### HOST

<a id="696effd37f659f6d"></a>
| Item | Description |
| --- | --- |
| Name | HOST |
| Description | It is an IP address of which gagent binds. |
| Data type | ip address (ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of which gagent binds for UDP communication.  
It uses an IP address in IP v4 form.

<a id="467b5ac1d7067a1a"></a>
#### REQUEST_PORT

<a id="cdbb7ac2cb8e5088"></a>
| Item | Description |
| --- | --- |
| Name | REQUEST_PORT |
| Description | It is a port which gagent uses for request. |
| Data type | INT |
| Default value/ range | 43581 / 1024~49151 |

It is a port of which gagent uses to request to glocator during tcp communication.  
The port from 1024 to 49151 can be used.

<a id="63d89577f0ac6a57"></a>
#### RESPONSE_PORT

<a id="8b863c37d3b720c6"></a>
| Item | Description |
| --- | --- |
| Name | RESPONSE_PORT |
| Description | It is a port which gagent uses for response. |
| Data type | INT |
| Default value/ range | 43582 / 1024~49151 |

It is a port of which gagent uses to receive the response from glocator during tcp communication.  
The port from 1024 to 49151 can be used.

<a id="b40d39d453d8da3f"></a>
#### LOCATOR_HOST

<a id="a5610ccaabc6c1f6"></a>
| Item | Description |
| --- | --- |
| Name | LOCATOR_HOST |
| Description | It is an IP address of glocator. |
| Data type | ip address(ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of glocator.

<a id="e39bb88afd7c0c2e"></a>
#### LOCATOR_PORT

<a id="bcce2554268a3a65"></a>
| Item | Description |
| --- | --- |
| Name | LOCATOR_PORT |
| Description | It is a port of which glocator waits for Recv. |
| Data type | INT |
| Default value/ range | 42581 / 1024~49151 |

It is the port of glocator of when gagent sends packets to glocator.  
The port from 1024 to 49151 can be used.

<a id="cae61304ef541ec8"></a>
#### SYSTEM_LOGGER_DIR

<a id="58b3af7b1514694c"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_LOGGER_DIR |
| Description | It is the directory path of gagent trace log file. |
| Data type | String |
| Default value/ range | &lt;GOLDILOCKS_DATA&gt;/trc |

It is the directory path in which system trace log file of gagent is stored. &lt;GOLDILOCKS_DATA&gt; of the default value is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="db86ce3f2994ba1c"></a>
#### SYSTEM_UDS_DIR

<a id="a78dbac1444e5e00"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_UDS_DIR |
| Description | It is the directory path which stores Unix Domain Socket file of gagent. |
| Data type | String |
| Default value/ range | /tmp (Maximum 50 bytes) |

It is the directory path which stores Unix Domain Socket file of gagent. The default value is /tmp. The directory length can be set up to 50 bytes.

<a id="642110fd2b0a1c05"></a>
#### ALTERNATE_LOCATORS

<a id="d382ea179682c040"></a>
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

<a id="70ba0bd0e37a157b"></a>
#### KEEPALIVE_IDLE_TIME

<a id="2ac306fe57d7d31f"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_IDLE_TIME |
| Description | tcp keepalive idle time for checking dead client session (sec) |
| Data type | INT |
| Default value/ range | 1 / 1 ~ 16383 |

It is the (idle) duration which the TCP packet is not sent nor is received before sending a keep alive packet. In other words, if TCP packet is not exchanged during the time set in KEEPALIVE_IDLE_TIME, then it performs the keep alive mechanism to detect the dead connection.

<a id="901de9314930be83"></a>
#### KEEPALIVE_COUNT

<a id="3500886e8006ec4d"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_COUNT |
| Description | tcp keepalive check count |
| Data type | INT |
| Default value/ range | 5 / 1 ~ 10 |

It is the number of performing keep alive mechanism.

<a id="a7cfe49d98df484c"></a>
#### KEEPALIVE_INTERVAL

<a id="bbf61fcd0b6abeb6"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_INTERVAL |
| Description | tcp keepalive packet interval (sec) |
| Data type | INT |
| Default value/ range | 5 |

It is the time interval to send the keep alive packet.

---

[← 46. glocator](46-glocator.md) · [Table of contents](../README.md) · [48. gloctl →](48-gloctl.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
