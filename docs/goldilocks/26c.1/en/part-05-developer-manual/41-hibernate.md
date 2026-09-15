<a id="9fe1189a8e2aec90"></a>

# 41. Hibernate

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/9fe1189a8e2aec90)  
> Tag: `26c.1_0_tag`

[← 40. SQLAlchemy](40-sqlalchemy.md) · [Table of contents](../README.md) · [42. gcreatedb →](../part-06-utility-manual/42-gcreatedb.md)

<a id="da4e0f320cacdc45"></a>
## Overview

Hibernate is a Object-Replation Mapping (ORM) framework of which Java Persistent API (JPA) model is applied to the database. It maps the relationship between DB table and Java object so that it helps the persistent logic processing. In other words, when using hibernate, it is easy to access and control DB without using SQL.

<a id="99656da7c857e4fc"></a>
## Interworking with Hibernate

<a id="c505229f5696aa51"></a>
### Downloading Hibernate

To port GoldilocksDialect to Hibernate, Hibernate ORM Core and all dependency libraries compatible with that version are required.  
These libraries are available from [Maven Central](https://mvnrepository.com/artifact/org.hibernate.orm/hibernate-core). When downloading manually, the dependency list specified in the POM of the selected hibernate-core version must be checked, and the corresponding dependencies of the same version must be downloaded together.

<a id="28c3c811326bb2ee"></a>
### Interworking with GoldilocksDialect Class

GOLDILOCKS provides GoldilocksDialect.java file which is appropriate to Hibernate ORM version. When using GoldilocksDialect.java 5 version file in Hibernate ORM 4 version, then a compile error occurs. Therefore, use GoldilocksDialect.java file which is appropriate for Hibernate version.

Especially, Hibernate ORM 4 version provides each different api according to the patch version, so GOLDILOCKS provides GoldilocksDialect.java according to it. For example, Goldilocks.java 4.0.0 version is used in Hibernate ORM 4.1.4 version, and GoldilocksDialect.java 4.1.5 version is used in Hibernate ORM 4.1.9 version.

GOLDILOCKS provides GoldilocksDialect.java in the directory under $GOLDILOCKS_HOME/app_dev/Hibernate/.

The following files are added since Hibernate 5.

- ClonedSharding.java
- HashSharding.java
- Integrator.java
- ListSharding.java
- MetaStorage.java
- RangeSharding.java
- ShardingType.java
- TableSharding.java
- Tablespace.java
- org.hibernate.integrator.spi.Integrator

<a id="c70d0b93274e1fc8"></a>
#### Porting to Hibernate jar File

It should be ported to the downloaded Hibernate jar file to interwork with Hibernate. All class files can be included in Hibernate jar file as follows.

<a id="acfac4f61ceb1217"></a>
##### hibernate 4

1. Create a class file by compiling all java files using javac. (The class file is differently created per each version.)
2. Decompress Hibernate jar file.
3. Move created class files to the corresponding package path.
4. Compress it again with Hibernate jar file.
5. Add the newly created jar file to classpath.

```
$ javac -cp hibernate-core-4.3.9.Final.jar *.java

$ jar -xvf hibernate-core-4.3.9.Final.jar

$ mv Goldilocks*.class org/hibernate/dialect

$ jar -cvf hibernate-core-4.3.9.Final.jar META-INF/MANIFEST.MF .
```

<a id="f0e26a414886e882"></a>
##### hibernate 5, 6, 7

1. Create a class file by compiling all java files using javac. (The class file is differently created per each version.)
2. Decompress Hibernate jar file.
3. Create com/sunjesoft/annotation directory.
4. Move created class files to the corresponding package path.
5. Compress it again with Hibernate jar file.
6. Add the newly created jar file to classpath.

```
$ javac -cp hibernate-core-5.2.11.Final.jar:hibernate-jpa-2.1-api-1.0.2.Final.jar *.java

$ jar -xvf hibernate-core-5.2.11.Final.jar

$ mkdir -p com/sunjesoft/annotation

$ mv Integrator*.class MetaStorage.class com/sunjesoft
$ mv ClonedSharding.class HashSharding.class ListSharding*.class RangeSharding*.class ShardingType.class TableSharding.class Tablespace.class com/sunjesoft/annotation
$ mv Goldilocks*.class org/hibernate/dialect

$ mv org.hibernate.integrator.spi.Integrator META-INF/services

$ jar -cvf hibernate.5.2.11.jar META-INF/MANIFEST.MF .
```

<a id="a5f7bd68cc5779de"></a>
#### Porting to Program Source

<a id="c723c4473fec5821"></a>
##### hibernate 4

Interworking is available by directly using the source file without porting the class file to jar file. Create org.hibernate.dialect package in the user project, then insert java files into this package.

<a id="61f0d8c59b1f5917"></a>
##### hibernate 5, 6, 7

Interworking is available by directly using the source file without porting the class file to jar file. Create com.sunjesoft, com.sunjesoft.annotation and org.hibernate.dialect packages in the user project, then insert java files into this package.

- com.sunjesoft
    - Integrator.java
    - MetaStorage.java

- com.sunjesoft.annotation
    - ClonedSharding.java
    - HashSharding.java
    - RangeSharding.java
    - ShardingType.java
    - ListSharding.java
    - TableSharding.java
    - Tablespace.java

- org.hibernate.dialect
    - GoldilocksDialect.java

- META-INF.services
    - org.hibernate.integrator.spi.Integrator

<a id="7468fc5462ceca42"></a>
## Examples

<a id="92dc53a82c968994"></a>
### Configuration

hibernate-configuration XML file and hibernate-mapping XML file are required to interqork Hibernate and DB.

<a id="28ef90c8d0a34bac"></a>
#### Hibernate Configuration File

Configuration XML file sets the connect information to access the dialect class and DB, and sets Hibernate-mapping files.   
For more information, refer to [Configuration](http://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html#configurations).

The following is an example of hibernate.conf.xml file.

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
 
<hibernate-configuration>
	<session-factory>
		<property name="hibernate.connection.driver_class">sunje.goldilocks.jdbc.GoldilocksDriver</property>
		<property name="hibernate.connection.url">jdbc:goldilocks://192.168.0.21:22581/test</property>
		<property name="hibernate.connection.username">test</property>
		<property name="hibernate.connection.password">test</property>
		<property name="hibernate.dialect">org.hibernate.dialect.GoldilocksDialect</property>
		<property name="show_sql">true</property>
		<property name="format_sql">true</property>
		<property name="hbm2ddl.auto"> create </property>
		<mapping resource="SampleTable.mapping.xml" />
	</session-factory>
</hibernate-configuration>
```

Set the DB connecting information on &lt;session-factory&gt; tag, and specifies the dialect class name of DB to connect to hibernate.dialect property. Also, specify hibernate-mapping files by using &lt;mapping-resource&gt; tag.

<a id="2e8b1207e82dbc5f"></a>
#### Hibernate Mapping File

Mapping XML is a configuration file including mapping information about DB table and Java object.   
For more information, refer to [Mapping](http://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html#annotations).

The following is an example of SampleTable.mapping.xml file which was used in the example above.

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-mapping PUBLIC 
"-//Hibernate/Hibernate Mapping DTD 3.0//EN" 
"http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">

<hibernate-mapping>
	<class name="SampleTable" table="SAMPLETABLE">
		<id column="ID" name="id" type="long">
			<generator class="increment" />
		</id>
		<property column="STUDENT_NAME" name="name" type="string" />
		<property column="BIGINT_VALUE" name="bigintValue" type="long" />
		<property column="INT_VALUE" name="intValue" type="int" />
		<property column="SMALL_VALUE" name="smallValue" type="short" />
		<property column="FLOAT_VALUE" name="floatValue" type="float" />
		<property column="DOUBLE_VALUE" name="doubleValue" type="double" />
		<property column="NUMERIC_VALUE" name="numericValue" type="big_integer" precision="10" scale="5" />
		<property column="DATE_VALUE" name="dateValue" type="date" />
		<property column="TIME_VALUE" name="timeValue" type="time" />
		<property column="TIMESTAMP_VALUE" name="timestampValue" type="timestamp" />
		<property column="VARBINARY_VALUE" name="binaryValue" type="byte[]" />
	</class>
</hibernate-mapping>
```

The mapping information about Java class and DB table are described on &lt;class&gt; tag. Data type used in a table column and Java are specified on &lt;property&gt; tag.

<a id="c0b463d943dd26fd"></a>
### Examples of Application

Java class to be mapped to DB table should be described. The following is an example of SampleTable.java which is described above.

```
import java.math.BigInteger;
import java.sql.Date;
import java.sql.Time;
import java.sql.Timestamp;

public class SampleTable {
    private long id;
    private String     name;
    private long       bigintValue;
    private int        intValue;
    private short      smallValue;
    private float      floatValue;
    private double     doubleValue;
    private BigInteger numericValue;
    private Date       dateValue;
    private Time       timeValue;
    private Timestamp  timestampValue;
    private byte[]     binaryValue;
    private String     longvarcharValue;
    private byte[]     longvarbinaryValue;
    
    public SampleTable() {
        this.name = null;
    }
    
    public SampleTable( String name ) {
        this.name = name;
    }

    public long getId() {
        return id;
    }
    
    public void setId( long id ) {
        this.id = id;
    }
    
    public String getName() {
        return name;
    }
    
    public void setName( String name ) {
        this.name = name;
    }
....
```

get/ set function of a variable corresponding to a column of SampleTable table should be described.

The data is processed in SamleTable table as follows.

1. It obtains org.hibernate.SessionFactory object through a configuraion file. 
2. It obtains org.hibernate.Session object through SessionFactory object. 
3. It processes the desired operation by calling a method of a session object.

The following is an example of inserting, updating, retrieving, deleting data in SampleTable table of DB. It obtains SessionFactory object through org.hibernate.Configuration class.

```
public class HibernateSample
{
    private static SessionFactory mFactory;

    public static void main( String[] args ) {
        try {
            mFactory = new Configuration().configure( "hibernate.conf.xml" ).buildSessionFactory();
        } catch( Throwable ex ) {
            System.err.println( "Failed to create sessionFactory object." + ex);
            throw new ExceptionInInitializerError(ex);
        }
        HibernateSample sHibernateSample = new HibernateSample();
```

- Insert 3 records

```
Long sRecord1 = sHibernateSample.addSample( "RECORD_1" );
Long sRecord2 = sHibernateSample.addSample( "RECORD_2" );
Long sRecord3 = sHibernateSample.addSample( "RECORD_3" );
```

- Update record 1

```
sHibernateSample.updateSample( sRecord1, ....
```

- Fetch table

```
sHibernateSample.fetchSample( 0, 3 );
```

- Delete record 2

```
sHibernateSample.deleteSample( sRecord2 );

sHibernateSample.closeFactory();
    }

public void closeFactory() {
        mFactory.close();
    }

....
```

The following is an example of a method inserting a record to HibernateSample class. First, it obtains a session object through SessionFactory class, then obtains org.hibernate.Transaction object. It can be committed or rolled back after starting a transaction by using a transaction class and inserting a record.

```
public Long addSample( String name ) {
	Session session = mFactory.openSession();
	Transaction tx = null;
	Long id = null;
        
	try{
```

- Begin transaction

```
tx = (Transaction) session.beginTransaction();
SampleTable sample = new SampleTable( name );
```

- Insert

```
id = (Long) session.save(sample);
```

- Commit transaction

```
tx.commit();
            
        System.out.println("add success");
    } catch( HibernateException e) {
        if( tx != null ) {
            tx.rollback();
        }
        System.out.println("add fail");
        e.printStackTrace();
    } finally {
        session.close();
    }
    return id;
}
```

The following is an example of a method retrieving SampleTable table. It obtains org.hibernate.Query object through a session class. fetchSample method retrieves SampleTable from offset to count.

```
public void fetchSample( int offset, int count ) {
    Session session = mFactory.openSession();
    Query query = null;
        
    try{
        query = session.createQuery( "FROM SampleTable" );

        query.setFirstResult( offset );
        query.setMaxResults( count );
        query.setFetchSize( 20 );
            
        @SuppressWarnings( "unchecked" )
		List<SampleTable> samples = (List<SampleTable>) query.list();

		for( Iterator<SampleTable> iter = samples.iterator(); iter.hasNext(); ) {
            SampleTable sample = (SampleTable) iter.next();
            System.out.print( "id: " + sample.getId() );
           ... Ellipsis ...
        }
    } catch ( HibernateException e ) {
        e.printStackTrace();
    } finally {
        session.close();
    }
}
```

The following is an exampel of a method updating SampleTable table. After altering to a set method described in SampleTable class, then it is updated by calling an update method of a session class.

```
public void updateSample( long id, ... ) {
	Session session = mFactory.openSession();
	Transaction tx = null;
	try {
		tx = session.beginTransaction();
		SampleTable sample = (SampleTable)session.get(SampleTable.class, id);
		sample.setName( name );
		...
		session.update( sample );
		tx.commit();
		System.out.println( "update success" );
		} catch ( HibernateException e ) {
			if( tx != null ){
				tx.rollback();
			}
			System.out.println("update fail");
			e.printStackTrace();
		} finally {
	session.close();
	}
}
```

The following is an example of deleting a record. It can be deleted by using a delete method of a session class.

```
public void deleteSample( long id ) {
	Session session = mFactory.openSession();
	Transaction tx = null;
        
	try {
        tx = session.beginTransaction();
        SampleTable sample = (SampleTable) session.get( SampleTable.class, id );       
		session.delete( sample );
        tx.commit();
            
        System.out.println( "delete success" );
	} catch ( HibernateException e ) {
        if( tx != null ) {
            tx.rollback();
        }

        System.out.println("delete fail");
        e.printStackTrace();
    } finally {
		session.close();
	}
}
```

---

[← 40. SQLAlchemy](40-sqlalchemy.md) · [Table of contents](../README.md) · [42. gcreatedb →](../part-06-utility-manual/42-gcreatedb.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
