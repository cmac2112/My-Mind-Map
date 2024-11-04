
2024-08-30 08:22

Status: in progress

Tags:[[URL]], [[Web dev book]], [[POST]], [[GET]], [[Escaping Characters]], [[Widgets]]

# web dev book ch 3

container - element in a web document body that has opening and closing tags.
<header>
<footer>
<address>
<main>
<section>
<article>
<nav>
<aside>
<div>
<span>

block elements: fills the width of the element's parent container and can contain other block elements, inline elements, and text. <h1> <table> <p>

Inline element: fills the minimum space possible in the elements parent container and can only contain text or other inline elements


3.2 Forms

<form> element allows the web browser to submit information from the user to the server
ex:
<form action="https://wp.zybooks.com/form-viewer.php" enctype="multipart/form-data" method="post">

GET method:
1. Collect all data from form fields into a query string. A query string is a set of name=value pairs separated by the ampersand character. Each name is specified as an attribute of the HTML field, and the value is the user entered data.
2. Create a [[URL]] with server page and name=value pairs. The url is composed of the action attribute specified in the form, the questionmark and the query string: http://example.com/apply?first=Rick&last=Deckard
3. use the newly created url to create and send an http get request
4. display or update the webpage using the http response received from the server

POST method: submit information to a web server by sending information in the http request body.
1. create an HTTP POST request using the url from the forms action attribute
2. create a query string from the form data
3. place the query string in the http request message body, and send the request.
4. display or update the webpage using the HTTP resposne received from the server

Escaping form data:
& ? and = all have special meaning in a query string. If a user enters these in a form they must be 'escaped' meaning the characters must be transformed into other representations.
Space -> +
All other reserved characters, newline, and tab -> %XX where XX is the ASCII hex value of the character

The web server un-escapes the data to determine its original value

<label> element displays descriptive text associated with a specific widget. A label has a for attribute whose value should match the id attribute for the widget being labeled. Labels help people using screen readers understand what input is expected

textarea widget allows user s to enter multiple lines of text and is created with the <textarea> element. 

checkbox: widget for input elements with the type attribute "checkbox"
sends on or off values to server

Radio button: widget for input elements with the type attribute of radio
sends radio's name and value attribute to the server

Drop-down menu: creates a dropdown menu which allows users to select <options>

List box: small vertical scrollbar list box

Button: button

Password field: widget for input of passwords

fieldset: groups related form widgets together and draws a box around the related widgets

Date picker: widget that allows the user to interactively pick a choice using a popup or other guided selection method

Color Picker: selector popup that helps the user explore and choose a color

Number Input: ensures user input is a value number

Range input: allows user to select a value by dragging a sliding control along the length of a line

Combo box: combination of a text box and drop down menu into a single widget

Audio element: plays an audio file in a webpage

source: used inside of auto element to specify an audio file to play.
autoplay, controls, loop, muted

Boolean attribute: attribute that is true when present and false when absent
<input type="checkbox" name="foodPreference" value="vegetarian" checked>
