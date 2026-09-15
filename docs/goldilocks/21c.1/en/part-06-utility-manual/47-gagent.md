<a id="a22cb176b3b19bea"></a>

# 47. gagent

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/a22cb176b3b19bea)  
> Tag: `21c.1_35_tag`

[← 46. glocator](46-glocator.md) · [Table of contents](../README.md) · [48. gloctl →](48-gloctl.md)

<a id="e9664eeec5227f27"></a>
## Overview of gagent

<a id="699627b3db333051"></a>
### Definition

gagent is a utility communicating with [glocator ](46-glocator.md#be082a202d51c996) by being executed with each member node in GOLDILOCKS cluster system.

When [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#29c2f9aec1f69689) server property value of the node to which gagent belongs is set to 1 or 2, and the connection between nodes is disconnected so the cluster failover is proceeding, then gagent enquires to glocator the validity of the node to which the gagent belongs.  
For more information, refer to [Cluster Failover](46-glocator.md#5788f839398a20db).

<a id="444cb90976aba92f"></a>
### Usage

```
gagent [options]
```

<a id="343d0a99c8c95e9d"></a>
### Options

<a id="ae672fb795a253d9"></a>
#### help

<a id="e2a3cd93d12d9179"></a>
##### Description

It outputs the help message.

<a id="4534fb17aa5adf96"></a>
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

<a id="f77c58d7c4843f6e"></a>
#### start

<a id="c9dc0ddf32f0a59d"></a>
##### Description

It starts gagent. If gagent having the same home directory already has been started, then an error occurs.

<a id="3e0aac921cb3cab8"></a>
##### Example

```
$ gagent --start

gagent is started.
```

<a id="9034d8c6bbd675dd"></a>
#### stop

<a id="7078f7557b3942ed"></a>
##### Description

It stops gagent which is in operation. The same home directory should be set to stop gagent in operation.

<a id="a02aaf6c3df77ffa"></a>
##### Example

```
$ gagent --stop

gagent is stopped.
```

<a id="6174995315d07889"></a>
#### status

<a id="164befa87c6a33d3"></a>
##### Description

It outputs the status message of gagent which is in operation. The same home directory should be set to check the status of gagent in operation.

<a id="cb51d9e9f42e4a86"></a>
##### Example

```
$ gagent --status

gagent(31938) is running.
```

<a id="97ac24d2f44f1625"></a>
#### conf

<a id="abd904c1a9c65606"></a>
##### Description

It sets the configure file when starting gagent.

<a id="303fec1a23708bb7"></a>
##### Example

```
$ gagent --start --conf goldilocks.gagent.conf

gagent is started.
```

<a id="d6801ec54bb591d8"></a>
#### home

<a id="cacedad178619d03"></a>
##### Description

It sets the server home directory of GOLDILOCKS when starting gagent.  
When a relative path is used, it searchs for the home directory based on &lt;GOLDILOCKS_DATA&gt;.  
&lt;GOLDILOCKS_DATA&gt; is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="2d2a4821bb937959"></a>
##### Example

```
$ gagent --start --home g1n1_home --conf goldilocks.gagent.conf  

gagent is started.
```

In the example above, gagent is started by setting &lt;GOLDILOCKS_DATA&gt;/g1n1_home to home.

<a id="c89df4c705b666f0"></a>
#### silent

<a id="467c1e6242bbb0e3"></a>
##### Description

It does not output the message of gagent about the execution.

<a id="033632e37b2c70d3"></a>
##### Example

```
$ gagent --start --silent
```

<a id="3337f8caaa986d77"></a>
#### no-copyright

<a id="d46ee832d23a582c"></a>
##### Description

It does not output the message of gagent's copyright and version about the execution.

<a id="48c131639589520b"></a>
##### Example

```
$ gagent --start --no-copyright

gagent is started.
```

<a id="c8602eb8b7763e3f"></a>
## gagent Configuration

<a id="5f3a12e8a03844d9"></a>
### Configuration File and Environment Variable

gagent can use a file or environment variable to set the configuration.

An environment variable can be set by using the name of which 'AGENT_' is added as a prefix to a configuration property name. For example, setting HOST in the configuration file has the same effect as specifying $AGENT_HOST.

The contents of a configuration file takes precedence over the environment variable setting values.

gagent has $GOLDILOCKS_DATA/conf/goldilocks.gagent.conf file as its environment file. To alter the driving environment of gagent, the file contents should be altered, or gagent should start after setting the environment variables.

<a id="f11f6640e8d816d2"></a>
### Configuration Properties

<a id="79a8312654daded7"></a>
#### HOST

<a id="f7dd53291ac78034"></a>
| Item | Description |
| --- | --- |
| Name | HOST |
| Description | It is an IP address of which gagent binds. |
| Data type | ip address (ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of which gagent binds for UDP communication.  
It uses an IP address in IP v4 form.

<a id="e3aeee99f1c4b29b"></a>
#### REQUEST_PORT

<a id="2168265666134227"></a>
| Item | Description |
| --- | --- |
| Name | REQUEST_PORT |
| Description | It is a port which gagent uses for request. |
| Data type | INT |
| Default value/ range | 43581 / 1024~49151 |

It is a port of which gagent uses to request to glocator during tcp communication.  
The port from 1024 to 49151 can be used.

<a id="29c3356ce9c3d493"></a>
#### RESPONSE_PORT

<a id="35a5abcc0b61bbc6"></a>
| Item | Description |
| --- | --- |
| Name | RESPONSE_PORT |
| Description | It is a port which gagent uses for response. |
| Data type | INT |
| Default value/ range | 43582 / 1024~49151 |

It is a port of which gagent uses to receive the response from glocator during tcp communication.  
The port from 1024 to 49151 can be used.

<a id="9eb7b7d8407af729"></a>
#### LOCATOR_HOST

<a id="c0e5075693fb2071"></a>
| Item | Description |
| --- | --- |
| Name | LOCATOR_HOST |
| Description | It is an IP address of glocator. |
| Data type | ip address(ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of glocator.

<a id="ee39a51a49a422cd"></a>
#### LOCATOR_PORT

<a id="3d7b348d700b4e6f"></a>
| Item | Description |
| --- | --- |
| Name | LOCATOR_PORT |
| Description | It is a port of which glocator waits for Recv. |
| Data type | INT |
| Default value/ range | 42581 / 1024~49151 |

It is the port of glocator of when gagent sends packets to glocator.  
The port from 1024 to 49151 can be used.

<a id="d9d4a7f7013edbbd"></a>
#### SYSTEM_LOGGER_DIR

<a id="8c0fe58da3597bc7"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_LOGGER_DIR |
| Description | It is the directory path of gagent trace log file. |
| Data type | String |
| Default value/ range | &lt;GOLDILOCKS_DATA&gt;/trc |

It is the directory path in which system trace log file of gagent is stored. &lt;GOLDILOCKS_DATA&gt; of the default value is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="ef42d26ddb8e1101"></a>
#### SYSTEM_UDS_DIR

<a id="77680dcd5adb60cd"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_UDS_DIR |
| Description | It is the directory path which stores Unix Domain Socket file of gagent. |
| Data type | String |
| Default value/ range | /tmp (Maximum 50 bytes) |

It is the directory path which stores Unix Domain Socket file of gagent. The default value is /tmp. The directory length can be set up to 50 bytes.

<a id="fdf941d45ac84043"></a>
#### ALTERNATE_LOCATORS

<a id="9ef8548500dc97ef"></a>
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

<a id="0274b87b5d30221b"></a>
#### KEEPALIVE_IDLE_TIME

<a id="66664b078d62d1e0"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_IDLE_TIME |
| Description | tcp keepalive idle time for checking dead client session (sec) |
| Data type | INT |
| Default value/ range | 1 / 1 ~ 16383 |

It is the (idle) duration which the TCP packet is not sent nor is received before sending a keep alive packet. In other words, if TCP packet is not exchanged during the time set in KEEPALIVE_IDLE_TIME, then it performs the keep alive mechanism to detect the dead connection.

<a id="269bdf1436316500"></a>
#### KEEPALIVE_COUNT

<a id="6385c63f39b510c1"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_COUNT |
| Description | tcp keepalive check count |
| Data type | INT |
| Default value/ range | 5 / 1 ~ 10 |

It is the number of performing keep alive mechanism.

<a id="97835228a22f2e93"></a>
#### KEEPALIVE_INTERVAL

<a id="4bd3b2a14e0d6aef"></a>
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
