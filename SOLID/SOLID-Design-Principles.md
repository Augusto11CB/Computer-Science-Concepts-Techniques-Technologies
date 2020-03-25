

# SOLID

## Single Responsibility Principal

**Definition:**  There should not be more than one reason for a class to change, or  **a class should always handle single functionality**.

**Main goal:**  To avoid introducing coupling between functionalities, because there is a chance of breaking coupled functionality when changes are made in of of them. That will require another round of testing to avoid any surprise on the production environment.

## Open Closed

**Definition:**  Classes, methods or functions should be Open for extension (new functionality) and Closed for modification.  
**Main goal:**  To prevent someone from changing already tried and tested code.

## Liskov Substitution Principle

When extending a class, the subclass (the one which inherits a base class), should be able to be passed in place of objects of
the parent class without breaking the client code. Meaning that the subclass should remain compatible with the behavior of the superclass. 

**One Use Very Important of Liskov Substitution Principle**
This concept  is critical when developing libraries and frameworks because the classes are going to be used by other people whose code cannot directly be accessed and changed.

### Liskov Substitution Requirements
* **A subclass shouldn’t strengthen pre-conditions**
A subclass shouldn’t strengthen pre-conditions. That is, a subclass shouldn’t strengthen pre-conditions.  
**Example:**  Before calling a method that reads from a database you may need to satisfy the precondition that the database connection is open. If the subclass add more conditions, there is a viollation of the principle

* **A subclass shouldn’t strengthen pre-conditions**
A subclass shouldn’t strengthen pre-conditions. This means that the subclass should cause the state of the program to be in the same state as the base class after a method call.
**Example:**  After calling a method that reads from a database it may be assumed that the database connection is closed after executing a SQL statement. If the subclass remove the condition of close the database conection, there is a viollation of the principle.

**Contextualizingwith an Example - By Uncle Bob**
> In mathematics, a **Square** is a **Rectangle**. Indeed it is a specialization of a rectangle. The **"is a"** makes you want to model this with inheritance. However if in code you made **Square** derive from **Rectangle**, then a **Square** should be usable anywhere you expect a **Rectangle**. This makes for some strange behavior.
> Imagine you had **SetWidth** and **SetHeight** methods on your **Rectangle** base class; this seems perfectly logical. However if your **Rectangle** reference pointed to a **Square**, then **SetWidth** and **SetHeight** doesn't make sense because setting one would change the other to match it. In this case **Square** fails the Liskov Substitution Test with Rectangle and the abstraction of having Square inherit from Rectangle is a bad one.

**Comments** - Requirements this example does not respect
	*  A subclass shouldn’t strengthen pre-conditions, because if you set a **Square**, immediatly you are saying that witdth and height must be the same, and it is not considered by the superclass, thus here we have a viollation.

## References
http://www.blackwasp.co.uk/lsp.aspx
https://stackoverflow.com/questions/56860/what-is-an-example-of-the-liskov-substitution-principle

