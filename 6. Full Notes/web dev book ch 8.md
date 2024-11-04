
2024-09-14 22:14

Status:

Tags:[[Web dev book]], [[JavaScript]]

# web dev book ch 8

# 8.1 regular expressions

Introduction

programs often need to determine if a string conforms to a pattern. Ex check if a phone number is formatted to a phone number

A Regular expression (regex) is a string patter that is matched against a string. 
`let re = new RegExp("abc")` or `let re = /abc/`

the pattern "abc" matches any string that contains "abc"

regular expressions can use characters with special meaning to create moew sophisticated patterns. The + character matches the preceding character at least once.
EX: /ab+c/ matches one "a" followed by at least one "b" and one "c" so "abc" and "abbbbc" both match. However "ac" does not match

|Character|Description|Example|
|---|---|---|
|`*`|Match the preceding character 0 or more times.|`/ab*c/` matches "abc", "abbbbc", and "ac".|
|`+`|Match the preceding character 1 or more times.|`/ab+c/` matches "abc" and "abbbbc" but not "ac".|
|`?`|Match the preceding character 0 or 1 time.|`/ab?c/` matches "abc" and "ac", but not "abbc".|
|`^`|Match at the beginning.|`/^ab/` matches "abc" but not "cab".|
|`$`|Match at the end.|`/ab$/` matches "cab" but not "abc".|
|`\|`|Match string on the left OR string on the right.|`/ab\|cd/` matches "abc" and "bcd".|
A metacharacter is a character or character sequence that matches a class of characters in a regular expression. Ex: The period character matches any single character except the newline character. So `/ab.c/` matches "abZc" and "ab2c", but not "abc" since the period must match a single character. Other metacharacters begin with a backslash.

|Metacharacter|Description|Example|
|---|---|---|
|`.`|Match any single character except newline.|`/a.b/` matches "aZb" and "a b".|
|`\w`|Match any word character (alphanumeric and underscore).|`/a\wb/` matches "aAb" and "a5b" but not "a b".|
|`\W`|Match any non-word character.|`/a\Wb/` matches "a-b" and "a b" but not "aZb".|
|`\d`|Match any digit.|`/a\db/` matches "a2b" and "a9b", but not "aZb".|
|`\D`|Match any non-digit.|`/a\Db/` matches "aZb" and "a b", but not "a2b".|
|`\s`|Match any whitespace character (space, tab, form feed, line feed).|`/a\sb/` matches "a b" but not "a4b".|
|`\S`|Match any non-whitespace character.|`/a\Sb/` matches "a!b" but not "a b".|

Mode modifyers - somtimes called a flag changes how a regex matches and is placed after the second slash in a regex

| Mode modifier | Description                                                                                     | Example                                                                              |
| ------------- | ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| `i`           | Case insensitivity - Pattern matches upper or lowercase.                                        | `/aBc/i` matches "abc" and "AbC".                                                    |
| `m`           | Multiline - Pattern with `^` and `$` match beginning and end of any line in a multiline string. | `/^ab/m` matches the second line of "cab\nabc", and `/ab$/m` matches the first line. |
| `g`           | Global search - Pattern is matched repeatedly instead of just once.                             | `/ab/g` matches "ab" twice in "cababc".                                              |

regex is literal chineese what the fuck is that
im not doing these

# 8.2 classes

a [[class]] is a special function, called a constructor function, that defined properties and methods from which an object may inherit.

A [[Constructor Function]] is a function that initializes a new object whe n an object is instantiated with the `new` operator.

the `this` keyword refers to ther current object and is used to access properties inside the class

Prototype object

Every [[JavaScript]] object is associated with a second object called the [[Prototype]]. The [[Prototype]] object contains properties that an associated object inherits when the associated object is created.

When an object is instantiated with the `new` keyword, the object is assigned the `prototype` property that is associated with the constructor function.

Ex: When a date object is instantiated with `new Date()` the date object is assigned the `Date.prototype` from the `Date` constructor function. 

Developers often assign methods to the class' prototype instead of the constructor function because prototype methods are more memory efficient. Because the [[JavaScript]] interpreter must allocate memory for each method defined in a constructor function, but a prototype method is only allocated memory once and is shared by all object created with the same constructor function

function Person(name, age) {
  this.name = name;
  this.age = age;
};

// Prototype method
Person.prototype.sayHello = function() {
  console.log("Hello, " + this.name);
};

let bob = new Person("Bob", 21);
let sue = new Person("Sue", 40);
let pam = new Person("Pam", 32);



// Student class
function Course(title, students) {
   this.title = title;
   this.students = [];
   
   this.addStudent = function(student) {
      this.students.push(student);
   }
}
      Course.prototype.displayStudents = function(){
      console.log(this.title);
      for(let i = 0; i < this.students.length; i++){
         console.log(this.students[i].name + ' GPA ' + this.students[i].gpa)
         }
         
         
   }
function Student(name, gpa) {
   this.name = name;
   this.gpa = gpa;
   
}
let timmeh = new Student("temmeh", 2.0)
let jimmeh = new Student("jimmeh", 3.1)

let a = new Course("shitty convocation")
a.addStudent(timmeh)
a.addStudent(jimmeh)
a.displayStudents()


Private Property and closures

A [[Private Property]] is a property that is only accessible to object methods but is not accessible from outside the class. Private properties may be simulated in [[JavaScript]] by creating local [[Variables]] in a constructor function with getters and setters to get and set the properties

Private class variables can be simulated in [[JavaScript]] because of closures. A closure is a special object that is automatically created and maintains a function's local variables and values after the function has returned.

function Person(name, age) {
   this.name = name;
   this.age = age;

   // private
   let secret;

   // public methods have access to private properties
   this.setSecret = function(s) {
      secret = s;
   };

   this.getSecret = function() {
      return secret;
   };
};

let bob = new Person("Bob", 21);
bob.setSecret("I have mutant powers!");
console.log(bob.getSecret());   // I have mutant powers!
console.log(bob.secret);        // undefined

Prototype methods do not have direct access to private (local) variables. Prototype methods must use getters and setters to access private properties.

`Person.prototype.getPartialSecret = function() { return this.getSecret().substr(0, 5) + "..."; };`

# Inheritance

[[Inheritance]] creates a new child class that adopts properties of a parent class. 
	Ex: a student class (child) may inherit from a Person class (parent), so a student class has the same properties of a Person and may add even more properties


# 8.3 Classes (ES6)

Classes in EcmaScript6 simplifies class declarations, introducing syntax that looks more familiar to [[Java]] or [[C(SHARP)]]. Although the syntax is different, the underlying prototype model is not changed.

A class is declared by using the `class` keyword followed by a class name.

Inheritance
[[Inheritance]]
The `Extends` keyword allows one class to inherit from another. In the inheriting class' constructor, calling the `super()` function calls the parent class' constructor. `super()` must be caleld before using the this keyword in the inheriting class' constructor

class Person {
   constructor(name, age) {
      this.name = name;
      this.age = age;
   }
    
   sayHello() {
      console.log("Hello.  My name is " + this.name + ".");
   }
}

// Student inherits from Person
class Student extends Person {
   constructor(name, age, gpa) {
      super(name, age);     // Call parent constructor
      this.gpa = gpa;
   }

   // Override parent's sayHello method
   sayHello() {
      console.log("Hi, I'm " + this.name + " with a " + this.gpa + " GPA!");
   }
}

Getters and setters
A class method declaration preceded by the `get` keyword defines a getter method for a property

A class method declaration preceded by the `set` keyword defines a setter method for a property

```
get area(){
return this.width * this.height
}
```
After creating a Square instance named s1, the expression s1.area without parentheses gets the square's area

Static Methods

A static method is a method that can be called without creating an instance of the class.

The method is called with the syntax `ClassName.methodName(arguments)`



# 8.4 Classes (ES13)

Classes in EcmaScript 2022
Although the syntax is different, the underling prototype model is not changed

declared by using the `class` keyword, followed by the classname.
The class is implemented by declaring fields and methods within braces. A field is a variable that stores data for a class. Each method declaration is similar to a function declaration, but without the `function` keyword
```

class City {
   name;
   state;
   
   constructor(name, state) {
      this.name = name;
      this.state = state;
   }

   toHTML() {
      return this.name + ",&nbsp;" + this.state;
   }
}
  
let city1 = new City("Austin", "Texas");
let city2 = new City("Madison", "Wisconsin");
```

Private fields and methods
By default fields and methods are public, meaning the fields and methods are accessible from outside the class. Fields and methods can be made private or inaccessable from outside the class, by prefixing the field or method name with #

class City {
   #foundingYear;
   
   constructor(name, state, foundingYear) {
      this.name = name;
      this.state = state;
      this.#foundingYear = foundingYear;
   }
   
   toString() {
      return this.name + ", " + this.state +
         " (" + this.#foundingYear + ")";
   }
}

Getters and setters - same as ES6 it seems

# 8.5 Inner [[Functions]], outer [[Functions]], Function scope

defined in [[Functions]] javascript area

Scope objects - To store a collection of variables for a particular scope, [[JavaScript]] implementaitons commonly use a `scope object`. An object that stores a collection of variable names and corresponding values. 

EX: when a function with local variables is executed, the [[JavaScript]] runtime creates a scope object that stores the function's local [[Variables]]

function logXYZ() {
   let x = Math.random();
   if (x < 0.5) {
      let y = x * 100;
      console.log(y);
   }

   let z = x * 1000;
   console.log(z);
}


1. When logXYZ() is called, a scope object for the function is created. Variables x and z are scoped to the entire function and are stored in the scope object.
2. The scope object includes the variable values. x is assigned with the random number 0.25 on the first line, and z is initially undefined.
3. A new block scope object is created when execution enters the if block. Variable y is declared with let and is scoped to the if block.
4. The block scope object is used by the runtime to lookup y's value for the console.log() call.
5. When execution leaves the if block, the block scope object with y's value is removed. The variable y is out of scope and no longer available.
6. The function scope object is used to store and lookup values for x and z.

Scope Chain
A `scope chain` is a linked list of scope objects used by the [[JavaScript]] runtime to store and lookup variable values when executing code.

When a variable is needed, a search begins at the scope object at the beginning of the scope chain. If the [[Variables]] is found the corresponding value is used. Otherwise, the next object in the scope chain is searched. If the result reaches a null object at the end of the scope chain, the variable is not found and a ReferenceError is thrown


# 8.6 Closures

Execution context and closures

An execution context is an object that stores information needed to execute [[JavaScript]] code, and includes but is not limited to:
- information about code execution state, such as the line of code being executed and the line to return to when a function completes
- a reference to a scope change
Execution contexts are stored on an execution stack. The current execution context (running execution context) is the execution context at the top of the execution stack. The current scope chain is the scope chain of the current execution context.

A closure is a combination of a function's code and a reference to a scope chain. When a [[JavaScript]] function is declared, a closure is created that includes the function's code and a reference to the current scope chain. Closures are what allow an inner function to access the outer functions [[Variables]]



![[Pasted image 20240917142854.png]]

![[Pasted image 20240917143041.png]]
![[Pasted image 20240917143250.png]]


![[Pasted image 20240917143643.png]]

probably has stuff to do with [[Compiler]] but [[JavaScript]] does not 'compile'


# 8.7 Modules

A website may use a significant amount of [[JavaScript]] code to fetch data from a web server, interact with the user, perform computations, etc. Developers organize [[JavaScript]] code by placing related functionality into modules.

A `module` is a [[JavaScript]] file that contains one or more variables, functions, or classes that are exported for use in other modules. Modules allow developers to write more maintainable and reusable code

A module uses an export statement to list items to be exported
- if exporting more than one item, braces must surround the items
- if exporting a single item, the `default` keyword is used in an export statement to name the one item to export. 


hello.js

function sayHello() {
   alert("Hello!");
}

function sayHi() {
   alert("Hi!");
}

export { sayHello, sayHi };

goodbye.js

function sayGoodbye() {
   alert("Goodbye!");
}

export default sayGoodbye;


Module imports
A module imports items from another module using an import statement. An `import` statement indicates which items are to be imported from a module

- if importing non-default items, braces must surround the items
- if importing a default item, no braces are used

# 8.8 Strict mode

A programmer can make the [[JavaScript]] interpreter catch mistakes like mistyped variable names using the strict mode. Strict mode makes [[JavaScript]] interpreter apply a set of restrictive syntax rules to [[JavaScript]] code.

To enable strict mode for an entire script, the statement "use strict"; must be placed before any other statements

# 8.9 Web Storage
The web storage api provides storage objects that allow Javascript programs to securely store key/value pairs in the web browser. It supports two storage objects

1. The sessionStorage object stores key/value pairs for an origin that are only available for the duration of the session. Closing the browser or browser tab ends the session
2. The localStorage object stores key/value pairs for an origin that are stored indefinitely

Accessing web storage data
The `localStorage` and `sessionStorage` objects provide methods for storing data, retrieving data, and removing data:
1. setItem(key, value) - stores the key string and associated value string in storage
2. getItem(key) - returns the value associated with the key in storaage or null if the key does not exist
3. removeItem(key) - removes the key and associated value from storage
4. clear() - removes all keys and associated values from storage

# 8.10 Canvas drawing

Canvas, context, and drawing rectangles

the `<canvas>` element defines a rectangular area of a webpage where shapes, images, and text can be displayed using [[JavaScript]]. The canvas origin (0,0) is located in the upper left corner of the canvas

strokeRect() - draws an outlined rectangle
fillRect() draws a filled rectangle.

|Method/Property|Description|Example|
|---|---|---|
|`fillRect(x, y, width, height)`|Draw a filled rectangle with top-left corner at (x, y)|context.fillRect(0, 5, 20, 30);|
|`fillStyle`|Interior color of filled rectangle|context.fillStyle = "maroon";|
|`lineWidth`|Outline width of stroked rectangle|context.lineWidth = 5;|
|`strokeRect(x, y, width, height)`|Draw a stroked (outlined) rectangle with top-left  <br>corner at (x, y)|context.strokeRect(0, 5, 20, 30);|
|`strokeStyle`|Outline color of stroked rectangle|context.strokeStyle = "blue";|

Lines and shapes can be drawn on a canvas using a path. A path is a list of points that are connected by lines. A path is created using various context methods:

1. The beginPath() method creates a new path.
2. The moveTo() method defines the path's starting point at coordinate (x, y).
3. The lineTo() method adds a line to the path from the last point to a new point at coordinate (x, y).
4. Additional calls to `moveTo()` and/or `lineTo()` create additional points or lines.
5. The closePath() method adds a line from the current point to the path's starting point.

The path does not appear on the canvas until `stroke()` or `fill()` is called. The stroke() method draws a path's outline. The fill() method fills a path's interior.

|                                                            |                                                             |                                                     |
| ---------------------------------------------------------- | ----------------------------------------------------------- | --------------------------------------------------- |
| `beginPath()`  <br>`closePath()`                           | Begin and close a path                                      | context.beginPath();<br>...<br>context.closePath(); |
| `fill()`                                                   | Draw a filled shape defined by the current path             | context.fill();                                     |
| `fillStyle`                                                | Interior color of filled shape                              | context.fillStyle = "blue";                         |
| `lineTo(x, y)`                                             | Draw a line from the last point in the path to (x, y)       | context.lineTo(100, 50);                            |
| `moveTo(x, y)`                                             | Move the path to (x, y)                                     | context.moveTo(50, 20);                             |
| `stroke()`                                                 | Draw a stroked (outlined) shape defined by the current path | context.stroke();                                   |
| `strokeStyle`                                              | Outline color of stroked shape                              | context.strokeStyle = "orange";                     |
| Method/Property                                            | Description                                                 | Example                                             |
| `arc(x, y, radius, startAngle, endAngle, [anticlockwise])` | Adds an arc to the path                                     | context.arc(50, 100, 30, 0, Math.PI, true);         |
| `fill()`                                                   | Draw a filled arc                                           | context.fill();                                     |
| `fillStyle`                                                | Interior color of arc                                       | context.fillStyle = "maroon";                       |
| `stroke()`                                                 | Draw a stroked (outlined) arc                               | context.stroke();                                   |
| `strokeStyle`                                              | Outline color of stroked arc                                | context.strokeStyle = "blue";                       |

# 8.12 [[Websockets]]

Websocket protocol and object

Many web applications need to update the application screen as soon as new data arrives on the server.
Developers use [[Ajax]] to dynamically update the application screen with new server data, but [[Ajax]] is designed for the client to initiate the request, not the server.

Polling is a technique where the client sends an [[Ajax]] request periodically to the web server asking if any new data is available. Polling is not always ideal because of lag time between server receiving new data and sending the next [[Ajax]] request

The WebSocket protocol runs over a single [[TCP]] connection and allows for real time communication between web servers and web browsers. As long as the WebSocket connection remains open between the browser and web server, the server can send information to the browser at any time.

let url = "wss://echo.websocket.events/";
let websocket = new WebSocket(url);
        
websocket.onopen = function() { 
   displayMessage("Connected");
   websocket.send("Hello, WebSockets!"); 
};
        
websocket.onclose = function() { 
   displayMessage("Disconnected");
};

websocket.onmessage = function(e) {
   displayMessage(e.data);
};

setTimeout(function() {
   websocket.close() }, 2000);
        
function displayMessage(message) {
   let para = document.createElement("p");
   para.innerHTML = message;
   document.getElementById("output").appendChild(para);
}


Websocket handshake

The browser and server perform a Websocket handshake to establish a WebSocket connection. The browser requests a websocket connection by sending the server a websocket handshake request, an HTTP request that contains several headers like:
- connection - value set to "upgrade"
- Sec-WebSocket-key-  String produced by the client and used by the server to produce a Sec-Websocket-Accept string that the client expects in response
- Upgrade - request to upgrade from HTTP to WebSocket protocol
If the server accepts the Websocket connection request, the server responds with a websocket handshake response that contains a 101 status code and several headers:
- Connection - value set to upgrade
- Sec-websocket-accept string produced by the server
- upgrade - upgrade to websocket protocol

```
--- START FILE: JavaScript ---


let connectionStatus = document.getElementById("connectionStatus");
let response = document.getElementById("response");
let message = document.getElementById("message");
connectionStatus.innerHTML = "Disconnected";
let websocket = null;

document.getElementById("connectBtn").addEventListener("click", function() {
   // User clicked Connect button
   websocket = new WebSocket("wss://echo.websocket.events/");

   // Connect the websocket to wss://echo.websocket.events/ and 
   // create open, close, and message event callbacks
   websocket.onopen = function() { 
      connectionStatus.innerHTML = "Connected"; 
   }; 

   websocket.onclose = function() { 
      connectionStatus.innerHTML = "Disconnected"; 
   }; 

   websocket.onmessage = function(e) { 
      response.innerHTML = e.data; 
   }; 
   
   websocket.onerror = function(e) { 
      alert("Error!");
      console.log(e); 
   };
});

document.getElementById("disconnectBtn").addEventListener("click", function() {
   // User clicked Disconnect button
   websocket.close();
});

document.getElementById("sendBtn").addEventListener("click", function() {
   // User clicks Send button
   console.log("Send: " + message.value); 

   // Make sure valid connection exists before sending a message
   if (websocket === null || websocket.readyState !== WebSocket.OPEN) {
      alert("Connect before you send.");
   }
   else {
      websocket.send(message.value);
   }
});


--- END FILE: JavaScript ---
```


# 8.13 Promises

Synchronous and asynchronous functions

Synchronous function - function that completes an operation before returning

Asynchronous function - function is a function that starts an operation and potentially returns before the operation completes. The operation completse in the background, allowing other code to execute in the meantime. 

Promise object - an object representing the eventual completion of the asynchronous operation

A promise object can be in one of three states:
- Pending - asynchronous operation is still running
- Fulfilled - asynchronous operation has been completed successfully
- Rejected - asynchronous operation has ended in failure to produce the intended result

Promise.then() method - can be called to request notifications about the state

## 

Table 8.13.1: Comparison of Promise object's then() and catch() usage scenarios.

| Code                                                      | Scenario                                                 | Function(s) called | Uncaught exception? |
| --------------------------------------------------------- | -------------------------------------------------------- | ------------------ | ------------------- |
| promise1.then(okFunc, failFunc);                          | promise1 fulfilled, okFunc() does NOT throw an exception | okFunc() only      | No                  |
| promise1 fulfilled, okFunc() throws an exception          | okFunc() only                                            | Yes                |                     |
| promise1 rejected, failFunc() does NOT throw an exception | failFunc() only                                          | No                 |                     |
| promise1 rejected, failFunc() throws an exception         | failFunc() only                                          | Yes                |                     |
| promise1.then(okFunc).catch(failFunc);                    | promise1 fulfilled, okFunc() does NOT throw an exception | okFunc() only      | No                  |
| promise1 fulfilled, okFunc() throws an exception          | okFunc() first, then failFunc()                          | No                 |                     |
| promise1 rejected, failFunc() does NOT throw an exception | failFunc() only                                          | No                 |                     |
| promise1 rejected, failFunc() throws an exception         | failFunc() only                                          | Yes                |                     |
|                                                           |                                                          |                    |                     |
|                                                           |                                                          |                    |                     |

# 8.14 async and await

### Async function

An async function provides simpler syntax for creating an asynchronous function that returns a Promise. An async function is a function that is declared with the `async` keyword. The async keyword must appear in a function declaration before the `function` keyword. An async function fulfills the Promise by returning a value, or rejects the Promise by throwing an exception.
### await keyword

The `await` keyword simplifies waiting for a Promise to resolve. The await keyword is used in an async function to wait for a Promise object to resolve before proceeding to the next statement. Waiting for an asynchronous operation to complete pauses the async function's execution. Then, after the Promise eventually resolves, execution resumes inside the async function at the statement following the `await`.

# 8.15 Fetch API

The Fetch API defined fetch() method for sending HTTP requests and receiving HTTP responses. The fetch method is a replacement for using the XMLHTTPRequest object directly and is generally easier to use

`fetch()` sends a [[GET]] request by default to the given url argument and returns a promise object. The promise object resolves to a Response object, which contains information about the HTTP response and methods for retrieving the response body.

properties of response

- The response.status property is the HTTP response's status code (200, 301, 404, etc)
- response.ok property is set to true if the HTTP response status code is 2xx, false otherwise
- response.headers property is an object containing the HTTP response headers
- response.text() returns a Promise thar resolves with the textual body of the HTTP response

The web browser restricts fetch() from sending Cors requests, which is a request made to another domain. A web server can implement cors to allow cross origin requests

[[POST]] request

the fetch() method has an optional second parameter, an object that specifies options to modify the HTTP request. Some common fetch() options.
- The `method` option indicates the HTTP method EX: GET, POST, PUT, DELETE
- The `headers` option specifies various HTTP request headers: EX: content-type and user-agent
- the `body` option specifies the HTTP request body, which could be form data, a JSON-encoded string, or binary data


# lab 1
function checkForm() {

   // TODO: Perform input validation

   let fullName = document.getElementById('fullName')

   let email = document.getElementById('email')

   let password = document.getElementById('password')

   let errorDiv = document.getElementById('formErrors')

   const emailRegEx = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,5}$/

   errorDiv.innerHTML = ''

   errorDiv.classList.add('hide')

   let hasError = false;

  

   fullName.classList.remove('error');

   email.classList.remove('error');

   password.classList.remove('error');

   passwordConfirm.classList.remove('error');

  

   const lowercaseRegex = /[a-z]/;  

   const uppercaseRegex = /[A-Z]/;  

   const digitRegex = /\d/;

  
  

   if(fullName.value < 1){

      let err = document.createElement('li')

      err.textContent = "Missing full name."

      errorDiv.appendChild(err)

      fullName.classList.add('error')

      hasError = true;

   }

   if(!emailRegEx.test(email.value)){

      let err = document.createElement('li')

      err.textContent = "Invalid or missing email address."

      errorDiv.appendChild(err)

      email.classList.add('error')

      hasError = true;

   }

   if(password.value.length < 10 || password.value.length > 20){

      let err = document.createElement('li')

      err.textContent = "Password must be between 10 and 20 characters."

      errorDiv.appendChild(err)

      password.classList.add('error')

      hasError = true;

   }

  

   if (!lowercaseRegex.test(password.value)) {

      let err = document.createElement('li')

      err.textContent = "Password must contain at least one lowercase character."

      errorDiv.appendChild(err)

      password.classList.add('error')

      hasError = true;

   }

   if (!uppercaseRegex.test(password.value)) {

      let err = document.createElement('li')

      err.textContent = "Password must contain at least one uppercase character."

      errorDiv.appendChild(err)

      password.classList.add('error')

      hasError = true;

   }

   if(!digitRegex.test(password.value)){

      let err = document.createElement('li')

      err.textContent = "Password must contain at least one digit."

      errorDiv.appendChild(err)

      password.classList.add('error')

      hasError = true;

   }

   if(document.getElementById('passwordConfirm').value != password.value){

      let err = document.createElement('li')

      err.textContent = "Password and confirmation password don't match."

      errorDiv.appendChild(err)

      document.getElementById('passwordConfirm').classList.add('error')

      hasError = true;

   }

   if(hasError){

      errorDiv.classList.remove('hide')

   }

   return !hasError;

}

  

document.getElementById("submit").addEventListener("click", function(event) {

   checkForm();

  

   // Prevent default form action. DO NOT REMOVE THIS LINE

   event.preventDefault();

});

# lab 2
// TODO: Define SuperHuman, SuperHero, and SuperVillain classes here

class SuperHuman{

   name;

   powerLevel;

   constructor(name, powerLevel){

      this.name = name;

      this.powerLevel = powerLevel

   }

}

  

class SuperHero extends SuperHuman{

   constructor(name, alias, powerLevel){

      super(name, powerLevel);

      this.alias = alias

   }

  

   battle(SuperVillain){

      if(this.powerLevel >= SuperVillain.powerLevel){

         return true

      }else{

         return false

      }

   }

}

  

class SuperVillain extends SuperHuman{

   constructor(name, alias, powerLevel){

      super(name, powerLevel);

      this.alias = alias

   }

   getEvilChuckle(){

      return "Ha ha ha!"

   }

}
# lab 3
let groceryList = [];

  

// Wait until DOM is loaded

window.addEventListener("DOMContentLoaded", function() {

   document.querySelector("#addBtn").addEventListener("click", addBtnClick);

   document.querySelector("#clearBtn").addEventListener("click", clearBtnClick);

  

   // Load the grocery list from localStorage

   let tempList = loadList();

   if (tempList) {

       groceryList = tempList;

   }

   if (groceryList.length > 0) {

      // Display list

      for (let item of groceryList) {

         showItem(item);

      }

   }

   else {

      // No list to display

      enableClearButton(false);

   }    

});

  

// Enable or disable the Clear button

function enableClearButton(enabled) {

   document.querySelector("#clearBtn").disabled = !enabled;

}

  

// Show item at end of the ordered list

function showItem(item) {

   let list = document.querySelector("ol");

   list.innerHTML += `<li>${item}</li>`;    

}

  

// Add item to grocery list

function addBtnClick() {

   let itemTextInput = document.querySelector("#item");

   let item = itemTextInput.value.trim();

   if (item.length > 0) {

      enableClearButton(true);

      showItem(item);

      groceryList.push(item);

  

      // Save groceryList to localStorage

      saveList(groceryList);

   }

  

   // Clear input and add focus

   itemTextInput.value = "";

   itemTextInput.focus();

}

  

// Clear the list

function clearBtnClick() {

   enableClearButton(false);

   groceryList = [];

   let list = document.querySelector("ol");

   list.innerHTML = "";

  

   // Remove the grocery list from localStorage

   clearList();

}

  

function loadList() {

   // TODO: Complete the function

   let list= localStorage.getItem('list')

   if (list){

      return list.split(',')

   }

   return []

}

  

function saveList(groceryList) {

   // TODO: Complete the function

   let str = groceryList.join(',')

   localStorage.setItem('list', str)

}

  

function clearList() {

   // TODO: Complete the function

   localStorage.clear()

  

}


# lab 4

// Size of a single snowflake

const flakeSize = 8;

  

window.addEventListener("DOMContentLoaded", function() {

   let canvas = document.querySelector("canvas");

   drawGround(canvas);

   drawSnowText(canvas);

   drawSnowman(canvas);  

   drawSnowflakes(canvas);  

});

  

function drawGround(canvas) {

   let context = canvas.getContext("2d");

  

   // Background

   context.fillStyle = "#bbb";

   context.fillRect(0, 0, canvas.width, canvas.height);

  

   // Ground

   context.fillStyle = "brown";

   context.fillRect(0, canvas.height - 80, canvas.width, canvas.height);

}

  

function drawSnowflakes(canvas) {  

   for (let c = 0; c < 100; c++) {

      let x = Math.floor(Math.random() * canvas.width);

      let y = Math.floor(Math.random() * canvas.height);

      drawSingleFlake(canvas, x, y);

   }

}

  

function drawSnowText(canvas) {

   // TODO: Complete the function

   let ctx = canvas.getContext("2d");

  

    ctx.font = "80px Verdana";

    ctx.textAlign = "center";

    ctx.textBaseline = "top";

    ctx.fillStyle = "blue";

  

    ctx.fillText("SNOW", canvas.width / 2, 10);

  

}

  

function drawSnowman(canvas) {

   // TODO: Complete the function

   let ctx = canvas.getContext("2d");

  

   ctx.beginPath();

   ctx.arc(150, 200, 50, 0, Math.PI * 2, false); // Bottom circle

   ctx.fillStyle = "white";

   ctx.fill();

  

   ctx.beginPath();

   ctx.arc(150, 120, 40, 0, Math.PI * 2, false); // Middle circle

   ctx.fillStyle = "white";

   ctx.fill();

  

   ctx.beginPath();

   ctx.arc(150, 60, 25, 0, Math.PI * 2, false); // Head (smallest)

   ctx.fillStyle = "white";

   ctx.fill();

  

}

  

function drawSingleFlake(canvas, x, y) {

   // TODO: Complete the function

   let ctx = canvas.getContext("2d");

  

   ctx.beginPath();

   ctx.moveTo(x,y)

   ctx.lineTo(x + flakeSize / 2, y + flakeSize / 2)

   ctx.lineTo(x, y + flakeSize)

   ctx.lineTo(x - flakeSize / 2, y + flakeSize / 2)

  

   ctx.fillStyle = "#eee";

   ctx.fill();

}