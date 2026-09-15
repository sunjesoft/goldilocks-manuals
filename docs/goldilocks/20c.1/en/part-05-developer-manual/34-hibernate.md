<a id="91b5e9fb7a837ad3"></a>

# 34. Hibernate

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/91b5e9fb7a837ad3)  
> Tag: `20c.1_30_tag`

[← 33. PyDBC](33-pydbc.md) · [Table of contents](../README.md) · [35. gcreatedb →](../part-06-utility-manual/35-gcreatedb.md)

<a id="b38aa0a393b7a451"></a>
## Overview

Hibernate is a Object-Replation Mapping (ORM) framework of which Java Persistent API (JPA) model is applied to the database. It maps the relationship between DB table and Java object so that it helps the persistent logic processing. In other words, when using hibernate, it is easy to access and control DB without using SQL.

<a id="a0c55d8f11f3aa8d"></a>
## Interworking with Hibernate

<a id="542288b480fde352"></a>
### Downloading Hibernate

Hibernate can be downloaded at [https://sourceforge.net/projects/hibernate/](https://sourceforge.net/projects/hibernate/). When the downloaded file is decompressed, many jar files are found in lib directory. These files are used to interwork with hibernate.

> Hibernate of GOLDILOCKS is created based on Hibernate version 5.2.

<a id="e61e95097624686b"></a>
### Interworking with GoldilocksDialect Class

It should be ported to the downloaded Hibernate jar file to interwork with Hibernate. GoldilocksDialect.class file and GoldilocksDialect$1.class file can be included in Hibernate jar file as follows.

1. Decompress Hibernate jar file.
2. Move GoldilocksDialect.class file and GoldilocksDialect$1.class file to the decomprressed org/hibernate/dialect directory.
3. Compress it again with Hibernate jar file.
4. Add the newly created jar file to classpath.

```
$ jar -xvf hibernate-core-5.2.11.Final.jar

$ pwd 
hibernate-release-5.2.11.Final/lib/required/
$ mv GoldilocksDialect*.class org/hibernate/dialect/

$ jar -cvf hibernate.5.2.11.jar  META-INF/MANIFEST.MF .
```

<a id="6dafff4af8754514"></a>
## Examples

<a id="f6a48b73ba0d563c"></a>
### Configuration

hibernate-configuration XML file and hibernate-mapping XML file are required to interqork Hibernate and DB.

<a id="fac074362c7e4713"></a>
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

<a id="4d846ae14b8a5538"></a>
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

<a id="31df2ba62e176496"></a>
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

[← 33. PyDBC](33-pydbc.md) · [Table of contents](../README.md) · [35. gcreatedb →](../part-06-utility-manual/35-gcreatedb.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
