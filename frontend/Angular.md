# Angular

## What makes a “single page application” (SPA) different from a normal web page?
- **Single Page Application** means there is only 1 true html file (usually index.html), and all components live there. We manage the layout(aka which component got displayed) by routing which copy html file style url 
- **Normal web page** in the other hand have multiple html file and each url represent 1 html file. 
- For first time load, normal webpage is faster but from the second time, single page application is faster

## Explain the difference between server-side and client-side rendering

**Server side (backend end) rendering**:
- The server get the data, use their programing language to **render** a webpage into plain HTML then send it to client.
 (ex: ```<h1>Hi <?php echo $username; ?> !</h1> // Hi Don```)
- It's a burden on memory and processing power on the Server
- Force user to wait while the page begin process and re-created. Good for SEO
- Faster at first time load

**Client side (front end) rendering**:
- Info from server managed using Javascript code, it'll be sent to the client and render into HTML. It was **process on the client** internet web browser
(ex: document.querySeletor("#hiDiv").innerHTML = "Hi "+ username // Hi Don)
- Faster response time, moreinteractive
- Tricky SEO
- Client browser must support client side language (javascript) 
- Slower at first time load

## What are some features of the Angular framework?
- Two-way data binding (ngModel) establish a connection between the user interface and business logic. When we input something, it will linked to a field in its Component class. We then can iterpolate that field in its html template
- Directives: instruction we provide to the DOM for rendering a template. ngModel for data binding is one of them, ng-repeat="x int names", *ng-if, *ng-for, @Component is also a directive
- Create user interface template in HTML rather than javascript
- Angular use Jasmine testing framework
- Also, Angular CLI is a pretty powerful tool

## How does TypeScript relate to JavaScript? What are the major benefits of using it over JavaScript?
- Javascript together with html and css are at the very core of the browser. It is a weakly and dynamic typed. It can cause a lots of unexpected errors
- TypeScript comes as a bridge to Javascript for developer with OOP background that support static typing, interfaces, classes. It compiles to pretty straightforward Javascript

## List the data types of TypeScript
- number, boolean, string, void (used on function return type), null, undefined, any

## How would you create a new Angular project?
Use the Anglar CLI: ng new projectName

## What is a component? How would you create one? List some other commands using the Angular CLI
- A component is the main building block of the application. It is a special kind of directive that uses a simpler configuration
- Each component control their own View and Data
- Each component had its own life cycle
- It inludes a component decorator( which contains template like html template link and metadata like selector, styleUrl) and an exported class
```angular
ng generate component componentName
ng g c componentName
ng g c componentName --flat
```


## What files make up a component? What is the “spec” file used for?
- A component make up of .html, .css, .ts, .spect.ts and they have to be declared in a module to be used
- spec file use for testing

## Explain the relevance of npm to Angular projects. Which file does npm use to track dependencies?
- If we clone an Angular project, we can use npm install to get all dependencies other users use
- package.json

## List some decorators for Angular apps
- A decorator allow you to attach meta data with a class, its member, or its method argument so Angular know which is which
- Class Decorators: @Component and @NgModule
- Property Decorators: @Input and @Output (These two decorators are used inside a class)
- Method Decorators: @HostListener (This decorator is used for methods inside a class like a click, mouse hover, etc.)
- Parameter Decorators: @Inject (This decorator is used inside class constructor).

## What is the lifecycle of a component? List some lifecycle hooks
- In Angular, every Component had a life cycle
- Every life cycle had 8 life cycle hooks
- They are: 
	- ngOnChances: called when an input values change. 1st time called before ngOnInit 
	- ngOnInit: called only once when compnent initalized. Good place to retrieve data from backend service
	- ngDoCheck: called during all change detection runs to update/detect changes 
	- ngAfterContentInit: linked with child component initalization
	- ngAfterContentChecked linked with child component initalization
	- ngAfterViewInit linked with child component initalization
	- ngAfterViewChecked linked with child component initalization
	- ngOnDestroy: This method will be executed just before Angular destroys the components. This method is very useful for unsubscribing the observables and detaching the event handlers to avoid memory leaks
- To use a life cycle hook, we need to implement its name
## What is a directive and what are the different types? How to tell these directives apart with syntax?
- A directive is instructions for rendering a template
- 3 diferent types:
	- Component: also know as Directives with templates, a special kind of Directive
	- Attribute Directives: change apperance or behavior of an element. Ex: 
```angular
<h1 [ngStyle]="aComponentField"></h1>
<button [attr.aria-label]="closeLabel"
```
	- Structural Directive (* asterisk): DOM structure/layout manipulation. Ex: *ngIf, *ngFor, *ngSwitch - *ngSwitchCase

## What is the benefit of using a directive like NgClass over the class attribute, or even property binding to the class attribute?
- With ngClass, we can pass multiple attributes. With class attribute, it's per attribute
- Property binding is more secure since Angular does not allow HTML with script tags.

What is a pipe? A service?
- A pile will transform a property before they are displayed. It seperated with a property by a vertical bar {{title | uppercase}}
- A service is a class with a focused purpose. It is used for features that are independent from any particular component and shared data or logic across components (or encapsulate external interactions)

How would you create a custom pipe? What about a service?
- To create a custom pipe:
	- ng generate pipe pipeName
	- @Pipe decorator to set pipe name
	- Implement PipeTransfrom interface
	- Use transform method with at least a parameter
	- Add it to any module need it

## How does dependency injection work in Angular?
- To have dependenct injection, we specify the dependency as paramenter with accessor keyword, follow by a name we made, then a semi colon, and its type (class name). Then we can use it by calling that name anywhere in the class
- It is a shortcut for declare the dependency field, pass it in construtor then set that field equal to it

What is an Angular module? What properties should you set inside it?
- It is a class with an NgModule decorator. Its purpose is to organize the pieces of our application and arrange them into blocks. It also allow us to sellectively adding classes from other module and re-export
- Properties we should set insided it (imports) is modules. Ex: RouteModule, BrowserModule, Form Module

What’s the difference between a JavaScript module and Angular module? What are some common Angular modules?
Js module | Angular module
-------- | --------
Each file is a module | A combination of diferent features, building blocks (component, directive, service, pipe)
Organize code | Organize application

How would you lazy load a module?
- First we must seperate some components to a features module. No app module should import this module or it'll eager load
- Then, in its own component, or in its owned route module.
- In the parent route module or app module, use loadChildren: es6 arrow function expression to import path to that module, then use .then to call that module class 

How have you used the HttpClient? What methods does it have and what do they return?
- Yes. HttpClient is a wrapper over the JavaScript XMLHttpRequest API
- Methods: get, post, 

What is an Observable? What’s the difference between it and a Promise?
- Observables are just 1 way to work with async in JavaScript. It is not belong to Angular alone but resides in a Js library called RxJs
- It is a wrapper around a stream of value (datasource). It called the subscribe method which have 3 functions to handle, 1 is success - a must have and 2 optional functions for error and complete
- An observable can only be accessed by a consumer who subscribes to it
oservable | promise
----- | -------
Aren't native to Javascript, it needs RxJs library | Doesn't need a third party
Able to cancel by unsubscribing | Cannot be cancel
Stream multiple events from the same API | Handle a signle event 

## What forms of data binding does Angular support? Explain the syntax for each
- 2 form: 2 way binding and 1 way binding. Using Form Module
- 1 way binding: 
	- (ngModel), for update the data to the component
	- Or [ng-model] or {{data.name}} is to display the existing data from component
- 2 way binding: [(ngModel)]="aComponentField"

## What does Webpack do for your ng project?
- Webpack is a Javascript module bundler. Angular cli uses it to pack and build the Angular app.
- It was embedding into Angular CLI. All of it complexicity was hidden. We can switch to native approach using ng eject to look at the webpack config file. But there's no way back
- A bundle is a JavaScript file that incorporates assets that belong together and should be served to the client in a response to a single file request. A bundle can include JavaScript, CSS, HTML, and almost any other kind of file.

## How would you implement routing in your project?
- Import RouterModule, Routes from @angluar/router
- Create a variable with Routes type, the minimum each object in the array must have is a path and a pointer to specify which component linked to that path
- In the import array in ngModule directive, add RouterModule.forRoot or forChild

## What is an EventEmitter and when would you use one?
EventEmitter used for a child to comunicate with its parent. It used with output decorative
```java
// child Component
@Output() propertyChange = new EventEmitter()
<button (click)= "propertyChange()"></button>
propertyChange(){this.propertyChange.emit("abc")}

// Parent Component
<child-component propertyChange="handleChildData($event)"></child-component>

handleChildData(data){
	console.log(data)
}
```

## What’s the difference between using reactive and template-driven forms? How would you setup each?
- Angular had 2 techniques to create forms: template-driven and reactive forms
template-driven | reactive
----- | -----
Build form completly in Html template | Build form and put logic in component
Cannot do unit test, validation handle by html input attr, error can also be display using html with ngIf, follow by inputName.error.required (or .minlength) | Able to do unit test
Make use of Forms module | Base on Reactive Forms Module
Mostly Asynchronus | Mostly Synchronous
Logic driven from template | Logic resides in component
- To setup templete driven, we import Form Module and use [(ngModel)] for every property followed by name attribute
```
<form #loginForm="ngForm" (ngSubmit)="login(loginForm.value)">
	<em *ngIf="loginForm.controls.password?.invalid && loginForm.controls.password?.touch"></em>
	<input (ngModel)="password" name="password" required id="password" />
</form

login(data){console.log(data)}
```
- **To setup reactive driven form**, we have to import ReactiveFormComponent in the module
- Then, we import {form-group, formControl} from '@angular/forms'
- Set a field and make their type FormGroup (temp name: profileForm)
- use ngOnInit to set that profileForm to a new FormGroup which each input field is equal to new FormControl()
- In html template, set [formGroup]="formName", formControlName="inputFieldName"
## How would you run your unit tests for an Angular project? ng test
