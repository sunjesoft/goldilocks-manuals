<a id="95fdeea213dbe839"></a>

# 37. gcreatedb

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/95fdeea213dbe839)  
> Tag: `22c.1_10_tag`

[← 36. Hibernate](../part-05-developer-manual/36-hibernate.md) · [Table of contents](../README.md) · [38. glsnr →](38-glsnr.md)

<a id="ebe3d43d5ba8cd8d"></a>
## Overview of gcreatedb

<a id="bc029bb3233b6404"></a>
### Definition

gcreatedb is a database creation utility provided by GOLDILOCKS.

<a id="59d8ac6a445c20da"></a>
### Feature

A new database is created by using DB_Name, comment, time zone, character set specified by a user.

<a id="e0febfbcfb4b411c"></a>
### Usage

```
gcreatedb [options]
```

<a id="e7b9afbcfe5b00dc"></a>
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

<a id="e8a7c6e8838639ac"></a>
### Example

```
$ gcreatedb --db_name="goldilocks" --db-comment="goldilocks database" --timezone="+09:00" --character_set="UTF8" --silent
```

<a id="b068997f1e4a0cb3"></a>
## Command Option

<a id="6db8979c1141f1a0"></a>
### --cluster

It creates the database of a cluster environment.  
If this option is not used, then it creates the database of a stand alone environment.

<a id="28af35976a698e19"></a>
### --db_name

It specifies the database name which a user wants to create.  
The default value is "goldilocks".  
The maximum length of database name is 128.

<a id="802d991f1b1155bc"></a>
### --db_comment

It specifies the database comment which a user wants to create.  
The default value is "goldilocks database".  
The maximum length of database comment is 1024.

<a id="c0ec291e87a533fd"></a>
### --timezone

It is the time zone value of database.  
The default value is the [TIMEZONE](../part-02-administration-manual/10-server-property.md#f2521763b8497dc5) value of the property.  
The property is applied when database is created and it has a value in range of '-14:00' ~ '+14:00'.

<a id="e798776d0f85e504"></a>
### --character_set

It is the database character set.  
The default value is the [CHARACTER_SET](../part-02-administration-manual/10-server-property.md#43f975ccd5788104) value of the property.

The property is applied when database is created, and its value is set to one of the followings.  
• GB18030  
• SQL_ASCII  
• UHC  
• UTF8

<a id="0d8ad0801204de33"></a>
### --char_length_units

It is the char length unit value which is used when defining the string column type such as CHAR, VARCHAR and omitting its char length unit as follows.

```
CREATE TABLE t1
(
    id   CHAR( 10 OCTETS ),         ❶ It refers to 10 bytes.
    name VARCHAR( 128 CHARACTERS ), ❷ It refers to 128 characters.
    addr VARCHAR( 1024 )            ❸ char length unit is omitted.
```

The default value is the [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#24f01f5e333485e5) value of the property.

The property is applied when database is created, and its value is set to one of the followings.  
• OCTETS: It is the number of bytes.  
• CHARACTERS: It is the number of characters.

The default value of char length unit is defined as CHARACTERS in the SQL standard and it is defined as follows in other DBMS.


> 
> - OCTETS is used in Oracle, DB2.
> - CHARACTERS is used in MS-SQL, MySQL, PostgreSQL.
> 

<a id="2c842dd3908324af"></a>
### --home

It sets the home directory of the database.  
The default value uses $GOLDILOCKS_HOME environment variable.

<a id="7111d211a22f1636"></a>
### --member

It sets the name of a local database in a cluster environment.

<a id="b95ea798e0c558b8"></a>
### --host

It sets the host address of a local database in a cluster environment.

<a id="f27ad2ef37482040"></a>
### --port

It sets the port number of a local database in a cluster environment.

<a id="ec287d41e70c261b"></a>
### --silent

Result messages are not displayed.

<a id="21be18f480def9a8"></a>
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

[← 36. Hibernate](../part-05-developer-manual/36-hibernate.md) · [Table of contents](../README.md) · [38. glsnr →](38-glsnr.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
