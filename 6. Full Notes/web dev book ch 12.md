
2024-10-17 21:02

Status:

Tags:[[Web dev book]],[[jquery]],[[JavaScript]]

# web dev book ch 12

# 12.1 Getting started with [[jQuery]]


## [[Javascript]] libraries

Developers use [[JavaScript]] libraries to simplify coding tasks. A [[library]] is a collection of functions that focus on a related set of tasks. [[jquery]] is a popular [[Javascript]] library that focuses on a broad range of tasks, many associated with the visual elements of a web page

```
## 

Library vs. framework

What is the difference between a "library" and a "framework"? A framework is a suite of libraries designed to offer a more comprehensive platform in which to program. When using a framework, the program's flow is dictated by the framework, not the programmer. Examples of popular JavaScript frameworks include [AngularJS](http://angularjs.org/), [Ember](http://emberjs.com/), and [Backbone.js](http://backbonejs.org/).
```

Table 12.1.1: Common tasks performed by jQuery.

|Task|Description|
|---|---|
|DOM manipulation|Find, alter, add, or remove DOM elements|
|User interaction|Respond to mouse clicks, mouse movement, or typing|
|Animation|Smoothly show, hide, or move webpage elements|
|Widgets|Display and manage the interaction of complex UI elements|
|Ajax|Issue asynchronous HTTP requests and handle responses|
|Browser quirks|Handle inconsistencies across different browsers|

## The `jQuery()` function

The [[jquery]] library defines a primary function called `jQuery()`. The function behaves differently depending on what arguments are passed to `jquery()`, but the function always returns a `jquery()` object. It is good practice to use [[Variables]] thar start with "$" to hold `jQuery` objects

`$()` is the same as `jQuery()`
# 12.2 Selectors

Basic Selectors

The `$()` function is used to select [[DOM]] elements using selectors. A selector is a string that is crafted to match specific [[DOM]] elements. Once an element is selected, other [[jquery]] methods can be used to add and remove [[CSS]] classes or properties from the selected element. The [[jquery]] method `addClass()` is used to add a [[CSS]] class to selected elements.

```
<!DOCTYPE html>
<html lang="en">
<title>jQuery Example</title>     
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<style>
   .important { color: red; }
</style>  
 
<p id="hello">Hello, jQuery!</p>    
<p>This stuff is great!</p>
    
<script>                
   let $allParas = $("p");
   $allParas.addClass("important");            
</script>  
</html>
```

1. The browser renders the webpage.
2. $("p") selects all `<p>` elements.
3. The addClass("important") method adds the "important" class to both paragraphs.
4. Changes to the DOM cause the browser to update the rendered webpage, making both paragraphs use a red font.


A web developer can select elements and call [[jquery]] methods to perform operations on the selected elements in a single line of code.

```

Example 12.2.1: Using $() and removeClass() on a single line.

// Select all paragraphs, then remove the "important" class from all of them
$("p").removeClass("important");
```

Table 12.2.1: Basic jQuery selectors.

|Selector Type|Example|Explanation|
|---|---|---|
|Element|$("p")|Selects all `<p>` elements|
|ID|$("#hello")|Selects the element with `id="hello"`|
|Class|$(".important")|Selects all elements with `class="important"`|

## Additional selectors

Attribute - selects elements based on attributes
Basic filter - Selects elements based on a variety properties
Child filter - Selects child elements based on location or other properties
Content filter - Selects elements based on an element's contents
Hierarchy selector - Selects elements based on an element's location within the [[DOM]] hierarchy

Table 12.2.2: Additional jQuery selectors.

|Selector Type|Example|Explanation|
|---|---|---|
|Attribute|$("span[id]")|Selects all `<span>` that have an `id` attribute|
|Attribute|$("a[href$='.pdf']")|Selects all `<a>` with `href` attributes ending in .pdf|
|Basic filter|$("p:first")|Selects the first `<p>` element|
|Basic filter|$("tr:even")|Selects the first, third, fifth, etc. table rows (zero-indexed)|
|Basic filter|$("li:eq(1)")|Selects the second `<li>` element (index `n`)|
|Child filter|$("li:last-child")|Selects the last `<li>` in each group|
|Content filter|$("p:contains('bye')")|Selects all `<p>` that contain the word "bye"|
|Hierarchy|$("li span")|Selects all `<span>` that are descendants of `<li>`|

# 12.3 Events

## [[Event Handler]]s

A developer may use [[jquery]] to define an event handler.
the jquery() `on()` method takes two arguments: an event name and an event handler. The event handler is registered to the selected elements of a jquery object

```
function buttonClicked() {
   alert("Click!");
}

$("#some-btn").on("click", buttonClicked);
```

## The Ready event

one of the most important [[jquery]] events is the `ready` event. The ready event is triggered when the browser has finally finished loading the webpages [[DOM]]. Good practice is to use [[jquery]] selectors inside the ready event handler to ensure the [[DOM]] is fully loaded before searching the [[DOM]] for elements

```
## 

Figure 12.3.1: Waiting for the ready event.

// Wait until the document's DOM is ready
$(document).ready(function() {
   // DOM is ready to go
   $("button").addClass("big");
});

Developers use the `ready` event so frequently that the shortcut `ready()` method is not needed. The `$()` function can be supplied an event handler that will only execute when the `ready` event triggers on the document.

## 

Figure 12.3.2: Registering a ready event handler with $().

$(function() {
   // DOM is ready to go
   $("button").addClass("big");
});
```

## Mouse events

[[jquery]] supports many types of mouse events besides click
Table 12.3.1: Mouse events.

|Event|Description|
|---|---|
|click|Triggered when the user clicks an element.|
|dblclick|Triggered when the user double-clicks an element.|
|mousedown / mouseup|Triggered when the user first clicks down on an element or releases the mouse.|
|mouseover / mouseout|Triggered when the mouse enters or leaves an element.|
|mousemove|Triggered when the mouse is moved while inside an element.|
## Keyboard and form events

[[jquery]] supports keyboard events that are helpful when a webpage needs to react to the user pressing or releasing keys on a keyboard. Ex: moving a spaceship left or right depending on what key is pressed.

Table 12.3.2: Keyboard events.

|Event|Description|
|---|---|
|keydown|Triggered when the user first presses a key on the keyboard.|
|keyup|Triggered when the user releases a key from the keyboard.|
|keypress|Triggered when the browser registers keyboard input from printable character keys. Non-printing keys like Shift and Esc do not register keypress events.|

Table 12.3.3: Form events.

|Event|Description|
|---|---|
|focus / blur|Triggered when an element gains or loses focus.|
|focusin / focusout|Triggered when an element or any of the element's children gain or lose focus.|
|change|Triggered when an element's value changes.|
|select|Triggered when a user selects text in an `<input type="text">` or `<textarea>` element.|
|submit|Triggered when the user is attempting to submit a form.|
```
$(function() {
   let $div = $("div");
           
   $div.on("mouseover", function() {
      $div.addClass("big");
   }).on("mouseout", function() {
      $div.removeClass("big");
   });
   
   $div.mousemove(function() {
     $div.toggleClass("yellow");
   });
});
```

# 12.4 Styles and animation

## The `css()` method

jquery simplifies the process of adding and removing [[CSS]] properties to an element's inline style. [[CSS]] properties can be added to selected elements with the `css()` method.

```
$("body").css("background-color", "peachpuff");

$("body").css({
   color: "green",
   "font-size": "20pt"
});
```

## JQuery effects

jquery has three sets of animation methods for showing and hiding webpage elements. The animation methods in the table below alter various [[CSS]] peroperties of selected elements to produce animations. The methods take a speed argument that determines the duration of the animation.

| Methods                                       | Example                                                                                  | Description                                   |
| --------------------------------------------- | ---------------------------------------------------------------------------------------- | --------------------------------------------- |
| show()  <br>hide()  <br>toggle()              | $("h1").show("slow");<br>$("h1").hide("slow");<br>$("h1").toggle("slow");                | Alters width, height, and opacity all at once |
| fadeIn()  <br>fadeOut()  <br>fadeToggle()     | $("h1").fadeIn("normal");<br>$("h1").fadeOut("normal");<br>$("h1").fadeToggle("normal"); | Alters opacity only                           |
| slideDown()  <br>slideUp()  <br>slideToggle() | $("h1").slideDown("fast");<br>$("h1").slideUp("fast");<br>$("h1").slideToggle("fast");   | Alters height only                            |
| Argument                                      | Example                                                                                  | Explanation                                   |
| `"slow"`                                      | $("p").show("slow");                                                                     | 0.6 seconds to show the paragraph             |
| `"normal"`                                    | $("p").show("normal");                                                                   | 0.4 seconds to show the paragraph             |
| `"fast"`                                      | $("p").show("fast");                                                                     | 0.2 seconds to show the paragraph             |
| milliseconds                                  | $("p").show(1500);                                                                       | 1.5 seconds to show the paragraph             |

## controlling animation order

Sometimes an operation should be performed after an effect completes. However, code that is written after a call to an animation method will execute before the animation is complete. To execute code after an animation is complete, the jquery animation methods can be passed a callback function
```
$("h1").fadeOut("slow"); 
$("h2").fadeOut("slow");

$("h1").fadeIn("slow", function() {
  $("h2").fadeIn("slow");
});
1. The fadeOut() methods cause <h1> and <h2> to fade out at the same time.
2. The first fadeIn() completes before the second fadeIn() is called, so <h2> fades in after <h1> has finished fading in.
```

when tow animations are applied to different elements, the animations occur at the same time. However, when two animations are applied to the same element, the first animation completes before starting the second animation. Jquery queues animations applied to the same element so that each animation finished before the next beings..

```
// Both animations occur at the same time
$("h1").fadeOut("slow");
$("h2").fadeOut("slow");

// Animations on the same element are queued
$("h1").fadeIn("slow");
$("h1").slideUp(1000);
```

```
$("h1").hide("slow")
   .addClass("important")  // Called immediately, not waiting for hide to complete
   .slideDown(1000);
```

Jquery provides a `queue()` method to aid in queuing code that should be executed after the previous animations complete. The `queue()` method can take the place of the callback function used with the animation methods. The `queue()` method takes a function argument that is passed as a function parameter called `next`. The `next` function must be called so the next animation in the queue can be processed. 

```
$("h1").hide("slow")
   .queue(function(next) {
      // Add the class after the <h1> hide completes
      $(this).addClass("important");

      // Process the next animation in the queue
      next();
   })
   .slideDown(1000);
```

## the animate() method

the `animate()` method creates an animation by specifying a set of [[CSS]] properties to change over the animations duration. `animate()` has 4 parameters, but only the first is required

1. properties - Object map of CSS properties specifying ending values
2. duration - Animation duration in milliseconds
3. easing - Easing function applied to the transition
4. complete - function called once when the animation completes

```
<body>
  <img src="cat.jpg" alt="cat"
     style="position: absolute;           
            left: 200px;
            top: 50px;
            height: 40px;
            width: 140px;
            opacity: 0.1;
            border: 2px solid red">
</body>
```
```
$("img").animate({
   left: "200px",
   height: "-=60"
}, "slow", "linear");

$("img").animate({
   opacity: 0.1,
   top: "+=50"
}, 2000);
                
$("img").animate({
   opacity: 1,
   width: "200px"
}, function() {
   $(this).css("border", "2px solid red");
});

1. The cat image initially displays 10px from the browser's left edge with a 100px height.
2. The first call to animate() specifies the two CSS properties to animate (left and height), a "slow" duration, and "linear" easing function.
3. animate() makes image's left become 200px and height become 100px - 60 = 40px with linear easing over 0.6 secs (length of "slow").
4. The second animate() call makes image's opacity change to 0.1, top to 0 + 50 = 50px over 2 seconds.
5. The third animate() call makes image's opacity change to 1 and width to 200px over 0.4 seconds (default length of time).
6. The complete function executes after the animation completes and calls css() to set the image's border to solid red.
```

# 12.5 [[DOM]] manipulation

Accessing element attributes

Jquery provides many methods for [[DOM]] manipulations that allow developers to dynmaically add, remove, or modify content on a webpage

the `arrt()` method gets and sets attribute values of a [[DOM]] element

```
// Change all images to <img src="star.png">
$("img").attr("src", "star.png");

// Change all images to <img src="star.png" alt="Bright star">
$("img").attr({
   src: "star.png",
   alt: "Bright star",
});
```

## Adding [[DOM]] nodes

The $() function creates new [[DOM]] nodes when given an [[HTML]] string
ex: `$("<span>)I'm a new node!</span>");` creates a span node. However, the new node is not visible until the node is added to the [[DOM]]

Table 12.5.1: Methods for adding DOM nodes.

| Methods                      | Example                                                                                                        | Before                                        | After                                                                   |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------- | --------------------------------------------- | ----------------------------------------------------------------------- |
| prependTo()  <br>prepend()   | ```<br>```$("<li>New first</li>").prependTo("ol");<br><br>// same as<br>$("ol").prepend("<li>New first</li>"); | <ol><br>  <li>A</li><br>  <li>B</li><br></ol> | <ol><br>   <li>New first</li>   <li>A</li><br>   <li>B</li><br></ol>    |
| appendTo()  <br>append()     | ```<br>```$("<li>New last</li>").appendTo("ol");<br><br>// same as<br>$("ol").append("<li>New last</li>");     | <ol><br>  <li>A</li><br>  <li>B</li><br></ol> | <ol><br>   <li>A</li><br>   <li>B</li><br>   <li>New last</li><br></ol> |
| insertBefore()  <br>before() | ```<br>```$("<p>Before</p>").insertBefore("h2");<br><br>// same as<br>$("h2").before("<p>Before</p>");         | <h2>Test</h2>                                 | <p>Before</p><br><h2>Test</h2>                                          |
| insertAfter()  <br>after()   | ```<br>```$("<p>After</p>").insertAfter("h2");<br><br>// same as<br>$("h2").after("<p>After</p>");             | <h2>Test</h2>                                 | <h2>Test</h2><br><p>After</p>                                           |
| wrap()                       | ```<br>```$("p").wrap("<div></div>");                                                                          | <p>A</p><br><p>B</p>                          | <div><br>   <p>A</p><br></div><br><div><br>   <p>B</p><br></div>        |
| wrapAll()                    | `$("p").wrapAll("<div></div>");                                                                                | <p>A</p><br><p>B</p>                          | <div><br>   <p>A</p><br>   <p>B</p><br></div>                           |
| wrapInner()                  | `$("p").wrapInner("<div></div>");                                                                              | <p>A</p><br><p>B</p>                          | <p><br>   <div>A</div><br></p><br><p><br>   <div>B</div><br></p>        |

## removing [[DOM]] nodes and manipulating [[HTML]] text

The jquery methods remove() and detach() remove dom nodes. Both methods are identical except `detach()` returns the removed nodes to the called as a Jquery object in case the developer wants to use the nodes for other purposes

| Methods    | Example                            | Before                                    | After         |
| ---------- | ---------------------------------- | ----------------------------------------- | ------------- |
| `remove()` | $("li").remove();                  | <ol><br>  <li>A</li>  <li>B</li><br></ol> | <ol><br></ol> |
| `detach()` | let $listElems = $("li").detach(); | <ol><br>  <li>A</li>  <li>B</li><br></ol> | <ol><br></ol> |


# 12.6 Ajax

## Loading [[HTML]] snippets

Writing [[Ajax]] code with plain [[JavaScript]] can be a daunting task, so [[jquery]] provides several functions to make writing [[Ajax]] code easier.

The `load()` method is used for asynchronously loading a short snippet of [[HTML]] that is inserted into a webpage

```
<body>
  <h1>Movie Information</h1>  
  <p id="movieinfo">
    <cite>Star Wars</cite>: Rated PG, released in 1977
  </p>         
</body>

$("#movieinfo").load("starwars.html")'


1. Browser renders the webpage with no movie information.
2. The load() method sends an HTTP request for starwars.html from the web server.
3. The web server responds with starwars.html in the HTTP response.
4. The content of starwars.html is placed in the paragraph with ID movieinfo.
5. The browser updates when the DOM is altered, displaying the movie information.
```


## [[GET]] and [[POST]] requests

Most web applications use [[Ajax]] to interact with programs that run on a web server. The programs may be created using a number of server-side technologies including [[PHP]], [[Node.js]], [[ASP.NET]], [[Python]], and [[Java]]. Regardless of what technology is being used on the web server, the server-side program generally accepts data from an [[Ajax]] request, uses the data to query a database, and send the response back to the web browser.

The web server's response may contain [[HTML]] or plain text, but frequently the response contains data in [[XML]] or [[JSON]] format. The [[jquery]] library has functions for parsing [[XML]] data, but [[JSON]] data is parsed automatically and is generally easier for web developers to work with.

The [[jquery]] methods `$.get()` and `$.post()` are general-purpose functions for sending asynchronous [[HTTP]] [[GET]] and [[POST]] requests to the web server. Both $.get and $.post are methods of the global `jquery` object, unlike methods like load() that work on instances of jquery objects

## The `$.ajax()` method

the $.ajax() method is a general purpose method for making [[Ajax]] requests. The $.ajax() method can send [[GET]] and [[POST]] requests like $.get() and $.post() but can also send [[PUT]] and [[DELETE]] requests.

The $.ajax() method's settings parameter is an object with a number of properties

- [[URL]] - the url to request
- method - [[HTTP]] request method "[[GET]]", "[[POST]]", etc.
- data - object that is converted into key/value pairs for a query string and sent in the request
- dataType - type of data expected back like html, json, text, xml etc

all the methods like ajax, get, and post returna jqXHR object. The jqXHR object has a callback method `done()` that is called when a successful HTTP response is received

```
// Data to send in request
let requestData = { title: "Star Wars" };

// Make GET request for Star Wars
$.get("lookup.php", requestData, function(data) { 
   console.log("success"); }, "json");

// Same thing as $.get()
$.ajax({
   url: "lookup.php", 
   method: "GET",
   data: requestData,
   dataType: "json"
})
.done(function(data) {
   console.log("success");
});
```

## Handling errors

common errors to handle

1. web server returns an empty response or a response with an error message because the requested data was not found
2. the web server returns a 40x or 500 response code
the jqXHR object has a callback method fail() that is called when a 40x or 500 response code is received from the [[Ajax]] request
```
// (a)
$.get("lookup.php", requestData, function(data) {
   if (data.title) {
      $("#movieinfo").html("<cite>" + data.title + "</cite>: Rated " +
         data.rating + ", released in " + data.year);
   }
   else {
      $("#movieinfo").html("The movie title could not be found.");
   }
}, "json");

// (b)
$.get("lookup.php", requestData, function(data) {
   $("#movieinfo").html("<cite>" + data.title + "</cite>: Rated " +
      data.rating + ", released in " + data.year);
}, "json").fail(function(jqXHR) {
   $("#movieinfo").html("There was a problem contacting the server: " +
      jqXHR.status + " " + jqXHR.responseText);
});
```