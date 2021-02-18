# SQL

### Unary, Binary, Tenary, N-ary Relationship Type

The arity of a relationship means The number of entities in a relationship.

Most common relationship types:

- **Unary**: One entity is involved in the relationship

	Ex: 
	. A person is a parent of another person. A person can have many children. This is a **one to many** recursive relationship. 
	. A person is married to other person is a **unary one to one** relationship

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
CREATE TABLE new LIKE original
- Populate the empty table with data in the original table:
INSERT INTO new SELECT * FROM original

### VIEW
- Hide complexity
- Security mechanism: If you have a customer table and you want to give your sales people access to everything accept credit_card_number, you can create a view with only the columns they need to access and grant them permission to access on the view

CREATE OR REPLACE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
- Support legacy code 

### Indexes

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

  Drop index primary key on a table: 

### Query Optimizer
The output from the optimizer is an execution plan that describes an optimum method of execution

### Referental Integrity Rule
- **Set to null delete rule**:
	sets column values in a child table to a missing value when the matching data is deleted from the parent table
- **Restrict delete rule**:
	FOREIGN KEY fk_priv (privacy) REFERENCES privacy_level (level) ON UPDATE CASCADE ON DELETE RESTRICT
	**ON DELETE RESTRICT** means you can't delete a given parent row if a child row that being referenced exists.

- **Default delete rule**
- **Cascade delete rule**