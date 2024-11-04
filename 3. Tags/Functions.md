
2024-08-26 18:09

Status:

Tags:[[C Book Ch 1]], [[C]], [[Python]], [[JavaScript]]

# Functions

functions as defined in [[C Book Ch 1]]
"A function contains statements that specify the computing operations to be done"
...
"C functions are like subroutines."

[[C]] main function serves as the entry point into your program

# Javascript
A function is a named group of statements. JavaScript functions are declared with the `function` keyword followed by the function name and parameter list in parentheses `()`. A parameter is a variable that supplies the function with input. The function's statements are enclosed in braces `{}`.

function functionName(parameter1, parameter2, ...) {
   // Statements to execute when function is called

}

defined in [[web dev book ch 6]]

JavaScript functions may be assigned to a variable with a function expression. A function expression is identical to a function declaration, except the function name may be omitted. A function without a name is called an anonymous function. Anonymous functions are often used with arrays and event handlers, discussed elsewhere in this material.

// Function name is omitted
let displaySum = function(x, y, z) {
   console.log(x + y + z);
}

// Function call
displaySum(2, 5, 3);

An arrow function is an anonymous function that uses an arrow `=>` to create a compact function. An arrow function's parameters are listed to the left of the arrow. The right side of the arrow may be a single expression or multiple statements in braces.

(parameter1, parameter2, ...) => expression

(parameter1, parameter2, ...) => { statements; }

  
let findSum = (a, b) => a + b;

let sum = findSum(3, 6);
console.log(sum);

let square = x => x * x;

console.log(square(5))

Inner function (nested function) is a function declared inside another function, An outer function is a functino containing an inner function. An inner function can access variables declared in the outer function



| Method                                              | Description                                                                                   | Example                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --------------------------------------------------- | --------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| push(value)                                         | Adds a value to the end of the array                                                          | let nums = [2, 4, 6];<br>nums.push(8);  // nums = [2, 4, 6, 8]                                                                                                                                                                                                                                                                                                                                                               |
| pop()                                               | Removes the last array element and returns the element                                        | let nums = [2, 4, 6];<br>let x = nums.pop();  // returns 6, nums = [2, 4]                                                                                                                                                                                                                                                                                                                                                    |
| unshift(value)                                      | Adds a value to the beginning of the array                                                    | let nums = [2, 4, 6];<br>nums.unshift(0);  // nums = [0, 2, 4, 6]                                                                                                                                                                                                                                                                                                                                                            |
| shift()                                             | Removes the first array element and returns the element                                       | let nums = [2, 4, 6];<br>let x = nums.shift();  // returns 2, nums = [4, 6]                                                                                                                                                                                                                                                                                                                                                  |
| splice(startingIndex, numElemToDelete, valuesToAdd) | Adds or removes elements from anywhere in the array and returns the deleted elements (if any) | let nums = [2, 4, 6, 8, 10];<br><br>// Deletes all elements from index 3 to the end<br>nums.splice(3);   // nums = [2, 4, 6]<br><br>// Deletes 2 elements starting at index 0 <br>nums.splice(0, 2);   // nums = [6]<br><br>// Adds 3, 5 starting at index 0 <br>nums.splice(0, 0, 3, 5);   // nums = [3, 5, 6]<br><br>// Adds 7, 9, 11 starting at index 2 <br>nums.splice(2, 0, 7, 9, 11);   // nums = [3, 5, 7, 9, 11, 6] |