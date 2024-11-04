
2024-09-13 21:04

Status:

Tags:[[web dev book ch 7]]

# Event Handler


Ways to use event handlers

1. Embedding the handler as part of the [[HTML]] such as<button onclick="clickHandler()">Click Me</button> this should be avoided because it mixes content and functionality 
2. Setting the [[DOM]] node event handler property directly using [[JavaScript]] - document.querySelector("#myButton").onclick = clickHandler. Using dom node properties is better than embedding handlers within the [[HTML]] but has the disadvantage that setting the property only allows one handler for that element to be registered
3. Using the [[JavaScript]] addEventListener() method to register an event handler for a [[DOM]] object. Ex: document.querySelector("#mybutton").addEventListener("click", clickHandler) registers a click event handler for the element wit the id "myButton". This method allows for separation of content and functionality and allows multiple handlers to be registered with an element for the same event

function myMouseoverHandler(event) {
   event.target.style.backgroundColor = "yellow";
}

function myMouseoutHandler(event) {
   event.target.style.backgroundColor = "white";
}
function myClickHandler(event){
   event.target.style.color = "black";
   }

// Register the event handlers here
let elements = document.getElementsByClassName("highlight");
for (let i = 0; i < elements.length; i++) {
   elements[i].addEventListener("mouseover", myMouseoverHandler);
   elements[i].addEventListener("mouseout", myMouseoutHandler);
   elements[i].addEventListener("click", myClickHandler)
}