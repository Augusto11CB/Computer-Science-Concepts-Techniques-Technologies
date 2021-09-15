## The Object Model

> Object model is the collection of principles that form the foundation of object-oriented design; a software engineering paradigm emphasizing the principles of abstraction, encapsulation, modularity, hierarchy, typing, concurrency, and persistence.

### Objects Definition
- Stefik and Bobrow define objects as "entities that combine the properties of procedures and data since they perform computations and save local state".
- Objects serve to unify the ideas of algorithmic and data abstraction.
- There exist invariant properties that characterize an object and its behavior.
    -  "An elevator, for example, is characterized by invariant properties including [that] it only travels up and down inside its shaft. Any elevator simulation must incorporate these invariants, for they are integral to the notion of an elevator"

### Object-Oriented Programming
> Object-oriented programming is a method of implementation in which **programs are organized as cooperative collections of objects**, each of which represents an instance of some class, and whose classes are all members of a hierarchy of classes united via inheritance relationships.

- Object-oriented programming uses objects, not algorithms, as its fundamental logical building blocks.
- Each object is an instance of some class.
- Classes may be related to one another via inheritance relationships.

### Object-Oriented Language - Features
A language is object-oriented if and only if it satisfies the following requirements:
- **It supports objects that are data abstractions with an interface of named operations and a hidden local state.**
- Objects have an associated type [class].
- Types [classes] may inherit attributes from supertypes [superclasses].

### Object-Oriented Design
> Object-oriented design is a method of design encompassing the process of object-oriented decomposition and a notation **for depicting** both logical and physical as well as static and dynamic models of the system under design.

- object-oriented design leads to an object-oriented decomposition
- **uses different notations to express different models of the logical (class and object structure) and physical (module** and process architecture) design of a system, in addition to the static and dynamic aspects of the system.


### Object-Oriented Analysis
- Object-oriented analysis (OOA) emphasizes the building of real-world models, using an object-oriented view of the world:

> Object-oriented analysis is a method of analysis that **examines requirements from the perspective of the classes and objects found in the vocabulary of the problem domain.**

### How are OOA, OOD, and OOP related?
The products of **object-oriented analysis serve as the models from which an object-oriented design can be started**. The products of object-oriented design can then be used as blueprints for completely implementing a system using object-oriented programming method


### Elements Object Model
1. Abstraction
2. Encapsulation
3. Modularity
4. Hierarchy

### Abstraction
> An abstraction denotes the essential characteristics of an object that distinguish it from all other kinds of objects and thus provide crisply defined conceptual boundaries, relative to the perspective of the viewer.

- An abstraction focuses on the outside view of an object and so serves to separate an object's essential behavior from its implementation
- Abstraction barrier is achieved by applying the principle of least commitment, through which the interface of an object provides its essential behavior, and nothing more.


From the most to the least useful, these kinds of abstractions include the following:

- **Entity abstraction**
    - An object that represents a useful model of a problem domain or solution domain entity
- **Action abstraction**
    - An object that provides a generalized set of operations, all of which perform the same kind of function
- **Virtual machine abstraction**
    - An object that groups operations that are all used by some superior level of control, or operations that all use some junior-level set of operations
image	
- **Coincidental abstraction**
    - An object that packages a set of operations that have no relation to each other


#### Behavior of an object & Contract Model Of Programming - Definition
- The behavior of an object can be characterized by considering the services that it provides to other objects, as well as the operations that it may perform on other objects. 

> Contract Model Of Programming states that the outside view of each object defines a contract on which other objects may depend, and which in turn must be carried out by the inside view of the object itself (often in collaboration with other objects).

- Contract Model encompasses the responsibilities of an object, namely, the behavior for which it is held accountable.

#### Protocol of an Object
> The ways in which an object may act and react, constituting the entire static and dynamic outside view of the object. The protocol of an object defines the envelope of the object's allowable behavior.

#### Invariant 
- Central to the idea of an abstraction is the concept of invariance
- For each operation associated with an object, we may define preconditions (invariants assumed by the operation) as well as postconditions (invariants satisfied by the operation). Violating an invariant breaks the contract associated with an abstraction.

#### Conclusion Abstraction 
The design decisions about how objects cooperate with one another define the boundaries of each abstraction and thus the responsibilities and protocol of each object.

### Encapsulation
- Abstraction and encapsulation are complementary concepts
    - Abstraction: It focuses on the observable behavior of an object
    - Encapsulation: It focuses on the implementation that gives rise to this behavior. 

> No part of a complex system should depend on the internal details of any other part
> Ingalls, D. The Smalltalk-76 Programming System Design and Implementation. Proceedings of the Fifth Annual ACM Symposium on Principles of Programming Languages. ACM, p. 9.

> Encapsulation is most often achieved through information hiding (not just data hiding), which is the process of hiding all the secrets of an object that do not contribute to its essential characteristics; typically, the structure of an object is hidden, as well as the implementation of its methods.
> Booch, G. et al. Object-Oriented Analysis and Design with Applications 

> Encapsulation is the process of **compartmentalizing the elements of an abstraction that constitute its structure and behavior**; **encapsulation serves to separate the contractual interface of an abstraction and its implementation**.
> Booch, G. et al. Object-Oriented Analysis and Design with Applications 

> - Intelligent encapsulation localizes design decisions that are likely to change. 
> - The ability to change the representation of an abstraction without disturbing any of its clients is the essential benefit of encapsulation
> Booch, G. et al. Object-Oriented Analysis and Design with Applications 

 #### Implementation of a Class - Definition 
 > The implementation of a class comprises the representation of the abstraction as well as the mechanisms that achieve the desired behavior.
 > Booch, G. et al. Object-Oriented Analysis and Design with Applications 

### Modularity
