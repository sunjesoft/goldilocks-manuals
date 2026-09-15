<a id="bfba78fd70c355ec"></a>

# 37. gcreatedb

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/bfba78fd70c355ec)  
> 태그: `21c.1_35_tag`

[← 36. Hibernate](../part-05-developer-manual/36-hibernate.md) · [전체 목차](../README.md) · [38. glsnr →](38-glsnr.md)

<a id="49beb195306c458d"></a>
## gcreatedb 소개

<a id="713085afceca7662"></a>
### 정의

gcreatedb는 GOLDILOCKS에서 제공하는 데이터베이스 생성 유틸리티이다.

<a id="3bbc604f0c8b4569"></a>
### 기능

사용자가 지정한 DB-name, comment, time zone, character set으로 새로운 데이터베이스를 생성한다.

<a id="664cb12abc2e8d74"></a>
### 사용법

```
gcreatedb [options]
```

<a id="141ca7fd3b25e976"></a>
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

<a id="513baab467ad4747"></a>
### 사용 예

```
$ gcreatedb --db_name="goldilocks" --db-comment="goldilocks database" --timezone="+09:00" --character_set="UTF8" --silent
```

<a id="d434830ce87eccdc"></a>
## Command Option

<a id="95dd85d53b6d7b8d"></a>
### --cluster

Cluster 환경의 database를 생성한다.   
이를 사용하지 않을 경우 stand alone database를 생성한다.

<a id="ffc76a9e68e3683f"></a>
### --db_name

사용자가 생성하려는 database name을 지정한다.   
Default value는 "goldilocks"이다.  
Database name의 최대 길이는 128 이다.

<a id="c8d1e20deaf7a131"></a>
### --db_comment

사용자가 생성하려는 database comment를 지정한다.   
Default value는 "goldilocks database" 이다.   
Database comment의 최대 길이는 1024 이다.

<a id="d04c1630c7d1defa"></a>
### --timezone

Database의 time zone 값이다.  
Default value는 property의 [TIMEZONE](../part-02-administration-manual/10-server-property.md#f49a6d4b79974d75) 값이다.  
Database를 생성할 때 적용되는 속성으로써 '-14:00' ~ '+14:00' 범위의 값을 사용할 수 있다.

<a id="e1745899df295051"></a>
### --character_set

Database의 character set이다.  
Default value는 property의 [CHARACTER_SET](../part-02-administration-manual/10-server-property.md#752cf14717dffe5e) 값이다.

Database를 생성할 때 적용되는 속성으로써 다음 중 하나의 값으로 설정할 수 있다.  
• GB18030  
• SQL_ASCII  
• UHC  
• UTF8

<a id="eb2907d063b9a5d9"></a>
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

Default value는 property의 [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#b205bdf9941e1ed4) 값이다.

Database를 생성할 때 적용되는 속성으로써 다음 중 하나의 값으로 설정할 수 있다.  
• OCTETS: Byte 수를 의미한다.  
• CHARACTERS: 문자 개수를 의미한다.

SQL 표준은 기본값을 CHARACTERS로 정의하고 있으며 다른 DBMS들의 char length unit 기본값은 다음과 같다.


> 
> - Oracle과 DB2에서는 OCTETS를 사용한다.
> - MS-SQL, MySQL, PostgreSQL에서는 CHARACTERS를 사용한다.
> 

<a id="415efd1e7bc3e568"></a>
### --home

Database의 home directory를 설정한다.  
Default value는 $GOLDILOCKS_HOME 환경 변수를 사용한다.

<a id="1b0089da29390c21"></a>
### --member

Cluster 환경에서 local database의 이름을 설정한다.

<a id="18420a955995d51b"></a>
### --host

Cluster 환경에서 local database의 host address를 설정한다.

<a id="60e4d7f8f9ccd531"></a>
### --port

Cluster 환경에서 local database의 port 번호를 설정한다.

<a id="cf3afd91475da7b8"></a>
### --silent

결과 메시지를 출력하지 않는다.

<a id="e8beb990c847ea11"></a>
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
