<a id="649be67a753ea5df"></a>

# 31. gcreatedb

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/649be67a753ea5df)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 30. Hibernate](../part-05-developer-manual/30-hibernate.md) · [Table of contents](../README.md) · [32. glsnr →](32-glsnr.md)

<a id="2e8d977eaea35f15"></a>
## Overview of gcreatedb

<a id="eaccf466af646313"></a>
### Definition

gcreatedb is a database creation utility provided by GOLDILOCKS.

<a id="b4cdc530e706c935"></a>
### Feature

A new database is created by using DB_Name, comment, time zone, character set specified by a user.

<a id="3c5cf386c31dba30"></a>
### Usage

```
gcreatedb [options]
```

<a id="00aab8455d9a07fe"></a>
### Options

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

<a id="121b848e1573adca"></a>
### Example

```
$ gcreatedb --db_name="goldilocks" --db-comment="goldilocks database" --timezone="+09:00" --character_set="UTF8" --silent
```

<a id="82b936dcc6d315b4"></a>
## Command Option

<a id="1e0a7183e0bf3b69"></a>
### --cluster

It creates the database of a cluster environment.  
If this option is not used, then it creates the database of a stand alone environment.

<a id="fafa94f3e2c407cf"></a>
### --db_name

It specifies the database name which a user wants to create.  
The default value is "goldilocks".  
The maximum length of database name is 128.

<a id="dfa8ebc8a77dfc48"></a>
### --db_comment

It specifies the database comment which a user wants to create.  
The default value is "goldilocks database".  
The maximum length of database comment is 1024.

<a id="7b845cf9658288c6"></a>
### --timezone

It is the time zone value of database.  
The default value is the [TIMEZONE](../part-02-administration-manual/10-server-property.md#c44fdc9c88a6cf8e) value of the property.  
The property is applied when database is created and it has a value in range of '-14:00' ~ '+14:00'.

<a id="07f6223828474639"></a>
### --character_set

It is the database character set.  
The default value is the [CHARACTER_SET](../part-02-administration-manual/10-server-property.md#3633168d2f3bb347) value of the property.

The property is applied when database is created, and its value is set to one of the followings.  
• GB18030  
• SQL_ASCII  
• UHC  
• UTF8

<a id="c8efbc1484cea208"></a>
### --char_length_units

It is the char length unit value which is used when defining the string column type such as CHAR, VARCHAR and omitting its char length unit as follows.

```
CREATE TABLE t1
(
    id   CHAR( 10 OCTETS ),         ❶ It refers to 10 bytes.
    name VARCHAR( 128 CHARACTERS ), ❷ It refers to 128 characters.
    addr VARCHAR( 1024 )            ❸ char length unit is omitted.
```

The default value is the [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#e6ecf251502c667b) value of the property.

The property is applied when database is created, and its value is set to one of the followings.  
• OCTETS: It is the number of bytes.  
• CHARACTERS: It is the number of characters.

The default value of char length unit is defined as CHARACTERS in the SQL standard and it is defined as follows in other DBMS.


> 
> - OCTETS is used in Oracle, DB2.
> - CHARACTERS is used in MS-SQL, MySQL, PostgreSQL.
> 

<a id="cf4c6d08599bf5df"></a>
### --home

It sets the home directory of the database.  
The default value uses $GOLDILOCSK_HOME environment variable.

<a id="2aabae9483b49518"></a>
### --member

It sets the name of a local database in a cluster environment.

<a id="75606b72b7683162"></a>
### --host

It sets the host address of a local database in a cluster environment.

<a id="e16c0d1aad2e1de0"></a>
### --port

It sets the port number of a local database in a cluster environment.

<a id="e8d8a5584a8618a3"></a>
### --silent

Result messages are not displayed.

<a id="136b4b58f728d388"></a>
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

[← 30. Hibernate](../part-05-developer-manual/30-hibernate.md) · [Table of contents](../README.md) · [32. glsnr →](32-glsnr.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
