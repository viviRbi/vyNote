# Spring
## What is Spring?
- Spring an umbrella term for a family of frameworks which can be utilized to rapidly create loosely coupled Java applications (lossly coupled = low or weak coupling. When two or more hardware and software components are attached or linked together to provide two services that are not dependent on one another)
- Spring start out as an **inversion of control container** for Java(IoC Container) (- IoC, or DI is the D- Dependency Inversion in SOLID ) 
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
- Dependency injection is a design pattern which implements the IoC principle to invert the creation of dependent objects. It sharing one single object across the application

- **Types** the injector class injects the service (dependency) to the client (dependent) in 3 way:

	- Constructor Injection: In the constructor injection, the injector supplies the service (dependency) through the client class constructor.

	- Property Injection: In the property injection (aka the Setter Injection), the injector supplies the dependency through a public property of the client class.

	- Method Injection: the dependency provides an injector method that will inject the dependency into any client passed to it. Clients must implement an interface that exposes a setter method that accepts the dependency.
- **Spring injjection type** - 2 types:
	- Inject by Constructor
	- Inject by Setter method

    
##  What types of dependency injection does Spring support?
- Constructor base dependecy injection
- Setter base dependecy injection
    
##  What are some differences between BeanFactory and ApplicationContext? Which one eagerly instantiates your beans?
BeanFactory | ApplicationContext
------ | -------
Loads on demand (lazy loading) | Load on Startup (Eager loading)
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
    
##  What are the different ways that Spring can wire beans?
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
- Spring bean had 5 scopes: 
	- singleton: Spring IoC container define only 1 instance  of the object
	- prototype: return different instance everytime request comes from IoC Container 
- Create though Http call. Only available in web aware context:
	- request: new instance for every http request and destroy when the call ends 
	- session: return new instance for every session
	- global-session: the instance shared accross our web app, every call receive the same bean instance. It is similar to singleton
- Singleton is the default
```java
<!-- A bean definition with singleton scope -->
<bean id = "..." class = "..." scope = "singleton">
   <!-- collaborators and configuration for this bean go here -->
</bean>
```
##  What is the concept of component scanning and how would you set it up?
- Fundamental functionality of a Spring Framework is injection. To know where the bean is and inject it, we need Component Scan.
- whenever Spring container the read the XML configuration, it will scan all the package that you defined in <context:component-scan base-package="org.websparrow.beans" /> and automatically creates the objects of all beans where you annotated by @Component, or its special case (@Service, @Repository which added with PersistenceExceptionTranslationPostProcessor in application context).
- Either use @Component Scan or XML Configuration
```
<context:component-scan base-package="com.abc.p1.repository"/>
@ComponentScan(basePackages = {"com.abc.p1.service"})
```
 - As soon as we add @SpringBootApplication, it automatically does the component scan in that class package
 
##  What are the benefits and limitations of Java configuration?
- Java configuration is the @Configuration that indicate that class can be used by the Spring IoC Container as a source of bean definition
- Benefits: using Java rather than XML, simplier to search, easier to understand, compiler time checking (able to fix typo immediately), easier to manage
- Limitations: it's long
    
##  What does the @Configuration and @Bean annotations do?
- @Configuration that indicate that class can be used by the Spring IoC Container as a source of bean definition
- @Bean is a method-level annotation and a direct analog of the XML <bean/> element. The annotation supports most of the attributes offered by <bean/>, such as: init-method, destroy-method, autowiring, lazy-init, dependency-check, depends-on and scope.
```java
@Configuration
public class AppConfig {
    @Bean
    public Foo foo() {
        return new Foo(bar());
    }

    @Bean
    public Bar bar() {
        return new Bar();
    }
}
```

##  What is @Value used for?
- Spring @Value annotation is used to assign default values to variables and method arguments. We can read spring environment variables as well as system variables using @Value annotation.
```
@Value("string value")
private String stringValue;

@Value("${rate}")
String rate;
```
    
##  What is Spring Expression Language? What can you reference using SpEL? What is the difference between $ and # in @value expressions?
- Spring Expression Language is a powerful expression language that supports querying dynamically at runtime. It can be use with XML or annotation base Spring config. It had servaral operators: boolean and relational operators, relational operators, ternary operator, conditiona loperator, regex operator, etc. We can also use it to inject value into Map and List
- We can reference to other beans, properties, static content in .properties files
- # is use for Spring Expresion language
- $ is use to map with a value in application.properties
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
		<property name="url" 		value="jdbc:postgresql://localhost:5432/postgres" />
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
- Some stereotype annotations are @Component, @Repository, @Service and @Controller. Component scanner will look and scan/ mangae the life cycle of the classes with these annotation. So we don't have to create a new instance of them evrytime we use
- Diferent:
	- @Component: Generic stereotype for any Spring-managed component. Should be used when our class doesn't fall into Controller, Service, or Dao. It shouldn't be use for static class like Model
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
- To extract a path parameter, we put a curry bracket between the @RequestMapping value, then in that method, we add **@PathVariable** annotaion, add the user keyword to its () and defines its datatype and name, then use that name to set or log that value
```java
@RequestMapping(value="/home/{user}", method=RequestMethod.GET)
public String sayHello(@PathVariable("user") String user, Model model){
	model.addAttribute("userName", user);
	System.out.println("user")
	return "welcome";
}
@GetMapping("/account/{accountId}")
public Account get (@PathVariable Long accountId){
  return accountService.get(accountId);
}
```
- To get the request query, we use** @RequestParam**("query name") or @RequestParam without value element, follow by datatype and a name to store the value
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
    
25.  How do you handle exceptions thrown in your code from your controller? What happens if you dont set up any exception handling?
    
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
    
## What are the advantages of using RestTemplate? 
- Rest template provides higher level methods that correspond to each of the six main HTTP methods. We can easilly make a request and receive a reponse from other Restful API

# Spring AOP

##  What is aspect-oriented programming? Define an aspect.
- **Aspect Oriented Programming** is a programming paradigm that used for **separating crosscutting concerns** (like logging) into **single units** called **aspects**
- The key unit of modularity in OOP is the class, whereas in AOP the unit of modularity is the aspect.
- Aspects can be a normal class configured through Spring XML configuration or @Aspect annotation.
- An aspect is a class that implements enterprise application concerns that cut across multiple classes, such as transaction management
 ```java
 @Before("execution(public void com.journaldev.spring.model..set*(*))")
	public void loggingAdvice(JoinPoint joinPoint){
		System.out.println("Before running loggingAdvice on method="+joinPoint.toString());
 ```
    
##  Give an example of a cross-cutting concern you could use AOP to address. 
- We need to log before and after a method run
- Security
- Validation
    
##  Define the following:
    

-  Join point: a point in a program like exception handling, changing obj variable. In Spring, join point is always the execution of method. At the join point, an aspect is injected.
    
-  Pointcut: an expression language that matched a join point
```java
@Pointcut("execution(public **(..))") // applied on all public method
@Pointcut("execution(* Operation.*(..))") // applied on all the methods of Operation class
//------------------------------------
@Aspect
public class EmployeeAOP{
@Pointcut("execution(public Employee.set*(..))")// applied on all public setter method of employee
public employeePointCut(){} // method of poincut annotation

@Before("employeePointCut()")
public void BeforeEmployeeSetter (Jointpoint jp){
	System.out.println("before each setter methods of Employee class---")
	logger.log("Class name is " + jp.getSignature())
}
}

// xml AOP
<aop:config>
    <aop:pointcut id="anyDaoMethod" 
      expression="@target(org.springframework.stereotype.Repository)"/>
</aop:config>
 @Pointcut("@annotation(org.springframework.web.bind.annotation.RequestMapping)")
public void requestMapping() {}

@Pointcut("within(blah.blah.controller.*) || within(blah.blah.aspect.*)")
public void myController() {}

@Around("requestMapping() && myController()")
public Object logAround(ProceedingJoinPoint joinPoint) throws Throwable {
      ...............
   } 
```
    
-  Advice: A method that execute when a certain join point meet a matching pointcut. Type of advice: Before Advice, After Advice, After Retuning Advice, Around Advice
    

##  What are the different types of advice? What is special about the @Around advice? How is the ProceedingJoinPoint used?
- An around advice is a special advice that can control when and if a method (or other join point) is executed. This is true for around advices only, so they require an argument of type ProceedingJoinPoint
- It used by passing a ProceedingJoinPoint to the method under @Around(""execution(* com.j.c.model.Emp.getName())"") and use proceedingJoinPoint.proceed() to get the valua (name of the employee)
    
##  Explain the pointcut expression syntax
- Join point type, class location start at com., class method
    
34.  What visibility must Spring bean methods have to be proxied using Spring AOP?
        
<br>    

# Spring Data

##  What is Spring ORM and Spring Data?
- Spring ORM is a Spring Application with a ORM / JPA vendor dependency like Hibernate
- Spring data create common Abstraction to store and retrieve data. It is a specification for Object Relational Mapping and it reduce a lot of duplicate code. We implement it by extends CrudRepository<Model, data-type-of-Id>
- The methods we get after extends CrudRepository are: save(), findById(id), findBy...(a class property like title, name), existsById(id), findAll(), findAll(Sort sorting), findAll(Pageable pagination) deleteById(id), count() and other
    
##  What is the Template design pattern and what is the JDBC template?
- Template design pattern means we define a skeleton of operations and leaves the details to be implemented by the child classes
- JDBC template: it is a powerful mechanism to connect to the database and execute SQL queries. It internally use JDBC API but help us reduce a lot of code
```xml
<bean id="eDao" class="com.abc.dao.EDaoImp">
	<property name="jdbcTemplate" ref="jdbcTemplate"></property>
</bean>
```
or
```java
pulic class EDaoImp implements EDao{
	@Autowired
	private JdbcTemplate jdbcTemplate;
}
```
both have
```xml
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
	<constructor-arg name="dataSource" ref="dataSource"></constructor-arg>
</bean>
```
    
## What does @Transactional do? What is the PlatformTransactionManager?
- **@Transaction annotation** defines the scope of a database transaction. It happens inside the scope of a PersistentContext
- **PlatformTransactionManager** is an interface that gives abstraction to Spring transaction management. Some of its implementations are DataSourceTransactionManager, HibernateTransactionManager, JpaTrasactionManager, etc
```xml
<bean id="txManager" class=
"org.springframework.orm.hibernate5.HibernateTransactionManager">
  <property name="sessionFactory" ref="sessionFactory"/>
</bean>

<!-- https://www.netjstech.com/2018/08/transaction-management-in-spring.html -->
```
    
##  What is a PersistenceContext?
- The persistence context is the first-level cache where all the entities are fetched from the database or saved to the database. It sits between our application and persistent storage
- Persistence context keeps track of any changes made into a managed entity. If anything changes during a transaction, then the entity is marked as dirty. When the transaction completes, these changes are flushed into persistent storage.
- The EntityManager is the interface that lets us interact with the persistence context
```java
@Component
public class TransctionPersistenceContextUserService {

    @PersistenceContext
    private EntityManager entityManager;
    
    @Transactional
    public User insertWithTransaction(User user) {
        entityManager.persist(user);
        return user;
    }
}
```
    
##  Explain how to integrate Spring and Hibernate using ContextualSession
- sessionFactory.getCurrentSession()
    
39.  What interfaces are available in Spring Data JPA?
    
40.  What is the difference between JPARepository and CrudRepository?
    
##  What is the naming conventions for methods in Spring Data repositories?
- Lowercase on the 1 word connect to other word by underscore
    
42.  How are Spring repositories implemented by Spring at runtime?
    
##  What is @Query used for?
- @Query is a Spring Data JPA annotation. We can either use JPQL or native SQL (by set nativeQuery = true)
- @Query annotation annotate the method. The result of the query will be return by the method under it
```
@Query(
  value = "SELECT * FROM USERS u WHERE u.status = 1", 
  nativeQuery = true)
Collection<User> findAllActiveUsersNative();
```
    
<br>

# Spring Boot
## Boot?
- Come from Bootstrap, means self-starting

##  How is Spring Boot different from legacy Spring applications? What does it mean that it is opinionated?
- **Spring Boot** is an extension of the Spring framework, which eliminates the boilerplate configurations required for setting up a Spring application
- Spring Boot takes an opinionated view of the Spring platform, which paves the way for a faster and more efficient development ecosystem
- **Unlike Spring**, Spring Boot requires only 1 dependency to get a web application running. That is the spring-boot-starter-web from org.springframework.boot
- **Spring Boot opinionate** because it follows the opinionated default configuration that reduces developer efforts to configure the application
    
##  What does convention over configuration mean?
- Convention over configuration is a software design paradigm which is used by many modern software frameworks that attempts to decrease the number of decisions that a developer can made without necessarily losing flexibility
- It takes a lot of burden away from developers
    
##  What annotation would you use for Spring Boot apps? What does it do behind the scenes?
- For all Spring Core Spring MVC Spring Boot annotation: https://www.javatpoint.com/spring-boot-annotations
- **@SpringBootApplication**: It is the combination of 3 annotation: @EnableAutoConfiguration, @ComponentScan and @Configuration
- @Configuration: not specific to Spring Boot. It tags the class a the source bean
- @EnableAutoConfiguration: a Spring Boot Annotation, enable the application to add the beans using classpath definitions. You can tell Spring to disable certain auto-configuration classes.  (i.e.  ```@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})``` )
@ComponentScan: This annotation tells the spring to look for oter components, configurations and services in the specified path
- When using Spring MVC, we have to configure these ourself: component scan, dispatcher servlet, view resolver, web jars, others
    
##  How does Boot autoconfiguration work?
- Spring Boot looks at Frameworks available on classpath, existing configuration for the application. Base on these, Spring Boot provide basic configuration needed to configure the aplication with these frameworks which called Auto Configuration
- Ex: As soon as we added SpringBoot Starter Web as a dependency, Spring Boot Autoconfiguration sees that Spring MVC is on the classpath. It autoconfigures dispatcherServlet, a default error page and webjars
- If we add Spring Boot Data JPA Starter, the auto configuration will auto configure a datasource and an Entity Manager
    
##  What is the advantage of having an embedded Tomcat server?
- When embebed Tomavat into your application, you are responsible for strating and stopping Tomcat. It will look like a regular jav program. You just launch it and that's it. It is useful for rapid deployment and testing 
   
##  What is the significance of the Spring Boot starter POM?
- Spring boot starter pom is based on the transisive nature of POM dependency
- The POM we have access to is the child POM. Its parent was declared in the parent tag with artifact id spring-boot-starter-parent. And its parent is spring-boot-dependency
- The child POM inherits all starter dependency from that spring-boot-dependencies along with the corect version
- If we want to exclude any of the starter dependency, inside spring-boot-starter-web exclusions tag, we can have an exclude tag and the group id of the file we want to exclude
```java
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
   <exclusions>
      <exclusion>
       <groupId>com.fasterxml.jackson.core</groupId>
     </exclusion>
  </exclusions>
</dependency>
```
- We can also add the same dependency with different version ad it'll override the spring-boot-dependences with the same artifactId
    
##  What is the Spring Boot actuator? What information can it give you?
- Spring Boot Actuator is a sub-project of Spring Boot
- It provides secured endpoints for monitoring and managing our Spring Boot application.
- Information it gives are: /metrics(memory used, memory tree, threads, classes, etc), /env (list of env var),/health,/info,trace
- To use it, in application.properties, disable the security features of the actuator then invoke the accotor url
```
management.security.enabled=false  
http://localhost:8080/actuator
http://localhost:8080/actuator/health
```
##  What files would you use to configure Spring Boot applications?
- application.properties inside src/main/resources
```
logging.level.some.package.path=DEBUG
logging.file=\path_to\logfile.log
server.port = 9080
```
    
##  What is the benefit of using Spring Boot profiles?
- Spring Boot profile help us ansered the qus: How do you have different configuration for different environments
```
application-dev.properties
application-qa.properties
application-stage.properties
application-prod.properties
application.properties
```
To set the environment we are in, in application.properties, add spring.profiles.active=prod. In VM Arguments, -Dspring.profiles.active=qa
