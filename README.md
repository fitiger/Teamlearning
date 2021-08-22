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

### Table create and update

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
### Basic select

## TODO add more details about each function  

- SELECT
  ```sql
  SELECT <col_name> 
  FROM table_name;
  ```
  \* means selecting all columns
- WHERE 
  - Add an condition to query
```sql
-- 想要查询出全部列时，可以使用代表所有列的星号（*）。
SELECT *
  FROM <表名>；
-- SQL语句可以使用AS关键字为列设定别名（用中文时需要双引号（“”））。
SELECT product_id     As id,
       product_name   As name,
       purchase_price AS "进货单价"
  FROM product;
-- 使用DISTINCT删除product_type列中重复的数据
SELECT DISTINCT product_type
  FROM product;
```

```sql
-- SQL语句中也可以使用运算表达式
SELECT product_name, sale_price, sale_price * 2 AS "sale_price x2"
  FROM product;
-- WHERE子句的条件表达式中也可以使用计算表达式
SELECT product_name, sale_price, purchase_price
  FROM product
 WHERE sale_price-purchase_price >= 500;
/* 对字符串使用不等号
首先创建chars并插入数据
选取出大于‘2’的SELECT语句*/
-- DDL：创建表
CREATE TABLE chars
（chr CHAR（3）NOT NULL, 
PRIMARY KEY（chr））;
-- 选取出大于'2'的数据的SELECT语句('2'为字符串)
SELECT chr
  FROM chars
 WHERE chr > '2';
-- 选取NULL的记录
SELECT product_name, purchase_price
  FROM product
 WHERE purchase_price IS NULL;
-- 选取不为NULL的记录
SELECT product_name, purchase_price
  FROM product
 WHERE purchase_price IS NOT NULL;
 ```

### Slect order

FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY

###Task 2 assignment
```sql
-- Q1
SELECT product_name, regist_date
FROM product
WHERE regist_date >= '2009-04-28'
-- Q2
SELECT product_name, sale_price, purchase_price 
FROM product
WHERE sale_price-purchase_price>=500
-- Q3
SELECT product_name, sale_price, product_type, sale_price*0.9 - purchase_price as profit 
FROM product
WHERE (product_type = "办公用品") OR (product_type =  "厨房用具")
AND sale_price*0.9 - purchase_price > 100
-- Q6
SELECT product_type, SUM(sale_price), SUM(purchase_price)
FROM product
GROUP BY product_type
HAVING SUM(sale_price) > 1.5* SUM(purchase_price)
-- Q7
SELECT *
FROM Product
ORDER BY ISNULL(regist_date), regist_date DESC, sale_price;
```

### Task 3 assignment

```sql
-- Q 3.1
CREATE VIEW ViewPractice5_1(product_name, sale_price, regist_date)
AS
SELECT product_name, sale_price, regist_date
FROM product
WHERE sale_price >= 1000
AND regist_date = '2009-09-20';
-- Q 3.3
SELECT product_id,
       product_name,
       product_type,
       sale_price,
       (SELECT AVG(sale_price) FROM Product) AS sale_price_all
FROM Product;
-- Q 3.4
CREATE VIEW AvgPriceByType AS
SELECT product_id,
       product_name,
       product_type,
       sale_price,
       (SELECT AVG(sale_price)
          FROM Product P2
         WHERE P1.product_type = P2.product_type
         GROUP BY P1.product_type) AS avg_sale_price
FROM Product P1;

-- 
SELECT SUM(CASE WHEN sale_price <= 1000 THEN 1 ELSE 0 END)               AS low_price,
       SUM(CASE WHEN sale_price BETWEEN 1001 AND 3000 THEN 1 ELSE 0 END) AS mid_price,
       SUM(CASE WHEN sale_price >= 3001 THEN 1 ELSE 0 END)               AS high_price
FROM Product;
```