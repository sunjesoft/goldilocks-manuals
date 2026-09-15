<a id="450832b1e88fed4c"></a>

# 46. glocator

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/450832b1e88fed4c)  
> Tag: `22c.1_10_tag`

[← 45. gtrclogger](45-gtrclogger.md) · [Table of contents](../README.md) · [47. gagent →](47-gagent.md)

<a id="4e23705d562834a7"></a>
## Overview of glocator

<a id="3f0e49cf36a3bc26"></a>
### Definition

glocator is a utility which provides locations to a client and manages them in GOLDILOCKS cluster system.  
The location information of cluster member nodes is provided to the glocator program through [gloctl](48-gloctl.md#aea8168e0da011e1).  
glocator communicates with the client and gloctl via UDP, and it communicates with gagent via TCP.

> glocator requires the location information such as a listener host, listener port and db home path, and this information is provided to the glocator through gloctl.

<a id="590c1bedfc565838"></a>
### Usage

```
glocator [options]
```

<a id="76ab22b1d2932ef6"></a>
### Options

<a id="08bfe53f46956ee9"></a>
#### help

<a id="cd08e6526b572c8c"></a>
##### Description

It outputs a help message.

<a id="b113479935de7024"></a>
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

<a id="068ea20eef879254"></a>
#### create

<a id="d2c119ecf3ce1dce"></a>
##### Description

It creates the data file of glocator.

<a id="dff90aa7e4d10a4b"></a>
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

<a id="2a96e4179bd50d94"></a>
#### start

<a id="186c23ce9cb01718"></a>
##### Description

It starts glocator. If glocator having the same port already has started, then an error occurs.

<a id="ac19b3a04d23765d"></a>
##### Example

```
$ glocator --start

glocator is started.
```

<a id="d7abb554a5bd0220"></a>
#### stop

<a id="78e5be815a8f9b39"></a>
##### Description

It stops glocator which is in operation. The same port should be set to stop glocator in operation.

<a id="771f5554cf57fc20"></a>
##### Example

```
$ glocator --stop

glocator is stopped.
```

<a id="a6302fd3ac0dd455"></a>
#### conf

<a id="fc9e22dbfa201619"></a>
##### Description

It sets the configure file when starting glocator.

<a id="bf2fa99af70fe5d7"></a>
##### Example

```
$ glocator --start --conf goldilocks.glocator.conf

glocator is started.
```

<a id="cd11e989be430cc0"></a>
#### status

<a id="5bbfb9becb3f832b"></a>
##### Description

It outputs the status message of glocator which is in operation. The same port should be set to check the status of glocator in operation.

<a id="f38e0e59f9d4606a"></a>
##### Example

```
$ glocator --status

Process ID: 26058
Configuration file: goldilocks.glocator.conf
Unix domain path: /tmp/unix-glocator.42581
Udp listen host: 0.0.0.0, Port: 42581
glocator is running.
```

<a id="c30abe2b881d4467"></a>
#### sync

<a id="ced49fa0923f1d48"></a>
##### Description

It synchronizes the data of glocator set in ALTERNATE_LOCATORS before driving glocator.

There are two methods for the data synchronization, whichare SOURCE and BOTH. SOURCE method brings data from ALTERNATE_LOCATORS, and BOTH method merges two glocators.

<a id="4ac5f4e80c751262"></a>
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

<a id="9a891345e60647fc"></a>
#### silent

<a id="0a12fb713c4e387d"></a>
##### Description

It does not output the message of glocator about the execution.

<a id="7d4dabd3bf55428d"></a>
##### Example

```
$ glocator --start --silent
```

<a id="5567871ff572a978"></a>
#### no-copyright

<a id="ec3f37e1b786f0c8"></a>
##### Description

It does not output the message of glocator's copyright and version about the execution.

<a id="9aeaa04da8f8a123"></a>
##### Example

```
$ glocator --start --no-copyright

glocator is started.
```

<a id="3b50d65833facc6b"></a>
## Using glocator

<a id="c4e030392151926c"></a>
### Data File

glocator data file should be created before starting glocator.

```
$ glocator --create

glocator is created.
```

The directory in which glocator data file is stored can be altered by editing configuration [LOCATION_FILE_DIR](#e9b5b1b4b2c779b8). The default value is created in &lt;GOLDILOCKS_DATA&gt;/db. The data file can be altered by editing [LOCATION_FILE_NAME](#b0cbd518705c0ba6). The default value is glocator.dat.

The maximum size and initial size of glocator data file can be altered by editing configuration [LOCATION_FILE_MAX_SIZE](#9b28a2a9e78fb914)and [LOCATION_FILE_SIZE](#efb96a7eeb955bb3).

<a id="ea4e957f202dfc60"></a>
### CSTARTUP and CSHUTDOWN

glocator can be used to CSTARTUP and CSHUTDOWN the GOLDILOCKS server.  
For that, glocator should be in operation, and CSTARTUP or CSHUTDOWN should be executed through gsqlnet.  
However, LOCATOR_DSN and the property should be set in odbc.ini of the device which executes gsqlnet. For more information, refer to [GOLDILOCKS UNIX ODBC driver libraries](../part-05-developer-manual/31-odbc.md#c5a3c2aa98485108).

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

<a id="56faad635683a5b0"></a>
### Replication

<a id="cc4faf4093f012f9"></a>
#### Overview

glocator replication keeps data consistent, so it enables the stable service through the remote glocator when an error occurs.

<a id="60e05a6a5f2100b1"></a>
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
> - For more information about glocator-related ODBC and how to set gagent, refer to [odbc.ini File](../part-05-developer-manual/31-odbc.md#725df1c9d28dbaab), [ALTERNATE_LOCATORS](47-gagent.md#642110fd2b0a1c05).
> 

<a id="1d719628535b3776"></a>
#### Synchronizing Data

The data should be consistent when the replicated glocator is in service. If glocator in operation does not exist, then all glocator can perform the normal start. If glocator in operation exists, an alternate glocator can be started by synchronizing the data using a [sync](#c30abe2b881d4467) option.

[sync](#c30abe2b881d4467) option has BOTH and SOURCE. BOTH merges glocator's own data and alternate glocator's data. SOURCE brings the data from the counterpart glocator. The sync operation of glocator is 1 : 1 correspondence task between a glocator and an alternate glocator. Therefore, if A and B are already being operated, and C is operated after syncing by using BOTH for the replication of three (A, B, C) glocators, then the data of A and B glocators may be different.

glocator in service synchronizes only the updated content. If the data synchronization fails due to the packet loss or other reasons, then the data may be different. In this case, update the data within that glocator by using [gloctl](48-gloctl.md#7294e10acec21070) program, or restart glocator with sync option.

<a id="454240056fc33453"></a>
## Features of glocator

<a id="301877c296e1b8a2"></a>
### Connection Service

It provides a service feature which enables arbitrarily access any node among user-defined nodes even though the location information of a specific node in a cluster environment is unknown.

The service feature is that a user specifies nodes managed by glocator an arbitrary group. This service can be registered by using gloctl program. Service lists managed by glocator can also be viewed by using gloctl program.

An application should be accessed by using ODBC driver, and LOCATOR_DSN and LOCATOR_SERVICE property should be specified in [odbc.ini file](../part-05-developer-manual/31-odbc.md#725df1c9d28dbaab).

<a id="7bb6d60b25d7db6f"></a>
![locator_service](../assets/images/89e2e4f16c2bf8c7.png)

The figure above describes that an application accesses to g1n1 belonging to service s3. The connecting sequence of ODBC driver by using the service is as same as the sequence of node registered in the service. If ODBC driver fails to connect to g1n1 in the example above, it will try to connect to the next node g2n1.

> To use the service feature, the valid location information of a node should be input in glocator in advance.

<a id="2ecdbe2e2c100d4c"></a>
### Cluster Failover

glocator is helpful when a server proceeds the failover.

When the value of server property [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#be19510d2caed4c1) is set to 1 or 2, and connection between nodes is disconnected in a cluster environment, a failover occurs, then each node proceeds the cluster failover and queries its viability to glocator through gagent.

The glocator which received a query determines the viability between two nodes which were disconnected, and transfer the result to the gagent which enquired the query.

Nodes received the viabilty results are terminated or proceeds the failover.

> The cluster failover processing time of the server is relevant to various properties. Server property [LOCATOR_QUERY_TIMEOUT](../part-02-administration-manual/10-server-property.md#6b7fa52b25651341) sets the time waiting for the response after the server enquires to glocator, and the default value is 3 seconds.   
> Server property [CLUSTER_SPLIT_BRAIN_RETRY_COUNT](../part-02-administration-manual/10-server-property.md#047d8ef8e5e13bea) sets the number of enquiring again when glocator does not respond, and it is relevant to the cluster failover processing time. The default value is 1.

<a id="90ccce540466f6ca"></a>
## glocator Configuration

<a id="d4dab6912c305437"></a>
### Configuration File and Environment Variable

glocator can use a file or environment variable to set the configuration.

An environment variable can be set by using the name of which 'LOCATOR_' is added as a prefix to a configuration property name. For example, setting HOST in the configuration file has the same effect as specifying $LOCATOR_HOST.

The contents of a configuration file takes precedence over the environment variable setting values.

glocator reads the configuration file by reading DSN as the default value of [LOCATOR].

glocator has $GOLDILOCKS_DATA/conf/goldilocks.glocator.conf file as its environment file. To alter the driving environment of glocator, the file contents should be altered, or glocator should start after setting the environment variables.

<a id="153f70b4171acb05"></a>
### Configuration Properties

<a id="c00906047a0c2dae"></a>
#### HOST

<a id="e56050b7267c5d4c"></a>
| Item | Description |
| --- | --- |
| Name | HOST |
| Description | It is an IP address of which glocator binds. |
| Data type | ip address (ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of which glocator binds for UDP communication.  
It uses an IP address in IP v4 form.

<a id="750732dae6088683"></a>
#### PORT

<a id="180d1e11169a9276"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is a port of which glocator waits for Recv. |
| Data type | INT |
| Default value/ range | 42581 / 1024~49151 |

It is a port of which glocator receives a packet through UDP communication.  
The port from 1024 to 49151 can be used.

<a id="a9289e1410955f72"></a>
#### WORKER_COUNT

<a id="3167a7cbc917c0f6"></a>
| Item | Description |
| --- | --- |
| Name | WORKER_COUNT |
| Description | It is the number of threads processing a job. |
| Data type | INT |
| Default value/ range | 1 / 1~8 |

It is the number of threads processing packets of which glocator received from a client or an internal process.

<a id="a3276263c16f7459"></a>
#### MAX_NODE_COUNT

<a id="6bda76801f08b92f"></a>
| Item | Description |
| --- | --- |
| Name | MAX_NODE_COUNT |
| Description | It is the maximum number of connectable gagent. |
| Data type | INT |
| Default value/ range | 64 / 1~8192 |

It is the maximum number of connectable gagent.

<a id="c3e6310a73507533"></a>
#### MESSAGE_QUEUE_SIZE

<a id="c710cb31e0866b87"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_QUEUE_SIZE |
| Description | It is the queue size in which received packets are stored before processing them. |
| Data type | INT |
| Default value/ range | 33554432 / 10485760~2147483648 |

It is the size of queue of which glocator stores packets received from a client or or an internal process before processing them.  
A packet is stored in a queue as a single item in message unit.

<a id="c75e98cd119c113b"></a>
#### MESSAGE_ALLOCATOR_SIZE

<a id="9d8d230f877fc450"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_ALLOCATOR_SIZE |
| Description | It is the size of an allocator which allocates an item to be stored in a message queue. |
| Data type | INT |
| Default value/ range | 33554432 / 10485760~2147483648 |

It is the size of an allocator which is used to allocate an item (message) to be stored in a message queue.

<a id="a9378d6d8df98af4"></a>
#### PACKET_ALLOCATOR_SIZE

<a id="8dca86a50db69ad1"></a>
| Item | Description |
| --- | --- |
| Name | PACKET_ALLOCATOR_SIZE |
| Description | It is the size of an allocator which allocates a packet when receiving packets through UDP communication. |
| Data type | INT |
| Default value/ range | 33554432 / 10485760~2147483648 |

It is the size of an allocator for a buffer which is allocated for glocator to receive packets.

<a id="c54c9549a51424cd"></a>
#### SYSTEM_LOGGER_DIR

<a id="9b4d097f82ba5639"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_LOGGER_DIR |
| Description | It is the directory path of glocator trace log file. |
| Data type | String |
| Default value/ range | &lt;GOLDILOCKS_DATA&gt;/trc |

It is the directory path in which system trace log file of glocator is stored. &lt;GOLDILOCKS_DATA&gt; of the default value is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="7d25895de9347124"></a>
#### SYSTEM_UDS_DIR

<a id="2fa981c1d98a4164"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_UDS_DIR |
| Description | It is the directory path in which unix domain socket file used in glocator is stored. |
| Data type | String |
| Default value/ range | /tmp (Maximum 60 byte) |

It sets the directory path in which the unix domain socket file used in glocator is stored. The maximum length of the directory should be set within 60 bytes.

<a id="e9b5b1b4b2c779b8"></a>
#### LOCATION_FILE_DIR

<a id="5269d40ab977d5c2"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_DIR |
| Description | It is the directory path in which the location file used in glocator is stored. |
| Data type | String |
| Default value/ range | &lt;GOLDILOCKS_DATA&gt;/db |

It sets the directory path in which the location file used in glocator is stored.

<a id="b0cbd518705c0ba6"></a>
#### LOCATION_FILE_NAME

<a id="4dfad127cd83f194"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_NAME |
| Description | It is the name of a location file which is used in glocator. |
| Data type | String |
| Default value/ range | glocator.dat |

It sets the name of a location file which is used in glocator.  
The default value is glocator.dat.

<a id="efb96a7eeb955bb3"></a>
#### LOCATION_FILE_SIZE

<a id="5679770bbe14ba4d"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_SIZE |
| Description | It is the initial size of a location file. |
| Data type | Int |
| Default value/ range | 1048576 / 104576~2147483648 |

It sets the initial size of a location file used in glocator.

<a id="9b28a2a9e78fb914"></a>
#### LOCATION_FILE_MAX_SIZE

<a id="ee6a24558e742f98"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_MAX_SIZE |
| Description | It is the maximum size of a location file. |
| Data type | Int |
| Default value/ range | 10485760 / 104576~2147483648 |

It sets the maximum size of a location file used in glocator.

<a id="9ee09dfce0f94ab0"></a>
#### MESSAGE_TIMEOUT

<a id="e87f51c15e7030c3"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_TIMEOUT |
| Description | It sets the maximum time for glocator to wait to receive packets. |
| Data type | Int |
| Default value/ range | 100 / 0 ~2147483648(unit: seconds) |

It sets the maximum time (seconds) for glocator to wait to receive packets. Packets exceeds the maximum time without being processed, are dumped.

<a id="88bfcbe98fea6fd5"></a>
#### ALTERNATE_LOCATORS

<a id="9f66fe6644573421"></a>
| Item | Description |
| --- | --- |
| Name | ALTERNATE_LOCATORS |
| Description | It sets an alternate locator and replication of glocator. |
| Data type | String |
| Default value/ range | empty / 0 ~ 1024 bytes |

It sets [Replication](#56faad635683a5b0) of glocator.

<a id="94c9dd48755b2197"></a>
#### SYNC_RETRY_COUNT

<a id="776b272e54ad2ad6"></a>
| Item | Description |
| --- | --- |
| Name | SYNC_RETRY_COUNT |
| Description | It sets the number of retry when glocator fails to synchronize with an alternate locator. |
| Data type | Int |
| Default value/ range | 1 / 0 ~ 5 |

It sets the number of redelivery of glocator synchronization.

glocator transfers the altered data to alternate locator when the data is altered, and it transfers the data again when it could not get any response.

<a id="74e13df510933bd9"></a>
#### SYNC_RESPONSE_TIMEOUT

<a id="cc9e5e6a7dade04a"></a>
| Item | Description |
| --- | --- |
| Name | SYNC_RESPONSE_TIMEOUT |
| Description | It sets the time waits for the response for the synchronization of glocator. |
| Data type | Int |
| Default value/ range | 5 / 1 ~ 20 |

It sets the time waits for the response for the synchronization data transferred from glocator.

<a id="71a96fcd9c80b214"></a>
#### KEEPALIVE_IDLE_TIME

<a id="699abf55644d419a"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_IDLE_TIME |
| Description | tcp keepalive idle time for checking dead client session (sec) |
| Data type | INT |
| Default value/ range | 1 / 1 ~ 16383 |

It is the (idle) duration which the TCP packet is not sent nor is received before sending a keep alive packet. In other words, if TCP packet is not exchanged during the time set in KEEPALIVE_IDLE_TIME, then it performs the keep alive mechanism to detect the dead connection.

<a id="1b603f93e815d843"></a>
#### KEEPALIVE_COUNT

<a id="e86052d3d7bb0f12"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_COUNT |
| Description | tcp keepalive check count |
| Data type | INT |
| Default value/ range | 5 / 1 ~ 10 |

It is the number of performing keep alive mechanism.

<a id="ca4149eec15fd865"></a>
#### KEEPALIVE_INTERVAL

<a id="454d9d697aa967b4"></a>
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
