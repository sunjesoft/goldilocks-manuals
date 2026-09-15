<a id="72e54e019eaf63fa"></a>

# 37. gcreatedb

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/72e54e019eaf63fa)  
> 태그: `22c.1_10_tag`

[← 36. Hibernate](../part-05-developer-manual/36-hibernate.md) · [전체 목차](../README.md) · [38. glsnr →](38-glsnr.md)

<a id="7d7428fa1dde5360"></a>
## gcreatedb 소개

<a id="e020128fac0edbfc"></a>
### 정의

gcreatedb는 GOLDILOCKS에서 제공하는 데이터베이스 생성 유틸리티이다.

<a id="99425cb29fec908f"></a>
### 기능

사용자가 지정한 DB-name, comment, time zone, character set으로 새로운 데이터베이스를 생성한다.

<a id="719ee35e6a365393"></a>
### 사용법

```
gcreatedb [options]
```

<a id="5a0f2bab91d51c9c"></a>
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

<a id="6f0c74df2b523afa"></a>
### 사용 예

```
$ gcreatedb --db_name="goldilocks" --db-comment="goldilocks database" --timezone="+09:00" --character_set="UTF8" --silent
```

<a id="c5f22db55659684b"></a>
## Command Option

<a id="65c1e1550ddd69c8"></a>
### --cluster

Cluster 환경의 database를 생성한다.   
이를 사용하지 않을 경우 stand alone database를 생성한다.

<a id="68a3ba2b4a3265d2"></a>
### --db_name

사용자가 생성하려는 database name을 지정한다.   
Default value는 "goldilocks"이다.  
Database name의 최대 길이는 128 이다.

<a id="ddcce7d540929284"></a>
### --db_comment

사용자가 생성하려는 database comment를 지정한다.   
Default value는 "goldilocks database" 이다.   
Database comment의 최대 길이는 1024 이다.

<a id="85134f5e43b92693"></a>
### --timezone

Database의 time zone 값이다.  
Default value는 property의 [TIMEZONE](../part-02-administration-manual/10-server-property.md#5525e5bf3452dfa7) 값이다.  
Database를 생성할 때 적용되는 속성으로써 '-14:00' ~ '+14:00' 범위의 값을 사용할 수 있다.

<a id="ba4829956a6608f2"></a>
### --character_set

Database의 character set이다.  
Default value는 property의 [CHARACTER_SET](../part-02-administration-manual/10-server-property.md#38891a7d14cc44ed) 값이다.

Database를 생성할 때 적용되는 속성으로써 다음 중 하나의 값으로 설정할 수 있다.  
• GB18030  
• SQL_ASCII  
• UHC  
• UTF8

<a id="9b486225db81fb40"></a>
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

Default value는 property의 [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#4f053a478d278f9f) 값이다.

Database를 생성할 때 적용되는 속성으로써 다음 중 하나의 값으로 설정할 수 있다.  
• OCTETS: Byte 수를 의미한다.  
• CHARACTERS: 문자 개수를 의미한다.

SQL 표준은 기본값을 CHARACTERS로 정의하고 있으며 다른 DBMS들의 char length unit 기본값은 다음과 같다.


> 
> - Oracle과 DB2에서는 OCTETS를 사용한다.
> - MS-SQL, MySQL, PostgreSQL에서는 CHARACTERS를 사용한다.
> 

<a id="5148eb14873abd07"></a>
### --home

Database의 home directory를 설정한다.  
Default value는 $GOLDILOCKS_HOME 환경 변수를 사용한다.

<a id="d99ffd5ed41b68e0"></a>
### --member

Cluster 환경에서 local database의 이름을 설정한다.

<a id="b077e069ea7d27d2"></a>
### --host

Cluster 환경에서 local database의 host address를 설정한다.

<a id="dd6b60f4ab0c61ce"></a>
### --port

Cluster 환경에서 local database의 port 번호를 설정한다.

<a id="e017a79a9724eb2f"></a>
### --silent

결과 메시지를 출력하지 않는다.

<a id="9a45addb135e13e5"></a>
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

[← 36. Hibernate](../part-05-developer-manual/36-hibernate.md) · [전체 목차](../README.md) · [38. glsnr →](38-glsnr.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
