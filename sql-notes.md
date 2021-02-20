# SQL

### Unary, Binary, Tenary, N-ary Relationship Type

The arity of a relationship means The number of entities in a relationship.

Most common relationship types:

- **Unary**: One entity is involved in the relationship

	Ex: 
	. A person is a parent of another person. A person can have many children. This is a **one to many** recursive relationship. 
	. A person is married to other person is a **unary one to one** relationship
	. -- From text book: 1 product made of many components and one component can be on many products is a many-to-many Unary relationship.

	3 cases of Unary: 
	. Mandatory-Mandatory: Each instance must fully participate in a relatonship. Ex: 1 person only married 1 person, 2 married persons must have a ring
	. Optional-Optional: Participation of an instance in the group is optional, not mandatory. Ex: one of them can fill a join taxe for both or just let it be and fill seperate taxes
	. Mandatory-Optional or opposite: 1 side must participate while other may or may not. Ex: Only 1 person need to pickup their kids.

- **Binary**: 2 entities is involved in the relationship

	Ex:
	. A person only have 1 driver license. This is a **Binary one to one** relationship 
	. A project can have many students working on it but 1 student can only work on 1 project. This is a **Binary one to many** relationship 
	. A teacher can teaches many students and A student can be taught by many teachers. This is a **Binary many to many** relationship 

- **Tenary**: 3 entities is involved in the relationship
	Ex:
	. A technician can only uses 1 notebook for each project, and that notebook only belong to him/her. This is a **Ternary one to one** relationship 
	. A technician can participate in serveral projects and uses the same notebook**s** writeen by many technicians for each project This is a **Ternary many to many** relationship 


#### SQL data types for images or sounds:
Binary, TinyBlob

### Clone a table
- Includes column attributes and indexes of the original table
```sql CREATE TABLE new LIKE original ```
- Populate the empty table with data in the original table:
```sql INSERT INTO new SELECT * FROM original ```

### VIEW
- Hide complexity
- Security mechanism: If you have a customer table and you want to give your sales people access to everything accept credit_card_number, you can create a view with only the columns they need to access and grant them permission to access on the view
- Support legacy code 

```sql
CREATE OR REPLACE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

```sql
ALTER VIEW HumanResources.EmployeeHireDate  
AS  
SELECT p.FirstName, p.LastName, e.HireDate  
FROM HumanResources.Employee AS e JOIN Person.Person AS p  
ON e.BusinessEntityID = p.BusinessEntityID  
WHERE HireDate < CONVERT(DATETIME,'20020101',101) ; 
```

### Indexes
- Indexes are **special lookup tables** that the database search engine can use to **speed up data retrieval**. Simply put, an index is a **pointer** to data in a table. An index in a database is very similar to an index in the back of a book.
- An index helps to speed up SELECT queries and WHERE clauses, but it slows down data input, with the UPDATE and the INSERT statements
-Basic indexes: ``` CREATE INDEX index_name ON table_name;```
```sql
CREATE [UNIQUE | FULLTEXT | SPATIAL] INDEX index_name
    [index_type]
    ON tbl_name (key_part,...)
    [index_option]
    [algorithm_option | lock_option] ...

key_part:
    col_name [(length)] [ASC | DESC]

index_option: {
    KEY_BLOCK_SIZE [=] value
  | index_type
  | WITH PARSER parser_name
  | COMMENT 'string'
}

index_type:
    USING {BTREE | HASH}

algorithm_option:
    ALGORITHM [=] {DEFAULT | INPLACE | COPY}

lock_option:
    LOCK [=] {DEFAULT | NONE | SHARED | EXCLUSIVE}
```

  - Drop index primary key on a table: ``` DROP INDEX PRIMARY ON table_name; ```
  - Basic drop index: ``` DROP INDEX index_name; ```
  - Create an index to be built on the city field :
``` ALTER TABLE 'Salesperson' ADD INDEX 'city_index' (city); ```

### Query Optimizer
The output from the optimizer is an execution plan that describes an optimum method of execution
The name of the special internal database where the query optimizer finds information is **Relational Catalog**

### Referental Integrity Rule
- **Set to null delete rule**:
	sets column values in a child table to a missing value when the matching data is deleted from the parent table
- **Restrict delete rule**:
	``` FOREIGN KEY fk_priv (privacy) REFERENCES privacy_level (level) ON UPDATE CASCADE ON DELETE RESTRICT ```
	**ON DELETE RESTRICT** means you can't delete a given parent row if a child row that being referenced exists.

- **Default delete rule**: had ophranage record
- **Cascade delete rule**: if a record in the parent table is deleted, then the corresponding records in the child table will automatically be deleted. 
``` sql
   ALTER TABLE child_table
   ADD CONSTRAINT fk_name
   FOREIGN KEY (child_col1, child_col2, ... child_col_n)
   REFERENCES parent_table (parent_col1, parent_col2, ... parent_col_n)ON DELETE CASCADE;
```