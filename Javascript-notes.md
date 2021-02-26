# JavaScript

### What is JavaScript? 
- Javascript is the **Programming Language** to make web page interactive. It allows you to implement complex features on web pages
- It is the third layer of the layer cake of standard web technologies, together with HTML and CSS 
- Js designed to intergrate into HTML. All major web browsers support Javascript

### What do we use it for?
- We use it to update and change both HTML and CSS
- It can also calculate, manipulate and validate data

### Can we run JavaScript in a web browser, on a server, or both?
Depend on what the language is implemented for, it can also run on a server. Nodejs is a perfect example

### What programming paradigm(s) does JS support?

JavaScript is a prototype-based, multi-paradigm scripting language that is dynamic, and supports object-oriented, imperative, and functional programming styles.

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
- Syntax: curly bracket with key value pairs (the keys are string)

### What is JSON? Is it different from JS objects?

Unlike JavaScript Object, a JSON Object has to be fed into a variable as a String and then parsed into JavaScript. A framework like jQuery can be very helpful when doing parsing.

### What are some ways you can use functions in JS?
4 main ways to declare function in Js:
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
- Functional scope: variable declared within a function's block {}
- Lexical/Block scoping: variable declare in a nested function or in a block of code inside a function only accesible there

### What are the different ways to declare global variables?
- Declare a variable outside a function
- Define a variable anywhere but do not write var, let, const before an assigment

### Is it a best practice to use global variables? Why or why not?

### What is function and variable hoisting?
- **Function hoisting**:
	- Function declaration was moved to the top of the scope. Because of that, you can call it before it was declare
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
	- Because of hoisting, y had been declared before it is used. But because initialization are not hoisted, the value of y is undefined
```
console.log(y)
var y = 7
```

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
### What is closure and when should you use it?
Closure means an inner function always has access to the variables of its outer function. It preversed the scope chain of the outer function by the time the outer function executed
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

### What is a truthy or falsy value? List the falsy values.

### What is the difference between == and ===? Which one allows for type coercion?

### Explain the template literal syntax

### What are arrays in JS? can you change their size?

### Explain what “strict mode” does

### Explain how inheritance works in JS

### What does the this keyword refer to?

### Explain the concept of lexical scope

### What will happen when I try to run this code: console.log(0.1+0.2==0.3) ?

## ES6+

### What new features did ES6 introduce?

### What is the difference between var, let, and const keywords?
- Var can be declared after used (```x=5; var x;```) but let and const will throw a ReferenceError (var, let and cost are hoisted to the top of the current scope, but let and const is in a temporal dead zone until it is declared)

### Does JS have classes? If so, when were they introduced?

## Events and DOM

### What is the DOM? How is it represented as a data structure? What object in a browser environment allows us to interact with the DOM?

### List some ways of querying the DOM for elements

### How would you insert a new element into the DOM?

### What are event listeners? What are some events we can listen for? What are some different ways of setting event listeners?

### What are some methods on the event object and what do they do?

### Default even listener? Bubling (false)