<a id="5c6d9f818741f0f3"></a>

# 46. glocator

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/5c6d9f818741f0f3)  
> Tag: `21c.1_35_tag`

[← 45. gtrclogger](45-gtrclogger.md) · [Table of contents](../README.md) · [47. gagent →](47-gagent.md)

<a id="be082a202d51c996"></a>
## Overview of glocator

<a id="85d69f6ce5cdd30e"></a>
### Definition

glocator is a utility which provides locations to a client and manages them in GOLDILOCKS cluster system.  
The location information of cluster member nodes is provided to the glocator program through [gloctl](48-gloctl.md#0008ba79a41d8f50).  
glocator communicates with the client and gloctl via UDP, and it communicates with gagent via TCP.

> glocator requires the location information such as a listener host, listener port and db home path, and this information is provided to the glocator through gloctl.

<a id="b3a8b4d8ef8c5c49"></a>
### Usage

```
glocator [options]
```

<a id="4754da865ea13d21"></a>
### Options

<a id="17526bc079cc0bbd"></a>
#### help

<a id="debcdb2bd5cfbcfa"></a>
##### Description

It outputs a help message.

<a id="b495ccade2831be6"></a>
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

<a id="cd4e587128d073f2"></a>
#### create

<a id="fe275b0b0f76be99"></a>
##### Description

It creates the data file of glocator.

<a id="cbefe3bec26e595f"></a>
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

<a id="4e699716de9ec9ee"></a>
#### start

<a id="fe9a6690595daba2"></a>
##### Description

It starts glocator. If glocator having the same port already has started, then an error occurs.

<a id="d9f2eb65f7c403a7"></a>
##### Example

```
$ glocator --start

glocator is started.
```

<a id="733617b38e8cb0e0"></a>
#### stop

<a id="a8a369ac5f405235"></a>
##### Description

It stops glocator which is in operation. The same port should be set to stop glocator in operation.

<a id="742f67579cde8e5a"></a>
##### Example

```
$ glocator --stop

glocator is stopped.
```

<a id="45b3facf84501412"></a>
#### conf

<a id="f5be3ef8140d148b"></a>
##### Description

It sets the configure file when starting glocator.

<a id="9847e5f792c6a6ee"></a>
##### Example

```
$ glocator --start --conf goldilocks.glocator.conf

glocator is started.
```

<a id="f93bdd883dc40469"></a>
#### status

<a id="d24e60a15f7338ca"></a>
##### Description

It outputs the status message of glocator which is in operation. The same port should be set to check the status of glocator in operation.

<a id="4ab92911c3f69837"></a>
##### Example

```
$ glocator --status

Process ID: 26058
Configuration file: goldilocks.glocator.conf
Unix domain path: /tmp/unix-glocator.42581
Udp listen host: 0.0.0.0, Port: 42581
glocator is running.
```

<a id="fbd99ac98a6627d8"></a>
#### sync

<a id="2fb2b2f40491277e"></a>
##### Description

It synchronizes the data of glocator set in ALTERNATE_LOCATORS before driving glocator.

There are two methods for the data synchronization, whichare SOURCE and BOTH. SOURCE method brings data from ALTERNATE_LOCATORS, and BOTH method merges two glocators.

<a id="36209898fc5723a2"></a>
##### Example

The following is an example of a successful use of the sync option with the SOURCE type.

```
$ glocator --start --sync SOURCE

glocator is started.
```

The following is an example of failure of a sync option. The ALTERNATE_LOCATORS property value is not set in the configure file.

```
$ glocator --start --sync SOURCE

ERR-HY000(60016): Need more alternate locator host information.
```

The following is an example of failure of a sync option. glocator set in ALTERNATE_LOCATORS property does not response.

```
$ glocator --start --sync SOURCE

ERR-HY000(60016): Need more alternate locator host information.
```

The following is an example of a failure when no argument is provided for the sync option.

```
$ glocator --start --sync

ERR-HY000(11000): Invalid argument
```

<a id="79379f83db211dff"></a>
#### silent

<a id="e13007d3530d6555"></a>
##### Description

It does not output the message of glocator about the execution.

<a id="75980d3a45b7c375"></a>
##### Example

```
$ glocator --start --silent
```

<a id="0d0e5a78454e066b"></a>
#### no-copyright

<a id="387036ff738467f4"></a>
##### Description

It does not output the message of glocator's copyright and version about the execution.

<a id="7d194e81a6bf125e"></a>
##### Example

```
$ glocator --start --no-copyright

glocator is started.
```

<a id="bf855c6a59144682"></a>
## Using glocator

<a id="4f868e3bb642b396"></a>
### Data File

glocator data file should be created before starting glocator.

```
$ glocator --create

glocator is created.
```

The directory in which glocator data file is stored can be altered by editing configuration [LOCATION_FILE_DIR](#4a380d6ce1cce7f6). The default value is created in &lt;GOLDILOCKS_DATA&gt;/db. The data file can be altered by editing [LOCATION_FILE_NAME](#39acb01769f2f0f4). The default value is glocator.dat.

The maximum size and initial size of glocator data file can be altered by editing configuration [LOCATION_FILE_MAX_SIZE](#27280d5f85b78263)and [LOCATION_FILE_SIZE](#d57ee3ed8f1db875).

<a id="655699b570ea382f"></a>
### CSTARTUP and CSHUTDOWN

glocator can be used to CSTARTUP and CSHUTDOWN the GOLDILOCKS server.  
For that, glocator should be in operation, and CSTARTUP or CSHUTDOWN should be executed through gsqlnet.  
However, LOCATOR_DSN and the property should be set in odbc.ini of the device which executes gsqlnet. For more information, refer to [GOLDILOCKS UNIX ODBC driver libraries](../part-05-developer-manual/31-odbc.md#f37538a6d9eb4e34).

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

<a id="22d6e183f09eb260"></a>
### Replication

<a id="f9264bd8db74e9c6"></a>
#### Overview

glocator replication keeps data consistent, so it enables the stable service through the remote glocator when an error occurs.

<a id="a6591b95c603a503"></a>
#### Configuration

Each glocator should set ALTERNATE_LOCATORS property in a configure file to use the replication feature. Locator_name should be set in ALTERNATE_LOCATORS property and the specified Locator_name should be set in a configure file together with HOST, PORT properties.

The following is how to set ALTERNATE_LOCATORS property.

```
[LOCATOR]
ALTERNATE_LOCATORS = (locator_name1,locator_name2)
[locator_name1]
HOST= ip_address
PORT = port_num
[locator_name2]
HOST= ip_address
PORT = port_num
```

The following is an example of a configure file which sets ALTERNATE_LOCATORS property.

```
[LOCATOR]
PORT=42581
SYNC_RESPONSE_TIMEOUT = 2
SYNC_RETRY_COUNT = 2
LOCATION_FILE_NAME='glocator_1.dat'
ALTERNATE_LOCATORS=(LOCATOR_2,LOCATOR_3)

[LOCATOR_2]
HOST=127.0.0.1
PORT=42582

[LOCATOR_3]
HOST=127.0.0.1
PORT=42583
```


> 
> - [LOCATOR] is DSN which is read as default by glocator.
> - For more information about glocator-related ODBC and how to set gagent, refer to [odbc.ini File](../part-05-developer-manual/31-odbc.md#dd24d6ea4d90d7f1), [ALTERNATE_LOCATORS](47-gagent.md#fdf941d45ac84043).
> 

<a id="bec7c6ad0fda6578"></a>
#### Synchronizing Data

The data should be consistent when the replicated glocator is in service. If glocator in operation does not exist, then all glocator can perform the normal start. If glocator in operation exists, an alternate glocator can be started by synchronizing the data using a [sync](#fbd99ac98a6627d8) option.

[sync](#fbd99ac98a6627d8) option has BOTH and SOURCE. BOTH merges glocator's own data and alternate glocator's data. SOURCE brings the data from the counterpart glocator. The sync operation of glocator is 1 : 1 correspondence task between a glocator and an alternate glocator. Therefore, if A and B are already being operated, and C is operated after syncing by using BOTH for the replication of three (A, B, C) glocators, then the data of A and B glocators may be different.

glocator in service synchronizes only the updated content. If the data synchronization fails due to the packet loss or other reasons, then the data may be different. In this case, update the data within that glocator by using [gloctl](48-gloctl.md#a4f051a64cd67b11) program, or restart glocator with sync option.

<a id="467380496def33e7"></a>
## Features of glocator

<a id="ec395111366d954b"></a>
### Connection Service

It provides a service feature which enables arbitrarily access any node among user-defined nodes even though the location information of a specific node in a cluster environment is unknown.

The service feature is that a user specifies nodes managed by glocator an arbitrary group. This service can be registered by using gloctl program. Service lists managed by glocator can also be viewed by using gloctl program.

An application should be accessed by using ODBC driver, and LOCATOR_DSN and LOCATOR_SERVICE property should be specified in [odbc.ini file](../part-05-developer-manual/31-odbc.md#dd24d6ea4d90d7f1).

<a id="25dbfd128a414eb3"></a>
![locator_service](../assets/images/367e682b7899d0de.png)

The figure above describes that an application accesses to g1n1 belonging to service s3. The connecting sequence of ODBC driver by using the service is as same as the sequence of node registered in the service. If ODBC driver fails to connect to g1n1 in the example above, it will try to connect to the next node g2n1.

> To use the service feature, the valid location information of a node should be input in glocator in advance.

<a id="5788f839398a20db"></a>
### Cluster Failover

glocator is helpful when a server proceeds the failover.

When the value of server property [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#29c2f9aec1f69689) is set to 1 or 2, and connection between nodes is disconnected in a cluster environment, a failover occurs, then each node proceeds the cluster failover and queries its viability to glocator through gagent.

The glocator which received a query determines the viability between two nodes which were disconnected, and transfer the result to the gagent which enquired the query.

Nodes received the viabilty results are terminated or proceeds the failover.

> The cluster failover processing time of the server is relevant to various properties. Server property [LOCATOR_QUERY_TIMEOUT](../part-02-administration-manual/10-server-property.md#dbae42f18a840e40) sets the time waiting for the response after the server enquires to glocator, and the default value is 3 seconds.   
> Server property [CLUSTER_SPLIT_BRAIN_RETRY_COUNT](../part-02-administration-manual/10-server-property.md#a42e52432a379da1) sets the number of enquiring again when glocator does not respond, and it is relevant to the cluster failover processing time. The default value is 1.

<a id="0e2ee669979a5c34"></a>
## glocator Configuration

<a id="bdc386c8f1afaa20"></a>
### Configuration File and Environment Variable

glocator can use a file or environment variable to set the configuration.

An environment variable can be set by using the name of which 'LOCATOR_' is added as a prefix to a configuration property name. For example, setting HOST in the configuration file has the same effect as specifying $LOCATOR_HOST.

The contents of a configuration file takes precedence over the environment variable setting values.

glocator reads the configuration file by reading DSN as the default value of [LOCATOR].

glocator has $GOLDILOCKS_DATA/conf/goldilocks.glocator.conf file as its environment file. To alter the driving environment of glocator, the file contents should be altered, or glocator should start after setting the environment variables.

<a id="6f2b6dbec03bd9c2"></a>
### Configuration Properties

<a id="2353e4f53ecc688f"></a>
#### HOST

<a id="f18a2a6d9532b902"></a>
| Item | Description |
| --- | --- |
| Name | HOST |
| Description | It is an IP address of which glocator binds. |
| Data type | ip address (ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of which glocator binds for UDP communication.  
It uses an IP address in IP v4 form.

<a id="d4172578581de4af"></a>
#### PORT

<a id="22c25bfcd6627e65"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is a port of which glocator waits for Recv. |
| Data type | INT |
| Default value/ range | 42581 / 1024~49151 |

It is a port of which glocator receives a packet through UDP communication.  
The port from 1024 to 49151 can be used.

<a id="7cd92f149b73598b"></a>
#### WORKER_COUNT

<a id="0506af195f4c225d"></a>
| Item | Description |
| --- | --- |
| Name | WORKER_COUNT |
| Description | It is the number of threads processing a job. |
| Data type | INT |
| Default value/ range | 1 / 1~8 |

It is the number of threads processing packets of which glocator received from a client or an internal process.

<a id="c63aea73b97ec18a"></a>
#### MAX_NODE_COUNT

<a id="f48c02e39da37749"></a>
| Item | Description |
| --- | --- |
| Name | MAX_NODE_COUNT |
| Description | It is the maximum number of connectable gagent. |
| Data type | INT |
| Default value/ range | 64 / 1~8192 |

It is the maximum number of connectable gagent.

<a id="76d5d673afe6d000"></a>
#### MESSAGE_QUEUE_SIZE

<a id="cae453a7bf4148f8"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_QUEUE_SIZE |
| Description | It is the queue size in which received packets are stored before processing them. |
| Data type | INT |
| Default value/ range | 33554432 / 10485760~2147483648 |

It is the size of queue of which glocator stores packets received from a client or or an internal process before processing them.  
A packet is stored in a queue as a single item in message unit.

<a id="a6fbdcb6e353a955"></a>
#### MESSAGE_ALLOCATOR_SIZE

<a id="d1a1c07d8865491a"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_ALLOCATOR_SIZE |
| Description | It is the size of an allocator which allocates an item to be stored in a message queue. |
| Data type | INT |
| Default value/ range | 33554432 / 10485760~2147483648 |

It is the size of an allocator which is used to allocate an item (message) to be stored in a message queue.

<a id="c6d8ad4a4dc07f92"></a>
#### PACKET_ALLOCATOR_SIZE

<a id="b8291363db5a4672"></a>
| Item | Description |
| --- | --- |
| Name | PACKET_ALLOCATOR_SIZE |
| Description | It is the size of an allocator which allocates a packet when receiving packets through UDP communication. |
| Data type | INT |
| Default value/ range | 33554432 / 10485760~2147483648 |

It is the size of an allocator for a buffer which is allocated for glocator to receive packets.

<a id="94003ffce5dc0df2"></a>
#### SYSTEM_LOGGER_DIR

<a id="6a2ba28547519224"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_LOGGER_DIR |
| Description | It is the directory path of glocator trace log file. |
| Data type | String |
| Default value/ range | &lt;GOLDILOCKS_DATA&gt;/trc |

It is the directory path in which system trace log file of glocator is stored. &lt;GOLDILOCKS_DATA&gt; of the default value is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="6900c48a08777104"></a>
#### SYSTEM_UDS_DIR

<a id="bc03921ccc374c19"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_UDS_DIR |
| Description | It is the directory path in which unix domain socket file used in glocator is stored. |
| Data type | String |
| Default value/ range | /tmp (Maximum 60 byte) |

It sets the directory path in which the unix domain socket file used in glocator is stored. The maximum length of the directory should be set within 60 bytes.

<a id="4a380d6ce1cce7f6"></a>
#### LOCATION_FILE_DIR

<a id="3501924128ab0266"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_DIR |
| Description | It is the directory path in which the location file used in glocator is stored. |
| Data type | String |
| Default value/ range | &lt;GOLDILOCKS_DATA&gt;/db |

It sets the directory path in which the location file used in glocator is stored.

<a id="39acb01769f2f0f4"></a>
#### LOCATION_FILE_NAME

<a id="3317bab99b681e98"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_NAME |
| Description | It is the name of a location file which is used in glocator. |
| Data type | String |
| Default value/ range | glocator.dat |

It sets the name of a location file which is used in glocator.  
The default value is glocator.dat.

<a id="d57ee3ed8f1db875"></a>
#### LOCATION_FILE_SIZE

<a id="c72224e2f532fbb6"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_SIZE |
| Description | It is the initial size of a location file. |
| Data type | Int |
| Default value/ range | 1048576 / 104576~2147483648 |

It sets the initial size of a location file used in glocator.

<a id="27280d5f85b78263"></a>
#### LOCATION_FILE_MAX_SIZE

<a id="9abca451e573e3fc"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_MAX_SIZE |
| Description | It is the maximum size of a location file. |
| Data type | Int |
| Default value/ range | 10485760 / 104576~2147483648 |

It sets the maximum size of a location file used in glocator.

<a id="d8c82e9522bb391a"></a>
#### MESSAGE_TIMEOUT

<a id="a3c209b318821111"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_TIMEOUT |
| Description | It sets the maximum time for glocator to wait to receive packets. |
| Data type | Int |
| Default value/ range | 100 / 0 ~2147483648(unit: seconds) |

It sets the maximum time (seconds) for glocator to wait to receive packets. Packets exceeds the maximum time without being processed, are dumped.

<a id="bbf4e71c0688820f"></a>
#### ALTERNATE_LOCATORS

<a id="045828d86e200ab0"></a>
| Item | Description |
| --- | --- |
| Name | ALTERNATE_LOCATORS |
| Description | It sets an alternate locator and replication of glocator. |
| Data type | String |
| Default value/ range | empty / 0 ~ 1024 bytes |

It sets [Replication](#22d6e183f09eb260) of glocator.

<a id="083eb4a70e620435"></a>
#### SYNC_RETRY_COUNT

<a id="6ad8f379a8fab2d0"></a>
| Item | Description |
| --- | --- |
| Name | SYNC_RETRY_COUNT |
| Description | It sets the number of retry when glocator fails to synchronize with an alternate locator. |
| Data type | Int |
| Default value/ range | 1 / 0 ~ 5 |

It sets the number of redelivery of glocator synchronization.

glocator transfers the altered data to alternate locator when the data is altered, and it transfers the data again when it could not get any response.

<a id="8e53166695fe1bfe"></a>
#### SYNC_RESPONSE_TIMEOUT

<a id="39c6ab1372e4be68"></a>
| Item | Description |
| --- | --- |
| Name | SYNC_RESPONSE_TIMEOUT |
| Description | It sets the time waits for the response for the synchronization of glocator. |
| Data type | Int |
| Default value/ range | 5 / 1 ~ 20 |

It sets the time waits for the response for the synchronization data transferred from glocator.

<a id="4fa19641583a42f0"></a>
#### KEEPALIVE_IDLE_TIME

<a id="1cfb6f3fd4beafac"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_IDLE_TIME |
| Description | tcp keepalive idle time for checking dead client session (sec) |
| Data type | INT |
| Default value/ range | 1 / 1 ~ 16383 |

It is the (idle) duration which the TCP packet is not sent nor is received before sending a keep alive packet. In other words, if TCP packet is not exchanged during the time set in KEEPALIVE_IDLE_TIME, then it performs the keep alive mechanism to detect the dead connection.

<a id="4b8a212d8f54fa27"></a>
#### KEEPALIVE_COUNT

<a id="1f6fd44dd4f4d17f"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_COUNT |
| Description | tcp keepalive check count |
| Data type | INT |
| Default value/ range | 5 / 1 ~ 10 |

It is the number of performing keep alive mechanism.

<a id="580ee73216023018"></a>
#### KEEPALIVE_INTERVAL

<a id="e66589fc5eeba9ff"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_INTERVAL |
| Description | tcp keepalive packet interval (sec) |
| Data type | INT |
| Default value/ range | 5 |

It is the time interval to send the keep alive packet.

---

[← 45. gtrclogger](45-gtrclogger.md) · [Table of contents](../README.md) · [47. gagent →](47-gagent.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
