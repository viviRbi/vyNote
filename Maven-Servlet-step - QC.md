# Maven-Servlet QC

## What is a servlet? What about a servlet container? Which servlet container have you worked with?
- A servlet is a small Java program that runs within a Web server. Servlets receive and respond to requests from Web clients, usually across HTTP, the HyperText Transfer Protocol
- In Java, **Servlet container** (also known as aWeb container) generates dynamic web pages. Servlet Container communicates between client Browsers and the servlets. Servlet Container managing the life cycle of servlet. Servlet container loading the servlets into memory, initializing and invoking servlet methods and to destroy them. There are a lot of Servlet Containers like Jboss, Apache Tomcat, WebLogic etc.
- Tomcat
## Describe the servlet class inheritance hierarchy. What methods are declared in each class or interface?
- Servlet Classinheritance hierachy:
	- Interfaces: Servlet, ServletConfig, Serializable
	- Build-in class: GenericServlet(implements those 3 interfaces), HttpServlet extends from GenericServlet
User define methods which are http specific
## How would you create your own servlet?
	- Extends a class from HttpServlet and override the doPost, doGet method or extends from a GenericServlet and ovveride service method
## What is the deployment descriptor? What file configures your servlet container?
- **Seployement discriptor** describe how the web application should be deployed
- It is the web.xml file that reside in a WEB-INF at the webapp folder
- File configures servlet container is web.xml
## Explain the lifecycle of a servlet - what methods are called and when are they called?
-3 methods: init, service, destroy 
- **init**: the servlet container (like Tomcat) call init method exactly once after instantiating the servlet. The servlet container cannot place the servlet into service if the init method throws a ServletException or not return within a time period defined by the web browser
- **service**: called after init method completed successfull, by the servlet container to allow servlet to responsd to a request
- **destroy**: Called by the servlet container to indicate to a servlet that the servlet is being taken out of service. It clean up any resources that are being held (memory, file handlers, threads)
## Is eager or lazy loading of servlets the default? How would you change this?

## What are some tags you would find in the web.xml file?
<servlet>,<display-name>,<welcome-file-list>,<welcome-file><error-page><location>,<servlet>,<servlet-mapping>,<serlet-name>,<url-pattern>
## What is the difference between the ServletConfig and ServletContext objects? How do you retrieve these in your servlet?
- **ServletConfig** contains initialization and startup parameters for this servlet
- **ServletContext** defines a sets of methods that a servlet uses to communicate with its servlet container (get the MINE type of a file, dispatch request, or write a log file)

## What is the purpose of the RequestDispatcher?
- Defines an obj that receives requests from the client an sends them to any resources (servlet, html file, jsp file). 
- It 2 methods: forward and include
- forward: forwards a request from a servlet to another resources (servlet, html, jsp)
- include: to include the response of 1 servlet into another sevlet's response

## Explain the difference between RequestDispatcher.forward() and HttpServletResponse.sendRedirect()

## What are some different ways of tracking a session with servlets?

## What is object mapping? Any Java libraries for this?

## How would you send text or objects back in the body of the HTTP response from a servlet?

## What is the difference between getParameter() and getAttribute() methods?

## Explain the front controller design pattern

## Static and Dynamic web app
- Static: non-interractive that provide generic info
- Dynamic: runs on a web container, generate page on the fly by contacting database

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