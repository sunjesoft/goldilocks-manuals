<a id="b17e41b7469eb8b7"></a>

# 44. glocator

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/b17e41b7469eb8b7)  
> Tag: `20c.1_30_tag`

[← 43. gtrclogger](43-gtrclogger.md) · [Table of contents](../README.md) · [45. gagent →](45-gagent.md)

<a id="19ceb541c706922f"></a>
## Overview of glocator

<a id="eae13df9dc86d910"></a>
### Definition

glocator is a utility which provides locations to a client and manages them in GOLDILOCKS cluster system.  
The location information of cluster member nodes is provided to the glocator program through [gloctl](46-gloctl.md#92eddab9e67d5932).  
glocator communicates with client and gloctl by using UDP, and it communicates with gagent by using TCP.

> glocator requires the location information such as a listener host, a listener port, a db home path. These location information is provided to the glocator through gloctl.

<a id="b6efb8a1729bd5a6"></a>
### Usage

```
glocator [options]
```

<a id="be3f2c690c329f12"></a>
### Options

<a id="6c349ebc21047322"></a>
#### help

<a id="beb91e736db6fddb"></a>
##### Description

It outputs a help message.

<a id="bd9a0ab3191e47eb"></a>
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

<a id="87428785093fcdff"></a>
#### create

<a id="f8298c0601289f5d"></a>
##### Description

It creates the data file of glocator.

<a id="a989a1d4893f109d"></a>
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

<a id="4dc0ce030bff19cb"></a>
#### start

<a id="553ce6d00fd57f0c"></a>
##### Description

It starts glocator. If glocator having the same port already has started, then an error occurs.

<a id="869619594e4e493a"></a>
##### Example

```
$ glocator --start

glocator is started.
```

<a id="81ad8af0b0410246"></a>
#### stop

<a id="3c02a7e41d2c7ed7"></a>
##### Description

It stops glocator which is in operation. The same port should be set to stop glocator in operation.

<a id="2f53982170172637"></a>
##### Example

```
$ glocator --stop

glocator is stopped.
```

<a id="49f957038f21da13"></a>
#### conf

<a id="befc04e8facfcca2"></a>
##### Description

It sets the configure file when starting glocator.

<a id="6ec402a140a5c02e"></a>
##### Example

```
$ glocator --start --conf goldilocks.glocator.conf

glocator is started.
```

<a id="66bf5616e1a8f44a"></a>
#### status

<a id="3ecd302c32efb378"></a>
##### Description

It outputs the status message of glocator which is in operation. The same port should be set to check the status of glocator in operation.

<a id="df4a02288ebdca6d"></a>
##### Example

```
$ glocator --status

Process ID: 26058
Configuration file: goldilocks.glocator.conf
Unix domain path: /tmp/unix-glocator.42581
Udp listen host: 0.0.0.0, Port: 42581
glocator is running.
```

<a id="c557d9b0e481888a"></a>
#### sync

<a id="09b8c05ca7e2007a"></a>
##### Description

It synchronizes the data of glocator set in ALTERNATE_LOCATORS before driving glocator.

There are two methods for the data synchronization, whichare SOURCE and BOTH. SOURCE method brings data from ALTERNATE_LOCATORS, and BOTH method merges two glocators.

<a id="1fd35887a5070461"></a>
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

<a id="445b22d8dcdc4201"></a>
#### silent

<a id="973ef31951a2f2a1"></a>
##### Description

It does not output the message of glocator about the execution.

<a id="98fc424ae05a0b08"></a>
##### Example

```
$ glocator --start --silent
```

<a id="cf88b75fb5b94375"></a>
#### no-copyright

<a id="a565be2a1e14f12b"></a>
##### Description

It does not output the message of glocator's copyright and version about the execution.

<a id="e771f45093123caa"></a>
##### Example

```
$ glocator --start --no-copyright

glocator is started.
```

<a id="3000e79cfc91ad66"></a>
## Using glocator

<a id="9c733bad76afa8d9"></a>
### Data File

glocator data file should be created before starting glocator.

```
$ glocator --create

glocator is created.
```

The directory in which glocator data file is stored can be altered by editing configuration [LOCATION_FILE_DIR](#39f763fdaf506c46). The default value is created in &lt;GOLDILOCKS_DATA&gt;/db. The data file can be altered by editing [LOCATION_FILE_NAME](#f6e5d8991fd2ce50). The default value is glocator.dat.

The maximum size and initial size of glocator data file can be altered by editing configuration [LOCATION_FILE_MAX_SIZE](#7a780e7cfce2385d)and [LOCATION_FILE_SIZE](#332d2875d0873aa3).

<a id="fe80aa22e0a52d83"></a>
### CSTARTUP and CSHUTDOWN

glocator can be used to CSTARTUP and CSHUTDOWN the GOLDILOCKS server.  
For that, glocator should be in operation, and CSTARTUP or CSHUTDOWN should be executed through gsqlnet.  
However, LOCATOR_DSN and the property should be set in odbc.ini of the device which executes gsqlnet. For more information, refer to [GOLDILOCKS UNIX ODBC driver libraries](../part-05-developer-manual/29-odbc.md#9a660839378ba63d).

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

<a id="23384c9eab044599"></a>
### Replication

<a id="26ad201c615c7aac"></a>
#### Overview

glocator replication keeps data consistent, so it enables the stable service through the remote glocator when an error occurs.

<a id="cf45313695ab2116"></a>
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
> - For more information about glocator-related ODBC and how to set gagent, refer to [odbc.ini File](../part-05-developer-manual/29-odbc.md#ff97025ffdef9296), [ALTERNATE_LOCATORS](45-gagent.md#602b7d8094a5b586).
> 

<a id="69d983f42fd9d2a4"></a>
#### Synchronizing Data

The data should be consistent when the replicated glocator is in service. If glocator in operation does not exist, then all glocator can perform the normal start. If glocator in operation exists, an alternate glocator can be started by synchronizing the data using a [sync](#c557d9b0e481888a) option.

[sync](#c557d9b0e481888a) option has BOTH and SOURCE. BOTH merges glocator's own data and alternate glocator's data. SOURCE brings the data from the counterpart glocator. The sync operation of glocator is 1 : 1 correspondence task between a glocator and an alternate glocator. Therefore, if A and B are already being operated, and C is operated after syncing by using BOTH for the replication of three (A, B, C) glocators, then the data of A and B glocators may be different.

glocator in service synchronizes only the updated content. If the data synchronization fails due to the packet loss or other reasons, then the data may be different. In this case, update the data within that glocator by using [gloctl](46-gloctl.md#92eddab9e67d5932) program, or restart glocator with sync option.

<a id="9df53fc07e5307c0"></a>
## Features of glocator

<a id="3d50def65fda6e6a"></a>
### Connection Service

It provides a service feature which enables arbitrarily access any node among user-defined nodes even though the location information of a specific node in a cluster environment is unknown.

The service feature is that a user specifies nodes managed by glocator an arbitrary group. This service can be registered by using gloctl program. Service lists managed by glocator can also be viewed by using gloctl program.

An application should be accessed by using ODBC driver, and LOCATOR_DSN and LOCATOR_SERVICE property should be specified in [odbc.ini file](../part-05-developer-manual/29-odbc.md#ff97025ffdef9296).

<a id="604bd9b4ce7eafb2"></a>
![locator_service](../assets/images/50e3bf3980e42169.png)

The figure above describes that an application accesses to g1n1 belonging to service s3. The connecting sequence of ODBC driver by using the service is as same as the sequence of node registered in the service. If ODBC driver fails to connect to g1n1 in the example above, it will try to connect to the next node g2n1.

> To use the service feature, the valid location information of a node should be input in glocator in advance.

<a id="c4448c510139171c"></a>
### Cluster Failover

glocator is helpful when a server proceeds the failover.

When the value of server property [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#26f74ad6f85847fb) is set to 1 or 2, and connection between nodes is disconnected in a cluster environment, a failover occurs, then each node proceeds the cluster failover and queries its viability to glocator through gagent.

The glocator which received a query determines the viability between two nodes which were disconnected, and transfer the result to the gagent which enquired the query.

Nodes received the viabilty results are terminated or proceeds the failover.

> The cluster failover processing time of the server is relevant to various properties. Server property [LOCATOR_QUERY_TIMEOUT](../part-02-administration-manual/10-server-property.md#11fc47d8eb3dc574) sets the time waiting for the response after the server enquires to glocator, and the default value is 3 seconds.   
> Server property [CLUSTER_SPLIT_BRAIN_RETRY_COUNT](../part-02-administration-manual/10-server-property.md#97e591676118d894) sets the number of enquiring again when glocator does not respond, and it is relevant to the cluster failover processing time. The default value is 1.

<a id="80d48f35b4e98d33"></a>
## glocator Configuration

<a id="4953d123050a36b0"></a>
### Configuration File and Environment Variable

glocator can use a file or environment variable to set the configuration.

An environment variable can be set by using the name of which 'LOCATOR_' is added as a prefix to a configuration property name. For example, setting HOST in the configuration file has the same effect as specifying $LOCATOR_HOST.

The contents of a configuration file takes precedence over the environment variable setting values.

glocator reads the configuration file by reading DSN as the default value of [LOCATOR].

glocator has $GOLDILOCKS_DATA/conf/goldilocks.glocator.conf file as its environment file. To alter the driving environment of glocator, the file contents should be altered, or glocator should start after setting the environment variables.

<a id="0368b2ed7f70243a"></a>
### Configuration Properties

<a id="18ae85c79930d4e5"></a>
#### HOST

<a id="78e80de7404c4c86"></a>
| Item | Description |
| --- | --- |
| Name | HOST |
| Description | It is an IP address of which glocator binds. |
| Data type | ip address (ip v4) |
| Default value/ range | 0.0.0.0 |

It is an IP address of which glocator binds for UDP communication.  
It uses an IP address in IP v4 form.

<a id="66bcf80a910eb7cf"></a>
#### PORT

<a id="cb8f53a074eb3ade"></a>
| Item | Description |
| --- | --- |
| Name | PORT |
| Description | It is a port of which glocator waits for Recv. |
| Data type | INT |
| Default value/ range | 42581 / 1024~49151 |

It is a port of which glocator receives a packet through UDP communication.  
The port from 1024 to 49151 can be used.

<a id="35eda308120a47dc"></a>
#### WORKER_COUNT

<a id="1c797e924b05869d"></a>
| Item | Description |
| --- | --- |
| Name | WORKER_COUNT |
| Description | It is the number of threads processing a job. |
| Data type | INT |
| Default value/ range | 1 / 1~8 |

It is the number of threads processing packets of which glocator received from a client or an internal process.

<a id="a673f5ae08659002"></a>
#### MAX_NODE_COUNT

<a id="d7c7141fdf3b1134"></a>
| Item | Description |
| --- | --- |
| Name | MAX_NODE_COUNT |
| Description | It is the maximum number of connectable gagent. |
| Data type | INT |
| Default value/ range | 64 / 1~8192 |

It is the maximum number of connectable gagent.

<a id="ead486e778751dde"></a>
#### MESSAGE_QUEUE_SIZE

<a id="7a576ebddb51e8e2"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_QUEUE_SIZE |
| Description | It is the queue size in which received packets are stored before processing them. |
| Data type | INT |
| Default value/ range | 33554432 / 10485760~2147483648 |

It is the size of queue of which glocator stores packets received from a client or or an internal process before processing them.  
Packets are stored as a single item of a message unit in a queue.

<a id="30c51daa45ae6350"></a>
#### MESSAGE_ALLOCATOR_SIZE

<a id="5635da4cd4f1291c"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_ALLOCATOR_SIZE |
| Description | It is the size of an allocator which allocates an item to be stored in a message queue. |
| Data type | INT |
| Default value/ range | 33554432 / 10485760~2147483648 |

It is the size of an allocator which is used to allocate an item (message) to be stored in a message queue.

<a id="159179fa97382500"></a>
#### PACKET_ALLOCATOR_SIZE

<a id="77e51b7a71b8c247"></a>
| Item | Description |
| --- | --- |
| Name | PACKET_ALLOCATOR_SIZE |
| Description | It is the size of an allocator which allocates a packet when receiving packets through UDP communication. |
| Data type | INT |
| Default value/ range | 33554432 / 10485760~2147483648 |

It is the size of an allocator for a buffer which is allocated for glocator to receive packets.

<a id="5ec22f366f0863c7"></a>
#### SYSTEM_LOGGER_DIR

<a id="c4b81a8e632292a4"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_LOGGER_DIR |
| Description | It is the directory path of glocator trace log file. |
| Data type | String |
| Default value/ range | &lt;GOLDILOCKS_DATA&gt;/trc |

It is the directory path in which system trace log file of glocator is stored. &lt;GOLDILOCKS_DATA&gt; of the default value is replaced with the environment variable value of $GOLDILOCKS_DATA.

<a id="b821725735d226ee"></a>
#### SYSTEM_UDS_DIR

<a id="dbfed4cb556fbb1e"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_UDS_DIR |
| Description | It is the directory path in which unix domain socket file used in glocator is stored. |
| Data type | String |
| Default value/ range | /tmp (Maximum 60 byte) |

It sets the directory path in which the unix domain socket file used in glocator is stored. The maximum length of the directory should be set within 60 bytes.

<a id="39f763fdaf506c46"></a>
#### LOCATION_FILE_DIR

<a id="99797586519dc90a"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_DIR |
| Description | It is the directory path in which the location file used in glocator is stored. |
| Data type | String |
| Default value/ range | &lt;GOLDILOCKS_DATA&gt;/db |

It sets the directory path in which the location file used in glocator is stored.

<a id="f6e5d8991fd2ce50"></a>
#### LOCATION_FILE_NAME

<a id="640bdefe0e728ca7"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_NAME |
| Description | It is the name of a location file which is used in glocator. |
| Data type | String |
| Default value/ range | glocator.dat |

It sets the name of a location file which is used in glocator.  
The default value is glocator.dat.

<a id="332d2875d0873aa3"></a>
#### LOCATION_FILE_SIZE

<a id="1b4d98abab6b4925"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_SIZE |
| Description | It is the initial size of a location file. |
| Data type | Int |
| Default value/ range | 1048576 / 104576~2147483648 |

It sets the initial size of a location file used in glocator.

<a id="7a780e7cfce2385d"></a>
#### LOCATION_FILE_MAX_SIZE

<a id="4e75e3132b2ede2f"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE_MAX_SIZE |
| Description | It is the maximum size of a location file. |
| Data type | Int |
| Default value/ range | 10485760 / 104576~2147483648 |

It sets the maximum size of a location file used in glocator.

<a id="ef2e626daba65864"></a>
#### MESSAGE_TIMEOUT

<a id="93b0cd0ed8bdd8b3"></a>
| Item | Description |
| --- | --- |
| Name | MESSAGE_TIMEOUT |
| Description | It sets the maximum time for glocator to wait to receive packets. |
| Data type | Int |
| Default value/ range | 100 / 0 ~2147483648(unit: seconds) |

It sets the maximum time (seconds) for glocator to wait to receive packets. Packets exceeds the maximum time without being processed, are dumped.

<a id="9acf5eccfd1d9f8c"></a>
#### ALTERNATE_LOCATORS

<a id="e05bfe44dd371b2c"></a>
| Item | Description |
| --- | --- |
| Name | ALTERNATE_LOCATORS |
| Description | It sets an alternate locator and replication of glocator. |
| Data type | String |
| Default value/ range | empty / 0 ~ 1024 bytes |

It sets [Replication](#23384c9eab044599) of glocator.

<a id="fe991f4ec36f1c93"></a>
#### SYNC_RETRY_COUNT

<a id="a51411a6e6126875"></a>
| Item | Description |
| --- | --- |
| Name | SYNC_RETRY_COUNT |
| Description | It sets the number of retry when glocator fails to synchronize with an alternate locator. |
| Data type | Int |
| Default value/ range | 1 / 0 ~ 5 |

It sets the number of redelivery of glocator synchronization.

glocator transfers the altered data to alternate locator when the data is altered, and it transfers the data again when it could not get any response.

<a id="3b4867e3ad45f165"></a>
#### SYNC_RESPONSE_TIMEOUT

<a id="fb2a99251452287b"></a>
| Item | Description |
| --- | --- |
| Name | SYNC_RESPONSE_TIMEOUT |
| Description | It sets the time waits for the response for the synchronization of glocator. |
| Data type | Int |
| Default value/ range | 5 / 1 ~ 20 |

It sets the time waits for the response for the synchronization data transferred from glocator.

<a id="8bcd2af50f4dbe8c"></a>
#### KEEPALIVE_IDLE_TIME

<a id="1092d79de24fdf42"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_IDLE_TIME |
| Description | tcp keepalive idle time for checking dead client session (sec) |
| Data type | INT |
| Default value/ range | 1 / 1 ~ 16383 |

It is the (idle) duration which the TCP packet is not sent nor is received before sending a keep alive packet. In other words, if TCP packet is not exchanged during the time set in KEEPALIVE_IDLE_TIME, then it performs the keep alive mechanism to detect the dead connection.

<a id="9f0fe87f8e18f998"></a>
#### KEEPALIVE_COUNT

<a id="c7bcdeee015bbaec"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_COUNT |
| Description | tcp keepalive check count |
| Data type | INT |
| Default value/ range | 5 / 1 ~ 10 |

It is the number of performing keep alive mechanism.

<a id="b21f5a4a10e1193a"></a>
#### KEEPALIVE_INTERVAL

<a id="656f2f87bb5ff583"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_INTERVAL |
| Description | tcp keepalive packet interval (sec) |
| Data type | INT |
| Default value/ range | 5 |

It is the time interval to send the keep alive packet.

---

[← 43. gtrclogger](43-gtrclogger.md) · [Table of contents](../README.md) · [45. gagent →](45-gagent.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
