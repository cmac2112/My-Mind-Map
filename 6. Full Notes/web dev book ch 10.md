
2024-10-02 15:56

Status:

Tags:[[SQL]],[[Node.js]],[[Relational Database]],[[Non-relational Database]],[[JavaScript]],[[JSON]],[[MongoDB]], [[Web dev book]]

# web dev book ch 10


# 10.1 Full-stack development (node)
full stack development

Web Hosting 
When creating a web application developers must decide where the application and application data are going to be hosted.

- Reliability - web hosting companies guarantee a certain level of uptime
- Flexibility - Websites that become popular may need to quickly scale up to handle more users. Web hosting companies may offer virtual private server that can quickly be duplicated on other servers to meet high demand. A VPS is an autonomous server that is hosted on a physical server with other virtual servers.
- Security - hackers may attempt to access a website's data or upload malware to a hosted website that attacks it.
- Price - some web hosting companies offer limited services for free and subsidize lost income with advertising.

Databases

Websites and web applications normally store and retrieve information from a database and have traditionally used relational databases.

A [[Relational Database]] stores data in relations (tables). The Structured Query Language [[SQL]] is a language for creating, editing, selecting, and deleting data in relational database.

[[Non-relational Database]], sometimes called non-sql databases, have been becoming increasingly popular over the last few years. Non-relational databases use different methods to store and retrieve data using a variety of data access languages.

Non relational databases come in several flavors
- Document database: For storing documents in [[JSON]] format with many levels of nesting
- Key-value database: for storing values that are associated with unique keys: ex redis
- object database: for storing objects created in object-oriented programming languages ex: cache
- column database: For storing and processing large amounts of data using pointers that link to columns distributed over a cluster ex: HBase
- Graph database: For storing graph structures with nodes and edges Ex: neo4j

# 10.2 getting started with [[Node.js]]

Node
Node.js is a [[JavaScript]] runtime environment that is primarily used to run server side web applications. Node has many benefits

- Event driven, non-blocking i/o architecture of [[Node.js]] to handle heigh loads
- [[Node.js]] allows developers to write [[JavaScript]] on the server and client, simplifying development tasks
- [[Node.js]] provides a simple mechanism to create and distribute modules. A [[Node.js]] [[module]] is a [[JavaScript]] file that provides some useful functionality
- [[Node.js]] works seamlessly with [[MongoDB]], a document database that stores [[JSON]] and uses [[JavaScript]] as a query language. 

Creating a simple web server

the http [[modules]] allows a [[Node.js]] application to create a simple web server. The http module's `createServer()` method creates a webserver that can receive http requests and send http responses. The `listen()` method starts the server listening for http requests on a particular port.
```

// server.js
const http = require("http");

http.createServer(function(request, response) {    
   response.writeHead(200, {"Content-Type": "text/html"});
   response.write("<h1>Hello, Node.js!</h1>");
   response.end();
   }).listen(3000)
   ```
   1. server.js is executed from the command line.
2. The require("http") command imports the "http" module.
3. createServer() creates a web server object that calls the provided callback function when an HTTP request is received.
4. listen() starts the web server listening on port 3000 for HTTP requests.
5. The user enters a URL to access the web server running on the same machine on port 3000.
6. The HTTP request is routed to the web server, causing the request callback function to execute.
7. writeHead() creates an HTTP response with a 200 status code and text/html content type.
8. write() sends the HTML to the HTTP response object.
9. end() sends the HTTP response to the web browser, which renders the HTML.

A Package is a directory containing one or more modules and a package.json file. A package.json file containes [[JSON]] that lists the package's name, version,license,dependencies, and other package metadata

Node Package Manager (npm) is the package manager for nodejs that allows developers to download,install, and update packaged modules. npm is install with nodejs and is executed from the command line

Nodemon is a utility that saves time by restarting a Node.js application whenever the files in a project are modified

## 

Table 10.2.1: Summary of npm commands.

|Command|Description|Example|
|---|---|---|
|`config`|Manage npm configuration files|npm config list <br>npm config get prefix|
|`install`|Install package locally or globally (-g)|npm install nodemon -g|
|`list`|List all installed local or global (-g) packages|npm list|
|`update`|Update a local or global (-g) package|npm update lodash|
|`uninstall`|Uninstall a local or global (-g) package|npm uninstall lodash|

A package-lock.json file is created or modified when project dependencies are added or removed. The file ensures that the same dependency versions are always used when the project is installed on different machines.

# 10.3 [[Express]]

Express server
Express is a popular web application framework for [[Node.js]] because [[Express]] allows developers to create web servers with less code.

Routes
Express uses routing to handle browser requests. An express [[route]] is a specific [[URL]] path and an http request method to which a callback function is assigned. A route's callback function has request and response parameters, which represent the http request and response

A route is defined with the structure: `app.method(path, callback)`
- `app` - express instance
- `method` - HTTP request method (get, post, etc)
- `path` - [[URL]] path
- `callback` - callback function executed when the route matches

```
// Called for GET request to http://localhost:3000/hello
app.get("/hello", function(req, res) {
   res.send("<h1>Hello, Express!</h1>");
});

// Called for POST request to http://localhost:3000/goodbye
app.post("/goodbye", function(req, res) {
   res.send("<h1>Goodbye, Express!</h1>");
});
```

Middleware
A middleware function is a function that examines or modifies the request and/or response objects. A middleware function has three parameters
- `req` - HTTP request object
- `res` - HTTP response object
- `next` - Callback to the middleware function
```
const express = require("express");
const app = express();

const logRequest = function(req, res, next) {
   console.log(`Request: ${req.method} for ${req.path}`);
   next();
};

app.use(logRequest);

app.get("/hello", function(req, res) {
   res.send("<h1>Hello, Express!</h1>");
});

app.listen(3000, function() {
   console.log("Listening on port 3000...");
```

## 

Table 10.3.1: Popular third-party middleware for Express.

|Middleware|Description|
|---|---|
|morgan|Logs HTTP request information|
|cookie-parser|Parses the cookie header in an HTTP request|
|errorhandler|Aids debugging during development|
|csurf|Protects against cross-site request forgery (CSRF)|
|compression|Compresses response bodies|
|express-session|Manages session data on the server|


# 10.4 [[Express]] request data

Query String Parameters

Express automatically parses query string parameters (values appearing after the ? in a [[URL]]) and stores the parameters names and values in the req.query object

url: http://localhost:3000/hello?name=Bob&age=21

```

app.get("/hello", function(req, res) {
   const html =
      `<h1>Hello, ${req.query.name}!</h1>
       <p>You are ${req.query.age} years old.</p>`;
  
   res.send(html);
});
```

Posting form data

when a form posts data to an [[Express]] route, the form's data is URL-encoded and sent in the body of the HTTP request. The `express.urlencoded()` method is middleware that parses URL-encoded data in a request body and adds the parsed values to the `req.body` object.


```
<form method="post" action="/hello">
  <p>
     <label>Name? <input type="text" name="name"></label>
  </p>
  <p>
     <label>Age? <input type="number" name="age"></label>
  </p>
  <input type="submit" value="Submit">
</form>


http://localhost:3000/hello.html

const express = require("express");
const app = express();

app.use(express.static("public"));

app.use(express.urlencoded({extended: false}));

app.post("/hello", function(req, res) {
   const html = `<h1>Hello, ${req.body.name}!</h1>
      <p>You are ${req.body.age} years old.</p>`;
   res.send(html);
});

app.listen(3000);
```
1. Express is configured to serve files in the "public" directory.
2. express.urlencoded() returns middleware that only parses HTTP request bodies when Content-Type: application/x-www-form-urlencoded is present in the header.
3. The web browser requests hello.html from the Express server and renders the webpage.
4. The user enters her name and age and presses Submit. A POST request with the user's name and age is sent to the Express server.
5. The middleware decodes posted data from the HTTP request body and attaches the data to req.body.
6. The request is posted to the /hello route callback function, which returns a response saying hello to the user.


Route Parameters
Express applications often use routes with data in the [[URL]] path to generate dynamic webpages. A `route parameter` is a string near or at the end of the [[URL]] path that specifies a data value. A route parameter's name is defined in the route path with a colon(:) before the parameter name

Ex: the route path "/users/:username", "username" is a route parameter's name. Route parameters are attached to the `req.params` object

Route parameter middleware

The [[Express]] object's `param()` method defined parameter middleware that executes before a route's callback function. The middleware function has a fourth parameter that contains the value assigned to the route parameter

The figure below shows the username parameter being examined in the parameter middleware. If the username is "jblack", the user's name is "Jack Black". Otherwise, the user's name is unknown. The `req` object is modified to contain a `user` object with properties `name` and `username`. A real-world application would replace the if-else statement with a database query that looks up names and usernames from a database.

```
// Parameter middleware executes before the route
app.param("username", function(req, res, next, username) {

   // Check if username is recognized
   if (username === "jblack") {
      req.user = { name: "Jack Black", username: username };
   } 
   else {
      req.user = { name: "Unknown", username: username };
   }

   // Continue processing the request
   next();
});

app.get("/users/:username", function(req, res) {

   // req.user contains the user info set in the parameter middleware
   res.send("<h1>Profile for " + req.user.name + "</h1>");
```


# 10.5 Pug

Template Engines

A Template engine creates dynamic webpages by replacing variables in a template file with specific values, creating HTML that is sent to the web browser.

## 

Table 10.5.1: Summary of Pug syntax.

|Description|Pug example|Rendered HTML|
|---|---|---|
|HTML doctype|doctype|<!DOCTYPE html>|
|Nesting tags|ol <br>   li Pug uses indentation <br>      em to embed tags inside<br>   li each other.|<ol><br>   <li>Pug uses indentation <br>      <em>to embed tags inside</em></li><br>   <li>each other.</li><br></ol>|
|Displaying text|p <br>   \| A pipe at the beginning of each line<br>   \| displays raw text.|<p>A pipe at the beginning of each line<br>displays raw text.</p>|
|Displaying lots of text|p. <br>   The period is the simplest way to include <br>   multiple lines of text because no pipe is<br>   required before each line.|<p>The period is the simplest way to include <br>multiple lines of text because no pipe is<br>required before each line.</p>|
|Tag attributes|div(style="width:400px")<br>   img(src="dog.jpg", alt="Barking dog")|<div style="width:400px"><br>   <img src="dog.jpg" alt="Barking dog"><br></div>|
|ID attribute|h1#headline Pug is everywhere!<br>#options div is the default tag|<h1 id="headline">Pug is everywhere!</h1><br><div id="options">div is the default tag</div>|
|Class attribute|span.important Read this first!<br>div.highlight.pull-right|<span class="important">Read this first!</span><br><div class="highlight pull-right"></div>|
|Comments|// Comment is visible in HTML<br>//- Invisible comment|<!--Comment is visible in HTML-->|

# 10.6 Relational databases and SQL (node)

Introduction to relational databases

Web applications often store data in [[Relational Database]] or [[Non-relational Database]]s. Relational databases have been popular since the 1970s due to the realtive simplicity and efficiency that relational databases offer

Notes in [[SQL]]



# 10.7 MySQL (Node)

Mysql is a popular Relational Database Management System that offers an open source version and a few commercial versions that provide additional functionality


mysql tool

the mysql command-line tool is a command line program that allows developers to connect to a MySQL server, perform administrative functions, and execute [[SQL]] statements.

access this tool under mysql command line client in windows search

```
mysql> create database test;
Query OK, 1 row affected (0.00 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| test               |
+--------------------+
1 rows in set (0.01 sec)

mysql> use test;
Database changed
```


## 

Figure 10.7.2: Creating a table and showing all the tables in the test database.
```
mysql> create table students (stuId int, name varchar(45), gpa float, primary key (stuId));
Query OK, 0 rows affected (0.37 sec)

mysql> show tables;
+----------------+
| Tables_in_test |
+----------------+
| students       |
+----------------+
1 row in set (0.00 sec)
```

## 

Figure 10.7.3: Inserting, selecting, and updating a student.
```

mysql> insert into students values (123, 'Susan', 3.1);
Query OK, 1 row affected (0.08 sec)

mysql> select * from students;
+-------+-------+------+
| stuId | name  | gpa  |
+-------+-------+------+
|   123 | Susan |  3.1 |
+-------+-------+------+
1 row in set (0.00 sec)

mysql> update students set gpa = 2.5 where stuid = 123;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```



# 10.8 mysql module

Installing and connectiong

The mysql module allows [[Node.js]] applications to interface with a MySQL database. The MySQL module is installed with the command: `npm install mysql`

The `mysql.createConnection()` method creates a connection object using an object parameter that specifies the hostname of the computer running MySQL, the developer's username and password, and the database to select

The connection object provides methods to interact with the MySQL server. The connection object's `connect()` method attempts to establish the database connection.

```
const mysql = require("mysql");

const conn = mysql.createConnection({
   host:     "localhost",
   user:     "myusername",
   password: "mypassword",
   database: "test"
});

conn.connect(function(err) {
   if (err) {
      console.log("Error connecting to MySQL:", err);
   }
   else {
      console.log("Connection established");
   }
});
```

SELECT statement

After establishing a connection with the MYSQL server, [[SQL]] statements can be executed using the connection object's `query()` method which has two parameters
1. a [[SQL]] statement
2. a callback function with two parameters
	2a. An error object that is set if an error occurs
	2b. Results of the [[SQL]] statement

```
const sql = "SELECT stuId, name, gpa FROM students";
conn.query(sql, function(err, rows) {
   if (err) {
      console.log("ERROR:", err);
   }
   else {
      // Loop through all the rows returned from SELECT statement
      rows.forEach(function(row) {
         console.log(row.name + " = " + row.gpa);
      });
   } 
});
```


Connection pool

A Node.js application may keep a connection to the database open the entire time the Node.js application is running. However, database connections are often terminated by the MySQL server at periodic intervals or when the MySQL server is restarted. A developer can use a connection pool to circumvent connection timeouts and to enable Node.js applications to execute more than one SQL command at a time. More about the connection pool can be found in the [mysql module documentation](https://github.com/felixge/node-mysql#pooling-connections).


Query with values array
The `query()` method accepts an optional values array, which holds values that are substituted for "?" characters in a [[SQL]] statement

```
conn.query("SELECT name, gpa FROM students WHERE gpa >= ? OR name = ?", [3.0, "Bob"], 
    function(err, rows) {
       ...
});
```
1. The optional values array contains data to be inserted into the SQL statement.
2. Array values are matched to "?" characters in the SQL query.
3. SQL query with substituted values is sent to MySQL.

```
app.get("/students", function(req, res) {

   // Get values from the query string
   const minGpa = req.query.min;
   const maxGpa = req.query.max;

   // Get ordered list of students by gpa
   conn.query("SELECT name, gpa FROM students WHERE " +
      "gpa >= ? and gpa <= ? ORDER BY gpa DESC", 
      [minGpa, maxGpa], function(err, rows) {
                
      if (err) {
         console.log("ERROR:", err);
      } 
      else {
         // Produce ordered list of students
         let html = "<ol>";
         rows.forEach(function(row) {
            html += "<li>" + row.name + " = " + row.gpa + "</li>";
         });
         html += "</ol>";
         res.send(html);
      }
   });

```
Web applications that use input from a user in an SQL statement are susceptible to SQL injection attacks. A SQL injection attack is when a malicious user enters input into a web application that alters the intent of a SQL statement. SQL injection attacks can lead to sensitive data being divulged or deleted. The mysql module's behavior of substituting values into a SQL statement helps circumvent SQL injection attacks.

INSERT statement

the `query()` method's values aarray may also be a map containing column names and values, which is helpful when executing an INSERT statement with a SET clause. 


```
## 

Figure 10.8.3: query() uses INSERT with map.

const student = { stuId: 777, name: "Maria", gpa: 3.3 };
conn.query("INSERT INTO students SET ?", student, function(err, result) {
   if (err) {
      if (err.errno === 1062) {
         console.log("Cannot insert duplicate ID " + student.stuId);
      } 
      else {
         console.log("ERROR:", err);
      }
   }
   else {
      console.log("Inserted " + result.affectedRows + " row");   // Success!
   }
});
```

UPDATE and DELETE statements

when the `query()` method executes UPDATE and DELETE statements, result.affectedRows contains the number of rows that were affected by the UPDATE or DELETE

```
conn.query("UPDATE students SET gpa = ? WHERE stuId = ?", [2.8, 777], function(err, result) {
   if (err) {
      console.log("ERROR:", err);
   } 
   else {
      console.log("Updated " + result.affectedRows + " rows");
   }
});
```
```
## 

Figure 10.8.7: .query() method executing a DELETE statement.

conn.query("DELETE FROM students WHERE stuId = ?", [777], function(err, result) {
   if (err) {
      console.log("ERROR:", err);
   } 
   else {
      console.log("Deleted " + result.affectedRows + " rows");
   }
});
```

# 10.9 [[MongoDB]]

MongoDB document database

[[Node.js]] web applications may use relational or non-relational (nosql) databases to store web application data. MongoDB is the most popular NoSQL database used by [[Node.js]] developers, [[MongoDB]] stores data objects as documents inside of a collection

- a Document is a single data object in a [[MongoDB]] database that is composed of field/value pairs, similar to [[JSON]] property/value pairs
- a Collection is a group of related documents in a [[MongoDB]] database
[[MongoDB]] stores documents internally as BSON documents (binary json)
BSON types include string, integer, double, date, boolean, null, and others

Inserting Documents
the `insertOne()` collection method inserts a single document into a collection. The `insertMany()` collection method inserts multiple documents into a collection

command line
```
mydb> db.students.insertOne({ name: "Sue", gpa: 3.1 })
{
  acknowledged: true,
  insertedId: ObjectId("62794229fc4ebd4933877a9d")
}

mydb> students = [
... { name: "Maria", gpa: 4.0 },
... { name: "Xiu", gpa: 3.8 },
... { name: "Braden", gpa: 2.5 } ]

mydb> db.students.insertMany(students)
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("627942f6fc4ebd4933877a9e"),
    '1': ObjectId("627942f6fc4ebd4933877a9f"),
    '2': ObjectId("627942f6fc4ebd4933877aa0")
  }
}

mydb> db.students.find()
[
  { _id: ObjectId("62794229fc4ebd4933877a9d"), name: 'Sue', gpa: 3.1 },
  { _id: ObjectId("627942f6fc4ebd4933877a9e"), name: 'Maria', gpa: 4 },
  { _id: ObjectId("627942f6fc4ebd4933877a9f"), name: 'Xiu', gpa: 3.8 },
  { _id: ObjectId("627942f6fc4ebd4933877aa0"), name: 'Braden', gpa: 2.5 }
]
```

The __id field is automatically assigned to every document and is always the first field in the document. The __id acts as a primary key. A primary key is a field that uniquely identifies eaach document in a collection.


Finding Documents
the `find()` collection method returns all documents by default or documents that match an optional query parameter. The `findOne()` collection method returns only the frist document matching the query. Both methods return null if the query matches no documents

```
## 

Figure 10.9.2: Find 'Sue' and students with GPA ≥ 3.0.

mydb> db.students.find({ name: 'Sue' })
[
  { _id: ObjectId("62794229fc4ebd4933877a9d"), name: 'Sue', gpa: 3.1 }
]

mydb> db.students.find({ gpa: { $gte: 3.0 } })
[
  { _id: ObjectId("62794229fc4ebd4933877a9d"), name: 'Sue', gpa: 3.1 },
  { _id: ObjectId("627942f6fc4ebd4933877a9e"), name: 'Maria', gpa: 4 },
  { _id: ObjectId("627942f6fc4ebd4933877a9f"), name: 'Xiu', gpa: 3.8 }
]
```



## 

Table 10.9.1: Common MongoDB query operators.

|Operator|Description|Example|
|---|---|---|
|`field:value`|Matches documents with fields that are equal to the given value.|// Matches student with this _id<br>{ "_id" : ObjectId("62794229fc4ebd4933877a9d") }|
|`$eq`     `$ne`|Matches values = or ≠ to the given value.|// Matches all docs except Sue<br>{ name: { $ne: "Sue" } }|
|`$gt`     `$gte`|Matches values > or ≥ to the given value.|// Matches students with gpa > 3.5<br>{ gpa: { $gt: 3.5 } }|
|`$lt`     `$lte`|Matches values < or ≤ to the given value.|// Matches students with gpa <= 3.0<br>{ gpa: { $lte: 3.0 } }|
|`$in`     `$nin`|Matches values in or not in a given array.|// Matches Sue, Susan, or Susie<br>{ name: { $in: ["Sue", "Susan", "Susie"] } }|
|`$and`|Joins query clauses with a logical AND, returns documents that match both clauses.|// Matches student with gpa >= 3.0 and gpa <= 3.5<br>{ $and: [{ gpa: { $gte: 3.0 } }, <br>         { gpa: { $lte: 3.5 } }] }|
|`$or`|Joins query clauses with a logical OR, returns documents that match either clauses.|// Matches students with gpa >= 3.9 or gpa <= 3.0<br>{ $or: [{ gpa: { $gte: 3.9 } }, <br>        { gpa: { $lte: 3.0 } }] }|

Updating Documents

The `updateOne()` collection method modifies a single document in a collection. `updateMany()` does multiple

The methods have two required parameters
1. query - The query to find the documents to update. An empty query ({}) matches all document
2. update - the modification to perform on matched documents using an update operator like $inc, $set, and $unset

```
## 

Figure 10.9.3: Change Sue's GPA to 3.3, and set all students with GPA > 3 to 1.

mydb> db.students.updateOne({ name: 'Sue' }, { $set: { gpa: 3.3 } })
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

mydb> db.students.find({ name: 'Sue' })
{ "_id" : ObjectId("5e600d18bbd10ee972f6ed9a"), "name" : "Sue", "gpa" : 3.3 }

mydb> db.students.updateMany({ gpa: { $gt: 3 } }, { $set: { gpa: 1 } })
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 3,
  modifiedCount: 3,
  upsertedCount: 0
}

mydb> db.students.find()
[
  { _id: ObjectId("62794229fc4ebd4933877a9d"), name: 'Sue', gpa: 1 },
  { _id: ObjectId("627942f6fc4ebd4933877a9e"), name: 'Maria', gpa: 1 },
  { _id: ObjectId("627942f6fc4ebd4933877a9f"), name: 'Xiu', gpa: 1 },
  { _id: ObjectId("627942f6fc4ebd4933877aa0"), name: 'Braden', gpa: 2.5 }
]
```




## 

Table 10.9.2: Common MongoDB update operators.

|Operator|Description|Example|
|---|---|---|
|`$currentDate`|Sets a field's value to the current date/time|// Sue's "birthDate" : ISODate("2022-05-09T16:39:00.121Z")<br>db.students.updateOne({ name: 'Sue' },<br>   { $currentDate: { birthDate: true } })|
|`$inc`|Increments a field's value by the specified amount|// Sue's "gpa" incremented from 3.1 to 3.2<br>db.students.updateOne({ name: 'Sue' },<br>   { $inc: { gpa: 0.1 } })|
|`$rename`|Renames a field|// Sue's "name" is now "firstName"<br>db.students.updateOne({ name: 'Sue' },<br>   { $rename: { name: 'firstName' } })|
|`$set`|Sets a field's value|// Sue's "gpa" : 4.0<br>db.students.updateOne({ name: 'Sue' },<br>   { $set: { gpa: 4.0 } })|
|`$unset`|Removes a field|// Removes Sue's "gpa" and "birthDate" fields<br>db.students.updateOne({ name: 'Sue' },<br>   { $unset: { gpa: "", birthDate: "" } })|

Deleting documents

the `deleteOne()` collection method deletes a single document from a collection. The `deleteMany()` deletes multiple

```
## 

Figure 10.9.4: Delete the first student with GPA < 3.5 (Sue), and delete all students with GPA > 3.5 (Maria and Xiu).

mydb> db.students.deleteOne({ gpa: { $lt:3.5 } })
{ acknowledged: true, deletedCount: 1 }

mydb> db.students.find()
[
  { _id: ObjectId("627942f6fc4ebd4933877a9e"), name: 'Maria', gpa: 4 },
  { _id: ObjectId("627942f6fc4ebd4933877a9f"), name: 'Xiu', gpa: 3.8 },
  { _id: ObjectId("627942f6fc4ebd4933877aa0"), name: 'Braden', gpa: 2.5 }
]

mydb> db.students.deleteMany({ gpa: { $gt:3.5 } })
{ acknowledged: true, deletedCount: 2 }

mydb> db.students.find()
[
  { _id: ObjectId("627942f6fc4ebd4933877aa0"), name: 'Braden', gpa: 2.5 }
]
```

# 10.10 Mongoose

Schemas and models

A [[Node.js]] application using [[MongoDB]] may use the mongodb module to interact with a [[MongoDB]] database using many of the same functions supported in the mongo shell. Mongoose simplifies [[MongoDB]] operations

Mongoose module provides object data mapping and structured schemas to [[MongoDB]]

supported data types
- `String` - "string"
- `Number` - Integers or floating-point numbers
- `Date` - Date and time
- `Buffer` - Binary data
- `Boolean` - `true` or `false`
- `Mixed` - Any kind of data
- `ObjectId` - MongoDB `ObjectId`
- `Array` - Array of any data type. Ex: `[Number]`.
```
## 

Figure 10.10.1: Mongoose schema for a student.

const mongoose = require("mongoose");

const studentSchema = new mongoose.Schema({
   name:      String,
   gpa:       { type: Number, min: 0, max: 4 },
   birthDate: { type: Date, default: Date.now },
   interests: [ String ]
});
```

Saving Documents

Mongoose provides a collection of methods for implementing [[CRUD]] operations.

- Document.save() - saves the document to a [[MongoDB]] database. The given callback function is executed after the save operation has completed
- Model.create() - saves a single document or array of documents to a [[MongoDB]] database


```
const express = require("express");
const mongoose = require("mongoose");

mongoose.connect("mongodb://localhost/mydb");

const studentSchema = new mongoose.Schema({
   name:          { type: String, required: true },
   gpa:           { type: Number, min: 0, max: 4 },
   birthDate: { type: Date, default: Date.now },
   interests: [ String ]
});

const Student = mongoose.model("Student", studentSchema);

const app = express();

app.get("/create", function(req, res) {
   const stu = new Student({
      name: "Sue Black",
      gpa: 3.1,
      birthDate: "1999-11-02",
      interests: ["biking", "reading"]
   });

   stu.save(function(err, stu) {
      res.send("Sue with id " + stu._id +
         " was saved.");  
   });  
});

app.listen(3000);
```
1. The express and mongoose modules are loaded.
2. Mongoose connects to the "mydb" database on MongoDB running on the local machine.
3. The student schema and model are created.
4. Express app defines the "/create" route and starts listening on port 3000.
5. When the browser requests the "/create" route, the server creates a new Student object from the Student model.
6. stu.save() saves the student object as a document in the mydb database where a new ObjectId is assigned to _id.
7. The Express server sends a response to the browser with Sue's ID.

## 

Table 10.10.1: Common Mongoose find methods.

|Method|Description|Example|
|---|---|---|
|`Model.find(conditions, [callback])`|Finds all documents that match the conditions.|// Find all students with gpa >= 3<br>Student.find({ gpa: { $gte: 3 }}, <br>   function(err, students) {<br>      console.log(students);<br>   }<br>);|
|`Model.findOne(conditions, [callback])`|Finds the first document that match the conditions.|// Find first student with "black" somewhere in the name<br>Student.findOne({ name: new RegExp("black", "i") }, <br>   function(err, stu) {<br>      if (stu === null) {<br>         console.log("No student found");<br>      } <br>      else {<br>         console.log(stu);<br>      }<br>   });|
|`Model.findById(id, [callback])`|Finds the document that matches the id.|// Find the student with this ObjectId<br>Student.findById("56e0ad2301c0b1ea806cadcd", <br>   function(err, stu) {<br>      if (stu === null) {<br>         console.log("No student found");<br>      } <br>      else {<br>         console.log(stu);<br>      }<br>   });|


All Mongoose find methods return a Query object. The `Query` object has a number of methods that may be chained to create a more readable query. Example methods include:

- The Query.where() method specifies a path to filter documents.
- The Query.sort() method sets the sort order.
- The Query.limit() method limits the number of documents returned.
- The Query.exec() method is called last to execute the query and provides a callback function that is called after the query executes.

## 

Table 10.10.2: Common Mongoose update methods.

|Method|Description|Example|
|---|---|---|
|`Model.updateOne(conditions, update, [options], [callback])`|Updates the first document that matches the conditions.|// Change Sue's birthDate to 1995-12-02<br>Student.updateOne({ name: "Sue Black" }, <br>   { birthDate: new Date(1995, 11, 2) },<br>   function(err, result) {<br>      console.log("Docs updated: " + <br>         result.modifiedCount);<br>   });|
|`Model.updateMany(conditions, update, [options], [callback])`|Updates all documents that match the conditions.|// Add 0.5 to all GPAs <= 3.5<br>Student.updateMany({ gpa: { $lte: 3.5 } }, <br>   { $inc: { gpa: 0.5 } },<br>   function(err, result) {<br>      console.log("Docs updated: " + <br>         result.modifiedCount);<br>   });|
|`Query.updateOne([conditions], [update], [options], [callback])`|Updates the first document that matches the optional conditions.|// Change this student's GPA to 3.9<br>Student.where({ _id: "56e711a9e1b0f9080f7a5621" })<br>   .updateOne({ $set: { gpa: 3.9 } })<br>   .exec(function(err, result) {<br>      console.log("Docs updated: " + <br>         result.modifiedCount);<br>   });|
|`Query.updateMany([conditions], [update], [options], [callback])`|Updates all documents that match the optional conditions.|// Set all GPAs <= 3.5 to 2<br>Student.where({ gpa: { $lte: 3.5 } })<br>   .updateMany({ $set: { gpa: 2 } })<br>   .exec(function(err, result) {<br>      console.log("Docs updated: " + <br>         result.modifiedCount);<br>   });|
## 

Table 10.10.3: Common Mongoose delete methods.

|Method|Description|Example|
|---|---|---|
|`Model.deleteOne(conditions, [callback])`|Deletes the first document that matches the conditions.|// Delete student with given id<br>Student.deleteOne({ _id: "56e711a9e1b0f9080f7a5621" }, <br>   function(err, result) {<br>      console.log("Deleted " + <br>         result.deletedCount);<br>   });|
|`Model.deleteMany(conditions, [callback])`|Deletes all documents that match the conditions.|// Delete all students with GPA < 3<br>Student.deleteMany({ gpa: { $lt: 3 }}, <br>   function(err, result) {<br>      console.log("Deleted " + <br>         result.deletedCount);<br>   });|
|`Query.deleteOne([conditions], [callback])`|Deletes the first document that matches the optional conditions.|// Delete first student with 2000-10-05 birthdate<br>Student.find({ birthDate: "2000-10-05" })<br>   .deleteOne()<br>   .exec(function(err, result) {<br>      console.log("Deleted " + <br>         result.deletedCount);<br>   });|
|`Query.deleteMany([conditions], [callback])`|Deletes all the documents that match the optional conditions.|// Delete all students with GPA < 2<br>Student.find({ gpa: { $lt: 2 }})<br>   .deleteMany()<br>   .exec();|


```
## 

Figure 10.10.7: Example Node.js project that adds new students entered in a form to a MongoDB database.

myproject
├── models
│   └── student.js
├── node_modules
│   ├── express
│   ├── mongoose
│   └── etc...
├── public
│   └── student.html
├── db.js
├── package.json
├── package-lock.json
└── server.js

  
  

|   |   |
|---|---|

```


# 10.11 Creating [[RESTful]] web APIs (Node)

Modern web applications use web API's to manipulate and transport data between the web browser and web server.

Web Api's are typically REST-based (representational state transfer) is an architectural style that describes how various components interact in a distributed hypermedia system. A [[RESTful]] web API is a web API that implements [[CRUD]] operations on resources using the mechanics of HTTP.


HTTP request verbs

[[RESTful]] web api's typically use four of the HTTP request verbs to implement [[CRUD]] operations

- POST - create a new resource
- GET - Retrieve a resource
- PUT - Update a resource
- DELETE - Delete a resource

Example request and responses for a Music Api

|Resource|Request verb|Description|Status code|
|---|---|---|---|
|/songs|GET|Get a list of all songs|200 OK|
|/songs?genre=pop|GET|Get all songs in the pop genre|200 OK|
|/songs/234|GET|Get song with ID 234|200 OK|
|/songs/999|GET|Get non-existing song with ID 999|404 Not Found|
|/songs|POST|Create a new song|201 Created|
|/songs/234|PUT|Update song with ID 234|204 No Content|
|/songs/234|DELETE|Delete song with ID 234|204 No Content|


Express Router
To create a web APU using Express, a developer uses the experss.Router class to create modular route clalbacks for the web API endpoints

```
const express = require("express");

const app = express();
const router = express.Router();

// GET request returns JSON-encoded song
router.get("/songs", function(req, res) {

   const song = {
      title: "Uptown Funk",
      artist: "Bruno Mars",
      popularity: 10,
      releaseDate: new Date(2014, 10, 10),
      genre: ["funk", "boogie"]
   };

   res.json(song);
});

// All requests to API begin with /api
app.use("/api", router);

app.listen(3000);
```
The call to app.get() creates a route for GET requests just like the call to router.get(). The benefit of using express.Router is when reorganizing routes into separate modules


# 10.12 Using [[RESTful]] apis with Fetch

A web application uses a web api running on the web server to manipulate data in the server's database.

- _id - Object ID uniquely identifying each song
- title - Required string
- artist - String
- popularity - Number between 1 and 10
- releaseDate - Date
- genre - Array of strings
## 

Table 10.12.1: Music API operations.

|Resource|Request verb|Description|Status code|
|---|---|---|---|
|/api/songs|GET|Gets a list of all songs in the database|200 OK|
|/api/songs/:id|GET|Gets the song with the given id|200 OK|
|/api/songs|POST|Adds the JSON-encoded song in the request body to the database|201 Created|
|/api/songs|PUT|Updates the existing song with the JSON-encoded song in the request body|204 No Content|
|/api/songs/:id|DELETE|Removes the song with the given id from the database|204 No Content|

Web applications call a web API from the browser by using the XMLHttpRequest object, the Fetch API, or some other library that can send [[HTTP]] requests.

```
addEventListener("DOMContentLoaded", async function() {
   const response = await fetch("/api/songs");
   const songs = await response.json();
    
   let html = "";
   for (let song of songs) {
      html += `<li>${song.title} - ${song.artist}</li>`;
   }

   document.querySelector("ul").innerHTML = html;
});

1. Browser requests songs.html from the Express web server and renders the HTML with an empty list.
2. fetch() sends a GET request using the URL /api/songs.
3. Web server's Music API retrieves all songs from MongoDB and returns the songs encoded in JSON.
4. response.json() parses the JSON-encoded songs and returns an array of song objects.
5. The for-of loop creates <li> elements containing each song title and artist. The <li> elements are added to <ul>, creating a bulleted list of songs.

Step 5: The for-of loop creates <li> elements containing each song title and artist. The <li> elements are added to <ul>, creating a bulleted list of songs. Step finished playing

```

Adding new songs
The `Fetch()` method can send a post request to a web api by specifying a second argument containing the request method, content-type header, and the data to send in the request body.

```
addEventListener("DOMContentLoaded", function() {
   document.querySelector("#addBtn").addEventListener("click", addSong);
});

async function addSong() {
   // Create a song object from the form fields
   const song = {
      title: document.querySelector("#title").value,
      artist: document.querySelector("#artist").value,
      releaseDate: document.querySelector("#released").value,
      popularity: document.querySelector("#popularity").value,
      genre: document.querySelector("#genre").value ? 
         document.querySelector("#genre").value.split(",") : []
   };

   // POST a JSON-encoded song to Music API
   const response = await fetch("/api/songs", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(song)
   });

   if (response.ok) {
      const results = await response.json();
      alert("Added song with ID " + results._id);

      // Reset the form after adding the song
      document.querySelector("form").reset();
   }
   else {
      document.querySelector("#error").innerHTML = "Cannot add song.";
   }     
}
```

Updating Songs

```
addEventListener("DOMContentLoaded", async function() {
   document.querySelector("#updateBtn").addEventListener("click", updateSong);

   // Load a song into the web form
   const songId = "5fe1097caf3b173148985746";
   const response = await fetch("/api/songs/" + songId);
   if (response.ok) {
      let song = await response.json();
      document.querySelector("#songId").value = song._id;
      document.querySelector("#title").value = song.title;
      document.querySelector("#artist").value = song.artist;
      document.querySelector("#released").value = 
         song.releaseDate.substring(0, 10);
      document.querySelector("#popularity").value = song.popularity;
      document.querySelector("#genre").value = song.genre;
   }
});

async function updateSong() {
   // Create a song object from the form fields
   const song = {
      _id: document.querySelector("#songId").value,
      title: document.querySelector("#title").value,
      artist: document.querySelector("#artist").value,
      releaseDate: document.querySelector("#released").value,
      popularity: document.querySelector("#popularity").value,
      genre: document.querySelector("#genre").value ? 
         document.querySelector("#genre").value.split(",") : []
   };
        
    // Send PUT request with JSON-encoded song to Music API
   const response = await fetch("/api/songs", {
      method: "PUT",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(song)
   });

   if (response.ok) {      
      alert("Updated song.");
   }
   else {
      document.querySelector("#error").innerHTML = "Cannot update song.";
   }     
}
```

# 10.13 Third Party web API's (node)

a public web [[API]] that is used by a web application to perform some operation.

To use a third-party web API, a developer usually registers with the third party to obtain an API key. Third parties require an API key for several reasons:

- The API key identifies who or what application is using the web API.
- The API key helps the third party limit the number of requests made to the API in a fixed time period or may be used to charge a developer a fee for additional requests.
- To obtain an API key, developers must agree to restrictions the third party places on data obtained from the web API.
```
const fetch = require("node-fetch");

app.get("/weather", function(req, res) { 
   const zip = 90210;
   const params = new URLSearchParams({ 
      zip: zip,
      units: "imperial", 
      appid: "APIKEY"}); 
  
   fetch("http://api.openweathermap.org/data/2.5/weather?" + params)
      .then(response => response.json())   
      .then(data => {
         const locals = {
            data: data, 
            zip: zip
         };
         res.render("weather", locals);
      })    
      .catch(error => console.log(error))
});
```

# 10.14 Token-based user authentication (Node)

User authentication is the process of verifying that a user is who the user claims to be. Many websites authenticate users based on a user provided username and password. Some websites supplement passwords with security questions, security images, and other techniques.

To implement use authentication, most websites use token-based authentication. `Token based authentication` is a technique where the client uses a signed token to "prove" to a server that the client has successfully authenticated. A signed token is a string of characters produced with a secret key that uniquely identifies the entity that created the token

flow 
1. User authenticates by entering a username and password, which are sent to the web server.
2. Web server verifies the username and password are valid and generates a token.
3. The token is returned to the web browser and stored for future requests.
4. Web app requests bsmith's calendar, so the token is sent in the web API request.
5. Web server validates bsmith's token and returns back bsmith's calendar data.

JSON web Tokens (JWT)

[[JSON]] web tokens are a popular way of implementing tokens in a token-based authentication. It is a string produced by the server that encodes [[JSON]] data. The string is signed with a secret key known only by the server to ensure the data in JWT is unaltered by the client.

JWT's are composed of three parts seperated by periods
`Header.Payload.Signature`

flow
1. The Header contains the type of token (JWT) and the algorithm used to sign the token (HMAC SHA256).
2. The Header is Base64 encoded.
3. The Payload containing the information to transmit is Base64 encoded.
4. The Signature is created using the HMAC SHA256 algorithm on the base64-encoded Header + base64-encoded Payload + Secret Key.
When the client sends a JWT back to the server, the server validates the JWT by generating a new signature based on the JWT's base64 encoded header and payload and the server's secret key. If the payload was not modified, the new signature should be identical to the JWT's signature.

jwt-simple module

The jwt-simple module is used to encode an decode JWT's in [[Node.js]] web applications. 
jwt provides a `jwt.encode()` method to create a JWT and a `jwt.decode()` method to decode a [[JWT]]
```

const jwt = require("jwt-simple");
const secret = "supersecret";
const payload = { username: "bsmith" };

// Create a JWT
const token = jwt.encode(payload, secret);
console.log("Token: " + token);

// Decode a JWT
const decoded = jwt.decode(token, secret);
console.log("Decoded payload: " + decoded.username);

Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6ImJvYiJ9.Mm0fNOZMBFOrFu99NlnHdz3jkp5IE_BQCNOz4sh1epQ
Decoded payload: bsmith
```


The figure below uses jwt-simple in the context of an Express server with two routes:

1. `/api/auth` - Accepts a username and password in a POST request. After verifying the username is "bsmith" and password is "pass", the route sends back a JWT carrying a payload containing bsmith's username.
    
2. `/api/status` - Accepts a GET request and expects the X-Auth header to contain the JWT obtained from the `/api/auth` route. After validating the JWT, the route sends back bsmith's status.
    

Developers can use a tool like Postman to test the Express server with the example HTTP requests shown at the bottom of the figure below.

```
const express = require("express");
const bodyParser = require("body-parser");
const jwt = require("jwt-simple");

const app = express();
const router = express.Router();

// Parse application/x-www-form-urlencoded
router.use(bodyParser.urlencoded(
   { extended: false }));

// Secret used to encode/decode JWTs
const secret = "supersecret";

router.post("/auth", function(req, res) {

    // Verify bsmith/pass was POSTed 
    if (req.body.username === "bsmith" && req.body.password === "pass") {
        // Send back a token that contains the user's username
        const token = jwt.encode({username: "bsmith"}, secret);
        res.json({ token: token });
    }
    else {
        // Unauthorized access
        res.status(401).json({ error: "Bad username/password" });   
    }
});

router.get("/status", function(req, res) {

    // Check if the X-Auth header is set
    if (!req.headers["x-auth"]) {
        return res.status(401).json({error: "Missing X-Auth header"});
    }

    // X-Auth should contain the token value
    const token = req.headers["x-auth"];
    try {
        const decoded = jwt.decode(token, secret);

        // Send back a status
        if (decoded.username === "bsmith") {
            res.json({status: "Enjoying a beautiful day!"});
        }
        else {
            res.json({status: "Working hard!"});
        }
    }
    catch (ex) {
        res.status(401).json({ error: "Invalid JWT" });
    }
});

app.use("/api", router);

app.listen(3000);
```


Using a database
Authentication services generally store and retrieve data from a database. Below shoes a [[Node.js]] project that stores data in a [[MongoDB]] database using Mongoose model called User.

1. `/api/user` - accepts a username, password, and status in a [[POST]] request. The route adds a new user to the database
2. `/api/auth` - Accepts a username and password in a POST request. The route verifies the POSTed username/password matches a username/password from the database and returns a JWT with the username in the payload
3. `/api/status` - Accepts a GET request and expects the X-Auth header to contain a valid JWT. The route validates the JWT and sends back the username and status of all users in the database

```
// api/users.js
const jwt = require("jwt-simple");
const User = require("../models/user");
const router = require("express").Router();

// For encoding/decoding JWT
const secret = "supersecret";

// Add a new user to the database
router.post("/user", function(req, res) {

   if (!req.body.username || !req.body.password) {
      res.status(400).json({ error: "Missing username and/or password"});
      return;
   }

   const newUser = new User({
      username: req.body.username,
      password: req.body.password,
      status:   req.body.status
   });

   newUser.save(function(err) {
      if (err) {
         res.status(400).send(err);
      }
      else {
         res.sendStatus(201);  // Created
      }
   });
});

// Sends a token when given valid username/password
router.post("/auth", function(req, res) {

   if (!req.body.username || !req.body.password) {
      res.status(401).json({ error: "Missing username and/or password"});
      return;
   }

   // Get user from the database
   User.findOne({ username: req.body.username }, function(err, user) {
      if (err) {
         res.status(400).send(err);
      }
      else if (!user) {
         // Username not in the database
         res.status(401).json({ error: "Bad username"});
      }
      else {
         // Check if password from database matches given password
         if (user.password != req.body.password) {
            res.status(401).json({ error: "Bad password"});
         }
         else {
            // Send back a token that contains the user's username
            const token = jwt.encode({ username: user.username }, secret);
            res.json({ token: token });
         }
      }
   });
});

// Gets the status of all users when given a valid token
router.get("/status", function(req, res) {

   // See if the X-Auth header is set
   if (!req.headers["x-auth"]) {
      return res.status(401).json({error: "Missing X-Auth header"});
   }

   // X-Auth should contain the token 
   const token = req.headers["x-auth"];
   try {
      const decoded = jwt.decode(token, secret);

      // Send back all username and status fields
      User.find({}, "username status", function(err, users) {
         res.json(users);
      });
   }
   catch (ex) {
      res.status(401).json({ error: "Invalid JWT" });
   }
});

module.exports = router;
```
```
// models/user.js
const db = require("../db");

// Create a model from the schema
const User = db.model("User", {
    username: { type: String, required: true },
    password: { type: String, required: true },
    status:   String
});

module.exports = User;

  
  

// db.js
const mongoose = require("mongoose");
mongoose.connect("mongodb://localhost/mydb");
module.exports = mongoose;

  
  

// server.js
const express = require("express");
const bodyParser = require("body-parser");
const User = require("./models/user");

const app = express();
const router = express.Router();
router.use(bodyParser.urlencoded(
   { extended: false }));
router.use("/api", require("./api/users"));
app.use(router);

app.listen(3000);
```


Storing JWT in local storage

The web application running in the web browser must interact with the server's api to authenticate the user, save the JWT, and transmit the JWT in subsequent API requests. The window.localStorage object allows web applications to store data in the web browser and is ideal for storing a JWT. The example below uses the Fetch API to obtain and transmit a JWT

```
async function login(username, password){
 const response = await fetch("/api/auth", {
      method: "POST",
      body: new URLSearchParams({ 
         username: username,
         password: password })
   });

   if (response.ok) {
      const tokenResponse = await response.json();
      localStorage.setItem("token", 
         tokenResponse.token);
   }
}

async function displayStatus() { 
   const token = localStorage.getItem("token");
   
   const response = await fetch("/api/status", {
      headers: { "X-Auth": token }
   });   

   if (response.ok) {
      const users = await response.json();
      let html = "";
      for (let user of users) {
         html += "<li>" + user.username + " - " +
            user.status + "</li>";
      }
      const status = document.querySelector("ul");
      status.innerHTML = html;
   }
}
```
1. The user enters a username and password and clicks Login button.
2. To authenticate the user, the browser calls login() with the username and password. The fetch() method sends a POST request with username and password to /api/auth.
3. The server verifies bsmith/pass and returns a JWT to the web browser.
4. response.json() extracts the token from the JSON response. The setItem() method saves the token to localStorage.
5. To display user statuses, displayStatus() retrieves the token from localStorage with getItem(). Then fetch() sends a GET request to /api/status with the token in the X-Auth header.
6. Token is validated by the server, so server sends JSON with all user statuses to the browser.
7. response.json() parses the user data. The usernames and statuses display in an unordered list.


# 10.15 Password Hashing (Node)

Cryptographic hash functions

Websites must exercise care when storing personal information about users. Numerous high-profile data breaches confirm that protecting personal data is very difficult to do. To protect users, organizations should store as little sensitive information as possible.

Passwords should never be stored as plain text in a database. Instead, developers should use cryptographic hash functions to convert passwords into hashes and store only the hashes in the database. A `cryptographic hash function` is a mathematical algorithm that converts text of any length into a fixed-length sequence of characters called the `hash digest` or `hash` 

## 

Figure 10.15.1: Hashing various passwords using the MD5 cryptographic hash function.

![Conversion of 4 passwords into hash digests using the MD5 hash function.  Although passwords are nearly identical, the hash digests are very different.](https://zytools.zybooks.com/zyAuthor/WebProgramming/70/IMAGES/72b14511-6dd4-967d-9cc1-9f56d053c3cc)

Hashed passwords and password cracking

An authentication system should only store password hashes, not plain text passwords. To authenticate a user, the authentication system hashes the password submitted by the user and compares the hash with the hash stored in the database. If the two hashes are identical, then the user provided the correct password


flow
1. New user's username and password hash is added to the database.
2. User pgreen attempts to login with the wrong password. Hash of "OpenSesame" does not match hash of "opensesame".
3. User pgreen attempts to login with the correct password. Hash of "opensesame" matches hash of "opensesame".
An attacker would be unable to directly convert the hashes back into the users' original passwords. However, some may use a variety of methods to crack password hashes. `Password cracking` is the process of recovering passwords from data, like the database of a compromised website

A `dictionary attack` is a popular password cracking strategy where the attacker feeds a number of possible passwords, such as words from a dictionary, into a hash function and compares the stolen hashes to the generated hashes. Passwords are revealed for any matching hashes. These attacks are computationally expensive, so attackers create precomputed dictionary tables in advance

Developers can use 'salt' to circumvent attacks with precomputed tables. A `salt` is a random string that is combined with a password so two identical passwords produce different hashes.

Strong passwords are less susceptible to dictionary attacks

A strong password has the following characteristics:

- Does not contain words found in a dictionary or on the web
- Composed of uppercase and lowercase letters, digits, and perhaps punctuation
- At least 10 characters in length
- Has not been used as a password before on the same website or on any other website
- Does not conform to popular password patterns like an initial capital letter, 2-4 digits at the end, or adding ! at the end

## 

2012 LinkedIn data breach

Russian cybercriminals stole 6.5 million password hashes from LinkedIn on June 5, 2012. The criminals cracked more than 60% of the unique passwords from the hashes and published the passwords in plain text on the web. LinkedIn had used the SHA1 hash function to generate the hashes but did not use salt. The data breach highlights the risk to users who do not use strong passwords.


bcryptjs

Cryptography researchers have found weaknesses in older hash functions like MD5 and SHA-1 that make those hash functions vulnerable to attacks. Good practice is to use strong hash function like bcrypt, scrypt, or PBKDF2, which purposely execute slowly and make password cracking significantly more difficult

```
const bcrypt = require("bcryptjs");

// Generate 3 hashes for the same password
for (let c = 0; c < 3; c++) {
   let hash = bcrypt.hashSync("opensesame", 10);
   console.log("Hash: " + hash);
}

// Compare hash produced by identical passwords
const passwordHash = bcrypt.hashSync("opensesame", 10);
if (bcrypt.compareSync("opensesame", passwordHash)) {
   console.log("Same!");
}
else {
   console.log("Not the same");
}



Hash: $2a$10$33M.4Zn7R7k3jHOISHxCe.yUqI4vl9mv4/oeiLuhHDQZcfySVg6wC
Hash: $2a$10$ByrTcHizkol25k1WOnlV2egFI3DdRzo9.xrjal/IyiaKd8X5diFpi
Hash: $2a$10$cd.MX7Ubbm3n9Lfc8ilrgeYw3MRpJ512fUtPq4kHEQyhI8wpJ8LPq
Same!
```

Example in node

```
const express = require('express');
const bcrypt = require('bcryptjs');
const bodyParser = require('body-parser');

const app = express();
const port = 3000;

// Middleware to parse request body as JSON
app.use(bodyParser.json());

// Simulate a database with an in-memory object
const users = [];

// Register route - hash the password and store the user
app.post('/register', async (req, res) => {
   const { username, password } = req.body;

   // Check if the user already exists
   const userExists = users.find(user => user.username === username);
   if (userExists) {
      return res.status(400).json({ message: "User already exists" });
   }

   try {
      // Hash the password using bcrypt
      const saltRounds = 10;
      const hashedPassword = await bcrypt.hash(password, saltRounds);

      // Save the user with the hashed password
      const newUser = { username, password: hashedPassword };
      users.push(newUser);

      res.status(201).json({ message: "User registered successfully" });
   } catch (err) {
      res.status(500).json({ message: "Error registering user" });
   }
});

// Login route - verify the password
app.post('/login', async (req, res) => {
   const { username, password } = req.body;

   // Find the user in the "database"
   const user = users.find(user => user.username === username);
   if (!user) {
      return res.status(400).json({ message: "Invalid username or password" });
   }

   try {
      // Compare the password with the hashed password stored in the "database"
      const isMatch = await bcrypt.compare(password, user.password);

      if (isMatch) {
         res.status(200).json({ message: "Login successful" });
      } else {
         res.status(400).json({ message: "Invalid username or password" });
      }
   } catch (err) {
      res.status(500).json({ message: "Error logging in" });
   }
});

// Start the server
app.listen(port, () => {
   console.log(`Server running on http://localhost:${port}`);
});

```