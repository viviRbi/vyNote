# Design Pattern

- Design Patterns represent the best practices used by experienced object-oriented software developers

### OOP design principles are called SOLID:
**Single responsibility principle**: 
- "A class should have only one reason to change". Which means if we have 2 reasons to chance for a class, we have to split funtionality into 2 classes
- It is a good pratice to make encapsulation works its best
- In other hand, each responsibility/ reason to change will add new dependency and make to code less robusted
- Ex: A Car class not only encapsulate the logic but also the database operations (2 responsibility, aka 2 reasons to change). This will make the code harder to maintain. Also, if we change the Car databse code, it might generate error in the Car logic. The solution would be create two classes: one to encapsulate the Car logic and other responsible for interacting with the Database (Car and CarDao class)

**Open/Closed principle**:
- "Modules, classes, and functions should be open for extension but closed for modifications". Means we should strive to write code that doesn't have to be changed everytime the requirement change
- Once we finish a part of our software, we should not modify it anymore but build on top of it (using inheritance and polymorphism)
- Ex: We have a class Area which calculate area of a shape ```public double Area(object[] shapes)``` We use a foreach loop and calculation method changed base on its shape (Rectangle, Circle). One problem with it is when we add a new shapw (triangle), we have to change the code inside. Instead, we can make an abstract class of Shape with an abstract method Area and extends class Rectangle, Triangle and create a calculate Area method base on it.

**Liskov Substitution Principle**:
- "Derived types must be completely substitutable for their base types". Meaning if we substitue a superclass object reference with an object of any of its subclasses, the program should not break
- Liskov Subtitution Principle is strongly related to subtyping polymorphism. 
- A derived object can be substituted with its parent type. Ex: if we have a Car object, it can be used in the code as a Vehicle
- The derived type should behave as its supertype and should not break its behavior (it called Strong Behavior subtyping)
- Ex: We have a Garage object that repairs all Vehicle. If we have a Truck extends from Vehicle, the Garage should be able to repaire it

**Interface Segregation Principle**
- "Clients should not be depend on interface they don't use"
- Violate situation: At first, u have a CoffeeMachine Interface, which implement by BasicCoffeeMachine class. Then the client wants to have an EspressoMachine class too. You decided to implent Coffee Machine interface since EspressoMachine is a Coffee machine too. But you don't have a brewEspresso method in that interface, so you add it. So now BasicCoffeeMachine class had a method they don't use (brewEspresso)
- Fix: split CoffeeMachine interface into multiple interfaces for different kinds of coffee machines. Since all machine need addGroundCoffee method, it'll be in the CoffeeMachine Interface. We extends CoffeeMachine to FilterCoffeeMachine and EspressoCoffeeMachine. Add brewFilterCoffee() to FilterCoffeeMachine interface and add brewEspresso() to EspressoCoffeeMachine

**Dependency Inversion Principle**
- "High-level modules should not depend on low level modules. Both should depend on abstraction."
- "Abstraction should not depend on details. Details should depend on abstractions."
- It focuses on the approach where the higher classes are not dependent on the lower classes instead depend upon the abstraction of the lower classes
- It is a combination of Open/Closed and Liskov Principle. It is important enough to have its own name
- Violate case: We have a LightBulb class, and an ElectricPowerSwitch class. The ElectricPowerSwitch class had a lightbulb field, and pass the lightbulb obj to that field in the constructor. We also have an isOn and press(for on/off) method. -> Our high class in this case depend on the low-level class (lightbulb). The switch should not be tied to a lightbulb. It should be able to turn other device on and off too. Each time we add a new device, we have to modify the switch class 
- Solution: To follow DIP, we need an abstract class for ElectricPowerSwitch (Switch interface with isOn() and press() method) and LightBulb (Switchable interface with turnOn() & turnOff() method). In ElectricPowerSwitch class, we add a field Switchable, and set the Switchable object to that field in a parameter constructor. Now we can add another class like Fan and implement Switchable interface and it'll work like lightBulb  

### Usage of Design Pattern
	- Common platform for developers
	- Best practices

### Types of Design Patterns: 
There are 26 design patterns which can be classified in 3 categories: Creational, Structural, Behavioral Patterns. Another category is J2EE patterns
	- **Creational Patterns**: designed for class instantiation
	- **Structural Patterns**: designed with regard to a class's structure and composition 
	- **Behavioral Patterns**: designed depend on how one class communicate with one another
	- **J2EE Patterns**: concerned with the presentation tier. These patterns are identified by Sun Java Center

## Creational Pattern
Singleton, Simple factory, Factory method, Abstract factory, Builder, Prototype, Object pool Patterns

### Singleton pattern
- It is a simple pattern and easy to used. Sometimes it is used where it not required. In that case, the disadventages of using it overweigh the advantages it brings. However, there are many times singletions are necessary
- Singleton pattern is used to ensure that only a single instance of an object can be created. It also provides global access to that instance.
- To ensure that the singleton instance is unique, all constructors should be made private
``` java
public class Singleton {
	private static Singleton instance;
	private Singleton(){
		System.out.println(){"Instanciated"};
	}
	public static Singleton getInstance(){
		if (instance == null)
			instance = new Singleton();
		return instance;
	}
}
```
Invoke the singleton object by ```Singleton.getInstance().doSomtihng();```
If instance = null, it had been created before

### Synchronized singleton
