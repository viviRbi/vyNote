

# Hibernate 

##  What is Hibernate? What is JPA?
- **Hibernate** is an open source object relational maping tool for Java. It provides a framework for mapping an object-oriented model to a relational database. It also provides data query and retrival facilities that can significantly reduce development time.
- It is a ‘JPA Provider’ framework. It is one of the most frequent used JPA implementation
- **Java Persistence API** is a collection of classes and methods to store the vast amounts of data into a database which is provided by the Oracle Corporation.
- JPA is an open source API. It is only a set of specifications for accessing, persisting and managing data between Jav obj and relational database entities which cannot be used without a provider/ aka its implementation, like  Hibernate, Eclipselink, Toplink, Spring Data JPA, etc.
## ORM 
- **ORM** Object relational mapping refers to the automated and transparent persistent of obj in a Java app to the tables in a relational database, using metadata that describes the mapping between obj and database
- **ORM advantage**:
  - Significantly reduct the development time
  - Involves writing less code
  - Increases system performance
  - Support different database management system
- **Hibernate Internal API**: JTA, JDBC, JNDI
---
##  What is the benefit of using Hibernate over JDBC?
JDBC (SQL) | Hibernate (ORM)
---------- | ----------
A Java technology | A Java framework
An implementation of JDBC API | An implimentaion of JPA (Java persistence API)
Need to write everything maunually | Provide build-in features for caching, versioning, time stamping, lazy loadin
Not portable across multiple database software | Portable across multiple database software
JDBS result set is non Serializable obj | Entity class in Hibernate can be Serializable
Exceptions raised by JDBC methods are checked exception | Exception raised by Hibernate are unchecked exception
----
##  JDBC API vs JPA 
JDBC API | Java Persistance API
------ | ----
Lower level and older standard for interacting with database | Higher level standard for the same purpose
Interacting database with pure sql, no notion of obj or hierachy. It's up to us to translate a Result set to a Java obj | Uses Object Relational Mapping, which map object to database table

-----

##  Tell me about some of the JPA annotations you have worked with? What do they do? How do you specify multiplicity relationships with JPA annotations?
--
Annotation was used in model layer
Annotation | What they do
----- | ----
@Entity | Means that class is a table. (Positioned on top of the class)
@Table(name="employee") | Specify table name (Positioned on top of the class)
@Id | On top of a field/property, before @column. It means that column is Primary Key
@Column(name="id") | Specify a column name. On top of a field/property
@GeneratedValue(strategy=GenerationType.AUTO) | to get a serial value. On top of a the field ``private int id;``
@OneToMany(mappedBy="superPrisonHolder", fetch = FetchType.LAZY) | Specify to Hibernate this is One to many relationship

```java
@Entity
@Table(name="Super_Prison")
public class SuperPrison {
	
	@Id
	@Column(name="sp_id")
	@GeneratedValue(strategy = GenerationType.AUTO)
	private int spId;
	
	@Column(name="sp_name")
	private String spName;
	
	@Column(name="sp_location")
	private String location;
	
	@OneToMany(mappedBy="superPrisonHolder", fetch = FetchType.LAZY)
	private List<SuperVillain> villList = new ArrayList<SuperVillain>();

	
	public SuperPrison() {	
	}
  // Getter and Setter

	
```

----
##  What are the interfaces of Hibernate?
Core Interface | What it does
---- | -----
Session | The persistence manager that manages the interaction to DB and execute CRUD (create, read, update, delete). It is not meant to be keep long since it is not thread-safe plus its instances are lightweight and inexpensive to create and destroy. It created in every DAO method and known as persistence obj. It had 3 life cycle: trasient (just instanciated), persistent (had a repesentation in the database and an identifier value, in the scope of a session). Detached: (detached instance had been persistent, but its session had close)
Configuration | gather information from ``hibernate.cfg.xml`` or ``hibernate.properties`` file. Loads mapping and configuration file into memory and makes them available to hibernate engine. It act as factory to create the SessionFactory | 
Session Fatory | Deliver session objects to hibernate application. Intance of it is not lightweight and usually there is only one instance for the whole application unless there is multiple database (need one per database)
Transaction | An optional interface. Define the unit of works. In hibernate, it is better to rollback the transaction if any exception occurs so the resources can be free
```java
try{
  Session session = sessionFactory.openSession();
  Transaction tx = session.beginTransaction();
  // some action
  tx.commit()
} catch (Exception ex){
  ex.printStackTrace()
  tx.rollback()
}

 ```
 Query and criteria | Query Used to write complex CRUD operation using HQL. Criteria used to apply fileration rules and logical condition
 ---- | ---
 ```java
String sql = "SELECT * FROM EMPLOYEE";
SQLQuery query = session.createSQLQuery(sql);
query.addEntity(Employee.class);
List results = query.list();
 ```
 ```java
Criteria cr = session.createCriteria(Employee.class);
// return record with salary equal to 2000
cr.add(Restrictions.eq("salary", 2000));
List results = cr.list();
 ```

##  Tell me how you set up hibernate? What files are you editing, what goes in them, etc.
- Create a maven project and add Hibernate dependency
- Add Hibernate configuration: In resources folder, create hibernate.cfg.xml with JDBC properties name ="hibernate.connection.username", "..password", "..url", driver properties:"...driver_class", "..dialect", "...pool_size", hibernate.hbm2ddl.auto,
- Create org.hibernate.SessionFactory obj
- Make hibernate API call on seesion obj
##  What ways are available to you to map an object to database entities in Hibernate?
    
7.  In the session interface, what is the difference between save and persist methods? get and load methods? Update vs merge methods?
    
8.  What are the different session methods?
    
9.  What is the difference between Eager and Lazy fetching and how to setup either?
    
10.  Under what circumstances would your program throw a LazyInitializationException?
    
11.  What are the 4 ways to make a query using Hibernate?
    
12.  What is HQL? What makes it different from SQL?
    
13.  What is the Criteria API? Can you perform all DDL and DML commands with it? How do Restrictions and Projections work within this API?
    
14.  What is caching? What is the difference between L1 and L2 cache?
- Level 1
  - Session scope
  - Enabled by default (no config)
  - Session.evict() removes one object
  - Session.clear() removes entire cache
  - Session.contains() returns t/f if cached object is available
  
- Level 2
  - SessionFactory scope
  - Not default behavior (must configure w/ 3rd party library like Ehcache)
  - Strategies/Use cases:
    - Read_Only – good for app config, things that are never updated
    - Read_Write – for objects to be updated, only aware of changes through hibernate
    
15.  How do you enable second level caching?
    
16.  Tell me about NamedQueries.
    
17.  Can you write native SQL with Hibernate? Is this a good idea?
    
18.  What are the configuration options for Hibernate?
    
*  How to specify the SQL dialect?
    
*  What data must be specified for the SessionFactory?
    
*  What is hbm2ddl?
    
19.  How would you configure Hibernate to print to the console all SQL statements run?
    
20.  What are the different object states in Hibernate? What methods move objects to different states?
    
21.  What is a proxy? When does the proxy resolve to the real object?

<hr>

# Hibernate Study Guide
The Hibernate framework is a ORM (Object-Relational Mapping) implementation which is built around JDBC.

ORM refers to the long-standing problem of setting up a relationship between a program's objects and rows in a SQL table.

```
class Customer {
    int id;
    String name;
    List<Account>;
}
```
```sql
Create Table Customer(
    id integer primary key,
    name varchar2(50),
    account_id foreign key references Account(id)
    --The above is an issue for mapping
);
```

Map our Java objects to database entities through Hibernate, built on top of JDBC, which will abstract for us all the persistence and transactions that we would normally do ourselves. Hibernate can use interfaces to abstract several different database connections, but can also generate SQL.

## Packages
- org.hibernate
- javax.persistence
    - JPA (Java Persistence API)
    - Generic annotations for ORMs

## Exceptions
- HibernateException
    - RuntimeException which wraps SQLException

## Dependencies
- hibernate-core
- hibernate-entityManager

## JDBC Interfaces vs Hibernate Interfaces
### JDBC
- DriverManager
- Connection
- Statement
- PreparedStatement
- CallableStatement
- ResultSet

### Hibernate
- **Configuration** creates session factories through a specified configuration file or class
- **SessionFactory** is a singleton which generates session objects using a factory design pattern.
    - >SessionFactory sf = new Configuration().configure("file").buildSessionFactory();
- **Session** represents the database connection
    - >Session s = sf.openSession();
    - >s.close();
- **Query** is used to write complex CRUD operations using HQL (Hibernate Query Language)
- **Criteria** is for programmatically writing Select queries
    ```java
    List<Animal> a = session.createCriteria(Animal.class)
        .addOrder(Order.asc("age"))
        .add(Restriction.between("age", 3, 7))
        .list();
    ```
- **Transaction** is an interface for managing ACID-complient transactions
    > Transaction tx = session.beginTransation();
    > //some inserts here
    > tx.commit();

## ACID
ACID is a set of rules to be respected whenever a transaction occures in a SQL database.

1. Atomicity
    - All or nothing approach, either every single line in a transaction succeeds without errors, or none do
1. Consistency
    - Every transaction must leave the database in a consistent state: respecting data, domain, and referential integrity
1. Isolation
    - All transactions that occur concurrently should create the same result in the database as if those transactions occured in series
1. Durability
    - All transactions must be permanent, leaving the database in a committed state that cannot be rolled back or lost

## Mapping with JPA Annotations
- @Entity: marks class for Hibernate
- @Table: maps entity to a table in database
- @Id: maps a property in an entity as a primary key in the database
- @Column: maps a property in an entity as a column in the database
- @JoinColumn: maps a property in an entity as a foreign key in the database

```java
//Student.java
import javax.persistence.*
@Entity
@Table(name=”student”)
public class Student(){
  @Id
  @column(name=”s_id”)
  private Integer studentId;
  
  @column(name=”s_name”)
  private String studentName;
}
```

- Multiplicity
  - @OneToOne
  - @OneToMany: used on parent relation
  - @ManyToOne: used on child relation
  - @ManyToMany

```java
@Entity
@Table(name=”dept”)
public class Department {
  @Id
  @Column(name=”d_id”)
  private Integer id;

  @Column(name=”d_name”)
  private String deptName
}

@Entity
@Table(name=”emp”)
public class Employee {
  @Id
  @Column(name=”e_id”)
  private Integer id;

  @Column(name=”e_name”)
  private String empName;
  
  @ManyToOne
  @JoinColumn(name=”dept_id”)
  private Department dept;
}
```

Alternatively, in Department.java:
```java
@OneToMany(mappedBy=”dept”)
private List<Employee> emps;
```

## Cascades
- By default, no transitive persistence or cascading of state in Hibernate objects with multiplicity relationships
- No default cascading of state or persistence by reachability
- Set up cascade types such as all, none, delete-orphan, etc, in mapping document or in annotation to establish parent/child lifecycle tables, where child lifespan is bounded by parent's lifespan

## Lazy/Eager Fetching
- Eager grabs all information, including associated objects, immediately
- Lazy grabs data only when needed, and creates a proxy in place of associated objects until then
- Proxies can be filled as long as session is open, otherwise a LazyInitializationException is thrown after session closes
- Ex: `@ManyToOne(fetch=FetchType.LAZY)`

## Object States
- Transient
  - Just Instantiated with 'new'
  - Not associated with a session
  - No database representation
- Persistent
  - Has database representation and an identifier
  - Within scope of a session
  - Any changes made in Java will be detected by Hibernate and reflected in database
- Detached
  - Was in a persistent state, but then the session ended
  - Automatic Dirty Checking
  - When connection closes, Hibernate checks for changes in persistent objects and puts all objects in Detached state
  
## Eager vs Lazy Hibernate session CRUD
- Get
  - Immediately (Eagerly) retrieve object from DB
  - Null if object does not exist
- Load
  - Retrieves a proxy (Lazily) which is filled only when used
  - Accessible while session is open

- Save
  - Returns generated PK
  - Immediately inserts regardless of transaction
- Persist
  - Void return type
  - Only inserts during a transaction

- Update
  - Updates object in DB
  - Brings transient object to persistent state
- Merge
  - Checks if object exists
  - Makes persistent object if it doesn't
  - Copies data into new persistent object

- SaveOrUpdate
  - Universal tool for persistent objects
  - If object exists, it will update
  - If not, it will create
  

