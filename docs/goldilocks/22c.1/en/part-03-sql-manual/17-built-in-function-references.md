<a id="e991846bb9b72960"></a>

# 17. Built-in Function References

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/e991846bb9b72960)  
> Tag: `22c.1_10_tag`

[← 16. Built-in Data Type References](16-built-in-data-type-references.md) · [Table of contents](../README.md) · [18. SQL References (A~B) →](18-sql-references-a-b.md)

<a id="827484d83904b881"></a>
## * (MULTIPLICATION)

<a id="69efc02365ff8e7d"></a>
### Syntax

```
expr1 * expr2
```

<a id="0057078e8aafda9a"></a>
### Description

It returns the multiplication result of expr1 and expr2.

The multiplication types and result types are as follows.  
For more information, refer to [Type Conversion](11-sql-elements.md#935e2183d0c42aa6).

**Numeric * operation**

<a id="df04b79e76d6d46f"></a>
| expr1 (expr2) | expr2 (expr1) | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="792c98c0f1a6574e"></a>
<table class="table column_count_3"><caption>INTERVAL * operation</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type is the interval type.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type is the interval type.)</div></td></tr><tr><td class="to_left" colspan="3"><div>Refer to <a class="reference text" href="#d0fd17f2cb1c026f">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

**INTERVAL type details which is included in INTERVAL type written in the following table**

<a id="d0fd17f2cb1c026f"></a>
<table><thead><tr><th align="center">INTERVAL YEAR TO MONTH</th><th align="center">INTERVAL DAY TO SECOND</th></tr></thead><tbody><tr><td valign="middle"><ul><li>INTERVAL YEAR</li><li>INTERVAL MONTH</li><li>INTERVAL YEAR TO MONTH</li></ul></td><td valign="middle"><ul><li>INTERVAL DAY</li><li>INTERVAL HOUR</li><li>INTERVAL MINUTE</li><li>INTERVAL SECOND</li><li>INTERVAL DAY TO HOUR</li><li>INTERVAL DAY TO MINUTE</li><li>INTERVAL DAY TO SECOND</li><li>INTERVAL HOUR TO MINUTE</li><li>INTERVAL HOUR TO SECOND</li><li>INTERVAL MINUTE TO SECOND</li></ul></td></tr></tbody></table>

<a id="cea124934466f54c"></a>
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

<a id="2b173b26816d57c1"></a>
## + (ADDITION)

<a id="718f6f7ec34f2eed"></a>
### Syntax

```
expr1 + expr2
```

<a id="bd9d8f4392fc12b2"></a>
### Description

It returns the addition result of expr1 and expr2.

The addition types and result types are as follows.  
For more information, refer to [Type Conversion](11-sql-elements.md#935e2183d0c42aa6).

**Numeric + operation**

<a id="151f61ac744aef6a"></a>
| expr1 (expr2) | expr2 (expr1) | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="4aeccb6a99722cf6"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) + operation</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference text" href="#d0fd17f2cb1c026f">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="71be442271f05c0f"></a>
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

<a id="0ad5e2857b9bf32a"></a>
## + (POSITIVE)

<a id="45952277ea3f345b"></a>
### Syntax

```
+ expr
```

<a id="745f75cd808eddf3"></a>
### Description

The + sign is displayed in expr.

<a id="3810b5f27bd539e2"></a>
### Example

```
gSQL> SELECT +3 AS RESULT1, +(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      3      -3
1 row selected.
```

<a id="feb96ef9f9abe06f"></a>
## - (NEGATIVE)

<a id="3b01510cff8dece9"></a>
### Syntax

```
- expr
```

<a id="789f49ff826a3f05"></a>
### Description

The - sign is displayed in expr.

<a id="051229dd9aede0a6"></a>
### Example

```
gSQL> SELECT -3 AS RESULT1, -(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     -3       3
1 row selected.
```

<a id="ccd72d1a1fab918e"></a>
## - (SUBTRACTION)

<a id="4c010797bcbe0565"></a>
### Syntax

```
expr1 - expr2
```

<a id="e93250ff8aa9d227"></a>
### Description

It returns the subtraction result of expr1 and expr2.

The subtraction types and result types are as follows.  
For more information, refer to [Type Conversion](11-sql-elements.md#935e2183d0c42aa6).

**Numeric - operation**

<a id="ea76c546526ae979"></a>
| expr1 | expr2 | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="9bd17806054e7bbd"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) - operation</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMBER</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference text" href="#d0fd17f2cb1c026f">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="4da7a1dd63e06a1f"></a>
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

<a id="7144049f41367f01"></a>
## / (DIVISION)

<a id="364d645d3549578c"></a>
### Syntax

```
expr1 / expr2
```

<a id="ef2dd3a015614e16"></a>
### Description

It returns the division result of expr1 and expr2.

The division types and result types are as follows.  
For more information, refer to [Type Conversion](11-sql-elements.md#935e2183d0c42aa6).

**Numeric / operation**

<a id="f9291d149bfab403"></a>
| expr1 | expr2 | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER | NUMBER |
| NATIVE_DOUBLE | NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="9414c15afdba6dff"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) / operation</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type is interval type.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type is interval type.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference text" href="#d0fd17f2cb1c026f">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="9b67bd30227cd5f5"></a>
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

<a id="3274505dd6136d12"></a>
## || (CONCATENATE)

<a id="589b16a819da2cf7"></a>
### Syntax

```
str1 || str2
```

<a id="df7e3d91e23121da"></a>
### Description

CONCATENATE returns the string concatenating str1 and str2.

If either str1 or str2 is NULL, the string except NULL is returned. If both of str1 and str2 are NULL, NULL is returned.

The argument can be a type which can be converted to either character string type or binary string type.  
For more information, refer to [Type Conversion](11-sql-elements.md#935e2183d0c42aa6).

It is an alias of [CONCAT](#0fb0770183ef9ff9), [CONCATENATE](#2b2d8c3da5454602).

The result types are as follows.

**The result types of || (CONCATENATE)**

<a id="00a8b548f2b788ec"></a>
| Data type | CHAR | VARCHAR | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR | CHAR | VARCHAR | LONG VARCHAR |
| VARCHAR | VARCHAR | VARCHAR | LONG VARCHAR |
| LONG VARCHAR | LONG VARCHAR | LONG VARCHAR | LONG VARCHAR |
| Data type | BINARY | VARBINARY | LONG VARBINARY |
| BINARY | BINARY | VARBINARY | LONG VARBINARY |
| VARBINARY | VARBINARY | VARBINARY | LONG VARBINARY |
| LONG VARBINARY | LONG VARBINARY | LONG VARBINARY | LONG VARBINARY |

<a id="22b5d38b9bd32e19"></a>
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

<a id="8d66550ee768794c"></a>
## ABS

<a id="5cef7bd7fe729362"></a>
### Syntax

```
ABS( num )
```

<a id="2c4ebd7b7ad9dad7"></a>
### Description

ABS returns the absolute value of num.

The num argument can be a numeric type or types which can be converted to number.  
If num is NULL, then it returns NULL.

<a id="088d0acc75c5ea5d"></a>
### Example

```
gSQL> SELECT ABS(-1) AS RESULT1, ABS(1) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1       1
1 row selected.
```

<a id="76e5689696dd8c07"></a>
## ACOS

<a id="ffcc9d59b87531c7"></a>
### Syntax

```
ACOS( num )
```

<a id="f573022a42a1c812"></a>
### Description

ACOS returns the arc cosine value of num.  

The num argument should be in the range of -1 to 1.   
If num is NULL, then it returns NULL.  

It returns the radians value in the range of 0 and pi.

<a id="2fc0a380768206bb"></a>
### Example

```
gSQL> SELECT ACOS( 1 ) FROM DUAL;
ACOS( 1 )
---------
        0
1 row selected.
```

<a id="927624817574e79b"></a>
## ADDDATE

<a id="8380eee2c0a75564"></a>
### Syntax

```
ADDDATE( date, INTERVAL expr unit  )
ADDDATE( expr, days )
```

<a id="78c5230a35e05fba"></a>
### Description

ADDDATE adds the second argument to the first argument, then returns the result.  

If any of the input argument value is NULL, the result is also NULL.  
The first argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, and the second argument data type can be INTERVAL or numeric.

The result type is as same as [(DATETIME/INTERVAL) + operation](#4aeccb6a99722cf6).

<a id="796b8c896c12a5e3"></a>
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

<a id="3a34762e4fa8c807"></a>
## ADDTIME

<a id="89eabaf2894ab857"></a>
### Syntax

```
ADDTIME( expr1, expr2 )
```

<a id="e2265925a52f638b"></a>
### Description

ADDTIME adds expr2 to expr1, then returns the result.

expr1 data type can be TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE TYPE, and expr2 data type can be INTERVAL DAY TO SECOND TYPE.  

If expr1 or expr2 is NULL, the result is NULL.

The result type is as same as [(DATETIME/INTERVAL) + operation](#4aeccb6a99722cf6).

<a id="691125fe5581f2be"></a>
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

<a id="4078b2e3840b6cf6"></a>
## ADD_MONTHS

<a id="57ad9a90885baac1"></a>
### Syntax

```
ADD_MONTHS( date, number )
```

<a id="2af690130c88d286"></a>
### Description

ADD_MONTHS adds as many month as the number to the date, then returns the result.  
After ADD_MONTHS operation, if the date is bigger than the last day of the month, it is adjusted to the last day of the month.

The data type of date argument can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, and the number argument can be a numeric type.  
If any of the input argument is NULL, the result is also NULL.

The result type is always DATE regardless of the input argument date type.

<a id="85efe5b0242081b9"></a>
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

<a id="2258ae3f25cf26a4"></a>
## ASCII

<a id="bf6dd3026a7a876a"></a>
### Syntax

```
ASCII( char )
```

<a id="957363a56359aff0"></a>
### Description

It returns the database character set code of the first character of char in decimal form.  

The data type of char can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING or can be a type which can be converted to a character type, and the return type is NUMBER.  
If char is NULL, then it returns NULL.

<a id="4ad0ae33062548d2"></a>
### Example

```
gSQL> SELECT ASCII( 'G' ) AS RESULT FROM DUAL;
RESULT
------
    71
1 row selected.
```

<a id="8ba6d7d603750dca"></a>
## ASIN

<a id="92db4556aa1588b8"></a>
### Syntax

```
ASIN( num )
```

<a id="76c2c21e6b556839"></a>
### Description

ASIN returns the arc sin value of num.

The num argument should be in the range of -1 to 1.  
If num is NULL, then it returns NULL.

It returns the radians value in the range of -pi/2 and pi/2.

<a id="33c24a085ab3e19d"></a>
### Example

```
gSQL> SELECT ASIN( 0 ) FROM DUAL;
ASIN( 0 )
---------
        0
1 row selected.
```

<a id="634cd71621ac85aa"></a>
## ATAN

<a id="e2d037d87f869155"></a>
### Syntax

```
ATAN( num )
```

<a id="2c5f848040c8ed89"></a>
### Description

ATAN returns the arc tangent value of num.

The num value range is not limited. It returns the radians value in the range of -pi/2 and pi/2.  
If num is NULL, then it returns NULL.

<a id="6bd436831d85dd0d"></a>
### Example

```
gSQL> SELECT ATAN(0.5) FROM DUAL;
       ATAN(0.5)
----------------
.463647609000806
1 row selected.
```

<a id="8cca65d5dd5349a8"></a>
## ATAN2

<a id="c84bcbe43b7739ff"></a>
### Syntax

```
ATAN2( num1, num2 )
```

<a id="77d2bf9d0d6be739"></a>
### Description

ATAN2 returns the arc tangent value of num1 and num2.

The num1 argument value range is not limited. It returns the radians value in the range of -pi and pi.  
Either num1 or num2 is NULL, then it returns NULL.

<a id="cece178e06a3a69b"></a>
### Example

```
gSQL> SELECT ATAN2(1,2) FROM DUAL; 
      ATAN2(1,2)
----------------
.463647609000806
1 row selected.
```

<a id="1650d73d263c108c"></a>
## AVG

<a id="004cfcf2701b968f"></a>
### Syntax

```
AVG( [ ALL | DISTINCT ] num )
```

<a id="686595d0d95afdeb"></a>
### Description

It is an aggregate function, and it obtains average value of exprs.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

<a id="77936d3a93393aea"></a>
### Example

```
gSQL> SELECT AVG(c1) FROM t1;

AVG(C1)
-------
      2

1 row selected.
```

<a id="692d399e54ef6e8c"></a>
## AVG() OVER

<a id="239e3e2b240fddce"></a>
### Syntax

```
AVG ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="29903e94977c0e78"></a>
### Description

Window function AVG calculates the average value of expr.  
NULL is excluded from the calculation.

<a id="d0289e2f9da0dbdb"></a>
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

<a id="83cc3df86bdca709"></a>
## BITAND

<a id="459a006d2c4b70f7"></a>
### Syntax

```
BITAND( num1, num2 )
```

<a id="cfca96c1c918b345"></a>
### Description

It returns the AND operation result for the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT or a data type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.  
If any of the input argument value is NULL, the result is also NULL.

The result type is NATIVE_BIGINT.

<a id="74c253b4df9f8437"></a>
### Example

```
gSQL> SELECT BITAND( 5, 3 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="55802fa58df7e2d1"></a>
## BITNOT

<a id="d75d1f1295c1ae97"></a>
### Syntax

```
BITNOT( num )
```

<a id="d13e205b64d20c5b"></a>
### Description

It returns the NOT operation result for the num bit.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT or a data type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.  
If the input argument is NULL, the result is also NULL.

The result type is as follows.  
• If the input argument is NATIVE_SMALLINT type, its result type is NATIVE_SMALLINT type.  
• If the input argument is NATIVE_INTEGER type, its result type is NATIVE_INTEGER type.  
• If the input argument is NATIVE_BIGINT type, its result type is NATIVE_BIGINT type.

<a id="c4adc3f3fd034a6d"></a>
### Example

```
gSQL> SELECT BITNOT( 5 ) AS RESULT FROM DUAL;
RESULT
------
    -6
1 row selected.
```

<a id="470026b2b34b56c1"></a>
## BITOR

<a id="a1beea4e0f6a2650"></a>
### Syntax

```
BITOR( num1, num2 )
```

<a id="875d14e2931b455c"></a>
### Description

It returns the OR operation result for the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT types or a data type which can be converted to NATIVE_BIGINT type.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.  
If any of the input argument value is NULL, the result is NULL.

The result type is NATIVE_BIGINT type.

<a id="edab49685d675ccc"></a>
### Example

```
gSQL> SELECT BITOR( 5, 3 ) FROM DUAL;

BITOR( 5, 3 )
-------------
            7
1 row selected.
```

<a id="79ca9cf7ca575a45"></a>
## BITXOR

<a id="49149691b180b9ff"></a>
### Syntax

```
BITXOR( num1, num2 )
```

<a id="030ac554316944a7"></a>
### Description

It returns the XOR operation result for the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT or a data type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.  
If any of the input argument value is NULL, the result is NULL.

The result type is NATIVE_BIGINT.

<a id="9e613d2118077a17"></a>
### Example

```
gSQL> SELECT BITXOR( 5, 3 ) FROM DUAL;
BITXOR( 5, 3 )
--------------
             6
1 row selected.
```

<a id="61bd92563542bb9a"></a>
## BIT_LENGTH

<a id="e37e34b961d079a3"></a>
### Syntax

```
BIT_LENGTH( str )
```

<a id="76125339ef480a24"></a>
### Description

BIT_LENGTH returns the number of bits for str.  
If str is NULL, then it returns NULL.

<a id="34f1e23fe2f88094"></a>
### Example

```
gSQL> SELECT BIT_LENGTH( 'LIKE' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
             32
    1 row selected.
```

<a id="076781007f6d69e0"></a>
## BYTE_LENGTH

<a id="13c45aa49928e214"></a>
### Syntax

```
BYTE_LENGTH( str )
```

<a id="e1beb7ccaf8268f7"></a>
### Description

It is an alias of OCTET_LENGTH.  
For more information, refer to [OCTET_LENGTH](#67879be1522706a0), [LENGTHB](#47f3cf241a8776e8).

<a id="02c42279531ca242"></a>
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

<a id="59eec3a092621013"></a>
## CASE2

<a id="2490087e239b4236"></a>
### Syntax

```
CASE2( condition1, result1
      [, condition2, result2
       , ...
       , conditionN, resultN ]
      [, default ] )
```

<a id="fce1c9f646b4a6c4"></a>
### Description

CASE2 evaluates the condition in the described order.  
If the comparison result is FALSE, it continues evaluating until TRUE comes up.  
If the comparison result is TRUE, it returns the corresponding result, and does not evaluate any more.  
If all the comparison results are FALSE, it returns the default value. If the default is omitted, it returns NULL.

If multiple types are used in result, then the result type is determined according to [Result Type Combination Rule](11-sql-elements.md#9a5dc6c72b766b73).

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

<a id="5dfd61403ccd61b2"></a>
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

<a id="fae5e1eced2d11ae"></a>
## CBRT

<a id="bb32f6bdfec2002e"></a>
### Syntax

```
CBRT( num )
```

<a id="941db2c44117d080"></a>
### Description

It returns the cube root of num.  
If num is NULL, the result is also NULL.

<a id="368ea5a7b5932e40"></a>
### Example

```
gSQL> SELECT CBRT( 27 ) FROM DUAL;
CBRT( 27 )
----------
         3
1 row selected.
```

<a id="c8ec8bc78684cdab"></a>
## CEIL

<a id="e8e3963e548473b2"></a>
### Syntax

```
CEIL( num )
CEILING( num )
```

<a id="c9d1f979f6d4f952"></a>
### Description

CEIL returns the smallest integer which is equal to or bigger than num.  
If num is NULL, then it returns NULL.

<a id="c73f03d6fae9c5c6"></a>
### Example

```
gSQL> SELECT CEIL( 3.5 ) AS RESULT1, CEIL( -3.5 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      4      -3
1 row selected.
```

<a id="a1c40efd346b484f"></a>
## CHAR_LENGTH

<a id="3558a32bea43833f"></a>
### Syntax

```
CHAR_LENGTH( str )            
CHARACTER_LENGTH( str )
```

<a id="15251cd57339e481"></a>
### Description

CHAR_LENGTH returns the number of character for str according to the character set.

The str can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or it can be a data type which can be converted to character type. The return type is NATIVE_BIGINT.

If the data type of str is CHARACTER, the trailing blanks are included in the calculation.  
If str is NULL, it returns NULL.

It is an alias of [LENGTH](#0429eb6207fb17d4).

<a id="6d7d32126aa0597c"></a>
### Example

Multi byte character set: (e.g. UTF8)

```
gSQL> SELECT CHAR_LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="6b1af6a08a64f12c"></a>
## CHR

<a id="cf0619cc513ee284"></a>
### Syntax

```
CHR( num )
```

<a id="771a2ff62175c5c6"></a>
### Description

It returns a character in the database character set code corresponding to num.

num is a numeric type.  
If num is NULL, then it returns NULL.  

The return type is VARCHAR.

<a id="1c0582ec658a7c36"></a>
### Example

```
gSQL> SELECT CHR(71) FROM DUAL;
CHR(71)
-------
G      
1 row selected.
```

<a id="0d949b2a5285a138"></a>
## CLOCK_DATE

<a id="fa087635d99e8bae"></a>
### Syntax

```
CLOCK_DATE()
```

<a id="745eb5a05af46df6"></a>
### Description

Whenever the CLOCK_DATE function is called, the current date (DATE type) value is obtained.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="3c10c4abbb1b4a2f"></a>
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

<a id="c6e7f72490b40439"></a>
## CLOCK_LOCALTIME

<a id="21d7e849c4fcc24c"></a>
### Syntax

```
CLOCK_LOCALTIME()
```

<a id="12f137664688ec1c"></a>
### Description

Whenever the CLOCK_LOCALTIME function is called, the current time value without TIME ZONE (TIME WITHOUT TIME ZONE type) is obtained.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.  
• STATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="7c27c127afac2519"></a>
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

<a id="5d29175d1ef4d164"></a>
## CLOCK_LOCALTIMESTAMP

<a id="0e9f559283fc1653"></a>
### Syntax

```
CLOCK_LOCALTIMESTAMP()
```

<a id="d2c2574ee360df46"></a>
### Description

Whenever the CLOCK_LOCALTIMESTAMP() function is called, the current TIMESTAMP value without TIME ZONE (TIMESTAMP WITHOUT TIME ZONE type) is obtained.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• STATEMENT_LOCALTIMESTAMP(): All TIMESTAMP values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="1e234e79efa55ae2"></a>
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

<a id="5c735218d2a5d1cc"></a>
## CLOCK_TIME

<a id="50389a0fdba06937"></a>
### Syntax

```
CLOCK_TIME()
```

<a id="88dfaca7062e9482"></a>
### Description

Whenever the CLOCK_TIME() function is called, the current time value with TIME ZONE (TIME WITH TIME ZONE type) is obtained.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• STATEMENT_TIME(): All time values in an SQL statement are same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="337766174699fb23"></a>
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

<a id="e794d20dbda51ce2"></a>
## CLOCK_TIMESTAMP

<a id="93d70bbe6538933e"></a>
### Syntax

```
CLOCK_TIMESTAMP()
```

<a id="7b2491dae0bc9abd"></a>
### Description

Whenever CLOCK_TIMESTAMP() function is called, the current TIMESTAMP value with TIME ZONE (TIMESTAMP WITH TIME ZONE type) is obtained.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_TIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• STATEMENT_TIMESTAMP(): All TIMESTAMP values in an SQL statement are same.   
• CLOCK_TIMESTAMP(): Whenever the function is called, the current TIMESTAMP value is obtained.

<a id="441f2183c78cc503"></a>
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

<a id="9721055bac9c198a"></a>
## COALESCE

<a id="8a3737fa62577cc7"></a>
### Syntax

```
COALESCE( expr1, ..., exprN )
```

<a id="3abf7520abf68922"></a>
### Description

It returns the first non null expr in the expr list.  
If all expr in the expr list are null, it returns null.  
In the expr list, there should be two or more expr.

If multiple types are in the expr list, the result type is determined by the [Result Type Combination Rule](11-sql-elements.md#9a5dc6c72b766b73).

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

<a id="e4a06347a6ecb233"></a>
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

<a id="0fb0770183ef9ff9"></a>
## CONCAT

<a id="ddd75dde3ff37260"></a>
### Syntax

```
CONCAT( str1, str2, ... )
```

<a id="c4af33751e19f9b4"></a>
### Description

It is an alias of || ( CONCATENATE ).  
It is an argument of CONCAT function and 2 ~ 254 number of CONCATs can be set.  
For more information, refer to [|| (CONCATENATE)](#3274505dd6136d12), [CONCATENATE](#2b2d8c3da5454602).

<a id="ec5949c34741fbe8"></a>
### Example

```
gSQL> SELECT CONCAT( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="2b2d8c3da5454602"></a>
## CONCATENATE

<a id="0529cd1a5545fb65"></a>
### Syntax

```
CONCATENATE( str1, str2, ... )
```

<a id="5321b5d77a652ee8"></a>
### Description

It is an alias of || ( CONCATENATE ).  
It is an argument of CONCATENATE  function and 2 ~ 254 number of CONCATENATEs can be set.  
For more information, refer to [CONCAT](#0fb0770183ef9ff9), [|| (CONCATENATE)](#3274505dd6136d12).

<a id="9c363b2bea241572"></a>
### Example

```
gSQL> SELECT CONCATENATE( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="05b0c5c0b1ca1211"></a>
## CORR() OVER

<a id="e8e0d145ee4b27e2"></a>
### Syntax

```
CORR( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="3df58106ccd8edd9"></a>
### Description

Window function CORR calculates the coefficient of correlation for the pair of exprs.

If expr1 or expr2 is NULL, then it is excluded from the calculation.  
If the number of rows for the pair of exprs is one or less, then it returns NULL as a result.

<a id="d43f7ea1e031b723"></a>
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

<a id="44e107982215212f"></a>
## COS

<a id="75f49ca66f03be5d"></a>
### Syntax

```
COS(num)
```

<a id="1ae564286750f701"></a>
### Description

It returns the COSINE value of num.  
If the num argument is NULL, the result is also NULL.

<a id="83b4e9c97e64160b"></a>
### Example

```
gSQL> SELECT COS( 0 ) FROM DUAL;
COS( 0 )
--------
       1
1 row selected.
```

<a id="70bf5c99a8ec5af4"></a>
## COT

<a id="5ad323a284f8053e"></a>
### Syntax

```
COT(num)
```

<a id="d4244c0e8c4203cd"></a>
### Description

It returns the COTANGENT value of num.  
If the num argument is NULL, the result is also NULL.

<a id="0d09b39b11481e91"></a>
### Example

```
gSQL> SELECT COT( 1 ) FROM DUAL;
        COT( 1 )
----------------
.642092615934331
1 row selected.
```

<a id="359fda9bb485db91"></a>
## COUNT

<a id="71c6439dcc283c04"></a>
### Syntax

```
COUNT( [ ALL | DISTINCT ] expr )
```

<a id="cd4f330dda1d5d10"></a>
### Description

It is an aggregate function. It returns the number of rows whose expr is not NULL.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

<a id="acd66bea09acc837"></a>
### Example

```
gSQL> SELECT COUNT(c1) FROM t1;

COUNT(C1)
---------
        3

1 row selected.
```

<a id="ba1b291cb1104884"></a>
## COUNT() OVER

<a id="c2da0b026234121f"></a>
### Syntax

```
COUNT ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="d431dc6af04171b2"></a>
### Description

Window function COUNT counts the number of rows.   
NULL is excluded from the calculation.

<a id="3d2d6196abcaa6c1"></a>
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

<a id="690facf6ba5fe621"></a>
## COUNT(*)

<a id="71f08729cc38deff"></a>
### Syntax

```
COUNT(*)
```

<a id="aa11f6ce5c6a5f67"></a>
### Description

It is an aggregate function, and the number of rows is obtained.  
It has nothing to do with whether it is NULL or not because an expression is not explicitly specified.

<a id="b8a2e9ea606991cd"></a>
### Example

```
gSQL> SELECT COUNT(*) FROM t1;

COUNT(*)
--------
       4

1 row selected.
```

<a id="9fe1ec2cf19c17bf"></a>
## COUNT(*) OVER

<a id="64419496af75983b"></a>
### Syntax

```
COUNT(*) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="32af512084b271ea"></a>
### Description

Window function COUNT(*) counts the number of rows.  
It does not separately specify an expression, so it is irrelevant whether the value is NULL or not.

<a id="73cea1a3ea57f692"></a>
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

<a id="af6dd5612064fb6a"></a>
## COVAR_POP() OVER

<a id="f80cb75882cf2fae"></a>
### Syntax

```
COVAR_POP( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="9acde7db5a9171af"></a>
### Description

Window function COVAR_POP calculates the population covariance for the pair of exprs.

If expr1 or expr2 is NULL, then it is excluded from the calculation.   
If the number of rows for the pair of exprs is one or less, then it returns 0 as a result.

<a id="418886188691a257"></a>
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

<a id="65c53271a2251f83"></a>
## COVAR_SAMP() OVER

<a id="b51e9f909e104455"></a>
### Syntax

```
COVAR_SAMP( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="a1537008305803ab"></a>
### Description

Window function COVAR_SAMP calculates the sample covariance for the pair of exprs.

If expr1 or expr2 is NULL, then it is excluded from the calculation.   
If the number of rows for the pair of exprs is one or less, then it returns NULL as a result.

<a id="0f5d9140c8394bf4"></a>
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

<a id="d269bdbb3864419a"></a>
## CUME_DIST() OVER

<a id="b484d051a31a28bc"></a>
### Syntax

```
CUME_DIST( ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="50107dfc21221681"></a>
### Description

Window function CUME_DIST calculates the cumulative distribution according to the relative position of the current row's value.

The result of CUME_DIST function is the number between 0 and 1.  
If the row values are same, then it returns the same result which is the biggest cumulative distribution value.

window frame is not available.

<a id="eda73767ad42be1d"></a>
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

<a id="3576503a05e8089a"></a>
## CURRENT_CATALOG

<a id="cabe2d483e38ce22"></a>
### Syntax

```
CURRENT_CATALOG [()]
```

<a id="e73161975550a926"></a>
### Description

The catalog name (database name) is obtained.

<a id="7b9d76a5d4c78707"></a>
### Example

```
gSQL> SELECT CURRENT_CATALOG FROM dual;

CURRENT_CATALOG
---------------
TEST_DB        

1 row selected.
```

<a id="11de16d40aab5ff8"></a>
## CURRENT_DATE

<a id="703a24a096941d09"></a>
### Syntax

```
CURRENT_DATE [()]
STATEMENT_DATE()
```

<a id="0bbc37befb72a111"></a>
### Description

The current date (DATE type) is obtained.

CURRENT_DATE is an SQL standard function.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• CURRENT_DATE, STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="f517add56c796067"></a>
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

<a id="9fd74f8eacd46a81"></a>
## CURRENT_SCHEMA

<a id="685f3b87de4f8ea5"></a>
### Syntax

```
CURRENT_SCHEMA [()]
```

<a id="213f331c5ad5e6f6"></a>
### Description

User's current SCHEMA is obtained.

<a id="36c619095faa230f"></a>
### Example

```
gSQL> SELECT CURRENT_SCHEMA FROM dual;

CURRENT_SCHEMA
--------------
PUBLIC        

1 row selected.
```

<a id="3138931fb3264137"></a>
## CURRENT_TIME

<a id="ab58bc150dbdd3ab"></a>
### Syntax

```
CURRENT_TIME [()]
STATEMENT_TIME()
```

<a id="68083b009502aebf"></a>
### Description

The current TIME WITH TIME ZONE type value based on the session time is obtained.

CURRENT_TIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• CURRENT_TIME, STATEMENT_TIME(): All time values in an SQL statement are same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="f404566f4918eb74"></a>
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

<a id="de1fe20a9404482d"></a>
## CURRENT_TIMESTAMP

<a id="ccf9e9b4c15648cf"></a>
### Syntax

```
CURRENT_TIMESTAMP [()]
STATEMENT_TIMESTAMP()
```

<a id="14fc69da3cdc0796"></a>
### Description

It obtains the TIMESTAMP WITH TIME ZONE type value based on the session time.

CURRENT_TIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_TIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• CURRENT_TIMESTAMP, STATEMENT_TIMESTAM(): All TIMESTAMP values in an SQL statement are same.  
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="d761ad17c4b678d2"></a>
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

<a id="222009ae9a551fee"></a>
## CURRENT_USER

<a id="6ca187a493430725"></a>
### Syntax

```
CURRENT_USER [()]
```

<a id="271130467949f9fd"></a>
### Description

It returns the current user.

The user information is managed in three types as follows.

- Logon user: It is a user who performed login, and it is maintained until the connection is closed.
- Session user: It is as same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: It is generally as same as the session user, but it is temporarily changed internally in system to control access when using the PSM, view.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="e1bdfb042ead4274"></a>
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

<a id="c8e656ddd5bf7118"></a>
## CURRVAL

<a id="8e0cce701db351fe"></a>
### Syntax

```
seq_name.CURRVAL
CURRVAL(seq_name)
```

<a id="cebefc4675835e16"></a>
### Description

The current value of the sequence object is obtained.

A sequence value should be set with NEXTVAL(seq_name) at least once.

<a id="aeebeb2941f58636"></a>
### Example

```
gSQL> SELECT seq.CURRVAL FROM dual;

SEQ.CURRVAL
-----------
          1

1 row selected.
```

<a id="73bc4e5a0097453e"></a>
## DATEADD

<a id="7a9aafe548773385"></a>
### Syntax

```
DATEADD( datepart, number, date )
```

<a id="9129825538090570"></a>
### Description

It adds number to the specified datepart of date, and returns the result.

If the number is decimal point, it is not rounded off.  
The date data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE.  
If number or date is NULL, the result is also NULL.

The result type which is as same as the input date argument type is returned.

**Available string format in datepart**

<a id="b27d82814a16bb4e"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">Description</th></tr><tr><td>YEAR</td><td>Year</td></tr><tr><td>QUARTER</td><td>Quarter</td></tr><tr><td>MONTH</td><td>Month</td></tr><tr><td>DAYOFYEAR</td><td>Day of year</td></tr><tr><td>DAY</td><td>Day</td></tr><tr><td>WEEK</td><td>Week</td></tr><tr><td>WEEKDAY</td><td>Weekday</td></tr><tr><td>HOUR</td><td>Hour</td></tr><tr><td>MINUTE</td><td>Minute</td></tr><tr><td>SECOND</td><td>Second</td></tr><tr><td>MILLISECOND</td><td>Millisecond</td></tr><tr><td>MICROSECOND</td><td>Microsecond</td></tr></tbody></table>

<a id="8c1facf4ddf131de"></a>
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

<a id="952b4d199f5f9ff9"></a>
## DATEDIFF

<a id="08b22bae16faeab9"></a>
### Syntax

```
DATEDIFF( datepart, startdate, enddate )
```

<a id="3c82dac1ff58287e"></a>
### Description

It substracts startdate from enddate, then returns the result to the specified datepart.

If the startdate or enddate is NULL, the result is also NULL.  
The data type of startdate and enddate can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME.

The result type is NUMBER.

**Available string format in datepart**

<a id="d4f212c480041538"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">Description</th></tr><tr><td>YEAR</td><td>Year</td></tr><tr><td>QUARTER</td><td>Quarter</td></tr><tr><td>MONTH</td><td>Month</td></tr><tr><td>DAYOFYEAR</td><td>Day of year</td></tr><tr><td>DAY</td><td>Day</td></tr><tr><td>HOUR</td><td>Hour</td></tr><tr><td>MINUTE</td><td>Minute</td></tr><tr><td>SECOND</td><td>Second</td></tr><tr><td>MILLISECOND</td><td>Millisecond</td></tr><tr><td>MICROSECOND</td><td>Microsecond</td></tr></tbody></table>

<a id="e1e713d216dd4ebc"></a>
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

<a id="c7d0d65ec40263a8"></a>
## DATE_ADD

<a id="77d7888dfbe3a3b4"></a>
### Syntax

```
DATE_ADD( date, INTERVAL expr unit  )
```

<a id="6a74a7b868aeae6b"></a>
### Description

It is the same function as [ADDDATE](#927624817574e79b) (date, INTERVAL expr unit).

<a id="9e8fb664023fc683"></a>
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

<a id="ca1f53ceaf11d028"></a>
## DATE_PART

<a id="2d9de4468bff4282"></a>
### Syntax

```
DATE_PART( field, datetime )
```

<a id="34924c4183e4b705"></a>
### Description

The result of DATE_PART is as same as the result of the EXTRACT function. It searches for the specified field from the input datetime type, and returns it.

The field argument should be text literal, and YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, TIMEZONE_HOUR, TIMEZONE_MINUTE can be specified to text literal.  
The datetime argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL.

If field is not in the range of datetime, an error is returned.   
For DATE type, field should be YEAR, MONTH, DAY, otherwise an error is returned.  
If datatime is NULL, then it returns NULL.

The return type is NUMBER.

For more information, refer to [EXTRACT](#c864a50524616031).

<a id="7bb3bde2a41bfd84"></a>
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

<a id="c9a93572129b7213"></a>
## DECODE

<a id="9ccd6743e9a141e5"></a>
### Syntax

```
DECODE( expr, comparison_expr1, result1
           [, comparison_expr2, result2
            , ...
            , comparison_exprN, resultN ]
           [, default ] )
```

<a id="3452f07f43a013ed"></a>
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

<a id="2cc635c509a453dd"></a>
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

<a id="1a2ad0a79787fcfe"></a>
## DEGREES

<a id="3f1ea66aa1a224e0"></a>
### Syntax

```
DEGREES( radians )
```

<a id="667289e92dc7962c"></a>
### Description

It converts a degree radians to a value in degrees, and returns the converted value.  
If radians is NULL, then it returns NULL.

<a id="3abaebe9ef81e412"></a>
### Example

```
gSQL> SELECT DEGREES( PI() ) AS RESULT FROM DUAL;
RESULT
------
   180
1 row selected.
```

<a id="3b285dd4138efd6c"></a>
## DENSE_RANK() OVER

<a id="feefcd943d318d6b"></a>
### Syntax

```
DENSE_RANK( ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="69e518e56983519c"></a>
### Description

Window function DENSE_RANK calculates the ranking.

The ranking is a consecutive integer starting from 1, and rows with the same value have the same rank.  
However, unlike RANK, even when rows with the same value appear, the ranking is not skipped.

window frame is not available.

<a id="eb5f338a278dc5eb"></a>
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

<a id="ba37ba1671acbc26"></a>
## DIGEST

<a id="6d1f43991b4455d6"></a>
### Syntax

```
DIGEST( data, type )
```

<a id="e7cdbaca79529cdc"></a>
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

<a id="0d4ce105900a3fec"></a>
### Example

```
gSQL> SELECT HEX( DIGEST( 'my password', 'SHA256' ) ) AS RESULT FROM DUAL;

RESULT                                                          
----------------------------------------------------------------
BB14292D91C6D0920A5536BB41F3A50F66351B7B9D94C804DFCE8A96CA1051F2

1 row selected.
```

<a id="9f742d88525891d7"></a>
## DUMP

<a id="b7a8a090bc8f0f10"></a>
### Syntax

```
DUMP( expr )
```

<a id="b9ac0b0726624b2f"></a>
### Description

It returns internal representation information of expr.  
Internal representation information is displayed as the data type, byte length and data information.

expr can be any data types.  
If expr is NULL, then it returns NULL.  

The return type is CHARACTER VARYING.

<a id="556d8981676715c1"></a>
### Example

```
gSQL> SELECT DUMP( 'DUMP' ) AS RESULT FROM DUAL;
RESULT                           
---------------------------------
Type=CHAR Len=4 : Str=68,85,77,80
1 row selected.
```

<a id="2600fc31f0747d3e"></a>
## EXP

<a id="f1012c4edd4f9d28"></a>
### Syntax

```
EXP( num )
```

<a id="a1616afa74bb84bd"></a>
### Description

It returns squared value of e (base of natural logarithm)'s num.  
If num is NULL, then it returns NULL.

<a id="8217291d03f863e0"></a>
### Example

```
gSQL> SELECT EXP( 1 ) AS RESULT FROM DUAL;
          RESULT
----------------
2.71828182845905
1 row selected.
```

<a id="c864a50524616031"></a>
## EXTRACT

<a id="faa3ab0db3247403"></a>
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

<a id="8ce0a088d61b576a"></a>
### Description

It searches for the specified field from an input datetime type, and returns it.

The datetime argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL.

If field is not in the range of datetime, an error is returned.   
For DATE type, the field should be YEAR, MONTH, DAY, otherwise an error is returned.  
The return type is NUMBER.

Result of EXTRACT is as same as the result of the [DATE_PART](#ca1f53ceaf11d028) function.

<a id="1da801e8f04e9a3a"></a>
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

<a id="a2d53e1ef16df5f7"></a>
## FACTORIAL

<a id="d5ae9e927a961431"></a>
### Syntax

```
FACTORIAL( num )
```

<a id="84e786424588287e"></a>
### Description

It multiplies the successive natural numbers from 1 to num in order, and returns the result.  
If num is NULL, then it returns NULL.

<a id="beccc1ebc7350c2a"></a>
### Example

```
gSQL> SELECT FACTORIAL( 5 ) AS RESULT FROM DUAL;
RESULT
------
   120
1 row selected.
```

<a id="3ea9b3192ce39867"></a>
## FIRST() OVER

<a id="a524ef2059338bd6"></a>
### Syntax

```
aggregation_function KEEP ( DENSE_RANK FIRST ORDER BY <sort specification list> ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="b6928bda85732a05"></a>
### Description

Window function FIRST sorts the sort specification list used in *order by* within KEEP clause, then returns the aggregation function value of rows whose DENSE_RANK is 1.

aggregation_functions are AVG, COUNT, COUNT(*), SUM, MAX, MIN, STDDEV, VARIANCE.

*order by* is not available within the window clause.  
window frame is not available.

<a id="80fe1217ab6f04b8"></a>
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

<a id="ff8ac9584af26954"></a>
## FIRST_VALUE() OVER

<a id="f68c97b461a4ee81"></a>
### Syntax

```
FIRST_VALUE ( expr ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

FIRST_VALUE ( expr [ RESPECT NULLS | IGNORE NULLS ] ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="64b8fe5cfbe82b2b"></a>
### Description

Window function FIRST_VALUE returns the first value of expr.

RESPECT NULLS returns the first value of rows including NULL.  
IGNORE NULLS returns the first value of row except for NULL.  
If it is not specified, the default value is RESPECT NULLS.

*order by* is not available in window clause.  
window frame is not available.

<a id="8a2826ad69ad22ba"></a>
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

<a id="7c53322abec2bc64"></a>
## FLOOR

<a id="c3725cab3dab7d8d"></a>
### Syntax

```
FLOOR( num )
```

<a id="0ba43a656663620b"></a>
### Description

It returns the biggest integer which is equal to or smaller than num.  
If num is NULL, then it returns NULL.

<a id="9d590d62f8476d42"></a>
### Example

```
gSQL> SELECT FLOOR(42.8) AS RESULT1, FLOOR(-42.8) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     42     -43
1 row selected.
```

<a id="8e25e052ba17c43a"></a>
## FROM_BASE64

<a id="3b171b7e4904f595"></a>
### Syntax

```
FROM_BASE64( str )
```

<a id="589339a181ec73de"></a>
### Description

The converted character by base 64 encoding is input to FROM_BASE64, then the decoded binary string is returned.

The input argument data type can be a character type such as CHARACTER VARYING, CHARACTER LONG VARYING, and the result type is a binary character such as BINARY VARYING or BINARY LONG VARYING.

If str is NULL, then the result value is also NULL.  
If str includes characters which are not in the range of base64 character, then it returns an error.  
A newline, carriage return, tab, and space of str is ignored when decoding.

For more information, refer to [TO_BASE64](#9042ca2ffd6f273a).

<a id="5dc7911182fa59e2"></a>
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

<a id="e364ff079d11e90d"></a>
## FROM_TZ

<a id="c21e6bb5b3a6162f"></a>
### Syntax

```
FROM_TZ( timestamp, timezone )
```

<a id="2ff9c321415b4982"></a>
### Description

FROM_TZ function converts the timestamp and the timezone in the specified format to TIMESTAMP WITH TIME ZONE type, then returns it.

The timestamp argument should be TIMESTAMP type or the type convertible to TIMESTAMP type.   
If the timestamp argument is NULL, then the result value is also NULL.

The timezone argument should be CHARACTER type such as CHARACTER and CHARACTER VARYING, and the format is 'TZH:TZM'.   
If the timezone argument is NULL, then the result is also NULL.

The result type is TIMESTAMP(6) WITH TIME ZONE.

<a id="3f64ffbd6bd014e5"></a>
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

<a id="e133acf2a0699694"></a>
## GREATEST

<a id="3e30fa66674d1ace"></a>
### Syntax

```
GREATEST( expr1 [, expr2, ... exprn ] )
```

<a id="b0b98234547741ea"></a>
### Description

It returns the largest value among the received expr argument.

If any expr argument is NULL, the result value is NULL.

The result type becomes the data type of expr1  (the first expr).   
If the data type of expr1 (the first expr) is a character type and a numeric type then it becomes the type including the range of expr1, ..., exprN each.  
If all of expr1, ..., exprN is described in CHAR type, then all exprs are compared in VARCHAR type and the result type is VARCHAR.

<a id="41ba6076dc86fa13"></a>
### Example

```
gSQL> SELECT GREATEST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
   200
1 row selected.
```

<a id="bf45ca2b2bcf6736"></a>
## HASH32

<a id="a23e4ad5c9ddb58c"></a>
### Syntax

```
HASH32( expr [, expr]... )
```

<a id="e1ddb49db7ff6450"></a>
### Description

The HASH32 function calculates and returns the hash value of the provided expr arguments.

At least one argument must be specified, and up to a maximum of 32 arguments can be provided.  
If any of the input arguments is NULL, the result will be NULL.

The return type is NATIVE_INTEGER.

<a id="9fd1dbb43b3a967a"></a>
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

<a id="ee8a91a688aadcab"></a>
## HEX

<a id="bc0af32a9b0621f3"></a>
### Syntax

```
HEX( str )
```

<a id="102a6e2433ab3404"></a>
### Description

It returns a str argument in hexadecimal character.  
A str argument data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, a type which can be converted to a character type, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.  
The result type is a character type such as CHARACTER VARYING or CHARACTER LONG VARYING.

If str is NULL, then the result value is also NULL.

If an argument of HEX function is a numeric type, then it returns an error.   
To convert a decimal number to a hexadecimal number, use TO_CHAR() function by using  'X' number format.  
e.g. TO_CHAR( 255, 'XX' )

For more information, refer to [UNHEX](#c1fe74c2be5e0dce).

<a id="2e14683f6bc1cc32"></a>
### Example

```
gSQL> SELECT HEX( 'abc' ) FROM DUAL;
HEX( 'abc' )
------------
616263      
1 row selected.
```

<a id="7507e2de61737b03"></a>
## INITCAP

<a id="64b44e1fc70fee33"></a>
### Syntax

```
INITCAP( str )
```

<a id="7527996e74ec4a61"></a>
### Description

It converts the first letter in each word of string str into uppercase, and converts all other letters into lowercase, then it returns the result.

str data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

Each word in string is classified by white space or characters which are not alphanumeric.  
If str is NULL, the result is also NULL.

The return type is as same as str argument datatype.

<a id="3faee819d7fc2fad"></a>
### Example

```
gSQL> SELECT INITCAP( 'hi GLIESE' ) AS RESULT FROM DUAL;
RESULT   
---------
Hi Gliese
1 row selected.
```

<a id="5dc08606e256048e"></a>
## INSTR

<a id="8962946a0158bf71"></a>
### Syntax

```
INSTR( str, substr [, position [, occurrence ] ] )
```

<a id="d18112c316039e5c"></a>
### Description

It search for occurrence<sup>th</sup> substr starting from str's position, and returns its location.

The data types of str arguments and substr arguments can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

The position argument and the occurrence argument can be numeric data type.

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

<a id="6394a223854de917"></a>
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

<a id="94293f3bf1dcc625"></a>
## JSON_ARRAY

<a id="4d6f718a3652cf46"></a>
### Syntax

```
JSON_ARRAY( [ value_expression [, ...] ]
            [<JSON constructor null clause>]
            [<JSON output clause>]
          )
```

For more information about the &lt;JSON constructor null clause&gt;, refer to the [JSON Constructor Null Clause](11-sql-elements.md#1c3a3c2ef843723a) section.

For more information about the &lt;JSON output clause&gt;, refer to the [JSON Output Clause](11-sql-elements.md#57242fece54b39a5) section.

<a id="5dfe31f280a70439"></a>
### Description

JSON_ARRAY returns zero or more expressions as a JSON array string.

The JSON constructor null clause is an option that specifies how to handle SQL null values.  
If not specified, the default is ABSENT ON NULL.

The JSON output clause is an option that specifies the data type of the function's result.  
If not specified, the default is VARCHAR(4000).

<a id="6f70d04365ab334e"></a>
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

<a id="601412b5f2e75023"></a>
## JSON_ARRAYAGG

<a id="bd5df4da5aad2130"></a>
### Syntax

```
JSON_ARRAYAGG( value_expression
               [<JSON constructor null clause>]
               [<JSON output clause>]
             )
```

For more information about the &lt;JSON constructor null clause&gt;, refer to the [JSON Constructor Null Clause](11-sql-elements.md#1c3a3c2ef843723a) section.

For more information about the &lt;JSON output clause&gt;, refer to the [JSON Output Clause](11-sql-elements.md#57242fece54b39a5) section.

<a id="f875951209e92d5d"></a>
### Description

JSON_ARRAYAGG is an aggregation function that concatenates value expressions and returns a single JSON array string row.

The JSON constructor null clause is an option that specifies how to handle SQL null values.   
If not specified, the default is ABSENT ON NULL.

The JSON output clause is an option that specifies the data type of the function's result.   
If not specified, the default is VARCHAR(4000).

<a id="6b2a1a24fac528a6"></a>
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
```

<a id="ea5a2230a661abf0"></a>
## JSON_ARRAYAGG() OVER

<a id="aa2fa6d86b022821"></a>
### Syntax

```
JSON_ARRAYAGG( value_expression
               [<JSON constructor null clause>]
               [<JSON output clause>]
             ) OVER < window name or specification >
```

For more information about the &lt;JSON constructor null clause&gt;, refer to the [JSON Constructor Null Clause](11-sql-elements.md#1c3a3c2ef843723a) section.

For more information about the &lt;JSON output clause&gt;, refer to the [JSON Output Clause](11-sql-elements.md#57242fece54b39a5) section.

For more information about the &lt;window name or specification&gt;, refer to the [window clause](20-sql-references-h-z.md#6de1c122457d94b3) section.

<a id="02fa3eae4d9898b0"></a>
### Description

JSON_ARRAYAGG is a window function that concatenates value expressions within the window frame to generate a JSON array string.

The JSON constructor null clause is an option that specifies how to handle SQL null values.   
If not specified, the default is ABSENT ON NULL.

The JSON output clause is an option that specifies the data type of the function's result.   
If not specified, the default is VARCHAR(4000).

<a id="bc5c4cb732afed48"></a>
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

<a id="b388bbc3cd35802e"></a>
## JSON_OBJECT

<a id="13fab75d45f6858c"></a>
### Syntax

```
JSON_OBJECT( [ <JSON name and value> [, ...] ]
             [ <JSON constuctor null clause> ]
             [ <JSON output clause> ]
           )

<JSON name and value> ::=
    [KEY] <JSON name> VALUE <value_expression>
  | <JSON name> : <value_expression>
```

For more information about the &lt;JSON constructor null clause&gt;, refer to the [JSON Constructor Null Clause](11-sql-elements.md#1c3a3c2ef843723a) section.

For more information about the &lt;JSON output clause&gt;, refer to the [JSON Output Clause](11-sql-elements.md#57242fece54b39a5) section.

<a id="d3ef52e44e43db61"></a>
### Description

JSON_OBJECT returns zero or more JSON name and values as a JSON object string.  
A JSON name must be an expression that can be represented as a character string.

The JSON constructor null clause is an option that specifies how to handle SQL null values.   
If not specified, the default is NULL ON NULL.

The JSON output clause is an option that specifies the data type of the function's result.   
If not specified, the default is VARCHAR(4000).

<a id="30d939b74e920cb5"></a>
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

<a id="3fa8c49abe80530b"></a>
## JSON_OBJECTAGG

<a id="5ae1fd07ccdc3888"></a>
### Syntax

```
JSON_OBJECTAGG( <JSON name and value>
                [ <JSON constructor null clause> ]
                [ <JSON output clause> ]
              )

<JSON name and value> ::=
    [KEY] <JSON name> VALUE <value_expression>
  | <JSON name> : <value_expression>
```

For more information about the &lt;JSON constructor null clause&gt;, refer to the [JSON Constructor Null Clause](11-sql-elements.md#1c3a3c2ef843723a) section.

For more information about the &lt;JSON output clause&gt;, refer to the [JSON Output Clause](11-sql-elements.md#57242fece54b39a5) section.

<a id="11ca5973b6dae6b9"></a>
### Description

JSON_OBJECTAGG is an aggregation function that concatenates JSON name-value pairs and returns a single JSON object string row.  
A JSON name must be an expression that can be represented as a character string.

The JSON constructor null clause is an option that specifies how to handle SQL null values.   
If not specified, the default is NULL ON NULL.

The JSON output clause is an option that specifies the data type of the function's result.   
If not specified, the default is VARCHAR(4000).

<a id="061a610a10e03511"></a>
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
```

<a id="4ada1dbdfa329af8"></a>
## JSON_OBJECTAGG() OVER

<a id="effcb861b69616c1"></a>
### Syntax

```
JSON_OBJECTAGG( <JSON name and value>
                [ <JSON constructor null clause> ]
                [ <JSON output clause> ]
              ) OVER < window name or specification >

<JSON name and value> ::=
    [KEY] <JSON name> VALUE <value_expression>
  | <JSON name> : <value_expression>
```

For more information about the &lt;JSON constructor null clause&gt;, refer to the [JSON Constructor Null Clause](11-sql-elements.md#1c3a3c2ef843723a) section.

For more information about the &lt;JSON output clause&gt;, refer to the [JSON Output Clause](11-sql-elements.md#57242fece54b39a5) section.

For more information about the &lt;window name or specification&gt;, refer to the [window clause](20-sql-references-h-z.md#6de1c122457d94b3) section.

<a id="79eb6ab25eceac47"></a>
### Description

JSON_OBJECTAGG is a window function that concatenates JSON name-value pairs within the window frame to generate a JSON object string.  
A JSON name must be an expression that can be represented as a character string.

The JSON constructor null clause is an option that specifies how to handle SQL null values.   
If not specified, the default is NULL ON NULL.

The JSON output clause is an option that specifies the data type of the function's result.   
If not specified, the default is VARCHAR(4000).

<a id="e55d74cfc0023511"></a>
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

<a id="af864d941533e203"></a>
## LAG() OVER

<a id="835addc235b3c8d4"></a>
### Syntax

```
LAG ( expr [, offset [, default ] ] ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

LAG ( expr [ RESPECT NULLS | IGNORE NULLS ] [, offset [, default ] ] ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="214fc2694a2f291e"></a>
### Description

Window function LAG returns the row value ahead from the current row as far as offset.  
If offset is out of window range, then it returns the default value.

If the offset and default values are not specified, they are set to the default value.    
The default value of offset is 1 and the default value of default is NULL.

RESPECT NULLS returns the row value ahead as far as offset including NULL.  
IGNORE NULLS returns the row value ahead as far as offset except for NULL.  
If it is not specified, the default value is RESPECT NULLS.

window frame is not available.

<a id="39becf2db3d25530"></a>
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

The following is an example of specifying offset.

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

The following is an example of specifying offset and default.

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

<a id="e241a2d11f0602c4"></a>
## LAST() OVER

<a id="9443cfdfa7abb76d"></a>
### Syntax

```
aggregation_function KEEP ( DENSE_RANK LAST ORDER BY <sort specification list> ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="773c27fe41e9bcbb"></a>
### Description

Window function LAST sorts the sort specification list used in *order by* within KEEP clause, then returns the aggregation function value of rows whose DENSE_RANK is the last.

aggregation_functions are AVG, COUNT, COUNT(*), SUM, MAX, MIN, STDDEV, VARIANCE.

*order by* is not available within the window clause.  
window frame is not available.

<a id="83d3a2e342a842f8"></a>
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

<a id="04b60c5de4f07e66"></a>
## LAST_DAY

<a id="3242c2c980150c96"></a>
### Syntax

```
LAST_DAY( date )
```

<a id="53f911e45a7956ef"></a>
### Description

It returns the last day of the month which is included in date.

The date argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.  
The return type is always DATE regardless of the date argument data type.  

If date is NULL, then it returns NULL.

<a id="0ecbb2e3e1d27522"></a>
### Example

```
gSQL> SELECT 
      LAST_DAY( TO_DATE( '2012-07-10', 'YYYY-MM-DD' ) ) AS RESULT FROM DUAL;
RESULT    
----------
2012-07-31
1 row selected.
```

<a id="e5492376ea4f8fe9"></a>
## LAST_IDENTITY_VALUE

<a id="a3f7755e9742ff77"></a>
### Syntax

```
LAST_IDENTITY_VALUE()
```

<a id="1b8fa982f784450c"></a>
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

To obtain an identity column value created when performing the INSERT, use [INSERT INTO name RETURNING .. INTO](20-sql-references-h-z.md#23ef94214962e563) statement as follows.

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

<a id="9832552739b19a97"></a>
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

<a id="65e774a52e3bfa7d"></a>
## LAST_VALUE() OVER

<a id="47a238d0241d40cc"></a>
### Syntax

```
LAST_VALUE ( expr ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

LAST_VALUE ( expr [ RESPECT NULLS | IGNORE NULLS ] ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="4d0a626012b308ff"></a>
### Description

Window function LAST_VALUE returns the last value of expr.

RESPECT NULLS returns the last value of rows including NULL.   
IGNORE NULLS returns the last value of row except for NULL.   
If it is not specified, the default value is RESPECT NULLS.

*order by* is not available in window clause.  
window frame is not available.

<a id="88111659088cb12e"></a>
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

The following is an example of specifying IGNORE NULLS in null_treatment.

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

<a id="5292f627db30261d"></a>
## LEAD() OVER

<a id="432fd92a1cabc0d6"></a>
### Syntax

```
LEAD ( expr [, offset [, default ] ] ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

LEAD ( expr [ RESPECT NULLS | IGNORE NULLS ] [, offset [, default ] ] ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="5d0bd479bbb2c0b4"></a>
### Description

Window function LEAD returns the row value behind from the current row as far as offset.   
If offset is out of window range, then it returns the default value.

If the offset and default values are not specified, they are set to the default value.    
The default value of offset is 1 and the default value of default is NULL.

RESPECT NULLS returns the row value behind as far as offset including NULL.  
IGNORE NULLS returns the row value behind as far as offset except for NULL.  
If it is not specified, the default value is RESPECT NULLS.

window frame is not available.

<a id="c3e29666c94b3890"></a>
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

The following is an example of specifying offset.

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

The following is an example of specifying offset and default.

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

<a id="2f641928d02d76a5"></a>
## LEAST

<a id="b90d41dc4576faa8"></a>
### Syntax

```
LEAST( expr1 [, expr2, ... exprn ] )
```

<a id="ea20f4dc2116533a"></a>
### Description

It returns the smallest value among received expr arguments.

If any of expr is NULL, the result is NULL.

The result type is determined according to the data type of expr1 (the first expr).   
If the data type of expr1 (the first expr) is a character type and a numeric type then it becomes the type including the range of expr1, ..., exprN each.  
If all of expr1, ..., exprN is described in CHAR type, then all exprs are compared in VARCHAR type and the result type is VARCHAR.

<a id="0e08ff3087d61fe5"></a>
### Example

```
gSQL> SELECT LEAST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="0429eb6207fb17d4"></a>
## LENGTH

<a id="811a3948812f1f84"></a>
### Syntax

```
LENGTH( str )
```

<a id="043452ba368272a3"></a>
### Description

It is an alias of [CHAR_LENGTH](#a1c40efd346b484f).

<a id="cbb039513f624b9e"></a>
### Example

Multi byte character set: (e.g.UTF8)

```
gSQL> SELECT LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="47f3cf241a8776e8"></a>
## LENGTHB

<a id="e9cb32318e6befbf"></a>
### Syntax

```
LENGTHB( str )
```

<a id="ea8705857c932e4a"></a>
### Description

It is an alias of [OCTET_LENGTH](#67879be1522706a0).  
For more information, refer to [BYTE_LENGTH](#076781007f6d69e0).

<a id="79993a1a0d8e1f3f"></a>
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

<a id="3f9e7bee2e2910a1"></a>
## LISTAGG() OVER

<a id="035f2bc9286286cc"></a>
### Syntax

```
LISTAGG( str [, delimiter] ) WITHIN GROUP ( ORDER BY <sort specification list> ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="e50a1e54ee82146a"></a>
### Description

Window function LISTAGG connects str in its order sorted within each group.

Only PARTITION BY clause is available in OVER() clause of LISTAGG.  
It divides the query result sets into groups by using OVER() clause.

It sorts the records within the group with WITHIN GROUP ( ORDER BY &lt;sort specification list&gt; ).

It connects str in the order of the record sorted within each group.  
If str is NULL, then it is excluded.

A delimiter is str connection delimiter, and if it is omitted the default value is NULL.

str can be a character string or a binary string.   
If str is a character string, then the result type is varchar.   
If str is a binary string, then the result type is varbinary.

<a id="9f71162dab7322ee"></a>
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

<a id="b3ddb38bb17446b4"></a>
## LN

<a id="84c172faed32cc83"></a>
### Syntax

```
LN( num )
```

<a id="def02e8804ea0362"></a>
### Description

It returns the natural logarithm value of num.  

num should be a value which is bigger than 0.  
If num is NULL, then it returns NULL.

<a id="d8a115f992225d1a"></a>
### Example

```
gSQL> SELECT LN( 2.71828182845905 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="c0cda34337abbdfa"></a>
## LNNVL

<a id="d099e7a95ebcf35c"></a>
### Syntax

```
LNNVL( expr )
```

<a id="2842e5455550710d"></a>
### Description

Logical Not Null VaLue (LNNVL) function is similar to NOT logical operator, but the difference is that it returns TRUE as in the following example when the input value is null.

<a id="29828ed25fe24c57"></a>
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

<a id="f87ec03dde9b2802"></a>
## LOCALTIME

<a id="619e65d45f9ae61c"></a>
### Syntax

```
LOCALTIME [()]
STATEMENT_LOCALTIME()
```

<a id="ceee5704c2d21fbb"></a>
### Description

The current TIME WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.  
• LOCALTIME, STATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="77f5e5590bcc3766"></a>
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

<a id="f60256001d044f94"></a>
## LOCALTIMESTAMP

<a id="5ca9599b69664ecc"></a>
### Syntax

```
LOCALTIMESTAMP [()]
STATEMENT_LOCALTIMESTAMP()
```

<a id="6da22345e75760d7"></a>
### Description

The current TIMESTAMP WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• LOCALTIMESTAMP, STATEMENT_LOCALTIMESTAMP(): All TIMESTAMP values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="d26eb9a70c5e1b05"></a>
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

<a id="5c89089c8397af05"></a>
## LOCAL_GROUP_ID

<a id="130d46d2d8251528"></a>
### Syntax

```
LOCAL_GROUP_ID()
```

<a id="a13a634da2984660"></a>
### Description

It returns a cluster group ID for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="efa5baa746b234c8"></a>
### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_GROUP_ID() FROM DUAL;

LOCAL_GROUP_ID()
----------------
               1

1 row selected.
```

<a id="0e263850d9082694"></a>
## LOCAL_GROUP_NAME

<a id="6051d55dc1bbed72"></a>
### Syntax

```
LOCAL_GROUP_NAME()
```

<a id="b75fca6854805c84"></a>
### Description

It returns a cluster group name for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="3e96fd7528411d2c"></a>
### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_GROUP_NAME() FROM DUAL;

LOCAL_GROUP_NAME()
------------------
G1                

1 row selected.
```

<a id="7babd9f04abc3862"></a>
## LOCAL_MEMBER_ID

<a id="5e702c142103ef03"></a>
### Syntax

```
LOCAL_MEMBER_ID()
```

<a id="52c774f62b9f04e7"></a>
### Description

It returns a cluster member ID for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="ecb27d4f5ce06c2f"></a>
### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_MEMBER_ID() FROM DUAL;

LOCAL_MEMBER_ID()
-----------------
                1

1 row selected.
```

<a id="7333285941213c5f"></a>
## LOCAL_MEMBER_NAME

<a id="4ef1485b43ffd7e4"></a>
### Syntax

```
LOCAL_MEMBER_NAME()
```

<a id="098c41f14c78ce3d"></a>
### Description

It returns a cluster member name for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="bebe1d97e25bb889"></a>
### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_MEMBER_NAME() FROM DUAL;

LOCAL_MEMBER_NAME()
-------------------
G1N1               

1 row selected.
```

<a id="528a94c43f2c58d6"></a>
## LOG

<a id="c3482495ce059415"></a>
### Syntax

```
LOG( num2 )
LOG( num1, num2 )
```

<a id="3123cf773c68030f"></a>
### Description

It returns the logarithm of num2 in the num1 base.  
If num1 is omitted, it returns the logarithm value whose base is 10.

num1 should be a positive number except 1 and 0, and num2 should be a positive number.

If num1 or num2 is NULL, then it returns NULL.

<a id="49fae00693d1ca21"></a>
### Example

```
gSQL> SELECT LOG( 100 ) AS RESULT1, LOG( 4, 16 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      2       2
1 row selected.
```

<a id="163d031127d7fd13"></a>
## LOGON_USER

<a id="82c3a7248390f64b"></a>
### Syntax

```
LOGON_USER()
```

<a id="e5e0e2e01bc5fc0e"></a>
### Description

It returns the logged-in user.

The user information is managed in three types as follows.

- Logon user: It is a user who performed login, and it is maintained until the connection is closed.
- Session user: It is as same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: It is generally as same as the session user, but it is temporarily changed internally in system to control access when using the PSM, view.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="a991c952512480ee"></a>
### Example

```
% gsql test test

gSQL> SELECT LOGON_USER() AS result FROM DUAL;

RESULT
------
TEST  

1 row selected.
```

<a id="40f49752a8d3215b"></a>
## LOWER

<a id="67c9197715715783"></a>
### Syntax

```
LOWER( str )
```

<a id="7a858fd7999bceec"></a>
### Description

It returns lowercases of str.

The str argument data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If str is NULL, the result is also NULL.

The return type is the same datatype as the str argument.

<a id="c95f271d811a0ae2"></a>
### Example

```
gSQL> SELECT LOWER( 'SPRING' ) AS RESULT FROM DUAL;
RESULT
------
spring
1 row selected.
```

<a id="d4db89e4b4fa9cb6"></a>
## LPAD

<a id="2d4ad1a0dde7870d"></a>
### Syntax

```
LPAD( str, length, [, fill] )
```

<a id="a84583e11432afe9"></a>
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

<a id="923a6b73977e08f3"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="390dace1dc4d5382"></a>
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

<a id="1b3ee0e257f64ca0"></a>
## LTRIM

<a id="1a928ae81a4dc2a1"></a>
### Syntax

```
LTRIM( trim_source [, trim_character ] )
```

<a id="b4e158e1a14614e3"></a>
### Description

It removes the matching characters by comparing from the left side of trim_character in trim_source until the matching character does not exist. Then it returns the result.

The data type of trim_character and trim_source arguments can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, and a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If any of trim_character, trim_source is NULL, the result is NULL.  
If trim_character is omitted, a single blank space (' ') is specified by default.

The following table describes the result types.

**Result type of LTRIM**

<a id="0d115068646f8572"></a>
| trim_source, trim_character type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="b2a67d8ab2ae3bb2"></a>
### Example

```
gSQL> SELECT LTRIM( '_____LTRIM', '_' ) AS RESULT FROM DUAL;
RESULT
------
LTRIM 
1 row selected.
```

<a id="240d07ce2ffb63f8"></a>
## MAX

<a id="7169962418668548"></a>
### Syntax

```
MAX( [ ALL | DISTINCT ] expr )
```

<a id="47275b02c197bd99"></a>
### Description

It is an aggregate function and the maximum value among rows' exprs is obtained.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

MAX function returns the same result without being affected by the ALL and DISTINCT.

<a id="6360b0ed0174bf00"></a>
### Example

```
gSQL> SELECT MAX(c1) FROM t1;

MAX(C1)
-------
      3

1 row selected.
```

<a id="c73e0fb020dfe7b8"></a>
## MAX() OVER

<a id="98adfb55091bcbed"></a>
### Syntax

```
MAX ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="a2c406734fbed72b"></a>
### Description

Window function MAX obtains the maximum value of exprs.  
NULL is excluded from the calculation.

<a id="d48c42f000ac399f"></a>
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

<a id="5cb6f7689a212ef4"></a>
## MEDIAN() OVER

<a id="0f54e6bd8d772b7c"></a>
### Syntax

```
MEDIAN ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="fb782b636e9cab8e"></a>
### Description

Window function MEDIAN returns the median value of row.  
NULL is excluded from the calculation.

*order by* is not available within the window clause.  
window frame is not available.

<a id="acf0bfe6d3704e6a"></a>
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

<a id="a8402ad42933c631"></a>
## MIN

<a id="c034ed0854b3edd7"></a>
### Syntax

```
MIN( [ ALL | DISTINCT ] expr )
```

<a id="5f12c6ce72a3c23a"></a>
### Description

It is an aggregate function and the minimum value among rows' exprs is obtained.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

MIN function returns the same result without being affected by the ALL and DISTINCT.

<a id="f5fb764e78db88cc"></a>
### Example

```
gSQL> SELECT MIN(c1) FROM t1;

MIN(C1)
-------
      1

1 row selected.
```

<a id="0c0c1f53bd41f8ab"></a>
## MIN() OVER

<a id="9044b296c4ba7f03"></a>
### Syntax

```
MIN ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="f8f895751952ce87"></a>
### Description

Window function MIN obtains the minimum value of exprs.   
NULL is excluded from the calculation.

<a id="9298c36343d80924"></a>
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

<a id="7fc24b7bac9976ff"></a>
## MOD

<a id="e0c571957fdd5d52"></a>
### Syntax

```
MOD( num1, num2 )
```

<a id="babf5d7e4fdec208"></a>
### Description

It divides num1 by num2, and returns the remainder.  

The num1 argument and num2 argument can be a numeric data type.  
If num2 is 0, an error is returned.  
If the num1 argument or num2 argument is NULL, then NULL is returned.

<a id="dde2207b704b86fa"></a>
### Example

```
gSQL> SELECT MOD(5, 4) AS RESULT1, MOD(-5, 4) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1      -1
1 row selected.
```

<a id="259bdca28b32e0a2"></a>
## MONTHS_BETWEEN

<a id="33cab53a6bd157c8"></a>
### Syntax

```
MONTHS_BETWEEN( date1, date2 )
```

<a id="dd092811283e38ef"></a>
### Description

MONTHS_BETWEEN returns the number of months of which days between date2 and date1 are divided by 31.

If date1 or date2 is NULL, then the result is also NULL.  
The date1 argument and date2 argument can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE type.

The result type is NUMBER.

> If the same date (e.g. 2014-01-15 and 2014-02-15), or the last day of the month (e.g. 2014-08-31 and 2014-09-30) is included both in date1 and date2, then it returns the integer result regardless of the agreement of timestamp section (if it exists).

<a id="f4bf9a641b3ceb0e"></a>
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

<a id="430d32ffb0c1d41d"></a>
## NEXT_DAY

<a id="bbeef9dcb681ff9a"></a>
### Syntax

```
NEXT_DAY( date, day )
```

<a id="f60098e40a37fb1f"></a>
### Description

It obtains a date of the day (day of week) which comes first after the given date (an argument).

The second day argument can be a string or a number which indicates the day.  
• String: SUNDAY ~ SATURDAY  or SUN ~ SAT  
• Number: 1 (sunday) ~ 7 (saturday)  

If any of the input argument is NULL, the result is also NULL.

The return type is always DATE regardless of the input type of the date.  
The hour, minute and second of the result value returns the same hour, minute and second of the input argument date.

<a id="e5212b703c3f315c"></a>
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

<a id="09a5871960e3dd2e"></a>
## NEXTVAL

<a id="55fe714714fcd6d9"></a>
### Syntax

```
seq_name.NEXTVAL
NEXTVAL( seq_name )
NEXT VALUE FOR seq_name
```

<a id="a2f853e112b736de"></a>
### Description

It obtains the next value of the sequence object.

<a id="e3b651c602194ff6"></a>
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

<a id="b2f2bcf02228e81c"></a>
## NTH_VALUE() OVER

<a id="c3657eb12f38c631"></a>
### Syntax

```
NTH_VALUE ( expr, n ) [ FROM { FIRST | LAST } ][ { RESPECT | IGNORE } NULLS ] OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="9fd96dfb9c95143e"></a>
### Description

Window function NTH_VALUE returns the expr value of the n-th row.  
If the number of window's rows is less than n, then it returns NULL.

The n argument can be a numeric type or types which can be converted to number.

FROM FIRST points to the n-th row from the first row.  
FROM LAST points to the n-th row from the last row.  
If it is not specified, the default value is FROM FIRST.

RESPECT NULLS returns the value of the n-th row including NULL.   
IGNORE NULLS returns the value of the n-th row except for NULL.   
If it is not specified, the default value is RESPECT NULLS.

<a id="899deaf2a140b5e1"></a>
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

The following is an example of when FROM LAST is specified.

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

The following is an example of when IGNORE NULLS is specified.

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

<a id="8f290d2d1cbce99c"></a>
## NTILE() OVER

<a id="7e9fa89f54fadb81"></a>
### Syntax

```
NTILE( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="adb0a3858670b67e"></a>
### Description

Window function NTILE returns the bucket number corresponding to each row.

The bucket number is a consecutive integer starting from 1, and the number of buckets are as same as the number of expr.  
If the number of buckets are bigger than that of rows, a bucket is given to each row and other buckets remains empty.

expr should be a positive constant. If expr is not a fixed number, then expr should be the target of *window partition by*.

window frame is not available.

<a id="4074c874678e686b"></a>
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

The following is an example of when the number of buckets (the number of expr) is bigger than the number of rows.

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

<a id="66e124ffb2b38351"></a>
## NULLIF

<a id="2a0ee6a9e5bfe5cd"></a>
### Syntax

```
NULLIF( expr1, expr2 )
```

<a id="d926c07170a67308"></a>
### Description

If expr1 is equal to expr2, it returns NULL. If they are not equal it returns expr1 which is the first argument.

If the data types of expr1 and expr2 are different, the result type is determined by [Result Type Combination Rule](11-sql-elements.md#9a5dc6c72b766b73).

NULLIF can be expressed by using CASE as follows.

- NULLIF( expr1, expr2 )

```
CASE WHEN expr1 = expr2 THEN NULL 
       ELSE expr1 
  END
```

<a id="3b53ec326c8212b0"></a>
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

<a id="310abb57145bd678"></a>
## NUMTODSINTERVAL

<a id="65d396563f31abbd"></a>
### Syntax

```
NUMTODSINTERVAL( num, interval_indicator )
```

<a id="b0cedc73c9a8cfb0"></a>
### Description

It converts the number in interval_indicator unit to interval day to second type, then returns it.

The argument *number* is a numeric type.

The argument interval_indicator is a character type, like CHAR or VARCHAR, and it should be one of 'DAY', 'HOUR', 'MINUTE', 'SECOND' which is case insensitive.

If any argument is NULL, then NULL is returned as a result.

interval day(6) to second(6) type is returned as a result, and a user can not arbitrarily modify the precision. If the leading precision of the converted result exceeds the default precision, then an error is returned. If the fraction precision exceeds the default precision, then the rounded value is returned as a result.

<a id="d8ee38bc45359e1e"></a>
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

<a id="d608b1cd886ee7b6"></a>
## NUMTOYMINTERVAL

<a id="449d3fca5e3c5b70"></a>
### Syntax

```
NUMTOYMINTERVAL( num, interval_indicator )
```

<a id="5775cd75f70701b4"></a>
### Description

It converts the number in interval_indicator unit to interval year to month type, then returns it.

The argument *number* is a numeric type.

The argument interval_indicator is a character type, like CHAR or VARCHAR, and it should be one of 'YEAR', 'MONTH' which is case insensitive.

If any argument is NULL, then NULL is returned as a result.

interval year(6) to month type is returned as a result, and a user can not arbitrarily modify the precision. If the leading precision of the converted result exceeds the default precision, then an error is returned.

<a id="1e9a4765d190a15b"></a>
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

<a id="20e1ecd24c4856cf"></a>
## NVL

<a id="2d15bcc7a6abffb5"></a>
### Syntax

```
NVL( expr1, expr2 )
```

<a id="6a72b34376054308"></a>
### Description

If expr1 is not NULL, then it returns expr1. If expr1 is NULL, it returns expr2.

The result type is determined according to the data type of expr1.  
If NULL is described in expr1, then the result type is determined according to the data type of expr2.   
If the data type of expr1 is a character type and a numeric type then it becomes the type including the range of expr1 and expr2 each.  
If the data type of both expr1 and expr2 is CHAR type, then the result type is VARCHAR.

<a id="426581ea7dd76b1d"></a>
### Example

```
gSQL> SELECT I1, NVL( I1, 0 ) FROM T1;
  I1 NVL( I1, 0 )
---- ------------
   1            1
null            0
2 rows selected.
```

<a id="b768727f6ab40534"></a>
## NVL2

<a id="1b24fcbf74739694"></a>
### Syntax

```
NVL2( expr1, expr2, expr3 )
```

<a id="0d0657fe1f6da246"></a>
### Description

If expr1 is not null, then it returns expr2. If expr1 is NULL, it returns expr3.

The result type is determined according to the data type of expr2.   
If NULL is described in expr2, then the result type is determined according to the data type of expr3.  
If the data type of expr2 is a character type and a numeric type then it becomes the type including the range of expr2 and expr3 each.  
If the data type of both expr2 and expr3 is CHAR type, then the result type is VARCHAR.

<a id="7d7538c28aece711"></a>
### Example

```
gSQL> SELECT I1, NVL2( I1, I1 * 1000, 0 ) FROM T1;
  I1 NVL2( I1, I1 * 1000, 0 )
---- ------------------------
   1                     1000
null                        0
2 rows selected.
```

<a id="67879be1522706a0"></a>
## OCTET_LENGTH

<a id="77bcb9682ed786ff"></a>
### Syntax

```
OCTET_LENGTH( str )  

BYTE_LENGTH( str )     

LENGTHB( str )
```

<a id="2af4f75ee41fb081"></a>
### Description

It returns the number of bytes in str.

The str argument data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONGVARYING.

If the str data type is CHARACTER, the white spaces are included in the calculation.  
If str is NULL, the result is also NULL.

It is an alias of [BYTE_LENGTH](#076781007f6d69e0) and [LENGTHB](#47f3cf241a8776e8).

<a id="15996cb32f8d3a92"></a>
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

<a id="5d0b15a953c1001d"></a>
## OVERLAY

<a id="130aa5bb275c9617"></a>
### Syntax

```
OVERLAY( str1 PLACING str2 FROM start_position  [ FOR string_length ] )
```

<a id="cfc02ea1040b5bc4"></a>
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

For more information, refer to [SUBSTRING](#92dc347da526af32).

The following table describes the result types.

**Result type of OVERLAY**

<a id="c155ffd01eb47947"></a>
| str1, str2 types | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="2532cee6ad4d6300"></a>
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

<a id="7408d6ee5a3c57ed"></a>
## PERCENT_RANK() OVER

<a id="35a1f7c4612a9f6c"></a>
### Syntax

```
PERCENT_RANK( ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="b7dc5232ca8220e9"></a>
### Description

Window function PERCENT_RANK calculates the ranking ratio of each row for the entire number of rows.

The result of PERCENT_RANK function is the number between 0 and 1, and the rows with the same value have the same ratio value.

window frame is not available.

<a id="49ca9bbb07ab2513"></a>
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

<a id="4093af94bd47f734"></a>
## PERCENTILE_CONT() OVER

<a id="0187689718ee3a75"></a>
### Syntax

```
PERCENTILE_CONT( expr ) WITHIN GROUP ( ORDER BY <sort specification> ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="557e32cf0bca6b22"></a>
### Description

Window function PERCENTILE_CONT is an inverse distribution function assuming a consecutive distribution model.

It calculates the value corresponding to the specified percentile score for *not null values* sorted within the group.   
The calculation result may differ from the specific value sorted within the group.

expr should be the percentile score between 0 and 1.

Only PARTITION BY clause is available in OVER() clause.   
It divides the query result sets into groups by using PARTITION BY clause.

It sorts the records within the group with WITHIN GROUP ( ORDER BY &lt;sort specification&gt; ).   
It can specify only one &lt;sort specification&gt; in ORDER BY.

NULL is excluded from the sorted values.

The following is a calculation formula.

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

MEDIAN window function is a specific case among PERCENTILE_CONT window functions, and its default value is percentile score 0.5.

For more information, refer to the followings.

- [MEDIAN() OVER](#5cb6f7689a212ef4)
- [PERCENTILE_DISC() OVER](#890f430d60a92678)

<a id="5e707537c0e5a9c2"></a>
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

<a id="890f430d60a92678"></a>
## PERCENTILE_DISC() OVER

<a id="1a6d9516f7444c33"></a>
### Syntax

```
PERCENTILE_DISC( expr ) WITHIN GROUP ( ORDER BY <sort specification> ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="4c0259ff609bef97"></a>
### Description

Window function PERCENTILE_DISC is an inverse distribution function assuming a discrete distribution model.

It calculates the percentile score for *not null values* sorted within the group.   
It determines the smallest value among the values same or over the arguments percentile score of calculated percentile scores.  
It returns the determined percentile score.

expr should be the percentile score between 0 and 1.

Only PARTITION BY clause is available in OVER() clause.   
It divides the query result sets into groups by using PARTITION BY clause.

It sorts the records within the group with WITHIN GROUP ( ORDER BY &lt;sort specification&gt; ).   
It can specify only one &lt;sort specification&gt; in ORDER BY.

It calculates CUME_DIST for the sort expression value with the sorted record.  
When calculating CUME_DIST, NULL is excluded.

It determines the smallest value among CUME_DIST which is same or over the percentile score specified as expr.  
It returns the determined CUME_DIST value.

The result type is as same as sort expression value type.

For more information, refer to [CUME_DIST() OVER](#d269bdbb3864419a).

<a id="7fb25af17cb1fbb9"></a>
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

<a id="f47366636a81f1d7"></a>
## PHYSICAL_LENGTH

<a id="92f15fc11e799674"></a>
### Syntax

```
PHYSICAL_LENGTH( expr )
```

<a id="cd1aa48a571af29f"></a>
### Description

PHYSICAL_LENGTH returns the number of internal expression information bytes in expr.

The expr argument can be any data type.

If an input argument is NULL, then the result is 0.

<a id="7630d3c32916bb9e"></a>
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

<a id="3d3110750adc751c"></a>
## PI

<a id="5e3fa516a23b5dad"></a>
### Syntax

```
PI()
```

<a id="04fc5a4fa06e8315"></a>
### Description

It returns "π" constant.

<a id="ab23f765703e59c4"></a>
### Example

```
gSQL> SELECT PI() AS RESULT FROM DUAL;
              RESULT
--------------------
3.141592653589793E+0
1 row selected.
```

<a id="c4398d0f2ff636ac"></a>
## POSITION

<a id="5d29d0fa2f95bf83"></a>
### Syntax

```
POSITION( str1 IN str2 )
```

<a id="e8a3a525ac9e4cd0"></a>
### Description

It searches for the first str1 within str2, then returns its location.

The data type of str1 argument and str2 argument can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If str1 can not be found within str2, the return value is 0.  
If str1 is found within str2, the position of str1 is returned, and the return value starts from 1.  
The returned position value is calculated in character unit (not in byte unit).  
If str1 or str2 is NULL, the return value is also NULL.

<a id="51f33db4e236a11c"></a>
### Example

```
gSQL> SELECT POSITION( 'CHAR' IN 'LONG CHAR 2000' ) AS RESULT FROM DUAL;
RESULT
------
     6
1 row selected.
```

<a id="efeb6aa68624102e"></a>
## POWER

<a id="feb05226c274566f"></a>
### Syntax

```
POWER( num1, num2 )
```

<a id="6e29c3ed9dc1417f"></a>
### Description

It squares num1 to num2, and returns the result.

The num1 argument and num2 argument can be a numeric data type.  

If num1 is a negative number, num2 should be an integer.  
If num1 or num2 is NULL, the result is also NULL.

<a id="b8a8d0ace0fc814c"></a>
### Example

```
gSQL> SELECT POWER( 2, 3 ) AS RESULT FROM DUAL;
RESULT
------
     8
1 row selected.
```

<a id="421e4f438006e135"></a>
## RADIANS

<a id="127d724e5a4eb5a9"></a>
### Syntax

```
RADIANS( degrees )
```

<a id="77c5bab2bc887e9d"></a>
### Description

It returns the radians of degrees.  

The degrees argument can be a numeric data type.  
If the degrees argument is NULL, then NULL is returned.

<a id="9f1c72e4a7d43058"></a>
### Example

```
gSQL> SELECT RADIANS( 180 ) AS RESULT FROM DUAL;
          RESULT
----------------
3.14159265358979
1 row selected.
```

<a id="cd712f3846834401"></a>
## RANDOM

<a id="790bb887a3bdc353"></a>
### Syntax

```
RANDOM( min, max )
```

<a id="e57cb94f6341f37f"></a>
### Description

It returns a random value in the range above min and below max.  

The min argument and max argument can be a numeric data type.  
If either min argument or the max argument is NULL, then NULL is returned.

<a id="1c844d284db33b55"></a>
### Example

```
gSQL> SELECT RANDOM( 1, 100 ) AS RESULT FROM DUAL;
          RESULT
----------------
34.1870528003201
1 row selected.
```

<a id="5455eeaa6bf1b5d8"></a>
## RANK() OVER

<a id="21e94cd4fe2b7bb4"></a>
### Syntax

```
RANK( ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="4fb637815458a739"></a>
### Description

Window function RANK calculates the ranking.

The ranking is an integer starting from 1, and rows with the same value have the same rank.

window frame is not available.

<a id="37e2125c97438977"></a>
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

<a id="8eec06f9d7726364"></a>
## RATIO_TO_REPORT() OVER

<a id="795a95a94359cab0"></a>
### Syntax

```
RATIO_TO_REPORT ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="3174bf8adeebb378"></a>
### Description

Window function RATIO_TO_REPORT calculates the ratio of each row value for the total sum of expr values.  
If the row value is NULL, then it returns NULL as a result.

*order by* is not available in window clause.  
window frame is not available.

<a id="cc5feaa6d4272992"></a>
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

<a id="edbb2307f5157566"></a>
## REGR_AVGX() OVER

<a id="7ed27f70eb45cb55"></a>
### Syntax

```
REGR_AVGX( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="319f27aad6e2173c"></a>
### Description

Window function REGR_AVGX is a linear regression function.  
It calculates the average value of the independent variable expr2 of (X, Y) set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are numeral types.

expr1 is the dependent variable ( y ) and expr2 is the independent variable ( x ).

If expr1 is NULL or expr2 is NULL, then it is excluded from the target.

The following is a calculation formula.

```
AVG( expr2 )
```

The returned type is a numeric type.

The returned value is the result from the calculation or NULL.  
If all records are excluded from the target because expr1 or expr2 is NULL, then it returns NULL.

<a id="01a0e4f9885cb144"></a>
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

<a id="0fbb6375923ea6fd"></a>
## REGR_AVGY() OVER

<a id="0bbb3e1a9010fcb3"></a>
### Syntax

```
REGR_AVGY( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="2fa194ba1430af4e"></a>
### Description

Window function REGR_AVGY is a linear regression function.   
It calculates the average value of the dependent variable expr1 of (X, Y) set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are numeral types.

expr1 is an dependent variable ( y ) and expr2 is a independent variable ( x ).

If expr1 is NULL or expr2 is NULL, then it is excluded from the target.

The following is a calculation formula.

```
AVG( expr1 )
```

The returned type is a numeric type.

The returned value is the result from the calculation or NULL.   
If all records are excluded from the target because expr1 or expr2 is NULL, then it returns NULL.

<a id="bb94d9186d48eaa4"></a>
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

<a id="c1fa8b8a38eaf7c9"></a>
## REGR_COUNT() OVER

<a id="8f4b51d7adadce17"></a>
### Syntax

```
REGR_COUNT( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="9e86889409bfb0ff"></a>
### Description

Window function REGR_COUNT is a linear regression function.   
It calculates the least-squares-fit linear equation of (X, Y) set.

It returns the number of ( X, Y ) pairs, the execution targets of the linear equation and both of which are not NULL.

The arguments of expr1 and expr2 are numeral types.

expr1 is an dependent variable ( y ) and expr2 is a independent variable ( x ).

If expr1 is NULL or expr2 is NULL, then it is excluded from the target.

The returned type is a numeric type.

It returns the number of pairs both of whose expr1 and expr2 are not NULL.   
If all records are excluded from the target because expr1 or expr2 is NULL, then it returns 0.

<a id="ee428c125b635c88"></a>
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

<a id="73813dcaa4b54a79"></a>
## REGR_INTERCEPT() OVER

<a id="2a3f646c6cf35aad"></a>
### Syntax

```
REGR_INTERCEPT( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="3dc205c472673d37"></a>
### Description

Window function REGR_INTERCEPT is a linear regression function.   
It calculates the y intercept of (X, Y) set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are numeral types.

expr1 is an dependent variable ( y ) and expr2 is a independent variable ( x ).

If expr1 is NULL or expr2 is NULL, then it is excluded from the target.

The following is a calculation formula.

```
AVG( expr1 ) - REGR_SLOPE( expr1, expr2 ) * AVG( expr2 )
```

The returned type is a numeric type.

The returned value is the result from the calculation or NULL.

It returns NULL in the following cases.  
• When all records are excluded from the target because expr1 or expr2 is NULL  
• When the result of REGR_SLOPE is null

<a id="b155f4c14f193948"></a>
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

<a id="574d3fc5b731769b"></a>
## REGR_R2() OVER

<a id="a1f79205b454ad09"></a>
### Syntax

```
REGR_R2( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="c99fc977710f94f2"></a>
### Description

Window function REGR_R2  is a linear regression function.   
It calculates the coefficient of determination (R-squared or fitness) of (X, Y) set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are numeral types.

expr1 is an dependent variable ( y ) and expr2 is a independent variable ( x ).

If expr1 is NULL or expr2 is NULL, then it is excluded from the target.

The following is a calculation formula.

```
If VAR_POP( expr2 ) = 0, then it is NULL. 
If VAR_POP( expr1 ) = 0 and VAR_POP( expr2 ) != 0, then it is 1.
If VAR_POP( expr1 ) > 0 and VAR_POP( expr2 ) != 0, then it is POWER( CORR( expr1, expr2), 2 ).
```

The returned type is a numeric type.

The returned value is the result from the calculation or NULL.

It returns NULL in the following cases.  
• When all records are excluded from the target because expr1 or expr2 is NULL  
• When the result of VAR_POP (expr2) is 0

<a id="aac812806af6f19b"></a>
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

<a id="a663cb7403064411"></a>
## REGR_SLOPE() OVER

<a id="7361c5a164d25cf9"></a>
### Syntax

```
REGR_SLOPE( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="ffbc0ac2db0121fb"></a>
### Description

Window function REGR_SLOPE is a linear regression function.   
It calculates the slope of (X, Y) set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are numeral types.

expr1 is an dependent variable ( y ) and expr2 is a independent variable ( x ).

If expr1 is NULL or expr2 is NULL, then it is excluded from the target.

The following is a calculation formula.

```
COVAR_POP(expr1, expr2) / VAR_POP(expr2)
```

The returned type is a numeric type.

The returned value is the result from the calculation or NULL.

It returns NULL in the following cases.  
• When all records are excluded from the target because expr1 or expr2 is NULL  
• When the result of VAR_POP is 0

<a id="a3e8f45c16f201f3"></a>
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

<a id="94fc9a4442b883f2"></a>
## REGR_SXX() OVER

<a id="7da88d7edb5f3f69"></a>
### Syntax

```
REGR_SXX( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="fa7f2beab6534031"></a>
### Description

Window function REGR_SXX is a linear regression function.   
It is an auxiliary function calculating the diagnostic statistics of (X, Y) set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are numeral types.

expr1 is an dependent variable ( y ) and expr2 is a independent variable ( x ).

If expr1 is NULL or expr2 is NULL, then it is excluded from the target.

The following is a calculation formula.

```
REGR_COUNT( expr1, expr2 ) * VAR_POP( expr2 )
```

The returned type is a numeric type.

The returned value is the result from the calculation or NULL.   
If all records are excluded from the target because expr1 or expr2 is NULL, then it returns NULL.

<a id="0a419a6bd7fd882e"></a>
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

<a id="84aade9f2316e893"></a>
## REGR_SXY() OVER

<a id="cbb79a2c98c70362"></a>
### Syntax

```
REGR_SXY( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="a21147929b5b3024"></a>
### Description

Window function REGR_SXY is a linear regression function.   
It is an auxiliary function calculating the diagnostic statistics of (X, Y) set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are numeral types.

expr1 is an dependent variable ( y ) and expr2 is a independent variable ( x ).

If expr1 is NULL or expr2 is NULL, then it is excluded from the target.

The following is a calculation formula.

```
REGR_COUNT( expr1, expr2 ) * COVAR_POP( expr1, expr2 )
```

The returned type is a numeric type.

The returned value is the result from the calculation or NULL.   
If all records are excluded from the target because expr1 or expr2 is NULL, then it returns NULL.

<a id="92eddb6b4163aebe"></a>
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

<a id="be007e5a648ff0e4"></a>
## REGR_SYY() OVER

<a id="e1c5919d17964034"></a>
### Syntax

```
REGR_SYY( expr1, expr2 ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="64dc7960140ba645"></a>
### Description

Window function REGR_SYY is a linear regression function.   
It is an auxiliary function calculating the diagnostic statistics of (X, Y) set's least-squares-fit linear equation.

The arguments of expr1 and expr2 are numeral types.

expr1 is an dependent variable ( y ) and expr2 is a independent variable ( x ).

If expr1 is NULL or expr2 is NULL, then it is excluded from the target.

The following is a calculation formula.

```
REGR_COUNT( expr1, expr2 ) * VAR_POP( expr1 )
```

The returned type is a numeric type.

The returned value is the result from the calculation or NULL.   
If all records are excluded from the target because expr1 or expr2 is NULL, then it returns NULL.

<a id="605212b1f83aea10"></a>
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

<a id="604648789df3963a"></a>
## REPEAT

<a id="f2db548bf9bd8cf7"></a>
### Syntax

```
REPEAT( str, num )
```

<a id="5c1ddfbef865246c"></a>
### Description

The string repeats str as many times as specified in num, and returns the result.

The str argument can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

The num argument can be a numeric data type.

If either str or num is NULL, the result is also NULL.  
If num is 0 or a negative number, the result is also NULL.

The following table describes the result types.

**Result type of REPEAT**

<a id="e5dd61c80dc8386a"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="dc19143b1b81cdcb"></a>
### Example

```
gSQL> SELECT REPEAT( 'ab', 3 ) AS RESULT FROM DUAL;
RESULT
------
ababab
1 row selected.
```

<a id="755b9c738c2de01a"></a>
## REPLACE

<a id="20e51467c8063343"></a>
### Syntax

```
REPLACE( str, from, to )
```

<a id="f1d710c644b1fca5"></a>
### Description

It replaces all *from* strings in str string with *to* strings, and returns the result.

The str argument, the from argument, and the to argument can be character data types such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If str is NULL, the result is also NULL.  
If from is NULL, the str is returned without replacement.  
If to value is omitted or NULL, the str value of which from is removed is returned.

The following table describes the result types.

**Result type of REPLACE**

<a id="576a2d13bcfb73ab"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="9d932e6f875719f3"></a>
### Example

```
gSQL> SELECT REPLACE( 'HI GLIESE', 'HI', 'HELLO' ) AS RESULT FROM DUAL;
RESULT      
------------
HELLO GLIESE
1 row selected.
```

<a id="79d84a4c72d71d48"></a>
## REVERSE

<a id="f5b5200c26699329"></a>
### Syntax

```
REVERSE( str )
```

<a id="ae52cd669a6363e2"></a>
### Description

REVERSE returns characters of str in reverse order.

The str argument can be types that are convertible to a character string type or a binary string type.  
A character string type is performed in a character unit, and a binary string type can be performed in a byte unit.

If str is NULL, then it returns NULL.

The following table describes the arguments and result types.

**Argument and result type of REVERSE**

<a id="f11d30e60832040f"></a>
| str | Result type |
| --- | --- |
| CHAR | CHAR |
| VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY | BINARY |
| VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="ebd5c4c14b8657f8"></a>
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

<a id="3ab0595bd4ce828e"></a>
## ROUND( number )

<a id="f19924f6a10dd699"></a>
### Syntax

```
ROUND( num [, scale ] )
```

<a id="39c7f48ffc4097f9"></a>
### Description

It rounds off num based on scale, and returns the result.

The num argument and scale argument can be numeric data types.

If scale is omitted, the scale becomes 0 and is executed as if it is ROUND(num, 0).  
If scale is a positive number, it is rounded off based on the number of right digit of the decimal point. If scale is a negative number, it is rounded off based on the number of left digit of the decimal point.  

If either num argument or the scale argument is NULL, then NULL is returned.

<a id="a3a51d00d56771b0"></a>
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

<a id="327eb9ab0c6f5d23"></a>
## ROUND( date )

<a id="706253e01bd30abf"></a>
### Syntax

```
ROUND( date [ , fmt ] )
```

<a id="e912ba274da2956a"></a>
### Description

It rounds off the date in the specified fmt unit, and returns the result.

The data type of date argument can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.   
The fmt argument can be a character type such as CHARACTER, CHARACTER VARYING.   
If either date argument or the fmt argument is NULL, then NULL is returned.  

The result type is always DATE regardless of the date argument data type.

If fmt is omitted, the default is DAY.  
The following table describes the available format strings.

**Available format sting of fmt**

<a id="bd508e24386adffb"></a>
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

<a id="0b42beae4fb68807"></a>
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

<a id="d582894215e065dd"></a>
## ROW_NUMBER() OVER

<a id="af85d035c3f1af48"></a>
### Syntax

```
ROW_NUMBER( ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="68d1d397557352f2"></a>
### Description

Window function ROW_NUMBER assigns the unique number to each row.  
The unique number is a consecutive integer starting from 1.

window frame is not available.

<a id="3ad4c7f06dad39ab"></a>
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

<a id="40b57d72048c57a1"></a>
## ROWID_GRID_BLOCK_ID

<a id="4aa68154d41c8a25"></a>
### Syntax

```
ROWID_GRID_BLOCK_ID( rowid )
```

<a id="f5f65e80a4b5d8fa"></a>
### Description

It returns the GRID block ID.

> It is a valid information in a cluster system.

<a id="30fb8dbe450dd544"></a>
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

<a id="acd18388ff477cf5"></a>
## ROWID_GRID_BLOCK_SEQ

<a id="f8594482cd96be29"></a>
### Syntax

```
ROWID_GRID_BLOCK_SEQ( rowid )
```

<a id="e86763c56f04da1d"></a>
### Description

It returns the GRID block sequence.

> It is a valid information in a cluster system.

<a id="36db9be2aff538de"></a>
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

<a id="ff85dc18c2d0624a"></a>
## ROWID_MEMBER_ID

<a id="dcc5dacadffb64a2"></a>
### Syntax

```
ROWID_MEMBER_ID( rowid )
```

<a id="3a63d39422a19e70"></a>
### Description

It returns the member ID.

> It is a valid information in a cluster system.

<a id="be6b3e31ee6e7ce2"></a>
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

<a id="aa8c6a3fe47fcbe2"></a>
## ROWID_OBJECT_ID

<a id="5de6f5c9a1bc882e"></a>
### Syntax

```
ROWID_OBJECT_ID( rowid )
```

<a id="6df286b0d0f749e4"></a>
### Description

It returns the object ID.

> It is an invalid information in a cluster system.

<a id="b01a30b7382d5db5"></a>
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

<a id="a1c13291e9855322"></a>
## ROWID_PAGE_ID

<a id="f92ba495c726462b"></a>
### Syntax

```
ROWID_PAGE_ID( rowid )
```

<a id="93db43ae1e711c8f"></a>
### Description

It returns the page ID.

> It is an invalid information in a cluster system.

<a id="90c104d4aa83d407"></a>
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

<a id="ecadd414bf9ba38e"></a>
## ROWID_ROW_NUMBER

<a id="0aadae2016df5577"></a>
### Syntax

```
ROWID_ROW_NUMBER( rowid )
```

<a id="cbe6bdfa9a1ab2a6"></a>
### Description

It returns the row number.

> It is an invalid information in a cluster system.

<a id="2beb860d5895eba3"></a>
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

<a id="3b00c98aa6983e82"></a>
## ROWID_SHARD_ID

<a id="20c6a9902beff3c7"></a>
### Syntax

```
ROWID_SHARD_ID( rowid )
```

<a id="6434b487a297a84b"></a>
### Description

It returns the shard ID.

> It is a valid information in a cluster system.

<a id="3e873f7f637ecd93"></a>
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

<a id="e5a780cb2a304400"></a>
## ROWID_TABLESPACE_ID

<a id="19d69f82920032ef"></a>
### Syntax

```
ROWID_TABLESPACE_ID( rowid )
```

<a id="d090ffa2393def77"></a>
### Description

It returns the tablespace ID.

> It is an invalid information in a cluster system.

<a id="2c444b21d1a99629"></a>
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

<a id="d90dc69fd788e5fd"></a>
## ROWNUM

<a id="f97e083c62ba5b02"></a>
### Syntax

```
ROWNUM
```

<a id="6e607cfcae596bc5"></a>
### Description

It sequentially allocates a number starting from 1 to rows which satisfy the WHERE condition.

It allows using ROWNUM in WHERE clause for the compatibility with Oracle.

However, to restrict the number of the query results, it is recommended to use [offset limit clause](20-sql-references-h-z.md#c771472d1efdac51) (the SQL standard) as follows.

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

<a id="a6fffcf794764119"></a>
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

<a id="7059ecaea6a50fc6"></a>
## RPAD

<a id="605480e6338beba4"></a>
### Syntax

```
RPAD( str, length, [, fill] )
```

<a id="7b1c8afbf820de12"></a>
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

<a id="d2db7d013c36be39"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="5ef4b0b3e7422ff8"></a>
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

<a id="8d9dbe696deed1af"></a>
## RTRIM

<a id="93e4b9bbcab4aed7"></a>
### Syntax

```
RTRIM( trim_source [, trim_character ] )
```

<a id="2329b5f428c66f7f"></a>
### Description

It removes the matching characters by comparing from the right side of trim_character in trim_source until the matching character does not exist. Then it returns the result.

The data type of trim_character and trim_source arguments can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING or a binary data type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If any of trim_character, trim_source is NULL, the result is NULL.  
If trim_character is omitted, a single blank space (' ') is specified by default.

The following table describes the result types.

**Result type of RTRIM**

<a id="af6e33a57be72fee"></a>
| trim_source type, trim_character type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="33e488f42959eed0"></a>
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

<a id="c4807e7f5dc63075"></a>
## SESSION_ID

<a id="b8647b87ea039c5d"></a>
### Syntax

```
SESSION_ID()
```

<a id="20461cc694678e13"></a>
### Description

It obtains the current session ID.

<a id="615f7433ec82b640"></a>
### Example

```
gSQL> SELECT SESSION_ID() FROM dual;

SESSION_ID()
------------
           4

1 row selected.
```

<a id="d9b48a25605c605d"></a>
## SESSION_SERIAL

<a id="e9ed544a411cb931"></a>
### Syntax

```
SESSION_SERIAL()
```

<a id="45ed64081cdf0e35"></a>
### Description

It obtains the serial number of current session.

<a id="d1c61a9775aeda02"></a>
### Example

```
gSQL> SELECT SESSION_SERIAL() FROM dual;

SESSION_SERIAL()
----------------
              16

1 row selected.
```

<a id="050d5bbebf1a1f99"></a>
## SESSION_USER

<a id="d7d3d2b5e8d3feb4"></a>
### Syntax

```
SESSION_USER[()]
```

<a id="394f57b1f1f01ba6"></a>
### Description

It returns the session user.

The user information is managed in three types as follows.

- Logon user: It is a user who performed login, and it is maintained until the connection is closed.
- Session user: It is as same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: It is generally as same as the session user, but it is temporarily changed internally in system to control access when using the PSM, view.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="afc181f8774c300f"></a>
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

<a id="464fac99a9ce4f64"></a>
## SESSIONTIMEZONE

<a id="68aee7865b5a4717"></a>
### Syntax

```
SESSIONTIMEZONE()
```

<a id="1d4d4190010612dd"></a>
### Description

SESSIONTIMEZONE returns the time zone of the current session.   
The returned value is '[+|-]TZH:TZM' format character.  
The returned type is varchar.

<a id="d9c63605fec14bb0"></a>
### Example

Check the time zone of the current session.

```
gSQL> SELECT SESSIONTIMEZONE() FROM dual;

SESSIONTIMEZONE()
-----------------
+09:00           

1 row selected.
```

When modifying the time zone of the current session, then it returns the modified time zone value.

```
gSQL> SET TIME ZONE '-05:00';

Session set.

gSQL> SELECT SESSIONTIMEZONE() FROM dual;

SESSIONTIMEZONE()
-----------------
-05:00           

1 row selected.
```

<a id="bbd0942ddd65594d"></a>
## SHARD_GROUP_ID

<a id="424c4f89f607f697"></a>
### Syntax

```
SHARD_GROUP_ID( table_name, shard_key_value [, ... ] )
```

<a id="c1fb48e60da85cc7"></a>
### Description

It returns the group ID managing the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is NATIVE_BIGINT.

> It is a valid information in a cluster system.

<a id="7ec3d725df5d9b23"></a>
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

<a id="86452fcd4749b92b"></a>
## SHARD_GROUP_NAME

<a id="f94d17cefe9ad1af"></a>
### Syntax

```
SHARD_GROUP_NAME( table_name, shard_key_value [, ... ] )
```

<a id="3977d96446614f1c"></a>
### Description

It returns the group NAME managing the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is VARCHAR.

> It is a valid information in a cluster system.

<a id="285e5c307fdeb0f5"></a>
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

<a id="0db7e14f9f0752f5"></a>
## SHARD_ID

<a id="808f2f3d0ef7a580"></a>
### Syntax

```
SHARD_ID( table_name, shard_key_value [, ... ] )
```

<a id="661576fd09cea02d"></a>
### Description

It returns the ID for the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is NATIVE_BIGINT.

> It is a valid information in a cluster system.

<a id="1736bab039d1c062"></a>
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

<a id="6e0c4ca5be499d9f"></a>
## SHARD_NAME

<a id="a81633b37a42594a"></a>
### Syntax

```
SHARD_NAME( table_name, shard_key_value [, ... ] )
```

<a id="3258a163bfdfa3cb"></a>
### Description

It returns the NAME for the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is VARCHAR.

> It is a valid information in a cluster system.

<a id="df27e39af12bfd0c"></a>
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

<a id="e78ae9de2914e02b"></a>
## SHIFT_LEFT

<a id="c9993a1ec72ae3c3"></a>
### Syntax

```
SHIFT_LEFT( num, cnt )
```

<a id="5b7d69a79b99be05"></a>
### Description

It moves num to the left as many as cnt bits, and returns the movement values.

The data type of input num argument and cnt argument can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or the type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type,  the decimal point is truncated.

cnt is masked with 6 bit, and it is processed to a value in the range within 6 bit.

If either num or cnt is NULL, then NULL is returned.

The result type is NATIVE_BIGINT.

<a id="b88835fd1886e46d"></a>
### Example

```
gSQL> SELECT SHIFT_LEFT(1, 3) FROM DUAL;
SHIFT_LEFT(1, 3)
----------------
               8
1 row selected.
```

<a id="84d8bc7d6307366d"></a>
## SHIFT_RIGHT

<a id="081e525dae22f5c0"></a>
### Syntax

```
SHIFT_RIGHT( num, cnt )
```

<a id="ecbeb83793e9ed4a"></a>
### Description

It moves num to the right as many as cnt bits, and returns the movement values.

The data type of input num argument and cnt argument can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or the type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.

cnt is masked with 6 bit, and it is processed to a value in the range within 6 bit.

If either num or cnt is NULL, then NULL is returned.

The result type is NATIVE_BIGINT.

<a id="759933fea939ed29"></a>
### Example

```
gSQL> SELECT SHIFT_RIGHT(8, 3) FROM DUAL;
SHIFT_RIGHT(8, 3)
-----------------
                1
1 row selected.
```

<a id="5000551fa54ad54d"></a>
## SIGN

<a id="274c708b44ccfb8d"></a>
### Syntax

```
SIGN( num )
```

<a id="771483875f53dece"></a>
### Description

It returns the sign of num.

The num argument can be a numeric data type.

The return value is as follows.   
• If num < 0,  -1 is returned.  
• If num = 0, 0 is returned.  
• If num > 0, 1 is returned.

If num is NULL, then NULL is returned.

<a id="88919dcdf64c6574"></a>
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

<a id="8efad287dc9c3384"></a>
## SIN

<a id="e09b968e2b9bf1f1"></a>
### Syntax

```
SIN( num )
```

<a id="f646c08912b98879"></a>
### Description

It returns the sine value of num.  
If num is NULL, then NULL is returned.

<a id="27f35b34f8e0da45"></a>
### Example

```
gSQL> SELECT SIN( 0 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="55771b527f4910fe"></a>
## SPLIT_PART

<a id="a74fe833f0d051c2"></a>
### Syntax

```
SPLIT_PART( string, delimiter, field )
```

<a id="8a5b552024d7dcbc"></a>
### Description

It returns a character string of the field by specifying a character as delimiter within a string.

The data type of string argument and delimiter argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

The field argument can be a numeric data type.

If any of string, delimiter, field is NULL, the result is also NULL.  
The value of field should be a numeric value above 1, and if it is 0 or a negative number, an error is returned.

The following table describes the result types.

**Result type of SPLIT_PART**

<a id="7ffa3e73567d2a17"></a>
| string type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="7aafd6a52daea2bc"></a>
### Example

```
gSQL> SELECT SPLIT_PART( 'AB;CD;EF;GH', ';', 3  ) AS RESULT FROM DUAL;
RESULT
------
EF    
1 row selected.
```

<a id="da1f1343e315a450"></a>
## SQRT

<a id="26b2f1f67002c099"></a>
### Syntax

```
SQRT( num )
```

<a id="996156b0dfe128a2"></a>
### Description

It returns the square root of num.

The num argument can be a numeric type, and it should not be a negative number, but above 0.  
If the num argument is NULL, then NULL is returned.

<a id="c90651f6df9d1c32"></a>
### Example

```
gSQL> SELECT SQRT( 9 ) AS RESULT FROM DUAL;
RESULT
------
     3
1 row selected.
```

<a id="72245005377e3513"></a>
## STATEMENT_DATE

<a id="eae0c3fa857c864c"></a>
### Syntax

```
STATEMENT_DATE()
CURRENT_DATE [()]
```

<a id="34eacedb92266423"></a>
### Description

The current date(DATE type) value is obtained.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="677a8e13acc63442"></a>
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

<a id="53c3b60ca5d08a42"></a>
## STATEMENT_LOCALTIME

<a id="f5be88d2e4444d58"></a>
### Syntax

```
STATEMENT_LOCALTIME()
LOCALTIME [()]
```

<a id="0f45c5ced400ee94"></a>
### Description

The current TIME WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.  
• TATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="2d1d79826ad6cb46"></a>
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

<a id="5583fa5e4241b577"></a>
## STATEMENT_LOCALTIMESTAMP

<a id="0c6623087e6e2374"></a>
### Syntax

```
STATEMENT_LOCALTIMESTAMP()
LOCALTIMESTAMP [()]
```

<a id="02fc8990b42e1bdf"></a>
### Description

The current TIMESTAMP WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_LOCALTIMESTAMP(): All timestamp values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="1f96e8bdca47c3ce"></a>
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

<a id="2ffed6aa412db546"></a>
## STATEMENT_TIME

<a id="7ea98d1a7e7a0403"></a>
### Syntax

```
STATEMENT_TIME()
CURRENT_TIME [()]
```

<a id="a952cc021c898b50"></a>
### Description

The current TIME WITH TIME ZONE type value is obtained.

CURRENT_TIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• STATEMENT_TIME(): All time values in an SQL statement are same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="52e4aec66130a5a2"></a>
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

<a id="ef98a5f0a9976e38"></a>
## STATEMENT_TIMESTAMP

<a id="fcd3f3ed9c05ae7e"></a>
### Syntax

```
STATEMENT_TIMESTAMP()
CURRENT_TIMESTAMP [()]
```

<a id="23f891c7a0d1d2f5"></a>
### Description

The current TIMESTAMP WITH TIME ZONE type value is obtained.

CURRENT_TIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_TIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_TIMESTAMP(): All timestamp values in an SQL statement are same.  
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="c61f4294cba7d61e"></a>
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

<a id="81bbdc72826b938f"></a>
## STATEMENT_VIEW_SCN

<a id="06fab86563c8e280"></a>
### Syntax

```
STATEMENT_VIEW_SCN()
```

<a id="ecded1d21c28bda5"></a>
### Description

It obtains VIEW SCN of the current STATEMENT.

<a id="5cb993e4ae8ebca5"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN() FROM dual;

STATEMENT_VIEW_SCN()
--------------------
17697.658.17880     

1 row selected.
```

<a id="e35977087ac568f8"></a>
## STATEMENT_VIEW_SCN_DCN

<a id="156d91d226e2a3f7"></a>
### Syntax

```
STATEMENT_VIEW_SCN_DCN()
```

<a id="b1ad899c35d38744"></a>
### Description

It obtains the Domain Change Number (DCN) value of the current STATEMENT's VIEW SCN.

<a id="5cf6c9c2e725e12a"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_DCN() FROM dual;

STATEMENT_VIEW_SCN_DCN()
------------------------
                     658

1 row selected.
```

<a id="d3ed4b80d26c10d0"></a>
## STATEMENT_VIEW_SCN_GCN

<a id="0bcd6beae11e1f3c"></a>
### Syntax

```
STATEMENT_VIEW_SCN_GCN()
```

<a id="a983b61c50e0d8f4"></a>
### Description

It obtains the Global Change Number (GCN) value of the current STATEMENT's VIEW SCN.

<a id="3ae80fc5b6ddec60"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_GCN() FROM dual;

STATEMENT_VIEW_SCN_GCN()
------------------------
                   17697

1 row selected.
```

<a id="f9bee7a7e9da0997"></a>
## STATEMENT_VIEW_SCN_LCN

<a id="c756e772fe3fe412"></a>
### Syntax

```
STATEMENT_VIEW_SCN_LCN()
```

<a id="8cb56f3376334544"></a>
### Description

It obtains the Local Change Number (LCN) value of the current STATEMENT's VIEW SCN.

<a id="3ce3bf5aa371e322"></a>
### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_LCN() FROM dual;

STATEMENT_VIEW_SCN_LCN()
------------------------
                   17880

1 row selected.
```

<a id="c73c3f8884cc1c52"></a>
## STDDEV

<a id="212e455e894a1df3"></a>
### Syntax

```
STDDEV( [ ALL | DISTINCT ] expr )
```

<a id="c8f6fdd6d0512a39"></a>
### Description

It is an aggregation function, and it obtains the standard deviation of an expr set.

If ALL is specified, this function is performed for all values. If DISTINCT is specified, this function is performed for the values of which the duplicates were deleted from. If it is not specified, it is processed as if ALL is apecified.

If the number of expr sets except for NULL after deleting the duplicates by using DISTINCT is one, then it returns 0 like as [VARIANCE](#aece5460fa03ff1f).

The following table describes the arguments and result types.

**Argument and result type of STDDEV**

<a id="43d539e1c455f09c"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

GOLDILOCKS gets the standard deviation as follows.  
　• If the number of expr sets is 1, then it returns 0.  
　• If the number of expr sets is bigger than 1, it returns the value of [STDDEV_SAMP( expr )](#528412563eda78a1).

> The standard deviation is a positive square root of a variance, and it is obtained calculating the square root of the variance. In other words, the STDDEV function is as same as the square root of [VARIANCE](#aece5460fa03ff1f) function.  
>   
> STDDEV( [ ALL ] expr )  
>  = SQRT( VARIANCE( [ ALL ] expr ) )  
>   
> STDDEV( DISTINCT expr )  
>  = SQRT( VARIANCE( DISTINCT expr ) )

<a id="d79010946cd8add7"></a>
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

<a id="c72f226331baf318"></a>
## STDDEV() OVER

<a id="35f6e9a5aaae0a75"></a>
### Syntax

```
STDDEV ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="ece5a2aafa622c05"></a>
### Description

Window function STDDEV calculates the standard deviation of expr.   
If the number of expr except for NULL is one, then it returns 0 as a result.

<a id="ac4787e390e8b292"></a>
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

<a id="fb8d9eee7b4e7dab"></a>
## STDDEV_POP

<a id="3305a0c0db070d8a"></a>
### Syntax

```
STDDEV_POP( expr )
```

<a id="8a89ef12118f31b2"></a>
### Description

It is an aggregation function, and it obtains the population standard deviation of an expr set.   
If the number of expr sets except for NULL is one, then it returns 0.

The following table describes the arguments and result types.

**Argument and result type of STDDEV_POP**

<a id="4e86ebde56bf11a1"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The population standard deviation is a positive square root of a population variance, and it is obtained by calculating the square root of the population variance. In other words, the STDDEV_POP function is as same as the square root of [VAR_POP](#c0a67a48fe1cb8c7) function.  
>   
> STDDEV_POP( expr )  
>  = SQRT( VAR_POP( expr ) )

<a id="31a88ccc235f7b08"></a>
### Example

```
gSQL> SELECT STDDEV_POP(c1) FROM t1;

 STDDEV_POP(C1)
---------------
10.283968105746

1 row selected.
```

<a id="ec58e43f967f0194"></a>
## STDDEV_POP() OVER

<a id="2369a213bc36e9ae"></a>
### Syntax

```
STDDEV_POP ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="e50e7298278ec276"></a>
### Description

Window function STDDEV_POP calculates the population standard deviation of expr.   
If the number of expr except for NULL is one, then it returns 0 as a result.

<a id="36a215aebb4e4e73"></a>
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

<a id="528412563eda78a1"></a>
## STDDEV_SAMP

<a id="165ca033c9eef449"></a>
### Syntax

```
STDDEV_SAMP( expr )
```

<a id="f6be1a29b722a3e1"></a>
### Description

It is an aggregation function, and it obtains the sample standard deviation of an expr set. If the number of expr sets except for NULL is one, then it returns NULL.

The following table describes the arguments and result types.

**Argument and result type of STDDEV_SAMP**

<a id="80d984b7dbc7ff2f"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The sample standard deviation is a positive square root of a sample variance, and it is obtained by calculating the square root of the sample variance. In other words, the STDDEV_SAMP function is as same as the square root of [VAR_SAMP](#bb45fcc7dcf1c737) function.  
>   
> STDDEV_SAMP( expr )  
>  = SQRT( VAR_SAMP( expr ) )

<a id="a18b7ca86f1bc8f2"></a>
### Example

```
gSQL> SELECT STDDEV_SAMP(c1) FROM t1;

 STDDEV_SAMP(C1)
----------------
11.4978258814438

1 row selected.
```

<a id="de4132b2ac197f6c"></a>
## STDDEV_SAMP() OVER

<a id="d47c6836230ddb05"></a>
### Syntax

```
STDDEV_SAMP ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="00725d06e37c7819"></a>
### Description

Window function STDDEV_SAMP calculates the sample standard deviation of expr.   
If the number of expr except for NULL is one, then it returns NULL as a result.

<a id="7c8208bf83537c22"></a>
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

<a id="6afb9e95275724c3"></a>
## STRING_AGG() OVER

<a id="be9fdf89887978fc"></a>
### Syntax

```
STRING_AGG( str [, delimiter] ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="dfc33e0426b08f70"></a>
### Description

Window function STRING_AGG connects str according to the function's execution range defined in OVER clause.

If str is NULL, then it is excluded.

A delimiter is str connection delimiter, and if it is omitted the default value is NULL.

str can be a character string or a binary string.   
If str is a character string, then the result type is varchar.   
If str is a binary string, then the result type is varbinary.

<a id="ce66dc1135095735"></a>
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

<a id="886c495b271eb0db"></a>
## SUBSTR

<a id="12a732f16f859f40"></a>
### Syntax

```
SUBSTR( str FROM start_position [ FOR string_length ] )
SUBSTR( str, start_position [ , string_length ] )
```

<a id="3b39f00b41e82752"></a>
### Description

It is an alias of [SUBSTRING](#92dc347da526af32).

<a id="67e4d6db1c597e22"></a>
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

<a id="0fa2064ee0a68d30"></a>
## SUBSTRB

<a id="f408627fe15b81a4"></a>
### Syntax

```
SUBSTRB( str, start_position [ , string_length ] )
```

<a id="111776186aec6d66"></a>
### Description

It extracts characters which are within string_length range from start_position, and returns the result for str.

This function is as same as [SUBSTRING](#92dc347da526af32) function, except that start_position and string_length of the SUBSTR function are calculated in byte units.

<a id="e0273321a45fae90"></a>
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

<a id="92dc347da526af32"></a>
## SUBSTRING

<a id="7722ad743f84b757"></a>
### Syntax

```
SUBSTRING( str FROM start_position [ FOR string_length ] )  
SUBSTRING( str, start_position [ , string_length ] )
```

<a id="4aee0a1ed723cc75"></a>
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

It is an alias of [SUBSTR](#886c495b271eb0db).  
For more information, refer to [SUBSTRB](#0fa2064ee0a68d30).

The following table describes the result types.

**Result type of SUBSTRING**

<a id="35f10c077f8e89f5"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="b4c205c581216738"></a>
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

<a id="ecc19ff5aa9f5e17"></a>
## SUM

<a id="9e4f138a2a6af020"></a>
### Syntax

```
SUM( [ ALL | DISTINCT ] expr )
```

<a id="2b2490f1568e04d6"></a>
### Description

It is an aggregate function and the sum of expr value is obtained.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

<a id="1311b24187f9e435"></a>
### Example

```
gSQL> SELECT SUM(c1) FROM t1;

SUM(C1)
-------
      6

1 row selected.
```

<a id="a3a8a6b2497fd1c2"></a>
## SUM() OVER

<a id="488ce7dd297b3252"></a>
### Syntax

```
SUM ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="77a4b43316b8f483"></a>
### Description

Window function SUM calculates the sum of expr value.  
NULL is excluded from the calculation.

<a id="02c7a4271afffe12"></a>
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

<a id="1c9c8cb0e5a7b7f2"></a>
## SYSDATE

<a id="865f0a7b3fb80a0a"></a>
### Syntax

```
SYSDATE
```

<a id="e9eea91e51e8163d"></a>
### Description

It obtains the current DATE type value based on the OS time of the database server.

<a id="905b6b08b943b12d"></a>
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

<a id="06217bd928ec2244"></a>
## SYS_EXTRACT_UTC

<a id="33847496f9a527c7"></a>
### Syntax

```
SYS_EXTRACT_UTC( datetime_with_timezone )
```

<a id="07332c123b50521b"></a>
### Description

It returns the UTC (Coordinated Universal Time—formerly Greenwich Mean Time) value.  
If the timezone is not specified, it is calculated as session time zone.

The data type of an input argument can be time, time with time zone, timestamp, timestamp with time zone.  
The result type is time or timestamp type.

<a id="21a63ee86cf221ff"></a>
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

<a id="c3006d12a5a804cd"></a>
## SYSTIME

<a id="eaa3fc59e8975ca8"></a>
### Syntax

```
SYSTIME
```

<a id="10fa2f11ca722242"></a>
### Description

It obtains the current TIME WITH TIME ZONE type value based on the OS time of the database server.

<a id="220e8e15a14de66f"></a>
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

<a id="1e392924dc96ef60"></a>
## SYSTIMESTAMP

<a id="e56ba2aa28577071"></a>
### Syntax

```
SYSTIMESTAMP
```

<a id="9704939653e4e3ca"></a>
### Description

It obtains the current TIMESTAMP WITH TIME ZONE type value based on the OS time of the database server.

<a id="042b2c6cb5214653"></a>
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

<a id="4cd5bf99ebf3d145"></a>
## TAN

<a id="02a146ca06e28d42"></a>
### Syntax

```
TAN( num )
```

<a id="96b924691f626c27"></a>
### Description

It returns the tangent value of num in radians unit.  
If num is NULL, then NULL is returned.

<a id="93d8cfeae2553c32"></a>
### Example

```
gSQL> SELECT TAN( 1 ) AS RESULT FROM DUAL;
         RESULT
---------------
1.5574077246549
1 row selected.
```

<a id="9042ca2ffd6f273a"></a>
## TO_BASE64

<a id="24a89f7151833116"></a>
### Syntax

```
TO_BASE64( str )
```

<a id="44f4ee204375374a"></a>
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

For more information, refer to [FROM_BASE64](#8e25e052ba17c43a).

<a id="4058481638b51687"></a>
### Example

```
gSQL> SELECT TO_BASE64( 'abc' ), TO_BASE64( 'abcd' ) FROM DUAL;

TO_BASE64( 'abc' ) TO_BASE64( 'abcd' )
------------------ -------------------
YWJj               YWJjZA==           
1 row selected.
```

<a id="24c99d6f3463acf6"></a>
## TO_CHAR( datetime )

<a id="9f2e855a648875de"></a>
### Syntax

```
TO_CHAR( datetime [, fmt ] )
```

<a id="4ee7ad75b402b8f6"></a>
### Description

It converts datetime to a string in the specified fmt format, and returns the result.

The datetime argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL.   
The fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING.  

If any argument is NULL, then NULL is returned.

If fmt is omitted, it follows the default format.  
• DATE: Refer to [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#7ea8c558693ab9b8).  
• TIMESTAMP: Refer to [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#f745ba729e1e8deb).  
• TIMESTAMP WITH TIME ZONE: Refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#226a187670420c2f).  
• TIME: Refer to [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#fff3ca3eeeea7a35).  
• TIME WITH TIME ZONE: Refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#6a87f7e07e80669e).

If the data type of the datetime argument is INTERVAL, it is converted to a string then returned regardless of fmt.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#b7a47f2ef79b2b26).

The result type is CHARACTER VARYING.

<a id="3da623ee2fb2a31d"></a>
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

<a id="d69061b89662a768"></a>
## TO_CHAR( number )

<a id="4160212e5c69b250"></a>
### Syntax

```
TO_CHAR( number [, fmt ] )
```

<a id="b3af8944c2020f18"></a>
### Description

It converts the number to a string in the specified fmt format, and returns the result.

The number argument can be a numeric data type.  
The fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING.  
If fmt is omitted, all significant digits are converted to the string and returned.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#38636b5b44a04ac0).  
If any input argument is NULL, then NULL is returned.

The result type is CHARACTER VARYING.

<a id="aa154478874f829b"></a>
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

<a id="5219142a4793653b"></a>
## TO_DATE

<a id="9618fccf76fe6a75"></a>
### Syntax

```
TO_DATE( str [, fmt ] )
```

<a id="e4c5aee0da374cd3"></a>
### Description

It converts the str string in the specified fmt format to DATE type, and returns the result.

The str argument and fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.  
If fmt is omitted, the default format is NLS_DATE_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#b7a47f2ef79b2b26).  
For more information, refer to [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#7ea8c558693ab9b8).  

If either str or fmt is NULL, then NULL is returned.

The result type is DATE.

<a id="ea6db333c083f286"></a>
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

<a id="4e932440d0c38f36"></a>
## TO_NATIVE_BIGINT

<a id="6095f4e0d6315e7a"></a>
### Syntax

```
TO_NATIVE_BIGINT( str [, fmt ] )
```

<a id="a3d74c9dca7a0044"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_BIGINT type, and returns the result.

The str argument and fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL,  the result is also NULL.    
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#38636b5b44a04ac0).

The result type is NATIVE_BIGINT.

<a id="541565110ee572df"></a>
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

<a id="54731f33ec124462"></a>
## TO_NATIVE_DOUBLE

<a id="0872a3f51e7a14ea"></a>
### Syntax

```
TO_NATIVE_DOUBLE( str [, fmt ] )
```

<a id="3411343a5df1710f"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_DOUBLE type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#38636b5b44a04ac0).

The result type is NATIVE_DOUBLE.

<a id="737d064a09a3bb7c"></a>
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

<a id="8e984895b0d5abb0"></a>
## TO_NATIVE_INTEGER

<a id="43ffc24683887898"></a>
### Syntax

```
TO_NATIVE_INTEGER( str [, fmt ] )
```

<a id="16f27bcc4e9439ad"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_INTEGER type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#38636b5b44a04ac0).

The result type is NATIVE_INTEGER.

<a id="5639035cef089f49"></a>
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

<a id="ae266ee6179f808b"></a>
## TO_NATIVE_REAL

<a id="05ac89bb110b37f8"></a>
### Syntax

```
TO_NATIVE_REAL( str [, fmt ] )
```

<a id="684884b17604578d"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_REAL type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#38636b5b44a04ac0).

The result type is NATIVE_REAL.

<a id="ec778ecd9ac94763"></a>
### Example

```
gSQL> SELECT TO_NATIVE_REAL( '123.45' ) AS RESULT1, 
             TO_NATIVE_REAL( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
```

<a id="898732df4fa8a0cf"></a>
## TO_NATIVE_SMALLINT

<a id="5c12b1c1ea717f6f"></a>
### Syntax

```
TO_NATIVE_SMALLINT( str [, fmt ] )
```

<a id="5e70a653e49c2e33"></a>
### Description

It converts the str string in the specified fmt format to NATIVE_SMALLINT type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#38636b5b44a04ac0).

The result type is NATIVE_SMALLINT.

<a id="c5c52aa862156031"></a>
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

<a id="f4c5f4089516a8f7"></a>
## TO_NUMBER

<a id="1dbad0e7c85cae08"></a>
### Syntax

```
TO_NUMBER( str [, fmt] )
```

<a id="e26fc0fe675bf577"></a>
### Description

It converts the str string in the specified fmt format to NUMBER type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](11-sql-elements.md#38636b5b44a04ac0).

The result type is NUMBER.

<a id="3734b82cb5b46a0a"></a>
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

<a id="9dbf37dc5504a5f2"></a>
## TO_TIME

<a id="e8f53f0770c73ed7"></a>
### Syntax

```
TO_TIME( str [, fmt ] )
```

<a id="429dbbdcee9d81a6"></a>
### Description

It converts the str string in the specified fmt format to TIME type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIME_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#b7a47f2ef79b2b26).  
For more information, refer to [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#fff3ca3eeeea7a35).  

If either str or fmt is NULL, then NULL is returned.

The result type is TIME.

<a id="76716ec7e15e4bc6"></a>
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

<a id="8cd8fe4291df2b52"></a>
## TO_TIME_TZ

<a id="2e2c58e7635779d7"></a>
### Syntax

```
TO_TIME_TZ( str [, fmt ] )
```

<a id="b5b40cea14a35a07"></a>
### Description

It is an alias of [TO_TIME_WITH_TIME_ZONE](#a7774652486ae49f).  
For more information, refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#6a87f7e07e80669e).

<a id="7a400631f8f8ff3a"></a>
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

<a id="a7774652486ae49f"></a>
## TO_TIME_WITH_TIME_ZONE

<a id="30925f78e77e0d9e"></a>
### Syntax

```
TO_TIME_WITH_TIME_ZONE( str [, fmt ] )
TO_TIME_TZ( str [, fmt ] )
```

<a id="665f2fa1e6d6cf01"></a>
### Description

It converts the str string in the specified fmt format to TIME WITH TIME ZONE type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIME_WITH_TIME_ZONE_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#b7a47f2ef79b2b26)  
For more information, refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#6a87f7e07e80669e).  

If either str or fmt is NULL, then NULL is returned.

It is an alias of [TO_TIME_TZ](#8cd8fe4291df2b52).

The result type is TIME WITH TIME ZONE.

<a id="c6aabb0f2d24fa2c"></a>
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

<a id="4343ab929dac120a"></a>
## TO_TIMESTAMP

<a id="ee8f0d647a360aeb"></a>
### Syntax

```
TO_TIMESTAMP( str [, fmt ] )
```

<a id="d484aaf1e4dd4cf0"></a>
### Description

It converts the str string in the specified fmt format to TIMESTAMP type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIMESTAMP_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](11-sql-elements.md#b7a47f2ef79b2b26).  
For more information, refer to [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#f745ba729e1e8deb).  

If either str or fmt is NULL, then NULL is returned.

The result type is TIMESTAMP.

<a id="d44fbb8419a48946"></a>
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

<a id="a94ee05b9240c010"></a>
## TO_TIMESTAMP_TZ

<a id="2bdd014b940319e6"></a>
### Syntax

```
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="04ee2e165d2d8105"></a>
### Description

It is an alias of [TO_TIMESTAMP_WITH_TIME_ZONE](#19ac77096078990f).  
For more information, refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#226a187670420c2f).

<a id="5a63a4f688d58e17"></a>
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

<a id="19ac77096078990f"></a>
## TO_TIMESTAMP_WITH_TIME_ZONE

<a id="3d33b58da1253291"></a>
### Syntax

```
TO_TIMESTAMP_WITH_TIME_ZONE( str [, fmt ] )
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="916eff8cb29b4b79"></a>
### Description

It converts the str string in the specified fmt format to TIMESTAMP WITH TIME ZONE type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to  [Datetime Format String](11-sql-elements.md#b7a47f2ef79b2b26).  
For more information, refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#226a187670420c2f).  

If either str or fmt is NULL, then NULL is returned.

It is an alias of [TO_TIMESTAMP_TZ](#a94ee05b9240c010).

The result type is TIMESTAMP WITH TIME ZONE .

<a id="404e8365bfb7763f"></a>
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

<a id="64c95a5834e1602a"></a>
## TRANSACTION_DATE

<a id="594b93e3db5c9b8a"></a>
### Syntax

```
TRANSACTION_DATE()
```

<a id="9d27832ce76d9b97"></a>
### Description

It obtains the current date (DATE type) value based on the session time.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="7c6e9300da62fce4"></a>
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

<a id="fe7eedefbda66b67"></a>
## TRANSACTION_LOCALTIME

<a id="e031b872411597fb"></a>
### Syntax

```
TRANSACTION_LOCALTIME()
```

<a id="f74fbcdd7855df49"></a>
### Description

It obtains the current TIME WITHOUT TIME ZONE type value based on the session time.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.   
• STATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="b52d6c857b1a5205"></a>
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

<a id="71272c35f4421ff2"></a>
## TRANSACTION_LOCALTIMESTAMP

<a id="decda52b9869d1a6"></a>
### Syntax

```
TRANSACTION_LOCALTIMESTAMP()
```

<a id="eae57736f73994cd"></a>
### Description

It obtains the current TIMESTAMP WITHOUT TIME ZONE type value based on the session time.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_LOCALTIMESTAMP(): All timestamp values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="b7d8d62f650379e7"></a>
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

<a id="c4743da8577b330c"></a>
## TRANSACTION_TIME

<a id="3ac55c10999dc24c"></a>
### Syntax

```
TRANSACTION_TIME()
```

<a id="9dea314ddbf4802a"></a>
### Description

It obtains the current TIME WITH TIME ZONE type value based on the session time.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• STATEMENT_TIME(): All time values in an SQL statement are same.   
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="5d2df1cee12492e5"></a>
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

<a id="8919352379027e52"></a>
## TRANSACTION_TIMESTAMP

<a id="21ad3bf340d6e231"></a>
### Syntax

```
TRANSACTION_TIMESTAMP()
```

<a id="6c8a5e6459fcb6fa"></a>
### Description

It obtains the current TIMESTAMP WITH TIME ZONE type value based on the session time.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_TIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_TIMESTAMP(): All timestamp values in an SQL statement are same.   
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="f9cdc85df093fcde"></a>
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

<a id="2ea59d7dc8a38b63"></a>
## TRANSLATE

<a id="39606055edccbfed"></a>
### Syntax

```
TRANSLATE( string, from, to )
```

<a id="cf16400badf7bd89"></a>
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

<a id="2083dcdab1a6f7b6"></a>
| string type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="75d825f76afb3b4c"></a>
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

<a id="d56383e8219aa445"></a>
## TRIM

<a id="e91d8a463614372a"></a>
### Syntax

```
TRIM([ [ LEADING | TRAILING | BOTH ]  [trim_character] FROM ] trim_source)
```

<a id="8ce1e00c18cf6913"></a>
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

<a id="3693f6f584cbf265"></a>
| trim_character, trim_source type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="27bf270a07a1782f"></a>
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

<a id="732613ba550860fa"></a>
## TRUNC( number )

<a id="9c2076336e455379"></a>
### Syntax

```
TRUNC( num [ , scale ] )
```

<a id="3e437ecaaded6b54"></a>
### Description

It truncates the num based on scale, then returns the result.

The num argument and scale argument can be a numeric type.  
If either the num argument or the scale argument is NULL, then NULL is returned.

If scale is omitted, the scale becomes 0, and it is executed as same as TRUNC( num, 0 ).  
If scale is a positive number, it is truncated based on the number of right digit of the decimal point.  
If scale is a negative number, it is truncated off based on the number of left digit of the decimal point.

<a id="2a82dd44926ce332"></a>
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

<a id="adc1e379c8ac0216"></a>
## TRUNC( date )

<a id="502e321d75845a08"></a>
### Syntax

```
TRUNC( date [ , fmt ] )
```

<a id="a8cbc3dce1639b62"></a>
### Description

It truncates the date in a specified fmt unit, and returns the result.

The date argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.  
The fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING.  
If either date argument or fmt argument is NULL, then NULL is returned.

The result type is always DATE regardless of the input date type.

If fmt is omitted, the default is *DAY*, and the available format string is described in the following table.

**Available format string in fmt**

<a id="850dbd538e336d1c"></a>
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

<a id="4b04d64ce1a54a55"></a>
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

<a id="51fcdd62ab430f53"></a>
## UPPER

<a id="7080dd2e276ca45f"></a>
### Syntax

```
UPPER( str )
```

<a id="9bf35f176ef80fce"></a>
### Description

It returns the uppercase characters of str.

The str argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.  
If str is NULL, the result is NULL.

The return type is as same as the str argument type.

<a id="5352baadf3e80b18"></a>
### Example

```
gSQL> SELECT UPPER( 'spring' ) AS RESULT FROM DUAL;
RESULT
------
SPRING
1 row selected.
```

<a id="c1fe74c2be5e0dce"></a>
## UNHEX

<a id="57a4d900d4394bc0"></a>
### Syntax

```
UNHEX( str )
```

<a id="a19f616ca0e1d608"></a>
### Description

str argument is a hexadecimal character and this function represents it as each byte and returns it as a binary string.

The input argument can be a character type such as CHARACTER VARYING, CHARACTER LONG VARYING. The result type is a binary character type such as BINARY VARYING or BINARY LONG VARYING.

If str is NULL, then the result value is also NULL.  
If str includes a character which does not belong to the hexadecimal range, then it returns an error.

For more information, refer to [HEX](#ee8a91a688aadcab).

<a id="9a83ec7a7453f2ac"></a>
### Example

```
gSQL> SELECT UNHEX( HEX( 'abc' ) ) FROM DUAL;
UNHEX( HEX( 'abc' ) )
---------------------
616263               
1 row selected.
```

<a id="1b2e77f74661483e"></a>
## UNHEX_TO_CHARSTR

<a id="1ca07e73983fbf42"></a>
### Syntax

```
UNHEX_TO_CHARSTR( str )
```

<a id="03f5295fc44c851f"></a>
### Description

str argument is a hexadecimal character and this function represents it as each byte and returns it as a character string.

The input argument can be a character type such as CHARACTER VARYING, CHARACTER LONG VARYING. The result type is a character type such as CHARACTER VARYING, CHARACTER LONG VARYING.

If str is NULL, then the result value is also NULL.  
If str includes a character which does not belong to the hexadecimal range, then it returns an error.

For more information, refer to [HEX](#ee8a91a688aadcab), [UNHEX](#c1fe74c2be5e0dce).

<a id="8185108fc43e988e"></a>
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

<a id="eebb6e9fa249c7f5"></a>
## USER_ID

<a id="189e8bfc7cb26c96"></a>
### Syntax

```
USER_ID ()
```

<a id="9e54d089bd7bdb64"></a>
### Description

It obtains the current user's number ID.

> In cluster system, the value may vary depending on the connected server.  
> It is recommended to use [CURRENT_USER](#222009ae9a551fee) function obtaining the current username.

<a id="aa1076a84a5c164c"></a>
### Example

```
% gsql test test

gSQL> SELECT USER_ID() FROM dual;

USER_ID()
---------
        6

1 row selected.
```

<a id="f0e0cf0916b60396"></a>
## UUID

<a id="663879f6481367c9"></a>
### Syntax

```
UUID()
```

<a id="fef944ecd2a070d6"></a>
### Description

It creates the universal unique identifier, then returns it.   
The return type is VARBINARY type, and it internally consists of 16 bytes.

<a id="07a27d4f82ed4c1c"></a>
### Example

```
gSQL> SELECT HEX( UUID() ) FROM DUAL;
HEX( UUID() )                   
--------------------------------
E6F0A5C2387511E8B95259E479C2FD50
1 row selected.
```

<a id="c0a67a48fe1cb8c7"></a>
## VAR_POP

<a id="2778948d41809b44"></a>
### Syntax

```
VAR_POP( expr )
```

<a id="3e4d7e4a9ea0c70b"></a>
### Description

It is an aggregation function, and it obtains the population variance of an expr set. If the number of expr sets except for NULL is one, then it returns 0.

The following table describes the arguments and result types.

**Argument and result type of VAR_POP**

<a id="64fe257333c0271f"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The population variance is a variance of the population (entire) group, and it is the average of the square value of deviation. In other words, it is calculated by extracting the population average (the entire average) from each value of the data, and squaring each value, then adding them together and dividing them by the number of datas in the population group.   
> This value is used to figure out how far each value is from the average value.

For more information, refer to [STDDEV_POP](#fb8d9eee7b4e7dab).

<a id="62abf81e2d239360"></a>
### Example

```
gSQL> SELECT VAR_POP(c1) FROM t1;

VAR_POP(C1)
-----------
     105.76

1 row selected.
```

<a id="a93fdf603939c4e1"></a>
## VAR_POP() OVER

<a id="450c6252cab3e7c8"></a>
### Syntax

```
VAR_POP ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="a3828b6aff2e57b9"></a>
### Description

Window function VAR_POP calculates the population variance of expr.   
If the number of expr except for NULL is one, then it returns 0 as a result.

<a id="9df0fbd6dd1e5bf5"></a>
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

<a id="bb45fcc7dcf1c737"></a>
## VAR_SAMP

<a id="aec2ff4a6392a821"></a>
### Syntax

```
VAR_SAMP( expr )
```

<a id="d1baa17f2a2d207c"></a>
### Description

It is an aggregation function, and it obtains the sample variance of an expr set. If the number of expr sets except for NULL is one, then it returns NULL.

The following table describes the arguments and result types.

**Argument and result type of VAR_SAMP**

<a id="5dfff027ed9023ca"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> Unlike the population variance dealing with the population (entire) group, the sample variance deals with the average and deviation of extracted samples. In other words, it is calculated by extracting the sample average from each value of the data, and squaring each value, then adding them together and dividing them by the number of datas in the population group minus 1.   
> This value is used to figure out the variance of the population group.

For more information, refer to [STDDEV_SAMP](#528412563eda78a1).

<a id="1c26d9494cfa5278"></a>
### Example

```
gSQL> SELECT VAR_SAMP(c1) FROM t1;

VAR_SAMP(C1)
------------
       132.2

1 row selected.
```

<a id="8fd647cd7085750a"></a>
## VAR_SAMP() OVER

<a id="445dfdb39406126d"></a>
### Syntax

```
VAR_SAMP ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="bd8742b140aa766f"></a>
### Description

Window function VAR_SAMP calculates the sample variance of expr.   
If the number of expr except for NULL is one, then it returns NULL as a result.

<a id="e464f2cae8c9dd77"></a>
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

<a id="aece5460fa03ff1f"></a>
## VARIANCE

<a id="63a675eae67f51cc"></a>
### Syntax

```
VARIANCE( [ ALL | DISTINCT ] expr )
```

<a id="64015970d2dbe8d0"></a>
### Description

It is an aggregation function, and it obtains the variance of an expr set.

If ALL is specified, this function is performed for all values. If DISTINCT is specified, this function is performed for the values of which the duplicates were deleted from. If it is not specified, it is processed as if ALL is apecified.

If the number of expr sets except for NULL after deleting the duplicates by using DISTINCT is one, then it returns 0.

The following table describes the arguments and result types.

**Argument and result type of VARIANCE**

<a id="903a79c9e9905ce4"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> GOLDILOCKS gets the variance as follows.  
> • If the number of expr sets is 1, then it returns 0.  
> • If the number of expr sets is bigger than 1, it returns the value of [STDDEV_SAMP (expr)](#528412563eda78a1).

For more information, refer to [STDDEV](#c73c3f8884cc1c52).

<a id="c5a273728acf43c9"></a>
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

<a id="76a32c257963857c"></a>
## VARIANCE() OVER

<a id="c60fb8182f5642b6"></a>
### Syntax

```
VARIANCE ( expr ) OVER < window name or specification >
```

For more information about &lt; window name or specification &gt;, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

<a id="41abc7d521fdc9f8"></a>
### Description

Window function VARIANCE calculates the variance of expr.   
If the number of expr except for NULL is one, then it returns 0 as a result.

<a id="3620133d0792f1ae"></a>
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

<a id="4c4cf16c3fb15e3f"></a>
## VERSION

<a id="d98390c968e0aad5"></a>
### Syntax

```
VERSION()
```

<a id="ad0317109a5b5ec1"></a>
### Description

It obtains the product's version string.

<a id="da3cb2e966e56dd6"></a>
### Example

```
gSQL> SELECT VERSION() FROM dual;

VERSION()                            
-------------------------------------
Release Name.X.X.X revision(XXXXX)

1 row selected.
```

<a id="9f15275ef5f64ced"></a>
## WIDTH_BUCKET

<a id="280e177fd0640165"></a>
### Syntax

```
WIDTH_BUCKET( num, min, max, cnt )
```

<a id="fa252112858f7595"></a>
### Description

It creates a section of the same width as cnt within a range between specified min and max, and it returns the section location in which the num is located.

The data type of num argument, min argument, max argument and cnt argument can be a numeric data type.

min, max means the range for the section. If the min value is equal to the max value, an error is returned.  
cnt means the number of sections. The cnt value should be a positive number. If the cnt value is 0 or a negative number, an error is returned.   
The section's location is numbered from one.

If any of num, min, max, cnt is NULL, the result is also NULL.

<a id="06ec37c2e1e1066e"></a>
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
