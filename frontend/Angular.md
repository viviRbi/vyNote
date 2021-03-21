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
- number, boolean, string, void (used on function return type), null, undefined, any. Anything else is object type (array, enum, class, interfaces,...)

## How would you create a new Angular project?
Use the Anglar CLI: ng new projectName

## What is a component? How would you create one? List some other commands using the Angular CLI
- A component is the main building block of the application. It is a special kind of directive that uses a simpler configuration
- Each component control their own View and Data
- Each component had its own life cycle
- A component ts file inludes a component decorator( which contains template like html template link and metadata like selector, styleUrl) and an exported class
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
	- Attribute Directives: change apperance or behavior of an element. Ex: <h1 [ngStyle]="aComponentField"></h1>
	- Structural Directive (* asterisk): DOM structure/layout manipulation. Ex: *ngIf, *ngFor, *ngSwitch - *ngSwitchCase

What is the benefit of using a directive like NgClass over the class attribute, or even property binding to the class attribute?

What is a pipe? A service?

How would you create a custom pipe? What about a service?

How does dependency injection work in Angular?

What is an Angular module? What properties should you set inside it?

What’s the difference between a JavaScript module and Angular module? What are some common Angular modules?

How would you lazy load a module?

How have you used the HttpClient? What methods does it have and what do they return?

What is an Observable? What’s the difference between it and a Promise?

What forms of data binding does Angular support? Explain the syntax for each

What does Webpack do for your ng project?

How would you implement routing in your project?

What is an EventEmitter and when would you use one?

What’s the difference between using reactive and template-driven forms? How would you setup each?

How would you run your unit tests for an Angular project?
