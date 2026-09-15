<a id="5a7f48d77d603569"></a>

# 17. Built-in Function References

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/5a7f48d77d603569)  
> Tag: `26c.1_0_tag`

[← 16. Built-in Data Type References](16-built-in-data-type-references.md) · [Table of contents](../README.md) · [18. SQL References (A~B) →](18-sql-references-a-b.md)

<a id="191216bd565738ac"></a>
## * (MULTIPLICATION)

<a id="0034628c7b981f11"></a>
### Syntax

```
expr1 * expr2
```

<a id="836ecfe1e679903e"></a>
### Description

It returns the result of multiplying expr1 and expr2.

The type of multiplication operation and the resulting type are as follows in the table.  
For more information, refer to [Type Conversion](11-sql-elements.md#fc718a805c53e7ba).

**Numeric * operation**

<a id="3244c12eeadb4350"></a>
| expr1 (expr2) | expr2 (expr1) | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="dc71d6a4b588f153"></a>
<table class="table column_count_3"><caption>INTERVAL * operation</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type is an interval type.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type is an interval type.)</div></td></tr><tr><td class="to_left" colspan="3"><div>Refer to <a class="reference text" href="#c06f3e9d8a2b8c96">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

**INTERVAL type specified in the table includes the following detailed INTERVAL subtypes**

<a id="c06f3e9d8a2b8c96"></a>
<table><thead><tr><th align="center">INTERVAL YEAR TO MONTH</th><th align="center">INTERVAL DAY TO SECOND</th></tr></thead><tbody><tr><td valign="middle"><ul><li>INTERVAL YEAR</li><li>INTERVAL MONTH</li><li>INTERVAL YEAR TO MONTH</li></ul></td><td valign="middle"><ul><li>INTERVAL DAY</li><li>INTERVAL HOUR</li><li>INTERVAL MINUTE</li><li>INTERVAL SECOND</li><li>INTERVAL DAY TO HOUR</li><li>INTERVAL DAY TO MINUTE</li><li>INTERVAL DAY TO SECOND</li><li>INTERVAL HOUR TO MINUTE</li><li>INTERVAL HOUR TO SECOND</li><li>INTERVAL MINUTE TO SECOND</li></ul></td></tr></tbody></table>

<a id="3bf5eb91d78ff30a"></a>
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

<a id="e730e487acc3f1d1"></a>
## + (ADDITION)

<a id="9f63028c83918f62"></a>
### Syntax

```
expr1 + expr2
```

<a id="a147b2cf7d5b8722"></a>
### Description

It returns the result of adding expr1 and expr2.

The type of addition operation and the resulting types are as follows in the table.  
For more information, refer to [Type Conversion](11-sql-elements.md#fc718a805c53e7ba).

**Numeric + operation**

<a id="5cba9537fa0eb8d5"></a>
| expr1 (expr2) | expr2 (expr1) | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="971067b37c03c02f"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) + operation</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference text" href="#c06f3e9d8a2b8c96">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="b991aec8c0dc12ad"></a>
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

<a id="f57fd446dd6d675f"></a>
## + (POSITIVE)

<a id="a2dd9c1a8dcfcaef"></a>
### Syntax

```
+ expr
```

<a id="2c8982234d522a84"></a>
### Description

It displays the + sign on expr.

<a id="77b94e038b2ecd7c"></a>
### Example

```
gSQL> SELECT +3 AS RESULT1, +(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      3      -3
1 row selected.
```

<a id="cb06a4fae99cbdc9"></a>
## - (NEGATIVE)

<a id="a794cb79e4e9f924"></a>
### Syntax

```
- expr
```

<a id="13df0fb3a642dc63"></a>
### Description

It displays the - sign on expr.

<a id="34aa647c69f5c067"></a>
### Example

```
gSQL> SELECT -3 AS RESULT1, -(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     -3       3
1 row selected.
```

<a id="a6113704936bbaf1"></a>
## - (SUBTRACTION)

<a id="f62d28bf3ecec694"></a>
### Syntax

```
expr1 - expr2
```

<a id="9112ff9e01740bfc"></a>
### Description

It returns the result of subtracting expr1 and expr2.

The type of subtraction operation and the resulting types are as follows in the table.  
For more information, refer to [Type Conversion](11-sql-elements.md#fc718a805c53e7ba).

**Numeric - operation**

<a id="36e1c469e537965c"></a>
| expr1 | expr2 | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="252f9360bdee393c"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) - operation</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMBER</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference text" href="#c06f3e9d8a2b8c96">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="7f0d9c2abea09424"></a>
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

<a id="ecfe4d7200d5c831"></a>
## / (DIVISION)

<a id="2070a4ad6bdbfd1c"></a>
### Syntax

```
expr1 / expr2
```

<a id="2386b2991febb946"></a>
### Description

It returns the result of dividing expr1 and expr2.

The type of division operation and the resulting types are as follows in the table.  
For more information, refer to [Type Conversion](11-sql-elements.md#fc718a805c53e7ba).

**Numeric / operation**

<a id="5297216ae8873a7b"></a>
| expr1 | expr2 | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER | NUMBER |
| NATIVE_DOUBLE | NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="5f1b5bcab21f6c40"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) / operation</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type is an interval type.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type is an interval type.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference text" href="#c06f3e9d8a2b8c96">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="e6141498b3bd7d94"></a>
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

<a id="ea2d45a74e2e0cbe"></a>
## || (CONCATENATE)

<a id="50b0d7003ead753e"></a>
### Syntax

```
str1 || str2
```

<a id="05f487956839c77c"></a>
### Description

CONCATENATE returns a string that is the result of concatenating str1 and str2.

If either str1 or str2 is NULL, the non-NULL string is returned. If both str1 and str2 are NULL, the result will also be NULL.

The argument can be a type that can be converted to either a character string type or a binary string type.  
For more information, refer to [Type Conversion](11-sql-elements.md#fc718a805c53e7ba).

It is an alias of [CONCAT](#f398b6d7062ffdd5) and [CONCATENATE](#e3a092e283852102).

The result types are as follows.

**The result types of || (CONCATENATE)**

<a id="740e244c8424e2ad"></a>
| Data type | CHAR | VARCHAR | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR | CHAR | VARCHAR | LONG VARCHAR |
| VARCHAR | VARCHAR | VARCHAR | LONG VARCHAR |
| LONG VARCHAR | LONG VARCHAR | LONG VARCHAR | LONG VARCHAR |
| Data type | BINARY | VARBINARY | LONG VARBINARY |
| BINARY | BINARY | VARBINARY | LONG VARBINARY |
| VARBINARY | VARBINARY | VARBINARY | LONG VARBINARY |
| LONG VARBINARY | LONG VARBINARY | LONG VARBINARY | LONG VARBINARY |

<a id="23eb4bf6bf881190"></a>
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

<a id="66debe22fe5fe5eb"></a>
## ABS

<a id="2fa473102a1a033a"></a>
### Syntax

```
ABS( num )
```

<a id="f465d967fd678769"></a>
### Description

ABS returns the absolute value of num.

The num argument can be a numeric type or any type that can be converted to a number.  
If num is NULL, the function returns NULL.

<a id="a1f713e38b039b82"></a>
### Example

```
gSQL> SELECT ABS(-1) AS RESULT1, ABS(1) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1       1
1 row selected.
```

<a id="6438e1149af0d7ef"></a>
## ACOS

<a id="fdfa554d1c199839"></a>
### Syntax

```
ACOS( num )
```

<a id="8ffe4aff1a7c36ba"></a>
### Description

ACOS returns the arc cosine value of num.  

The num argument must be in the range of -1 to 1.   
If num is NULL, the function returns NULL.  

It returns a value in radians, which is in the range of 0 to pi.

<a id="b5c5da6076edad24"></a>
### Example

```
gSQL> SELECT ACOS( 1 ) FROM DUAL;
ACOS( 1 )
---------
        0
1 row selected.
```

<a id="8e020f57d0e00036"></a>
## ADDDATE

<a id="8f484ec241e35fac"></a>
### Syntax

```
ADDDATE( date, INTERVAL expr unit  )
ADDDATE( expr, days )
```

<a id="6dfa206af714ab79"></a>
### Description

ADDDATE adds the second argument to the first argument and returns the result.  

If either of the input arguments is NULL, the result will also be NULL.  
The first argument can be of type DATE, TIMESTAMP, or TIMESTAMP WITH TIME ZONE, while the second argument can be of type INTERVAL or numeric.

The result type is the same as [(DATETIME/INTERVAL) + operation](#971067b37c03c02f).

<a id="cc846bdd9a6c81ff"></a>
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

<a id="59fdbc5cb3e7c8aa"></a>
## ADDTIME

<a id="dc9970cd81716af3"></a>
### Syntax

```
ADDTIME( expr1, expr2 )
```

<a id="5051a43f02936878"></a>
### Description

ADDTIME adds expr2 to expr1, and returns the result.

expr1 can be of type TIME, TIME WITH TIME ZONE, TIMESTAMP, or TIMESTAMP WITH TIME ZONE TYPE, while expr2 can be of type INTERVAL DAY TO SECOND TYPE.  

If either expr1 or expr2 is NULL, the result will also be NULL.

The result type is the same as [(DATETIME/INTERVAL) + operation](#971067b37c03c02f).

<a id="fd89fae76260b270"></a>
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

<a id="1ce6a0e7cb7a13e4"></a>
## ADD_MONTHS

<a id="725d818973d826fb"></a>
### Syntax

```
ADD_MONTHS( date, number )
```

<a id="55ff41c947815942"></a>
### Description

ADD_MONTHS returns the date obtained by adding the specified number of months to the given date. If the resulting date is later than the last day of the month, it is adjusted to the last day of that month.

The data type of the date argument can be DATE, TIMESTAMP, or TIMESTAMP WITH TIME ZONE, and the number argument can be a numeric type.  
If any of the input arguments is NULL, the result will also be NULL.

The result type is always DATE, regardless of the input argument's date type.

<a id="60af21ec6cf11ae0"></a>
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

<a id="051f809810e5e2aa"></a>
## APPROX_COUNT_DISTINCT

<a id="5a69254a879b7c91"></a>
### Syntax

```
APPROX_COUNT_DISTINCT( expr [, expr, ...] ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="6585e7488c466c03"></a>
### Description

As an aggregation function, it estimates the approximate number of rows with non-NULL values among the distinct values of expr.  

APPROX_COUNT_DISTINCT provides results that are nearly identical to those of COUNT(DISTINCT expr), while processing large volumes of data much faster.  

If a FILTER is specified, aggregation is performed only on values that satisfy the specified condition.

<a id="d1c2f37fb364fe7b"></a>
### Example

```
gSQL> SELECT APPROX_COUNT_DISTINCT( c1 ) FROM t1;

APPROX_COUNT_DISTINCT( C1 )
---------------------------
                         99

1 row selected.

gSQL> SELECT APPROX_COUNT_DISTINCT( c1 ) FILTER ( c2 > 50 ) FROM t1;

APPROX_COUNT_DISTINCT( C1 ) FILTER ( C2 > 50 )
----------------------------------------------
                                            49

1 row selected.
```

> The APPROX_COUNT_DISTINCT function estimates the number of distinct values based on the HyperLogLog algorithm.

<a id="9379d1be7b7614bc"></a>
## ASCII

<a id="46292aa0c1c45ed9"></a>
### Syntax

```
ASCII( char )
```

<a id="29901a4c957cdb52"></a>
### Description

It returns the database character set code of the first character of char in decimal form.  

The data type of char can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or any type that can be converted to a character type, and the return type is NUMBER.  
If char is NULL, the function returns NULL.

<a id="727e4a7411b5d429"></a>
### Example

```
gSQL> SELECT ASCII( 'G' ) AS RESULT FROM DUAL;
RESULT
------
    71
1 row selected.
```

<a id="539398a6119ea91d"></a>
## ASIN

<a id="c0da5d3c114593b9"></a>
### Syntax

```
ASIN( num )
```

<a id="66d201bea69fc72e"></a>
### Description

ASIN returns the arc sin value of num.

The num argument must be in the range of -1 to 1.  
If num is NULL, the function returns NULL.

It returns a radian value in the range of -pi/2 to pi/2.

<a id="24c0f3cd53b806a6"></a>
### Example

```
gSQL> SELECT ASIN( 0 ) FROM DUAL;
ASIN( 0 )
---------
        0
1 row selected.
```

<a id="906d826bffba6a12"></a>
## ATAN

<a id="7718ce469d466d9b"></a>
### Syntax

```
ATAN( num )
```

<a id="1bf3940cc756d00d"></a>
### Description

ATAN returns the arc tangent value of num.

There is no range limitation for the value of num, and it returns a radian value in the range of -pi/2 to pi/2.   
If num is NULL, it returns NULL.

<a id="e674cbe430e2da20"></a>
### Example

```
gSQL> SELECT ATAN(0.5) FROM DUAL;
       ATAN(0.5)
----------------
.463647609000806
1 row selected.
```

<a id="b757df1a93296ea8"></a>
## ATAN2

<a id="233c4c05aa05ead5"></a>
### Syntax

```
ATAN2( num1, num2 )
```

<a id="65a0161be5e94968"></a>
### Description

ATAN2 returns the arc tangent value of num1 and num2.

There is no range limitation for the value of num1 argument, and it returns a radian value in the range of -pi to pi.  
If either num1 or num2 is NULL, the function returns NULL.

<a id="b1b25a921bbbdde8"></a>
### Example

```
gSQL> SELECT ATAN2(1,2) FROM DUAL; 
      ATAN2(1,2)
----------------
.463647609000806
1 row selected.
```

<a id="6bd804108bf49c64"></a>
## AVG

<a id="e590cf434e4149af"></a>
### Syntax

```
AVG( [ ALL | DISTINCT ] num ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="d024f659c82fc92f"></a>
### Description

It is used as an aggregation function to calculate the average value of exprs.

When ALL is specified, aggregation is performed on all values.  
When DISTINCT is specified, aggregation is performed on the values with duplicates removed.  
When neither ALL nor DISTINCT is specified, it is treated the same as if ALL were specified.

If FILTER is specified, aggregation is performed only for values that satisfy the condition.

<a id="9a43c3fe6759234f"></a>
### Example

```
gSQL> SELECT AVG( c1 ) FROM t1;

AVG(C1)
-------
      2

1 row selected.


gSQL> SELECT AVG( c1 ) FILTER( WHERE c1 > 1 ) FROM t1;

AVG(C1)
-------
      3

1 row selected.
```

<a id="1376b5bf52f22ea4"></a>
## AVG() OVER

<a id="b7a4d32689e296ef"></a>
### Syntax

```
AVG ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="6e442597ac4c789d"></a>
### Description

The window function AVG calculates the average value of expr.  
NULL values are excluded from the calculation.

<a id="8c016914792fcd4e"></a>
### Example

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , AVG( min_price ) OVER ( ORDER BY min_price ) AS "AVG"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE              AVG
--------- ----------------
       73               73
      247              160
      731 350.333333333333
     null 350.333333333333
     null 350.333333333333

5 rows selected.
```

<a id="190418c8624fe2fd"></a>
## BITAND

<a id="553a44f97b5855bf"></a>
### Syntax

```
BITAND( num1, num2 )
```

<a id="2cb9f0d47746d809"></a>
### Description

It returns the result of the AND operation on the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or any data type that can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT, the decimal point is truncated.  
If any of the input argument values is NULL, the result will also be NULL.

The result type is NATIVE_BIGINT.

<a id="66fd616588190bc0"></a>
### Example

```
gSQL> SELECT BITAND( 5, 3 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="17e3a5b7f80cada4"></a>
## BITNOT

<a id="ed88d78ec2a8dbad"></a>
### Syntax

```
BITNOT( num )
```

<a id="57023ce013c70932"></a>
### Description

It returns the result of the NOT operation on the num bit.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or any data type that can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT, the decimal point is truncated.  
If the input argument is NULL, the result will also be NULL.

The result type is as follows.  
• If the input argument is NATIVE_SMALLINT, the result type is NATIVE_SMALLINT.  
• If the input argument is NATIVE_INTEGER, the result type is NATIVE_INTEGER.  
• If the input argument is NATIVE_BIGINT, the result type is NATIVE_BIGINT.

<a id="7ad752961904833e"></a>
### Example

```
gSQL> SELECT BITNOT( 5 ) AS RESULT FROM DUAL;
RESULT
------
    -6
1 row selected.
```

<a id="440875e5887624e9"></a>
## BITOR

<a id="9d23d92d2a21f4bd"></a>
### Syntax

```
BITOR( num1, num2 )
```

<a id="012c61f474d12ef2"></a>
### Description

It returns the result of the OR operation on the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or any data type that can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT, the decimal point is truncated.  
If any input argument is NULL, the result will also be NULL.

The result type is NATIVE_BIGINT.

<a id="e5d879524dd35538"></a>
### Example

```
gSQL> SELECT BITOR( 5, 3 ) FROM DUAL;

BITOR( 5, 3 )
-------------
            7
1 row selected.
```

<a id="b75a04128803f30b"></a>
## BITXOR

<a id="63583f41b0f8c105"></a>
### Syntax

```
BITXOR( num1, num2 )
```

<a id="b0499d201e716e78"></a>
### Description

It returns the result of the XOR operation result on the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or any data type that can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT, the decimal point is truncated.  
If any input argument is NULL, the result will be NULL.

The result type is NATIVE_BIGINT.

<a id="7a6ca364d1d60190"></a>
### Example

```
gSQL> SELECT BITXOR( 5, 3 ) FROM DUAL;
BITXOR( 5, 3 )
--------------
             6
1 row selected.
```

<a id="cb321790057d5f91"></a>
## BIT_LENGTH

<a id="09d9e90f3ee5d2d3"></a>
### Syntax

```
BIT_LENGTH( str )
```

<a id="2634007c5b85898d"></a>
### Description

BIT_LENGTH returns the number of bits for the given str.  
If str is NULL, it returns NULL.

<a id="4877ac0e39750b27"></a>
### Example

```
gSQL> SELECT BIT_LENGTH( 'LIKE' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
             32
    1 row selected.
```

<a id="a55aa7d89b47253c"></a>
## BYTE_LENGTH

<a id="d6e76930a692046d"></a>
### Syntax

```
BYTE_LENGTH( str )
```

<a id="28347074a355903a"></a>
### Description

It is an alias of OCTET_LENGTH.  
For more information, refer to [OCTET_LENGTH](#ddbc8d3776b14b1b), [LENGTHB](#c5f46ba504cefe4a).

<a id="cc5e59d05bc2c0d8"></a>
### Example

- Multi-byte character set (e.g. UTF8): 1-byte character

```
gSQL> SELECT BYTE_LENGTH( 'OCTET_LENGTH' ) AS RESULT_1BYTE_CHARACTERS 
        FROM DUAL;
RESULT_1BYTE_CHARACTERS
-----------------------
                     12
1 row selected.
```

- Multi-byte character set (e.g. UTF8): 2-byte character

```
gSQL> SELECT BYTE_LENGTH( 'αβ' ) AS RESULT_2BYTE_CHARACTERS FROM DUAL;
RESULT_2BYTE_CHARACTERS
-----------------------
                      4
1 row selected.
```

<a id="00ada028ea4b123c"></a>
## CASE2

<a id="f3981125d719aab0"></a>
### Syntax

```
CASE2( condition1, result1
      [, condition2, result2
       , ...
       , conditionN, resultN ]
      [, default ] )
```

<a id="1453d1a7c5775ce9"></a>
### Description

CASE2 evaluates the conditions in the specified order.  
If the comparison result is FALSE, it continues evaluating until TRUE is found.  
If the comparison result is TRUE, it returns the corresponding result and stops further evaluation.  
If all the comparison results are FALSE, it returns the default value. If no default is specified, it returns NULL.

If multiple types are used in the result, the result type is determined according to the [Result Type Combination Rule](11-sql-elements.md#4c0e2485bf66d2d0).

CASE2 can be expressed using CASE as follows.

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

<a id="2f56c5f986dac1cb"></a>
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

<a id="9defd2f6f7bf22d3"></a>
## CBRT

<a id="ee149278d286b9f5"></a>
### Syntax

```
CBRT( num )
```

<a id="3605be50ee9c7491"></a>
### Description

It returns the cube root of num.  
If num is NULL, the result will also be NULL.

<a id="cbbb6ee0da0670e8"></a>
### Example

```
gSQL> SELECT CBRT( 27 ) FROM DUAL;
CBRT( 27 )
----------
         3
1 row selected.
```

<a id="e6f694aeb902a472"></a>
## CEIL

<a id="defa1718deec6c76"></a>
### Syntax

```
CEIL( num )
CEILING( num )
```

<a id="17eddaf26b94427e"></a>
### Description

CEIL returns the smallest integer that is greater than or equal to num.  
If num is NULL, it returns NULL.

<a id="28a2c9cfb84421ee"></a>
### Example

```
gSQL> SELECT CEIL( 3.5 ) AS RESULT1, CEIL( -3.5 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      4      -3
1 row selected.
```

<a id="bfc30a82c549098c"></a>
## CHAR_LENGTH

<a id="4f7f8ebe996190f0"></a>
### Syntax

```
CHAR_LENGTH( str )            
CHARACTER_LENGTH( str )
```

<a id="38f3a3346cf566c1"></a>
### Description

CHAR_LENGTH returns the number of characters in str according to the character set.

The str can be a character type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING, or it can be a data type that can be converted to a character type. The return type is NATIVE_BIGINT.

If the data type of str is CHARACTER, trailing blanks are included in the calculation.  
If str is NULL, it returns NULL.

It is an alias of [LENGTH](#dec729ca5cf2693b).

<a id="e9c2f36807885d20"></a>
### Example

Multi-byte character set: (e.g. UTF8)

```
gSQL> SELECT CHAR_LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="82383ccc5174878b"></a>
## CHR

<a id="11fff8c4f7c75a16"></a>
### Syntax

```
CHR( num )
```

<a id="c2397a791e0101d2"></a>
### Description

It returns the character in the database character set code corresponding to num.

num is a numeric type.  
If num is NULL, it returns NULL.  

The return type is VARCHAR.

<a id="e5e3e1c348e2f6c3"></a>
### Example

```
gSQL> SELECT CHR(71) FROM DUAL;
CHR(71)
-------
G      
1 row selected.
```

<a id="52e4f702da64bdb5"></a>
## CLOCK_DATE

<a id="f5ce402e68cf368d"></a>
### Syntax

```
CLOCK_DATE()
```

<a id="d976e4a1b2db4dff"></a>
### Description

Whenever the CLOCK_DATE function is called, it returns the current date (DATE type).

The differences among the functions for obtaining the current date are as follows.  

• TRANSACTION_DATE(): All date values within the transaction are the same.  
• STATEMENT_DATE(): All date values within an SQL statement are the same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is returned.

<a id="7c004ad78236d53e"></a>
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

<a id="c2958ed1e6aca851"></a>
## CLOCK_LOCALTIME

<a id="9b3c6a9f1e4081a6"></a>
### Syntax

```
CLOCK_LOCALTIME()
```

<a id="803b8497d57627aa"></a>
### Description

Whenever the CLOCK_LOCALTIME function is called, it returns the current time value without TIME ZONE (TIME WITHOUT TIME ZONE type).

The differences among the functions for obtaining the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values within the transaction are the same.  
• STATEMENT_LOCALTIME(): All time values within an SQL statement are the same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is returned.

<a id="caaa8a91597db141"></a>
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

<a id="32abd59cdbe768f1"></a>
## CLOCK_LOCALTIMESTAMP

<a id="085ca96ee308b12c"></a>
### Syntax

```
CLOCK_LOCALTIMESTAMP()
```

<a id="5cc73ffc56b227e6"></a>
### Description

Whenever the CLOCK_LOCALTIMESTAMP() function is called, it returns the current TIMESTAMP value without TIME ZONE (TIMESTAMP WITHOUT TIME ZONE type).

The differences among the functions for obtaining the current TIMESTAMP are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All TIMESTAMP values within the transaction are the same.  
• STATEMENT_LOCALTIMESTAMP(): All TIMESTAMP values within an SQL statement are the same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is returned.

<a id="93c02f46d9524f7c"></a>
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

<a id="1d0b0e4659e03f78"></a>
## CLOCK_TIME

<a id="1768bc91283e552b"></a>
### Syntax

```
CLOCK_TIME()
```

<a id="b32572747054e999"></a>
### Description

Whenever the CLOCK_TIME() function is called, it returns the current time value with TIME ZONE (TIME WITH TIME ZONE type).

The differences among the functions for obtaining the current time are as follows.  

• TRANSACTION_TIME(): All time values within the transaction are the same.  
• STATEMENT_TIME(): All time values within an SQL statement are the same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is returned.

<a id="abcdef29bda88160"></a>
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

<a id="93901a08c3c2b5c9"></a>
## CLOCK_TIMESTAMP

<a id="c4ea51c6f700fd86"></a>
### Syntax

```
CLOCK_TIMESTAMP()
```

<a id="c796257e5399f496"></a>
### Description

Whenever the CLOCK_TIMESTAMP() function is called, it returns the current TIMESTAMP value with TIME ZONE (TIMESTAMP WITH TIME ZONE type).

The differences among the functions for obtaining the current TIMESTAMP are as follows.  

• TRANSACTION_TIMESTAMP(): All TIMESTAMP values within the transaction are the same.  
• STATEMENT_TIMESTAMP(): All TIMESTAMP values within an SQL statement are the same.   
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is returned.

<a id="4e288d064f973342"></a>
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

<a id="8ecf82e319ad8324"></a>
## COALESCE

<a id="3a84269042553459"></a>
### Syntax

```
COALESCE( expr1, ..., exprN )
```

<a id="139e7086a325527e"></a>
### Description

It returns the first non-null expr in the expr list.  
If all expr in the expr list are null, it returns null.  
There must be two or more exprs.

If multiple types are present in the expr list, the result type is determined by the [Result Type Combination Rule](11-sql-elements.md#4c0e2485bf66d2d0).

- COALESCE can be expressed using CASE as follows.

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

<a id="396cba996bcd28f9"></a>
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

<a id="f398b6d7062ffdd5"></a>
## CONCAT

<a id="5a26e3a2351c910b"></a>
### Syntax

```
CONCAT( str1, str2, ... )
```

<a id="39c108ca8eb36833"></a>
### Description

It is an alias of || ( CONCATENATE ).  
It is an argument of the CONCAT function, and between 2 and 254 CONCATs can be specified.  
For more information, refer to [|| (CONCATENATE)](#ea2d45a74e2e0cbe) and [CONCATENATE](#e3a092e283852102).

<a id="17df125a57f20ce4"></a>
### Example

```
gSQL> SELECT CONCAT( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="e3a092e283852102"></a>
## CONCATENATE

<a id="9ed46b7693b5d8bf"></a>
### Syntax

```
CONCATENATE( str1, str2, ... )
```

<a id="a05190198664676d"></a>
### Description

It is an alias of || ( CONCATENATE ).  
It is an argument of the CONCATENATE  function, and between  2  and 254 CONCATENATEs can be specified.  
For more information, refer to [CONCAT](#f398b6d7062ffdd5) and [|| (CONCATENATE)](#ea2d45a74e2e0cbe).

<a id="ea23133172fc1ef8"></a>
### Example

```
gSQL> SELECT CONCATENATE( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="f0f3126e0b34eaaa"></a>
## CORR() OVER

<a id="ed64ac1ba259a6c6"></a>
### Syntax

```
CORR( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="5847d5205c5dc244"></a>
### Description

The window function CORR calculates the coefficient of correlation for the pair of exprs.

If either expr1 or expr2 is NULL, it is excluded from the calculation.  
If the number of rows for the pair of exprs is one or fewer, the result is NULL.

<a id="75566da9cee06cf0"></a>
### Example

```
gSQL> SELECT employee_id, TO_CHAR( hire_date, 'YYYY' ) AS hire_date, salary,
             CORR( TO_CHAR( hire_date, 'YYYY' ), salary ) OVER ( ORDER BY employee_id ) AS corr
      FROM employees
      WHERE department_id = 60;

EMPLOYEE_ID HIRE_DATE SALARY              CORR
----------- --------- ------ -----------------
        103 1990        9000              null
        104 1991        6000                -1
        105 1997        4800 -.805837379342809
        106 1998        4800 -.840210805972693
        107 1999        4200 -.875185734200534

5 rows selected.
```

<a id="01430adf113ff75c"></a>
## COS

<a id="eedc38b265b1e9ff"></a>
### Syntax

```
COS(num)
```

<a id="85564f97146c648c"></a>
### Description

It returns the COSINE value of num.  
If the num argument is NULL, the result will also be NULL.

<a id="72eba07b29e07168"></a>
### Example

```
gSQL> SELECT COS( 0 ) FROM DUAL;
COS( 0 )
--------
       1
1 row selected.
```

<a id="68c7f9a4e95e4dd2"></a>
## COT

<a id="7bec8b21a3962b4d"></a>
### Syntax

```
COT(num)
```

<a id="0460aad0afe615b7"></a>
### Description

It returns the COTANGENT value of num.  
If the num argument is NULL, the result will also be NULL.

<a id="593eeb95b4796bcf"></a>
### Example

```
gSQL> SELECT COT( 1 ) FROM DUAL;
        COT( 1 )
----------------
.642092615934331
1 row selected.
```

<a id="f006671e89899b6b"></a>
## COUNT

<a id="eeb5d849e8e5280a"></a>
### Syntax

```
COUNT( [ ALL | DISTINCT ] expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="5c23a29b942724ec"></a>
### Description

It is an aggregate function. It returns the number of rows where expr is not NULL.

If ALL is explicitly specified, the aggregation is performed on all values.  
If DISTINCT is explicitly specified, the aggregation is performed on the values excluding duplicates.  
If neither ALL nor DISTINCT is explicitly specified, it is processed as if ALL were specified.

If FILTER is specified, the aggregation is performed only on the values that satisfy the condition.

<a id="aec392006f92bf56"></a>
### Example

```
gSQL> SELECT COUNT( c1 ) FROM t1;

COUNT(C1)
---------
        3

1 row selected.


gSQL> SELECT COUNT( c1 ) FILTER( WHERE c1 > 1 ) FROM t1;

COUNT(C1)
---------
        2

1 row selected.
```

<a id="7a9d83c1c4f33ad5"></a>
## COUNT() OVER

<a id="1e4e09365328e945"></a>
### Syntax

```
COUNT ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="ce4b109f83f27779"></a>
### Description

The window function COUNT counts the number of rows.   
NULL values are excluded from the calculation.

<a id="5e384bd8a49f923d"></a>
### Example

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , COUNT( min_price ) OVER ( ORDER BY min_price ) AS "COUNT"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE COUNT
--------- -----
       73     1
      247     2
      731     3
     null     3
     null     3

5 rows selected.
```

<a id="d9b43e9a86df6f7b"></a>
## COUNT(*)

<a id="5b1881e898ceb0e1"></a>
### Syntax

```
COUNT(*) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="a9a74169c170d52c"></a>
### Description

It is an aggregate function that counts the number of rows. It doesn't consider whether the values are NULL or not, as no specific expression is explicitly provided.

If a FILTER is specified, the aggregation is performed only for values that satisfy the condition.

<a id="ebefedc41965389c"></a>
### Example

```
gSQL> SELECT COUNT(*) FROM t1;

COUNT(*)
--------
       4

1 row selected.


gSQL> SELECT COUNT(*) FILTER( WHERE c1 > 1 ) FROM t1;

COUNT(*)
--------
       2

1 row selected.
```

<a id="8df906e8b2c6ef7b"></a>
## COUNT(*) OVER

<a id="24f86f2d17abe530"></a>
### Syntax

```
COUNT(*) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="f2641833eb4dea1b"></a>
### Description

The window function COUNT(*) counts the number of rows.  
Since no expression is explicitly specified, it doesn't matter whether the value is NULL or not.

<a id="ef5597f2589e6b0c"></a>
### Example

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , COUNT(*) OVER ( ORDER BY min_price ) AS "COUNT(*)"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE COUNT(*)
--------- --------
       73        1
      247        2
      731        3
     null        5
     null        5

5 rows selected.
```

<a id="71040c22ebaa8b2b"></a>
## COVAR_POP() OVER

<a id="eb57516dd34e9e12"></a>
### Syntax

```
COVAR_POP( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="614d4d96d589f49d"></a>
### Description

The window function COVAR_POP calculates the population covariance for a pair of exprs.

If either expr1 or expr2 is NULL, it is excluded from the calculation.   
If the number of rows for the pair of exprs is one or fewer, the result will be 0.

<a id="129a263d9689d861"></a>
### Example

```
gSQL> SELECT employee_id, TO_CHAR( hire_date, 'YYYY' ) AS hire_date, salary,
             COVAR_POP( TO_CHAR( hire_date, 'YYYY' ), salary ) OVER ( ORDER BY employee_id ) AS covar_pop
      FROM employees
      WHERE department_id = 60;

EMPLOYEE_ID HIRE_DATE SALARY COVAR_POP
----------- --------- ------ ---------
        103 1990        9000         0
        104 1991        6000      -750
        105 1997        4800     -4400
        106 1998        4800     -5100
        107 1999        4200     -5640

5 rows selected.
```

<a id="726b04caaea6a059"></a>
## COVAR_SAMP() OVER

<a id="b44648c9969a4e7f"></a>
### Syntax

```
COVAR_SAMP( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="6d1daf99a124e323"></a>
### Description

The window function COVAR_SAMP calculates the sample covariance for a pair of exprs.

If either expr1 or expr2 is NULL, it is excluded from the calculation.   
If the number of rows for the pair of exprs is one or fewer, the result will be NULL.

<a id="249c840dc4956bd4"></a>
### Example

```
gSQL> SELECT employee_id, TO_CHAR( hire_date, 'YYYY' ) AS hire_date, salary,
             COVAR_SAMP( TO_CHAR( hire_date, 'YYYY' ), salary ) OVER ( ORDER BY employee_id ) AS covar_samp
      FROM employees
      WHERE department_id = 60;

EMPLOYEE_ID HIRE_DATE SALARY COVAR_SAMP
----------- --------- ------ ----------
        103 1990        9000       null
        104 1991        6000      -1500
        105 1997        4800      -6600
        106 1998        4800      -6800
        107 1999        4200      -7050

5 rows selected.
```

<a id="1084d34375187411"></a>
## CUME_DIST() OVER

<a id="d0085c0701be7f42"></a>
### Syntax

```
CUME_DIST( ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="d907055977306461"></a>
### Description

The window function CUME_DIST calculates the cumulative distribution based on the relative position of the current row's value.

The result of the CUME_DIST function is a number between 0 and 1.  
If the values of the rows are the same, it returns the same result, which is the largest cumulative distribution value.

A window frame can not be used.

<a id="03a33cc0b090e9ec"></a>
### Example

```
gSQL> SELECT department_id, salary,
             CUME_DIST() OVER ( ORDER BY salary ) AS cume_dist
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY CUME_DIST
------------- ------ ---------
           60   4200        .2
           60   4800        .6
           60   4800        .6
           60   6000        .8
           60   9000         1

5 rows selected.
```

<a id="a6a2f59adbdb357d"></a>
## CURRENT_CATALOG

<a id="a4aa7ea734c7eca7"></a>
### Syntax

```
CURRENT_CATALOG [()]
```

<a id="45b135cce53af458"></a>
### Description

The catalog name (i.e., the database name) is obtained.

<a id="b42c17db6a4fdfef"></a>
### Example

```
gSQL> SELECT CURRENT_CATALOG FROM dual;

CURRENT_CATALOG
---------------
TEST_DB        

1 row selected.
```

<a id="4a5eee8c77603529"></a>
## CURRENT_DATE

<a id="227d0b6147836ae2"></a>
### Syntax

```
CURRENT_DATE [()]
STATEMENT_DATE()
```

<a id="7b839781517afb75"></a>
### Description

The current date (DATE type) is obtained.

CURRENT_DATE is an SQL standard function.

The differences among the functions for obtaining the current date are as follows.  

• TRANSACTION_DATE(): All date values within the transaction are the same.  
• CURRENT_DATE, STATEMENT_DATE(): All date values within an SQL statement are the same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is returned.

<a id="f628f226df867921"></a>
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

<a id="38ee0469541ddc0f"></a>
## CURRENT_ROLE

<a id="7939751be2955ca8"></a>
### Syntax

```
CURRENT_ROLE [()]
```

<a id="08cf3a84a3ce145a"></a>
### Description

It returns the role of the current session.

<a id="d1e0a2bcf76bacb9"></a>
### Example

```
% gsql sys gliese

gSQL> SELECT current_user, current_role FROM dual;

CURRENT_USER CURRENT_ROLE
------------ ------------
SYS          null        

1 row selected.

gSQL> SET ROLE sysdba;

Session set.

gSQL> SELECT current_user, current_role FROM dual;

CURRENT_USER CURRENT_ROLE
------------ ------------
SYS          SYSDBA      

1 row selected.

gSQL> SET ROLE NONE;

Session set.


gSQL> SELECT current_user, current_role FROM dual;

CURRENT_USER CURRENT_ROLE
------------ ------------
SYS          null        

1 row selected.
```

<a id="fe4ad0b4ed2109ab"></a>
## CURRENT_SCHEMA

<a id="a49e2a419b1c597a"></a>
### Syntax

```
CURRENT_SCHEMA [()]
```

<a id="0349f6b57ac6adbe"></a>
### Description

The user's current SCHEMA is obtained.

<a id="932adfe050afbb1a"></a>
### Example

```
gSQL> SELECT CURRENT_SCHEMA FROM dual;

CURRENT_SCHEMA
--------------
PUBLIC        

1 row selected.
```

<a id="29a0a944688833fc"></a>
## CURRENT_TIME

<a id="7f774d0ac715e69f"></a>
### Syntax

```
CURRENT_TIME [()]
STATEMENT_TIME()
```

<a id="1b2cd50b125973f5"></a>
### Description

The current TIME WITH TIME ZONE type value, based on the session time, is obtained.

CURRENT_TIME is an SQL standard function.

The differences among the functions for obtaining the current time are as follows.  

• TRANSACTION_TIME(): All time values within the transaction are the same.  
• CURRENT_TIME, STATEMENT_TIME(): All time values within an SQL statement are the same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is returned.

<a id="9c3a1e8532fc16bb"></a>
### Example

All rows contain the same value.

```
gSQL> SELECT CURRENT_TIME FROM t1;

CURRENT_TIME          
----------------------
16:27:10.116396 +09:00
16:27:10.116396 +09:00
16:27:10.116396 +09:00

3 rows selected.
```

<a id="f242b35f2a25d86c"></a>
## CURRENT_TIMESTAMP

<a id="4719f989a784ea0f"></a>
### Syntax

```
CURRENT_TIMESTAMP [()]
STATEMENT_TIMESTAMP()
```

<a id="cc93036c3ddb5948"></a>
### Description

The TIMESTAMP WITH TIME ZONE type value, based on the session time, is obtained.

CURRENT_TIMESTAMP is an SQL standard function.

The differences among the functions for obtaining the current TIMESTAMP are as follows.  

• TRANSACTION_TIMESTAMP(): All TIMESTAMP values within the transaction are the same.  
• CURRENT_TIMESTAMP, STATEMENT_TIMESTAM(): All TIMESTAMP values within an SQL statement are the same.  
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is returned.

<a id="5232c241b6c89f5c"></a>
### Example

All rows contain the same value.

```
gSQL> SELECT CURRENT_TIMESTAMP FROM t1;

CURRENT_TIMESTAMP                
---------------------------------
2013-12-12 16:34:55.649632 +09:00
2013-12-12 16:34:55.649632 +09:00
2013-12-12 16:34:55.649632 +09:00

3 rows selected.
```

<a id="3d2fbc075f3881c1"></a>
## CURRENT_USER

<a id="3c97a9fe0f797e08"></a>
### Syntax

```
CURRENT_USER [()]
```

<a id="e5aa9fc6684e7dcf"></a>
### Description

It returns the current user.

User information is managed in three types, as follows.

- Logon user: The user who performed the login, and their identity is maintained until the connection is closed.
- Session user: It is the same as the initial logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: Generally the same as the session user, but it may be temporarily altered internally by the system for access control when using PSM, views, or similar features.
    - The distinction between the session user and current user is similar to the difference between the real user and effective user in Unix systems.

<a id="462e03c3e6188393"></a>
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

<a id="a9f13cbd9fea3680"></a>
## CURRVAL

<a id="0ebe3a3cc724d8da"></a>
### Syntax

```
seq_name.CURRVAL
CURRVAL(seq_name)
```

<a id="07f13fdd43e858da"></a>
### Description

The current value of the sequence object is obtained.

A sequence value must be set using NEXTVAL(seq_name) at least once.

<a id="f8ef607b300170a7"></a>
### Example

```
gSQL> SELECT seq.CURRVAL FROM dual;

SEQ.CURRVAL
-----------
          1

1 row selected.
```

<a id="e08c2b0d186f7434"></a>
## DATEADD

<a id="c8a5164f2c62589a"></a>
### Syntax

```
DATEADD( datepart, number, date )
```

<a id="63cbb31f97b265ef"></a>
### Description

It adds a specified number to the given datepart of a date and returns the result.

If the number has a decimal point, it is not rounded.  
The supported date data types are DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, and TIME WITH TIME ZONE.  
If either the number or date is NULL, the result will also be NULL.

The result will have the same data type as the input date argument.

**Available format string for datepart**

<a id="f839e31019d59c45"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">Description</th></tr><tr><td>YEAR</td><td>Year</td></tr><tr><td>QUARTER</td><td>Quarter</td></tr><tr><td>MONTH</td><td>Month</td></tr><tr><td>DAYOFYEAR</td><td>Day of year</td></tr><tr><td>DAY</td><td>Day</td></tr><tr><td>WEEK</td><td>Week</td></tr><tr><td>WEEKDAY</td><td>Weekday</td></tr><tr><td>HOUR</td><td>Hour</td></tr><tr><td>MINUTE</td><td>Minute</td></tr><tr><td>SECOND</td><td>Second</td></tr><tr><td>MILLISECOND</td><td>Millisecond</td></tr><tr><td>MICROSECOND</td><td>Microsecond</td></tr></tbody></table>

<a id="83e8d8b85fadfe23"></a>
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

<a id="0a5c8116c798633e"></a>
## DATEDIFF

<a id="5232f0de04cb96bd"></a>
### Syntax

```
DATEDIFF( datepart, startdate, enddate )
```

<a id="f33f53b0a545102c"></a>
### Description

It substracts startdate from enddate, and returns the result in the specified datepart.

If either startdate or enddate is NULL, the result will also be NULL.  
The data types of startdate and enddate can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, or TIME.

The result type is a NUMBER.

**Available format string for datepart**

<a id="07cf107f83ef7eaf"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">Description</th></tr><tr><td>YEAR</td><td>Year</td></tr><tr><td>QUARTER</td><td>Quarter</td></tr><tr><td>MONTH</td><td>Month</td></tr><tr><td>DAYOFYEAR</td><td>Day of year</td></tr><tr><td>DAY</td><td>Day</td></tr><tr><td>HOUR</td><td>Hour</td></tr><tr><td>MINUTE</td><td>Minute</td></tr><tr><td>SECOND</td><td>Second</td></tr><tr><td>MILLISECOND</td><td>Millisecond</td></tr><tr><td>MICROSECOND</td><td>Microsecond</td></tr></tbody></table>

<a id="c388e9aa218ebbb0"></a>
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

<a id="2c1ca00fa963ce14"></a>
## DATE_ADD

<a id="e6d6d428edc2d0ea"></a>
### Syntax

```
DATE_ADD( date, INTERVAL expr unit  )
```

<a id="57cf8912a08c01c9"></a>
### Description

It is the same function as [ADDDATE](#8e020f57d0e00036) (date, INTERVAL expr unit).

<a id="a159af570417ca3a"></a>
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

<a id="1060ca0ee1b36b88"></a>
## DATE_PART

<a id="15e173d155d12e13"></a>
### Syntax

```
DATE_PART( field, datetime )
```

<a id="f4e9af9f50868df8"></a>
### Description

The result of DATE_PART is the same as that of the EXTRACT function. It retrieves the specified field from the given datetime type and returns it.

The field argument must be a text literal, and valid values such as YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, TIMEZONE_HOUR, and TIMEZONE_MINUTE can be specified as text literals.  
The datetime argument can be of the DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, or INTERVAL data types.

If the field is not within the range of the datetime, an error will be returned.   
For the DATE type, the field must be YEAR, MONTH, or DAY; otherwise, an error will be returned.  
If the datatime is NULL, the function will return NULL.

The return type is a NUMBER.

For more information, refer to [EXTRACT](#ac1108d8f983023f).

<a id="aa8df546bc955752"></a>
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

<a id="7530326fc1dda91b"></a>
## DECODE

<a id="bf99c36fc6bce917"></a>
### Syntax

```
DECODE( expr, comparison_expr1, result1
           [, comparison_expr2, result2
            , ...
            , comparison_exprN, resultN ]
           [, default ] )
```

<a id="415c3f69bee2ea78"></a>
### Description

It evaluates expr and comparison_expr in the specified order in the DECODE statement using the equal operation.  
If the comparison result is FALSE, the evaluation continues until a TRUE result is found.  
When the comparison result is TRUE, it returns the corresponding value and stops further evaluation.

If expr and comparison_expr are equal, or if both expr and comparison_expr are NULL ( i.e., null = null ), the result is evaluated as TRUE, and the corresponding value is returned.  
If all evaluated results are FALSE, it returns the default value. If the default is omitted, NULL is returned.

- Comparison of expr and comparison_expr  
  All expr, comparison_expr1, ..., comparison_exprN are converted to the data type of comparison_expr1 (the first comparison_expr) for comparison.  
  If comparison_expr1 (the first comparison_expr) is a character type or a numeric type, it will be converted to a type that can include the ranges of all the types specified in *expr, comparison_expr1, ..., comparison_exprN*.  
  If all types specified in *expr, comparison_expr1, ..., comparison_exprN* are of the CHAR type, a VARCHAR type comparison is performed.

- Result type  
  The result type is determined by the data type of result1 (the first result).  
  If the data type of result1 (the first result) is a character type or a numeric type, the result type becomes the type that includes the range of types specified in result1, ..., resultN.  
  If result1 (the first result) is CHAR or NULL, the result type will be VARCHAR.

DECODE can be expressed using CASE as follows.

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

<a id="60c1fa22a545e15b"></a>
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

<a id="1d433d7c0ea7a97c"></a>
## DEGREES

<a id="4cbaf4a175268d0c"></a>
### Syntax

```
DEGREES( radians )
```

<a id="cacc36e61b23eab5"></a>
### Description

It returns the value of the angle radians converted from radians to degrees.  
If radians is NULL, the result will also be NULL.

<a id="59136e415e5857c1"></a>
### Example

```
gSQL> SELECT DEGREES( PI() ) AS RESULT FROM DUAL;
RESULT
------
   180
1 row selected.
```

<a id="5e4ac5c4854abc9e"></a>
## DENSE_RANK() OVER

<a id="e885a85a0a20314d"></a>
### Syntax

```
DENSE_RANK( ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="dab2714a047faa5c"></a>
### Description

The window function DENSE_RANK calculates the ranking.

The ranking is a consecutive integer starting from 1, and rows with the same value have the same rank.  
However, unlike RANK, when rows with the same value appear, the ranking is not skipped.

A window frame can not be used.

<a id="970aa8071bde1cd6"></a>
### Example

```
gSQL> SELECT department_id, salary,
             DENSE_RANK() OVER ( ORDER BY salary ) AS d_rank
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY D_RANK
------------- ------ ------
           60   4200      1
           60   4800      2
           60   4800      2
           60   6000      3
           60   9000      4

5 rows selected.
```

<a id="e3d9b3a20030165f"></a>
## DIGEST

<a id="4d8a68df2b795512"></a>
### Syntax

```
DIGEST( data, type )
```

<a id="6d46a23e6ad9daf6"></a>
### Description

It hashes the data to the specified type and returns the result as VARBINARY.

An implicit conversion may occur when inputting a data type based on the following rules.  

• BINARY and VARBINARY type data are input as VARBINARY.  
• LONG VARBINARY type data is input as LONG VARBINARY.  
• LONG VARCHAR type data is input as LONG VARCHAR.  
• All other data types are implicitly converted to VARCHAR before being input.

The DIGEST function supports the following hash types.  

• The result of 'SHA1' is a 20-byte varbinary.  
• The result of 'SHA224' is a 28-byte varbinary.  
• The result of 'SHA256' is a 32-byte varbinary.  
• The result of 'SHA384' is a 48-byte varbinary.  
• The result of 'SHA512' is a 64-byte varbinary.

Since the result is returned in VARBINARY type, the HEX function must be used to view it as a hexadecimal string. In this case, the length will be twice the original.

<a id="ae0226a7d266700b"></a>
### Example

```
gSQL> SELECT HEX( DIGEST( 'my password', 'SHA256' ) ) AS RESULT FROM DUAL;

RESULT                                                          
----------------------------------------------------------------
BB14292D91C6D0920A5536BB41F3A50F66351B7B9D94C804DFCE8A96CA1051F2

1 row selected.
```

<a id="efa55e6bf0828d57"></a>
## DUMP

<a id="20f0d505fc37f336"></a>
### Syntax

```
DUMP( expr )
```

<a id="5fbcc688d8f1a1fe"></a>
### Description

It returns the internal representation information of expr.   
This information includes the data type, byte length, and data content.

expr can be of any data type.  
If expr is NULL, it returns NULL.  

The return type is CHARACTER VARYING.

<a id="371886def3933cd6"></a>
### Example

```
gSQL> SELECT DUMP( 'DUMP' ) AS RESULT FROM DUAL;
RESULT                           
---------------------------------
Type=CHAR Len=4 : Str=68,85,77,80
1 row selected.
```

<a id="76fc20b41ca68dec"></a>
## EXP

<a id="c5cec06d2ae497e3"></a>
### Syntax

```
EXP( num )
```

<a id="7ed69f6121482103"></a>
### Description

It returns the value of e (the base of the natural logarithm) raised to the power of num.  
If num is NULL, it returns NULL.

<a id="8d4cc26b53c771d4"></a>
### Example

```
gSQL> SELECT EXP( 1 ) AS RESULT FROM DUAL;
          RESULT
----------------
2.71828182845905
1 row selected.
```

<a id="ac1108d8f983023f"></a>
## EXTRACT

<a id="2265e3a95529914d"></a>
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

<a id="d9dd2da9eec3350d"></a>
### Description

It searches for the specified field within an input datetime type and returns the result.

The datetime argument can be of DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, or INTERVAL data types.

If the field is not within the range of the datetime, an error is returned.   
For the DATE type, the field must be YEAR, MONTH, or DAY; otherwise an error is returned.  
The return type is NUMBER.

The result of EXTRACT is the same as the result of the [DATE_PART](#1060ca0ee1b36b88) function.

<a id="de7c46927bdc33ee"></a>
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

<a id="dd9a0095c17bf009"></a>
## FACTORIAL

<a id="1af9c9e280ccc693"></a>
### Syntax

```
FACTORIAL( num )
```

<a id="37a6fbbc8e3cc6e9"></a>
### Description

It returns the result of successively multiplying the natural numbers from 1 to num.  
If num is NULL, it returns NULL.

<a id="82570370e9319748"></a>
### Example

```
gSQL> SELECT FACTORIAL( 5 ) AS RESULT FROM DUAL;
RESULT
------
   120
1 row selected.
```

<a id="4953a10d0f413251"></a>
## FIRST() OVER

<a id="7e2f7151a7ebceb3"></a>
### Syntax

```
aggregation_function KEEP ( DENSE_RANK FIRST ORDER BY <sort specification list> ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="b671a8ded8ef7897"></a>
### Description

The window function FIRST sorts the sort specification list written in the *order by* within the KEEP clause, and then returns the aggregation function value of the rows with a DENSE_RANK of 1.

aggregation_functions includes AVG, COUNT, COUNT(*), SUM, MAX, MIN, STDDEV, and VARIANCE.

*order by* is not allowed within the window clause.  
A window frame can not be used.

<a id="7bf0da8e530ce279"></a>
### Example

```
gSQL> SELECT department_id, salary,
           DENSE_RANK() OVER ( ORDER BY department_id ) AS "DENSE_RANK",
           MAX( salary ) KEEP ( DENSE_RANK FIRST ORDER BY department_id ) OVER () AS "MAX_FIRST"
  FROM employees
 WHERE department_id BETWEEN 90 AND 100;
    
DEPARTMENT_ID SALARY DENSE_RANK MAX_FIRST
------------- ------ ---------- ---------
           90  24000          1     24000
           90  17000          1     24000
           90  17000          1     24000
          100  12000          2     24000
          100   9000          2     24000
          100   8200          2     24000
          100   7700          2     24000
          100   7800          2     24000
          100   6900          2     24000

9 rows selected.
```

<a id="5eb75302623eb2a6"></a>
## FIRST_VALUE() OVER

<a id="3a98731e76aea527"></a>
### Syntax

```
FIRST_VALUE ( expr ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

FIRST_VALUE ( expr [ RESPECT NULLS | IGNORE NULLS ] ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="af7d8f5027971682"></a>
### Description

The window function FIRST_VALUE returns the first value of expr.

RESPECT NULLS returns the first value of rows, including NULL.  
IGNORE NULLS returns the first value of row, excluding NULL.  
If not specified, the default is RESPECT NULLS.

<a id="0f06f645d7f9b73f"></a>
### Example

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , FIRST_VALUE( min_price ) OVER ( ORDER BY min_price NULLS FIRST ) AS "FIRST_VALUE"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE FIRST_VALUE
--------- -----------
     null        null
     null        null
       73        null
      247        null
      731        null

5 rows selected.
```

The following is an example of specifying IGNORE NULLS in null_treatment.

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , FIRST_VALUE( min_price IGNORE NULLS ) OVER ( ORDER BY min_price NULLS FIRST )
                                                       AS "FIRST_VALUE"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE FIRST_VALUE
--------- -----------
     null        null
     null        null
       73          73
      247          73
      731          73

5 rows selected.
```

<a id="dfe1ce74826d9936"></a>
## FLOOR

<a id="b9d156454b9a7d91"></a>
### Syntax

```
FLOOR( num )
```

<a id="0327bc5f8a532347"></a>
### Description

It returns the largest integer that is less than or equal to num.  
If num is NULL, it returns NULL.

<a id="2a9f241da83d8aef"></a>
### Example

```
gSQL> SELECT FLOOR(42.8) AS RESULT1, FLOOR(-42.8) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     42     -43
1 row selected.
```

<a id="0d50a7fd97d90202"></a>
## FROM_BASE64

<a id="85fc4117f6d4e215"></a>
### Syntax

```
FROM_BASE64( str )
```

<a id="b685c901f39f381d"></a>
### Description

FROM_BASE64 takes a character encoded in base64 as input and returns the decoded binary string.

The input argument data type can be a character type, such as CHARACTER VARYING or CHARACTER LONG VARYING, and the result type is a binary character type, such as BINARY VARYING or BINARY LONG VARYING.

If str is NULL, the result will also be NULL.  
If str contains characters that are not within the base64 character range, an error will be returned.  
Newlines, carriage returns, tabs, and spaces in str are ignored during decoding.

For more information, refer to [TO_BASE64](#3044e7537d8a1aaf).

<a id="c834672e95667645"></a>
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

<a id="76dc6a1d1e48f0dd"></a>
## FROM_TZ

<a id="c16ecc479a6fb361"></a>
### Syntax

```
FROM_TZ( timestamp, timezone )
```

<a id="d3f56842fefdbc39"></a>
### Description

The FROM_TZ function converts the timestamp and the timezone in the specified format to the TIMESTAMP WITH TIME ZONE type and returns it.

The timestamp argument must be of TIMESTAMP type or a type convertible to TIMESTAMP.   
If the timestamp argument is NULL, the result will also be NULL.

The timezone argument must be of CHARACTER type, such as CHARACTER or CHARACTER VARYING, and the format must be 'TZH:TZM'.   
If the timezone argument is NULL, the result will also be NULL.

The result type is TIMESTAMP(6) WITH TIME ZONE.

<a id="619f05c6072702db"></a>
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

<a id="067117605c1b92c1"></a>
## GREATEST

<a id="fa7929d1f3f703f0"></a>
### Syntax

```
GREATEST( expr1 [, expr2, ... exprn ] )
```

<a id="33ee8ccf08a23121"></a>
### Description

It returns the largest value among the expr arguments provided.

If any expr argument is NULL, the result will be NULL.

The result type is the data type of expr1 (the first expr).  
If the data type of expr1 is numeric or character, the result type is determined to be a type that can include the range of expr1, ..., exprN.  
If all of expr1, ..., exprN are defined as CHAR type, then all exprs are compared as VARCHAR type, and the result type is determined to be VARCHAR.

<a id="df504fcd5d1bb7d4"></a>
### Example

```
gSQL> SELECT GREATEST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
   200
1 row selected.
```

<a id="6618c1617cf70e9a"></a>
## GROUPING

<a id="80c3a837fd478d0c"></a>
### Syntax

```
GROUPING( expr [, expr]... )
```

<a id="6213db0ad5afa6cf"></a>
### Description

The GROUPING function should be used together with GROUP BY.  
expr is an argument where each expr represents a single bit, and it returns the corresponding number. If it is used as a GROUPING KEY, the value is 0; otherwise, it is 1.  
The result datatype is NATIVE_INTEGER. The maximum number of bits that can be represented as a positive integer is 31, so the maximum number of GROUPING() arguments is 31.

The GROUPING function works as follows when used together with GROUP BY ROLLUP(a,b).

<a id="e85586b635569a00"></a>
| Grouping Set | Bit vector | GROUPING |
| --- | --- | --- |
| a, b | 0 0 | 0 |
| a | 0 1 | 1 |
| null | 1 1 | 3 |

The GROUPING function works as follows when used together with GROUP BY CUBE(a,b).

<a id="3f32bd727e833a8d"></a>
| Grouping Set | Bit vector | GROUPING |
| --- | --- | --- |
| a,b | 0 0 | 0 |
| a | 0 1 | 1 |
| b | 1 0 | 2 |
| null | 1 1 | 3 |

<a id="c370e5438518f934"></a>
### Example

```
\EXPLAIN PLAN
SELECT 
       calendar_year as year 
     , calendar_quarter_desc as quarter
     , calendar_month_desc as month
     , GROUPING( calendar_year, calendar_quarter_desc, calendar_month_desc ) as grouping_id_func
  FROM sales, times
 WHERE sales.time_id=times.time_id 
   AND times.calendar_year = 2001
   AND sales.cust_id < 1000 AND sales.prod_id > 142 AND sales.channel_id > 2
 GROUP BY ROLLUP(calendar_year, calendar_quarter_desc, calendar_month_desc)
 ORDER BY 1, 2, 3;    2     3     4     5     6     7     8     9    10    11    12 

YEAR QUARTER MONTH   GROUPING_ID_FUNC
---- ------- ------- ----------------
2001 2001-01 2001-01                0
2001 2001-01 2001-02                0
2001 2001-01 2001-03                0
2001 2001-01 null                   1
2001 2001-02 2001-04                0
2001 2001-02 2001-05                0
2001 2001-02 2001-06                0
2001 2001-02 null                   1
2001 2001-03 2001-07                0
2001 2001-03 2001-08                0
2001 2001-03 2001-09                0
2001 2001-03 null                   1
2001 2001-04 2001-10                0
2001 2001-04 2001-11                0
2001 2001-04 2001-12                0
2001 2001-04 null                   1
2001 null    null                   3
null null    null                   7

18 rows selected.
```

<a id="fd268ffdd95f2b3b"></a>
## GROUPING_ID

<a id="9942a746a2b944a5"></a>
### Syntax

```
GROUPING_ID( expr [, expr]... )
```

<a id="5b29b65d43e2b0f4"></a>
### Description

It is the same as the GROUPING function. In other words, it is an alias for GROUPING.

<a id="ebc4032c6cf2d850"></a>
### Example

```
\EXPLAIN PLAN
SELECT 
       calendar_year as year 
     , calendar_quarter_desc as quarter
     , calendar_month_desc as month
     , GROUPING_ID( calendar_year, calendar_quarter_desc, calendar_month_desc ) as grouping_id_func
  FROM sales, times
 WHERE sales.time_id=times.time_id 
   AND times.calendar_year = 2001
   AND sales.cust_id < 1000 AND sales.prod_id > 142 AND sales.channel_id > 2
 GROUP BY ROLLUP(calendar_year, calendar_quarter_desc, calendar_month_desc)
 ORDER BY 1, 2, 3;  

YEAR QUARTER MONTH   GROUPING_ID_FUNC
---- ------- ------- ----------------
2001 2001-01 2001-01                0
2001 2001-01 2001-02                0
2001 2001-01 2001-03                0
2001 2001-01 null                   1
2001 2001-02 2001-04                0
2001 2001-02 2001-05                0
2001 2001-02 2001-06                0
2001 2001-02 null                   1
2001 2001-03 2001-07                0
2001 2001-03 2001-08                0
2001 2001-03 2001-09                0
2001 2001-03 null                   1
2001 2001-04 2001-10                0
2001 2001-04 2001-11                0
2001 2001-04 2001-12                0
2001 2001-04 null                   1
2001 null    null                   3
null null    null                   7

18 rows selected.
```

<a id="d60f8977301c682f"></a>
## GSI_PHYSICAL_STATS

<a id="81a8aef5473af2eb"></a>
### Syntax

```
GSI_PHYSICAL_STATS( [schema_name.]table_name [,sampling_ratio_value] )
```

<a id="323558571a57cebc"></a>
### Description

GSI_PHYSICAL_STATS is a function that returns page fragmentation information for the global secondary index of a table in a cluster environment.

The input parameter table_name must be specified as an identifier, and an error is raised if the corresponding object is not a base table.

The input parameter sampling_ratio_value represents the percentage (%) of the total pages owned by the object that will be accessed for analysis.  
By randomly sampling and analyzing only a subset of pages instead of processing all pages, the operation can be performed more quickly and efficiently.  
The Used and Fragmented values in the result represent the sizes analyzed based on the sampled pages, not the total allocated pages.  
If this parameter is omitted, a default value of 100% is applied, and all pages are analyzed.  
The valid range of this value is 1 to 100. An error is returned if the value is outside this range.

The result type is VARCHAR and includes the fields Page, Used, and Fragmented.  
• Page: The total number of pages allocated to the global secondary index.  
• Used: The size of the used space, which is the sum of the page header size and the size of the stored data. The unit is bytes.  
• Fragmented: The size of the fragmented space, in bytes.

> This function provides valid information only in a cluster system.  
> In addition, GLOBAL_DUAL can be used to retrieve this information from all nodes in the cluster.

<a id="b0e62b61ad905240"></a>
### Example

- When using DUAL
    - Returns the object information of the connected node.
    - In a cluster environment, a cluster domain can be specified.

```
gSQL> SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(T1) FROM DUAL;
CLUSTER_MEMBER_NAME GSI_PHYSICAL_STATS(T1)                      
------------------- --------------------------------------------
G1N1                Page: 384, Used: 1703308, Fragmented: 766659
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(PUBLIC.T1) FROM DUAL;
CLUSTER_MEMBER_NAME GSI_PHYSICAL_STATS(PUBLIC.T1)               
------------------- --------------------------------------------
G1N1                Page: 384, Used: 1703308, Fragmented: 766659
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(PUBLIC.T1, 50) FROM DUAL;
CLUSTER_MEMBER_NAME GSI_PHYSICAL_STATS(PUBLIC.T1, 50)          
------------------- -------------------------------------------
G1N1                Page: 384, Used: 821311, Fragmented: 368207
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(T1) FROM DUAL@G1N1
      UNION ALL
      SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(T1) FROM DUAL@G2N1
      UNION ALL
      SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(T1) FROM DUAL@G3N1;
CLUSTER_MEMBER_NAME GSI_PHYSICAL_STATS(T1)                         
------------------- -----------------------------------------------
G1N1                Page: 384, Used: 1703308, Fragmented: 766659   
G2N1                Page: 1088, Used: 5115758, Fragmented: 2300000 
G3N1                Page: 2080, Used: 10226411, Fragmented: 4600000
3 rows selected.
```

- When using GLOBAL_DUAL
    - Returns the object information from all nodes in the cluster environment.
    - A cluster domain can be specified.

```
gSQL> SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(PUBLIC.T1, 50)
        FROM GLOBAL_DUAL
      ORDER BY CLUSTER_MEMBER_NAME;
CLUSTER_MEMBER_NAME GSI_PHYSICAL_STATS(PUBLIC.T1, 50)             
------------------- ----------------------------------------------
G1N1                Page: 384, Used: 887714, Fragmented: 398199   
G1N2                Page: 384, Used: 775345, Fragmented: 347438   
G2N1                Page: 1088, Used: 2603073, Fragmented: 1175875
G2N2                Page: 1088, Used: 2669476, Fragmented: 1205867
G3N1                Page: 2080, Used: 5021814, Fragmented: 2265086
G3N2                Page: 2080, Used: 5129068, Fragmented: 2313547
6 rows selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(PUBLIC.T1, 50)
        FROM GLOBAL_DUAL@G1N1|G2N1|G3N1
      ORDER BY CLUSTER_MEMBER_NAME;
CLUSTER_MEMBER_NAME GSI_PHYSICAL_STATS(PUBLIC.T1, 50)             
------------------- ----------------------------------------------
G1N1                Page: 384, Used: 851955, Fragmented: 382053   
G2N1                Page: 1088, Used: 2700097, Fragmented: 1219736
G3N1                Page: 2080, Used: 5384404, Fragmented: 2428961
3 rows selected.
```

<a id="4eb497bc2b25806e"></a>
## HASH32

<a id="3523adaf77897b15"></a>
### Syntax

```
HASH32( expr [, expr]... )
```

<a id="548ba8af6c2c2ae8"></a>
### Description

The HASH32 function calculates and returns the hash value of the provided expr arguments.

At least one argument must be specified, and up to a maximum of 32 arguments can be provided.  
If any of the input arguments is NULL, the result will be NULL.

The return type is NATIVE_INTEGER.

<a id="fddeb0a55f49cbab"></a>
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

<a id="86c83702c5f76005"></a>
## HEX

<a id="f0cbbf0f2f5b7fb7"></a>
### Syntax

```
HEX( str )
```

<a id="76a9488d04bab96d"></a>
### Description

It returns the str argument as a hexadecimal character.  
The str argument can be a character type such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING, a type that can be converted to a character type, or a binary character type such as BINARY, BINARY VARYING, or BINARY LONG VARYING.  
The result type is a character type, such as CHARACTER VARYING or CHARACTER LONG VARYING.

If str is NULL, the result will also be NULL.

If the argument of the HEX function is a numeric type, it returns an error.   
To convert a decimal number to a hexadecimal number, use the TO_CHAR() function with the 'X' number format.  
e.g. TO_CHAR( 255, 'XX' )

For more information, refer to [UNHEX](#dc778c3715262f05).

<a id="96c0c41e9de8a185"></a>
### Example

```
gSQL> SELECT HEX( 'abc' ) FROM DUAL;
HEX( 'abc' )
------------
616263      
1 row selected.
```

<a id="483bdb639e6046de"></a>
## INDEX_PHYSICAL_STATS

<a id="00b1d69cbb41fb2b"></a>
### Syntax

```
INDEX_PHYSICAL_STATS( [schema_name.]index_name [,sampling_ratio_value] )
```

<a id="3c8b902f5ca2701f"></a>
### Description

INDEX_PHYSICAL_STATS is a function that returns fragmentation information for the pages allocated to an index.

The input parameter index_name must be specified as an identifier, and an error is raised if the corresponding object is not an index.

The input parameter sampling_ratio_value represents the percentage (%) of the total pages owned by the object that will be accessed for analysis.   
By randomly sampling and analyzing only a subset of pages instead of processing all pages, the operation can be performed more quickly and efficiently.   
The Used and Fragmented values in the result represent the sizes analyzed based on the sampled pages, not the total allocated pages.   
If this parameter is omitted, a default value of 100% is applied, and all pages are analyzed.  
The valid range of this value is 1 to 100. An error is returned if the value is outside this range.

The result type is VARCHAR and includes the fields Page, Used, and Fragmented.  
• Page: The total number of pages allocated to the index.  
• Used: The size of the used space, which is the sum of the page header size and the size of the stored data. The unit is bytes.  
• Fragmented: The size of the fragmented space, in bytes.

> GLOBAL_DUAL can be used to retrieve this information from all nodes in the cluster.

<a id="b6b816f66a5f4893"></a>
### Example

- When using DUAL
    - Returns the object information of the connected node.
    - In a cluster environment, a cluster domain can be specified.

```
gSQL> SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(T1_UIDX1) FROM DUAL;
CLUSTER_MEMBER_NAME INDEX_PHYSICAL_STATS(T1_UIDX1)              
------------------- --------------------------------------------
G1N1                Page: 480, Used: 2026050, Fragmented: 892587
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1) FROM DUAL;
CLUSTER_MEMBER_NAME INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1)       
------------------- --------------------------------------------
G1N1                Page: 480, Used: 2026050, Fragmented: 892587
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1, 50) FROM DUAL;
CLUSTER_MEMBER_NAME INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1, 50)   
------------------- --------------------------------------------
G1N1                Page: 480, Used: 1136487, Fragmented: 506293
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(T1_UIDX1) FROM DUAL@G1N1
      UNION ALL
      SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(T1_UIDX1) FROM DUAL@G2N1
      UNION ALL
      SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(T1_UIDX1) FROM DUAL@G3N1;
CLUSTER_MEMBER_NAME INDEX_PHYSICAL_STATS(T1_UIDX1)                 
------------------- -----------------------------------------------
G1N1                Page: 480, Used: 2026050, Fragmented: 892587   
G2N1                Page: 1280, Used: 6097450, Fragmented: 2697980 
G3N1                Page: 2464, Used: 12182935, Fragmented: 5395960
3 rows selected.
```

- When using GLOBAL_DUAL
    - Returns the object information from all nodes in the cluster environment.
    - A cluster domain can be specified.

```
gSQL> SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1, 50)
        FROM GLOBAL_DUAL
      ORDER BY CLUSTER_MEMBER_NAME;
CLUSTER_MEMBER_NAME INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1, 50)     
------------------- ----------------------------------------------
G1N1                Page: 480, Used: 1146717, Fragmented: 510879  
G1N2                Page: 480, Used: 1115998, Fragmented: 497144  
G2N1                Page: 1280, Used: 3110836, Fragmented: 1371868
G2N2                Page: 1280, Used: 3142877, Fragmented: 1390133
G3N1                Page: 2464, Used: 6072430, Fragmented: 2687620
G3N2                Page: 2464, Used: 6177784, Fragmented: 2737856
6 rows selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1, 50)
        FROM GLOBAL_DUAL@G1N1|G2N1|G3N1
      ORDER BY CLUSTER_MEMBER_NAME;
CLUSTER_MEMBER_NAME INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1, 50)     
------------------- ----------------------------------------------
G1N1                Page: 480, Used: 1213355, Fragmented: 540555  
G2N1                Page: 1280, Used: 3102215, Fragmented: 1369573
G3N1                Page: 2464, Used: 6347994, Fragmented: 2810966
3 rows selected.
```

<a id="2bd35ece6f4fc38a"></a>
## INITCAP

<a id="7911629f47cbb4ae"></a>
### Syntax

```
INITCAP( str )
```

<a id="1726fc5aeeb9d7ba"></a>
### Description

It converts the first letter of each word in the string str to uppercase and all other letters to lowercase, then returns the result.

The str data type can be a character type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

Each word in the string is separated by whitespace or characters that are not alphanumeric.  
If str is NULL, the result will also be NULL.

The return type is the same as the str argument's datatype.

<a id="3441288eadce3dec"></a>
### Example

```
gSQL> SELECT INITCAP( 'hi GLIESE' ) AS RESULT FROM DUAL;
RESULT   
---------
Hi Gliese
1 row selected.
```

<a id="d8ca8cd4bcc08919"></a>
## INSTR

<a id="b29ea62acb2743ed"></a>
### Syntax

```
INSTR( str, substr [, position [, occurrence ] ] )
```

<a id="5dc6402d784a5c6b"></a>
### Description

It search for the occurrence-th substr starting from the position in str and returns its location.

The data types of the str and substr arguments can be character types such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or binary character types such as BINARY, BINARY VARYING, or BINARY LONG VARYING.

The position and occurrence arguments can be of a numeric data type.

If position and occurrence are omitted, the default value is 1.  
Both position and occurrence start from 1, and they are calculated in character units according to character set (not in byte units).

The position represents the first position to search substr in str, it must be a positive integer and cannot be zero.

- If the position is positive: It searches for the position of substr by comparing from the beginning of str to the right until it finds the substring.
- If the position is negative: It searches for the position of substr by comparing from the end of str to the left until it finds the substring.
- If the position is 0: The result is 0.

The occurrence refers to the number of times the substr repeats in str, and it must be a positive integer.

If any of the input arguments is NULL, the result will also be NULL.

<a id="f93562b7f3759a51"></a>
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

<a id="63c4885c31474998"></a>
## JSON_ARRAY

<a id="9589fd8edf730221"></a>
### Syntax

```
JSON_ARRAY( [ value_expression [, ...] ]
            [<JSON constructor null clause>]
            [<JSON output clause>]
          )
```

For more information about the &lt;JSON constructor null clause&gt;, refer to the [JSON Constructor Null Clause](11-sql-elements.md#917c50e61800ff6a) section.

For more information about the &lt;JSON output clause&gt;, refer to the [JSON Output Clause](11-sql-elements.md#91fe9ef765ec473f) section.

<a id="e6adabf1ea5a9828"></a>
### Description

JSON_ARRAY returns zero or more expressions as a JSON array string.

The JSON constructor null clause is an option that specifies how to handle SQL null values.  
If not specified, the default is ABSENT ON NULL.

The JSON output clause is an option that allows control over the data type and output format of the string generated by the function.  
The result type can be specified by declaring a data type. If not specified, the default is VARCHAR(4000).  
The output format of the JSON string can be changed by specifying the PRETTY option.

<a id="30f4721a8cf9b206"></a>
### Example

```
CREATE TABLE accounts ( name VARCHAR(20), balances INTEGER );
INSERT INTO accounts VALUES ( 'Alice', 50000 );
INSERT INTO accounts VALUES ( 'Bob', NULL );
INSERT INTO accounts VALUES ( 'Chris', 1000 );

gSQL> SELECT JSON_ARRAY( name, balances ) AS res_json_array
        FROM accounts;

RES_JSON_ARRAY 
---------------
["Alice",50000]
["Bob"]        
["Chris",1000] 

3 rows selected.
```

<a id="7bc8aa387314ee48"></a>
## JSON_ARRAYAGG

<a id="5b4dfbd63e9d57cc"></a>
### Syntax

```
JSON_ARRAYAGG( value_expression
               [<JSON array aggregate order by clause>]
               [<JSON constructor null clause>]
               [<JSON output clause>]
             ) [ FILTER ( [ WHERE ] condition )
```

For more information about the &lt;JSON array aggregate order by clause&gt; refer to the [JSON Array Aggregate Order By Clause](11-sql-elements.md#d705909cfd7dce0a) section.

For more information about the &lt;JSON constructor null clause&gt;, refer to the [JSON Constructor Null Clause](11-sql-elements.md#917c50e61800ff6a) section.

For more information about the &lt;JSON output clause&gt;, refer to the [JSON Output Clause](11-sql-elements.md#91fe9ef765ec473f) section.

If a FILTER is specified, aggregation is performed only on values that satisfy the specified condition.

<a id="2b4ff810e2cd4a39"></a>
### Description

JSON_ARRAYAGG is an aggregation function that concatenates value expressions and returns a single JSON array string row.

The JSON array aggregate order by clause is an option that sorts JSON array values for output.

The JSON constructor null clause is an option that specifies how to handle SQL null values.   
If not specified, the default is ABSENT ON NULL.

The JSON output clause is an option that allows control over the data type and output format of the string generated by the function.  
The result type can be specified by declaring a data type. If not specified, the default is VARCHAR(4000).  
The output format of the JSON string can be changed by specifying the PRETTY option.

<a id="8c124aac8d7d33a9"></a>
### Example

```
CREATE TABLE accounts ( name VARCHAR(20), balances INTEGER );
INSERT INTO accounts VALUES ( 'Alice', 50000 );
INSERT INTO accounts VALUES ( 'Bob', NULL );
INSERT INTO accounts VALUES ( 'Chris', 1000 );

gSQL> SELECT JSON_ARRAYAGG( name ) AS name_arrayagg,
             JSON_ARRAYAGG( balances ) AS balances_arrayagg
        FROM accounts; 

NAME_ARRAYAGG           BALANCES_ARRAYAGG
----------------------- -----------------
["Alice","Bob","Chris"] [50000,1000]     

1 row selected.

gSQL> SELECT JSON_ARRAYAGG( name ) 
             FILTER ( balances > 10000 ) AS name_arrayagg,
             JSON_ARRAYAGG( balances ) 
             FILTER ( balances > 10000 ) AS balances_arrayagg
        FROM accounts; 

NAME_ARRAYAGG BALANCES_ARRAYAGG
------------- -----------------
["Alice"]     [50000]          

1 row selected.
```

<a id="b3c3b1418c509029"></a>
## JSON_ARRAYAGG() OVER

<a id="5a59fa6f99e81f01"></a>
### Syntax

```
JSON_ARRAYAGG( value_expression
               [<JSON array aggregate order by clause>]
               [<JSON constructor null clause>]
               [<JSON output clause>]
             ) OVER < window name or specification >
```

For more information about the &lt;JSON array aggregate order by clause&gt; refer to the [JSON Array Aggregate Order By Clause](11-sql-elements.md#d705909cfd7dce0a) section.

For more information about the &lt;JSON constructor null clause&gt;, refer to the [JSON Constructor Null Clause](11-sql-elements.md#917c50e61800ff6a) section.

For more information about the &lt;JSON output clause&gt;, refer to the [JSON Output Clause](11-sql-elements.md#91fe9ef765ec473f) section.

For more information about the &lt;window name or specification&gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49) section.

<a id="efd5d993c2c4e66a"></a>
### Description

JSON_ARRAYAGG is a window function that concatenates value expressions within the window frame to generate a JSON array string.

The JSON array aggregate order by clause is an option that sorts JSON array values for output.

The JSON constructor null clause is an option that specifies how to handle SQL null values.   
If not specified, the default is ABSENT ON NULL.

The JSON output clause is an option that allows control over the data type and output format of the string generated by the function.  
The result type can be specified by declaring a data type. If not specified, the default is VARCHAR(4000).   
The output format of the JSON string can be changed by specifying the PRETTY option.

<a id="5e5481caa4eadbe1"></a>
### Example

```
CREATE TABLE accounts ( name VARCHAR(20), balances INTEGER );
INSERT INTO accounts VALUES ( 'Alice', 50000 );
INSERT INTO accounts VALUES ( 'Bob', NULL );
INSERT INTO accounts VALUES ( 'Chris', 1000 );

gSQL> SELECT JSON_ARRAYAGG( name ) OVER ( ORDER BY balances DESC NULLS LAST ) AS name_arrayagg_over,
             JSON_ARRAYAGG( balances ) OVER ( ORDER BY balances DESC NULLS LAST ) AS balances_arrayagg_over
        FROM accounts;

NAME_ARRAYAGG_OVER      BALANCES_ARRAYAGG_OVER
----------------------- ----------------------
["Alice"]               [50000]               
["Alice","Chris"]       [50000,1000]          
["Alice","Chris","Bob"] [50000,1000]          

3 rows selected.
```

<a id="fbd9eb4c70306dc1"></a>
## JSON_OBJECT

<a id="9dec75123afea2b6"></a>
### Syntax

```
JSON_OBJECT( [ <JSON name and value> [, ...] ]
             [ <JSON constuctor null clause> ]
             [ <JSON key uniqueness constraint> ]
             [ <JSON output clause> ]
           )

<JSON name and value> ::=
    [KEY] <JSON name> VALUE <value_expression>
  | <JSON name> : <value_expression>
```

For more information about the &lt;JSON constructor null clause&gt;, refer to the [JSON Constructor Null Clause](11-sql-elements.md#917c50e61800ff6a) section.

For more information about the &lt; JSON key uniqueness constraint &gt;, refer to the [JSON Key Uniqueness Constraint](11-sql-elements.md#2b244b19e881dcb5) section.

For more information about the &lt;JSON output clause&gt;, refer to the [JSON Output Clause](11-sql-elements.md#91fe9ef765ec473f) section.

<a id="237d2a71b45ec31f"></a>
### Description

JSON_OBJECT returns zero or more JSON name and values as a JSON object string.  
A JSON name must be an expression that can be represented as a character string.

The JSON constructor null clause is an option that specifies how to handle SQL null values.   
If not specified, the default is NULL ON NULL.

The JSON key uniqueness constraint is an option that determines whether duplicate keys are allowed in a JSON object.   
If not specified, the default is WITHOUT UNIQUE KEYS.

The JSON output clause is an option that allows control over the data type and output format of the string generated by the function.  
The result type can be specified by declaring a data type. If not specified, the default is VARCHAR(4000).   
The output format of the JSON string can be changed by specifying the PRETTY option.

<a id="9637a882ac655947"></a>
### Example

```
CREATE TABLE accounts ( name VARCHAR(20), balances INTEGER );
INSERT INTO accounts VALUES ( 'Alice', 50000 );
INSERT INTO accounts VALUES ( 'Bob', NULL );
INSERT INTO accounts VALUES ( 'Chris', 1000 );

gSQL> SELECT JSON_OBJECT( name VALUE balances ) AS res_json_object
       FROM accounts;

RES_JSON_OBJECT
---------------
{"Alice":50000}
{"Bob":null}   
{"Chris":1000} 

3 rows selected.
```

<a id="61c76e5d901661ed"></a>
## JSON_OBJECTAGG

<a id="66088c728dff55e3"></a>
### Syntax

```
JSON_OBJECTAGG( <JSON name and value>
                [ <JSON constructor null clause> ]
                [ <JSON key uniqueness constraint> ]
                [ <JSON output clause> ]
              ) [ FILTER ( [ WHERE ] condition ) ]

<JSON name and value> ::=
    [KEY] <JSON name> VALUE <value_expression>
  | <JSON name> : <value_expression>
```

For more information about the &lt;JSON constructor null clause&gt;, refer to the [JSON Constructor Null Clause](11-sql-elements.md#917c50e61800ff6a) section.

For more information about the &lt; JSON key uniqueness constraint &gt;, refer to the [JSON Key Uniqueness Constraint](11-sql-elements.md#2b244b19e881dcb5) section.

For more information about the &lt;JSON output clause&gt;, refer to the [JSON Output Clause](11-sql-elements.md#91fe9ef765ec473f) section.

If a FILTER is specified, aggregation is performed only on values that satisfy the specified condition.

<a id="73f9e0ef299a3a2e"></a>
### Description

JSON_OBJECTAGG is an aggregation function that concatenates JSON name-value pairs and returns a single JSON object string row.  
A JSON name must be an expression that can be represented as a character string.

The JSON constructor null clause is an option that specifies how to handle SQL null values.   
If not specified, the default is NULL ON NULL.

The JSON key uniqueness constraint is an option that determines whether duplicate keys are allowed in a JSON object.   
If not specified, the default is WITHOUT UNIQUE KEYS.

The JSON output clause is an option that allows control over the data type and output format of the string generated by the function.  
The result type can be specified by declaring a data type. If not specified, the default is VARCHAR(4000).   
The output format of the JSON string can be changed by specifying the PRETTY option.

<a id="fe3824b99300305a"></a>
### Example

```
CREATE TABLE accounts ( name VARCHAR(20), balances INTEGER );
INSERT INTO accounts VALUES ( 'Alice', 50000 );
INSERT INTO accounts VALUES ( 'Bob', NULL );
INSERT INTO accounts VALUES ( 'Chris', 1000 );

gSQL> SELECT JSON_OBJECTAGG( name VALUE balances ) AS res_json_objectagg
        FROM accounts;

RES_JSON_OBJECTAGG                     
---------------------------------------
{"Alice":50000,"Bob":null,"Chris":1000}

1 row selected.

gSQL> SELECT JSON_OBJECTAGG( name VALUE balances ) 
                    FILTER ( balances > 10000 ) AS res_json_objectagg
       FROM accounts;   

RES_JSON_OBJECTAGG
------------------
{"Alice":50000}   

1 row selected.
```

<a id="821bcca33f74cbfd"></a>
## JSON_OBJECTAGG() OVER

<a id="85c76dcea6b1dc45"></a>
### Syntax

```
JSON_OBJECTAGG( <JSON name and value>
                [ <JSON constructor null clause> ]
                [ <JSON key uniqueness constraint> ]
                [ <JSON output clause> ]
              ) OVER < window name or specification >

<JSON name and value> ::=
    [KEY] <JSON name> VALUE <value_expression>
  | <JSON name> : <value_expression>
```

For more information about the &lt;JSON constructor null clause&gt;, refer to the [JSON Constructor Null Clause](11-sql-elements.md#917c50e61800ff6a) section.

For more information about the &lt; JSON key uniqueness constraint &gt;, refer to the [JSON Key Uniqueness Constraint](11-sql-elements.md#2b244b19e881dcb5) section.

For more information about the &lt;JSON output clause&gt;, refer to the [JSON Output Clause](11-sql-elements.md#91fe9ef765ec473f) section.

For more information about the &lt;window name or specification&gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49) section.

<a id="ea7cd58a6ee5363d"></a>
### Description

JSON_OBJECTAGG is a window function that concatenates JSON name-value pairs within the window frame to generate a JSON object string.  
A JSON name must be an expression that can be represented as a character string.

The JSON constructor null clause is an option that specifies how to handle SQL null values.   
If not specified, the default is NULL ON NULL.

The JSON key uniqueness constraint is an option that determines whether duplicate keys are allowed in a JSON object.   
If not specified, the default is WITHOUT UNIQUE KEYS.

The JSON output clause is an option that allows control over the data type and output format of the string generated by the function.  
The result type can be specified by declaring a data type. If not specified, the default is VARCHAR(4000).   
The output format of the JSON string can be changed by specifying the PRETTY option.

<a id="526931e22ea84ef2"></a>
### Example

```
CREATE TABLE accounts ( name VARCHAR(20), balances INTEGER );
INSERT INTO accounts VALUES ( 'Alice', 50000 );
INSERT INTO accounts VALUES ( 'Bob', NULL );
INSERT INTO accounts VALUES ( 'Chris', 1000 );

gSQL> SELECT JSON_OBJECTAGG( name VALUE balances ) OVER ( ORDER BY balances DESC NULLS LAST ) AS res_json_objectagg_over
        FROM accounts;
RES_JSON_OBJECTAGG_OVER                
---------------------------------------
{"Alice":50000}                        
{"Alice":50000,"Chris":1000}           
{"Alice":50000,"Chris":1000,"Bob":null}

3 rows selected.
```

<a id="335ae138bc8c502e"></a>
## LAG() OVER

<a id="b6bf87408bb770be"></a>
### Syntax

```
LAG ( expr [, offset [, default ] ] ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

LAG ( expr [ RESPECT NULLS | IGNORE NULLS ] [, offset [, default ] ] ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="aae65872982e188b"></a>
### Description

The window function LAG returns the value of the row ahead of the current row by the specified offset.  
If the offset is outside the window range, it returns the default value.

If the offset and default values are not specified, they are set to their default values.    
The default offset value is 1, and the default value for the default is NULL.

RESPECT NULLS returns the value of the row ahead by the specified offset, including NULLs.  
IGNORE NULLS returns the value of the row ahead by the specified offset, excluding NULLs.  
If not specified, the default value is RESPECT NULLS.

A window frame can not be used.

<a id="b21e31ade3646f18"></a>
### Example

```
gSQL> SELECT department_id, employee_id, manager_id,
             LAG( manager_id ) OVER ( ORDER BY employee_id ) AS lag
        FROM employees
       WHERE department_id = 90;

DEPARTMENT_ID EMPLOYEE_ID MANAGER_ID  LAG
------------- ----------- ---------- ----
           90         100       null null
           90         101        100 null
           90         102        100  100

3 rows selected.
```

The following is an example of how to specify the offset.

```
gSQL> SELECT department_id, employee_id, manager_id,
             LAG( manager_id, 2 ) OVER ( ORDER BY employee_id ) AS lag
        FROM employees
       WHERE department_id = 90;

DEPARTMENT_ID EMPLOYEE_ID MANAGER_ID  LAG
------------- ----------- ---------- ----
           90         100       null null
           90         101        100 null
           90         102        100 null

3 rows selected.
```

The following is an example of how to specify the offset and default values.

```
gSQL> SELECT department_id, employee_id, manager_id,
             LAG( manager_id, 2, 0 ) OVER ( ORDER BY employee_id ) AS lag
        FROM employees
       WHERE department_id = 90;

DEPARTMENT_ID EMPLOYEE_ID MANAGER_ID  LAG
------------- ----------- ---------- ----
           90         100       null    0
           90         101        100    0
           90         102        100 null

3 rows selected.
```

<a id="5c6145cc5b391ab1"></a>
## LAST() OVER

<a id="bb091138668bfffd"></a>
### Syntax

```
aggregation_function KEEP ( DENSE_RANK LAST ORDER BY <sort specification list> ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="c2160b12653662bf"></a>
### Description

The window function LAST sorts the sort specification list used in the *order by* clause within the KEEP clause, then returns the aggregation function value of rows whose DENSE_RANK is last.

The aggregation_functions are AVG, COUNT, COUNT(*), SUM, MAX, MIN, STDDEV, and VARIANCE.

*order by* is not allowed within the window clause.   
A window frame can not be used.

<a id="e957dd03751fe486"></a>
### Example

```
gSQL> SELECT department_id, salary,
           DENSE_RANK() OVER ( ORDER BY department_id ) AS "DENSE_RANK",
           MAX( salary ) KEEP ( DENSE_RANK LAST ORDER BY department_id ) OVER () AS "MAX_LAST"
  FROM employees
 WHERE department_id BETWEEN 90 AND 100;

DEPARTMENT_ID SALARY DENSE_RANK MAX_LAST
------------- ------ ---------- --------
           90  24000          1    12000
           90  17000          1    12000
           90  17000          1    12000
          100  12000          2    12000
          100   9000          2    12000
          100   8200          2    12000
          100   7700          2    12000
          100   7800          2    12000
          100   6900          2    12000

9 rows selected.
```

<a id="3333e5c7caa18122"></a>
## LAST_DAY

<a id="c24cf0d63905749c"></a>
### Syntax

```
LAST_DAY( date )
```

<a id="4b3377a51bf5f5c6"></a>
### Description

It returns the last day of the month that is included in the date.

The data type of the date argument can be DATE, TIMESTAMP, or TIMESTAMP WITH TIME ZONE.  
The return type is always DATE, regardless of the data type of the date argument.  

If the date is NULL, it returns NULL.

<a id="cd6a25a654b10b19"></a>
### Example

```
gSQL> SELECT 
      LAST_DAY( TO_DATE( '2012-07-10', 'YYYY-MM-DD' ) ) AS RESULT FROM DUAL;
RESULT    
----------
2012-07-31
1 row selected.
```

<a id="6034d7de06501d08"></a>
## LAST_IDENTITY_VALUE

<a id="c564823965df89c6"></a>
### Syntax

```
LAST_IDENTITY_VALUE()
```

<a id="bc91bde59b1c25f6"></a>
### Description

It is the most recent value automatically generated for an identity column in the current session, and the result type is NATIVE_BIGINT.

If no automatically generated value exists, it returns NULL.

This function is similar to @@IDENTITY in MS-SQL and LAST_INSERT_ID() in MySQL. Be cautious when using it, as the last altered table determines the value when performing DML on multiple tables, as shown below.

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

To obtain the identity column value created during an INSERT, use the [INSERT INTO name RETURNING .. INTO](20-sql-references-h-z.md#b4cbafb4ebba9b68) statement, as shown below.

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

<a id="889d301e7df7da73"></a>
### Example

The following is an example of how to use the LAST_IDENTITY_VALUE() function.

```
gSQL> CREATE TABLE t1 ( id   INTEGER GENERATED BY DEFAULT AS IDENTITY,
                        name VARCHAR(32) ); 

Table created.

gSQL> COMMIT;

Commit complete.
```

- There is no identity value created in the current session.

```
gSQL> SELECT LAST_IDENTITY_VALUE() FROM dual;

LAST_IDENTITY_VALUE()
---------------------
                 null

1 row selected.
```

- An identity value (1) is automatically generated.

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

- An identity value (2) is automatically generated as the default value.

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

- The user input value does not automatically generate an identity value.

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

<a id="aba2351fe4a17e32"></a>
## LAST_VALUE() OVER

<a id="f1bad941d72e298e"></a>
### Syntax

```
LAST_VALUE ( expr ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

LAST_VALUE ( expr [ RESPECT NULLS | IGNORE NULLS ] ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="ca67ccfa333755fc"></a>
### Description

The window function LAST_VALUE returns the last value of the expr.

RESPECT NULLS returns the last value of rows, including NULLs.   
IGNORE NULLS returns the last value of rows, excluding NULLs.   
If not specified, the default value is RESPECT NULLS.

<a id="b88005dd8a5943a6"></a>
### Example

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , LAST_VALUE( min_price ) OVER ( ORDER BY min_price ) AS "LAST_VALUE"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE LAST_VALUE
--------- ----------
       73         73
      247        247
      731        731
     null       null
     null       null

5 rows selected.
```

The following is an example of specifying IGNORE NULLS for null_treatment.

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , LAST_VALUE( min_price IGNORE NULLS ) OVER ( ORDER BY min_price ) AS "LAST_VALUE"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE LAST_VALUE
--------- ----------
       73         73
      247        247
      731        731
     null        731
     null        731

5 rows selected.
```

<a id="f55af5c9d24fd9f6"></a>
## LEAD() OVER

<a id="435a73198c4653f4"></a>
### Syntax

```
LEAD ( expr [, offset [, default ] ] ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

LEAD ( expr [ RESPECT NULLS | IGNORE NULLS ] [, offset [, default ] ] ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="e09216dfa2fddaa7"></a>
### Description

The window function LEAD returns the value of the row behind the current row by the specified offset.   
If the offset is outside of the window range, it returns the default value.

If the offset and default values are not specified, they are set to their default values.    
The default offset value is 1, and the default value for the default is NULL.

RESPECT NULLS returns the value of the row behind by the specified offset, including NULLs.  
IGNORE NULLS returns the value of the row behind by the specified offset, excluding NULLs.  
If not specified, the default value is RESPECT NULLS.

A window frame can not be used.

<a id="2ac1a602cfadb296"></a>
### Example

```
gSQL> SELECT department_id, employee_id, manager_id,
             LEAD( manager_id ) OVER ( ORDER BY employee_id DESC ) AS lead
        FROM employees
       WHERE department_id = 90;

DEPARTMENT_ID EMPLOYEE_ID MANAGER_ID LEAD
------------- ----------- ---------- ----
           90         102        100  100
           90         101        100 null
           90         100       null null

3 rows selected.
```

The following is an example of how to specify the offset.

```
gSQL> SELECT department_id, employee_id, manager_id,
             LEAD( manager_id, 2 ) OVER ( ORDER BY employee_id DESC ) AS lead
        FROM employees
       WHERE department_id = 90;

DEPARTMENT_ID EMPLOYEE_ID MANAGER_ID LEAD
------------- ----------- ---------- ----
           90         102        100 null
           90         101        100 null
           90         100       null null

3 rows selected.
```

The following is an example of how to specify the offset and default values.

```
gSQL> SELECT department_id, employee_id, manager_id,
             LEAD( manager_id, 2, 0 ) OVER ( ORDER BY employee_id DESC ) AS lead
        FROM employees
       WHERE department_id = 90;

DEPARTMENT_ID EMPLOYEE_ID MANAGER_ID LEAD
------------- ----------- ---------- ----
           90         102        100 null
           90         101        100    0
           90         100       null    0

3 rows selected.
```

<a id="14e8563c1aac8330"></a>
## LEAST

<a id="0d845e69f52c5b07"></a>
### Syntax

```
LEAST( expr1 [, expr2, ... exprn ] )
```

<a id="335739fe09e7bf2b"></a>
### Description

It returns the smallest value among the expr arguments provided.

If any expr argument is NULL, the result will be NULL.

The result type is determined based on the data type of expr1 (the first expr).   
If the data type of expr1 is numeric or character, the result type is determined to be a type that can include the range of expr1, ..., exprN each.  
If all of expr1, ..., exprN are defined as CHAR type, then all exprs are compared as VARCHAR type, and the result type is determined to be VARCHAR.

<a id="9f01fa044bbbe4cc"></a>
### Example

```
gSQL> SELECT LEAST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="dec729ca5cf2693b"></a>
## LENGTH

<a id="0418d25c2f36d26d"></a>
### Syntax

```
LENGTH( str )
```

<a id="572d37c702a07304"></a>
### Description

It is an alias of [CHAR_LENGTH](#bfc30a82c549098c).

<a id="6c478c460b1567bd"></a>
### Example

Multi-byte character set: (e.g.UTF8)

```
gSQL> SELECT LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="c5f46ba504cefe4a"></a>
## LENGTHB

<a id="81abf1f3e22608b1"></a>
### Syntax

```
LENGTHB( str )
```

<a id="9827c256773f5be9"></a>
### Description

It is an alias of [OCTET_LENGTH](#ddbc8d3776b14b1b).  
For more information, refer to [BYTE_LENGTH](#a55aa7d89b47253c).

<a id="138059814b9dfdff"></a>
### Example

- Multi-byte character set (e.g.UTF8): 1 byte character

```
gSQL> SELECT LENGTHB( 'OCTET_LENGTH' ) AS RESULT_1BYTE_CHARACTERS 
        FROM DUAL;
RESULT_1BYTE_CHARACTERS
-----------------------
                     12
1 row selected.
```

- Multi-byte character set (e.g.UTF8): 2 byte character

```
gSQL> SELECT LENGTHB( 'αβ' ) AS RESULT_2BYTE_CHARACTERS FROM DUAL;
RESULT_2BYTE_CHARACTERS
-----------------------
                      4
1 row selected.
```

<a id="b4aed9657b112c16"></a>
## LISTAGG() OVER

<a id="d9b9cc954580cc4c"></a>
### Syntax

```
LISTAGG( str [, delimiter] ) WITHIN GROUP ( ORDER BY <sort specification list> ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="565d446f68c661ad"></a>
### Description

The window function LISTAGG concatenates str in their sorted order within each group.

Only the PARTITION BY clause can be used in the OVER() clause of LISTAGG.  
It divides the query result set into groups using the OVER() clause.

It sorts the records within the group using WITHIN GROUP ( ORDER BY &lt;sort specification list&gt; ).

It concatenates str in the order of the records sorted within each group.   
If str is NULL, it is excluded.

A delimiter is str connection delimiter, and if omitted, the default value is NULL.

The str can be either a character string or a binary string.   
If str is a character string, the result type is varchar.   
If str is a binary string, the result type is varbinary.

<a id="5b3fc429cbeee680"></a>
### Example

```
gSQL> 
SELECT regionkey,
       name,
       LISTAGG( name ) WITHIN GROUP ( ORDER BY nationkey ) 
                       OVER ( PARTITION BY regionkey ) 
       AS "LISTAGG( name ) RESULT",
       LISTAGG( name, ', ' ) WITHIN GROUP ( ORDER BY nationkey ) 
                             OVER ( PARTITION BY regionkey ) 
       AS "LISTAGG( name, ', ' ) RESULT"
  FROM nation;

REGIONKEY NAME    LISTAGG( name ) RESULT    LISTAGG( name, ', ' ) RESULT
--------- ------- ------------------------- ----------------------------
        1 BRAZIL  BRAZILCANADAPERU          BRAZIL, CANADA, PERU        
        1 CANADA  BRAZILCANADAPERU          BRAZIL, CANADA, PERU        
        1 PERU    BRAZILCANADAPERU          BRAZIL, CANADA, PERU        
        1 null    BRAZILCANADAPERU          BRAZIL, CANADA, PERU        
        2 null    INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 INDIA   INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 null    INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 null    INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 JAPAN   INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 CHINA   INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 null    INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 VIETNAM INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        3 EGYPT   EGYPTIRANIRAQ             EGYPT, IRAN, IRAQ           
        3 IRAN    EGYPTIRANIRAQ             EGYPT, IRAN, IRAQ           
        3 IRAQ    EGYPTIRANIRAQ             EGYPT, IRAN, IRAQ           

15 rows selected.
```

<a id="42927b87e9319c86"></a>
## LN

<a id="2f845b3121cf487b"></a>
### Syntax

```
LN( num )
```

<a id="36751dec07bb78ee"></a>
### Description

It returns the natural logarithm value of num.  

num must be greater than 0.  
If num is NULL, it returns NULL.

<a id="d456d17fb003b1f5"></a>
### Example

```
gSQL> SELECT LN( 2.71828182845905 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="196d1dc7488ff30d"></a>
## LNNVL

<a id="4314a0f8fe154760"></a>
### Syntax

```
LNNVL( expr )
```

<a id="86dfd77c381e07bb"></a>
### Description

The Logical Not Null VaLue (LNNVL) function is similar to the NOT logical operator, but the difference is that it returns TRUE when the input value is NULL, as shown in the following example.

<a id="badc1c862d7424b4"></a>
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

<a id="326df674131c714f"></a>
## LOCAL_GROUP_ID

<a id="6ebf496b9da1e954"></a>
### Syntax

```
LOCAL_GROUP_ID()
```

<a id="9eda14b605962101"></a>
### Description

It returns the cluster group ID for the server that processes a user's query.

> It is valid information in a cluster system.

<a id="bb66250b7a9716e9"></a>
### Example

All rows contain the same value.

```
gSQL> SELECT LOCAL_GROUP_ID() FROM DUAL;

LOCAL_GROUP_ID()
----------------
               1

1 row selected.
```

<a id="1a9dda85030d29dc"></a>
## LOCAL_GROUP_NAME

<a id="99ee54dffce171ab"></a>
### Syntax

```
LOCAL_GROUP_NAME()
```

<a id="93434bc5a6b9edd3"></a>
### Description

It returns the cluster group name for the server that processes a user's query.

> It is valid information in a cluster system.

<a id="5fc28dc0864976e8"></a>
### Example

All rows contain the same value.

```
gSQL> SELECT LOCAL_GROUP_NAME() FROM DUAL;

LOCAL_GROUP_NAME()
------------------
G1                

1 row selected.
```

<a id="577bfde745c2061c"></a>
## LOCAL_MEMBER_ID

<a id="9cfea6b61b39edb2"></a>
### Syntax

```
LOCAL_MEMBER_ID()
```

<a id="ff5d867544a5da1e"></a>
### Description

It returns the cluster member ID for the server that processes a user's query.

> It is valid information in a cluster system.

<a id="e01678092000130c"></a>
### Example

All rows contain the same value.

```
gSQL> SELECT LOCAL_MEMBER_ID() FROM DUAL;

LOCAL_MEMBER_ID()
-----------------
                1

1 row selected.
```

<a id="67e808f06445e48d"></a>
## LOCAL_MEMBER_NAME

<a id="8e83999b84878e05"></a>
### Syntax

```
LOCAL_MEMBER_NAME()
```

<a id="8a956fb9aaddf4a2"></a>
### Description

It returns the cluster member name for the server that processes a user's query.

> It is valid information in a cluster system.

<a id="b47eb29a5be22cee"></a>
### Example

All rows contain the same value.

```
gSQL> SELECT LOCAL_MEMBER_NAME() FROM DUAL;

LOCAL_MEMBER_NAME()
-------------------
G1N1               

1 row selected.
```

<a id="3e18ea582f6a25fa"></a>
## LOCAL_MEMBER_POSITION

<a id="4177ab020ae5cd35"></a>
### Syntax

```
LOCAL_MEMBER_POSITION()
```

<a id="fb27bed5295190e0"></a>
### Description

It returns the cluster member position for the server that processes a user's query.

> It is valid information in a cluster system.

<a id="4bdc304ff3ab4270"></a>
### Example

All rows contain the same value.

```
gSQL> SELECT LOCAL_MEMBER_POSITION() FROM DUAL;

LOCAL_MEMBER_POSITION()
-----------------------
                      0

1 row selected.
```

<a id="c20987197caf3bbc"></a>
## LOCALTIME

<a id="2453ef2df86cae84"></a>
### Syntax

```
LOCALTIME [()]
STATEMENT_LOCALTIME()
```

<a id="4acd7dae59a9ff01"></a>
### Description

The current TIME WITHOUT TIME ZONE type value is obtained based on the session time.

LOCALTIME is an SQL standard function.

The differences among the functions for obtaining the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values within the transaction are the same.  
• LOCALTIME, STATEMENT_LOCALTIME(): All time values within an SQL statement are the same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is returned.

<a id="1ec19dd5ddfe3595"></a>
### Example

All the rows have the same value.

```
gSQL>  SELECT LOCALTIME FROM t1;

LOCALTIME      
---------------
16:17:08.592459
16:17:08.592459
16:17:08.592459

3 rows selected.
```

<a id="9fa35889a1bb6bcb"></a>
## LOCALTIMESTAMP

<a id="67f5d6b611358720"></a>
### Syntax

```
LOCALTIMESTAMP [()]
STATEMENT_LOCALTIMESTAMP()
```

<a id="83b7461600ed3bce"></a>
### Description

The current value of the TIMESTAMP WITHOUT TIME ZONE type is obtained based on the session time.

LOCALTIMESTAMP is an SQL standard function.

The differences among the functions for obtaining the current TIMESTAMP are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All TIMESTAMP values within the transaction are the same.  
• LOCALTIMESTAMP, STATEMENT_LOCALTIMESTAMP(): All TIMESTAMP values within an SQL statement are the same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is returned.

<a id="14a02d76316554fb"></a>
### Example

All rows contain the same value.

```
gSQL> SELECT LOCALTIMESTAMP FROM t1;

LOCALTIMESTAMP            
--------------------------
2013-12-12 16:21:51.790614
2013-12-12 16:21:51.790614
2013-12-12 16:21:51.790614

3 rows selected.
```

<a id="941f72dc33770e54"></a>
## LOG

<a id="40fe18c9dc9020c9"></a>
### Syntax

```
LOG( num2 )
LOG( num1, num2 )
```

<a id="59c37a9dba69f457"></a>
### Description

It returns the logarithm of num2 with base num1.  
If num1 is omitted, the value is calculated with base 10.

num1 must be a positive number, except for 1 and 0, and num2 must be a positive number.

If num1 or num2 is NULL, it returns NULL.

<a id="1554f820025c3d01"></a>
### Example

```
gSQL> SELECT LOG( 100 ) AS RESULT1, LOG( 4, 16 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      2       2
1 row selected.
```

<a id="5f65dfcc71c8119c"></a>
## LOGON_USER

<a id="30c88cbcc202380c"></a>
### Syntax

```
LOGON_USER()
```

<a id="999c111b31854782"></a>
### Description

It returns the currently logged-in user.

User information is managed in three types, as follows.

- Logon user: The user who performed the login, and their identity is maintained until the connection is closed.
- Session user: It is the same as the initial logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: Generally the same as the session user, but it may be temporarily altered internally by the system for access control when using PSM, views, or similar features.
    - The distinction between the session user and current user is similar to the difference between the real user and effective user in Unix systems.

<a id="3c5df4f42ea71f46"></a>
### Example

```
% gsql test test

gSQL> SELECT LOGON_USER() AS result FROM DUAL;

RESULT
------
TEST  

1 row selected.
```

<a id="da1c90e5c6d23d83"></a>
## LOWER

<a id="35a710471b2b9fbb"></a>
### Syntax

```
LOWER( str )
```

<a id="57211082d433cb50"></a>
### Description

It returns the lowercase version of str.

The data type of the str argument can be a character type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.  
If str is NULL, the result will also be NULL.

The return type is the same as the data type of the str argument.

<a id="ad79cfeb9b5bf886"></a>
### Example

```
gSQL> SELECT LOWER( 'SPRING' ) AS RESULT FROM DUAL;
RESULT
------
spring
1 row selected.
```

<a id="fab61635d016946f"></a>
## LPAD

<a id="531853bdc6425348"></a>
### Syntax

```
LPAD( str, length, [, fill] )
```

<a id="e6bdf4f6b967d678"></a>
### Description

It returns the value of str with the specified fill string added to the left side until the length of the string reaches length.

The data type of the str argument can be a character type, such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type, such as BINARY, BINARY VARYING, or BINARY LONG VARYING.

The length argument is a numeric type.

length represents the number of characters, and its maximum range is the maximum PRECISION of the result type.  
If fill is omitted, a whitespace character is added.  
If str is longer than length, str is truncated to the specified length before being returned.  
If any of str, length, or fill is NULL, the result will also be NULL.  
If length is 0 or a negative number, the result will also be NULL.

The following table describes the result types.

**Result type of LPAD**

<a id="0117193834701e2e"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="01eba022d03b31b3"></a>
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

<a id="ffd108b6dd98ff5a"></a>
## LTRIM

<a id="edc2a7f603872246"></a>
### Syntax

```
LTRIM( trim_source [, trim_character ] )
```

<a id="391f7e95add02cad"></a>
### Description

It removes the characters that match trim_character from the left side of trim_source, continuing until there are no more matching characters, and then returns the result.

The data type of the trim_character and trim_source arguments can be a character type, such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type, such as BINARY, BINARY VARYING, or BINARY LONG VARYING.

If either trim_character or trim_source is NULL, the result will be NULL.  
If trim_character is omitted, a single blank space (' ') is used by default.

The following table describes the result types.

**Result type of LTRIM**

<a id="4aac008d929337c3"></a>
| trim_source, trim_character type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="a639990cd0dbb9c1"></a>
### Example

```
gSQL> SELECT LTRIM( '_____LTRIM', '_' ) AS RESULT FROM DUAL;
RESULT
------
LTRIM 
1 row selected.
```

<a id="4e04ee8ff083abc1"></a>
## MAX

<a id="39add2f804dce0d8"></a>
### Syntax

```
MAX( [ ALL | DISTINCT ] expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="6c8b46ad899d7a08"></a>
### Description

It is an aggregate function that returns the maximum value from the exprs of all rows.

If ALL is explicitly specified, the aggregation is performed for all values.  
If DISTINCT is explicitly specified, aggregation is performed for the values excluding duplicates.  
If neither ALL nor DISTINCT is specified, it is treated as if ALL were specified.

The MAX function returns the same result, unaffected by ALL or DISTINCT.

If FILTER is specified, aggregation is performed only on the values that satisfy the condition.

<a id="a35cff30e8415c15"></a>
### Example

```
gSQL> SELECT MAX( c1 ) FROM t1;

MAX(C1)
-------
      3

1 row selected.


gSQL> SELECT MAX( c1 ) FILTER( WHERE c1 < 3 ) FROM t1;

MAX(C1)
-------
      2

1 row selected.
```

<a id="e470bba9db176384"></a>
## MAX() OVER

<a id="282850cc0b991606"></a>
### Syntax

```
MAX ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="7f10dd44b3efd501"></a>
### Description

The window function MAX returns the maximum value of exprs.  
NULL values are excluded from the calculation.

<a id="13d7a6069d46cc55"></a>
### Example

```
gSQL> SELECT product_id AS "PRODUCT_ID", min_price AS "MIN_PRICE"
             , MAX( min_price ) OVER ( ORDER BY product_id ) AS "MAX"
        FROM product_information
       WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE  MAX
---------- --------- ----
      1769      null null
      1770        73   73
      2378       247  247
      2382       731  731
      3355      null  731

5 rows selected.
```

<a id="af88b35602436133"></a>
## MEDIAN() OVER

<a id="06d578840ce2deac"></a>
### Syntax

```
MEDIAN ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="d92e3e2665ab26b5"></a>
### Description

The window function MEDIAN returns the median value of rows.  
NULL values are excluded from the calculation.

*order by* is not allowed within the window clause.  
A window frame can not be used.

<a id="e5abc8aec99fb813"></a>
### Example

```
gSQL> SELECT supplier_id, min_price
             , MEDIAN( min_price ) OVER ( PARTITION BY supplier_id ) AS "MEDIAN"
        FROM product_information
       WHERE supplier_id = 102050;

SUPPLIER_ID MIN_PRICE MEDIAN
----------- --------- ------
     102050        73    247
     102050       247    247
     102050       731    247
     102050      null    247
     102050      null    247

5 rows selected.
```

<a id="3eaa7160a04afaa7"></a>
## MIN

<a id="d62bfa8e4b8a42d6"></a>
### Syntax

```
MIN( [ ALL | DISTINCT ] expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="b9a0c25b898daa83"></a>
### Description

It is an aggregate function that returns the minimum value from the exprs of all rows.

If ALL is explicitly specified, the aggregation is performed for all values.  
If DISTINCT is explicitly specified, aggregation is performed for the values excluding duplicates.  
If neither ALL nor DISTINCT is specified, it is treated as if ALL were specified.

The MIN function returns the same result, unaffected by ALL or DISTINCT.

If FILTER is specified, aggregation is performed only on the values that satisfy the condition.

<a id="5047402007e09b15"></a>
### Example

```
gSQL> SELECT MIN( c1 ) FROM t1;

MIN(C1)
-------
      1

1 row selected.


gSQL> SELECT MIN( c1 ) FILTER( WHERE c1 > 1 ) FROM t1;

MIN(C1)
-------
      2

1 row selected.
```

<a id="1759858523c292e5"></a>
## MIN() OVER

<a id="f6f4e4832740ed37"></a>
### Syntax

```
MIN ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="a5df2e3e19ad5b3a"></a>
### Description

The window function MIN returns the minimum value of exprs.   
NULL values are excluded from the calculation.

<a id="662a21e22c9d2dcb"></a>
### Example

```
gSQL> SELECT product_id AS "PRODUCT_ID", min_price AS "MIN_PRICE"
             , MIN( min_price ) OVER ( ORDER BY product_id DESC ) AS "MIN"
        FROM product_information
       WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE  MIN
---------- --------- ----
      3355      null null
      2382       731  731
      2378       247  247
      1770        73   73
      1769      null   73

5 rows selected.
```

<a id="0013864abae4530e"></a>
## MOD

<a id="2497997aac0cd2be"></a>
### Syntax

```
MOD( num1, num2 )
```

<a id="e64468a4bf6703bf"></a>
### Description

It divides num1 by num2 and returns the remainder.  

Both num1 and num2 arguments can be of a numeric data type.  
If num2 is 0, an error is returned.  
If either the num1 or num2 argument is NULL, the result will also be NULL.

<a id="1ef62f0dafdfdd20"></a>
### Example

```
gSQL> SELECT MOD(5, 4) AS RESULT1, MOD(-5, 4) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1      -1
1 row selected.
```

<a id="e794dcf77475be45"></a>
## MONTHS_BETWEEN

<a id="6ebb6745194ecbf2"></a>
### Syntax

```
MONTHS_BETWEEN( date1, date2 )
```

<a id="24b159e8423d6e27"></a>
### Description

MONTHS_BETWEEN returns the number of months by dividing the number of days between date2 and date1 by 31.

If either date1 or date2 is NULL, the result will also be NULL.  
The date1 and date2 arguments can be of type DATE, TIMESTAMP, or TIMESTAMP WITH TIME ZONE.

The result type is NUMBER.

> If the same date (e.g., 2014-01-15 and 2014-02-15) or the last day of the month (e.g., 2014-08-31 and 2014-09-30) is included in both date1 and date2, the result will be an integer, regardless of any discrepancy in the timestamp portion (if present).

<a id="5f5799267e6f7d9e"></a>
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

<a id="a54caf77b7b948ba"></a>
## NEXT_DAY

<a id="fa9a5cbfa15c5d19"></a>
### Syntax

```
NEXT_DAY( date, day )
```

<a id="407697b2be1b6132"></a>
### Description

It returns the date of the first day of the week that comes after the given date (argument).

The second argument, day, can be a string or a number that represents a day.  
• String: SUNDAY ~ SATURDAY  or SUN ~ SAT  
• Number: 1 (sunday) ~ 7 (saturday)  

If any of the input argument is NULL, the result will also be NULL.

The return type is always DATE, regardless of the input type of the date.  
The hour, minute, and second of the result will be the same as those of the input argument date.

<a id="c400937fa9966946"></a>
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

<a id="bc1e3ceed22e9e15"></a>
## NEXTVAL

<a id="738865c3d8a78bb0"></a>
### Syntax

```
seq_name.NEXTVAL
NEXTVAL( seq_name )
NEXT VALUE FOR seq_name
```

<a id="1410b3f5db83b55d"></a>
### Description

It retrieves the next value from the sequence object.

<a id="fe96d20c088132b4"></a>
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

<a id="80b5c54f4311faa4"></a>
## NTH_VALUE() OVER

<a id="1db74c7c7c430be2"></a>
### Syntax

```
NTH_VALUE ( expr, n ) [ FROM { FIRST | LAST } ][ { RESPECT | IGNORE } NULLS ] OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="10cb6da59fc8c0f5"></a>
### Description

The window function NTH_VALUE returns the value of expr for the n-th row.  
If the number of rows in the window is less than n, it returns NULL.

The n argument can be a numeric type or a type that can be converted to a number.

FROM FIRST refers to the n-th row starting from the first row.  
FROM LAST refers to the n-th row starting from the last row.  
If not specified, the default value is FROM FIRST.

RESPECT NULLS returns the value of the n-th row, including NULL.   
IGNORE NULLS returns the value of the n-th row, excluding NULL.   
If not specified, the default value is RESPECT NULLS.

<a id="f0ecc7640645abce"></a>
### Example

```
gSQL> SELECT product_id, min_price,
             NTH_VALUE( min_price, 2 ) OVER ( ORDER BY product_id ) AS nth_value
      FROM product_information
      WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE NTH_VALUE
---------- --------- ---------
      1769      null      null
      1770        73        73
      2378       247        73
      2382       731        73
      3355      null        73

5 rows selected.
```

The following is an example when FROM LAST is specified.

```
gSQL> SELECT product_id, min_price,
             NTH_VALUE( min_price, 2 ) FROM LAST OVER ( ORDER BY product_id ) AS nth_value
      FROM product_information
      WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE NTH_VALUE
---------- --------- ---------
      1769      null      null
      1770        73      null
      2378       247        73
      2382       731       247
      3355      null       731

5 rows selected.
```

The following is an example when IGNORE NULLS is specified.

```
gSQL> SELECT product_id, min_price,
             NTH_VALUE( min_price, 2 ) IGNORE NULLS OVER ( ORDER BY product_id ) AS nth_value
      FROM product_information
      WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE NTH_VALUE
---------- --------- ---------
      1769      null      null
      1770        73      null
      2378       247       247
      2382       731       247
      3355      null       247

5 rows selected.
```

<a id="8cff1c7fb3275c6f"></a>
## NTILE() OVER

<a id="64f36c5915fe8f90"></a>
### Syntax

```
NTILE( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="f7ba55a16353a8e0"></a>
### Description

The window function NTILE returns the bucket number for each row.

The bucket numbers are consecutive integers starting from 1, and the number of buckets is the same as the number of expr.  
If the number of buckets exceeds the number of rows, each row is assigned a bucket, and the remaining buckets will be empty.

expr must be a positive constant. If expr is not a fixed number, it must be the target of the *window partition by*.

A window frame can not be used.

<a id="cba58b38026a24b8"></a>
### Example

```
gSQL> SELECT department_id, salary,
             NTILE(3) OVER ( ORDER BY salary ) AS ntile
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY NTILE
------------- ------ -----
           60   4200     1
           60   4800     1
           60   4800     2
           60   6000     2
           60   9000     3

5 rows selected.
```

The following is an example where the number of buckets (the number of expr) is greater than the number of rows.

```
gSQL> SELECT department_id, salary,
             NTILE(6) OVER ( ORDER BY salary ) AS ntile
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY NTILE
------------- ------ -----
           60   4200     1
           60   4800     2
           60   4800     3
           60   6000     4
           60   9000     5

5 rows selected.
```

<a id="aef2dc5f3ce03844"></a>
## NULLIF

<a id="b6d2b2310588de35"></a>
### Syntax

```
NULLIF( expr1, expr2 )
```

<a id="8ff01814c307616e"></a>
### Description

If expr1 is equal to expr2, it returns NULL. If they are not equal, it returns expr1, the first argument.

If the data types of expr1 and expr2 are different, the result type is determined by the [Result Type Combination Rule](11-sql-elements.md#4c0e2485bf66d2d0).

NULLIF can be expressed using CASE as follows.

- NULLIF( expr1, expr2 )

```
CASE WHEN expr1 = expr2 THEN NULL 
       ELSE expr1 
  END
```

<a id="c5885a510168cd75"></a>
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

<a id="36e622b41cbe994b"></a>
## NUMTODSINTERVAL

<a id="8b158cde38e18517"></a>
### Syntax

```
NUMTODSINTERVAL( num, interval_indicator )
```

<a id="e2d1e878f0240f79"></a>
### Description

It converts the number in the interval_indicator unit to an interval day to second type and returns it.

The argument *number* is of a numeric type.

The argument interval_indicator is a character type, like CHAR or VARCHAR, and it must be one of 'DAY', 'HOUR', 'MINUTE', or 'SECOND', case-insensitive.

If any argument is NULL, the result will also be NULL.

The result is returned as an interval day(6) to second(6) type, and the user cannot arbitrarily modify the precision. If the leading precision of the converted result exceeds the default precision, an error is returned. If the fraction precision exceeds the default, the rounded value is returned.

<a id="e59b2c19b8125eb4"></a>
### Example

- It converts *1 Day* to an interval day to second type.

```
gSQL> SELECT NUMTODSINTERVAL(1, 'DAY') FROM DUAL;

NUMTODSINTERVAL(1, 'DAY')
-------------------------
+000001 00:00:00.000000  

1 row selected.
```

- It converts *36 Hour* to an interval day to second type.

```
gSQL> SELECT NUMTODSINTERVAL(36, 'HOUR') FROM DUAL;

NUMTODSINTERVAL(36, 'HOUR')
---------------------------
+000001 12:00:00.000000    

1 row selected.
```

- It converts *1530 Minute* to an interval day to second type.

```
gSQL> SELECT NUMTODSINTERVAL(1530, 'MINUTE') FROM DUAL;

NUMTODSINTERVAL(1530, 'MINUTE')
-------------------------------
+000001 01:30:00.000000        

1 row selected.
```

- It converts *90100.1234567 Second* to an interval day to second type.

```
gSQL> SELECT NUMTODSINTERVAL(90100.1234567, 'SECOND') FROM DUAL;

NUMTODSINTERVAL(90100.1234567, 'SECOND')
----------------------------------------
+000001 01:01:40.123457                 

1 row selected.
```

<a id="76ea4a5700a8dd3d"></a>
## NUMTOYMINTERVAL

<a id="926d383dc5644819"></a>
### Syntax

```
NUMTOYMINTERVAL( num, interval_indicator )
```

<a id="57acc378b08ba21c"></a>
### Description

It converts the number in the interval_indicator unit to an interval year to month type and returns it.

The argument *number* is of a numeric type.

The argument interval_indicator is a character type, like CHAR or VARCHAR, and it must be one of 'YEAR', or 'MONTH', case-insensitive.

If any argument is NULL, the result will also be NULL.

The result is returned as an interval year(6) to month type, and the user cannot arbitrarily modify the precision. If the leading precision of the converted result exceeds the default precision, an error is returned.

<a id="c188f91fda134c1c"></a>
### Example

- It converts *1 Year* to an interval year to month type.

```
gSQL> SELECT NUMTOYMINTERVAL(1, 'YEAR') FROM DUAL;

NUMTOYMINTERVAL(1, 'YEAR')
--------------------------
+000001-00                

1 row selected.
```

- It converts *13.5 Month* to an interval year to month type.

```
gSQL> SELECT NUMTOYMINTERVAL(13.5, 'MONTH') FROM DUAL;

NUMTOYMINTERVAL(13.5, 'MONTH')
------------------------------
+000001-02                    

1 row selected.
```

<a id="70e7a47e2c3d528c"></a>
## NVL

<a id="17cc7e133bbc3adf"></a>
### Syntax

```
NVL( expr1, expr2 )
```

<a id="206f7acd0e10e0c9"></a>
### Description

If expr1 is not NULL, it returns expr1. If expr1 is NULL, it returns expr2.

The result type is determined by the data type of expr1.  
If NULL is specified in expr1, the result type is determined by the data type of expr2.   
If the data type of expr1 is numeric or character type, the result type is determined to include the ranges of expr1 and expr2 respectively.  
If both expr1 and expr2 are of the CHAR type, the result type is determined to be VARCHAR.

<a id="1b99383acfa0a4af"></a>
### Example

```
gSQL> SELECT I1, NVL( I1, 0 ) FROM T1;
  I1 NVL( I1, 0 )
---- ------------
   1            1
null            0
2 rows selected.
```

<a id="4e5a4c6988683394"></a>
## NVL2

<a id="d9242b774f491111"></a>
### Syntax

```
NVL2( expr1, expr2, expr3 )
```

<a id="180bf5bf394d8cc0"></a>
### Description

If expr1 is not null, it returns expr2. If expr1 is NULL, it returns expr3.

The result type is determined by the data type of expr2.   
If NULL is specified in expr2, the result type is determined by the data type of expr3.  
If the data type of expr2 is numeric or character type, the result type is determined to include the ranges of expr2 and expr3 respectively.  
If both expr2 and expr3 are of the CHAR type, the result type is determined to be VARCHAR.

<a id="f1ba5d5ab46bcbec"></a>
### Example

```
gSQL> SELECT I1, NVL2( I1, I1 * 1000, 0 ) FROM T1;
  I1 NVL2( I1, I1 * 1000, 0 )
---- ------------------------
   1                     1000
null                        0
2 rows selected.
```

<a id="ddbc8d3776b14b1b"></a>
## OCTET_LENGTH

<a id="cf30ea04deb3e6af"></a>
### Syntax

```
OCTET_LENGTH( str )  

BYTE_LENGTH( str )     

LENGTHB( str )
```

<a id="0f3e86e650bec3d4"></a>
### Description

It returns the number of bytes in the str.

The str argument can be of a character type, such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type, such as BINARY, BINARY VARYING, BINARY LONGVARYING.

If the str data type is CHARACTER, white spaces are included in the calculation.  
If str is NULL, the result will also be NULL.

It is an alias of [BYTE_LENGTH](#a55aa7d89b47253c) and [LENGTHB](#c5f46ba504cefe4a).

<a id="a4b045e1c1b5ecc9"></a>
### Example

- Multi-byte character set (e.g. UTF8): 1 byte character

```
gSQL> SELECT OCTET_LENGTH( 'OCTET_LENGTH' ) AS RESULT_1BYTE_CHARACTERS 
        FROM DUAL;
RESULT_1BYTE_CHARACTERS
-----------------------
                     12
1 row selected.
```

- Multi-byte character set (e.g. UTF8): 2 byte character

```
gSQL> SELECT OCTET_LENGTH( 'αβ' ) AS RESULT_2BYTE_CHARACTERS FROM DUAL;
RESULT_2BYTE_CHARACTERS
-----------------------
                      4
1 row selected.
```

<a id="19716074501dd867"></a>
## OVERLAY

<a id="9f00c7d7f61f2167"></a>
### Syntax

```
OVERLAY( str1 PLACING str2 FROM start_position  [ FOR string_length ] )
```

<a id="a5e909eaa31568a8"></a>
### Description

It overlays the characters in the range between str1's start_position and string_length with str2.

The data types of str1 and str2 arguments can be character types, such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or binary character types, such as BINARY, BINARY VARYING, BINARY LONG VARYING  

The start_position and string_length arguments can be of a numeric data type.

- The result of the OVERLAY function is as follows.
    - When FOR is specified.  
      SUBSTRING( str1 FROM 1 FOR (start_position - 1) )  
      || str2  
      || SUBSTRING( str1 FROM (start_position + string_length )
    - When FOR is omitted.  
      SUBSTRING( str1 FROM 1 FOR (start_position - 1) )  
      || str2  
      || SUBSTRING( str1 FROM (start_position + CHAR_LENGTH(str2))

For more information, refer to [SUBSTRING](#c9a451794ac8d7d6).

The following table describes the result types.

**Result type of OVERLAY**

<a id="28c4537143ca374d"></a>
| str1, str2 types | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="618c9c9d27bdea6b"></a>
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

<a id="d06751ea6d93e3bb"></a>
## PERCENT_RANK() OVER

<a id="842fab981f3ce008"></a>
### Syntax

```
PERCENT_RANK( ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="b4eb57393824110a"></a>
### Description

The window function PERCENT_RANK calculates the ranking ratio of each row relative to the total number of rows.

The result of the PERCENT_RANK function is a number between 0 and 1, and if the row values are the same, the ratio value is also the same.

A window frame can not be used.

<a id="b5336aaeeae860ab"></a>
### Example

```
gSQL> SELECT department_id, salary,
             PERCENT_RANK() OVER ( ORDER BY salary ) AS p_rank
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY P_RANK
------------- ------ ------
           60   4200      0
           60   4800    .25
           60   4800    .25
           60   6000    .75
           60   9000      1

5 rows selected.
```

<a id="4f7de04feb86ca45"></a>
## PERCENTILE_CONT() OVER

<a id="960ba82a27a910ee"></a>
### Syntax

```
PERCENTILE_CONT( expr ) WITHIN GROUP ( ORDER BY <sort specification> ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="8ee3daea9c641744"></a>
### Description

The window function PERCENTILE_CONT is an inverse distribution function that assumes a continuous distribution model.

It calculates the value corresponding to the specified percentile score for *not null values* sorted within the group.   
The result of the calculation may differ from the specific value sorted within the group.

expr must be the percentile score, which is a value between 0 and 1.

Only the PARTITION BY clause is available in the OVER() clause.   
It divides the query result set into groups using the PARTITION BY clause.

It sorts the records within the group using WITHIN GROUP ( ORDER BY &lt;sort specification&gt; ).   
Only one &lt;sort specification&gt; can be specified in the ORDER BY clause.

NULL values are excluded from the sorted values.

The following is the calculation formula.

```
P : Percentile score 
N : The number of the records of not null values sorted within the group
RN = ( 1 + ( P * (N-1) ) )
CRN = CEILING( RN )
FRM = FLOOR( RN )

* if ( CRN = FRN = RN )
     sort expression value of RN
* else
     sort expression value of ( CRN - RN ) * FRN + sort expression value of ( RN - FRN ) * CRN
```

The window function MEDIAN is a specific case of the PERCENTILE_CONT window function, with a default percentile score of 0.5.

For more information, refer to the following.

- [MEDIAN() OVER](#af88b35602436133)
- [PERCENTILE_DISC() OVER](#d600d89cafc9b5d2)

<a id="b15fe4de9c2c7109"></a>
### Example

```
gSQL> 
SELECT item_no, 
       sales,
       PERCENTILE_CONT( 0.5 ) WITHIN GROUP ( ORDER BY sales ) 
                              OVER ( PARTITION BY item_no ) 
       AS PERCENTILE_CONT
  FROM store;

ITEM_NO SALES PERCENTILE_CONT
------- ----- ---------------
    100    50             125
    100    90             125
    100    90             125
    100   100             125
    100   120             125
    100   130             125
    100   150             125
    100   150             125
    100   170             125
    100   200             125
    235    50              90
    235    70              90
    235    90              90
    235   130              90
    235   190              90

15 rows selected.
```

<a id="d600d89cafc9b5d2"></a>
## PERCENTILE_DISC() OVER

<a id="ebf887968b631c16"></a>
### Syntax

```
PERCENTILE_DISC( expr ) WITHIN GROUP ( ORDER BY <sort specification> ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="106c4e3dc2f8c076"></a>
### Description

The window function PERCENTILE_DISC is an inverse distribution function that assumes a discrete distribution model.

It calculates the percentile score for *not null values* sorted within the group.   
It determines the smallest value among those greater than or equal to the specified percentile.  
The function then returns the value corresponding to the determined percentile.

expr must be the percentile score, which is a value between 0 and 1.

Only the PARTITION BY clause is available in the OVER() clause.   
It divides the query result set into groups using the PARTITION BY clause.

It sorts the records within the group using WITHIN GROUP ( ORDER BY &lt;sort specification&gt; ).   
Only one &lt;sort specification&gt; can be specified in the ORDER BY clause.

It calculates the CUME_DIST for the sort expression value based on the sorted records.  
When calculating CUME_DIST, NULL values are excluded.

It determines the smallest CUME_DIST value that is greater than or equal to the percentile specified by the expr.  
It then returns the determined CUME_DIST value.

The result type is the same as the type of the sort expression value.

For more information, refer to [CUME_DIST() OVER](#1084d34375187411).

<a id="a9e6632ae7873801"></a>
### Example

```
gSQL> 
SELECT item_no, 
       sales,
       CUME_DIST() OVER ( PARTITION BY item_no ORDER BY sales ) 
       AS CUME_DIST,
       PERCENTILE_DISC( 0.5 ) WITHIN GROUP ( ORDER BY sales ) 
                              OVER ( PARTITION BY item_no ) 
       AS PERCENTILE_DISC
  FROM store;

ITEM_NO SALES CUME_DIST PERCENTILE_DISC
------- ----- --------- ---------------
    100    50        .1             120
    100    90        .3             120
    100    90        .3             120
    100   100        .4             120
    100   120        .5             120
    100   130        .6             120
    100   150        .8             120
    100   150        .8             120
    100   170        .9             120
    100   200         1             120
    235    50        .2              90
    235    70        .4              90
    235    90        .6              90
    235   130        .8              90
    235   190         1              90

15 rows selected.
```

<a id="ac47b95fbee9bcfb"></a>
## PHYSICAL_LENGTH

<a id="48530af07f0351d6"></a>
### Syntax

```
PHYSICAL_LENGTH( expr )
```

<a id="46dc941a0bcacd2c"></a>
### Description

The PHYSICAL_LENGTH function returns the number of bytes of internal expression representation for the given expr.

The expr argument can be of any data type.

If an input argument is NULL, the result will be 0.

<a id="e6163e6f4ede8632"></a>
### Example

- When an input argument is NULL

```
gSQL> SELECT PHYSICAL_LENGTH( NULL ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

- The following is an example that shows the NUMBER type byte count for 1, 123, and 12345.

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

<a id="f38bfce7d7746322"></a>
## PI

<a id="b3945bfe2755094a"></a>
### Syntax

```
PI()
```

<a id="fa5371811de02561"></a>
### Description

It returns the constant "π".

<a id="9fae3ca1e500527e"></a>
### Example

```
gSQL> SELECT PI() AS RESULT FROM DUAL;
              RESULT
--------------------
3.141592653589793E+0
1 row selected.
```

<a id="b97361a0b31fc8b6"></a>
## POSITION

<a id="3e020170d4a9ea61"></a>
### Syntax

```
POSITION( str1 IN str2 )
```

<a id="59986d80b6374be7"></a>
### Description

It searches for the first occurrence of str1 within str2 and returns its position.

The data type of the str1 and str2 arguments can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, or BINARY LONG VARYING.

If str1 cannot be found within str2, the return value is 0.  
If str1 is found within str2, the position of str1 is returned, starting from 1.  
The returned position value is calculated in character units (not in byte units).  
If either str1 or str2 is NULL, the return value is also NULL.

<a id="8e60c86fa2d85980"></a>
### Example

```
gSQL> SELECT POSITION( 'CHAR' IN 'LONG CHAR 2000' ) AS RESULT FROM DUAL;
RESULT
------
     6
1 row selected.
```

<a id="923289d2965eeaa2"></a>
## POWER

<a id="1bb71497037972fb"></a>
### Syntax

```
POWER( num1, num2 )
```

<a id="2157e116a003cc89"></a>
### Description

It returns the value of num1 raised to the power of num2.

The num1 and num2 arguments can be of a numeric data type.  

If num1 is a negative number, num2 must be an integer.  
If either num1 or num2 is NULL, the result will also be NULL.

<a id="7595f5c217ed1be2"></a>
### Example

```
gSQL> SELECT POWER( 2, 3 ) AS RESULT FROM DUAL;
RESULT
------
     8
1 row selected.
```

<a id="8712212aed5abfe3"></a>
## RADIANS

<a id="47670ff577986dc7"></a>
### Syntax

```
RADIANS( degrees )
```

<a id="6a63b2cce7501c6d"></a>
### Description

It returns the radians of the given degrees.  

The degrees argument can be a numeric data type.  
If the degrees argument is NULL, the result will also be NULL.

<a id="a0bf726a061eb3b5"></a>
### Example

```
gSQL> SELECT RADIANS( 180 ) AS RESULT FROM DUAL;
          RESULT
----------------
3.14159265358979
1 row selected.
```

<a id="8603ff42fa54e75a"></a>
## RANDOM

<a id="dd61c30dd170a2e5"></a>
### Syntax

```
RANDOM( min, max )
```

<a id="1dafa0270304100d"></a>
### Description

It returns a random value greater than or equal to min and less than or equal to max.  

The min and max arguments can be of a numeric data type.  
If either the min or max argument is NULL, the result will also be NULL.

<a id="fa1cd95c639a090d"></a>
### Example

```
gSQL> SELECT RANDOM( 1, 100 ) AS RESULT FROM DUAL;
          RESULT
----------------
34.1870528003201
1 row selected.
```

<a id="bbb8aa77da81f0c5"></a>
## RANK() OVER

<a id="20d898735c16b5bf"></a>
### Syntax

```
RANK( ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="b283e561d84bf9e9"></a>
### Description

The window function RANK calculates the ranking.

The ranking is an integer starting from 1, and rows with the same value have the same rank.

A window frame can not be used.

<a id="44bd2828754816d8"></a>
### Example

```
gSQL> SELECT department_id, salary,
             RANK() OVER ( ORDER BY salary ) AS rank
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY RANK
------------- ------ ----
           60   4200    1
           60   4800    2
           60   4800    2
           60   6000    4
           60   9000    5

5 rows selected.
```

<a id="1e112e5c333c9548"></a>
## RATIO_TO_REPORT() OVER

<a id="6533b968ef0a44c2"></a>
### Syntax

```
RATIO_TO_REPORT ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="508d5917e6b6f18b"></a>
### Description

The window function RATIO_TO_REPORT calculates the ratio of each row value relative to the total sum of the expr values.  
If the row value is NULL, the result will also be NULL.

*order by* cannot be used in the window clause.  
A window frame cannot be used.

<a id="4608ea72b84dc46b"></a>
### Example

```
gSQL> SELECT supplier_id, min_price
             , RATIO_TO_REPORT( min_price ) OVER ( PARTITION BY supplier_id ) AS "RATIO"
        FROM product_information
       WHERE supplier_id = 102050;

SUPPLIER_ID MIN_PRICE             RATIO
----------- --------- -----------------
     102050       731  .695528068506185
     102050      null              null
     102050        73 .0694576593720266
     102050       247  .235014272121789
     102050      null              null

5 rows selected.
```

<a id="54924611a881f204"></a>
## REGEXP_COUNT

<a id="71ea57014442d599"></a>
### Syntax

```
REGEXP_COUNT ( source_string, pattern [, position [, match_param ] ] )
```

<a id="ea4bf9ce86724e0c"></a>
### Description

It returns the number of times the pattern is matched in the source_string.  
If no match is found, it returns 0.

*source_string*  
It is the character expression of the search target, and it can be of a character type or a type that can be converted to a character, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

*pattern*  
It is the regular expression, and it can be of a character type or a type that can be converted to a character, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.   
It can be described up to 512 bytes.  
For more information about the operators that can be specified in the pattern, refer to the [Regular Expression Operators](11-sql-elements.md#7abbfdba9d28e093).

*position*  
It is the positive integer that indicates the starting character position for searching in the source_string.  
The default value is 1, meaning the search starts from the first character of the source_string.

*match_param*  
It is the character expression that can alter the default matching operation of a function, and it can be of a character type such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

'i', 'c', 'n', 'm', 'x' can be specified in match_param, and one or more can be used.

- **'i':** It is case-insensitive.
- **'c':** It is case-sensitive.
- **'n':** The dot operator ( . ) allows matching with the newline character.
- **'m':** It treats the source_string as multiple lines. It interprets ^ ( Beginning-of-Line Anchor ) and $ ( End-of-Line Anchor ) for each line.
- **'x':** It ignores whitespaces within the pattern.

If a character other than 'i', 'c', 'n', 'm', or 'x' appears in match_param, an error is returned.   
If contradictory uppercase and lowercase matching options, such as 'ic', are listed in match_param, an error is returned.

If match_param is omitted:  
&nbsp;• It is case sensitive.   
&nbsp;• The dot operator ( . ) does not allow matching with the newline character.   
&nbsp;• It treats the source_string as a single line.

<a id="7b170a9b0d1c26da"></a>
### Example

```
gSQL> 
SELECT reason_desc, REGEXP_COUNT( reason_desc, '\w+' ) AS word_cnt 
  FROM reason;
REASON_DESC                     WORD_CNT
------------------------------- --------
Wrong size                             2
Did not like the color                 5
No service location in my area         6
Found a better price in a store        7
4 rows selected.

### position
gSQL> 
SELECT start_date,
       REGEXP_COUNT( start_date, '-\d{2}', 3 ) AS RESULT
  FROM call_center;
START_DATE  RESULT
----------- ------
1998-01-01       2
1999-JAN-03      1
2000-02-21       2
2001-03-31       2
29-NOV-23        1
5 rows selected.
```

<a id="75e1a53f48309d9a"></a>
## REGEXP_INSTR

<a id="680d374f7c7626b1"></a>
### Syntax

```
REGEXP_INSTR ( source_string, pattern [, position [, occurrence [, return_opt [, match_param [, subexpr ] ] ] ] ] )
```

<a id="e12c7b8085c2c52b"></a>
### Description

It returns the starting position of the string where the pattern is matched, or the position of the next character after the matched string in source_string as a number.  
If the matched string does not exist, it returns 0.

*source_string*  
It is the character expression of the search target, and it can be a character type or a type that can be converted to a character, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

*pattern*  
It is the regular expression, and it can be of a character type or a type that can be converted to a character, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.  
It can be described up to 512 bytes.  
For more information about the operators that can be specified in the pattern, refer to the [Regular Expression Operators](11-sql-elements.md#7abbfdba9d28e093).

*position*  
It is the positive integer that indicates the starting character position for searching in the source_string.  
The default value is 1, meaning the search starts from the first character of the source_string.

*occurrence*  
It is the positive integer that indicates the ordinal number of the matched pattern to search for in source_string.  
The default value is 1, meaning it searches for the first matching in source_string.

*return_opt*  
It indicates which result to return for the string where the pattern is matched in the source_string.

- If return_opt is 0, 
    - It is the default value, and it returns the position of the first character of the matched string.
- If return_opt is 1,
    - It returns the position of the character following the matched string.

*match_param*  
It is the character expression that can alter the default matching operation of a function, and it can be of a character type such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

'i', 'c', 'n', 'm', 'x' can be specified in match_param, and one or more can be used.

- **'i':** It is case-insensitive.
- **'c':** It is case-sensitive.
- **'n':** The dot operator ( . ) allows matching with the newline character.
- **'m':** It treats the source_string as multiple lines. It interprets ^ ( Beginning-of-Line Anchor ) and $ ( End-of-Line Anchor ) for each line.
- **'x':** It ignores whitespaces within the pattern.

If a character other than 'i', 'c', 'n', 'm', or 'x' appears in match_param, an error is returned.   
If contradictory uppercase and lowercase matching options, such as 'ic', are listed in match_param, an error is returned.

If match_param is omitted:  
&nbsp;• It is case sensitive.  
&nbsp;• The dot operator ( . ) does not allow matching with the newline character.  
&nbsp;• It treats the source_string as a single line.

subexpr  
It is a positive number from 0 to 9 that indicates the subexpression described in the pattern.  
For more information about subexpr, refer to the [Regular Expression Operators](11-sql-elements.md#7abbfdba9d28e093).

<a id="391df125cb7e2f6b"></a>
### Example

```
gSQL> 
SELECT reason_desc, 
       REGEXP_INSTR( reason_desc, '[[:space:]]' ) AS RESULT
  FROM reason;
REASON_DESC                     RESULT
------------------------------- ------
Wrong size                           6
Did not like the color               4
No service location in my area       3
Found a better price in a store      6
4 rows selected.

### position, occurrence
gSQL> 
SELECT reason_desc, REGEXP_INSTR( reason_desc, '\w+', 1, 2 ) AS RESULT
  FROM reason;
REASON_DESC                     RESULT
------------------------------- ------
Wrong size                           7
Did not like the color               5
No service location in my area       4
Found a better price in a store      7
4 rows selected.

### return_opt
gSQL> 
SELECT reason_desc, 
       REGEXP_INSTR( reason_desc, '\w+', 1, 2, 0 ) AS RESULT_RETURN_OPT_0,
       REGEXP_INSTR( reason_desc, '\w+', 1, 2, 1 ) AS RESULT_RETURN_OPT_1
  FROM reason;
REASON_DESC                     RESULT_RETURN_OPT_0 RESULT_RETURN_OPT_1
------------------------------- ------------------- -------------------
Wrong size                                        7                  11
Did not like the color                            5                   8
No service location in my area                    4                  11
Found a better price in a store                   7                   8
4 rows selected.

### subexpr
gSQL> 
SELECT REGEXP_INSTR( '123456789', '(12)(3456(789))', 1, 1, 0, 'i', 3 ) 
       AS RESULT
  FROM dual;
RESULT
------
     7
1 row selected.
```

<a id="42d99f66190078af"></a>
## REGEXP_REPLACE

<a id="9683f87d9175104e"></a>
### Syntax

```
REGEXP_REPLACE ( source_string, pattern [, replace_string [, position [, occurrence [, match_param ] ] ] ]  )
```

<a id="2e406ee044b765d8"></a>
### Description

It returns a string in which the matched pattern in the source_string is replaced with the replace_string.

*source_string*  
It is the character expression of the search target, and it can be of a character type or a type that can be converted to a character, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

*pattern*  
It is the regular expression, and it can be of a character type or a type that can be converted to a character, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.  
It can be described up to 512 bytes.  
For more information about the operators that can be specified in the pattern, refer to the [Regular Expression Operators](11-sql-elements.md#7abbfdba9d28e093).

*replace_string*  
It is the character expression that replaces the string matching the pattern in source_string, and it can be of a character type or a type that can be converted to a character, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.  
replace_string may include backrefercence in the form of \n, where n is an integer from 1 to 9.  
To include a backslash (\) as a character in replace_string, describe it together with the escape character backslash (\\).

*position*  
It is the positive integer that indicates the starting character position for searching in the source_string.  
The default value is 1, meaning the search starts from the first character of the source_string.

*occurrence*  
It is the positive integer that indicates the ordinal number of the matched pattern to search for in source_string.  
If it is 0, it replaces all strings that match the pattern with replace_string.  
If it is a positive integer n, it replaces the n-th string that matches the pattern with replace_string.  
If it is omitted, the default value is 0.

*match_param*  
It is the character expression that can alter the default matching operation of a function, and it can be of a character type such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

'i', 'c', 'n', 'm', 'x' can be specified in match_param, and one or more can be used.

- **'i':** It is case-insensitive.
- **'c':** It is case-sensitive.
- **'n':** The dot operator ( . ) allows matching with the newline character.
- **'m':** It treats the source_string as multiple lines. It interprets ^ ( Beginning-of-Line Anchor ) and $ ( End-of-Line Anchor ) for each line.
- **'x':** It ignores whitespaces within the pattern.

If a character other than 'i', 'c', 'n', 'm', 'x' appears in match_param, an error is returned.   
If contradictory uppercase and lowercase matching options, such as 'ic', are listed in match_param, an error is returned.

If match_param is omitted,   
• It is case sensitive.   
• The dot operator ( . ) does not allow matching with the newline character.   
• It treats the source_string as a single line.

<a id="b69aefcdde952749"></a>
### Example

```
gSQL> 
SELECT reason_desc, 
       REGEXP_REPLACE( reason_desc, '\s', '[ ]' ) AS RESULT
  FROM reason;
REASON_DESC                     RESULT                                     
------------------------------- -------------------------------------------
Wrong size                      Wrong[ ]size                               
Did not like the color          Did[ ]not[ ]like[ ]the[ ]color             
No service location in my area  No[ ]service[ ]location[ ]in[ ]my[ ]area   
Found a better price in a store Found[ ]a[ ]better[ ]price[ ]in[ ]a[ ]store
4 rows selected.


### It includes the backreference in the replace string.
gSQL> 
SELECT start_date,
       REGEXP_REPLACE( start_date, 
                       '([[:digit:]]{4})-([[:digit:]]{2})-([[:digit:]]{2})',
                       '\3/\2/\1' ) AS RESULT
  FROM call_center;
START_DATE RESULT    
---------- ----------
1998-01-01 01/01/1998
2000-02-21 21/02/2000
2001-03-31 31/03/2001
3 rows selected.
```

<a id="be5a2413d7c8ae27"></a>
## REGEXP_SUBSTR

<a id="76408a8b0e99a12d"></a>
### Syntax

```
REGEXP_SUBSTR ( source_string, pattern [, position [, occurrence [, match_param [, subexpr ] ] ] ] )
```

<a id="d01d6d783e875e4e"></a>
### Description

It returns the string that matches the pattern in source_string.

*source_string*  
It is the character expression of the search target, and it can be of a character type or a type that can be converted to a character, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

*pattern*  
It is the regular expression, and it can be of a character type or a type that can be converted to a character, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.  
It can be described up to 512 bytes.  
For more information about the operators that can be specified in the pattern, refer to the [Regular Expression Operators](11-sql-elements.md#7abbfdba9d28e093).

*position*  
It is the positive integer that indicates the starting character position for searching in the source_string.  
The default value is 1, meaning the search starts from the first character of the source_string.

*occurrence*  
It is the positive integer that indicates the ordinal number of the matched pattern to search for in source_string.  
The default value is 1, meaning it searches for the first matching in source_string.

*match_param*  
It is the character expression that can alter the default matching operation of a function, and it can be of a character type such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

'i', 'c', 'n', 'm', 'x' can be specified in match_param, and one or more can be used.

- **'i':** It is case-insensitive.
- **'c':** It is case-sensitive.
- **'n':** The dot operator ( . ) allows matching with the newline character.
- **'m':** It treats the source_string as multiple lines. It interprets ^ ( Beginning-of-Line Anchor ) and $ ( End-of-Line Anchor ) for each line.
- **'x':** It ignores whitespaces within the pattern.

If a character other than 'i', 'c', 'n', 'm', or 'x' appears in match_param, an error is returned.   
If contradictory uppercase and lowercase matching options, such as 'ic', are listed in match_param, an error is returned.

If match_param is omitted:  
&nbsp;• It is case sensitive.  
&nbsp;• The dot operator ( . ) does not allow matching with the newline character.  
&nbsp;• It treats the source_string as a single line.

*subexpr*  
It is a positive number from 0 to 9 that indicates the subexpression described in the pattern.   
A subexpression is a part of the pattern enclosed in parentheses ( ) .  
For more information about subexpr, refer to the [Regular Expression Operators](11-sql-elements.md#7abbfdba9d28e093).

<a id="a004196c3659fe9b"></a>
### Example

```
gSQL> 
SELECT reason_desc,
       REGEXP_SUBSTR( reason_desc, '[[:alpha:]]+' ) AS RESULT
  FROM reason;
REASON_DESC                     RESULT
------------------------------- ------
Wrong size                      Wrong 
Did not like the color          Did   
No service location in my area  No    
Found a better price in a store Found 
4 rows selected.


### position, occurrence
gSQL> 
SELECT start_date,
       REGEXP_SUBSTR( start_date, '[[:punct:]]\d+', 5, 2 ) AS RESULT
  FROM call_center;
START_DATE RESULT
---------- ------
1998-01-01 -01   
2000-02-21 -21   
2001-03-31 -31   
3 rows selected.

### subexpr
gSQL> 
SELECT start_date,
       REGEXP_SUBSTR( start_date, 
                      '([[:digit:]]{4})-([[:digit:]]{2})-([[:digit:]]{2})',
                      1,
                      1,
                      'i',
                      2 ) AS RESULT
  FROM call_center;
START_DATE RESULT
---------- ------
1998-01-01 01    
2000-02-21 02    
2001-03-31 03    
3 rows selected.
```

<a id="c669a282cdf0f8d1"></a>
## REGR_AVGX() OVER

<a id="de46c23f5353e726"></a>
### Syntax

```
REGR_AVGX( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="5751239b1344a2d0"></a>
### Description

The window function REGR_AVGX is a linear regression function.  
It calculates the average value of the independent variable expr2 from the least-squares-fit linear equation of the (X, Y) data set.

The arguments of expr1 and expr2 are of numeric types.

expr1 is the dependent variable ( y ), and expr2 is the independent variable ( x ).

If expr1 is NULL or expr2 is NULL, it will be excluded from the target.

The following is the calculation formula.

```
AVG( expr2 )
```

The returned type is a numeric type.

The returned value is the result of the calculation or NULL.  
If all records are excluded from the target because expr1 or expr2 is NULL, then it returns NULL.

<a id="6541a427fedb8e57"></a>
### Example

```
gSQL> 
SELECT item_no,
       price,
       year,
       REGR_AVGX( price, year ) OVER ( PARTITION BY item_no )
       AS "REGR_AVGX(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_AVGX(price,year)
------- ----- ---- ---------------------
   3758 15000 2000                  2003
   3758 14700 2001                  2003
   3758 15300 2002                  2003
   3758 15200 2003                  2003
   3758 15100 2004                  2003
   3758 15300 2005                  2003
   3758 15350 2006                  2003

7 rows selected.
```

<a id="f5400e9901665ea5"></a>
## REGR_AVGY() OVER

<a id="b41337f18f4b857e"></a>
### Syntax

```
REGR_AVGY( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="53de228baf9e4432"></a>
### Description

The window function REGR_AVGY is a linear regression function.   
It calculates the average value of the dependent variable expr1 from the least-squares-fit linear equation of the (X, Y) data set.

The arguments of expr1 and expr2 are of numeric types.

expr1 is the dependent variable ( y ), and expr2 is the independent variable ( x ).

If expr1 is NULL or expr2 is NULL, it will be excluded from the target.

The following is the calculation formula.

```
AVG( expr1 )
```

The returned type is a numeric type.

The returned value is the result of the calculation or NULL.   
If all records are excluded from the target because expr1 or expr2 is NULL, then it returns NULL.

<a id="b1ff0a7a89a0afe2"></a>
### Example

```
gSQL> 
SELECT item_no,
       price,
       year,
       round( REGR_AVGY( price, year ) OVER ( PARTITION BY item_no ), 5 )
       AS "REGR_AVGY(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_AVGY(price,year)
------- ----- ---- ---------------------
   3758 15000 2000           15135.71429
   3758 14700 2001           15135.71429
   3758 15300 2002           15135.71429
   3758 15200 2003           15135.71429
   3758 15100 2004           15135.71429
   3758 15300 2005           15135.71429
   3758 15350 2006           15135.71429

7 rows selected.
```

<a id="fba4384faf0f46d0"></a>
## REGR_COUNT() OVER

<a id="98f88182afc59096"></a>
### Syntax

```
REGR_COUNT( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="2dd5c1faf42c1219"></a>
### Description

The window function REGR_COUNT is a linear regression function.   
It calculates the least-squares-fit linear equation of the (X, Y) data set.

It returns the number of ( X, Y ) pairs, the execution targets of the linear equation, both of which are not NULL.

The arguments of expr1 and expr2 are of numeric types.

expr1 is the dependent variable ( y ), and expr2 is the independent variable ( x ).

If expr1 is NULL or expr2 is NULL, it will be excluded from the target.

The returned type is a numeric type.

It returns the number of pairs where both expr1 and expr2 are not NULL.   
If all records are excluded from the target because expr1 or expr2 is NULL, then it returns 0.

<a id="785468321283ded8"></a>
### Example

```
gSQL> 
SELECT item_no,
       price,
       year,
       REGR_COUNT( price, year ) OVER ( PARTITION BY item_no )
       AS "REGR_COUNT(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_COUNT(price,year)
------- ----- ---- ----------------------
   3758 15000 2000                      7
   3758 14700 2001                      7
   3758 15300 2002                      7
   3758 15200 2003                      7
   3758 15100 2004                      7
   3758 15300 2005                      7
   3758 15350 2006                      7

7 rows selected.
```

<a id="84b5f2bd5dcecfdb"></a>
## REGR_INTERCEPT() OVER

<a id="9d61f1e69f8632c1"></a>
### Syntax

```
REGR_INTERCEPT( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="9fa8604501ddd86a"></a>
### Description

The window function REGR_INTERCEPT is a linear regression function.   
It calculates the y-intercept of the (X, Y) data set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are of numeric types.

expr1 is the dependent variable ( y ), and expr2 is the independent variable ( x ).

If expr1 is NULL or expr2 is NULL, it will be excluded from the target.

The following is the calculation formula.

```
AVG( expr1 ) - REGR_SLOPE( expr1, expr2 ) * AVG( expr2 )
```

The returned type is a numeric type.

The returned value is the result of the calculation or NULL.

It returns NULL in the following cases:  
• When all records are excluded from the target because expr1 or expr2 is NULL.  
• When the result of REGR_SLOPE is null.

<a id="bc6c309a29396897"></a>
### Example

```
gSQL> 
SELECT item_no,
       price,
       year,
       REGR_INTERCEPT( price, year ) OVER ( PARTITION BY item_no )
       AS "REGR_INTERCEPT(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_INTERCEPT(price,year)
------- ----- ---- --------------------------
   3758 15000 2000                  -131512.5
   3758 14700 2001                  -131512.5
   3758 15300 2002                  -131512.5
   3758 15200 2003                  -131512.5
   3758 15100 2004                  -131512.5
   3758 15300 2005                  -131512.5
   3758 15350 2006                  -131512.5

7 rows selected.
```

<a id="5d67d28ce3593acd"></a>
## REGR_R2() OVER

<a id="ee3ca8330178f888"></a>
### Syntax

```
REGR_R2( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="8cb83bce60fd7bfb"></a>
### Description

The window function REGR_R2 is a linear regression function.   
It calculates the coefficient of determination (R-squared or fitness) of the (X, Y) data set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are of numeric types.

expr1 is the dependent variable ( y ), and expr2 is the independent variable ( x ).

If expr1 is NULL or expr2 is NULL, it will be excluded from the target.

The following is the calculation formula.

```
If VAR_POP( expr2 ) = 0, then it is NULL. 
If VAR_POP( expr1 ) = 0 and VAR_POP( expr2 ) != 0, then it is 1.
If VAR_POP( expr1 ) > 0 and VAR_POP( expr2 ) != 0, then it is POWER( CORR( expr1, expr2), 2 ).
```

The returned type is a numeric type.

The returned value is the result of the calculation or NULL.

It returns NULL in the following cases:  
• When all records are excluded from the target because expr1 or expr2 is NULL  
• When the result of VAR_POP (expr2) is 0.

<a id="1a76dcc9acae676b"></a>
### Example

```
gSQL> 
SELECT item_no,
       price,
       year,
       round( REGR_R2( price, year ) OVER ( PARTITION BY item_no ), 10 )
       AS "REGR_R2(price,year)"
  FROM store
 WHERE item_no = 3758;

ITEM_NO PRICE YEAR REGR_R2(price,year)
------- ----- ---- -------------------
   3758 15000 2000         .4786446469
   3758 14700 2001         .4786446469
   3758 15300 2002         .4786446469
   3758 15200 2003         .4786446469
   3758 15100 2004         .4786446469
   3758 15300 2005         .4786446469
   3758 15350 2006         .4786446469

7 rows selected.
```

<a id="0ebaf0321b9d6651"></a>
## REGR_SLOPE() OVER

<a id="38f7ec58f1833ef1"></a>
### Syntax

```
REGR_SLOPE( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="f70224ac85203de2"></a>
### Description

The window function REGR_SLOPE is a linear regression function.   
It calculates the slope of the (X, Y) data set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are numeric types.

expr1 is the dependent variable ( y ), and expr2 is the independent variable ( x ).

If expr1 is NULL or expr2 is NULL, it will be excluded from the target.

The following is the calculation formula.

```
COVAR_POP(expr1, expr2) / VAR_POP(expr2)
```

The returned type is a numeric type.

The returned value is the result of the calculation or NULL.

It returns NULL in the following cases:  
• When all records are excluded from the target because expr1 or expr2 is NULL  
• When the result of VAR_POP is 0.

<a id="5f3e4480f254927b"></a>
### Example

```
gSQL> 
SELECT item_no,
       price,
       year,
       round( REGR_SLOPE( price, year ) OVER ( PARTITION BY item_no ), 10 )
       AS "REGR_SLOPE(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_SLOPE(price,year)
------- ----- ---- ----------------------
   3758 15000 2000          73.2142857143
   3758 14700 2001          73.2142857143
   3758 15300 2002          73.2142857143
   3758 15200 2003          73.2142857143
   3758 15100 2004          73.2142857143
   3758 15300 2005          73.2142857143
   3758 15350 2006          73.2142857143

7 rows selected.
```

<a id="ff52783c9d467670"></a>
## REGR_SXX() OVER

<a id="8b8549a6c8d8eccb"></a>
### Syntax

```
REGR_SXX( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="3be127a4da1c025c"></a>
### Description

The window function REGR_SXX is a linear regression function.   
It is an auxiliary function that calculates the diagnostic statistics of the (X, Y) data set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are of numeric types.

expr1 is the dependent variable ( y ), and expr2 is the independent variable ( x ).

If expr1 is NULL or expr2 is NULL, it will be excluded from the target.

The following is the calculation formula.

```
REGR_COUNT( expr1, expr2 ) * VAR_POP( expr2 )
```

The returned type is a numeric type.

The returned value is the result of the calculation or NULL.   
If all records are excluded from the target because expr1 or expr2 is NULL, then it returns NULL.

<a id="e9e20a052e2d0c0b"></a>
### Example

```
gSQL> 
SELECT item_no,
       price,
       year,
       REGR_SXX( price, year ) OVER ( PARTITION BY item_no )
       AS "REGR_SXX(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_SXX(price,year)
------- ----- ---- --------------------
   3758 15000 2000                   28
   3758 14700 2001                   28
   3758 15300 2002                   28
   3758 15200 2003                   28
   3758 15100 2004                   28
   3758 15300 2005                   28
   3758 15350 2006                   28

7 rows selected.
```

<a id="0556439554d27a68"></a>
## REGR_SXY() OVER

<a id="c6324dd9295f0989"></a>
### Syntax

```
REGR_SXY( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="ad3200fdaed2c0b3"></a>
### Description

The window function REGR_SXY is a linear regression function.   
It is an auxiliary function that calculates the diagnostic statistics of the (X, Y) data set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are of numeric types.

expr1 is the dependent variable ( y ), and expr2 is the independent variable ( x ).

If expr1 is NULL or expr2 is NULL, it will be excluded from the target.

The following is the calculation formula.

```
REGR_COUNT( expr1, expr2 ) * COVAR_POP( expr1, expr2 )
```

The returned type is a numeric type.

The returned value is the result of the calculation or NULL.   
If all records are excluded from the target because expr1 or expr2 is NULL, then it returns NULL.

<a id="c60e31021d1d3b52"></a>
### Example

```
gSQL> 
SELECT item_no,
       price,
       year,
       REGR_SXY( price, year ) OVER ( PARTITION BY item_no )
       AS "REGR_SXY(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_SXY(price,year)
------- ----- ---- --------------------
   3758 15000 2000                 2050
   3758 14700 2001                 2050
   3758 15300 2002                 2050
   3758 15200 2003                 2050
   3758 15100 2004                 2050
   3758 15300 2005                 2050
   3758 15350 2006                 2050

7 rows selected.
```

<a id="b8f6487e9302fcd9"></a>
## REGR_SYY() OVER

<a id="b1a7020644e698a8"></a>
### Syntax

```
REGR_SYY( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="36eb91a74f025988"></a>
### Description

The window function REGR_SYY is a linear regression function.   
It is an auxiliary function that calculates the diagnostic statistics of the (X, Y) data set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are numeric types.

expr1 is the dependent variable ( y ), and expr2 is the independent variable ( x ).

If expr1 is NULL or expr2 is NULL, it will be excluded from the target.

The following is the calculation formula.

```
REGR_COUNT( expr1, expr2 ) * VAR_POP( expr1 )
```

The returned type is a numeric type.

The returned value is the result of the calculation or NULL.   
If all records are excluded from the target because expr1 or expr2 is NULL, then it returns NULL.

<a id="db6eb1f1f5d8d4a5"></a>
### Example

```
gSQL> 
SELECT item_no,
       price,
       year,
       round( REGR_SYY( price, year ) OVER ( PARTITION BY item_no ), 4 )
       AS "REGR_SYY(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_SYY(price,year)
------- ----- ---- --------------------
   3758 15000 2000          313571.4286
   3758 14700 2001          313571.4286
   3758 15300 2002          313571.4286
   3758 15200 2003          313571.4286
   3758 15100 2004          313571.4286
   3758 15300 2005          313571.4286
   3758 15350 2006          313571.4286

7 rows selected.
```

<a id="45c45d22ae1585c9"></a>
## REPEAT

<a id="01b4391180fb9930"></a>
### Syntax

```
REPEAT( str, num )
```

<a id="54db11ec178338b6"></a>
### Description

The string repeats str as many times as specified by num, and returns the result.

The str argument can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, or BINARY LONG VARYING.

The num argument can be a numeric data type.

If either str or num is NULL, the result will also be NULL.  
If num is 0 or a negative number, the result will be NULL.

The following table describes the result types.

**Result type of REPEAT**

<a id="695889685dd0c90f"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="70fddaba5ee303c9"></a>
### Example

```
gSQL> SELECT REPEAT( 'ab', 3 ) AS RESULT FROM DUAL;
RESULT
------
ababab
1 row selected.
```

<a id="088a48138c2c0bac"></a>
## REPLACE

<a id="f771d5ef549b2a10"></a>
### Syntax

```
REPLACE( str, from, to )
```

<a id="a91615d9521116d3"></a>
### Description

It replaces all occurrences of the *from* string in the string str with the *to* string, and returns the result.

The str argument, the *from* argument, and the *to* argument can be character data types such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

If str is NULL, the result will also be NULL.  
If *from* is NULL, the str is returned without any replacement.  
If the *to* value is omitted or NULL, the str with *from* removed is returned.

The following table describes the result types.

**Result type of REPLACE**

<a id="4173f35c240822bd"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="49cf4ebf653b1db0"></a>
### Example

```
gSQL> SELECT REPLACE( 'HI GLIESE', 'HI', 'HELLO' ) AS RESULT FROM DUAL;
RESULT      
------------
HELLO GLIESE
1 row selected.
```

<a id="a5c8ce6a760ed4d6"></a>
## REVERSE

<a id="fd9d59c828468cc2"></a>
### Syntax

```
REVERSE( str )
```

<a id="90b0f8e8d422b5e2"></a>
### Description

REVERSE returns the characters of str in reverse order.

The str argument can be of types that are convertible to a character string type or a binary string type.  
A character string type is processed in character units, while a binary string type is processed in byte units.

If str is NULL, then it returns NULL.

The following table describes the argument and result types.

**Argument and result type of REVERSE**

<a id="76a8f8501188e79d"></a>
| str | Result type |
| --- | --- |
| CHAR | CHAR |
| VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY | BINARY |
| VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="5ee0ffe941afe4cc"></a>
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

<a id="4849ac41d73729b5"></a>
## ROUND( number )

<a id="43ffd0add51e26a5"></a>
### Syntax

```
ROUND( num [, scale ] )
```

<a id="b44a43c13bd2689e"></a>
### Description

It rounds off num based on the scale, and returns the result.

The num argument and scale argument can be numeric data types.

If scale is omitted, the scale becomes 0 and the function is executed as if it were ROUND(num, 0).  
If scale is a positive number, it is rounded based on the number of digits to the right of the decimal point.  
If scale is a negative number, it is rounded based on the number of digits to the left of the decimal point.  

If either num or scale is NULL, it returns NULL.

<a id="178a111edd332197"></a>
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

<a id="74b35e163196c100"></a>
## ROUND( date )

<a id="1b62dfb25c3b8e2b"></a>
### Syntax

```
ROUND( date [ , fmt ] )
```

<a id="b817eca402b85d2e"></a>
### Description

It rounds off the date in the specified fmt unit and returns the result.

The data type of the date argument can be DATE, TIMESTAMP, or TIMESTAMP WITH TIME ZONE.   
The fmt argument can be a character type such as CHARACTER or CHARACTER VARYING.   
If either the date argument or the fmt argument is NULL, the result will also be NULL.  

The result type is always DATE, regardless of the date argument's data type.

If fmt is omitted, the default is DAY.  
The following table describes the available format strings.

**Available format sting of fmt**

<a id="2ce422202df94a34"></a>
| String | Description |
| --- | --- |
| CC, SCC | It represents the year in four digits, rounded off starting from the 51st year. (e.g., XX01) |
| YYYY, YEAR, SYYYY, SYEAR, YYY, YY, Y | It is rounded off starting from July 1st. |
| IYYY, IYY, IY, I | It represents the year that embraces the calendar week defined by ISO 8601 standards, rounded off starting from July 1st. |
| Q | It is rounded off starting from the 16th day of the second month of the quarter. |
| MONTH, MON, MM, RM | It is rounded off starting from the 16th day. |
| WW | A week starts from January 1st of the year, and it is rounded off on Wednesday at 12 p.m. of the WEEK. |
| IW | It represents the calendar week defined by ISO 8601 standards (1 ~ 52 weeks or 1 ~ 53 weeks), rounded off on Thursday 12 p.m. |
| W | A week starts from the 1st day of the month, and it is rounded off on Wednesday 12 p.m. of the WEEK. |
| DDD, DD, J | It is rounded off at 12 p.m. |
| DAY, DY, D | It is rounded off on Wednesday at 12 p.m. of the WEEK. |
| HH, HH12, HH24 | It is rounded off from 30 minutes. |
| MI | It is rounded off from 30 seconds. |

<a id="959b44c4b7519763"></a>
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

<a id="3125db1255495115"></a>
## ROW_NUMBER() OVER

<a id="8460d391473b928f"></a>
### Syntax

```
ROW_NUMBER( ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="35849e2c35f95124"></a>
### Description

The window function ROW_NUMBER assigns a unique number to each row.  
The unique number is a consecutive integer starting from 1.

A window frame cannot be used.

<a id="1e772e568bde0e79"></a>
### Example

```
gSQL> SELECT department_id, salary,
             ROW_NUMBER() OVER ( ORDER BY salary ) AS row_num
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY ROW_NUM
------------- ------ -------
           60   4200       1
           60   4800       2
           60   4800       3
           60   6000       4
           60   9000       5

5 rows selected.
```

<a id="8758283a97cdf796"></a>
## ROWID_GRID_BLOCK_ID

<a id="a5f29d45f4595926"></a>
### Syntax

```
ROWID_GRID_BLOCK_ID( rowid )
```

<a id="e0fb5e7fcf5638cf"></a>
### Description

It returns the GRID block ID.

> It is valid information in a cluster system.

<a id="39664ef6d0c90d11"></a>
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

<a id="8c5473eab75a8d0d"></a>
## ROWID_GRID_BLOCK_SEQ

<a id="c435bbd3b48dfe61"></a>
### Syntax

```
ROWID_GRID_BLOCK_SEQ( rowid )
```

<a id="5cfbb379378995d0"></a>
### Description

It returns the GRID block sequence.

> It is valid information in a cluster system.

<a id="e10ac55a4ff1f47b"></a>
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

<a id="302c837a4ed91459"></a>
## ROWID_MEMBER_ID

<a id="95acb8f0facfe0d4"></a>
### Syntax

```
ROWID_MEMBER_ID( rowid )
```

<a id="aee4667f14d2ca75"></a>
### Description

It retrieves the member ID.

> It is valid information in a cluster system.

<a id="6d579fa67f65d0d7"></a>
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

<a id="e58e8b325a36c0cd"></a>
## ROWID_OBJECT_ID

<a id="278b704a4d164c88"></a>
### Syntax

```
ROWID_OBJECT_ID( rowid )
```

<a id="6f32d59d0a7cbb82"></a>
### Description

It retrieves the object ID.

> It is an invalid information in a cluster system.

<a id="39581f070f05bef5"></a>
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

<a id="ade88b5651078a78"></a>
## ROWID_PAGE_ID

<a id="5ea0203112a8b887"></a>
### Syntax

```
ROWID_PAGE_ID( rowid )
```

<a id="c076707a5f1aca61"></a>
### Description

It retrieves the page ID.

> It is an invalid information in a cluster system.

<a id="78b2284b5c349303"></a>
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

<a id="19f1ed7225a03628"></a>
## ROWID_ROW_NUMBER

<a id="e3c46a92297d2037"></a>
### Syntax

```
ROWID_ROW_NUMBER( rowid )
```

<a id="b853c00a490a12ce"></a>
### Description

It retrieves the row number.

> It is an invalid information in a cluster system.

<a id="b048c1215ceb18a9"></a>
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

<a id="c3822a2f6ddbd3ca"></a>
## ROWID_SHARD_ID

<a id="4a77f016dbef2c40"></a>
### Syntax

```
ROWID_SHARD_ID( rowid )
```

<a id="f760fd5f8e7de3cf"></a>
### Description

It retrieves the shard ID.

> It is valid information in a cluster system.

<a id="7c5dcc60cc29a837"></a>
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

<a id="eb30fc64dd130c8d"></a>
## ROWID_TABLESPACE_ID

<a id="834bc689a383561f"></a>
### Syntax

```
ROWID_TABLESPACE_ID( rowid )
```

<a id="0976ff35ffe3c72e"></a>
### Description

It retrieves the tablespace ID.

> It is an invalid information in a cluster system.

<a id="f90d0a0dd7dc7f0a"></a>
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

<a id="3c69e446ac188320"></a>
## ROWNUM

<a id="95a0fae51f4fca3e"></a>
### Syntax

```
ROWNUM
```

<a id="ee8ea41b255d73b8"></a>
### Description

It sequentially allocates numbers starting from 1 to the rows that satisfy the WHERE condition.

It allows the use of ROWNUM in the WHERE clause for compatibility with Oracle.

However, to limit the number of query results, it is recommended to use the [offset limit clause](20-sql-references-h-z.md#0980c29c08cd8fe9) (the SQL standard) as follows.

- Describing the number of results using (non-standard) ROWNUM

```
gSQL> SELECT * FROM t1 WHERE ROWNUM <= 3;

C1
--
A 
B 
C 

3 rows selected.
```

- Describing the number of results using (SQL-standard) FETCH statement

```
gSQL> SELECT * FROM t1 FETCH 3;

C1
--
A 
B 
C 

3 rows selected.
```

To restrict the range of query results, it is recommended to use the OFFSET and FETCH statements as follows.

- Describing the range of result counts using (non-standard) ROWNUM

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

- Describing the range of result counts using (SQL standard) ROWNUM OFFSET and FETCH statements

```
gSQL> SELECT c1 FROM t1 OFFSET 1 FETCH 2;

C1
--
B 
C 

2 rows selected.
```

It is not recommended to use ROWNUM in the WHERE clause for purposes other than restricting the number of results.

The results for the same query may vary depending on the execution method when using the ambiguous condition (WHERE c1 < ROWNUM + 3), as shown below.

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

- In the case of Oracle

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

- In the case of GOLDILOCKS

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

<a id="7de3c5d818acac36"></a>
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

<a id="63806191e5a3cf12"></a>
## RPAD

<a id="1312ba28d743a885"></a>
### Syntax

```
RPAD( str, length, [, fill] )
```

<a id="193969c427c6038d"></a>
### Description

It adds a fill string to the right side of str until the string's length reaches the specified length, and then returns the result.

The str argument can be a character type, such as CHARACTER, CHARACTER VARYING, CHARACTER LONGVARYING, or a binary character type, such as BINARY, BINARY VARYING, BINARY LONG VARYING.

The length argument can be a numeric type.

length refers to the number of characters, with its maximum range being the maximum PRECISION of the result type.   
If fill is omitted, a whitespace is added by default.  
If str is longer than length, it will be truncated to fit the specified length before being returned.  
If any of str, length, or fill is NULL, the result will also be NULL.   
If length is 0 or a negative number, the result will also be NULL.

The following table describes the result types.

**Result type of RPAD**

<a id="82d312022f1a5ce8"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="edab1640e12e6081"></a>
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

<a id="defacd4fef7e10c1"></a>
## RTRIM

<a id="70c307e93d4ecee1"></a>
### Syntax

```
RTRIM( trim_source [, trim_character ] )
```

<a id="155f03ccfbe5e507"></a>
### Description

It removes matching characters by comparing from the right side of trim_character in trim_source, continuing until no matching character is found. Then, it returns the result.

The trim_character and trim_source arguments can be of a character type, such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type, such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If either trim_character or trim_source is NULL, the result will also be NULL.  
If trim_character is omitted, a single blank space (' ') is specified by default.

The following table describes the result types.

**Result type of RTRIM**

<a id="9ec0d5805de041ae"></a>
| trim_source type, trim_character type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="b8759eacd5daba10"></a>
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

<a id="1e212dba8d6c5a39"></a>
## SESSION_ID

<a id="b20fd6f156c24360"></a>
### Syntax

```
SESSION_ID()
```

<a id="b88a0488486bc4c1"></a>
### Description

It retrieves the current session ID.

<a id="4e1d0ace31d6e925"></a>
### Example

```
gSQL> SELECT SESSION_ID() FROM dual;

SESSION_ID()
------------
           4

1 row selected.
```

<a id="a1540a88dca6d4c6"></a>
## SESSION_SERIAL

<a id="88a18eb8667da3e3"></a>
### Syntax

```
SESSION_SERIAL()
```

<a id="480059cb8a8d12ba"></a>
### Description

It retrieves the serial number of the current session.

<a id="e181cc103be3c23c"></a>
### Example

```
gSQL> SELECT SESSION_SERIAL() FROM dual;

SESSION_SERIAL()
----------------
              16

1 row selected.
```

<a id="1991305773bb0cac"></a>
## SESSION_USER

<a id="f12c5a050235cb5c"></a>
### Syntax

```
SESSION_USER[()]
```

<a id="94442868aa3e3927"></a>
### Description

It returns the session's user.

User information is managed in three types, as follows.

- Logon user: It is a user who performed login, and it is maintained until the connection is closed.
- Session user: It is the same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: It is generally the same as the session user, but it is temporarily changed internally in system to control access when using the PSM, view.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="2f4eefd600624719"></a>
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

<a id="06d78e4d0eeda18a"></a>
## SESSIONTIMEZONE

<a id="38bf7766738faa70"></a>
### Syntax

```
SESSIONTIMEZONE()
```

<a id="3bd77bc56a439486"></a>
### Description

SESSIONTIMEZONE returns the time zone of the current session.   
The returned value is in the '[+|-]TZH:TZM' format.  
The returned type is varchar.

<a id="3c0b7a8424644a18"></a>
### Example

Check the time zone of the current session.

```
gSQL> SELECT SESSIONTIMEZONE() FROM dual;

SESSIONTIMEZONE()
-----------------
+09:00           

1 row selected.
```

When modifying the time zone of the current session, it returns the updated time zone value.

```
gSQL> SET TIME ZONE '-05:00';

Session set.

gSQL> SELECT SESSIONTIMEZONE() FROM dual;

SESSIONTIMEZONE()
-----------------
-05:00           

1 row selected.
```

<a id="9356f5de29f1f0c2"></a>
## SHARD_GROUP_ID

<a id="e73f63906514eaa8"></a>
### Syntax

```
SHARD_GROUP_ID( table_name, shard_key_value [, ... ] )
```

<a id="d847fb37abe4d40c"></a>
### Description

It returns the group ID managing the shard that stores the shard_key_value when the shard strategy is defined in table_name.

The table_name (an input argument) must be specified as an identifier. If the object corresponding to the table_name is not a base table, or if the shard strategy is not defined, an error will occur.

The shard_key_value (an input argument) must be listed in the same order as the shard key columns in the shard strategy defined in table_name. If the number of shard_key_value entries does not match the number of shard key columns, an error will occur.

The result type is NATIVE_BIGINT.

> It is valid information in a cluster system.

<a id="19bd4063d9c49be6"></a>
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

<a id="784029460bb64147"></a>
## SHARD_GROUP_NAME

<a id="3875fb35647a4e90"></a>
### Syntax

```
SHARD_GROUP_NAME( table_name, shard_key_value [, ... ] )
```

<a id="c64d8ca75fc64ced"></a>
### Description

It returns the group NAME managing the shard that stores the shard_key_value when the shard strategy is defined in table_name.

The table_name (an input argument) must be specified as an identifier. If the object corresponding to the table_name is not a base table, or if the shard strategy is not defined, an error will occur.

The shard_key_value (an input argument) must be listed in the same order as the shard key columns in the shard strategy defined in table_name. If the number of shard_key_value entries does not match the number of shard key columns, an error will occur.

The result type is VARCHAR.

> It is valid information in a cluster system.

<a id="4634f7198bfd3c33"></a>
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

<a id="68e5e1fa36c9d98b"></a>
## SHARD_ID

<a id="40c8c532dabeef22"></a>
### Syntax

```
SHARD_ID( table_name, shard_key_value [, ... ] )
```

<a id="91387bfc2ef3a7b8"></a>
### Description

It returns the ID of the shard that stores the shard_key_value when the shard strategy is defined in table_name.

The table_name (an input argument) must be specified as an identifier. If the object corresponding to the table_name is not a base table, or if the shard strategy is not defined, an error will occur.

The shard_key_value (an input argument) must be listed in the same order as the shard key columns in the shard strategy defined in table_name. If the number of shard_key_value entries does not match the number of shard key columns, an error will occur.

The result type is NATIVE_BIGINT.

> It is valid information in a cluster system.

<a id="f4dffc47c964c429"></a>
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

<a id="1a5da4a9371f44a0"></a>
## SHARD_NAME

<a id="3a6d2818d91fbd49"></a>
### Syntax

```
SHARD_NAME( table_name, shard_key_value [, ... ] )
```

<a id="1c31a0c19b6e446a"></a>
### Description

It returns the NAME of the shard that stores the shard_key_value when the shard strategy is defined in table_name.

The table_name (an input argument) must be specified as an identifier. If the object corresponding to the table_name is not a base table, or if the shard strategy is not defined, an error will occur.

The shard_key_value (an input argument) must be listed in the same order as the shard key columns in the shard strategy defined in table_name. If the number of shard_key_value entries does not match the number of shard key columns, an error will occur.

The result type is VARCHAR.

> It is valid information in a cluster system.

<a id="5124fce164c37859"></a>
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

<a id="8c4d8eb730a7ae5c"></a>
## SHIFT_LEFT

<a id="5cf427252542c8c7"></a>
### Syntax

```
SHIFT_LEFT( num, cnt )
```

<a id="c55d377ff62278fc"></a>
### Description

It returns the value obtained by shifting num to the left by cnt bits.

The data types of the input num and cnt arguments can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or any type that can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT, the decimal point is truncated.

cnt is masked with 6 bits and is processed to a value within the 6-bit range.

If either num or cnt is NULL, the result will also be NULL.

The result type is NATIVE_BIGINT.

<a id="2438e3f5b82a3473"></a>
### Example

```
gSQL> SELECT SHIFT_LEFT(1, 3) FROM DUAL;
SHIFT_LEFT(1, 3)
----------------
               8
1 row selected.
```

<a id="be8f3a3649231204"></a>
## SHIFT_RIGHT

<a id="84c768d6e14f675b"></a>
### Syntax

```
SHIFT_RIGHT( num, cnt )
```

<a id="0f81e6aed79fe17d"></a>
### Description

It returns the value obtained by shifting num to the right by cnt bits.

The data types of the input num and cnt arguments can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or any type that can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.

cnt is masked with 6 bits and is processed to a value within the 6-bit range.

If either num or cnt is NULL, the result will also be NULL.

The result type is NATIVE_BIGINT.

<a id="0bb7b237a72ef5a3"></a>
### Example

```
gSQL> SELECT SHIFT_RIGHT(8, 3) FROM DUAL;
SHIFT_RIGHT(8, 3)
-----------------
                1
1 row selected.
```

<a id="7baca0f310be0340"></a>
## SIGN

<a id="431e179bb7c165b1"></a>
### Syntax

```
SIGN( num )
```

<a id="c9adc83b90daf2ca"></a>
### Description

It returns the sign of num.

The num argument can be of a numeric data type.

The return value is as follows.   
• If num < 0,  -1 is returned.  
• If num = 0, 0 is returned.  
• If num > 0, 1 is returned.

If num is NULL, the result will also be NULL.

<a id="a0b2ac7121e03b9d"></a>
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

<a id="519eef61f86535a5"></a>
## SIN

<a id="8e804fd5473e64e8"></a>
### Syntax

```
SIN( num )
```

<a id="06ab267124e8235c"></a>
### Description

It returns the sine value of num.  
If num is NULL, the result will also be NULL.

<a id="89bd9f7bdc642cb9"></a>
### Example

```
gSQL> SELECT SIN( 0 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="9144e8314d0b83cc"></a>
## SPLIT_PART

<a id="f71c2eb551a97b82"></a>
### Syntax

```
SPLIT_PART( string, delimiter, field )
```

<a id="b31223b920231ead"></a>
### Description

It returns a string of the field, using the specified delimiter character within the string.

The data types of the string and delimiter arguments can be character data types, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

The field argument can be a numeric data type.

If either string, delimiter, or field is NULL, the result will also be NULL. The value of field must be a numeric value greater than 1; if it is 0 or a negative number, an error will be returned.

The following table describes the result types.

**Result type of SPLIT_PART**

<a id="c8a203a8c5338ec4"></a>
| string type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="e5335b0904b5370b"></a>
### Example

```
gSQL> SELECT SPLIT_PART( 'AB;CD;EF;GH', ';', 3  ) AS RESULT FROM DUAL;
RESULT
------
EF    
1 row selected.
```

<a id="06f4b7fab8af7238"></a>
## SQRT

<a id="15e7e52876c02398"></a>
### Syntax

```
SQRT( num )
```

<a id="0ddf7a647a4c3f64"></a>
### Description

It returns the square root of num.

The num argument can be a numeric type and must be a value greater than or equal to 0 (non-negative).  
If the num argument is NULL, the result will also be NULL.

<a id="7df860e4811042e8"></a>
### Example

```
gSQL> SELECT SQRT( 9 ) AS RESULT FROM DUAL;
RESULT
------
     3
1 row selected.
```

<a id="3ba5dfafe71fd478"></a>
## STATEMENT_DATE

<a id="8d18a7b4abd3e519"></a>
### Syntax

```
STATEMENT_DATE()
CURRENT_DATE [()]
```

<a id="5c6f5ae75b86af20"></a>
### Description

It retrieves the current date (of DATE type).

The differences among the functions for obtaining the current date are as follows.  

• TRANSACTION_DATE(): All date values within the transaction are the same.  
• STATEMENT_DATE(): All date values within an SQL statement are the same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is returned.

<a id="514c44affccd0c84"></a>
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

<a id="3b96012a99b7f57b"></a>
## STATEMENT_LOCALTIME

<a id="7b7502ab8124bd3d"></a>
### Syntax

```
STATEMENT_LOCALTIME()
LOCALTIME [()]
```

<a id="a02afd9535201321"></a>
### Description

It retrieves the current value of the TIME WITHOUT TIME ZONE type based on the session time.

LOCALTIME is an SQL standard function.

The differences among the functions for obtaining the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values within the transaction are the same.  
• TATEMENT_LOCALTIME(): All time values within an SQL statement are the same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is returned.

<a id="5aa27f2132c96d1f"></a>
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

<a id="b9af643d31fd0351"></a>
## STATEMENT_LOCALTIMESTAMP

<a id="ffe287905be3f80f"></a>
### Syntax

```
STATEMENT_LOCALTIMESTAMP()
LOCALTIMESTAMP [()]
```

<a id="0cd5c8985d4529f6"></a>
### Description

It retrieves the current value of the TIMESTAMP WITHOUT TIME ZONE type based on the session time.

LOCALTIMESTAMP is an SQL standard function.

The differences among the functions for obtaining the current timestamp are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All TIMESTAMP values within the transaction are the same.  
• STATEMENT_LOCALTIMESTAMP(): All TIMESTAMP values within an SQL statement are the same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is returned.

<a id="48019908e6d3f356"></a>
### Example

All rows contain the same value.

```
gSQL> SELECT STATEMENT_LOCALTIMESTAMP() FROM t1;

STATEMENT_LOCALTIMESTAMP()
--------------------------
2013-12-12 16:23:39.782187
2013-12-12 16:23:39.782187
2013-12-12 16:23:39.782187

3 rows selected.
```

<a id="944704796ac0d078"></a>
## STATEMENT_TIME

<a id="d6a8baa1da2e1f0a"></a>
### Syntax

```
STATEMENT_TIME()
CURRENT_TIME [()]
```

<a id="5d800470061f3828"></a>
### Description

It retrieves the current value of the TIME WITH TIME ZONE type.

CURRENT_TIME is an SQL standard function.

The differences among the functions for obtaining the current time are as follows.  

• TRANSACTION_TIME(): All time values within the transaction are the same.  
• STATEMENT_TIME(): All time values within an SQL statement are the same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is returned.

<a id="a89dd68fcd7eb985"></a>
### Example

All rows contain the same value.

```
gSQL> SELECT STATEMENT_TIME() AS result FROM t1;

RESULT                
----------------------
16:28:19.268513 +09:00
16:28:19.268513 +09:00
16:28:19.268513 +09:00

3 rows selected.
```

<a id="9651210adb0ca813"></a>
## STATEMENT_TIMESTAMP

<a id="213ad2554fea929d"></a>
### Syntax

```
STATEMENT_TIMESTAMP()
CURRENT_TIMESTAMP [()]
```

<a id="e39d21415910361b"></a>
### Description

It retrieves the current value of the TIMESTAMP WITH TIME ZONE type.

CURRENT_TIMESTAMP is an SQL standard function.

The differences among the functions for obtaining the current timestamp are as follows.  

• TRANSACTION_TIMESTAMP(): All TIMESTAMP values within the transaction are the same.  
• STATEMENT_TIMESTAMP(): All TIMESTAMP values within an SQL statement are the same.  
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is returned.

<a id="485d51df1a82cd13"></a>
### Example

All rows contain the same value.

```
gSQL> SELECT STATEMENT_TIMESTAMP() AS result FROM t1;

RESULT                           
---------------------------------
2013-12-12 16:36:11.032957 +09:00
2013-12-12 16:36:11.032957 +09:00
2013-12-12 16:36:11.032957 +09:00

3 rows selected.
```

<a id="ab2f5de729ed4cf9"></a>
## STATEMENT_VIEW_SCN

<a id="8ca2ed7784cb2331"></a>
### Syntax

```
STATEMENT_VIEW_SCN()
```

<a id="4321242d7f75c92e"></a>
### Description

It retrieves the VIEW SCN of the current STATEMENT.

<a id="4884e01c8bcbb3c4"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN() FROM dual;

STATEMENT_VIEW_SCN()
--------------------
17697.658.17880     

1 row selected.
```

<a id="1dbdb0d5e7d54954"></a>
## STATEMENT_VIEW_SCN_DCN

<a id="09b6e01d9db0c95c"></a>
### Syntax

```
STATEMENT_VIEW_SCN_DCN()
```

<a id="b0e4e6faec826e72"></a>
### Description

It retrieves the Domain Change Number (DCN) value of the VIEW SCN for the current STATEMENT.

<a id="51b1097f09965b68"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_DCN() FROM dual;

STATEMENT_VIEW_SCN_DCN()
------------------------
                     658

1 row selected.
```

<a id="a9e6925109044ba6"></a>
## STATEMENT_VIEW_SCN_GCN

<a id="491d10f6306db2d4"></a>
### Syntax

```
STATEMENT_VIEW_SCN_GCN()
```

<a id="5a54e39fc279c1bd"></a>
### Description

It retrieves the Global Change Number (GCN) value of the VIEW SCN for the current STATEMENT.

<a id="2aee230465081dca"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_GCN() FROM dual;

STATEMENT_VIEW_SCN_GCN()
------------------------
                   17697

1 row selected.
```

<a id="7b88db428292689b"></a>
## STATEMENT_VIEW_SCN_LCN

<a id="b915156880262210"></a>
### Syntax

```
STATEMENT_VIEW_SCN_LCN()
```

<a id="51e376a1a5d2f1df"></a>
### Description

It retrieves the Local Change Number (LCN) value of the VIEW SCN for the current STATEMENT.

<a id="81b6b0c6c8355b77"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_LCN() FROM dual;

STATEMENT_VIEW_SCN_LCN()
------------------------
                   17880

1 row selected.
```

<a id="846fb9419b4408b2"></a>
## STDDEV

<a id="474fcaa5ad512489"></a>
### Syntax

```
STDDEV( [ ALL | DISTINCT ] expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="2c437eccd67f2faa"></a>
### Description

It is an aggregation function, and it calculates the standard deviation of an expr set.

When ALL is specified, it is performed on all values. When DISTINCT is specified, it is performed on the values with duplicates removed. If neither is specified, it is treated as if ALL were specified.

If FILTER is specified, the aggregation is performed only for the values that satisfy the condition.

If the number of expr sets, excluding NULL values after duplicates are removed using DISTINCT, is one, it returns 0, similar to [VARIANCE](#fa3ad26fea8effe3).

The following table describes the argument and result types.

**Argument and result type of STDDEV**

<a id="afe60ed8a1458e92"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

GOLDILOCKS calculates the standard deviation as follows.  
　• If the number of expr sets is 1, it returns 0.  
　• If the number of expr sets is greater than 1, it returns the value of [STDDEV_SAMP( expr )](#ede27e56f90e140c).

> The standard deviation is the positive square root of the variance, and it is obtained by calculating the square root of the variance. In other words, the STDDEV function is equivalent to the square root of the [VARIANCE](#fa3ad26fea8effe3) function.  
>   
> STDDEV( [ ALL ] expr )  
>  = SQRT( VARIANCE( [ ALL ] expr ) )  
>   
> STDDEV( DISTINCT expr )  
>  = SQRT( VARIANCE( DISTINCT expr ) )

<a id="4fe845bdbe95067d"></a>
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


gSQL> SELECT STDDEV(c1) FILTER( WHERE c1 > 0 ) FROM t1;

      STDDEV(C1)
----------------
11.4978258814438

1 row selected.
```

<a id="0d306a5e79990e63"></a>
## STDDEV() OVER

<a id="60f024ebdfc4643f"></a>
### Syntax

```
STDDEV ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="aa13052ae1ee5ea9"></a>
### Description

The window function STDDEV calculates the standard deviation of expr.   
If the number of expr values, excluding NULLs, is one, it returns 0 as the result.

<a id="99c870e445c10970"></a>
### Example

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , STDDEV( min_price ) OVER ( ORDER BY min_price ) AS "STDDEV"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE           STDDEV
--------- ----------------
       73                0
      247 123.036579926459
      731 340.953564775811
     null 340.953564775811
     null 340.953564775811

5 rows selected.
```

<a id="c40e9f4ed7b6baf7"></a>
## STDDEV_POP

<a id="cb6f0376066f775b"></a>
### Syntax

```
STDDEV_POP( expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="c2ccd41c9f6b87e1"></a>
### Description

It is an aggregation function, and it calculates the population standard deviation of an expr set.   
If the number of expr set values, excluding NULLs, is one, it returns 0.

If FILTER is specified, the aggregation is performed only for the values that satisfy the condition.

The following table describes the argument and result types.

**Argument and result type of STDDEV_POP**

<a id="1b6c444b9664b8f5"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The population standard deviation is the positive square root of the population variance, and it is obtained by calculating the square root of the population variance. In other words, the STDDEV_POP function is equivalent to the square root of the [VAR_POP](#d3d9330ec5d2493a) function.  
>   
> STDDEV_POP( expr )  
>  = SQRT( VAR_POP( expr ) )

<a id="b65efdd6aa77f38d"></a>
### Example

```
gSQL> SELECT STDDEV_POP(c1) FROM t1;

 STDDEV_POP(C1)
---------------
10.283968105746

1 row selected.


gSQL> SELECT STDDEV_POP(c1) FILTER( WHERE c1 > 0 ) FROM t1;

 STDDEV_POP(C1)
---------------
10.283968105746

1 row selected.
```

<a id="b62a4ce3fbe7f69a"></a>
## STDDEV_POP() OVER

<a id="0c202c08866e8bd5"></a>
### Syntax

```
STDDEV_POP ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="4b7cc8c87f74979f"></a>
### Description

The window function STDDEV_POP calculates the population standard deviation of expr.   
If the number of expr values, excluding NULLs, is one, it returns 0 as the result.

<a id="49d462915425a937"></a>
### Example

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , STDDEV_POP( min_price ) OVER ( ORDER BY min_price ) AS "STDDEV_POP"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE      STDDEV_POP
--------- ---------------
       73               0
      247              87
      731 278.38741989457
     null 278.38741989457
     null 278.38741989457

5 rows selected.
```

<a id="ede27e56f90e140c"></a>
## STDDEV_SAMP

<a id="686dba15cff98800"></a>
### Syntax

```
STDDEV_SAMP( expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="2b3b4e7551ede019"></a>
### Description

It is an aggregation function, and it calculates the sample standard deviation of an expr set.   
If the number of expr set values, excluding NULLs, is one, it returns NULL.

If FILTER is specified, the aggregation is performed only for the values that satisfy the condition.

The following table describes the argument and result types.

**Argument and result type of STDDEV_SAMP**

<a id="7ae19e349f0fec4f"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The sample standard deviation is the positive square root of the sample variance, and it is obtained by calculating the square root of the sample variance. In other words, the STDDEV_SAMP function is equivalent to the square root of the [VAR_SAMP](#fc3eda323e3927d6) function.  
>   
> STDDEV_SAMP( expr )  
>  = SQRT( VAR_SAMP( expr ) )

<a id="3dfd49210dfe453b"></a>
### Example

```
gSQL> SELECT STDDEV_SAMP(c1) FROM t1;

 STDDEV_SAMP(C1)
----------------
11.4978258814438

1 row selected.


gSQL> SELECT STDDEV_SAMP(c1) FILTER( WHERE c1 > 0 ) FROM t1;

 STDDEV_SAMP(C1)
----------------
11.4978258814438

1 row selected.
```

<a id="dff5254ae89fb63b"></a>
## STDDEV_SAMP() OVER

<a id="887386ab2560d44e"></a>
### Syntax

```
STDDEV_SAMP ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="4a99f922acf6855a"></a>
### Description

The window function STDDEV_SAMP calculates the sample standard deviation of expr.   
If the number of expr values, excluding NULLs, is one, it returns NULL as the result.

<a id="a9dfb0c26b26be15"></a>
### Example

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , STDDEV_SAMP( min_price ) OVER ( ORDER BY min_price ) AS "STDDEV_SAMP"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE      STDDEV_SAMP
--------- ----------------
       73             null
      247 123.036579926459
      731 340.953564775811
     null 340.953564775811
     null 340.953564775811

5 rows selected.
```

<a id="0bc3017b9662aa76"></a>
## STRING_AGG() OVER

<a id="8572b76202112e14"></a>
### Syntax

```
STRING_AGG( str [, delimiter] ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="534369a63f8c2da3"></a>
### Description

The window function STRING_AGG connects str according to the execution range defined in the OVER clause.

If str is NULL, it will be excluded.

A delimiter is str connection delimiter, and if omitted, the default value is NULL.

str can be either a character string or a binary string.   
If str is a character string, the result type will be varchar.   
If str is a binary string, then the result type will be varbinary.

<a id="51abd321e498a767"></a>
### Example

```
gSQL> 
SELECT regionkey,
       name,
       STRING_AGG( name ) OVER ( PARTITION BY regionkey
                                 ORDER BY nationkey
                                 ROWS BETWEEN UNBOUNDED PRECEDING 
                                          AND CURRENT ROW ) 
       AS "STRING_AGG( name ) OVER",
       STRING_AGG( name, ', ' ) OVER ( PARTITION BY regionkey
                                       ORDER BY nationkey
                                       ROWS BETWEEN UNBOUNDED PRECEDING
                                                AND CURRENT ROW ) 
       AS "STRING_AGG( name, ', ' ) OVER"  
  FROM nation;

REGIONKEY NAME    STRING_AGG( name ) OVER STRING_AGG( name, ', ' ) OVER
--------- ------- ----------------------- -----------------------------
        1 BRAZIL  BRAZIL                  BRAZIL                       
        1 CANADA  BRAZILCANADA            BRAZIL, CANADA               
        1 PERU    BRAZILCANADAPERU        BRAZIL, CANADA, PERU         
        1 null    BRAZILCANADAPERU        BRAZIL, CANADA, PERU         
        2 null    null                    null                         
        2 INDIA   INDIA                   INDIA                        
        2 null    INDIA                   INDIA                        
        2 null    INDIA                   INDIA                        
        2 JAPAN   INDIAJAPAN              INDIA, JAPAN                 
        2 CHINA   INDIAJAPANCHINA         INDIA, JAPAN, CHINA          
        2 null    INDIAJAPANCHINA         INDIA, JAPAN, CHINA          
        2 VIETNAM INDIAJAPANCHINAVIETNAM  INDIA, JAPAN, CHINA, VIETNAM 
        3 EGYPT   EGYPT                   EGYPT                        
        3 IRAN    EGYPTIRAN               EGYPT, IRAN                  
        3 IRAQ    EGYPTIRANIRAQ           EGYPT, IRAN, IRAQ            

15 rows selected.
```

<a id="6d713ac965ddd147"></a>
## SUBSTR

<a id="901551ffbfd11023"></a>
### Syntax

```
SUBSTR( str FROM start_position [ FOR string_length ] )
SUBSTR( str, start_position [ , string_length ] )
```

<a id="564c88a9309b452d"></a>
### Description

It is an alias of [SUBSTRING](#c9a451794ac8d7d6).

<a id="1381cd7b6f1b9b0a"></a>
### Example

- Multi-byte character set (e.g. UTF8): 1 byte character

```
gSQL> SELECT 
      SUBSTR( 'DATABASE MANAGEMENT SYSTEM', 10, 10 ) AS RESULT 
      FROM DUAL;
RESULT    
----------
MANAGEMENT
1 row selected.
```

- Multi-byte character set (e.g. UTF8): 2 bytes or 3 bytes character

```
gSQL> SELECT SUBSTR( '“αβ≠ΑΒ”', 2, 5 ) AS RESULT FROM DUAL;
RESULT
------
αβ≠ΑΒ 
1 row selected.
```

<a id="b888761fc5a7b8e9"></a>
## SUBSTRB

<a id="5f4b26762bcd6668"></a>
### Syntax

```
SUBSTRB( str, start_position [ , string_length ] )
```

<a id="1f140d4a0bb05d8c"></a>
### Description

It extracts characters within the string_length range, starting from start_position, and returns the result for str.

This function is the same as the [SUBSTRING](#c9a451794ac8d7d6) function, except that the start_position and string_length in the SUBSTR function are calculated in byte units.

<a id="85c933789b627f71"></a>
### Example

- Multi-byte character set (e.g. UTF8): 1 byte character

```
gSQL> SELECT 
      SUBSTRB( 'DATABASE MANAGEMENT SYSTEM', 10, 10 ) AS RESULT 
      FROM DUAL;
RESULT    
----------
MANAGEMENT
1 row selected.
```

- Multi-byte character set (e.g. UTF8): 2 bytes or 3 bytes character

```
gSQL> SELECT SUBSTRB( '“αβ≠ΑΒ”', 4, 11 ) AS RESULT FROM DUAL;
RESULT
------
αβ≠ΑΒ 
1 row selected.
```

<a id="c9a451794ac8d7d6"></a>
## SUBSTRING

<a id="94744c9311a115d4"></a>
### Syntax

```
SUBSTRING( str FROM start_position [ FOR string_length ] )  
SUBSTRING( str, start_position [ , string_length ] )
```

<a id="3c3e1279b6b4c643"></a>
### Description

It extracts characters within the string_length range, starting from start_position, and returns the result for str.

The str argument data type can be a character type, such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary data type, such as BINARY, BINARY VARYING, BINARY LONG VARYING.

The start_position and string_length arguments can be of a numeric data type.

If any of str, start_position, or string_length is NULL, the result will be NULL.   
Both start_position and string_length start at 1 and are calculated in character units according to the character set (not in byte units).

If start_position is 0, it is set to 1.   
If start_position is a positive number, it searches for the position forwards (to the right) from the beginning of str.   
If start_ position is a negative number, it searches for the position backwards (to the left) from the end of str.   
If string_length is omitted, characters from start_position to the last character of str are returned.

If string_length is 0 or a negative number, the result will be NULL.  
If start_position > (str length), the result will be NULL.  
If (str length + start_position) < 0, the result will be NULL.

It is an alias of [SUBSTR](#6d713ac965ddd147).  
For more information, refer to [SUBSTRB](#b888761fc5a7b8e9).

The following table describes the result types.

**Result type of SUBSTRING**

<a id="1d4ace9a3c927ad7"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="986afc5a80918d5e"></a>
### Example

- Multi-byte character set (e.g. UTF8): 1 byte character

```
gSQL> SELECT 
      SUBSTRING( 'DATABASE MANAGEMENT SYSTEM' FROM 10 FOR 10 ) AS RESULT 
      FROM DUAL;
RESULT    
----------
MANAGEMENT
1 row selected.
```

- Multi-byte character set (e.g. UTF8): 2 bytes or 3 bytes character

```
gSQL> SELECT SUBSTRING( '“αβ≠ΑΒ”' FROM 2 FOR 5 ) AS RESULT FROM DUAL;
RESULT
------
αβ≠ΑΒ 
1 row selected.
```

<a id="07ac6a4ba1ffd0d0"></a>
## SUM

<a id="98ed6a47d58849b7"></a>
### Syntax

```
SUM( [ ALL | DISTINCT ] expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="3d5ffa16c31ce735"></a>
### Description

It is an aggregate function that returns the sum of the expr values.

If ALL is explicitly specified, aggregation is performed on all values.  
If DISTINCT is explicitly specified, aggregation is performed on the values excluding duplicates.  
If neither ALL nor DISTINCT is specified, the aggregation is performed as if ALL were specified.

If FILTER is specified, the aggregation is performed only on the values that satisfy the condition.

<a id="a8e8a48f5d9917c8"></a>
### Example

```
gSQL> SELECT SUM( c1 ) FROM t1;

SUM(C1)
-------
      6

1 row selected.


gSQL> SELECT SUM( c1 ) FILTER( WHERE c1 > 1 ) FROM t1;

SUM(C1)
-------
      5

1 row selected.
```

<a id="670852541b343c04"></a>
## SUM() OVER

<a id="279c4617b68a0fea"></a>
### Syntax

```
SUM ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="515dcf8786260839"></a>
### Description

The window function SUM calculates the sum of the expr values.  
NULLs are excluded from the calculation.

<a id="bd36cbd4da6f1364"></a>
### Example

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , SUM( min_price ) OVER ( ORDER BY min_price ) AS "SUM"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE  SUM
--------- ----
       73   73
      247  320
      731 1051
     null 1051
     null 1051

5 rows selected.
```

<a id="0ed762465c5eb8c3"></a>
## SYSDATE

<a id="6bd76dd00d946417"></a>
### Syntax

```
SYSDATE
```

<a id="cd2e008f3d791976"></a>
### Description

It returns the current DATE value based on the OS time of the database server.

<a id="fef1ac281302bebb"></a>
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

<a id="63de58248675b940"></a>
## SYS_EXTRACT_UTC

<a id="a7982aa0cc47489e"></a>
### Syntax

```
SYS_EXTRACT_UTC( datetime_with_timezone )
```

<a id="cb8a02fd2176d374"></a>
### Description

It returns the UTC (Coordinated Universal Time, formerly known as Greenwich Mean Time) value.  
If the timezone is not specified, it is calculated based on the session time zone.

The data type of an input argument can be TIME, TIME WITH TIME ZONE, TIMESTAMP, or TIMESTAMP WITH TIME ZONE.  
The result type will be either TIME or TIMESTAMP.

<a id="57ce33a16ffc23b7"></a>
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

<a id="8c555df283556811"></a>
## SYSTIME

<a id="c0eba13dca86b9e2"></a>
### Syntax

```
SYSTIME
```

<a id="b39b554bfe992242"></a>
### Description

It returns the current TIME WITH TIME ZONE value based on the OS time of the database server.

<a id="804e577dc6133db8"></a>
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

<a id="bb8441e714395584"></a>
## SYSTIMESTAMP

<a id="821ddc5c201f3669"></a>
### Syntax

```
SYSTIMESTAMP
```

<a id="719003107395e065"></a>
### Description

It returns the current TIMESTAMP WITH TIME ZONE value based on the OS time of the database server.

<a id="b7358c9488c05864"></a>
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

<a id="77a8c39a1b430f52"></a>
## TABLE_PHYSICAL_STATS

<a id="613d1255f561c800"></a>
### Syntax

```
TABLE_PHYSICAL_STATS( [schema_name.]table_name [,sampling_ratio_value] )
```

<a id="0577edba08267dd3"></a>
### Description

TABLE_PHYSICAL_STATS is a function that returns fragmentation information for the pages allocated to a table.

The input parameter table_name must be specified as an identifier, and an error is raised if the corresponding object is not a base table.

The input parameter sampling_ratio_value represents the percentage (%) of the total pages owned by the object that will be accessed for analysis.   
By randomly sampling and analyzing only a subset of pages instead of processing all pages, the operation can be performed more quickly and efficiently.   
The Used and Fragmented values in the result represent the sizes analyzed based on the sampled pages, not the total allocated pages.   
If this parameter is omitted, a default value of 100% is applied, and all pages are analyzed.  
The valid range of this value is 1 to 100. An error is returned if the value is outside this range.

The result type is VARCHAR and includes the fields Page, Used, and Fragmented.  
• Page: The total number of pages allocated to the table.  
• Used: The size of the used space, which is the sum of the page header size and the size of the stored data. The unit is bytes.  
• Fragmented: The size of the fragmented space, in bytes.

> GLOBAL_DUAL can be used to retrieve this information from all nodes in the cluster.

<a id="b648c3a0dc42bfa4"></a>
### Example

- When using DUAL
    - Returns the object information of the connected node.
    - In a cluster environment, a cluster domain can be specified.

```
gSQL> SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(T1) FROM DUAL;
CLUSTER_MEMBER_NAME TABLE_PHYSICAL_STATS(T1)                     
------------------- ---------------------------------------------
G1N1                Page: 992, Used: 4935498, Fragmented: 2133312
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(PUBLIC.T1) FROM DUAL;
CLUSTER_MEMBER_NAME TABLE_PHYSICAL_STATS(PUBLIC.T1)              
------------------- ---------------------------------------------
G1N1                Page: 992, Used: 4935498, Fragmented: 2133312
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(PUBLIC.T1, 50) FROM DUAL;
CLUSTER_MEMBER_NAME TABLE_PHYSICAL_STATS(PUBLIC.T1, 50)          
------------------- ---------------------------------------------
G1N1                Page: 992, Used: 2497724, Fragmented: 1079680
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(T1) FROM DUAL@G1N1
      UNION ALL
      SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(T1) FROM DUAL@G2N1
      UNION ALL
      SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(T1) FROM DUAL@G3N1;
CLUSTER_MEMBER_NAME TABLE_PHYSICAL_STATS(T1)                        
------------------- ------------------------------------------------
G1N1                Page: 992, Used: 4935498, Fragmented: 2133312   
G2N1                Page: 2912, Used: 14806136, Fragmented: 6400000 
G3N1                Page: 5760, Used: 29611846, Fragmented: 12800000
3 rows selected.
```

- When using GLOBAL_DUAL
    - Returns the object information from all nodes in the cluster environment.
    - A cluster domain can be specified.

```
gSQL> SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(PUBLIC.T1, 50)
        FROM GLOBAL_DUAL
      ORDER BY CLUSTER_MEMBER_NAME;
CLUSTER_MEMBER_NAME TABLE_PHYSICAL_STATS(PUBLIC.T1, 50)            
------------------- -----------------------------------------------
G1N1                Page: 992, Used: 2591000, Fragmented: 1120000  
G1N2                Page: 992, Used: 2290444, Fragmented: 990080   
G2N1                Page: 2912, Used: 7120068, Fragmented: 3077760 
G2N2                Page: 2912, Used: 7405078, Fragmented: 3200960 
G3N1                Page: 5760, Used: 15095166, Fragmented: 6525120
G3N2                Page: 5760, Used: 14494054, Fragmented: 6265280
6 rows selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(PUBLIC.T1, 50)
        FROM GLOBAL_DUAL@G1N1|G2N1|G3N1
      ORDER BY CLUSTER_MEMBER_NAME;
CLUSTER_MEMBER_NAME TABLE_PHYSICAL_STATS(PUBLIC.T1, 50)            
------------------- -----------------------------------------------
G1N1                Page: 992, Used: 2399266, Fragmented: 1037120  
G2N1                Page: 2912, Used: 7353258, Fragmented: 3178560 
G3N1                Page: 5760, Used: 14633968, Fragmented: 6325760
3 rows selected.
```

<a id="768f911404616e1b"></a>
## TAN

<a id="5e0c05bf8365512f"></a>
### Syntax

```
TAN( num )
```

<a id="479cd03e738dec1b"></a>
### Description

It returns the tangent value of num in radians.  
If num is NULL, the result will also be NULL.

<a id="ca0ac0aeebf3d691"></a>
### Example

```
gSQL> SELECT TAN( 1 ) AS RESULT FROM DUAL;
         RESULT
---------------
1.5574077246549
1 row selected.
```

<a id="3044e7537d8a1aaf"></a>
## TO_BASE64

<a id="359a0644dd4e0c6b"></a>
### Syntax

```
TO_BASE64( str )
```

<a id="982c3ddc370ce47c"></a>
### Description

It converts str using base64 encoding and returns the converted value.  
The str argument can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, a type convertible to a character type, or a binary type such as BINARY, BINARY VARYING, or BINARY LONG VARYING.  
The result type is a character type, such as CHARACTER VARYING or CHARACTER LONG VARYING.

If str is NULL, the result will also be NULL.

Base64 encoding represents 8-bit binary data using 64 characters from the ascii character set.  
These 64 characters consist of  A~Z, a~z, 0~9, +, and /.

Each 6 bits are represented by a single character, and every three characters (24 bits) are represented by four characters as a unit.  
If the encoded output does not fill 4 characters, the remaining space is filled with '='.  
If the encoded string exceeds 76 characters, a newline is added, and it is split into multiple lines.

Use the FROM_BASE64() function to decode a base64-encoded string.  
Newlines, carriage returns, tabs, and spaces are ignored during base64 decoding.

For more information, refer to [FROM_BASE64](#0d50a7fd97d90202).

<a id="39d619ca93044af8"></a>
### Example

```
gSQL> SELECT TO_BASE64( 'abc' ), TO_BASE64( 'abcd' ) FROM DUAL;

TO_BASE64( 'abc' ) TO_BASE64( 'abcd' )
------------------ -------------------
YWJj               YWJjZA==           
1 row selected.
```

<a id="5f3a74b3e90ec4f6"></a>
## TO_CHAR( datetime )

<a id="94eb2a55176eefc0"></a>
### Syntax

```
TO_CHAR( datetime [, fmt ] )
```

<a id="2593f0326c67d528"></a>
### Description

It converts the datetime to a string in the specified fmt format and returns the result.

The datetime argument can be of a data type such as DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, or INTERVAL.   
The fmt argument can be a character data type, such as CHARACTER or CHARACTER VARYING.  
If any argument is NULL, the result will also be NULL.

If fmt is omitted, the default format is used.  
• DATE: Refer to [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#86120b98fe0558e4).  
• TIMESTAMP: Refer to [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#5129c923d9116f8d).  
• TIMESTAMP WITH TIME ZONE: Refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#8a228be667cdaef8).  
• TIME: Refer to [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#b303d4bd630c0388).  
• TIME WITH TIME ZONE: Refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#81aefd62dd9e1a5a).

If the data type of the datetime argument is INTERVAL, it is converted to a string and returned, regardless of the fmt argument.

For more information about the strings that can be specified in fmt, refer to the [Datetime Format String](11-sql-elements.md#c0861393ec3cf3cf).

The result type is CHARACTER VARYING.

<a id="770cf11e8ec40612"></a>
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

<a id="06e9d7b88a3c7d10"></a>
## TO_CHAR( number )

<a id="abb2b19c24d1d0c4"></a>
### Syntax

```
TO_CHAR( number [, fmt ] )
```

<a id="d71ece35544328be"></a>
### Description

It converts the number to a string in the specified fmt format and returns the result.

The number argument can be of a numeric data type.  
The fmt argument can be of a character data type, such as CHARACTER or CHARACTER VARYING.  
If fmt is omitted, all significant digits are converted to a string and returned.  
For more information about the strings that can be specified in fmt, refer to the [Number Format String](11-sql-elements.md#8dde7bcd7362fc93).  
If any input argument is NULL, the result will also be NULL.

The result type is CHARACTER VARYING.

<a id="d895fab5ff326b50"></a>
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

<a id="74b46ad0bc9dbb10"></a>
## TO_DATE

<a id="2d985372d2f68057"></a>
### Syntax

```
TO_DATE( str [, fmt ] )
```

<a id="2d8ad48437df70c2"></a>
### Description

It converts the string str in the specified fmt format to the DATE type and returns the result.

The str and fmt arguments can be of a character data type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.  
If fmt is omitted, the default format is NLS_DATE_FORMAT, and in this case, str must match the default format string.

For more information about the string that can be specified in fmt, refer to the [Datetime Format String](11-sql-elements.md#c0861393ec3cf3cf).  
For more information, refer to [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#86120b98fe0558e4).  

If either str or fmt is NULL, the result will also be NULL.

The result type is DATE.

<a id="df6ce778fc6f0817"></a>
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

<a id="a0f4163ceae2b2da"></a>
## TO_NATIVE_BIGINT

<a id="de8f5507574e902c"></a>
### Syntax

```
TO_NATIVE_BIGINT( str [, fmt ] )
```

<a id="d1ef79f4e548d9d4"></a>
### Description

It converts the string str in the specified fmt format to the NATIVE_BIGINT type and returns the result.

The str and fmt arguments can be of a character data type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

If either str or fmt is NULL, the result will also be NULL.    
For more information about the strings that can be specified in fmt, refer to the [Number Format String](11-sql-elements.md#8dde7bcd7362fc93).

The result type is NATIVE_BIGINT.

<a id="566e136fe9d384a1"></a>
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

<a id="37b2e9541ce0eb78"></a>
## TO_NATIVE_DOUBLE

<a id="27158dbeca68bfa2"></a>
### Syntax

```
TO_NATIVE_DOUBLE( str [, fmt ] )
```

<a id="f9812e03804fbc96"></a>
### Description

It converts the string str in the specified fmt format to the NATIVE_DOUBLE type and returns the result.

The str and fmt arguments can be of a character data type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

If either the str or fmt is NULL, the result will also be NULL.  
For more information about the string that can be specified in fmt, refer to the [Number Format String](11-sql-elements.md#8dde7bcd7362fc93).

The result type is NATIVE_DOUBLE.

<a id="fd3ff07d633bd789"></a>
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

<a id="b7ba82a1d907f3c6"></a>
## TO_NATIVE_INTEGER

<a id="adfaf5c9c71d9a63"></a>
### Syntax

```
TO_NATIVE_INTEGER( str [, fmt ] )
```

<a id="18dec5364f3fb7ed"></a>
### Description

It converts the string str in the specified fmt format to the NATIVE_INTEGER type and returns the result.

The str and fmt arguments can be of a character data type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

If either the str or fmt is NULL, the result will also be NULL.  
For more information about the string that can be specified in fmt, refer to the [Number Format String](11-sql-elements.md#8dde7bcd7362fc93).

The result type is NATIVE_INTEGER.

<a id="7f3178107bce9710"></a>
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

<a id="d1401c04ea742970"></a>
## TO_NATIVE_REAL

<a id="44c654ed99db6091"></a>
### Syntax

```
TO_NATIVE_REAL( str [, fmt ] )
```

<a id="d681b0f30a4fec01"></a>
### Description

It converts the string str in the specified fmt format to the NATIVE_REAL type and returns the result.

The str and fmt arguments can be of a character data type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

If either the str or fmt is NULL, the result will also be NULL.  
For more information about the string that can be specified in fmt, refer to the [Number Format String](11-sql-elements.md#8dde7bcd7362fc93).

The result type is NATIVE_REAL.

<a id="c44cf9fe5153b611"></a>
### Example

```
gSQL> SELECT TO_NATIVE_REAL( '123.45' ) AS RESULT1, 
             TO_NATIVE_REAL( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
```

<a id="194e111618562fc9"></a>
## TO_NATIVE_SMALLINT

<a id="f60e2fc008121d4d"></a>
### Syntax

```
TO_NATIVE_SMALLINT( str [, fmt ] )
```

<a id="ba01ab7d42508990"></a>
### Description

It converts the string str in the specified fmt format to the NATIVE_SMALLINT type and returns the result.

The str and fmt arguments can be of a character data type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

If either the str or fmt is NULL, the result will also be NULL.  
For more information about the string that can be specified in fmt, refer to the [Number Format String](11-sql-elements.md#8dde7bcd7362fc93).

The result type is NATIVE_SMALLINT.

<a id="f281fa8f910ec067"></a>
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

<a id="a547796f56907926"></a>
## TO_NUMBER

<a id="dd01271fd11831f2"></a>
### Syntax

```
TO_NUMBER( str [, fmt] )
```

<a id="43ac07f668147dda"></a>
### Description

It converts the string str in the specified fmt format to the NUMBER type and returns the result.

The str and fmt arguments can be of a character data type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

If either the str or fmt is NULL, the result will also be NULL.  
For more information about the string that can be specified in fmt, refer to the [Number Format String](11-sql-elements.md#8dde7bcd7362fc93).

The result type is NUMBER.

<a id="862478d6815e219a"></a>
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

<a id="369e424a6a243c31"></a>
## TO_TIME

<a id="3e98510ddc74bfab"></a>
### Syntax

```
TO_TIME( str [, fmt ] )
```

<a id="ce2aee9110600495"></a>
### Description

It converts the string str in the specified fmt format to the TIME type and returns the result.

The str and fmt arguments can be of a character data type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIME_FORMAT, and in this case, str must match the default format string.

For more information about the string that can be specified in fmt, refer to the [Datetime Format String](11-sql-elements.md#c0861393ec3cf3cf).  
For more information, refer to [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#b303d4bd630c0388).  

If either str or fmt is NULL, the result will also be NULL.

The result type is TIME.

<a id="bc9242f87f38c3b3"></a>
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

<a id="3d8ed12ebeef772c"></a>
## TO_TIME_TZ

<a id="352a67b447eb0475"></a>
### Syntax

```
TO_TIME_TZ( str [, fmt ] )
```

<a id="e069a22293821d88"></a>
### Description

It is an alias of [TO_TIME_WITH_TIME_ZONE](#7d0b935c0acaee3f).  
For more information, refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#81aefd62dd9e1a5a).

<a id="979a754394167c0c"></a>
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

<a id="7d0b935c0acaee3f"></a>
## TO_TIME_WITH_TIME_ZONE

<a id="d0c25c75f2318395"></a>
### Syntax

```
TO_TIME_WITH_TIME_ZONE( str [, fmt ] )
TO_TIME_TZ( str [, fmt ] )
```

<a id="be3018885b5dd92a"></a>
### Description

It converts the string str in the specified fmt format to the TIME WITH TIME ZONE type and returns the result.

The str and fmt arguments can be of a character data type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIME_WITH_TIME_ZONE_FORMAT, and in this case, str must match the default format string.

For more information about the string that can be specified in fmt, refer to the [Datetime Format String](11-sql-elements.md#c0861393ec3cf3cf)  
For more information, refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#81aefd62dd9e1a5a).  

If either str or fmt is NULL, the result will also be NULL.

It is an alias of [TO_TIME_TZ](#3d8ed12ebeef772c).

The result type is TIME WITH TIME ZONE.

<a id="d73e70a67a5bed99"></a>
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

<a id="b03348c605444fea"></a>
## TO_TIMESTAMP

<a id="b31307b746a288f5"></a>
### Syntax

```
TO_TIMESTAMP( str [, fmt ] )
```

<a id="dadc5fee899a9c17"></a>
### Description

It converts the string str in the specified fmt format to the TIMESTAMP type and returns the result.

The str and fmt arguments can be of a character data type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIMESTAMP_FORMAT, and in this case, str must be the default format string.

For more information about the string that can be specified in fmt, refer to the [Datetime Format String](11-sql-elements.md#c0861393ec3cf3cf).  
For more information, refer to [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#5129c923d9116f8d).  

If either str or fmt is NULL, the result will also be NULL.

The result type is TIMESTAMP.

<a id="28e7510a850995f6"></a>
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

<a id="83872faa8a33c95f"></a>
## TO_TIMESTAMP_TZ

<a id="e1ac8abcd34ff981"></a>
### Syntax

```
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="b7624f3da8ff8aa2"></a>
### Description

It is an alias of [TO_TIMESTAMP_WITH_TIME_ZONE](#785d71b6e8e5c13b).  
For more information, refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#8a228be667cdaef8).

<a id="fec1ccf43c3cac6e"></a>
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

<a id="785d71b6e8e5c13b"></a>
## TO_TIMESTAMP_WITH_TIME_ZONE

<a id="866994840c095713"></a>
### Syntax

```
TO_TIMESTAMP_WITH_TIME_ZONE( str [, fmt ] )
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="6df9f4ffb3761ae0"></a>
### Description

It converts the string str in the specified fmt format to the TIMESTAMP WITH TIME ZONE type and returns the result.

The str and fmt arguments can be of a character data type, such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT, and in this case, str must match the default format string.

For more information about the string that can be specified in fmt, refer to the  [Datetime Format String](11-sql-elements.md#c0861393ec3cf3cf).  
For more information, refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#8a228be667cdaef8).  

If either str or fmt is NULL, the result will also be NULL.

It is an alias of [TO_TIMESTAMP_TZ](#83872faa8a33c95f).

The result type is TIMESTAMP WITH TIME ZONE .

<a id="cc33257ef827961a"></a>
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

<a id="3334c80c7c712441"></a>
## TRANSACTION_DATE

<a id="b8febe425076ae51"></a>
### Syntax

```
TRANSACTION_DATE()
```

<a id="9fb1d5417469f128"></a>
### Description

It returns the current date (DATE type) value based on the session time.

The differences among the functions for obtaining the current date are as follows.  

• TRANSACTION_DATE(): All date values within the transaction are the same.  
• STATEMENT_DATE(): All date values within an SQL statement are the same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is returned.

<a id="eae994650dd90961"></a>
### Example

All date values are always the same within a single transaction.

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

<a id="ac7edc81a7e0cf69"></a>
## TRANSACTION_LOCALTIME

<a id="40332af04bb0c6c3"></a>
### Syntax

```
TRANSACTION_LOCALTIME()
```

<a id="1952e25a26ce878f"></a>
### Description

It returns the current TIME WITHOUT TIME ZONE value based on the session time.

The differences among the functions for obtaining the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values within the transaction are the same.   
• STATEMENT_LOCALTIME(): All time values within an SQL statement are the same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is returned.

<a id="0d340dc339ca61c8"></a>
### Example

All time values are always the same within a single transaction.

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

<a id="2ce7ed638d065160"></a>
## TRANSACTION_LOCALTIMESTAMP

<a id="9b40727c37670e89"></a>
### Syntax

```
TRANSACTION_LOCALTIMESTAMP()
```

<a id="6159e3870ff2e81e"></a>
### Description

It returns the current TIMESTAMP WITHOUT TIME ZONE value based on the session time.

The differences among the functions for obtaining the current timestamp are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All TIMESTAMP values within the transaction are the same.  
• STATEMENT_LOCALTIMESTAMP(): All TIMESTAMP values within an SQL statement are the same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is returned.

<a id="0c2a43bc0deccdbc"></a>
### Example

All timestamp values are always the same within a single transaction.

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

<a id="2d2fd5c6c8fca6db"></a>
## TRANSACTION_TIME

<a id="000c72069fe6ff7b"></a>
### Syntax

```
TRANSACTION_TIME()
```

<a id="6ec6a1e21730e044"></a>
### Description

It returns the current TIME WITH TIME ZONE value based on the session time.

The differences among the functions for obtaining the current time are as follows.  

• TRANSACTION_TIME(): All time values within the transaction are the same.  
• STATEMENT_TIME(): All time values within an SQL statement are the same.   
• CLOCK_TIME(): Whenever the function is called, the current time value is returned.

<a id="5014e7fa4697c2eb"></a>
### Example

All time values are always the same within a single transaction.

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

<a id="1c814c7a014ca275"></a>
## TRANSACTION_TIMESTAMP

<a id="c9c181019af0f274"></a>
### Syntax

```
TRANSACTION_TIMESTAMP()
```

<a id="4f4cf58002e5f59d"></a>
### Description

It returns the current TIMESTAMP WITH TIME ZONE value based on the session time.

The differences among the functions for obtaining the current timestamp are as follows.  

• TRANSACTION_TIMESTAMP(): All TIMESTAMP values within the transaction are the same.  
• STATEMENT_TIMESTAMP(): All TIMESTAMP values within an SQL statement are the same.   
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is returned.

<a id="308ce63811828c7a"></a>
### Example

All timestamp values are always the same within a single transaction.

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

<a id="0e091ffaeb163a5e"></a>
## TRANSLATE

<a id="1e3457c1c45e6fd7"></a>
### Syntax

```
TRANSLATE( string, from, to )
```

<a id="b84c3d4d171f6a17"></a>
### Description

It replaces characters by substituting each character in the string that matches a character from *from* with the corresponding character from *to* at the same position and returns the result.

The arguments string, from, and to can be of a CHARACTER data type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

If either string, from, or to is NULL, the result will also be NULL.

- If a character in the string matches a character from *from*:
    - If the length of *from* is equal to the length of *to*, the characters in *from* are replaced with the corresponding characters in *to* at the same positions.
    - If the length of *from* is greater than the length of *to*, any characters in *from* beyond the length of *to* will be removed from the string.
    - If *from* consists of duplicate characters, the characters in *from* are replaced with the corresponding characters in *to* at the same positions as the first occurrence of each duplicated character in *from*.
- If no character in the string matches any character from *from*, the string will remain unchanged.

The following table describes the result types.

**Result type of TRANSLATE**

<a id="9559b989b33cdd99"></a>
| string type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="afe6c84d3244e1c4"></a>
### Example

- When a character in the string matches one from the *from* set, it is replaced with the corresponding character from the *to* set at the same position.
    - A → Z, C → Y, E → X, G → W

```
gSQL> SELECT TRANSLATE('ABCDEFG', 'ACEG', 'ZYXW') AS RESULT
FROM DUAL;
RESULT 
-------
ZBYDXFW
1 row selected.
```

- If the length of the *from* string is longer than that of the *to* string, the characters in *from* that are beyond the length of the *to* string are deleted and replaced.
    - A → Z, C → Y, deleting E, deleting G

```
gSQL> SELECT TRANSLATE('ABCDEFG', 'ACEG', 'ZY') AS RESULT
      FROM DUAL;
RESULT
------
ZBYDF 
1 row selected.
```

<a id="57e64d312bc89918"></a>
## TRIM

<a id="350d776ea5e06d13"></a>
### Syntax

```
TRIM([ [ LEADING | TRAILING | BOTH ]  [trim_character] FROM ] trim_source)
```

<a id="3a48da40e4c7741b"></a>
### Description

It removes the matching characters by comparing the trim_character in trim_source from the LEADING, TRAILING, or BOTH directions until no matching character remains. Then, it returns the result.

The trim_character and trim_source arguments can be of a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING or a binary character data type such as BINARY, BINARY VARYING, or BINARY LONG VARYING.

If either trim_character or trim_source is NULL, the result will also be NULL.

- [ LEADING | TRAILING | BOTH ]
    - LEADING: Removes trim_character from the beginning of trim_source.
    - TRAILING: Removes trim_character from the end of trim_source.
    - BOTH: Removes trim_character from both the beginning and the end of trim_source.
- trim_character must be a single character.
- If trim_character is omitted, a single blank space (' ') is specified by default.
- When FROM is specified
    - [ LEADING | TRAILING | BOTH ], trim_character or [ LEADING | TRAILING | BOTH ] trim_character must be specified.
        - e.g., TRIM( LEADING FROM ' abc' ) , TRIM( 'x' FROM 'xabc' ) , TRIM( LEADING 'x' FROM 'xabc' )
    - If [ LEADING | TRAILING | BOTH ] is omitted, BOTH is specified by default.
- When FROM is omitted.
    - It is TRIM(trim_source), which behaves the same as TRIM(BOTH ' ' FROM trim_source).

The following table describes the result types.

**Result type of TRIM**

<a id="2bb7989581f1b22f"></a>
| trim_character, trim_source type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="9c35d7952eabd96c"></a>
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

<a id="2eadbb656d48170b"></a>
## TRUNC( number )

<a id="ea4d0e42d6a314df"></a>
### Syntax

```
TRUNC( num [ , scale ] )
```

<a id="7f73a6a1236bbcaa"></a>
### Description

It truncates the num based on the scale and then returns the result.

The num and scale arguments can be of a numeric type.  
If either the num or scale argument is NULL, the result will also be NULL.

If scale is omitted, it defaults to 0 and is executed as TRUNC(num, 0).  
If scale is positive, the number is truncated based on the digits to the right of the decimal point.  
If scale is negative, the number is truncated based on the digits to the left of the decimal point.

<a id="60837c50f5fd2d84"></a>
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

<a id="fbbc89be20785aea"></a>
## TRUNC( date )

<a id="da27606690aa57f1"></a>
### Syntax

```
TRUNC( date [ , fmt ] )
```

<a id="ff41b2de7d8bb6cd"></a>
### Description

It returns the truncated value of the date based on the specified fmt unit.

The date argument can be of the DATE, TIMESTAMP, or TIMESTAMP WITH TIME ZONE data type.  
The fmt argument can be a character data type, such as CHARACTER or CHARACTER VARYING.  
If either the date or fmt argument is NULL, the result will also be NULL.

The result type is always DATE, regardless of the input date type.

If fmt is omitted, the default is *DAY*, and the available format strings are described in the following table.

**Available format strings for fmt**

<a id="f7225d20caf69379"></a>
| Format string | Description |
| --- | --- |
| CC, SCC | Century |
| YYYY, YEAR, SYYYY, SYEAR, YYY, YY, Y | Year |
| IYYY, IYY, IY, I | The year that accommodates the calendar week defined by the ISO 8601 standard. |
| Q | Quarter |
| MONTH, MON, MM, RM | Month |
| WW | The week that starts with January 1st of the year. |
| IW | The first week of the year is the week that contains the first Thursday, according to the calendar week (1–52 or 1–53 weeks) defined by the ISO 8601 standard. |
| W | The week that starts with the 1st day of the month. |
| DDD, DD, J | Day |
| DAY, DY, D | Day of the week |
| HH, HH12, HH24 | Hour |
| MI | Minute |

<a id="a92d272ef1b18818"></a>
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

<a id="6f03606b9029b12d"></a>
## UPPER

<a id="110b568bffbff39f"></a>
### Syntax

```
UPPER( str )
```

<a id="b151b3095363061a"></a>
### Description

It returns the uppercase version of str.

The str argument can be of a character data type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.  
If str is NULL, the result will also be NULL.

The return type is the same as the type of the str argument.

<a id="5ec84498e87552be"></a>
### Example

```
gSQL> SELECT UPPER( 'spring' ) AS RESULT FROM DUAL;
RESULT
------
SPRING
1 row selected.
```

<a id="dc778c3715262f05"></a>
## UNHEX

<a id="dc3d373852ac900b"></a>
### Syntax

```
UNHEX( str )
```

<a id="a25093af2ac4b5b6"></a>
### Description

The str argument is a hexadecimal character, which is represented as individual bytes and returned as a binary string.

The input argument can be of a character type, such as CHARACTER VARYING or CHARACTER LONG VARYING. The result type can be of a binary character type, such as BINARY VARYING or BINARY LONG VARYING.

If str is NULL, the result will also be NULL.  
If str contains a character that is not within the hexadecimal range, an error will be returned.

For more information, refer to [HEX](#86c83702c5f76005).

<a id="3e8e2e63699ecb5e"></a>
### Example

```
gSQL> SELECT UNHEX( HEX( 'abc' ) ) FROM DUAL;
UNHEX( HEX( 'abc' ) )
---------------------
616263               
1 row selected.
```

<a id="188af09b3f6ed341"></a>
## UNHEX_TO_CHARSTR

<a id="495d19c36a07f5f3"></a>
### Syntax

```
UNHEX_TO_CHARSTR( str )
```

<a id="77882827276e17cb"></a>
### Description

The str argument is a hexadecimal character, which is represented as individual bytes and returned as  a character string.

The input argument can be of a character type, such as CHARACTER VARYING or CHARACTER LONG VARYING. The result type can be of a character type, such as CHARACTER VARYING or CHARACTER LONG VARYING.

If str is NULL, the result will also be NULL.  
If str contains a character that is not within the hexadecimal range, an error will be returned.

For more information, refer to [HEX](#86c83702c5f76005), [UNHEX](#dc778c3715262f05).

<a id="37dbbe83e160e143"></a>
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

<a id="58c8f8adf8e35e6d"></a>
## USER_ID

<a id="06d1ba29ce4c63b8"></a>
### Syntax

```
USER_ID ()
```

<a id="7ce23d63216cac31"></a>
### Description

It retrieves the current user's number ID.

> In a cluster system, the value may vary depending on the connected server.  
> It is recommended to use the [CURRENT_USER](#3d2fbc075f3881c1) function to obtain the current username.

<a id="27976d8faee13fd4"></a>
### Example

```
% gsql test test

gSQL> SELECT USER_ID() FROM dual;

USER_ID()
---------
        6

1 row selected.
```

<a id="f1c1aa1a4f1f22e3"></a>
## UUID

<a id="174ecd7ce8824e77"></a>
### Syntax

```
UUID()
```

<a id="adb70d72e74dfc22"></a>
### Description

It generates a Universally Unique Identifier (UUID) and returns it.   
The return type is VARBINARY, consisting of 16 bytes internally.

<a id="0470b346f61b3963"></a>
### Example

```
gSQL> SELECT HEX( UUID() ) FROM DUAL;
HEX( UUID() )                   
--------------------------------
E6F0A5C2387511E8B95259E479C2FD50
1 row selected.
```

<a id="d3d9330ec5d2493a"></a>
## VAR_POP

<a id="f87b52ffbe816946"></a>
### Syntax

```
VAR_POP( expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="919c2c71422dc9a7"></a>
### Description

It is an aggregation function that calculates the population variance of the expr set.   
If the number of expr sets, excluding NULL, is one, it returns 0.

If a FILTER is specified, the aggregation is performed only on the values that satisfy the condition.

The following table describes the argument and result types.

**Argument and result type of VAR_POP**

<a id="c1d22df5cac13fec"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The population variance is the variance of the entire population, and variance is the average of the squared deviations. In other words, it is calculated by subtracting the population average (the average of the entire group) from each data point, squaring the results, summing them up, and dividing by the number of data points in the population.  
> This is used to determine how much each observation deviates from the average.

For more information, refer to [STDDEV_POP](#c40e9f4ed7b6baf7).

<a id="f16417662e2c4a15"></a>
### Example

```
gSQL> SELECT VAR_POP(c1) FROM t1;

VAR_POP(C1)
-----------
     105.76

1 row selected.


gSQL> SELECT VAR_POP(c1) FILTER( WHERE c1 > 0 ) FROM t1;

VAR_POP(C1)
-----------
     105.76

1 row selected.
```

<a id="5de9a2268c5eaa32"></a>
## VAR_POP() OVER

<a id="d29a19cbb4da0cb7"></a>
### Syntax

```
VAR_POP ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="3bdcd9175ef13da7"></a>
### Description

The window function VAR_POP calculates the population variance of expr.   
If the number of expr values, excluding NULL, is one, it returns 0 as the result.

<a id="a395b5146f4f6f49"></a>
### Example

```
gSQL> SELECT product_id, min_price
             , VAR_POP( min_price ) OVER ( ORDER BY product_id ) AS "VAR_POP"
        FROM product_information
       WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE          VAR_POP
---------- --------- ----------------
      1769      null             null
      1770        73                0
      2378       247             7569
      2382       731 77499.5555555556
      3355      null 77499.5555555556

5 rows selected.
```

<a id="fc3eda323e3927d6"></a>
## VAR_SAMP

<a id="17ee3bc26ec28dcd"></a>
### Syntax

```
VAR_SAMP( expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="28a2f2c1b3245ade"></a>
### Description

It is an aggregation function that calculates the sample variance of the expr set.   
If the number of expr sets, excluding NULL, is one, it returns NULL.

If a FILTER is specified, the aggregation is performed only on the values that satisfy the condition.

The following table describes the argument and result types.

**Argument and result type of VAR_SAMP**

<a id="2cd61525529831fb"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> Unlike population variance, which deals with the entire population, sample variance deals with the average and deviations of the extracted sample. In other words, it is calculated by subtracting the sample average from each data point, squaring the results, summing them up, and then dividing by the number of data points in the sample minus 1.   
> This is used to estimate the variance of the population.

For more information, refer to [STDDEV_SAMP](#ede27e56f90e140c).

<a id="7c1cf666da076f95"></a>
### Example

```
gSQL> SELECT VAR_SAMP(c1) FROM t1;

VAR_SAMP(C1)
------------
       132.2

1 row selected.


gSQL> SELECT VAR_SAMP(c1) FILTER( WHERE c1 > 0 ) FROM t1;

VAR_SAMP(C1)
------------
       132.2

1 row selected.
```

<a id="b2b2417aa592ee6c"></a>
## VAR_SAMP() OVER

<a id="cdd6c7387b99b3f9"></a>
### Syntax

```
VAR_SAMP ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="ab4792ed09beb6b2"></a>
### Description

The window function VAR_SAMP calculates the sample variance of expr.   
If the number of expr values, excluding NULL, is one, it returns NULL as the result.

<a id="d489a1c4321394da"></a>
### Example

```
gSQL> SELECT product_id, min_price
             , VAR_SAMP( min_price ) OVER ( ORDER BY product_id ) AS "VAR_SAMP"
        FROM product_information
       WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE         VAR_SAMP
---------- --------- ----------------
      1769      null             null
      1770        73             null
      2378       247            15138
      2382       731 116249.333333333
      3355      null 116249.333333333

5 rows selected.
```

<a id="fa3ad26fea8effe3"></a>
## VARIANCE

<a id="2450df7e48a77af6"></a>
### Syntax

```
VARIANCE( [ ALL | DISTINCT ] expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="86d287e2b3cac96f"></a>
### Description

It is an aggregation function that calculates the variance of the expr set.

If ALL is specified, the function is applied to all values. If DISTINCT is specified, the function is applied to values with duplicates removed. If neither is specified, the function behaves as if ALL were specified.

If, after removing duplicates using DISTINCT, the number of expr sets (excluding NULL) is one, the function returns 0.

If a FILTER is specified, the aggregation is performed only on the values that satisfy the condition.

The following table describes the argument and result types.

**Argument and result type of VARIANCE**

<a id="d314a80c2b60f1be"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> GOLDILOCKS calculates the variance as follows:  
> • If the number of expr sets is 1, it returns 0.  
> • If the number of expr sets is greater than 1, It returns the value of [VAR_SAMP ( expr )](#fc3eda323e3927d6).

<a id="824a2731c8f0511c"></a>
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


gSQL> SELECT VARIANCE(c1) FILTER( WHERE c1 > 0 ) FROM t1;

VARIANCE(C1)
------------
       132.2

1 row selected.
```

<a id="ec280e0f2fdadf65"></a>
## VARIANCE() OVER

<a id="60960ceb9d453f6d"></a>
### Syntax

```
VARIANCE ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

<a id="a93800e4c57e09a8"></a>
### Description

The window function VARIANCE calculates the variance of expr.   
If the number of expr values, excluding NULL, is one, it returns 0 as the result.

<a id="cd54e353279d5211"></a>
### Example

```
gSQL> SELECT product_id, min_price
             , VARIANCE( min_price ) OVER ( ORDER BY product_id ) AS "VARIANCE"
        FROM product_information
       WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE         VARIANCE
---------- --------- ----------------
      1769      null             null
      1770        73                0
      2378       247            15138
      2382       731 116249.333333333
      3355      null 116249.333333333

5 rows selected.
```

<a id="39bf4f4db2bd030c"></a>
## VERSION

<a id="8bfd0cd4ca8f2c5a"></a>
### Syntax

```
VERSION()
```

<a id="72fa93c6a28f0d09"></a>
### Description

It retrieves the product's version string.

<a id="1100e80016a9eced"></a>
### Example

```
gSQL> SELECT VERSION() FROM dual;

VERSION()                            
-------------------------------------
Release Name.X.X.X revision(XXXXX)

1 row selected.
```

<a id="6c5b40e928a7d7a1"></a>
## WIDTH_BUCKET

<a id="70aa5d34ae307704"></a>
### Syntax

```
WIDTH_BUCKET( num, min, max, cnt )
```

<a id="6794a0bd5a3f0576"></a>
### Description

It creates sections with the same width as cnt within the specified min and max range, and returns the position of the section that contains num.

The data types of the num, min, max, and cnt arguments can all be numeric data types.

min, max define the range for the sections. If the min value is equal to the max value, an error is returned.  
cnt represents the number of sections. The cnt must be a positive number. If cnt is 0 or a negative number, an error will be returned.   
The position of the sections is numbered starting from 1.

If any of num, min, max, or cnt is NULL, the result will also be NULL.

<a id="b6e648a615a06cfb"></a>
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
