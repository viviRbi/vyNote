# JavaScript

### What is JavaScript? 
- Javascript is the **Programming Language** to make web page interactive, we can implement complex features on web pages
- It was originally created as small scripting language that could interact with the DOM.
- Js designed to intergrate into HTML. All major web browsers support Javascript

### What do we use it for?
- We use it to update and change both HTML and CSS
- It can also calculate, manipulate and validate data

### Can we run JavaScript in a web browser, on a server, or both?
Depend on what the language is implemented for, it can also run on a server. Nodejs and Demo is a perfect example

### What programming paradigm(s) does JS support?

JavaScript is a prototype-based, multi-paradigm scripting language that is dynamic, and supports object-oriented, imperative, and functional programming styles.

- Prototype-based is a programming model that works on the concept of object cloning and prototyping. It utilizes object inheritance, where one object can be reused by another object without the need for creating any class. Behaviour reuse is performed by cloning existing objects that serve as prototypes

- Dynamic: It allows us to declare a value before knowing the data type, and we can switch the data type without causing error

- Fuctional: support first class function, which means functions in Js are treated like other variables

- Imperative: means command in Latin. It made up of clearly-defined sequence of instructions

- Object oriented: Javascript had all 4 of the 4 pillars of obj oriented:
	- Encapsulation: closure
	- Inheritance: each obj have a prototype obj the inherit methods and properties from other obj, and that obj also had a prototype that inherit from other obj, and so on until reached null, the end of the prototype chain
	- Polymorphism: 2 children object can overload a parent method
	- Abstraction: we can create abstraction in JS by throw new Error that prevent users from instantiate a new object. That obj now can only be use for inheritance 

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
- Invoke an anonymous function right after written using ()
- Use as a variable value
- Use as a callback function

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
**Old school**:
- Global scope: variable declared here are accessible from ANYWHERE. 
- Functional/ local scope: variable declared inside a function and cannot be access from global scope \n

**Modern**:
- Lexical/Block scoping: variable only know fron the top of the scope they are declared within. Can only use let and const to have achive a lexical/block scope (var will be hoisted to the very first outer function)

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
- Closure is a feature in Js that is very powerful
- It makes sure that the inner function always have access to the outer function even if the outer function had finished running and pop off the stack
- It preversed the scope chain of the outer function by the time the outer function executed
- (It is unwise to unnecessarily create functions within other functions if closures are not needed for a particular task, as it will negatively affect script performance both in terms of processing speed and memory consumption.)
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

### Explain what a strict mode does(```'use strict'```)
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

### Explain how inheritance works in J
- When it comes to inheritance, JavaScript only has one construct: objects since it's a prototype based language. Each object has a private property which holds a link to another object called its prototype.
- Prototype is empty by default. We can add property and method to it. If we create a child obj from a parent object whose prototype had some properties and methods, this child obj will inherit those property and methods, as well as inherit properties and methods of that prototype's protoype and so on until it reached null which is the final link of the prototype chain
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
- This keyword always refer to an object. It is a confused keyword because it different each time depend on where it is and how it is called
- Basically, it refers to the object that invokes the function where it is used
- Outside a function, and inside a function define in global scope, this refer to the global obj. 
- In cases where this inside a method attracted to an object, this become that object because the method it belong to will be invoked by that obj
- If we had an obj with a method inside, and we pass that method to an eventListener of a button, this keyword will no longer refer to that obj but refer to where the method is executed, which is the button object, which will throw us a property undefined error. The solution for this case is to bind the obj
```$('button').click(user.clickHandler.bind(user))```
- If a method in an object had a closure, this refered to the window obj. To avoid this problem, we should set this to a variable

### What is scope in Js?
- Scope in Js defines the accessibility of variables, objects and functions

### Explain the concept of lexical scope
- Lexical scoping means variables declared within a specific scope only accessible within that region

### What will happen when I try to run this code: console.log(0.1+0.2==0.3) ?
- The result will be false because Javascript use a double-precision floating point number (IEEE 754, binary64) which represent as binary, and most decimal fractions cannot be represnted exactly as binary fractions, so the floating-point arithmetic is not 100% accurate
- To avoid this problems, we should use integer as much as possible or use a library that provide an alternative to Javascript numbers

## ES6+

### What new features did ES6 introduce?
- let and const keyword with block scope
- Arrow function: short and concise
- New method for String prototype, array, array prototype, Math
	- A couple of new method to string prototype (startsWith, endsWith, includes, repeats)
	- New Array and Array prototype method (Array.from to create an array of NodeList from querySeletor), Array.of(2,4) to initalize array values, find, findIndex, fill
	- Couple of Math method (Math.sign to return sign of the number as 1 for positive,-1 as negative,0), Math.trunc(3.1) to return the number without fractional digits, Math.cbrt to retur nthe cube root of a number ex: 64 return 4)
- Template literal
- Spread Operator: takes an array or object and expands it (merge obj/array, clone obj/array, add new obj properties, array values)
``` javascript
const obj1 = {a:'a',b:'b'}
const obj2 = {c:'c', ...obj1}
```
- Destruturing: extract data from object or arrays
```javascript
let obj = {x:1, y:2};
let {x} = obj;
```
- Rest Parameter: collect array or object properties togetther
```javascript
const user = {name:'a', age: 2,address:'sd'}
const {age, ...rest} = user
console.log(age, rest)
```
Module (import, export)
``` javascript
export defult function (){}
import {sum, pi} from "lib/math";
import * as math from "lib/math"
```
- Class: which is basically a syntatic sugar for setting up prototype chains that provides cleaner inheritance. Js does not hoist class definition

### What is the difference between var, let, and const keywords?
- **Var** can be declared after used (```x=5; var x;```) but **let** and **const** will throw a ReferenceError (var, let and cost are hoisted to the top of the current scope, but let and const is in a temporal dead zone until it is declared)
- **let and const** keyword is a **block scope** variable while **var** keyword is **function scope**. Once a var keyword declared inside an if or a loop statement, it moves to the top of the outer function and gives us undefined value when we try to access outside our if or loop statement
- Redeclaring a variable using the let and const keyword will result in an error.
- If you try to change **const** variable or if you dont a set a value immediately, youll get an error

### Does JS have classes? If so, when were they introduced?
The class keyword and other oop-like keyword like constructor, super, static, getter, setterwas introduced in ES2015, but it is syntactical sugar. Javascript remains prototype base

## Events and DOM

### What is the DOM? How is it represented as a data structure? What object in a browser environment allows us to interact with the DOM?
***Dom***
- The Document Object Model (DOM) is a application programming interface(API) for HTML and XML documents. It defines the logical structure of documents and the way a document is accessed and manipulated.
(- DOM methods allow programmatic access to its tree-like structure; so you can change the structure, style or content of a document. 
- Nodes can have event handlers attached to them. Once an event is triggered, the event handlers get executed
- Web browser uses the DOM to render webpage .(html to DOM (to be render in web browser): Bytes -> Characters -> Tokens -> Node -> DOM)

***How the Dom represent Data Structure**
- The DOM represents a document with a logical tree. Each branch ends in a node, each noe contains obj.
- It is not a set of data structures, it is an object model that specifies interfaces. Although the document contains diagrams showing parent/child relationships, these are **logical relationships** defined by the **programming interfaces**, not representations of any particular internal data structures
- Their nodes are also not represent data structure, they **represent object**, which have function and identity

**What object in a browser environment allows us to interact with the DOM**
- Developer tool or The DOM Inspector? they are tool, not obj though
- window.document.all or window.document.querySelector(...) ?

### What is an API?
- Application Programming Interface
- It's like a restaurant menu. I have dishes with description. After we select a dish, the cooker do the work. We don't need to know how it was made

### List some ways of querying the DOM for elements

### How would you insert a new element into the DOM?
var a = document.createElement("div")
body.appendChild(a)
body.insertBefore(a, some old div a will be inserted before)
body.insertAfter(a, reference element)

### What are event listeners? What are some events we can listen for? What are some different ways of setting event listeners?
- Event Listener represents an object that can handle an event dispatched by an EventTarget object.
- Some event we can listen for is onChange, onClick, onFocus
- We can add EventListener using:
	- With a callback function ```el.addEventListener("click", modifyText, false);```
	- With an anonymous function ```l.addEventListener("click", function(){modifyText("four")}, false);```
	- With an arrow function ```el.addEventListener("click", () => { modifyText("four"); }, false);```

### What are some methods on the event object and what do they do?
- **stopPropagation**: prevent the bubbling or capturing events by stop all of the events of outer or inner html tag.
- **preventDefault**: cancel the default event (if it cancelable), like cancel the event of the submit btn

### Default event listener? 
``` element.addEventListener(eventName, eventHandler, useCapture -> default is false aka bubbling)```
- **Bubbling**: the event handled by the innermost element then move up
- **Capturing**: the event handle by the outermost element then go down
