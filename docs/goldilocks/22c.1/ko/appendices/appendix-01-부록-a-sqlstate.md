<a id="aa6c242290586c73"></a>

# 부록 A. SQLSTATE

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/aa6c242290586c73)  
> 태그: `22c.1_10_tag`

[← 52. CYFILE](../part-07-replication/52-cyfile.md) · [전체 목차](../README.md) · [부록 B. Error Codes →](appendix-02-부록-b-error-codes.md)

SQL 표준 ISO-9075 에서 정의한 SQLSTATE 는 다음과 같다.

SQLSTATE 의 앞 두 글자는 class 이고, 뒤 세 글자는 subclass 이다.

Class의 첫 글자와 subclass의 첫 글자 (세 번째 글자) 중에 아래 문자들은 SQL 표준에서 정의된 영역에 속하는 문자이므로, vendor-specific SQLSTATE는 다른 문자를 사용하여 정의되어야 한다.

- Reserved SQLSTATE character
    - '0', '1', '2', '3', '4'
    - 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H'

참고로 ODBC 표준 (SQL 표준이 아님) 은 아래와 같은 character 를 사용한다.

- Class 의 첫 글자: 대문자 'I'
- Subclass 의 첫 글자: 'S'

Goldilocks 에서 자체 정의한 SQLSTATE 는 아래와 같은 character 를 사용한다.

- Class 의 첫 글자: 'R'
- Subclass 의 첫 글자: 'R'

**00 class : successful completion**

<a id="fa88bff812732d37"></a>
| SQLSTATE | description |
| --- | --- |
| 00000 | successful completion: general |

**01 class : warning**

<a id="1e59044c7442f14e"></a>
| SQLSTATE | description |
| --- | --- |
| 01000 | general warning |
| 01001 | warning: cursor operation conflict |
| 01002 | warning: disconnect error |
| 01003 | warning: null value eliminated in set function |
| 01004 | warning: string data, right truncation |
| 01005 | warning: insufficient item descriptor areas |
| 01006 | warning: privilege not revoked |
| 01007 | warning: privilege not granted |
| 01009 | warning: search condition too long for information schema |
| 0100A | warning: query expression too long for information schema |
| 0100B | warning: default value too long for information schema |
| 0100C | warning: result sets returned |
| 0100D | warning: additional result sets returned |
| 0100E | warning: attempt to return too many result sets |
| 0100F | warning: statement too long for information schema |
| 01010 | warning: column cannot be mapped |
| 01011 | warning : SQL-Java path too long for information schema |
| 01012 | warning: invalid number of conditions |
| 0102F | warning: array data, right truncation |
| 01S00 | warning: invalid connection string attribute |
| 01S01 | warning: error in row |
| 01S02 | warning: option value changed |
| 01S06 | warning: attempt to fetch before the result set returned the first rowset |
| 01S07 | warning: fractional truncation |
| 01S08 | warning: error saving File DSN |
| 01S09 | warning: invalid keyword |

**02 class : no data**

<a id="23906a17c6a9cea8"></a>
| SQLSTATE | description |
| --- | --- |
| 02000 | no data: general |
| 02001 | no data: no additional result sets returned |

**07 class : dynamic SQL error**

<a id="d8e3754365d406e2"></a>
| SQLSTATE | description |
| --- | --- |
| 07000 | dynamic SQL error: general |
| 07001 | dynamic SQL error: using clause does not match dynamic parameter specifications |
| 07002 | dynamic SQL error: using clause does not match target specifications |
| 07003 | dynamic SQL error: cursor specification cannot be executed |
| 07004 | dynamic SQL error: using clause required for dynamic parameters |
| 07005 | dynamic SQL error: prepared statement not a cursor specification |
| 07006 | dynamic SQL error: restricted data type attribute violation |
| 07007 | dynamic SQL error: using clause required for result fields |
| 07008 | dynamic SQL error: invalid descriptor count |
| 07009 | dynamic SQL error: invalid descriptor index |
| 0700B | dynamic SQL error: data type transform function violation |
| 0700C | dynamic SQL error: undefined DATA value |
| 0700D | dynamic SQL error: invalid DATA target |
| 0700E | dynamic SQL error: invalid LEVEL value |
| 0700F | dynamic SQL error: invalid DATETIME_INTERVAL_CODE |
| 07S01 | dynamic SQL error: invalid use of default parameter |

**08 class : connection exception**

<a id="889f1d7c9b6406e7"></a>
| SQLSTATE | description |
| --- | --- |
| 08000 | connection exception: general |
| 08001 | connection exception: SQL-client unable to establish SQL-connection |
| 08002 | connection exception: connection name in use |
| 08003 | connection exception: connection does not exist |
| 08004 | connection exception: SQL-server rejected establishment of SQL-connection |
| 08006 | connection exception: connection failure |
| 08007 | connection exception: transaction resolution unknown |
| 08S01 | connection exception: communication link failure |

**09 class : triggered action exception**

<a id="3508a28bc0856c11"></a>
| SQLSTATE | description |
| --- | --- |
| 09000 | triggered action exception: general |

**0A class : feature not supported**

<a id="78d915d3551ff17c"></a>
| SQLSTATE | description |
| --- | --- |
| 0A000 | feature not supported: general error |
| 0A001 | feature not supported: multiple server transactions |

**0D class : invalid target type specification**

<a id="c0c49ef05bb97bc1"></a>
| SQLSTATE | description |
| --- | --- |
| 0D000 | invalid target type specification: general |

**0E class : invalid schema name list specification**

<a id="80cec104df896c46"></a>
| SQLSTATE | description |
| --- | --- |
| 0E000 | invalid schema name list specification: general |

**0F class : locator exception**

<a id="9434110174ab8ec2"></a>
| SQLSTATE | description |
| --- | --- |
| 0F000 | locator exception: general |
| 0F001 | locator exception: invalid specification |

**0K class : resignal when handler not active**

<a id="3a4e159f938be394"></a>
| SQLSTATE | description |
| --- | --- |
| 0K000 | resignal when handler not active: general |

**0L class : invalid grantor**

<a id="b1499d7113969c10"></a>
| SQLSTATE | description |
| --- | --- |
| 0L000 | invalid grantor: general |

**0M class : invalid SQL-invoked procedure reference**

<a id="96603892f64000d4"></a>
| SQLSTATE | description |
| --- | --- |
| 0M000 | invalid SQL-invoked procedure reference: general |

**0N class : SQL/XML mapping error**

<a id="4cc32d6bcad90b8e"></a>
| SQLSTATE | description |
| --- | --- |
| 0N000 | SQL/XML mapping error: general |
| 0N001 | SQL/XML mapping error: unmappable XML Name |
| 0N002 | SQL/XML mapping error: invalid XML character |

**0P class : invalid role specification**

<a id="bbd97dda3605a7f5"></a>
| SQLSTATE | description |
| --- | --- |
| 0P000 | invalid role specification: general |

**0S class : invalid transform group name specification**

<a id="119df80d35585c98"></a>
| SQLSTATE | description |
| --- | --- |
| 0S000 | invalid transform group name specification: general |

**0T class : target table disagrees with cursor specification**

<a id="f59760c499bb6a86"></a>
| SQLSTATE | description |
| --- | --- |
| 0T000 | target table disagrees with cursor specification: general |

**0U class : attempt to assign to non-updatable**

<a id="c0d602b914b88045"></a>
| SQLSTATE | description |
| --- | --- |
| 0U000 | attempt to assign to non-updatable: general |

**0V class : attempt to assign to ordering column**

<a id="f563af70985707dc"></a>
| SQLSTATE | description |
| --- | --- |
| 0V000 | attempt to assign to ordering column: general |

**0W class : prohibited statement encountered during trigger execution**

<a id="fc305122456b1874"></a>
| SQLSTATE | description |
| --- | --- |
| 0W000 | prohibited statement encountered during trigger execution: general |
| 0W001 | prohibited statement encountered during trigger execution: modify table modified by data change delta table |

**0X class : invalid foreign server specification**

<a id="0e9c2e4288790d66"></a>
| SQLSTATE | description |
| --- | --- |
| 0X000 | invalid foreign server specification: general |

**0Y class : pass-through specific condition**

<a id="93e2d13b37c9bf86"></a>
| SQLSTATE | description |
| --- | --- |
| 0Y000 | pass-through specific condition: general |
| 0Y001 | pass-through specific condition: invalid cursor option |
| 0Y002 | pass-through specific condition: invalid cursor allocation |

**0Z class : diagnostics exception**

<a id="6de1038ee8a0b430"></a>
| SQLSTATE | description |
| --- | --- |
| 0Z000 | diagnostics exception: general |
| 0Z001 | diagnostics exception: maximum number of stacked diagnostics areas exceeded |
| 0Z002 | diagnostics exception: stacked diagnostics accessed without active handler |

**10 class : XQuery error**

<a id="51d919743b08613b"></a>
| SQLSTATE | description |
| --- | --- |
| 10000 | XQuery error: general |

**20 class : case not found for case statement**

<a id="b6406df43e98a62e"></a>
| SQLSTATE | description |
| --- | --- |
| 20000 | case not found for case statement: general |

**21 class : cardinality violation**

<a id="646f1d524d143839"></a>
| SQLSTATE | description |
| --- | --- |
| 21000 | cardinality violation: general |
| 21S01 | cardinality violation: insert value list does not match column list |
| 21S02 | cardinality violation: degree of derived table does not match column list |

**22 class : data exception**

<a id="7344b2f56027d5fd"></a>
| SQLSTATE | description |
| --- | --- |
| 22000 | data exception: general |
| 22001 | data exception: string data, right truncation |
| 22002 | data exception: null value, no indicator parameter |
| 22003 | data exception: numeric value out of range |
| 22004 | data exception: null value not allowed |
| 22005 | data exception: error in assignment |
| 22006 | data exception: invalid interval format |
| 22007 | data exception: invalid datetime format |
| 22008 | data exception: datetime field overflow |
| 22009 | data exception: invalid time zone displacement value |
| 2200B | data exception: escape character conflict |
| 2200C | data exception: invalid use of escape character |
| 2200D | data exception: invalid escape octet |
| 2200E | data exception: null value in array target |
| 2200F | data exception: zero-length character string |
| 2200G | data exception: most specific type mismatch |
| 2200H | data exception: sequence generator limit exceeded |
| 2200J | data exception: nonidentical notations with the same name |
| 2200K | data exception: nonidentical unparsed entities with the same name |
| 2200L | data exception: not an XML document |
| 2200M | data exception: invalid XML document |
| 2200N | data exception: invalid XML content |
| 2200P | data exception: interval value out of range |
| 2200Q | data exception: multiset value overflow |
| 2200R | data exception: XML value overflow |
| 2200S | data exception: invalid comment |
| 2200T | data exception: invalid processing instruction |
| 2200U | data exception: not an XQuery document node |
| 2200V | data exception: invalid XQuery context item |
| 2200W | data exception: XQuery serialization error |
| 22010 | data exception: invalid indicator parameter value |
| 22011 | data exception: substring error |
| 22012 | data exception: division by zero |
| 22013 | data exception: invalid preceding or following size in window function |
| 22014 | data exception: invalid argument for NTILE function |
| 22015 | data exception: interval field overflow |
| 22016 | data exception: invalid argument for NTH_VALUE function |
| 22017 | data exception: invalid data specified for datalink |
| 22018 | data exception: invalid character value for cast |
| 22019 | data exception: invalid escape character |
| 2201A | data exception: null argument passed to datalink constructor |
| 2201B | data exception: invalid regular expression |
| 2201C | data exception: null row not permitted in table |
| 2201D | data exception: datalink value exceeds maximum length |
| 2201E | data exception: invalid argument for natural logarithm |
| 2201F | data exception: invalid argument for power function |
| 2201G | data exception: invalid argument for width bucket function |
| 2201H | data exception: invalid row version |
| 2201J | data exception: XQuery sequence cannot be validated |
| 2201K | data exception: XQuery document node cannot be validated |
| 2201L | data exception: no XML schema found |
| 2201M | data exception: element namespace not declared |
| 2201N | data exception: global element not declared |
| 2201P | data exception: no XML element with the specified QName |
| 2201Q | data exception: no XML element with the specified namespace |
| 2201R | data exception: validation failure |
| 2201S | data exception: invalid XQuery regular expression |
| 2201T | data exception: invalid XQuery option flag |
| 2201U | data exception: attempt to replace a zero-length string |
| 2201V | data exception: invalid XQuery replacement string |
| 2201W | data exception: invalid row count in fetch first clause |
| 2201X | data exception: invalid row count in result offset clause |
| 22021 | data exception: character not in repertoire |
| 22022 | data exception: indicator overflow |
| 22023 | data exception: invalid parameter value |
| 22024 | data exception: unterminated C string |
| 22025 | data exception: invalid escape sequence |
| 22026 | data exception: string data, length mismatch |
| 22027 | data exception: trim error |
| 22029 | data exception: noncharacter in UCS string |
| 2202A | data exception: null value in field reference |
| 2202D | data exception: null value substituted for mutator subject parameter |
| 2202E | data exception: array element error |
| 2202F | data exception: array data, right truncation |
| 2202G | data exception: invalid repeat argument in a sample clause |
| 2202H | data exception: invalid sample size |

**23 class : integrity constraint violation**

<a id="5974be82830705a8"></a>
| SQLSTATE | description |
| --- | --- |
| 23000 | integrity constraint violation: general |
| 23001 | integrity constraint violation: restrict violation |

**24 class : invalid cursor state**

<a id="06f399090b08926c"></a>
| SQLSTATE | description |
| --- | --- |
| 24000 | invalid cursor state: general |

**25 class : invalid transaction state**

<a id="4a6d4d0e32026c0d"></a>
| SQLSTATE | description |
| --- | --- |
| 25000 | invalid transaction state: general |
| 25001 | invalid transaction state: active SQL-transaction |
| 25002 | invalid transaction state: branch transaction already active |
| 25003 | invalid transaction state: inappropriate access mode for branch transaction |
| 25004 | invalid transaction state: inappropriate isolation level for branch transaction |
| 25005 | invalid transaction state: no active SQL-transaction for branch transaction |
| 25006 | invalid transaction state: read-only SQL-transaction |
| 25007 | invalid transaction state: schema and data statement mixing not supported |
| 25008 | invalid transaction state: held cursor requires same isolation level |
| 25S01 | invalid transaction state: transaction state |
| 25S02 | invalid transaction state: transaction is still active |
| 25S03 | invalid transaction state: transaction is rolled back |

**26 class : invalid SQL statement name**

<a id="78716212eddcd1a6"></a>
| SQLSTATE | description |
| --- | --- |
| 26000 | invalid SQL statement name: general |

**27 class : triggered data change violation**

<a id="0b7009b0f2fc2dcc"></a>
| SQLSTATE | description |
| --- | --- |
| 27000 | triggered data change violation: general |
| 27001 | triggered data change violation: modify table modified by data change delta table |

**28 class : invalid authorization specification**

<a id="f5f25ac73559975f"></a>
| SQLSTATE | description |
| --- | --- |
| 28000 | invalid authorization specification: general |

**2B class : dependent privilege descriptors**

<a id="88a6a59c30e0d08b"></a>
| SQLSTATE | description |
| --- | --- |
| 2B000 | dependent privilege descriptors: general |

**2C class : invalid character set name**

<a id="abe1d6d71f0a1a0e"></a>
| SQLSTATE | description |
| --- | --- |
| 2C000 | invalid character set name: general |

**2D class : invalid transaction termination**

<a id="3f12368646dae32b"></a>
| SQLSTATE | description |
| --- | --- |
| 2D000 | invalid transaction termination: general |

**2E class : invalid connection name**

<a id="b0dfae37780d87e5"></a>
| SQLSTATE | description |
| --- | --- |
| 2E000 | invalid connection name: general |

**2F class : SQL routine exception**

<a id="650dfe25c290046b"></a>
| SQLSTATE | description |
| --- | --- |
| 2F000 | SQL routine exception: general |
| 2F002 | SQL routine exception: modifying SQL-data not permitted |
| 2F003 | SQL routine exception: prohibited SQL-statement attempted |
| 2F004 | SQL routine exception: reading SQL-data not permitted |
| 2F005 | SQL routine exception: function executed no return statement |

**2H class : invalid collation name**

<a id="0b9ed7001d09ca82"></a>
| SQLSTATE | description |
| --- | --- |
| 2H000 | invalid collation name: general |

**30 class : invalid SQL statement identifier**

<a id="3558b2f0f16f54fe"></a>
| SQLSTATE | description |
| --- | --- |
| 30000 | invalid SQL statement identifier: general |

**33 class : invalid SQL descriptor name**

<a id="ada3bd88f5c126d3"></a>
| SQLSTATE | description |
| --- | --- |
| 33000 | invalid SQL descriptor name: general |

**34 class : invalid cursor name**

<a id="f30b4aba3f65dfd6"></a>
| SQLSTATE | description |
| --- | --- |
| 34000 | invalid cursor name: general |

**35 class : invalid condition number**

<a id="0fd9e2a7ebe92643"></a>
| SQLSTATE | description |
| --- | --- |
| 35000 | invalid condition number: general |

**36 class : cursor sensitivity exception**

<a id="d1ac611eaf0719e8"></a>
| SQLSTATE | description |
| --- | --- |
| 36000 | cursor sensitivity exception: general |
| 36001 | cursor sensitivity exception: request rejected |
| 36002 | cursor sensitivity exception: request failed |

**38 class : external routine exception**

<a id="4f14e07672de00c1"></a>
| SQLSTATE | description |
| --- | --- |
| 38000 | external routine exception: general |
| 38001 | external routine exception: containing SQL not permitted |
| 38002 | external routine exception: modifying SQL-data not permitted |
| 38003 | external routine exception: prohibited SQL-statement attempted |
| 38004 | external routine exception: reading SQL-data not permitted |

**39 class : external routine invocation exception**

<a id="ca221716009cc97a"></a>
| SQLSTATE | description |
| --- | --- |
| 39000 | external routine invocation exception: general |
| 39004 | external routine invocation exception: null value not allowed |

**3B class : savepoint exception**

<a id="451d510f84f08f01"></a>
| SQLSTATE | description |
| --- | --- |
| 3B000 | savepoint exception: general |
| 3B001 | savepoint exception: invalid specification |
| 3B002 | savepoint exception: too many |

**3C class : ambiguous cursor name**

<a id="c92124549b69c1a5"></a>
| SQLSTATE | description |
| --- | --- |
| 3C000 | ambiguous cursor name: general |

**3D class : invalid catalog name**

<a id="bcac314e3a914281"></a>
| SQLSTATE | description |
| --- | --- |
| 3D000 | invalid catalog name: general |

**3F class : invalid schema name**

<a id="08663567e80117e7"></a>
| SQLSTATE | description |
| --- | --- |
| 3F000 | invalid schema name: general |

**40 class : transaction rollback**

<a id="fd9e572e4b0cafba"></a>
| SQLSTATE | description |
| --- | --- |
| 40000 | transaction rollback: general |
| 40001 | transaction rollback: serialization failure |
| 40002 | transaction rollback: integrity constraint violation |
| 40003 | transaction rollback: statement completion unknown |
| 40004 | transaction rollback: triggered action exception |

**42 class : syntax error or access rule violation**

<a id="4be575dcb29ecf80"></a>
| SQLSTATE | description |
| --- | --- |
| 42000 | syntax error or access rule violation: general |
| 42R01 | syntax error or access rule violation: (cluster DML failure) unable to access remote data |
| 42R02 | syntax error or access rule violation: (cluster DDL failure) unable to access cluster member |
| 42S01 | syntax error or access rule violation: base table or view already exists |
| 42S02 | syntax error or access rule violation: base table or view not found |
| 42S11 | syntax error or access rule violation: index already exists |
| 42S12 | syntax error or access rule violation: index not found |
| 42S21 | syntax error or access rule violation: column already exists |
| 42S22 | syntax error or access rule violation: column not found |

**44 class : with check option violation**

<a id="b4e12f46f60376bd"></a>
| SQLSTATE | description |
| --- | --- |
| 44000 | with check option violation: general |

**45 class : unhandled user-defined exception**

<a id="995284a3f263a614"></a>
| SQLSTATE | description |
| --- | --- |
| 45000 | unhandled user-defined exception: general |

**46 class : Java Execution**

<a id="f8fa927e1d12249d"></a>
| SQLSTATE | description |
| --- | --- |
| 46000 | Java Execution: general |
| 46001 | Java DDL: invalid URL |
| 46002 | Java DDL: invalid JAR name |
| 46003 | Java DDL: invalid class deletion |
| 46005 | Java DDL: invalid replacement |
| 4600A | Java DDL: attempt to replace uninstalled JAR |
| 4600B | Java DDL: attempt to remove uninstalled JAR |
| 4600C | Java DDL: invalid JAR removal |
| 4600D | Java DDL: invalid path |
| 4600E | Java DDL: self-referencing path |
| 46102 | Java execution: invalid JAR name in path |
| 46103 | Java execution: unresolved class name |
| 46110 | OLB-specific error: unsupported feature |
| 46120 | OLB-specific error: invalid class declaration |
| 46121 | OLB-specific error: invalid column name |
| 46122 | OLB-specific error: invalid number of columns |
| 46130 | OLB-specific error: invalid profile state |

**HV class : FDW-specific condition**

<a id="a80f8c4f02fe75d5"></a>
| SQLSTATE | description |
| --- | --- |
| HV000 | FDW-specific condition: general |
| HV001 | FDW-specific condition: memory allocation error |
| HV002 | FDW-specific condition: dynamic parameter value needed |
| HV004 | FDW-specific condition: invalid data type |
| HV005 | FDW-specific condition: column name not found |
| HV006 | FDW-specific condition: invalid data type descriptors |
| HV007 | FDW-specific condition: invalid column name |
| HV008 | FDW-specific condition: invalid column number |
| HV009 | FDW-specific condition: invalid use of null pointer |
| HV00A | FDW-specific condition: invalid string format |
| HV00B | FDW-specific condition: invalid handle |
| HV00C | FDW-specific condition: invalid option index |
| HV00D | FDW-specific condition: invalid option name |
| HV00J | FDW-specific condition: option name not found |
| HV00K | FDW-specific condition: reply handle |
| HV00L | FDW-specific condition: unable to create execution |
| HV00M | FDW-specific condition: unable to create reply |
| HV00N | FDW-specific condition: unable to establish connection |
| HV00P | FDW-specific condition: no schemas |
| HV00Q | FDW-specific condition: schema not found |
| HV00R | FDW-specific condition: table not found |
| HV010 | FDW-specific condition: function sequence error |
| HV014 | FDW-specific condition: limit on number of handles exceeded |
| HV021 | FDW-specific condition: inconsistent descriptor information |
| HV024 | FDW-specific condition: invalid attribute value |
| HV090 | FDW-specific condition: invalid string length or buffer length |
| HV091 | FDW-specific condition: invalid descriptor field identifier |

**HW class : datalink exception**

<a id="2de43c9f492fd560"></a>
| SQLSTATE | description |
| --- | --- |
| HW000 | datalink exception: general |
| HW001 | datalink exception: external file not linked |
| HW002 | datalink exception: external file already linked |
| HW003 | datalink exception: referenced file does not exist |
| HW004 | datalink exception: invalid write token |
| HW005 | datalink exception: invalid datalink construction |
| HW006 | datalink exception: invalid write permission for update |
| HW007 | datalink exception: referenced file not valid |

**HY class : CLI-specific condition**

<a id="f9445debe69b7f8d"></a>
| SQLSTATE | description |
| --- | --- |
| HY000 | general error |
| HY001 | CLI-specific condition: memory allocation error |
| HY003 | CLI-specific condition: invalid data type in application descriptor |
| HY004 | CLI-specific condition: invalid data type |
| HY007 | CLI-specific condition: associated statement is not prepared |
| HY008 | CLI-specific condition: operation canceled |
| HY009 | CLI-specific condition: invalid use of null pointer |
| HY010 | CLI-specific condition: function sequence error |
| HY011 | CLI-specific condition: attribute cannot be set now |
| HY012 | CLI-specific condition: invalid transaction operation code |
| HY013 | CLI-specific condition: memory management error |
| HY014 | CLI-specific condition: limit on number of handles exceeded |
| HY015 | CLI-specific condition: no cursor name available |
| HY016 | CLI-specific condition: cannot modify an implementation row descriptor |
| HY017 | CLI-specific condition: invalid use of automatically allocated descriptor handle |
| HY018 | CLI-specific condition: server declined the cancellation request |
| HY019 | CLI-specific condition: non-string data cannot be sent in pieces |
| HY020 | CLI-specific condition: attempt to concatenate a null value |
| HY021 | CLI-specific condition: inconsistent descriptor information |
| HY024 | CLI-specific condition: invalid attribute value |
| HY055 | CLI-specific condition: non-string data cannot be used with string routine |
| HY090 | CLI-specific condition: invalid string length or buffer length |
| HY091 | CLI-specific condition: invalid descriptor field identifier |
| HY092 | CLI-specific condition: invalid attribute identifier |
| HY093 | CLI-specific condition: invalid datalink value |
| HY095 | CLI-specific condition: invalid FunctionId specified |
| HY096 | CLI-specific condition: invalid information type |
| HY097 | CLI-specific condition: column type out of range |
| HY098 | CLI-specific condition: scope out of range |
| HY099 | CLI-specific condition: nullable type out of range |
| HY100 | CLI-specific condition: uniqueness option type out of range |
| HY101 | CLI-specific condition: accuracy option type out of range |
| HY103 | CLI-specific condition: invalid retrieval code |
| HY104 | CLI-specific condition: invalid Length/Precision value |
| HY105 | CLI-specific condition: invalid parameter mode |
| HY106 | CLI-specific condition: invalid fetch orientation |
| HY107 | CLI-specific condition: row value out of range |
| HY109 | CLI-specific condition: invalid cursor position |
| HY110 | CLI-specific condition: invalid driver completion |
| HY111 | CLI-specific condition: invalid bookmark value |
| HYC00 | CLI-specific condition: optional feature not implemented |
| HYT00 | CLI-specific condition: timeout expired |
| HYT01 | CLI-specific condition: connection timeout expired |

**HZ class : Remote Database Access**

<a id="d9c6b87821575460"></a>
| SQLSTATE | description |
| --- | --- |
| HZ000 | Remote Database Access: general |

**IM class : ODBC driver manager**

<a id="e1f08658dde473ef"></a>
| SQLSTATE | description |
| --- | --- |
| IM001 | Driver does not support this function |
| IM002 | Data source name not found and no default driver specified |
| IM003 | Specified driver could not be loaded |
| IM004 | Driver's SQLAllocHandle on SQL_HANDLE_ENV failed |
| IM005 | Driver's SQLAllocHandle on SQL_HANDLE_DBC failed |
| IM006 | Driver's SQLSetConnectAttr failed |
| IM007 | No data source or driver specified; dialog prohibited |
| IM008 | Dialog failed |
| IM009 | Unable to load translation DLL |
| IM010 | Data source name too long |
| IM011 | Driver name too long |
| IM012 | DRIVER keyword syntax error |
| IM013 | Trace file error |
| IM014 | Invalid name of File DSN |
| IM015 | Corrupt file data source |

**RD class : Database resource exception**

<a id="d9c61fffef02b854"></a>
| SQLSTATE | description |
| --- | --- |
| RD000 | Database resource exception: general |

**RP class : Operating system resource exception**

<a id="446547a988c4c8ff"></a>
| SQLSTATE | description |
| --- | --- |
| RP000 | Operating system resource exception: general |

---

[← 52. CYFILE](../part-07-replication/52-cyfile.md) · [전체 목차](../README.md) · [부록 B. Error Codes →](appendix-02-부록-b-error-codes.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
