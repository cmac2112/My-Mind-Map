
2024-09-11 22:45

Status: in progress

Tags:[[JavaScript]], [[DOM]], [[HTML]] [[Web dev book]]

# Javascript in the browser

# 7.1
document.writeln() outputs [[HTML]] into the document and alters the [[DOM]]


window object: [[JavaScript]] running the the browser has access to the window object.
	window.location - is a location object that contains information about the windows current URL 
		ex: window.location.hostname is the urls hostname
	window.navigator - is a navigator object that contains information about the browser
	window.innerHeight and window.innerWidth - are the height and width in pixels of the windows content area
	window.alert displays an alert dialog box
	window.confirm displays a confirmation dialog box
	window.open opens a new browser window

Console
	The browser provides a console object with a defined set of methods or [[API]], that the console object supports.
	console.log()
	console.warn
	console.error
	console.dir - displays javascript object to the console


Minification and obfuscation
	to reduce the amount of [[JavaScript]] that must be downloaded from a web server, developers often minify a website's [[JavaScript]]. Minification or minimization is the process of removing unnecessary characters from code so it executes the same but with fewer characters.\


# 7.2
# Document Object Model

Dom structure - [[Data Structure]] corresponding to the HTML document displays in a web browser. A [[DOM]] tree is a visualization of the structure.

Searching the [[DOM]]:
	document.getElementById() - returns [[DOM]] node whose id attribute is the same as the methods parameter
	document.getElementsByTagName() - returns array of all [[DOM]] nodes whose type is the same as the methods parameter
	document.getElementsByClassName() - method returns an array containing all the [[DOM]] nodes whose class attribute matches the methods parameter
	document.querySelectorAll() - method returns an array containing all [[DOM]] nodes that match the [[CSS]] selector passed as the methods parameter
	document.querySelector() - returns first element found in [[DOM]] that matches the [[CSS]] selector passed as the method's parameter.

Modifying [[DOM]] node attributes
	After searching the [[DOM]], [[JavaScript]] can be used to examine the element's attributes or to change the attributes. 
	ex: 
	- Change what image is displayed by modifying an `img` element's `src` attribute
	- Determine which image is currently being displayed by reading the `img` element's `src` attribute
	- Change an element's CSS styling by modifying the element's `style` attribute
removeAttribute() - removes attributes from the selected element

Modifying [[DOM]] node content
	textContent property gets or sets a [[DOM]] node's text content:
		document.querySelector("p").textContent="whatever" changes the paragraph to <p>Whatever</p>

innerHTML property gets or sets a [[DOM]] node's content including all of the node's children


# 7.3 More DOM modification

appendchild() - appends a [[DOM]] node to the object's child nodes.

insertBefore() - inserts a DOM node as a child node before an objects existing child node

removeChild() - method removes a node from the objects children


# 7.4 Event-driven programming

An event is an action, usually caused by a user, that the web browser responds to.

Event driven programming is a programming style where code runs only in response to various events. Code that runs in response to an event is called an [[Event Handler]] or event listener

click
mouseover
mouseout
mousemove
keydown
keyup
input

A <em>change</em> event is caused by an element value being modified

An <em>input</em> event is caused when the value of an input or textarea element is changed

A <em>load</em> event is caused when the browser completes loading a resource and dependent resources. Usually load is used within the body element to execute code once all the webpage's [[CSS]], [[JavaScript]] and images have finished loading

A <em>DOMContentLoaded</em> event is caused when the [[HTML]] file has been loaded and parsed, although other related resources such as [[CSS]], and [[JavaScript]] may not be

a <em>focus</em> even is caused when an element becomes the current receiver of keyboard input.

a <em>blur</em> event is caused when an element loses focus and the element will no longer receive future keyboard input

a <em>submit</em> event is caused when the user submits a form to the web server

talks about [[Event Handler]]

When an event occurs, the browser follows a simple DOM traversal process to determine which handlers are relevant and need to be called. The DOM traversal process has three phases: capturing, at target, and bubbling.

1. In the event capturing phase, the browser traverses the DOM tree from the root to the event target node, at each node calling any event-specific handlers that were explicitly registered for activation during the capturing phase.
    
2. In the at target phase, the browser calls all event-specific handlers registered on the target node.
    
3. In the event bubbling phase, the browser traverses the DOM tree from the event target node back to the root node, at each node calling all event-specific handlers registered for the bubbling phase on the current node.



# 7.5 Timers

Some events are related to time instead of user actions.

A web browser is able to execute a function after a time delay using setTimeout(x: function, y: time(ms)). 

The method takes two arguments, a function and time delay in ms

The browser calls the function after the time delay.
can be canceled by clearTimeout()

Intervals
A web browser is able to execute a function repeatedly with a time delay between calls using setInterval(x: function, y: time(ms)) method. This takes two arguments, a function and a time interval in ms. The browser calls the function every t milliseconds until the interval is cancelled. 

can be cleared by clearInterval()

# 7.6 Modifying CSS with javascript

[[JavaScript]] can manipulate a webpage's [[CSS]] dynmaically to alter the looks of a webpage

getPropertyValue() returns the value of an elements css property or an empty string if the property is not set
ex: elem.style.getPropertyValue("color") gets the elements color value
- The setProperty() method sets the value of an element's CSS property. Ex: `elem.style.setProperty("color", "blue")` sets the element's color to blue.
    
- The removeProperty() method removes an element's CSS property. Ex: `elem.style.removeProperty("color")` removes the element's color property.
    

The `style` CSS properties can alternatively be accessed and modified using JavaScript property names. Ex: `elem.style.color = "blue"` is equivalent to `elem.style.setProperty("color", "blue")`. CSS property names that have dashes are converted into property names that use camel case. Ex: `background-color` becomes the JavaScript property `backgroundColor`.


Using the CSSOM to manipulate CSS properties and stylesheets is useful and sometimes necessary, but mixing CSS with JavaScript code blurs the separation between a web application's presentation and functionality. Good practice is to declare CSS classes that perform the styling and use JavaScript to add and remove classes to and from DOM nodes as needed.

Every DOM node has a classList property that lists the classes assigned to the node. Ex: The div node created from `<div class="account warning">` has a `classList` with items "account" and "warning". Methods exist to add and remove `classList` items:

- The add() method adds a class to the node's `classList`. Ex: `elem.classList.add("mystyle")` adds the class `mystyle` to the element's list of classes.
    
- The remove() method removes a class from the node's `classList`. Ex: `elem.classList.remove("mystyle")` removes the class `mystyle` from the element's list of classes.
    
- The toggle() method adds the class to the node's `classList` if the class is not present. If the class is already present, the class is removed. Ex: `elem.classList.toggle("mystyle")` toggles the class `mystyle` on or off.
    

A DOM node's class list can also be modified directly using the className property, which is a space-delimited list of the classes assigned to the node. Ex: `elem.className = "cat adopted"` assigns the `cat` and `adopted` classes to the element and removes any previously assigned classes from the node. All classes assigned to `className` are also added to the node's `classList`. Adding and removing properties with `classList` is often easier than using `className`.





document.querySelector("#submitBtn").addEventListener("click", submitBtnClick);

function isStrongPassword(password) {
   if(password.length < 6){
      document.getElementById("1").classList.add("error")
      }
      else if (/d/.test(password)){
      document.getElementById("2").classList.add("error")
      }
      else if (password == "password1"){
      document.getElementById("3").classList.add("error")
      }
   return password.length >= 6 && /\d/.test(password) && password !== "password1";
}

function submitBtnClick() {
   let password = document.querySelector("#password").value;
   if (isStrongPassword(password)) {
      document.querySelector("#errorMsg").classList.add("hidden");
      
      // Remove error-textbox class
      
   } else {
      document.querySelector("#errorMsg").classList.remove("hidden");

      // Add error-textbox class

   }
}

# 7.7 Form validation

Data validation is checking input for correctness. A better user expereince occurs when the web browser performs the same data validation before submitting.

Validating form input with [[JavaScript]]
	Each textual imput in an [[HTML]] document has a value attribute that is associated with the user-entered text. 
	The `value` attribute can be used to validate user-entered text by checking desired properties, such as:

- Checking for a specific length using the `length` property on the `value` attribute
- Checking if entered text is a specific value using `===`
- Checking if the text contains a specific value using the string `indexOf()` method on the `value` attribute
- Checking if the text is a number using `isNaN()`
- Checking that text matches a desired pattern using a regular expression and the string `match()` method

### Validating form data upon submission

Validating form data using JavaScript that executes when the user submits the form can be performed by:

1. Register a handler for the form's submit event that executes a validation function.
    
2. Within the validation function, inspect the form's input fields via the appropriate DOM elements and element attributes.
    
3. If the form is invalid, call the `preventDefault()` method on the event to cancel the form submission and prevent the form data from being sent to the server.
[[Validation code example]]


# 7.8 Javascript object notation (JSON)

Communicating data between the server and browser is a significant task for modern web applications.
[[JSON]]

Communication with [[JSON]] is efficient because computers can transmit and parse [[JSON]] quickly. As a result, [[JSON]] has rapidly become the dominant format of data transfer between web browsers and servers

[[JSON]] has six basic data types defined in the [[JSON]] note here

{
   "name": "John Doe",
   "vehicles": [
      {
         "make": "Ford",
         "model": "F-150",
         "color": "white"
      }, 
      {
         "make": "Toyota",
         "model": "Camry",
         "color": "red"
      }
   ],
   "married": false,
   "previous_customer": true,
   "known_associates": [],
   "notes": null
}
This Json structure is an object with six name/value pairs
1. `name` has the string value `John Doe`.
2. `vehicles` has an array value of two objects. Each object in the vehicles array has three name/value pairs: make, model, and color.
    1. The array's first object's `make` is the string `Ford`, `model` is the string `F-150`, and `color` is the string `white`.
    2. The array's second object's `make` is `Toyota`, `model` is `Camry`, and `color` is `red`.
3. `married` is `false`.
4. `previous_customer` is `true`.
5. `known_associates` is an empty array.
6. `notes` is `null`.

JSON.parse() creates a [[JavaScript]] object from a string containing [[JSON]]. 
EX: JSON.parse('[1, "two", null]') converts the string '[1, "two", null]' into the [[JavaScript]] array [1, "two", null]. Typically Json.parse() is used with data received from a server

Json.stringify() method creates a string from a [[JavaScript]] object. Typically JSON.stringify() is used with data sent to a server. This creates a string representation of any passed object by either calling the object's toJson() method if defined or recursitvely serializing all the enumerable, non function properties
EX: json.stringify(new Date('2020-08-06')) converts the [[JavaScript]] date object to the string 2020-08-06T00:00:00.000Z by calling the Date object's toJson() method

JSON.stringify({a:"one",b:"two",c:"three"},["a","c"])
second argument is a replacer parameter and the result of this would be '{"a": "one","c":"three"}'

JSON.stringify({a:{b:1,c:3}}, null, '  ')
third argument is a spacer parameter which controls the whitespace
which yields this
'{
"a":{
	"b": 1,
	"c": 3
}
}'

# Assigning data with parsed values, then change value 'position'
let stringStructure = '{ "name": "Michael Jordan", "height": { "ft": 6, "in": 6 }, "points": 25, "position": "Power forward" }';

/* Your solution goes here */
jsonStructure = JSON.parse(stringStructure)
jsonStructure.position = "Point guard"

stringStructure = JSON.stringify(jsonStructure)

# Reviver function example, modifying year in the stringObject before returning it

let stringObject = '{ "year": 2017, "month": 8, "day":9, "hour": 8, "minute": 49 }';

let jsonData = JSON.parse(stringObject, function(key, value){
if(key == "year"){
return value + 4; //if our key is equal to the year we want to modify then modify it
}
return value; //else return the values
})

# Replacer example

let jsonObject = { "year": 2011, "month": 2, "day": 9, "hour": 9, "minute": 49 };

/* Your solution goes here */
let stringStructure = JSON.stringify(jsonObject, ["month", "day"])

only returning the month and day properties


# Spacer example 
let jsonData = { "day": "Thursday", "date": { "year": 2015, "month": 2, "day": 12 }, "time": { "hour": 11, "minute": 44 } };

/* Your solution goes here */
let a = JSON.stringify(jsonData, null, '.....')
console.log(a)

will input 5 dots before each item
{ ....."day": "Thursday", ....."date": { .........."year": 2015, .........."month": 2, .........."day": 12 .....}, ....."time": { .........."hour": 11, .........."minute": 44 .....} }



# XMLHttpRequest (ajax)

[[Ajax]] --defined


an XMLHttpRequest is an object for communicating with webservers using [[Ajax]]. Using this it allows web browsers to hide the communication latency and continue to provide a responsive user interface while waiting on server response.

The steps for using the XMLHttpRequest API are:

1. Create a new XMLHttpRequest object.
    
2. Assign handlers to the desired events via the `addEventListener()` method. The `addEventListener()` method takes two arguments: the event name and the event handler, code that should execute when the event occurs. If the handlers are not set up prior to calling the `open()` method, the progress events will not execute.
    
3. Initialize a connection to a remote resource using the `open()` method. The open() method takes two arguments: the HTTP request type and the URL for the resource. Most browsers only support "GET" and "POST" request types.
    
4. Modify the default HTTP request headers if needed with the setRequestHeader() method. Ex: `xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded")` sets the `Content-Type` header so a URL-encoded string may be sent in a POST request.
    
5. Send the HTTP request via the send() method. For POST requests, the data to be sent with the request is passed as the argument to the `send()` method.

# Common HTTP response status codes

|   |   |
|---|---|
|200|HTTP request successful|
|3XX|General form for request redirection errors|
|301|Resource permanently moved, the new URL is provided|
|4XX|General form for client errors|
|400|Bad request. Ex: Incorrect request syntax|
|401|Unauthorized request. Ex: Not properly authenticated.|
|403|Request forbidden. Ex: User does not have necessary permissions.|
|404|Not found. Ex: Requested resource does not exist.|
|5XX|General form for server error codes|
|500|Internal server error. Ex: Server-side code crashed.|
|503|Service unavailable. Ex: Webpage is temporarily unavailable due to site maintenance.|

# level 1 sotring new xmlhttprequest object in xhr var, then assigning event listener

function xhrHandler() {
   console.log("handling response: " + this.responseText);
}

/* Your solution goes here */
let xhr = new XMLHttpRequest();
xhr.addEventListener("load", xhrHandler)

# Level 2 
Using the xhr variable, initialize a connection to GET https://wp.zybooks.com/grades.php?name=Katie, set the response type to text, then send the request.

function responseReceivedHandler() {
   console.log("Response received");
}

let xhr = new XMLHttpRequest();
xhr.addEventListener("load", responseReceivedHandler);
xhr.open("GET", "https://wp.zybooks.com/grades.php?name=Katie")
xhr.responseType = 'json'
xhr.send()
/* Your solution goes here */


# Level 3 
Log "successful" to the console if the response's status is 200. Otherwise, log "not successful" to the console.

function responseReceivedHandler() {

   /* Your solution goes here */
if(this.status == 200){
   console.log('successful')
   }else{
      console.log('not successful')}
}

let xhr = new XMLHttpRequest();
xhr.addEventListener("load", responseReceivedHandler);
xhr.addEventListener("error", responseReceivedHandler);
xhr.open("GET", "https://wp.zybooks.com/weather.php?zip=90210");
xhr.send();

# Level 4 
If the response object's success property is true, log the final grade from the response to the console. Otherwise, log the error from the response to the console. Hint: this.response is the response.

function responseReceivedHandler() {
   /* Successful request:
      {
         "success": true,
         "grades": {
            "final": "...",
            ...
         }
      }

      Unsuccessful request:
      {
         "success": false,
         "error": "..."
      } */

   /* Your solution goes here */
if(this.response.success == true){
   console.log(this.response.grades.final)
   }else{
      console.log(this.response.error)}
}

let xhr = new XMLHttpRequest();
xhr.responseType = "json";
xhr.addEventListener("load", responseReceivedHandler);
xhr.open("GET", "https://wp.zybooks.com/grades.php?name=Kelly");
xhr.send();

# 7.10 Using third-party web API's

Most third-party web APIs are RESTful. A RESTful web API is a web API that is called with a URL that specifies API parameters and returns JSON or XML containing the API data. Ex: The URL http://linkedin.com/api/article?id=123 specifies the article ID 123, so the article would be returned formatted in JSON.

Third-party web APIs may be called from the web server or the web browser. This material shows how to call web APIs from the web browser using JavaScript.