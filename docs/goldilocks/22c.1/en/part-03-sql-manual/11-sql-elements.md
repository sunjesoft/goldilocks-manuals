<a id="8aa8d470d0f8bf77"></a>

# 11. SQL Elements

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/8aa8d470d0f8bf77)  
> Tag: `22c.1_10_tag`

[← 10. Server Property](../part-02-administration-manual/10-server-property.md) · [Table of contents](../README.md) · [12. SQL Languages →](12-sql-languages.md)

<a id="2b3631537851d91e"></a>
## Syntax Elements

<a id="ceb44fbf00a35273"></a>
### Identifiers

Identifier is divided into an ordinary identifier and a delimited identifier.  
An ordinary identifier consists of letters or a combination of letters and numbers, and it is used by internally substituting all characters to uppercase letters. Therefore, an ordinary identifier is not case-sensitive.

The following is an example of an ordinary identifier.

```
GOLDILOCKS
GoldiLocks
```

A delimited identifier consists of letters or a combination of letters and numbers enclosed in double quotes ("). All the characters are used literally as internally described. Therefore, a delimited identifier is case-sensitive.

The following is an example of a delimited identifier.

```
"GOLDILOCKS"
"GoldiLocks"
```

<a id="8b9df43f351a1f27"></a>
### Literals

Literals mean representation of non-null value.

<a id="40c8857c0b4da7e2"></a>
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

<a id="e35d263da02c6458"></a>
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

<a id="f524b98080716185"></a>
#### Datetime Literals

Datetime literals are representation of date/time type.   
Datetime value is specified using string literal, or by converting character or numeric value to datetime value using TO_*function (TO_DATE, etc).

Datetime data types are DATE, TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE.

<a id="b0587faae87d76d3"></a>
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

For more information, refer to [TO_DATE](17-built-in-function-references.md#5219142a4793653b), [Datetime Format String](#b7a47f2ef79b2b26), [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#7ea8c558693ab9b8).

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

<a id="43ea460ce8516097"></a>
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

For more information, refer to [TO_TIME](17-built-in-function-references.md#9dbf37dc5504a5f2), [Datetime Format String](#b7a47f2ef79b2b26), [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#fff3ca3eeeea7a35).

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

<a id="a5ec0ff246fabe14"></a>
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

For more information, refer to [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#a7774652486ae49f), [Datetime Format String](#b7a47f2ef79b2b26), [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#6a87f7e07e80669e).

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

<a id="2ea699144d21921e"></a>
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

For more information, refer to [TO_TIMESTAMP](17-built-in-function-references.md#4343ab929dac120a), [Datetime Format String](#b7a47f2ef79b2b26), [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#f745ba729e1e8deb).

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

<a id="f917d4c9493483f4"></a>
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

For more information, refer to [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#19ac77096078990f), [Datetime Format String](#b7a47f2ef79b2b26) , [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#226a187670420c2f).

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

<a id="63d668408fea8219"></a>
#### Interval Literals

The interval literals specify the time interval.

Intervals are classified and expressed as follows.

- Year-month INTERVAL values
    - It includes YEAR and MONTH.
    - Display string expression: 'year-month'
    - It can be written in a form as *INTERVAL 'string literal' YEAR[leading precision] TO MONTH* or *NUMTOYMINTERVAL( num, interval_indicator )*
- Day-time INTERVAL values
    - It includes DAY, HOUR, MINUTE, SECOND (fractional seconds).
    - Display string expression: 'day hour:minute:second.fractional_seconds'
    - It can be written in a form as *INTERVAL 'string literal' DAY[leading precision] TO SECOND[fractiona l seconds precision]* or *NUMTODSINTERVAL( num, interval_indicator )*.
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
• It is the digit number of the field, it can be specified from 2 to 6. If it is not specified, the default   
&nbsp;&nbsp;value is set to 2.  
• If the leading field value exceeds the leading precision, then an error is returned.

Fractional seconds precision  
• It is the digit number of fractional seconds, and it can be specified from 0 to 6. If it is not specified,  
&nbsp;the default value is set to 6.  
• If the fractional second field value exceeds the fractional seconds precision, then it is rounded off.

For more information, refer to [INTERVAL](16-built-in-data-type-references.md#22fc0092f6f0fd6f), [Precisions and value range of the second or later field in INTERVAL * TO * ](16-built-in-data-type-references.md#36ef5919e77b6362), [NUMTODSINTERVAL](17-built-in-function-references.md#310abb57145bd678), [NUMTOYMINTERVAL](17-built-in-function-references.md#d608b1cd886ee7b6).

<a id="f2a3b01402233412"></a>
#### Examples of Using Interval Literals.

The followings are examples of using interval literals.

<a id="c0dfd35e50471296"></a>
##### Interval YEAR

The followings are examples of using interval YEAR literals.

**Interval YEAR literals.**

<a id="a8fce086162ef7b8"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'YEAR INTERVAL'01-00'YEAR | 1 year | +01-00 |
| INTERVAL'100'YEAR | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100'YEAR(3) | 100 year | +100-00 |
| INTERVAL'+999999'YEAR(6) | 999999 year | +999999-00 |
| INTERVAL'-999999'YEAR(6) | -(999999 year) | -999999-00 |

<a id="6582ee0db82f7e44"></a>
##### Interval MONTH

The followings are examples of using interval MONTH literals.

<a id="bc01af2cdbbc2394"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'MONTH INTERVAL'00-01'MONTH | 1 month | +00-01 |
| INTERVAL'100'MONTH | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100'MONTH(3) | 8 year 4 month | +008-04 |
| INTERVAL'+999999'MONTH(6) | 83333 year 3 month | +083333-03 |
| INTERVAL'-999999'MONTH(6) | -(83333 year 3 month) | -083333-03 |

<a id="9c799340a6d6b890"></a>
##### Interval YEAR TO MONTH

The followings are examples of using interval YEAR TO MONTH literals.

<a id="34cf09fe71712da7"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1-06'YEAR TO MONTH | 1 year 6 month | +01-06 |
| INTERVAL'1-12'YEAR TO MONTH | The month value exceeded 11, so it returns the error. | - |
| INTERVAL'100-11'YEAR TO MONTH | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100-11'YEAR(3) TO MONTH | 100 year 11 month | +100-11 |
| INTERVAL'+999999-11'YEAR(6) TO MONTH | 999999 year 11 month | +999999-11 |
| INTERVAL'-999999-11'YEAR(6) TO MONTH | -(999999 year 11 month) | -999999-11 |

<a id="e45e351881f26250"></a>
##### Interval DAY

The followings are examples of using interval DAY literals.

<a id="8ed54a4a3f863aa8"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'DAY INTERVAL'01 00:00:00'DAY | 1 day | +01 00:00:00 |
| INTERVAL'100'DAY | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100'DAY(3) | 100 day | +100 00:00:00 |
| INTERVAL'+999999'DAY(6) | 999999 day | +999999 00:00:00 |
| INTERVAL'-999999'DAY(6) | -(999999 day) | -999999 00:00:00 |

<a id="8a5bf2c70f4d1e5e"></a>
##### Interval HOUR

The followings are examples of using interval HOUR literals.

<a id="81a848958a69b988"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'HOUR INTERVAL'00 01:00:00'HOUR | 1 hour | +00 01:00:00 |
| INTERVAL'1000'HOUR(3) | It exceeds the leading precision 3, so it returns the error | - |
| INTERVAL'1000'HOUR(4) | 41 day 16 hour | +0041 16:00:00 |
| INTERVAL'+999999'HOUR(6) | 41666 day 15 hour | +041666 15:00:00 |
| INTERVAL'-999999'HOUR(6) | -(41666 day 15 hour) | -041666 15:00:00 |

<a id="17611436f6094f8d"></a>
##### Interval MINUTE

The following are examples of using interval MINUTE literals.

<a id="d69bc8ba8483fb4b"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'MINUTE INTERVAL'00 00:01:00'MINUTE | 1 minute | +00 00:01:00 |
| INTERVAL'12345'MINUTE(4) | It exceeds the leading precision 4, so it returns the error | - |
| INTERVAL'12345'MINUTE(5) | 8 day 13 hour 45 minute | +00008 13:45:00 |
| INTERVAL'+999999'MINUTE(6) | 694 day 10 hour 39 minute | +000694 10:39:00 |
| INTERVAL'-999999'MINUTE(6) | -(694 day 10 hour 39 minute) | -000694 10:39:00 |

<a id="d664c6690500036e"></a>
##### Interval SECOND

The followings are examples of using interval SECOND literals.

<a id="664ad08551bfc902"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'SECOND INTERVAL'00 00:00:01.000000'SECOND | 1 second | +00 00:00:01.000000 |
| INTERVAL'100'SECOND | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'99.9999999'SECOND INTERVAL'99.9999999'SECOND(2,6) | The fractional seconds are rounded off to become 100 second, then it exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'99.9999999'SECOND(3) | 1 minute 40 second | +000 00:01:40.000000 |
| INTERVAL'29.506167'SECOND(2, 2) | 29.51 second | +00 00:00:29.51 |
| INTERVAL'999999.999999'SECOND(6,6) | 11day 13 hour 46 minute 39.999999 second | +000011 13:46:39.999999 |
| INTERVAL'-999999.999999'SECOND(6,6) | -(11day 13 hour 46 minute 39.999999 second) | -000011 13:46:39.999999 |

<a id="b80f5563de3026b3"></a>
##### Interval DAY TO HOUR

The followings are examples of using interval DAY TO HOUR literals.

<a id="e3becc94548707b6"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1 23'DAY TO HOUR INTERVAL'01 23:00:00'DAY TO HOUR | 1 day 23 hour | +01 23:00:00 |
| INTERVAL'1 24'DAY TO HOUR | The hour value exceeds 23 (invalid), so it returns the error. | - |
| INTERVAL'100 23'DAY TO HOUR | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100 23'DAY(3) TO HOUR | 100 day 23 hour | +100 23:00:00 |
| INTERVAL'+999999 23'DAY(6) TO HOUR | 999999 day 23 hour | +999999 23:00:00 |
| INTERVAL'-999999 23'DAY(6) TO HOUR | -(999999 day 23 hour) | -999999 23:00:00 |
| INTERVAL'-999999 +23'DAY(6) TO HOUR | Invalid sign error | - |

<a id="5768f8370e514ad9"></a>
##### Interval DAY TO MINUTE

The followings are examples of using interval DAY TO MINUTE literals.

<a id="df4f0f90207ee09b"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1 23:59'DAY TO MINUTE INTERVAL'01 23:59:00'DAY TO MINUTE | 1 day 23 hour 59 second | +01 23:59:00 |
| INTERVAL'1 24:59'DAY TO MINUTE | The hour value exceeds 23 (invalid), so it returns the error. | - |
| INTERVAL'1 23:60'DAY TO MINUTE | The minute value exceeds 59 (invalid), so it returns the error. | - |
| INTERVAL'100 23:59'DAY TO MINUTE | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100 23:59'DAY(3) TO MINUTE | 100 day 23 hour 59 minute | +100 23:59:00 |
| INTERVAL'+999999 23:59'DAY(6) TO MINUTE | 999999 day 23 hour 59 minute | +999999 23:59:00 |
| INTERVAL'-999999 23:59'DAY(6) TO MINUTE | -(999999 day 23 hour 59 minute) | -999999 23:59:00 |

<a id="5e76c47219a2d834"></a>
##### Interval DAY TO SECOND

The followings are examples of using interval DAY TO SECOND literals.

<a id="5cd0eb0e9441280f"></a>
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

<a id="0d55ff132805bc7e"></a>
##### Interval HOUR TO MINUTE

The followings are examples of using interval HOUR TO MINUTE literals.

<a id="47b993c7c33e47d5"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'23:59'HOUR TO MINUTE INTERVAL'00 23:59:00'HOUR TO MINUTE | 23 hour 59 minute | +00 23:59:00 |
| INTERVAL'23:60'HOUR TO MINUTE | The minute value exceeds 59, so it returns the error. | - |
| INTERVAL'100:59'HOUR TO MINUTE | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100:59'HOUR(3) TO MINUTE | 4 day 4 hour 59 minute | +004 04:59:00 |
| INTERVAL'+999999:59'HOUR(6) TO MINUTE | 41666 day 15 hour 59 minute | +041666 15:59:00 |
| INTERVAL'-999999:59'HOUR(6) TO MINUTE | -(41666 day 15 hour 59 minute) | -041666 15:59:00 |

<a id="d72bf30e9720a235"></a>
##### Interval HOUR TO SECOND

The followings are examples of using interval HOUR TO SECOND literals.

<a id="7e7066f08c6e2a07"></a>
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

<a id="8ecfb5f72c55c12d"></a>
##### Interval MINUTE TO SECOND

The followings are examples of using interval MINUTE TO SECOND literals.

<a id="af2f3d579c98c9c1"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL '15:23.123456'MINUTE TO SECOND INTERVAL '00 00:15:23.123456'MINUTE TO SECOND | 15 minute 23.123456 second | +00 00:15:23.123456 |
| INTERVAL '15:60.123456'MINUTE TO SECOND | The second value exceeds 59, so it returns the error. | - |
| INTERVAL '99:59.999999'MINUTE TO SECOND(2) | The fractional seconds are rounded off to become 100 minute, then it exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL '99:59.999999'MINUTE(3) TO SECOND(2) | 1 hour 40 minute | +000 01:40:00.00 |
| INTERVAL '+999999:59.999999'MINUTE(6) TO SECOND(6) | 694 day 10 hour 39 minute 59.999999 second | +000694 10:39:59.999999 |
| INTERVAL '-999999:59.999999'MINUTE(6) TO SECOND(6) | -(694 day 10 hour 39 minute 59.999999 second) | -000694 10:39:59.999999 |

<a id="79e2a1092a16aa23"></a>
### Null Value

Null value is an unknown value or an undefined value. NULL value can be a value of any data type. The unknown value of the boolean type is represented as null value.  
Null value is defined as a keyword and it is not case-sensitive.

The following is an example of null value representation.

```
NULL
Null
```

<a id="49ffe3ea6c4c9c20"></a>
### Comments

<a id="6c7a47be56a9cd02"></a>
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

<a id="896853ba877814d2"></a>
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

<a id="230d96dd82f95da7"></a>
#### Hint Comment

A hint comment is a comment which starts with /*+ and ends with */. Hint comment is similar to multiple line comment, but the difference is that the hint comment has + at the beginning.   
Do not use a space between * and +. If  so,  it will be treated as multiple line comment.

Unlike other comments, a hint comment is specified to be used only at the location which is right after the SELECT keyword. The processing method which a user specified to GOLDILOCKS optimizer is described in the hint comment. For more information, refer to [SQL Hint](15-sql-tuning.md#e90c024d4bbaa9c2).

The following is an example of using hint comment.

```
gSQL> SELECT /*+ FULL(T1) */ * FROM T1;

I1        I2        I3        I4        I5       
--------- --------- --------- --------- ---------
column i1 column i2 column i3 column i4 column i5

1 row selected.
```

<a id="6cca99875cc7b4c1"></a>
### SQL Reserved Words and Keywords

<a id="5ae7cebdbdcec4ca"></a>
#### SQL Reserved Words

GOLDILOCKS supports reserved words which are specified as SQL reserved words. The SQL reserved words can not be used other than specified location.

SQL reserved words can be used as identifiers by using double quotes ("), but it is not recommended to use it as follows, because readability decreases.

```
gSQL> CREATE TABLE "SELECT" ( "FROM" INTEGER );

Table created.

gSQL> INSERT INTO "SELECT" ( "FROM" ) VALUES ( 1 );

1 row created.

gSQL> SELECT "FROM" FROM "SELECT";

FROM
----
   1

1 row selected.
```

The followings are SQL reserved words of GOLDILOCKS. * marked SQL reserved words are supported by the SQL standard.   
For more information about the list, refer to [V$RESERVED_WORDS](../part-02-administration-manual/9-database-information.md#d58140da46e78771).

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

<a id="b13522f7af5e7d39"></a>
#### SQL Keywords

GOLDILOCKS SQL keywords are not reserved words. However, they are keywords which are internally used by GOLDILOCKS. Therefore, it is not recommended to use GOLDILOCKS SQL keywords because it can decrease the readability of the results.

GOLDILOCKS SQL keywords list can be viewed through [V$KEYWORDS](../part-02-administration-manual/9-database-information.md#67f0fb12c1cb72b7).

<a id="218e8097ceb8b9d0"></a>
### Compatibility for Syntax Elements

The SQL standard compatibility for syntax element is as follows.

**SQL standard compatibility for syntax element**

<a id="d306302643e21e4c"></a>
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

<a id="545971a2288a7b29"></a>
## Data Type

<a id="d01260c583e50d66"></a>
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

<a id="ae7e8f7fcee8a477"></a>
#### Decimal Numeric Type

This type's precision and scale are based on decimal number. The precision indicates accuracy of the valid digits, and the scale indicates the range of fraction.

<a id="a1276bb263e38ebc"></a>
##### Decimal Fixed Point Number Type

The decimal fixed point number type is defined in SQL.

**Decimal fixed point number type**

<a id="a55ef66a8be14f2f"></a>
| Type | Decimal precision | Decimal scale | Refer to |
| --- | --- | --- | --- |
| NUMBER( p ) | p | 0 | [NUMBER](16-built-in-data-type-references.md#8b9bf393a6b71702) |
| NUMBER( p, s ) | p | s | [NUMBER](16-built-in-data-type-references.md#8b9bf393a6b71702) |
| NUMERIC( p ) | p | 0 | [NUMERIC](16-built-in-data-type-references.md#8cdfb339ae3e47bf) |
| NUMERIC( p, s ) | p | s | [NUMERIC](16-built-in-data-type-references.md#8cdfb339ae3e47bf) |
| DECIMAL( p ) | p | 0 | [NUMERIC](16-built-in-data-type-references.md#8cdfb339ae3e47bf) type alias |
| DECIMAL( p, s ) | p | s | [NUMERIC](16-built-in-data-type-references.md#8cdfb339ae3e47bf) type alias |
| DEC( p ) | p | 0 | [NUMERIC](16-built-in-data-type-references.md#8cdfb339ae3e47bf) type alias |
| DEC( p, s ) | p | s | [NUMERIC](16-built-in-data-type-references.md#8cdfb339ae3e47bf) type alias |
| SMALLINT | 5 | 0 | [NUMBER](16-built-in-data-type-references.md#8b9bf393a6b71702) type alias |
| INTEGER | 10 | 0 | [NUMBER](16-built-in-data-type-references.md#8b9bf393a6b71702) type alias |
| BIGINT | 19 | 0 | [NUMBER](16-built-in-data-type-references.md#8b9bf393a6b71702) type alias |
| INT2 | 5 | 0 | [NUMBER](16-built-in-data-type-references.md#8b9bf393a6b71702) type alias |
| INT4 | 10 | 0 | [NUMBER](16-built-in-data-type-references.md#8b9bf393a6b71702) type alias |
| INT8 | 19 | 0 | [NUMBER](16-built-in-data-type-references.md#8b9bf393a6b71702) type alias |

<a id="dc5a6ec986b5446f"></a>
##### Decimal Floating Point Number Type

The decimal floating point number type is defined in SQL.

**Decimal floating point number type**

<a id="f4afa94c53f0e2f8"></a>
| Type | Decimal precision | Decimal scale | Refer to |
| --- | --- | --- | --- |
| NUMBER | 38 | N/A | [NUMBER](16-built-in-data-type-references.md#8b9bf393a6b71702) |
| FLOAT( p ) | ceil( log<sub>10</sub> 2<sup>p</sup> ) | N/A | [FLOAT](16-built-in-data-type-references.md#e1bb6a1eec7496d0) |
| REAL | ceil( log<sub>10</sub> 2<sup>24</sup> ) = 8 | N/A | [FLOAT](16-built-in-data-type-references.md#e1bb6a1eec7496d0) type alias |
| DOUBLE | ceil( log<sub>10</sub> 2<sup>53</sup> ) = 16 | N/A | [FLOAT](16-built-in-data-type-references.md#e1bb6a1eec7496d0) type alias |
| FLOAT4 | ceil( log<sub>10</sub> 2<sup>24</sup> ) = 8 | N/A | [FLOAT](16-built-in-data-type-references.md#e1bb6a1eec7496d0) type alias |
| FLOAT8 | ceil( log<sub>10</sub> 2<sup>53</sup> ) = 16 | N/A | [FLOAT](16-built-in-data-type-references.md#e1bb6a1eec7496d0) type alias |

<a id="794ed8183d369f4c"></a>
#### Binary Number Type

This type's precision and scale are based on binary number. The precision indicates accuracy of the valid digits, and the scale indicates the range of fraction.

<a id="53e3ea4d6ed037e3"></a>
##### Binary Fixed Point Number Type

The binary fixed point number type refers to the signed integer data type of C language.  
1 bit is used to represent the sign bit, and other bits are used to represent the precision, but not any bit is used to represent the scale.

**Binary fixed point number type**

<a id="f28a36016d4bc47b"></a>
| Type | Binary precision | Binary scale | Refer to |
| --- | --- | --- | --- |
| NATIVE_SMALLINT | 15 | 0 | [NATIVE_SMALLINT](16-built-in-data-type-references.md#6d0effad10db44e1) |
| NATIVE_INTEGER | 31 | 0 | [NATIVE_INTEGER](16-built-in-data-type-references.md#781670ea6f07e05f) |
| NATIVE_BIGINT | 63 | 0 | [NATIVE_BIGINT](16-built-in-data-type-references.md#3ab4c4c4b2da694c) |

<a id="75c73c75d26633db"></a>
##### Binary Floating Point Number Type

The binary floating point type refers to the float and double data type in C language.  
1 bit is used to represent the sign bit, and other bits are used to represent the precision and scale.

**Binary floating point number type**

<a id="fe26e5908565edf2"></a>
| Type | Binary precision | Binary scale | Refer to |
| --- | --- | --- | --- |
| NATIVE_REAL | 23 | 8 | [NATIVE_REAL](16-built-in-data-type-references.md#00e9340516368be0) |
| NATIVE_DOUBLE | 52 | 11 | [NATIVE_DOUBLE](16-built-in-data-type-references.md#16b7464454d1f023) |

> The precision and scale of binary floating point type is subject to change depending on the influence of the compiler and OS.

<a id="752907f1cc4f8892"></a>
### CHARACTER STRING Type

CHARACTER STRING data types are classified according to whether it is a variable length string and the maximum length of string.

- Classification by whether it is a variable length string
    - Fixed length string
        - Refer to [CHARACTER](16-built-in-data-type-references.md#c2f6a601412ef1cc).
    - Variable length string 
        - Refer to [CHARACTER VARYING](16-built-in-data-type-references.md#f627085c747f8be8), [CHARACTER LONG VARYING](16-built-in-data-type-references.md#ce64f50f891e4a29).
- Classification by the maximum length of a string
    - 2000 [ characters or bytes ] 
        - Refer to [CHARACTER](16-built-in-data-type-references.md#c2f6a601412ef1cc).
    - 4000 [ characters or bytes ] 
        - Refer to [CHARACTER VARYING](16-built-in-data-type-references.md#f627085c747f8be8).
    - 100 megabytes 
        - Refer to [CHARACTER LONG VARYING](16-built-in-data-type-references.md#ce64f50f891e4a29).

<a id="53d13823562bef41"></a>
### BINARY STRING Type

BINARY STRING data types are classified according to whether it is a variable length binary string and the maximum length of binary string.

- Classification by whether it is a variable length binary string 
    - Fixed length binary string 
        - Refer to [BINARY](16-built-in-data-type-references.md#cdba24bfff4b3bfd).
    - Variable length binary string 
        - Refer to [BINARY VARYING](16-built-in-data-type-references.md#b2a630321104f6a3), [BINARY LONG VARYING](16-built-in-data-type-references.md#40f9036f7bb326d8).
- Classification by the maximum length of binary string
    - 2000 
        - Refer to [BINARY](16-built-in-data-type-references.md#cdba24bfff4b3bfd).
    - 4000 
        - Refer to [BINARY VARYING](16-built-in-data-type-references.md#b2a630321104f6a3).
    - 100 Mega Bytes 
        - Refer to [BINARY LONG VARYING](16-built-in-data-type-references.md#40f9036f7bb326d8).

<a id="d8b2afd2a5a14f39"></a>
### Date/ Time Type

Date/ time data type specifies the year, month, day, hour, minute, second, time zone offset in accordance with their representation method.   
Date/ time type has [DATE](16-built-in-data-type-references.md#8689fda1b80cf3b7), [TIME](16-built-in-data-type-references.md#654af5ad2c0e7412), [TIMESTAMP](16-built-in-data-type-references.md#a616b596ff859564) types.

<a id="87bf3ead3985b893"></a>
### INTERVAL Type

INTERVAL data type specifies the time interval.   
It specifies the time interval of the year, month, day, hour, minute, second in accordance with their representation method.

[INTERVAL](16-built-in-data-type-references.md#22fc0092f6f0fd6f) data types are classified to the YEAR TO MONTH family type and the DAY TO SECOND family type, according to the range of value representation.

<a id="062ff2008813de64"></a>
### BOOLEAN Type

The BOOLEAN data type stores truth value of TRUE, FALSE, UNKNOWN. UNKNOWN value is represented as a null value. All expressions used as conditions return the BOOLEAN value and the column or the value defined as a BOOLEAN data type can be used as a condition.

The following literals can be stored in the boolean data type.

- TRUE
    - Keyword: TRUE
    - Literal: 't', 'true' , 'y', 'yes' , 'on' ,'1'
- FALSE
    - Keyword: FALSE
    - Literal: 'f', 'false', 'n', 'no', 'off', '0'
- UNKNOWN
    - Keyword: UNKNOWN, NULL

For more information, refer to [BOOLEAN](16-built-in-data-type-references.md#a62b94ed1d88f602).

<a id="a235ad344ca3cce7"></a>
### ROWID Type

All records stored in the database have unique location information. The record identifier (ROWID) is used to distinguish each record.

ROWID data type is used to store and manage the record identifier (ROWID).  
Record identifier (ROWID) is obtained by the query using the ROWID pseudo column.

For more information, refer to [ROWID](16-built-in-data-type-references.md#15b522cf4559d114).

<a id="74108eb6d21a543c"></a>
### Type Comparison

Comparing two types is executed on the basis of one representative type. If the comparison target type is different from the representative type, then the comparison can go through a type conversion.  
[The representative types for type comparison](#e1676865899f5530) defines the representative type for comparing two types.

The following table describes target type conversion for comparison per each representative type.

- [ Type conversion for the VC comparison](#54d309301071217a)
- [Type conversion for the LC comparison](#f7eef3e5f5be4b8f)
- [Type conversion for the VB comparison](#4b82179de60ecdf6)
- [Type conversion for the LB comparison](#f45876c36de78cee)
- [Type conversion for the NB comparison](#18206b264fda64ab)
- [Type conversion for the ND comparison](#abee9b8e63ebffba)
- [Type conversion for the NU comparison](#6ca196d5f5b96cfd)
- [Type conversion for the DA comparison](#42b490eeedf27ab3)
- [Type conversion for the TI comparison](#bad7ccf7e6ec9112)
- [Type conversion for the TZ comparison](#c561ec50604c4730)
- [Type conversion for the TS comparison](#27a0c60b008ef6c8)
- [Type conversion for the SZ comparison](#d7f53615c7590b93)
- [Type conversion for the YM comparison](#a915c32c71b8f52a)
- [Type conversion for the DS comparison](#9dd65ec227742938)
- [Type conversion for the BO comparison](#130229901666c319)
- [Type conversion for the RI comparison](#c0f900fdb1cc095e)

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

<a id="e1676865899f5530"></a>
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

<a id="54d309301071217a"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | CHAR (no conversion) |
| VARCHAR | VARCHAR (no conversion) |

**Type conversion for the LC comparison**

<a id="f7eef3e5f5be4b8f"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | CHAR (no conversion) |
| VARCHAR | VARCHAR (no conversion) |
| LONG VARCHAR | LONG VARCHAR (no conversion) |

**Type conversion for the VB comparison**

<a id="4b82179de60ecdf6"></a>
| Source type | Converted type |
| --- | --- |
| BINARY | BINARY (no conversion) |
| VARBINARY | VARBINARY (no conversion) |

**Type conversion for the LB comparison**

<a id="f45876c36de78cee"></a>
| Source type | Converted type |
| --- | --- |
| BINARY | BINARY (no conversion) |
| VARBINARY | VARBINARY (no conversion) |
| LONG VARBINARY | LONG VARBINARY (no conversion) |

**Type conversion for the NB comparison**

<a id="18206b264fda64ab"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | NATIVE_BIGINT |
| VARCHAR | NATIVE_BIGINT |
| LONG VARCHAR | NATIVE_BIGINT |
| NATIVE_SMALLINT | NATIVE_SMALLINT (no conversion) |
| NATIVE_INTEGER | NATIVE_INTEGER (no conversion) |
| NATIVE_BIGINT | NATIVE_BIGINT (no conversion) |

**Type conversion for the ND comparison**

<a id="abee9b8e63ebffba"></a>
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

<a id="6ca196d5f5b96cfd"></a>
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

<a id="42b490eeedf27ab3"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | DATE |
| VARCHAR | DATE |
| LONG VARCHAR | DATE |
| DATE | DATE (no conversion) |

**Type conversion for the TI comparison**

<a id="bad7ccf7e6ec9112"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | TIME |
| VARCHAR | TIME |
| LONG VARCHAR | TIME |
| TIME | TIME (no conversion) |

**Type conversion for the TZ comparison**

<a id="c561ec50604c4730"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | TIME_TZ |
| VARCHAR | TIME_TZ |
| LONG VARCHAR | TIME_TZ |
| TIME | TIME_TZ |
| TIME_TZ | TIME_TZ (no conversion) |

**Type conversion for the TS comparison**

<a id="27a0c60b008ef6c8"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | TIMESTAMP |
| VARCHAR | TIMESTAMP |
| LONG VARCHAR | TIMESTAMP |
| DATE | DATE (no conversion) |
| TIMESTAMP | TIMESTAMP (no conversion) |

**Type conversion for the SZ comparison**

<a id="d7f53615c7590b93"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | TIMESTAMP_TZ |
| VARCHAR | TIMESTAMP_TZ |
| LONG VARCHAR | TIMESTAMP_TZ |
| DATE | TIMESTAMP_TZ |
| TIMESTAMP | TIMESTAMP_TZ |
| TIMESTAMP_TZ | TIMESTAMP_TZ (no conversion) |

**Type conversion for the YM comparison**

<a id="a915c32c71b8f52a"></a>
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

<a id="9dd65ec227742938"></a>
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

<a id="130229901666c319"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | BOOLEAN |
| VARCHAR | BOOLEAN |
| LONG VARCHAR | BOOLEAN |
| BOOLEAN | BOOLEAN (no conversion) |

**Type conversion for the RI comparison**

<a id="c0f900fdb1cc095e"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | ROWID |
| VARCHAR | ROWID |
| LONG VARCHAR | ROWID |
| ROWID | ROWID (no conversion) |

<a id="935e2183d0c42aa6"></a>
### Type Conversion

Type conversions are classified into implicit type conversion and explicit type conversion.

- Implicit type conversion occurs in an expression, an operator, a function, a condition for select, insert, delete, update.
- Explicit type conversion occurs through the CAST operator.

[The availability of type conversion](#66454a14986f3134) describes the availability of data type conversion from a type to another type.

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

<a id="66454a14986f3134"></a>
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
        - For more information, refer to [Interval Literals](#63d668408fea8219).
        - An overflow can occur due to a precision which is defined in the converted type.
    - When the source type is NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, NUMBER, NUMERIC or FLOAT type: 
        - The converted type should be a single field (YEAR, MONTH).
        - An overflow can occur due to a precision which is defined in the converted type.
    - When the source type is INTERVAL YEAR TO MONTH family type: 
        - An overflow can occur due to a precision which is defined in the converted type.

- Conversion to INTERVAL DAY TO SECOND family type 
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the day-time interval literal format, then an error occurs. 
        - For more information, refer to [Interval Literals](#63d668408fea8219).
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

<a id="9438f6bc84fe7548"></a>
### Type Combination

<a id="57bc8450b96059e0"></a>
#### When Type Combination Is Required

A CASE operator and a [set operator](20-sql-references-h-z.md#fcd983bb04411568) have many expressions as a result of operation.  
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
    - [set operator](20-sql-references-h-z.md#fcd983bb04411568)
    - CASE operator
        - [CASE Expression](#dfe24bf5cf0e78f1)
        - [COALESCE](17-built-in-function-references.md#9721055bac9c198a)
        - [NULLIF](17-built-in-function-references.md#66e124ffb2b38351)

<a id="9a5dc6c72b766b73"></a>
#### Result Type Combination Rule

Each expression's data type should be the same family type which is available to combine.

- Examples of applying result type combination rule
    - [set operator](20-sql-references-h-z.md#fcd983bb04411568)
    - CASE operator
        - [CASE Expression](#dfe24bf5cf0e78f1)
        - [COALESCE](17-built-in-function-references.md#9721055bac9c198a)
        - [NULLIF](17-built-in-function-references.md#66e124ffb2b38351)

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

<a id="ba23932e1947e13a"></a>
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
- For more information, refer to [Type Comparison](#74108eb6d21a543c).

<a id="9a3233f3f0654fd0"></a>
### Compatibility for Data Type

The SQL standard compatibility for data type is as follows.

**SQL standard compatibility for data type**

<a id="d5ceb35119c13ccf"></a>
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

<a id="204fc42f50290b86"></a>
## Format String

Format string defines the format which is used when a numeric type or date/time type is converted to a character string or when a character string is converted to a numeric types or date/time type.

- When a numeric type or date/time type is converted to a character string type, the representation format of the string is as follows.
    - Refer to [TO_CHAR( number )](17-built-in-function-references.md#d69061b89662a768), [TO_CHAR( datetime )](17-built-in-function-references.md#24c99d6f3463acf6).
    - Numeric type: TO_CHAR( 1234.56, 'S9,999.99' ) → '+1,234.56'
    - Date/time type: TO_CHAR( SYSDATE, 'YYYY-MM-DD' ) → '2012-07-15'
- When a character string is converted to the numeric type or date/time type, the representation format of the string is as follows.
    - Refer to [TO_NUMBER](17-built-in-function-references.md#f4c5f4089516a8f7), [TO_NATIVE_REAL](17-built-in-function-references.md#ae266ee6179f808b), [TO_NATIVE_DOUBLE](17-built-in-function-references.md#54731f33ec124462). 
    - Refer to [TO_DATE](17-built-in-function-references.md#5219142a4793653b).
    - Refer to [TO_TIMESTAMP](17-built-in-function-references.md#4343ab929dac120a), [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#19ac77096078990f).
    - Refer to [TO_TIME](17-built-in-function-references.md#9dbf37dc5504a5f2), [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#a7774652486ae49f) .
    - Numeric type: TO_NUMBER( '+1,234.56', 'S9,999.99' ) → NUMBER TYPE
    - Date/time type: TO_DATE( '2012-07-15', 'YYYY-MM-DD' ) → DATE TYPE

Format strings are classified according to the type.  
• Numeric data type: Refer to [Number Format String](#38636b5b44a04ac0).  
• Date/time type: Refer to [Datetime Format String](#b7a47f2ef79b2b26).

<a id="38636b5b44a04ac0"></a>
### Number Format String

Number format string defines the format which is used when a numeric type is converted to a character string type, or when a character string type is converted to a numeric type.

Number format string is used as an argument of the functions such as [TO_CHAR( number )](17-built-in-function-references.md#d69061b89662a768), [TO_NATIVE_SMALLINT](17-built-in-function-references.md#898732df4fa8a0cf), [TO_NATIVE_INTEGER](17-built-in-function-references.md#8e984895b0d5abb0), [TO_NATIVE_BIGINT](17-built-in-function-references.md#4e932440d0c38f36), [TO_NUMBER](17-built-in-function-references.md#f4c5f4089516a8f7), [TO_NATIVE_REAL](17-built-in-function-references.md#ae266ee6179f808b), [TO_NATIVE_DOUBLE](17-built-in-function-references.md#54731f33ec124462).

Number format string can specify multiple format elements according to the desired format.

All number format elements are rounded off to fit the format.  
If the number of digits before the decimal point of the value to be converted is bigger than the number of digits specified in the format string, then they are replaced with '#' character.  
If the format element representing the sign of MI, S, PR is not specified, a negative number returns - sign and a positive number returns a white space to the front of the number.

**Number format elements**

<a id="f9a52349f038d011"></a>
| Format  element | Example | Description |
| --- | --- | --- |
| , (comma) | 9,999 | It returns a comma to the specified position. Multiple commas can be specified. Format string can not begin with a comma, and it can not come after the decimal point (.). |
| . (period) | 99.99 | It returns a decimal point (.) to the specified position. The decimal point in the format string can be specified only once. |
| $ | $9999 | It returns the $ sign to the front of the number. |
| 0 | 0999  9990 | It returns zero (0) to the front of or to the end of the number.  If the number of digits of the value to be converted is smaller than the number of digits to the zero position of the format string, then the gap is filled with zero (0)s and is returned. |
| 9 | 9999 | It returns a white space and numbers according to the sign and the number of specified 9. If the number of digits of the value to be converted is smaller than the number of the specified 9, then the gap is filled with white spaces and is returned. For a positive number, a white space is returned to the front of the number. For a negative number, '-' symbol is returned to the front of the number. If the value before the format string's decimal point is 0, then 0 is returned as a white space. e.g. TO_CHAR( 0.123, '9.999' ) → .123 e.g. TO_CHAR( 0, '9' ) → 0 |
| B | B9999 | If the value is zero, it returns a white space. |
| EEEE | 9.9EEEE | It returns in exponential notation. It can be at the end of format string or it can be in front of S, MI, PR.  It can not be specified together with a comma (,). |
| MI | 9999MI | For a positive number, a white space is returned to the end of the number. For a negative number, '-' symbol is returned to the end of the number. It can be specified only at the end of format string and it can not be specified together with S, PR. |
| PR | 9999PR | For a positive number, white spaces are returned to the beginning and end of the number. For a negative number, it returns the number into the inside of angle brackets. &lt;number&gt;  It can be specified only at the end of format string, and it can not be specified together with S, MI. |
| RN  rn | RN rn | Roman numerals are converted to uppercase and returned. (RN) Roman numerals are converted to lowercase and returned. (rn) Only the numbers between 1 ~ 3999 are returned. It can be specified together only with FM format element, but it can not be specified with any other format elements. It can not be used in TO_NUMBER function. |
| S | S9999 9999S | For a positive number, '+' symbol is returned to the front of the number. For a negative number, '-' symbol is returned to the front of the number. (S9999) For a positive number, '+' symbol is returned to the end of the number. For a negative number, '-' symbol is returned to the end of the number. (9999S) It can be specified only at the beginning of format string or at the end of format string. It can not be specified together with MI, PR. |
| V | 999V99 | 10<sup>n</sup>(n: the digit number of 9 after V format element) multiplied by the value is returned.  It can not specified together with the decimal point (.). It can not be used in TO_NUMBER function. |
| X | XXXX xxxx | It returns the white space and hexadecimal number according to the digit number of the specified X. It converts an integer value to the hexadecimal number, and returns it. (A non-integer value is rounded off to make it to an integer value.) XXX returns hexadecimal uppercase letters and xxxx returns hexadecimal lowercase letters. If the number of the converted hexadecimal digit is smaller than the number of the specified X, then the gap is filled with white spaces and is returned. Only 0 and positive integers are processed, and negative numbers are replaced with '#'. It can be specified together only with format element 0 and FM, but it can not be specified with any other format elements. |
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

<a id="b7a47f2ef79b2b26"></a>
### Datetime Format String

Datetime format string defines the format which is used when a date/time type is converted to a character string type, or when a character string type is converted to a date/time type.

Datetime format string is used as an argument of the functions such as [TO_CHAR( datetime )](17-built-in-function-references.md#24c99d6f3463acf6), [TO_DATE](17-built-in-function-references.md#5219142a4793653b), [TO_TIMESTAMP](17-built-in-function-references.md#4343ab929dac120a), [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#19ac77096078990f), [TO_TIME](17-built-in-function-references.md#9dbf37dc5504a5f2), [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#a7774652486ae49f).

For datetime format string, if the format string is not specified, then the default value is used. The default value of each type is specified in the session property (NLS _ * _ FORMAT).

- DATE: Refer to [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#7ea8c558693ab9b8).
- TIMESTAMP: Refer to [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#f745ba729e1e8deb).
- TIMESTAMP WITH TIME ZONE: Refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#226a187670420c2f).
- TIME: Refer to [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#fff3ca3eeeea7a35).
- TIME WITH TIME ZONE: Refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#6a87f7e07e80669e).

NLS * _FORMAT values can be changed by using [ALTER SESSION SET property_name](18-sql-references-a-b.md#92680bbe05326073).

In datetime format string, multiple format elements can be specified upon the desired representation.

**Datetime format elements**

<a id="2ac82badb9f973a2"></a>
<table><thead><tr><th align="center" valign="middle">Format<br>element</th><th align="center" valign="middle">Whether to use TO_*<br>datetime</th><th align="center" valign="middle">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">-<br>/<br>,<br>.<br>;<br>:<br>"text"<br>Special characters</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the format element character to the specified location.</td></tr><tr><td align="left" valign="middle">AD<br>A.D.</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">AD with or without periods.</td></tr><tr><td align="left" valign="middle">AM<br>A.M.</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">AM with or without periods.</td></tr><tr><td align="left" valign="middle">BC<br>B.C.</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">BC with or without periods.</td></tr><tr><td align="left" valign="middle">CC</td><td align="left" valign="middle">N</td><td align="left" valign="middle">Century<br>If the last two digits of the four digits year is 01~ 99, the value which is added by one to the first two digits is returned. (e.g. If the year is 2005, 21 is returned.)<br>If the last two digits of the four digits year is 00, the first two digits value is returned. (e.g. If the year is 2000, 20 is returned.)</td></tr><tr><td align="left" valign="middle">D</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the sequence of the day in a week. (1 ~ 7)<br>Sunday is 1, saturday is 7, and so on.</td></tr><tr><td align="left" valign="middle">DAY<br>Day<br>day</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the day of the week. (e.g. SUNDAY )<br><ul><li>DAY: The day which is all in uppercase is returned.</li><li>Day: The day whose first character is uppercase and others are lowercase is returned.</li><li>day: The day which is all in lowercase is returned.</li></ul></td></tr><tr><td align="left" valign="middle">DD</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the sequence of the day in a month. (1 ~ 31)</td></tr><tr><td align="left" valign="middle">DDD</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the sequence of the day in a year. (1 ~ 366)</td></tr><tr><td align="left" valign="middle">DY<br>Dy<br>dy</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the abbreviated word for the day of the week. (e.g. SUN)<br><ul><li>DY: The day which is all in uppercase is returned.</li><li>Dy: The day whose first character is uppercase and others are lowercase is returned.</li><li>dy: The day which is all in lowercase is returned.</li></ul></td></tr><tr><td align="left" valign="middle">FF[1..6]</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns fractional seconds as many as the number of the specified digits (1-6) after FF.<br>If the number is not specified, the default value is 6. (FF is equal to FF6.)<br>If the number of fractional seconds digit is bigger than the number specified after FF, then it is rounded down.<br>If the number of fractional seconds digit is smaller than the number specified after FF, then zero(0) is added according to the specified number.<br>It can not be used in DATE type.</td></tr><tr><td align="left" valign="middle">HH<br>HH12</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">The hour (1 ~ 12)</td></tr><tr><td align="left" valign="middle">HH24</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">The hour (0 ~ 23)</td></tr><tr><td align="left" valign="middle">IW</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The week containing the first thursday of the year designated as the calendar week by ISO 8601 standards (1 ~ 52 week or 1 ~ 53 weeks) becomes the first week.<br><ul><li>The calendar week starts from monday.</li><li>The first calendar week includes January 4th.</li><li>The first calendar week may includes December 29th, 30th, and 31st.</li><li>The last calendar week may include January 1st, 2nd, and 3rd.</li></ul></td></tr><tr><td align="left" valign="middle">IYYY</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The 4 digits year embracing the calendar week defined by ISO 8601 standards.</td></tr><tr><td align="left" valign="middle">IYY<br>IY<br>I</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The 3 digits year embracing the calendar week defined by ISO 8601 standards.<br>The 2 digits year embracing the calendar week defined by ISO 8601 standards.<br>The single digit year embracing the calendar week defined by ISO 8601 standards.</td></tr><tr><td align="left" valign="middle">J</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Julian day: The number of days since BC 4714-11-24</td></tr><tr><td align="left" valign="middle">MI</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Minute (0 ~ 59)</td></tr><tr><td align="left" valign="middle">MM</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Month (01 ~ 12), January(01)~December(12)</td></tr><tr><td align="left" valign="middle">MON<br>Mon<br>mon</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">The abbreviated word for the month. (e.g. JAN)<br><ul><li>MON: The month which is all in uppercase is returned.</li><li>Mon: The month whose first character is uppercase and others are lowercase is returned.</li><li>mon: The month which is all in lowercase is returned.</li></ul></td></tr><tr><td align="left" valign="middle">MONTH<br>Month<br>month</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">The month name (e.g. JANUARY )<br><ul><li>MONTH: All uppercase month name is returned.</li><li>Month: The month name that only the first letter is uppercase and others are lowercase is returned.</li><li>month: The month of which is all in lowercase is returned.</li></ul></td></tr><tr><td align="left" valign="middle">PM<br>P.M.</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">PM with or without periods.</td></tr><tr><td align="left" valign="middle">Q</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The quarter of the year (1 ~ 4)<br>January to March is 1 and October to December is 4.</td></tr><tr><td align="left" valign="middle">RM<br>Rm<br>rm</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the roman numeral month. (e.g. I)<br><ul><li>RM: The month which is all in uppercase is returned.</li><li>Rm: The month whose first character is uppercase and others are lowercase is returned.</li><li>rm: The month which is all in lowercase is returned.</li></ul></td></tr><tr><td align="left" valign="middle">RR</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Adjusted two digit year<br>The two digit year represented by RR can be converted to four digit year as follows.<br><ul><li>When the two digit year represented by RR is 00~49:<br><ul><li>If the last two digits of the current year is 00~50,<br><ul><li>the four digit year is represented using the first two digits of the current year and the two digits which is represented by RR.</li></ul></li><li>If the last two digits of the current year is 51~99,<br><ul><li>the four digit year is represented using "the first two digits of the current year+1" and the two digits which is represented by RR.</li></ul></li></ul></li><li>When the two digit year represented by RR is 50~99:<br><ul><li>If the last two digits of the current year is 00~50,<br><ul><li>the four digit year is represented using "the first two digit of the current year - 1" and the two digits which is represented by RR.</li></ul></li><li>If the last two digit of the current year is 51~99,<br><ul><li>the four digit year is expressed using the first two digit of the current year and the two digits which is represented by RR.</li></ul></li></ul></li></ul></td></tr><tr><td align="left" valign="middle">RRRR</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Adjusted four digit year<br>Two digit or four digit can be input.<br>Two digit input is processed in the same way as RR.</td></tr><tr><td align="left" valign="middle">SS</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Second (0 ~ 59)</td></tr><tr><td align="left" valign="middle">SSSSS</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Seconds since last midnight (0 ~ 86399)</td></tr><tr><td align="left" valign="middle">TZH</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Time Zone Hour<br>It can not be used in DATE, TIMESTAMP, TIME types. It is available in TIMESTAMP WITH TIME ZONE, TIME WITH TIME ZONE types.</td></tr><tr><td align="left" valign="middle">TZM</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Time Zone Minute<br>It can not be used in DATE, TIMESTAMP, TIME types. It can be used only in TIMESTAMP WITH TIME ZONE, TIME WITH TIME ZONE types.</td></tr><tr><td align="left" valign="middle">WW</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The sequence of the week in a year. (1~ 53)<br>The first week 1 starts on the first day of the year and continues to the seventh day of the year.</td></tr><tr><td align="left" valign="middle">W</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The sequence of the week in a month. (1 ~ 5)<br>The first week 1 starts on the first day of the month and ends on the seventh day.</td></tr><tr><td align="left" valign="middle">Y,YYY</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the year with comma in the Y,YYY form.</td></tr><tr><td align="left" valign="middle">YYYY<br>SYYYY</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Four digit year.<br>SYYYY displays the sign of year.<br><ul><li>If it is BC, it displays '-'. If it is AD, it displays ' '.</li></ul></td></tr><tr><td align="left" valign="middle">YYY<br>YY<br>Y</td><td align="left" valign="middle">Y</td><td align="left" valign="middle"><ul><li>YYY: The last three digit year of the current year</li><li>YY: The last two digit year of the current year</li><li>Y: The last one digit year of the current year</li></ul></td></tr></tbody></table>

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
  • TO_CHAR( TO_DATE( '2000-01-01', 'SYYYY-MM-DD' ), 'SYYYY' )
    ==> ' 2000'

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

<a id="82a01b5b328b6d8d"></a>
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
• Compound expression  
• Boolean value expression  
• Case expression  
• Datetime expression  
• Scalar subquery expression  
• Sequence manipulation expression

Simple expressions are column, pseudo columns, literals, and null value.  
Compound expressions are combination of multiple expressions.

For more information, refer to the followings.  
•  [Null Value](#79e2a1092a16aa23)  
•  [Literals](#8b9df43f351a1f27)  
•  [Pseudo Columns](#7ffd98bd5eda90c9)  
•  [Operators](#e1cc6b31a2601cec)  
•  [Functions](#a7e7ad935e284511)

<a id="0e68bbc0e9b58fb8"></a>
### Boolean Value Expression

<a id="8caf8e2d4901c90c"></a>
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

<a id="39f224b576875d70"></a>
#### Description

&lt;boolean value expression&gt; describes a boolean value. &lt;boolean primary&gt; with boolean value are &lt;column&gt;, &lt;condition&gt;, and &lt;boolean predicand&gt;. &lt;column&gt; should be declared as BOOLEAN type, and it is allowed to return a boolean value using CAST.

&lt;boolean value expression&gt; can use logical operators such as AND, OR, NOT, and the dedicated operators of boolean value such as IS, IS NOT are also supported.

IS operator and IS NOT operator which are described in &lt;boolean test&gt; determine whether the boolean value described in &lt;boolean primary&gt; matches with one of the &lt;truth value&gt; (TRUE, FALSE, UNKNOWN).

For more information, refer to [Conditions](#d509ae5b9f752c9a).

<a id="71a9d22180888b5f"></a>
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

<a id="dfe24bf5cf0e78f1"></a>
### CASE Expression

<a id="38d407c745d550bb"></a>
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

<a id="5c8b9442279feb3a"></a>
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

If there are multiple types of THEN or ELSE clause results, the result type is determined by [Result Type Combination Rule](#9a5dc6c72b766b73).

For more information, refer to the followings.  
• [COALESCE](17-built-in-function-references.md#9721055bac9c198a)  
• [NULLIF](17-built-in-function-references.md#66e124ffb2b38351)

<a id="16fbc6c47df2758d"></a>
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

<a id="200d1e19d8f9f1aa"></a>
### CAST Specification

<a id="7f6b0521a0f250ec"></a>
#### Syntax

```
CAST( expression AS data_type )
```

<a id="29d7b9e3c7d47b4b"></a>
#### Description

CAST converts the expression data type to the data type of the specified data_type.

<a id="ab98d1b2f53f7658"></a>
#### Example

```
gSQL> SELECT CAST( '1-2' AS INTERVAL YEAR TO MONTH ) AS RESULT FROM DUAL;  
RESULT
------
+01-02
1 row selected.
```

<a id="80f1dc3bba65909c"></a>
### Scalar Subquery Expression

Scalar subquery expression is a subquery which returns a single row with one column as a result. The scalar subquery expression result is the values described in select list of the subquery.

If the subquery does not return any row, then the result value is NULL, and if it returns two or more rows, then an error occurs.

Scalar subquery expression can be described on most position which describes expression. The subquery should be enclosed in parentheses. Even when scalar subquery expression is used as a function argument and the scalar subquery expression is enclosed in parentheses, other parentheses for the subquery is required regardless of the function parentheses. Otherwise, an error occurs.

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

<a id="348852b220fb8c0d"></a>
### Compatibility

The SQL standard compatibility for expression is as follows.

**SQL standard compatibility for expression**

<a id="497e667ba9f59112"></a>
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
| T121 | WITH (excluding RECURSIVE) in query expression | O |
| T581 | Regular expression substring function | X |

<a id="7ffd98bd5eda90c9"></a>
## Pseudo Columns

Pseudo column is not only similar to function, but also it is similar to table column because it can return different value in row unit every time the pseudo column is executed.

**Supported pseudo column**

<a id="5dc89b53b021502c"></a>
<table><tbody><tr><th align="center">Name</th><th align="center">Description</th><th align="center">Refer to</th></tr><tr><td align="left" valign="middle">CURRVAL</td><td align="left" valign="middle">It is a pseudo column which is related to a sequence.</td><td align="left" valign="middle"><a href="17-built-in-function-references.md#c8e656ddd5bf7118">CURRVAL</a></td></tr><tr><td align="left" valign="middle">NEXTVAL</td><td align="left" valign="middle">It is a pseudo column which is related to a sequence.</td><td align="left" valign="middle"><a href="#1be00498c6fd4676">ROWID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">ROWNUM</td><td align="left" valign="middle">It is the row number which satisfies the condition.</td><td align="left" valign="middle"><a href="17-built-in-function-references.md#d90dc69fd788e5fd">ROWNUM</a></td></tr><tr><td align="left" valign="middle">ROWID</td><td align="left" valign="middle">It returns the record identifier in database.</td><td align="left" valign="middle"><a href="#1be00498c6fd4676">ROWID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_GROUP_ID</td><td align="left" valign="middle">It returns the group identifier in database.</td><td align="left" valign="middle"><a href="#55dbbfadabdaa9f9">CLUSTER_GROUP_ID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_MEMBER_ID</td><td align="left" valign="middle">It returns the member identifier in which the record is stored.</td><td align="left" valign="middle"><a href="#e7869e021625d8f9">CLUSTER_MEMBER_ID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_GROUP_NAME</td><td align="left" valign="middle">It returns the group name in which the record is stored.</td><td align="left" valign="middle"><a href="#15eade318b4045d1">CLUSTER_GROUP_NAME Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_MEMBER_NAME</td><td align="left" valign="middle">It returns the member name in which the record is stored.</td><td align="left" valign="middle"><a href="#e2caabacccf8931a">CLUSTER_MEMBER_NAME Pseudo Column</a></td></tr><tr><td valign="middle">CLUSTER_SHARD_ID</td><td valign="middle">It returns the shard identifier in which the record is stored.</td><td valign="middle"><a href="#23326da41e89ac94">CLUSTER_SHARD_ID Pseudo Column</a></td></tr></tbody></table>

<a id="1be00498c6fd4676"></a>
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

For more information, refer to [ROWID](16-built-in-data-type-references.md#15b522cf4559d114), [ROWID-related Functions](#6a6d19f960a479a3).

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

<a id="55dbbfadabdaa9f9"></a>
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

<a id="e7869e021625d8f9"></a>
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

<a id="15eade318b4045d1"></a>
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

<a id="e2caabacccf8931a"></a>
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

<a id="23326da41e89ac94"></a>
### CLUSTER_SHARD_ID Pseudo Column

CLUSTER_SHARD_ID pseudo column returns the shard identifier in which the record is stored.

CLUSTER_SHARD_ID pseudo column is allowed for SELECT only, but it is not allowed for INSERT, UPDATE, or DELETE.

> This information in valid in the cluster system.

The following is an example of retrieving CLUSTER_SHARD_ID pseudo column.

```
gSQL> SELECT T1.C1, T1.CLUSTER_SHARD_ID FROM T1;

C1 CLUSTER_SHARD_ID
-- ----------------
A                14
B                17
C                 4

3 rows selected.
```

<a id="d29f6a18210af1b8"></a>
### Compatibility

The SQL standard compatibility for pseudo column is as follows.

**SQL standard compatibility for pseudo column**

<a id="5162254e763fb9cb"></a>
<table><tbody><tr><th align="center">&nbsp;Feature ID</th><th align="center">&nbsp;Description</th><th align="center">&nbsp;Availability</th></tr><tr><td align="left">T176</td><td align="left">Sequence generator support</td><td align="center">O</td></tr><tr><td align="left">T177</td><td align="left">&nbsp;Sequence generator support: simple restart option</td><td align="center">O</td></tr></tbody></table>

<a id="e1cc6b31a2601cec"></a>
## Operators

An operator is represented by one or more specific symbols or keywords, and it performs an operation using one or more arguments.

The operator types are various as follows.  
• Arithmetic operator  
• Concatenation operator  
• Set operator

<a id="884c4f1b147de77c"></a>
### Arithmetic Operator

<a id="df3d3dc2a5ad487c"></a>
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

<a id="64893c9d9f3240bd"></a>
#### Description

An arithmetic operator performs an arithmetic operation of the numeric types, date/time types or interval types.

The arithmetic operator precedence is as follows.

1. [+ (POSITIVE)](17-built-in-function-references.md#0ad5e2857b9bf32a), [- (NEGATIVE)](17-built-in-function-references.md#feb96ef9f9abe06f)
2. [* (MULTIPLICATION)](17-built-in-function-references.md#827484d83904b881), [/ (DIVISION)](17-built-in-function-references.md#7144049f41367f01)
3. [+ (ADDITION)](17-built-in-function-references.md#2b173b26816d57c1), [- (SUBTRACTION)](17-built-in-function-references.md#ccd72d1a1fab918e)

<a id="16aa497bbae9b50a"></a>
### Concatenation Operator

<a id="3de383bac71fb965"></a>
#### Syntax

```
<concatenation operator> ::=
        <expression> || <expression>
```

<a id="6b8b7bf20ae25414"></a>
#### Description

A concatenation operator returns strings which connect between values of CHARACTER STRING type or BINARY STRING type.  
For more information, refer to [|| (CONCATENATE)](17-built-in-function-references.md#3274505dd6136d12), [CONCATENATE](17-built-in-function-references.md#2b2d8c3da5454602).

<a id="b645761c4acdbc2f"></a>
### Set Operator

<a id="3e7695f321c07f86"></a>
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

<a id="a0fec60643f5ec14"></a>
#### Description

[set operator](20-sql-references-h-z.md#fcd983bb04411568) performs a set operation of the subquery results.

INTERSECT ALL/DISTINCT has a higher precedence than other set operators.

**Set operators**

<a id="0e7b6e386bfc1905"></a>
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

<a id="c47f64dba4c7dc4e"></a>
### Compatibility

The SQL standard compatibility for operator is as follows.

**SQL standard compatibility for operator**

<a id="6afcff68bcdb9e9f"></a>
<table><tbody><tr><th align="center">&nbsp;Feature ID</th><th align="center">&nbsp;Description</th><th align="center">&nbsp;Availability</th></tr><tr><td align="left" valign="middle">E011-04</td><td align="left" valign="middle">Arithmetic operators</td><td align="center" valign="middle">O</td></tr><tr><td valign="middle">E021-07</td><td valign="middle">Character concatenation</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-01</td><td align="left" valign="middle">UNION DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-02</td><td align="left" valign="middle">UNION ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-03</td><td align="left" valign="middle">&nbsp;EXCEPT DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-05</td><td align="left" valign="middle">Columns combined via table operators need not have exactly the same data type</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-06</td><td align="left" valign="middle">Table operators in subqueries</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F041-08</td><td align="left" valign="middle">All comparison operators are supported (rather than just =)</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F302-01</td><td align="left" valign="middle">&nbsp;INTERSECT DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F302-02</td><td align="left" valign="middle">INTERSECT ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F304</td><td align="left" valign="middle">&nbsp;EXCEPT ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F846</td><td align="left" valign="middle">Octet support in regular expression operators</td><td align="center" valign="middle">X</td></tr><tr><td align="left" valign="middle">J571</td><td align="left" valign="middle">NEW operator</td><td align="center" valign="middle">X</td></tr></tbody></table>

<a id="a7e7ad935e284511"></a>
## Functions

Functions and operators are similar in features. However, to represent arguments, functions use parentheses after its name. A function can have zero or more arguments.

The function has two types as follows.  
.• Single row function  
• Aggregate function

<a id="3933ae3a2bef6316"></a>
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

<a id="0f61bc20bc7a048a"></a>
#### Numeric Functions

A numeric value is input in numeric function, and the numeric function returns a numeric result.

For more information about the numeric function types, refer to the followings.

- [ABS](17-built-in-function-references.md#8d66550ee768794c)
- [ACOS](17-built-in-function-references.md#76e5689696dd8c07)
- [ASIN](17-built-in-function-references.md#8ba6d7d603750dca)
- [ATAN](17-built-in-function-references.md#634cd71621ac85aa)
- [ATAN2](17-built-in-function-references.md#8cca65d5dd5349a8)
- [BITAND](17-built-in-function-references.md#83cc3df86bdca709)
- [BITNOT](17-built-in-function-references.md#55802fa58df7e2d1)
- [BITOR](17-built-in-function-references.md#470026b2b34b56c1)
- [BITXOR](17-built-in-function-references.md#79ca9cf7ca575a45)
- [CBRT](17-built-in-function-references.md#fae5e1eced2d11ae)
- [CEIL](17-built-in-function-references.md#c8ec8bc78684cdab)
- [COS](17-built-in-function-references.md#44e107982215212f)
- [COT](17-built-in-function-references.md#70bf5c99a8ec5af4)
- [DEGREES](17-built-in-function-references.md#1a2ad0a79787fcfe)
- [EXP](17-built-in-function-references.md#2600fc31f0747d3e)
- [FACTORIAL](17-built-in-function-references.md#a2d53e1ef16df5f7)
- [FLOOR](17-built-in-function-references.md#7c53322abec2bc64)
- [LN](17-built-in-function-references.md#b3ddb38bb17446b4)
- [LOG](17-built-in-function-references.md#528a94c43f2c58d6)
- [MOD](17-built-in-function-references.md#7fc24b7bac9976ff)
- [PI](17-built-in-function-references.md#3d3110750adc751c)
- [POWER](17-built-in-function-references.md#efeb6aa68624102e)
- [RADIANS](17-built-in-function-references.md#421e4f438006e135)
- [RANDOM](17-built-in-function-references.md#cd712f3846834401)
- [ROUND( number )](17-built-in-function-references.md#3ab0595bd4ce828e)
- [SHARD_ID](17-built-in-function-references.md#0db7e14f9f0752f5)
- [SHIFT_LEFT](17-built-in-function-references.md#e78ae9de2914e02b)
- [SHIFT_RIGHT](17-built-in-function-references.md#84d8bc7d6307366d)
- [SIGN](17-built-in-function-references.md#5000551fa54ad54d)
- [SIN](17-built-in-function-references.md#8efad287dc9c3384)
- [SQRT](17-built-in-function-references.md#da1f1343e315a450)
- [TAN](17-built-in-function-references.md#4cd5bf99ebf3d145)
- [TRUNC( number )](17-built-in-function-references.md#732613ba550860fa)
- [WIDTH_BUCKET](17-built-in-function-references.md#9f15275ef5f64ced)

<a id="c471a1d785c99caa"></a>
#### Character String Functions Returning Character Values

A character string type value is input in character string functions returning character values, and the function returns the result of character string type.

For more information about character string functions returning character values types, refer to the followings.

- [CHR](17-built-in-function-references.md#6b1af6a08a64f12c)
- [CONCAT](17-built-in-function-references.md#0fb0770183ef9ff9)
- [CONCATENATE](17-built-in-function-references.md#2b2d8c3da5454602)
- [INITCAP](17-built-in-function-references.md#7507e2de61737b03)
- [LOWER](17-built-in-function-references.md#40f49752a8d3215b)
- [LPAD](17-built-in-function-references.md#d4db89e4b4fa9cb6)
- [LTRIM](17-built-in-function-references.md#1b3ee0e257f64ca0)
- [OVERLAY](17-built-in-function-references.md#5d0b15a953c1001d)
- [REPEAT](17-built-in-function-references.md#604648789df3963a)
- [REPLACE](17-built-in-function-references.md#755b9c738c2de01a)
- [REVERSE](17-built-in-function-references.md#79d84a4c72d71d48)
- [RPAD](17-built-in-function-references.md#7059ecaea6a50fc6)
- [RTRIM](17-built-in-function-references.md#8d9dbe696deed1af)
- [SPLIT_PART](17-built-in-function-references.md#55771b527f4910fe)
- [SUBSTR](17-built-in-function-references.md#886c495b271eb0db)
- [SUBSTRB](17-built-in-function-references.md#0fa2064ee0a68d30)
- [TRANSLATE](17-built-in-function-references.md#2ea59d7dc8a38b63)
- [TRIM](17-built-in-function-references.md#d56383e8219aa445)
- [UPPER](17-built-in-function-references.md#51fcdd62ab430f53)

<a id="eb1b6c64f4dca069"></a>
#### Character String Functions Returning Number Values

A character string type value is input in character string functions returning number values the value, and the function returns the result of number type.

For more information about character string functions returning number values types, refer to the followings.

- [ASCII](17-built-in-function-references.md#2258ae3f25cf26a4)
- [BIT_LENGTH](17-built-in-function-references.md#61bd92563542bb9a)
- [BYTE_LENGTH](17-built-in-function-references.md#076781007f6d69e0)
- [CHAR_LENGTH](17-built-in-function-references.md#a1c40efd346b484f)
- [INSTR](17-built-in-function-references.md#5dc08606e256048e)
- [LENGTH](17-built-in-function-references.md#0429eb6207fb17d4)
- [LENGTHB](17-built-in-function-references.md#47f3cf241a8776e8)
- [OCTET_LENGTH](17-built-in-function-references.md#67879be1522706a0)
- [POSITION](17-built-in-function-references.md#c4398d0f2ff636ac)

<a id="8ec9f2164f31e0ea"></a>
#### Datetime Functions

The value of date/time/timestamp/interval type is input in datetime function, and the function returns the result of date/time/timestamp/interval type.

For more information about datetime functions types, refer to the followings.

- [ADDDATE](17-built-in-function-references.md#927624817574e79b)
- [ADDTIME](17-built-in-function-references.md#3a34762e4fa8c807)
- [ADD_MONTHS](17-built-in-function-references.md#4078b2e3840b6cf6)
- [DATEADD](17-built-in-function-references.md#73bc4e5a0097453e)
- [DATEDIFF](17-built-in-function-references.md#952b4d199f5f9ff9)
- [DATE_ADD](17-built-in-function-references.md#c7d0d65ec40263a8)
- [DATE_PART](17-built-in-function-references.md#ca1f53ceaf11d028)
- [EXTRACT](17-built-in-function-references.md#c864a50524616031)
- [FROM_TZ](17-built-in-function-references.md#e364ff079d11e90d)
- [LAST_DAY](17-built-in-function-references.md#04b60c5de4f07e66)
- [MONTHS_BETWEEN](17-built-in-function-references.md#259bdca28b32e0a2)

<a id="3705621d8afb2d89"></a>
#### General Comparison Functions

General comparison function returns a minimum value or a maximum value for the value set.

For more information about general comparison function types, refer to the followings.

- [GREATEST](17-built-in-function-references.md#e133acf2a0699694)
- [LEAST](17-built-in-function-references.md#2f641928d02d76a5)

<a id="859be6abf928b279"></a>
#### Conversion Functions

Conversion function sets the value of a particular data type.

For more information about conversion function types, refer to the followings.

- [NUMTODSINTERVAL](17-built-in-function-references.md#310abb57145bd678)
- [NUMTOYMINTERVAL](17-built-in-function-references.md#d608b1cd886ee7b6)
- [TO_CHAR( datetime )](17-built-in-function-references.md#24c99d6f3463acf6)
- [TO_CHAR( number )](17-built-in-function-references.md#d69061b89662a768)
- [TO_DATE](17-built-in-function-references.md#5219142a4793653b)
- [TO_NATIVE_BIGINT](17-built-in-function-references.md#4e932440d0c38f36)
- [TO_NATIVE_DOUBLE](17-built-in-function-references.md#54731f33ec124462)
- [TO_NATIVE_INTEGER](17-built-in-function-references.md#8e984895b0d5abb0)
- [TO_NATIVE_REAL](17-built-in-function-references.md#ae266ee6179f808b)
- [TO_NATIVE_SMALLINT](17-built-in-function-references.md#898732df4fa8a0cf)
- [TO_NUMBER](17-built-in-function-references.md#f4c5f4089516a8f7)
- [TO_TIME](17-built-in-function-references.md#9dbf37dc5504a5f2)
- [TO_TIME_TZ](17-built-in-function-references.md#8cd8fe4291df2b52)
- [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#a7774652486ae49f)
- [TO_TIMESTAMP](17-built-in-function-references.md#4343ab929dac120a)
- [TO_TIMESTAMP_TZ](17-built-in-function-references.md#a94ee05b9240c010)
- [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#19ac77096078990f)

<a id="3010ca28e36c2980"></a>
#### Conditional Functions

Conditional function returns a result of specific value depending on a condition.

For more information about conditional function types, refer to the followings.

- [CASE2](17-built-in-function-references.md#59eec3a092621013)
- [DECODE](17-built-in-function-references.md#c9a93572129b7213)

<a id="e3ad44a939f7be24"></a>
#### NULL-related Functions

NULL-related function returns a result of specific value depending on whether the input value is a NULL value.

For more information about null-related function types, refer to the followings.

- [COALESCE](17-built-in-function-references.md#9721055bac9c198a)
- [NULLIF](17-built-in-function-references.md#66e124ffb2b38351)
- [NVL](17-built-in-function-references.md#20e1ecd24c4856cf)
- [NVL2](17-built-in-function-references.md#b768727f6ab40534)

<a id="6a6d19f960a479a3"></a>
#### ROWID-related Functions

ROWID-related function is used to obtain information about the ROWID.

For more information about ROWID-related function types, refer to the followings.

- Valid functions in stand-alone
    - [ROWID_OBJECT_ID](17-built-in-function-references.md#aa8c6a3fe47fcbe2)
    - [ROWID_TABLESPACE_ID](17-built-in-function-references.md#e5a780cb2a304400)
    - [ROWID_PAGE_ID](17-built-in-function-references.md#a1c13291e9855322)
    - [ROWID_ROW_NUMBER](17-built-in-function-references.md#ecadd414bf9ba38e)

- Valid functions in cluster
    - [ROWID_GRID_BLOCK_ID](17-built-in-function-references.md#40b57d72048c57a1)
    - [ROWID_GRID_BLOCK_SEQ](17-built-in-function-references.md#acd18388ff477cf5)
    - [ROWID_MEMBER_ID](17-built-in-function-references.md#ff85dc18c2d0624a)
    - [ROWID_SHARD_ID](17-built-in-function-references.md#3b00c98aa6983e82)

<a id="e62120012f75467a"></a>
#### Encryption Functions

encryption function encrypts, decrypts, or hashes the given plain text by using the specific algorithm, then returns the result.

The types of encryption functions are as follows.

- [DIGEST](17-built-in-function-references.md#ba37ba1671acbc26)
- [HASH32](17-built-in-function-references.md#bf45ca2b2bcf6736)

<a id="8aa71f7a2377c1bc"></a>
#### System Information Functions

System information function is used to obtain information about sessions and the system.

For more information about system information function type, refer to the followings.

- [CLOCK_DATE](17-built-in-function-references.md#0d949b2a5285a138)
- [CLOCK_LOCALTIME](17-built-in-function-references.md#c6e7f72490b40439)
- [CLOCK_LOCALTIMESTAMP](17-built-in-function-references.md#5d29175d1ef4d164)
- [CURRENT_CATALOG](17-built-in-function-references.md#3576503a05e8089a)
- [CURRENT_DATE](17-built-in-function-references.md#11de16d40aab5ff8)
- [CURRENT_SCHEMA](17-built-in-function-references.md#9fd74f8eacd46a81)
- [CURRENT_TIME](17-built-in-function-references.md#3138931fb3264137)
- [CURRENT_TIMESTAMP](17-built-in-function-references.md#de1fe20a9404482d)
- [CURRENT_USER](17-built-in-function-references.md#222009ae9a551fee)
- [LAST_IDENTITY_VALUE](17-built-in-function-references.md#e5492376ea4f8fe9)
- [LOCALTIME](17-built-in-function-references.md#f87ec03dde9b2802)
- [LOCALTIMESTAMP](17-built-in-function-references.md#f60256001d044f94)
- [LOGON_USER](17-built-in-function-references.md#163d031127d7fd13)
- [SESSION_ID](17-built-in-function-references.md#c4807e7f5dc63075)
- [SESSION_SERIAL](17-built-in-function-references.md#d9b48a25605c605d)
- [SESSION_USER](17-built-in-function-references.md#050d5bbebf1a1f99)
- [SESSIONTIMEZONE](17-built-in-function-references.md#464fac99a9ce4f64)
- [STATEMENT_DATE](17-built-in-function-references.md#72245005377e3513)
- [STATEMENT_LOCALTIME](17-built-in-function-references.md#53c3b60ca5d08a42)
- [STATEMENT_LOCALTIMESTAMP](17-built-in-function-references.md#5583fa5e4241b577)
- [STATEMENT_TIME](17-built-in-function-references.md#2ffed6aa412db546)
- [STATEMENT_TIMESTAMP](17-built-in-function-references.md#ef98a5f0a9976e38)
- [STATEMENT_VIEW_SCN](17-built-in-function-references.md#81bbdc72826b938f)
- [SYSDATE](17-built-in-function-references.md#1c9c8cb0e5a7b7f2)
- [SYSTIME](17-built-in-function-references.md#c3006d12a5a804cd)
- [SYSTIMESTAMP](17-built-in-function-references.md#1e392924dc96ef60)
- [TRANSACTION_DATE](17-built-in-function-references.md#64c95a5834e1602a)
- [TRANSACTION_LOCALTIME](17-built-in-function-references.md#fe7eedefbda66b67)
- [TRANSACTION_LOCALTIMESTAMP](17-built-in-function-references.md#71272c35f4421ff2)
- [TRANSACTION_TIME](17-built-in-function-references.md#c4743da8577b330c)
- [TRANSACTION_TIMESTAMP](17-built-in-function-references.md#8919352379027e52)
- [USER_ID](17-built-in-function-references.md#eebb6e9fa249c7f5)
- [VERSION](17-built-in-function-references.md#4c4cf16c3fb15e3f)

<a id="95bfb0a454bd6b9b"></a>
### Aggregate Function

Aggregate function creates a single result row for multiple rows.

For more information about aggregate function types, refer to the followings.

- [COUNT](17-built-in-function-references.md#359fda9bb485db91)
- [COUNT(*)](17-built-in-function-references.md#690facf6ba5fe621)
- [SUM](17-built-in-function-references.md#ecc19ff5aa9f5e17)
- [AVG](17-built-in-function-references.md#1650d73d263c108c)
- [MIN](17-built-in-function-references.md#a8402ad42933c631)
- [MAX](17-built-in-function-references.md#240d07ce2ffb63f8)
- [STDDEV](17-built-in-function-references.md#c73c3f8884cc1c52)
- [STDDEV_POP](17-built-in-function-references.md#fb8d9eee7b4e7dab)
- [STDDEV_SAMP](17-built-in-function-references.md#528412563eda78a1)
- [VAR_POP](17-built-in-function-references.md#c0a67a48fe1cb8c7)
- [VAR_SAMP](17-built-in-function-references.md#bb45fcc7dcf1c737)
- [VARIANCE](17-built-in-function-references.md#aece5460fa03ff1f)

<a id="5e0cdfb173eec832"></a>
### Window Function

It returns the result of the function for the defined record range.

The defined record range is called as a window, and the execution range is defined in OVER &lt;window name or specification&gt;.

For more information about the window, refer to [window clause](20-sql-references-h-z.md#6de1c122457d94b3).

Each record within the group has the result of executing the window function for the window (defined range). Therefore, unlike aggregate function, the window function returns multiple records for each group.

The window function is available in *select list* and *order by* clause.

Window functions are as follows.

- [AVG() OVER](17-built-in-function-references.md#692d399e54ef6e8c)
- [CORR() OVER](17-built-in-function-references.md#05b0c5c0b1ca1211)
- [COUNT() OVER](17-built-in-function-references.md#ba1b291cb1104884)
- [COUNT(*) OVER](17-built-in-function-references.md#9fe1ec2cf19c17bf)
- [COVAR_POP() OVER](17-built-in-function-references.md#af6dd5612064fb6a)
- [COVAR_SAMP() OVER](17-built-in-function-references.md#65c53271a2251f83)
- [CUME_DIST() OVER](17-built-in-function-references.md#d269bdbb3864419a)
- [DENSE_RANK() OVER](17-built-in-function-references.md#3b285dd4138efd6c)
- [FIRST() OVER](17-built-in-function-references.md#3ea9b3192ce39867)
- [FIRST_VALUE() OVER](17-built-in-function-references.md#ff8ac9584af26954)
- [LAG() OVER](17-built-in-function-references.md#af864d941533e203)
- [LAST() OVER](17-built-in-function-references.md#e241a2d11f0602c4)
- [LAST_VALUE() OVER](17-built-in-function-references.md#65e774a52e3bfa7d)
- [LEAD() OVER](17-built-in-function-references.md#5292f627db30261d)
- [LISTAGG() OVER](17-built-in-function-references.md#3f9e7bee2e2910a1)
- [MAX() OVER](17-built-in-function-references.md#c73e0fb020dfe7b8)
- [MEDIAN() OVER](17-built-in-function-references.md#5cb6f7689a212ef4)
- [MIN() OVER](17-built-in-function-references.md#0c0c1f53bd41f8ab)
- [NTH_VALUE() OVER](17-built-in-function-references.md#b2f2bcf02228e81c)
- [NTILE() OVER](17-built-in-function-references.md#8f290d2d1cbce99c)
- [PERCENT_RANK() OVER](17-built-in-function-references.md#7408d6ee5a3c57ed)
- [PERCENTILE_CONT() OVER](17-built-in-function-references.md#4093af94bd47f734)
- [PERCENTILE_DISC() OVER](17-built-in-function-references.md#890f430d60a92678)
- [RANK() OVER](17-built-in-function-references.md#5455eeaa6bf1b5d8)
- [RATIO_TO_REPORT() OVER](17-built-in-function-references.md#8eec06f9d7726364)
- [REGR_AVGX() OVER](17-built-in-function-references.md#edbb2307f5157566)
- [REGR_AVGY() OVER](17-built-in-function-references.md#0fbb6375923ea6fd)
- [REGR_COUNT() OVER](17-built-in-function-references.md#c1fa8b8a38eaf7c9)
- [REGR_INTERCEPT() OVER](17-built-in-function-references.md#73813dcaa4b54a79)
- [REGR_R2() OVER](17-built-in-function-references.md#574d3fc5b731769b)
- [REGR_SLOPE() OVER](17-built-in-function-references.md#a663cb7403064411)
- [REGR_SXX() OVER](17-built-in-function-references.md#94fc9a4442b883f2)
- [REGR_SXY() OVER](17-built-in-function-references.md#84aade9f2316e893)
- [REGR_SYY() OVER](17-built-in-function-references.md#be007e5a648ff0e4)
- [ROW_NUMBER() OVER](17-built-in-function-references.md#d582894215e065dd)
- [STDDEV() OVER](17-built-in-function-references.md#c72f226331baf318)
- [STDDEV_POP() OVER](17-built-in-function-references.md#ec58e43f967f0194)
- [STDDEV_SAMP() OVER](17-built-in-function-references.md#de4132b2ac197f6c)
- [STRING_AGG() OVER](17-built-in-function-references.md#6afb9e95275724c3)
- [SUM() OVER](17-built-in-function-references.md#a3a8a6b2497fd1c2) 
- [VAR_POP() OVER](17-built-in-function-references.md#a93fdf603939c4e1)
- [VAR_SAMP() OVER](17-built-in-function-references.md#8fd647cd7085750a)
- [VARIANCE() OVER](17-built-in-function-references.md#76a32c257963857c)

<a id="068e3ef3c3d506d4"></a>
### Compatibility

The SQL standard compatibility for function is as follows.

**SQL standard compatibility for function**

<a id="9eb18d6f312d5e8d"></a>
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
| F441 | Extended set function support | O |
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
| T321-01 | User-defined functions with no overloading | O |
| T326 | Table functions | X |
| T341 | Overloading of SQL-invoked functions and SQL-invoked procedures | X |
| T433 | Multiargument GROUPING function | X |
| T441 | ABS and MOD functions | O |
| T571 | Array-returning external SQL-invoked functions | X |
| T572 | Multiset-returning external SQL-invoked functions | X |
| T581 | Regular expression substring function | X |
| T614 | NTILE function | O |
| T615 | LEAD and LAG functions | O |
| T616 | Null treatment option for LEAD and LAG functions | O |
| T617 | FIRST_VALUE and LAST_VALUE functions | O |
| T618 | NTH_VALUE function | O |
| T619 | Nested window functions | X |
| T621 | Enhanced numeric functions | O |

<a id="d509ae5b9f752c9a"></a>
## Conditions

<a id="157b5403c733cf29"></a>
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
• Distinct condition

**Condition precedence**

<a id="115391f7241ef313"></a>
| Precedence | Condition type |
| --- | --- |
| 1 | Operators in condition clauses |
| 2 | =, !=, &lt;, &gt;, &lt;=, &gt;= |
| 3 | IS [NOT] NULL, [NOT] BETWEEN,  [NOT] IN,  LIKE, EXISTS, IS [NOT] DISTINCT FROM |
| 4 | NOT |
| 5 | AND |
| 6 | OR |

<a id="276df7842abc5fa7"></a>
### Comparison Conditions

It compares both conditional expressions, and returns the boolean type of TRUE, FALSE, UNKNOWN values.

**Comparison conditions**

<a id="750d5c9d5423b545"></a>
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

For more information, refer to [Type Comparison](#74108eb6d21a543c).

<a id="f9ba661f6c72f37c"></a>
#### &lt; Simple Comparison Conditions &gt;

<a id="efb0f020f07508d2"></a>
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

For more information, refer to [Scalar Subquery Expression](#80f1dc3bba65909c).

<a id="d74b3bbe9a5ddeee"></a>
##### Description

If the expr list or subquery comes to both left and right of comparison_operator, then the number of expr or subquery target to be compared should be same.  
If there is a subquery, the number of result records should be one.

<a id="0d69ab34536225c5"></a>
##### Example

**Example of simple comparison conditions**

<a id="5eded02e55d0177b"></a>
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

<a id="1b863bfa01f24d47"></a>
#### &lt;Group Comparison Conditions&gt;

<a id="4892cb9483691a9a"></a>
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

For more information, refer to [Scalar Subquery Expression](#80f1dc3bba65909c).

<a id="fdf571d5b258a381"></a>
##### Description

If the expr list or subquery comes to both left and right of comparison_operator, then the number of expr or subquery target to be compared should be same.  
If a subquery comes to the left of comparison_operator, the number of result records should be one.  
If a subquery comes to the right of comparison_operator, the number of result records can be multiple.

<a id="07e27b4c18f11399"></a>
##### Example

<a id="cc12e8058151eaa6"></a>
<table class="table column_count_2"><caption>Example of group comparison conditions</caption><thead><tr><th class="to_center"><div>Conditional expression</div></th><th class="to_center"><div>Result</div></th></tr></thead><tbody><tr><td><div>1 =any ( 1, 2, 3, 4, 5 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>1 =any ( 1, 2, null, 4, 5 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>1 =any ( 2, null, 4, 5 )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td><div>1 =any ( 100, 2, 3, 4, 5 )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td><div>1 =all ( 1, +1, 1E+0 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>1 =all ( 1, +1, 1E+0, null )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td><div>1 =all ( 1, 2, 3, 4, 5 )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td><div>( 1, 2 ) =any ( ( 0, 1 ), ( 1, 2 ), ( 3, 4 ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>( 1, 2 ) =any ( ( 0, 1 ), ( 1, 2 ), ( null, null ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>( 1, 2 ) =any ( ( 0, 1 ), ( 2, 3 ), ( 3, 4 ) )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td><div>( 1, 2 ) =all ( ( 1, 2 ), ( +1, +2 ), ( 1E+0, 2E+0 ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>( 1, 2 ) =all ( ( 1, 2 ), ( +1, +2 ), ( null, null ) )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td><div>( 1, 2 ) =all ( ( 0, 1 ), ( 2, 3 ), ( 3, 4 ) )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><th colspan="2"><div>When the result record of comparison_operator's right subquery is 0</div></th></tr><tr><td><div>( 'X' ) =any ( select dummy from dual where dummy = 'Y' )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td><div>( 'X' ) =all ( select dummy from dual where dummy = 'Y' )</div></td><td class="to_left"><div>TRUE</div></td></tr></tbody></table>

<a id="c594f9959205c510"></a>
### Logical Conditions

Logical conditions are such as AND, OR, NOT.

<a id="a2e5c2284a30caa3"></a>
#### AND

<a id="a514600bab8647fa"></a>
##### Syntax

```
<boolean value expression> AND <boolean value expression>
```

<a id="681d5d2a4f6f31c3"></a>
##### Description

**Truth table of AND boolean operator**

<a id="241ec26f4c2926f8"></a>
| AND | True | False | Unknown |
| --- | --- | --- | --- |
| True | True | False | Unknown |
| False | False | False | False |
| Unknown | Unknown | False | Unknown |

<a id="792cada6e9c5f4e1"></a>
#### OR

<a id="1cea69a608dd1c40"></a>
##### Syntax

```
<boolean value expression> OR <boolean value expression>
```

<a id="c9bb8414a7c834d3"></a>
##### Description

**Truth table of OR boolean operator**

<a id="438a2a21fa22b024"></a>
| OR | True | False | Unknown |
| --- | --- | --- | --- |
| True | True | True | True |
| False | True | False | Unknown |
| Unknown | True | Unknown | Unknown |

<a id="9f3aa2f6c81a120e"></a>
#### NOT

<a id="8f3125600e6dc03b"></a>
##### Syntax

```
NOT <boolean value expression>
```

<a id="02c368dfb64adce8"></a>
##### Description

**Truth table of NOT boolean operator**

<a id="5df6bea78daba371"></a>
| expr | NOT |
| --- | --- |
| True | False |
| False | True |
| Unknown | Unknown |

<a id="14162074b62021ee"></a>
### Null Condition

<a id="9403ce6a66b875f3"></a>
#### Syntax

```
<expr> IS [NOT] NULL
```

<a id="4d487e9fd7b9ee43"></a>
#### Description

It checks whether the result value of expr is NULL.

**Result table of IS NULL condition**

<a id="6c312c0f15d756b9"></a>
| expr | IS NULL | IS NOT NULL |
| --- | --- | --- |
| NULL | True | False |
| NOT NULL | False | True |

<a id="04a1c6beb2e42aef"></a>
### Compound Conditions

It is a conditional expression in which multiple conditions are combined.

```
compound_condition ::=
        ( condition )
      | NOT condition
      | condition < AND | OR > condition
```

<a id="1def3558437befef"></a>
### Pattern-matching Conditions

<a id="18d8e59b0ea281e3"></a>
#### Like Condition

<a id="b961226ec09b16ca"></a>
##### Syntax

```
like_condition ::=
        string [NOT] LIKE pattern [ ESCAPE escape_character ]
```

<a id="605f08ada1f7964d"></a>
##### Description

It checks if a string matches the specified pattern.

Arguments such as string, pattern, escape_character can be of a character type such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or of the type which is available to be converted to a character type.  
If string, pattern, escape_character are NULL, it returns NULL.

If escape_character is omitted, there is not a default value.  
If escape_character is specified, the escape_character should be one character.

If pattern does not include '_' nor '%', it is processed in the same way as equal operation(string = pattern).  
If pattern includes '_'  or '%', the string checks if it matches as follows.  
• '_': If it corresponds to one arbitrary character.  
• '%': If it corresponds to the arbitrary character string which has zero or more characters.

Use ESCAPE syntax to compare '_' or '%' included in the pattern with characters.   
Specify escape_character, and describe the specified escape_character before the pattern's '_' or '%'.

<a id="f723196df93d4bee"></a>
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

<a id="9c4735e58e05831a"></a>
### BETWEEN Condition

<a id="319f72c0b5b45090"></a>
#### Syntax

```
<between condition> ::=
   <expr1> [ NOT ] BETWEEN [ ASYMMETRIC | SYMMETRIC ] <expr2> AND <expr3>
```

<a id="1306b968c00217d5"></a>
#### Description

It checks whether expr1 is within the range between expr2 and expr3.

If ASYMMETRIC or SYMMETRIC is omitted, the default is ASYMMETRIC.  
If data types among expr1, expr2, expr3 are different, they are converted.   
For more information, refer to [Type Comparison](#74108eb6d21a543c), [Type Conversion](#935e2183d0c42aa6).

**Equivalence of between conditions**

<a id="6bce722841bdec71"></a>
| A | B |
| --- | --- |
| X BETWEEN ASYMMETRIC Y AND Z | X BETWEEN Y AND Z |
| X BETWEEN Y AND Z | X >= Y AND X <= Z |
| X NOT BETWEEN Y AND Z | NOT( X BETWEEN Y AND Z ) |
| X BETWEEN SYMMETRIC Y AND Z | ((X BETWEEN Y AND Z) OR (X BETWEEN Z AND Y) |
| X NOT BETWEEN SYMMETRIC Y AND Z | NOT( X BETWEEN SYMMETRIC Y AND Z ) |

<a id="c97b550b0aab7e08"></a>
#### Example

<a id="13169f2294c03fb2"></a>
<table class="table column_count_3"><caption>Example of between condition</caption><thead><tr><th class="to_center" colspan="2"><div>Conditional expression</div></th><th class="to_center"><div>Result</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>BETWEEN [ ASYMMETRIC ]</div></td><td class="to_middle"><div>3 BETWEEN 1 AND 5</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr><tr><td class="to_middle"><div>NULL BETWEEN 1 AND 5
3 BETWEEN NULL AND 5
3 BETWEEN 1 AND NULL</div></td><td class="to_left to_middle"><div>NULL</div></td></tr><tr><td class="to_middle"><div>3 BETWEEN 5 AND 1</div></td><td class="to_left to_middle"><div>FALSE</div></td></tr><tr><td class="to_middle" rowspan="3"><div>BETWEEN SYMMETRIC</div></td><td class="to_middle"><div>3 BETWEEN SYMMETRIC 1 AND 5</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr><tr><td class="to_middle"><div>NULL BETWEEN SYMMETRIC 1 AND 5
3 BETWEEN SYMMETRIC NULL AND 5
3 BETWEEN SYMMETRIC 1 AND NULL</div></td><td class="to_left to_middle"><div>NULL</div></td></tr><tr><td class="to_middle"><div>3 BETWEEN SYMMETRIC 5 AND 1</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr></tbody></table>

<a id="7b53b3eb98047687"></a>
### IN Condition

<a id="3024132c02d5706b"></a>
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

<a id="c300f379d15d1af9"></a>
#### Description

In condition returns the same result as = ANY.  
NOT IN condition returns the same result as !=ALL.

For more information, refer to [Comparison Conditions](#276df7842abc5fa7).

<a id="754c1a9761ae166d"></a>
#### Example

**Example of IN condition**

<a id="6c020b8c6aa7baa6"></a>
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

<a id="d51c6a30d7d8cc74"></a>
### EXISTS Condition

<a id="202be962779e0585"></a>
#### Syntax

```
exists_conditions ::= 
        EXISTS ( subquery )
```

<a id="df7f4e666c9a8a08"></a>
#### Description

It checks whether the result record of subquery exists.   
If the result record of subquery exists, it returns TRUE. Otherwise, it returns FALSE.

<a id="abd3023253bef788"></a>
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

<a id="7790b87414ab1367"></a>
### DISTINCT Condition

<a id="7d359d7238555fa8"></a>
#### Syntax

```
distinct_conditions ::= 
        <expr> IS [NOT] DISTINCT FROM <expr>
      | ( <expr_list> ) IS [NOT] DISTINCT FROM ( <expr_list> )
```

<a id="e5d421eb28b49546"></a>
#### Description

The operand type of distinct condition should be comparable one another.  
If the operand is &lt;expr_list&gt;, then the data in the same position becomes the comparison target.

If all operands of distinct condition is not null value,  
*is distinct from* is as same as *not equal(!=)*,  
*is not distinct from* returns the same result of when it is *eqaul(=)*.

DISTINCT condition processes NULL value as a general data instead of unknown, and this is what is different from other comparing operators.

- IS DISTINCT FROM
    - If all operands are NULL
        - NULL is distinct from NULL => FALSE
    - If one of the operand is NULL
        - NULL is distinct from 1 => TRUE
        - 1 is distinct from NULL => TRUE
    - If all operands are not NULL
        - 1 is distinct from 1 => FALSE
        - 1 is distinct from 2 => TRUE
    - If the operand is &lt;expr_list&gt;
        - ( 1, 2, 3 ) is distinct from ( 1, 2, 3 ) => FALSE
        - ( 1, 2, 3 ) is distinct from ( 1, 3, 3 ) => TRUE
        - ( 1, 2, 3 ) is distinct from ( 4, 5, 6 ) => TRUE

- IS NOT DISTINCT FROM
    - If all operands are NULL
        - NULL is not distinct from NULL => TRUE
    - If one of the operand is NULL
        - NULL is not distinct from 1 => FALSE
        - 1 is not distinct from NULL => FALSE
    - If all operands are not NULL
        - 1 is not distinct from 1 => TRUE
        - 1 is not distinct from 2 => FALSE
    - If the operand is &lt;expr_list&gt;
        - ( 1, 2, 3 ) is not distinct from ( 1, 2, 3 ) => TRUE
        - ( 1, 2, 3 ) is not distinct from ( 1, 3, 3 ) => FALSE
        - ( 1, 2, 3 ) is not distinct from ( 4, 5, 6 ) => FALSE

<a id="55c4509d0478c538"></a>
#### Example

```
* IS DISTINCT FROM

gSQL>
SELECT i1,
       i2,
       i1 IS DISTINCT FROM i2 AS IsDistinct
  FROM t1; 

  I1   I2 ISDISTINCT
---- ---- ----------
   1 null TRUE      
   1    1 FALSE     
   1    2 TRUE      
null null FALSE     
null    1 TRUE      
null    2 TRUE      

6 rows selected.

gSQL> 
SELECT i1,
       i2,
       i3,
       ( I1, I2, I3 ) IS DISTINCT FROM ( 1, 1, 1 ) AS RESULT 
  FROM t1;

  I1   I2   I3 RESULT
---- ---- ---- ------
   1    1    1 FALSE 
   2 null    3 TRUE  
null null null TRUE  

3 rows selected.


* IS NOT DISTINCT FROM

gSQL>
SELECT i1,
       i2,
       i1 IS NOT DISTINCT FROM i2 AS IsNotDistinct 
  FROM t1; 

  I1   I2 ISNOTDISTINCT
---- ---- -------------
   1 null FALSE        
   1    1 TRUE         
   1    2 FALSE        
null null TRUE         
null    1 FALSE        
null    2 FALSE        

6 rows selected.

gSQL> 
SELECT i1,
       i2,
       i3,
       ( I1, I2, I3 ) IS NOT DISTINCT FROM ( 1, 1, 1 ) AS RESULT
 FROM t1;

  I1   I2   I3 RESULT
---- ---- ---- ------
   1    1    1 TRUE  
   2 null    3 FALSE 
null null null FALSE 

3 rows selected.
```

<a id="a6006fef09d68507"></a>
### Compatibility

The SQL standard compatibility for condition is as follows.

**SQL standard compatibility for condition**

<a id="b8a166499a301b49"></a>
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
| T501 | Enhanced EXISTS predicate | O |
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

<a id="120c84b6ceea6934"></a>
## JSON String Constructor

The JSON string constructor is a function that takes an SQL expression as an argument and generates a string in JSON format.

The JSON string constructor is categorized as follows:  
• JSON value constructor  
• JSON aggregate constructor  
• JSON window constructor

<a id="7bebd87d7a04a6f6"></a>
### JSON String Constructor

<a id="41cb4c11a3101920"></a>
#### JSON value Constructor

The JSON value constructor is a single row function that generates one JSON string row for each input row.

The JSON value constructor is categorized as follows:

- [JSON_ARRAY](17-built-in-function-references.md#94293f3bf1dcc625)
- [JSON_OBJECT](17-built-in-function-references.md#b388bbc3cd35802e)

<a id="3af21881e760a885"></a>
#### JSON aggregate Constructor

The JSON aggregate constructor is an aggregate function that generates a single JSON string row by aggregating the results.

The JSON aggregate constructor is categorized as follows:

- [JSON_ARRAYAGG](17-built-in-function-references.md#601412b5f2e75023)
- [JSON_OBJECTAGG](17-built-in-function-references.md#3fa8c49abe80530b)

<a id="0dd41eb77b364796"></a>
#### JSON window Constructor

The JSON window constructor is a window function that generates JSON strings over a defined range of records using the OVER clause.

It differs from an aggregate function in that the number of result rows is determined by the groups within the window.

The JSON window constructor is categorized as follows:

- [JSON_ARRAYAGG() OVER](17-built-in-function-references.md#ea5a2230a661abf0)
- [JSON_OBJECTAGG() OVER](17-built-in-function-references.md#4ada1dbdfa329af8)

<a id="4fc7cf205e211640"></a>
### JSON String

There are two types of JSON strings: JSON object strings and JSON array strings.

<a id="0a685e5ca49122b4"></a>
#### JSON Object String

A JSON object string is composed of consecutive key-value pairs enclosed in curly braces, and each key must be an SQL string.

```
{ key : value }
{ key : value, key : value, ... }
```

The following three functions return a JSON object string as the result.

- [JSON_OBJECT](17-built-in-function-references.md#b388bbc3cd35802e)
- [JSON_OBJECTAGG](17-built-in-function-references.md#3fa8c49abe80530b)
- [JSON_OBJECTAGG() OVER](17-built-in-function-references.md#4ada1dbdfa329af8)

<a id="2a727d24d3dccf5e"></a>
#### JSON Array String

A JSON array string is composed of a sequence of values enclosed in square brackets.

```
[ value ]
[ value, value, ... ]
```

The following three functions return a JSON array string as the result.

- [JSON_ARRAY](17-built-in-function-references.md#94293f3bf1dcc625)
- [JSON_ARRAYAGG](17-built-in-function-references.md#601412b5f2e75023)
- [JSON_ARRAYAGG() OVER](17-built-in-function-references.md#ea5a2230a661abf0)

<a id="410093118f3fad17"></a>
### JSON Structural Characters

There are six types of characters that make up a JSON string.

<a id="4b102d2bc24f796b"></a>
| JSON structural character | Description |
| --- | --- |
| [ | It is the square bracket used to start a JSON array string. |
| ] | It is the square bracket used to close a JSON array string. |
| { | It is the curly brace used to start a JSON object string. |
| } | It is the curly brace used to close a JSON object string. |
| : | It is the character that separates keys. |
| , | It is the character that separates values. |

These characters allow spaces before and after them.

<a id="bf20e264be9d5704"></a>
### JSON Escape Characters

The characters that are escaped within a JSON string are as follows.

<a id="a0e03d5bca7fbc85"></a>
| Character | escape form | Description |
| --- | --- | --- |
| " | \" | quotation mark |
| \ | \\ | back slash |
| CHR(8) | \b | backspace |
| CHR(12) | \f | form feed |
| CHR(10) | \n | new line feed |
| CHR(19) | \r | carriage return |
| CHR(9) | \t | tab |

The following are examples of characters being escaped.

```
gSQL> SELECT JSON_OBJECT( 'quote' VALUE '"',
                          'backslash' VALUE '\',
                          'backspace' VALUE CHR(8),
                          'formfeed' VALUE CHR(12),
                          'newline' VALUE CHR(10),
                          'carriage_return' VALUE CHR(13),
                          'tab' VALUE CHR(9) ) AS escaped_json
       FROM dual;

ESCAPED_JSON                                                                    
-------------------------------------------------------------------------
{"quote":"\"","backslash":"\\","backspace":"\b","formfeed":"\f","newline":"\n","carriage_return":"\r","tab":"\t"}                                   

1 row selected.
```

The following is an example comparing an unescaped string and an escaped string.

```
--# Unescaped result
SELECT * FROM sample_table;

ID STRING_DATA             
-- ------------------------
 1 simple string           
 2 This is first sentence. 
   This is second sentence.
 3 He said, "Hello".       

3 rows selected.


--# Escaped result
SELECT JSON_OBJECT( 'ID'    VALUE id,
                    'DATA'  VALUE string_data ) AS json_string
  FROM sample_table;

JSON_STRING                                                        
-------------------------------------------------------------------
{"ID":1,"DATA":"simple string"}                                    
{"ID":2,"DATA":"This is first sentence.\nThis is second sentence."}
{"ID":3,"DATA":"He said, \"Hello\"."}                              

3 rows selected.
```

<a id="2e6bf08207f55a87"></a>
### JSON Result Control Options

<a id="1c3a3c2ef843723a"></a>
#### JSON Constructor Null Clause

These options control the output when the value argument of the JSON string constructor is null.

```
<JSON constructor null clause> ::=
    NULL ON NULL
  | ABSENT ON NULL
  | EMPTY STRING ON NULL
```

<a id="1570524e187e13a8"></a>
##### NULL ON NULL

When the value is null, it outputs JSON string null.

```
gSQL> SELECT JSON_OBJECT( name VALUE balances NULL ON NULL ) AS res_json_object
        FROM accounts;

RES_JSON_OBJECT
---------------
{"Alice":50000}
{"Bob":null}   
{"Chris":1000} 

3 rows selected.

gSQL> SELECT JSON_ARRAY( name, balances NULL ON NULL ) AS res_json_array
        FROM accounts;

RES_JSON_ARRAY 
---------------
["Alice",50000]
["Bob",null]   
["Chris",1000] 

3 rows selected.
```

<a id="7be97b8d350e0cec"></a>
##### ABSENT ON NULL

When the value is null, it is ignored and nothing is output.

```
gSQL> SELECT JSON_OBJECT( name VALUE balances ABSENT ON NULL ) AS res_json_object
        FROM accounts;

RES_JSON_OBJECT
---------------
{"Alice":50000}
{}             
{"Chris":1000} 

3 rows selected.

gSQL> SELECT JSON_ARRAY( name, balances ABSENT ON NULL ) AS res_json_array
        FROM accounts; 

RES_JSON_ARRAY 
---------------
["Alice",50000]
["Bob"]        
["Chris",1000] 

3 rows selected.
```

<a id="ecde2e6afd0bcfb1"></a>
##### EMPTY STRING ON NULL

When the value is null, it outputs an empty string ("").

```
gSQL> SELECT JSON_OBJECT( name VALUE balances EMPTY STRING ON NULL ) AS res_json_object
        FROM accounts;

RES_JSON_OBJECT
---------------
{"Alice":50000}
{"Bob":""}     
{"Chris":1000} 

3 rows selected.

gSQL> SELECT JSON_ARRAY( name, balances EMPTY STRING ON NULL ) AS res_json_array
        FROM accounts;

RES_JSON_ARRAY 
---------------
["Alice",50000]
["Bob",""]     
["Chris",1000] 

3 rows selected.
```

<a id="57242fece54b39a5"></a>
#### JSON Output Clause

It defines the data type of the resulting string generated by the JSON string constructor.

The data type can be set to one of the character string types.

```
<JSON output clause> ::=
    RETURNING <string data type> 

<string data type> ::=
    CHAR(n)
  | VARCHAR(n)
  | LONG VARCHAR
```

The following is an example that specifies the JSON output clause.

```
SELECT JSON_OBJECT( name VALUE balance RETURNING VARCHAR(100) ) AS res_json_object
  FROM accounts;
```

<a id="f75f4801d0edd28a"></a>
### JSON String Output Format

The string generated by the JSON string constructor is output as follows, depending on the SQL data type of the expression argument.

<a id="ded5b5060e978fb5"></a>
| SQL data type of the expression | Output format |
| --- | --- |
| Number | Numeric |
| Boolean | Boolean |
| Character string | String |
| Binary string | String |
| Date/time | String |
| Interval | String |

- If the output format is string, the expression is output including double quotation marks (") at the beginning and end.

The output format of the resulting JSON string according to the SQL data type of each expression argument is as follows.

<a id="1d72ab3dbc6ffd05"></a>
#### Number

The number type can represent all valid significant digits supported by numeric values.

```
gSQL> SELECT JSON_OBJECT( 'k_num' VALUE 100 ) AS result
        FROM dual;

RESULT       
-------------
{"k_num":100}

1 row selected.

gSQL> SELECT JSON_ARRAY( 100 ) AS result
        FROM dual;

RESULT
------
[100] 

1 row selected.
```

<a id="d2f3fb80ea591af9"></a>
#### Boolean

```
gSQL> SELECT JSON_OBJECT( 'k_boolean' VALUE true ) AS result
        FROM dual;

RESULT            
------------------
{"k_boolean":true}

1 row selected.

gSQL> SELECT JSON_ARRAY( true ) AS result
        FROM dual;

RESULT
------
[true]

1 row selected.
```

<a id="b6159465ffaa326d"></a>
#### Character String

```
gSQL> SELECT JSON_OBJECT( 'k_char' VALUE 'hello' ) AS result
        FROM dual;

RESULT            
------------------
{"k_char":"hello"}

1 row selected.

gSQL> SELECT JSON_ARRAY( 'hello' ) AS result
        FROM dual; 

RESULT   
---------
["hello"]

1 row selected.
```

<a id="473f4de38a8b1b7e"></a>
#### Binary String

A binary string is represented as a hexadecimal string.

```
gSQL> SELECT JSON_OBJECT( 'k_binary' VALUE X'0011FF' ) AS result
        FROM dual;

RESULT               
---------------------
{"k_binary":"0011FF"}

1 row selected.

gSQL> SELECT JSON_ARRAY( X'0011FF' ) AS result
        FROM dual; 

RESULT    
----------
["0011FF"]

1 row selected.
```

<a id="dc4efb3654935ae5"></a>
#### Date/ Time

<a id="6d979d448914cb06"></a>
##### Date

The date type is output in the 'YYYY-MM-DDTHH:MM:SS' format.

- 'T' is the delimiter between the date and time.

```
gSQL> SELECT JSON_OBJECT( 'k_date' VALUE DATE '2025-05-05' ) AS result
        FROM dual;

RESULT                          
--------------------------------
{"k_date":"2025-05-05T00:00:00"}

1 row selected.

gSQL> SELECT JSON_ARRAY( DATE '2025-05-05' ) AS result
        FROM dual;

RESULT                 
-----------------------
["2025-05-05T00:00:00"]

1 row selected.
```

<a id="33a3ea545212f64c"></a>
##### Time

The time type is output in the 'HH:MM:SS.FF6' format.

- If necessary, the time zone is represented in the format 'HH:MM:SS.FF6±TZH:TZM'.

```
gSQL> SELECT JSON_OBJECT( 'k_time' VALUE TIME '15:30:59.999999' ) AS result
        FROM dual;

RESULT                      
----------------------------
{"k_time":"15:30:59.999999"}

1 row selected.

gSQL> SELECT JSON_ARRAY( TIME'15:30:59.999999' ) AS result
        FROM dual; 

RESULT             
-------------------
["15:30:59.999999"]

1 row selected.
```

<a id="63320cbf0cc531a6"></a>
##### Timestamp

The timestamp type is output in the 'YYYY-MM-DDTHH:MM:SS.FF6' format.

- 'T' is the delimiter between the date and time.
- If necessary, the time zone is represented in the format 'YYYY-MM-DDTHH:MM:SS.FF6±TZH:TZM'.

```
gSQL> SELECT JSON_OBJECT( 'k_timestamp' VALUE TIMESTAMP '2025-05-05 12:30:45 +09:00' ) AS result
        FROM dual;

RESULT                                            
--------------------------------------------------
{"k_timestamp":"2025-05-05T12:30:45.000000+09:00"}

1 row selected.

gSQL> SELECT JSON_ARRAY( TIMESTAMP '2025-05-05 12:30:45 +09:00' ) AS result
        FROM dual;

RESULT                              
------------------------------------
["2025-05-05T12:30:45.000000+09:00"]

1 row selected.
```

<a id="9a00edfd241fb5cb"></a>
#### Interval

The interval type follows the duration format defined by ISO 8601.

<a id="50067b95d9970984"></a>
##### Interval Year to Month

The Interval Year to Month type is represented in the 'P[n]Y[n]M' format.

- 'P' is a prefix that indicates a period.
- 'Y' (year) and 'M' (month) are units that represent date-based durations, and any unit with a value of 0 is omitted.
    - e.g. "P1Y" (1 year), "P3M" (3 months), "P1Y2M" (1 year and 2 months)
- If all values are 0, the default output is "P0Y".

```
gSQL> SELECT JSON_OBJECT( 'k_int_ytom' VALUE INTERVAL '3-6' YEAR TO MONTH ) AS result
        FROM dual; 

RESULT                
----------------------
{"k_int_ytom":"P3Y6M"}

1 row selected.

gSQL> SELECT JSON_ARRAY( INTERVAL '3-6' YEAR TO MONTH ) AS result
        FROM dual; 

RESULT   
---------
["P3Y6M"]

1 row selected.

gSQL> SELECT JSON_OBJECT( 'k_int_ytom' VALUE INTERVAL '0-6' YEAR TO MONTH ) AS result
        FROM dual; 

RESULT              
--------------------
{"k_int_ytom":"P6M"}

1 row selected.

gSQL> SELECT JSON_ARRAY( INTERVAL '0-6' YEAR TO MONTH ) AS result
        FROM dual; 

RESULT 
-------
["P6M"]

1 row selected.

gSQL> SELECT JSON_OBJECT( 'k_int_ytom' VALUE INTERVAL '0-0' YEAR TO MONTH ) AS result
        FROM dual;

RESULT              
--------------------
{"k_int_ytom":"P0Y"}

1 row selected.

gSQL> SELECT JSON_ARRAY( INTERVAL '0-0' YEAR TO MONTH ) AS result
        FROM dual; 

RESULT 
-------
["P0Y"]

1 row selected.
```

<a id="1115a079a772ccf7"></a>
##### Interval Day to Second

The Interval Day to Second type is represented in the 'P[n]DT[n]H[n]M[n]S' format.

- 'P' is a prefix that indicates a period.
- 'D' (day) is a unit that represents a date-based duration.
- 'T' is the delimiter between the date-based and time-based portions of the duration.
- 'H' (hour), 'M' (minute), and 'S' (second) are units that represent time-based durations.
- If necessary, fractional seconds may be included and they are fixed to six decimal places.
    - e.g. 'P1DT2H30M15.123000S' (1 day, 2 hours, 30 minutes, 15.123 seconds)
- Any unit with a value of 0 is omitted.
    - e.g. 'P2DT3H' (2 days, 3 hours), 'PT45M' (45 minutes)
- If all values are 0, the default output is "P0D".

```
gSQL> SELECT JSON_OBJECT( 'k_int_dtos' VALUE INTERVAL '1 2:30:15.123' DAY TO SECOND ) AS result
        FROM dual;

RESULT                              
------------------------------------
{"k_int_dtos":"P1DT2H30M15.123000S"}

1 row selected.


gSQL> SELECT JSON_ARRAY( INTERVAL '1 2:30:15.123' DAY TO SECOND ) AS result
        FROM dual;

RESULT                 
-----------------------
["P1DT2H30M15.123000S"]

1 row selected.

gSQL> SELECT JSON_OBJECT( 'k_int_dtos' VALUE INTERVAL '0 00:30:00' DAY TO SECOND ) AS result
        FROM dual;

RESULT                
----------------------
{"k_int_dtos":"PT30M"}

1 row selected.

gSQL> SELECT JSON_ARRAY( INTERVAL '0 00:30:00' DAY TO SECOND ) AS result
        FROM dual;

RESULT   
---------
["PT30M"]

1 row selected.

gSQL> SELECT JSON_OBJECT( 'k_int_dtos' VALUE INTERVAL '0 00:00:00' DAY TO SECOND ) AS result
        FROM dual;

RESULT              
--------------------
{"k_int_dtos":"P0D"}

1 row selected.

gSQL> SELECT JSON_ARRAY( INTERVAL '0 00:00:00' DAY TO SECOND ) AS result
        FROM dual;

RESULT 
-------
["P0D"]

1 row selected.
```

<a id="fa51104610ca0b54"></a>
### Compatibility

The SQL standard compatibility for the JSON string constructor is as follows.

**SQL standard compatibility for functions**

<a id="d7a58d04d862f4b1"></a>
| Feature ID | Description | Availability |
| --- | --- | --- |
| T811 | Basic SQL/JSON constructor functions | O |
| T812 | SQL/JSON: JSON_OBJECTAGG | O |
| T813 | SQL/JSON: JSON_ARRAYAGG with ORDER BY | X |
| T814 | Colon in JSON_OBJECT or JSON_OBJECTAGG | O |
| T830 | Enforcing unique keys in SQL/JSON constructor functions | X |

---

[← 10. Server Property](../part-02-administration-manual/10-server-property.md) · [Table of contents](../README.md) · [12. SQL Languages →](12-sql-languages.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
