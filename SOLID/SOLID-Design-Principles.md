

# Design Principles
## SOLID

### Single Responsibility Principal
**Definition:**  There should not be more than one reason for a class to change, or  **a class should always handle single functionality**.

**Main goal:**  To avoid introducing coupling between functionalities, because there is a chance of breaking coupled functionality when changes are made in of of them. That will require another round of testing to avoid any surprise on the production environment.

### Open/Closed Principle

**Definition:**  Classes, methods or functions should be Open to extension (new functionality) and Closed to modification.  
**Main goal:**  To prevent someone from changing already tried and tested code and allows the system to be open for extension through the use of inheritance, or interfaces. The main idea of this principle is to keep existing code from breaking when you implement new features.

**What does Open to Extension mean?**
This statement means that when a class is been designed the ideia of that new funcionalities can be added as new requirements are generated must be considered. 

**What does Closed to Modification mean?**
The statement **closed to extension** means that once a class is developed and tested this class should not be modified anymore, exept to correct bugs.

Generally extension can be achieved by using abstractions for dependencies, such as abstract classes and interfaces rather than using concrete classes.


### Liskov Substitution Principle
When extending a class, the subclass (the one which inherits a base class), should be able to be passed in place of objects of
the parent class without breaking the client code. Meaning that the subclass should remain compatible with the behavior of the superclass. 

**One Use Very Important of Liskov Substitution Principle**
This concept  is critical when developing libraries and frameworks because the classes are going to be used by other people whose code cannot directly be accessed and changed.

#### Liskov Substitution Requirements
* **A subclass shouldn’t strengthen pre-conditions**
A subclass shouldn’t strengthen pre-conditions. That is, a subclass shouldn’t strengthen pre-conditions.  
**Example:**  Before calling a method that reads from a database you may need to satisfy the precondition that the database connection is open. If the subclass add more conditions, there is a viollation of the principle

* **A subclass shouldn’t strengthen pre-conditions**
A subclass shouldn’t strengthen pre-conditions. This means that the subclass should cause the state of the program to be in the same state as the base class after a method call.
**Example:**  After calling a method that reads from a database it may be assumed that the database connection is closed after executing a SQL statement. If the subclass remove the condition of close the database conection, there is a viollation of the principle.

* **Invariants of a superclass must be preserved**
Invariant conditions that exist in the base class, must also remain invariant in the subclass. Since invariant conditions are expected to be immutable, the subclass should not change them as it may cause a side effect in the behaviours of the base class or the program. Invariants can be described as:
	> "A condition of a process that is true before the process begins and remains true afterwards" [font](http://www.blackwasp.co.uk/lsp.aspx)

	**Example:** Consider a class that has a method to handle files. If the method handles the process to open and close a file, an invariant may be that the file is not open befor the call of this respective method.

* **Immutable characteristics of a base class must not be changed by the subclass**
An subclass inherits methods and properties of its superclasses. The **immutable characteristc** constraint says that new or modified members should not modify the state of an object in a manner that would not be permitted by the base class. For example, if the base class represents an object with a fixed size, the subclass should not permit this size to be modified.

* **The subclasses should not throw exceptions that are not thrown by the base class**
types of exceptions should match or be subtypes of the ones that the base method is already able to throw. 

**Contextualizingwith an Example - By Uncle Bob**
> In mathematics, a **Square** is a **Rectangle**. Indeed it is a specialization of a rectangle. The **"is a"** makes you want to model this with inheritance. However if in code you made **Square** derive from **Rectangle**, then a **Square** should be usable anywhere you expect a **Rectangle**. This makes for some strange behavior.

> Imagine you had **SetWidth** and **SetHeight** methods on your **Rectangle** base class; this seems perfectly logical. However if your **Rectangle** reference pointed to a **Square**, then **SetWidth** and **SetHeight** doesn't make sense because setting one would change the other to match it. In this case **Square** fails the Liskov Substitution Test with Rectangle and the abstraction of having Square inheriting from Rectangle is a bad one.

**Comments** - Requirements this example does not respect
	*  A subclass shouldn’t strengthen pre-conditions, because if you set a **Square**, immediatly you are saying that witdth and height must be the same, and it is not considered by the superclass, thus here we have a viollation.

### Interface Segregation Principle
The principle Interface Segregation states that **a class should not be forced to depend on methods it does not use**. Meaning that any classes that implement an interface, should not have "dummy" implementations of any methods defined in the interface. Instead, **large interfaces should be splited into smaller generalizations**.

* A class should not be forced to depend on methods it does not use
* Interfaces should be split up in such a way that it can properly describe the separate functionalities of your system


### Dependency Inversion Principle
This principle states that high level modules should depend on high level generalizations, and not on low level details. Meaning that classes if will there dependencies they should depend on a interface or abstract class rathar than concreate classes. If clients are dependent on higher-level generalizations then low level implementations can be changed or replaced with more ease later on. This is a form of looser coupling.

Also, dependency inversion helps in the generalization of the behavior of your concrete classes into abstract classes and interfaces

## Composing Objects Principle
Composing Objects Principle states that **classes should achieve code reuse through aggregation and delegation rather than inheritance.**
* Provide means of code reuse withoud the tight coupling of inharitance
* Independency among the compose classes since they don't share attributes or implementations of behaviours and operates separately. 
* Dynamically change the behaviour of objects at run time achieved by composing objects. In inheritance case, the behaviours are defined during the compiled time, which means that while the programm is running it cannot change how they behave.

![ Composing Objects Principle](ComposingObjectsPrinciple.png)

**Disadvantages**
The biggest drawback of the composition is that the implementations must be provided implementations for all behaviour without be benefit of inheritance to share code. Meaning that might exist similar implementations across classes.

## Principle of Least Knowledge
A class should be designed so that it does not need to know about and depend upon almost every other class in the system. This approach avoids increasing coupling and turn hard the maintenance. By limiting which classes communicate with each other, the principle of least knowledge is enforced.

### Law of Demeter
This law define how classes should interact with each other, the should not have access to the entire system because it causes a high degrre of couplin.
A classes should know about and interact with as few other classes as possible. This means that any class should only communicate with its immediate friends. These friends would be other classes that one class should only know about.

**Goal:** THis design principle focuses more broadly on how methods call shoud be made.

#### Rule #1 -
A method, M, in an object, O, can call on any other method within O itself.

#### Rule #2 - 
A method, M, can call the methods of any parameter P.

#### Rule #3 - 
A method, M, can call a method, N, of an object, I, If I is instantiated within M.

#### Rule #4 - 
A method, M, in object O, can invoke methods of any type of object that is a direct component of O.

#### Summary of Law of Demeter
>You should not allow a method to access another method by "reaching through" an object. This means that **a method should not invoke methods of any object that is not local** (local: passed in through parameters or they should be instantiated within a method).

**Conditions that Break Down the Rules of the Law of Demeter**
* Chain of method call to objects that the class "should not know about".

```java
public class Driver {^
	Car myCar = new Car();
	
	public void drive() {
		this.myCar.engine.start(); // The driver only know about the Car class and the engine is not a 			object defined within de Driver class, thus the driver should not be calling methods of the engine
	}
}
```

* Use methods of an unknown type of object that is returned from a local method call.
Returned objects must be of the same type as:
	*	Those declared in the method parameter
	*	Those declared and instantiated locally in the method
	*	Those declared in instances variables of the class that encapsulates the method

```java
public class Driver {^
	Car myCar = new Car();
	
	public void rentVehicle(VehicleRentalStore store) {
		Motorcycle myRental = store.rent("motorcycle"); // Since the class MotorCycle is not specified with the method parameters or local instanciations, the driver should not work with Motercycles.
		myRental.drive();
	}
}
```




## References
http://www.blackwasp.co.uk/lsp.aspx

https://stackoverflow.com/questions/56860/what-is-an-example-of-the-liskov-substitution-principle

