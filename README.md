# This is a repo for TeamLearning SQL

This is a cheatsheet.

## Introduction  

Database Management System(DBMS) mainly have 5 different types:

- Hierarchical Database
- Relational Database
- Object Oriented Database
- XML Database
- Key-Value Store e.g. MongoDB

SQL Standard:

- Data Definition Language (DDL)
  - create or delete database/table/object
  - Create, Drop, Alter
- Data Manipulation Language (DML)
  - query or change data in table
  - Select, insert, update, delete
- Data Control Language (DCL)
  - permission grant or change confirm
  - Commit, Rollback, Grant, Revoke

### SQL style guide  

[style guide](https://www.sqlstyle.guide/)
At least, read the general and naming conventions parts.


### Table manipulation

Create table
```sql
CREATE TABLE product
(product_id CHAR(4) NOT NULL,
 product_name VARCHAR(100) NOT NULL,
 product_type VARCHAR(32) NOT NULL,
 sale_price INTEGER ,
 purchase_price INTEGER ,
 regist_date DATE ,
 PRIMARY KEY (product_id));
```

Delete table
```sql
DROP product;
```

Update table info
```sql
ALTER TABLE <table_name> ADD COLUMN <column_definition>;
```

Insert data
```sql
INSERT INTO <table_name> (c1, c2, c3, ……) VALUES (v1, v2, v3, ……);  
```
