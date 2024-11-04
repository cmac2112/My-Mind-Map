
2024-08-26 18:11

Status:

Tags:[[C Book Ch 1]], [[C]], [[JavaScript]]

# Variables in C

Variables as defined in the [[C Book Ch 1]].

"Variables store values used during the computation"

list of types in [[C]]
int: variables are integers

float: numbers that may have decimals.

The range of both float and int depends on the machine you are using; (old book) 16-bit ints, which lie between -32768 and +32767, are common. (most modern computers use 64bit architecture)

A float number is typically of 32-bit quantity with at least six significant digits and magnitude generally between about 10^-38 and 10^38 

Other C variable types

char: character - single byte
short: short integer
long: long integer
double: double precision floating point

# printing variables in C
%d: print as decimal integer
%6d: print as decimal integer, at least 6 characters wide
%f: print as floating point
%6f print as floating point, at least 6 characters wide
%.2f print as floating point, 2 characters after decimal point
%6.2f print as floating point, at least 6 wide and 2 after decimal point

%o: octal
%x: hexadecimal
%c: character
%s: string
%%: for % itself
%%

# Variables-in-Javascript
As described in [[web dev book ch 6]]
A variable is a named container that stores a value in memory
A variable declaration is a statement that declares a new variable with the keyword let followed by the variable name. Ex: `let score` declares a variable named score.

|   |   |   |
|---|---|---|
|string|Group of characters delimited with 'single' or "double" quotes|let name = "Naya";<br>let quote = 'He asked, "Shall we play a game?"';|
|number|Numbers with or without decimal places|let highScore = 950;<br>let pi = 3.14;|
|boolean|true or false|let hungry = true;<br>let thirsty = false;|
|array|List of items|let teams = ["Broncos", "Cowboys", "49ers"];|
|object|Collection of property and value pairs|let movie = { title:"Sing", rating:"PG" };|
|undefined|Variable that has not been assigned a value|let message;|
|null|Intentionally absent of any object value|let book = null;|
Printing variables:
console.log(var)
console.log("hello " + name + "how are you")

returns "hello (your name) how are you"

# scope js

A variable declared inside a function has local scope, so only the function that defines the variable has access to the local variable. A variable declared outside a function has global scope, and all functions have access to a global variable.

A variable declared inside a function with `var` has function scope: the variable is accessible anywhere within the function, but not outside. A variable declared inside a function with `let` has block scope: the variable is accessible only within the enclosing pair of braces.

A variable declared using `var` or `let` that is not inside a function creates a global variable that is accessible from anywhere in the code.