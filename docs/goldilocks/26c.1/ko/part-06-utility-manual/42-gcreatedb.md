<a id="070b6679f923fc0d"></a>

# 42. gcreatedb

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/070b6679f923fc0d)  
> 태그: `26c.1_0_tag`

[← 41. Hibernate](../part-05-developer-manual/41-hibernate.md) · [전체 목차](../README.md) · [43. glsnr →](43-glsnr.md)

<a id="24dc89b31a067685"></a>
## gcreatedb 소개

<a id="1c6de260ca8d00ed"></a>
### 정의

gcreatedb는 GOLDILOCKS에서 제공하는 데이터베이스 생성 유틸리티이다.

<a id="9deaff3c54128ecd"></a>
### 기능

사용자가 지정한 DB-name, comment, time zone, character set으로 새로운 데이터베이스를 생성한다.

<a id="0b9cefd64b39b41b"></a>
### 사용법

```
gcreatedb [options]
```

<a id="cc99f85651d767fa"></a>
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

<a id="20c5594449dd607e"></a>
### 사용 예

```
$ gcreatedb --db_name="goldilocks" --db-comment="goldilocks database" --timezone="+09:00" --character_set="UTF8" --silent
```

<a id="6ca34f47bae263e6"></a>
## Command Option

<a id="88e39a502664e31e"></a>
### --cluster

Cluster 환경의 database를 생성한다.   
이를 사용하지 않을 경우 stand alone database를 생성한다.

<a id="162074240e4cf035"></a>
### --db_name

사용자가 생성하려는 database name을 지정한다.   
Default value는 "goldilocks"이다.  
Database name의 최대 길이는 128 이다.

<a id="1489181e118ae416"></a>
### --db_comment

사용자가 생성하려는 database comment를 지정한다.   
Default value는 "goldilocks database" 이다.   
Database comment의 최대 길이는 1024 이다.

<a id="c333bb0f134a0e1b"></a>
### --timezone

Database의 time zone 값이다.  
Default value는 property의 [TIMEZONE](../part-02-administration-manual/10-server-property.md#e5a8420441fa46e1) 값이다.  
Database를 생성할 때 적용되는 속성으로써 '-14:00' ~ '+14:00' 범위의 값을 사용할 수 있다.

<a id="6cf1f7ba683df9b5"></a>
### --character_set

Database의 character set이다.  
Default value는 property의 [CHARACTER_SET](../part-02-administration-manual/10-server-property.md#136f16d5d32f730b) 값이다.

Database를 생성할 때 적용되는 속성으로써 다음 중 하나의 값으로 설정할 수 있다.  
• GB18030  
• SQL_ASCII  
• UHC  
• UTF8

<a id="dc5a5698865d91cd"></a>
### --char_length_units

CHAR, VARCHAR와 같은 문자열 column을 정의하면서 다음과 같이 char length unit을 생략할 경우에 사용되는 char length units 값이다.

```
CREATE TABLE t1
(
    id   CHAR( 10 OCTETS ),         ❶ 10 bytes를 의미한다.
    name VARCHAR( 128 CHARACTERS ), ❷ 128 글자를 의미한다.
    addr VARCHAR( 1024 )            ❸ char length unit이 생략되었다.
);
```

Default value는 property의 [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#502c307b879b9ff8) 값이다.

Database를 생성할 때 적용되는 속성으로써 다음 중 하나의 값으로 설정할 수 있다.  
• OCTETS: Byte 수를 의미한다.  
• CHARACTERS: 문자 개수를 의미한다.

SQL 표준은 기본값을 CHARACTERS로 정의하고 있으며 다른 DBMS들의 char length unit 기본값은 다음과 같다.


> 
> - Oracle과 DB2에서는 OCTETS를 사용한다.
> - MS-SQL, MySQL, PostgreSQL에서는 CHARACTERS를 사용한다.
> 

<a id="393fd2c4b06a9598"></a>
### --home

Database의 home directory를 설정한다.  
Default value는 $GOLDILOCKS_HOME 환경 변수를 사용한다.

<a id="d5bc7106aeffd45a"></a>
### --member

Cluster 환경에서 local database의 이름을 설정한다.

<a id="622ee6ae4839c872"></a>
### --host

Cluster 환경에서 local database의 host address를 설정한다.

<a id="ddbaf2cd239c3523"></a>
### --port

Cluster 환경에서 local database의 port 번호를 설정한다.

<a id="471c6402b3ad3711"></a>
### --silent

결과 메시지를 출력하지 않는다.

<a id="96de6a657baeb8fd"></a>
### --help

Help 메시지를 출력한다.

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

[← 41. Hibernate](../part-05-developer-manual/41-hibernate.md) · [전체 목차](../README.md) · [43. glsnr →](43-glsnr.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
