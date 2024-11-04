
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

