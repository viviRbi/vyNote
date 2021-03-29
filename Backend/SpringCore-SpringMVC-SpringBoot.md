# Spring
## What is Spring?
- Spring an umbrella term for a family of frameworks which can be utilized to rapidly create loosely coupled Java applications (lossly coupled = low or weak coupling. When two or more hardware and software components are attached or linked together to provide two services that are not dependent on one another)
- Spring start out as an **inversion of control container** for Java(IoC Container)(which often refer as dependency injection DI) (- IoC, or DI is the D- Dependency Inversion in SOLID ) 
- Spring enables developers to build java applications utilizing a POJO design pattern, and applying enterprises services, as needed.

## What is POJO?
- It is a Java object that doesn't extend or implement some specialized classes and interfaces respectively require by the EJB framework

## Aplication context interface
- Repesent IoC
- Use it though ClassPathXmlApplicationContext and FileSystemXmlApplicationContext
```
ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml")
```
## Advantage of Spring
- Predefined Templates
- Loose Couping
- Easy to test
- Light weight
- Fast developement
- Powerful abstaction
- Declarative support
# Spring Core

##  What are Spring Projects and Spring Modules? 
https://springtutorials.com/spring-ecosystem/
- Before Spring 3 came out, the entire Spring Framework can be download as one big jar. But then they stop that because of the module conflict of different jars version
- **Spring Project**:
	- Developed on top of Spring Framework
	- Contains 1 or more module
	- A Spring project will bring all its dependency together
	- Ex: Spring Boot, Cloud, Security, mobile
- **Spring Module**:
	- It is the building blocks of Spring project and Framework. It exists from day 1
	- A Spring Module is a complete and independent feature with minimal dependency on other external libraries and projects
	- Ex: Spring JDBC, Spring Web, and Spring MVC

##  What is IOC and what does the IOC Container do?
- IoC stands for Inversion of Control. It is a principle which is all about inverting the control to achieve loose coupling between classes. It implemented using DI - Dependency injection
- IOC Container is a framework used to manage automatic dependency injection throughout the application without creating them
- We cannot achieve loosely coupled classes by using IoC alone. Along with IoC, we also need to use DIP, DI and IoC container.
- Process: Tigtly Coupled Class -> Implement IoC using Factory Pattern -> Implement DIP by creating abstraction -> Implement DI -> Use IoC Container -> Loosely Coupled classes
- Note: it is used together with DIP, Dependency Inversion Principle, the 5th one fron SOLID OOP design principle which states that states that the high-level module must not depend on the low-level module, but they should depend on abstractions.
	- Principle: IoC, PIP
	- Pattern: DI
	- Framwork: IoC Container

##  What is dependency injection and what are some of the benefits of using dependency injection?
- Dependency injection is a design pattern which implements the IoC principle to invert the creation of dependent objects
- It uses one object to suplies the dependencies of other object

- **Types** the injector class injects the service (dependency) to the client (dependent). The injector class injects dependencies broadly in three ways: through a constructor, through a property, or through a method:

	- Constructor Injection: In the constructor injection, the injector supplies the service (dependency) through the client class constructor.

	- Property Injection: In the property injection (aka the Setter Injection), the injector supplies the dependency through a public property of the client class.

	- Method Injection: the dependency provides an injector method that will inject the dependency into any client passed to it. Clients must implement an interface that exposes a setter method that accepts the dependency.

    
##  What types of dependency injection does Spring support?
- Constructor base dependecy injection
- Setter base dependecy injection
    
##  What are some differences between BeanFactory and ApplicationContext? Which one eagerly instantiates your beans?
BeanFactory | ApplicationContext
------ | -------
Loads on demand (lazy loading) | Load on Startup (Lazy loading)
Considered a lightweight Container | Considered a heavy Container
Interface, older | Interface extends from BeanFactory Interface
Only support Singleton and prototype | More features. Provide several suitable features for enterprise applications. Preferable in complex enterprise application. Suport all 5 type of bean scopes (Singleton,Prototype, Request, Session, Global)
Automatically registers BeanFactoryPostProcessor and BeanPostProcessor at startup | Does not register these interfaces automatically (while Spring 2 and above use BeanPostProcessor heavily)

## What is Spring Bean
- It is a POJO that managed by the Spring IoC container
    
##  What is the Spring Bean lifecycle?
- Spring Bean life cycle had 2 hooks: init and destroy
- It managed by the spring container
- To set an init method, inside application context, declared the bean class, and the init method name

```java
//aplication context
<bean name="MainBean" class="com.example.MainBean">
	<constructor-arg name="motdServiceBean"  ref="MotdServiceBean" />
</bean>
<bean name="MotdServiceBean" class="com.example.services.MotdServiceBean" init-method="initMotds">
	<property name="defaultMotdIndex"><value>4</value></property>
</bean>

//main bean class
public class MainBean {
	private MotdServiceBean motdServiceBean;

	public MainBean(MotdServiceBean motdServiceBean) {
		this.motdServiceBean = motdServiceBean;
	}
	
	public static void main(String[] args) {
		AbstractApplicationContext ac = new ClassPathXmlApplicationContext("application-context.xml");
		 MainBean mainBean = ac.getBean("MainBean", MainBean.class);
						System.out.println(mainBean.motdServiceBean.getMotd(-1));
		ac.close(); 
	}
	
}

// MotdService
public class MotdServiceBean {
	
	protected List<String> motds = new ArrayList<String>();
	
	protected int defaultMotdIndex;
	
	public String getMotd(int motdIndex) {
		
		if (motdIndex < 0 || motdIndex >= motds.size()) {
			return motds.get(defaultMotdIndex);
		}
		
		return motds.get(motdIndex);
	}
	
	// init-method="initMotds" in application context
	protected void initMotds() {
		motds.addAll(Arrays.asList("Good Morning", "it's done", "Positive"));
	}
	
	public void setDefaultMotdIndex(int defaultMotdIndex) {
		this.defaultMotdIndex = defaultMotdIndex;
	}	
}
```
    
##  What is bean wiring? What about autowiring?
- Bean wiring is the process of combining beans with Spring container. The required beans are to be informed to the container and how the container should use dependency injection to tie them together, at the time of wiring the beans.
- Auto wiring: The Spring container can autowire relationships between collaborating beans without using ```<constructor-arg> ```and ```<property>``` elements, which helps cut down on the amount of XML configuration
- There are 5 auto-wiring mode: no, byName, byType, constructor, autodetect
```java
public class Department {
    private String deptName;
    public String getDeptName() {
        return deptName;
    }
    public void setDeptName(String deptName) {
        this.deptName = deptName;
    }
}
public class Employee {
    private String ename;
    private Department department;
    public String getEname() {
        return ename;
    }
    public void setEname(String ename) {
        this.ename = ename;
    }
    public Department getDepartment() {
        return department;
    }
    public void setDepartment(Department department) {
        this.department = department;
    }
    public void showEployeeDetails(){
        System.out.println("Employee Name : " + ename);
        System.out.println("Department : " + department.getDeptName());
    }
}
// Application Context
<beans ....>
	<bean id="department" class="guru.springframework.autowiringdemo.Department">
	<property name="deptName" value="Information Technology" />
</bean>
	<bean id="emp" class="guru.springframework.autowiringdemo.Employee" autowire="byName"></bean>
</beans>
```
    
8.  What are the different ways that Spring can wire beans?
- Using aplication context xml file
- Using Autowired Annotation on a field, a setter method or a constructor
- If it's on a property/field, spring look for it and inject the field when that class created
```java
import org.springframework.beans.factory.annotation.Autowired;
public class Employee {
    @Autowired
    private Department department;
    public int getEid() {
        return eid;
    }
    public void showEployeeDetails(){
        System.out.println("Department : " + department.getDeptName());
    }
}
```
    
##  What are the scopes of Spring beans? Which is default?
- Spring bean had 5 scopes: singleton, prototype, request, session, global-session
- Singleton is the default
```java
<!-- A bean definition with singleton scope -->
<bean id = "..." class = "..." scope = "singleton">
   <!-- collaborators and configuration for this bean go here -->
</bean>
```
10.  What is the concept of component scanning and how would you set it up?
    
11.  What are the benefits and limitations of Java configuration?
    
12.  What does the @Configuration and @Bean annotations do?
    
13.  What is @Value used for?
    
14.  What is Spring Expression Language? What can you reference using SpEL? What is the difference between $ and # in @value expressions?
    
<br>

# Spring MVC
## What is Spring MVC
- I is a request-driven, designed around a central Servlet that dispatches requests to controllers and offers other functionality
##  Explain the MVC architecture and how HTTP requests are processed in the architecture
- Spring MVC follows the Model-View-Controller design patterns
- It had a Front Controller which calles Servlet Dispatcher
- How http process: At first, a http request will be read by RequestDispatcher. Then, it'll passes the request to the corresponding controller based on url mapping. The controller performs the task and return model and view. Dispatcher servlet maps the view to coresponsing jsp or html using view resolver. The view renders the model and display it
## Step to create Spring MVC
- In web.xml, tell where is the application context and Dispatcher Servlet is and add ContextLoaderListener
- Dispatcher servlet can contain index.xml
- In application Context:
	- Enable reading Spring MVC annotation ```<mvc:annotation-driven/>```. Enable @trasaction ```<tx:annotation-driven/>```
	- Scan all the packeages that manage the classes
```java
<context:component-scan base-package="com.revature.service"/>
// ...
```
	- Declare dataSource beans to write JDBC credentials
```xml
	<bean name="dataSource"
		class="org.springframework.jdbc.datasource.DriverManagerDataSource">
		<property name="driverClassName"
			value="org.postgresql.Driver" /
		<property name="url"
			value="jdbc:postgresql://localhost:5432/postgres" />
		<property name="username" value="" />
		<property name="password" value="" />
	</bean>
```
	- Declare sessionFactory to work with Hibernate, wiring datasource bean into sessionFactory
```xml
<bean name="sessionFactory"
		class="org.springframework.orm.hibernate4.LocalSessionFactoryBean">
		<property name="dataSource" ref="dataSource" />

		<!-- Annotation Mapping -->
		<property name="packagesToScan" value="com.revature.model" />
		<property name="hibernateProperties">

			<props>
				<prop key="hibernate.dialect">org.hibernate.dialect.PostgreSQLDialect</prop>
				<prop key="show_sql">true</prop>
				<prop key="hibernate.hbm2ddl.auto">update</prop>
			
				<prop key="hibernate.default_schema">public</prop>
			</props>
		</property>
</bean>
```
    
##  What is the role of the DispatcherServlet? What about the ViewResolver?
- Dispatcher Servlet is the Front controller. Its job is to receive the request, send it to a HandlerMapping and pass the request to the right controller. The controller wil then build the model/view and send back to Dispatcher Servlet and it'll send the response to the client.

- Spring MVC provides the View Ressolver interface which maps view name to acual views
- Basically it takes the view name from the controler and prepare the view in the browser without use to hardcode the view location (ex: in class ABC controller, return "/WEB-INF/view/Cricket.jsp"). It'll take the view, add a prefix which is /WEB-INF/view and the suffix which is ".jsp" and add the view name in between
    
##  List some stereotype annotations. What are the differences between these?
- Some stereotype annotations are @Component, @Repository, @Service and @Controller
- Diferent:
	- @Component: Generic stereotype for any Spring-managed component. Should be used when our class doesn't fall into Controller, Service, or Dao
	- @Repository: indicates that this class provides a mechanism for CRUD operations of this particular object
	- @Service: stereotype for service layer
	- @Controller: stereotype for presentation layer (for view and controller in spring mvc). If you add the @Controller annotation to a class then you can use handler mapping annotation i.e. @RequestMapping

##  How would you declare which HTTP requests you like a controller to process?
- https://springframework.guru/spring-requestmapping-annotation/ (requestmapping multiple url, mapping a request param)
- @RequestMapping(method = RequestMethod.GET)
- Request mapping shortcut (Spring 4.3): @PostMapping, @DeleteMapping, @GetMapping
    
##  What is the difference between @RequestMapping and @GetMapping?
- @GetMapping acts as a shortcut for @RequestMapping(method = RequestMethod.GET)
    
##  How to declare the data format your controller expects from requests or will create in responses?
- To have data format expects form a request: ```@RequestMapping(value = "/cons", consumes = {"application/JSON", "application/XML"})```
- To have them create in a response: 
```java
@RequestMapping(value = "/prod", produces ={"application/JSON"})
 @ResponseBody
```
##  What annotation would you use to bypass the ViewResolver?
- @ResponseBody
    
##  How would you extract query and path parameters from a request URL in your controller?
- To extract a path parameter, we put a curry bracket between the @RequestMapping value, then in that method, we add @PathVariable annotaion, add the user keyword to its () and defines its datatype and name, then use that name to set or log that value
```java
@RequestMapping(value="/home/{user}", method=RequestMethod.GET)
publi String sayHello(@PathVariable("user") String user, Model model){
	model.addAttribute("userName", user);
	System.out.println("user")
	return "welcome";
}
```
- To get the request query, we use @RequestParam("query name") or @RequestParam without value element, follow by datatype and a name to store the value
- @RequestParam without value element only works if the request param and handler method parameter names are same ```localhost:8090/home/personId?personId=5```
 
```java
@RequestMapping(value = "/personId")              
  String getId(@RequestParam String personId){
    System.out.println("ID is "+personId);  
    return "Get ID from query string of URL without value element";  
  }
```
- With value
```java
@RestController
@RequestMapping("/home")
public class IndexController {
  @RequestMapping(value = "/name")
  String getName(@RequestParam(value = "person", required = false) String personName){
    return "Required element of request param";
  }
}
// require = false means if there's no query, just /home/name, it still accept
```
@RequestMapping(value="/home/{user}", method=RequestMethod.GET)
publi String sayHello(@PathVariable("user") String user, Model model){
	model.addAttribute("message", "Welcome from Spring")
}
``` 
23.  What concerns is the controller layer supposed to handle vs the service layer?
    
##  How would you specify HTTP status codes to return from your controller?
- Use ```return new ResponseEntity(HttpStatus.NOT_ACCEPTABLE); ``` with @ResponseBody to bypass the ViewResolver
    
25.  How do you handle exceptions thrown in your code from your controller? What happens if you don’t set up any exception handling?
    
##  How would you consume an external web service using Spring?
- Using a rest template which have getForObject, getForEntity, postForObject, postForLocation, put, delete headForHeaders, optionsForAllow method
```java
public class SpringRestClient {
 
 private static RestTemplate restTemplate = new RestTemplate();
 private static final String baseURL = "http://localhost:8080/restapi/";

 public static void main(String[] args) {
  //Read Account details for a given accountId = 1 using GET method of RestTemplate
  Account accountDetail = restTemplate.getForObject(baseURL+"account/1", Account.class);
  System.out.println("Account Detail for given AccountId : " +accountDetail); 
  
 }

}
```
    
##  What are the advantages of using RestTemplate?
    
<br>

# Spring AOP

28.  What is aspect-oriented programming�? Define an aspect.
    
29.  Give an example of a cross-cutting concern you could use AOP to address
    
30.  Define the following:
    

*  Join point
    
*  Pointcut
    
*  Advice
    

31.  What are the different types of advice? What is special about the @Around advice? How is the ProceedingJoinPoint used?
    
33.  Explain the pointcut expression syntax
    
34.  What visibility must Spring bean methods have to be proxied using Spring AOP?
        
<br>    

# Spring Data

34.  What is Spring ORM and Spring Data?
    
35.  What is the Template design pattern and what is the JDBC template?
    
36.  What does @Transactional do? What is the PlatformTransactionManager?
    
37.  What is a PersistenceContext?
    
38.  Explain how to integrate Spring and Hibernate using ContextualSession
    
39.  What interfaces are available in Spring Data JPA?
    
40.  What is the difference between JPARepository and CrudRepository?
    
41.  What is the naming conventions for methods in Spring Data repositories?
    
42.  How are Spring repositories implemented by Spring at runtime?
    
43.  What is @Query used for?
    
<br>

# Spring Boot

44.  How is Spring Boot different from legacy Spring applications? What does it mean that it is opinionated?
    
45.  What does “convention over configuration” mean?
    
46.  What annotation would you use for Spring Boot apps? What does it do behind the scenes?
    
47.  How does Boot autoconfiguration work?
    
48.  What is the advantage of having an embedded Tomcat server?
    
49.  What is the significance of the Spring Boot starter POM?
    
50.  What is the Spring Boot actuator? What information can it give you?
    
51.  What files would you use to configure Spring Boot applications?
    
52.  What is the benefit of using Spring Boot profiles?
