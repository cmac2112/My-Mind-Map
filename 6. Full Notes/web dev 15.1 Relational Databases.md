
2024-11-03 18:45

Status:

Tags:[[SQL]], [[Web dev book]], [[Relational Database]]

# web dev 15.1 Relational Databases


Relational databases and tables

Applications often need to store and retrieve large amounts of information. [[Relational Database]]s have been popular for storing data since the 1970's due to the relative simplicity and efficiency that relational databases offer

A [[Relational Database]] stores data about entities. An `entity` is any object that an application wants to store information about. 

Relational databases store entity data in tables

- A `table` is a collection of related entity data that is organized into columns and rows similar to a spreadsheed
- A `column` is a set of values of the same type. Each column has a name, different from other column names in the table
- A `row` is a set of values, one for each column


## Data types
Each column has a data type. Data types vary between relational databases, but 3 common data types include:

1. Chararacter - data that contains one or more characters or symbols.
2. Number - Numeric data that supports arithmetic
3. Date - Calendar dates that can be compared to each other

## keys
Every table must have a primary key, a column or combination of columns that uniquely identifies each row. 

Two tables that have a relationship are linked together using a foreign key, a primary key from one table that is shared in another table. Foreign keys help a database maintain referential integrity, which means that if a foreign key contains a value, the value is guaranteed to exist in the primary key.

## Relationships

Creating a relational database involves mapping entities to tables. A [[relationship]] describes association between entities. Three types of relationships are possible between entities A and B:
1. A `one-to-one relationship` (1:1) means that entity A is associated with only one entity B and vice versa. Ex: one department chair heads one department, and one department can have only one department chair
2. A `one-to-many relationship`(1:M) means that entity A is associated with one or more B entities, and one B entity is associated with only one A entity. Ex: one course can have many classes, but a single class is created from a single course
3. A `many-to-many relationship` (M:N) means that one A entity is associated with many B entities, and one B entity is associated with many A entities. Ex: one student enrolls in many classes, and a single class has many enrolled students
A Linking table links two tables together by creating a primary key that is composed of the foreign keys from the two linked entities. A linking table divides an M:N relationship into two 1:M relationships

# 15.2 Structured Query Language

## RDBMS and SQL

A Relational Database management system is a software that implements a relational database

## [[SQL]] syntax

A [[SQL]] statement is a complete command composed of one or more clauses. A `clause` groups [[SQL]] keywords with table, names, column names, conditions, etc. A [[SQL]] statement may be written on a single line, but good practice is to write each clause on a separate line

```
SELECT last_name
FROM student
WHERE gpa > 3.0

1. The SELECT clause starts the statement.
2. The FROM clause must follow the SELECT clause.
3. The WHERE clause is optional. When included, the WHERE clause must follow the FROM clause.
4. The three clauses ending in a semicolon is a statement.
```

## 

Table 15.2.1: Summary of SQL syntax features.

|Type|Description|Examples|
|---|---|---|
|Literals|Explicit values that are string, numeric, or binary. Strings must be surrounded by single or double quotes. Binary values are represented with `x'0'` where the 0 is any hex value.|'String'<br>"String"<br>123<br>x'0fa2'|
|Keywords|Words with special meaning.|SELECT, FROM, WHERE|
|Identifiers|Objects from the database like tables, columns, etc.|student, last_name, gpa|
|Comments|Statement intended only for humans and ignored by the RDBMS when parsing a SQL statement.|-- single line comment<br><br>/* multi-line <br>   comment */|

# 15.3 Creating, altering, and deleting tables


## create table statement

The `CREATE TABLE` statement creates a new table by specifiying the table name, column names, column data types, and constraints. A `constraint` is a rule that applies to table data. The `PRIMARY KEY` constraint is used in the CREATE TABLE statement to specify the table's primary key

## 

Table 15.3.1: Common data types in MySQL.

|Data type|Description|Example|
|---|---|---|
|`CHAR(n)`|Fixed-length character string of length _n_|`'CODE123'`|
|`VARCHAR(n)`|Variable-length character string with maximum length _n_|`'Super Bowl'`|
|`BOOLEAN`|TRUE or FALSE|`TRUE`|
|`INTEGER` or `INT`|Integer number|`12345`|
|`FLOAT`|Approximate number|`3.1416`|
|`DECIMAL(p, s)`|Precise number where _p_ is precision and _s_ is scale|`5.99`|
|`DATE`|Year, month, day: YYYY-MM-DD|`'2020-12-25'`|
|`TIME`|Hour, minute, second: HH:MM:SS|`'14:06:00'`|
|`DATETIME`|Year, month, day, hour, minute, second: YYYY-MM-DD HH:MM:SS|`'2020-12-25 14:06:00'`|
```
-- Write your CREATE TABLE statement here:
CREATE TABLE product (
id INT,
name VARCHAR(40),
product_type CHAR(3),
origin_date DATE,
weight DECIMAL(5, 1),
PRIMARY KEY(id)
);

INSERT INTO product (id, name, product_type, origin_date, weight) VALUES 
  (100, 'Tricorder', 'COM', '2020-08-11', 2.4),
  (200, 'Food replicator', 'FOD', '2020-09-21', 54.2),
  (300, 'Cloaking device', 'SPA', '2019-02-04', 177.9);

SELECT *
FROM product;
```

## Null values

A `NULL` value is a special value that can mean unknown or nothing.

The NOT NULL constraint, listed by a column name in a CREATE TABLE statement, prevents a column from having a NULL value. The primary key columns do not need a NOT NULL constraint because a primary key cannot be NULL

## Foreign keys

A foreign key constraint is specified using the `FOREIGN KEY` and `REFERENCES` keywords. 

This below creates a faculty table with a dept_code as the foreign key, which references the department table's dept_code column. The foreign key constraint forces the faculty table's dept_code to only use values from the department table dept_code column. 

```
## 

Figure 15.3.3: faculty table with foreign key.

CREATE TABLE faculty (
  fac_id INTEGER,
  last_name VARCHAR(50),
  first_name VARCHAR(50),
  dept_code VARCHAR(4),
  hire_date DATE,
  tenured BOOLEAN,
  PRIMARY KEY(fac_id),
  FOREIGN KEY(dept_code) REFERENCES department(dept_code)
);
```

# auto increment columns

ID columns are frequently created as auto-increment columns. An `auto-increment column` is a column that is assigned an automatically incrementing value.

## Altering and deleting tables

After creating a table, the table can be altered by adding or removing columns or changing a column's data type by using the `ALTER TABLE` statement with the ADD, DROP COLUMN, and MODIFY clauses. The DROP TABLE statement deletes a table along with all the table's rows.

# 15.4 Inserting rows

## INSERT statement

An `insert` statement inserts one or more rows into a table. The column names can be listed in parentheses after the table name, or the names can be omitted if inserted in the same order as the table's columns

## 

Figure 15.4.1: INSERT syntax.

|   |   |
|---|---|
|Column names<br><br>INSERT INTO table_name (column1, column2, column3, ...)<br>VALUES (value1, value2, value3, ...);|No column names<br><br>INSERT INTO table_name<br>VALUES (value1, value2, value3, ...);|

When a table has auto-increment column, the INSERT statement should not specify a value for the auto-increment column. Specifying a value over-writes the automatically assigned value

# 15.5 Selecting rows

SELECT statement

The SELECT statement retrieves data from a table. The data returned from the SELECT  statement is stored in a `result table` the column names listed after "SELECT" are included in the result table. if `*` is given as a column name, then all columns are included in the result table

WHERE clause

The select statement retrieves all rows by default, but the WHERE clause limits the rows that are retrived. The Where clause works like an `if` statement in a programming language, specifying conditions that must be true for a row to be selected



## 

Table 15.5.1: WHERE condition operators.

|Operator|Description|Example|
|---|---|---|
|`=`|Compares two values for equality|`1 = 2` is false|
|`!=`|Compares two values for inequality|`1 != 2` is true|
|`<`|Compares two values with <|`2 < 2` is false|
|`<=`|Compares two values with ≤|`2 <= 2` is true|
|`>`|Compares two values with >|`3 > 3` is false|
|`>=`|Compares two values with ≥|`3 >= 3` is true|
|`AND`|Performs logical AND between two conditions|`1 > 2 AND 2 < 3` is false|
|`OR`|Performs logical OR between two conditions|`1 > 2 OR 2 < 3` is true|
|`NOT`|Negates a condition|`NOT 1 > 2` is true|

## Like operator

A where clause performs exact string comparison with the equality operator (=) but the LIKE operator matches text against a patter using the two wildcard characters % and underscore

- % matches any number of characters
- underscore matches exactly one character

# 15.6 [[SQL]] functions

Aggregate functions

RDBMS provide a wide range of [[SQL]] functions that work with or manipulate numbers, string, dates, and times. an `aggregate function` is a function that works on a group of values. Some common aggregate functions include:

- Count() - counts the number of rows retrieved by a SELECt statement
- MIN() - finds the min value in a group
- MAX() - find the max val in a group
- SUM() - sums all values in a group
- AVG() - finds the arithmetic mean of all the values in a group

aggregate functions my be used with the GROUP BY clause, which groups results using one or more columns.

The HAVING clause is used with the GROUP BY clause to filter group results.


# 15.7 Joining tables

Join types

A [[SQL]] join in a SELECT statement that joins information from two tables into a single result.

![[Pasted image 20241103205235.png]]

Inner Join

in a SELECT statement, the FROM clause indicates the left table, the JOIN clause indicates the right table, and the ON clause specifies the join condition. An INNER JOIN clause performs an inner join, joining all rows from the left and right tables where the join condition is met.

```
SELECT column1, column2, ...
FROM left_table_name
INNER JOIN right_table_name
ON condition;
```

Outer joins

the following sql join clauses perofmr left, right, and full outer joins

LEFT OUTER JOIN clause - Joins al lrows from the left table along with rows from the right table where the join condition is met

RIGHT OUTER JOIN clause - Joins all rows from the right table along with rows from the left table where the join conditions met

FULL OUTER JOIN clause - Joins all rows from the left and right tables regardless if the join condition is met

# 15.8 Updating and deleting rows

UPDATE statement

An UPDATE statement changes the values of existing rows in the table. The WHERE clause determines which rows are updated

```
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

DELETE statement

removes rows from a table. The WHERE clause determines which rows are removed. If no where clause is specified, all rows are removed

```
DELETE FROM table_name 
WHERE condition;
```
