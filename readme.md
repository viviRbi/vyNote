Java Full Stack Review Questions
Java
Basics
### Java is pass by value. A variable that holds an object will be stored in the stack, with a pointer to that object in the heap
## What is Java? / Explain some features of Java
Java:
- Java is a high-level, compiled, strongly typed object-oriented programming (OOP) language.

- High-level: Code that is easily human readable, as opposed to binary or assembly.
- Hybrid between compiled and interpreted language: Human-readable code is compiled, or transformed, into a form more optimized for computers to read
- For example, C++ code is compiled into binary
- Java code on the other hand is compiled into Java byte-code, which the Java Virtual Machine (JVM) will then interpret this byte-code and essentially run the program.
- Strongly-typed: variables declared of a certain type can only have values assigned to it of that same type

- Features:
- Java is Platform Independent. WORA. It is also a compiled and interpreted language: 
	- Unlike C which compile to binary and can only excute code for a particular machine, 
	- Java convert code into Java Bytecode and sent to Java Virtual mechine which resides in the RAM of any operating system. JMV recognizes its platform and convert that bytecode into that platform native machine code 
- Java comes up with garbage collected by default:
	- In C and C++, programmer is responsible for both the creation and destruction of objects. If programmer forget, the application suffer from memory leaks. Method like free() in C and delete() in C++ will perform garbage collector
	- In Java, Gabarge collector happens automatically. Over the life time of a Java application, some objects will no longer needed, . At that time the heap memory consist of 2 object types: Live & Dead. The Garbage Collector find these unused obj and free up the memory
- Java has the 2nd fastest compiler (JIT - Just in Time)
- Java support multithreaded (parallel programming) which makes the program runs faster which is more preferable in the market. 
	- By default all Java thread is single threaded. To enable multi-thread, we have 2 ways:
		- Extends java.lang.Thread class
		- Implementing java.lang.Runnable interface (prefer)

```java
 public static void main(String[] args) {
  // TODO Auto-generated method stub
  GuruThread3 threadguru1 = new GuruThread3("guru1");
  threadguru1.start();
  GuruThread3 threadguru2 = new GuruThread3("guru2");
  threadguru2.start();
 }
}
class GuruThread2 implements Runnable {..}

// 2 thread runs at the same time. If 1 thread slowdown, other will take place
```

## What is JRE / JDK / JVM?
- JVM (Java Virtual Machine): Enables a computer to run Java programs. It essentially behaves like an interpreter or just-in-time compiler (JIT) which takes bytecode and translate it to something the computer can understand.
	- We have different implementations of the JVM for different operating systems: Linux, Windows, Mac, etc..
	- The important thing to take away from this is that this allows you to run the same bytecode on any operating system (platform independence)
- JRE (Java runtime environment): Contains the JVM and core libraries that our code may be calling and using. If the only thing we need to do is run Java programs, all we need to install is the JRE.
- JDK (Java development kit): contains the JRE (which of course contains the JVM) + developer tools like the compiler (javac), debugger, documentation tools (javadoc), and other command-line utilities

## What is the difference between an object and a class?
- Class is a blue print of an object
- Object is an instance of a class where it contains and a real world entity that exists like car1, person1.

## What is the root class from which every class extends?
- The Object class

## What are the primitive data types in Java?
- Boolean, Integer, Byte, Short, Double, Float, Char
- By default: 0 for int, 0 for byte, 0.0 for float

## Where are Strings stored?
- Strings are stored on the Heap area in a separate memory location known as String Constant pool
- When we create another String obj as ```String str2 = "Hello"```,JVM look at the string pool, if it's already exist, JVM gives its variable which stored on the stack the same address 

## Explain stack vs heap
- Stack and Heap are 2 ways Java allocated their memory
- If Java variable and method were to declare the same time in an Java app, it'll cost lots of RAM that the application maybe bloated (too much).
- That's why Java Virtual Machine divide memory between Stack Memory and Heap Space
- **Heap space**: Create by the JVM when it starts and the memory used as long as the app running.
	- When an obj created, it is always created in the Heap. Java Runtime use it to allocate memory to bject. It had a global access to be reference everywhere in the app
	- The main objective of a Garbage collector is to free the heap space by clear un-used object
- **Stack Memory**: Only use for the method that are currently running. When the method return, everything discard. This is the temporary memory where variables are stored when their methods are invokes. After the method finished, the memory contain those value is cleared.
	 - If a new instance of an object is created. The pointer to that object in the heap stored in the stack

## Are variable references stored on the stack or heap? What about the objects they refer to?
- If a new instance of an object is created. The pointer to that object in the heap stored in the stack

## What is a stack frame? When are these created?
- It is a frame of data of a function that haven't return that was pushed to the stack
- When a function called, a stack frame created. And then all the data put onto the stack frame. When the function return, the current stack frame deleted from the stack

## What are annotations?
- Provide the extra information of a method source code
- Ex: @override

## What is a POJO vs a bean?
- Plain old Java Object: ordinary Java obj 
- The only difference between both the classes is Java make java beans objects serialized so that the state of a bean class could be preserved in case required. So due to this a Java Bean class must either implements Serializable or Externalizable interface.

## Can you force garbage collection in Java? When is an object eligible for GC?
- System.gc() Runtime.gc() but should be avoid since there is no way to predict when garbage collectior will occur at runtime (non-deterministic)
- Force garbage collector best practice is to set flags on the JVM, a flag can adjust when a garbage collector will be use like set the initial and maximum size of the heap, the size of the heap sections (Young genration, old generation - younf one that lives long enough) (set flag using the CMD -command prompt)

## Why are strings immutable in java? How would you make your own objects immutable?
- Because String class was made final. 
- Performent: String pool is possible only because String is immutatable in Java. It saves a lot of heap space because different String variable can refer to the same String variable in the pool.
- Security: It will impact security for ex: dabase username and password are pass as String. If it were mutable, hacker could change the reference to cause security issues
- Multithread: String are safe for multithread because it's immutable
- To made our own object immutable, we declared our class as final

## What is the difference between String, StringBuilder, and StringBuffer?
String | String Buffer | String Buider
----- | ----- | ------
a final class(thread safe)| synchronized(thread safe) | non-synchonized (not thread-safe)
immutable | mutable | mutable
use new keyword or = sign to create | new keyword to create an obj only| new keyword to create an obj only
-- | less efficent than String Builder | More efficent than String Buffer, faster

## What are the different variable scopes in Java?
1. Static Scope
    - Static scope refers to a variable that belongs to the class itself
2. Instance Scope
    - Instance scope referes to a variable that belongs to a particular instance/object
    - Instance methods can access static fields/methods! (directly)
3. Method Scope
    - Refers to variables defined within a method
    - Once the method finishes executing (when the method returns), then the variable will no longer be in scope
4. Block Scope
    - Refers to a block of code within a method
    - For example, variables declared inside an if statement code block, for loop block, while loop block, etc.


## What are the access modifiers in Java? Explain them.
- 

15. What are the non-access modifiers in Java?

16. What is the difference between static and final variables?

## What are the default values for all data types in Java?
- Boolean

## What is a wrapper class? List them.
- Wrapper class 

## What is autoboxing / unboxing?
- Coeversion between primitives and object

## Is Java pass-by-value or pass-by-reference?
- Java pass by value

## What makes a class immutable?
- Makes its field final
- 

## If two objects are equal, do they have the same hashcode? If not equal?
- If 2 objects are equal, they have the same hashed. 
- If not, they can or cannot

## What data types are supported in switch statements?
- Int, Short, Char, Boolean and String

## List all non-access modifiers

## How to pass multiple values with a single parameter into a method? 
- String[], int[], datatype + square bracket

## What is a static block?
- Static block is used for initializing the static variables
- We can also call static methods inside a static block. It is also the only way to call static methods at time of class creation. They are called only once. Instanciate 2 or 3 more new objects won't call them again

## What are static imports? 
- Import static method and filed without instanciate the class

## What methods are available in the Object class?
- toSting(), equal(), hashcode()

## What is the difference between == and .equals()?
- == used to check the value of the variable
- .equals9) check value and data type together

## What is an enhanced for loop and what is a forEach loop?
- for loop use index
- with forEach, it loop through each value without the use of index

## What are the 3 usages of super keyword?
- Use to get parent constructor
- Use to get parent value
- super can be use to assign value to the parent

## What is the first line of any constructor?
- super()

## How would you perform constructor chaining?
- Constructor chaining is the process of calling one constructor from another constructor
	
34. What happens if you dont define a constructor for a class? Can you still instantiate it?

# OOP
## What are the 4 pillars of OOP? Explain each and give examples of you implement them
in Java code

## Explain the principles of the SOLID acronym

## What is the difference between an abstract class and an interface?

## Can abstract methods have concrete methods? Can concrete (non-abstract) classes
have abstract methods?

5. Can static methods access instance variables? Can non-static methods access static
variables?

6. What are the implicit modifiers for interface variables? Methods?

7. What is the difference between method overloading and overriding? What are the rules
for changing the method signature of overloaded methods?

8. Can you overload / override a main method? static method? a private method? a default method? a protected method?

9. What are covariant return types? What rules apply to return types for overridden
methods?

10. When do you use extends or implements keywords?

11. What are enumerations (enums)?

12. What are the implicit modifiers for interface variables / methods?


# Collections / Generics
## Look at if it's a class or an interface first, then look at which interface it implements from
## What are collections in Java?
- All collections are part of java.util package
- A wide variable type of collection, each have their own specialize
- All collections are dynamic, resizable, accepts only object, Iterable, the root interface of all collection (except Map) is Collection

## Some method of the Collection interface
- contains, containsAll (return true if contain all member of other collection)
- remove, removeAll (remove all elements contain on other collection)
- retainAll (remove all elements contain NOT on other collection)
- size(), clear(), isEmpty(), add(), addAll()


## What are the interfaces in the Collections API?
- List, Map, Set, Queue, etc

## What is the difference between a Set and a List?
Set | List
----- | -----
lood like dynamic unique array | exactly like array but dynamic
had no position | maintains order of insertion
not allow duplication. Check using equals & hashedCode method | allow duplications
allow 1 null | not allow any null
Implemented by HashedSet, LinkedHashedSet, TreeSet
Set implemented by HashSet, LinkedHashSet, TreeSet | List implemented in ArrayList, LinkedList, Vector, Stack classes
Set is unindexed (no position of element) | List is indexed. It had position for all the value
Memory by default 16 allocations and load factor is .75  | Memory decide by its implemented class


## What is the difference between an Array and an ArrayList?
Array | ArrayList
basic functionality of Java | Part of the collection framework
stored any | Stored referent type
not dynamic | dynamic
access using [] with index position | use its method to access (add, get)
Default capacity of an array is length we give it when it created and it's fixed | the default capability of an arrayList is 10. Once filled, new capacity =(current capacity*3)/2+ 1
Use for loop to iterate | use an Iterator to interate over an array

## What is the difference between ArrayList and Vector?
Both implemet list interface and and provide the same functionalities. However there are some differences:
ArrayList | Vector
------ | ------
Not thread safe (inconsitent result in multithreading, an use ```Collections.synchronizedList(new ArrayList(arrayList1));```  to archive threadsafe) | Thread safe (in Multithreading, when work on the same data, a thread will prevent another thread perform on that data -> thread safe)
by default 10 memory location. Once filled, new capacity =(current capacity*3)/2+1 | by default 10 memory locations once it is filled it will give 10 more
contiguous (meaning data stored with no discontinuities and no padding between them. If memory is so little that only smaller pieces are free, this memory allocation cannot be sastisfy. Faster execution) | not contiguous (allocates separate blocks of memory, fit into small free sapce, reduce waste of memory, slower in excecution)
newer | older

## What is the difference between TreeSet and HashSet?
TreeSet | HashedSet
------ | ------
implements Set, SortedSet, NavigableSet | implements Set

maintain data in sorted order. Compare them by implement Comparable interface inside the object class and use compareTo method. If it's just Integer or String, asc by default. It had decendingSet and decendingIterator method to reverse the sort | un-order

no null allow (since it use a Comparator, If something compare to null, a NullPointException will be throw) | allow one null (since hashedSet use hashedMap internally and null value added as a key with a dummy empty value, hashedMap check for null key and doesn't hashed the null key)
not thread safe | not thread safe
slower | faster
internally use TreeMap to stored alement. | internally use HashMap to store element. It instatiate HashMap in the constructor, pass it to a variable name map. When we use hashSet.add("123"), internally, it call map.("123",with a dummy value call PRESENT) and then added to the HashMap instance. The dummy PRESENT is just a ```public static final Object PRESENT = new Object();```


## What is the difference between HashTable and HashMap?
HashMap and HashTable both implement Map. They stored key/value pairs in a hashTable. When use, we specify a key and value object. The key is then hashed and that hash code then used as index of the value
HashTable | HashMap
----- | ------
Thread safe, synchronized | Not thread safe, not synchronized
Doesn't allow null key or value (since the key obj had to implement hashcode method and equals, and if the value null then the put method'll throw NullPointerException)| allow one null key and multiple null value
old | advance version of HashTable
doesn't maintain order of insertion | doesn't maintain order of insertion but have a subclass HashLinkedList which is ordered

``` Everthing named Listed is either have index or mantain order. List interface had indexes. Other mantains value```
## LinkedHashMap<K,V> class
- Its child of HashMap, so it gets all the props of Map and HashMap.
- Only difference is it maintains the order of insertion.

## LinkedHashSet<E> class
- It is a subclass of HashSet
- The only difference is it uses DoublyLinkedList internally to maintains the order of insertion.

## LinkedList<E> class
- LinkedList implements List,Queue and Dequeue.
- It isnt thread safe class.
- It allocates only one memory at a time. When new element comes in it will create one more.
- Memory is not contiguous.
- Insertion and Deletion is much faster here than other classes. We can use Deque (Double End Queue)(implements from Queue Interface) to add.., get.., removeFirst and Last method

## Stack class
- Stack class extends from Vector (Vector implements List interface)
- It provide pop push peek (at the top item) and a method to test if the stack is empty, and a method to search to see how an item for from the top 

## Are Maps in the Collections API? What makes Map different from other interfaces?
- Map is a part of collections but not under Collection API since its Interface doesn't extends from Collection Interface
- It comes with a key value pairs
- It is unindexed and unordered
- Map implemted in HashMap, LinkedHashMap, TreeMap and HashTable classes

## List several ways to iterate over a Collection. How would you iterate over a Map?
- Enhance for loop (```for (datatype variable : collection_used)```)
- Iterator ```for (Iterator variable = collection.iterator(); variable.hasNext();)```
- Simple for loop
- ForEach: ```colections.forEach(datatype name -> System.out.println(name))```

## What is the purpose of the Iterable interface? What about Iterator?
- Able to use .forEach(..=>..) and .interator()
- Iterator is an Interface used to stored a collection that call the interator method. Some of its method are hasNext(), next(), remove()

## What is the difference between the Comparable and Comparator interfaces?
- Java provide 2 interfaces to sort objects using data members of the class: Camparable and Comparator
- Comparable implemented by a class. It had a compareTo(Obj obj2) method. Used when there is only 1 way to sort the object
- Comparator doesn't afftect the original class. It is compare() method. Used when you want to sort the objects in multiple ways
```java
class Sortbyroll implements Comparator<Student> {
    // Used for sorting in ascending order of
    // roll number
    public int compare(Student a, Student b)
    {
        return a.rollno - b.rollno;
    }
}
```

## What are generics? What is the diamond operator (<>)? 
- Generics allow the author of a class to use type parameters, which are symbols that can be substituted for any concrete type. Ex: Map<K,V>, List <T>. Or we can create our own Generic type which is Triple <K, V, I>
- The diamon operature is where you declare the datatype of the type parameter 

## Create and instantiate a generic class. Create and use a generic method.
```java
public class Pair<T,S>{
	private final T firstVar;
	private final S secondVar;

	public printValue{
		System.out.println("First value is "+ firstVar.toString() + 
		" Second value is " + secondVar.toString());
	}
}

Pair<String, Integer> pair1 = new Pair<>("a",1)
pair1.printValue()

Pair<Person, Place> pair2 = new Pair<>(new Person("a"), new Place("River"))
pair2.printValue()
```


# Threads
## What is multi-threading?
- Multi threading means there will be 2 to more task running at the same time. It makes our app faster and smarter. Faster is always smore preferable in the market. When in a multithread, we cannot identify which thread comming first and last
## In what ways can you create a thread?
There are 2 ways of create a thread in Java: 
- Extending java.lang.Thread class (which already implement Runnable interface)
- Implement java.lang.Runnable
## List the methods in the Thread class and Runnable interface
- Runnable interface: run
- Thread class: getName (name of thread), start, run, sleep, yield, join, isAlive
## Explain the lifecycle of a thread
- A thread, acording to Sun, have 4 states: new, runable, non-runable, terminated
## What is deadlock?
## What is the synchronized keyword?

## Compile time and Runtime 
- compile time is a phase wherein the java compiler converts the java program into java bytecode
- the java compiler can't compile the code, often because of syntax errors


# IO / Serialization
## What is serialize in Java
When we serialize an obj in Java, we convert the data into byte streams that then later convert back into the copy of the original data

## How do you serialize / deserialize an object in Java?
- To serialize an obj in Java, we implement Serializable interface.
- JVM skips transient variables during the serialization process. That means the value of the age variable is not stored when the object is being serialized.
- Create file output stream, object output stream and use its write object methode then close all stream
```java
Student st = new Student("ABC","HighSchool");

FileOutputStream fileOutStr =  new FileOutputStream("student.ser");	
	 
//Create object output stream and write object
ObjectOutputStream objOutStr = new ObjectOutputStream(fileOutStr);
objOutStr.writeObject(st);

//Close all streams
objOutStr.close();
fileOutStr.close();
```

- To deserialize, use File Input Stream, Object input stream, and readObject() method of Object input stream then close all the stream

## What is a Marker interface? What does Serializable interface do?
- Marker interface is an interface with nothing inside. Example of it is the Serializable interface, Clonnable interface, Remote interface
- Ex: Serializable interface. It is used to mark that an object is eligiable for saving its state inside a file.

## What are transient variables?
- JVM skips transient variables during the serialization process. That means the value of the trainsient variable is not stored when the object is being serialized.

## Difference between FileReader and BufferedReader?
File Reader and BufferedReader ar eused to read data from a given character stream
BufferedReader | FileReader
---- | ----
Read characters from any input | Can be used only for reading files
Use Buffere internally to read | Directly read from hard drive
Faster | Slower
More efficient | Less efficient
Can read a single character or a line at a time | Can only read one character at a time, cannot read line

## Explain the try-with-resources syntax
- try-with-resouces will close the resource immediately after use
- Its syntax is
```java
try (resource declaration){

} catch (ExceptionType err){}

String line;

try(BufferedReader br = new BufferedReader(new FileReader("test.txt"))) {
      while ((line = br.readLine()) != null) {
        System.out.println("Line =>"+line);
      }
} catch (IOException e) {
      System.out.println("IOException in try block =>" + e.getMessage());
    }
```

## List some methods in the Scanner class
- nextInt(), nextLine(), nextLong(), boolean hasNext(), close() 


# Exceptions
## What is the difference between final, .finalize(), and finally?
- final : cannot change a variable value anymore. Compile time error. It is a keyword
- finally is a block of code that goes together with the try block. It'll executed despite of exception is catch or not. It is a block
- Finalize is used to perform clean up processing just before object is garbage collected. It is also use to release resources used by objects before they're removed from the memory. The time hen finalizer called are out of our control. It is a method
- If a finalizer throws an exception, the finalization process stops, leaving the object in a corrupted state without any notification
- Finalizer had ugly side effects at runtime. Deprecate since Java 9, will soon be remove

## Explain throw vs throws vs Throwable
- throws used to throw multiple exceptions at the method level to the calling method. It is used to force programmer handle it
- throw used to create the exception obj of our own to throw our own customised exception with our customised message

## Do you need a catch block? Can you have more than 1? Is there an order to follow?
- If we have a try block and didn't want to have a finally block, there must be a catch block
- Able to catch multiple block
- The order of a catch block is whatever matches first, gets executed 

## Compiler vs Runtime
- Compile time is a phase wherein the java compiler converts the java program into java bytecode. In other words java source code get's converted in to .class file
- In runtime, the java virtual machine loads the .class file in memory and executes that to generate the output

## Compiler error an runtime error
- Compile time error - the java compiler can't compile the code, often because of syntax errors
- the code did compile, can be executed but crashes at some point, like you have a division by zero

## What is base class of all exceptions? What interface do they all implement?
- Throwable is the base class of all exceptions (Exception, Error class extends from it) (RuntimeException and OtherException extends from it)
- They all implements Serializable interface (so that we can serialize the exception object and save it into a file?)

## List some checked and unchecked exceptions?
- All the exceptions occur at runtime but checked exceptions are detected by the compiler at compile time so it becomes mandatory to handle them
- Checked exception (java.lang.Exception) forces programmer to handle it. Until it is handled, the compiler won't allow to run. Some of the Checked exceptions are: FileNotFoundException, SQLException, ClassNotFoundException, FileNotFoundException, et
- Unchecked exceptions are part of RuntimeException 
## Error
- Error is irrecoverable e.g. OutOfMemoryError, VirtualMachineError, AssertionError
- Programmer cannot do anything about it

## Multi-catch block - can you catch more than one exception in a single catch block?
- Yes, from Java 7 to newer, we can by using or | symbol



# Reflections API
## What is Reflection API?
- Java Reflection is a process of examining or modifying the run time behavior of a class at run time.
- It is a very powerful concept
- It had little use in normal programming but it's the backbone for most Java frameworks. Some of the framework uses reflection are Junit, Spring, Tomcat, Eclipse, Hibernate
- We should not use it in normal programming when we already had access to the classes and interfaces
- java.lang.Class is the entry point of all the reflection operators
```java
Test abc = new Test();
  
Class cls = abc.getClass();
System.out.println(
	cls.getName();
	cls.getConstructor().getName();
	
);
Method[] method = cls.getMethods();
```
	
## What can you do with the Reflections API that you cant do in normal code?
- Check if a class had a certain method. IDE like Eclipse able to giving us a list of methods in a class, auto complete the field because of the reflection API
- Dependency injection in Java depend heavily on reflection

	
## List some classes and methods of the Reflections API
- getClass(), getMethods(). getName(), get

## Example of using Reflection API
JDBC API uses Java Reflection API to achieve loose coupling between java programs and JDBC Drivers
	

# Design patterns
## What are Singleton / Factory design patterns?
- Creational category, revolve around the creation of objects
- A singleton pattern ensures that you always get back the same instance of whatever type you are retrieving, 
- whereas the factory pattern generally gives you a different instance of each type. Basically Factory pattern is when a method returns one of several super class that share a common super class. Use when don' know what class u'll need. Like a random enemy base on user input

2. How would you create a Singleton?

3. Explain the DAO design pattern



# JDBC
## What is JDBC?
JDBC stands for Java Database Connectivity. It is a relatively low-level API used to write Java code that interacts with relational databases via SQL.


## What are the core interfaces / classes in JDBC?
- `DriverManager` class: used to register a database driver
- `DataSource` interface: used to retrieve connections as an alternative to `DriverManager`
- `Connection` interface: represents the actual physical connection with the database
- `SQLException` class: this is the general exception that is thrown when something goes wrong when accessing the database
- `Statement` interface: used in order to execute SQL statements
- `PreparedStatement` interface: represents pre-compiled SQL statements (which you can also pass different parameters into)
- `CallableStatement` interface: used to execute stored procedures (user defined functions)
- `ResultSet` interface: represents data returned from the database


## What is a stored procedure and how would you call it in Java?
- Stored Procedure is a user define function in the database
- To call it in Java, we use CallableStatement instead of PreparedStatement or Statement
```java
con = DriverManager.getConnection(dburl, dbuser, dbpass);
csmt=(CallableStatement)con.prepareCall("{call InsertProc(?,?)}");
csmt.setString(1, "Intel i7 Processor");
     csmt.setString(2, "27000");
     csmt.execute();
```

## What is the difference between Statement and PreparedStatement?
- Statement takes th whole sql string
- PrepareStament take each value that need to be filled which marked as ?, and setValue to them. It is more sercure from SQL injection attack because it esacpe spacial characters

## Steps to executing an SQL query using JDBC?
- Create an sql string
- Create a Statement or preparedStatement
- If it's a prepareStament, set parameter for each ?
- If it's a select or have a returning clause, executeUpdate() the Prepare Statement and and save the result in a ResultSet obj, then use if statement with resultObj.next() to get each value in each column. If there's an array of result, use while statement with result object.next()

## How to execute stored procedures using JDBC?
- Use CallableStatement instead of PrepareStament or Statement
stored procedures | user define functions
------- | --------
may or maynot return a value | have to return something (ex: if use a delete stament, return null, update: return new when use with Trigger)
can call a function | unable to call a procedure
support try catch block | not support
cannot be used in join clause as a result set | can be use in join clause

## Which interface is responsible for transaction management?
- The Connection interface maintains a session with the database. It can be used for transaction management. It provides factory methods that returns the instance of Statement, PreparedStatement, CallableStatement and DatabaseMetaData.



# JUnit
## What is Junit?
- Junit is a testing framework for Java

## What is TDD?
- Test driven development is a software development process relying on software development being converted to test cases before software is fully developed

## What are the annotations in JUnit? Order of execution?
- @FixMethodOrder(MethodSorters.NAME_ASCENDING): sort all test method inside a class by name. It's a class annotation
- Life cycle annotations:
- @BeforeClass: execute some statement before all test cases. It execute before the first test method
- @BeforeEach: precondition before each test case. Exceute before the @test under it
- @Test: the void method which it attached too is a test case. Execute the test case
- @AfterEach
- @AfterAll


## Give an example of a test case
```java
public class JunitExampleTest {				

    private ArrayList<String> list;	
	
	@BeforeClass
	pubic static void beforeAll(){
		System.out.println("Junit example test class")
	}	

	@BeforeEach
	public void createAnEmptyArrayList(){
		list = new ArrayList<String>();
	}

	@Test
	public void testListSize(){
		list.add("testing");
		assertFalse(list.isEmpty());
		assertEquals(1, list.size());
	}

	@AfterEach
	public void clear list(){
		list.clear();
	}
	@BeforeEach
	public beforeTest2(){System.out.println("Before test 2")}
	@test 
	public test2(){...}
}

// Junit example test case
// array list instanciate
// testListSize result true true
// Before test 2
// test2 result				
```

## How would you prevent a test from being run without commenting it out?
- @Disabled, @Ignore annotation
- @Disable let we write some message for the disabled test
0 We can also delete the @test annotation too. But it is not a good pratice as it not searchable or maintainable

# Log4j
1. What are the advantages to using a logging library?
- Logging is a powerful aid for understanding and debugging program's run-time behavior. Logs capture and persist the important data and make it available for analysis at any point in time.
- Loging libraries are popular because they run together with our application and they are portable (able to change file location) and easy to use

## What is log4j?
- log4j is a popular logging library for Java
```private static final Logger LOGGER = Logger.getLogger(ExampleLog4j.class);```

## What are the logging levels of log4j?
- Info, debug, warn, error, fatal
- Still in research: multiple logs files 
```
log4j.rootLogger=ALL,STDOUT,debugLog  
log4j.logger.reportsLogger=INFO,reportsLog 

-- All messages except report message
log4j.appender.debugLog=org.apache.log4j.RollingFileAppender  
log4j.appender.debugLog.File="/Users/test/debuglog.log"  
log4j.appender.debugLog.layout=org.apache.log4j.PatternLayout  
log4j.appender.debugLog.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} %-5p %C:%L - %m%n

-- report messages
log4j.appender.reportsLog=org.apache.log4j.RollingFileAppender  
log4j.appender.reportsLog.File="/Users/test/reportslog.log"  
log4j.appender.reportsLog.layout=org.apache.log4j.PatternLayout  
log4j.appender.reportsLog.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} %-5p %C:%L - %m%n  

private static Log log= LogFactory.getLog("debugLogger");  
private static Log reportsLog= LogFactory.getLog("reportsLogger"); 
  
log.debug("debug log message");  
reportsLog.debug("reports debug message");  
``` 

# Maven
## What is Maven?
- Maven is a dependency manager and build automation tool for Java programs. Maven project configuration and dependencies are handled using the Project Object Model, which is defined in a file called the `pom.xml` file

## What is the default Maven build lifecycle?

## Where / when does Maven retrieve dependencies from? Where are they stored locally?

## What is the POM and what is the pom.xml?
- POM is short for Project Object Model. It is the representation of a Maven project held in a file named pom.xml
- pom.xml is an XML file that contains information about the project and configuration details used by Maven to build the project

## What defines Maven project coordinates?
- groupId, artifactId, version, packaging, (classifier)

# Advanced
## What are functional interfaces? List some that come with the JRE for Java 8

2. What are lambdas?

## What is try-with-resources? What interface must the resource implement to use this feature?
- Generally finally block is used to close all the resources (viz., file, database connection, socket or anything that should be closed after its task is done) to prevent any leaks.
- There is a possibility of the close method throwing an exception and hence it has to be surrounded in a try catch block.
- The try-with-resources statement makes sure that every opened resource is closed at the end of the statement. So a try-with-resources statement is nothing but a try statement that declares one or more resources. A resource is said to be any object that implements java.lang.AutoCloseable interface

4. How to make numbers in your code more readable?

## Which collections cannot hold null values?
- HashTable, implements from Map collections, because its key required to be serialize and have to be able to use .equals
- TreeSet, which needs Comparble and Comparator interface
- TreeMap's key, because its keys need to be sorted 

## If 2 interfaces have default methods and you implement both, what happens?
- Only 1 unimplemented method show up. And if we write that method, both interface satisfy

## If 2 interfaces have the same variable names and you implement both, what happens?

## Why does HashTable not take null key?
- Because HashTable serilize the key, if it takes null, it'll throw a null pointer exception

9. What new syntax for creating variables was introduced with Java 10?

10. Is there an interactive REPL tool for Java like there is for languages like Python?

## What are collection factory methods?
- They are a new features in Java 9, they allow for easy initialization of immutable collections.
- These factory methods are only available for List, Set, Map
```java
List ilist = List.of();
Map<Integer, String> map = Map.of(1,"A", 2,"B", 3,"C");
```
- Note that They are structurally immutable. Elements cannot be added, removed, or replaced. Calling any mutator method will always cause UnsupportedOperationException to be thrown. However, if the contained elements are themselves mutable, this may cause the contents to appear to change.
- They disallow null elements

## SQL
1. Explain what SQL is. What are some SQL databases?

2. Draw a simple ERD for modelling Students and Classes

3. What are the 5 sublanguages of SQL? Which commands correspond to them?

4. What is the difference between DELETE, DROP, and TRUNCATE commands?

5. What are some SQL clauses you can use with SELECT statements?

6. What is the difference between WHERE and HAVING?

7. Explain what the ORDER BY and GROUP BY clauses do

8. Explain the concept of relational integrity

9. List the integrity constraints

10. Define the word schema

11. What is a candidate key? What about a surrogate key?

12. What conditions lead to orphan records?

13. What are some SQL data types?

14. What is normalization? What are the levels?

## What are the properties a transaction must follow?
-  Atomic, Consistent, Isolated, and Durable

## Explain the different isolation levels. What read phenomena do each prevent?
- Isolation level: Read uncommited, Read Commited, Repeated Read, Serialization
- Phenomenal: Dirty Read, Unrepeapted Read, Phantom Read 

## What is the difference between joins and set operators?
- Join: horizontaly, add more colum
- Set: add more row, some colum, add verticaly

18. What are the types of joins? Explain the differences.

19. Explain the difference between UNION, UNION ALL, and INTERSECT

20. What is a cascade delete?

21. What is the purpose of a view? What about an index?

22. Whats the difference between a clustered and non-clustered index?

23. What is a trigger? Give the syntax for creating a trigger.

24. How would you setup a primary key that automatically increments with every INSERT
statement?

25. What is the difference between scalar and aggregate functions? Give examples of each

26. Whats the difference between implicit and explicit cursors?

# HTML/CSS
# HTML
1. What is HTML?

2. What is the HTML5 doctype declaration?

3. List some tags. What is <head> used for? <body>?

4. What are the required tags for an HTML document?

5. What is the tag for ordered list? unordered list? Change bullet styling?

6. What features came with HTML5? Are HTML 5 tags different from other tags?

7. Do all tags come in a pair? List a self-closing tag.

8. Whats the difference between an element and an attribute? List some global attributes.

9. What is the syntax for a comment in HTML?

10. What tags would you use to create a table? A navbar? What about a form?

11. Whats the difference between a class and id?

12. How would you include CSS into an HTML document? What about JS?

13. What is a semantic tag? What about formatting tags/elements?

14. Whats the difference between a block and an inline element?



# CSS
15. What is CSS? what are the different ways of styling an html file?
	
16. Which way has highest priority when styles cascade: inline, internal, and external
stylesheets. Which is best practice? Why?
	
17. What are the different CSS selectors? Write the syntax for each.
	
18. What is a psuedo-class? What is the syntax for selecting that?
	
19. Write a CSS selector for styling all spans inside of a div. What about only targeting
spans that are direct descendents of divs?
	
20. Can I select multiple elements at once with CSS? If so, what is the syntax?
	
21. Explain the concept of specificity and how it relates to styling conflicts
	
22. Explain the CSS box model
	
23. What features did CSS3 introduce?
	
24. What is Bootstrap? What are some bootstrap classes you can use?
	
25. How many columns make up the Bootstrap grid system?
	
26. What is a CDN? what are the benefits? When would you choose to use a CDN vs
downloading and using the Bootstrap source code in your project?
	




# JavaScript
# Language Fundamentals
1. What is JavaScript? What do we use it for?

2. Can we run JavaScript in a web browser, on a server, or both?

3. What programming paradigm(s) does JS support?

4. What are the data types in JS?

a. What is the type of NaN? What is the isNaN function?

b. What is the data type of a function?

c. What about an array?

d. What is the difference between undefined and null?

5. What are JS objects? what is the syntax?

6. What is JSON? Is it different from JS objects?

7. What are some ways you can use functions in JS?

8. What are the different scopes of variables in JS?

a. What are the different ways to declare global variables?

b. Is it a best practice to use global variables? Why or why not?

9. What is function and variable hoisting?

10. What is the global object in client-side JavaScript?

a. What are some built-in functions (methods on the global object)?

b. How would you set some code to run at a specified time in the future? What
about repeatedly?

11. Explain how the guard and default operators work

12. What are callback functions? What about self-invoking functions?

13. What is closure and when should you use it?

14. Use the object literal syntax to create an object with some properties

15. What is a truthy or falsy value? List the falsy values.

16. What is the difference between == and ===? Which one allows for type coercion?

17. Explain the template literal syntax

18. What is a Promise?

19. What are arrays in JS? can you change their size?

20. List some array methods and explain how they work

21. Explain what strict mode does

22. Explain how inheritance works in JS

23. What does the "this" keyword refer to?

24. Explain the concept of lexical scope

25. What are some methods on the function prototype?

26. What will happen when I try to run this code: console.log(0.1+0.2==0.3) ?


# ES6+
27. What new features did ES6 introduce?

28. What is the difference between var, let, and const keywords?

29. Give the syntax for template literals / string interpolation

30. Whats the difference between a normal function declaration and an arrow function?

31. Does JS have classes? If so, when were they introduced?

32. What is object and array destructuring? What is the rest/spread operator?

33. How would you set default values for parameters to a function?

34. What is the difference between for-of and for-in loops?

35. Whats the benefit of computed property names?

36. Explain the async/await keywords. Why is it preferred to use this instead of .then()
methods?

37. What is a generator function? Whats the point of the yield keyword?

38. What built-in data structures does JavaScript provide?


# Events and DOM
39. What is the DOM? How is it represented as a data structure? What object in a browser
environment allows us to interact with the DOM?

40. List some ways of querying the DOM for elements

41. How would you insert a new element into the DOM?

42. What are event listeners? What are some events we can listen for? What are some
different ways of setting event listeners?

43. What is bubbling and capturing and what is the difference?

44. What are some methods on the event object and what do they do?

45. How would you submit a form using JS?



# AJAX
46. What is AJAX? why do we use it?

a. What are the benefits of using AJAX?

b. Are there any downsides of using AJAX?

47. Explain why it is important that AJAX is asynchronous

48. List the steps to sending an AJAX request

49. What are steps to sending an AJAX request?

50. List the different ready states of the XmlHttpRequest object

51. How does the fetch API differ from the XHR object?


# Servlets
1. What is a servlet? What about a servlet container? Which servlet container have you
worked with?

2. Describe the servlet class inheritance hierarchy. What methods are declared in each
class or interface?

3. How would you create your own servlet?

4. What is the deployment descriptor? What file configures your servlet container?

5. Explain the lifecycle of a servlet - what methods are called and when are they called?

6. Is eager or lazy loading of servlets the default? How would you change this?

7. What are some tags you would find in the web.xml file?

8. What is the difference between the ServletConfig and ServletContext objects? How do
you retrieve these in your servlet?

9. What is the purpose of the RequestDispatcher?

10. Explain the difference between RequestDispatcher.forward() and
HttpServletResponse.sendRedirect()

11. What are some different ways of tracking a session with servlets?

12. What is object mapping? Any Java libraries for this?

13. How would you send text or objects back in the body of the HTTP response from a
servlet?

14. What is the difference between getParameter() and getAttribute() methods?

15. Explain the front controller design pattern



# Angular
1. What makes a single page application (SPA) different from a normal web page?

2. Explain the difference between server-side and client-side rendering
 
3. What are some features of the Angular framework?

4. How does TypeScript relate to JavaScript? What are the major benefits of using it over
JavaScript?

5. List the data types of TypeScript

6. How would you create a new Angular project?

7. What is a component? How would you create one? List some other commands using the
Angular CLI

8. What files make up a component? What is the spec file used for?

9. Explain the relevance of npm to Angular projects. Which file does npm use to track
dependencies?

10. List some decorators for Angular apps

11. What is the lifecycle of a component? List some lifecycle hooks

12. What is a directive and what are the different types? How to tell these directives apart
with syntax?

13. What is the benefit of using a directive like NgClass over the class attribute, or even
property binding to the class attribute?

14. What is a pipe? A service?

15. How would you create a custom pipe? What about a service?

16. How does dependency injection work in Angular?

17. What is an Angular module? What properties should you set inside it?




18. Whats the difference between a JavaScript module and Angular module? What are
some common Angular modules?

19. How would you lazy load a module?

20. How have you used the HttpClient? What methods does it have and what do they
return?

21. What is an Observable? Whats the difference between it and a Promise?

22. What forms of data binding does Angular support? Explain the syntax for each

23. What does Webpack do for your ng project?

24. How would you implement routing in your project?

25. What is an EventEmitter and when would you use one?

26. Whats the difference between using reactive and template-driven forms? How would
you setup each?

27. How would you run your unit tests for an Angular project?



# DevOps + Linux + AWS
# DevOps
1. What is DevOps? What is the goal of various DevOps processes?

2. Explain CI/CD. What is the difference between Continuous Deployment and Continuous Delivery?

3. What tools have you used to achieve CI/CD? Explain how youve setup and used them

4. What is a DevOps pipeline? Explain the steps to setting one up

5. What is SonarQube / SonarCloud? Explain some of the features of it

6. What is a build? What is the end result of a build? What is the build tool youve used for
Java projects?

7. What are the Maven lifecycles? List the steps in the build lifecycle







# Linux
8. What is Unix? Linux? How are Linux OSs different from other OSs?

9. List some Linux distributions

10. Explain the terms terminal, shell, console, command-line?

11. What is the bash shell? How would you write a bash script?

12. What is the shebang syntax and purpose?

13. What is an environment variable and how would you set one?

14. What is the difference between relative and absolute paths?

15. Where are the root and home directories located? How to get to each?

16. What Linux command would you use to:
a. Search for text in a text file

b. Navigate your file hierarchy on the command line?

c. List files? What about hidden files? See permissions for the files?

d. Change the permissions of a file

e. Edit a file from the terminal

17. How do file permissions work on a Linux system?

18. What is a package manager? What are some common Linux package managers?

19. What does I/O redirection mean?

20. Explain the following bash commands:
a. cat actors.txt | grep Tom Cruise

b. echo hello world > myfile.txt

21. You run a command but get an error message saying you dont have enough
permissions. What could you try to resolve this?

22. You spin up a web server that listens for web traffic on port 80, but you forget the name
of the process. How would you look this up and then terminate the process on a Linux
command line?




# AWS
23. How would you describe AWS? What is the cloud or cloud computing and why is it so popular now?

24. Define Infrastructure, Platform, and Software as a Service
- IaaS: Infrastructure as a service - it delivers cloud computing infrastructures like servers, network, operating systems, and storage. Clients are responsible for managing applications, runtime, middleware. The provider manages servers, hard drives, networking, virtualization, storage. Ex: AWS, Microsoft Azure, DigitalOcean

- PaaS: Platform as a service - a complete deployment and development environment in the cloud. It include infrastructure, middleware, database management system Client building the software. Provider manages the operating system, updates. Ex: AWS ElasticBeanstalk, Heroku, Window Azure

- SaaS: Software as a Service - allow users to connect to and use cloud-based, pay-as-you-go apps Ex: Dropbox, Salesforce

25. Whats the difference between a Region and an Availability Zone (AZ)?

26. How are you charged for using AWS services?

27. Explain the following AWS services:
a. EC2

b. EBS

c. RDS

d. Route 53

e. VPN

f. S3 / Glacier

g. Lambda

h. AMI

i. IAM

j. ELB

28. What steps would you take to create an EC2 and connect to it via your shell?

29. What configuration options are available for an EC2?

30. What are Security Groups? When defining a rule for a security group, what 3 things do
you need to specify?

31. Whats the difference between scalability, elasticity, and resiliency? What is autoscaling?

# Hibernate
## What is Hibernate? What is JPA?
- Hibernate is a framework which provides some abstraction layer, meaning that the programmer does not have to worry about the implementations, Hibernate does the implementations for you internally like Establishing a connection with the database, writing query to perform CRUD operations etc.
-JPA is just a specification that make it easy for object-relational mapping to manage relational data in Java applications. It provides a platform to work directly with objects instead of using SQL statements.

## What is the benefit of using Hibernate over JDBC?
- Too much boiler code in JDBC
- Have to convert data from each column while JPA helps us to return object

3. Tell me about some of the JPA annotations you have worked with? What do they do?
How do you specify multiplicity relationships with JPA annotations?

4. What are the interfaces of Hibernate?

5. Tell me how you set up hibernate? What files are you editing, what goes in them, etc.

6. What ways are available to you to map an object to database entities in Hibernate?

7. In the session interface, what is the difference between save and persist methods? get
and load methods? Update vs merge methods?

8. What are the different session methods?

9. What is the difference between Eager and Lazy fetching and how to setup either?

10. Under what circumstances would your program throw a LazyInitializationException?

11. What are the 4 ways to make a query using Hibernate?

12. What is HQL? What makes it different from SQL?

13. What is the Criteria API? Can you perform all DDL and DML commands with it? How do
Restrictions and Projections work within this API?

14. What is caching? What is the difference between L1 and L2 cache?

15. How do you enable second level caching?

16. Tell me about NamedQueries.

17. Can you write native SQL with Hibernate? Is this a good idea?

18. What are the configuration options for Hibernate?

a. How to specify the SQL dialect?

b. What data must be specified for the SessionFactory?

c. What is hbm2ddl?

d. How would you configure Hibernate to print to the console all SQL statements
run?

19. What are the different object states in Hibernate? What methods move objects to
different states?

20. What is a proxy? When does the proxy resolve to the real object?

21. What is the difference between Dynamic Insert and Dynamic Update?

22. What is automatic dirty checking?

23. What is Transactional Write Behind?

24. Explain how transaction propagation works



# Spring
# Spring Core
1. What are Spring Projects and Spring Modules?

2. What is IOC and what does the IOC Container do?

3. What is dependency injection and what are some of the benefits of using dependency
injection?

4. What types of dependency injection does Spring support?

5. What are some differences between BeanFactory and ApplicationContext? Which one
eagerly instantiates your beans?

6. What is the Spring Bean lifecycle?

7. What is bean wiring? What about autowiring?

8. What are the different ways that Spring can wire beans?

9. What are the scopes of Spring beans? Which is default?

10. What is the concept of component scanning and how would you set it up?

11. What are the benefits and limitations of Java configuration?

12. What does the @Configuration and @Bean annotations do?

13. What is @Value used for?

14. What is Spring Expression Language? What can you reference using SpEL? What is the
difference between $ and # in @value expressions?


# Spring MVC
15. Explain the MVC architecture and how HTTP requests are processed in the architecture

16. What is the role of the DispatcherServlet? What about the ViewResolver?

17. List some stereotype annotations. What are the differences between these?

18. How would you declare which HTTP requests youd like a controller to process?

19. What is the difference between @RequestMapping and @GetMapping?

20. How to declare the data format your controller expects from requests or will create in
responses?

21. What annotation would you use to bypass the ViewResolver?

22. How would you extract query and path parameters from a request URL in your
controller?

23. What concerns is the controller layer supposed to handle vs the service layer?

24. How would you specify HTTP status codes to return from your controller?

25. How do you handle exceptions thrown in your code from your controller? What happens
if you dont set up any exception handling?

26. How would you consume an external web service using Spring?

27. What are the advantages of using RestTemplate?



# Spring AOP
28. What is aspect-oriented programming? Define an aspect.

29. Give an example of a cross-cutting concern you could use AOP to address

30. Define the following:
a. Join point

b. Pointcut

c. Advice

31. What are the different types of advice? What is special about the @Around advice? How
is the ProceedingJoinPoint used?

32. Explain the pointcut expression syntax

33. What visibility must Spring bean methods have to be proxied using Spring AOP?


# Spring Data
34. What is Spring ORM and Spring Data?

35. What is the Template design pattern and what is the JDBC template?

36. What does @Transactional do? What is the PlatformTransactionManager?

37. What is a PersistenceContext?

38. Explain how to integrate Spring and Hibernate using ContextualSession

39. What interfaces are available in Spring Data JPA?

40. What is the difference between JPARepository and CrudRepository?

41. What is the naming conventions for methods in Spring Data repositories?

42. How are Spring repositories implemented by Spring at runtime?

43. What is @Query used for?


# Spring Boot
44. How is Spring Boot different from legacy Spring applications? What does it mean that it
is opinionated?

45. What does convention over configuration mean?

46. What annotation would you use for Spring Boot apps? What does it do behind the
scenes?

47. How does Boots autoconfiguration work?

48. What is the advantage of having an embedded Tomcat server?

49. What is the significance of the Spring Boot starter POM?

50. What is the Spring Boot actuator? What information can it give you?

51. What files would you use to configure Spring Boot applications?

52. What is the benefit of using Spring Boot profiles?




# Web Services
HTTP
## What is a web service? Whats the advantage of distributing software as a web service?
- Web service is a standardized medium to propagate communication between the client and server applications on the World Wide Web

## Whats the difference between REST and SOAP services?
REST | SOAP
---- | ----
Representational State Transfer | Simple Object Access Protocol 
faster | slower
lighter | heavier
an architectural pattern | a protocol
works with plain text, html, xml, json | works only with XML
can make use of SOAP | cannot make use of REST

## What does HTTP stand for?
- Hyper Text Transfter Protocol

## What are the components inside of an HTTP request? What about an HTTP response?
- Http request: verb, URI, HTTP version, Request header, request body
- Http response: Status, HTTP version, Response Header, Response Body

## What are the important HTTP verbs / methods and what do they do?

- Which are idempotent? GET, PUT, DELETE, HEAD (check the server information, like check a file size)

- Which are safe? GET, HEAD

6. List the levels of HTTP status codes and what they mean

7. What are some specific HTTP status codes that are commonly used?

## What is service-oriented architecture (SOA)?
-  An SOA architecture recognizes that within an application these components are required, and creates a structure where the components themselves can exist independent of each other
- Service-oriented architecture (SOA) is an architectural pattern as well as a collection of design principles that support loose coupling and reusability of different components
- loose couping is the key concept of SOA
- Common used tech to archieve SOA: WSDL, SOAP, REST
- SOA provides access to reusable components (i.e. Web services) over a Network
- Service-oriented architecture is often compared to microservices as both share the same fundamentals. Microservices, which are more recently developed than SOA, are even considered to be a type of SOA
SOA | Web service
---- | ----
creat reusable service | continuous interation and delivery is key
older | new
access common data store | each microservice has its own data repository (self-contained)

## How can you achieve loose coupling with SOA?
- Enterprise Service Bus
- Business Process Management
- Service Oriented Intergration

## What is an Enterprise Service Bus (ESB)?
- Enterprised Service bus is used to comunicate between services, ensure delivery and response of messages, as well as monitoring the flow of communication

## What are some best practices when creating web services?



# SOAP
## What does the acronym SOAP stand for?
- Simple Object Access Protocol
- lightweight, XML-based protocol for exchanging information in a decentralized, distributed environment.

## What protocols and data format do SOAP services use?
- SOAP itself is a protocol Simple Object Access Protocol
- Data format: XML file with  header element<?xml?>, Envelope element (<soap:Envelope>), body element<soap:Body>, fault element

14. What is the contract for a SOAP service?

15. Whats the structure of a SOAP message? Envelope (hold everything, require), Header , Body (requir), Fault

16. What are the SOAP messaging modes? Messaging Exchange Patterns?

17. Are SOAP messages delivered with GET or POST requests?
- yes, it can if it binds to Http protocol

## Soap vs Xml
- XML is a markup language that is used to transfer data between driver hardware, operating systems and applications with little human intervention, while SOAP is a protocol based on XML that is used to communicate between applications through internet




# REST

## Http
- HTTP protocol is a staeless protocol used for fetching resources on the internet

## What does the acronym REST stand for? What makes a service RESTful?
- REST stands for Representational State Transfer. Its an architectural pattern for creating web services
- RESTful service implements REST pattern. It is considered restful when it had all architecture coinstain of REST aside for the optional code on demand one 

## What protocols and data format do REST services use?
- Html
- Xml, Json, Plain text

## What are the architectural constraints of REST?
 Uniform interface (consistent namespace), Client server (front & back seperate), Stateless (server not stored http request), Cachable, Layer System (deploy on server A, authenticate request on server C, store data on server B), Code on demand

21. Explain the levels of the Richardson Maturity Model

22. Explain the HATEOAS concept

## What is a resource in a REST service?
- Rest treat everthing as a resource. 
- It uses various representations to represent a resource like Text, JSON, XML

24. What does the uniform interface constraint mean? Give an example of some RESTful
endpoints you would create for an API. Should the URLs contain nouns, verbs, or
adjectives?

25. How would you implement authentication/authorization in a RESTful web service while
maintaining statelessness?


# Microservices
## Compare the microservice and monolithic architectures. What are the advantages / disadvantages of each?
### Monoliths: 
- Single codebase, Single process Single host, Single database, Consistent technology
- **Benefit**: 
	- Simple, one codebase- easy to find, for deployment, there's only 1 application to update. 
	- It Works well for small app, with a small dev team (2-3 members), work together for a few months, moderate visitors
- **Problem**: its scale. 
	- When codebase become big, it is very difficute to deploy: Even one small change requires downtime and break the code
	- Really difficult to scale: unable to scale horizontally and vertical scalling are expensive. Plus, the entire application have to be scalled together
	- Hard to get away from legacy code since we have to move the entire application to a new framework
### Microservices:
- Benefit:
	- Contains small services that can be owned by small development team. A rule of thumb is it should be small enough to be throw away and rewritten in a different way
	- Able to adopt new technology without the need to update anything in one go. We can choose the right tool for the job
- Ability to deploy them individually which minimize downtime and reduce risk enable frequent updates
	- Scaling: scale the services individually
	- The services can be reuse
- Challenges:
	- Complex interaction 


## Can a Java microservice communicate with a Node.js microservice? Why or why not?
- Yes. Beacause each service is independent to each other. The only thing we need is to send or received data from the REST API

## Whats the difference between horizontal and vertical scalability? Which way do monoliths and microservices typically scale?
- Vertical scaling/ Scale up: upgrade/ add more RAM, processor (like add more seat to your car). It cost a lot of money and we are stuck with a particular vendor
- Horizontal Scalling:  adding more machines. It reduces price, easier to maintain, less downtime

## What are some best practices for building microservices?
- Centralize logging is the first and most importnt rule of micro service logging. We can use a centralize logging system like Loggly, Splunk, Stackify
- Need to implement fault torelent by break the circuit if there is no response

## What is a messaging queue and how is using one different from calling service APIs directly?
- Once we've shattered our monolith, how do we put it back together into a larger system that still makes sense? That is when static load balancing, Messaging queue, API Gateway and Service Mesh come to place
- A message queue is a form of asynchronous service-to-service communication used in microservices architectures
- Different :
	- Message queues are asynchronous and can retry a number of times if delivery fails. 
	- When calling service API directly, if the server fails, the client handles the error. When server restart, client resend
	

6. What is a replica?

## Explain the Netflix OSS stack for microservices (Eureka, Zuul, Hystrix)
- **Netflix OSS** is a tool in the **Container Tools category** of a tech stack. It provides 5 important componants to overcome some microservies drawback which is hard to manage when there are hundreds of services
- **Netflix Eureka** : Service registration (for producer) and service discovery (for consumer). It's like a Naming server, other service lookup to consume other service
- **Netflix Ribbon** : Dynamic Routing and Load Balancer. It is an admin of multiple instances of a service. If one collapse, call the other
- ''Netflix Feign Client**: Communication among micro services
- **Netflix Zuul** : Edge/ proxy/ Gateway Server. Client gets a registered service in Eureka Registry Server using Zuul server. It's a client side load balancing
- **Netflix Hystrix** : Circuit Breaker (fault tolerance, default response when things break)
## How would you setup and configure Eureka? Zuul? Hystrix?
- ''Eureka** : 
	- Create a new Spring Boot project for Eureka, choose Eureka server dependency. Set register with Eureka and fetch-registry = false for that registry service in application.yml. For other services depend on it. Add Eureka For Client dependency, set to true for both properties
	- @EnableEurekaServer for producer, @EnableEurekaDiscovery(for consumer)
	- In application.yml of services, set default zone of service-url to Eureka register project url and its hostname will be localhost. Set application name too
	- Now, if run 2 services and eureka, information will appeared in erureka register project localhost. Should use that name with rest template to do http get, post request for department (if there's no API gateway)
- **Zuul**: 
	- Create a new project, add Erureaka Client, Gateway, Acculator. @EnableEurekaClient
	- Application ->name, cloud ->gateway ->routes with id = register name, uri = lb://register-name, predicates -> path: /user/** so every path with /user will gor to User service registered in Eureka server
	- So now when we make a http request, all request should go to Zuul gateway. /user will interact with user service 
- **Hystrix**: 
	- Get Hystrix dependency and add in Zuul Gateway.
	- @EnableEurekaServer, @EnableHystrix in Main
	- Create a controller name FallBack/Fail Controller. Use @RestController annotation, on method, use @GetMapping("userFailMethod"), create a method that return a string said please try again later
	- In application.yml, under predicates where the http path is, add filters -> name: CircuitBreaker, args -> name: register name, fallbackuri: userFailMethod (from @GetMapping)
	- Able to set timeout too. If user doesn't get a response in 4000 mili second, it'll http get to fallback path and send the fail message. hystrix->command->fallbackcmd->execution->isolation->thread->timeoutInMilliseconds

## What is the purpose of an API gateway and how does Zuul perform this?

10. What is service discovery and how does Eureka do this?

11. What is the circuit breaker pattern and how does Hystrix implement it? What are the different circuit states?

12. Is there any order in which you need to spin up these services?

## One of my microservices is throwing a TransportException! What might be the problem?
- Basically, this happens due to the wrong configuration in application.properties or application.yml.
- Either spelling mistakes, or wrong registerWithEureka and fetchRegistry value. (eureka server should set them t false, services that registry to Eureka should set to true)



# Docker
- Docker is a set of platform as a service products that use OS-level virtualization to deliver software in packages called containers.
- JVM is a Application level virtualization btw

## What is containerization?
- Also called operating-system-virtualization
- A way to ship the code from 1 computer environment to other
- It ship everything we needed. Code, runtime, system tools, system libraries, settings, OS-level virtualization into 1 package and it's very lightweight
- Multiple cointainers can share the same runtime, system libraries, settings, OS level virtualization 

##OS level virtualization
- It like a permanent loaded on the local device
- The physical server and single instance of the operating system is virtualized into multiple isolated partitions, where each partition replicates a real server

## How are containers different from virtual machines?
Containers are often compared to Virtual Machines (VMs), since both of them allow multiple types of software to be run in contained environments
Container | Virtual machine
----- | -----
abstraction of application layer | abstraction of hardware layer
containers are lightweight because they do not require an extra load of a hypervisor. They run directly within the hosts machine. Nospace needed for virtualization | Each VM is a guess OS
Faster | Requires entire OS to be loaded before starting
more secure | less sercure
complex usage mechanism | simplier to work with

## Docker Daemon
- Docker Daemon is a server
- When you use docker run command to start up a container, your docker client will translate that command into http API call, sends it to docker daemon

## What is a Docker image? Container?
```
docker pull <image name>, 
docker images -f "dangling=false" (filter by not associate with any container), 
docker images -a (list), 
docker run <image-name> (save to a container)
```
- Docker images are templates used to create a docker cointainer
- When running a container, it uses an isolated filesystem. This custom filesystem is provided by a container image
- An image is a static representation of the app or service and its configuration and dependencies.


## List the steps to create a Docker image and spin up a container
- Create a working directory
- Create a file name DockerFile, add some info like FROM scratch/ibuntu/php:7.1
```touch DockerFile```
- Build an image
```docker build -t random-name ```
``` docker run --name container-name -p 80:80 image-name ```

## What is the relevance of the Dockerfile to this process? List some keywords in the Dockerfile
-  Docker file uses to build a Docker image. It is a The Docker file is a text-based script
```docker
FROM --platform=<platform> <image-name>
RUN apt-get update
```

## What is the benefit to an image being built in Layers?
- We can commit our changes. Docker Layer works like a version cotrol system

## What are some other Docker commands?
- docker commit -m""
- exit
- docker push localhost:5000/ubuntu
- // local host:5000/ubuntu is a tag
- docker tag image-name tag-name
- docker image ls

## What is a container registry? How would you retrieve and upload images to DockerHub?
- The registry is like a bookshelf where images are stored and available to be pulled
- docker image pull image-name:tag-name, docker pull tag-name 
- docker image push [tag-name]

22. What is Docker compose and why is it useful?
- Compose is a tool for defining and running multi-container Docker applications as a single service. With Compose, you use a DockerCompose.yml file to configure your applications services
- Benefits: Single host deployment, easy to use, reduce times
```
#start all service
Docker Compose up
#Stop all
Docker compose down
#Scall a service
Docker Compose up -d -scale
```

23. If you want to store state for a container, how does Docker recommend doing that?



# Kubernetes
1. What is container orchestration? How does Kubernetes help with this?

2. What is a pod? A service? A deployment? A replicaSet?

3. Explain the pod lifecycle

4. What configuration file would you write for a Kubernetes deployment and what properties
would you set?

5. What is the difference between a pod and a node?

6. What containers would be grouped together in a pod?

7. What is the purpose of the master and worker nodes on Kubernetes?

8. List some kubectl commands you know and what they do

9. How do you handle secrets in Kubernetes?

# Misc/Other
# Git
1. What is version control? What makes git different from other version control software?

2. List the git commands you know and what they do

3. How would you prevent a file from being tracked by git?

4. What is a branch? What are some common branching strategies?

5. What is a merge conflict? How do you prevent these and resolve if it happens?

6. What is a GitHub pull request?

7. What is the git workflow for editing code and saving changes?

8. What is a commit?

9. How would you go back in your commit history if you make a mistake?

# SDLC
## What are the steps in the software development lifecycle?
- requirement gathering + data analysis -> Design -> code -> testing -> deploy -> maintenance

## What is the difference between Waterfall and Agile methodologies? Explain the benefits
and drawbacks of each
- Waterfall is rigid. There is only 1 way to go. Good when little to no client involement. Bad when direction always change
- Agile is flexible. Opposit

3. List some of the principles declared in the Agile manifesto

## What specific Agile frameworks exist? What are the main features of each?
- Scum: stresses teamwork in project management. 2 primary roles: Scum master, product owner
- Lean Software Development: highly flexible. Rely on rapid feedback between programmers and customers
- Kanban Software Development: build upon lean software. 3 base principles: Visualization, limit the ammount of working progress, Enhance flow
- Feature Driven Development (FDD): its benchmark is: Developing the overl model, build a feature list, plan on list begin, design, implement

5. What is the Scrum process? Explain each of the Scrum ceremonies


## How long is a typical sprint?
- Sprint are fixed length events of one month or less to create consistency

7. What is a standup and what should you report about your work?

## What is the role of a Scrum master in a project? What about the Product owner?

9. Explain the following metrics/charts: sprint velocity, burndown chart

10. What is a Scrum board? Have you used any software tools for your teams Scrum
board?
