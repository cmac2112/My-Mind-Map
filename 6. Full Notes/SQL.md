
2024-10-03 16:43

Status:

Tags:[[Relational Database]]. [[Programming Language]]. [[Web dev book]]

# SQL


`CREATE TRABLE` statement
An [[SQL]] statement is a complete command and is terminated with a semicolon. [[SQL]] uses keywords like CREATE, SELECT, WHERE, and others that are often capitalized but not case sensitive

|Data type|Description|Example|
|---|---|---|
|`CHAR(n)`|Fixed-length character string of length n|`'CODE123'`|
|`VARCHAR(n)`|Variable-length character string with maximum length n|`'Super Bowl'`|
|`BOOLEAN`|TRUE or FALSE|`TRUE`|
|`INTEGER`|Integer number (-2,147,483,648 to 2,147,483,647)|`12345`|
|`FLOAT`|Approximate number with mantissa precision 16|`3.14`|
|`DATE`|Year, month, day: YYYY-MM-DD|`'2010-12-25'`|
|`TIME`|Hour, minute, second: HH:MM:SS|`'14:06:00'`|
|`DATETIME`|Year, month, day, hour, minute, second: YYYY-MM-DD HH:MM:SS|`'2010-12-25 14:06:00'`|

Auto increment columns

Id columns are frequently created as auto-increment columns. An auto-increment column is a columns assigned an automatically incrementing value.
```
CREATE TABLE students (
  stuId INTEGER AUTO_INCREMENT,
  name VARCHAR(45),
  gpa FLOAT,
  PRIMARY KEY (stuId));
```


INSERT statement
[[SQL]] provides four statements (or commands) that perform [[CRUD]] operations on a table

An INSERT statement inserts one or more rows into a table. The values composing the rows are listed after the VALUES keyword

string values must be delimited with single quotation marks

```
INSERT INTO movie VALUES
  (1, 'Rogue One: A Star Wars Story', 'PG-13', '2016-12-10'),
  (2, 'Hidden Figures', 'PG', '2017-01-06'),
  (3, 'Toy Story', 'G', '1995-11-22'),
  (4, 'Avengers: Endgame', 'PG-13', '2019-04-26'),
  (5, 'The Godfather', 'R', '1972-03-14'),
  (6, 'Borat', 'R', '2006-1-11');

```
Inserting with auto-Incrementing columns. The INSERT statement should not specify a value for the auto-increment column.

```
INSERT INTO students (name, gpa) 
VALUES ('MingMing', 2.9);
```

SELECT statement
The SELECT statement retrieves data from a table. The column names listed after SELECT are included in the retrieval result. If * is given as a column name then all columns are selected

The SELECT statement retrieves all rows by default, but the WHERE clause limits the rows are that are retrieved. The WHERE clause works like an if statement in a programming language, specifying conditions that must be true for a row to be selected.

A SELECT statement may use the ORDER BY clause to sort selected rows in ascending (alphabetic) order. SQL also defines a number of functions that may be used in a SELECT statement. Ex: The COUNT() function counts how many rows are returned by a SELECT statement.

Where condition operators

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
LIKE operator performs a [[SQL]] pattern matching where % matches any number of characters

DATEDIFF() returns the number of days between two dates
```
SELECT * 
FROM shows 
WHERE DATEDIFF('2016-08-01', releaseDate) > 365 * 10;
```

## 

Joining data from multiple tables.

Most databases are comprised of multiple tables with relationships between the tables. Ex: The grades table below assigns letter grades to students in each course identified by a courseId. To retrieve the student's name, course ID, and grade of all students requires the students and grades tables be joined. The SELECT statement uses a JOIN clause with an ON clause to join data in multiple tables.

![SELECT statement with JOIN...ON merges data from two tables into a single table.](https://zytools.zybooks.com/zyAuthor/WebProgramming/70/IMAGES/e05d5be7-ddd4-1fb3-8e96-555e20cb606c)

The example above joins the name column from the students table and the courseId and grade columns from the grades table into a single table that matches the stuId columns from both tables. Joins allow developers to write complex queries that answer questions like, "What is the name of the student who performed the best in all courses?" and "Which students were not assigned a passing grade?" Joins are covered in more detail elsewhere in this material.


UPDATE and DELETE statements

The UPDATE statement changes the values of existing rows in the table. The WHERE clause determines which rows are updated\

```
UPDATE song SET title = 'With Or Without You' WHERE title = 'One';
UPDATE song SET artist = 'Aretha Franklin' WHERE artist = 'The Righteous Brothers';
UPDATE song SET release_year = '2021' WHERE release_year > 1990;

```
delete is similar

