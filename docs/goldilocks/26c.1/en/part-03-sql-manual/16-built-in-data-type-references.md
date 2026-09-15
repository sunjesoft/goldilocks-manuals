<a id="1ef27eb5cccbe6f9"></a>

# 16. Built-in Data Type References

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/1ef27eb5cccbe6f9)  
> Tag: `26c.1_0_tag`

[← 15. SQL Tuning](15-sql-tuning.md) · [Table of contents](../README.md) · [17. Built-in Function References →](17-built-in-function-references.md)

<a id="513777896d946002"></a>
## Aliases of Built-in Data Types

- BIGINT
    - It is the same as NUMBER(19,0).
    - Refer to [NUMBER](#2f8065df8574cbef).
- BINARY
    - Refer to [BINARY](#fbf3d5ebb7224a2c).
- BINARY VARYING
    - Refer to [BINARY VARYING](#0b0914f37f5ffeb8).
- BINARY LONG VARYING
    - Refer to [BINARY LONG VARYING](#ae884d0ba0d97a74).
- BOOLEAN
    - Refer to [BOOLEAN](#ef47d9ed3ac8c254).
- CHAR
    - It is the same as CHARACTER.
    - Refer to [CHARACTER](#3d552befa621e8be).
- CHARACTER
    - Refer to [CHARACTER](#3d552befa621e8be).
- CHARACTER VARYING
    - Refer to [CHARACTER VARYING](#03dae4745525807e).
- CHARACTER LONG VARYING
    - Refer to [CHARACTER LONG VARYING](#1cc378ee86bc0d15).
- DATE
    - Refer to [DATE](#e1a7517d0f63a48f).
- DEC
    - It is the same as NUMERIC.
    - Refer to [NUMERIC](#0c1a790db2a97db2).
- DECIMAL
    - It is the same as NUMERIC.
    - Refer to [NUMERIC](#0c1a790db2a97db2).
- DOUBLE
    - It is the same as FLOAT(53).
    - Refer to [FLOAT](#0ef612f8546e2023).
- DOUBLE PRECISION
    - It is the same as FLOAT(53).
    - Refer to [FLOAT](#0ef612f8546e2023).
- FLOAT
    - Refer to [FLOAT](#0ef612f8546e2023).
- FLOAT4
    - It is the same as FLOAT(24).
    - Refer to [FLOAT](#0ef612f8546e2023).
- FLOAT8
    - It is the same as FLOAT(53).
    - Refer to [FLOAT](#0ef612f8546e2023).
- INT
    - It is the same as NUMBER(10,0).
    - Refer to [NUMBER](#2f8065df8574cbef).
- INT2
    - It is the same as NUMBER(5,0).
    - Refer to [NUMBER](#2f8065df8574cbef).
- INT4
    - It is the same as NUMBER(10,0).
    - Refer to [NUMBER](#2f8065df8574cbef).
- INT8
    - It is the same as NUMBER(19,0).
    - Refer to [NUMBER](#2f8065df8574cbef).
- INTEGER
    - It is the same as NUMBER(10,0).
    - Refer to [NUMBER](#2f8065df8574cbef).
- INTERVAL
    - Refer to [INTERVAL](#3719f3256f650b0f).
- LONG BINARY VARYING
    - It is the same as BINARY LONG VARYING. 
    - Refer to [BINARY LONG VARYING](#ae884d0ba0d97a74).
- LONG CHAR VARYING
    - It is the same as CHARACTER LONG VARYING. 
    - Refer to [CHARACTER LONG VARYING](#1cc378ee86bc0d15).
- LONG CHARACTER VARYING
    - It is the same as CHARACTER LONG VARYING. 
    - Refer to [CHARACTER LONG VARYING](#1cc378ee86bc0d15).
- LONG VARCHAR
    - It is the same as CHARACTER LONG VARYING.
    - Refer to [CHARACTER LONG VARYING](#1cc378ee86bc0d15).
- NATIVE_BIGINT
    - Refer to [NATIVE_BIGINT](#a1fa84b35b583bfd).
- NATIVE_DOUBLE
    - Refer to [NATIVE_DOUBLE](#b8657b67d632227e).
- NATIVE_INTEGER
    - Refer to [NATIVE_INTEGER](#b54b66a89b51d7b5).
- NATIVE_REAL
    - Refer to [NATIVE_REAL](#e668050ffd2fe5d3).
- NATIVE_SMALLINT
    - Refer to [NATIVE_SMALLINT](#e9fdbaf1b1795369).
- NUMBER
    - Refer to [NUMBER](#2f8065df8574cbef).
- NUMERIC
    - Refer to [NUMERIC](#0c1a790db2a97db2).
- ROWID
    - Refer to [ROWID](#72823db80276ccca).
- SMALLINT
    - It is the same as NUMBER(5,0). 
    - Refer to [NUMBER](#2f8065df8574cbef).
- TIME
    - Refer to [TIME](#726749f4da2c8c97).
- TIMESTAMP
    - Refer to [TIMESTAMP](#3f728dfee44599c8).
- VARBINARY
    - It is the same as BINARY VARYING.
    - Refer to [BINARY VARYING](#0b0914f37f5ffeb8).
- VARCHAR
    - It is the same as CHARACTER VARYING. 
    - Refer to [CHARACTER VARYING](#03dae4745525807e).
- VARCHAR2
    - It is the same as CHARACTER VARYING. 
    - Refer to [CHARACTER VARYING](#03dae4745525807e).

<a id="fbf3d5ebb7224a2c"></a>
## BINARY

<a id="f5c1927ab7e35025"></a>
### Syntax

```
BINARY [ (length) ]
```

<a id="492054aa6376fbc3"></a>
### Syntax Rules and Parameters

- length: It refers to the length of the binary string.
    - Range: 1 ~ 2000
    - Default value: 1

<a id="75646261c03d8737"></a>
### Description

A fixed-length binary string is stored.  
If the binary string length to be stored is shorter than the specified length,  X'00 ' is stored in the remaining part.  
• Storage size: The number of bytes corresponding to the length value

<a id="1709946d9823c610"></a>
### For More Information

Refer to the following.

- [BINARY VARYING](#0b0914f37f5ffeb8)
- [BINARY LONG VARYING](#ae884d0ba0d97a74)

<a id="0b0914f37f5ffeb8"></a>
## BINARY VARYING

<a id="a69cda9a80d2035c"></a>
### Syntax

```
BINARY VARYING (length)
```

<a id="1747252dfa875f6a"></a>
### Syntax Rules and Parameters

- length: It refers to the maximum length of binary string.
    - Range: 1 ~ 4000

<a id="0043d6d84086bbdf"></a>
### Description

A variable-length binary string is stored.  

• Storage size: The number of bytes of the binary string to be stored  
• Alias names: VARBINARY

<a id="0d9abbe6f395b833"></a>
### For More Information

Refer to the following.

- [BINARY](#fbf3d5ebb7224a2c)
- [BINARY LONG VARYING](#ae884d0ba0d97a74)

<a id="ae884d0ba0d97a74"></a>
## BINARY LONG VARYING

<a id="8786c29e1dfe6a03"></a>
### Syntax

```
BINARY LONG VARYING
```

<a id="5b0a79442722862a"></a>
### Description

The value of the long variable binary string is stored.  

• Maximum storage size: 100 megabytes  
• Storage size: The number of bytes of the binary string to be stored  
• Alias names: LONG BINARY VARYING, LONG VARBINARY

It cannot be used as a column of the key, so there are the following limitations:  

• It can not be used as a key column of an index.  
• It can not be used in the expression of the ORDER BY clause.   
• It can not be used in the expression of the GROUP BY clause.  
• It can not be used in the expression of the DISTINCT clause.  
• It can not be used in the expression of the UNION, INTERSECT, or EXCEPT clauses.

<a id="9402c26aaac31d5e"></a>
### For More Information

Refer to the following.

- [BINARY](#fbf3d5ebb7224a2c)
- [BINARY VARYING](#0b0914f37f5ffeb8)

<a id="ef47d9ed3ac8c254"></a>
## BOOLEAN

<a id="d2d45f49d13af50f"></a>
### Syntax

```
BOOLEAN
```

<a id="0a1ac03fadd41c75"></a>
### Description

TRUE or FALSE is stored.  
• Storage size: 1 byte.

<a id="3d552befa621e8be"></a>
## CHARACTER

<a id="7e2e626e4d9510e9"></a>
### Syntax

```
CHARACTER [ (length [ CHARACTERS | OCTETS | CHAR | BYTE ] ) ]
```

<a id="54fdfc929f60d9c8"></a>
### Syntax Rules and Parameters

- length: It refers to the string length.
    - Range: 1 ~ 2000
    - Default value: 1

- [ CHARACTERS | OCTETS | CHAR | BYTE ]: It is unit of length.
    - CHARACTERS
        - The number of characters
        - CHAR is the same as CHARACTERS.
    - OCTETS
        - The number of bytes
        - BYTE is the same as OCTETS.
    - If omitted, the default is the property value of [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#b06a0825ab72d342) set when the database is created.

<a id="3d9f1c4561651997"></a>
### Description

A fixed-length string is stored.  
If the length of the string to be stored is shorter than the specified length, whitespace characters are stored in the remaining space.

- Storage size: The number of bytes corresponding to the length value
- Alias name: CHAR

<a id="e69a77b9622c6918"></a>
### For More Information

Refer to the following.

- [CHARACTER VARYING](#03dae4745525807e)
- [CHARACTER LONG VARYING](#1cc378ee86bc0d15)

<a id="03dae4745525807e"></a>
## CHARACTER VARYING

<a id="e6980d061451251c"></a>
### Syntax

```
CHARACTER VARYING ( length [ CHARACTERS | OCTETS | CHAR | BYTE ] )
```

<a id="4695011247b49d72"></a>
### Syntax Rules and Parameters

- length: It refers to the string length.
    - Range: 1 ~ 4000

- [ CHARACTERS | OCTETS | CHAR | BYTE ]: It is unit of length.
    - CHARACTERS
        - The number of characters
        - CHAR is the same as CHARACTERS.
    - OCTETS
        - The number of bytes
        - BYTE is the same as OCTETS.
    - If omitted, the default is the property value of [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#b06a0825ab72d342) set when the database is created.

<a id="1c0de1f46bd8065f"></a>
### Description

The variable-length string is stored.  

• Storage size: The number of bytes of the string to be stored  
• Alias names: VARCHAR, VARCHAR2

<a id="6888db57cf07bc6d"></a>
### For More Information

Refer to the following.

- [CHARACTER](#3d552befa621e8be)
- [CHARACTER LONG VARYING](#1cc378ee86bc0d15)

<a id="1cc378ee86bc0d15"></a>
## CHARACTER LONG VARYING

<a id="99fa1174b9aa1f16"></a>
### Syntax

```
CHARACTER LONG VARYING
```

<a id="53c820446eea215e"></a>
### Description

The value of the long variable-length string is stored.  

• Maximum storage size: 100 megabytes  
• Storage size: The number of bytes of the string to be stored   
• Alias names: LONG CHARACTER VARYING, LONG CHAR VARYING, LONG VARCHAR

It can not be used as a column of the key, so there are the following limitations:  

• It can not be used as a key column of an index.  
• It can not be used in the expression of the ORDER BY clause.   
• It can not be used in the expression of the GROUP BY clause.  
• It can not be used in the expression of the DISTINCT clause.  
• It can not be used in the expression of the UNION, INTERSECT, or EXCEPT clauses.

<a id="b6fa86212446a2a5"></a>
### For More Information

Refer to the following.

- [CHARACTER](#3d552befa621e8be)
- [CHARACTER VARYING](#03dae4745525807e)

<a id="e1a7517d0f63a48f"></a>
## DATE

<a id="fe95766d2a8551bf"></a>
### Syntax

```
DATE
```

<a id="0f040a7c8d09d4e2"></a>
### Description

It is a date type that includes YEAR, MONTH, DAY, HOUR, MINUTE, and SECOND (excluding fractional seconds).  

• Value range: Date values between '4714-11-24 BC' and '9999-12-31 AD'   
• Storage size: 8 bytes

<a id="491e903b77ff8292"></a>
### For More Information

Refer to the following.

- [Date Literals](11-sql-elements.md#a2f402a0fdce6c45)
- [TIME](#726749f4da2c8c97)
- [TIMESTAMP](#3f728dfee44599c8)

<a id="0ef612f8546e2023"></a>
## FLOAT

<a id="d5d552b80eb9e92a"></a>
### Syntax

```
FLOAT[ ( precision ) ]
```

<a id="dd604adfd5d255c2"></a>
### Syntax Rules and Parameters

- precision: It refers to the binary precision of significant digits.
    - Precision range: 1 ~ 126
    - Default value: 126

<a id="35387af6ecb8279c"></a>
### Description

A floating-point value with binary precision is stored.

- Exponential range: 1E-130 ~ 1E+125
- Storage size: (number of digits in the integer part + 1) / 2 + (number of digits in the fractional part + 1) / 2 + 1 (for exponent and sign)

It has a binary precision value, unlike the [NUMBER](#2f8065df8574cbef) and  [NUMERIC](#0c1a790db2a97db2) types.

- Alias names: REAL = FLOAT(24), DOUBLE = FLOAT(53), DOUBLE PRECISION = FLOAT(53), FLOAT4 = FLOAT(24), FLOAT8 = FLOAT(53).

<a id="cce6502ea26819d8"></a>
### For More Information

Refer to the following.

- [NUMBER](#2f8065df8574cbef)
- [NUMERIC](#0c1a790db2a97db2)

<a id="3719f3256f650b0f"></a>
## INTERVAL

<a id="a7bf009f8966a760"></a>
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

<a id="eb3de4a278f3fcbb"></a>
### Syntax Rules and Parameters

- INTERVAL YEAR [ ( leading_precision ) ]: A period of YEAR is stored.
    - leading_precision 
        - The number of digits for YEAR
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL MONTH [ ( leading_precision ) ]: A period of MONTH is stored.
    - leading_precision 
        - The number of digits for MONTH
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL YEAR [ ( leading_precision ) ] TO MONTH: A period of YEAR and MONTH is stored.
    - leading_precision
        - The number of digits for YEAR
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL DAY [ ( leading_precision ) ]: A period of DAY is stored.
    - leading_precision 
        - The number of digits for DAY
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL HOUR [ ( leading_precision ) ]: A period of HOUR is stored.
    - leading_precision 
        - The number of digits for HOUR
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL MINUTE [ ( leading_precision ) ]: A period of MINUTE is stored.
    - leading_precision 
        - The number of digits for MINUTE
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL SECOND [ ( leading_precision [ , fractional_seconds_precision ] ) ]: A period of SECOND is stored.
    - leading_precision 
        - The number of digits for SECOND
        - Value range: 2 ~ 6
        - Default value: 2
    - fractional_seconds_precision
        - The number of digits for fractional seconds
        - Value range: 0 ~ 6
        - Default value: 6

- INTERVAL DAY [ ( leading_precision ) ] TO HOUR: A period of DAY and HOUR is stored.
    - leading_precision 
        - The number of digits for DAY
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL DAY [ ( leading_precision ) ] TO MINUTE: A period of DAY, HOUR, and MINUTE is stored.
    - leading_precision 
        - The number of digits for DAY
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL DAY [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]: A period of DAY, HOUR, MINUTE, and SECOND is stored.
    - leading_precision 
        - The number of digits for DAY
        - Value range: 2 ~ 6
        - Default value: 2
    - fractional_seconds_precision
        - The number of digits for fractional seconds
        - Value range: 0 ~ 6
        - Default value: 6

- INTERVAL HOUR [ ( leading_precision ) ] TO MINUTE: A period of HOUR and MINUTE is stored.
    - leading_precision 
        - The number of digits for HOUR
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL HOUR [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]: A period of HOUR, MINUTE and SECOND is stored.
    - leading_precision 
        - The number of digits for HOUR
        - Value range: 2 ~ 6
        - Default value: 2
    - fractional_seconds_precision
        - The number of digits for fractional seconds
        - Value range: 0 ~ 6
        - Default value: 6

- INTERVAL MINUTE [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]: A period of MINUTE and SECOND is stored.
    - leading_precision 
        - The number of digits for MINUTE 
        - Value range: 2 ~ 6
        - Default value: 2
    - fractional_seconds_precision
        - The number of digits for fractional seconds
        - Value range: 0 ~ 6
        - Default value: 6

<a id="3a60a4c484474f56"></a>
### Description

INTERVAL types can be classified into two families—YEAR TO MONTH and DAY TO SECOND—based on the range of value representation, as follows.

- YEAR TO MONTH family type: The storage size is 8 bytes.
    - INTERVAL YEAR
    - INTERVAL MONTH
    - INTERVAL YEAR TO MONTH

- DAY TO SECOND family type: The storage size is 16 bytes.
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

If a number larger than the specified number of digits is entered in a field where leading_precision is specified, an error is returned.  
If a number larger than the specified number of digits is entered in a field where fractional_seconds_precision is specified, it is rounded off.

**In the **INTERVAL * TO *** type, the precision and value range of the fields after the second field.**

<a id="5cb5c423faf9a449"></a>
| Field | Precision | Value range |
| --- | --- | --- |
| MONTH | 2 | 0 ~ 11 |
| HOUR | 2 | 0 ~ 23 |
| MINUTE | 2 | 0 ~ 59 |
| SECOND (integer part) | 2 | 0 ~ 59 |

<a id="b363b115b3231f17"></a>
### For More Information

Refer to [Interval Literals](11-sql-elements.md#daf1003f657050c1).

<a id="a1fa84b35b583bfd"></a>
## NATIVE_BIGINT

<a id="a3dd7757aafab1c1"></a>
### Syntax

```
NATIVE_BIGINT
```

<a id="94c67aff1c65fbff"></a>
### Description

A signed 8-byte integer is stored.

It is the same as the long long data type in C language (8 byte integer).

- Value range: -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807
- Storage size: 8 bytes

<a id="b8657b67d632227e"></a>
## NATIVE_DOUBLE

<a id="6b7770d474d0ff27"></a>
### Syntax

```
NATIVE_DOUBLE
```

<a id="4a9c006b4758d1e2"></a>
### Description

A double-precision floating-point number (8 bytes) is stored.

It is the same as the double data type in C language.

- Exponential range: 1E-307 ~ 1E+308
- Storage size: 8 bytes

<a id="b54b66a89b51d7b5"></a>
## NATIVE_INTEGER

<a id="d8b0dfd7c9e02fc0"></a>
### Syntax

```
NATIVE_INTEGER
```

<a id="b237dfb3c3cefcc3"></a>
### Description

A signed 4-byte integer is stored.

It is the same as the integer data type in C language (4 bytes).

- Value range: -2,147,483,648 ~ +2,147,483,647
- Storage size: 4 bytes

<a id="e668050ffd2fe5d3"></a>
## NATIVE_REAL

<a id="0262478b75d67fa0"></a>
### Syntax

```
NATIVE_REAL
```

<a id="0b30aeb4e6d85fd8"></a>
### Description

A single-precision floating-point number (4 bytes) is stored.

It is the same as the float data type in C language.

- Exponential range: 1E-37 ~ 1E+37
- Storage size: 4 bytes

<a id="e9fdbaf1b1795369"></a>
## NATIVE_SMALLINT

<a id="d28debdd5a35d548"></a>
### Syntax

```
NATIVE_SMALLINT
```

<a id="15cdf29ea33c3cbb"></a>
### Description

A signed 2-byte integer is stored.

It is the same as the short data type in C language.

- Value range: -32,768 ~ 32,767
- Storage size: 2 bytes

<a id="2f8065df8574cbef"></a>
## NUMBER

<a id="708828c6cdffcdf4"></a>
### Syntax

```
NUMBER  [ ( precision [ , scale ] ) ]
```

<a id="aaf9981bc12dc127"></a>
### Syntax Rules and Parameters

- NUMBER: A floating-point number is stored without precision or scale.
    - Range of significant digits: 38
    - Exponential range: 1E-130 ~ 1E+125
    - It is equivalent to FLOAT (126).

- NUMBER(precision): An integer with the specified number of significant digits (precision) is stored.
    - Precision range: 1 ~ 38
    - Scale value: 0
    - Unlike the FLOAT type, it has decimal precision.
    - It is equivalent to NUMBER(precision, 0) and NUMERIC(precision, 0).

- NUMBER(precision, scale): A fixed-point number with the specified precision and scale is stored.
    - Precision range: 1 ~ 38
    - Scale range: -84 ~ 127
    - Unlike the FLOAT type, it has decimal precision.
    - It is equivalent to NUMERIC (precision,scale).
    - Alias names: SMALLINT = NUMBER(5,0), INTEGER = NUMBER(10,0), BIGINT = NUMBER(19,0), INT2 = NUMBER(5,0), INT4 = NUMBER(10,0), INT8 = NUMBER(19,0)

<a id="d226234fe7882eca"></a>
### Description

The NUMBER type is similar to the NUMERIC type, but if both precision and scale are omitted, the NUMBER type stores a floating-point number without specified precision and scale.

- NUMBER without precision, scale: A floating-point number
- NUMERIC without precision, scale: A fixed-point number of NUMERIC(38, 0)
- Storage size: (number of digits in the integer part + 1) / 2 + (number of digits in the fractional part + 1) / 2 + 1 (exponent, sign)

<a id="c81aec7a064ade80"></a>
### For More Information

Refer to the following.

- [FLOAT](#0ef612f8546e2023)
- [NUMERIC](#0c1a790db2a97db2)

<a id="0c1a790db2a97db2"></a>
## NUMERIC

<a id="7c197ad4e0f00031"></a>
### Syntax

```
NUMERIC  [ ( precision [ , scale ] ) ]
```

<a id="344a37bf762b824b"></a>
### Syntax Rules and Parameters

- precision: It refers to the decimal precision of significant digits.
    - precision range: 1 ~ 38
    - Default value: 38

- scale: It refers to the range of decimal precision.
    - scale range: -84 ~ 127
    - Default value: 0

<a id="1d4c64ddee5a3122"></a>
### Description

A fixed-point number with the specified precision and scale is stored.

If the precision and scale are omitted, it is interpreted as follows.

- NUMERIC = NUMERIC(38,0)
- NUMERIC(p) = NUMERIC(p,0)

The NUMBER type is similar to the NUMERIC type, but if both precision and scale are omitted, the NUMBER type stores a floating-point number without specified precision and scale.

- NUMBER without precision, scale: A floating-point number
- NUMERIC without precision, scale: A fixed-point number of NUMERIC(38,0)
- Storage size: (number of digits in the integer part + 1) / 2 + (number of digits in the fractional part + 1) / 2 + 1 (exponent, sign)

<a id="a742bcf2557faf25"></a>
### For More Information

Refer to the following.

- [FLOAT](#0ef612f8546e2023)
- [NUMBER](#2f8065df8574cbef)

<a id="72823db80276ccca"></a>
## ROWID

<a id="64cc46b80adc1c7f"></a>
### Syntax

```
ROWID
```

<a id="def458d77408e83f"></a>
### Description

The ROWID type stores the record identifier (ROWID).  

A record identifier (ROWID) is the unique identification information for each record in the database.  

When querying the ROWID pseudo column, the corresponding record identifier (ROWID) value for each record can be obtained. This ROWID pseudo column has the ROWID data type.

The components of the ROWID type in a standalone system are as follows:  
• OBJECT_ID   
• TABLESPACE_ID   
• PAGE_ID   
• OFFSET within PAGE

The components of the ROWID type in a cluster system are as follows:  
• GRID_BLOCK_SEQUENCE  
• GRID_BLOCK_ID  
• MEMBER_ID  
• SHARD_ID

ROWID is stored in a base-64 value, which can include A ~ Z, a ~ z, 0 ~ 9, +, and /.  
The components of the ROWID can be obtained using ROWID-related functions.

• Storage size: 16 bytes

<a id="7cae050595dd24b4"></a>
### For More Information

Refer to the following.

- [ROWID Pseudo Column](11-sql-elements.md#ddfdf6ed362ba8f0)
- [ROWID-related Functions](11-sql-elements.md#8f97efbf5938c2e2)

<a id="726749f4da2c8c97"></a>
## TIME

<a id="d89b2a1e0f6ac69d"></a>
### Syntax

```
TIME [ ( fractional_seconds_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
```

<a id="f1b2725a112dcbc5"></a>
### Syntax Rules and Parameters

- fractional_seconds_precision: It refers to the number of significant digits in fractional seconds.
    - fractional_seconds_precision range: 0 ~ 6
    - Default value: 6

- [ WITH TIME ZONE | WITHOUT TIME ZONE ]: It specifies whether to store the TIME ZONE value.
    - WITH TIME ZONE: The time that includes the time zone
    - WITHOUT TIME ZONE: The time that does not include the time zone
    - Default value: WITHOUT TIME ZONE

<a id="f262e5ff896641a8"></a>
### Description

The time, including HOUR, MINUTE, and SECOND, is stored.

- Storage size 
    - TIME WITHOUT TIME ZONE: 8 bytes
    - TIME WITH TIME ZONE: 12 bytes

<a id="471148af4933d269"></a>
### For More Information

Refer to the following.

- [Time Literals](11-sql-elements.md#f03167b962c6a80b)
- [Time with Time Zone Literals](11-sql-elements.md#2bc09a30c6210f96)
- [DATE](#e1a7517d0f63a48f)
- [TIMESTAMP](#3f728dfee44599c8)

<a id="3f728dfee44599c8"></a>
## TIMESTAMP

<a id="07d7c95cc0177b18"></a>
### Syntax

```
TIMESTAMP [ ( fractional_seconds_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
```

<a id="4f4cf18a64ace82f"></a>
### Syntax Rules and Parameters

- fractional_seconds_precision: It refers to the number of significant digits in fractional seconds.
    - fractional_seconds_precision range: 0 ~ 6
    - Default value: 6

- [ WITH TIME ZONE | WITHOUT TIME ZONE ]: It specifies whether to store the TIME ZONE value.
    - WITH TIME ZONE: The time that includes the time zone. 
    - WITHOUT TIME ZONE: The time that does not include the time zone. 
    - Default value: WITHOUT TIME ZONE

<a id="75f198ffb01a4af7"></a>
### Description

The time, including YEAR, MONTH, DATE, HOUR, MINUTE, and SECOND, is stored.

- Storage size 
    - TIMESTAMP WITHOUT TIME ZONE: 8 bytes
    - TIMESTAMP WITH TIME ZONE: 12 bytes

<a id="74a464a912e17914"></a>
### For More Information

Refer to the following.

- [Timestamp Literals](11-sql-elements.md#6701ce4c7c705e13)
- [Timestamp with Time Zone Literals](11-sql-elements.md#b7e21173111bed2b)
- [DATE](#e1a7517d0f63a48f)
- [TIME](#726749f4da2c8c97)

---

[← 15. SQL Tuning](15-sql-tuning.md) · [Table of contents](../README.md) · [17. Built-in Function References →](17-built-in-function-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
