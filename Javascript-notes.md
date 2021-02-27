# JavaScript

### What is JavaScript? 
- Javascript is the **Programming Language** to make web page interactive. It allows use to implement complex features on web pages
- It is the third layer of the layer cake of standard web technologies, together with HTML and CSS 
- Js designed to intergrate into HTML. All major web browsers support Javascript

### What do we use it for?
- We use it to update and change both HTML and CSS
- It can also calculate, manipulate and validate data

### Can we run JavaScript in a web browser, on a server, or both?
Depend on what the language is implemented for, it can also run on a server. Nodejs is a perfect example

### What programming paradigm(s) does JS support?

JavaScript is a prototype-based, multi-paradigm scripting language that is dynamic, and supports object-oriented, imperative, and functional programming styles.

- Prototype-based is a programming model that works on the concept of object cloning and prototyping. It utilizes object inheritance, where one object can be reused by another object without the need for creating any class. Behaviour reuse is performed by cloning existing objects that serve as prototypes

-

### What are the data types in JS?
- Primitive data type (single value, no behavior): Strings, Numbers (NaN is Number), Bool, Undefined, Null
- Reference data type (a group of states): Object, Function

### What is the type of NaN? What is the isNaN function?
- Type of NaN is number. Some array methods like indexOf and findIndex cannot find NaN
- isNaN function determine if the value is not a number or not

### What is the data type of a function?
Data type of a function is function (function is an instance of object)

### What about an array?
An array in Javascript is a special type of Object. It's a list-like Object whose item can be access using its index position. Its length can change anytime

### What is the difference between undefined and null?
- Null is the intentional absence of any object value
- Undefined means the variable has been declared but not assigned
- Null and Undefined is equal but not strickly equal
- (there is still an error shows that typeof null is an object)

### What are JS objects? what is the syntax?
- Js Objects represents one of Js data types. It used to stored various keyed collections and more complex entities
- Syntax: comma-separated list of name-value pairs wrapped in curly braces (optional comma if there is only 1 key value pair)

### What is JSON? Is it different from JS objects?
- JSON(JavaScript Object Notation) is a lightweight data-interchange format. It is a way to pass structured information between languages. JSON is built on 2 structures: a collection of key/value pairs and an order list of values
- Different:
 	- Unlike JavaScript Object, a JSON Object has to be fed into a variable as a String and then parsed into a JavaScript Object. 	
	- JSON cannot represent funtions or Date()
	- JSON keys must be quoted while Js key doesn't need to

### What are some ways you can use functions in JS?
- Invoke the function using ()
- Use as a variable value

#### Declare a function
4 ways to declare function in Js:
- Function Declaration
``` function divide(a,b){ return a/b}; ```
- Function expression
```const divide2 = function (a,b) {return a/b}; ```
- Arrow function Expression
``` const divide3 = (a,b) => {return a/b}```
- Arrow function Expression - Concise
```const divide4 = (a,b) => a/b;```

### What are the different scopes of variables in JS?
- Global scope: variable declared here are accessible from ANYWHERE. 
- Functional scope: variable declared and accessible within a that function's block {}
- Lexical/Block scoping: variable only accessible within that nested function or that a block of code

### What are the different ways to declare global variables?
- Declare a variable outside a function (if use var, that variable becomes a part of the global object and can be access through window.varNAM)
- Define a variable anywhere but do not write var, let, const before an assigment
- Declare it using window.variableName or this.variableName

### Is it a best practice to use global variables? Why or why not?
It is not a best practice to use global variable because:
- Global variable take longer to find than local variables
- It easy to forget where we declare a global variable.
- It can be overwritten by coworkers or ourself. This get even worse when we declare it by forgot the var/let/const keyword
- Affect security, specifically on the web where user had access to the window (or global) object and able to modify it

### What is function and variable hoisting?
- **Function hoisting**:
	- Function declaration was moved to the top of the scope. Because of that, we can call it before it was declare. Unlike variable hoisting, function hoisting hoist the function name and its declaration
``` javascript
sayHi()
function sayHi() {console.log('Hi')}
```
- A no name function (anonymous and arrow functions) will not be hoisted in Javascript because it is function expression, not function declaration
- **Variable hoisting**: 
	- A variable declaration will always internally be hoisted (moved) to the top of the current scope.
``` javascript
var hello; 
console.log(hello);
hello = "Hi"
// output: Hi
```
``` javascript
console.log(y)
var y = 7
```
- Because of hoisting, y had been declared before it is used. But because initialization are not hoisted, the value of y is undefined

### What is the global object in client-side JavaScript? - What are some built-in functions (methods on the global object)?
- The global obj in Javascript provides variable and functions that are available everywhere. In the browser, it is named window
- When scripts create global variables defined with the var keyword, they're created as members of the global object.
- Global function can be called using the window object as ```window.functionName()```
- Some build-in function of the global obj are alert, innerHeight, console

### What are callback functions? What about self-invoking functions?
- Callback function is a function that we define to be called by other function
``` javascript
function startup(){console.log("Starting")}
window.onload = startup()
```
- Self-invoking functions are function that invoke immediately after define. They are nameless most of the time

### What is closure and when should you use it?
- A closure is the combination of a function and the lexical scope within which that function was declared
- Closure means an inner function always has access to the variables of its outer function. It preversed the scope chain of the outer function by the time the outer function executed
``` javascript
function Counter(){
	var counter = 0
	function Increase() { return counter += 1 }
	return Increase
}
var counterApp = Counter()
alert(counterApp()) // 1
alert(counterApp()) // 2 
```
- Closure is an attempt at encapsulation. It can be use when we want to create some public functions that can access private function and variable

### Use the object literal syntax to create an object with some properties
(- A JavaScript object literal is a comma-separated list of name-value pairs wrapped in curly braces
- Object literals are defined using the following syntax rules:
	- A colon separates property name[1] from value
	- A comma separates each name-value pair from the next
	- A comma after the last name-value pair is optional)
- Create an object:
``` javascript
var random = {
    images: ["smile.gif", "grim.gif", "frown.gif", "bomb.gif"],
    pos: { 
        x: 40,
        y: 300
    },
    sumValue: function(a,b) {
        return a+b
    }
};
```

### What is a truthy or falsy value? List the falsy values.
- Js use type conversion to coerce(force) any value to a Boolean in context that require it
- A **falsy** value is a value that is considered false when encountered in a Boolean context. Ex: 0, '', null, undefined, NaN. (In && operator, if the obj is falsy, it returns that obj. Ex: ```0 && 'dog'``` -> 0)
- A truthly value is a value that is considered true when encounter in a Boolean context. All value are truthly unles defined as falsy (false, 0, 0n, '', null, undefined, NaN). Ex: {}, [], new Date(), Infinity, etc

### What is the difference between == and ===? Which one allows for type coercion?
- Loosly equal used to compareing 2 variables but ignores their datatype whereas Strickly equal compare both value and data type
- Loosely equal == allows type coercion while strictly equal does not

### Coercion
- There is only 3 type of conversion in Js: to String, to Number, to Boolean
- 2 types of coersion Implicit and explicit
- Implicit: 'true' == true, 12/'6', [1]>null, ['x'] = 'x', new Date(0) - 0, 123 + '' (turn to a string)
- Explicit: String(123) -> '123', String(true) -> 'true', Boolean({})->true (because it is not in the conversion list & not null/underfined/NaN), Boolean(null)->false, Boolean(2)->true, Number(true) -> 1, Number(null)->0

### Explain the template literal syntax
(- **Template literal** are string literals allowing embedded expressions. We can use multi-line strings and string interpolation features with them
- Replacement of placeholders with values inside of a string literal is called string interpolation)
- Template literals are enclosed by the backtick (``) character. They can contain placeholders, represented by the dollar sign and curly braces, with the expression in the curry bracket treated as Javascript (${expression}) 

### Explain what a strict mode does (```'use strict'```)
- Strict mode is a new feature in ECMAScript5 that allow us to place a program or function in a 'strict' operating context.

- **Converting mistake into error**
	- Strict mode makes it **impossible to accidentally create a global variables** (Reference Error)
	- Make an assigment which should have **silently fail** to **throw an exception**. Ex: ```var NaN = 2``` (Type Error) or write on a read only obj
	- It makes attempt to **delete undeletable properties** throw an error (Type Error)
	- It **forbids** a 0 prefixed **octal** literal (0644 === 420) or octal escape sequence ('\45' === '%')
	- It **forbid setting properties on primitive values** (throw a Type error). Without strict mode, it will be ignored
	- Some **reverse word cannot be used as a variable **(ex: argument)

- **Simplify variable use**
	- Duplicating a parameter name or an obj property is not allowed (Syntax Error)

-  strict mode **fixes mistakes that make it difficult for JavaScript engines to perform optimizations.**

- **Secure Js** by set this keyword to undefined

- Strict mode changes semantics. Relying on those changes will cause mistakes and errors in browsers which don't implement strict mode

### Explain how inheritance works in JS
- By default, every obj had a prototype. This property is empty by default. We can add property and method to it. If we create a child obj from a parent object whose prototype had some properties and methods, this child obj will inherit those property and methods, as well as inherit properties and methods of that prototype's protoype and so on until it reached null which is the final chain
``` javascript
// Every function expression in Js is a constructor
var x = function(j){
		this.j = j
		this.getJ = function () {return this.j}
	}
var x1 = new x(1)
console.log(x1.getJ()) // 1

var x = function(j){
		this.j = j
	}
x.prototype.getJ = function () {return this.j}
var x1 = new x(1)
console.log(x1.getJ()) // 1 -> behave the same aside from getJ() is now belong to x prototype

```
(- In order to inherit from a function, we need to use the call() function inside the Child to inherit all method and properties of the parent (like a super keyword).  (Parent.call(this, name, size))
- Then, we have to inherit the prototype of parent (by set the prototype of the child equal to Object.create of the parent's prototype Child.prototype = Object.create(Parent.prtotype). 
- And set the constructor of the child by set its prototype constructor to itself (Child.prototype.constructor = Child)
)

### What does the this keyword refer to?

### Explain the concept of lexical scope

### What will happen when I try to run this code: console.log(0.1+0.2==0.3) ?

## ES6+

### What new features did ES6 introduce?

### What is the difference between var, let, and const keywords?
- Var can be declared after used (```x=5; var x;```) but let and const will throw a ReferenceError (var, let and cost are hoisted to the top of the current scope, but let and const is in a temporal dead zone until it is declared)
- let keyword is a block scope variable while var key word is not. Once a var keyword declared inside an if or a loop statement, it moves to the top of that function scope and gives us undefined value when we try to access outside our if or loop statement

### Does JS have classes? If so, when were they introduced?
The class keyword was introduced in ES2015, but it is syntactical sugar. Javascript remains prototype base

## Events and DOM

### What is the DOM? How is it represented as a data structure? What object in a browser environment allows us to interact with the DOM?

### List some ways of querying the DOM for elements

### How would you insert a new element into the DOM?

### What are event listeners? What are some events we can listen for? What are some different ways of setting event listeners?

### What are some methods on the event object and what do they do?

### Default even listener? Bubling (false)
