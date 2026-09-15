<a id="b4ed5ba13f79f52b"></a>

# 28. External Routine

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/b4ed5ba13f79f52b)  
> Tag: `26c.1_0_tag`

[← 27. PSM Packages](27-psm-packages.md) · [Table of contents](../README.md) · [29. Trigger →](29-trigger.md)

This chapter describes how to develop the database application calling an external routine written in another programming language.

<a id="2fb71bf0a9a14e30"></a>
## External Routine

The external routine is a function stored in the shared library.

Execute the external routine after loading the shared library through the external routine process (gextproc) in PSM routine.  
gextproc returns the execution result of the external routine as the result of PSM routine.  
The user can use the feature implemented in the shared library in DBMS through this feature when it is in need.

<a id="bcadd2c00138b050"></a>
![External routine](../assets/images/9c31bf192fc5ebb5.png)

<a id="34bb77f4fc35e9c7"></a>
## Call Specification

The call specification specifies the information to load and execute the external C function.  
external C function is an external routine which is programmed with C language.

Roles of call specification are as follows.

- Shared library information
- Converting the datatype the parameter
- Mapping according to the parameter's IN, OUT, or IN OUT mode
- Managing the memory
- A call specification can be used in either a Package Specification or a Package Body.

For more information, refer to [Call Specification](30-psm-language-element-references.md#f24bb921ad663f66).

<a id="67ff93d5102f8bc8"></a>
## Loading External C Function

Start external routine process (gextproc) to execute the external C function.  
Use the network which was set in GOLDILOCKS to transfer the following information to gextproc during the PSM routine runtime.

- The path and the name of the shared library file
- The name of the external c function
- The information about the external parameter

gextproc loads the shared library, and executes the external c function, then transfers the return result.

Execute the following steps to call the external C function.

1. Define the external C function.
2. Create the library object which is the schema object corresponding to the shared library
3. Define the call specification to call the external C function.

<a id="3084d8cf3c73fa95"></a>
### External C function

Define the external C function.

The following is an example of creating an addition function.

```
#include <stdio.h>

int add( int a , int b )
{
  return a + b;
}
```

The following is an example of creating the shared library in linux environment.  
gcc option can be added according to the user convenience.

```
gcc -shared -fPIC -o add.so add.c
```

<a id="ec58af926d090453"></a>
### Creating Library Object

The shared library file is an operating system file which stores the external C function and can be dynamically loaded.  
DBA controls the access to the shared library to ensure the security for the shared library.  
DBA uses [CREATE LIBRARY](31-psm-sql-references.md#d3c4a1abc483c544) statement to create the schema object indicating the shared library.  
Then, if the user has a privilege, DBA grants EXECUTE privilege for the library object to the user.  
Or, DBA can grant CREATE ANY LIBRARY privilege, and the user with this privilege can directly create the library object.

```
CREATE LIBRARY [ <schema name> ].<library name>
   { IS | AS } '<file path name>';
```

Specify the name only or the entire path of the shared library file to create the library object.

If only the filename is specified as in the following example, the shared library file must be located in the folder set by the EXTLIB_DIR property to be loaded.

```
CREATE LIBRARY lib_add AS 'add.so';
```

If the user specifies the entire path about the shared library as follows, then gextproc loads the shared library file in the path.

```
CREATE LIBRARY lib_add AS '/home/user/extlib/add.so';
```

<a id="9dca232a83d7d1e4"></a>
### Publish External C function

Specify the external C function to execute by describing the [call specification](30-psm-language-element-references.md#f24bb921ad663f66) statement when DDL the procedure, function or the package.

The example of the PSM routine calling the external C function defined in 3.1 is as follows.

```
CREATE FUNCTION func1( p1 IN NATIVE_INTEGER, 
                       p2 IN NATIVE_INTEGER )
      RETURN NATIVE_INTEGER AS
LANGUAGE C
LIBRARY lib_add NAME "add"
PARAMETERS ( p1 INT,
             p2 INT,
             RETURN INT );
```

Check if the definition of the stored function's PARAMETERS matches the prototype of the external C function as follows.

```
gSQL> \set vertical on

gSQL> SELECT routine_name,
       external_name,
       external_c_function
  FROM information_schema.routines
 WHERE routine_name = 'FUNC1';

            ROUTINE_NAME # FUNC1
           EXTERNAL_NAME # add
     EXTERNAL_C_FUNCTION # int add( int P1 , int P2 )

1 row selected.
```

<a id="cfefc8480c8143e2"></a>
## Specifying External C Function

Execute the published external C function through [Call specification](30-psm-language-element-references.md#f24bb921ad663f66) mapping the external C function name, the parameter datatype and the return datatype to PSM routine.

The call specification consists of the following.

- Development language information
    - Only C language is allowed.
- The name of the library object corresponding to the shared library
- The name of the external C function in the shared library
- Various options to specify the parameter transfer method

The call specification is used in the following statements.

- [CREATE PROCEDURE](31-psm-sql-references.md#d439613cbc283235)
- [CREATE FUNCTION](31-psm-sql-references.md#8343c001bfba29fc)
- [CREATE PACKAGE](31-psm-sql-references.md#d67c80375fa9e3c8)
- [CREATE PACKAGE BODY](31-psm-sql-references.md#397f0c3a716022e0)

The call specification statement is as follows.

```
LANGUAGE C
{ LIBRARY <library name> NAME <double_quote_string> |
  NAME <double_quote_string> LIBRARY <library name> }
[ WITH CONTEXT ] 
PARAMETERS ( <external parameter> [ , ... ] )
```

&lt;library name&gt; is the name of  library schema object, and &lt;double_quote_string&gt; is the name of the external C function.  
&lt;external parameter&gt; is as follows.

```
{
   CONTEXT
 | <parameter name> [ <property> ] [ BY REFERENCE ] <external datatype> 
 | RETURN [ <property> ] [ BY REFERENCE ] <external datatype> 
}
```

&lt;property&gt; is as follows.

```
{
   INDICATOR | LENGTH | MAXLEN 
}
```

<a id="8e84d53eddd6eecc"></a>
### LIBRARY

It is the schema object corresponding to the shared library, and the library name is an identifier.   
The library can be executed only when the EXECUTE privilege exists.

<a id="f57c8a6c3b050803"></a>
### NAME

It is the name of the external C function to call.  
Enclose the name of the external C function with double quotes (" ").

<a id="c5d6ad57df21d1c6"></a>
### LANGUAGE

It indicates the programming language with which the external routine was described.  
Currently, only C language is allowed.

<a id="f1826df0ada4608e"></a>
### WITH CONTEXT

It sets that the CONTEXT is transferred to the  external C function.

<a id="83177ffac2b66f5c"></a>
### PARAMETERS

It specifies the sequence and the datatype of the parameter which is transferred to the external C function.  
It can specify the parameter properties such as the current length and the maximum length, and how to transfer the parameter value.

<a id="97984ee31c5fbe48"></a>
## Example of Call Specifications

- Procedure

```
gSQL>
CREATE OR REPLACE PROCEDURE proc1( p1 IN NATIVE_INTEGER,
                                   p2 IN NATIVE_INTEGER,
                                   p3 OUT NATIVE_INTEGER )
AS
LANGUAGE C
LIBRARY lib_sample NAME "sample_add_proc"
PARAMETERS( p1 INT,
            p2 INT,
            p3 INT );
/

Procedure created.
```

- Function

```
gSQL>
CREATE OR REPLACE FUNCTION func1( p1 IN NATIVE_INTEGER,
                                  p2 IN NATIVE_INTEGER )
    RETURN NATIVE_INTEGER
AS
LANGUAGE C
NAME "sample_add_func" LIBRARY lib_sample
PARAMETERS( p1 INT,
            p2 INT,
            RETURN INT );
/

Function created.
```

- Package specification

```
gSQL>
CREATE OR REPLACE PACKAGE pkg1 AS  
  FUNCTION func1( p1 IN NATIVE_INTEGER,
                  p2 IN NATIVE_INTEGER )
      RETURN NATIVE_INTEGER
  AS
  LANGUAGE C
  NAME "sample_add_func" LIBRARY lib_sample
  PARAMETERS( p1 INT,
              p2 INT,
              RETURN INT );
END;
/

Package created.
```

- Package body

```
gSQL>
CREATE OR REPLACE PACKAGE pkg1 AS   
  FUNCTION func1( p1 IN NATIVE_INTEGER,
                  p2 IN NATIVE_INTEGER )
      RETURN NATIVE_INTEGER;
END;
/

Package created.

gSQL>
CREATE OR REPLACE PACKAGE BODY pkg1 AS   
  FUNCTION func1( p1 IN NATIVE_INTEGER,
                  p2 IN NATIVE_INTEGER )
      RETURN NATIVE_INTEGER
  AS
  LANGUAGE C
  NAME "sample_add_func" LIBRARY lib_sample
  PARAMETERS( p1 INT,
              p2 INT,
              RETURN INT );
END;
/

Package created.
```

<a id="f023c704e3580e98"></a>
## Passing Parameters to External C Functions with Call Specifications

The call specification maps PSM to the datatype of C.  
It is complicated to transfer the parameter of the external C function for some reasons.

- The matching of the datatype of PSM and the datatype of C is not 1:1.
- Unlike C, the parameter of PSM has NULL of RDBMS, so NULL is allowed for the parameter of PSM, but NULL is not allowed to the parameter of C.
- The external C function may require the length of PSM datatype such as CHAR, VACHAR, LONG VARCHAR, BINARY, VARBINARY, and LONG VARBINARY, or the maximum length information.
- PSM routine may require the current length of the value returned from the external C function and NULL state information.

<a id="6b0591097506393d"></a>
### Parameter Data Type Mapping

The parameter of PSM routine is mapped to the external C function as follows.

**Parameter Data Type Mappings**

<a id="3539923d3f546a1f"></a>
| PSM datatype | external datatype | recommend external datatype |
| --- | --- | --- |
| BOOLEAN | UNSIGNED CHAR CHAR UNSIGNED SHORT SHORT UNSIGNED INT INT UNSIGNED LONG LONG | CHAR |
| NATIVE_SMALLINT | UNSIGNED CHAR CHAR UNSIGNED SHORT SHORT UNSIGNED INT INT UNSIGNED LONG LONG | SHORT |
| NATIVE_INTEGER | UNSIGNED CHAR CHAR UNSIGNED SHORT SHORT UNSIGNED INT INT UNSIGNED LONG LONG | INT |
| NATIVE_BIGINT | UNSIGNED CHAR CHAR UNSIGNED SHORT SHORT UNSIGNED INT INT UNSIGNED LONG LONG | LONG |
| NATIVE_REAL | FLOAT DOUBLE | FLOAT |
| NATIVE_DOUBLE | FLOAT DOUBLE | DOUBLE |
| FLOAT | DOUBLE | DOUBLE |
| NUMBER w/o precision | DOUBLE | DOUBLE |
| NUMBER w/ precision | SQL_NUMERIC | SQL_NUMERIC |
| CHAR | STRING | STRING |
| VARCHAR | STRING | STRING |
| LONG VARCHAR | SQL_LONG_VARIABLE_LENGTH | SQL_LONG_VARIABLE_LENGTH |
| BINARY | RAW | RAW |
| VARBINARY | RAW | RAW |
| LONG VARBINARY | SQL_LONG_VARIABLE_LENGTH | SQL_LONG_VARIABLE_LENGTH |
| DATE | SQL_DATA SQL_TIMESTAMP | SQL_TIMESTAMP |
| TIME | SQL_TIME | SQL_TIME |
| TIME WITH TIME ZONE | SQL_TIME_TZ | SQL_TIME_TZ |
| TIMESTAMP | SQL_TIMESTAMP | SQL_TIMESTAMP |
| TIMESTAMP WITH TIME ZONE | SQL_TIMESTAMP_TZ | SQL_TIMESTAMP_TZ |
| INTERVAL YEAR TO MONTH | SQL_INTERVAL | SQL_INTERVAL |
| INTERVAL DAY TO SECOND | SQL_INTERVAL | SQL_INTERVAL |
| ROWID | STRING | STRING |

<a id="efed85a023366f6e"></a>
### External Data Type Mapping

The external datatype is mapped to C datatype. Refer to the following table to avoid an error when describing C prototype.

**External Data Type Mapping**

<a id="4ef8572adee543fb"></a>
| external datatype | parameter mode is IN or RETURN | parameter mode is  IN by reference or RETURNING by reference | parameter mode is  OUT type, IN OUT type |
| --- | --- | --- | --- |
| UNSIGNED CHAR | unsigned char | unsigned char * | unsigned char * |
| CHAR | char | char * | char * |
| UNSIGNED SHORT | unsigned short | unsigned short * | unsigned short * |
| SHORT | short | short * | short * |
| UNSIGNED INT | unsigned int | unsigned int * | unsigned int * |
| INT | int | int * | int * |
| UNSIGNED LONG | unsigned long | unsigned long * | unsigned long * |
| LONG | long | long * | long * |
| FLOAT | float | float * | float * |
| DOUBLE | double | double * | double * |
| STRING | char * | char * | char * |
| RAW | unsigned char * | unsigned char * | unsigned char * |
| SQL_LONG_VARIABLE_LENGTH | SQL_LONG_VARIABLE_LENGTH_STRUCT * | SQL_LONG_VARIABLE_LENGTH_STRUCT * | SQL_LONG_VARIABLE_LENGTH_STRUCT * |
| SQL_NUMERIC | SQL_NUMERIC_STRUCT * | SQL_NUMERIC_STRUCT * | SQL_NUMERIC_STRUCT * |
| SQL_DATE | SQL_DATE_STRUCT * | SQL_DATE_STRUCT * | SQL_DATE_STRUCT * |
| SQL_TIME | SQL_TIME_STRUCT * | SQL_TIME_STRUCT * | SQL_TIME_STRUCT * |
| SQL_TIME_TZ | SQL_TIME_WITH_TIMEZONE_STRUCT * | SQL_TIME_WITH_TIMEZONE_STRUCT * | SQL_TIME_WITH_TIMEZONE_STRUCT * |
| SQL_TIMESTAMP | SQL_TIMESTAMP_STRUCT * | SQL_TIMESTAMP_STRUCT * | SQL_TIMESTAMP_STRUCT * |
| SQL_TIMESTAMP_TZ | SQL_TIMESTAMP_WITH_TIMEZONE_STRUCT * | SQL_TIMESTAMP_WITH_TIMEZONE_STRUCT * | SQL_TIMESTAMP_WITH_TIMEZONE_STRUCT * |
| SQL_INTERNAL | SQL_INTERVAL_STRUCT * | SQL_INTERVAL_STRUCT * | SQL_INTERVAL_STRUCT * |

<a id="01cdfba147fe3bd0"></a>
### Passing Parameters by VALUE or BY REFERENCE

If the parameter mode is IN type or RETURN, then it is transferred as pass by value. If BY REFERENCE option is given, it is transferred as pass by reference even though the parameter mode is IN type or RETURN.  
If the parameter mode is OUT type or IN OUT type, then it is transferred as pass by reference.  BY REFERENCE option does not have any effect.   
However, the following external datatypes are transferred as pass by reference.

- STRING
- RAW
- SQL_LONG_VARIABLE_LENGTH
- SQL_NUMERIC
- SQL_DATE
- SQL_TIME
- SQL_TIME_TZ
- SQL_TIMESTAMP
- SQL_TIMESTAMP_TZ
- SQL_INTERVAL

<a id="a93237316677968d"></a>
### Declaring Formal Parameters

Generally, the routine executing the external C function declares the formal parameters as follows.

```
CREATE FUNCTION func1( p1 IN NATIVE_INTEGER, 
                       p2 IN NATIVE_INTEGER )
      RETURN NATIVE_INTEGER AS
LANGUAGE C
LIBRARY lib_add NAME "add"
PARAMETERS ( p1 INT,
             p2 INT,
             RETURN INT );
```

Specify the parameter mode and the datatype when declaring each formal parameter. This information is required for the external C function, and it provides the following information by using PARAMETERS clause.

- external datatype
- The current length and the maximum length of the parameter
- NULL/NOT NULL indicator for the parameter
- The location of the parameter
- How to transfer IN type parameter

Be cautious the following when describing PARAMETERS clause.

- All formal parameters should be described in PARAMETERS clause.
- If a WITH CONTEXT clause is included, then CONTEXT parameter should be specified in PARAMETERS clause.
- RETURN should always be specified last.

<a id="b1ffbd9aef640cda"></a>
### Properties

PSM formal parameter and the function result can be transferred to the external C function by using PARAMETERS clause. It is executed by specifying properties.

The following table describes the external datatype, the PSM datatype and the PSM Parameter mode which are allowed to the specified property.

**Properties and data types**

<a id="c3ce2f5fc71dace0"></a>
| Property | external datatype | default external datatype | PSM datatype | PSM Parameter Mode | Passing Method |
| --- | --- | --- | --- | --- | --- |
| INDICATOR | short | short | all datatype | IN IN OUT OUT RETURN | BY VALUE BY REFERENCE BY REFERENCE BY REFERENCE |
| LENGTH | unsigned short short unsigned int int unsigned long long | int | CHAR VARCHAR LONG VARCHAR BINARY VARBINARY LONG VARBINARY | IN IN OUT OUT RETURN | BY VALUE BY REFERENCE BY REFERENCE BY REFERENCE |
| MAXLEN | unsigned short short unsigned int int unsigned long long | int | CHAR VARCHAR LONG VARCHAR BINARY VARBINARY LONG VARBINARY | IN OUT OUT RETURN | BY VALUE |

The following is an example of specifying the properties of PSM formal parameter and RETURN by using PARAMETER clause.

```
CREATE OR REPLACE FUNCTION strncpy_func( p1 IN CHAR(10),
                                         p2 IN OUT CHAR(10) )
RETURN VARCHAR AS
LANGUAGE C
LIBRARY strncpy_lib NAME "strncpy_extern_func"
PARAMETERS( p1 STRING,              -- The value of formal parameter p1
            p1 INDICATOR SHORT,     -- Whether the formal parameter p1 is NULL
            p1 LENGTH INT,          -- The current length of formal parameter p1
            p2 STRING,              -- The value of formal parameter p2
            p2 INDICATOR SHORT,     -- Whether the formal parameter p2 is NULL
            p2 LENGTH INT,          -- The current length of formal parameter p2   
            p2 MAXLEN INT,          -- The maximum length of formal parameter p2
            RETURN LENGTH INT,      -- The current length of RETURN value
            RETURN STRING );        -- RETURN value
```

The following C prototype is expected through PARAMETERS clause above.

```
char * strncpy_extern_func( char  * p1,
                            short   p1_indicator,
                            int     p1_length,
                            char  * p2,
                            short * p2_indicator,
                            int   * p2_length,
                            int     p2_maxlen,
                            int   * return_length );
```

C prototype as given above can be found through information_schema.routines.

```
gSQL> \set vertical on

gSQL>
SELECT routine_name,
       external_name,
       external_c_function
  FROM information_schema.routines
 WHERE routine_name = 'STRNCPY_FUNC';

            ROUTINE_NAME # STRNCPY_FUNC
           EXTERNAL_NAME # strncpy_extern_func
     EXTERNAL_C_FUNCTION # char * strncpy_extern_func( char * P1 , short P1_INDICATOR , int P1_LENGTH , char * P2 , short * P2_INDICATOR , int * P2_LENGTH , int P2_MAXLEN , int * RETURN_LENGTH )

1 row selected.
```

<a id="eec3678fe6b0cb2d"></a>
#### INDICATOR

INDICATOR is a property indicating whether the parameter is NULL.

DBMS has a NULL, but C language does not have a NULL.  
NULL information should be transferable between the PSM routine and the external C function.  
If the parameter is NULL, then it should be able to find that the parameter value is NULL in the external C function.  
On the other hand, if the return result of the external C function is NULL, then it should be able to find in the server.

In this case, the information is transferable through INDICATOR property.  
INDICATOR value can be found through SQL_NULL_DATA constant.

- If INDICATOR value is the same as SQL_NULL_DATA, then the related parameter value is NULL.
- If INDICATOR value is not same as SQL_NULL_DATA, then the related parameter value is not NULL.

If it is parameter mode and RETURN, the INDICATOR value is transferred as follows.

- Parameter Mode
    - IN mode
        - Transfer by value, read mode
    - OUT mode , IN OUT mode
        - Transfer by the reference
- RETURN
    - Transfer by the reference

<a id="0393e925248f2aec"></a>
#### LENGTH and MAXLEN

LENGTH and MAXLEN are properties which represent the current length and the maximum length of the CHARACTER STRING type, BINARY STRING type parameters.

LENGTH value represents the current length of the parameter mode and RETURN, and it is transferred as follows.

- Parameter Mode
    - IN mode
        - Transfer by value, read mode
    - OUT mode , IN OUT mode
        - Transfer by the reference
- RETURN
    - Transfer by the reference

MAXLEN value represents the maximum length of the parameter mode and RETURN, and it is transferred as follows.

- Parameter Mode
    - IN mode
        - not applicable
    - OUT mode , IN OUT mode
        - Transfer by the reference, read only
- RETURN
    - Transfer by the reference, read only

<a id="1dd643203b5f6f8f"></a>
#### BY REFERENCE

BY REFERENCE specifies to transfer the value by the reference.  
The constant can be transferred by the value or by the reference in C language.   
If C function is a pointer variable, then it specifies BY REFERENCE statement and transfers the parameter by the reference.

The following is an example.

```
CREATE OR REPLACE PROCEDURE circleArea( radius IN NATIVE_INTEGER,
                                        area OUT FLOAT ) AS
LANGUAGE C
NAME "circle_area" LIBRARY circle_lib
PARAMETERS( radius BY REFERENCE INT,
            area DOUBLE );
/
```

In this case, the prototype of c function is as follows.

```
void circle_area( int * radius , double * area );
```

<a id="d9266a14fba98273"></a>
#### WITH CONTEXT

If WITH CONTEXT clause is included, then the access privilege to information about the parameter, the memory allocation and the exception can be granted in the external C function.  
WITH CONTEXT clause specifies that CONTEXT variable is transferred to the external C function.

The following is an example.

```
CREATE FUNCTION str_concat( p1 VARCHAR,
                            p2 VARCHAR )
RETURN VARCHAR
AS LANGUAGE C
LIBRARY lib_context
NAME "c_concat"
WITH CONTEXT
PARAMETERS ( CONTEXT,
             p1 STRING,
             p2 STRING,
             RETURN STRING );
/
```

In this case, the prototype of C function is as follows.

```
char * c_concat( SQLExtProcContext * context , char * p1 , char * p2 );
```

<a id="9c7b5f7beaece03a"></a>
## Using Service Routines with External C Functions

<a id="125e938214130235"></a>
### SQLExtProcAllocCallMemory()

SQLExtProcAllocCallMemory function allocates the memory in the external C function.  
The memories allocated in the function is automatically released when they are returned to PSM.

The following is an example of PSM and C function for SQLExtProcAllocCallMemory().

- C prototype

```
char * c_concat( SQLExtProcContext * context,    
                 char              * p1,    
                 short               p1_indicator,     
                 int                 p1_length,         
                 char              * p2,    
                 short               p2_indicator,    
                 int                 p2_length,    
                 short             * result_indicator,    
                 int               * result_length );
```

- PSM function and execution

```
CREATE OR REPLACE  FUNCTION str_concat( p1 VARCHAR,
                                        p2 VARCHAR )
  RETURN VARCHAR AS
LANGUAGE C
LIBRARY lib_concat
NAME "c_concat"
WITH CONTEXT
PARAMETERS ( CONTEXT,
             p1 STRING,
             p1 INDICATOR SHORT,
             p1 LENGTH INT,
             p2 STRING,
             p2 INDICATOR SHORT,
             p2 LENGTH INT,
             RETURN INDICATOR SHORT,
             RETURN LENGTH INT,
             RETURN STRING );
/
```

```
gSQL>
SELECT str_concat( 'Hello, ' , 'GOLDILOCKS' ) FROM dual;

STR_CONCAT( 'Hello, ' , 'GOLDILOCKS' )
--------------------------------------
Hello, GOLDILOCKS                     

1 row selected.
```

- C function which allocates the memory by using SQLExtProcAllocCallMemory()

```
#include <stdio.h>
#include <string.h>
#include <goldilocks.h>

char * c_concat( SQLExtProcContext * context,
                 char              * p1,
                 short               p1_indicator,
                 int                 p1_length,
                 char              * p2,
                 short               p2_indicator,
                 int                 p2_length,
                 short             * result_indicator,
                 int               * result_length )
{ 
    char * resultStr       = NULL;
    int    resultLen       = 0;
    short  resultIndicator = SQL_NULL_DATA;

    /*
     * Check whether it is NULL
     */      
    
    if( (p1_indicator == SQL_NULL_DATA) || (p2_indicator == SQL_NULL_DATA) )
    {
        resultIndicator = SQL_NULL_DATA;
        resultLen       = 0;
             
        /*   
         * PSM does not have a NULL Pointer. Therefore, it returns zero-byte string as the result.
         */

        resultStr = SQLExtProcAllocCallMemory( context, 1 );
        resultStr[resultLen] = '\0';
    }
    else
    {
        resultIndicator = !SQL_NULL_DATA;
        resultLen       = p1_length + p2_length;

        /*
         * It allocates the memory for the result considering the last NULL terminator.
         */

        resultStr = SQLExtProcAllocCallMemory( context, resultLen + 1 );

        /*
         * string concat
         */

        strcpy( resultStr, p1 );
        strcat( resultStr, p2 );
        resultStr[resultLen] = '\0';
    }

    /*
     * Return result
     * PSM releases the allocated memory later.
     */

    *result_indicator = resultIndicator;
    *result_length    = resultLen;

    return resultStr;
}
```

<a id="2af8ed21f4f5368c"></a>
### SQLExtProcRaiseServerError()

SQLExtProcRaiseServerError function causes a predefined exception.   
Specify GOLDILOCKS error number to use this exception.

The following is an example of PSM and C function for SQLExtProcRaiseServerError().

- C prototype

```
void c_division( SQLExtProcContext * context,
                 int                 dividend,
                 int                 divisor,
                 double            * result );
```

- PSM function and execution

```
CREATE OR REPLACE PROCEDURE proc_division( dividend     NATIVE_INTEGER,
                                           divisor  IN  NATIVE_INTEGER,
                                           result   OUT FLOAT )
AS
LANGUAGE C
LIBRARY lib_division NAME "c_division"
WITH CONTEXT
PARAMETERS( CONTEXT,
            dividend INT,
            divisor  INT,
            result   DOUBLE );
/
```

```
gSQL> \var ret double

gSQL> CALL proc_division( 10 , 0 , :ret );

ERR-38000(12122): divisor is equal to zero : ERROR at PROCEDURE("PROC_DIVISION")
```

- C function which allocates the memory by using SQLExtProcAllocCallMemory()

```
#include <stdio.h>
#include <assert.h>
#include <goldilocks.h>

void c_division( SQLExtProcContext * context,
                 int                 dividend,
                 int                 divisor,
                 double            * result )
{
    /*
     * Check if divisor is 0.
     */
    
    if( divisor == 0 )
    {
        /*
         * It returns ZERO_DIVIDE error.
         * GOLDILOCKS error code is 12122.
         */ 
    
        if( SQLExtProcRaiseServerError( context, 12122 ) == SQL_SUCCESS )
        {
            return;
        }
        else
        {
            assert( 0 );
        }
    }

    *result = (double) dividend / (double) divisor;
}
```

<a id="5ead7a017aab9ac2"></a>
### SQLExtProcRaiseUserError()

SQLExtProcRaiseUserError causes a user-defined exception.  
The user can define the error by specifying the error code and the error message.  
Error codes 20000 ~ 20999 are available.

The following is an example of PSM and C function for SQLExtProcRaiseUserError().

- C prototype

```
void c_division( SQLExtProcContext * context,
                 int                 dividend,
                 int                 divisor,
                 double            * result );
```

- PSM function and execution

```
CREATE OR REPLACE PROCEDURE proc_division( dividend     NATIVE_INTEGER,
                                           divisor  IN  NATIVE_INTEGER,
                                           result   OUT FLOAT )
AS
LANGUAGE C
LIBRARY lib_division NAME "c_division"
WITH CONTEXT
PARAMETERS( CONTEXT,
            dividend INT,
            divisor  INT,
            result   DOUBLE );
/
```

```
gSQL> \var ret double

gSQL> CALL proc_division( 10 , 0 , :ret );

ERR-38000(20001): 0 is not allowed in the divisor. : ERROR at PROCEDURE("PROC_DIVISION")
```

- C function which allocates the memory by using SQLExtProcAllocCallMemory()

```
#include <stdio.h>
#include <assert.h>
#include <goldilocks.h>

void c_division( SQLExtProcContext * context,
                 int                 dividend,
                 int                 divisor,
                 double            * result )
{
    /*
     * Check if divisor is 0.
     */
            
    if( divisor == 0 )
    {
        /*  
         * It returns User Defined exception.
         * In this case, the error code and message should be included.
         * Use can use the error codes 20000 ~ 20999.
         */
            
        if( SQLExtProcRaiseUserError( context, 20001, (SQLCHAR *) "0 is not allowed in the divisor." ) == SQL_SUCCESS )
        {
            return;
        } 
        else
        {
            assert( 0 );
        }
    }

    *result = (double) dividend / (double) divisor;
}
```

<a id="6f1c121f6414e55c"></a>
## Troubleshooting of ERR-39000(26009): Lost Connection to 'gextproc'

ERR-39000(26009): lost connection to 'gextproc' mostly caused by two user errors.

- If the external C function written by the user is wrong
- If the PARAMETERS information of user-written external C function and PSM routine are different

If ERR-39000(26009) error occurs because gextproc process is abnormally terminated, the trace log file is created in $GOLDILOCKS_DATA/extlib directory, classified by a process ID.

<a id="62833ac7441160a1"></a>
### If External C Function Written By User Is Wrong

If the user library is wrong, then the C function name called in the user library is found in callstack of the trace log file.

The following C function is wrong.

```
int add_f(int a, int b)
{
    int *c = NULL;
    *c = a + b;
    return a + b;
}
```

The following is an example of writing PSM routine calling the external C function.

```
gSQL>
CREATE LIBRARY lib1 as 'add.so';
/
Library created.

gSQL>
CREATE OR REPLACE FUNCTION func1( p1 NATIVE_INTEGER, p2 NATIVE_INTEGER ) 
    RETURN NATIVE_INTEGER AS
LANGUAGE C
LIBRARY lib1 NAME "add_f"
PARAMETERS ( p1 INT , p2 INT , RETURN INT );
/
Function created.

gSQL> SELECT func1(1, 1) FROM dual;
ERR-39000(26009): lost connection to 'gextproc': ERROR at FUNCTION("FUNC1")
```

The following is the trace file (gextproc.448892.trc) created as above.

```
% cat gextproc.448892.trc
SIGNAL(11) received
=================================================
CALL STACK
=================================================
gextproc(stbBacktraceToFile+0x18)[0x4f2ed8]
gextproc(ztemFatalHandler+0x178)[0x431e58]
gextproc(steFatalHandler+0x6a)[0x4f2e6a]
/lib/x86_64-linux-gnu/libpthread.so.0(+0x14420)[0x7faaa025c420]
/home/test/work/product/Gliese/home/extlib/managed/add.so(add_f+0x22)[0x7faaa03d111b]
gextproc[0x4f2a12]
```

It is found in the trace file that add.so(add_f+0x22) line is included in callstack.

<a id="b2a30c7267ded2fe"></a>
### If the PARAMETERS information of user-written external C function and PSM routine are different

If the PARAMETERS information of user-written external C function and PSM routine are different, then only gextproc exists in callstack of the trace log.

The following is C function written by the user.

```
int add(int p1, int p2)
{
    return p1 + p2;
}
```

The following is PSM routine calling the external C function called as add.

```
gSQL> 
CREATE LIBRARY lib2 AS 'add.so';
/
Library created.

gSQL>
CREATE OR REPLACE FUNCTION func2(p1 NATIVE_INTEGER, 
                                 p2 NATIVE_INTEGER,
                                 p3 NATIVE_INTEGER)
    RETURN VARCHAR AS
LANGUAGE C
LIBRARY lib2 NAME "add"
PARAMETERS ( p1 INT , p2 INT , p3 INT , RETURN STRING );
/
Function created.

gSQL> SELECT func2(1, 1, 1) FROM dual;
ERR-39000(26009): lost connection to 'gextproc': ERROR at FUNCTION("FUNC2")
```

The following is the trace file (gextproc.449987.trc) created as above.

```
% cat gextproc.449987.trc
SIGNAL(11) received
=================================================
CALL STACK
=================================================
gextproc(stbBacktraceToFile+0x18)[0x4f2ed8]
gextproc(ztemFatalHandler+0x178)[0x431e58]
gextproc(steFatalHandler+0x6a)[0x4f2e6a]
/lib/x86_64-linux-gnu/libpthread.so.0(+0x14420)[0x7f5b0a52a420]
/lib/x86_64-linux-gnu/libc.so.6(+0x188915)[0x7f5b0a49c915]
gextproc(ffvExternalStringToParameterVarChar+0x108)[0x438a48]
gextproc(fffSetOutParameterValues+0x315)[0x438475]
gextproc(fflExecuteFunction+0x138)[0x434eb8]
gextproc(ztepCmdCallExternalFunction+0x177)[0x4341d7]
gextproc(ztecRun+0x362)[0x432b52]
gextproc(main+0x1ce)[0x431bce]
/lib/x86_64-linux-gnu/libc.so.6(__libc_start_main+0xf3)[0x7f5b0a338083]
gextproc(_start+0x2e)[0x431c1e]
```

The user library does not exist in callstack, and the error occurred only in gextproc.

The external C function prototype configured through the PARAMETERS information of PSM routine is found as follows.

```
gSQL>
SELECT specific_name ,
       external_c_function
  FROM information_schema.routines
 WHERE specific_name = 'FUNC2';

SPECIFIC_NAME EXTERNAL_C_FUNCTION                   
------------- --------------------------------------
FUNC2         char * add( int P1 , int P2 , int P3 )

1 row selected.
```

The information above describes that the PARAMETER information of the user-written external C function and the created PSM routine are different.

- User-written external C function

```
int add(int p1, int p2)
```

- The external C function prototype by PARAMETER information of when creating PSM routine.

```
char * add( int P1 , int P2 , int P3 )
```

PARAMETERS information of the user-written external C function and that of PSM routine creation should be same to properly operate the external routine.  
Otherwise, the external routine process is abnormally terminated and unexpected result may occur.

---

[← 27. PSM Packages](27-psm-packages.md) · [Table of contents](../README.md) · [29. Trigger →](29-trigger.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
