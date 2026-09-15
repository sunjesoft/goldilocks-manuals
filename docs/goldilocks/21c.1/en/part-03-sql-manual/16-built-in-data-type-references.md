<a id="af245228e0cc4b4e"></a>

# 16. Built-in Data Type References

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/af245228e0cc4b4e)  
> Tag: `21c.1_35_tag`

[← 15. SQL Tuning](15-sql-tuning.md) · [Table of contents](../README.md) · [17. Built-in Function References →](17-built-in-function-references.md)

<a id="9595e6e5f4617073"></a>
## Aliases of Built-in Data Types

- BIGINT
    - It is as same as NUMBER(19,0).
    - Refer to [NUMBER](#0528f4e214aa9174).
- BINARY
    - Refer to [BINARY](#903ceec0bccf512c).
- BINARY VARYING
    - Refer to [BINARY VARYING](#c989ee4e53c29ac8).
- BINARY LONG VARYING
    - Refer to [BINARY LONG VARYING](#411320dfee032cb9).
- BOOLEAN
    - Refer to [BOOLEAN](#3e2be4ffbf1adeb4).
- CHAR
    - It is as same as CHARACTER.
    - Refer to [CHARACTER](#577b1040addb69dc).
- CHARACTER
    - Refer to [CHARACTER](#577b1040addb69dc).
- CHARACTER VARYING
    - Refer to [CHARACTER VARYING](#152a268c572008b1).
- CHARACTER LONG VARYING
    - Refer to [CHARACTER LONG VARYING](#b058aea936972774).
- DATE
    - Refer to [DATE](#1876eba8c76e5c08).
- DEC
    - It is as same as NUMERIC.
    - Refer to [NUMERIC](#2051e8f8ae4daa81).
- DECIMAL
    - It is as same as NUMERIC.
    - Refer to [NUMERIC](#2051e8f8ae4daa81).
- DOUBLE
    - It is as same as FLOAT(53).
    - Refer to [FLOAT](#92493efa6e610bbe).
- DOUBLE PRECISION
    - It is as same as FLOAT(53).
    - Refer to [FLOAT](#92493efa6e610bbe).
- FLOAT
    - Refer to [FLOAT](#92493efa6e610bbe).
- FLOAT4
    - It is as same as FLOAT(24).
    - Refer to [FLOAT](#92493efa6e610bbe).
- FLOAT8
    - It is as same as FLOAT(53).
    - Refer to [FLOAT](#92493efa6e610bbe).
- INT
    - It is as same as NUMBER(10,0).
    - Refer to [NUMBER](#0528f4e214aa9174).
- INT2
    - It is as same as NUMBER(5,0).
    - Refer to [NUMBER](#0528f4e214aa9174).
- INT4
    - It is as same as NUMBER(10,0).
    - Refer to [NUMBER](#0528f4e214aa9174).
- INT8
    - It is as same as NUMBER(19,0).
    - Refer to [NUMBER](#0528f4e214aa9174).
- INTEGER
    - It is as same as NUMBER(10,0).
    - Refer to [NUMBER](#0528f4e214aa9174).
- INTERVAL
    - Refer to [INTERVAL](#6d2310477d861113).
- LONG BINARY VARYING
    - It is as same as BINARY LONG VARYING. 
    - Refer to [BINARY LONG VARYING](#411320dfee032cb9).
- LONG CHAR VARYING
    - It is as same as CHARACTER LONG VARYING. 
    - Refer to [CHARACTER LONG VARYING](#b058aea936972774).
- LONG CHARACTER VARYING
    - It is as same as CHARACTER LONG VARYING. 
    - Refer to [CHARACTER LONG VARYING](#b058aea936972774).
- LONG VARCHAR
    - It is as same as CHARACTER LONG VARYING.
    - Refer to [CHARACTER LONG VARYING](#b058aea936972774).
- NATIVE_BIGINT
    - Refer to [NATIVE_BIGINT](#62ab51de7e978ede).
- NATIVE_DOUBLE
    - Refer to [NATIVE_DOUBLE](#650f2a5883a8059d).
- NATIVE_INTEGER
    - Refer to [NATIVE_INTEGER](#6077bca8efaefd77).
- NATIVE_REAL
    - Refer to [NATIVE_REAL](#a7040ee2777d995c).
- NATIVE_SMALLINT
    - Refer to [NATIVE_SMALLINT](#b6bf9340bbfc4904).
- NUMBER
    - Refer to [NUMBER](#0528f4e214aa9174).
- NUMERIC
    - Refer to [NUMERIC](#2051e8f8ae4daa81).
- ROWID
    - Refer to [ROWID](#5640cb398d2830d1).
- SMALLINT
    - It is as same as NUMBER(5,0). 
    - Refer to [NUMBER](#0528f4e214aa9174).
- TIME
    - Refer to [TIME](#4c35506be1ac9ad6).
- TIMESTAMP
    - Refer to [TIMESTAMP](#fa1328ca29a5e4f3).
- VARBINARY
    - It is as same as BINARY VARYING.
    - Refer to [BINARY VARYING](#c989ee4e53c29ac8).
- VARCHAR
    - It is as same as CHARACTER VARYING. 
    - Refer to [CHARACTER VARYING](#152a268c572008b1).
- VARCHAR2
    - It is as same as CHARACTER VARYING. 
    - Refer to [CHARACTER VARYING](#152a268c572008b1).

<a id="903ceec0bccf512c"></a>
## BINARY

<a id="b0621d74300ec508"></a>
### Syntax

```
BINARY [ (length) ]
```

<a id="e5412ca982da166f"></a>
### Syntax Rules and Parameters

- length: It is the binary string length.
    - Range: 1 ~ 2000
    - Default value: 1

<a id="7c53a406b39dcef0"></a>
### Description

A fixed-length binary string is stored.  
If the binary string length to be stored is shorter than the specified length,  X'00 ' is stored in the remaining part.  
• Storage size: Bytes of the length value

<a id="1e60ed844382aa2c"></a>
### For More Information

Refer to the followings.

- [BINARY VARYING](#c989ee4e53c29ac8)
- [BINARY LONG VARYING](#411320dfee032cb9)

<a id="c989ee4e53c29ac8"></a>
## BINARY VARYING

<a id="01832384af609a3f"></a>
### Syntax

```
BINARY VARYING (length)
```

<a id="40be0823718aee3d"></a>
### Syntax Rules and Parameters

- length: It is the maximum length of binary string.
    - Range: 1 ~ 4000

<a id="3d6ec91cef1b9005"></a>
### Description

The variable-length binary string is stored.  

• Storage size: Bytes of the binary string to be stored  
• Alias names: VARBINARY

<a id="e3affbcfd976434c"></a>
### For More Information

Refer to the followings.

- [BINARY](#903ceec0bccf512c)
- [BINARY LONG VARYING](#411320dfee032cb9)

<a id="411320dfee032cb9"></a>
## BINARY LONG VARYING

<a id="529daf636a07db9f"></a>
### Syntax

```
BINARY LONG VARYING
```

<a id="9568968f3e5803ea"></a>
### Description

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

<a id="88c30332c440ba52"></a>
### For More Information

Refer to the followings.

- [BINARY](#903ceec0bccf512c)
- [BINARY VARYING](#c989ee4e53c29ac8)

<a id="3e2be4ffbf1adeb4"></a>
## BOOLEAN

<a id="ce8d3e8a454efce5"></a>
### Syntax

```
BOOLEAN
```

<a id="6ff8dd1a0c9d37ed"></a>
### Description

TRUE or FALSE is stored.  
• Storage size: 1 byte.

<a id="577b1040addb69dc"></a>
## CHARACTER

<a id="6b88945492410ecb"></a>
### Syntax

```
CHARACTER [ (length [ CHARACTERS | OCTETS | CHAR | BYTE ] ) ]
```

<a id="e134b9b31754ea8e"></a>
### Syntax Rules and Parameters

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
    - If omitted, the default is the property value of [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#305fe0fd4eb06210) which is set when creating database.

<a id="14389d5bdfd16329"></a>
### Description

A fixed-length string is stored.  
If the length of the string to be stored is shorter than the specified length, white spaces are stored in the remaining part.

- Storage size: Bytes of the length value
- Alias name: CHAR

<a id="103f0a8dfcfe0eaa"></a>
### For More Information

Refer to the followings.

- [CHARACTER VARYING](#152a268c572008b1)
- [CHARACTER LONG VARYING](#b058aea936972774)

<a id="152a268c572008b1"></a>
## CHARACTER VARYING

<a id="56a68186a601d343"></a>
### Syntax

```
CHARACTER VARYING ( length [ CHARACTERS | OCTETS | CHAR | BYTE ] )
```

<a id="c8517ed1da64f277"></a>
### Syntax Rules and Parameters

- length: It is the string length.
    - Range: 1 ~ 4000

- [ CHARACTERS | OCTETS | CHAR | BYTE ]: It is unit of length.
    - CHARACTERS
        - The number of characters
        - CHAR is as same as CHARACTERS.
    - OCTETS
        - The number of bytes
        - BYTE is as same as OCTETS.
    - If omitted, the default is the property value of [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#305fe0fd4eb06210) which is set when creating database.

<a id="aa8ea51287184900"></a>
### Description

The variable-length string is stored.  

• Storage size: Bytes of the string to be stored  
• Alias names: VARCHAR, VARCHAR2

<a id="95cf26b502662ea8"></a>
### For More Information

Refer to the followings.

- [CHARACTER](#577b1040addb69dc)
- [CHARACTER LONG VARYING](#b058aea936972774)

<a id="b058aea936972774"></a>
## CHARACTER LONG VARYING

<a id="7ab2e80369498e26"></a>
### Syntax

```
CHARACTER LONG VARYING
```

<a id="b1e6e170fbfbbe6f"></a>
### Description

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

<a id="9e81b0e2dfe515db"></a>
### For More Information

Refer to the followings.

- [CHARACTER](#577b1040addb69dc)
- [CHARACTER VARYING](#152a268c572008b1)

<a id="1876eba8c76e5c08"></a>
## DATE

<a id="82354995528316ca"></a>
### Syntax

```
DATE
```

<a id="e94cedee7075ea8f"></a>
### Description

It is the date type including YEAR, MONTH, DAY, HOUR, MINUTE and SECOND (excluding fractional seconds).  
• Value range: Date value between '4714-11-24 BC' and '9999-12-31 AD'   
• Storage size: 8 bytes

<a id="e980312a25778c88"></a>
### For More Information

Refer to the followings.

- [Date Literals](11-sql-elements.md#301907176cba74f1)
- [TIME](#4c35506be1ac9ad6)
- [TIMESTAMP](#fa1328ca29a5e4f3)

<a id="92493efa6e610bbe"></a>
## FLOAT

<a id="0ffef8bd20961f85"></a>
### Syntax

```
FLOAT[ ( precision ) ]
```

<a id="5397546f26b5a1ce"></a>
### Syntax Rules and Parameters

- precision: It is the binary precision of significant digits.
    - Precision range: 1 ~ 126
    - Default value: 126

<a id="09d876506a700008"></a>
### Description

The floating point value with a binary precision is stored.

- Exponential range: 1E-130 ~ 1E+125
- Storage size: (number of digits in integer part + 1) / 2 + (number of digits in fractional part + 1) / 2 + 1 (exponent, sign)

It has a binary precision value unlike [NUMBER](#0528f4e214aa9174), [NUMERIC](#2051e8f8ae4daa81) types.

- Alias names: REAL = FLOAT(24), DOUBLE = FLOAT(53), DOUBLE PRECISION = FLOAT(53), FLOAT4 = FLOAT(24), FLOAT8 = FLOAT(53).

<a id="11932f5c508f2c71"></a>
### For More Information

Refer to the followings.

- [NUMBER](#0528f4e214aa9174)
- [NUMERIC](#2051e8f8ae4daa81)

<a id="6d2310477d861113"></a>
## INTERVAL

<a id="15f9cf74c98c7aa1"></a>
### Syntax

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

<a id="f2f25148968909c2"></a>
### Syntax Rules and Parameters

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

<a id="2ebe8e0b30307427"></a>
### Description

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

<a id="c677efa4aaf43772"></a>
| Field | Precision | Value range |
| --- | --- | --- |
| MONTH | 2 | 0 ~ 11 |
| HOUR | 2 | 0 ~ 23 |
| MINUTE | 2 | 0 ~ 59 |
| SECOND (interger part) | 2 | 0 ~ 59 |

<a id="a858efbe378fd852"></a>
### For More Information

Refer to [Interval Literals](11-sql-elements.md#b601eec9ab332ab5).

<a id="62ab51de7e978ede"></a>
## NATIVE_BIGINT

<a id="964eb99d2e12391b"></a>
### Syntax

```
NATIVE_BIGINT
```

<a id="709cbb3dacb403b0"></a>
### Description

Signed 8-byte integer is stored.

It is as same as long long data type of C language (8 bytes integer).

- Value range: -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807
- Storage size: 8 bytes

<a id="650f2a5883a8059d"></a>
## NATIVE_DOUBLE

<a id="e5fdd9862505e618"></a>
### Syntax

```
NATIVE_DOUBLE
```

<a id="c43a1c0a1f88d184"></a>
### Description

Double precision floating-point number (8 bytes) is stored.

It is as same as double data type of C language.

- Exponential range: 1E-307 ~ 1E+308
- Storage size: 8 bytes

<a id="6077bca8efaefd77"></a>
## NATIVE_INTEGER

<a id="d1dfb6eb538c5bed"></a>
### Syntax

```
NATIVE_INTEGER
```

<a id="0a66957815693ef1"></a>
### Description

Signed 4 byte integer is stored.

It is as same as integer data type of C language (4 bytes).

- Value range: -2,147,483,648 ~ +2,147,483,647
- Storage size: 4 bytes

<a id="a7040ee2777d995c"></a>
## NATIVE_REAL

<a id="542eb931395132b2"></a>
### Syntax

```
NATIVE_REAL
```

<a id="399df6dc623f475a"></a>
### Description

Single precision floating-point number (4 bytes) is stored.

It is as same as float data type of C language.

- Exponential range: 1E-37 ~ 1E+37
- Storage size: 4 bytes

<a id="b6bf9340bbfc4904"></a>
## NATIVE_SMALLINT

<a id="ce44d7abb04b3347"></a>
### Syntax

```
NATIVE_SMALLINT
```

<a id="ecf03b04cdd5c50e"></a>
### Description

Signed 2 byte integer is stored.

It is as same as short data type of C language.

- Value range: -32,768 ~ 32,767
- Storage size: 2 bytes

<a id="0528f4e214aa9174"></a>
## NUMBER

<a id="abc1ed0f21b66344"></a>
### Syntax

```
NUMBER  [ ( precision [ , scale ] ) ]
```

<a id="e051cb971677c6d8"></a>
### Syntax Rules and Parameters

- NUMBER: A floating point number without a precision and scale is stored.
    - The range of significant digits: 38
    - Exponential range: 1E-130 ~ 1E+125
    - It is as same as FLOAT (126).

- NUMBER(precision): The integer with significant digits of precision is stored.
    - Precision range: 1 ~ 38
    - The scale value: 0
    - It has a decimal precision value unlike [FLOAT](#92493efa6e610bbe) type.
    - It is as same as NUMBER(precision, 0), NUMERIC(precision, 0).

- NUMBER(precision, scale): A fixed point number with precision and scale is stored.
    - Precision range: 1 ~ 38
    - Scale range: -84 ~ 127
    - It has a decimal precision value unlike [FLOAT](#92493efa6e610bbe) type.
    - It is as same as NUMERIC (precision,scale).
    - Alias names: SMALLINT = NUMBER(5,0), INTEGER = NUMBER(10,0), BIGINT = NUMBER(19,0), INT2 = NUMBER(5,0), INT4 = NUMBER(10,0), INT8 = NUMBER(19,0)

<a id="ff7d3b564b6b8dc1"></a>
### Description

NUMBER type is similar to NUMERIC type, but if both the precision and scale are omitted, NUMBER type stores the floating point number whose precision and scale are not specified.

- NUMBER without precision, scale: Floating-point number
- NUMERIC without precision, scale: The fixed point number of NUMERIC(38, 0)
- Storage size: (number of digits in integer part + 1) / 2 + (number of digits in fractional part + 1) / 2 + 1 (exponent, sign)

<a id="46b4a55c024f76cb"></a>
### For More Information

Refer to the followings.

- [FLOAT](#92493efa6e610bbe)
- [NUMERIC](#2051e8f8ae4daa81)

<a id="2051e8f8ae4daa81"></a>
## NUMERIC

<a id="41a91de65a881523"></a>
### Syntax

```
NUMERIC  [ ( precision [ , scale ] ) ]
```

<a id="7abd0a6a07571f14"></a>
### Syntax Rules and Parameters

- precision: It is the decimal precision of significant digits.
    - precision range: 1 ~ 38
    - Default value: 38

- scale: It is the decimal point range.
    - scale range: -84 ~ 127
    - Default value: 0

<a id="ff771d7818d7dbb7"></a>
### Description

A fixed point number with precision and scale is stored.

If the precision and scale are omitted, it means as follows.

- NUMERIC = NUMERIC(38,0)
- NUMERIC(p) = NUMERIC(p,0)

NUMBER type is similar to NUMERIC type, but if both the precision and scale are omitted, NUMBER type stores the floating-point number whose precision and scale are not specified.

- NUMBER without precision, scale: Floating point number
- NUMERIC without precision, scale: Fixed point number of NUMERIC(38,0)
- Storage size: (number of digits in integer part + 1) / 2 + (number of digits in fractional part + 1) / 2 + 1 (exponent, sign)

<a id="1168ea492a1a2a10"></a>
### For More Information

Refer to the followings.

- [FLOAT](#92493efa6e610bbe)
- [NUMBER](#0528f4e214aa9174)

<a id="5640cb398d2830d1"></a>
## ROWID

<a id="d9aeec4272e8727e"></a>
### Syntax

```
ROWID
```

<a id="cf8d8eb697b7f293"></a>
### Description

A record identifier (ROWID) is stored.  

A record identifier (ROWID) is the identification information of each record in database.  

When querying the ROWID pseudo column, each record identifier (ROWID) is obtained. This ROWID pseudo column has the ROWID data type information.

ROWID type consists of the followings in a stand-alone system.  
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

<a id="f37a70db4f8afa46"></a>
### For More Information

Refer to the followings.

- [ROWID Pseudo Column](11-sql-elements.md#97d0dedf97e4117b)
- [ROWID-related Functions](11-sql-elements.md#1b2810e407fc31bd)

<a id="4c35506be1ac9ad6"></a>
## TIME

<a id="aa5aefea8c19cc66"></a>
### Syntax

```
TIME [ ( fractional_seconds_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
```

<a id="22475c69feea662f"></a>
### Syntax Rules and Parameters

- fractional_seconds_precision: It is the number of significant digits in fractional seconds.
    - fractional_seconds_precision range: 0 ~ 6
    - Default value: 6

- [ WITH TIME ZONE | WITHOUT TIME ZONE ]: It specifies whether to store TIME ZONE value.
    - WITH TIME ZONE: The time which includes time zone
    - WITHOUT TIME ZONE: The time which does not include time zone
    - Default value: WITHOUT TIME ZONE

<a id="df6a1a638d9f39e0"></a>
### Description

The time which includes HOUR, MINUTE and SECOND is stored.

- Storage size 
    - TIME WITHOUT TIME ZONE: 8 bytes
    - TIME WITH TIME ZONE: 12 bytes

<a id="aed4a737a769d4f5"></a>
### For More Information

Refer to the followings.

- [Time Literals](11-sql-elements.md#e57ca13b100ce39c)
- [Time with Time Zone Literals](11-sql-elements.md#09c29b15a3d38e83)
- [DATE](#1876eba8c76e5c08)
- [TIMESTAMP](#fa1328ca29a5e4f3)

<a id="fa1328ca29a5e4f3"></a>
## TIMESTAMP

<a id="c669577a9218f69b"></a>
### Syntax

```
TIMESTAMP [ ( fractional_seconds_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
```

<a id="d386727658dbb0b7"></a>
### Syntax Rules and Parameters

- fractional_seconds_precision: It is the number of significant digits in the fractional seconds.
    - fractional_seconds_precision range: 0 ~ 6
    - Default value: 6

- [ WITH TIME ZONE | WITHOUT TIME ZONE ]: It specifies whether to store TIME ZONE value.
    - WITH TIME ZONE: The time which includes time zone. 
    - WITHOUT TIME ZONE: The time which does not include time zone. 
    - Default value: WITHOUT TIME ZONE

<a id="6cb3ff2face7b2c0"></a>
### Description

The time which includes YEAR, MONTH, DATE, HOUR, MINUTE and SECOND is stored.

- Storage size 
    - TIMESTAMP WITHOUT TIME ZONE: 8 bytes
    - TIMESTAMP WITH TIME ZONE: 12 bytes

<a id="95e721a2555b2d62"></a>
### For More Information

Refer to the followings.

- [Timestamp Literals](11-sql-elements.md#963a5d389b1685a6)
- [Timestamp with Time Zone Literals](11-sql-elements.md#478c1178ac518475)
- [DATE](#1876eba8c76e5c08)
- [TIME](#4c35506be1ac9ad6)

---

[← 15. SQL Tuning](15-sql-tuning.md) · [Table of contents](../README.md) · [17. Built-in Function References →](17-built-in-function-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
