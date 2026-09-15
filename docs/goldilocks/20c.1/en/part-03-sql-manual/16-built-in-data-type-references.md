<a id="d0d05e646b222330"></a>

# 16. Built-in Data Type References

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/d0d05e646b222330)  
> Tag: `20c.1_30_tag`

[← 15. SQL Tuning](15-sql-tuning.md) · [Table of contents](../README.md) · [17. Built-in Function References →](17-built-in-function-references.md)

<a id="0623962c739a70d0"></a>
## Aliases of Built-in Data Types

- BIGINT
    - It is as same as NUMBER(19,0).
    - Refer to [NUMBER](#73cf1c9140545670).
- BINARY
    - Refer to [BINARY](#b80aad0452177f9b).
- BINARY VARYING
    - Refer to [BINARY VARYING](#57cbd68a64ca7b6a).
- BINARY LONG VARYING
    - Refer to [BINARY LONG VARYING](#4bd53518584625b0).
- BOOLEAN
    - Refer to [BOOLEAN](#752094d653f0cbec).
- CHAR
    - It is as same as CHARACTER.
    - Refer to [CHARACTER](#a1a5afd22ae72722).
- CHARACTER
    - Refer to [CHARACTER](#a1a5afd22ae72722).
- CHARACTER VARYING
    - Refer to [CHARACTER VARYING](#50aca3bb031ba30d).
- CHARACTER LONG VARYING
    - Refer to [CHARACTER LONG VARYING](#d16f1e010a72ec9c).
- DATE
    - Refer to [DATE](#1d706dc0d418b961).
- DEC
    - It is as same as NUMERIC.
    - Refer to [NUMERIC](#ce6a34fd3ac9eac3).
- DECIMAL
    - It is as same as NUMERIC.
    - Refer to [NUMERIC](#ce6a34fd3ac9eac3).
- DOUBLE
    - It is as same as FLOAT(53).
    - Refer to [FLOAT](#c8cff93830b9dec0).
- DOUBLE PRECISION
    - It is as same as FLOAT(53).
    - Refer to [FLOAT](#c8cff93830b9dec0).
- FLOAT
    - Refer to [FLOAT](#c8cff93830b9dec0).
- FLOAT4
    - It is as same as FLOAT(24).
    - Refer to [FLOAT](#c8cff93830b9dec0).
- FLOAT8
    - It is as same as FLOAT(53).
    - Refer to [FLOAT](#c8cff93830b9dec0).
- INT
    - It is as same as NUMBER(10,0).
    - Refer to [NUMBER](#73cf1c9140545670).
- INT2
    - It is as same as NUMBER(5,0).
    - Refer to [NUMBER](#73cf1c9140545670).
- INT4
    - It is as same as NUMBER(10,0).
    - Refer to [NUMBER](#73cf1c9140545670).
- INT8
    - It is as same as NUMBER(19,0).
    - Refer to [NUMBER](#73cf1c9140545670).
- INTEGER
    - It is as same as NUMBER(10,0).
    - Refer to [NUMBER](#73cf1c9140545670).
- INTERVAL
    - Refer to [INTERVAL](#4917c503756cb2b1).
- LONG BINARY VARYING
    - It is as same as BINARY LONG VARYING. 
    - Refer to [BINARY LONG VARYING](#4bd53518584625b0).
- LONG CHAR VARYING
    - It is as same as CHARACTER LONG VARYING. 
    - Refer to [CHARACTER LONG VARYING](#d16f1e010a72ec9c).
- LONG CHARACTER VARYING
    - It is as same as CHARACTER LONG VARYING. 
    - Refer to [CHARACTER LONG VARYING](#d16f1e010a72ec9c).
- LONG VARCHAR
    - It is as same as CHARACTER LONG VARYING.
    - Refer to [CHARACTER LONG VARYING](#d16f1e010a72ec9c).
- NATIVE_BIGINT
    - Refer to [NATIVE_BIGINT](#92ac319a7f187989).
- NATIVE_DOUBLE
    - Refer to [NATIVE_DOUBLE](#40587f5837b2f7d4).
- NATIVE_INTEGER
    - Refer to [NATIVE_INTEGER](#56cd3a3221bf2264).
- NATIVE_REAL
    - Refer to [NATIVE_REAL](#81b4385f27d1ea09).
- NATIVE_SMALLINT
    - Refer to [NATIVE_SMALLINT](#83122b210b62cffb).
- NUMBER
    - Refer to [NUMBER](#73cf1c9140545670).
- NUMERIC
    - Refer to [NUMERIC](#ce6a34fd3ac9eac3).
- ROWID
    - Refer to [ROWID](#1b1f212380d82e23).
- SMALLINT
    - It is as same as NUMBER(5,0). 
    - Refer to [NUMBER](#73cf1c9140545670).
- TIME
    - Refer to [TIME](#15179a3ddb3002db).
- TIMESTAMP
    - Refer to [TIMESTAMP](#2109a8936ce6d086).
- VARBINARY
    - It is as same as BINARY VARYING.
    - Refer to [BINARY VARYING](#57cbd68a64ca7b6a).
- VARCHAR
    - It is as same as CHARACTER VARYING. 
    - Refer to [CHARACTER VARYING](#50aca3bb031ba30d).
- VARCHAR2
    - It is as same as CHARACTER VARYING. 
    - Refer to [CHARACTER VARYING](#50aca3bb031ba30d).

<a id="b80aad0452177f9b"></a>
## BINARY

<a id="7626364b29f9b3e4"></a>
### Syntax

```
BINARY [ (length) ]
```

<a id="eb7e234d4e3716d6"></a>
### Syntax Rules and Parameters

- length: It is the binary string length.
    - Range: 1 ~ 2000
    - Default value: 1

<a id="16cbd8d1557427a8"></a>
### Description

A fixed-length binary string is stored.  
If the binary string length to be stored is shorter than the specified length,  X'00 ' is stored in the remaining part.  
• Storage size: Bytes of the length value

<a id="8f56e0e56063a895"></a>
### For More Information

Refer to the followings.

- [BINARY VARYING](#57cbd68a64ca7b6a)
- [BINARY LONG VARYING](#4bd53518584625b0)

<a id="57cbd68a64ca7b6a"></a>
## BINARY VARYING

<a id="62b0381dbd78f71a"></a>
### Syntax

```
BINARY VARYING (length)
```

<a id="03c20d0f403133c0"></a>
### Syntax Rules and Parameters

- length: It is the maximum length of binary string.
    - Range: 1 ~ 4000

<a id="91976247430bfd42"></a>
### Description

The variable-length binary string is stored.  

• Storage size: Bytes of the binary string to be stored  
• Alias names: VARBINARY

<a id="ed787c1af1e157c3"></a>
### For More Information

Refer to the followings.

- [BINARY](#b80aad0452177f9b)
- [BINARY LONG VARYING](#4bd53518584625b0)

<a id="4bd53518584625b0"></a>
## BINARY LONG VARYING

<a id="d18b70c14a5e7f57"></a>
### Syntax

```
BINARY LONG VARYING
```

<a id="d938c93c0935bfb0"></a>
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

<a id="301952e492d5c95a"></a>
### For More Information

Refer to the followings.

- [BINARY](#b80aad0452177f9b)
- [BINARY VARYING](#57cbd68a64ca7b6a)

<a id="752094d653f0cbec"></a>
## BOOLEAN

<a id="1ca79fcf2f33ed85"></a>
### Syntax

```
BOOLEAN
```

<a id="737132106f78dab9"></a>
### Description

TRUE or FALSE is stored.  
• Storage size: 1 byte.

<a id="a1a5afd22ae72722"></a>
## CHARACTER

<a id="4251a7784c98c16c"></a>
### Syntax

```
CHARACTER [ (length [ CHARACTERS | OCTETS | CHAR | BYTE ] ) ]
```

<a id="a049c90480c77593"></a>
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
    - If omitted, the default is the property value of [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#3c69a6a4ea2b681f) which is set when creating database.

<a id="28d422fc48dfb1ed"></a>
### Description

A fixed-length string is stored.  
If the length of the string to be stored is shorter than the specified length, white spaces are stored in the remaining part.

- Storage size: Bytes of the length value
- Alias name: CHAR

<a id="ac3cabc4b5883627"></a>
### For More Information

Refer to the followings.

- [CHARACTER VARYING](#50aca3bb031ba30d)
- [CHARACTER LONG VARYING](#d16f1e010a72ec9c)

<a id="50aca3bb031ba30d"></a>
## CHARACTER VARYING

<a id="ea922826bb820bef"></a>
### Syntax

```
CHARACTER VARYING ( length [ CHARACTERS | OCTETS | CHAR | BYTE ] )
```

<a id="2a1d969f3ac91b1d"></a>
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
    - If omitted, the default is the property value of [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#3c69a6a4ea2b681f) which is set when creating database.

<a id="62a91c886812ade2"></a>
### Description

The variable-length string is stored.  

• Storage size: Bytes of the string to be stored  
• Alias names: VARCHAR, VARCHAR2

<a id="ea0681f723ba86b1"></a>
### For More Information

Refer to the followings.

- [CHARACTER](#a1a5afd22ae72722)
- [CHARACTER LONG VARYING](#d16f1e010a72ec9c)

<a id="d16f1e010a72ec9c"></a>
## CHARACTER LONG VARYING

<a id="4e57e31cc5b1435f"></a>
### Syntax

```
CHARACTER LONG VARYING
```

<a id="476bff0824097dfc"></a>
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

<a id="10db442d8af28b4a"></a>
### For More Information

Refer to the followings.

- [CHARACTER](#a1a5afd22ae72722)
- [CHARACTER VARYING](#50aca3bb031ba30d)

<a id="1d706dc0d418b961"></a>
## DATE

<a id="ae19af761d7f7eaa"></a>
### Syntax

```
DATE
```

<a id="ade938414ba5d095"></a>
### Description

It is the date type including YEAR, MONTH, DAY, HOUR, MINUTE and SECOND (excluding fractional seconds).  
• Value range: Date value between '4714-11-24 BC' and '9999-12-31 AD'   
• Storage size: 8 bytes

<a id="cc1c41b9f90bfe45"></a>
### For More Information

Refer to the followings.

- [Date Literals](11-sql-elements.md#98a69fdd4cbc913c)
- [TIME](#15179a3ddb3002db)
- [TIMESTAMP](#2109a8936ce6d086)

<a id="c8cff93830b9dec0"></a>
## FLOAT

<a id="7cffd5d69c999432"></a>
### Syntax

```
FLOAT[ ( precision ) ]
```

<a id="c8508757068a3e7f"></a>
### Syntax Rules and Parameters

- precision: It is the binary precision of significant digits.
    - Precision range: 1 ~ 126
    - Default value: 126

<a id="936649224341a143"></a>
### Description

The floating point value with a binary precision is stored.

- Exponential range: 1E-130 ~ 1E+125
- Storage size: (number of digits in integer part + 1) / 2 + (number of digits in fractional part + 1) / 2 + 1 (exponent, sign)

It has a binary precision value unlike [NUMBER](#73cf1c9140545670), [NUMERIC](#ce6a34fd3ac9eac3) types.

- Alias names: REAL = FLOAT(24), DOUBLE = FLOAT(53), DOUBLE PRECISION = FLOAT(53), FLOAT4 = FLOAT(24), FLOAT8 = FLOAT(53).

<a id="f21d762149020de1"></a>
### For More Information

Refer to the followings.

- [NUMBER](#73cf1c9140545670)
- [NUMERIC](#ce6a34fd3ac9eac3)

<a id="4917c503756cb2b1"></a>
## INTERVAL

<a id="3b8f13d3d1893981"></a>
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

<a id="72691fa6d80de091"></a>
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

<a id="cc829dc3f4b41e33"></a>
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

<a id="d4806829e31af378"></a>
| Field | Precision | Value range |
| --- | --- | --- |
| MONTH | 2 | 0 ~ 11 |
| HOUR | 2 | 0 ~ 23 |
| MINUTE | 2 | 0 ~ 59 |
| SECOND (interger part) | 2 | 0 ~ 59 |

<a id="4a107e60b5ea0175"></a>
### For More Information

Refer to [Interval Literals](11-sql-elements.md#0c2b9a555deb3fcc).

<a id="92ac319a7f187989"></a>
## NATIVE_BIGINT

<a id="425c23dbcd27dd4e"></a>
### Syntax

```
NATIVE_BIGINT
```

<a id="e20daf4691cf8a3c"></a>
### Description

Signed 8-byte integer is stored.

It is as same as long long data type of C language (8 bytes integer).

- Value range: -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807
- Storage size: 8 bytes

<a id="40587f5837b2f7d4"></a>
## NATIVE_DOUBLE

<a id="33d1626cd3da2b2c"></a>
### Syntax

```
NATIVE_DOUBLE
```

<a id="7173b4d668f1b3d7"></a>
### Description

Double precision floating-point number (8 bytes) is stored.

It is as same as double data type of C language.

- Exponential range: 1E-307 ~ 1E+308
- Storage size: 8 bytes

<a id="56cd3a3221bf2264"></a>
## NATIVE_INTEGER

<a id="cd8b6ccd98e6b6f5"></a>
### Syntax

```
NATIVE_INTEGER
```

<a id="909e2b4d0fb61971"></a>
### Description

Signed 4 byte integer is stored.

It is as same as integer data type of C language (4 bytes).

- Value range: -2,147,483,648 ~ +2,147,483,647
- Storage size: 4 bytes

<a id="81b4385f27d1ea09"></a>
## NATIVE_REAL

<a id="a4e1f061caf1fc28"></a>
### Syntax

```
NATIVE_REAL
```

<a id="d17c4d8826c85722"></a>
### Description

Single precision floating-point number (4 bytes) is stored.

It is as same as float data type of C language.

- Exponential range: 1E-37 ~ 1E+37
- Storage size: 4 bytes

<a id="83122b210b62cffb"></a>
## NATIVE_SMALLINT

<a id="7089bdf16973743d"></a>
### Syntax

```
NATIVE_SMALLINT
```

<a id="cd5e25947ac7fe2f"></a>
### Description

Signed 2 byte integer is stored.

It is as same as short data type of C language.

- Value range: -32,768 ~ 32,767
- Storage size: 2 bytes

<a id="73cf1c9140545670"></a>
## NUMBER

<a id="de77f3e3dac04261"></a>
### Syntax

```
NUMBER  [ ( precision [ , scale ] ) ]
```

<a id="6fe1ba3be66da87a"></a>
### Syntax Rules and Parameters

- NUMBER: A floating point number without a precision and scale is stored.
    - The range of significant digits: 38
    - Exponential range: 1E-130 ~ 1E+125
    - It is as same as FLOAT (126).

- NUMBER(precision): The integer with significant digits of precision is stored.
    - Precision range: 1 ~ 38
    - The scale value: 0
    - It has a decimal precision value unlike [FLOAT](#c8cff93830b9dec0) type.
    - It is as same as NUMBER(precision, 0), NUMERIC(precision, 0).

- NUMBER(precision, scale): A fixed point number with precision and scale is stored.
    - Precision range: 1 ~ 38
    - Scale range: -84 ~ 127
    - It has a decimal precision value unlike [FLOAT](#c8cff93830b9dec0) type.
    - It is as same as NUMERIC (precision,scale).
    - Alias names: SMALLINT = NUMBER(5,0), INTEGER = NUMBER(10,0), BIGINT = NUMBER(19,0), INT2 = NUMBER(5,0), INT4 = NUMBER(10,0), INT8 = NUMBER(19,0)

<a id="0682093ed69c72bb"></a>
### Description

NUMBER type is similar to NUMERIC type, but if both the precision and scale are omitted, NUMBER type stores the floating point number whose precision and scale are not specified.

- NUMBER without precision, scale: Floating-point number
- NUMERIC without precision, scale: The fixed point number of NUMERIC(38, 0)
- Storage size: (number of digits in integer part + 1) / 2 + (number of digits in fractional part + 1) / 2 + 1 (exponent, sign)

<a id="ca1896e2b33476ac"></a>
### For More Information

Refer to the followings.

- [FLOAT](#c8cff93830b9dec0)
- [NUMERIC](#ce6a34fd3ac9eac3)

<a id="ce6a34fd3ac9eac3"></a>
## NUMERIC

<a id="cb5d7d3121882bcc"></a>
### Syntax

```
NUMERIC  [ ( precision [ , scale ] ) ]
```

<a id="8124674cea6b9416"></a>
### Syntax Rules and Parameters

- precision: It is the decimal precision of significant digits.
    - precision range: 1 ~ 38
    - Default value: 38

- scale: It is the decimal point range.
    - scale range: -84 ~ 127
    - Default value: 0

<a id="e753c90f4e40a5d5"></a>
### Description

A fixed point number with precision and scale is stored.

If the precision and scale are omitted, it means as follows.

- NUMERIC = NUMERIC(38,0)
- NUMERIC(p) = NUMERIC(p,0)

NUMBER type is similar to NUMERIC type, but if both the precision and scale are omitted, NUMBER type stores the floating-point number whose precision and scale is not specified.

- NUMBER without precision, scale: Floating point number
- NUMERIC without precision, scale: Fixed point number of NUMERIC(38,0)
- Storage size: (number of digits in integer part + 1) / 2 + (number of digits in fractional part + 1) / 2 + 1 (exponent, sign)

<a id="8f8f0eeab3f6b8ee"></a>
### For More Information

Refer to the followings.

- [FLOAT](#c8cff93830b9dec0)
- [NUMBER](#73cf1c9140545670)

<a id="1b1f212380d82e23"></a>
## ROWID

<a id="e49e26a392bedbeb"></a>
### Syntax

```
ROWID
```

<a id="c5efcd58120de79e"></a>
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

<a id="a522deb8f6f0e9fe"></a>
### For More Information

Refer to the followings.

- [ROWID Pseudo Column](11-sql-elements.md#e00b57105e5778da)
- [ROWID-related Functions](11-sql-elements.md#22c04b83b6443bee)

<a id="15179a3ddb3002db"></a>
## TIME

<a id="de8f6af18f66e073"></a>
### Syntax

```
TIME [ ( fractional_seconds_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
```

<a id="6f164045486f0fe6"></a>
### Syntax Rules and Parameters

- fractional_seconds_precision: It is the number of significant digits in fractional seconds.
    - fractional_seconds_precision range: 0 ~ 6
    - Default value: 6

- [ WITH TIME ZONE | WITHOUT TIME ZONE ]: It specifies whether to store TIME ZONE value.
    - WITH TIME ZONE: The time which includes time zone
    - WITHOUT TIME ZONE: The time which does not include time zone
    - Default value: WITHOUT TIME ZONE

<a id="94fef34b5da0c232"></a>
### Description

The time which includes HOUR, MINUTE and SECOND is stored.

- Storage size 
    - TIME WITHOUT TIME ZONE: 8 bytes
    - TIME WITH TIME ZONE: 12 bytes

<a id="9e6873f3bcfb887c"></a>
### For More Information

Refer to the followings.

- [Time Literals](11-sql-elements.md#8796f143774bb1dd)
- [Time with Time Zone Literals](11-sql-elements.md#48c6bbd22ffa117a)
- [DATE](#1d706dc0d418b961)
- [TIMESTAMP](#2109a8936ce6d086)

<a id="2109a8936ce6d086"></a>
## TIMESTAMP

<a id="723103fe87d08a76"></a>
### Syntax

```
TIMESTAMP [ ( fractional_seconds_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
```

<a id="ac9cc8e10a96dbeb"></a>
### Syntax Rules and Parameters

- fractional_seconds_precision: It is the number of significant digits in the fractional seconds.
    - fractional_seconds_precision range: 0 ~ 6 
    - Default value: 6

- [ WITH TIME ZONE | WITHOUT TIME ZONE ]: It specifies whether to store TIME ZONE value.
    - WITH TIME ZONE: The time which includes time zone. 
    - WITHOUT TIME ZONE: The time which does not include time zone. 
    - Default value: WITHOUT TIME ZONE

<a id="843866de5c8020f0"></a>
### Description

The time which includes YEAR, MONTH, DATE, HOUR, MINUTE and SECOND is stored.

- Storage size 
    - TIMESTAMP WITHOUT TIME ZONE: 8 bytes
    - TIMESTAMP WITH TIME ZONE: 12 bytes

<a id="20da01569d9664dd"></a>
### For More Information

Refer to the followings.

- [Timestamp Literals](11-sql-elements.md#377822d9253b54c0)
- [Timestamp with Time Zone Literals](11-sql-elements.md#32e899dbeb0264ff)
- [DATE](#1d706dc0d418b961)
- [TIME](#15179a3ddb3002db)

---

[← 15. SQL Tuning](15-sql-tuning.md) · [Table of contents](../README.md) · [17. Built-in Function References →](17-built-in-function-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
