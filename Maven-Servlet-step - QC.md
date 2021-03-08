# Maven-Servlet QC

## What is a servlet? What about a servlet container? Which servlet container have you worked with?
- A servlet is a small Java program that runs within a Web server. Servlets receive and respond to requests from Web clients, usually across HTTP, the HyperText Transfer Protocol
- In Java, **Servlet container** (also known as aWeb container) generates dynamic web pages. Servlet Container communicates between client Browsers and the servlets. Servlet Container managing the life cycle of servlet. Servlet container loading the servlets into memory, initializing and invoking servlet methods and to destroy them. There are a lot of Servlet Containers like Jboss, Apache Tomcat, WebLogic etc.
- Tomcat

## Describe the servlet class inheritance hierarchy. What methods are declared in each class or interface?
- Servlet Classinheritance hierachy:
	- Interfaces: Servlet, ServletConfig, Serializable
	- Build-in class: GenericServlet(implements those 3 interfaces), HttpServlet extends from GenericServlet
	- User define methods which are http specific
- Method in each class:
	- Servlet interface: init, service, destroy, getServerConfig, getServlet
	- Servlet Config Interface: getServletName, getServletContext, getInitParameter, getInitParameterNames
	- Serializable: from java.io.Seralizable
	- GenericServlet: getServletContext, getServletInfo, getServletName, abstract method service (force to override if extends)
	- HttpServlet: doHead, doPut, doDelete, doGet, doPost, service

## How would you create your own servlet?
- Create a Marven Project
- Add java.servlet dependency to pom.xml
- Create the Deployment Descriptor
- Extends a class from HttpServlet and override the doPost, doGet method or extends from a GenericServlet and ovveride service method

## What is the deployment descriptor? What file configures your servlet container?
- **Deployement discriptor** describe how the web application should be deployed
- It is the web.xml file that reside in a WEB-INF folder at the webapp folder
- File configures servlet container is web.xml

## Explain the lifecycle of a servlet - what methods are called and when are they called?
- **Life cycle of a servlet**: 4 phrases: Instanciation, Initialization, Servicing, Destruction
- Instanciation (loading and initializing Servlet by the web/servlet container)
- Initialization (container using Servlet.init(ServletConfig)) to instanciate the servlet object)
- Service (create Servlet Request and Response obj. If it is an Http class, create HttpServletRequest an Response obj which are their sub type. Then, it invoke Servlet.service obj when the Servlet Instance locaated to a service request)
-**3 methods**: init, service, destroy 
- **init**: the servlet container (like Tomcat) call init method exactly once after instantiating the servlet. The servlet container cannot place the servlet into service if the init method throws a ServletException or not return within a time period defined by the web browser
- **service**: called after init method completed successfull, by the servlet container to allow servlet to responsd to a request
- **destroy**: Called by the servlet container to indicate to a servlet that the servlet is being taken out of service. It clean up any resources that are being held (memory, file handlers, threads)

## Is eager or lazy loading of servlets the default? How would you change this?
- Lazy loading was servlet default. It only initialized when the client sends a request. Ex: photo do not load until user scroll down where the next photo are 
- EagerLoading is initialized through configuration in xml, it load all your resources as once. Good if your pafe light weight
- Add load-on-start-up to servlet tag in web.xml
```java
<servlet>
	<servlet-name>Abv<servlet-name>
	<servlet-class>com.java.AbvServlet</servlet>
	<load-on-startup>0</load-on-startup>
</servlet>
```

## What are some tags you would find in the web.xml file?
servlet,display-name,welcome-file-list,welcome-file,error-page,location,servlet,servlet-mapping,serlet-name,url-pattern

## What is the difference between the ServletConfig and ServletContext objects? How do you retrieve these in your servlet?
- **ServletConfig** contains initialization and startup parameters for a single servlet. Web container will create 1 ServletConfig instance for each servlet. Properties remain the same for users invoking the servlet. Can be used for a single servlet
- **ServletContext** its instance created by web container when we deploy a web application in it. It is global and can set and get attr of the whole application

## What is the purpose of the RequestDispatcher?
- Defines an obj that receives requests from the client an sends them to any resources (servlet, html file, jsp file). 
- It 2 methods: forward and include
- forward: forwards a request from a servlet to another resources (servlet, html, jsp)
- include: to include the response of 1 servlet into another sevlet's response

## Explain the difference between RequestDispatcher.forward() and HttpServletResponse.sendRedirect()
- RequestDispatcher.forward(): the request transfer to other resources within the same server, faster. We pass the request and response obj to the new resource. Move to url of http page but the web link still the same 
- HttpServletResponse.sendRedirect(): the request transfer to other resources (to a different domain, or server), slower. The old request and response obj are lost. Change url 

## What are some different ways of tracking a session with servlets?
- Using HttpSession
```java
HttpSession session = request.getSession();
session.setAttribute("username",username);
```
- Using cookies. Sometimes client turn cookie off
```java
String name = request.getParameter("username");
Cookie c = new Cookie("username", name);
response.addCookie
```
- Hidden form field

## What is object mapping? Any Java libraries for this?
- Object maping is the process of convert an object to other datatype or other object and reverse
- Library: Jackson ObjectMapper (JSON to obj and vice versa), (Model Mapper(map between models and Data Transfer Obj))

## How would you send text or objects back in the body of the HTTP response from a servlet?
- For servlet page:
	- Use PrintWriter and println method 

-For frontend and backend:
	- Send a request from front end to a servlet
	- That Servlet get the request 
	- It send some data back using PrintWritter println method or Dispatcher forward
	- Front end receive the data as Json, turn it to an obj and use querySelector to update html

## What is the difference between getParameter() and getAttribute() methods?
- getParameter used to retieve data from client page submit form. It returns a string
```html
<form>
	<input name="number" value = 2>
</form
```
```java
	class GetNum extends HttpServlet(...req, ...res) throws..{
		String a = req.getParameter("number"); // 2
		PrintWriter pw = res.getWriter();
		res.setContentType("text/html")
		pw.println(a + 6) //Send to frontend
		pw.close()
	}
```
- request.getAttribute() use to pass data to JSP/Serlet (server-side usageW, inside only 1 application). It can return object

## Explain the front controller design pattern
- All requests that come from a resource in an application will be handle by a single handler then dispatched to the appropriate handler for that type of request

## Static and Dynamic web app
- Static: non-interractive that provide generic info
- Dynamic: runs on a web container, generate page on the fly by contacting database

## GenericServlet vs HttpServlet
- Generic Servlet: Can be used with any protocol, service() is abstract method and should be overridden
- Http servlet: HTTP protocol only, service() need not be overidden and it can be replace with doGet, doPost

## Http error code
- Informational responses (100–199), Successful responses (200–299), Redirects (300–399), Client errors (400–499), Server errors (500–599)

-204: no content
- 400 Bad Request: server cannot understand the request due to invalid syntax
- 404: not found, 403: Forbiden (doesn't have permission to view content)
- 408: request timeout
- 500: internal server error (unexpected fault that prevent use from connect to the server)
- 503: Service unavailabe (server is not available because of overload traffic)
- 504: Gateway timeout: internet issue, the server does not response data in a timely manner
- 405: Method Not allow method is know by server but cannot be use