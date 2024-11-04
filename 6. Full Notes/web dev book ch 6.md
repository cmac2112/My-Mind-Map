
2024-09-03 16:48

Status: chapter notes

Tags: [[Variables]], [[JavaScript]]

# web dev book ch 6

This chapter goes over the programming language basics of [[JavaScript]]

section 1 goes over the declaration of [[Variables]],
second 2 goes over simple arithmetic
second 3 goes over if else statements
section 4 more conditionals

Section 4: Truthy and falsy 
	A truthy value is a non-Boolean value that evaluates to true in a boolean context.

	EX: if (18) evaluates to True because non-zero numbers are truthy values

	A falsy value is a non-Boolean value that evaluates to false in a boolean context
	ex: if (null) evaluates to false because null is a falsy value

also talks about [[Conditional (ternary) Operator]]
switch statements

section 5 talks about [[While loop]], [[For statement loop]]

Section 6 Functions
[[Functions]]


# 6.7 Scope and the global object

### The var keyword and scope

In addition to declaring variables with `let`, a variable can be declared with the var keyword. Ex: `var x = 6;` declares the variable `x` with an initial value of 6. When JavaScript was first created, `var` was the only way to declare a variable. The `let` keyword was added to JavaScript in 2015.

Both `let` and `var` declare variables but with differing scope. A JavaScript variable's scope is the context in which the variable can be accessed.

A variable declared inside a function has local scope, so only the function that defines the variable has access to the local variable. A variable declared outside a function has global scope, and all functions have access to a global variable.

A variable declared inside a function with `var` has function scope: the variable is accessible anywhere within the function, but not outside. A variable declared inside a function with `let` has block scope: the variable is accessible only within the enclosing pair of braces.

A variable declared using `var` or `let` that is not inside a function creates a global variable that is accessible from anywhere in the code.


# 6.8 Arrays
[[Data Structure]]
[[For statement loop]]
[[Arrays]]


