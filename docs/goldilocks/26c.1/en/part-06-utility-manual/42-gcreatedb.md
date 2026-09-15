<a id="7d4adb6d596a32f4"></a>

# 42. gcreatedb

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/7d4adb6d596a32f4)  
> Tag: `26c.1_0_tag`

[← 41. Hibernate](../part-05-developer-manual/41-hibernate.md) · [Table of contents](../README.md) · [43. glsnr →](43-glsnr.md)

<a id="e3880044a24457a8"></a>
## Overview of gcreatedb

<a id="27efa8cd419b60cc"></a>
### Definition

gcreatedb is a database creation utility provided by GOLDILOCKS.

<a id="c595e2c9c0ca53af"></a>
### Feature

A new database is created by using DB_Name, comment, time zone, character set specified by a user.

<a id="d459b81244e024f8"></a>
### Usage

```
gcreatedb [options]
```

<a id="7cfbce010dd8d436"></a>
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
--silent               suppresses the display of the result message
--help                 print help message
```

<a id="6e5f4a45280e6dd6"></a>
### Example

```
$ gcreatedb --db_name="goldilocks" --db-comment="goldilocks database" --timezone="+09:00" --character_set="UTF8" --silent
```

<a id="04aa23053fcf287f"></a>
## Command Option

<a id="f5295d0d53da2805"></a>
### --cluster

It creates the database of a cluster environment.  
If this option is not used, then it creates the database of a stand alone environment.

<a id="c93b6b4eba4adf09"></a>
### --db_name

It specifies the database name which a user wants to create.  
The default value is "goldilocks".  
The maximum length of database name is 128.

<a id="396250fdf9a0d425"></a>
### --db_comment

It specifies the database comment which a user wants to create.  
The default value is "goldilocks database".  
The maximum length of database comment is 1024.

<a id="183ed58f998429be"></a>
### --timezone

It is the time zone value of database.  
The default value is the [TIMEZONE](../part-02-administration-manual/10-server-property.md#f9d2b587e8535ce0) value of the property.  
The property is applied when database is created and it has a value in range of '-14:00' ~ '+14:00'.

<a id="33260d928d93cd28"></a>
### --character_set

It is the database character set.  
The default value is the [CHARACTER_SET](../part-02-administration-manual/10-server-property.md#e0299b8677bc1e4e) value of the property.

The property is applied when database is created, and its value is set to one of the following.  
• GB18030  
• SQL_ASCII  
• UHC  
• UTF8

<a id="d397ec254505ed12"></a>
### --char_length_units

It is the char length unit value that is used when defining the string column type such as CHAR, VARCHAR and omitting its char length unit as follows.

```
CREATE TABLE t1
(
    id   CHAR( 10 OCTETS ),         ❶ It refers to 10 bytes.
    name VARCHAR( 128 CHARACTERS ), ❷ It refers to 128 characters.
    addr VARCHAR( 1024 )            ❸ char length unit is omitted.
```

The default value is the [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#b06a0825ab72d342) value of the property.

The property is applied when database is created, and its value is set to one of the following.  
• OCTETS: It is the number of bytes.  
• CHARACTERS: It is the number of characters.

The default value of char length unit is defined as CHARACTERS in the SQL standard and it is defined as follows in other DBMS.


> 
> - OCTETS is used in Oracle, DB2.
> - CHARACTERS is used in MS-SQL, MySQL, PostgreSQL.
> 

<a id="c23dceab07e5dbf8"></a>
### --home

It sets the home directory of the database.  
The default value uses $GOLDILOCKS_HOME environment variable.

<a id="96d0cb72568621f4"></a>
### --member

It sets the name of a local database in a cluster environment.

<a id="689cf50905f8bbf5"></a>
### --host

It sets the host address of a local database in a cluster environment.

<a id="030e7259143d5a20"></a>
### --port

It sets the port number of a local database in a cluster environment.

<a id="536dbf52cf0d0e1b"></a>
### --silent

Result messages are not displayed.

<a id="3ba10df1519bba2f"></a>
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

[← 41. Hibernate](../part-05-developer-manual/41-hibernate.md) · [Table of contents](../README.md) · [43. glsnr →](43-glsnr.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
