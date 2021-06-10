# Principle of Least Knowledge
A class should be designed so that it does not need to know about and depend upon almost every other class in the system. This approach avoids increasing coupling and turn hard the maintenance. By limiting which classes communicate with each other, the principle of least knowledge is enforced.

## Law of Demeter
This law define how classes should interact with each other, the should not have access to the entire system because it causes a high degrre of couplin.
A classes should know about and interact with as few other classes as possible. This means that any class should only communicate with its immediate friends. These friends would be other classes that one class should only know about.

**Goal:** THis design principle focuses more broadly on how methods call shoud be made.

#### Rule #1 
A method, M, in an object, O, can call on any other method within O itself.

#### Rule #2 
A method, M, can call the methods of any parameter P.

#### Rule #3 
A method, M, can call a method, N, of an object, I, If I is instantiated within M.

#### Rule #4 
A method, M, in object O, can invoke methods of any type of object that is a direct component of O.

### Summary of Law of Demeter
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

