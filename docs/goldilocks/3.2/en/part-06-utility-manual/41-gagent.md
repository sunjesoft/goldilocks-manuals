<a id="c2ee11cb474f773f"></a>

# 41. gagent

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/c2ee11cb474f773f)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 40. glocator](40-glocator.md) · [Table of contents](../README.md) · [42. gloctl →](42-gloctl.md)

<a id="95406be694697639"></a>
## Overview of gagent

<a id="1a4e4de3aed981cf"></a>
### Definition

gagent is a utility communicating with [glocator ](40-glocator.md#787a6a38e78fc2e9) by being executed with each member node in GOLDILOCKS cluster system.

> gagent can provide location information of a local node to glocator. For the consistency of location information, glocator should be executed ahead of gagent.

<a id="8fa326de8179494f"></a>
### Usage

```
gagent [options]
```

<a id="d174e0c86d3df726"></a>
### Options

<a id="240b22cf0ae688c9"></a>
#### help

<a id="528c3434b31f0fe5"></a>
##### Description

It outputs the help message.

<a id="d84e4a722c169e67"></a>
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

<a id="02d0b93ffffcc68c"></a>
#### start

<a id="f1c5efbe07f9b20b"></a>
##### Description

It starts gagent. If gagent having the same home directory already has been started, then an error occurs.

<a id="2246896a379a4f8a"></a>
##### Example

```
$ gagent --start

gagent is started.
```

<a id="1c750c65b91e9da7"></a>
#### stop

<a id="2d2550fabc38352e"></a>
##### Description

It stops gagent which is in operation. The same home directory should be set to stop gagent in operation.

<a id="610a27b7ff1c6b0d"></a>
##### Example

```
$ gagent --stop

gagent is stopped.
```

<a id="3760a444781416d4"></a>
#### status

<a id="cb708df11006bc45"></a>
##### Description

It outputs the status message of gagent which is in operation. The same home directory should be set to check the status of gagent in operation.

<a id="702c0be6dd632e93"></a>
##### Example

```
$ gagent --status

gagent(31938) is running.
```

<a id="9497a25bf76a072e"></a>
#### conf

<a id="c9a61260080b159c"></a>
##### Description

It sets the configure file when starting gagent.

<a id="7346f35cc1283baa"></a>
##### Example

```
$ gagent --start --conf goldilocks.gagent.conf

gagent is started.
```

<a id="d969e4f083ccaa8d"></a>
#### home

<a id="1e1e2cc472dd85e5"></a>
##### Description

It sets the server home directory of GOLDILOCKS when starting gagent.  
When a relative path is used, it searchs for the home directory based on &lt;GOLDILOCKS_DATA&gt;.  
&lt;GOLDILOCKS_DATA&gt; is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="1dd6d9da7816c49c"></a>
##### Example

```
$ gagent --start --home g1n1_home --conf goldilocks.gagent.conf  

gagent is started.
```

In the example above, gagent is started by setting &lt;GOLDILOCKS_DATA&gt;/g1n1_home to home.

<a id="a59750f4d37a6a53"></a>
#### silent

<a id="032cce4162b1dd9a"></a>
##### Description

It does not output the message of gagent about the execution.

<a id="afd6000c53853ff1"></a>
##### Example

```
$ gagent --start --silent
```

<a id="f27d384e647e838b"></a>
#### no-copyright

<a id="47b860deca9894b1"></a>
##### Description

It does not output the message of gagent's copyright and version about the execution.

<a id="d29f13465d42d85a"></a>
##### Example

```
$ gagent --start --no-copyright

gagent is started.
```

<a id="b6e3c72396264d1c"></a>
## gagent Configuration

<a id="d6f772893436a1da"></a>
### Configuration File and Environment Variable

gagent can use a file or environment variable to set the configuration.

An environment variable can be set by using the name of which 'AGENT_' is added as a prefix to a configuration property name. For example, setting HOST in the configuration file has the same effect as specifying $AGENT_HOST.

The contents of a configuration file takes precedence over the environment variable setting values.

gagent has $GOLDILOCKS_DATA/conf/goldilocks.gagent.conf file as its environment file. To alter the driving environment of gagent, the file contents should be altered, or gagent should start after setting the environment variables.

<a id="5241e63aa2a74c86"></a>
### Configuration Properties

<a id="1e5791df670a8ab9"></a>
#### HOST

<a id="f9b0f20054f3368b"></a>
| Item | Description |
| --- | --- |
| Name | HOST |
| Description | It is an IP address of which gagent binds. |
| Data type | ip address (ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of which gagent binds for UDP communication.  
It uses an IP address in IP v4 form.

<a id="4af2456f6f7f683e"></a>
#### PORT

<a id="2f559785b04ce651"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is a port of which gagent waits for Recv. |
| Data type | INT |
| Default value/ range | 43581 / 1024~49151 |

It is a port of which gagent receives a packet through UDP communication.  
The port from 1024 to 49151 can be used.

<a id="0a2277931d96f3fa"></a>
#### LOCATOR_HOST

<a id="699b190d6f51e377"></a>
| Item | Description |
| --- | --- |
| Name | LOCATOR_HOST |
| Description | It is an IP address of glocator. |
| Data type | ip address(ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of glocator.

<a id="59abe9c11c29d2f1"></a>
#### LOCATOR_PORT

<a id="e8797014a28d4938"></a>
| Item | Description |
| --- | --- |
| Name | LOCATOR_PORT |
| Description | It is a port of which glocator waits for Recv. |
| Data type | INT |
| Default value/ range | 42581 / 1024~49151 |

It is the port of glocator of when gagent sends packets to glocator.  
The port from 1024 to 49151 can be used.

<a id="7d4c22afe0306592"></a>
#### COMMAND_QUEUE_SIZE

<a id="e6a75b45b03f7d6a"></a>
| Item | Description |
| --- | --- |
| Name | COMMAND_QUEUE_SIZE |
| Description | It is the queue size in which received packets are stored before processing them. |
| Data type | INT |
| Default value/ range | 1048576 / 1048576~2147483648 |

It is the size of queue of which gagent stores packets received from glocator before processing them.  
Packets are stored as an item of a command unit in a queue.

<a id="62ae0f2a72467abb"></a>
#### COMMAND_ALLOCATOR_SIZE

<a id="20d8200b99ed2d71"></a>
| Item | Description |
| --- | --- |
| Name | COMMAND_ALLOCATOR+SIZE |
| Description | It is the size of an allocator which allocates an item to be stored in a command queue. |
| Data type | INT |
| Default value/ range | 1048576 / 1048576~2147483648 |

It is the size of an allocator which is used to allocate an item (command) to be stored in a command queue.

<a id="a43c76280772d685"></a>
#### PACKET_ALLOCATOR_SIZE

<a id="8a73e73220fb4fbf"></a>
| Item | Description |
| --- | --- |
| Name | PACKET_ALLOCATOR+SIZE |
| Description | It is the size of an allocator which allocates a packet when receiving packets through UDP communication. |
| Data type | INT |
| Default value/ range | 1048576 / 1048576~2147483648 |

It is the size of an allocator for a buffer which is allocated for gagent to receive packets.

<a id="4ae5e042e5d8d705"></a>
#### SYSTEM_LOGGER_DIR

<a id="74ac7f6f927bf638"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_LOGGER_DIR |
| Description | It is the directory path of gagent trace log file. |
| Data type | String |
| Default value/ range | '&lt;GOLDILOCKS_DATA&gt;/trc' |

It is the directory path in which system trace log file of gagent is stored. &lt;GOLDILOCKS_DATA&gt; of the default value is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="4e4cdb74802cb85d"></a>
#### UPDATE_LOCATION_TIME

<a id="df1a536396a84b42"></a>
| Item | Description |
| --- | --- |
| Name | UPDATE_LOCATION_TIME |
| Description | It sets the cycle for gagent to update its location information to glocator. |
| Data type | Int |
| Default value/ range | 120 / 30~2147483648 (second unit) |

It sets the cycle for gagent to update its node location information to glocator.

<a id="4c7c845cd606c428"></a>
#### SESSION_TIMEOUT

<a id="25d2021c13f12ddd"></a>
| Item | Description |
| --- | --- |
| Name | SESSION_TIMEOUT |
| Description | It sets the maximum time for gagent to wait to receive packets. |
| Data type | Int |
| Default value/ range | 60 / 0 ~2147483648 (second unit) |

It sets the maximum time (seconds) for gagent to wait to receive packets. Packets exceeds the maximum time without being processed, are dumped.

<a id="8756177d001cb056"></a>
#### ALTERNATE_LOCATORS

<a id="866d4bbd0e1d957b"></a>
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
ALTERNATE_LOCATORS='LOCATOR1,LOCATOR2'

[LOCATOR1]
HOST=127.0.0.1
PORT=42582

[LOCATOR2]
HOST=127.0.0.1
PORT=42583
```

---

[← 40. glocator](40-glocator.md) · [Table of contents](../README.md) · [42. gloctl →](42-gloctl.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
