<a id="77edebfc1bb86c29"></a>

# 41. Hibernate

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/77edebfc1bb86c29)  
> 태그: `26c.1_0_tag`

[← 40. SQLAlchemy](40-sqlalchemy.md) · [전체 목차](../README.md) · [42. gcreatedb →](../part-06-utility-manual/42-gcreatedb.md)

<a id="837e6900bd3d7878"></a>
## 개요

Hibernate는 Java Persistent API (JPA) 모델을 데이터베이스에 적용한 Object-Replation Mapping (ORM) 프레임워크이다. DB 테이블과 Java 객체와의 관계를 매핑시켜 지속성 있는 로직 (persistent logic) 처리를 도와준다. 즉, Hibernate를 이용하면 SQL을 이용하지 않고도 DB에 쉽게 접근하고 제어할 수 있다.

<a id="33fe5575c26ed762"></a>
## 연동

<a id="925f554b068082d5"></a>
### 다운로드

Hibernate에 GoldilocksDialect를 porting 하려면 Hibernate ORM Core와 해당 버전에 맞는 모든 의존성 라이브러리가 필요하다.   
이 라이브러리들은 [Maven Central](https://mvnrepository.com/artifact/org.hibernate.orm/hibernate-core)에서 받을 수 있는데, 수동으로 다운로드할 경우에는 선택한 hibernate-core 버전의 POM에 명시된 의존성 목록을 확인하여 동일한 버전으로 함께 받아야 한다.

<a id="7c5d9e232f158357"></a>
### GoldilocksDialect 클래스 연동

GOLDILOCKS는 Hibernate ORM 버전에 맞게 GoldilocksDialect.java 파일을 제공한다. Hibernate ORM 4버전에 GoldilocksDialect.java 5 버전 파일을 사용하면 컴파일 에러가 발생한다. 따라서 사용하는 Hibernate 버전에 맞는 GoldilocksDialect.java 파일을 사용해야 한다.

특히 Hibernate ORM 4 버전은 패치 버전에 따라 제공되는 api가 다르기 때문에 GOLDILOCKS도 이에 맞춘 GoldilocksDialect.java 파일을 제공한다. 예를 들어, 사용하는 Hibernate ORM의 버전이 4.1.4라면 Goldilocks.java 4.0.0 버전을 사용하고 Hibernate ORM 버전이 4.1.9이라면 GoldilocksDialect.java 4.1.5 버전을 사용하면 된다.

GOLDILOCKS는 $GOLDILOCKS_HOME/app_dev/Hibernate/ 이하 디렉토리에 GoldilocksDialect.java를 제공하고 있다.

다음은 Hibernate 5 부터 추가된 파일이다.

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

<a id="a9a39f5b7f893b9e"></a>
#### Hibernate jar 파일에 이식

Hibernate와 연동하려면 다운로드 받은 Hibernate jar 파일에 이식해야 한다. 다음과 같이 모든 class 파일을 Hibernate jar 파일에 포함시킬 수 있다.

<a id="10ce007c99a4b688"></a>
##### hibernate 4

1. 모든 java 파일을 javac로 컴파일하여 class 파일을 생성한다. (버전별로 생성되는 class 파일이 다르다.)
2. Hibernate jar 파일의 압축을 푼다.
3. 생성된 class 파일을 패키지 경로에 맞도록 이동시킨다.
4. Hibernate jar 파일로 다시 압축한다.
5. 새로 생성한 jar 파일을 classpath에 추가한다.

```
$ javac -cp hibernate-core-4.3.9.Final.jar *.java

$ jar -xvf hibernate-core-4.3.9.Final.jar

$ mv Goldilocks*.class org/hibernate/dialect

$ jar -cvf hibernate-core-4.3.9.Final.jar META-INF/MANIFEST.MF .
```

<a id="01f89b7742031c81"></a>
##### hibernate 5, 6, 7

1. 모든 java 파일을 javac로 컴파일하여 class 파일을 생성한다. (버전별로 생성되는 class 파일이 다르다.)
2. Hibernate jar 파일의 압축을 푼다.
3. com/sunjesoft/annotation 디렉토리를 생성한다.
4. 생성된 class 파일을 패키지 경로에 맞도록 이동시킨다.
5. Hibernate jar 파일로 다시 압축한다.
6. 새로 생성한 jar 파일을 classpath에 추가한다.

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

<a id="dc6e353f0eb5bc43"></a>
#### Program 소스에 이식

<a id="d96b577e8ef5184c"></a>
##### hibernate 4

jar 파일에 class 파일을 이식하지 않고 소스 파일을 직접 이용하여 연동할 수 있다. 사용자 프로젝트에 org.hibernate.dialect package 를 생성하고 java 파일을 패키지에 넣으면 된다.

<a id="8dd105cfc32d0bd9"></a>
##### hibernate 5, 6, 7

jar 파일에 class 파일을 이식하지 않고 소스 파일을 직접 이용하여 연동할 수 있다. 사용자 프로젝트에 com.sunjesoft, com.sunjesoft.annotation 및 org.hibernate.dialect package 를 생성하고 java 파일을 패키지에 넣으면 된다.

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

<a id="9f8cb7f171c1976f"></a>
## 사용 예

<a id="e36fb03c9526c9de"></a>
### 설정

Hibernate를 DB와 연동하려면 hibernate-configuration XML 파일과 hibernate-mapping XML 파일이 필요하다.

<a id="1acb3b383c62d5cc"></a>
#### Hibernate Configuration 파일

Configuration XML 파일은 dialect 클래스와 DB에 접속하기 위한 연결 정보 및 Hibernate-mapping 파일들을 설정하는 파일이다.   
자세한 내용은 [Configuration](http://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html#configurations)을 참조한다.

다음은 hibernate.conf.xml 파일의 예이다.

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

&lt;session-factory&gt; 태그에 DB 연결 정보를 설정하고 hibernate.dialect 속성에 연결하려는 DB의 Dialect 클래스 이름을 명시한다. 또한 &lt;mapping-resource&gt; 태그를 이용하여 hibernate-mapping 파일들을 명시한다.

<a id="06e98702b4d67a09"></a>
#### Hibernate Mapping 파일

Mapping XML은 DB 테이블과 Java object의 매핑 정보를 담고 있는 설정 파일이다.   
자세한 내용은 [Mapping](http://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html#annotations)을 참조한다.

다음은 위 예에서 사용한 SampleTable.mapping.xml 파일의 예이다.

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

&lt;class&gt; 태그에는 Java 클래스와 DB 테이블의 매핑 정보를 기술한다. &lt;property&gt; 태그에는 테이블의 column과 Java에서 사용하는 데이터 타입을 지정한다.

<a id="f03ff85e5b00d0b5"></a>
### Application 예제

DB 테이블에 매핑되는 Java 클래스를 기술해야 한다. 다음은 위에서 설명한 SampleTable.java의 예이다.

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

SampleTable 테이블의 column에 대응하는 변수의 get/set 함수를 작성해야 한다.

SamleTable 테이블에서는 다음과 같이 데이터를 처리한다.

1. configuraion 파일을 통해 org.hibernate.SessionFactory 객체를 얻어온다. 
2. SessionFactory 객체를 통해 org.hibernate.Session 객체를 얻어온다. 
3. Session 객체의 method를 호출하여 원하는 작업을 한다.

다음은 DB의 SampleTable 테이블에 데이터를 추가, 갱신, 조회, 삭제하는 응용 프로그램의 예이다. org.hibernate.Configuration 클래스를 통해서 SessionFactory 객체를 얻는다.

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

다음은 HibernateSample 클래스에 레코드를 삽입하는 method의 예이다. 먼저 SessionFactory 클래스를 통해 session 객체를 얻은 후 org.hibernate.Transaction 객체를 얻는다. Transaction 클래스를 이용하여 transaction을 시작하고 레코드를 삽입한 후에 commit 하거나 rollback 할 수 있다.

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

다음은 SampleTable 테이블을 조회하는 method의 예이다. Session 클래스를 통해 org.hibernate.Query 객체를 얻는다. fetchSample method는 SampleTable을 offset부터 count 만큼 조회한다.

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
            ... 중략 ...
        }
    } catch ( HibernateException e ) {
        e.printStackTrace();
    } finally {
        session.close();
    }
}
```

다음은 SampleTable 테이블을 갱신하는 method의 예이다. SampleTable 클래스에 작성된 set method로 변경한 후에 session 클래스의 update method를 호출하여 갱신한다.

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

다음은 레코드를 삭제하는 예이다. Session 클래스의 delete method를 이용해서 삭제할 수 있다.

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

[← 40. SQLAlchemy](40-sqlalchemy.md) · [전체 목차](../README.md) · [42. gcreatedb →](../part-06-utility-manual/42-gcreatedb.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
