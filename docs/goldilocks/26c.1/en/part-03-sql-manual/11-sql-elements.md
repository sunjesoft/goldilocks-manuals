<a id="2626851844143001"></a>

# 11. SQL Elements

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/2626851844143001)  
> Tag: `26c.1_0_tag`

[← 10. Server Property](../part-02-administration-manual/10-server-property.md) · [Table of contents](../README.md) · [12. SQL Languages →](12-sql-languages.md)

<a id="7d4617651b196f1e"></a>
## Syntax Elements

<a id="e5afdf099617232e"></a>
### Identifiers

An identifier is divided into an ordinary identifier and a delimited identifier.  
An ordinary identifier consists of letters or a combination of letters and numbers, and it is used by internally converting all characters to uppercase. Therefore, it is case-insensitive.

The following is an example of an ordinary identifier.

```
GOLDILOCKS
GoldiLocks
```

A delimited identifier consists of letters or a combination of letters and numbers enclosed in double quotes ("). Internally, all characters are used exactly as specified. Therefore, when using a delimited identifier, case sensitivity is observed.

The following is an example of a delimited identifier.

```
"GOLDILOCKS"
"GoldiLocks"
```

<a id="013e0dda4b33d931"></a>
### Literals

Literals refer to the representation of non-null values.

<a id="d8a396393b868d0a"></a>
#### Text Literals

Text literals refer to the representation of strings and binary strings.

Use a single quote (') at the beginning and end of a string to represent text literals.  
In addition to double quotes ("), all strings except for the single quote (') string can be enclosed in single quotes (').  
Write two consecutive single quotes without any spaces in between to use a single quote (') in the string.   
A string can contain a maximum of 4,000 characters.

The following are examples of text literals for strings.

```
'GOLDILOCKS'
'Sunje''s DBMS'
```

A binary string of text literals is a string of hexadecimal numbers that starts with x' (X') and ends with '. Each position in a hexadecimal string can only contain characters corresponding to 0-9 and A (a) to F (f). The length of a hexadecimal string must always be an even number as two digits represent one byte. A binary string can contain a maximum of 4,000 characters.

The following are examples of text literals for binary strings.

```
x'001f'
X'FF0A'
x'aF37BBc013'
```

<a id="59c314d69e48658f"></a>
#### Numeric Literals

Numeric literals refer to literals of numeric types, which can include integers or numbers with decimal points. The syntax for numeric literals is as follows:

```
[ + | - ] <digits> [ . <digits> ] [ E | e [ + | - ] <digits> ] [ f | F | d | D ]
```

- The first + or - indicates whether the overall number is positive or negative. The + or - can be omitted, and if omitted, it is considered positive.
- In &lt;digits&gt;, numbers between 0 and 9 can be listed without spaces, and a decimal point (.) can be used to include digits after the decimal.
- After the first &lt;digits&gt;, an exponent can be written in the form of an E or e to indicate the exponent. Following this, a + or - sign can be added to specify the sign of the exponent, followed by &lt;digits&gt;. The sign of the exponent is optional, and if omitted, it is considered positive.
- Finally, characters such as f, F, d, or D can appear after the number to indicate that it is of type BINARY_FLOAT or BINARY_DOUBLE. If these characters are omitted, the number is considered to be of the NUMBER type.

The following are examples of numeric literals.

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

<a id="e5113ffdea3a8672"></a>
#### Datetime Literals

Datetime literals refer to literals of the date/time type.   
A datetime value can be specified using a string literal or by converting a character or numeric value to a datetime value using TO_*function (TO_DATE, etc).

Datetime data types include DATE, TIME, TIME WITH TIME ZONE, TIMESTAMP, and TIMESTAMP WITH TIME ZONE.

<a id="a2f402a0fdce6c45"></a>
##### Date Literals

Date literals can be written in the form of DATE'string literal' or TO_DATE(string_literal [, format]).

- DATE'string literal'
    - The format for the date type is ' SYYYY-MM-DD'.
    - DATE'2002-07-15'
- TO_DATE(string_literal [, format])
    - If the format is not specified, the default format for the date type is NLS_DATE_FORMAT.
    - If a format is specified, that format will be applied.

- The date type includes year, month, day, hour, minute, and second (excluding fractional seconds).
- If the date is omitted, the default value is the first day of the current month.
- If the hour, minute, or second is omitted, the default value is midnight.
    - HH24 format: '00:00:00'
    - HH12 format: '12:00:00'
- To set the hour, minute, and second to the default value (midnight) when a date value includes these components, use the TRUNC(date) function. 
    - For example, in TRUNC(SYSDATE), SYSDATE includes the values for year, month, day, hour, minute, and second.
- To compare only the year, month, and day values among date values, use the TRUNC function to set the hour, minute, and second to midnight.

For more information, refer to [TO_DATE](17-built-in-function-references.md#74b46ad0bc9dbb10), [Datetime Format String](#c0861393ec3cf3cf), [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#86120b98fe0558e4).

- The following is an example of date literals.

```
DATE'2002-07-15'
```

- The following is an example where the format is not specified, so NLS_DATE_FORMAT is 'YYYY-MM-DD'.

```
TO_DATE( '2002-07-15' )
```

- The following are examples where the format is specified.

```
TO_DATE( '15-JUL-02', 'DD-MON-RR' )
TO_DATE( '2002-07-15 00:00:00', 'YYYY-MM-DD HH24:MI:SS' )
TO_DATE( '2002-07-15 13:25:30', 'YYYY-MM-DD HH24:MI:SS' )
```

- The following is an example where the date is omitted. (It is set to the first day of the current month).

```
gSQL> SELECT TO_DATE( '2000-07', 'YYYY-MM' ) FROM DUAL;
TO_DATE( '2000-07', 'YYYY-MM' )
-------------------------------
2000-07-01
```

- The following is an example where the hour, minute, and second are omitted. (They are set to midnight).

```
gSQL> SELECT 
      TO_CHAR( DATE'2002-07-15', 'YYYY-MM-DD HH24:MI:SS' ) AS RESULT
      FROM DUAL;
RESULT             
-------------------
2002-07-15 00:00:00
```

- The following is an example of setting the hour, minute, and second of a DATE value (SYSDATE) to the default value (midnight).

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

- The following is an example of comparing only the year, month, and day values among date values.

```
gSQL> SELECT 
      TO_DATE( '2002-08-12' ) = 
      TRUNC( TO_DATE( '2002-08-12 23:59:59', 'YYYY-MM-DD HH24:MI:SS' ) )
      AS RESULT FROM DUAL;
RESULT
------
TRUE
```

<a id="f03167b962c6a80b"></a>
##### Time Literals

Time literals can be written in the form of TIME'string literal' or TO_TIME(string_literal [, format]).

- TIME'string literal'
    - The format for the time type is 'HH24:MI:SS[.[FF6]]'.
    - TIME'15:30:59.999999'
- TO_TIME(string_literal [, format])
    - If the format is not specified, the default format for the time type is NLS_TIME_FORMAT.
    - If a format is specified, that format will be applied.

The time type includes hour, minute, second (fractional seconds).  
Fractional seconds can be specified with a maximum of six digits.

For more information, refer to [TO_TIME](17-built-in-function-references.md#369e424a6a243c31), [Datetime Format String](#c0861393ec3cf3cf), [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#b303d4bd630c0388).

- The following is an example of time literals.

```
TIME'15:30:59.999999'
```

- The following is an example where the format is not specified, so NLS_TIME_FORMAT is 'HH24:MI:SS.FF6'.

```
TO_TIME( '15:30:59.999999' )
```

- The following is an example where the format is specified.

```
TO_TIME( '09.45.03.546873 AM', 'HH12.MI.SS.FF6 AM' )
TO_TIME( '09:45:03', 'HH12:MI:SS' )
```

<a id="2bc09a30c6210f96"></a>
##### Time with Time Zone Literals

Time with time zone literals can be written in the form of TIME'string literal', TIME WITH TIME ZONE'string literal',  TO_TIME_WITH_TIME_ZONE(string_literal [, format] ), or TO_TIME_TZ(string_literal [, format] ).

- TIME'string literal' or TIME WITH TIME ZONE'string literal'
    - The format for the time with time zone type is 'HH24:MI:SS[.[FF6]] TZH:TZM'.
    - TIME'15:30:59.999999 +09:00'
    - TIME WITH TIME ZONE'15:30:59.999999 +09:00'
- TO_TIME_WITH_TIME_ZONE(string_literal [, format] )
    - If the format is not specified, the default format for the time with time zone type is NLS_TIME_WITH_TIME_ZONE_FORMAT.
    - If a format is specified, that format is applied.

The time with time zone type includes hour, minute, second (fractional seconds), and time zone offset (time zone hour, time zone minute).  
Fractional seconds can be specified with a maximum of six digits.

For more information, refer to [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#7d0b935c0acaee3f), [Datetime Format String](#c0861393ec3cf3cf), [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#81aefd62dd9e1a5a).

- The following are examples of time with time zone literals.

```
TIME'15:30:59.999999 +09:00'

TIME WITH TIME ZONE'15:30:59.999999 +09:00'
```

- The following is an example where the format is not specified, so NLS_TIME_WITH_TIME_ZONE_FORMAT is 'HH24:MI:SS.FF6 TZH:TZM'.

```
TO_TIME_WITH_TIME_ZONE( '15:30:59.999999 +09:00' )
TO_TIME_TZ( '15:30:59.999999 +09:00' )
```

- The following is an example where the format is specified.

```
TO_TIME_WITH_TIME_ZONE( '09.45.03.546873 +09:00 AM', 
                        'HH12.MI.SS.FF6 TZH:TZM AM' )
```

<a id="6701ce4c7c705e13"></a>
##### Timestamp Literals

Timestamp literals can be written in the form of TIMESTAMP'string literal' or TO_TIMESTAMP(string_literal [, format] ).

- TIMESTAMP'string literal'
    - The format for the timestamp type is 'SYYYY-MM-DD HH24:MI:SS[.[FF6]]'.
    - TIMESTAMP'2002-07-15 15:39:59.999999'
- TO_TIMESTAMP(string_literal [, format] )
    - If the format is not specified, the default format for the timestamp type is NLS_TIMESTAMP_FORMAT.
    - If a format is specified, that format will be applied.

Timestamp type includes year, month, day, hour, minute, second (fractional seconds).  
Fractional seconds can be specified with a maximum of six digits.

For more information, refer to [TO_TIMESTAMP](17-built-in-function-references.md#b03348c605444fea), [Datetime Format String](#c0861393ec3cf3cf), [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#5129c923d9116f8d).

- The following is an example of timestamp literals.

```
TIMESTAMP'2002-07-15 15:39:59.999999'
```

- The following is an example where the format is not specified, so NLS_TIMESTAMP_FORMAT is 'YYYY-MM-DD HH24:MI:SS.FF6'.

```
TO_TIMESTAMP( '2002-07-15 15:39:59.999999' )
```

- The following is an example where the format is specified.

```
TO_TIMESTAMP( '15-JUL-02 11.06.30.123456 AM', 
              'DD-MON-RR HH12.MI.SS.FF6 AM' )
```

<a id="b7e21173111bed2b"></a>
##### Timestamp with Time Zone Literals

Timestamp with time zone literals can be written in the form of TIMESTAMP'string literal',  TIMESTAMP WITH TIME ZONE'string literal', TO_TIMESTAMP_WITH_TIME_ZONE(string_literal [, formt] ), or TO_TIMESTAMP_TZ(string_literal [, format]).

- TIMESTAMP'string literal' or TIMESTAMP WITH TIME ZONE'string literal'
    - The format for the timestamp with time zone type is 'SYYYY-MM-DD HH24:MI:SS[.[FF6]] TZH:TZM'.
    - TIMESTAMP'2002-07-15 15:39:59.999999 +09:00'
    - TIMESTAMP WITH TIME ZONE'2002-07-15 15:39:59.999999 +09:00'
- TO_TIMESTAMP_WITH_TIME_ZONE(string_literal [, formt] )
    - If the format is not specified, the default format for the timestamp with time zone type is NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT. 
    - If a format is specified, that format will be applied.

Timestamp with time zone type includes year, month, day, hour, minute, second (fractional seconds), time zone offset (time zone hour, time zone minute).  
Fractional seconds can be specified with a maximum of six digits.

For more information, refer to [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#785d71b6e8e5c13b), [Datetime Format String](#c0861393ec3cf3cf) , [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#8a228be667cdaef8).

- The following is an example of timestamp with time zone literals.

```
TIMESTAMP'2002-07-15 15:39:59.999999 +09:00'
TIMESTAMP WITH TIME ZONE'2002-07-15 15:39:59.999999 +09:00'
```

- The following is an example where the format is not specified, so NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT is 'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM'.

```
TO_TIMESTAMP_WITH_TIME_ZONE( '2002-07-15 15:39:59.999999 +09:00' )
TO_TIMESTAMP_TZ( '2002-07-15 15:39:59.999999 +09:00' )
```

- The following is an example where the format is specified.

```
TO_TIMESTAMP_WITH_TIME_ZONE( '15-JUL-02 11.06.30.123456 +09:00 AM',
                             'DD-MON-RR HH12.MI.SS.FF6 TZH:TZM AM' )
TO_TIMESTAMP_TZ( '15-JUL-02 11.06.30.123456 +09:00 AM',
                 'DD-MON-RR HH12.MI.SS.FF6 TZH:TZM AM' )
```

<a id="daf1003f657050c1"></a>
#### Interval Literals

Interval literals specify a time interval.

Intervals are classified and expressed as follows.

- Year-month INTERVAL values
    - These include YEAR and MONTH.
    - Display string representation: 'year-month'
    - They can be written in the form of *INTERVAL 'string literal' YEAR[leading precision] TO MONTH* or *NUMTOYMINTERVAL( num, interval_indicator )*
- Day-time INTERVAL values
    - These include DAY, HOUR, MINUTE, SECOND (fractional seconds).
    - Display string representation: 'day hour:minute:second.fractional_seconds'
    - They can be written in the form of *INTERVAL 'string literal' DAY[leading precision] TO SECOND[fractiona l seconds precision]* or *NUMTODSINTERVAL( num, interval_indicator )*.
- The sign of the interval value can be specified only once at the very beginning of the string representation.  
  e.g. INTERVAL'+3 11:22:33.999999'DAY TO SECOND (O)  
  INTERVAL'-3 +11:22:33.999999'DAY TO SECOND (X)

The following is a list of interval types.

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
• It is the number of digits in the field and can be specified from 2 to 6. If not specified, the default value is set to 2.  
• If the leading field value exceeds the specified leading precision, an error will be returned.

Fractional seconds precision  
• It is the number of digits for fractional seconds and can be specified from 0 to 6. If not specified, the default value is set to 6.  
• If the fractional second field value exceeds the specified fractional seconds precision, it will be rounded off.

For more information, refer to [INTERVAL](16-built-in-data-type-references.md#3719f3256f650b0f), [Precisions and value range of the second or later field in INTERVAL * TO * ](16-built-in-data-type-references.md#5cb5c423faf9a449), [NUMTODSINTERVAL](17-built-in-function-references.md#36e622b41cbe994b), [NUMTOYMINTERVAL](17-built-in-function-references.md#76ea4a5700a8dd3d).

<a id="06df0a91b8ea0be6"></a>
#### Examples of Using Interval Literals.

The following are examples of using interval literals.

<a id="0555ca77cafd71de"></a>
##### Interval YEAR

The following are examples of using interval YEAR literals.

**Interval YEAR literals.**

<a id="b1b42ab4ec276952"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'YEAR INTERVAL'01-00'YEAR | 1 year | +01-00 |
| INTERVAL'100'YEAR | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100'YEAR(3) | 100 year | +100-00 |
| INTERVAL'+999999'YEAR(6) | 999999 year | +999999-00 |
| INTERVAL'-999999'YEAR(6) | -(999999 year) | -999999-00 |

<a id="18655e8ff8458178"></a>
##### Interval MONTH

The following are examples of using interval MONTH literals.

<a id="ae99d77eb193751f"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'MONTH INTERVAL'00-01'MONTH | 1 month | +00-01 |
| INTERVAL'100'MONTH | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100'MONTH(3) | 8 year 4 month | +008-04 |
| INTERVAL'+999999'MONTH(6) | 83333 year 3 month | +083333-03 |
| INTERVAL'-999999'MONTH(6) | -(83333 year 3 month) | -083333-03 |

<a id="9fc257af39ed09c4"></a>
##### Interval YEAR TO MONTH

The following are examples of using interval YEAR TO MONTH literals.

<a id="2a020483acf734b3"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1-06'YEAR TO MONTH | 1 year 6 month | +01-06 |
| INTERVAL'1-12'YEAR TO MONTH | The month value exceeded 11, so it returns the error. | - |
| INTERVAL'100-11'YEAR TO MONTH | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100-11'YEAR(3) TO MONTH | 100 year 11 month | +100-11 |
| INTERVAL'+999999-11'YEAR(6) TO MONTH | 999999 year 11 month | +999999-11 |
| INTERVAL'-999999-11'YEAR(6) TO MONTH | -(999999 year 11 month) | -999999-11 |

<a id="f96ae5fd3af769a7"></a>
##### Interval DAY

The following are examples of using interval DAY literals.

<a id="7ce12ecd04b52549"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'DAY INTERVAL'01 00:00:00'DAY | 1 day | +01 00:00:00 |
| INTERVAL'100'DAY | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100'DAY(3) | 100 day | +100 00:00:00 |
| INTERVAL'+999999'DAY(6) | 999999 day | +999999 00:00:00 |
| INTERVAL'-999999'DAY(6) | -(999999 day) | -999999 00:00:00 |

<a id="d2af08a8b8fa4158"></a>
##### Interval HOUR

The following are examples of using interval HOUR literals.

<a id="149e6ed14dd25535"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'HOUR INTERVAL'00 01:00:00'HOUR | 1 hour | +00 01:00:00 |
| INTERVAL'1000'HOUR(3) | It exceeds the leading precision 3, so it returns the error | - |
| INTERVAL'1000'HOUR(4) | 41 day 16 hour | +0041 16:00:00 |
| INTERVAL'+999999'HOUR(6) | 41666 day 15 hour | +041666 15:00:00 |
| INTERVAL'-999999'HOUR(6) | -(41666 day 15 hour) | -041666 15:00:00 |

<a id="78497d59152c50a8"></a>
##### Interval MINUTE

The following are examples of using interval MINUTE literals.

<a id="0cbac9869203fd60"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'MINUTE INTERVAL'00 00:01:00'MINUTE | 1 minute | +00 00:01:00 |
| INTERVAL'12345'MINUTE(4) | It exceeds the leading precision 4, so it returns the error | - |
| INTERVAL'12345'MINUTE(5) | 8 day 13 hour 45 minute | +00008 13:45:00 |
| INTERVAL'+999999'MINUTE(6) | 694 day 10 hour 39 minute | +000694 10:39:00 |
| INTERVAL'-999999'MINUTE(6) | -(694 day 10 hour 39 minute) | -000694 10:39:00 |

<a id="14078cc7f894bd89"></a>
##### Interval SECOND

The following are examples of using interval SECOND literals.

<a id="cdb4c54333ec385d"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1'SECOND INTERVAL'00 00:00:01.000000'SECOND | 1 second | +00 00:00:01.000000 |
| INTERVAL'100'SECOND | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'99.9999999'SECOND INTERVAL'99.9999999'SECOND(2,6) | The fractional seconds are rounded off to become 100 second, then it exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'99.9999999'SECOND(3) | 1 minute 40 second | +000 00:01:40.000000 |
| INTERVAL'29.506167'SECOND(2, 2) | 29.51 second | +00 00:00:29.51 |
| INTERVAL'999999.999999'SECOND(6,6) | 11day 13 hour 46 minute 39.999999 second | +000011 13:46:39.999999 |
| INTERVAL'-999999.999999'SECOND(6,6) | -(11day 13 hour 46 minute 39.999999 second) | -000011 13:46:39.999999 |

<a id="14e83363064b6e1e"></a>
##### Interval DAY TO HOUR

The following are examples of using interval DAY TO HOUR literals.

<a id="463ea42f21aca92f"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1 23'DAY TO HOUR INTERVAL'01 23:00:00'DAY TO HOUR | 1 day 23 hour | +01 23:00:00 |
| INTERVAL'1 24'DAY TO HOUR | The hour value exceeds 23(invalid), so it returns the error. | - |
| INTERVAL'100 23'DAY TO HOUR | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100 23'DAY(3) TO HOUR | 100 day 23 hour | +100 23:00:00 |
| INTERVAL'+999999 23'DAY(6) TO HOUR | 999999 day 23 hour | +999999 23:00:00 |
| INTERVAL'-999999 23'DAY(6) TO HOUR | -(999999 day 23 hour) | -999999 23:00:00 |
| INTERVAL'-999999 +23'DAY(6) TO HOUR | Invalid sign error | - |

<a id="0ee1be1e83c02e7a"></a>
##### Interval DAY TO MINUTE

The following are examples of using interval DAY TO MINUTE literals.

<a id="1666642586739afd"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'1 23:59'DAY TO MINUTE INTERVAL'01 23:59:00'DAY TO MINUTE | 1 day 23 hour 59 second | +01 23:59:00 |
| INTERVAL'1 24:59'DAY TO MINUTE | The hour value exceeds 23 (invalid), so it returns the error. | - |
| INTERVAL'1 23:60'DAY TO MINUTE | The minute value exceeds 59 (invalid), so it returns the error. | - |
| INTERVAL'100 23:59'DAY TO MINUTE | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100 23:59'DAY(3) TO MINUTE | 100 day 23 hour 59 minute | +100 23:59:00 |
| INTERVAL'+999999 23:59'DAY(6) TO MINUTE | 999999 day 23 hour 59 minute | +999999 23:59:00 |
| INTERVAL'-999999 23:59'DAY(6) TO MINUTE | -(999999 day 23 hour 59 minute) | -999999 23:59:00 |

<a id="51e7e3ee0eae4696"></a>
##### Interval DAY TO SECOND

The following are examples of using interval DAY TO SECOND literals.

<a id="878fed07f5678952"></a>
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

<a id="db8d07eab6ba28d6"></a>
##### Interval HOUR TO MINUTE

The following are examples of using interval HOUR TO MINUTE literals.

<a id="a000837f94bc5d7f"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL'23:59'HOUR TO MINUTE INTERVAL'00 23:59:00'HOUR TO MINUTE | 23 hour 59 minute | +00 23:59:00 |
| INTERVAL'23:60'HOUR TO MINUTE | The minute value exceeds 59, so it returns the error. | - |
| INTERVAL'100:59'HOUR TO MINUTE | It exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL'100:59'HOUR(3) TO MINUTE | 4 day 4 hour 59 minute | +004 04:59:00 |
| INTERVAL'+999999:59'HOUR(6) TO MINUTE | 41666 day 15 hour 59 minute | +041666 15:59:00 |
| INTERVAL'-999999:59'HOUR(6) TO MINUTE | -(41666 day 15 hour 59 minute) | -041666 15:59:00 |

<a id="a1aa76d2097f4673"></a>
##### Interval HOUR TO SECOND

The following are examples of using interval HOUR TO SECOND literals.

<a id="cf365547fafb331d"></a>
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

<a id="cd132c4dd8d767ef"></a>
##### Interval MINUTE TO SECOND

The following are examples of using interval MINUTE TO SECOND literals.

<a id="24ff045a9fdc2963"></a>
| Example | Description | Display string |
| --- | --- | --- |
| INTERVAL '15:23.123456'MINUTE TO SECOND INTERVAL '00 00:15:23.123456'MINUTE TO SECOND | 15 minute 23.123456 second | +00 00:15:23.123456 |
| INTERVAL '15:60.123456'MINUTE TO SECOND | The second value exceeds 59, so it returns the error. | - |
| INTERVAL '99:59.999999'MINUTE TO SECOND(2) | The fractional seconds are rounded off to become 100 minute, then it exceeds the leading precision 2, so it returns the error. | - |
| INTERVAL '99:59.999999'MINUTE(3) TO SECOND(2) | 1 hour 40 minute | +000 01:40:00.00 |
| INTERVAL '+999999:59.999999'MINUTE(6) TO SECOND(6) | 694 day 10 hour 39 minute 59.999999 second | +000694 10:39:59.999999 |
| INTERVAL '-999999:59.999999'MINUTE(6) TO SECOND(6) | -(694 day 10 hour 39 minute 59.999999 second) | -000694 10:39:59.999999 |

<a id="d9e7f612fecde5cf"></a>
### Null Value

A null value is an unknown or undefined value. A NULL value can be of any data type. The unknown value for the boolean type is also represented as a null value.  
Null is defined as a keyword and is not case-sensitive.

The following is an example of null value representation.

```
NULL
Null
```

<a id="a1b453895353bf95"></a>
### Comments

<a id="8207c44d53cd08d6"></a>
#### Single Line Comment

Single line comments are comments that start with -- or //. Single line comments treat everything from the comment symbol to the end of the line as a comment.

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

<a id="df32129250738a8c"></a>
#### Multiple Line Comment

Multiple line comments are comments that start with /* and ends with */. Multiple line comments are defined from /* to */ and can span multiple lines.

The following is an example of using a multiple line comment.

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

<a id="d4158b266bc73fd6"></a>
#### Hint Comment

A hint comment is a comment that starts with /*+ and ends with */. Hint comments are similar to multiple line comments, but the difference is that the hint comments have + at the beginning.   
Do not use a space between * and +; otherwise, it will be treated as a multiple line comment.

Unlike other comments, hint comments are specifically meant to be used immediately after the SELECT keyword. The processing instructions specified by the user for the GOLDILOCKS optimizer are described in the hint comment. For more information, refer to [SQL Hint](15-sql-tuning.md#df9172b533f52953).

The following is an example of using a hint comment.

```
gSQL> SELECT /*+ FULL(T1) */ * FROM T1;

I1        I2        I3        I4        I5       
--------- --------- --------- --------- ---------
column i1 column i2 column i3 column i4 column i5

1 row selected.
```

<a id="33b8c20f9eb3da7a"></a>
### SQL Reserved Words and Keywords

<a id="0dc91230fd72b797"></a>
#### SQL Reserved Words

GOLDILOCKS supports reserved words that are defined as SQL reserved words. These SQL reserved words can not be used outside of their specified locations.

SQL reserved words can be used as identifiers by enclosing them in double quotes ("), but this practice is not recommended, as it decreases readability.

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

The following are the SQL reserved words for GOLDILOCKS. The words marked with an asterisk (*) are supported by the SQL standard.   
For more information about this list, refer to [V$RESERVED_WORDS](../part-02-administration-manual/9-database-information.md#f1ea9f619c72a2e2).

ABSOLUTE  
ACCESS  
ADMINISTRATION  
ALL *  
ALLOCATE *  
ALTER *  
ANALYZE         
AND *  
ANTI            
ANY *  
ARE *  
AS *  
ASYMMETRIC *  
AT *  
AUDIT           
AUTHORIZATION *  
BEGIN *  
BETWEEN *  
BOTH *  
BY *  
CALL *  
CASE *  
CHECK *  
CLOSE *  
CLUSTER              
CLUSTER_GROUP_ID     
CLUSTER_GROUP_NAME   
CLUSTER_MEMBER_ID    
CLUSTER_MEMBER_NAME  
CLUSTER_SHARD_ID     
COLUMN *  
COMMENT  
COMMIT *  
CONNECT *  
CONNECT_BY_ISCYCLE   
CONNECT_BY_ISLEAF    
CONNECT_BY_ROOT      
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
DISCONNECT *  
DISTINCT *  
DROP *  
ELSE *  
EMPTY         
END *  
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
INDEX         
INDICATOR *  
INNER *  
INOUT *  
INSERT *  
INTERSECT *  
INTO *  
IS *  
JOIN *  
LAST  
LATERAL         
LEADING *  
LEFT *  
LEVEL           
LIKE *  
LIMIT  
LOCAL *  
LOCALTIME *  
LOCALTIMESTAMP *  
LOCAL_OFFLINE   
LOCK            
MATCH *  
MEMBER *  
MERGE *  
MINUS  
NATURAL *  
NEW *  
NEXT  
NOAUDIT         
NONE            
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
OVER              
PACKAGE           
PHYSICAL_PAGE_ID  
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
ROWNUM           
ROWS *  
ROW_NUMBER *  
SAVEPOINT *  
SELECT *  
SEMI             
SESSION_USER *  
SET *  
SHARDING_HANDLE  
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
SYS_CONNECT_BY_PATH  
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
USAGE         
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

<a id="90bdf77163c3517c"></a>
#### SQL Keywords

GOLDILOCKS SQL keywords are not reserved words. However, they are keywords that are used internally by GOLDILOCKS. Therefore, it is not recommended to use GOLDILOCKS SQL keywords, as doing so can decrease the readability of the results.

The list of GOLDILOCKS SQL keywords can be viewed through [V$KEYWORDS](../part-02-administration-manual/9-database-information.md#972f4fbced8050ff).

<a id="d9d7b73fa6a50450"></a>
### Compatibility for Syntax Elements

The SQL standard compatibility for syntax element is as follows.

**SQL standard compatibility for syntax element**

<a id="53bfea8cda59b289"></a>
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

<a id="d31560e2b64a41fa"></a>
## Data Type

<a id="86054e752849e8bc"></a>
### Numeric Type

Numeric data types are classified based on their storage method and the representation of the fractional part.

- Classification by storage method 
    - Decimal numeric type
        - It stores decimal numbers on a 100-digit basis.
        - Types: NUMBER, NUMERIC, FLOAT
    - Binary numeric type 
        - It stores numbers in the same format as used in the C programming language.
        - Types: NATIVE_INTEGER, NATIVE_DOUBLE

- Classification by fractional part representation
    - Fixed point data type (exact numeric)
        - This numeric type has a fixed scale. 
        - Types: NUMERIC(precision, scale), NATIVE_INTEGER
    - Floating point data type (approximate numeric)
        - This numeric type has a variable scale. 
        - Types: FLOAT(precision), NATIVE_DOUBLE

<a id="901ef88227934714"></a>
#### Decimal Numeric Type

The precision and scale of this type are based on decimal numbers. Precision, which indicates the accuracy of valid digits, and scale, which defines the range of the fractional part, are based on decimal numbers.

<a id="9b2270bbb3a1a416"></a>
##### Decimal Fixed-Point Number Type

The decimal fixed-point number type is defined in SQL.

**Decimal fixed-point number type**

<a id="c9f804f24750e741"></a>
| Type | Decimal precision | Decimal scale | Refer to |
| --- | --- | --- | --- |
| NUMBER( p ) | p | 0 | [NUMBER](16-built-in-data-type-references.md#2f8065df8574cbef) |
| NUMBER( p, s ) | p | s | [NUMBER](16-built-in-data-type-references.md#2f8065df8574cbef) |
| NUMERIC( p ) | p | 0 | [NUMERIC](16-built-in-data-type-references.md#0c1a790db2a97db2) |
| NUMERIC( p, s ) | p | s | [NUMERIC](16-built-in-data-type-references.md#0c1a790db2a97db2) |
| DECIMAL( p ) | p | 0 | [NUMERIC](16-built-in-data-type-references.md#0c1a790db2a97db2) type alias |
| DECIMAL( p, s ) | p | s | [NUMERIC](16-built-in-data-type-references.md#0c1a790db2a97db2) type alias |
| DEC( p ) | p | 0 | [NUMERIC](16-built-in-data-type-references.md#0c1a790db2a97db2) type alias |
| DEC( p, s ) | p | s | [NUMERIC](16-built-in-data-type-references.md#0c1a790db2a97db2) type alias |
| SMALLINT | 5 | 0 | [NUMBER](16-built-in-data-type-references.md#2f8065df8574cbef) type alias |
| INTEGER | 10 | 0 | [NUMBER](16-built-in-data-type-references.md#2f8065df8574cbef) type alias |
| BIGINT | 19 | 0 | [NUMBER](16-built-in-data-type-references.md#2f8065df8574cbef) type alias |
| INT2 | 5 | 0 | [NUMBER](16-built-in-data-type-references.md#2f8065df8574cbef) type alias |
| INT4 | 10 | 0 | [NUMBER](16-built-in-data-type-references.md#2f8065df8574cbef) type alias |
| INT8 | 19 | 0 | [NUMBER](16-built-in-data-type-references.md#2f8065df8574cbef) type alias |

<a id="6514aa7e695e83e5"></a>
##### Decimal Floating Point Number Type

The decimal floating-point number type is defined in SQL.

**Decimal floating-point number type**

<a id="12958c06a75c68b9"></a>
| Type | Decimal precision | Decimal scale | Refer to |
| --- | --- | --- | --- |
| NUMBER | 38 | N/A | [NUMBER](16-built-in-data-type-references.md#2f8065df8574cbef) |
| FLOAT( p ) | ceil( log<sub>10</sub> 2<sup>p</sup> ) | N/A | [FLOAT](16-built-in-data-type-references.md#0ef612f8546e2023) |
| REAL | ceil( log<sub>10</sub> 2<sup>24</sup> ) = 8 | N/A | [FLOAT](16-built-in-data-type-references.md#0ef612f8546e2023) type alias |
| DOUBLE | ceil( log<sub>10</sub> 2<sup>53</sup> ) = 16 | N/A | [FLOAT](16-built-in-data-type-references.md#0ef612f8546e2023) type alias |
| FLOAT4 | ceil( log<sub>10</sub> 2<sup>24</sup> ) = 8 | N/A | [FLOAT](16-built-in-data-type-references.md#0ef612f8546e2023) type alias |
| FLOAT8 | ceil( log<sub>10</sub> 2<sup>53</sup> ) = 16 | N/A | [FLOAT](16-built-in-data-type-references.md#0ef612f8546e2023) type alias |

<a id="a9a4d1448aa9d210"></a>
#### Binary Number Type

The precision and scale of this type are based on binary numbers. Precision, which indicates the accuracy of valid digits, and scale, which defines the range of the fractional part, are based on binary numbers.

<a id="2a90f9f132b8c6b0"></a>
##### Binary Fixed-Point Number Type

The binary fixed-point number type refers to the signed integer data type in the C language.  
1 bit is used to represent the sign, while the remaining bits are used to represent the precision. However, no bits are used to represent the scale.

**Binary fixed-point number type**

<a id="32ccc6af024c03b0"></a>
| Type | Binary precision | Binary scale | Refer to |
| --- | --- | --- | --- |
| NATIVE_SMALLINT | 15 | 0 | [NATIVE_SMALLINT](16-built-in-data-type-references.md#e9fdbaf1b1795369) |
| NATIVE_INTEGER | 31 | 0 | [NATIVE_INTEGER](16-built-in-data-type-references.md#b54b66a89b51d7b5) |
| NATIVE_BIGINT | 63 | 0 | [NATIVE_BIGINT](16-built-in-data-type-references.md#a1fa84b35b583bfd) |

<a id="bcb7f05af96d215b"></a>
##### Binary Floating-Point Number Type

The binary floating-point type refers to the float and double data types in the C language.  
1 bit is used to represent the sign, while the remaining bits are used to represent both the precision and the scale.

**Binary floating-point number type**

<a id="582b3df1100be6c6"></a>
| Type | Binary precision | Binary scale | Refer to |
| --- | --- | --- | --- |
| NATIVE_REAL | 23 | 8 | [NATIVE_REAL](16-built-in-data-type-references.md#e668050ffd2fe5d3) |
| NATIVE_DOUBLE | 52 | 11 | [NATIVE_DOUBLE](16-built-in-data-type-references.md#b8657b67d632227e) |

> The precision and scale of the binary floating-point type can vary depending on the compiler and OS.

<a id="fe8fbca167dbf2d1"></a>
### CHARACTER STRING Type

CHARACTER STRING data types are classified based on whether they are variable-length strings and the maximum string length.

- Classification based on whether the string is variable-length
    - Fixed-length string
        - Refer to [CHARACTER](16-built-in-data-type-references.md#3d552befa621e8be).
    - Variable-length string 
        - Refer to [CHARACTER VARYING](16-built-in-data-type-references.md#03dae4745525807e), [CHARACTER LONG VARYING](16-built-in-data-type-references.md#1cc378ee86bc0d15).
- Classification based on maximum string length
    - 2000 [ characters or bytes ] 
        - Refer to [CHARACTER](16-built-in-data-type-references.md#3d552befa621e8be).
    - 4000 [ characters or bytes ] 
        - Refer to [CHARACTER VARYING](16-built-in-data-type-references.md#03dae4745525807e).
    - 100 megabytes 
        - Refer to [CHARACTER LONG VARYING](16-built-in-data-type-references.md#1cc378ee86bc0d15).

<a id="9be109305bce78d2"></a>
### BINARY STRING Type

BINARY STRING data types are classified based on whether they are variable-length binary strings and the maximum binary string length.

- Classification based on whether the binary string is variable-length
    - Fixed-length binary string 
        - Refer to [BINARY](16-built-in-data-type-references.md#fbf3d5ebb7224a2c).
    - Variable-length binary string 
        - Refer to [BINARY VARYING](16-built-in-data-type-references.md#0b0914f37f5ffeb8), [BINARY LONG VARYING](16-built-in-data-type-references.md#ae884d0ba0d97a74).
- Classification based on maximum binary string length
    - 2000 
        - Refer to [BINARY](16-built-in-data-type-references.md#fbf3d5ebb7224a2c).
    - 4000 
        - Refer to [BINARY VARYING](16-built-in-data-type-references.md#0b0914f37f5ffeb8).
    - 100 Mega Bytes 
        - Refer to [BINARY LONG VARYING](16-built-in-data-type-references.md#ae884d0ba0d97a74).

<a id="ed0bf66efb3053e7"></a>
### Date/ Time Type

The date/time data type specifies the year, month, day, hour, minute, second, and time zone offset,  according to its representation method.   
The date/time type includes the [DATE](16-built-in-data-type-references.md#e1a7517d0f63a48f), [TIME](16-built-in-data-type-references.md#726749f4da2c8c97), and [TIMESTAMP](16-built-in-data-type-references.md#3f728dfee44599c8) types.

<a id="92d3262e9cbfe041"></a>
### INTERVAL Type

The INTERVAL data type specifies a time interval.   
It specifies the interval in terms of years, months, days, hours, minutes, seconds according to its representation method.

[INTERVAL](16-built-in-data-type-references.md#3719f3256f650b0f) data types are classified into the YEAR TO MONTH family and the DAY TO SECOND family, based on the range of value representation.

<a id="e40ac31845a9313d"></a>
### BOOLEAN Type

The BOOLEAN data type stores truth values of TRUE, FALSE, and UNKNOWN. The UNKNOWN value is represented as a null value. All expressions used as conditions return a BOOLEAN value, and any column or value defined as a BOOLEAN data type can be used as a condition.

The following literals can be stored in the boolean data type.

- TRUE
    - Keyword: TRUE
    - Literal: 't', 'true' , 'y', 'yes' , 'on' ,'1'
- FALSE
    - Keyword: FALSE
    - Literal: 'f', 'false', 'n', 'no', 'off', '0'
- UNKNOWN
    - Keyword: UNKNOWN, NULL

For more information, refer to [BOOLEAN](16-built-in-data-type-references.md#ef47d9ed3ac8c254).

<a id="a5b5e29fc4114ffb"></a>
### ROWID Type

All records stored in the database have unique location information. The record identifier (ROWID) is used to distinguish each record.

The ROWID data type is used to store and manage the record identifier (ROWID).  
The record identifier (ROWID) is obtained by querying the ROWID pseudo column.

For more information, refer to [ROWID](16-built-in-data-type-references.md#72823db80276ccca).

<a id="9411d3a5627fa793"></a>
### Type Comparison

Comparing two types is done based on a single   representative type. If the  types being compared are different from the representative type, a type conversion may occur.  
[The representative types for type comparison](#2a410f10403ff966) define the type used as the reference for comparison.

The following table describes the target type conversion for comparison based on each representative type.

- [ Type conversion for the VC comparison](#76773664cdf8e3fe)
- [Type conversion for the LC comparison](#4e11afc21cc74fa5)
- [Type conversion for the VB comparison](#4dda73d981de25e3)
- [Type conversion for the LB comparison](#5254715fdbe922f5)
- [Type conversion for the NB comparison](#7cd5cbc57010022b)
- [Type conversion for the ND comparison](#ec1f7d08865321ed)
- [Type conversion for the NU comparison](#842343fa473c6c45)
- [Type conversion for the DA comparison](#2cc39ad45bae6411)
- [Type conversion for the TI comparison](#8dc60795f6019df3)
- [Type conversion for the TZ comparison](#24e42eba85bb849b)
- [Type conversion for the TS comparison](#dc12f7bc001cec95)
- [Type conversion for the SZ comparison](#0d48b805b7aa4230)
- [Type conversion for the YM comparison](#67a69e4569c90282)
- [Type conversion for the DS comparison](#499bb7f4251da66e)
- [Type conversion for the BO comparison](#4a61d16105e46fed)
- [Type conversion for the RI comparison](#23a66ce058c0d27d)

> The following are the abbreviations used for type comparison.
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

> In the type comparison table, built-in data types are represented by abbreviated words enclosed in double quotes ("").
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

**Representative types for type comparison**

<a id="2a410f10403ff966"></a>
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

**Type conversion for VC comparison**

<a id="76773664cdf8e3fe"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | CHAR (no conversion) |
| VARCHAR | VARCHAR (no conversion) |

**Type conversion for LC comparison**

<a id="4e11afc21cc74fa5"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | CHAR (no conversion) |
| VARCHAR | VARCHAR (no conversion) |
| LONG VARCHAR | LONG VARCHAR (no conversion) |

**Type conversion for VB comparison**

<a id="4dda73d981de25e3"></a>
| Source type | Converted type |
| --- | --- |
| BINARY | BINARY (no conversion) |
| VARBINARY | VARBINARY (no conversion) |

**Type conversion for LB comparison**

<a id="5254715fdbe922f5"></a>
| Source type | Converted type |
| --- | --- |
| BINARY | BINARY (no conversion) |
| VARBINARY | VARBINARY (no conversion) |
| LONG VARBINARY | LONG VARBINARY (no conversion) |

**Type conversion for NB comparison**

<a id="7cd5cbc57010022b"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | NATIVE_BIGINT |
| VARCHAR | NATIVE_BIGINT |
| LONG VARCHAR | NATIVE_BIGINT |
| NATIVE_SMALLINT | NATIVE_SMALLINT (no conversion) |
| NATIVE_INTEGER | NATIVE_INTEGER (no conversion) |
| NATIVE_BIGINT | NATIVE_BIGINT (no conversion) |

**Type conversion for ND comparison**

<a id="ec1f7d08865321ed"></a>
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

**Type conversion for NU comparison**

<a id="842343fa473c6c45"></a>
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

**Type conversion for DA comparison**

<a id="2cc39ad45bae6411"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | DATE |
| VARCHAR | DATE |
| LONG VARCHAR | DATE |
| DATE | DATE (no conversion) |

**Type conversion for TI comparison**

<a id="8dc60795f6019df3"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | TIME |
| VARCHAR | TIME |
| LONG VARCHAR | TIME |
| TIME | TIME (no conversion) |

**Type conversion for TZ comparison**

<a id="24e42eba85bb849b"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | TIME_TZ |
| VARCHAR | TIME_TZ |
| LONG VARCHAR | TIME_TZ |
| TIME | TIME_TZ |
| TIME_TZ | TIME_TZ (no conversion) |

**Type conversion for TS comparison**

<a id="dc12f7bc001cec95"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | TIMESTAMP |
| VARCHAR | TIMESTAMP |
| LONG VARCHAR | TIMESTAMP |
| DATE | DATE (no conversion) |
| TIMESTAMP | TIMESTAMP (no conversion) |

**Type conversion for SZ comparison**

<a id="0d48b805b7aa4230"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | TIMESTAMP_TZ |
| VARCHAR | TIMESTAMP_TZ |
| LONG VARCHAR | TIMESTAMP_TZ |
| DATE | TIMESTAMP_TZ |
| TIMESTAMP | TIMESTAMP_TZ |
| TIMESTAMP_TZ | TIMESTAMP_TZ (no conversion) |

**Type conversion for YM comparison**

<a id="67a69e4569c90282"></a>
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

**Type conversion for DS comparison**

<a id="499bb7f4251da66e"></a>
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

**Type conversion for BO comparison**

<a id="4a61d16105e46fed"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | BOOLEAN |
| VARCHAR | BOOLEAN |
| LONG VARCHAR | BOOLEAN |
| BOOLEAN | BOOLEAN (no conversion) |

**Type conversion for RI comparison**

<a id="23a66ce058c0d27d"></a>
| Source type | Converted type |
| --- | --- |
| CHAR | ROWID |
| VARCHAR | ROWID |
| LONG VARCHAR | ROWID |
| ROWID | ROWID (no conversion) |

<a id="fc718a805c53e7ba"></a>
### Type Conversion

Type conversions are classified into implicit and explicit type conversions.

- Implicit type conversion occurs in expressions, operators, functions, conditions, and in operations such as SELECT, INSERT, DELETE, and UPDATE.
- Explicit type conversion is performed using the CAST operator.

[The availability of type conversion](#ce42903a6a9a1959) refers to the ability to convert a data type from one type  to another.

> In the type conversion table, built-in data types are represented by abbreviated strings enclosed in double quotes ("").
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

<a id="ce42903a6a9a1959"></a>
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
        - If the source type precision is greater than the CHARACTER type precision, an error occurs.
        - If the source type precision equals the CHARACTER type precision, the string remains unchanged.
        - If the source type precision is smaller than the CHARACTER type precision, spaces are added to the string to fill the precision difference.
    - When the source type is CHARACTER VARYING or CHARACTER LONG VARYING type: 
        - If the source type string length exceeds the CHARACTER type precision, an error occurs.
        - If the source type string length equals the CHARACTER type precision, the string remains unchanged.
        - If the source type string length is smaller than the CHARACTER type precision, spaces are added to the string to fill the precision difference.
    - When the source type is numeric, date/time, INTERVAL, BOOLEAN, or ROWID type:
        - If the converted string length of the source type exceeds the CHARACTER type precision, an error occurs.
        - If the converted string length of the source type equals the CHARACTER type precision, the string remains unchanged.
        - If the converted string length of the source type is smaller than the CHARACTER type precision, spaces are added to the string to fill the precision difference.

- Conversion to CHARACTER VARYING type 
    - When the source type is CHARACTER type: 
        - If the source type precision is greater than the CHARACTER VARYING type precision, an error occurs.
        - If the source type precision is smaller than or equal to the CHARACTER VARYING type precision, the string remains unchanged.
    - When the source type is CHARACTER VARYING or CHARACTER LONG VARYING type:
        - If the source type string length exceeds the CHARACTER VARYING type precision, an error occurs.
        - If the source type string length is smaller than or equal to the CHARACTER VARYING type precision, the string remains unchanged.
    - When the source type is a numeric, date/time, INTERVAL, BOOLEAN or ROWID type: 
        - If the converted string length of the source type exceeds the CHARACTER VARYING type precision, an error occurs.
        - If the converted string length of the source type is smaller than or equal to the CHARACTER VARYING type precision, the string remains unchanged.

- Conversion to CHARACTER LONG VARYING type
    - When the source type is CHARACTER STRING type:
        - The source type string remains unchanged.
    - When the source type is a numeric, date/time, INTERVAL, BOOLEAN or ROWID type:
        - The converted string of the source type remains unchanged.

- Conversion to BINARY type 
    - When the source type is BINARY type: 
        - If the source type precision is greater than the BINARY type precision, an error occurs.
        - If the source type precision equals the BINARY type precision, the binary string remains unchanged. 
        - If the source type precision is smaller than the BINARY type precision, the X'00' characters are added to the binary string to fill the precision difference.
    - When the source type is BINARY VARYING or BINARY LONG VARYING type: 
        - If the source type binary string length exceeds the BINARY type precision, an error occurs.
        - If the source type binary string length equals the BINARY type precision, the binary string remains unchanged. 
        - If the source type binary string length is smaller than the BINARY type precision, the X'00' characters are added to the binary string to fill the precision difference.

- Conversion to BINARY VARYING type 
    - When the source type is BINARY type: 
        - If the source type precision is greater than the BINARY VARYING type precision, an error occurs. 
        - If the source type precision is smaller than or equal to the BINARY VARYING type precision, the binary string remains unchanged.
    - When the source type is BINARY VARYING or BINARY LONG VARYING type: 
        - If the source type binary string length exceeds the BINARY VARYING type precision, an error occurs.
        - If the source type binary string length is smaller than or equal to the BINARY VARYING type precision, the binary string remains unchanged.

- Conversion to BINARY LONG VARYING type 
    - If the source type is BINARY STRING type, the source type binary string remains unchanged.

- Conversion to numeric type
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the numeric format, an error occurs. 
        - An overflow or rounding may occur due to the precision and scale defined in the converted type.
    - When the source type is numeric type: 
        - An overflow or rounding may occur due to the precision and scale defined in the converted type.
    - When the source type is INTERVAL type: 
        - It can be converted to the numeric type only when the source type is a single field (YEAR, MONTH, DAY, HOUR, MINUTE, SECOND).
        - An overflow or rounding may occur due to the precision and scale defined in the converted type.

- Conversion to DATE type
    - When the source type is CHARACTER STRING type:
        - If the string does not comply with the DATE type format, an error occurs.
        - An overflow may occur due to the value range defined in the converted type.
    - When the source type is DATE or TIMESTAMP type:
        - No error will occur.
    - When the source type is TIMESTAMP WITH TIME ZONE type:
        - It will be converted to a DATE type value, taking the time zone offset into account.

- Conversion to TIME type 
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the TIME type format, an error occurs. 
        - A rounding may occur due to the value range defined in the converted type.
    - When the source type is TIME or TIMESTAMP type: 
        - No error will occur.
    - When the source type is TIME WITH TIME ZONE or TIMESTAMP WITH TIME ZONE type: 
        - It will be converted to a TIME type value, taking the time zone offset into account.

- Conversion to TIME WITH TIME ZONE type 
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the TIME WITH TIME ZONE type format, an error occurs. 
        - A rounding may occur due to the value range defined in the converted type.
    - When the source type is TIME, TIME WITH TIME ZONE, or TIMESTAMP WITH TIME ZONE type: 
        - It will be converted to a TIME WITH TIME ZONE type value, taking the time zone offset into account.

- Conversion to TIMESTAMP type 
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the TIMESTAMP type format, an error occurs. 
        - An overflow or rounding may occur due to the value range defined in the converted type.
    - When the source type is DATE or TIMESTAMP type:
        - No error will occur.
    - When the source type is TIMESTAMP WITH TIME ZONE type: 
        - It will be converted to a TIMESTAMP type value, taking the time zone offset into account.

- Conversion to TIMESTAMP WITH TIME ZONE type 
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the TIMESTAMP WITH TIME ZONE type format, an error occurs. 
        - An overflow or rounding may occur due to the value range defined in the converted type.
    - When the source type is DATE, TIMESTAMP, or TIMESTAMP WITH TIME ZONE type: 
        - It will be converted to a TIMESTAMP WITH TIME ZONE type value, taking the time zone offset into account.

- Conversion to INTERVAL YEAR TO MONTH family type
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the year-month interval literal format, an error occurs. 
        - For more information, refer to [Interval Literals](#daf1003f657050c1).
        - An overflow may occur due to the precision defined in the converted type.
    - When the source type is NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, NUMBER, NUMERIC or FLOAT type: 
        - The converted type should consist of a single field (YEAR, MONTH).
        - An overflow may occur due to the precision defined in the converted type.
    - When the source type is INTERVAL YEAR TO MONTH family type: 
        - An overflow may occur due to the precision defined in the converted type.

- Conversion to INTERVAL DAY TO SECOND family type 
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the day-time interval literal format, an error occurs. 
        - For more information, refer to [Interval Literals](#daf1003f657050c1).
        - An overflow or rounding may occur due to the precision defined in the converted type.
    - When the source type is NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, NUMBER, NUMERIC, or FLOAT type:
        - The converted type should consist of a single field (DAY, HOUR, MINUTE, SECOND)
        - An overflow or rounding may occur due to the precision defined in the converted type.
    - When the source type is INTERVAL DAY TO SECOND family type: 
        - An overflow or rounding may occur due to the precision defined in the converted type.

- Conversion to BOOLEAN type 
    - When the source type is CHARACTER STRING type: 
        - Conversion is possible when the string is "TRUE" or "FALSE", and it is case-insensitive. (Conversion is also allowed when there are spaces before or after the string.) 
    - When the source type is BOOLEAN type: 
        - No error will occur.

- Conversion to ROWID type 
    - When the source type is CHARACTER STRING type: 
        - If the string does not comply with the ROWID type format, an error occurs. 
    - When the source type is ROWID type: 
        - No error will occur.

<a id="85d98cdf6ed395fe"></a>
### Type Combination

<a id="ca852303f34544c3"></a>
#### When Type Combination Is Required

The CASE operator and [set operator](20-sql-references-h-z.md#1e4cbe254403f053) produce multiple expressions as the result of the operation.  
When, as in the example below, each expression has a different type, the result type must be determined.

- The following describes the execution result of a CASE operator.

```
SELECT CASE expr WHEN expr THEN char(3)
                 WHEN expr THEN char(5)
                 ELSE char(1)
       END   
  FROM t1;
```

- The following describes the execution result of a set operator.

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

A rule is applied to determine the result type based on the combination of types. The following is an example of how the rule is applied.

- Result type combination rule
    - [set operator](20-sql-references-h-z.md#1e4cbe254403f053)
    - CASE operator
        - [CASE Expression](#2c1180b7f27274c8)
        - [COALESCE](17-built-in-function-references.md#8ecf82e319ad8324)
        - [NULLIF](17-built-in-function-references.md#aef2dc5f3ce03844)

<a id="4c0e2485bf66d2d0"></a>
#### Result Type Combination Rule

Each expression's data type must belong to the same family of types that can be combined.

- Examples of applying the result type combination rule
    - [set operator](20-sql-references-h-z.md#1e4cbe254403f053)
    - CASE operator
        - [CASE Expression](#2c1180b7f27274c8)
        - [COALESCE](17-built-in-function-references.md#8ecf82e319ad8324)
        - [NULLIF](17-built-in-function-references.md#aef2dc5f3ce03844)

The result types determined by the result type combination rule are shown in the table below.

> The following abbreviations are used to describe the result type combination rules.
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

> In the result type combination table, built-in data types are represented by abbreviated words enclosed in double quotes ("").
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

**The result type determined by the result type combination rule**

<a id="31361ae14b18b486"></a>
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

- Result type when all expressions are CHAR type
    - If the lengths are different, the result type is VARCHAR.
    - If the lengths are equal, the result type is CHAR.
- Result type when all expressions are BINARY type
    - If the lengths are different, the result type is VARBINARY.
    - If the lengths are equal, the result type is BINARY.
- Result type of INTERVAL YEAR TO MONTH type
    - If YEAR and MONTH types are mixed, the result type is INTERVAL YEAR TO MONTH.
    - If only YEAR type is used, the result type is INTERVAL YEAR.
    - If only MONTH type is used, the result type is INTERVAL MONTH.
- Result type of INTERVAL DAY TO SECOND
    - The start field is the largest range field of each target expression.
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
- For more information, refer to [Type Comparison](#9411d3a5627fa793).

<a id="be494b5eb3deea8b"></a>
### Compatibility for Data Type

The SQL standard compatibility for data type is as follows.

**SQL standard compatibility for data types**

<a id="9559368953dad960"></a>
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

<a id="19f3f91083d596f3"></a>
## Format String

A format string defines the format used when a numeric type or date/time type is converted to a character string, or when a character string is converted to a numeric type or date/time type.

- When converting a numeric type or date/time type to a character string type, the string is represented in the following format.
    - Refer to [TO_CHAR( number )](17-built-in-function-references.md#06e9d7b88a3c7d10), [TO_CHAR( datetime )](17-built-in-function-references.md#5f3a74b3e90ec4f6).
    - Numeric type: TO_CHAR( 1234.56, 'S9,999.99' ) → '+1,234.56'
    - Date/time type: TO_CHAR( SYSDATE, 'YYYY-MM-DD' ) → '2012-07-15'
- When converting a character string to the numeric type or date/time type, the string is represented in the following format.
    - Refer to [TO_NUMBER](17-built-in-function-references.md#a547796f56907926), [TO_NATIVE_REAL](17-built-in-function-references.md#d1401c04ea742970), [TO_NATIVE_DOUBLE](17-built-in-function-references.md#37b2e9541ce0eb78). 
    - Refer to [TO_DATE](17-built-in-function-references.md#74b46ad0bc9dbb10).
    - Refer to [TO_TIMESTAMP](17-built-in-function-references.md#b03348c605444fea), [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#785d71b6e8e5c13b).
    - Refer to [TO_TIME](17-built-in-function-references.md#369e424a6a243c31), [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#7d0b935c0acaee3f) .
    - Numeric type: TO_NUMBER( '+1,234.56', 'S9,999.99' ) → NUMBER TYPE
    - Date/time type: TO_DATE( '2012-07-15', 'YYYY-MM-DD' ) → DATE TYPE

Format strings are classified by type.  
• Numeric data type: Refer to [Number Format String](#8dde7bcd7362fc93).  
• Date/time type: Refer to [Datetime Format String](#c0861393ec3cf3cf).

<a id="8dde7bcd7362fc93"></a>
### Number Format String

The number format string defines the format used when a numeric type is converted to a character string, or when a character string is converted to a numeric type.

The number format string is used as an argument in functions such as [TO_CHAR( number )](17-built-in-function-references.md#06e9d7b88a3c7d10), [TO_NATIVE_SMALLINT](17-built-in-function-references.md#194e111618562fc9), [TO_NATIVE_INTEGER](17-built-in-function-references.md#b7ba82a1d907f3c6), [TO_NATIVE_BIGINT](17-built-in-function-references.md#a0f4163ceae2b2da), [TO_NUMBER](17-built-in-function-references.md#a547796f56907926), [TO_NATIVE_REAL](17-built-in-function-references.md#d1401c04ea742970), [TO_NATIVE_DOUBLE](17-built-in-function-references.md#37b2e9541ce0eb78).

The number format string can specify multiple format elements based on the desired format.

All number format elements are rounded to fit the specified format.  
If the number of digits before the decimal point in the value to be converted exceeds the number of digits specified in the format string, the extra digits are replaced with the # character.  
If the format element representing the sign of MI, S, PR is not specified, a negative number will display a - sign, and a positive number will have a space in front.

**Number format elements**

<a id="4db239d3bd6bd1f3"></a>
| Format  element | Example | Description |
| --- | --- | --- |
| , (comma) | 9,999 | It returns a comma to the specified position. Multiple commas can be specified. The format string can not begin with a comma, nor can a comma appear after the decimal point (.). |
| . (period) | 99.99 | It returns a decimal point (.) to the specified position. The decimal point in the format string can only be specified once. |
| $ | $9999 | It returns the $ sign to the front of the number. |
| 0 | 0999  9990 | It returns a zero (0) to the front or the end of the number.  If the number of digits in the value to be converted is smaller than the number of digits to the zero position in the format string, the gap is filled with zero (0)s and returned. |
| 9 | 9999 | It returns a white space and numbers according to the sign and the number of specified 9. If the number of digits in the value to be converted is smaller than the number of specified 9, the gap is filled with white spaces and returned. For a positive number, a white space is returned to the front of the number. For a negative number, a '-' symbol is returned to the front of the number. If the value before the decimal point in the format string is 0, a white space is returned instead of 0. e.g. TO_CHAR( 0.123, '9.999' ) → .123 e.g. TO_CHAR( 0, '9' ) → 0 |
| B | B9999 | If the value is zero, a white space is returned. |
| EEEE | 9.9EEEE | It returns the value in exponential notation. It can appear at the end of the format string or in front of S, MI, or PR.  It can not be specified together with a comma (,). |
| MI | 9999MI | For a positive number, a white space is returned to the end of the number. For a negative number, a '-' symbol is returned to the end of the number. It can only be specified at the end of the format string and can not be used together with S or PR. |
| PR | 9999PR | For a positive number, white spaces are returned to both the beginning and end of the number. For a negative number, it returns the number enclosed within angle brackets. &lt;number&gt;  It can only be specified at the end of the format string, and can not be used together with S or MI. |
| RN  rn | RN rn | Roman numerals are converted to uppercase and returned. (RN) Roman numerals are converted to lowercase and returned. (rn) Only numbers between 1 ~ 3999 are supported. It can only be used together with the FM format element and can not be combined with any other format elements. It can not be used in the TO_NUMBER function. |
| S | S9999 9999S | For a positive number, a '+' symbol is returned to the front of the number. For a negative number, a '-' symbol is returned to the front of the number. (S9999) For a positive number, a '+' symbol is returned to the end of the number. For a negative number, a '-' symbol is returned to the end of the number. (9999S) It can only be specified at the beginning or at the end of the format string. It can not be used together with MI or PR. |
| V | 999V99 | When the number of digits of 9 following the V format element is n, the value is multiplied by 10<sup>n</sup>. It can not be specified together with a decimal point (.). It can not be used in the TO_NUMBER function. |
| X | XXXX xxxx | It returns a white space and a hexadecimal number based on the specified number of X digits. The integer value is converted to a hexadecimal number and returned. (Non-integer values are rounded to the nearest integer.) XXX returns hexadecimal digits in uppercase letters, while xxxx returns them in lowercase letters. If the number of converted hexadecimal digits is smaller than the number specified by X, the gap is filled with white spaces. Only 0 and positive integers are processed, and negative numbers are replaced with '#'. It can only be used with the 0 and FM format elements, but can not be combined with any other format elements. |
| FM | FM | It removes the leading and trailing white spaces, and returns a left-aligned effect. It removes the leading and trailing white spaces from the number. It removes the zeros (0) added after the decimal point by the 9 format element. |

Following are examples of using number format strings.

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

<a id="c0861393ec3cf3cf"></a>
### Datetime Format String

The datetime format string is a string that defines the format used to convert a date/time value to a string, or to convert a string to a date/time value.

A datetime format string is used as an argument in functions such as [TO_CHAR( datetime )](17-built-in-function-references.md#5f3a74b3e90ec4f6), [TO_DATE](17-built-in-function-references.md#74b46ad0bc9dbb10), [TO_TIMESTAMP](17-built-in-function-references.md#b03348c605444fea), [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#785d71b6e8e5c13b), and [TO_TIME](17-built-in-function-references.md#369e424a6a243c31), [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#7d0b935c0acaee3f).

For a datetime format string, if no format is specified, the default value is used. The default value for each type is defined in the session property (NLS _ * _ FORMAT).

- DATE: Refer to [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#86120b98fe0558e4).
- TIMESTAMP: Refer to [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#5129c923d9116f8d).
- TIMESTAMP WITH TIME ZONE: Refer to [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#8a228be667cdaef8).
- TIME: Refer to [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#b303d4bd630c0388).
- TIME WITH TIME ZONE: Refer to [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#81aefd62dd9e1a5a).

NLS * _FORMAT values can be modified using the [ALTER SESSION SET property_name](18-sql-references-a-b.md#a7df2194f3a8476a).

In a datetime format string, multiple format elements can be specified to achieve the desired representation.

**Datetime format elements**

<a id="5ee5d838082df247"></a>
<table><thead><tr><th align="center" valign="middle">Format<br>element</th><th align="center" valign="middle">Whether to use TO_*<br>datetime</th><th align="center" valign="middle">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">-<br>/<br>,<br>.<br>;<br>:<br>"text"<br>Special characters</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the character of the format element to the specified location.</td></tr><tr><td align="left" valign="middle">AD<br>A.D.</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">AD, with or without periods.</td></tr><tr><td align="left" valign="middle">AM<br>A.M.</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">AM, with or without periods.</td></tr><tr><td align="left" valign="middle">BC<br>B.C.</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">BC, with or without periods.</td></tr><tr><td align="left" valign="middle">CC</td><td align="left" valign="middle">N</td><td align="left" valign="middle">Century<br>If the last two digits of a four-digit year are between 01 and 99, the value obtained by adding one to the first two digits is returned. (e.g. If the year is 2005, 21 is returned.)<br>If the last two digits of the four-digit year are 00, the first two digits are returned. (e.g. If the year is 2000, 20 is returned.)</td></tr><tr><td align="left" valign="middle">D</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the day number of the week (1 to 7).<br>Sunday is 1, Saturday is 7, and so on.</td></tr><tr><td align="left" valign="middle">DAY<br>Day<br>day</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the day of the week. (e.g. SUNDAY )<br><ul><li>DAY: It returns the day in uppercase.</li><li>Day: It returns the day with the first letter capitalized and the rest in lowercase.</li><li>day: It returns the day in lowercase.</li></ul></td></tr><tr><td align="left" valign="middle">DD</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the day of the month (1 to 31).</td></tr><tr><td align="left" valign="middle">DDD</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the day of the year (1 to 366).</td></tr><tr><td align="left" valign="middle">DY<br>Dy<br>dy</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the abbreviated form of the day of the week. (e.g. SUN)<br><ul><li>DY: It returns the day in uppercase.</li><li>Dy: It returns the day with the first letter capitalized and the rest in lowercase.</li><li>dy: It returns the day in lowercase.</li></ul></td></tr><tr><td align="left" valign="middle">FF[1..6]</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns fractional seconds with the number of digits specified after "FF" (1 to 6).<br>If no number is specified, the default value is 6 (i.e., "FF" is equivalent to "FF6").<br>If the number of fractional second digits exceeds the number specified after FF, they are rounded down.<br>If the number of fractional second digits is fewer than the number specified after FF, zeros (0) are added to match the specified number.<br>It can not be used with the DATE type.</td></tr><tr><td align="left" valign="middle">HH<br>HH12</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">The hour (1 ~ 12)</td></tr><tr><td align="left" valign="middle">HH24</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">The hour (0 ~ 23)</td></tr><tr><td align="left" valign="middle">IW</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The week containing the first Thursday of the year is designated as the first calendar week according to the ISO 8601 standard (week 1 to 52 or 1 to 53).<br><ul><li>The calendar week starts on Monday.</li><li>The first calendar week always include January 4th.</li><li>The first calendar week may also include December 29th, 30th, and 31st.</li><li>The last calendar week may include January 1st, 2nd, and 3rd.</li></ul></td></tr><tr><td align="left" valign="middle">IYYY</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The 4-digit year that contains the calendar week defined by the ISO 8601 standard.</td></tr><tr><td align="left" valign="middle">IYY<br>IY<br>I</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The 3-digit year that contains the calendar week defined by the ISO 8601 standard<br>The 2-digit year that contains the calendar week defined by the ISO 8601 standard<br>The single digit year that contains the calendar week defined by the ISO 8601 standard</td></tr><tr><td align="left" valign="middle">J</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Julian day: The number of days since November 24, 4714 BC</td></tr><tr><td align="left" valign="middle">MI</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Minute (0 ~ 59)</td></tr><tr><td align="left" valign="middle">MM</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Month (01 ~ 12), January (01) ~ December (12)</td></tr><tr><td align="left" valign="middle">MON<br>Mon<br>mon</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">The abbreviated form of the month (e.g. JAN)<br><ul><li>MON: It returns the month in uppercase.</li><li>Mon: It returns the month with the first letter capitalized and the rest in lowercase.</li><li>mon: It returns the month in lowercase.</li></ul></td></tr><tr><td align="left" valign="middle">MONTH<br>Month<br>month</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">The month name (e.g. JANUARY )<br><ul><li>MONTH: It returns the month name in uppercase.</li><li>Month: It returns the month name with the first letter capitalized and the rest in lowercase.</li><li>month: It returns the month name in lowercase.</li></ul></td></tr><tr><td align="left" valign="middle">PM<br>P.M.</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">PM, with or without periods.</td></tr><tr><td align="left" valign="middle">Q</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The quarter of the year (1 ~ 4)<br>January to March is 1 and October to December is 4.</td></tr><tr><td align="left" valign="middle">RM<br>Rm<br>rm</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the Roman numeral for the month. (e.g. I)<br><ul><li>RM: It returns the Roman numeral in uppercase.</li><li>Rm: It returns the Roman numeral with the first letter capitalized and the rest in lowercase.</li><li>rm: It returns the Roman numeral in lowercase.</li></ul></td></tr><tr><td align="left" valign="middle">RR</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Adjusted two-digit year<br>The two-digit year represented by RR can be converted to a four-digit year as follows.<br><ul><li>When the two-digit year (RR) is between 00 and 49:<br><ul><li>If the last two digits of the current year are between 00 and 50,<br><ul><li>the four-digit year is formed using the first two digits of the current year and the two digits represented by RR.</li></ul></li><li>If the last two digits of the current year are between 51 and 99,<br><ul><li>the four-digit year is formed using the first two digits of the current year+1, and the two digits represented by RR.</li></ul></li></ul></li><li>When the two-digit year (RR) is between 50 and 99:<br><ul><li>If the last two digits of the current year are between 00 and 50,<br><ul><li>the four-digit year is formed using the first two digits of the current year - 1, and the two digits represented by RR.</li></ul></li><li>If the last two digits of the current year are between 51 and 99,<br><ul><li>the four-digit year is formed using the first two digits of the current year and the two digits represented by RR.</li></ul></li></ul></li></ul></td></tr><tr><td align="left" valign="middle">RRRR</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Adjusted four-digit year<br>Both two-digit and four-digit years can be input.<br>Two-digit input is processed the same way as RR</td></tr><tr><td align="left" valign="middle">SS</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Second (0 ~ 59)</td></tr><tr><td align="left" valign="middle">SSSSS</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Seconds since the last midnight (0 ~ 86399)</td></tr><tr><td align="left" valign="middle">TZH</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Time Zone Hour<br>This can not be used with DATE, TIMESTAMP, or TIME types. It is available for use with TIMESTAMP WITH TIME ZONE, and TIME WITH TIME ZONE types.</td></tr><tr><td align="left" valign="middle">TZM</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Time Zone Minute<br>This can not be used with DATE, TIMESTAMP, or TIME types. It can only be used with TIMESTAMP WITH TIME ZONE and TIME WITH TIME ZONE types.</td></tr><tr><td align="left" valign="middle">WW</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The sequence of the week in a year. (1~ 53)<br>Week 1 starts on the first day of the year and continues through to the seventh day of the year.</td></tr><tr><td align="left" valign="middle">W</td><td align="left" valign="middle">N</td><td align="left" valign="middle">The sequence of the week in a month. (1 ~ 5)<br>Week 1 starts on the first day of the month and ends on the seventh day.</td></tr><tr><td align="left" valign="middle">Y,YYY</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">It returns the year in the "Y,YYY" format, with a comma separating the thousands.</td></tr><tr><td align="left" valign="middle">YYYY<br>SYYYY</td><td align="left" valign="middle">Y</td><td align="left" valign="middle">Four-digit year.<br>SYYYY displays the sign of the year.<br><ul><li>If the year is BC, it displays a '-'. If the year is AD, it displays a ' '.</li></ul></td></tr><tr><td align="left" valign="middle">YYY<br>YY<br>Y</td><td align="left" valign="middle">Y</td><td align="left" valign="middle"><ul><li>YYY: The last three digits of the current year</li><li>YY: The last two digits of the current year</li><li>Y: The last digit of the current year</li></ul></td></tr></tbody></table>

The following are examples of using a datetime format string.

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

<a id="f3a30ecf2e1cfcc4"></a>
## Expressions

An expression is a combination of values, operators, and functions used to retrieve data.

The following shows the positions in SQL where expressions can be used.  
• Target clause in SELECT  
• GROUP BY clause in SELECT  
• ORDER BY clause in SELECT  
• WHERE clause and HAVING clause in SELECT  
• INSERT VALUES clause  
• UPDATE SET clause  
• RETURN clause in INSERT, DELETE, UPDATE

Expression types are as follows.  
• Simple expression  
• Compound expression  
• Boolean value expression  
• Case expression  
• Datetime expression  
• Scalar subquery expression  
• Sequence manipulation expression

Simple expressions include columns, pseudo-columns, literals, and null values.  
Compound expressions are combinations of multiple expressions.

For more information, refer to the following.  
•  [Null Value](#d9e7f612fecde5cf)  
•  [Literals](#013e0dda4b33d931)  
•  [Pseudo Columns](#f67e0c248cd3d29d)  
•  [Operators](#b554f8b97f2d370f)  
•  [Functions](#45f0cb169e5de3b6)

<a id="764f98d4c4d82703"></a>
### Boolean Value Expression

<a id="f6814dd335623288"></a>
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

<a id="0f552533bea1c013"></a>
#### Description

A &lt;boolean value expression&gt; describes a boolean value. &lt;boolean primary&gt; expressions that have a boolean value include &lt;column&gt;, &lt;condition&gt;, and &lt;boolean predicand&gt;. A &lt;column&gt; must be declared as the BOOLEAN type, but it can also return a boolean value using CAST.

A &lt;boolean value expression&gt; can be used with logical operators such as AND, OR, and NOT, and supports boolean-specific operators like IS and IS NOT.

The IS and IS NOT operators, as described in &lt;boolean test&gt;, determine whether the boolean value in &lt;boolean primary&gt; matches one of the &lt;truth value&gt; (TRUE, FALSE, UNKNOWN).

For more information, refer to [Conditions](#e7913ce53ce3e011).

<a id="2d816aa2f54baef3"></a>
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

<a id="2c1180b7f27274c8"></a>
### CASE Expression

<a id="3b9206ddf6bf2dc0"></a>
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

<a id="d366a07f0e21b332"></a>
#### Description

The WHEN ... THEN clauses are evaluated in the order they appear in the CASE statement.  
If a comparison result is FALSE, the subsequent WHEN ... THEN clauses are evaluated until TRUE is encountered.  
If a comparison result is TRUE, the corresponding result is returned, and no further evaluations are performed.

• Simple case   
&nbsp;&nbsp;The comparison_expr in the CASE expr and the WHEN ... THEN clause is evaluated using the equal operation.     
&nbsp;&nbsp;(expr = comparison_expr).  
• Searched case  
&nbsp;&nbsp;The condition in the WHEN ... THEN clause is evaluated.

If all evaluations in the WHEN clauses result in FALSE, the result of the ELSE clause is returned.  
If the ELSE clause is omitted, NULL is returned.

If there are multiple types of results in the THEN or ELSE clauses, the result type is determined by the [Result Type Combination Rule](#4c0e2485bf66d2d0).

For more information, refer to the following.  
• [COALESCE](17-built-in-function-references.md#8ecf82e319ad8324)  
• [NULLIF](17-built-in-function-references.md#aef2dc5f3ce03844)

<a id="c62a0b6f123cc8a0"></a>
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

<a id="c59692d02b604656"></a>
### CAST Specification

<a id="f98b0f995303f008"></a>
#### Syntax

```
CAST( expression AS data_type )
```

<a id="93aeec92ed3120d4"></a>
#### Description

CAST converts the data type of an expression to the specified data_type.

<a id="1f9f4be6e94cb55d"></a>
#### Example

```
gSQL> SELECT CAST( '1-2' AS INTERVAL YEAR TO MONTH ) AS RESULT FROM DUAL;  
RESULT
------
+01-02
1 row selected.
```

<a id="8329d99814ce23d2"></a>
### Scalar Subquery Expression

A scalar subquery expression is a subquery that returns a single row with one column as a result. The result of the scalar subquery expression is the value(s) specified in the subquery's select list.

If the subquery does not return any rows, the result is NULL, and if it returns two or more rows, an error occurs.

A scalar subquery expression can be described in most positions where an expression is allowed, but the subquery must be enclosed in parentheses. Even when a scalar subquery expression is used as an argument in a function and is already enclosed in parentheses, it must be enclosed in separate parentheses for the subquery itself. Otherwise, an error will occur.

The following is an example of using a scalar subquery expression.

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

<a id="bd8b3d3e1a75cab3"></a>
### Compatibility

The SQL standard compatibility for expressions is as follows.

**SQL standard compatibility for expressions**

<a id="3409ec74d2258e8c"></a>
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

<a id="f67e0c248cd3d29d"></a>
## Pseudo Columns

A pseudo column is similar not only to a function, but also to a table column, as it can return a different value for each row every time it is executed.

**Supported pseudo column**

<a id="9ea03bd2f233fbdf"></a>
<table><tbody><tr><th align="center">Name</th><th align="center">Description</th><th align="center">Refer to</th></tr><tr><td align="left" valign="middle">CURRVAL</td><td align="left" valign="middle">It is a pseudo column associated with a sequence.</td><td align="left" valign="middle"><a href="17-built-in-function-references.md#a9f13cbd9fea3680">CURRVAL</a></td></tr><tr><td align="left" valign="middle">NEXTVAL</td><td align="left" valign="middle">It is a pseudo column associated with a sequence.</td><td align="left" valign="middle"><a href="#ddfdf6ed362ba8f0">ROWID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">ROWNUM</td><td align="left" valign="middle">It is the row number that satisfies the condition.</td><td align="left" valign="middle"><a href="17-built-in-function-references.md#3c69e446ac188320">ROWNUM</a></td></tr><tr><td align="left" valign="middle">ROWID</td><td align="left" valign="middle">It returns the record identifier in the database.</td><td align="left" valign="middle"><a href="#ddfdf6ed362ba8f0">ROWID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_GROUP_ID</td><td align="left" valign="middle">It returns the group identifier in the database.</td><td align="left" valign="middle"><a href="#6f546401c38714d1">CLUSTER_GROUP_ID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_MEMBER_ID</td><td align="left" valign="middle">It returns the member identifier where the record is stored.</td><td align="left" valign="middle"><a href="#43c1ef9a45c6df5d">CLUSTER_MEMBER_ID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_GROUP_NAME</td><td align="left" valign="middle">It returns the group name where the record is stored.</td><td align="left" valign="middle"><a href="#9d24864e174958eb">CLUSTER_GROUP_NAME Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_MEMBER_NAME</td><td align="left" valign="middle">It returns the member name where the record is stored.</td><td align="left" valign="middle"><a href="#a83fff075b37b85d">CLUSTER_MEMBER_NAME Pseudo Column</a></td></tr><tr><td valign="middle">CLUSTER_SHARD_ID</td><td valign="middle">It returns the shard identifier where the record is stored.</td><td valign="middle"><a href="#f38fe3eabf46ee98">CLUSTER_SHARD_ID Pseudo Column</a></td></tr></tbody></table>

<a id="ddfdf6ed362ba8f0"></a>
### ROWID Pseudo Column

The ROWID pseudo column is a record identifier that returns the identification information for each database record.

ROWID contains the information needed to identify the location within the database, depending on the system.

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

When querying ROWID, the information stored internally in base 64 encoding is converted into values such as A-Z, a-z, 0-9, +, and / for output.

Each piece of information used to identify the address within the database, stored in ROWID, can be obtained using ROWID-related functions.

The address of a deleted record can be reassigned to a record that is to be inserted.

The ROWID pseudo column can only be used in SELECT operations and can not be used in INSERT, UPDATE, or DELETE operations.

For more information, refer to [ROWID](16-built-in-data-type-references.md#72823db80276ccca), [ROWID-related Functions](#8f97efbf5938c2e2).

The following is an example of querying the ROWID pseudo column.

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

<a id="6f546401c38714d1"></a>
### CLUSTER_GROUP_ID Pseudo Column

The CLUSTER_GROUP_ID pseudo column returns the group identifier of the server where the record is stored.

The CLUSTER_GROUP_ID pseudo column can be used in SELECT operations, but can not be used in INSERT, UPDATE, or DELETE operations.

> This information is valid in the cluster system.

The following is an example of retrieving the CLUSTER_GROUP_ID pseudo column.

```
gSQL> SELECT T1.C1, T1.CLUSTER_GROUP_ID FROM T1;
C1 T1.CLUSTER_GROUP_ID
-- -------------------
A                    1
B                    2
C                    3

3 rows selected.
```

<a id="43c1ef9a45c6df5d"></a>
### CLUSTER_MEMBER_ID Pseudo Column

The CLUSTER_MEMBER_ID pseudo column returns the member identifier of the server where the record is stored.

The CLUSTER_MEMBER_ID pseudo column can be used in SELECT operations, but can not be used in INSERT, UPDATE, or DELETE operations.

> This information is valid in the cluster system.

The following is an example of retrieving the CLUSTER_MEMBER_ID pseudo column.

```
gSQL> SELECT T1.C1, T1.CLUSTER_MEMBER_ID FROM T1;
C1 T1.CLUSTER_MEMBER_ID
-- --------------------
A                     1
B                     3
C                     5

3 rows selected.
```

<a id="9d24864e174958eb"></a>
### CLUSTER_GROUP_NAME Pseudo Column

The CLUSTER_GROUP_NAME pseudo column returns the group name of the server where the record is stored.

The CLUSTER_GROUP_NAME pseudo column can be used in SELECT operations, but can not be used in INSERT, UPDATE, or DELETE operations.

> This information is valid in the cluster system.

The following is an example of retrieving the CLUSTER_GROUP_NAME pseudo column.

```
gSQL> SELECT T1.C1, T1.CLUSTER_GROUP_NAME FROM T1;
C1 T1.CLUSTER_GROUP_NAME
-- ---------------------
A  G1                   
B  G2                   
C  G3                   

3 rows selected.
```

<a id="a83fff075b37b85d"></a>
### CLUSTER_MEMBER_NAME Pseudo Column

The CLUSTER_MEMBER_NAME pseudo column returns the member name of the server where the record is stored.

The CLUSTER_MEMBER_NAME pseudo column can be used in SELECT operations, but can not be used in INSERT, UPDATE, or DELETE operations.

> This information is valid in the cluster system.

The following is an example of retrieving the CLUSTER_MEMBER_NAME pseudo column.

```
gSQL> SELECT T1.C1, T1.CLUSTER_MEMBER_NAME FROM T1;
C1 T1.CLUSTER_MEMBER_NAME
-- ----------------------
A  G1N1                  
B  G2N1                  
C  G3N1                  

3 rows selected.
```

<a id="f38fe3eabf46ee98"></a>
### CLUSTER_SHARD_ID Pseudo Column

The CLUSTER_SHARD_ID pseudo column returns the shard identifier where the record is stored.

The CLUSTER_SHARD_ID pseudo column is allowed for SELECT statements only, it can not be used in INSERT, UPDATE, or DELETE statements.

> This information is valid in the cluster system.

The following is an example of how to retrieve the CLUSTER_SHARD_ID pseudo column.

```
gSQL> SELECT T1.C1, T1.CLUSTER_SHARD_ID FROM T1;

C1 CLUSTER_SHARD_ID
-- ----------------
A                14
B                17
C                 4

3 rows selected.
```

<a id="da354a9499dad75b"></a>
### Compatibility

The SQL standard compatibility for the pseudo column is as follows.

**SQL standard compatibility for pseudo column**

<a id="d9efacebdc84a5da"></a>
<table><tbody><tr><th align="center">&nbsp;Feature ID</th><th align="center">&nbsp;Description</th><th align="center">&nbsp;Availability</th></tr><tr><td align="left">T176</td><td align="left">Sequence generator support</td><td align="center">O</td></tr><tr><td align="left">T177</td><td align="left">&nbsp;Sequence generator support: simple restart option</td><td align="center">O</td></tr></tbody></table>

<a id="b554f8b97f2d370f"></a>
## Operators

An operator is represented by one or more specific symbols or keywords in the syntax, and it performs an operation on one or more arguments.

The types of operators are as follows.  
• Arithmetic operator  
• Concatenation operator  
• Set operator

<a id="42058bdb79f6d0e0"></a>
### Arithmetic Operator

<a id="a2772dccbd386447"></a>
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

<a id="ade6b07298e8dafb"></a>
#### Description

An arithmetic operator performs arithmetic operations on numeric types, date/time types, or interval types.

The precedence of arithmetic operators is as follows.

1. [+ (POSITIVE)](17-built-in-function-references.md#f57fd446dd6d675f), [- (NEGATIVE)](17-built-in-function-references.md#cb06a4fae99cbdc9)
2. [* (MULTIPLICATION)](17-built-in-function-references.md#191216bd565738ac), [/ (DIVISION)](17-built-in-function-references.md#ecfe4d7200d5c831)
3. [+ (ADDITION)](17-built-in-function-references.md#e730e487acc3f1d1), [- (SUBTRACTION)](17-built-in-function-references.md#a6113704936bbaf1)

<a id="6bfa12523bdac777"></a>
### Concatenation Operator

<a id="73e57caf78731546"></a>
#### Syntax

```
<concatenation operator> ::=
        <expression> || <expression>
```

<a id="da66d0bdb24540b7"></a>
#### Description

The concatenation operator returns a string that connects the values of the CHARACTER STRING or BINARY STRING types.  
For more information, refer to [|| (CONCATENATE)](17-built-in-function-references.md#ea2d45a74e2e0cbe), [CONCATENATE](17-built-in-function-references.md#e3a092e283852102).

<a id="6c111d5580d86586"></a>
### Set Operator

<a id="18066b049a78fecb"></a>
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

<a id="2b71d3a6c0df9b86"></a>
#### Description

A [set operator](20-sql-references-h-z.md#1e4cbe254403f053) performs a set operation on the results of a subquery.

INTERSECT ALL/DISTINCT has higher precedence than other set operators.

**Set operators**

<a id="8e1ca41f958f3ada"></a>
| Operator | Description |
| --- | --- |
| UNION ALL | It is the union that does not exclude duplicate rows from the subquery result. |
| UNION DISTINCT | It is the union that excludes duplicate rows from the subquery result. |
| EXCEPT ALL | It is the difference set that does not exclude duplicate rows from the subquery result. |
| EXCEPT DISTINCT | It is the difference set that excludes duplicate rows from the subquery result. |
| MINUS ALL | It is the same as EXCEPT ALL. |
| MINUS DISTINCT | It is the same as EXCEPT DISTINCT. |
| INTERSECT ALL | It is the intersection that does not exclude duplicate rows from the subquery result. |
| INTERSECT DISTINCT | It is the intersection that excludes duplicate rows from the subquery result. |

<a id="49f2a86864524afb"></a>
### Compatibility

The SQL standard compatibility for operators is as follows.

**SQL standard compatibility for operators**

<a id="8b05e4d3c29c6727"></a>
<table><tbody><tr><th align="center">&nbsp;Feature ID</th><th align="center">&nbsp;Description</th><th align="center">&nbsp;Availability</th></tr><tr><td align="left" valign="middle">E011-04</td><td align="left" valign="middle">Arithmetic operators</td><td align="center" valign="middle">O</td></tr><tr><td valign="middle">E021-07</td><td valign="middle">Character concatenation</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-01</td><td align="left" valign="middle">UNION DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-02</td><td align="left" valign="middle">UNION ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-03</td><td align="left" valign="middle">&nbsp;EXCEPT DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-05</td><td align="left" valign="middle">Columns combined via table operators need not have exactly the same data type</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-06</td><td align="left" valign="middle">Table operators in subqueries</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F041-08</td><td align="left" valign="middle">All comparison operators are supported (rather than just =)</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F303</td><td align="left" valign="middle">INTERSECT DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F305</td><td align="left" valign="middle">INTERSECT ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F304</td><td align="left" valign="middle">EXCEPT ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F846</td><td align="left" valign="middle">Octet support in regular expression operators</td><td align="center" valign="middle">X</td></tr><tr><td align="left" valign="middle">J571</td><td align="left" valign="middle">NEW operator</td><td align="center" valign="middle">X</td></tr></tbody></table>

<a id="45f0cb169e5de3b6"></a>
## Functions

Although operators and functions are similar in functionality, a function specifies its arguments by using parentheses after its name. A function can accept zero or more arguments.

The function has two types, as follows.  
.• Single row function  
• Aggregate function

<a id="8bb51f6f89b17325"></a>
### Single Row Function

A single-row function returns one result row for each row in the table or view.

The single-row functions are as follows.

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
- Statistics information function

<a id="9dd9c86c20d6e709"></a>
#### Numeric Functions

A numeric value is input into a numeric function, which returns a numeric result.

For more information about numeric function types, refer to the following.

- [ABS](17-built-in-function-references.md#66debe22fe5fe5eb)
- [ACOS](17-built-in-function-references.md#6438e1149af0d7ef)
- [ASIN](17-built-in-function-references.md#539398a6119ea91d)
- [ATAN](17-built-in-function-references.md#906d826bffba6a12)
- [ATAN2](17-built-in-function-references.md#b757df1a93296ea8)
- [BITAND](17-built-in-function-references.md#190418c8624fe2fd)
- [BITNOT](17-built-in-function-references.md#17e3a5b7f80cada4)
- [BITOR](17-built-in-function-references.md#440875e5887624e9)
- [BITXOR](17-built-in-function-references.md#b75a04128803f30b)
- [CBRT](17-built-in-function-references.md#9defd2f6f7bf22d3)
- [CEIL](17-built-in-function-references.md#e6f694aeb902a472)
- [COS](17-built-in-function-references.md#01430adf113ff75c)
- [COT](17-built-in-function-references.md#68c7f9a4e95e4dd2)
- [DEGREES](17-built-in-function-references.md#1d433d7c0ea7a97c)
- [EXP](17-built-in-function-references.md#76fc20b41ca68dec)
- [FACTORIAL](17-built-in-function-references.md#dd9a0095c17bf009)
- [FLOOR](17-built-in-function-references.md#dfe1ce74826d9936)
- [LN](17-built-in-function-references.md#42927b87e9319c86)
- [LOG](17-built-in-function-references.md#941f72dc33770e54)
- [MOD](17-built-in-function-references.md#0013864abae4530e)
- [PI](17-built-in-function-references.md#f38bfce7d7746322)
- [POWER](17-built-in-function-references.md#923289d2965eeaa2)
- [RADIANS](17-built-in-function-references.md#8712212aed5abfe3)
- [RANDOM](17-built-in-function-references.md#8603ff42fa54e75a)
- [ROUND( number )](17-built-in-function-references.md#4849ac41d73729b5)
- [SHARD_ID](17-built-in-function-references.md#68e5e1fa36c9d98b)
- [SHIFT_LEFT](17-built-in-function-references.md#8c4d8eb730a7ae5c)
- [SHIFT_RIGHT](17-built-in-function-references.md#be8f3a3649231204)
- [SIGN](17-built-in-function-references.md#7baca0f310be0340)
- [SIN](17-built-in-function-references.md#519eef61f86535a5)
- [SQRT](17-built-in-function-references.md#06f4b7fab8af7238)
- [TAN](17-built-in-function-references.md#768f911404616e1b)
- [TRUNC( number )](17-built-in-function-references.md#2eadbb656d48170b)
- [WIDTH_BUCKET](17-built-in-function-references.md#6c5b40e928a7d7a1)

<a id="575ac830a23020ac"></a>
#### Character String Functions Returning Character Values

A character string value is input into character string functions returning character values, and the function returns a result of character string type.

For more information about character string functions returning character values, refer to the following.

- [CHR](17-built-in-function-references.md#82383ccc5174878b)
- [CONCAT](17-built-in-function-references.md#f398b6d7062ffdd5)
- [CONCATENATE](17-built-in-function-references.md#e3a092e283852102)
- [INITCAP](17-built-in-function-references.md#2bd35ece6f4fc38a)
- [LOWER](17-built-in-function-references.md#da1c90e5c6d23d83)
- [LPAD](17-built-in-function-references.md#fab61635d016946f)
- [LTRIM](17-built-in-function-references.md#ffd108b6dd98ff5a)
- [OVERLAY](17-built-in-function-references.md#19716074501dd867)
- [REGEXP_REPLACE](17-built-in-function-references.md#42d99f66190078af)
- [REGEXP_SUBSTR](17-built-in-function-references.md#be5a2413d7c8ae27)
- [REPEAT](17-built-in-function-references.md#45c45d22ae1585c9)
- [REPLACE](17-built-in-function-references.md#088a48138c2c0bac)
- [REVERSE](17-built-in-function-references.md#a5c8ce6a760ed4d6)
- [RPAD](17-built-in-function-references.md#63806191e5a3cf12)
- [RTRIM](17-built-in-function-references.md#defacd4fef7e10c1)
- [SPLIT_PART](17-built-in-function-references.md#9144e8314d0b83cc)
- [SUBSTR](17-built-in-function-references.md#6d713ac965ddd147)
- [SUBSTRB](17-built-in-function-references.md#b888761fc5a7b8e9)
- [TRANSLATE](17-built-in-function-references.md#0e091ffaeb163a5e)
- [TRIM](17-built-in-function-references.md#57e64d312bc89918)
- [UPPER](17-built-in-function-references.md#6f03606b9029b12d)

<a id="49c0d5462a3ccec1"></a>
#### Character String Functions Returning Number Values

A character string value is input into character string functions returning number values, and the function returns a result of number type.

For more information about character string functions returning number values types, refer to the following.

- [ASCII](17-built-in-function-references.md#9379d1be7b7614bc)
- [BIT_LENGTH](17-built-in-function-references.md#cb321790057d5f91)
- [BYTE_LENGTH](17-built-in-function-references.md#a55aa7d89b47253c)
- [CHAR_LENGTH](17-built-in-function-references.md#bfc30a82c549098c)
- [INSTR](17-built-in-function-references.md#d8ca8cd4bcc08919)
- [LENGTH](17-built-in-function-references.md#dec729ca5cf2693b)
- [LENGTHB](17-built-in-function-references.md#c5f46ba504cefe4a)
- [OCTET_LENGTH](17-built-in-function-references.md#ddbc8d3776b14b1b)
- [POSITION](17-built-in-function-references.md#b97361a0b31fc8b6)
- [REGEXP_COUNT](17-built-in-function-references.md#54924611a881f204)
- [REGEXP_INSTR](17-built-in-function-references.md#75e1a53f48309d9a)

<a id="7a7db741a4c8e5d2"></a>
#### Datetime Functions

The value of the date/time/timestamp/interval type is input into a datetime function, and the function returns a result of the date/time/timestamp/interval type.

For more information about datetime function types, refer to the following.

- [ADDDATE](17-built-in-function-references.md#8e020f57d0e00036)
- [ADDTIME](17-built-in-function-references.md#59fdbc5cb3e7c8aa)
- [ADD_MONTHS](17-built-in-function-references.md#1ce6a0e7cb7a13e4)
- [DATEADD](17-built-in-function-references.md#e08c2b0d186f7434)
- [DATEDIFF](17-built-in-function-references.md#0a5c8116c798633e)
- [DATE_ADD](17-built-in-function-references.md#2c1ca00fa963ce14)
- [DATE_PART](17-built-in-function-references.md#1060ca0ee1b36b88)
- [EXTRACT](17-built-in-function-references.md#ac1108d8f983023f)
- [FROM_TZ](17-built-in-function-references.md#76dc6a1d1e48f0dd)
- [LAST_DAY](17-built-in-function-references.md#3333e5c7caa18122)
- [MONTHS_BETWEEN](17-built-in-function-references.md#e794dcf77475be45)

<a id="d32be19d9c2e2e3c"></a>
#### General Comparison Functions

A general comparison function returns either the minimum or maximum value from a set of values.

For more information about general comparison function types, refer to the following.

- [GREATEST](17-built-in-function-references.md#067117605c1b92c1)
- [LEAST](17-built-in-function-references.md#14e8563c1aac8330)

<a id="939918b25ceb26f0"></a>
#### Conversion Functions

A conversion function sets a value to a specific data type.

For more information about the types of conversion functions, refer to the following.

- [NUMTODSINTERVAL](17-built-in-function-references.md#36e622b41cbe994b)
- [NUMTOYMINTERVAL](17-built-in-function-references.md#76ea4a5700a8dd3d)
- [TO_CHAR( datetime )](17-built-in-function-references.md#5f3a74b3e90ec4f6)
- [TO_CHAR( number )](17-built-in-function-references.md#06e9d7b88a3c7d10)
- [TO_DATE](17-built-in-function-references.md#74b46ad0bc9dbb10)
- [TO_NATIVE_BIGINT](17-built-in-function-references.md#a0f4163ceae2b2da)
- [TO_NATIVE_DOUBLE](17-built-in-function-references.md#37b2e9541ce0eb78)
- [TO_NATIVE_INTEGER](17-built-in-function-references.md#b7ba82a1d907f3c6)
- [TO_NATIVE_REAL](17-built-in-function-references.md#d1401c04ea742970)
- [TO_NATIVE_SMALLINT](17-built-in-function-references.md#194e111618562fc9)
- [TO_NUMBER](17-built-in-function-references.md#a547796f56907926)
- [TO_TIME](17-built-in-function-references.md#369e424a6a243c31)
- [TO_TIME_TZ](17-built-in-function-references.md#3d8ed12ebeef772c)
- [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#7d0b935c0acaee3f)
- [TO_TIMESTAMP](17-built-in-function-references.md#b03348c605444fea)
- [TO_TIMESTAMP_TZ](17-built-in-function-references.md#83872faa8a33c95f)
- [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#785d71b6e8e5c13b)

<a id="dc11137341c9b7e5"></a>
#### Conditional Functions

A conditional function returns a specific value based on a condition.

For more information about the types of conditional functions, refer to the following.

- [CASE2](17-built-in-function-references.md#00ada028ea4b123c)
- [DECODE](17-built-in-function-references.md#7530326fc1dda91b)

<a id="d78a9633a23b7f4c"></a>
#### NULL-related Functions

A NULL-related function returns a specific value based on whether the input value is NULL.

For more information about the types of NULL-related functions, refer to the following.

- [COALESCE](17-built-in-function-references.md#8ecf82e319ad8324)
- [NULLIF](17-built-in-function-references.md#aef2dc5f3ce03844)
- [NVL](17-built-in-function-references.md#70e7a47e2c3d528c)
- [NVL2](17-built-in-function-references.md#4e5a4c6988683394)

<a id="8f97efbf5938c2e2"></a>
#### ROWID-related Functions

A ROWID-related function is used to retrieve information about the ROWID.

For more information about the types of ROWID-related functions, refer to the following.

- Functions valid in a stand-alone
    - [ROWID_OBJECT_ID](17-built-in-function-references.md#e58e8b325a36c0cd)
    - [ROWID_TABLESPACE_ID](17-built-in-function-references.md#eb30fc64dd130c8d)
    - [ROWID_PAGE_ID](17-built-in-function-references.md#ade88b5651078a78)
    - [ROWID_ROW_NUMBER](17-built-in-function-references.md#19f1ed7225a03628)

- Functions valid in a cluster
    - [ROWID_GRID_BLOCK_ID](17-built-in-function-references.md#8758283a97cdf796)
    - [ROWID_GRID_BLOCK_SEQ](17-built-in-function-references.md#8c5473eab75a8d0d)
    - [ROWID_MEMBER_ID](17-built-in-function-references.md#302c837a4ed91459)
    - [ROWID_SHARD_ID](17-built-in-function-references.md#c3822a2f6ddbd3ca)

<a id="3a19f2159a5063fe"></a>
#### Encryption Functions

The encryption function encrypts, decrypts, or hashes the given plain text using a specific algorithm and then returns the result.

The types of encryption functions are as follows.

- [DIGEST](17-built-in-function-references.md#e3d9b3a20030165f)
- [HASH32](17-built-in-function-references.md#4eb497bc2b25806e)

<a id="c0376d7e8efabffe"></a>
#### System Information Functions

The system information function is used to obtain information about sessions and the system.

For more information about the types of system information functions, refer to the following.

- [CLOCK_DATE](17-built-in-function-references.md#52e4f702da64bdb5)
- [CLOCK_LOCALTIME](17-built-in-function-references.md#c2958ed1e6aca851)
- [CLOCK_LOCALTIMESTAMP](17-built-in-function-references.md#32abd59cdbe768f1)
- [CURRENT_CATALOG](17-built-in-function-references.md#a6a2f59adbdb357d)
- [CURRENT_DATE](17-built-in-function-references.md#4a5eee8c77603529)
- [CURRENT_ROLE](17-built-in-function-references.md#38ee0469541ddc0f)
- [CURRENT_SCHEMA](17-built-in-function-references.md#fe4ad0b4ed2109ab)
- [CURRENT_TIME](17-built-in-function-references.md#29a0a944688833fc)
- [CURRENT_TIMESTAMP](17-built-in-function-references.md#f242b35f2a25d86c)
- [CURRENT_USER](17-built-in-function-references.md#3d2fbc075f3881c1)
- [LAST_IDENTITY_VALUE](17-built-in-function-references.md#6034d7de06501d08)
- [LOCAL_MEMBER_POSITION](17-built-in-function-references.md#3e18ea582f6a25fa)
- [LOCALTIME](17-built-in-function-references.md#c20987197caf3bbc)
- [LOCALTIMESTAMP](17-built-in-function-references.md#9fa35889a1bb6bcb)
- [LOGON_USER](17-built-in-function-references.md#5f65dfcc71c8119c)
- [SESSION_ID](17-built-in-function-references.md#1e212dba8d6c5a39)
- [SESSION_SERIAL](17-built-in-function-references.md#a1540a88dca6d4c6)
- [SESSION_USER](17-built-in-function-references.md#1991305773bb0cac)
- [SESSIONTIMEZONE](17-built-in-function-references.md#06d78e4d0eeda18a)
- [STATEMENT_DATE](17-built-in-function-references.md#3ba5dfafe71fd478)
- [STATEMENT_LOCALTIME](17-built-in-function-references.md#3b96012a99b7f57b)
- [STATEMENT_LOCALTIMESTAMP](17-built-in-function-references.md#b9af643d31fd0351)
- [STATEMENT_TIME](17-built-in-function-references.md#944704796ac0d078)
- [STATEMENT_TIMESTAMP](17-built-in-function-references.md#9651210adb0ca813)
- [STATEMENT_VIEW_SCN](17-built-in-function-references.md#ab2f5de729ed4cf9)
- [SYSDATE](17-built-in-function-references.md#0ed762465c5eb8c3)
- [SYSTIME](17-built-in-function-references.md#8c555df283556811)
- [SYSTIMESTAMP](17-built-in-function-references.md#bb8441e714395584)
- [TRANSACTION_DATE](17-built-in-function-references.md#3334c80c7c712441)
- [TRANSACTION_LOCALTIME](17-built-in-function-references.md#ac7edc81a7e0cf69)
- [TRANSACTION_LOCALTIMESTAMP](17-built-in-function-references.md#2ce7ed638d065160)
- [TRANSACTION_TIME](17-built-in-function-references.md#2d2fd5c6c8fca6db)
- [TRANSACTION_TIMESTAMP](17-built-in-function-references.md#1c814c7a014ca275)
- [USER_ID](17-built-in-function-references.md#58c8f8adf8e35e6d)
- [VERSION](17-built-in-function-references.md#39bf4f4db2bd030c)

<a id="77b282b7a0b08d8f"></a>
#### Statistics Information function

A statistics information function is used to retrieve information about an object.

The types of statistics information functions are as follows.

- [TABLE_PHYSICAL_STATS](17-built-in-function-references.md#77a8c39a1b430f52)
- [INDEX_PHYSICAL_STATS](17-built-in-function-references.md#483bdb639e6046de)
- [GSI_PHYSICAL_STATS](17-built-in-function-references.md#d60f8977301c682f)

<a id="f67400ca8ab799e1"></a>
### Aggregate Function

An aggregate function generates a single result row for multiple rows.

For more information about aggregate function types, refer to the following.

- [COUNT](17-built-in-function-references.md#f006671e89899b6b)
- [COUNT(*)](17-built-in-function-references.md#d9b43e9a86df6f7b)
- [SUM](17-built-in-function-references.md#07ac6a4ba1ffd0d0)
- [AVG](17-built-in-function-references.md#6bd804108bf49c64)
- [MIN](17-built-in-function-references.md#3eaa7160a04afaa7)
- [MAX](17-built-in-function-references.md#4e04ee8ff083abc1)
- [STDDEV](17-built-in-function-references.md#846fb9419b4408b2)
- [STDDEV_POP](17-built-in-function-references.md#c40e9f4ed7b6baf7)
- [STDDEV_SAMP](17-built-in-function-references.md#ede27e56f90e140c)
- [VAR_POP](17-built-in-function-references.md#d3d9330ec5d2493a)
- [VAR_SAMP](17-built-in-function-references.md#fc3eda323e3927d6)
- [VARIANCE](17-built-in-function-references.md#fa3ad26fea8effe3)
- [APPROX_COUNT_DISTINCT](17-built-in-function-references.md#051f809810e5e2aa)

<a id="587d6da9bc5f0c63"></a>
### Window Function

It returns the result of the function for the defined range of records.

The defined range of records is called a window, and the execution range is defined using OVER &lt;window name or specification&gt;.

For more information about the window, refer to the [window clause](20-sql-references-h-z.md#465362e9aeb4ca49).

Each record within the group contains the result of executing the window function over the defined window (range). Therefore, unlike an aggregate function, the window function returns multiple records for each group.

The window function is available in the *select list* and the *order by* clause.

The window functions are listed below.

- [AVG() OVER](17-built-in-function-references.md#1376b5bf52f22ea4)
- [CORR() OVER](17-built-in-function-references.md#f0f3126e0b34eaaa)
- [COUNT() OVER](17-built-in-function-references.md#7a9d83c1c4f33ad5)
- [COUNT(*) OVER](17-built-in-function-references.md#8df906e8b2c6ef7b)
- [COVAR_POP() OVER](17-built-in-function-references.md#71040c22ebaa8b2b)
- [COVAR_SAMP() OVER](17-built-in-function-references.md#726b04caaea6a059)
- [CUME_DIST() OVER](17-built-in-function-references.md#1084d34375187411)
- [DENSE_RANK() OVER](17-built-in-function-references.md#5e4ac5c4854abc9e)
- [FIRST() OVER](17-built-in-function-references.md#4953a10d0f413251)
- [FIRST_VALUE() OVER](17-built-in-function-references.md#5eb75302623eb2a6)
- [LAG() OVER](17-built-in-function-references.md#335ae138bc8c502e)
- [LAST() OVER](17-built-in-function-references.md#5c6145cc5b391ab1)
- [LAST_VALUE() OVER](17-built-in-function-references.md#aba2351fe4a17e32)
- [LEAD() OVER](17-built-in-function-references.md#f55af5c9d24fd9f6)
- [LISTAGG() OVER](17-built-in-function-references.md#b4aed9657b112c16)
- [MAX() OVER](17-built-in-function-references.md#e470bba9db176384)
- [MEDIAN() OVER](17-built-in-function-references.md#af88b35602436133)
- [MIN() OVER](17-built-in-function-references.md#1759858523c292e5)
- [NTH_VALUE() OVER](17-built-in-function-references.md#80b5c54f4311faa4)
- [NTILE() OVER](17-built-in-function-references.md#8cff1c7fb3275c6f)
- [PERCENT_RANK() OVER](17-built-in-function-references.md#d06751ea6d93e3bb)
- [PERCENTILE_CONT() OVER](17-built-in-function-references.md#4f7de04feb86ca45)
- [PERCENTILE_DISC() OVER](17-built-in-function-references.md#d600d89cafc9b5d2)
- [RANK() OVER](17-built-in-function-references.md#bbb8aa77da81f0c5)
- [RATIO_TO_REPORT() OVER](17-built-in-function-references.md#1e112e5c333c9548)
- [REGR_AVGX() OVER](17-built-in-function-references.md#c669a282cdf0f8d1)
- [REGR_AVGY() OVER](17-built-in-function-references.md#f5400e9901665ea5)
- [REGR_COUNT() OVER](17-built-in-function-references.md#fba4384faf0f46d0)
- [REGR_INTERCEPT() OVER](17-built-in-function-references.md#84b5f2bd5dcecfdb)
- [REGR_R2() OVER](17-built-in-function-references.md#5d67d28ce3593acd)
- [REGR_SLOPE() OVER](17-built-in-function-references.md#0ebaf0321b9d6651)
- [REGR_SXX() OVER](17-built-in-function-references.md#ff52783c9d467670)
- [REGR_SXY() OVER](17-built-in-function-references.md#0556439554d27a68)
- [REGR_SYY() OVER](17-built-in-function-references.md#b8f6487e9302fcd9)
- [ROW_NUMBER() OVER](17-built-in-function-references.md#3125db1255495115)
- [STDDEV() OVER](17-built-in-function-references.md#0d306a5e79990e63)
- [STDDEV_POP() OVER](17-built-in-function-references.md#b62a4ce3fbe7f69a)
- [STDDEV_SAMP() OVER](17-built-in-function-references.md#dff5254ae89fb63b)
- [STRING_AGG() OVER](17-built-in-function-references.md#0bc3017b9662aa76)
- [SUM() OVER](17-built-in-function-references.md#670852541b343c04) 
- [VAR_POP() OVER](17-built-in-function-references.md#5de9a2268c5eaa32)
- [VAR_SAMP() OVER](17-built-in-function-references.md#b2b2417aa592ee6c)
- [VARIANCE() OVER](17-built-in-function-references.md#ec280e0f2fdadf65)

<a id="b568b1fc7cec34c1"></a>
### Compatibility

The SQL standard compatibility for functions is as follows.

**SQL standard compatibility for functions**

<a id="3f008d1abca5b649"></a>
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

<a id="e7913ce53ce3e011"></a>
## Conditions

<a id="b82b8c7c6646561b"></a>
### Condition

A condition is an expression that is evaluated as TRUE, FALSE, or UNKNOWN.

A condition can be used in the following SQL statements.  

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

<a id="c16b406a7a8cf3e5"></a>
| Precedence | Condition type |
| --- | --- |
| 1 | Operators in condition clauses |
| 2 | =, !=, &lt;, &gt;, &lt;=, &gt;= |
| 3 | IS [NOT] NULL, [NOT] BETWEEN,  [NOT] IN,  LIKE, EXISTS, IS [NOT] DISTINCT FROM |
| 4 | NOT |
| 5 | AND |
| 6 | OR |

<a id="259e86d4050ee6f0"></a>
### Comparison Conditions

It compares both conditional expressions and returns a boolean value of TRUE, FALSE, or UNKNOWN.

**Comparison conditions**

<a id="bd840a2a839b6cc5"></a>
| Condition | Description |
| --- | --- |
| = | It checks if both conditions are equal. |
| !=, &lt;&gt; | It checks if both conditions are not equal. |
| > | It compares which one of the two conditions is greater. |
| < | It compares which one of the two conditions is smaller. |
| >= | It compares which one of the two conditions is greater or equal. |
| <= | It compares which one of the two conditions is smaller or equal. |
| ANY, SOME | If there is a condition whose left expr satisfies at least one of the right expr_list (or subquery results), then it returns TRUE. If there is no right subquery result, then it returns FALSE. |
| ALL | If there is a condition whose left expr satisfies all the right expr_list (or subquery results), then it returns TRUE. If there is no right subquery result, then it returns TRUE. |

For more information, refer to [Type Comparison](#9411d3a5627fa793).

<a id="64def6d64d28b856"></a>
#### &lt; Simple Comparison Conditions &gt;

<a id="894d98c31e1617d4"></a>
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

For more information, refer to [Scalar Subquery Expression](#8329d99814ce23d2).

<a id="dd44e668de27b453"></a>
##### Description

If the expr list or subquery appears on both sides of the comparison_operator, the number of expr or subquery targets to be compared must be same.  
If there is a subquery, the number of result records must be one.

<a id="c87863f6e6d7548c"></a>
##### Example

**Example of simple comparison conditions**

<a id="070d0630478c5415"></a>
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

<a id="f8b8886f84f751b4"></a>
#### &lt;Group Comparison Conditions&gt;

<a id="4ebc4a0bd257f319"></a>
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

For more information, refer to [Scalar Subquery Expression](#8329d99814ce23d2).

<a id="47696338d3927a06"></a>
##### Description

If the expr list or subquery appears on both sides of the comparison_operator, the number of expr or subquery targets to be compared must be the same.  
If a subquery appears on the left side of the comparison_operator, the number of result records must be one.  
If a subquery appears on the right side of the comparison_operator, the number of result records can be multiple.

<a id="8c4bac6eba95fe0c"></a>
##### Example

<a id="d73fd0f2cc15a4f3"></a>
<table class="table column_count_2"><caption>Example of group comparison conditions</caption><thead><tr><th class="to_center"><div>Conditional expression</div></th><th class="to_center"><div>Result</div></th></tr></thead><tbody><tr><td><div>1 =any ( 1, 2, 3, 4, 5 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>1 =any ( 1, 2, null, 4, 5 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>1 =any ( 2, null, 4, 5 )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td><div>1 =any ( 100, 2, 3, 4, 5 )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td><div>1 =all ( 1, +1, 1E+0 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>1 =all ( 1, +1, 1E+0, null )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td><div>1 =all ( 1, 2, 3, 4, 5 )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td><div>( 1, 2 ) =any ( ( 0, 1 ), ( 1, 2 ), ( 3, 4 ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>( 1, 2 ) =any ( ( 0, 1 ), ( 1, 2 ), ( null, null ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>( 1, 2 ) =any ( ( 0, 1 ), ( 2, 3 ), ( 3, 4 ) )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td><div>( 1, 2 ) =all ( ( 1, 2 ), ( +1, +2 ), ( 1E+0, 2E+0 ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td><div>( 1, 2 ) =all ( ( 1, 2 ), ( +1, +2 ), ( null, null ) )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td><div>( 1, 2 ) =all ( ( 0, 1 ), ( 2, 3 ), ( 3, 4 ) )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><th colspan="2"><div>When the result record of comparison_operator's right subquery is 0</div></th></tr><tr><td><div>( 'X' ) =any ( select dummy from dual where dummy = 'Y' )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td><div>( 'X' ) =all ( select dummy from dual where dummy = 'Y' )</div></td><td class="to_left"><div>TRUE</div></td></tr></tbody></table>

<a id="88f4ffdfad3322b2"></a>
### Logical Conditions

Logical conditions include AND, OR, and NOT.

<a id="972fa199a67cb3ef"></a>
#### AND

<a id="4badfbdebfffa8f1"></a>
##### Syntax

```
<boolean value expression> AND <boolean value expression>
```

<a id="ec04f76a40680e4d"></a>
##### Description

**Truth table of AND boolean operator**

<a id="e69ba49285506928"></a>
| AND | True | False | Unknown |
| --- | --- | --- | --- |
| True | True | False | Unknown |
| False | False | False | False |
| Unknown | Unknown | False | Unknown |

<a id="c3967404c793f9a6"></a>
#### OR

<a id="cff800d262ae903b"></a>
##### Syntax

```
<boolean value expression> OR <boolean value expression>
```

<a id="a34b49bd8dd0335b"></a>
##### Description

**Truth table of OR boolean operator**

<a id="800cc2c4b913f1a4"></a>
| OR | True | False | Unknown |
| --- | --- | --- | --- |
| True | True | True | True |
| False | True | False | Unknown |
| Unknown | True | Unknown | Unknown |

<a id="63a9db0e8180774d"></a>
#### NOT

<a id="7f37e34dabd8f113"></a>
##### Syntax

```
NOT <boolean value expression>
```

<a id="ffbd4ee33faea3aa"></a>
##### Description

**Truth table of NOT boolean operator**

<a id="d9c961295651be67"></a>
| expr | NOT |
| --- | --- |
| True | False |
| False | True |
| Unknown | Unknown |

<a id="e89b943ce4549e29"></a>
### Null Condition

<a id="cf903ea46abaacce"></a>
#### Syntax

```
<expr> IS [NOT] NULL
```

<a id="ff6ab97298baa69c"></a>
#### Description

It checks whether the result value of expr is NULL.

**Result table of IS NULL condition**

<a id="0f0d24c19310aa5a"></a>
| expr | IS NULL | IS NOT NULL |
| --- | --- | --- |
| NULL | True | False |
| NOT NULL | False | True |

<a id="934c399f4df49c44"></a>
### Compound Conditions

It is a conditional expression that combines multiple conditions.

```
compound_condition ::=
        ( condition )
      | NOT condition
      | condition < AND | OR > condition
```

<a id="70d0f77bed49a0ba"></a>
### Pattern-matching Conditions

<a id="fc43aa96248f808a"></a>
#### Like Condition

<a id="16f58982e93a03fd"></a>
##### Syntax

```
like_condition ::=
        string [NOT] LIKE pattern [ ESCAPE escape_character ]
```

<a id="f9d88b5cc8f0f388"></a>
##### Description

It checks whether a string matches the specified pattern.

Arguments such as string, pattern, and escape_character can be of a character type, such as CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING, or any type that can be converted to a character type.  
If string, pattern, or escape_character is NULL, it returns NULL.

If the escape_character is omitted, there is no default value.  
If the escape_character is specified, it should be a single character.

If pattern does not include '_' or '%', it is processed the same way as an equal operation (string = pattern).  
If the pattern includes '_'  or '%', the string is checked for a match as follows.  
• '_': It corresponds to any single character.  
• '%': It corresponds to any string of zero or more characters.

To compare the '_' or '%' included in the pattern as literal characters, use the ESCAPE clause.  
Specify the escape_character and place it before the '_' or '%' in the pattern.

<a id="9c645b00f224fa48"></a>
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

<a id="f7b851fa4ca3e27d"></a>
#### REGEXP_LIKE Condition

<a id="245480afd9ec7441"></a>
##### Syntax

```
regexp_like_condition ::=
        REGEXP_LIKE ( source_string, pattern[, match_param ] )
```

<a id="c4aa70f6b1bd157e"></a>
##### Description

It checks whether the source_string matches the specified pattern.

*source_string*  
It is the character expression of the search target, and it can be of a character type or a type that can be converted to a character, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

*pattern*  
It is the regular expression, and it can be of a character type or a type that can be converted to a character such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.  
It can be described up to 512 bytes.  
For more information about the operators that can be specified in the pattern, refer to [Regular Expression](#c7aeceb78ecfda89).

*match_param*  
It is the character expression that can alter the default matching operation of a function, and it can be of a character type, such as CHARACTER, CHARACTER VARYING, or CHARACTER LONG VARYING.

'i', 'c', 'n', 'm', 'x' can be specified in match_param, and one or more of them can be described.

- **'i':** It is case-insensitive.
- **'c':** It is case-sensitive.
- **'n':** The dot operator ( . ) allows matching with the newline character.
- **'m':** It processes the source_string as multiple lines. It interprets ^ ( Beginning-of-Line Anchor ) and $ ( End-of-Line Anchor ) for each line.
- **'x':** It ignores whitespace in the pattern.

If a character other than 'i', 'c', 'n', 'm', or 'x' appears in match_param, an error is returned.   
If contradictory case matching, such as 'ic', is listed in match_param, an error is returned.

If match_param is omitted,  
&nbsp;• It is case-sensitive.  
&nbsp;• The dot operator ( . ) does not allow matching with the newline character.  
&nbsp;• It processes the source_string as a single line.

<a id="27133fa87f08e679"></a>
##### Example

```
gSQL> 
SELECT web_street_name FROM web_site;
WEB_STREET_NAME
---------------
Dogwood Sunset 
7th            
2nd 3rd        
Hill 5th       
Cedar North    
5 rows selected.

gSQL> 
SELECT *
  FROM web_site
 WHERE REGEXP_LIKE( web_street_name, '[[:digit:]]th$' );
WEB_STREET_NAME
---------------
7th            
Hill 5th       
2 rows selected.
```

<a id="0326bba6bcf9d1a5"></a>
### BETWEEN Condition

<a id="a83c5a067c8a47b3"></a>
#### Syntax

```
<between condition> ::=
   <expr1> [ NOT ] BETWEEN [ ASYMMETRIC | SYMMETRIC ] <expr2> AND <expr3>
```

<a id="c8f41c59fc26f90d"></a>
#### Description

It checks whether expr1 is within the range between expr2 and expr3.

If ASYMMETRIC or SYMMETRIC is omitted, the default is ASYMMETRIC.  
If the data types of expr1, expr2, and expr3 are different, they will be converted.   
For more information, refer to [Type Comparison](#9411d3a5627fa793), [Type Conversion](#fc718a805c53e7ba).

**Equivalence of the BETWEEN clause**

<a id="b2b456a4543858ef"></a>
| A | B |
| --- | --- |
| X BETWEEN ASYMMETRIC Y AND Z | X BETWEEN Y AND Z |
| X BETWEEN Y AND Z | X >= Y AND X <= Z |
| X NOT BETWEEN Y AND Z | NOT( X BETWEEN Y AND Z ) |
| X BETWEEN SYMMETRIC Y AND Z | ((X BETWEEN Y AND Z) OR (X BETWEEN Z AND Y) |
| X NOT BETWEEN SYMMETRIC Y AND Z | NOT( X BETWEEN SYMMETRIC Y AND Z ) |

<a id="f7459843dffa3607"></a>
#### Example

<a id="5a92ebe3dc6eac4d"></a>
<table class="table column_count_3"><caption>Example of BETWEEN clause</caption><thead><tr><th class="to_center" colspan="2"><div>Conditional expression</div></th><th class="to_center"><div>Result</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>BETWEEN [ ASYMMETRIC ]</div></td><td class="to_middle"><div>3 BETWEEN 1 AND 5</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr><tr><td class="to_middle"><div>NULL BETWEEN 1 AND 5
3 BETWEEN NULL AND 5
3 BETWEEN 1 AND NULL</div></td><td class="to_left to_middle"><div>NULL</div></td></tr><tr><td class="to_middle"><div>3 BETWEEN 5 AND 1</div></td><td class="to_left to_middle"><div>FALSE</div></td></tr><tr><td class="to_middle" rowspan="3"><div>BETWEEN SYMMETRIC</div></td><td class="to_middle"><div>3 BETWEEN SYMMETRIC 1 AND 5</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr><tr><td class="to_middle"><div>NULL BETWEEN SYMMETRIC 1 AND 5
3 BETWEEN SYMMETRIC NULL AND 5
3 BETWEEN SYMMETRIC 1 AND NULL</div></td><td class="to_left to_middle"><div>NULL</div></td></tr><tr><td class="to_middle"><div>3 BETWEEN SYMMETRIC 5 AND 1</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr></tbody></table>

<a id="5933e103c1237c33"></a>
### IN Condition

<a id="b58ae4e8f8b1d9e9"></a>
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

<a id="a4eae9642cb77964"></a>
#### Description

The IN condition returns the same result as = ANY.  
The NOT IN condition returns the same result as !=ALL.

For more information, refer to [Comparison Conditions](#259e86d4050ee6f0).

<a id="c28d9d7e0aa883ea"></a>
#### Example

**Example of IN condition**

<a id="7b202b7cc2b5e944"></a>
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

<a id="ca235275bca669c1"></a>
### EXISTS Condition

<a id="a8b29d3a0ef41831"></a>
#### Syntax

```
exists_conditions ::= 
        EXISTS ( subquery )
```

<a id="24aa6d08df790074"></a>
#### Description

It checks whether the result record of the subquery exists.   
If the subquery returns a result record, it returns TRUE. Otherwise, it returns FALSE.

<a id="87dba6c6f1e1ec04"></a>
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

<a id="9df4dc07443b0a25"></a>
### DISTINCT Condition

<a id="2ab8ac203e624f23"></a>
#### Syntax

```
distinct_conditions ::= 
        <expr> IS [NOT] DISTINCT FROM <expr>
      | ( <expr_list> ) IS [NOT] DISTINCT FROM ( <expr_list> )
```

<a id="90d3772de1a2803e"></a>
#### Description

The operand types in a distinct condition must be comparable to each other.  
If the operand is &lt;expr_list&gt;, the data at the same position becomes the comparison target.

When all operands of a DISTINCT condition are *not null value*,  
*is distinct from* returns the same result as *not equal* (!=)  
and *is not distinct from* returns the same result as *equal* (=).

The DISTINCT condition treats NULL values as regular data, rather than as unknown, which distinguishes it from other comparison operators.

- IS DISTINCT FROM
    - When all operands are NULL
        - NULL is distinct from NULL => FALSE
    - When one operand is NULL
        - NULL is distinct from 1 => TRUE
        - 1 is distinct from NULL => TRUE
    - When neither operand is NULL
        - 1 is distinct from 1 => FALSE
        - 1 is distinct from 2 => TRUE
    - When operands are &lt;expr_list&gt;
        - ( 1, 2, 3 ) is distinct from ( 1, 2, 3 ) => FALSE
        - ( 1, 2, 3 ) is distinct from ( 1, 3, 3 ) => TRUE
        - ( 1, 2, 3 ) is distinct from ( 4, 5, 6 ) => TRUE

- IS NOT DISTINCT FROM
    - When all operands are NULL
        - NULL is not distinct from NULL => TRUE
    - When one operand is NULL
        - NULL is not distinct from 1 => FALSE
        - 1 is not distinct from NULL => FALSE
    - When neither operand is NULL
        - 1 is not distinct from 1 => TRUE
        - 1 is not distinct from 2 => FALSE
    - When operands are &lt;expr_list&gt;
        - ( 1, 2, 3 ) is not distinct from ( 1, 2, 3 ) => TRUE
        - ( 1, 2, 3 ) is not distinct from ( 1, 3, 3 ) => FALSE
        - ( 1, 2, 3 ) is not distinct from ( 4, 5, 6 ) => FALSE

<a id="0da7f60b339d6cc1"></a>
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

<a id="1f86c29e4d5ad711"></a>
### Compatibility

The SQL standard compatibility for conditions is as follows.

**SQL standard compatibility for conditions**

<a id="47677936dc650064"></a>
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

<a id="c7aeceb78ecfda89"></a>
## Regular Expression

A regular expression defines a search pattern using meta-characters (operators) and character literals.

```
July (fourth|4(th)?)
```

- Meta character (operator)
    - (), |, ?
- Character literal
    - July, fourth, 4, th
- Matching string
    - July fourth
    - July 4th
    - July 4

<a id="f49e16abfe8d2304"></a>
### Regular Expressions

- [REGEXP_LIKE Condition](#f7b851fa4ca3e27d)
- [REGEXP_COUNT](17-built-in-function-references.md#54924611a881f204)
- [REGEXP_INSTR](17-built-in-function-references.md#75e1a53f48309d9a)
- [REGEXP_REPLACE](17-built-in-function-references.md#42d99f66190078af)
- [REGEXP_SUBSTR](17-built-in-function-references.md#be5a2413d7c8ae27)

<a id="3fe49b08c719ab72"></a>
### Regular Expression Matching Options

The options specifying the matching operation of the regular expression are as follows.

- i
- c
- n
- m
- x

```
* i : case-insensitive matching

gSQL>
SELECT REGEXP_COUNT( 'Superscript digits', 's', 1, 'i' ) AS RESULT
  FROM dual;
RESULT
------
     3
1 row selected.
```

```
* c : case-sensitive matching

gSQL> 
SELECT REGEXP_COUNT( 'Superscript digits', 's', 1, 'c' ) AS RESULT
  FROM dual;
RESULT
------
     2
1 row selected.
```

```
* n : Dot operator(.) allows the match with the newline character.

gSQL> 
SELECT * FROM t1;
C1               
-----------------
matching options:
i, c, n, m, x    
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, ':.+', 1, 1, 'n' ) AS RESULT
  FROM t1;
RESULT       
-------------
:            
i, c, n, m, x
1 row selected.
```

```
* m : It specifies the newline character within the string as the multiline mode terminating the row.

gSQL> 
SELECT * FROM t1;
C1               
-----------------
matching options:
i, c, n, m, x    
1 row selected.

gSQL> 
SELECT REGEXP_COUNT( c1, '^.+', 1, 'm' ) AS RESULT
  FROM t1;
RESULT
------
     2
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, '^.+', 1, 1, 'm' ) AS RESULT1,
       REGEXP_SUBSTR( c1, '^.+', 1, 2, 'm' ) AS RESULT2
  FROM t1;
RESULT1           RESULT2      
----------------- -------------
matching options: i, c, n, m, x
1 row selected.
```

```
* x : It ignores the whitespace within the regular expression.

gSQL> 
SELECT REGEXP_SUBSTR('MATCHING', 'M A T C H I N G', 1, 1, 'x') AS RESULT
  FROM dual;
RESULT  
--------
MATCHING
1 row selected.
```

<a id="7abbfdba9d28e093"></a>
### Regular Expression Operators

The operator processes data from the database character set and includes multibyte characters in the match.

**Regular Expression Operators**

<a id="4d058db990f00702"></a>
<table><thead><tr><th align="center">Operator</th><th align="center">Description</th></tr></thead><tbody><tr><td valign="middle">\</td><td valign="middle">escape character<br>The backslash (\) treats the character following it as a literal.<br><ul><li>It can search for an operator as a character.<br><ul><li>e.g. \+ (It searches for + as a character.)</li><li>e.g. \\ (It searches for \ as a character.)</li></ul></li></ul></td></tr><tr><td valign="middle">.</td><td valign="middle">It matches one character.</td></tr><tr><td valign="middle">*</td><td valign="middle">It matches zero or more. (greedy)</td></tr><tr><td valign="middle">+</td><td valign="middle">It matches one or more. (greedy)</td></tr><tr><td valign="middle">?</td><td valign="middle">It matches 0 or 1 ( zero or one ). (greedy)</td></tr><tr><td valign="middle">|</td><td valign="middle">Alternation: It matches one of several expressions.</td></tr><tr><td valign="middle">^</td><td valign="middle"><ul><li>Default mode: It matches the beginning of the string.<br><ul><li>In the string abc\ndef, the regular expression ^. matches a.</li></ul></li><li>Multiline mode (matching option 'm'): It matches the beginning of each row in the string.<br><ul><li>In the string abc\ndef, the regular expression ^. matches a and d.</li></ul></li></ul></td></tr><tr><td valign="middle">$</td><td valign="middle"><ul><li>Default mode: It matches the character at the end of the string, or the character immediately before \n at the end of the string.<br><ul><li>e.g. In abc\ndef, abc\ndef\n strings, the regular expression .$ matches all occurrences of f.</li></ul></li><li>Multiline mode (matching option 'm'): It matches the end of each row in the string.<br><ul><li>e.g. In abc\ndef string, the regular expression .$ matches c and f.</li></ul></li></ul></td></tr><tr><td valign="middle">[ ]</td><td valign="middle">It matches one of the characters from the list within [ ].<br><ul><li>single character, - (range), [: :] (character class) can be included in the character list within [ ].<br><ul><li>e.g. REGEXP_SUBSTR( 'aB9', '[aA-Z[:digit:]]*' ) ==&gt; aB9</li></ul></li><li>The characters specified by - (range) are compared based on their Unicode binary codes.</li><li>All characters are interpreted as literals, except for - (range), [: :] (character class).</li><li>To include the ] (right bracket) character in the character list, it should be placed first in the list.<br><ul><li>e.g. REGEXP_SUBSTR( ']', '[]Bracket]' ) ==&gt; ]</li></ul></li><li>To include the - (hyphen) character in the character list, it should be placed first or last in the list.t.<br><ul><li>e.g. REGEXP_SUBSTR( '-', '[-Bracket]' ) ==&gt; -</li><li>e.g. REGEXP_SUBSTR( '-', '[Bracket-]' ) ==&gt; -</li></ul></li></ul></td></tr><tr><td valign="middle">[^ ]</td><td valign="middle">It matches characters that are not present in the character list inside [ ].<br><ul><li>The character list inside [ ] can include single characters, - (range), and [: :] (character class).<br><ul><li>e.g. REGEXP_SUBSTR( 'aB9', '[^aA-Z[:digit:]]*' ) ==&gt; NULL</li></ul></li><li>The characters specified by - (range) are compared based on their Unicode binary codes.</li><li>All characters are interpreted as literals, except for - (range) and [: :] (character class).</li></ul>*To include the ] (right bracket) character in the character list, it should be placed after the ^.<br><ul><li>N/A<br><ul><li>e.g. REGEXP_SUBSTR( ']', '[^]Bracket]' ) ==&gt; NULL</li></ul></li><li>To include the - (hyphen) character in the character list, it should be placed after the ^ or at the end of the list.<br><ul><li>e.g. REGEXP_SUBSTR( '-', '[^-Bracket]' ) ==&gt; NULL</li><li>e.g. REGEXP_SUBSTR( '-', '[^Bracket-]' ) ==&gt; NULL</li></ul></li></ul></td></tr><tr><td valign="middle">( )</td><td valign="middle">It treats the expression within ( ) as a subexpression group.<br>A subexpression can be included within another subexpression.<br>Subexpressions are numbered from left to right, starting with the opening parenthesis ( of the subexpression.<br><ul><li>(abc)((12(345))67(89))<br><ul><li>1 : abc</li><li>2 : 123456789</li><li>3 : 12345</li><li>4 : 345</li><li>5 : 89</li></ul></li></ul></td></tr><tr><td valign="middle">{m}</td><td valign="middle">It matches m times.</td></tr><tr><td valign="middle">{m,}</td><td valign="middle">It matches at least m times. (greedy)</td></tr><tr><td valign="middle">{m,n}</td><td valign="middle">It matches at least m times and at most n times. (greedy)</td></tr><tr><td valign="middle">\n</td><td valign="middle">Back Reference<br>It matches the n-th subexpression defined before the back reference.<br>n is an integer between 1 and 9.<br>The back reference counts subexpressions from left to right, starting with the opening parenthesis ( of each subexpression.</td></tr><tr><td valign="middle">b[: :]</td><td valign="middle">It matches characters that belong to a specified character class.<br><ul><li>[:alnum:] : Alphabetic characters and digits</li><li>[:alpha:] : Alphabetic characters</li><li>[:blank:] : Whitespace and tab</li><li>[:cntrl:] : Control characters</li><li>[:digit:] : Digits</li><li>[:graph:] : Printable characters, excluding space</li><li>[:lower:] : Lowercase letters</li><li>[:print:] : Printable characters, including space</li><li>[:punct:] : Special characters</li><li>[:space:] : Whitespace characters</li><li>[:upper:] : Uppercase letters</li><li>[:xdigit:] : Hexadecimal digits</li></ul></td></tr><tr><td valign="middle">\d</td><td valign="middle">It matches a digit character.<br>It is the same as [[:digit:]].</td></tr><tr><td valign="middle">\D</td><td valign="middle">It matches a character that is not a digit.<br>It is the same as [^[:digit:]].</td></tr><tr><td valign="middle">\w</td><td valign="middle">It matches an alphanumeric character or an underscore.<br>It is the same as [[:alnum:]_].</td></tr><tr><td valign="middle">\W</td><td valign="middle">It matches a character that is not a word character.<br>It is the same as [^[:alnum:]_].</td></tr><tr><td valign="middle">\s</td><td valign="middle">It matches a whitespace character.<br>It is the same as [[:space:]].</td></tr><tr><td valign="middle">\S</td><td valign="middle">It matches a character that is not a whitespace character.<br>It is the same as [^[:space:]].</td></tr><tr><td valign="middle">\A</td><td valign="middle">It matches the start of the string.</td></tr><tr><td valign="middle">\Z</td><td>It matches the character at the end of the string or the character immediately before \n at the end of the string.<br>e.g. The regular expression .\Z matches the character f in both abc\ndef and abc\ndef\n.</td></tr><tr><td valign="middle">\z</td><td valign="middle">It matches the end of the string.</td></tr><tr><td valign="middle">*?</td><td valign="middle">It matches 0 or more times. (nongreedy)</td></tr><tr><td valign="middle">+?</td><td valign="middle">It matches one or more times. (nongreedy)</td></tr><tr><td valign="middle">??</td><td valign="middle">It matches 0 or 1 time. (nongreedy)</td></tr><tr><td valign="middle">{m}?</td><td valign="middle">It matches m times. (nongreedy)</td></tr><tr><td valign="middle">{m,}?</td><td valign="middle">It matches at least m times. (nongreedy)</td></tr><tr><td valign="middle">{m,n}?</td><td valign="middle">It matches at least m times and at most n times. (nongreedy)</td></tr></tbody></table>

- greedy
    - It finds the items that match the pattern as many times as possible.
- nongreedy
    - It finds the items that match the pattern as few times as possible.

```
### e.g.

gSQL> 
SELECT REGEXP_SUBSTR( 'axxxbxbxb', 'a\w+b' ) AS RES_GREEDY,
       REGEXP_SUBSTR( 'axxxbxbxb', 'a\w+?b' ) AS RES_NON_GREEDY
  FROM dual;
RES_GREEDY RES_NON_GREEDY
---------- --------------
axxxbxbxb  axxxb         
1 row selected.
```

The following are examples of using each regular expression operator.

```
• \

gSQL> 
SELECT REGEXP_SUBSTR( '(a)\1', '\(a\)\\1' ) AS RESULT FROM dual;
RESULT
------
(a)\1 
1 row selected.
```

```
•.

gSQL> SELECT REGEXP_SUBSTR( 'abcde', 'a...e' ) AS RESULT FROM dual;
RESULT
------
abcde 
1 row selected.
```

```
• *, +, ?

gSQL> 
SELECT REGEXP_SUBSTR( 'ab', 'ax*b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axb', 'ax*b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxb', 'ax*b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
ab      axb     axxxb  
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'ab', 'ax+b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axb', 'ax+b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxb', 'ax+b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
null    axb     axxxb  
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'ab', 'ax?b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axb', 'ax?b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxb', 'ax?b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
ab      axb     null   
1 row selected.
```

```
• |

gSQL> 
SELECT REGEXP_SUBSTR( 'Regexp', '(R|r)egexp' ) AS RESULT1,
       REGEXP_SUBSTR( 'regexp', '(R|r)egexp' ) AS RESULT2
 FROM dual;
RESULT1 RESULT2
------- -------
Regexp  regexp 
1 row selected.
```

```
• ^, $

gSQL> 
SELECT * FROM t1;
C1             
---------------
Line1 : aaa xy1
Line2 : bbb xy2
Line3 : ccc xy3
1 row selected.

gSQL> 
SELECT REGEXP_COUNT( c1, '^Line[[:digit:]]' ) AS RESULT_DEFAULT_MODE,
       REGEXP_COUNT( c1, '^Line[[:digit:]]', 1, 'm' ) AS RESULT_MULTILINE_MODE
  FROM t1;
RESULT_DEFAULT_MODE RESULT_MULTILINE_MODE
------------------- ---------------------
                  1                     3
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, '^Line[[:digit:]]', 1 ) AS RES_DEFAULT,
       REGEXP_SUBSTR( c1, '^Line[[:digit:]]', 1, 1, 'm' ) AS RES_MULTILINE_1,
       REGEXP_SUBSTR( c1, '^Line[[:digit:]]', 1, 2, 'm' ) AS RES_MULTILINE_2,
       REGEXP_SUBSTR( c1, '^Line[[:digit:]]', 1, 3, 'm' ) AS RES_MULTILINE_3
  FROM t1;
RES_DEFAULT RES_MULTILINE_1 RES_MULTILINE_2 RES_MULTILINE_3
----------- --------------- --------------- ---------------
Line1       Line1           Line2           Line3          
1 row selected.


gSQL> 
SELECT REGEXP_COUNT( c1, 'xy[[:digit:]]$' ) AS RESULT_DEFAULT_MODE,
       REGEXP_COUNT( c1, 'xy[[:digit:]]$', 1, 'm' ) AS RESULT_MULTILINE_MODE
  FROM t1;
RESULT_DEFAULT_MODE RESULT_MULTILINE_MODE
------------------- ---------------------
                  1                     3
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, 'xy[[:digit:]]$', 1 ) AS RES_DEFAULT,
       REGEXP_SUBSTR( c1, 'xy[[:digit:]]$', 1, 1, 'm' ) AS RES_MULTILINE_1,
       REGEXP_SUBSTR( c1, 'xy[[:digit:]]$', 1, 2, 'm' ) AS RES_MULTILINE_2,
       REGEXP_SUBSTR( c1, 'xy[[:digit:]]$', 1, 3, 'm' ) AS RES_MULTILINE_3
  FROM t1;
RES_DEFAULT RES_MULTILINE_1 RES_MULTILINE_2 RES_MULTILINE_3
----------- --------------- --------------- ---------------
xy3         xy1             xy2             xy3            
1 row selected.
```

```
• [ ], [^ ]

gSQL> 
SELECT REGEXP_SUBSTR( 'a', '[abc]' ) AS RESULT1,
       REGEXP_SUBSTR( 'A', '[A-Z]' ) AS RESULT2,
       REGEXP_SUBSTR( '1', '[[:digit:]]' ) AS RESULT3,
       REGEXP_SUBSTR( 'abAB12', '[abcA-Z[:digit:]]+' ) AS RESULT
  FROM dual;
RESULT1 RESULT2 RESULT3 RESULT
------- ------- ------- ------
a       A       1       abAB12
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'x', '[^abc]' ) AS RESULT1,
       REGEXP_SUBSTR( 'y', '[^A-Z]' ) AS RESULT2,
       REGEXP_SUBSTR( 'z', '[^[:digit:]]' ) AS RESULT3,
       REGEXP_SUBSTR( 'xyz', '[^abcA-Z[:digit:]]+' ) AS RESULT
  FROM dual;
RESULT1 RESULT2 RESULT3 RESULT
------- ------- ------- ------
x       y       z       xyz   
1 row selected.
```

```
• ( ), \n

gSQL> 
SELECT REGEXP_SUBSTR( 'abcbcabc', 'a(bc)\1a\1' ) AS RESULT1,
       REGEXP_SUBSTR( 'abcbcabc', '(a)(b)(c)\2\3\1\2\3' ) AS RESULT2,
       REGEXP_SUBSTR( 'abcbcabc', '(a(bc))\2\1' ) AS RESULT3
 FROM dual;
RESULT1  RESULT2  RESULT3 
-------- -------- --------
abcbcabc abcbcabc abcbcabc
1 row selected.
```

```
• {m}, {m,}, {m,n}

gSQL> 
SELECT REGEXP_SUBSTR( 'axxb', 'ax{3}b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxb', 'ax{3}b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxxxb', 'ax{3}b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
null    axxxb   null   
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'axxb', 'ax{3,}b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxb', 'ax{3,}b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxxxb', 'ax{3,}b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
null    axxxb   axxxxxb
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'axxb', 'ax{3,5}b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxb', 'ax{3,5}b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxxxb', 'ax{3,5}b' ) AS RESULT3,
       REGEXP_SUBSTR( 'axxxxxxxb', 'ax{3,5}b' ) AS RESULT4
  FROM dual;
RESULT1 RESULT2 RESULT3 RESULT4
------- ------- ------- -------
null    axxxb   axxxxxb null   
1 row selected.
```

```
• [: :]

gSQL> 
SELECT REGEXP_SUBSTR( 'abc123', '[[:alnum:]]+' ) AS RESULT1,
       REGEXP_SUBSTR( 'abc', '[[:alpha:]]+' ) AS RESULT2,
       REGEXP_SUBSTR( '123', '[[:digit:]]+' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
abc123  abc     123    
1 row selected.
```

```
• \d, \D, \w, \W, \s, \S

gSQL> 
SELECT REGEXP_SUBSTR( '123', '\d+' ) AS RESULT1,
       REGEXP_SUBSTR( 'abc', '\D+' ) AS RESULT2
  FROM dual;
RESULT1 RESULT2
------- -------
123     abc    
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'A_B_C', '\w+' ) AS RESULT1,
       REGEXP_SUBSTR( '+ @', '\W+' ) AS RESULT2
  FROM dual;
RESULT1 RESULT2
------- -------
A_B_C   + @    
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'a   d', 'a\s+d' ) AS RESULT1,
       REGEXP_SUBSTR( 'abc d', '\S+' ) AS RESULT2
  FROM dual;
RESULT1 RESULT2
------- -------
a   d   abc    
1 row selected.
```

```
• \A

gSQL> 
select * from t1;
C1             
---------------
Line1 : aaa xy1
Line2 : bbb xy2
Line3 : ccc xy3
1 row selected.

gSQL> 
SELECT REGEXP_COUNT( c1, '\ALine[[:digit:]]' ) AS RESULT_DEFAULT_MODE,
       REGEXP_COUNT( c1, '\ALine[[:digit:]]', 1, 'm' ) AS RESULT_MULTILINE_MODE
  FROM t1;
RESULT_DEFAULT_MODE RESULT_MULTILINE_MODE
------------------- ---------------------
                  1                     1
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, '\ALine[[:digit:]]' ) AS RESULT_DEFAULT_MODE,
       REGEXP_SUBSTR( c1, '\ALine[[:digit:]]', 1, 1, 'm' ) AS RESULT_MULTILINE_MODE
  FROM t1;
RESULT_DEFAULT_MODE RESULT_MULTILINE_MODE
------------------- ---------------------
Line1               Line1                
1 row selected.
```

```
• \Z

gSQL> 
SELECT c1 FROM t1;
C1 
---
abc    <-- First record abc\ndef 
def
abc    <-- Second record abc\ndef\n
def
   
2 rows selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, '.\Z' ) AS REGEXP_SUBSTR_RES 
  FROM t1;
REGEXP_SUBSTR_RES
-----------------
f                
f                
2 rows selected.
```

```
• \z

gSQL> 
SELECT * FROM t1;
C1             
---------------
Line1 : aaa xy1
Line2 : bbb xy2
Line3 : ccc xy3
1 row selected.

gSQL> 
SELECT REGEXP_COUNT( c1, '\w+\d\z' ) AS RESULT_DEFAULT_MODE,
       REGEXP_COUNT( c1, '\w+\d\z', 1, 'm' ) AS RESULT_MULTILINE_MODE
  FROM t1;
RESULT_DEFAULT_MODE RESULT_MULTILINE_MODE
------------------- ---------------------
                  1                     1
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, '\w+\d\z' ) AS RESULT_DEFAULT_MODE,
       REGEXP_SUBSTR( c1, '\w+\d\z', 1, 1, 'm' ) AS RESULT_MULTILINE_MODE
  FROM t1;
RESULT_DEFAULT_MODE RESULT_MULTILINE_MODE
------------------- ---------------------
xy3                 xy3                  
1 row selected.
```

```
• *?, +?, ??

gSQL> 
SELECT REGEXP_SUBSTR( 'ab', 'a\w*?b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxbxb', 'a\w*?b' ) AS RESULT2
  FROM dual;
RESULT1 RESULT2
------- -------
ab      axxxb  
1 row selected.


gSQL> 
SELECT REGEXP_SUBSTR( 'ab', 'a\w+?b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxbxb', 'a\w+?b' ) AS RESULT2
  FROM dual;
RESULT1 RESULT2
------- -------
null    axxxb  
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'ab', 'a\w??b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axbxb', 'a\w??b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxbxb', 'a\w?b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
ab      axb     null   
1 row selected.
```

```
• {n}?, {n,}?, {n,m}?

gSQL> 
SELECT REGEXP_SUBSTR( 'abxb', 'a\w{3}?b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxbxbxb', 'a\w{3}?b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxxxbxbxb', 'a\w{3}?b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
null    axxxb   null   
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'abxb', 'a\w{3,}?b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxbxb', 'a\w{3,}?b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxxxbxbxb', 'a\w{3,}?b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
null    axxxb   axxxxxb
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'abxb', 'a\w{3,5}?b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxbxb', 'a\w{3,5}?b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxxxbxbxb', 'a\w{3,5}?b' ) AS RESULT3,
       REGEXP_SUBSTR( 'axxxxxxxbxbxb', 'a\w{3,5}?b' ) AS RESULT4
  FROM dual;
RESULT1 RESULT2 RESULT3 RESULT4
------- ------- ------- -------
null    axxxb   axxxxxb null   
1 row selected.
```

<a id="5f5005d01175dec7"></a>
## JSON String Constructor

The JSON string constructor is a function that takes an SQL expression as an argument and generates a string in JSON format.

The JSON string constructor is categorized as follows:  
• JSON value constructor  
• JSON aggregate constructor  
• JSON window constructor

<a id="2763c0825b7b4369"></a>
### JSON String Constructor

<a id="1050549ebace95a5"></a>
#### JSON value Constructor

The JSON value constructor is a single row function that generates one JSON string row for each input row.

The JSON value constructor is categorized as follows:

- [JSON_ARRAY](17-built-in-function-references.md#63c4885c31474998)
- [JSON_OBJECT](17-built-in-function-references.md#fbd9eb4c70306dc1)

<a id="8f919c556b771612"></a>
#### JSON aggregate Constructor

The JSON aggregate constructor is an aggregate function that generates a single JSON string row by aggregating the results.

The JSON aggregate constructor is categorized as follows:

- [JSON_ARRAYAGG](17-built-in-function-references.md#7bc8aa387314ee48)
- [JSON_OBJECTAGG](17-built-in-function-references.md#61c76e5d901661ed)

<a id="722fcac87eabd4b5"></a>
#### JSON window Constructor

The JSON window constructor is a window function that generates JSON strings over a defined range of records using the OVER clause.

It differs from an aggregate function in that the number of result rows is determined by the groups within the window.

The JSON window constructor is categorized as follows:

- [JSON_ARRAYAGG() OVER](17-built-in-function-references.md#b3c3b1418c509029)
- [JSON_OBJECTAGG() OVER](17-built-in-function-references.md#821bcca33f74cbfd)

<a id="21c4e29fa3fa142a"></a>
### JSON String

There are two types of JSON strings: JSON object strings and JSON array strings.

<a id="c983999273e3f20f"></a>
#### JSON Object String

A JSON object string is composed of consecutive key-value pairs enclosed in curly braces, and each key must be an SQL string.

```
{ key : value }
{ key : value, key : value, ... }
```

The following three functions return a JSON object string as the result.

- [JSON_OBJECT](17-built-in-function-references.md#fbd9eb4c70306dc1)
- [JSON_OBJECTAGG](17-built-in-function-references.md#61c76e5d901661ed)
- [JSON_OBJECTAGG() OVER](17-built-in-function-references.md#821bcca33f74cbfd)

<a id="fb0da57780ef2b83"></a>
#### JSON Array String

A JSON array string is composed of a sequence of values enclosed in square brackets.

```
[ value ]
[ value, value, ... ]
```

The following three functions return a JSON array string as the result.

- [JSON_ARRAY](17-built-in-function-references.md#63c4885c31474998)
- [JSON_ARRAYAGG](17-built-in-function-references.md#7bc8aa387314ee48)
- [JSON_ARRAYAGG() OVER](17-built-in-function-references.md#b3c3b1418c509029)

<a id="2d687246a09b4226"></a>
### JSON Structural Characters

There are six types of characters that make up a JSON string.

<a id="2b1a83ac806685a8"></a>
| JSON structural character | Description |
| --- | --- |
| [ | It is the square bracket used to start a JSON array string. |
| ] | It is the square bracket used to close a JSON array string. |
| { | It is the curly brace used to start a JSON object string. |
| } | It is the curly brace used to close a JSON object string. |
| : | It is the character that separates keys. |
| , | It is the character that separates values. |

These characters allow spaces before and after them.

<a id="7f2a149b7dceec11"></a>
### JSON Escape Characters

The characters that are escaped within a JSON string are as follows.

<a id="e6c59cec7338d5d1"></a>
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

<a id="17faa0e2553ffb68"></a>
### JSON Result Control Options

<a id="917c50e61800ff6a"></a>
#### JSON Constructor Null Clause

These options control the output when the value argument of the JSON string constructor is null.

```
<JSON constructor null clause> ::=
    NULL ON NULL
  | ABSENT ON NULL
  | EMPTY STRING ON NULL
```

<a id="cfb13d6f91c75d24"></a>
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

<a id="e6b9ce363aa8be02"></a>
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

<a id="45dac4ba777ff541"></a>
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

<a id="2b244b19e881dcb5"></a>
#### JSON Key Uniqueness Constraint

The allowance of duplicate JSON object key fields can be configured.

```
<JSON key uniqueness constraint> ::=
    WITH UNIQUE [ KEYS ]
  | WITHOUT UNIQUE [ KEYS ]
```

<a id="6a1f1742d0563880"></a>
##### WITH UNIQUE [ KEYS ]

Duplicate keys are not allowed within a JSON object. An error is returned if duplicates exist.

```
CREATE TABLE t1 ( key1 VARCHAR(3), data1 VARCHAR(3) );
INSERT INTO t1 VALUES ( 'K1', 'D1' );
INSERT INTO t1 VALUES ( 'K2', 'D2' );
INSERT INTO t1 VALUES ( 'K1', 'D3' );
COMMIT;

gSQL> SELECT JSON_OBJECTAGG( key1 VALUE data1 WITH UNIQUE KEYS ) AS result 
        FROM t1;

ERR-42000(13065): duplicate key names 'K1' in JSON object
```

<a id="fcdf06ffa1a09365"></a>
##### WITHOUT UNIQUE [ KEYS ]

Duplicate keys are allowed within a JSON object.

```
gSQL> SELECT JSON_OBJECTAGG( key1 VALUE data1 WITHOUT UNIQUE KEYS ) AS result
      FROM t1;

RESULT                         
-------------------------------
{"K1":"D1","K2":"D2","K1":"D3"}

1 row selected.
```

<a id="d705909cfd7dce0a"></a>
#### JSON Array Aggregate Order By Clause

It generates the JSON_ARRAYAGG result by sorting values according to the sort specification list specified in the ORDER BY clause.

```
<JSON array aggregate order by clause> ::=
    ORDER BY <sort specification list>

<sort specification list> ::=
    <sort specification> [ { <comma> <sort specification> }... ]

<sort specification> ::=
    <sort key> [ <ordering specification> ] [ <null ordering> ]

<sort key> ::=
    <value expression>

<ordering specification> ::=
      ASC
    | DESC

<null ordering> ::=
      NULLS FIRST
    | NULLS LAST
```

The following is an example of sorting JSON array values using the JSON array aggregate order by clause.

```
CREATE TABLE t1 ( c1 int );
INSERT INTO t1 VALUES (3),(1),(null),(2);

gSQL> SELECT JSON_ARRAYAGG( c1 ) AS res_json_sort
       FROM t1;

RES_JSON_SORT
-------------
[3,1,2]     

gSQL> SELECT JSON_ARRAYAGG( c1 ORDER BY c1 ) AS res_json_sort
       FROM t1;

RES_JSON_SORT
-------------
[1,2,3]
```

- &lt;ordering specification&gt;
    - It specifies the sort order.
        - ASC: Sorts in ascending order.
        - DESC: Sorts in descending order.
    - If not specified, the default is ASC.

```
gSQL> SELECT JSON_ARRAYAGG( c1 ORDER BY c1 ASC ) AS res_json_sort
        FROM t1;

RES_JSON_SORT
-------------
[1,2,3]                            

1 row selected.

gSQL> SELECT JSON_ARRAYAGG( c1 ORDER BY c1 DESC ) AS res_json_sort
        FROM t1;

RES_JSON_SORT
-------------
[3,2,1]                             

1 row selected.
```

- &lt;null ordering&gt;
    - It specifies the order of NULL and non-NULL values.
        - NULLS FIRST: Sorts NULL values first. 
        - NULLS LAST: PSorts NULL values last. 
    - If not specified, the default is NULLS LAST.

```
gSQL> SELECT JSON_ARRAYAGG( c1 ORDER BY c1 NULL ON NULL ) AS res_json_sort
        FROM t1;

RES_JSON_SORT
-------------
[1,2,3,null]                                

1 row selected.

gSQL> SELECT JSON_ARRAYAGG( c1 ORDER BY c1 NULLS FIRST NULL ON NULL ) AS res_json_sort
        FROM t1;

RES_JSON_SORT
-------------
[null,1,2,3]                                            

1 row selected.

gSQL> SELECT JSON_ARRAYAGG( c1 ORDER BY c1 NULLS LAST NULL ON NULL ) AS res_json_sort
        FROM t1;

RES_JSON_SORT
-------------
[1,2,3,null]                                           

1 row selected.
```

<a id="91fe9ef765ec473f"></a>
#### JSON Output Clause

The result type and output format of the string generated by the JSON string constructor can be controlled.

```
<JSON output clause> ::=
    RETURNING <string data type> [PRETTY]

<string data type> ::=
    CHAR(n)
  | VARCHAR(n)
  | LONG VARCHAR
```

- The data type of the result string can be specified.
    - The data type must be one of the character string types.

- The output format can be changed using the PRETTY option.

The following is an example that specifies the result data type using the JSON output clause.

```
gSQL> SELECT JSON_OBJECT( name VALUE balances RETURNING VARCHAR(100) ) AS res_json_object
        FROM accounts;

RES_JSON_OBJECT
---------------
{"Alice":50000}
{"Bob":null}   
{"Chris":1000} 

3 rows selected.
```

The following is the result of applying the PRETTY option to the same example.

```
gSQL> SELECT JSON_OBJECT( name VALUE balances RETURNING VARCHAR(100) PRETTY ) AS res_json_object
        FROM accounts;

RES_JSON_OBJECT  
-----------------
{                
    "Alice":50000
}                
{                
    "Bob":null   
}                
{                
    "Chris":1000 
}                

3 rows selected.
```

<a id="7d74e835d9d4cc95"></a>
### JSON String Output Format

The string generated by the JSON string constructor is output as follows, depending on the SQL data type of the expression argument.

<a id="1e9ba8ba38c24d42"></a>
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

<a id="1f307e7156ddf768"></a>
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

<a id="6256ec6393808693"></a>
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

<a id="52f93701deb757b6"></a>
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

<a id="463d3ce23d41ef3d"></a>
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

<a id="46b3baf532d74d35"></a>
#### Date/ Time

<a id="f2dabd9d34fc6494"></a>
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

<a id="e54d2293168b1ed0"></a>
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

<a id="4c8c65774fea53ea"></a>
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

<a id="e23e03bc9b44fa62"></a>
#### Interval

The interval type follows the duration format defined by ISO 8601.

<a id="d46e68f93edb2978"></a>
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

<a id="74255fc07c376597"></a>
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

<a id="b3d01ed93b9025c0"></a>
### Compatibility

The SQL standard compatibility for the JSON string constructor is as follows.

**SQL standard compatibility for functions**

<a id="191491454a722d06"></a>
| Feature ID | Description | Availability |
| --- | --- | --- |
| T811 | Basic SQL/JSON constructor functions | O |
| T812 | SQL/JSON: JSON_OBJECTAGG | O |
| T813 | SQL/JSON: JSON_ARRAYAGG with ORDER BY | O |
| T814 | Colon in JSON_OBJECT or JSON_OBJECTAGG | O |
| T830 | Enforcing unique keys in SQL/JSON constructor functions | O |

---

[← 10. Server Property](../part-02-administration-manual/10-server-property.md) · [Table of contents](../README.md) · [12. SQL Languages →](12-sql-languages.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
