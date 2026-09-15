<a id="1d05c2641db0a780"></a>

# 37. PDO

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/1d05c2641db0a780)  
> Tag: `26c.1_0_tag`

[← 36. Embedded SQL](36-embedded-sql.md) · [Table of contents](../README.md) · [38. PyDBC →](38-pydbc.md)

<a id="870009b161ef6f3d"></a>
## Overview of PDO

GOLDILOCKS PDO (PDO_GOLDILOCKS) driver provides PDO interface to access GOLDILOCKS database in PDO.

PDO_GOLDILOCKS is implemented based on the GOLDILOCKS CLI driver. The GOLDILOCKS distribution package provides PDO_GOLDILOCKS source code and PECL package metadata for each supported PHP version.

<a id="0a237ab99dd2bea4"></a>
## Installation /Configuration

<a id="3cec64f75fba3806"></a>
### Requirement

The GOLDILOCKS client package must be installed on the same system as PHP, and the $GOLDILOCKS_HOME environment variable must be configured.

Building the source requires a C compiler and the development package corresponding to the installed PHP version. The phpize and php-config commands must also be available. To build or install a PECL package, PEAR/PECL must be installed.

<a id="6804c53920ee8c9f"></a>
### Installation

<a id="d75720af1f187e02"></a>
#### Selecting the Source for the PHP Version

The PDO_GOLDILOCKS source is provided in PHP version-specific directories under $GOLDILOCKS_HOME/app_dev/pdo. Select the source directory that matches the installed PHP version.

<a id="4cc9a7f2cf6d1fca"></a>
| PHP version | Source directory |
| --- | --- |
| PHP 5.1 ~ 5.6 | PDO_legacy |
| PHP 7.0 ~ 8.0 | PDO_php7_to_80 |
| PHP 8.1 and_above | PDO_php81_and_above |

The php, phpize, and php-config commands must all correspond to the same PHP version. The installed PHP version can be verified by running the following command:

```
% php -v
```

PECL does not automatically select the source directory corresponding to the PHP version. Therefore, even when using PECL, the appropriate source directory must be selected according to the table above.

<a id="489f10c1f3382749"></a>
#### Installing with PECL

Run the pecl pickle command in the selected source directory to generate a PECL package. The following example uses the source for PHP 7.0–8.0.

```
% cd $GOLDILOCKS_HOME/app_dev/pdo/PDO_php7_to_80
% pecl pickle
Attempting to process the second package file
Package PDO_GOLDILOCKS-26.1.0.tgz done
```

After the PDO_GOLDILOCKS package file is generated, install the package by using the pecl command.

```
% sudo -E pecl install ./PDO_GOLDILOCKS-26.1.0.tgz
```

<a id="744a566420a7a5ee"></a>
#### Installing from Source

Instead of generating a PECL package, the extension can be built directly from the selected source directory. The following example uses the source for PHP 7.0–8.0.

1. Move to the source directory.

```
% cd $GOLDILOCKS_HOME/app_dev/pdo/PDO_php7_to_80
```

2. Run the phpize command to prepare the build environment for the PDO_GOLDILOCKS extension.

```
% phpize
```

3. Build the extension by specifying the php-config command and the $GOLDILOCKS_HOME path.

```
% ./configure --with-php-config="$(command -v php-config)" --with-pdo-goldilocks="$GOLDILOCKS_HOME"
```

```
% make
```

4. Install the built extension.

```
% sudo -E make install
```

<a id="8af68d235e61e229"></a>
#### Modifying the PHP Configuration File

Run the following command to identify the configuration file and the additional configuration file directory used by PHP.

```
% php --ini
```

Add the following entry to the pdo_goldilocks.ini file in the identified configuration file or the additional configuration file directory.

```
extension=pdo_goldilocks.so
```

CLI and the web server or PHP-FPM may use different PHP configuration files. Verify the configuration file used by each.

<a id="2ee5ddc6b08abb51"></a>
#### Restarting the Web Server or PHP-FPM

If PDO_GOLDILOCKS is used in a web application, restart the web server or PHP-FPM.

<a id="85cfbb7a48f7cfd3"></a>
#### Verifying the PDO_GOLDILOCKS Installation

Run the following commands to verify that the PDO_GOLDILOCKS extension module and the PDO driver are enabled.

```
% php -m | grep -i '^pdo_goldilocks$'
pdo_goldilocks
```

```
% php -i | grep 'PDO Driver for GOLDILOCKS'
PDO Driver for GOLDILOCKS => enabled
```

<a id="6198ec6e9e219615"></a>
## Usage

<a id="620e74f47d4ea479"></a>
### Data Source Name (DSN)

Data Source Name (DSN) of PDO_GOLDILOCKS is configured as follows.

<a id="bc84d8efb9b418ca"></a>
| Property | Description |
| --- | --- |
| DSN prefix | goldilocks |
| DSN | ODBC Data Source Name (DSN) |
| HOST | IP address of a server |
| PORT | PORT number of server |
| UID | User ID |
| PWD | User password |

<a id="5a32ce96509c9065"></a>
## Examples

- Connecting to GOLDILOCKS

```
print "\n[Connecting to GOLDILOCKS]\n";
$db = new PDO('goldilocks:HOST=192.168.0.16;PORT=22581', 'test', 'test');
//$db = new PDO('goldilocks:DSN=GOLDILOCKS;UID=test;PWD=test');
$db->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
```

- Set test data

```
$result = $db->exec('DROP TABLE IF EXISTS t1');
$result = $db->exec('CREATE TABLE t1 ( id INTEGER GENERATED BY DEFAULT AS IDENTITY, name VARCHAR(32) )');
$result = $db->exec("INSERT INTO t1(name) VALUES ('Carol')");
$result = $db->exec("INSERT INTO t1(name) VALUES ('Ted')");
$result = $db->exec("INSERT INTO t1(name) VALUES (null)");
$result = $db->exec("INSERT INTO t1(name) VALUES ('William')");
$result = $db->exec("INSERT INTO t1(name) VALUES ('Chelsea')");
$result = $db->exec("INSERT INTO t1(name) VALUES ('Colin')");

$result = $db->exec('DROP TABLE IF EXISTS t2');
$result = $db->exec('CREATE TABLE t2 ( id INTEGER, name VARCHAR(32) )');
$result = $db->exec("INSERT INTO t2 VALUES (1, 'John')");
$result = $db->exec("INSERT INTO t2 VALUES (1, 'John')");
$result = $db->exec("INSERT INTO t2 VALUES (1, 'John')");
$result = $db->exec("INSERT INTO t2 VALUES (2, 'Smith')");
$result = $db->exec("INSERT INTO t2 VALUES (2, 'Smith')");

$result = $db->exec('DROP TABLE IF EXISTS images');
$result = $db->exec('CREATE TABLE images ( id INTEGER, contenttype VARCHAR(256), imagedata LONG VARBINARY )');

$result = $db->exec('DROP PROCEDURE IF EXISTS sp_out_string');
$result = $db->exec("CREATE OR REPLACE PROCEDURE sp_out_string( v1 OUT VARCHAR(32) ) ".
                    "IS ".
                    "BEGIN ".
                    "  v1 := 'WORLD'; ".
                    "END; ");

$result = $db->exec('DROP PROCEDURE IF EXISTS sp_inout_string');
$result = $db->exec("CREATE OR REPLACE PROCEDURE sp_inout_string( v1 INOUT VARCHAR(32) ) ".
                    "IS ".
                    "BEGIN ".
                    "  v1 := V1 || ' WORLD'; ".
                    "END; ");
```

- Quoting a normal string

```
print "\n[Quoting a normal string]\n";
$string = 'Nice';

print "Unquoted string: $string\n";
print "Quoted string  : " . $db->quote($string) . "\n";
```

- Quoting a dangerous string

```
print "\n[Quoting a dangerous string]\n";
$string = 'Naughty \' string';

print "Unquoted string: $string\n";
print "Quoted string  :" . $db->quote($string) . "\n";
```

- Quoting a complex string

```
print "\n[Quoting a complex string]\n";
$string = "Co'mpl''ex \"st'\"ring";

print "Unquoted string: $string\n";
print "Quoted string  : " . $db->quote($string) . "\n";
```

- Handling an error

```
print "\n[Error Handling]\n";
try
{
    //connect as appropriate as above
    $db->query('invalid query'); //invalid query!
}
catch(PDOException $ex)
{
    print "ERROR:".$ex->getMessage()."\n";
}
```

- Retrieving column metadata

```
print "\n[Retrieving column metadata]\n";
$stmt = $db->query('SELECT * FROM t1');
foreach(range(0, $stmt->columnCount() - 1) as $column_index)
{
    $meta = $stmt->getColumnMeta($column_index);
    var_dump($meta);
}
```

- Running simple select statements

```
print "\n[Running Simple Select Statements]\n";

print "\n#1\n";
foreach($db->query('SELECT * FROM t1') as $row)
{
    print $row['ID'].' '.$row['NAME']."\n";
}

print "\n#2\n";
$stmt = $db->query('SELECT * FROM t1');
 
while($row = $stmt->fetch(PDO::FETCH_ASSOC))
{
    print $row['ID'].' '.$row['NAME']."\n";
}
```

- Fetching rows using different fetch styles

```
print "\n[Fetching rows using different fetch styles]\n";
$stmt = $db->prepare("SELECT id, name FROM t1");
$stmt->execute();

print("PDO::FETCH_ASSOC: ");
print("Return next row as an array indexed by column name\n");
$result = $stmt->fetch(PDO::FETCH_ASSOC);
print_r($result);
print("\n");

print("PDO::FETCH_BOTH: ");
print("Return next row as an array indexed by both column name and number\n");
$result = $stmt->fetch(PDO::FETCH_BOTH);
print_r($result);
print("\n");

print("PDO::FETCH_LAZY: ");
print("Return next row as an anonymous object with column names as properties\n");
$result = $stmt->fetch(PDO::FETCH_LAZY);
print_r($result);
print("\n");

print("PDO::FETCH_OBJ: ");
print("Return next row as an anonymous object with column names as properties\n");
$result = $stmt->fetch(PDO::FETCH_OBJ);
print $result->NAME;
print("\n");
```

- Fetching rows with a scrollable cursor

```
print "\n[Fetching rows using different fetch styles]\n";
print "\n[Fetching rows with a scrollable cursor]\n";
$sql = 'SELECT id, name FROM t1 ORDER BY id';

print "Reading forwards:\n";
try
{
    $stmt = $db->prepare($sql, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));
    $stmt->execute();
    while( $row = $stmt->fetch(PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT) )
    {
        $data = $row[0] . "\t" . $row[1] . "\n";
        print $data;
    }
    $stmt = null;
}
catch (PDOException $e)
{
    print $e->getMessage();
}

print "Reading backwards:\n";
try
{
    $stmt = $db->prepare($sql, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));
    $stmt->execute();
    $row = $stmt->fetch(PDO::FETCH_NUM, PDO::FETCH_ORI_LAST);
    do
    {
        $data = $row[0] . "\t" . $row[1] . "\n";
        print $data;
    } while( $row = $stmt->fetch(PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR) );

    $stmt = null;
}
catch (PDOException $e)
{
    print $e->getMessage();
}
```

- Constructing an order

```
print "\n[Construction order]\n";
class Person
{
    private $NAME;

    public function __construct()
    {
        $this->tell();
    }

    public function tell()
    {
        if (isset($this->NAME))
        {
            print "I am {$this->NAME}.\n";
        }
        else
        {
            print "I don't have a name yet.\n";
        }
    }
}
$stmt = $db->query("SELECT name FROM t1");
$stmt->setFetchMode(PDO::FETCH_CLASS, 'Person');
$person = $stmt->fetch();
$person->tell();
$stmt->setFetchMode(PDO::FETCH_CLASS|PDO::FETCH_PROPS_LATE, 'Person');
$person = $stmt->fetch();
$person->tell();
```

- Running simple INSERT, UPDATE, or DELETE statements

```
print "\n[Running Simple INSERT, UPDATE, or DELETE statements]\n";
$affected_rows = $db->exec("INSERT INTO t1(name) VALUES ('John'), ('Marry')");
print $affected_rows." were affected\n";
```

- Getting the last insert id

```
print "\n[Getting the Last Insert Id]\n";
$affected_rows = $db->exec("INSERT INTO t1(name) VALUES ('Smith')");
$insertId = $db->lastInsertId();
print "last insert id : ".$insertId."\n";
```

- Running statements with parameters

```
print "\n[Running Statements With Parameters]\n";

print "\n#1 array\n";
$id = 1;
$name = 'John';

$stmt = $db->prepare("SELECT * FROM t2 WHERE id=? AND name=?");
$stmt->execute(array($id, $name));
$rows = $stmt->fetchAll(PDO::FETCH_ASSOC);

var_dump($rows);

print "\n#2 bindValue\n";
$id = 2;
$name = 'Smith';

$stmt = $db->prepare("SELECT * FROM t2 WHERE id=? AND name=?");
$stmt->bindValue(1, $id, PDO::PARAM_INT);
$stmt->bindValue(2, $name, PDO::PARAM_STR);
$stmt->execute();
$rows = $stmt->fetchAll(PDO::FETCH_ASSOC);

var_dump($rows);
```

- Named placeholders

```
print "\n[Named Placeholders]\n";

print "\n#1 array\n";
$id = 1;
$name = 'John';

$stmt = $db->prepare("SELECT * FROM t2 WHERE id=:id AND name=:name");
$stmt->execute(array(':name' => $name, ':id' => $id));
$rows = $stmt->fetchAll(PDO::FETCH_ASSOC);

var_dump($rows);

print "\n#2 bindValue\n";
$id = 2;
$name = 'Smith';

$stmt = $db->prepare("SELECT * FROM t2 WHERE id=:id AND name=:name");
$stmt->bindValue(':id', $id, PDO::PARAM_INT);
$stmt->bindValue(':name', $name, PDO::PARAM_STR);
$stmt->execute();
$rows = $stmt->fetchAll(PDO::FETCH_ASSOC);

var_dump($rows);
```

- Executing prepared statements in a loop

```
print "\n[Executing prepared statements in a loop]\n";
$values = array('bob', 'alice', 'lisa', 'john');
$name = '';
$stmt = $db->prepare("INSERT INTO t1(name) VALUES(:name)");
$stmt->bindParam(':name', $name, PDO::PARAM_STR);
foreach($values as $name)
{
   $stmt->execute();
}

foreach($db->query('SELECT * FROM t1') as $row)
{
    print $row[0].' '.$row[1]."\n";
}
```

- Calling a stored procedure with an output parameter

```
print "\n[Calling a stored procedure with an output parameter]\n";
$stmt = $db->prepare("CALL sp_out_string(?)");
$stmt->bindParam(1, $value, PDO::PARAM_STR, 32); 
$stmt->execute();

print "procedure returned $value\n";
```

- Calling a stored procedure with an input/output parameter

```
print "\n[Calling a stored procedure with an input/output parameter]\n";
$stmt = $db->prepare("CALL sp_inout_string(?)");
$value = 'HELLO';
$stmt->bindParam(1, $value, PDO::PARAM_STR|PDO::PARAM_INPUT_OUTPUT, 32); 
$stmt->execute();

print "procedure returned $value\n";
```

- Transactions

```
print "\n[Transactions]\n";

print "\n#1 commit\n";
try
{
    $db->beginTransaction();
 
    $db->exec("INSERT INTO t1(name) VALUES('kim')");

    $name = 'lee';
    $stmt = $db->prepare("INSERT INTO t1(name) VALUES(?)");
    $stmt->execute(array($name));
 
    $id = 3;
    $name = 'park';
    $stmt = $db->prepare("INSERT INTO t2 VALUES(?, ?)");
    $stmt->execute(array($id, $name));
 
    $db->commit();
}
catch(PDOException $ex)
{
    //Something went wrong rollback!
    $db->rollBack();
    print $ex->getMessage()."\n";
}

print "\nT1\n";
foreach($db->query('SELECT * FROM t1') as $row)
{
    print $row[0].' '.$row[1]."\n";
}

print "\nT2\n";
foreach($db->query('SELECT * FROM t2') as $row)
{
    print $row[0].' '.$row[1]."\n";
}

print "\n#2 rollback\n";
try
{
    $db->beginTransaction();
 
    $db->exec("INSERT INTO t1(name) VALUES('KIM')");

    $name = 'LEE';
    $stmt = $db->prepare("INSERT INTO t1(name) VALUES(?)");
    $stmt->execute(array($name));
 
    $id = 3;
    $name = 'PARK';
    $stmt = $db->prepare("INSERT INTO invalid VALUES(?, ?)");
    $stmt->execute(array($id, $name));
 
    $db->commit();
}
catch(PDOException $ex)
{
    //Something went wrong rollback!
    $db->rollBack();
    print $ex->getMessage()."\n";
}

print "\nT1\n";
foreach($db->query('SELECT * FROM t1') as $row)
{
    print $row[0].' '.$row[1]."\n";
}

print "\nT2\n";
foreach($db->query('SELECT * FROM t2') as $row)
{
    print $row[0].' '.$row[1]."\n";
}
```

- Inserting an image into a database

```
print "\n[Inserting an image into a database]\n";
try
{
    $stmt = $db->prepare("INSERT INTO images (id, contenttype, imagedata) VALUES (?, ?, ?)");

    $id = 1;
    $type = "image/png";
    $fp = fopen("logo.png", "rb");

    $stmt->bindParam(1, $id, PDO::PARAM_INT);
    $stmt->bindParam(2, $type, PDO::PARAM_STR, 256);
    $stmt->bindParam(3, $fp, PDO::PARAM_LOB);

    $db->beginTransaction();
    $stmt->execute();
    $db->commit();
}
catch(PDOException $ex)
{
    $db->rollBack();
    print $ex->getMessage()."\n";
}

foreach($db->query('SELECT id, contenttype, lengthb(imagedata) FROM images') as $row)
{
    print $row[0].' '.$row[1].' '.$row[2]."\n";
}
```

- Displaying an image from a database

```
print "\n[Displaying an image from a database]\n";
try
{
    $stmt = $db->prepare("SELECT contenttype, imagedata FROM images WHERE id = ?");

    $id = 1;
    $stmt->execute(array($id));
    $stmt->bindColumn(1, $type, PDO::PARAM_STR, 256);
    $stmt->bindColumn(2, $lob, PDO::PARAM_LOB);
    $stmt->fetch(PDO::FETCH_BOUND);

    print 'Content-Type: '.$type."\n";
    print 'size: '.file_put_contents($id.".png", $lob)."\n";
}
catch(PDOException $ex)
{
    print $ex->getMessage()."\n";
}
```

---

[← 36. Embedded SQL](36-embedded-sql.md) · [Table of contents](../README.md) · [38. PyDBC →](38-pydbc.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
