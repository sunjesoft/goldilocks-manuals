<a id="d7dcb4af5b8f7568"></a>

# 35. gcreatedb

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/d7dcb4af5b8f7568)  
> Tag: `20c.1_30_tag`

[← 34. Hibernate](../part-05-developer-manual/34-hibernate.md) · [Table of contents](../README.md) · [36. glsnr →](36-glsnr.md)

<a id="0c6675a447a5328f"></a>
## Overview of gcreatedb

<a id="ba89f76e7ca77bab"></a>
### Definition

gcreatedb is a database creation utility provided by GOLDILOCKS.

<a id="01eff3030e3c0283"></a>
### Feature

A new database is created by using DB_Name, comment, time zone, character set specified by a user.

<a id="89c709e8aa7bb73d"></a>
### Usage

```
gcreatedb [options]
```

<a id="cf5c3c67ed369b35"></a>
### Option

```
--cluster              cluster system (if not specified, stand-alone system)
--db_name              database name
--db_comment           database comment
--timezone             timezone ( {+/-}{TZH:TZM} )
--character_set        character set
                            SQL_ASCII
                            UTF8
                            UHC
                            GB18030
--char_length_units    char length units
                            OCTETS
                            CHARACTERS
--home                 home directory
--member               local member name
--host                 host address
--port                 host port
--silent               suppersses the display of the result message
--help                 print help message
```

<a id="4418b8e8170c6f89"></a>
### Example

```
$ gcreatedb --db_name="goldilocks" --db-comment="goldilocks database" --timezone="+09:00" --character_set="UTF8" --silent
```

<a id="a1aeee2e4b921e2c"></a>
## Command Option

<a id="ac5402a43d6bc956"></a>
### --cluster

It creates the database of a cluster environment.  
If this option is not used, then it creates the database of a stand alone environment.

<a id="54f00bcb3dd056af"></a>
### --db_name

It specifies the database name which a user wants to create.  
The default value is "goldilocks".  
The maximum length of database name is 128.

<a id="c833c7b469bdf489"></a>
### --db_comment

It specifies the database comment which a user wants to create.  
The default value is "goldilocks database".  
The maximum length of database comment is 1024.

<a id="4618a43239eaac5e"></a>
### --timezone

It is the time zone value of database.  
The default value is the [TIMEZONE](../part-02-administration-manual/10-server-property.md#0211eda8f9578dfb) value of the property.  
The property is applied when database is created and it has a value in range of '-14:00' ~ '+14:00'.

<a id="f9e451df3974f55b"></a>
### --character_set

It is the database character set.  
The default value is the [CHARACTER_SET](../part-02-administration-manual/10-server-property.md#be7fc290b526b319) value of the property.

The property is applied when database is created, and its value is set to one of the followings.  
• GB18030  
• SQL_ASCII  
• UHC  
• UTF8

<a id="61086f8facf517e4"></a>
### --char_length_units

It is the char length unit value which is used when defining the string column type such as CHAR, VARCHAR and omitting its char length unit as follows.

```
CREATE TABLE t1
(
    id   CHAR( 10 OCTETS ),         ❶ It refers to 10 bytes.
    name VARCHAR( 128 CHARACTERS ), ❷ It refers to 128 characters.
    addr VARCHAR( 1024 )            ❸ char length unit is omitted.
```

The default value is the [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#3c69a6a4ea2b681f) value of the property.

The property is applied when database is created, and its value is set to one of the followings.  
• OCTETS: It is the number of bytes.  
• CHARACTERS: It is the number of characters.

The default value of char length unit is defined as CHARACTERS in the SQL standard and it is defined as follows in other DBMS.


> 
> - OCTETS is used in Oracle, DB2.
> - CHARACTERS is used in MS-SQL, MySQL, PostgreSQL.
> 

<a id="e57685e75e17fe28"></a>
### --home

It sets the home directory of the database.  
The default value uses $GOLDILOCKS_HOME environment variable.

<a id="c8c04e8c3b544d29"></a>
### --member

It sets the name of a local database in a cluster environment.

<a id="8e614ad365e853fe"></a>
### --host

It sets the host address of a local database in a cluster environment.

<a id="01c72320e0257a1a"></a>
### --port

It sets the port number of a local database in a cluster environment.

<a id="7ca0490450516d40"></a>
### --silent

Result messages are not displayed.

<a id="e17ed3bf3fe482e8"></a>
### --help

Help messages are displayed.

```
$ gcreatedb --help

Usage 
    gcreatedb [options]
Options:
    --db_name                 database name
    --db_comment              database comment
    --timezone                timezone ( {+/-}{TZH:TZM} )
    --character_set           character set
                                SQL_ASCII
                                UTF8
                                UHC
                                GB18030
    --char_length_units       char length units
                                OCTETS
                                CHARACTERS
    --silent                  suppresses the display of the result message
    --help                    print help message

examples:
    gcreatedb --db_name="goldilocks" --db_comment="goldilocks database" --timezone="+09:00" --character_set="UTF8" --char_length_units="OCTETS" --silent
```

---

[← 34. Hibernate](../part-05-developer-manual/34-hibernate.md) · [Table of contents](../README.md) · [36. glsnr →](36-glsnr.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
