<a id="9d0108928f78c3cd"></a>

# 51. glocator

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/9d0108928f78c3cd)  
> Tag: `26c.1_0_tag`

[← 50. gtrclogger](50-gtrclogger.md) · [Table of contents](../README.md) · [52. gagent →](52-gagent.md)

<a id="0e0291a55963f28e"></a>
## Overview of glocator

<a id="cbd7ba0b7e6c5861"></a>
### Definition

glocator is a utility which provides locations to a client and manages them in GOLDILOCKS cluster system.  
The location information of cluster member nodes is provided to the glocator program through [gloctl](53-gloctl.md#1863208c2c2b4d41).  
glocator communicates with the client and gloctl via UDP, and it communicates with gagent via TCP.

> glocator requires the location information such as a listener host, listener port and db home path, and this information is provided to the glocator through gloctl.

<a id="f33f5fa91c3b623c"></a>
### Usage

```
glocator [options]
```

<a id="e39563759ade98ba"></a>
### Options

<a id="c9f3ff7d72f5bf63"></a>
#### help

<a id="0ee911f4ea4cd477"></a>
##### Description

It outputs a help message.

<a id="0908cbefa7177e66"></a>
##### Example

```
$ glocator --help

Usage:
 glocator [options]

Options:

-c  --create       Create glocator environment
-s  --start        Start glocator
-t  --stop         Stop glocator
-f  --conf         Set configure file
-u  --status       Get glocator status
-l  --silent       Suppress display message
-r  --no-copyright Suppress display copy right and version
-h  --help         Print help message
```

<a id="979c23d88de27ef1"></a>
#### create

<a id="3be4e0d834a8346c"></a>
##### Description

It creates the data file of glocator.

<a id="ebdcf6e60010546f"></a>
##### Example

```
$ glocator --create

glocator is created.
```

> The data file of glocator is created in &lt;GOLDILOCKS_DATA&gt;/db directory.

```
$ ls
README  glocator.dat  system_data.dbf  system_dict.dbf  system_undo.dbf
```

<a id="6595689ab894e52f"></a>
#### start

<a id="1ffb8d5ee8922f58"></a>
##### Description

It starts glocator. If glocator having the same port already has started, then an error occurs.

<a id="bd01db7f06b50de7"></a>
##### Example

```
$ glocator --start

glocator is started.
```

<a id="b3fe852ffa6aa59d"></a>
#### stop

<a id="c5b92f66ffd6a30f"></a>
##### Description

It stops glocator which is in operation. The same port should be set to stop glocator in operation.

<a id="322e58f6c80d9bec"></a>
##### Example

```
$ glocator --stop

glocator is stopped.
```

<a id="ac0fa59cb8a068d3"></a>
#### conf

<a id="c77fcffefae93682"></a>
##### Description

It sets the configure file when starting glocator.

<a id="1caa2ae5078a3120"></a>
##### Example

```
$ glocator --start --conf goldilocks.glocator.conf

glocator is started.
```

<a id="ebc68f52774c7db0"></a>
#### status

<a id="468fc129520346ae"></a>
##### Description

It outputs the status message of glocator which is in operation. The same port should be set to check the status of glocator in operation.

<a id="4f11e8c3b050b3a7"></a>
##### Example

```
$ glocator --status

Process ID: 26058
Configuration file: goldilocks.glocator.conf
Unix domain path: /tmp/unix-glocator.42581
Udp listen host: 0.0.0.0, Port: 42581
glocator is running.
```

<a id="7d9d648f19eea72e"></a>
#### sync

<a id="a48e855c2ed38c6f"></a>
##### Description

It connects with ALTERNATE_LOCATOR and synchronizes the data.

Data synchronization merges the data of two glocators, and in the event of a conflict, the more recent data is selected based on the creation time.

<a id="bbbfc03e04e700df"></a>
##### Example

The following is an example of using the sync option.

```
$ glocator --start --sync

glocator is started.
```

The following is an example of failure of a sync option. The ALTERNATE_LOCATOR property value is not set in the configure file.

```
$ glocator --start --sync

ERR-HY000(60016): Need more alternate locator host information.
```

<a id="9e866a5108eaeb7a"></a>
#### silent

<a id="fe2d66ee00c91f7f"></a>
##### Description

It does not output the message of glocator about the execution.

<a id="8da753bff2c34527"></a>
##### Example

```
$ glocator --start --silent
```

<a id="32b9f91e1b157cab"></a>
#### no-copyright

<a id="935773819e25c961"></a>
##### Description

It does not output the message of glocator's copyright and version about the execution.

<a id="ab7a5a8c8ca719e4"></a>
##### Example

```
$ glocator --start --no-copyright

glocator is started.
```

<a id="aa1379246cb503b7"></a>
## Using glocator

<a id="507a6f4ae17435fe"></a>
### Data File

glocator data file should be created before starting glocator.

```
$ glocator --create

glocator is created.
```

The directory in which glocator data file is stored can be altered by editing configuration [LOCATION_FILE_DIR](#b13e3878c9e8d599). The default value is created in &lt;GOLDILOCKS_DATA&gt;/db. The data file can be altered by editing [LOCATION_FILE_NAME](#c169d071c552bcef). The default value is glocator.dat.

The maximum size and initial size of glocator data file can be altered by editing configuration [LOCATION_FILE_MAX_SIZE](#5915e2becb31c698)and [LOCATION_FILE_SIZE](#64bb988fd5715b44).

<a id="2669a328626f7c4e"></a>
### CSTARTUP and CSHUTDOWN

glocator can be used to CSTARTUP and CSHUTDOWN the GOLDILOCKS server.  
For that, glocator should be in operation, and CSTARTUP or CSHUTDOWN should be executed through gsqlnet.  
However, LOCATOR_DSN and the property should be set in odbc.ini of the device which executes gsqlnet. For more information, refer to [GOLDILOCKS UNIX ODBC driver libraries](../part-05-developer-manual/34-odbc.md#7eea426ebb5fbf19).

The following contents is set in odbc.ini to use glocator.

```
[GOLDILOCKS]
HOST=127.0.0.1
PORT=20101
UID=sys
PWD=gliese
LOCATOR_DSN=GLOCATOR

[GLOCATOR]
HOST=127.0.0.1
PORT=42581
```

> If FILE property exists in DSN [GLOCATOR], then the file specified in FILE property takes precedence instead of using glocator. Therefore, FILE property should be excluded.

glocator should know the location information of member nodes to execute CSTARTUP and CSHUTDOWN.

<a id="c043ba4461eaa7aa"></a>
### Replication

<a id="555faabcabdea395"></a>
#### Overview

glocator replication ensures data consistency, allowing for stable service through the remote glocator in the event of an error during operation.

<a id="dd16a1a7205960de"></a>
#### Configuration

To use replication, the ALTERNATE_LOCATOR property must be set in the configuration file. This property should specify the locator name, which must also exist in the configuration file along with the HOST and PORT properties. The master glocator is not required to define the ALTERNATE_LOCATOR property; however, if it is defined, it must match the HOST and PORT properties of the sub glocator.

The following is how to set ALTERNATE_LOCATOR property.

```
[LOCATOR]
ALTERNATE_LOCATOR = locator_name1
[locator_name1]
HOST= ip_address
PORT = port_num
```

The following is an example of a configure file which sets ALTERNATE_LOCATOR property.

```
[LOCATOR]
PORT=42581
SYNC_RESPONSE_TIMEOUT = 2
SYNC_RETRY_COUNT = 2
LOCATION_FILE_NAME='glocator_1.dat'
ALTERNATE_LOCATOR=LOCATOR_2

[LOCATOR_2]
HOST=127.0.0.1
PORT=42582
```


> 
> - [LOCATOR] is DSN which is read as default by glocator.
> - For more information about glocator-related ODBC and how to set gagent, refer to [odbc.ini File](../part-05-developer-manual/34-odbc.md#a37d4e15f0c71e92), [ALTERNATE_LOCATOR](52-gagent.md#bb1e499f25842748).
> 

<a id="f14cd71b41a5af75"></a>
#### Synchronizing Data

The data should be consistent when the replicated glocator is in service. If glocator in operation does not exist, then all glocator can perform the normal start. If glocator in operation exists, an alternate glocator can be started by synchronizing the data using a [sync](#7d9d648f19eea72e) option.

The [sync](#7d9d648f19eea72e) option merges the data of the two glocators. Any conflicting duplicate data is overwritten by the newly updated data.

When data changes during the glocator service, it attempts to synchronize the data. However, if synchronization fails due to reasons such as packet loss, discrepancies may arise between the datasets. In this case, use the [gloctl](53-gloctl.md#1863208c2c2b4d41) program to directly modify the data on the affected glocator or restart the glocator with the sync option.

<a id="89e2634891c49a74"></a>
#### Replication and gagent

glocator replication is categorized into master and sub (substitute). This distinction is determined by their startup order. A later-started sub glocator must use the [sync](#7d9d648f19eea72e) option to connect with the previously started master glocator.

The gagent must always connect to the master. This is to prevent the gagent from being distributed. If the glocator that the gagent is trying to connect to is a sub, the connection will be terminated, and it will adjust to connect to the master.

<a id="562ce2d71dc2be89"></a>
## Features of glocator

<a id="ae1f9b7769ef1776"></a>
### Connection Service

It provides a service feature which enables arbitrarily access any node among user-defined nodes even though the location information of a specific node in a cluster environment is unknown.

The service feature is that a user specifies nodes managed by glocator an arbitrary group. This service can be registered by using gloctl program. Service lists managed by glocator can also be viewed by using gloctl program.

An application should be accessed by using ODBC driver, and LOCATOR_DSN and LOCATOR_SERVICE property should be specified in [odbc.ini file](../part-05-developer-manual/34-odbc.md#a37d4e15f0c71e92).

<a id="5776068bacafe336"></a>
![locator_service](../assets/images/52849528da8de1b7.png)

The figure above describes that an application accesses to g1n1 belonging to service s3. The connecting sequence of ODBC driver by using the service is the same as the sequence of node registered in the service. If ODBC driver fails to connect to g1n1 in the example above, it will try to connect to the next node g2n1.

> To use the service feature, the valid location information of a node should be input in glocator in advance.

<a id="e6961f973f6c391e"></a>
### Cluster Failover

glocator is helpful when a server proceeds the failover.

When the value of server property [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#77027a79e36b9077) is set to 1 or 2, and connection between nodes is disconnected in a cluster environment, a failover occurs, then each node proceeds the cluster failover and queries its viability to glocator through gagent.

The glocator which received a query determines the viability between two nodes which were disconnected, and transfer the result to the gagent which enquired the query.

Nodes received the viabilty results are terminated or proceeds the failover.

> The cluster failover processing time of the server is relevant to various properties. Server property [LOCATOR_QUERY_TIMEOUT](../part-02-administration-manual/10-server-property.md#1efe52fc87229d75) sets the time waiting for the response after the server enquires to glocator, and the default value is 20 seconds.   
> Server property [CLUSTER_SPLIT_BRAIN_RETRY_COUNT](../part-02-administration-manual/10-server-property.md#e6891e5f0a93f43b) sets the number of enquiring again when glocator does not respond, and it is relevant to the cluster failover processing time. The default value is 1.

<a id="abfaae046b10dd0e"></a>
## glocator Configuration

<a id="8bb153595de8d449"></a>
### Configuration File and Environment Variable

glocator can use a file or environment variable to set the configuration.

An environment variable can be set by using the name of which 'LOCATOR_' is added as a prefix to a configuration property name. For example, setting HOST in the configuration file has the same effect as specifying $LOCATOR_HOST.

The contents of a configuration file takes precedence over the environment variable setting values.

glocator reads the configuration file by reading DSN as the default value of [LOCATOR].

glocator has $GOLDILOCKS_DATA/conf/goldilocks.glocator.conf file as its environment file. To alter the driving environment of glocator, the file contents should be altered, or glocator should start after setting the environment variables.

<a id="aa7624bce423dd8b"></a>
### Configuration Properties

<a id="a3976413ec584203"></a>
#### HOST

<a id="e4f221d8306094c2"></a>
| Item | Description |
| --- | --- |
| Name | HOST |
| Description | It is an IP address of which glocator binds. |
| Data type | ip address (ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of which glocator binds for UDP communication.  
It uses an IP address in IP v4 form.

<a id="69b83be330cb1c0b"></a>
#### PORT

<a id="69368f6c71bc7f6d"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is a port of which glocator waits for Recv. |
| Data type | INT |
| Default value/ range | 42581 / 1024~49151 |

It is a port of which glocator receives a packet through UDP communication.  
The port from 1024 to 49151 can be used.

<a id="b4ec62b9281709d0"></a>
#### WORKER_COUNT

<a id="e6c2c368606d2cb7"></a>
| Item | Description |
| --- | --- |
| Name | WORKER_COUNT |
| Description | It is the number of threads processing a job. |
| Data type | INT |
| Default value/ range | 1 / 1~8 |

It is the number of threads processing packets of which glocator received from a client or an internal process.

<a id="c8bb8340e9049bff"></a>
#### MAX_NODE_COUNT

<a id="284d3e066ceb0672"></a>
| Item | Description |
| --- | --- |
| Name | MAX_NODE_COUNT |
| Description | It is the maximum number of connectable gagent. |
| Data type | INT |
| Default value/ range | 64 / 1~8192 |

It is the maximum number of connectable gagent.

<a id="99eb46224c9579a7"></a>
#### MESSAGE_QUEUE_SIZE

<a id="e08c30d7c438184c"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_QUEUE_SIZE |
| Description | It is the queue size in which received packets are stored before processing them. |
| Data type | INT |
| Default value/ range | 33554432 / 10485760~2147483648 |

It is the size of queue of which glocator stores packets received from a client or or an internal process before processing them.  
A packet is stored in a queue as a single item in message unit.

<a id="6efacf85159d5d34"></a>
#### MESSAGE_ALLOCATOR_SIZE

<a id="1f0caefc2a5d19a0"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_ALLOCATOR_SIZE |
| Description | It is the size of an allocator which allocates an item to be stored in a message queue. |
| Data type | INT |
| Default value/ range | 33554432 / 10485760~2147483648 |

It is the size of an allocator which is used to allocate an item (message) to be stored in a message queue.

<a id="d38a0c2917a442e9"></a>
#### PACKET_ALLOCATOR_SIZE

<a id="0f1acf8a1dbedae6"></a>
| Item | Description |
| --- | --- |
| Name | PACKET_ALLOCATOR_SIZE |
| Description | It is the size of an allocator which allocates a packet when receiving packets through UDP communication. |
| Data type | INT |
| Default value/ range | 33554432 / 10485760~2147483648 |

It is the size of an allocator for a buffer which is allocated for glocator to receive packets.

<a id="228358a720a189fc"></a>
#### SYSTEM_LOGGER_DIR

<a id="117d153f2710189b"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_LOGGER_DIR |
| Description | It is the directory path of glocator trace log file. |
| Data type | String |
| Default value/ range | &lt;GOLDILOCKS_DATA&gt;/trc |

It is the directory path in which system trace log file of glocator is stored. &lt;GOLDILOCKS_DATA&gt; of the default value is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="03b0b377adaffce8"></a>
#### SYSTEM_UDS_DIR

<a id="58806806620fd52e"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_UDS_DIR |
| Description | It is the directory path in which unix domain socket file used in glocator is stored. |
| Data type | String |
| Default value/ range | /tmp (Maximum 60 byte) |

It sets the directory path in which the unix domain socket file used in glocator is stored. The maximum length of the directory should be set within 60 bytes.

<a id="b13e3878c9e8d599"></a>
#### LOCATION_FILE_DIR

<a id="92313d0946af92c3"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_DIR |
| Description | It is the directory path in which the location file used in glocator is stored. |
| Data type | String |
| Default value/ range | &lt;GOLDILOCKS_DATA&gt;/db |

It sets the directory path in which the location file used in glocator is stored.

<a id="c169d071c552bcef"></a>
#### LOCATION_FILE_NAME

<a id="46a362a1a774872e"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_NAME |
| Description | It is the name of a location file which is used in glocator. |
| Data type | String |
| Default value/ range | glocator.dat |

It sets the name of a location file which is used in glocator.  
The default value is glocator.dat.

<a id="64bb988fd5715b44"></a>
#### LOCATION_FILE_SIZE

<a id="00da7ca1901d1c5b"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_SIZE |
| Description | It is the initial size of a location file. |
| Data type | Int |
| Default value/ range | 1048576 / 104576~2147483648 |

It sets the initial size of a location file used in glocator.

<a id="5915e2becb31c698"></a>
#### LOCATION_FILE_MAX_SIZE

<a id="0bbda87f302e8150"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_MAX_SIZE |
| Description | It is the maximum size of a location file. |
| Data type | Int |
| Default value/ range | 10485760 / 104576~2147483648 |

It sets the maximum size of a location file used in glocator.

<a id="0fc619ead127ddbb"></a>
#### MESSAGE_TIMEOUT

<a id="e6892f53a6ef5013"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_TIMEOUT |
| Description | It sets the maximum time for glocator to wait to receive packets. |
| Data type | Int |
| Default value/ range | 100 / 0 ~2147483648(unit: seconds) |

It sets the maximum time (seconds) for glocator to wait to receive packets. Packets exceeds the maximum time without being processed, are dumped.

<a id="3c94efd1ba6aa60b"></a>
#### ALTERNATE_LOCATOR

<a id="b854c970322a109e"></a>
| Item | Description |
| --- | --- |
| Name | ALTERNATE_LOCATOR |
| Description | It sets an alternate locator and replication of glocator. |
| Data type | String |
| Default value/ range | empty / 0 ~ 1024 bytes |

It sets [Replication](#c043ba4461eaa7aa) of glocator.

<a id="e62a6dedfb79c6e8"></a>
#### SYNC_RETRY_COUNT

<a id="f26a9949265764f1"></a>
| Item | Description |
| --- | --- |
| Name | SYNC_RETRY_COUNT |
| Description | It sets the number of retry when glocator fails to synchronize with an alternate locator. |
| Data type | Int |
| Default value/ range | 1 / 0 ~ 5 |

It sets the number of redelivery of glocator synchronization.

glocator transfers the altered data to alternate locator when the data is altered, and it transfers the data again when it could not get any response.

<a id="1f6a49aec1617e63"></a>
#### SYNC_RESPONSE_TIMEOUT

<a id="9c7ab0925eb20a0b"></a>
| Item | Description |
| --- | --- |
| Name | SYNC_RESPONSE_TIMEOUT |
| Description | It sets the time waits for the response for the synchronization of glocator. |
| Data type | Int |
| Default value/ range | 5 / 1 ~ 20 |

It sets the time waits for the response for the synchronization data transferred from glocator.

<a id="6459409dfa4fbbea"></a>
#### KEEPALIVE_IDLE_TIME

<a id="7a0d43482dc2ff76"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_IDLE_TIME |
| Description | tcp keepalive idle time for checking dead client session (sec) |
| Data type | INT |
| Default value/ range | 1 / 1 ~ 16383 |

It is the (idle) duration which the TCP packet is not sent nor is received before sending a keep alive packet. In other words, if TCP packet is not exchanged during the time set in KEEPALIVE_IDLE_TIME, then it performs the keep alive mechanism to detect the dead connection.

<a id="82d30c8756af813b"></a>
#### KEEPALIVE_COUNT

<a id="40b27b0ea0298cbc"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_COUNT |
| Description | tcp keepalive check count |
| Data type | INT |
| Default value/ range | 5 / 1 ~ 10 |

It is the number of performing keep alive mechanism.

<a id="2f990537bcec077e"></a>
#### KEEPALIVE_INTERVAL

<a id="063223b19b8bcbfc"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_INTERVAL |
| Description | tcp keepalive packet interval (sec) |
| Data type | INT |
| Default value/ range | 5 |

It is the time interval to send the keep alive packet.

---

[← 50. gtrclogger](50-gtrclogger.md) · [Table of contents](../README.md) · [52. gagent →](52-gagent.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
