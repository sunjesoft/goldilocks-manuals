<a id="c0114970637ab47d"></a>

# 17. Built-in Function References

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/c0114970637ab47d)  
> Tag: `20c.1_30_tag`

[← 16. Built-in Data Type References](16-built-in-data-type-references.md) · [Table of contents](../README.md) · [18. SQL References →](18-sql-references.md)

<a id="fb2da38cea7a5685"></a>
## * (MULTIPLICATION)

<a id="63e9f2e2a4118ea2"></a>
### Syntax

```
expr1 * expr2
```

<a id="eca769c5b021bdc7"></a>
### Description

It returns the multiplication result of expr1 and expr2.

The multiplication types and result types are as follows.  
For more information, refer to [Type Conversion](11-sql-elements.md#e4c62967f1fb488d).

**Numeric * operation**

<a id="f58f229fdd9742a6"></a>
| expr1 (expr2) | expr2 (expr1) | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="6ecf6a947cd4d100"></a>
<table class="table column_count_3"><caption>INTERVAL * operation</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type is the interval type.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type is the interval type.)</div></td></tr><tr><td class="to_left" colspan="3"><div>Refer to <a class="reference text" href="#53d83238fe334f17">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

**INTERVAL type details which is included in INTERVAL type written in the following table**

<a id="53d83238fe334f17"></a>
<table><thead><tr><th align="center">INTERVAL YEAR TO MONTH</th><th align="center">INTERVAL DAY TO SECOND</th></tr></thead><tbody><tr><td valign="middle"><ul><li>INTERVAL YEAR</li><li>INTERVAL MONTH</li><li>INTERVAL YEAR TO MONTH</li></ul></td><td valign="middle"><ul><li>INTERVAL DAY</li><li>INTERVAL HOUR</li><li>INTERVAL MINUTE</li><li>INTERVAL SECOND</li><li>INTERVAL DAY TO HOUR</li><li>INTERVAL DAY TO MINUTE</li><li>INTERVAL DAY TO SECOND</li><li>INTERVAL HOUR TO MINUTE</li><li>INTERVAL HOUR TO SECOND</li><li>INTERVAL MINUTE TO SECOND</li></ul></td></tr></tbody></table>

<a id="ad8617727fa42629"></a>
### Example

```
gSQL> SELECT INTERVAL'1-2'YEAR TO MONTH * 2 AS RESULT FROM DUAL;
RESULT    
----------
+000002-04
1 row selected.

gSQL> SELECT INTERVAL'1 01:02:03.400000'DAY TO SECOND * 2 AS RESULT 
      FROM DUAL;
RESULT                 
-----------------------
+000002 02:04:06.800000
1 row selected.
```

<a id="c5baaa65c70cf68b"></a>
## + (ADDITION)

<a id="c410166a31be0570"></a>
### Syntax

```
expr1 + expr2
```

<a id="35e00bcbe9925dc7"></a>
### Description

It returns the addition result of expr1 and expr2.

The addition types and result types are as follows.  
For more information, refer to [Type Conversion](11-sql-elements.md#e4c62967f1fb488d).

**Numeric + operation**

<a id="99cfe7774e3b2b6d"></a>
| expr1 (expr2) | expr2 (expr1) | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="df6803255369d10d"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) + operation</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference text" href="#53d83238fe334f17">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="dc4e2b9f3f07792c"></a>
### Example

```
gSQL> SELECT TO_DATE( '2012-05-05', 'YYYY-MM-DD' ) + 5 AS RESULT FROM DUAL;
RESULT    
----------
2012-05-10
1 row selected.

gSQL> SELECT 
      TO_DATE( '2012-05-05', 'YYYY-MM-DD' ) + INTERVAL'01-01'YEAR TO MONTH
      AS RESULT 
      FROM DUAL;
RESULT    
----------
2013-06-05
1 row selected.

gSQL> SELECT 
      INTERVAL'01-01'YEAR TO MONTH + INTERVAL'02-10'YEAR TO MONTH 
      AS RESULT 
      FROM DUAL;
RESULT    
----------
+000003-11
1 row selected.
```

<a id="571356c3cec454bb"></a>
## + (POSITIVE)

<a id="faad149f74863c4a"></a>
### Syntax

```
+ expr
```

<a id="f794954f07790ac7"></a>
### Description

The + sign is displayed in expr.

<a id="089cc07ce864ff43"></a>
### Example

```
gSQL> SELECT +3 AS RESULT1, +(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      3      -3
1 row selected.
```

<a id="71cf85ea3b234a4c"></a>
## - (NEGATIVE)

<a id="8a390b5aa93117ae"></a>
### Syntax

```
- expr
```

<a id="df5370be83d02c6c"></a>
### Description

The - sign is displayed in expr.

<a id="bfb0b1f2a01d684d"></a>
### Example

```
gSQL> SELECT -3 AS RESULT1, -(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     -3       3
1 row selected.
```

<a id="6ac7e8deca12b1e0"></a>
## - (SUBTRACTION)

<a id="74b7eb83134c885e"></a>
### Syntax

```
expr1 - expr2
```

<a id="a6565687a8566882"></a>
### Description

It returns the subtraction result of expr1 and expr2.

The subtraction types and result types are as follows.  
For more information, refer to [Type Conversion](11-sql-elements.md#e4c62967f1fb488d).

**Numeric - operation**

<a id="f1c14d9445c1d530"></a>
| expr1 | expr2 | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="5cd9853e62ad090e"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) - operation</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMBER</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference" href="#53d83238fe334f17">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="f071fd26918f7f02"></a>
### Example

```
gSQL> SELECT 
      TO_DATE( '2012-05-05' ) - TO_DATE( '2012-05-01' ) AS RESULT 
      FROM DUAL;
RESULT
------
     4
1 row selected.

gSQL> SELECT TO_DATE( '2012-05-05' ) - 3 AS RESULT FROM DUAL;
RESULT    
----------
2012-05-02
1 row selected.

gSQL> SELECT 
      TO_DATE( '2012-05-05' ) - INTERVAL'01-02'YEAR TO MONTH AS RESULT 
      FROM DUAL;
RESULT    
----------
2011-03-05
1 row selected.

gSQL> SELECT
      INTERVAL'05-01'YEAR TO MONTH - INTERVAL'02-01'YEAR TO MONTH
      AS RESULT 
      FROM DUAL;
RESULT    
----------
+000003-00
1 row selected.

gSQL> SELECT INTERVAL'15 23:59:59.999999'DAY TO SECOND 
           - INTERVAL'10 23:59:59.999999'DAY TO SECOND AS RESULT 
      FROM DUAL;
RESULT                 
-----------------------
+000005 00:00:00.000000
1 row selected.
```

<a id="a30ceb683443b26b"></a>
## / (DIVISION)

<a id="4093fb990275db77"></a>
### Syntax

```
expr1 / expr2
```

<a id="342918e91183e753"></a>
### Description

It returns the division result of expr1 and expr2.

The division types and result types are as follows.  
For more information, refer to [Type Conversion](11-sql-elements.md#e4c62967f1fb488d).

**Numeric / operation**

<a id="96b28fb79ca046f7"></a>
| expr1 | expr2 | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER | NUMBER |
| NATIVE_DOUBLE | NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="8c1f402c9a2e9996"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) / operation</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type is interval type.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type is interval type.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference text" href="#53d83238fe334f17">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="58536f6f793d3ba8"></a>
### Example

```
gSQL> SELECT INTERVAL'20-10'YEAR TO MONTH / 2 AS RESULT FROM DUAL;
RESULT    
----------
+000010-05
1 row selected.

gSQL> SELECT   INTERVAL'02 02:04:06.800000'DAY TO SECOND / 2 AS RESULT 
      FROM DUAL;
RESULT                 
-----------------------
+000001 01:02:03.400000
1 row selected.
```

<a id="635b0e1ac0a73e47"></a>
## || (CONCATENATE)

<a id="1b99d331ed0124b4"></a>
### Syntax

```
str1 || str2
```

<a id="25c394d7ac4b6d7d"></a>
### Description

CONCATENATE returns the string concatenating str1 and str2.

If either str1 or str2 is NULL, the string except NULL is returned. If both of str1 and str2 are NULL, NULL is returned.

The argument can be a type which can be converted to either character string type or binary string type.  
For more information, refer to [Type Conversion](11-sql-elements.md#e4c62967f1fb488d).

It is an alias of [CONCAT](#219fbabc9b9afa84), [CONCATENATE](#a31e786d9534cafd).

The result types are as follows.

**The result types of || (CONCATENATE)**

<a id="649b97e0998b0903"></a>
| Data type | CHAR | VARCHAR | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR | CHAR | VARCHAR | LONG VARCHAR |
| VARCHAR | VARCHAR | VARCHAR | LONG VARCHAR |
| LONG VARCHAR | LONG VARCHAR | LONG VARCHAR | LONG VARCHAR |
| Data type | BINARY | VARBINARY | LONG VARBINARY |
| BINARY | BINARY | VARBINARY | LONG VARBINARY |
| VARBINARY | VARBINARY | VARBINARY | LONG VARBINARY |
| LONG VARBINARY | LONG VARBINARY | LONG VARBINARY | LONG VARBINARY |

<a id="f7b759233afa3950"></a>
### Example

```
gSQL> SELECT 'DATA' || 'BASE' AS RESULT1,
             'DATA' || NULL   AS RESULT2,
               NULL || NULL   AS RESULT3 
       FROM DUAL;
RESULT1  RESULT2 RESULT3
-------- ------- -------
DATABASE DATA    null   
1 row selected.
```

<a id="8bc5aec5673ab396"></a>
## ABS

<a id="816d6c5fce272854"></a>
### Syntax

```
ABS( num )
```

<a id="54349c4379c6ec31"></a>
### Description

ABS returns the absolute value of num.

The num argument can be a numeric type or types which can be converted to number.  
If num is NULL, then it returns NULL.

<a id="da744502b0490107"></a>
### Example

```
gSQL> SELECT ABS(-1) AS RESULT1, ABS(1) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1       1
1 row selected.
```

<a id="27b6abcd9db2efd3"></a>
## ACOS

<a id="adbec83be956a830"></a>
### Syntax

```
ACOS( num )
```

<a id="dd96d8ba70da82ce"></a>
### Description

ACOS returns the arc cosine value of num.  

The num argument should be in the range of -1 to 1.   
If num is NULL, then it returns NULL.  

It returns the radians value in the range of 0 and pi.

<a id="ef61b625c49b388d"></a>
### Example

```
gSQL> SELECT ACOS( 1 ) FROM DUAL;
ACOS( 1 )
---------
        0
1 row selected.
```

<a id="4f0c5db194ec3444"></a>
## ADDDATE

<a id="602ca6e5c2f9e053"></a>
### Syntax

```
ADDDATE( date, INTERVAL expr unit  )
ADDDATE( expr, days )
```

<a id="6442e030dc8bf5a1"></a>
### Description

ADDDATE adds the second argument to the first argument, then returns the result.

The first argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, and the second argument data type can be INTERVAL or numeric.   
If any of the input argument value is NULL, the result is also NULL.

The result type is as same as [(DATETIME/INTERVAL) + operation](#df6803255369d10d).

<a id="1c0abd2f1e71eed1"></a>
### Example

```
gSQL> SELECT ADDDATE( TO_DATE( '2012-12-12', 'YYYY-MM-DD' ), 1 ) AS RESULT
        FROM DUAL;
RESULT    
----------
2012-12-13
1 row selected.

gSQL> SELECT ADDDATE( TO_DATE( '2012-11-11', 'YYYY-MM-DD' ),
                      INTERVAL'01-01'YEAR TO MONTH ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2013-12-11
1 row selected.
```

<a id="805ee966646d0b5a"></a>
## ADDTIME

<a id="3f7502ad251a45dd"></a>
### Syntax

```
ADDTIME( expr1, expr2 )
```

<a id="6db5ae67c4edc7e5"></a>
### Description

ADDTIME adds expr2 to expr1, then returns the result.

expr1 data type can be TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE TYPE, and expr2 data type can be INTERVAL DAY TO SECOND TYPE.  

If expr1 or expr2 is NULL, the result is NULL.

The result type is as same as [(DATETIME/INTERVAL) + operation](#df6803255369d10d).

<a id="c9d2c92a3aed87f5"></a>
### Example

```
gSQL> SELECT
      ADDTIME( TO_TIMESTAMP( '2001-05-05 06:00:00', 
                             'YYYY-MM-DD HH24:MI:SS' ),
               INTERVAL'0 00:06:06.666666'DAY TO SECOND ) AS RESULT
      FROM DUAL;
RESULT                    
--------------------------
2001-05-05 06:06:06.666666
1 row selected.
```

<a id="c9039eb53d212495"></a>
## ADD_MONTHS

<a id="0ec0b3788f0d69fc"></a>
### Syntax

```
ADD_MONTHS( date, number )
```

<a id="c2cd3f8d17d9f291"></a>
### Description

ADD_MONTHS adds as many month as the number to the date, then returns the result.  
After ADD_MONTHS operation, if the date is bigger than the last day of the month, it is adjusted to the last day of the month.

The data type of date argument can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, and the number argument can be a numeric type.  
If any of the input argument is NULL, the result is NULL.

The result type is always DATE regardless of the input argument date type.

<a id="c175cd0dcbcdc879"></a>
### Example

```
gSQL> SELECT 
      ADD_MONTHS( TO_DATE( '2001-07-31', 'YYYY-MM-DD' ), 1 ) AS RESULT1,
      ADD_MONTHS( TO_DATE( '2001-07-31', 'YYYY-MM-DD' ), 2 ) AS RESULT2
      FROM DUAL;
RESULT1    RESULT2   
---------- ----------
2001-08-31 2001-09-30
1 row selected.
```

<a id="d6f05af717c0a9b1"></a>
## ASCII

<a id="d034a831d18dd360"></a>
### Syntax

```
ASCII( char )
```

<a id="44a3c42b58f91b99"></a>
### Description

It returns the database character set code of the first character of char in decimal form.  

The data type of char can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING or can be a type which can be converted to a character type, and the return type is NUMBER.  
If char is NULL, then it returns NULL.

<a id="256a10845680165f"></a>
### Example

```
gSQL> SELECT ASCII( 'G' ) AS RESULT FROM DUAL;
RESULT
------
    71
1 row selected.
```

<a id="8b3f631de8835380"></a>
## ASIN

<a id="f1e8d13e09bfa06a"></a>
### Syntax

```
ASIN( num )
```

<a id="9104c1ac25d769f3"></a>
### Description

ASIN returns the arc sin value of num.

The num argument should be in the range of -1 to 1.  
If num is NULL, then it returns NULL.

It returns the radians value in the range of -pi/2 and pi/2.

<a id="68cecc9bc4172800"></a>
### Example

```
gSQL> SELECT ASIN( 0 ) FROM DUAL;
ASIN( 0 )
---------
        0
1 row selected.
```

<a id="085f958ca3833c42"></a>
## ATAN

<a id="6ef51733aa23e15b"></a>
### Syntax

```
ATAN( num )
```

<a id="a9ce37e302d9032d"></a>
### Description

ATAN returns the arc tangent value of num.

The num value range is not limited. It returns the radians value in the range of -pi/2 and pi/2.  
If num is NULL, then it returns NULL.

<a id="a887c57b03bc2ce3"></a>
### Example

```
gSQL> SELECT ATAN(0.5) FROM DUAL;
       ATAN(0.5)
----------------
.463647609000806
1 row selected.
```

<a id="2db4a0944f359ff3"></a>
## ATAN2

<a id="eb4348adda986bba"></a>
### Syntax

```
ATAN2( num1, num2 )
```

<a id="f67b186bcd645ed4"></a>
### Description

ATAN2 returns the arc tangent value of num1 and num2.

The num1 argument value range is not limited. It returns the radians value in the range of -pi and pi.  
Either num1 or num2 is NULL, then it returns NULL.

<a id="e99068532ed6e5a4"></a>
### Example

```
gSQL> SELECT ATAN2(1,2) FROM DUAL; 
      ATAN2(1,2)
----------------
.463647609000806
1 row selected.
```

<a id="1e10e37c7a55cff7"></a>
## AVG

<a id="d21e20acf1d01fb5"></a>
### Syntax

```
AVG( [ ALL | DISTINCT ] num )
```

<a id="18f049acd8dae73e"></a>
### Description

It is an aggregate function, and it obtains average value of exprs.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

<a id="527a4a9d1ca90adb"></a>
### Example

```
gSQL> SELECT AVG(c1) FROM t1;

AVG(C1)
-------
      2

1 row selected.
```

<a id="1666a43f7da2932b"></a>
## BITAND

<a id="634292d15ffa4f8a"></a>
### Syntax

```
BITAND( num1, num2 )
```

<a id="2c0bb9140b374a6b"></a>
### Description

It returns the AND operation result for the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT or a data type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.  
If any of the input argument is NULL, the result is also NULL.

The result type is NATIVE_BIGINT.

<a id="9f873ee5e0158057"></a>
### Example

```
gSQL> SELECT BITAND( 5, 3 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="c0703bb1447a3813"></a>
## BITNOT

<a id="cb1321048664c5a1"></a>
### Syntax

```
BITNOT( num )
```

<a id="c24cdefbde3bf25a"></a>
### Description

It returns the NOT operation result for the num bit.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT or a data type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.  
If the input argument is NULL, the result is also NULL.

The result type is as follows.  
• If the input argument is NATIVE_SMALLINT type, its result type is NATIVE_SMALLINT type.  
• If the input argument is NATIVE_INTEGER type, its result type is NATIVE_INTEGER type.  
• If the input argument is NATIVE_BIGINT type, its result type is NATIVE_BIGINT type.

<a id="07c0a0dcfc9e8066"></a>
### Example

```
gSQL> SELECT BITNOT( 5 ) AS RESULT FROM DUAL;
RESULT
------
    -6
1 row selected.
```

<a id="450f5099391d5a08"></a>
## BITOR

<a id="ec6ded3de9badaa3"></a>
### Syntax

```
BITOR( num1, num2 )
```

<a id="eb73377630f55d36"></a>
### Description

It returns the OR operation result for the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT types or a data type which can be converted to NATIVE_BIGINT type.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.  
If any of the input argument value is NULL, the result is NULL.

The result type is NATIVE_BIGINT type.

<a id="c0175331edb63bcf"></a>
### Example

```
gSQL> SELECT BITOR( 5, 3 ) FROM DUAL;

BITOR( 5, 3 )
-------------
            7
1 row selected.
```

<a id="8d27aee5384b4efb"></a>
## BITXOR

<a id="c14cad8484dfdc46"></a>
### Syntax

```
BITXOR( num1, num2 )
```

<a id="33440be8e63678b9"></a>
### Description

It returns the XOR operation result for the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT or a data type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.  
If any of the input argument value is NULL, the result is NULL.

The result type is NATIVE_BIGINT.

<a id="e44c2954b2ee025b"></a>
### Example

```
gSQL> SELECT BITXOR( 5, 3 ) FROM DUAL;
BITXOR( 5, 3 )
--------------
             6
1 row selected.
```

<a id="6f2c13856ca1b319"></a>
## BIT_LENGTH

<a id="6a2715a7d9fd38fd"></a>
### Syntax

```
BIT_LENGTH( str )
```

<a id="1fad7cd35b7d7ce0"></a>
### Description

BIT_LENGTH returns the number of bits for str.  
If str is NULL, then it returns NULL.

<a id="43ee303edfc8e87a"></a>
### Example

```
gSQL> SELECT BIT_LENGTH( 'LIKE' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
             32
    1 row selected.
```

<a id="6252970883521ebc"></a>
## BYTE_LENGTH

<a id="e33ad902618b7c8e"></a>
### Syntax

```
BYTE_LENGTH( str )
```

<a id="3742631de3fb8c99"></a>
### Description

It is an alias of OCTET_LENGTH.  
For more information, refer to [OCTET_LENGTH](#f5e2f14f42d4ae0f), [LENGTHB](#16160b297e8ce147).

<a id="c3c72bee30266197"></a>
### Example

- Multi byte character set (e.g. UTF8): 1 byte character

```
gSQL> SELECT BYTE_LENGTH( 'OCTET_LENGTH' ) AS RESULT_1BYTE_CHARACTERS 
        FROM DUAL;
RESULT_1BYTE_CHARACTERS
-----------------------
                     12
1 row selected.
```

- Multi byte character set (e.g. UTF8): 2 byte character

```
gSQL> SELECT BYTE_LENGTH( 'αβ' ) AS RESULT_2BYTE_CHARACTERS FROM DUAL;
RESULT_2BYTE_CHARACTERS
-----------------------
                      4
1 row selected.
```

<a id="9a8d088a9c4f3917"></a>
## CASE2

<a id="f3b9e1b5d298ef68"></a>
### Syntax

```
CASE2( condition1, result1
      [, condition2, result2
       , ...
       , conditionN, resultN ]
      [, default ] )
```

<a id="4a5ebea4ec713fb9"></a>
### Description

CASE2 evaluates the condition in the described order.  
If the comparison result is FALSE, it continues evaluating until TRUE comes up.  
If the comparison result is TRUE, it returns the corresponding result, and does not evaluate any more.  
If all the comparison results are FALSE, it returns the default value. If the default is omitted, it returns NULL.

If multiple types are used in result, then the result type is determined according to [Result Type Combination Rule](11-sql-elements.md#8ed35905e84aa434).

CASE2 can be expressed by using CASE as follows.

- CASE2( condition1, res1, condition2, res2 )

```
CASE WHEN condition1 THEN res1
     WHEN condition2 THEN res2
     ELSE NULL
  END
```

- CASE2( condition1, res1, condition2, res2, default )

```
CASE WHEN condition1 THEN res1
     WHEN condition2 THEN res2
     ELSE default
  END
```

<a id="0aa3e82e28477f8b"></a>
### Example

```
gSQL> SELECT I1,
        CASE2( I1 = 1, 'ONE', I1 = 2, 'TWO' ) AS CASE2_RESULT1,
        CASE2( I1 = 1, 'ONE', I1 = 2, 'TWO', 'NUMBER' ) AS CASE2_RESULT2
      FROM T1;
I1 CASE2_RESULT1 CASE2_RESULT2
-- ------------- -------------
 1 ONE           ONE          
 2 TWO           TWO          
 3 null          NUMBER       
3 rows selected.
```

<a id="039a0b5783647815"></a>
## CBRT

<a id="7227e43920fec08f"></a>
### Syntax

```
CBRT( num )
```

<a id="e47faa93769853b5"></a>
### Description

It returns the cube root of num.  
If num is NULL, the result is also NULL.

<a id="b8713d016cb0ec9a"></a>
### Example

```
gSQL> SELECT CBRT( 27 ) FROM DUAL;
CBRT( 27 )
----------
         3
1 row selected.
```

<a id="251f62fb7bde6912"></a>
## CEIL

<a id="b29810cda196d9e6"></a>
### Syntax

```
CEIL( num )
CEILING( num )
```

<a id="f0897a0a53aa83b2"></a>
### Description

CEIL returns the smallest integer which is equal to or bigger than num.  
If num is NULL, then it returns NULL.

<a id="769de05854774c2f"></a>
### Example

```
gSQL> SELECT CEIL( 3.5 ) AS RESULT1, CEIL( -3.5 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      4      -3
1 row selected.
```

<a id="90284f3cb97390d5"></a>
## CHAR_LENGTH

<a id="2ad74304a4d00179"></a>
### Syntax

```
CHAR_LENGTH( str )            
CHARACTER_LENGTH( str )
```

<a id="274e77b517c7ca5f"></a>
### Description

CHAR_LENGTH returns the number of character for str according to the character set.

The str can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or it can be a data type which can be converted to character type. The return type is NATIVE_BIGINT.

If the data type of str is CHARACTER, the trailing blanks are included in the calculation.  
If str is NULL, it returns NULL.

It is an alias of [LENGTH](#870862810f0a2cfd).

<a id="99cdde3bbf6c8798"></a>
### Example

Multi byte character set: (e.g. UTF8)

```
gSQL> SELECT CHAR_LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="9cd93bd8a7fd0233"></a>
## CHR

<a id="307cbac03cc90006"></a>
### Syntax

```
CHR( num )
```

<a id="48a5948a36e1a6c7"></a>
### Description

It returns a character in the database character set code corresponding to num.

num is a numeric type.  
If num is NULL, then it returns NULL.  

The return type is VARCHAR.

<a id="6dc17e8480744116"></a>
### Example

```
gSQL> SELECT CHR(71) FROM DUAL;
CHR(71)
-------
G      
1 row selected.
```

<a id="e0b0e52ec74f4386"></a>
## CLOCK_DATE

<a id="19160c75b759071d"></a>
### Syntax

```
CLOCK_DATE()
```

<a id="add6253fb985aa70"></a>
### Description

Whenever the CLOCK_DATE function is called, the current date (DATE type) value is obtained.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="6a0acdad73f5e0c0"></a>
### Example

Each row can have a different date value.

```
gSQL> SELECT CLOCK_DATE() FROM t1;

CLOCK_DATE()
------------
2013-12-12  
2013-12-12  
2013-12-13  

3 rows selected.
```

<a id="dd3d018a08c898bf"></a>
## CLOCK_LOCALTIME

<a id="61875e84d1cbe209"></a>
### Syntax

```
CLOCK_LOCALTIME()
```

<a id="586c3483fd1d68d4"></a>
### Description

Whenever the CLOCK_LOCALTIME function is called, the current time value without TIME ZONE (TIME WITHOUT TIME ZONE type) is obtained.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.  
• STATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="2ca27907fd521e6a"></a>
### Example

Each row can have a different time value.

```
gSQL> SELECT CLOCK_LOCALTIME() FROM t1;

CLOCK_LOCALTIME()
-----------------
14:42:05.470757  
14:42:05.470759  
14:42:05.470759  

3 rows selected.
```

<a id="7123ff0d6f58c3f9"></a>
## CLOCK_LOCALTIMESTAMP

<a id="ce8fed5f29709d7c"></a>
### Syntax

```
CLOCK_LOCALTIMESTAMP()
```

<a id="d94c3fd74bd6f50b"></a>
### Description

Whenever the CLOCK_LOCALTIMESTAMP() function is called, the current TIMESTAMP value without TIME ZONE (TIMESTAMP WITHOUT TIME ZONE type) is obtained.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• STATEMENT_LOCALTIMESTAMP(): All TIMESTAMP values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="34e944b331eb403b"></a>
### Example

Each row can have a different timestamp value.

```
gSQL> SELECT CLOCK_LOCALTIMESTAMP() FROM t1;

CLOCK_LOCALTIMESTAMP()    
--------------------------
2013-12-12 14:46:17.309206
2013-12-12 14:46:17.309209
2013-12-12 14:46:17.309209
```

<a id="4484fc251452b798"></a>
## CLOCK_TIME

<a id="2e4516c28d7b96b0"></a>
### Syntax

```
CLOCK_TIME()
```

<a id="d9be50ec6e04362b"></a>
### Description

Whenever the CLOCK_TIME() function is called, the current time value with TIME ZONE (TIME WITH TIME ZONE type) is obtained.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• STATEMENT_TIME(): All time values in an SQL statement are same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="475d8a7cb2a6cf87"></a>
### Example

Each row can have a different time value.

```
gSQL> SELECT CLOCK_TIME() FROM t1;

CLOCK_TIME()          
----------------------
14:48:21.052324 +09:00
14:48:21.052326 +09:00
14:48:21.052327 +09:00

3 rows selected.
```

<a id="18efc62895fc9f19"></a>
## CLOCK_TIMESTAMP

<a id="04215037e47c5dc9"></a>
### Syntax

```
CLOCK_TIMESTAMP()
```

<a id="ed632f5ff877f501"></a>
### Description

Whenever CLOCK_TIMESTAMP() function is called, the current TIMESTAMP value with TIME ZONE (TIMESTAMP WITH TIME ZONE type) is obtained.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_TIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• STATEMENT_TIMESTAMP(): All TIMESTAMP values in an SQL statement are same.   
• CLOCK_TIMESTAMP(): Whenever the function is called, the current TIMESTAMP value is obtained.

<a id="6da04c84c7795738"></a>
### Example

Each row can have a different timestamp value.

```
gSQL> SELECT CLOCK_TIMESTAMP() FROM t1;

CLOCK_TIMESTAMP()                
---------------------------------
2013-12-12 14:49:45.051709 +09:00
2013-12-12 14:49:45.051714 +09:00
2013-12-12 14:49:45.051714 +09:00

3 rows selected.
```

<a id="7449b46fd3a3a94b"></a>
## COALESCE

<a id="809f9897fceac75b"></a>
### Syntax

```
COALESCE( expr1, ..., exprN )
```

<a id="651369820c8d9023"></a>
### Description

It returns the first non null expr in the expr list.  
If all expr in the expr list are null, it returns null.  
In the expr list, there should be two or more expr.

If multiple types are in the expr list, the result type is determined by the [Result Type Combination Rule](11-sql-elements.md#8ed35905e84aa434).

- COALESCE can be expressed by using CASE as follows.

    - COALESCE( expr1, expr2 )

```
CASE WHEN expr1 IS NOT NULL THEN expr1
       ELSE expr2
  END
```

    - COALESCE( expr1, expr2, ..., exprN )

```
CASE WHEN expr1 IS NOT NULL THEN expr1
       ELSE COALESCE( expr2, ..., exprN )
  END
```

<a id="e6c01a775817a9e5"></a>
### Example

```
gSQL> SELECT COALESCE( NULL, 1, 2 ) FROM DUAL;
COALESCE( NULL, 1, 2 )
----------------------
                     1
1 row selected.

gSQL> SELECT COALESCE( NULL, NULL, NULL ) FROM DUAL;
COALESCE( NULL, NULL, NULL )
----------------------------
null                        
1 row selected.
```

<a id="219fbabc9b9afa84"></a>
## CONCAT

<a id="7e4a32b3295f239e"></a>
### Syntax

```
CONCAT( str1, str2, ... )
```

<a id="8e583e9d2e2635e6"></a>
### Description

It is an alias of || ( CONCATENATE ).  
It is an argument of CONCAT function and 2 ~ 254 number of CONCATs can be set.  
For more information, refer to [|| (CONCATENATE)](#635b0e1ac0a73e47), [CONCATENATE](#a31e786d9534cafd).

<a id="77daba3f8fb4a348"></a>
### Example

```
gSQL> SELECT CONCAT( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="a31e786d9534cafd"></a>
## CONCATENATE

<a id="9b59f3b83667b07f"></a>
### Syntax

```
CONCATENATE( str1, str2, ... )
```

<a id="f141d62f355413bf"></a>
### Description

It is an alias of || ( CONCATENATE ).  
It is an argument of CONCATENATE  function and 2 ~ 254 number of CONCATENATEs can be set.  
For more information, refer to [CONCAT](#219fbabc9b9afa84), [|| (CONCATENATE)](#635b0e1ac0a73e47).

<a id="033818f61bf2d42d"></a>
### Example

```
gSQL> SELECT CONCATENATE( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="bb8672c7433ff513"></a>
## COS

<a id="6ff54bf01fc83e2a"></a>
### Syntax

```
COS(num)
```

<a id="e7572601436405f4"></a>
### Description

It returns the COSINE value of num.  
If the num argument is NULL, the result is also NULL.

<a id="768f50cafed9b0ab"></a>
### Example

```
gSQL> SELECT COS( 0 ) FROM DUAL;
COS( 0 )
--------
       1
1 row selected.
```

<a id="99e393462379545e"></a>
## COT

<a id="b613ce3c5ef9fb8b"></a>
### Syntax

```
COT(num)
```

<a id="1e0c5b0fc573bb20"></a>
### Description

It returns the COTANGENT value of num.  
If the num argument is NULL, the result is also NULL.

<a id="77adc916d81ad8db"></a>
### Example

```
gSQL> SELECT COT( 1 ) FROM DUAL;
        COT( 1 )
----------------
.642092615934331
1 row selected.
```

<a id="841587eef1a7f1b6"></a>
## COUNT

<a id="b989caf76a48774c"></a>
### Syntax

```
COUNT( [ ALL | DISTINCT ] expr )
```

<a id="351783bd856723d7"></a>
### Description

It is an aggregate function. It returns the number of rows whose expr is not NULL.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

<a id="dc611a4074c4f304"></a>
### Example

```
gSQL> SELECT COUNT(c1) FROM t1;

COUNT(C1)
---------
        3

1 row selected.
```

<a id="2f8118f137a2eee0"></a>
## COUNT(*)

<a id="6a4fdc4cfc8cdd8b"></a>
### Syntax

```
COUNT(*)
```

<a id="e91671cd37d71063"></a>
### Description

It is an aggregate function, and the number of rows is obtained.  
It has nothing to do with whether it is NULL or not because an expression is not explicitly specified.

<a id="c407f865d4b753a2"></a>
### Example

```
gSQL> SELECT COUNT(*) FROM t1;

COUNT(*)
--------
       4

1 row selected.
```

<a id="e25b96fcf68ed40a"></a>
## CURRENT_CATALOG

<a id="de59d88c84cc3b5c"></a>
### Syntax

```
CURRENT_CATALOG [()]
```

<a id="517bb86e81b5dd92"></a>
### Description

The catalog name (database name) is obtained.

<a id="832d7c58f2fa0632"></a>
### Example

```
gSQL> SELECT CURRENT_CATALOG FROM dual;

CURRENT_CATALOG
---------------
TEST_DB        

1 row selected.
```

<a id="a15210f4e5a15069"></a>
## CURRENT_DATE

<a id="95296de424c06963"></a>
### Syntax

```
CURRENT_DATE [()]
STATEMENT_DATE()
```

<a id="175ff438638d31d0"></a>
### Description

The current date (DATE type) is obtained.

CURRENT_DATE is an SQL standard function.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• CURRENT_DATE, STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="e9dab6c8d65d4cc6"></a>
### Example

```
gSQL> SELECT CURRENT_DATE FROM t1;

CURRENT_DATE
------------
2013-12-12  
2013-12-12  
2013-12-12  

3 rows selected.
```

<a id="a84d1e2b247e4149"></a>
## CURRENT_SCHEMA

<a id="1e8e835eea4188a8"></a>
### Syntax

```
CURRENT_SCHEMA [()]
```

<a id="32ce7452e906c0c3"></a>
### Description

User's current SCHEMA is obtained.

<a id="e0d25e982078a5ba"></a>
### Example

```
gSQL> SELECT CURRENT_SCHEMA FROM dual;

CURRENT_SCHEMA
--------------
PUBLIC        

1 row selected.
```

<a id="41060514eb7badef"></a>
## CURRENT_TIME

<a id="f5262bc044821083"></a>
### Syntax

```
CURRENT_TIME [()]
STATEMENT_TIME()
```

<a id="7bd04eeaf6ed2030"></a>
### Description

The current TIME WITH TIME ZONE type value based on the session time is obtained.

CURRENT_TIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• CURRENT_TIME, STATEMENT_TIME(): All time values in an SQL statement are same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="721ee180c7849d55"></a>
### Example

All rows have the same value.

```
gSQL> SELECT CURRENT_TIME FROM t1;

CURRENT_TIME          
----------------------
16:27:10.116396 +09:00
16:27:10.116396 +09:00
16:27:10.116396 +09:00

3 rows selected.
```

<a id="07bcd31b7971348e"></a>
## CURRENT_TIMESTAMP

<a id="0c796f7e98825be9"></a>
### Syntax

```
CURRENT_TIMESTAMP [()]
STATEMENT_TIMESTAMP()
```

<a id="62187403a0faee9f"></a>
### Description

It obtains the TIMESTAMP WITH TIME ZONE type value based on the session time.

CURRENT_TIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_TIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• CURRENT_TIMESTAMP, STATEMENT_TIMESTAM(): All TIMESTAMP values in an SQL statement are same.  
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="527eb5790ecf920f"></a>
### Example

All rows have the same value.

```
gSQL> SELECT CURRENT_TIMESTAMP FROM t1;

CURRENT_TIMESTAMP                
---------------------------------
2013-12-12 16:34:55.649632 +09:00
2013-12-12 16:34:55.649632 +09:00
2013-12-12 16:34:55.649632 +09:00

3 rows selected.
```

<a id="26fdffa4d0851f4c"></a>
## CURRENT_USER

<a id="08e25f6955ee3dfa"></a>
### Syntax

```
CURRENT_USER [()]
```

<a id="997bbf328418de72"></a>
### Description

It returns the current user.

The user information is managed in three types as follows.

- Logon user: It is a user who performed login, and it is maintained until the connection is closed.
- Session user: It is as same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: It is generally as same as the session user, but it is temporarily changed internally in system to control access when using the PSM, view.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="35274e79b7a80cac"></a>
### Example

```
% gsql sys gliese

gSQL> SET SESSION AUTHORIZATION test;

Session set.

gSQL> SELECT 
        LOGON_USER() AS result1, 
        SESSION_USER() AS result2, 
        CURRENT_USER() AS result3 
      FROM DUAL;

RESULT1 RESULT2 RESULT3
------- ------- -------
SYS     TEST    TEST

1 row selected.
```

<a id="5f59a81ef62c1fba"></a>
## CURRVAL

<a id="1d094bc4f764508f"></a>
### Syntax

```
seq_name.CURRVAL
CURRVAL(seq_name)
```

<a id="1d83bba78070a894"></a>
### Description

The current value of the sequence object is obtained.

A sequence value should be set with NEXTVAL(seq_name) at least once.

<a id="46f027b023854e43"></a>
### Example

```
gSQL> SELECT seq.CURRVAL FROM dual;

SEQ.CURRVAL
-----------
          1

1 row selected.
```

<a id="e28ce518b9ddf54d"></a>
## DATEADD

<a id="c4a9897ef69d6401"></a>
### Syntax

```
DATEADD( datepart, number, date )
```

<a id="02189163f70ec4e4"></a>
### Description

It adds number to the specified datepart of date, and returns the result.

If the number is decimal point, it is not rounded off.  
The date data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE.  
If number or date is NULL, the result is also NULL.

The result type which is as same as the input date argument type is returned.

**Available string format in datepart**

<a id="e967b34b1f63ea78"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">Description</th></tr><tr><td>YEAR</td><td>Year</td></tr><tr><td>QUARTER</td><td>Quarter</td></tr><tr><td>MONTH</td><td>Month</td></tr><tr><td>DAYOFYEAR</td><td>Day of year</td></tr><tr><td>DAY</td><td>Day</td></tr><tr><td>WEEK</td><td>Week</td></tr><tr><td>WEEKDAY</td><td>Weekday</td></tr><tr><td>HOUR</td><td>Hour</td></tr><tr><td>MINUTE</td><td>Minute</td></tr><tr><td>SECOND</td><td>Second</td></tr><tr><td>MILLISECOND</td><td>Millisecond</td></tr><tr><td>MICROSECOND</td><td>Microsecond</td></tr></tbody></table>

<a id="4f1f22862f43ea04"></a>
### Example

```
gSQL> SELECT 
      DATEADD( YEAR, 1, TO_DATE( '2013-05-14', 'YYYY-MM-DD' ) ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2014-05-14
1 row selected.

gSQL> SELECT 
      DATEADD( MONTH, 13, TO_DATE('2013-05-14', 'YYYY-MM-DD') ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2014-06-14
1 row selected.

gSQL> SELECT 
      DATEADD( DAY, 397, TO_DATE('2013-05-14', 'YYYY-MM-DD') ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2014-06-15
1 row selected.
```

<a id="b8b818dc911fb82b"></a>
## DATEDIFF

<a id="6f4f1ad93f0b86a7"></a>
### Syntax

```
DATEDIFF( datepart, startdate, enddate )
```

<a id="4064b731283e7f87"></a>
### Description

It substracts startdate from enddate, then returns the result to the specified datepart.

If the startdate or enddate is NULL, the result is also NULL.  
The data type of startdate and enddate can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME.

The result type is NUMBER.

**Available string format in datepart**

<a id="2014c6f8cfce8f4f"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">Description</th></tr><tr><td>YEAR</td><td>Year</td></tr><tr><td>QUARTER</td><td>Quarter</td></tr><tr><td>MONTH</td><td>Month</td></tr><tr><td>DAYOFYEAR</td><td>Day of year</td></tr><tr><td>DAY</td><td>Day</td></tr><tr><td>HOUR</td><td>Hour</td></tr><tr><td>MINUTE</td><td>Minute</td></tr><tr><td>SECOND</td><td>Second</td></tr><tr><td>MILLISECOND</td><td>Millisecond</td></tr><tr><td>MICROSECOND</td><td>Microsecond</td></tr></tbody></table>

<a id="18b110b0fa793a74"></a>
### Example

```
gSQL>  SELECT 
       DATEDIFF( YEAR, 
                 TO_DATE( '2013-05-14', 'YYYY-MM-DD' ), 
                 TO_DATE( '2014-06-15', 'YYYY-MM-DD' ) ) AS RESULT 
       FROM DUAL;
RESULT
------
     1
1 row selected.

gSQL> SELECT 
      DATEDIFF( MONTH, 
                TO_DATE( '2013-05-14', 'YYYY-MM-DD' ), 
                TO_DATE( '2014-06-15', 'YYYY-MM-DD' ) ) AS RESULT 
      FROM DUAL;
RESULT
------
    13
1 row selected.

gSQL> SELECT 
      DATEDIFF( DAY, 
                TO_DATE( '2013-05-14', 'YYYY-MM-DD' ), 
                TO_DATE( '2014-06-15', 'YYYY-MM-DD' ) ) AS RESULT 
      FROM DUAL;
RESULT
------
   397
1 row selected.
```

<a id="c9c36d4517e9474a"></a>
## DATE_ADD

<a id="f07a503ed9fdb673"></a>
### Syntax

```
DATE_ADD( date, INTERVAL expr unit  )
```

<a id="27bd323339f642e4"></a>
### Description

It is the same function as [ADDDATE](#4f0c5db194ec3444) (date, INTERVAL expr unit).

<a id="d6d20d880c913b88"></a>
### Example

```
gSQL> SELECT 
      DATE_ADD( TO_DATE( '2012-01-02', 'YYYY-MM-DD' ),
                INTERVAL '2-2' YEAR TO MONTH ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2014-03-02
1 row selected.
```

<a id="2470d2bc00c929d5"></a>
## DATE_PART

<a id="681c75ff4b48194c"></a>
### Syntax

```
DATE_PART( field, datetime )
```

<a id="640670f3b745c309"></a>
### Description

The result of DATE_PART is as same as the result of the EXTRACT function. It searches for the specified field from the input datetime type, and returns it.

The field argument should be text literal, and YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, TIMEZONE_HOUR, TIMEZONE_MINUTE can be specified to text literal.  
The datetime argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL.

If field is not in the range of datetime, an error is returned.   
For DATE type, field should be YEAR, MONTH, DAY, otherwise an error is returned.  
If datatime is NULL, then it returns NULL.

The return type is NUMBER.

For more information, refer to [EXTRACT](#e603ae2692dec703).

<a id="efdb0b69a1723166"></a>
### Example

```
gSQL> SELECT 
      DATE_PART( 'DAY', TO_DATE( '2012-01-02', 'YYYY-MM-DD' ) ) AS RESULT
      FROM DUAL;
RESULT
------
     2
1 row selected.

gSQL> SELECT 
      DATE_PART( 'YEAR', INTERVAL'9-11'YEAR TO MONTH ) AS RESULT 
      FROM DUAL;
RESULT
------
     9
1 row selected.
```

<a id="86d0467900783995"></a>
## DECODE

<a id="b30fb62dae059234"></a>
### Syntax

```
DECODE( expr, comparison_expr1, result1
           [, comparison_expr2, result2
            , ...
            , comparison_exprN, resultN ]
           [, default ] )
```

<a id="b0105c46db63900c"></a>
### Description

It evaluates expr and comparison_expr in the described order in DECODE statement using equal operation.  
If the comparison result is FALSE, it continues evaluating until TRUE comes up.  
If the comparison result is TRUE, it returns the corresponding result, and does not evaluate any more.

If expr and comparison_expr are equal, or if both expr and comparison_expr are NULL( null = null ), it is evaluated as TRUE, and returns the corresponding result.  
If all of the evaluated results are FALSE, it returns default. If the default is omitted, it returns NULL.

- Comparing expr and comparison_expr  
  All expr, comparison_expr1, ..., comparison_exprN are converted to the data type of comparison_expr1 (the first comparison_expr), then they are compared.  
  If comparison_expr1 (the first comparison_expr) is a character type and a numeric type then it becomes the type including the range of types described in each *expr, comparison_expr1, ..., comparison_exprN*.  
  If all types described in *expr, comparison_expr1, ..., comparison_exprN* are CHAR, then VARCHAR type comparison is performed.

- Result type  
  The result type becomes the data type of result1 (the first result).  
  If the data type of result1 (the first result) is a character type and a numeric type then it becomes the type including the range of types described in result1, ..., resultN each.  
  If result1 (the first result) is CHAR or NULL, then the result type is VARCHAR.

DECODE can be expressed by using CASE as follows.

- DECODE( expr, comp_expr1, res1, comp_expr2, res2 )

```
CASE WHEN (expr = comp_expr1) OR (expr IS NULL AND comp_expr1 IS NULL ) THEN res1
     WHEN (expr = comp_expr2) OR (expr IS NULL AND comp_expr2 IS NULL ) THEN res2
     ELSE NULL
  END
```

- DECODE( expr, comp_expr1, res1, comp_expr2, res2, default )

```
CASE WHEN (expr = comp_expr1) OR (expr IS NULL AND comp_expr1 IS NULL ) THEN res1
     WHEN (expr = comp_expr2) OR (expr IS NULL AND comp_expr2 IS NULL ) THEN res2
     ELSE default
  END
```

<a id="bb949426d984a04e"></a>
### Example

```
gSQL> SELECT I1,
             DECODE( I1, 1, 'ONE', 
                         2, 'TWO', 
                         NULL, 'NULL VALUE', 
                         'DEFAULT VALUE' ) AS DECODE_RESULT
      FROM T1;
  I1 DECODE_RESULT
---- -------------
   1 ONE          
   2 TWO          
null NULL VALUE   
   3 DEFAULT VALUE
4 rows selected.
```

<a id="5008d54e049cabbb"></a>
## DEGREES

<a id="f7ce8cd92ff559be"></a>
### Syntax

```
DEGREES( radians )
```

<a id="bd2ff7d1b1159190"></a>
### Description

It converts a degree radians to a value in degrees, and returns the converted value.  
If radians is NULL, then it returns NULL.

<a id="4c7a70b6af0d8293"></a>
### Example

```
gSQL> SELECT DEGREES( PI() ) AS RESULT FROM DUAL;
RESULT
------
   180
1 row selected.
```

<a id="f7e72361252d4d3c"></a>
## DIGEST

<a id="4042a06342a04c6a"></a>
### Syntax

```
DIGEST( data, type )
```

<a id="f814c26e36a6b201"></a>
### Description

It hashes the data to the given type, and returns the result in VARBINARY type.

An implicit conversion may occur when inputting data type based on the following rules.  

• Input the BINARY, VARBINARY type data in VARBINARY type.  
• Input LONG VARBINARY type data in LONG VARBINARY type.  
• Input LONG VARCHAR type data in LONG VARCHAR type.  
• Input all other type of data after implicitly converting it to VARCHAR type.

DIGEST function supports the following hash types.  

• The result of 'SHA1' is 20 byte varbinary.  
• The result of 'SHA224' is 28 byte varbinary.  
• The result of 'SHA256' is 32 byte varbinary.  
• The result of 'SHA384' is 48 byte varbinary.  
• The result of 'SHA512' is 64 byte varbinary.

Use HEX function to view the result in hexadecimal character because the result is returned in VARBINARY type. In this case, the length becomes double of the original.

<a id="99f8a747a1e94f06"></a>
### Example

```
gSQL> SELECT HEX( DIGEST( 'my password', 'SHA256' ) ) AS RESULT FROM DUAL;

RESULT                                                          
----------------------------------------------------------------
BB14292D91C6D0920A5536BB41F3A50F66351B7B9D94C804DFCE8A96CA1051F2

1 row selected.
```

<a id="7caeeb54faeeed9f"></a>
## DUMP

<a id="8082579691a911b7"></a>
### Syntax

```
DUMP( expr )
```

<a id="c497b22188e0db97"></a>
### Description

It returns internal representation information of expr.  
Internal representation information is displayed as the data type, byte length and data information.

expr can be any data types.  
If expr is NULL, then it returns NULL.  

The return type is CHARACTER VARYING.

<a id="adb7039059251a31"></a>
### Example

```
gSQL> SELECT DUMP( 'DUMP' ) AS RESULT FROM DUAL;
RESULT                           
---------------------------------
Type=CHAR Len=4 : Str=68,85,77,80
1 row selected.
```

<a id="ccfd62714a239834"></a>
## EXP

<a id="5312fb4d55e5c4b8"></a>
### Syntax

```
EXP( num )
```

<a id="de02b033e3b3a0df"></a>
### Description

It returns squared value of e (base of natural logarithm)'s num.  
If num is NULL, then it returns NULL.

<a id="682faae96c96c653"></a>
### Example

```
gSQL> SELECT EXP( 1 ) AS RESULT FROM DUAL;
          RESULT
----------------
2.71828182845905
1 row selected.
```

<a id="e603ae2692dec703"></a>
## EXTRACT

<a id="c4d012f24f784194"></a>
### Syntax

```
EXTRACT( <field> FROM datetime )

<field> ::= 
        YEAR
      | MONTH
      | DAY
      | HOUR
      | MINUTE
      | SECOND
      | TIMEZONE_HOUR
      | TIMEZONE_MINUTE
```

<a id="0bf187351ab55289"></a>
### Description

It searches for the specified field from an input datetime type, and returns it.

The datetime argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL.

If field is not in the range of datetime, an error is returned.   
For DATE type, the field should be YEAR, MONTH, DAY, otherwise an error is returned.  
The return type is NUMBER.

Result of EXTRACT is as same as the result of the [DATE_PART](#2470d2bc00c929d5) function.

<a id="8d75e5ee64dfb86d"></a>
### Example

```
gSQL> SELECT 
      EXTRACT( SECOND FROM TO_TIMESTAMP( '2012-12-13 01:23:44.5', 
                                         'YYYY-MM-DD HH24:MI:SS.FF1' )  ) 
              AS RESULT 
      FROM DUAL;
RESULT
------
  44.5
1 row selected.

gSQL> SELECT
      EXTRACT( YEAR FROM CAST('2-3' AS INTERVAL YEAR TO MONTH) ) AS RESULT
      FROM DUAL;
RESULT
------
     2
1 row selected.
```

<a id="4848a49e829fbc4e"></a>
## FACTORIAL

<a id="fbbdc13854387e6a"></a>
### Syntax

```
FACTORIAL( num )
```

<a id="14553deb2a2d6177"></a>
### Description

It multiplies the successive natural numbers from 1 to num in order, and returns the result.  
If num is NULL, then it returns NULL.

<a id="df5591060dccb7ac"></a>
### Example

```
gSQL> SELECT FACTORIAL( 5 ) AS RESULT FROM DUAL;
RESULT
------
   120
1 row selected.
```

<a id="d0f5bb7c6dea6d8b"></a>
## FLOOR

<a id="1284dd2f6f6c2979"></a>
### Syntax

```
FLOOR( num )
```

<a id="ae08fc5a523456f1"></a>
### Description

It returns the biggest integer which is equal to or smaller than num.  
If num is NULL, then it returns NULL.

<a id="cff2860335b42c7f"></a>
### Example

```
gSQL> SELECT FLOOR(42.8) AS RESULT1, FLOOR(-42.8) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     42     -43
1 row selected.
```

<a id="13811824d98292f5"></a>
## FROM_BASE64

<a id="d6cc7026563d67ff"></a>
### Syntax

```
FROM_BASE64( str )
```

<a id="da746018d4dbfb88"></a>
### Description

The converted character by base 64 encoding is input to FROM_BASE64, then the decoded binary string is returned.

The input argument data type can be a character type such as CHARACTER VARYING, CHARACTER LONG VARYING, and the result type is a binary character such as BINARY VARYING or BINARY LONG VARYING.

If str is NULL, then the result value is also NULL.  
If str includes characters which are not in the range of base64 character, then it returns an error.  
A newline, carriage return, tab, and space of str is ignored when decoding.

For more information, refer to [TO_BASE64](#8f90bf4109b26d9a).

<a id="337abeb2d9f0af38"></a>
### Example

```
gSQL> SELECT FROM_BASE64( TO_BASE64( 'abc' ) ),
             FROM_BASE64( TO_BASE64( 'abcd' ) ) 
        FROM DUAL;
FROM_BASE64( TO_BASE64( 'abc' ) ) FROM_BASE64( TO_BASE64( 'abcd' ) )
--------------------------------- ----------------------------------
616263                            61626364                          
1 row selected.
```

<a id="788c0f5902605f6a"></a>
## GREATEST

<a id="e5dca28be8a8ae03"></a>
### Syntax

```
GREATEST( expr1 [, expr2, ... exprn ] )
```

<a id="1481c1e76727eab2"></a>
### Description

It returns the largest value among the received expr argument.

If any expr argument is NULL, the result value is NULL.

The result type becomes the data type of expr1  (the first expr).   
If the data type of expr1 (the first expr) is a character type and a numeric type then it becomes the type including the range of expr1, ..., exprN each.  
If all of expr1, ..., exprN is described in CHAR type, then all exprs are compared in VARCHAR type and the result type is VARCHAR.

<a id="71ac8ae33f39315b"></a>
### Example

```
gSQL> SELECT GREATEST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
   200
1 row selected.
```

<a id="7db25d1e4b8e4867"></a>
## HEX

<a id="a151c6ac0c24a9fb"></a>
### Syntax

```
HEX( str )
```

<a id="19a73e6690ce8690"></a>
### Description

It returns a str argument in hexadecimal character.  
A str argument data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, a type which can be converted to a character type, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.  
The result type is a character type such as CHARACTER VARYING or CHARACTER LONG VARYING.

If str is NULL, then the result value is also NULL.

If an argument of HEX function is a numeric type, then it returns an error.   
To convert a decimal number to a hexadecimal number, use TO_CHAR() function by using  'X' number format.  
e.g. TO_CHAR( 255, 'XX' )

For more information, refer to [UNHEX](#dd027ce981dca375).

<a id="d327b4963aac96bc"></a>
### Example

```
gSQL> SELECT HEX( 'abc' ) FROM DUAL;
HEX( 'abc' )
------------
616263      
1 row selected.
```

<a id="5727424753db77ef"></a>
## INITCAP

<a id="0ff9f4d273028113"></a>
### Syntax

```
INITCAP( str )
```

<a id="2ec23cb6615f54c9"></a>
### Description

It converts the first letter in each word of string str into uppercase, and converts all other letters into lowercase, then it returns the result.

str data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

Each word in string is classified by white space or characters which are not alphanumeric.  
If str is NULL, the result is also NULL.

The return type is as same as str argument datatype.

<a id="0136d52d586aea2b"></a>
### Example

```
gSQL> SELECT INITCAP( 'hi GLIESE' ) AS RESULT FROM DUAL;
RESULT   
---------
Hi Gliese
1 row selected.
```

<a id="8de36caf5860960a"></a>
## INSTR

<a id="3995ef2b0cfe2fef"></a>
### Syntax

```
INSTR( str, substr [, position [, occurrence ] ] )
```

<a id="c003884698eb844e"></a>
### Description

It search for occurrence<sup>th</sup> substr starting from str's position, and returns its location.

The data types of str arguments and substr arguments can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

The position argument and occurrence argument can be numeric data type.

If position and occurrence are omitted, the default is 1.  
The position and occurrence start from 1, and they are calculated in character unit according to character set (not in byte unit).

The position means the first position to search substr in str, it should not be zero, but an integer value.  
&nbsp;&nbsp;• If the position is positive: It compares forwards  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(toward the right) from the beginning of str until it finds the position of substr.  
&nbsp;&nbsp;•  If the position is negative: It compares backwards    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(toward the left) from the end of str it finds the position of substr.  
&nbsp;&nbsp;•  If the position is 0: The result is 0.

The occurrence means the number of repeating the subtr in the str, and it should be a positive integer.

If any of the input argument is NULL, the result is also NULL.

<a id="30c3bd857543d4d4"></a>
### Example

```
gSQL> SELECT INSTR( 'ABCD ABCD ABCDABCD', 'BC' ) AS RESULT1,
             INSTR( 'ABCD ABCD ABCDABCD', 'BC', 4 ) AS RESULT2
      FROM DUAL;
RESULT1 RESULT2
------- -------
      2       7
1 row selected.

gSQL> SELECT INSTR( 'ABCD ABCD ABCDABCD', 'BC', 5 , 3 ) AS RESULT1,
             INSTR( 'ABCD ABCD ABCDABCD', 'BC', -5,  3 ) AS RESULT2
      FROM DUAL;
RESULT1 RESULT2
------- -------
     16       2
1 row selected.
```

<a id="0c2d50ae48cc1061"></a>
## LAST_DAY

<a id="12a102d71cf2972c"></a>
### Syntax

```
LAST_DAY( date )
```

<a id="076c334a2de43a76"></a>
### Description

It returns the last day of the month which is included in date.

The date argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.  
The return type is always DATE regardless of the date argument data type.

If date is NULL, then it returns NULL.

<a id="af0f2d7b33a06e40"></a>
### Example

```
gSQL> SELECT 
      LAST_DAY( TO_DATE( '2012-07-10', 'YYYY-MM-DD' ) ) AS RESULT FROM DUAL;
RESULT    
----------
2012-07-31
1 row selected.
```

<a id="749b714a42e7eb60"></a>
## LAST_IDENTITY_VALUE

<a id="04fbc0fe5ad15f68"></a>
### Syntax

```
LAST_IDENTITY_VALUE()
```

<a id="b090a96e687f86e5"></a>
### Description

It is the recent value automatically created for an identity column in the current session, and the result type is NATIVE_BIGINT.

If there is not an automatically created value, then it returns null.

This function is similar to @@IDENTITY of MS-SQL and LAST_INSERT_ID() of MySQL. Be cautious when using it because the last altered table determines the value when performing DML for multiple tables as follows.

```
gSQL> INSERT INTO t1(name) VALUES ( 'leekmo' );

1 row created.

gSQL> SELECT LAST_IDENTITY_VALUE() FROM dual;

LAST_IDENTITY_VALUE()
---------------------
                   12

1 row selected.


gSQL> INSERT INTO t2(name) VALUES ( 'leekmo' );

1 row created.



gSQL> SELECT LAST_IDENTITY_VALUE() FROM dual;

LAST_IDENTITY_VALUE()
---------------------
                    2

1 row selected.
```

To obtain an identity column value created when performing the INSERT, use [INSERT INTO name RETURNING .. INTO](18-sql-references.md#f91945147cdebfe8) statement as follows.

```
gSQL> CREATE TABLE t1 ( id INTEGER GENERATED BY DEFAULT AS IDENTITY, name VARCHAR(32) );

Table created.

gSQL> \var v1 integer
gSQL> INSERT INTO t1(name) VALUES ( 'leekmo' ) RETURN id INTO :v1;

V1
--
 1

1 row created.
```

<a id="4cf9ae517954ff49"></a>
### Example

The following is an example of using LAST_IDENTITY_VALUE() function.

```
gSQL> CREATE TABLE t1 ( id   INTEGER GENERATED BY DEFAULT AS IDENTITY,
                        name VARCHAR(32) ); 

Table created.

gSQL> COMMIT;

Commit complete.
```

- There is not an identity value created in the current session.

```
gSQL> SELECT LAST_IDENTITY_VALUE() FROM dual;

LAST_IDENTITY_VALUE()
---------------------
                 null

1 row selected.
```

- Identity value (1) is automatically created.

```
gSQL> INSERT INTO t1(name) VALUES ( 'leekmo' ); 
1 row created.
```

- Result: 1

```
gSQL> SELECT LAST_IDENTITY_VALUE() FROM dual;

LAST_IDENTITY_VALUE()
---------------------
                    1

1 row selected.
```

- Identity value (2) is automatically created as a default value.

```
gSQL> UPDATE t1 SET id = DEFAULT;

1 row updated.
```

- Result: 2

```
gSQL> SELECT LAST_IDENTITY_VALUE() FROM dual;

LAST_IDENTITY_VALUE()
---------------------
                    2

1 row selected.
```

- The user input value does not automatically create an identity value.

```
INSERT INTO t1 VALUES ( 100, 'jhkim' );

1 row updated.
```

- Result: 2

```
SELECT LAST_IDENTITY_VALUE() FROM dual;

LAST_IDENTITY_VALUE()
---------------------
                    2

1 row selected.
```

<a id="f0b815f60fc29fcd"></a>
## LEAST

<a id="402e547c0e401768"></a>
### Syntax

```
LEAST( expr1 [, expr2, ... exprn ] )
```

<a id="38c8a80fd692c6d0"></a>
### Description

It returns the smallest value among received expr arguments.

If any of expr is NULL, the result is NULL.

The result type is determined according to the data type of expr1 (the first expr).   
If the data type of expr1 (the first expr) is a character type and a numeric type then it becomes the type including the range of expr1, ..., exprN each.  
If all of expr1, ..., exprN is described in CHAR type, then all exprs are compared in VARCHAR type and the result type is VARCHAR.

<a id="82f170fd26d580d9"></a>
### Example

```
gSQL> SELECT LEAST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="870862810f0a2cfd"></a>
## LENGTH

<a id="3adcf48ae0eefe57"></a>
### Syntax

```
LENGTH( str )
```

<a id="b9b7265a4be66530"></a>
### Description

It is an alias of [CHAR_LENGTH](#90284f3cb97390d5).

<a id="316089b534b62519"></a>
### Example

Multi byte character set: (e.g.UTF8)

```
gSQL> SELECT LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="16160b297e8ce147"></a>
## LENGTHB

<a id="917f1ece4aacb739"></a>
### Syntax

```
LENGTHB( str )
```

<a id="3ec6c2f87551c792"></a>
### Description

It is an alias of [OCTET_LENGTH](#f5e2f14f42d4ae0f).  
For more information, refer to [BYTE_LENGTH](#6252970883521ebc).

<a id="bcb16ed7182196ee"></a>
### Example

- Multi byte character set (e.g.UTF8): 1 byte character

```
gSQL> SELECT LENGTHB( 'OCTET_LENGTH' ) AS RESULT_1BYTE_CHARACTERS 
        FROM DUAL;
RESULT_1BYTE_CHARACTERS
-----------------------
                     12
1 row selected.
```

- Multi byte character set (e.g.UTF8): 2 byte character

```
gSQL> SELECT LENGTHB( 'αβ' ) AS RESULT_2BYTE_CHARACTERS FROM DUAL;
RESULT_2BYTE_CHARACTERS
-----------------------
                      4
1 row selected.
```

<a id="f94e7f479aee3675"></a>
## LN

<a id="f85362bb26238768"></a>
### Syntax

```
LN( num )
```

<a id="9309c9efba6b56be"></a>
### Description

It returns the natural logarithm value of num.

num should be a value which is bigger than 0.  
If num is NULL, then it returns NULL.

<a id="6209d82aefd48fee"></a>
### Example

```
gSQL> SELECT LN( 2.71828182845905 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="03e7bd17010092b5"></a>
## LNNVL

<a id="4b2d2e4d881bbf59"></a>
### Syntax

```
LNNVL( expr )
```

<a id="17fa7ec5b2e6bc11"></a>
### Description

Logical Not Null VaLue (LNNVL) function is similar to NOT logical operator, but the difference is that it returns TRUE as in the following example when the input value is null.

<a id="91e8dd83be72b929"></a>
### Example

```
gSQL> SELECT c1, c2, (c1 = c2), NOT(c1 = c2), LNNVL(c1 = c2) FROM t1;

C1   C2 (C1 = C2) NOT(C1 = C2) LNNVL(C1 = C2)
-- ---- --------- ------------ --------------
 1    1 TRUE      FALSE        FALSE         
 1    2 FALSE     TRUE         TRUE          
 1 null null      null         TRUE          

3 rows selected.
```

<a id="5acc088f05616d09"></a>
## LOCALTIME

<a id="de1f28631731eaa4"></a>
### Syntax

```
LOCALTIME [()]
STATEMENT_LOCALTIME()
```

<a id="456b7ad59f79bd74"></a>
### Description

The current TIME WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.  
• LOCALTIME, STATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="c5e2e32ef61318d2"></a>
### Example

All rows have the same value.

```
gSQL>  SELECT LOCALTIME FROM t1;

LOCALTIME      
---------------
16:17:08.592459
16:17:08.592459
16:17:08.592459

3 rows selected.
```

<a id="3223425234d69b1c"></a>
## LOCALTIMESTAMP

<a id="015a4f9be0064e5b"></a>
### Syntax

```
LOCALTIMESTAMP [()]
STATEMENT_LOCALTIMESTAMP()
```

<a id="edcbcfc4012448cf"></a>
### Description

The current TIMESTAMP WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• LOCALTIMESTAMP, STATEMENT_LOCALTIMESTAMP(): All TIMESTAMP values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="c800fb49c3e21b3a"></a>
### Example

All rows have the same value.

```
gSQL> SELECT LOCALTIMESTAMP FROM t1;

LOCALTIMESTAMP            
--------------------------
2013-12-12 16:21:51.790614
2013-12-12 16:21:51.790614
2013-12-12 16:21:51.790614

3 rows selected.
```

<a id="336339e8b54bb8af"></a>
## LOCAL_GROUP_ID

<a id="aa86add543c4be24"></a>
### Syntax

```
LOCAL_GROUP_ID()
```

<a id="090928ff04ab3977"></a>
### Description

It returns a cluster group ID for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="04f27c46e159bb1f"></a>
### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_GROUP_ID() FROM DUAL;

LOCAL_GROUP_ID()
----------------
               1

1 row selected.
```

<a id="400525844dcb36cc"></a>
## LOCAL_GROUP_NAME

<a id="3058940981047b6b"></a>
### Syntax

```
LOCAL_GROUP_NAME()
```

<a id="9e5519a6b342fddd"></a>
### Description

It returns a cluster group name for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="a6bbb8e11a8e1733"></a>
### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_GROUP_NAME() FROM DUAL;

LOCAL_GROUP_NAME()
------------------
G1                

1 row selected.
```

<a id="3cfa0a34ab66629a"></a>
## LOCAL_MEMBER_ID

<a id="7ce28d33bfc8212d"></a>
### Syntax

```
LOCAL_MEMBER_ID()
```

<a id="9b6cef194931221f"></a>
### Description

It returns a cluster member ID for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="657ce56704d83521"></a>
### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_MEMBER_ID() FROM DUAL;

LOCAL_MEMBER_ID()
-----------------
                1

1 row selected.
```

<a id="d6e501a9fdb21bc4"></a>
## LOCAL_MEMBER_NAME

<a id="d148cf46fe544d9e"></a>
### Syntax

```
LOCAL_MEMBER_NAME()
```

<a id="28ea7a40d6115ba1"></a>
### Description

It returns a cluster member name for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="eba0c13341678add"></a>
### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_MEMBER_NAME() FROM DUAL;

LOCAL_MEMBER_NAME()
-------------------
G1N1               

1 row selected.
```

<a id="b363566e6b803992"></a>
## LOG

<a id="44f12b424dc857c3"></a>
### Syntax

```
LOG( num2 )
LOG( num1, num2 )
```

<a id="ba2e9b8ad11b6ccd"></a>
### Description

It returns the logarithm of num2 in the num1 base.  
If num1 is omitted, it returns the logarithm value whose base is 10.

num1 should be a positive number except 1 and 0, and num2 should be a positive number.

If num1 or num2 is NULL, then it returns NULL.

<a id="563a4aa1189ff571"></a>
### Example

```
gSQL> SELECT LOG( 100 ) AS RESULT1, LOG( 4, 16 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      2       2
1 row selected.
```

<a id="eb26242ce10eeaf2"></a>
## LOGON_USER

<a id="6cf86c949aae19bf"></a>
### Syntax

```
LOGON_USER()
```

<a id="94856d1b5c1c939e"></a>
### Description

It returns the logged-in user.

The user information is managed in three types as follows.

- Logon user: It is a user who performed login, and it is maintained until the connection is closed.
- Session user: It is as same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: It is generally as same as the session user, but it is temporarily changed internally in system to control access when using the PSM, View.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="db90ac6cbdfc881a"></a>
### Example

```
% gsql test test

gSQL> SELECT LOGON_USER() AS result FROM DUAL;

RESULT
------
TEST  

1 row selected.
```

<a id="eb35bc13a2fb48bb"></a>
## LOWER

<a id="ea4c1b1cd294546f"></a>
### Syntax

```
LOWER( str )
```

<a id="3b03d3bb17187426"></a>
### Description

It returns lowercases of str.

The str argument data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If str is NULL, the result is also NULL.

The return type is the same datatype as the str argument.

<a id="63e0dc9b2a007c84"></a>
### Example

```
gSQL> SELECT LOWER( 'SPRING' ) AS RESULT FROM DUAL;
RESULT
------
spring
1 row selected.
```

<a id="ac631b982b643f95"></a>
## LPAD

<a id="8aec5bd2ecea108d"></a>
### Syntax

```
LPAD( str, length, [, fill] )
```

<a id="6f39d189191d04a5"></a>
### Description

It adds character string fill to the left side of str until the string length becomes length, then returns the result.

The str argument data type can be character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, and a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

The length argument is numeric type.

length means the number of characters, and its maximum range is the maximum precision of the result type.   
If fill is omitted, a white space is added.  
If str is longer than the length, it cuts the str as long as the length, then returns it.  
If any of str, length, fill is NULL, the result is also NULL.   
If length is 0 or a negative number, the result is NULL.

The following table describes the result types.

**Result type of LPAD**

<a id="00f131f224f4b355"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="41083b3ce4e235ca"></a>
### Example

```
gSQL> SELECT LPAD('AA', 5) AS RESULT1,
             LPAD('AA', 5, 'X' ) AS RESULT2,
             LPAD('AA', 1 ) AS RESULT3
      FROM DUAL;
RESULT1 RESULT2 RESULT3
------- ------- -------
   AA   XXXAA   A      
1 row selected.
```

<a id="3a3f1a3db4270cc8"></a>
## LTRIM

<a id="28743949a73ca5a7"></a>
### Syntax

```
LTRIM( trim_source [, trim_character ] )
```

<a id="2c5aacac9a27d8ae"></a>
### Description

It removes the matching characters by comparing from the left side of trim_character in trim_source until the matching character does not exist. Then it returns the result.

The data type of trim_character and trim_source arguments can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, and a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If any of trim_character, trim_source is NULL, the result is NULL.  
If trim_character is omitted, a single blank space (' ') is specified by default.

The following table describes the result types.

**Result type of LTRIM**

<a id="9e188f75e95a8b0a"></a>
| trim_source, trim_character type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="9afc658fc499d65d"></a>
### Example

```
gSQL> SELECT LTRIM( '_____LTRIM', '_' ) AS RESULT FROM DUAL;
RESULT
------
LTRIM 
1 row selected.
```

<a id="afb52fc04ee9a682"></a>
## MAX

<a id="5e6d947a0c47c83c"></a>
### Syntax

```
MAX( [ ALL | DISTINCT ] expr )
```

<a id="49943fe9578a7e22"></a>
### Description

It is an aggregate function and the maximum value among rows' exprs is obtained.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

MAX function returns the same result without being affected by the ALL and DISTINCT.

<a id="87caa614c0449e6e"></a>
### Example

```
gSQL> SELECT MAX(c1) FROM t1;

MAX(C1)
-------
      3

1 row selected.
```

<a id="66edffa4daca1481"></a>
## MIN

<a id="ecc672bfd01fffb3"></a>
### Syntax

```
MIN( [ ALL | DISTINCT ] expr )
```

<a id="8e5d5418752957ff"></a>
### Description

It is an aggregate function and the minimum value among rows' exprs is obtained.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

MIN function returns the same result without being affected by the ALL and DISTINCT.

<a id="7a3c5174a4745376"></a>
### Example

```
gSQL> SELECT MIN(c1) FROM t1;

MIN(C1)
-------
      1

1 row selected.
```

<a id="dc19df4f69745028"></a>
## MOD

<a id="43841cc3447466e8"></a>
### Syntax

```
MOD( num1, num2 )
```

<a id="c63a74755e3a403b"></a>
### Description

It divides num1 by num2, and returns the remainder.  

The num1 argument and num2 argument can be a numeric data type.  
If num2 is 0, an error is returned.  
If the num1 argument or num2 argument is NULL, then NULL is returned.

<a id="a789a1033fd06c67"></a>
### Example

```
gSQL> SELECT MOD(5, 4) AS RESULT1, MOD(-5, 4) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1      -1
1 row selected.
```

<a id="5ce053b5b5dde82b"></a>
## MONTHS_BETWEEN

<a id="577fc884b080f7ca"></a>
### Syntax

```
MONTHS_BETWEEN( date1, date2 )
```

<a id="0f45773fd086a19b"></a>
### Description

MONTHS_BETWEEN returns the number of months of which days between date2 and date1 are divided by 31.

If date1 or date2 is NULL, then the result is also NULL.  
The date1 argument and date2 argument can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE type.

The result type is NUMBER.

> If the same date (e.g. 2014-01-15 and 2014-02-15), or the last day of the month (e.g. 2014-08-31 and 2014-09-30) is included both in date1 and date2, then it returns the integer result regardless of the agreement of timestamp section (if it exists).

<a id="f2b4f13245fe8fe8"></a>
### Example

```
gSQL> SELECT
        MONTHS_BETWEEN('2018-01-18', '2018-01-17')
  FROM DUAL;

MONTHS_BETWEEN('2018-01-18', '2018-01-17')
------------------------------------------
                      3.225806451612903E-2
1 row selected.

gSQL> SELECT
        MONTHS_BETWEEN('2018-02-17', '2018-01-17')
  FROM DUAL;

MONTHS_BETWEEN('2018-02-17', '2018-01-17')
------------------------------------------
                                         1
1 row selected.

gSQL> SELECT
        MONTHS_BETWEEN('2018-02-28', '2018-01-31')
  FROM DUAL;

MONTHS_BETWEEN('2018-02-28', '2018-01-31')
------------------------------------------
                                         1
1 row selected.
```

<a id="e0d515a6d59c4704"></a>
## NEXT_DAY

<a id="2746a5d262c29d86"></a>
### Syntax

```
NEXT_DAY( date, day )
```

<a id="7636173371116263"></a>
### Description

It obtains a date of the day (day of week) which comes first after the given date (an argument).

The second day argument can be a string or a number which indicates the day.  
• String: SUNDAY ~ SATURDAY  or SUN ~ SAT  
• Number: 1 (sunday) ~ 7 (saturday)  

If any of the input argument is NULL, the result is also NULL.

The return type is always DATE regardless of the input type of the date.  
The hour, minute and second of the result value returns the same hour, minute and second of the input argument date.

<a id="a8604b6d11ea4121"></a>
### Example

- 2020-08-11 is Tuesday.

```
gSQL> SELECT NEXT_DAY( TO_DATE( '2020-08-11', 'YYYY-MM-DD'),
                       'SUNDAY' ) AS RESULT1
      FROM DUAL;
RESULT1   
----------
2020-08-16
1 row selected.

gSQL> SELECT NEXT_DAY( TO_DATE( '2020-08-11', 'YYYY-MM-DD' ),
                       'SUN' ) AS RESULT1
FROM DUAL;
RESULT1   
----------
2020-08-16
1 row selected.

gSQL> SELECT NEXT_DAY( TO_DATE( '2020-08-11', 'YYYY-MM-DD' ),
                       1 ) AS RESULT1
FROM DUAL;
RESULT1   
----------
2020-08-16
1 row selected.

gSQL> SELECT TO_CHAR( NEXT_DAY( TO_DATE( '2020-08-11', 'YYYY-MM-DD' ),
                                'SUNDAY' ),
                      'YYYY-MM-DD HH24:MI:SS' ) AS RESULT1
FROM DUAL;
RESULT1            
-------------------
2020-08-16 00:00:00
1 row selected.
```

<a id="1c44abe739678742"></a>
## NEXTVAL

<a id="3fda4e0f46a5394e"></a>
### Syntax

```
seq_name.NEXTVAL
NEXTVAL( seq_name )
NEXT VALUE FOR seq_name
```

<a id="84d8db11a6b8616c"></a>
### Description

It obtains the next value of the sequence object.

<a id="0c3dd586c86f4aca"></a>
### Example

```
gSQL> CREATE SEQUENCE seq;

Sequence created.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT seq.NEXTVAL FROM dual;

SEQ.NEXTVAL
-----------
          1

1 row selected.

gSQL> SELECT NEXTVAL( seq ) FROM dual;

NEXTVAL( SEQ )
--------------
             2

1 row selected.

gSQL> SELECT NEXT VALUE FOR seq FROM dual;

NEXT VALUE FOR SEQ
------------------
                 3

1 row selected.
```

<a id="ac67e7ce157daa37"></a>
## NULLIF

<a id="6a0fde0ca3cfd1e7"></a>
### Syntax

```
NULLIF( expr1, expr2 )
```

<a id="5b49799a17c1ca19"></a>
### Description

If expr1 is equal to expr2, it returns NULL. If it is not equal it returns expr1 which is the first argument.

If the data types of expr1 and expr2 are different, the result type is determined by [Result Type Combination Rule](11-sql-elements.md#8ed35905e84aa434).

NULLIF can be expressed by using CASE as follows.

- NULLIF( expr1, expr2 )

```
CASE WHEN expr1 = expr2 THEN NULL 
       ELSE expr1 
  END
```

<a id="3d3b675416e5e224"></a>
### Example

```
gSQL> SELECT NULLIF( 'SUN', 'SUN' ) AS RESULT1, 
             NULLIF( 'SUN', 'MOON' ) AS RESULT2 
       FROM DUAL;
RESULT1 RESULT2
------- -------
null    SUN    
1 row selected.
```

<a id="178b15afb662f3e7"></a>
## NUMTODSINTERVAL

<a id="15a9133b6db45907"></a>
### Syntax

```
NUMTODSINTERVAL( num, interval_indicator )
```

<a id="385e8952d07b7d70"></a>
### Description

It converts the number in interval_indicator unit to interval day to second type, then returns it.

The argument *number* is a numeric type.

The argument interval_indicator is a character type, like CHAR or VARCHAR, and it should be one of 'DAY', 'HOUR', 'MINUTE', 'SECOND' which is case insensitive.

If any argument is NULL, then NULL is returned as a result.

interval day(6) to second(6) type is returned as a result, and a user can not arbitrarily modify the precision. If the leading precision of the converted result exceeds the default precision, then an error is returned. If the fraction precision exceeds the default precision, then the rounded value is returned as a result.

<a id="4e671bae7f100cbe"></a>
### Example

- It converts *1 Day* to interval day to second type.

```
gSQL> SELECT NUMTODSINTERVAL(1, 'DAY') FROM DUAL;

NUMTODSINTERVAL(1, 'DAY')
-------------------------
+000001 00:00:00.000000  

1 row selected.
```

- It converts *36 Hour* to interval day to second type.

```
gSQL> SELECT NUMTODSINTERVAL(36, 'HOUR') FROM DUAL;

NUMTODSINTERVAL(36, 'HOUR')
---------------------------
+000001 12:00:00.000000    

1 row selected.
```

- It converts *1530 Minute* to interval day to second type.

```
gSQL> SELECT NUMTODSINTERVAL(1530, 'MINUTE') FROM DUAL;

NUMTODSINTERVAL(1530, 'MINUTE')
-------------------------------
+000001 01:30:00.000000        

1 row selected.
```

- It converts *90100.1234567 Second* to interval day to second type.

```
gSQL> SELECT NUMTODSINTERVAL(90100.1234567, 'SECOND') FROM DUAL;

NUMTODSINTERVAL(90100.1234567, 'SECOND')
----------------------------------------
+000001 01:01:40.123457                 

1 row selected.
```

<a id="65a06975c0f29f33"></a>
## NUMTOYMINTERVAL

<a id="04b1ad431466846a"></a>
### Syntax

```
NUMTOYMINTERVAL( num, interval_indicator )
```

<a id="d065438884df2156"></a>
### Description

It converts the number in interval_indicator unit to interval year to month type, then returns it.

The argument *number* is a numeric type.

The argument interval_indicator is a character type, like CHAR or VARCHAR, and it should be one of 'YEAR', 'MONTH' which is case insensitive.

If any argument is NULL, then NULL is returned as a result.

interval year(6) to month type is returned as a result, and a user can not arbitrarily modify the precision. If the leading precision of the converted result exceeds the default precision, then an error is returned.

<a id="42466b4cad446883"></a>
### Example

- It converts *1 Year* to interval year to month type.

```
gSQL> SELECT NUMTOYMINTERVAL(1, 'YEAR') FROM DUAL;

NUMTOYMINTERVAL(1, 'YEAR')
--------------------------
+000001-00                

1 row selected.
```

- It converts *13.5 Month* to interval year to month type.

```
gSQL> SELECT NUMTOYMINTERVAL(13.5, 'MONTH') FROM DUAL;

NUMTOYMINTERVAL(13.5, 'MONTH')
------------------------------
+000001-02                    

1 row selected.
```

<a id="ef72769c9a4788e3"></a>
## NVL

<a id="90eaf62e24c68f4f"></a>
### Syntax

```
NVL( expr1, expr2 )
```

<a id="5cd4a6e787ccaf6a"></a>
### Description

If expr1 is not NULL, then it returns expr1. If expr1 is NULL, it returns expr2.

The result type is determined according to the data type of expr1.  
If NULL is described in expr1, then the result type is determined according to the data type of expr2.   
If the data type of expr1 is a character type and a numeric type then it becomes the type including the range of expr1 and expr2 each.  
If the data type of both expr1 and expr2 is CHAR type, then the result type is VARCHAR.

<a id="2ccc4e9d1e4d19bf"></a>
### Example

```
gSQL> SELECT I1, NVL( I1, 0 ) FROM T1;
  I1 NVL( I1, 0 )
---- ------------
   1            1
null            0
2 rows selected.
```

<a id="9c0e50ffc1d6c8cc"></a>
## NVL2

<a id="471ba0fb87a3b2fc"></a>
### Syntax

```
NVL2( expr1, expr2, expr3 )
```

<a id="9fa05b3550629001"></a>
### Description

If expr1 is not null, then it returns expr2. If expr1 is NULL, it returns expr3.

The result type is determined according to the data type of expr2.   
If NULL is described in expr2, then the result type is determined according to the data type of expr3.  
If the data type of expr2 is a character type and a numeric type then it becomes the type including the range of expr2 and expr3 each.  
If the data type of both expr2 and expr3 is CHAR type, then the result type is VARCHAR.

<a id="d5fd8ebbb432e8c5"></a>
### Example

```
gSQL> SELECT I1, NVL2( I1, I1 * 1000, 0 ) FROM T1;
  I1 NVL2( I1, I1 * 1000, 0 )
---- ------------------------
   1                     1000
null                        0
2 rows selected.
```

<a id="f5e2f14f42d4ae0f"></a>
## OCTET_LENGTH

<a id="1f0d7444b29fe647"></a>
### Syntax

```
OCTET_LENGTH( str )  

BYTE_LENGTH( str )     

LENGTHB( str )
```

<a id="def73abf91453524"></a>
### Description

It returns the number of bytes in str.

The str argument data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONGVARYING.

If the str data type is CHARACTER, the white spaces are included in the calculation.  
If str is NULL, the result is also NULL.

It is an alias of [BYTE_LENGTH](#6252970883521ebc) and [LENGTHB](#16160b297e8ce147).

<a id="4fedd9c769f2a672"></a>
### Example

- Multi byte character set (e.g. UTF8): 1 byte character

```
gSQL> SELECT OCTET_LENGTH( 'OCTET_LENGTH' ) AS RESULT_1BYTE_CHARACTERS 
        FROM DUAL;
RESULT_1BYTE_CHARACTERS
-----------------------
                     12
1 row selected.
```

- Multi byte character set (e.g. UTF8): 2 byte character

```
gSQL> SELECT OCTET_LENGTH( 'αβ' ) AS RESULT_2BYTE_CHARACTERS FROM DUAL;
RESULT_2BYTE_CHARACTERS
-----------------------
                      4
1 row selected.
```

<a id="22fab77b380f2124"></a>
## OVERLAY

<a id="da5ab62e6d809b35"></a>
### Syntax

```
OVERLAY( str1 PLACING str2 FROM start_position  [ FOR string_length ] )
```

<a id="53958435cadb99fb"></a>
### Description

It overlays the characters in the range between str1's start_position and string_lenght with str2.

The data types of str1 argument and str2 argument can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING  

The start_position argument and string_length argument can be numeric data type.

- OVERLAY function has the following result.
    - When FOR is specified.  
      SUBSTRING( str1 FROM 1 FOR (start_position - 1) )  
      || str2  
      || SUBSTRING( str1 FROM (start_position + string_length )
    - When FOR is omitted.  
      SUBSTRING( str1 FROM 1 FOR (start_position - 1) )  
      || str2  
      || SUBSTRING( str1 FROM (start_position + CHAR_LENGTH(str2))

For more information, refer to [SUBSTRING](#bba28ac2ca8a9186).

The following table describes the result types.

**Result type of OVERLAY**

<a id="577437ac4110d01d"></a>
| str1, str2 types | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="c558655ed1d73872"></a>
### Example

```
gSQL> SELECT
         OVERLAY( 'RESULT_OF_XXX_FUNC' PLACING 'OVERLAY' FROM 11 )
         AS RESULT1,
         OVERLAY( 'RESULT_OF_XXX_FUNC' PLACING 'OVERLAY' FROM 11 FOR 3 )
         AS RESULT2
      FROM DUAL;
RESULT1            RESULT2               
------------------ ----------------------
RESULT_OF_OVERLAYC RESULT_OF_OVERLAY_FUNC
1 row selected.
```

<a id="a772f0c90f1e1f39"></a>
## PHYSICAL_LENGTH

<a id="774839154b6dcc7c"></a>
### Syntax

```
PHYSICAL_LENGTH( expr )
```

<a id="7095dadc6bb622e5"></a>
### Description

PHYSICAL_LENGTH returns the number of internal expression information bytes in expr.

The expr argument can be any data type.

If an input argument is NULL, then the result is 0.

<a id="79c3536a9881e1d3"></a>
### Example

- When an input argument is NULL

```
gSQL> SELECT PHYSICAL_LENGTH( NULL ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

- The following example shows the number of NUMBER type bytes of 1, 123 and 12345.

```
gSQL> SELECT PHYSICAL_LENGTH( 1 ) AS RESULT FROM DUAL;
RESULT
------
     2
1 row selected.

gSQL> SELECT PHYSICAL_LENGTH( 123 ) AS RESULT FROM DUAL;
RESULT
------
     3
1 row selected.

gSQL> SELECT PHYSICAL_LENGTH( 12345 ) AS RESULT FROM DUAL;
RESULT
------
     4
1 row selected.
```

<a id="63271fe818542bed"></a>
## PI

<a id="9374055098efa19f"></a>
### Syntax

```
PI()
```

<a id="2f2324745a45a1b3"></a>
### Description

It returns "π" constant.

<a id="0772cb4513b61b46"></a>
### Example

```
gSQL> SELECT PI() AS RESULT FROM DUAL;
              RESULT
--------------------
3.141592653589793E+0
1 row selected.
```

<a id="b498924215a64eb5"></a>
## POSITION

<a id="713c4cb13150fe69"></a>
### Syntax

```
POSITION( str1 IN str2 )
```

<a id="d2054d366b152aef"></a>
### Description

It searches for the first str1 within str2, then returns its location.

The data type of str1 argument and str2 argument can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If str1 can not be found within str2, the return value is 0.  
If str1 is found within str2, the position of str1 is returned, and the return value starts from 1.  
The returned position value is calculated in character unit (not in byte unit).  
If str1 or str2 is NULL, the return value is also NULL.

<a id="54064c9e522b60db"></a>
### Example

```
gSQL> SELECT POSITION( 'CHAR' IN 'LONG CHAR 2000' ) AS RESULT FROM DUAL;
RESULT
------
     6
1 row selected.
```

<a id="97add6e19cdcbcbe"></a>
## POWER

<a id="c18243057a82af7b"></a>
### Syntax

```
POWER( num1, num2 )
```

<a id="de534a31652a3cb8"></a>
### Description

It squares num1 to num2, and returns the result.

The num1 argument and num2 argument can be a numeric data type.  

If num1 is a negative number, num2 should be an integer.  
If num1 or num2 is NULL, the result is also NULL.

<a id="38e03e0c980872be"></a>
### Example

```
gSQL> SELECT POWER( 2, 3 ) AS RESULT FROM DUAL;
RESULT
------
     8
1 row selected.
```

<a id="33b07c6c7233f020"></a>
## RADIANS

<a id="84102c4dbf9528cf"></a>
### Syntax

```
RADIANS( degrees )
```

<a id="153b345015a6e59b"></a>
### Description

It returns the radians of degrees.  

The degrees argument can be a numeric data type.  
If the degrees argument is NULL, then NULL is returned.

<a id="c9c84581961cd102"></a>
### Example

```
gSQL> SELECT RADIANS( 180 ) AS RESULT FROM DUAL;
          RESULT
----------------
3.14159265358979
1 row selected.
```

<a id="f1daee920e3614fe"></a>
## RANDOM

<a id="4aedf57c20f14b3c"></a>
### Syntax

```
RANDOM( min, max )
```

<a id="4df2c3a5d6e47a92"></a>
### Description

It returns a random value in the range above min and below max.  

The min argument and max argument can be a numeric data type.  
If either min argument or the max argument is NULL, then NULL is returned.

<a id="8812e40925afbbd9"></a>
### Example

```
gSQL> SELECT RANDOM( 1, 100 ) AS RESULT FROM DUAL;
          RESULT
----------------
34.1870528003201
1 row selected.
```

<a id="67725f70fa61958a"></a>
## REPEAT

<a id="97182ef2788c8663"></a>
### Syntax

```
REPEAT( str, num )
```

<a id="3a5aa7128b28b6d4"></a>
### Description

The string repeats str as many times as specified in num, and returns the result.

The str argument can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

The num argument can be a numeric data type.

If either str or num is NULL, the result is also NULL.  
If num is 0 or a negative number, the result is also NULL.

The following table describes the result types.

**Result type of REPEAT**

<a id="f44d6e52f008a1e7"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="4c2bf3272536394c"></a>
### Example

```
gSQL> SELECT REPEAT( 'ab', 3 ) AS RESULT FROM DUAL;
RESULT
------
ababab
1 row selected.
```

<a id="d10abdb71b8eb3fc"></a>
## REPLACE

<a id="cc0dbaa117e4145e"></a>
### Syntax

```
REPLACE( str, from, to )
```

<a id="57cfce7f54c1415d"></a>
### Description

It replaces all *from* strings in str string with *to* strings, and returns the result.

The str argument, the from argument, and the to argument can be character data types such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If str is NULL, the result is also NULL.  
If from is NULL, the str is returned without replacement.  
If to value is omitted or NULL, the str value of which from is removed is returned.

The following table describes the result types.

**Result type of REPLACE**

<a id="ff92dd9937b38c07"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="f23711763bd9f13f"></a>
### Example

```
gSQL> SELECT REPLACE( 'HI GLIESE', 'HI', 'HELLO' ) AS RESULT FROM DUAL;
RESULT      
------------
HELLO GLIESE
1 row selected.
```

<a id="1891b5e3a70c0bd8"></a>
## REVERSE

<a id="0e99ab23834b5417"></a>
### Syntax

```
REVERSE( str )
```

<a id="3bd7f50ec79fd3e9"></a>
### Description

REVERSE returns characters of str in reverse order.

The str argument can be types that are convertible to a character string type or a binary string type.  
A character string type is performed in a character unit, and a binary string type can be performed in a byte unit.

If str is NULL, then it returns NULL.

The following table describes the arguments and result types.

**Argument and result type of REVERSE**

<a id="874fa12a822efc34"></a>
| str | Result type |
| --- | --- |
| CHAR | CHAR |
| VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY | BINARY |
| VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="fd5916af5a6ce99a"></a>
### Example

```
gSQL> SELECT REVERSE( 'GOLDILOCKS' ) AS RESULT FROM DUAL;

RESULT      
----------
SKCOLIDLOG

1 row selected.

gSQL> SELECT REVERSE( '선재소프트 2018' ) AS RESULT FROM DUAL;

RESULT         
---------------
8102 트프소재선

1 row selected.
```

<a id="106df7e6dd5a1b21"></a>
## ROUND( number )

<a id="8d608827f8a867a4"></a>
### Syntax

```
ROUND( num [, scale ] )
```

<a id="26243f1241e715d5"></a>
### Description

It rounds off num based on scale, and returns the result.

The num argument and scale argument can be numeric data types.

If scale is omitted, the scale becomes 0 and is executed as if it is ROUND(num, 0).  
If scale is a positive number, it is rounded off based on the number of right digit of the decimal point. If scale is a negative number, it is rounded off based on the number of left digit of the decimal point.  

If either num argument or the scale argument is NULL, then NULL is returned.

<a id="eb549afd0f934f68"></a>
### Example

```
gSQL> SELECT ROUND( 152.4282, 2 ) AS RESULT FROM DUAL;
RESULT
------
152.43
1 row selected.

gSQL> SELECT ROUND( 152.4282, -2 ) AS RESULT FROM DUAL;
RESULT
------
   200
1 row selected.
```

<a id="98ce880e79125048"></a>
## ROUND( date )

<a id="6151859e6b5bca1f"></a>
### Syntax

```
ROUND( date [ , fmt ] )
```

<a id="8ab5d42c7418af8f"></a>
### Description

It rounds off the date in the specified fmt unit, and returns the result.

The data type of date argument can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.   
The fmt argument can be a character type such as CHARACTER, CHARACTER VARYING.   
If either date argument or the fmt argument is NULL, then NULL is returned.  

The result type is always DATE regardless of the date argument data type.

If fmt is omitted, the default is DAY.  
The following table describes the available format strings.

**Available format sting of fmt**

<a id="82b07fd07949044b"></a>
| String | Description |
| --- | --- |
| CC, SCC | It is represented in four digit year by rounding off from 51 year. (e.g. XX01) |
| YYYY, YEAR, SYYYY, SYEAR, YYY, YY, Y | It is rounded off from July 1st. |
| IYYY, IYY, IY, I | It is the year embracing the calendar week defined by ISO 8601 standards, and it is rounded off from July 1st. |
| Q | It is rounded off from the 16th day in the second month of the quarter. |
| MONTH, MON, MM, RM | It is rounded off from the 16th day. |
| WW | A week starts from January 1st of the year, and it is rounded off on wednesday 12 p.m of WEEK. |
| IW | It is the calendar week defined by ISO 8601 standards (1 ~ 52 weeks or 1 ~ 53 weeks), and it is rounded off on thursday 12 p.m. |
| W | A week starts from the 1st day of the month, and it is rounded off on wednesday 12 p.m of WEEK. |
| DDD, DD, J | It is rounded off at 12 p.m. |
| DAY, DY, D | It is rounded off on wednesday 12 p.m of WEEK. |
| HH, HH12, HH24 | It is rounded off from 30 minutes. |
| MI | It is rounded off from 30 seconds. |

<a id="c6e006563d0f17b8"></a>
### Example

```
gSQL> SELECT 
      ROUND( TO_DATE( '2051-07-16', 'YYYY-MM-DD' ), 'CC' ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2101-01-01
1 row selected.

gSQL> SELECT 
      ROUND( TO_DATE( '2051-07-16', 'YYYY-MM-DD' ), 'YYYY' ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2052-01-01
1 row selected.

gSQL> SELECT 
      ROUND( TO_DATE( '2051-07-16', 'YYYY-MM-DD' ), 'MONTH' ) AS   RESULT 
      FROM DUAL;
RESULT    
----------
2051-08-01
1 row selected.

gSQL> SELECT 
      ROUND( TO_TIMESTAMP( '2001-05-05 15:22:33.999999', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ) ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2001-05-06
1 row selected.
```

<a id="ddfe11708471135f"></a>
## ROWID_GRID_BLOCK_ID

<a id="5456ef310d05a513"></a>
### Syntax

```
ROWID_GRID_BLOCK_ID( rowid )
```

<a id="28751c6c24a6d715"></a>
### Description

It returns the GRID block ID.

> It is a valid information in a cluster system.

<a id="ae8b1bf3be11b039"></a>
### Example

```
gSQL> SELECT C1, ROWID_GRID_BLOCK_ID( ROWID ) FROM T1;
C1 ROWID_GRID_BLOCK_ID( ROWID )
-- ----------------------------
 1                           52
 2                           52
 3                           52

3 rows selected.
```

<a id="8aba479cf489f797"></a>
## ROWID_GRID_BLOCK_SEQ

<a id="1535af30e4e27854"></a>
### Syntax

```
ROWID_GRID_BLOCK_SEQ( rowid )
```

<a id="c2414d6a1c554e33"></a>
### Description

It returns the GRID block sequence.

> It is a valid information in a cluster system.

<a id="e7bb6fd988305dc5"></a>
### Example

```
gSQL> SELECT C1, ROWID_GRID_BLOCK_SEQ( ROWID ) FROM T1;
C1 ROWID_GRID_BLOCK_SEQ( ROWID )
-- -----------------------------
 1                        747465
 2                        747466
 3                        747467

3 rows selected.
```

<a id="1df9cf89ebed3d42"></a>
## ROWID_MEMBER_ID

<a id="4867245c2eab6da2"></a>
### Syntax

```
ROWID_MEMBER_ID( rowid )
```

<a id="cb22642b848fd613"></a>
### Description

It returns the member ID.

> It is a valid information in a cluster system.

<a id="38b10ee414031eed"></a>
### Example

```
gSQL> SELECT C1, ROWID_MEMBER_ID( ROWID ) FROM T1;
C1 ROWID_MEMBER_ID( ROWID )
-- ------------------------
 1                        1
 2                        1
 3                        1

3 rows selected.
```

<a id="ee23eff9e0d7f085"></a>
## ROWID_OBJECT_ID

<a id="b75246a14f70aff2"></a>
### Syntax

```
ROWID_OBJECT_ID( rowid )
```

<a id="0fc2a5412d4b8677"></a>
### Description

It returns the object ID.

> It is an invalid information in a cluster system.

<a id="e94407e2dea9e1bb"></a>
### Example

```
gSQL> SELECT ROWID_OBJECT_ID( t1.ROWID ) FROM t1;
ROWID_OBJECT_ID( T1.ROWID )
---------------------------
                      22012
                      22012
                      22012
                      22012
4 rows selected.
```

<a id="3ed2fa111af4d72d"></a>
## ROWID_PAGE_ID

<a id="c1e444fc030ac2c3"></a>
### Syntax

```
ROWID_PAGE_ID( rowid )
```

<a id="bd440ad21fc151b6"></a>
### Description

It returns the page ID.

> It is an invalid information in a cluster system.

<a id="70b5c2959d1645cf"></a>
### Example

```
gSQL> SELECT ROWID_PAGE_ID( t1.ROWID ) FROM t1;
ROWID_PAGE_ID( T1.ROWID )
-------------------------
                     8227
                     8227
                     8227
                     8227
4 rows selected.
```

<a id="73837b7a58117857"></a>
## ROWID_ROW_NUMBER

<a id="74d374468fc59841"></a>
### Syntax

```
ROWID_ROW_NUMBER( rowid )
```

<a id="5735fc62e207c80d"></a>
### Description

It returns the row number.

> It is an invalid information in a cluster system.

<a id="d59d3acc22dc2aef"></a>
### Example

```
gSQL> SELECT ROWID_ROW_NUMBER( t1.ROWID ) FROM t1;
ROWID_ROW_NUMBER( T1.ROWID )
----------------------------
                           0
                           1
                           2
                           3
4 rows selected.
```

<a id="69d78340f593c9a7"></a>
## ROWID_SHARD_ID

<a id="17a38e05dbd2d8b3"></a>
### Syntax

```
ROWID_SHARD_ID( rowid )
```

<a id="39bc3d854027a83e"></a>
### Description

It returns the shard ID.

> It is a valid information in a cluster system.

<a id="a2e27183740d5d30"></a>
### Example

```
gSQL> SELECT C1, ROWID_SHARD_ID( ROWID ) FROM T1;
C1 ROWID_SHARD_ID( ROWID )
-- -----------------------
 1                       0
 2                       1
 3                       2

3 rows selected.
```

<a id="2e8c7c55fc762b26"></a>
## ROWID_TABLESPACE_ID

<a id="1fc8edb427dc2fe3"></a>
### Syntax

```
ROWID_TABLESPACE_ID( rowid )
```

<a id="9def80eb5642f692"></a>
### Description

It returns the tablespace ID.

> It is an invalid information in a cluster system.

<a id="5de43bf40acd0a2d"></a>
### Example

```
gSQL> SELECT ROWID_TABLESPACE_ID( t1.ROWID ) FROM t1;
ROWID_TABLESPACE_ID( T1.ROWID )
-------------------------------
                              2
                              2
                              2
                              2
4 rows selected.
```

<a id="295d2d14e2c704a6"></a>
## ROWNUM

<a id="d6862a70aa0b1055"></a>
### Syntax

```
ROWNUM
```

<a id="b81218f4ce53f025"></a>
### Description

It sequentially allocates a number starting from 1 to rows which satisfy the WHERE condition.

It allows using ROWNUM in WHERE clause for the compatibility with Oracle.

However, to restrict the number of the query results, it is recommended to use [offset limit clause](18-sql-references.md#c09e07831754ec15) (the SQL standard) as follows.

- (Non standard) Describing the number of the results by using ROWNUM

```
gSQL> SELECT * FROM t1 WHERE ROWNUM <= 3;

C1
--
A 
B 
C 

3 rows selected.
```

- (SQL standard) Describing the number of the results by using FETCH statement

```
gSQL> SELECT * FROM t1 FETCH 3;

C1
--
A 
B 
C 

3 rows selected.
```

To restrict the range of the query results, it is recommended to use OFFSET, FETCH statement as follows.

- (Non standard) Describing the range of the number of the results by using ROWNUM

```
gSQL> SELECT c1 
        FROM ( SELECT ROWNUM rn, c1 
                 FROM t1 )
        WHERE rn BETWEEN 2 AND 3;

C1
--
B 
C 

2 rows selected.
```

- (SQL standard) Describing the range of the number of the results by using ROWNUM OFFSET, FETCH statement

```
gSQL> SELECT c1 FROM t1 OFFSET 1 FETCH 2;

C1
--
B 
C 

2 rows selected.
```

It is not recommended to use ROWNUM in WHERE clause for any other uses than the restriction of the number of the results.

The results for the same query may be different according to the execution method as follows when using the ambiguous condition (WHERE c1 < ROWNUM + 3).

- Creating the data

```
CREATE TABLE t1 ( c1 INTEGER );
CREATE INDEX t1_idx ON t1(c1);
INSERT INTO t1 VALUES (1);
INSERT INTO t1 VALUES (2);
INSERT INTO t1 VALUES (3);
INSERT INTO t1 VALUES (4);
INSERT INTO t1 VALUES (5);
COMMIT;
```

- In case of Oracle

```
SQL> SELECT ROWNUM, c1 FROM t1 WHERE c1 < ROWNUM + 3;

    ROWNUM	   C1
---------- ----------
	 1	    1
	 2	    2

SQL> DROP INDEX t1_idx;
```

    - The index has been deleted.

```
SQL> SELECT ROWNUM, c1 FROM t1 WHERE c1 < ROWNUM + 3;

    ROWNUM	   C1
---------- ----------
	 1	    1
	 2	    2
	 3	    3
	 4	    4
	 5	    5
```

- In case of GOLDILOCKS

```
gSQL> SELECT ROWNUM, c1 FROM t1 WHERE c1 < ROWNUM + 3;

ROWNUM C1
------ --
     1  1
     2  2
     3  3
     4  4
     5  5

5 rows selected.

gSQL> DROP INDEX t1_idx;

Index dropped.

gSQL> SELECT ROWNUM, c1 FROM t1 WHERE c1 < ROWNUM + 3;

ROWNUM C1
------ --
     1  1
     2  2
     3  3
     4  4
     5  5

5 rows selected.
```

<a id="b20df0bcd815bdcf"></a>
### Example

```
gSQL> SELECT ROWNUM, c1 FROM t1;

ROWNUM C1
------ --
     1 A 
     2 B 
     3 C 
     4 D 
     5 E 

5 rows selected.
```

<a id="8a9889395cf0b5c2"></a>
## RPAD

<a id="ed2c19d550001a59"></a>
### Syntax

```
RPAD( str, length, [, fill] )
```

<a id="00185c2943fc9cff"></a>
### Description

It adds fill string to the right side of str until the string's length becomes length, and it returns the result.

The str argument can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONGVARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

The length argument can be a numeric type.

length means the number of characters, and its maximum range is the maximum PRECISION of the result type.   
If fill is omitted, a white space is added.  
If str is longer than length, it cuts the str as long as the length, then returns it.  
If any of str, length, fill is NULL, the result is also NULL.   
If length is 0 or a negative number, the result is NULL.

The following table describes the result types.

**Result type of RPAD**

<a id="26e7897ddf1df0ba"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="8990770e2e4a6b5b"></a>
### Example

```
gSQL> SELECT RPAD('AA', 5) AS RESULT1,
             RPAD('AA', 5, 'X') AS RESULT2,
             RPAD('AA', 1) AS RESULT3
      FROM DUAL; 
RESULT1 RESULT2 RESULT3
------- ------- -------
AA      AAXXX   A      
1 row selected.
```

<a id="d46515ca1b2019ff"></a>
## RTRIM

<a id="6c4155b59ab7cacc"></a>
### Syntax

```
RTRIM( trim_source [, trim_character ] )
```

<a id="4d75c3b4b883640a"></a>
### Description

It removes the matching characters by comparing from the right side of trim_character in trim_source until the matching character does not exist. Then it returns the result.

The data type of trim_character and trim_source arguments can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING or a binary data type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If any of trim_character, trim_source is NULL, the result is NULL.  
If trim_character is omitted, a single blank space (' ') is specified by default.

The following table describes the result types.

**Result type of RTRIM**

<a id="0ad1181b31cc3cdd"></a>
| trim_source type, trim_character type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="5106a98f91f40cd1"></a>
### Example

```
gSQL> SELECT RTRIM('      rtrim      ') AS RESULT1,
             RTRIM('______rtrim______','_') AS RESULT2
      FROM DUAL;
RESULT1     RESULT2    
----------- -----------
      rtrim ______rtrim
1 row selected.
```

<a id="c85bfe5585eb42cc"></a>
## SESSION_ID

<a id="9b8822ee08fe0b24"></a>
### Syntax

```
SESSION_ID()
```

<a id="dd175d4947414322"></a>
### Description

It obtains the current session ID.

<a id="b23e8660c5f7c0c7"></a>
### Example

```
gSQL> SELECT SESSION_ID() FROM dual;

SESSION_ID()
------------
           4

1 row selected.
```

<a id="f7b01dfa0f976860"></a>
## SESSION_SERIAL

<a id="278e9df8ec2c66f0"></a>
### Syntax

```
SESSION_SERIAL()
```

<a id="0dcbdd54b9f3afd4"></a>
### Description

It obtains the serial number of current session.

<a id="876b60486ee07521"></a>
### Example

```
gSQL> SELECT SESSION_SERIAL() FROM dual;

SESSION_SERIAL()
----------------
              16

1 row selected.
```

<a id="4346986d9bf8e7dc"></a>
## SESSION_USER

<a id="bc7b5436e17c4044"></a>
### Syntax

```
SESSION_USER[()]
```

<a id="b78dc43f0be02a17"></a>
### Description

It returns the session user.

The user information is managed in three types as follows.

- Logon user: It is a user who performed login, and it is maintained until the connection is closed.
- Session user: It is as same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: It is generally as same as the session user, but it is temporarily changed internally in system to control access when using the PSM, view.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="a0342c1697abd6ee"></a>
### Example

```
% gsql sys gliese
gSQL>  SET SESSION AUTHORIZATION test;

Session set.

gSQL> SELECT LOGON_USER() AS result1, SESSION_USER() AS result2 FROM DUAL;

RESULT1 RESULT2
------- -------
SYS     TEST   

1 row selected.
```

<a id="9a80b9e45f815567"></a>
## SHARD_GROUP_ID

<a id="b33ce77cf931a15b"></a>
### Syntax

```
SHARD_GROUP_ID( table_name, shard_key_value [, ... ] )
```

<a id="3edb25206563eb3c"></a>
### Description

It returns the group ID managing the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is NATIVE_BIGINT.

> It is a valid information in a cluster system.

<a id="2e1138c850de8a89"></a>
### Example

```
gSQL> SELECT T1.C1, SHARD_GROUP_ID( T1, T1.C1 ) FROM T1;
C1 SHARD_GROUP_ID( T1, T1.C1 )
-- ---------------------------
A                            1
B                            2
C                            3

3 rows selected.


gSQL> SELECT SHARD_GROUP_ID( T1, 'B' ) FROM DUAL;
SHARD_GROUP_ID( T1, 'B' )
-------------------------
                        2

1 row selected.
```

<a id="a771660b6f2d5eb4"></a>
## SHARD_GROUP_NAME

<a id="b1d2892ed478157b"></a>
### Syntax

```
SHARD_GROUP_NAME( table_name, shard_key_value [, ... ] )
```

<a id="19d7b5f952b34b31"></a>
### Description

It returns the group NAME managing the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is VARCHAR.

> It is a valid information in a cluster system.

<a id="963f1631858e0c3c"></a>
### Example

```
gSQL> SELECT T1.C1, SHARD_GROUP_NAME( T1, T1.C1 ) FROM T1;

C1 SHARD_GROUP_NAME( T1, T1.C1 )
-- -----------------------------
A  G1                           
B  G2                           
C  G3                           

3 rows selected.

gSQL> SELECT SHARD_GROUP_NAME( T1, 'B' ) FROM DUAL;

SHARD_GROUP_NAME( T1, 'B' )
---------------------------
G2                         

1 row selected.
```

<a id="106113d974f19879"></a>
## SHARD_ID

<a id="e5a893a0c9c41836"></a>
### Syntax

```
SHARD_ID( table_name, shard_key_value [, ... ] )
```

<a id="6ee679b5a51f3720"></a>
### Description

It returns the ID for the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is NATIVE_BIGINT.

> It is a valid information in a cluster system.

<a id="174ef40c0bb03995"></a>
### Example

```
gSQL> SELECT T1.C1, SHARD_ID( T1, T1.C1 ) FROM T1;
C1 SHARD_ID( T1, T1.C1 )
-- ---------------------
A                      0
B                      1
C                      2

3 rows selected.


gSQL> SELECT SHARD_ID( T1, 'B' ) FROM DUAL;
SHARD_ID( T1, 'B' )
-------------------
                  1

1 row selected.
```

<a id="f6e499642c169562"></a>
## SHARD_NAME

<a id="58cde56defdb5638"></a>
### Syntax

```
SHARD_NAME( table_name, shard_key_value [, ... ] )
```

<a id="b8f7108e26a24194"></a>
### Description

It returns the NAME for the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is VARCHAR.

> It is a valid information in a cluster system.

<a id="96468d0d43eb3bd1"></a>
### Example

```
gSQL> SELECT T1.C1, SHARD_NAME( T1, T1.C1 ) FROM T1;

C1 SHARD_NAME( T1, T1.C1 )
-- -----------------------
A  S1                     
B  S2                     
C  S3                     

3 rows selected.

gSQL> SELECT SHARD_NAME( T1, 'B' ) FROM DUAL;

SHARD_NAME( T1, 'B' )
---------------------
S2                   

1 row selected.
```

<a id="b89236b194876299"></a>
## SHIFT_LEFT

<a id="44a33380aaafb3c4"></a>
### Syntax

```
SHIFT_LEFT( num, cnt )
```

<a id="d85033c5fbf8171d"></a>
### Description

It moves num to the left as many as cnt bits, and returns the movement values.

The data type of input num argument and cnt argument can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or the type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.

cnt is masked with 6 bit, and it is processed to a value in the range within 6 bit.

If either num or cnt is NULL, then NULL is returned.

The result type is NATIVE_BIGINT.

<a id="d3cbf94ed31b8e8d"></a>
### Example

```
gSQL> SELECT SHIFT_LEFT(1, 3) FROM DUAL;
SHIFT_LEFT(1, 3)
----------------
               8
1 row selected.
```

<a id="68bb5716e262d8fd"></a>
## SHIFT_RIGHT

<a id="c9205e25a936ef5b"></a>
### Syntax

```
SHIFT_RIGHT( num, cnt )
```

<a id="73fe01d1d66da7de"></a>
### Description

It moves num to the right as many as cnt bits, and returns the movement values.

The data type of input num argument and cnt argument can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or the type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.

cnt is masked with 6 bit, and it is processed to a value in the range within 6 bit.

If either num or cnt is NULL, then NULL is returned.

The result type is NATIVE_BIGINT.

<a id="12186f278242d950"></a>
### Example

```
gSQL> SELECT SHIFT_RIGHT(8, 3) FROM DUAL;
SHIFT_RIGHT(8, 3)
-----------------
                1
1 row selected.
```

<a id="bb48a985d0e68961"></a>
## SIGN

<a id="f1a024a2a0028e09"></a>
### Syntax

```
SIGN( num )
```

<a id="09d438e3b66f8239"></a>
### Description

It returns the sign of num.

The num argument can be a numeric data type.

The return value is as follows.   
• If num < 0,  -1 is returned.  
• If num = 0, 0 is returned.  
• If num > 0, 1 is returned.

If num is NULL, then NULL is returned.

<a id="773c6e9ee2aa0128"></a>
### Example

```
gSQL> SELECT SIGN(-10) AS RESULT1, 
             SIGN(0) AS RESULT2, 
             SIGN(10) AS RESULT3 FROM DUAL;
RESULT1 RESULT2 RESULT3
------- ------- -------
     -1       0       1
1 row selected.
```

<a id="571f33fdc2302926"></a>
## SIN

<a id="a0b7c881c014a8ec"></a>
### Syntax

```
SIN( num )
```

<a id="612ad4f60190424e"></a>
### Description

It returns the sine value of num.  
If num is NULL, then NULL is returned.

<a id="89e7c3dc4b6492ca"></a>
### Example

```
gSQL> SELECT SIN( 0 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="19e33cbfd722cbe1"></a>
## SPLIT_PART

<a id="48e1a4bcffe436cb"></a>
### Syntax

```
SPLIT_PART( string, delimiter, field )
```

<a id="cf1bed86ad239b6a"></a>
### Description

It returns a character string of the field by specifying a character as delimiter within a string.

The data type of string argument and delimiter argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

The field argument can be a numeric data type.

If any of string, delimiter, field is NULL, the result is also NULL.  
The value of field should be a numeric value above 1, and if it is 0 or a negative number, an error is returned.

The following table describes the result types.

**Result type of SPLIT_PART**

<a id="e3e63fc6f365d3d0"></a>
| string type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="2f282056c9f49030"></a>
### Example

```
gSQL> SELECT SPLIT_PART( 'AB;CD;EF;GH', ';', 3  ) AS RESULT FROM DUAL;
RESULT
------
EF    
1 row selected.
```

<a id="2cd22a227a5bc630"></a>
## SQRT

<a id="f5d0283d834fe7a4"></a>
### Syntax

```
SQRT( num )
```

<a id="98643b2301433713"></a>
### Description

It returns the square root of num.

The num argument can be a numeric type, and it should not be a negative number, but above 0.  
If the num argument is NULL, then NULL is returned.

<a id="453ff75460b11c8c"></a>
### Example

```
gSQL> SELECT SQRT( 9 ) AS RESULT FROM DUAL;
RESULT
------
     3
1 row selected.
```

<a id="ad803f75c2a83942"></a>
## STATEMENT_DATE

<a id="a645ca54946c228b"></a>
### Syntax

```
STATEMENT_DATE()
CURRENT_DATE [()]
```

<a id="4ae1c1530bff06eb"></a>
### Description

The current date(DATE type) value is obtained.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="693e5d5e398d8f67"></a>
### Example

```
gSQL> SELECT STATEMENT_DATE() AS result FROM t1;

RESULT    
----------
2013-12-12
2013-12-12
2013-12-12

3 rows selected.
```

<a id="040753ae51946fa2"></a>
## STATEMENT_LOCALTIME

<a id="ad3a37dc8fc845a4"></a>
### Syntax

```
STATEMENT_LOCALTIME()
LOCALTIME [()]
```

<a id="82ab822e56aada36"></a>
### Description

The current TIME WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.  
• TATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="eb1aca8626146bb0"></a>
### Example

All rows have the same time value.

```
gSQL> SELECT STATEMENT_LOCALTIME() AS result FROM t1;

RESULT         
---------------
16:18:50.775870
16:18:50.775870
16:18:50.775870

3 rows selected.
```

<a id="de1962d05099f240"></a>
## STATEMENT_LOCALTIMESTAMP

<a id="33883a4d12e2baf0"></a>
### Syntax

```
STATEMENT_LOCALTIMESTAMP()
LOCALTIMESTAMP [()]
```

<a id="bfdfa884b0802f5a"></a>
### Description

The current TIMESTAMP WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_LOCALTIMESTAMP(): All timestamp values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="f8a8d47141cf3e9e"></a>
### Example

All rows have the same value.

```
gSQL> SELECT STATEMENT_LOCALTIMESTAMP() FROM t1;

STATEMENT_LOCALTIMESTAMP()
--------------------------
2013-12-12 16:23:39.782187
2013-12-12 16:23:39.782187
2013-12-12 16:23:39.782187

3 rows selected.
```

<a id="be59f083793c4b89"></a>
## STATEMENT_TIME

<a id="b8e09a7538e29dc4"></a>
### Syntax

```
STATEMENT_TIME()
CURRENT_TIME [()]
```

<a id="479d43bfafd26e6c"></a>
### Description

The current TIME WITH TIME ZONE type value is obtained.

CURRENT_TIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• STATEMENT_TIME(): All time values in an SQL statement are same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="d5e05d18f134a955"></a>
### Example

All rows have the same time value.

```
gSQL> SELECT STATEMENT_TIME() AS result FROM t1;

RESULT                
----------------------
16:28:19.268513 +09:00
16:28:19.268513 +09:00
16:28:19.268513 +09:00

3 rows selected.
```

<a id="0389194089416bf2"></a>
## STATEMENT_TIMESTAMP

<a id="979a943f2610d3db"></a>
### Syntax

```
STATEMENT_TIMESTAMP()
CURRENT_TIMESTAMP [()]
```

<a id="c52db93fc8004020"></a>
### Description

The current TIMESTAMP WITH TIME ZONE type value is obtained.

CURRENT_TIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_TIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_TIMESTAMP(): All timestamp values in an SQL statement are same.  
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="bf0e89fd6f0fc05a"></a>
### Example

All rows have the same value.

```
gSQL> SELECT STATEMENT_TIMESTAMP() AS result FROM t1;

RESULT                           
---------------------------------
2013-12-12 16:36:11.032957 +09:00
2013-12-12 16:36:11.032957 +09:00
2013-12-12 16:36:11.032957 +09:00

3 rows selected.
```

<a id="b4ba53773c334431"></a>
## STATEMENT_VIEW_SCN

<a id="ed0a7059fd5bb897"></a>
### Syntax

```
STATEMENT_VIEW_SCN()
```

<a id="a6ce520d61048a5c"></a>
### Description

It obtains VIEW SCN of the current STATEMENT.

<a id="f4c3bf2d1cab2b10"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN() FROM dual;

STATEMENT_VIEW_SCN()
--------------------
17697.658.17880     

1 row selected.
```

<a id="e8cfbf0a37194179"></a>
## STATEMENT_VIEW_SCN_DCN

<a id="0465ff6ddab44797"></a>
### Syntax

```
STATEMENT_VIEW_SCN_DCN()
```

<a id="80f3bbf1e470fc99"></a>
### Description

It obtains the Domain Change Number (DCN) value of the current STATEMENT's VIEW SCN.

<a id="b1514c746c98a753"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_DCN() FROM dual;

STATEMENT_VIEW_SCN_DCN()
------------------------
                     658

1 row selected.
```

<a id="9bfacbe01c6b6dad"></a>
## STATEMENT_VIEW_SCN_GCN

<a id="8704b014071456f3"></a>
### Syntax

```
STATEMENT_VIEW_SCN_GCN()
```

<a id="c7f980608854f921"></a>
### Description

It obtains the Global Change Number (GCN) value of the current STATEMENT's VIEW SCN.

<a id="9923c88f14cf4b5f"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_GCN() FROM dual;

STATEMENT_VIEW_SCN_GCN()
------------------------
                   17697

1 row selected.
```

<a id="79ce175a5fdf048e"></a>
## STATEMENT_VIEW_SCN_LCN

<a id="2ea152a73718b6b3"></a>
### Syntax

```
STATEMENT_VIEW_SCN_LCN()
```

<a id="4c00722f0dd591b7"></a>
### Description

It obtains the Local Change Number (LCN) value of the current STATEMENT's VIEW SCN.

<a id="d6144d4ed543f0d4"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_LCN() FROM dual;

STATEMENT_VIEW_SCN_LCN()
------------------------
                   17880

1 row selected.
```

<a id="443de9b5cf1bfac6"></a>
## STDDEV

<a id="2d0be4b0c940437c"></a>
### Syntax

```
STDDEV( [ ALL | DISTINCT ] expr )
```

<a id="dc5379b3fa43dd15"></a>
### Description

It is an aggregation function, and it obtains the standard deviation of an expr set.

If ALL is specified, this function is performed for all values. If DISTINCT is specified, this function is performed for the values of which the duplicates were deleted from. If it is not specified, it is processed as if ALL is apecified.

If the number of expr sets except for NULL after deleting the duplicates by using DISTINCT is one, then it returns 0 like as [VARIANCE](#b796833489baa110).

The following table describes the arguments and result types.

**Argument and result type of STDDEV**

<a id="10ff1046516aed37"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

GOLDILOCKS gets the standard deviation as follows.  
　• If the number of expr sets is 1, then it returns 0.  
　• If the number of expr sets is bigger than 1, it returns the value of [STDDEV_SAMP( expr )](#d4efefa035560e9e).

> The standard deviation is a positive square root of a variance, and it is obtained calculating the square root of the variance. In other words, the STDDEV function is as same as the square root of [VARIANCE](#b796833489baa110) function.  
>   
> STDDEV( [ ALL ] expr )  
>  = SQRT( VARIANCE( [ ALL ] expr ) )  
>   
> STDDEV( DISTINCT expr )  
>  = SQRT( VARIANCE( DISTINCT expr ) )

<a id="828da4931b898b88"></a>
### Example

```
gSQL> SELECT STDDEV(c1) FROM t1;

      STDDEV(C1)
----------------
11.4978258814438

1 row selected.


gSQL> SELECT STDDEV(ALL c1) FROM t1;

  STDDEV(ALL C1)
----------------
11.4978258814438

1 row selected.


gSQL> SELECT STDDEV(DISTINCT c1) FROM t1;

STDDEV(DISTINCT C1)
-------------------
   13.2759180473518

1 row selected.
```

<a id="d0a07183b6011d0d"></a>
## STDDEV_POP

<a id="5eb26e15107aab86"></a>
### Syntax

```
STDDEV_POP( expr )
```

<a id="7407716a99862587"></a>
### Description

It is an aggregation function, and it obtains the population standard deviation of an expr set. If the number of expr sets except for NULL is one, then it returns 0.

The following table describes the arguments and result types.

**Argument and result type of STDDEV_POP**

<a id="02392383c083728b"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The population standard deviation is a positive square root of a population variance, and it is obtained by calculating the square root of the population variance. In other words, the STDDEV_POP function is as same as the square root of [VAR_POP](#1cd428a63cef1d10) function.  
>   
> STDDEV_POP( expr )  
>  = SQRT( VAR_POP( expr ) )

<a id="5d3284619f15c4cd"></a>
### Example

```
gSQL> SELECT STDDEV_POP(c1) FROM t1;

 STDDEV_POP(C1)
---------------
10.283968105746

1 row selected.
```

<a id="d4efefa035560e9e"></a>
## STDDEV_SAMP

<a id="23f4d2539738f800"></a>
### Syntax

```
STDDEV_SAMP( expr )
```

<a id="adf23ff1e3d0c81d"></a>
### Description

It is an aggregation function, and it obtains the sample standard deviation of an expr set. If the number of expr sets except for NULL is one, then it returns NULL.

The following table describes the arguments and result types.

**Argument and result type of STDDEV_SAMP**

<a id="bf9730bc67fdf52c"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The sample standard deviation is a positive square root of a sample variance, and it is obtained by calculating the square root of the sample variance. In other words, the STDDEV_SAMP function is as same as the square root of [VAR_SAMP](#4ad2679db722d599) function.  
>   
> STDDEV_SAMP( expr )  
>  = SQRT( VAR_SAMP( expr ) )

<a id="b10b32c9c71f2941"></a>
### Example

```
gSQL> SELECT STDDEV_SAMP(c1) FROM t1;

 STDDEV_SAMP(C1)
----------------
11.4978258814438

1 row selected.
```

<a id="ac450fb697471e8b"></a>
## SUBSTR

<a id="c1697c7d1916353b"></a>
### Syntax

```
SUBSTR( str FROM start_position [ FOR string_length ] )
SUBSTR( str, start_position [ , string_length ] )
```

<a id="62d4769b6278d917"></a>
### Description

It is an alias of [SUBSTRING](#bba28ac2ca8a9186).

<a id="d2444a3563b13b78"></a>
### Example

- Multi byte character set (e.g. UTF8): 1 byte character

```
gSQL> SELECT 
      SUBSTR( 'DATABASE MANAGEMENT SYSTEM', 10, 10 ) AS RESULT 
      FROM DUAL;
RESULT    
----------
MANAGEMENT
1 row selected.
```

- Multi byte character set (e.g. UTF8): 2 bytes or 3 bytes character

```
gSQL> SELECT SUBSTR( '“αβ≠ΑΒ”', 2, 5 ) AS RESULT FROM DUAL;
RESULT
------
αβ≠ΑΒ 
1 row selected.
```

<a id="148a2b0ef17b2289"></a>
## SUBSTRB

<a id="799362e84103d4d8"></a>
### Syntax

```
SUBSTRB( str, start_position [ , string_length ] )
```

<a id="9b0b9e6ab605c1d5"></a>
### Description

It extracts characters which are within string_length range from start_position, and returns the result for str.

This function is as same as [SUBSTRING](#bba28ac2ca8a9186) function, except that start_position and string_length of the SUBSTR function are calculated in byte units.

<a id="fad194036847b5c5"></a>
### Example

- Multi byte character set (e.g. UTF8): 1 byte character

```
gSQL> SELECT 
      SUBSTRB( 'DATABASE MANAGEMENT SYSTEM', 10, 10 ) AS RESULT 
      FROM DUAL;
RESULT    
----------
MANAGEMENT
1 row selected.
```

- Multi byte character set (e.g. UTF8): 2 bytes or 3 bytes character

```
gSQL> SELECT SUBSTRB( '“αβ≠ΑΒ”', 4, 11 ) AS RESULT FROM DUAL;
RESULT
------
αβ≠ΑΒ 
1 row selected.
```

<a id="bba28ac2ca8a9186"></a>
## SUBSTRING

<a id="6aee1026878eaaaa"></a>
### Syntax

```
SUBSTRING( str FROM start_position [ FOR string_length ] )  
SUBSTRING( str, start_position [ , string_length ] )
```

<a id="26e4ab0671617813"></a>
### Description

It extracts characters which are within string_length range from start_position, and returns the result for str.

The str argument data type can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary data type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

The start_position argument and string_length argument can be a numeric data type.

If any of str, start_position, string_length is NULL, the result is NULL.   
The start_position and string_length start from 1, and they are calculated in character unit according to character set (not in byte unit).

If start_position is 0, the start_position is assigned to 1.   
If start_position is a positive number, it searches for the position forwards (towards right) from the beginning of str.   
If start_ position is a negative number, it searches for the position backwards (towards left) from the end of str.   
If string_length is omitted, characters from the start_position to the last character of str, are returned.

If string_length is 0 or a negative number, the result is NULL.  
If start_position > (str length), the result is NULL.  
If (str length + start_position) < 0, the result is NULL.

It is an alias of [SUBSTR](#ac450fb697471e8b).  
For more information, refer to [SUBSTRB](#148a2b0ef17b2289).

The following table describes the result types.

**Result type of SUBSTRING**

<a id="5c1b040cf097dbfa"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="c94031f16ad0f15e"></a>
### Example

- Multi byte character set (e.g. UTF8): 1 byte character

```
gSQL> SELECT 
      SUBSTRING( 'DATABASE MANAGEMENT SYSTEM' FROM 10 FOR 10 ) AS RESULT 
      FROM DUAL;
RESULT    
----------
MANAGEMENT
1 row selected.
```

- Multi byte character set (e.g. UTF8): 2 bytes or 3 bytes character

```
gSQL> SELECT SUBSTRING( '“αβ≠ΑΒ”' FROM 2 FOR 5 ) AS RESULT FROM DUAL;
RESULT
------
αβ≠ΑΒ 
1 row selected.
```

<a id="b57f7f016eb74f73"></a>
## SUM

<a id="4998fccb70ca02cb"></a>
### Syntax

```
SUM( [ ALL | DISTINCT ] expr )
```

<a id="3d28703d213cb43a"></a>
### Description

It is an aggregate function and the sum of expr value is obtained.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

<a id="6560bfcf164f9033"></a>
### Example

```
gSQL> SELECT SUM(c1) FROM t1;

SUM(C1)
-------
      6

1 row selected.
```

<a id="82bd7f8aca000c92"></a>
## SYSDATE

<a id="9661b44c6992f00f"></a>
### Syntax

```
SYSDATE
```

<a id="178892fb5df394c4"></a>
### Description

It obtains the current DATE type value based on the OS time of the database server.

<a id="c255133ee67767eb"></a>
### Example

```
gSQL> SELECT SYSDATE FROM t1;

SYSDATE   
----------
2013-12-12
2013-12-12
2013-12-12

3 rows selected.
```

<a id="37b17b7f3a7e7eee"></a>
## SYS_EXTRACT_UTC

<a id="b74bc3a0cc7890a2"></a>
### Syntax

```
SYS_EXTRACT_UTC( datetime_with_timezone )
```

<a id="efb56aa2cc7e1555"></a>
### Description

It returns the UTC (Coordinated Universal Time—formerly Greenwich Mean Time) value.  
If the timezone is not specified, it is calculated as session time zone.

The data type of an input argument can be time, time with time zone, timestamp, timestamp with time zone.  
The result type is time or timestamp type.

<a id="2acee2687c88ba2e"></a>
### Example

```
gSQL> SELECT
      SYS_EXTRACT_UTC( 
          TO_TIMESTAMP_TZ( '2017-05-25 00:00:00.000000 +09:00',
                           'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM' ) 
          ) AS RESULT
      FROM DUAL; 
RESULT                    
--------------------------
2017-05-24 15:00:00.000000
1 row selected.
```

<a id="75644a4c2bc0787c"></a>
## SYSTIME

<a id="52c13564d4efa3cf"></a>
### Syntax

```
SYSTIME
```

<a id="0df609c2aa13cfc5"></a>
### Description

It obtains the current TIME WITH TIME ZONE type value based on the OS time of the database server.

<a id="6914fd989969412d"></a>
### Example

```
gSQL> SELECT SYSTIME FROM t1;

SYSTIME               
----------------------
16:30:46.954941 +09:00
16:30:46.954941 +09:00
16:30:46.954941 +09:00

3 rows selected.
```

<a id="9ab4675a7c095e1f"></a>
## SYSTIMESTAMP

<a id="3f5a93817d2924d1"></a>
### Syntax

```
SYSTIMESTAMP
```

<a id="ce9516153d2e049d"></a>
### Description

It obtains the current TIMESTAMP WITH TIME ZONE type value based on the OS time of the database server.

<a id="0c783d13ae8714fd"></a>
### Example

```
gSQL> SELECT SYSTIMESTAMP FROM t1;

SYSTIMESTAMP                     
---------------------------------
2013-12-12 16:37:34.432241 +09:00
2013-12-12 16:37:34.432241 +09:00
2013-12-12 16:37:34.432241 +09:00

3 rows selected.
```

<a id="832c8a228cfc8071"></a>
## TAN

<a id="89475e80a35a00fc"></a>
### Syntax

```
TAN( num )
```

<a id="447fef9cb57d3801"></a>
### Description

It returns the tangent value of num in radians unit.  
If num is NULL, then NULL is returned.

<a id="9a95d2e06e3e2ce6"></a>
### Example

```
gSQL> SELECT TAN( 1 ) AS RESULT FROM DUAL;
         RESULT
---------------
1.5574077246549
1 row selected.
```

<a id="8f90bf4109b26d9a"></a>
## TO_BASE64

<a id="9f5ddf4a8f691b24"></a>
### Syntax

```
TO_BASE64( str )
```

<a id="e3f8ed7d4baffbd6"></a>
### Description

It converts str by using base64 encoding, and returns the converted character.  
str argument can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, a type which can be converted to a character type, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.  
The result type is a character such as CHARACTER VARYING or CHARACTER LONG VARYING.

If str is NULL, the result value is also NULL.

Base64 encoding represents 8 bit binary data in 64 characters consisting of ascii areas.  
64 characters consist of  A~Z, a~z, 0~9, +, /.

6 bit is represented as a character, and three characters (24 bits) are represented with 4 characters as a unit.  
If the encoded characters can not fill 4 characters, then others are filled with '='.  
If encoded characters are over 76, then a newline is added and they are divided into multiple lines.

Use FROM_BASE64() function to decode the base64 encoded character.  
The newline, carriage return, tab, space are ignored when decoding base64.

For more information, refer to [FROM_BASE64](#13811824d98292f5).

<a id="bec0531eeb33a749"></a>
### Example

```
gSQL> SELECT TO_BASE64( 'abc' ), TO_BASE64( 'abcd' ) FROM DUAL;

TO_BASE64( 'abc' ) TO_BASE64( 'abcd' )
------------------ -------------------
YWJj               YWJjZA==           
1 row selected.
```

<a id="1fa54d9bf1e47d8e"></a>
## TO_CHAR( datetime )

<a id="fb18f517c77c7d89"></a>
### Syntax

```
TO_CHAR( datetime [, fmt ] )
```

<a id="3371ae8af8310aec"></a>
### Description

It converts datetime to a string in the specified fmt format, and returns the result.

The datetime argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL.   
The fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING.  

If any argument is NULL, then NULL is returned.

If fmt is omitted, it follows the default format.  
• DATE: Refer to [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#60cec08fdb546878).  
• TIMESTAMP: Refer to [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#c7bd2aeb63024fb5).  
• TIMESTAMP WITH TIME ZONE: Refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#3de636e485510342).  
• TIME: Refer to [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#d04abb17d05e3a69).  
• TIME WITH TIME ZONE: Refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#74c3e90b61fe6686).

If the data type of the datetime argument is INTERVAL, it is converted to a string then returned regardless of fmt.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#92dc2a9a1c8773fb).

The result type is CHARACTER VARYING.

<a id="fcfcfcd3c20e0ddc"></a>
### Example

The following is an example of when fmt is omitted, and NLS_DATE_FORMAT = 'YYYY-MM-DD'.

```
gSQL> SELECT 
      TO_CHAR( TO_DATE( '2012-03-15','YYYY-MM-DD' ) ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2012-03-15
1 row selected.
```

The following is an example of when fmt is specified.

```
gSQL> SELECT 
      TO_CHAR( TO_DATE('2012-03-15','YYYY-MM-DD'), 'DD-MON-YY' ) AS RESULT
      FROM DUAL;
RESULT   
---------
15-MAR-12
1 row selected.
```

<a id="9240e7d5f6e36827"></a>
## TO_CHAR( number )

<a id="ebba64790cc49470"></a>
### Syntax

```
TO_CHAR( number [, fmt ] )
```

<a id="34e32fbb722b0d67"></a>
### Description

It converts the number to a string in the specified fmt format, and returns the result.

The number argument can be a numeric data type.  
The fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING.  
If fmt is omitted, all significant digits are converted to the string and returned.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#b66411f6c9926d66).  
If any input argument is NULL, then NULL is returned.

The result type is CHARACTER VARYING.

<a id="988bca25167bd1f3"></a>
### Example

```
gSQL> SELECT TO_CHAR( 12500000 ) AS RESULT FROM DUAL;
RESULT  
--------
12500000
1 row selected.

gSQL> SELECT TO_CHAR( 12500000, 'S999,999,999' ) AS RESULT FROM DUAL;
RESULT      
------------
 +12,500,000
1 row selected.
```

<a id="c767d502ec2b1a44"></a>
## TO_DATE

<a id="1398d9da2e9315e8"></a>
### Syntax

```
TO_DATE( str [, fmt ] )
```

<a id="82506e22ae15a1ba"></a>
### Description

It converts the str string in the specified fmt format to DATE type, and returns the result.

The str argument and fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.  
If fmt is omitted, the default format is NLS_DATE_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#92dc2a9a1c8773fb).  
For more information, refer to [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#60cec08fdb546878).  

If either str or fmt is NULL, then NULL is returned.

The result type is DATE.

<a id="b01b9afba831ca40"></a>
### Example

The following is an example of when fmt is omitted, and NLS_DATE_FORMAT = 'YYYY-MM-DD'.

```
gSQL> SELECT TO_DATE( '2009-07-29' ) AS RESULT FROM DUAL;
RESULT    
----------
2009-07-29
1 row selected.
```

The following is an example of when fmt is specified.

```
gSQL> SELECT TO_DATE( '29-JUL-09', 'DD-MON-YY' ) AS RESULT FROM DUAL;
RESULT    
----------
2009-07-29
1 row selected.
```

<a id="4ca029a562131b56"></a>
## TO_NATIVE_BIGINT

<a id="14536223a5903fb0"></a>
### Syntax

```
TO_NATIVE_BIGINT( str [, fmt ] )
```

<a id="61642643d6ae1eae"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_BIGINT type, and returns the result.

The str argument and fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.    
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#b66411f6c9926d66).

The result type is NATIVE_BIGINT.

<a id="d28671d54f51cadc"></a>
### Example

```
gSQL> SELECT TO_NATIVE_BIGINT( '123.45' ) AS RESULT1,
             TO_NATIVE_BIGINT( '+123.45', 'S999.99' ) AS RESULT2
        FROM DUAL;
RESULT1 RESULT2
------- -------
    123     123
1 row selected.
```

<a id="e9f06f5b75026f18"></a>
## TO_NATIVE_DOUBLE

<a id="8374dd0c9da94313"></a>
### Syntax

```
TO_NATIVE_DOUBLE( str [, fmt ] )
```

<a id="c6eb50b6bf966557"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_DOUBLE type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#b66411f6c9926d66).

The result type is NATIVE_DOUBLE.

<a id="2f19d69764f3f675"></a>
### Example

```
gSQL> SELECT TO_NATIVE_DOUBLE( '123.45' ) AS RESULT1, 
             TO_NATIVE_DOUBLE( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
1 row selected.
```

<a id="8c40f9722a4badbe"></a>
## TO_NATIVE_INTEGER

<a id="d8789b44fac556b9"></a>
### Syntax

```
TO_NATIVE_INTEGER( str [, fmt ] )
```

<a id="5f60ec36f0df8e0d"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_INTEGER type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#b66411f6c9926d66).

The result type is NATIVE_INTEGER.

<a id="fb83793400abf411"></a>
### Example

```
gSQL> SELECT TO_NATIVE_INTEGER( '123.45' ) AS RESULT1,
             TO_NATIVE_INTEGER( '+123.45', 'S999.99' ) AS RESULT2
        FROM DUAL;
RESULT1 RESULT2
------- -------
    123     123
1 row selected.
```

<a id="213295da6c934e7e"></a>
## TO_NATIVE_REAL

<a id="a8f2de513bd4c896"></a>
### Syntax

```
TO_NATIVE_REAL( str [, fmt ] )
```

<a id="5c79a57ad91c1eb1"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_REAL type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#b66411f6c9926d66).

The result type is NATIVE_REAL.

<a id="6fbc43eb183a38c8"></a>
### Example

```
gSQL> SELECT TO_NATIVE_REAL( '123.45' ) AS RESULT1, 
             TO_NATIVE_REAL( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
```

<a id="c3d517a3792a9ee9"></a>
## TO_NATIVE_SMALLINT

<a id="8c3033f9583cd139"></a>
### Syntax

```
TO_NATIVE_SMALLINT( str [, fmt ] )
```

<a id="fe2e088ede7ec03c"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_SMALLINT type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#b66411f6c9926d66).

The result type is NATIVE_SMALLINT.

<a id="bdabea36876cd7fc"></a>
### Example

```
gSQL> SELECT TO_NATIVE_SMALLINT( '123.45' ) AS RESULT1,
             TO_NATIVE_SMALLINT( '+123.45', 'S999.99' ) AS RESULT2
        FROM DUAL;
RESULT1 RESULT2
------- -------
    123     123
1 row selected.
```

<a id="3026dda988e50e6c"></a>
## TO_NUMBER

<a id="8fb3c44ff686a221"></a>
### Syntax

```
TO_NUMBER( str [, fmt] )
```

<a id="925e1fd541da11e3"></a>
### Description

It converts the str string in the specified fmt format to NUMBER type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#b66411f6c9926d66).

The result type is NUMBER.

<a id="d5f684a81c6965b4"></a>
### Example

```
gSQL> SELECT TO_NUMBER( '123.45' ) AS RESULT1, 
             TO_NUMBER( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
1 row selected.
```

<a id="80925e24c2cccff0"></a>
## TO_TIME

<a id="f62230da3ca3bfc5"></a>
### Syntax

```
TO_TIME( str [, fmt ] )
```

<a id="08e8d47509450a14"></a>
### Description

It converts the str string in the specified fmt format to TIME type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIME_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#92dc2a9a1c8773fb).  
For more information, refer to [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#d04abb17d05e3a69).  

If either str or fmt is NULL, then NULL is returned.

The result type is TIME.

<a id="85ebc84d5b906d8f"></a>
### Example

The following is an example of when fmt is omitted, and NLS_TIME_FORMAT = 'HH24:MI:SS.FF6'.

```
gSQL> SELECT TO_TIME( '11:22:33.999999' ) AS RESULT FROM DUAL;
RESULT         
---------------
11:22:33.999999
1 row selected.
```

The following is an example of when fmt is specified.

```
gSQL> SELECT 
      TO_TIME( '112233.999999/P.M.', 'HH12MISS.FF6/P.M.' ) AS RESULT 
      FROM DUAL;
RESULT         
---------------
23:22:33.999999
1 row selected.
```

<a id="7990ec599087099b"></a>
## TO_TIME_TZ

<a id="09dc6f98cf4dbece"></a>
### Syntax

```
TO_TIME_TZ( str [, fmt ] )
```

<a id="901cf9aed347d0b5"></a>
### Description

It is an alias of [TO_TIME_WITH_TIME_ZONE](#741406e9fe9e8378).  
For more information, refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#74c3e90b61fe6686).

<a id="de30fc8a653ad13d"></a>
### Example

The following is an example of when fmt is omitted, and NLS_TIME_WITH_TIME_ZONE_FORMAT = 'HH24:MI:SS.FF6 TZH:TZM'.

```
gSQL> SELECT TO_TIME_TZ( '11:22:33.999999 +09:00' ) AS RESULT FROM DUAL;
RESULT                
----------------------
11:22:33.999999 +09:00
1 row selected.
```

The following is an example of when fmt is specified.

```
gSQL> SELECT TO_TIME_TZ( '11:22:33.999999 +09:00 PM', 
                         'HH12:MI:SS.FF6 TZH:TZM PM' ) AS RESULT 
      FROM DUAL;
RESULT                
----------------------
23:22:33.999999 +09:00
1 row selected.
```

<a id="741406e9fe9e8378"></a>
## TO_TIME_WITH_TIME_ZONE

<a id="4e5a5d446ffd0121"></a>
### Syntax

```
TO_TIME_WITH_TIME_ZONE( str [, fmt ] )
TO_TIME_TZ( str [, fmt ] )
```

<a id="548498be8d0ed30e"></a>
### Description

It converts the str string in the specified fmt format to TIME WITH TIME ZONE type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIME_WITH_TIME_ZONE_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#92dc2a9a1c8773fb)  
For more information, refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#74c3e90b61fe6686).  

If either str or fmt is NULL, then NULL is returned.

It is an alias of [TO_TIME_TZ](#7990ec599087099b).

The result type is TIME WITH TIME ZONE.

<a id="7f537af49f8933ed"></a>
### Example

The following is an example of when fmt is omitted, and NLS_TIME_WITH_TIME_ZONE_FORMAT = 'HH24:MI:SS.FF6 TZH:TZM'.

```
gSQL> SELECT 
      TO_TIME_WITH_TIME_ZONE( '11:22:33.999999 +09:00' ) AS RESULT 
      FROM DUAL;
RESULT                
----------------------
11:22:33.999999 +09:00
1 row selected.
```

The following is an example of when fmt is specified.

```
gSQL> SELECT 
      TO_TIME_WITH_TIME_ZONE( '11:22:33.999999 +09:00 PM', 
                              'HH12:MI:SS.FF6 TZH:TZM PM' ) 
      AS RESULT 
      FROM DUAL;
RESULT                
----------------------
23:22:33.999999 +09:00
1 row selected.
```

<a id="bc899076d23d916d"></a>
## TO_TIMESTAMP

<a id="25c686ab9fc8d742"></a>
### Syntax

```
TO_TIMESTAMP( str [, fmt ] )
```

<a id="04008fc97cad20f5"></a>
### Description

It converts the str string in the specified fmt format to TIMESTAMP type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIMESTAMP_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#92dc2a9a1c8773fb).  
For more information, refer to [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#c7bd2aeb63024fb5).  

If either str or fmt is NULL, then NULL is returned.

The result type is TIMESTAMP.

<a id="aa7dda0bd154f806"></a>
### Example

The following is an example of when fmt is omitted, and NLS_TIMESTAMP_FORMAT = 'YYYY-MM-DD HH24:MI:SS.FF6'.

```
gSQL> SELECT 
      TO_TIMESTAMP( '2009-07-29 11:22:33.999999' ) AS RESULT 
      FROM DUAL;
RESULT                    
--------------------------
2009-07-29 11:22:33.999999
1 row selected.
```

The following is an example of when fmt is specified.

```
gSQL> SELECT 
      TO_TIMESTAMP( '090729 112233999999 PM', 'YYMMDD HH12MISSFF6 PM' ) 
      AS RESULT 
      FROM DUAL;

RESULT                    
--------------------------
2009-07-29 23:22:33.999999
1 row selected.
```

<a id="d680d2b496e9d7f2"></a>
## TO_TIMESTAMP_TZ

<a id="4b4f03123e668f49"></a>
### Syntax

```
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="d399dc6d12f70dc5"></a>
### Description

It is an alias of [TO_TIMESTAMP_WITH_TIME_ZONE](#21d04d587ce7501d).  
For more information, refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#3de636e485510342).

<a id="2f595ddf2469d883"></a>
### Example

The following is an example of when fmt is omitted, and NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT = 'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM'.

```
gSQL> SELECT 
      TO_TIMESTAMP_TZ( '2009-07-29 11:22:33.999999 +09:00' ) AS RESULT 
      FROM DUAL;
RESULT                           
---------------------------------
2009-07-29 11:22:33.999999 +09:00
1 row selected.
```

The following is an example of when fmt is specified.

```
gSQL> SELECT 
      TO_TIMESTAMP_TZ( '29-JUL-09 11:22:33.999999 +09:00',
                       'DD-MON-RR HH12:MI:SS.FF6 TZH:TZM' ) AS RESULT 
      FROM DUAL;
RESULT                           
---------------------------------
2009-07-29 11:22:33.999999 +09:00
1 row selected.
```

<a id="21d04d587ce7501d"></a>
## TO_TIMESTAMP_WITH_TIME_ZONE

<a id="3597a9f248b90501"></a>
### Syntax

```
TO_TIMESTAMP_WITH_TIME_ZONE( str [, fmt ] )
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="04fe724a02d50660"></a>
### Description

It converts the str string in the specified fmt format to TIMESTAMP WITH TIME ZONE type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to  [Datetime Format String](11-sql-elements.md#92dc2a9a1c8773fb).  
For more information, refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#3de636e485510342).  

If either str or fmt is NULL, then NULL is returned.

It is an alias of [TO_TIMESTAMP_TZ](#d680d2b496e9d7f2).

The result type is TIMESTAMP WITH TIME ZONE .

<a id="e2f8ed2c2b089b03"></a>
### Example

The following is an example of when fmt is omitted, and NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT = 'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM'.

```
gSQL> SELECT 
      TO_TIMESTAMP_WITH_TIME_ZONE( '2009-07-29 11:22:33.999999 +09:00' ) 
      AS RESULT 
      FROM DUAL;
RESULT                           
---------------------------------
2009-07-29 11:22:33.999999 +09:00
1 row selected.
```

The following is an example of when fmt is specified.

```
gSQL> SELECT 
      TO_TIMESTAMP_WITH_TIME_ZONE( '29-JUL-09 11:22:33.999999 +09:00',
                                   'DD-MON-RR HH12:MI:SS.FF6 TZH:TZM' ) 
      AS RESULT 
      FROM DUAL;
RESULT                           
---------------------------------
2009-07-29 11:22:33.999999 +09:00
1 row selected.
```

<a id="fcf2124b87e59aa7"></a>
## TRANSACTION_DATE

<a id="cf1e620341fa6d17"></a>
### Syntax

```
TRANSACTION_DATE()
```

<a id="530fe4a74b4bf099"></a>
### Description

It obtains the current date (DATE type) value based on the session time.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="9cc910e22ab09771"></a>
### Example

All date values are always same within a single transaction.

```
gSQL> SELECT TRANSACTION_DATE() FROM dual;

TRANSACTION_DATE()
------------------
2013-12-12        

1 row selected.

gSQL> SELECT TRANSACTION_DATE() FROM dual;

TRANSACTION_DATE()
------------------
2013-12-12        

1 row selected.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT TRANSACTION_DATE() FROM dual;

TRANSACTION_DATE()
------------------
2013-12-13        

1 row selected.
```

<a id="568377cb1cb2af01"></a>
## TRANSACTION_LOCALTIME

<a id="b1e30ba80d590d91"></a>
### Syntax

```
TRANSACTION_LOCALTIME()
```

<a id="4bec0617b34db1df"></a>
### Description

It obtains the current TIME WITHOUT TIME ZONE type value based on the session time.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.   
• STATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="19d34ee56c14b223"></a>
### Example

All time values are always same within a single transaction.

```
gSQL> SELECT TRANSACTION_LOCALTIME() FROM dual;

TRANSACTION_LOCALTIME()
-----------------------
16:43:24.391834        

1 row selected.

gSQL> SELECT TRANSACTION_LOCALTIME() FROM dual;

TRANSACTION_LOCALTIME()
-----------------------
16:43:24.391834        

1 row selected.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT TRANSACTION_LOCALTIME() FROM dual;

TRANSACTION_LOCALTIME()
-----------------------
16:43:32.651833        

1 row selected.
```

<a id="d38c04c0d4676769"></a>
## TRANSACTION_LOCALTIMESTAMP

<a id="f807b89995b07b96"></a>
### Syntax

```
TRANSACTION_LOCALTIMESTAMP()
```

<a id="724dd30f67be6bb5"></a>
### Description

It obtains the current TIMESTAMP WITHOUT TIME ZONE type value based on the session time.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_LOCALTIMESTAMP(): All timestamp values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="b8ff16415ce51056"></a>
### Example

All timestamp values are always same within a single transaction.

```
gSQL> SELECT TRANSACTION_LOCALTIMESTAMP() FROM dual;

TRANSACTION_LOCALTIMESTAMP()
----------------------------
2013-12-12 16:43:32.651833  

1 row selected.

gSQL> SELECT TRANSACTION_LOCALTIMESTAMP() FROM dual;

TRANSACTION_LOCALTIMESTAMP()
----------------------------
2013-12-12 16:43:32.651833  

1 row selected.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT TRANSACTION_LOCALTIMESTAMP() FROM dual;

TRANSACTION_LOCALTIMESTAMP()
----------------------------
2013-12-12 16:46:07.831834  

1 row selected.
```

<a id="1425318fcedcbc2a"></a>
## TRANSACTION_TIME

<a id="db8e08cb8c4243a4"></a>
### Syntax

```
TRANSACTION_TIME()
```

<a id="2927619cd3f2a13a"></a>
### Description

It obtains the current TIME WITH TIME ZONE type value based on the session time.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• STATEMENT_TIME(): All time values in an SQL statement are same.   
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="6c5186ae1cc0273a"></a>
### Example

All time values are always same within a single transaction.

```
gSQL> SELECT TRANSACTION_TIME() FROM dual;

TRANSACTION_TIME()    
----------------------
16:46:07.831834 +09:00

1 row selected.

gSQL> SELECT TRANSACTION_TIME() FROM dual;

TRANSACTION_TIME()    
----------------------
16:46:07.831834 +09:00

1 row selected.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT TRANSACTION_TIME() FROM dual;

TRANSACTION_TIME()    
----------------------
16:48:00.691827 +09:00

1 row selected.
```

<a id="be9ce26baafe2ee5"></a>
## TRANSACTION_TIMESTAMP

<a id="b2114ffbdd9e6ab5"></a>
### Syntax

```
TRANSACTION_TIMESTAMP()
```

<a id="5da4b17a66652522"></a>
### Description

It obtains the current TIMESTAMP WITH TIME ZONE type value based on the session time.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_TIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_TIMESTAMP(): All timestamp values in an SQL statement are same.   
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="9e83351d84346933"></a>
### Example

All timestamp values are always same within a single transaction.

```
gSQL> SELECT TRANSACTION_TIMESTAMP() FROM dual;

TRANSACTION_TIMESTAMP()          
---------------------------------
2013-12-12 16:48:00.691827 +09:00

1 row selected.

gSQL> SELECT TRANSACTION_TIMESTAMP() FROM dual;

TRANSACTION_TIMESTAMP()          
---------------------------------
2013-12-12 16:48:00.691827 +09:00

1 row selected.

gSQL> COMMIT;

Commit complete.

gSQL>  SELECT TRANSACTION_TIMESTAMP() FROM dual;

TRANSACTION_TIMESTAMP()          
---------------------------------
2013-12-12 16:49:26.291827 +09:00

1 row selected.
```

<a id="69ed3018814a747e"></a>
## TRANSLATE

<a id="fbe8c1b6ae764c19"></a>
### Syntax

```
TRANSLATE( string, from, to )
```

<a id="cb65ab5a5c0d3075"></a>
### Description

It replaces characters. It replaces characters of string which corresponds to the the character of *from* with the character of *to* at the same position as the character of *from*.

The data type of the string argument, the from argument, and the to argument can be a data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of *string, from, to* is NULL, the result is also NULL.

- When the character of string which are as same as those of *from* exists,
    - If the length of *from* is as same as that of *to*, then it is replaced with the character of *to* at the same position as the character of *from*.
    - If the length of *from* is longer than that of *to*, then characters of *from* at the position after that of *to* length are deleted from the string.
    - If the character of *from* is duplicate, then it is replaced with the character of *to* at the same position as the first duplicate character of *from*.
- When the character of string which is as same as those of *from* does not exist, then the string is not replaced.

The following table describes the result types.

**Result type of TRANSLATE**

<a id="554374b834c2093f"></a>
| string type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="784d540ffc0b38dc"></a>
### Example

- When the character of string which are as same as those of *from* exists, then it is replaced with the character of *to* at the same position as the character of *from*.
    - A → Z, C → Y, E → X, G → W

```
gSQL> SELECT TRANSLATE('ABCDEFG', 'ACEG', 'ZYXW') AS RESULT
FROM DUAL;
RESULT 
-------
ZBYDXFW
1 row selected.
```

- If the length of *from* string is longer than that of *to* string, then characters of *from* at the position after that of *to* string length are deleted *from* the string, and replaced.
    - A → Z, C → Y, deleting E, deleting G

```
gSQL> SELECT TRANSLATE('ABCDEFG', 'ACEG', 'ZY') AS RESULT
      FROM DUAL;
RESULT
------
ZBYDF 
1 row selected.
```

<a id="8388736443de9f33"></a>
## TRIM

<a id="2dd38350e02a0f95"></a>
### Syntax

```
TRIM([ [ LEADING | TRAILING | BOTH ]  [trim_character] FROM ] trim_source)
```

<a id="2f45472c7fd97b0f"></a>
### Description

It removes the matching characters by comparing trim_character in trim_source from the LEADING, TRAILING, BOTH direction until the matching character does not exist. Then it returns the result.

The trim_character argument and trim_source argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING or a binary character data type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If any of trim_character, trim_source is NULL, the result is NULL.

- [ LEADING | TRAILING | BOTH ]
    - LEADING: Removes trim_character from the beginning of trim_source.
    - TRAILING: Removes trim_character from the back of trim_source.
    - BOTH: Removes trim_character from the both direction (the beginning, the back) of trim_source.
- trim_character should be a single character.
- If trim_character is omitted, single blank space (' ') is specified by default.
- When FROM is specified
    - [ LEADING | TRAILING | BOTH ], trim_character or [ LEADING | TRAILING | BOTH ] trim_character should be specified.
        - e.g. TRIM( LEADING FROM ' abc' ) , TRIM( 'x' FROM 'xabc' ) , TRIM( LEADING 'x' FROM 'xabc' )
    - If [ LEADING | TRAILING | BOTH ] is omitted, BOTH is specified by default.
- When FROM is omitted.
    - It is TRIM( trim_source ), it is executed in the same way as TRIM( BOTH ' ' FROM trim_source ).

The following table describes the result types.

**Result type of TRIM**

<a id="c6f1814808d1a91a"></a>
| trim_character, trim_source type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="20930a8c2c52696e"></a>
### Example

```
gSQL> SELECT TRIM( LEADING '_' FROM '___TRIM FUNCTION___' ) AS RESULT 
      FROM DUAL;
RESULT          
----------------
TRIM FUNCTION___
1 row selected.

gSQL> SELECT TRIM( TRAILING '_' FROM '___TRIM FUNCTION___' ) AS RESULT 
      FROM DUAL;
RESULT          
----------------
___TRIM FUNCTION
1 row selected.

gSQL> SELECT TRIM( BOTH '_' FROM '___TRIM FUNCTION___' ) AS RESULT 
      FROM DUAL;
RESULT       
-------------
TRIM FUNCTION
1 row selected.
```

<a id="9992000b3129b322"></a>
## TRUNC( number )

<a id="d6e2dea825046cf1"></a>
### Syntax

```
TRUNC( num [ , scale ] )
```

<a id="9a9558addd748766"></a>
### Description

It truncates the num based on scale, then returns the result.

The num argument and scale argument can be a numeric type.  
If either the num argument or the scale argument is NULL, then NULL is returned.

If scale is omitted, the scale becomes 0, and it is executed as same as TRUNC( num, 0 ).  
If scale is a positive number, it is truncated based on the number of right digit of the decimal point.  
If scale is a negative number, it is truncated off based on the number of left digit of the decimal point.

<a id="f0d921b132f9e233"></a>
### Example

```
gSQL> SELECT TRUNC( 142.4282, 2 ) AS RESULT FROM DUAL;
RESULT
------
142.42
1 row selected.

gSQL> SELECT TRUNC( 142.4282, -2 ) AS RESULT FROM DUAL;
RESULT
------
   100
1 row selected.
```

<a id="2034840ea0034910"></a>
## TRUNC( date )

<a id="a5883874797a4ff7"></a>
### Syntax

```
TRUNC( date [ , fmt ] )
```

<a id="b64a0936836745f9"></a>
### Description

It truncates the date in a specified fmt unit, and returns the result.

The date argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.  
The fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING.  
If either date argument or fmt argument is NULL, then NULL is returned.

The result type is always DATE regardless of the input date type.

If fmt is omitted, the default is *DAY*, and the available format string is described in the following table.

**Available format string in fmt**

<a id="da88fa356ade7d5f"></a>
| Format string | Description |
| --- | --- |
| CC, SCC | Century |
| YYYY, YEAR, SYYYY, SYEAR, YYY, YY, Y | Year |
| IYYY, IYY, IY, I | The year embracing the calendar week defined by ISO 8601 standards |
| Q | Quarter |
| MONTH, MON, MM, RM | Month |
| WW | The week whose first week starts from January 1st of the year |
| IW | The week containing the first thursday of the year designated as the calendar week by ISO 8601 standards ( 1 ~ 52 weeks or 1 ~ 53 weeks) becomes the first week. |
| W | The week whose first week starts from the first day of the month |
| DDD, DD, J | Day |
| DAY, DY, D | Day of the week |
| HH, HH12, HH24 | Hour |
| MI | Minute |

<a id="21fb672a132ccff0"></a>
### Example

```
gSQL> SELECT 
      TRUNC( TO_DATE( '2051-07-16', 'YYYY-MM-DD' ), 'CC' ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2001-01-01
1 row selected.

gSQL> SELECT 
      TRUNC( TO_DATE( '2051-07-16', 'YYYY-MM-DD' ), 'YYYY' ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2051-01-01
1 row selected.

gSQL> SELECT 
      TRUNC( TO_DATE( '2051-07-16', 'YYYY-MM-DD' ), 'MONTH' ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2051-07-01
1 row selected.

gSQL> SELECT 
      TRUNC( TO_TIMESTAMP( '2001-05-05 11:22:33.999999',         
             'YYYY-MM-DD HH24:MI:SS.FF6' ) ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2001-05-05
1 row selected.
```

<a id="0d9ab70eec712c13"></a>
## UPPER

<a id="17f005d2b436ded3"></a>
### Syntax

```
UPPER( str )
```

<a id="cc3c18bfecdf070f"></a>
### Description

It returns the uppercase characters of str.

The str argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.  
If str is NULL, the result is NULL.

The return type is as same as the str argument type.

<a id="191cc00acd02b1bd"></a>
### Example

```
gSQL> SELECT UPPER( 'spring' ) AS RESULT FROM DUAL;
RESULT
------
SPRING
1 row selected.
```

<a id="dd027ce981dca375"></a>
## UNHEX

<a id="d614b3ad43ded589"></a>
### Syntax

```
UNHEX( str )
```

<a id="159cf9c8472d6de1"></a>
### Description

str argument is a hexadecimal character and this function represents it as each byte and returns it as a binary string.

The input argument can be a character type such as CHARACTER VARYING, CHARACTER LONG VARYING. The result type is a binary character type such as BINARY VARYING or BINARY LONG VARYING.

If str is NULL, then the result value is also NULL.  
If str includes a character which does not belong to the hexadecimal range, then it returns an error.

For more information, refer to [HEX](#7db25d1e4b8e4867).

<a id="f1cf254c00f078eb"></a>
### Example

```
gSQL> SELECT UNHEX( HEX( 'abc' ) ) FROM DUAL;
UNHEX( HEX( 'abc' ) )
---------------------
616263               
1 row selected.
```

<a id="5fb437d4f3c0163c"></a>
## UNHEX_TO_CHARSTR

<a id="a2b05a0f84c5ca0e"></a>
### Syntax

```
UNHEX_TO_CHARSTR( str )
```

<a id="7a8780453b93a880"></a>
### Description

str argument is a hexadecimal character and this function represents it as each byte and returns it as a character string.

The input argument can be a character type such as CHARACTER VARYING, CHARACTER LONG VARYING. The result type is a character type such as CHARACTER VARYING, CHARACTER LONG VARYING.

If str is NULL, then the result value is also NULL.  
If str includes a character which does not belong to the hexadecimal range, then it returns an error.

When returning it as a character string, it applies the currently applicable character set and returns the result value because the str argument is a hexadecimal character of an unknown data.  
If it is not included in the currently applicable character set, then it returns an error.

For more information, refer to [HEX](#7db25d1e4b8e4867), [UNHEX](#dd027ce981dca375).

<a id="1e0a0aa60ebf5f13"></a>
### Example

```
gSQL> SELECT UNHEX_TO_CHARSTR( '616263' ) FROM DUAL;
UNHEX_TO_CHARSTR( '616263' )
----------------------------
abc                         
1 row selected.

gSQL> SELECT UNHEX_TO_CHARSTR( HEX( 'abc' ) ) FROM DUAL;
UNHEX_TO_CHARSTR( HEX( 'abc' ) )
--------------------------------
abc                             
1 row selected.
```

<a id="fd5c887bc855eed3"></a>
## USER_ID

<a id="1cfddc251402bd5d"></a>
### Syntax

```
USER_ID ()
```

<a id="4bfc85d2dc40c4c4"></a>
### Description

It obtains the current user's number ID.

> In cluster system, the value may vary depending on the connected server.  
> It is recommended to use [CURRENT_USER](#26fdffa4d0851f4c) function obtaining the current username.

<a id="5f8d8106b8b64c0d"></a>
### Example

```
% gsql test test

gSQL> SELECT USER_ID() FROM dual;

USER_ID()
---------
        6

1 row selected.
```

<a id="87a6865823800b0e"></a>
## UUID

<a id="99b51ab8ac249fad"></a>
### Syntax

```
UUID()
```

<a id="9a401149cdecb73a"></a>
### Description

It creates the universal unique identifier, then returns it.   
The return type is VARBINARY type, and it internally consists of 16 bytes.

<a id="9709551069fb834d"></a>
### Example

```
gSQL> SELECT HEX( UUID() ) FROM DUAL;
HEX( UUID() )                   
--------------------------------
E6F0A5C2387511E8B95259E479C2FD50
1 row selected.
```

<a id="1cd428a63cef1d10"></a>
## VAR_POP

<a id="d25713898293480c"></a>
### Syntax

```
VAR_POP( expr )
```

<a id="ed1e80d54dded0ba"></a>
### Description

It is an aggregation function, and it obtains the population variance of an expr set. If the number of expr sets except for NULL is one, then it returns 0.

The following table describes the arguments and result types.

**Argument and result type of VAR_POP**

<a id="15147335fbff9282"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The population variance is a variance of the population (entire) group, and it is the average of the square value of deviation. In other words, it is calculated by extracting the population average (the entire average) from each value of the data, and squaring each value, then adding them together and dividing them by the number of datas in the population group.   
> This value is used to figure out how far each value is from the average value.

For more information, refer to [STDDEV_POP](#d0a07183b6011d0d).

<a id="f0e86d11630929ea"></a>
### Example

```
gSQL> SELECT VAR_POP(c1) FROM t1;

VAR_POP(C1)
-----------
     105.76

1 row selected.
```

<a id="4ad2679db722d599"></a>
## VAR_SAMP

<a id="0ec1a7d20ef104e8"></a>
### Syntax

```
VAR_SAMP( expr )
```

<a id="1132fcd4ed31393e"></a>
### Description

It is an aggregation function, and it obtains the sample variance of an expr set. If the number of expr sets except for NULL is one, then it returns NULL.

The following table describes the arguments and result types.

**Argument and result type of VAR_SAMP**

<a id="a5c7c52fb745481e"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> Unlike the population variance dealing with the population (entire) group, the sample variance deals with the average and deviation of extracted samples. In other words, it is calculated by extracting the sample average from each value of the data, and squaring each value, then adding them together and dividing them by the number of datas in the population group minus 1.   
> This value is used to figure out the variance of the population group.

For more information, refer to [STDDEV_SAMP](#d4efefa035560e9e).

<a id="576edab1f42754e3"></a>
### Example

```
gSQL> SELECT VAR_SAMP(c1) FROM t1;

VAR_SAMP(C1)
------------
       132.2

1 row selected.
```

<a id="b796833489baa110"></a>
## VARIANCE

<a id="e24709818a7405fa"></a>
### Syntax

```
VARIANCE( [ ALL | DISTINCT ] expr )
```

<a id="80f775a1eeeebb94"></a>
### Description

It is an aggregation function, and it obtains the variance of an expr set.

If ALL is specified, this function is performed for all values. If DISTINCT is specified, this function is performed for the values of which the duplicates were deleted from. If it is not specified, it is processed as if ALL is apecified.

If the number of expr sets except for NULL after deleting the duplicates by using DISTINCT is one, then it returns 0.

The following table describes the arguments and result types.

**Argument and result type of VARIANCE**

<a id="cb7d403c6b010782"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> GOLDILOCKS gets the variance as follows.  
> • If the number of expr sets is 1, then it returns 0.  
> • If the number of expr sets is bigger than 1, it returns the value of [STDDEV_SAMP (expr)](#d4efefa035560e9e).

For more information, refer to [STDDEV](#443de9b5cf1bfac6).

<a id="01441fdd18316dfe"></a>
### Example

```
gSQL> SELECT VARIANCE(c1) FROM t1;

VARIANCE(C1)
------------
       132.2

1 row selected.


gSQL> SELECT VARIANCE(ALL c1) FROM t1;

VARIANCE(ALL C1)
----------------
           132.2

1 row selected.


gSQL> SELECT VARIANCE(DISTINCT c1) FROM t1;

VARIANCE(DISTINCT C1)
---------------------
               176.25

1 row selected.
```

<a id="6c548c20dd8a2b67"></a>
## VERSION

<a id="0bd16f1f7298dc1b"></a>
### Syntax

```
VERSION()
```

<a id="ce1366c44da13554"></a>
### Description

It obtains the product's version string.

<a id="526f63ff1b301d09"></a>
### Example

```
gSQL> SELECT VERSION() FROM dual;

VERSION()                            
-------------------------------------
Release Name.X.X.X revision(XXXXX)

1 row selected.
```

<a id="a8fa56ec19de906b"></a>
## WIDTH_BUCKET

<a id="bda596e0863e790e"></a>
### Syntax

```
WIDTH_BUCKET( num, min, max, cnt )
```

<a id="f4240890e9bc70aa"></a>
### Description

It creates a section of the same width as cnt within a range between specified min and max, and it returns the section location in which the num is located.

The data type of num argument, min argument, max argument and cnt argument can be a numeric data type.

min, max means the range for the section. If the min value is equal to the max value, an error is returned.  
cnt means the number of sections. The cnt value should be a positive number. If the cnt value is 0 or a negative number, an error is returned.   
The section's location is numbered from one.

If any of num, min, max, cnt is NULL, the result is also NULL.

<a id="f82d5d47c8f9c7a5"></a>
### Example

```
gSQL> SELECT WIDTH_BUCKET( 5, 1, 20, 5 ) AS RESULT FROM DUAL;
RESULT
------
     2
1 row selected.
```

---

[← 16. Built-in Data Type References](16-built-in-data-type-references.md) · [Table of contents](../README.md) · [18. SQL References →](18-sql-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
