<a id="c50a929fc9fb7263"></a>

# 45. gloader/gloadernet (Upload/download Tool)

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/c50a929fc9fb7263)  
> Tag: `26c.1_0_tag`

[← 44. gsql/gsqlnet (Interactive SQL Tool)](44-gsql-gsqlnet-interactive-sql-tool.md) · [Table of contents](../README.md) · [46. gdump →](46-gdump.md)

<a id="a46331ab983393e8"></a>
## Overview of gloader and gloadernet

gloader is a utility which downloads or uploads data of GOLDILOCKS in table unit.

**Execution files**

<a id="035bedf9b35a970b"></a>
| Name | Description |
| --- | --- |
| gloader | It is used in Direct Attach (D/A) environment. |
| gloadernet | It is used in Client/ Server (C/S) environment. |

<a id="fbe9e8111fe9dc51"></a>
### Environment

gloader should be connected to the database and it requires attention to all required files while using gloader.

<a id="ec8a2ca275cc24b8"></a>
![gloader environment](../assets/images/f9793e9cfe7eac26.png)

The control file and datafile are required to upload the data, then the log file is generated as a result.  
The control file is required to download the data, then the datafile, log file, and bad file are generated as the results.

<a id="1c74f3776b193281"></a>
#### Control File

The control file is a file for operating gloader and it includes the following information. (Refer to [Control File Syntax](#6232e22e3f4f912c).)

- Table name
- Schema name
- The delimiter between columns in a row
- The qualifier notifying the start and end of the data
- The delimiter between rows
- Character set
- Whether to trim the whitespace character
- Where clause
- Column designation

<a id="3095a8282f59651a"></a>
#### DataFile

The datafile should be prepared when gloader uploads the data, and it is created when gloader downloads the data.  
The datafile supports text format and binary format.

- The datafile in text format has an advantage of which the file contents can be checked and directly updated. 
- The datafile in binary format can be performed faster comparing to the datafile in text format.

> gloader uses direct I/O for the data file by default. gloader arbitrarily adjusts the file size if the file size is not an array appropriate for direct I/O when uploading the data file by using direct I/O.

<a id="a97e213f6c72139b"></a>
#### Log File

Log file is a file which stores the following errors and results which occur while operating gloader.

- The row number and cause of the error 
- The operating results of gloader

<a id="252131448a123d4e"></a>
#### Bad File

Bad file is a file which stores the rows in which an error occurred while gloader uploads the data. The delimiter between columns and rows, and the qualifier which are used to store the bad file should be user-defined.

<a id="6e517f7c7eae6df2"></a>
### Example

The following is an example of downloading and uploading data by using gloader.

A table is created by using the SQL statement as follows.

```
$ cat test.sql
CREATE TABLE TEST
(
TEST_NAME VARCHAR(60),
TEST_NUM  INTEGER,
TEST_TIME TIMESTAMP(0) WITH TIME ZONE
);

INSERT INTO TEST VALUES
( 'NAME', 1, '1999-01-08 04:05:06.789 -8:00' );
INSERT INTO TEST VALUES
( 'NAME', 2, '1999-01-08 04:05:06.789 -8:00' );
INSERT INTO TEST VALUES
( 'NAME', 3, '1999-01-08 04:05:06.789 -8:00' );
COMMIT;
```

The control file is used as follows.

```
$ cat test.ctl
TABLE TEST
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
```

- Export: It downloads the data.

```
$ gloader test test --export --control test.ctl --data test.dat --no-prompt

 COMPLETED IN EXPORTING TABLE: PUBLIC.TEST, 3 RECORDS
$ cat test.dat
"NAME","1","1999-01-08 04:05:07. -08:00"
"NAME","2","1999-01-08 04:05:07. -08:00"
"NAME","3","1999-01-08 04:05:07. -08:00"
$ cat test.log
cat test.log
COMPLETED IN EXPORTING TABLE: PUBLIC.TEST, 3 RECORDS [ Start Time: 2010-1-1 01:01:01 End Time: 2010-1-1 01:01:01 Taken Time: 56496 micro-sec ]
```

- Import: It uploads the data.

```
$ cat import.dat
"NAME","1","1999-01-08 04:05:07. -08:00"
"NAME","2","1999-01-08 04:05:07. -08:00"
"NAME","3","1999-01-08 04:05:07. -08:00"
"FAIL","FAIL","FAIL"

$ gloader test test --import --control test.ctl --data import.dat --no-prompt

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 4 RECORDS, SUCCEEDED 3 RECORDS

$ gsql test test
gSQL> select * from test;
TEST_NAME TEST_NUM TEST_TIME                        
--------- -------- ---------------------------------
NAME             1 1999-01-08 04:05:07.000000 -08:00
NAME             2 1999-01-08 04:05:07.000000 -08:00
NAME             3 1999-01-08 04:05:07.000000 -08:00
NAME             1 1999-01-08 04:05:07.000000 -08:00
NAME             2 1999-01-08 04:05:07.000000 -08:00
NAME             3 1999-01-08 04:05:07.000000 -08:00

6 rows selected.

$ cat import.log
Err Rec(4) Col(2): 22018(12006): data value is not a numeric literal
COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 4 RECORDS, SUCCEEDED 3 RECORDS [ Start Time: 2010-1-1 01:01:01 End Time: 2010-1-1 01:01:01 Taken Time: 56496 micro-sec ]

$ cat import.bad
"FAIL","FAIL","FAIL"
```

<a id="ca6bdeca4d305771"></a>
## Using gloader

<a id="60debe1440188869"></a>
### Datafile Type

<a id="aa9dc2acec22bf26"></a>
#### Text Datafile

It is represented with a string which can be checked and edited by the user. A user can directly create, edit the file, or can download the data from the existing tables in the database. A user also can use the data in a text format downloaded from another DBMS products.  
The description for the representation of the text type datafile is recorded in the control file.

<a id="121bb957bfd5438e"></a>
#### Binary Datafile

The file consists of binary data. A user can not directly create or edit the binary datafile. The file is generated when downloading the data from the existing tables in the database.

The binary type file is uploaded faster than the text type because the data is written to the file appropriate to the data structure type defined in GOLDILOCKS.

> When GOLDILOCKS databases' versions are different one another, then it is not recommended to upload/ download by using a binary datafile. Also, it may be required to chang a column size when uploading/ downloading data between databases whose string sets are different.

<a id="6148c99b9e84e070"></a>
### Downloading Data

<a id="7e9d8a0eb81cd19a"></a>
#### Downloading in Text File

<a id="fc2da8f35061b76e"></a>
##### Simple Download

The following is the structure and data of the table to be downloaded.

```
$ cat test.sql
CREATE TABLE TEST ( I1 INTEGER PRIMARY KEY, I2 VARCHAR(10), I3 VARBINARY(10) );
INSERT INTO TEST VALUES( 1, 'LKH', X'10' );
INSERT INTO TEST VALUES( 2, 'KMM', X'A0' );
INSERT INTO TEST VALUES( 3, 'ksj', X'CD' );
COMMIT;

$ gsql test test
gSQL> SELECT * FROM TEST;

I1 I2  I3
-- --- --
 1 LKH 10
 2 KMM A0
 3 ksj CD

3 rows selected.
```

The following is the contents of the control file which is created to download the table data.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
```

The data in the table T1 is downloaded through gloader as follows.

```
$ gloader test test --export --control test.ctl --data test.dat

 COMPLETED IN EXPORTING TABLE: PUBLIC.test, 3 RECORDS
```

The data in the table TEST is downloaded to the datafile as follows.

```
$ ls 
test.ctl test.dat test.log
$ cat test.dat
1,LKH,10
2,KMM,A0
3,ksj,CD
```

<a id="934bf4c5f2df18e5"></a>
##### Whitespace Character

The following is the structure and data of the table to be downloaded.

```
$ cat test.sql
CREATE TABLE TEST ( I1 INTEGER PRIMARY KEY, I2 VARCHAR(10), I3 VARBINARY(10) );
INSERT INTO TEST VALUES( 1, ' L K H ', X'10' );
INSERT INTO TEST VALUES( 2, 'KIM
MM', X'A0' );
INSERT INTO TEST VALUES( 3, ' KIM S 
J ', X'CD' );
COMMIT;

$ gsql test test
gSQL> SELECT * FROM TEST;

I1 I2      I3
-- ------- --
 1  L K H  10
 2 KIM     A0
   MM        
 3  KIM S  CD
   J       
3 rows selected.
```

- The control file without using OPTIONALLY ENCLOSED BY statement

    - The following is the contents of the control file which is created to download the table data.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
LINES TERMINATED BY '\n'
```

    - The data in the table TEST is downloaded to the datafile as follows.

```
$ ls 
test.ctl test.dat test.log
$ cat test.dat
1, L K H ,10
2,KIM
MM,A0
3, KIM S 
J ,CD
```

> The control file should be used with the OPTIONALLY ENCLOSED BY statement for the data including the white space to maintain the downloaded data and the uploaded data as same.

- The control file using OPTIONALLY ENCLOSED BY statement

    - The following is the contents of the control file which is created to download the table data.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
```

    - The data in the table TEST is downloaded to the datafile as follows.

```
$ ls 
test.ctl test.dat test.log
$ cat test.dat
"1"," L K H ","10"
"2","KIM
MM","A0"
"3"," KIM S 
J ","CD"
```

<a id="42474eb4704de78d"></a>
##### Time Related Data Type

DATE, TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE are output in the property default format when downloaded.

The following is each data type of DATE, TIME WITH TIME ZONE, TIMESTAMP WITH TIME ZONE.

```
$ gsql test test
gSQL> SELECT PROPERTY_VALUE, INIT_VALUE FROM V$PROPERTY WHERE PROPERTY_NAME LIKE 'NLS_DATE_FORMAT';

PROPERTY_VALUE                    INIT_VALUE                       
--------------------------------- ---------------------------------
YYYY-MM-DD                        YYYY-MM-DD 

1 row selected.

gSQL> SELECT PROPERTY_VALUE, INIT_VALUE FROM V$PROPERTY WHERE PROPERTY_NAME LIKE 'NLS_TIME_WITH_TIME_ZONE_FORMAT';

PROPERTY_VALUE                    INIT_VALUE                       
--------------------------------- ---------------------------------
HH24:MI:SS.FF6 TZH:TZM            HH24:MI:SS.FF6 TZH:TZM 

1 row selected.

gSQL> SELECT PROPERTY_VALUE, INIT_VALUE FROM V$PROPERTY WHERE PROPERTY_NAME LIKE 
'NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT';

PROPERTY_VALUE                    INIT_VALUE                       
--------------------------------- ---------------------------------
YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM

1 row selected.
```

The following is the structure and data of the table to be downloaded.

```
$ cat test.sql
CREATE TABLE TEST ( I1 INTEGER, I2 DATE, I3 TIME WITH TIME ZONE, I4 TIMESTAMP WITH TIME ZONE );

INSERT INTO TEST VALUES ( 1, '1999-12-31', '01:01:01', '1999-12-31 01:01:01.789 -8:00' );
INSERT INTO TEST VALUES ( 2, '2000-01-01', '23:12:12', '2000-01-01 23:12:06.0 +8:00' );
INSERT INTO TEST VALUES ( 3, '2000-12-31', '23:12:12', '2000-12-31 23:12:12.0 -8:00' );
COMMIT;

$ gsql test test
gSQL> SELECT * FROM T1;
I1 I2         I3                     I4                               
-- ---------- ---------------------- ---------------------------------
 1 1999-12-31 01:01:01.000000 +09:00 1999-12-31 01:01:01.789000 -08:00
 2 2000-01-01 23:12:12.000000 +09:00 2000-01-01 23:12:06.000000 +08:00
 3 2000-12-31 23:12:12.000000 +09:00 2000-12-31 23:12:12.000000 -08:00

3 rows selected.
```

The following is the contents of the control file which is created to download the table data.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
```

The data in the table TEST is downloaded to the datafile as follows.

```
$ gloader test test -e -c test.ctl -d test.dat

 COMPLETED IN EXPORTING TABLE: PUBLIC.TEST, 3 RECORDS 

$ ls 
test.ctl test.dat test.log
$ cat test.dat
"1","1999-12-31 00:00:00","01:01:01.000000 +09:00","1999-12-31 01:01:01.789000 -08:00"
"2","2000-01-01 00:00:00","23:12:12.000000 +09:00","2000-01-01 23:12:06.000000 +08:00"
"3","2000-12-31 00:00:00","23:12:12.000000 +09:00","2000-12-31 23:12:12.000000 -08:00"
```

<a id="3b12613e29c76c94"></a>
#### Downloading in Binary File

<a id="cbf3a677d3c97ba6"></a>
##### Simple Download

The following is the structure and data of the table to be downloaded.

```
$ cat test.sql
CREATE TABLE TEST ( I1 INTEGER PRIMARY KEY, I2 VARCHAR(10), I3 VARBINARY(10) );
INSERT INTO TEST VALUES( 1, 'LKH', X'10' );
INSERT INTO TEST VALUES( 2, 'KMM', X'A0' );
INSERT INTO TEST VALUES( 3, 'ksj', X'CD' );
COMMIT;

$ gsql test test
gSQL> SELECT * FROM TEST;

I1 I2  I3
-- --- --
 1 LKH 10
 2 KMM A0
 3 ksj CD

3 rows selected.
```

The following is the contents of the control file which is created to download the table data.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
```

The data in the table TEST is downloaded through gloader as follows.

```
$ gloader test test --export --control test.ctl --data test.dat --format binary

 COMPLETED IN EXPORTING TABLE: PUBLIC.test, 3 RECORDS
```

The following file is generated after executing gloader.

```
$ ls 
test.ctl test.dat test.log
```

> A user can not directly check or edit the binary file.

<a id="57c02843b3d595b4"></a>
##### Complex Download

The following is the structure and data of the table to be downloaded.

```
$ gsql test test
gSQL>\desc TEST

COLUMN_NAME TYPE                        IS_NULLABLE
----------- --------------------------- -----------
I1          NUMBER(10,0)                TRUE       
I2          DATE                        TRUE       
I3          TIME(6) WITH TIME ZONE      TRUE       
I4          TIMESTAMP(6) WITH TIME ZONE TRUE       

gSQL> SELECT COUNT(*) FROM TEST;

COUNT(*)
--------
 1572864

1 row selected.
```

The following is the contents of the control file which is created to download the table data.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
```

- Downloading in a single file

    - The data in the table TEST is downloaded through gloader as follows.

```
$ gloader test test --export --control test.ctl --data test.dat --format binary

loaded 1000 records into PUBLIC.TEST

loaded 2000 records into PUBLIC.TEST

... Ellipsis ... 

loaded 1571000 records into PUBLIC.TEST

loaded 1572000 records into PUBLIC.TEST

 COMPLETED IN EXPORTING TABLE: PUBLIC.TEST, TOTAL 1572864 RECORDS
```

    - The following file is generated after executing gloader.

```
$ ll test.*
-rw-r--r-- 1 test test       71 2014-08-28 12:13 t1.ctl
-rw-r--r-- 1 test test 59930624 2014-08-28 12:49 t1.dat
-rw-r--r-- 1 test test      159 2014-08-28 12:49 t1.log
```

- Downloading in multiple files

    - The data in the table TEST is downloaded through gloader as follows.

```
$ gloader test test --export --control test.ctl --data test.dat --format binary --filesize 31461376

loaded 1000 records into PUBLIC.TEST

loaded 2000 records into PUBLIC.TEST

... Ellipsis ...

loaded 1571000 records into PUBLIC.TEST

loaded 1572000 records into PUBLIC.TEST

 COMPLETED IN EXPORTING TABLE: PUBLIC.TEST, TOTAL 1572864 RECORDS
```

    - The following file is generated after executing gloader.

```
$ ll test.*
-rw-r--r-- 1 test test       71 2014-08-28 12:13 test.ctl
-rw-r--r-- 1 test test 31461376 2014-08-28 13:02 test.dat
-rw-r--r-- 1 test test 28474880 2014-08-28 13:02 test.dat.001
-rw-r--r-- 1 test test      159 2014-08-28 12:49 test.log
```

<a id="38e32e7553dc342c"></a>
##### Array Option

When downloading a binary file, the [--array](#e14c21bfc592d8ad) option can be used to specify the number of rows to bind.  
Because the same array size is used for both downloading and uploading a binary file, the --array option must be specified during the download process.

<a id="224d8a7077b092dc"></a>
### Uploading Data

<a id="ee2d2dae86d7106c"></a>
#### Uploading Text File

<a id="ee99794bf05d2992"></a>
##### Simple Upload

The following is the table to be uploaded.

```
gSQL> \DESC TEST

COLUMN_NAME TYPE                        IS_NULLABLE
----------- --------------------------- -----------
I1          NUMBER(10,0)                TRUE       
I2          DATE                        TRUE       
I3          TIME(6) WITH TIME ZONE      TRUE       
I4          TIMESTAMP(6) WITH TIME ZONE TRUE       

gSQL> SELECT * FROM TEST;

no rows selected.
```

The following is the datafile to be uploaded.

```
$ cat test.dat
1,1999-12-31 00:00:00,01:01:01.000000 +09:00,1999-12-31 01:01:01.789000 -08:00
2,2000-01-01 00:00:00,23:12:12.000000 +09:00,2000-01-01 23:12:06.000000 +08:00
3,2000-12-31 00:00:00,23:12:12.000000 +09:00,2000-12-31 23:12:12.000000 -08:00
```

The datafile is uploaded with gloader and the result is output as follows.

```
$ gloader test test --import --control test.ctl --data test.dat

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3 RECORDS, SUCCEEDED 3 RECORDS 

$ gsql test test

gSQL> select * from test;

I1 I2         I3                     I4                               
-- ---------- ---------------------- ---------------------------------
 1 1999-12-31 01:01:01.000000 +09:00 1999-12-31 01:01:01.789000 -08:00
 2 2000-01-01 23:12:12.000000 +09:00 2000-01-01 23:12:06.000000 +08:00
 3 2000-12-31 23:12:12.000000 +09:00 2000-12-31 23:12:12.000000 -08:00

3 rows selected.
```

<a id="aa3656c61d26d4ed"></a>
##### Whitespace Character

The following is the table to be uploaded.

```
gSQL> \DESC TEST

COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(10) TRUE       
I3          BINARY VARYING(10)    TRUE    

gSQL> SELECT * FROM TEST;

no rows selected.
```

- The datafile downloaded without using OPTIONALLY ENCLOSED BY statement in the control file

    - The datafile is downloaded without using OPTIONALLY ENCLOSED BY statement in the control file as follows. (Refer to [Downloading in Text File](#7e9d8a0eb81cd19a).)

```
$ cat test.dat
1, L K H ,10
2,KIM
MM,A0
3, KIM S 
J ,CD

```

    - The datafile is uploaded with gloader and the result is output as follows. Even though New Line ('`\`n') exists in the data of the second and third records, but a qualifier notifying the start and end of the column data is not set, so it is recognized as a row identifier.

```
$ gloader test test --import --control test.ctl --data test.dat

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 5 RECORDS, SUCCEEDED 3 RECORDS

$ gsql test test

gSQL> select * from test;

I1 I2     I3  
-- ------ ----
 1 L K H  10  
 2 KIM    null
 3 KIM S  null

3 rows selected.
```

- The datafile downloaded using OPTIONALLY ENCLOSED BY statement in the control file

    - The datafile is downloaded by using the OPTIONALLY ENCLOSED BY statement of the control file as follows. (Refer to [Downloading in Text File](#7e9d8a0eb81cd19a).) Differently from the result above, New Line ('`\n`') is treated as a part of data in the result below.

```
$ cat test.dat
"1"," L K H ","10"
"2","KIM
MM","A0"
"3"," KIM S 
J ","CD"
```

    - The datafile is uploaded with gloader and the result is output as follows.

```
$ gloader test test --import --control test.ctl --data test.dat

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 5 RECORDS, SUCCEEDED 3 RECORDS

$ gsql test test

gSQL> select * from test;


I1 I2      I3
-- ------- --
 1  L K H  10
 2 KIM     A0
   MM        
 3  KIM S  CD
   J         

3 rows selected.
```

<a id="b2e3ccd07096863e"></a>
#### Uploading Binary File

<a id="d8797ad4f019e775"></a>
##### Simple Upload

The following is the structure of the table to be uploaded.

```
gSQL> \DESC TEST

COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(10) TRUE       
I3          BINARY VARYING(10)    TRUE    

gSQL> SELECT * FROM TEST;

no rows selected.
```

The following is the content of the control file written to download the table data.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
```

The following is a file to be uploaded with gloader. *test.dat* was already downloaded when [Downloading in Binary File](#3b12613e29c76c94).

```
$ ls 
test.dat
```

The datafile is uploaded to the table TEST and the result is output as follows.

```
$ gloader test test --import --control test.ctl --data test.dat --format binary

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3 RECORDS, SUCCEEDED 3 RECORDS

$ gsql test test
gSQL> SELECT * FROM TEST;

I1 I2  I3
-- --- --
 1 LKH 10
 2 KMM A0
 3 ksj CD

3 rows selected.
```

<a id="82c5d1548f8fee8f"></a>
##### Complex Upload

The following is the structure of the table to be uploaded.

```
gSQL> \DESC TEST

COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(10) TRUE       
I3          BINARY VARYING(10)    TRUE    

gSQL> SELECT * FROM TEST;

no rows selected.
```

The following is the datafile to be uploaded.

```
$ ll test.*
 -rw-r--r-- 1 test test       71 2014-08-28 12:13 test.ctl
 -rw-r--r-- 1 test test 31461376 2014-08-28 13:02 test.dat
 -rw-r--r-- 1 test test 28474880 2014-08-28 13:02 test.dat.001
 -rw-r--r-- 1 test test      159 2014-08-28 12:49 test.log
```

When uploading multiple downloaded files with --filesize, gloader should be separately performed for each datafile.

```
$ gloader test test --import --control test.ctl --data test.dat --format binary
 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 860728 RECORDS, SUCCEEDED 2285000 RECORDS, ERRORED 0 RECORDS 

$ gloader test test --import --control test.ctl --data test.dat.001 --format binary 
 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 860728 RECORDS, SUCCEEDED 860728 RECORDS, ERRORED 0 RECORDS
```

The upload result is as follows.

```
gSQL> select count(*) from test;

COUNT(*)
--------
 3145728

1 row selected.
```

<a id="377458978df1f682"></a>
#### Controlling Upload Unit

The data can be uploaded faster by using the options which is related to performance.  
For more information, refer to [--array](#e14c21bfc592d8ad), [--commit](#cec0e02c0af493d2), [--atomic](#f2b8bd73786c6b3b).

The following is the datafile with approximately 380,000 records.

```
$ ll test.dat
-rw-r--r-- 1 test test 75092480 2014-08-28 15:59 test.dat
```

The following is the control file which is used for uploading.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
```

<a id="26bf36a836dc7976"></a>
##### Array Binding and Commit Cycle

The following gloader command uploads records to be bound in 5,000 unit and uploads records to be committed in 20,000 unit.

```
$ gloader test test --import --control test.ctl --data test.dat --array 5000 --commit 20000

loaded 5000 records into PUBLIC.TEST


loaded 10000 records into PUBLIC.TEST


loaded 15000 records into PUBLIC.TEST

... Ellipsis ...
loaded 3810000 records into PUBLIC.TEST


loaded 3815000 records into PUBLIC.TEST


loaded 3818244 records into PUBLIC.TEST

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3818243 RECORDS, SUCCEEDED 3818243 RECORDS
```

The following is the result of executing gloader.

```
gSQL> SELECT I1, I2, I3 FROM TEST FETCH 3;
I1 I2 I3
-- ------- --
1 L K H 10
2 KIM A0
3 KIM S CD
3 rows selected.
gSQL> SELECT COUNT(*) FROM TEST;
COUNT(*)
--------
3818246
1 row selected.
```

<a id="c34acaa5ba1c2370"></a>
##### Array Binding and Atomic Option

The following gloader commands uploads records to be bound in 5000 unit with atomic INSERT, and 1,000 records are failed.

```
$ gloader test test --import --control test.ctl --data test.dat --array 5000 --atomic

loaded 5000 records into PUBLIC.TEST


loaded 10000 records into PUBLIC.TEST


loaded 15000 records into PUBLIC.TEST

... Ellipsis ...
loaded 38175000 records into PUBLIC.TEST

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3818243 RECORDS, SUCCEEDED 3817243 RECORDS
```

The following is the result of executing gloader.

```
gSQL> SELECT I1, I2, I3 FROM TEST FETCH 3;
I1 I2 I3
-- ------- --
1 L K H 10
2 KIM A0
3 KIM S CD
3 rows selected.
gSQL> SELECT COUNT(*) FROM TEST;
COUNT(*)
--------
3817243
1 row selected.
```

The following is the result for the cause of the upload failure and they are recorded in the log file. The upload is failed because the non-numeric data is stored in the first column of the first record.

```
$ cat test.log
Err Rec(1) Col(1): 22018(12006): data value is not a numeric literal
Err Rec(1) Col(-1): HY000(19041): Failed to atomic execution
Err Rec(1001) Col(1): 22018(12006): data value is not a numeric literal
Err Rec(1001) Col(-1): HY000(19041): Failed to atomic execution
COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3818243 RECORDS, SUCCEEDED 3817243 RECORDS [ Start Time: 2014-8-28 16:46:42 End Time: 2014-8-28 16:46:52 Taken Time: 10084582 micro-sec ]
```

The following is the result of the records which failed to upload and they are recorded in the bad file. 1000 records were stored because it is uploaded in 500 array units.

```
"s1"," L K H ","10"
"2","KIM","A0"
"3"," KIM S J ","CD"
... Ellipsis ...
```

> Array, commit options do not affect the execution result, but success or failure of INSERT in the atomic operation is treated in an array unit, so if a record is failed to upload, all records in a unit to which the records belong are treated as INSERT failure.  
> The cause of the first failed records of the array is recorded in the log file and the causes for failed record later is not recorded.

<a id="c6d0dda6d43ad821"></a>
#### Parallel Upload

gloader improves the performance of GOLDILOCKS by dividing the operation into parts and uploading them in thread unit. (Refer to [--parallel](#43906e8ce54e7aab).)

The following is the datafile with approximately 380,000 records.

```
$ ll test.dat
-rw-r--r-- 1 test test 75092480 2014-08-28 15:59 test.dat
```

The following is the control file which is used for uploading.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
```

The following gloader commands uploads records which is bound to a thread performing four uploads. It is uploaded in 5000 unit with INSERT, and 100 records are failed.

```
$ gloader test test --import --control test.ctl --data test.dat --array 5000 --parallel 4

loaded 5000 records into PUBLIC.TEST


loaded 10000 records into PUBLIC.TEST


loaded 15000 records into PUBLIC.TEST

... Ellipsis ...
loaded 3810000 records into PUBLIC.TEST

loaded 3815000 records into PUBLIC.TEST

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3818243 RECORDS, SUCCEEDED 3818143 RECORDS
```

The following is the result of executing gloader.

```
gSQL> SELECT I1, I2, I3 FROM TEST FETCH 3;
I1 I2 I3
-- ------- --
1 L K H 10
2 KIM A0
3 KIM S CD
3 rows selected.
gSQL> SELECT COUNT(*) FROM TEST;
COUNT(*)
--------
3818143
1 row selected.
```

The cause of failure during the upload is recorded in the log file as follows.

```
$ cat test.log
Err Rec(1) Col(1): 22018(12006): data value is not a numeric literal
Err Rec(3) Col(1): 22018(12006): data value is not a numeric literal
Err Rec(5) Col(1): 22018(12006): data value is not a numeric literal
... Ellipsis ...
Err Rec(1001) Col(1): 22018(12006): data value is not a numeric literal
... Ellipsis ...
COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3818243 RECORDS, SUCCEEDED 3818143 RECORDS [ Start Time: 2014-8-28 16:46:42 End Time: 2014-8-28 16:46:52 Taken Time: 10084582 micro-sec ]
```

The following is a result of failed records recorded on the bad file during the upload. 100 records are stored.

```
"s1"," L K H ","10"
"s2","KIM","A0"
"s3"," KIM S J ","CD"
... Ellipsis ...
```

> When uploading the data with multiple threads, the records in which errors occur after INSERT are stored in the log file and bad file. In this case, the order of records may not be the same as the order in the data files.

<a id="b5eafd354f0f909d"></a>
### Troubleshooting for Uploading

The record upload failure may occur by various causes. The failed record is stored in the bad file, and the information about the cause of failure is stored in the log file.

<a id="cc117a44e3e60bda"></a>
#### Failure due to Redundant Constraint

<a id="8131cf276b171ecb"></a>
##### The redundant data is already in the constrained table to be uploaded. (primary key or unique index)

The following is the structure of the table to be uploaded.

```
gSQL>\desc T1

COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(10) TRUE       
I3          BINARY VARYING(10)    TRUE    

gSQL> SELECT * FROM T1;

I1 I2  I3
-- --- --
 1 LKH 10
 2 KMM A0
 3 ksj CD

3 rows selected.
```

The following is the datafile to be uploaded.

```
$ cat t1.dat
"1","LKH"
"4","SOS"
"5","OKO"
```

The following are the upload result by using gloader, and the created log file and bad file.  
The upload is failed because the record violated a primary key constraint.

```
$ gloader test test -i -c t1.ctl -d t1.dat

 COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 3 RECORDS, SUCCEEDED 2 RECORDS 
$
$ cat t1.log
Err Rec(1) Col(-1): 40002(16057): unique constraint (PUBLIC.T1_PRIMARY_KEY) violated
COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 3 RECORDS, SUCCEEDED 2 RECORDS [ Start Time: 2014-8-26 16:19:51 End Time: 2014-8-26 16:19:51 Taken Time: 15455 micro-sec ]
$
$ cat t1.bad
"1","LKH"
```

<a id="328fdc6996cd6e19"></a>
#### Failure due to Date/time Format

The format can be set for the data type such as DATE, TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, and it may cause the failure of upload using gloader.

The following is the table to be uploaded.

```
gSQL> \DESC T1

COLUMN_NAME TYPE IS_NULLABLE
----------- --------------------------- -----------
I1 NUMBER(10,0) TRUE
I2 TIMESTAMP(6) WITH TIME ZONE TRUE

gSQL> SELECT * FROM T1;
no rows selected.
```

The format of the TIMESTAMP WITH TIME ZONE on the server is as follows.

```
gSQL> SELECT PROPERTY_VALUE, INIT_VALUE FROM V$PROPERTY WHERE PROPERTY_NAME LIKE 'NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT';

PROPERTY_VALUE                    INIT_VALUE                       
--------------------------------- ---------------------------------
YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM
```

The following is the datafile to be uploaded.

```
$ cat t1.dat
"4","20000108 00:00:00"
"5","20000108 04:05:06"
"6","20000108 04:05:06"
```

The following is the result of executing upload by using gloader.

```
$ gloader test test -i -c t1.ctl -d t1.dat
 
 COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 3 RECORDS, SUCCEEDED 0 RECORDS
```

The cause and records of upload failure are stored in the log file and the bad file as follows.

```
$ cat t1.log
Err Rec(1) Col(2): HY000(12136): literal does not match format string
Err Rec(2) Col(2): HY000(12136): literal does not match format string
Err Rec(3) Col(2): HY000(12136): literal does not match format string
COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 3 RECORDS, SUCCEEDED 0 RECORDS [ Start Time: 2014-8-27 13:56:29 End Time: 2014-8-27 13:56:29 Taken Time: 20670 micro-sec ]

$ cat t1.bad 
"4","20000108 00:00:00"
"5","20000108 04:05:06"
"6","20000108 04:05:06"
```

<a id="4c8943b5ef60d474"></a>
##### Troubleshooting

The problem occurs when the data type format of the datafile and that of the data used on the server are different. The data type format of the datafile should be set to solve the problem. In this case, .odbc.ini is used.

The data type format is set in .odbc.ini file as follows.

```
$ cat .odbc.ini
[GOLDILOCKS]
HOST = 127.0.0.1
PORT = 21123
DATE_FORMAT = YYYYMMDD
TIME_FORMAT = HH24MISS
TIME_WITH_TIME_ZONE_FORMAT = HH24MISS TZHTZM
TIMESTAMP_FORMAT = YYYYMMDD HHMISS
TIMESTAMP_WITH_TIME_ZONE_FORMAT = YYYYMMDD HH:MI:SS
```

The following is the result of setting .odbc.ini and performing gloader again.

```
$ gloader test test -i -c t1.ctl -d t1.dat

 COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 3 RECORDS, SUCCEEDED 3 RECORDS
```


> 
> - The data type format set in .odbc.ini is applied to the entire column, and it can not be separately set.
> - If the data type format is set in .odbc.ini, it is also applied when downloading to gloader.
> 

<a id="dc3c6066222619fd"></a>
#### Failure Due to Lack of Capacity

gloader is performed and failed as follows.

```
$ gloader test test -i -c t1.ctl -d t2.dat

loaded 4000 records into PUBLIC.T1
COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 4200 RECORDS, SUCCEEDED 0 RECORDS
```

It is failed due to lack of the space for datafile in the tablespace.

```
$ cat t1.log
Err Rec(1) Col(-1): HY000(14015): there is no extendible datafile in tablespace 'MEM_DATA_TBS'
Err Rec(2) Col(-1): HY000(14015): there is no extendible datafile in tablespace 'MEM_DATA_TBS'
... Ellipsis ...
COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 4200 RECORDS, SUCCEEDED 0 RECORDS [ Start Time: 2014-8-27 15:7:28 End Time: 2014-8-27 15:7:29 Taken Time: 317885 micro-sec ]
```

<a id="9c43894f1cc1184c"></a>
##### Troubleshooting

The datafile of a tablespace should be extended or added to solve the problem.   
For more information, refer to [ALTER TABLESPACE](../part-03-sql-manual/18-sql-references-a-b.md#4e7cd5f52e3f3a17).

<a id="5250981d28561fdf"></a>
#### Datafile Analysis Failure

The field terminator, the qualifier, and the line terminator described in the control file may be different in the text datafile because of misuse.

The following is the structure of the table object to be uploaded.

```
gSQL>\desc T1
COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(10) TRUE       
I3          BINARY VARYING(10)    TRUE
```

The following is the control file to be uploaded.

```
$ cat t1.ctl
TABLE  T1
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
```

The following is the datafile to be uploaded.

```
$ cat t1.dat
'1',"LKH","aa"
"2","SOS"","aa"
"5","OKO","00"
```

The following is the result of executing upload by using gloader.

```
$ gloader test test --import --control t1.ctl --data t1.dat

 COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 3 RECORDS, SUCCEEDED 1 RECORDS
```

The cause and records of upload failure are as follows.

```
$ cat t1.log
Err Rec(1) Col(1): 22018(12006): data value is not a numeric literal
COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3 RECORDS, SUCCEEDED 1 RECORDS [ Start Time: 2014-8-28 18:6:13 End Time: 2014-8-28 18:6:13 Taken Time: 18679 micro-sec ]
$
$ cat t1.bad
"2","SOS"","aa"
'1',"LKH","aa"
```

<a id="65e360f13cfb8d14"></a>
##### Troubleshooting

The records fail to analyze the data due to qualifier or delimiter which are used improperly. Therefore, to solve this problem, the field terminator, the qualifier and the delimiter in the control file and the datafile should be checked, then the datafile should be edited based on the records of the bad file.

> The records which are failed to parse in the data analysis process are stored in the bad file, not in the log file.

<a id="4d16c4b753e0290c"></a>
#### Uploading to Another Database Whose Character Set Is Different

Adjusting the column size may be required when downloading/ uploading data in binary type between databases whose character sets are different one another.

The following is the structure of the table object to be uploaded.

```
gSQL>\desc T1
COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(36) TRUE
```

The following is the table data, and it is a VARCHAR type, its size is 36 and is completely filled.

```
SELECT * FROM T1;

I1    I2
---- ------------------------------------ 
   1 일이삼사오육칠팔구십일이삼사오육칠팔
```

The following error occurs when downloading data above from UHC database then uploading to UTF8 database which has the same schema.

```
$ gloader test test -i -f binary -T T1 -d t1.dup

ERR-HY000(42023): byte length of data greater than column length.

ERROR: FAILED TO IMPORT TABLE PUBLIC.T1
```

<a id="9e7fdaf20beb764a"></a>
##### Troubleshooting

The data upload succeeds when adjusting the length of column I2 as follows.  
Declare I2 as VARCHAR(18 CHAR), or declare I2 as VARCAR(54) size.

```
gSQL>\desc T1
COLUMN_NAME TYPE                       IS_NULLABLE
----------- -------------------------- -----------
I1          NUMBER(10,0)               TRUE
I2          CHARACTER VARYING(18 CHAR) TRUE
```

```
gSQL>\desc T1
COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(54) TRUE
```

<a id="6232e22e3f4f912c"></a>
## Control File Syntax

```
TABLE table_name [(column_description)]
FIELDS TERMINATED BY 'Field Terminator'
[OPTIONALLY ENCLOSED BY 'Open Qualifier' [AND 'Close Qualifier']]
[LINES TERMINATED BY 'Line Terminator']
[Characterset characterset_name]
[RTRIM [ON|OFF]]
[LTRIM [ON|OFF]]
[WHERE="conditional statement"]
```

> A control file describes only one table. Therefore, each item above should be described in the control file only once, and if it is described redundantly, then the control parsing error occurs.

<a id="742f4a07b0c4eb65"></a>
### CHARACTERSET

<a id="a745002e29d15bf8"></a>
#### Syntax

```
CHARACTERSET characterset_name
```

<a id="c9401cf5bb205eac"></a>
#### Description

It refers to the character set of the data file to be downloaded or uploaded.  
If the character set is not explicitly specified, the client character set is determined based on the following priority: the CHARSET of the ODBC data source, the GOLDILOCKS_NLS_CHARACTERSET environment variable, and the system locale settings.  
This clause does not apply when downloading data in binary format; it applies only when uploading.

<a id="f1ee904ec35a24e1"></a>
#### Example

The following is an example of which the character set of the datafile to be uploaded or downloaded is the ASCII code.

```
% cat sample.ctl
CHARACTERSET ASCII
```

<a id="a036d2242c09e35e"></a>
### TABLE

<a id="df6ead1e173ef13e"></a>
#### Syntax

```
TABLE <table_name> [( <column_description> )]

<table_name> ::=
    [schema_name.]table_name[@domain_name]
<column_description> ::=
    column_name [<column_bypass>] (, ... )

<column_bypass> ::=
    (ADD | SKIP) [<column_bypass_value>]

<column_bypass_value> ::=
      empty
    | DEFAULT
    | NULL
    | CONSTANT <quote_string>
    | SEQUENCE sequence_name (NEXTVAL | CURRVAL)
```

<a id="70f9e8d093cf22e5"></a>
#### Description

<a id="a907f7a7ceb550df"></a>
##### Table

It specifies the name of table to which upload or download the data, or specifies the schema name  to which the table belongs, or the domain name.  
The domain name can be used only for data download, and it downloads only the data of the corresponding member.  
The string or double-quoted (") string is used in the table name.  
If the table name is given as the command row argument in gloader as well, then the value of the command row argument takes precedence over the value in the control file.

<a id="85cbe0f5f449e500"></a>
##### Column

Basically, it can upload or download data if the table name exists even though the column is not specified.  
It can select the column to upload or download by specifying the column in the text mode.   
It can change the sequence of the columns or exclude the specific column by specifying the column. However, all columns should be specified even when a column is excluded. Specify SKIP and ADD after the column name to exclude the column.

<a id="eca9fceef749e052"></a>
###### **SKIP/ADD**

- **SKIP:** 

- It excludes the corresponding column or substitutes the column with the specific data when downloading the data.
- It substitutes the corresponding column's data with NULL, a constant, DEFAULT or SEQUENCE when uploading the data. The data field mapped to the corresponding column is also ignored.

- **ADD:** 

- It is not available when downloading the data.
- It substitutes the corresponding column's data with NULL, a constant, DEFAULT or SEQUENCE when uploading the data. The data field mapped to the corresponding column is mapped to the next column.

<a id="401bbb46d130ae1a"></a>
###### **VALUE**

- **empty:** 

If it is empty after SKIP or ADD, the column is excluded when downloading, and NULL or DEFAULT, the column's default value, is created when uploading.

- **NULL:** 

The column value is empty when downloading. The column value is created as NULL when uploading.

- **DEFAULT:** 

SKIP for column is ignored so the column data is downloaded when downloading. DEFAULT value of the column is created when uploading.

- **CONSTANT:** 

The column data is substituted with a constant and downloaded when downloading. The column value is substituted with a constant and created when uploading.

- **SEQUENCE:** 

The column data is substituted with SEQUENCE value and downloaded when downloading. The column value is substituted with SEQUENCE value and created when uploading.

<a id="768c073b244ecd14"></a>
#### Examples

<a id="0c1f429c56bc4ac9"></a>
##### Table

The following is an example of specifying only the table name.

```
% cat sample.ctl
TABLE lineitem
```

The following is an example of specifying the schema PUBLIC and the table name. It has the same meaning as the example above.

```
% cat sample.ctl
TABLE PUBLIC.lineitem
```

The following is an example of specifying the schema PUBLIC and the table name of G1N1 member. It has the same meaning as the example above.

```
% cat sample.ctl
TABLE PUBLIC.lineitem@G1N1
```

The following is an example of specifying the table name created by the delimited identifier.

```
gSQL> CREATE TABLE "Tab*&^" ( id INTEGER );
```

```
% cat sample.ctl
TABLE "Tab*&^"
```

<a id="f3d082ab39518808"></a>
##### Column

The following is a sample table and data file for usage.

```
gSQL> \desc test

COLUMN_NAME TYPE         IS_NULLABLE
----------- ------------ -----------
C1          NUMBER(10,0) TRUE       
C2          NUMBER(10,0) TRUE       
C3          NUMBER(10,0) TRUE
```

```
% cat sample.dat
1,2,3
11,22,33
```

The following is an example of describing a column.

```
% cat sample.ctl
TABLE test
(
    c1,
    c2,
    c3
)
```

The following is an example of uploading data excluding column C2, and its result.

```
% cat sample.ctl
TABLE test
(
    c1,
    c2 SKIP,
    c3
)

% gloader test test -i -c sample.ctl -d sample.dat
```

The value of column C2 is created as NULL, the DEFAULT value of C2, because only SKIP keyword was used.

```
gSQL> SELECT * FROM TEST;

C1   C2 C3
-- ---- --
 1 null  3
11 null 33

2 rows selected.
```

The following is an example of using ADD keyword instead of SKIP in the example above, and its result.

```
% cat sample.ctl
TABLE test
(
    c1,
    c2 SKIP,
    c3
)

% gloader test test -i -c sample.ctl -d sample.dat
```

The field mapped to column C2 in the data file is mapped to column C3.

```
gSQL> SELECT * FROM TEST;

C1   C2 C3
-- ---- --
 1 null  2
11 null 22

2 rows selected.
```

The following is an example of downloading data excluding column C2, and its result.

```
% cat sample.ctl
TABLE test
(
    c1,
    c2 SKIP,
    c3
)

gSQL> SELECT * FROM TEST;

C1 C2 C3
-- -- --
 1  2  3
11 22 33

2 rows selected.

% gloader test test -e -c sample.ctl -d down_sample.dat
```

The value of column C2 is created as NULL, the DEFAULT value of C2, because only SKIP keyword was used.

```
$ cat down_sample.dat
1,,3
11,,33
```

The following is an example of using CONSTANT while SKIPping column C2.

```
% cat sample.ctl
TABLE test
(
    c1,
    c2 SKIP CONSTANT '-2',
    c3
)

% gloader test test -i -c sample.ctl -d sample.dat
```

-2 is created as the value of column C2.

```
gSQL> SELECT * FROM TEST;

C1 C2 C3
-- -- --
 1 -2  3
11 -2 33

2 rows selected.
```

The following is an example of using SEQUENCE while SKIPping column C2.

```
% cat sample.ctl
TABLE test
(
    c1,
    c2 SKIP SEQUENCE MY_SEQ NEXTVAL,
    c3
)

gSQL> SELECT MY_SEQ.CURRVAL FROM DUAL;

CURRVAL
-------
      4

1 row selected.

% gloader test test -i -c sample.ctl -d sample.dat
```

NEXTVAL of MY_SEQ is created as the value of column C2.

```
gSQL> SELECT * FROM TEST;

C1 C2 C3
-- -- --
 1  4  3
11  5 33

2 rows selected.
```

<a id="fb04e49b65046373"></a>
### FIELDS TERMINATED BY

<a id="6bc9ceeeadea3dc8"></a>
#### Syntax

```
FIELDS TERMINATED BY 'Field Terminator'
```

<a id="d4f91d15ab16f678"></a>
#### Description

The field terminator is used as a delimiter between columns in the record data of the data file. Setting the field terminator in the control file can not be omitted.  
The field terminator can be set with one or more strings, and should not be redundant with a qualifier or line terminator, and it should not use the subset string.  
There is not any constraintfor the string to be set as a field terminator. However, `\` or % should be added to in front of each n, t, r when setting NEW LINE or TAB, CARRIAGE RETURN character.  
If the field terminator is given as the command row argument in gloader as well, then the value of the command row argument takes precedence over the value in the control file.

<a id="6295822fa736839a"></a>
#### Example

The following is an example of setting the field terminator as COMMA and NEW LINE.

```
% cat sample.ctl

FIELDS TERMINATED BY ',\n'
```

```
% cat sample.ctl

FIELDS TERMINATED BY ',%n'
```

<a id="6e2d051e9d07f7d5"></a>
### OPTIONALLY ENCLOSED BY

<a id="f59d6019ed5ee901"></a>
#### Syntax

```
OPTIONALLY ENCLOSED BY 'Open Qualifier' [AND 'Close Qualifier']
```

<a id="bd58ae1bca8e2277"></a>
#### Description

Qualifier is used as a delimiter to represent the start and end of the column.  
Qualifier is a single character, and the first qualifier is a open qualifier, the last qualifier is a close qualifier. The same characters can be used to set an open qualifier and a close qualifier, or the different characters can be used to represent the start and end of the column.  
Characters set as a qualifier can not be used in a field terminator nor in a line terminator.  
If a close qualifier literally belongs to a column data, two close qualifiers are used to represent a single valid data.  
If an open qualifier is set omitting a close qualifier, then characters the same as those in an open qualifier is set in a close qualifier.

If OPTIONALLY ENCLOSED BY statement does not exist, the column data is distinguished by the field terminator.  
If the qualifier is given as the command row argument in gloader as well, then the value of the command row argument takes precedence over the value in the control file.

> If OPTIONALLY ENCLOSED BY statement does not exist, the results of the uploading and downloading data may be different. (Refer to [Troubleshooting Uploading](#b5eafd354f0f909d).)

<a id="5fc3ad65155b6394"></a>
#### Example

The following is an example of using double quotes (") and a single quote (') as a open qualifier and a close qualifier each.

```
% cat sample.ctl
OPTIONALLY ENCLOSED BY '"' AND "'"
```

<a id="74eb2544e4baf879"></a>
### LINES TERMINATED BY

<a id="cc8cb7f07de8c467"></a>
#### Syntax

```
LINES TERMINATED BY 'Line Terminator'
```

The line terminator is used as a delimiter between records in the data file.  
The line terminator can be set with one or more strings, and should not be redundant with a qualifier or a field terminator, and it should not use the subset string.

When omitting the line terminator setting, then  NEW LINE ('`\`n' or '%n') is used by default.   
If the line terminator is given as the command row argument in gloader as well, then the value of thecommand row argument takes precedence over the value in the control file.

<a id="c6227b046b7833e4"></a>
#### Description

> • Differently from Unix, CARRIAGE RETURN and NEW LINE are written together instead of a single NEW LINE in the data file exported from Windows OS. When importing data by using this data file, LINES TERMINATED BY in the control file should be explicitly set like as '`\`r`\`n' so that the data is normally imported.  
>   
> • It is recommended to set a field terminator and a line terminator with a different string each. The more mutual string including the first character exist the poorer the import performance due to the internal comparing. In other words, when a field terminator and a line terminator are set with different strings each, then the shorter the string the better the performnace.

<a id="0e4f45f5de7d64b0"></a>
#### Example

The following is an example of using '^^`\`t`\`r`\`n' as a line terminator

```
% cat sample.ctl

LINES TERMINATED BY '^^\t\r\n'
```

<a id="604e2e08c0e980e0"></a>
### LTRIM

<a id="32306957f0cabaae"></a>
#### Syntax

```
LTRIM ON|OFF
```

<a id="c08118beca6df112"></a>
#### Description

It determines a left trim.  
The default value is OFF, and when it is set to OFF, then the left WHITESPACE is considered data.  
When it is set to ON, then the left WHITESPACE is ignored.

> OPTIONALLY ENCLOSED BY is applied only when the syntax does not exist.  
> If OPTIONALLY ENCLOSED BY is used and the column is enclosed with delimiters in the data file, then RTRIM and LTRIM is OFF.

<a id="4ee8e2197c996b59"></a>
#### Example

The following is an example of setting LTRIM to ON.

```
% cat sample.ctl
LTRIM ON
```

<a id="c1d475a54ddc0dee"></a>
### RTRIM

<a id="ab7357bc99ccb3ab"></a>
#### Syntax

```
RTRIM ON|OFF
```

<a id="0b5608000b893814"></a>
#### Description

It determines a right trim.  
The default value is OFF, and when it is set to OFF, then the right WHITESPACE is considered data.  
When it is set to ON, then the right WHITESPACE is ignored.

> OPTIONALLY ENCLOSED BY is applied only when the syntax does not exist.  
> If OPTIONALLY ENCLOSED BY is used and the column is enclosed with delimiters in the data file, then RTRIM and LTRIM is OFF.

<a id="043871e2ea0eb7e4"></a>
#### Example

The following is an example of setting RTRIM to ON.

```
% cat sample.ctl
RTRIM ON
```

<a id="dceb8569241944c7"></a>
### WHERE

<a id="2c672e6645fc86c2"></a>
#### Syntax

```
WHERE="conditional_statement"
```

<a id="326d97146d142057"></a>
#### Description

It uses a conditional clause when downloading data.

<a id="195ae112c885a4bd"></a>
#### Example

The following is an example of using WHERE.

```
% cat sample.ctl
WHERE="I2 > 3"
```

<a id="4e9874d5f18dae64"></a>
## gloader Argument References

<a id="ad7eafe83ca4ddea"></a>
### Usage

```
$ gloader --help
Usage 
    gloader user password mode data [control] [format] [options]

    user                user name
    password            password

mode: gloader's mode. 
  --export              export data
  --import              import data

data:
  --data                data file

options:
  --control                       control file
  --format                        file format(text|binary, Default text)
  --log                           log file
  --bad                           bad file
  --dsn                           dsn string
  --array                         number of rows in bind array(Default 1000)
  --filesize                      max file size
  --commit                        number of commit unit(Default 5000)
  --comment                       commenting on commit
  --atomic                        use atomic function
  --parallel                      use parallel in import
  --propagation                   enabling or disabling a redo log propagation(ON|OFF)
  --errors                        number of error count to allow(Default 100)
  --AsTIMESTAMP                   bind DATE as TIMESTAMP
  --buffered                      buffered disk io(Default direct io)
  --tablename                     [schema_name.]table_name[@domain_name]
  --fieldterm                     field terminator
  --lineterm                      line terminator
  --qualifier                     qualifier(column data encloser)
  --where                         export only rows selected by given WHERE condition
  --group-id                      importing distributed data by group id using global connections in a clustered environment
  --append                        action before data importing (APPEND|REPLACE|TRUNCATE, Default APPEND)
  --skip                          number of records to skip
  --no-copyright                  suppresses the display of the banner
  --silent                        suppresses the display of the result message
  --merge                         import data using new space (EXTENT|SEGMENT, Default NONE) 
  --skip_index_maintenance        index maintenance option to import data using new space
  --nologging                     nologging append insert option to import data using new space
  --help                          print help message
```

<a id="6b28715d0892222f"></a>
### Mandatory Argument

The arguments are entered in an order of username and password to connect to the database.  
gloader operation mode, control file, datafile are entered as arguments.

<a id="24bc51ab2b44e846"></a>
| Argument | Description |
| --- | --- |
| user_name | It is the user name. The maximum length of user name is 128. |
| password | It is password. The maximum length of password is 128. |

<a id="ea8e029e401ee92c"></a>
#### --export

<a id="ee0e766988922cd9"></a>
##### Description

It specifies for gloader to download the data in the database.

<a id="4e9142ee56e58c83"></a>
##### Example

```
$ gloader test test --export -c sample.ctl -d sample.dat
```

<a id="77616ab88707e4eb"></a>
#### --import

<a id="f78f2d7ffa781f9c"></a>
##### Description

It specifies for gloader to upload the data in the database.

<a id="0f192b0581299f3c"></a>
##### Example

```
$ gloader test test --import -c sample.ctl -d sample.dat
```

<a id="4e17396137c077f5"></a>
#### --control

<a id="fae5edaf4586afaa"></a>
##### Description

It specifies the control file path.

If --tablename is given as an argument, the control file can be omitted. The table name is mandatory to execute gloader, so the table name should be given via a control file or an argument. If the table name is not given as an argument, TABLE item should be set via a control file.

When a control file is omitted, a field terminator, a qualifier, a line terminator can be given as an argument. If these delimiters are not given as an argument, then delimiters in CSV form is used by default.

<a id="3e0b3f84a90acd4f"></a>
##### Example

The following is an example of using a control file whose name is sample.ctl.

```
$ gloader test test -i --control sample.ctl -d sample.dat
```

<a id="6dc548620b0054c9"></a>
#### --data

<a id="4d606359cc765d69"></a>
##### Description

It specifies the data file path to download or upload.

<a id="14f19299d967e8fc"></a>
##### Example

The following is an example of uploading a control file whose name is sample.dat.

```
$ gloader test test -i -c sample.ctl --data sample.dat
```

<a id="5ce4a400cb576dcc"></a>
### Optional Argument

<a id="8885b980b6d7c4ec"></a>
#### --tablename

<a id="c108d401d93b3ffa"></a>
##### Description

It specifies the table name in [Schemaname.]Tablename[@domain_name] form.

The table name should be given via setting TABLE of an argument or a control file. In other words, if a control file is omitted, the table name argument is mandatory.  
If a tablename argument is given when TABLE item of a control file is set, then argument value takes precedence over the value in the control file.

<a id="7f2ee4496d5a93b9"></a>
##### Example

The following is an example of uploading data in CSV form by giving a tablename argument because the control file argument is omitted

```
$ gloader test test -i --tablename PUBLIC.T1 --data sample.dat
```

The following is an argument of omitting a tablename argument because TABLE item is omitted in the control file.

```
$ cat sample.ctl | grep TABLE
  TABLE T1
$ gloader test test -i -c sample.ctl --data sample.dat
```

<a id="09d4ce8da84ac618"></a>
#### --format

<a id="e1ea87d0cd83e4f5"></a>
##### Description

It specifies the datafile format.  
The datafile format may be text or binary, and the default value is text when the format is not set.

<a id="302c5047bb00d582"></a>
##### Example

The following is an example of downloading the data to sample.dat in binary form.

```
$ gloader test test --export --control sample.ctl --data sample.dat --format binary
```

The following are sample.dat and sample.log which are created after executing gloader as above.

```
$ ls
sample.ctl sample.dat sample.log
```

<a id="ba18ecbe6ef6cda0"></a>
#### --log

<a id="998705721d28683d"></a>
##### Description

It specifies the logfile path.  
gloader records the error and results occurred during the execution.  
If the file name is not specified, the name is created the same as the datafile by changing its extension to log.

<a id="4d2d4dd9a743151e"></a>
##### Example

The following is an example of when the name of the log file is specified by using --log option.

```
$ gloader test test --export --control sample.ctl --data sample.dat --log SAMPLE.log
```

The following are sample.dat, SAMPLE.log which are created after executing gloader as above.

```
$ ls
sample.ctl sample.dat SAMPLE.log
```

The following is an example of when the name of the log file is not specified by using --log option.

```
$ gloader test test --export --control sample.ctl --data sample.dat
```

The following are sample.dat, sample.log which are created after executing gloader as above.

```
$ ls
sample.ctl sample.dat sample.log
```

<a id="aa4acd39c66d55e4"></a>
#### --bad

<a id="8cadd098293bd872"></a>
##### Description

It specifies the bad file path.  
It is valid only when gloader performs the import operation. Rows which can not be uploaded due to an error are stored in the bad file.  
If the file name is not specified, the name is created the same as the datafile by changing its extension to bad.

<a id="9bf85cc857db9e56"></a>
##### Example

The following is an example of when the name of the bad file is specified by using --bad option.

```
$ gloader test test --import --control sample.ctl --data sample.dat --bad SAMPLE.bad
```

The following are sample.dat, sample.log, SAMPLE.bad which are created after executing gloader as above.

```
$ ls
SAMPLE.bad sample.ctl sample.dat sample.log
```

The following is an example of when the name of the bad file is not specified by using --bad option.

```
$ gloader test test --export --control sample.ctl --data sample.dat
```

The following are sample.dat, sample.log, sample.bad which are created after executing gloader as above.

```
$ ls
sample.bad sample.ctl sample.dat sample.log
```

<a id="cd7a2295234e3f58"></a>
#### --dsn

<a id="3269bfa83bb5088d"></a>
##### Description

It is the dsn string. The maximum length is 128.  
It is used to specify the format of the time-related data type represented in the data file to be downloaded or uploaded.  
It is used to specify the server when using gloadernet in the Client/ Server (C/S) environment.  
For more information, refer to [odbc.ini File](../part-05-developer-manual/34-odbc.md#a37d4e15f0c71e92).

<a id="3ae430dc48518fd1"></a>
##### Example

The following is an example of .odbc.ini described to use --dsn option.

```
$ cat .odbc.ini
[GOLDILOCKS]
HOST = 127.0.0.1
PORT = 21123
DATE_FORMAT = YYYYMMDD
TIME_FORMAT = HH24MISS
TIME_WITH_TIME_ZONE_FORMAT = HH24MISS TZHTZM
TIMESTAMP_FORMAT = YYYYMMDD HHMISS
TIMESTAMP_WITH_TIME_ZONE_FORMAT = YYYYMMDD HH:MI:SS
```

The following is an example of uploading the data to the goldilocks server by using --dsn option.

```
$ gloadernet test test --dsn goldilocks --import --control sample.ctl --data sample.dat
```

The following is an example of defining the format of time-related data type of the data file by using --dsn option, and then downloading data.

```
$ gloader test test --dsn goldilocks --export --control sample.ctl --data sample.dat
```

For more information, refer to [Failure due to date/time format](#328fdc6996cd6e19).

<a id="e14c21bfc592d8ad"></a>
#### --array

<a id="a0e8a251f3fc7ef2"></a>
##### Description

It specifies the number of rows to bind when importing data.  
Memory usage increases proportionally with the array size, and if the option is not specified, the default is 1,000 rows for text mode and 40 rows for binary mode.  
This option applies only during upload in text mode and only during download in binary mode.

<a id="135365c9e76058ac"></a>
##### Example

The following is an example of uploading a text data file in units of 2,000 records:

```
$ gloader test test --import --control sample.ctl --data sample.dat --array 2000
```

The following is an example of downloading a binary data file in units of 2,000 records:

```
$ gloader test test --export --format binary --control sample.ctl --data sample.dup --array 2000
```

<a id="29073bdb770f5f16"></a>
#### --filesize

<a id="9b96a698c2038087"></a>
##### Description

The maximum size of the file can be set when gloader downloads the data. If the amount of data exceeds the maximum size, the file is generated by adding the permutation number to the file extension.  
If not specified, the maximum file size is unlimited, and the minimum is 31,461,376 (30 Mbytes).  
The option is valid only for the binary type data file.

<a id="3655b6f47beb3562"></a>
##### Example

The following is an example of executing the commands, then the file size exceeds the specified maximum, so new files are generated as results.

```
$ gloader test test --export --control sample.ctl --data sample.dat --filesize 31461376
```

```
$ls -al
-rw-r--r-- 1 test test 31461376 sample.dat
-rw-r--r-- 1 test test 31461376 sample.dat.001
-rw-r--r-- 1 test test  6715392 sample.dat.002
```

<a id="cec0e02c0af493d2"></a>
#### --commit

<a id="b43765be58abcef2"></a>
##### Description

While gloader uploads the data, the transaction is in the no commit state. The commit cycle may be set by using --commit option.  
If not set, the default value is 5,000 (rows).

<a id="30fc6ef284527197"></a>
##### Example

The following is an example of using --commit option.

```
$ gloader test test --import --control sample.ctl --data sample.dat --commit 10000
```

<a id="b625b392dae21447"></a>
#### --comment

<a id="9e01119d7a49046d"></a>
##### Description

When gloader commits the transaction, it specifies the comment on the transaction.

<a id="e4b2f796a93cda05"></a>
##### Example

The following is an example of using --comment option.

```
$ gloader test test --import --control sample.ctl --data sample.dat --comment import_sample
```

<a id="f2b8bd73786c6b3b"></a>
#### --atomic

<a id="13cae7188f0538b0"></a>
##### Description

It is the option for performing array INSERT, and it is useful when uploading the data.  
The performance is faster than the existing array insert, because atomic array INSERT processes the insert statements as many as the size of array in a single transaction.

<a id="39e844f8ae67212f"></a>
##### Example

The following is an example of using --atomic option.

```
$ gloader test test --import --control sample.ctl --data sample.dat --array 1000 --atomic
```

<a id="43906e8ce54e7aab"></a>
#### --parallel

<a id="ed39af8a7aacea42"></a>
##### Description

It specifies the number of threads for parallel processing.  
It is useful only when gloader uploads the data, and the performance gets faster when the number of threads is increased by adjusting --parallel option.  
The performance gets faster by increasing the number of threads, but it is recommended to set the number of threads according to the operational environment.  
The default value is 1, and the maximum value is 32.

<a id="cd503d72b8c28f4d"></a>
##### Example

The following is an example of using eight threads when uploading data. Ten threads are operated together including threads analyzing the data files and read only threads, besides the eight uploading threads.

```
$ gloader test test --import --control sample.ctl --data sample.dat --parallel 8
```

<a id="2dc10a33db59fd34"></a>
#### --propagation

<a id="7eb60783bf1a66b1"></a>
##### Description

It determines whether to propagate the upload transaction log to another replicated server.  
It can be set to ON or OFF.

<a id="0fd53a1e96a45e85"></a>
##### Example

The following is an example of which the upload transaction log is not propagated to another replicated server.

```
$ gloader test test --import --control sample.ctl --data sample.dat --propagation off
```

<a id="0c774e3521c78fbf"></a>
#### --errors

<a id="9fa6d237c0555b6d"></a>
##### Description

It sets the number of errors permitted when gloader uploads the data.  
If not set, 100 (rows) are used. If it is set to 0, the --errors option is ignored.  
If it is smaller than the size of --array option, the number of permitted error is the number of array.

<a id="b795804726e100a8"></a>
##### Example

The following is an example of using --errors option.

```
$ gloader test test --import --control sample.ctl --data sample.dat --errors 10000
```

<a id="97b269ece4fb8efa"></a>
#### --AsTIMESTAMP

<a id="08f92d960dac82e2"></a>
##### Description

It sets the DATE type data stored in TIMESTAMP  format to be operated in TIMESTAMP format for backward compatibility.  
TIMESTAMP_FORMAT is also applied to the DATE type data when using the --AsTIMESTAMP option.

<a id="c6d723ce2e0a3adc"></a>
##### Example

The following is an example of using --AsTIMESTAMP option.

```
$ gloader test test --import --control sample.ctl --data sample.dat --AsTIMESTAMP
```

<a id="30c3d24bbd4b3d49"></a>
#### --buffered

<a id="4f2ab6953c4d3466"></a>
##### Description

Only the datafile uses the buffered IO instead of the direct IO.

The log file and bad file use the buffered IO.

<a id="d99e626a1dc2eabd"></a>
##### Example

The following is an example of using --buffered option.

```
$ gloader test test --import --control sample.ctl --data sample.dat --buffered
```

<a id="1a491eaa9b5d00b4"></a>
#### --fieldterm

<a id="66f9bd8f042e625d"></a>
##### Description

It provides a field terminator.  
If it is set in a control file as well, then the fieldterm argument value is preferentially used.   
% is added in front of n, r, t each for NEW LINE, CARRIAGE RETURN, TAB.  
Characters which is used as a shell meta character such as ', ", \, & is not recommended to use.

<a id="e87a74a3ad29e46b"></a>
##### Example

The following is an example of using --fieldterm option.

```
$ gloader test test --i -c sample.ctl -d sample.dat --fieldterm ",,,"
$ gloader test test --i -c sample.ctl -d sample.dat --fieldterm ,,,
$ gloader test test --i -c sample.ctl -d sample.dat --fieldterm ',,,'
```

<a id="2253c56d342ac34e"></a>
#### --lineterm

<a id="796cc3d6dacddfd0"></a>
##### Description

It provides a line terminator.  
If it is set in a control file as well, then the lineterm argument value is preferentially used.   
The detailed usage is the same as that of the fieldterm argument.

<a id="43c10b17ddf89b59"></a>
##### Example

The following is an example of using --lineterm option.

```
$ gloader test test --i -T PUBLIC.test -d sample.dat --lineterm ",,,"
$ gloader test test --i -T PUBLIC.test -d sample.dat --lineterm ,,,
$ gloader test test --i -T PUBLIC.test -d sample.dat --lineterm ',,,'
```

<a id="8eb738ea65952cf5"></a>
#### --qualifier

<a id="5909c3fff135b55c"></a>
##### Description

It provides a qualifier which is to be added to the start and the end of the column data. Only a single character can be set as a qualifier.  
If it is set in a control file as well, then the qualifier argument value is preferentially used.   
The detailed usage is the same as that of the fieldterm argument.

<a id="accf1b3d6a46cfb0"></a>
##### Example

The following is an example of using --qualifier option.

```
$ gloader test test --i -T PUBLIC.test -d sample.dat --qualifier "|"
$ gloader test test --i -T PUBLIC.test -d sample.dat --qualifier '"'
```

<a id="ec23c6ae1dc6bdc4"></a>
#### --where

<a id="f228b76b3b3fa280"></a>
##### Description

It downloads the data by setting a conditional clause for export operation.  
If the where clause is also set in a control file, then the where argument value is preferentially used.

<a id="d340e67fdc85cfca"></a>
##### Example

The following is an example of using --where option.

```
$ gloader test test --i -T PUBLIC.test -d sample.dat --where "I2 > 4"
```

<a id="3b346f0b6c7f0057"></a>
#### --group-id

<a id="aa76ff055ea3027b"></a>
##### Description

It directly uploads the data to the corresponding group after sorting the data by group when uploading the data in the sharded table in the cluster environment.  
If this option is used when uploading the data to the non-sharded table, the option is not valid.  
This option is operated only in C/S environment, so it is valid only in gloadernet and it can be used only when uploading text files.

*--group-id* option uses [GLOBAL CONNECTION](../part-05-developer-manual/34-odbc.md#563f4abadbee6767) of ODBC, so properties related to the [Data Source Configuration](../part-05-developer-manual/34-odbc.md#c0bc1af6b9e0ca88) should be set.

<a id="7b3d38c1ba3bf242"></a>
##### Example

The following is odbc.ini configuration file to use the global connection.

```
$cat .odbc.ini
[GOLDILOCKS]
HOST=127.0.0.1
PORT = 22581
LOCALITY_AWARE_TRANSACTION=1
LOCATOR_DSN = LOCATOR
[LOCATOR]
LOCATOR_FILE=.locator.ini
```

The following is an example of using *--group-id* option in gloadernet.

```
$ gloadernet test test --i -T PUBLIC.test -d sample.dat --group-id
COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 20 RECORDS, SUCCEEDED 20 RECORDS
```

The following is an example of an error which occurred due to using *--group-id* option in gloader.

```
$ gloader test test --i -T PUBLIC.test -d sample.dat --group-id
ERR-HY010(19009): Function sequence error : The function should be called only when the SQL_ATTR_LOCALITY_AWARE_TRANSACTION connection attribute is set.

```

<a id="ef9c34856da98d6a"></a>
#### --append

<a id="50d106a2273fc75c"></a>
##### Description

This is an option to process the existing data before loading the data in import mode. The DEFAULT value is APPEND.  
APPEND maintains the existing data, then loads the new data.  
REPLACE deletes the existing data with DELETE statement, then loads the new data.  
TRUNCATE deletes the existing data with TRUNCATE statement, then loads the new data.

<a id="0f6496f3af2abe6c"></a>
##### Example

The following is an example of using TRUNCATE for --append option.

```
$ gloader test test --i -T PUBLIC.test -d sample.dat --append TRUNCATE
```

<a id="b455497af89398b8"></a>
#### --directio-size

<a id="a8e83f69644fd379"></a>
##### Description

deprecated

<a id="6f6d7cb32f3ee8c9"></a>
#### --skip

<a id="b8f13c815ce4725f"></a>
##### Description

It sets the number of records to skip when uploading the data file. The default value is 0.

<a id="defc9464938c376e"></a>
##### Example

The following is an example of skipping 10 records by setting skip in gloader.

```
$ gloader test test --i -T PUBLIC.test -d sample.dat --skip 10
```

<a id="b6c0bb4b82487448"></a>
#### --no-copyright

<a id="51b237c7f91cc741"></a>
##### Description

It does not output the copyright and version.

<a id="e283f28a616e3afe"></a>
##### Example

The following is the result of executing gloader with --no-copyright option.

```
$ gloader test test --import --control sample.ctl --data sample.dat --no-copyright 
COMPLETED IN EXPORTING TABLE: PUBLIC.t1, 3 RECORDS 
$
```

<a id="6a36baed6763f543"></a>
#### --silent

<a id="adbbe86b0d48d7a2"></a>
##### Description

It does not output the results of executing gloader.

<a id="853c00d796434420"></a>
##### Example

The following is the result of executing gloader with --silent option.

```
$ gloader test test --import --control sample.ctl --data sample.dat --silent

$
```

<a id="27a4cd18817a5e57"></a>
#### --merge

<a id="69b35e5a3c91b53d"></a>
##### Description

Specifies the EXTENT or SEGMENT mode to use when loading data with the APPEND INSERT method.

- EXTENT: Loads data using the serial APPEND INSERT method.
- SEGMENT: Loads data using the PARALLEL APPEND INSERT method.

<a id="78412d1cc0ba140e"></a>
##### Example

The following is an example of executing gloader using the --merge option.

```
$ gloader test test --import --control sample.ctl --data sample.dat --merge EXTENT

$ gloader test test --import --control sample.ctl --data sample.dat --merge SEGMENT
```

<a id="c0a82b6402fa92ce"></a>
#### --skip_index_maintenance

<a id="0aa6c28685fdbf1d"></a>
##### Description

When loading data using the APPEND INSERT method, this option does not update indexes sets the index segments to UNUSABLE.  
This option must be used with the --merge option. If this option is omitted, the operation is performed using the DEFERRED_INDEX_MAINTENANCE method.

<a id="b7956f40534ab9b8"></a>
##### Example

The following is an example of executing gloader using the --skip_index_maintenance option.

```
$ gloader test test --import --control sample.ctl --data sample.dat --merge EXTENT --skip_index_maintenance
```

<a id="675744aca3d9fdc3"></a>
#### --nologging

<a id="a69351fe19daf4a3"></a>
##### Description

This option loads data using the NOLOGGING APPEND INSERT method.  
This option must be used with the --merge SEGMENT option. If omitted, the operation is performed using the LOGGING method.

<a id="7db81280a578c2b7"></a>
##### Example

The following is an example of executing gloader using the --nologging option.

```
$ gloader test test --import --control sample.ctl --data sample.dat --merge SEGMENT --nologging
```

<a id="af60c97cc4ea1deb"></a>
#### --help

<a id="11e6b5d0d2c45900"></a>
##### Description

It displays the help messages.  
For more information, refer to [Usage](#ad7eafe83ca4ddea).

---

[← 44. gsql/gsqlnet (Interactive SQL Tool)](44-gsql-gsqlnet-interactive-sql-tool.md) · [Table of contents](../README.md) · [46. gdump →](46-gdump.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
