<a id="54320cd425746e45"></a>

# 37. gcreatedb

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/54320cd425746e45)  
> Tag: `21c.1_35_tag`

[← 36. Hibernate](../part-05-developer-manual/36-hibernate.md) · [Table of contents](../README.md) · [38. glsnr →](38-glsnr.md)

<a id="30f52897660fc094"></a>
## Overview of gcreatedb

<a id="72829c9944cf1859"></a>
### Definition

gcreatedb is a database creation utility provided by GOLDILOCKS.

<a id="8daa776d415697e1"></a>
### Feature

A new database is created by using DB_Name, comment, time zone, character set specified by a user.

<a id="906aed07044146d8"></a>
### Usage

```
gcreatedb [options]
```

<a id="da65e28050029f5b"></a>
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

<a id="e43d6490de9feac5"></a>
### Example

```
$ gcreatedb --db_name="goldilocks" --db-comment="goldilocks database" --timezone="+09:00" --character_set="UTF8" --silent
```

<a id="1fae385b5371e3ac"></a>
## Command Option

<a id="08cd66d0d1772325"></a>
### --cluster

It creates the database of a cluster environment.  
If this option is not used, then it creates the database of a stand alone environment.

<a id="f1c36e462d6f12be"></a>
### --db_name

It specifies the database name which a user wants to create.  
The default value is "goldilocks".  
The maximum length of database name is 128.

<a id="c0ec47ccc0f3a38a"></a>
### --db_comment

It specifies the database comment which a user wants to create.  
The default value is "goldilocks database".  
The maximum length of database comment is 1024.

<a id="d6b6979d49ba82f8"></a>
### --timezone

It is the time zone value of database.  
The default value is the [TIMEZONE](../part-02-administration-manual/10-server-property.md#add5466e40448a63) value of the property.  
The property is applied when database is created and it has a value in range of '-14:00' ~ '+14:00'.

<a id="9f5210d38fbf6878"></a>
### --character_set

It is the database character set.  
The default value is the [CHARACTER_SET](../part-02-administration-manual/10-server-property.md#252318a04d4fbe0e) value of the property.

The property is applied when database is created, and its value is set to one of the followings.  
• GB18030  
• SQL_ASCII  
• UHC  
• UTF8

<a id="3e1695372f46847c"></a>
### --char_length_units

It is the char length unit value which is used when defining the string column type such as CHAR, VARCHAR and omitting its char length unit as follows.

```
CREATE TABLE t1
(
    id   CHAR( 10 OCTETS ),         ❶ It refers to 10 bytes.
    name VARCHAR( 128 CHARACTERS ), ❷ It refers to 128 characters.
    addr VARCHAR( 1024 )            ❸ char length unit is omitted.
```

The default value is the [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#305fe0fd4eb06210) value of the property.

The property is applied when database is created, and its value is set to one of the followings.  
• OCTETS: It is the number of bytes.  
• CHARACTERS: It is the number of characters.

The default value of char length unit is defined as CHARACTERS in the SQL standard and it is defined as follows in other DBMS.


> 
> - OCTETS is used in Oracle, DB2.
> - CHARACTERS is used in MS-SQL, MySQL, PostgreSQL.
> 

<a id="6c11b8312ca2d730"></a>
### --home

It sets the home directory of the database.  
The default value uses $GOLDILOCKS_HOME environment variable.

<a id="f62c831952980655"></a>
### --member

It sets the name of a local database in a cluster environment.

<a id="31c63096d468435a"></a>
### --host

It sets the host address of a local database in a cluster environment.

<a id="fc140b3cf7ba29e2"></a>
### --port

It sets the port number of a local database in a cluster environment.

<a id="1b6512dc49c0c028"></a>
### --silent

Result messages are not displayed.

<a id="4a9f019bf25f2e91"></a>
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
