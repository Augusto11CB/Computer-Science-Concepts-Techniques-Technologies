

# Design Principles
Improving quality, design and maintainability with Design Principles

**Code Fragility** by Robert C. Martin
> Fragility is the tendency of the sw to break in many places every time it is changed

**Code Rigidity** by Robert C. Martin
> Rigidity is the tendency for software to be difficult to change, even in simple ways. Every change causes a cascade of subsequent changes in dependent modules

## D.R.Y (Don’t repeat yourself) Principle
Analysis of the written code and the desire to improve it are always key in software writing.

When writing several classes with similar properties, we may encounter similar problems. This is a sign that the code inside these classes is common and it may indicate that it should be separated into another class that will deal with repetitive tasks in one place. Thanks to this operation, both classes will use the same code, and thus, the probability of error will drop.

## KISS - Keep It Simple, Stupid!
This rule is often mentioned when discussing architecture or details of building projects. Its essence is striving to maintain an elegant and transparent structure, without adding unnecessary elements.

## SOC - Separation of Concern
The separation of issues consists in the division of the program into separate modules that overlap with as little functionality as possible. We call this kind of program modular. Each element of the system should have its separate and singular application. The purpose of SoC (Separation of Concern) is to create a system in which each part plays a significant role while maintaining the possibility of maximum adaptation to changes. SoC does not refer only to the system architecture, but to various issues, eg to divide the application into layers (presentation, business logic, access to data, database).

## CQS - Command Query Separation
It is a rule that says that every method in the system should be classified into one of two groups:

Command - these are methods that change the state of the application and do not return anything.
Query - these are methods that return something, but do not change the state of the application.

## Tell, don't ask Principle
Used to eliminate type casting and checkong


## SOLID Principles

## Single Responsibility Principal
**Definition:**  There should not be more than one reason for a class to change, or  **a class should always handle single functionality**.

**Main goal:**  To avoid introducing coupling between functionalities, because there is a chance of breaking coupled functionality when changes are made in o of them. That will require another round of testing to avoid any surprise on the production environment.

## Open/Closed Principle

**Definition:**  Classes, methods or functions should be Open tofor extension (new functionality) and Closed tofor modification.  
**ain goal:**  o prevent someone from changing already tried and tested code and allows the system to be open  extension through the use of inheritance, or interfaces. The main idea of this principle is to keep existing code from breaking when you implement new features.

**What does Open to Extension mean?**
This statement means that when a class is been designed the ideia of that new funcionalities can be added as new requirements are generated must be considered. 

**What does Closed to Modification mean?**
The statement **closed to extension** means that once a class is developed and tested this class should not be modified anymore, exept to correct bugs.

Generally extension can be achieved by using abstractions for dependencies, such as abstract classes and interfaces rather than using concrete classes.


## Liskov Substitution Principle

When extending a class, the subclass (the one which inherits a base class), should be able to be passed in place of objects of
the parent class without breaking the client code. Meaning that the subclass should remain compatible with the behavior of the superclass. 

**Don't ask if some class "is a" other class, Instead prefer ask _Does the classA fully substitute the classB _**

**One Use Very Important of Liskov Substitution Principle**
This concept  is critical when developing libraries and frameworks because the classes are going to be used by other people whose code cannot directly be accessed and changed.

### Liskov Substitution Requirements
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

### Exemplos of non-adherence of Liskov Substitution Principle

#### Verify for a specific type 
The below code snippet receives a set of taks and set the status of each of them to "in progress", except for bug fix that must first be initialized before assuming any status;

```java
for (Taks t: tasks){
	if(t instanceof BugFix){
		BugFix bf = (BugFix) t;
		bf.initializeBugDescription();
	}
    t.setInProgress();
}
```
This kind of approach where for most subtypes, one thing is done, but for particular subtypes something else must be performed. It indicates that the subtypes cannot be fully replace by its base class. In this situation inheritance are not been used properly 

**Solution:** Apply the principle "tell, don't ask"
```java
Class BugFix Extends Taks {
	
	@Override
	public void setInProgress()
    	this.initializeBugDescription();
	    super;setInProgress();

} 
// new for loop
for (Taks t: tasks){
    t.setInProgress();
}

```

## Interface Segregation Principle
The principle Interface Segregation states that **a class should not be forced to depend on methods it does not use**. Meaning that any classes that implement an interface, should not have "dummy" implementations of any methods defined in the interface. Instead, **large interfaces should be splited into smaller generalizations**. If it is not possible use the design pattern Adapter.

* A class should not be forced to depend on methods it does not use
* Interfaces should be split up in such a way that it can properly describe the separate functionalities of your system


### Dependency Inversion Principle
This principle states that high level modules should depend on high level generalizations, and not on low level details. Meaning that classes if will there dependencies they should depend on a interface or abstract class rathar than concreate classes. If clients are dependent on higher-level generalizations then low level implementations can be changed or replaced with more ease later on. This is a form of looser coupling.

Also, dependency inversion helps in the generalization of the behavior of your concrete classes into abstract classes and interfaces


## References
http://www.blackwasp.co.uk/lsp.aspx

https://stackoverflow.com/questions/56860/what-is-an-example-of-the-liskov-substitution-principle

