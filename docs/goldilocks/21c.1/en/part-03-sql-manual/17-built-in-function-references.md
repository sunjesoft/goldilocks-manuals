<a id="2a02d5750e742ea5"></a>

# 17. Built-in Function References

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/2a02d5750e742ea5)  
> Tag: `21c.1_35_tag`

[← 16. Built-in Data Type References](16-built-in-data-type-references.md) · [Table of contents](../README.md) · [18. SQL References (A~B) →](18-sql-references-a-b.md)

<a id="6d1c78a7e3320173"></a>
## * (MULTIPLICATION)

<a id="611b516f51db6c0d"></a>
### Syntax

```
expr1 * expr2
```

<a id="e0a0057565ea96b9"></a>
### Description

It returns the multiplication result of expr1 and expr2.

The multiplication types and result types are as follows.  
For more information, refer to [Type Conversion](11-sql-elements.md#6b01e7e8d592753b).

**Numeric * operation**

<a id="8ff0f6276561ef37"></a>
| expr1 (expr2) | expr2 (expr1) | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="bc6acd88b01670e2"></a>
<table class="table column_count_3"><caption>INTERVAL * operation</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type is the interval type.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type is the interval type.)</div></td></tr><tr><td class="to_left" colspan="3"><div>Refer to <a class="reference text" href="#234e67b6c3f4206b">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

**INTERVAL type details which is included in INTERVAL type written in the following table**

<a id="234e67b6c3f4206b"></a>
<table><thead><tr><th align="center">INTERVAL YEAR TO MONTH</th><th align="center">INTERVAL DAY TO SECOND</th></tr></thead><tbody><tr><td valign="middle"><ul><li>INTERVAL YEAR</li><li>INTERVAL MONTH</li><li>INTERVAL YEAR TO MONTH</li></ul></td><td valign="middle"><ul><li>INTERVAL DAY</li><li>INTERVAL HOUR</li><li>INTERVAL MINUTE</li><li>INTERVAL SECOND</li><li>INTERVAL DAY TO HOUR</li><li>INTERVAL DAY TO MINUTE</li><li>INTERVAL DAY TO SECOND</li><li>INTERVAL HOUR TO MINUTE</li><li>INTERVAL HOUR TO SECOND</li><li>INTERVAL MINUTE TO SECOND</li></ul></td></tr></tbody></table>

<a id="c97bc5449e175e5a"></a>
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

<a id="0e2c8a0de2443dd0"></a>
## + (ADDITION)

<a id="78d0e3146f10682f"></a>
### Syntax

```
expr1 + expr2
```

<a id="d7d058e565f4357f"></a>
### Description

It returns the addition result of expr1 and expr2.

The addition types and result types are as follows.  
For more information, refer to [Type Conversion](11-sql-elements.md#6b01e7e8d592753b).

**Numeric + operation**

<a id="3a0f1a90ea346d9e"></a>
| expr1 (expr2) | expr2 (expr1) | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="b729c636adb1350d"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) + operation</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference text" href="#234e67b6c3f4206b">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="481fd39bd7717529"></a>
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

<a id="14f953b679c0fbaa"></a>
## + (POSITIVE)

<a id="d9e5c8c01b1932bf"></a>
### Syntax

```
+ expr
```

<a id="3bbc20cd1801d184"></a>
### Description

The + sign is displayed in expr.

<a id="85ef142123c7a43c"></a>
### Example

```
gSQL> SELECT +3 AS RESULT1, +(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      3      -3
1 row selected.
```

<a id="a6b18efcabddbb15"></a>
## - (NEGATIVE)

<a id="2b8b03615893e021"></a>
### Syntax

```
- expr
```

<a id="16749c3891ccccd6"></a>
### Description

The - sign is displayed in expr.

<a id="165d6bd5aaaacfe6"></a>
### Example

```
gSQL> SELECT -3 AS RESULT1, -(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     -3       3
1 row selected.
```

<a id="dd9bf2d82d91f7e0"></a>
## - (SUBTRACTION)

<a id="1d4dd9ec491e7494"></a>
### Syntax

```
expr1 - expr2
```

<a id="88ecf1c0e3f6e24b"></a>
### Description

It returns the subtraction result of expr1 and expr2.

The subtraction types and result types are as follows.  
For more information, refer to [Type Conversion](11-sql-elements.md#6b01e7e8d592753b).

**Numeric - operation**

<a id="8e4cad4aacc2f51c"></a>
| expr1 | expr2 | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="db35eb6c40676205"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) - operation</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMBER</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference" href="#234e67b6c3f4206b">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="835b3db3a6ca7802"></a>
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

<a id="d48bd63124db7ea5"></a>
## / (DIVISION)

<a id="3ed6bf80bc3407ad"></a>
### Syntax

```
expr1 / expr2
```

<a id="859e011adac81e1b"></a>
### Description

It returns the division result of expr1 and expr2.

The division types and result types are as follows.  
For more information, refer to [Type Conversion](11-sql-elements.md#6b01e7e8d592753b).

**Numeric / operation**

<a id="967ef0a0f22e7ebe"></a>
| expr1 | expr2 | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER | NUMBER |
| NATIVE_DOUBLE | NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="2d60fcfb4a0b25a8"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) / operation</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type is interval type.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type is interval type.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference text" href="#234e67b6c3f4206b">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="68de5b3fee25c5e0"></a>
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

<a id="27f96168e3b13d2a"></a>
## || (CONCATENATE)

<a id="076d3e7f03ce772c"></a>
### Syntax

```
str1 || str2
```

<a id="40929bdd244b2505"></a>
### Description

CONCATENATE returns the string concatenating str1 and str2.

If either str1 or str2 is NULL, the string except NULL is returned. If both of str1 and str2 are NULL, NULL is returned.

The argument can be a type which can be converted to either character string type or binary string type.  
For more information, refer to [Type Conversion](11-sql-elements.md#6b01e7e8d592753b).

It is an alias of [CONCAT](#a4c488494880b2bf), [CONCATENATE](#3e3cf35912cee071).

The result types are as follows.

**The result types of || (CONCATENATE)**

<a id="eb7c607d17107ced"></a>
| Data type | CHAR | VARCHAR | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR | CHAR | VARCHAR | LONG VARCHAR |
| VARCHAR | VARCHAR | VARCHAR | LONG VARCHAR |
| LONG VARCHAR | LONG VARCHAR | LONG VARCHAR | LONG VARCHAR |
| Data type | BINARY | VARBINARY | LONG VARBINARY |
| BINARY | BINARY | VARBINARY | LONG VARBINARY |
| VARBINARY | VARBINARY | VARBINARY | LONG VARBINARY |
| LONG VARBINARY | LONG VARBINARY | LONG VARBINARY | LONG VARBINARY |

<a id="6b8a25aa695ed22c"></a>
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

<a id="8589f4e17cd05e3a"></a>
## ABS

<a id="76e70f933d6d89c9"></a>
### Syntax

```
ABS( num )
```

<a id="db1c52ee9f7f0f0e"></a>
### Description

ABS returns the absolute value of num.

The num argument can be a numeric type or types which can be converted to number.  
If num is NULL, then it returns NULL.

<a id="6be12d9441ff1f3f"></a>
### Example

```
gSQL> SELECT ABS(-1) AS RESULT1, ABS(1) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1       1
1 row selected.
```

<a id="ea90107bb9072638"></a>
## ACOS

<a id="70f9deddbc4e2b0e"></a>
### Syntax

```
ACOS( num )
```

<a id="e58e1c5767941f94"></a>
### Description

ACOS returns the arc cosine value of num.  

The num argument should be in the range of -1 to 1.   
If num is NULL, then it returns NULL.  

It returns the radians value in the range of 0 and pi.

<a id="5019111fad92ba7b"></a>
### Example

```
gSQL> SELECT ACOS( 1 ) FROM DUAL;
ACOS( 1 )
---------
        0
1 row selected.
```

<a id="ef9d64c764ea7905"></a>
## ADDDATE

<a id="b0ced401ce4ff048"></a>
### Syntax

```
ADDDATE( date, INTERVAL expr unit  )
ADDDATE( expr, days )
```

<a id="a7a7776fb5af4725"></a>
### Description

ADDDATE adds the second argument to the first argument, then returns the result.  

If any of the input argument value is NULL, the result is also NULL.  
The first argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, and the second argument data type can be INTERVAL or numeric.

The result type is as same as [(DATETIME/INTERVAL) + operation](#b729c636adb1350d).

<a id="396470c7f7d9cad0"></a>
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

<a id="48367ba7e97de00e"></a>
## ADDTIME

<a id="3d8668c47751b4d5"></a>
### Syntax

```
ADDTIME( expr1, expr2 )
```

<a id="78e11375cb94f9fb"></a>
### Description

ADDTIME adds expr2 to expr1, then returns the result.

expr1 data type can be TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE TYPE, and expr2 data type can be INTERVAL DAY TO SECOND TYPE.  

If expr1 or expr2 is NULL, the result is NULL.

The result type is as same as [(DATETIME/INTERVAL) + operation](#b729c636adb1350d).

<a id="e426d2d0811fd118"></a>
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

<a id="cd34a065d201fe45"></a>
## ADD_MONTHS

<a id="3efd631f71595d6e"></a>
### Syntax

```
ADD_MONTHS( date, number )
```

<a id="ec06ae35a74dd2fa"></a>
### Description

ADD_MONTHS adds as many month as the number to the date, then returns the result.  
After ADD_MONTHS operation, if the date is bigger than the last day of the month, it is adjusted to the last day of the month.

The data type of date argument can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, and the number argument can be a numeric type.  
If any of the input argument is NULL, the result is also NULL.

The result type is always DATE regardless of the input argument date type.

<a id="c72ee2224963a4d7"></a>
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

<a id="561481b108d62495"></a>
## ASCII

<a id="d4b9a26b81108cb3"></a>
### Syntax

```
ASCII( char )
```

<a id="ea25d65d54004f88"></a>
### Description

It returns the database character set code of the first character of char in decimal form.  

The data type of char can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING or can be a type which can be converted to a character type, and the return type is NUMBER.  
If char is NULL, then it returns NULL.

<a id="f3bd7e4db35e219e"></a>
### Example

```
gSQL> SELECT ASCII( 'G' ) AS RESULT FROM DUAL;
RESULT
------
    71
1 row selected.
```

<a id="00cfe6ec333363ea"></a>
## ASIN

<a id="9cab9a46a188080d"></a>
### Syntax

```
ASIN( num )
```

<a id="d681bec341ac70d9"></a>
### Description

ASIN returns the arc sin value of num.

The num argument should be in the range of -1 to 1.  
If num is NULL, then it returns NULL.

It returns the radians value in the range of -pi/2 and pi/2.

<a id="39f336b371076d99"></a>
### Example

```
gSQL> SELECT ASIN( 0 ) FROM DUAL;
ASIN( 0 )
---------
        0
1 row selected.
```

<a id="dc225d9a2fd0cf75"></a>
## ATAN

<a id="f1bf06cd35a676eb"></a>
### Syntax

```
ATAN( num )
```

<a id="46f82fe04b067076"></a>
### Description

ATAN returns the arc tangent value of num.

The num value range is not limited. It returns the radians value in the range of -pi/2 and pi/2.  
If num is NULL, then it returns NULL.

<a id="2871db52aea90151"></a>
### Example

```
gSQL> SELECT ATAN(0.5) FROM DUAL;
       ATAN(0.5)
----------------
.463647609000806
1 row selected.
```

<a id="9e6cb004df3acf4d"></a>
## ATAN2

<a id="1e261fcdbf0a2abe"></a>
### Syntax

```
ATAN2( num1, num2 )
```

<a id="ec129ac46211f1b1"></a>
### Description

ATAN2 returns the arc tangent value of num1 and num2.

The num1 argument value range is not limited. It returns the radians value in the range of -pi and pi.  
Either num1 or num2 is NULL, then it returns NULL.

<a id="e01cf85cbd29ae6c"></a>
### Example

```
gSQL> SELECT ATAN2(1,2) FROM DUAL; 
      ATAN2(1,2)
----------------
.463647609000806
1 row selected.
```

<a id="d4598c5a16608649"></a>
## AVG

<a id="b3b886d22de2e2c5"></a>
### Syntax

```
AVG( [ ALL | DISTINCT ] num )
```

<a id="290d5ec7486988f6"></a>
### Description

It is an aggregate function, and it obtains average value of exprs.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

<a id="adcd1cf3fc051aea"></a>
### Example

```
gSQL> SELECT AVG(c1) FROM t1;

AVG(C1)
-------
      2

1 row selected.
```

<a id="5e22e5a15e8239bb"></a>
## BITAND

<a id="1429df99f65019bb"></a>
### Syntax

```
BITAND( num1, num2 )
```

<a id="626e4c69f64b8f7a"></a>
### Description

It returns the AND operation result for the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT or a data type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.  
If any of the input argument is NULL, the result is also NULL.

The result type is NATIVE_BIGINT.

<a id="f8d864cf2cd69968"></a>
### Example

```
gSQL> SELECT BITAND( 5, 3 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="7e9d9703d589fa0b"></a>
## BITNOT

<a id="8b46b415d768546e"></a>
### Syntax

```
BITNOT( num )
```

<a id="b1dbde6722cf54f2"></a>
### Description

It returns the NOT operation result for the num bit.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT or a data type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.  
If the input argument is NULL, the result is also NULL.

The result type is as follows.  
• If the input argument is NATIVE_SMALLINT type, its result type is NATIVE_SMALLINT type.  
• If the input argument is NATIVE_INTEGER type, its result type is NATIVE_INTEGER type.  
• If the input argument is NATIVE_BIGINT type, its result type is NATIVE_BIGINT type.

<a id="2f2ab4a46a5adad4"></a>
### Example

```
gSQL> SELECT BITNOT( 5 ) AS RESULT FROM DUAL;
RESULT
------
    -6
1 row selected.
```

<a id="6bc333068edf7846"></a>
## BITOR

<a id="649dc8c4cff6a802"></a>
### Syntax

```
BITOR( num1, num2 )
```

<a id="4fa937e9cde79760"></a>
### Description

It returns the OR operation result for the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT types or a data type which can be converted to NATIVE_BIGINT type.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.  
If any of the input argument value is NULL, the result is NULL.

The result type is NATIVE_BIGINT type.

<a id="95e510b90ecf59c5"></a>
### Example

```
gSQL> SELECT BITOR( 5, 3 ) FROM DUAL;

BITOR( 5, 3 )
-------------
            7
1 row selected.
```

<a id="564b16f195b9e142"></a>
## BITXOR

<a id="ed7c77b8179cd9b3"></a>
### Syntax

```
BITXOR( num1, num2 )
```

<a id="45bd792c15c21c9a"></a>
### Description

It returns the XOR operation result for the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT or a data type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.  
If any of the input argument value is NULL, the result is NULL.

The result type is NATIVE_BIGINT.

<a id="81b37ef46b49cc07"></a>
### Example

```
gSQL> SELECT BITXOR( 5, 3 ) FROM DUAL;
BITXOR( 5, 3 )
--------------
             6
1 row selected.
```

<a id="431251aa94f8c579"></a>
## BIT_LENGTH

<a id="5b0d03d85592f529"></a>
### Syntax

```
BIT_LENGTH( str )
```

<a id="31c89cf6aef77a78"></a>
### Description

BIT_LENGTH returns the number of bits for str.  
If str is NULL, then it returns NULL.

<a id="0e11ceb4633aa50e"></a>
### Example

```
gSQL> SELECT BIT_LENGTH( 'LIKE' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
             32
    1 row selected.
```

<a id="22909c13767b86f4"></a>
## BYTE_LENGTH

<a id="7fedafeec1957264"></a>
### Syntax

```
BYTE_LENGTH( str )
```

<a id="2f537c207f13a958"></a>
### Description

It is an alias of OCTET_LENGTH.  
For more information, refer to [OCTET_LENGTH](#e589ba3d27704d5c), [LENGTHB](#ef7333f082e22889).

<a id="7a8e3e19861a81d0"></a>
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

<a id="45142aa16736b922"></a>
## CASE2

<a id="97e233709b9a0953"></a>
### Syntax

```
CASE2( condition1, result1
      [, condition2, result2
       , ...
       , conditionN, resultN ]
      [, default ] )
```

<a id="be6edd1c93f78a8c"></a>
### Description

CASE2 evaluates the condition in the described order.  
If the comparison result is FALSE, it continues evaluating until TRUE comes up.  
If the comparison result is TRUE, it returns the corresponding result, and does not evaluate any more.  
If all the comparison results are FALSE, it returns the default value. If the default is omitted, it returns NULL.

If multiple types are used in result, then the result type is determined according to [Result Type Combination Rule](11-sql-elements.md#ea5401033b086287).

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

<a id="e8c02839e5de1fdc"></a>
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

<a id="f7045587f751bee5"></a>
## CBRT

<a id="ff483827ae78ef75"></a>
### Syntax

```
CBRT( num )
```

<a id="b3ad5d7539e4a5ae"></a>
### Description

It returns the cube root of num.  
If num is NULL, the result is also NULL.

<a id="3477289f4100b728"></a>
### Example

```
gSQL> SELECT CBRT( 27 ) FROM DUAL;
CBRT( 27 )
----------
         3
1 row selected.
```

<a id="1eca766774a5cc00"></a>
## CEIL

<a id="507b92ecc6d4d3b0"></a>
### Syntax

```
CEIL( num )
CEILING( num )
```

<a id="96fc861ef4b1dee3"></a>
### Description

CEIL returns the smallest integer which is equal to or bigger than num.  
If num is NULL, then it returns NULL.

<a id="0df0fb64f4f25291"></a>
### Example

```
gSQL> SELECT CEIL( 3.5 ) AS RESULT1, CEIL( -3.5 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      4      -3
1 row selected.
```

<a id="0a6476d441957234"></a>
## CHAR_LENGTH

<a id="65b3806a3a967aff"></a>
### Syntax

```
CHAR_LENGTH( str )            
CHARACTER_LENGTH( str )
```

<a id="23fd341795153a0d"></a>
### Description

CHAR_LENGTH returns the number of character for str according to the character set.

The str can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or it can be a data type which can be converted to character type. The return type is NATIVE_BIGINT.

If the data type of str is CHARACTER, the trailing blanks are included in the calculation.  
If str is NULL, it returns NULL.

It is an alias of [LENGTH](#351ffd54a652fede).

<a id="8aa4dd39985d792b"></a>
### Example

Multi byte character set: (e.g. UTF8)

```
gSQL> SELECT CHAR_LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="72aa3e509a49b6b7"></a>
## CHR

<a id="e814a71e4e5a5dc5"></a>
### Syntax

```
CHR( num )
```

<a id="e68b8a97d708bae8"></a>
### Description

It returns a character in the database character set code corresponding to num.

num is a numeric type.  
If num is NULL, then it returns NULL.  

The return type is VARCHAR.

<a id="30f54aad188e8d4b"></a>
### Example

```
gSQL> SELECT CHR(71) FROM DUAL;
CHR(71)
-------
G      
1 row selected.
```

<a id="63c056411adfe1d1"></a>
## CLOCK_DATE

<a id="b17723f55fafabd6"></a>
### Syntax

```
CLOCK_DATE()
```

<a id="5afe5f828cea778d"></a>
### Description

Whenever the CLOCK_DATE function is called, the current date (DATE type) value is obtained.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="97b43e6e87ff4b77"></a>
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

<a id="80bb14b23f48618e"></a>
## CLOCK_LOCALTIME

<a id="3a7e062d25094ad1"></a>
### Syntax

```
CLOCK_LOCALTIME()
```

<a id="d90facf8bcabfe85"></a>
### Description

Whenever the CLOCK_LOCALTIME function is called, the current time value without TIME ZONE (TIME WITHOUT TIME ZONE type) is obtained.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.  
• STATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="2a9f9e4295ef1ef1"></a>
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

<a id="db6e91619975b991"></a>
## CLOCK_LOCALTIMESTAMP

<a id="5e41b4a7d6980bab"></a>
### Syntax

```
CLOCK_LOCALTIMESTAMP()
```

<a id="7cebf968ccf27c73"></a>
### Description

Whenever the CLOCK_LOCALTIMESTAMP() function is called, the current TIMESTAMP value without TIME ZONE (TIMESTAMP WITHOUT TIME ZONE type) is obtained.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• STATEMENT_LOCALTIMESTAMP(): All TIMESTAMP values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="32324c9ee8a933eb"></a>
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

<a id="54e79ce90b38a26a"></a>
## CLOCK_TIME

<a id="59cce990e45a92d3"></a>
### Syntax

```
CLOCK_TIME()
```

<a id="4d05593b5a6acee1"></a>
### Description

Whenever the CLOCK_TIME() function is called, the current time value with TIME ZONE (TIME WITH TIME ZONE type) is obtained.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• STATEMENT_TIME(): All time values in an SQL statement are same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="291702efe7c832a2"></a>
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

<a id="9fad6c92cb1884b1"></a>
## CLOCK_TIMESTAMP

<a id="024221d871cf26bf"></a>
### Syntax

```
CLOCK_TIMESTAMP()
```

<a id="22e42e56b547f990"></a>
### Description

Whenever CLOCK_TIMESTAMP() function is called, the current TIMESTAMP value with TIME ZONE (TIMESTAMP WITH TIME ZONE type) is obtained.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_TIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• STATEMENT_TIMESTAMP(): All TIMESTAMP values in an SQL statement are same.   
• CLOCK_TIMESTAMP(): Whenever the function is called, the current TIMESTAMP value is obtained.

<a id="bc1a084d72ddec53"></a>
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

<a id="0583103bf73111d0"></a>
## COALESCE

<a id="bdf2148d5ba2c107"></a>
### Syntax

```
COALESCE( expr1, ..., exprN )
```

<a id="a3b3019b9ebc736e"></a>
### Description

It returns the first non null expr in the expr list.  
If all expr in the expr list are null, it returns null.  
In the expr list, there should be two or more expr.

If multiple types are in the expr list, the result type is determined by the [Result Type Combination Rule](11-sql-elements.md#ea5401033b086287).

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

<a id="cb04a78d59aa2ce3"></a>
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

<a id="a4c488494880b2bf"></a>
## CONCAT

<a id="1ee56a3f8f147e94"></a>
### Syntax

```
CONCAT( str1, str2, ... )
```

<a id="558702a2174dc108"></a>
### Description

It is an alias of || ( CONCATENATE ).  
It is an argument of CONCAT function and 2 ~ 254 number of CONCATs can be set.  
For more information, refer to [|| (CONCATENATE)](#27f96168e3b13d2a), [CONCATENATE](#3e3cf35912cee071).

<a id="6912763d63ce19b3"></a>
### Example

```
gSQL> SELECT CONCAT( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="3e3cf35912cee071"></a>
## CONCATENATE

<a id="80aeff173b333801"></a>
### Syntax

```
CONCATENATE( str1, str2, ... )
```

<a id="2e7e4bd039555915"></a>
### Description

It is an alias of || ( CONCATENATE ).  
It is an argument of CONCATENATE  function and 2 ~ 254 number of CONCATENATEs can be set.  
For more information, refer to [CONCAT](#a4c488494880b2bf), [|| (CONCATENATE)](#27f96168e3b13d2a).

<a id="e42f4fde63fdabed"></a>
### Example

```
gSQL> SELECT CONCATENATE( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="ccdf5e5a5f9f42c7"></a>
## COS

<a id="dadb4d995976652b"></a>
### Syntax

```
COS(num)
```

<a id="e82b210817a1cdfa"></a>
### Description

It returns the COSINE value of num.  
If the num argument is NULL, the result is also NULL.

<a id="1412b34766e65ffd"></a>
### Example

```
gSQL> SELECT COS( 0 ) FROM DUAL;
COS( 0 )
--------
       1
1 row selected.
```

<a id="c62fbf540941bd93"></a>
## COT

<a id="f57fc262211e5ec1"></a>
### Syntax

```
COT(num)
```

<a id="64f5b579c40df316"></a>
### Description

It returns the COTANGENT value of num.  
If the num argument is NULL, the result is also NULL.

<a id="dc4769529375cbed"></a>
### Example

```
gSQL> SELECT COT( 1 ) FROM DUAL;
        COT( 1 )
----------------
.642092615934331
1 row selected.
```

<a id="998f0f569b77e8f7"></a>
## COUNT

<a id="bd2d6d3dd7adc63e"></a>
### Syntax

```
COUNT( [ ALL | DISTINCT ] expr )
```

<a id="7970cc5bda5227fb"></a>
### Description

It is an aggregate function. It returns the number of rows whose expr is not NULL.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

<a id="6b231595b4eba1dc"></a>
### Example

```
gSQL> SELECT COUNT(c1) FROM t1;

COUNT(C1)
---------
        3

1 row selected.
```

<a id="c4a7790c0e2bb2cb"></a>
## COUNT(*)

<a id="6e80c03a378e7f8f"></a>
### Syntax

```
COUNT(*)
```

<a id="a679ed879255bcf2"></a>
### Description

It is an aggregate function, and the number of rows is obtained.  
It has nothing to do with whether it is NULL or not because an expression is not explicitly specified.

<a id="c8dce5c05119743a"></a>
### Example

```
gSQL> SELECT COUNT(*) FROM t1;

COUNT(*)
--------
       4

1 row selected.
```

<a id="d77c71ce74d7c1f9"></a>
## CURRENT_CATALOG

<a id="2bbc88a3f19b2345"></a>
### Syntax

```
CURRENT_CATALOG [()]
```

<a id="bea6ee7e90f6fbd0"></a>
### Description

The catalog name (database name) is obtained.

<a id="e649bf99556e8c8e"></a>
### Example

```
gSQL> SELECT CURRENT_CATALOG FROM dual;

CURRENT_CATALOG
---------------
TEST_DB        

1 row selected.
```

<a id="87a9c1e1d15a3493"></a>
## CURRENT_DATE

<a id="7f339263b56f9d2c"></a>
### Syntax

```
CURRENT_DATE [()]
STATEMENT_DATE()
```

<a id="79ee38c6054bfd78"></a>
### Description

The current date (DATE type) is obtained.

CURRENT_DATE is an SQL standard function.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• CURRENT_DATE, STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="a37db8cf10691af1"></a>
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

<a id="edecc20440a54b30"></a>
## CURRENT_SCHEMA

<a id="698e698e36eeb1c8"></a>
### Syntax

```
CURRENT_SCHEMA [()]
```

<a id="1471791c247a9c71"></a>
### Description

User's current SCHEMA is obtained.

<a id="6823b80c35aa71d8"></a>
### Example

```
gSQL> SELECT CURRENT_SCHEMA FROM dual;

CURRENT_SCHEMA
--------------
PUBLIC        

1 row selected.
```

<a id="d245853296663b19"></a>
## CURRENT_TIME

<a id="0a3c652bd4f1bde7"></a>
### Syntax

```
CURRENT_TIME [()]
STATEMENT_TIME()
```

<a id="94febbdedfa0a591"></a>
### Description

The current TIME WITH TIME ZONE type value based on the session time is obtained.

CURRENT_TIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• CURRENT_TIME, STATEMENT_TIME(): All time values in an SQL statement are same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="25e7ddbbfd4a0960"></a>
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

<a id="025b5d7f009a8d60"></a>
## CURRENT_TIMESTAMP

<a id="c2d8750178372c87"></a>
### Syntax

```
CURRENT_TIMESTAMP [()]
STATEMENT_TIMESTAMP()
```

<a id="a21fd878490585a1"></a>
### Description

It obtains the TIMESTAMP WITH TIME ZONE type value based on the session time.

CURRENT_TIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_TIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• CURRENT_TIMESTAMP, STATEMENT_TIMESTAM(): All TIMESTAMP values in an SQL statement are same.  
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="865f130cbb6671e5"></a>
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

<a id="b8d8322580f3d222"></a>
## CURRENT_USER

<a id="80e4aea681d71276"></a>
### Syntax

```
CURRENT_USER [()]
```

<a id="8204b5b3e98a53b4"></a>
### Description

It returns the current user.

The user information is managed in three types as follows.

- Logon user: It is a user who performed login, and it is maintained until the connection is closed.
- Session user: It is as same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: It is generally as same as the session user, but it is temporarily changed internally in system to control access when using the PSM, view.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="91569098a3ca627e"></a>
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

<a id="e0d30993727500e4"></a>
## CURRVAL

<a id="7f635afc138fb8de"></a>
### Syntax

```
seq_name.CURRVAL
CURRVAL(seq_name)
```

<a id="f1bd4efe8494f263"></a>
### Description

The current value of the sequence object is obtained.

A sequence value should be set with NEXTVAL(seq_name) at least once.

<a id="59a408fa70358903"></a>
### Example

```
gSQL> SELECT seq.CURRVAL FROM dual;

SEQ.CURRVAL
-----------
          1

1 row selected.
```

<a id="2aebd9e439b5cde3"></a>
## DATEADD

<a id="1845a07634d1288d"></a>
### Syntax

```
DATEADD( datepart, number, date )
```

<a id="fe95883eec2e6118"></a>
### Description

It adds number to the specified datepart of date, and returns the result.

If the number is decimal point, it is not rounded off.  
The date data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE.  
If number or date is NULL, the result is also NULL.

The result type which is as same as the input date argument type is returned.

**Available string format in datepart**

<a id="10893c003195f6e3"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">Description</th></tr><tr><td>YEAR</td><td>Year</td></tr><tr><td>QUARTER</td><td>Quarter</td></tr><tr><td>MONTH</td><td>Month</td></tr><tr><td>DAYOFYEAR</td><td>Day of year</td></tr><tr><td>DAY</td><td>Day</td></tr><tr><td>WEEK</td><td>Week</td></tr><tr><td>WEEKDAY</td><td>Weekday</td></tr><tr><td>HOUR</td><td>Hour</td></tr><tr><td>MINUTE</td><td>Minute</td></tr><tr><td>SECOND</td><td>Second</td></tr><tr><td>MILLISECOND</td><td>Millisecond</td></tr><tr><td>MICROSECOND</td><td>Microsecond</td></tr></tbody></table>

<a id="9e0f32867a8a1de6"></a>
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

<a id="3c6d25f2c067f3df"></a>
## DATEDIFF

<a id="5e0c56ff5d861ea1"></a>
### Syntax

```
DATEDIFF( datepart, startdate, enddate )
```

<a id="ffa8e52600ca77ff"></a>
### Description

It substracts startdate from enddate, then returns the result to the specified datepart.

If the startdate or enddate is NULL, the result is also NULL.  
The data type of startdate and enddate can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME.

The result type is NUMBER.

**Available string format in datepart**

<a id="6ad6408661e44aaf"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">Description</th></tr><tr><td>YEAR</td><td>Year</td></tr><tr><td>QUARTER</td><td>Quarter</td></tr><tr><td>MONTH</td><td>Month</td></tr><tr><td>DAYOFYEAR</td><td>Day of year</td></tr><tr><td>DAY</td><td>Day</td></tr><tr><td>HOUR</td><td>Hour</td></tr><tr><td>MINUTE</td><td>Minute</td></tr><tr><td>SECOND</td><td>Second</td></tr><tr><td>MILLISECOND</td><td>Millisecond</td></tr><tr><td>MICROSECOND</td><td>Microsecond</td></tr></tbody></table>

<a id="a3a7c0d48c1fd19b"></a>
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

<a id="b774d3b4cdb11212"></a>
## DATE_ADD

<a id="f0d45336a4b3833b"></a>
### Syntax

```
DATE_ADD( date, INTERVAL expr unit  )
```

<a id="1b6dffb788b86984"></a>
### Description

It is the same function as [ADDDATE](#ef9d64c764ea7905) (date, INTERVAL expr unit).

<a id="31de870ceb271d48"></a>
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

<a id="e7d1a3d4b868a9fd"></a>
## DATE_PART

<a id="df6e9f0ff11a3943"></a>
### Syntax

```
DATE_PART( field, datetime )
```

<a id="00d38fb93ccdc69e"></a>
### Description

The result of DATE_PART is as same as the result of the EXTRACT function. It searches for the specified field from the input datetime type, and returns it.

The field argument should be text literal, and YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, TIMEZONE_HOUR, TIMEZONE_MINUTE can be specified to text literal.  
The datetime argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL.

If field is not in the range of datetime, an error is returned.   
For DATE type, field should be YEAR, MONTH, DAY, otherwise an error is returned.  
If datatime is NULL, then it returns NULL.

The return type is NUMBER.

For more information, refer to [EXTRACT](#78638c1e494fd6df).

<a id="640afb9c51865959"></a>
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

<a id="1282686d20a1d1f0"></a>
## DECODE

<a id="7937dc634f0f52ed"></a>
### Syntax

```
DECODE( expr, comparison_expr1, result1
           [, comparison_expr2, result2
            , ...
            , comparison_exprN, resultN ]
           [, default ] )
```

<a id="5df17455f02675da"></a>
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

<a id="43e5e57062fdb2db"></a>
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

<a id="4f9b93fba517963b"></a>
## DEGREES

<a id="c9e3e9b52d33ecc3"></a>
### Syntax

```
DEGREES( radians )
```

<a id="a9b4c792122dc213"></a>
### Description

It converts a degree radians to a value in degrees, and returns the converted value.  
If radians is NULL, then it returns NULL.

<a id="6e62034917d1dd0a"></a>
### Example

```
gSQL> SELECT DEGREES( PI() ) AS RESULT FROM DUAL;
RESULT
------
   180
1 row selected.
```

<a id="f1fbb910ceb7a5e4"></a>
## DIGEST

<a id="ae8f3c7943d5f7ef"></a>
### Syntax

```
DIGEST( data, type )
```

<a id="168b821e1a481d1a"></a>
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

<a id="75ec1c2b271cb78d"></a>
### Example

```
gSQL> SELECT HEX( DIGEST( 'my password', 'SHA256' ) ) AS RESULT FROM DUAL;

RESULT                                                          
----------------------------------------------------------------
BB14292D91C6D0920A5536BB41F3A50F66351B7B9D94C804DFCE8A96CA1051F2

1 row selected.
```

<a id="fc1335d823f4b270"></a>
## DUMP

<a id="0e16d994b2145950"></a>
### Syntax

```
DUMP( expr )
```

<a id="36636f80f9c11999"></a>
### Description

It returns internal representation information of expr.  
Internal representation information is displayed as the data type, byte length and data information.

expr can be any data types.  
If expr is NULL, then it returns NULL.  

The return type is CHARACTER VARYING.

<a id="1cdc9134ddb3edc7"></a>
### Example

```
gSQL> SELECT DUMP( 'DUMP' ) AS RESULT FROM DUAL;
RESULT                           
---------------------------------
Type=CHAR Len=4 : Str=68,85,77,80
1 row selected.
```

<a id="b232bfbda09c5d51"></a>
## EXP

<a id="2e11432cfea974cf"></a>
### Syntax

```
EXP( num )
```

<a id="43a6ae4aad6f5d93"></a>
### Description

It returns squared value of e (base of natural logarithm)'s num.  
If num is NULL, then it returns NULL.

<a id="1c9ba02e63c41647"></a>
### Example

```
gSQL> SELECT EXP( 1 ) AS RESULT FROM DUAL;
          RESULT
----------------
2.71828182845905
1 row selected.
```

<a id="78638c1e494fd6df"></a>
## EXTRACT

<a id="4825a9c850ff3ada"></a>
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

<a id="ea42a4bba8e3ad35"></a>
### Description

It searches for the specified field from an input datetime type, and returns it.

The datetime argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL.

If field is not in the range of datetime, an error is returned.   
For DATE type, the field should be YEAR, MONTH, DAY, otherwise an error is returned.  
The return type is NUMBER.

Result of EXTRACT is as same as the result of the [DATE_PART](#e7d1a3d4b868a9fd) function.

<a id="0afd7c3b45a7396b"></a>
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

<a id="6de97f2c59cc5d59"></a>
## FACTORIAL

<a id="ddec491386495aab"></a>
### Syntax

```
FACTORIAL( num )
```

<a id="34d97455b7f056a5"></a>
### Description

It multiplies the successive natural numbers from 1 to num in order, and returns the result.  
If num is NULL, then it returns NULL.

<a id="6235c2149e69d94c"></a>
### Example

```
gSQL> SELECT FACTORIAL( 5 ) AS RESULT FROM DUAL;
RESULT
------
   120
1 row selected.
```

<a id="e6ce69c54566b085"></a>
## FLOOR

<a id="19250f3a160a241a"></a>
### Syntax

```
FLOOR( num )
```

<a id="eed6ca49706b1173"></a>
### Description

It returns the biggest integer which is equal to or smaller than num.  
If num is NULL, then it returns NULL.

<a id="78f510f732a9bdcd"></a>
### Example

```
gSQL> SELECT FLOOR(42.8) AS RESULT1, FLOOR(-42.8) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     42     -43
1 row selected.
```

<a id="77c63d71a11e0ca5"></a>
## FROM_BASE64

<a id="596683c2fa307095"></a>
### Syntax

```
FROM_BASE64( str )
```

<a id="e7b504b38a4a988f"></a>
### Description

The converted character by base 64 encoding is input to FROM_BASE64, then the decoded binary string is returned.

The input argument data type can be a character type such as CHARACTER VARYING, CHARACTER LONG VARYING, and the result type is a binary character such as BINARY VARYING or BINARY LONG VARYING.

If str is NULL, then the result value is also NULL.  
If str includes characters which are not in the range of base64 character, then it returns an error.  
A newline, carriage return, tab, and space of str is ignored when decoding.

For more information, refer to [TO_BASE64](#b3a0389eb5f09fa5).

<a id="d3c3a91b7995eb5e"></a>
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

<a id="1415b60dacb7dc8b"></a>
## FROM_TZ

<a id="c1996c82b8c6aa56"></a>
### Syntax

```
FROM_TZ( timestamp, timezone )
```

<a id="c7ad1c6d4f2274d1"></a>
### Description

FROM_TZ function converts the timestamp and the timezone in the specified format to TIMESTAMP WITH TIME ZONE type, then returns it.

The timestamp argument should be TIMESTAMP type or the type convertible to TIMESTAMP type.   
If the timestamp argument is NULL, then the result value is also NULL.

The timezone argument should be CHARACTER type such as CHARACTER and CHARACTER VARYING, and the format is 'TZH:TZM'.   
If the timezone argument is NULL, then the result is also NULL.

The result type is TIMESTAMP(6) WITH TIME ZONE.

<a id="70aa13dc6f841707"></a>
### Example

```
gSQL> SELECT 
      FROM_TZ( TIMESTAMP'2021-01-01 10:10:20.000000', '+06:00' ) AS RESULT
        FROM DUAL;
RESULT
-----------------------------------
2021-01-01 10:10:20.000000 +06:00
1 row selected.
```

<a id="3378b66e7e71729f"></a>
## GREATEST

<a id="a7dd6867108821bb"></a>
### Syntax

```
GREATEST( expr1 [, expr2, ... exprn ] )
```

<a id="9c4c3506378ed8be"></a>
### Description

It returns the largest value among the received expr argument.

If any expr argument is NULL, the result value is NULL.

The result type becomes the data type of expr1  (the first expr).   
If the data type of expr1 (the first expr) is a character type and a numeric type then it becomes the type including the range of expr1, ..., exprN each.  
If all of expr1, ..., exprN is described in CHAR type, then all exprs are compared in VARCHAR type and the result type is VARCHAR.

<a id="e05513d8e026efb7"></a>
### Example

```
gSQL> SELECT GREATEST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
   200
1 row selected.
```

<a id="63329345ff035cec"></a>
## HASH32

<a id="9bb53c134126cb0c"></a>
### Syntax

```
HASH32( expr [, expr]... )
```

<a id="2229f2b36c9b28fb"></a>
### Description

The HASH32 function calculates and returns the hash value of the provided expr arguments.

At least one argument must be specified, and up to a maximum of 32 arguments can be provided.  
If any of the input arguments is NULL, the result will be NULL.

The return type is NATIVE_INTEGER.

<a id="6ef2560f13b335ea"></a>
### Example

```
CREATE TABLE t1 ( c_int INTEGER, c_vchar VARCHAR(10), c_date DATE );
INSERT INTO t1 VALUES ( 100, 'GOLDILOCKS', sysdate );
INSERT INTO t1 VALUES ( 200, null, sysdate );

gSQL> SELECT * FROM t1;

C_INT C_VCHAR    C_DATE    
----- ---------- ----------
  100 GOLDILOCKS 2026-02-26
  200 null       2026-02-26

2 rows selected.

gSQL> SELECT HASH32( c_int, c_vchar, c_date ) FROM t1;

HASH32( C_INT, C_VCHAR, C_DATE )
--------------------------------
                      1116649224
                            null

2 rows selected.
```

<a id="feea5870e157c348"></a>
## HEX

<a id="64fa13e8f3f51017"></a>
### Syntax

```
HEX( str )
```

<a id="1586bbc393b73953"></a>
### Description

It returns a str argument in hexadecimal character.  
A str argument data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, a type which can be converted to a character type, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.  
The result type is a character type such as CHARACTER VARYING or CHARACTER LONG VARYING.

If str is NULL, then the result value is also NULL.

If an argument of HEX function is a numeric type, then it returns an error.   
To convert a decimal number to a hexadecimal number, use TO_CHAR() function by using  'X' number format.  
e.g. TO_CHAR( 255, 'XX' )

For more information, refer to [UNHEX](#730bf9e5ae137ebd).

<a id="83dc3ec845057d9b"></a>
### Example

```
gSQL> SELECT HEX( 'abc' ) FROM DUAL;
HEX( 'abc' )
------------
616263      
1 row selected.
```

<a id="d90b3cf94f8f82b3"></a>
## INITCAP

<a id="64a39fe6c9432a40"></a>
### Syntax

```
INITCAP( str )
```

<a id="37757a8f5baa402a"></a>
### Description

It converts the first letter in each word of string str into uppercase, and converts all other letters into lowercase, then it returns the result.

str data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

Each word in string is classified by white space or characters which are not alphanumeric.  
If str is NULL, the result is also NULL.

The return type is as same as str argument datatype.

<a id="b1a264c1edcf96ee"></a>
### Example

```
gSQL> SELECT INITCAP( 'hi GLIESE' ) AS RESULT FROM DUAL;
RESULT   
---------
Hi Gliese
1 row selected.
```

<a id="f31b33524287849a"></a>
## INSTR

<a id="1ba2320c32f8090c"></a>
### Syntax

```
INSTR( str, substr [, position [, occurrence ] ] )
```

<a id="dc2633115c5a3abb"></a>
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

<a id="5fd2e8659e69a599"></a>
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

<a id="52ff0f67a4be1ac5"></a>
## LAST_DAY

<a id="faf333b8ed8ab5cf"></a>
### Syntax

```
LAST_DAY( date )
```

<a id="14ccb3d1128b58ae"></a>
### Description

It returns the last day of the month which is included in date.

The date argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.  
The return type is always DATE regardless of the date argument data type.

If date is NULL, then it returns NULL.

<a id="80948ea0ea381b64"></a>
### Example

```
gSQL> SELECT 
      LAST_DAY( TO_DATE( '2012-07-10', 'YYYY-MM-DD' ) ) AS RESULT FROM DUAL;
RESULT    
----------
2012-07-31
1 row selected.
```

<a id="8ce062813a747033"></a>
## LAST_IDENTITY_VALUE

<a id="6bec1d70be52defc"></a>
### Syntax

```
LAST_IDENTITY_VALUE()
```

<a id="5dbc31fdf421b259"></a>
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

To obtain an identity column value created when performing the INSERT, use [INSERT INTO name RETURNING .. INTO](20-sql-references-h-z.md#1daa6b22c80b52a7) statement as follows.

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

<a id="44b5709415bf9619"></a>
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

<a id="47a3756453ec8bcf"></a>
## LEAST

<a id="49bc5c493428eb12"></a>
### Syntax

```
LEAST( expr1 [, expr2, ... exprn ] )
```

<a id="64a7c4d4801ccab6"></a>
### Description

It returns the smallest value among received expr arguments.

If any of expr is NULL, the result is NULL.

The result type is determined according to the data type of expr1 (the first expr).   
If the data type of expr1 (the first expr) is a character type and a numeric type then it becomes the type including the range of expr1, ..., exprN each.  
If all of expr1, ..., exprN is described in CHAR type, then all exprs are compared in VARCHAR type and the result type is VARCHAR.

<a id="c1713f3adffbfabb"></a>
### Example

```
gSQL> SELECT LEAST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="351ffd54a652fede"></a>
## LENGTH

<a id="927a2f3e79f737bf"></a>
### Syntax

```
LENGTH( str )
```

<a id="c97fef53330c0049"></a>
### Description

It is an alias of [CHAR_LENGTH](#0a6476d441957234).

<a id="0385c24be585bbac"></a>
### Example

Multi byte character set: (e.g.UTF8)

```
gSQL> SELECT LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="ef7333f082e22889"></a>
## LENGTHB

<a id="85cdcd59687b4d47"></a>
### Syntax

```
LENGTHB( str )
```

<a id="9b64af0dd1369cdb"></a>
### Description

It is an alias of [OCTET_LENGTH](#e589ba3d27704d5c).  
For more information, refer to [BYTE_LENGTH](#22909c13767b86f4).

<a id="7274582fffb80ce0"></a>
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

<a id="73b0ca3463ed0b5f"></a>
## LN

<a id="697992bf10a7633b"></a>
### Syntax

```
LN( num )
```

<a id="6c5d28768e1ce985"></a>
### Description

It returns the natural logarithm value of num.  

num should be a value which is bigger than 0.  
If num is NULL, then it returns NULL.

<a id="59952479a258daff"></a>
### Example

```
gSQL> SELECT LN( 2.71828182845905 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="469187cd4d924612"></a>
## LNNVL

<a id="18e09c28ba5716ed"></a>
### Syntax

```
LNNVL( expr )
```

<a id="713fdd27df8245d4"></a>
### Description

Logical Not Null VaLue (LNNVL) function is similar to NOT logical operator, but the difference is that it returns TRUE as in the following example when the input value is null.

<a id="91a821fa7d7574c9"></a>
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

<a id="c0a4c7ad91be28f3"></a>
## LOCALTIME

<a id="4daf7f53abe3322f"></a>
### Syntax

```
LOCALTIME [()]
STATEMENT_LOCALTIME()
```

<a id="7e732d38fff4a90d"></a>
### Description

The current TIME WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.  
• LOCALTIME, STATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="54a6fda3ee53a82e"></a>
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

<a id="41488f82e1ce2c8e"></a>
## LOCALTIMESTAMP

<a id="1d457057d4e5b791"></a>
### Syntax

```
LOCALTIMESTAMP [()]
STATEMENT_LOCALTIMESTAMP()
```

<a id="cb3d383f6704a989"></a>
### Description

The current TIMESTAMP WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• LOCALTIMESTAMP, STATEMENT_LOCALTIMESTAMP(): All TIMESTAMP values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="f31e8deb3530a4b5"></a>
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

<a id="c40e6fcef36aabe1"></a>
## LOCAL_GROUP_ID

<a id="49342d7250f6c70e"></a>
### Syntax

```
LOCAL_GROUP_ID()
```

<a id="145112bbe76df7c9"></a>
### Description

It returns a cluster group ID for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="df3763feeeb0b149"></a>
### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_GROUP_ID() FROM DUAL;

LOCAL_GROUP_ID()
----------------
               1

1 row selected.
```

<a id="dc1b97f0a47f73bd"></a>
## LOCAL_GROUP_NAME

<a id="e677823fbd37920f"></a>
### Syntax

```
LOCAL_GROUP_NAME()
```

<a id="4e1833b30a9a1a9e"></a>
### Description

It returns a cluster group name for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="c1e4eae428b767a2"></a>
### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_GROUP_NAME() FROM DUAL;

LOCAL_GROUP_NAME()
------------------
G1                

1 row selected.
```

<a id="5e47e0b37d7bd474"></a>
## LOCAL_MEMBER_ID

<a id="0763f9fc2ece948d"></a>
### Syntax

```
LOCAL_MEMBER_ID()
```

<a id="ac6b2a59de65f896"></a>
### Description

It returns a cluster member ID for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="be1f0224e3a384d2"></a>
### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_MEMBER_ID() FROM DUAL;

LOCAL_MEMBER_ID()
-----------------
                1

1 row selected.
```

<a id="808db729403ee9a6"></a>
## LOCAL_MEMBER_NAME

<a id="991cd9d795296d46"></a>
### Syntax

```
LOCAL_MEMBER_NAME()
```

<a id="68037da51a58836f"></a>
### Description

It returns a cluster member name for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="bf5765a74bf55f79"></a>
### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_MEMBER_NAME() FROM DUAL;

LOCAL_MEMBER_NAME()
-------------------
G1N1               

1 row selected.
```

<a id="a36e399ef53a89a4"></a>
## LOG

<a id="7e55eabe799bee6e"></a>
### Syntax

```
LOG( num2 )
LOG( num1, num2 )
```

<a id="c96881c4961414f5"></a>
### Description

It returns the logarithm of num2 in the num1 base.  
If num1 is omitted, it returns the logarithm value whose base is 10.

num1 should be a positive number except 1 and 0, and num2 should be a positive number.

If num1 or num2 is NULL, then it returns NULL.

<a id="9e4de6151f387209"></a>
### Example

```
gSQL> SELECT LOG( 100 ) AS RESULT1, LOG( 4, 16 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      2       2
1 row selected.
```

<a id="3eb56e15110f14a3"></a>
## LOGON_USER

<a id="3304c80785828c67"></a>
### Syntax

```
LOGON_USER()
```

<a id="3f3239f31053978a"></a>
### Description

It returns the logged-in user.

The user information is managed in three types as follows.

- Logon user: It is a user who performed login, and it is maintained until the connection is closed.
- Session user: It is as same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: It is generally as same as the session user, but it is temporarily changed internally in system to control access when using the PSM, view.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="1ed3bfd2c4bb31a7"></a>
### Example

```
% gsql test test

gSQL> SELECT LOGON_USER() AS result FROM DUAL;

RESULT
------
TEST  

1 row selected.
```

<a id="b61ef6da327fa368"></a>
## LOWER

<a id="ca26ad9d9bb09896"></a>
### Syntax

```
LOWER( str )
```

<a id="01b4fb0263893daf"></a>
### Description

It returns lowercases of str.

The str argument data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If str is NULL, the result is also NULL.

The return type is the same datatype as the str argument.

<a id="5b43e4f9183709ff"></a>
### Example

```
gSQL> SELECT LOWER( 'SPRING' ) AS RESULT FROM DUAL;
RESULT
------
spring
1 row selected.
```

<a id="4953f4d79a5daf47"></a>
## LPAD

<a id="d5cba219ebd7fb8a"></a>
### Syntax

```
LPAD( str, length, [, fill] )
```

<a id="64ad15e5a041faff"></a>
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

<a id="09002ecd8fe1bef3"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="5986387da9662672"></a>
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

<a id="4ca546bc2c3ffe04"></a>
## LTRIM

<a id="c673f680ce483ca7"></a>
### Syntax

```
LTRIM( trim_source [, trim_character ] )
```

<a id="9bfd4c0b428cd15f"></a>
### Description

It removes the matching characters by comparing from the left side of trim_character in trim_source until the matching character does not exist. Then it returns the result.

The data type of trim_character and trim_source arguments can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, and a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If any of trim_character, trim_source is NULL, the result is NULL.  
If trim_character is omitted, a single blank space (' ') is specified by default.

The following table describes the result types.

**Result type of LTRIM**

<a id="1f10ef0149f5a4c0"></a>
| trim_source, trim_character type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="e1219bf8ec72887e"></a>
### Example

```
gSQL> SELECT LTRIM( '_____LTRIM', '_' ) AS RESULT FROM DUAL;
RESULT
------
LTRIM 
1 row selected.
```

<a id="2bfd71ba988d3af0"></a>
## MAX

<a id="a23b74acc2ede211"></a>
### Syntax

```
MAX( [ ALL | DISTINCT ] expr )
```

<a id="2bd94eec05a6d371"></a>
### Description

It is an aggregate function and the maximum value among rows' exprs is obtained.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

MAX function returns the same result without being affected by the ALL and DISTINCT.

<a id="40766b147f92218c"></a>
### Example

```
gSQL> SELECT MAX(c1) FROM t1;

MAX(C1)
-------
      3

1 row selected.
```

<a id="a3e909d4bfdd0040"></a>
## MIN

<a id="bae1e265a18da341"></a>
### Syntax

```
MIN( [ ALL | DISTINCT ] expr )
```

<a id="a68dfe11dbdc7ba2"></a>
### Description

It is an aggregate function and the minimum value among rows' exprs is obtained.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

MIN function returns the same result without being affected by the ALL and DISTINCT.

<a id="07fde65949d0d171"></a>
### Example

```
gSQL> SELECT MIN(c1) FROM t1;

MIN(C1)
-------
      1

1 row selected.
```

<a id="67c30bf83b6ff728"></a>
## MOD

<a id="105226d30b68c68d"></a>
### Syntax

```
MOD( num1, num2 )
```

<a id="26101b69abac3fee"></a>
### Description

It divides num1 by num2, and returns the remainder.  

The num1 argument and num2 argument can be a numeric data type.  
If num2 is 0, an error is returned.  
If the num1 argument or num2 argument is NULL, then NULL is returned.

<a id="d7489858e8ce893f"></a>
### Example

```
gSQL> SELECT MOD(5, 4) AS RESULT1, MOD(-5, 4) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1      -1
1 row selected.
```

<a id="31dbabf1b27367bc"></a>
## MONTHS_BETWEEN

<a id="b7e07b4212a8b3f1"></a>
### Syntax

```
MONTHS_BETWEEN( date1, date2 )
```

<a id="552f62dc6425bd05"></a>
### Description

MONTHS_BETWEEN returns the number of months of which days between date2 and date1 are divided by 31.

If date1 or date2 is NULL, then the result is also NULL.  
The date1 argument and date2 argument can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE type.

The result type is NUMBER.

> If the same date (e.g. 2014-01-15 and 2014-02-15), or the last day of the month (e.g. 2014-08-31 and 2014-09-30) is included both in date1 and date2, then it returns the integer result regardless of the agreement of timestamp section (if it exists).

<a id="90947aad706f95f1"></a>
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

<a id="b3220c1cea364dc9"></a>
## NEXT_DAY

<a id="2290cda68044283f"></a>
### Syntax

```
NEXT_DAY( date, day )
```

<a id="eb237ed4acef7cac"></a>
### Description

It obtains a date of the day (day of week) which comes first after the given date (an argument).

The second day argument can be a string or a number which indicates the day.  
• String: SUNDAY ~ SATURDAY  or SUN ~ SAT  
• Number: 1 (sunday) ~ 7 (saturday)  

If any of the input argument is NULL, the result is also NULL.

The return type is always DATE regardless of the input type of the date.   
The hour, minute and second of the result value returns the same hour, minute and second of the input argument date.

<a id="78a96a53eee1983b"></a>
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

<a id="09b72a3c73f75661"></a>
## NEXTVAL

<a id="02735b9f99af5d1e"></a>
### Syntax

```
seq_name.NEXTVAL
NEXTVAL( seq_name )
NEXT VALUE FOR seq_name
```

<a id="480d07f34c703f91"></a>
### Description

It obtains the next value of the sequence object.

<a id="2fba258b959e8f7e"></a>
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

<a id="f710d1c714f3d249"></a>
## NULLIF

<a id="6f3930e043664a15"></a>
### Syntax

```
NULLIF( expr1, expr2 )
```

<a id="df26fe5029922730"></a>
### Description

If expr1 is equal to expr2, it returns NULL. If they are not equal it returns expr1 which is the first argument.

If the data types of expr1 and expr2 are different, the result type is determined by [Result Type Combination Rule](11-sql-elements.md#ea5401033b086287).

NULLIF can be expressed by using CASE as follows.

- NULLIF( expr1, expr2 )

```
CASE WHEN expr1 = expr2 THEN NULL 
       ELSE expr1 
  END
```

<a id="f38c659ba6f79995"></a>
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

<a id="cf00732cb6ecb9ff"></a>
## NUMTODSINTERVAL

<a id="4cbbe60805d3f49d"></a>
### Syntax

```
NUMTODSINTERVAL( num, interval_indicator )
```

<a id="bd47a79a4cda45e6"></a>
### Description

It converts the number in interval_indicator unit to interval day to second type, then returns it.

The argument *number* is a numeric type.

The argument interval_indicator is a character type, like CHAR or VARCHAR, and it should be one of 'DAY', 'HOUR', 'MINUTE', 'SECOND' which is case insensitive.

If any argument is NULL, then NULL is returned as a result.

interval day(6) to second(6) type is returned as a result, and a user can not arbitrarily modify the precision. If the leading precision of the converted result exceeds the default precision, then an error is returned. If the fraction precision exceeds the default precision, then the rounded value is returned as a result.

<a id="f1f54084e64d3176"></a>
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

<a id="4148dcb310152811"></a>
## NUMTOYMINTERVAL

<a id="876b760d479f2584"></a>
### Syntax

```
NUMTOYMINTERVAL( num, interval_indicator )
```

<a id="25dbd85a8262ebf7"></a>
### Description

It converts the number in interval_indicator unit to interval year to month type, then returns it.

The argument *number* is a numeric type.

The argument interval_indicator is a character type, like CHAR or VARCHAR, and it should be one of 'YEAR', 'MONTH' which is case insensitive.

If any argument is NULL, then NULL is returned as a result.

interval year(6) to month type is returned as a result, and a user can not arbitrarily modify the precision. If the leading precision of the converted result exceeds the default precision, then an error is returned.

<a id="a373a4459b2e5951"></a>
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

<a id="cd33dd220c45d2a3"></a>
## NVL

<a id="8657a45290fec686"></a>
### Syntax

```
NVL( expr1, expr2 )
```

<a id="1e6951b8c571297b"></a>
### Description

If expr1 is not NULL, then it returns expr1. If expr1 is NULL, it returns expr2.

The result type is determined according to the data type of expr1.  
If NULL is described in expr1, then the result type is determined according to the data type of expr2.   
If the data type of expr1 is a character type and a numeric type then it becomes the type including the range of expr1 and expr2 each.  
If the data type of both expr1 and expr2 is CHAR type, then the result type is VARCHAR.

<a id="fb8ec30ae9680564"></a>
### Example

```
gSQL> SELECT I1, NVL( I1, 0 ) FROM T1;
  I1 NVL( I1, 0 )
---- ------------
   1            1
null            0
2 rows selected.
```

<a id="b8f0e8176b82c161"></a>
## NVL2

<a id="40c86854b3ff46d9"></a>
### Syntax

```
NVL2( expr1, expr2, expr3 )
```

<a id="29ba876f26e1cb2f"></a>
### Description

If expr1 is not null, then it returns expr2. If expr1 is NULL, it returns expr3.

The result type is determined according to the data type of expr2.   
If NULL is described in expr2, then the result type is determined according to the data type of expr3.  
If the data type of expr2 is a character type and a numeric type then it becomes the type including the range of expr2 and expr3 each.  
If the data type of both expr2 and expr3 is CHAR type, then the result type is VARCHAR.

<a id="337c5ddf3c5e0634"></a>
### Example

```
gSQL> SELECT I1, NVL2( I1, I1 * 1000, 0 ) FROM T1;
  I1 NVL2( I1, I1 * 1000, 0 )
---- ------------------------
   1                     1000
null                        0
2 rows selected.
```

<a id="e589ba3d27704d5c"></a>
## OCTET_LENGTH

<a id="fb0d8f61e42e9965"></a>
### Syntax

```
OCTET_LENGTH( str )  

BYTE_LENGTH( str )     

LENGTHB( str )
```

<a id="10c80181a2a638f9"></a>
### Description

It returns the number of bytes in str.

The str argument data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONGVARYING.

If the str data type is CHARACTER, the white spaces are included in the calculation.  
If str is NULL, the result is also NULL.

It is an alias of [BYTE_LENGTH](#22909c13767b86f4) and [LENGTHB](#ef7333f082e22889).

<a id="3b36e44790505c33"></a>
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

<a id="f0952de74da019d4"></a>
## OVERLAY

<a id="04564ab3e3cc1a60"></a>
### Syntax

```
OVERLAY( str1 PLACING str2 FROM start_position  [ FOR string_length ] )
```

<a id="f8cbc47ba0529989"></a>
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

For more information, refer to [SUBSTRING](#4297de45ecd34865).

The following table describes the result types.

**Result type of OVERLAY**

<a id="4804f692339631c8"></a>
| str1, str2 types | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="1e9a36d5a3b7abc7"></a>
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

<a id="5c6be669bdf134e8"></a>
## PHYSICAL_LENGTH

<a id="bf9e07e50dee57ea"></a>
### Syntax

```
PHYSICAL_LENGTH( expr )
```

<a id="cf9eee25f44c2f13"></a>
### Description

PHYSICAL_LENGTH returns the number of internal expression information bytes in expr.

The expr argument can be any data type.

If an input argument is NULL, then the result is 0.

<a id="bb2402cd68e9d4fa"></a>
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

<a id="323b9865911f0d7c"></a>
## PI

<a id="335422afd18dcc8e"></a>
### Syntax

```
PI()
```

<a id="e7bc0dfb53d96169"></a>
### Description

It returns "π" constant.

<a id="708ab66095db116b"></a>
### Example

```
gSQL> SELECT PI() AS RESULT FROM DUAL;
              RESULT
--------------------
3.141592653589793E+0
1 row selected.
```

<a id="c341698defe4d875"></a>
## POSITION

<a id="9bcef150ae4d72a4"></a>
### Syntax

```
POSITION( str1 IN str2 )
```

<a id="f877b17b045f387a"></a>
### Description

It searches for the first str1 within str2, then returns its location.

The data type of str1 argument and str2 argument can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If str1 can not be found within str2, the return value is 0.  
If str1 is found within str2, the position of str1 is returned, and the return value starts from 1.  
The returned position value is calculated in character unit (not in byte unit).  
If str1 or str2 is NULL, the return value is also NULL.

<a id="fe799d702644f6ae"></a>
### Example

```
gSQL> SELECT POSITION( 'CHAR' IN 'LONG CHAR 2000' ) AS RESULT FROM DUAL;
RESULT
------
     6
1 row selected.
```

<a id="2b20871069f8a87d"></a>
## POWER

<a id="f7bb8fe17ecd3b05"></a>
### Syntax

```
POWER( num1, num2 )
```

<a id="b5f095de5c71b743"></a>
### Description

It squares num1 to num2, and returns the result.

The num1 argument and num2 argument can be a numeric data type.  

If num1 is a negative number, num2 should be an integer.  
If num1 or num2 is NULL, the result is also NULL.

<a id="1788d7e48eebf8e6"></a>
### Example

```
gSQL> SELECT POWER( 2, 3 ) AS RESULT FROM DUAL;
RESULT
------
     8
1 row selected.
```

<a id="afb88242e6712a07"></a>
## RADIANS

<a id="46a06209589ff032"></a>
### Syntax

```
RADIANS( degrees )
```

<a id="be5f1fdbde45aac2"></a>
### Description

It returns the radians of degrees.  

The degrees argument can be a numeric data type.  
If the degrees argument is NULL, then NULL is returned.

<a id="10c2ac63bfd2b5af"></a>
### Example

```
gSQL> SELECT RADIANS( 180 ) AS RESULT FROM DUAL;
          RESULT
----------------
3.14159265358979
1 row selected.
```

<a id="0d76ef6f5bce0ec3"></a>
## RANDOM

<a id="e4602a82c04f2e3a"></a>
### Syntax

```
RANDOM( min, max )
```

<a id="4eccc7e846c01310"></a>
### Description

It returns a random value in the range above min and below max.  

The min argument and max argument can be a numeric data type.  
If either min argument or the max argument is NULL, then NULL is returned.

<a id="214731d78a2ceced"></a>
### Example

```
gSQL> SELECT RANDOM( 1, 100 ) AS RESULT FROM DUAL;
          RESULT
----------------
34.1870528003201
1 row selected.
```

<a id="ae042b77814a18d9"></a>
## REPEAT

<a id="4630f6b14623e3e1"></a>
### Syntax

```
REPEAT( str, num )
```

<a id="dfa581b6a1759b7e"></a>
### Description

The string repeats str as many times as specified in num, and returns the result.

The str argument can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

The num argument can be a numeric data type.

If either str or num is NULL, the result is also NULL.  
If num is 0 or a negative number, the result is also NULL.

The following table describes the result types.

**Result type of REPEAT**

<a id="b7c741b27ccc6b3b"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="376d01ccc7af1ef0"></a>
### Example

```
gSQL> SELECT REPEAT( 'ab', 3 ) AS RESULT FROM DUAL;
RESULT
------
ababab
1 row selected.
```

<a id="75fc92b5e0800bc4"></a>
## REPLACE

<a id="718c940322851790"></a>
### Syntax

```
REPLACE( str, from, to )
```

<a id="0b8db3e2dff19912"></a>
### Description

It replaces all *from* strings in str string with *to* strings, and returns the result.

The str argument, the from argument, and the to argument can be character data types such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If str is NULL, the result is also NULL.  
If from is NULL, the str is returned without replacement.  
If to value is omitted or NULL, the str value of which from is removed is returned.

The following table describes the result types.

**Result type of REPLACE**

<a id="0b561982fb979ff6"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="fee0a438d59a1b08"></a>
### Example

```
gSQL> SELECT REPLACE( 'HI GLIESE', 'HI', 'HELLO' ) AS RESULT FROM DUAL;
RESULT      
------------
HELLO GLIESE
1 row selected.
```

<a id="627c7154e9d81951"></a>
## REVERSE

<a id="acc14a0fcea41174"></a>
### Syntax

```
REVERSE( str )
```

<a id="75187c72c6589195"></a>
### Description

REVERSE returns characters of str in reverse order.

The str argument can be types that are convertible to a character string type or a binary string type.  
A character string type is performed in a character unit, and a binary string type can be performed in a byte unit.

If str is NULL, then it returns NULL.

The following table describes the arguments and result types.

**Argument and result type of REVERSE**

<a id="813a160290772698"></a>
| str | Result type |
| --- | --- |
| CHAR | CHAR |
| VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY | BINARY |
| VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="668b1f0938bf7891"></a>
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

<a id="c827410b3b659bc7"></a>
## ROUND( number )

<a id="7b82d8f56db29a4f"></a>
### Syntax

```
ROUND( num [, scale ] )
```

<a id="858552db879a9f96"></a>
### Description

It rounds off num based on scale, and returns the result.

The num argument and scale argument can be numeric data types.

If scale is omitted, the scale becomes 0 and is executed as if it is ROUND(num, 0).  
If scale is a positive number, it is rounded off based on the number of right digit of the decimal point. If scale is a negative number, it is rounded off based on the number of left digit of the decimal point.  

If either num argument or the scale argument is NULL, then NULL is returned.

<a id="7642a2adcf3ace92"></a>
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

<a id="21a63c30ce48090d"></a>
## ROUND( date )

<a id="1ba160a607097669"></a>
### Syntax

```
ROUND( date [ , fmt ] )
```

<a id="5ea2da16bd699186"></a>
### Description

It rounds off the date in the specified fmt unit, and returns the result.

The data type of date argument can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.   
The fmt argument can be a character type such as CHARACTER, CHARACTER VARYING.   
If either date argument or the fmt argument is NULL, then NULL is returned.  

The result type is always DATE regardless of the date argument data type.

If fmt is omitted, the default is DAY.  
The following table describes the available format strings.

**Available format sting of fmt**

<a id="007cb908e992465f"></a>
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

<a id="1b262fe727ffae9b"></a>
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

<a id="5b10c3e66ad77591"></a>
## ROWID_GRID_BLOCK_ID

<a id="dd37099ce6a72cac"></a>
### Syntax

```
ROWID_GRID_BLOCK_ID( rowid )
```

<a id="74eff0fe86d90a10"></a>
### Description

It returns the GRID block ID.

> It is a valid information in a cluster system.

<a id="d0e72e726fc698d7"></a>
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

<a id="a6f6189516b10f49"></a>
## ROWID_GRID_BLOCK_SEQ

<a id="dcfbae121e085deb"></a>
### Syntax

```
ROWID_GRID_BLOCK_SEQ( rowid )
```

<a id="cb44dac585b9aca2"></a>
### Description

It returns the GRID block sequence.

> It is a valid information in a cluster system.

<a id="042d585bf0e4c9b2"></a>
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

<a id="811f229ddda8eb43"></a>
## ROWID_MEMBER_ID

<a id="fb0d96e6816291f5"></a>
### Syntax

```
ROWID_MEMBER_ID( rowid )
```

<a id="b482ebd8e398b9ea"></a>
### Description

It returns the member ID.

> It is a valid information in a cluster system.

<a id="a8b39f83be271fa3"></a>
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

<a id="8fb5f800a965ccbd"></a>
## ROWID_OBJECT_ID

<a id="1399ec66649a75cf"></a>
### Syntax

```
ROWID_OBJECT_ID( rowid )
```

<a id="85d0187443474e54"></a>
### Description

It returns the object ID.

> It is an invalid information in a cluster system.

<a id="8b6a22f8eb2ee7a3"></a>
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

<a id="0686d4005f804804"></a>
## ROWID_PAGE_ID

<a id="9fa9e53175d764de"></a>
### Syntax

```
ROWID_PAGE_ID( rowid )
```

<a id="9dab848f2ab1b748"></a>
### Description

It returns the page ID.

> It is an invalid information in a cluster system.

<a id="ea189c9787d1adca"></a>
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

<a id="534715e0effb9b0f"></a>
## ROWID_ROW_NUMBER

<a id="f274cd90b95a276c"></a>
### Syntax

```
ROWID_ROW_NUMBER( rowid )
```

<a id="ea7b758acd02b85b"></a>
### Description

It returns the row number.

> It is an invalid information in a cluster system.

<a id="1118d876cd2ab802"></a>
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

<a id="0b78a959e1a8c435"></a>
## ROWID_SHARD_ID

<a id="ce15c73625a48ea7"></a>
### Syntax

```
ROWID_SHARD_ID( rowid )
```

<a id="1f3f5009f525a6f1"></a>
### Description

It returns the shard ID.

> It is a valid information in a cluster system.

<a id="c37981c420dfac43"></a>
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

<a id="fca80a825f8ee6d3"></a>
## ROWID_TABLESPACE_ID

<a id="aad59a1036edaa87"></a>
### Syntax

```
ROWID_TABLESPACE_ID( rowid )
```

<a id="e2f3927f5c410c5a"></a>
### Description

It returns the tablespace ID.

> It is an invalid information in a cluster system.

<a id="e24989a21387073a"></a>
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

<a id="5ade016384c7cd70"></a>
## ROWNUM

<a id="40b3741ed92c7eff"></a>
### Syntax

```
ROWNUM
```

<a id="22a752420e5d97b0"></a>
### Description

It sequentially allocates a number starting from 1 to rows which satisfy the WHERE condition.

It allows using ROWNUM in WHERE clause for the compatibility with Oracle.

However, to restrict the number of the query results, it is recommended to use [offset limit clause](20-sql-references-h-z.md#ba0c692a791aafab) (the SQL standard) as follows.

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

<a id="40b1109f6c403b93"></a>
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

<a id="38e5d0d4ee94236b"></a>
## RPAD

<a id="7035ba0fe40b31fd"></a>
### Syntax

```
RPAD( str, length, [, fill] )
```

<a id="1c50a6bd65fc9575"></a>
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

<a id="5da589ee82827953"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="ef9b0ff563626ff1"></a>
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

<a id="25f79d3a84592309"></a>
## RTRIM

<a id="3efbed185fc7589a"></a>
### Syntax

```
RTRIM( trim_source [, trim_character ] )
```

<a id="9675c8e45ea5091a"></a>
### Description

It removes the matching characters by comparing from the right side of trim_character in trim_source until the matching character does not exist. Then it returns the result.

The data type of trim_character and trim_source arguments can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING or a binary data type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If any of trim_character, trim_source is NULL, the result is NULL.  
If trim_character is omitted, a single blank space (' ') is specified by default.

The following table describes the result types.

**Result type of RTRIM**

<a id="4147529eedd4a086"></a>
| trim_source type, trim_character type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="932d2a79946299c5"></a>
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

<a id="8867be0ffaec5ffc"></a>
## SESSION_ID

<a id="cafe242ebbcf4385"></a>
### Syntax

```
SESSION_ID()
```

<a id="f35868b0ace70f86"></a>
### Description

It obtains the current session ID.

<a id="7fbacd3d178ec8ca"></a>
### Example

```
gSQL> SELECT SESSION_ID() FROM dual;

SESSION_ID()
------------
           4

1 row selected.
```

<a id="7bae115698af570f"></a>
## SESSION_SERIAL

<a id="03f23862c57062f4"></a>
### Syntax

```
SESSION_SERIAL()
```

<a id="3f276f00628f6f7d"></a>
### Description

It obtains the serial number of current session.

<a id="dc0eaa5f0070af87"></a>
### Example

```
gSQL> SELECT SESSION_SERIAL() FROM dual;

SESSION_SERIAL()
----------------
              16

1 row selected.
```

<a id="fa9578611b565dd2"></a>
## SESSION_USER

<a id="c6a3c0eb996330d2"></a>
### Syntax

```
SESSION_USER[()]
```

<a id="f5a73fa07a8c452f"></a>
### Description

It returns the session user.

The user information is managed in three types as follows.

- Logon user: It is a user who performed login, and it is maintained until the connection is closed.
- Session user: It is as same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: It is generally as same as the session user, but it is temporarily changed internally in system to control access when using the PSM, view.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="5b0baa38720fb873"></a>
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

<a id="af65f89c5357239d"></a>
## SHARD_GROUP_ID

<a id="5a4d8e81a31fb009"></a>
### Syntax

```
SHARD_GROUP_ID( table_name, shard_key_value [, ... ] )
```

<a id="0da3ad54e3402831"></a>
### Description

It returns the group ID managing the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is NATIVE_BIGINT.

> It is a valid information in a cluster system.

<a id="aa29a23935602d5f"></a>
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

<a id="a947644a8bf9562a"></a>
## SHARD_GROUP_NAME

<a id="92d627679520a55e"></a>
### Syntax

```
SHARD_GROUP_NAME( table_name, shard_key_value [, ... ] )
```

<a id="122658dc2380d0e0"></a>
### Description

It returns the group NAME managing the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is VARCHAR.

> It is a valid information in a cluster system.

<a id="39cec9b0c60c27f0"></a>
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

<a id="7ddd3a6954bc253f"></a>
## SHARD_ID

<a id="9f3172c69e7b7c8c"></a>
### Syntax

```
SHARD_ID( table_name, shard_key_value [, ... ] )
```

<a id="bce77396163e9cd6"></a>
### Description

It returns the ID for the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is NATIVE_BIGINT.

> It is a valid information in a cluster system.

<a id="50b2bd6f772e97fe"></a>
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

<a id="eaab3c027e87528e"></a>
## SHARD_NAME

<a id="dce312f39c44cb3b"></a>
### Syntax

```
SHARD_NAME( table_name, shard_key_value [, ... ] )
```

<a id="5d26a41960a79083"></a>
### Description

It returns the NAME for the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is VARCHAR.

> It is a valid information in a cluster system.

<a id="8af2dd0e161a2370"></a>
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

<a id="152fa9fe3a6d871f"></a>
## SHIFT_LEFT

<a id="5f9ba52425a35602"></a>
### Syntax

```
SHIFT_LEFT( num, cnt )
```

<a id="c5af2490971f9140"></a>
### Description

It moves num to the left as many as cnt bits, and returns the movement values.

The data type of input num argument and cnt argument can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or the type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type,  the decimal point is truncated.

cnt is masked with 6 bit, and it is processed to a value in the range within 6 bit.

If either num or cnt is NULL, then NULL is returned.

The result type is NATIVE_BIGINT.

<a id="073c5f0335df90e6"></a>
### Example

```
gSQL> SELECT SHIFT_LEFT(1, 3) FROM DUAL;
SHIFT_LEFT(1, 3)
----------------
               8
1 row selected.
```

<a id="cb0c5e4625362a36"></a>
## SHIFT_RIGHT

<a id="181cbd2d769ea556"></a>
### Syntax

```
SHIFT_RIGHT( num, cnt )
```

<a id="ea9c2e5cc31bae1a"></a>
### Description

It moves num to the right as many as cnt bits, and returns the movement values.

The data type of input num argument and cnt argument can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or the type which can be converted to NATIVE_BIGINT.   
When converting to NATIVE_BIGINT type, the decimal point is truncated.

cnt is masked with 6 bit, and it is processed to a value in the range within 6 bit.

If either num or cnt is NULL, then NULL is returned.

The result type is NATIVE_BIGINT.

<a id="ee4b19722adef9ce"></a>
### Example

```
gSQL> SELECT SHIFT_RIGHT(8, 3) FROM DUAL;
SHIFT_RIGHT(8, 3)
-----------------
                1
1 row selected.
```

<a id="9f8daacc2b306294"></a>
## SIGN

<a id="40cc6dc03714fcab"></a>
### Syntax

```
SIGN( num )
```

<a id="a6f9c001a2bc858f"></a>
### Description

It returns the sign of num.

The num argument can be a numeric data type.

The return value is as follows.   
• If num < 0,  -1 is returned.  
• If num = 0, 0 is returned.  
• If num > 0, 1 is returned.

If num is NULL, then NULL is returned.

<a id="042fc5fbd1d694dd"></a>
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

<a id="66300bf3448dd0eb"></a>
## SIN

<a id="390eeaac3514366b"></a>
### Syntax

```
SIN( num )
```

<a id="21efbcf23d27b9e5"></a>
### Description

It returns the sine value of num.  
If num is NULL, then NULL is returned.

<a id="50783bd25f7caac1"></a>
### Example

```
gSQL> SELECT SIN( 0 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="ad9b101d46356e19"></a>
## SPLIT_PART

<a id="08d6f3e48357274a"></a>
### Syntax

```
SPLIT_PART( string, delimiter, field )
```

<a id="12e6da06bd630a48"></a>
### Description

It returns a character string of the field by specifying a character as delimiter within a string.

The data type of string argument and delimiter argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

The field argument can be a numeric data type.

If any of string, delimiter, field is NULL, the result is also NULL.  
The value of field should be a numeric value above 1, and if it is 0 or a negative number, an error is returned.

The following table describes the result types.

**Result type of SPLIT_PART**

<a id="eaa04524d6e0373d"></a>
| string type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="c4934d04606b4b0f"></a>
### Example

```
gSQL> SELECT SPLIT_PART( 'AB;CD;EF;GH', ';', 3  ) AS RESULT FROM DUAL;
RESULT
------
EF    
1 row selected.
```

<a id="eed7ba2ff4e9dc72"></a>
## SQRT

<a id="23f5228a344f1a47"></a>
### Syntax

```
SQRT( num )
```

<a id="6099026ad34224df"></a>
### Description

It returns the square root of num.

The num argument can be a numeric type, and it should not be a negative number, but above 0.  
If the num argument is NULL, then NULL is returned.

<a id="73398d19dba5a29f"></a>
### Example

```
gSQL> SELECT SQRT( 9 ) AS RESULT FROM DUAL;
RESULT
------
     3
1 row selected.
```

<a id="30502dc040b5c01f"></a>
## STATEMENT_DATE

<a id="4916317badaddf61"></a>
### Syntax

```
STATEMENT_DATE()
CURRENT_DATE [()]
```

<a id="08c7987e5a708ca5"></a>
### Description

The current date(DATE type) value is obtained.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="61d1228739dfefec"></a>
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

<a id="9cf14acfdfc39b82"></a>
## STATEMENT_LOCALTIME

<a id="1c967e7dd9e48bd2"></a>
### Syntax

```
STATEMENT_LOCALTIME()
LOCALTIME [()]
```

<a id="26e8eb6e90bf01f5"></a>
### Description

The current TIME WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.  
• TATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="437a5c08ad7f2282"></a>
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

<a id="855933dbcf28a3c7"></a>
## STATEMENT_LOCALTIMESTAMP

<a id="be2593239556eb0e"></a>
### Syntax

```
STATEMENT_LOCALTIMESTAMP()
LOCALTIMESTAMP [()]
```

<a id="e80ed2f34373b15f"></a>
### Description

The current TIMESTAMP WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_LOCALTIMESTAMP(): All timestamp values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="f15e236fa56c83e7"></a>
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

<a id="b2f1dcad4d40a2f1"></a>
## STATEMENT_TIME

<a id="03d1b531667a4c4f"></a>
### Syntax

```
STATEMENT_TIME()
CURRENT_TIME [()]
```

<a id="fa653b9d9834713a"></a>
### Description

The current TIME WITH TIME ZONE type value is obtained.

CURRENT_TIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• STATEMENT_TIME(): All time values in an SQL statement are same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="5774dcf5f8502f44"></a>
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

<a id="1b1ab52273ec6e21"></a>
## STATEMENT_TIMESTAMP

<a id="5b7321c39246cc30"></a>
### Syntax

```
STATEMENT_TIMESTAMP()
CURRENT_TIMESTAMP [()]
```

<a id="49aec9c1cdb110e1"></a>
### Description

The current TIMESTAMP WITH TIME ZONE type value is obtained.

CURRENT_TIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_TIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_TIMESTAMP(): All timestamp values in an SQL statement are same.  
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="e36ee78be9a7e11a"></a>
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

<a id="ab1e7a9d4f179328"></a>
## STATEMENT_VIEW_SCN

<a id="8b7589c7b96718d9"></a>
### Syntax

```
STATEMENT_VIEW_SCN()
```

<a id="c09e943bb2a8689d"></a>
### Description

It obtains VIEW SCN of the current STATEMENT.

<a id="a14da9a4f860a0de"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN() FROM dual;

STATEMENT_VIEW_SCN()
--------------------
17697.658.17880     

1 row selected.
```

<a id="ee957179afa6713a"></a>
## STATEMENT_VIEW_SCN_DCN

<a id="e827207937ba1d14"></a>
### Syntax

```
STATEMENT_VIEW_SCN_DCN()
```

<a id="c301beee4ad111ee"></a>
### Description

It obtains the Domain Change Number (DCN) value of the current STATEMENT's VIEW SCN.

<a id="e516e82a462986fd"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_DCN() FROM dual;

STATEMENT_VIEW_SCN_DCN()
------------------------
                     658

1 row selected.
```

<a id="68ce6aa95235112d"></a>
## STATEMENT_VIEW_SCN_GCN

<a id="8427855feafea6bf"></a>
### Syntax

```
STATEMENT_VIEW_SCN_GCN()
```

<a id="da86fa6bb7b41ded"></a>
### Description

It obtains the Global Change Number (GCN) value of the current STATEMENT's VIEW SCN.

<a id="dd96c027c4f86fd2"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_GCN() FROM dual;

STATEMENT_VIEW_SCN_GCN()
------------------------
                   17697

1 row selected.
```

<a id="cafbf3987dcb0db5"></a>
## STATEMENT_VIEW_SCN_LCN

<a id="024927a6aa23fe87"></a>
### Syntax

```
STATEMENT_VIEW_SCN_LCN()
```

<a id="ea224df86dd2f820"></a>
### Description

It obtains the Local Change Number (LCN) value of the current STATEMENT's VIEW SCN.

<a id="e5f82de1e4e4f015"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_LCN() FROM dual;

STATEMENT_VIEW_SCN_LCN()
------------------------
                   17880

1 row selected.
```

<a id="b69e3ade827e1705"></a>
## STDDEV

<a id="b4dba7b850283efc"></a>
### Syntax

```
STDDEV( [ ALL | DISTINCT ] expr )
```

<a id="4ec6bc2715f6b84d"></a>
### Description

It is an aggregation function, and it obtains the standard deviation of an expr set.

If ALL is specified, this function is performed for all values. If DISTINCT is specified, this function is performed for the values of which the duplicates were deleted from. If it is not specified, it is processed as if ALL is apecified.

If the number of expr sets except for NULL after deleting the duplicates by using DISTINCT is one, then it returns 0 like as [VARIANCE](#c80a723029120adb).

The following table describes the arguments and result types.

**Argument and result type of STDDEV**

<a id="32eb954bcf114c00"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

GOLDILOCKS gets the standard deviation as follows.  
　• If the number of expr sets is 1, then it returns 0.  
　• If the number of expr sets is bigger than 1, it returns the value of [STDDEV_SAMP( expr )](#447c9e328f1a0472).

> The standard deviation is a positive square root of a variance, and it is obtained calculating the square root of the variance. In other words, the STDDEV function is as same as the square root of [VARIANCE](#c80a723029120adb) function.  
>   
> STDDEV( [ ALL ] expr )  
>  = SQRT( VARIANCE( [ ALL ] expr ) )  
>   
> STDDEV( DISTINCT expr )  
>  = SQRT( VARIANCE( DISTINCT expr ) )

<a id="13fcb3db17b9a300"></a>
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

<a id="2be3066d0dff3e98"></a>
## STDDEV_POP

<a id="6f0e12f6aa0936ac"></a>
### Syntax

```
STDDEV_POP( expr )
```

<a id="51766d8e39e4d4de"></a>
### Description

It is an aggregation function, and it obtains the population standard deviation of an expr set. If the number of expr sets except for NULL is one, then it returns 0.

The following table describes the arguments and result types.

**Argument and result type of STDDEV_POP**

<a id="5cc3ea4f5d937cd1"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The population standard deviation is a positive square root of a population variance, and it is obtained by calculating the square root of the population variance. In other words, the STDDEV_POP function is as same as the square root of [VAR_POP](#fe67b3bcc540e1b1) function.  
>   
> STDDEV_POP( expr )  
>  = SQRT( VAR_POP( expr ) )

<a id="add4c1e1b33f2299"></a>
### Example

```
gSQL> SELECT STDDEV_POP(c1) FROM t1;

 STDDEV_POP(C1)
---------------
10.283968105746

1 row selected.
```

<a id="447c9e328f1a0472"></a>
## STDDEV_SAMP

<a id="0d0063f6435d8847"></a>
### Syntax

```
STDDEV_SAMP( expr )
```

<a id="6661e36cb3e35d05"></a>
### Description

It is an aggregation function, and it obtains the sample standard deviation of an expr set. If the number of expr sets except for NULL is one, then it returns NULL.

The following table describes the arguments and result types.

**Argument and result type of STDDEV_SAMP**

<a id="080b8677d26fa459"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The sample standard deviation is a positive square root of a sample variance, and it is obtained by calculating the square root of the sample variance. In other words, the STDDEV_SAMP function is as same as the square root of [VAR_SAMP](#a6e0fa57cdf03a12) function.  
>   
> STDDEV_SAMP( expr )  
>  = SQRT( VAR_SAMP( expr ) )

<a id="dfca2174fb16f1a6"></a>
### Example

```
gSQL> SELECT STDDEV_SAMP(c1) FROM t1;

 STDDEV_SAMP(C1)
----------------
11.4978258814438

1 row selected.
```

<a id="7592eb42043c961b"></a>
## SUBSTR

<a id="ee8698e0c8c74e06"></a>
### Syntax

```
SUBSTR( str FROM start_position [ FOR string_length ] )
SUBSTR( str, start_position [ , string_length ] )
```

<a id="8734612787ceff38"></a>
### Description

It is an alias of [SUBSTRING](#4297de45ecd34865).

<a id="036e1b8f5a11709e"></a>
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

<a id="6975e74424e7e719"></a>
## SUBSTRB

<a id="8ed32b6646d17eb8"></a>
### Syntax

```
SUBSTRB( str, start_position [ , string_length ] )
```

<a id="a1b4ba258ea9cad7"></a>
### Description

It extracts characters which are within string_length range from start_position, and returns the result for str.

This function is as same as [SUBSTRING](#4297de45ecd34865) function, except that start_position and string_length of the SUBSTR function are calculated in byte units.

<a id="e0b68f83efa6c233"></a>
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

<a id="4297de45ecd34865"></a>
## SUBSTRING

<a id="6ef173b83f11f0ce"></a>
### Syntax

```
SUBSTRING( str FROM start_position [ FOR string_length ] )  
SUBSTRING( str, start_position [ , string_length ] )
```

<a id="198d3502e5958654"></a>
### Description

It extracts characters which are within string_length range from start_position, and returns the result for str.

The  str argument data type can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary data type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

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

It is an alias of [SUBSTR](#7592eb42043c961b).  
For more information, refer to [SUBSTRB](#6975e74424e7e719).

The following table describes the result types.

**Result type of SUBSTRING**

<a id="2cc93b35e62e8eb8"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="b38b02c63900c5ef"></a>
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

<a id="488beb2e8ce7f406"></a>
## SUM

<a id="40eaf163e6623132"></a>
### Syntax

```
SUM( [ ALL | DISTINCT ] expr )
```

<a id="e365d033f145de42"></a>
### Description

It is an aggregate function and the sum of expr value is obtained.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

<a id="3f729216e2d984c1"></a>
### Example

```
gSQL> SELECT SUM(c1) FROM t1;

SUM(C1)
-------
      6

1 row selected.
```

<a id="669beb3891433bc8"></a>
## SYSDATE

<a id="f04efe5f5922a871"></a>
### Syntax

```
SYSDATE
```

<a id="40059453499e09ce"></a>
### Description

It obtains the current DATE type value based on the OS time of the database server.

<a id="677b038217907b14"></a>
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

<a id="b5fd70342575fd69"></a>
## SYS_EXTRACT_UTC

<a id="21687729c993f2fd"></a>
### Syntax

```
SYS_EXTRACT_UTC( datetime_with_timezone )
```

<a id="5d04832409a231d3"></a>
### Description

It returns the UTC (Coordinated Universal Time—formerly Greenwich Mean Time) value.  
If the timezone is not specified, it is calculated as session time zone.

The data type of an input argument can be time, time with time zone, timestamp, timestamp with time zone.  
The result type is time or timestamp type.

<a id="24803b02ebe69422"></a>
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

<a id="14ba835d1e6b314a"></a>
## SYSTIME

<a id="20222bdd4cf630d8"></a>
### Syntax

```
SYSTIME
```

<a id="a1dfc82551757ea7"></a>
### Description

It obtains the current TIME WITH TIME ZONE type value based on the OS time of the database server.

<a id="277d90760cf551fc"></a>
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

<a id="6af0351965bc17c3"></a>
## SYSTIMESTAMP

<a id="3c4408e6efbee14a"></a>
### Syntax

```
SYSTIMESTAMP
```

<a id="ea66b632f01d74dc"></a>
### Description

It obtains the current TIMESTAMP WITH TIME ZONE type value based on the OS time of the database server.

<a id="fb37399c8164fb46"></a>
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

<a id="6ef44bddb52ec126"></a>
## TAN

<a id="2d87cc9016ab49dc"></a>
### Syntax

```
TAN( num )
```

<a id="c295a170631f0c44"></a>
### Description

It returns the tangent value of num in radians unit.  
If num is NULL, then NULL is returned.

<a id="a0eba4e0dd5a9de6"></a>
### Example

```
gSQL> SELECT TAN( 1 ) AS RESULT FROM DUAL;
         RESULT
---------------
1.5574077246549
1 row selected.
```

<a id="b3a0389eb5f09fa5"></a>
## TO_BASE64

<a id="413a9de3c6a515bb"></a>
### Syntax

```
TO_BASE64( str )
```

<a id="3fc71df7ab20b363"></a>
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

For more information, refer to [FROM_BASE64](#77c63d71a11e0ca5).

<a id="c46f25fedd937ae1"></a>
### Example

```
gSQL> SELECT TO_BASE64( 'abc' ), TO_BASE64( 'abcd' ) FROM DUAL;

TO_BASE64( 'abc' ) TO_BASE64( 'abcd' )
------------------ -------------------
YWJj               YWJjZA==           
1 row selected.
```

<a id="309f9d740c184e9b"></a>
## TO_CHAR( datetime )

<a id="0b50f592d5591753"></a>
### Syntax

```
TO_CHAR( datetime [, fmt ] )
```

<a id="6967b19e3954c143"></a>
### Description

It converts datetime to a string in the specified fmt format, and returns the result.

The datetime argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL.   
The fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING.  

If any argument is NULL, then NULL is returned.

If fmt is omitted, it follows the default format.  
• DATE: Refer to [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#f225d3a5b17e6d4e).  
• TIMESTAMP: Refer to [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#43c4980b87076f57).  
• TIMESTAMP WITH TIME ZONE: Refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#dd69442f6469d388).  
• TIME: Refer to [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#7158a76ad2c0e3ca).  
• TIME WITH TIME ZONE: Refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#41f3a85cc18588b8).

If the data type of the datetime argument is INTERVAL, it is converted to a string then returned regardless of fmt.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#03671a64abd1a4db).

The result type is CHARACTER VARYING.

<a id="2436bcede1a1c689"></a>
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

<a id="2a659c08a4b94105"></a>
## TO_CHAR( number )

<a id="69d0f5b0f5f0c893"></a>
### Syntax

```
TO_CHAR( number [, fmt ] )
```

<a id="1d3044cbad9fe942"></a>
### Description

It converts the number to a string in the specified fmt format, and returns the result.

The number argument can be a numeric data type.  
The fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING.  
If fmt is omitted, all significant digits are converted to the string and returned.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#271d8abc058accde).  
If any input argument is NULL, then NULL is returned.

The result type is CHARACTER VARYING.

<a id="5ea4208b3c047554"></a>
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

<a id="35ded5fdc8f041e5"></a>
## TO_DATE

<a id="e3623b1bae46319b"></a>
### Syntax

```
TO_DATE( str [, fmt ] )
```

<a id="3d73d271a32c3afb"></a>
### Description

It converts the str string in the specified fmt format to DATE type, and returns the result.

The str argument and fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.  
If fmt is omitted, the default format is NLS_DATE_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#03671a64abd1a4db).  
For more information, refer to [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#f225d3a5b17e6d4e).  

If either str or fmt is NULL, then NULL is returned.

The result type is DATE.

<a id="60234752c5df306d"></a>
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

<a id="d42ac4a58a77211a"></a>
## TO_NATIVE_BIGINT

<a id="5b4ccf3e17458374"></a>
### Syntax

```
TO_NATIVE_BIGINT( str [, fmt ] )
```

<a id="eff86a6a0d2e19e1"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_BIGINT type, and returns the result.

The str argument and fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.    
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#271d8abc058accde).

The result type is NATIVE_BIGINT.

<a id="7ebc111111f747ab"></a>
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

<a id="4162e40cd48b1033"></a>
## TO_NATIVE_DOUBLE

<a id="e3f9a9b25b82a518"></a>
### Syntax

```
TO_NATIVE_DOUBLE( str [, fmt ] )
```

<a id="3d01869cfe685111"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_DOUBLE type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#271d8abc058accde).

The result type is NATIVE_DOUBLE.

<a id="93c0b7f829414204"></a>
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

<a id="32715269ef2ff475"></a>
## TO_NATIVE_INTEGER

<a id="2f59c428da178ff4"></a>
### Syntax

```
TO_NATIVE_INTEGER( str [, fmt ] )
```

<a id="5295494bc62e0e57"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_INTEGER type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#271d8abc058accde).

The result type is NATIVE_INTEGER.

<a id="bf604980460fdb46"></a>
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

<a id="7ddf5975b5109253"></a>
## TO_NATIVE_REAL

<a id="4df4ffc868808fb8"></a>
### Syntax

```
TO_NATIVE_REAL( str [, fmt ] )
```

<a id="bcaa7c27f4e8a0e4"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_REAL type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#271d8abc058accde).

The result type is NATIVE_REAL.

<a id="cbaf848fc3529f71"></a>
### Example

```
gSQL> SELECT TO_NATIVE_REAL( '123.45' ) AS RESULT1, 
             TO_NATIVE_REAL( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
```

<a id="577ebbdd94adf670"></a>
## TO_NATIVE_SMALLINT

<a id="0f12822cf83ee156"></a>
### Syntax

```
TO_NATIVE_SMALLINT( str [, fmt ] )
```

<a id="e1dd26920a3ab4a7"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_SMALLINT type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#271d8abc058accde).

The result type is NATIVE_SMALLINT.

<a id="318960cd819f8124"></a>
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

<a id="20749517ec1fc491"></a>
## TO_NUMBER

<a id="ef8bdf571547f69a"></a>
### Syntax

```
TO_NUMBER( str [, fmt] )
```

<a id="ceff5cab67f583af"></a>
### Description

It converts the str string in the specified fmt format to NUMBER type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#271d8abc058accde).

The result type is NUMBER.

<a id="593816ee26e53a61"></a>
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

<a id="d08df835c6ceefa2"></a>
## TO_TIME

<a id="4669fa39f1f6b1ff"></a>
### Syntax

```
TO_TIME( str [, fmt ] )
```

<a id="5665b91c1ff42d8c"></a>
### Description

It converts the str string in the specified fmt format to TIME type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIME_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#03671a64abd1a4db).  
For more information, refer to [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#7158a76ad2c0e3ca).  

If either str or fmt is NULL, then NULL is returned.

The result type is TIME.

<a id="f11a4882f444c67c"></a>
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

<a id="37e0986cf3b6ca6f"></a>
## TO_TIME_TZ

<a id="90cdba1f1c2c618d"></a>
### Syntax

```
TO_TIME_TZ( str [, fmt ] )
```

<a id="1d9d3ba841f07923"></a>
### Description

It is an alias of [TO_TIME_WITH_TIME_ZONE](#831d2a3df6572bc3).  
For more information, refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#41f3a85cc18588b8).

<a id="5858ae8f112a871d"></a>
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

<a id="831d2a3df6572bc3"></a>
## TO_TIME_WITH_TIME_ZONE

<a id="910270fe4b11c853"></a>
### Syntax

```
TO_TIME_WITH_TIME_ZONE( str [, fmt ] )
TO_TIME_TZ( str [, fmt ] )
```

<a id="c104beef92daa484"></a>
### Description

It converts the str string in the specified fmt format to TIME WITH TIME ZONE type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIME_WITH_TIME_ZONE_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#03671a64abd1a4db)  
For more information, refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#41f3a85cc18588b8).  

If either str or fmt is NULL, then NULL is returned.

It is an alias of [TO_TIME_TZ](#37e0986cf3b6ca6f).

The result type is TIME WITH TIME ZONE.

<a id="8fa2fb77357f4e7f"></a>
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

<a id="a8dcc7ffea47ee5d"></a>
## TO_TIMESTAMP

<a id="89d8880a2d135787"></a>
### Syntax

```
TO_TIMESTAMP( str [, fmt ] )
```

<a id="9cb827214713e86c"></a>
### Description

It converts the str string in the specified fmt format to TIMESTAMP type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIMESTAMP_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#03671a64abd1a4db).  
For more information, refer to [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#43c4980b87076f57).  

If either str or fmt is NULL, then NULL is returned.

The result type is TIMESTAMP.

<a id="6e29a08c91cd52ff"></a>
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

<a id="94a7fe7f72f2fafd"></a>
## TO_TIMESTAMP_TZ

<a id="8eaecd3a21ef1a0f"></a>
### Syntax

```
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="241cbec8dfe16985"></a>
### Description

It is an alias of [TO_TIMESTAMP_WITH_TIME_ZONE](#da15df017267a889).  
For more information, refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#dd69442f6469d388).

<a id="f047ab4dff1cbdce"></a>
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

<a id="da15df017267a889"></a>
## TO_TIMESTAMP_WITH_TIME_ZONE

<a id="c52fd3e9f214df56"></a>
### Syntax

```
TO_TIMESTAMP_WITH_TIME_ZONE( str [, fmt ] )
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="60d0a4ba64f2b120"></a>
### Description

It converts the str string in the specified fmt format to TIMESTAMP WITH TIME ZONE type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to  [Datetime Format String](11-sql-elements.md#03671a64abd1a4db).  
For more information, refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#dd69442f6469d388).  

If either str or fmt is NULL, then NULL is returned.

It is an alias of [TO_TIMESTAMP_TZ](#94a7fe7f72f2fafd).

The result type is TIMESTAMP WITH TIME ZONE .

<a id="eb28f9ddd12bc3eb"></a>
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

<a id="9c0959e92f3abb0a"></a>
## TRANSACTION_DATE

<a id="5b564e1eb69c1db0"></a>
### Syntax

```
TRANSACTION_DATE()
```

<a id="22c7c6f5a54c998d"></a>
### Description

It obtains the current date (DATE type) value based on the session time.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="7b91c7224ad439af"></a>
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

<a id="f9372f7602a7623c"></a>
## TRANSACTION_LOCALTIME

<a id="bd008cadddaef0e6"></a>
### Syntax

```
TRANSACTION_LOCALTIME()
```

<a id="2fbc4628bed92b4a"></a>
### Description

It obtains the current TIME WITHOUT TIME ZONE type value based on the session time.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.   
• STATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="de226d8c375af600"></a>
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

<a id="94dda3e05e16fe39"></a>
## TRANSACTION_LOCALTIMESTAMP

<a id="af1da494962caef7"></a>
### Syntax

```
TRANSACTION_LOCALTIMESTAMP()
```

<a id="1881b1ef323378da"></a>
### Description

It obtains the current TIMESTAMP WITHOUT TIME ZONE type value based on the session time.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_LOCALTIMESTAMP(): All timestamp values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="b8f0a14c38fc064b"></a>
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

<a id="7871ccf4beb3b499"></a>
## TRANSACTION_TIME

<a id="2367d602ec17484d"></a>
### Syntax

```
TRANSACTION_TIME()
```

<a id="e57dc30732721bff"></a>
### Description

It obtains the current TIME WITH TIME ZONE type value based on the session time.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• STATEMENT_TIME(): All time values in an SQL statement are same.   
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="9588dd792e1248a1"></a>
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

<a id="97ea0c7f3af04cef"></a>
## TRANSACTION_TIMESTAMP

<a id="35152cd4e1d42337"></a>
### Syntax

```
TRANSACTION_TIMESTAMP()
```

<a id="aeca7855dc07f737"></a>
### Description

It obtains the current TIMESTAMP WITH TIME ZONE type value based on the session time.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_TIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_TIMESTAMP(): All timestamp values in an SQL statement are same.   
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="17a36196a0db7aef"></a>
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

<a id="4dc9d596e8c82a3f"></a>
## TRANSLATE

<a id="32f0befafc4432cd"></a>
### Syntax

```
TRANSLATE( string, from, to )
```

<a id="5eb110622e73957a"></a>
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

<a id="4b3186e84ea94092"></a>
| string type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="ec80548056af6a26"></a>
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

<a id="54d2ad23584c50d5"></a>
## TRIM

<a id="aec8643d517a80fb"></a>
### Syntax

```
TRIM([ [ LEADING | TRAILING | BOTH ]  [trim_character] FROM ] trim_source)
```

<a id="59681cb69a79ae41"></a>
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

<a id="f2e4e0b20bbb47c8"></a>
| trim_character, trim_source type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="c4006e0fdbb3f296"></a>
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

<a id="fdf4d89f7e765d75"></a>
## TRUNC( number )

<a id="30c597596e48f9d4"></a>
### Syntax

```
TRUNC( num [ , scale ] )
```

<a id="e8e0ed50794806b5"></a>
### Description

It truncates the num based on scale, then returns the result.

The num argument and scale argument can be a numeric type.  
If either the num argument or the scale argument is NULL, then NULL is returned.

If scale is omitted, the scale becomes 0, and it is executed as same as TRUNC( num, 0 ).  
If scale is a positive number, it is truncated based on the number of right digit of the decimal point.  
If scale is a negative number, it is truncated off based on the number of left digit of the decimal point.

<a id="798a5658af825f08"></a>
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

<a id="9b43c0eac285f48b"></a>
## TRUNC( date )

<a id="6ca0e7708dbe4488"></a>
### Syntax

```
TRUNC( date [ , fmt ] )
```

<a id="ac3a81630d237a26"></a>
### Description

It truncates the date in a specified fmt unit, and returns the result.

The date argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.  
The fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING.  
If either date argument or fmt argument is NULL, then NULL is returned.

The result type is always DATE regardless of the input date type.

If fmt is omitted, the default is *DAY*, and the available format string is described in the following table.

**Available format string in fmt**

<a id="a05e17ba8766abc0"></a>
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

<a id="44a58bc71af66846"></a>
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

<a id="df6f0d999a275d24"></a>
## UPPER

<a id="08ff508d2d9755fe"></a>
### Syntax

```
UPPER( str )
```

<a id="8c8bd59d80708f88"></a>
### Description

It returns the uppercase characters of str.

The str argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.  
If str is NULL, the result is NULL.

The return type is as same as the str argument type.

<a id="bb51f3797c16985c"></a>
### Example

```
gSQL> SELECT UPPER( 'spring' ) AS RESULT FROM DUAL;
RESULT
------
SPRING
1 row selected.
```

<a id="730bf9e5ae137ebd"></a>
## UNHEX

<a id="e87699ec43b0c04c"></a>
### Syntax

```
UNHEX( str )
```

<a id="ef57eab55bbf9324"></a>
### Description

str argument is a hexadecimal character and this function represents it as each byte and returns it as a binary string.

The input argument can be a character type such as CHARACTER VARYING, CHARACTER LONG VARYING. The result type is a binary character type such as BINARY VARYING or BINARY LONG VARYING.

If str is NULL, then the result value is also NULL.  
If str includes a character which does not belong to the hexadecimal range, then it returns an error.

For more information, refer to [HEX](#feea5870e157c348).

<a id="df9871f7377af15b"></a>
### Example

```
gSQL> SELECT UNHEX( HEX( 'abc' ) ) FROM DUAL;
UNHEX( HEX( 'abc' ) )
---------------------
616263               
1 row selected.
```

<a id="8d1ea3cad0edddee"></a>
## UNHEX_TO_CHARSTR

<a id="d6bcb704dea6fe64"></a>
### Syntax

```
UNHEX_TO_CHARSTR( str )
```

<a id="0b2ce89722b12336"></a>
### Description

str argument is a hexadecimal character and this function represents it as each byte and returns it as a character string.

The input argument can be a character type such as CHARACTER VARYING, CHARACTER LONG VARYING. The result type is a character type such as CHARACTER VARYING, CHARACTER LONG VARYING.

If str is NULL, then the result value is also NULL.  
If str includes a character which does not belong to the hexadecimal range, then it returns an error.

For more information, refer to [HEX](#feea5870e157c348), [UNHEX](#730bf9e5ae137ebd).

<a id="2c515552a5b336de"></a>
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

<a id="6687587b0dbfdae8"></a>
## USER_ID

<a id="006c890b62972e6d"></a>
### Syntax

```
USER_ID ()
```

<a id="1580a1ed0fffac56"></a>
### Description

It obtains the current user's number ID.

> In cluster system, the value may vary depending on the connected server.  
> It is recommended to use [CURRENT_USER](#b8d8322580f3d222) function obtaining the current username.

<a id="a069249debc10b2f"></a>
### Example

```
% gsql test test

gSQL> SELECT USER_ID() FROM dual;

USER_ID()
---------
        6

1 row selected.
```

<a id="e1002c30757e6782"></a>
## UUID

<a id="564e3e4f8e623c84"></a>
### Syntax

```
UUID()
```

<a id="eb498b2dbb9bc33e"></a>
### Description

It creates the universal unique identifier, then returns it.   
The return type is VARBINARY type, and it internally consists of 16 bytes.

<a id="02d5e60567844ef4"></a>
### Example

```
gSQL> SELECT HEX( UUID() ) FROM DUAL;
HEX( UUID() )                   
--------------------------------
E6F0A5C2387511E8B95259E479C2FD50
1 row selected.
```

<a id="fe67b3bcc540e1b1"></a>
## VAR_POP

<a id="a2f1019b0bf07522"></a>
### Syntax

```
VAR_POP( expr )
```

<a id="8aa90acc3ddafaf4"></a>
### Description

It is an aggregation function, and it obtains the population variance of an expr set. If the number of expr sets except for NULL is one, then it returns 0.

The following table describes the arguments and result types.

**Argument and result type of VAR_POP**

<a id="5f197daba9767bc6"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The population variance is a variance of the population (entire) group, and it is the average of the square value of deviation. In other words, it is calculated by extracting the population average (the entire average) from each value of the data, and squaring each value, then adding them together and dividing them by the number of datas in the population group.   
> This value is used to figure out how far each value is from the average value.

For more information, refer to [STDDEV_POP](#2be3066d0dff3e98).

<a id="0feb5ca9daba7e66"></a>
### Example

```
gSQL> SELECT VAR_POP(c1) FROM t1;

VAR_POP(C1)
-----------
     105.76

1 row selected.
```

<a id="a6e0fa57cdf03a12"></a>
## VAR_SAMP

<a id="3cc963b3b956a37c"></a>
### Syntax

```
VAR_SAMP( expr )
```

<a id="57640f888fcf5c08"></a>
### Description

It is an aggregation function, and it obtains the sample variance of an expr set. If the number of expr sets except for NULL is one, then it returns NULL.

The following table describes the arguments and result types.

**Argument and result type of VAR_SAMP**

<a id="afa17d0e9149b478"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> Unlike the population variance dealing with the population (entire) group, the sample variance deals with the average and deviation of extracted samples. In other words, it is calculated by extracting the sample average from each value of the data, and squaring each value, then adding them together and dividing them by the number of datas in the population group minus 1.   
> This value is used to figure out the variance of the population group.

For more information, refer to [STDDEV_SAMP](#447c9e328f1a0472).

<a id="2542103c2420067b"></a>
### Example

```
gSQL> SELECT VAR_SAMP(c1) FROM t1;

VAR_SAMP(C1)
------------
       132.2

1 row selected.
```

<a id="c80a723029120adb"></a>
## VARIANCE

<a id="2afe28858a408ed3"></a>
### Syntax

```
VARIANCE( [ ALL | DISTINCT ] expr )
```

<a id="c2c153a06a92ba98"></a>
### Description

It is an aggregation function, and it obtains the variance of an expr set.

If ALL is specified, this function is performed for all values. If DISTINCT is specified, this function is performed for the values of which the duplicates were deleted from. If it is not specified, it is processed as if ALL is apecified.

If the number of expr sets except for NULL after deleting the duplicates by using DISTINCT is one, then it returns 0.

The following table describes the arguments and result types.

**Argument and result type of VARIANCE**

<a id="6f1be24ed96c79a4"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> GOLDILOCKS gets the variance as follows.  
> • If the number of expr sets is 1, then it returns 0.  
> • If the number of expr sets is bigger than 1, it returns the value of [STDDEV_SAMP (expr)](#447c9e328f1a0472).

For more information, refer to [STDDEV](#b69e3ade827e1705).

<a id="cba609c858ac825f"></a>
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

<a id="0b8239d121998713"></a>
## VERSION

<a id="2d5d44c7bef1bd18"></a>
### Syntax

```
VERSION()
```

<a id="54b601576922313c"></a>
### Description

It obtains the product's version string.

<a id="211c6193c65971c3"></a>
### Example

```
gSQL> SELECT VERSION() FROM dual;

VERSION()                            
-------------------------------------
Release Name.X.X.X revision(XXXXX)

1 row selected.
```

<a id="a5c0965562dfe164"></a>
## WIDTH_BUCKET

<a id="d046b1a2e32d8e04"></a>
### Syntax

```
WIDTH_BUCKET( num, min, max, cnt )
```

<a id="904c8f79cf1ef6ca"></a>
### Description

It creates a section of the same width as cnt within a range between specified min and max, and it returns the section location in which the num is located.

The data type of num argument, min argument, max argument and cnt argument can be a numeric data type.

min, max means the range for the section. If the min value is equal to the max value, an error is returned.  
cnt means the number of sections. The cnt value should be a positive number. If the cnt value is 0 or a negative number, an error is returned.   
The section's location is numbered from one.

If any of num, min, max, cnt is NULL, the result is also NULL.

<a id="6bbe9e626a686413"></a>
### Example

```
gSQL> SELECT WIDTH_BUCKET( 5, 1, 20, 5 ) AS RESULT FROM DUAL;
RESULT
------
     2
1 row selected.
```

---

[← 16. Built-in Data Type References](16-built-in-data-type-references.md) · [Table of contents](../README.md) · [18. SQL References (A~B) →](18-sql-references-a-b.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
