<a id="a9294d7e7997ebf8"></a>

# 11. SQL Elements

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/a9294d7e7997ebf8)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 10. Server Property](../part-02-administration-manual/10-server-property.md) · [Table of contents](../README.md) · [12. SQL Languages →](12-sql-languages.md)

<a id="1ee62551c81f1a36"></a>
## Syntax Elements

<a id="7dd57524acbd452f"></a>
### Identifiers

Identifier is divided into an ordinary identifier and a delimited identifier.  
An ordinary identifier consists of letters or a combination of letters and numbers, and it is used by internally substituting all characters to uppercase letters. Therefore, an ordinary identifier is not case-sensitive.

The following is an example of an ordinary identifier.

```
GOLDILOCKS
GoldiLocks
```

A delimited identifier consists of letters or a combination of letters and numbers enclosed in double quotes ("). All the characters are used as internally described. Therefore, a delimited identifier is case-sensitive.

The following is an example of a delimited identifier.

```
"GOLDILOCKS"
"GoldiLocks"
```

<a id="5f90e3f36ae1d537"></a>
### Literals

Literals mean representation of non-null value.

<a id="47e7d67dec617698"></a>
#### Text Literals

Text literals mean representation of strings and binary strings.

Use single quote (') at the beginning and end of a string to write string of text literals.  
Not only the double quotes (") string but also all strings except for the single quote (') string can be written within a single quote (').   
Use a single quote twice without white spaces in between to write a single quote (') in a string.   
A maximum of 4000 characters can be written in a string.

The followings are examples of text literals for a string.

```
'GOLDILOCKS'
'Sunje''s DBMS'
```

A binary string of text literals is a string of hexadecimal numbers which starts with x'(X') and ends with '. Only the characters corresponding to 0 ~ 9, A (a) ~ F (f) can be written in each position of a hexadecimal string. The length of a hexadecimal string should always be an even number because its two digits mean one byte. A maximum of 4,000 characters can be written in a binary string.

The followings are examples of text literals for a binary string.

```
x'001f'
X'FF0A'
x'aF37BBc013'
```

<a id="c05541f4b26b69c5"></a>
#### Numeric Literals

Numeric literals mean literals of numeric type, and integers or the number with decimal point can be written. The syntax for numeric literals is as follows.

```
[ + | - ] <digits> [ . <digits> ] [ E | e [ + | - ] <digits> ] [ f | F | d | D ]
```

- The first +/- means a positive or negative value of the entire number, and it can be omitted. If omitted, the default value is a positive value.
- In &lt;digits&gt;, numbers from 0 to 9 can be listed without white space, the number with decimal point can be written by using decimal point (.).
- An exponent form can be written after the first &lt;digits&gt;, and E or e is written, and it stands for exponent. Then +/- is written according to exponent sign, and &lt;digits&gt; is written. +/- of exponent can be omitted. If omitted, the default value is a positive value.
- Lastly, character such as f, F, d, D can be written after numbers. It means that it is a number of BINARY_FLOAT, BINARY_DOUBLE. If the corresponding character is omitted, the number is considered as NUMBER type.

The followings are examples of numeric literals.

```
20
+123.45
0.03
+1.23E-02
-1.5

10f
+123.45F
1.2E-3F
-22d
123.45D
-1.23E+05D
```

<a id="ddd1cf1ae653e139"></a>
#### Datetime Literals

Datetime literals are representation of date/time type.   
Datetime value is specified using string literal, or by converting character or numeric value to datetime value using TO_*function (TO_DATE, etc).

Datetime data types are DATE, TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.

<a id="3967c655d974c30c"></a>
##### Date Literals

Date literals are written in a form of DATE'string literal' or TO_DATE(string_literal [, format]).

- DATE'string literal'
    - The format of date type is ' SYYYY-MM-DD'.
    - DATE'2002-07-15'
- TO_DATE(string_literal [, format])
    - If the format is not specified, the format of date type is NLS_DATE_FORMAT by default.
    - If the format is specified, the specified format is applied.

- The date type includes year, month, day, hour, minute, second (except for fractional seconds).
- If the date is omitted, the default value is the first day of the current month.
- If the hour, minute, second are omitted, the default value is midnight.
    - HH24 format: '00:00:00'
    - HH12 format: '12:00:00'
- To set the hour, minute, second to the default value (midnight) when the date value includes hour, minute, second, then use the TRUNC(date) function. 
- For example, in TRUNC(SYSDATE), SYSDATE includes the values of the year, month, day, hour, minute, second.
- To compare only the values of the year, month, day among date values, then set the values of the hour, minute, second are set to midnight using the TRUNC function.

For more information, refer to [TO_DATE](#25eb6843029ae86c), [Datetime Format String](#f23ffe951177a789), [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#6c5301741d86446c).

- The following is an example of date literals.

```
DATE'2002-07-15'
```

- The following is an example of when the format is not specified, so NLS_DATE_FORMAT is 'YYYY-MM-DD'.

```
TO_DATE( '2002-07-15' )
```

- The followings are examples of when the format is specified.

```
TO_DATE( '15-JUL-02', 'DD-MON-RR' )
TO_DATE( '2002-07-15 00:00:00', 'YYYY-MM-DD HH24:MI:SS' )
TO_DATE( '2002-07-15 13:25:30', 'YYYY-MM-DD HH24:MI:SS' )
```

- The following is an example of when the date is omitted. (It is set to the first day of the current month).

```
gSQL> SELECT TO_DATE( '2000-07', 'YYYY-MM' ) FROM DUAL;
TO_DATE( '2000-07', 'YYYY-MM' )
-------------------------------
2000-07-01
```

- The following is an example of when the hour, minute, second are omitted. (It is set to the midnight).

```
gSQL> SELECT 
      TO_CHAR( DATE'2002-07-15', 'YYYY-MM-DD HH24:MI:SS' ) AS RESULT
      FROM DUAL;
RESULT             
-------------------
2002-07-15 00:00:00
```

- The following is an example of setting the hour, minute, second of DATE value (SYSDATE) to the default value (midnight).

```
gSQL> SELECT 
      TO_CHAR( SYSDATE, 
               'YYYY-MM-DD HH24:MI:SS' ) AS RESULT_SYSDATE,
      TO_CHAR( TRUNC( SYSDATE ),
               'YYYY-MM-DD HH24:MI:SS' ) AS RESULT_TRUNC_SYSDATE 
      FROM DUAL;
RESULT_SYSDATE      RESULT_TRUNC_SYSDATE
  ------------------- --------------------
  2014-08-19 10:06:49 2014-08-19 00:00:00
```

- The following is an example of comparing only the values of the year, month, day among date values.

```
gSQL> SELECT 
      TO_DATE( '2002-08-12' ) = 
      TRUNC( TO_DATE( '2002-08-12 23:59:59', 'YYYY-MM-DD HH24:MI:SS' ) )
      AS RESULT FROM DUAL;
RESULT
------
TRUE
```

<a id="49e8d4527de6cb84"></a>
##### Time Literals

Time literals are written in a form of TIME'string literal' or TO_TIME(string_literal [, format]).

- TIME'string literal'
    - The format of time type is 'HH24:MI:SS[.[FF6]]'.
    - TIME'15:30:59.999999'
- TO_TIME(string_literal [, format])
    - If the format is not specified, the format of time type is NLS_TIME_FORMAT by default.
    - If the format is specified, the specified format is applied.

The time type includes hour, minute, second (fractional seconds).  
Fractional seconds can be specified to maximum six digits numbers format.

For more information, refer to [TO_TIME](#d9a48ce329494e11), [Datetime Format String](#f23ffe951177a789), [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#3eb7e8d0be6c45dd).

- The following is an example of time literals.

```
TIME'15:30:59.999999'
```

- The following is an example of when the format is not specified, so NLS_TIME_FORMAT is 'HH24:MI:SS.FF6'.

```
TO_TIME( '15:30:59.999999' )
```

- The following is an example of when the format is specified.

```
TO_TIME( '09.45.03.546873 AM', 'HH12.MI.SS.FF6 AM' )
TO_TIME( '09:45:03', 'HH12:MI:SS' )
```

<a id="c48cf3b2011afcce"></a>
##### Time with Time Zone Literals

Time with time zone literals is written in a form of TIME'string literal', TIME WITH TIME ZONE'string literal',  TO_TIME_WITH_TIME_ZONE(string_literal [, format] ), or TO_TIME_TZ(string_literal [, format] ).

- TIME'string literal' or TIME WITH TIME ZONE'string literal'
    - The format of time with time zone type is 'HH24:MI:SS[.[FF6]] TZH:TZM'.
    - TIME'15:30:59.999999 +09:00'
    - TIME WITH TIME ZONE'15:30:59.999999 +09:00'
- TO_TIME_WITH_TIME_ZONE(string_literal [, format] )
    - If the format is not specified, the format of time with time zone type is NLS_TIME_WITH_TIME_ZONE_FORMAT by default.
    - If the format is specified, the specified format is applied.

Time with time zone type includes hour, minute, second (fractional seconds), and time zone offset (time zone hour, time zone minute).  
Fractional seconds can be specified to maximum six digits numbers format.

For more information, refer to [TO_TIME_WITH_TIME_ZONE](#766da9ffc336d7e2), [Datetime Format String](#f23ffe951177a789), [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#dc93f1addc88cbde).

- The followings are examples of time with time zone literals.

```
TIME'15:30:59.999999 +09:00'

TIME WITH TIME ZONE'15:30:59.999999 +09:00'
```

- The following is an example of when the format is not specified, so NLS_TIME_WITH_TIME_ZONE_FORMAT is 'HH24:MI:SS.FF6 TZH:TZM'.

```
TO_TIME_WITH_TIME_ZONE( '15:30:59.999999 +09:00' )
TO_TIME_TZ( '15:30:59.999999 +09:00' )
```

- The following is an example of when the format is specified.

```
TO_TIME_WITH_TIME_ZONE( '09.45.03.546873 +09:00 AM', 
                        'HH12.MI.SS.FF6 TZH:TZM AM' )
```

<a id="3427e629e71c129e"></a>
##### Timestamp Literals

Timestamp literals are written in a form of TIMESTAMP'string literal' or TO_TIMESTAMP(string_literal [, format] ).

- TIMESTAMP'string literal'
    - The format of timestamp type is 'SYYYY-MM-DD HH24:MI:SS[.[FF6]]'.
    - TIMESTAMP'2002-07-15 15:39:59.999999'
- TO_TIMESTAMP(string_literal [, format] )
    - If the format is not specified, the format of timestamp type is NLS_TIMESTAMP_FORMAT by default.
    - If the format is specified, the specified format is applied.

Timestamp type includes year, month, day, hour, minute, second (fractional seconds).  
Fractional seconds can be specified to maximum six digits numbers format.

For more information, refer to [TO_TIMESTAMP](#3e1f1636fafd674a), [Datetime Format String](#f23ffe951177a789), [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#f04f20ba0ffa3caf).

- The following is an example of timestamp literals.

```
TIMESTAMP'2002-07-15 15:39:59.999999'
```

- The following is an example of when the format is not specified, so NLS_TIMESTAMP_FORMAT is 'YYYY-MM-DD HH24:MI:SS.FF6'.

```
TO_TIMESTAMP( '2002-07-15 15:39:59.999999' )
```

- The following is an example of when the format is specified.

```
TO_TIMESTAMP( '15-JUL-02 11.06.30.123456 AM', 
              'DD-MON-RR HH12.MI.SS.FF6 AM' )
```

<a id="179066ecde8e8fcb"></a>
##### Timestamp with Time Zone Literals

Timestamp with time zone literals is written in a form of TIMESTAMP'string literal',  TIMESTAMP WITH TIME ZONE'string literal', TO_TIMESTAMP_WITH_TIME_ZONE(string_literal [, formt] ), or TO_TIMESTAMP_TZ(string_literal [, format]).

- TIMESTAMP'string literal' or TIMESTAMP WITH TIME ZONE'string literal'
    - The format of timestamp with time zone type is 'SYYYY-MM-DD HH24:MI:SS[.[FF6]] TZH:TZM'.
    - TIMESTAMP'2002-07-15 15:39:59.999999 +09:00'
    - TIMESTAMP WITH TIME ZONE'2002-07-15 15:39:59.999999 +09:00'
- TO_TIMESTAMP_WITH_TIME_ZONE(string_literal [, formt] )
    - If the format is not specified, the format of timestamp with time zone type is NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT by default. 
    - If the format is specified, the specified format is applied.

Timestamp with time zone type includes year, month, day, hour, minute, second (fractional seconds), time zone offset (time zone hour, time zone minute).  
Fractional seconds can be specified to maximum six digits numbers format.

For more information, refer to [TO_TIMESTAMP_WITH_TIME_ZONE](#77a90650f33e49f9), [Datetime Format String](#f23ffe951177a789) , [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#edba3110d229ce95).

- The following is an example of timestamp with time zone literals.

```
TIMESTAMP'2002-07-15 15:39:59.999999 +09:00'
TIMESTAMP WITH TIME ZONE'2002-07-15 15:39:59.999999 +09:00'
```

- The following is an example of when the format is not specified, so NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT is 'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM'.

```
TO_TIMESTAMP_WITH_TIME_ZONE( '2002-07-15 15:39:59.999999 +09:00' )
TO_TIMESTAMP_TZ( '2002-07-15 15:39:59.999999 +09:00' )
```

- The following is an example of when the format is specified.

```
TO_TIMESTAMP_WITH_TIME_ZONE( '15-JUL-02 11.06.30.123456 +09:00 AM',
                             'DD-MON-RR HH12.MI.SS.FF6 TZH:TZM AM' )
TO_TIMESTAMP_TZ( '15-JUL-02 11.06.30.123456 +09:00 AM',
                 'DD-MON-RR HH12.MI.SS.FF6 TZH:TZM AM' )
```

<a id="3e1e94e284d2f9d2"></a>
#### Interval Literals

The interval literals specify the time interval.

Intervals are classified and expressed as follows.

- Year-month INTERVAL values
    - It includes YEAR and MONTH.
    - Display string expression: 'year-month'
- Day-time INTERVAL values
    - It includes DAY, HOUR, MINUTE, SECOND (fractional seconds).
    - Display string expression: 'day hour:minute:second.fractional_seconds'
- The interval value's sign is specified only once at the beginning of the string representation.  
  e.g. INTERVAL'+3 11:22:33.999999'DAY TO SECOND (O)  
  INTERVAL'-3 +11:22:33.999999'DAY TO SECOND (X)

The followings are the list of interval types.

- INTERVAL YEAR (leading precision)
- INTERVAL MONTH (leading precision)
- INTERVAL YEAR (leading precision) TO MONTH
- INTERVAL DAY (leading precision)
- INTERVAL HOUR (leading precision)
- INTERVAL MINUTE (leading precision)
- INTERVAL SECOND (leading precision[, fractional seconds precision] )
- INTERVAL DAY (leading precision) TO HOUR
- INTERVAL DAY (leading precision) TO MINUTE
- INTERVAL DAY (leading precision) TO SECOND (fractional seconds precision)
- INTERVAL HOUR (leading precision) TO MINUTE
- INTERVAL HOUR (leading precision) TO SECOND (fractional seconds precision)
- INTERVAL MINUTE (leading precision) TO SECOND (fractional seconds precision)

Leading precision  
&nbsp;• It is the digit number of the field, it can be specified from 2 to 6. If it is not specified, the default   
&nbsp;&nbsp;&nbsp;value is set to 2.  
&nbsp;• If the leading field value exceeds the leading precision, then an error is returned.

Fractional seconds precision  
• It is the digit number of fractional seconds, and it can be specified from 0 to 6. If it is not specified,  
&nbsp;the default value is set to 6.  
• If the fractional second field value exceeds the fractional seconds precision, then it is rounded off.

For more information, refer to [INTERVAL](#f6b7d049ffca0557), [Precisions and value range of the second or later field in INTERVAL * TO * ](#7c86b8edb02937b9).

<a id="966028984f938d37"></a>
#### Examples of Using Interval Literals.

The followings are examples of using interval literals.

<a id="4dde3737c89474f6"></a>
##### Interval YEAR

The followings are examples of using interval YEAR literals.

**Interval YEAR literals.**

<a id="6e22f2e55fc1e4a6"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'YEAR INTERVAL'01-00'YEAR | 1 year | +01-00 |
| INTERVAL'100'YEAR | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100'YEAR(3) | 100 year | +100-00 |
| INTERVAL'+999999'YEAR(6) | 999999 year | +999999-00 |
| INTERVAL'-999999'YEAR(6) | -(999999 year) | -999999-00 |

<a id="e50fb10948b8c096"></a>
##### Interval MONTH

The followings are examples of using interval MONTH literals.

<a id="1a3afe6d602469e5"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'MONTH INTERVAL'00-01'MONTH | 1 month | +00-01 |
| INTERVAL'100'MONTH | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100'MONTH(3) | 8 year 4 month | +008-04 |
| INTERVAL'+999999'MONTH(6) | 83333 year 3 month | +083333-03 |
| INTERVAL'-999999'MONTH(6) | -(83333 year 3 month) | -083333-03 |

<a id="d3fc842cc905b7eb"></a>
##### Interval YEAR TO MONTH

The followings are examples of using interval YEAR TO MONTH literals.

<a id="fadbed9702dedece"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1-06'YEAR TO MONTH | 1 year 6 month | +01-06 |
| INTERVAL'1-12'YEAR TO MONTH | The month value exceeded 11, so it returns the error. | - |
| INTERVAL'100-11'YEAR TO MONTH | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100-11'YEAR(3) TO MONTH | 100 year 11 month | +100-11 |
| INTERVAL'+999999-11'YEAR(6) TO MONTH | 999999 year 11 month | +999999-11 |
| INTERVAL'-999999-11'YEAR(6) TO MONTH | -(999999 year 11 month) | -999999-11 |

<a id="e59c14943249d61c"></a>
##### Interval DAY

The followings are examples of using interval DAY literals.

<a id="e7ae13ebfcc1abd5"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'DAY INTERVAL'01 00:00:00'DAY | 1 day | +01 00:00:00 |
| INTERVAL'100'DAY | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100'DAY(3) | 100 day | +100 00:00:00 |
| INTERVAL'+999999'DAY(6) | 999999 day | +999999 00:00:00 |
| INTERVAL'-999999'DAY(6) | -(999999 day) | -999999 00:00:00 |

<a id="3cb010114376620f"></a>
##### Interval HOUR

The followings are examples of using interval HOUR literals.

<a id="942eb06f0824a92a"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'HOUR INTERVAL'00 01:00:00'HOUR | 1 hour | +00 01:00:00 |
| INTERVAL'1000'HOUR(3) | It exceeds the leading precision 3, so it returns the error | - |
| INTERVAL'1000'HOUR(4) | 41 day 16 hour | +0041 16:00:00 |
| INTERVAL'+999999'HOUR(6) | 41666 day 15 hour | +041666 15:00:00 |
| INTERVAL'-999999'HOUR(6) | -(41666 day 15 hour) | -041666 15:00:00 |

<a id="8c0c09f256a3f5c0"></a>
##### Interval MINUTE

The following are examples of using interval MINUTE literals.

<a id="005f9bdbc41f2377"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'MINUTE INTERVAL'00 00:01:00'MINUTE | 1 minute | +00 00:01:00 |
| INTERVAL'12345'MINUTE(4) | It exceeds the leading precision 4, so it returns the error | - |
| INTERVAL'12345'MINUTE(5) | 8 day 13 hour 45 minute | +00008 13:45:00 |
| INTERVAL'+999999'MINUTE(6) | 694 day 10 hour 39 minute | +000694 10:39:00 |
| INTERVAL'-999999'MINUTE(6) | -(694 day 10 hour 39 minute) | -000694 10:39:00 |

<a id="0227820522fc5ec3"></a>
##### Interval SECOND

The followings are examples of using interval SECOND literals.

<a id="2ac14c74cc6e01e9"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'SECOND INTERVAL'00 00:00:01.000000'SECOND | 1 second | +00 00:00:01.000000 |
| INTERVAL'100'SECOND | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'99.9999999'SECOND INTERVAL'99.9999999'SECOND(2,6) | The fractional seconds are rounded off to become 100 second, then it exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'99.9999999'SECOND(3) | 1 minute 40 second | +000 00:01:40.000000 |
| INTERVAL'29.506167'SECOND(2, 2) | 29.51 second | +00 00:00:29.51 |
| INTERVAL'999999.999999'SECOND(6,6) | 11day 13 hour 46 minute 39.999999 second | +000011 13:46:39.999999 |
| INTERVAL'-999999.999999'SECOND(6,6) | -(11day 13 hour 46 minute 39.999999 second) | -000011 13:46:39.999999 |

<a id="893592209d536024"></a>
##### Interval DAY TO HOUR

The followings are examples of using interval DAY TO HOUR literals.

<a id="0364830f7213e166"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1 23'DAY TO HOUR INTERVAL'01 23:00:00'DAY TO HOUR | 1 day 23 hour | +01 23:00:00 |
| INTERVAL'1 24'DAY TO HOUR | The hour value exceeds 23 (invalid), so it returns the error. | - |
| INTERVAL'100 23'DAY TO HOUR | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100 23'DAY(3) TO HOUR | 100 day 23 hour | +100 23:00:00 |
| INTERVAL'+999999 23'DAY(6) TO HOUR | 999999 day 23 hour | +999999 23:00:00 |
| INTERVAL'-999999 23'DAY(6) TO HOUR | -(999999 day 23 hour) | -999999 23:00:00 |
| INTERVAL'-999999 +23'DAY(6) TO HOUR | Invalid sign error | - |

<a id="aa14c795856c43fe"></a>
##### Interval DAY TO MINUTE

The followings are examples of using interval DAY TO MINUTE literals.

<a id="7967665a048340df"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1 23:59'DAY TO MINUTE INTERVAL'01 23:59:00'DAY TO MINUTE | 1 day 23 hour 59 second | +01 23:59:00 |
| INTERVAL'1 24:59'DAY TO MINUTE | The hour value exceeds 23 (invalid), so it returns the error. | - |
| INTERVAL'1 23:60'DAY TO MINUTE | The minute value exceeds 59 (invalid), so it returns the error. | - |
| INTERVAL'100 23:59'DAY TO MINUTE | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100 23:59'DAY(3) TO MINUTE | 100 day 23 hour 59 minute | +100 23:59:00 |
| INTERVAL'+999999 23:59'DAY(6) TO MINUTE | 999999 day 23 hour 59 minute | +999999 23:59:00 |
| INTERVAL'-999999 23:59'DAY(6) TO MINUTE | -(999999 day 23 hour 59 minute) | -999999 23:59:00 |

<a id="eb6ff216cf989ab7"></a>
##### Interval DAY TO SECOND

The followings are examples of using interval DAY TO SECOND literals.

<a id="924975bb1efec529"></a>
| Example | Description | display string |
| --- | --- | --- |
| INTERVAL '1 23:59:59.999999'DAY TO SECOND | 1 day 23 hour 59 minute 59.999999 second | +01 23:59:59.999999 |
| INTERVAL '1 24:59:59.999999'DAY TO SECOND | The hour value exceeds 23, so it returns the error. | - |
| INTERVAL '1 23:60:59.999999'DAY TO SECOND | The minute value exceeds 59, so it returns the error. | - |
| INTERVAL '1 23:59:60.999999'DAY TO SECOND | The second value exceeds 60, so it returns the error. | - |
| INTERVAL '99 23:59:59.9999999'DAY TO SECOND | The fractional seconds are rounded off to become 100 day, then it exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL '99 23:59:59.9999999'DAY(3) TO SECOND | 100 day | +100 00:00:00.000000 |
| INTERVAL '1 11:22:33.567890'DAY(2) TO SECOND(2) | 1 day 11 hour 22 minute 33.57 second | +01 11:22:33.57 |
| INTERVAL '+999999 23:59:59.999999'DAY(6) TO SECOND(6) | 999999 day 23 hour 59 minute 59.999999 hour | +999999 23:59:59.999999 |
| INTERVAL '-999999 23:59:59.999999'DAY(6) TO SECOND(6) | -(999999 day 23 hour 59 minute 59.999999 hour) | -999999 23:59:59.999999 |

<a id="f4c741e5af1f90e8"></a>
##### Interval HOUR TO MINUTE

The followings are examples of using interval HOUR TO MINUTE literals.

<a id="941f2375df42546f"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'23:59'HOUR TO MINUTE INTERVAL'00 23:59:00'HOUR TO MINUTE | 23 hour 59 minute | +00 23:59:00 |
| INTERVAL'23:60'HOUR TO MINUTE | The minute value exceeds 59, so it returns the error. | - |
| INTERVAL'100:59'HOUR TO MINUTE | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100:59'HOUR(3) TO MINUTE | 4 day 4 hour 59 minute | +004 04:59:00 |
| INTERVAL'+999999:59'HOUR(6) TO MINUTE | 41666 day 15 hour 59 minute | +041666 15:59:00 |
| INTERVAL'-999999:59'HOUR(6) TO MINUTE | -(41666 day 15 hour 59 minute) | -041666 15:59:00 |

<a id="9520c37771b3bad2"></a>
##### Interval HOUR TO SECOND

The followings are examples of using interval HOUR TO SECOND literals.

<a id="88c39f8c0c185e52"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL '23:59:59.999999'HOUR TO SECOND INTERVAL '00 23:59:59.999999'HOUR TO SECOND | 23 hour 59 minute 59.999999 second | +00 23:59:59.999999 |
| INTERVAL '23:60:59.999999'HOUR TO SECOND | The minute value exceeds 59, so it returns the error. | - |
| INTERVAL '23:59:60.999999'HOUR TO SECOND | The second value exceeds 59, so it returns the error. | - |
| INTERVAL '99:59:59.9999999'HOUR TO SECOND | The fractional seconds are rounded off to become 100 hour, then it exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL '99:59:59.9999999'HOUR(3) TO SECOND | 4 day 4 hour | +004 04:00:00.000000 |
| INTERVAL '11:22:29.569'HOUR(3) TO SECOND(1) | 11 hour 22 minute 29.6 second | +000 11:22:29.6 |
| INTERVAL '+999999:59:59.999999'HOUR(6) TO SECOND(6) | 41666 day 15 hour 59 minute 59.999999 second | +041666 15:59:59.999999 |
| INTERVAL '-999999:59:59.999999'HOUR(6) TO SECOND(6) | -(41666 day 15 hour 59 minute 59.999999 second) | -041666 15:59:59.999999 |

<a id="7669f7ccae73265d"></a>
##### Interval MINUTE TO SECOND

The followings are examples of using interval MINUTE TO SECOND literals.

<a id="0edccc9a8dea7a50"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL '15:23.123456'MINUTE TO SECOND INTERVAL '00 00:15:23.123456'MINUTE TO SECOND | 15 minute 23.123456 second | +00 00:15:23.123456 |
| INTERVAL '15:60.123456'MINUTE TO SECOND | The second value exceeds 59, so it returns the error. | - |
| INTERVAL '99:59.999999'MINUTE TO SECOND(2) | The fractional seconds are rounded off to become 100 minute, then it exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL '99:59.999999'MINUTE(3) TO SECOND(2) | 1 hour 40 minute | +000 01:40:00.00 |
| INTERVAL '+999999:59.999999'MINUTE(6) TO SECOND(6) | 694 day 10 hour 39 minute 59.999999 second | +000694 10:39:59.999999 |
| INTERVAL '-999999:59.999999'MINUTE(6) TO SECOND(6) | -(694 day 10 hour 39 minute 59.999999 second) | -000694 10:39:59.999999 |

<a id="9ec3fc0fb5a0644d"></a>
### Null Value

Null value is an unknown value or an undefined value. NULL value can be a value of any data type. The unknown value of the boolean type is represented as null value.  
Null value is defined as a keyword and it is not case-sensitive.

The following is an example of null value representation.

```
NULL
Null
```

<a id="32c3f5531959f130"></a>
### Comments

<a id="933055ab162cd9f1"></a>
#### Single Line Comment

A single line comment is a comment which starts with -- or //. The single line comment processes a comment from the behind of the comment's symbol to the end of the line.

The following is an example of using a single line comment.

```
gSQL> SELECT I1, -- I2, I3,
2 I4, I5
3 FROM T1;

I1        I4        I5       
--------- --------- ---------
column i1 column i4 column i5

1 row selected.


gSQL> SELECT I1, // I2, I3,
2 I4, I5
3 FROM T1;

I1        I4        I5       
--------- --------- ---------
column i1 column i4 column i5

1 row selected.
```

<a id="3c45cae65c3d60ae"></a>
#### Multiple Line Comment

A multiple line comment is a comment which starts with /* and ends with */. Multiple line comments specify a comment from /* to */, and it can use multiple lines to represent comments.

The following is an example of using multiple line comment.

```
gSQL> SELECT I1, I2, I3, I4, I5
2  /* Output 
3   all columns of TABLE T1 */

4 FROM T1;

I1        I2        I3        I4        I5       
--------- --------- --------- --------- ---------
column i1 column i2 column i3 column i4 column i5

1 row selected.
```

<a id="c1b18df58eb3739c"></a>
#### Hint Comment

A hint comment is a comment which starts with /*+ and ends with */. Hint comment is similar to multiple line comment, but the difference is that the hint comment has + at the beginning.   
Do not use a space between * and +. If  so,  it will be treated as multiple line comment.

Unlike other comments, a hint comment is specified to be used only at the location which is right after the SELECT keyword. The processing method which a user specified to GOLDILOCKS optimizer is described in the hint comment. For more information, refer to [hint clause](16-sql-references.md#ad0ef76d32e7f521).  

The following is an example of using hint comment.

```
gSQL> SELECT /*+ FULL(T1) */ * FROM T1;

I1        I2        I3        I4        I5       
--------- --------- --------- --------- ---------
column i1 column i2 column i3 column i4 column i5

1 row selected.
```

<a id="8eba0a8bbc086ac6"></a>
### SQL Reserved Words and Keywords

<a id="2254d7b4ce3d169e"></a>
#### SQL Reserved Words

GOLDILOCKS supports reserved words which are specified as SQL reserved words. The SQL reserved words can not be used without quotation marks other than specified location. However, it is not recommended to use SQL reserved words with quotation marks.

The followings are SQL reserved words of GOLDILOCKS. * marked SQL reserved words are supported by the SQL standard.   
For more information about the list, refer to [V$RESERVED_WORDS](../part-02-administration-manual/9-database-information.md#5c6b10f7f13abfbf).

ABSOLUTE  
ACCESS  
ALL *  
ALLOCATE *  
ALTER *  
AND *  
ANY *  
ARE *  
AS *  
ASYMMETRIC *  
AT *  
AUTHORIZATION *  
BEGIN *  
BETWEEN *  
BOTH *  
BY *  
CALL *  
CASE *  
CHECK *  
CLOSE *  
COLUMN *  
COMMENT  
COMMIT *  
CONNECT *  
CONSTRAINT *  
CREATE *  
CROSS *  
CURRENT *  
CURRENT_CATALOG *  
CURRENT_DATE *  
CURRENT_DEFAULT_TRANSFORM_GROUP *  
CURRENT_PATH *  
CURRENT_ROLE *  
CURRENT_ROW *  
CURRENT_SCHEMA *  
CURRENT_TIME *  
CURRENT_TIMESTAMP *  
CURRENT_TRANSFORM_GROUP_FOR_TYPE *  
CURRENT_USER *  
DATABASE  
DEALLOCATE *  
DECLARE *  
DEFAULT *  
DELETE *  
DEREF *  
DESCRIBE *  
DETERMINISTIC *  
DISCONNECT *  
DISTINCT *  
DROP *  
ELSE *  
END *  
END_EXEC *  
ESCAPE *  
EXCEPT *  
EXEC *  
EXECUTE *  
EXISTS *  
FALSE *  
FETCH *  
FILTER *  
FIRST  
FOR *  
FOREIGN *  
FREE *  
FROM *  
FULL *  
FUNCTION *  
GET *  
GLOBAL *  
GRANT *  
GROUP *  
HAVING *  
HOLD *  
IDENTIFIED  
IF  
IMMEDIATE  
IN *  
INDICATOR *  
INNER *  
INOUT *  
INSERT *  
INTERSECT *  
INTO *  
IS *  
JOIN *  
LAST  
LEADING *  
LEFT *  
LIKE *  
LIMIT  
LOCAL *  
LOCALTIME *  
LOCALTIMESTAMP *  
MATCH *  
MEMBER *  
MERGE *  
MINUS  
NATURAL *  
NEW *  
NEXT  
NOT *  
NULL *  
OF *  
OFFSET *  
OLD *  
ON *  
OPEN *  
OR *  
ORDER *  
OUT *  
PREPARE *  
PRIMARY *  
PRIOR  
PROCEDURE *  
PROFILE  
REF *  
REFERENCES *  
RELATIVE  
RELEASE *  
RENAME  
RETURN *  
RETURNING  
RETURNS *  
REVOKE *  
RIGHT *  
ROLLBACK *  
ROW *  
ROWID  
ROWS *  
ROW_NUMBER *  
SAVEPOINT *  
SELECT *  
SESSION_USER *  
SET *  
SOME *  
SQL *  
SQLEXCEPTION *  
SQLSTATE *  
SQLWARNING *  
START *  
SYMMETRIC *  
SYNONYM  
SYSDATE  
SYSTEM *  
SYSTEM_USER *  
SYSTIME  
SYSTIMESTAMP  
TABLE *  
THEN *  
TO *  
TRAILING *  
TRIGGER *  
TRUE *  
TRUNCATE *  
UNION *  
UNIQUE *  
UNKNOWN *  
UPDATE *  
UPPER *  
USER *  
USING *  
VALUES *  
VIEW  
WHEN *  
WHENEVER *  
WHERE *  
WINDOW *  
WITH *  
WITHOUT *

<a id="3f18b1ad5e57df8b"></a>
#### SQL Keywords

GOLDILOCKS SQL keywords are not reserved words. However, they are keywords which are internally used by GOLDILOCKS. Therefore, it is not recommended to use GOLDILOCKS SQL keywords because it can decrease the readability of the results.

GOLDILOCKS SQL keywords list can be viewed through [V$KEYWORDS](../part-02-administration-manual/9-database-information.md#1080ad52fff7eced).

<a id="12a37b9791ef874c"></a>
### Compatibility for Syntax Elements

The SQL standard compatibility for syntax element is as follows.

**SQL standard compatibility for syntax element**

<a id="c476e2d05d889d4b"></a>
| Feature ID | Description | Availability |
| --- | --- | --- |
| E021-03 | Character literals | O |
| E131 | Null value support (nulls in lieu of values) | O |
| E161 | SQL comments using leading double minus | O |
| F051-01 | DATE data type (including support of DATE literal) | O |
| F051-02 | TIME data type (including support of TIME literal) with fractional seconds precision of at least 0 | O |
| F051-03 | TIMESTAMP data type (including support of TIMESTAMP literal) with fractional seconds precision of at least 0 and 6 | O |
| F271 | Compound character literals | X |
| F383 | Set column not null clause | O |
| F391 | Long identifiers | X |
| F392 | Unicode escapes in identifiers | X |
| F393 | Unicode escapes in literals | X |
| T023 | Compound binary literals | X |
| T024 | Spaces in binary literals | X |
| T101 | Enhanced nullability determination | X |
| T351 | Bracketed comments | X |
| T591 | UNIQUE constraints of possibly null columns | O |
| X041 | Basic table mapping: null absent | X |
| X042 | Basic table mapping: null as nil | X |
| X051 | Advanced table mapping: null absent | X |
| X052 | Advanced table mapping: null as nil | X |
| X170 | XML null handling options | X |
| X400 | Name and identifier mapping | X |

<a id="9ebaf6ccb06f475d"></a>
## Data Type

<a id="1f3d6870f7da5b41"></a>
### Numeric Type

Numeric data types are classified according to the storage method and the fractional part representation.

- Classification by the storage method 
    - Decimal numeric type
        - It stores decimal numbers in 100 digits basis.
        - Types: NUMBER, NUMERIC, FLOAT
    - Binary numeric type 
        - It stores numbers of C language as it is.
        - Types: NATIVE_INTEGER, NATIVE_DOUBLE

- Classification by fractional part representation
    - Fixed point data type (exact numeric)
        - It is a numeric type whose scale is fixed. 
        - Types: NUMERIC(precision, scale), NATIVE_INTEGER
    - Floating point data type (approximate numeric)
        - It is a numeric type whose scale is not fixed. 
        - Types: FLOAT(precision), NATIVE_DOUBLE

<a id="ab67684b67d4464a"></a>
#### Decimal Numeric Type

This type's precision and scale are based on decimal number. The precision indicates accuracy of the valid digits, and the scale indicates the range of fraction.

<a id="e5cac7d665e5b45d"></a>
##### Decimal Fixed Point Number Type

The decimal fixed point number type is defined in SQL.

**Decimal fixed point number type**

<a id="568c9b15717dba7a"></a>
| Type | Decimal precision | Decimal scale | Refer to |
| --- | --- | --- | --- |
| NUMBER( p ) | p | 0 | [NUMBER](#68b0be359ae3c9d6) |
| NUMBER( p, s ) | p | s | [NUMBER](#68b0be359ae3c9d6) |
| NUMERIC( p ) | p | 0 | [NUMERIC](#4cc855c2aaab3d4e) |
| NUMERIC( p, s ) | p | s | [NUMERIC](#4cc855c2aaab3d4e) |
| DECIMAL( p ) | p | 0 | [NUMERIC](#4cc855c2aaab3d4e) type alias |
| DECIMAL( p, s ) | p | s | [NUMERIC](#4cc855c2aaab3d4e) type alias |
| DEC( p ) | p | 0 | [NUMERIC](#4cc855c2aaab3d4e) type alias |
| DEC( p, s ) | p | s | [NUMERIC](#4cc855c2aaab3d4e) type alias |
| SMALLINT | 5 | 0 | [NUMERIC](#4cc855c2aaab3d4e) type alias |
| INTEGER | 10 | 0 | [NUMERIC](#4cc855c2aaab3d4e) type alias |
| BIGINT | 19 | 0 | [NUMERIC](#4cc855c2aaab3d4e) type alias |
| INT2 | 5 | 0 | [NUMERIC](#4cc855c2aaab3d4e) type alias |
| INT4 | 10 | 0 | [NUMERIC](#4cc855c2aaab3d4e) type alias |
| INT8 | 19 | 0 | [NUMERIC](#4cc855c2aaab3d4e) type alias |

<a id="8653a33b7574e42b"></a>
##### Decimal Floating Point Number Type

The decimal floating point number type is defined in SQL.

**Decimal floating point number type**

<a id="f00488b5692448d9"></a>
| Type | Decimal precision | Decimal scale | Refer to |
| --- | --- | --- | --- |
| NUMBER | 38 | N/A | [NUMBER](#68b0be359ae3c9d6) |
| FLOAT( p ) | ceil( log<sub>10</sub> 2<sup>p</sup> ) | N/A | [FLOAT](#04e4e9aa22dbfbfa) |
| REAL | ceil( log<sub>10</sub> 2<sup>24</sup> ) = 8 | N/A | [FLOAT](#04e4e9aa22dbfbfa) type alias |
| DOUBLE | ceil( log<sub>10</sub> 2<sup>53</sup> ) = 16 | N/A | [FLOAT](#04e4e9aa22dbfbfa) type alias |
| FLOAT4 | ceil( log<sub>10</sub> 2<sup>24</sup> ) = 8 | N/A | [FLOAT](#04e4e9aa22dbfbfa) type alias |
| FLOAT8 | ceil( log<sub>10</sub> 2<sup>53</sup> ) = 16 | N/A | [FLOAT](#04e4e9aa22dbfbfa) type alias |

<a id="9ba7ffb5a97011b7"></a>
#### Binary Number Type

This type's precision and scale are based on binary number. The precision indicates accuracy of the valid digits, and the scale indicates the range of fraction.

<a id="544db3812c8fd35f"></a>
##### Binary Fixed Point Number Type

The binary fixed point number type refers to the signed integer data type of C language.  
1 bit is used to represent the sign bit, and other bits are used to represent the precision, but not any bit is used to represent the scale.

**Binary fixed point number type**

<a id="ffe5f2c9f79eace7"></a>
| Type | Binary precision | Binary scale | Refer to |
| --- | --- | --- | --- |
| NATIVE_SMALLINT | 15 | 0 | [NATIVE_SMALLINT](#fc64233a3ddee2c5) |
| NATIVE_INTEGER | 31 | 0 | [NATIVE_INTEGER](#a7125330e516b594) |
| NATIVE_BIGINT | 63 | 0 | [NATIVE_BIGINT](#74b62854715c94af) |

<a id="9da726171a356d3c"></a>
##### Binary Floating Point Number Type

The binary floating point type refers to the float and double data type in C language.  
1 bit is used to represent the sign bit, and other bits are used to represent the precision and scale.

**Binary floating point number type**

<a id="b031f07ec77c4907"></a>
| Type | Binary precision | Binary scale | Refer to |
| --- | --- | --- | --- |
| NATIVE_REAL | 23 | 8 | [NATIVE_REAL](#701e2c4fabd684e2) |
| NATIVE_DOUBLE | 52 | 11 | [NATIVE_DOUBLE](#37e17e763fe87201) |

> The precision and scale of binary floating point type is subject to change depending on the influence of the compiler and OS.

<a id="f1cc8e366b347833"></a>
### CHARACTER STRING Type

CHARACTER STRING data types are classified according to whether it is a variable length string and the maximum length of string.

- Classification by whether a variable length string exists
    - Fixed length string
        - Refer to [CHARACTER](#0911bf6123a5f020).
    - Variable length string 
        - Refer to [CHARACTER VARYING](#ad554c09b6feef05), [CHARACTER LONG VARYING](#429ccd166922ee94).
- Classification by the maximum length of a string
    - 2000 [ characters or bytes ] 
        - Refer to [CHARACTER](#0911bf6123a5f020).
    - 4000 [ characters or bytes ] 
        - Refer to [CHARACTER VARYING](#ad554c09b6feef05).
    - 100 megabytes 
        - Refer to [CHARACTER LONG VARYING](#429ccd166922ee94).

<a id="2116ef372aa832c2"></a>
### BINARY STRING Type

BINARY STRING data types are classified according to whether it is a variable length binary string and the maximum length of binary string.

- Classification by whether it is a variable length binary string 
    - Fixed length binary string 
        - Refer to [BINARY](#5209bc041cbb637f).
    - Variable length binary string 
        - Refer to [BINARY VARYING](#6abd619dad707497), [BINARY LONG VARYING](#3045806ebc113f60).
- Classification by the maximum length of binary string
    - 2000 
        - Refer to [BINARY](#5209bc041cbb637f).
    - 4000 
        - Refer to [BINARY VARYING](#6abd619dad707497).
    - 100 Mega Bytes 
        - Refer to [BINARY LONG VARYING](#3045806ebc113f60).

<a id="dc6a408d7c498d2c"></a>
### Date/ Time Type

Date/ time data type specifies the year, month, day, hour, minute, second, time zone offset in accordance with their representation method.   
Date/ time data type has [DATE](#3a80607ae5e62f9a), [TIME](#d1cf3fafd4663cb4), [TIMESTAMP](#e301c3bda5651cd6) types.

<a id="8ffc316f68cf458c"></a>
### INTERVAL Type

INTERVAL data type specifies the time interval.   
It specifies the time interval of the year, month, day, hour, minute, second in accordance with their representation method.

[INTERVAL](#f6b7d049ffca0557) data types are classified to the YEAR TO MONTH family type and the DAY TO SECOND family type, according to the range of value representation.

<a id="f847a465e9670492"></a>
### BOOLEAN Type

The BOOLEAN data type stores values of TRUE, FALSE, UNKNOWN. UNKNOWN value is represented as a null value. All expressions used as conditions return the BOOLEAN value and the column or the value defined as a BOOLEAN data type can be used as a condition.

For more information, refer to [BOOLEAN](#d49c3b75726d4ba1).

<a id="a1528dca01536478"></a>
### ROWID Type

All records stored in the database have unique location information. The record identifier (ROWID) is used to distinguish each record.

ROWID data type is used to store and manage the record identifier (ROWID).  
Record identifier (ROWID) is obtained by the query using the ROWID pseudo column.

For more information, refer to [ROWID](#b43645fb3f6eb862).

<a id="0b812e6987dc67cb"></a>
### Type Comparison

Comparing two types is executed on the basis of one representative type. If the comparison target type is different from the representative type, then the comparison can go through a type conversion.  
[The representative types for type comparison](#7a224e9a69218b28) defines the representative type for comparing two types.

The following table describes target type conversion for comparison per each representative type.

- [ Type conversion for the VC comparison](#79d1fa8deb20f282)
- [Type conversion for the LC comparison](#5a050c4af4f13572)
- [Type conversion for the VB comparison](#c41dfe9966c042ab)
- [Type conversion for the LB comparison](#85cf3ef88c911ba2)
- [Type conversion for the NB comparison](#ac9f662dba1fc61d)
- [Type conversion for the ND comparison](#36f0605d1c5c04d6)
- [Type conversion for the NU comparison](#1a0e53360f2c240b)
- [Type conversion for the DA comparison](#793ebc4518cbdf3c)
- [Type conversion for the TI comparison](#02eebddd22bbc49c)
- [Type conversion for the TZ comparison](#f91e528a19b267d1)
- [Type conversion for the TS comparison](#c202263a86eae381)
- [Type conversion for the SZ comparison](#6db8805f6f242116)
- [Type conversion for the YM comparison](#efd0d3938a7c7387)
- [Type conversion for the DS comparison](#5a2e4f371c185701)
- [Type conversion for the BO comparison](#c053498dca1f2806)
- [Type conversion for the RI comparison](#5d40f79ad66d9822)

> The followings are abbreviations which are used for the type comparison.
> 
> - "`VC`": CHARACTER VARYING
> - "`LC`": CHARACTER LONG VARYING
> - "`VB`": BINARY VARYING
> - "`LB`": BINARY LONG VARYING
> - "`NB`": NATIVE_BIGINT
> - "`ND`": NATIVE_DOUBLE
> - "`NU`": NUMBER
> - "`DA`": DATE
> - "`TI`": TIME
> - "`TZ`": TIME WITH TIMEZONE
> - "`TS`": TIMESTAMP
> - "`SZ`": TIMESTAMP WITH TIMEZONE
> - "`YM`": INTERVAL YEAR TO MONTH
> - "`DS`": INTERVAL DAY TO SECOND
> - "`BO`": BOOLEAN
> - "`RI`": ROWID
> 

> In the type comparison table, the built-in data types are represented by an abbreviated word enclosed in double quotes ("").
> 
> - "CHAR": CHARACTER
> - "VARCHAR": CHARACTER VARYING
> - "LONG VARCHAR": CHARACTER LONG VARYING
> - "VARBINARY": BINARY VARYING
> - "LONG VARBINARY": BINARY LONG VARYING
> - "TIME_TZ": TIME WITH TIMEZONE
> - "TIMESTAMP_TZ": TIMESTAMP WITH TIMEZONE
> - "INTERVAL_YM": INTERVAL YEAR TO MONTH
> - "INTERVAL_DS": INTERVAL DAY TO SECOND
> 

**The representative types for type comparison**

<a id="7a224e9a69218b28"></a>
| Data type | C H A R | V A R C H A R | L O N G  V A R C H A R | B I N A R Y | V A R B I N A R Y | L O N G  V A R B I N A R Y | N A T I V E  S M A L L I N T | N A T I V E  I N T E G E R | N A T I V E  B I G I N T | N A T I V E  R E A L | N A T I V E  D O U B L E | N U M B E R | N U M E R I C | F L O A T | D A T E | T I M E | T I M E    T Z | T I M E S T A M P | T I M E S T A T M P   T Z | I N T E R V A L  Y M | I N T E R V A L  D S | B O O L E A N | R O W I D |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CHAR | `VC` | `VC` | `LC` |  |  |  | `NU` | `NU` | `NU` | `NU` | `ND` | `NU` | `NU` | `NU` | `DA` | `TI` | `TZ` | `TS` | `SZ` | `YM` | `DS` | `BO` | `RI` |
| VARCHAR | `VC` | `VC` | `LC` |  |  |  | `NU` | `NU` | `NU` | `NU` | `ND` | `NU` | `NU` | `NU` | `DA` | `TI` | `TZ` | `TS` | `SZ` | `YM` | `DS` | `BO` | `RI` |
| LONG VARCHAR | `LC` | `LC` | `LC` |  |  |  | `NU` | `NU` | `NU` | `NU` | `ND` | `NU` | `NU` | `NU` | `DA` | `TI` | `TZ` | `TS` | `SZ` | `YM` | `DS` | `BO` | `RI` |
| BINARY |  |  |  | `VB` | `VB` | `LB` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| VARBINARY |  |  |  | `VB` | `VB` | `LB` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| LONG VARBINARY |  |  |  | `LB` | `LB` | `LB` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| NATIVE_SMALLINT | `NU` | `NU` | `NU` |  |  |  | `NB` | `NB` | `NB` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  | `YM` | `DS` |  |  |
| NATIVE_INTEGER | `NU` | `NU` | `NU` |  |  |  | `NB` | `NB` | `NB` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  | `YM` | `DS` |  |  |
| NATIVE_BIGINT | `NU` | `NU` | `NU` |  |  |  | `NB` | `NB` | `NB` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  | `YM` | `DS` |  |  |
| NATIVE_REAL | `NU` | `NU` | `NU` |  |  |  | `ND` | `ND` | `ND` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  |  |  |  |  |
| NATIVE_DOUBLE | `ND` | `ND` | `ND` |  |  |  | `ND` | `ND` | `ND` | `ND` | `ND` | `ND` | `ND` | `ND` |  |  |  |  |  |  |  |  |  |
| NUMBER | `NU` | `NU` | `NU` |  |  |  | `NU` | `NU` | `NU` | `NU` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  | `YM` | `DS` |  |  |
| NUMERIC | `NU` | `NU` | `NU` |  |  |  | `NU` | `NU` | `NU` | `NU` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  | `YM` | `DS` |  |  |
| FLOAT | `NU` | `NU` | `NU` |  |  |  | `NU` | `NU` | `NU` | `NU` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  | `YM` | `DS` |  |  |
| DATE | `DA` | `DA` | `DA` |  |  |  |  |  |  |  |  |  |  |  | `DA` |  |  | `TS` | `SZ` |  |  |  |  |
| TIME | `TI` | `TI` | `TI` |  |  |  |  |  |  |  |  |  |  |  |  | `TI` | `TZ` |  |  |  |  |  |  |
| TIME_TZ | `TZ` | `TZ` | `TZ` |  |  |  |  |  |  |  |  |  |  |  |  | `TZ` | `TZ` |  |  |  |  |  |  |
| TIMESTAMP | `TS` | `TS` | `TS` |  |  |  |  |  |  |  |  |  |  |  | `TS` |  |  | `TS` | `SZ` |  |  |  |  |
| TIMESTAMP_TZ | `SZ` | `SZ` | `SZ` |  |  |  |  |  |  |  |  |  |  |  | `SZ` |  |  | `SZ` | `SZ` |  |  |  |  |
| INTERVAL_YM | `YM` | `YM` | `YM` |  |  |  | `YM` | `YM` | `YM` |  |  | `YM` | `YM` | `YM` |  |  |  |  |  | `YM` |  |  |  |
| INTERVAL_DS | `DS` | `DS` | `DS` |  |  |  | `DS` | `DS` | `DS` |  |  | `DS` | `DS` | `DS` |  |  |  |  |  |  | `DS` |  |  |
| BOOLEAN | `BO` | `BO` | `BO` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `BO` |  |
| ROWID | `RI` | `RI` | `RI` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `RI` |

**Type conversion for the VC comparison**

<a id="79d1fa8deb20f282"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | CHAR (no conversion) |
| VARCHAR | VARCHAR (no conversion) |

**Type conversion for the LC comparison**

<a id="5a050c4af4f13572"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | CHAR (no conversion) |
| VARCHAR | VARCHAR (no conversion) |
| LONG VARCHAR | LONG VARCHAR (no conversion) |

**Type conversion for the VB comparison**

<a id="c41dfe9966c042ab"></a>
| Source type | Converted type |
| --- | --- |
| BINARY | BINARY (no conversion) |
| VARBINARY | VARBINARY (no conversion) |

**Type conversion for the LB comparison**

<a id="85cf3ef88c911ba2"></a>
| Source type | Converted type |
| --- | --- |
| BINARY | BINARY (no conversion) |
| VARBINARY | VARBINARY (no conversion) |
| LONG VARBINARY | LONG VARBINARY (no conversion) |

**Type conversion for the NB comparison**

<a id="ac9f662dba1fc61d"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | NATIVE_BIGINT |
| VARCHAR | NATIVE_BIGINT |
| LONG VARCHAR | NATIVE_BIGINT |
| NATIVE_SMALLINT | NATIVE_SMALLINT (no conversion) |
| NATIVE_INTEGER | NATIVE_INTEGER (no conversion) |
| NATIVE_BIGINT | NATIVE_BIGINT (no conversion) |

**Type conversion for the ND comparison**

<a id="36f0605d1c5c04d6"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | NATIVE_DOUBLE |
| VARCHAR | NATIVE_DOUBLE |
| LONG VARCHAR | NATIVE_DOUBLE |
| NATIVE_SMALLINT | NATIVE_SMALLINT (no conversion) |
| NATIVE_INTEGER | NATIVE_INTEGER (no conversion) |
| NATIVE_BIGINT | NATIVE_BIGINT (no conversion) |
| NATIVE_REAL | NATIVE_REAL (no conversion) |
| NATIVE_DOUBLE | NATIVE_DOUBLE (no conversion) |
| NUMBER | NUMBER (no conversion) |
| NUMERIC | NUMERIC (no conversion) |
| FLOAT | FLOAT (no conversion) |

**Type conversion for the NU comparison**

<a id="1a0e53360f2c240b"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | NUMBER |
| VARCHAR | NUMBER |
| LONG VARCHAR | NUMBER |
| NATIVE_SMALLINT | NATIVE_SMALLINT (no conversion) |
| NATIVE_INTEGER | NATIVE_INTEGER (no conversion) |
| NATIVE_BIGINT | NATIVE_BIGINT (no conversion) |
| NATIVE_REAL | NATIVE_REAL (no conversion) |
| NATIVE_DOUBLE | NATIVE_DOUBLE (no conversion) |
| NUMBER | NUMBER (no conversion) |
| NUMERIC | NUMERIC (no conversion) |
| FLOAT | FLOAT (no conversion) |

**Type conversion for the DA comparison**

<a id="793ebc4518cbdf3c"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | DATE |
| VARCHAR | DATE |
| LONG VARCHAR | DATE |
| DATE | DATE (no conversion) |

**Type conversion for the TI comparison**

<a id="02eebddd22bbc49c"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | TIME |
| VARCHAR | TIME |
| LONG VARCHAR | TIME |
| TIME | TIME (no conversion) |

**Type conversion for the TZ comparison**

<a id="f91e528a19b267d1"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | TIME_TZ |
| VARCHAR | TIME_TZ |
| LONG VARCHAR | TIME_TZ |
| TIME | TIME_TZ |
| TIME_TZ | TIME_TZ (no conversion) |

**Type conversion for the TS comparison**

<a id="c202263a86eae381"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | TIMESTAMP |
| VARCHAR | TIMESTAMP |
| LONG VARCHAR | TIMESTAMP |
| DATE | DATE (no conversion) |
| TIMESTAMP | TIMESTAMP (no conversion) |

**Type conversion for the SZ comparison**

<a id="6db8805f6f242116"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | TIMESTAMP_TZ |
| VARCHAR | TIMESTAMP_TZ |
| LONG VARCHAR | TIMESTAMP_TZ |
| DATE | TIMESTAMP_TZ |
| TIMESTAMP | TIMESTAMP_TZ |
| TIMESTAMP_TZ | TIMESTAMP_TZ (no conversion) |

**Type conversion for the YM comparison**

<a id="efd0d3938a7c7387"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | INTERVAL_YM |
| VARCHAR | INTERVAL_YM |
| LONG VARCHAR | INTERVAL_YM |
| NATIVE_SMALLINT | INTERVAL_YM |
| NATIVE_INTEGER | INTERVAL_YM |
| NATIVE_BIGINT | INTERVAL_YM |
| NUMBER | INTERVAL_YM |
| NUMERIC | INTERVAL_YM |
| FLOAT | INTERVAL_YM |
| INTERVAL_YM | INTERVAL_YM (no conversion) |

**Type conversion for the DS comparison**

<a id="5a2e4f371c185701"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | INTERVAL_DS |
| VARCHAR | INTERVAL_DS |
| LONG VARCHAR | INTERVAL_DS |
| NATIVE_SMALLINT | INTERVAL_DS |
| NATIVE_INTEGER | INTERVAL_DS |
| NATIVE_BIGINT | INTERVAL_DS |
| NUMBER | INTERVAL_DS |
| NUMERIC | INTERVAL_DS |
| FLOAT | INTERVAL_DS |
| INTERVAL_DS | INTERVAL_DS (no conversion) |

**Type conversion for the BO comparison**

<a id="c053498dca1f2806"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | BOOLEAN |
| VARCHAR | BOOLEAN |
| LONG VARCHAR | BOOLEAN |
| BOOLEAN | BOOLEAN (no conversion) |

**Type conversion for the RI comparison**

<a id="5d40f79ad66d9822"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | ROWID |
| VARCHAR | ROWID |
| LONG VARCHAR | ROWID |
| ROWID | ROWID (no conversion) |

<a id="ee64dd045e8e2ced"></a>
### Type Conversion

Type conversions are classified into implicit type conversion and explicit type conversion.

- Implicit type conversion occurs in an expression, an operator, a function, a condition, for select, insert, delete, update.
- Explicit type conversion occurs through the CAST operator.

[The availability of type conversion](#ad29b8ebab2276b8) describes the availability of data type conversion from a type to another type.

> In the type conversion table, the built-in data types are represented by an abbreviated string enclosed in double quotes ("").
> 
> - "CHAR": CHARACTER
> - "VARCHAR": CHARACTER VARYING
> - "LONG VARCHAR": CHARACTER LONG VARYING
> - "VARBINARY": BINARY VARYING
> - "LONG VARBINARY": BINARY LONG VARYING
> - "TIME_TZ": TIME WITH TIMEZONE
> - "TIMESTAMP_TZ": TIMESTAMP WITH TIMEZONE
> - "INTERVAL_YM": INTERVAL YEAR TO MONTH
> - "INTERVAL_DS": INTERVAL DAY TO SECOND
> 

**The availability of type conversion**

<a id="ad29b8ebab2276b8"></a>
| Data type | C H A R | V A R C H A R | L O N G  V A R C H A R | B I N A R Y | V A R B I N A R Y | L O N G  V A R B I N A R Y | N A T I V E  S M A L L I N T | N A T I V E  I N T E G E R | N A T I V E  B I G I N T | N A T I V E  R E A L | N A T I V E  D O U B L E | N U M B E R | N U M E R I C | F L O A T | D A T E | T I M E | T I M E    T Z | T I M E S T A M P | T I M E S T A T M P   T Z | I N T E R V A L  Y M | I N T E R V A L  D S | B O O L E A N | R O W I D |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CHAR | O | O | O |  |  |  | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O |
| VARCHAR | O | O | O |  |  |  | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O |
| LONG VARCHAR | O | O | O |  |  |  | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O |
| BINARY |  |  |  | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| VARBINARY |  |  |  | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| LONG VARBINARY |  |  |  | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| NATIVE_SMALLINT | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  | O | O |  |  |
| NATIVE_INTEGER | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  | O | O |  |  |
| NATIVE_BIGINT | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  | O | O |  |  |
| NATIVE_REAL | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  |  |  |  |  |
| NATIVE_DOUBLE | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  |  |  |  |  |
| NUMBER | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  | O | O |  |  |
| NUMERIC | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  | O | O |  |  |
| FLOAT | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  | O | O |  |  |
| DATE | O | O | O |  |  |  |  |  |  |  |  |  |  |  | O |  |  | O | O |  |  |  |  |
| TIME | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  | O | O |  |  |  |  |  |  |
| TIME_TZ | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  | O | O |  |  |  |  |  |  |
| TIMESTAMP | O | O | O |  |  |  |  |  |  |  |  |  |  |  | O | O |  | O | O |  |  |  |  |
| TIMESTAMP_TZ | O | O | O |  |  |  |  |  |  |  |  |  |  |  | O | O | O | O | O |  |  |  |  |
| INTERVAL_YM | O | O | O |  |  |  | O | O | O |  |  | O | O | O |  |  |  |  |  | O |  |  |  |
| INTERVAL_DS | O | O | O |  |  |  | O | O | O |  |  | O | O | O |  |  |  |  |  |  | O |  |  |
| BOOLEAN | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | O |  |
| ROWID | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | O |

- Conversion to CHARACTER type
    - When the source type is CHARACTER type:
        - If the source type precision is bigger than the CHARACTER type precision, then an error occurs.
        - If the source type precision is equal to the CHARACTER type precision, then the string is not changed.
        - If the source type precision is smaller than the CHARACTER type precision, then space characters are added to the string as many as the precision difference.
    - When the source type is CHARACTER VARYING type or CHARACTER LONG VARYING type:
        - If the source type string length is bigger than the CHARACTER type precision, then an error occurs.
        - If the source type string length is equal to the CHARACTER type precision, then the string is not changed.
        - If the source type string length is smaller than the CHARACTER type precision, then space characters are added to the string as many as precision difference.
    - When the source type is numeric type, date/time type, INTERVAL type, BOOLEAN type or ROWID type:
        - If the converted string length of the source type is bigger than the CHARACTER type precision, then an error occurs.
        - If the converted string length of the source type is equal to the CHARACTER type precision, the string is not changed.
        - If the converted string length of the source type is smaller than the CHARACTER type precision, then space characters are added to the string as many as precision difference.

- Conversion to CHARACTER VARYING type
    - When the source type is CHARACTER type:
        - If the source type precision is bigger than the CHARACTER VARYING type precision, then an error occurs.
        - If the source type precision is equal or smaller than the CHARACTER VARYING type precision, then the string is not changed.
    - When the source type is CHARACTER VARYING type or CHARACTER LONG VARYING type:
        - If the source type string length is bigger than the CHARACTER VARYING type precision, then an error occurs.
        - If the source type string length is equal or smaller than the CHARACTER VARYING type precision, then the string is not changed.
    - When the source type is numeric type, date/time type, INTERVAL type, BOOLEAN type or ROWID type:
        - If the converted string length of the source type is bigger than the CHARACTER VARYING type precision, then an error occurs.
        - If the converted string length of the source type is equal or smaller than the CHARACTER VARYING type precision, then the string is not changed.

- Conversion to CHARACTER LONG VARYING type
    - When the source type is CHARACTER STRING type:
        - The source type string is not changed.
    - When the source type is numeric type, date/time type, INTERVAL type, BOOLEAN type or ROWID type:
        - The converted string of the source type is not changed.

- Conversion to BINARY type 
    - When the source type is BINARY type: 
        - If the source type precision is bigger than the BINARY type precision, then an error occurs.
        - If the source type precision is equal to the BINARY type precision, then the binary string is not changed. 
        - If the source type precision is smaller than the BINARY type precision, the X'00' characters are added to the binary string as many as the precision difference.
    - When the source type is BINARY VARYING type or BINARY LONG VARYING type: 
        - If the source type binary string length is bigger than the BINARY type precision, then an error occurs.
        - If the source type binary string length is equal to the BINARY type precision, then the binary string is not changed. 
        - If the source type binary string length is smaller than the BINARY type precision, the X'00' characters are added to a binary string as many as precision difference.

- Conversion to BINARY VARYING type 
    - When the source type is BINARY type: 
        - If the source type precision is bigger than the BINARY VARYING type precision, then an error occurs. 
        - If the source type precision is equal or smaller than the BINARY VARYING type precision, then the binary string is not changed.
    - When the source type is BINARY VARYING type, BINARY LONG VARYING type: 
        - If the source type binary string length is bigger than the BINARY VARYING type precision, then an error occurs.
        - If the source type binary string length is equal or smaller than the BINARY VARYING type precision, the binary string is not changed.

- Conversion to BINARY LONG VARYING type 
    - If the source type is BINARY STRING type, the source type binary string is not changed.

- Conversion to numeric type
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the numeric format, then an error occurs. 
        - An overflow or rounding can occur due to the precision and scale which is defined in the converted type.
    - When the source type is numeric type: 
        - An overflow or rounding can occur due to the precision and scale which is defined in the converted type.
    - When the source type is INTERVAL type: 
        - It can be converted to the numeric type only when the source type is the single field (YEAR, MONTH, DAY, HOUR, MINUTE, SECOND).
        - An overflow or rounding can occur due to the precision and scale which is defined in the converted type.

- Conversion to DATE type
    - When the source type is CHARACTER STRING type:
        - If the string does not comply with the DATE type format, then an error occurs.
        - An overflow can occur due to a value range which is defined in the converted type.
    - When the source type is DATE type or TIMESTAMP type:
        - The error does not occur.
    - When the source type is TIMESTAMP WITH TIME ZONE type:
        - It is converted to the DATE type value upon consideration of the time zone offset.

- Conversion to TIME type 
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the TIME type format, then an error occurs. 
        - A rounding can occur due to a value range which is defined in the converted type.
    - When the source type is TIME type or TIMESTAMP type: 
        - The error does not occur.
    - When the source type is TIME WITH TIME ZONE type or TIMESTAMP WITH TIME ZONE type: 
        - It is converted to the value of TIME type upon consideration of the time zone offset.

- Conversion to TIME WITH TIME ZONE type 
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the TIME WITH TIME ZONE type format, then an error occurs. 
        - A rounding can occur due to a value range which is defined in the converted type.
    - When the source type is TIME type, TIME WITH TIME ZONE type or TIMESTAMP WITH TIME ZONE type: 
        - It is converted to the value of TIME WITH TIME ZONE type upon consideration of the time zone offset.

- Conversion to TIMESTAMP type 
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the TIMESTAMP type format, then an error occurs. 
        - An overflow or rounding can occur due to a value range which is defined in the converted type.
    - When the source type is DATE type or TIMESTAMP type:
        - The error does not occur.
    - When the source type is TIMESTAMP WITH TIME ZONE type: 
        - It is converted to the TIMESTAMP type value upon consideration of the time zone offset.

- Conversion to TIMESTAMP WITH TIME ZONE type 
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the TIMESTAMP WITH TIME ZONE type format, then an error occurs. 
        - An overflow or rounding can occur due to a value range which is defined in the converted type.
    - When the source type is DATE type, TIMESTAMP type or TIMESTAMP WITH TIME ZONE type: 
        - It is converted to the value of TIMESTAMP WITH TIME ZONE type upon consideration of the time zone offset.

- Conversion to INTERVAL YEAR TO MONTH family type
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the year-month interval literal format, then an error occurs. 
        - For more information, refer to [Interval Literals](#3e1e94e284d2f9d2).
        - An overflow can occur due to a precision which is defined in the converted type.
    - When the source type is NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, NUMBER, NUMERIC or FLOAT type: 
        - The converted type should be a single field (YEAR, MONTH).
        - An overflow can occur due to a precision which is defined in the converted type.
    - When the source type is INTERVAL YEAR TO MONTH family type: 
        - An overflow can occur due to a precision which is defined in the converted type.

- Conversion to INTERVAL DAY TO SECOND family type 
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the day-time interval literal format, then an error occurs. 
        - For more information, refer to [Interval Literals](#3e1e94e284d2f9d2).
        - An overflow or rounding can occur due to the precision which is defined in the converted type.
    - When the source type is NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, NUMBER, NUMERIC, or FLOAT type:
        - The converted type should be a single field (DAY, HOUR, MINUTE, SECOND)
        - An overflow or rounding can occur due to the precision which is defined in the converted type.
    - When the source type is INTERVAL DAY TO SECOND family type: 
        - An overflow or rounding can occur due to the precision which is defined in the converted type.

- Conversion to BOOLEAN type 
    - When the source type is CHARACTER STRING type: 
        - The conversion is available when the string is "TRUE" or "FALSE", and it is case-insensitive. (It is convertible even when the string includes a space before and after it.) 
    - When the source type is BOOLEAN type: 
        - The error does not occur.

- Conversion to ROWID type 
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the ROWID type format, then an error occurs. 
    - When the source type is ROWID type: 
        - The error does not occur.

<a id="1a3089b8bd544ccc"></a>
### Type Combination

<a id="fbbf7a3bc1538a84"></a>
#### When Type Combination Is Required

A CASE operator and a [set operator](16-sql-references.md#ab0a1ea34982332b) have many expressions as a result of operation.  
Each expression can have different types each other as follows. In this case, the result type should be determined.

- The following describes an execution result of a CASE operator.

```
SELECT CASE expr WHEN expr THEN char(3)
                 WHEN expr THEN char(5)
                 ELSE char(1)
       END   
  FROM t1;
```

- The following describes an execution result of a set operator.

```
SELECT float_column
  FROM t1
UNION ALL
SELECT number_precision_column
  FROM t2
UNION ALL
SELECT native_integer_column
  FROM t3;
```

A rule is applied to determine the result type according to the type combination. The following is an example of applying the rule.

- Result type combination rule
    - [set operator](16-sql-references.md#ab0a1ea34982332b)
    - CASE operator
        - [CASE Expression](#d8dbcaa9e4c75351)
        - [COALESCE](#2f66c19ba9c3c73f)
        - [NULLIF](#68b32611305a934d)

<a id="7b9ef315990930de"></a>
#### Result Type Combination Rule

Each expression's data type should be the same family type which is available to combine.

- Examples of applying result type combination rule
    - [set operator](16-sql-references.md#ab0a1ea34982332b)
    - CASE operator
        - [CASE Expression](#d8dbcaa9e4c75351)
        - [COALESCE](#2f66c19ba9c3c73f)
        - [NULLIF](#68b32611305a934d)

The result types determined by result type combination rule are described in the following table.

> The following abbreviations are used to describe the result type combination rule.
> 
> - "VC": CHARACTER VARYING
> - "LC": CHARACTER LONG VARYING
> - "VB": BINARY VARYING
> - "LB": BINARY LONG VARYING
> - "NS": NATIVE_SMALLINT
> - "NI": NATIVE_INTEGER
> - "NB": NATIVE_BIGINT
> - "NR": NATIVE_REAL
> - "ND": NATIVE_DOUBLE
> - "FL": FLOAT
> - "NU": NUMBER
> - "DA": DATE
> - "TI": TIME
> - "TZ": TIME WITH TIMEZONE
> - "TS": TIMESTAMP
> - "SZ": TIMESTAMP WITH TIMEZONE
> - "YM": INTERVAL YEAR TO MONTH
> - "DS": INTERVAL DAY TO SECOND
> - "BO": BOOLEAN
> - "RI": ROWID
> 

> In result type combination table, the built-in data types are represented by an abbreviated word enclosed in double quotes ("").
> 
> - "CHAR": CHARACTER
> - "VARCHAR": CHARACTER VARYING
> - "LONG VARCHAR": CHARACTER LONG VARYING
> - "BINARY": BINARY
> - "VARBINARY": BINARY VARYING
> - "LONG VARBINARY": BINARY LONG VARYING
> - "TIME_TZ": TIME WITH TIMEZONE
> - "TIMESTAMP_TZ": TIMESTAMP WITH TIMEZONE
> - "INTERVAL_YM": INTERVAL YEAR TO MONTH
> - "INTERVAL_DS": INTERVAL DAY TO SECOND
> 

**The result type determined by result type combination rule**

<a id="5e06907455cd69e1"></a>
| Data type | C H A R | V A R C H A R | L O N G  V A R C H A R | B I N A R Y | V A R B I N A R Y | L O N G  V A R B I N A R Y | N A T I V E  S M A L L I N T | N A T I V E  I N T E G E R | N A T I V E  B I G I N T | N A T I V E  R E A L | N A T I V E  D O U B L E | N U M B E R | N U M E R I C | F L O A T | D A T E | T I M E | T I M E    T Z | T I M E S T A M P | T I M E S T A T M P   T Z | I N T E R V A L  Y M | I N T E R V A L  D S | B O O L E A N | R O W I D |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CHAR | `VC` | `VC` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| VARCHAR | `VC` | `VC` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| LONG VARCHAR |  |  | `LC` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| BINARY |  |  |  | `VB` | `VB` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| VARBINARY |  |  |  | `VB` | `VB` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| LONG VARBINARY |  |  |  |  |  | `LB` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| NATIVE_SMALLINT |  |  |  |  |  |  | `NS` | `NI` | `NB` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  |  |  |  |  |
| NATIVE_INTEGER |  |  |  |  |  |  | `NI` | `NI` | `NB` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  |  |  |  |  |
| NATIVE_BIGINT |  |  |  |  |  |  | `NB` | `NB` | `NB` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  |  |  |  |  |
| NATIVE_REAL |  |  |  |  |  |  | `ND` | `ND` | `ND` | `NR` | `ND` | `ND` | `ND` | `ND` |  |  |  |  |  |  |  |  |  |
| NATIVE_DOUBLE |  |  |  |  |  |  | `ND` | `ND` | `ND` | `ND` | `ND` | `ND` | `ND` | `ND` |  |  |  |  |  |  |  |  |  |
| NUMBER |  |  |  |  |  |  | `NU` | `NU` | `NU` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  |  |  |  |  |
| NUMERIC |  |  |  |  |  |  | `NU` | `NU` | `NU` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  |  |  |  |  |
| FLOAT |  |  |  |  |  |  | `NU` | `NU` | `NU` | `ND` | `ND` | `NU` | `NU` | `FL ` |  |  |  |  |  |  |  |  |  |
| DATE |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `DA` |  |  | `TS` | `SZ` |  |  |  |  |
| TIME |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `TI` | `TZ` |  |  |  |  |  |  |
| TIME_TZ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `TZ` | `TZ` |  |  |  |  |  |  |
| TIMESTAMP |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `TS` |  |  | `TS` | `SZ` |  |  |  |  |
| TIMESTAMP_TZ |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `SZ` |  |  | `SZ` | `SZ` |  |  |  |  |
| INTERVAL_YM |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `YM` |  |  |  |
| INTERVAL_DS |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `DS` |  |  |
| BOOLEAN |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `BO` |  |
| ROWID |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `RI` |

- The result type of when all is CHAR type
    - If the lengths are different, then it is VARCHAR type.
    - If the lengths are equal, then it is CHAR type.
- The result type of when all is BINARY type
    - If the lengths are different, then it is VARBINARY type.
    - If the lengths are equal, then it is BINARY type.
- The result type of INTERVAL YEAR TO MONTH type
    - If YEAR type and MONTH type are mixed, then it is INTERVAL YEAR TO MONTH type.
    - If there is only YEAR type, then it is INTERVAL YEAR type.
    - If there is only MONTH type, then it is INTERVAL MONTH type.
- The result type of INTERVAL DAY TO SECOND type 
    - The start field is the biggest range field of each target expression.
    - The end field is the smallest range field of each target expression.
    - e.g. {INTERVAL DAY, INTERVAL HOUR} => INTERVAL DAY TO HOUR
- The precision, scale of the result type
    - CHARACTER STRING type
        - The maximum character length of the target expression
    - BINARY STRING type
        - The maximum character length of the target expression
    - NUMERIC type
        - It specifies an acceptable maximum range of the type's value.
    - TIME/TIMESTAMP type
        - The maximum fractional seconds precision of the target expression
    - INTERVAL YEAR TO MONTH
        - The maximum leading precision of the target expression
    - INTERVAL DAY TO SECOND
        - Leading precision is the maximum leading precision of the start field
        - Fractional seconds precision is the maximum fractional seconds precision.
- For more information, refer to [Type Comparison](#0b812e6987dc67cb).

<a id="413757a6449a20cd"></a>
### Compatibility for Data Type

The SQL standard compatibility for data type is as follows.

**SQL standard compatibility for data type**

<a id="d42b5c646a0a2a56"></a>
| Feature ID | Description | Availability |
| --- | --- | --- |
| B033 | Untyped SQL-invoked function arguments | X |
| E011-01 | INTEGER and SMALLINT data types | O |
| E011-02 | REAL, DOUBLE PRECISION, and FLOAT data types | O |
| E011-03 | DECIMAL and NUMERIC data types | X |
| E011-04 | Arithmetic operators | O |
| E011-05 | Numeric comparison | O |
| E011-06 | Implicit casting among the numeric data types | O |
| E021-01 | CHARACTER data type | O |
| E021-02 | CHARACTER VARYING data type | O |
| E021-03 | Character literals | O |
| E021-04 | CHARACTER_LENGTH function | O |
| E021-05 | OCTET_LENGTH function | O |
| E021-06 | SUBSTRING function | O |
| E021-07 | Character concatenation | O |
| E021-08 | UPPER and LOWER functions | O |
| E021-09 | TRIM function | O |
| E021-10 | Implicit casting among the fixed-length and variable-length character string types | O |
| E021-11 | POSITION function | O |
| E021-12 | Character comparison | O |
| E071-05 | Columns combined via table operators need not have exactly the same data type | O |
| F051-01 | DATE data type (including support of DATE literal) | O |
| F051-02 | TIME data type (including support of TIME literal) with fractional seconds precision of at least 0 | O |
| F051-03 | TIMESTAMP data type (including support of TIMESTAMP literal) with fractional seconds precision of at least 0 and 6 | O |
| F051-04 | Comparison predicate on DATE, TIME, and TIMESTAMP data types | X |
| F051-05 | Explicit CAST between datetime types and character string types | O |
| F054 | TIMESTAMP in DATE type precedence list | X |
| F382 | Alter column data type | O |
| F611 | Indicator data types | X |
| F741 | Referential MATCH types | X |
| J521 | JDBC data types | X |
| J622 | external Java types | X |
| S011-01 | USER_DEFINED_TYPES view | X |
| S023 | Basic structured types | X |
| S024 | Enhanced structured types | X |
| S025 | Final structured types | X |
| S026 | Self-referencing structured types | X |
| S041 | Basic reference types | X |
| S043 | Enhanced reference types | X |
| S051 | Create table of type | X |
| S071 | SQL paths in function and type name resolution | X |
| S091-01 | Arrays of built-in data types | X |
| S091-02 | Arrays of distinct types | X |
| S092 | Arrays of user-defined types | X |
| S094 | Arrays of reference types | X |
| S161 | Subtype treatment | X |
| S162 | Subtype treatment for references | X |
| S201-02 | Array as result type of functions | X |
| S231 | Structured type locators | X |
| S261 | Specific type method | X |
| S272 | Multisets of user-defined types | X |
| S274 | Multisets of reference types | X |
| S281 | Nested collection types | X |
| S401 | Distinct types based on array types | X |
| S402 | Distinct types based on distinct types | X |
| T021 | BINARY and VARBINARY data types | O |
| T022 | Advanced support for BINARY and VARBINARY data types | O |
| T031 | BOOLEAN data type | O |
| T041 | Basic LOB data type support | X |
| T042 | Extended LOB data type support | X |
| T051 | Row types | X |
| T071 | BIGINT data type | O |
| T201 | Comparable data types for referential constraints | X |
| T322 | Declared data type attributes | X |
| X010 | XML type | X |
| X011 | Arrays of XML type | X |
| X012 | XMultisets of XML type | X |
| X013 | Distinct types of XML type | X |
| X014 | Attributes of XML type | X |
| X015 | Fields of XML type | X |
| X181 | XML(DOCUMENT(UNTYPED)) type | X |
| X182 | XML(DOCUMENT(ANY)) type | X |
| X190 | XML(SEQUENCE) type | X |
| X191 | XML(DOCUMENT(XMLSCHEMA)) type | X |
| X192 | XML(CONTENT(XMLSCHEMA)) type | X |
| X231 | XML(CONTENT(UNTYPED)) type | X |
| X232 | XML(CONTENT(ANY)) type | X |
| X251 | Persistent XML values of XML(DOCUMENT(UNTYPED)) type | X |
| X252 | Persistent XML values of XML(DOCUMENT(ANY)) type | X |
| X253 | Persistent XML values of XML(CONTENT(UNTYPED)) type | X |
| X254 | Persistent XML values of XML(CONTENT(ANY)) type | X |
| X255 | Persistent XML values of XML(SEQUENCE) type | X |
| X256 | Persistent XML values of XML(DOCUMENT(XMLSCHEMA)) type | X |
| X257 | Persistent XML values of XML(CONTENT(XMLSCHEMA)) type | X |
| X260 | XML type: ELEMENT clause | X |
| X261 | XML type: NAMESPACE without ELEMENT clause | X |
| X263 | XML type: NO NAMESPACE with ELEMENT clause | X |
| X264 | XML type: schema location | X |
| X410 | Alter column data type: XML type | X |

<a id="4aabeb20675356f5"></a>
## Format String

Format string defines the format which is used when a numeric type or date/time type is converted to a character string or when a character string is converted to a numeric types or date/time type.

- When a numeric type or date/time type is converted to a character string type, the representation format of the string is as follows.
    - Refer to [TO_CHAR( number )](#949621fdd02e5356), [TO_CHAR( datetime )](#9688fd0405cae768).
    - Numeric type: TO_CHAR( 1234.56, 'S9,999.99' ) → '+1,234.56'
    - Date/time type: TO_CHAR( SYSDATE, 'YYYY-MM-DD' ) → '2012-07-15'
- When a character string is converted to the numeric type or date/time type, the representation format of the string is as follows.
    - Refer to [TO_NUMBER](#491715806db53986), [TO_NATIVE_REAL](#0cf01e33445e03e5), [TO_NATIVE_DOUBLE](#d03ab835f5df2038).
    - Refer to [TO_DATE](#25eb6843029ae86c).
    - Refer to [TO_TIMESTAMP](#3e1f1636fafd674a), [TO_TIMESTAMP_WITH_TIME_ZONE](#77a90650f33e49f9).
    - Refer to [TO_TIME](#d9a48ce329494e11), [TO_TIME_WITH_TIME_ZONE](#766da9ffc336d7e2) .
    - Numeric type: TO_NUMBER( '+1,234.56', 'S9,999.99' ) → NUMBER TYPE
    - Date/time type: TO_DATE( '2012-07-15', 'YYYY-MM-DD' ) → DATE TYPE

Format strings are classified according to the type.  
• Numeric data type: Refer to [Number Format String](#d1928fe9c7363ae1).  
• Date/time type: Refer to [Datetime Format String](#f23ffe951177a789).

<a id="d1928fe9c7363ae1"></a>
### Number Format String

Number format string defines the format which is used when a numeric type is converted to a character string type, or when a character string type is converted to a numeric type.

Number format string is used as an argument of the functions such as [TO_CHAR( number )](#949621fdd02e5356), [TO_NUMBER](#491715806db53986), [TO_NATIVE_REAL](#0cf01e33445e03e5), [TO_NATIVE_DOUBLE](#d03ab835f5df2038).

Number format string can specify multiple format elements according to the desired format.

All number format elements are rounded off to fit the format.  
If the number of digits before the decimal point of the value to be converted is bigger than the number of digits specified in the format string, then they are replaced with '#' character.  
If the format element representing the sign of MI, S, PR is not specified, a negative number returns - sign and a positive number returns a white space to the front of the number.

**Number format elements**

<a id="9a29b90232950ace"></a>
| Format  element | Example | Description |
| --- | --- | --- |
| , (comma) | 9,999 | It returns a comma to the specified position. Multiple commas can be specified. Format string can not begin with a comma, and it can not come after the decimal point (.). |
| . (period) | 99.99 | It returns a decimal point(.) to the specified position. The decimal point in the format string can be specified only once. |
| $ | $9999 | It returns the $ sign to the front of the number. |
| 0 | 0999  9990 | It returns zero(0) to the front of or to the end of the number.  If the number of digits of the value to be converted is smaller than the number of digits to the zero position of the format string, then the gap is filled with zero(0)s and is returned. |
| 9 | 9999 | It returns a white space and numbers according to the sign and the number of specified 9. If the number of digits of the value to be converted is smaller than the number of the specified 9, then the gap is filled with white spaces and is returned. For a positive number, a white space is returned to the front of the number. For a negative number, '-' symbol is returned to the front of the number. If the value before the format string's decimal point is 0, then 0 is returned as a white space. e.g. TO_CHAR( 0.123, '9.999' ) → .123 e.g. TO_CHAR( 0, '9' ) → 0 |
| B | B9999 | If the value is zero, it returns a white space. |
| EEEE | 9.9EEEE | It returns in exponential notation. It can be at the end of format string or it can be in front of S, MI, PR.  It can not be specified together with a comma (,). |
| MI | 9999MI | For a positive number, a white space is returned to the end of the number. For a negative number, '-' symbol is returned to the end of the number. It can be specified only at the end of format string and it can not be specified together with S, PR. |
| PR | 9999PR | For a positive number, white spaces are returned to the beginning and end of the number. For a negative number, it returns the number into the inside of angle brackets. &lt;number&gt;  It can be specified only at the end of format string, and it can not be specified together with S, MI. |
| RN  rn | RN rn | Roman numerals are converted to uppercase and returned. (RN) Roman numerals are converted to lowercase and returned. (rn) Only the numbers between 1 ~ 3999 are returned. It can be specified together only with FM format element, but it can not be specified with any other format elements. It can not be used in TO_NUMBER function. |
| S | S9999 9999S | For a positive number, '+' symbol is returned to the front of the number. For a negative number, '-' symbol is returned to the front of the number.(S9999 For a positive number, '+' symbol is returned to the end of the number. For a negative number, '-' symbol is returned to the end of the number.(9999S) It can be specified only at the beginning of format string or at the end of format string. It can not be specified together with MI, PR. |
| V | 999V99 | 10<sup>n</sup>(n: the digit number of 9 after V format element) multiplied by the value is returned.  It can not specified together with the decimal point (.). It can not be used in TO_NUMBER function. |
| X | XXXX xxxx | It returns the white space and hexadecimal number according to the digit number of the specified X. It converts an integer value to the hexadecimal number, and returns it. (A non-integer value is rounded off to make it to an integer value) XXX returns hexadecimal uppercase letters and xxxx returns hexadecimal lowercase letters. If the number of the converted hexadecimal digit is smaller than the number of the specified X, then the gap is filled with white spaces and is returned. Only 0 and positive integers are processed, and negative numbers are replaced with '#'. It can be specified together only with format element 0 and FM, but it can not be specified with any other format elements. |
| FM | FM | It removes the front and end white spaces, and returns left aligned effect. It removes the front and end white spaces of the number. It removes zero(0)s under the decimal point which are added by 9 format element. |

Followings are examples of using number format string.

```
TO_CHAR( 12345, '99,999' )           : ' 12,345'
TO_CHAR( 123456789, '999,999,999' )  : ' 123,456,789'
TO_CHAR( 12.345, '99.999' )          : ' 12.345'
TO_CHAR( 1234.56, '$9,999.99' )      : ' $1,234.56'
TO_CHAR( 123, '099999' )             : ' 000123'
TO_CHAR( 0.2, '0.9' )                : ' 0.2'
TO_CHAR( 123.45, '999999.99' )       : '    123.45'
TO_CHAR( -123.45, '999999.99' )      : '   -123.45'
TO_CHAR( 123.45, 'FM999999.99' )     : '123.45'
TO_CHAR( -123.45, 'FM999999.99' )    : '-123.45'
TO_CHAR( 12345.67, '999.99' )        : '#######'
TO_CHAR( 123.100567, '999.999' )     : ' 123.101'
TO_CHAR( 0.2, '90.99' )              : '  0.20'
TO_CHAR( 0.2, '99.99' )              : '   .20'
TO_CHAR( 0, '90.99' )                : '  0.00'
TO_CHAR( 0, 'B90.99' )               : '      '
TO_CHAR( 123.45, '9.9EEEE' )         : '  1.2E+02'
TO_CHAR( 123.45, '999.99MI' )        : '123.45 '
TO_CHAR( -123.45, '999.99MI' )       : '123.45-'
TO_CHAR( 123.45, '999.99PR' )        : ' 123.45 '
TO_CHAR( -123.45, '999.99PR' )       : '<123.45>'
TO_CHAR( 123, 'RN' )                 : '         CXXIII'
TO_CHAR( 123, 'rn' )                 : '         cxxiii'
TO_CHAR( 123, 'FMRN' )               : 'CXXIII'
TO_CHAR( 4000, 'RN' )                : '###############'
TO_CHAR( 123.45, 'S999.99' )         : '+123.45'
TO_CHAR( -123.45, 'S999.99' )        : '-123.45'
TO_CHAR( 123.45, '999.99S' )         : '123.45+'
TO_CHAR( -123.45, '999.99S' )        : '123.45-'
TO_CHAR( 123.45, '999V999' )         : ' 123450'
TO_CHAR( 123, 'XX' )                 : ' 7B'
TO_CHAR( 123, 'xx' )                 : ' 7b'
TO_CHAR( 45678, 'XXXXXXX' )          : '    B26E'
TO_CHAR( 45678, 'FMXXXXXXX' )        : 'B26E'
TO_CHAR( 123.45, '99,999.999999' )   : '    123.450000'
TO_CHAR( 123.45, 'FM99,999.999999' ) : '123.45'
```

<a id="f23ffe951177a789"></a>
### Datetime Format String

Datetime format string defines the format which is used when a date/time type is converted to a character string type, or when a character string type is converted to a date/time type.

Datetime format string is used as an argument of the functions such as [TO_CHAR( datetime )](#9688fd0405cae768), [TO_DATE](#25eb6843029ae86c), [TO_TIMESTAMP](#3e1f1636fafd674a), [TO_TIMESTAMP_WITH_TIME_ZONE](#77a90650f33e49f9), [TO_TIME](#d9a48ce329494e11), [TO_TIME_WITH_TIME_ZONE](#766da9ffc336d7e2).

For datetime format string, if the format string is not specified, then the default value is used. The default value of each type is specified in the session property (NLS _ * _ FORMAT).

- DATE: Refer to [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#6c5301741d86446c).
- TIMESTAMP: Refer to [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#f04f20ba0ffa3caf).
- TIMESTAMP WITH TIME ZONE: Refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#edba3110d229ce95).
- TIME: Refer to [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#3eb7e8d0be6c45dd).
- TIME WITH TIME ZONE: Refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#dc93f1addc88cbde).

NLS * _FORMAT values can be changed by using [ALTER SESSION SET property_name](16-sql-references.md#c7a0e93656726619).

In datetime format string, multiple format elements can be specified upon the desired representation.

**Datetime format elements**

<a id="940b4c1efbdc7feb"></a>
<table><thead><tr><th align="center" valign="middle">Format<br>element</th><th align="center" valign="middle">Whether to use TO_*<br>datetime</th><th align="center" valign="middle">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">-<br>/<br>,<br>.<br>;<br>:<br>"text"<br>Special characters</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the format element character to the specified location.</td></tr><tr><td align="left" valign="middle">AD<br>A.D.</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">AD with or without periods.</td></tr><tr><td align="left" valign="middle">AM<br>A.M.</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">AM with or without periods.</td></tr><tr><td align="left" valign="middle">BC<br>B.C.</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">BC with or without periods.</td></tr><tr><td align="left" valign="middle">CC</td><td align="left" valign="middle">N</td><td align="left" valign="middle">Century<br>If the last two digits of the four digits year is 01~ 99, the value which is added by one to the first two digits is returned. (e.g. If the year is 2005, 21 is returned.)<br>If the last two digits of the four digits year is 00, the first two digits value is returned. (e.g. If the year is 2000, 20 is returned.)</td></tr><tr><td align="left" valign="middle">D</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the sequence of the day in a week. (1 ~ 7)<br>Sunday is 1, saturday is 7, and so on.</td></tr><tr><td align="left" valign="middle">DAY<br>Day<br>day</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the day of the week. (e.g. SUNDAY)<br><ul><li>DAY: The day which is all in uppercase is returned.</li><li>Day: The day whose first character is uppercase and others are lowercase is returned.</li><li>day: The day which is all in lowercase is returned.</li></ul></td></tr><tr><td align="left" valign="middle">DD</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the sequence of the day in a month. (1 ~ 31)</td></tr><tr><td align="left" valign="middle">DDD</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the sequence of the day in a year. (1 ~ 366)</td></tr><tr><td align="left" valign="middle">DY<br>Dy<br>dy</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the abbreviated word for the day of the week. (e.g. SUN)<br><ul><li>DY: The day which is all in uppercase is returned.</li><li>Dy: The day whose first character is uppercase and others are lowercase is returned.</li><li>dy: The day which is all in lowercase is returned.</li></ul></td></tr><tr><td align="left" valign="middle">FF[1..6]</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns fractional seconds as many as the number of the specified digits (1-6) after FF.<br>If the number is not specified, the default value is 6. (FF is equal to FF6.)<br>If the number of fractional seconds digit is bigger than the number specified after FF, then it is rounded down.<br>If the number of fractional seconds digit is smaller than the number specified after FF, then zero(0) is added according to the specified number.<br>It can not be used in DATE type.</td></tr><tr><td align="left" valign="middle">HH<br>HH12</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">The hour (1 ~ 12)</td></tr><tr><td align="left" valign="middle">HH24</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">The hour (0 ~ 23)</td></tr><tr><td align="left" valign="middle">IW</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The week containing the first thursday of the year designated as the calendar week by ISO 8601 standards (1 ~ 52 weeks or 1 ~ 53 weeks) becomes the first week.<br><ul><li>The calendar week starts from monday.</li><li>The first calendar week includes January 4th.</li><li>The first calendar week may includes December 29th, 30th, and 31st.</li><li>The last calendar week may include January 1st, 2nd, and 3rd.</li></ul></td></tr><tr><td align="left" valign="middle">IYYY</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The 4 digits year embracing the calendar week defined by ISO 8601 standards.</td></tr><tr><td align="left">IYY<br>IY<br>I</td><td align="left" valign="middle">N</td><td align="left">The 3 digits year embracing the calendar week defined by ISO 8601 standards.<br>The 2 digits year embracing the calendar week defined by ISO 8601 standards.<br>The single digit year embracing the calendar week defined by ISO 8601 standards.</td></tr><tr><td align="left" valign="middle">J</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Julian day: The number of days since BC 4714-11-24</td></tr><tr><td align="left" valign="middle">MI</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Minute (0 ~ 59)</td></tr><tr><td align="left" valign="middle">MM</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Month (01 ~ 12), January(01)~December(12)</td></tr><tr><td align="left" valign="middle">MON<br>Mon<br>mon</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">The abbreviated word for the month. (e.g. JAN)<br><ul><li>MON: The month which is all in uppercase is returned.</li><li>Mon: The month whose first character is uppercase and others are lowercase is returned.</li><li>mon: The month which is all in lowercase is returned.</li></ul></td></tr><tr><td align="left" valign="middle">MONTH<br>Month<br>month</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">The month name (e.g. JANUARY)<br><ul><li>MONTH: All uppercase month name is returned.</li><li>Month: The month name that only the first letter is uppercase and others are lowercase is returned.</li><li>month: The month of which is all in lowercase is returned.</li></ul></td></tr><tr><td align="left" valign="middle">PM<br>P.M.</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">PM with or without periods.</td></tr><tr><td align="left" valign="middle">Q</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The quarter of the year (1 ~ 4)<br>January to March is 1 and October to December is 4.</td></tr><tr><td align="left" valign="middle">RM<br>Rm<br>rm</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the roman numeral month. (e.g. I)<br><ul><li>RM: The month which is all in uppercase is returned.</li><li>Rm: The month whose first character is uppercase and others are lowercase is returned.</li><li>rm: The month which is all in lowercase is returned.</li></ul></td></tr><tr><td align="left" valign="middle">RR</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Adjusted two digit year<br>The two digit year represented by RR can be converted to four digit year as follows.<br><ul><li>When the two digit year represented by RR is 00~49:<br><ul><li>If the last two digits of the current year is 00~50,<br><ul><li>the four digit year is represented using the first two digits of the current year and the two digits which is represented by RR.</li></ul></li><li>If the last two digits of the current year is 51~99,<br><ul><li>the four digit year is represented using "the first two digits of the current year+1" and the two digits which is represented by RR.</li></ul></li></ul></li><li>When the two digit year represented by RR is 50~99:<br><ul><li>If the last two digits of the current year is 00~50,<br><ul><li>the four digit year is represented using "the first two digit of the current year - 1" and the two digits which is represented by RR.</li></ul></li><li>If the last two digit of the current year is 51~99,<br><ul><li>the four digit year is expressed using the first two digit of the current year and the two digits which is represented by RR.</li></ul></li></ul></li></ul></td></tr><tr><td align="left" valign="middle">RRRR</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Adjusted four digit year<br>Two digit or four digit can be input.<br>Two digit input is processed in the same way as RR.</td></tr><tr><td align="left" valign="middle">SS</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Second (0 ~ 59)</td></tr><tr><td align="left" valign="middle">SSSSS</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Seconds since last midnight (0 ~ 86399)</td></tr><tr><td align="left" valign="middle">TZH</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Time Zone Hour<br>It can not be used in DATE, TIMESTAMP, TIME types. It is available in TIMESTAMP WITH TIME ZONE, TIME WITH TIME ZONE types.</td></tr><tr><td align="left" valign="middle">TZM</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Time Zone Minute<br>It can not be used in DATE, TIMESTAMP, TIME types. It can be used only in TIMESTAMP WITH TIME ZONE, TIME WITH TIME ZONE types.</td></tr><tr><td align="left" valign="middle">WW</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The sequence of the week in a year. (1~ 53)<br>The first week 1 starts on the first day of the year and continues to the seventh day of the year.</td></tr><tr><td align="left" valign="middle">W</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The sequence of the week in a month. (1 ~ 5)<br>The first week 1 starts on the first day of the month and ends on the seventh day.</td></tr><tr><td align="left" valign="middle">Y,YYY</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the year with comma in the Y,YYY form.</td></tr><tr><td align="left" valign="middle">YYYY<br>SYYYY</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Four digit year.<br>If it is BC, SYYYY returns '-' signal.</td></tr><tr><td align="left" valign="middle">YYY<br>YY<br>Y</td><td align="left" valign="middle">Y</td><td align="left" valign="middle"><ul><li>YYY: The last three digit year of the current year</li><li>YY: The last two digit year of the current year</li><li>Y: The last one digit year of the current year</li></ul></td></tr></tbody></table>

The followings are examples of using datetime format string.

```
* - / , . ; : "text" Special character 
  • TO_CHAR( TO_DATE( '2012-07-15 03:30:30', 'YYYY-MM-DD HH12:MI:SS' ),
             'YYYY/MM/DD HH12:MI:SS' )
    ==> '2012/07/15 03:30:30'
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 
             'YYYY"year" DDD"th day"' )
    ==> '2012year 197th day'
```

```
* AD
  • TO_CHAR( TO_DATE( '2012-07-15 AD', 'YYYY-MM-DD AD' ), 'YYYY AD' )
    ==> '2012 AD'
  • TO_CHAR( TO_DATE( '0001-01-01 BC', 'YYYY-MM-DD AD'), 'YYYY AD' )
    ==> '0001 BC'

* BC 
  • TO_CHAR( TO_DATE( '0001-01-01 BC', 'YYYY-MM-DD BC'), 'YYYY BC' )
    ==> '0001 BC'
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'YYYY BC' )
    ==> '2012 AD'
```

```
* AM
  • TO_CHAR( TO_DATE( '2012-07-15 03:30:30 AM',
                      'YYYY-MM-DD HH12:MI:SS AM' ),
             'HH12:MI:SS AM' )
    ==> '03:30:30 AM'
  • TO_CHAR( TO_DATE( '2012-07-15 21:30:30', 'YYYY-MM-DD HH24:MI:SS' ),
             'HH12:MI:SS AM' )
    ==> '09:30:30 PM'

* PM 
  • TO_CHAR( TO_DATE( '2012-07-15 03:30:30', 
                      'YYYY-MM-DD HH24:MI:SS' ), 
             'HH12:MI:SS PM' )
    ==> '03:30:30 AM'
  • TO_CHAR( TO_DATE( '2012-07-15 09:30:30 PM', 
                      'YYYY-MM-DD HH12:MI:SS PM' ), 
             'HH12:MI:SS PM' )
    ==> '09:30:30 PM'
```

```
* CC
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'CC' )
    ==> '21'
```

```
* D
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'D' )
    ==> '1'

* DD
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'DD' )
    ==>  '15'

* DDD
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'DDD' )
    ==> '197'
```

```
* DAY
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'DAY' )
    ==> 'SUNDAY   '
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'Day' )
    ==> 'Sunday   '
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'day' )
    ==> 'sunday   '

* DY
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'DY' )
    ==> 'SUN'
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'Dy' )
    ==> 'Sun'
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'dy' )
    ==> 'sun'
```

```
* FF[1 ... 6]
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 03:30:45.123456', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'FF' )
    ==> '123456'
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 03:30:45.123456', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'FF5' )
    ==> '12345'
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 03:30:45.9',
                           'YYYY-MM-DD HH24:MI.SS.FF1' ) , 
             'FF6' )
    ==> '900000'
```

```
* HH HH12 HH24
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 03:30:45.123456', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'HH12' )
    ==> '03'
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 23:30:45.123456', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'HH12' )
    ==> '11'
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 23:30:45.123456', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'HH24' )
    ==> '23'
```

```
* IW
  • TO_CHAR( DATE'2016-01-01', 'IW' )
    ==> 53
  • TO_CHAR( DATE'2014-12-30', 'IW' )
    ==> 01
```

```
* IYYY
  • TO_CHAR( DATE'2016-01-01', 'IYYY' )
    ==> 2015
  • TO_CHAR( DATE'2014-12-30', 'IYYY' )
    ==> 2015

* IYY
  • TO_CHAR( DATE'2016-01-01', 'IYY' )
    ==> 015

* IY
  • TO_CHAR( DATE'2016-01-01', 'IY' )
    ==> 15

* I
  • TO_CHAR( DATE'2016-01-01', 'I' )
    ==> 5
```

```
* J
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'J' )
    ==> '2456124'
  • TO_CHAR( TO_DATE( '2456124', 'J' ), 'YYYY-MM-DD' )
    ==> '2012-07-15'
```

```
* MI
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 23:30:45.123456', 
             'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'MI' ) 
    ==> '30'
```

```
* MM
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 23:30:45.123456', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'MM' )
    ==> '07'
```

```
* MON
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'MON' )
    ==> 'JUL'
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'Mon' )
    ==> 'Jul'
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'mon' )
    ==> 'jul'

* MONTH
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'MONTH' )
    ==> 'JULY     '
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'Month' )
    ==> 'July     '
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'month' )
    ==> 'july     '
```

```
* Q
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'Q' )
    ==> '3'
```

```
* RM
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'RM' )
    ==> 'VII ' 
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'Rm' )
    ==> 'Vii '
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'rm' )
    ==> 'vii '
```

```
* RR, RRRR ( The current year is 2014. )
  • TO_CHAR( TO_DATE( '49-07-15', 'RR-MM-DD' ), 'RRRR' )
    ==> '2049'
  • TO_CHAR( TO_DATE( '49-07-15', 'RR-MM-DD' ), 'YYYY' )
    ==> '2049'
  • TO_CHAR( TO_DATE( '50-07-15', 'RR-MM-DD' ), 'RRRR' )
    ==> '1950'
  • TO_CHAR( TO_DATE( '50-07-15', 'RR-MM-DD' ), 'YYYY' )
    ==> '1950'
  • TO_CHAR( TO_DATE( '50-07-15', 'YY-MM-DD' ), 'RRRR' )
    ==> '2050'
  • TO_CHAR( TO_DATE( '49-07-15', 'RRRR-MM-DD' ), 'YYYY' )
    ==> '2049'
  • TO_CHAR( TO_DATE( '50-07-15', 'RRRR-MM-DD' ), 'YYYY' )
    ==> '1950'

* RR, RRRR ( The current year is 2051. )
  • TO_CHAR( TO_DATE( '49-07-15', 'RR-MM-DD' ), 'RRRR' )
    ==> '2149'
  • TO_CHAR( TO_DATE( '49-07-15', 'RR-MM-DD' ), 'YYYY' )
    ==> '2149'
  • TO_CHAR( TO_DATE( '50-07-15', 'RR-MM-DD' ), 'RRRR' )
    ==> '2050'
  • TO_CHAR( TO_DATE( '50-07-15', 'RR-MM-DD' ), 'YYYY' )
    ==> '2050'
  • TO_CHAR( TO_DATE( '50-07-15', 'YY-MM-DD' ), 'RRRR' )
    ==> '2050'
  • TO_CHAR( TO_DATE( '49-07-15', 'RRRR-MM-DD' ), 'YYYY' )
    ==> '2149'
  • TO_CHAR( TO_DATE( '50-07-15', 'RRRR-MM-DD' ), 'YYYY' )
    ==> '2050'
```

```
* SS
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 23:30:45.123456',
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'SS' )
    ==> '45' 

* SSSSS
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 23:30:45.123456',
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'SSSSS' )
    ==> '84645'
```

```
* TZH 
  • TO_CHAR( TO_TIMESTAMP_TZ( '2012-07-15 23:30:45.123456 +09:00',
                              'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM' ),
             'TZH' )
    ==> '+09'

* TZM
  • TO_CHAR( TO_TIMESTAMP_TZ( '2012-07-15 23:30:45.123456 +09:00',
                              'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM' ),
             'TZM' )
    ==> '00'

  • TO_CHAR( TO_TIMESTAMP_TZ( '2012-07-15 23:30:45.123456 +09:00',
                              'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM' ),
             'TZH:TZM' )
    ==> '+09:00'
```

```
* WW
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'WW' )
    ==> '29'

* W
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'W' )
    ==> '3'
```

```
* Y,YYY
  • TO_CHAR( TO_DATE( '2,012-07-15', 'Y,YYY-MM-DD' ), 'Y,YYY' )
    ==> '2,012'

* YYYY
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'YYYY' )
    ==> '2012'

* SYYYY
  • TO_CHAR( TO_DATE( '-0001-01-01', 'SYYYY-MM-DD' ), 'SYYYY' )
    ==> '-0001' 

* YYY
  • TO_CHAR( TO_DATE( '012-07-15', 'YYY-MM-DD' ), 'YYY' )
    ==> '012'
  • TO_CHAR( TO_DATE( '012-07-15', 'YYY-MM-DD' ), 'YYYY' )
    ==> '2012' ( (Current year / 1000) is 2 )

* YY
  • TO_CHAR( TO_DATE( '12-07-15', 'YY-MM-DD' ), 'YY' )
    ==> '12'
  • TO_CHAR( TO_DATE( '12-07-15', 'YY-MM-DD' ), 'YYYY' )
    ==> '2012' ( (Current year / 100) is 20 ) 
    ==> '2112' ( (Current year / 100) is 21 ) 

* Y
  • TO_CHAR( TO_DATE( '2-07-15', 'Y-MM-DD' ), 'Y' )
    ==> '2'
  • TO_CHAR( TO_DATE( '12-07-15', 'YY-MM-DD' ), 'YYYY' )
    ==> '2012' ( (Current year / 10 years) is 201 )
    ==> '2052' ( (Current year / 10 years) is 205 )
```

<a id="f8c7dc95bb41226d"></a>
## Expressions

Expression is a combination of value, operator and function for getting data values.

The following is the position of the SQL commands in which expression can be used.  
• Target clause in SELECT  
• GROUP BY clause in SELECT  
• ORDER BY clause in SELECT  
• WHERE clause and HAVING clause in SELECT  
• INSERT VALUES clause  
• UPDATE SET clause  
• RETURN clause in INSERT, DELETE, UPDATE

Expression types are various as follows.  
• Simple expression  
• Compound expresssion  
• Boolean value expression  
• Case expression  
• Datetime expression  
• Scalar subquery expression  
• Sequence manipulation expression

Simple expressions are column, pseudo columns, literals, and null value.  
Compound expressions are combination of multiple expressions.

For more information, refer to the followings.  
•  [Null Value](#9ec3fc0fb5a0644d)  
•  [Literals](#5f90e3f36ae1d537)  
•  [Pseudo Columns](#03685b1e1567cf4c)  
•  [Operators](#4083513845b214db)  
•  [Functions](#512e123dcb8530aa)

<a id="b45d040877cb44c6"></a>
### Boolean Value Expression

<a id="ad737d91c3c6817e"></a>
#### Syntax

```
<boolean value expression> ::=
        <boolean term>
      | <boolean value expression> OR <boolean term>

<boolean term> ::=
        <boolean factor>
      | <boolean term> AND <boolean factor>

<boolean factor> ::=
        [ NOT ] <boolean test>

<boolean test> ::=
        <boolean primary> [ IS [ NOT ] <truth value> ]

<truth value> ::=
        TRUE
      | FALSE
      | UNKNOWN

<boolean primary> ::=
        <column>
        <condition>
      | <boolean predicand>

<boolean predicand> ::=
        <parenthesized boolean value expression>
      | <nonparenthesized value expression primary>

<parenthesized boolean value expression> ::=
        <left paren> <boolean value expression> <right paren>
```

<a id="b0e5af12773834c1"></a>
#### Description

&lt;boolean value expression&gt; describes a boolean value. &lt;boolean primary&gt; with boolean value are &lt;column&gt;, &lt;condition&gt;, and &lt;boolean predicand&gt;. &lt;column&gt; should be declared as BOOLEAN type, and it is allowed to return a boolean value using CAST.

&lt;boolean value expression&gt; can use logical operators such as AND, OR, NOT, and the dedicated operators of boolean value such as IS, IS NOT are also supported.

IS operator and IS NOT operator which are described in &lt;boolean test&gt; determine whether the boolean value described in &lt;boolean primary&gt; matches with one of the &lt;truth value&gt; (TRUE, FALSE, UNKNOWN).

For more information, refer to [Conditions](#35320a70860f96ff).

<a id="10f5113ea68fe28c"></a>
#### Example

```
gSQL> SELECT * FROM T1 WHERE CAST('TRUE' AS BOOLEAN);

I1   
-----
TRUE 
FALSE
null 

3 rows selected.

gSQL> SELECT * FROM T1 WHERE I1;

I1  
----
TRUE

1 row selected.

gSQL> SELECT * FROM T1 WHERE I1 IS TRUE;

I1  
----
TRUE

1 row selected.

gSQL> SELECT * FROM T1 WHERE I1 IS NOT FALSE;

I1  
----
TRUE
null

2 rows selected.

gSQL> SELECT * FROM T1 WHERE I1 IS UNKNOWN;

I1  
----
null

1 row selected.
```

<a id="d8dbcaa9e4c75351"></a>
### CASE Expression

<a id="0aa8798beed993d9"></a>
#### Syntax

```
<case expression> ::=
        <simple case>
      | <searched case>

<simple case> ::=
        CASE expr WHEN comparison_expr THEN result 
                 [ WHEN comparison_expr THEN result ... ] 
                 [ ELSE result ]
        END

<searched case> ::=
        CASE WHEN condition THEN result
             [ WHEN condition THEN result ... ] 
             [ ELSE result ]
        END
```

<a id="e48cf03abd8699cc"></a>
#### Description

WHEN ... THEN clause is evaluated in the order of which is described in the CASE statement.  
If a comparison result is FALSE, the subsequent WHEN ... THEN clauses are evaluated until TRUE comes up.  
If a comparison result is TRUE, the result is returned, and the evaluation is not executed any more.

• Simple case  
&nbsp;&nbsp;The comparison_expr of CASE expr and WHEN ... THEN clause is evaluated as the equal operation.    
&nbsp;&nbsp;(expr = comparison_expr).  
• Searched case  
&nbsp;&nbsp;The condition of WHEN ... THEN clause is evaluated.

If all evaluation results of the WHEN clause are FALSE, then result of ELSE clause is returned.  
If ELSE clause is omitted, NULL is returned as a result.

If there are multiple types of THEN or ELSE clause results, the result type is determined by [Result Type Combination Rule](#7b9ef315990930de).

For more information, refer to the followings.  
• [COALESCE](#2f66c19ba9c3c73f)  
• [NULLIF](#68b32611305a934d)

<a id="cbff01f73f87cf0d"></a>
#### Example

- Simple case

```
gSQL> SELECT I1,
             CASE I1 WHEN 1 THEN 'ONE'
                     WHEN 2 THEN 'TWO'
                     ELSE 'NUMBER'
             END AS CASE_RESULT1,
             CASE I1 WHEN 1 THEN 'ONE'
                     WHEN 2 THEN 'TWO'
             END AS CASE_RESULT2
        FROM T1;
I1 CASE_RESULT1 CASE_RESULT2
-- ------------ -----------
 1 ONE          ONE        
 2 TWO          TWO        
 3 NUMBER       null       
3 rows selected.
```

- Searched case

```
gSQL> SELECT I1,
             CASE WHEN I1 = 1 THEN 'ONE'
                  WHEN I1 = 2 THEN 'TWO'
                  ELSE 'NUMBER'    
             END AS CASE_RESULT1,
             CASE WHEN I1 = 1 THEN 'ONE'
                  WHEN I1 = 2 THEN 'TWO'
             END AS CASE_RESULT2 
        FROM T1;
I1 CASE_RESULT1 CASE_RESULT2
-- ------------ ------------
 1 ONE          ONE         
 2 TWO          TWO         
 3 NUMBER       null        
3 rows selected.
```

<a id="4ea8f1fe70024e32"></a>
### CAST Specification

<a id="fa7697298ea87740"></a>
#### Syntax

```
CAST( expression AS data_type )
```

<a id="c241e5cf1af08621"></a>
#### Description

CAST converts the expression data type to the data type of the specified data_type.

<a id="8d2c4371e5928ab2"></a>
#### Example

```
gSQL> SELECT CAST( '1-2' AS INTERVAL YEAR TO MONTH ) AS RESULT FROM DUAL;  
RESULT
------
+01-02
1 row selected.
```

<a id="73cf5be6c0469d35"></a>
### Scalar Subquery Expression

Scalar subquery expression is a subquery which returns a single row with one column as a result. The scalar subquery expression result is the values described in select list of the subquery.

If the subquery does not return any row, then the result value is NULL, and if it returns two or more rows, then an error occurs.

Scalar subquery expression can be described on most position which describes expression. The subquery should be enclosed in parentheses. Even when scalar subquery expression is used as a function argument and the scalar subquery expression is enclosed in parentheses, other parentheses for the subquery is required regardless of the function parentheses. Otherwise, an error occurs

The following is an example of using scalar subquery expression.

```
gSQL> select * from dual where dummy = (select * from dual);

DUMMY
-----
X    

1 row selected.

gSQL> select sum(select 1 from dual) from dual;

ERR-42000(40000): syntax error 
select sum(select 1 from dual) from dual
...........^    ^
Error at line 1

gSQL> select sum((select 1 from dual)) from dual;

SUM((SELECT 1 FROM DUAL))
-------------------------
                        1

1 row selected.
```

<a id="8b54e5b3fa7136af"></a>
### Compatibility

The SQL standard compatibility for expression is as follows.

**SQL standard compatibility for expression**

<a id="ef7f9a6857bbcb08"></a>
| Feature ID | Description | Availability |
| --- | --- | --- |
| E121-03 | Value expressions in ORDER BY clause | O |
| F051-05 | Basic date and time Explicit CAST between datetime types and character string types | O |
| F201 | CAST function | O |
| F261-01 | Simple CASE | O |
| F261-02 | Searched CASE | O |
| F261-03 | NULLIF | O |
| F261-04 | COALESCE | O |
| F263 | Comma-separated predicates in simple CASE expression | X |
| F301 | CORRESPONDING in query expressions | X |
| F385 | Drop column generation expression clause | X |
| F561 | Full value expressions | X |
| F846 | Octet support in regular expression operators | X |
| F847 | Nonconstant regular expressions | X |
| F850 | Top-level &lt;order by clause&gt; in &lt;query expression&gt; | O |
| F855 | Nested &lt;order by clause&gt; in &lt;query expression&gt; | O |
| F856 | Nested &lt;fetch first clause&gt; in &lt;query expression&gt; | O |
| F857 | Top-level &lt;fetch first clause&gt; in &lt;query expression&gt; | O |
| F861 | Top-level &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| F863 | Nested &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| S091-03 | Arrays expressions | X |
| S111 | ONLY in query expressions | X |
| T121 | WITH (excluding RECURSIVE) in query expression | X |
| T581 | Regular expression substring function | X |

<a id="03685b1e1567cf4c"></a>
## Pseudo Columns

Pseudo column is not only similar to function, but also it is similar to table column because it can return different value in row unit every time the pseudo column is executed.

**Supported pseudo column**

<a id="3b90fa015d069991"></a>
<table><tbody><tr><th align="center">&nbsp;Name</th><th align="center">&nbsp;Description</th><th align="center">&nbsp;Remarks</th></tr><tr><td align="left" valign="middle">CURRVAL</td><td align="left" valign="middle">It is a pseudo column which is related to a sequence.</td><td align="left" valign="middle"><a href="#564199c8f133c07b">CURRVAL</a></td></tr><tr><td align="left" valign="middle">NEXTVAL</td><td align="left" valign="middle">It is a pseudo column which is related to a sequence.</td><td align="left" valign="middle"><a href="#39329e8ee5b2fa13">NEXTVAL</a></td></tr><tr><td align="left" valign="middle">ROWNUM</td><td align="left" valign="middle">It is the row number which satisfies the condition.</td><td align="left" valign="middle"><a href="#c079dac1c5a3b312">ROWNUM</a></td></tr><tr><td align="left" valign="middle">ROWID</td><td align="left" valign="middle">It returns the record identifier in database.</td><td align="left" valign="middle"><a href="#52bdf5a8567273d4">ROWID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_GROUP_ID</td><td align="left" valign="middle">It returns the group identifier in database.</td><td align="left" valign="middle"><a href="#bb1ab299e56a5e97">CLUSTER_GROUP_ID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_MEMBER_ID</td><td align="left" valign="middle">It returns the member identifier in which the record is stored.</td><td align="left" valign="middle"><a href="#04d1b5d6f2cac90b">CLUSTER_MEMBER_ID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_GROUP_NAME</td><td align="left" valign="middle">It returns the group name in which the record is stored.</td><td align="left" valign="middle"><a href="#efd283114a5af6a9">CLUSTER_GROUP_NAME Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_MEMBER_NAME</td><td align="left" valign="middle">It returns the member name in which the record is stored.</td><td align="left" valign="middle"><a href="#94c92f0e27ebd207">CLUSTER_MEMBER_NAME Pseudo Column</a></td></tr></tbody></table>

<a id="52bdf5a8567273d4"></a>
### ROWID Pseudo Column

ROWID pseudo column is a record identifier, and it returns the identification information of each database record.

ROWID has the following information to identify the location within the database depending on the system.

Standalone system  
• OBJECT_ID  
• TABLESPACE_ID  
• PAGE_ID  
• OFFSET in PAGE

Cluster system  
• GRID_BLOCK_SEQUENCE  
• GRID_BLOCK_ID  
• MEMBER_ID  
• SHARD_ID

The information stored inside in base 64 encoding is converted into the value such as A-Z, a-z, 0-9, +, / then output when querying ROWID.

Each information to identify the address within database stored in ROWID can be obtained using the ROWID-related functions.

The address of the deleted record can be newly reassigned to the record to be inserted.

ROWID pseudo column can be used only in SELECT operation, but it can not be used in INSERT, UPDATE, DELETE operations.

For more information, refer to [ROWID](#b43645fb3f6eb862), [ROWID-related Functions](#b4277f25602ce7c4).

The following is an example of querying ROWID pseudo column.

```
gSQL> SELECT ROWID FROM T1;
                  ROWID
-----------------------
AAAAAAAAFpEAACAAAEAkAAA
AAAAAAAAFpEAACAAAEAkAAB
AAAAAAAAFpEAACAAAEAkAAC
AAAAAAAAFpEAACAAAEAkAAD
AAAAAAAAFpEAACAAAEAkAAE
5 rows selected.
```

<a id="bb1ab299e56a5e97"></a>
### CLUSTER_GROUP_ID Pseudo Column

CLUSTER_GROUP_ID pseudo column returns the group identifier of a server in which the record is stored.

CLUSTER_GROUP_ID pseudo column can perform the SELECT, but it can not perform the INSERT, UPDATE, or DELETE.

> This information in valid in the cluster system.

The following is an example of retrieving CLUSTER_GROUP_ID pseudo column.

```
gSQL> SELECT T1.C1, T1.CLUSTER_GROUP_ID FROM T1;
C1 T1.CLUSTER_GROUP_ID
-- -------------------
A                    1
B                    2
C                    3

3 rows selected.
```

<a id="04d1b5d6f2cac90b"></a>
### CLUSTER_MEMBER_ID Pseudo Column

CLUSTER_MEMBER_ID pseudo column returns the member identifier of a server in which the record is stored.

CLUSTER_MEMBER_ID pseudo column can perform the SELECT, but it can not perform the INSERT, UPDATE, or DELETE.

> This information in valid in the cluster system.

The following is an example of retrieving CLUSTER_MEMBER_ID pseudo column.

```
gSQL> SELECT T1.C1, T1.CLUSTER_MEMBER_ID FROM T1;
C1 T1.CLUSTER_MEMBER_ID
-- --------------------
A                     1
B                     3
C                     5

3 rows selected.
```

<a id="efd283114a5af6a9"></a>
### CLUSTER_GROUP_NAME Pseudo Column

CLUSTER_GROUP_NAME pseudo column returns the group name of a server in which the record is stored.

CLUSTER_GROUP_NAME pseudo column can perform the SELECT, but it can not perform the INSERT, UPDATE, or DELETE.

> This information in valid in the cluster system.

The following is an example of retrieving CLUSTER_GROUP_NAME pseudo column.

```
gSQL> SELECT T1.C1, T1.CLUSTER_GROUP_NAME FROM T1;
C1 T1.CLUSTER_GROUP_NAME
-- ---------------------
A  G1                   
B  G2                   
C  G3                   

3 rows selected.
```

<a id="94c92f0e27ebd207"></a>
### CLUSTER_MEMBER_NAME Pseudo Column

CLUSTER_MEMBER_NAME pseudo column returns the member name of a server in which the record is stored.

CLUSTER_MEMBER_NAME pseudo column can perform the SELECT, but it can not perform the INSERT, UPDATE, or DELETE.

> This information in valid in the cluster system.

The following is an example of retrieving CLUSTER_MEMBER_NAME pseudo column.

```
gSQL> SELECT T1.C1, T1.CLUSTER_MEMBER_NAME FROM T1;
C1 T1.CLUSTER_MEMBER_NAME
-- ----------------------
A  G1N1                  
B  G2N1                  
C  G3N1                  

3 rows selected.
```

<a id="55b709690624eea8"></a>
### Compatibility

The SQL standard compatibility for pseudo column is as follows.

**SQL standard compatibility for pseudo column**

<a id="e56accc16d3f7326"></a>
<table><tbody><tr><th align="center">&nbsp;Feature ID</th><th align="center">&nbsp;Description</th><th align="center">&nbsp;Availability</th></tr><tr><td align="left">T176</td><td align="left">Sequence generator support</td><td align="center">O</td></tr><tr><td align="left">T177</td><td align="left">&nbsp;Sequence generator support: simple restart option</td><td align="center">O</td></tr></tbody></table>

<a id="4083513845b214db"></a>
## Operators

An operator is represented by one or more specific symbols or keywords, and it performs an operation using one or more arguments.

The operator types are various as follows.  
• Arithmetic operator  
• Concatenation operator  
• Set operator

<a id="c066d156ef3004bf"></a>
### Arithmetic Operator

<a id="17c2438c4217349b"></a>
#### Syntax

```
<arithmetic operator> ::=
        <value term>
      | <expression> + <value term>
      | <expression> - <value term>

<value term> ::=
        <value factor>
      | <value term> * <value factor>
      | <value term> / <value factor>

<value factor> ::=
        <expression>
      | + <expression>
      | - <expression>
```

<a id="2e91d15820ba23eb"></a>
#### Description

An arithmetic operator performs an arithmetic operation of the numeric types, date/time types or interval types.

The arithmetic operator precedence is as follows.

1. [+ (POSITIVE)](#9772442869533d19), [- (NEGATIVE)](#bf43f613dc2c8eff)
2. [* (MULTIPLICATION)](#652c0269ee3d817b), [/ (DIVISION)](#ea26b480cf202650)
3. [+ (ADDITION)](#02e92cc92093f2fc), [- (SUBTRACTION)](#a446b04d99e17bbf)

<a id="ea54d91f222ed37a"></a>
### Concatenation Operator

<a id="39ce29fdb4faf68b"></a>
#### Syntax

```
<concatenation operator> ::=
        <expression> || <expression>
```

<a id="87c056e2fb9e3747"></a>
#### Description

A concatenation operator returns strings which connect between values of CHARACTER STRING type or BINARY STRING type.  
For more information, refer to [|| (CONCATENATE)](#917f504cb710ba23), [CONCATENATE](#5f5f25ab865e559d).

<a id="3b73326e502b52ff"></a>
### Set Operator

<a id="ffe406b9f18a789e"></a>
#### Syntax

```
<set operator> ::=
        <set operator term>
      | <subquery> UNION [ ALL | DISTINCT ] <set operator term>
      | <subquery> EXCEPT [ ALL | DISTINCT ] <set operator term>
      | <subquery> MINUS [ ALL | DISTINCT ] <set operator term>

<set operator term> ::=
        <subquery>
      | <subquery> INTERSECT [ ALL | DISTINCT ] <set operator term>
```

<a id="98a8d55403dca235"></a>
#### Description

A set operator performs a set operation of the subquery results.  
For more information, refer to [set operator](16-sql-references.md#ab0a1ea34982332b).  

INTERSECT ALL/DISTINCT has a higher precedence than other set operators.

**Set operators**

<a id="f48a3c46d1d302c7"></a>
| Operator | Description |
| --- | --- |
| UNION ALL | It is the union which does not exclude duplicated rows of the subquery result. |
| UNION DISTINCT | It is the union which excludes duplicated rows of the subquery result. |
| EXCEPT ALL | It is the difference set which does not exclude duplicated rows of the subquery result. |
| EXCEPT DISTINCT | It is the difference set which excludes duplicated rows of the subquery result. |
| MINUS ALL | It is as same as EXCEPT ALL. |
| MINUS DISTINCT | It is as same as EXCEPT DISTINCT. |
| INTERSECT ALL | It is the intersection which does not exclude duplicated rows of the subquery result. |
| INTERSECT DISTINCT | It is the intersection which excludes duplicated rows of the subquery result. |

<a id="c55333aa468b20cc"></a>
### Compatibility

The SQL standard compatibility for operator is as follows.

**SQL standard compatibility for operator**

<a id="965b28009fb9dae4"></a>
<table><tbody><tr><th align="center">&nbsp;Feature ID</th><th align="center">&nbsp;Description</th><th align="center">&nbsp;Availability</th></tr><tr><td align="left" valign="middle">E011-04</td><td align="left" valign="middle">Arithmetic operators</td><td align="center" valign="middle">O</td></tr><tr><td valign="middle">E021-07</td><td valign="middle">Character concatenation</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-01</td><td align="left" valign="middle">UNION DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-02</td><td align="left" valign="middle">UNION ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-03</td><td align="left" valign="middle">&nbsp;EXCEPT DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-05</td><td align="left" valign="middle">Columns combined via table operators need not have exactly the same data type</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-06</td><td align="left" valign="middle">Table operators in subqueries</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F041-08</td><td align="left" valign="middle">All comparison operators are supported (rather than just =)</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F302-01</td><td align="left" valign="middle">&nbsp;INTERSECT DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F302-02</td><td align="left" valign="middle">INTERSECT ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F304</td><td align="left" valign="middle">&nbsp;EXCEPT ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F846</td><td align="left" valign="middle">Octet support in regular expression operators</td><td align="center" valign="middle">X</td></tr><tr><td align="left" valign="middle">J571</td><td align="left" valign="middle">NEW operator</td><td align="center" valign="middle">X</td></tr></tbody></table>

<a id="512e123dcb8530aa"></a>
## Functions

Functions and operators are similar in features. However, to represent arguments, functions use parentheses after its name. A function can have zero or more arguments.

The function has two types as follows.   
• Single row function   
• Aggregate function

<a id="6a3c43ef85b02452"></a>
### Single Row Function

Single row function creates a single result row for each row in the table or view.

The single row functions are as follows.

- Numeric function
- Character string function returning character values
- Character string function returning number values
- Datetime function
- General comparison function
- Conversion function
- Conditional function
- NULL-related function
- ROWID-related function
- Encryption function
- System information function

<a id="cde02aaa4b4bd4d0"></a>
#### Numeric Functions

A numeric value is input in numeric function, and the numeric function returns a numeric result.

For more information about the numeric function types, refer to the followings.

- [ABS](#dfdee4df4a227251)
- [ACOS](#34932733dd8dfbb4)
- [ASIN](#cd8b61de7cc12080)
- [ATAN](#aa3df36a602928a3)
- [ATAN2](#424bb734187725c5)
- [BITAND](#6e6f94631f17df2b)
- [BITNOT](#2efa355ec7189d1a)
- [BITOR](#997dce3445e53985)
- [BITXOR](#6e6b21b3872728a0)
- [CBRT](#eadefdbcf33dc583)
- [CEIL](#dff29042322b9ff9)
- [COS](#cd7aa4cdaad0ea5d)
- [COT](#c976849a3a444b6b)
- [DEGREES](#1c17f177307d3bfd)
- [EXP](#39645d4f45d9f0c2)
- [FACTORIAL](#85c6baee4193141e)
- [FLOOR](#c193f1462bbadbdb)
- [LN](#33f8c9daee11124d)
- [LOG](#23e6513ead447ac6)
- [MOD](#9b6e83832f14f490)
- [PI](#2c39f94f95c55d14)
- [POWER](#0a5ad1f0fc0166a6)
- [RADIANS](#b108567e5848b3a7)
- [RANDOM](#79ba3d3328a95148)
- [ROUND( number )](#c8b3ec16eee4195e)
- [SHARD_ID](#b70d05f1aa8e26bf)
- [SHIFT_LEFT](#f317fc13b9b3626a)
- [SHIFT_RIGHT](#fb156c0b07fbf0ff)
- [SIGN](#1d74ed5378a447eb)
- [SIN](#eb34d1ce3213abd7)
- [SQRT](#f79ee8c8f18aefb4)
- [TAN](#d5f6f1c95a4ff85b)
- [TRUNC( number )](#b8bf6dce147c4d4d)
- [WIDTH_BUCKET](#4bdb442901525b95)

<a id="7d75fddc27a5dfb1"></a>
#### Character String Functions Returning Character Values

A character string type value is input in character string functions returning character values, and the function returns the result of character string type.

For more information about character string functions returning character values types, refer to the followings.

- [CHR](#0fd684a8ebce7997)
- [CONCAT](#cf7e8a29d9f60724)
- [CONCATENATE](#5f5f25ab865e559d)
- [INITCAP](#d80f5e4a419f8f7d)
- [LOWER](#20ef3cb6fa1ffd96)
- [LPAD](#7050c762d819354f)
- [LTRIM](#f948b1d10dca4377)
- [OVERLAY](#042f47383ad1bf70)
- [REPEAT](#b6ee30a80a455048)
- [REPLACE](#5fc89474312dcfc2)
- [REVERSE](#ebd260b7c3d0fd65)
- [RPAD](#c8f3cbca700acca7)
- [RTRIM](#8f753ae671600f5f)
- [SPLIT_PART](#4c4079406d453973)
- [SUBSTR](#e66f5efc914d611a)
- [SUBSTRB](#e63cf2098b590fa6)
- [TRANSLATE](#2f553624d615ebb3)
- [TRIM](#6d310074cd59564e)
- [UPPER](#493003178bffe899)

<a id="576ef308efedd9f7"></a>
#### Character String Functions Returning Number Values

A character string type value is input in character string functions returning number values the value, and the function returns the result of number type.

For more information about character string functions returning number values types, refer to the followings.

- [ASCII](#ee5d6de43ce03584)
- [BIT_LENGTH](#82a4d52ccc5574ee)
- [BYTE_LENGTH](#1bbb0c781e8dcb83)
- [CHAR_LENGTH](#2eca28868d47dbb6)
- [INSTR](#20a87cfb135089bd)
- [LENGTH](#dc5af3c589ed5f26)
- [LENGTHB](#20776ee9a823baa5)
- [OCTET_LENGTH](#aa49ee5d59240063)
- [POSITION](#4420e99863c02102)

<a id="c5652714a9234d84"></a>
#### Datetime Functions

The value of date/time/timestamp/interval type is input in datetime function, and the function returns the result of date/time/timestamp/interval type.

For more information about datetime functions types, refer to the followings.

- [ADDDATE](#fc62fbea08ef6611)
- [ADDTIME](#707d4cd698322e86)
- [ADD_MONTHS](#bc6fe5196680e191)
- [DATEADD](#49a793f8c6a4ead4)
- [DATEDIFF](#84c0f25f4ed73fec)
- [DATE_ADD](#21bfa491b404217f)
- [DATE_PART](#1362fd95fc14f2a7)
- [EXTRACT](#cc4fdf75ce2721be)
- [LAST_DAY](#c41960f76e6d586b)
- [MONTHS_BETWEEN](#d02398fbef36e530)

<a id="f63e6e8405eaca5b"></a>
#### General Comparison Functions

General comparison function returns a minimum value or a maximum value for the value set.

For more information about general comparison function types, refer to the followings.

- [GREATEST](#92b4d4ac77f31342)
- [LEAST](#3613239b9d2c8956)

<a id="fb73e361570a301a"></a>
#### Conversion Functions

Conversion function sets the value of a particular data type.

For more information about conversion function types, refer to the followings.

- [TO_CHAR( datetime )](#9688fd0405cae768)
- [TO_CHAR( number )](#949621fdd02e5356)
- [TO_DATE](#25eb6843029ae86c)
- [TO_NATIVE_DOUBLE](#d03ab835f5df2038)
- [TO_NATIVE_REAL](#0cf01e33445e03e5)
- [TO_NUMBER](#491715806db53986)
- [TO_TIME](#d9a48ce329494e11)
- [TO_TIME_TZ](#4de565a0a89e0975)
- [TO_TIME_WITH_TIME_ZONE](#766da9ffc336d7e2)
- [TO_TIMESTAMP](#3e1f1636fafd674a)
- [TO_TIMESTAMP_TZ](#d2eebad23d9c35e9)
- [TO_TIMESTAMP_WITH_TIME_ZONE](#77a90650f33e49f9)

<a id="10dea728e2dba31b"></a>
#### Conditional Functions

Conditional function returns a result of specific value depending on a condition.

For more information about conditional function types, refer to the followings.

- [CASE2](#c96da2ab487de213)
- [DECODE](#368116d4fe5d0775)

<a id="293d791da7c8a495"></a>
#### NULL-related Functions

NULL-related function returns a result of specific value depending on whether the input value is a NULL value.

For more information about null-related function types, refer to the followings.

- [COALESCE](#2f66c19ba9c3c73f)
- [NULLIF](#68b32611305a934d)
- [NVL](#f4977777f7c3da09)
- [NVL2](#b52d0d48e4e25bdf)

<a id="b4277f25602ce7c4"></a>
#### ROWID-related Functions

ROWID-related function is used to obtain information about the ROWID.

For more information about ROWID-related function types, refer to the followings.

- Valid functions in standalone
    - [ROWID_OBJECT_ID](#d1b8e6f4947b8b65)
    - [ROWID_TABLESPACE_ID](#c05f19eb31962101)
    - [ROWID_PAGE_ID](#52907e0ee66a7b9e)
    - [ROWID_ROW_NUMBER](#8d7c7bc10bcbc471)

- Valid functions in cluster
    - [ROWID_GRID_BLOCK_ID](#7d33395f20dfc490)
    - [ROWID_GRID_BLOCK_SEQ](#7db0634c14678f92)
    - [ROWID_MEMBER_ID](#f1aa8d2905444ab8)
    - [ROWID_SHARD_ID](#db09c390bdf597e2)

<a id="b6e67f5f286dcae0"></a>
#### Encryption Functions

encryption function encrypts, decrypts, or hashes the given plain text by using the specific algorithm, then returns the result.

For more information about the encryption function, refer to [DIGEST](#f601b11d1b300e45).

<a id="a2024bfcfd93d9ff"></a>
#### System Information Functions

System information function is used to obtain information about sessions and the system.

For more information about system information function type, refer to the followings.

- [CLOCK_DATE](#6f063576d028e346)
- [CLOCK_LOCALTIME](#9f4b01fffd6b5962)
- [CLOCK_LOCALTIMESTAMP](#a76b0c51947a496d)
- [CURRENT_CATALOG](#97d4603c31df7d25)
- [CURRENT_DATE](#42efebf33a44b909)
- [CURRENT_SCHEMA](#7f63d2fcb279719c)
- [CURRENT_TIME](#406eee865fb2c767)
- [CURRENT_TIMESTAMP](#cf40f2352a534e8c)
- [CURRENT_USER](#3439ccb21bfded13)
- [LAST_IDENTITY_VALUE](#449eb64862a9ab35)
- [LOCALTIME](#14cb2452ce1695c1)
- [LOCALTIMESTAMP](#65a9dfe6178838e6)
- [LOGON_USER](#f3552430bea50cd2)
- [SESSION_ID](#9c2301781c5bc335)
- [SESSION_SERIAL](#14c93071437db5a4)
- [SESSION_USER](#579803a5ccda992b)
- [STATEMENT_DATE](#d9cd0a5fed32919e)
- [STATEMENT_LOCALTIME](#b4caddc36c85506a)
- [STATEMENT_LOCALTIMESTAMP](#9b450c5721628b0d)
- [STATEMENT_TIME](#291da7b42a18babb)
- [STATEMENT_TIMESTAMP](#c42ed707a9aac6d6)
- [STATEMENT_VIEW_SCN](#19558d3073e868bb)
- [SYSDATE](#f5814f4ef90c26ab)
- [SYSTIME](#7a4172f8ee6040b9)
- [SYSTIMESTAMP](#11c7ec435aff8644)
- [TRANSACTION_DATE](#c14c9f18d38d6e78)
- [TRANSACTION_LOCALTIME](#df6720b7efb5e738)
- [TRANSACTION_LOCALTIMESTAMP](#fa3d9ac50d6f8ab7)
- [TRANSACTION_TIME](#751918936eb9a572)
- [TRANSACTION_TIMESTAMP](#85779505c3ed1d67)
- [USER_ID](#b9f46eb5de8d0551)
- [VERSION](#0b9ef75fafd757f8)

<a id="032c4f47483bdb31"></a>
### Aggregate Function

Aggregate function creates a single result row for multiple rows.

For more information about aggregate function types, refer to the followings.

- [COUNT](#79fa00ba0bfca24c)
- [COUNT(*)](#63f5d99817501bb1)
- [SUM](#cc930e2799495e28)
- [AVG](#d7df7013c27d65c7)
- [MIN](#372b04034981ef63)
- [MAX](#33196967d64cc7dc)
- [STDDEV](#aa121de14f05d3e8)
- [STDDEV_POP](#70c13c621cbfb9c8)
- [STDDEV_SAMP](#3aed39af2add9685)
- [VAR_POP](#a6f898169be957da)
- [VAR_SAMP](#9881748ecbb23c59)
- [VARIANCE](#80ab44261e08c113)

<a id="9725a9df47ffdef5"></a>
### Compatibility

The SQL standard compatibility for function is as follows.

**SQL standard compatibility for function**

<a id="1f07207ff980556a"></a>
| Feature ID | Description | Availability |
| --- | --- | --- |
| B033 | Untyped SQL-invoked function arguments | X |
| E021-04 | CHARACTER_LENGTH function | O |
| E021-05 | OCTET_LENGTH function | O |
| E021-06 | SUBSTRING function | O |
| E021-08 | UPPER and LOWER functions | O |
| E021-09 | TRIM function | O |
| E021-11 | POSITION function | O |
| E091-01 | AVG | O |
| E091-02 | COUNT | O |
| E091-03 | MAX | O |
| E091-04 | MIN | O |
| E091-05 | SUM | O |
| E091-06 | ALL quantifier | O |
| E091-07 | DISTINCT quantifier | O |
| F131-03 | Set functions supported in queries with grouped views | O |
| F201 | CAST function | O |
| F441 | Extended set function support | X |
| F442 | Mixed column references in set functions | X |
| F801 | Full set function | X |
| F842 | OCCURRENCES_REGEX function | X |
| F843 | POSITION_REGEX function | X |
| S071 | SQL paths in function and type name resolution | X |
| S201-02 | Array as result type of functions | X |
| S211 | User-defined cast functions | X |
| S241 | Transform functions | X |
| T041-03 | POSITION, LENGTH, LOWER, TRIM, UPPER, and SUBSTRING functions for LOB data types | X |
| T312 | OVERLAY function | O |
| T321-01 | User-defined functions with no overloading | X |
| T326 | Table functions | X |
| T341 | Overloading of SQL-invoked functions and SQL-invoked procedures | X |
| T433 | Multiargument GROUPING function | X |
| T441 | ABS and MOD functions | O |
| T571 | Array-returning external SQL-invoked functions | X |
| T572 | Multiset-returning external SQL-invoked functions | X |
| T581 | Regular expression substring function | X |
| T614 | NTILE function | X |
| T615 | LEAD and LAG functions | X |
| T616 | Null treatment option for LEAD and LAG functions | X |
| T617 | FIRST_VALUE and LAST_VALUE functions | X |
| T618 | NTH_VALUE function | X |
| T619 | Nested window functions | X |
| T621 | Enhanced numeric functions | O |

<a id="35320a70860f96ff"></a>
## Conditions

<a id="dc83840eec6d2ac1"></a>
### Condition

Condition is an expression which is evaluated as TRUE, FALSE, UNKNOWN.

Condition can be used in the following SQL statements.  

• WHERE clauses in DELETE, UPDATE statements  
• WHERE and HAVING clauses in SELECT statement  
• Where the BOOLEAN TYPE can be used

The condition types are as follows.  

• Comparison condition  
• Logical condition  
• Null condition  
• Compound condition  
• Pattern-matching condition  
• Between condition  
• In condition  
• Exists condition

**Condition precedence**

<a id="1d847b6bdd262f03"></a>
| Precedence | Condition type |
| --- | --- |
| 1 | Operators in condition clauses |
| 2 | =, !=, &lt;, &gt;, &lt;=, &gt;= |
| 3 | IS [NOT] NULL, [NOT] BETWEEN,  [NOT] IN,  LIKE, EXISTS |
| 4 | NOT |
| 5 | AND |
| 6 | OR |

<a id="6d02960b79df97d4"></a>
### Comparison Conditions

It compares both conditional expressions, and returns the boolean type of TRUE, FALSE, UNKNOWN values.

**Comparison conditions**

<a id="19c2632724c54d0d"></a>
| Condition | Description |
| --- | --- |
| = | It checks if both conditions are equal. |
| !=, &lt;&gt; | It checks if both conditions are not equal. |
| > | It compares which one of both conditions is bigger. |
| < | It compares which one of both conditions is smaller. |
| >= | It compares which one of both conditions is bigger or equal. |
| <= | It compares which one of both conditions is smaller or equal. |
| ANY, SOME | If there is a condition whose left expr satisfies at least one of right expr_list (or subquery results), then it returns TRUE. If there is not right subquery result, then it returns FALSE. |
| ALL | If there is a condition whose left expr satisfies all right expr_list (or subquery results), then it returns TRUE. If there is not right subquery result, then it returns TRUE. |

For more information, refer to [Type Comparison](#0b812e6987dc67cb).

<a id="fa72a174caa1c5a5"></a>
#### &lt; Simple Comparison Conditions &gt;

<a id="49fe64cb7472940e"></a>
##### Syntax

```
<simple_comparison_condition> ::=
        <expr>          <comparison_operator> <expr>
      | <expr>          <comparison_operator> ( <subquery> )
      | ( <subquery> )  <comparison_operator> <expr>
      | ( <subquery> )  <comparison_operator> ( <subquery> ) 
      | ( <expr_list> ) <comparison_operator> ( <expr_list> )
      | ( <expr_list> ) <comparison_operator> ( <subquery> )
      | ( <subquery> )  <comparison_operator> ( <expr_list> )
      | ( <subquery> )  <comparison_operator> ( <subquery> )

<comparison_operator> ::=
        <  =   >
      | <  !=  >
      | <  <   >
      | <  >   >
      | <  <=  >
      | <  >=  >

<expr_list> ::= 
        <expr>
      | <expr>, ... , <expr>
      | ( <expr> )
      | ( <expr> , ... , <expr> )
```

For more information, refer to [Scalar Subquery Expression](#73cf5be6c0469d35).

<a id="7ab9ded26df013f2"></a>
##### Description

If the expr list or subquery comes to both left and right of comparison_operator, then the number of expr or subquery target to be compared should be same.  
If there is a subquery, the number of result records should be one.

<a id="cfd7fb173fb85228"></a>
##### Example

**Example of simple comparison conditions**

<a id="244975db67e94209"></a>
| Conditional expression | Result |
| --- | --- |
| 'abc' = 'abc' | TRUE |
| 'abc' != 'abc' | FALSE |
| 'abc' < 'abc' | FALSE |
| 'abc' <= 'abc' | TRUE |
| 'abc' > 'abc' | FALSE |
| 'abc' >= 'abc' | TRUE |
| ( 1, 2, 3 ) = ( 1, 2, 3 ) | TRUE |
| ( 1, 2, 3 ) = ( 1, 2, 4 ) | FALSE |
| ( 1, 2, 3 ) != ( 4, 5, 6 ) | TRUE |
| ( 1, 2, 3 ) != ( 1, 2, 3 ) | FALSE |
| ( 1, 2, 3 ) < ( 1, 2, 4 ) | TRUE |
| ( 1, 2, 3 ) < ( 1, 2, 3 ) | FALSE |
| ( 1, 2, 3 ) <= ( 1, 2, 4 ) | TRUE |
| ( 1, 2, 3 ) <= ( 1, 2, 2 ) | FALSE |
| ( 1, 2, 3 ) > ( 1, 2, 2 ) | TRUE |
| ( 1, 2, 3 ) > ( 1, 2, 4 ) | FALSE |
| ( 1, 2, 3 ) >= ( 1, 2, 2 ) | TRUE |
| ( 1, 2, 3 ) >= ( 1, 2, 4 ) | FALSE |

<a id="2cc20b78d7c6ece5"></a>
#### &lt;Group Comparison Conditions&gt;

<a id="5a7bd8339bc5db69"></a>
##### Syntax

```
<group_comparison_condition> ::=
   <expr>          <comparison_operator> <quantifier> ( <expr_list> )
 | <expr>          <comparison_operator> <quantifier> ( <subquery> )
 | ( <expr_list> ) <comparison_operator> <quantifier> ( <expr_list_list> )
 | ( <expr_list> ) <comparison_operator> <quantifier> ( <subquery> )
 | ( <subquery> )  <comparison_operator> <quantifier> ( <expr_list> )
 | ( <subquery> )  <comparison_operator> <quantifier> ( <expr_list_list> )
 | ( <subquery> )  <comparison_operator> <quantifier> ( <subquery> )

<comparison_operator> ::=
        <  =   >
      | <  !=  >
      | <  <   >
      | <  >   >
      | <  <=  >
      | <  >=  >

<quantifier> ::=
        ALL
      | ANY
      | SOME

<expr_list> ::= 
        <expr>
      | <expr>, ... , <expr>
      | ( <expr> )
      | ( <expr> , ... , <expr> )

<expr_list_list> ::=
        <expr_list>
      | <expr_list>, ... , <expr_list>
```

For more information, refer to [Scalar Subquery Expression](#73cf5be6c0469d35).

<a id="ea8444421e299772"></a>
##### Description

If the expr list or subquery comes to both left and right of comparison_operator, then the number of expr or subquery target to be compared should be same.  
If a subquery comes to the left of comparison_operator, the number of result records should be one.  
If a subquery comes to the right of comparison_operator, the number of result records can be multiple.

<a id="44f8cadc1e095575"></a>
##### Example

<a id="d9f8181bebe6fc9a"></a>
<table class="table column_count_2"><caption>Example of group comparison conditions</caption><thead><tr><th class="to_center"><div>Conditional expression</div></th><th class="to_center"><div>Result</div></th></tr></thead><tbody><tr><td><div>1 =any ( 1, 2, 3, 4, 5 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>1 =any ( 1, 2, null, 4, 5 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>1 =any ( 2, null, 4, 5 )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td><div>1 =any ( 100, 2, 3, 4, 5 )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td><div>1 =all ( 1, +1, 1E+0 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>1 =all ( 1, +1, 1E+0, null )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td><div>1 =all ( 1, 2, 3, 4, 5 )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td><div>( 1, 2 ) =any ( ( 0, 1 ), ( 1, 2 ), ( 3, 4 ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>( 1, 2 ) =any ( ( 0, 1 ), ( 1, 2 ), ( null, null ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>( 1, 2 ) =any ( ( 0, 1 ), ( 2, 3 ), ( 3, 4 ) )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td><div>( 1, 2 ) =all ( ( 1, 2 ), ( +1, +2 ), ( 1E+0, 2E+0 ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>( 1, 2 ) =all ( ( 1, 2 ), ( +1, +2 ), ( null, null ) )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td><div>( 1, 2 ) =all ( ( 0, 1 ), ( 2, 3 ), ( 3, 4 ) )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><th colspan="2"><div>When the result record of comparison_operator's right subquery is 0</div></th></tr><tr><td><div>( 'X' ) =any ( select dummy from dual where dummy = 'Y' )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td><div>( 'X' ) =all ( select dummy from dual where dummy = 'Y' )</div></td><td class="to_left"><div>TRUE</div></td></tr></tbody></table>

<a id="a4f19eb02fe02dd0"></a>
### Logical Conditions

Logical conditions are such as AND, OR, NOT.

<a id="8f477533462e4b85"></a>
#### AND

<a id="da322a9951dd3dcf"></a>
##### Syntax

```
<boolean value expression> AND <boolean value expression>
```

<a id="6c28a5396e8a727e"></a>
##### Description

**Truth table of AND boolean operator**

<a id="7591674b7ca70c93"></a>
| AND | True | False | Unknown |
| --- | --- | --- | --- |
| True | True | False | Unknown |
| False | False | False | False |
| Unknown | Unknown | False | Unknown |

<a id="def2602d2cead4bd"></a>
#### OR

<a id="542960729f63e55a"></a>
##### Syntax

```
<boolean value expression> OR <boolean value expression>
```

<a id="3e106962ed177863"></a>
##### Description

**Truth table of OR boolean operator**

<a id="4414d965111d3f4f"></a>
| OR | True | False | Unknown |
| --- | --- | --- | --- |
| True | True | True | True |
| False | True | False | Unknown |
| Unknown | True | Unknown | Unknown |

<a id="93031d5472be02a9"></a>
#### NOT

<a id="de173004a7a5c843"></a>
##### Syntax

```
NOT <boolean value expression>
```

<a id="2a005e3a6feff63c"></a>
##### Description

**Truth table of NOT boolean operator**

<a id="014b5754e7d78a95"></a>
| expr | NOT |
| --- | --- |
| True | False |
| False | True |
| Unknown | Unknown |

<a id="9c120266a706353f"></a>
### Null Condition

<a id="74363a66691389c8"></a>
#### Syntax

```
<expr> IS [NOT] NULL
```

<a id="d53e571e59cc2f99"></a>
#### Description

It checks whether the result value of expr is NULL.

**Result table of IS NULL condition**

<a id="e269c225468aa230"></a>
| expr | IS NULL | IS NOT NULL |
| --- | --- | --- |
| NULL | True | False |
| NOT NULL | False | True |

<a id="578efa84837e6a11"></a>
### Compound Conditions

It is a conditional expression in which multiple conditions are combined.

```
compound_condition ::=
        ( condition )
      | NOT condition
      | condition < AND | OR > condition
```

<a id="bb07bcebf463628f"></a>
### Pattern-matching Conditions

<a id="2847eb367aedfad2"></a>
#### Like Condition

<a id="9d1b625f3d4529ff"></a>
##### Syntax

```
like_condition ::=
        string [NOT] LIKE pattern [ ESCAPE escape_character ]
```

<a id="31e4884a3110b824"></a>
##### Description

It checks if a string matches the specified pattern.

Arguments such as string, pattern, escape_character can be of a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or of the type which is available to be converted to a character type.  
If string, pattern, escape_character are NULL, it returns NULL.

If escape_character is omitted, there is not a default value.  
If escape_character is specified, the escape_character should be one character.

If pattern does not include '_'  nor '%', it is processed in the same way as equal operation(string = pattern).  
If pattern includes '_'  or '%', the string checks if it matches as follows.  
• '_': If it corresponds to one arbitrary character.  
• '%': If it corresponds to the arbitrary character string which has zero or more characters.

Use ESCAPE syntax to compare '_' or '%' included in the pattern with characters.   
Specify escape_character, and describe the specified escape_character before the pattern's  '_' or '%'.

<a id="9cf436c06a7635f9"></a>
##### Example

```
gSQL> SELECT 'hello%' LIKE 'h%o!%' ESCAPE '!' AS RESULT FROM DUAL;
RESULT
------
TRUE

• 'represent' LIKE 'represent'   => TRUE
• 'represent' LIKE ' represent ' => FALSE
• 'represent' LIKE 'REPRESENT'   => FALSE
• 'represent' LIKE 'r_pr_s_nt'   => TRUE
• 'represent' LIKE 're%t'        => TRUE
• 'represent' LIKE 'rep'         => FALSE

• 'summer_vacation' LIKE 'summer\_vacation' ESCAPE '\'  => TRUE
• NULL LIKE 'summer\_vacation' ESCAPE '\'               => NULL
• 'summer_vacation' LIKE NULL ESCAPE '\'                => NULL
• 'summer_vacation' LIKE 'summer\_vacation' ESCAPE NULL => NULL
```

<a id="0f644ab785e83b31"></a>
### BETWEEN Condition

<a id="99057c312b0e4a2f"></a>
#### Syntax

```
<between condition> ::=
   <expr1> [ NOT ] BETWEEN [ ASYMMETRIC | SYMMETRIC ] <expr2> AND <expr3>
```

<a id="845a4ac3cac409c3"></a>
#### Description

It checks whether expr1 is within the range between expr2 and expr3.

If ASYMMETRIC or SYMMETRIC is omitted, the default is ASYMMETRIC.  
If data types among expr1, expr2, expr3 are different, they are converted.   
For more information, refer to [Type Comparison](#0b812e6987dc67cb), [Type Conversion](#ee64dd045e8e2ced).

**Equivalence of between conditions**

<a id="8ff11b5698bd49e2"></a>
| A | B |
| --- | --- |
| X BETWEEN ASYMMETRIC Y AND Z | X BETWEEN Y AND Z |
| X BETWEEN Y AND Z | X >= Y AND X <= Z |
| X NOT BETWEEN Y AND Z | NOT( X BETWEEN Y AND Z ) |
| X BETWEEN SYMMETRIC Y AND Z | ((X BETWEEN Y AND Z) OR (X BETWEEN Z AND Y) |
| X NOT BETWEEN SYMMETRIC Y AND Z | NOT( X BETWEEN SYMMETRIC Y AND Z ) |

<a id="bd4d245ddeb38af6"></a>
#### Example

<a id="8a416af418db5820"></a>
<table class="table column_count_3"><caption>Example of between condition</caption><thead><tr><th class="to_center" colspan="2"><div>Conditional expression</div></th><th class="to_center"><div>Result</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>BETWEEN [ ASYMMETRIC ]</div></td><td class="to_middle"><div>3 BETWEEN 1 AND 5</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr><tr><td class="to_middle"><div>NULL BETWEEN 1 AND 5
3 BETWEEN NULL AND 5
3 BETWEEN 1 AND NULL</div></td><td class="to_left to_middle"><div>NULL</div></td></tr><tr><td class="to_middle"><div>3 BETWEEN 5 AND 1</div></td><td class="to_left to_middle"><div>FALSE</div></td></tr><tr><td class="to_middle" rowspan="3"><div>BETWEEN SYMMETRIC</div></td><td class="to_middle"><div>3 BETWEEN SYMMETRIC 1 AND 5</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr><tr><td class="to_middle"><div>NULL BETWEEN SYMMETRIC 1 AND 5
3 BETWEEN SYMMETRIC NULL AND 5
3 BETWEEN SYMMETRIC 1 AND NULL</div></td><td class="to_left to_middle"><div>NULL</div></td></tr><tr><td class="to_middle"><div>3 BETWEEN SYMMETRIC 5 AND 1</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr></tbody></table>

<a id="0e9b07ed54d72cec"></a>
### IN Condition

<a id="65a5997dff494a0a"></a>
#### Syntax

```
<in_condition> ::=
        <expr>          [NOT] IN ( <expr_list> )  
      | <expr>          [NOT] IN ( <subquery> )  
      | ( <expr_list> ) [NOT] IN ( <expr_list_list> )  
      | ( <expr_list> ) [NOT] IN ( <subquery> )
      | ( <subquery> )  [NOT] IN ( <expr_list> )  
      | ( <subquery> )  [NOT] IN ( <expr_list_list> )  
      | ( <subquery> )  [NOT] IN ( <subquery> )  

<expr_list> ::=          
        <expr>       
      | <expr>, ... , <expr>       
      | ( <expr> )       
      | ( <expr> , ... , <expr> )  

<expr_list_list> ::=         
        <expr_list>       
      | <expr_list>, ... , <expr_list>
```

<a id="d0d49fc4011df842"></a>
#### Description

In condition returns the same result as = ANY.  
NOT IN condition returns the same result as !=ALL.

For more information, refer to [Comparison Conditions](#6d02960b79df97d4).

<a id="3882c8aecac5d4ab"></a>
#### Example

**Example of IN condition**

<a id="ff3ce3741e7142a6"></a>
| Conditional expression | Result |
| --- | --- |
| 1 IN ( 1, 2, 3, 4, 5 ) | TRUE |
| 1 IN ( 1, 2, null, 4, 5 ) | TRUE |
| 1 IN ( 2, null, 4, 5 ) | NULL |
| 1 IN ( 100, 2, 3, 4, 5 ) | FALSE |
| NULL IN ( 1, 2, 3 ) | NULL |
| 1 NOT IN ( 2, 3, 4, 5 ) | TRUE |
| 1 NOT IN ( 2, null, 4, 5 ) | NULL |
| 1 NOT IN ( 1, 2, null, 4, 5 ) | FALSE |
| 1 NOT IN ( 100, 2, 3, 4, 5 ) | TRUE |
| NULL NOT IN ( 1, 2, 3 ) | NULL |

<a id="ea3194ac45182ade"></a>
### EXISTS Condition

<a id="43305005041f458a"></a>
#### Syntax

```
exists_conditions ::= 
        EXISTS ( subquery )
```

<a id="eea1642fdd5d95f7"></a>
#### Description

It checks whether the result record of subquery exists.  
If the result record of subquery exists, it returns TRUE. Otherwise, it returns FALSE.

<a id="eb46f090aa0cfdf0"></a>
#### Example

```
gSQL> SELECT * FROM DUAL WHERE EXISTS ( SELECT * FROM DUAL );
      DUMMY
      -----
      X    
      1 row selected.

gSQL> SELECT * FROM DUAL 
       WHERE EXISTS ( SELECT * FROM DUAL WHERE DUMMY = 'Y' );
      no rows selected.
```

<a id="eac295b908a2d4f7"></a>
### Compatibility

The SQL standard compatibility for condition is as follows.

**SQL standard compatibility for condition**

<a id="2236787c51ca4922"></a>
| Feature ID | Description | Availability |
| --- | --- | --- |
| E061-01 | Comparison predicate | O |
| E061-02 | BETWEEN predicate | O |
| E061-03 | IN predicate with list of values | O |
| E061-04 | LIKE predicate | O |
| E061-05 | LIKE predicate: ESCAPE clause | O |
| E061-06 | NULL predicate | O |
| E061-07 | Quantified comparison predicate | O |
| E061-08 | EXISTS predicate | O |
| E061-09 | Subqueries in comparison predicate | O |
| E061-11 | Subqueries in IN predicate | O |
| E061-12 | Subqueries in quantified comparison predicate | O |
| E061-13 | Correlated subqueries | O |
| E061-14 | Search condition | O |
| F051-04 | Comparison predicate on DATE, TIME, and TIMESTAMP data types | X |
| F053 | OVERLAPS predicate | X |
| F263 | Comma-separated predicates in simple CASE expression | X |
| F291 | UNIQUE predicate | X |
| F481 | Expanded NULL predicate | O |
| F841 | LIKE_REGEX predicate | X |
| P008 | Comma-separated predicates in a CASE statement Extended CASE | X |
| S151 | Type predicate | X |
| T141 | SIMILAR predicate | X |
| T151 | DISTINCT predicate | X |
| T152 | DISTINCT predicate with negation | X |
| T461 | Symmetric BETWEEN predicate | O |
| T501 | Enhanced EXISTS predicate | X |
| T631 | IN predicate with one list element | X |
| X090 | XML document predicate | X |
| X091 | XML content predicate | X |
| X141 | IS VALID predicate: data-driven case | X |
| X142 | IS VALID predicate: ACCORDING TO clause | X |
| X143 | IS VALID predicate: ELEMENT clause | X |
| X144 | IS VALID predicate: schema location | X |
| X145 | IS VALID predicate outside check constraints | X |
| X151 | IS VALID predicate with DOCUMENT option | X |
| X152 | IS VALID predicate with CONTENT option | X |
| X153 | IS VALID predicate with SEQUENCE option | X |
| X155 | IS VALID predicate: NAMESPACE without ELEMENT clause | X |
| X157 | IS VALID predicate: NO NAMESPACE with ELEMENT clause | X |

<a id="fb134a7b0cc3f5f7"></a>
## Built-in Data Type References

<a id="1b3f742cc4342b0f"></a>
### Aliases of Built-in Data Types

- BIGINT
    - It is as same as NUMBER(19,0).
    - Refer to [NUMBER](#68b0be359ae3c9d6)
- BINARY
    - Refer to [BINARY](#5209bc041cbb637f)
- BINARY VARYING
    - Refer to [BINARY VARYING](#6abd619dad707497)
- BINARY LONG VARYING
    - Refer to [BINARY LONG VARYING](#3045806ebc113f60)
- BOOLEAN
    - Refer to [BOOLEAN](#d49c3b75726d4ba1)
- CHAR
    - It is as same as CHARACTER.
    - Refer to [CHARACTER](#0911bf6123a5f020)
- CHARACTER
    - Refer to [CHARACTER](#0911bf6123a5f020)
- CHARACTER VARYING
    - Refer to [CHARACTER VARYING](#ad554c09b6feef05)
- CHARACTER LONG VARYING
    - Refer to [CHARACTER LONG VARYING](#429ccd166922ee94)
- DATE
    - Refer to [DATE](#3a80607ae5e62f9a)
- DEC
    - It is as same as NUMERIC.
    - Refer to [NUMERIC](#4cc855c2aaab3d4e)
- DECIMAL
    - It is as same as NUMERIC.
    - Refer to [NUMERIC](#4cc855c2aaab3d4e)
- DOUBLE
    - It is as same as FLOAT(53).
    - Refer to [FLOAT](#04e4e9aa22dbfbfa)
- DOUBLE PRECISION
    - It is as same as FLOAT(53).
    - Refer to [FLOAT](#04e4e9aa22dbfbfa)
- FLOAT
    - Refer to [FLOAT](#04e4e9aa22dbfbfa)
- FLOAT4
    - It is as same as FLOAT(24).
    - Refer to [FLOAT](#04e4e9aa22dbfbfa)
- FLOAT8
    - It is as same as FLOAT(53).
    - Refer to [FLOAT](#04e4e9aa22dbfbfa)
- INT
    - It is as same as NUMBER(10,0).
    - Refer to [NUMBER](#68b0be359ae3c9d6)
- INT2
    - It is as same as NUMBER(5,0).
    - Refer to [NUMBER](#68b0be359ae3c9d6)
- INT4
    - It is as same as NUMBER(10,0).
    - Refer to [NUMBER](#68b0be359ae3c9d6)
- INT8
    - It is as same as NUMBER(19,0).
    - Refer to [NUMBER](#68b0be359ae3c9d6)
- INTEGER
    - It is as same as NUMBER(10,0).
    - Refer to [NUMBER](#68b0be359ae3c9d6)
- INTERVAL
    - Refer to [INTERVAL](#f6b7d049ffca0557)
- LONG BINARY VARYING
    - It is as same as BINARY LONG VARYING. 
    - Refer to [BINARY LONG VARYING](#3045806ebc113f60)
- LONG CHAR VARYING
    - It is as same as CHARACTER LONG VARYING. 
    - Refer to [CHARACTER LONG VARYING](#429ccd166922ee94)
- LONG CHARACTER VARYING
    - It is as same as CHARACTER LONG VARYING. 
    - Refer to [CHARACTER LONG VARYING](#429ccd166922ee94)
- LONG VARCHAR
    - It is as same as CHARACTER LONG VARYING.
    - Refer to [CHARACTER LONG VARYING](#429ccd166922ee94)
- NATIVE_BIGINT
    - Refer to [NATIVE_BIGINT](#74b62854715c94af)
- NATIVE_DOUBLE
    - Refer to [NATIVE_DOUBLE](#37e17e763fe87201)
- NATIVE_INTEGER
    - Refer to [NATIVE_INTEGER](#a7125330e516b594)
- NATIVE_REAL
    - Refer to [NATIVE_REAL](#701e2c4fabd684e2)
- NATIVE_SMALLINT
    - Refer to [NATIVE_SMALLINT](#fc64233a3ddee2c5)
- NUMBER
    - Refer to [NUMBER](#68b0be359ae3c9d6)
- NUMERIC
    - Refer to [NUMERIC](#4cc855c2aaab3d4e)
- ROWID
    - Refer to [ROWID](#b43645fb3f6eb862)
- SMALLINT
    - It is as same as NUMBER(5,0). 
    - Refer to [NUMBER](#68b0be359ae3c9d6)
- TIME
    - Refer to [TIME](#d1cf3fafd4663cb4)
- TIMESTAMP
    - Refer to [TIMESTAMP](#e301c3bda5651cd6)
- VARBINARY
    - It is as same as BINARY VARYING.
    - Refer to [BINARY VARYING](#6abd619dad707497)
- VARCHAR
    - It is as same as CHARACTER VARYING. 
    - Refer to [CHARACTER VARYING](#ad554c09b6feef05)
- VARCHAR2
    - It is as same as CHARACTER VARYING. 
    - Refer to [CHARACTER VARYING](#ad554c09b6feef05)

<a id="5209bc041cbb637f"></a>
### BINARY

<a id="81f520a721d34e4e"></a>
#### Syntax

```
BINARY [ (length) ]
```

<a id="8f7e0434ae8d4d01"></a>
#### Syntax Rules and Parameters

- length: It is the binary string length.
    - Range: 1 ~ 2000
    - Default value: 1

<a id="b443c0c11fb74cd5"></a>
#### Description

A fixed-length binary string is stored.  
If the binary string length to be stored is shorter than the specified length,  X'00 ' is stored in the remaining part.  
• Storage size: Bytes of the length value

<a id="05b7cf5878a8b1d9"></a>
#### For More Information

Refer to the followings.

- [BINARY VARYING](#6abd619dad707497)
- [BINARY LONG VARYING](#3045806ebc113f60)

<a id="6abd619dad707497"></a>
### BINARY VARYING

<a id="41fb49fbcaec05db"></a>
#### Syntax

```
BINARY VARYING (length)
```

<a id="3469b12c55af5495"></a>
#### Syntax Rules and Parameters

- length: It is the maximum length of binary string.
    - Range: 1 ~ 4000

<a id="79cc218d157f1fd9"></a>
#### Description

The variable-length binary string is stored.  

• Storage size: Bytes of the binary string to be stored  
• Alias names: VARBINARY

<a id="89781d94751ae29f"></a>
#### For More Information

Refer to the followings.

- [BINARY](#5209bc041cbb637f)
- [BINARY LONG VARYING](#3045806ebc113f60)

<a id="3045806ebc113f60"></a>
### BINARY LONG VARYING

<a id="e9059c0cfc946e46"></a>
#### Syntax

```
BINARY LONG VARYING
```

<a id="e3a303703f0aa436"></a>
#### Description

The value of the long variable binary string is stored.  
• Maximum storage size: 100 megabytes  
• Storage size: Bytes of the binary string to be stored  
• Alias names: LONG BINARY VARYING, LONG VARBINARY

It can not be used as a column of the key, so there are limitations as follows.  
• It can not be used as a key column of an index.  
• It can not be used as the expression of ORDER BY clause.   
• It can not be used as the expression of GROUP BY clause.  
• It can not be used as the expression of DISTINCT clause.  
• It can not be used as the expression of UNION, INTERSECT, EXCEPT clauses.

<a id="7c348d178c747454"></a>
#### For More Information

Refer to the followings.

- [BINARY](#5209bc041cbb637f)
- [BINARY VARYING](#6abd619dad707497)

<a id="d49c3b75726d4ba1"></a>
### BOOLEAN

<a id="2c67a906a7ff1d5d"></a>
#### Syntax

```
BOOLEAN
```

<a id="b5818ac1a349f484"></a>
#### Description

TRUE or FALSE is stored.  
• Storage size: 1 byte.

<a id="0911bf6123a5f020"></a>
### CHARACTER

<a id="bb5cf5f3743cdb83"></a>
#### Syntax

```
CHARACTER [ (length [ CHARACTERS | OCTETS | CHAR | BYTE ] ) ]
```

<a id="a1f6c04982088afc"></a>
#### Syntax Rules and Parameters

- length: It is the string length.
    - Range: 1 ~ 2000
    - Default value: 1

- [ CHARACTERS | OCTETS | CHAR | BYTE ]: It is unit of length.
    - CHARACTERS
        - The number of characters
        - CHAR is as same as CHARACTERS.
    - OCTETS
        - The number of bytes
        - BYTE is as same as OCTETS.
    - If omitted, the default is the property value of [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#e6ecf251502c667b) which is set when creating database.

<a id="a984dab71abaf149"></a>
#### Description

A fixed-length string is stored.  
If the length of the string to be stored is shorter than the specified length, white spaces are stored in the remaining part.

- Storage size: Bytes of the length value
- Alias names: CHAR

<a id="b8c7225ead373b40"></a>
#### For More Information

Refer to the followings.

- [CHARACTER VARYING](#ad554c09b6feef05)
- [CHARACTER LONG VARYING](#429ccd166922ee94)

<a id="ad554c09b6feef05"></a>
### CHARACTER VARYING

<a id="9aacfed057f3e361"></a>
#### Syntax

```
CHARACTER VARYING ( length [ CHARACTERS | OCTETS | CHAR | BYTE ] )
```

<a id="4744f67919b1af90"></a>
#### Syntax Rules and Parameters

- length: It is the string length.
    - Range: 1 ~ 4000

- [ CHARACTERS | OCTETS | CHAR | BYTE ]: It is unit of length.
    - CHARACTERS
        - The number of characters
        - CHAR is as same as CHARACTERS.
    - OCTETS
        - The number of bytes
        - BYTE is as same as OCTETS.
    - If omitted, the default is the property value of [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#e6ecf251502c667b) which is set when creating database.

<a id="868c9636222747e1"></a>
#### Description

The variable-length string is stored.  

• Storage size: Bytes of the string to be stored  
• Alias names: VARCHAR, VARCHAR2

<a id="23062a6f85e63dea"></a>
#### For More Information

Refer to the followings.

- [CHARACTER](#0911bf6123a5f020)
- [CHARACTER LONG VARYING](#429ccd166922ee94)

<a id="429ccd166922ee94"></a>
### CHARACTER LONG VARYING

<a id="ceb4d9e9472904f6"></a>
#### Syntax

```
CHARACTER LONG VARYING
```

<a id="f08541d651f6af64"></a>
#### Description

The value of the long variable-length string is stored.  

• Maximum storage size: 100 megabytes  
• Storage size: Bytes of the string to be stored   
• Alias names: LONG CHARACTER VARYING, LONG CHAR VARYING, LONG VARCHAR

It can not be used as a column of the key, so there are limitations as follows.  

• It can not be used as a key column of an index.  
• It can not be used as the expression of ORDER BY clause.   
• It can not be used as the expression of GROUP BY clause.  
• It can not be used as the expression of DISTINCT clause.  
• It can not be used as the expression of UNION, INTERSECT, EXCEPT clauses.

<a id="dfea9534799d28bb"></a>
#### For More Information

Refer to the followings.

- [CHARACTER](#0911bf6123a5f020)
- [CHARACTER VARYING](#ad554c09b6feef05)

<a id="3a80607ae5e62f9a"></a>
### DATE

<a id="6256198903f20101"></a>
#### Syntax

```
DATE
```

<a id="d2fee5be1d5a36fe"></a>
#### Description

It is the date type including YEAR, MONTH, DAY, HOUR, MINUTE and SECOND (excluding fractional seconds).

- Value range: Date value between '4714-11-24 BC' and '9999-12-31 AD'
- Storage size: 8 bytes

<a id="fb7d6983bd3e8621"></a>
#### For More Information

Refer to the followings.

- [Date Literals](#3967c655d974c30c)
- [TIME](#d1cf3fafd4663cb4)
- [TIMESTAMP](#e301c3bda5651cd6).

<a id="04e4e9aa22dbfbfa"></a>
### FLOAT

<a id="f5c2bc6b3a937d95"></a>
#### Syntax

```
FLOAT[ ( precision ) ]
```

<a id="ebfe23bc98d5e6ac"></a>
#### Syntax Rules and Parameters

- precision: It is the binary precision of significant digits.
    - Precision range: 1 ~ 126
    - Default value: 126

<a id="9888698d23b1814e"></a>
#### Description

The floating point value with a binary precision is stored.

- Exponential range: 1E-130 ~ 1E+125
- Storage size: (number of digits in integer part + 1) / 2 + (number of digits in fractional part + 1) / 2 + 1 (exponent, sign)

It has a binary precision value unlike [NUMBER](#68b0be359ae3c9d6), [NUMERIC](#4cc855c2aaab3d4e) types.

- Alias names: REAL = FLOAT(24), DOUBLE = FLOAT(53), DOUBLE PRECISION = FLOAT(53), FLOAT4 = FLOAT(24), FLOAT8 = FLOAT(53).

<a id="e6e608951c492e31"></a>
#### For More Information

Refer to the followings.

- [NUMBER](#68b0be359ae3c9d6)
- [NUMERIC](#4cc855c2aaab3d4e)

<a id="f6b7d049ffca0557"></a>
### INTERVAL

<a id="1747001930f27547"></a>
#### Syntax

```
<interval_type> ::=
      INTERVAL YEAR [ ( leading_precision ) ] 
    | INTERVAL MONTH [ ( leading_precision ) ] 
    | INTERVAL DAY [ ( leading_precision ) ] 
    | INTERVAL HOUR [ ( leading_precision ) ] 
    | INTERVAL MINUTE [ ( leading_precision ) ]
    | INTERVAL SECOND [ ( leading_precision  [ , fractional_seconds_precision ] ) ]
    | INTERVAL YEAR [ ( leading_precision ) ] TO MONTH
    | INTERVAL DAY [ ( leading_precision ) ] TO HOUR
    | INTERVAL DAY [ ( leading_precision ) ] TO MINUTE
    | INTERVAL DAY [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]
    | INTERVAL HOUR [ ( leading_precision ) ] TO MINUTE
    | INTERVAL HOUR [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]
    | INTERVAL MINUTE [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]
```

<a id="037675ed462809fa"></a>
#### Syntax Rules and Parameters

- INTERVAL YEAR [ ( leading_precision ) ]: A period of YEAR is stored.
    - leading_precision 
        - The number of digits in YEAR
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL MONTH [ ( leading_precision ) ]: A period of MONTH is stored.
    - leading_precision 
        - The number of digits in MONTH
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL YEAR [ ( leading_precision ) ] TO MONTH: A period of YEAR and MONTH is stored.
    - leading_precision
        - The number of digits in YEAR
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL DAY [ ( leading_precision ) ]: A period of DAY is stored.
    - leading_precision 
        - The number of digits in DAY
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL HOUR [ ( leading_precision ) ]: A period of HOUR is stored.
    - leading_precision 
        - The number of digits in HOUR
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL MINUTE [ ( leading_precision ) ]: A period of MINUTE is stored.
    - leading_precision 
        - The number of digits in MINUTE
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL SECOND [ ( leading_precision [ , fractional_seconds_precision ] ) ]: A period of SECOND is stored.
    - leading_precision 
        - The number of digits in SECOND
        - Value range: 2 ~ 6
        - Default value: 2
    - fractional_seconds_precision
        - The number of digits in fractional seconds
        - Value range: 0 ~ 6
        - Default value: 6

- INTERVAL DAY [ ( leading_precision ) ] TO HOUR: A period of DAY and HOUR is stored.
    - leading_precision 
        - The number of digits in DAY
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL DAY [ ( leading_precision ) ] TO MINUTE: A period of DAY, HOUR, and MINUTE is stored.
    - leading_precision 
        - The number of digits in DAY
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL DAY [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]: A period of DAY, HOUR, MINUTE, and SECOND is stored.
    - leading_precision 
        - The number of digits in DAY
        - Value range: 2 ~ 6
        - Default value: 2
    - fractional_seconds_precision
        - The number of digits in fractional seconds
        - Value range: 0 ~ 6
        - Default value: 6

- INTERVAL HOUR [ ( leading_precision ) ] TO MINUTE: A period of HOUR and MINUTE is stored.
    - leading_precision 
        - The number of digits in HOUR
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL HOUR [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]: A period of HOUR, MINUTE and SECOND is stored.
    - leading_precision 
        - The number of digits in HOUR
        - Value range: 2 ~ 6
        - Default value: 2
    - fractional_seconds_precision
        - The number of digits in fractional seconds
        - Value range: 0 ~ 6
        - Default value: 6

- INTERVAL MINUTE [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]: A period of MINUTE and SECOND is stored.
    - leading_precision 
        - The number of digits in MINUTE 
        - Value range: 2 ~ 6
        - Default value: 2
    - fractional_seconds_precision
        - The number of digits in fractional seconds
        - Value range: 0 ~ 6
        - Default value: 6

<a id="c21730d3cfd1bae4"></a>
#### Description

INTERVAL types are classified into YEAR TO MONTH family type and DAY TO SECOND family type depending on the range of value representation as follows.

- YEAR TO MONTH family type: Its storage size is 8 bytes.
    - INTERVAL YEAR
    - INTERVAL MONTH
    - INTERVAL YEAR TO MONTH

- DAY TO SECOND family type: Its storage size is 16 bytes.
    - INTERVAL DAY
    - INTERVAL HOUR
    - INTERVAL MINUTE
    - INTERVAL SECOND
    - INTERVAL DAY TO HOUR
    - INTERVAL DAY TO MINUTE
    - INTERVAL DAY TO SECOND
    - INTERVAL HOUR TO MINUTE
    - INTERVAL HOUR TO SECOND
    - INTERVAL MINUTE TO SECOND

If the number which is bigger than number of the specified digits is in the field to which the leading_precision is specified, then an error is returned.  
If the number which is bigger than number of the specified digits is in the field to which the fractional_seconds_precision is specified, it is rounded off.

**Precisions and value range of the second or later field in INTERVAL * TO ***

<a id="7c86b8edb02937b9"></a>
| Field | Precision | Value range |
| --- | --- | --- |
| MONTH | 2 | 0 ~ 11 |
| HOUR | 2 | 0 ~ 23 |
| MINUTE | 2 | 0 ~ 59 |
| SECOND (interger part) | 2 | 0 ~ 59 |

<a id="1daa35d456baff58"></a>
#### For More Information

Refer to [Interval Literals](#3e1e94e284d2f9d2).

<a id="74b62854715c94af"></a>
### NATIVE_BIGINT

<a id="ec5cc264331aa4d1"></a>
#### Syntax

```
NATIVE_BIGINT
```

<a id="e3fada2eea72cc82"></a>
#### Description

Signed 8-byte integer is stored.

It is as same as long long data type of C language (8 bytes integer).

- Value range: -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807
- Storage size: 8 bytes

<a id="37e17e763fe87201"></a>
### NATIVE_DOUBLE

<a id="83459d5387d1f444"></a>
#### Syntax

```
NATIVE_DOUBLE
```

<a id="bafc2ba8a771ee6a"></a>
#### Description

Double precision floating-point number (8 bytes) is stored.

It is as same as double data type of C language.

- Exponential range: 1E-307 ~ 1E+308
- Storage size: 8 bytes

<a id="a7125330e516b594"></a>
### NATIVE_INTEGER

<a id="71cb6a7a1f4a4993"></a>
#### Syntax

```
NATIVE_INTEGER
```

<a id="aea9cb4874bd4aac"></a>
#### Description

Signed 4 byte integer is stored.

It is as same as integer data type of C language (4 bytes).

- Value range: -2,147,483,648 ~ +2,147,483,647
- Storage size: 4 bytes

<a id="701e2c4fabd684e2"></a>
### NATIVE_REAL

<a id="cba49d7014b5728f"></a>
#### Syntax

```
NATIVE_REAL
```

<a id="4734a5f1f90277e9"></a>
#### Description

Single precision floating-point number (4 bytes) is stored.

It is as same as float data type of C language.

- Exponential range: 1E-37 ~ 1E+37
- Storage size: 4 bytes

<a id="fc64233a3ddee2c5"></a>
### NATIVE_SMALLINT

<a id="fc61403648e28c9b"></a>
#### Syntax

```
NATIVE_SMALLINT
```

<a id="7f3f3a19dd24c3c0"></a>
#### Description

Signed 2 byte integer is stored.

It is as same as short data type of C language.

- Value range: -32,768 ~ 32,767
- Storage size: 2 bytes

<a id="68b0be359ae3c9d6"></a>
### NUMBER

<a id="5fb604bd2464557d"></a>
#### Syntax

```
NUMBER  [ ( precision [ , scale ] ) ]
```

<a id="a55f1c9757a3b768"></a>
#### Syntax Rules and Parameters

- NUMBER: A floating point number without a precision and scale is stored.
    - The range of significant digits: 38
    - Exponential range: 1E-130 ~ 1E+125
    - It is as same as FLOAT (126).

- NUMBER(precision): The integer with significant digits of precision is stored.
    - Precision range: 1 ~ 38
    - The scale value: 0
    - It has a decimal precision value unlike [FLOAT](#04e4e9aa22dbfbfa) type.
    - It is as same as NUMBER(precision, 0), NUMERIC(precision, 0).

- NUMBER(precision, scale): A fixed point number with precision and scale is stored.
    - Precision range: 1 ~ 38
    - Scale range: -84 ~ 127
    - It has a decimal precision value unlike [FLOAT](#04e4e9aa22dbfbfa) type.
    - It is as same as NUMERIC (precision,scale).
    - Alias names: SMALLINT = NUMBER(5,0), INTEGER = NUMBER(10,0), BIGINT = NUMBER(19,0), INT2 = NUMBER(5,0), INT4 = NUMBER(10,0), INT8 = NUMBER(19,0)

<a id="b38b7fb289621571"></a>
#### Description

NUMBER type is similar to NUMERIC type, but if both the precision and scale are omitted, NUMBER type stores the floating point number whose precision and scale are not specified.

- NUMBER without precision, scale: Floating-point number
- NUMERIC without precision, scale: The fixed point number of NUMERIC(38, 0)
- Storage size: (number of digits in integer part + 1) / 2 + (number of digits in fractional part + 1) / 2 + 1(exponent, sign)

<a id="ce57aa0e0f9c0396"></a>
#### For More Information

Refer to the followings.

- [FLOAT](#04e4e9aa22dbfbfa)
- [NUMERIC](#4cc855c2aaab3d4e)

<a id="4cc855c2aaab3d4e"></a>
### NUMERIC

<a id="3ba27c96a804c243"></a>
#### Syntax

```
NUMERIC  [ ( precision [ , scale ] ) ]
```

<a id="4c600918018ad7e8"></a>
#### Syntax Rules and Parameters

- precision: It is the decimal precision of significant digits.
    - precision range: 1 ~ 38
    - Default value: 38

- scale: It is the decimal point range.
    - scale range: -84 ~ 127
    - Default value: 0

<a id="0658338d01ecd73a"></a>
#### Description

A fixed point number with precision and scale is stored.

If the precision and scale are omitted, it means as follows.

- NUMERIC = NUMERIC(38,0)
- NUMERIC(p) = NUMERIC(p,0)

NUMBER type is similar to NUMERIC type, but if both the precision and scale are omitted, NUMBER type stores the floating-point number whose precision and scale is not specified.

- NUMBER without precision, scale: Floating point number
- NUMERIC without precision, scale: Fixed point number of NUMERIC(38,0)
- Storage size: (number of digits in integer part + 1) / 2 + (number of digits in fractional part + 1) / 2 + 1(exponent, sign)

<a id="a026bf8998ea9278"></a>
#### For More Information

Refer to the followings.

- [FLOAT](#04e4e9aa22dbfbfa)
- [NUMBER](#68b0be359ae3c9d6)

<a id="b43645fb3f6eb862"></a>
### ROWID

<a id="d73d083622d17c36"></a>
#### Syntax

```
ROWID
```

<a id="cf490f26c65cecc2"></a>
#### Description

A record identifier (ROWID) is stored.  

A record identifier (ROWID) is the identification information of each record in database.  

When querying the ROWID pseudo column, each record identifier (ROWID) is obtained. This ROWID pseudo column has the ROWID data type information.

ROWID type consists of the followings in a standalone system.  
• OBJECT_ID   
• TABLESPACE_ID   
• PAGE_ID   
• OFFSET within PAGE

ROWID type consists of the followings in a cluster system.  
• GRID_BLOCK_SEQUENCE  
• GRID_BLOCK_ID  
• MEMBER_ID  
• SHARD_ID

ROWID is stored in the base 64 value, which can include A ~ Z, a ~ z, 0 ~ 9, +, /.  
Each component information of ROWID is obtained using ROWID-related functions.

• Storage size: 16 bytes

<a id="ce583520a2c72dc5"></a>
#### For More Information

Refer to the followings.

- [ROWID Pseudo Column](#52bdf5a8567273d4)
- [ROWID-related Functions](#b4277f25602ce7c4)

<a id="d1cf3fafd4663cb4"></a>
### TIME

<a id="d273b51bae629ba6"></a>
#### Syntax

```
TIME [ ( fractional_seconds_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
```

<a id="88c9872f59748190"></a>
#### Syntax Rules and Parameters

- fractional_seconds_precision: It is the number of significant digits in fractional seconds.
    - fractional_seconds_precision range: 0 ~ 6
    - Default value: 6

- [ WITH TIME ZONE | WITHOUT TIME ZONE ]: It specifies whether to store TIME ZONE value.
    - WITH TIME ZONE: The time which includes time zone
    - WITHOUT TIME ZONE: The time which does not include time zone
    - Default value: WITHOUT TIME ZONE

<a id="7bbcac186bb60802"></a>
#### Description

The time which includes HOUR, MINUTE and SECOND is stored.

- Storage size 
    - TIME WITHOUT TIME ZONE: 8 bytes
    - TIME WITH TIME ZONE: 12 bytes

<a id="88f70c9bb3c307f6"></a>
#### For More Information

Refer to the followings.

- [Time Literals](#49e8d4527de6cb84)
- [Time with Time Zone Literals](#c48cf3b2011afcce)
- [DATE](#3a80607ae5e62f9a)
- [TIMESTAMP](#e301c3bda5651cd6).

<a id="e301c3bda5651cd6"></a>
### TIMESTAMP

<a id="b0d49b413320f5f3"></a>
#### Syntax

```
TIMESTAMP [ ( fractional_seconds_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
```

<a id="83e91e1b63812a06"></a>
#### Syntax Rules and Parameters

- fractional_seconds_precision: It is the number of significant digits in the fractional seconds.
    - fractional_seconds_precision range: 0 ~ 6 
    - Default value: 6

- [ WITH TIME ZONE | WITHOUT TIME ZONE ]: It specifies whether to store TIME ZONE value.
    - WITH TIME ZONE: The time which includes time zone.
    - WITHOUT TIME ZONE: The time which does not include time zone.
    - Default value: WITHOUT TIME ZONE

<a id="238957a06d39450b"></a>
#### Description

The time which includes YEAR, MONTH, DATE, HOUR, MINUTE and SECOND is stored.

- Storage size 
    - TIMESTAMP WITHOUT TIME ZONE: 8 bytes
    - TIMESTAMP WITH TIME ZONE: 12 bytes

<a id="d5296356964eb7d7"></a>
#### For More Information

Refer to the followings.

- [Timestamp Literals](#3427e629e71c129e)
- [Timestamp with Time Zone Literals](#179066ecde8e8fcb)
- [DATE](#3a80607ae5e62f9a)
- [TIME](#d1cf3fafd4663cb4)

<a id="2124145ac560592e"></a>
## Built-in Function References

<a id="652c0269ee3d817b"></a>
### * (MULTIPLICATION)

<a id="9f7a449ec426bc28"></a>
#### Syntax

```
expr1 * expr2
```

<a id="39611b01585647ca"></a>
#### Description

It returns the multiplication result of expr1 and expr2.

The multiplication types and result types are as follows.  
For more information, refer to [Type Conversion](#ee64dd045e8e2ced).

**Numeric * operation**

<a id="03e210a0e819514f"></a>
| expr1 (expr2) | expr2 (expr1) | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="50a8f448e8e0d886"></a>
<table class="table column_count_3"><caption>INTERVAL * operation</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type is the interval type.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type is the interval type.)</div></td></tr><tr><td class="to_left" colspan="3"><div>Refer to <a class="reference text" href="#b9aa42daeeaae02a">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

**INTERVAL type details which is included in INTERVAL type written in the following table**

<a id="b9aa42daeeaae02a"></a>
<table><thead><tr><th align="center">INTERVAL YEAR TO MONTH</th><th align="center">INTERVAL DAY TO SECOND</th></tr></thead><tbody><tr><td valign="middle"><ul><li>INTERVAL YEAR</li><li>INTERVAL MONTH</li><li>INTERVAL YEAR TO MONTH</li></ul></td><td valign="middle"><ul><li>INTERVAL DAY</li><li>INTERVAL HOUR</li><li>INTERVAL MINUTE</li><li>INTERVAL SECOND</li><li>INTERVAL DAY TO HOUR</li><li>INTERVAL DAY TO MINUTE</li><li>INTERVAL DAY TO SECOND</li><li>INTERVAL HOUR TO MINUTE</li><li>INTERVAL HOUR TO SECOND</li><li>INTERVAL MINUTE TO SECOND</li></ul></td></tr></tbody></table>

<a id="0e31260c02e9657b"></a>
#### Example

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

<a id="02e92cc92093f2fc"></a>
### + (ADDITION)

<a id="56a7abad385abd76"></a>
#### Syntax

```
expr1 + expr2
```

<a id="a97590623c2ba72d"></a>
#### Description

It returns the addition result of expr1 and expr2.

The addition types and result types are as follows.  
For more information, refer to [Type Conversion](#ee64dd045e8e2ced).

**Numeric + operation**

<a id="9de7d533d2fb0dcc"></a>
| expr1 (expr2) | expr2 (expr1) | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="64e2652f5a3a11de"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) + operation</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference text" href="#b9aa42daeeaae02a">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="4e28842fce150215"></a>
#### Example

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

<a id="9772442869533d19"></a>
### + (POSITIVE)

<a id="4fd3ecb178adf9a4"></a>
#### Syntax

```
+ expr
```

<a id="0040e0ba3a04403e"></a>
#### Description

The + sign is displayed in expr.

<a id="9f707bbc27bb4b89"></a>
#### Example

```
gSQL> SELECT +3 AS RESULT1, +(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      3      -3
1 row selected.
```

<a id="bf43f613dc2c8eff"></a>
### - (NEGATIVE)

<a id="c4b86ba454bdc078"></a>
#### Syntax

```
- expr
```

<a id="5fc1ada9c47bf9f5"></a>
#### Description

The - sign is displayed in expr.

<a id="4ee06cd05b50f4b2"></a>
#### Example

```
gSQL> SELECT -3 AS RESULT1, -(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     -3       3
1 row selected.
```

<a id="a446b04d99e17bbf"></a>
### - (SUBTRACTION)

<a id="fc8076a6c122e19b"></a>
#### Syntax

```
expr1 - expr2
```

<a id="dfea7141dc62f499"></a>
#### Description

It returns the subtraction result of expr1 and expr2.

The subtraction types and result types are as follows.  
For more information, refer to [Type Conversion](#ee64dd045e8e2ced).

**Numeric - operation**

<a id="3d22b1d6d41ee495"></a>
| expr1 | expr2 | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="054145f74da8d771"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) - operation</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMBER</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type includes all the interval range of expr1 and expr2.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference" href="#b9aa42daeeaae02a">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="ba983757624c2680"></a>
#### Example

```
gSQL> SELECT 
      TO_DATE( '2012-05-05' ) - TO_DATE( '2012-01-01' ) AS RESULT 
      FROM DUAL;
RESULT
------
   125
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
      INTERVAL'05-11'YEAR TO MONTH - INTERVAL'02-01'YEAR TO MONTH 
      AS RESULT 
      FROM DUAL;
RESULT    
----------
+000003-10
1 row selected.

gSQL> SELECT INTERVAL'15 23:59:59.999999'DAY TO SECOND 
           - INTERVAL'10 23:59:59.999999'DAY TO SECOND AS RESULT 
      FROM DUAL;
RESULT                 
-----------------------
+000005 00:00:00.000000
1 row selected.
```

<a id="ea26b480cf202650"></a>
### / (DIVISION)

<a id="e37246387ab47a6f"></a>
#### Syntax

```
expr1 / expr2
```

<a id="7a1aa2ce56c2ec27"></a>
#### Description

It returns the division result of expr1 and expr2.

The division types and result types are as follows.  
For more information, refer to [Type Conversion](#ee64dd045e8e2ced).

**Numeric / operation**

<a id="3f6b93ae43422e12"></a>
| expr1 | expr2 | Result type |
| --- | --- | --- |
| NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER | NUMBER |
| NATIVE_DOUBLE | NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="3c4a5e5b62f13f5a"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) / operation</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>Result type</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(The result type is interval type.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>Numeric type</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(The result type is interval type.)</div></td></tr><tr><td colspan="3"><div>Refer to <a class="reference text" href="#b9aa42daeeaae02a">INTERVAL type details which is included in INTERVAL type written in the following table</a>.</div></td></tr></tbody></table>

<a id="20718c8e3ea48b1d"></a>
#### Example

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

<a id="917f504cb710ba23"></a>
### || (CONCATENATE)

<a id="464b60700255b014"></a>
#### Syntax

```
str1 || str2
```

<a id="8e8d94edc2c5bb9d"></a>
#### Description

CONCATENATE returns the string concatenating str1 and str2.  
If either str1 or str2 is NULL, the string except NULL is returned. If both of str1 and str2 are NULL, NULL is returned.

The argument can be a type which can be converted to either character string type or binary string type.  
For more information, refer to [Type Conversion](#ee64dd045e8e2ced).

It is an alias of [CONCAT](#cf7e8a29d9f60724), [CONCATENATE](#5f5f25ab865e559d).

The result types are as follows.

**The result types of || (CONCATENATE)**

<a id="428222d7a359e814"></a>
| Data type | CHAR | VARCHAR | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR | CHAR | VARCHAR | LONG VARCHAR |
| VARCHAR | VARCHAR | VARCHAR | LONG VARCHAR |
| LONG VARCHAR | LONG VARCHAR | LONG VARCHAR | LONG VARCHAR |
| Data type | BINARY | VARBINARY | LONG VARBINARY |
| BINARY | BINARY | VARBINARY | LONG VARBINARY |
| VARBINARY | VARBINARY | VARBINARY | LONG VARBINARY |
| LONG VARBINARY | LONG VARBINARY | LONG VARBINARY | LONG VARBINARY |

<a id="ed4f20fdb7edb64f"></a>
#### Example

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

<a id="dfdee4df4a227251"></a>
### ABS

<a id="2c0390ad4a8d4d15"></a>
#### Syntax

```
ABS( num )
```

<a id="a064270e6821e066"></a>
#### Description

ABS returns the absolute value of num.  
The num argument can be a numeric type or types which can be converted to number.

<a id="9807b80baecbeab9"></a>
#### Example

```
gSQL> SELECT ABS(-1) AS RESULT1, ABS(1) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1       1
1 row selected.
```

<a id="34932733dd8dfbb4"></a>
### ACOS

<a id="2b6b3a61f8c68f31"></a>
#### Syntax

```
ACOS( num )
```

<a id="a3db11ef00324b76"></a>
#### Description

ACOS returns the arc cosine value of num.  
The num argument should be in the range of -1 to 1.   
It returns the radians value in the range of 0 and pi.

<a id="667c8fc4d6d432f0"></a>
#### Example

```
gSQL> SELECT ACOS( 1 ) FROM DUAL;
ACOS( 1 )
---------
        0
1 row selected.
```

<a id="fc62fbea08ef6611"></a>
### ADDDATE

<a id="c61d3282679e9daf"></a>
#### Syntax

```
ADDDATE( date, INTERVAL expr unit  )
ADDDATE( expr, days )
```

<a id="07a4c478d7d43be2"></a>
#### Description

ADDDATE adds the second argument to the first argument, then returns the result.  
If any of the input argument value is NULL, the result is also NULL.  
The first argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, and the second argument data type can be INTERVAL or numeric.

The result type is as same as [(DATETIME/INTERVAL) + operation](#64e2652f5a3a11de).

<a id="045a7cea6c207f4e"></a>
#### Example

```
gSQL> SELECT ADDDATE( TO_DATE( '2012-12-12', 'YYYY-MM-DD' ), 1 ) AS RESULT
        FROM DUAL;
RESULT    
----------
2012-12-13
1 row selected.

gSQL> SELECT ADDDATE( TO_DATE( '2012-12-12', 'YYYY-MM-DD' ),
                      INTERVAL'01-01'YEAR TO MONTH ) AS RESULT 
        FROM DUAL;
RESULT    
----------
2014-01-12
1 row selected.
```

<a id="707d4cd698322e86"></a>
### ADDTIME

<a id="b8ae04b8a5cfe421"></a>
#### Syntax

```
ADDTIME( expr1, expr2 )
```

<a id="b6da5bf8bcc9da92"></a>
#### Description

ADDTIME adds expr2 to expr1, then returns the result.

If expr1 or expr2 is NULL, the result is NULL.  
expr1 data type can be TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE TYPE, and expr2 data type can be INTERVAL DAY TO SECOND TYPE.

The result type is as same as [(DATETIME/INTERVAL) + operation](#64e2652f5a3a11de).

<a id="60df953401058584"></a>
#### Example

```
gSQL> SELECT 
      ADDTIME( TO_TIMESTAMP( '2001-05-10 11:22:33', 
                             'YYYY-MM-DD HH24:MI:SS' ),
               INTERVAL'0 01:02:03.999999'DAY TO SECOND ) AS RESULT
        FROM DUAL;
RESULT                    
--------------------------
2001-05-10 12:24:36.999999
1 row selected.
```

<a id="bc6fe5196680e191"></a>
### ADD_MONTHS

<a id="a71ff8dbc5a2c15a"></a>
#### Syntax

```
ADD_MONTHS( date, number )
```

<a id="d30f96007cd88a5b"></a>
#### Description

ADD_MONTHS adds as many month as the number to the date, then returns the result.  
If any of the input argument is NULL, the result is NULL.  
After ADD_MONTHS operation, if the date is bigger than the last day of the month, it is adjusted to the last day of the month.

The data type of date argument can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, and the number argument can be a numeric type.

The result type is always DATE regardless of the input argument date type.

<a id="c3290a7920fc6283"></a>
#### Example

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

<a id="ee5d6de43ce03584"></a>
### ASCII

<a id="321e876f090d8f52"></a>
#### Syntax

```
ASCII( char )
```

<a id="d68878c85209788f"></a>
#### Description

It returns the database character set code of the first character of char in decimal form.  

The data type of char can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING or can be a type which can be converted to a character type, and the return type is NUMBER.

<a id="c5caba4a0bd8a07c"></a>
#### Example

```
gSQL> SELECT ASCII( 'G' ) AS RESULT FROM DUAL;
RESULT
------
    71
1 row selected.
```

<a id="cd8b61de7cc12080"></a>
### ASIN

<a id="b168b781a9835aa0"></a>
#### Syntax

```
ASIN( num )
```

<a id="4f70f82a9f7525ef"></a>
#### Description

ASIN returns the arc sin value of num.  
The num argument should be in the range of  -1 to 1.   
It returns the radians value in the range of -pi/2 and pi/2.

<a id="198160c2af612b1f"></a>
#### Example

```
gSQL> SELECT ASIN( 0 ) FROM DUAL;
ASIN( 0 )
---------
        0
1 row selected.
```

<a id="aa3df36a602928a3"></a>
### ATAN

<a id="0615f4fd42fb0e1d"></a>
#### Syntax

```
ATAN( num )
```

<a id="3bf824fa12cec976"></a>
#### Description

ATAN returns the arc tangent value of num.  
The num value range is not limited. It returns the radians value in the range of -pi/2 and pi/2.

<a id="9c74661a900ef4d1"></a>
#### Example

```
gSQL> SELECT ATAN( 1 ) FROM DUAL;
       ATAN( 1 )
----------------
.785398163397448
1 row selected.
```

<a id="424bb734187725c5"></a>
### ATAN2

<a id="b5e590f9738d1888"></a>
#### Syntax

```
ATAN2( num1, num2 )
```

<a id="2ad9bebba9733b5b"></a>
#### Description

ATAN2 returns the arc tangent value of num1 and num2.  
The num1 argument value range is not limited. It returns the radians value in the range of -pi and pi.

<a id="63042d18af3ce013"></a>
#### Example

```
gSQL> SELECT ATAN2( 1, 0 ) FROM DUAL;
  ATAN2( 1, 0 )
---------------
1.5707963267949
1 row selected.
```

<a id="d7df7013c27d65c7"></a>
### AVG

<a id="589b9ea8a934709b"></a>
#### Syntax

```
AVG( [ ALL | DISTINCT ] num )
```

<a id="2e86c49460872f85"></a>
#### Description

It is an aggregate function, and it obtains average value of exprs.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

<a id="2de660248e82dfee"></a>
#### Example

```
gSQL> SELECT AVG(c1) FROM t1;

AVG(C1)
-------
      2

1 row selected.
```

<a id="6e6f94631f17df2b"></a>
### BITAND

<a id="8d937c53476fbc33"></a>
#### Syntax

```
BITAND( num1, num2 )
```

<a id="5c1d08f927391c09"></a>
#### Description

It returns the AND operation result for the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT or a data type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.

The result type is NATIVE_BIGINT.

<a id="2afa00e11b0d391a"></a>
#### Example

```
gSQL> SELECT BITAND( 5, 3 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="2efa355ec7189d1a"></a>
### BITNOT

<a id="0caaa6d69e0c1476"></a>
#### Syntax

```
BITNOT( num )
```

<a id="c1fd9b80ddc06afd"></a>
#### Description

It returns the NOT operation result for the num bit.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT or a data type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.

The result type is as follows.  
• If the input argument is NATIVE_SMALLINT type, its result type is NATIVE_SMALLINT type.  
• If the input argument is NATIVE_INTEGER type, its result type is NATIVE_INTEGER type.  
• If the input argument is NATIVE_BIGINT type, its result type is NATIVE_BIGINT type.

<a id="cfe717d65c43b697"></a>
#### Example

```
gSQL> SELECT BITNOT( 5 ) AS RESULT FROM DUAL;
RESULT
------
    -6
1 row selected.
```

<a id="997dce3445e53985"></a>
### BITOR

<a id="0ec9e78991b6c32e"></a>
#### Syntax

```
BITOR( num1, num2 )
```

<a id="545759351d49bb89"></a>
#### Description

It returns the OR operation result for the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT types or a data type which can be converted to NATIVE_BIGINT type.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.

The result type is NATIVE_BIGINT type.

<a id="0204520e87eddd5b"></a>
#### Example

```
gSQL> SELECT BITOR( 5, 3 ) FROM DUAL;

BITOR( 5, 3 )
-------------
            7
1 row selected.
```

<a id="6e6b21b3872728a0"></a>
### BITXOR

<a id="a853598bb4bd40fd"></a>
#### Syntax

```
BITXOR( num1, num2 )
```

<a id="87e87834be65a9d6"></a>
#### Description

It returns the XOR operation result for the bits of num1 and num2.

The input argument data type can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT or a data type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.

The result type is NATIVE_BIGINT.

<a id="0ae9dba8e026b7f5"></a>
#### Example

```
gSQL> SELECT BITXOR( 5, 3 ) FROM DUAL;
BITXOR( 5, 3 )
--------------
             6
1 row selected.
```

<a id="82a4d52ccc5574ee"></a>
### BIT_LENGTH

<a id="545a9957de1cdaa9"></a>
#### Syntax

```
BIT_LENGTH( str )
```

<a id="f09f1051a76d0f40"></a>
#### Description

BIT_LENGTH returns the number of bits for str.

<a id="159c8cbfc3f0bfe2"></a>
#### Example

```
gSQL> SELECT BIT_LENGTH( 'LIKE' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
             32
    1 row selected.
```

<a id="1bbb0c781e8dcb83"></a>
### BYTE_LENGTH

<a id="9d35445949f529bd"></a>
#### Syntax

```
BYTE_LENGTH( str )
```

<a id="1af27440a29255a5"></a>
#### Description

It is an alias of OCTET_LENGTH.  
For more information, refer to [OCTET_LENGTH](#aa49ee5d59240063), [LENGTHB](#20776ee9a823baa5).

<a id="600d194855f0cc27"></a>
#### Example

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

<a id="c96da2ab487de213"></a>
### CASE2

<a id="3cc7700d3a67c787"></a>
#### Syntax

```
CASE2( condition1, result1
      [, condition2, result2
       , ...
       , conditionN, resultN ]
      [, default ] )
```

<a id="f67d33ff38296739"></a>
#### Description

CASE2 evaluates the condition in the described order.  
If the comparison result is FALSE, it continues evaluating until TRUE comes up.  
If the comparison result is TRUE, it returns the corresponding result, and does not evaluate any more.  
If all the comparison results are FALSE, it returns the default value. If the default is omitted, it returns NULL.

The result type is the data type of result1 (the first result).   
If the data type of result1 (the first result) is a numeric type and a character type then each data type includes the range of result1, ..., resultN.  
If result1 (the first result) is CHAR or NULL, then the result type is VARCHAR.

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

<a id="ff42aaecd2ff201f"></a>
#### Example

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

<a id="eadefdbcf33dc583"></a>
### CBRT

<a id="3455abfb9bb4a80e"></a>
#### Syntax

```
CBRT( num )
```

<a id="450847d4394629dd"></a>
#### Description

It returns the cube root of num.  
If the num argument is NULL, the result is also NULL.

<a id="3d7b65d7dfb69945"></a>
#### Example

```
gSQL> SELECT CBRT( 27 ) FROM DUAL;
CBRT( 27 )
----------
         3
1 row selected.
```

<a id="dff29042322b9ff9"></a>
### CEIL

<a id="63a672640896431c"></a>
#### Syntax

```
CEIL( num )
CEILING( num )
```

<a id="168f69f1fb761026"></a>
#### Description

CEIL returns the smallest integer which is equal to or bigger than num.

<a id="20e65063f38f3101"></a>
#### Example

```
gSQL> SELECT CEIL( 3.5 ) AS RESULT1, CEIL( -3.5 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      4      -3
1 row selected.
```

<a id="2eca28868d47dbb6"></a>
### CHAR_LENGTH

<a id="fc20f1dc9b6d06a1"></a>
#### Syntax

```
CHAR_LENGTH( str )            
CHARACTER_LENGTH( str )
```

<a id="7911e14787f70c0c"></a>
#### Description

CHAR_LENGTH returns the number of character for str according to the character set.

The str can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or it can be a data type which can be converted to character type. The return type is NATIVE_BIGINT.

If the data type of str is CHARACTER, the trailing blanks are included in the calculation.  
If str is NULL, it returns NULL.

It is an alias of [LENGTH](#dc5af3c589ed5f26).

<a id="9c29972150d5e8a4"></a>
#### Example

Multi byte character set: (e.g. UTF8)

```
gSQL> SELECT CHAR_LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="0fd684a8ebce7997"></a>
### CHR

<a id="63ecc979cc71f80f"></a>
#### Syntax

```
CHR( num )
```

<a id="1024cc509e573c38"></a>
#### Description

It returns a character in the database character set code corresponding to num.

An input argument can be a numeric type and the return type is VARCHAR.

<a id="4aec5cdce18496c7"></a>
#### Example

```
gSQL> SELECT CHR(71) FROM DUAL;
CHR(71)
-------
G      
1 row selected.
```

<a id="6f063576d028e346"></a>
### CLOCK_DATE

<a id="e195ea17ca9ac359"></a>
#### Syntax

```
CLOCK_DATE()
```

<a id="2a8bce2972a1682e"></a>
#### Description

Whenever the CLOCK_DATE function is called, the current date (DATE type) value is obtained.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="2fbaa3587edfc4dc"></a>
#### Example

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

<a id="9f4b01fffd6b5962"></a>
### CLOCK_LOCALTIME

<a id="fc06f22ac140bdbf"></a>
#### Syntax

```
CLOCK_LOCALTIME()
```

<a id="f0746c71f6c1022a"></a>
#### Description

Whenever the CLOCK_LOCALTIME function is called, the current time value without TIME ZONE (TIME WITHOUT TIME ZONE type) is obtained.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.  
• STATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="2816c19e5c59d29e"></a>
#### Example

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

<a id="a76b0c51947a496d"></a>
### CLOCK_LOCALTIMESTAMP

<a id="4a1a8e0e70941e52"></a>
#### Syntax

```
CLOCK_LOCALTIMESTAMP()
```

<a id="17663e152b104e14"></a>
#### Description

Whenever the CLOCK_LOCALTIMESTAMP() function is called, the current TIMESTAMP value without TIME ZONE (TIMESTAMP WITHOUT TIME ZONE type) is obtained.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• STATEMENT_LOCALTIMESTAMP(): All TIMESTAMP values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="9af763bcb4b6cc6b"></a>
#### Example

Each row can have a different timestamp value.

```
gSQL> SELECT CLOCK_LOCALTIMESTAMP() FROM t1;

CLOCK_LOCALTIMESTAMP()    
--------------------------
2013-12-12 14:46:17.309206
2013-12-12 14:46:17.309209
2013-12-12 14:46:17.309209
```

<a id="8374f60df78d55d3"></a>
### CLOCK_TIME

<a id="2cdc3582d0e2d001"></a>
#### Syntax

```
CLOCK_TIME()
```

<a id="129b5c72534ee77d"></a>
#### Description

Whenever the CLOCK_TIME() function is called, the current time value with TIME ZONE (TIME WITH TIME ZONE type) is obtained.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• STATEMENT_TIME(): All time values in an SQL statement are same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="f18ee943c7c96a17"></a>
#### Example

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

<a id="14cc788c7cd87a3c"></a>
### CLOCK_TIMESTAMP

<a id="876398ffefdfb413"></a>
#### Syntax

```
CLOCK_TIMESTAMP()
```

<a id="7ecbf8eb4fd12f2b"></a>
#### Description

Whenever CLOCK_TIMESTAMP() function is called, the current TIMESTAMP value with TIME ZONE (TIMESTAMP WITH TIME ZONE type) is obtained.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_TIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• STATEMENT_TIMESTAMP(): All TIMESTAMP values in an SQL statement are same.   
• CLOCK_TIMESTAMP(): Whenever the function is called, the current TIMESTAMP value is obtained.

<a id="ab645a3619c7bdd1"></a>
#### Example

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

<a id="2f66c19ba9c3c73f"></a>
### COALESCE

<a id="d695c7c523ebb65d"></a>
#### Syntax

```
COALESCE( expr1, ..., exprN )
```

<a id="bdad501c3844aa6f"></a>
#### Description

It returns the first non null expr in the expr list.  
If all expr in the expr list are null, it returns null.  
In the expr list, there should be two or more expr.

If multiple types are in the expr list, the result type is determined by the [Result Type Combination Rule](#7b9ef315990930de).

COALESCE can be expressed by using CASE as follows.

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

<a id="a5df0b7b73e4bef4"></a>
#### Example

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

<a id="cf7e8a29d9f60724"></a>
### CONCAT

<a id="0b3f74980dbfd09d"></a>
#### Syntax

```
CONCAT( str1, str2, ... )
```

<a id="4019a628a89c3b6a"></a>
#### Description

It is an alias of || ( CONCATENATE ).  
It is an argument of CONCAT function and 2 ~ 254 number of CONCATs can be set.  
For more information, refer to [|| (CONCATENATE)](#917f504cb710ba23), [CONCATENATE](#5f5f25ab865e559d).

<a id="a64bcb62185fbeb3"></a>
#### Example

```
gSQL> SELECT CONCAT( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="5f5f25ab865e559d"></a>
### CONCATENATE

<a id="96861d1d59d98cbc"></a>
#### Syntax

```
CONCATENATE( str1, str2, ... )
```

<a id="bcfe4a3dfde4282c"></a>
#### Description

It is an alias of || ( CONCATENATE ).  
It is an argument of CONCATENATE  function and 2 ~ 254 number of CONCATENATEs can be set.  
For more information, refer to [CONCAT](#cf7e8a29d9f60724), [|| (CONCATENATE)](#917f504cb710ba23).

<a id="175e795dd02e8857"></a>
#### Example

```
gSQL> SELECT CONCATENATE( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="cd7aa4cdaad0ea5d"></a>
### COS

<a id="e9bbefeef74faef8"></a>
#### Syntax

```
COS(num)
```

<a id="01ab04ae184e76f8"></a>
#### Description

It returns the COSINE value of num.  
If the num argument is NULL, the result is also NULL.

<a id="6065cc4d06e4b2b6"></a>
#### Example

```
gSQL> SELECT COS( 0 ) FROM DUAL;
COS( 0 )
--------
       1
1 row selected.
```

<a id="c976849a3a444b6b"></a>
### COT

<a id="b2b150830da5631d"></a>
#### Syntax

```
COT(num)
```

<a id="97a5457e6401120c"></a>
#### Description

It returns the COTANGENT value of num.  

If the num argument is NULL, the result is also NULL.

<a id="fad885485191e900"></a>
#### Example

```
gSQL> SELECT COT( 1 ) FROM DUAL;
        COT( 1 )
----------------
.642092615934331
1 row selected.
```

<a id="79fa00ba0bfca24c"></a>
### COUNT

<a id="e7c02a894444dbab"></a>
#### Syntax

```
COUNT( [ ALL | DISTINCT ] expr )
```

<a id="3682ddd9065caef3"></a>
#### Description

It is an aggregate function. It returns the number of rows whose expr is not NULL.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

<a id="e9797e789023f356"></a>
#### Example

```
gSQL> SELECT COUNT(c1) FROM t1;

COUNT(C1)
---------
        3

1 row selected.
```

<a id="63f5d99817501bb1"></a>
### COUNT(*)

<a id="8124b9d3c8551e38"></a>
#### Syntax

```
COUNT(*)
```

<a id="4dd2e58803cbc434"></a>
#### Description

It is an aggregate function, and the number of rows is obtained.  
It has nothing to do with whether it is NULL or not because an expression is not explicitly specified.

<a id="66e26ffdbcc3a154"></a>
#### Example

```
gSQL> SELECT COUNT(*) FROM t1;

COUNT(*)
--------
       4

1 row selected.
```

<a id="97d4603c31df7d25"></a>
### CURRENT_CATALOG

<a id="fc37549e92703b2a"></a>
#### Syntax

```
CURRENT_CATALOG [()]
```

<a id="df3c788e43ff6bab"></a>
#### Description

The catalog name (database name) is obtained.

<a id="ec5a2a91c99b29a7"></a>
#### Example

```
gSQL> SELECT CURRENT_CATALOG FROM dual;

CURRENT_CATALOG
---------------
TEST_DB        

1 row selected.
```

<a id="42efebf33a44b909"></a>
### CURRENT_DATE

<a id="f35456f4d6c10298"></a>
#### Syntax

```
CURRENT_DATE [()]
STATEMENT_DATE()
```

<a id="ec528540dc565e2f"></a>
#### Description

The current date (DATE type) is obtained.

CURRENT_DATE is an SQL standard function.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• CURRENT_DATE, STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="6ec507ba8251a20e"></a>
#### Example

```
gSQL> SELECT CURRENT_DATE FROM t1;

CURRENT_DATE
------------
2013-12-12  
2013-12-12  
2013-12-12  

3 rows selected.
```

<a id="7f63d2fcb279719c"></a>
### CURRENT_SCHEMA

<a id="5ec439b918324c80"></a>
#### Syntax

```
CURRENT_SCHEMA [()]
```

<a id="b1a25f82aecc9f52"></a>
#### Description

User's current SCHEMA is obtained.

<a id="089d286defba6e6f"></a>
#### Example

```
gSQL> SELECT CURRENT_SCHEMA FROM dual;

CURRENT_SCHEMA
--------------
PUBLIC        

1 row selected.
```

<a id="406eee865fb2c767"></a>
### CURRENT_TIME

<a id="35db901e4e68684f"></a>
#### Syntax

```
CURRENT_TIME [()]
STATEMENT_TIME()
```

<a id="42318c569e496d36"></a>
#### Description

The current TIME WITH TIME ZONE type value based on the session time is obtained.

CURRENT_TIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• CURRENT_TIME, STATEMENT_TIME(): All time values in an SQL statement are same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="26953132de11dc79"></a>
#### Example

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

<a id="cf40f2352a534e8c"></a>
### CURRENT_TIMESTAMP

<a id="9a918244822d0e30"></a>
#### Syntax

```
CURRENT_TIMESTAMP [()]
STATEMENT_TIMESTAMP()
```

<a id="9550cb1564fb9aee"></a>
#### Description

It obtains the TIMESTAMP WITH TIME ZONE type value based on the session time.

CURRENT_TIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_TIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• CURRENT_TIMESTAMP, STATEMENT_TIMESTAM(): All TIMESTAMP values in an SQL statement are same.  
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="fa3b675272f0dc2e"></a>
#### Example

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

<a id="3439ccb21bfded13"></a>
### CURRENT_USER

<a id="f2d1138105c46893"></a>
#### Syntax

```
CURRENT_USER [()]
```

<a id="a645d8d81faffae3"></a>
#### Description

It returns the current user.

The user information is managed in three types as follows.

- Logon user: It is a user who performed login, and it is maintained until the connection is closed.
- Session user: It is as same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: It is generally as same as the session user, but it is temporarily changed internally in system to control access when using the PSM, view.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="fd41a35864dc9154"></a>
#### Example

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

<a id="564199c8f133c07b"></a>
### CURRVAL

<a id="fcaaa4376133e351"></a>
#### Syntax

```
seq_name.CURRVAL
CURRVAL(seq_name)
```

<a id="c12da1778a4e4783"></a>
#### Description

The current value of the sequence object is obtained.

A sequence value should be set with NEXTVAL(seq_name) at least once.

<a id="704c32496e6f5ef8"></a>
#### Example

```
gSQL> SELECT seq.CURRVAL FROM dual;

SEQ.CURRVAL
-----------
          1

1 row selected.
```

<a id="49a793f8c6a4ead4"></a>
### DATEADD

<a id="a41077c9f853a754"></a>
#### Syntax

```
DATEADD( datepart, number, date )
```

<a id="06c55d4f3bc29ae9"></a>
#### Description

It adds number to the specified datepart of date, and returns the result.

If the number is decimal point, it is not rounded off.  
The date data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE.  
If number or date is NULL, the result is also NULL.

The result type which is as same as the input date argument type is returned.

**Available string format in datepart**

<a id="83346d0fdfa5b763"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">Description</th></tr><tr><td>YEAR</td><td>Year</td></tr><tr><td>QUARTER</td><td>Quarter</td></tr><tr><td>MONTH</td><td>Month</td></tr><tr><td>DAYOFYEAR</td><td>Day of year</td></tr><tr><td>DAY</td><td>Day</td></tr><tr><td>WEEK</td><td>Week</td></tr><tr><td>WEEKDAY</td><td>Weekday</td></tr><tr><td>HOUR</td><td>Hour</td></tr><tr><td>MINUTE</td><td>Minute</td></tr><tr><td>SECOND</td><td>Second</td></tr><tr><td>MILLISECOND</td><td>Millisecond</td></tr><tr><td>MICROSECOND</td><td>Microsecond</td></tr></tbody></table>

<a id="52f05a777e9e03b8"></a>
#### Example

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

<a id="84c0f25f4ed73fec"></a>
### DATEDIFF

<a id="3752c2a6a3eef00a"></a>
#### Syntax

```
DATEDIFF( datepart, startdate, enddate )
```

<a id="6f4f5f18e82bccde"></a>
#### Description

It substracts startdate from enddate, then returns the result to the specified datepart.

If the startdate or enddate is NULL, the result is also NULL.  
The data type of startdate and enddate can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME.

The result type is NUMBER.

**Available string format in datepart**

<a id="2f2309e88e98d774"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">Description</th></tr><tr><td>YEAR</td><td>Year</td></tr><tr><td>QUARTER</td><td>Quarter</td></tr><tr><td>MONTH</td><td>Month</td></tr><tr><td>DAYOFYEAR</td><td>Day of year</td></tr><tr><td>DAY</td><td>Day</td></tr><tr><td>HOUR</td><td>Hour</td></tr><tr><td>MINUTE</td><td>Minute</td></tr><tr><td>SECOND</td><td>Second</td></tr><tr><td>MILLISECOND</td><td>Millisecond</td></tr><tr><td>MICROSECOND</td><td>Microsecond</td></tr></tbody></table>

<a id="901acf09bdfb3aad"></a>
#### Example

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

<a id="21bfa491b404217f"></a>
### DATE_ADD

<a id="67861635837f9bc2"></a>
#### Syntax

```
DATE_ADD( date, INTERVAL expr unit  )
```

<a id="95e3a190c4e2ee74"></a>
#### Description

It is the same function as [ADDDATE](#fc62fbea08ef6611) (date, INTERVAL expr unit).

<a id="281227b72546cb14"></a>
#### Example

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

<a id="1362fd95fc14f2a7"></a>
### DATE_PART

<a id="d9b4888da353b7c2"></a>
#### Syntax

```
DATE_PART( field, datetime )
```

<a id="3838eaa8a085a8ea"></a>
#### Description

The result of DATE_PART is as same as the result of the EXTRACT function. It searches for the specified field from the input datetime type, and returns it.

The field argument should be text literal, and YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, TIMEZONE_HOUR, TIMEZONE_MINUTE can be specified to text literal.  
The datetime argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL.

If field is not in the range of datetime, an error is returned. For DATE type, field should be YEAR, MONTH, DAY, otherwise an error is returned.  

The return type is NUMBER.

For more information, refer to [EXTRACT](#cc4fdf75ce2721be).

<a id="f09379cb9f4e50c4"></a>
#### Example

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

<a id="368116d4fe5d0775"></a>
### DECODE

<a id="e37d2e8a3fd912cf"></a>
#### Syntax

```
DECODE( expr, comparison_expr1, result1
           [, comparison_expr2, result2
            , ...
            , comparison_exprN, resultN ]
           [, default ] )
```

<a id="a18a33feef69a349"></a>
#### Description

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

<a id="bdc2f6a0c13ece6b"></a>
#### Example

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

<a id="1c17f177307d3bfd"></a>
### DEGREES

<a id="31232a5fd453e368"></a>
#### Syntax

```
DEGREES( radians )
```

<a id="0cc531c26b47aebb"></a>
#### Description

It converts a degree radians to a value in degrees, and returns the converted value.

<a id="9633b7eebbeff695"></a>
#### Example

```
gSQL> SELECT DEGREES( PI() ) AS RESULT FROM DUAL;
RESULT
------
   180
1 row selected.
```

<a id="f601b11d1b300e45"></a>
### DIGEST

<a id="d146c768d219fb9e"></a>
#### Syntax

```
DIGEST( data, type )
```

<a id="88206146db754418"></a>
#### Description

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

<a id="79ee928f44e9275b"></a>
#### Example

```
gSQL> SELECT HEX( DIGEST( 'my password', 'SHA256' ) ) AS RESULT FROM DUAL;

RESULT                                                          
----------------------------------------------------------------
BB14292D91C6D0920A5536BB41F3A50F66351B7B9D94C804DFCE8A96CA1051F2

1 row selected.
```

<a id="6ff88b1ac03220b2"></a>
### DUMP

<a id="8e1012bb390a5cc2"></a>
#### Syntax

```
DUMP( expr )
```

<a id="58b3d400ae266c8e"></a>
#### Description

It returns internal representation information of expr.  
Internal representation information is displayed as the data type, byte length and data information.

expr can be any data types, and the return type is CHARACTER VARYING.

<a id="60211d477abdc81c"></a>
#### Example

```
gSQL> SELECT DUMP( 'DUMP' ) AS RESULT FROM DUAL;
RESULT                           
---------------------------------
Type=CHAR Len=4 : Str=68,85,77,80
1 row selected.
```

<a id="39645d4f45d9f0c2"></a>
### EXP

<a id="ab10af3b27113fa3"></a>
#### Syntax

```
EXP( num )
```

<a id="206578a7ac3a85ba"></a>
#### Description

It returns squared value of e (base of natural logarithm)'s num.

<a id="bd0bba4e8a37bdff"></a>
#### Example

```
gSQL> SELECT EXP( 1 ) AS RESULT FROM DUAL;
          RESULT
----------------
2.71828182845905
1 row selected.
```

<a id="cc4fdf75ce2721be"></a>
### EXTRACT

<a id="5352bb4e9b3d1af6"></a>
#### Syntax

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

<a id="9934836b84e40895"></a>
#### Description

It searches for the specified field from an input datetime type, and returns it.

The datetime argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL.

If field is not in the range of datetime, an error is returned.   
For DATE type, the field should be YEAR, MONTH, DAY, otherwise an error is returned.  
The return type is NUMBER.

Result of EXTRACT is as same as the result of the [DATE_PART](#1362fd95fc14f2a7) function.

<a id="029a74169b3b766f"></a>
#### Example

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

<a id="85c6baee4193141e"></a>
### FACTORIAL

<a id="0e2cc116db98b35e"></a>
#### Syntax

```
FACTORIAL( num )
```

<a id="d9577632fe7e950a"></a>
#### Description

It multiplies the successive natural numbers from 1 to num in order, and returns the result.

<a id="f61466d8567289fe"></a>
#### Example

```
gSQL> SELECT FACTORIAL( 5 ) AS RESULT FROM DUAL;
RESULT
------
   120
1 row selected.
```

<a id="c193f1462bbadbdb"></a>
### FLOOR

<a id="3dcf76cf70032be1"></a>
#### Syntax

```
FLOOR( num )
```

<a id="e6e51b84b7dd4db8"></a>
#### Description

It returns the biggest integer which is equal to or smaller than num.

<a id="a4320a93f0d778b7"></a>
#### Example

```
gSQL> SELECT FLOOR(42.8) AS RESULT1, FLOOR(-42.8) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     42     -43
1 row selected.
```

<a id="f99ff94c769c793e"></a>
### FROM_BASE64

<a id="119003be394e09d0"></a>
#### Syntax

```
FROM_BASE64( str )
```

<a id="aff9b9d3336e0c10"></a>
#### Description

The converted character by base 64 encoding is input to FROM_BASE64, then the decoded binary string is returned.

The input argument data type can be a character type such as CHARACTER VARYING, CHARACTER LONG VARYING, and the result type is a binary character such as BINARY VARYING or BINARY LONG VARYING.

If str is NULL, then the result value is also NULL.  
If str includes characters which are not in the range of base64 character, then it returns an error.  
A newline, carriage return, tab, and space of str is ignored when decoding.

For more information, refer to [TO_BASE64](#5ae9c294a6c57303).

<a id="67bc93e4d3afec17"></a>
#### Example

```
gSQL> SELECT FROM_BASE64( TO_BASE64( 'abc' ) ),
             FROM_BASE64( TO_BASE64( 'abcd' ) ) 
        FROM DUAL;
FROM_BASE64( TO_BASE64( 'abc' ) ) FROM_BASE64( TO_BASE64( 'abcd' ) )
--------------------------------- ----------------------------------
616263                            61626364                          
1 row selected.
```

<a id="92b4d4ac77f31342"></a>
### GREATEST

<a id="9e89a1af3b8bb7f5"></a>
#### Syntax

```
GREATEST( expr1 [, expr2, ... exprn ] )
```

<a id="3fa63a07474b5ddd"></a>
#### Description

It returns the largest value among the received expr argument.

If any expr argument is NULL, the result value is NULL.

The result type becomes the data type of expr1  (the first expr).   
If the data type of expr1 (the first expr) is a character type and a numeric type then it becomes the type including the range of expr1, ..., exprN each.  
If all of expr1, ..., exprN is described in CHAR type, then all exprs are compared in VARCHAR type and the result type is VARCHAR.

<a id="28013d87bf9c3647"></a>
#### Example

```
gSQL> SELECT GREATEST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
   200
1 row selected.
```

<a id="8037fe9dcc2be3fc"></a>
### HEX

<a id="b4e8e1b36bf4d698"></a>
#### Syntax

```
HEX( str )
```

<a id="83de27f2b204720d"></a>
#### Description

It returns a str argument in hexadecimal character.  
A str argument data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, a type which can be converted to a character type, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.  
The result type is a character type such as CHARACTER VARYING or CHARACTER LONG VARYING.

If str is NULL, then the result value is also NULL.

If an argument of HEX function is a numeric type, then it returns an error.   
To convert a decimal number to a hexadecimal number, use TO_CHAR() function by using  'X' number format.  
e.g. TO_CHAR( 255, 'XX' )

For more information, refer to [UNHEX](#074ed8a093c71249).

<a id="f97d64ad2ae20036"></a>
#### Example

```
gSQL> SELECT HEX( 'abc' ) FROM DUAL;
HEX( 'abc' )
------------
616263      
1 row selected.
```

<a id="d80f5e4a419f8f7d"></a>
### INITCAP

<a id="05ba384d706132ba"></a>
#### Syntax

```
INITCAP( str )
```

<a id="4e5a299178370cbc"></a>
#### Description

It converts the first letter in each word of string str into uppercase, and converts all other letters into lowercase, then it returns the result.

str data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

Each word in string is classified by white space or characters which are not alphanumeric.  
If str is NULL, the result is also NULL.

The return type is as same as str argument datatype.

<a id="2a6fb62f5fb7abd1"></a>
#### Example

```
gSQL> SELECT INITCAP( 'hi GLIESE' ) AS RESULT FROM DUAL;
RESULT   
---------
Hi Gliese
1 row selected.
```

<a id="20a87cfb135089bd"></a>
### INSTR

<a id="bd0e9667b6346d26"></a>
#### Syntax

```
INSTR( str, substr [, position [, occurrence ] ] )
```

<a id="17e453a214e40b77"></a>
#### Description

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

<a id="4da00c241b4d4452"></a>
#### Example

```
gSQL> SELECT INSTR( 'INSTR( STR, SUBSTR )', 'SUB' ) AS RESULT1,
             INSTR( 'INSTR( STR, SUBSTR )', 'SUB', 5 ) AS RESULT2
        FROM DUAL;
RESULT1 RESULT2
------- -------
     13      13
1 row selected.

gSQL> SELECT INSTR( 'INSTR( STR, SUBSTR )', 'STR', 6, 2 ) AS RESULT1,
             INSTR( 'INSTR( STR, SUBSTR )', 'STR', -6, 2 ) AS RESULT2
      FROM DUAL;
RESULT1 RESULT2
------- -------
     16       3
1 row selected.
```

<a id="c41960f76e6d586b"></a>
### LAST_DAY

<a id="4f596d872574a5cf"></a>
#### Syntax

```
LAST_DAY( date )
```

<a id="74cc813f2802540a"></a>
#### Description

It returns the last day of the month which is included in date.

The date argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.  
The return type is always DATE regardless of the date argument data type.

<a id="b9900711657231fd"></a>
#### Example

```
gSQL> SELECT 
      LAST_DAY( TO_DATE( '2012-07-10', 'YYYY-MM-DD' ) ) AS RESULT FROM DUAL;
RESULT    
----------
2012-07-31
1 row selected.
```

<a id="449eb64862a9ab35"></a>
### LAST_IDENTITY_VALUE

<a id="577d4e2142f24278"></a>
#### Syntax

```
LAST_IDENTITY_VALUE()
```

<a id="3b5acf86c8c7dd77"></a>
#### Description

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

To obtain an identity column value created when performing the INSERT, use [INSERT INTO name RETURNING .. INTO](16-sql-references.md#be8a8f852c974819) statement as follows.

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

<a id="5b990fecbeca09d4"></a>
#### Example

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

<a id="3613239b9d2c8956"></a>
### LEAST

<a id="2a33c0939dfee6f0"></a>
#### Syntax

```
LEAST( expr1 [, expr2, ... exprn ] )
```

<a id="fea0377eaf4db643"></a>
#### Description

It returns the smallest value among received expr arguments.

If any of expr is NULL, the result is NULL.

The result type is determined according to the data type of expr1 (the first expr).   
If the data type of expr1 (the first expr) is a character type and a numeric type then it becomes the type including the range of expr1, ..., exprN each.  
If all of expr1, ..., exprN is described in CHAR type, then all exprs are compared in VARCHAR type and the result type is VARCHAR.

<a id="4b0f218b857882e6"></a>
#### Example

```
gSQL> SELECT LEAST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="dc5af3c589ed5f26"></a>
### LENGTH

<a id="ce2cdf2dd1b8f6e8"></a>
#### Syntax

```
LENGTH( str )
```

<a id="dc9e32f7d65c219b"></a>
#### Description

It is an alias of [CHAR_LENGTH](#2eca28868d47dbb6).

<a id="a3b4a7dde6130ada"></a>
#### Example

Multi byte character set: (e.g.UTF8)

```
gSQL> SELECT LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="20776ee9a823baa5"></a>
### LENGTHB

<a id="ec5a466eb89d1bcc"></a>
#### Syntax

```
LENGTHB( str )
```

<a id="382599cbc7a1a037"></a>
#### Description

It is an alias of [OCTET_LENGTH](#aa49ee5d59240063).  
For more information, refer to [BYTE_LENGTH](#1bbb0c781e8dcb83).

<a id="c6cd941781bf682d"></a>
#### Example

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

<a id="33f8c9daee11124d"></a>
### LN

<a id="fdea2d39a8a8e852"></a>
#### Syntax

```
LN( num )
```

<a id="42a3894b744fa340"></a>
#### Description

It returns the natural logarithm value of num.  
num should be a value which is bigger than 0.

<a id="35d45ed6585ae6dd"></a>
#### Example

```
gSQL> SELECT LN( 2.71828182845905 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="14cb2452ce1695c1"></a>
### LOCALTIME

<a id="f18057d9eaa62925"></a>
#### Syntax

```
LOCALTIME [()]
STATEMENT_LOCALTIME()
```

<a id="1619359735d254bc"></a>
#### Description

The current TIME WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.  
• LOCALTIME, STATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="049c46df2450ab22"></a>
#### Example

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

<a id="65a9dfe6178838e6"></a>
### LOCALTIMESTAMP

<a id="c853e3cdedff4b49"></a>
#### Syntax

```
LOCALTIMESTAMP [()]
STATEMENT_LOCALTIMESTAMP()
```

<a id="46b1233ba55350b6"></a>
#### Description

The current TIMESTAMP WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current TIMESTAMP are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All TIMESTAMP values in the transaction are same.  
• LOCALTIMESTAMP, STATEMENT_LOCALTIMESTAMP(): All TIMESTAMP values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="3ceafe62ff8557d9"></a>
#### Example

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

<a id="4ae03fd6c008cab2"></a>
### LOCAL_GROUP_ID

<a id="fa6daa05dca7544b"></a>
#### Syntax

```
LOCAL_GROUP_ID()
```

<a id="cb7a140c12454c41"></a>
#### Description

It returns a cluster group ID for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="fde62ce5ad1ef0c8"></a>
#### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_GROUP_ID() FROM DUAL;

LOCAL_GROUP_ID()
----------------
               1

1 row selected.
```

<a id="491ad632708bc8d1"></a>
### LOCAL_GROUP_NAME

<a id="d1cb8bcd01c92c50"></a>
#### Syntax

```
LOCAL_GROUP_NAME()
```

<a id="14948a9678c3d9ee"></a>
#### Description

It returns a cluster group name for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="eb73111eb97228ce"></a>
#### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_GROUP_NAME() FROM DUAL;

LOCAL_GROUP_NAME()
------------------
G1                

1 row selected.
```

<a id="af1b718fdee145ee"></a>
### LOCAL_MEMBER_ID

<a id="f9e5fbc2b1c3c3bf"></a>
#### Syntax

```
LOCAL_MEMBER_ID()
```

<a id="90e8f12c5d3a00a7"></a>
#### Description

It returns a cluster member ID for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="6506ef70b470eb56"></a>
#### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_MEMBER_ID() FROM DUAL;

LOCAL_MEMBER_ID()
-----------------
                1

1 row selected.
```

<a id="62eefce3152a96f5"></a>
### LOCAL_MEMBER_NAME

<a id="377ba52e34593902"></a>
#### Syntax

```
LOCAL_MEMBER_NAME()
```

<a id="704b365a7572666c"></a>
#### Description

It returns a cluster member name for a server which processes a query from a user.

> It is a valid information in a cluster system.

<a id="7dacb389c2eff192"></a>
#### Example

All rows have the same value.

```
gSQL> SELECT LOCAL_MEMBER_NAME() FROM DUAL;

LOCAL_MEMBER_NAME()
-------------------
G1N1               

1 row selected.
```

<a id="23e6513ead447ac6"></a>
### LOG

<a id="3010bcac052a2813"></a>
#### Syntax

```
LOG( num2 )
LOG( num1, num2 )
```

<a id="1dac140067e99737"></a>
#### Description

It returns the logarithm of num2 in the num1 base.  
If num1 is omitted, it returns the logarithm value whose base is 10.

num1 should be a positive number except 1 and 0, and num2 should be a positive number.

<a id="b7cf34f1510766b8"></a>
#### Example

```
gSQL> SELECT LOG( 100 ) AS RESULT1, LOG( 4, 16 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      2       2
1 row selected.
```

<a id="f3552430bea50cd2"></a>
### LOGON_USER

<a id="ac18570efec772a7"></a>
#### Syntax

```
LOGON_USER()
```

<a id="92590263f92d9ac1"></a>
#### Description

It returns the logged-in user.

The user information is managed in three types as follows.

- Logon user: It is a user who performed login, and it is maintained until the connection is closed.
- Session user: It is as same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: It is generally as same as the session user, but it is temporarily changed internally in system to control access when using the PSM, view.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="14d54a557dedeea5"></a>
#### Example

```
% gsql test test

gSQL> SELECT LOGON_USER() AS result FROM DUAL;

RESULT
------
TEST  

1 row selected.
```

<a id="20ef3cb6fa1ffd96"></a>
### LOWER

<a id="65a9bfb3ce6f6aa2"></a>
#### Syntax

```
LOWER( str )
```

<a id="ebc646e1f71cc54c"></a>
#### Description

It returns lowercases of str.

The str argument data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If str is NULL, the result is also NULL.

The return type is the same datatype as the str argument.

<a id="d09a66dc35ece821"></a>
#### Example

```
gSQL> SELECT LOWER( 'SPRING' ) AS RESULT FROM DUAL;
RESULT
------
spring
1 row selected.
```

<a id="7050c762d819354f"></a>
### LPAD

<a id="eddc05c7cc8e503f"></a>
#### Syntax

```
LPAD( str, length, [, fill] )
```

<a id="ffc3938f418cb11a"></a>
#### Description

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

<a id="71f8be18213708af"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="cc6e7374909798b3"></a>
#### Example

```
gSQL> SELECT LPAD( 'aa', 5, 'b' ) AS RESULT FROM DUAL;
RESULT
------
bbbaa 
1 row selected.
```

<a id="f948b1d10dca4377"></a>
### LTRIM

<a id="901d8aa0aba9caee"></a>
#### Syntax

```
LTRIM( trim_source [, trim_character ] )
```

<a id="96162d391f80dcb3"></a>
#### Description

It removes the matching characters by comparing from the left side of trim_character in trim_source until the matching character does not exist. Then it returns the result.

The data type of trim_character and trim_source arguments can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, and a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If any of trim_character, trim_source is NULL, the result is NULL.  
If trim_character is omitted, a single blank space (' ') is specified by default.

The following table describes the result types.

**Result type of LTRIM**

<a id="be6a7eec5c77437f"></a>
| trim_source, trim_character type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="d203fd9f65e6b7d7"></a>
#### Example

```
gSQL> SELECT LTRIM( '_____LTRIM', '_' ) AS RESULT FROM DUAL;
RESULT
------
LTRIM 
1 row selected.
```

<a id="33196967d64cc7dc"></a>
### MAX

<a id="fdcfb7818570548d"></a>
#### Syntax

```
MAX( [ ALL | DISTINCT ] expr )
```

<a id="b3c557b45f078179"></a>
#### Description

It is an aggregate function and the maximum value among rows' exprs is obtained.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

MAX function returns the same result without being affected by the ALL and DISTINCT.

<a id="3ef6aad9f9c5ca57"></a>
#### Example

```
gSQL> SELECT MAX(c1) FROM t1;

MAX(C1)
-------
      3

1 row selected.
```

<a id="372b04034981ef63"></a>
### MIN

<a id="da93126e8069b60f"></a>
#### Syntax

```
MIN( [ ALL | DISTINCT ] expr )
```

<a id="00a448705e89da89"></a>
#### Description

It is an aggregate function and the minimum value among rows' exprs is obtained.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

MIN function returns the same result without being affected by the ALL and DISTINCT.

<a id="14abc9489d51262a"></a>
#### Example

```
gSQL> SELECT MIN(c1) FROM t1;

MIN(C1)
-------
      1

1 row selected.
```

<a id="9b6e83832f14f490"></a>
### MOD

<a id="752a9b22cdcfcf62"></a>
#### Syntax

```
MOD( num1, num2 )
```

<a id="62a56054d77be3f9"></a>
#### Description

It divides num1 by num2, and returns the remainder.  

The num1 argument and num2 argument can be a numeric data type.  

If num2 is 0, an error is returned.

<a id="49303c3aee26e150"></a>
#### Example

```
gSQL> SELECT MOD(5, 4) AS RESULT1, MOD(-5, 4) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1      -1
1 row selected.
```

<a id="d02398fbef36e530"></a>
### MONTHS_BETWEEN

<a id="b7cbc7ef646a2acb"></a>
#### Syntax

```
MONTHS_BETWEEN( date1, date2 )
```

<a id="b5e8856495f6922c"></a>
#### Description

MONTHS_BETWEEN returns the number of months of which days between date2 and date1 are divided by 31.

If date1 or date2 is NULL, then the result is also NULL.  
The date1 argument and date2 argument can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE type.

The result type is NUMBER.

> If the same date (e.g. 2014-01-15 and 2014-02-15), or the last day of the month (e.g. 2014-08-31 and 2014-09-30) is included both in date1 and date2, then it returns the integer result regardless of the agreement of timestamp section (if it exists).

<a id="1d2d7d5d9f8b8ff3"></a>
#### Example

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

<a id="5e33b785272e916e"></a>
### NEXT_DAY

<a id="4ce6e124c06c4a81"></a>
#### Syntax

```
NEXT_DAY( date, day )
```

<a id="36a56830e74ebc78"></a>
#### Description

It obtains a date of the day (day of week) which comes first after the given date (an argument).

The second day argument can be a string or a number which indicates the day.  
• String: SUNDAY ~ SATURDAY  or SUN ~ SAT  
• Number: 1 (sunday) ~ 7 (saturday)

The return type is always DATE regardless of the input type of the date.  
The hour, minute and second of the result value returns the same hour, minute and second of the input argument date.

<a id="85a2e48c81a58b74"></a>
#### Example

```
gSQL> SELECT NEXT_DAY( TO_DATE( '2010-05-01', 'YYYY-MM-DD' ),
                       'SUNDAY' ) AS RESULT1 
        FROM DUAL;

RESULT1   
----------
2010-05-02

gSQL> SELECT NEXT_DAY( TO_DATE( '2010-05-01', 'YYYY-MM-DD' ),
                       'SUN' ) AS RESULT1 
        FROM DUAL;

RESULT1   
----------
2010-05-02

gSQL> SELECT NEXT_DAY( TO_DATE( '2010-05-01', 'YYYY-MM-DD' ),
                       1 ) AS RESULT1 
        FROM DUAL;

RESULT1   
----------
2010-05-02

gSQL> SELECT TO_CHAR( NEXT_DAY( TO_DATE( '2010-05-01', 'YYYY-MM-DD' ),
                                'SUNDAY' ),
                      'YYYY-MM-DD HH24:MI:SS' ) AS RESULT2 
        FROM DUAL;

RESULT2            
-------------------
2010-05-02 00:00:00
```

<a id="39329e8ee5b2fa13"></a>
### NEXTVAL

<a id="b2395dfbc8da413e"></a>
#### Syntax

```
seq_name.NEXTVAL
NEXTVAL( seq_name )
NEXT VALUE FOR seq_name
```

<a id="af573171d8df104b"></a>
#### Description

It obtains the next value of the sequence object.

<a id="66a8f35a414a791c"></a>
#### Example

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

<a id="68b32611305a934d"></a>
### NULLIF

<a id="bf87ed78d01de2ea"></a>
#### Syntax

```
NULLIF( expr1, expr2 )
```

<a id="2d43d3167ffe8d88"></a>
#### Description

If expr1 is equal to expr2, it returns NULL. If it is not equal it returns expr1 which is the first argument.

If the data types of expr1 and expr2 are different, the result type is determined by [Result Type Combination Rule](#7b9ef315990930de).

NULLIF can be expressed by using CASE as follows.

- NULLIF( expr1, expr2 )

```
CASE WHEN expr1 = expr2 THEN NULL 
       ELSE expr1 
  END
```

<a id="65a5c9c82990c406"></a>
#### Example

```
gSQL> SELECT NULLIF( 'SUN', 'SUN' ) AS RESULT1, 
             NULLIF( 'SUN', 'MOON' ) AS RESULT2 
       FROM DUAL;
RESULT1 RESULT2
------- -------
null    SUN    
1 row selected.
```

<a id="f4977777f7c3da09"></a>
### NVL

<a id="7069554394bd806d"></a>
#### Syntax

```
NVL( expr1, expr2 )
```

<a id="3f71e047c3048699"></a>
#### Description

If expr1 is not NULL, then it returns expr1. If expr1 is NULL, it returns expr2.

The result type is determined according to the data type of expr1.  
If NULL is described in expr1, then the result type is determined according to the data type of expr2.   
If the data type of expr1 is a character type and a numeric type then it becomes the type including the range of expr1 and expr2 each.  
If the data type of both expr1 and expr2 is CHAR type, then the result type is VARCHAR.

<a id="634762ca614e9ac2"></a>
#### Example

```
gSQL> SELECT I1, NVL( I1, 0 ) FROM T1;
  I1 NVL( I1, 0 )
---- ------------
   1            1
null            0
2 rows selected.
```

<a id="b52d0d48e4e25bdf"></a>
### NVL2

<a id="625eeda3bdacad5a"></a>
#### Syntax

```
NVL2( expr1, expr2, expr3 )
```

<a id="d94a3c101bdb1e9c"></a>
#### Description

If expr1 is not null, then it returns expr2. If expr1 is NULL, it returns expr3.

The result type is determined according to the data type of expr2.   
If NULL is described in expr2, then the result type is determined according to the data type of expr3.  
If the data type of expr2 is a character type and a numeric type then it becomes the type including the range of expr2 and expr3 each.  
If the data type of both expr2 and expr3 is CHAR type, then the result type is VARCHAR.

<a id="beaacb75ce1151df"></a>
#### Example

```
gSQL> SELECT I1, NVL2( I1, I1 * 1000, 0 ) FROM T1;
  I1 NVL2( I1, I1 * 1000, 0 )
---- ------------------------
   1                     1000
null                        0
2 rows selected.
```

<a id="aa49ee5d59240063"></a>
### OCTET_LENGTH

<a id="bbf31cf6e8c0b339"></a>
#### Syntax

```
OCTET_LENGTH( str )  

BYTE_LENGTH( str )     

LENGTHB( str )
```

<a id="c37c6c3dff5e973b"></a>
#### Description

It returns the number of bytes in str.

The str argument data type can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONGVARYING.

If the str data type is CHARACTER, the white spaces are included in the calculation.  
If str is NULL, the result is also NULL.

It is an alias of [BYTE_LENGTH](#1bbb0c781e8dcb83) and [LENGTHB](#20776ee9a823baa5).

<a id="e4eb2518452acded"></a>
#### Example

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

<a id="042f47383ad1bf70"></a>
### OVERLAY

<a id="057ecd734eb9e23c"></a>
#### Syntax

```
OVERLAY( str1 PLACING str2 FROM start_position  [ FOR string_length ] )
```

<a id="60c9c631e0686814"></a>
#### Description

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

For more information, refer to [SUBSTRING](#e3575b3c7baae2bb).

The following table describes the result types.

**Result type of OVERLAY**

<a id="c3812c78dbea9dc2"></a>
| str1, str2 types | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="1003a6fc0ba5ec0d"></a>
#### Example

```
gSQL> SELECT 
      OVERLAY( 'RESULT_OF_XXX_FUNC' PLACING 'OVERLAY' FROM 11 FOR 3 ) 
      AS RESULT 
      FROM DUAL;
RESULT                
----------------------
RESULT_OF_OVERLAY_FUNC
1 row selected.
```

<a id="2c39f94f95c55d14"></a>
### PI

<a id="7f73738539f00fe0"></a>
#### Syntax

```
PI()
```

<a id="4ae730178fc0a22b"></a>
#### Description

It returns "π" constant.

<a id="54ea6690ff43f6ef"></a>
#### Example

```
gSQL> SELECT PI() AS RESULT FROM DUAL;
              RESULT
--------------------
3.141592653589793E+0
1 row selected.
```

<a id="4420e99863c02102"></a>
### POSITION

<a id="5ea8a35697673fea"></a>
#### Syntax

```
POSITION( str1 IN str2 )
```

<a id="6690ab56b84bc965"></a>
#### Description

It searches for the first str1 within str2, then returns its location.

The data type of str1 argument and str2 argument can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If str1 can not be found within str2, the return value is 0.  
If str1 is found within str2, the position of str1 is returned, and the return value starts from 1.  
The returned position value is calculated in character unit (not in byte unit).  
If str1 or str2 is NULL, the return value is also NULL.

<a id="b6ca6d6ec9a24b0a"></a>
#### Example

```
gSQL> SELECT POSITION( 'CHAR' IN 'LONG CHAR 2000' ) AS RESULT FROM DUAL;
RESULT
------
     6
1 row selected.
```

<a id="0a5ad1f0fc0166a6"></a>
### POWER

<a id="57c29c43808847a5"></a>
#### Syntax

```
POWER( num1, num2 )
```

<a id="16024c365d458135"></a>
#### Description

It squares num1 to num2, and returns the result.

The num1 argument and num2 argument can be a numeric data type.  

If num1 is a negative number, num2 should be an integer.  
If num1 or num2 is NULL, the result is also NULL.

<a id="664905a0b6c2cc47"></a>
#### Example

```
gSQL> SELECT POWER( 2, 3 ) AS RESULT FROM DUAL;
RESULT
------
     8
1 row selected.
```

<a id="b108567e5848b3a7"></a>
### RADIANS

<a id="70fbc7d83d0d1c15"></a>
#### Syntax

```
RADIANS( degrees )
```

<a id="f353af1fd13c7b32"></a>
#### Description

It returns the radians of degrees.  

The degrees argument can be a numeric data type.

<a id="40839f6c880cc351"></a>
#### Example

```
gSQL> SELECT RADIANS( 180 ) AS RESULT FROM DUAL;
          RESULT
----------------
3.14159265358979
1 row selected.
```

<a id="79ba3d3328a95148"></a>
### RANDOM

<a id="9367e6e2a4d74b62"></a>
#### Syntax

```
RANDOM( min, max )
```

<a id="162bf2d49189c394"></a>
#### Description

It returns a random value in the range above min and below max.  

The min argument and max argument can be a numeric data type.

<a id="50e32747c475f6a2"></a>
#### Example

```
gSQL> SELECT RANDOM( 1, 100 ) AS RESULT FROM DUAL;
          RESULT
----------------
34.1870528003201
1 row selected.
```

<a id="b6ee30a80a455048"></a>
### REPEAT

<a id="6b7e135a049ee3e5"></a>
#### Syntax

```
REPEAT( str, num )
```

<a id="940f2d142e1ec766"></a>
#### Description

The string repeats str as many times as specified in num, and returns the result.

The str argument can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or a binary character type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

The num argument can be a numeric data type.

If either str or num is NULL, the result is also NULL.  
If num is 0 or a negative number, the result is also NULL.

The following table describes the result types.

**Result type of REPEAT**

<a id="0258c6231bb95cad"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="9369a891dcb256db"></a>
#### Example

```
gSQL> SELECT REPEAT( 'ab', 3 ) AS RESULT FROM DUAL;
RESULT
------
ababab
1 row selected.
```

<a id="5fc89474312dcfc2"></a>
### REPLACE

<a id="639b3aebdf306d95"></a>
#### Syntax

```
REPLACE( str, from, to )
```

<a id="68803d2d46e9dab5"></a>
#### Description

It replaces all *from* strings in str string with *to* strings, and returns the result.

The str argument, the from argument, and the to argument can be character data types such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If str is NULL, the result is also NULL.  
If from is NULL, the str is returned without replacement.  
If to value is omitted or NULL, the str value of which from is removed is returned.

The following table describes the result types.

**Result type of REPLACE**

<a id="5ae3585ea25550b2"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="601f9b6b86146f09"></a>
#### Example

```
gSQL> SELECT REPLACE( 'HI GLIESE', 'HI', 'HELLO' ) AS RESULT FROM DUAL;
RESULT      
------------
HELLO GLIESE
1 row selected.
```

<a id="ebd260b7c3d0fd65"></a>
### REVERSE

<a id="6a24d768db833af0"></a>
#### Syntax

```
REVERSE( str )
```

<a id="783e672389589723"></a>
#### Description

REVERSE returns characters of str in reverse order.

The str argument can be types that are convertible to a character string type or a binary string type.  
A character string type is performed in a character unit, and a binary string type can be performed in a byte unit.

If str is NULL, then it returns NULL.

The following table describes the arguments and result types.

**Argument and result type of REVERSE**

<a id="db0e4c3587da4328"></a>
| str | Result type |
| --- | --- |
| CHAR | CHAR |
| VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY | BINARY |
| VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="4347228479819028"></a>
#### Example

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

<a id="c8b3ec16eee4195e"></a>
### ROUND( number )

<a id="72dd07022ff5d5ba"></a>
#### Syntax

```
ROUND( num [, scale ] )
```

<a id="622e4b6be308782b"></a>
#### Description

It rounds off num based on scale, and returns the result.

The num argument and scale argument can be numeric data types.

If scale is omitted, the scale becomes 0 and is executed as if it is ROUND(num, 0).  
If scale is a positive number, it is rounded off based on the number of right digit of the decimal point. If scale is a negative number, it is rounded off based on the number of left digit of the decimal point.

<a id="bd7cea3ff4eff24b"></a>
#### Example

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

<a id="caf4d6b242635423"></a>
### ROUND( date )

<a id="c4dfe16b952fa549"></a>
#### Syntax

```
ROUND( date [ , fmt ] )
```

<a id="6dbf97e13a8080d1"></a>
#### Description

It rounds off the date in the specified fmt unit, and returns the result.

The data type of date argument can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.   
The fmt argument can be a character type such as CHARACTER, CHARACTER VARYING.   
The result type is always DATE regardless of the date argument data type.

If fmt is omitted, the default is DAY.  
The following table describes the available format strings.

**Available format sting of fmt**

<a id="a3b4a8887309f67e"></a>
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

<a id="a4cec8c5fd66d4e0"></a>
#### Example

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

<a id="7d33395f20dfc490"></a>
### ROWID_GRID_BLOCK_ID

<a id="a07bcef45c38992a"></a>
#### Syntax

```
ROWID_GRID_BLOCK_ID( rowid )
```

<a id="4e6c36922250867b"></a>
#### Description

It returns the GRID block ID.

> It is a valid information in a cluster system.

<a id="0d909b77783cf8a0"></a>
#### Example

```
gSQL> SELECT C1, ROWID_GRID_BLOCK_ID( ROWID ) FROM T1;
C1 ROWID_GRID_BLOCK_ID( ROWID )
-- ----------------------------
 1                           52
 2                           52
 3                           52

3 rows selected.
```

<a id="7db0634c14678f92"></a>
### ROWID_GRID_BLOCK_SEQ

<a id="736c9b8c7738b3f5"></a>
#### Syntax

```
ROWID_GRID_BLOCK_SEQ( rowid )
```

<a id="36e1e7599bf40925"></a>
#### Description

It returns the GRID block sequence.

> It is a valid information in a cluster system.

<a id="0805dd73babba0c8"></a>
#### Example

```
gSQL> SELECT C1, ROWID_GRID_BLOCK_SEQ( ROWID ) FROM T1;
C1 ROWID_GRID_BLOCK_SEQ( ROWID )
-- -----------------------------
 1                        747465
 2                        747466
 3                        747467

3 rows selected.
```

<a id="f1aa8d2905444ab8"></a>
### ROWID_MEMBER_ID

<a id="860cc7e3593e10c3"></a>
#### Syntax

```
ROWID_MEMBER_ID( rowid )
```

<a id="b00f91f0da168bb5"></a>
#### Description

It returns the member ID.

> It is a valid information in a cluster system.

<a id="5a13a5fa47a67a93"></a>
#### Example

```
gSQL> SELECT C1, ROWID_MEMBER_ID( ROWID ) FROM T1;
C1 ROWID_MEMBER_ID( ROWID )
-- ------------------------
 1                        1
 2                        1
 3                        1

3 rows selected.
```

<a id="d1b8e6f4947b8b65"></a>
### ROWID_OBJECT_ID

<a id="8f5850ce66078d95"></a>
#### Syntax

```
ROWID_OBJECT_ID( rowid )
```

<a id="c15e62e3c7894ca0"></a>
#### Description

It returns the object ID.

> It is an invalid information in a cluster system.

<a id="31decc3f85423f03"></a>
#### Example

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

<a id="52907e0ee66a7b9e"></a>
### ROWID_PAGE_ID

<a id="d0643f4cc1057a0c"></a>
#### Syntax

```
ROWID_PAGE_ID( rowid )
```

<a id="3b33ce861c6f7de4"></a>
#### Description

It returns the page ID.

> It is an invalid information in a cluster system.

<a id="08dc08bf9e45335c"></a>
#### Example

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

<a id="8d7c7bc10bcbc471"></a>
### ROWID_ROW_NUMBER

<a id="e74982f435edb689"></a>
#### Syntax

```
ROWID_ROW_NUMBER( rowid )
```

<a id="b69001290c3d5374"></a>
#### Description

It returns the row number.

> It is an invalid information in a cluster system.

<a id="2a70bb6d0d0b5e95"></a>
#### Example

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

<a id="db09c390bdf597e2"></a>
### ROWID_SHARD_ID

<a id="e4cd6bd5ea55fc61"></a>
#### Syntax

```
ROWID_SHARD_ID( rowid )
```

<a id="823465ea033160f0"></a>
#### Description

It returns the shard ID.

> It is a valid information in a cluster system.

<a id="d27d5cb14a1337ec"></a>
#### Example

```
gSQL> SELECT C1, ROWID_SHARD_ID( ROWID ) FROM T1;
C1 ROWID_SHARD_ID( ROWID )
-- -----------------------
 1                       0
 2                       1
 3                       2

3 rows selected.
```

<a id="c05f19eb31962101"></a>
### ROWID_TABLESPACE_ID

<a id="cf2daee2e0564b1e"></a>
#### Syntax

```
ROWID_TABLESPACE_ID( rowid )
```

<a id="6609aaf156697036"></a>
#### Description

It returns the tablespace ID.

> It is an invalid information in a cluster system.

<a id="8b7f5824251fa018"></a>
#### Example

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

<a id="c079dac1c5a3b312"></a>
### ROWNUM

<a id="832fd98491393555"></a>
#### Syntax

```
ROWNUM
```

<a id="138dc1c7dae10d02"></a>
#### Description

It sequentially allocates a number starting from 1 to rows which satisfy the WHERE condition.

It allows using ROWNUM in WHERE clause for the compatibility with Oracle.

However, to restrict the number of the query results, it is recommended to use [offset limit clause](16-sql-references.md#a7e3de58d6de6bbb) (the SQL standard) as follows.

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

<a id="32fd0a2d19410824"></a>
#### Example

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

<a id="c8f3cbca700acca7"></a>
### RPAD

<a id="128eef8f1d6a636d"></a>
#### Syntax

```
RPAD( str, length, [, fill] )
```

<a id="dd29e8b1d56b704e"></a>
#### Description

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

<a id="24d33f66735f2f7b"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="da4efd1d6b20263a"></a>
#### Example

```
gSQL> SELECT RPAD( 'aa', 5, 'b' ) AS RESULT FROM DUAL;
RESULT
------
aabbb 
1 row selected.
```

<a id="8f753ae671600f5f"></a>
### RTRIM

<a id="68891618ed4a524b"></a>
#### Syntax

```
RTRIM( trim_source [, trim_character ] )
```

<a id="4ea03a67cadb5770"></a>
#### Description

It removes the matching characters by comparing from the right side of trim_character in trim_source until the matching character does not exist. Then it returns the result.

The data type of trim_character and trim_source arguments can be a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING or a binary data type such as BINARY, BINARY VARYING, BINARY LONG VARYING.

If any of trim_character, trim_source is NULL, the result is NULL.  
If trim_character is omitted, a single blank space (' ') is specified by default.

The following table describes the result types.

**Result type of RTRIM**

<a id="800c917871b45b8f"></a>
| trim_source type, trim_character type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="79722bf87bf36e89"></a>
#### Example

```
gSQL> SELECT RTRIM( 'RTRIM_____', '_' ) AS RESULT FROM DUAL;
RESULT
------
RTRIM 
1 row selected.
```

<a id="9c2301781c5bc335"></a>
### SESSION_ID

<a id="b3aa096ee470c159"></a>
#### Syntax

```
SESSION_ID()
```

<a id="5ca862ef76bcbb40"></a>
#### Description

It obtains the current session ID.

<a id="e1b6bbdaf29f145a"></a>
#### Example

```
gSQL> SELECT SESSION_ID() FROM dual;

SESSION_ID()
------------
           4

1 row selected.
```

<a id="14c93071437db5a4"></a>
### SESSION_SERIAL

<a id="b951bf2ec2e110ec"></a>
#### Syntax

```
SESSION_SERIAL()
```

<a id="e902121b9f51b1cd"></a>
#### Description

It obtains the serial number of current session.

<a id="8d57abfa69b6874c"></a>
#### Example

```
gSQL> SELECT SESSION_SERIAL() FROM dual;

SESSION_SERIAL()
----------------
              16

1 row selected.
```

<a id="579803a5ccda992b"></a>
### SESSION_USER

<a id="32eb81fe9f15375a"></a>
#### Syntax

```
SESSION_USER[()]
```

<a id="df5b91255f0619cc"></a>
#### Description

It returns the session user.

The user information is managed in three types as follows.

- Logon user: It is a user who performed login, and it is maintained until the connection is closed.
- Session user: It is as same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user: It is generally as same as the session user, but it is temporarily changed internally in system to control access when using the PSM, View.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="c87c0cfb851a4fee"></a>
#### Example

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

<a id="ee8287d985a86340"></a>
### SHARD_GROUP_ID

<a id="463ded44de33cbd6"></a>
#### Syntax

```
SHARD_GROUP_ID( table_name, shard_key_value [, ... ] )
```

<a id="db4060b3372a07ce"></a>
#### Description

It returns the group ID managing the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is NATIVE_BIGINT.

> It is a valid information in a cluster system.

<a id="874c6966dfc80875"></a>
#### Example

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

<a id="a356610d2deb54a6"></a>
### SHARD_GROUP_NAME

<a id="78ee46843428b2a7"></a>
#### Syntax

```
SHARD_GROUP_NAME( table_name, shard_key_value [, ... ] )
```

<a id="29986810202c2f5e"></a>
#### Description

It returns the group NAME managing the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is VARCHAR.

> It is a valid information in a cluster system.

<a id="5e11177f9c273751"></a>
#### Example

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

<a id="b70d05f1aa8e26bf"></a>
### SHARD_ID

<a id="4a15b1719758d92e"></a>
#### Syntax

```
SHARD_ID( table_name, shard_key_value [, ... ] )
```

<a id="fdf7c7b1515e607d"></a>
#### Description

It returns the ID for the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is NATIVE_BIGINT.

> It is a valid information in a cluster system.

<a id="85d46516f24f5305"></a>
#### Example

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

<a id="9c2042d312fec9e1"></a>
### SHARD_NAME

<a id="506c0736337e6a09"></a>
#### Syntax

```
SHARD_NAME( table_name, shard_key_value [, ... ] )
```

<a id="ca67699694e2a86e"></a>
#### Description

It returns the NAME for the shard which stores shard_key_value when the shard strategy is defined in the table_name.

The table_name (an input argument) should be described by an identifier. If an object corresponding to the table_name is not a base table, or if the shard strategy is not defined, then an error occurs.

The shard_key_value (an input argument) should be listed in an order of shard key column in the shard strategy defined in the table_name. If the number of shard_key_value and the number of shard key columns is not same, then an error occurs.

The result type is VARCHAR.

> It is a valid information in a cluster system.

<a id="bb5a4a4411b42834"></a>
#### Example

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

<a id="f317fc13b9b3626a"></a>
### SHIFT_LEFT

<a id="e197884b97fd2aab"></a>
#### Syntax

```
SHIFT_LEFT( num, cnt )
```

<a id="58b4db79e80f0fe0"></a>
#### Description

It moves num to the left as many as cnt bits, and returns the movement values.

The data type of input num argument and cnt argument can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or the type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.

cnt is masked with 6 bit, and it is processed to a value in the range within 6 bit.

The result type is NATIVE_BIGINT.

<a id="da65d2bcf75892b1"></a>
#### Example

```
gSQL> SELECT SHIFT_LEFT( 7, 3 ) AS RESULT FROM DUAL;
RESULT
------
    56
1 row selected.
```

<a id="fb156c0b07fbf0ff"></a>
### SHIFT_RIGHT

<a id="6fe6608167710474"></a>
#### Syntax

```
SHIFT_RIGHT( num, cnt )
```

<a id="10a7274febd7b704"></a>
#### Description

It moves num to the right as many as cnt bits, and returns the movement values.

The data type of input num argument and cnt argument can be NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, or the type which can be converted to NATIVE_BIGINT.  
When converting to NATIVE_BIGINT type, the decimal point is truncated.

cnt is masked with 6 bit, and it is processed to a value in the range within 6 bit.

The result type is NATIVE_BIGINT.

<a id="6c0bd0fe1a05bec9"></a>
#### Example

```
gSQL> SELECT SHIFT_RIGHT( 56, 3 ) AS RESULT FROM DUAL;
RESULT
------
     7
1 row selected.
```

<a id="1d74ed5378a447eb"></a>
### SIGN

<a id="7557e7a8a9b413a5"></a>
#### Syntax

```
SIGN( num )
```

<a id="46764ff76d729eb0"></a>
#### Description

It returns the sign of num.

The num argument can be a numeric data type.

The return value is as follows.   
• If num < 0,  -1 is returned.  
• If num = 0, 0 is returned.  
• If num > 0, 1 is returned.

<a id="92c64f8d7ca01b5b"></a>
#### Example

```
gSQL> SELECT SIGN(-10) AS RESULT1, 
             SIGN(0) AS RESULT2, 
             SIGN(10) AS RESULT3 FROM DUAL;
RESULT1 RESULT2 RESULT3
------- ------- -------
     -1       0       1
1 row selected.
```

<a id="eb34d1ce3213abd7"></a>
### SIN

<a id="ca716f3ab01eae11"></a>
#### Syntax

```
SIN( num )
```

<a id="7d9aaff883dbf348"></a>
#### Description

It returns the sine value of num.

<a id="34fb889654373843"></a>
#### Example

```
gSQL> SELECT SIN( 0 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="4c4079406d453973"></a>
### SPLIT_PART

<a id="9986e04b526eac7f"></a>
#### Syntax

```
SPLIT_PART( string, delimiter, field )
```

<a id="8d1818d2e7b8c353"></a>
#### Description

It returns a character string of the field by specifying a character as delimiter within a string.

The data type of string argument and delimiter argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

The field argument can be a numeric data type.

If any of string, delimiter, field is NULL, the result is also NULL.  
The value of field should be a numeric value above 1, and if it is 0 or a negative number, an error is returned.

The following table describes the result types.

**Result type of SPLIT_PART**

<a id="8e88eb5277d80f88"></a>
| string type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="dbf06eab34f4b6dd"></a>
#### Example

```
gSQL> SELECT SPLIT_PART( 'AB;CD;EF;GH', ';', 3  ) AS RESULT FROM DUAL;
RESULT
------
EF    
1 row selected.
```

<a id="f79ee8c8f18aefb4"></a>
### SQRT

<a id="b027ed6bdb8f47e1"></a>
#### Syntax

```
SQRT( num )
```

<a id="a2bc8a26969a7b5d"></a>
#### Description

It returns the square root of num.

The num argument can be a numeric type, and it should not be a negative number, but above 0.

<a id="3fe1b8846e669136"></a>
#### Example

```
gSQL> SELECT SQRT( 9 ) AS RESULT FROM DUAL;
RESULT
------
     3
1 row selected.
```

<a id="d9cd0a5fed32919e"></a>
### STATEMENT_DATE

<a id="d71167ff86e377ca"></a>
#### Syntax

```
STATEMENT_DATE()
CURRENT_DATE [()]
```

<a id="f3aa268e0e80e8ce"></a>
#### Description

The current date(DATE type) value is obtained.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="8525099332b2bf67"></a>
#### Example

```
gSQL> SELECT STATEMENT_DATE() AS result FROM t1;

RESULT    
----------
2013-12-12
2013-12-12
2013-12-12

3 rows selected.
```

<a id="b4caddc36c85506a"></a>
### STATEMENT_LOCALTIME

<a id="8da87547037704ef"></a>
#### Syntax

```
STATEMENT_LOCALTIME()
LOCALTIME [()]
```

<a id="b3ea377b3e95cedf"></a>
#### Description

The current TIME WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.  
• TATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="945cd9c0cca19dca"></a>
#### Example

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

<a id="9b450c5721628b0d"></a>
### STATEMENT_LOCALTIMESTAMP

<a id="130ff8402a213100"></a>
#### Syntax

```
STATEMENT_LOCALTIMESTAMP()
LOCALTIMESTAMP [()]
```

<a id="3e303b1dce366ad1"></a>
#### Description

The current TIMESTAMP WITHOUT TIME ZONE type value based on the session time is obtained.

LOCALTIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_LOCALTIMESTAMP(): All timestamp values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="e6bd493aefb59361"></a>
#### Example

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

<a id="291da7b42a18babb"></a>
### STATEMENT_TIME

<a id="f750bd7c7619aee2"></a>
#### Syntax

```
STATEMENT_TIME()
CURRENT_TIME [()]
```

<a id="25986597f8ca5393"></a>
#### Description

The current TIME WITH TIME ZONE type value is obtained.

CURRENT_TIME is an SQL standard function.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• STATEMENT_TIME(): All time values in an SQL statement are same.  
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="f22472d24c3304ae"></a>
#### Example

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

<a id="c42ed707a9aac6d6"></a>
### STATEMENT_TIMESTAMP

<a id="2247e91e77d28680"></a>
#### Syntax

```
STATEMENT_TIMESTAMP()
CURRENT_TIMESTAMP [()]
```

<a id="78558bc374bb8cac"></a>
#### Description

The current TIMESTAMP WITH TIME ZONE type value is obtained.

CURRENT_TIMESTAMP is an SQL standard function.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_TIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_TIMESTAMP(): All timestamp values in an SQL statement are same.  
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="4c7cc60731f3d459"></a>
#### Example

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

<a id="19558d3073e868bb"></a>
### STATEMENT_VIEW_SCN

<a id="c5279e9f7af6e32a"></a>
#### Syntax

```
STATEMENT_VIEW_SCN()
```

<a id="4bf3bc430a6516e7"></a>
#### Description

It obtains VIEW SCN of the current STATEMENT.

<a id="2f18577a86ce30b0"></a>
#### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN() FROM dual;

STATEMENT_VIEW_SCN()
--------------------
17697.658.17880     

1 row selected.
```

<a id="94ba1a8e2e6ab153"></a>
### STATEMENT_VIEW_SCN_DCN

<a id="d65314cfc7709489"></a>
#### Syntax

```
STATEMENT_VIEW_SCN_DCN()
```

<a id="c0e7b299ca2a18c9"></a>
#### Description

It obtains the Domain Change Number (DCN) value of the current STATEMENT's VIEW SCN.

<a id="e3d333527eff1ddb"></a>
#### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_DCN() FROM dual;

STATEMENT_VIEW_SCN_DCN()
------------------------
                     658

1 row selected.
```

<a id="a0d053b00616f49c"></a>
### STATEMENT_VIEW_SCN_GCN

<a id="1b5017a3526d71fe"></a>
#### Syntax

```
STATEMENT_VIEW_SCN_GCN()
```

<a id="b75ea51b7d0ad85a"></a>
#### Description

It obtains the Global Change Number (GCN) value of the current STATEMENT's VIEW SCN.

<a id="9201a6dcd9546ba5"></a>
#### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_GCN() FROM dual;

STATEMENT_VIEW_SCN_GCN()
------------------------
                   17697

1 row selected.
```

<a id="4cda8610893b1db1"></a>
### STATEMENT_VIEW_SCN_LCN

<a id="5fc7fc5bf703a4ad"></a>
#### Syntax

```
STATEMENT_VIEW_SCN_LCN()
```

<a id="a28997e0818a614e"></a>
#### Description

It obtains the Local Change Number (LCN) value of the current STATEMENT's VIEW SCN.

<a id="555ccebf745a2a13"></a>
#### Example

```
gSQL> SELECT STATEMENT_VIEW_SCN_LCN() FROM dual;

STATEMENT_VIEW_SCN_LCN()
------------------------
                   17880

1 row selected.
```

<a id="aa121de14f05d3e8"></a>
### STDDEV

<a id="0c6aff50429cd2d8"></a>
#### Syntax

```
STDDEV( [ ALL | DISTINCT ] expr )
```

<a id="eb7b76afadf03b72"></a>
#### Description

It is an aggregation function, and it obtains the standard deviation of an expr set.

If ALL is specified, this function is performed for all values. If DISTINCT is specified, this function is performed for the values of which the duplicates were deleted from. If it is not specified, it is processed as if ALL is apecified.

If the number of expr sets except for NULL after deleting the duplicates by using DISTINCT is one, then it returns 0 like as [VARIANCE](#80ab44261e08c113).

The following table describes the arguments and result types.

**Argument and result type of STDDEV**

<a id="973756937e5cd61c"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

GOLDILOCKS gets the standard deviation as follows.  
　• If the number of expr sets is 1, then it returns 0.  
　• If the number of expr sets is bigger than 1, It returns the value of [STDDEV_SAMP( expr )](#3aed39af2add9685).

> The standard deviation is a positive square root of a variance, and it is obtained calculating the square root of the variance. In other words, the STDDEV function is as same as the square root of [VARIANCE](#80ab44261e08c113) function.  
>   
> STDDEV( [ ALL ] expr )  
>  = SQRT( VARIANCE( [ ALL ] expr ) )  
>   
> STDDEV( DISTINCT expr )  
>  = SQRT( VARIANCE( DISTINCT expr ) )

<a id="9e372a68b2d809a0"></a>
#### Example

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

<a id="70c13c621cbfb9c8"></a>
### STDDEV_POP

<a id="2f36637affc9e8ac"></a>
#### Syntax

```
STDDEV_POP( expr )
```

<a id="b0bee2850151d1a9"></a>
#### Description

It is an aggregation function, and it obtains the population standard deviation of an expr set. If the number of expr sets except for NULL is one, then it returns 0.

The following table describes the arguments and result types.

**Argument and result type of STDDEV_POP**

<a id="c6db60c8d7c5405c"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The population standard deviation is a positive square root of a population variance, and it is obtained by calculating the square root of the population variance. In other words, the STDDEV_POP function is as same as the square root of [VAR_POP](#a6f898169be957da) function.  
>   
> STDDEV_POP( expr )  
>  = SQRT( VAR_POP( expr ) )

<a id="a39b58a77a24b40b"></a>
#### Example

```
gSQL> SELECT STDDEV_POP(c1) FROM t1;

 STDDEV_POP(C1)
---------------
10.283968105746

1 row selected.
```

<a id="3aed39af2add9685"></a>
### STDDEV_SAMP

<a id="607ea2ec141ea8fa"></a>
#### Syntax

```
STDDEV_SAMP( expr )
```

<a id="683e3c296fd2c342"></a>
#### Description

It is an aggregation function, and it obtains the sample standard deviation of an expr set. If the number of expr sets except for NULL is one, then it returns NULL.

The following table describes the arguments and result types.

**Argument and result type of STDDEV_SAMP**

<a id="1cdf2c15cf7dc98e"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The sample standard deviation is a positive square root of a sample variance, and it is obtained by calculating the square root of the sample variance. In other words, the STDDEV_SAMP function is as same as the square root of [VAR_SAMP](#9881748ecbb23c59) function.  
>   
> STDDEV_SAMP( expr )  
>  = SQRT( VAR_SAMP( expr ) )

<a id="2fc1ef34347ec5be"></a>
#### Example

```
gSQL> SELECT STDDEV_SAMP(c1) FROM t1;

 STDDEV_SAMP(C1)
----------------
11.4978258814438

1 row selected.
```

<a id="e66f5efc914d611a"></a>
### SUBSTR

<a id="bbbbb4e7c3aa97b8"></a>
#### Syntax

```
SUBSTR( str FROM start_position [ FOR string_length ] )
SUBSTR( str, start_position [ , string_length ] )
```

<a id="e08f71d30871fc58"></a>
#### Description

It is an alias of [SUBSTRING](#e3575b3c7baae2bb).

<a id="ad8225e69225ae13"></a>
#### Example

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

<a id="e63cf2098b590fa6"></a>
### SUBSTRB

<a id="873ef590ec107cb4"></a>
#### Syntax

```
SUBSTRB( str, start_position [ , string_length ] )
```

<a id="c2285588b1c118ea"></a>
#### Description

It extracts characters which are within string_length range from start_position, and returns the result for str.

This function is as same as [SUBSTRING](#e3575b3c7baae2bb) function, except that start_position and string_length of the SUBSTR function are calculated in byte units.

<a id="f5c15c6dac601e6d"></a>
#### Example

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

<a id="e3575b3c7baae2bb"></a>
### SUBSTRING

<a id="66f903402ba45b2d"></a>
#### Syntax

```
SUBSTRING( str FROM start_position [ FOR string_length ] )  
SUBSTRING( str, start_position [ , string_length ] )
```

<a id="c8c700eb41202a76"></a>
#### Description

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

It is an alias of [SUBSTR](#e66f5efc914d611a).  
For more information, refer to [SUBSTRB](#e63cf2098b590fa6).

The following table describes the result types.

**Result type of SUBSTRING**

<a id="728f09ee246c27d8"></a>
| str type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="9acb0d1291a72691"></a>
#### Example

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

<a id="cc930e2799495e28"></a>
### SUM

<a id="ae30f3139eda8190"></a>
#### Syntax

```
SUM( [ ALL | DISTINCT ] expr )
```

<a id="bd8d03a988a04524"></a>
#### Description

It is an aggregate function and the sum of expr value is obtained.

If ALL is explicitly specified, aggregation is executed for all values.  
If DISTINCT is explicitly specified, aggregation is executed for the values which exclude duplicate values.  
If ALL or DISTINCT is not explicitly specified, it is processed in the same way as when ALL is specified.

<a id="342e7a029fb73d70"></a>
#### Example

```
gSQL> SELECT SUM(c1) FROM t1;

SUM(C1)
-------
      6

1 row selected.
```

<a id="f5814f4ef90c26ab"></a>
### SYSDATE

<a id="d1e5fe8dc07d2dbe"></a>
#### Syntax

```
SYSDATE
```

<a id="cdee5e9fdcbd8baf"></a>
#### Description

It obtains the current DATE type value based on the OS time of the database server.

<a id="8dc59daf20b62dd2"></a>
#### Example

```
gSQL> SELECT SYSDATE FROM t1;

SYSDATE   
----------
2013-12-12
2013-12-12
2013-12-12

3 rows selected.
```

<a id="429e0b7c3e339fbc"></a>
### SYS_EXTRACT_UTC

<a id="3f95ecc34557102e"></a>
#### Syntax

```
SYS_EXTRACT_UTC( datetime_with_timezone )
```

<a id="b54b941688329691"></a>
#### Description

It returns the UTC (Coordinated Universal Time—formerly Greenwich Mean Time) value.  
If the timezone is not specified, it is calculated as session time zone.

The data type of an input argument can be time, time with time zone, timestamp, timestamp with time zone.  
The result type is time or timestamp type.

<a id="536620d87bbe84ab"></a>
#### Example

```
gSQL> SELECT 
      SYS_EXTRACT_UTC( 
          TO_TIMESTAMP_TZ( '2017-05-25 21:13:32.123456 +09:00',
                           'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM') 
          ) AS RESULT 
      FROM DUAL;
RESULT                    
--------------------------
2017-05-25 12:13:32.123456
1 row selected.
```

<a id="7a4172f8ee6040b9"></a>
### SYSTIME

<a id="f8e7fca4198ce8f1"></a>
#### Syntax

```
SYSTIME
```

<a id="0877b9ac2e663182"></a>
#### Description

It obtains the current TIME WITH TIME ZONE type value based on the OS time of the database server.

<a id="84fdc7f0c73982f1"></a>
#### Example

```
gSQL> SELECT SYSTIME FROM t1;

SYSTIME               
----------------------
16:30:46.954941 +09:00
16:30:46.954941 +09:00
16:30:46.954941 +09:00

3 rows selected.
```

<a id="11c7ec435aff8644"></a>
### SYSTIMESTAMP

<a id="19abf3babd54e7f4"></a>
#### Syntax

```
SYSTIMESTAMP
```

<a id="2185b9e3860b083f"></a>
#### Description

It obtains the current TIMESTAMP WITH TIME ZONE type value based on the OS time of the database server.

<a id="7c99bcdc97599b2d"></a>
#### Example

```
gSQL> SELECT SYSTIMESTAMP FROM t1;

SYSTIMESTAMP                     
---------------------------------
2013-12-12 16:37:34.432241 +09:00
2013-12-12 16:37:34.432241 +09:00
2013-12-12 16:37:34.432241 +09:00

3 rows selected.
```

<a id="d5f6f1c95a4ff85b"></a>
### TAN

<a id="efc3800841087653"></a>
#### Syntax

```
TAN( num )
```

<a id="d30a07db244c3012"></a>
#### Description

It returns the tangent value of num in radians unit.

<a id="224233ed2d20d528"></a>
#### Example

```
gSQL> SELECT TAN( 1 ) AS RESULT FROM DUAL;
         RESULT
---------------
1.5574077246549
1 row selected.
```

<a id="5ae9c294a6c57303"></a>
### TO_BASE64

<a id="c926235bc2bae285"></a>
#### Syntax

```
TO_BASE64( str )
```

<a id="6041769b0c0355b8"></a>
#### Description

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

For more information, refer to [FROM_BASE64](#f99ff94c769c793e).

<a id="fbb5ec2bc12ce84b"></a>
#### Example

```
gSQL> SELECT TO_BASE64( 'abc' ), TO_BASE64( 'abcd' ) FROM DUAL;

TO_BASE64( 'abc' ) TO_BASE64( 'abcd' )
------------------ -------------------
YWJj               YWJjZA==           
1 row selected.
```

<a id="9688fd0405cae768"></a>
### TO_CHAR( datetime )

<a id="03aeae8a8b836b1e"></a>
#### Syntax

```
TO_CHAR( datetime [, fmt ] )
```

<a id="b8a8922d3706fb87"></a>
#### Description

It converts datetime to a string in the specified fmt format, and returns the result.

The datetime argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL.   
The fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING.

If fmt is omitted, it follows the default format.  
• DATE: Refer to [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#6c5301741d86446c).  
• TIMESTAMP: Refer to [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#f04f20ba0ffa3caf).  
• TIMESTAMP WITH TIME ZONE: Refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#edba3110d229ce95).  
• TIME: Refer to [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#3eb7e8d0be6c45dd).  
• TIME WITH TIME ZONE: Refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#dc93f1addc88cbde).

If the data type of the datetime argument is INTERVAL, it is converted to a string then returned regardless of fmt.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](#f23ffe951177a789).

The result type is CHARACTER VARYING.

<a id="4fa1726a116cb636"></a>
#### Example

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

<a id="949621fdd02e5356"></a>
### TO_CHAR( number )

<a id="89f2585b1b265db2"></a>
#### Syntax

```
TO_CHAR( number [, fmt ] )
```

<a id="f1e8d4a180a7f0db"></a>
#### Description

It converts the number to a string in the specified fmt format, and returns the result.

The number argument can be a numeric data type.  
The fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING.  
If fmt is omitted, all significant digits are converted to the string and returned.  
For more information about the string which can be specified in fmt, refer to [Number Format String](#d1928fe9c7363ae1).

The result type is CHARACTER VARYING.

<a id="705455a2bb8f8272"></a>
#### Example

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

<a id="25eb6843029ae86c"></a>
### TO_DATE

<a id="ada357c2624d78ab"></a>
#### Syntax

```
TO_DATE( str [, fmt ] )
```

<a id="9fedb768a589c47c"></a>
#### Description

It converts the str string in the specified fmt format to DATE type, and returns the result.

The str argument and fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.  
If fmt is omitted, the default format is NLS_DATE_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](#f23ffe951177a789).  
For more information, refer to [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#6c5301741d86446c).

The result type is DATE.

<a id="f068e8fc886cb9ed"></a>
#### Example

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

<a id="d03ab835f5df2038"></a>
### TO_NATIVE_DOUBLE

<a id="9d73af632d32ca81"></a>
#### Syntax

```
TO_NATIVE_DOUBLE( str [, fmt ] )
```

<a id="665445843d38a06b"></a>
#### Description

It converts the str string in the specified fmt format to NATIVE_DOUBLE type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](#d1928fe9c7363ae1).

The result type is NATIVE_DOUBLE.

<a id="f30c4553e13be4eb"></a>
#### Example

```
gSQL> SELECT TO_NATIVE_DOUBLE( '123.45' ) AS RESULT1, 
             TO_NATIVE_DOUBLE( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
1 row selected.
```

<a id="0cf01e33445e03e5"></a>
### TO_NATIVE_REAL

<a id="82813ef6fb5a7457"></a>
#### Syntax

```
TO_NATIVE_REAL( str [, fmt ] )
```

<a id="865c500ce6d07bd0"></a>
#### Description

It converts the str string in the specified fmt format to NATIVE_REAL type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](#d1928fe9c7363ae1).

The result type is NATIVE_REAL.

<a id="63b410e7c1838edb"></a>
#### Example

```
gSQL> SELECT TO_NATIVE_REAL( '123.45' ) AS RESULT1, 
             TO_NATIVE_REAL( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
```

<a id="491715806db53986"></a>
### TO_NUMBER

<a id="ff0917a910a8f520"></a>
#### Syntax

```
TO_NUMBER( str [, fmt] )
```

<a id="7ac21a650f6e16b1"></a>
#### Description

It converts the str string in the specified fmt format to NUMBER type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of str, fmt is NULL, the result is also NULL.  
For more information about the string which can be specified in fmt, refer to [Number Format String](#d1928fe9c7363ae1).

The result type is NUMBER.

<a id="595279ac8efd9952"></a>
#### Example

```
gSQL> SELECT TO_NUMBER( '123.45' ) AS RESULT1, 
             TO_NUMBER( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
1 row selected.
```

<a id="d9a48ce329494e11"></a>
### TO_TIME

<a id="a7da8580228b6933"></a>
#### Syntax

```
TO_TIME( str [, fmt ] )
```

<a id="f8cc69501eb6c81a"></a>
#### Description

It converts the str string in the specified fmt format to TIME type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIME_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](#f23ffe951177a789).  
For more information, refer to [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#3eb7e8d0be6c45dd).

The result type is TIME.

<a id="da8525ad6637f688"></a>
#### Example

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

<a id="4de565a0a89e0975"></a>
### TO_TIME_TZ

<a id="4ceb36ca27f43628"></a>
#### Syntax

```
TO_TIME_TZ( str [, fmt ] )
```

<a id="501b22622176e8d5"></a>
#### Description

It is an alias of [TO_TIME_WITH_TIME_ZONE](#766da9ffc336d7e2).  
For more information, refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#dc93f1addc88cbde).

<a id="488c544797991f6a"></a>
#### Example

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

<a id="766da9ffc336d7e2"></a>
### TO_TIME_WITH_TIME_ZONE

<a id="48e526674e88e9d6"></a>
#### Syntax

```
TO_TIME_WITH_TIME_ZONE( str [, fmt ] )
TO_TIME_TZ( str [, fmt ] )
```

<a id="071c00caab16a224"></a>
#### Description

It converts the str string in the specified fmt format to TIME WITH TIME ZONE type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIME_WITH_TIME_ZONE_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](#f23ffe951177a789)  
For more information, refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#dc93f1addc88cbde).

It is an alias of [TO_TIME_TZ](#4de565a0a89e0975).

The result type is TIME WITH TIME ZONE.

<a id="68e8315378cf3100"></a>
#### Example

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

<a id="3e1f1636fafd674a"></a>
### TO_TIMESTAMP

<a id="71acfa4b980bb01d"></a>
#### Syntax

```
TO_TIMESTAMP( str [, fmt ] )
```

<a id="b571410ba37d0b30"></a>
#### Description

It converts the str string in the specified fmt format to TIMESTAMP type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIMESTAMP_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to [Datetime Format String](#f23ffe951177a789).  
For more information, refer to [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#f04f20ba0ffa3caf).

The result type is TIMESTAMP.

<a id="a3a04d3fde632157"></a>
#### Example

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

<a id="d2eebad23d9c35e9"></a>
### TO_TIMESTAMP_TZ

<a id="06d9e305ce86ab79"></a>
#### Syntax

```
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="21be85bf3292e3fb"></a>
#### Description

It is an alias of [TO_TIMESTAMP_WITH_TIME_ZONE](#77a90650f33e49f9).  
For more information, refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#edba3110d229ce95).

<a id="835be175fa608663"></a>
#### Example

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

<a id="77a90650f33e49f9"></a>
### TO_TIMESTAMP_WITH_TIME_ZONE

<a id="8614498416abf4fa"></a>
#### Syntax

```
TO_TIMESTAMP_WITH_TIME_ZONE( str [, fmt ] )
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="e7e7bfeb99fac70c"></a>
#### Description

It converts the str string in the specified fmt format to TIMESTAMP WITH TIME ZONE type, and returns the result.

The data type of str argument and fmt argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.   
If fmt is omitted, the default format is NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT, and in this case str should be the default format string.

For more information about the string which can be specified in fmt, refer to  [Datetime Format String](#f23ffe951177a789).  
For more information, refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#edba3110d229ce95).

It is an alias of [TO_TIMESTAMP_TZ](#d2eebad23d9c35e9).

The result type is TIMESTAMP WITH TIME ZONE .

<a id="0d1029e46e7be7e0"></a>
#### Example

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

<a id="c14c9f18d38d6e78"></a>
### TRANSACTION_DATE

<a id="a07765f90669fe40"></a>
#### Syntax

```
TRANSACTION_DATE()
```

<a id="ca523742f74539b0"></a>
#### Description

It obtains the current date (DATE type) value based on the session time.

The differences among the functions to obtain the current date are as follows.  

• TRANSACTION_DATE(): All date values in the transaction are same.  
• STATEMENT_DATE(): All date values in an SQL statement are same.  
• CLOCK_DATE(): Whenever the function is called, the current date value is obtained.

<a id="6ad9fa0040b2ab62"></a>
#### Example

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

<a id="df6720b7efb5e738"></a>
### TRANSACTION_LOCALTIME

<a id="50325c6a2c1bcd29"></a>
#### Syntax

```
TRANSACTION_LOCALTIME()
```

<a id="8cc9358a2a99a3fa"></a>
#### Description

It obtains the current TIME WITHOUT TIME ZONE type value based on the session time.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_LOCALTIME(): All time values in the transaction are same.   
• STATEMENT_LOCALTIME(): All time values in an SQL statement are same.  
• CLOCK_LOCALTIME(): Whenever the function is called, the current time value is obtained.

<a id="5caebe4b322a23fb"></a>
#### Example

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

<a id="fa3d9ac50d6f8ab7"></a>
### TRANSACTION_LOCALTIMESTAMP

<a id="e406e601b72625e3"></a>
#### Syntax

```
TRANSACTION_LOCALTIMESTAMP()
```

<a id="4cc1ca4da7a92b6f"></a>
#### Description

It obtains the current TIMESTAMP WITHOUT TIME ZONE type value based on the session time.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_LOCALTIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_LOCALTIMESTAMP(): All timestamp values in an SQL statement are same.  
• CLOCK_LOCALTIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="b1b41cbf9f747f3c"></a>
#### Example

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

<a id="751918936eb9a572"></a>
### TRANSACTION_TIME

<a id="015e20e57f974093"></a>
#### Syntax

```
TRANSACTION_TIME()
```

<a id="99d7ca4a590eaf97"></a>
#### Description

It obtains the current TIME WITH TIME ZONE type value based on the session time.

The differences among the functions to obtain the current time are as follows.  

• TRANSACTION_TIME(): All time values in the transaction are same.  
• STATEMENT_TIME(): All time values in an SQL statement are same.   
• CLOCK_TIME(): Whenever the function is called, the current time value is obtained.

<a id="6fb5f9234b469516"></a>
#### Example

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

<a id="85779505c3ed1d67"></a>
### TRANSACTION_TIMESTAMP

<a id="571a20c81a811896"></a>
#### Syntax

```
TRANSACTION_TIMESTAMP()
```

<a id="3c7c5b0ec55bf3a9"></a>
#### Description

It obtains the current TIMESTAMP WITH TIME ZONE type value based on the session time.

The differences among the functions to obtain the current timestamp are as follows.  

• TRANSACTION_TIMESTAMP(): All timestamp values in the transaction are same.  
• STATEMENT_TIMESTAMP(): All timestamp values in an SQL statement are same.   
• CLOCK_TIMESTAMP(): Whenever the function is called, the current timestamp value is obtained.

<a id="5157485051a903dd"></a>
#### Example

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

<a id="2f553624d615ebb3"></a>
### TRANSLATE

<a id="c2f6bf06f3ad3bb2"></a>
#### Syntax

```
TRANSLATE( string, from, to )
```

<a id="37064878987c4959"></a>
#### Description

It converts all characters which are same as the characters in *from* to its corresponding characters in *to*. Then it returns the result.

The data type of the string argument, the from argument, and the to argument can be a data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.

If any of *string, from, to* is NULL, the result is also NULL.

Characters in string which are not same as characters in *from*, are not replaced.  
Characters in string which are same as characters in *from*, are replaced to its corresponding characters in *to*.  
If the number of characters in *from* is bigger than the number of characters in *to*, the characters in *from* which does not correspond to the characters in *to*, are removed, and returned.  
If the same characters are repeated multiple times in *from*, they are replaced with the first mapped character.

The following table describes the result types.

**Result type of TRANSLATE**

<a id="b2d149842adca85e"></a>
| string type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="010ad9d820ed0933"></a>
#### Example

```
gSQL> SELECT TRANSLATE( '12345', '15', 'FL'  ) AS RESULT FROM DUAL;
RESULT
------
F234L 
1 row selected.

gSQL> SELECT TRANSLATE( 'ABC12345', 'ABC12345', 'XYZ' ) AS RESULT FROM DUAL;
RESULT
------
XYZ   
1 row selected.

gSQL> SELECT TRANSLATE( 'ABC12345ABC', 'ABCABCABC', 'XYZ^&*xyz' ) AS RESULT 
      FROM DUAL;
RESULT     
-----------
XYZ12345XYZ
1 row selected.
```

<a id="6d310074cd59564e"></a>
### TRIM

<a id="43a33647e2531101"></a>
#### Syntax

```
TRIM([ [ LEADING | TRAILING | BOTH ]  [trim_character] FROM ] trim_source)
```

<a id="ba75e6e7dcb6b068"></a>
#### Description

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

<a id="04ab7a5aec22dc3b"></a>
| trim_character, trim_source type | Result type |
| --- | --- |
| CHAR or VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY or VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="b7e58906cc1de418"></a>
#### Example

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

<a id="b8bf6dce147c4d4d"></a>
### TRUNC( number )

<a id="556c48b5e7a6a3bb"></a>
#### Syntax

```
TRUNC( num [ , scale ] )
```

<a id="ae97948c31018b12"></a>
#### Description

It truncates the num based on scale, then returns the result.

The num argument and scale argument can be a numeric type.

If scale is omitted, the scale becomes 0, and it is executed as same as TRUNC( num, 0 ).  
If scale is a positive number, it is truncated based on the number of right digit of the decimal point.  
If scale is a negative number, it is truncated off based on the number of left digit of the decimal point.

<a id="3ba35f0de597c4d5"></a>
#### Example

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

<a id="5263975713629961"></a>
### TRUNC( date )

<a id="948e3407379a5242"></a>
#### Syntax

```
TRUNC( date [ , fmt ] )
```

<a id="a6cb99e54c2a1a08"></a>
#### Description

It truncates the date in a specified fmt unit, and returns the result.

The date argument data type can be DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.  
The fmt argument data type can be a character data type such as CHARACTER, CHARACTER VARYING.

The result type is always DATE regardless of the input date type.

If fmt is omitted, the default is *DAY*, and the available format string is described in the following table.

**Available format string in fmt**

<a id="5852b71e2a4ef005"></a>
| Format string | Description |
| --- | --- |
| CC, SCC | Century |
| YYYY, YEAR, SYYYY, SYEAR, YYY, YY, Y | Year |
| IYYY, IYY, IY, I | The year embracing the calendar week defined by ISO 8601 standards |
| Q | Quarter |
| MONTH, MON, MM, RM | Month |
| WW | The week whose first week starts from January 1st of the year |
| IW | The week containing the first thursday of the year designated as the calendar week by ISO 8601 standards (1 ~ 52 weeks or 1 ~ 53 weeks) becomes the first week. |
| W | The week whose first week starts from the first day of the month |
| DDD, DD, J | Day |
| DAY, DY, D | Day of the week |
| HH, HH12, HH24 | Hour |
| MI | Minute |

<a id="c9f2908a2cdf0934"></a>
#### Example

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

<a id="493003178bffe899"></a>
### UPPER

<a id="2375ac570a1be9ef"></a>
#### Syntax

```
UPPER( str )
```

<a id="24d2cc1fec770568"></a>
#### Description

It returns the uppercase characters of str.

The str argument can be a character data type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING.  
If str is NULL, the result is NULL.

The return type is as same as the str argument type.

<a id="8ea50788bbdfaad7"></a>
#### Example

```
gSQL> SELECT UPPER( 'spring' ) AS RESULT FROM DUAL;
RESULT
------
SPRING
1 row selected.
```

<a id="074ed8a093c71249"></a>
### UNHEX

<a id="45b25ff0bdedcf07"></a>
#### Syntax

```
UNHEX( str )
```

<a id="6713a366903686d1"></a>
#### Description

str argument is a hexadecimal character and this function represents it as each byte and returns it as a binary string.

The input argument can be a character type such as CHARACTER VARYING, CHARACTER LONG VARYING. The result type is a binary character type such as BINARY VARYING or BINARY LONG VARYING.

If str is NULL, then the result value is also NULL.  
If str includes a character which does not belong to the hexadecimal range, then it returns an error.

For more information, refer to [HEX](#8037fe9dcc2be3fc).

<a id="1d14cca76bac53e6"></a>
#### Example

```
gSQL> SELECT UNHEX( HEX( 'abc' ) ) FROM DUAL;
UNHEX( HEX( 'abc' ) )
---------------------
616263               
1 row selected.
```

<a id="442e98a48f5b0278"></a>
### UNHEX_TO_CHARSTR

<a id="88b5f8af3b665821"></a>
#### Syntax

```
UNHEX_TO_CHARSTR( str )
```

<a id="64cc92a98e466192"></a>
#### Description

str argument is a hexadecimal character and this function represents it as each byte and returns it as a character string.

The input argument can be a character type such as CHARACTER VARYING, CHARACTER LONG VARYING. The result type is a character type such as CHARACTER VARYING, CHARACTER LONG VARYING.

If str is NULL, then the result value is also NULL.  
If str includes a character which does not belong to the hexadecimal range, then it returns an error.

When returning it as a character string, it applies the currently applicable character set and returns the result value because the str argument is a hexadecimal character of an unknown data.  
If it is not included in the currently applicable character set, then it returns an error.

For more information, refer to [HEX](#8037fe9dcc2be3fc), [UNHEX](#074ed8a093c71249).

<a id="ddfba5eaae8b43ef"></a>
#### Example

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

<a id="b9f46eb5de8d0551"></a>
### USER_ID

<a id="2753d13905b20d24"></a>
#### Syntax

```
USER_ID ()
```

<a id="79727980043e9b33"></a>
#### Description

It obtains the current user's number ID.

> In cluster system, the value may vary depending on the connected server.  
> It is recommended to use [CURRENT_USER](#3439ccb21bfded13) function obtaining the current username.

<a id="fb35b1ae09d5506d"></a>
#### Example

```
% gsql test test

gSQL> SELECT USER_ID() FROM dual;

USER_ID()
---------
        6

1 row selected.
```

<a id="5fbd77aa4d267ad2"></a>
### UUID

<a id="419441f0728b6c76"></a>
#### Syntax

```
UUID()
```

<a id="ffe973b83cbe848a"></a>
#### Description

It creates the universal unique identifier, then returns it.   
The return type is VARBINARY type, and it internally consists of 16 bytes.

<a id="a84fac09a4074eb4"></a>
#### Example

```
gSQL> SELECT HEX( UUID() ) FROM DUAL;
HEX( UUID() )                   
--------------------------------
E6F0A5C2387511E8B95259E479C2FD50
1 row selected.
```

<a id="a6f898169be957da"></a>
### VAR_POP

<a id="601c8c9aa4168428"></a>
#### Syntax

```
VAR_POP( expr )
```

<a id="887d1bb6af153ce5"></a>
#### Description

It is an aggregation function, and it obtains the population variance of an expr set. If the number of expr sets except for NULL is one, then it returns 0.

The following table describes the arguments and result types.

**Argument and result type of VAR_POP**

<a id="c9b94984a8aa3f76"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> The population variance is a variance of the population (entire) group, and it is the average of the square value of deviation. In other words, it is calculated by extracting the population average (the entire average) from each value of the data, and squaring each value, then adding them together and dividing them by the number of datas in the population group.   
> This value is used to figure out how far each value is from the average value.

For more information, refer to [STDDEV_POP](#70c13c621cbfb9c8).

<a id="6745eb12731b0c65"></a>
#### Example

```
gSQL> SELECT VAR_POP(c1) FROM t1;

VAR_POP(C1)
-----------
     105.76

1 row selected.
```

<a id="9881748ecbb23c59"></a>
### VAR_SAMP

<a id="45c07568a2863b4a"></a>
#### Syntax

```
VAR_SAMP( expr )
```

<a id="40ab28e4454abff3"></a>
#### Description

It is an aggregation function, and it obtains the sample variance of an expr set. If the number of expr sets except for NULL is one, then it returns NULL.

The following table describes the arguments and result types.

**Argument and result type of VAR_SAMP**

<a id="fc7c32bc699c7079"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> Unlike the population variance dealing with the population (entire) group, the sample variance deals with the average and deviation of extracted samples. In other words, it is calculated by extracting the sample average from each value of the data, and squaring each value, then adding them together and dividing them by the number of datas in the population group minus 1.   
> This value is used to figure out the variance of the population group.

For more information, refer to [STDDEV_SAMP](#3aed39af2add9685).

<a id="046ea48d39c4b478"></a>
#### Example

```
gSQL> SELECT VAR_SAMP(c1) FROM t1;

VAR_SAMP(C1)
------------
       132.2

1 row selected.
```

<a id="80ab44261e08c113"></a>
### VARIANCE

<a id="52ef16212ebc769b"></a>
#### Syntax

```
VARIANCE( [ ALL | DISTINCT ] expr )
```

<a id="162d403a55bdd42a"></a>
#### Description

It is an aggregation function, and it obtains the variance of an expr set.

If ALL is specified, this function is performed for all values. If DISTINCT is specified, this function is performed for the values of which the duplicates were deleted from. If it is not specified, it is processed as if ALL is apecified.

If the number of expr sets except for NULL after deleting the duplicates by using DISTINCT is one, then it returns 0.

The following table describes the arguments and result types.

**Argument and result type of VARIANCE**

<a id="3a3f2330681a574a"></a>
| expr | Result type |
| --- | --- |
| NATIVE_INTEGER family * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE family * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> GOLDILOCKS gets the variance as follows.  
> • If the number of expr sets is 1, then it returns 0.  
> • If the number of expr sets is bigger than 1, It returns the value of [STDDEV_SAMP (expr)](#3aed39af2add9685).

For more information, refer to [STDDEV](#aa121de14f05d3e8).

<a id="6b63dc887ec5aed8"></a>
#### Example

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

<a id="0b9ef75fafd757f8"></a>
### VERSION

<a id="4874170b2f5ae00b"></a>
#### Syntax

```
VERSION()
```

<a id="3270f3d0de75b00d"></a>
#### Description

It obtains the product's version string.

<a id="38d76f262474bdc7"></a>
#### Example

```
gSQL> SELECT VERSION() FROM dual;

VERSION()                            
-------------------------------------
Release Name.X.X.X revision(XXXXX)

1 row selected.
```

<a id="4bdb442901525b95"></a>
### WIDTH_BUCKET

<a id="38813957921fcdff"></a>
#### Syntax

```
WIDTH_BUCKET( num, min, max, cnt )
```

<a id="d01d23e5ef3e7694"></a>
#### Description

It creates a section of the same width as cnt within a range between specified min and max, and it returns the section location in which the num is located.

The data type of num argument, min argument, max argument and cnt argument can be a numeric data type.

min, max means the range for the section. If the min value is equal to the max value, an error is returned.  
cnt means the number of sections. The cnt value should be a positive number. If the cnt value is 0 or a negative number, an error is returned.   
The section's location is numbered from one.

If any of num, min, max, cnt is NULL, the result is also NULL.

<a id="b562b769d2d68262"></a>
#### Example

```
gSQL> SELECT WIDTH_BUCKET( 5, 1, 20, 5 ) AS RESULT FROM DUAL;
RESULT
------
     2
1 row selected.
```

---

[← 10. Server Property](../part-02-administration-manual/10-server-property.md) · [Table of contents](../README.md) · [12. SQL Languages →](12-sql-languages.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
